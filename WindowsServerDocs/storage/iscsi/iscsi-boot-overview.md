---
ms.assetid: 134840f3-c416-4a10-ad73-ef7855b206f7
title: Visão geral da inicialização do destino iSCSI
ms.prod: windows-server
ms.technology: storage-iscsi
ms.topic: article
author: JasonGerend
manager: dougkim
ms.author: jgerend
ms.date: 09/11/2018
ms.openlocfilehash: 9c359c7929ff90968d16e92b1128f4fc8ebde37c
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71402991"
---
# <a name="iscsi-target-boot-overview"></a>Visão geral da inicialização do destino iSCSI

> Aplica-se ao Windows Server 2016

O Servidor de Destino iSCSI no Windows Server permite inicializar centenas de computadores por meio de uma única imagem do sistema operacional, armazenada em um local centralizado. Isso aumenta a eficiência, a capacidade de gerenciamento, a disponibilidade e a segurança.  
  
## <a name="BKMK_OVER"></a>Descrição do recurso  
Usando discos rígidos virtuais diferenciais \(VHDs\), você pode usar uma única imagem do sistema operacional \(a\) "imagem mestra" para inicializar até 256 computadores. Como exemplo, vamos supor que você implantou o Windows Server com uma imagem do sistema operacional de aproximadamente 20 GB e usou duas unidades de disco espelhadas para atuar como o volume de inicialização. Seria necessário cerca de 10 TB de armazenamento somente para a imagem de sistema operacional para inicializar 256 computadores. Com o Servidor de Destino iSCSI, você usará 40 GB para a imagem base do sistema operacional e 2 GB para discos rígidos virtuais diferenciais por instância do servidor, totalizando 552 GB para as imagens do sistema operacional. Isso proporciona uma economia de mais de 90% em armazenamento somente para as imagens do sistema operacional.  
  
## <a name="BKMK_APP"></a>Aplicativos práticos  
Usar uma imagem controlada do sistema operacional oferece os seguintes benefícios:  
  
**Mais segurança e gerenciamento mais fácil.** Algumas empresas exigem que os dados sejam protegidos bloqueando fisicamente o armazenamento em um local centralizado. Nesse cenário, os servidores acessam os dados remotamente, inclusive a imagem do sistema operacional. Com o Servidor de Destino iSCSI, os administradores podem gerenciar centralmente as imagens de inicialização do sistema operacional e controlar quais aplicativos devem ser usados para a imagem mestra.  
  
**Implantação rápida.** Como a imagem mestra é preparada usando o Sysprep, quando os computadores são inicializados por meio da imagem mestra, eles pulam a fase de cópia e instalação do arquivo que ocorre durante a Instalação do Windows, indo diretamente para a fase de personalização. Em testes internos da Microsoft, 256 computadores foram implantados em 34 minutos.  
  
**Recuperação rápida.** Como as imagens do sistema operacional são hospedadas no computador executando o Servidor de Destino iSCSI, se o cliente sem disco precisar ser substituído, o novo computador poderá apontar para a imagem do sistema operacional e ser inicializado imediatamente.  
  
> [!NOTE]  
> Vários fornecedores oferecem uma solução de inicialização SAN \(rede de área de armazenamento\), que pode ser usada pelo Servidor de Destino iSCSI no Windows Server em hardware de mercadoria.  
  
## <a name="BKMK_HARD"></a>Requisitos de hardware  
O Servidor de Destino iSCSI não exige hardware especial para verificação funcional. Nos data centers com implantações em grande escala\-, o design deve ser validado em relação a um hardware específico. Para referência, o teste interno da Microsoft indicou que uma implantação de computador 256 exigiu 24x15k\-discos RPM em uma configuração de RAID 10 para armazenamento. Uma largura de banda de rede de 10 GB é ideal. Uma estimativa geral é de 60 servidores de inicialização iSCSI por adaptador de rede de 1 GB.  
  
Não é necessário ter um adaptador de rede para esse cenário, e um carregador de inicialização de software pode ser usado \(como o firmware de inicialização de software livre iPXE\).  
  
## <a name="BKMK_SOFT"></a>Requisitos de software  
O Servidor de Destino iSCSI pode ser instalado como parte do serviço de função Arquivo e Serviços iSCSI no Gerenciador de Servidores.

> [!NOTE]
> Não há suporte para inicialização do Nano Server do iSCSI (da implementação do Servidor de Destino iSCSI do Windows ou de uma implementação de destino de terceiros).

## <a name="see-also"></a>Consulte também
* [Servidor de destino iSCSI](https://technet.microsoft.com/library/hh848272(v=ws.11).aspx)
* [cmdlets do iniciador iSCSI](https://technet.microsoft.com/library/hh826099(v=wps.640).aspx)
* [cmdlets do servidor de destino iSCSI](https://technet.microsoft.com/library/jj612803(v=wps.630).aspx)