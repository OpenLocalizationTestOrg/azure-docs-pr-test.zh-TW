---
title: "在以 Windows 為基礎的 HDInsight 中使用 Tez UI - Azure | Microsoft Docs"
description: "了解在以 Windows 為基礎的 HDInsight 上如何使用 Tez UI 偵錯 Tez 作業。"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: a55bccb9-7c32-4ff2-b654-213a2354bd5c
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 01/17/2017
ms.author: larryfr
ROBOTS: NOINDEX
ms.openlocfilehash: 3889fa1c3523eb0330cbe3b7640fd8590a5ceadf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-tez-ui-to-debug-tez-jobs-on-windows-based-hdinsight"></a><span data-ttu-id="a0537-103">在以 Windows 為基礎的 HDInsight 上使用 Tez UI 偵錯 Tez 作業</span><span class="sxs-lookup"><span data-stu-id="a0537-103">Use the Tez UI to debug Tez Jobs on Windows-based HDInsight</span></span>
<span data-ttu-id="a0537-104">對於在以 Windows 為基礎的 HDInsight 叢集上使用 Tez 作為執行引擎的作業，Tez UI 是一個可用來了解和偵錯這些作業的網頁。</span><span class="sxs-lookup"><span data-stu-id="a0537-104">The Tez UI is a web page that can be used to understand and debug jobs that use Tez as the execution engine on Windows-based HDInsight clusters.</span></span> <span data-ttu-id="a0537-105">Tez UI 可讓您把作業視覺化有已連接項目的圖表、深入每個項目、取得統計資料，以及記錄資訊。</span><span class="sxs-lookup"><span data-stu-id="a0537-105">The Tez UI allows you to visualize the job as a graph of connected items, drill into each item, and retrieve statistics and logging information.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a0537-106">本文件中的步驟需要一個使用 Windows 的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="a0537-106">The steps in this document require an HDInsight cluster that uses Windows.</span></span> <span data-ttu-id="a0537-107">Linux 是唯一使用於 HDInsight 3.4 版或更新版本的作業系統。</span><span class="sxs-lookup"><span data-stu-id="a0537-107">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="a0537-108">如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。</span><span class="sxs-lookup"><span data-stu-id="a0537-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a0537-109">必要條件</span><span class="sxs-lookup"><span data-stu-id="a0537-109">Prerequisites</span></span>
* <span data-ttu-id="a0537-110">以 Windows 為基礎的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="a0537-110">A Windows-based HDInsight cluster.</span></span> <span data-ttu-id="a0537-111">如需建立新叢集的步驟，請參閱 [開始使用以 Windows 為基礎的 HDInsight](hdinsight-hadoop-tutorial-get-started-windows.md)。</span><span class="sxs-lookup"><span data-stu-id="a0537-111">For steps on creating a new cluster, see [Get started using Windows-based HDInsight](hdinsight-hadoop-tutorial-get-started-windows.md).</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="a0537-112">只有在 2016 年 2 月 8 日之後建立的以 Windows 為基礎的 HDInsight 叢集上才能使用 Tez UI。</span><span class="sxs-lookup"><span data-stu-id="a0537-112">The Tez UI is only available on Windows-based HDInsight clusters created after February 8th, 2016.</span></span>
  >
  >
* <span data-ttu-id="a0537-113">以 Windows 為基礎的遠端桌面用戶端。</span><span class="sxs-lookup"><span data-stu-id="a0537-113">A Windows-based Remote Desktop client.</span></span>

## <a name="understanding-tez"></a><span data-ttu-id="a0537-114">了解 Tez</span><span class="sxs-lookup"><span data-stu-id="a0537-114">Understanding Tez</span></span>
<span data-ttu-id="a0537-115">Tez 是 Hadoop 中資料處理用的可延伸架構，資料處理的速度比傳統的 MapReduce 處理方式還要快。</span><span class="sxs-lookup"><span data-stu-id="a0537-115">Tez is an extensible framework for data processing in Hadoop that provides greater speeds than traditional MapReduce processing.</span></span> <span data-ttu-id="a0537-116">對於以 Windows 為基礎的 HDInsight 叢集，它是選擇性的引擎，只要在 Hive 查詢中使用下列命令，就可以對 Hive 啟用它：</span><span class="sxs-lookup"><span data-stu-id="a0537-116">For Windows-based HDInsight clusters, it is an optional engine that you can enable for Hive by using the following command as part of your Hive query:</span></span>

    set hive.execution.engine=tez;

