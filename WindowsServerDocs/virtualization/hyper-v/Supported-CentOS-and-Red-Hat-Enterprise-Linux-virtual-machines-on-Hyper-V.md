---
title: Máquinas virtuais CentOS e Red Hat Enterprise Linux com suporte no Hyper-V
description: Lista as versões do Linux Integration Services para distribuições do CentOS e Red Hat Enterprise com suporte
ms.prod: windows-server
ms.technology: compute-hyper-v
ms.topic: article
ms.assetid: 4bf8783d-dee5-4b3e-8cce-2b11b117c189
author: danihalfin
ms.author: vichen
ms.date: 04/06/2020
ms.openlocfilehash: 5d30f373390ffa61ebe8710de82d20107456462b
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80855979"
---
# <a name="supported-centos-and-red-hat-enterprise-linux-virtual-machines-on-hyper-v"></a>Máquinas virtuais CentOS e Red Hat Enterprise Linux com suporte no Hyper-V

>Aplica-se a: Windows Server 2019, Hyper-V Server 2019, Windows Server 2016, Hyper-V Server 2016, Windows Server 2012 R2, Hyper-V Server 2012 R2, Windows 10, Windows 8.1

Os mapas de distribuição de recursos a seguir indicam os recursos que estão presentes nas versões internas e baixáveis do Linux Integration Services. Os problemas conhecidos e as soluções alternativas para cada distribuição são listados após as tabelas.

