---
title: "Hadoop、 Spark、 Kafka、 HBase，或 R 伺服器-Azure HDInsight aaaCluster 安裝 |Microsoft 文件"
description: "設定 Hadoop、 Kafka、 Spark、 HBase、 R 伺服器或 Storm 叢集 hdinsight 從瀏覽器、 hello Azure CLI、 Azure PowerShell、 REST 或 SDK。"
keywords: "hadoop 叢集設定、kafka 叢集設定、spark 叢集設定、什麼是 hadoop 中的叢集"
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 23a01938-3fe5-4e2e-8e8b-3368e1bbe2ca
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/06/2017
ms.author: jgao
ms.openlocfilehash: 80ec59d8a39f7fccb940503fd2dc3ae5afee6bcf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-clusters-in-hdinsight-with-hadoop-spark-kafka-and-more"></a><span data-ttu-id="7b013-104">使用 Hadoop、Spark 及 Kafka 等在 HDInsight 中設定叢集</span><span class="sxs-lookup"><span data-stu-id="7b013-104">Set up clusters in HDInsight with Hadoop, Spark, Kafka, and more</span></span>

[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

<span data-ttu-id="7b013-105">深入了解如何 tooset 安裝及設定在 HDInsight Hadoop、 Spark、 Kafka、 互動式 Hive、 HBase、 R 伺服器或 Storm 叢集。</span><span class="sxs-lookup"><span data-stu-id="7b013-105">Learn how tooset up and configure clusters in HDInsight with Hadoop, Spark, Kafka, Interactive Hive, HBase, R Server, or Storm.</span></span> <span data-ttu-id="7b013-106">此外，了解 toocustomize 的叢集，並將這些 tooa 網域加入安全性。</span><span class="sxs-lookup"><span data-stu-id="7b013-106">Also, learn how toocustomize clusters and add security by joining them tooa domain.</span></span>

<span data-ttu-id="7b013-107">Hadoop 叢集由數個虛擬機器 (節點) 組成，可用於分散處理作業。</span><span class="sxs-lookup"><span data-stu-id="7b013-107">A Hadoop cluster consists of several virtual machines (nodes) that are used for distributed processing of tasks.</span></span> <span data-ttu-id="7b013-108">Azure HDInsight 處理安裝的實作詳細資料和設定個別的節點，因此您只需要 tooprovide 一般組態資訊。</span><span class="sxs-lookup"><span data-stu-id="7b013-108">Azure HDInsight handles implementation details of installation and configuration of individual nodes, so you only have tooprovide general configuration information.</span></span> 

> [!IMPORTANT]
><span data-ttu-id="7b013-109">一旦建立叢集，並停止刪除 hello 叢集時，就會開始 HDInsight 叢集計費。</span><span class="sxs-lookup"><span data-stu-id="7b013-109">HDInsight cluster billing starts once a cluster is created and stops when hello cluster is deleted.</span></span> <span data-ttu-id="7b013-110">計費是以每分鐘按比例計算，因此不再使用時，請一律刪除您的叢集。</span><span class="sxs-lookup"><span data-stu-id="7b013-110">Billing is pro-rated per minute, so you should always delete your cluster when it is no longer in use.</span></span> <span data-ttu-id="7b013-111">了解如何太[刪除叢集。](hdinsight-delete-cluster.md)</span><span class="sxs-lookup"><span data-stu-id="7b013-111">Learn how too[delete a cluster.](hdinsight-delete-cluster.md)</span></span>
>

## <a name="cluster-setup-methods"></a><span data-ttu-id="7b013-112">叢集設定方法</span><span class="sxs-lookup"><span data-stu-id="7b013-112">Cluster setup methods</span></span>
<span data-ttu-id="7b013-113">hello 下表顯示 hello 不同的方法可以使用 tooset HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="7b013-113">hello following table shows hello different methods you can use tooset up an HDInsight cluster.</span></span>

| <span data-ttu-id="7b013-114">叢集建立方法</span><span class="sxs-lookup"><span data-stu-id="7b013-114">Clusters created with</span></span> | <span data-ttu-id="7b013-115">Web 瀏覽器</span><span class="sxs-lookup"><span data-stu-id="7b013-115">Web browser</span></span> | <span data-ttu-id="7b013-116">命令列</span><span class="sxs-lookup"><span data-stu-id="7b013-116">Command line</span></span> | <span data-ttu-id="7b013-117">REST API</span><span class="sxs-lookup"><span data-stu-id="7b013-117">REST API</span></span> | <span data-ttu-id="7b013-118">SDK</span><span class="sxs-lookup"><span data-stu-id="7b013-118">SDK</span></span> | 
| --- |:---:|:---:|:---:|:---:|
| [<span data-ttu-id="7b013-119">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="7b013-119">Azure portal</span></span>](hdinsight-hadoop-create-linux-clusters-portal.md) |<span data-ttu-id="7b013-120">✔</span><span class="sxs-lookup"><span data-stu-id="7b013-120">✔</span></span> |&nbsp; |&nbsp; |&nbsp; |
| [<span data-ttu-id="7b013-121">Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="7b013-121">Azure Data Factory</span></span>](hdinsight-hadoop-create-linux-clusters-adf.md) |<span data-ttu-id="7b013-122">✔</span><span class="sxs-lookup"><span data-stu-id="7b013-122">✔</span></span> |<span data-ttu-id="7b013-123">✔</span><span class="sxs-lookup"><span data-stu-id="7b013-123">✔</span></span> |<span data-ttu-id="7b013-124">✔</span><span class="sxs-lookup"><span data-stu-id="7b013-124">✔</span></span> |<span data-ttu-id="7b013-125">✔</span><span class="sxs-lookup"><span data-stu-id="7b013-125">✔</span></span> |
| [<span data-ttu-id="7b013-126">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="7b013-126">Azure CLI</span></span>](hdinsight-hadoop-create-linux-clusters-azure-cli.md) |&nbsp; |<span data-ttu-id="7b013-127">✔</span><span class="sxs-lookup"><span data-stu-id="7b013-127">✔</span></span> |&nbsp; |&nbsp; |
| [<span data-ttu-id="7b013-128">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="7b013-128">Azure PowerShell</span></span>](hdinsight-hadoop-create-linux-clusters-azure-powershell.md) |&nbsp; |<span data-ttu-id="7b013-129">✔</span><span class="sxs-lookup"><span data-stu-id="7b013-129">✔</span></span> |&nbsp; |&nbsp; |
| [<span data-ttu-id="7b013-130">cURL</span><span class="sxs-lookup"><span data-stu-id="7b013-130">cURL</span></span>](hdinsight-hadoop-create-linux-clusters-curl-rest.md) |&nbsp; |<span data-ttu-id="7b013-131">✔</span><span class="sxs-lookup"><span data-stu-id="7b013-131">✔</span></span> |<span data-ttu-id="7b013-132">✔</span><span class="sxs-lookup"><span data-stu-id="7b013-132">✔</span></span> |&nbsp; |
| [<span data-ttu-id="7b013-133">.NET SDK</span><span class="sxs-lookup"><span data-stu-id="7b013-133">.NET SDK</span></span>](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md) |&nbsp; |&nbsp; |&nbsp; |<span data-ttu-id="7b013-134">✔</span><span class="sxs-lookup"><span data-stu-id="7b013-134">✔</span></span> |
| [<span data-ttu-id="7b013-135">Azure 資源管理員範本</span><span class="sxs-lookup"><span data-stu-id="7b013-135">Azure Resource Manager templates</span></span>](hdinsight-hadoop-create-linux-clusters-arm-templates.md) |&nbsp; |<span data-ttu-id="7b013-136">✔</span><span class="sxs-lookup"><span data-stu-id="7b013-136">✔</span></span> |&nbsp; |&nbsp; |

## <a name="quick-create-basic-cluster-setup"></a><span data-ttu-id="7b013-137">快速建立：基本的叢集設定</span><span class="sxs-lookup"><span data-stu-id="7b013-137">Quick create: Basic cluster setup</span></span>
<span data-ttu-id="7b013-138">這篇文章會引導您完成安裝程式在 hello [Azure 入口網站](https://portal.azure.com)，其中您可以建立 HDInsight 叢集使用*快速建立*或*自訂*。</span><span class="sxs-lookup"><span data-stu-id="7b013-138">This article walks you through setup in hello [Azure portal](https://portal.azure.com), where you can create an HDInsight cluster using *Quick create* or *Custom*.</span></span> 

<span data-ttu-id="7b013-139">按照 hello 螢幕 toodo 基本叢集設定中的指示進行。</span><span class="sxs-lookup"><span data-stu-id="7b013-139">Follow instructions on hello screen toodo a basic cluster setup.</span></span> <span data-ttu-id="7b013-140">以下是下列各項的詳細資訊：</span><span class="sxs-lookup"><span data-stu-id="7b013-140">Details are provided below for:</span></span>

* [<span data-ttu-id="7b013-141">資源群組名稱</span><span class="sxs-lookup"><span data-stu-id="7b013-141">Resource group name</span></span>](#resource-group-name)
* [<span data-ttu-id="7b013-142">叢集類型和設定</span><span class="sxs-lookup"><span data-stu-id="7b013-142">Cluster types and configuration</span></span>](#cluster-types) 
* [<span data-ttu-id="7b013-143">叢集登入和 SSH 使用者名稱</span><span class="sxs-lookup"><span data-stu-id="7b013-143">Cluster login and SSH username</span></span>](#cluster-login-and-ssh-username)
* [<span data-ttu-id="7b013-144">位置</span><span class="sxs-lookup"><span data-stu-id="7b013-144">Location</span></span>](#location)

> [!IMPORTANT]
> <span data-ttu-id="7b013-145">Linux 為 hello 僅作業系統 HDInsight 3.4 或更新版本上使用。</span><span class="sxs-lookup"><span data-stu-id="7b013-145">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="7b013-146">如需詳細資訊，請參閱 [HDInsight 3.3 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。</span><span class="sxs-lookup"><span data-stu-id="7b013-146">For more information, see [HDInsight 3.3 retirement](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>
>

## <a name="resource-group-name"></a><span data-ttu-id="7b013-147">資源群組名稱</span><span class="sxs-lookup"><span data-stu-id="7b013-147">Resource group name</span></span> 

<span data-ttu-id="7b013-148">[Azure 資源管理員](../azure-resource-manager/resource-group-overview.md)可協助您處理 hello 資源群組中，參考 tooas 為應用程式中的 Azure 資源群組。</span><span class="sxs-lookup"><span data-stu-id="7b013-148">[Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) helps you work with hello resources in your application as a group, referred tooas an Azure resource group.</span></span> <span data-ttu-id="7b013-149">您可以部署、 更新、 監視或刪除您的應用程式在單一協調作業中的 hello 的所有資源。</span><span class="sxs-lookup"><span data-stu-id="7b013-149">You can deploy, update, monitor, or delete all hello resources for your application in a single coordinated operation.</span></span>

## <span data-ttu-id="7b013-150"><a name="cluster-types"></a>叢集類型和設定</span><span class="sxs-lookup"><span data-stu-id="7b013-150"><a name="cluster-types"></a> Cluster types and configuration</span></span>
<span data-ttu-id="7b013-151">Azure HDInsight 目前提供 hello 下列叢集類型，各有一組元件 tooprovide 的某些功能。</span><span class="sxs-lookup"><span data-stu-id="7b013-151">Azure HDInsight currently provides hello following cluster types, each with a set of components tooprovide certain functionalities.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7b013-152">HDInsight 叢集有多種類型，每種類型各適合單一工作負載或技術。</span><span class="sxs-lookup"><span data-stu-id="7b013-152">HDInsight clusters are available in various types, each for a single workload or technology.</span></span> <span data-ttu-id="7b013-153">沒有任何支援的方法 toocreate 結合多個類型，例如 Storm 和上一個叢集的 HBase 叢集。</span><span class="sxs-lookup"><span data-stu-id="7b013-153">There is no supported method toocreate a cluster that combines multiple types, such as Storm and HBase on one cluster.</span></span> <span data-ttu-id="7b013-154">如果您的方案要求分散到多個的 HDInsight 叢集類型的技術[Azure 虛擬網路](https://docs.microsoft.com/azure/virtual-network)可以連接所需的 hello 叢集類型。</span><span class="sxs-lookup"><span data-stu-id="7b013-154">If your solution requires technologies that are spread across multiple HDInsight cluster types, an [Azure virtual network](https://docs.microsoft.com/azure/virtual-network) can connect hello required cluster types.</span></span> 
>
>

| <span data-ttu-id="7b013-155">叢集類型</span><span class="sxs-lookup"><span data-stu-id="7b013-155">Cluster type</span></span> | <span data-ttu-id="7b013-156">功能</span><span class="sxs-lookup"><span data-stu-id="7b013-156">Functionality</span></span> |
| --- | --- |
| [<span data-ttu-id="7b013-157">Hadoop</span><span class="sxs-lookup"><span data-stu-id="7b013-157">Hadoop</span></span>](hdinsight-hadoop-introduction.md) |<span data-ttu-id="7b013-158">批次查詢和分析儲存的資料</span><span class="sxs-lookup"><span data-stu-id="7b013-158">Batch query and analysis of stored data</span></span> |
| [<span data-ttu-id="7b013-159">HBase</span><span class="sxs-lookup"><span data-stu-id="7b013-159">HBase</span></span>](hdinsight-hbase-overview.md) |<span data-ttu-id="7b013-160">處理大量無綱要的 NoSQL 資料</span><span class="sxs-lookup"><span data-stu-id="7b013-160">Processing for large amounts of schemaless, NoSQL data</span></span> |
| [<span data-ttu-id="7b013-161">Storm</span><span class="sxs-lookup"><span data-stu-id="7b013-161">Storm</span></span>](hdinsight-storm-overview.md) |<span data-ttu-id="7b013-162">即時事件處理</span><span class="sxs-lookup"><span data-stu-id="7b013-162">Real-time event processing</span></span> |
| [<span data-ttu-id="7b013-163">Spark</span><span class="sxs-lookup"><span data-stu-id="7b013-163">Spark</span></span>](hdinsight-apache-spark-overview.md) |<span data-ttu-id="7b013-164">記憶體內處理、互動式查詢、微批次串流處理</span><span class="sxs-lookup"><span data-stu-id="7b013-164">In-memory processing, interactive queries, micro-batch stream processing</span></span> |
| [<span data-ttu-id="7b013-165">Kafka (預覽)</span><span class="sxs-lookup"><span data-stu-id="7b013-165">Kafka (Preview)</span></span>](hdinsight-apache-kafka-introduction.md) | <span data-ttu-id="7b013-166">分散式的資料流平台可能是使用的 toobuild 即時資料流資料管線和應用程式</span><span class="sxs-lookup"><span data-stu-id="7b013-166">A distributed streaming platform that can be used toobuild real-time streaming data pipelines and applications</span></span> |
| [<span data-ttu-id="7b013-167">R 伺服器</span><span class="sxs-lookup"><span data-stu-id="7b013-167">R Server</span></span>](hdinsight-hadoop-r-server-overview.md) |<span data-ttu-id="7b013-168">各種巨量資料統計資料、預測模型和機器學習功能</span><span class="sxs-lookup"><span data-stu-id="7b013-168">Various big data statistics, predictive modeling, and machine learning capabilities</span></span> |
| [<span data-ttu-id="7b013-169">互動式 Hive (預覽)</span><span class="sxs-lookup"><span data-stu-id="7b013-169">Interactive Hive (Preview)</span></span>](hdinsight-hadoop-use-interactive-hive.md) |<span data-ttu-id="7b013-170">更快速之互動式 Hive 查詢的記憶體內快取</span><span class="sxs-lookup"><span data-stu-id="7b013-170">In-memory caching for interactive and faster Hive queries</span></span> |

### <a name="number-of-nodes-for-each-cluster-type"></a><span data-ttu-id="7b013-171">每個叢集類型的節點數目</span><span class="sxs-lookup"><span data-stu-id="7b013-171">Number of nodes for each cluster type</span></span>
<span data-ttu-id="7b013-172">每個叢集類型都有自己的節點數目、節點術語和預設 VM 大小。</span><span class="sxs-lookup"><span data-stu-id="7b013-172">Each cluster type has its own number of nodes, terminology for nodes, and default VM size.</span></span> <span data-ttu-id="7b013-173">在下表的 hello，hello 每個節點類型的節點數目是在括號中。</span><span class="sxs-lookup"><span data-stu-id="7b013-173">In hello following table, hello number of nodes for each node type is in parentheses.</span></span>

| <span data-ttu-id="7b013-174">類型</span><span class="sxs-lookup"><span data-stu-id="7b013-174">Type</span></span> | <span data-ttu-id="7b013-175">節點</span><span class="sxs-lookup"><span data-stu-id="7b013-175">Nodes</span></span> | <span data-ttu-id="7b013-176">圖表</span><span class="sxs-lookup"><span data-stu-id="7b013-176">Diagram</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7b013-177">Hadoop</span><span class="sxs-lookup"><span data-stu-id="7b013-177">Hadoop</span></span> |<span data-ttu-id="7b013-178">前端節點 (2)、資料節點 (1+)</span><span class="sxs-lookup"><span data-stu-id="7b013-178">Head node (2), data node (1+)</span></span> |![HDInsight Hadoop 叢集節點](./media/hdinsight-hadoop-provision-linux-clusters/hdinsight-hadoop-cluster-type-nodes.png) |
| <span data-ttu-id="7b013-180">HBase</span><span class="sxs-lookup"><span data-stu-id="7b013-180">HBase</span></span> |<span data-ttu-id="7b013-181">前端伺服器 (2)、區域伺服器 (1+)、主要/Zookeeper 節點 (3)</span><span class="sxs-lookup"><span data-stu-id="7b013-181">Head server (2), region server (1+), master/ZooKeeper node (3)</span></span> |![HDInsight HBase 叢集節點](./media/hdinsight-hadoop-provision-linux-clusters/hdinsight-hbase-cluster-type-setup.png) |
| <span data-ttu-id="7b013-183">Storm</span><span class="sxs-lookup"><span data-stu-id="7b013-183">Storm</span></span> |<span data-ttu-id="7b013-184">Nimbus 節點 (2)、監督員伺服器 (1+)、Zookeeper 節點 (3)</span><span class="sxs-lookup"><span data-stu-id="7b013-184">Nimbus node (2), supervisor server (1+), ZooKeeper node (3)</span></span> |![HDInsight Storm 叢集節點](./media/hdinsight-hadoop-provision-linux-clusters/hdinsight-storm-cluster-type-setup.png) |
| <span data-ttu-id="7b013-186">Spark</span><span class="sxs-lookup"><span data-stu-id="7b013-186">Spark</span></span> |<span data-ttu-id="7b013-187">前端節點 (2)、背景工作角色節點 (1+)、Zookeeper 節點 (3) (A1 Zookeeper VM 大小不限)</span><span class="sxs-lookup"><span data-stu-id="7b013-187">Head node (2), worker node (1+), ZooKeeper node (3) (free for A1 ZooKeeper VM size)</span></span> |![HDInsight Spark 叢集節點](./media/hdinsight-hadoop-provision-linux-clusters/hdinsight-spark-cluster-type-setup.png) |

<span data-ttu-id="7b013-189">如需詳細資訊，請參閱[預設叢集的節點，以及虛擬機器大小](hdinsight-component-versioning.md#default-node-configuration-and-virtual-machine-sizes-for-clusters)中 「 什麼是 hello Hadoop 元件與 HDInsight 中的版本 」？</span><span class="sxs-lookup"><span data-stu-id="7b013-189">For more information, see [Default node configuration and virtual machine sizes for clusters](hdinsight-component-versioning.md#default-node-configuration-and-virtual-machine-sizes-for-clusters) in "What are hello Hadoop components and versions in HDInsight?"</span></span>

### <a name="hdinsight-version"></a><span data-ttu-id="7b013-190">HDInsight 版本</span><span class="sxs-lookup"><span data-stu-id="7b013-190">HDInsight version</span></span>
<span data-ttu-id="7b013-191">選擇此叢集 HDInsight hello 版本。</span><span class="sxs-lookup"><span data-stu-id="7b013-191">Choose hello version of HDInsight for this cluster.</span></span> <span data-ttu-id="7b013-192">如需詳細資訊，請參閱[支援的 HDInsight 版本](hdinsight-component-versioning.md#supported-hdinsight-versions)。</span><span class="sxs-lookup"><span data-stu-id="7b013-192">For more information, see [Supported HDInsight versions](hdinsight-component-versioning.md#supported-hdinsight-versions).</span></span>

### <span data-ttu-id="7b013-193"><a name="cluster-tiers"></a>叢集層：HDInsight 服務層</span><span class="sxs-lookup"><span data-stu-id="7b013-193"><a name="cluster-tiers"></a>Cluster tier: HDInsight service tiers</span></span>

<span data-ttu-id="7b013-194">Azure HDInsight 提供兩個服務層中的 hello 巨量資料雲端方案： Standard 和 Premium。</span><span class="sxs-lookup"><span data-stu-id="7b013-194">Azure HDInsight provides hello big data cloud offerings in two service tiers: Standard and Premium.</span></span>  <span data-ttu-id="7b013-195">如需詳細資訊，請參閱 [HDInsight Standard 和 HDInsight Premium](hdinsight-component-versioning.md#hdinsight-standard-and-hdinsight-premium)。</span><span class="sxs-lookup"><span data-stu-id="7b013-195">For more information, see [HDInsight Standard and HDInsight Premium](hdinsight-component-versioning.md#hdinsight-standard-and-hdinsight-premium).</span></span>

<span data-ttu-id="7b013-196">hello 下列螢幕擷取畫面顯示 hello 選擇叢集類型的 Azure 入口網站的資訊。</span><span class="sxs-lookup"><span data-stu-id="7b013-196">hello following screenshot shows hello Azure portal information for choosing cluster types.</span></span>

![HDInsight 進階組態](./media/hdinsight-hadoop-provision-linux-clusters/hdinsight-cluster-type-configuration.png)


## <a name="cluster-login-and-ssh-user-name"></a><span data-ttu-id="7b013-198">叢集登入和 SSH 使用者名稱</span><span class="sxs-lookup"><span data-stu-id="7b013-198">Cluster login and SSH user name</span></span>
<span data-ttu-id="7b013-199">使用 HDInsight 叢集，您可以在建立叢集期間設定兩個使用者帳戶：</span><span class="sxs-lookup"><span data-stu-id="7b013-199">With HDInsight clusters, you can configure two user accounts during cluster creation:</span></span>

* <span data-ttu-id="7b013-200">HTTP 使用者： hello 預設使用者名稱是*admin*。它會使用基本組態的 hello hello Azure 入口網站上。</span><span class="sxs-lookup"><span data-stu-id="7b013-200">HTTP user: hello default user name is *admin*. It uses hello basic configuration on hello Azure portal.</span></span> <span data-ttu-id="7b013-201">有時稱之為「叢集使用者」。</span><span class="sxs-lookup"><span data-stu-id="7b013-201">Sometimes it is called "Cluster user."</span></span>
* <span data-ttu-id="7b013-202">SSH 使用者 （Linux 叢集）： 透過 SSH 使用的 tooconnect toohello 叢集。</span><span class="sxs-lookup"><span data-stu-id="7b013-202">SSH user (Linux clusters): Used tooconnect toohello cluster through SSH.</span></span> <span data-ttu-id="7b013-203">如需詳細資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。</span><span class="sxs-lookup"><span data-stu-id="7b013-203">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

## <span data-ttu-id="7b013-204"><a name="location"></a>叢集與儲存體的位置 (區域)</span><span class="sxs-lookup"><span data-stu-id="7b013-204"><a name="location"></a>Location (regions) for clusters and storage</span></span>

<span data-ttu-id="7b013-205">您不需要 toospecify hello 叢集位置明確： hello 叢集處於 hello 與 hello 預設儲存體相同的位置。</span><span class="sxs-lookup"><span data-stu-id="7b013-205">You don't need toospecify hello cluster location explicitly: hello cluster is in hello same location as hello default storage.</span></span> <span data-ttu-id="7b013-206">如需支援的地區中，按一下 hello**區域**下拉式清單上的[HDInsight 定價](https://go.microsoft.com/fwLink/?LinkID=282635&clcid=0x409)。</span><span class="sxs-lookup"><span data-stu-id="7b013-206">For a list of supported regions, click hello **Region** drop-down list on [HDInsight pricing](https://go.microsoft.com/fwLink/?LinkID=282635&clcid=0x409).</span></span>

## <a name="storage-endpoints-for-clusters"></a><span data-ttu-id="7b013-207">叢集的儲存體端點</span><span class="sxs-lookup"><span data-stu-id="7b013-207">Storage endpoints for clusters</span></span>

<span data-ttu-id="7b013-208">雖然在內部部署安裝的 Hadoop 使用 hello Hadoop 分散式檔案系統 (HDFS) hello 叢集上的存放裝置，但在 hello 雲端使用儲存體端點會連接 toocluster。</span><span class="sxs-lookup"><span data-stu-id="7b013-208">Although an on-premises installation of Hadoop uses hello Hadoop Distributed File System (HDFS) for storage on hello cluster, in hello cloud you use storage endpoints connected toocluster.</span></span> <span data-ttu-id="7b013-209">HDInsight 叢集會使用 [Azure Data Lake Store](hdinsight-hadoop-use-data-lake-store.md) 或 [Azure 儲存體中的 Blob](hdinsight-hadoop-use-blob-storage.md)。</span><span class="sxs-lookup"><span data-stu-id="7b013-209">HDInsight clusters use either [Azure Data Lake Store](hdinsight-hadoop-use-data-lake-store.md) or [blobs in Azure Storage](hdinsight-hadoop-use-blob-storage.md).</span></span> <span data-ttu-id="7b013-210">使用 Azure 儲存體或資料湖存放區，表示您可以安全地刪除 hello HDInsight 叢集用於計算，同時保留您的資料。</span><span class="sxs-lookup"><span data-stu-id="7b013-210">Using Azure Storage or Data Lake Store means you can safely delete hello HDInsight clusters used for computation while still retaining your data.</span></span> 

> [!WARNING]
> <span data-ttu-id="7b013-211">不支援從 hello HDInsight 叢集的不同位置中使用額外的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="7b013-211">Using an additional storage account in a different location from hello HDInsight cluster is not supported.</span></span>

<span data-ttu-id="7b013-212">在設定期間，對於 hello 預設儲存體端點指定 blob 容器的 Azure 儲存體帳戶或資料湖存放區。</span><span class="sxs-lookup"><span data-stu-id="7b013-212">During configuration, for hello default storage endpoint you specify a blob container of an Azure Storage account or a Data Lake Store.</span></span> <span data-ttu-id="7b013-213">hello 預設儲存體包含應用程式與系統記錄檔。</span><span class="sxs-lookup"><span data-stu-id="7b013-213">hello default storage contains application and system logs.</span></span> <span data-ttu-id="7b013-214">您可以選擇性地指定其他連結的 Azure 儲存體帳戶和 hello 叢集的 Data Lake Store 帳戶可以存取。</span><span class="sxs-lookup"><span data-stu-id="7b013-214">Optionally, you can specify additional linked Azure Storage accounts and Data Lake Store accounts that hello cluster can access.</span></span> <span data-ttu-id="7b013-215">hello HDInsight 叢集和 hello 相依的儲存體帳戶必須在 hello 相同的 Azure 位置。</span><span class="sxs-lookup"><span data-stu-id="7b013-215">hello HDInsight cluster and hello dependent storage accounts must be in hello same Azure location.</span></span>

![叢集儲存體設定：HDFS 相容的儲存體端點](./media/hdinsight-hadoop-provision-linux-clusters/hdinsight-cluster-creation-storage.png)

[!INCLUDE [secure-transfer-enabled-storage-account](../../includes/hdinsight-secure-transfer.md)]


### <a name="optional-metastores"></a><span data-ttu-id="7b013-217">選擇性中繼存放區</span><span class="sxs-lookup"><span data-stu-id="7b013-217">Optional metastores</span></span>
<span data-ttu-id="7b013-218">您可以建立選擇性的 Hive 或 Oozie 中繼存放區。</span><span class="sxs-lookup"><span data-stu-id="7b013-218">You can create optional Hive or Oozie metastores.</span></span> <span data-ttu-id="7b013-219">不過，並非所有叢集類型都支援中繼存放區，且 Azure SQL 資料倉儲不相容於中繼存放區。</span><span class="sxs-lookup"><span data-stu-id="7b013-219">However, not all cluster types support metastores, and Azure SQL Data Warehouse isn't compatible with metastores.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="7b013-220">當您建立自訂的中繼存放區時，不使用連字號、 連字號或空格 hello 資料庫名稱。</span><span class="sxs-lookup"><span data-stu-id="7b013-220">When you create a custom metastore, don't use dashes, hyphens, or spaces in hello database name.</span></span> <span data-ttu-id="7b013-221">這可能會造成 hello 叢集建立程序 toofail。</span><span class="sxs-lookup"><span data-stu-id="7b013-221">This can cause hello cluster creation process toofail.</span></span>

### <span data-ttu-id="7b013-222"><a name="use-hiveoozie-metastore"></a>Hive 中繼存放區</span><span class="sxs-lookup"><span data-stu-id="7b013-222"><a name="use-hiveoozie-metastore"></a>Hive metastore</span></span>

<span data-ttu-id="7b013-223">如果您想 tooretain Hive 資料表刪除 HDInsight 叢集之後，，使用自訂的中繼存放區。</span><span class="sxs-lookup"><span data-stu-id="7b013-223">If you want tooretain your Hive tables after you delete an HDInsight cluster, use a custom metastore.</span></span> <span data-ttu-id="7b013-224">然後，您可以附加 hello 中繼存放區 tooanother HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="7b013-224">You can then attach hello metastore tooanother HDInsight cluster.</span></span>

<span data-ttu-id="7b013-225">針對某個 HDInsight 叢集版本建立的 HDInsight 中繼存放區，不能在不同的 HDInsight 叢集版本之間共用。</span><span class="sxs-lookup"><span data-stu-id="7b013-225">An HDInsight metastore that is created for one HDInsight cluster version cannot be shared across different HDInsight cluster versions.</span></span> <span data-ttu-id="7b013-226">如需 HDInsight 版本清單，請參閱[支援的 HDInsight 版本](hdinsight-component-versioning.md#supported-hdinsight-versions)。</span><span class="sxs-lookup"><span data-stu-id="7b013-226">For a list of HDInsight versions, see [Supported HDInsight versions](hdinsight-component-versioning.md#supported-hdinsight-versions).</span></span>

### <a name="oozie-metastore"></a><span data-ttu-id="7b013-227">Oozie 中繼存放區</span><span class="sxs-lookup"><span data-stu-id="7b013-227">Oozie metastore</span></span>

<span data-ttu-id="7b013-228">tooincrease 效能時使用 Oozie，使用自訂的中繼存放區。</span><span class="sxs-lookup"><span data-stu-id="7b013-228">tooincrease performance when using Oozie, use a custom metastore.</span></span> <span data-ttu-id="7b013-229">刪除您的叢集之後，中繼存放區也可以提供存取 tooOozie 作業資料。</span><span class="sxs-lookup"><span data-stu-id="7b013-229">A metastore can also provide access tooOozie job data after you delete your cluster.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="7b013-230">您無法重複使用自訂的 Oozie 中繼存放區。</span><span class="sxs-lookup"><span data-stu-id="7b013-230">You cannot reuse a custom Oozie metastore.</span></span> <span data-ttu-id="7b013-231">toouse 自訂的 Oozie 中繼存放區，建立 hello HDInsight 叢集時，必須提供空的 Azure SQL Database。</span><span class="sxs-lookup"><span data-stu-id="7b013-231">toouse a custom Oozie metastore, you must provide an empty Azure SQL Database when creating hello HDInsight cluster.</span></span>

## <a name="configure-cluster-size"></a><span data-ttu-id="7b013-232">設定叢集大小</span><span class="sxs-lookup"><span data-stu-id="7b013-232">Configure cluster size</span></span>

<span data-ttu-id="7b013-233">您付費的節點使用量，只要 hello 叢集存在。</span><span class="sxs-lookup"><span data-stu-id="7b013-233">You are billed for node usage for as long as hello cluster exists.</span></span> <span data-ttu-id="7b013-234">在叢集建立時並停止刪除 hello 叢集時，就會開始計費。</span><span class="sxs-lookup"><span data-stu-id="7b013-234">Billing starts when a cluster is created and stops when hello cluster is deleted.</span></span> <span data-ttu-id="7b013-235">無法取消配置或保留叢集。</span><span class="sxs-lookup"><span data-stu-id="7b013-235">Clusters can’t be de-allocated or put on hold.</span></span>

<span data-ttu-id="7b013-236">HDInsight 叢集的 hello 成本取決於節點和 hello hello 節點的虛擬機器大小的 hello 數目。</span><span class="sxs-lookup"><span data-stu-id="7b013-236">hello cost of HDInsight clusters is determined by hello number of nodes and hello virtual machines sizes for hello nodes.</span></span> 

<span data-ttu-id="7b013-237">不同的叢集類型具有不同的節點類型、節點數目和節點大小：</span><span class="sxs-lookup"><span data-stu-id="7b013-237">Different cluster types have different node types, numbers of nodes, and node sizes:</span></span>
* <span data-ttu-id="7b013-238">Hadoop 叢集類型的預設值：</span><span class="sxs-lookup"><span data-stu-id="7b013-238">Hadoop cluster type default:</span></span> 
    * <span data-ttu-id="7b013-239">兩個*前端節點*</span><span class="sxs-lookup"><span data-stu-id="7b013-239">Two *head nodes*</span></span>  
    * <span data-ttu-id="7b013-240">四個*資料節點*</span><span class="sxs-lookup"><span data-stu-id="7b013-240">Four *data nodes*</span></span>
* <span data-ttu-id="7b013-241">Storm 叢集類型的預設值：</span><span class="sxs-lookup"><span data-stu-id="7b013-241">Storm cluster type default:</span></span> 
    * <span data-ttu-id="7b013-242">兩個 *Nimbus 節點*</span><span class="sxs-lookup"><span data-stu-id="7b013-242">Two *Nimbus nodes*</span></span>
    * <span data-ttu-id="7b013-243">三個 *ZooKeeper 節點*</span><span class="sxs-lookup"><span data-stu-id="7b013-243">Three *ZooKeeper nodes*</span></span>
    * <span data-ttu-id="7b013-244">四個*監督員節點*</span><span class="sxs-lookup"><span data-stu-id="7b013-244">Four *supervisor nodes*</span></span> 

<span data-ttu-id="7b013-245">如果您只是在試用 HDInsight，建議您使用一個資料節點。</span><span class="sxs-lookup"><span data-stu-id="7b013-245">If you are just trying out HDInsight, we recommend you use one data node.</span></span> <span data-ttu-id="7b013-246">如需關於 HDInsight 定價的詳細資訊，請參閱 [HDInsight 定價](https://go.microsoft.com/fwLink/?LinkID=282635&clcid=0x409)。</span><span class="sxs-lookup"><span data-stu-id="7b013-246">For more information about HDInsight pricing, see [HDInsight pricing](https://go.microsoft.com/fwLink/?LinkID=282635&clcid=0x409).</span></span>

> [!NOTE]
> <span data-ttu-id="7b013-247">hello 叢集大小限制會因 Azure 訂用帳戶而異。</span><span class="sxs-lookup"><span data-stu-id="7b013-247">hello cluster size limit varies among Azure subscriptions.</span></span> <span data-ttu-id="7b013-248">請連絡[Azure 計費支援](https://docs.microsoft.com/azure/azure-supportability/how-to-create-azure-support-request)tooincrease hello 限制。</span><span class="sxs-lookup"><span data-stu-id="7b013-248">Contact [Azure billing support](https://docs.microsoft.com/azure/azure-supportability/how-to-create-azure-support-request) tooincrease hello limit.</span></span>
>

<span data-ttu-id="7b013-249">當您使用 hello Azure 入口網站 tooconfigure hello 叢集時，hello 節點大小是可透過 hello**節點定價層**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="7b013-249">When you use hello Azure portal tooconfigure hello cluster, hello node size is available through hello **Node Pricing Tiers** blade.</span></span> <span data-ttu-id="7b013-250">在 hello 入口網站，您也可以查看 hello hello 不同的節點大小與相關聯的成本。</span><span class="sxs-lookup"><span data-stu-id="7b013-250">In hello portal, you can also see hello cost associated with hello different node sizes.</span></span> 

![HDinsight VM 節點大小](./media/hdinsight-hadoop-provision-linux-clusters/hdinsight-node-sizes.png)

### <a name="virtual-machine-sizes"></a><span data-ttu-id="7b013-252">虛擬機器大小</span><span class="sxs-lookup"><span data-stu-id="7b013-252">Virtual machine sizes</span></span> 
<span data-ttu-id="7b013-253">當您部署叢集時，選擇基礎的計算資源 hello 解決方案計劃 toodeploy。</span><span class="sxs-lookup"><span data-stu-id="7b013-253">When you deploy clusters, choose compute resources based on hello solution you plan toodeploy.</span></span> <span data-ttu-id="7b013-254">下列 Vm 用於 HDInsight 叢集的 hello:</span><span class="sxs-lookup"><span data-stu-id="7b013-254">hello following VMs are used for HDInsight clusters:</span></span>
* <span data-ttu-id="7b013-255">A 和 D1-4 系列 VM：[一般用途 Linux VM 大小](https://docs.microsoft.com/azure/virtual-machines/linux/sizes-general)</span><span class="sxs-lookup"><span data-stu-id="7b013-255">A and D1-4 series VMs: [General-purpose Linux VM sizes](https://docs.microsoft.com/azure/virtual-machines/linux/sizes-general)</span></span>
* <span data-ttu-id="7b013-256">D11-14 系列 VM：[記憶體最佳化 Linux VM 大小](https://docs.microsoft.com/azure/virtual-machines/linux/sizes-memory)</span><span class="sxs-lookup"><span data-stu-id="7b013-256">D11-14 series VM: [Memory-optimized Linux VM sizes](https://docs.microsoft.com/azure/virtual-machines/linux/sizes-memory)</span></span>

<span data-ttu-id="7b013-257">toofind 出何值您應該使用的 toospecify 時建立叢集使用的 VM 大小 hello 不同的 Sdk，或在使用 Azure PowerShell，請參閱[VM 大小的 HDInsight 叢集的 toouse](../cloud-services/cloud-services-sizes-specs.md#size-tables)。</span><span class="sxs-lookup"><span data-stu-id="7b013-257">toofind out what value you should use toospecify a VM size while creating a cluster using hello different SDKs or while using Azure PowerShell, see [VM sizes toouse for HDInsight clusters](../cloud-services/cloud-services-sizes-specs.md#size-tables).</span></span> <span data-ttu-id="7b013-258">在此連結的文件，請同時使用 hello 值 hello**大小**hello 資料表的資料行。</span><span class="sxs-lookup"><span data-stu-id="7b013-258">From this linked article, use hello value in hello **Size** column of hello tables.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7b013-259">如果您的叢集需要 32 個以上的背景工作角色節點，則必須選取具有至少 8 個核心和 14 GB RAM 的前端節點大小。</span><span class="sxs-lookup"><span data-stu-id="7b013-259">If you need more than 32 worker nodes in a cluster, you must select a head node size with at least 8 cores and 14 GB of RAM.</span></span>
>
>

<span data-ttu-id="7b013-260">如需相關資訊，請參閱[虛擬機器的大小](../virtual-machines/windows/sizes.md)。</span><span class="sxs-lookup"><span data-stu-id="7b013-260">For more information, see [Sizes for virtual machines](../virtual-machines/windows/sizes.md).</span></span> <span data-ttu-id="7b013-261">如需定價的 hello 各種大小資訊，請參閱[HDInsight 定價](https://azure.microsoft.com/pricing/details/hdinsight)。</span><span class="sxs-lookup"><span data-stu-id="7b013-261">For information about pricing of hello various sizes, see [HDInsight pricing](https://azure.microsoft.com/pricing/details/hdinsight).</span></span>   

## <a name="custom-cluster-setup"></a><span data-ttu-id="7b013-262">自訂叢集設定</span><span class="sxs-lookup"><span data-stu-id="7b013-262">Custom cluster setup</span></span>
<span data-ttu-id="7b013-263">自訂的叢集安裝組建上 hello 快速建立設定，並加入 hello 下列選項︰</span><span class="sxs-lookup"><span data-stu-id="7b013-263">Custom cluster setup builds on hello Quick create settings, and adds hello following options:</span></span>
- [<span data-ttu-id="7b013-264">HDInsight 應用程式</span><span class="sxs-lookup"><span data-stu-id="7b013-264">HDInsight applications</span></span>](#hdinsight-applications)
- [<span data-ttu-id="7b013-265">叢集大小</span><span class="sxs-lookup"><span data-stu-id="7b013-265">Cluster size</span></span>](#cluster-size)
- <span data-ttu-id="7b013-266">進階設定</span><span class="sxs-lookup"><span data-stu-id="7b013-266">Advanced settings</span></span>
  - [<span data-ttu-id="7b013-267">指令碼動作</span><span class="sxs-lookup"><span data-stu-id="7b013-267">Script actions</span></span>](#customize-clusters-using-script-action)
  - [<span data-ttu-id="7b013-268">虛擬網路</span><span class="sxs-lookup"><span data-stu-id="7b013-268">Virtual network</span></span>](#use-virtual-network)

## <a name="install-hdinsight-applications-on-clusters"></a><span data-ttu-id="7b013-269">在叢集上安裝 HDInsight 應用程式</span><span class="sxs-lookup"><span data-stu-id="7b013-269">Install HDInsight applications on clusters</span></span>

<span data-ttu-id="7b013-270">HDInsight 應用程式是使用者可以在以 Linux 為基礎的 HDInsight 叢集上安裝的應用程式。</span><span class="sxs-lookup"><span data-stu-id="7b013-270">An HDInsight application is an application that users can install on a Linux-based HDInsight cluster.</span></span> <span data-ttu-id="7b013-271">您可以使用由 Microsoft、協力廠商所提供或您自己開發的應用程式。</span><span class="sxs-lookup"><span data-stu-id="7b013-271">You can use applications provided by Microsoft, third parties, or that you develop yourself.</span></span> <span data-ttu-id="7b013-272">如需詳細資訊，請參閱[在 Azure HDInsight 上安裝第三方 Hadoop 應用程式](hdinsight-apps-install-applications.md)。</span><span class="sxs-lookup"><span data-stu-id="7b013-272">For more information, see [Install third-party Hadoop applications on Azure HDInsight](hdinsight-apps-install-applications.md).</span></span>

<span data-ttu-id="7b013-273">大部分的 hello HDInsight 應用程式會安裝空白邊緣節點上。</span><span class="sxs-lookup"><span data-stu-id="7b013-273">Most of hello HDInsight applications are installed on an empty edge node.</span></span>  <span data-ttu-id="7b013-274">空白邊緣節點是以相同的用戶端工具安裝並設定與 hello 前端節點的 hello 的 Linux 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="7b013-274">An empty edge node is a Linux virtual machine with hello same client tools installed and configured as in hello head node.</span></span> <span data-ttu-id="7b013-275">您可以使用 hello 邊緣節點存取 hello 叢集、 測試用戶端應用程式，以及裝載用戶端應用程式。</span><span class="sxs-lookup"><span data-stu-id="7b013-275">You can use hello edge node for accessing hello cluster, testing your client applications, and hosting your client applications.</span></span> <span data-ttu-id="7b013-276">如需詳細資訊，請參閱 [Use empty edge nodes in HDInsight (在 HDInsight 中使用空白的邊緣節點)](hdinsight-apps-use-edge-node.md)。</span><span class="sxs-lookup"><span data-stu-id="7b013-276">For more information, see [Use empty edge nodes in HDInsight](hdinsight-apps-use-edge-node.md).</span></span>

## <a name="advanced-settings-script-actions"></a><span data-ttu-id="7b013-277">進階設定：指令碼動作</span><span class="sxs-lookup"><span data-stu-id="7b013-277">Advanced settings: Script actions</span></span>

<span data-ttu-id="7b013-278">您可以在建立期間使用指令碼來安裝其他元件或自訂組態。</span><span class="sxs-lookup"><span data-stu-id="7b013-278">You can install additional components or customize cluster configuration by using scripts during creation.</span></span> <span data-ttu-id="7b013-279">這類指令碼會透過叫用**指令碼動作**，這是可以在 hello Azure 入口網站、 HDInsight Windows PowerShell cmdlet 或 hello HDInsight.NET SDK 中使用的組態選項。</span><span class="sxs-lookup"><span data-stu-id="7b013-279">Such scripts are invoked via **Script Action**, which is a configuration option that can be used from hello Azure portal, HDInsight Windows PowerShell cmdlets, or hello HDInsight .NET SDK.</span></span> <span data-ttu-id="7b013-280">如需詳細資訊，請參閱 [使用指令碼動作自訂 HDInsight 叢集](hdinsight-hadoop-customize-cluster-linux.md)。</span><span class="sxs-lookup"><span data-stu-id="7b013-280">For more information, see [Customize HDInsight cluster using Script Action](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

<span data-ttu-id="7b013-281">某些原生 Java 元件，例如砲象兵和 Cascading，可以在 hello 叢集上執行，以 Java 封存檔 (JAR) 檔案。</span><span class="sxs-lookup"><span data-stu-id="7b013-281">Some native Java components, like Mahout and Cascading, can be run on hello cluster as Java Archive (JAR) files.</span></span> <span data-ttu-id="7b013-282">這些 JAR 檔案可以是分散式的 tooAzure 儲存體，而且與 Hadoop 工作提交機制提交 tooHDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="7b013-282">These JAR files can be distributed tooAzure Storage and submitted tooHDInsight clusters with Hadoop job submission mechanisms.</span></span> <span data-ttu-id="7b013-283">如需詳細資訊，請參閱 [以程式設計方式提交 Hadoop 工作](hdinsight-submit-hadoop-jobs-programmatically.md)。</span><span class="sxs-lookup"><span data-stu-id="7b013-283">For more information, see [Submit Hadoop jobs programmatically](hdinsight-submit-hadoop-jobs-programmatically.md).</span></span>

> [!NOTE]
> <span data-ttu-id="7b013-284">如果您有問題部署 JAR 檔案 tooHDInsight 叢集，或呼叫 JAR 檔案，在 HDInsight 叢集，請連絡[Microsoft 支援服務](https://azure.microsoft.com/support/options/)。</span><span class="sxs-lookup"><span data-stu-id="7b013-284">If you have issues deploying JAR files tooHDInsight clusters, or calling JAR files on HDInsight clusters, contact [Microsoft Support](https://azure.microsoft.com/support/options/).</span></span>
>
> <span data-ttu-id="7b013-285">Cascading 不受 HDInsight 支援，而且不符合「Microsoft 支援」的資格。</span><span class="sxs-lookup"><span data-stu-id="7b013-285">Cascading is not supported by HDInsight and is not eligible for Microsoft Support.</span></span> <span data-ttu-id="7b013-286">支援的元件清單中，請參閱[hello 叢集版本 HDInsight 所提供的新](hdinsight-component-versioning.md)。</span><span class="sxs-lookup"><span data-stu-id="7b013-286">For lists of supported components, see [What's new in hello cluster versions provided by HDInsight](hdinsight-component-versioning.md).</span></span>
>
>

<span data-ttu-id="7b013-287">有時候，您需要下列組態檔案 hello 建立程序期間 tooconfigure hello:</span><span class="sxs-lookup"><span data-stu-id="7b013-287">Sometimes, you want tooconfigure hello following configuration files during hello creation process:</span></span>

* <span data-ttu-id="7b013-288">clusterIdentity.xml</span><span class="sxs-lookup"><span data-stu-id="7b013-288">clusterIdentity.xml</span></span>
* <span data-ttu-id="7b013-289">core-site.xml</span><span class="sxs-lookup"><span data-stu-id="7b013-289">core-site.xml</span></span>
* <span data-ttu-id="7b013-290">gateway.xml</span><span class="sxs-lookup"><span data-stu-id="7b013-290">gateway.xml</span></span>
* <span data-ttu-id="7b013-291">hbase-env.xml</span><span class="sxs-lookup"><span data-stu-id="7b013-291">hbase-env.xml</span></span>
* <span data-ttu-id="7b013-292">hbase-site.xml</span><span class="sxs-lookup"><span data-stu-id="7b013-292">hbase-site.xml</span></span>
* <span data-ttu-id="7b013-293">hdfs-site.xml</span><span class="sxs-lookup"><span data-stu-id="7b013-293">hdfs-site.xml</span></span>
* <span data-ttu-id="7b013-294">hive-env.xml</span><span class="sxs-lookup"><span data-stu-id="7b013-294">hive-env.xml</span></span>
* <span data-ttu-id="7b013-295">hive-site.xml</span><span class="sxs-lookup"><span data-stu-id="7b013-295">hive-site.xml</span></span>
* <span data-ttu-id="7b013-296">mapred-site</span><span class="sxs-lookup"><span data-stu-id="7b013-296">mapred-site</span></span>
* <span data-ttu-id="7b013-297">oozie-site.xml</span><span class="sxs-lookup"><span data-stu-id="7b013-297">oozie-site.xml</span></span>
* <span data-ttu-id="7b013-298">oozie-env.xml</span><span class="sxs-lookup"><span data-stu-id="7b013-298">oozie-env.xml</span></span>
* <span data-ttu-id="7b013-299">storm-site.xml</span><span class="sxs-lookup"><span data-stu-id="7b013-299">storm-site.xml</span></span>
* <span data-ttu-id="7b013-300">tez-site.xml</span><span class="sxs-lookup"><span data-stu-id="7b013-300">tez-site.xml</span></span>
* <span data-ttu-id="7b013-301">webhcat-site.xml</span><span class="sxs-lookup"><span data-stu-id="7b013-301">webhcat-site.xml</span></span>
* <span data-ttu-id="7b013-302">yarn-site.xml</span><span class="sxs-lookup"><span data-stu-id="7b013-302">yarn-site.xml</span></span>

<span data-ttu-id="7b013-303">如需詳細資訊，請參閱 [使用 Bootstrap 自訂 HDInsight 叢集](hdinsight-hadoop-customize-cluster-bootstrap.md)。</span><span class="sxs-lookup"><span data-stu-id="7b013-303">For more information, see [Customize HDInsight clusters using Bootstrap](hdinsight-hadoop-customize-cluster-bootstrap.md).</span></span>

## <a name="advanced-settings-extend-clusters-with-a-virtual-network"></a><span data-ttu-id="7b013-304">進階設定：使用虛擬網路擴充叢集</span><span class="sxs-lookup"><span data-stu-id="7b013-304">Advanced settings: Extend clusters with a virtual network</span></span>
<span data-ttu-id="7b013-305">如果您的方案要求分散到多個的 HDInsight 叢集類型的技術[Azure 虛擬網路](https://docs.microsoft.com/azure/virtual-network)可以連接所需的 hello 叢集類型。</span><span class="sxs-lookup"><span data-stu-id="7b013-305">If your solution requires technologies that are spread across multiple HDInsight cluster types, an [Azure virtual network](https://docs.microsoft.com/azure/virtual-network) can connect hello required cluster types.</span></span> <span data-ttu-id="7b013-306">此設定可讓 hello 叢集，以及部署 toothem 任何程式碼，toodirectly 彼此通訊。</span><span class="sxs-lookup"><span data-stu-id="7b013-306">This configuration allows hello clusters, and any code you deploy toothem, toodirectly communicate with each other.</span></span>

<span data-ttu-id="7b013-307">如需如何搭配使用 Azure 虛擬網路與 HDInsight 的詳細資訊，請參閱[使用 Azure 虛擬網路擴充 HDInsight](hdinsight-extend-hadoop-virtual-network.md)。</span><span class="sxs-lookup"><span data-stu-id="7b013-307">For more information on using an Azure virtual network with HDInsight, see [Extend HDInsight with Azure virtual networks](hdinsight-extend-hadoop-virtual-network.md).</span></span>

<span data-ttu-id="7b013-308">如需在 Azure 虛擬網路內使用兩個叢集類型的範例，請參閱[使用 Storm 和 HBase 分析感應器資料](hdinsight-storm-sensor-data-analysis.md)。</span><span class="sxs-lookup"><span data-stu-id="7b013-308">For an example of using two cluster types within an Azure virtual network, see [Analyze sensor data with Storm and HBase](hdinsight-storm-sensor-data-analysis.md).</span></span> <span data-ttu-id="7b013-309">如需有關使用 HDInsight 與虛擬網路，包括特定組態需求的 hello 虛擬網路，請參閱[擴充 HDInsight 功能，方法是使用 Azure 虛擬網路](hdinsight-extend-hadoop-virtual-network.md)。</span><span class="sxs-lookup"><span data-stu-id="7b013-309">For more information about using HDInsight with a virtual network, including specific configuration requirements for hello virtual network, see [Extend HDInsight capabilities by using Azure Virtual Network](hdinsight-extend-hadoop-virtual-network.md).</span></span>

## <a name="troubleshoot-access-control-issues"></a><span data-ttu-id="7b013-310">針對存取控制問題進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="7b013-310">Troubleshoot access control issues</span></span>

<span data-ttu-id="7b013-311">如果您在建立 HDInsight 叢集時遇到問題，請參閱[存取控制需求](hdinsight-administer-use-portal-linux.md#create-clusters)。</span><span class="sxs-lookup"><span data-stu-id="7b013-311">If you run into issues with creating HDInsight clusters, see [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>

## <a name="next-steps"></a><span data-ttu-id="7b013-312">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7b013-312">Next steps</span></span>

- [<span data-ttu-id="7b013-313">HDInsight、 hello Hadoop 生態系統和 Hadoop 叢集為何？</span><span class="sxs-lookup"><span data-stu-id="7b013-313">What are HDInsight, hello Hadoop ecosystem, and Hadoop clusters?</span></span>](hdinsight-hadoop-introduction.md)
- [<span data-ttu-id="7b013-314">開始在 HDInsight 中使用 Hadoop</span><span class="sxs-lookup"><span data-stu-id="7b013-314">Get started using Hadoop in HDInsight</span></span>](hdinsight-hadoop-linux-tutorial-get-started.md)
- [<span data-ttu-id="7b013-315">從 Windows PC 在 HDInsight 上的 Hadoop 中作業</span><span class="sxs-lookup"><span data-stu-id="7b013-315">Work in Hadoop on HDInsight from a Windows PC</span></span>](hdinsight-hadoop-windows-tools.md)
