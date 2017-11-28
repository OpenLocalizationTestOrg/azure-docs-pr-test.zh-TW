---
title: "案例 - 使用 Azure 無伺服器建立客戶深入解析儀表板 | Microsoft Docs"
description: "舉例說明如何使用 Azure Logic Apps 與 Azure Functions 來建置儀表板，以管理客戶的意見反應、社交資料和其他項目。"
keywords: 
services: logic-apps
author: jeffhollan
manager: anneta
editor: 
documentationcenter: 
ms.assetid: d565873c-6b1b-4057-9250-cf81a96180ae
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/29/2017
ms.author: jehollan
ms.openlocfilehash: 0b6e118cb13ab8185d8eeb42bec6147155967967
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-real-time-customer-insights-dashboard-with-azure-logic-apps-and-azure-functions"></a><span data-ttu-id="7d433-103">使用 Azure Logic Apps 與 Azure Functions 來建立即時的客戶深入解析儀表板</span><span class="sxs-lookup"><span data-stu-id="7d433-103">Create a real-time customer insights dashboard with Azure Logic Apps and Azure Functions</span></span>

<span data-ttu-id="7d433-104">Azure 無伺服器工具提供了強大的功能，可在雲端中快速建置及裝載應用程式，而不必考慮基礎結構。</span><span class="sxs-lookup"><span data-stu-id="7d433-104">Azure Serverless tools provide powerful capabilities to quickly build and host applications in the cloud, without having to think about infrastructure.</span></span>  <span data-ttu-id="7d433-105">在此案例中，我們將建立會對客戶的意見反應而觸發的儀表板、使用機器學習服務分析意見反應，並為深入解析發佈來源，例如 Power BI 或 Azure Data Lake。</span><span class="sxs-lookup"><span data-stu-id="7d433-105">In this scenario, we will create a dashboard to trigger on customer feedback, analyze feedback with machine learning, and publish insights a source like Power BI or Azure Data Lake.</span></span>

## <a name="overview-of-the-scenario-and-tools-used"></a><span data-ttu-id="7d433-106">所用案例和工具的概觀</span><span class="sxs-lookup"><span data-stu-id="7d433-106">Overview of the scenario and tools used</span></span>

