---
title: Gerenciar máquinas virtuais do Windows com o PowerShell Direct
description: Fornece instruções sobre como usar o PowerShell Direct para gerenciar máquinas virtuais sem depender de uma rede ou conexão remota a elas.
ms.prod: windows-server
manager: dongill
ms.technology: compute-hyper-v
ms.topic: article
ms.assetid: b5715c02-a90f-4de9-a71e-0fc09093ba2d
author: kbdazure
ms.author: kathydav
ms.date: 10/04/2016
ms.openlocfilehash: c4a051de2d8f62c38ae0c44b1a62d5bf9df339e8
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80859429"
---
# <a name="manage-windows-virtual-machines-with-powershell-direct"></a>Gerenciar máquinas virtuais do Windows com o PowerShell Direct

>Aplica-se a: Windows 10, Windows Server 2016, Windows Server 2019
  
Você pode usar o PowerShell Direct para gerenciar remotamente uma máquina virtual do Windows 10, Windows Server 2016 ou Windows Server 2019 de um host Hyper-V do Windows 10, Windows Server 2016 ou Windows Server 2019. O PowerShell Direct permite o gerenciamento do Windows PowerShell dentro de uma máquina virtual, independentemente da configuração de rede ou das configurações de gerenciamento remoto no host Hyper-V ou na máquina virtual. Isso facilita a tarefa dos Administradores do Hyper-V de automatizar e executar scripts de configuração e gerenciamento de máquinas virtuais.  
  
Há duas maneiras de executar o PowerShell Direct:  
  
- Criar e sair de uma sessão direta do PowerShell usando cmdlets de PSSession
  
- Executar script ou comando com o cmdlet Invoke-Command
  
Se você estiver gerenciando máquinas virtuais mais antigas, use o VMConnect (Conexão com Máquina Virtual) ou [configure uma rede virtual para a máquina virtual](https://technet.microsoft.com/library/cc816585.aspx).  
  
## <a name="create-and-exit-a-powershell-direct-session-using-pssession-cmdlets"></a>Criar e sair de uma sessão direta do PowerShell usando cmdlets de PSSession  
  
1. No servidor do Hyper-V, abra o Windows PowerShell como Administrador.  
  
2. Use o cmdlet [Enter-PSSession](https://technet.microsoft.com/library/hh849707.aspx) para se conectar à máquina virtual. Execute um dos seguintes comandos para criar uma sessão usando o nome ou o GUID da máquina virtual:  
  
    ```  
    Enter-PSSession -VMName <VMName>  
    ```  
  
    ```  
    Enter-PSSession -VMGUID <VMGUID>  
    ```  
  
3. Digite suas credenciais para a máquina virtual.   
4. Execute os comandos necessários. Esses comandos são executados na máquina virtual com a qual você criou a sessão.  
  
5.  Quando terminar, use [Exit-PSSession](https://technet.microsoft.com/library/hh849743.aspx) para fechar a sessão.   
  
    ```  
    Exit-PSSession  
    ```  
  
## <a name="run-script-or-command-with-invoke-command-cmdlet"></a>Executar script ou comando com o cmdlet Invoke-Command  
Você pode usar o cmdlet [Invoke-Command](https://docs.microsoft.com/powershell/module/Microsoft.PowerShell.Core/Invoke-Command) para executar um conjunto predeterminado de comandos na máquina virtual. Aqui está um exemplo de como você pode usar o cmdlet Invoke-Command, onde PSTest é o nome da máquina virtual e o script a ser executado (foo.ps1) está na pasta de script na unidade “C:/”:  
  
```  
Invoke-Command -VMName PSTest  -FilePath C:\script\foo.ps1  
```  
  
Para executar um único comando, use o parâmetro **-ScriptBlock**:  
  
```  
Invoke-Command -VMName PSTest  -ScriptBlock { cmdlet }  
```  
  
## <a name="whats-required-to-use-powershell-direct"></a>O que é necessário para usar o PowerShell Direct?  
Para criar uma sessão do PowerShell Direct em uma máquina virtual,  
  
-   A máquina virtual deve ser executada localmente no host e inicializada.  
  
-   Você deve estar conectado ao computador host como um administrador do Hyper-V.  
  
-   É necessário fornecer credenciais de usuário válidas para a máquina virtual.  
  
-   O sistema operacional do host deve executar pelo menos o Windows 10 ou o Windows Server 2016.
  
-   A máquina virtual deve executar pelo menos o Windows 10 ou o Windows Server 2016.  
  
Você pode usar o cmdlet [Get-VM](https://docs.microsoft.com/powershell/module/hyper-v/get-vm) para verificar se as credenciais que você está usando têm a função Administrador do Hyper-V e para obter uma lista das máquinas virtuais em execução localmente no host e inicializadas.  
  
## <a name="see-also"></a>Consulte também  
[Enter-PSSession](https://docs.microsoft.com/powershell/module/Microsoft.PowerShell.Core/Enter-PSSession)  
[Sair-PSSession](https://docs.microsoft.com/powershell/module/Microsoft.PowerShell.Core/Exit-PSSession)  
[Invoke-Command](https://docs.microsoft.com/powershell/module/Microsoft.PowerShell.Core/Invoke-Command)  
  


