---
title: extend
description: Tópico de comandos do Windows para * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 2414e21d-fc0b-40e8-9e33-3e072f8ad76b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 11991f9fc338dca5201d8f9c9c598b9d7dcf239b
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80844779"
---
# <a name="extend"></a>extend

>Aplicável a: Windows Server (canal semestral), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

estende o volume ou a partição com foco e seu sistema de arquivos para livre \(espaço\) não alocado em um disco.  
  
  
  
## <a name="syntax"></a>Sintaxe  
  
```  
extend [size=<n>] [disk=<n>] [noerr]  
extend filesystem [noerr]  
```  
  
### <a name="parameters"></a>Parâmetros  
  
| Parâmetro  |                                                                                             Descrição                                                                                              |
|------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| tamanho\=<n>  |      Especifica a quantidade de espaço em megabytes \(MB\) a ser adicionada ao volume ou à partição atual. Se nenhum tamanho for fornecido, todo o espaço livre contíguo disponível no disco será usado.       |
| \=de disco <n>  |                          Especifica o disco no qual o volume ou a partição é estendida. Se nenhum disco for especificado, o volume ou a partição será estendido no disco atual.                          |
| WPD |                                   estende o sistema de arquivos do volume com foco. Para uso somente em discos em que o sistema de arquivos não foi estendido com o volume.                                    |
|   NOERR    | somente para scripts. Quando um erro é encontrado, o DiskPart continua processando comandos como se o erro não tivesse ocorrido. Sem esse parâmetro, um erro faz com que o DiskPart saia com um código de erro. |
  
## <a name="remarks"></a>Comentários  
  
-   Em discos básicos, o espaço livre deve estar no mesmo disco que o volume ou a partição com foco. Ele também deve seguir imediatamente o volume ou a partição com foco \(ou seja, ele deve iniciar no próximo deslocamento de setor\).  
  
-   Em discos dinâmicos com volumes simples ou estendidos, um volume pode ser estendido para qualquer espaço livre em qualquer disco dinâmico. Usando esse comando, você pode converter um volume dinâmico simples em um volume dinâmico estendido. Volumes espelhados, RAID\-5 e distribuídos não podem ser estendidos.  
  
-   se a partição tiver sido formatada anteriormente com o sistema de arquivos NTFS, o sistema de arquivos será estendido automaticamente para preencher a partição maior e não ocorrerá nenhuma perda de dados.  
  
-   se a partição tiver sido formatada anteriormente com um sistema de arquivos diferente de NTFS, o comando falhará sem alteração na partição.  
  
-   se a partição não tiver sido formatada anteriormente com um sistema de arquivos, a partição ainda será estendida.  
  
-   A partição deve ter um volume associado para que possa ser estendida.  
  
## <a name="examples"></a><a name=BKMK_examples></a>Disso  
Para estender o volume ou a partição com foco em 500 megabytes, no disco 3, digite:  
  
```  
extend size=500 disk=3  
```  
  
Para estender o sistema de arquivos de um volume depois que ele foi estendido, digite:  
  
```  
extend filesystem  
```  
  
## <a name="additional-references"></a>Referências adicionais  
- [Chave da sintaxe de linha de comando](command-line-syntax-key.md)  
  

  

