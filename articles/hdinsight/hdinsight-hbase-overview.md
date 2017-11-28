---
title: "aaaWhat 會位於 Azure HDInsight HBase 嗎？ | Microsoft Docs"
description: "簡介 tooApache 在 HDInsight HBase，Hadoop 上建置的 NoSQL 資料庫。 了解使用案例，然後比較 HBase tooother Hadoop 叢集。"
keywords: "bigtable,nosql,什麼是 hbase,apache hbase,hbase,habase 概觀,"
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: d2a76d53-133a-4849-a30c-88d9c794391c
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/17/2017
ms.author: jgao
ms.openlocfilehash: 0d28378d07b1a168e38748548578be11310d2228
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-hbase-in-hdinsight-a-nosql-database-that-provides-bigtable-like-capabilities-for-hadoop"></a><span data-ttu-id="df162-106">什麼是 HDInsight 中的 HBase：為 Hadoop 提供類似 BigTable 功能的 NoSQL 資料庫</span><span class="sxs-lookup"><span data-stu-id="df162-106">What is HBase in HDInsight: A NoSQL database that provides BigTable-like capabilities for Hadoop</span></span>
<span data-ttu-id="df162-107">Apache HBase 是開放原始碼的 NoSQL 資料庫，其建置於 Hadoop 上並模仿 Google BigTable。</span><span class="sxs-lookup"><span data-stu-id="df162-107">Apache HBase is an open-source, NoSQL database that is built on Hadoop and modeled after Google BigTable.</span></span> <span data-ttu-id="df162-108">HBase 可針對依資料行系列組織的無結構描述資料庫中的大量非結構化及半結構化資料，提供隨機存取功能和強大一致性。</span><span class="sxs-lookup"><span data-stu-id="df162-108">HBase provides random access and strong consistency for large amounts of unstructured and semistructured data in a schemaless database organized by column families.</span></span>

<span data-ttu-id="df162-109">資料會儲存在 hello 資料表，資料列和資料列中的依資料欄系列。</span><span class="sxs-lookup"><span data-stu-id="df162-109">Data is stored in hello rows of a table, and data within a row is grouped by column family.</span></span> <span data-ttu-id="df162-110">HBase 是 hello 兩者皆非 hello 資料行，也不 hello 類型的資料儲存在它們的意義上 schemaless 資料庫需要 toobe 之前使用這些定義。</span><span class="sxs-lookup"><span data-stu-id="df162-110">HBase is a schemaless database in hello sense that neither hello columns nor hello type of data stored in them need toobe defined before using them.</span></span> <span data-ttu-id="df162-111">hello 開放原始碼縮放數千個節點上以線性方式 toohandle pb 計的資料。</span><span class="sxs-lookup"><span data-stu-id="df162-111">hello open-source code scales linearly toohandle petabytes of data on thousands of nodes.</span></span> <span data-ttu-id="df162-112">它會依賴資料備援、 批次處理和其他功能所提供的 hello Hadoop 生態系統中的分散式應用程式。</span><span class="sxs-lookup"><span data-stu-id="df162-112">It can rely on data redundancy, batch processing, and other features that are provided by distributed applications in hello Hadoop ecosystem.</span></span>

## <a name="how-is-hbase-implemented-in-azure-hdinsight"></a><span data-ttu-id="df162-113">Azure HDInsight 中的 HBase 是如何實作的？</span><span class="sxs-lookup"><span data-stu-id="df162-113">How is HBase implemented in Azure HDInsight?</span></span>
<span data-ttu-id="df162-114">為受管理的叢集整合到 Azure 環境的 hello 提供 HDInsight HBase。</span><span class="sxs-lookup"><span data-stu-id="df162-114">HDInsight HBase is offered as a managed cluster that is integrated into hello Azure environment.</span></span> <span data-ttu-id="df162-115">hello 叢集是直接在設定的 toostore 資料[Azure 儲存體](./hdinsight-hadoop-use-blob-storage.md)或[Azure Data Lake Store](./hdinsight-hadoop-use-data-lake-store.md)，其中提供低延遲、 效能及成本的選項中增加的彈性。</span><span class="sxs-lookup"><span data-stu-id="df162-115">hello clusters are configured toostore data directly in [Azure Storage](./hdinsight-hadoop-use-blob-storage.md) or [Azure Data Lake Store](./hdinsight-hadoop-use-data-lake-store.md), which provides low latency and increased elasticity in performance and cost choices.</span></span> <span data-ttu-id="df162-116">這可讓客戶 toobuild 之互動網站使用大型資料集，儲存感應器和遙測資料包含數百萬個結束點和 tooanalyze toobuild 服務將此資料與 Hadoop 工作。</span><span class="sxs-lookup"><span data-stu-id="df162-116">This enables customers toobuild interactive websites that work with large datasets, toobuild services that store sensor and telemetry data from millions of end points, and tooanalyze this data with Hadoop jobs.</span></span> <span data-ttu-id="df162-117">HBase 和 Hadoop 是很好的起點巨量資料專案中 Azure;尤其，他們可以啟用即時應用程式 toowork 大型資料集。</span><span class="sxs-lookup"><span data-stu-id="df162-117">HBase and Hadoop are good starting points for big data project in Azure; in particular, they can enable real-time applications toowork with large datasets.</span></span>

