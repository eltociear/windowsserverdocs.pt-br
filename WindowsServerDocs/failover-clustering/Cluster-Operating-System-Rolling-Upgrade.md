---
title: Atualização sem interrupção do sistema operacional do cluster
ms.prod: windows-server
ms.technology: storage-failover-clustering
ms.topic: get-started-article
ms.assetid: 6e102c1f-df26-4eaa-bc7a-d0d55d3b82d5
author: jasongerend
ms.author: jgerend
manager: lizross
ms.date: 03/27/2018
ms.openlocfilehash: 8b2ea665542d57b12899a5993a62973c446485a7
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80828349"
---
# <a name="cluster-operating-system-rolling-upgrade"></a>Atualização sem interrupção do sistema operacional do cluster

> Aplica-se a: Windows Server 2019, Windows Server 2016

A atualização sem interrupção do so do cluster permite que um administrador atualize o sistema operacional dos nós do cluster sem interromper o Hyper-V ou as cargas de trabalho de Servidor de Arquivos de Escalabilidade Horizontal. Usando esse recurso, as penalidades de tempo de inatividade em SLAs (Contratos de Nível de Serviço) podem ser evitadas.

A atualização sem interrupção do sistema operacional do cluster oferece os seguintes benefícios:

- Os clusters de failover que executam a máquina virtual do Hyper-V e cargas de trabalho do SOFS (servidor de arquivos de escalabilidade horizontal) podem ser atualizados do Windows Server 2012 R2 (em execução em todos os nós no cluster) para o Windows Server 2016 (em execução em todos os nós de cluster do cluster) sem tempo de inatividade. Outras cargas de trabalho de cluster, como SQL Server, ficarão indisponíveis durante o tempo (normalmente menos de cinco minutos) para o failover para o Windows Server 2016.  
- Ele não requer hardware adicional. Embora você possa adicionar mais nós de cluster temporariamente a clusters pequenos para melhorar a disponibilidade do cluster durante o processo de atualização sem interrupção do sistema operacional do cluster.  
- O cluster não precisa ser interrompido ou reiniciado.  
- Um novo cluster não é necessário. O cluster existente é atualizado. Além disso, os objetos de cluster existentes armazenados em Active Directory são usados.  
- O processo de atualização é reversível até que o cliente escolha o "ponto de não-retorno", quando todos os nós de cluster estão executando o Windows Server 2016 e quando o cmdlet do PowerShell Update-ClusterFunctionalLevel é executado.  
- O cluster pode dar suporte a operações de patch e manutenção durante a execução no modo de sistema operacional misto.  
- Ele dá suporte à automação por meio do PowerShell e do WMI.  
- A propriedade pública de propriedade **ClusterFunctionalLevel** do cluster indica o estado do cluster em nós de cluster do Windows Server 2016. Essa propriedade pode ser consultada usando o cmdlet do PowerShell de um nó de cluster do Windows Server 2016 que pertence a um cluster de failover:  
    ```PowerShell
    Get-Cluster | Select ClusterFunctionalLevel  
    ```  

    Um valor de **8** indica que o cluster está sendo executado no nível funcional do Windows Server 2012 R2. Um valor de **9** indica que o cluster está sendo executado no nível funcional do Windows Server 2016.  

Este guia descreve os vários estágios do processo de atualização sem interrupção do sistema operacional do cluster, etapas de instalação, limitações de recursos e perguntas frequentes (FAQs) e é aplicável aos seguintes cenários de atualização sem interrupção do sistema operacional do cluster no Windows Server 2016:  
- Clusters do Hyper-V  
- Clusters Servidor de Arquivos de Escalabilidade Horizontal  

O cenário a seguir não tem suporte no Windows Server 2016:  
-  Atualização sem interrupção do sistema operacional do cluster de clusters de convidado usando o disco rígido virtual (arquivo. vhdx) como armazenamento compartilhado  

