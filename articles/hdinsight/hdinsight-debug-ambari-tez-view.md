---
title: "aaaUse Ambari Tez 檢視與 HDInsight 的 Azure |Microsoft 文件"
description: "了解 toouse hello Ambari Tez HDInsight 上檢視 toodebug Tez 作業的方式。"
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
ms.openlocfilehash: 5d61bd0403c98284c86982073af91468ae62ac60
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-ambari-views-toodebug-tez-jobs-on-hdinsight"></a><span data-ttu-id="5a72b-103">HDInsight 上使用 Ambari 檢視 toodebug Tez 作業</span><span class="sxs-lookup"><span data-stu-id="5a72b-103">Use Ambari Views toodebug Tez Jobs on HDInsight</span></span>

<span data-ttu-id="5a72b-104">hello Ambari Web UI hdinsight 包含 Tez 檢視可以使用使用 Tez toounderstand 和偵錯作業。</span><span class="sxs-lookup"><span data-stu-id="5a72b-104">hello Ambari Web UI for HDInsight contains a Tez view that can be used toounderstand and debug jobs that use Tez.</span></span> <span data-ttu-id="5a72b-105">hello Tez 檢視可讓您 toovisualize hello 作業的已連接的項目圖形下鑽研至每個項目，以及擷取統計資料和記錄資訊。</span><span class="sxs-lookup"><span data-stu-id="5a72b-105">hello Tez view allows you toovisualize hello job as a graph of connected items, drill into each item, and retrieve statistics and logging information.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5a72b-106">本文件中的 hello 步驟需要使用 Linux 的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="5a72b-106">hello steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="5a72b-107">Linux 為 hello 僅作業系統 HDInsight 3.4 或更新版本上使用。</span><span class="sxs-lookup"><span data-stu-id="5a72b-107">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="5a72b-108">如需詳細資訊，請參閱 [HDInsight 元件版本設定](hdinsight-component-versioning.md#hdinsight-windows-retirement)。</span><span class="sxs-lookup"><span data-stu-id="5a72b-108">For more information, see [HDInsight component versioning](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5a72b-109">必要條件</span><span class="sxs-lookup"><span data-stu-id="5a72b-109">Prerequisites</span></span>

