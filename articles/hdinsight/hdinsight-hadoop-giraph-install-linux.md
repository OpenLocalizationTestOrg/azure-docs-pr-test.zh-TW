---
title: "安裝並使用 HDInsight (Hadoop) 上的 Giraph | Microsoft Docs"
description: "在本主題中，您將學習如何使用指令碼動作在以 Linux 為基礎的 HDInsight 叢集上安裝 Giraph。 透過變更叢集組態或自訂安裝服務與公用程式，指令碼動作可讓您在叢集建立期間自訂叢集。"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 9fcac906-8f06-4002-9fe8-473e42f8fd0f
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: 6e2f6983e00f874420f7f0907dbc68185f0af713
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="install-giraph-on-hdinsight-hadoop-clusters-and-use-giraph-to-process-large-scale-graphs"></a><span data-ttu-id="ac944-104">在 HDInsight Hadoop 叢集上安裝 Giraph，以及使用 Giraph 來處理大規模圖形</span><span class="sxs-lookup"><span data-stu-id="ac944-104">Install Giraph on HDInsight Hadoop clusters, and use Giraph to process large-scale graphs</span></span>

<span data-ttu-id="ac944-105">了解如何在 HDInsight 叢集上安裝 Apache Giraph。</span><span class="sxs-lookup"><span data-stu-id="ac944-105">Learn how to install Apache Giraph on an HDInsight cluster.</span></span> <span data-ttu-id="ac944-106">HDInsight 的指令碼動作功能可讓您執行 bash 指令碼來自訂叢集。</span><span class="sxs-lookup"><span data-stu-id="ac944-106">The script action feature of HDInsight allows you to customize your cluster by running a bash script.</span></span> <span data-ttu-id="ac944-107">在叢集建立期間和之後，可利用指令碼來自訂叢集。</span><span class="sxs-lookup"><span data-stu-id="ac944-107">Scripts can be used to customize clusters during and after cluster creation.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ac944-108">此文件中的步驟需要使用 Linux 的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="ac944-108">The steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="ac944-109">Linux 是唯一使用於 HDInsight 3.4 版或更新版本的作業系統。</span><span class="sxs-lookup"><span data-stu-id="ac944-109">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="ac944-110">如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。</span><span class="sxs-lookup"><span data-stu-id="ac944-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <span data-ttu-id="ac944-111"><a name="whatis"></a>什麼是 Giraph</span><span class="sxs-lookup"><span data-stu-id="ac944-111"><a name="whatis"></a>What is Giraph</span></span>

