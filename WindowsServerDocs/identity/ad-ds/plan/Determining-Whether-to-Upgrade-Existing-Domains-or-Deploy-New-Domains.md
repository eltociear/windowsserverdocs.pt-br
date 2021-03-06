---
ms.assetid: c20231dd-2b83-4494-9385-1172272e00d6
title: Determinando se é necessário atualizar domínios existentes ou implantar novos domínios
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: 1e058240bc971d949de279407701e57cd021712c
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80822590"
---
# <a name="determining-whether-to-upgrade-existing-domains-or-deploy-new-domains"></a>Determinando se é necessário atualizar domínios existentes ou implantar novos domínios

>Aplica-se a: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Cada domínio em seu design será um novo domínio ou um domínio atualizado existente. Os usuários de domínios existentes que você não atualizar devem ser movidos para novos domínios.  
  
A movimentação de contas entre domínios pode afetar os usuários finais. Antes de decidir se deseja mover os usuários para um novo domínio ou para atualizar os domínios existentes, avalie os benefícios administrativos de longo prazo de um novo domínio de AD DS em relação ao custo de mover os usuários para o domínio.  
  
Para obter mais informações sobre como atualizar domínios de Active Directory para o Windows Server 2008, consulte [atualizando domínios de Active Directory para domínios do Windows server 2008 e do Windows server 2008 R2 AD DS](https://technet.microsoft.com/library/cc731188.aspx).  
  
Para obter mais informações sobre como reestruturar AD DS domínios dentro e entre florestas, consulte Active Directory ferramenta de migração versão 3,1 Guia de migração ([https://go.microsoft.com/fwlink/?LinkId=93678](https://go.microsoft.com/fwlink/?LinkId=93678)).  
  
Para uma planilha para ajudá-lo a documentar seus planos para domínios novos e atualizados, baixe Job_Aids_Designing_and_Deploying_Directory_and_Security_Services. zip de auxílios de trabalho para o Windows Server 2003 Deployment Kit ([https://go.microsoft.com/fwlink/?LinkID=102558](https://go.microsoft.com/fwlink/?LinkID=102558)) e abra "planejamento de domínio" (DSSLOGI_5. doc).  
  