<span data-ttu-id="df162-118">hello HDInsight 實作會利用 hello 向外延展架構的 HBase tooprovide 自動分區化的資料表，強式一致性的讀取和寫入，以及自動容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="df162-118">hello HDInsight implementation leverages hello scale-out architecture of HBase tooprovide automatic sharding of tables, strong consistency for reads and writes, and automatic failover.</span></span> <span data-ttu-id="df162-119">透過在記憶體內部快取讀取和高輸送量的串流寫入，來提高效能。</span><span class="sxs-lookup"><span data-stu-id="df162-119">Performance is enhanced by in-memory caching for reads and high-throughput streaming for writes.</span></span> <span data-ttu-id="df162-120">可以在虛擬網路內建立 HBase 叢集。</span><span class="sxs-lookup"><span data-stu-id="df162-120">HBase cluster can be created inside virtual network.</span></span> <span data-ttu-id="df162-121">如需詳細資訊，請參閱[在 Azure 虛擬網路上建立 HDInsight 叢集][hbase-provision-vnet]。</span><span class="sxs-lookup"><span data-stu-id="df162-121">For details, see  [Create HDInsight clusters on Azure Virtual Network][hbase-provision-vnet].</span></span>

## <a name="how-is-data-managed-in-hdinsight-hbase"></a><span data-ttu-id="df162-122">如何在 HDInsight HBase 中管理資料？</span><span class="sxs-lookup"><span data-stu-id="df162-122">How is data managed in HDInsight HBase?</span></span>
<span data-ttu-id="df162-123">資料可以使用來管理對 HBase 中 hello `create`， `get`， `put`，和`scan`hello HBase 殼層命令。</span><span class="sxs-lookup"><span data-stu-id="df162-123">Data can be managed in HBase by using hello `create`, `get`, `put`, and `scan` commands from hello HBase shell.</span></span> <span data-ttu-id="df162-124">資料透過使用撰寫 toohello 資料庫`put`和使用讀取`get`。</span><span class="sxs-lookup"><span data-stu-id="df162-124">Data is written toohello database by using `put` and read by using `get`.</span></span> <span data-ttu-id="df162-125">hello`scan`命令是使用的 tooobtain 資料從資料表中的多個資料列。</span><span class="sxs-lookup"><span data-stu-id="df162-125">hello `scan` command is used tooobtain data from multiple rows in a table.</span></span> <span data-ttu-id="df162-126">資料也可以使用 hello HBase C# API，可提供用戶端程式庫之上 hello HBase REST API 來管理。</span><span class="sxs-lookup"><span data-stu-id="df162-126">Data can also be managed using hello HBase C# API, which provides a client library on top of hello HBase REST API.</span></span> <span data-ttu-id="df162-127">HBase 資料庫也可使用 Hive 進行查詢。</span><span class="sxs-lookup"><span data-stu-id="df162-127">An HBase database can also be queried by using Hive.</span></span> <span data-ttu-id="df162-128">如簡介 toothese，程式設計模型，請參閱[開始透過 HDInsight 中的 Hadoop 使用 HBase][hbase-get-started]。</span><span class="sxs-lookup"><span data-stu-id="df162-128">For an introduction toothese programming models, see [Get started using HBase with Hadoop in HDInsight][hbase-get-started].</span></span> <span data-ttu-id="df162-129">副處理器也會提供，可讓該主機 hello 資料庫 hello 節點中的資料處理。</span><span class="sxs-lookup"><span data-stu-id="df162-129">Co-processors are also available, which allow data processing in hello nodes that host hello database.</span></span>

