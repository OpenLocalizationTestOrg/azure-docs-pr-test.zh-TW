---
title: "aaaInstall HDInsight (Hadoop)-Azure 上使用 Giraph |Microsoft 文件"
description: "了解如何 tooinstall Giraph 上以 Linux 為基礎的 HDInsight 叢集使用指令碼動作。 指令碼動作可讓您 toocustomize hello 叢集建立期間，可以變更叢集設定或安裝服務和公用程式。"
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
ms.openlocfilehash: 0f195b65cebf5e24d1808ef33b95b4d362555521
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="install-giraph-on-hdinsight-hadoop-clusters-and-use-giraph-tooprocess-large-scale-graphs"></a><span data-ttu-id="3876b-104">在 HDInsight Hadoop 叢集上安裝 Giraph 和使用 Giraph tooprocess 大規模圖形</span><span class="sxs-lookup"><span data-stu-id="3876b-104">Install Giraph on HDInsight Hadoop clusters, and use Giraph tooprocess large-scale graphs</span></span>

<span data-ttu-id="3876b-105">深入了解如何 tooinstall Apache Giraph 在 HDInsight 叢集上的。</span><span class="sxs-lookup"><span data-stu-id="3876b-105">Learn how tooinstall Apache Giraph on an HDInsight cluster.</span></span> <span data-ttu-id="3876b-106">HDInsight hello 指令碼動作功能可讓您 toocustomize 您的叢集執行 bash 指令碼。</span><span class="sxs-lookup"><span data-stu-id="3876b-106">hello script action feature of HDInsight allows you toocustomize your cluster by running a bash script.</span></span> <span data-ttu-id="3876b-107">指令碼和建立叢集之後，可以是使用的 toocustomize 叢集。</span><span class="sxs-lookup"><span data-stu-id="3876b-107">Scripts can be used toocustomize clusters during and after cluster creation.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3876b-108">本文件中的 hello 步驟需要使用 Linux 的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="3876b-108">hello steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="3876b-109">Linux 為 hello 僅作業系統 HDInsight 3.4 或更新版本上使用。</span><span class="sxs-lookup"><span data-stu-id="3876b-109">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="3876b-110">如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。</span><span class="sxs-lookup"><span data-stu-id="3876b-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <span data-ttu-id="3876b-111"><a name="whatis"></a>什麼是 Giraph</span><span class="sxs-lookup"><span data-stu-id="3876b-111"><a name="whatis"></a>What is Giraph</span></span>

