---
title: Relatórios de Serviço de Integridade
ms.prod: windows-server
manager: eldenc
ms.author: cosdar
ms.technology: storage-health-service
ms.topic: article
author: cosmosdarwin
ms.date: 10/05/2017
ms.openlocfilehash: 3b47e1abf3805b7e6e3dc180d5d937ddb2723fa4
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80827539"
---
# <a name="health-service-reports"></a>Relatórios de Serviço de Integridade
> Aplica-se a: Windows Server 2019, Windows Server 2016

## <a name="what-are-reports"></a>O que são relatórios  

O Serviço de Integridade reduz o trabalho necessário para obter informações de desempenho e capacidade ao vivo de seu cluster Espaços de Armazenamento Diretos. Um novo cmdlet fornece uma lista organizada de métricas essenciais, que são coletadas com eficiência e agregadas dinamicamente entre os nós, com lógica interna para detectar a associação do cluster. Todos os valores são apenas pontuais e em tempo real.  

## <a name="usage-in-powershell"></a>Uso no PowerShell

Use este cmdlet para obter métricas para todo o cluster de Espaços de Armazenamento Diretos:

```PowerShell
Get-StorageSubSystem Cluster* | Get-StorageHealthReport
```

O parâmetro de **contagem** opcional indica quantos conjuntos de valores retornar, em intervalos de um segundo.  

```PowerShell
Get-StorageSubSystem Cluster* | Get-StorageHealthReport -Count <Count>  
```

Você também pode obter métricas para um volume ou servidor específico:  

```PowerShell
Get-Volume -FileSystemLabel <Label> | Get-StorageHealthReport -Count <Count>  

Get-StorageNode -Name <Name> | Get-StorageHealthReport -Count <Count>
```

## <a name="usage-in-net-and-c"></a>Uso no .NET eC#

### <a name="connect"></a>Conectar

Para consultar o Serviço de Integridade, será necessário estabelecer um **CimSession** com o cluster. Para fazer isso, você precisará de algumas coisas que estão disponíveis apenas no .NET completo, o que significa que não é possível fazer isso prontamente diretamente de um aplicativo Web ou móvel. Esses exemplos de código usarão o C\#, a opção mais direta para essa camada de acesso a dados.

``` 
...
using System.Security;
using Microsoft.Management.Infrastructure;

public CimSession Connect(string Domain = "...", string Computer = "...", string Username = "...", string Password = "...")
{
    SecureString PasswordSecureString = new SecureString();
    foreach (char c in Password)
    {
        PasswordSecureString.AppendChar(c);
    }

    CimCredential Credentials = new CimCredential(
        PasswordAuthenticationMechanism.Default, Domain, Username, PasswordSecureString);
    WSManSessionOptions SessionOptions = new WSManSessionOptions();
    SessionOptions.AddDestinationCredentials(Credentials);
    Session = CimSession.Create(Computer, SessionOptions);
    return Session;
}
```

O nome de usuário fornecido deve ser um administrador local do computador de destino.

É recomendável que você construa a **SecureString** de senha diretamente da entrada do usuário em tempo real, para que sua senha nunca seja armazenada na memória em texto não criptografado. Isso ajuda a atenuar uma variedade de questões de segurança. Mas, na prática, construí-lo como acima é comum para fins de criação de protótipos.

### <a name="discover-objects"></a>Descobrir objetos

Com o **CimSession** estabelecido, você pode consultar Instrumentação de gerenciamento do Windows (WMI) no cluster.

Antes que você possa obter falhas ou métricas, você precisará obter instâncias de vários objetos relevantes. Primeiro, o **MSFT\_StorageSubSystem** que representa espaços de armazenamento diretos no cluster. Usando isso, você pode obter cada **msft\_StorageNode** no cluster e todos os\_de dados do **MSFT** Por fim, você precisará do **MSFT\_StorageHealth**, o serviço de integridade em si.

