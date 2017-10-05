---
title: "使用 Apache Kafka 確保高可用性 - Azure HDInsight | Microsoft Docs"
description: "了解如何使用 Azure HDInsight 上的 Apache Kafka 確保高可用性。 了解如何重新平衡 Kafka 中的磁碟分割複本，使其位於包含 HDInsight 的 Azure 區域內的不同容錯網域上。"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: 
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/26/2017
ms.author: larryfr
ms.openlocfilehash: f8164d1c3483b28e5f2abcc8035da78880daec1e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="high-availability-of-your-data-with-apache-kafka-preview-on-hdinsight"></a><span data-ttu-id="391b2-104">使用 HDInsight 上的 Apache Kafka (預覽) 確保您資料的高可用性</span><span class="sxs-lookup"><span data-stu-id="391b2-104">High availability of your data with Apache Kafka (preview) on HDInsight</span></span>

<span data-ttu-id="391b2-105">了解如何設定 Kafka 主題的磁碟分割複本，以利用基礎硬體機架組態。</span><span class="sxs-lookup"><span data-stu-id="391b2-105">Learn how to configure partition replicas for Kafka topics to take advantage of underlying hardware rack configuration.</span></span> <span data-ttu-id="391b2-106">此組態可確保在 HDInsight 上 Apache Kafka 中儲存之資料的可用性。</span><span class="sxs-lookup"><span data-stu-id="391b2-106">This configuration ensures the availability of data stored in Apache Kafka on HDInsight.</span></span>

## <a name="fault-and-update-domains-with-kafka"></a><span data-ttu-id="391b2-107">容錯和更新網域與 Kafka</span><span class="sxs-lookup"><span data-stu-id="391b2-107">Fault and update domains with Kafka</span></span>

<span data-ttu-id="391b2-108">容錯網域是 Azure 資料中心內基礎硬體的邏輯群組。</span><span class="sxs-lookup"><span data-stu-id="391b2-108">A fault domain is a logical grouping of underlying hardware in an Azure data center.</span></span> <span data-ttu-id="391b2-109">每個容錯網域會共用通用電源和網路交換器。</span><span class="sxs-lookup"><span data-stu-id="391b2-109">Each fault domain shares a common power source and network switch.</span></span> <span data-ttu-id="391b2-110">實作 HDInsight 叢集內節點的虛擬機器和受控磁碟會分散於這些容錯網域。</span><span class="sxs-lookup"><span data-stu-id="391b2-110">The virtual machines and managed disks that implement the nodes within an HDInsight cluster are distributed across these fault domains.</span></span> <span data-ttu-id="391b2-111">此架構會限制實體硬體故障的潛在影響。</span><span class="sxs-lookup"><span data-stu-id="391b2-111">This architecture limits the potential impact of physical hardware failures.</span></span>

