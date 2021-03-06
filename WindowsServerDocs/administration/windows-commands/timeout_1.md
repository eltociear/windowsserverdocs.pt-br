---
title: timeout
description: O tópico de comandos do Windows para tempo limite, que pausa o processador de comandos para o número de segundos especificado.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: e26b4a84-0e30-46e1-aa10-0667b7d3cb4c
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: bd0a43e49e8a7567ac975333b04a9e6f549a0fd8
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80832809"
---
# <a name="timeout"></a>timeout

Pausa o processador de comandos para o número de segundos especificado.

Para obter exemplos de como usar esse comando, consulte [Exemplos](#BKMK_examples).

## <a name="syntax"></a>Sintaxe

```
timeout /t <TimeoutInSeconds> [/nobreak] 
```

### <a name="parameters"></a>Parâmetros

|Parâmetro|Descrição|
|---------|-----------|
|/t \<TimeoutInSeconds >|Especifica o número decimal de segundos (entre-1 e 99999) a aguardar antes do processamento do processador de comando continuar. O valor-1 faz com que o computador aguarde indefinidamente por um pressionamento de tecla.|
|/nobreak|Especifica para ignorar os traços de tecla do usuário.|
|/?|Exibe a ajuda no prompt de comando.|

## <a name="remarks"></a>Comentários

-   O comando **Timeout** normalmente é usado em arquivos em lotes.
-   Um pressionamento de tecla do usuário retoma a execução do processador de comando imediatamente, mesmo que o período de tempo limite não tenha expirado.
-   Quando usado em conjunto com o comando **Sleep** , o **tempo limite** é semelhante ao comando **Pause** .

## <a name="examples"></a><a name=BKMK_examples></a>Disso

Para pausar o processador de comandos por dez segundos, digite:
```
timeout /t 10
```
Para pausar o processador de comando por 100 segundos e ignorar qualquer pressionamento de tecla, digite:
```
timeout /t 100 /nobreak
```
Para pausar o processador de comandos indefinidamente até que uma tecla seja pressionada, digite:
```
timeout /t -1
```

## <a name="additional-references"></a>Referências adicionais

- [Chave da sintaxe de linha de comando](command-line-syntax-key.md)
