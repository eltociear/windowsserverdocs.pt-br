---
title: copiar imagem
description: O tópico de comandos do Windows para Copy-Image, que copia imagens que estão dentro do mesmo grupo de imagens.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: bea41cf4-36e6-4181-afa5-00170ebd4fdc
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 443fa5bc87bbc7554e13f4b2a7fb7e36aa43dfaa
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80831699"
---
# <a name="copy-image"></a>copiar imagem

>Aplicável a: Windows Server (canal semestral), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Copia imagens que estão dentro do mesmo grupo de imagens. Para copiar imagens entre grupos de imagens, use o comando de [comando Export-Image](using-the-export-image-command.md) e, em seguida, o [usando o comando de comando Add-Image](using-the-add-image-command.md) .
para obter exemplos de como você pode usar esse comando, consulte [exemplos](#BKMK_examples).

## <a name="syntax"></a>Sintaxe
```
wdsutil [Options] /copy-Imagmedia:<Image name> [/Server:<Server name>]
   mediatype:Install
    mediaGroup:<Image group name>]
     [/Filename:<File name>]
     /DestinationImage
         /Name:<Name>
         /Filename:<File name>
         [/Description:<Description>]
```
### <a name="parameters"></a>Parâmetros
|Parâmetro|Descrição|
|-------|--------|
mídia:<Image name>|Especifica o nome da imagem a ser copiada.|
|[/Server:<Server name>]|Especifica o nome do servidor. Pode ser o nome NetBIOS ou o FQDN (nome de domínio totalmente qualificado). Se nenhum nome de servidor for especificado, o servidor local será usado.|
MediaType: instalar|Especifica o tipo de imagem a ser copiada. Essa opção deve ser definida como **instalar**.|
|\mediaGroup:<Image group name>]|Especifica o grupo de imagens que contém a imagem a ser copiada. Se nenhum grupo de imagens for especificado e houver apenas um grupo no servidor, esse grupo de imagens será usado por padrão. Se houver mais de um grupo de imagens no servidor, você deverá especificar o grupo de imagens.|
|[/Filename:<Filename>]|Especifica o nome do arquivo da imagem a ser copiada. Se a imagem de origem não puder ser identificada exclusivamente pelo nome, você deverá especificar o nome do arquivo.|
|/DestinationImage|Especifica as configurações para a imagem de destino, conforme descrito na tabela a seguir.<p>-/Name:<Name>-define o nome de exibição da imagem a ser copiada.<br />-/Filename:<Filename>-define o nome do arquivo de imagem de destino que conterá a cópia da imagem.<br />- [/Description: <Description>] – Define a descrição da cópia da imagem.|
## <a name="examples"></a><a name=BKMK_examples></a>Disso
Para criar uma cópia da imagem especificada e nomeá-la Aplicativoscompatíveis. wim, digite:
```
wdsutil /copy-Imagmedia:Windows Vista with Officemediatype:Install /DestinationImage /Name:copy of Windows Vista with Office /Filename:WindowsVista.wim
```
Para criar uma cópia da imagem especificada, aplique as configurações especificadas e nomeie a cópia Aplicativoscompatíveis. wim, digite:
```
wdsutil /verbose /Progress /copy-Imagmedia:Windows Vista with Office /Server:MyWDSServemediatype:InstalmediaGroup:ImageGroup1 
/Filename:install.wim /DestinationImage /Name:copy of Windows Vista with Office /Filename:WindowsVista.wim /Description:This is a copy of the original Windows image with Office installed
```
## <a name="additional-references"></a>Referências adicionais
- [A chave de sintaxe de linha de comando](command-line-syntax-key.md)
usando o [comando add-Image](using-the-add-image-command.md)
[usando o comando Export-Image](using-the-export-image-command.md)
[usando o comando Get-Image](using-the-get-image-command.md)
[usando o comando Remove-](using-the-remove-image-command.md) Image
[usando o comando Replace-Image](using-the-replace-image-command.md)
[Subcommand: Set-Image](subcommand-set-image.md)
