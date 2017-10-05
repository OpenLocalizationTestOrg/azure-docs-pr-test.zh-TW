---
title: "HDInsight 上的 Apache Kafka 簡介 - Azure | Microsoft Docs"
description: "了解 HDInsight 上的 Apache Kafka：它是什麼、其用途以及到何處尋找範例和入門資訊。"
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
ms.openlocfilehash: 1976c52bd7fa56bb07104e205ab3699b2dfa4c50
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="introducing-apache-kafka-on-hdinsight-preview"></a><span data-ttu-id="e6f80-103">HDInsight 上的 Apache Kafka (預覽) 簡介</span><span class="sxs-lookup"><span data-stu-id="e6f80-103">Introducing Apache Kafka on HDInsight (preview)</span></span>

<span data-ttu-id="e6f80-104">[Apache Kafka](https://kafka.apache.org) 是開放原始碼分散式串流平台，可用來建置即時串流資料管線和應用程式。</span><span class="sxs-lookup"><span data-stu-id="e6f80-104">[Apache Kafka](https://kafka.apache.org) is an open-source distributed streaming platform that can be used to build real-time streaming data pipelines and applications.</span></span> <span data-ttu-id="e6f80-105">Kafka 也提供類似於訊息佇列的訊息代理程式功能，可讓您發佈和訂閱具名資料流。</span><span class="sxs-lookup"><span data-stu-id="e6f80-105">Kafka also provides message broker functionality similar to a message queue, where you can publish and subscribe to named data streams.</span></span> <span data-ttu-id="e6f80-106">在 HDInsight 上的 Kafka 為您在 Microsoft Azure 雲端中提供受管理、高可調整性和高可用性的服務。</span><span class="sxs-lookup"><span data-stu-id="e6f80-106">Kafka on HDInsight provides you with a managed, highly scalable, and highly available service in the Microsoft Azure cloud.</span></span>

## <a name="why-use-kafka-on-hdinsight"></a><span data-ttu-id="e6f80-107">為何使用 HDInsight 上的 Kafka？</span><span class="sxs-lookup"><span data-stu-id="e6f80-107">Why use Kafka on HDInsight?</span></span>

<span data-ttu-id="e6f80-108">Kafka 提供下列功能：</span><span class="sxs-lookup"><span data-stu-id="e6f80-108">Kafka provides the following features:</span></span>

* <span data-ttu-id="e6f80-109">發佈-訂閱傳訊模式︰Kafka 提供生產者 API，可將記錄發佈到 Kafka 主題。</span><span class="sxs-lookup"><span data-stu-id="e6f80-109">Publish-subscribe messaging pattern: Kafka provides a Producer API for publishing records to a Kafka topic.</span></span> <span data-ttu-id="e6f80-110">訂閱主題時會使用取用者 API。</span><span class="sxs-lookup"><span data-stu-id="e6f80-110">The Consumer API is used when subscribing to a topic.</span></span>

* <span data-ttu-id="e6f80-111">串流處理︰Kafka 通常與 Apache Storm 或 Spark 一起用來處理即時串流。</span><span class="sxs-lookup"><span data-stu-id="e6f80-111">Stream processing: Kafka is often used with Apache Storm or Spark for real-time stream processing.</span></span> <span data-ttu-id="e6f80-112">Kafka 0.10.0.0 (HDInsight 3.5 版) 引進串流 API，讓您不需要 Storm 或 Spark 就能建置串流解決方案。</span><span class="sxs-lookup"><span data-stu-id="e6f80-112">Kafka 0.10.0.0 (HDInsight version 3.5) introduced a streaming API that allows you to build streaming solutions without requiring Storm or Spark.</span></span>

* <span data-ttu-id="e6f80-113">水平縮放︰Kafka 可將串流分割給 HDInsight 叢集的各節點。</span><span class="sxs-lookup"><span data-stu-id="e6f80-113">Horizontal scale: Kafka partitions streams across the nodes in the HDInsight cluster.</span></span> <span data-ttu-id="e6f80-114">取用者處理程序可以與個別的資料分割相關聯，在取用記錄時可平衡負載。</span><span class="sxs-lookup"><span data-stu-id="e6f80-114">Consumer processes can be associated with individual partitions to provide load balancing when consuming records.</span></span>

* <span data-ttu-id="e6f80-115">依序傳遞︰在每個資料分割內，記錄會依收到時的順序儲存在串流中。</span><span class="sxs-lookup"><span data-stu-id="e6f80-115">In-order delivery: Within each partition, records are stored in the stream in the order that they were received.</span></span> <span data-ttu-id="e6f80-116">每個資料分割與一個取用者處理序建立關聯之後，就能保證依序處理記錄。</span><span class="sxs-lookup"><span data-stu-id="e6f80-116">By associating one consumer process per partition, you can guarantee that records are processed in-order.</span></span>

* <span data-ttu-id="e6f80-117">容錯︰節點之間可以複寫資料分割，發揮容錯能力。</span><span class="sxs-lookup"><span data-stu-id="e6f80-117">Fault-tolerant: Partitions can be replicated between nodes to provide fault tolerance.</span></span>

* <span data-ttu-id="e6f80-118">與 Azure 受控磁碟整合：受控磁碟可在 HDInsight 叢集中，針對虛擬機器所使用的磁碟提供更高的級別和輸送量。</span><span class="sxs-lookup"><span data-stu-id="e6f80-118">Integration with Azure Managed Disks: Managed disks provides higher scale and throughput for the disks used by the virtual machines in the HDInsight cluster.</span></span>

    <span data-ttu-id="e6f80-119">預設會啟用 HDInsight 上 Kafka 的受控磁碟，且在 HDInsight 建立期間，可以設定每個節點使用的磁碟數目。</span><span class="sxs-lookup"><span data-stu-id="e6f80-119">Managed disks are enabled by default for Kafka on HDInsight, and the number of disks used per node can be configured during HDInsight creation.</span></span> <span data-ttu-id="e6f80-120">如需受控磁碟的詳細資訊，請參閱 [Azure 受控磁碟](../virtual-machines/windows/managed-disks-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="e6f80-120">For more information on managed disks, see [Azure Managed Disks](../virtual-machines/windows/managed-disks-overview.md).</span></span>

    <span data-ttu-id="e6f80-121">如需使用 HDInsight 上的 Kafka 設定受控磁碟的資訊，請參閱[提高 HDInsight 上的 Kafka 延展性](hdinsight-apache-kafka-scalability.md)。</span><span class="sxs-lookup"><span data-stu-id="e6f80-121">For information on configuring managed disks with Kafka on HDInsight, see [Increase scalability of Kafka on HDInsight](hdinsight-apache-kafka-scalability.md).</span></span>

## <a name="use-cases"></a><span data-ttu-id="e6f80-122">使用案例</span><span class="sxs-lookup"><span data-stu-id="e6f80-122">Use cases</span></span>

* <span data-ttu-id="e6f80-123">**傳訊**︰Kafka 支援發佈-訂閱傳訊模式，通常作為訊息代理程式。</span><span class="sxs-lookup"><span data-stu-id="e6f80-123">**Messaging**: Since it supports the publish-subscribe message pattern, Kafka is often used as a message broker.</span></span>

* <span data-ttu-id="e6f80-124">**活動追蹤**︰Kafka 能夠依序登載記錄，可用來追蹤和重新建立活動。</span><span class="sxs-lookup"><span data-stu-id="e6f80-124">**Activity tracking**: Since Kafka provides in-order logging of records, it can be used to track and re-create activities.</span></span> <span data-ttu-id="e6f80-125">例如，網站或應用程式中的使用者動作。</span><span class="sxs-lookup"><span data-stu-id="e6f80-125">For example, user actions on a web site or within an application.</span></span>

* <span data-ttu-id="e6f80-126">**彙總**︰您可以利用串流處理來彙總不同串流的資訊，將資訊結合並集中而成為可操作的資料。</span><span class="sxs-lookup"><span data-stu-id="e6f80-126">**Aggregation**: Using stream processing, you can aggregate information from different streams to combine and centralize the information into operational data.</span></span>

* <span data-ttu-id="e6f80-127">**轉換**︰您可以利用串流處理來結合並充實多個輸入主題的資料，而成為一個或多個輸出主題。</span><span class="sxs-lookup"><span data-stu-id="e6f80-127">**Transformation**: Using stream processing, you can combine and enrich data from multiple input topics into one or more output topics.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e6f80-128">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e6f80-128">Next steps</span></span>

<span data-ttu-id="e6f80-129">使用下列連結以了解如何使用 HDInsight 上的 Apache Kafka：</span><span class="sxs-lookup"><span data-stu-id="e6f80-129">Use the following links to learn how to use Apache Kafka on HDInsight:</span></span>

* [<span data-ttu-id="e6f80-130">開始使用 HDInsight 上的 Kafka</span><span class="sxs-lookup"><span data-stu-id="e6f80-130">Get started with Kafka on HDInsight</span></span>](hdinsight-apache-kafka-get-started.md)

* [<span data-ttu-id="e6f80-131">使用 MirrorMaker 建立 Apache Kafka on HDInsight 複本</span><span class="sxs-lookup"><span data-stu-id="e6f80-131">Use MirrorMaker to create a replica of Kafka on HDInsight</span></span>](hdinsight-apache-kafka-mirroring.md)

* [<span data-ttu-id="e6f80-132">使用 Apache Storm 搭配 HDInsight 上的 Kafka</span><span class="sxs-lookup"><span data-stu-id="e6f80-132">Use Apache Storm with Kafka on HDInsight</span></span>](hdinsight-apache-storm-with-kafka.md)

* [<span data-ttu-id="e6f80-133">使用 Apache Spark 搭配 Kafka on HDInsight</span><span class="sxs-lookup"><span data-stu-id="e6f80-133">Use Apache Spark with Kafka on HDInsight</span></span>](hdinsight-apache-spark-with-kafka.md)

* [<span data-ttu-id="e6f80-134">透過 Azure 虛擬網路連線至 Kafka</span><span class="sxs-lookup"><span data-stu-id="e6f80-134">Connect to Kafka through an Azure Virtual Network</span></span>](hdinsight-apache-kafka-connect-vpn-gateway.md)