```
CimInstance Cluster;
List<CimInstance> Nodes;
List<CimInstance> Volumes;
CimInstance HealthService;

public void DiscoverObjects(CimSession Session)
{
    // Get MSFT_StorageSubSystem for Storage Spaces Direct
    Cluster = Session.QueryInstances(@"root\microsoft\windows\storage", "WQL", "SELECT * FROM MSFT_StorageSubSystem")
        .First(Instance => (Instance.CimInstanceProperties["FriendlyName"].Value.ToString()).Contains("Cluster"));

    // Get MSFT_StorageNode for each cluster node
    Nodes = Session.EnumerateAssociatedInstances(Cluster.CimSystemProperties.Namespace,
        Cluster, "MSFT_StorageSubSystemToStorageNode", null, "StorageSubSystem", "StorageNode").ToList();

    // Get MSFT_Volumes for each data volume
    Volumes = Session.EnumerateAssociatedInstances(Cluster.CimSystemProperties.Namespace,
        Cluster, "MSFT_StorageSubSystemToVolume", null, "StorageSubSystem", "Volume").ToList();

    // Get MSFT_StorageHealth itself
    HealthService = Session.EnumerateAssociatedInstances(Cluster.CimSystemProperties.Namespace,
        Cluster, "MSFT_StorageSubSystemToStorageHealth", null, "StorageSubSystem", "StorageHealth").First();
}
```

Esses são os mesmos objetos que você obtém no PowerShell usando cmdlets como **Get-StorageSubSystem**, **Get-StorageNode**e **Get-volume**.

