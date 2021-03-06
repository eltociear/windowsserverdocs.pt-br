---
title: Reg Compare
description: Tópico de comandos do Windows para * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 177dc6a3-034e-4846-a394-330d03c14e0b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 21eb459711f8ca72bf2f6d841d958bb25a96f845
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80836539"
---
# <a name="reg-compare"></a>Reg Compare



Compara as entradas ou subchaves do registro especificadas.

Para obter exemplos de como usar esse comando, consulte [Exemplos](#BKMK_examples).

## <a name="syntax"></a>Sintaxe

```
reg compare <KeyName1> <KeyName2> [{/v ValueName | /ve}] [{/oa | /od | /os | on}] [/s]
```

### <a name="parameters"></a>Parâmetros

|    Parâmetro    |                                                                                                                                                                                                                                                                                          Descrição                                                                                                                                                                                                                                                                                           |
|-----------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|   \<KeyName1 >   |                                                               Especifica o caminho completo da primeira subchave a ser comparada. Para especificar um computador remoto, inclua o nome do computador (no formato \\\\ComputerName\) como parte do *KeyName*. Omitir \\\\computername \ faz com que a operação seja padronizada para o computador local. O *KeyName* deve incluir uma chave de raiz válida. As chaves de raiz válidas para o computador local são: HKLM, HKCU, HKCR, HKU e HKCC. Se um computador remoto for especificado, as chaves de raiz válidas serão: HKLM e HKU.                                                                |
|   \<KeyName2 >   | Especifica o caminho completo da segunda subchave a ser comparada. Para especificar um computador remoto, inclua o nome do computador (no formato \\\\ComputerName\) como parte do *KeyName*. Omitir \\\\computername \ faz com que a operação seja padronizada para o computador local. Especificar apenas o nome do computador em *KeyName2* faz com que a operação use o caminho para a subchave especificada em *KeyName1*. O *KeyName* deve incluir uma chave de raiz válida. As chaves de raiz válidas para o computador local são: HKLM, HKCU, HKCR, HKU e HKCC. Se um computador remoto for especificado, as chaves de raiz válidas serão: HKLM e HKU. |
| /v \<valueName > |                                                                                                                                                                                                                                                                     Especifica o nome do valor a ser comparado sob a subchave.                                                                                                                                                                                                                                                                      |
|       /ve       |                                                                                                                                                                                                                                                         Especifica que somente as entradas que têm um nome de valor nulo devem ser comparadas.                                                                                                                                                                                                                                                         |
|      [{/oa      |                                                                                                                                                                                                                                                                                              /OD                                                                                                                                                                                                                                                                                               |
|       /oa       |                                                                                                                                                                                                                                             Especifica que todas as diferenças e correspondências são exibidas. Por padrão, somente as diferenças são listadas.                                                                                                                                                                                                                                             |
|       /OD       |                                                                                                                                                                                                                                                          Especifica que apenas as diferenças são exibidas. Esse é o comportamento padrão.                                                                                                                                                                                                                                                          |
|       /os       |                                                                                                                                                                                                                                                    Especifica que somente as correspondências são exibidas. Por padrão, somente as diferenças são listadas.                                                                                                                                                                                                                                                     |
|       /on       |                                                                                                                                                                                                                                                       Especifica que nada é exibido. Por padrão, somente as diferenças são listadas.                                                                                                                                                                                                                                                        |
|       /s        |                                                                                                                                                                                                                                                                         Compara todas as subchaves e entradas recursivamente.                                                                                                                                                                                                                                                                          |
|       /?        |                                                                                                                                                                                                                                                                    Exibe a ajuda para **reg Compare** no prompt de comando.                                                                                                                                                                                                                                                                    |

## <a name="remarks"></a>Comentários

A tabela a seguir lista os valores de retorno para **reg Compare**.

|{1&gt;Valor&lt;1}|Descrição|
|-----|-----------|
|0|A comparação é bem-sucedida e o resultado é idêntico.|
|1|Falha na comparação.|
|2|A comparação foi bem-sucedida e foram encontradas diferenças.|

A tabela a seguir lista os símbolos exibidos nos resultados.

|Símbolo|Descrição|
|------|-----------|
|=|Os dados de *KeyName1* são iguais aos dados de *KeyName2* .|
|<|Os dados de *KeyName1* são menores que os dados de *KeyName2* .|
|>|Os dados de *KeyName1* são maiores que os dados de *KeyName2* .|

## <a name="examples"></a><a name=BKMK_examples></a>Disso

Para comparar todos os valores na chave **MyApp** com todos os valores na chave **SaveMyApp**, digite:

REG COMPARE HKLM\Software\MyCo\MyApp HKLM\Software\MyCo\SaveMyApp

Para comparar o valor da versão sob a chave **MYCO** e o valor da versão sob a chave **MyCo1**, digite:

REG COMPARE HKLM\Software\MyCo HKLM\Software\MyCo1/v versão

Para comparar todas as subchaves e valores em HKLM\Software\MyCo no computador chamado ZODIAC com todas as subchaves e valores em HKLM\Software\MyCo no computador local, digite:

REG COMPARE \\\\ZODIAC\HKLM\Software\MyCo \\\\. /s

## <a name="additional-references"></a>Referências adicionais

- [Chave da sintaxe de linha de comando](command-line-syntax-key.md)