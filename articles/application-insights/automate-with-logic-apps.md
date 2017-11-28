---
title: "aaaAutomate 使用 Logic Apps 處理 Azure Application Insights。"
description: "了解如何您可以快速自動化重複程序加入 hello Application Insights 連接器 tooyour 邏輯應用程式。"
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: bwren
ms.openlocfilehash: 8565aadf0644ffb10da8a0964821901907db2e27
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="automate-application-insights-processes-by-using-logic-apps"></a><span data-ttu-id="cd5ca-103">使用 Logic Apps 自動執行 Application Insights 程序</span><span class="sxs-lookup"><span data-stu-id="cd5ca-103">Automate Application Insights processes by using Logic Apps</span></span>

<span data-ttu-id="cd5ca-104">您發現自己重複 hello 相同的查詢上執行您的遙測資料 toocheck 是否正常運作您的服務？</span><span class="sxs-lookup"><span data-stu-id="cd5ca-104">Do you find yourself repeatedly running hello same queries on your telemetry data toocheck whether your service is functioning properly?</span></span> <span data-ttu-id="cd5ca-105">您尋找 tooautomate 這些查詢來尋找趨勢和異常及再建置您自己的工作流程周圍嗎？Logic apps hello Azure Application Insights 連接器 （預覽） 是針對此用途的 hello 正確的工具。</span><span class="sxs-lookup"><span data-stu-id="cd5ca-105">Are you looking tooautomate these queries for finding trends and anomalies and then build your own workflows around them? hello Azure Application Insights connector (preview) for Logic Apps is hello right tool for this purpose.</span></span>

<span data-ttu-id="cd5ca-106">有了此整合，您就能自動執行許多流程，而不需撰寫任何一行程式碼。</span><span class="sxs-lookup"><span data-stu-id="cd5ca-106">With this integration, you can automate numerous processes without writing a single line of code.</span></span> <span data-ttu-id="cd5ca-107">您可以建立邏輯應用程式以 hello Application Insights 連接器 tooquickly 任何 Application Insights 程序自動化。</span><span class="sxs-lookup"><span data-stu-id="cd5ca-107">You can create a logic app with hello Application Insights connector tooquickly automate any Application Insights process.</span></span> 

