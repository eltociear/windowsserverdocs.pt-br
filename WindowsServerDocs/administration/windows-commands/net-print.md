---
title: Net print
description: Tópico de comandos do Windows para * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: f59b2015-4698-415d-9a74-09566c466f40
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ad631788a59c24dcb92d180330de25a5be320154
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80839049"
---
# <a name="net-print"></a>Net print

>Aplicável a: Windows Server (canal semestral), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Exibe informações sobre uma fila de impressora especificada ou um trabalho de impressão especificado, ou controla um trabalho de impressão especificado.
para obter exemplos de como usar esse comando, consulte a seção de [exemplos](#BKMK_examples) deste documento.
> [!NOTE]
> Esse comando foi preterido no Windows 7 e no Windows Server 2008 R2. No entanto, você pode executar muitas das mesmas tarefas usando o prnjobs, Instrumentação de Gerenciamento do Windows (WMI) ou cmdlets do Windows PowerShell. Para obter mais informações, consulte [prnjobs](prnjobs.md), [Instrumentação de gerenciamento do Windows](https://go.microsoft.com/fwlink/?LinkID=29991) (https://go.microsoft.com/fwlink/?LinkID=29991), [Windows PowerShell](https://go.microsoft.com/fwlink/?LinkID=128426) (https://go.microsoft.com/fwlink/?LinkID=128426)e a [galeria de script Center do TechNet](https://go.microsoft.com/fwlink/?LinkId=164635) (https://go.microsoft.com/fwlink/?LinkId=164635).
> ## <a name="syntax"></a>Sintaxe
> ```
> Net print {\\<computerName>\<Sharename> | 
> \\<computerName> <JobNumber> [/hold | /release | /delete]} [help]
> ```
> ### <a name="parameters"></a>Parâmetros
> 
> |               Parâmetros               |                                                                                                                                                                                                                     Descrição                                                                                                                                                                                                                      |
> |----------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
> |    \\\\<computerName>\\<Sharename>     |                                                                                                                                                                            Especifica (por nome) o computador e a fila de impressão sobre os quais você deseja exibir informações.                                                                                                                                                                             |
> |           \\\\<computerName>           |                                                                                                                                 Especifica (por nome) o computador que hospeda o trabalho de impressão que você deseja controlar. Se você não especificar um computador, o computador local será assumido. Requer o parâmetro <JobNumber>.                                                                                                                                  |
> |              <JobNumber>               |                                             Especifica o número do trabalho de impressão que você deseja controlar. Esse número é atribuído pelo computador que hospeda a fila de impressão onde o trabalho de impressão é enviado. Depois que um computador atribui um número a um trabalho de impressão, esse número não é atribuído a outros trabalhos de impressão em nenhuma fila hospedada por esse computador. Necessário ao usar o parâmetro \\\\<computerName>.                                             |
> | [/Hold &#124; /Release &#124; /DELETE] | Especifica a ação a ser tomada com o trabalho de impressão.<p>-O parâmetro **/Hold** atrasa o trabalho, permitindo que outros trabalhos de impressão o ignorem até que sejam liberados.<br />-O parâmetro **/Release** libera um trabalho de impressão que foi atrasado.<br />-O parâmetro **/delete** remove um trabalho de impressão de uma fila de impressão.<p>Se você especificar um número de trabalho, mas não especificar nenhuma ação, as informações sobre o trabalho de impressão serão exibidas. |
> |                  ajuda                  |                                                                                                                                                                                                     Exibe a ajuda para o comando **net Print** .                                                                                                                                                                                                     |
> 
> ## <a name="remarks"></a>Comentários
> - \\de **impressão de rede** \\<computerName> exibe informações sobre trabalhos de impressão em uma fila de impressora compartilhada. Veja a seguir um exemplo de um relatório para todos os trabalhos de impressão em uma fila para uma impressora compartilhada chamada LASER:
>   ```
>   printers at \\PRODUCTION
>   Name              Job #      Size      Status
>   -----------------------------
>   LASER Queue       3 jobs               *printer active*
>      USER1          84        93844      printing
>      USER2          85        12555      Waiting
>      USER3          86        10222      Waiting
>   ```
> - Veja a seguir um exemplo de um relatório para um trabalho de impressão:
>   ```
>   Job #            35
>   Status           Waiting
>   Size             3096
>   remark
>   Submitting user  USER2
>   Notify           USER2
>   Job data type
>   Job parameters
>   additional info
>   ```
>   ## <a name="examples"></a><a name=BKMK_examples></a>Disso
>   Este exemplo mostra como listar o conteúdo da fila de impressão Dotmatrix no computador \\\Production:
>   ```
>   Net print \\Production\Dotmatrix 
>   ```
>   Este exemplo mostra como exibir informações sobre o número de trabalho 35 no computador \\\Production:
>   ```
>   Net print \\Production 35 
>   ```
>   Este exemplo mostra como atrasar o número do trabalho 263 no computador \\\Production:
>   ```
>   Net print \\Production 263 /hold 
>   ```
>   Este exemplo mostra como liberar o número do trabalho 263 no computador \\\Production:
>   ```
>   Net print \\Production 263 /release 
>   ```
>   ## <a name="additional-references"></a>Referências adicionais
>   - [Chave de sintaxe de linha de comando](command-line-syntax-key.md)
>   [referência de comando de impressão](print-command-reference.md)
