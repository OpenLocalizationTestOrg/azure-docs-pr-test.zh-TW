---
title: "使用 Microsoft Flow 自動化 Azure Application Insights 程序"
description: "了解如何利用 Application Insights Connector，使用 Microsoft Flow 來快速自動執行可重複的程序。"
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
ms.openlocfilehash: 510f4f284bbd0dbe4171896899f7ade7dee19e39
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="automate-azure-application-insights-processes-with-the-connector-for-microsoft-flow"></a><span data-ttu-id="c0927-103">使用適用於 Microsoft Flow 的連接器自動執行 Azure Application Insights 程序</span><span class="sxs-lookup"><span data-stu-id="c0927-103">Automate Azure Application Insights processes with the connector for Microsoft Flow</span></span>

<span data-ttu-id="c0927-104">您是否發現自己在遙測資料上不斷重複地執行相同查詢，以檢查服務是否正常運作？</span><span class="sxs-lookup"><span data-stu-id="c0927-104">Do you find yourself repeatedly running the same queries on your telemetry data to check that your service is functioning properly?</span></span> <span data-ttu-id="c0927-105">想要將此類查詢自動化以尋找趨勢和異常，然後針對它們建立您自己的工作流程嗎？</span><span class="sxs-lookup"><span data-stu-id="c0927-105">Are you looking to automate these queries for finding trends and anomalies and then build your own workflows around them?</span></span> <span data-ttu-id="c0927-106">適用於 Microsoft Flow 的 Application Insights Connector (預覽) 正是符合這些用途的工具。</span><span class="sxs-lookup"><span data-stu-id="c0927-106">The Azure Application Insights connector (preview) for Microsoft Flow is the right tool for these purposes.</span></span>

<span data-ttu-id="c0927-107">有了此整合，您就能立即自動執行許多流程，而不需撰寫任何一行程式碼。</span><span class="sxs-lookup"><span data-stu-id="c0927-107">With this integration, you can now automate numerous processes without writing a single line of code.</span></span> <span data-ttu-id="c0927-108">在您使用 Application Insights 動作建立流程後，此流程會自動執行 Application Insights Analytics 查詢。</span><span class="sxs-lookup"><span data-stu-id="c0927-108">After you create a flow by using an Application Insights action, the flow automatically runs your Application Insights Analytics query.</span></span> 

