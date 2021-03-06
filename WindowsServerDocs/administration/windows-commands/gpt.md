---
title: GPT
description: Tópico de comandos do Windows para * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 1d6f9029-807f-4420-a336-36669b5361bc
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1db2a3fe21b0343c23bbc2432d4d07a500b72e8e
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80842449"
---
# <a name="gpt"></a>GPT

>Aplicável a: Windows Server (canal semestral), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Em discos básicos da tabela de partição GUID (GPT), o atribui os atributos GPT à partição com foco.  os atributos de partição GPT fornecem informações adicionais sobre o uso da partição. Alguns atributos são específicos para o GUID do tipo de partição.

> [!CAUTION]
> Alterar os atributos de GPT pode fazer com que os volumes de dados básicos não recebam letras de unidade ou impeçam que o sistema de arquivos seja montado. Você não deve alterar os atributos de GPT, a menos que seja um fabricante de equipamento original (OEM) ou um profissional de ti que tenha experiência com discos GPT.

## <a name="syntax"></a>Sintaxe

```
gpt attributes=<n>
```

### <a name="parameters"></a>Parâmetros

|   Parâmetro    |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               Descrição                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
|----------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| atributos =<n> | Especifica o valor do atributo que você deseja aplicar à partição com foco. O campo atributo GPT é um campo de 64 bits que contém dois subcampos. O campo superior é interpretado apenas no contexto da ID da partição, enquanto o campo inferior é comum a todas as IDs de partição. Os valores aceitos incluem:<p>-   **0x0000000000000001**. Especifica que a partição é exigida pelo computador para funcionar corretamente.<br />-   **0x8000000000000000**. Especifica que a partição não receberá uma letra de unidade por padrão quando o disco for movido para outro computador ou quando o disco for visto pela primeira vez por um computador.<br />-   **0x4000000000000000**. Oculta o volume de uma partição. Ou seja, a partição não será detectada pelo Gerenciador de montagem.<br />-   **0x2000000000000000**. Especifica que a partição é uma cópia de sombra de outra partição.<br />-   **0x1000000000000000**. Especifica que a partição é somente leitura. Esse atributo impede que o volume seja gravado no.<p>Para obter mais informações sobre esses atributos, consulte a seção atributos em [Create_PARTITION_PARAMETERS estrutura](https://go.microsoft.com/fwlink/?LinkId=203812). |

## <a name="remarks"></a>Comentários

- A partição do sistema EFI contém somente os binários necessários para iniciar o sistema operacional. Isso torna mais fácil para os binários OEM ou binários específicos de um sistema operacional serem colocados em outras partições.
- Uma partição GPT básica deve ser selecionada para que essa operação tenha sucesso. Use o comando **selecionar partição** para selecionar uma partição GPT básica e deslocar o foco para ela.

## <a name="examples"></a><a name=BKMK_examples></a>Disso

  Se você estiver movendo um disco GPT para um novo computador e quiser impedir que esse computador atribua automaticamente uma letra de unidade à partição com foco, digite:
  ```
  gpt attributes=0x8000000000000000
  ```
