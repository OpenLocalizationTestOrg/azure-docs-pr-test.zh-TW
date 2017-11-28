---
title: "使用 Microsoft Flow 的 aaaAutomate Azure Log Analytics 處理"
description: "了解如何使用 Microsoft Flow tooquickly 使用 hello Azure Log Analytics 連接器來自動化重複程序。"
services: log-analytics
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: log-analytics
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: bwren
ms.openlocfilehash: 52026df968682842cc9f8d55f6f9875c5f9c10b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="automate-log-analytics-processes-with-hello-connector-for-microsoft-flow"></a><span data-ttu-id="640f8-103">Microsoft flow 自動化與 hello 連接器的記錄分析程序</span><span class="sxs-lookup"><span data-stu-id="640f8-103">Automate Log Analytics processes with hello connector for Microsoft Flow</span></span>
<span data-ttu-id="640f8-104">[Microsoft Flow](https://ms.flow.microsoft.com)可讓您使用的各種服務數百個動作的 toocreate 自動化工作流程。</span><span class="sxs-lookup"><span data-stu-id="640f8-104">[Microsoft Flow](https://ms.flow.microsoft.com) allows you toocreate automated workflows using hundreds of actions for a variety of services.</span></span> <span data-ttu-id="640f8-105">從一個動作的輸出可以用作 toocreate 不同的服務之間的整合可讓您輸入 tooanother。</span><span class="sxs-lookup"><span data-stu-id="640f8-105">Output from one action can be used as input tooanother allowing you toocreate integration between different services.</span></span>  <span data-ttu-id="640f8-106">Microsoft flow hello Azure Log Analytics 連接器可讓您 toobuild 工作流程包含在記錄分析記錄搜尋所擷取的資料。</span><span class="sxs-lookup"><span data-stu-id="640f8-106">hello Azure Log Analytics connector for Microsoft Flow allow you toobuild workflows that include data retrieved by log searches in Log Analytics.</span></span>

<span data-ttu-id="640f8-107">比方說，您可以從 Office 365 電子郵件通知中使用 Microsoft Flow toouse 記錄分析資料、 在 Visual Studio Team Services 中建立 bug 或張貼 Slack 的訊息。</span><span class="sxs-lookup"><span data-stu-id="640f8-107">For example, you can use Microsoft Flow toouse Log Analytics data in an email notification from Office 365, create a bug in Visual Studio Team Services, or post a Slack message.</span></span>  <span data-ttu-id="640f8-108">您可以使用簡易排程或從連接的服務中的某個動作觸發工作流程，例如收到郵件或推文時。</span><span class="sxs-lookup"><span data-stu-id="640f8-108">You can trigger a workflow by a simple schedule or from some action in a connected service such as when a mail or a tweet is received.</span></span>  


> [!NOTE]
> <span data-ttu-id="640f8-109">Microsoft flow hello Azure Log Analytics 連接器需要您工作區升級 toobe toohello 新記錄分析查詢語言。</span><span class="sxs-lookup"><span data-stu-id="640f8-109">hello Azure Log Analytics connector for Microsoft Flow requires your workspace toobe upgraded toohello new Log Analytics query language.</span></span> <span data-ttu-id="640f8-110">您可以深入了解 hello 新語言，並取得 hello 程序 tooupgrade 在工作區[升級您的 Azure 記錄分析工作區 toonew 記錄搜尋](log-analytics-log-search-upgrade.md)。</span><span class="sxs-lookup"><span data-stu-id="640f8-110">You can learn more about hello new language and get hello procedure tooupgrade your workspace at [Upgrade your Azure Log Analytics workspace toonew log search](log-analytics-log-search-upgrade.md).</span></span>  

<span data-ttu-id="640f8-111">本文章中的 hello 教學課程會示範如何 toocreate 流程，會自動傳送 hello 透過電子郵件、 一個範例，告訴您可以使用 Microsoft Flow 的記錄分析的記錄分析記錄搜尋結果。</span><span class="sxs-lookup"><span data-stu-id="640f8-111">hello tutorial in this article shows you how toocreate a flow that automatically sends hello results of a Log Analytics log search by email, just one example of how you can use Log Analytics in Microsoft Flow.</span></span> 


## <a name="step-1-create-a-flow"></a><span data-ttu-id="640f8-112">步驟 1：建立流程</span><span class="sxs-lookup"><span data-stu-id="640f8-112">Step 1: Create a flow</span></span>
1. <span data-ttu-id="640f8-113">登入太[Microsoft Flow](http://flow.microsoft.com)，然後選取**我流動**。</span><span class="sxs-lookup"><span data-stu-id="640f8-113">Sign in too[Microsoft Flow](http://flow.microsoft.com), and select **My Flows**.</span></span>
2. <span data-ttu-id="640f8-114">按一下 [+ 從空白建立]。</span><span class="sxs-lookup"><span data-stu-id="640f8-114">Click **+ Create from blank**.</span></span>

## <a name="step-2-create-a-trigger-for-your-flow"></a><span data-ttu-id="640f8-115">步驟 2：建立流程的觸發程序</span><span class="sxs-lookup"><span data-stu-id="640f8-115">Step 2: Create a trigger for your flow</span></span>
1. <span data-ttu-id="640f8-116">按一下 [Search hundreds of connectors and triggers] \(搜尋數以百計的連接器和觸發程序) 。</span><span class="sxs-lookup"><span data-stu-id="640f8-116">Click **Search hundreds of connectors and triggers**.</span></span>
2. <span data-ttu-id="640f8-117">型別**排程**hello [搜尋] 方塊中。</span><span class="sxs-lookup"><span data-stu-id="640f8-117">Type **Schedule** in hello search box.</span></span>
3. <span data-ttu-id="640f8-118">依序選取 [排程] 和 [排程 - 重複]。</span><span class="sxs-lookup"><span data-stu-id="640f8-118">Select **Schedule**, and then select **Schedule - Recurrence**.</span></span>
4. <span data-ttu-id="640f8-119">在 hello**頻率**中，選取**天**在 hello**間隔**方塊中，輸入**1**。</span><span class="sxs-lookup"><span data-stu-id="640f8-119">In hello **Frequency** box select **Day** and in hello **Interval** box, enter **1**.</span></span><br><br><span data-ttu-id="640f8-120">![Microsoft Flow 觸發程序對話方塊](media/log-analytics-flow-tutorial/flow01.png)</span><span class="sxs-lookup"><span data-stu-id="640f8-120">![Microsoft Flow trigger dialog box](media/log-analytics-flow-tutorial/flow01.png)</span></span>


## <a name="step-3-add-a-log-analytics-action"></a><span data-ttu-id="640f8-121">步驟 3：新增 Log Analytics 動作</span><span class="sxs-lookup"><span data-stu-id="640f8-121">Step 3: Add a Log Analytics action</span></span>
1. <span data-ttu-id="640f8-122">按一下 + 新增步驟，然後按一下新增動作。</span><span class="sxs-lookup"><span data-stu-id="640f8-122">Click **+ New step**, and then click **Add an action**.</span></span>
2. <span data-ttu-id="640f8-123">搜尋 **Log Analytics**。</span><span class="sxs-lookup"><span data-stu-id="640f8-123">Search for **Log Analytics**.</span></span>
3. <span data-ttu-id="640f8-124">按一下 [Azure Log Analytics – Run query and visualize results] \(Azure Log Analytics – 執行查詢，並將結果視覺化) 。</span><span class="sxs-lookup"><span data-stu-id="640f8-124">Click **Azure Log Analytics – Run query and visualize results**.</span></span><br><br><span data-ttu-id="640f8-125">![Log Analytics 執行查詢視窗](media/log-analytics-flow-tutorial/flow02.png)</span><span class="sxs-lookup"><span data-stu-id="640f8-125">![Log Analytics run query window](media/log-analytics-flow-tutorial/flow02.png)</span></span>

## <a name="step-4-configure-hello-log-analytics-action"></a><span data-ttu-id="640f8-126">步驟 4： 設定 hello 記錄分析動作</span><span class="sxs-lookup"><span data-stu-id="640f8-126">Step 4: Configure hello Log Analytics action</span></span>

1. <span data-ttu-id="640f8-127">指定您包括 hello 訂用帳戶 ID、 資源群組和工作區名稱的工作區的 hello 詳細資料。</span><span class="sxs-lookup"><span data-stu-id="640f8-127">Specify hello details for your workspace including hello Subscription ID, Resource Group, and Workspace Name.</span></span>
2. <span data-ttu-id="640f8-128">新增下列記錄分析查詢 toohello hello**查詢**視窗。</span><span class="sxs-lookup"><span data-stu-id="640f8-128">Add hello following Log Analytics query toohello **Query** window.</span></span>  <span data-ttu-id="640f8-129">這只是範例查詢，您可以使用任何其他可傳回資料的查詢取代。</span><span class="sxs-lookup"><span data-stu-id="640f8-129">This is only a sample query, and you can replace with any other that returns data.</span></span>
```
    Event
    | where EventLevelName == "Error" 
    | where TimeGenerated > ago(1day)
    | summarize count() by Computer
    | sort by Computerindow. 
```

2. <span data-ttu-id="640f8-130">選取**HTML 表格**hello**圖表類型**。</span><span class="sxs-lookup"><span data-stu-id="640f8-130">Select **HTML Table** for hello **Chart Type**.</span></span><br><br><span data-ttu-id="640f8-131">![Log Analytics 動作](media/log-analytics-flow-tutorial/flow03.png)</span><span class="sxs-lookup"><span data-stu-id="640f8-131">![Log Analytics action](media/log-analytics-flow-tutorial/flow03.png)</span></span>

## <a name="step-5-configure-hello-flow-toosend-email"></a><span data-ttu-id="640f8-132">步驟 5： 設定 hello 流程 toosend 電子郵件</span><span class="sxs-lookup"><span data-stu-id="640f8-132">Step 5: Configure hello flow toosend email</span></span>

1. <span data-ttu-id="640f8-133">按一下 新增步驟，然後按一下+ 新增動作。</span><span class="sxs-lookup"><span data-stu-id="640f8-133">Click **New step**, and then click **+ Add an action**.</span></span>
2. <span data-ttu-id="640f8-134">搜尋 **Office 365 Outlook**。</span><span class="sxs-lookup"><span data-stu-id="640f8-134">Search for **Office 365 Outlook**.</span></span>
3. <span data-ttu-id="640f8-135">按一下 [Office 365 Outlook – 傳送電子郵件]。</span><span class="sxs-lookup"><span data-stu-id="640f8-135">Click **Office 365 Outlook – Send an email**.</span></span><br><br><span data-ttu-id="640f8-136">![Office 365 Outlook 選取視窗](media/log-analytics-flow-tutorial/flow04.png)</span><span class="sxs-lookup"><span data-stu-id="640f8-136">![Office 365 Outlook selection window](media/log-analytics-flow-tutorial/flow04.png)</span></span>

4. <span data-ttu-id="640f8-137">指定在 hello hello 收件者的電子郵件地址**至**視窗，並在 hello 電子郵件的主旨**主旨**。</span><span class="sxs-lookup"><span data-stu-id="640f8-137">Specify hello email address of a recipient in hello **To** window and a subject for hello email in **Subject**.</span></span>
5. <span data-ttu-id="640f8-138">按一下任何位置中的 hello**主體**方塊。</span><span class="sxs-lookup"><span data-stu-id="640f8-138">Click anywhere in hello **Body** box.</span></span>  <span data-ttu-id="640f8-139">隨即開啟 [動態內容] 視窗，並具有來自先前動作的值。</span><span class="sxs-lookup"><span data-stu-id="640f8-139">A **Dynamic content** window opens with values from previous actions.</span></span>  
6. <span data-ttu-id="640f8-140">選取 [內文]。</span><span class="sxs-lookup"><span data-stu-id="640f8-140">Select **Body**.</span></span>  <span data-ttu-id="640f8-141">這是 hello hello 記錄分析動作中的 hello 查詢的結果。</span><span class="sxs-lookup"><span data-stu-id="640f8-141">This is hello results of hello query in hello Log Analytics action.</span></span>
6. <span data-ttu-id="640f8-142">按一下 [顯示進階選項]。</span><span class="sxs-lookup"><span data-stu-id="640f8-142">Click **Show advanced options**.</span></span>
7. <span data-ttu-id="640f8-143">在 hello**是 HTML**方塊中，選取**是**。</span><span class="sxs-lookup"><span data-stu-id="640f8-143">In hello **Is HTML** box, select **Yes**.</span></span><br><br><span data-ttu-id="640f8-144">![Office 365 電子郵件設定畫面](media/log-analytics-flow-tutorial/flow05.png)</span><span class="sxs-lookup"><span data-stu-id="640f8-144">![Office 365 email configuration window](media/log-analytics-flow-tutorial/flow05.png)</span></span>

## <a name="step-6-save-and-test-your-flow"></a><span data-ttu-id="640f8-145">步驟 6：儲存並測試流程</span><span class="sxs-lookup"><span data-stu-id="640f8-145">Step 6: Save and test your flow</span></span>
1. <span data-ttu-id="640f8-146">在 hello**流程名稱**方塊中，加入您的流程的名稱，然後按一下**建立流程**。</span><span class="sxs-lookup"><span data-stu-id="640f8-146">In hello **Flow name** box, add a name for your flow, and then click **Create flow**.</span></span><br><br><span data-ttu-id="640f8-147">![儲存流程](media/log-analytics-flow-tutorial/flow06.png)</span><span class="sxs-lookup"><span data-stu-id="640f8-147">![Save flow](media/log-analytics-flow-tutorial/flow06.png)</span></span>
2. <span data-ttu-id="640f8-148">hello 流程現在所建立，而且這是您指定的 hello 排程一天後會執行。</span><span class="sxs-lookup"><span data-stu-id="640f8-148">hello flow is now created and will run after a day which is hello schedule you specified.</span></span> 
3. <span data-ttu-id="640f8-149">tooimmediately 測試 hello 流程中，按一下 **立即執行**然後**執行流程**。</span><span class="sxs-lookup"><span data-stu-id="640f8-149">tooimmediately test hello flow, click **Run Now** and then **Run flow**.</span></span><br><br><span data-ttu-id="640f8-150">![執行流程](media/log-analytics-flow-tutorial/flow07.png)</span><span class="sxs-lookup"><span data-stu-id="640f8-150">![Run flow](media/log-analytics-flow-tutorial/flow07.png)</span></span>
3. <span data-ttu-id="640f8-151">Hello 流程完成時，請檢查 hello hello 收件者所指定的郵件。</span><span class="sxs-lookup"><span data-stu-id="640f8-151">When hello flow completes, check hello mail of hello recipient that you specified.</span></span>  <span data-ttu-id="640f8-152">您應該會收到郵件本文類似 toohello 下列：</span><span class="sxs-lookup"><span data-stu-id="640f8-152">You should have received a mail with a body similar toohello following:</span></span><br><br>![範例電子郵件](media/log-analytics-flow-tutorial/flow08.png)


## <a name="next-steps"></a><span data-ttu-id="640f8-154">後續步驟</span><span class="sxs-lookup"><span data-stu-id="640f8-154">Next steps</span></span>

- <span data-ttu-id="640f8-155">深入了解 [Log Analytics 中的記錄搜尋](log-analytics-log-search-new.md)。</span><span class="sxs-lookup"><span data-stu-id="640f8-155">Learn more about [log searches in Log Analytics](log-analytics-log-search-new.md).</span></span>
- <span data-ttu-id="640f8-156">深入了解 [Microsoft Flow](https://ms.flow.microsoft.com)。</span><span class="sxs-lookup"><span data-stu-id="640f8-156">Learn more about [Microsoft Flow](https://ms.flow.microsoft.com).</span></span>