> [!NOTE]
> <span data-ttu-id="df162-130">Thrift 不受 HDInsight 中的 HBase 所支援。</span><span class="sxs-lookup"><span data-stu-id="df162-130">Thrift is not supported by HBase in HDInsight.</span></span>
>

## <a name="scenarios-use-cases-for-hbase"></a><span data-ttu-id="df162-131">情節：HBase 的使用案例</span><span class="sxs-lookup"><span data-stu-id="df162-131">Scenarios: Use cases for HBase</span></span>
<span data-ttu-id="df162-132">hello 標準的使用案例的 BigTable （以及藉由擴充，HBase） 所建立的 web 搜尋。</span><span class="sxs-lookup"><span data-stu-id="df162-132">hello canonical use case for which BigTable (and by extension, HBase) was created was web search.</span></span> <span data-ttu-id="df162-133">搜尋引擎會建立對應詞彙 toohello 網頁包含它們的索引。</span><span class="sxs-lookup"><span data-stu-id="df162-133">Search engines build indexes that map terms toohello web pages that contain them.</span></span> <span data-ttu-id="df162-134">除此之外，HBase 還有其他許多適用的使用案例，本節會列舉其中幾個。</span><span class="sxs-lookup"><span data-stu-id="df162-134">But there are many other use cases that HBase is suitable for—several of which are itemized in this section.</span></span>

* <span data-ttu-id="df162-135">索引鍵-值存放區</span><span class="sxs-lookup"><span data-stu-id="df162-135">Key-value store</span></span>
  
    <span data-ttu-id="df162-136">HBase 可做為索引鍵-值存放區，也很適合用來管理訊息系統。</span><span class="sxs-lookup"><span data-stu-id="df162-136">HBase can be used as a key-value store, and it is suitable for managing message systems.</span></span> <span data-ttu-id="df162-137">Facebook 在訊息系統中使用 HBase，其用來儲存和管理網際網路通訊相當理想。</span><span class="sxs-lookup"><span data-stu-id="df162-137">Facebook uses HBase for their messaging system, and it is ideal for storing and managing Internet communications.</span></span> <span data-ttu-id="df162-138">WebTable 使用 HBase toosearch 的並管理從網頁擷取的資料表。</span><span class="sxs-lookup"><span data-stu-id="df162-138">WebTable uses HBase toosearch for and manage tables that are extracted from webpages.</span></span>
* <span data-ttu-id="df162-139">感應器資料</span><span class="sxs-lookup"><span data-stu-id="df162-139">Sensor data</span></span>
  
    <span data-ttu-id="df162-140">HBase 適合用來擷取從多個來源收集累加的資料。</span><span class="sxs-lookup"><span data-stu-id="df162-140">HBase is useful for capturing data that is collected incrementally from various sources.</span></span> <span data-ttu-id="df162-141">這包括社交分析、時間序列、讓互動式儀表板保有最新的趨勢與計數器，以及管理稽核記錄系統。</span><span class="sxs-lookup"><span data-stu-id="df162-141">This includes social analytics, time series, keeping interactive dashboards up-to-date with trends and counters, and managing audit log systems.</span></span> <span data-ttu-id="df162-142">範例包括 Bloomberg 商人終端機和 hello 開啟時間序列的資料庫 (OpenTSDB)，它會儲存，並提供存取 toometrics 收集關於 hello 伺服器系統的健全狀況。</span><span class="sxs-lookup"><span data-stu-id="df162-142">Examples include Bloomberg trader terminal and hello Open Time Series Database (OpenTSDB), which stores and provides access toometrics collected about hello health of server systems.</span></span>