Você pode acessar todas as mesmas propriedades, documentadas em [classes de API de gerenciamento de armazenamento](https://msdn.microsoft.com/library/windows/desktop/hh830612(v=vs.85).aspx).

```
...
using System.Diagnostics;

foreach (CimInstance Node in Nodes)
{
    // For illustration, write each node's Name to the console. You could also write State (up/down), or anything else!
    Debug.WriteLine("Discovered Node " + Node.CimInstanceProperties["Name"].Value.ToString());
}
```

Invoque **GetReport** para começar a transmitir amostras de uma lista de métricas essenciais, que são coletadas com eficiência e agregadas dinamicamente entre os nós, com lógica interna para detectar a associação do cluster. Os exemplos chegarão a cada segundo daí em diante. Todos os valores são apenas pontuais e em tempo real.

As métricas podem ser transmitidas para três escopos: o cluster, qualquer nó ou qualquer volume.

A lista completa de métricas disponíveis em cada escopo no Windows Server 2016 está documentada abaixo.

### <a name="iobserveronnext"></a>IObserver. OnNext ()

Este código de exemplo usa o [padrão de design do observador](https://msdn.microsoft.com/library/ee850490(v=vs.110).aspx) para implementar um observador cujo método **OnNext ()** será invocado quando cada nova amostra de métricas chegar. Seu método **OnCompleted ()** será chamado se/quando o streaming terminar. Por exemplo, você pode usá-lo para reiniciar o streaming e, portanto, continua indefinidamente.

```
class MetricsObserver<T> : IObserver<T>
{
    public void OnNext(T Result)
    {
        // Cast
        CimMethodStreamedResult StreamedResult = Result as CimMethodStreamedResult;

        if (StreamedResult != null)
        {
            // For illustration, you could store the metrics in this dictionary
            Dictionary<string, string> Metrics = new Dictionary<string, string>();

            // Unpack
            CimInstance Report = (CimInstance)StreamedResult.ItemValue;
            IEnumerable<CimInstance> Records = (IEnumerable<CimInstance>)Report.CimInstanceProperties["Records"].Value;
            foreach (CimInstance Record in Records)
            {
                /// Each Record has "Name", "Value", and "Units"
                Metrics.Add(
                    Record.CimInstanceProperties["Name"].Value.ToString(),
                    Record.CimInstanceProperties["Value"].Value.ToString()
                    );
            }

            // TODO: Whatever you want!
        }
    }
    public void OnError(Exception e)
    {
        // Handle Exceptions
    }
    public void OnCompleted()
    {
        // Reinvoke BeginStreamingMetrics(), defined in the next section
    }
}
```

### <a name="begin-streaming"></a>Iniciar streaming

Com o observador definido, você pode iniciar o streaming.

Especifique o **CimInstance** de destino para o qual você deseja que as métricas sejam escopos. Pode ser o cluster, qualquer nó ou qualquer volume.

O parâmetro de contagem é o número de amostras antes de o streaming terminar.

```
CimInstance Target = Cluster; // From among the objects discovered in DiscoverObjects()

public void BeginStreamingMetrics(CimSession Session, CimInstance HealthService, CimInstance Target)
{
    // Set Parameters
    CimMethodParametersCollection MetricsParams = new CimMethodParametersCollection();
    MetricsParams.Add(CimMethodParameter.Create("TargetObject", Target, CimType.Instance, CimFlags.In));
    MetricsParams.Add(CimMethodParameter.Create("Count", 999, CimType.UInt32, CimFlags.In));
    // Enable WMI Streaming
    CimOperationOptions Options = new CimOperationOptions();
    Options.EnableMethodResultStreaming = true;
    // Invoke API
    CimAsyncMultipleResults<CimMethodResultBase> InvokeHandler;
    InvokeHandler = Session.InvokeMethodAsync(
        HealthService.CimSystemProperties.Namespace, HealthService, "GetReport", MetricsParams, Options
        );
    // Subscribe the Observer
    MetricsObserver<CimMethodResultBase> Observer = new MetricsObserver<CimMethodResultBase>(this);
    IDisposable Disposeable = InvokeHandler.Subscribe(Observer);
}
```

Não é necessário dizer que essas métricas podem ser visualizadas, armazenadas em um banco de dados ou usadas de qualquer modo que você veja.

### <a name="properties-of-reports"></a>Propriedades de relatórios

Cada exemplo de métricas é um "relatório" que contém muitos "registros" correspondentes a métricas individuais.

Para o esquema completo, inspecione as classes **msft\_StorageHealthReport** e **MSFT\_HealthRecord** no *storagewmi. mof*.

Cada métrica tem apenas três propriedades, por esta tabela.

| **Propriedade** | **Exemplo**       |
| -------------|-------------------|
| {1&gt;Nome&lt;1}         | IOLatencyAverage  |
| {1&gt;Valor&lt;1}        | 0, 21           |
| Unidades        | 3                 |

Units = {0, 1, 2, 3, 4}, em que 0 = "bytes", 1 = "BytesPerSecond", 2 = "CountPerSecond", 3 = "Seconds" ou 4 = "Percentage".

## <a name="coverage"></a>Cobertura

Abaixo estão as métricas disponíveis para cada escopo no Windows Server 2016.

### <a name="msft_storagesubsystem"></a>MSFT_StorageSubSystem

| **Nome**                        | **Unit** |
|---------------------------------|-----------|
| Os                        | 4         |
| CapacityPhysicalPooledAvailable | 0         |
| CapacityPhysicalPooledTotal     | 0         |
| CapacityPhysicalTotal           | 0         |
| CapacityPhysicalUnpooled        | 0         |
| CapacityVolumesAvailable        | 0         |
| CapacityVolumesTotal            | 0         |
| IOLatencyAverage                | 3         |
| IOLatencyRead                   | 3         |
| IOLatencyWrite                  | 3         |
| IOPSRead                        | 2         |
| IOPSTotal                       | 2         |
| IOPSWrite                       | 2         |
| IOThroughputRead                | 1         |
| IOThroughputTotal               | 1         |
| IOThroughputWrite               | 1         |
| MemoryAvailable                 | 0         |
| MemoryTotal                     | 0         |


### <a name="msft_storagenode"></a>MSFT_StorageNode

| **Nome**            | **Unit** |
|---------------------|-----------|
| Os            | 4         |
| IOLatencyAverage    | 3         |
| IOLatencyRead       | 3         |
| IOLatencyWrite      | 3         |
| IOPSRead            | 2         |
| IOPSTotal           | 2         |
| IOPSWrite           | 2         |
| IOThroughputRead    | 1         |
| IOThroughputTotal   | 1         |
| IOThroughputWrite   | 1         |
| MemoryAvailable     | 0         |
| MemoryTotal         | 0         |

### <a name="msft_volume"></a>MSFT_Volume

| **Nome**            | **Unit** |
|---------------------|-----------|
| CapacityAvailable   | 0         |
| CapacityTotal       | 0         |
| IOLatencyAverage    | 3         |
| IOLatencyRead       | 3         |
| IOLatencyWrite      | 3         |
| IOPSRead            | 2         |
| IOPSTotal           | 2         |
| IOPSWrite           | 2         |
| IOThroughputRead    | 1         |
| IOThroughputTotal   | 1         |
| IOThroughputWrite   | 1         |

## <a name="see-also"></a>Consulte também

- [Serviço de Integridade no Windows Server 2016](health-service-overview.md)