<span data-ttu-id="cd5ca-108">您也可以新增額外的動作。</span><span class="sxs-lookup"><span data-stu-id="cd5ca-108">You can add additional actions as well.</span></span> <span data-ttu-id="cd5ca-109">Azure App Service hello Logic Apps 功能可讓您提供數百個動作。</span><span class="sxs-lookup"><span data-stu-id="cd5ca-109">hello Logic Apps feature of Azure App Service makes hundreds of actions available.</span></span> <span data-ttu-id="cd5ca-110">例如，使用邏輯應用程式，您可以自動傳送電子郵件通知，或在 Visual Studio Team Services 中建立 Bug。</span><span class="sxs-lookup"><span data-stu-id="cd5ca-110">For example, by using a logic app, you can automatically send an email notification or create a bug in Visual Studio Team Services.</span></span> <span data-ttu-id="cd5ca-111">您也可以使用其中一個 hello 許多可用[範本](https://docs.microsoft.com/azure/logic-apps/logic-apps-use-logic-app-templates)toohelp 加速 hello 處理程序的建立應用程式邏輯。</span><span class="sxs-lookup"><span data-stu-id="cd5ca-111">You can also use one of hello many available [templates](https://docs.microsoft.com/azure/logic-apps/logic-apps-use-logic-app-templates) toohelp speed up hello process of creating your logic app.</span></span> 

## <a name="create-a-logic-app-for-application-insights"></a><span data-ttu-id="cd5ca-112">建立 Application Insights 的邏輯應用程式</span><span class="sxs-lookup"><span data-stu-id="cd5ca-112">Create a logic app for Application Insights</span></span>

<span data-ttu-id="cd5ca-113">在此教學課程中，您學會 toocreate 邏輯應用程式使用 hello 分析 autocluster 演算法 toogroup 屬性是如何在 web 應用程式的 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="cd5ca-113">In this tutorial, you learn how toocreate a logic app that uses hello Analytics autocluster algorithm toogroup attributes in hello data for a web application.</span></span> <span data-ttu-id="cd5ca-114">hello 流量會透過電子郵件、 一個範例，告訴您可以使用應用程式 Insights 分析和邏輯應用程式一起自動傳送 hello 結果。</span><span class="sxs-lookup"><span data-stu-id="cd5ca-114">hello flow automatically sends hello results by email, just one example of how you can use Application Insights Analytics and Logic Apps together.</span></span> 

### <a name="step-1-create-a-logic-app"></a><span data-ttu-id="cd5ca-115">步驟 1：建立邏輯應用程式</span><span class="sxs-lookup"><span data-stu-id="cd5ca-115">Step 1: Create a logic app</span></span>
1. <span data-ttu-id="cd5ca-116">登入 toohello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="cd5ca-116">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="cd5ca-117">在 hello**新增**窗格中，選取**Web + 行動**，然後選取**邏輯應用程式**。</span><span class="sxs-lookup"><span data-stu-id="cd5ca-117">In hello **New** pane, select **Web + Mobile**, and then select **Logic App**.</span></span>

    ![新增邏輯應用程式視窗](./media/automate-with-logic-apps/logicapp1.png)

### <a name="step-2-create-a-trigger-for-your-logic-app"></a><span data-ttu-id="cd5ca-119">步驟 2：建立邏輯應用程式的觸發程序</span><span class="sxs-lookup"><span data-stu-id="cd5ca-119">Step 2: Create a trigger for your logic app</span></span>
1. <span data-ttu-id="cd5ca-120">在 hello**邏輯應用程式的設計工具**視窗底下**一般的觸發程序的開頭**，選取**循環**。</span><span class="sxs-lookup"><span data-stu-id="cd5ca-120">In hello **Logic App Designer** window, under **Start with a common trigger**, select **Recurrence**.</span></span>

    ![邏輯應用程式設計工具視窗](./media/automate-with-logic-apps/logicapp2.png)

2. <span data-ttu-id="cd5ca-122">在 hello**頻率**方塊中，選取**天**，然後在 hello**間隔**方塊中，輸入**1**。</span><span class="sxs-lookup"><span data-stu-id="cd5ca-122">In hello **Frequency** box, select **Day** and then, in hello **Interval** box, type **1**.</span></span>

    ![邏輯應用程式設計工具 [參考] 視窗](./media/automate-with-logic-apps/step2b.png)

### <a name="step-3-add-an-application-insights-action"></a><span data-ttu-id="cd5ca-124">步驟 3：新增 Application Insights 動作</span><span class="sxs-lookup"><span data-stu-id="cd5ca-124">Step 3: Add an Application Insights action</span></span>
1. <span data-ttu-id="cd5ca-125">按一下 新增步驟，然後按一下新增動作。</span><span class="sxs-lookup"><span data-stu-id="cd5ca-125">Click **New step**, and then click **Add an action**.</span></span>

2. <span data-ttu-id="cd5ca-126">在 [hello**選擇動作**搜尋] 方塊中，輸入**Azure Application Insights**。</span><span class="sxs-lookup"><span data-stu-id="cd5ca-126">In hello **Choose an action** search box, type **Azure Application Insights**.</span></span>

3. <span data-ttu-id="cd5ca-127">在 [動作] 之下，按一下 [Azure Application Insights – 視覺化 Analytics 查詢預覽]。</span><span class="sxs-lookup"><span data-stu-id="cd5ca-127">Under **Actions**, click **Azure Application Insights – Visualize Analytics query Preview**.</span></span>

    ![邏輯應用程式設計工具的「選擇動作」視窗](./media/automate-with-logic-apps/flow2.png)

### <a name="step-4-connect-tooan-application-insights-resource"></a><span data-ttu-id="cd5ca-129">步驟 4： 連接 tooan Application Insights 資源</span><span class="sxs-lookup"><span data-stu-id="cd5ca-129">Step 4: Connect tooan Application Insights resource</span></span>

<span data-ttu-id="cd5ca-130">toocomplete 此步驟中，您需要您為資源的應用程式識別碼和 API 金鑰。</span><span class="sxs-lookup"><span data-stu-id="cd5ca-130">toocomplete this step, you need an application ID and an API key for your resource.</span></span> <span data-ttu-id="cd5ca-131">您可以從取回 hello Azure 入口網站中 hello 下列圖表所示：</span><span class="sxs-lookup"><span data-stu-id="cd5ca-131">You can retrieve them from hello Azure portal, as shown in hello following diagram:</span></span>

![在 hello Azure 入口網站應用程式識別碼](./media/automate-with-logic-apps/appid.png) 

<span data-ttu-id="cd5ca-133">提供您的連接、 hello 應用程式識別碼和 hello API 金鑰的名稱。</span><span class="sxs-lookup"><span data-stu-id="cd5ca-133">Provide a name for your connection, hello application ID, and hello API key.</span></span>

![邏輯應用程式設計工具連線視窗](./media/automate-with-logic-apps/flow3.png)

### <a name="step-5-specify-hello-analytics-query-and-chart-type"></a><span data-ttu-id="cd5ca-135">步驟 5： 指定 hello 分析查詢和圖表類型</span><span class="sxs-lookup"><span data-stu-id="cd5ca-135">Step 5: Specify hello Analytics query and chart type</span></span>
<span data-ttu-id="cd5ca-136">在下列範例的 hello，hello 查詢會選取 hello 最後一天中的 hello 失敗要求，並將它們與 hello 作業期間發生的例外狀況相互關聯。</span><span class="sxs-lookup"><span data-stu-id="cd5ca-136">In hello following example, hello query selects hello failed requests within hello last day and correlates them with exceptions that occurred as part of hello operation.</span></span> <span data-ttu-id="cd5ca-137">分析相互關聯 hello 失敗的要求，根據 hello operation_Id 識別項。</span><span class="sxs-lookup"><span data-stu-id="cd5ca-137">Analytics correlates hello failed requests, based on hello operation_Id identifier.</span></span> <span data-ttu-id="cd5ca-138">hello 查詢然後區段 hello 結果使用 hello autocluster 演算法。</span><span class="sxs-lookup"><span data-stu-id="cd5ca-138">hello query then segments hello results by using hello autocluster algorithm.</span></span> 

<span data-ttu-id="cd5ca-139">當您建立您自己的查詢時，確認它們會正常運作在分析中加入 tooyour 流程之前。</span><span class="sxs-lookup"><span data-stu-id="cd5ca-139">When you create your own queries, verify that they are working properly in Analytics before you add it tooyour flow.</span></span>

1. <span data-ttu-id="cd5ca-140">在 hello**查詢**方塊中，加入下列分析查詢的 hello:</span><span class="sxs-lookup"><span data-stu-id="cd5ca-140">In hello **Query** box, add hello following Analytics query:</span></span> 

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

2. <span data-ttu-id="cd5ca-141">在 hello**圖表類型**方塊中，選取**Html 表格**。</span><span class="sxs-lookup"><span data-stu-id="cd5ca-141">In hello **Chart Type** box, select **Html Table**.</span></span>

    ![Analytics 查詢設定畫面](./media/automate-with-logic-apps/flow4.png)

### <a name="step-6-configure-hello-logic-app-toosend-email"></a><span data-ttu-id="cd5ca-143">步驟 6： 設定 hello 邏輯應用程式 toosend 電子郵件</span><span class="sxs-lookup"><span data-stu-id="cd5ca-143">Step 6: Configure hello logic app toosend email</span></span>

1. <span data-ttu-id="cd5ca-144">按一下 [新增步驟]，然後選取 [新增動作]。</span><span class="sxs-lookup"><span data-stu-id="cd5ca-144">Click **New step**, and then select **Add an action**.</span></span>

2. <span data-ttu-id="cd5ca-145">在 [hello] 搜尋方塊中，輸入**Office 365 Outlook**。</span><span class="sxs-lookup"><span data-stu-id="cd5ca-145">In hello search box, type **Office 365 Outlook**.</span></span>

3. <span data-ttu-id="cd5ca-146">按一下 [Office 365 Outlook – 傳送電子郵件]。</span><span class="sxs-lookup"><span data-stu-id="cd5ca-146">Click **Office 365 Outlook – Send an email**.</span></span>

    ![Office 365 Outlook 選項](./media/automate-with-logic-apps/flow2b.png)

4. <span data-ttu-id="cd5ca-148">在 hello**傳送電子郵件**視窗中，執行下列 hello:</span><span class="sxs-lookup"><span data-stu-id="cd5ca-148">In hello **Send an email** window, do hello following:</span></span>

   <span data-ttu-id="cd5ca-149">a.</span><span class="sxs-lookup"><span data-stu-id="cd5ca-149">a.</span></span> <span data-ttu-id="cd5ca-150">輸入 hello hello 收件者電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="cd5ca-150">Type hello email address of hello recipient.</span></span>

   <span data-ttu-id="cd5ca-151">b.</span><span class="sxs-lookup"><span data-stu-id="cd5ca-151">b.</span></span> <span data-ttu-id="cd5ca-152">輸入 hello 電子郵件的主旨。</span><span class="sxs-lookup"><span data-stu-id="cd5ca-152">Type a subject for hello email.</span></span>

   <span data-ttu-id="cd5ca-153">c.</span><span class="sxs-lookup"><span data-stu-id="cd5ca-153">c.</span></span> <span data-ttu-id="cd5ca-154">按一下任何位置中的 hello**主體**方塊，然後 hello 動態內容功能表開啟在 hello 右、 上選取**主體**。</span><span class="sxs-lookup"><span data-stu-id="cd5ca-154">Click anywhere in hello **Body** box and then, on hello dynamic content menu that opens at hello right, select **Body**.</span></span>

   <span data-ttu-id="cd5ca-155">d.</span><span class="sxs-lookup"><span data-stu-id="cd5ca-155">d.</span></span> <span data-ttu-id="cd5ca-156">按一下 [顯示進階選項]。</span><span class="sxs-lookup"><span data-stu-id="cd5ca-156">Click **Show advanced options**.</span></span>

      ![Office 365 Outlook 設定](./media/automate-with-logic-apps/flow5.png)

5. <span data-ttu-id="cd5ca-158">Hello 動態內容功能表上，hello 遵循：</span><span class="sxs-lookup"><span data-stu-id="cd5ca-158">On hello dynamic content menu, do hello following:</span></span>

    <span data-ttu-id="cd5ca-159">a.</span><span class="sxs-lookup"><span data-stu-id="cd5ca-159">a.</span></span> <span data-ttu-id="cd5ca-160">選取 [附件名稱]。</span><span class="sxs-lookup"><span data-stu-id="cd5ca-160">Select **Attachment Name**.</span></span>

    <span data-ttu-id="cd5ca-161">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="cd5ca-161">b.</span></span> <span data-ttu-id="cd5ca-162">選取 [附件內容]。</span><span class="sxs-lookup"><span data-stu-id="cd5ca-162">Select **Attachment Content**.</span></span>
    
    <span data-ttu-id="cd5ca-163">c.</span><span class="sxs-lookup"><span data-stu-id="cd5ca-163">c.</span></span> <span data-ttu-id="cd5ca-164">在 hello**是 HTML**方塊中，選取**是**。</span><span class="sxs-lookup"><span data-stu-id="cd5ca-164">In hello **Is HTML** box, select **Yes**.</span></span>

      ![Office 365 電子郵件設定畫面](./media/automate-with-logic-apps/flow7.png)

### <a name="step-7-save-and-test-your-logic-app"></a><span data-ttu-id="cd5ca-166">步驟 7：儲存並測試邏輯應用程式</span><span class="sxs-lookup"><span data-stu-id="cd5ca-166">Step 7: Save and test your logic app</span></span>
* <span data-ttu-id="cd5ca-167">按一下**儲存**toosave 您的變更。</span><span class="sxs-lookup"><span data-stu-id="cd5ca-167">Click **Save** toosave your changes.</span></span>

<span data-ttu-id="cd5ca-168">您可以等候 hello 觸發程序 toorun hello 邏輯應用程式，或您可以立即執行 hello 邏輯應用程式，方法是選取**執行**。</span><span class="sxs-lookup"><span data-stu-id="cd5ca-168">You can wait for hello trigger toorun hello logic app, or you can run hello logic app immediately by selecting **Run**.</span></span>

![邏輯應用程式建立畫面](./media/automate-with-logic-apps/step7.png)

<span data-ttu-id="cd5ca-170">邏輯應用程式執行時，您指定 hello 電子郵件清單中的 hello 收件者會收到電子郵件，看起來像 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="cd5ca-170">When your logic app runs, hello recipients you specified in hello email list will receive an email that looks like hello following:</span></span>

![邏輯應用程式電子郵件訊息](./media/automate-with-logic-apps/flow9.png)

## <a name="next-steps"></a><span data-ttu-id="cd5ca-172">後續步驟</span><span class="sxs-lookup"><span data-stu-id="cd5ca-172">Next steps</span></span>

- <span data-ttu-id="cd5ca-173">深入了解建立 [Analytics 查詢](app-insights-analytics-using.md)。</span><span class="sxs-lookup"><span data-stu-id="cd5ca-173">Learn more about creating [Analytics queries](app-insights-analytics-using.md).</span></span>
- <span data-ttu-id="cd5ca-174">深入了解 [Logic Apps](https://docs.microsoft.com/azure/logic-apps/logic-apps-what-are-logic-apps)。</span><span class="sxs-lookup"><span data-stu-id="cd5ca-174">Learn more about [Logic Apps](https://docs.microsoft.com/azure/logic-apps/logic-apps-what-are-logic-apps).</span></span>



<!--Link references-->