<span data-ttu-id="7d433-107">為了實作此解決方案，我們會在 Azure 中利用無伺服器應用程式的兩個重要元件︰[Azure Functions](https://azure.microsoft.com/services/functions/) 和 [Azure Logic Apps](https://azure.microsoft.com/services/logic-apps/)。</span><span class="sxs-lookup"><span data-stu-id="7d433-107">In order to implement this solution, we will leverage the two key components of serverless apps in Azure: [Azure Functions](https://azure.microsoft.com/services/functions/) and [Azure Logic Apps](https://azure.microsoft.com/services/logic-apps/).</span></span>

<span data-ttu-id="7d433-108">Logic Apps 是雲端中的無伺服器工作流程引擎。</span><span class="sxs-lookup"><span data-stu-id="7d433-108">Logic Apps is a serverless workflow engine in the cloud.</span></span>  <span data-ttu-id="7d433-109">它可跨無伺服器元件提供協調流程，而且也會連線到超過 100 個服務和 API。</span><span class="sxs-lookup"><span data-stu-id="7d433-109">It provides orchestration across serverless components, and also connects to over 100 services and APIs.</span></span>  <span data-ttu-id="7d433-110">在此案例中，我們會建立針對客戶的意見反映而觸發的邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="7d433-110">For this scenario, we will create a logic app to trigger on feedback from customers.</span></span>  <span data-ttu-id="7d433-111">某些連接器有助於回應客戶的意見反應，這些連接器包括 Outlook.com、Office 365、Survey Monkey、Twitter 和[來自 Web 表單](https://blogs.msdn.microsoft.com/logicapps/2017/01/30/calling-a-logic-app-from-an-html-form/)的 HTTP 要求。</span><span class="sxs-lookup"><span data-stu-id="7d433-111">Some of the connectors that can assist in reacting to customer feedback include Outlook.com, Office 365, Survey Monkey, Twitter, and an HTTP Request [from a web form](https://blogs.msdn.microsoft.com/logicapps/2017/01/30/calling-a-logic-app-from-an-html-form/).</span></span>  <span data-ttu-id="7d433-112">針對下面的工作流程，我們會監視 Twitter 上的主題標籤。</span><span class="sxs-lookup"><span data-stu-id="7d433-112">For the workflow below, we will monitor a hashtag on Twitter.</span></span>

<span data-ttu-id="7d433-113">函式可在雲端中提供無伺服器計算。</span><span class="sxs-lookup"><span data-stu-id="7d433-113">Functions provide serverless compute in the cloud.</span></span>  <span data-ttu-id="7d433-114">在此案例中，我們會使用 Azure Functions 來根據一系列的預先定義關鍵字，為客戶所發的推文加上旗標。</span><span class="sxs-lookup"><span data-stu-id="7d433-114">In this scenario, we will use Azure Functions to flag tweets from customers based on a series of pre-defined key words.</span></span>

<span data-ttu-id="7d433-115">整個解決方案可以[建置在 Visual Studio 中](logic-apps-deploy-from-vs.md)，也可[部署為資源範本的一部分](logic-apps-create-deploy-template.md)。</span><span class="sxs-lookup"><span data-stu-id="7d433-115">The entire solution can be [build in Visual Studio](logic-apps-deploy-from-vs.md) and [deployed as part of a resource template](logic-apps-create-deploy-template.md).</span></span>  <span data-ttu-id="7d433-116">另外，[Channel 9 上](http://aka.ms/logicappsdemo)還有影片來逐步解說此案例。</span><span class="sxs-lookup"><span data-stu-id="7d433-116">There is also video walkthrough of the scenario [on Channel 9](http://aka.ms/logicappsdemo).</span></span>

## <a name="build-the-logic-app-to-trigger-on-customer-data"></a><span data-ttu-id="7d433-117">建置會針對客戶資料觸發的邏輯應用程式</span><span class="sxs-lookup"><span data-stu-id="7d433-117">Build the logic app to trigger on customer data</span></span>

<span data-ttu-id="7d433-118">在 Visual Studio 或 Azure 入口網站中[建立邏輯應用程式](logic-apps-create-a-logic-app.md)之後︰</span><span class="sxs-lookup"><span data-stu-id="7d433-118">After [creating a logic app](logic-apps-create-a-logic-app.md) in Visual Studio or the Azure portal:</span></span>

1. <span data-ttu-id="7d433-119">針對來自 Twitter 的**新推文**新增觸發程序</span><span class="sxs-lookup"><span data-stu-id="7d433-119">Add a trigger for **On New Tweets** from Twitter</span></span>
2. <span data-ttu-id="7d433-120">設定觸發程序來接聽推文上的關鍵字或主題標籤。</span><span class="sxs-lookup"><span data-stu-id="7d433-120">Configure the trigger to listen to tweets on a keyword or hashtag.</span></span>

   > [!NOTE]
   > <span data-ttu-id="7d433-121">觸發程序的循環屬性會決定邏輯應用程式檢查輪詢式觸發程序上是否有新項目的頻率</span><span class="sxs-lookup"><span data-stu-id="7d433-121">The recurrence property on the trigger will determine how frequently the logic app checks for new items on polling-based triggers</span></span>

   ![Twitter 觸發程序的範例][1]

<span data-ttu-id="7d433-123">此應用程式現在會針對所有新推文引發。</span><span class="sxs-lookup"><span data-stu-id="7d433-123">This app will now fire on all new tweets.</span></span>  <span data-ttu-id="7d433-124">然後，我們可以取得該推文資料，並了解其中所表達的更多情緒。</span><span class="sxs-lookup"><span data-stu-id="7d433-124">We can then take that tweet data and understand more of the sentiment expressed.</span></span>  <span data-ttu-id="7d433-125">為此，我們使用 [Azure 辨識服務](https://azure.microsoft.com/services/cognitive-services/)來偵測文字的情緒。</span><span class="sxs-lookup"><span data-stu-id="7d433-125">For this we use the [Azure Cognitive Service](https://azure.microsoft.com/services/cognitive-services/) to detect sentiment of text.</span></span>

1. <span data-ttu-id="7d433-126">按一下 [新步驟]</span><span class="sxs-lookup"><span data-stu-id="7d433-126">Click **New Step**</span></span>
1. <span data-ttu-id="7d433-127">選取或搜尋 [文字分析] 連接器</span><span class="sxs-lookup"><span data-stu-id="7d433-127">Select or search for the **Text Analytics** connector</span></span>
1. <span data-ttu-id="7d433-128">選取 [偵測情緒] 作業</span><span class="sxs-lookup"><span data-stu-id="7d433-128">Select the **Detect Sentiment** operation</span></span>
1. <span data-ttu-id="7d433-129">如果出現提示，請提供適用於文字分析服務的有效辨識服務金鑰</span><span class="sxs-lookup"><span data-stu-id="7d433-129">If prompted, provide a valid Cognitive Services key for the Text Analytics service</span></span>
1. <span data-ttu-id="7d433-130">新增 [推文文字] 作為要分析的文字。</span><span class="sxs-lookup"><span data-stu-id="7d433-130">Add the **Tweet Text** as the text to analyze.</span></span>

<span data-ttu-id="7d433-131">現在，我們已有推文資料和有關推文的深入解析，因此可能會有其他許多相關的連接器︰</span><span class="sxs-lookup"><span data-stu-id="7d433-131">Now that we have the tweet data, and insights on the tweet, a number of other connectors may be relevant:</span></span>
* <span data-ttu-id="7d433-132">Power BI - 新增資料列到串流資料集︰在 Power BI 儀表板上檢視即時推文。</span><span class="sxs-lookup"><span data-stu-id="7d433-132">Power BI - Add Rows to Streaming Dataset: View tweets real time on a Power BI dashboard.</span></span>
* <span data-ttu-id="7d433-133">Azure Data Lake - 附加檔案︰將客戶資料新增至要納入分析作業的 Azure Data Lake 資料集。</span><span class="sxs-lookup"><span data-stu-id="7d433-133">Azure Data Lake - Append file: Add customer data to an Azure Data Lake dataset to include in analytics jobs.</span></span>
* <span data-ttu-id="7d433-134">SQL - 新增資料列︰將資料儲存在資料庫中，以供日後擷取。</span><span class="sxs-lookup"><span data-stu-id="7d433-134">SQL - Add rows: Store data in a database for later retrieval.</span></span>
* <span data-ttu-id="7d433-135">Slack - 傳送訊息︰針對需要有所行動的負面意見反應在 Slack 通道上發出警示。</span><span class="sxs-lookup"><span data-stu-id="7d433-135">Slack - Send message: Alert a slack channel on negative feedback that requires actions.</span></span>

<span data-ttu-id="7d433-136">Azure Function 也可用來根據資料執行更多的自訂計算。</span><span class="sxs-lookup"><span data-stu-id="7d433-136">An Azure Function can also be used to do more custom compute on top of the data.</span></span>

## <a name="enriching-the-data-with-an-azure-function"></a><span data-ttu-id="7d433-137">使用 Azure Function 來豐富資料</span><span class="sxs-lookup"><span data-stu-id="7d433-137">Enriching the data with an Azure Function</span></span>

<span data-ttu-id="7d433-138">在建立函式之前，我們必須先在 Azure 訂用帳戶中擁有函式應用程式。</span><span class="sxs-lookup"><span data-stu-id="7d433-138">Before we can create a function, we need to have a function app in our Azure subscription.</span></span>  <span data-ttu-id="7d433-139">您可以[在這裡找到](../azure-functions/functions-create-first-azure-function-azure-portal.md)有關在入口網站中建立 Azure Function 的詳細資料</span><span class="sxs-lookup"><span data-stu-id="7d433-139">Details on creating an Azure Function in the portal can [be found here](../azure-functions/functions-create-first-azure-function-azure-portal.md)</span></span>

<span data-ttu-id="7d433-140">函式若要能夠直接從邏輯應用程式中呼叫，就必須有 HTTP 繫結觸發程序。</span><span class="sxs-lookup"><span data-stu-id="7d433-140">For a function to be called directly from a logic app, it needs to have an HTTP trigger binding.</span></span>  <span data-ttu-id="7d433-141">我們建議使用 **HttpTrigger** 範本。</span><span class="sxs-lookup"><span data-stu-id="7d433-141">We recommend using the **HttpTrigger** template.</span></span>

<span data-ttu-id="7d433-142">在此案例中，Azure Function 的要求本文會是推文文字。</span><span class="sxs-lookup"><span data-stu-id="7d433-142">In this scenario, the request body of the Azure Function would be the tweet text.</span></span>  <span data-ttu-id="7d433-143">在函式程式碼中，只需定義關於推文文字是包含關鍵字還是片語的邏輯。</span><span class="sxs-lookup"><span data-stu-id="7d433-143">In the function code, simply define logic on if the tweet text contains a key word or phrase.</span></span>  <span data-ttu-id="7d433-144">函式本身可視案例所需而保持簡單或複雜。</span><span class="sxs-lookup"><span data-stu-id="7d433-144">The function itself could be kept as simple or complex as needed for the scenario.</span></span>

<span data-ttu-id="7d433-145">在函式結束時，只需對邏輯應用程式傳回含有一些資料的回應。</span><span class="sxs-lookup"><span data-stu-id="7d433-145">At the end of the function, simply return a response to the logic app with some data.</span></span>  <span data-ttu-id="7d433-146">這可能是簡單的布林值 (例如 `containsKeyword`) 或複雜的物件。</span><span class="sxs-lookup"><span data-stu-id="7d433-146">This could be a simple boolean value (e.g. `containsKeyword`), or a complex object.</span></span>

![已設定的 Azure Function 步驟][2]

> [!TIP]
> <span data-ttu-id="7d433-148">在存取邏輯應用程式函式中的複雜回應時，請使用剖析 JSON 動作。</span><span class="sxs-lookup"><span data-stu-id="7d433-148">When accessing a complex response from a function in a logic app, use the Parse JSON action.</span></span>

<span data-ttu-id="7d433-149">函式儲存後，就能新增至先前建立的邏輯應用程式中。</span><span class="sxs-lookup"><span data-stu-id="7d433-149">Once the function is saved, it can be added into the logic app created above.</span></span>  <span data-ttu-id="7d433-150">在邏輯應用程式中：</span><span class="sxs-lookup"><span data-stu-id="7d433-150">In the logic app:</span></span>

1. <span data-ttu-id="7d433-151">按一下以新增 [新步驟]</span><span class="sxs-lookup"><span data-stu-id="7d433-151">Click to add a **New Step**</span></span>
1. <span data-ttu-id="7d433-152">選取 [Azure Functions] 連接器</span><span class="sxs-lookup"><span data-stu-id="7d433-152">Select the **Azure Functions** connector</span></span>
1. <span data-ttu-id="7d433-153">選取要選擇現有函式，並瀏覽至所建立的函式</span><span class="sxs-lookup"><span data-stu-id="7d433-153">Select to choose an existing function, and browse to the function created</span></span>
1. <span data-ttu-id="7d433-154">為**要求本文**傳入**推文文字**</span><span class="sxs-lookup"><span data-stu-id="7d433-154">Send in the **Tweet Text** for the **Request Body**</span></span>

## <a name="running-and-monitoring-the-solution"></a><span data-ttu-id="7d433-155">執行和監控解決方案</span><span class="sxs-lookup"><span data-stu-id="7d433-155">Running and monitoring the solution</span></span>

<span data-ttu-id="7d433-156">在 Logic Apps 中撰寫無伺服器協調流程的優點之一是其擁有豐富的偵錯和監控功能。</span><span class="sxs-lookup"><span data-stu-id="7d433-156">One of the benefits of authoring serverless orchestrations in Logic Apps is the rich debug and monitoring capabilities.</span></span>  <span data-ttu-id="7d433-157">任何執行 (目前或過去的) 皆可從 Visual Studio 內、Azure 入口網站或透過 REST API 和 SDK 來檢視。</span><span class="sxs-lookup"><span data-stu-id="7d433-157">Any run (current or historic) can be viewed from within Visual Studio, the Azure portal, or via the REST API and SDKs.</span></span>

<span data-ttu-id="7d433-158">若要測試邏輯應用程式，其中一個最簡單的方法是使用設計工具中的 [執行] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="7d433-158">One of the easiest ways to test a logic app is using the **Run** button in the designer.</span></span>  <span data-ttu-id="7d433-159">按一下 [執行] 就會繼續每隔 5 秒輪詢觸發程序一次直到偵測到事件，並在執行進行時提供即時檢視。</span><span class="sxs-lookup"><span data-stu-id="7d433-159">Clicking **Run** will continue to poll the trigger every 5 seconds until an event is detected, and give a live view as the run progresses.</span></span>

<span data-ttu-id="7d433-160">先前執行的歷程記錄可在 Azure 入口網站中的 [概觀] 刀鋒視窗上檢視，或使用 Visual Studio Cloud Explorer 來檢視。</span><span class="sxs-lookup"><span data-stu-id="7d433-160">Previous run histories can be viewed on the Overview blade in the Azure portal, or using the Visual Studio Cloud Explorer.</span></span>

## <a name="creating-a-deployment-template-for-automated-deployments"></a><span data-ttu-id="7d433-161">建立部署範本來進行自動化部署</span><span class="sxs-lookup"><span data-stu-id="7d433-161">Creating a deployment template for automated deployments</span></span>

<span data-ttu-id="7d433-162">解決方案開發成功後，就能透過 Azure 部署範本加以擷取並部署到世界上的任何 Azure 區域。</span><span class="sxs-lookup"><span data-stu-id="7d433-162">Once a solution has been developed, it can be captured and deployed via an Azure deployment template to any Azure region in the world.</span></span>  <span data-ttu-id="7d433-163">這不僅適用於修改參數以獲得此工作流程的不同版本，也適用於在建置和發行管線中整合此解決方案。</span><span class="sxs-lookup"><span data-stu-id="7d433-163">This is useful for both modifying parameters for different versions of this workflow, but also for integrating this solution in a build and release pipeline.</span></span>  <span data-ttu-id="7d433-164">關於建立部署範本的詳細資料可以[在此文章中](logic-apps-create-deploy-template.md)找到。</span><span class="sxs-lookup"><span data-stu-id="7d433-164">Details on creating a deployment template can be found [in this article](logic-apps-create-deploy-template.md).</span></span>

<span data-ttu-id="7d433-165">Azure Functions 也可納入部署範本中，因此，您可以將整個解決方案與所有相依性當作單一範本來管理。</span><span class="sxs-lookup"><span data-stu-id="7d433-165">Azure Functions can also be incorporated in the deployment template - so the entire solution with all dependencies can be managed as a single template.</span></span>  <span data-ttu-id="7d433-166">函式部署範本的範例可在 [Azure 快速入門範本儲存機制](https://github.com/Azure/azure-quickstart-templates/tree/master/101-function-app-create-dynamic)中找到。</span><span class="sxs-lookup"><span data-stu-id="7d433-166">An example of a function deployment template can be found in the [Azure quickstart template repository](https://github.com/Azure/azure-quickstart-templates/tree/master/101-function-app-create-dynamic).</span></span>

## <a name="next-steps"></a><span data-ttu-id="7d433-167">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7d433-167">Next steps</span></span>

* [<span data-ttu-id="7d433-168">查看 Azure Logic Apps 的其他範例和案例</span><span class="sxs-lookup"><span data-stu-id="7d433-168">See other examples and scenarios for Azure Logic Apps</span></span>](logic-apps-examples-and-scenarios.md)
* [<span data-ttu-id="7d433-169">觀看關於完整建立此解決方案的影片逐步解說</span><span class="sxs-lookup"><span data-stu-id="7d433-169">Watch a video walkthrough on creating this solution end-to-end</span></span>](http://aka.ms/logicappsdemo)
* [<span data-ttu-id="7d433-170">了解如何在邏輯應用程式內處理和攔截例外狀況</span><span class="sxs-lookup"><span data-stu-id="7d433-170">Learn how to handle and catch exceptions within a logic app</span></span>](logic-apps-exception-handling.md)

<!-- Image References -->
[1]: ./media/logic-apps-scenario-social-serverless/twitter.png
[2]: ./media/logic-apps-scenario-social-serverless/function.png