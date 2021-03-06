---
ms.assetid: 8c3536b7-d091-4ee6-ad04-24713f070862
title: Implantando o AD FS na organização do parceiro de conta
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 7a1d92a932638388ef50322078084c648c9dfdb9
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80853189"
---
# <a name="deploying-ad-fs-in-the-account-partner-organization"></a>Implantando o AD FS na organização do parceiro de conta

Um parceiro de conta no Serviços de Federação do Active Directory (AD FS) \(AD FS\) representa a organização na relação de confiança da Federação que armazena fisicamente as contas de usuário em um repositório de atributos com suporte. Para obter mais informações sobre quais repositórios de atributos têm suporte, consulte [a função de repositórios de atributos](../../ad-fs/technical-reference/The-Role-of-Attribute-Stores.md).  
  
O servidor de Federação na organização do parceiro de conta autentica usuários locais e cria tokens de segurança que são usados pelo parceiro de recurso para tomar decisões de autorização. Partes confiáveis, como sites e Web Services, são capazes de se registrar facilmente no servidor de Federação e consumir tokens emitidos para autenticação e controle de acesso.  
  
Em cenários em que você precisa fornecer aos usuários acesso a vários aplicativos ou serviços federados — quando cada aplicativo ou serviço é hospedado por uma organização diferente — você pode configurar o servidor de Federação de parceiro de conta para que você possa implantar várias partes confiáveis.  
  
Para obter mais informações sobre como instalar e configurar a organização do parceiro de conta, consulte [Checklist: Configuring the Account Partner Organization](../../ad-fs/deployment/Checklist--Configuring-the-Account-Partner-Organization.md).  
  
## <a name="in-this-section"></a>Nesta seção  
  
-   [Analisar a função do servidor de federação no parceiro de conta](Review-the-Role-of-the-Federation-Server-in-the-Account-Partner.md)  
  
-   [Analisar a função do proxy do servidor de federação no parceiro de conta](Review-the-Role-of-the-Federation-Server-Proxy-in-the-Account-Partner.md)  
  
-   [Preparar computadores cliente no parceiro de conta](Prepare-Client-Computers-in-the-Account-Partner.md)  
  
## <a name="see-also"></a>Consulte também
[Guia de design do AD FS no Windows Server 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)
