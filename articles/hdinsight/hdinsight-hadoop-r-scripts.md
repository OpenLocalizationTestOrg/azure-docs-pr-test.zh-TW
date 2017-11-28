---
title: "在 HDInsight 中使用 R 來自訂叢集 - Azure | Microsoft Docs"
description: "了解如何使用指令碼動作安裝 R，以及在 HDInsight 叢集上使用 R。"
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: be851270-afa5-4af0-a69e-2d343a4deeb7
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: 5b9b793d49217acd9f0c6c518596a7afb5600d69
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="install-and-use-r-on-hdinsight-hadoop-clusters"></a><span data-ttu-id="05d35-103">在 HDInsight Hadoop 叢集上安裝和使用 R</span><span class="sxs-lookup"><span data-stu-id="05d35-103">Install and use R on HDInsight Hadoop clusters</span></span>

<span data-ttu-id="05d35-104">了解如何使用指令碼動作來以 R 自訂以 Windows 為基礎的 HDInsight 叢集，以及如何在 HDInsight 叢集上使用 R。</span><span class="sxs-lookup"><span data-stu-id="05d35-104">Learn how to customize Windows based HDInsight cluster with R using Script Action, and how to use R on HDInsight clusters.</span></span> <span data-ttu-id="05d35-105">[HDInsight 供應項目](https://azure.microsoft.com/pricing/details/hdinsight/)包括隨附於 HDInsight 叢集的 R 伺服器。</span><span class="sxs-lookup"><span data-stu-id="05d35-105">The [HDInsight offering](https://azure.microsoft.com/pricing/details/hdinsight/) includes R Server as part of your HDInsight cluster.</span></span> <span data-ttu-id="05d35-106">這可讓 R 指令碼使用 MapReduce 和 Spark 來執行分散式計算。</span><span class="sxs-lookup"><span data-stu-id="05d35-106">This allows R scripts to use MapReduce and Spark to run distributed computations.</span></span> <span data-ttu-id="05d35-107">如需詳細資訊，請參閱[開始使用 HDInsight 上的 R 伺服器](hdinsight-hadoop-r-server-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="05d35-107">For more information, see [Get started using R Server on HDInsight](hdinsight-hadoop-r-server-get-started.md).</span></span> <span data-ttu-id="05d35-108">如需搭配以 Linux 為基礎的叢集使用 R 的詳細資訊，請參閱[在 HDInsight Hadoop 叢集上安裝和使用 R (Linux)](hdinsight-hadoop-r-scripts-linux.md)。</span><span class="sxs-lookup"><span data-stu-id="05d35-108">For information on using R with a Linux-based cluster, see [Install and use R on HDinsight Hadoop clusters (Linux)](hdinsight-hadoop-r-scripts-linux.md).</span></span>

<span data-ttu-id="05d35-109">您也可以使用「指令碼動作」，在 Azure HDInsight 的任一類型的叢集 (Hadoop、Storm、HBase、Spark) 上安裝 R。</span><span class="sxs-lookup"><span data-stu-id="05d35-109">You can install R on any type of cluster (Hadoop, Storm, HBase, Spark) on Azure HDInsight by using *Script Action*.</span></span> <span data-ttu-id="05d35-110">您可以從一個唯讀的 Azure 儲存體 Blob 取得在 HDInsight 叢集上安裝 R 的範例指令碼，網址為 [https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1](https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1)。</span><span class="sxs-lookup"><span data-stu-id="05d35-110">A sample script to install R on an HDInsight cluster is available from a read-only Azure storage blob at [https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1](https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1).</span></span>

<span data-ttu-id="05d35-111">**相關文章**</span><span class="sxs-lookup"><span data-stu-id="05d35-111">**Related articles**</span></span>

* [<span data-ttu-id="05d35-112">在 HDInsight Hadoop 叢集上安裝和使用 R (Linux)</span><span class="sxs-lookup"><span data-stu-id="05d35-112">Install and use R on HDinsight Hadoop clusters (Linux)</span></span>](hdinsight-hadoop-r-scripts-linux.md)
* <span data-ttu-id="05d35-113">[在 HDInsight 中建立 Hadoop 叢集](hdinsight-hadoop-provision-linux-clusters.md)：有關建立 HDInsight 叢集的一般資訊</span><span class="sxs-lookup"><span data-stu-id="05d35-113">[Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md): general information on creating HDInsight clusters</span></span>
* <span data-ttu-id="05d35-114">[使用指令碼動作來自訂 HDInsight 叢集][hdinsight-cluster-customize]：有關使用指令碼動作來自訂 HDInsight 叢集的一般資訊。</span><span class="sxs-lookup"><span data-stu-id="05d35-114">[Customize HDInsight cluster using Script Action][hdinsight-cluster-customize]: general information on customizing HDInsight clusters using Script Action</span></span>
* [<span data-ttu-id="05d35-115">開發 HDInsight 的指令碼動作指令碼</span><span class="sxs-lookup"><span data-stu-id="05d35-115">Develop Script Action scripts for HDInsight</span></span>](hdinsight-hadoop-script-actions.md)

## <a name="what-is-r"></a><span data-ttu-id="05d35-116">什麼是 R？</span><span class="sxs-lookup"><span data-stu-id="05d35-116">What is R?</span></span>
<span data-ttu-id="05d35-117"><a href="http://www.r-project.org/" target="_blank">R Project for Statistical Computing</a> 是一個用於統計計算的開放原始碼語言和環境。</span><span class="sxs-lookup"><span data-stu-id="05d35-117">The <a href="http://www.r-project.org/" target="_blank">R Project for Statistical Computing</a> is an open source language and environment for statistical computing.</span></span> <span data-ttu-id="05d35-118">R 提供數百個內建的統計函數及它自己的程式設計語言，此語言結合了函數型和物件導向程式設計的層面。</span><span class="sxs-lookup"><span data-stu-id="05d35-118">R provides hundreds of build-in statistical functions and its own programming language that combines aspects of functional and object-oriented programming.</span></span> <span data-ttu-id="05d35-119">它也提供廣泛的圖形功能。</span><span class="sxs-lookup"><span data-stu-id="05d35-119">It also provides extensive graphical capabilities.</span></span> <span data-ttu-id="05d35-120">R 是各種不同廣泛領域中，大多數專業統計人員和科學家慣用的程式設計環境。</span><span class="sxs-lookup"><span data-stu-id="05d35-120">R is the preferred programming environment for most professional statisticians and scientists in a wide variety of fields.</span></span>

<span data-ttu-id="05d35-121">R 與 Azure Blob 儲存體 (WASB) 相容，因此便可在 HDInsight 上使用 R 來處理儲存在該處的資料。</span><span class="sxs-lookup"><span data-stu-id="05d35-121">R is compatible with Azure Blob Storage (WASB) so that data that is stored there can be processed using R on HDInsight.</span></span>  

## <a name="install-r"></a><span data-ttu-id="05d35-122">安裝 R</span><span class="sxs-lookup"><span data-stu-id="05d35-122">Install R</span></span>
<span data-ttu-id="05d35-123">您可以從 Azure 儲存體中的唯讀 Blob，取得用以在 HDInsight 叢集上安裝 R 的[範例指令碼](https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1)。</span><span class="sxs-lookup"><span data-stu-id="05d35-123">A [sample script](https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1) to install R on an HDInsight cluster is available from a read-only blob in Azure Storage.</span></span> <span data-ttu-id="05d35-124">本節提供有關如何在使用 Azure 入口網站建立叢集時使用範例指令碼的指示。</span><span class="sxs-lookup"><span data-stu-id="05d35-124">This section provides instructions about how to use the sample script while creating the cluster using the Azure Portal.</span></span>

> [!NOTE]
> <span data-ttu-id="05d35-125">範例指令碼是在 HDInsight 叢集版本 3.1 中所推出。</span><span class="sxs-lookup"><span data-stu-id="05d35-125">The sample script was introduced with HDInsight cluster version 3.1.</span></span> <span data-ttu-id="05d35-126">如需 HDInsight 叢集版本的詳細資訊，請參閱 [HDInsight 叢集版本](hdinsight-component-versioning.md)。</span><span class="sxs-lookup"><span data-stu-id="05d35-126">For more information about  HDInsight cluster versions, see [HDInsight cluster versions](hdinsight-component-versioning.md).</span></span>
>
>

1. <span data-ttu-id="05d35-127">當您從入口網站建立 HDInsight 叢集時，請按一下 [選擇性組態]，然後按一下 [指令碼動作]。</span><span class="sxs-lookup"><span data-stu-id="05d35-127">When you create an HDInsight cluster from the Portal, click **Optional Configuration**, and then click **Script Actions**.</span></span>
2. <span data-ttu-id="05d35-128">在 [指令碼動作] 頁面上，輸入下列值：</span><span class="sxs-lookup"><span data-stu-id="05d35-128">On the **Script Actions** page, enter the following values:</span></span>

    <span data-ttu-id="05d35-129">![使用指令碼動作以自訂叢集](./media/hdinsight-hadoop-r-scripts/hdi-r-script-action.png "使用指令碼動作以自訂叢集")</span><span class="sxs-lookup"><span data-stu-id="05d35-129">![Use Script Action to customize a cluster](./media/hdinsight-hadoop-r-scripts/hdi-r-script-action.png "Use Script Action to customize a cluster")</span></span>

    <table border='1'>
        <tr><th><span data-ttu-id="05d35-130">屬性</span><span class="sxs-lookup"><span data-stu-id="05d35-130">Property</span></span></th><th><span data-ttu-id="05d35-131">值</span><span class="sxs-lookup"><span data-stu-id="05d35-131">Value</span></span></th></tr>
        <tr><td><span data-ttu-id="05d35-132">名稱</span><span class="sxs-lookup"><span data-stu-id="05d35-132">Name</span></span></td>
            <td><span data-ttu-id="05d35-133">指定指令碼動作的名稱，例如<b>安裝 R</b>。</span><span class="sxs-lookup"><span data-stu-id="05d35-133">Specify a name for the script action, for example, <b>Install R</b>.</span></span></td></tr>
        <tr><td><span data-ttu-id="05d35-134">指令碼 URI</span><span class="sxs-lookup"><span data-stu-id="05d35-134">Script URI</span></span></td>
            <td><span data-ttu-id="05d35-135">指定為了自訂叢集所叫用之指令碼的 URI，例如 <i>https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1</i></span><span class="sxs-lookup"><span data-stu-id="05d35-135">Specify the URI to the script that is invoked to customize the cluster, for example, <i>https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1</i></span></span></td></tr>
        <tr><td><span data-ttu-id="05d35-136">節點類型</span><span class="sxs-lookup"><span data-stu-id="05d35-136">Node Type</span></span></td>
            <td><span data-ttu-id="05d35-137">指定執行自訂指令碼的節點。</span><span class="sxs-lookup"><span data-stu-id="05d35-137">Specify the nodes on which the customization script is run.</span></span> <span data-ttu-id="05d35-138">您可以選擇 [所有節點]<b></b>、[僅限前端節點]<b></b> 或 [僅限背景工作節點]<b></b>。</span><span class="sxs-lookup"><span data-stu-id="05d35-138">You can choose <b>All Nodes</b>, <b>Head nodes only</b>, or <b>Worker nodes</b> only.</span></span>
        <tr><td><span data-ttu-id="05d35-139">參數</span><span class="sxs-lookup"><span data-stu-id="05d35-139">Parameters</span></span></td>
            <td><span data-ttu-id="05d35-140">如果指令碼要求，請指定參數。</span><span class="sxs-lookup"><span data-stu-id="05d35-140">Specify the parameters, if required by the script.</span></span> <span data-ttu-id="05d35-141">不過，用來安裝 R 的指令碼不需要任何參數，因此可以將此欄位留白。</span><span class="sxs-lookup"><span data-stu-id="05d35-141">However, the script to install R does not require any parameters, so you can leave this blank.</span></span></td></tr>
    </table>

    <span data-ttu-id="05d35-142">您可以加入一個以上的指令碼動作，以在叢集上安裝多個元件。</span><span class="sxs-lookup"><span data-stu-id="05d35-142">You can add more than one script action to install multiple components on the cluster.</span></span> <span data-ttu-id="05d35-143">加入指令碼之後，請按一下核取記號以開始建立叢集。</span><span class="sxs-lookup"><span data-stu-id="05d35-143">After you have added the scripts, click the check mark to start crating the cluster.</span></span>

<span data-ttu-id="05d35-144">您也可以使用 Azure PowerShell 或 HDInsight .NET SDK，使用指令碼在 HDInsight 上安裝 R。</span><span class="sxs-lookup"><span data-stu-id="05d35-144">You can also use the script to install R on HDInsight by using Azure PowerShell or the HDInsight .NET SDK.</span></span> <span data-ttu-id="05d35-145">此文章稍後會提供這些程序的指示。</span><span class="sxs-lookup"><span data-stu-id="05d35-145">Instructions for these procedures are provided later in this article.</span></span>

## <a name="run-r-scripts"></a><span data-ttu-id="05d35-146">執行 R 指令碼</span><span class="sxs-lookup"><span data-stu-id="05d35-146">Run R scripts</span></span>
<span data-ttu-id="05d35-147">本節說明如何使用 HDInsight 在 Hadoop 叢集上執行 R 指令碼。</span><span class="sxs-lookup"><span data-stu-id="05d35-147">This section describes how to run an R script on the Hadoop cluster with HDInsight.</span></span>

1. <span data-ttu-id="05d35-148">**建立與叢集的遠端桌面連線**：從入口網站，針對您所建立且已安裝 R 的叢集啟用遠端桌面，然後連線到叢集。</span><span class="sxs-lookup"><span data-stu-id="05d35-148">**Establish a Remote Desktop connection to the cluster**: From the Portal, enable Remote Desktop for the cluster you created with R installed, and then connect to the cluster.</span></span> <span data-ttu-id="05d35-149">如需指示，請參閱[使用 RDP 連接至 HDInsight 叢集](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp)。</span><span class="sxs-lookup"><span data-stu-id="05d35-149">For instructions, see [Connect to HDInsight clusters using RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span></span>
2. <span data-ttu-id="05d35-150">**開啟 R 主控台**：R 安裝會在前端節點的桌面上放置 R 主控台的連結。</span><span class="sxs-lookup"><span data-stu-id="05d35-150">**Open the R console**: The R installation puts a link to the R console on the desktop of the head node.</span></span> <span data-ttu-id="05d35-151">按一下該連結以開啟 R 主控台。</span><span class="sxs-lookup"><span data-stu-id="05d35-151">Click on it to open the R console.</span></span>
3. <span data-ttu-id="05d35-152">**執行 R 指令碼**：您可以透過貼上、選取然後按 Enter 的方式，直接從 R 主控台執行 R 指令碼。</span><span class="sxs-lookup"><span data-stu-id="05d35-152">**Run the R script**: The R script can be run directly from the R console by pasting it, selecting it, and pressing ENTER.</span></span> <span data-ttu-id="05d35-153">以下是一個簡單的範例指令碼，此指令碼會產生數字 1 到 100，然後將它們乘以 2。</span><span class="sxs-lookup"><span data-stu-id="05d35-153">Here is a simple example script that generates the numbers 1 to 100 and then multiplies them by 2.</span></span>

        library(rmr2)
        library(rhdfs)
        ints = to.dfs(1:100)
        calc = mapreduce(input = ints, map = function(k, v) cbind(v, 2*v))
        from.dfs(calc)

<span data-ttu-id="05d35-154">前兩行會呼叫與 R 一起安裝的 RHadoop 程式庫。最後一行會將結果列印到主控台。</span><span class="sxs-lookup"><span data-stu-id="05d35-154">The first two lines call the RHadoop libraries that are installed with R. The final line prints the results to the console.</span></span> <span data-ttu-id="05d35-155">輸出看起來應該會像下面這樣：</span><span class="sxs-lookup"><span data-stu-id="05d35-155">The output should look like this:</span></span>

    [1,]  1 2
    [2,]  2 4
    .
    .
    .
    [98,]  98 196
    [99,]  99 198
    [100,] 100 200


## <a name="install-r-using-aure-powershell"></a><span data-ttu-id="05d35-156">使用 Azure PowerShell 安裝 R</span><span class="sxs-lookup"><span data-stu-id="05d35-156">Install R using Aure PowerShell</span></span>
<span data-ttu-id="05d35-157">請參閱[使用指令碼動作來自訂 HDInsight 叢集](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell)。</span><span class="sxs-lookup"><span data-stu-id="05d35-157">See [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span></span>  <span data-ttu-id="05d35-158">此範例示範如何使用 Azure PowerShell 安裝 Spark。</span><span class="sxs-lookup"><span data-stu-id="05d35-158">The sample demonstrates how to install Spark using Azure PowerShell.</span></span> <span data-ttu-id="05d35-159">您需要自訂指令碼以使用 [https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1](https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1)。</span><span class="sxs-lookup"><span data-stu-id="05d35-159">You need to customize the script to use [https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1](https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1).</span></span>

## <a name="install-r-using-net-sdk"></a><span data-ttu-id="05d35-160">使用 .NET SDK 安裝 R</span><span class="sxs-lookup"><span data-stu-id="05d35-160">Install R using .NET SDK</span></span>
<span data-ttu-id="05d35-161">請參閱[使用指令碼動作來自訂 HDInsight 叢集](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell)。</span><span class="sxs-lookup"><span data-stu-id="05d35-161">See [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span></span> <span data-ttu-id="05d35-162">此範例示範如何使用 .NET SDK 安裝 Spark。</span><span class="sxs-lookup"><span data-stu-id="05d35-162">The sample demonstrates how to install Spark using the .NET SDK.</span></span> <span data-ttu-id="05d35-163">您需要自訂指令碼以使用 [https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1](https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps11)。</span><span class="sxs-lookup"><span data-stu-id="05d35-163">You need to customize the script to use [https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1](https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps11).</span></span>

## <a name="see-also"></a><span data-ttu-id="05d35-164">另請參閱</span><span class="sxs-lookup"><span data-stu-id="05d35-164">See also</span></span>
* [<span data-ttu-id="05d35-165">在 HDInsight Hadoop 叢集上安裝和使用 R (Linux)</span><span class="sxs-lookup"><span data-stu-id="05d35-165">Install and use R on HDinsight Hadoop clusters (Linux)</span></span>](hdinsight-hadoop-r-scripts-linux.md)
* <span data-ttu-id="05d35-166">[在 HDInsight 中建立 Hadoop 叢集](hdinsight-hadoop-provision-linux-clusters.md)：有關建立 HDInsight 叢集的一般資訊</span><span class="sxs-lookup"><span data-stu-id="05d35-166">[Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md): general information on creating HDInsight clusters</span></span>
* <span data-ttu-id="05d35-167">[使用指令碼動作來自訂 HDInsight 叢集][hdinsight-cluster-customize]：有關使用指令碼動作來自訂 HDInsight 叢集的一般資訊。</span><span class="sxs-lookup"><span data-stu-id="05d35-167">[Customize HDInsight cluster using Script Action][hdinsight-cluster-customize]: general information on customizing HDInsight clusters using Script Action</span></span>
* [<span data-ttu-id="05d35-168">開發 HDInsight 的指令碼動作指令碼</span><span class="sxs-lookup"><span data-stu-id="05d35-168">Develop Script Action scripts for HDInsight</span></span>](hdinsight-hadoop-script-actions.md)
* <span data-ttu-id="05d35-169">[在 HDInsight 叢集上安裝和使用 Spark][hdinsight-install-spark]：有關安裝 Spark 的指令碼動作範例</span><span class="sxs-lookup"><span data-stu-id="05d35-169">[Install and use Spark on HDInsight clusters][hdinsight-install-spark]: Script Action sample about installing Spark</span></span>
* <span data-ttu-id="05d35-170">[在 HDInsight 叢集上安裝 Giraph](hdinsight-hadoop-giraph-install.md)：有關安裝 Giraph 的指令碼動作範例</span><span class="sxs-lookup"><span data-stu-id="05d35-170">[Install Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install.md): Script Action sample about installing Giraph</span></span>
* <span data-ttu-id="05d35-171">[在 HDInsight 叢集上安裝 Solr](hdinsight-hadoop-solr-install-linux.md)：有關安裝 Solr 的指令碼動作範例。</span><span class="sxs-lookup"><span data-stu-id="05d35-171">[Install Solr on HDInsight clusters](hdinsight-hadoop-solr-install-linux.md): Script Action sample about installing Solr.</span></span>

[powershell-install-configure]: /powershell/azureps-cmdlets-docs
[hdinsight-provision]: ../hdinsight-provision-clusters/
[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster-linux.md
[hdinsight-install-spark]: hdinsight-apache-spark-jupyter-spark-sql.md
