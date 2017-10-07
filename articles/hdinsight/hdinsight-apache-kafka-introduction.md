---
title: "aaaAn 簡介 tooApache HDInsight 的 Azure 上 Kafka |Microsoft 文件"
description: "深入了解 HDInsight 上的 Apache Kafka： 它是什麼、 它的功能和 toofind 範例及取得啟動資訊。"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: f284b6e3-5f3b-4a50-b455-917e77588069
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/15/2017
ms.author: larryfr
ms.openlocfilehash: 1bc198d4cf93a4682030d4fa5f71030f49ad64be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="introducing-apache-kafka-on-hdinsight-preview"></a><span data-ttu-id="5e94d-103">HDInsight 上的 Apache Kafka (預覽) 簡介</span><span class="sxs-lookup"><span data-stu-id="5e94d-103">Introducing Apache Kafka on HDInsight (preview)</span></span>

<span data-ttu-id="5e94d-104">[Apache Kafka](https://kafka.apache.org)開放原始碼分散式資料流平台可能是使用的 toobuild 即時串流資料管線和應用程式。</span><span class="sxs-lookup"><span data-stu-id="5e94d-104">[Apache Kafka](https://kafka.apache.org) is an open-source distributed streaming platform that can be used toobuild real-time streaming data pipelines and applications.</span></span> <span data-ttu-id="5e94d-105">Kafka 也會提供訊息代理程式的功能類似 tooa 訊息佇列，您可以在其中發佈和訂閱 toonamed 資料流。</span><span class="sxs-lookup"><span data-stu-id="5e94d-105">Kafka also provides message broker functionality similar tooa message queue, where you can publish and subscribe toonamed data streams.</span></span> <span data-ttu-id="5e94d-106">Kafka HDInsight 上的為您提供 hello Microsoft Azure 雲端中受管理、 高擴充性和高可用性服務。</span><span class="sxs-lookup"><span data-stu-id="5e94d-106">Kafka on HDInsight provides you with a managed, highly scalable, and highly available service in hello Microsoft Azure cloud.</span></span>

## <a name="why-use-kafka-on-hdinsight"></a><span data-ttu-id="5e94d-107">為何使用 HDInsight 上的 Kafka？</span><span class="sxs-lookup"><span data-stu-id="5e94d-107">Why use Kafka on HDInsight?</span></span>

<span data-ttu-id="5e94d-108">Kafka 提供下列功能的 hello:</span><span class="sxs-lookup"><span data-stu-id="5e94d-108">Kafka provides hello following features:</span></span>

* <span data-ttu-id="5e94d-109">發行-訂閱訊息模式： Kafka 提供生產者 API，以發行記錄 tooa Kafka 主題。</span><span class="sxs-lookup"><span data-stu-id="5e94d-109">Publish-subscribe messaging pattern: Kafka provides a Producer API for publishing records tooa Kafka topic.</span></span> <span data-ttu-id="5e94d-110">訂閱 tooa 主題時，會使用 hello 取用者應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="5e94d-110">hello Consumer API is used when subscribing tooa topic.</span></span>

* <span data-ttu-id="5e94d-111">串流處理︰Kafka 通常與 Apache Storm 或 Spark 一起用來處理即時串流。</span><span class="sxs-lookup"><span data-stu-id="5e94d-111">Stream processing: Kafka is often used with Apache Storm or Spark for real-time stream processing.</span></span> <span data-ttu-id="5e94d-112">Kafka 0.10.0.0 (HDInsight 3.5 版) 導入了資料流處理的 API，可讓您串流處理解決方案，而不需要風暴或 Spark toobuild。</span><span class="sxs-lookup"><span data-stu-id="5e94d-112">Kafka 0.10.0.0 (HDInsight version 3.5) introduced a streaming API that allows you toobuild streaming solutions without requiring Storm or Spark.</span></span>

* <span data-ttu-id="5e94d-113">水平縮放： Kafka hello hello HDInsight 叢集節點之間分割資料流。</span><span class="sxs-lookup"><span data-stu-id="5e94d-113">Horizontal scale: Kafka partitions streams across hello nodes in hello HDInsight cluster.</span></span> <span data-ttu-id="5e94d-114">取用者處理程序可以與個別資料分割 tooprovide 負載平衡使用的記錄時產生關聯。</span><span class="sxs-lookup"><span data-stu-id="5e94d-114">Consumer processes can be associated with individual partitions tooprovide load balancing when consuming records.</span></span>

* <span data-ttu-id="5e94d-115">依序傳遞： 內每個資料分割，記錄會儲存在已收到 hello 順序中的 hello 資料流。</span><span class="sxs-lookup"><span data-stu-id="5e94d-115">In-order delivery: Within each partition, records are stored in hello stream in hello order that they were received.</span></span> <span data-ttu-id="5e94d-116">每個資料分割與一個取用者處理序建立關聯之後，就能保證依序處理記錄。</span><span class="sxs-lookup"><span data-stu-id="5e94d-116">By associating one consumer process per partition, you can guarantee that records are processed in-order.</span></span>

* <span data-ttu-id="5e94d-117">容錯： 資料分割可以複寫之間節點 tooprovide 容錯功能。</span><span class="sxs-lookup"><span data-stu-id="5e94d-117">Fault-tolerant: Partitions can be replicated between nodes tooprovide fault tolerance.</span></span>

* <span data-ttu-id="5e94d-118">Azure 受管理的磁碟與整合： hello hello hello HDInsight 叢集中的虛擬機器所使用的磁碟管理磁碟提供更高規模和輸送量。</span><span class="sxs-lookup"><span data-stu-id="5e94d-118">Integration with Azure Managed Disks: Managed disks provides higher scale and throughput for hello disks used by hello virtual machines in hello HDInsight cluster.</span></span>

    <span data-ttu-id="5e94d-119">預設會啟用受管理的磁碟的 HDInsight 上 Kafka 和 hello 每個節點使用的磁碟數目可以 HDInsight 建立期間設定。</span><span class="sxs-lookup"><span data-stu-id="5e94d-119">Managed disks are enabled by default for Kafka on HDInsight, and hello number of disks used per node can be configured during HDInsight creation.</span></span> <span data-ttu-id="5e94d-120">如需受控磁碟的詳細資訊，請參閱 [Azure 受控磁碟](../virtual-machines/windows/managed-disks-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="5e94d-120">For more information on managed disks, see [Azure Managed Disks](../virtual-machines/windows/managed-disks-overview.md).</span></span>

    <span data-ttu-id="5e94d-121">如需使用 HDInsight 上的 Kafka 設定受控磁碟的資訊，請參閱[提高 HDInsight 上的 Kafka 延展性](hdinsight-apache-kafka-scalability.md)。</span><span class="sxs-lookup"><span data-stu-id="5e94d-121">For information on configuring managed disks with Kafka on HDInsight, see [Increase scalability of Kafka on HDInsight](hdinsight-apache-kafka-scalability.md).</span></span>

## <a name="use-cases"></a><span data-ttu-id="5e94d-122">使用案例</span><span class="sxs-lookup"><span data-stu-id="5e94d-122">Use cases</span></span>

* <span data-ttu-id="5e94d-123">**傳訊**： 因為它支援 hello 發行-訂閱訊息模式、 Kafka 通常是當做訊息仲介。</span><span class="sxs-lookup"><span data-stu-id="5e94d-123">**Messaging**: Since it supports hello publish-subscribe message pattern, Kafka is often used as a message broker.</span></span>

* <span data-ttu-id="5e94d-124">**活動追蹤**： 因為 Kafka 提供的記錄順序中記錄，所以可以使用的 tootrack 且重新建立活動。</span><span class="sxs-lookup"><span data-stu-id="5e94d-124">**Activity tracking**: Since Kafka provides in-order logging of records, it can be used tootrack and re-create activities.</span></span> <span data-ttu-id="5e94d-125">例如，網站或應用程式中的使用者動作。</span><span class="sxs-lookup"><span data-stu-id="5e94d-125">For example, user actions on a web site or within an application.</span></span>

* <span data-ttu-id="5e94d-126">**彙總**： 使用資料流處理，您可以從不同的資料流 toocombine 資訊彙總並集中管理將操作資料的 hello 資訊。</span><span class="sxs-lookup"><span data-stu-id="5e94d-126">**Aggregation**: Using stream processing, you can aggregate information from different streams toocombine and centralize hello information into operational data.</span></span>

* <span data-ttu-id="5e94d-127">**轉換**︰您可以利用串流處理來結合並充實多個輸入主題的資料，而成為一個或多個輸出主題。</span><span class="sxs-lookup"><span data-stu-id="5e94d-127">**Transformation**: Using stream processing, you can combine and enrich data from multiple input topics into one or more output topics.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5e94d-128">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5e94d-128">Next steps</span></span>

<span data-ttu-id="5e94d-129">如何使用 hello 下列連結的 toolearn toouse Apache Kafka HDInsight 上：</span><span class="sxs-lookup"><span data-stu-id="5e94d-129">Use hello following links toolearn how toouse Apache Kafka on HDInsight:</span></span>

* [<span data-ttu-id="5e94d-130">開始使用 HDInsight 上的 Kafka</span><span class="sxs-lookup"><span data-stu-id="5e94d-130">Get started with Kafka on HDInsight</span></span>](hdinsight-apache-kafka-get-started.md)

* [<span data-ttu-id="5e94d-131">在 HDInsight 上使用 MirrorMaker toocreate Kafka 的複本</span><span class="sxs-lookup"><span data-stu-id="5e94d-131">Use MirrorMaker toocreate a replica of Kafka on HDInsight</span></span>](hdinsight-apache-kafka-mirroring.md)

* [<span data-ttu-id="5e94d-132">使用 Apache Storm 搭配 HDInsight 上的 Kafka</span><span class="sxs-lookup"><span data-stu-id="5e94d-132">Use Apache Storm with Kafka on HDInsight</span></span>](hdinsight-apache-storm-with-kafka.md)

* [<span data-ttu-id="5e94d-133">使用 Apache Spark 搭配 Kafka on HDInsight</span><span class="sxs-lookup"><span data-stu-id="5e94d-133">Use Apache Spark with Kafka on HDInsight</span></span>](hdinsight-apache-spark-with-kafka.md)

* [<span data-ttu-id="5e94d-134">透過 Azure 虛擬網路連線 tooKafka</span><span class="sxs-lookup"><span data-stu-id="5e94d-134">Connect tooKafka through an Azure Virtual Network</span></span>](hdinsight-apache-kafka-connect-vpn-gateway.md)
