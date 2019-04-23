---
title: winnt32
description: 'Tópico de comandos do Windows para * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5a0a6fb3-ba4e-4ace-8984-7f6d3875560e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 28675ac6d5a1f1a7f56a9b72ef11a3e99e4ed130
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59851257"
---
# <a name="winnt32"></a>winnt32

>Aplica-se a: Windows Server (canal semestral), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Executa uma instalação ou atualização de um produto no Windows Server 2003. Você pode executar **winnt32** no prompt de comando em um computador executando o Windows 95, Windows 98, Windows Millennium edition, Windows NT, Windows 2000, Windows XP ou um produto no Windows Server 2003. Se você executar **winnt32** em um computador executando o Windows NT versão 4.0, primeiro você deve aplicar o Service Pack 5 ou posterior.
## <a name="syntax"></a>Sintaxe
```
winnt32 [/checkupgradeonly] [/cmd: <CommandLine>] [/cmdcons] [/copydir:{i386|ia64}\<FolderName>] [/copysource: <FolderName>] [/debug[<Level>]:[ <FileName>]] [/dudisable] [/duprepare: <pathName>] [/dushare: <pathName>] [/emsport:{com1|com2|usebiossettings|off}] [/emsbaudrate: <BaudRate>] [/m: <FolderName>]  [/makelocalsource] [/noreboot] [/s: <Sourcepath>] [/syspart: <DriveLetter>] [/tempdrive: <DriveLetter>] [/udf: <ID>[,<UDB_File>]] [/unattend[<Num>]:[ <AnswerFile>]]
```
### <a name="parameters"></a>Parâmetros
|Parâmetro|Descrição|
|-------|--------|
|/checkupgradeonly|Verifica se o computador de compatibilidade de atualização com produtos no Windows Server 2003.<br /><br />Se você usar essa opção com **/Unattend**, nenhuma entrada do usuário é necessária.  Caso contrário, os resultados são exibidos na tela, e você pode salvá-los com o nome do arquivo que você especificar. O nome de arquivo padrão é **upgrade** na pasta raiz do sistema.|
|/cmd|Instrui a instalação a executar um comando específico antes da fase final da instalação. Isso ocorre após a reinicialização do computador e após a instalação coletar as informações de configuração necessárias, mas antes da instalação for concluída.|
|\<CommandLine>|Especifica a linha de comando a ser realizada antes da fase final da instalação.|
|/cmdcons|Em um computador baseado em x86, instala a Console de recuperação como uma opção de inicialização.  A Console de recuperação é uma interface de linha de comando em que você pode executar tarefas como iniciar e interromper serviços e acessar a unidade local (incluindo unidades formatadas com NTFS). Você só pode usar o **/cmdcons** opção após a conclusão da instalação.|
|/copydir|cria uma pasta adicional dentro da pasta na qual os arquivos de sistema operacional estão instalados.  Por exemplo, para computadores baseados em x64 e x86, você poderia criar uma pasta chamada *Drivers_particulares* dentro da pasta de origem i386 para sua instalação e arquivos de driver do local na pasta. tipo de **/copydir: i386\\* * * Drivers_particulares* para que a copiar essa pasta para o computador recém-instalado, tornando o novo local da pasta de instalação **systemroot** \\*Drivers_particulares *.<br /><br />-   **i386** Especifica i386<br />-   **ia64** Especifica ia64<br /><br />Você pode usar **/copydir** para criar as pastas adicionais você deseja.|
|\<FolderName>|Especifica a pasta que você criou para armazenar as modificações para o seu site.|
|/copysource|cria uma pasta adicional temporária dentro da pasta na qual os arquivos de sistema operacional estão instalados. Você pode usar **/copysource** para criar as pastas adicionais você deseja.<br /><br />Ao contrário das pastas **/copydir** cria, **/copysource** pastas são excluídas após a conclusão da instalação.|
|/debug|cria um log de depuração no nível especificado, por exemplo, **/debug4**.  O arquivo de log padrão é **C:\ systemroot\winnt32.log**, e|
|\<level>|Descrições e valores de nível<br /><br />-   0: Erros graves<br />-   1: Erros<br />-   2: Nível padrão. Avisos<br />-   3: Informações do<br />-4: informações detalhadas para depuração<br /><br />Cada nível inclui os níveis inferiores.|
|/dudisable|Impede a execução de atualização dinâmica. Sem atualização dinâmica, a instalação é executada apenas com os arquivos de instalação original. Essa opção Desativar a atualização dinâmica, mesmo se você usar um arquivo de resposta e especificar opções de atualização dinâmica nesse arquivo.|
|/duprepare|Prepara um compartilhamento de instalação de modo que ele pode ser usado com arquivos de atualização dinâmica que você baixou do site do Windows Update. Esse compartilhamento, em seguida, pode ser usado para instalar o Windows XP para vários clientes.|
|\<pathName>|Especifica o nome do caminho completo.|
|/dushare|Especifica um compartilhamento no qual você baixou anteriormente (arquivos atualizados para uso com a instalação) de arquivos de atualização dinâmica do site do Windows Update e no qual você executou **/duprepare: * * * < caminho >*. Quando executado em um cliente, especifica que a instalação do cliente usará os arquivos atualizados no compartilhamento especificado em <pathName>.|
|/emsport|Habilita ou desabilita os serviços de gerenciamento de emergência durante a instalação e depois que o sistema operacional foi instalado. Com o EMS, você pode gerenciar remotamente um servidor em situações de emergência que normalmente exigiria um local teclado, mouse e monitor, como quando a rede está indisponível ou o servidor não está funcionando corretamente. O EMS tem requisitos de hardware específicos e está disponível apenas para os produtos no Windows Server 2003.<br /><br />-   **COM1** é aplicável somente para computadores baseados em x86 (não a computadores baseados em arquitetura Itanium).<br />-   **COM2**é aplicável somente para computadores baseados em x86 (não a computadores baseados em arquitetura Itanium).<br />-Padrão. Usa a configuração especificada na tabela de redirecionamento de Console de porta Serial (SPCR) BIOS ou, na arquitetura com base em sistemas Itanium, através do caminho de dispositivo do console EFI. Se você especificar **usebiossettings** e não há nenhuma tabela SPCR ou um caminho de dispositivo do console EFI apropriado, serviços de gerenciamento de emergência não serão habilitados.<br />-   **desativar** desabilita os serviços de gerenciamento de emergência. Você pode ativá-lo posteriormente modificando as configurações de inicialização.|
|/emsbaudrate|para computadores baseados em x86, especifica a taxa de transmissão de serviços de gerenciamento de emergência. (A opção não é aplicável para computadores baseados em arquitetura Itanium). Deve ser usado com **/emsport: COM1** ou **/emsport: COM2** (caso contrário, **/emsbaudrate** é ignorado).|
|\<Taxa de transmissão >|Especifica a taxa de transmissão de 9600, 19200, 57600 ou 115200. 9600 é o padrão.|
|/m|Especifica que a instalação copiará arquivos de substituição de um local alternativo.  Instrui a instalação a procurar primeiro no local alternativo e, se os arquivos estiverem presentes, usá-los em vez dos arquivos do local padrão.|
|/makelocalsource|Instrui a instalação para copiar todos os arquivos de origem de instalação para o disco rígido local.  Use **/makelocalsource** durante a instalação de um cd para fornecer arquivos de instalação quando o cd não estiver disponível posteriormente na instalação.|
|/noreboot|Instrui a instalação não reiniciar o computador após a fase de cópia de arquivo de configuração para que você possa executar outro comando.|
|/s|Especifica o local de origem dos arquivos para a instalação. Para copiar arquivos simultaneamente de vários servidores, digite o **/s:**\<Sourcepath > opção várias vezes (até um máximo de oito). Se você digitar a opção várias vezes, o primeiro servidor especificado deve estar disponível, ou haverá falha na instalação.|
|\<Caminho de origem >|Especifica o nome de caminho do código-fonte completo.|
|/syspart|Em um computador baseado em x86, especifica que você pode copiar arquivos de inicialização do programa de instalação em um disco rígido, marcar o disco como ativo e, em seguida, instale o disco em outro computador. Quando você inicia esse computador, ele começará automaticamente a próxima fase da instalação.<br /><br />Você sempre deve usar o **/tempdrive** parâmetro com o **/syspart** parâmetro.<br /><br />Você pode começar **winnt32** com o **/syspart** opção em um computador baseado em x86, executando o Windows NT 4.0, Windows 2000, Windows XP ou um produto no Windows Server 2003. Se o computador estiver executando o Windows NT versão 4.0, ele requer o Service Pack 5 ou posterior. O computador não pode estar executando o Windows 95, Windows 98 ou Windows Millennium edition.|
|\<DriveLetter>|Especifica a letra da unidade.|
|/tempdrive|Instrui a instalação para colocar os arquivos temporários na partição especificada.<br /><br />para uma nova instalação, o sistema operacional do servidor também será instalado na partição especificada.<br /><br />para uma atualização, o **/tempdrive** opção afeta o posicionamento de arquivos temporários somente; o sistema operacional será atualizado na partição em que você executou **winnt32**.|
|/udf|Indica um identificador (\<ID >) que a instalação usa para especificar como um arquivo de banco de dados de exclusividade (UDB) modifica um arquivo de resposta (consulte a **/Unattend** opção).  O UDF substitui valores no arquivo de resposta e o identificador determina quais valores do arquivo UDB são usados. Por exemplo, **/UDF** substitui as configurações especificadas para o identificador usuario_RAS no arquivo de empresa. Se nenhum \<arquivo_UDB > for especificado, o usuário insira um disco que contém a instalação solicitará que o **$Unique$. udb** arquivo.|
|\<ID>|Indica um identificador usado para especificar como um arquivo de banco de dados de exclusividade (UDB) modifica um arquivo de resposta.|
|\<UDB_file>|Especifica um arquivo de banco de dados de exclusividade (UDB).|
|/unattend|Em um computador baseado em x86, atualiza a versão anterior do Windows NT 4.0 Server (com Service Pack 5 ou posterior) ou Windows 2000 no modo de instalação autônoma. Todas as configurações de usuário são utilizadas da instalação anterior, nenhuma intervenção do usuário é necessária durante a instalação.|
|\<num>|Especifica o número de segundos entre a hora em que a instalação termina de copiar os arquivos e quando o computador é reiniciado. Você pode usar \<Num > em qualquer computador executando o Windows 98, Windows Millennium edition, Windows NT, Windows 2000, Windows XP ou um produto no Windows Server 2003. Se o computador estiver executando o Windows NT versão 4.0, ele requer o Service Pack 5 ou posterior.|
|\<AnswerFile>|Fornece a instalação com as especificações personalizadas|
|/?|Exibe a ajuda no prompt de comando.|

