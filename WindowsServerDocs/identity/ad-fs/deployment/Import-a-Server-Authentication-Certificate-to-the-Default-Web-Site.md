---
ms.assetid: e1f2ce2d-b24f-4ccd-8add-9e69419fc6c1
title: Importar um Certificado de Autenticação de Servidor para o site padrão
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 3f02358167b024247f934a46218028575e393ba9
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80855399"
---
# <a name="import-a-server-authentication-certificate-to-the-default-web-site"></a>Importar um Certificado de Autenticação de Servidor para o site padrão

Depois de obter um certificado de autenticação de servidor de uma autoridade de certificação \(\)de AC, você deve instalar manualmente esse certificado no site padrão para cada servidor de Federação ou proxy de servidor de Federação em um farm de servidores.  
  
Para servidores Web, instale manualmente o certificado de autenticação de servidor no site ou no diretório virtual apropriado em que reside seu aplicativo federado.  
  
Se estiver configurando um farm, assegure-se de realizar esse procedimento de forma idêntica — usando exatamente as mesmas configurações — em cada um dos servidores em seu farm.  
  
> [!NOTE]  
> O\-snap de gerenciamento de AD FS no refere-se aos certificados de autenticação de servidor para servidores de Federação como certificados de comunicação de serviço.  
  
A associação em **Administradores**, ou equivalente, no computador local é o mínimo necessário para concluir este procedimento.  Examine os detalhes sobre como usar as contas apropriadas e as associações de grupo em [grupos padrão e de domínio](https://go.microsoft.com/fwlink/?LinkId=83477).   
  
### <a name="to-import-a-server-authentication-certificate-to-the-default-web-site"></a>Para importar um certificado de autenticação de servidor para o Site Padrão  
  
1.  Na tela **Iniciar** , digite**serviços de informações da Internet \(o Gerenciador de\) do IIS**e pressione Enter.  
  
2.  Na árvore de console, clique em **ComputerName**.  
  
3.  No painel central, clique duas vezes\-em **certificados de servidor**.  
  
4.  No painel **Ações**, clique em **Importar**.  
  
5.  Na caixa de diálogo **importar certificado** , clique em **..** . .  
  
6.  Navegue para o local do arquivo do certificado pfx, realce-o e, em seguida, clique em **Abrir**.  
  
7.  Digite uma senha para o certificado e, em seguida, clique em **OK**.  
  
## <a name="additional-references"></a>Referências adicionais  
[Lista de verificação: Configurando um servidor de Federação](Checklist--Setting-Up-a-Federation-Server.md)  
  
[Lista de verificação: Configurando um proxy de servidor de Federação](Checklist--Setting-Up-a-Federation-Server-Proxy.md)  
  
[Requisitos de certificado para servidores de federação](https://technet.microsoft.com/library/dd807040.aspx)  
  
[Requisitos de certificado para proxies do servidor de federação](https://technet.microsoft.com/library/dd807054.aspx)  
   
  

