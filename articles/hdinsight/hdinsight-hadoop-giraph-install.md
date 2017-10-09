---
title: "aaaInstall 和使用 Giraph 在 Hadoop 叢集 HDInsight 的 Azure 中 |Microsoft 文件"
description: "了解如何 toocustomize HDInsight 叢集 Giraph，以及如何 toouse Giraph。"
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 77a1d0e0-55de-4e61-98a0-060914fb7ca0
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/05/2016
ms.author: nitinme
ROBOTS: NOINDEX
ms.openlocfilehash: bd473faca9d3c87c29d7566a18fc94211c50f059
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-use-giraph-on-windows-based-hdinsight-clusters"></a><span data-ttu-id="d321d-103">在 Windows 型 HDInsight 叢集上安裝和使用 Giraph</span><span class="sxs-lookup"><span data-stu-id="d321d-103">Install and use Giraph on Windows-based HDInsight clusters</span></span>

<span data-ttu-id="d321d-104">了解如何使用指令碼動作 Giraph toocustomize Windows 依據 HDInsight 叢集以及如何 toouse Giraph tooprocess 大規模圖形。</span><span class="sxs-lookup"><span data-stu-id="d321d-104">Learn how toocustomize Windows based HDInsight cluster with Giraph using Script Action, and how toouse Giraph tooprocess large-scale graphs.</span></span> <span data-ttu-id="d321d-105">如需搭配以 Linux 為基礎的叢集使用 Giraph 的詳細資訊，請參閱 [在 HDInsight Hadoop 叢集上安裝 Giraph (Linux)](hdinsight-hadoop-giraph-install-linux.md)。</span><span class="sxs-lookup"><span data-stu-id="d321d-105">For information on using Giraph with a Linux-based cluster, see [Install Giraph on HDInsight Hadoop clusters (Linux)](hdinsight-hadoop-giraph-install-linux.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d321d-106">hello 中此文件僅搭配 Windows 為基礎的 HDInsight 叢集的步驟。</span><span class="sxs-lookup"><span data-stu-id="d321d-106">hello steps in this document only work with Windows-based HDInsight clusters.</span></span> <span data-ttu-id="d321d-107">Windows 上的 HDInsight 只提供低於 HDInsight 3.4 的版本。</span><span class="sxs-lookup"><span data-stu-id="d321d-107">HDInsight is only available on Windows for versions lower than HDInsight 3.4.</span></span> <span data-ttu-id="d321d-108">Linux 為 hello 僅作業系統 HDInsight 3.4 或更新版本上使用。</span><span class="sxs-lookup"><span data-stu-id="d321d-108">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="d321d-109">如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。</span><span class="sxs-lookup"><span data-stu-id="d321d-109">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span> <span data-ttu-id="d321d-110">如需詳細資訊 tooinstall Giraph 於 linux 的 HDInsight 叢集上，請參閱[HDInsight Hadoop 叢集 (Linux) 上的安裝 Giraph](hdinsight-hadoop-giraph-install-linux.md)。</span><span class="sxs-lookup"><span data-stu-id="d321d-110">For information on how tooinstall Giraph on a Linux-based HDInsight cluster, see [Install Giraph on HDInsight Hadoop clusters (Linux)](hdinsight-hadoop-giraph-install-linux.md).</span></span>


<span data-ttu-id="d321d-111">您也可以使用「指令碼動作」 ，在 Azure HDInsight 的任一類型的叢集 (Hadoop、Storm、HBase、Spark) 上安裝 Giraph。</span><span class="sxs-lookup"><span data-stu-id="d321d-111">You can install Giraph on any type of cluster (Hadoop, Storm, HBase, Spark) on Azure HDInsight by using *Script Action*.</span></span> <span data-ttu-id="d321d-112">範例指令碼 tooinstall Giraph 在 HDInsight 叢集上的都可從唯讀的 Azure 儲存體 blob [https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1)。</span><span class="sxs-lookup"><span data-stu-id="d321d-112">A sample script tooinstall Giraph on an HDInsight cluster is available from a read-only Azure storage blob at [https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1).</span></span> <span data-ttu-id="d321d-113">hello 範例指令碼僅適用於 HDInsight 叢集版本 3.1。</span><span class="sxs-lookup"><span data-stu-id="d321d-113">hello sample script works only with HDInsight cluster version 3.1.</span></span> <span data-ttu-id="d321d-114">如需 HDInsight 叢集版本的詳細資訊，請參閱 [HDInsight 叢集版本](hdinsight-component-versioning.md)。</span><span class="sxs-lookup"><span data-stu-id="d321d-114">For more information on HDInsight cluster versions, see [HDInsight cluster versions](hdinsight-component-versioning.md).</span></span>

<span data-ttu-id="d321d-115">**相關文章**</span><span class="sxs-lookup"><span data-stu-id="d321d-115">**Related articles**</span></span>

* [<span data-ttu-id="d321d-116">在 HDInsight Hadoop 叢集上安裝 Giraph (Linux)</span><span class="sxs-lookup"><span data-stu-id="d321d-116">Install Giraph on HDInsight Hadoop clusters (Linux)</span></span>](hdinsight-hadoop-giraph-install-linux.md)
* <span data-ttu-id="d321d-117">[在 HDInsight 叢集中建立 Hadoop](hdinsight-provision-clusters.md)：建立 HDInsight 叢集的一般資訊。</span><span class="sxs-lookup"><span data-stu-id="d321d-117">[Create Hadoop clusters in HDInsight](hdinsight-provision-clusters.md): general information on creating HDInsight clusters.</span></span>
* <span data-ttu-id="d321d-118">[使用指令碼動作來自訂 HDInsight 叢集][hdinsight-cluster-customize]：關於使用指令碼動作來自訂 HDInsight 叢集的一般資訊。</span><span class="sxs-lookup"><span data-stu-id="d321d-118">[Customize HDInsight cluster using Script Action][hdinsight-cluster-customize]: general information on customizing HDInsight clusters using Script Action.</span></span>
* <span data-ttu-id="d321d-119">[開發 HDInsight 的指令碼動作指令碼](hdinsight-hadoop-script-actions.md)</span><span class="sxs-lookup"><span data-stu-id="d321d-119">[Develop Script Action scripts for HDInsight](hdinsight-hadoop-script-actions.md).</span></span>

## <a name="what-is-giraph"></a><span data-ttu-id="d321d-120">什麼是 Giraph？</span><span class="sxs-lookup"><span data-stu-id="d321d-120">What is Giraph?</span></span>
<span data-ttu-id="d321d-121"><a href="http://giraph.apache.org/" target="_blank">Apache Giraph</a>可讓您使用 Hadoop，處理 tooperform 圖形，並可以搭配 Azure HDInsight。</span><span class="sxs-lookup"><span data-stu-id="d321d-121"><a href="http://giraph.apache.org/" target="_blank">Apache Giraph</a> allows you tooperform graph processing by using Hadoop, and can be used with Azure HDInsight.</span></span> <span data-ttu-id="d321d-122">圖形物件，例如大型網路 hello 網際網路，類似於各路由器間 hello 連接之間的關聯性模型化，或者 (有時候參照 tooas 社交圖形) 的社交網路上的人員之間的關聯性。</span><span class="sxs-lookup"><span data-stu-id="d321d-122">Graphs model relationships between objects, such as hello connections between routers on a large network like hello Internet, or relationships between people on social networks (sometimes referred tooas a social graph).</span></span> <span data-ttu-id="d321d-123">圖表處理可讓您 hello 在圖形中，物件之間的關聯性的相關 tooreason 例如：</span><span class="sxs-lookup"><span data-stu-id="d321d-123">Graph processing allows you tooreason about hello relationships between objects in a graph, such as:</span></span>

* <span data-ttu-id="d321d-124">根據目前的人際關係找出可能的朋友。</span><span class="sxs-lookup"><span data-stu-id="d321d-124">Identifying potential friends based on your current relationships.</span></span>
* <span data-ttu-id="d321d-125">用來識別網路中的兩部電腦之間的 hello 最短路由。</span><span class="sxs-lookup"><span data-stu-id="d321d-125">Identifying hello shortest route between two computers in a network.</span></span>
* <span data-ttu-id="d321d-126">計算 hello 頁面順位的網頁。</span><span class="sxs-lookup"><span data-stu-id="d321d-126">Calculating hello page rank of webpages.</span></span>

## <a name="install-giraph-using-portal"></a><span data-ttu-id="d321d-127">使用入口網站安裝 Giraph</span><span class="sxs-lookup"><span data-stu-id="d321d-127">Install Giraph using portal</span></span>
1. <span data-ttu-id="d321d-128">啟動 建立叢集使用 hello**自訂建立**選項，依照[在 HDInsight 中的建立 Hadoop 叢集](hdinsight-provision-clusters.md)。</span><span class="sxs-lookup"><span data-stu-id="d321d-128">Start creating a cluster by using hello **CUSTOM CREATE** option, as described at [Create Hadoop clusters in HDInsight](hdinsight-provision-clusters.md).</span></span>
2. <span data-ttu-id="d321d-129">在 [hello**指令碼動作**頁面 hello 精靈] 中，按一下**加入指令碼動作**tooprovide 詳細 hello 指令碼動作，如下所示：</span><span class="sxs-lookup"><span data-stu-id="d321d-129">On hello **Script Actions** page of hello wizard, click **add script action** tooprovide details about hello script action, as shown below:</span></span>

    <span data-ttu-id="d321d-130">![使用指令碼動作 toocustomize 叢集](./media/hdinsight-hadoop-giraph-install/hdi-script-action-giraph.png "使用指令碼動作 toocustomize 叢集")</span><span class="sxs-lookup"><span data-stu-id="d321d-130">![Use Script Action toocustomize a cluster](./media/hdinsight-hadoop-giraph-install/hdi-script-action-giraph.png "Use Script Action toocustomize a cluster")</span></span>

    <table border='1'>
        <tr><th><span data-ttu-id="d321d-131">屬性</span><span class="sxs-lookup"><span data-stu-id="d321d-131">Property</span></span></th><th><span data-ttu-id="d321d-132">值</span><span class="sxs-lookup"><span data-stu-id="d321d-132">Value</span></span></th></tr>
        <tr><td><span data-ttu-id="d321d-133">名稱</span><span class="sxs-lookup"><span data-stu-id="d321d-133">Name</span></span></td>
            <td><span data-ttu-id="d321d-134">指定 hello 指令碼動作的名稱。</span><span class="sxs-lookup"><span data-stu-id="d321d-134">Specify a name for hello script action.</span></span> <span data-ttu-id="d321d-135">例如，<b>安裝 Giraph</b>。</span><span class="sxs-lookup"><span data-stu-id="d321d-135">For example, <b>Install Giraph</b>.</span></span></td></tr>
        <tr><td><span data-ttu-id="d321d-136">指令碼 URI</span><span class="sxs-lookup"><span data-stu-id="d321d-136">Script URI</span></span></td>
            <td><span data-ttu-id="d321d-137">指定 hello 統一資源識別元 (URI) toohello 指令碼會叫用的 toocustomize hello 叢集。</span><span class="sxs-lookup"><span data-stu-id="d321d-137">Specify hello Uniform Resource Identifier (URI) toohello script that is invoked toocustomize hello cluster.</span></span> <span data-ttu-id="d321d-138">例如，<i>https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1</i></span><span class="sxs-lookup"><span data-stu-id="d321d-138">For example, <i>https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1</i></span></span></td></tr>
        <tr><td><span data-ttu-id="d321d-139">節點類型</span><span class="sxs-lookup"><span data-stu-id="d321d-139">Node Type</span></span></td>
            <td><span data-ttu-id="d321d-140">指定 hello hello 自訂指令碼執行所在的節點。</span><span class="sxs-lookup"><span data-stu-id="d321d-140">Specify hello nodes on which hello customization script is run.</span></span> <span data-ttu-id="d321d-141">您可以選擇 [所有節點]<b></b>、[僅限前端節點]<b></b> 或 [僅限背景工作節點]<b></b>。</span><span class="sxs-lookup"><span data-stu-id="d321d-141">You can choose <b>All nodes</b>, <b>Head nodes only</b>, or <b>Worker nodes only</b>.</span></span>
        <tr><td><span data-ttu-id="d321d-142">參數</span><span class="sxs-lookup"><span data-stu-id="d321d-142">Parameters</span></span></td>
            <td><span data-ttu-id="d321d-143">指定 hello 參數，如果 hello 指令碼所需。</span><span class="sxs-lookup"><span data-stu-id="d321d-143">Specify hello parameters, if required by hello script.</span></span> <span data-ttu-id="d321d-144">hello 指令碼 tooinstall Giraph 不需要任何參數，因此您可以讓此處空白。</span><span class="sxs-lookup"><span data-stu-id="d321d-144">hello script tooinstall Giraph does not require any parameters, so you can leave this blank.</span></span></td></tr>
    </table>

    <span data-ttu-id="d321d-145">您可以在 hello 叢集上新增多個指令碼動作 tooinstall 多個元件。</span><span class="sxs-lookup"><span data-stu-id="d321d-145">You can add more than one script action tooinstall multiple components on hello cluster.</span></span> <span data-ttu-id="d321d-146">加入 hello 指令碼之後，按一下 建立 hello 叢集 hello 核取記號 toostart。</span><span class="sxs-lookup"><span data-stu-id="d321d-146">After you have added hello scripts, click hello checkmark toostart creating hello cluster.</span></span>

## <a name="use-giraph"></a><span data-ttu-id="d321d-147">使用 Giraph</span><span class="sxs-lookup"><span data-stu-id="d321d-147">Use Giraph</span></span>
<span data-ttu-id="d321d-148">我們使用 hello SimpleShortestPathsComputation 範例 toodemonstrate hello basic <a href = "http://people.apache.org/~edwardyoon/documents/pregel.pdf">Pregel</a>尋找 hello 圖形中的物件之間最短的路徑實作。</span><span class="sxs-lookup"><span data-stu-id="d321d-148">We use hello SimpleShortestPathsComputation example toodemonstrate hello basic <a href = "http://people.apache.org/~edwardyoon/documents/pregel.pdf">Pregel</a> implementation for finding hello shortest path between objects in a graph.</span></span> <span data-ttu-id="d321d-149">使用下列步驟 tooupload hello 範例資料和 hello 範例 jar，以便使用 hello SimpleShortestPathsComputation 範例中，然後按一下 檢視 hello 結果執行工作的 hello。</span><span class="sxs-lookup"><span data-stu-id="d321d-149">Use hello following steps tooupload hello sample data and hello sample jar, run a job by using hello SimpleShortestPathsComputation example, and then view hello results.</span></span>

1. <span data-ttu-id="d321d-150">上傳範例資料檔案 tooAzure Blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="d321d-150">Upload a sample data file tooAzure Blob storage.</span></span> <span data-ttu-id="d321d-151">在本機工作站上，建立名為 **tiny_graph.txt** 的新檔案。</span><span class="sxs-lookup"><span data-stu-id="d321d-151">On your local workstation, create a new file named **tiny_graph.txt**.</span></span> <span data-ttu-id="d321d-152">它應該包含下列行 hello:</span><span class="sxs-lookup"><span data-stu-id="d321d-152">It should contain hello following lines:</span></span>

        [0,0,[[1,1],[3,3]]]
        [1,0,[[0,1],[2,2],[3,1]]]
        [2,0,[[1,2],[4,4]]]
        [3,0,[[0,3],[1,1],[4,4]]]
        [4,0,[[3,4],[2,4]]]

    <span data-ttu-id="d321d-153">上傳 hello tiny_graph.txt 檔案 toohello 主要儲存體您的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="d321d-153">Upload hello tiny_graph.txt file toohello primary storage for your HDInsight cluster.</span></span> <span data-ttu-id="d321d-154">如需有關指示 tooupload 資料，請參閱 < [HDInsight 中的 Hadoop 工作的資料上傳](hdinsight-upload-data.md)。</span><span class="sxs-lookup"><span data-stu-id="d321d-154">For instructions on how tooupload data, see [Upload data for Hadoop jobs in HDInsight](hdinsight-upload-data.md).</span></span>

    <span data-ttu-id="d321d-155">這項資料會描述一種導向圖形，藉由使用 hello 格式中的物件之間的關聯性 [來源\_識別碼、 來源\_值] [[目的地\_識別碼]，[邊緣\_值]，...]]。每一行代表 **source\_id** 物件和一或多個 **dest\_id** 物件之間的關聯性。</span><span class="sxs-lookup"><span data-stu-id="d321d-155">This data describes a relationship between objects in a directed graph, by using hello format [source\_id, source\_value,[[dest\_id], [edge\_value],...]]. Each line represents a relationship between a **source\_id** object and one or more **dest\_id** objects.</span></span> <span data-ttu-id="d321d-156">hello**邊緣\_值**（或加權） 可以視為 hello 強度或 hello 連線之間的距離**source_id**和**目的地\_識別碼**.</span><span class="sxs-lookup"><span data-stu-id="d321d-156">hello **edge\_value** (or weight) can be thought of as hello strength or distance of hello connection between **source_id** and **dest\_id**.</span></span>

    <span data-ttu-id="d321d-157">繪製出，且使用 hello 值 （或加權），做為 hello 物件之間的距離，hello 上方資料看起來可能像這樣：</span><span class="sxs-lookup"><span data-stu-id="d321d-157">Drawn out, and using hello value (or weight) as hello distance between objects, hello above data might look like this:</span></span>

    ![tiny_graph.txt drawn as circles with lines of varying distance between](./media/hdinsight-hadoop-giraph-install/giraph-graph.png)
