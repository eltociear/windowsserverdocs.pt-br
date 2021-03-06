---
title: Criar certificados raiz para autenticação de VPN com o Azure AD
description: O Azure AD usa o certificado VPN para assinar certificados emitidos para clientes Windows 10 ao autenticar no Azure AD para conectividade de VPN. O certificado marcado como primário é o emissor que o AD do Azure usa.
ms.prod: windows-server
ms.technology: networking-ras
ms.topic: article
ms.date: 06/28/2019
ms.author: v-tea
author: Teresa-MOTIV
ms.localizationpriority: medium
ms.reviewer: deverette
ms.openlocfilehash: f4501c244726ee9b23a6d517c4b835f0c9418302
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80818799"
---
# <a name="step-72-create-conditional-access-root-certificates-for-vpn-authentication-with-azure-ad"></a>Etapa 7.2. Criar certificados raiz de acesso condicional para autenticação VPN com o Azure AD

>Aplica-se a: Windows Server (canal semestral), Windows Server 2016, Windows Server 2012 R2, Windows 10

- [**Anterior:** Etapa 7,1. Configurar o EAP-TLS para ignorar a verificação da CRL (lista de certificados revogados)](vpn-config-eap-tls-to-ignore-crl-checking.md)
- [**Em seguida:** Etapa 7,3. Configurar a política de acesso condicional](vpn-config-conditional-access-policy.md)

Nesta etapa, você configura certificados raiz de acesso condicional para autenticação VPN com o Azure AD, que cria automaticamente um aplicativo de nuvem chamado servidor VPN no locatário. Para configurar o acesso condicional para conectividade VPN, você precisa:

1. Crie um certificado VPN no portal do Azure.
2. Baixe o certificado VPN.
3. Implante o certificado nos servidores VPN e NPS.

> [!IMPORTANT]
> Depois que um certificado VPN for criado na portal do Azure, o Azure AD começará a usá-lo imediatamente para emitir certificados de vida curta para o cliente VPN. É fundamental que o certificado VPN seja implantado imediatamente no servidor VPN para evitar problemas com a validação de credenciais do cliente VPN.

Quando um usuário tenta uma conexão VPN, o cliente VPN faz uma chamada para o WAM (Web Account Manager) no cliente Windows 10. O WAM faz uma chamada para o aplicativo de nuvem do servidor VPN. Quando as condições e os controles na política de acesso condicional são satisfeitos, o Azure AD emite um token na forma de um certificado de curta duração (1 hora) para o WAM. O WAM coloca o certificado no repositório de certificados do usuário e passa o controle para o cliente VPN.  

Em seguida, o cliente VPN envia os problemas de certificado pelo Azure AD para a VPN para validação de credenciais.  

> [!NOTE]
> O Azure AD usa o certificado criado mais recentemente na folha de conectividade de VPN como o emissor.

**Procedure**

1. Entre em seu [portal do Azure](https://portal.azure.com) como um administrador global.
2. No menu à esquerda, clique em **Azure Active Directory**.
3. Na página **Azure Active Directory** , na seção **gerenciar** , clique em **acesso condicional**.
4. Na página **acesso condicional** , na seção **gerenciar** , clique em **conectividade VPN (versão prévia)** .
5. Na página **conectividade VPN** , clique em **novo certificado**.
6. Na página **novo** , execute as seguintes etapas: a. Para **selecionar duração**, selecione 1, 2 ou 3 anos.
   b. Selecione **Criar**.

## <a name="next-steps"></a>{1&gt;{2&gt;Próximas etapas&lt;2}&lt;1}

[Etapa 7,3. Configurar a política de acesso condicional](vpn-config-conditional-access-policy.md): nesta etapa, você configura a política de acesso condicional para conectividade VPN.
