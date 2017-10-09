---
title: "HDInsight toocustomize 叢集 Azure 中的 R aaaUse |Microsoft 文件"
description: "深入了解如何使用 tooinstall R 指令碼動作，並使用 R 的 HDInsight 叢集上。"
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
ms.openlocfilehash: bf5adf2e18dc43a743b29fd1567fad731b9c3ab7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-use-r-on-hdinsight-hadoop-clusters"></a><span data-ttu-id="fd721-103">在 HDInsight Hadoop 叢集上安裝和使用 R</span><span class="sxs-lookup"><span data-stu-id="fd721-103">Install and use R on HDInsight Hadoop clusters</span></span>

<span data-ttu-id="fd721-104">了解如何 toocustomize Windows HDInsight 叢集以使用指令碼動作的 R 和 toouse R HDInsight 上的叢集。</span><span class="sxs-lookup"><span data-stu-id="fd721-104">Learn how toocustomize Windows based HDInsight cluster with R using Script Action, and how toouse R on HDInsight clusters.</span></span> <span data-ttu-id="fd721-105">hello [HDInsight 供應項目](https://azure.microsoft.com/pricing/details/hdinsight/)包含 R 伺服器做為您的 HDInsight 叢集的一部分。</span><span class="sxs-lookup"><span data-stu-id="fd721-105">hello [HDInsight offering](https://azure.microsoft.com/pricing/details/hdinsight/) includes R Server as part of your HDInsight cluster.</span></span> <span data-ttu-id="fd721-106">這可讓 R 指令碼 toouse MapReduce 和 Spark toorun 分散式計算。</span><span class="sxs-lookup"><span data-stu-id="fd721-106">This allows R scripts toouse MapReduce and Spark toorun distributed computations.</span></span> <span data-ttu-id="fd721-107">如需詳細資訊，請參閱[開始使用 HDInsight 上的 R 伺服器](hdinsight-hadoop-r-server-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="fd721-107">For more information, see [Get started using R Server on HDInsight](hdinsight-hadoop-r-server-get-started.md).</span></span> <span data-ttu-id="fd721-108">如需搭配以 Linux 為基礎的叢集使用 R 的詳細資訊，請參閱[在 HDInsight Hadoop 叢集上安裝和使用 R (Linux)](hdinsight-hadoop-r-scripts-linux.md)。</span><span class="sxs-lookup"><span data-stu-id="fd721-108">For information on using R with a Linux-based cluster, see [Install and use R on HDinsight Hadoop clusters (Linux)](hdinsight-hadoop-r-scripts-linux.md).</span></span>

<span data-ttu-id="fd721-109">您也可以使用「指令碼動作」，在 Azure HDInsight 的任一類型的叢集 (Hadoop、Storm、HBase、Spark) 上安裝 R。</span><span class="sxs-lookup"><span data-stu-id="fd721-109">You can install R on any type of cluster (Hadoop, Storm, HBase, Spark) on Azure HDInsight by using *Script Action*.</span></span> <span data-ttu-id="fd721-110">範例指令碼 tooinstall R 在 HDInsight 叢集上的都可從唯讀的 Azure 儲存體 blob [https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1](https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1)。</span><span class="sxs-lookup"><span data-stu-id="fd721-110">A sample script tooinstall R on an HDInsight cluster is available from a read-only Azure storage blob at [https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1](https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1).</span></span>

<span data-ttu-id="fd721-111">**相關文章**</span><span class="sxs-lookup"><span data-stu-id="fd721-111">**Related articles**</span></span>

* [<span data-ttu-id="fd721-112">在 HDInsight Hadoop 叢集上安裝和使用 R (Linux)</span><span class="sxs-lookup"><span data-stu-id="fd721-112">Install and use R on HDinsight Hadoop clusters (Linux)</span></span>](hdinsight-hadoop-r-scripts-linux.md)
* <span data-ttu-id="fd721-113">[在 HDInsight 中建立 Hadoop 叢集](hdinsight-hadoop-provision-linux-clusters.md)：有關建立 HDInsight 叢集的一般資訊</span><span class="sxs-lookup"><span data-stu-id="fd721-113">[Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md): general information on creating HDInsight clusters</span></span>
* <span data-ttu-id="fd721-114">[使用指令碼動作來自訂 HDInsight 叢集][hdinsight-cluster-customize]：有關使用指令碼動作來自訂 HDInsight 叢集的一般資訊。</span><span class="sxs-lookup"><span data-stu-id="fd721-114">[Customize HDInsight cluster using Script Action][hdinsight-cluster-customize]: general information on customizing HDInsight clusters using Script Action</span></span>
* [<span data-ttu-id="fd721-115">開發 HDInsight 的指令碼動作指令碼</span><span class="sxs-lookup"><span data-stu-id="fd721-115">Develop Script Action scripts for HDInsight</span></span>](hdinsight-hadoop-script-actions.md)

## <a name="what-is-r"></a><span data-ttu-id="fd721-116">什麼是 R？</span><span class="sxs-lookup"><span data-stu-id="fd721-116">What is R?</span></span>
<span data-ttu-id="fd721-117">hello <a href="http://www.r-project.org/" target="_blank">for Statistical Computing 的 R 專案</a>是開放原始碼語言和統計計算環境。</span><span class="sxs-lookup"><span data-stu-id="fd721-117">hello <a href="http://www.r-project.org/" target="_blank">R Project for Statistical Computing</a> is an open source language and environment for statistical computing.</span></span> <span data-ttu-id="fd721-118">R 提供數百個內建的統計函數及它自己的程式設計語言，此語言結合了函數型和物件導向程式設計的層面。</span><span class="sxs-lookup"><span data-stu-id="fd721-118">R provides hundreds of build-in statistical functions and its own programming language that combines aspects of functional and object-oriented programming.</span></span> <span data-ttu-id="fd721-119">它也提供廣泛的圖形功能。</span><span class="sxs-lookup"><span data-stu-id="fd721-119">It also provides extensive graphical capabilities.</span></span> <span data-ttu-id="fd721-120">R 是 hello 慣用的程式設計環境最專業統計學家也不斷和科學家在各種不同的欄位。</span><span class="sxs-lookup"><span data-stu-id="fd721-120">R is hello preferred programming environment for most professional statisticians and scientists in a wide variety of fields.</span></span>

<span data-ttu-id="fd721-121">R 與 Azure Blob 儲存體 (WASB) 相容，因此便可在 HDInsight 上使用 R 來處理儲存在該處的資料。</span><span class="sxs-lookup"><span data-stu-id="fd721-121">R is compatible with Azure Blob Storage (WASB) so that data that is stored there can be processed using R on HDInsight.</span></span>  

## <a name="install-r"></a><span data-ttu-id="fd721-122">安裝 R</span><span class="sxs-lookup"><span data-stu-id="fd721-122">Install R</span></span>
<span data-ttu-id="fd721-123">A[範例指令碼](https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1)tooinstall R 在 HDInsight 叢集上的可從 Azure 儲存體中的 blob 唯讀狀態。</span><span class="sxs-lookup"><span data-stu-id="fd721-123">A [sample script](https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1) tooinstall R on an HDInsight cluster is available from a read-only blob in Azure Storage.</span></span> <span data-ttu-id="fd721-124">本節提供有關如何 toouse hello 建立 hello 叢集使用 hello Azure 入口網站時的範例指令碼的指示。</span><span class="sxs-lookup"><span data-stu-id="fd721-124">This section provides instructions about how toouse hello sample script while creating hello cluster using hello Azure Portal.</span></span>

> [!NOTE]
> <span data-ttu-id="fd721-125">HDInsight 叢集版本 3.1 被引進 hello 範例指令碼。</span><span class="sxs-lookup"><span data-stu-id="fd721-125">hello sample script was introduced with HDInsight cluster version 3.1.</span></span> <span data-ttu-id="fd721-126">如需 HDInsight 叢集版本的詳細資訊，請參閱 [HDInsight 叢集版本](hdinsight-component-versioning.md)。</span><span class="sxs-lookup"><span data-stu-id="fd721-126">For more information about  HDInsight cluster versions, see [HDInsight cluster versions](hdinsight-component-versioning.md).</span></span>
>
>

1. <span data-ttu-id="fd721-127">當您從 hello 入口網站中建立的 HDInsight 叢集時，按一下 **選擇性組態**，然後按一下**指令碼動作**。</span><span class="sxs-lookup"><span data-stu-id="fd721-127">When you create an HDInsight cluster from hello Portal, click **Optional Configuration**, and then click **Script Actions**.</span></span>
2. <span data-ttu-id="fd721-128">在 hello**指令碼動作**頁面上，輸入下列值的 hello:</span><span class="sxs-lookup"><span data-stu-id="fd721-128">On hello **Script Actions** page, enter hello following values:</span></span>

    <span data-ttu-id="fd721-129">![使用指令碼動作 toocustomize 叢集](./media/hdinsight-hadoop-r-scripts/hdi-r-script-action.png "使用指令碼動作 toocustomize 叢集")</span><span class="sxs-lookup"><span data-stu-id="fd721-129">![Use Script Action toocustomize a cluster](./media/hdinsight-hadoop-r-scripts/hdi-r-script-action.png "Use Script Action toocustomize a cluster")</span></span>

    <table border='1'>
        <tr><th><span data-ttu-id="fd721-130">屬性</span><span class="sxs-lookup"><span data-stu-id="fd721-130">Property</span></span></th><th><span data-ttu-id="fd721-131">值</span><span class="sxs-lookup"><span data-stu-id="fd721-131">Value</span></span></th></tr>
        <tr><td><span data-ttu-id="fd721-132">名稱</span><span class="sxs-lookup"><span data-stu-id="fd721-132">Name</span></span></td>
            <td><span data-ttu-id="fd721-133">為指定名稱 hello 指令碼動作，例如<b>安裝 R</b>。</span><span class="sxs-lookup"><span data-stu-id="fd721-133">Specify a name for hello script action, for example, <b>Install R</b>.</span></span></td></tr>
        <tr><td><span data-ttu-id="fd721-134">指令碼 URI</span><span class="sxs-lookup"><span data-stu-id="fd721-134">Script URI</span></span></td>
            <td><span data-ttu-id="fd721-135">指定 hello URI toohello 指令碼，例如，會叫用的 toocustomize hello 叢集中， <i>https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1</i></span><span class="sxs-lookup"><span data-stu-id="fd721-135">Specify hello URI toohello script that is invoked toocustomize hello cluster, for example, <i>https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1</i></span></span></td></tr>
        <tr><td><span data-ttu-id="fd721-136">節點類型</span><span class="sxs-lookup"><span data-stu-id="fd721-136">Node Type</span></span></td>
            <td><span data-ttu-id="fd721-137">指定 hello hello 自訂指令碼執行所在的節點。</span><span class="sxs-lookup"><span data-stu-id="fd721-137">Specify hello nodes on which hello customization script is run.</span></span> <span data-ttu-id="fd721-138">您可以選擇 [所有節點]<b></b>、[僅限前端節點]<b></b> 或 [僅限背景工作節點]<b></b>。</span><span class="sxs-lookup"><span data-stu-id="fd721-138">You can choose <b>All Nodes</b>, <b>Head nodes only</b>, or <b>Worker nodes</b> only.</span></span>
        <tr><td><span data-ttu-id="fd721-139">參數</span><span class="sxs-lookup"><span data-stu-id="fd721-139">Parameters</span></span></td>
            <td><span data-ttu-id="fd721-140">指定 hello 參數，如果 hello 指令碼所需。</span><span class="sxs-lookup"><span data-stu-id="fd721-140">Specify hello parameters, if required by hello script.</span></span> <span data-ttu-id="fd721-141">不過，hello 指令碼 tooinstall R 不需要任何參數，因此您可以讓此處空白。</span><span class="sxs-lookup"><span data-stu-id="fd721-141">However, hello script tooinstall R does not require any parameters, so you can leave this blank.</span></span></td></tr>
    </table>

    <span data-ttu-id="fd721-142">您可以在 hello 叢集上新增多個指令碼動作 tooinstall 多個元件。</span><span class="sxs-lookup"><span data-stu-id="fd721-142">You can add more than one script action tooinstall multiple components on hello cluster.</span></span> <span data-ttu-id="fd721-143">加入 hello 指令碼之後，按一下來建立 hello 叢集 hello 核取記號 toostart。</span><span class="sxs-lookup"><span data-stu-id="fd721-143">After you have added hello scripts, click hello check mark toostart crating hello cluster.</span></span>

<span data-ttu-id="fd721-144">您也可以使用 Azure PowerShell 或 hello HDInsight.NET SDK，在 HDInsight 上使用 hello 指令碼 tooinstall R。</span><span class="sxs-lookup"><span data-stu-id="fd721-144">You can also use hello script tooinstall R on HDInsight by using Azure PowerShell or hello HDInsight .NET SDK.</span></span> <span data-ttu-id="fd721-145">此文章稍後會提供這些程序的指示。</span><span class="sxs-lookup"><span data-stu-id="fd721-145">Instructions for these procedures are provided later in this article.</span></span>

## <a name="run-r-scripts"></a><span data-ttu-id="fd721-146">執行 R 指令碼</span><span class="sxs-lookup"><span data-stu-id="fd721-146">Run R scripts</span></span>
<span data-ttu-id="fd721-147">本章節描述 toorun R 指令碼的 hello Hadoop 與 HDInsight 叢集的方式。</span><span class="sxs-lookup"><span data-stu-id="fd721-147">This section describes how toorun an R script on hello Hadoop cluster with HDInsight.</span></span>

1. <span data-ttu-id="fd721-148">**建立遠端桌面連線 toohello 叢集**: hello 入口網站，從 R 安裝，以建立 hello 叢集啟用遠端桌面，然後連接 toohello 叢集。</span><span class="sxs-lookup"><span data-stu-id="fd721-148">**Establish a Remote Desktop connection toohello cluster**: From hello Portal, enable Remote Desktop for hello cluster you created with R installed, and then connect toohello cluster.</span></span> <span data-ttu-id="fd721-149">如需指示，請參閱[連接使用 RDP tooHDInsight 叢集](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp)。</span><span class="sxs-lookup"><span data-stu-id="fd721-149">For instructions, see [Connect tooHDInsight clusters using RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span></span>
2. <span data-ttu-id="fd721-150">**開啟 hello R 主控台**: hello R 安裝會將桌面上 hello hello 前端節點的連結 toohello R 主控台。</span><span class="sxs-lookup"><span data-stu-id="fd721-150">**Open hello R console**: hello R installation puts a link toohello R console on hello desktop of hello head node.</span></span> <span data-ttu-id="fd721-151">按一下以 tooopen hello R 主控台。</span><span class="sxs-lookup"><span data-stu-id="fd721-151">Click on it tooopen hello R console.</span></span>
3. <span data-ttu-id="fd721-152">**執行 hello R 指令碼**: hello R 指令碼可以直接從 hello R 主控台執行貼上它，選取它，並按 ENTER 鍵。</span><span class="sxs-lookup"><span data-stu-id="fd721-152">**Run hello R script**: hello R script can be run directly from hello R console by pasting it, selecting it, and pressing ENTER.</span></span> <span data-ttu-id="fd721-153">以下是簡單的範例指令碼會產生 hello 數字 1 too100，然後將其乘以 2。</span><span class="sxs-lookup"><span data-stu-id="fd721-153">Here is a simple example script that generates hello numbers 1 too100 and then multiplies them by 2.</span></span>

        library(rmr2)
        library(rhdfs)
        ints = to.dfs(1:100)
        calc = mapreduce(input = ints, map = function(k, v) cbind(v, 2*v))
        from.dfs(calc)

<span data-ttu-id="fd721-154">hello 前兩行呼叫 hello RHadoop 文件庫以 r 安裝的 hello 最後一行沖印 hello 結果 toohello 主控台。</span><span class="sxs-lookup"><span data-stu-id="fd721-154">hello first two lines call hello RHadoop libraries that are installed with R. hello final line prints hello results toohello console.</span></span> <span data-ttu-id="fd721-155">hello 輸出應該看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="fd721-155">hello output should look like this:</span></span>

    [1,]  1 2
    [2,]  2 4
    .
    .
    .
    [98,]  98 196
    [99,]  99 198
    [100,] 100 200


## <a name="install-r-using-aure-powershell"></a><span data-ttu-id="fd721-156">使用 Azure PowerShell 安裝 R</span><span class="sxs-lookup"><span data-stu-id="fd721-156">Install R using Aure PowerShell</span></span>
<span data-ttu-id="fd721-157">請參閱[使用指令碼動作來自訂 HDInsight 叢集](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell)。</span><span class="sxs-lookup"><span data-stu-id="fd721-157">See [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span></span>  <span data-ttu-id="fd721-158">hello 範例會示範如何使用 Azure PowerShell 的 Spark tooinstall。</span><span class="sxs-lookup"><span data-stu-id="fd721-158">hello sample demonstrates how tooinstall Spark using Azure PowerShell.</span></span> <span data-ttu-id="fd721-159">您需要 toocustomize hello 指令碼 toouse [https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1](https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1)。</span><span class="sxs-lookup"><span data-stu-id="fd721-159">You need toocustomize hello script toouse [https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1](https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1).</span></span>

## <a name="install-r-using-net-sdk"></a><span data-ttu-id="fd721-160">使用 .NET SDK 安裝 R</span><span class="sxs-lookup"><span data-stu-id="fd721-160">Install R using .NET SDK</span></span>
<span data-ttu-id="fd721-161">請參閱[使用指令碼動作來自訂 HDInsight 叢集](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell)。</span><span class="sxs-lookup"><span data-stu-id="fd721-161">See [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span></span> <span data-ttu-id="fd721-162">hello 範例會示範如何 tooinstall Spark 使用 hello.NET SDK。</span><span class="sxs-lookup"><span data-stu-id="fd721-162">hello sample demonstrates how tooinstall Spark using hello .NET SDK.</span></span> <span data-ttu-id="fd721-163">您需要 toocustomize hello 指令碼 toouse [https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1](https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps11)。</span><span class="sxs-lookup"><span data-stu-id="fd721-163">You need toocustomize hello script toouse [https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1](https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps11).</span></span>

## <a name="see-also"></a><span data-ttu-id="fd721-164">另請參閱</span><span class="sxs-lookup"><span data-stu-id="fd721-164">See also</span></span>
* [<span data-ttu-id="fd721-165">在 HDInsight Hadoop 叢集上安裝和使用 R (Linux)</span><span class="sxs-lookup"><span data-stu-id="fd721-165">Install and use R on HDinsight Hadoop clusters (Linux)</span></span>](hdinsight-hadoop-r-scripts-linux.md)
* <span data-ttu-id="fd721-166">[在 HDInsight 中建立 Hadoop 叢集](hdinsight-hadoop-provision-linux-clusters.md)：有關建立 HDInsight 叢集的一般資訊</span><span class="sxs-lookup"><span data-stu-id="fd721-166">[Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md): general information on creating HDInsight clusters</span></span>
* <span data-ttu-id="fd721-167">[使用指令碼動作來自訂 HDInsight 叢集][hdinsight-cluster-customize]：有關使用指令碼動作來自訂 HDInsight 叢集的一般資訊。</span><span class="sxs-lookup"><span data-stu-id="fd721-167">[Customize HDInsight cluster using Script Action][hdinsight-cluster-customize]: general information on customizing HDInsight clusters using Script Action</span></span>
* [<span data-ttu-id="fd721-168">開發 HDInsight 的指令碼動作指令碼</span><span class="sxs-lookup"><span data-stu-id="fd721-168">Develop Script Action scripts for HDInsight</span></span>](hdinsight-hadoop-script-actions.md)
* <span data-ttu-id="fd721-169">[在 HDInsight 叢集上安裝和使用 Spark][hdinsight-install-spark]：有關安裝 Spark 的指令碼動作範例</span><span class="sxs-lookup"><span data-stu-id="fd721-169">[Install and use Spark on HDInsight clusters][hdinsight-install-spark]: Script Action sample about installing Spark</span></span>
* <span data-ttu-id="fd721-170">[在 HDInsight 叢集上安裝 Giraph](hdinsight-hadoop-giraph-install.md)：有關安裝 Giraph 的指令碼動作範例</span><span class="sxs-lookup"><span data-stu-id="fd721-170">[Install Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install.md): Script Action sample about installing Giraph</span></span>
* <span data-ttu-id="fd721-171">[在 HDInsight 叢集上安裝 Solr](hdinsight-hadoop-solr-install-linux.md)：有關安裝 Solr 的指令碼動作範例。</span><span class="sxs-lookup"><span data-stu-id="fd721-171">[Install Solr on HDInsight clusters](hdinsight-hadoop-solr-install-linux.md): Script Action sample about installing Solr.</span></span>

[powershell-install-configure]: /powershell/azureps-cmdlets-docs
[hdinsight-provision]: ../hdinsight-provision-clusters/
[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster-linux.md
[hdinsight-install-spark]: hdinsight-apache-spark-jupyter-spark-sql.md
