---
title: "在 HDInsight 的 Hadoop 叢集上安裝和使用 Giraph - Azure | Microsoft Docs"
description: "了解如何使用 Giraph 自訂 HDInsight 叢集，以及如何使用 Giraph。"
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
ms.openlocfilehash: f0eb5c1f457380600463a370043f03e6d655a02c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="install-and-use-giraph-on-windows-based-hdinsight-clusters"></a><span data-ttu-id="6b03d-103">在 Windows 型 HDInsight 叢集上安裝和使用 Giraph</span><span class="sxs-lookup"><span data-stu-id="6b03d-103">Install and use Giraph on Windows-based HDInsight clusters</span></span>

<span data-ttu-id="6b03d-104">了解如何使用指令碼動作來自訂以 Windows 為基礎的 HDInsight 叢集，以及如何使用 Giraph 來處理大型圖形。</span><span class="sxs-lookup"><span data-stu-id="6b03d-104">Learn how to customize Windows based HDInsight cluster with Giraph using Script Action, and how to use Giraph to process large-scale graphs.</span></span> <span data-ttu-id="6b03d-105">如需搭配以 Linux 為基礎的叢集使用 Giraph 的詳細資訊，請參閱 [在 HDInsight Hadoop 叢集上安裝 Giraph (Linux)](hdinsight-hadoop-giraph-install-linux.md)。</span><span class="sxs-lookup"><span data-stu-id="6b03d-105">For information on using Giraph with a Linux-based cluster, see [Install Giraph on HDInsight Hadoop clusters (Linux)](hdinsight-hadoop-giraph-install-linux.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6b03d-106">本文件的步驟只適用於 Windows HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="6b03d-106">The steps in this document only work with Windows-based HDInsight clusters.</span></span> <span data-ttu-id="6b03d-107">Windows 上的 HDInsight 只提供低於 HDInsight 3.4 的版本。</span><span class="sxs-lookup"><span data-stu-id="6b03d-107">HDInsight is only available on Windows for versions lower than HDInsight 3.4.</span></span> <span data-ttu-id="6b03d-108">Linux 是唯一使用於 HDInsight 3.4 版或更新版本的作業系統。</span><span class="sxs-lookup"><span data-stu-id="6b03d-108">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="6b03d-109">如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。</span><span class="sxs-lookup"><span data-stu-id="6b03d-109">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span> <span data-ttu-id="6b03d-110">如需有關如何在 Linux 型 HDInsight 叢集上安裝 Giraph 的詳細資訊，請參閱[在 HDInsight Hadoop 叢集上安裝 Giraph (Linux)](hdinsight-hadoop-giraph-install-linux.md)。</span><span class="sxs-lookup"><span data-stu-id="6b03d-110">For information on how to install Giraph on a Linux-based HDInsight cluster, see [Install Giraph on HDInsight Hadoop clusters (Linux)](hdinsight-hadoop-giraph-install-linux.md).</span></span>


<span data-ttu-id="6b03d-111">您也可以使用「指令碼動作」 ，在 Azure HDInsight 的任一類型的叢集 (Hadoop、Storm、HBase、Spark) 上安裝 Giraph。</span><span class="sxs-lookup"><span data-stu-id="6b03d-111">You can install Giraph on any type of cluster (Hadoop, Storm, HBase, Spark) on Azure HDInsight by using *Script Action*.</span></span> <span data-ttu-id="6b03d-112">您可以從一個唯讀的 Azure 儲存體 Blob 取得在 HDInsight 叢集上安裝 Giraph 的範例指令碼，網址為 [https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1)。</span><span class="sxs-lookup"><span data-stu-id="6b03d-112">A sample script to install Giraph on an HDInsight cluster is available from a read-only Azure storage blob at [https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1).</span></span> <span data-ttu-id="6b03d-113">範例指令碼只能與 HDInsight 叢集版本 3.1 搭配使用。</span><span class="sxs-lookup"><span data-stu-id="6b03d-113">The sample script works only with HDInsight cluster version 3.1.</span></span> <span data-ttu-id="6b03d-114">如需 HDInsight 叢集版本的詳細資訊，請參閱 [HDInsight 叢集版本](hdinsight-component-versioning.md)。</span><span class="sxs-lookup"><span data-stu-id="6b03d-114">For more information on HDInsight cluster versions, see [HDInsight cluster versions](hdinsight-component-versioning.md).</span></span>

<span data-ttu-id="6b03d-115">**相關文章**</span><span class="sxs-lookup"><span data-stu-id="6b03d-115">**Related articles**</span></span>

* [<span data-ttu-id="6b03d-116">在 HDInsight Hadoop 叢集上安裝 Giraph (Linux)</span><span class="sxs-lookup"><span data-stu-id="6b03d-116">Install Giraph on HDInsight Hadoop clusters (Linux)</span></span>](hdinsight-hadoop-giraph-install-linux.md)
* <span data-ttu-id="6b03d-117">[在 HDInsight 叢集中建立 Hadoop](hdinsight-provision-clusters.md)：建立 HDInsight 叢集的一般資訊。</span><span class="sxs-lookup"><span data-stu-id="6b03d-117">[Create Hadoop clusters in HDInsight](hdinsight-provision-clusters.md): general information on creating HDInsight clusters.</span></span>
* <span data-ttu-id="6b03d-118">[使用指令碼動作來自訂 HDInsight 叢集][hdinsight-cluster-customize]：關於使用指令碼動作來自訂 HDInsight 叢集的一般資訊。</span><span class="sxs-lookup"><span data-stu-id="6b03d-118">[Customize HDInsight cluster using Script Action][hdinsight-cluster-customize]: general information on customizing HDInsight clusters using Script Action.</span></span>
* <span data-ttu-id="6b03d-119">[開發 HDInsight 的指令碼動作指令碼](hdinsight-hadoop-script-actions.md)</span><span class="sxs-lookup"><span data-stu-id="6b03d-119">[Develop Script Action scripts for HDInsight](hdinsight-hadoop-script-actions.md).</span></span>

## <a name="what-is-giraph"></a><span data-ttu-id="6b03d-120">什麼是 Giraph？</span><span class="sxs-lookup"><span data-stu-id="6b03d-120">What is Giraph?</span></span>
<span data-ttu-id="6b03d-121"><a href="http://giraph.apache.org/" target="_blank">Apache Giraph</a> 可讓您利用 Hadoop 執行圖形處理，且可以搭配 Azure HDInsight 一起使用。</span><span class="sxs-lookup"><span data-stu-id="6b03d-121"><a href="http://giraph.apache.org/" target="_blank">Apache Giraph</a> allows you to perform graph processing by using Hadoop, and can be used with Azure HDInsight.</span></span> <span data-ttu-id="6b03d-122">圖形可以模型化物件之間的關聯，例如大型網路 (像是網際網路) 上的路由器之間的連線，或社交網路上的人際關係 (有時稱為社交圖形)。</span><span class="sxs-lookup"><span data-stu-id="6b03d-122">Graphs model relationships between objects, such as the connections between routers on a large network like the Internet, or relationships between people on social networks (sometimes referred to as a social graph).</span></span> <span data-ttu-id="6b03d-123">圖形處理可讓您分析圖形中物件之間的關聯，例如：</span><span class="sxs-lookup"><span data-stu-id="6b03d-123">Graph processing allows you to reason about the relationships between objects in a graph, such as:</span></span>

* <span data-ttu-id="6b03d-124">根據目前的人際關係找出可能的朋友。</span><span class="sxs-lookup"><span data-stu-id="6b03d-124">Identifying potential friends based on your current relationships.</span></span>
* <span data-ttu-id="6b03d-125">識別網路中兩台電腦之間的最短路線。</span><span class="sxs-lookup"><span data-stu-id="6b03d-125">Identifying the shortest route between two computers in a network.</span></span>
* <span data-ttu-id="6b03d-126">計算網頁的頁面排名。</span><span class="sxs-lookup"><span data-stu-id="6b03d-126">Calculating the page rank of webpages.</span></span>

## <a name="install-giraph-using-portal"></a><span data-ttu-id="6b03d-127">使用入口網站安裝 Giraph</span><span class="sxs-lookup"><span data-stu-id="6b03d-127">Install Giraph using portal</span></span>
1. <span data-ttu-id="6b03d-128">使用 [自訂建立] 選項，依[在 HDInsight 中建立 Hadoop 叢集](hdinsight-provision-clusters.md)中的描述開始建立叢集。</span><span class="sxs-lookup"><span data-stu-id="6b03d-128">Start creating a cluster by using the **CUSTOM CREATE** option, as described at [Create Hadoop clusters in HDInsight](hdinsight-provision-clusters.md).</span></span>
2. <span data-ttu-id="6b03d-129">在精靈的 [指令碼動作] 頁面上，按一下 [加入指令碼動作] 以提供有關指令碼動作的詳細資料，如下所示：</span><span class="sxs-lookup"><span data-stu-id="6b03d-129">On the **Script Actions** page of the wizard, click **add script action** to provide details about the script action, as shown below:</span></span>

    <span data-ttu-id="6b03d-130">![使用指令碼動作以自訂叢集](./media/hdinsight-hadoop-giraph-install/hdi-script-action-giraph.png "使用指令碼動作以自訂叢集")</span><span class="sxs-lookup"><span data-stu-id="6b03d-130">![Use Script Action to customize a cluster](./media/hdinsight-hadoop-giraph-install/hdi-script-action-giraph.png "Use Script Action to customize a cluster")</span></span>

    <table border='1'>
        <tr><th><span data-ttu-id="6b03d-131">屬性</span><span class="sxs-lookup"><span data-stu-id="6b03d-131">Property</span></span></th><th><span data-ttu-id="6b03d-132">值</span><span class="sxs-lookup"><span data-stu-id="6b03d-132">Value</span></span></th></tr>
        <tr><td><span data-ttu-id="6b03d-133">名稱</span><span class="sxs-lookup"><span data-stu-id="6b03d-133">Name</span></span></td>
            <td><span data-ttu-id="6b03d-134">指定指令碼動作的名稱。</span><span class="sxs-lookup"><span data-stu-id="6b03d-134">Specify a name for the script action.</span></span> <span data-ttu-id="6b03d-135">例如，<b>安裝 Giraph</b>。</span><span class="sxs-lookup"><span data-stu-id="6b03d-135">For example, <b>Install Giraph</b>.</span></span></td></tr>
        <tr><td><span data-ttu-id="6b03d-136">指令碼 URI</span><span class="sxs-lookup"><span data-stu-id="6b03d-136">Script URI</span></span></td>
            <td><span data-ttu-id="6b03d-137">指定為自訂叢集叫用的指令碼統一資源識別項 (URI)。</span><span class="sxs-lookup"><span data-stu-id="6b03d-137">Specify the Uniform Resource Identifier (URI) to the script that is invoked to customize the cluster.</span></span> <span data-ttu-id="6b03d-138">例如，<i>https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1</i></span><span class="sxs-lookup"><span data-stu-id="6b03d-138">For example, <i>https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1</i></span></span></td></tr>
        <tr><td><span data-ttu-id="6b03d-139">節點類型</span><span class="sxs-lookup"><span data-stu-id="6b03d-139">Node Type</span></span></td>
            <td><span data-ttu-id="6b03d-140">指定執行自訂指令碼的節點。</span><span class="sxs-lookup"><span data-stu-id="6b03d-140">Specify the nodes on which the customization script is run.</span></span> <span data-ttu-id="6b03d-141">您可以選擇 [所有節點]<b></b>、[僅限前端節點]<b></b> 或 [僅限背景工作節點]<b></b>。</span><span class="sxs-lookup"><span data-stu-id="6b03d-141">You can choose <b>All nodes</b>, <b>Head nodes only</b>, or <b>Worker nodes only</b>.</span></span>
        <tr><td><span data-ttu-id="6b03d-142">參數</span><span class="sxs-lookup"><span data-stu-id="6b03d-142">Parameters</span></span></td>
            <td><span data-ttu-id="6b03d-143">如果指令碼要求，請指定參數。</span><span class="sxs-lookup"><span data-stu-id="6b03d-143">Specify the parameters, if required by the script.</span></span> <span data-ttu-id="6b03d-144">要安裝 Giraph 的指令碼不需要任何參數，因此可以讓此處空白。</span><span class="sxs-lookup"><span data-stu-id="6b03d-144">The script to install Giraph does not require any parameters, so you can leave this blank.</span></span></td></tr>
    </table>

    <span data-ttu-id="6b03d-145">您可以加入一個以上的指令碼動作，以在叢集上安裝多個元件。</span><span class="sxs-lookup"><span data-stu-id="6b03d-145">You can add more than one script action to install multiple components on the cluster.</span></span> <span data-ttu-id="6b03d-146">加入指令碼之後，請按一下核取記號以開始建立叢集。</span><span class="sxs-lookup"><span data-stu-id="6b03d-146">After you have added the scripts, click the checkmark to start creating the cluster.</span></span>

## <a name="use-giraph"></a><span data-ttu-id="6b03d-147">使用 Giraph</span><span class="sxs-lookup"><span data-stu-id="6b03d-147">Use Giraph</span></span>
<span data-ttu-id="6b03d-148">我們使用 SimpleShortestPathsComputation 範例來示範在圖形中的物件之間找出最短路徑的基本<a href = "http://people.apache.org/~edwardyoon/documents/pregel.pdf">Pregel</a> 實作。</span><span class="sxs-lookup"><span data-stu-id="6b03d-148">We use the SimpleShortestPathsComputation example to demonstrate the basic <a href = "http://people.apache.org/~edwardyoon/documents/pregel.pdf">Pregel</a> implementation for finding the shortest path between objects in a graph.</span></span> <span data-ttu-id="6b03d-149">請使用下列步驟來上傳範例資料及範例 jar，使用 SimpleShortestPathsComputation 範例執行工作，然後檢視結果。</span><span class="sxs-lookup"><span data-stu-id="6b03d-149">Use the following steps to upload the sample data and the sample jar, run a job by using the SimpleShortestPathsComputation example, and then view the results.</span></span>

1. <span data-ttu-id="6b03d-150">將範例資料檔案上傳至 Azure Blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="6b03d-150">Upload a sample data file to Azure Blob storage.</span></span> <span data-ttu-id="6b03d-151">在本機工作站上，建立名為 **tiny_graph.txt** 的新檔案。</span><span class="sxs-lookup"><span data-stu-id="6b03d-151">On your local workstation, create a new file named **tiny_graph.txt**.</span></span> <span data-ttu-id="6b03d-152">應該包含下列幾行：</span><span class="sxs-lookup"><span data-stu-id="6b03d-152">It should contain the following lines:</span></span>

        [0,0,[[1,1],[3,3]]]
        [1,0,[[0,1],[2,2],[3,1]]]
        [2,0,[[1,2],[4,4]]]
        [3,0,[[0,3],[1,1],[4,4]]]
        [4,0,[[3,4],[2,4]]]

    <span data-ttu-id="6b03d-153">將 tiny_graph.txt 檔案上傳至 HDInsight 叢集的主要儲存體。</span><span class="sxs-lookup"><span data-stu-id="6b03d-153">Upload the tiny_graph.txt file to the primary storage for your HDInsight cluster.</span></span> <span data-ttu-id="6b03d-154">如需有關如何上傳資料的指示，請參閱 [在 HDInsight 上將 Hadoop 工作的資料上傳](hdinsight-upload-data.md)。</span><span class="sxs-lookup"><span data-stu-id="6b03d-154">For instructions on how to upload data, see [Upload data for Hadoop jobs in HDInsight](hdinsight-upload-data.md).</span></span>

    <span data-ttu-id="6b03d-155">這項資料會使用 [source_id, source_value,[[dest_id], [edge_value],...]][source\_id, source\_value,[[dest\_id], [edge\_value],...]] 格式，描述一個有向圖形中物件之間的關聯性。</span><span class="sxs-lookup"><span data-stu-id="6b03d-155">This data describes a relationship between objects in a directed graph, by using the format [source\_id, source\_value,[[dest\_id], [edge\_value],...]].</span></span> <span data-ttu-id="6b03d-156">每一行代表 **source\_id** 物件和一或多個 **dest\_id** 物件之間的關聯性。</span><span class="sxs-lookup"><span data-stu-id="6b03d-156">Each line represents a relationship between a **source\_id** object and one or more **dest\_id** objects.</span></span> <span data-ttu-id="6b03d-157">**edge\_value** (或權數) 可以視為 **source_id** 和 **dest\_id** 之間的連線強度或距離。</span><span class="sxs-lookup"><span data-stu-id="6b03d-157">The **edge\_value** (or weight) can be thought of as the strength or distance of the connection between **source_id** and **dest\_id**.</span></span>

    <span data-ttu-id="6b03d-158">如果使用值 (或權數) 當做物件之間的距離繪製出來，上述資料可能如下圖所示：</span><span class="sxs-lookup"><span data-stu-id="6b03d-158">Drawn out, and using the value (or weight) as the distance between objects, the above data might look like this:</span></span>

    ![tiny_graph.txt drawn as circles with lines of varying distance between](./media/hdinsight-hadoop-giraph-install/giraph-graph.png)
2. <span data-ttu-id="6b03d-160">執行 SimpleShortestPathsComputation 範例。</span><span class="sxs-lookup"><span data-stu-id="6b03d-160">Run the SimpleShortestPathsComputation example.</span></span> <span data-ttu-id="6b03d-161">使用 tiny_graph.txt 檔案做為輸入，即可使用下列 Azure PowerShell Cmdlet 來執行此範例。</span><span class="sxs-lookup"><span data-stu-id="6b03d-161">Use the following Azure PowerShell cmdlets to run the example by using the tiny_graph.txt file as input.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="6b03d-162">使用 Azure Service Manager 管理 HDInsight 資源的 Azure PowerShell 支援已**被取代**，並已在 2017 年 1 月 1 日移除。</span><span class="sxs-lookup"><span data-stu-id="6b03d-162">Azure PowerShell support for managing HDInsight resources using Azure Service Manager is **deprecated**, and was removed on January 1, 2017.</span></span> <span data-ttu-id="6b03d-163">本文件中的步驟會使用可與 Azure Resource Manager 搭配使用的新 HDInsight Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="6b03d-163">The steps in this document use the new HDInsight cmdlets that work with Azure Resource Manager.</span></span>
    >
    > <span data-ttu-id="6b03d-164">請遵循 [安裝和設定 Azure PowerShell](/powershell/azureps-cmdlets-docs) 中的步驟來安裝最新版的 Azure PowerShell。</span><span class="sxs-lookup"><span data-stu-id="6b03d-164">Please follow the steps in [Install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) to install the latest version of Azure PowerShell.</span></span> <span data-ttu-id="6b03d-165">如果您需要修改指令碼才能使用適用於 Azure Resource Manager 的新 Cmdlet，請參閱 [移轉至以 Azure Resource Manager 為基礎的開發工具 (適用於 HDInsight 叢集)](hdinsight-hadoop-development-using-azure-resource-manager.md) ，以取得詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="6b03d-165">If you have scripts that need to be modified to use the new cmdlets that work with Azure Resource Manager, see [Migrating to Azure Resource Manager-based development tools for HDInsight clusters](hdinsight-hadoop-development-using-azure-resource-manager.md) for more information.</span></span>

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
    # Create the definition
    $jobDefinition = New-AzureHDInsightMapReduceJobDefinition
        -JarFile $jarFile
        -ClassName "org.apache.giraph.GiraphRunner"
        -Arguments $jobArguments

    # Run the job, write output to the Azure PowerShell window
    $job = Start-AzureHDInsightJob -Cluster $clusterName -JobDefinition $jobDefinition
    Write-Host "Wait for the job to complete ..." -ForegroundColor Green
    Wait-AzureHDInsightJob -Job $job
    Write-Host "STDERR"
    Get-AzureHDInsightJobOutput -Cluster $clusterName -JobId $job.JobId -StandardError
    Write-Host "Display the standard output ..." -ForegroundColor Green
    Get-AzureHDInsightJobOutput -Cluster $clusterName -JobId $job.JobId -StandardOutput
    ```

    <span data-ttu-id="6b03d-166">在上述範例中，利用您已安裝 Giraph 的 HDInsight 叢集名稱取代 **clustername** 。</span><span class="sxs-lookup"><span data-stu-id="6b03d-166">In the above example, replace **clustername** with the name of your HDInsight cluster that has Giraph installed.</span></span>
3. <span data-ttu-id="6b03d-167">檢視結果。</span><span class="sxs-lookup"><span data-stu-id="6b03d-167">View the results.</span></span> <span data-ttu-id="6b03d-168">工作完成之後，結果會儲存於 **wasb:///example/out/shotestpaths** 資料夾中的兩個輸出檔案。</span><span class="sxs-lookup"><span data-stu-id="6b03d-168">Once the job has finished, the results will be stored in two output files in the **wasb:///example/out/shotestpaths** folder.</span></span> <span data-ttu-id="6b03d-169">這些檔案稱為 **part-m-00001** 和 **part-m-00002**。</span><span class="sxs-lookup"><span data-stu-id="6b03d-169">The files are called **part-m-00001** and **part-m-00002**.</span></span> <span data-ttu-id="6b03d-170">執行下列步驟來下載和檢視輸出：</span><span class="sxs-lookup"><span data-stu-id="6b03d-170">Perform the following steps to download and view the output:</span></span>

    ```powershell
    $subscriptionName = "<SubscriptionName>"       # Azure subscription name
    $storageAccountName = "<StorageAccountName>"   # Azure Storage account name
    $containerName = "<ContainerName>"             # Blob storage container name

    # Select the current subscription
    Select-AzureSubscription $subscriptionName

    # Create the Storage account context object
    $storageAccountKey = Get-AzureStorageKey $storageAccountName | %{ $_.Primary }
    $storageContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey

    # Download the job output to the workstation
    Get-AzureStorageBlobContent -Container $containerName -Blob example/output/shortestpaths/part-m-00001 -Context $storageContext -Force
    Get-AzureStorageBlobContent -Container $containerName -Blob example/output/shortestpaths/part-m-00002 -Context $storageContext -Force
    ```

    <span data-ttu-id="6b03d-171">這會在工作站上目前的目錄中建立 **example/output/shortestpaths** 目錄結構，並將兩個輸出檔案下載到該位置。</span><span class="sxs-lookup"><span data-stu-id="6b03d-171">This will create the **example/output/shortestpaths** directory structure in the current directory on your workstation, and download the two output files to that location.</span></span>

    <span data-ttu-id="6b03d-172">使用 **Cat** Cmdlet 顯示檔案的內容：</span><span class="sxs-lookup"><span data-stu-id="6b03d-172">Use the **Cat** cmdlet to display the contents of the files:</span></span>

        Cat example/output/shortestpaths/part*

    <span data-ttu-id="6b03d-173">輸出應該如下所示：</span><span class="sxs-lookup"><span data-stu-id="6b03d-173">The output should appear similar to the following:</span></span>

        0    1.0
        4    5.0
        2    2.0
        1    0.0
        3    1.0

    <span data-ttu-id="6b03d-174">SimpleShortestPathComputation 範例已刻意設計成從物件識別碼 1 開始，尋找前往其他物件的最短路徑。</span><span class="sxs-lookup"><span data-stu-id="6b03d-174">The SimpleShortestPathComputation example is hard coded to start with object ID 1 and find the shortest path to other objects.</span></span> <span data-ttu-id="6b03d-175">因此，輸出應該會顯示 `destination_id distance`，其中 distance 是物件識別碼 1 與目標識別碼之間經過的邊緣的值 (或權數)。</span><span class="sxs-lookup"><span data-stu-id="6b03d-175">So the output should be read as `destination_id distance`, where distance is the value (or weight) of the edges traveled between object ID 1 and the target ID.</span></span>

    <span data-ttu-id="6b03d-176">顯現為圖形後，您可以走過識別碼 1 與其他所有物件之間的最短路徑來驗證結果。</span><span class="sxs-lookup"><span data-stu-id="6b03d-176">Visualizing this, you can verify the results by traveling the shortest paths between ID 1 and all other objects.</span></span> <span data-ttu-id="6b03d-177">請注意，識別碼 1 和識別碼 4 之間的最短路徑為 5。</span><span class="sxs-lookup"><span data-stu-id="6b03d-177">Note that the shortest path between ID 1 and ID 4 is 5.</span></span> <span data-ttu-id="6b03d-178">這是<span style="color:orange">識別碼 1 和 3 之間</span>加上<span style="color:red">識別碼 3 和 4 之間</span>的總距離。</span><span class="sxs-lookup"><span data-stu-id="6b03d-178">This is the total distance between <span style="color:orange">ID 1 and 3</span>, and then <span style="color:red">ID 3 and 4</span>.</span></span>

    ![Drawing of objects as circles with shortest paths drawn between](./media/hdinsight-hadoop-giraph-install/giraph-graph-out.png)

## <a name="install-giraph-using-aure-powershell"></a><span data-ttu-id="6b03d-180">使用 Aure PowerShell 安裝 Giraph</span><span class="sxs-lookup"><span data-stu-id="6b03d-180">Install Giraph using Aure PowerShell</span></span>
<span data-ttu-id="6b03d-181">請參閱[使用指令碼動作來自訂 HDInsight 叢集](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell)。</span><span class="sxs-lookup"><span data-stu-id="6b03d-181">See [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span></span>  <span data-ttu-id="6b03d-182">此範例示範如何使用 Azure PowerShell 安裝 Spark。</span><span class="sxs-lookup"><span data-stu-id="6b03d-182">The sample demonstrates how to install Spark using Azure PowerShell.</span></span> <span data-ttu-id="6b03d-183">您需要自訂指令碼以使用 [https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1)。</span><span class="sxs-lookup"><span data-stu-id="6b03d-183">You need to customize the script to use [https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1).</span></span>

## <a name="install-giraph-using-net-sdk"></a><span data-ttu-id="6b03d-184">使用 .NET SDK 安裝 Giraph</span><span class="sxs-lookup"><span data-stu-id="6b03d-184">Install Giraph using .NET SDK</span></span>
<span data-ttu-id="6b03d-185">請參閱[使用指令碼動作來自訂 HDInsight 叢集](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell)。</span><span class="sxs-lookup"><span data-stu-id="6b03d-185">See [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span></span> <span data-ttu-id="6b03d-186">此範例示範如何使用 .NET SDK 安裝 Spark。</span><span class="sxs-lookup"><span data-stu-id="6b03d-186">The sample demonstrates how to install Spark using the .NET SDK.</span></span> <span data-ttu-id="6b03d-187">您需要自訂指令碼以使用 [https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1)。</span><span class="sxs-lookup"><span data-stu-id="6b03d-187">You need to customize the script to use [https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1).</span></span>

## <a name="see-also"></a><span data-ttu-id="6b03d-188">另請參閱</span><span class="sxs-lookup"><span data-stu-id="6b03d-188">See also</span></span>
* [<span data-ttu-id="6b03d-189">在 HDInsight Hadoop 叢集上安裝 Giraph (Linux)</span><span class="sxs-lookup"><span data-stu-id="6b03d-189">Install Giraph on HDInsight Hadoop clusters (Linux)</span></span>](hdinsight-hadoop-giraph-install-linux.md)
* <span data-ttu-id="6b03d-190">[在 HDInsight 叢集中建立 Hadoop](hdinsight-provision-clusters.md)：建立 HDInsight 叢集的一般資訊。</span><span class="sxs-lookup"><span data-stu-id="6b03d-190">[Create Hadoop clusters in HDInsight](hdinsight-provision-clusters.md): general information on creating HDInsight clusters.</span></span>
* <span data-ttu-id="6b03d-191">[使用指令碼動作來自訂 HDInsight 叢集][hdinsight-cluster-customize]：關於使用指令碼動作來自訂 HDInsight 叢集的一般資訊。</span><span class="sxs-lookup"><span data-stu-id="6b03d-191">[Customize HDInsight cluster using Script Action][hdinsight-cluster-customize]: general information on customizing HDInsight clusters using Script Action.</span></span>
* <span data-ttu-id="6b03d-192">[開發 HDInsight 的指令碼動作指令碼](hdinsight-hadoop-script-actions.md)</span><span class="sxs-lookup"><span data-stu-id="6b03d-192">[Develop Script Action scripts for HDInsight](hdinsight-hadoop-script-actions.md).</span></span>
* <span data-ttu-id="6b03d-193">[在 HDInsight 叢集上安裝和使用 Spark][hdinsight-install-spark]：關於安裝 Spark 的指令碼動作範例。</span><span class="sxs-lookup"><span data-stu-id="6b03d-193">[Install and use Spark on HDInsight clusters][hdinsight-install-spark]: Script Action sample about installing Spark.</span></span>
* <span data-ttu-id="6b03d-194">[在 HDInsight 叢集上安裝 R][hdinsight-install-r]：關於安裝 R 的指令碼動作範例。</span><span class="sxs-lookup"><span data-stu-id="6b03d-194">[Install R on HDInsight clusters][hdinsight-install-r]: Script Action sample about installing R.</span></span>
* <span data-ttu-id="6b03d-195">[在 HDInsight 叢集上安裝 Solr](hdinsight-hadoop-solr-install.md)：關於安裝 Solr 的指令碼動作範例。</span><span class="sxs-lookup"><span data-stu-id="6b03d-195">[Install Solr on HDInsight clusters](hdinsight-hadoop-solr-install.md): Script Action sample about installing Solr.</span></span>

[tools]: https://github.com/Blackmist/hdinsight-tools
[aps]: http://azure.microsoft.com/documentation/articles/install-configure-powershell/

[powershell-install]: /powershell/azureps-cmdlets-docs
[hdinsight-provision]: hdinsight-provision-clusters.md
[hdinsight-install-r]: hdinsight-hadoop-r-scripts.md
[hdinsight-install-spark]: hdinsight-hadoop-spark-install.md
[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster.md