2. <span data-ttu-id="d321d-159">執行 hello SimpleShortestPathsComputation 範例。</span><span class="sxs-lookup"><span data-stu-id="d321d-159">Run hello SimpleShortestPathsComputation example.</span></span> <span data-ttu-id="d321d-160">使用下列 Azure PowerShell cmdlet toorun hello 範例利用 hello tiny_graph.txt 檔案做為輸入 hello。</span><span class="sxs-lookup"><span data-stu-id="d321d-160">Use hello following Azure PowerShell cmdlets toorun hello example by using hello tiny_graph.txt file as input.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="d321d-161">使用 Azure Service Manager 管理 HDInsight 資源的 Azure PowerShell 支援已**被取代**，並已在 2017 年 1 月 1 日移除。</span><span class="sxs-lookup"><span data-stu-id="d321d-161">Azure PowerShell support for managing HDInsight resources using Azure Service Manager is **deprecated**, and was removed on January 1, 2017.</span></span> <span data-ttu-id="d321d-162">此文件使用 hello 新 HDInsight 的 cmdlet 可與 Azure 資源管理員中的步驟 hello。</span><span class="sxs-lookup"><span data-stu-id="d321d-162">hello steps in this document use hello new HDInsight cmdlets that work with Azure Resource Manager.</span></span>
    >
    > <span data-ttu-id="d321d-163">請依照中的 hello 步驟[安裝和設定 Azure PowerShell](/powershell/azureps-cmdlets-docs) tooinstall hello 最新版的 Azure PowerShell。</span><span class="sxs-lookup"><span data-stu-id="d321d-163">Please follow hello steps in [Install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) tooinstall hello latest version of Azure PowerShell.</span></span> <span data-ttu-id="d321d-164">如果您有指令碼的需要 toobe 修改 toouse hello 新的 cmdlet 可與 Azure 資源管理員，請參閱[移轉 tooAzure 資源管理員為基礎的開發工具的 HDInsight 叢集](hdinsight-hadoop-development-using-azure-resource-manager.md)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="d321d-164">If you have scripts that need toobe modified toouse hello new cmdlets that work with Azure Resource Manager, see [Migrating tooAzure Resource Manager-based development tools for HDInsight clusters](hdinsight-hadoop-development-using-azure-resource-manager.md) for more information.</span></span>

    ```powershell
    $clusterName = "clustername"
    # Giraph examples jar
    $jarFile = "wasb:///example/jars/giraph-examples.jar"
    # Arguments for this job
    $jobArguments = "org.apache.giraph.examples.SimpleShortestPathsComputation",
                    "-ca", "mapred.job.tracker=headnodehost:9010",
                    "-vif", "org.apache.giraph.io.formats.JsonLongDoubleFloatDoubleVertexInputFormat",
                    "-vip", "wasb:///example/data/tiny_graph.txt",
                    "-vof", "org.apache.giraph.io.formats.IdWithValueTextOutputFormat",
                    "-op",  "wasb:///example/output/shortestpaths",
                    "-w", "2"
    # Create hello definition
    $jobDefinition = New-AzureHDInsightMapReduceJobDefinition
        -JarFile $jarFile
        -ClassName "org.apache.giraph.GiraphRunner"
        -Arguments $jobArguments

    # Run hello job, write output toohello Azure PowerShell window
    $job = Start-AzureHDInsightJob -Cluster $clusterName -JobDefinition $jobDefinition
    Write-Host "Wait for hello job toocomplete ..." -ForegroundColor Green
    Wait-AzureHDInsightJob -Job $job
    Write-Host "STDERR"
    Get-AzureHDInsightJobOutput -Cluster $clusterName -JobId $job.JobId -StandardError
    Write-Host "Display hello standard output ..." -ForegroundColor Green
    Get-AzureHDInsightJobOutput -Cluster $clusterName -JobId $job.JobId -StandardOutput
    ```

    <span data-ttu-id="d321d-165">在上述範例中的 hello，取代**clustername** hello 您已安裝的 Giraph 的 HDInsight 叢集名稱。</span><span class="sxs-lookup"><span data-stu-id="d321d-165">In hello above example, replace **clustername** with hello name of your HDInsight cluster that has Giraph installed.</span></span>
