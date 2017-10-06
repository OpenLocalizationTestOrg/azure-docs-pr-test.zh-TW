---
title: "以 Windows 為基礎的 HDInsight 的 Azure Tez UI aaaUse |Microsoft 文件"
description: "了解 toouse hello Tez UI toodebug Tez Windows 為基礎的 HDInsight HDInsight 上的工作。"
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
ms.openlocfilehash: 7ae21242ee1f8dc34a8501bed1ca995480885540
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-tez-ui-toodebug-tez-jobs-on-windows-based-hdinsight"></a><span data-ttu-id="c6aea-103">使用 Windows 為基礎的 HDInsight 上的 hello Tez UI toodebug Tez 工作</span><span class="sxs-lookup"><span data-stu-id="c6aea-103">Use hello Tez UI toodebug Tez Jobs on Windows-based HDInsight</span></span>
<span data-ttu-id="c6aea-104">hello Tez UI 是可以使用的 toounderstand 和偵錯工作 Tez 作為 hello 執行引擎在 Windows 為基礎的 HDInsight 叢集上的網頁。</span><span class="sxs-lookup"><span data-stu-id="c6aea-104">hello Tez UI is a web page that can be used toounderstand and debug jobs that use Tez as hello execution engine on Windows-based HDInsight clusters.</span></span> <span data-ttu-id="c6aea-105">hello Tez UI 允許 toovisualize hello 工作的已連接的項目圖形下鑽研至每個項目，以及擷取統計資料和記錄資訊。</span><span class="sxs-lookup"><span data-stu-id="c6aea-105">hello Tez UI allows you toovisualize hello job as a graph of connected items, drill into each item, and retrieve statistics and logging information.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c6aea-106">本文件中的 hello 步驟需要使用 Windows 的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="c6aea-106">hello steps in this document require an HDInsight cluster that uses Windows.</span></span> <span data-ttu-id="c6aea-107">Linux 為 hello 僅作業系統 HDInsight 3.4 或更新版本上使用。</span><span class="sxs-lookup"><span data-stu-id="c6aea-107">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="c6aea-108">如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。</span><span class="sxs-lookup"><span data-stu-id="c6aea-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c6aea-109">必要條件</span><span class="sxs-lookup"><span data-stu-id="c6aea-109">Prerequisites</span></span>
* <span data-ttu-id="c6aea-110">以 Windows 為基礎的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="c6aea-110">A Windows-based HDInsight cluster.</span></span> <span data-ttu-id="c6aea-111">如需建立新叢集的步驟，請參閱 [開始使用以 Windows 為基礎的 HDInsight](hdinsight-hadoop-tutorial-get-started-windows.md)。</span><span class="sxs-lookup"><span data-stu-id="c6aea-111">For steps on creating a new cluster, see [Get started using Windows-based HDInsight](hdinsight-hadoop-tutorial-get-started-windows.md).</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="c6aea-112">只有在 2016 年 2 月 8 日之後建立的 Windows 為基礎的 HDInsight 叢集上使用 hello Tez UI。</span><span class="sxs-lookup"><span data-stu-id="c6aea-112">hello Tez UI is only available on Windows-based HDInsight clusters created after February 8th, 2016.</span></span>
  >
  >
* <span data-ttu-id="c6aea-113">以 Windows 為基礎的遠端桌面用戶端。</span><span class="sxs-lookup"><span data-stu-id="c6aea-113">A Windows-based Remote Desktop client.</span></span>

## <a name="understanding-tez"></a><span data-ttu-id="c6aea-114">了解 Tez</span><span class="sxs-lookup"><span data-stu-id="c6aea-114">Understanding Tez</span></span>
<span data-ttu-id="c6aea-115">Tez 是 Hadoop 中資料處理用的可延伸架構，資料處理的速度比傳統的 MapReduce 處理方式還要快。</span><span class="sxs-lookup"><span data-stu-id="c6aea-115">Tez is an extensible framework for data processing in Hadoop that provides greater speeds than traditional MapReduce processing.</span></span> <span data-ttu-id="c6aea-116">Windows 為基礎的 HDInsight 叢集，它是選擇性的引擎，您可以使用下列命令為 Hive 查詢的一部份的 hello 啟用登錄區：</span><span class="sxs-lookup"><span data-stu-id="c6aea-116">For Windows-based HDInsight clusters, it is an optional engine that you can enable for Hive by using hello following command as part of your Hive query:</span></span>

    set hive.execution.engine=tez;

