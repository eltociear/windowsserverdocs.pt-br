---
title: Evntcmd
description: Tópico de comandos do Windows para * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: c1aabb74-76e7-4304-95a6-50ad87e92fd9
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 86e4290543ffcc0da1c768a661fd88a7638b1146
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80845009"
---
# <a name="evntcmd"></a>Evntcmd

>Aplicável a: Windows Server (canal semestral), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Configura a conversão de eventos em interceptações, destinos de interceptação ou ambos com base nas informações de um arquivo de configuração.   
## <a name="syntax"></a>Sintaxe  
```  
evntcmd [/s <computerName>] [/v <verbosityLevel>] [/n] <FileName>  
```  
#### <a name="parameters"></a>Parâmetros  

|      Parâmetro      |                                                                                                                                                            Descrição                                                                                                                                                             |
|---------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|  /s <computerName>  |                                                         Especifica, por nome, o computador no qual você deseja configurar a tradução de eventos para interceptações, destinos de interceptação ou ambos. Se você não especificar um computador, a configuração ocorrerá no computador local.                                                          |
| /v <verbosityLevel> | Especifica quais tipos de mensagens de status aparecem como interceptações e destinos de interceptação são configurados. Esse parâmetro deve ser um inteiro entre 0 e 10. Se você especificar 10, todos os tipos de mensagens serão exibidos, incluindo mensagens de rastreamento e avisos sobre se a configuração de interceptação foi bem-sucedida. Se você especificar 0, nenhuma mensagem será exibida. |
|         /n          |                                                                                                           Especifica que o serviço SNMP não deve ser reiniciado se este computador receber alterações de configuração de interceptação.                                                                                                            |
|     <FileName>      |                                                                                     Especifica, por nome, o arquivo de configuração que contém informações sobre a tradução de eventos para interceptações e destinos de interceptação que você deseja configurar.                                                                                     |
|         /?          |                                                                                                                                                Exibe a ajuda no prompt de comando.                                                                                                                                                |

## <a name="remarks"></a>Comentários  
- Se você quiser configurar interceptações, mas não os destinos de interceptação, poderá criar um arquivo de configuração válido usando o conversor de evento para interceptação, que é um utilitário gráfico. Se você tiver o serviço SNMP instalado, poderá iniciar o conversor de evento para interceptação digitando **evntwin** em um prompt de comando. Depois de definir as interceptações desejadas, clique em exportar para criar um arquivo adequado para uso com o **evntcmd**. Você pode usar o conversor de evento para interceptação para criar facilmente um arquivo de configuração e, em seguida, usar o arquivo de configuração com **evntcmd** no prompt de comando para configurar rapidamente os desvios em vários computadores.  
- A sintaxe para configurar uma interceptação é a seguinte:  
  **#pragma adicionar**<em><EventLogFile> <EventSource> <EventID> [<Count> [<Period>]]</em>  
  -   O texto **#pragma** deve aparecer no início de cada entrada no arquivo.  
  -   O parâmetro **Add** especifica que você deseja adicionar um evento à configuração de interceptação.  
  -   Os parâmetros *eventlogfile*, *EventSource*e *EventID* são obrigatórios. O parâmetro *eventlogfile* especifica o arquivo no qual o evento é registrado. O parâmetro *EventSource* especifica o aplicativo que gera o evento. O parâmetro *EventID* especifica o número exclusivo que identifica cada evento. Para descobrir quais valores correspondem a eventos específicos, inicie o evento para o conversor de interceptação digitando **evntwin** em um prompt de comando. Clique em **personalizado**e em **Editar**. Em **origens do evento**, procure as pastas até localizar o evento que deseja configurar, clique nele e, em seguida, clique em **Adicionar**. As informações sobre a origem do evento, o arquivo de log de eventos e a ID do evento aparecem em **origem, log**e **ID específica da interceptação**, respectivamente.  
  -   O parâmetro *Count* é opcional e especifica quantas vezes o evento deve ocorrer antes que uma mensagem de interceptação seja enviada. Se você não usar o parâmetro *Count* , a mensagem de interceptação será enviada depois que o evento ocorrer uma vez.  
  -   O parâmetro *period* é opcional, mas exige que você use o parâmetro *Count* . O parâmetro *period* especifica um período de tempo (em segundos) durante o qual o evento deve ocorrer o número de vezes especificado com o parâmetro Count antes que uma mensagem de interceptação seja enviada. Se você não usar o parâmetro *period* , uma mensagem de interceptação será enviada depois que o evento ocorrer o número de vezes especificado com o parâmetro *Count* , independentemente da quantidade de tempo decorrido entre ocorrências.  
