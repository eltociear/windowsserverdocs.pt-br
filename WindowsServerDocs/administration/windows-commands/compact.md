---
title: Compact
description: O tópico de comandos do Windows para Compact, que exibe ou altera a compactação de arquivos ou diretórios em partições NTFS.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 429b3752-df0a-43a4-a210-df2f3ad03c3b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e9e6a3ba71ecc0c8e264ac4af8dc1da42d23fdc2
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80847349"
---
# <a name="compact"></a>Compact

Exibe ou altera a compactação de arquivos ou diretórios em partições NTFS. Se usado sem parâmetros, **Compact** exibe o estado de compactação do diretório atual e os arquivos que ele contém.

Para obter exemplos de como usar esse comando, consulte [Exemplos](#BKMK_examples).

## <a name="syntax"></a>Sintaxe

```
compact [/c | /u] [/s[:<Dir>]] [/a] [/i] [/f] [/q] [<FileName>[...]]
```

### <a name="parameters"></a>Parâmetros

|Parâmetro|Descrição|
|---------|-----------|
|/c|Compacta o diretório ou arquivo especificado.|
|/u|Descompacta o diretório ou arquivo especificado.|
|/s [:\<dir >]|Aplica o comando **Compact** a todos os subdiretórios do diretório especificado (ou do diretório atual, se nenhum for especificado).|
|/a|Exibe arquivos ocultos ou do sistema.|
|/i|Ignora erros.|
|/f|Força a compactação ou descompactação do diretório ou arquivo especificado. **/f** é usado no caso de um arquivo que foi parcialmente compactado quando a operação foi interrompida por uma falha do sistema. Para forçar o arquivo a ser compactado em sua totalidade, use os parâmetros **/c** e **/f** e especifique o arquivo parcialmente compactado.|
|/q|Relata apenas as informações mais essenciais.|
|\<nome de arquivo >|Especifica o arquivo ou diretório. Você pode usar vários nomes de arquivo e o **&#42;** e o **?** caracteres curinga.|
|/?|Exibe a ajuda no prompt de comando.|

## <a name="remarks"></a>Comentários

-   O comando **Compact** é a versão de linha de comando do recurso de compactação do sistema de arquivos NTFS. O estado de compactação de um diretório indica se os arquivos são compactados automaticamente quando são adicionados ao diretório. Definir o estado de compactação de um diretório não altera necessariamente o estado de compactação dos arquivos que já estão no diretório.
-   Você não pode usar o **Compact** para ler, gravar ou montar volumes que foram compactados usando o DriveSpace ou o DoubleSpace.
-   Você não pode usar o **Compact** para compactar partições FAT (tabela de alocação de arquivos) ou FAT32.

## <a name="examples"></a><a name=BKMK_examples></a>Disso

Para definir o estado de compactação do diretório atual, seus subdiretórios e arquivos existentes, digite:
```
compact /c /s 
```
Para definir o estado de compactação de arquivos e subdiretórios no diretório atual, sem alterar o estado de compactação do próprio diretório atual, digite:
```
compact /c /s *.*
```
Para compactar um volume, no diretório raiz do volume, digite:
```
compact /c /i /s:\
```

> [!NOTE]
> Este exemplo define o estado de compactação de todos os diretórios (incluindo o diretório raiz no volume) e compacta todos os arquivos no volume. O parâmetro **/i** impede que mensagens de erro interrompam o processo de compactação.

Para compactar todos os arquivos com a extensão de nome de arquivo. bmp no diretório \tmp e todos os subdiretórios de \tmp, sem modificar o atributo compactado dos diretórios, digite:
```
compact /c /s:\tmp *.bmp
```
Para forçar a compactação completa do arquivo pretas. bmp, que foi parcialmente compactado durante uma falha do sistema, digite:
```
compact /c /f zebra.bmp
```
Para remover o atributo compactado do diretório C:\Tmp, sem alterar o estado de compactação de todos os arquivos nesse diretório, digite:
```
compact /u c:\tmp
```

## <a name="additional-references"></a>Referências adicionais

- [Chave da sintaxe de linha de comando](command-line-syntax-key.md)