<span data-ttu-id="c0927-109">您也可以新增額外的動作。</span><span class="sxs-lookup"><span data-stu-id="c0927-109">You can add additional actions as well.</span></span> <span data-ttu-id="c0927-110">Microsoft Flow 提供數百個動作。</span><span class="sxs-lookup"><span data-stu-id="c0927-110">Microsoft Flow makes hundreds of actions available.</span></span> <span data-ttu-id="c0927-111">例如，您可以使用 Microsoft Flow 來自動傳送電子郵件通知，或是在 Visual Studio Team Services 中建立錯誤 (Bug)。</span><span class="sxs-lookup"><span data-stu-id="c0927-111">For example, you can use Microsoft Flow to automatically send an email notification or create a bug in Visual Studio Team Services.</span></span> <span data-ttu-id="c0927-112">您也可以使用提供給適用於 Microsoft Flow 之連接器的任何一種[範本](https://ms.flow.microsoft.com/en-us/connectors/shared_applicationinsights/?slug=azure-application-insights)。</span><span class="sxs-lookup"><span data-stu-id="c0927-112">You can also use one of the many [templates](https://ms.flow.microsoft.com/en-us/connectors/shared_applicationinsights/?slug=azure-application-insights) that are available for the connector for Microsoft Flow.</span></span> <span data-ttu-id="c0927-113">這些範本可加快建立流程的程序。</span><span class="sxs-lookup"><span data-stu-id="c0927-113">These templates speed up the process of creating a flow.</span></span> 

<!--The Application Insights connector also works with [Azure Power Apps](https://powerapps.microsoft.com/en-us/) and [Azure Logic Apps](https://azure.microsoft.com/services/logic-apps/?v=17.23h). --> 

## <a name="create-a-flow-for-application-insights"></a><span data-ttu-id="c0927-114">建立 Application Insights 的流程</span><span class="sxs-lookup"><span data-stu-id="c0927-114">Create a flow for Application Insights</span></span>

<span data-ttu-id="c0927-115">在此教學課程中，您將學習如何建立流程，該流程會使用 Analytics 自動叢集演算法將 Web 應用程式資料中的屬性分組。</span><span class="sxs-lookup"><span data-stu-id="c0927-115">In this tutorial, you will learn how to create a flow that uses the Analytics auto-cluster algorithm to group attributes in the data for a web application.</span></span> <span data-ttu-id="c0927-116">此流程會以電子郵件自動傳送結果，這只是如何將 Microsoft Flow 和 Application Insights Analytics 一起使用的其中一個範例。</span><span class="sxs-lookup"><span data-stu-id="c0927-116">The flow automatically sends the results by email, just one example of how you can use Microsoft Flow and Application Insights Analytics together.</span></span> 

### <a name="step-1-create-a-flow"></a><span data-ttu-id="c0927-117">步驟 1：建立流程</span><span class="sxs-lookup"><span data-stu-id="c0927-117">Step 1: Create a flow</span></span>
1. <span data-ttu-id="c0927-118">登入 [Microsoft Flow](http://flow.microsoft.com)，然後選取 [我的流程]。</span><span class="sxs-lookup"><span data-stu-id="c0927-118">Sign in to [Microsoft Flow](http://flow.microsoft.com), and then select **My Flows**.</span></span>
2. <span data-ttu-id="c0927-119">按一下 [從空白建立流程]。</span><span class="sxs-lookup"><span data-stu-id="c0927-119">Click **Create a flow from blank**.</span></span>

### <a name="step-2-create-a-trigger-for-your-flow"></a><span data-ttu-id="c0927-120">步驟 2：建立流程的觸發程序</span><span class="sxs-lookup"><span data-stu-id="c0927-120">Step 2: Create a trigger for your flow</span></span>
1. <span data-ttu-id="c0927-121">依序選取 [排程] 和 [排程 - 重複]。</span><span class="sxs-lookup"><span data-stu-id="c0927-121">Select **Schedule**, and then select **Schedule - Recurrence**.</span></span>
2. <span data-ttu-id="c0927-122">在 [頻率] 方塊中選取 [天]，然後在 [間隔] 方塊中輸入 **1**。</span><span class="sxs-lookup"><span data-stu-id="c0927-122">In the **Frequency** box, select **Day**, and in the **Interval** box, enter **1**.</span></span>

    ![Microsoft Flow 觸發程序對話方塊](./media/app-insights-automate-with-flow/flow1.png)


### <a name="step-3-add-an-application-insights-action"></a><span data-ttu-id="c0927-124">步驟 3：新增 Application Insights 動作</span><span class="sxs-lookup"><span data-stu-id="c0927-124">Step 3: Add an Application Insights action</span></span>
1. <span data-ttu-id="c0927-125">按一下 [新增步驟]，然後按一下 [新增動作]。</span><span class="sxs-lookup"><span data-stu-id="c0927-125">Click **New step**, and then click **Add an action**.</span></span>
2. <span data-ttu-id="c0927-126">搜尋 **Azure Application Insights**。</span><span class="sxs-lookup"><span data-stu-id="c0927-126">Search for **Azure Application Insights**.</span></span>
3. <span data-ttu-id="c0927-127">按一下 [Azure Application Insights – 視覺化 Analytics 查詢預覽]。</span><span class="sxs-lookup"><span data-stu-id="c0927-127">Click **Azure Application Insights – Visualize Analytics query Preview**.</span></span>

    ![執行 Analytics 查詢視窗](./media/app-insights-automate-with-flow/flow2.png)

### <a name="step-4-connect-to-an-application-insights-resource"></a><span data-ttu-id="c0927-129">步驟 4：連線到 Application Insights 資源</span><span class="sxs-lookup"><span data-stu-id="c0927-129">Step 4: Connect to an Application Insights resource</span></span>

<span data-ttu-id="c0927-130">若要完成此步驟，您需要資源的應用程式識別碼和 API 金鑰。</span><span class="sxs-lookup"><span data-stu-id="c0927-130">To complete this step, you need an application ID and an API key for your resource.</span></span> <span data-ttu-id="c0927-131">您可以從 Azure 入口網站擷取這些資訊，如下圖所示：</span><span class="sxs-lookup"><span data-stu-id="c0927-131">You can retrieve them from the Azure portal, as shown in the following diagram:</span></span>

![Azure 入口網站中的應用程式識別碼](./media/app-insights-automate-with-flow/appid.png) 

- <span data-ttu-id="c0927-133">為您的連線提供名稱，以及應用程式識別碼和 API 金鑰。</span><span class="sxs-lookup"><span data-stu-id="c0927-133">Provide a name for your connection, along with the application ID and API key.</span></span>

    ![Microsoft Flow 連線視窗](./media/app-insights-automate-with-flow/flow3.png)

### <a name="step-5-specify-the-analytics-query-and-chart-type"></a><span data-ttu-id="c0927-135">步驟 5：指定 Analytics 查詢和圖表類型</span><span class="sxs-lookup"><span data-stu-id="c0927-135">Step 5: Specify the Analytics query and chart type</span></span>
<span data-ttu-id="c0927-136">此範例查詢會選取最後一天內的失敗要求，並將它們與作業發生的例外狀況相互關聯。</span><span class="sxs-lookup"><span data-stu-id="c0927-136">This example query selects the failed requests within the last day and correlates them with exceptions that occurred as part of the operation.</span></span> <span data-ttu-id="c0927-137">Analytics 會根據 operation_Id 識別碼使其相互關聯。</span><span class="sxs-lookup"><span data-stu-id="c0927-137">Analytics correlates them based on the operation_Id identifier.</span></span> <span data-ttu-id="c0927-138">查詢接著會使用自動叢集演算法將結果分段。</span><span class="sxs-lookup"><span data-stu-id="c0927-138">The query then segments the results by using the autocluster algorithm.</span></span> 

<span data-ttu-id="c0927-139">建立自己的查詢時，先確認它們可在 Analytics 中正常運作，再將其新增到您的流程中。</span><span class="sxs-lookup"><span data-stu-id="c0927-139">When you create your own queries, verify that they are working properly in Analytics before you add it to your flow.</span></span>

- <span data-ttu-id="c0927-140">新增下列 Analytics 查詢，然後選取 HTML 表格圖表類型。</span><span class="sxs-lookup"><span data-stu-id="c0927-140">Add the following Analytics query, and then select the HTML table chart type.</span></span> 

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

### <a name="step-6-configure-the-flow-to-send-email"></a><span data-ttu-id="c0927-142">步驟 6：設定傳送電子郵件的流程</span><span class="sxs-lookup"><span data-stu-id="c0927-142">Step 6: Configure the flow to send email</span></span>

1. <span data-ttu-id="c0927-143">按一下 [新增步驟]，然後按一下 [新增動作]。</span><span class="sxs-lookup"><span data-stu-id="c0927-143">Click **New step**, and then click **Add an action**.</span></span>
2. <span data-ttu-id="c0927-144">搜尋 **Office 365 Outlook**。</span><span class="sxs-lookup"><span data-stu-id="c0927-144">Search for **Office 365 Outlook**.</span></span>
3. <span data-ttu-id="c0927-145">按一下 [Office 365 Outlook – 傳送電子郵件]。</span><span class="sxs-lookup"><span data-stu-id="c0927-145">Click **Office 365 Outlook – Send an email**.</span></span>

    ![Office 365 Outlook 選取視窗](./media/app-insights-automate-with-flow/flow2b.png)

4. <span data-ttu-id="c0927-147">在 [傳送電子郵件]  視窗中，執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="c0927-147">In the **Send an email** window, do the following:</span></span>

   <span data-ttu-id="c0927-148">a.</span><span class="sxs-lookup"><span data-stu-id="c0927-148">a.</span></span> <span data-ttu-id="c0927-149">輸入收件者的電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="c0927-149">Type the email address of the recipient.</span></span>

   <span data-ttu-id="c0927-150">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="c0927-150">b.</span></span> <span data-ttu-id="c0927-151">輸入電子郵件的主旨。</span><span class="sxs-lookup"><span data-stu-id="c0927-151">Type a subject for the email.</span></span>

   <span data-ttu-id="c0927-152">c.</span><span class="sxs-lookup"><span data-stu-id="c0927-152">c.</span></span> <span data-ttu-id="c0927-153">按一下 [內文] 方塊中的任意處，然後在右方開啟的動態內容功能表上，選取 [內文]。</span><span class="sxs-lookup"><span data-stu-id="c0927-153">Click anywhere in the **Body** box and then, on the dynamic content menu that opens at the right, select **Body**.</span></span>

   <span data-ttu-id="c0927-154">d.</span><span class="sxs-lookup"><span data-stu-id="c0927-154">d.</span></span> <span data-ttu-id="c0927-155">按一下 [顯示進階選項]。</span><span class="sxs-lookup"><span data-stu-id="c0927-155">Click **Show advanced options**.</span></span>

    ![Office 365 Outlook 設定](./media/app-insights-automate-with-flow/flow5.png)

5. <span data-ttu-id="c0927-157">在動態內容功能表上執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="c0927-157">On the dynamic content menu, do the following:</span></span>

    <span data-ttu-id="c0927-158">a.</span><span class="sxs-lookup"><span data-stu-id="c0927-158">a.</span></span> <span data-ttu-id="c0927-159">選取 [附件名稱]。</span><span class="sxs-lookup"><span data-stu-id="c0927-159">Select **Attachment Name**.</span></span>

    <span data-ttu-id="c0927-160">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="c0927-160">b.</span></span> <span data-ttu-id="c0927-161">選取 [附件內容]。</span><span class="sxs-lookup"><span data-stu-id="c0927-161">Select **Attachment Content**.</span></span>
    
    <span data-ttu-id="c0927-162">c.</span><span class="sxs-lookup"><span data-stu-id="c0927-162">c.</span></span> <span data-ttu-id="c0927-163">在 [為 HTML] 方塊中選取 [是]。</span><span class="sxs-lookup"><span data-stu-id="c0927-163">In the **Is HTML** box, select **Yes**.</span></span>

    ![Office 365 電子郵件設定畫面](./media/app-insights-automate-with-flow/flow7.png)

### <a name="step-7-save-and-test-your-flow"></a><span data-ttu-id="c0927-165">步驟 7：儲存並測試流程</span><span class="sxs-lookup"><span data-stu-id="c0927-165">Step 7: Save and test your flow</span></span>
- <span data-ttu-id="c0927-166">在 [流程名稱] 方塊中，新增您的流程名稱，然後按一下 [建立流程]。</span><span class="sxs-lookup"><span data-stu-id="c0927-166">In the **Flow name** box, add a name for your flow, and then click **Create flow**.</span></span>

    ![流程建立視窗](./media/app-insights-automate-with-flow/flow8.png)

<span data-ttu-id="c0927-168">您可以等候觸發程序執行此動作，或[視需要執行觸發程序](https://flow.microsoft.com/blog/run-now-and-six-more-services/)來立即執行流程。</span><span class="sxs-lookup"><span data-stu-id="c0927-168">You can wait for the trigger to run this action, or you can run the flow immediately by [running the trigger on demand](https://flow.microsoft.com/blog/run-now-and-six-more-services/).</span></span>

<span data-ttu-id="c0927-169">流程執行時，您在電子郵件清單中所指定的收件者會收到看起來如下的電子郵件：</span><span class="sxs-lookup"><span data-stu-id="c0927-169">When the flow runs, the recipients you have specified in the email list receive an email message that looks like the following:</span></span>

![範例電子郵件](./media/app-insights-automate-with-flow/flow9.png)


## <a name="next-steps"></a><span data-ttu-id="c0927-171">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c0927-171">Next steps</span></span>

- <span data-ttu-id="c0927-172">深入了解建立 [Analytics 查詢](app-insights-analytics-using.md)。</span><span class="sxs-lookup"><span data-stu-id="c0927-172">Learn more about creating [Analytics queries](app-insights-analytics-using.md).</span></span>
- <span data-ttu-id="c0927-173">深入了解 [Microsoft Flow](https://ms.flow.microsoft.com)。</span><span class="sxs-lookup"><span data-stu-id="c0927-173">Learn more about [Microsoft Flow](https://ms.flow.microsoft.com).</span></span>



<!--Link references-->