<span data-ttu-id="c6aea-117">已提交的 tooTez 工作時，它會建立導向非循環圖 (DAG) 描述 hello hello 作業所需的 hello 動作的執行順序。</span><span class="sxs-lookup"><span data-stu-id="c6aea-117">When work is submitted tooTez, it creates a Directed Acyclic Graph (DAG) that describes hello order of execution of hello actions required by hello job.</span></span> <span data-ttu-id="c6aea-118">個別的動作稱為頂點，和執行一段 hello 整體的作業。</span><span class="sxs-lookup"><span data-stu-id="c6aea-118">Individual actions are called vertices, and execute a piece of hello overall job.</span></span> <span data-ttu-id="c6aea-119">hello 實際執行的 hello 頂點所描述的工作稱為工作，並可能散佈在 hello 叢集中的多個節點。</span><span class="sxs-lookup"><span data-stu-id="c6aea-119">hello actual execution of hello work described by a vertex is called a task, and may be distributed across multiple nodes in hello cluster.</span></span>

### <a name="understanding-hello-tez-ui"></a><span data-ttu-id="c6aea-120">了解 hello Tez UI</span><span class="sxs-lookup"><span data-stu-id="c6aea-120">Understanding hello Tez UI</span></span>
<span data-ttu-id="c6aea-121">hello Tez UI 是 web 網頁會提供有關處理序正在執行，或有先前執行的使用 Tez。</span><span class="sxs-lookup"><span data-stu-id="c6aea-121">hello Tez UI is a web page provides information on processes that are running, or have previously ran using Tez.</span></span> <span data-ttu-id="c6aea-122">它可讓您 tooview hello Tez，所產生的 DAG 如何分散在叢集中，例如工作和頂點，錯誤訊息所使用的記憶體計數器。</span><span class="sxs-lookup"><span data-stu-id="c6aea-122">It allows you tooview hello DAG generated by Tez, how it is distributed across clusters, counters such as memory used by tasks and vertices, and error information.</span></span> <span data-ttu-id="c6aea-123">它可能提供有用的資訊，在下列案例的 hello:</span><span class="sxs-lookup"><span data-stu-id="c6aea-123">It may offer useful information in hello following scenarios:</span></span>

* <span data-ttu-id="c6aea-124">監視長時間執行處理程序，檢視 hello 對應的進度，並減少的工作。</span><span class="sxs-lookup"><span data-stu-id="c6aea-124">Monitoring long-running processes, viewing hello progress of map and reduce tasks.</span></span>
* <span data-ttu-id="c6aea-125">分析成功或失敗的處理序 toolearn 歷程記錄資料，處理方式可提升或失敗的原因。</span><span class="sxs-lookup"><span data-stu-id="c6aea-125">Analyzing historical data for successful or failed processes toolearn how processing could be improved or why it failed.</span></span>

## <a name="generate-a-dag"></a><span data-ttu-id="c6aea-126">產生 DAG</span><span class="sxs-lookup"><span data-stu-id="c6aea-126">Generate a DAG</span></span>
<span data-ttu-id="c6aea-127">如果工作使用 hello 的 Tez 引擎目前正在執行，或已在過去的 hello 已執行 hello Tez UI 只會包含資料。</span><span class="sxs-lookup"><span data-stu-id="c6aea-127">hello Tez UI will only contain data if a job that uses hello Tez engine is currently running, or has been ran in hello past.</span></span> <span data-ttu-id="c6aea-128">簡單的 Hive 查詢通常不用 Tez 就能解決，但更複雜的查詢 (會進行篩選、分組、排序、 聯結等) 通常需要使用 Tez。</span><span class="sxs-lookup"><span data-stu-id="c6aea-128">Simple Hive queries can usually be resolved without using Tez, however more complex queries that do filtering, grouping, ordering, joins, etc. will usually require Tez.</span></span>

<span data-ttu-id="c6aea-129">使用下列步驟 toorun Hive 查詢將會執行使用 Tez hello。</span><span class="sxs-lookup"><span data-stu-id="c6aea-129">Use hello following steps toorun a Hive query that will execute using Tez.</span></span>

