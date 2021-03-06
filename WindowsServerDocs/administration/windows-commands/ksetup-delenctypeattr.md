---
title: 'ksetup: delenctypeattr'
description: Tópico de comandos do Windows para * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 4fc25ef3-e271-4229-a712-72c507df55aa
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c650b973ac34e28394d5b6ec38142a058ad76338
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80841759"
---
# <a name="ksetupdelenctypeattr"></a>ksetup: delenctypeattr



Remove o atributo de tipo de criptografia para o domínio. Para obter exemplos de como esse comando pode ser usado, consulte [exemplos](#BKMK_Examples).

## <a name="syntax"></a>Sintaxe

```
ksetup /delenctypeattr <DomainName> 
```

#### <a name="parameters"></a>Parâmetros

|Parâmetro|Descrição|
|---------|-----------|
|\<nome_do_domínio >|Nome do domínio ao qual você deseja estabelecer uma conexão. Use o nome de domínio totalmente qualificado ou uma forma simples do nome, como corp.contoso.com ou contoso.|

## <a name="remarks"></a>Comentários

Para exibir o tipo de criptografia para o tíquete de concessão de tíquete (TGT) e a chave de sessão do Kerberos, execute o comando **klist** e exiba a saída.

Uma mensagem de status é exibida após A conclusão bem-sucedida ou falha.

Para definir o domínio ao qual você deseja se conectar e usar, execute o comando **ksetup/domain \<domainname >** .

## <a name="examples"></a><a name=BKMK_Examples></a>Disso

Determine os tipos de criptografia atuais que estão definidos neste computador:
```
klist
```
Defina o domínio como mit.contoso.com:
```
ksetup /domain mit.contoso.com
```
Verifique qual é o atributo de tipo de criptografia para o domínio:
```
ksetup /getenctypeattr mit.contoso.com
```
Remova o atributo definir tipo de criptografia para o mit.contoso.com de domínio:
```
ksetup /delenctypeattr mit.contoso.com
```

## <a name="additional-references"></a>Referências adicionais

-   [Klist](klist.md)
-   [Ksetup:domain](ksetup-domain.md)
-   [Ksetup:addenctypeattr](ksetup-addenctypeattr.md)
-   [Ksetup:setenctypeattr](ksetup-setenctypeattr.md)
-   [Ksetup:delenctypeattr](ksetup-delenctypeattr.md)
-   - [Chave da sintaxe de linha de comando](command-line-syntax-key.md)