## <a name="remarks"></a>Comentários
Se você estiver implantando o Windows XP nos computadores cliente, você pode usar a versão do winnt32.exe que vem com o Windows XP. Outra maneira de implantar o Windows XP é usar o Winnt32. msi, que funciona por meio do Windows Installer, parte do IntelliMirror conjunto de tecnologias. Para obter mais informações sobre implantações do cliente, consulte o Windows Server 2003 Deployment Kit, que é descrito em [usando o Windows Deployment and Resource Kits](https://technet.microsoft.com/library/cc779317(v=ws.10).aspx).

Em um computador baseado em Itanium, **winnt32** podem ser executados na Interface de Firmware extensível (EFI) ou do Windows Server 2003 Enterprise, Windows Server 2003 R2 Enterprise, Windows Server 2003 R2 Datacenter ou Windows Server 2003 Data Center. Além disso, em um computador baseado em arquitetura Itanium, **/cmdcons** e **/syspart** não estão disponíveis e as opções relacionadas a atualizações não estão disponíveis.
Para obter mais informações sobre compatibilidade de hardware, consulte [compatibilidade de Hardware](https://technet.microsoft.com/library/cc757927(v=ws.10).aspx).
Para obter mais informações sobre como usar a atualização dinâmica e a instalação de vários clientes, consulte o Windows Server 2003 Deployment Kit, que é descrito em [usando o Windows Deployment and Resource Kits](https://technet.microsoft.com/library/cc779317(v=ws.10).aspx).
Para obter informações sobre como modificar as configurações de inicialização, consulte a implantação do Windows e os Kits de recursos para o Windows Server 2003. Para obter mais informações, consulte [usando o Windows Deployment and Resource Kits](https://technet.microsoft.com/library/cc779317(v=ws.10).aspx).
Usando o **/Unattend** a opção de linha de comando para automatizar a instalação confirmará que você leu e aceitou o contrato de licença de Microsoft para Windows Server 2003. Antes de usar essa opção de linha de comando para instalar o Windows Server 2003 em nome de uma organização diferente do seu, você deve confirmar que o usuário final (seja um indivíduo ou uma única entidade) recebeu, leu e aceitou os termos do Microsoft License Contrato para o produto.  Os OEMs não podem especificar essa chave em máquinas vendidas para usuários finais.

## <a name="additional-references"></a>Referências adicionais
-   [Chave de sintaxe de linha de comando](command-line-syntax-key.md)