1. <span data-ttu-id="c6aea-130">在 web 瀏覽器中，瀏覽 toohttps://CLUSTERNAME.azurehdinsight.net，其中**CLUSTERNAME** hello 您的 HDInsight 叢集名稱。</span><span class="sxs-lookup"><span data-stu-id="c6aea-130">In a web browser, navigate toohttps://CLUSTERNAME.azurehdinsight.net, where **CLUSTERNAME** is hello name of your HDInsight cluster.</span></span>
2. <span data-ttu-id="c6aea-131">從 hello 頁面頂端的 hello hello 功能表上，選取 hello**登錄區編輯器**。</span><span class="sxs-lookup"><span data-stu-id="c6aea-131">From hello menu at hello top of hello page, select hello **Hive Editor**.</span></span> <span data-ttu-id="c6aea-132">這會顯示頁面，以下列範例查詢中的 hello。</span><span class="sxs-lookup"><span data-stu-id="c6aea-132">This will display a page with hello following example query.</span></span>

        Select * from hivesampletable

    <span data-ttu-id="c6aea-133">清除 hello 範例查詢，並以 hello 下列取代它。</span><span class="sxs-lookup"><span data-stu-id="c6aea-133">Erase hello example query and replace it with hello following.</span></span>

        set hive.execution.engine=tez;
        select market, state, country from hivesampletable where deviceplatform='Android' group by market, country, state;
3. <span data-ttu-id="c6aea-134">選取 hello**送出** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="c6aea-134">Select hello **Submit** button.</span></span> <span data-ttu-id="c6aea-135">hello**作業工作階段**在 hello hello 頁面底部的區段會顯示 hello hello 查詢狀態。</span><span class="sxs-lookup"><span data-stu-id="c6aea-135">hello **Job Session** section at hello bottom of hello page will display hello status of hello query.</span></span> <span data-ttu-id="c6aea-136">一次太 hello 狀態變更**已完成**，選取 hello**檢視詳細資料**連結 tooview hello 結果。</span><span class="sxs-lookup"><span data-stu-id="c6aea-136">Once hello status changes too**Completed**, select hello **View Details** link tooview hello results.</span></span> <span data-ttu-id="c6aea-137">hello**作業輸出**應該類似 toohello 下列：</span><span class="sxs-lookup"><span data-stu-id="c6aea-137">hello **Job Output** should be similar toohello following:</span></span>

        en-GB   Hessen      Germany
        en-GB   Kingston    Jamaica
        en-GB   Nairobi Area    Kenya

## <a name="use-hello-tez-ui"></a><span data-ttu-id="c6aea-138">使用 hello Tez UI</span><span class="sxs-lookup"><span data-stu-id="c6aea-138">Use hello Tez UI</span></span>
> [!NOTE]
> <span data-ttu-id="c6aea-139">hello Tez UI 才可用從 hello 桌面 hello 叢集前端節點，因此您必須使用遠端桌面 tooconnect toohello 前端節點。</span><span class="sxs-lookup"><span data-stu-id="c6aea-139">hello Tez UI is only available from hello desktop of hello cluster head nodes, so you must use Remote Desktop tooconnect toohello head nodes.</span></span>
>
>

