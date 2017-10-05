---
title: "Hadoop、Spark、Kafka、HBase 或 R Server 的叢集設定 - Azure HDInsight | Microsoft Docs"
description: "從瀏覽器、Azure CLI、Azure PowerShell、REST 或 SDK 設定 HDInsight 的 Hadoop、Kafka、Spark、HBase、R 伺服器或 Storm 叢集。"
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
ms.openlocfilehash: 473d71672cadb1d23f5942cb70294d213a8bbbca
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="set-up-clusters-in-hdinsight-with-hadoop-spark-kafka-and-more"></a><span data-ttu-id="9a832-104">使用 Hadoop、Spark 及 Kafka 等在 HDInsight 中設定叢集</span><span class="sxs-lookup"><span data-stu-id="9a832-104">Set up clusters in HDInsight with Hadoop, Spark, Kafka, and more</span></span>

[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

<span data-ttu-id="9a832-105">了解如何在 HDInsight 中使用 Hadoop、Spark、Kafka、Interactive Hive、HBase、R 伺服器或 Storm 安裝並設定叢集。</span><span class="sxs-lookup"><span data-stu-id="9a832-105">Learn how to set up and configure clusters in HDInsight with Hadoop, Spark, Kafka, Interactive Hive, HBase, R Server, or Storm.</span></span> <span data-ttu-id="9a832-106">此外，了解如何自訂叢集，並將叢集加入網域以提升安全性。</span><span class="sxs-lookup"><span data-stu-id="9a832-106">Also, learn how to customize clusters and add security by joining them to a domain.</span></span>

<span data-ttu-id="9a832-107">Hadoop 叢集由數個虛擬機器 (節點) 組成，可用於分散處理作業。</span><span class="sxs-lookup"><span data-stu-id="9a832-107">A Hadoop cluster consists of several virtual machines (nodes) that are used for distributed processing of tasks.</span></span> <span data-ttu-id="9a832-108">Azure HDInsight 會處理個別節點所安裝和設定的實作細節，您只需要提供一般設定資訊即可。</span><span class="sxs-lookup"><span data-stu-id="9a832-108">Azure HDInsight handles implementation details of installation and configuration of individual nodes, so you only have to provide general configuration information.</span></span> 

> [!IMPORTANT]
><span data-ttu-id="9a832-109">HDInsight 叢集的計費起自叢集建立時，終至叢集刪除時。</span><span class="sxs-lookup"><span data-stu-id="9a832-109">HDInsight cluster billing starts once a cluster is created and stops when the cluster is deleted.</span></span> <span data-ttu-id="9a832-110">計費是以每分鐘按比例計算，因此不再使用時，請一律刪除您的叢集。</span><span class="sxs-lookup"><span data-stu-id="9a832-110">Billing is pro-rated per minute, so you should always delete your cluster when it is no longer in use.</span></span> <span data-ttu-id="9a832-111">了解如何[刪除叢集。](hdinsight-delete-cluster.md)</span><span class="sxs-lookup"><span data-stu-id="9a832-111">Learn how to [delete a cluster.](hdinsight-delete-cluster.md)</span></span>
>

## <a name="cluster-setup-methods"></a><span data-ttu-id="9a832-112">叢集設定方法</span><span class="sxs-lookup"><span data-stu-id="9a832-112">Cluster setup methods</span></span>
<span data-ttu-id="9a832-113">下表顯示可用來設定 HDInsight 叢集的不同方法。</span><span class="sxs-lookup"><span data-stu-id="9a832-113">The following table shows the different methods you can use to set up an HDInsight cluster.</span></span>

| <span data-ttu-id="9a832-114">叢集建立方法</span><span class="sxs-lookup"><span data-stu-id="9a832-114">Clusters created with</span></span> | <span data-ttu-id="9a832-115">Web 瀏覽器</span><span class="sxs-lookup"><span data-stu-id="9a832-115">Web browser</span></span> | <span data-ttu-id="9a832-116">命令列</span><span class="sxs-lookup"><span data-stu-id="9a832-116">Command line</span></span> | <span data-ttu-id="9a832-117">REST API</span><span class="sxs-lookup"><span data-stu-id="9a832-117">REST API</span></span> | <span data-ttu-id="9a832-118">SDK</span><span class="sxs-lookup"><span data-stu-id="9a832-118">SDK</span></span> | 
| --- |:---:|:---:|:---:|:---:|
| [<span data-ttu-id="9a832-119">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="9a832-119">Azure portal</span></span>](hdinsight-hadoop-create-linux-clusters-portal.md) |<span data-ttu-id="9a832-120">✔</span><span class="sxs-lookup"><span data-stu-id="9a832-120">✔</span></span> |&nbsp; |&nbsp; |&nbsp; |
| [<span data-ttu-id="9a832-121">Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="9a832-121">Azure Data Factory</span></span>](hdinsight-hadoop-create-linux-clusters-adf.md) |<span data-ttu-id="9a832-122">✔</span><span class="sxs-lookup"><span data-stu-id="9a832-122">✔</span></span> |<span data-ttu-id="9a832-123">✔</span><span class="sxs-lookup"><span data-stu-id="9a832-123">✔</span></span> |<span data-ttu-id="9a832-124">✔</span><span class="sxs-lookup"><span data-stu-id="9a832-124">✔</span></span> |<span data-ttu-id="9a832-125">✔</span><span class="sxs-lookup"><span data-stu-id="9a832-125">✔</span></span> |
| [<span data-ttu-id="9a832-126">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="9a832-126">Azure CLI</span></span>](hdinsight-hadoop-create-linux-clusters-azure-cli.md) |&nbsp; |<span data-ttu-id="9a832-127">✔</span><span class="sxs-lookup"><span data-stu-id="9a832-127">✔</span></span> |&nbsp; |&nbsp; |
| [<span data-ttu-id="9a832-128">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="9a832-128">Azure PowerShell</span></span>](hdinsight-hadoop-create-linux-clusters-azure-powershell.md) |&nbsp; |<span data-ttu-id="9a832-129">✔</span><span class="sxs-lookup"><span data-stu-id="9a832-129">✔</span></span> |&nbsp; |&nbsp; |
| [<span data-ttu-id="9a832-130">cURL</span><span class="sxs-lookup"><span data-stu-id="9a832-130">cURL</span></span>](hdinsight-hadoop-create-linux-clusters-curl-rest.md) |&nbsp; |<span data-ttu-id="9a832-131">✔</span><span class="sxs-lookup"><span data-stu-id="9a832-131">✔</span></span> |<span data-ttu-id="9a832-132">✔</span><span class="sxs-lookup"><span data-stu-id="9a832-132">✔</span></span> |&nbsp; |
| [<span data-ttu-id="9a832-133">.NET SDK</span><span class="sxs-lookup"><span data-stu-id="9a832-133">.NET SDK</span></span>](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md) |&nbsp; |&nbsp; |&nbsp; |<span data-ttu-id="9a832-134">✔</span><span class="sxs-lookup"><span data-stu-id="9a832-134">✔</span></span> |
| [<span data-ttu-id="9a832-135">Azure 資源管理員範本</span><span class="sxs-lookup"><span data-stu-id="9a832-135">Azure Resource Manager templates</span></span>](hdinsight-hadoop-create-linux-clusters-arm-templates.md) |&nbsp; |<span data-ttu-id="9a832-136">✔</span><span class="sxs-lookup"><span data-stu-id="9a832-136">✔</span></span> |&nbsp; |&nbsp; |

## <a name="quick-create-basic-cluster-setup"></a><span data-ttu-id="9a832-137">快速建立：基本的叢集設定</span><span class="sxs-lookup"><span data-stu-id="9a832-137">Quick create: Basic cluster setup</span></span>
<span data-ttu-id="9a832-138">本文會逐步引導您完成 [Azure 入口網站](https://portal.azure.com)中的設定，您可以在此入口網站中使用 [Quick create] \(快速建立\) 或 [Custom] \(自訂\) 建立 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="9a832-138">This article walks you through setup in the [Azure portal](https://portal.azure.com), where you can create an HDInsight cluster using *Quick create* or *Custom*.</span></span> 

<span data-ttu-id="9a832-139">依照畫面上指示執行基本的叢集設定。</span><span class="sxs-lookup"><span data-stu-id="9a832-139">Follow instructions on the screen to do a basic cluster setup.</span></span> <span data-ttu-id="9a832-140">以下是下列各項的詳細資訊：</span><span class="sxs-lookup"><span data-stu-id="9a832-140">Details are provided below for:</span></span>

* [<span data-ttu-id="9a832-141">資源群組名稱</span><span class="sxs-lookup"><span data-stu-id="9a832-141">Resource group name</span></span>](#resource-group-name)
* [<span data-ttu-id="9a832-142">叢集類型和設定</span><span class="sxs-lookup"><span data-stu-id="9a832-142">Cluster types and configuration</span></span>](#cluster-types) 
* [<span data-ttu-id="9a832-143">叢集登入和 SSH 使用者名稱</span><span class="sxs-lookup"><span data-stu-id="9a832-143">Cluster login and SSH username</span></span>](#cluster-login-and-ssh-username)
* [<span data-ttu-id="9a832-144">位置</span><span class="sxs-lookup"><span data-stu-id="9a832-144">Location</span></span>](#location)

> [!IMPORTANT]
> <span data-ttu-id="9a832-145">Linux 是唯一使用於 HDInsight 3.4 版或更新版本的作業系統。</span><span class="sxs-lookup"><span data-stu-id="9a832-145">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="9a832-146">如需詳細資訊，請參閱 [HDInsight 3.3 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。</span><span class="sxs-lookup"><span data-stu-id="9a832-146">For more information, see [HDInsight 3.3 retirement](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>
>

## <a name="resource-group-name"></a><span data-ttu-id="9a832-147">資源群組名稱</span><span class="sxs-lookup"><span data-stu-id="9a832-147">Resource group name</span></span> 

<span data-ttu-id="9a832-148">[Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) 可協助您將應用程式中的資源做為群組使用，稱為 Azure 資源群組。</span><span class="sxs-lookup"><span data-stu-id="9a832-148">[Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) helps you work with the resources in your application as a group, referred to as an Azure resource group.</span></span> <span data-ttu-id="9a832-149">您可以在單一、協調的作業中，將應用程式的所有資源進行部署、更新、監視或刪除。</span><span class="sxs-lookup"><span data-stu-id="9a832-149">You can deploy, update, monitor, or delete all the resources for your application in a single coordinated operation.</span></span>

## <span data-ttu-id="9a832-150"><a name="cluster-types"></a>叢集類型和設定</span><span class="sxs-lookup"><span data-stu-id="9a832-150"><a name="cluster-types"></a> Cluster types and configuration</span></span>
<span data-ttu-id="9a832-151">Azure HDInsight 目前提供下列的叢集類型，每種都有一組提供特定功能的元件。</span><span class="sxs-lookup"><span data-stu-id="9a832-151">Azure HDInsight currently provides the following cluster types, each with a set of components to provide certain functionalities.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9a832-152">HDInsight 叢集有多種類型，每種類型各適合單一工作負載或技術。</span><span class="sxs-lookup"><span data-stu-id="9a832-152">HDInsight clusters are available in various types, each for a single workload or technology.</span></span> <span data-ttu-id="9a832-153">沒有任何支援方法可建立結合多個類型的叢集，例如在一個叢集上並存 Storm 和 HBase。</span><span class="sxs-lookup"><span data-stu-id="9a832-153">There is no supported method to create a cluster that combines multiple types, such as Storm and HBase on one cluster.</span></span> <span data-ttu-id="9a832-154">如果您的解決方案需要會分散到多個 HDInsight 叢集類型的技術，[Azure 虛擬網路](https://docs.microsoft.com/azure/virtual-network)可以連接必要的叢集類型。</span><span class="sxs-lookup"><span data-stu-id="9a832-154">If your solution requires technologies that are spread across multiple HDInsight cluster types, an [Azure virtual network](https://docs.microsoft.com/azure/virtual-network) can connect the required cluster types.</span></span> 
>
>

| <span data-ttu-id="9a832-155">叢集類型</span><span class="sxs-lookup"><span data-stu-id="9a832-155">Cluster type</span></span> | <span data-ttu-id="9a832-156">功能</span><span class="sxs-lookup"><span data-stu-id="9a832-156">Functionality</span></span> |
| --- | --- |
| [<span data-ttu-id="9a832-157">Hadoop</span><span class="sxs-lookup"><span data-stu-id="9a832-157">Hadoop</span></span>](hdinsight-hadoop-introduction.md) |<span data-ttu-id="9a832-158">批次查詢和分析儲存的資料</span><span class="sxs-lookup"><span data-stu-id="9a832-158">Batch query and analysis of stored data</span></span> |
| [<span data-ttu-id="9a832-159">HBase</span><span class="sxs-lookup"><span data-stu-id="9a832-159">HBase</span></span>](hdinsight-hbase-overview.md) |<span data-ttu-id="9a832-160">處理大量無綱要的 NoSQL 資料</span><span class="sxs-lookup"><span data-stu-id="9a832-160">Processing for large amounts of schemaless, NoSQL data</span></span> |
| [<span data-ttu-id="9a832-161">Storm</span><span class="sxs-lookup"><span data-stu-id="9a832-161">Storm</span></span>](hdinsight-storm-overview.md) |<span data-ttu-id="9a832-162">即時事件處理</span><span class="sxs-lookup"><span data-stu-id="9a832-162">Real-time event processing</span></span> |
| [<span data-ttu-id="9a832-163">Spark</span><span class="sxs-lookup"><span data-stu-id="9a832-163">Spark</span></span>](hdinsight-apache-spark-overview.md) |<span data-ttu-id="9a832-164">記憶體內處理、互動式查詢、微批次串流處理</span><span class="sxs-lookup"><span data-stu-id="9a832-164">In-memory processing, interactive queries, micro-batch stream processing</span></span> |
| [<span data-ttu-id="9a832-165">Kafka (預覽)</span><span class="sxs-lookup"><span data-stu-id="9a832-165">Kafka (Preview)</span></span>](hdinsight-apache-kafka-introduction.md) | <span data-ttu-id="9a832-166">可用來建置即時串流資料管線和應用程式的分散式串流平台</span><span class="sxs-lookup"><span data-stu-id="9a832-166">A distributed streaming platform that can be used to build real-time streaming data pipelines and applications</span></span> |
| [<span data-ttu-id="9a832-167">R 伺服器</span><span class="sxs-lookup"><span data-stu-id="9a832-167">R Server</span></span>](hdinsight-hadoop-r-server-overview.md) |<span data-ttu-id="9a832-168">各種巨量資料統計資料、預測模型和機器學習功能</span><span class="sxs-lookup"><span data-stu-id="9a832-168">Various big data statistics, predictive modeling, and machine learning capabilities</span></span> |
| [<span data-ttu-id="9a832-169">互動式 Hive (預覽)</span><span class="sxs-lookup"><span data-stu-id="9a832-169">Interactive Hive (Preview)</span></span>](hdinsight-hadoop-use-interactive-hive.md) |<span data-ttu-id="9a832-170">更快速之互動式 Hive 查詢的記憶體內快取</span><span class="sxs-lookup"><span data-stu-id="9a832-170">In-memory caching for interactive and faster Hive queries</span></span> |

### <a name="number-of-nodes-for-each-cluster-type"></a><span data-ttu-id="9a832-171">每個叢集類型的節點數目</span><span class="sxs-lookup"><span data-stu-id="9a832-171">Number of nodes for each cluster type</span></span>
<span data-ttu-id="9a832-172">每個叢集類型都有自己的節點數目、節點術語和預設 VM 大小。</span><span class="sxs-lookup"><span data-stu-id="9a832-172">Each cluster type has its own number of nodes, terminology for nodes, and default VM size.</span></span> <span data-ttu-id="9a832-173">下表中各節點類型的節點數目位於括號中。</span><span class="sxs-lookup"><span data-stu-id="9a832-173">In the following table, the number of nodes for each node type is in parentheses.</span></span>

| <span data-ttu-id="9a832-174">類型</span><span class="sxs-lookup"><span data-stu-id="9a832-174">Type</span></span> | <span data-ttu-id="9a832-175">節點</span><span class="sxs-lookup"><span data-stu-id="9a832-175">Nodes</span></span> | <span data-ttu-id="9a832-176">圖表</span><span class="sxs-lookup"><span data-stu-id="9a832-176">Diagram</span></span> |
| --- | --- | --- |
| <span data-ttu-id="9a832-177">Hadoop</span><span class="sxs-lookup"><span data-stu-id="9a832-177">Hadoop</span></span> |<span data-ttu-id="9a832-178">前端節點 (2)、資料節點 (1+)</span><span class="sxs-lookup"><span data-stu-id="9a832-178">Head node (2), data node (1+)</span></span> |![HDInsight Hadoop 叢集節點](./media/hdinsight-hadoop-provision-linux-clusters/hdinsight-hadoop-cluster-type-nodes.png) |
| <span data-ttu-id="9a832-180">HBase</span><span class="sxs-lookup"><span data-stu-id="9a832-180">HBase</span></span> |<span data-ttu-id="9a832-181">前端伺服器 (2)、區域伺服器 (1+)、主要/Zookeeper 節點 (3)</span><span class="sxs-lookup"><span data-stu-id="9a832-181">Head server (2), region server (1+), master/ZooKeeper node (3)</span></span> |![HDInsight HBase 叢集節點](./media/hdinsight-hadoop-provision-linux-clusters/hdinsight-hbase-cluster-type-setup.png) |
| <span data-ttu-id="9a832-183">Storm</span><span class="sxs-lookup"><span data-stu-id="9a832-183">Storm</span></span> |<span data-ttu-id="9a832-184">Nimbus 節點 (2)、監督員伺服器 (1+)、Zookeeper 節點 (3)</span><span class="sxs-lookup"><span data-stu-id="9a832-184">Nimbus node (2), supervisor server (1+), ZooKeeper node (3)</span></span> |![HDInsight Storm 叢集節點](./media/hdinsight-hadoop-provision-linux-clusters/hdinsight-storm-cluster-type-setup.png) |
| <span data-ttu-id="9a832-186">Spark</span><span class="sxs-lookup"><span data-stu-id="9a832-186">Spark</span></span> |<span data-ttu-id="9a832-187">前端節點 (2)、背景工作角色節點 (1+)、Zookeeper 節點 (3) (A1 Zookeeper VM 大小不限)</span><span class="sxs-lookup"><span data-stu-id="9a832-187">Head node (2), worker node (1+), ZooKeeper node (3) (free for A1 ZooKeeper VM size)</span></span> |![HDInsight Spark 叢集節點](./media/hdinsight-hadoop-provision-linux-clusters/hdinsight-spark-cluster-type-setup.png) |

<span data-ttu-id="9a832-189">如需詳細資訊，請參閱＜HDInsight 中的 Hadoop 元件和版本是什麼？＞中的[叢集的預設節點設定和虛擬機器大小](hdinsight-component-versioning.md#default-node-configuration-and-virtual-machine-sizes-for-clusters)。</span><span class="sxs-lookup"><span data-stu-id="9a832-189">For more information, see [Default node configuration and virtual machine sizes for clusters](hdinsight-component-versioning.md#default-node-configuration-and-virtual-machine-sizes-for-clusters) in "What are the Hadoop components and versions in HDInsight?"</span></span>

### <a name="hdinsight-version"></a><span data-ttu-id="9a832-190">HDInsight 版本</span><span class="sxs-lookup"><span data-stu-id="9a832-190">HDInsight version</span></span>
<span data-ttu-id="9a832-191">選擇此叢集的 HDInsight 版本。</span><span class="sxs-lookup"><span data-stu-id="9a832-191">Choose the version of HDInsight for this cluster.</span></span> <span data-ttu-id="9a832-192">如需詳細資訊，請參閱[支援的 HDInsight 版本](hdinsight-component-versioning.md#supported-hdinsight-versions)。</span><span class="sxs-lookup"><span data-stu-id="9a832-192">For more information, see [Supported HDInsight versions](hdinsight-component-versioning.md#supported-hdinsight-versions).</span></span>

### <span data-ttu-id="9a832-193"><a name="cluster-tiers"></a>叢集層：HDInsight 服務層</span><span class="sxs-lookup"><span data-stu-id="9a832-193"><a name="cluster-tiers"></a>Cluster tier: HDInsight service tiers</span></span>

<span data-ttu-id="9a832-194">Azure HDInsight 提供兩種服務層的巨量資料雲端提供項目：Standard 和 Premium。</span><span class="sxs-lookup"><span data-stu-id="9a832-194">Azure HDInsight provides the big data cloud offerings in two service tiers: Standard and Premium.</span></span>  <span data-ttu-id="9a832-195">如需詳細資訊，請參閱 [HDInsight Standard 和 HDInsight Premium](hdinsight-component-versioning.md#hdinsight-standard-and-hdinsight-premium)。</span><span class="sxs-lookup"><span data-stu-id="9a832-195">For more information, see [HDInsight Standard and HDInsight Premium](hdinsight-component-versioning.md#hdinsight-standard-and-hdinsight-premium).</span></span>

<span data-ttu-id="9a832-196">以下螢幕擷取畫面顯示選擇叢集類型的 Azure 入口網站資訊。</span><span class="sxs-lookup"><span data-stu-id="9a832-196">The following screenshot shows the Azure portal information for choosing cluster types.</span></span>

![HDInsight 進階組態](./media/hdinsight-hadoop-provision-linux-clusters/hdinsight-cluster-type-configuration.png)


## <a name="cluster-login-and-ssh-user-name"></a><span data-ttu-id="9a832-198">叢集登入和 SSH 使用者名稱</span><span class="sxs-lookup"><span data-stu-id="9a832-198">Cluster login and SSH user name</span></span>
<span data-ttu-id="9a832-199">使用 HDInsight 叢集，您可以在建立叢集期間設定兩個使用者帳戶：</span><span class="sxs-lookup"><span data-stu-id="9a832-199">With HDInsight clusters, you can configure two user accounts during cluster creation:</span></span>

* <span data-ttu-id="9a832-200">HTTP 使用者：預設使用者名稱為 *admin*。</span><span class="sxs-lookup"><span data-stu-id="9a832-200">HTTP user: The default user name is *admin*.</span></span> <span data-ttu-id="9a832-201">使用 Azure 入口網站上的基本組態。</span><span class="sxs-lookup"><span data-stu-id="9a832-201">It uses the basic configuration on the Azure portal.</span></span> <span data-ttu-id="9a832-202">有時稱之為「叢集使用者」。</span><span class="sxs-lookup"><span data-stu-id="9a832-202">Sometimes it is called "Cluster user."</span></span>
* <span data-ttu-id="9a832-203">SSH 使用者 (Linux 叢集)：用來透過 SSH 連線到叢集。</span><span class="sxs-lookup"><span data-stu-id="9a832-203">SSH user (Linux clusters): Used to connect to the cluster through SSH.</span></span> <span data-ttu-id="9a832-204">如需詳細資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。</span><span class="sxs-lookup"><span data-stu-id="9a832-204">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

## <span data-ttu-id="9a832-205"><a name="location"></a>叢集與儲存體的位置 (區域)</span><span class="sxs-lookup"><span data-stu-id="9a832-205"><a name="location"></a>Location (regions) for clusters and storage</span></span>

<span data-ttu-id="9a832-206">不需明確指定叢集位置：叢集位於和預設儲存體相同的位置。</span><span class="sxs-lookup"><span data-stu-id="9a832-206">You don't need to specify the cluster location explicitly: The cluster is in the same location as the default storage.</span></span> <span data-ttu-id="9a832-207">如需支援的區域清單，請按一下 [HDInsight 價格](https://go.microsoft.com/fwLink/?LinkID=282635&clcid=0x409)中的 [區域] 下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="9a832-207">For a list of supported regions, click the **Region** drop-down list on [HDInsight pricing](https://go.microsoft.com/fwLink/?LinkID=282635&clcid=0x409).</span></span>

## <a name="storage-endpoints-for-clusters"></a><span data-ttu-id="9a832-208">叢集的儲存體端點</span><span class="sxs-lookup"><span data-stu-id="9a832-208">Storage endpoints for clusters</span></span>

<span data-ttu-id="9a832-209">內部部署安裝的 Hadoop 叢集使用 Hadoop 分散式檔案系統 (HDFS) 作為叢集上的儲存體，但在雲端中，您可以使用已連接到叢集的儲存體端點。</span><span class="sxs-lookup"><span data-stu-id="9a832-209">Although an on-premises installation of Hadoop uses the Hadoop Distributed File System (HDFS) for storage on the cluster, in the cloud you use storage endpoints connected to cluster.</span></span> <span data-ttu-id="9a832-210">HDInsight 叢集會使用 [Azure Data Lake Store](hdinsight-hadoop-use-data-lake-store.md) 或 [Azure 儲存體中的 Blob](hdinsight-hadoop-use-blob-storage.md)。</span><span class="sxs-lookup"><span data-stu-id="9a832-210">HDInsight clusters use either [Azure Data Lake Store](hdinsight-hadoop-use-data-lake-store.md) or [blobs in Azure Storage](hdinsight-hadoop-use-blob-storage.md).</span></span> <span data-ttu-id="9a832-211">使用 Azure 儲存體或 Data Lake Store 表示您可以放心地刪除用於計算的 HDInsight 叢集，但您的資料仍會留存。</span><span class="sxs-lookup"><span data-stu-id="9a832-211">Using Azure Storage or Data Lake Store means you can safely delete the HDInsight clusters used for computation while still retaining your data.</span></span> 

> [!WARNING]
> <span data-ttu-id="9a832-212">不支援在與 HDInsight 叢集不同的位置中使用其他儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="9a832-212">Using an additional storage account in a different location from the HDInsight cluster is not supported.</span></span>

<span data-ttu-id="9a832-213">在設定期間，您要為預設儲存體端點指定 Azure 儲存體帳戶的 Blob 容器或 Data Lake Store。</span><span class="sxs-lookup"><span data-stu-id="9a832-213">During configuration, for the default storage endpoint you specify a blob container of an Azure Storage account or a Data Lake Store.</span></span> <span data-ttu-id="9a832-214">預設儲存體包含應用程式與系統記錄檔。</span><span class="sxs-lookup"><span data-stu-id="9a832-214">The default storage contains application and system logs.</span></span> <span data-ttu-id="9a832-215">您也可以選擇指定叢集可存取的其他已連結 Azure 儲存體帳戶和 Data Lake Store 帳戶。</span><span class="sxs-lookup"><span data-stu-id="9a832-215">Optionally, you can specify additional linked Azure Storage accounts and Data Lake Store accounts that the cluster can access.</span></span> <span data-ttu-id="9a832-216">HDInsight 叢集與相依的儲存體帳戶必須位於相同的 Azure 位置。</span><span class="sxs-lookup"><span data-stu-id="9a832-216">The HDInsight cluster and the dependent storage accounts must be in the same Azure location.</span></span>

![叢集儲存體設定：HDFS 相容的儲存體端點](./media/hdinsight-hadoop-provision-linux-clusters/hdinsight-cluster-creation-storage.png)

[!INCLUDE [secure-transfer-enabled-storage-account](../../includes/hdinsight-secure-transfer.md)]


### <a name="optional-metastores"></a><span data-ttu-id="9a832-218">選擇性中繼存放區</span><span class="sxs-lookup"><span data-stu-id="9a832-218">Optional metastores</span></span>
<span data-ttu-id="9a832-219">您可以建立選擇性的 Hive 或 Oozie 中繼存放區。</span><span class="sxs-lookup"><span data-stu-id="9a832-219">You can create optional Hive or Oozie metastores.</span></span> <span data-ttu-id="9a832-220">不過，並非所有叢集類型都支援中繼存放區，且 Azure SQL 資料倉儲不相容於中繼存放區。</span><span class="sxs-lookup"><span data-stu-id="9a832-220">However, not all cluster types support metastores, and Azure SQL Data Warehouse isn't compatible with metastores.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="9a832-221">在建立自訂中繼存放區時，資料庫名稱請勿使用破折號、連字號或空格。</span><span class="sxs-lookup"><span data-stu-id="9a832-221">When you create a custom metastore, don't use dashes, hyphens, or spaces in the database name.</span></span> <span data-ttu-id="9a832-222">這可能會導致叢集建立程序失敗。</span><span class="sxs-lookup"><span data-stu-id="9a832-222">This can cause the cluster creation process to fail.</span></span>

### <span data-ttu-id="9a832-223"><a name="use-hiveoozie-metastore"></a>Hive 中繼存放區</span><span class="sxs-lookup"><span data-stu-id="9a832-223"><a name="use-hiveoozie-metastore"></a>Hive metastore</span></span>

<span data-ttu-id="9a832-224">如果想要在刪除 HDInsight 叢集之後保留 Hive 資料表，請使用自訂的中繼存放區。</span><span class="sxs-lookup"><span data-stu-id="9a832-224">If you want to retain your Hive tables after you delete an HDInsight cluster, use a custom metastore.</span></span> <span data-ttu-id="9a832-225">您可以接著將中繼存放區附加至另一個 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="9a832-225">You can then attach the metastore to another HDInsight cluster.</span></span>

<span data-ttu-id="9a832-226">針對某個 HDInsight 叢集版本建立的 HDInsight 中繼存放區，不能在不同的 HDInsight 叢集版本之間共用。</span><span class="sxs-lookup"><span data-stu-id="9a832-226">An HDInsight metastore that is created for one HDInsight cluster version cannot be shared across different HDInsight cluster versions.</span></span> <span data-ttu-id="9a832-227">如需 HDInsight 版本清單，請參閱[支援的 HDInsight 版本](hdinsight-component-versioning.md#supported-hdinsight-versions)。</span><span class="sxs-lookup"><span data-stu-id="9a832-227">For a list of HDInsight versions, see [Supported HDInsight versions](hdinsight-component-versioning.md#supported-hdinsight-versions).</span></span>

### <a name="oozie-metastore"></a><span data-ttu-id="9a832-228">Oozie 中繼存放區</span><span class="sxs-lookup"><span data-stu-id="9a832-228">Oozie metastore</span></span>

<span data-ttu-id="9a832-229">為提升使用 Oozie 時的效能，請使用自訂的中繼存放區。</span><span class="sxs-lookup"><span data-stu-id="9a832-229">To increase performance when using Oozie, use a custom metastore.</span></span> <span data-ttu-id="9a832-230">在您刪除叢集後，中繼存放區也可提供 Oozie 作業資料的存取。</span><span class="sxs-lookup"><span data-stu-id="9a832-230">A metastore can also provide access to Oozie job data after you delete your cluster.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="9a832-231">您無法重複使用自訂的 Oozie 中繼存放區。</span><span class="sxs-lookup"><span data-stu-id="9a832-231">You cannot reuse a custom Oozie metastore.</span></span> <span data-ttu-id="9a832-232">若要使用自訂的 Oozie 中繼存放區，您必須在建立 HDInsight 叢集時提供空的 Azure SQL Database。</span><span class="sxs-lookup"><span data-stu-id="9a832-232">To use a custom Oozie metastore, you must provide an empty Azure SQL Database when creating the HDInsight cluster.</span></span>

## <a name="configure-cluster-size"></a><span data-ttu-id="9a832-233">設定叢集大小</span><span class="sxs-lookup"><span data-stu-id="9a832-233">Configure cluster size</span></span>

<span data-ttu-id="9a832-234">只要叢集存在，就會針對您的節點使用量收費。</span><span class="sxs-lookup"><span data-stu-id="9a832-234">You are billed for node usage for as long as the cluster exists.</span></span> <span data-ttu-id="9a832-235">建立叢集後就開始計費，並在叢集刪除後停止計費。</span><span class="sxs-lookup"><span data-stu-id="9a832-235">Billing starts when a cluster is created and stops when the cluster is deleted.</span></span> <span data-ttu-id="9a832-236">無法取消配置或保留叢集。</span><span class="sxs-lookup"><span data-stu-id="9a832-236">Clusters can’t be de-allocated or put on hold.</span></span>

<span data-ttu-id="9a832-237">HDInsight 叢集的成本是由節點數和節點的虛擬機器大小來決定。</span><span class="sxs-lookup"><span data-stu-id="9a832-237">The cost of HDInsight clusters is determined by the number of nodes and the virtual machines sizes for the nodes.</span></span> 

<span data-ttu-id="9a832-238">不同的叢集類型具有不同的節點類型、節點數目和節點大小：</span><span class="sxs-lookup"><span data-stu-id="9a832-238">Different cluster types have different node types, numbers of nodes, and node sizes:</span></span>
* <span data-ttu-id="9a832-239">Hadoop 叢集類型的預設值：</span><span class="sxs-lookup"><span data-stu-id="9a832-239">Hadoop cluster type default:</span></span> 
    * <span data-ttu-id="9a832-240">兩個*前端節點*</span><span class="sxs-lookup"><span data-stu-id="9a832-240">Two *head nodes*</span></span>  
    * <span data-ttu-id="9a832-241">四個*資料節點*</span><span class="sxs-lookup"><span data-stu-id="9a832-241">Four *data nodes*</span></span>
* <span data-ttu-id="9a832-242">Storm 叢集類型的預設值：</span><span class="sxs-lookup"><span data-stu-id="9a832-242">Storm cluster type default:</span></span> 
    * <span data-ttu-id="9a832-243">兩個 *Nimbus 節點*</span><span class="sxs-lookup"><span data-stu-id="9a832-243">Two *Nimbus nodes*</span></span>
    * <span data-ttu-id="9a832-244">三個 *ZooKeeper 節點*</span><span class="sxs-lookup"><span data-stu-id="9a832-244">Three *ZooKeeper nodes*</span></span>
    * <span data-ttu-id="9a832-245">四個*監督員節點*</span><span class="sxs-lookup"><span data-stu-id="9a832-245">Four *supervisor nodes*</span></span> 

<span data-ttu-id="9a832-246">如果您只是在試用 HDInsight，建議您使用一個資料節點。</span><span class="sxs-lookup"><span data-stu-id="9a832-246">If you are just trying out HDInsight, we recommend you use one data node.</span></span> <span data-ttu-id="9a832-247">如需關於 HDInsight 定價的詳細資訊，請參閱 [HDInsight 定價](https://go.microsoft.com/fwLink/?LinkID=282635&clcid=0x409)。</span><span class="sxs-lookup"><span data-stu-id="9a832-247">For more information about HDInsight pricing, see [HDInsight pricing](https://go.microsoft.com/fwLink/?LinkID=282635&clcid=0x409).</span></span>

> [!NOTE]
> <span data-ttu-id="9a832-248">叢集大小限制會隨著 Azure 訂用帳戶而有所不同。</span><span class="sxs-lookup"><span data-stu-id="9a832-248">The cluster size limit varies among Azure subscriptions.</span></span> <span data-ttu-id="9a832-249">若要提高限制，請與 [Azure 帳務支援人員](https://docs.microsoft.com/azure/azure-supportability/how-to-create-azure-support-request)連絡。</span><span class="sxs-lookup"><span data-stu-id="9a832-249">Contact [Azure billing support](https://docs.microsoft.com/azure/azure-supportability/how-to-create-azure-support-request) to increase the limit.</span></span>
>

<span data-ttu-id="9a832-250">使用 Azure 入口網站設定叢集時，節點大小會透過 [節點定價層] 刀鋒視窗公開。</span><span class="sxs-lookup"><span data-stu-id="9a832-250">When you use the Azure portal to configure the cluster, the node size is available through the **Node Pricing Tiers** blade.</span></span> <span data-ttu-id="9a832-251">在入口網站中，您也可以查看與不同節點大小相關聯的成本。</span><span class="sxs-lookup"><span data-stu-id="9a832-251">In the portal, you can also see the cost associated with the different node sizes.</span></span> 

![HDinsight VM 節點大小](./media/hdinsight-hadoop-provision-linux-clusters/hdinsight-node-sizes.png)

### <a name="virtual-machine-sizes"></a><span data-ttu-id="9a832-253">虛擬機器大小</span><span class="sxs-lookup"><span data-stu-id="9a832-253">Virtual machine sizes</span></span> 
<span data-ttu-id="9a832-254">當您部署叢集時，請依據計劃部署的解決方案選擇計算資源。</span><span class="sxs-lookup"><span data-stu-id="9a832-254">When you deploy clusters, choose compute resources based on the solution you plan to deploy.</span></span> <span data-ttu-id="9a832-255">下列 VM 可用於 HDInsight 叢集：</span><span class="sxs-lookup"><span data-stu-id="9a832-255">The following VMs are used for HDInsight clusters:</span></span>
* <span data-ttu-id="9a832-256">A 和 D1-4 系列 VM：[一般用途 Linux VM 大小](https://docs.microsoft.com/azure/virtual-machines/linux/sizes-general)</span><span class="sxs-lookup"><span data-stu-id="9a832-256">A and D1-4 series VMs: [General-purpose Linux VM sizes](https://docs.microsoft.com/azure/virtual-machines/linux/sizes-general)</span></span>
* <span data-ttu-id="9a832-257">D11-14 系列 VM：[記憶體最佳化 Linux VM 大小](https://docs.microsoft.com/azure/virtual-machines/linux/sizes-memory)</span><span class="sxs-lookup"><span data-stu-id="9a832-257">D11-14 series VM: [Memory-optimized Linux VM sizes](https://docs.microsoft.com/azure/virtual-machines/linux/sizes-memory)</span></span>

<span data-ttu-id="9a832-258">如需使用不同的 SDK 或使用 Azure PowerShell 建立叢集時應用來指定 VM 大小的值，請參閱[使用於 HDInsight 叢集的 VM 大小](../cloud-services/cloud-services-sizes-specs.md#size-tables)。</span><span class="sxs-lookup"><span data-stu-id="9a832-258">To find out what value you should use to specify a VM size while creating a cluster using the different SDKs or while using Azure PowerShell, see [VM sizes to use for HDInsight clusters](../cloud-services/cloud-services-sizes-specs.md#size-tables).</span></span> <span data-ttu-id="9a832-259">在此連結的文件中，請使用資料表中 **Size (大小)** 資料行的值。</span><span class="sxs-lookup"><span data-stu-id="9a832-259">From this linked article, use the value in the **Size** column of the tables.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9a832-260">如果您的叢集需要 32 個以上的背景工作角色節點，則必須選取具有至少 8 個核心和 14 GB RAM 的前端節點大小。</span><span class="sxs-lookup"><span data-stu-id="9a832-260">If you need more than 32 worker nodes in a cluster, you must select a head node size with at least 8 cores and 14 GB of RAM.</span></span>
>
>

<span data-ttu-id="9a832-261">如需相關資訊，請參閱[虛擬機器的大小](../virtual-machines/windows/sizes.md)。</span><span class="sxs-lookup"><span data-stu-id="9a832-261">For more information, see [Sizes for virtual machines](../virtual-machines/windows/sizes.md).</span></span> <span data-ttu-id="9a832-262">如需各式大小的價格資訊，請參閱 [HDInsight 價格](https://azure.microsoft.com/pricing/details/hdinsight)。</span><span class="sxs-lookup"><span data-stu-id="9a832-262">For information about pricing of the various sizes, see [HDInsight pricing](https://azure.microsoft.com/pricing/details/hdinsight).</span></span>   

## <a name="custom-cluster-setup"></a><span data-ttu-id="9a832-263">自訂叢集設定</span><span class="sxs-lookup"><span data-stu-id="9a832-263">Custom cluster setup</span></span>
<span data-ttu-id="9a832-264">自訂叢集設定是以 [Quick create] \(快速建立\) 的設定為基礎，並加入下列選項：</span><span class="sxs-lookup"><span data-stu-id="9a832-264">Custom cluster setup builds on the Quick create settings, and adds the following options:</span></span>
- [<span data-ttu-id="9a832-265">HDInsight 應用程式</span><span class="sxs-lookup"><span data-stu-id="9a832-265">HDInsight applications</span></span>](#hdinsight-applications)
- [<span data-ttu-id="9a832-266">叢集大小</span><span class="sxs-lookup"><span data-stu-id="9a832-266">Cluster size</span></span>](#cluster-size)
- <span data-ttu-id="9a832-267">進階設定</span><span class="sxs-lookup"><span data-stu-id="9a832-267">Advanced settings</span></span>
  - [<span data-ttu-id="9a832-268">指令碼動作</span><span class="sxs-lookup"><span data-stu-id="9a832-268">Script actions</span></span>](#customize-clusters-using-script-action)
  - [<span data-ttu-id="9a832-269">虛擬網路</span><span class="sxs-lookup"><span data-stu-id="9a832-269">Virtual network</span></span>](#use-virtual-network)

## <a name="install-hdinsight-applications-on-clusters"></a><span data-ttu-id="9a832-270">在叢集上安裝 HDInsight 應用程式</span><span class="sxs-lookup"><span data-stu-id="9a832-270">Install HDInsight applications on clusters</span></span>

<span data-ttu-id="9a832-271">HDInsight 應用程式是使用者可以在以 Linux 為基礎的 HDInsight 叢集上安裝的應用程式。</span><span class="sxs-lookup"><span data-stu-id="9a832-271">An HDInsight application is an application that users can install on a Linux-based HDInsight cluster.</span></span> <span data-ttu-id="9a832-272">您可以使用由 Microsoft、協力廠商所提供或您自己開發的應用程式。</span><span class="sxs-lookup"><span data-stu-id="9a832-272">You can use applications provided by Microsoft, third parties, or that you develop yourself.</span></span> <span data-ttu-id="9a832-273">如需詳細資訊，請參閱[在 Azure HDInsight 上安裝第三方 Hadoop 應用程式](hdinsight-apps-install-applications.md)。</span><span class="sxs-lookup"><span data-stu-id="9a832-273">For more information, see [Install third-party Hadoop applications on Azure HDInsight](hdinsight-apps-install-applications.md).</span></span>

<span data-ttu-id="9a832-274">大部分的 HDInsight 應用程式會安裝在空白的邊緣節點。</span><span class="sxs-lookup"><span data-stu-id="9a832-274">Most of the HDInsight applications are installed on an empty edge node.</span></span>  <span data-ttu-id="9a832-275">空白的邊緣節點是一部 Linux 虛擬機器，其中已安裝及設定和前端節點相同的用戶端工具。</span><span class="sxs-lookup"><span data-stu-id="9a832-275">An empty edge node is a Linux virtual machine with the same client tools installed and configured as in the head node.</span></span> <span data-ttu-id="9a832-276">您可以使用邊緣節點來存取叢集、測試用戶端應用程式，以及裝載用戶端應用程式。</span><span class="sxs-lookup"><span data-stu-id="9a832-276">You can use the edge node for accessing the cluster, testing your client applications, and hosting your client applications.</span></span> <span data-ttu-id="9a832-277">如需詳細資訊，請參閱 [Use empty edge nodes in HDInsight (在 HDInsight 中使用空白的邊緣節點)](hdinsight-apps-use-edge-node.md)。</span><span class="sxs-lookup"><span data-stu-id="9a832-277">For more information, see [Use empty edge nodes in HDInsight](hdinsight-apps-use-edge-node.md).</span></span>

## <a name="advanced-settings-script-actions"></a><span data-ttu-id="9a832-278">進階設定：指令碼動作</span><span class="sxs-lookup"><span data-stu-id="9a832-278">Advanced settings: Script actions</span></span>

<span data-ttu-id="9a832-279">您可以在建立期間使用指令碼來安裝其他元件或自訂組態。</span><span class="sxs-lookup"><span data-stu-id="9a832-279">You can install additional components or customize cluster configuration by using scripts during creation.</span></span> <span data-ttu-id="9a832-280">這類指令碼可透過 **指令碼動作**叫用，指令碼動作是一個組態選項，其可從 Azure 入口網站、HDInsight Windows PowerShell Cmdlet 或 HDInsight .NET SDK 使用。</span><span class="sxs-lookup"><span data-stu-id="9a832-280">Such scripts are invoked via **Script Action**, which is a configuration option that can be used from the Azure portal, HDInsight Windows PowerShell cmdlets, or the HDInsight .NET SDK.</span></span> <span data-ttu-id="9a832-281">如需詳細資訊，請參閱 [使用指令碼動作自訂 HDInsight 叢集](hdinsight-hadoop-customize-cluster-linux.md)。</span><span class="sxs-lookup"><span data-stu-id="9a832-281">For more information, see [Customize HDInsight cluster using Script Action](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

<span data-ttu-id="9a832-282">您可以使用 Java 封存 (JAR) 檔案形式在叢集上執行一些原生 Java 元件 (例如 Mahout 和 Cascading)。</span><span class="sxs-lookup"><span data-stu-id="9a832-282">Some native Java components, like Mahout and Cascading, can be run on the cluster as Java Archive (JAR) files.</span></span> <span data-ttu-id="9a832-283">這些 JAR 檔案可以配送至 Azure 儲存體，並透過 Hadoop 作業提交機制提交至 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="9a832-283">These JAR files can be distributed to Azure Storage and submitted to HDInsight clusters with Hadoop job submission mechanisms.</span></span> <span data-ttu-id="9a832-284">如需詳細資訊，請參閱 [以程式設計方式提交 Hadoop 工作](hdinsight-submit-hadoop-jobs-programmatically.md)。</span><span class="sxs-lookup"><span data-stu-id="9a832-284">For more information, see [Submit Hadoop jobs programmatically](hdinsight-submit-hadoop-jobs-programmatically.md).</span></span>

> [!NOTE]
> <span data-ttu-id="9a832-285">如果您在將 JAR 檔案部署至 HDInsight 叢集，或在 HDInsight 叢集上呼叫 JAR 檔案時發生問題，請連絡 [Microsoft 支援](https://azure.microsoft.com/support/options/)。</span><span class="sxs-lookup"><span data-stu-id="9a832-285">If you have issues deploying JAR files to HDInsight clusters, or calling JAR files on HDInsight clusters, contact [Microsoft Support](https://azure.microsoft.com/support/options/).</span></span>
>
> <span data-ttu-id="9a832-286">Cascading 不受 HDInsight 支援，而且不符合「Microsoft 支援」的資格。</span><span class="sxs-lookup"><span data-stu-id="9a832-286">Cascading is not supported by HDInsight and is not eligible for Microsoft Support.</span></span> <span data-ttu-id="9a832-287">如需所支援元件的清單，請參閱 [HDInsight 所提供叢集版本的新功能](hdinsight-component-versioning.md)。</span><span class="sxs-lookup"><span data-stu-id="9a832-287">For lists of supported components, see [What's new in the cluster versions provided by HDInsight](hdinsight-component-versioning.md).</span></span>
>
>

<span data-ttu-id="9a832-288">有時候，您可能要在建立程序期間設定下列組態檔：</span><span class="sxs-lookup"><span data-stu-id="9a832-288">Sometimes, you want to configure the following configuration files during the creation process:</span></span>

* <span data-ttu-id="9a832-289">clusterIdentity.xml</span><span class="sxs-lookup"><span data-stu-id="9a832-289">clusterIdentity.xml</span></span>
* <span data-ttu-id="9a832-290">core-site.xml</span><span class="sxs-lookup"><span data-stu-id="9a832-290">core-site.xml</span></span>
* <span data-ttu-id="9a832-291">gateway.xml</span><span class="sxs-lookup"><span data-stu-id="9a832-291">gateway.xml</span></span>
* <span data-ttu-id="9a832-292">hbase-env.xml</span><span class="sxs-lookup"><span data-stu-id="9a832-292">hbase-env.xml</span></span>
* <span data-ttu-id="9a832-293">hbase-site.xml</span><span class="sxs-lookup"><span data-stu-id="9a832-293">hbase-site.xml</span></span>
* <span data-ttu-id="9a832-294">hdfs-site.xml</span><span class="sxs-lookup"><span data-stu-id="9a832-294">hdfs-site.xml</span></span>
* <span data-ttu-id="9a832-295">hive-env.xml</span><span class="sxs-lookup"><span data-stu-id="9a832-295">hive-env.xml</span></span>
* <span data-ttu-id="9a832-296">hive-site.xml</span><span class="sxs-lookup"><span data-stu-id="9a832-296">hive-site.xml</span></span>
* <span data-ttu-id="9a832-297">mapred-site</span><span class="sxs-lookup"><span data-stu-id="9a832-297">mapred-site</span></span>
* <span data-ttu-id="9a832-298">oozie-site.xml</span><span class="sxs-lookup"><span data-stu-id="9a832-298">oozie-site.xml</span></span>
* <span data-ttu-id="9a832-299">oozie-env.xml</span><span class="sxs-lookup"><span data-stu-id="9a832-299">oozie-env.xml</span></span>
* <span data-ttu-id="9a832-300">storm-site.xml</span><span class="sxs-lookup"><span data-stu-id="9a832-300">storm-site.xml</span></span>
* <span data-ttu-id="9a832-301">tez-site.xml</span><span class="sxs-lookup"><span data-stu-id="9a832-301">tez-site.xml</span></span>
* <span data-ttu-id="9a832-302">webhcat-site.xml</span><span class="sxs-lookup"><span data-stu-id="9a832-302">webhcat-site.xml</span></span>
* <span data-ttu-id="9a832-303">yarn-site.xml</span><span class="sxs-lookup"><span data-stu-id="9a832-303">yarn-site.xml</span></span>

<span data-ttu-id="9a832-304">如需詳細資訊，請參閱 [使用 Bootstrap 自訂 HDInsight 叢集](hdinsight-hadoop-customize-cluster-bootstrap.md)。</span><span class="sxs-lookup"><span data-stu-id="9a832-304">For more information, see [Customize HDInsight clusters using Bootstrap](hdinsight-hadoop-customize-cluster-bootstrap.md).</span></span>

## <a name="advanced-settings-extend-clusters-with-a-virtual-network"></a><span data-ttu-id="9a832-305">進階設定：使用虛擬網路擴充叢集</span><span class="sxs-lookup"><span data-stu-id="9a832-305">Advanced settings: Extend clusters with a virtual network</span></span>
<span data-ttu-id="9a832-306">如果您的解決方案需要會分散到多個 HDInsight 叢集類型的技術，[Azure 虛擬網路](https://docs.microsoft.com/azure/virtual-network)可以連接必要的叢集類型。</span><span class="sxs-lookup"><span data-stu-id="9a832-306">If your solution requires technologies that are spread across multiple HDInsight cluster types, an [Azure virtual network](https://docs.microsoft.com/azure/virtual-network) can connect the required cluster types.</span></span> <span data-ttu-id="9a832-307">此組態可讓叢集以及其中部署的任何程式碼直接彼此通訊。</span><span class="sxs-lookup"><span data-stu-id="9a832-307">This configuration allows the clusters, and any code you deploy to them, to directly communicate with each other.</span></span>

<span data-ttu-id="9a832-308">如需如何搭配使用 Azure 虛擬網路與 HDInsight 的詳細資訊，請參閱[使用 Azure 虛擬網路擴充 HDInsight](hdinsight-extend-hadoop-virtual-network.md)。</span><span class="sxs-lookup"><span data-stu-id="9a832-308">For more information on using an Azure virtual network with HDInsight, see [Extend HDInsight with Azure virtual networks](hdinsight-extend-hadoop-virtual-network.md).</span></span>

<span data-ttu-id="9a832-309">如需在 Azure 虛擬網路內使用兩個叢集類型的範例，請參閱[使用 Storm 和 HBase 分析感應器資料](hdinsight-storm-sensor-data-analysis.md)。</span><span class="sxs-lookup"><span data-stu-id="9a832-309">For an example of using two cluster types within an Azure virtual network, see [Analyze sensor data with Storm and HBase](hdinsight-storm-sensor-data-analysis.md).</span></span> <span data-ttu-id="9a832-310">如需搭配虛擬網路使用 HDInsight 的詳細資訊 (包含虛擬網路的特定組態需求)，請參閱 [使用 Azure 虛擬網路延伸 HDInsight 功能](hdinsight-extend-hadoop-virtual-network.md)。</span><span class="sxs-lookup"><span data-stu-id="9a832-310">For more information about using HDInsight with a virtual network, including specific configuration requirements for the virtual network, see [Extend HDInsight capabilities by using Azure Virtual Network](hdinsight-extend-hadoop-virtual-network.md).</span></span>

## <a name="troubleshoot-access-control-issues"></a><span data-ttu-id="9a832-311">針對存取控制問題進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="9a832-311">Troubleshoot access control issues</span></span>

<span data-ttu-id="9a832-312">如果您在建立 HDInsight 叢集時遇到問題，請參閱[存取控制需求](hdinsight-administer-use-portal-linux.md#create-clusters)。</span><span class="sxs-lookup"><span data-stu-id="9a832-312">If you run into issues with creating HDInsight clusters, see [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>

## <a name="next-steps"></a><span data-ttu-id="9a832-313">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9a832-313">Next steps</span></span>

- [<span data-ttu-id="9a832-314">什麼是 HDInsight、Hadoop 生態系統以及 Hadoop 叢集？</span><span class="sxs-lookup"><span data-stu-id="9a832-314">What are HDInsight, the Hadoop ecosystem, and Hadoop clusters?</span></span>](hdinsight-hadoop-introduction.md)
- [<span data-ttu-id="9a832-315">開始在 HDInsight 中使用 Hadoop</span><span class="sxs-lookup"><span data-stu-id="9a832-315">Get started using Hadoop in HDInsight</span></span>](hdinsight-hadoop-linux-tutorial-get-started.md)
- [<span data-ttu-id="9a832-316">從 Windows PC 在 HDInsight 上的 Hadoop 中作業</span><span class="sxs-lookup"><span data-stu-id="9a832-316">Work in Hadoop on HDInsight from a Windows PC</span></span>](hdinsight-hadoop-windows-tools.md)
