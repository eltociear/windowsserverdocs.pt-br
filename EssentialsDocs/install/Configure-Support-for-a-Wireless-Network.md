---
title: Configurar Suporte a uma Rede sem Fio
description: Descreve como usar o Windows Server Essentials
ms.date: 10/03/2016
ms.prod: windows-server
ms.topic: article
ms.assetid: 4d7020d4-fd46-4858-a406-de5c0f21ea06
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 284ae73a846ccad98fe352ac143e89f79fc2a17b
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80818419"
---
# <a name="configure-support-for-a-wireless-network"></a>Configurar Suporte a uma Rede sem Fio

>Aplica-se a: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

Você pode configurar o sistema operacional para dar suporte a uma rede sem fio. Os seguintes requisitos devem ser atendidos para habilitar o suporte sem fio no servidor:  
  
-   O servidor deve ter um adaptador de rede com fio instalado.  
  
-   O driver correto para o adaptador de rede sem fio deverá ser pré-instalado se o adaptador de rede não for suportado pelo sistema operacional.  
  
-   A capacidade de habilitar e desabilitar o adaptador de rede sem fio deve estar disponível. Os métodos para fazer isso podem incluir um botão físico no servidor ou uma interface do usuário personalizada no Dashboard. O manual do produto deve fornecer as etapas para habilitar e desabilitar o adaptador de rede sem fio.  
  
-   A capacidade de selecionar uma rede sem fio e conectar-se a ela deve estar disponível. Isso deve ser feito adicionando uma interface do usuário personalizada ao Dashboard. O manual do produto deve fornecer as etapas para selecionar e conectar-se a uma rede sem fio.  
  
-   Se for necessário suporte para uma rede ad hoc sem fio, deverá ser fornecida uma interface do usuário estendida no Dashboard. A interface do usuário pode ser um botão ou um link que inicia o Assistente de Configuração de uma Rede Ad hoc sem Fio no painel de controle no Windows Server 2008 R2.  
  
## <a name="additional-considerations"></a>Considerações adicionais  
 As seguintes informações também devem ser consideradas ao configurar o suporte para uma rede sem fio:  
  
-   O servidor deve estar conectado à rede com um fio para executar a instalação.  
  
-   Um computador da rede no qual uma restauração bare-metal é executada deve estar conectado à rede através de um fio.  
  
-   O servidor deve estar conectado à rede através de um fio para executar uma restauração bare-metal do servidor.  
  
-   Se uma rede ad hoc for criada no servidor, o adaptador de rede sem fio será dedicado à rede ad hoc, de modo que o usuário sempre deverá conectar o cabo de rede no servidor para obter uma conexão com a Internet.  
  
> [!NOTE]
>  Para obter mais informações sobre como configurar conexões de rede, consulte [Pré-configurando um Roteador](Preconfiguring-a-Router.md).  
  
## <a name="see-also"></a>Consulte também  
 [Criando e personalizando a imagem](Creating-and-Customizing-the-Image.md)   
 [Personalizações adicionais](Additional-Customizations.md)   
 [Preparando a imagem para implantação](Preparing-the-Image-for-Deployment.md)   
 [Testar a experiência do usuário](Testing-the-Customer-Experience.md)