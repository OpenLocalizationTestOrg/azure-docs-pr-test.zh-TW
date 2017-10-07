---
title: "使用 Apache Kafka-Azure HDInsight aaaHigh 可用性 |Microsoft 文件"
description: "深入了解如何使用 Azure HDInsight 上的 Apache Kafka tooensure 高可用性。 了解如何 toorebalance 分割 Kafka 的複本，使其在不同容錯網域內 hello 包含 HDInsight 的 Azure 區域。"
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
ms.openlocfilehash: 337468f36b531f83c2999e87907de89cf3d19dd4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="high-availability-of-your-data-with-apache-kafka-preview-on-hdinsight"></a><span data-ttu-id="fd41c-104">使用 HDInsight 上的 Apache Kafka (預覽) 確保您資料的高可用性</span><span class="sxs-lookup"><span data-stu-id="fd41c-104">High availability of your data with Apache Kafka (preview) on HDInsight</span></span>

<span data-ttu-id="fd41c-105">了解如何 tooconfigure 磁碟分割複本的基礎硬體 Kafka 主題 tootake 利用機架組態。</span><span class="sxs-lookup"><span data-stu-id="fd41c-105">Learn how tooconfigure partition replicas for Kafka topics tootake advantage of underlying hardware rack configuration.</span></span> <span data-ttu-id="fd41c-106">此設定可確保資料儲存在 HDInsight 上的 Apache Kafka hello 可用性。</span><span class="sxs-lookup"><span data-stu-id="fd41c-106">This configuration ensures hello availability of data stored in Apache Kafka on HDInsight.</span></span>

## <a name="fault-and-update-domains-with-kafka"></a><span data-ttu-id="fd41c-107">容錯和更新網域與 Kafka</span><span class="sxs-lookup"><span data-stu-id="fd41c-107">Fault and update domains with Kafka</span></span>

<span data-ttu-id="fd41c-108">容錯網域是 Azure 資料中心內基礎硬體的邏輯群組。</span><span class="sxs-lookup"><span data-stu-id="fd41c-108">A fault domain is a logical grouping of underlying hardware in an Azure data center.</span></span> <span data-ttu-id="fd41c-109">每個容錯網域會共用通用電源和網路交換器。</span><span class="sxs-lookup"><span data-stu-id="fd41c-109">Each fault domain shares a common power source and network switch.</span></span> <span data-ttu-id="fd41c-110">hello 虛擬機器和實作 hello 節點內的 HDInsight 叢集的受管理的磁碟的分散這些容錯網域。</span><span class="sxs-lookup"><span data-stu-id="fd41c-110">hello virtual machines and managed disks that implement hello nodes within an HDInsight cluster are distributed across these fault domains.</span></span> <span data-ttu-id="fd41c-111">此架構會限制 hello 的實體硬體失敗的潛在影響。</span><span class="sxs-lookup"><span data-stu-id="fd41c-111">This architecture limits hello potential impact of physical hardware failures.</span></span>

