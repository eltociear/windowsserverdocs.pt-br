---
title: Gerenciar VPN no Windows Server Essentials
description: Descreve como usar o Windows Server Essentials
ms.date: 10/03/2016
ms.prod: windows-server
ms.topic: article
ms.assetid: cc2b264a-b9a8-4114-9f7b-8604f77096e5
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 38c0b0e7bfc29f0b7717cd18a103ae068bbb259b
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80852689"
---
# <a name="manage-vpn-in-windows-server-essentials"></a>Gerenciar VPN no Windows Server Essentials

>Aplica-se a: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials 
  
 As conexões VPN (rede privada virtual) permitem que os usuários que trabalham em casa ou em viagens acessem um servidor em uma rede privada usando a infraestrutura fornecida por uma rede pública, como a Internet. Para usar VPN para acessar recursos do servidor, você deve:  
  
-   [Habilitar VPN para acesso remoto no servidor](Manage-VPN-in-Windows-Server-Essentials.md#BKMK_1)  
  
-   [Definir permissões de VPN para usuários de rede](Manage-VPN-in-Windows-Server-Essentials.md#BKMK_2)  
  
-   [Conectar computadores cliente ao servidor](Manage-VPN-in-Windows-Server-Essentials.md#BKMK_Connect)  
  
-   [Usar VPN para se conectar ao Windows Server Essentials](Manage-VPN-in-Windows-Server-Essentials.md#BKMK_3)  
  
##  <a name="enable-vpn-for-remote-access-on-the-server"></a><a name="BKMK_1"></a>Habilitar VPN para acesso remoto no servidor  
 Conclua o procedimento a seguir para configurar o VPN no Windows Server Essentials de modo a habilitar o acesso remoto.  
  
#### <a name="to-enable-vpn-in-windows-server-essentials"></a>Para habilitar o VPN no Windows Server Essentials  
  
1.  Abra o Dashboard.  
  
2.  Clique em **Configurações** e clique na guia **Acesso em Qualquer Local**.  
  
3.  Clique em **Configurar**. O assistente de configuração do Acesso em Qualquer Local é exibido.  
  
4.  Na página **Escolher os recursos do Acesso em Qualquer Local a habilitar**, marque a caixa de seleção **Rede Virtual Privada**.  
  
5.  Siga as instruções para concluir o assistente.  
  
##  <a name="set-vpn-permissions-for-network-users"></a><a name="BKMK_2"></a>Definir permissões de VPN para usuários de rede  
 Você pode usar VPN para se conectar ao Windows Server Essentials e acessar todos os seus recursos que estão armazenados no servidor. Isso é especialmente útil se você tiver um computador cliente que está configurado com contas de rede que podem ser usadas para se conectar a um servidor do Windows Server Essentials hospedado por meio de uma conexão VPN. Todas as contas de usuário recém-criadas no Windows Server Essentials hospedado devem usar VPN para fazer logon no computador cliente pela primeira vez.  
  
#### <a name="to-set-vpn-permissions-for-network-users"></a>Para configurar permissões de VPN para os usuários da rede  
  
1.  Abra o Dashboard.  
  
2.  Na barra de navegação, clique em **USUÁRIOS**.  
  
3.  Na lista de contas de usuário, selecione a conta de usuário que você deseja conceder permissões para acessar a área de trabalho remotamente.  
  
4.  No painel **< contas de usuário\> tarefas** , clique em **Propriedades**.  
  
5.  Na **< conta de usuário\> Propriedades**, clique na guia **acesso em qualquer lugar** .  
  
6.  Na guia **Acesso em Qualquer Local** , para permitir que um usuário se conecte ao servidor usando VPN, marque a caixa de seleção **Permitir VPN (rede privada virtual)**  .  
  
7.  Clique em **Aplicar**e clique em **OK**.  
  
##  <a name="connect-client-computers-to-the-server"></a><a name="BKMK_Connect"></a>Conectar computadores cliente ao servidor  
 Depois que a VPN estiver habilitada em um servidor que esteja executando o Windows Server Essentials para acesso remoto, você poderá usar uma conexão VPN para se conectar e acessar todos os seus recursos armazenados no servidor. Porém, primeiro você deve conectar o computador ao servidor. Quando você conecta um computador ao servidor usando o Assistente de Conexão de Computador ao Servidor, uma conexão de rede VPN é gerada automaticamente no computador cliente e pode ser usada para acessar recursos do servidor quando você trabalha em casa ou em viagens. Para obter instruções passo a passo sobre a conexão de seu computador ao servidor, consulte [Connect computers to the server](../use/Get-Connected-in-Windows-Server-Essentials.md#BKMK_9).  
  
##  <a name="use-vpn-to-connect-to-windows-server-essentials"></a><a name="BKMK_3"></a>Usar VPN para se conectar ao Windows Server Essentials  
 Se você tiver um computador cliente que está configurado com contas de rede que podem ser usadas para se conectar a um servidor hospedado executando o Windows Server Essentials por meio de uma conexão VPN, todas as contas de usuário recém-criadas no servidor hospedado devem usar VPN para fazer logon no computador cliente pela primeira vez. Conclua o procedimento a seguir no computador cliente conectado ao servidor.  
  
#### <a name="to-use-vpn-to-remotely-access-server-resources"></a>Para usar VPN para acessar remotamente os recursos do servidor  
  
1.  Pressione Ctrl + Alt + Delete no computador cliente.  
  
2.  Clique em **Trocar Usuário** na tela de logon.  
  
3.  Clique no ícone de logon de rede no canto inferior direito da tela.  
  
4.  Fazer logon na rede do Windows Server Essentials usando seu nome de usuário e senha.  
  
## <a name="see-also"></a>Consulte também  
  
-   [Trabalhar remotamente](../use/Work-Remotely-in-Windows-Server-Essentials.md)  
  
-   [Gerenciar acesso em qualquer local](Manage-Anywhere-Access-in-Windows-Server-Essentials.md)  
  
-   [Gerenciar o Windows Server Essentials](Manage-Windows-Server-Essentials.md)
