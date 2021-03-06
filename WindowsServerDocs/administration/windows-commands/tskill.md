---
title: tskill
description: Tópico de comandos do Windows para tskill, que encerra um processo em execução em uma sessão em um servidor de Host da Sessão da Área de Trabalho Remota.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 08986e6a-6900-4ece-85a1-8f73b14db1b3 Lizap
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 57a3d2c9d5ea90fafeffefd0811bb9378adbe81e
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80832459"
---
# <a name="tskill"></a>tskill

>Aplicável a: Windows Server (canal semestral), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Encerra um processo em execução em uma sessão em um servidor de Host da Sessão da Área de Trabalho Remota.
para obter exemplos de como usar esse comando, consulte [exemplos](#BKMK_examples).

> [!NOTE]
> No Windows Server 2008 R2, os Serviços de Terminal foram renomeados como Serviços de Área de Trabalho Remota. Para descobrir as novidades da versão mais recente, consulte [novidades do serviços de área de trabalho remota no Windows server 2012](https://technet.microsoft.com/library/hh831527) na biblioteca do TechNet do Windows Server.

## <a name="syntax"></a>Sintaxe
```
tskill {<ProcessID> | <ProcessName>} [/server:<ServerName>] [/id:<SessionID> | /a] [/v]
```

### <a name="parameters"></a>Parâmetros

|Parâmetro|Descrição|
|-------|--------|
|\<ProcessID >|Especifica a ID do processo que você deseja encerrar.|
|\<ProcessName >|Especifica o nome do processo que você deseja encerrar. Esse parâmetro pode incluir caracteres curinga.|
|/Server:\<ServerName >|Especifica o servidor de terminal que contém o processo que você deseja encerrar. Se **/Server** não for especificado, o servidor de host da Sessão RD atual será usado.|
|/ID:\<SessionID >|Encerra o processo que está sendo executado na sessão especificada.|
|/a|Encerra o processo que está sendo executado em todas as sessões.|
|/v|Exibe informações sobre as ações que estão sendo executadas.|
|/?|Exibe a ajuda no prompt de comando.|

## <a name="remarks"></a>Comentários
- Você pode usar **tskill** para finalizar somente os processos que pertencem a você, a menos que você seja um administrador. Os administradores têm acesso total a todas as funções **tskill** e podem finalizar processos que estão em execução em outras sessões de usuário.
- Quando todos os processos que estão sendo executados em uma sessão terminam, a sessão também termina.
- Se você usar os parâmetros *ProcessName* e **/Server:** <em>ServerName</em> , também deverá especificar o parâmetro **/ID:** <em>SessionID</em> ou **/a** .

## <a name="examples"></a><a name=BKMK_examples></a>Disso
- Para encerrar o processo 6543, digite:
  ```
  tskill 6543
  ```
- Para finalizar o Gerenciador de processos em execução na sessão 5, digite:
  ```
  tskill explorer /id:5
  ```
  ## <a name="additional-references"></a>Referências adicionais
  - [Chave de sintaxe de linha de comando](command-line-syntax-key.md)
  [referência de comando serviços de área de trabalho remota (serviços de terminal)](remote-desktop-services-terminal-services-command-reference.md)