* <span data-ttu-id="df162-143">即時查詢</span><span class="sxs-lookup"><span data-stu-id="df162-143">Real-time query</span></span>
  
    <span data-ttu-id="df162-144">[Phoenix](http://phoenix.apache.org/) 是適用於 Apache HBase 的 SQL 查詢引擎。</span><span class="sxs-lookup"><span data-stu-id="df162-144">[Phoenix](http://phoenix.apache.org/) is a SQL query engine for Apache HBase.</span></span> <span data-ttu-id="df162-145">其以 JDBC 驅動程式的形式進行存取，並可使用 SQL 查詢和管理 HBase 資料表。</span><span class="sxs-lookup"><span data-stu-id="df162-145">It is accessed as a JDBC driver, and it enables querying and managing HBase tables by using SQL.</span></span>
* <span data-ttu-id="df162-146">HBase 即平台</span><span class="sxs-lookup"><span data-stu-id="df162-146">HBase as a platform</span></span>
  
    <span data-ttu-id="df162-147">應用程式可以將 HBase 做為資料存放區，並在此基礎上執行。</span><span class="sxs-lookup"><span data-stu-id="df162-147">Applications can run on top of HBase by using it as a datastore.</span></span> <span data-ttu-id="df162-148">範例包括 Phoenix、OpenTSDB、Kiji 及 Titan。</span><span class="sxs-lookup"><span data-stu-id="df162-148">Examples include Phoenix, OpenTSDB, Kiji, and Titan.</span></span> <span data-ttu-id="df162-149">應用程式也可與 HBase 整合。</span><span class="sxs-lookup"><span data-stu-id="df162-149">Applications can also integrate with HBase.</span></span> <span data-ttu-id="df162-150">範例包括 Hive、Pig、Solr、Storm、Flume、Impala、Spark、Ganglia 及 Drill。</span><span class="sxs-lookup"><span data-stu-id="df162-150">Examples include Hive, Pig, Solr, Storm, Flume, Impala, Spark, Ganglia, and Drill.</span></span>

## <span data-ttu-id="df162-151"><a name="next-steps"></a>接續步驟</span><span class="sxs-lookup"><span data-stu-id="df162-151"><a name="next-steps"></a>Next steps</span></span>
* <span data-ttu-id="df162-152">[開始在 HDInsight 中搭配使用 HBase 與 Hadoop][hbase-get-started]</span><span class="sxs-lookup"><span data-stu-id="df162-152">[Get started using HBase with Hadoop in HDInsight][hbase-get-started]</span></span>
* <span data-ttu-id="df162-153">[在 Azure 虛擬網路上建立 HDInsight 叢集][hbase-provision-vnet]</span><span class="sxs-lookup"><span data-stu-id="df162-153">[Create HDInsight clusters on Azure Virtual Network][hbase-provision-vnet]</span></span>
* [<span data-ttu-id="df162-154">在 HDInsight 中設定 HBase 複寫</span><span class="sxs-lookup"><span data-stu-id="df162-154">Configure HBase replication in HDInsight</span></span>](hdinsight-hbase-replication.md)
* <span data-ttu-id="df162-155">[使用 HDInsight 中的 HBase 分析 Twitter 情緒][hbase-twitter-sentiment]</span><span class="sxs-lookup"><span data-stu-id="df162-155">[Analyze Twitter sentiment with HBase in HDInsight][hbase-twitter-sentiment]</span></span>
* <span data-ttu-id="df162-156">[使用 Maven toobuild Java 應用程式與 HDInsight (Hadoop) 使用 HBase][hbase-build-java-maven]</span><span class="sxs-lookup"><span data-stu-id="df162-156">[Use Maven toobuild Java applications that use HBase with HDInsight (Hadoop)][hbase-build-java-maven]</span></span>

## <span data-ttu-id="df162-157"><a name="see-also"></a>另請參閱</span><span class="sxs-lookup"><span data-stu-id="df162-157"><a name="see-also"></a>See also</span></span>
* [<span data-ttu-id="df162-158">Apache HBase</span><span class="sxs-lookup"><span data-stu-id="df162-158">Apache HBase</span></span>](https://hbase.apache.org/)
* [<span data-ttu-id="df162-159">Bigtable：結構化資料的分散式儲存體系統</span><span class="sxs-lookup"><span data-stu-id="df162-159">Bigtable: A Distributed Storage System for Structured Data</span></span>](http://research.google.com/archive/bigtable.html)

[hbase-provision-vnet]: hdinsight-hbase-provision-vnet.md

[hbase-twitter-sentiment]: hdinsight-hbase-analyze-twitter-sentiment.md

[hbase-build-java-maven]: hdinsight-hbase-build-java-maven.md

[hdinsight-use-hive]: hdinsight-use-hive.md

[hdinsight-storage]: ../hdinsight-hadoop-use-blob-storage.md

[hbase-get-started]: http://azure.microsoft.com/documentation/articles/hdinsight-hbase-get-started/

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[azure-management-portal]: https://portal.azure.com/
[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md

[apache-hadoop]: http://hadoop.apache.org/
