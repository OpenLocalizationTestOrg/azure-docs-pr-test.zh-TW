---
title: "aaaScenario-使用 Azure 無伺服器建立客戶 insights 儀表板 |Microsoft 文件"
description: "如何建置儀表板 toomanage 客戶，意見反應、 社交資料，以及更多 Azure 邏輯應用程式與 Azure 函式的範例。"
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
ms.openlocfilehash: db175e895e37aa795a9c34bf4d65566bf68f8c37
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-real-time-customer-insights-dashboard-with-azure-logic-apps-and-azure-functions"></a><span data-ttu-id="a57a1-103">使用 Azure Logic Apps 與 Azure Functions 來建立即時的客戶深入解析儀表板</span><span class="sxs-lookup"><span data-stu-id="a57a1-103">Create a real-time customer insights dashboard with Azure Logic Apps and Azure Functions</span></span>

<span data-ttu-id="a57a1-104">Azure 的無伺服器工具提供強大的功能 tooquickly hello 雲端中的建置和裝載應用程式而不需要 toothink 相關基礎結構。</span><span class="sxs-lookup"><span data-stu-id="a57a1-104">Azure Serverless tools provide powerful capabilities tooquickly build and host applications in hello cloud, without having toothink about infrastructure.</span></span>  <span data-ttu-id="a57a1-105">在此案例中，我們將客戶的意見反應上建立儀表板 tootrigger、 分析使用機器學習和發行 insights 像 Power BI 或 Azure 資料湖來源。</span><span class="sxs-lookup"><span data-stu-id="a57a1-105">In this scenario, we will create a dashboard tootrigger on customer feedback, analyze feedback with machine learning, and publish insights a source like Power BI or Azure Data Lake.</span></span>

## <a name="overview-of-hello-scenario-and-tools-used"></a><span data-ttu-id="a57a1-106">Hello 案例及使用工具的概觀</span><span class="sxs-lookup"><span data-stu-id="a57a1-106">Overview of hello scenario and tools used</span></span>