A atualização sem interrupção do sistema operacional do cluster tem suporte total pelo SCVMM (System Center Virtual Machine Manager) 2016. Se você estiver usando o SCVMM 2016, consulte [executar uma atualização sem interrupção de um cluster de host do Hyper-V para o Windows Server 2016 no VMM](https://docs.microsoft.com/system-center/vmm/hyper-v-rolling-upgrade?view=sc-vmm-1807) para obter orientação sobre como atualizar os clusters e automatizar as etapas descritas neste documento.  

## <a name="requirements"></a>{1&gt;{2&gt;Requisitos&lt;2}&lt;1}  
Conclua os seguintes requisitos antes de iniciar o processo de atualização sem interrupção do sistema operacional do cluster:

- Comece com um cluster de failover executando o Windows Server (canal semestral), Windows Server 2016 ou Windows Server 2012 R2.
- Não há suporte para a atualização de um cluster Espaços de Armazenamento Diretos para o Windows Server, versão 1709.
- Se a carga de trabalho do cluster for de VMs do Hyper-V ou Servidor de Arquivos de Escalabilidade Horizontal, você poderá esperar uma atualização sem tempo de inatividade.
- Verifique se os nós do Hyper-V têm CPUs que dão suporte a SLAT (tabela de endereçamento de segundo nível) usando um dos seguintes métodos;  
        -Examine se [você é compatível com slat? Artigo da dica do SDK do WP8 01](https://blogs.msdn.com/b/devfish/archive/2012/11/06/are-you-slat-compatible-wp8-sdk-tip-01.aspx) que descreve dois métodos para verificar se uma CPU dá suporte a slats  
        -Baixe a ferramenta [Coreinfo v 3.31](https://technet.microsoft.com/sysinternals/cc835722) para determinar se uma CPU oferece suporte a slat.

## <a name="cluster-transition-states-during-cluster-os-rolling-upgrade"></a>Estados de transição de cluster durante a atualização sem interrupção do sistema operacional do cluster

Esta seção descreve os vários Estados de transição do cluster do Windows Server 2012 R2 que estão sendo atualizados para o Windows Server 2016 usando a atualização sem interrupção do sistema operacional do cluster.  

Para manter as cargas de trabalho de cluster em execução durante o processo de atualização sem interrupção do sistema operacional do cluster, mover uma carga de trabalho de cluster de um nó do Windows Server 2012 R2 para o Windows Server 2016 funciona como se ambos os nós estivessem executando o sistema operacional Windows Server 2012 R2. Quando nós do Windows Server 2016 são adicionados ao cluster, eles operam em um modo de compatibilidade do Windows Server 2012 R2. Um novo modo de cluster conceitual, chamado "modo de sistema operacional misto", permite que os nós de versões diferentes existam no mesmo cluster (consulte a Figura 1).  

![ilustração mostrando os três estágios de uma atualização sem interrupção do sistema operacional do cluster: todos os nós do Windows Server 2012 R2, do modo misto do sistema operacional e de todos os nós do Windows Server 2016](media/Cluster-Operating-System-Rolling-Upgrade/Clustering_RollingUpgrade_Overview.png)  
**Figura 1: transições de estado do sistema operacional do cluster**  

Um cluster do Windows Server 2012 R2 entra no modo de sistema operacional misto quando um nó do Windows Server 2016 é adicionado ao cluster. O processo é totalmente reversível-os nós do Windows Server 2016 podem ser removidos do cluster e os nós do Windows Server 2012 R2 podem ser adicionados ao cluster nesse modo. O "ponto de nenhum retorno" ocorre quando o cmdlet do PowerShell Update-ClusterFunctionalLevel é executado no cluster. Para que esse cmdlet seja bem sucedido, todos os nós devem ser Windows Server 2016 e todos os nós devem estar online.  

## <a name="transition-states-of-a-four-node-cluster-while-performing-rolling-os-upgrade"></a>Estados de transição de um cluster de quatro nós ao executar a atualização do sistema operacional sem interrupção

Esta seção ilustra e descreve os quatro estágios diferentes de um cluster com armazenamento compartilhado cujos nós são atualizados do Windows Server 2012 R2 para o Windows Server 2016.  

"Estágio 1" é o estado inicial – começamos com um cluster do Windows Server 2012 R2.  

![ilustração mostrando o estado inicial: todos os nós Windows Server 2012 R2](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_Stage1.png)  
**Figura 2: estado inicial: cluster de failover do Windows Server 2012 R2 (estágio 1)**  

No "estágio 2", dois nós foram pausados, drenados, removidos, reformatados e instalados com o Windows Server 2016.  

![ilustração mostrando o cluster no modo de sistema operacional misto: fora do exemplo de cluster de 4 nós, dois nós estão executando o Windows Server 2016 e dois nós estão executando o Windows Server 2012 R2](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_Stage2.png)  
**Figura 3: estado intermediário: modo de sistema operacional misto: cluster de failover do Windows Server 2012 R2 e do Windows Server 2016 (estágio 2)**  

No "estágio 3", todos os nós no cluster foram atualizados para o Windows Server 2016 e o cluster está pronto para ser atualizado com o cmdlet do PowerShell Update-ClusterFunctionalLevel.  

> [!NOTE]  
> Nesse estágio, o processo pode ser totalmente revertido e os nós do Windows Server 2012 R2 podem ser adicionados a esse cluster.  

![ilustração mostrando que o cluster foi totalmente atualizado para o Windows Server 2016 e está pronto para o cmdlet Update-ClusterFunctionalLevel para colocar o nível funcional do cluster no Windows Server 2016](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_Stage3.png)  
**Figura 4: estado intermediário: todos os nós atualizados para o Windows Server 2016, pronto para Update-ClusterFunctionalLevel (estágio 3)**  

Após a execução de Update-ClusterFunctionalLevelcmdlet, o cluster entra em "estágio 4", onde novos recursos de cluster do Windows Server 2016 podem ser usados.  

![ilustração mostrando que a atualização do sistema operacional sem interrupção do cluster foi concluída com êxito; todos os nós foram atualizados para o Windows Server 2016 e o cluster está sendo executado no nível funcional do cluster do Windows Server 2016](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_Stage4.png)  
**Figura 5: estado final: cluster de failover do Windows Server 2016 (estágio 4)**  

## <a name="cluster-os-rolling-upgrade-process"></a>Processo de atualização sem interrupção do sistema operacional do cluster

Esta seção descreve o fluxo de trabalho para executar a atualização sem interrupção do sistema operacional do cluster.  

![ilustração mostrando o fluxo de trabalho para atualizar um cluster](media/Cluster-Operating-System-Rolling-Upgrade/Clustering_RollingUpgrade_Workflow.png)  
**Figura 6: fluxo de trabalho do processo de atualização sem interrupção do so do cluster**  

A atualização sem interrupção do sistema operacional do cluster inclui as seguintes etapas:  

1. Prepare o cluster para a atualização do sistema operacional da seguinte maneira:  
    1. A atualização sem interrupção do sistema operacional do cluster requer a remoção de um nó por vez do cluster. Verifique se você tem capacidade suficiente no cluster para manter os SLAs de alta disponibilidade quando um dos nós de cluster for removido do cluster para uma atualização do sistema operacional. Em outras palavras, você precisa da capacidade de failover de cargas de trabalho para outro nó quando um nó é removido do cluster durante o processo de atualização sem interrupção do sistema operacional do cluster? O cluster tem a capacidade de executar as cargas de trabalho necessárias quando um nó é removido do cluster para a atualização sem interrupção do sistema operacional do cluster?  
    2. Para cargas de trabalho do Hyper-V, verifique se todos os hosts do Windows Server 2016 Hyper-V têm suporte de CPU para SLAT (tabela de endereços de segundo nível). Somente computadores compatíveis com SLAT podem usar a função Hyper-V no Windows Server 2016.  
    3. Verifique se todos os backups de carga de trabalho foram concluídos e considere fazer backup do cluster. Interrompa as operações de backup ao adicionar nós ao cluster.  
    4. Verifique se todos os nós de cluster estão online/running/up usando o cmdlet [`Get-ClusterNode`](https://docs.microsoft.com/powershell/module/failoverclusters/Get-ClusterNode?view=win10-ps) (veja a Figura 7).  

        ![captura mostrando os resultados da execução do cmdlet Get-ClusterNode](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_GetClusterNode.png)  
        **Figura 7: determinando o status do nó usando o cmdlet Get-ClusterNode**  

    5. Se você estiver executando as atualizações de reconhecimento de cluster (CAU), verifique se a CAU está em execução no momento usando a interface do usuário de **atualização com suporte a cluster** ou o cmdlet [`Get-CauRun`](https://docs.microsoft.com/powershell/module/clusterawareupdating/Get-CauRun?view=win10-ps) (consulte a Figura 8). Interrompa a CAU usando o cmdlet [`Disable-CauClusterRole`](https://docs.microsoft.com/powershell/module/clusterawareupdating/Disable-CauClusterRole?view=win10-ps) (consulte a Figura 9) para impedir que todos os nós sejam pausados e drenados pela Cau durante o processo de atualização sem interrupção do sistema operacional do cluster.  

        ![captura mostrando a saída do cmdlet Get-CauRun](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_GetCAU.png)  
        **Figura 8: usando o cmdlet [`Get-CauRun`](https://docs.microsoft.com/powershell/module/clusterawareupdating/Get-CauRun?view=win10-ps) para determinar se as atualizações com reconhecimento de cluster estão em execução no cluster**  

        ![captura mostrando a saída do cmdlet Disable-CauClusterRole](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_DisableCAU.png)  
        **Figura 9: desabilitando a função de atualizações com suporte de cluster usando o cmdlet [`Disable-CauClusterRole`](https://docs.microsoft.com/powershell/module/clusterawareupdating/Disable-CauClusterRole?view=win10-ps)**  

2. Para cada nó no cluster, conclua o seguinte:  
    1. Usando a interface do usuário do Gerenciador de cluster, selecione um nó e use a **pausa |** A opção de menu dreno para drenar o nó (consulte a Figura 10) ou use o cmdlet [`Suspend-ClusterNode`](https://docs.microsoft.com/powershell/module/failoverclusters/Suspend-ClusterNode?view=win10-ps) (consulte a Figura 11).  

        ![captura mostrando como esvaziar funções com a interface do usuário do Gerenciador de cluster](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_FCM_DrainRoles.png)  
        **Figura 10: esvaziando funções de um nó usando Gerenciador de Cluster de Failover**  

        ![captura mostrando a saída do cmdlet Suspend-ClusterNode](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_SuspendNode.png)  
        **Figura 11: esvaziando funções de um nó usando o cmdlet [`Suspend-ClusterNode`](https://docs.microsoft.com/powershell/module/failoverclusters/Suspend-ClusterNode?view=win10-ps)**  

    2.  Usando a interface do usuário do Gerenciador de cluster, **remova** o nó em pausa do cluster ou use o cmdlet [`Remove-ClusterNode`](https://docs.microsoft.com/powershell/module/failoverclusters/Remove-ClusterNode?view=win10-ps) .  

        ![captura mostrando a saída do cmdlet Remove-ClusterNode](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_RemoveNode.png)  
        **Figura 12: remover um nó do cluster usando [`Remove-ClusterNode`](https://docs.microsoft.com/powershell/module/failoverclusters/Remove-ClusterNode?view=win10-ps) cmdlet**  

    3.  Reformate a unidade do sistema e execute uma "instalação limpa do sistema operacional" do Windows Server 2016 no nó usando a opção de instalação **personalizada: instalar somente Windows (avançado)** (consulte a Figura 13) em setup. exe. Evite selecionar a opção **Atualizar: instalar o Windows e manter arquivos, configurações e aplicativos** , pois a atualização sem interrupção do sistema operacional do cluster não incentiva a atualização in-loco.  

        ![captura do assistente de instalação do Windows Server 2016 mostrando a opção de instalação personalizada selecionada](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_InstallOption.png)  
        **Figura 13: opções de instalação disponíveis para o Windows Server 2016**  

    4.  Adicione o nó ao domínio de Active Directory apropriado.  
    5.  Adicione os usuários apropriados ao grupo Administradores.  
    6.  Usando a interface do usuário do Gerenciador do Servidor ou o cmdlet Install-WindowsFeature do PowerShell, instale todas as funções de servidor necessárias, como o Hyper-V.  

        ```PowerShell
        Install-WindowsFeature -Name Hyper-V  
        ```  

    7.  Usando a interface do usuário do Gerenciador do Servidor ou o cmdlet Install-WindowsFeature do PowerShell, instale o recurso clustering de failover.  

        ```PowerShell
        Install-WindowsFeature -Name Failover-Clustering  
        ```  

    8.  Instale quaisquer recursos adicionais necessários para suas cargas de trabalho de cluster.  
    9. Verifique as configurações de conectividade de rede e armazenamento usando a interface do usuário do Gerenciador de Cluster de Failover.  
    10. Se o Firewall do Windows for usado, verifique se as configurações do firewall estão corretas para o cluster. Por exemplo, os clusters habilitados para CAU (atualização com reconhecimento de cluster) podem exigir a configuração do firewall.  
    11. Para cargas de trabalho do Hyper-V, use a IU do Gerenciador do Hyper-V para iniciar a caixa de diálogo Gerenciador de comutador virtual (consulte a Figura 14).  

        Verifique se o nome dos comutadores virtuais usados são idênticos para todos os nós de host do Hyper-V no cluster.  

        ![captura mostrando o local da caixa de diálogo Gerenciador de comutador virtual do Hyper-V](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_VMSwitch.png)  
        **Figura 14: Gerenciador de comutador virtual**  

    12. Em um nó do Windows Server 2016 (não use um nó do Windows Server 2012 R2), use a Gerenciador de Cluster de Failover (consulte a Figura 15) para se conectar ao cluster.  

        ![captura mostrando a caixa de diálogo Selecionar cluster](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_AddNode.png)  
        **Figura 15: adicionando um nó ao cluster usando Gerenciador de Cluster de Failover**  

    13. Use a interface do usuário do Gerenciador de Cluster de Failover ou o cmdlet [`Add-ClusterNode`](https://docs.microsoft.com/powershell/module/failoverclusters/Add-ClusterNode?view=win10-ps) (consulte a Figura 16) para adicionar o nó ao cluster.  

        ![captura mostrando a saída do cmdlet Add-ClusterNode](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_AddNode3.png)  
        **Figura 16: adicionando um nó ao cluster usando [`Add-ClusterNode`](https://docs.microsoft.com/powershell/module/failoverclusters/Add-ClusterNode?view=win10-ps) cmdlet**  

        > [!NOTE]  
        > Quando o primeiro nó do Windows Server 2016 ingressa no cluster, o cluster entra no modo "sistema operacional misto" e os recursos principais do cluster são movidos para o nó do Windows Server 2016. Um cluster de modo "sistema operacional misto" é um cluster totalmente funcional em que os novos nós são executados em um modo de compatibilidade com os nós antigos. O modo "sistema operacional misto" é um modo transitório para o cluster. Não se destina a ser permanente e os clientes devem atualizar todos os nós de seu cluster dentro de quatro semanas.  

    14. Depois que o nó do Windows Server 2016 for adicionado com êxito ao cluster, você poderá (opcionalmente) mover parte da carga de trabalho do cluster para o nó recém-adicionado a fim de reequilibrar a carga de trabalho no cluster da seguinte maneira:

        ![captura mostrando a saída do cmdlet Move-ClusterVirtualMachineRole](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_MoveVMRole.png)  
        **Figura 17: movendo uma carga de trabalho de cluster (função VM de cluster) usando [`Move-ClusterVirtualMachineRole`](https://docs.microsoft.com/powershell/module/failoverclusters/Move-ClusterVirtualMachineRole?view=win10-ps) cmdlet**  

        1. Use **migração ao vivo** do Gerenciador de cluster de failover para máquinas virtuais ou o cmdlet [`Move-ClusterVirtualMachineRole`](https://docs.microsoft.com/powershell/module/failoverclusters/Move-ClusterVirtualMachineRole?view=win10-ps) (consulte a figura 17) para executar uma migração dinâmica das máquinas virtuais.  

            ```PowerShell
            Move-ClusterVirtualMachineRole -Name VM1 -Node robhind-host3  
            ```  

        2. Use **mover** do Gerenciador de cluster de failover ou o cmdlet [`Move-ClusterGroup`](https://docs.microsoft.com/powershell/module/failoverclusters/Move-ClusterGroup?view=win10-ps) para outras cargas de trabalho de cluster.  

3. Quando cada nó tiver sido atualizado para o Windows Server 2016 e adicionado de volta ao cluster, ou quando quaisquer nós restantes do Windows Server 2012 R2 tiverem sido removidos, faça o seguinte:  

    > [!IMPORTANT]  
    > -   Depois de atualizar o nível funcional do cluster, você não pode voltar para o nível funcional do Windows Server 2012 R2 e os nós do Windows Server 2012 R2 não podem ser adicionados ao cluster.
    > -   Até que o cmdlet de [`Update-ClusterFunctionalLevel`](https://docs.microsoft.com/powershell/module/failoverclusters/Update-ClusterFunctionalLevel?view=win10-ps) seja executado, o processo é totalmente reversível e os nós do windows Server 2012 R2 podem ser adicionados a esse cluster e os nós do windows Server 2016 podem ser removidos.  
    > -   Depois que o cmdlet [`Update-ClusterFunctionalLevel`](https://docs.microsoft.com/powershell/module/failoverclusters/Update-ClusterFunctionalLevel?view=win10-ps) for executado, novos recursos estarão disponíveis.  

    1.  Usando a interface do usuário do Gerenciador de Cluster de Failover ou o cmdlet [`Get-ClusterGroup`](https://docs.microsoft.com/powershell/module/failoverclusters/Get-ClusterGroup?view=win10-ps) , verifique se todas as funções de cluster estão em execução no cluster conforme o esperado. No exemplo a seguir, o armazenamento disponível não está sendo usado, em vez disso, o CSV é usado, portanto, o armazenamento disponível exibe um status **offline** (consulte a Figura 18).  

        ![captura mostrando a saída do cmdlet Get-cluster](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_GetClusterGroup.png)  
        **Figura 18: verificando se todos os grupos de clusters (funções de cluster) estão em execução usando o cmdlet [`Get-ClusterGroup`](https://docs.microsoft.com/powershell/module/failoverclusters/Get-ClusterGroup?view=win10-ps)**  

    2.  Verifique se todos os nós de cluster estão online e em execução usando o cmdlet [`Get-ClusterNode`](https://docs.microsoft.com/powershell/module/failoverclusters/Get-ClusterNode?view=win10-ps) .  
    3.  Execute o cmdlet [`Update-ClusterFunctionalLevel`](https://technet.microsoft.com/library/mt589702.aspx) -nenhum erro deve ser retornado (consulte a Figura 19).  

        ![captura mostrando a saída do cmdlet Update-ClusterFunctionalLevel](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_SelectFunctionalLevel.png)  
        **Figura 19: atualizando o nível funcional de um cluster usando o PowerShell**  

    4.  Depois que o cmdlet [`Update-ClusterFunctionalLevel`](https://docs.microsoft.com/powershell/module/failoverclusters/Update-ClusterFunctionalLevel?view=win10-ps) for executado, novos recursos estarão disponíveis.  

4. Windows Server 2016-retomar backups e atualizações de cluster normais:  

    1. Se você estava executando a CAU anteriormente, reinicie-a usando a interface do usuário da CAU ou use o cmdlet [`Enable-CauClusterRole`](https://docs.microsoft.com/powershell/module/clusterawareupdating/Enable-CauClusterRole?view=win10-ps) (consulte a figura 20).  

        ![captura mostrando a saída do](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_EnableCAUClusterRole.png) Enable-CauClusterRole  
        **Figura 20: habilitar a função de atualizações com suporte de cluster usando o cmdlet [`Enable-CauClusterRole`](https://docs.microsoft.com/powershell/module/clusterawareupdating/Enable-CauClusterRole?view=win10-ps)**  

    2. Retomar as operações de backup.  

5. Habilite e use os recursos do Windows Server 2016 em máquinas virtuais do Hyper-V.  

    1. Depois que o cluster tiver sido atualizado para o nível funcional do Windows Server 2016, muitas cargas de trabalho como as VMs do Hyper-V terão novos recursos. Para obter uma lista dos novos recursos do Hyper-V. consulte [migrar e atualizar máquinas virtuais](https://msdn.microsoft.com/virtualization/hyperv_on_windows/user_guide/migrating_vms)  

    2. Em cada nó de host do Hyper-V no cluster, use o cmdlet [`Get-VMHostSupportedVersion`](https://docs.microsoft.com/powershell/module/hyper-v/Get-VMHostSupportedVersion?view=win10-ps) para exibir as versões de configuração de VM do Hyper-v com suporte no host.  

        ![captura mostrando a saída do cmdlet Get-VMHostSupportedVersion](media/Cluster-Operating-System-Rolling-Upgrade/Clustering_GetVMHostSupportVersion.png)  
        **Figura 21: exibindo as versões de configuração de VM do Hyper-V com suporte no host**  

   3. Em cada nó de host do Hyper-V no cluster, as versões de configuração da VM do Hyper-V podem ser atualizadas agendando uma breve janela de manutenção com usuários, fazendo backup, desativando máquinas virtuais e executando o cmdlet [`Update-VMVersion`](https://docs.microsoft.com/powershell/module/hyper-v/Update-VMVersion?view=win10-ps) (consulte a Figura 22). Isso atualizará a versão da máquina virtual e habilitará novos recursos do Hyper-V, eliminando a necessidade de atualizações de IC (componente de integração do Hyper-V) futuras. Esse cmdlet pode ser executado a partir do nó do Hyper-V que está hospedando a VM ou o parâmetro `-ComputerName` pode ser usado para atualizar a versão da VM remotamente. Neste exemplo, atualizamos a versão de configuração do VM1 de 5,0 para 7,0 para aproveitar os muitos recursos novos do Hyper-V associados a essa versão de configuração da VM, como pontos de verificação de produção (backups consistentes com o aplicativo) e o arquivo de configuração de VM binária.  

       ![captura mostrando o cmdlet Update-VMVersion em ação](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_StopVM.png)  
       **Figura 22: atualizando uma versão de VM usando o cmdlet Update-VMVersion do PowerShell**  

6. Os pools de armazenamento podem ser atualizados usando o cmdlet do PowerShell [Update-StoragePool](https://docs.microsoft.com/powershell/module/storage/Update-StoragePool?view=win10-ps) -esta é uma operação online.  

Embora tenhamos como alvo cenários de nuvem privada, especificamente o Hyper-V e os clusters de servidores de arquivos de escalabilidade horizontal, que podem ser atualizados sem tempo de inatividade, o processo de atualização sem interrupção do sistema operacional do cluster pode ser usado para qualquer função de cluster.  

## <a name="restrictions--limitations"></a>Restrições/limitações  
- Esse recurso funciona apenas para o Windows Server 2012 R2 para versões do Windows Server 2016. Esse recurso não pode atualizar versões anteriores do Windows Server, como o Windows Server 2008, o Windows Server 2008 R2 ou o Windows Server 2012 para o Windows Server 2016.  
- Cada nó do Windows Server 2016 deve ser reformatado/novo instalação. O tipo de instalação "in-loco" ou "upgrade" não é recomendado.  
- Um nó do Windows Server 2016 deve ser usado para adicionar nós do Windows Server 2016 ao cluster.  
- Ao gerenciar um cluster de modo de sistema operacional misto, sempre execute as tarefas de gerenciamento de um nó de uplevem que esteja executando o Windows Server 2016. Os nós do Windows Server 2012 R2 de nível inferior não podem usar a interface do usuário nem as ferramentas de gerenciamento no Windows Server 2016.  
- Incentivamos os clientes a percorrer o processo de atualização de cluster rapidamente, pois alguns recursos de cluster não são otimizados para o modo de sistema operacional misto.  
- Evite criar ou redimensionar o armazenamento em nós do Windows Server 2016 enquanto o cluster estiver sendo executado no modo de sistema operacional misto devido a possíveis incompatibilidades no failover de um nó do Windows Server 2016 para nós do Windows Server 2012 R2 de nível inferior.  

## <a name="frequently-asked-questions"></a>Perguntas frequentes  
**Quanto tempo o cluster de failover pode ser executado no modo de sistema operacional misto?**  
    Incentivamos os clientes a concluir a atualização dentro de quatro semanas. Há muitas otimizações no Windows Server 2016. Nós atualizamos com êxito o Hyper-V e os clusters de servidor de arquivos de escalabilidade horizontal com tempo de inatividade zero em menos de quatro horas no total.  

**Você vai portar esse recurso para o Windows Server 2012, o Windows Server 2008 R2 ou o Windows Server 2008?**  
    Não temos planos para portar esse recurso de volta para versões anteriores. A atualização sem interrupção do sistema operacional do cluster é nossa visão para atualizar clusters do Windows Server 2012 R2 para o Windows Server 2016 e posterior.  

**O cluster do Windows Server 2012 R2 precisa ter todas as atualizações de software instaladas antes de iniciar o processo de atualização sem interrupção do sistema operacional do cluster?**  
    Sim, antes de iniciar o processo de atualização sem interrupção do sistema operacional do cluster, verifique se todos os nós do cluster estão atualizados com as atualizações de software mais recentes.  

**Posso executar o cmdlet [`Update-ClusterFunctionalLevel`](https://docs.microsoft.com/powershell/module/failoverclusters/Update-ClusterFunctionalLevel?view=win10-ps) enquanto os nós estiverem desligados ou em pausa?**  
    Não. Todos os nós de cluster devem ser ativados e na associação ativa para que o cmdlet de [`Update-ClusterFunctionalLevel`](https://docs.microsoft.com/powershell/module/failoverclusters/Update-ClusterFunctionalLevel?view=win10-ps) funcione.  

**O trabalho de atualização sem interrupção do sistema operacional do cluster funciona para qualquer carga do cluster? Ele funciona para SQL Server?**  
    Sim, a atualização sem interrupção do sistema operacional do cluster funciona para qualquer carga de trabalho de cluster. No entanto, é apenas um tempo de inatividade para o Hyper-V e clusters de servidores de arquivos de escalabilidade horizontal. A maioria das outras cargas de trabalho incorrem em algum tempo de inatividade (normalmente alguns minutos) durante o failover e o failover é necessário pelo menos uma vez durante o processo de atualização sem interrupção do sistema operacional do cluster.  

**Posso automatizar esse processo usando o PowerShell?**  
    Sim, criamos a atualização sem interrupção do sistema operacional do cluster para ser automatizada usando o PowerShell.  

**Para um cluster grande que tem capacidade de failover e carga de trabalho extra, posso atualizar vários nós simultaneamente?**  
    Sim. Quando um nó é removido do cluster para atualizar o sistema operacional, o cluster terá um nó less para failover e, portanto, terá uma capacidade de failover reduzida. Para clusters grandes com carga de trabalho e capacidade de failover suficientes, vários nós podem ser atualizados simultaneamente. Você pode adicionar nós de cluster temporariamente ao cluster para fornecer uma capacidade de carga de trabalho e failover aprimorada durante o processo de atualização sem interrupção do sistema operacional do cluster.  

**E se eu descobrir um problema em meu cluster depois que [`Update-ClusterFunctionalLevel`](https://docs.microsoft.com/powershell/module/failoverclusters/Update-ClusterFunctionalLevel?view=win10-ps) foi executado com êxito?**  
    Se tiver feito backup do banco de dados de cluster com um backup de estado do sistema antes de executar [`Update-ClusterFunctionalLevel`](https://docs.microsoft.com/powershell/module/failoverclusters/Update-ClusterFunctionalLevel?view=win10-ps), você deverá ser capaz de executar uma restauração autoritativa em um nó de cluster do Windows Server 2012 R2 e restaurar o banco de dados do cluster original e a configuração.  

**Posso usar a atualização in-loco para cada nó em vez de usar a instalação limpa do sistema operacional reformatando a unidade do sistema?**  
    Não incentivamos o uso da atualização in-loco do Windows Server, mas estamos cientes de que ele funciona em alguns casos em que os drivers padrão são usados. Leia atentamente todas as mensagens de aviso exibidas durante a atualização in-loco de um nó de cluster.  

**Se estiver usando a replicação do Hyper-V para uma VM do Hyper-V em meu cluster do Hyper-V, a replicação permanecerá intacta durante e após o processo de atualização sem interrupção do sistema operacional do cluster?**  
    Sim, a réplica do Hyper-V permanece intacta durante e após o processo de atualização sem interrupção do sistema operacional do cluster.  

**Posso usar o SCVMM (System Center 2016 Virtual Machine Manager) para automatizar o processo de atualização sem interrupção do sistema operacional do cluster?**  
    Sim, você pode automatizar o processo de atualização sem interrupção do sistema operacional do cluster usando o VMM no System Center 2016.  

## <a name="see-also"></a>Consulte também  
-   [Notas de versão: problemas importantes no Windows Server 2016](../get-started/Release-Notes--Important-Issues-in-Windows-Server-2016-Technical-Preview.md)  
-   [Novidades no Windows Server 2016](../get-started/What-s-New-in-windows-server-2016.md)  
-   [O que há de novo no clustering de failover no Windows Server](whats-new-in-failover-clustering.md)  
