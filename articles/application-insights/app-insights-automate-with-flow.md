---
title: "aaaAutomate 與 Microsoft Flow 處理 Azure Application Insights"
description: "了解如何使用 Microsoft Flow tooquickly 使用 hello Application Insights 連接器來自動化重複程序。"
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 06/25/2017
ms.author: bwren
ms.openlocfilehash: b34488a6b8b8b0a6add960a67f1426cbbbc13552
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="automate-azure-application-insights-processes-with-hello-connector-for-microsoft-flow"></a><span data-ttu-id="c7292-103">Microsoft flow 自動化 Azure Application Insights 處理程序與 hello 連接器</span><span class="sxs-lookup"><span data-stu-id="c7292-103">Automate Azure Application Insights processes with hello connector for Microsoft Flow</span></span>

<span data-ttu-id="c7292-104">您發現自己重複 hello 相同的查詢上執行您的服務運作正常您遙測資料 toocheck 嗎？</span><span class="sxs-lookup"><span data-stu-id="c7292-104">Do you find yourself repeatedly running hello same queries on your telemetry data toocheck that your service is functioning properly?</span></span> <span data-ttu-id="c7292-105">您尋找 tooautomate 這些查詢來尋找趨勢和異常及再建置您自己的工作流程周圍嗎？Microsoft flow hello Azure Application Insights 連接器 （預覽） 會針對這些用途是 hello 正確的工具。</span><span class="sxs-lookup"><span data-stu-id="c7292-105">Are you looking tooautomate these queries for finding trends and anomalies and then build your own workflows around them? hello Azure Application Insights connector (preview) for Microsoft Flow is hello right tool for these purposes.</span></span>

<span data-ttu-id="c7292-106">有了此整合，您就能立即自動執行許多流程，而不需撰寫任何一行程式碼。</span><span class="sxs-lookup"><span data-stu-id="c7292-106">With this integration, you can now automate numerous processes without writing a single line of code.</span></span> <span data-ttu-id="c7292-107">使用 Application Insights 動作建立流程之後，hello 流程會自動執行應用程式 Insights 分析查詢。</span><span class="sxs-lookup"><span data-stu-id="c7292-107">After you create a flow by using an Application Insights action, hello flow automatically runs your Application Insights Analytics query.</span></span> 