<span data-ttu-id="a0537-117">當工作提交到 Tez 時，Tez 會建立有向非循環圖 (DAG) 來說明該作業所需動作的執行順序。</span><span class="sxs-lookup"><span data-stu-id="a0537-117">When work is submitted to Tez, it creates a Directed Acyclic Graph (DAG) that describes the order of execution of the actions required by the job.</span></span> <span data-ttu-id="a0537-118">個別的動作稱為頂點，它會執行整體作業的一部分。</span><span class="sxs-lookup"><span data-stu-id="a0537-118">Individual actions are called vertices, and execute a piece of the overall job.</span></span> <span data-ttu-id="a0537-119">由頂點所描述的實際工作 (Work) 執行程序稱為工作 (Task)，且可能會分散到叢集中的多個節點上。</span><span class="sxs-lookup"><span data-stu-id="a0537-119">The actual execution of the work described by a vertex is called a task, and may be distributed across multiple nodes in the cluster.</span></span>

### <a name="understanding-the-tez-ui"></a><span data-ttu-id="a0537-120">了解 Tez UI</span><span class="sxs-lookup"><span data-stu-id="a0537-120">Understanding the Tez UI</span></span>
<span data-ttu-id="a0537-121">針對使用 Tez 正在執行或先前執行的處理序，Tez UI 是一個提供相關資訊的網頁。</span><span class="sxs-lookup"><span data-stu-id="a0537-121">The Tez UI is a web page provides information on processes that are running, or have previously ran using Tez.</span></span> <span data-ttu-id="a0537-122">它能讓您檢視由 Tez 所產生的 DAG、它如何分散到不同叢集上、計數器 (例如工作及頂點所使用的記憶體)，以及錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="a0537-122">It allows you to view the DAG generated by Tez, how it is distributed across clusters, counters such as memory used by tasks and vertices, and error information.</span></span> <span data-ttu-id="a0537-123">它可能會提供下列案例中的有用資訊：</span><span class="sxs-lookup"><span data-stu-id="a0537-123">It may offer useful information in the following scenarios:</span></span>

* <span data-ttu-id="a0537-124">監視長期執行的處理序、檢視對應進度，以及減少工作。</span><span class="sxs-lookup"><span data-stu-id="a0537-124">Monitoring long-running processes, viewing the progress of map and reduce tasks.</span></span>
* <span data-ttu-id="a0537-125">分析成功或失敗的處理序歷史資料，以便了解如何改進處理序，或是處理序失敗的原因。</span><span class="sxs-lookup"><span data-stu-id="a0537-125">Analyzing historical data for successful or failed processes to learn how processing could be improved or why it failed.</span></span>

## <a name="generate-a-dag"></a><span data-ttu-id="a0537-126">產生 DAG</span><span class="sxs-lookup"><span data-stu-id="a0537-126">Generate a DAG</span></span>
<span data-ttu-id="a0537-127">Tez UI 只包含正在或曾經使用 Tez 引擎來執行之作業的資料。</span><span class="sxs-lookup"><span data-stu-id="a0537-127">The Tez UI will only contain data if a job that uses the Tez engine is currently running, or has been ran in the past.</span></span> <span data-ttu-id="a0537-128">簡單的 Hive 查詢通常不用 Tez 就能解決，但更複雜的查詢 (會進行篩選、分組、排序、 聯結等) 通常需要使用 Tez。</span><span class="sxs-lookup"><span data-stu-id="a0537-128">Simple Hive queries can usually be resolved without using Tez, however more complex queries that do filtering, grouping, ordering, joins, etc. will usually require Tez.</span></span>

<span data-ttu-id="a0537-129">請使用下列步驟，來執行會使用 Tez 來執行的 Hive 查詢。</span><span class="sxs-lookup"><span data-stu-id="a0537-129">Use the following steps to run a Hive query that will execute using Tez.</span></span>