Os drivers de Integration Services Red Hat Enterprise Linux internos para Hyper-V (disponíveis desde Red Hat Enterprise Linux 6,4) são suficientes para os convidados Red Hat Enterprise Linux serem executados usando os dispositivos sintéticos de alto desempenho em hosts Hyper-V. Esses drivers internos são certificados pelo Red Hat para esse uso. As configurações certificadas podem ser exibidas nesta página da Web do Red Hat: [Catálogo de certificação Red Hat](https://access.redhat.com/ecosystem/search/#/ecosystem/Red%20Hat%20Enterprise%20Linux?sort=sortTitle%20asc&vendors=Microsoft&category=Server). Não é necessário baixar e instalar pacotes de Integration Services do Linux do centro de download da Microsoft e fazer isso pode limitar o suporte a Red Hat, conforme descrito no artigo 1067 da base de conhecimento do Red Hat: [Red Hat knowledgebase 1067](https://access.redhat.com/articles/1067).

Devido a possíveis conflitos entre o suporte de LIS interno e o suporte à LIS para download quando você atualiza o kernel, desabilite as atualizações automáticas, desinstale os pacotes de LIS download, atualize o kernel, reinicialize e instale a versão mais recente do LIS e reinicialize.

> [!NOTE]
> As informações oficiais de certificação de Red Hat Enterprise Linux estão disponíveis por meio do [portal do cliente do Red Hat](https://access.redhat.com/ecosystem/search/#/category/Server?sort=sortTitle%20asc&query=windows%20server&ecosystem=Red%20Hat%20Enterprise%20Linux).

Nesta seção:

* [Série RHEL/CentOS 8. x](#rhelcentos-8x-series)

* [Série RHEL/CentOS 7. x](#rhelcentos-7x-series)

* [Série RHEL/CentOS 6. x](#rhelcentos-6x-series)

* [Série RHEL/CentOS 5. x](#rhelcentos-5x-series)

* [Registra](#notes)

## <a name="table-legend"></a>Legenda da tabela

* A LIS **interna** é incluída como parte dessa distribuição do Linux. Os números de versão do módulo do kernel para a LIS interna (conforme mostrado por **lsmod**, por exemplo) são diferentes do número de versão no pacote de download do LIS fornecido pela Microsoft. Uma incompatibilidade não indica que a LIS interna está desatualizada.

* &#10004;-Recurso disponível

* (*em branco*)-recurso não disponível

## <a name="rhelcentos-8x-series"></a>Série RHEL/CentOS 8. x

|       **Recurso**     |       **Versão do Windows Server**      |       **8,1**     |       **8,0**     | 
|-----------------------|---------------------------------------|-------------------|-------------------|
|       **Disponibilidade**        |   |   |
|       **[Core](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#core)**      | 2019, 2016, 2012 R2 | &#10004; | &#10004;
|       Tempo preciso do Windows Server 2016       | 2019, 2016 | &#10004; | &#10004; 
|       **[Rede](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#networking)**      |   |  |
|       Quadros jumbo        | 2019, 2016, 2012 R2 | &#10004; | &#10004;|
|       Marcação e entroncamento de VLAN       | 2019, 2016, 2012 R2 | &#10004;  | &#10004; |
|       Migração ao vivo      | 2019, 2016, 2012 R2 | &#10004; | &#10004;|
|       Injeção de IP estático     |  2019, 2016, 2012 R2 | &#10004;Observação 2 | &#10004;Observação 2|
|       vRSS     | 2019, 2016, 2012 R2 | &#10004; | &#10004;|
|       Segmentação de TCP e descarregamentos de soma de verificação | 2019, 2016, 2012 R2 | &#10004;|  &#10004; |
|       SR-IOV  | 2019, 2016 |  &#10004;   | &#10004; |
|       **[Repositório](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#storage)** |  |  |
|       Redimensionamento de VHDX  | 2019, 2016, 2012 R2 | &#10004; | &#10004; |
|       Fibre Channel Virtual | 2019, 2016, 2012 R2 | &#10004;Observação 3  | &#10004;Observação 3 |
|       Backup de máquina virtual ao vivo  | 2019, 2016, 2012 R2 | &#10004;Observação 5 | &#10004;Observação 5|
|       Suporte a corte | 2019, 2016, 2012 R2 | &#10004;  | &#10004; |
|       WWN DO SCSI | 2019, 2016, 2012 R2 | &#10004;  | &#10004; |
|       **[Memória](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#memory)** | |  |
|       Suporte ao kernel de PAE  | 2019, 2016, 2012 R2 |  {1&gt;N/A&lt;1} | {1&gt;N/A&lt;1}
|       Configuração da lacuna de MMIO  | 2019, 2016, 2012 R2 | &#10004; | &#10004;  |
|       Memória Dinâmica-adição a quente | 2019, 2016, 2012 R2  | &#10004;Nota 8, 9, 10 | &#10004;Nota 8, 9, 10 |
|       Memória Dinâmica-balões | 2019, 2016, 2012 R2 | &#10004;Nota 8, 9, 10 | &#10004;Nota 8, 9, 10 |
|       Redimensionamento de memória de Runtime | 2019, 2016  | &#10004;  | &#10004; |
|       **[Monitor](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#video)** | | |
|       Dispositivo de vídeo específico do Hyper-V | 2019, 2016, 2012 R2 | &#10004;   | &#10004; |
|       **[Várias](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#miscellaneous)** | | |
|       Par chave-valor  | 2019, 2016, 2012 R2 | &#10004;   | &#10004;  |
|       Interrupção não mascarável | 2019, 2016, 2012 R2 | &#10004;  | &#10004; |
|       Cópia de arquivo do host para o convidado | 2019, 2016, 2012 R2 | &#10004;  | &#10004; |
|       comando lsvmbus | 2019, 2016, 2012 R2 | &#10004;  | &#10004; |
|       Soquetes do Hyper-V | 2019, 2016 | &#10004;  | &#10004; |
|       Passagem de PCI/DDA | 2019, 2016 | &#10004; | &#10004; |
| **[Máquinas virtuais de geração 2](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#generation-2-virtual-machines)** | |  |
|       Inicializar usando UEFI | 2019, 2016, 2012 R2 |  &#10004;Nota 14  | &#10004;Nota 14   
|       Inicialização segura | 2019, 2016 |  &#10004; |  &#10004; |


## <a name="rhelcentos-7x-series"></a>Série RHEL/CentOS 7. x

Esta série tem apenas kernels de 64 bits.


|                                                                 **Recurso**                                                                  |     **Versão do Windows Server**     |                             **7.5-7.8**                             |                             **7.3-7.4**                             |                             **7.0-7.2**                             |     **7.5-7.8**     |       **7,4**       |       **7,3**       |       **7,2**       |       **7,1**       |        **7,0**         |
|----------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------|---------------------------------------------------------------------|---------------------------------------------------------------------|---------------------------------------------------------------------|---------------------|---------------------|---------------------|---------------------|---------------------|------------------------|
|                                                               **Disponibilidade**                                                               |                                    | [LIS 4,3](https://www.microsoft.com/download/details.aspx?id=55106) | [LIS 4,3](https://www.microsoft.com/download/details.aspx?id=55106) | [LIS 4,3](https://www.microsoft.com/download/details.aspx?id=55106) |      Interno       |      Interno       |      Interno       |      Interno       |      Interno       |        Interno        |
|                          **[Core](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#core)**                          | 2019, 2016, 2012 R2 |                              &#10004;                               |                              &#10004;                               |                              &#10004;                               |      &#10004;       |      &#10004;       |      &#10004;       |      &#10004;       |      &#10004;       |        &#10004;        |
|                                                      Tempo preciso do Windows Server 2016                                                       |             2019, 2016             |                              &#10004;                               |                              &#10004;                               |                                                                     |                     |                     |                     |                     |                     |                        |
|                    **[Rede](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#networking)**                    |                                    |                                                                     |                                                                     |                                                                     |                     |                     |                     |                     |                     |                        |
|                                                                 Quadros jumbo                                                                 | 2019, 2016, 2012 R2 |                              &#10004;                               |                              &#10004;                               |                              &#10004;                               |      &#10004;       |      &#10004;       |      &#10004;       |      &#10004;       |      &#10004;       |        &#10004;        |
|                                                          Marcação e entroncamento de VLAN                                                           | 2019, 2016, 2012 R2 |                              &#10004;                               |                              &#10004;                               |                              &#10004;                               |      &#10004;       |      &#10004;       |      &#10004;       |      &#10004;       |      &#10004;       |        &#10004;        |
|                                                                Migração ao vivo                                                                | 2019, 2016, 2012 R2 |                              &#10004;                               |                              &#10004;                               |                              &#10004;                               |      &#10004;       |      &#10004;       |      &#10004;       |      &#10004;       |      &#10004;       |        &#10004;        |
|                                                             Injeção de IP estático                                                              |     2019, 2016, 2012 R2      |                           &#10004;Observação 2                           |                           &#10004;Observação 2                           |                           &#10004;Observação 2                           |   &#10004;Observação 2   |   &#10004;Observação 2   |   &#10004;Observação 2   |   &#10004;Observação 2   |   &#10004;Observação 2   |    &#10004;Observação 2     |
|                                                                     vRSS                                                                     |        2019, 2016, 2012 R2         |                              &#10004;                               |                              &#10004;                               |                              &#10004;                               |      &#10004;       |      &#10004;       |      &#10004;       |      &#10004;       |      &#10004;       |                        |
|                                                    Segmentação de TCP e descarregamentos de soma de verificação                                                    | 2019, 2016, 2012 R2 |                              &#10004;                               |                              &#10004;                               |                              &#10004;                               |      &#10004;       |      &#10004;       |      &#10004;       |      &#10004;       |      &#10004;       |                        |
|                                                                    SR-IOV                                                                    |             2019, 2016             |                              &#10004;                               |                              &#10004;                               |                                                                     |      &#10004;       |      &#10004;       |      &#10004;       |                     |                     |                        |
|                       **[Repositório](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#storage)**                       |                                    |                                                                     |                                                                     |                                                                     |                     |                     |                     |                     |                     |                        |
|                                                                 Redimensionamento de VHDX                                                                  |        2019, 2016, 2012 R2         |                              &#10004;                               |                              &#10004;                               |                              &#10004;                               |      &#10004;       |      &#10004;       |      &#10004;       |      &#10004;       |                     |                        |
|                                                            Fibre Channel Virtual                                                             |        2019, 2016, 2012 R2         |                           &#10004;Observação 3                           |                           &#10004;Observação 3                           |                           &#10004;Observação 3                           |   &#10004;Observação 3   |   &#10004;Observação 3   |   &#10004;Observação 3   |   &#10004;Observação 3   |   &#10004;Observação 3   |    &#10004;Observação 3     |
|                                                         Backup de máquina virtual ao vivo                                                          |        2019, 2016, 2012 R2         |                           &#10004;Observação 5                           |                           &#10004;Observação 5                           |                           &#10004;Observação 5                           |  &#10004;Observação 4, 5  | &#10004;Observação 4, 5  | &#10004;Observação 4, 5  | &#10004;Observação 4, 5  | &#10004;Observação 4, 5  |   &#10004;Observação 4, 5   |
|                                                                 Suporte a corte                                                                 |        2019, 2016, 2012 R2         |                              &#10004;                               |                              &#10004;                               |                              &#10004;                               |      &#10004;       |      &#10004;       |      &#10004;       |      &#10004;       |                     |                        |
|                                                                   WWN DO SCSI                                                                   |        2019, 2016, 2012 R2         |                              &#10004;                               |                              &#10004;                               |                              &#10004;                               |      &#10004;       |                     |                     |                     |                     |                        |
|                        **[Memória](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#memory)**                        |                                    |                                                                     |                                                                     |                                                                     |                     |                     |                     |                     |                     |                        |
|                                                              Suporte ao kernel de PAE                                                              | 2019, 2016, 2012 R2 |                                 {1&gt;N/A&lt;1}                                 |                                 {1&gt;N/A&lt;1}                                 |                                 {1&gt;N/A&lt;1}                                 |         {1&gt;N/A&lt;1}         |         {1&gt;N/A&lt;1}         |         {1&gt;N/A&lt;1}         |         {1&gt;N/A&lt;1}         |         {1&gt;N/A&lt;1}         |          {1&gt;N/A&lt;1}           |
|                                                          Configuração da lacuna de MMIO                                                           |        2019, 2016, 2012 R2         |                              &#10004;                               |                              &#10004;                               |                              &#10004;                               |      &#10004;       |      &#10004;       |      &#10004;       |      &#10004;       |      &#10004;       |        &#10004;        |
|                                                           Memória Dinâmica-adição a quente                                                           |     2019, 2016, 2012 R2      |                       &#10004;Nota 8, 9, 10                        |                       &#10004;Nota 8, 9, 10                        |                       &#10004;Nota 8, 9, 10                        | &#10004;Nota 9, 10 | &#10004;Nota 9, 10 | &#10004;Nota 9, 10 | &#10004;Nota 9, 10 | &#10004;Nota 9, 10 | &#10004;Nota 8, 9, 10 |
|                                                         Memória Dinâmica-balões                                                          |     2019, 2016, 2012 R2      |                       &#10004;Nota 8, 9, 10                        |                       &#10004;Nota 8, 9, 10                        |                       &#10004;Nota 8, 9, 10                        | &#10004;Nota 9, 10 | &#10004;Nota 9, 10 | &#10004;Nota 9, 10 | &#10004;Nota 9, 10 | &#10004;Nota 9, 10 | &#10004;Nota 8, 9, 10 |
|                                                            Redimensionamento de memória de Runtime                                                             |             2019, 2016             |                              &#10004;                               |                              &#10004;                               |                              &#10004;                               |                     |                     |                     |                     |                     |                        |
|                         **[Monitor](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#video)**                         |                                    |                                                                     |                                                                     |                                                                     |                     |                     |                     |                     |                     |                        |
|                                                        Dispositivo de vídeo específico do Hyper-V                                                         | 2019, 2016, 2012 R2 |                              &#10004;                               |                              &#10004;                               |                              &#10004;                               |      &#10004;       |      &#10004;       |      &#10004;       |      &#10004;       |      &#10004;       |        &#10004;        |
|                 **[Várias](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#miscellaneous)**                 |                                    |                                                                     |                                                                     |                                                                     |                     |                     |                     |                     |                     |                        |
|                                                                Par chave-valor                                                                | 2019, 2016, 2012 R2 |                              &#10004;                               |                              &#10004;                               |                              &#10004;                               |      &#10004;       |      &#10004;       |      &#10004;       |      &#10004;       |      &#10004;       |        &#10004;        |
|                                                            Interrupção não mascarável                                                            |        2019, 2016, 2012 R2         |                              &#10004;                               |                              &#10004;                               |                              &#10004;                               |      &#10004;       |      &#10004;       |      &#10004;       |      &#10004;       |      &#10004;       |        &#10004;        |
|                                                         Cópia de arquivo do host para o convidado                                                         |        2019, 2016, 2012 R2         |                              &#10004;                               |                              &#10004;                               |                              &#10004;                               |      &#10004;       |      &#10004;       |      &#10004;       |      &#10004;       |      &#10004;       |                        |
|                                                               comando lsvmbus                                                                | 2019, 2016, 2012 R2 |                              &#10004;                               |                              &#10004;                               |                              &#10004;                               |                     |                     |                     |                     |                     |                        |
|                                                               Soquetes do Hyper-V                                                                |             2019, 2016             |                              &#10004;                               |                              &#10004;                               |                              &#10004;                               |                     |                     |                     |                     |                     |                        |
|                                                             Passagem de PCI/DDA                                                              |             2019, 2016             |                              &#10004;                               |                              &#10004;                               |                                                                     |      &#10004;       |      &#10004;       |      &#10004;       |                     |                     |                        |
| **[Máquinas virtuais de geração 2](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#generation-2-virtual-machines)** |                                    |                                                                     |                                                                     |                                                                     |                     |                     |                     |                     |                     |                        |
|                                                               Inicializar usando UEFI                                                                |        2019, 2016, 2012 R2         |                          &#10004;Nota 14                           |                          &#10004;Nota 14                           |                          &#10004;Nota 14                           |  &#10004;Nota 14   |  &#10004;Nota 14   |  &#10004;Nota 14   |  &#10004;Nota 14   |  &#10004;Nota 14   |    &#10004;Nota 14    |
|                                                                 Inicialização segura                                                                  |             2019, 2016             |                              &#10004;                               |                              &#10004;                               |                              &#10004;                               |      &#10004;       |      &#10004;       |      &#10004;       |      &#10004;       |      &#10004;       |        &#10004;        |


## <a name="rhelcentos-6x-series"></a>Série RHEL/CentOS 6. x

O kernel de 32 bits para esta série é habilitado para PAE. Não há suporte interno de LIS para RHEL/CentOS 6.0-6.3.

|  **Recurso**  | **Versão do Windows Server** |  **6.7-6.10** |  **6.4-6.6** | **6.0-6.3** |   **6,10, 6,9, 6,8**   |       **6,6, 6,7**        |          **6,5**          |          **6,4**           |
|---------------|----------------------------|---------------|--------------|-------------|------------------------|---------------------------|----------------------------|---------------------------|
|  **Disponibilidade** |   | [LIS 4,3](https://www.microsoft.com/download/details.aspx?id=55106) | [LIS 4,3](https://www.microsoft.com/download/details.aspx?id=55106) | [LIS 4,3](https://www.microsoft.com/download/details.aspx?id=55106) |        Interno        |         Interno          |         Interno          |          Interno          |
|  **[Core](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#core)** | 2019, 2016, 2012 R2 |  &#10004; | &#10004;  | &#10004;  | &#10004; | &#10004; | &#10004;| &#10004; |
|  Tempo preciso do Windows Server 2016 | 2019, 2016 | |  | |  |  |   |   |
|  **[Rede](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#networking)**  | |   |  | |  |  |   |  |
|  Quadros jumbo | 2019, 2016, 2012 R2 | &#10004; |  &#10004; | &#10004; | &#10004; | &#10004; | &#10004; | &#10004; |
|  Marcação e entroncamento de VLAN | 2019, 2016, 2012 R2 | &#10004;Observação 1 | &#10004;Observação 1 | &#10004;Observação 1 | &#10004;Observação 1 | &#10004;Observação 1|  &#10004;Observação 1 |&#10004;Observação 1 |
|  Migração ao vivo | 2019, 2016, 2012 R2 | &#10004; | &#10004; | &#10004;| &#10004; | &#10004; | &#10004;  | &#10004; |
|  Injeção de IP estático |  2019, 2016, 2012 R2 | &#10004;Observação 2 |  &#10004;Observação 2  | &#10004;Observação 2 | &#10004;Observação 2 | &#10004;Observação 2 | &#10004;Observação 2  | &#10004;Observação 2 |
|  vRSS  | 2019, 2016, 2012 R2 | &#10004; | &#10004; |  &#10004; | &#10004; | &#10004;  |   |   |
|  Segmentação de TCP e descarregamentos de soma de verificação | 2019, 2016, 2012 R2 | &#10004; | &#10004; | &#10004; | &#10004; | &#10004;  |   |    |
|  SR-IOV   | 2019, 2016 |    |  |   |   |   |   |  |
|  **[Repositório](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#storage)**  |  |   |   |  | |  |  | |
|  Redimensionamento de VHDX | 2019, 2016, 2012 R2| &#10004; | &#10004; | &#10004; | &#10004; | &#10004; | &#10004; |  |
|  Fibre Channel Virtual  | 2019, 2016, 2012 R2 |  &#10004;Observação 3  | &#10004;Observação 3  | &#10004;Observação 3  | &#10004;Observação 3 | &#10004;Observação 3  | &#10004;Observação 3  |    |
|  Backup de máquina virtual ao vivo | 2019, 2016, 2012 R2 | &#10004;Observação 5  | &#10004;Observação 5  | &#10004;Observação 5 | &#10004;Observação 4, 5 | &#10004;Observação 4, 5 | &#10004;Observação 4, 5, 6 | &#10004;Observação 4, 5, 6 |
|  Suporte a corte  | 2019, 2016, 2012 R2  | &#10004; | &#10004; | &#10004; | &#10004; |  |  |  |
|  WWN DO SCSI  | 2019, 2016, 2012 R2  | &#10004; | &#10004;  | &#10004;  |  |   |  |  |
|  **[Memória](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#memory)** | |  | | |  | |  |  |
|  Suporte ao kernel de PAE | 2019, 2016, 2012 R2 | &#10004;  | &#10004;  | &#10004; | &#10004; |  &#10004;  |  &#10004; |  &#10004; |
|  Configuração da lacuna de MMIO  | 2019, 2016, 2012 R2 | &#10004;  | &#10004;  | &#10004;  |  &#10004;  | &#10004;  |  &#10004; |  &#10004; |
|  Memória Dinâmica-adição a quente | 2019, 2016, 2012 R2 |  &#10004;Observação 7, 9, 10  | &#10004;Observação 7, 9, 10 | &#10004;Observação 7, 9, 10 | &#10004;Observação 7, 9, 10 | &#10004;Observação: 7, 8, 9, 10 | &#10004;Observação: 7, 8, 9, 10 | |
|  Memória Dinâmica-balões | 2019, 2016, 2012 R2 | &#10004;Observação 7, 9, 10  | &#10004;Observação 7, 9, 10  | &#10004;Observação 7, 9, 10 | &#10004;Observação 7, 9, 10 |  &#10004;Observação 7, 9, 10   |  &#10004;Observação 7, 9, 10   | &#10004;Observação: 7, 9, 10, 11 |
| Redimensionamento de memória de Runtime | 2019, 2016  |  |   |  |  | |  |  |
| **[Monitor](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#video)** || | | |  |  |  | |
| Dispositivo de vídeo específico do Hyper-V | 2019, 2016, 2012 R2 | &#10004;  | &#10004;  | &#10004;  | &#10004; | &#10004; | &#10004; | |
| **[Várias](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#miscellaneous)** |  |  |  |   |  | |  |  |
| Par chave-valor | 2019, 2016, 2012 R2 | &#10004; | &#10004;| &#10004; | &#10004;Nota 12 | &#10004;Nota 12 | &#10004;Nota 12, 13 | &#10004;Nota 12, 13 |
| Interrupção não mascarável | 2019, 2016, 2012 R2 | &#10004;  | &#10004;  | &#10004; | &#10004; | &#10004;  |  &#10004;| &#10004; |
| Cópia de arquivo do host para o convidado | 2019, 2016, 2012 R2 | &#10004;  |  &#10004; | &#10004; | &#10004; | &#10004; | |  |
| comando lsvmbus | 2019, 2016, 2012 R2 |  &#10004; |  &#10004;  |  &#10004; |   |   |    |  |
| Soquetes do Hyper-V | 2019, 2016  | &#10004;  |  &#10004;  |  &#10004; |  |   |   |  |
| Passagem de PCI/DDA | 2019, 2016 | &#10004;  | |   |  |  | |   |
| **[Máquinas virtuais de geração 2](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#generation-2-virtual-machines)** | |  | | | | | | |
| Inicializar usando UEFI  | 2012 R2 |  |  |  |  |  | |
|  |2019, 2016 | &#10004;Nota 14 | &#10004;Nota 14| &#10004;Nota 14 |    &#10004;Nota 14    |  | |  |
|Inicialização segura| 2019, 2016|  ||  |  |  | ||



## <a name="rhelcentos-5x-series"></a>Série RHEL/CentOS 5. x

Esta série tem um kernel de PAE de 32 bits com suporte disponível. Não há suporte interno de LIS para RHEL/CentOS antes de 5,9.


|                                                                 **Recurso**                                                                  |     **Versão do Windows Server**     |                              5,2-5,11                              |                            **5.2-5.11**                             |    **5,9-5,11**     |
|----------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------|---------------------------------------------------------------------|---------------------------------------------------------------------|-----------------------|
|                                                               **Disponibilidade**                                                               |                                    | [LIS 4,3](https://www.microsoft.com/download/details.aspx?id=55106) | [LIS 4,1](https://www.microsoft.com/download/details.aspx?id=51612) |       Interno        |
|                          **[Core](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#core)**                          | 2019, 2016, 2012 R2 |                              &#10004;                               |                              &#10004;                               |       &#10004;        |
|                                                      Tempo preciso do Windows Server 2016                                                       |             2019, 2016             |                                                                     |                                                                     |                       |
|                    **[Rede](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#networking)**                    |                                    |                                                                     |                                                                     |                       |
|                                                                 Quadros jumbo                                                                 | 2019, 2016, 2012 R2 |                              &#10004;                               |                              &#10004;                               |       &#10004;        |
|                                                          Marcação e entroncamento de VLAN                                                           | 2019, 2016, 2012 R2 |                           &#10004;Observação 1                           |                           &#10004;Observação 1                           |    &#10004;Observação 1    |
|                                                                Migração ao vivo                                                                | 2019, 2016, 2012 R2 |                              &#10004;                               |                              &#10004;                               |       &#10004;        |
|                                                             Injeção de IP estático                                                              |     2019, 2016, 2012 R2      |                           &#10004;Observação 2                           |                           &#10004;Observação 2                           |    &#10004;Observação 2    |
|                                                                     vRSS                                                                     |        2019, 2016, 2012 R2         |                                                                     |                                                                     |                       |
|                                                    Segmentação de TCP e descarregamentos de soma de verificação                                                    | 2019, 2016, 2012 R2 |                              &#10004;                               |                              &#10004;                               |                       |
|                                                                    SR-IOV                                                                    |             2019, 2016             |                                                                     |                                                                     |                       |
|                       **[Repositório](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#storage)**                       |                                    |                                                                     |                                                                     |                       |
|                                                                 Redimensionamento de VHDX                                                                  |        2019, 2016, 2012 R2         |                              &#10004;                               |                              &#10004;                               |                       |
|                                                            Fibre Channel Virtual                                                             |        2019, 2016, 2012 R2         |                           &#10004;Observação 3                           |                           &#10004;Observação 3                           |                       |
|                                                         Backup de máquina virtual ao vivo                                                          |        2019, 2016, 2012 R2         |                         &#10004;Nota 5, 15                         |                           &#10004;Observação 5                           | &#10004;Observação 4, 5, 6 |
|                                                                 Suporte a corte                                                                 |        2019, 2016, 2012 R2         |                                                                     |                                                                     |                       |
|                                                                   WWN DO SCSI                                                                   |        2019, 2016, 2012 R2         |                                                                     |                                                                     |                       |
|                        **[Memória](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#memory)**                        |                                    |                                                                     |                                                                     |                       |
|                                                              Suporte ao kernel de PAE                                                              | 2019, 2016, 2012 R2 |                              &#10004;                               |                              &#10004;                               |       &#10004;        |
|                                                          Configuração da lacuna de MMIO                                                           |        2019, 2016, 2012 R2         |                              &#10004;                               |                              &#10004;                               |       &#10004;        |
|                                                           Memória Dinâmica-adição a quente                                                           |     2019, 2016, 2012 R2      |                                                                     |                                                                     |                       |
|                                                         Memória Dinâmica-balões                                                          |     2019, 2016, 2012 R2      |                     &#10004;Observação: 7, 9, 10, 11                      |                     &#10004;Observação: 7, 9, 10, 11                      |                       |
|                                                            Redimensionamento de memória de Runtime                                                             |             2019, 2016             |                                                                     |                                                                     |                       |
|                         **[Monitor](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#video)**                         |                                    |                                                                     |                                                                     |                       |
|                                                        Dispositivo de vídeo específico do Hyper-V                                                         | 2019, 2016, 2012 R2 |                              &#10004;                               |                              &#10004;                               |                       |
|                 **[Várias](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#miscellaneous)**                 |                                    |                                                                     |                                                                     |                       |
|                                                                Par chave-valor                                                                | 2019, 2016, 2012 R2 |                              &#10004;                               |                              &#10004;                               |                       |
|                                                            Interrupção não mascarável                                                            |        2019, 2016, 2012 R2         |                              &#10004;                               |                              &#10004;                               |       &#10004;        |
|                                                         Cópia de arquivo do host para o convidado                                                         |        2019, 2016, 2012 R2         |                              &#10004;                               |                              &#10004;                               |                       |
|                                                               comando lsvmbus                                                                | 2019, 2016, 2012 R2 |                                                                     |                                                                     |                       |
|                                                               Soquetes do Hyper-V                                                                |             2019, 2016             |                                                                     |                                                                     |                       |
|                                                             Passagem de PCI/DDA                                                              |             2019, 2016             |                                                                     |                                                                     |                       |
| **[Máquinas virtuais de geração 2](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#generation-2-virtual-machines)** |                                    |                                                                     |                                                                     |                       |
|                                                               Inicializar usando UEFI                                                                |        2019, 2016, 2012 R2         |                                                                     |                                                                     |                       |
|                                                                 Inicialização segura                                                                  |             2019, 2016             |                                                                     |                                                                     |                       |

## <a name="notes"></a>{1&gt;Observações&lt;1}

1. Para esta versão RHEL/CentOS, a marcação de VLAN funciona, mas o entroncamento de VLAN não.

2. A injeção de IP estático poderá não funcionar se o Gerenciador de rede tiver sido configurado para um determinado adaptador de rede sintético na máquina virtual. Para um funcionamento suave da injeção de IP estático, verifique se o Gerenciador de rede está desligado completamente ou se foi desligado para um adaptador de rede específico por meio de seu arquivo ifcfg-ethX.

3. No Windows Server 2012 R2, ao usar dispositivos de Fibre Channel virtual, verifique se o número de unidade lógica 0 (LUN 0) foi populado. Se o LUN 0 não tiver sido populado, uma máquina virtual Linux poderá não ser capaz de montar dispositivos Fibre Channel nativamente.

4. Para LIS interna, o pacote "HyperV-daemons" deve ser instalado para essa funcionalidade.

5. Se houver identificadores de arquivos abertos durante uma operação de backup de máquina virtual ao vivo, em alguns casos de canto, os VHDs com backup poderão ter que passar por uma verificação de consistência do sistema de arquivos (fsck) na restauração. As operações de backup dinâmico podem falhar silenciosamente se a máquina virtual tiver um dispositivo iSCSI conectado ou um armazenamento de conexão direta (também conhecido como um disco de passagem).

6. Embora o download do Linux Integration Services seja preferencial, o suporte ao Live backup para RHEL/CentOS 5,9-5.11/6.4/6.5 também está disponível por meio [do Essentials do backup do Hyper-V para Linux](https://github.com/LIS/backupessentials/tree/1.0).

7. O suporte à memória dinâmica só está disponível em máquinas virtuais de 64 bits.

8. O suporte de adição automática não está habilitado por padrão nesta distribuição. Para habilitar o suporte de adição automática, você precisa adicionar uma regra udev em/etc/udev/rules.d/da seguinte maneira:

   1. Crie um arquivo **/etc/udev/rules.d/100-Balloon.Rules**. Você pode usar qualquer outro nome desejado para o arquivo.

   2. Adicione o seguinte conteúdo ao arquivo: `SUBSYSTEM=="memory", ACTION=="add", ATTR{state}="online"`

   3. Reinicialize o sistema para habilitar o suporte a Hot-Add.

   Enquanto o download do Integration Services do Linux cria essa regra na instalação, a regra também é removida quando o LIS é desinstalado, portanto, a regra deve ser recriada se a memória dinâmica for necessária após a desinstalação.

9. As operações de memória dinâmica podem falhar se o sistema operacional convidado estiver sendo executado com pouca memória. Veja a seguir algumas práticas recomendadas:

   * A memória de inicialização e a memória mínima devem ser iguais ou maiores que a quantidade de memória que o fornecedor de distribuição recomenda.

   * Os aplicativos que tendem a consumir toda a memória disponível em um sistema estão limitados a consumir até 80% da RAM disponível.

10. Se você estiver usando Memória Dinâmica em um sistema operacional Windows Server 2016 ou Windows Server 2012 R2, especifique a **memória de inicialização**, **memória mínima**e parâmetros de **memória máxima** em múltiplos de 128 megabytes (MB). Não fazer isso pode levar a falhas de adição automática e talvez você não veja nenhum aumento de memória em um sistema operacional convidado.

11. Determinadas distribuições, incluindo as que usam LIS 4,0 e 4,1, fornecem apenas suporte a balões e não fornecem suporte de adição automática. Nesse cenário, o recurso de memória dinâmica pode ser usado definindo o parâmetro de memória de inicialização para um valor que é igual ao parâmetro de memória máxima. Isso faz com que toda a memória necessária seja adicionada à máquina virtual no momento da inicialização e, depois, dependendo dos requisitos de memória do host, o Hyper-V pode alocar ou desalocar livremente a memória do convidado usando o balão. Configure a **memória de inicialização** e a **memória mínima** no ou acima do valor recomendado para a distribuição.

12. Para habilitar a infraestrutura de par chave/valor (KVP), instale o pacote RPM do hypervkvpd ou HyperV-daemons do seu ISO RHEL. Como alternativa, o pacote pode ser instalado diretamente de repositórios do RHEL.

13. A infraestrutura do par chave/valor (KVP) pode não funcionar corretamente sem uma atualização de software do Linux. Entre em contato com seu fornecedor de distribuição para obter a atualização de software caso você veja problemas com esse recurso.

14. Em máquinas virtuais do Windows Server 2012 R2 geração 2 têm inicialização segura habilitada por padrão e algumas máquinas virtuais do Linux não serão inicializadas a menos que a opção de inicialização segura esteja desabilitada. Você pode desabilitar a inicialização segura na seção **firmware** das configurações da máquina virtual no Gerenciador do **Hyper-V** ou pode desabilitá-la usando o PowerShell:

    ```Powershell
    Set-VMFirmware -VMName "VMname" -EnableSecureBoot Off
    ```

    O download do Integration Services do Linux pode ser aplicado a VMs existentes de geração 2, mas não comunicar a funcionalidade de geração 2.

15. Em Red Hat Enterprise Linux ou CentOS 5,2, 5,3 e 5,4 a funcionalidade de congelamento do sistema de arquivos não está disponível, portanto, o backup de máquina virtual em tempo real também não está disponível.

Consulte também

* [Set-VMFirmware](https://technet.microsoft.com/library/dn464287.aspx)

* [Máquinas virtuais do Debian com suporte no Hyper-V](Supported-Debian-virtual-machines-on-Hyper-V.md)

* [Máquinas virtuais Oracle Linux com suporte no Hyper-V](Supported-Oracle-Linux-virtual-machines-on-Hyper-V.md)

* [Máquinas virtuais SUSE com suporte no Hyper-V](Supported-SUSE-virtual-machines-on-Hyper-V.md)

* [Máquinas virtuais Ubuntu com suporte no Hyper-V](Supported-Ubuntu-virtual-machines-on-Hyper-V.md)

* [Máquinas virtuais FreeBSD com suporte no Hyper-V](Supported-FreeBSD-virtual-machines-on-Hyper-V.md)

* [Descrições de recursos para máquinas virtuais Linux e FreeBSD no Hyper-V](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md)

* [Práticas recomendadas para executar o Linux no Hyper-V](Best-Practices-for-running-Linux-on-Hyper-V.md)

* [Certificação de hardware Red Hat](https://hardware.redhat.com/&quicksearch=Microsoft)