<span data-ttu-id="c7292-108">您也可以新增額外的動作。</span><span class="sxs-lookup"><span data-stu-id="c7292-108">You can add additional actions as well.</span></span> <span data-ttu-id="c7292-109">Microsoft Flow 提供數百個動作。</span><span class="sxs-lookup"><span data-stu-id="c7292-109">Microsoft Flow makes hundreds of actions available.</span></span> <span data-ttu-id="c7292-110">例如，您可以使用 Microsoft Flow tooautomatically 傳送電子郵件通知，或在 Visual Studio Team Services 中建立 bug。</span><span class="sxs-lookup"><span data-stu-id="c7292-110">For example, you can use Microsoft Flow tooautomatically send an email notification or create a bug in Visual Studio Team Services.</span></span> <span data-ttu-id="c7292-111">您也可以使用其中一個 hello 許多[範本](https://ms.flow.microsoft.com/en-us/connectors/shared_applicationinsights/?slug=azure-application-insights)可用的 Microsoft flow hello 連接器。</span><span class="sxs-lookup"><span data-stu-id="c7292-111">You can also use one of hello many [templates](https://ms.flow.microsoft.com/en-us/connectors/shared_applicationinsights/?slug=azure-application-insights) that are available for hello connector for Microsoft Flow.</span></span> <span data-ttu-id="c7292-112">這些範本會加快建立資料流程的 hello 程序。</span><span class="sxs-lookup"><span data-stu-id="c7292-112">These templates speed up hello process of creating a flow.</span></span> 

<!--hello Application Insights connector also works with [Azure Power Apps](https://powerapps.microsoft.com/en-us/) and [Azure Logic Apps](https://azure.microsoft.com/services/logic-apps/?v=17.23h). --> 

## <a name="create-a-flow-for-application-insights"></a><span data-ttu-id="c7292-113">建立 Application Insights 的流程</span><span class="sxs-lookup"><span data-stu-id="c7292-113">Create a flow for Application Insights</span></span>

<span data-ttu-id="c7292-114">在本教學課程中，您將學習如何 toocreate 使用 hello 分析自動叢集演算法 toogroup 資料流程中的屬性 hello web 應用程式的資料。</span><span class="sxs-lookup"><span data-stu-id="c7292-114">In this tutorial, you will learn how toocreate a flow that uses hello Analytics auto-cluster algorithm toogroup attributes in hello data for a web application.</span></span> <span data-ttu-id="c7292-115">hello 流量會透過電子郵件、 只在一個範例，告訴您可以使用 Microsoft Flow 及應用程式 Insights 分析一起自動傳送 hello 結果。</span><span class="sxs-lookup"><span data-stu-id="c7292-115">hello flow automatically sends hello results by email, just one example of how you can use Microsoft Flow and Application Insights Analytics together.</span></span> 

### <a name="step-1-create-a-flow"></a><span data-ttu-id="c7292-116">步驟 1：建立流程</span><span class="sxs-lookup"><span data-stu-id="c7292-116">Step 1: Create a flow</span></span>
1. <span data-ttu-id="c7292-117">登入太[Microsoft Flow](http://flow.microsoft.com)，然後選取**我流動**。</span><span class="sxs-lookup"><span data-stu-id="c7292-117">Sign in too[Microsoft Flow](http://flow.microsoft.com), and then select **My Flows**.</span></span>
2. <span data-ttu-id="c7292-118">按一下 [從空白建立流程]。</span><span class="sxs-lookup"><span data-stu-id="c7292-118">Click **Create a flow from blank**.</span></span>

### <a name="step-2-create-a-trigger-for-your-flow"></a><span data-ttu-id="c7292-119">步驟 2：建立流程的觸發程序</span><span class="sxs-lookup"><span data-stu-id="c7292-119">Step 2: Create a trigger for your flow</span></span>
1. <span data-ttu-id="c7292-120">依序選取 [排程] 和 [排程 - 重複]。</span><span class="sxs-lookup"><span data-stu-id="c7292-120">Select **Schedule**, and then select **Schedule - Recurrence**.</span></span>
2. <span data-ttu-id="c7292-121">在 hello**頻率**方塊中，選取**天**，在 hello**間隔**方塊中，輸入**1**。</span><span class="sxs-lookup"><span data-stu-id="c7292-121">In hello **Frequency** box, select **Day**, and in hello **Interval** box, enter **1**.</span></span>

    ![Microsoft Flow 觸發程序對話方塊](./media/app-insights-automate-with-flow/flow1.png)


### <a name="step-3-add-an-application-insights-action"></a><span data-ttu-id="c7292-123">步驟 3：新增 Application Insights 動作</span><span class="sxs-lookup"><span data-stu-id="c7292-123">Step 3: Add an Application Insights action</span></span>
1. <span data-ttu-id="c7292-124">按一下 新增步驟，然後按一下新增動作。</span><span class="sxs-lookup"><span data-stu-id="c7292-124">Click **New step**, and then click **Add an action**.</span></span>
2. <span data-ttu-id="c7292-125">搜尋 **Azure Application Insights**。</span><span class="sxs-lookup"><span data-stu-id="c7292-125">Search for **Azure Application Insights**.</span></span>
3. <span data-ttu-id="c7292-126">按一下 [Azure Application Insights – 視覺化 Analytics 查詢預覽]。</span><span class="sxs-lookup"><span data-stu-id="c7292-126">Click **Azure Application Insights – Visualize Analytics query Preview**.</span></span>

    ![執行 Analytics 查詢視窗](./media/app-insights-automate-with-flow/flow2.png)

### <a name="step-4-connect-tooan-application-insights-resource"></a><span data-ttu-id="c7292-128">步驟 4： 連接 tooan Application Insights 資源</span><span class="sxs-lookup"><span data-stu-id="c7292-128">Step 4: Connect tooan Application Insights resource</span></span>

<span data-ttu-id="c7292-129">toocomplete 此步驟中，您需要您為資源的應用程式識別碼和 API 金鑰。</span><span class="sxs-lookup"><span data-stu-id="c7292-129">toocomplete this step, you need an application ID and an API key for your resource.</span></span> <span data-ttu-id="c7292-130">您可以從取回 hello Azure 入口網站中 hello 下列圖表所示：</span><span class="sxs-lookup"><span data-stu-id="c7292-130">You can retrieve them from hello Azure portal, as shown in hello following diagram:</span></span>

![在 hello Azure 入口網站應用程式識別碼](./media/app-insights-automate-with-flow/appid.png) 

- <span data-ttu-id="c7292-132">提供您的連線，以及 hello 應用程式識別碼和 API 金鑰的名稱。</span><span class="sxs-lookup"><span data-stu-id="c7292-132">Provide a name for your connection, along with hello application ID and API key.</span></span>

    ![Microsoft Flow 連線視窗](./media/app-insights-automate-with-flow/flow3.png)

### <a name="step-5-specify-hello-analytics-query-and-chart-type"></a><span data-ttu-id="c7292-134">步驟 5： 指定 hello 分析查詢和圖表類型</span><span class="sxs-lookup"><span data-stu-id="c7292-134">Step 5: Specify hello Analytics query and chart type</span></span>
<span data-ttu-id="c7292-135">這個範例查詢會選取 hello 最後一天中的 hello 失敗要求，並將它們與 hello 作業期間發生的例外狀況相互關聯。</span><span class="sxs-lookup"><span data-stu-id="c7292-135">This example query selects hello failed requests within hello last day and correlates them with exceptions that occurred as part of hello operation.</span></span> <span data-ttu-id="c7292-136">分析相互關聯根據 hello operation_Id 識別項。</span><span class="sxs-lookup"><span data-stu-id="c7292-136">Analytics correlates them based on hello operation_Id identifier.</span></span> <span data-ttu-id="c7292-137">hello 查詢然後區段 hello 結果使用 hello autocluster 演算法。</span><span class="sxs-lookup"><span data-stu-id="c7292-137">hello query then segments hello results by using hello autocluster algorithm.</span></span> 

<span data-ttu-id="c7292-138">當您建立您自己的查詢時，確認它們會正常運作在分析中加入 tooyour 流程之前。</span><span class="sxs-lookup"><span data-stu-id="c7292-138">When you create your own queries, verify that they are working properly in Analytics before you add it tooyour flow.</span></span>

- <span data-ttu-id="c7292-139">新增下列分析查詢的 hello，然後選取 hello HTML 表格的圖表類型。</span><span class="sxs-lookup"><span data-stu-id="c7292-139">Add hello following Analytics query, and then select hello HTML table chart type.</span></span> 

    ```
    requests
    | where timestamp > ago(1d)
    | where success == "False"
    | project name, operation_Id
    | join ( exceptions
        | project problemId, outerMessage, operation_Id
    ) on operation_Id
    | evaluate autocluster()
    ```
    
    ![Analytics 查詢設定畫面](./media/app-insights-automate-with-flow/flow4.png)

### <a name="step-6-configure-hello-flow-toosend-email"></a><span data-ttu-id="c7292-141">步驟 6： 設定 hello 流程 toosend 電子郵件</span><span class="sxs-lookup"><span data-stu-id="c7292-141">Step 6: Configure hello flow toosend email</span></span>

1. <span data-ttu-id="c7292-142">按一下 新增步驟，然後按一下新增動作。</span><span class="sxs-lookup"><span data-stu-id="c7292-142">Click **New step**, and then click **Add an action**.</span></span>
2. <span data-ttu-id="c7292-143">搜尋 **Office 365 Outlook**。</span><span class="sxs-lookup"><span data-stu-id="c7292-143">Search for **Office 365 Outlook**.</span></span>
3. <span data-ttu-id="c7292-144">按一下 [Office 365 Outlook – 傳送電子郵件]。</span><span class="sxs-lookup"><span data-stu-id="c7292-144">Click **Office 365 Outlook – Send an email**.</span></span>

    ![Office 365 Outlook 選取視窗](./media/app-insights-automate-with-flow/flow2b.png)

4. <span data-ttu-id="c7292-146">在 hello**傳送電子郵件**視窗中，執行下列 hello:</span><span class="sxs-lookup"><span data-stu-id="c7292-146">In hello **Send an email** window, do hello following:</span></span>

   <span data-ttu-id="c7292-147">a.</span><span class="sxs-lookup"><span data-stu-id="c7292-147">a.</span></span> <span data-ttu-id="c7292-148">輸入 hello hello 收件者電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="c7292-148">Type hello email address of hello recipient.</span></span>

   <span data-ttu-id="c7292-149">b.</span><span class="sxs-lookup"><span data-stu-id="c7292-149">b.</span></span> <span data-ttu-id="c7292-150">輸入 hello 電子郵件的主旨。</span><span class="sxs-lookup"><span data-stu-id="c7292-150">Type a subject for hello email.</span></span>

   <span data-ttu-id="c7292-151">c.</span><span class="sxs-lookup"><span data-stu-id="c7292-151">c.</span></span> <span data-ttu-id="c7292-152">按一下任何位置中的 hello**主體**方塊，然後 hello 動態內容功能表開啟在 hello 右、 上選取**主體**。</span><span class="sxs-lookup"><span data-stu-id="c7292-152">Click anywhere in hello **Body** box and then, on hello dynamic content menu that opens at hello right, select **Body**.</span></span>

   <span data-ttu-id="c7292-153">d.</span><span class="sxs-lookup"><span data-stu-id="c7292-153">d.</span></span> <span data-ttu-id="c7292-154">按一下 [顯示進階選項]。</span><span class="sxs-lookup"><span data-stu-id="c7292-154">Click **Show advanced options**.</span></span>

    ![Office 365 Outlook 設定](./media/app-insights-automate-with-flow/flow5.png)

5. <span data-ttu-id="c7292-156">Hello 動態內容功能表上，hello 遵循：</span><span class="sxs-lookup"><span data-stu-id="c7292-156">On hello dynamic content menu, do hello following:</span></span>

    <span data-ttu-id="c7292-157">a.</span><span class="sxs-lookup"><span data-stu-id="c7292-157">a.</span></span> <span data-ttu-id="c7292-158">選取 [附件名稱]。</span><span class="sxs-lookup"><span data-stu-id="c7292-158">Select **Attachment Name**.</span></span>

    <span data-ttu-id="c7292-159">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="c7292-159">b.</span></span> <span data-ttu-id="c7292-160">選取 [附件內容]。</span><span class="sxs-lookup"><span data-stu-id="c7292-160">Select **Attachment Content**.</span></span>
    
    <span data-ttu-id="c7292-161">c.</span><span class="sxs-lookup"><span data-stu-id="c7292-161">c.</span></span> <span data-ttu-id="c7292-162">在 hello**是 HTML**方塊中，選取**是**。</span><span class="sxs-lookup"><span data-stu-id="c7292-162">In hello **Is HTML** box, select **Yes**.</span></span>

    ![Office 365 電子郵件設定畫面](./media/app-insights-automate-with-flow/flow7.png)

### <a name="step-7-save-and-test-your-flow"></a><span data-ttu-id="c7292-164">步驟 7：儲存並測試流程</span><span class="sxs-lookup"><span data-stu-id="c7292-164">Step 7: Save and test your flow</span></span>
- <span data-ttu-id="c7292-165">在 hello**流程名稱**方塊中，加入您的流程的名稱，然後按一下**建立流程**。</span><span class="sxs-lookup"><span data-stu-id="c7292-165">In hello **Flow name** box, add a name for your flow, and then click **Create flow**.</span></span>

    ![流程建立視窗](./media/app-insights-automate-with-flow/flow8.png)

<span data-ttu-id="c7292-167">您可以等候 hello 觸發程序 toorun 此動作，或者您可以立即藉由執行 hello 流程[依需求執行 hello 觸發程序](https://flow.microsoft.com/blog/run-now-and-six-more-services/)。</span><span class="sxs-lookup"><span data-stu-id="c7292-167">You can wait for hello trigger toorun this action, or you can run hello flow immediately by [running hello trigger on demand](https://flow.microsoft.com/blog/run-now-and-six-more-services/).</span></span>

<span data-ttu-id="c7292-168">Hello 流程執行時，hello hello 的電子郵件清單中所指定的收件者會收到電子郵件訊息，看起來像下列 hello:</span><span class="sxs-lookup"><span data-stu-id="c7292-168">When hello flow runs, hello recipients you have specified in hello email list receive an email message that looks like hello following:</span></span>

![範例電子郵件](./media/app-insights-automate-with-flow/flow9.png)


## <a name="next-steps"></a><span data-ttu-id="c7292-170">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c7292-170">Next steps</span></span>

- <span data-ttu-id="c7292-171">深入了解建立 [Analytics 查詢](app-insights-analytics-using.md)。</span><span class="sxs-lookup"><span data-stu-id="c7292-171">Learn more about creating [Analytics queries](app-insights-analytics-using.md).</span></span>
- <span data-ttu-id="c7292-172">深入了解 [Microsoft Flow](https://ms.flow.microsoft.com)。</span><span class="sxs-lookup"><span data-stu-id="c7292-172">Learn more about [Microsoft Flow](https://ms.flow.microsoft.com).</span></span>



<!--Link references-->





