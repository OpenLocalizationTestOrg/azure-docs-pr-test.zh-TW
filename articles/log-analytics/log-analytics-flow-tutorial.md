---
title: "使用 Microsoft Flow 自動化 Azure Log Analytics 流程"
description: "了解如何利用 Azure Log Analytics Connector，使用 Microsoft Flow 來快速自動化可重複的程序。"
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
ms.openlocfilehash: 4955f90de06cd720d78c5bb60c0adcd7dc633245
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="automate-log-analytics-processes-with-the-connector-for-microsoft-flow"></a><span data-ttu-id="63010-103">使用適用於 Microsoft Flow 的連接器自動化 Log Analytics 程序</span><span class="sxs-lookup"><span data-stu-id="63010-103">Automate Log Analytics processes with the connector for Microsoft Flow</span></span>
<span data-ttu-id="63010-104">[Microsoft Flow](https://ms.flow.microsoft.com) 可讓您使用數百個動作建立各種不同服務的自動化工作流程。</span><span class="sxs-lookup"><span data-stu-id="63010-104">[Microsoft Flow](https://ms.flow.microsoft.com) allows you to create automated workflows using hundreds of actions for a variety of services.</span></span> <span data-ttu-id="63010-105">從一個動作的輸出可用來作為另一個動作的輸入，讓您建立不同服務之間的整合。</span><span class="sxs-lookup"><span data-stu-id="63010-105">Output from one action can be used as input to another allowing you to create integration between different services.</span></span>  <span data-ttu-id="63010-106">適用於 Microsoft Flow 的 Azure Log Analytics 連接器可讓您建立工作流程，包含 Log Analytics 記錄搜尋所擷取的資料。</span><span class="sxs-lookup"><span data-stu-id="63010-106">The Azure Log Analytics connector for Microsoft Flow allow you to build workflows that include data retrieved by log searches in Log Analytics.</span></span>

<span data-ttu-id="63010-107">例如，您可以使用 Microsoft Flow，從 Office 365 在電子郵件通知中使用 Log Analytics 資料、在 Visual Studio Team Services 中建立 Bug 或張貼 Slack 訊息。</span><span class="sxs-lookup"><span data-stu-id="63010-107">For example, you can use Microsoft Flow to use Log Analytics data in an email notification from Office 365, create a bug in Visual Studio Team Services, or post a Slack message.</span></span>  <span data-ttu-id="63010-108">您可以使用簡易排程或從連接的服務中的某個動作觸發工作流程，例如收到郵件或推文時。</span><span class="sxs-lookup"><span data-stu-id="63010-108">You can trigger a workflow by a simple schedule or from some action in a connected service such as when a mail or a tweet is received.</span></span>  


> [!NOTE]
> <span data-ttu-id="63010-109">適用於 Microsoft Flow 的 Azure Log Analytics 連接器需要您的工作區升級為新的 Log Analytics 查詢語言。</span><span class="sxs-lookup"><span data-stu-id="63010-109">The Azure Log Analytics connector for Microsoft Flow requires your workspace to be upgraded to the new Log Analytics query language.</span></span> <span data-ttu-id="63010-110">您可以在[將 Azure Log Analytics 工作區升級為新的記錄搜尋](log-analytics-log-search-upgrade.md)中，深入了解新的語言，並且取得升級工作區的程序。</span><span class="sxs-lookup"><span data-stu-id="63010-110">You can learn more about the new language and get the procedure to upgrade your workspace at [Upgrade your Azure Log Analytics workspace to new log search](log-analytics-log-search-upgrade.md).</span></span>  

<span data-ttu-id="63010-111">這篇文章中的教學課程會示範如何建立流程，自動透過電子郵件傳送 Log Analytics 記錄搜尋結果，這只是如何在 Microsoft Flow 中使用 Log Analytics 的一個範例。</span><span class="sxs-lookup"><span data-stu-id="63010-111">The tutorial in this article shows you how to create a flow that automatically sends the results of a Log Analytics log search by email, just one example of how you can use Log Analytics in Microsoft Flow.</span></span> 


## <a name="step-1-create-a-flow"></a><span data-ttu-id="63010-112">步驟 1：建立流程</span><span class="sxs-lookup"><span data-stu-id="63010-112">Step 1: Create a flow</span></span>
1. <span data-ttu-id="63010-113">登入 [Microsoft Flow](http://flow.microsoft.com)，然後選取 [我的流程]。</span><span class="sxs-lookup"><span data-stu-id="63010-113">Sign in to [Microsoft Flow](http://flow.microsoft.com), and select **My Flows**.</span></span>
2. <span data-ttu-id="63010-114">按一下 [+ 從空白建立]。</span><span class="sxs-lookup"><span data-stu-id="63010-114">Click **+ Create from blank**.</span></span>

## <a name="step-2-create-a-trigger-for-your-flow"></a><span data-ttu-id="63010-115">步驟 2：建立流程的觸發程序</span><span class="sxs-lookup"><span data-stu-id="63010-115">Step 2: Create a trigger for your flow</span></span>
1. <span data-ttu-id="63010-116">按一下 [Search hundreds of connectors and triggers] (搜尋數以百計的連接器和觸發程序)。</span><span class="sxs-lookup"><span data-stu-id="63010-116">Click **Search hundreds of connectors and triggers**.</span></span>
2. <span data-ttu-id="63010-117">在搜尋方塊中鍵入**排程**。</span><span class="sxs-lookup"><span data-stu-id="63010-117">Type **Schedule** in the search box.</span></span>
3. <span data-ttu-id="63010-118">依序選取 [排程] 和 [排程 - 重複]。</span><span class="sxs-lookup"><span data-stu-id="63010-118">Select **Schedule**, and then select **Schedule - Recurrence**.</span></span>
4. <span data-ttu-id="63010-119">在 [頻率] 方塊中選取 [天]，然後在 [間隔] 方塊中輸入 **1**。</span><span class="sxs-lookup"><span data-stu-id="63010-119">In the **Frequency** box select **Day** and in the **Interval** box, enter **1**.</span></span><br><br><span data-ttu-id="63010-120">![Microsoft Flow 觸發程序對話方塊](media/log-analytics-flow-tutorial/flow01.png)</span><span class="sxs-lookup"><span data-stu-id="63010-120">![Microsoft Flow trigger dialog box](media/log-analytics-flow-tutorial/flow01.png)</span></span>


## <a name="step-3-add-a-log-analytics-action"></a><span data-ttu-id="63010-121">步驟 3：新增 Log Analytics 動作</span><span class="sxs-lookup"><span data-stu-id="63010-121">Step 3: Add a Log Analytics action</span></span>
1. <span data-ttu-id="63010-122">按一下 [+ 新增步驟]，然後按一下 [新增動作]。</span><span class="sxs-lookup"><span data-stu-id="63010-122">Click **+ New step**, and then click **Add an action**.</span></span>
2. <span data-ttu-id="63010-123">搜尋 **Log Analytics**。</span><span class="sxs-lookup"><span data-stu-id="63010-123">Search for **Log Analytics**.</span></span>
3. <span data-ttu-id="63010-124">按一下 [Azure Log Analytics – Run query and visualize results] \(Azure Log Analytics – 執行查詢，並將結果視覺化) 。</span><span class="sxs-lookup"><span data-stu-id="63010-124">Click **Azure Log Analytics – Run query and visualize results**.</span></span><br><br><span data-ttu-id="63010-125">![Log Analytics 執行查詢視窗](media/log-analytics-flow-tutorial/flow02.png)</span><span class="sxs-lookup"><span data-stu-id="63010-125">![Log Analytics run query window](media/log-analytics-flow-tutorial/flow02.png)</span></span>

## <a name="step-4-configure-the-log-analytics-action"></a><span data-ttu-id="63010-126">步驟 4：設定 Log Analytics 動作</span><span class="sxs-lookup"><span data-stu-id="63010-126">Step 4: Configure the Log Analytics action</span></span>

1. <span data-ttu-id="63010-127">指定工作區的詳細資料，包括訂用帳戶識別碼、資源群組和工作區名稱。</span><span class="sxs-lookup"><span data-stu-id="63010-127">Specify the details for your workspace including the Subscription ID, Resource Group, and Workspace Name.</span></span>
2. <span data-ttu-id="63010-128">在 [查詢] 視窗新增下列 Log Analytics 查詢。</span><span class="sxs-lookup"><span data-stu-id="63010-128">Add the following Log Analytics query to the **Query** window.</span></span>  <span data-ttu-id="63010-129">這只是範例查詢，您可以使用任何其他可傳回資料的查詢取代。</span><span class="sxs-lookup"><span data-stu-id="63010-129">This is only a sample query, and you can replace with any other that returns data.</span></span>
```
    Event
    | where EventLevelName == "Error" 
    | where TimeGenerated > ago(1day)
    | summarize count() by Computer
    | sort by Computerindow. 
```

2. <span data-ttu-id="63010-130">針對 [圖表類型] 選取 [HTML 表格]。</span><span class="sxs-lookup"><span data-stu-id="63010-130">Select **HTML Table** for the **Chart Type**.</span></span><br><br><span data-ttu-id="63010-131">![Log Analytics 動作](media/log-analytics-flow-tutorial/flow03.png)</span><span class="sxs-lookup"><span data-stu-id="63010-131">![Log Analytics action](media/log-analytics-flow-tutorial/flow03.png)</span></span>

## <a name="step-5-configure-the-flow-to-send-email"></a><span data-ttu-id="63010-132">步驟 5：設定傳送電子郵件的流程</span><span class="sxs-lookup"><span data-stu-id="63010-132">Step 5: Configure the flow to send email</span></span>

1. <span data-ttu-id="63010-133">按一下 [新增步驟]，然後按一下 [+ 新增動作]。</span><span class="sxs-lookup"><span data-stu-id="63010-133">Click **New step**, and then click **+ Add an action**.</span></span>
2. <span data-ttu-id="63010-134">搜尋 **Office 365 Outlook**。</span><span class="sxs-lookup"><span data-stu-id="63010-134">Search for **Office 365 Outlook**.</span></span>
3. <span data-ttu-id="63010-135">按一下 [Office 365 Outlook – 傳送電子郵件]。</span><span class="sxs-lookup"><span data-stu-id="63010-135">Click **Office 365 Outlook – Send an email**.</span></span><br><br><span data-ttu-id="63010-136">![Office 365 Outlook 選取視窗](media/log-analytics-flow-tutorial/flow04.png)</span><span class="sxs-lookup"><span data-stu-id="63010-136">![Office 365 Outlook selection window](media/log-analytics-flow-tutorial/flow04.png)</span></span>

4. <span data-ttu-id="63010-137">在 [收件者] 視窗中指定收件者的電子郵件地址，並在 [主旨] 指定電子郵件的主旨。</span><span class="sxs-lookup"><span data-stu-id="63010-137">Specify the email address of a recipient in the **To** window and a subject for the email in **Subject**.</span></span>
5. <span data-ttu-id="63010-138">在 [內文] 方塊的任何地方按一下。</span><span class="sxs-lookup"><span data-stu-id="63010-138">Click anywhere in the **Body** box.</span></span>  <span data-ttu-id="63010-139">隨即開啟 [動態內容] 視窗，並具有來自先前動作的值。</span><span class="sxs-lookup"><span data-stu-id="63010-139">A **Dynamic content** window opens with values from previous actions.</span></span>  
6. <span data-ttu-id="63010-140">選取 [內文]。</span><span class="sxs-lookup"><span data-stu-id="63010-140">Select **Body**.</span></span>  <span data-ttu-id="63010-141">這是 Log Analytics 動作中的查詢結果。</span><span class="sxs-lookup"><span data-stu-id="63010-141">This is the results of the query in the Log Analytics action.</span></span>
6. <span data-ttu-id="63010-142">按一下 [顯示進階選項]。</span><span class="sxs-lookup"><span data-stu-id="63010-142">Click **Show advanced options**.</span></span>
7. <span data-ttu-id="63010-143">在 [為 HTML] 方塊中選取 [是]。</span><span class="sxs-lookup"><span data-stu-id="63010-143">In the **Is HTML** box, select **Yes**.</span></span><br><br><span data-ttu-id="63010-144">![Office 365 電子郵件設定畫面](media/log-analytics-flow-tutorial/flow05.png)</span><span class="sxs-lookup"><span data-stu-id="63010-144">![Office 365 email configuration window](media/log-analytics-flow-tutorial/flow05.png)</span></span>

## <a name="step-6-save-and-test-your-flow"></a><span data-ttu-id="63010-145">步驟 6：儲存並測試流程</span><span class="sxs-lookup"><span data-stu-id="63010-145">Step 6: Save and test your flow</span></span>
1. <span data-ttu-id="63010-146">在 [流程名稱] 方塊中，新增您的流程名稱，然後按一下 [建立流程]。</span><span class="sxs-lookup"><span data-stu-id="63010-146">In the **Flow name** box, add a name for your flow, and then click **Create flow**.</span></span><br><br><span data-ttu-id="63010-147">![儲存流程](media/log-analytics-flow-tutorial/flow06.png)</span><span class="sxs-lookup"><span data-stu-id="63010-147">![Save flow](media/log-analytics-flow-tutorial/flow06.png)</span></span>
2. <span data-ttu-id="63010-148">現在已建立流程，並且會在一天之後，也就是您指定的排程時執行。</span><span class="sxs-lookup"><span data-stu-id="63010-148">The flow is now created and will run after a day which is the schedule you specified.</span></span> 
3. <span data-ttu-id="63010-149">若要立即測試流程，請依序按一下 [立即執行]、[執行流程]。</span><span class="sxs-lookup"><span data-stu-id="63010-149">To immediately test the flow, click **Run Now** and then **Run flow**.</span></span><br><br><span data-ttu-id="63010-150">![執行流程](media/log-analytics-flow-tutorial/flow07.png)</span><span class="sxs-lookup"><span data-stu-id="63010-150">![Run flow](media/log-analytics-flow-tutorial/flow07.png)</span></span>
3. <span data-ttu-id="63010-151">流程完成時，請檢查您指定的收件者郵件。</span><span class="sxs-lookup"><span data-stu-id="63010-151">When the flow completes, check the mail of the recipient that you specified.</span></span>  <span data-ttu-id="63010-152">您應該會收到內文類似如下的郵件：</span><span class="sxs-lookup"><span data-stu-id="63010-152">You should have received a mail with a body similar to the following:</span></span><br><br>![範例電子郵件](media/log-analytics-flow-tutorial/flow08.png)


## <a name="next-steps"></a><span data-ttu-id="63010-154">後續步驟</span><span class="sxs-lookup"><span data-stu-id="63010-154">Next steps</span></span>

- <span data-ttu-id="63010-155">深入了解 [Log Analytics 中的記錄搜尋](log-analytics-log-search-new.md)。</span><span class="sxs-lookup"><span data-stu-id="63010-155">Learn more about [log searches in Log Analytics](log-analytics-log-search-new.md).</span></span>
- <span data-ttu-id="63010-156">深入了解 [Microsoft Flow](https://ms.flow.microsoft.com)。</span><span class="sxs-lookup"><span data-stu-id="63010-156">Learn more about [Microsoft Flow](https://ms.flow.microsoft.com).</span></span>