3. <span data-ttu-id="d321d-166">檢視 hello 結果。</span><span class="sxs-lookup"><span data-stu-id="d321d-166">View hello results.</span></span> <span data-ttu-id="d321d-167">一旦 hello 工作已完成，hello 結果將會儲存在兩個輸出檔案中 hello **wasb: / 範例/out/shotestpaths**資料夾。</span><span class="sxs-lookup"><span data-stu-id="d321d-167">Once hello job has finished, hello results will be stored in two output files in hello **wasb:///example/out/shotestpaths** folder.</span></span> <span data-ttu-id="d321d-168">hello 檔案被稱為**一部分-m-00001**和**一部分-m-00002**。</span><span class="sxs-lookup"><span data-stu-id="d321d-168">hello files are called **part-m-00001** and **part-m-00002**.</span></span> <span data-ttu-id="d321d-169">執行下列步驟 toodownload 和檢視 hello 輸出 hello:</span><span class="sxs-lookup"><span data-stu-id="d321d-169">Perform hello following steps toodownload and view hello output:</span></span>

    ```powershell
    $subscriptionName = "<SubscriptionName>"       # Azure subscription name
    $storageAccountName = "<StorageAccountName>"   # Azure Storage account name
    $containerName = "<ContainerName>"             # Blob storage container name

    # Select hello current subscription
    Select-AzureSubscription $subscriptionName

    # Create hello Storage account context object
    $storageAccountKey = Get-AzureStorageKey $storageAccountName | %{ $_.Primary }
    $storageContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey

    # Download hello job output toohello workstation
    Get-AzureStorageBlobContent -Container $containerName -Blob example/output/shortestpaths/part-m-00001 -Context $storageContext -Force
    Get-AzureStorageBlobContent -Container $containerName -Blob example/output/shortestpaths/part-m-00002 -Context $storageContext -Force
    ```

    <span data-ttu-id="d321d-170">這會建立 hello**範例/輸出/shortestpaths** hello 等您的工作站，下載 hello 兩個輸出檔案 toothat 位置的目前目錄中的目錄結構。</span><span class="sxs-lookup"><span data-stu-id="d321d-170">This will create hello **example/output/shortestpaths** directory structure in hello current directory on your workstation, and download hello two output files toothat location.</span></span>

    <span data-ttu-id="d321d-171">使用 hello **Cat** hello 檔案的 cmdlet toodisplay hello 內容：</span><span class="sxs-lookup"><span data-stu-id="d321d-171">Use hello **Cat** cmdlet toodisplay hello contents of hello files:</span></span>

        Cat example/output/shortestpaths/part*

    <span data-ttu-id="d321d-172">hello 輸出應該看起來類似 toohello 下列：</span><span class="sxs-lookup"><span data-stu-id="d321d-172">hello output should appear similar toohello following:</span></span>

        0    1.0
        4    5.0
        2    2.0
        1    0.0
        3    1.0

    <span data-ttu-id="d321d-173">hello SimpleShortestPathComputation 範例是硬式編碼的 toostart 與物件識別碼為 1，並尋找 hello 最短路徑 tooother 物件。</span><span class="sxs-lookup"><span data-stu-id="d321d-173">hello SimpleShortestPathComputation example is hard coded toostart with object ID 1 and find hello shortest path tooother objects.</span></span> <span data-ttu-id="d321d-174">因此 hello 輸出應該會讀取成`destination_id distance`距離所在 hello 值 （或加權） 旅行 hello 邊緣的物件識別碼為 1 與 hello 目標 id。</span><span class="sxs-lookup"><span data-stu-id="d321d-174">So hello output should be read as `destination_id distance`, where distance is hello value (or weight) of hello edges traveled between object ID 1 and hello target ID.</span></span>

    <span data-ttu-id="d321d-175">將此視覺化，您可以確認 hello 結果識別碼 1 和所有其他物件之間旅行 hello 最短的路徑。</span><span class="sxs-lookup"><span data-stu-id="d321d-175">Visualizing this, you can verify hello results by traveling hello shortest paths between ID 1 and all other objects.</span></span> <span data-ttu-id="d321d-176">請注意，hello 識別碼 1 和識別碼 4 之間的最短路徑為 5。</span><span class="sxs-lookup"><span data-stu-id="d321d-176">Note that hello shortest path between ID 1 and ID 4 is 5.</span></span> <span data-ttu-id="d321d-177">這是 hello 總之間的距離<span style="color:orange">識別碼 1 和 3</span>，然後<span style="color:red">ID 為 3 和 4</span>。</span><span class="sxs-lookup"><span data-stu-id="d321d-177">This is hello total distance between <span style="color:orange">ID 1 and 3</span>, and then <span style="color:red">ID 3 and 4</span>.</span></span>

    ![Drawing of objects as circles with shortest paths drawn between](./media/hdinsight-hadoop-giraph-install/giraph-graph-out.png)