<span data-ttu-id="391b2-112">每個 Azure 區域有特定數目的容錯網域。</span><span class="sxs-lookup"><span data-stu-id="391b2-112">Each Azure region has a specific number of fault domains.</span></span> <span data-ttu-id="391b2-113">如需網域清單及其包含的容錯網域數目，請參閱[可用性設定組](../virtual-machines/linux/regions-and-availability.md#availability-sets)文件。</span><span class="sxs-lookup"><span data-stu-id="391b2-113">For a list of domains and the number of fault domains they contain, see the [Availability sets](../virtual-machines/linux/regions-and-availability.md#availability-sets) documentation.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="391b2-114">Kafka 不知道容錯網域。</span><span class="sxs-lookup"><span data-stu-id="391b2-114">Kafka is not aware of fault domains.</span></span> <span data-ttu-id="391b2-115">當您在 Kafka 中建立主題時，它可將所有磁碟分割複本儲存在相同的容錯網域中。</span><span class="sxs-lookup"><span data-stu-id="391b2-115">When you create a topic in Kafka, it may store all partition replicas in the same fault domain.</span></span> <span data-ttu-id="391b2-116">若要解決這個問題，我們提供 [Kafka 磁碟分割重新平衡工具](https://github.com/hdinsight/hdinsight-kafka-tools)。</span><span class="sxs-lookup"><span data-stu-id="391b2-116">To solve this problem, we provide the [Kafka partition rebalance tool](https://github.com/hdinsight/hdinsight-kafka-tools).</span></span>

## <a name="when-to-rebalance-partition-replicas"></a><span data-ttu-id="391b2-117">何時重新平衡磁碟分割複本</span><span class="sxs-lookup"><span data-stu-id="391b2-117">When to rebalance partition replicas</span></span>

<span data-ttu-id="391b2-118">若要確保 Kafka 資料的最高的可用性，您應該在下列時間重新平衡您主題的磁碟分割複本：</span><span class="sxs-lookup"><span data-stu-id="391b2-118">To ensure the highest availability of your Kafka data, you should rebalance the partition replicas for your topic at the following times:</span></span>

* <span data-ttu-id="391b2-119">建立新主題或磁碟分割時</span><span class="sxs-lookup"><span data-stu-id="391b2-119">When a new topic or partition is created</span></span>

* <span data-ttu-id="391b2-120">當您相應增加叢集時</span><span class="sxs-lookup"><span data-stu-id="391b2-120">When you scale up a cluster</span></span>

## <a name="replication-factor"></a><span data-ttu-id="391b2-121">複寫因子</span><span class="sxs-lookup"><span data-stu-id="391b2-121">Replication factor</span></span>

> [!IMPORTANT]
> <span data-ttu-id="391b2-122">我們建議使用包含三個容錯網域的 Azure 地區，以及使用複寫因子 3。</span><span class="sxs-lookup"><span data-stu-id="391b2-122">We recommend using an Azure region that contains three fault domains, and using a replication factor of 3.</span></span>

<span data-ttu-id="391b2-123">如果您必須使用只包含兩個容錯網域的區域，請使用複寫因子 4 將複本平均分散於兩個容錯網域。</span><span class="sxs-lookup"><span data-stu-id="391b2-123">If you must use a region that contains only two fault domains, use a replication factor of 4 to spread the replicas evenly across the two fault domains.</span></span>

<span data-ttu-id="391b2-124">如需建立主題及設定複寫因子的範例，請參閱[開始使用 HDInsight 上的 Kafka](hdinsight-apache-kafka-get-started.md)文件。</span><span class="sxs-lookup"><span data-stu-id="391b2-124">For an example of creating topics and setting the replication factor, see the [Start with Kafka on HDInsight](hdinsight-apache-kafka-get-started.md) document.</span></span>

## <a name="how-to-rebalance-partition-replicas"></a><span data-ttu-id="391b2-125">如何重新平衡磁碟分割複本</span><span class="sxs-lookup"><span data-stu-id="391b2-125">How to rebalance partition replicas</span></span>

<span data-ttu-id="391b2-126">使用 [Kafka 磁碟割區重新平衡工具](https://github.com/hdinsight/hdinsight-kafka-tools)來重新平衡所選的主題。</span><span class="sxs-lookup"><span data-stu-id="391b2-126">Use the [Kafka partition rebalance tool](https://github.com/hdinsight/hdinsight-kafka-tools) to rebalance selected topics.</span></span> <span data-ttu-id="391b2-127">必須從 Kafka 叢集前端節點的 SSH 工作階段執行此工具。</span><span class="sxs-lookup"><span data-stu-id="391b2-127">This tool must be ran from an SSH session to the head node of your Kafka cluster.</span></span>

<span data-ttu-id="391b2-128">如需使用 SSH 連線至 HDInsight 的詳細資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md) 文件。</span><span class="sxs-lookup"><span data-stu-id="391b2-128">For more information on connecting to HDInsight using SSH, see the [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) document.</span></span>

## <a name="next-steps"></a><span data-ttu-id="391b2-129">後續步驟</span><span class="sxs-lookup"><span data-stu-id="391b2-129">Next steps</span></span>

* [<span data-ttu-id="391b2-130">HDInsight 上的 Kafka 延展性</span><span class="sxs-lookup"><span data-stu-id="391b2-130">Scalability of Kafka on HDInsight</span></span>](hdinsight-apache-kafka-scalability.md)
* [<span data-ttu-id="391b2-131">使用 HDInsight 上的 Kafka 進行鏡像處理</span><span class="sxs-lookup"><span data-stu-id="391b2-131">Mirroring with Kafka on HDInsight</span></span>](hdinsight-apache-kafka-mirroring.md)