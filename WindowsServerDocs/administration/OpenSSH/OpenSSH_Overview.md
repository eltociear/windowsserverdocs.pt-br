---
ms.date: 01/07/2019
contributor: damaerteMSFT
author: maertendmsft
title: OpenSSH no Windows
ms.product: windows-server
ms.openlocfilehash: 57126f38245f4547a04ea3a51f58aee865b5eb97
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80852029"
---
# <a name="openssh-in-windows"></a>OpenSSH no Windows

OpenSSH é uma versão de software livre das ferramentas SSH (Secure Shell) usadas por administradores de Linux e outros sistemas não Windows para gerenciamento multiplataforma de sistemas remotos. O OpenSSH foi adicionado ao Windows no segundo semestre de 2018 e foi incluído no Windows 10 e no Windows Server 2019. 

O SSH baseia-se em uma arquitetura cliente-servidor em que o sistema no qual o usuário está trabalhando é o cliente e o sistema remoto que está sendo gerenciado é o servidor. O OpenSSH inclui uma variedade de componentes e ferramentas projetados para fornecer uma abordagem segura e direta à administração remota do sistema, incluindo:

* sshd.exe, que é o componente do servidor SSH que deve estar em execução no sistema que está sendo gerenciado remotamente 
* ssh.exe, que é o componente de cliente SSH executado no sistema local do usuário
* ssh-keygen.exe gera, gerencia e converte chaves de autenticação para SSH 
* ssh-agent.exe armazena chaves privadas usadas para autenticação de chave pública
* ssh-add.exe adiciona chaves privadas à lista permitida pelo servidor
* o ssh-keyscan.exe ajuda a coletar as chaves de host SSH públicas de vários hosts
* o sftp.exe é o serviço que fornece o protocolo FTP seguro e é executado por SSH
* scp.exe é um utilitário de cópia de arquivo executado no SSH

A documentação nesta seção concentra-se em como o OpenSSH é usado no Windows, incluindo instalação e casos de uso e configuração específicos do Windows. Estes são os tópicos:
* Como instalar e desinstalar o OpenSSH para Windows Server 2019 e Windows 10

A documentação detalhada adicional para recursos comuns do OpenSSH está disponível online em [OpenSSH.com](https://www.openssh.com/manual.html). 

O [projeto de software livre OpenSSH](https://www.openssh.com) mestre é gerenciado por desenvolvedores no projeto OpenBSD. O Microsoft Fork deste projeto está no [GitHub](https://github.com/PowerShell/openssh-portable).
Os comentários sobre o Windows OpenSSH são bem-vindos e podem ser fornecidos pela criação de problemas do GitHub em nosso repositório GitHub [OpenSSH](https://github.com/PowerShell/openssh-portable). 