- A sintaxe para remover uma interceptação é a seguinte:  
  **#pragma excluir**<em><EventSource> <EventLogFile> <EventID></em>  
  -   O texto **#pragma** deve aparecer no início de cada entrada no arquivo.  
  -   A *exclusão* do parâmetro especifica que você deseja remover um evento para a configuração de interceptação.  
  -   Os parâmetros *eventlogfile*, *EventSource*e *EventID* são obrigatórios. O parâmetro *eventlogfile* especifica o log no qual o evento é registrado. O parâmetro *EventSource* especifica o aplicativo que gera o evento. O parâmetro *EventID* especifica o número exclusivo que identifica cada evento.  
- A sintaxe para configurar um destino de interceptação é a seguinte:  
  **#pragma add_TRAP_DEST**<em><CommunityName> <HostID></em>  
  -   O texto **#pragma** deve aparecer no início de cada entrada no arquivo.  
  -   O parâmetro **add_TRAP_DEST** especifica que você deseja que as mensagens de interceptação sejam enviadas para um host especificado em uma comunidade.  
  -   O parâmetro *communityname* especifica, por nome, a Comunidade na qual as mensagens de interceptação são enviadas.  
  -   O parâmetro *hostid* especifica, por nome ou endereço IP, o host para o qual você deseja que as mensagens de interceptação sejam enviadas.  
- A sintaxe para remover um destino de interceptação é a seguinte:  
  **#pragma delete_TRAP_DEST**<em><CommunityName> <HostID></em>  
  - O texto **#pragma** deve aparecer no início de cada entrada no arquivo.  
  - O parâmetro *delete_TRAP_DEST* especifica que você não deseja que as mensagens de interceptação sejam enviadas a um host especificado em uma comunidade.  
  - O parâmetro *communityname* especifica, por nome, a Comunidade na qual as mensagens de interceptação são enviadas.  
  - O parâmetro *hostid* especifica, por nome ou endereço IP, o host para o qual você não deseja que as mensagens de interceptação sejam enviadas.  
    ## <a name="examples"></a><a name=BKMK_Examples></a>Disso  
    Os exemplos a seguir ilustram as entradas no arquivo de configuração para o comando **evntcmd** . Eles não são projetados para serem digitados em um prompt de comando.  
    Para enviar uma mensagem de interceptação se o serviço log de eventos for reiniciado, digite:  
    ```  
    #pragma add System Eventlog 2147489653  
    ```  
    Para enviar uma mensagem de interceptação se o serviço log de eventos for reiniciado duas vezes em três minutos, digite:  
    ```  
    #pragma add System Eventlog 2147489653 2 180  
    ```  
    Para interromper o envio de uma mensagem de interceptação sempre que o serviço de log de eventos for reiniciado, digite:  
    ```  
    #pragma delete System Eventlog 2147489653  
    ```  
    Para enviar mensagens de interceptação na Comunidade denominada public para o host com o endereço IP 192.168.100.100, digite:  
    ```  
    #pragma add_TRAP_DEST public 192.168.100.100  
    ```  
    Para enviar mensagens de interceptação na Comunidade denominada particular para o host chamado Host1, digite:  
    ```  
    #pragma add_TRAP_DEST private Host1  
    ```  
    Para interromper o envio de mensagens de interceptação na comunidade chamada particular para o mesmo computador em que você está configurando destinos de interceptação, digite:  
    ```  
    #pragma delete_TRAP_DEST private localhost  
    ```  
    ## <a name="additional-references"></a>Referências adicionais  
- - [Chave da sintaxe de linha de comando](command-line-syntax-key.md)  
