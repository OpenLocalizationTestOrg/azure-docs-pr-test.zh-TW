---
title: "aaaWhat 是 Apache Storm 的 Azure HDInsight |Microsoft 文件"
description: "Apache Storm 可讓您的即時資料 tooprocess 資料流。 Azure HDInsight 可讓您 tooeasily hello Azure 雲端上建立 Storm 叢集。 與 Visual Studio 中，您可以建立使用 C# 的 Storm 方案，然後再部署的 tooyour HDInsight Storm 叢集。"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
keywords: "apache storm 使用案例,storm 叢集,什麼是 apache storm"
ms.assetid: 72d54080-1e48-4a5e-aa50-cce4ffc85077
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/03/2017
ms.author: larryfr
ms.openlocfilehash: 6c6b2925ef3e5666dfecc3fb3c835bb362902c51
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-apache-storm-on-azure-hdinsight"></a><span data-ttu-id="76a13-106">什麼是 Apache Storm on Azure HDInsight？</span><span class="sxs-lookup"><span data-stu-id="76a13-106">What is Apache Storm on Azure HDInsight?</span></span>

<span data-ttu-id="76a13-107">[Apache Storm](http://storm.apache.org/) 是一個容錯的分散式開放原始碼計算系統。</span><span class="sxs-lookup"><span data-stu-id="76a13-107">[Apache Storm](http://storm.apache.org/) is a distributed, fault-tolerant, open-source computation system.</span></span> <span data-ttu-id="76a13-108">您可以使用 Storm tooprocess 資料流的即時的 Hadoop。</span><span class="sxs-lookup"><span data-stu-id="76a13-108">You can use Storm tooprocess streams of data in real time with Hadoop.</span></span> <span data-ttu-id="76a13-109">Storm 解決方案也可以提供保證的資料處理，與 hello 能力 tooreplay 未成功的資料處理 hello 第一次。</span><span class="sxs-lookup"><span data-stu-id="76a13-109">Storm solutions can also provide guaranteed processing of data, with hello ability tooreplay data that was not successfully processed hello first time.</span></span>

<span data-ttu-id="76a13-110">出現在 HDInsight 上的提供下列主要優點 hello:</span><span class="sxs-lookup"><span data-stu-id="76a13-110">Storm on HDInsight provides hello following key benefits:</span></span>

* <span data-ttu-id="76a13-111">可作為受管理服務執行，且具有 99.9% 運作時間的 SLA。</span><span class="sxs-lookup"><span data-stu-id="76a13-111">Performs as a managed service with an SLA of 99.9 percent uptime.</span></span>

* <span data-ttu-id="76a13-112">在建立期間或之後針對 Storm 叢集執行指令碼，可支援輕鬆自訂。</span><span class="sxs-lookup"><span data-stu-id="76a13-112">Supports easy customization by running scripts against a Storm cluster during or after creation.</span></span> <span data-ttu-id="76a13-113">如需詳細資訊，請參閱[使用指令碼動作來自訂 HDInsight 叢集](hdinsight-hadoop-customize-cluster-linux.md)。</span><span class="sxs-lookup"><span data-stu-id="76a13-113">For more information, see [Customize HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

* <span data-ttu-id="76a13-114">使用各種不同的語言。</span><span class="sxs-lookup"><span data-stu-id="76a13-114">Uses various languages.</span></span> <span data-ttu-id="76a13-115">在您的選擇，例如 Java、 C# 和 Python 的 hello 語言中，您可以撰寫 Storm 元件。</span><span class="sxs-lookup"><span data-stu-id="76a13-115">You can write Storm components in hello language of your choice, such as Java, C#, and Python.</span></span>

    * <span data-ttu-id="76a13-116">與 HDInsight 的 Visual Studio 整合的 hello 開發、 管理及監視的 C# 拓撲中。</span><span class="sxs-lookup"><span data-stu-id="76a13-116">Integrates Visual Studio with HDInsight for hello development, management, and monitoring of C# topologies.</span></span> <span data-ttu-id="76a13-117">如需詳細資訊，請參閱[以 hello HDInsight Tools for Visual Studio C# 開發 Storm 拓撲](hdinsight-storm-develop-csharp-visual-studio-topology.md)。</span><span class="sxs-lookup"><span data-stu-id="76a13-117">For more information, see [Develop C# Storm topologies with hello HDInsight Tools for Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span></span>

    * <span data-ttu-id="76a13-118">支援 hello 戟 Java 介面。</span><span class="sxs-lookup"><span data-stu-id="76a13-118">Supports hello Trident Java interface.</span></span> <span data-ttu-id="76a13-119">您可以建立 Storm 拓撲，以支援一次性處理訊息、交易式資料存放區持續性和一組常用的串流分析作業。</span><span class="sxs-lookup"><span data-stu-id="76a13-119">You can create Storm topologies that support exactly once processing of messages, transactional datastore persistence, and a set of common stream analytics operations.</span></span>

*  <span data-ttu-id="76a13-120">輕鬆地相應增加和相應減少 Storm 叢集。</span><span class="sxs-lookup"><span data-stu-id="76a13-120">Easily scale Storm clusters up and down.</span></span> <span data-ttu-id="76a13-121">您可以新增或移除背景工作節點沒有影響 toorunning Storm 拓撲。</span><span class="sxs-lookup"><span data-stu-id="76a13-121">You can add or remove worker nodes with no impact toorunning Storm topologies.</span></span>

* <span data-ttu-id="76a13-122">會與下列 Azure 服務的 hello 整合：</span><span class="sxs-lookup"><span data-stu-id="76a13-122">Integrates with hello following Azure services:</span></span>

    * <span data-ttu-id="76a13-123">Azure 事件中心</span><span class="sxs-lookup"><span data-stu-id="76a13-123">Azure Event Hubs</span></span>

    * <span data-ttu-id="76a13-124">Azure 虛擬網路</span><span class="sxs-lookup"><span data-stu-id="76a13-124">Azure Virtual Network</span></span>

    * <span data-ttu-id="76a13-125">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="76a13-125">Azure SQL Database</span></span>

    * <span data-ttu-id="76a13-126">Azure 儲存體</span><span class="sxs-lookup"><span data-stu-id="76a13-126">Azure Storage</span></span>

    * <span data-ttu-id="76a13-127">Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="76a13-127">Azure Cosmos DB</span></span>

* <span data-ttu-id="76a13-128">安全地將多個 HDInsight 叢集的 hello 功能結合使用虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="76a13-128">Securely combines hello capabilities of multiple HDInsight clusters by using Virtual Network.</span></span> <span data-ttu-id="76a13-129">您可以建立使用 Storm、Kafka、HBase 或 Hadoop 叢集的分析管線。</span><span class="sxs-lookup"><span data-stu-id="76a13-129">You can create analytic pipelines that use Storm, Kafka, Spark, HBase, or Hadoop clusters.</span></span>

<span data-ttu-id="76a13-130">如需使用 Apache Storm 作為即時分析解決方案的公司清單，請參閱[使用 Apache Storm 的公司](https://storm.apache.org/documentation/Powered-By.html)。</span><span class="sxs-lookup"><span data-stu-id="76a13-130">For a list of companies that are using Apache Storm for their real-time analytics solutions, see [Companies using Apache Storm](https://storm.apache.org/documentation/Powered-By.html).</span></span>

<span data-ttu-id="76a13-131">tooget 啟動使用 Storm，請參閱[開始使用 HDInsight 上的 Storm][gettingstarted]。</span><span class="sxs-lookup"><span data-stu-id="76a13-131">tooget started using Storm, see [Get started with Storm on HDInsight][gettingstarted].</span></span>

## <a name="how-does-storm-work"></a><span data-ttu-id="76a13-132">Storm 的運作方式</span><span class="sxs-lookup"><span data-stu-id="76a13-132">How does Storm work</span></span>

<span data-ttu-id="76a13-133">Storm 執行而不是 hello 拓撲可能已經熟悉的 MapReduce 工作。</span><span class="sxs-lookup"><span data-stu-id="76a13-133">Storm runs topologies instead of hello MapReduce jobs that you might be familiar with.</span></span> <span data-ttu-id="76a13-134">Storm 拓撲是由有向非循環圖 (DAG) 中排列的多個元件所組成。</span><span class="sxs-lookup"><span data-stu-id="76a13-134">Storm topologies are composed of multiple components that are arranged in a directed acyclic graph (DAG).</span></span> <span data-ttu-id="76a13-135">Hello 圖形中的 hello 元件之間流動的資料。</span><span class="sxs-lookup"><span data-stu-id="76a13-135">Data flows between hello components in hello graph.</span></span> <span data-ttu-id="76a13-136">每個元件會取用一或多個資料流，並可選擇性地發出一或多個資料流。</span><span class="sxs-lookup"><span data-stu-id="76a13-136">Each component consumes one or more data streams, and can optionally emit one or more streams.</span></span> <span data-ttu-id="76a13-137">hello 下列圖表說明基本的字數統計拓撲中的元件之間資料流動的方式：</span><span class="sxs-lookup"><span data-stu-id="76a13-137">hello following diagram illustrates how data flows between components in a basic word-count topology:</span></span>

![Storm 拓撲中元件排列方式的範例](./media/hdinsight-storm-overview/example-apache-storm-topology-diagram.png)

* <span data-ttu-id="76a13-139">Spout 元件可將資料帶入拓撲中。</span><span class="sxs-lookup"><span data-stu-id="76a13-139">Spout components bring data into a topology.</span></span> <span data-ttu-id="76a13-140">它們會發出一或多個資料流到 hello 拓撲。</span><span class="sxs-lookup"><span data-stu-id="76a13-140">They emit one or more streams into hello topology.</span></span>

* <span data-ttu-id="76a13-141">Bolt 元件會取用 Spout 或其他 Bolt 所發出的串流。</span><span class="sxs-lookup"><span data-stu-id="76a13-141">Bolt components consume streams emitted from spouts or other bolts.</span></span> <span data-ttu-id="76a13-142">發射到 hello 拓撲，可能會選擇性地發出資料流。</span><span class="sxs-lookup"><span data-stu-id="76a13-142">Bolts might optionally emit streams into hello topology.</span></span> <span data-ttu-id="76a13-143">發射也會負責撰寫資料 tooexternal 服務或儲存體，例如 HDFS、 Kafka 或 HBase。</span><span class="sxs-lookup"><span data-stu-id="76a13-143">Bolts are also responsible for writing data tooexternal services or storage, such as HDFS, Kafka, or HBase.</span></span>

## <a name="ease-of-creation"></a><span data-ttu-id="76a13-144">容易建立</span><span class="sxs-lookup"><span data-stu-id="76a13-144">Ease of creation</span></span>

<span data-ttu-id="76a13-145">只要花數分鐘即可在 HDInsight 上佈建新的 Storm 叢集。</span><span class="sxs-lookup"><span data-stu-id="76a13-145">You can provision a new Storm cluster on HDInsight in minutes.</span></span> <span data-ttu-id="76a13-146">如需建立 Storm 叢集的相關資訊，請參閱[開始使用 Storm on HDInsight](hdinsight-apache-storm-tutorial-get-started-linux.md)。</span><span class="sxs-lookup"><span data-stu-id="76a13-146">For more information on creating a Storm cluster, see [Get started with Storm on HDInsight](hdinsight-apache-storm-tutorial-get-started-linux.md).</span></span>

## <a name="ease-of-use"></a><span data-ttu-id="76a13-147">容易使用</span><span class="sxs-lookup"><span data-stu-id="76a13-147">Ease of use</span></span>

* <span data-ttu-id="76a13-148">__安全殼層 (SSH) 連線__： 您也可以使用 SSH hello 網際網路上存取 hello Storm 叢集前端節點。</span><span class="sxs-lookup"><span data-stu-id="76a13-148">__Secure Shell (SSH) connectivity__: You can access hello head nodes of your Storm cluster over hello Internet by using SSH.</span></span> <span data-ttu-id="76a13-149">您可以使用 SSH，直接在叢集上執行命令。</span><span class="sxs-lookup"><span data-stu-id="76a13-149">You can run commands directly on your cluster by using SSH.</span></span>

  <span data-ttu-id="76a13-150">如需詳細資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。</span><span class="sxs-lookup"><span data-stu-id="76a13-150">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

* <span data-ttu-id="76a13-151">__Web 連線__： 所有的 HDInsight 叢集提供 hello Ambari web UI。</span><span class="sxs-lookup"><span data-stu-id="76a13-151">__Web connectivity__: All HDInsight clusters provide hello Ambari web UI.</span></span> <span data-ttu-id="76a13-152">您可以輕鬆地監視、 設定及管理服務在叢集上使用 hello Ambari web UI。</span><span class="sxs-lookup"><span data-stu-id="76a13-152">You can easily monitor, configure, and manage services on your cluster by using hello Ambari web UI.</span></span> <span data-ttu-id="76a13-153">Storm 叢集也提供 hello Storm UI。</span><span class="sxs-lookup"><span data-stu-id="76a13-153">Storm clusters also provide hello Storm UI.</span></span> <span data-ttu-id="76a13-154">您可以監視使用和管理執行 Storm 拓撲從瀏覽器 hello Storm UI。</span><span class="sxs-lookup"><span data-stu-id="76a13-154">You can monitor and manage running Storm topologies from your browser by using hello Storm UI.</span></span>

  <span data-ttu-id="76a13-155">如需詳細資訊，請參閱 hello[管理 HDInsight 使用 hello Ambari Web UI](hdinsight-hadoop-manage-ambari.md)和[監視和管理使用 hello Storm UI](hdinsight-storm-deploy-monitor-topology-linux.md#monitor-and-manage-storm-ui)文件。</span><span class="sxs-lookup"><span data-stu-id="76a13-155">For more information, see hello [Manage HDInsight using hello Ambari Web UI](hdinsight-hadoop-manage-ambari.md) and [Monitor and manage using hello Storm UI](hdinsight-storm-deploy-monitor-topology-linux.md#monitor-and-manage-storm-ui) documents.</span></span>

* <span data-ttu-id="76a13-156">__Azure PowerShell 和 Azure CLI__: PowerShell 和 CLI 這兩者都提供可讓您從您使用 HDInsight 和其他 Azure 服務的用戶端系統 toowork 命令列公用程式。</span><span class="sxs-lookup"><span data-stu-id="76a13-156">__Azure PowerShell and Azure CLI__: PowerShell and CLI both provide command-line utilities that you can use from your client system toowork with HDInsight and other Azure services.</span></span>

* <span data-ttu-id="76a13-157">__Visual Studio 整合__: Azure 資料湖 Tools for Visual Studio 包括專案範本建立 C# Storm 拓撲使用 hello SCP.Net 架構。</span><span class="sxs-lookup"><span data-stu-id="76a13-157">__Visual Studio integration__: Azure Data Lake Tools for Visual Studio include project templates for creating C# Storm topologies by using hello SCP.Net framework.</span></span> <span data-ttu-id="76a13-158">資料湖工具也提供工具 toodeploy 監視和管理 HDInsight 上出現的解決方案。</span><span class="sxs-lookup"><span data-stu-id="76a13-158">Data Lake Tools also provide tools toodeploy, monitor, and manage solutions with Storm on HDInsight.</span></span>

  <span data-ttu-id="76a13-159">如需詳細資訊，請參閱[以 hello HDInsight Tools for Visual Studio C# 開發 Storm 拓撲](hdinsight-storm-develop-csharp-visual-studio-topology.md)。</span><span class="sxs-lookup"><span data-stu-id="76a13-159">For more information, see [Develop C# Storm topologies with hello HDInsight Tools for Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span></span>

## <a name="integration-with-other-azure-services"></a><span data-ttu-id="76a13-160">與其他 Azure 服務整合</span><span class="sxs-lookup"><span data-stu-id="76a13-160">Integration with other Azure services</span></span>

* <span data-ttu-id="76a13-161">__Azure Data Lake Store__：如需使用 Data Lake Store 搭配 Storm 叢集的範例，請參閱[使用 Azure Data Lake Store 搭配 Apache Storm on HDInsight](hdinsight-storm-write-data-lake-store.md)。</span><span class="sxs-lookup"><span data-stu-id="76a13-161">__Azure Data Lake Store__: For an example of using Data Lake Store with a Storm cluster, see [Use Azure Data Lake Store with Apache Storm on HDInsight](hdinsight-storm-write-data-lake-store.md).</span></span>

* <span data-ttu-id="76a13-162">__事件中心__: Storm 叢集與使用事件中心的範例，請參閱下列文件的 hello:</span><span class="sxs-lookup"><span data-stu-id="76a13-162">__Event Hubs__: For an example of using Event Hubs with a Storm cluster, see hello following documents:</span></span>

    * [<span data-ttu-id="76a13-163">開發 Storm on HDInsight 的 Java 型拓撲</span><span class="sxs-lookup"><span data-stu-id="76a13-163">Develop a Java-based topology for Storm on HDInsight</span></span>](hdinsight-storm-develop-java-topology.md)

    * [<span data-ttu-id="76a13-164">利用 Storm on HDInsight 處理 Azure 事件中樞的事件 (C#)</span><span class="sxs-lookup"><span data-stu-id="76a13-164">Process events from Azure Event Hubs with Storm on HDInsight (C#)</span></span>](hdinsight-storm-develop-csharp-event-hub-topology.md)

* <span data-ttu-id="76a13-165">__SQL Database__， __Cosmos DB__，__事件中心__，和__HBase__： 範本範例隨附 hello Data Lake Tools for Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="76a13-165">__SQL Database__, __Cosmos DB__, __Event Hubs__, and __HBase__: Template examples are included in hello Data Lake Tools for Visual Studio.</span></span> <span data-ttu-id="76a13-166">如需詳細資訊，請參閱[開發 Storm on HDInsight 的 C# 拓撲](hdinsight-storm-develop-csharp-visual-studio-topology.md)。</span><span class="sxs-lookup"><span data-stu-id="76a13-166">For more information, see [Develop a C# topology for Storm on HDInsight](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span></span>

## <a name="reliability"></a><span data-ttu-id="76a13-167">可靠性</span><span class="sxs-lookup"><span data-stu-id="76a13-167">Reliability</span></span>

<span data-ttu-id="76a13-168">Apache Storm 可保證，每個連入訊息一律會完整處理時，即使 hello 資料分析遍佈數百個節點。</span><span class="sxs-lookup"><span data-stu-id="76a13-168">Apache Storm guarantees that each incoming message is always fully processed, even when hello data analysis is spread over hundreds of nodes.</span></span>

<span data-ttu-id="76a13-169">hello Nimbus 節點提供的功能類似 toohello Hadoop JobTracker，並指派工作 tooother 動物園管理員透過叢集中的節點。</span><span class="sxs-lookup"><span data-stu-id="76a13-169">hello Nimbus node provides functionality similar toohello Hadoop JobTracker, and it assigns tasks tooother nodes in a cluster through Zookeeper.</span></span> <span data-ttu-id="76a13-170">動物園管理員節點提供協調叢集，並促進 Nimbus 與 hello 監督員 hello 背景工作節點上的處理序之間的通訊。</span><span class="sxs-lookup"><span data-stu-id="76a13-170">Zookeeper nodes provide coordination for a cluster and facilitate communication between Nimbus and hello Supervisor process on hello worker nodes.</span></span> <span data-ttu-id="76a13-171">如果某個處理節點關閉時，通知 hello Nimbus 節點，並 hello 工作與相關聯的資料 tooanother 節點，會將它指派。</span><span class="sxs-lookup"><span data-stu-id="76a13-171">If one processing node goes down, hello Nimbus node is informed, and it assigns hello task and associated data tooanother node.</span></span>

<span data-ttu-id="76a13-172">hello Apache Storm 叢集的預設設定是 toohave 只有一個 Nimbus 節點。</span><span class="sxs-lookup"><span data-stu-id="76a13-172">hello default configuration for Apache Storm clusters is toohave only one Nimbus node.</span></span> <span data-ttu-id="76a13-173">Storm on HDInsight 會提供兩個 Nimbus 節點。</span><span class="sxs-lookup"><span data-stu-id="76a13-173">Storm on HDInsight provides two Nimbus nodes.</span></span> <span data-ttu-id="76a13-174">如果 hello 主要節點失敗，hello Storm 叢集 hello 主要節點恢復時，就會切換 toohello 次要節點。</span><span class="sxs-lookup"><span data-stu-id="76a13-174">If hello primary node fails, hello Storm cluster switches toohello secondary node while hello primary node is recovered.</span></span> <span data-ttu-id="76a13-175">hello 下列圖表說明 Storm HDInsight 上的 hello 工作流程組態：</span><span class="sxs-lookup"><span data-stu-id="76a13-175">hello following diagram illustrates hello task flow configuration for Storm on HDInsight:</span></span>

![Nimbus、Zookeeper 和監督員的圖表](./media/hdinsight-storm-overview/nimbus.png)

## <a name="scale"></a><span data-ttu-id="76a13-177">調整</span><span class="sxs-lookup"><span data-stu-id="76a13-177">Scale</span></span>

<span data-ttu-id="76a13-178">新增或移除背景工作節點即可動態調整 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="76a13-178">HDInsight clusters can be dynamically scaled by adding or removing worker nodes.</span></span> <span data-ttu-id="76a13-179">在處理資料時，可以執行這項作業。</span><span class="sxs-lookup"><span data-stu-id="76a13-179">This operation can be performed while processing data.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="76a13-180">tootake 利用新的節點會透過調整，加入需要 toorebalance Storm 拓撲啟動之前已增加 hello 叢集大小。</span><span class="sxs-lookup"><span data-stu-id="76a13-180">tootake advantage of new nodes added through scaling, you need toorebalance Storm topologies started before hello cluster size was increased.</span></span>

## <a name="support"></a><span data-ttu-id="76a13-181">支援</span><span class="sxs-lookup"><span data-stu-id="76a13-181">Support</span></span>

<span data-ttu-id="76a13-182">Storm on HDInsight 隨附完整的企業級連續支援。</span><span class="sxs-lookup"><span data-stu-id="76a13-182">Storm on HDInsight comes with full enterprise-level continuous support.</span></span> <span data-ttu-id="76a13-183">Storm on HDInsight 也有 99.9% 的 SLA。</span><span class="sxs-lookup"><span data-stu-id="76a13-183">Storm on HDInsight also has an SLA of 99.9 percent.</span></span> <span data-ttu-id="76a13-184">這表示我們保證 Storm 叢集具備外部連線能力的 hello 時間至少 99.9%。</span><span class="sxs-lookup"><span data-stu-id="76a13-184">That means we guarantee that a Storm cluster has external connectivity at least 99.9 percent of hello time.</span></span>

<span data-ttu-id="76a13-185">如需詳細資訊，請參閱 [Azure 文章](https://azure.microsoft.com/support/options/)。</span><span class="sxs-lookup"><span data-stu-id="76a13-185">For more information, see [Azure support](https://azure.microsoft.com/support/options/).</span></span>

## <a name="apache-storm-use-cases"></a><span data-ttu-id="76a13-186">Apache Storm 使用案例</span><span class="sxs-lookup"><span data-stu-id="76a13-186">Apache Storm use cases</span></span>

<span data-ttu-id="76a13-187">hello 以下是一些常見的案例，您可能會使用出現在 HDInsight:</span><span class="sxs-lookup"><span data-stu-id="76a13-187">hello following are some common scenarios for which you might use Storm on HDInsight:</span></span>

* <span data-ttu-id="76a13-188">物聯網 (IoT)</span><span class="sxs-lookup"><span data-stu-id="76a13-188">Internet of Things (IoT)</span></span>
* <span data-ttu-id="76a13-189">詐騙偵測</span><span class="sxs-lookup"><span data-stu-id="76a13-189">Fraud detection</span></span>
* <span data-ttu-id="76a13-190">社交分析</span><span class="sxs-lookup"><span data-stu-id="76a13-190">Social analytics</span></span>
* <span data-ttu-id="76a13-191">擷取、轉換和載入 (ETL)</span><span class="sxs-lookup"><span data-stu-id="76a13-191">Extraction, transformation, and loading (ETL)</span></span>
* <span data-ttu-id="76a13-192">網路監視</span><span class="sxs-lookup"><span data-stu-id="76a13-192">Network monitoring</span></span>
* <span data-ttu-id="76a13-193">搜尋</span><span class="sxs-lookup"><span data-stu-id="76a13-193">Search</span></span>
* <span data-ttu-id="76a13-194">Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="76a13-194">Mobile engagement</span></span>

<span data-ttu-id="76a13-195">真實世界案例的相關資訊，請參閱 hello[公司如何使用 Storm](https://storm.apache.org/documentation/Powered-By.html)文件。</span><span class="sxs-lookup"><span data-stu-id="76a13-195">For information about real-world scenarios, see hello [How companies are using Storm](https://storm.apache.org/documentation/Powered-By.html) document.</span></span>

## <a name="development"></a><span data-ttu-id="76a13-196">開發</span><span class="sxs-lookup"><span data-stu-id="76a13-196">Development</span></span>

<span data-ttu-id="76a13-197">.NET 開發人員可以使用 Data Lake Tools for Visual Studio，以 C# 語言設計和實作拓撲。</span><span class="sxs-lookup"><span data-stu-id="76a13-197">.NET developers can design and implement topologies in C# by using Data Lake Tools for Visual Studio.</span></span> <span data-ttu-id="76a13-198">您也可以建立使用 Java 和 C# 元件的混合式拓撲。</span><span class="sxs-lookup"><span data-stu-id="76a13-198">You can also create hybrid topologies that use Java and C# components.</span></span>

<span data-ttu-id="76a13-199">如需詳細資訊，請參閱 [使用 Visual Studio 開發 Storm on HDInsight 的 C# 拓撲](hdinsight-storm-develop-csharp-visual-studio-topology.md)。</span><span class="sxs-lookup"><span data-stu-id="76a13-199">For more information, see [Develop C# topologies for Storm on HDInsight using Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span></span>

<span data-ttu-id="76a13-200">您也可以使用您選擇的 IDE hello 開發 Java 方案。</span><span class="sxs-lookup"><span data-stu-id="76a13-200">You can also develop Java solutions by using hello IDE of your choice.</span></span> <span data-ttu-id="76a13-201">如需詳細資訊，請參閱[開發 Storm on HDInsight 的 Java 拓撲](hdinsight-storm-develop-java-topology.md)。</span><span class="sxs-lookup"><span data-stu-id="76a13-201">For more information, see [Develop Java topologies for Storm on HDInsight](hdinsight-storm-develop-java-topology.md).</span></span>

<span data-ttu-id="76a13-202">Python 也可以使用的 toodevelop Storm 元件。</span><span class="sxs-lookup"><span data-stu-id="76a13-202">Python can also be used toodevelop Storm components.</span></span> <span data-ttu-id="76a13-203">如需詳細資訊，請參閱[使用 Python on HDInsight 開發 Storm 拓撲](hdinsight-storm-develop-python-topology.md)。</span><span class="sxs-lookup"><span data-stu-id="76a13-203">For more information, see [Develop Storm topologies using Python on HDInsight](hdinsight-storm-develop-python-topology.md).</span></span>

## <a name="common-development-patterns"></a><span data-ttu-id="76a13-204">常見的開發模式</span><span class="sxs-lookup"><span data-stu-id="76a13-204">Common development patterns</span></span>

### <a name="guaranteed-message-processing"></a><span data-ttu-id="76a13-205">保證處理訊息</span><span class="sxs-lookup"><span data-stu-id="76a13-205">Guaranteed message processing</span></span>

<span data-ttu-id="76a13-206">Apache Storm 可以提供不同程度的訊息處理保證。</span><span class="sxs-lookup"><span data-stu-id="76a13-206">Apache Storm can provide different levels of guaranteed message processing.</span></span> <span data-ttu-id="76a13-207">例如，基本的 Storm 應用程式可以保證至少處理一次，而 Trident 可以保證只處理一次。</span><span class="sxs-lookup"><span data-stu-id="76a13-207">For example, a basic Storm application can guarantee at-least-once processing, and Trident can guarantee exactly once processing.</span></span>

<span data-ttu-id="76a13-208">如需詳細資訊，請參閱 apache.org 上的 [保證處理資料](https://storm.apache.org/about/guarantees-data-processing.html) (英文)。</span><span class="sxs-lookup"><span data-stu-id="76a13-208">For more information, see [Guarantees on data processing](https://storm.apache.org/about/guarantees-data-processing.html) at apache.org.</span></span>

### <a name="ibasicbolt"></a><span data-ttu-id="76a13-209">IBasicBolt</span><span class="sxs-lookup"><span data-stu-id="76a13-209">IBasicBolt</span></span>

<span data-ttu-id="76a13-210">hello 讀取輸入的 tuple，發出零或多個 tuple 的模式，然後立即結尾 hello hello acking hello 輸入的 tuple execute 方法很常見。</span><span class="sxs-lookup"><span data-stu-id="76a13-210">hello pattern of reading an input tuple, emitting zero or more tuples, and then acking hello input tuple immediately at hello end of hello execute method is common.</span></span> <span data-ttu-id="76a13-211">Storm 提供 hello [IBasicBolt](https://storm.apache.org/releases/1.0.3/javadocs/org/apache/storm/topology/IBasicBolt.html)介面 tooautomate 此模式。</span><span class="sxs-lookup"><span data-stu-id="76a13-211">Storm provides hello [IBasicBolt](https://storm.apache.org/releases/1.0.3/javadocs/org/apache/storm/topology/IBasicBolt.html) interface tooautomate this pattern.</span></span>

### <a name="joins"></a><span data-ttu-id="76a13-212">聯結</span><span class="sxs-lookup"><span data-stu-id="76a13-212">Joins</span></span>

<span data-ttu-id="76a13-213">資料流的聯結方式會隨應用程式而異。</span><span class="sxs-lookup"><span data-stu-id="76a13-213">How data streams are joined varies between applications.</span></span> <span data-ttu-id="76a13-214">例如，您可以將多個串流中的每個 Tuple 聯結成一個新的串流，也可以只聯結特定時間範圍的幾批 Tuple。</span><span class="sxs-lookup"><span data-stu-id="76a13-214">For example, you can join each tuple from multiple streams into one new stream, or you can join only batches of tuples for a specific window.</span></span> <span data-ttu-id="76a13-215">無論何者，都可利用 [fieldsGrouping](http://storm.apache.org/releases/current/javadocs/org/apache/storm/topology/InputDeclarer.html#fieldsGrouping-java.lang.String-org.apache.storm.tuple.Fields-) 來完成聯結。</span><span class="sxs-lookup"><span data-stu-id="76a13-215">Either way, joining can be accomplished by using [fieldsGrouping](http://storm.apache.org/releases/current/javadocs/org/apache/storm/topology/InputDeclarer.html#fieldsGrouping-java.lang.String-org.apache.storm.tuple.Fields-).</span></span> <span data-ttu-id="76a13-216">群組欄位會是一種方式定義 tuple 的路由的 toobolts 的方式。</span><span class="sxs-lookup"><span data-stu-id="76a13-216">Field grouping is a way of defining how tuples are routed toobolts.</span></span>

<span data-ttu-id="76a13-217">在下列範例 Java hello，fieldsGrouping 會是"1"、"2"和"3"的元件 toohello MyJoiner 閃電源自使用的 tooroute tuple:</span><span class="sxs-lookup"><span data-stu-id="76a13-217">In hello following Java example, fieldsGrouping is used tooroute tuples that originate from components "1", "2", and "3" toohello MyJoiner bolt:</span></span>

    builder.setBolt("join", new MyJoiner(), parallelism) .fieldsGrouping("1", new Fields("joinfield1", "joinfield2")) .fieldsGrouping("2", new Fields("joinfield1", "joinfield2")) .fieldsGrouping("3", new Fields("joinfield1", "joinfield2"));

### <a name="batches"></a><span data-ttu-id="76a13-218">批次</span><span class="sxs-lookup"><span data-stu-id="76a13-218">Batches</span></span>

<span data-ttu-id="76a13-219">Apache Storm 提供稱為「計時 Tuple」的內部計時機制。</span><span class="sxs-lookup"><span data-stu-id="76a13-219">Apache Storm provides an internal timing mechanism known as a "tick tuple."</span></span> <span data-ttu-id="76a13-220">您可以設定在您的拓撲中發出計時 Tuple 的頻率。</span><span class="sxs-lookup"><span data-stu-id="76a13-220">You can set how often a tick tuple is emitted in your topology.</span></span>

<span data-ttu-id="76a13-221">如需使用 C# 元件中 tick tuple 的範例，請參閱 [PartialBoltCount.cs](https://github.com/hdinsight/hdinsight-storm-examples/blob/3b2c960549cac122e8874931df4801f0934fffa7/EventCountExample/EventCountTopology/src/main/java/com/microsoft/hdinsight/storm/examples/PartialCountBolt.java)。</span><span class="sxs-lookup"><span data-stu-id="76a13-221">For an example of using a tick tuple from a C# component, see [PartialBoltCount.cs](https://github.com/hdinsight/hdinsight-storm-examples/blob/3b2c960549cac122e8874931df4801f0934fffa7/EventCountExample/EventCountTopology/src/main/java/com/microsoft/hdinsight/storm/examples/PartialCountBolt.java).</span></span>

### <a name="caches"></a><span data-ttu-id="76a13-222">快取</span><span class="sxs-lookup"><span data-stu-id="76a13-222">Caches</span></span>

<span data-ttu-id="76a13-223">通常會使用記憶體內部快取當做加速處理的機制，因為此方式可以將常用的資產保留在記憶體內。</span><span class="sxs-lookup"><span data-stu-id="76a13-223">In-memory caching is often used as a mechanism for speeding up processing because it keeps frequently used assets in memory.</span></span> <span data-ttu-id="76a13-224">由於拓撲會分散到多個節點，多個處理序位於每個節點內，您應該考慮使用 [fieldsGrouping](http://storm.apache.org/releases/current/javadocs/org/apache/storm/topology/InputDeclarer.html#fieldsGrouping-java.lang.String-org.apache.storm.tuple.Fields-)。</span><span class="sxs-lookup"><span data-stu-id="76a13-224">Because a topology is distributed across multiple nodes, and multiple processes within each node, you should consider using [fieldsGrouping](http://storm.apache.org/releases/current/javadocs/org/apache/storm/topology/InputDeclarer.html#fieldsGrouping-java.lang.String-org.apache.storm.tuple.Fields-).</span></span> <span data-ttu-id="76a13-225">使用`fieldsGrouping`tooensure tuple，其中包含用於快取查閱的 hello 欄位一律會路由的 toohello 相同的處理序。</span><span class="sxs-lookup"><span data-stu-id="76a13-225">Use `fieldsGrouping` tooensure that tuples containing hello fields that are used for cache lookup are always routed toohello same process.</span></span> <span data-ttu-id="76a13-226">此群組功能可避免快取項目在程序之間重複。</span><span class="sxs-lookup"><span data-stu-id="76a13-226">This grouping functionality avoids duplication of cache entries across processes.</span></span>

### <a name="stream-top-n"></a><span data-ttu-id="76a13-227">串流「前 N 個」</span><span class="sxs-lookup"><span data-stu-id="76a13-227">Stream "top N"</span></span>

<span data-ttu-id="76a13-228">計算 top N 值取決於您的拓撲，計算以平行方式 hello 前 n 個值。</span><span class="sxs-lookup"><span data-stu-id="76a13-228">When your topology depends on calculating a top N value, calculate hello top N value in parallel.</span></span> <span data-ttu-id="76a13-229">然後合併 hello 輸出從這些計算成全域值。</span><span class="sxs-lookup"><span data-stu-id="76a13-229">Then merge hello output from those calculations into a global value.</span></span> <span data-ttu-id="76a13-230">這項作業可藉由來使用[fieldsGrouping](http://storm.apache.org/releases/current/javadocs/org/apache/storm/topology/InputDeclarer.html#fieldsGrouping-java.lang.String-org.apache.storm.tuple.Fields-) tooroute 透過平行處理的欄位。</span><span class="sxs-lookup"><span data-stu-id="76a13-230">This operation can be done by using [fieldsGrouping](http://storm.apache.org/releases/current/javadocs/org/apache/storm/topology/InputDeclarer.html#fieldsGrouping-java.lang.String-org.apache.storm.tuple.Fields-) tooroute by field for parallel processing.</span></span> <span data-ttu-id="76a13-231">然後您可以路由 tooa 閃電全域決定 hello 前 n 個值。</span><span class="sxs-lookup"><span data-stu-id="76a13-231">Then you can route tooa bolt that globally determines hello top N value.</span></span>

<span data-ttu-id="76a13-232">如需計算前 n 個值的範例，請參閱 hello [RollingTopWords](https://github.com/apache/storm/blob/master/examples/storm-starter/src/jvm/org/apache/storm/starter/RollingTopWords.java)範例。</span><span class="sxs-lookup"><span data-stu-id="76a13-232">For an example of calculating a top N value, see hello [RollingTopWords](https://github.com/apache/storm/blob/master/examples/storm-starter/src/jvm/org/apache/storm/starter/RollingTopWords.java) example.</span></span>

## <a name="logging"></a><span data-ttu-id="76a13-233">記錄</span><span class="sxs-lookup"><span data-stu-id="76a13-233">Logging</span></span>

<span data-ttu-id="76a13-234">Storm 使用 Apache Log4j toolog 資訊。</span><span class="sxs-lookup"><span data-stu-id="76a13-234">Storm uses Apache Log4j toolog information.</span></span> <span data-ttu-id="76a13-235">根據預設，大量的資料會記錄，並可能很難 toosort 透過 hello 資訊。</span><span class="sxs-lookup"><span data-stu-id="76a13-235">By default, a large amount of data is logged, and it can be difficult toosort through hello information.</span></span> <span data-ttu-id="76a13-236">您可以包含記錄的組態檔做為您的 Storm 拓樸 toocontrol 記錄行為的一部分。</span><span class="sxs-lookup"><span data-stu-id="76a13-236">You can include a logging configuration file as part of your Storm topology toocontrol logging behavior.</span></span>

<span data-ttu-id="76a13-237">示範範例拓撲如何 tooconfigure 記錄，請參閱[Java 為基礎的 WordCount](hdinsight-storm-develop-java-topology.md) Storm HDInsight 上的範例。</span><span class="sxs-lookup"><span data-stu-id="76a13-237">For an example topology that demonstrates how tooconfigure logging, see [Java-based WordCount](hdinsight-storm-develop-java-topology.md) example for Storm on HDInsight.</span></span>

## <a name="next-steps"></a><span data-ttu-id="76a13-238">後續步驟</span><span class="sxs-lookup"><span data-stu-id="76a13-238">Next steps</span></span>

<span data-ttu-id="76a13-239">深入了解使用 Storm on HDInsight 的即時分析解決方案：</span><span class="sxs-lookup"><span data-stu-id="76a13-239">Learn more about real-time analytics solutions with Storm on HDInsight:</span></span>

* <span data-ttu-id="76a13-240">[開始使用 Apache Storm on HDInsight][gettingstarted]</span><span class="sxs-lookup"><span data-stu-id="76a13-240">[Get started with Apache Storm on HDInsight][gettingstarted]</span></span>
* [<span data-ttu-id="76a13-241">Apache Storm on HDInsight 的範例拓撲</span><span class="sxs-lookup"><span data-stu-id="76a13-241">Example topologies for Apache Storm on HDInsight</span></span>](hdinsight-storm-example-topology.md)

[stormtrident]: https://storm.apache.org/documentation/Trident-API-Overview.html
[samoa]: http://yahooeng.tumblr.com/post/65453012905/introducing-samoa-an-open-source-platform-for-mining
[apachetutorial]: https://storm.apache.org/documentation/Tutorial.html
[gettingstarted]: hdinsight-apache-storm-tutorial-get-started-linux.md
