---
title: reset session
description: Tópico de comandos do Windows para * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 4f029ecc-874e-415a-95a8-8b731bae35f9
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 07/11/2018
ms.openlocfilehash: b83aa67e0d90be9ddc679b32c8ffa4270efec41f
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80835789"
---
# <a name="reset-session"></a>reset session

>Aplicável a: Windows Server (canal semestral), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Permite que você redefina (exclua) uma sessão em um servidor Host da Sessão da Área de Trabalho Remota (host de sessão da área de trabalho remota).  
para obter exemplos de como usar esse comando, consulte [exemplos](#BKMK_examples).  

> [!NOTE]  
> No Windows Server 2008 R2, os Serviços de Terminal foram renomeados como Serviços de Área de Trabalho Remota. Para descobrir as novidades da versão mais recente, consulte [novidades do serviços de área de trabalho remota no Windows server 2012](https://technet.microsoft.com/library/hh831527) na biblioteca do TechNet do Windows Server.  

## <a name="syntax"></a>Sintaxe  
```  
reset session {<SessionName> | <SessionID>} [/server:<ServerName>] [/v]  
```  

### <a name="parameters"></a>Parâmetros  

|Parâmetro|Descrição|  
|-------|--------|  
|\<SessionName >|Especifica o nome da sessão que você deseja redefinir. Para determinar o nome da sessão, use o comando **Query Session** .|  
|\<SessionID >|Especifica a ID da sessão a ser redefinida.|  
|/Server:\<ServerName >|Especifica o servidor de terminal que contém a sessão que você deseja redefinir. Caso contrário, o servidor host da Sessão RD atual será usado.|  
|/v|Exibe informações sobre as ações que estão sendo executadas.|  
|/?|Exibe a ajuda no prompt de comando.|  

## <a name="remarks"></a>Comentários  
-   Você sempre pode redefinir suas próprias sessões, mas deve ter permissão de acesso controle total para redefinir a sessão de outro usuário.  
-   Lembre-se de que redefinir a sessão de um usuário sem aviso o usuário pode resultar na perda de dados na sessão.  
-   Você deve redefinir uma sessão somente quando ela não está funcionando corretamente ou parece ter parado de responder.  
-   O parâmetro **/Server** será necessário apenas se você usar **Redefinir sessão** de um servidor remoto.  

## <a name="examples"></a><a name=BKMK_examples></a>Disso  
- Para redefinir a sessão de RDP designada-TCP # 6, digite:  
  ```  
  reset session rdp-tcp#6  
  ```  
- Para redefinir a sessão que usa a ID de sessão 3, digite:  
  ```  
  reset session 3  
  ```  

## <a name="additional-references"></a>Referências adicionais  
- [Chave da sintaxe de linha de comando](command-line-syntax-key.md)  
[Referência aos comandos dos Serviços de Área de Trabalho Remota (Serviços de Terminal)](remote-desktop-services-terminal-services-command-reference.md)  