<span data-ttu-id="3876b-112">[Apache Giraph](http://giraph.apache.org/)可讓您使用 Hadoop，處理 tooperform 圖形，並可以搭配 Azure HDInsight。</span><span class="sxs-lookup"><span data-stu-id="3876b-112">[Apache Giraph](http://giraph.apache.org/) allows you tooperform graph processing by using Hadoop, and can be used with Azure HDInsight.</span></span> <span data-ttu-id="3876b-113">圖形可以為物件之間的關聯性建立模型。</span><span class="sxs-lookup"><span data-stu-id="3876b-113">Graphs model relationships between objects.</span></span> <span data-ttu-id="3876b-114">例如，大型的網路上的路由器之間的 hello 連線，例如 hello 網際網路或社交網路上的使用者之間的關聯性。</span><span class="sxs-lookup"><span data-stu-id="3876b-114">For example, hello connections between routers on a large network like hello Internet, or relationships between people on social networks.</span></span> <span data-ttu-id="3876b-115">圖表處理可讓您 hello 在圖形中，物件之間的關聯性的相關 tooreason 例如：</span><span class="sxs-lookup"><span data-stu-id="3876b-115">Graph processing allows you tooreason about hello relationships between objects in a graph, such as:</span></span>

* <span data-ttu-id="3876b-116">根據目前的人際關係找出可能的朋友。</span><span class="sxs-lookup"><span data-stu-id="3876b-116">Identifying potential friends based on your current relationships.</span></span>

* <span data-ttu-id="3876b-117">用來識別網路中的兩部電腦之間的 hello 最短路由。</span><span class="sxs-lookup"><span data-stu-id="3876b-117">Identifying hello shortest route between two computers in a network.</span></span>

* <span data-ttu-id="3876b-118">計算 hello 頁面順位的網頁。</span><span class="sxs-lookup"><span data-stu-id="3876b-118">Calculating hello page rank of webpages.</span></span>

> [!WARNING]
> <span data-ttu-id="3876b-119">提供與 hello HDInsight 叢集的元件可以完全支援-tooisolate 可協助 Microsoft 支援服務，並解決問題相關的 toothese 元件。</span><span class="sxs-lookup"><span data-stu-id="3876b-119">Components provided with hello HDInsight cluster are fully supported - Microsoft Support helps tooisolate and resolve issues related toothese components.</span></span>
>
> <span data-ttu-id="3876b-120">自訂元件，例如 Giraph，會收到盡商業上合理支援 toohelp 您 toofurther hello 問題進行疑難排解。</span><span class="sxs-lookup"><span data-stu-id="3876b-120">Custom components, such as Giraph, receive commercially reasonable support toohelp you toofurther troubleshoot hello issue.</span></span> <span data-ttu-id="3876b-121">Microsoft 支援服務可能無法 tooresolving hello 問題。</span><span class="sxs-lookup"><span data-stu-id="3876b-121">Microsoft Support may be able tooresolving hello issue.</span></span> <span data-ttu-id="3876b-122">如果無法解決，則您必須諮詢開放原始碼社群，以尋求該項技術的深厚專業知識。</span><span class="sxs-lookup"><span data-stu-id="3876b-122">If not, you must consult open source communities where deep expertise for that technology is found.</span></span> <span data-ttu-id="3876b-123">例如，有許多社群網站可以使用，像是：[HDInsight 的 MSDN 論壇](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight)、[http://stackoverflow.com](http://stackoverflow.com)。另外，Apache 專案在 [http://apache.org](http://apache.org) 上有專案網站，例如 [Hadoop](http://hadoop.apache.org/)。</span><span class="sxs-lookup"><span data-stu-id="3876b-123">For example, there are many community sites that can be used, like: [MSDN forum for HDInsight](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com). Also Apache projects have project sites on [http://apache.org](http://apache.org), for example: [Hadoop](http://hadoop.apache.org/).</span></span>


## <a name="what-hello-script-does"></a><span data-ttu-id="3876b-124">哪些 hello 指令碼會執行</span><span class="sxs-lookup"><span data-stu-id="3876b-124">What hello script does</span></span>

<span data-ttu-id="3876b-125">此指令碼會執行下列動作的 hello:</span><span class="sxs-lookup"><span data-stu-id="3876b-125">This script performs hello following actions:</span></span>

* <span data-ttu-id="3876b-126">安裝 Giraph 太`/usr/hdp/current/giraph`</span><span class="sxs-lookup"><span data-stu-id="3876b-126">Installs Giraph too`/usr/hdp/current/giraph`</span></span>

* <span data-ttu-id="3876b-127">複製 hello`giraph-examples.jar`檔案 toodefault 儲存體 (WASB) 為您的叢集：`/example/jars/giraph-examples.jar`</span><span class="sxs-lookup"><span data-stu-id="3876b-127">Copies hello `giraph-examples.jar` file toodefault storage (WASB) for your cluster: `/example/jars/giraph-examples.jar`</span></span>

## <span data-ttu-id="3876b-128"><a name="install"></a>使用指令碼動作安裝 Giraph</span><span class="sxs-lookup"><span data-stu-id="3876b-128"><a name="install"></a>Install Giraph using Script Actions</span></span>

<span data-ttu-id="3876b-129">範例指令碼 tooinstall Giraph 在 HDInsight 叢集上的將會位於下列位置的 hello:</span><span class="sxs-lookup"><span data-stu-id="3876b-129">A sample script tooinstall Giraph on an HDInsight cluster is available at hello following location:</span></span>

    https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh

<span data-ttu-id="3876b-130">本節提供指示 toouse hello 範例指令碼時使用 hello Azure 入口網站建立 hello 叢集的方式。</span><span class="sxs-lookup"><span data-stu-id="3876b-130">This section provides instructions on how toouse hello sample script while creating hello cluster by using hello Azure portal.</span></span>

> [!NOTE]
> <span data-ttu-id="3876b-131">您可以使用任何下列方法的 hello 套用指令碼動作：</span><span class="sxs-lookup"><span data-stu-id="3876b-131">A script action can be applied using any of hello following methods:</span></span>
> * <span data-ttu-id="3876b-132">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="3876b-132">Azure PowerShell</span></span>
> * <span data-ttu-id="3876b-133">hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="3876b-133">hello Azure CLI</span></span>
> * <span data-ttu-id="3876b-134">hello HDInsight.NET SDK</span><span class="sxs-lookup"><span data-stu-id="3876b-134">hello HDInsight .NET SDK</span></span>
> * <span data-ttu-id="3876b-135">Azure 資源管理員範本</span><span class="sxs-lookup"><span data-stu-id="3876b-135">Azure Resource Manager templates</span></span>
> 
> <span data-ttu-id="3876b-136">您也可以套用指令碼動作 tooalready 執行中的叢集。</span><span class="sxs-lookup"><span data-stu-id="3876b-136">You can also apply script actions tooalready running clusters.</span></span> <span data-ttu-id="3876b-137">如需詳細資訊，請參閱 [使用指令碼動作自訂 HDInsight 叢集](hdinsight-hadoop-customize-cluster-linux.md)。</span><span class="sxs-lookup"><span data-stu-id="3876b-137">For more information, see [Customize HDInsight clusters with Script Actions](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

1. <span data-ttu-id="3876b-138">開始使用中的 hello 步驟建立叢集[建立 Linux 為基礎的 HDInsight 叢集](hdinsight-hadoop-create-linux-clusters-portal.md)，但無法完成建立。</span><span class="sxs-lookup"><span data-stu-id="3876b-138">Start creating a cluster by using hello steps in [Create Linux-based HDInsight clusters](hdinsight-hadoop-create-linux-clusters-portal.md), but do not complete creation.</span></span>

2. <span data-ttu-id="3876b-139">在 hello**選擇性組態**刀鋒視窗中，選取**指令碼動作**，並提供下列資訊的 hello:</span><span class="sxs-lookup"><span data-stu-id="3876b-139">On hello **Optional Configuration** blade, select **Script Actions**, and provide hello following information:</span></span>

   * <span data-ttu-id="3876b-140">**名稱**： 輸入 hello 指令碼動作的易記名稱。</span><span class="sxs-lookup"><span data-stu-id="3876b-140">**NAME**: Enter a friendly name for hello script action.</span></span>

   * <span data-ttu-id="3876b-141">**指令碼 URI**：https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh</span><span class="sxs-lookup"><span data-stu-id="3876b-141">**SCRIPT URI**: https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh</span></span>

   * <span data-ttu-id="3876b-142">**HEAD**：勾選此項目</span><span class="sxs-lookup"><span data-stu-id="3876b-142">**HEAD**: Check this entry</span></span>

   * <span data-ttu-id="3876b-143">**WORKER**：保持不勾選此項目</span><span class="sxs-lookup"><span data-stu-id="3876b-143">**WORKER**: Leave this entry unchecked</span></span>

   * <span data-ttu-id="3876b-144">**ZOOKEEPER**：保持不勾選此項目</span><span class="sxs-lookup"><span data-stu-id="3876b-144">**ZOOKEEPER**: Leave this entry unchecked</span></span>

   * <span data-ttu-id="3876b-145">**參數**：將此欄位保留空白</span><span class="sxs-lookup"><span data-stu-id="3876b-145">**PARAMETERS**: Leave this field blank</span></span>

3. <span data-ttu-id="3876b-146">在 hello 底部 hello**指令碼動作**，使用 hello**選取**按鈕 toosave hello 組態。</span><span class="sxs-lookup"><span data-stu-id="3876b-146">At hello bottom of hello **Script Actions**, use hello **Select** button toosave hello configuration.</span></span> <span data-ttu-id="3876b-147">最後，使用 hello**選取**在 hello hello 底部的按鈕**選擇性組態**刀鋒視窗 toosave hello 選擇性的組態資訊。</span><span class="sxs-lookup"><span data-stu-id="3876b-147">Finally, use hello **Select** button at hello bottom of hello **Optional Configuration** blade toosave hello optional configuration information.</span></span>

4. <span data-ttu-id="3876b-148">繼續中所述建立 hello 叢集[建立 Linux 為基礎的 HDInsight 叢集](hdinsight-hadoop-create-linux-clusters-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="3876b-148">Continue creating hello cluster as described in [Create Linux-based HDInsight clusters](hdinsight-hadoop-create-linux-clusters-portal.md).</span></span>

## <span data-ttu-id="3876b-149"><a name="usegiraph"></a>如何在 HDInsight 中使用 Giraph？</span><span class="sxs-lookup"><span data-stu-id="3876b-149"><a name="usegiraph"></a>How do I use Giraph in HDInsight?</span></span>

<span data-ttu-id="3876b-150">一旦建立 hello 叢集之後，請使用下列步驟 toorun hello SimpleShortestPathsComputation 範例隨附 Giraph hello。</span><span class="sxs-lookup"><span data-stu-id="3876b-150">Once hello cluster has been created, use hello following steps toorun hello SimpleShortestPathsComputation example included with Giraph.</span></span> <span data-ttu-id="3876b-151">這個範例會使用 hello basic [Pregel](http://people.apache.org/~edwardyoon/documents/pregel.pdf)尋找 hello 圖形中的物件之間最短的路徑實作。</span><span class="sxs-lookup"><span data-stu-id="3876b-151">This example uses hello basic [Pregel](http://people.apache.org/~edwardyoon/documents/pregel.pdf) implementation for finding hello shortest path between objects in a graph.</span></span>

1. <span data-ttu-id="3876b-152">連線使用 SSH toohello HDInsight 叢集：</span><span class="sxs-lookup"><span data-stu-id="3876b-152">Connect toohello HDInsight cluster using SSH:</span></span>

    ```bash
    ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="3876b-153">如需相關資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。</span><span class="sxs-lookup"><span data-stu-id="3876b-153">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="3876b-154">使用 hello 下列命令 toocreate 名為**tiny_graph.txt**:</span><span class="sxs-lookup"><span data-stu-id="3876b-154">Use hello following command toocreate a file named **tiny_graph.txt**:</span></span>

    ```bash
    nano tiny_graph.txt
    ```

    <span data-ttu-id="3876b-155">使用 hello hello 這個檔案的內容為下列文字：</span><span class="sxs-lookup"><span data-stu-id="3876b-155">Use hello following text as hello contents of this file:</span></span>

    ```text
    [0,0,[[1,1],[3,3]]]
    [1,0,[[0,1],[2,2],[3,1]]]
    [2,0,[[1,2],[4,4]]]
    [3,0,[[0,3],[1,1],[4,4]]]
    [4,0,[[3,4],[2,4]]]
    ```

    <span data-ttu-id="3876b-156">這項資料會描述一種導向圖形，藉由使用 hello 格式中的物件之間的關聯性`[source_id, source_value,[[dest_id], [edge_value],...]]`。</span><span class="sxs-lookup"><span data-stu-id="3876b-156">This data describes a relationship between objects in a directed graph, by using hello format `[source_id, source_value,[[dest_id], [edge_value],...]]`.</span></span> <span data-ttu-id="3876b-157">每一行代表 `source_id` 物件和一或多個 `dest_id` 物件之間的關聯性。</span><span class="sxs-lookup"><span data-stu-id="3876b-157">Each line represents a relationship between a `source_id` object and one or more `dest_id` objects.</span></span> <span data-ttu-id="3876b-158">hello`edge_value`可以視為 hello 強度或 hello 連線之間的距離`source_id`和`dest\_id`。</span><span class="sxs-lookup"><span data-stu-id="3876b-158">hello `edge_value` can be thought of as hello strength or distance of hello connection between `source_id` and `dest\_id`.</span></span>

    <span data-ttu-id="3876b-159">繪製出，並使用 hello 值 （或加權），做為 hello 物件之間的距離，hello 資料看起來會像下列圖表中的 hello:</span><span class="sxs-lookup"><span data-stu-id="3876b-159">Drawn out, and using hello value (or weight) as hello distance between objects, hello data might look like hello following diagram:</span></span>

    ![tiny_graph.txt drawn as circles with lines of varying distance between](./media/hdinsight-hadoop-giraph-install-linux/giraph-graph.png)

3. <span data-ttu-id="3876b-161">toosave hello 檔案，使用**Ctrl + X**，然後**Y**，最後再**Enter** tooaccept hello 檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="3876b-161">toosave hello file, use **Ctrl+X**, then **Y**, and finally **Enter** tooaccept hello file name.</span></span>

4. <span data-ttu-id="3876b-162">使用下列 toostore hello 資料到您的 HDInsight 叢集的主要儲存體的 hello:</span><span class="sxs-lookup"><span data-stu-id="3876b-162">Use hello following toostore hello data into primary storage for your HDInsight cluster:</span></span>

    ```bash
    hdfs dfs -put tiny_graph.txt /example/data/tiny_graph.txt
    ```

5. <span data-ttu-id="3876b-163">使用下列命令的 hello 執行的 hello SimpleShortestPathsComputation 範例：</span><span class="sxs-lookup"><span data-stu-id="3876b-163">Run hello SimpleShortestPathsComputation example using hello following command:</span></span>

    ```bash
    yarn jar /usr/hdp/current/giraph/giraph-examples.jar org.apache.giraph.GiraphRunner org.apache.giraph.examples.SimpleShortestPathsComputation -ca mapred.job.tracker=headnodehost:9010 -vif org.apache.giraph.io.formats.JsonLongDoubleFloatDoubleVertexInputFormat -vip /example/data/tiny_graph.txt -vof org.apache.giraph.io.formats.IdWithValueTextOutputFormat -op /example/output/shortestpaths -w 2
    ```

    <span data-ttu-id="3876b-164">hello 下表描述此命令搭配使用的 hello 參數：</span><span class="sxs-lookup"><span data-stu-id="3876b-164">hello parameters used with this command are described in hello following table:</span></span>

   | <span data-ttu-id="3876b-165">參數</span><span class="sxs-lookup"><span data-stu-id="3876b-165">Parameter</span></span> | <span data-ttu-id="3876b-166">作用</span><span class="sxs-lookup"><span data-stu-id="3876b-166">What it does</span></span> |
   | --- | --- |
   | `jar` |<span data-ttu-id="3876b-167">包含 hello 範例 hello jar 檔案。</span><span class="sxs-lookup"><span data-stu-id="3876b-167">hello jar file containing hello examples.</span></span> |
   | `org.apache.giraph.GiraphRunner` |<span data-ttu-id="3876b-168">使用 toostart hello 範例 hello 類別。</span><span class="sxs-lookup"><span data-stu-id="3876b-168">hello class used toostart hello examples.</span></span> |
   | `org.apache.giraph.examples.SimpleShortestPathsCoputation` |<span data-ttu-id="3876b-169">hello 用的範例。</span><span class="sxs-lookup"><span data-stu-id="3876b-169">hello example that is used.</span></span> <span data-ttu-id="3876b-170">在此範例中，它會計算 hello 識別碼 1 和 hello 圖形中的所有其他識別碼之間的最短路徑。</span><span class="sxs-lookup"><span data-stu-id="3876b-170">In this example, it computes hello shortest path between ID 1 and all other IDs in hello graph.</span></span> |
   | `-ca mapred.job.tracker` |<span data-ttu-id="3876b-171">hello 叢集 hello 前端節點。</span><span class="sxs-lookup"><span data-stu-id="3876b-171">hello headnode for hello cluster.</span></span> |
   | `-vif` |<span data-ttu-id="3876b-172">hello 輸入的格式 toouse hello 輸入資料。</span><span class="sxs-lookup"><span data-stu-id="3876b-172">hello input format toouse for hello input data.</span></span> |
   | `-vip` |<span data-ttu-id="3876b-173">hello 輸入的資料檔。</span><span class="sxs-lookup"><span data-stu-id="3876b-173">hello input data file.</span></span> |
   | `-vof` |<span data-ttu-id="3876b-174">hello 輸出格式。</span><span class="sxs-lookup"><span data-stu-id="3876b-174">hello output format.</span></span> <span data-ttu-id="3876b-175">在此範例中，識別碼和值是純文字。</span><span class="sxs-lookup"><span data-stu-id="3876b-175">In this example, ID and value as plain text.</span></span> |
   | `-op` |<span data-ttu-id="3876b-176">hello 輸出位置。</span><span class="sxs-lookup"><span data-stu-id="3876b-176">hello output location.</span></span> |
   | `-w 2` |<span data-ttu-id="3876b-177">hello toouse 背景工作數目。</span><span class="sxs-lookup"><span data-stu-id="3876b-177">hello number of workers toouse.</span></span> <span data-ttu-id="3876b-178">在此範例中是 2。</span><span class="sxs-lookup"><span data-stu-id="3876b-178">In this example, 2.</span></span> |

    <span data-ttu-id="3876b-179">如需有關這些錯誤碼和其他 Giraph 範例搭配使用的參數的詳細資訊，請參閱 hello [Giraph 快速入門](http://giraph.apache.org/quick_start.html)。</span><span class="sxs-lookup"><span data-stu-id="3876b-179">For more information on these, and other parameters used with Giraph samples, see hello [Giraph quickstart](http://giraph.apache.org/quick_start.html).</span></span>

6. <span data-ttu-id="3876b-180">一旦 hello 工作已完成，hello 結果會儲存在 hello **/example/out/shotestpaths**目錄。</span><span class="sxs-lookup"><span data-stu-id="3876b-180">Once hello job has finished, hello results are stored in hello **/example/out/shotestpaths** directory.</span></span> <span data-ttu-id="3876b-181">hello 輸出檔案名稱的開頭**一部分-m-** ，而結尾數字，指出 hello 首先，第二，等檔案。</span><span class="sxs-lookup"><span data-stu-id="3876b-181">hello output file names begin with **part-m-** and end with a number indicating hello first, second, etc. file.</span></span> <span data-ttu-id="3876b-182">使用下列命令 tooview hello 輸出 hello:</span><span class="sxs-lookup"><span data-stu-id="3876b-182">Use hello following command tooview hello output:</span></span>

    ```bash
    hdfs dfs -text /example/output/shortestpaths/*
    ```

    <span data-ttu-id="3876b-183">hello 輸出應該看起來類似 toohello 下列文字：</span><span class="sxs-lookup"><span data-stu-id="3876b-183">hello output should appear similar toohello following text:</span></span>

        0    1.0
        4    5.0
        2    2.0
        1    0.0
        3    1.0

    <span data-ttu-id="3876b-184">hello SimpleShortestPathComputation 範例是硬式編碼的 toostart 與物件識別碼為 1，並尋找 hello 最短路徑 tooother 物件。</span><span class="sxs-lookup"><span data-stu-id="3876b-184">hello SimpleShortestPathComputation example is hard coded toostart with object ID 1 and find hello shortest path tooother objects.</span></span> <span data-ttu-id="3876b-185">hello 輸出的格式的 hello`destination_id`和`distance`。</span><span class="sxs-lookup"><span data-stu-id="3876b-185">hello output is in hello format of `destination_id` and `distance`.</span></span> <span data-ttu-id="3876b-186">hello`distance`為 hello 值 （或加權） 旅行 hello 邊緣的物件識別碼為 1 與 hello 目標 id。</span><span class="sxs-lookup"><span data-stu-id="3876b-186">hello `distance` is hello value (or weight) of hello edges traveled between object ID 1 and hello target ID.</span></span>

    <span data-ttu-id="3876b-187">視覺化資料，您可以確認 hello 結果識別碼 1 和所有其他物件之間旅行 hello 最短的路徑。</span><span class="sxs-lookup"><span data-stu-id="3876b-187">Visualizing this data, you can verify hello results by traveling hello shortest paths between ID 1 and all other objects.</span></span> <span data-ttu-id="3876b-188">hello 識別碼 1 和識別碼 4 之間的最短路徑為 5。</span><span class="sxs-lookup"><span data-stu-id="3876b-188">hello shortest path between ID 1 and ID 4 is 5.</span></span> <span data-ttu-id="3876b-189">此值為 hello 總之間的距離<span style="color:orange">識別碼 1 和 3</span>，然後<span style="color:red">ID 為 3 和 4</span>。</span><span class="sxs-lookup"><span data-stu-id="3876b-189">This value is hello total distance between <span style="color:orange">ID 1 and 3</span>, and then <span style="color:red">ID 3 and 4</span>.</span></span>

    ![Drawing of objects as circles with shortest paths drawn between](./media/hdinsight-hadoop-giraph-install-linux/giraph-graph-out.png)

## <a name="next-steps"></a><span data-ttu-id="3876b-191">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3876b-191">Next steps</span></span>

* <span data-ttu-id="3876b-192">[在 HDInsight 叢集上安裝及使用 Hue](hdinsight-hadoop-hue-linux.md)。</span><span class="sxs-lookup"><span data-stu-id="3876b-192">[Install and use Hue on HDInsight clusters](hdinsight-hadoop-hue-linux.md).</span></span>

* <span data-ttu-id="3876b-193">[在 HDInsight 叢集上安裝 Solr](hdinsight-hadoop-solr-install-linux.md)。</span><span class="sxs-lookup"><span data-stu-id="3876b-193">[Install Solr on HDInsight clusters](hdinsight-hadoop-solr-install-linux.md).</span></span>
