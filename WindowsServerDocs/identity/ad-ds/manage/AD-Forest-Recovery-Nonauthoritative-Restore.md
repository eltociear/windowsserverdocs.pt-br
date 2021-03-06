---
title: Recuperação de floresta do AD-restauração não autoritativa
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.prod: windows-server
ms.assetid: e4ce1d18-d346-492a-8bca-f85513aa3ac1
ms.technology: identity-adds
ms.openlocfilehash: 4fe4905bba944c86d168eaa46ae699ad25ba0194
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80823949"
---
# <a name="performing-a-nonauthoritative-restore-of-active-directory-domain-services"></a>Executando uma restauração não autoritativa de Active Directory Domain Services 

>Aplica-se a: Windows Server 2016, Windows Server 2012 e 2012 R2, Windows Server 2008 e 2008 R2

Para executar uma restauração não autoritativa, conclua o procedimento a seguir.  
  
Os procedimentos a seguir usam o Wbadmin. exe para executar uma restauração não autoritativa de Active Directory ou Active Directory Domain Services (AD DS). Se você estiver usando uma solução de backup diferente ou se pretender concluir a restauração autoritativa do SYSVOL mais tarde no processo de recuperação de floresta, poderá executar uma restauração autoritativa do SYSVOL usando estes métodos alternativos:  
  
- Se você estiver usando o FRS (serviço de replicação de arquivo) para replicar o SYSVOL, siga as etapas no [artigo 290762](https://go.microsoft.com/fwlink/?LinkId=148443) da base de dados de conhecimento Microsoft, usando a chave do registro **BurFlags** para reinicializar os conjuntos de réplicas do FRS ou, se necessário, o artigo 315457 [315457](https://support.microsoft.com/kb/315457)para recriar a árvore SYSVOL. Para determinar se o SYSVOL é replicado pelo FRS, consulte [determinando se a pasta SYSVOL do controlador de domínio é replicada pelo DFSR ou pelo FRS](https://msdn.microsoft.com/library/windows/desktop/cc507518.aspx#determining_whether_a_domain_controller_s_sysvol_folder_is_replicated_by_dfsr_or_frs).  
- Se você estiver usando a replicação do Sistema de Arquivos Distribuído (DFS) para replicar o SYSVOL, consulte [executar uma sincronização autoritativa de SYSVOL replicado pelo DFSR](AD-Forest-Recovery-Authoritative-Recovery-SYSVOL.md).  

## <a name="performing-a-nonauthoritative-restore"></a>Executando uma restauração não autoritativa

Use o procedimento a seguir para executar uma restauração não autoritativa de AD DS e uma restauração autoritativa do SYSVOL ao mesmo tempo usando o Wbadmin. exe em um DC que executa o Windows Server 2012, o Windows Server 2008 R2 ou o Windows Server 2008. O backup deve incluir explicitamente os dados de estado do sistema; um backup de servidor completo que é usado para a recuperação de servidor completa não funcionará. Para obter mais informações sobre como criar um backup de estado do sistema, consulte [fazendo backup dos dados de estado do sistema](AD-Forest-Recovery-Backing-up-System-State.md).  
  
### <a name="to-perform-a-nonauthoritative-restore-of-ad-ds-and-authoritative-restore-of-sysvol-using-wbadminexe"></a>Para executar uma restauração não autoritativa de AD DS e restauração autoritativa de SYSVOL usando Wbadmin. exe  
  
- Inclua a opção **-authsysvol** no comando de recuperação, conforme mostrado no exemplo a seguir:  

   ```  
   wbadmin start systemstaterecovery <otheroptions> -authsysvol  
   ```  

   Por exemplo:  

   ```  
   wbadmin start systemstaterecovery -version:11/20/2012-13:00 -authsysvol  
   ```  
  
![Restauração](media/AD-Forest-Recovery-Nonauthoritative-Restore/nonauth.png)

## <a name="next-steps"></a>{1&gt;{2&gt;Próximas etapas&lt;2}&lt;1}

- [Guia de recuperação de floresta do AD](AD-Forest-Recovery-Guide.md)
- [Recuperação de floresta do AD – Procedimentos](AD-Forest-Recovery-Procedures.md)