1. <span data-ttu-id="a0537-130">在網頁瀏覽器中瀏覽至 https://CLUSTERNAME.azurehdinsight.net，其中 **CLUSTERNAME** 是 HDInsight 叢集的名稱。</span><span class="sxs-lookup"><span data-stu-id="a0537-130">In a web browser, navigate to https://CLUSTERNAME.azurehdinsight.net, where **CLUSTERNAME** is the name of your HDInsight cluster.</span></span>
2. <span data-ttu-id="a0537-131">在頁面頂端的功能表中，選取 [Hive 編輯器]。</span><span class="sxs-lookup"><span data-stu-id="a0537-131">From the menu at the top of the page, select the **Hive Editor**.</span></span> <span data-ttu-id="a0537-132">這會顯示包含下列範例查詢的頁面。</span><span class="sxs-lookup"><span data-stu-id="a0537-132">This will display a page with the following example query.</span></span>

        Select * from hivesampletable

    <span data-ttu-id="a0537-133">清除範例查詢並取代為下列內容。</span><span class="sxs-lookup"><span data-stu-id="a0537-133">Erase the example query and replace it with the following.</span></span>

        set hive.execution.engine=tez;
        select market, state, country from hivesampletable where deviceplatform='Android' group by market, country, state;
3. <span data-ttu-id="a0537-134">選取 [提交] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="a0537-134">Select the **Submit** button.</span></span> <span data-ttu-id="a0537-135">頁面底部的 [作業工作階段] 會顯示查詢的狀態。</span><span class="sxs-lookup"><span data-stu-id="a0537-135">The **Job Session** section at the bottom of the page will display the status of the query.</span></span> <span data-ttu-id="a0537-136">當狀態變更為 [已完成] 後，請選取 [檢視詳細資料] 連結來檢視結果。</span><span class="sxs-lookup"><span data-stu-id="a0537-136">Once the status changes to **Completed**, select the **View Details** link to view the results.</span></span> <span data-ttu-id="a0537-137">[作業輸出] 應該類似如下：</span><span class="sxs-lookup"><span data-stu-id="a0537-137">The **Job Output** should be similar to the following:</span></span>

        en-GB   Hessen      Germany
        en-GB   Kingston    Jamaica
        en-GB   Nairobi Area    Kenya

## <a name="use-the-tez-ui"></a><span data-ttu-id="a0537-138">使用 Tez UI</span><span class="sxs-lookup"><span data-stu-id="a0537-138">Use the Tez UI</span></span>
> [!NOTE]
> <span data-ttu-id="a0537-139">只有從叢集前端節點的桌面上才能使用 Tez UI，因此您必須使用遠端桌面連接到前端節點。</span><span class="sxs-lookup"><span data-stu-id="a0537-139">The Tez UI is only available from the desktop of the cluster head nodes, so you must use Remote Desktop to connect to the head nodes.</span></span>
>
>