<span data-ttu-id="ac944-112">[Apache Giraph](http://giraph.apache.org/) 可讓您利用 Hadoop 執行圖形處理，且可以搭配 Azure HDInsight 一起使用。</span><span class="sxs-lookup"><span data-stu-id="ac944-112">[Apache Giraph](http://giraph.apache.org/) allows you to perform graph processing by using Hadoop, and can be used with Azure HDInsight.</span></span> <span data-ttu-id="ac944-113">圖形可以為物件之間的關聯性建立模型。</span><span class="sxs-lookup"><span data-stu-id="ac944-113">Graphs model relationships between objects.</span></span> <span data-ttu-id="ac944-114">例如，大型網路 (例如網際網路) 上各路由器之間的連線，或社交網路上的人際關係。</span><span class="sxs-lookup"><span data-stu-id="ac944-114">For example, the connections between routers on a large network like the Internet, or relationships between people on social networks.</span></span> <span data-ttu-id="ac944-115">圖形處理可讓您分析圖形中物件之間的關聯，例如：</span><span class="sxs-lookup"><span data-stu-id="ac944-115">Graph processing allows you to reason about the relationships between objects in a graph, such as:</span></span>

* <span data-ttu-id="ac944-116">根據目前的人際關係找出可能的朋友。</span><span class="sxs-lookup"><span data-stu-id="ac944-116">Identifying potential friends based on your current relationships.</span></span>

* <span data-ttu-id="ac944-117">識別網路中兩台電腦之間的最短路線。</span><span class="sxs-lookup"><span data-stu-id="ac944-117">Identifying the shortest route between two computers in a network.</span></span>

* <span data-ttu-id="ac944-118">計算網頁的頁面排名。</span><span class="sxs-lookup"><span data-stu-id="ac944-118">Calculating the page rank of webpages.</span></span>

> [!WARNING]
> <span data-ttu-id="ac944-119">完全支援 HDInsight 叢集隨附的元件 - Microsoft 支援服務會協助釐清與解決這些元件的相關問題。</span><span class="sxs-lookup"><span data-stu-id="ac944-119">Components provided with the HDInsight cluster are fully supported - Microsoft Support helps to isolate and resolve issues related to these components.</span></span>
>
> <span data-ttu-id="ac944-120">自訂元件 (例如 Giraph) 則獲得商務上合理的支援，協助您進一步對問題進行疑難排解。</span><span class="sxs-lookup"><span data-stu-id="ac944-120">Custom components, such as Giraph, receive commercially reasonable support to help you to further troubleshoot the issue.</span></span> <span data-ttu-id="ac944-121">Microsoft 支援服務可能有能力解決問題。</span><span class="sxs-lookup"><span data-stu-id="ac944-121">Microsoft Support may be able to resolving the issue.</span></span> <span data-ttu-id="ac944-122">如果無法解決，則您必須諮詢開放原始碼社群，以尋求該項技術的深厚專業知識。</span><span class="sxs-lookup"><span data-stu-id="ac944-122">If not, you must consult open source communities where deep expertise for that technology is found.</span></span> <span data-ttu-id="ac944-123">例如，有許多社群網站可以使用，像是：[HDInsight 的 MSDN 論壇](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight)、[http://stackoverflow.com](http://stackoverflow.com)。</span><span class="sxs-lookup"><span data-stu-id="ac944-123">For example, there are many community sites that can be used, like: [MSDN forum for HDInsight](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com).</span></span> <span data-ttu-id="ac944-124">另外，Apache 專案在 [http://apache.org](http://apache.org) 上有專案網站，例如 [Hadoop](http://hadoop.apache.org/)。</span><span class="sxs-lookup"><span data-stu-id="ac944-124">Also Apache projects have project sites on [http://apache.org](http://apache.org), for example: [Hadoop](http://hadoop.apache.org/).</span></span>


## <a name="what-the-script-does"></a><span data-ttu-id="ac944-125">指令碼會執行哪些作業</span><span class="sxs-lookup"><span data-stu-id="ac944-125">What the script does</span></span>

<span data-ttu-id="ac944-126">此指令碼會執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="ac944-126">This script performs the following actions:</span></span>

* <span data-ttu-id="ac944-127">將 Giraph 安裝至 `/usr/hdp/current/giraph`</span><span class="sxs-lookup"><span data-stu-id="ac944-127">Installs Giraph to `/usr/hdp/current/giraph`</span></span>

* <span data-ttu-id="ac944-128">將 `giraph-examples.jar` 檔案複製到您的叢集的預設儲存體 (WASB)：`/example/jars/giraph-examples.jar`</span><span class="sxs-lookup"><span data-stu-id="ac944-128">Copies the `giraph-examples.jar` file to default storage (WASB) for your cluster: `/example/jars/giraph-examples.jar`</span></span>

## <span data-ttu-id="ac944-129"><a name="install"></a>使用指令碼動作安裝 Giraph</span><span class="sxs-lookup"><span data-stu-id="ac944-129"><a name="install"></a>Install Giraph using Script Actions</span></span>

<span data-ttu-id="ac944-130">在 HDInsight 叢集上安裝 Giraph 的範例指令碼位於下列位置：</span><span class="sxs-lookup"><span data-stu-id="ac944-130">A sample script to install Giraph on an HDInsight cluster is available at the following location:</span></span>

    https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh

<span data-ttu-id="ac944-131">本節提供有關如何在使用 Azure 入口網站建立叢集時使用範例指令碼的指示。</span><span class="sxs-lookup"><span data-stu-id="ac944-131">This section provides instructions on how to use the sample script while creating the cluster by using the Azure portal.</span></span>

> [!NOTE]
> <span data-ttu-id="ac944-132">您可以使用下列任何方法套用指令碼動作︰</span><span class="sxs-lookup"><span data-stu-id="ac944-132">A script action can be applied using any of the following methods:</span></span>
> * <span data-ttu-id="ac944-133">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="ac944-133">Azure PowerShell</span></span>
> * <span data-ttu-id="ac944-134">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="ac944-134">The Azure CLI</span></span>
> * <span data-ttu-id="ac944-135">HDInsight .NET SDK</span><span class="sxs-lookup"><span data-stu-id="ac944-135">The HDInsight .NET SDK</span></span>
> * <span data-ttu-id="ac944-136">Azure 資源管理員範本</span><span class="sxs-lookup"><span data-stu-id="ac944-136">Azure Resource Manager templates</span></span>
> 
> <span data-ttu-id="ac944-137">您也可以將指令碼動作套用到執行中的叢集上。</span><span class="sxs-lookup"><span data-stu-id="ac944-137">You can also apply script actions to already running clusters.</span></span> <span data-ttu-id="ac944-138">如需詳細資訊，請參閱 [使用指令碼動作自訂 HDInsight 叢集](hdinsight-hadoop-customize-cluster-linux.md)。</span><span class="sxs-lookup"><span data-stu-id="ac944-138">For more information, see [Customize HDInsight clusters with Script Actions](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

1. <span data-ttu-id="ac944-139">使用 [建立以 Linux 為基礎的 HDInsight 叢集](hdinsight-hadoop-create-linux-clusters-portal.md)中的步驟開始建立叢集，但是不完成建立。</span><span class="sxs-lookup"><span data-stu-id="ac944-139">Start creating a cluster by using the steps in [Create Linux-based HDInsight clusters](hdinsight-hadoop-create-linux-clusters-portal.md), but do not complete creation.</span></span>

2. <span data-ttu-id="ac944-140">在 [選用組態] 刀鋒視窗中，選取 [指令碼動作]，並提供下列資訊：</span><span class="sxs-lookup"><span data-stu-id="ac944-140">On the **Optional Configuration** blade, select **Script Actions**, and provide the following information:</span></span>

   * <span data-ttu-id="ac944-141">**名稱**：輸入指令碼動作的易記名稱。</span><span class="sxs-lookup"><span data-stu-id="ac944-141">**NAME**: Enter a friendly name for the script action.</span></span>

   * <span data-ttu-id="ac944-142">**指令碼 URI**：https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh</span><span class="sxs-lookup"><span data-stu-id="ac944-142">**SCRIPT URI**: https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh</span></span>

   * <span data-ttu-id="ac944-143">**HEAD**：勾選此項目</span><span class="sxs-lookup"><span data-stu-id="ac944-143">**HEAD**: Check this entry</span></span>

   * <span data-ttu-id="ac944-144">**WORKER**：保持不勾選此項目</span><span class="sxs-lookup"><span data-stu-id="ac944-144">**WORKER**: Leave this entry unchecked</span></span>

   * <span data-ttu-id="ac944-145">**ZOOKEEPER**：保持不勾選此項目</span><span class="sxs-lookup"><span data-stu-id="ac944-145">**ZOOKEEPER**: Leave this entry unchecked</span></span>

   * <span data-ttu-id="ac944-146">**參數**：將此欄位保留空白</span><span class="sxs-lookup"><span data-stu-id="ac944-146">**PARAMETERS**: Leave this field blank</span></span>

3. <span data-ttu-id="ac944-147">在 [指令碼動作] 底部，使用 [選取] 按鈕以儲存組態。</span><span class="sxs-lookup"><span data-stu-id="ac944-147">At the bottom of the **Script Actions**, use the **Select** button to save the configuration.</span></span> <span data-ttu-id="ac944-148">最後，使用 [選用組態] 刀鋒視窗底部的 [選取] 按鈕，儲存選用組態資訊。</span><span class="sxs-lookup"><span data-stu-id="ac944-148">Finally, use the **Select** button at the bottom of the **Optional Configuration** blade to save the optional configuration information.</span></span>

4. <span data-ttu-id="ac944-149">繼續如 [建立以 Linux 為基礎的 HDInsight 叢集](hdinsight-hadoop-create-linux-clusters-portal.md)中所述建立叢集。</span><span class="sxs-lookup"><span data-stu-id="ac944-149">Continue creating the cluster as described in [Create Linux-based HDInsight clusters](hdinsight-hadoop-create-linux-clusters-portal.md).</span></span>

## <span data-ttu-id="ac944-150"><a name="usegiraph"></a>如何在 HDInsight 中使用 Giraph？</span><span class="sxs-lookup"><span data-stu-id="ac944-150"><a name="usegiraph"></a>How do I use Giraph in HDInsight?</span></span>

<span data-ttu-id="ac944-151">建立叢集之後，請使用下列步驟執行 Giraph 隨附的 SimpleShortestPathsComputation 範例。</span><span class="sxs-lookup"><span data-stu-id="ac944-151">Once the cluster has been created, use the following steps to run the SimpleShortestPathsComputation example included with Giraph.</span></span> <span data-ttu-id="ac944-152">此範例會使用基本 [Pregel](http://people.apache.org/~edwardyoon/documents/pregel.pdf) 實作，在圖表中找出物件之間的最短路徑。</span><span class="sxs-lookup"><span data-stu-id="ac944-152">This example uses the basic [Pregel](http://people.apache.org/~edwardyoon/documents/pregel.pdf) implementation for finding the shortest path between objects in a graph.</span></span>

1. <span data-ttu-id="ac944-153">使用 SSH 連線到 HDInsight 叢集</span><span class="sxs-lookup"><span data-stu-id="ac944-153">Connect to the HDInsight cluster using SSH:</span></span>

    ```bash
    ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="ac944-154">如需相關資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。</span><span class="sxs-lookup"><span data-stu-id="ac944-154">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="ac944-155">使用以下命令建立名為 **tiny_graph.txt** 的檔案：</span><span class="sxs-lookup"><span data-stu-id="ac944-155">Use the following command to create a file named **tiny_graph.txt**:</span></span>

    ```bash
    nano tiny_graph.txt
    ```

    <span data-ttu-id="ac944-156">使用下列文字做為此檔案的內容：</span><span class="sxs-lookup"><span data-stu-id="ac944-156">Use the following text as the contents of this file:</span></span>

    ```text
    [0,0,[[1,1],[3,3]]]
    [1,0,[[0,1],[2,2],[3,1]]]
    [2,0,[[1,2],[4,4]]]
    [3,0,[[0,3],[1,1],[4,4]]]
    [4,0,[[3,4],[2,4]]]
    ```

    <span data-ttu-id="ac944-157">此資料使用 `[source_id, source_value,[[dest_id], [edge_value],...]]` 格式，描述有向圖形中物件之間的關聯。</span><span class="sxs-lookup"><span data-stu-id="ac944-157">This data describes a relationship between objects in a directed graph, by using the format `[source_id, source_value,[[dest_id], [edge_value],...]]`.</span></span> <span data-ttu-id="ac944-158">每一行代表 `source_id` 物件和一或多個 `dest_id` 物件之間的關聯性。</span><span class="sxs-lookup"><span data-stu-id="ac944-158">Each line represents a relationship between a `source_id` object and one or more `dest_id` objects.</span></span> <span data-ttu-id="ac944-159">`edge_value` 可以視為 `source_id` 和 `dest\_id` 之間的連線強度或距離。</span><span class="sxs-lookup"><span data-stu-id="ac944-159">The `edge_value` can be thought of as the strength or distance of the connection between `source_id` and `dest\_id`.</span></span>

    <span data-ttu-id="ac944-160">使用值 (或權數) 當作物件之間的距離繪製出來後，資料可能如下圖所示：</span><span class="sxs-lookup"><span data-stu-id="ac944-160">Drawn out, and using the value (or weight) as the distance between objects, the data might look like the following diagram:</span></span>

    ![tiny_graph.txt drawn as circles with lines of varying distance between](./media/hdinsight-hadoop-giraph-install-linux/giraph-graph.png)

3. <span data-ttu-id="ac944-162">若要儲存檔案，依序使用 **Ctrl+X**、**Y**，最後按 **Enter** 以接受檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="ac944-162">To save the file, use **Ctrl+X**, then **Y**, and finally **Enter** to accept the file name.</span></span>

4. <span data-ttu-id="ac944-163">使用下列項目以將資料儲存至您的 HDInsight 叢集的主要儲存體：</span><span class="sxs-lookup"><span data-stu-id="ac944-163">Use the following to store the data into primary storage for your HDInsight cluster:</span></span>

    ```bash
    hdfs dfs -put tiny_graph.txt /example/data/tiny_graph.txt
    ```

5. <span data-ttu-id="ac944-164">使用下列命令執行 SimpleShortestPathsComputation 範例：</span><span class="sxs-lookup"><span data-stu-id="ac944-164">Run the SimpleShortestPathsComputation example using the following command:</span></span>

    ```bash
    yarn jar /usr/hdp/current/giraph/giraph-examples.jar org.apache.giraph.GiraphRunner org.apache.giraph.examples.SimpleShortestPathsComputation -ca mapred.job.tracker=headnodehost:9010 -vif org.apache.giraph.io.formats.JsonLongDoubleFloatDoubleVertexInputFormat -vip /example/data/tiny_graph.txt -vof org.apache.giraph.io.formats.IdWithValueTextOutputFormat -op /example/output/shortestpaths -w 2
    ```

    <span data-ttu-id="ac944-165">下表說明與此命令搭配使用的參數：</span><span class="sxs-lookup"><span data-stu-id="ac944-165">The parameters used with this command are described in the following table:</span></span>

   | <span data-ttu-id="ac944-166">參數</span><span class="sxs-lookup"><span data-stu-id="ac944-166">Parameter</span></span> | <span data-ttu-id="ac944-167">作用</span><span class="sxs-lookup"><span data-stu-id="ac944-167">What it does</span></span> |
   | --- | --- |
   | `jar` |<span data-ttu-id="ac944-168">包含範例的 jar 檔案。</span><span class="sxs-lookup"><span data-stu-id="ac944-168">The jar file containing the examples.</span></span> |
   | `org.apache.giraph.GiraphRunner` |<span data-ttu-id="ac944-169">用於啟動範例的類別。</span><span class="sxs-lookup"><span data-stu-id="ac944-169">The class used to start the examples.</span></span> |
   | `org.apache.giraph.examples.SimpleShortestPathsCoputation` |<span data-ttu-id="ac944-170">所使用的範例。</span><span class="sxs-lookup"><span data-stu-id="ac944-170">The example that is used.</span></span> <span data-ttu-id="ac944-171">在此範例中，它會計算圖表中識別碼 1 和所有其他識別碼之間的最短路徑。</span><span class="sxs-lookup"><span data-stu-id="ac944-171">In this example, it computes the shortest path between ID 1 and all other IDs in the graph.</span></span> |
   | `-ca mapred.job.tracker` |<span data-ttu-id="ac944-172">叢集的前端節點。</span><span class="sxs-lookup"><span data-stu-id="ac944-172">The headnode for the cluster.</span></span> |
   | `-vif` |<span data-ttu-id="ac944-173">用於輸入資料的輸入格式。</span><span class="sxs-lookup"><span data-stu-id="ac944-173">The input format to use for the input data.</span></span> |
   | `-vip` |<span data-ttu-id="ac944-174">輸入資料檔案。</span><span class="sxs-lookup"><span data-stu-id="ac944-174">The input data file.</span></span> |
   | `-vof` |<span data-ttu-id="ac944-175">輸出格式。</span><span class="sxs-lookup"><span data-stu-id="ac944-175">The output format.</span></span> <span data-ttu-id="ac944-176">在此範例中，識別碼和值是純文字。</span><span class="sxs-lookup"><span data-stu-id="ac944-176">In this example, ID and value as plain text.</span></span> |
   | `-op` |<span data-ttu-id="ac944-177">輸出位置。</span><span class="sxs-lookup"><span data-stu-id="ac944-177">The output location.</span></span> |
   | `-w 2` |<span data-ttu-id="ac944-178">要使用的背景工作角色數目。</span><span class="sxs-lookup"><span data-stu-id="ac944-178">The number of workers to use.</span></span> <span data-ttu-id="ac944-179">在此範例中是 2。</span><span class="sxs-lookup"><span data-stu-id="ac944-179">In this example, 2.</span></span> |

    <span data-ttu-id="ac944-180">如需這些項目以及與 Giraph 範例搭配使用之其他參數的詳細資訊，請參閱 [Giraph 快速入門](http://giraph.apache.org/quick_start.html)。</span><span class="sxs-lookup"><span data-stu-id="ac944-180">For more information on these, and other parameters used with Giraph samples, see the [Giraph quickstart](http://giraph.apache.org/quick_start.html).</span></span>

6. <span data-ttu-id="ac944-181">一旦作業完成，結果會儲存在 **/example/out/shotestpaths** 目錄中。</span><span class="sxs-lookup"><span data-stu-id="ac944-181">Once the job has finished, the results are stored in the **/example/out/shotestpaths** directory.</span></span> <span data-ttu-id="ac944-182">輸出檔的名稱會以 **part-m-** 開頭，結束的數字表示是第一個、第二個檔案，依此類推。</span><span class="sxs-lookup"><span data-stu-id="ac944-182">The output file names begin with **part-m-** and end with a number indicating the first, second, etc. file.</span></span> <span data-ttu-id="ac944-183">使用下列命令來檢視輸出：</span><span class="sxs-lookup"><span data-stu-id="ac944-183">Use the following command to view the output:</span></span>

    ```bash
    hdfs dfs -text /example/output/shortestpaths/*
    ```

    <span data-ttu-id="ac944-184">輸出應該如下列文字所示：</span><span class="sxs-lookup"><span data-stu-id="ac944-184">The output should appear similar to the following text:</span></span>

        0    1.0
        4    5.0
        2    2.0
        1    0.0
        3    1.0

    <span data-ttu-id="ac944-185">SimpleShortestPathComputation 範例已刻意設計成從物件識別碼 1 開始，尋找前往其他物件的最短路徑。</span><span class="sxs-lookup"><span data-stu-id="ac944-185">The SimpleShortestPathComputation example is hard coded to start with object ID 1 and find the shortest path to other objects.</span></span> <span data-ttu-id="ac944-186">輸出的格式為 `destination_id` 和 `distance`。</span><span class="sxs-lookup"><span data-stu-id="ac944-186">The output is in the format of `destination_id` and `distance`.</span></span> <span data-ttu-id="ac944-187">`distance` 是物件識別碼 1 與目標識別碼之間經過之邊緣的值 (或權數)。</span><span class="sxs-lookup"><span data-stu-id="ac944-187">The `distance` is the value (or weight) of the edges traveled between object ID 1 and the target ID.</span></span>

    <span data-ttu-id="ac944-188">將此資料視覺化之後，您可以走過識別碼 1 和其他所有物件之間的最短路徑來驗證結果。</span><span class="sxs-lookup"><span data-stu-id="ac944-188">Visualizing this data, you can verify the results by traveling the shortest paths between ID 1 and all other objects.</span></span> <span data-ttu-id="ac944-189">識別碼 1 和識別碼 4 之間的最短路徑為 5。</span><span class="sxs-lookup"><span data-stu-id="ac944-189">The shortest path between ID 1 and ID 4 is 5.</span></span> <span data-ttu-id="ac944-190">此值為<span style="color:orange">識別碼 1 和 3</span> 之間加上<span style="color:red">識別碼 3 和 4</span> 之間的總距離。</span><span class="sxs-lookup"><span data-stu-id="ac944-190">This value is the total distance between <span style="color:orange">ID 1 and 3</span>, and then <span style="color:red">ID 3 and 4</span>.</span></span>

    ![Drawing of objects as circles with shortest paths drawn between](./media/hdinsight-hadoop-giraph-install-linux/giraph-graph-out.png)

## <a name="next-steps"></a><span data-ttu-id="ac944-192">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ac944-192">Next steps</span></span>

* <span data-ttu-id="ac944-193">[在 HDInsight 叢集上安裝及使用 Hue](hdinsight-hadoop-hue-linux.md)。</span><span class="sxs-lookup"><span data-stu-id="ac944-193">[Install and use Hue on HDInsight clusters](hdinsight-hadoop-hue-linux.md).</span></span>

* <span data-ttu-id="ac944-194">[在 HDInsight 叢集上安裝 Solr](hdinsight-hadoop-solr-install-linux.md)。</span><span class="sxs-lookup"><span data-stu-id="ac944-194">[Install Solr on HDInsight clusters](hdinsight-hadoop-solr-install-linux.md).</span></span>
