---
title: processo de consulta
description: Tópico de comandos do Windows para * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 36ce3ffc-0092-4eb1-a374-28e6616ca946
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 5ee42286691444c3a667801be3174514a81441c6
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80836959"
---
# <a name="query-process"></a>processo de consulta

>Aplicável a: Windows Server (canal semestral), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Exibe informações sobre os processos que estão sendo executados em um servidor Host da Sessão da Área de Trabalho Remota (host de Sessão RD).
Você pode usar esse comando para descobrir quais programas um usuário específico está executando e também quais usuários estão executando um programa específico.
para obter exemplos de como usar esse comando, consulte [exemplos](#BKMK_examples).
> [!NOTE]
> No Windows Server 2008 R2, os Serviços de Terminal foram renomeados como Serviços de Área de Trabalho Remota. Para descobrir as novidades da versão mais recente, consulte [novidades do serviços de área de trabalho remota no Windows server 2012](https://technet.microsoft.com/library/hh831527) na biblioteca do TechNet do Windows Server.
> ## <a name="syntax"></a>Sintaxe
> ```
> query process [* | <ProcessID> | <UserName> | <SessionName> | /id:<nn> | <ProgramName>] [/server:<ServerName>]
> ```
> ### <a name="parameters"></a>Parâmetros
> 
> |      Parâmetro       |                                                                 Descrição                                                                  |
> |----------------------|----------------------------------------------------------------------------------------------------------------------------------------------|
> |          \*          |                                                    lista os processos para todas as sessões.                                                     |
> |     <ProcessID>      |                                   Especifica a ID numérica que identifica o processo que você deseja consultar.                                   |
> |      <UserName>      |                                       Especifica o nome do usuário cujos processos você deseja listar.                                       |
> |    <SessionName>     |                                     Especifica o nome da sessão cujos processos você deseja listar.                                      |
> |       /ID:<nn>       |                                      Especifica a ID da sessão cujos processos você deseja listar.                                       |
> |    <ProgramName>     |                     Especifica o nome do programa cujos processos você deseja consultar. A extensão. exe é necessária.                     |
> | /server:<ServerName> | Especifica o servidor de host da sessão da área de trabalho remota cujos processos você deseja listar. Se não for especificado, o servidor no qual você está conectado no momento será usado. |
> |          /?          |                                                     Exibe a ajuda no prompt de comando.                                                     |
> 
> ## <a name="remarks"></a>Comentários
> - Os administradores têm acesso completo a todas as funções de **processo de consulta** .
> - Se você não especificar o < de*nome de usuário*>, <*SessionName*>, **/ID:** <*NN*>, <*programaname*> ou parâmetros **\\** *, o **processo de consulta** exibirá somente os processos que pertencem ao usuário atual.
> - se uma sessão for especificada, ela deverá identificar uma sessão ativa.
> - o **processo de consulta** retorna as seguintes informações:
>   -   O usuário que possui o processo
>   -   A sessão que possui o processo
>   -   A ID da sessão
>   -   O nome do processo
>   -   A ID do processo
> - Quando o **processo de consulta** retorna informações, um símbolo maior que (>) é exibido antes de cada processo pertencente à sessão atual.
>   ## <a name="examples"></a><a name=BKMK_examples></a>Disso
> - Para exibir informações sobre os processos que estão sendo usados por todas as sessões, digite:
>   ```
>   query process *
>   ```
> - Para exibir informações sobre os processos que estão sendo usados pela ID de sessão 2, digite:
>   ```
>   query process /ID:2
>   ```
>   ## <a name="additional-references"></a>Referências adicionais
>   - [Chave de sintaxe de linha de comando](command-line-syntax-key.md)
>   
>   [consultar](query.md) a [referência de comando serviços de área de trabalho remota (serviços de terminal)](remote-desktop-services-terminal-services-command-reference.md)