1. <span data-ttu-id="a0537-140">從 [Azure 入口網站](https://portal.azure.com)，選取您的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="a0537-140">From the [Azure portal](https://portal.azure.com), select your HDInsight cluster.</span></span> <span data-ttu-id="a0537-141">從 HDInsight 刀鋒視窗的頂端，選取 [遠端桌面] 圖示。</span><span class="sxs-lookup"><span data-stu-id="a0537-141">From the top of the HDInsight blade, select the **Remote Desktop** icon.</span></span> <span data-ttu-id="a0537-142">這會顯示遠端桌面刀鋒視窗</span><span class="sxs-lookup"><span data-stu-id="a0537-142">This will display the remote desktop blade</span></span>

    ![遠端桌面圖示](./media/hdinsight-debug-tez-ui/remotedesktopicon.png)
2. <span data-ttu-id="a0537-144">從 [遠端桌面] 刀鋒視窗中，選取 [連接] 來連線到叢集前端節點。</span><span class="sxs-lookup"><span data-stu-id="a0537-144">From the Remote Desktop blade, select **Connect** to connect to the cluster head node.</span></span> <span data-ttu-id="a0537-145">出現提示時，使用遠端桌面使用者名稱和密碼來驗證連線。</span><span class="sxs-lookup"><span data-stu-id="a0537-145">When prompted, use the cluster Remote Desktop user name and password to authenticate the connection.</span></span>

    ![遠端桌面連線圖示](./media/hdinsight-debug-tez-ui/remotedesktopconnect.png)

   > [!NOTE]
   > <span data-ttu-id="a0537-147">如果您未啟用遠端桌面連線功能，請提供使用者名稱、密碼和到期日，然後選取 [啟用] 來啟用遠端桌面。</span><span class="sxs-lookup"><span data-stu-id="a0537-147">If you have not enabled Remote Desktop connectivity, provide a user name, password, and expiration date, then select **Enable** to enable Remote Desktop.</span></span> <span data-ttu-id="a0537-148">啟用之後，請使用先前的步驟來連接。</span><span class="sxs-lookup"><span data-stu-id="a0537-148">Once it has been enabled, use the previous steps to connect.</span></span>
   >
   >
3. <span data-ttu-id="a0537-149">連線之後，請在遠端桌面開啟 Internet Explorer，選取瀏覽器右上方的齒輪圖示，然後選取 [相容性檢視設定]。</span><span class="sxs-lookup"><span data-stu-id="a0537-149">Once connected, open Internet Explorer on the remote desktop, select the gear icon in the upper right of the browser, and then select **Compatibility View Settings**.</span></span>
4. <span data-ttu-id="a0537-150">從 [相容性檢視設定] 的底部，清除 [在相容性檢視下顯示內部網路網站] 核取方塊和 [使用 Microsoft 相容性清單]，然後選取 [關閉]。</span><span class="sxs-lookup"><span data-stu-id="a0537-150">From the bottom of **Compatibility View Settings**, clear the check box for **Display intranet sites in Compatibility View** and **Use Microsoft compatibility lists**, and then select **Close**.</span></span>
5. <span data-ttu-id="a0537-151">在 Internet Explorer 中，瀏覽至 http://headnodehost:8188/tezui/#/。</span><span class="sxs-lookup"><span data-stu-id="a0537-151">In Internet Explorer, browse to http://headnodehost:8188/tezui/#/.</span></span> <span data-ttu-id="a0537-152">這會顯示 Tez UI</span><span class="sxs-lookup"><span data-stu-id="a0537-152">This will display the Tez UI</span></span>

    ![Tez UI](./media/hdinsight-debug-tez-ui/tezui.png)

    <span data-ttu-id="a0537-154">當 Tez UI 載入時，您會看到叢集上目前正在執行或已執行的一份 DAG 清單。</span><span class="sxs-lookup"><span data-stu-id="a0537-154">When the Tez UI loads, you will see a list of DAGs that are currently running, or have been ran on the cluster.</span></span> <span data-ttu-id="a0537-155">預設檢視包括 Dag 名稱、識別碼、傳送者、狀態、開始時間、結束時間、持續時間、應用程式識別碼和佇列。</span><span class="sxs-lookup"><span data-stu-id="a0537-155">The default view includes the Dag Name, Id, Submitter, Status, Start Time, End Time, Duration, Application ID, and Queue.</span></span> <span data-ttu-id="a0537-156">使用頁面右邊的齒輪圖示可以加入更多資料行。</span><span class="sxs-lookup"><span data-stu-id="a0537-156">More columns can be added using the gear icon at the right of the page.</span></span>

    <span data-ttu-id="a0537-157">如果您只有一個項目，則會是關於您在上一節執行的查詢。</span><span class="sxs-lookup"><span data-stu-id="a0537-157">If you have only one entry, it will be for the query that you ran in the previous section.</span></span> <span data-ttu-id="a0537-158">如果您有多個項目，可以在 DAG 上方的欄位中輸入搜尋準則來搜尋，然後按 **Enter**。</span><span class="sxs-lookup"><span data-stu-id="a0537-158">If you have multiple entries, you can search by entering search criteria in the fields above the DAGs, then hit **Enter**.</span></span>
6. <span data-ttu-id="a0537-159">選取最新 DAG 項目的 [Dag 名稱]。</span><span class="sxs-lookup"><span data-stu-id="a0537-159">Select the **Dag Name** for the most recent DAG entry.</span></span> <span data-ttu-id="a0537-160">這會顯示 DAG 的相關資訊，以及用來下載 JSON 壓縮檔 (包含 DAG 的相關資訊) 的選項。</span><span class="sxs-lookup"><span data-stu-id="a0537-160">This will display information about the DAG, as well as the option to download a zip of JSON files that contain information about the DAG.</span></span>

    ![DAG 詳細資料](./media/hdinsight-debug-tez-ui/dagdetails.png)
7. <span data-ttu-id="a0537-162">[DAG 詳細資料] 上方有幾個連結可用來顯示 DAG 的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="a0537-162">Above the **DAG Details** are several links that can be used to display information about the DAG.</span></span>

   * <span data-ttu-id="a0537-163">[DAG 計數器] 顯示此 DAG 的計數器資訊。</span><span class="sxs-lookup"><span data-stu-id="a0537-163">**DAG Counters** displays counters information for this DAG.</span></span>
   * <span data-ttu-id="a0537-164">[圖形檢視] 顯示此 DAG 的圖形表示。</span><span class="sxs-lookup"><span data-stu-id="a0537-164">**Graphical View** displays a graphical representation of this DAG.</span></span>
   * <span data-ttu-id="a0537-165">[所有頂點] 顯示此 DAG 中的頂點清單。</span><span class="sxs-lookup"><span data-stu-id="a0537-165">**All Vertices** displays a list of the vertices in this DAG.</span></span>
   * <span data-ttu-id="a0537-166">[所有工作] 顯示此 DAG 中所有頂點的工作清單。</span><span class="sxs-lookup"><span data-stu-id="a0537-166">**All Tasks** displays a list of the tasks for all vertices in this DAG.</span></span>
   * <span data-ttu-id="a0537-167">[所有工作嘗試] 顯示嘗試對此 DAG 執行工作的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="a0537-167">**All TaskAttempts** displays information about the attempts to run tasks for this DAG.</span></span>

     > [!NOTE]
     > <span data-ttu-id="a0537-168">如果您捲動 [頂點]、[工作] 和 [工作嘗試] 的資料行顯示，請注意有連結可以檢視每個資料列的**計數器**和**檢視或下載記錄檔**。</span><span class="sxs-lookup"><span data-stu-id="a0537-168">If you scroll the column display for Vertices, Tasks and TaskAttempts, notice that there are links to view **counters** and **view or download logs** for each row.</span></span>
     >
     >

     <span data-ttu-id="a0537-169">如果作業執行失敗，[DAG 詳細資料] 會顯示 [FAILED] 狀態，以及可前往失敗工作相關資訊的連結。</span><span class="sxs-lookup"><span data-stu-id="a0537-169">If there was a failure with the job, the DAG Details will display a status of FAILED, along with links to information about the failed task.</span></span> <span data-ttu-id="a0537-170">DAG 詳細資料下方會顯示診斷資訊。</span><span class="sxs-lookup"><span data-stu-id="a0537-170">Diagnostics information will be displayed beneath the DAG details.</span></span>
8. <span data-ttu-id="a0537-171">選取 [圖形檢視]。</span><span class="sxs-lookup"><span data-stu-id="a0537-171">Select **Graphical View**.</span></span> <span data-ttu-id="a0537-172">這會以圖形化的方式來顯示 DAG。</span><span class="sxs-lookup"><span data-stu-id="a0537-172">This displays a graphical representation of the DAG.</span></span> <span data-ttu-id="a0537-173">您可以將滑鼠游標移動到檢視中的每個頂點上，來顯示該頂點的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="a0537-173">You can place the mouse over each vertex in the view to display information about it.</span></span>

    ![圖形檢視](./media/hdinsight-debug-tez-ui/dagdiagram.png)
9. <span data-ttu-id="a0537-175">按一下頂點會載入該項目的 [頂點詳細資料] 。</span><span class="sxs-lookup"><span data-stu-id="a0537-175">Clicking on a vertex will load the **Vertex Details** for that item.</span></span> <span data-ttu-id="a0537-176">按一下 [對應 1] 頂點來顯示此項目的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="a0537-176">Click on the **Map 1** vertex to display details for this item.</span></span> <span data-ttu-id="a0537-177">選取 [確認] 來確認瀏覽。</span><span class="sxs-lookup"><span data-stu-id="a0537-177">Select **Confirm** to confirm the navigation.</span></span>

    ![頂點詳細資料](./media/hdinsight-debug-tez-ui/vertexdetails.png)
10. <span data-ttu-id="a0537-179">請注意，現在頁面頂端有與頂點和工作相關的連結。</span><span class="sxs-lookup"><span data-stu-id="a0537-179">Note that you now have links at the top of the page that are related to vertices and tasks.</span></span>

    > [!NOTE]
    > <span data-ttu-id="a0537-180">您也可以回到 [DAG 詳細資料]、選取 [頂點詳細資料]，然後選取 [對應 1] 頂點，就可進入此頁面。</span><span class="sxs-lookup"><span data-stu-id="a0537-180">You can also arrive at this page by going back to **DAG Details**, selecting **Vertex Details**, and then selecting the **Map 1** vertex.</span></span>
    >
    >

    * <span data-ttu-id="a0537-181">[頂點計數器] 顯示此頂點的計數器資訊。</span><span class="sxs-lookup"><span data-stu-id="a0537-181">**Vertex Counters** displays counter information for this vertex.</span></span>
    * <span data-ttu-id="a0537-182">[工作] 顯示此頂點的工作。</span><span class="sxs-lookup"><span data-stu-id="a0537-182">**Tasks** displays tasks for this vertex.</span></span>
    * <span data-ttu-id="a0537-183">[工作嘗試] 顯示嘗試對此頂端執行工作的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="a0537-183">**Task Attempts** displays information about attempts to run tasks for this vertex.</span></span>
    * <span data-ttu-id="a0537-184">[來源與接收] 顯示此頂點的資料來源和接收。</span><span class="sxs-lookup"><span data-stu-id="a0537-184">**Sources & Sinks** displays data sources and sinks for this vertex.</span></span>

      > [!NOTE]
      > <span data-ttu-id="a0537-185">跟前一個功能表一樣，您可以捲動 [工作]、[工作嘗試] 及 [來源與接收] 的資料行顯示，來顯示可前往每個項目詳細資訊的連結。</span><span class="sxs-lookup"><span data-stu-id="a0537-185">As with the previous menu, you can scroll the column display for Tasks, Task Attempts, and Sources & Sinks__ to display links to more information for each item.</span></span>
      >
      >
11. <span data-ttu-id="a0537-186">選取 [工作]，然後選取名為 **00_000000** 的項目。</span><span class="sxs-lookup"><span data-stu-id="a0537-186">Select **Tasks**, and then select the item named **00_000000**.</span></span> <span data-ttu-id="a0537-187">這會顯示這項工作的 [工作詳細資料]。</span><span class="sxs-lookup"><span data-stu-id="a0537-187">This will display **Task Details** for this task.</span></span> <span data-ttu-id="a0537-188">在此畫面中，您可以檢視 [工作計數器] 和 [工作嘗試]。</span><span class="sxs-lookup"><span data-stu-id="a0537-188">From this screen, you can view **Task Counters** and **Task Attempts**.</span></span>

    ![作業詳細資料](./media/hdinsight-debug-tez-ui/taskdetails.png)

## <a name="next-steps"></a><span data-ttu-id="a0537-190">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a0537-190">Next Steps</span></span>
<span data-ttu-id="a0537-191">既然您已了解如何使用 Tez 檢視，請深入了解 [在 HDInsight 上使用 Hive](hdinsight-use-hive.md)。</span><span class="sxs-lookup"><span data-stu-id="a0537-191">Now that you have learned how to use the Tez view, learn more about [Using Hive on HDInsight](hdinsight-use-hive.md).</span></span>

<span data-ttu-id="a0537-192">如需 Tez 的詳細技術資訊，請參閱 [Hortonworks 的 Tez 頁面](http://hortonworks.com/hadoop/tez/)。</span><span class="sxs-lookup"><span data-stu-id="a0537-192">For more detailed technical information on Tez, see the [Tez page at Hortonworks](http://hortonworks.com/hadoop/tez/).</span></span>
