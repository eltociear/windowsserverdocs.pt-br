---
title: Data center definido por software do Windows Server
Description: Visão geral do Windows Server SDDC
ms.prod: windows-server
ms.technology: SDDC
ms.topic: get-started article
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 06/04/2019
ms.localizationpriority: medium
ms.openlocfilehash: 5a90ad13a51a540c6c76adacb7df0225d642573a
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80857189"
---
# <a name="windows-server-software-defined-datacenter"></a>Datacenter definido por software do Windows Server

>Aplica-se a: Windows Server 2019, Windows Server 2016

![](media/sddc/heading.png)

## <a name="what-is-windows-server-software-defined-datacenter"></a>O que é o datacenter definido por software do Windows Server?

O SDDC (datacenter definido por software) é um termo comum no setor, que geralmente se refere a um Datacenter em que a infraestrutura inteira é virtualizada. A virtualização é a chave e significa simplesmente que o hardware e o software no datacenter se expandem além de uma proporção de um para um tradicional. Com um hardware de emulação de hipervisor de software, é possível abstrair sistemas operacionais e aplicativos do hardware físico e multiplicar para formar grupos de recursos elásticos de processadores, memória, E/S e redes.
 
A implementação do SDDC da Microsoft consiste nas tecnologias do Windows Server destacadas neste artigo. Começa com o hipervisor do Hyper-V que fornece a plataforma de virtualização na qual a rede e o armazenamento são criados. As tecnologias de segurança, desenvolvidas para desafios específicos da infraestrutura virtualizada, reduzem as ameaças internas e externas. Com o PowerShell integrado ao Windows Server e a adição do [System Center](https://docs.microsoft.com/system-center/) e/ou do [Operations Management Suite](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview), você pode programar e automatizar o provisionamento, a implantação, a configuração e o gerenciamento.

As tecnologias integradas ao Windows Server e ao System Center são as principais bases da experiência do Windows Server SDDC. Porém, mesmo que seja uma plataforma virtualizada, ela ainda requer o hardware adequado. Os parceiros da Microsoft participando dos programas **Soluções WSSD (Definidas por Software do Windows Server)** e **Soluções do Azure Stack HCI** podem ajudar sua empresa a adquirir o hardware adequado, instalá-lo e executá-lo desde o primeiro dia.

![](media/sddc/video.png) **[Assista ao vídeo para saber mais sobre o SDDC da Microsoft](https://mva.microsoft.com/training-courses/whats-new-in-windows-server-2016-16457?l=YcsJR6sXC_1006218965)**

![](media/sddc/poster-ico.png) **[Baixe um arquivo .pdf de tamanho de pôster desta página](https://github.com/MicrosoftDocs/windowsserverdocs/blob/master/WindowsServerDocs/media/sddc/sddc_poster_0801417_ANSI-E.pdf)**

![](media/sddc/spacer1.png)<a href="https://github.com/MicrosoftDocs/windowsserverdocs/blob/master/WindowsServerDocs//media/sddc/sddc_poster_0801417_ANSI-E.pdf"><img src="media/sddc/poster.png"></a>

## <a name="azure-stack-hci-solutions"></a>Soluções do Azure Stack HCI

Criar seu datacenter definido por software do Windows Server na infraestrutura de hardware adequada é a primeira etapa essencial para o sucesso. É por isso que fizemos uma parceria com 15 parceiros para criar designs de SDDC e práticas recomendadas validadas pela Microsoft para implantação.

Os parceiros da Microsoft oferecem uma matriz de soluções que funcionam com o Windows Server 2019 por meio do programa do Azure Stack HCI e do Microsoft Server 2016 por meio do programa WSSD (definido por software do Windows Server) para fornecer uma infraestrutura de rede e armazenamento de alto desempenho e hiperconvergente. As soluções hiperconvergentes unem a computação, o armazenamento e a rede em servidores padrão do setor e os componentes para aprimorar a inteligência e o controle do datacenter.

![](media/sddc/learn.png) **[Saiba mais sobre as Soluções Azure Stack HCI](https://azure.microsoft.com/overview/azure-stack/hci)**

![](media/sddc/learn.png) **[Saiba mais sobre as soluções WSSD](https://www.microsoft.com/cloud-platform/software-defined-datacenter)**

## <a name="windows-server-virtualized-technologies"></a>Tecnologias virtualizadas do Windows Server ##

O restante deste tópico lista as tecnologias do Windows Server SDDC e fornece links para a documentação de cada uma. As tecnologias são listadas na tabela abaixo:

![](media/sddc/table.png)

![](media/sddc/virtualize.png)

### <a name="windows-server-hyper-converged"></a>Windows Server hiperconvergente

As tecnologias de virtualização do Windows Server incluem atualizações ao Hyper-V, ao Comutador Virtual do Hyper-V, à Malha Protegida e a VMs (Máquinas Virtuais) Protegidas, que aprimorar a segurança, a escalabilidade e a confiabilidade. As atualizações de cluster de failover, rede e armazenamento facilitam ainda mais a implantação e o gerenciamento dessas tecnologias quando usadas com o Hyper-V.

![](media/sddc/spacer1.png)![](media/sddc/hyper-converged.png)

![](media/sddc/learn.png) **[Saiba mais sobre o Windows Server hiperconvergente](https://docs.microsoft.com/windows-server/get-started/what-s-new-in-windows-server-2016#computevirtualizationvirtualizationmd)**

### <a name="hyper-v-hypervisor"></a>Hipervisor do Hyper-V

O Hyper-V é uma tecnologia de virtualização com base em hipervisor para o Windows. O hipervisor é essencial para a virtualização. Ele é a plataforma de virtualização específica por processador que permite que vários sistemas operacionais isolados compartilhem uma única plataforma de hardware.

![](media/sddc/spacer1.png)![](media/sddc/hypervisor.png)

![](media/sddc/learn.png) **[Saiba mais sobre o Hipervisor do Hyper-V](https://www.microsoft.com/cloud-platform/server-virtualization)**

### <a name="guest-clustering-with-shared-vhdx"></a>Clustering de convidado com VHDX compartilhado

![](media/sddc/virtualize-line.png)

Flexível, seguro e não vinculado à topologia de armazenamento subjacente, o VHDX compartilhado elimina a necessidade de apresentar o armazenamento físico subjacente a um SO convidado. O novo VHDX compartilhado é compatível com o redimensionamento online.

![](media/sddc/spacer1.png)![](media/sddc/cluster.png)

- O VHDX compartilhado pode residir em um CSV (Volume Compartilhado Clusterizado) no armazenamento de bloco ou no armazenamento SMB com base em arquivos.
- Protegido: o VHDX compartilhado é compatível com a Réplica do Hyper-V e ao backup em nível de host.

![](media/sddc/learn.png) **[Saiba mais sobre o Clustering de convidado com VHDX compartilhado](https://technet.microsoft.com/library/dn281956(v=ws.11).aspx)**

### <a name="hyper-v-replica"></a>Réplica do Hyper-V

![](media/sddc/virtualize-line.png)

Replicação integrada de VM com base em software pela rede com certificados. Não está vinculada ao hardware de servidor, rede ou armazenamento em nenhum dos sites.

![](media/sddc/spacer1.png)![](media/sddc/replica.png)

Não requer outras tecnologias de replicação de máquina virtual, reduzindo os custos.
- Processa a migração dinâmica automaticamente.
- Gerenciamento e configuração simples: por meio do Gerenciador do Hyper-V, PowerShell ou com o Azure Site Recovery.

![](media/sddc/learn.png) **[Saiba mais sobre a Réplica do Hyper-V](https://docs.microsoft.com/windows-server/virtualization/hyper-v/manage/set-up-hyper-v-replica)**

![](media/sddc/networking.png)

### <a name="network-controller"></a>Controlador de rede

![](media/sddc/networking-line.png)

Um ponto centralizado e programável de automação para gerenciar, configurar, monitorar e solucionar problemas de infraestrutura de rede física e virtual em seu datacenter.

![](media/sddc/spacer1.png)![](media/sddc/netcontroller.png)

Os administradores usam uma Ferramenta de Gerenciamento que interage diretamente com o Controlador de Rede. O Controlador de Rede fornece informações sobre a infraestrutura de rede, incluindo a infraestrutura física e virtual para a Ferramenta de Gerenciamento.

![](media/sddc/learn.png) **[Saiba mais sobre o Controlador de Rede](https://docs.microsoft.com/windows-server/networking/sdn/technologies/network-controller/network-controller)**

### <a name="datacenter-firewall"></a>Firewall do Datacenter

![](media/sddc/networking-line.png)

Quando implantado e oferecido como um serviço, os administradores locatários podem instalar e configurar políticas de firewall para ajudar a proteger redes virtuais contra tráfego indesejado da Internet e redes de intranet.

![](media/sddc/spacer1.png)![](media/sddc/firewall.png)

O administrador do provedor de serviço ou o administrador de locatário pode gerenciar as políticas de Firewall do Datacenter usando o controlador de rede.

![](media/sddc/learn.png) **[Saiba mais sobre o Firewall do Datacenter](https://docs.microsoft.com/windows-server/networking/sdn/technologies/network-function-virtualization/datacenter-firewall-overview)**

### <a name="switch-embedded-teaming"></a>Agrupamento Incorporado de Comutador

![](media/sddc/networking-line.png)

O SET é uma solução alternativa de Agrupamento NIC que você pode usar em ambientes que incluem o Hyper-V e a pilha de [SDN (Rede Definida por Software)](https://docs.microsoft.com/windows-server/networking/sdn/software-defined-networking).

![](media/sddc/spacer1.png)![](media/sddc/teaming.png)

![](media/sddc/learn.png) **[Saiba mais sobre o Agrupamento Incorporado de Comutador](https://docs.microsoft.com/windows-server/networking/sdn/technologies/set-for-sdn)**

### <a name="software-load-balancing"></a>Balanceamento de carga do software

![](media/sddc/networking-line.png)

O SLB permite que vários servidores hospedem a mesma carga de trabalho, fornecendo alta disponibilidade e escalabilidade. Aumente os recursos de balanceamento de carga usando VMs de SLB nos mesmos servidores do Hyper-V que você usa para outras cargas de trabalho de VM. O SLB é compatível com a criação e a exclusão rápidas de pontos de extremidade de balanceamento de carga para operações de provedor de serviços de nuvem. O SLB é compatível com dezenas de gigabytes por cluster, fornece um modelo simples de provisionamento e é fácil de aumentar.

![](media/sddc/spacer1.png)![](media/sddc/balancer.png)

![](media/sddc/learn.png) **[Saiba mais sobre o Balanceamento de Carga de Software](https://docs.microsoft.com/windows-server/networking/sdn/technologies/network-function-virtualization/software-load-balancing-for-sdn)**


![](media/sddc/storage.png)

### <a name="storage-spaces-direct"></a>Espaços de Armazenamento Direct

![](media/sddc/storage-line.png)

Usando os servidores padrão do setor com unidades conectadas localmente, os Espaços de Armazenamento Diretos fornecem armazenamento definido pelo software altamente disponível e escalonável com custo menor do que o de matrizes de SAN ou NAS tradicionais. Sua arquitetura simplifica radicalmente a aquisição e a implantação.

![Cada nó tem unidades agrupadas no nível do cluster conectadas localmente por Espaços de Armazenamento Diretos acessado por VMs pelos CSVs](media/sddc/spacer1.png)![](media/sddc/ssd.png)

Os Espaços de Armazenamento Diretos introduzem o novo Barramento de Armazenamento de Software e aproveitam muitos dos recursos que você conhece hoje no Windows Server, como Clustering de Failover, CSVs (Volumes Compartilhados Clusterizados), Protocolo SMB 3 e os Espaços de Armazenamento.

![](media/sddc/learn.png) **[Saiba mais sobre os Espaços de Armazenamento Diretos](storage/storage-spaces/storage-spaces-direct-overview.md)**
### <a name="storage-quality-of-service"></a>Qualidade de serviço do armazenamento ###

![](media/sddc/storage-line.png)

Monitore e gerencie centralmente o desempenho de armazenamento de máquinas virtuais usando o Hyper-V e as funções de Servidor de Arquivos de Escalabilidade Horizontal, aprimorando a justiça de recursos de armazenamento entre diversas máquinas virtuais.

![](media/sddc/spacer1.png)![](media/sddc/qos.png)

A QoS do armazenamento é integrada na solução de armazenamento definida por software da Microsoft fornecida pelo Servidor de Arquivos de Escalabilidade Horizontal e pelo Hyper-V usando o protocolo SMB3. Um novo Gerenciador de Política oferece monitoramento de desempenho de armazenamento central.

![](media/sddc/learn.png) **[Saiba mais sobre a QoS de Armazenamento](https://docs.microsoft.com/windows-server/storage/storage-qos/storage-qos-overview)**

### <a name="storage-replica"></a>Réplica de Armazenamento


![](media/sddc/storage-line.png)

A preparação e a recuperação de desastres possibilitam que não haja nenhuma perda de dados, com a capacidade de proteger os dados de modo síncrono em diferentes racks, andares, edifícios, campus, cidades e países com uso mais eficiente de vários datacenters.

![](media/sddc/spacer1.png)
![](media/sddc/storage-replica.png)

Replicação síncrona

1. O aplicativo grava dados
2. Dados de log são gravados e os dados são replicados para o local remoto
3. Dados de log são gravados no local remoto
4. Confirmação do local remoto
5. Gravação de aplicativo confirmada

t e t1: dados liberados para o volume, logs sempre realizam gravação

![](media/sddc/learn.png) **[Saiba mais sobre Réplica de Armazenamento](https://docs.microsoft.com/windows-server/storage/storage-replica/storage-replica-overview)**

![](media/sddc/security.png)

### <a name="guarded-fabric"></a>Malha protegida

![](media/sddc/security-line.png)

Como um provedor de serviços de nuvem ou um administrador de nuvem privada corporativa, você pode usar uma malha protegida para fornecer um ambiente mais seguro para as VMs. Uma malha protegida consiste em um HGS (Serviço de Guardião de Host), em geral, um cluster de três nós, além de um ou mais hosts protegidos e um conjunto de VMs (máquinas virtuais) protegidas.

![](media/sddc/spacer1.png)![](media/sddc/guarded-fabric.png)

![](media/sddc/learn.png) **[Saiba mais sobre a malha protegida](https://docs.microsoft.com/windows-server/virtualization/guarded-fabric-shielded-vm/guarded-fabric-and-shielded-vms)**

### <a name="shielded-vms"></a>VMs blindadas

![](media/sddc/security-line.png)

Os dados e o estado de uma VM blindada são protegidos contra inspeção, roubo e adulteração por administradores de malware e datacenter.

![](media/sddc/spacer1.png)![](media/sddc/shielded.png)

- As VMs blindadas serão executadas somente em malhas designadas como proprietárias da VM.
- As VMs blindadas são criptografadas pelo BitLocker ou outros meios para que somente os proprietários designados possam executá-las.
- As VMs em execução podem ser convertidas em blindadas.

![](media/sddc/learn.png) **[Saiba mais sobre as VMs blindadas](https://docs.microsoft.com/windows-server/virtualization/guarded-fabric-shielded-vm/guarded-fabric-and-shielded-vms)**

### <a name="host-guardian-service"></a>Serviço Guardião de Host

![](media/sddc/security-line.png)

O Serviço Guardião de Host detém as chaves para malhas legítimas, bem como máquinas virtuais criptografadas.

![](media/sddc/spacer1.png)![](media/sddc/guardian.png)

![](media/sddc/learn.png) **[Saiba mais sobre o Serviço Guardião de Host](https://docs.microsoft.com/windows-server/virtualization/guarded-fabric-shielded-vm/guarded-fabric-manage-hgs)**

### <a name="device-health-attestation"></a>Atestado de Integridade do Dispositivo

![](media/sddc/security-line.png)

O atestado permite que as empresas elevem o nível de segurança de suas organizações para hardwares monitorados e segurança atestada com pouco ou nenhum impacto sobre os custos da operação.


![](media/sddc/spacer1.png)![](media/sddc/attestation.png)


O modo confiável de hardware mostrado acima fornece o nível mais alto de garantia, com confiança proveniente de hardware do TPM v2.0 e conformidade com a política de integridade de código para lançamento de chave.


![](media/sddc/learn.png) **[Saiba mais sobre o Atestado de integridade do dispositivo](https://docs.microsoft.com/windows-server/security/device-health-attestation)**

![](media/sddc/management.png)

### <a name="powershell-desired-state-configuration"></a>Desired State Configuration do PowerShell

![](media/sddc/management-line.png)

A Desired State Configuration do Windows PowerShell fornece uma plataforma de gerenciamento de configuração integrada no Windows que se baseia em padrões abertos. A DSC é flexível o suficiente para funcionar de maneira confiável e consistente em cada estágio do ciclo de vida de implantação (desenvolvimento, teste, pré-produção, produção), bem como durante a expansão.

![](media/sddc/spacer1.png)![](media/sddc/dsc.png)

A DSC é compatível com "implantações contínuas" para que você possa implantar configurações repetidamente sem perder nada.

-  As configurações de DSC aplicam-se somente às configurações que foram alteradas em relação à original para implantações mais rápidas.
-  A DSC pode ser usada em um ambiente de Nuvem pública, privada ou local.
-  Você pode integrar a DSC a qualquer solução da Microsoft ou não, desde que possa executar um script do PowerShell no sistema alvo.

![](media/sddc/learn.png) **[Saiba mais sobre a DSC do PowerShell](https://docs.microsoft.com/powershell/dsc/overview)**


### <a name="system-center-vmm"></a>System Center VMM

![](media/sddc/management-line.png)

O Virtual Machine Manager faz parte do pacote do System Center, usado para configurar, gerenciar e transformar os datacenters tradicionais para proporcionar uma experiência de gerenciamento unificada em todos os locais e provedor de serviços de nuvem do Azure.

![](media/sddc/spacer1.png)![](media/sddc/vmm.png)

- Datacenter: Configure e gerencie os componentes do datacenter como uma malha no VMM. 
- Host de virtualização: o VMM pode adicionar, provisionar e gerenciar os hosts de virtualização do Hyper-V e VMware, além de clusters.
- Rede: o VMM fornece virtualização de rede, incluindo suporte para criar e gerenciar redes virtuais e gateways de rede. 
- Armazenamento: o VMM pode descobrir, classificar, provisionar, alocar e atribuir o armazenamento local e remoto.

![](media/sddc/learn.png) **[Saiba mais sobre o System Center VMM](https://docs.microsoft.com/system-center/vmm/)**

### <a name="windows-admin-center"></a>Windows Admin Center

![](media/sddc/management-line.png)

O Windows Admin Center é um conjunto de ferramentas de gerenciamento implantado localmente com base em navegador que permite a administração no local de servidores do Windows sem dependência do Azure nem da nuvem. O Windows Admin Center fornece aos administradores de TI controle total sobre todos os aspectos da infraestrutura de servidor e é particularmente útil para o gerenciamento de redes privadas que não estão conectadas à Internet.

![](media/sddc/spacer1.png)![](media/sddc/architecture.png)

A publicação do servidor Web no DNS e a configuração do firewall corporativo possibilitam que você acesse o Windows Admin Center pela Internet pública, permitindo que você se conecte e gerencie os servidores de qualquer lugar com o Microsoft Edge ou o Google Chrome.

![](media/sddc/learn.png) **[Saiba mais sobre o Windows Admin Center](manage/windows-admin-center/overview.md)**
