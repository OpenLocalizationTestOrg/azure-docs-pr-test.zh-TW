---
title: "搭配 HDInsight 來使用 Ambari Tez 檢視 - Azure | Microsoft Docs"
description: "了解如何在 HDInsight 上使用 Ambari Tez 檢視來為 Tez 作業偵錯。"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 9c39ea56-670b-4699-aba0-0f64c261e411
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: 65d89309b9eea8544b85d16687baa90d49688d77
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="use-ambari-views-to-debug-tez-jobs-on-hdinsight"></a><span data-ttu-id="cabfa-103">在 HDInsight 上使用 Ambari 檢視來為 Tez 作業偵錯</span><span class="sxs-lookup"><span data-stu-id="cabfa-103">Use Ambari Views to debug Tez Jobs on HDInsight</span></span>

<span data-ttu-id="cabfa-104">適用於 HDInsight 的 Ambari Web UI 包含 Tez 檢視，可用來了解使用 Tez 的作業，和為該類型作業偵錯。</span><span class="sxs-lookup"><span data-stu-id="cabfa-104">The Ambari Web UI for HDInsight contains a Tez view that can be used to understand and debug jobs that use Tez.</span></span> <span data-ttu-id="cabfa-105">Tez 檢視可讓您把作業視覺化有已連接項目的圖表、深入每個項目、取得統計資料，以及記錄資訊。</span><span class="sxs-lookup"><span data-stu-id="cabfa-105">The Tez view allows you to visualize the job as a graph of connected items, drill into each item, and retrieve statistics and logging information.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="cabfa-106">本文件中的步驟需要一個使用 Linux 的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="cabfa-106">The steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="cabfa-107">Linux 是唯一使用於 HDInsight 3.4 版或更新版本的作業系統。</span><span class="sxs-lookup"><span data-stu-id="cabfa-107">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="cabfa-108">如需詳細資訊，請參閱 [HDInsight 元件版本設定](hdinsight-component-versioning.md#hdinsight-windows-retirement)。</span><span class="sxs-lookup"><span data-stu-id="cabfa-108">For more information, see [HDInsight component versioning](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cabfa-109">必要條件</span><span class="sxs-lookup"><span data-stu-id="cabfa-109">Prerequisites</span></span>

* <span data-ttu-id="cabfa-110">以 Linux 為基礎的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="cabfa-110">A Linux-based HDInsight cluster.</span></span> <span data-ttu-id="cabfa-111">如需建立叢集的步驟，請參閱[開始使用以 Linux 為基礎的 HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="cabfa-111">For steps on creating a cluster, see [Get started using Linux-based HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).</span></span>
* <span data-ttu-id="cabfa-112">支援 HTML5 的新式網頁瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="cabfa-112">A modern web browser that supports HTML5.</span></span>

## <a name="understanding-tez"></a><span data-ttu-id="cabfa-113">了解 Tez</span><span class="sxs-lookup"><span data-stu-id="cabfa-113">Understanding Tez</span></span>

<span data-ttu-id="cabfa-114">Tez 是 Hadoop 中資料處理用的可延伸架構，資料處理的速度比傳統的 MapReduce 處理方式還要快。</span><span class="sxs-lookup"><span data-stu-id="cabfa-114">Tez is an extensible framework for data processing in Hadoop that provides greater speeds than traditional MapReduce processing.</span></span> <span data-ttu-id="cabfa-115">而對於 Linux 型 HDInsight 叢集來說，Tez 是 Hive 的預設引擎。</span><span class="sxs-lookup"><span data-stu-id="cabfa-115">For Linux-based HDInsight clusters, it is the default engine for Hive.</span></span>

<span data-ttu-id="cabfa-116">Tez 會建立有向非循環圖 (DAG)，說明作業所需動作的順序。</span><span class="sxs-lookup"><span data-stu-id="cabfa-116">Tez creates a Directed Acyclic Graph (DAG) that describes the order of actions required by jobs.</span></span> <span data-ttu-id="cabfa-117">個別的動作稱為頂點，它會執行整體作業的一部分。</span><span class="sxs-lookup"><span data-stu-id="cabfa-117">Individual actions are called vertices, and execute a piece of the overall job.</span></span> <span data-ttu-id="cabfa-118">而由端點所描述的實際工作 (Work) 執行程序稱為工作 (Task)，且可能會分散到叢集中的多個節點上。</span><span class="sxs-lookup"><span data-stu-id="cabfa-118">The actual execution of the work described by a vertex is called a task, and may be distributed across multiple nodes in the cluster.</span></span>

### <a name="understanding-the-tez-view"></a><span data-ttu-id="cabfa-119">了解 Tez 檢視</span><span class="sxs-lookup"><span data-stu-id="cabfa-119">Understanding the Tez view</span></span>

<span data-ttu-id="cabfa-120">Tez 檢視同時提供歷程記錄資訊和正在執行之處理序的資訊。</span><span class="sxs-lookup"><span data-stu-id="cabfa-120">The Tez view provides both historical information and information on processes that are running.</span></span> <span data-ttu-id="cabfa-121">這項資訊顯示作業如何分散到叢集。</span><span class="sxs-lookup"><span data-stu-id="cabfa-121">This information shows how a job is distributed across clusters.</span></span> <span data-ttu-id="cabfa-122">它也會顯示工作和頂點使用的計數器，以及與作業相關的錯誤資訊。</span><span class="sxs-lookup"><span data-stu-id="cabfa-122">It also displays counters used by tasks and vertices, and error information related to the job.</span></span> <span data-ttu-id="cabfa-123">它可能會提供下列案例中的有用資訊：</span><span class="sxs-lookup"><span data-stu-id="cabfa-123">It may offer useful information in the following scenarios:</span></span>

* <span data-ttu-id="cabfa-124">監視長期執行的處理序、檢視對應進度，以及減少工作。</span><span class="sxs-lookup"><span data-stu-id="cabfa-124">Monitoring long-running processes, viewing the progress of map and reduce tasks.</span></span>
* <span data-ttu-id="cabfa-125">分析成功或失敗的處理序歷史資料，以便了解如何改進處理序，或是處理序失敗的原因。</span><span class="sxs-lookup"><span data-stu-id="cabfa-125">Analyzing historical data for successful or failed processes to learn how processing could be improved or why it failed.</span></span>

## <a name="generate-a-dag"></a><span data-ttu-id="cabfa-126">產生 DAG</span><span class="sxs-lookup"><span data-stu-id="cabfa-126">Generate a DAG</span></span>

<span data-ttu-id="cabfa-127">Tez 檢視只有在使用 Tez 引擎的作業目前正在執行，或先前曾執行過才會包含資料。</span><span class="sxs-lookup"><span data-stu-id="cabfa-127">The Tez view only contains data if a job that uses the Tez engine is currently running, or has been ran previously.</span></span> <span data-ttu-id="cabfa-128">簡單的 Hive 查詢可不使用 Tez 進行解析。</span><span class="sxs-lookup"><span data-stu-id="cabfa-128">Simple Hive queries can be resolved without using Tez.</span></span> <span data-ttu-id="cabfa-129">複雜的查詢會執行諸如篩選、群組、排序、聯結等等</span><span class="sxs-lookup"><span data-stu-id="cabfa-129">More complex queries that do filtering, grouping, ordering, joins, etc.</span></span> <span data-ttu-id="cabfa-130">則需使用 Tez 引擎。</span><span class="sxs-lookup"><span data-stu-id="cabfa-130">use the Tez engine.</span></span>

<span data-ttu-id="cabfa-131">使用下列步驟來執行使用 Tez 的 Hive 查詢：</span><span class="sxs-lookup"><span data-stu-id="cabfa-131">Use the following steps to run a Hive query that uses Tez:</span></span>

1. <span data-ttu-id="cabfa-132">在網頁瀏覽器中瀏覽至 https://CLUSTERNAME.azurehdinsight.net，其中 **CLUSTERNAME** 是 HDInsight 叢集的名稱。</span><span class="sxs-lookup"><span data-stu-id="cabfa-132">In a web browser, navigate to https://CLUSTERNAME.azurehdinsight.net, where **CLUSTERNAME** is the name of your HDInsight cluster.</span></span>

2. <span data-ttu-id="cabfa-133">在頁面頂端的功能表中，選取 [檢視] 圖示。</span><span class="sxs-lookup"><span data-stu-id="cabfa-133">From the menu at the top of the page, select the **Views** icon.</span></span> <span data-ttu-id="cabfa-134">此圖示看起來像一系列正方形。</span><span class="sxs-lookup"><span data-stu-id="cabfa-134">This icon looks like a series of squares.</span></span> <span data-ttu-id="cabfa-135">在隨後出現的下拉式清單中，選取 [Hive 檢視]。</span><span class="sxs-lookup"><span data-stu-id="cabfa-135">In the dropdown that appears, select **Hive view**.</span></span>

    ![選取 [Hive 檢視]](./media/hdinsight-debug-ambari-tez-view/selecthive.png)

3. <span data-ttu-id="cabfa-137">當 Hive 檢視載入之後，在查詢編輯器中貼上下列查詢，然後按一下 [執行]。</span><span class="sxs-lookup"><span data-stu-id="cabfa-137">When the Hive view loads, paste the following query into the Query Editor, and then click **execute**.</span></span>

        select market, state, country from hivesampletable where deviceplatform='Android' group by market, country, state;

    <span data-ttu-id="cabfa-138">當作業完成之後，您應該會在 [查詢處理程序結果] 區段看到輸出。</span><span class="sxs-lookup"><span data-stu-id="cabfa-138">Once the job has completed, you should see the output displayed in the **Query Process Results** section.</span></span> <span data-ttu-id="cabfa-139">結果應該會與下列文字類似：</span><span class="sxs-lookup"><span data-stu-id="cabfa-139">The results should be similar to the following text:</span></span>

        market  state       country
        en-GB   Hessen      Germany
        en-GB   Kingston    Jamaica

4. <span data-ttu-id="cabfa-140">選取 [記錄] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="cabfa-140">Select the **Log** tab.</span></span> <span data-ttu-id="cabfa-141">您會看到類似下列文字的資訊：</span><span class="sxs-lookup"><span data-stu-id="cabfa-141">You see information similar to the following text:</span></span>

        INFO : Session is already open
        INFO :

        INFO : Status: Running (Executing on YARN cluster with App id application_1454546500517_0063)

    <span data-ttu-id="cabfa-142">請儲存 **App id** 的值，因為您會在下一節中使用它。</span><span class="sxs-lookup"><span data-stu-id="cabfa-142">Save the **App id** value, as this value is used in the next section.</span></span>

## <a name="use-the-tez-view"></a><span data-ttu-id="cabfa-143">使用 Tez 檢視</span><span class="sxs-lookup"><span data-stu-id="cabfa-143">Use the Tez View</span></span>

1. <span data-ttu-id="cabfa-144">在頁面頂端的功能表中，選取 [檢視] 圖示。</span><span class="sxs-lookup"><span data-stu-id="cabfa-144">From the menu at the top of the page, select the **Views** icon.</span></span> <span data-ttu-id="cabfa-145">在隨後出現的下拉式清單中，選取 [Tez 檢視]。</span><span class="sxs-lookup"><span data-stu-id="cabfa-145">In the dropdown that appears, select **Tez view**.</span></span>

    ![選取 [Tez 檢視]](./media/hdinsight-debug-ambari-tez-view/selecttez.png)

2. <span data-ttu-id="cabfa-147">當 Tez 檢視載入時，您會看到正在或曾經在叢集上執行的 Hive 查詢清單。</span><span class="sxs-lookup"><span data-stu-id="cabfa-147">When the Tez view loads, you see a list of hive queries that are currently running, or have been ran on the cluster.</span></span>

    ![所有 DAG](./media/hdinsight-debug-ambari-tez-view/tez-view-home.png)

3. <span data-ttu-id="cabfa-149">如果您只有一個項目，則它是您在上一節中執行的查詢。</span><span class="sxs-lookup"><span data-stu-id="cabfa-149">If you have only one entry, it is for the query that you ran in the previous section.</span></span> <span data-ttu-id="cabfa-150">如果您有多個項目，可以使用頁面頂端的欄位搜尋。</span><span class="sxs-lookup"><span data-stu-id="cabfa-150">If you have multiple entries, you can search by using the fields at the top of the page.</span></span>

4. <span data-ttu-id="cabfa-151">選取 Hive 查詢的 [Query ID] \(查詢識別碼\)。</span><span class="sxs-lookup"><span data-stu-id="cabfa-151">Select the **Query ID** for a Hive query.</span></span> <span data-ttu-id="cabfa-152">關於查詢的詳細資訊隨即顯示。</span><span class="sxs-lookup"><span data-stu-id="cabfa-152">Information about the query is displayed.</span></span>

    ![DAG 詳細資料](./media/hdinsight-debug-ambari-tez-view/query-details.png)

5. <span data-ttu-id="cabfa-154">此頁面上的索引標籤可讓您檢視下列資訊：</span><span class="sxs-lookup"><span data-stu-id="cabfa-154">The tabs on this page allow you to view the following information:</span></span>

    * <span data-ttu-id="cabfa-155">**查詢詳細資料**：Hive 查詢的相關詳細資料。</span><span class="sxs-lookup"><span data-stu-id="cabfa-155">**Query Details**: Details about the Hive query.</span></span>
    * <span data-ttu-id="cabfa-156">**時間軸**：每個處理階段所耗費時間的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="cabfa-156">**Timeline**: Information about how long each stage of processing took.</span></span>
    * <span data-ttu-id="cabfa-157">**設定**：此查詢使用的設定。</span><span class="sxs-lookup"><span data-stu-id="cabfa-157">**Configurations**: The configuration used for this query.</span></span>

    <span data-ttu-id="cabfa-158">從 [Query Details] \(查詢詳細資料\)，您可以使用連結來尋找和此查詢的 [Application] \(應用程式\) 或 [DAG] 相關的資訊。</span><span class="sxs-lookup"><span data-stu-id="cabfa-158">From __Query Details__ you can use the links to find information about the __Application__ or the __DAG__ for this query.</span></span>
    
    * <span data-ttu-id="cabfa-159">[Application] \(應用程式\) 連結會顯示此查詢的 YARN 應用程式相關資訊。</span><span class="sxs-lookup"><span data-stu-id="cabfa-159">The __Application__ link displays information about the YARN application for this query.</span></span> <span data-ttu-id="cabfa-160">您可以從此處存取 YARN 應用程式記錄檔。</span><span class="sxs-lookup"><span data-stu-id="cabfa-160">From here you can access the YARN application logs.</span></span>
    * <span data-ttu-id="cabfa-161">[DAG] 連結會顯示此查詢的有向非循環圖相關資訊。</span><span class="sxs-lookup"><span data-stu-id="cabfa-161">The __DAG__ link displays information about the directed acyclic graph for this query.</span></span> <span data-ttu-id="cabfa-162">您可以從此處以圖形化的方式檢視 DAG。</span><span class="sxs-lookup"><span data-stu-id="cabfa-162">From here you can view a graphical representation of the DAG.</span></span> <span data-ttu-id="cabfa-163">您也可以尋找關於 DAG 內之頂點的資訊。</span><span class="sxs-lookup"><span data-stu-id="cabfa-163">You can also find information on the vertices within the DAG.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cabfa-164">後續步驟</span><span class="sxs-lookup"><span data-stu-id="cabfa-164">Next Steps</span></span>

<span data-ttu-id="cabfa-165">既然您已了解如何使用 Tez 檢視，請深入了解 [在 HDInsight 上使用 Hive](hdinsight-use-hive.md)。</span><span class="sxs-lookup"><span data-stu-id="cabfa-165">Now that you have learned how to use the Tez view, learn more about [Using Hive on HDInsight](hdinsight-use-hive.md).</span></span>

<span data-ttu-id="cabfa-166">如需 Tez 的詳細技術資訊，請參閱 [Hortonworks 的 Tez 頁面](http://hortonworks.com/hadoop/tez/)。</span><span class="sxs-lookup"><span data-stu-id="cabfa-166">For more detailed technical information on Tez, see the [Tez page at Hortonworks](http://hortonworks.com/hadoop/tez/).</span></span>

<span data-ttu-id="cabfa-167">如需如何搭配 HDInsight 來使用 Ambari 的詳細資訊，請參閱 [使用 Ambari Web UI 管理 HDInsight 叢集](hdinsight-hadoop-manage-ambari.md)</span><span class="sxs-lookup"><span data-stu-id="cabfa-167">For more information on using Ambari with HDInsight, see [Manage HDInsight clusters using the Ambari Web UI](hdinsight-hadoop-manage-ambari.md)</span></span>
