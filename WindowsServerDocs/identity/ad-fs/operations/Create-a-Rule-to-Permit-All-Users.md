---
ms.assetid: 8c179884-f0d9-4c7a-973d-820119cf3c38
title: Criar uma regra para permitir todos os usuários
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 894857813115002f3998a9ab5000d57b944fd448
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80816779"
---
# <a name="create-a-rule-to-permit-all-users"></a>Criar uma regra para permitir todos os usuários

No Windows Server 2016, você pode usar uma **política de controle de acesso** para criar uma regra que dará a todos os usuários acesso a uma terceira parte confiável.  No Windows Server 2012 R2, usando o modelo de regra **permitir todos os usuários** no Serviços de Federação do Active Directory (AD FS) \(AD FS\), você pode criar uma regra de autorização que dará a todos os usuários acesso à terceira parte confiável. 

Você pode usar regras de autorização adicionais para restringir ainda mais o acesso. Usuários com permissão de acesso à terceira parte confiável do Serviço de Federação ainda podem ter o serviço negado pela terceira parte confiável.  
  
Você pode usar os procedimentos a seguir para criar uma regra de declaração com o snap\-de gerenciamento de AD FS no.  
  
A associação em **Administradores**, ou equivalente, no computador local é o mínimo necessário para concluir este procedimento.  Examine os detalhes sobre como usar as contas apropriadas e as associações de grupo em [grupos padrão e de domínio](https://go.microsoft.com/fwlink/?LinkId=83477). 

## <a name="to-create-a-rule-to-permit-all-users-in-windows-server-2016"></a>Para criar uma regra para permitir todos os usuários no Windows Server 2016

1.  Em Gerenciador do Servidor, clique em **ferramentas**e, em seguida, selecione **Gerenciamento de AD FS**.  
  
2.  Na árvore de console, em **AD FS**, clique em **relações de confiança**de terceira parte confiável. 
![criar](media/Create-a-Rule-to-Permit-All-Users/permitall1.PNG) de regra

3.  Clique com o botão direito do mouse na **relação de confiança** de terceira parte confiável à qual você deseja permitir acesso e selecione **Editar política de controle de acesso**.  
![criar](media/Create-a-Rule-to-Permit-All-Users/permitall2.PNG) de regra

4. Na política de controle de acesso, selecione **permitir todos** e, em seguida, clique em **aplicar** e em **OK**.
![criar](media/Create-a-Rule-to-Permit-All-Users/permitall3.PNG) de regra
  
## <a name="to-create-a-rule-to-permit-all-users-in-windows-server-2012-r2"></a>Para criar uma regra para permitir todos os usuários no Windows Server 2012 R2 
  
1.  Em Gerenciador do Servidor, clique em **ferramentas**e, em seguida, selecione **Gerenciamento de AD FS**.  
  
2.  Na árvore de console, em **AD FS\\relações de confiança\\confianças**de terceira parte confiável, clique em uma relação de confiança específica na lista em que você deseja criar essa regra.  

3.  À direita\-clique na relação de confiança selecionada e, em seguida, clique em **Editar regras de declaração**.  
![criar](media/Create-a-Rule-to-Permit-All-Users/permitall4.PNG) de regra  

4.  Na caixa de diálogo **Editar regras de declaração** , clique na guia **regras de autorização de emissão** ou na guia regras de autorização de **delegação** \(com base no tipo de regra de autorização que você precisa\)e, em seguida, clique em **Adicionar regra** para iniciar o **Assistente para Adicionar regra de declaração de autorização**.  
![criar](media/Create-a-Rule-to-Permit-All-Users/permitall5.PNG) de regra  
5.  Na página **selecionar modelo de regra** , em **modelo de regra de declaração**, selecione **permitir todos os usuários** na lista e clique em **Avançar**.  
![criar](media/Create-a-Rule-to-Permit-All-Users/permitall6.PNG) de regra    
6.  Na página **Configurar regra** , clique em **concluir**.  
  
7.  Na caixa de diálogo **Editar regras de declaração** , clique em **OK** para salvar a regra.  

## <a name="additional-references"></a>Referências adicionais 
[Configurar regras de declaração](Configure-Claim-Rules.md)  
 
[Lista de verificação: Criando regras de declaração para uma terceira parte confiável](https://technet.microsoft.com/library/ee913578.aspx)  
  
[Quando usar uma regra de declaração de autorização](../../ad-fs/technical-reference/When-to-Use-an-Authorization-Claim-Rule.md)  

[A função das declarações](../../ad-fs/technical-reference/The-Role-of-Claims.md)  
  
[A função das regras de declaração](../../ad-fs/technical-reference/The-Role-of-Claim-Rules.md)  