1. <span data-ttu-id="c6aea-140">從 hello [Azure 入口網站](https://portal.azure.com)，選取您的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="c6aea-140">From hello [Azure portal](https://portal.azure.com), select your HDInsight cluster.</span></span> <span data-ttu-id="c6aea-141">從 hello hello HDInsight 刀鋒視窗頂端，選取 hello**遠端桌面**圖示。</span><span class="sxs-lookup"><span data-stu-id="c6aea-141">From hello top of hello HDInsight blade, select hello **Remote Desktop** icon.</span></span> <span data-ttu-id="c6aea-142">這會顯示 hello 遠端桌面刀鋒視窗</span><span class="sxs-lookup"><span data-stu-id="c6aea-142">This will display hello remote desktop blade</span></span>

    ![遠端桌面圖示](./media/hdinsight-debug-tez-ui/remotedesktopicon.png)
2. <span data-ttu-id="c6aea-144">從 hello 遠端桌面刀鋒視窗中，選取**連接**tooconnect toohello 叢集前端節點。</span><span class="sxs-lookup"><span data-stu-id="c6aea-144">From hello Remote Desktop blade, select **Connect** tooconnect toohello cluster head node.</span></span> <span data-ttu-id="c6aea-145">出現提示時，使用 hello 叢集遠端桌面使用者名稱和密碼 tooauthenticate hello 連線。</span><span class="sxs-lookup"><span data-stu-id="c6aea-145">When prompted, use hello cluster Remote Desktop user name and password tooauthenticate hello connection.</span></span>

    ![遠端桌面連線圖示](./media/hdinsight-debug-tez-ui/remotedesktopconnect.png)

   > [!NOTE]
   > <span data-ttu-id="c6aea-147">如果您未啟用遠端桌面連線，提供使用者名稱、 密碼以及到期日，然後選取 **啟用**tooenable 遠端桌面。</span><span class="sxs-lookup"><span data-stu-id="c6aea-147">If you have not enabled Remote Desktop connectivity, provide a user name, password, and expiration date, then select **Enable** tooenable Remote Desktop.</span></span> <span data-ttu-id="c6aea-148">已啟用它，一旦使用上一個步驟 tooconnect hello。</span><span class="sxs-lookup"><span data-stu-id="c6aea-148">Once it has been enabled, use hello previous steps tooconnect.</span></span>
   >
   >
3. <span data-ttu-id="c6aea-149">一旦連接之後，在 hello 遠端桌面上，hello 右上角 hello 瀏覽器中，選取 hello 齒輪圖示開啟 Internet Explorer，然後選取**相容性檢視設定**。</span><span class="sxs-lookup"><span data-stu-id="c6aea-149">Once connected, open Internet Explorer on hello remote desktop, select hello gear icon in hello upper right of hello browser, and then select **Compatibility View Settings**.</span></span>
4. <span data-ttu-id="c6aea-150">從 hello 底部**相容性檢視設定**，清除 hello 核取方塊**在相容性檢視中顯示的內部網路網站**和**使用 Microsoft 相容性清單**，然後選取**關閉**。</span><span class="sxs-lookup"><span data-stu-id="c6aea-150">From hello bottom of **Compatibility View Settings**, clear hello check box for **Display intranet sites in Compatibility View** and **Use Microsoft compatibility lists**, and then select **Close**.</span></span>
5. <span data-ttu-id="c6aea-151">在 Internet Explorer 中，瀏覽 toohttp://headnodehost:8188/tezui / #/。</span><span class="sxs-lookup"><span data-stu-id="c6aea-151">In Internet Explorer, browse toohttp://headnodehost:8188/tezui/#/.</span></span> <span data-ttu-id="c6aea-152">這會顯示 hello Tez UI</span><span class="sxs-lookup"><span data-stu-id="c6aea-152">This will display hello Tez UI</span></span>

    ![Tez UI](./media/hdinsight-debug-tez-ui/tezui.png)

    <span data-ttu-id="c6aea-154">Hello Tez UI 載入時，您會看到一份目前正在執行，或者已被 Dag 執行 hello 叢集上。</span><span class="sxs-lookup"><span data-stu-id="c6aea-154">When hello Tez UI loads, you will see a list of DAGs that are currently running, or have been ran on hello cluster.</span></span> <span data-ttu-id="c6aea-155">hello 預設檢視包含 hello Dag 名稱、 識別碼、 傳送者、 狀態、 開始時間、 結束時間、 持續時間、 應用程式識別碼和佇列。</span><span class="sxs-lookup"><span data-stu-id="c6aea-155">hello default view includes hello Dag Name, Id, Submitter, Status, Start Time, End Time, Duration, Application ID, and Queue.</span></span> <span data-ttu-id="c6aea-156">可以在 hello hello 頁面的右邊使用 hello 齒輪圖示加入更多的資料行。</span><span class="sxs-lookup"><span data-stu-id="c6aea-156">More columns can be added using hello gear icon at hello right of hello page.</span></span>

    <span data-ttu-id="c6aea-157">如果您有只有一個項目，即是您已執行 hello 前一節中的 hello 查詢。</span><span class="sxs-lookup"><span data-stu-id="c6aea-157">If you have only one entry, it will be for hello query that you ran in hello previous section.</span></span> <span data-ttu-id="c6aea-158">如果您有多個項目，您可以搜尋 hello hello Dag，上面的欄位中輸入搜尋準則，然後叫用**Enter**。</span><span class="sxs-lookup"><span data-stu-id="c6aea-158">If you have multiple entries, you can search by entering search criteria in hello fields above hello DAGs, then hit **Enter**.</span></span>
6. <span data-ttu-id="c6aea-159">選取 hello **Dag 名稱**hello 最近 DAG 項目。</span><span class="sxs-lookup"><span data-stu-id="c6aea-159">Select hello **Dag Name** for hello most recent DAG entry.</span></span> <span data-ttu-id="c6aea-160">這會顯示 hello DAG，及 hello 選項 toodownload zip 包含 hello DAG 的相關資訊的 JSON 檔案的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="c6aea-160">This will display information about hello DAG, as well as hello option toodownload a zip of JSON files that contain information about hello DAG.</span></span>

    ![DAG 詳細資料](./media/hdinsight-debug-tez-ui/dagdetails.png)
7. <span data-ttu-id="c6aea-162">上述 hello **DAG 詳細資料**是數個可以使用的 toodisplay hello DAG 資訊的連結。</span><span class="sxs-lookup"><span data-stu-id="c6aea-162">Above hello **DAG Details** are several links that can be used toodisplay information about hello DAG.</span></span>

   * <span data-ttu-id="c6aea-163">[DAG 計數器] 顯示此 DAG 的計數器資訊。</span><span class="sxs-lookup"><span data-stu-id="c6aea-163">**DAG Counters** displays counters information for this DAG.</span></span>
   * <span data-ttu-id="c6aea-164">[圖形檢視] 顯示此 DAG 的圖形表示。</span><span class="sxs-lookup"><span data-stu-id="c6aea-164">**Graphical View** displays a graphical representation of this DAG.</span></span>
   * <span data-ttu-id="c6aea-165">**所有的頂點**顯示此 DAG 中的 hello 頂點清單。</span><span class="sxs-lookup"><span data-stu-id="c6aea-165">**All Vertices** displays a list of hello vertices in this DAG.</span></span>
   * <span data-ttu-id="c6aea-166">**所有工作**此 DAG 中顯示的所有頂點的 hello 工作清單。</span><span class="sxs-lookup"><span data-stu-id="c6aea-166">**All Tasks** displays a list of hello tasks for all vertices in this DAG.</span></span>
   * <span data-ttu-id="c6aea-167">**所有 TaskAttempts** hello 的顯示資訊的這個 DAG 嘗試 toorun 工作。</span><span class="sxs-lookup"><span data-stu-id="c6aea-167">**All TaskAttempts** displays information about hello attempts toorun tasks for this DAG.</span></span>

     > [!NOTE]
     > <span data-ttu-id="c6aea-168">當您捲動頂點、 工作和 TaskAttempts hello 資料行顯示，請注意，有連結 tooview**計數器**和**檢視或下載記錄檔**每個資料列。</span><span class="sxs-lookup"><span data-stu-id="c6aea-168">If you scroll hello column display for Vertices, Tasks and TaskAttempts, notice that there are links tooview **counters** and **view or download logs** for each row.</span></span>
     >
     >

     <span data-ttu-id="c6aea-169">如果發生與 hello 作業失敗，hello DAG 詳細資料會顯示失敗狀態以及連結 tooinformation hello 失敗的工作有關。</span><span class="sxs-lookup"><span data-stu-id="c6aea-169">If there was a failure with hello job, hello DAG Details will display a status of FAILED, along with links tooinformation about hello failed task.</span></span> <span data-ttu-id="c6aea-170">下方 hello DAG 詳細資料，將會顯示診斷資訊。</span><span class="sxs-lookup"><span data-stu-id="c6aea-170">Diagnostics information will be displayed beneath hello DAG details.</span></span>
8. <span data-ttu-id="c6aea-171">選取 [圖形檢視]。</span><span class="sxs-lookup"><span data-stu-id="c6aea-171">Select **Graphical View**.</span></span> <span data-ttu-id="c6aea-172">這會顯示 hello DAG 的圖形表示法。</span><span class="sxs-lookup"><span data-stu-id="c6aea-172">This displays a graphical representation of hello DAG.</span></span> <span data-ttu-id="c6aea-173">您可以透過在 hello 檢視 toodisplay 資訊中的每個頂點放置 hello 滑鼠。</span><span class="sxs-lookup"><span data-stu-id="c6aea-173">You can place hello mouse over each vertex in hello view toodisplay information about it.</span></span>

    ![圖形檢視](./media/hdinsight-debug-tez-ui/dagdiagram.png)
9. <span data-ttu-id="c6aea-175">按一下 上一個頂點會載入 hello**端點詳細資料**該項目。</span><span class="sxs-lookup"><span data-stu-id="c6aea-175">Clicking on a vertex will load hello **Vertex Details** for that item.</span></span> <span data-ttu-id="c6aea-176">按一下 hello**對應 1**頂點 toodisplay 詳細資料，此項目。</span><span class="sxs-lookup"><span data-stu-id="c6aea-176">Click on hello **Map 1** vertex toodisplay details for this item.</span></span> <span data-ttu-id="c6aea-177">選取**確認**tooconfirm hello 瀏覽。</span><span class="sxs-lookup"><span data-stu-id="c6aea-177">Select **Confirm** tooconfirm hello navigation.</span></span>

    ![頂點詳細資料](./media/hdinsight-debug-tez-ui/vertexdetails.png)
10. <span data-ttu-id="c6aea-179">請注意現在有 hello 頁面頂端的 hello 相關的 toovertices 和工作的連結。</span><span class="sxs-lookup"><span data-stu-id="c6aea-179">Note that you now have links at hello top of hello page that are related toovertices and tasks.</span></span>

    > [!NOTE]
    > <span data-ttu-id="c6aea-180">您可以也到達此頁面移回太**DAG 詳細資料**、 選取**端點詳細資料**，然後選取 hello**對應 1**頂點。</span><span class="sxs-lookup"><span data-stu-id="c6aea-180">You can also arrive at this page by going back too**DAG Details**, selecting **Vertex Details**, and then selecting hello **Map 1** vertex.</span></span>
    >
    >

    * <span data-ttu-id="c6aea-181">[頂點計數器] 顯示此頂點的計數器資訊。</span><span class="sxs-lookup"><span data-stu-id="c6aea-181">**Vertex Counters** displays counter information for this vertex.</span></span>
    * <span data-ttu-id="c6aea-182">[工作] 顯示此頂點的工作。</span><span class="sxs-lookup"><span data-stu-id="c6aea-182">**Tasks** displays tasks for this vertex.</span></span>
    * <span data-ttu-id="c6aea-183">**工作嘗試**顯示此頂點嘗試 toorun 工作的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="c6aea-183">**Task Attempts** displays information about attempts toorun tasks for this vertex.</span></span>
    * <span data-ttu-id="c6aea-184">[來源與接收] 顯示此頂點的資料來源和接收。</span><span class="sxs-lookup"><span data-stu-id="c6aea-184">**Sources & Sinks** displays data sources and sinks for this vertex.</span></span>

      > [!NOTE]
      > <span data-ttu-id="c6aea-185">當與 hello 上一個功能表，您可以捲動 hello 資料行顯示的工作時，工作嘗試，以及來源和 Sinks__ toodisplay 連結 toomore 資訊每個項目。</span><span class="sxs-lookup"><span data-stu-id="c6aea-185">As with hello previous menu, you can scroll hello column display for Tasks, Task Attempts, and Sources & Sinks__ toodisplay links toomore information for each item.</span></span>
      >
      >
11. <span data-ttu-id="c6aea-186">選取**工作**，接著選取 hello 項目是具名**00_000000**。</span><span class="sxs-lookup"><span data-stu-id="c6aea-186">Select **Tasks**, and then select hello item named **00_000000**.</span></span> <span data-ttu-id="c6aea-187">這會顯示這項工作的 [工作詳細資料]。</span><span class="sxs-lookup"><span data-stu-id="c6aea-187">This will display **Task Details** for this task.</span></span> <span data-ttu-id="c6aea-188">在此畫面中，您可以檢視 [工作計數器] 和 [工作嘗試]。</span><span class="sxs-lookup"><span data-stu-id="c6aea-188">From this screen, you can view **Task Counters** and **Task Attempts**.</span></span>

    ![作業詳細資料](./media/hdinsight-debug-tez-ui/taskdetails.png)

## <a name="next-steps"></a><span data-ttu-id="c6aea-190">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c6aea-190">Next Steps</span></span>
<span data-ttu-id="c6aea-191">既然您已經學會如何 toouse hello Tez 檢視，深入了解[HDInsight 上使用 Hive](hdinsight-use-hive.md)。</span><span class="sxs-lookup"><span data-stu-id="c6aea-191">Now that you have learned how toouse hello Tez view, learn more about [Using Hive on HDInsight](hdinsight-use-hive.md).</span></span>

<span data-ttu-id="c6aea-192">如需詳細 Tez 上的技術資訊，請參閱 hello [Hortonworks Tez 頁面](http://hortonworks.com/hadoop/tez/)。</span><span class="sxs-lookup"><span data-stu-id="c6aea-192">For more detailed technical information on Tez, see hello [Tez page at Hortonworks](http://hortonworks.com/hadoop/tez/).</span></span>