<span data-ttu-id="a57a1-107">在排序 tooimplement 此解決方案中，我們將利用的無伺服器的應用程式在 Azure 中的 hello 兩個主要元件： [Azure 函式](https://azure.microsoft.com/services/functions/)和[Azure Logic Apps](https://azure.microsoft.com/services/logic-apps/)。</span><span class="sxs-lookup"><span data-stu-id="a57a1-107">In order tooimplement this solution, we will leverage hello two key components of serverless apps in Azure: [Azure Functions](https://azure.microsoft.com/services/functions/) and [Azure Logic Apps](https://azure.microsoft.com/services/logic-apps/).</span></span>

<span data-ttu-id="a57a1-108">邏輯應用程式是無伺服器的工作流程引擎 hello 雲端中。</span><span class="sxs-lookup"><span data-stu-id="a57a1-108">Logic Apps is a serverless workflow engine in hello cloud.</span></span>  <span data-ttu-id="a57a1-109">它提供無伺服器的元件之間的協調流程，並且也會連接 tooover 100 個服務和應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="a57a1-109">It provides orchestration across serverless components, and also connects tooover 100 services and APIs.</span></span>  <span data-ttu-id="a57a1-110">此案例中，我們將建立邏輯應用程式 tootrigger 來自客戶的意見反應。</span><span class="sxs-lookup"><span data-stu-id="a57a1-110">For this scenario, we will create a logic app tootrigger on feedback from customers.</span></span>  <span data-ttu-id="a57a1-111">對回應 toocustomer 意見反應可協助 hello 連接器包括 Outlook.com、 Office 365、 問卷猴子、 Twitter 和 HTTP 要求[從 web 表單](https://blogs.msdn.microsoft.com/logicapps/2017/01/30/calling-a-logic-app-from-an-html-form/)。</span><span class="sxs-lookup"><span data-stu-id="a57a1-111">Some of hello connectors that can assist in reacting toocustomer feedback include Outlook.com, Office 365, Survey Monkey, Twitter, and an HTTP Request [from a web form](https://blogs.msdn.microsoft.com/logicapps/2017/01/30/calling-a-logic-app-from-an-html-form/).</span></span>  <span data-ttu-id="a57a1-112">如下列的 hello 工作流程，我們會監視在 Twitter 上的說明。</span><span class="sxs-lookup"><span data-stu-id="a57a1-112">For hello workflow below, we will monitor a hashtag on Twitter.</span></span>

<span data-ttu-id="a57a1-113">函式提供無伺服器 hello 雲端中的計算。</span><span class="sxs-lookup"><span data-stu-id="a57a1-113">Functions provide serverless compute in hello cloud.</span></span>  <span data-ttu-id="a57a1-114">在此案例中，我們將使用來自客戶的一系列預先定義的索引鍵文字為基礎的 Azure 函式 tooflag 推文。</span><span class="sxs-lookup"><span data-stu-id="a57a1-114">In this scenario, we will use Azure Functions tooflag tweets from customers based on a series of pre-defined key words.</span></span>

<span data-ttu-id="a57a1-115">hello 整個方案可以是[Visual Studio 中建置](logic-apps-deploy-from-vs.md)和[做為資源範本的一部分部署](logic-apps-create-deploy-template.md)。</span><span class="sxs-lookup"><span data-stu-id="a57a1-115">hello entire solution can be [build in Visual Studio](logic-apps-deploy-from-vs.md) and [deployed as part of a resource template](logic-apps-create-deploy-template.md).</span></span>  <span data-ttu-id="a57a1-116">另外還有 hello 案例的視訊逐步解說[Channel 9 上](http://aka.ms/logicappsdemo)。</span><span class="sxs-lookup"><span data-stu-id="a57a1-116">There is also video walkthrough of hello scenario [on Channel 9](http://aka.ms/logicappsdemo).</span></span>

## <a name="build-hello-logic-app-tootrigger-on-customer-data"></a><span data-ttu-id="a57a1-117">Hello 邏輯應用程式 tootrigger 根據客戶資料</span><span class="sxs-lookup"><span data-stu-id="a57a1-117">Build hello logic app tootrigger on customer data</span></span>

<span data-ttu-id="a57a1-118">之後[建立邏輯應用程式](logic-apps-create-a-logic-app.md)在 Visual Studio 或 hello Azure 入口網站：</span><span class="sxs-lookup"><span data-stu-id="a57a1-118">After [creating a logic app](logic-apps-create-a-logic-app.md) in Visual Studio or hello Azure portal:</span></span>

1. <span data-ttu-id="a57a1-119">針對來自 Twitter 的**新推文**新增觸發程序</span><span class="sxs-lookup"><span data-stu-id="a57a1-119">Add a trigger for **On New Tweets** from Twitter</span></span>
2. <span data-ttu-id="a57a1-120">設定 hello 觸發程序 toolisten tootweets 關鍵字或雜湊標記上。</span><span class="sxs-lookup"><span data-stu-id="a57a1-120">Configure hello trigger toolisten tootweets on a keyword or hashtag.</span></span>

   > [!NOTE]
   > <span data-ttu-id="a57a1-121">hello 的觸發程序的 hello 循環屬性將決定 hello 邏輯應用程式檢查新的項目，以輪詢為基礎的觸發程序的頻率</span><span class="sxs-lookup"><span data-stu-id="a57a1-121">hello recurrence property on hello trigger will determine how frequently hello logic app checks for new items on polling-based triggers</span></span>

   ![Twitter 觸發程序的範例][1]

<span data-ttu-id="a57a1-123">此應用程式現在會針對所有新推文引發。</span><span class="sxs-lookup"><span data-stu-id="a57a1-123">This app will now fire on all new tweets.</span></span>  <span data-ttu-id="a57a1-124">我們可以採取該推文中的資料，並了解多個表示 hello 人氣。</span><span class="sxs-lookup"><span data-stu-id="a57a1-124">We can then take that tweet data and understand more of hello sentiment expressed.</span></span>  <span data-ttu-id="a57a1-125">為此，我們使用 hello [Azure 認知服務](https://azure.microsoft.com/services/cognitive-services/)toodetect 人氣的文字。</span><span class="sxs-lookup"><span data-stu-id="a57a1-125">For this we use hello [Azure Cognitive Service](https://azure.microsoft.com/services/cognitive-services/) toodetect sentiment of text.</span></span>

1. <span data-ttu-id="a57a1-126">按一下 [新步驟]</span><span class="sxs-lookup"><span data-stu-id="a57a1-126">Click **New Step**</span></span>
1. <span data-ttu-id="a57a1-127">選取或搜尋 hello**文字分析**連接器</span><span class="sxs-lookup"><span data-stu-id="a57a1-127">Select or search for hello **Text Analytics** connector</span></span>
1. <span data-ttu-id="a57a1-128">選取 hello**偵測人氣**作業</span><span class="sxs-lookup"><span data-stu-id="a57a1-128">Select hello **Detect Sentiment** operation</span></span>
1. <span data-ttu-id="a57a1-129">如果出現提示，請提供有效的認知的服務金鑰的 hello 文字分析服務</span><span class="sxs-lookup"><span data-stu-id="a57a1-129">If prompted, provide a valid Cognitive Services key for hello Text Analytics service</span></span>
1. <span data-ttu-id="a57a1-130">新增 hello**推文文字**hello 文字 tooanalyze 如下。</span><span class="sxs-lookup"><span data-stu-id="a57a1-130">Add hello **Tweet Text** as hello text tooanalyze.</span></span>

<span data-ttu-id="a57a1-131">現在，我們已經 hello 推文中的資料和 insights hello 推文上時，可能相關的其他連接器的數字：</span><span class="sxs-lookup"><span data-stu-id="a57a1-131">Now that we have hello tweet data, and insights on hello tweet, a number of other connectors may be relevant:</span></span>
* <span data-ttu-id="a57a1-132">Power BI-加入資料集的資料列 tooStreaming: Power BI 儀表板上的即時檢視排行推文。</span><span class="sxs-lookup"><span data-stu-id="a57a1-132">Power BI - Add Rows tooStreaming Dataset: View tweets real time on a Power BI dashboard.</span></span>
* <span data-ttu-id="a57a1-133">Azure Data Lake 的附加檔案： 將客戶資料 tooan Azure 資料湖資料集 tooinclude 加入在分析工作。</span><span class="sxs-lookup"><span data-stu-id="a57a1-133">Azure Data Lake - Append file: Add customer data tooan Azure Data Lake dataset tooinclude in analytics jobs.</span></span>
* <span data-ttu-id="a57a1-134">SQL - 新增資料列︰將資料儲存在資料庫中，以供日後擷取。</span><span class="sxs-lookup"><span data-stu-id="a57a1-134">SQL - Add rows: Store data in a database for later retrieval.</span></span>
* <span data-ttu-id="a57a1-135">Slack - 傳送訊息︰針對需要有所行動的負面意見反應在 Slack 通道上發出警示。</span><span class="sxs-lookup"><span data-stu-id="a57a1-135">Slack - Send message: Alert a slack channel on negative feedback that requires actions.</span></span>

<span data-ttu-id="a57a1-136">Azure 函式也可以使用的 toodo 需自訂計算 hello 中的資料之上。</span><span class="sxs-lookup"><span data-stu-id="a57a1-136">An Azure Function can also be used toodo more custom compute on top of hello data.</span></span>

## <a name="enriching-hello-data-with-an-azure-function"></a><span data-ttu-id="a57a1-137">充實 hello 資料與 Azure 函式</span><span class="sxs-lookup"><span data-stu-id="a57a1-137">Enriching hello data with an Azure Function</span></span>

<span data-ttu-id="a57a1-138">我們可以建立函式之前，我們將在我們的 Azure 訂用帳戶中需要 toohave 函式應用程式。</span><span class="sxs-lookup"><span data-stu-id="a57a1-138">Before we can create a function, we need toohave a function app in our Azure subscription.</span></span>  <span data-ttu-id="a57a1-139">Hello 入口網站中建立 Azure 函式的詳細資訊可以[在這裡找到](../azure-functions/functions-create-first-azure-function-azure-portal.md)</span><span class="sxs-lookup"><span data-stu-id="a57a1-139">Details on creating an Azure Function in hello portal can [be found here](../azure-functions/functions-create-first-azure-function-azure-portal.md)</span></span>

<span data-ttu-id="a57a1-140">針對直接從邏輯應用程式呼叫函式 toobe，就需要 toohave HTTP 觸發繫結。</span><span class="sxs-lookup"><span data-stu-id="a57a1-140">For a function toobe called directly from a logic app, it needs toohave an HTTP trigger binding.</span></span>  <span data-ttu-id="a57a1-141">我們建議您使用 hello **HttpTrigger**範本。</span><span class="sxs-lookup"><span data-stu-id="a57a1-141">We recommend using hello **HttpTrigger** template.</span></span>

<span data-ttu-id="a57a1-142">在此案例中，hello 要求主體的 hello Azure 函式會推文中的 hello 文字。</span><span class="sxs-lookup"><span data-stu-id="a57a1-142">In this scenario, hello request body of hello Azure Function would be hello tweet text.</span></span>  <span data-ttu-id="a57a1-143">在 hello 函式程式碼，只是邏輯上定義如果推文中的 hello 文字包含關鍵字或片語。</span><span class="sxs-lookup"><span data-stu-id="a57a1-143">In hello function code, simply define logic on if hello tweet text contains a key word or phrase.</span></span>  <span data-ttu-id="a57a1-144">為簡單或複雜視 hello 案例中，無法保留 hello 函式本身。</span><span class="sxs-lookup"><span data-stu-id="a57a1-144">hello function itself could be kept as simple or complex as needed for hello scenario.</span></span>

<span data-ttu-id="a57a1-145">在 hello hello 函式結尾，就只會傳回回應 toohello 邏輯應用程式的某些資料。</span><span class="sxs-lookup"><span data-stu-id="a57a1-145">At hello end of hello function, simply return a response toohello logic app with some data.</span></span>  <span data-ttu-id="a57a1-146">這可能是簡單的布林值 (例如 `containsKeyword`) 或複雜的物件。</span><span class="sxs-lookup"><span data-stu-id="a57a1-146">This could be a simple boolean value (e.g. `containsKeyword`), or a complex object.</span></span>

![已設定的 Azure Function 步驟][2]

> [!TIP]
> <span data-ttu-id="a57a1-148">當從邏輯應用程式中的函式中存取複雜的回應，請使用 hello 剖析 JSON 動作。</span><span class="sxs-lookup"><span data-stu-id="a57a1-148">When accessing a complex response from a function in a logic app, use hello Parse JSON action.</span></span>

<span data-ttu-id="a57a1-149">Hello 函式儲存之後，它會加入到上面所建立的 hello 邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="a57a1-149">Once hello function is saved, it can be added into hello logic app created above.</span></span>  <span data-ttu-id="a57a1-150">在 hello 邏輯應用程式：</span><span class="sxs-lookup"><span data-stu-id="a57a1-150">In hello logic app:</span></span>

1. <span data-ttu-id="a57a1-151">按一下 tooadd**新步驟**</span><span class="sxs-lookup"><span data-stu-id="a57a1-151">Click tooadd a **New Step**</span></span>
1. <span data-ttu-id="a57a1-152">選取 hello **Azure 函式**連接器</span><span class="sxs-lookup"><span data-stu-id="a57a1-152">Select hello **Azure Functions** connector</span></span>
1. <span data-ttu-id="a57a1-153">選取 toochoose 現有的函式，並瀏覽所建立的 toohello 函式</span><span class="sxs-lookup"><span data-stu-id="a57a1-153">Select toochoose an existing function, and browse toohello function created</span></span>
1. <span data-ttu-id="a57a1-154">傳送嗨**推文文字**hello**要求本文**</span><span class="sxs-lookup"><span data-stu-id="a57a1-154">Send in hello **Tweet Text** for hello **Request Body**</span></span>

## <a name="running-and-monitoring-hello-solution"></a><span data-ttu-id="a57a1-155">執行且監視 hello 方案</span><span class="sxs-lookup"><span data-stu-id="a57a1-155">Running and monitoring hello solution</span></span>

<span data-ttu-id="a57a1-156">撰寫無伺服器的協調流程中的 Logic Apps hello 優點的其中一個是 hello 豐富的偵錯和監視功能。</span><span class="sxs-lookup"><span data-stu-id="a57a1-156">One of hello benefits of authoring serverless orchestrations in Logic Apps is hello rich debug and monitoring capabilities.</span></span>  <span data-ttu-id="a57a1-157">在 Visual Studio 中，hello Azure 入口網站，或透過 hello REST API 和 Sdk，可以從檢視任何執行 （目前或歷程記錄）。</span><span class="sxs-lookup"><span data-stu-id="a57a1-157">Any run (current or historic) can be viewed from within Visual Studio, hello Azure portal, or via hello REST API and SDKs.</span></span>

<span data-ttu-id="a57a1-158">其中一個最簡單方式 tootest hello 邏輯應用程式正在使用 hello**執行**hello 設計工具中的按鈕。</span><span class="sxs-lookup"><span data-stu-id="a57a1-158">One of hello easiest ways tootest a logic app is using hello **Run** button in hello designer.</span></span>  <span data-ttu-id="a57a1-159">按一下**執行**會繼續直到偵測到事件時，每隔 5 秒 toopoll hello 觸發程序，並隨著 hello 執行提供的即時檢視。</span><span class="sxs-lookup"><span data-stu-id="a57a1-159">Clicking **Run** will continue toopoll hello trigger every 5 seconds until an event is detected, and give a live view as hello run progresses.</span></span>

<span data-ttu-id="a57a1-160">Hello Azure 入口網站，或使用 hello Visual Studio Cloud Explorer 中的 hello 概觀刀鋒視窗上，您可以檢視先前執行的記錄。</span><span class="sxs-lookup"><span data-stu-id="a57a1-160">Previous run histories can be viewed on hello Overview blade in hello Azure portal, or using hello Visual Studio Cloud Explorer.</span></span>

## <a name="creating-a-deployment-template-for-automated-deployments"></a><span data-ttu-id="a57a1-161">建立部署範本來進行自動化部署</span><span class="sxs-lookup"><span data-stu-id="a57a1-161">Creating a deployment template for automated deployments</span></span>

<span data-ttu-id="a57a1-162">一旦開發的解決方案，它可以擷取，並透過 Azure 部署範本 tooany hello 世界中的 Azure 地區部署。</span><span class="sxs-lookup"><span data-stu-id="a57a1-162">Once a solution has been developed, it can be captured and deployed via an Azure deployment template tooany Azure region in hello world.</span></span>  <span data-ttu-id="a57a1-163">這不僅適用於修改參數以獲得此工作流程的不同版本，也適用於在建置和發行管線中整合此解決方案。</span><span class="sxs-lookup"><span data-stu-id="a57a1-163">This is useful for both modifying parameters for different versions of this workflow, but also for integrating this solution in a build and release pipeline.</span></span>  <span data-ttu-id="a57a1-164">關於建立部署範本的詳細資料可以[在此文章中](logic-apps-create-deploy-template.md)找到。</span><span class="sxs-lookup"><span data-stu-id="a57a1-164">Details on creating a deployment template can be found [in this article](logic-apps-create-deploy-template.md).</span></span>

<span data-ttu-id="a57a1-165">Azure 函式也在 hello 部署範本-合併，因此可視為單一範本管理 hello 整個方案的所有相依性。</span><span class="sxs-lookup"><span data-stu-id="a57a1-165">Azure Functions can also be incorporated in hello deployment template - so hello entire solution with all dependencies can be managed as a single template.</span></span>  <span data-ttu-id="a57a1-166">函式的部署範本的範例，請參閱 hello [Azure 快速入門範本儲存機制](https://github.com/Azure/azure-quickstart-templates/tree/master/101-function-app-create-dynamic)。</span><span class="sxs-lookup"><span data-stu-id="a57a1-166">An example of a function deployment template can be found in hello [Azure quickstart template repository](https://github.com/Azure/azure-quickstart-templates/tree/master/101-function-app-create-dynamic).</span></span>

## <a name="next-steps"></a><span data-ttu-id="a57a1-167">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a57a1-167">Next steps</span></span>

* [<span data-ttu-id="a57a1-168">查看 Azure Logic Apps 的其他範例和案例</span><span class="sxs-lookup"><span data-stu-id="a57a1-168">See other examples and scenarios for Azure Logic Apps</span></span>](logic-apps-examples-and-scenarios.md)
* [<span data-ttu-id="a57a1-169">觀看關於完整建立此解決方案的影片逐步解說</span><span class="sxs-lookup"><span data-stu-id="a57a1-169">Watch a video walkthrough on creating this solution end-to-end</span></span>](http://aka.ms/logicappsdemo)
* [<span data-ttu-id="a57a1-170">深入了解如何在邏輯應用程式內 toohandle 和 catch 例外狀況</span><span class="sxs-lookup"><span data-stu-id="a57a1-170">Learn how toohandle and catch exceptions within a logic app</span></span>](logic-apps-exception-handling.md)

<!-- Image References -->
[1]: ./media/logic-apps-scenario-social-serverless/twitter.png
[2]: ./media/logic-apps-scenario-social-serverless/function.png