* <span data-ttu-id="5a72b-110">以 Linux 為基礎的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="5a72b-110">A Linux-based HDInsight cluster.</span></span> <span data-ttu-id="5a72b-111">如需建立叢集的步驟，請參閱[開始使用以 Linux 為基礎的 HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="5a72b-111">For steps on creating a cluster, see [Get started using Linux-based HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).</span></span>
* <span data-ttu-id="5a72b-112">支援 HTML5 的新式網頁瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="5a72b-112">A modern web browser that supports HTML5.</span></span>

## <a name="understanding-tez"></a><span data-ttu-id="5a72b-113">了解 Tez</span><span class="sxs-lookup"><span data-stu-id="5a72b-113">Understanding Tez</span></span>

<span data-ttu-id="5a72b-114">Tez 是 Hadoop 中資料處理用的可延伸架構，資料處理的速度比傳統的 MapReduce 處理方式還要快。</span><span class="sxs-lookup"><span data-stu-id="5a72b-114">Tez is an extensible framework for data processing in Hadoop that provides greater speeds than traditional MapReduce processing.</span></span> <span data-ttu-id="5a72b-115">以 Linux 為基礎的 HDInsight 叢集，則是 Hive hello 預設的引擎。</span><span class="sxs-lookup"><span data-stu-id="5a72b-115">For Linux-based HDInsight clusters, it is hello default engine for Hive.</span></span>

<span data-ttu-id="5a72b-116">Tez 建立導向非循環圖 (DAG) 來描述 hello 順序的作業所需的動作。</span><span class="sxs-lookup"><span data-stu-id="5a72b-116">Tez creates a Directed Acyclic Graph (DAG) that describes hello order of actions required by jobs.</span></span> <span data-ttu-id="5a72b-117">個別的動作稱為頂點，和執行一段 hello 整體的作業。</span><span class="sxs-lookup"><span data-stu-id="5a72b-117">Individual actions are called vertices, and execute a piece of hello overall job.</span></span> <span data-ttu-id="5a72b-118">hello 實際執行的 hello 頂點所描述的工作稱為工作，並可能散佈在 hello 叢集中的多個節點。</span><span class="sxs-lookup"><span data-stu-id="5a72b-118">hello actual execution of hello work described by a vertex is called a task, and may be distributed across multiple nodes in hello cluster.</span></span>

### <a name="understanding-hello-tez-view"></a><span data-ttu-id="5a72b-119">了解 hello Tez 檢視</span><span class="sxs-lookup"><span data-stu-id="5a72b-119">Understanding hello Tez view</span></span>

<span data-ttu-id="5a72b-120">hello Tez 檢視上執行的處理序中提供的歷程記錄資訊和資訊。</span><span class="sxs-lookup"><span data-stu-id="5a72b-120">hello Tez view provides both historical information and information on processes that are running.</span></span> <span data-ttu-id="5a72b-121">這項資訊顯示作業如何分散到叢集。</span><span class="sxs-lookup"><span data-stu-id="5a72b-121">This information shows how a job is distributed across clusters.</span></span> <span data-ttu-id="5a72b-122">它也會顯示使用工作和頂點，計數器以及錯誤相關的資訊 toohello 作業。</span><span class="sxs-lookup"><span data-stu-id="5a72b-122">It also displays counters used by tasks and vertices, and error information related toohello job.</span></span> <span data-ttu-id="5a72b-123">它可能提供有用的資訊，在下列案例的 hello:</span><span class="sxs-lookup"><span data-stu-id="5a72b-123">It may offer useful information in hello following scenarios:</span></span>

* <span data-ttu-id="5a72b-124">監視長時間執行處理程序，檢視 hello 對應的進度，並減少的工作。</span><span class="sxs-lookup"><span data-stu-id="5a72b-124">Monitoring long-running processes, viewing hello progress of map and reduce tasks.</span></span>
* <span data-ttu-id="5a72b-125">分析成功或失敗的處理序 toolearn 歷程記錄資料，處理方式可提升或失敗的原因。</span><span class="sxs-lookup"><span data-stu-id="5a72b-125">Analyzing historical data for successful or failed processes toolearn how processing could be improved or why it failed.</span></span>

## <a name="generate-a-dag"></a><span data-ttu-id="5a72b-126">產生 DAG</span><span class="sxs-lookup"><span data-stu-id="5a72b-126">Generate a DAG</span></span>

<span data-ttu-id="5a72b-127">hello Tez 檢視只包含資料，如果工作使用 hello Tez 引擎目前正在執行，或先前執行。</span><span class="sxs-lookup"><span data-stu-id="5a72b-127">hello Tez view only contains data if a job that uses hello Tez engine is currently running, or has been ran previously.</span></span> <span data-ttu-id="5a72b-128">簡單的 Hive 查詢可不使用 Tez 進行解析。</span><span class="sxs-lookup"><span data-stu-id="5a72b-128">Simple Hive queries can be resolved without using Tez.</span></span> <span data-ttu-id="5a72b-129">複雜的查詢會執行諸如篩選、群組、排序、聯結等等</span><span class="sxs-lookup"><span data-stu-id="5a72b-129">More complex queries that do filtering, grouping, ordering, joins, etc.</span></span> <span data-ttu-id="5a72b-130">使用 hello Tez 引擎。</span><span class="sxs-lookup"><span data-stu-id="5a72b-130">use hello Tez engine.</span></span>

<span data-ttu-id="5a72b-131">使用下列步驟 toorun 使用 Tez 的 Hive 查詢的 hello:</span><span class="sxs-lookup"><span data-stu-id="5a72b-131">Use hello following steps toorun a Hive query that uses Tez:</span></span>

1. <span data-ttu-id="5a72b-132">在 web 瀏覽器中，瀏覽 toohttps://CLUSTERNAME.azurehdinsight.net，其中**CLUSTERNAME** hello 您的 HDInsight 叢集名稱。</span><span class="sxs-lookup"><span data-stu-id="5a72b-132">In a web browser, navigate toohttps://CLUSTERNAME.azurehdinsight.net, where **CLUSTERNAME** is hello name of your HDInsight cluster.</span></span>

2. <span data-ttu-id="5a72b-133">從 hello 頁面頂端的 hello hello 功能表上，選取 hello**檢視**圖示。</span><span class="sxs-lookup"><span data-stu-id="5a72b-133">From hello menu at hello top of hello page, select hello **Views** icon.</span></span> <span data-ttu-id="5a72b-134">此圖示看起來像一系列正方形。</span><span class="sxs-lookup"><span data-stu-id="5a72b-134">This icon looks like a series of squares.</span></span> <span data-ttu-id="5a72b-135">在出現的 hello 下拉式清單中選取**Hive 檢視**。</span><span class="sxs-lookup"><span data-stu-id="5a72b-135">In hello dropdown that appears, select **Hive view**.</span></span>

    ![選取 [Hive 檢視]](./media/hdinsight-debug-ambari-tez-view/selecthive.png)

3. <span data-ttu-id="5a72b-137">當 hello Hive 檢視載入時，貼上 hello 以下查詢 hello 查詢編輯器中，並按一下**執行**。</span><span class="sxs-lookup"><span data-stu-id="5a72b-137">When hello Hive view loads, paste hello following query into hello Query Editor, and then click **execute**.</span></span>

        select market, state, country from hivesampletable where deviceplatform='Android' group by market, country, state;

    <span data-ttu-id="5a72b-138">Hello 作業完成後，您應該會看到 hello 輸出顯示在 hello**查詢程序結果**> 一節。</span><span class="sxs-lookup"><span data-stu-id="5a72b-138">Once hello job has completed, you should see hello output displayed in hello **Query Process Results** section.</span></span> <span data-ttu-id="5a72b-139">hello 結果應該類似 toohello 下列文字：</span><span class="sxs-lookup"><span data-stu-id="5a72b-139">hello results should be similar toohello following text:</span></span>

        market  state       country
        en-GB   Hessen      Germany
        en-GB   Kingston    Jamaica

4. <span data-ttu-id="5a72b-140">選取 hello**記錄** 索引標籤。您會看到下列文字的資訊類似 toohello:</span><span class="sxs-lookup"><span data-stu-id="5a72b-140">Select hello **Log** tab. You see information similar toohello following text:</span></span>

        INFO : Session is already open
        INFO :

        INFO : Status: Running (Executing on YARN cluster with App id application_1454546500517_0063)

    <span data-ttu-id="5a72b-141">儲存 hello**應用程式識別碼**值，這個值用於 hello 下一節。</span><span class="sxs-lookup"><span data-stu-id="5a72b-141">Save hello **App id** value, as this value is used in hello next section.</span></span>

## <a name="use-hello-tez-view"></a><span data-ttu-id="5a72b-142">使用 hello Tez 檢視</span><span class="sxs-lookup"><span data-stu-id="5a72b-142">Use hello Tez View</span></span>

1. <span data-ttu-id="5a72b-143">從 hello 頁面頂端的 hello hello 功能表上，選取 hello**檢視**圖示。</span><span class="sxs-lookup"><span data-stu-id="5a72b-143">From hello menu at hello top of hello page, select hello **Views** icon.</span></span> <span data-ttu-id="5a72b-144">在出現的 hello 下拉式清單中選取**Tez 檢視**。</span><span class="sxs-lookup"><span data-stu-id="5a72b-144">In hello dropdown that appears, select **Tez view**.</span></span>

    ![選取 [Tez 檢視]](./media/hdinsight-debug-ambari-tez-view/selecttez.png)

2. <span data-ttu-id="5a72b-146">Hello Tez 檢視載入時，您會看到一份目前正在執行，或者已被 hive 查詢執行 hello 叢集上。</span><span class="sxs-lookup"><span data-stu-id="5a72b-146">When hello Tez view loads, you see a list of hive queries that are currently running, or have been ran on hello cluster.</span></span>

    ![所有 DAG](./media/hdinsight-debug-ambari-tez-view/tez-view-home.png)

3. <span data-ttu-id="5a72b-148">如果您有只有一個項目時，它是您已執行 hello 前一節中的 hello 查詢。</span><span class="sxs-lookup"><span data-stu-id="5a72b-148">If you have only one entry, it is for hello query that you ran in hello previous section.</span></span> <span data-ttu-id="5a72b-149">如果您有多個項目，您可以使用 hello 頁面頂端的 hello hello 欄位進行搜尋。</span><span class="sxs-lookup"><span data-stu-id="5a72b-149">If you have multiple entries, you can search by using hello fields at hello top of hello page.</span></span>

4. <span data-ttu-id="5a72b-150">選取 hello**查詢識別碼**Hive 查詢。</span><span class="sxs-lookup"><span data-stu-id="5a72b-150">Select hello **Query ID** for a Hive query.</span></span> <span data-ttu-id="5a72b-151">會顯示 hello 查詢的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="5a72b-151">Information about hello query is displayed.</span></span>

    ![DAG 詳細資料](./media/hdinsight-debug-ambari-tez-view/query-details.png)

5. <span data-ttu-id="5a72b-153">此頁面上的 hello 索引標籤可讓您 tooview hello 下列資訊：</span><span class="sxs-lookup"><span data-stu-id="5a72b-153">hello tabs on this page allow you tooview hello following information:</span></span>

    * <span data-ttu-id="5a72b-154">**查詢詳細資料**: hello Hive 查詢的相關詳細資料。</span><span class="sxs-lookup"><span data-stu-id="5a72b-154">**Query Details**: Details about hello Hive query.</span></span>
    * <span data-ttu-id="5a72b-155">**時間軸**：每個處理階段所耗費時間的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="5a72b-155">**Timeline**: Information about how long each stage of processing took.</span></span>
    * <span data-ttu-id="5a72b-156">**設定**: hello 組態用於這個查詢。</span><span class="sxs-lookup"><span data-stu-id="5a72b-156">**Configurations**: hello configuration used for this query.</span></span>

    <span data-ttu-id="5a72b-157">從__查詢詳細資料__您可以使用 hello 連結 toofind hello 資訊__應用程式__或 hello __DAG__這個查詢。</span><span class="sxs-lookup"><span data-stu-id="5a72b-157">From __Query Details__ you can use hello links toofind information about hello __Application__ or hello __DAG__ for this query.</span></span>
    
    * <span data-ttu-id="5a72b-158">hello__應用程式__連結顯示 hello 這個查詢的 YARN 應用程式的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="5a72b-158">hello __Application__ link displays information about hello YARN application for this query.</span></span> <span data-ttu-id="5a72b-159">您可以從這裡存取 hello YARN 應用程式記錄檔。</span><span class="sxs-lookup"><span data-stu-id="5a72b-159">From here you can access hello YARN application logs.</span></span>
    * <span data-ttu-id="5a72b-160">hello __DAG__連結顯示 hello 導向非循環的圖形這個查詢的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="5a72b-160">hello __DAG__ link displays information about hello directed acyclic graph for this query.</span></span> <span data-ttu-id="5a72b-161">您可以從此處檢視 hello DAG 的圖形表示法。</span><span class="sxs-lookup"><span data-stu-id="5a72b-161">From here you can view a graphical representation of hello DAG.</span></span> <span data-ttu-id="5a72b-162">您也可以尋找 hello DAG 中的 hello 頂點上的資訊。</span><span class="sxs-lookup"><span data-stu-id="5a72b-162">You can also find information on hello vertices within hello DAG.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5a72b-163">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5a72b-163">Next Steps</span></span>

<span data-ttu-id="5a72b-164">既然您已經學會如何 toouse hello Tez 檢視，深入了解[HDInsight 上使用 Hive](hdinsight-use-hive.md)。</span><span class="sxs-lookup"><span data-stu-id="5a72b-164">Now that you have learned how toouse hello Tez view, learn more about [Using Hive on HDInsight](hdinsight-use-hive.md).</span></span>

<span data-ttu-id="5a72b-165">如需詳細 Tez 上的技術資訊，請參閱 hello [Hortonworks Tez 頁面](http://hortonworks.com/hadoop/tez/)。</span><span class="sxs-lookup"><span data-stu-id="5a72b-165">For more detailed technical information on Tez, see hello [Tez page at Hortonworks](http://hortonworks.com/hadoop/tez/).</span></span>

<span data-ttu-id="5a72b-166">在 HDInsight 中使用 Ambari 的詳細資訊，請參閱[使用 hello Ambari Web UI 管理 HDInsight 叢集](hdinsight-hadoop-manage-ambari.md)</span><span class="sxs-lookup"><span data-stu-id="5a72b-166">For more information on using Ambari with HDInsight, see [Manage HDInsight clusters using hello Ambari Web UI](hdinsight-hadoop-manage-ambari.md)</span></span>
