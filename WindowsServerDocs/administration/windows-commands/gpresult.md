---
title: gpresult
description: Tópico de comandos do Windows para * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: dfaa3adf-2c83-486c-86d6-23f93c5c883c
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 480599a4040ab1fdcc3842cdb0eaa8c35afa873c
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80842459"
---
# <a name="gpresult"></a>gpresult

>Aplicável a: Windows Server (canal semestral), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Exibe o conjunto resultante de informações de política (RSoP) para um usuário e computador remoto.
Para usar relatórios RSoP para computadores de destino remoto por meio do firewall, você deve ter regras de firewall que habilitem o tráfego de rede de entrada nas portas.

## <a name="syntax"></a>Sintaxe

```
gpresult [/s <system> [/u <USERNAME> [/p [<PASSWOrd>]]]] [/user [<TARGETDOMAIN>\]<TARGETUSER>] [/scope {user | computer}] {/r | /v | /z | [/x | /h] <FILENAME> [/f] | /?}
```

### <a name="parameters"></a>Parâmetros

> [!NOTE]
> Exceto quando você usa **/?** , você deve incluir uma opção de saída, ou **/r**, **/v**, **/z**, **/x**ou **/h**.

|                Parâmetro                 |                                                                                                     Descrição                                                                                                      |
|------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|              /s \<\> do sistema               |                                                  Especifica o nome ou o endereço IP de um computador remoto. Não use barras invertidas. O padrão é o computador local.                                                   |
|             /u \<nome de usuário\>              |                                Usa as credenciais do usuário especificado para executar o comando. O usuário padrão é o usuário que fez logon no computador que emite o comando.                                 |
|            /p [\<a senha\>]             |            Especifica a senha da conta de usuário que é fornecida no parâmetro **/u** . Se **/p** for omitido, **GPResult** solicitará a senha. **/p** não pode ser usado com **/x** ou **/h**.            |
| /User [\<TARGETDOMAIN\>\\]\<TARGETUSER\> |                                                                            Especifica o usuário remoto cujos dados RSoP serão exibidos.                                                                             |
|      /Scope {computador &#124; do usuário}       |                                Exibe dados RSoP para o usuário ou o computador. Se **/Scope** for omitido, **GPResult** exibirá dados RSoP para o usuário e o computador.                                 |
|        [/x &#124; /h] <FILENAME>         | Salva o relatório em formato XML ( **/x**) ou HTML ( **/h**) no local e com o nome do arquivo especificado pelo parâmetro *filename* . Não pode ser usado com **/u**, **/p**, **/r**, **/v**ou **/z**. |
|                    /f                    |                                                           força o **GPResult** a substituir o nome de arquivo especificado na opção **/x** ou **/h** .                                                           |
|                    /r                    |                                                                                             Exibe dados de Resumo de RSoP.                                                                                              |
|                    /v                    |                                                    Exibe informações detalhadas da política. Isso inclui configurações detalhadas que foram aplicadas com uma precedência de 1.                                                    |
|                    /z                    |                                     Exibe todas as informações disponíveis sobre Política de Grupo. Isso inclui configurações detalhadas que foram aplicadas com uma precedência de 1 e superior.                                      |
|                    /?                    |                                                                                         Exibe a ajuda no prompt de comando.                                                                                         |

## <a name="remarks"></a>Comentários
- Política de Grupo é a ferramenta administrativa principal para definir e controlar como programas, recursos de rede e o sistema operacional operam para usuários e computadores em uma organização. Em um ambiente do Active Directory, Política de Grupo é aplicada a usuários ou computadores com base em sua associação em sites, domínios ou unidades organizacionais.
- Como você pode aplicar configurações de política sobrepostas a qualquer computador ou usuário, o recurso Política de Grupo gera um conjunto resultante de configurações de política quando o usuário faz logon. **GPResult** exibe o conjunto resultante de configurações de política que foram impostas no computador para o usuário especificado quando o usuário fez logon.
- Como **/v** e **/z** produzem muitas informações, é útil redirecionar a saída para um arquivo de texto (por exemplo, **GPResult/z > Policy. txt**).
- O comando **GPResult** está disponível no windows Server 2012, windows Server 2008 R2, Windows Server 2008, Windows 8, Windows 7 e Windows Vista.
  ## <a name="examples"></a>Exemplos
  O exemplo a seguir recupera dados RSoP para o usuário remoto **targetusername** do computador **srvmain**e exibe dados RSoP apenas sobre o usuário. O comando é executado com as credenciais do usuário **maindom\hiropln**e <strong>p@ssW23</strong> é inserido como a senha para esse usuário.

  ```
  gpresult /s srvmain /u maindom\hiropln /p p@ssW23 /user targetusername /scope user /r
  ```
  
O exemplo a seguir salva todas as informações disponíveis sobre Política de Grupo para o usuário remoto **targetusername** do computador **srvmain** para um arquivo chamado **Policy. txt**. Nenhum dado está incluído no computador. O comando é executado com as credenciais do usuário **maindom\hiropln**e <strong>p@ssW23</strong> é inserido como a senha para esse usuário.

  ```
  gpresult /s srvmain /u maindom\hiropln /p p@ssW23 /user targetusername /z > policy.txt
  ```
  
O exemplo a seguir exibe dados RSoP para o computador **srvmain** e o usuário conectado. Os dados são incluídos no usuário e no computador. O comando é executado com as credenciais do usuário **maindom\hiropln**e <strong>p@ssW23</strong> é inserido como a senha para esse usuário.

  ```
  gpresult /s srvmain /u maindom\hiropln /p p@ssW23 /r
  ```
  
## <a name="additional-references"></a>Referências adicionais
- [TechCenter do Política de Grupo](https://go.microsoft.com/fwlink/?LinkID=145531)

- - [Chave da sintaxe de linha de comando](command-line-syntax-key.md)