<span data-ttu-id="fd41c-112">每個 Azure 區域有特定數目的容錯網域。</span><span class="sxs-lookup"><span data-stu-id="fd41c-112">Each Azure region has a specific number of fault domains.</span></span> <span data-ttu-id="fd41c-113">如需網域及它們包含的容錯網域的 hello 數目的清單，請參閱 hello[可用性設定組](../virtual-machines/linux/regions-and-availability.md#availability-sets)文件。</span><span class="sxs-lookup"><span data-stu-id="fd41c-113">For a list of domains and hello number of fault domains they contain, see hello [Availability sets](../virtual-machines/linux/regions-and-availability.md#availability-sets) documentation.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fd41c-114">Kafka 不知道容錯網域。</span><span class="sxs-lookup"><span data-stu-id="fd41c-114">Kafka is not aware of fault domains.</span></span> <span data-ttu-id="fd41c-115">當您建立主題 Kafka 中時，其可能會將所有資料分割的複本儲存在 hello 相同容錯網域。</span><span class="sxs-lookup"><span data-stu-id="fd41c-115">When you create a topic in Kafka, it may store all partition replicas in hello same fault domain.</span></span> <span data-ttu-id="fd41c-116">toosolve 這個問題，我們提供 hello [Kafka 分割重新平衡工具](https://github.com/hdinsight/hdinsight-kafka-tools)。</span><span class="sxs-lookup"><span data-stu-id="fd41c-116">toosolve this problem, we provide hello [Kafka partition rebalance tool](https://github.com/hdinsight/hdinsight-kafka-tools).</span></span>

## <a name="when-toorebalance-partition-replicas"></a><span data-ttu-id="fd41c-117">當 toorebalance 分割複本</span><span class="sxs-lookup"><span data-stu-id="fd41c-117">When toorebalance partition replicas</span></span>

<span data-ttu-id="fd41c-118">tooensure hello 最高的可用性 Kafka 資料，您應該重新 hello 磁碟分割複本平衡的主題在下列時間的 hello:</span><span class="sxs-lookup"><span data-stu-id="fd41c-118">tooensure hello highest availability of your Kafka data, you should rebalance hello partition replicas for your topic at hello following times:</span></span>

* <span data-ttu-id="fd41c-119">建立新主題或磁碟分割時</span><span class="sxs-lookup"><span data-stu-id="fd41c-119">When a new topic or partition is created</span></span>

* <span data-ttu-id="fd41c-120">當您相應增加叢集時</span><span class="sxs-lookup"><span data-stu-id="fd41c-120">When you scale up a cluster</span></span>

## <a name="replication-factor"></a><span data-ttu-id="fd41c-121">複寫因子</span><span class="sxs-lookup"><span data-stu-id="fd41c-121">Replication factor</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fd41c-122">我們建議使用包含三個容錯網域的 Azure 地區，以及使用複寫因子 3。</span><span class="sxs-lookup"><span data-stu-id="fd41c-122">We recommend using an Azure region that contains three fault domains, and using a replication factor of 3.</span></span>

<span data-ttu-id="fd41c-123">如果您必須使用包含只有兩個容錯網域的區域，使用複寫因數的 4 個 toospread hello 複本平均橫跨 hello 兩個容錯網域。</span><span class="sxs-lookup"><span data-stu-id="fd41c-123">If you must use a region that contains only two fault domains, use a replication factor of 4 toospread hello replicas evenly across hello two fault domains.</span></span>

<span data-ttu-id="fd41c-124">建立主題和設定 hello 複寫因數的範例，請參閱 hello [Kafka HDInsight 上的開頭](hdinsight-apache-kafka-get-started.md)文件。</span><span class="sxs-lookup"><span data-stu-id="fd41c-124">For an example of creating topics and setting hello replication factor, see hello [Start with Kafka on HDInsight](hdinsight-apache-kafka-get-started.md) document.</span></span>

## <a name="how-toorebalance-partition-replicas"></a><span data-ttu-id="fd41c-125">Toorebalance 分割複本的方式</span><span class="sxs-lookup"><span data-stu-id="fd41c-125">How toorebalance partition replicas</span></span>

<span data-ttu-id="fd41c-126">使用 hello [Kafka 分割重新平衡工具](https://github.com/hdinsight/hdinsight-kafka-tools)toorebalance 選取主題。</span><span class="sxs-lookup"><span data-stu-id="fd41c-126">Use hello [Kafka partition rebalance tool](https://github.com/hdinsight/hdinsight-kafka-tools) toorebalance selected topics.</span></span> <span data-ttu-id="fd41c-127">從 Kafka 叢集的 SSH 工作階段 toohello 前端節點，就必須執行此工具。</span><span class="sxs-lookup"><span data-stu-id="fd41c-127">This tool must be ran from an SSH session toohello head node of your Kafka cluster.</span></span>

<span data-ttu-id="fd41c-128">如需有關如何連接使用 SSH tooHDInsight 的詳細資訊，請參閱[搭配使用 SSH 和 HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md)文件。</span><span class="sxs-lookup"><span data-stu-id="fd41c-128">For more information on connecting tooHDInsight using SSH, see the [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) document.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fd41c-129">後續步驟</span><span class="sxs-lookup"><span data-stu-id="fd41c-129">Next steps</span></span>

* [<span data-ttu-id="fd41c-130">HDInsight 上的 Kafka 延展性</span><span class="sxs-lookup"><span data-stu-id="fd41c-130">Scalability of Kafka on HDInsight</span></span>](hdinsight-apache-kafka-scalability.md)
* [<span data-ttu-id="fd41c-131">使用 HDInsight 上的 Kafka 進行鏡像處理</span><span class="sxs-lookup"><span data-stu-id="fd41c-131">Mirroring with Kafka on HDInsight</span></span>](hdinsight-apache-kafka-mirroring.md)