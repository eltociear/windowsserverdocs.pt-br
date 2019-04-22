---
title: RDS - criar e implantar
description: Etapas para criar uma implantação de área de trabalho remota
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.author: elizapo
ms.date: 04/18/2017
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 176ae424-96e9-4c78-88f5-da418e76c3d7
author: lizap
manager: dongill
ms.openlocfilehash: 0ab4be6ba326db05e8fc6a9c14e84c8cbb855926
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59814747"
---
# <a name="build-and-deploy-your-remote-desktop-services-deployment"></a>Criar e implantar sua implantação de serviços de área de trabalho remota

Uma implantação de serviços de área de trabalho remota é a infraestrutura usada para compartilhar aplicativos e recursos com seus usuários. Dependendo da experiência que você deseja fornecer, você pode tornar pequenas ou complexa conforme necessário. Implantações de área de trabalho remota são dimensionadas com facilidade. Você pode aumentar e diminuir o acesso remoto via Web da área de trabalho, servidores de Gateway, o agente de Conexão e o Host de sessão em serão. Você pode usar o agente de Conexão de área de trabalho remota para distribuir cargas de trabalho. Autenticação do Active Directory com base fornece um ambiente altamente seguro. 

[Os clientes de Desktop remotos](clients\remote-desktop-clients.md) habilitar o acesso em qualquer Windows, Apple ou Android computador, tablet ou telefone.

Ver [arquitetura dos serviços de área de trabalho remota](desktop-hosting-logical-architecture.md) para uma discussão detalhada sobre as diferentes partes que funcionam em conjunto para fazer backup de sua implantação de serviços de área de trabalho remota.

Tem uma implantação de área de trabalho remota existente criada em uma versão anterior do Windows Server? Confira as opções para mover para o WIndows Server 2016, em que você pode tirar proveito das funcionalidades novas e melhores em torno de desempenho e escala:

- [Migrar sua implantação do RDS para o Windows Server 2016](migrate-rds-role-services.md)
- [Atualizar a implantação do RDS para o Windows Server 2016](upgrade-to-rds-2016.md)

Deseja criar uma nova implantação de área de trabalho remota? Use as informações a seguir para implantar a área de trabalho remota no Windows Server 2016:

- [Implantar a infraestrutura de serviços de área de trabalho remota](rds-deploy-infrastructure.md)
- [Criar uma coleção de sessão para manter os aplicativos e recursos que você deseja compartilhar](rds-create-collection.md)
- [Licenciar sua implantação do RDS](rds-client-access-license.md)
- Que os usuários instalem um [cliente de área de trabalho remota](clients/remote-desktop-clients.md) para que possam acessar a aplicativos e recursos. 
- Habilite a alta disponibilidade com a adição de Hosts de sessão e agentes de Conexão adicionais:
   - [Escalar horizontalmente uma coleção de RDS existente com um farm de Host de sessão de área de trabalho remota](rds-scale-rdsh-farm.md)
   - [Adicionar a alta disponibilidade para a infraestrutura de agente de Conexão de área de trabalho](rds-connection-broker-cluster.md)
   - [Adicionar a alta disponibilidade para a frente da web da Web da área de trabalho remota e Gateway de área de trabalho remota](rds-rdweb-gateway-ha.md)
   - [Implantar um sistema de arquivos de espaços de armazenamento diretos de dois nós para armazenamento UPD](rds-storage-spaces-direct-deployment.md)


Se você for um parceiro de hospedagem interessado em usar a área de trabalho remota para fornecer aplicativos e recursos aos clientes ou um cliente procurando alguém hospedar seus aplicativos, fazer check-out [parceiros de hospedagem de serviços de área de trabalho remota](rds-hosting-partners.md) para obter informações sobre um avaliação, você pode tirar sobre como usar RDS no Azure como um ambiente de hospedagem, bem como uma lista de parceiros que passou a ele.