## <a name="install-giraph-using-aure-powershell"></a><span data-ttu-id="d321d-179">使用 Aure PowerShell 安裝 Giraph</span><span class="sxs-lookup"><span data-stu-id="d321d-179">Install Giraph using Aure PowerShell</span></span>
<span data-ttu-id="d321d-180">請參閱[使用指令碼動作來自訂 HDInsight 叢集](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell)。</span><span class="sxs-lookup"><span data-stu-id="d321d-180">See [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span></span>  <span data-ttu-id="d321d-181">hello 範例會示範如何使用 Azure PowerShell 的 Spark tooinstall。</span><span class="sxs-lookup"><span data-stu-id="d321d-181">hello sample demonstrates how tooinstall Spark using Azure PowerShell.</span></span> <span data-ttu-id="d321d-182">您需要 toocustomize hello 指令碼 toouse [https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1)。</span><span class="sxs-lookup"><span data-stu-id="d321d-182">You need toocustomize hello script toouse [https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1).</span></span>

## <a name="install-giraph-using-net-sdk"></a><span data-ttu-id="d321d-183">使用 .NET SDK 安裝 Giraph</span><span class="sxs-lookup"><span data-stu-id="d321d-183">Install Giraph using .NET SDK</span></span>
<span data-ttu-id="d321d-184">請參閱[使用指令碼動作來自訂 HDInsight 叢集](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell)。</span><span class="sxs-lookup"><span data-stu-id="d321d-184">See [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span></span> <span data-ttu-id="d321d-185">hello 範例會示範如何 tooinstall Spark 使用 hello.NET SDK。</span><span class="sxs-lookup"><span data-stu-id="d321d-185">hello sample demonstrates how tooinstall Spark using hello .NET SDK.</span></span> <span data-ttu-id="d321d-186">您需要 toocustomize hello 指令碼 toouse [https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1)。</span><span class="sxs-lookup"><span data-stu-id="d321d-186">You need toocustomize hello script toouse [https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1).</span></span>

## <a name="see-also"></a><span data-ttu-id="d321d-187">另請參閱</span><span class="sxs-lookup"><span data-stu-id="d321d-187">See also</span></span>
* [<span data-ttu-id="d321d-188">在 HDInsight Hadoop 叢集上安裝 Giraph (Linux)</span><span class="sxs-lookup"><span data-stu-id="d321d-188">Install Giraph on HDInsight Hadoop clusters (Linux)</span></span>](hdinsight-hadoop-giraph-install-linux.md)
* <span data-ttu-id="d321d-189">[在 HDInsight 叢集中建立 Hadoop](hdinsight-provision-clusters.md)：建立 HDInsight 叢集的一般資訊。</span><span class="sxs-lookup"><span data-stu-id="d321d-189">[Create Hadoop clusters in HDInsight](hdinsight-provision-clusters.md): general information on creating HDInsight clusters.</span></span>
* <span data-ttu-id="d321d-190">[使用指令碼動作來自訂 HDInsight 叢集][hdinsight-cluster-customize]：關於使用指令碼動作來自訂 HDInsight 叢集的一般資訊。</span><span class="sxs-lookup"><span data-stu-id="d321d-190">[Customize HDInsight cluster using Script Action][hdinsight-cluster-customize]: general information on customizing HDInsight clusters using Script Action.</span></span>
* <span data-ttu-id="d321d-191">[開發 HDInsight 的指令碼動作指令碼](hdinsight-hadoop-script-actions.md)</span><span class="sxs-lookup"><span data-stu-id="d321d-191">[Develop Script Action scripts for HDInsight](hdinsight-hadoop-script-actions.md).</span></span>
* <span data-ttu-id="d321d-192">[在 HDInsight 叢集上安裝和使用 Spark][hdinsight-install-spark]：關於安裝 Spark 的指令碼動作範例。</span><span class="sxs-lookup"><span data-stu-id="d321d-192">[Install and use Spark on HDInsight clusters][hdinsight-install-spark]: Script Action sample about installing Spark.</span></span>
* <span data-ttu-id="d321d-193">[在 HDInsight 叢集上安裝 R][hdinsight-install-r]：關於安裝 R 的指令碼動作範例。</span><span class="sxs-lookup"><span data-stu-id="d321d-193">[Install R on HDInsight clusters][hdinsight-install-r]: Script Action sample about installing R.</span></span>
* <span data-ttu-id="d321d-194">[在 HDInsight 叢集上安裝 Solr](hdinsight-hadoop-solr-install.md)：關於安裝 Solr 的指令碼動作範例。</span><span class="sxs-lookup"><span data-stu-id="d321d-194">[Install Solr on HDInsight clusters](hdinsight-hadoop-solr-install.md): Script Action sample about installing Solr.</span></span>

[tools]: https://github.com/Blackmist/hdinsight-tools
[aps]: http://azure.microsoft.com/documentation/articles/install-configure-powershell/

[powershell-install]: /powershell/azureps-cmdlets-docs
[hdinsight-provision]: hdinsight-provision-clusters.md
[hdinsight-install-r]: hdinsight-hadoop-r-scripts.md
[hdinsight-install-spark]: hdinsight-hadoop-spark-install.md
[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster.md
