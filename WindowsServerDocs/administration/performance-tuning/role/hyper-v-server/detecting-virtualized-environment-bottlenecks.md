---
title: Detectando afunilamentos em um ambiente virtualizado
description: Como detectar e resolver possíveis afunilamentos de desempenho do Hyper-v
ms.prod: windows-server
ms.technology: performance-tuning-guide
ms.topic: article
ms.author: asmahi; sandysp; jopoulso
author: phstee
ms.date: 10/16/2017
ms.openlocfilehash: 211f35c151e94bc8b8a11a614edad18053cb18b9
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80851769"
---
# <a name="detecting-bottlenecks-in-a-virtualized-environment"></a>Detectando afunilamentos em um ambiente virtualizado

Esta seção deve fornecer algumas dicas sobre o que monitorar usando o monitor de desempenho e como identificar onde o problema pode ocorrer quando o host ou algumas das máquinas virtuais não são executadas como você esperava.

## <a name="processor-bottlenecks"></a>Afunilamentos de processador

Aqui estão alguns cenários comuns que poderiam causar afunilamentos de processador:

-   Um ou mais processadores lógicos estão carregados

-   Um ou mais processadores virtuais estão carregados

Você pode usar os seguintes contadores de desempenho do host:

-   Utilização do processador lógico-\\processador lógico do hipervisor Hyper-V (\*)\\% tempo de execução total

-   Utilização do processador virtual-\\processador virtual do hipervisor Hyper-V (\*)\\% tempo de execução total

-   Utilização do processador virtual raiz-\\processador virtual do hipervisor Hyper-V (\*)\\% tempo de execução total

Se o **processador lógico do hipervisor Hyper-V (\_total)\\contador de tempo de execução% total** for superior a 90%, o host estará sobrecarregado. Você deve adicionar mais capacidade de processamento ou mover algumas máquinas virtuais para um host diferente.

Se o **processador virtual do hipervisor Hyper-V (nome da VM: VP x)\\% total** do contador de tempo de execução for de mais de 90% para todos os processadores virtuais, você deverá fazer o seguinte:

-   Verifique se o host não está sobrecarregado

-   Descubra se a carga de trabalho pode aproveitar mais processadores virtuais

-   Atribuir mais processadores virtuais à máquina virtual

Se o **processador virtual do hipervisor Hyper-V (nome da VM: VP x)\\% total** do contador de tempo de execução for de mais de 90% para alguns, mas não para todos, dos processadores virtuais, você deverá fazer o seguinte:

-   Se sua carga de trabalho receber uso intensivo de rede, você deverá considerar o uso de vRSS.

-   Se as máquinas virtuais não estiverem executando o Windows Server 2012 R2, você deverá adicionar mais adaptadores de rede.

-   Se sua carga de trabalho for de uso intensivo de armazenamento, você deverá habilitar o NUMA virtual e adicionar mais discos virtuais.

Se o **processador virtual raiz do hipervisor Hyper-V (VP raiz x)\\% total** do contador de tempo de execução for de mais de 90% para alguns, mas nem todos os processadores virtuais e o **processador (x)\\% tempo de interrupção e processador (x)\\%** do contador de tempo de DPC aproximadamente se somam ao valor do **processador virtual raiz (VP de raiz x)\\contador de tempo de execução total** , você deve garantir a habilitação da VMQ nos adaptadores de rede.

## <a name="memory-bottlenecks"></a>Afunilamentos de memória

Aqui estão alguns cenários comuns que podem causar gargalos de memória:

-   O host não está respondendo.

-   As máquinas virtuais não podem ser iniciadas.

-   As máquinas virtuais ficam sem memória.

Você pode usar os seguintes contadores de desempenho do host:

-   Memória\\MBytes disponíveis

-   O balanceador de Memória Dinâmica do Hyper-V (\*)\\memória disponível

Você pode usar os seguintes contadores de desempenho da máquina virtual:

-   Memória\\MBytes disponíveis

Se a **memória\\MBytes disponíveis** e o **balanceador de memória dinâmica do Hyper-V (\*)\\** os contadores de memória disponíveis estiverem insuficientes no host, você deverá parar os serviços não essenciais e migrar uma ou mais máquinas virtuais para outro host.

Se o contador **memória\\MB disponíveis** estiver baixo na máquina virtual, você deverá atribuir mais memória à máquina virtual. Se você estiver usando Memória Dinâmica, deverá aumentar a configuração de memória máxima.

## <a name="network-bottlenecks"></a>Afunilamentos de rede

Aqui estão alguns cenários comuns que poderiam causar afunilamentos de rede:

-   O host está associado à rede.

-   A máquina virtual está ligada à rede.

Você pode usar os seguintes contadores de desempenho do host:

-   Interface de rede (*nome do adaptador de rede*)\\bytes/s

Você pode usar os seguintes contadores de desempenho da máquina virtual:

-   Adaptador de rede virtual do Hyper-V (*nome do nome da máquina virtual&lt;&gt;do GUID* )\\bytes/s

Se o contador **bytes de NIC física/s** for maior ou igual a 90% da capacidade, você deverá adicionar adaptadores de rede adicionais, migrar máquinas virtuais para outro host e configurar a QoS de rede.

Se o contador **bytes/s do adaptador de rede virtual do Hyper-V** for maior ou igual a 250 Mbps, você deverá adicionar adaptadores de rede agrupados adicionais na máquina virtual, habilitar o vRSS e usar o Sr-iov.

Se suas cargas de trabalho não puderem atender à latência de rede, habilite a SR-IOV para apresentar os recursos do adaptador de rede física à máquina virtual.

## <a name="storage-bottlenecks"></a>Afunilamentos de armazenamento

Aqui estão alguns cenários comuns que poderiam causar gargalos de armazenamento:

-   As operações de host e máquina virtual são lentas ou expiram.

-   A máquina virtual está lenta.

Você pode usar os seguintes contadores de desempenho do host:

-   Disco físico (*letra do disco*)\\média de disco s/leitura

-   Disco físico (*letra do disco*)\\média de disco s/gravação

-   Disco físico (*letra do disco*)\\tamanho médio da fila de leitura de disco

-   Disco físico (*letra do disco*)\\comprimento médio da fila de gravação de disco

Se as latências forem consistentemente maiores que 50 ms, você deverá fazer o seguinte:

-   Distribuir máquinas virtuais entre armazenamentos adicionais

-   Considere comprar um armazenamento mais rápido

-   Considere os espaços de armazenamento em camadas, que foram introduzidos no Windows Server 2012 R2

-   Considere o uso de QoS de armazenamento, que foi introduzido no Windows Server 2012 R2

-   Usar VHDX

## <a name="see-also"></a>Consulte também

-   [Terminologia do Hyper-V](terminology.md)

-   [Arquitetura Hyper-V](architecture.md)

-   [Configuração do servidor do Hyper-V](configuration.md)

-   [Desempenho do processador do Hyper-V](processor-performance.md)

-   [Desempenho de memória do Hyper-V](memory-performance.md)

-   [Desempenho de E/S de armazenamento do Hyper-V](storage-io-performance.md)

-   [Desempenho de E/S de rede do Hyper-V](network-io-performance.md)

-   [Máquinas virtuais do Linux](linux-virtual-machine-considerations.md)
