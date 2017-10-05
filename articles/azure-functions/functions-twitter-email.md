---
title: "建立與 Azure Logic Apps 整合的函式 | Microsoft Docs"
description: "建立可整合 Azure Logic Apps 和 Azure 辨識服務的函數，以將推文情感進行分類，並在偵測到不佳的情感時傳送通知。"
services: functions, logic-apps, cognitive-services
keywords: "工作流程, 雲端應用程式, 雲端服務, 商務程序, 系統整合, 企業應用程式整合, EAI"
documentationcenter: 
author: ggailey777
manager: erikre
editor: 
ms.assetid: 60495cc5-1638-4bf0-8174-52786d227734
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 4a5dc668e21c5328b308c8f5852aaa922232374d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-function-that-integrates-with-azure-logic-apps"></a><span data-ttu-id="0ade7-104">建立與 Azure Logic Apps 整合的函式</span><span class="sxs-lookup"><span data-stu-id="0ade7-104">Create a function that integrates with Azure Logic Apps</span></span>

<span data-ttu-id="0ade7-105">Azure Functions 與 Logic Apps 設計工具中的 Azure Logic Apps 進行整合。</span><span class="sxs-lookup"><span data-stu-id="0ade7-105">Azure Functions integrates with Azure Logic Apps in the Logic Apps Designer.</span></span> <span data-ttu-id="0ade7-106">這項整合可讓您搭配其他 Azure 和第三方服務，使用協調流程中的 Functions 計算能力。</span><span class="sxs-lookup"><span data-stu-id="0ade7-106">This integration lets you use the computing power of Functions in orchestrations with other Azure and third-party services.</span></span> 

<span data-ttu-id="0ade7-107">本教學課程說明如何使用 Functions 搭配 Logic Apps 和 Azure 辨識服務，分析來自 Twitter 貼文的情感。</span><span class="sxs-lookup"><span data-stu-id="0ade7-107">This tutorial shows you how to use Functions with Logic Apps and Azure Cognitive Services to analyze sentiment from Twitter posts.</span></span> <span data-ttu-id="0ade7-108">HTTP 觸發函式會以情感分數作為基礎，將推文分類為綠色、黃色或紅色。</span><span class="sxs-lookup"><span data-stu-id="0ade7-108">An HTTP triggered function categorizes tweets as green, yellow, or red based on the sentiment score.</span></span> <span data-ttu-id="0ade7-109">偵測到不佳的情感時，會傳送一封電子郵件。</span><span class="sxs-lookup"><span data-stu-id="0ade7-109">An email is sent when poor sentiment is detected.</span></span> 

![此映像顯示邏輯應用程式設計工具中應用程式的前兩個步驟](media/functions-twitter-email/designer1.png)

<span data-ttu-id="0ade7-111">在本教學課程中，您將了解如何：</span><span class="sxs-lookup"><span data-stu-id="0ade7-111">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="0ade7-112">建立辨識服務帳戶。</span><span class="sxs-lookup"><span data-stu-id="0ade7-112">Create a Cognitive Services account.</span></span>
> * <span data-ttu-id="0ade7-113">建立可將推文情感進行分類的函式。</span><span class="sxs-lookup"><span data-stu-id="0ade7-113">Create a function that categorizes tweet sentiment.</span></span>
> * <span data-ttu-id="0ade7-114">建立連線至 Twitter 的邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="0ade7-114">Create a logic app that connects to Twitter.</span></span>
> * <span data-ttu-id="0ade7-115">將情感偵測新增至邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="0ade7-115">Add sentiment detection to the logic app.</span></span> 
> * <span data-ttu-id="0ade7-116">將邏輯應用程式連線至函式。</span><span class="sxs-lookup"><span data-stu-id="0ade7-116">Connect the logic app to the function.</span></span>
> * <span data-ttu-id="0ade7-117">以函式的回應作為基礎來傳送電子郵件。</span><span class="sxs-lookup"><span data-stu-id="0ade7-117">Send an email based on the response from the function.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0ade7-118">必要條件</span><span class="sxs-lookup"><span data-stu-id="0ade7-118">Prerequisites</span></span>

+ <span data-ttu-id="0ade7-119">使用中的 [Twitter](https://twitter.com/) 帳戶。</span><span class="sxs-lookup"><span data-stu-id="0ade7-119">An active [Twitter](https://twitter.com/) account.</span></span> 
+ <span data-ttu-id="0ade7-120">[Outlook.com](https://outlook.com/) 帳戶 (用於傳送通知)。</span><span class="sxs-lookup"><span data-stu-id="0ade7-120">An [Outlook.com](https://outlook.com/) account (for sending notifications).</span></span>
+ <span data-ttu-id="0ade7-121">本主題使用[從 Azure 入口網站建立您的第一個函式](functions-create-first-azure-function.md)中所建立的資源作為起點。</span><span class="sxs-lookup"><span data-stu-id="0ade7-121">This topic uses as its starting point the resources created in [Create your first function from the Azure portal](functions-create-first-azure-function.md).</span></span>  
<span data-ttu-id="0ade7-122">如果您尚未這麼做，請立即完成這些步驟，才能建立函式應用程式。</span><span class="sxs-lookup"><span data-stu-id="0ade7-122">If you haven't already done so, complete these steps now to create your function app.</span></span>

## <a name="create-a-cognitive-services-account"></a><span data-ttu-id="0ade7-123">建立辨識服務帳戶</span><span class="sxs-lookup"><span data-stu-id="0ade7-123">Create a Cognitive Services account</span></span>

<span data-ttu-id="0ade7-124">需要有辨識服務帳戶，才能偵測所監視之推文的情感。</span><span class="sxs-lookup"><span data-stu-id="0ade7-124">A Cognitive Services account is required to detect the sentiment of tweets being monitored.</span></span>

1. <span data-ttu-id="0ade7-125">登入 [Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="0ade7-125">Sign in to the [Azure portal](https://portal.azure.com/).</span></span>

2. <span data-ttu-id="0ade7-126">按一下 Azure 入口網站左上角的 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="0ade7-126">Click the **New** button found on the upper left-hand corner of the Azure portal.</span></span>

3. <span data-ttu-id="0ade7-127">按一下 [資料 + 分析] > **辨識服務**。</span><span class="sxs-lookup"><span data-stu-id="0ade7-127">Click **Data + Analytics** > **Cognitive  Services**.</span></span> <span data-ttu-id="0ade7-128">然後，使用資料表中指定的設定、接受條款，並勾選 [釘選到儀表板]。</span><span class="sxs-lookup"><span data-stu-id="0ade7-128">Then, use the settings as specified in the table, accept the terms, and check **Pin to dashboard**.</span></span>

    ![[建立辨識帳戶] 刀鋒視窗](media/functions-twitter-email/cog_svcs_account.png)

    | <span data-ttu-id="0ade7-130">設定</span><span class="sxs-lookup"><span data-stu-id="0ade7-130">Setting</span></span>      |  <span data-ttu-id="0ade7-131">建議的值</span><span class="sxs-lookup"><span data-stu-id="0ade7-131">Suggested value</span></span>   | <span data-ttu-id="0ade7-132">說明</span><span class="sxs-lookup"><span data-stu-id="0ade7-132">Description</span></span>                                        |
    | --- | --- | --- |
    | <span data-ttu-id="0ade7-133">**名稱**</span><span class="sxs-lookup"><span data-stu-id="0ade7-133">**Name**</span></span> | <span data-ttu-id="0ade7-134">MyCognitiveServicesAccnt</span><span class="sxs-lookup"><span data-stu-id="0ade7-134">MyCognitiveServicesAccnt</span></span> | <span data-ttu-id="0ade7-135">請選擇唯一的帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="0ade7-135">Choose a unique account name.</span></span> |
    | <span data-ttu-id="0ade7-136">**API 類型**</span><span class="sxs-lookup"><span data-stu-id="0ade7-136">**API type**</span></span> | <span data-ttu-id="0ade7-137">文字分析 API</span><span class="sxs-lookup"><span data-stu-id="0ade7-137">Text Analytics API</span></span> | <span data-ttu-id="0ade7-138">用來分析文字的 API。</span><span class="sxs-lookup"><span data-stu-id="0ade7-138">API used to analyze text.</span></span>  |
    | <span data-ttu-id="0ade7-139">**位置**</span><span class="sxs-lookup"><span data-stu-id="0ade7-139">**Location**</span></span> | <span data-ttu-id="0ade7-140">美國西部</span><span class="sxs-lookup"><span data-stu-id="0ade7-140">West US</span></span> | <span data-ttu-id="0ade7-141">目前，只有 [美國西部] 適用於文字分析。</span><span class="sxs-lookup"><span data-stu-id="0ade7-141">Currently, only **West US** is available for text analytics.</span></span> |
    | <span data-ttu-id="0ade7-142">**定價層**</span><span class="sxs-lookup"><span data-stu-id="0ade7-142">**Pricing tier**</span></span> | <span data-ttu-id="0ade7-143">F0</span><span class="sxs-lookup"><span data-stu-id="0ade7-143">F0</span></span> | <span data-ttu-id="0ade7-144">從最低層開始。</span><span class="sxs-lookup"><span data-stu-id="0ade7-144">Start with the lowest tier.</span></span> <span data-ttu-id="0ade7-145">如果您用完呼叫，請調整為較高層。</span><span class="sxs-lookup"><span data-stu-id="0ade7-145">If you run out of calls, scale to a higher tier.</span></span>|
    | <span data-ttu-id="0ade7-146">**資源群組**</span><span class="sxs-lookup"><span data-stu-id="0ade7-146">**Resource group**</span></span> | <span data-ttu-id="0ade7-147">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="0ade7-147">myResourceGroup</span></span> | <span data-ttu-id="0ade7-148">本教學課程中所有的服務，都是使用相同的資源群組。</span><span class="sxs-lookup"><span data-stu-id="0ade7-148">Use the same resource group for all services in this tutorial.</span></span>|

4. <span data-ttu-id="0ade7-149">按一下 [建立] 可建立帳戶。</span><span class="sxs-lookup"><span data-stu-id="0ade7-149">Click **Create** to create your account.</span></span> <span data-ttu-id="0ade7-150">建立帳戶之後，按一下釘選到儀表板的新辨識服務帳戶。</span><span class="sxs-lookup"><span data-stu-id="0ade7-150">After the account is created, click your new Cognitive Services account pinned to the dashboard.</span></span> 

5. <span data-ttu-id="0ade7-151">在帳戶中，按一下 [金鑰]，然後將**金鑰 1** 的值複製並加以儲存。</span><span class="sxs-lookup"><span data-stu-id="0ade7-151">In the account, click **Keys**, and then copy the value of **Key 1** and save it.</span></span> <span data-ttu-id="0ade7-152">您可以使用此金鑰，將邏輯應用程式連線至辨識服務帳戶。</span><span class="sxs-lookup"><span data-stu-id="0ade7-152">You use this key to connect the logic app to your Cognitive Services account.</span></span> 
 
    ![之間的信任](media/functions-twitter-email/keys.png)

## <a name="create-the-function"></a><span data-ttu-id="0ade7-154">建立函式</span><span class="sxs-lookup"><span data-stu-id="0ade7-154">Create the function</span></span>

<span data-ttu-id="0ade7-155">Functions 提供的絕佳方法，可讓您將 Logic Apps 工作流程中的處理工作進行卸載。</span><span class="sxs-lookup"><span data-stu-id="0ade7-155">Functions provides a great way to offload processing tasks in a logic apps workflow.</span></span> <span data-ttu-id="0ade7-156">本教學課程會使用 HTTP 觸發函式來處理辨識服務的推文情感分數，並將類別值傳回。</span><span class="sxs-lookup"><span data-stu-id="0ade7-156">This tutorial uses an HTTP triggered function to process tweet sentiment scores from Cognitive Services and return a category value.</span></span>  

1. <span data-ttu-id="0ade7-157">展開函式應用程式，按一下 [函式] 旁的 [+] 按鈕，然後按一下 [HTTPTrigger] 範本。</span><span class="sxs-lookup"><span data-stu-id="0ade7-157">Expand your function app, click the **+** button next to **Functions**, click the **HTTPTrigger** template.</span></span> <span data-ttu-id="0ade7-158">輸入 `CategorizeSentiment` 作為函式**名稱**，然後按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="0ade7-158">Type `CategorizeSentiment` for the function **Name** and click **Create**.</span></span>

    ![函式應用程式刀鋒視窗，Functions +](media/functions-twitter-email/add_fun.png)

2. <span data-ttu-id="0ade7-160">使用下列程式碼取代 run.csx 檔案的內容，然後按一下 [儲存]：</span><span class="sxs-lookup"><span data-stu-id="0ade7-160">Replace the contents of the run.csx file with the following code, then click **Save**:</span></span>

    ```c#
    using System.Net;
    
    public static async Task<HttpResponseMessage> Run(HttpRequestMessage req, TraceWriter log)
    {
        // The sentiment category defaults to 'GREEN'. 
        string category = "GREEN";
    
        // Get the sentiment score from the request body.
        double score = await req.Content.ReadAsAsync<double>();
        log.Info(string.Format("The sentiment score received is '{0}'.",
                    score.ToString()));
    
        // Set the category based on the sentiment score.
        if (score < .3)
        {
            category = "RED";
        }
        else if (score < .6)
        {
            category = "YELLOW";
        }
        return req.CreateResponse(HttpStatusCode.OK, category);
    }
    ```
    <span data-ttu-id="0ade7-161">此函式程式碼會以要求中所收到的情感分數作為基礎，將色彩類別傳回。</span><span class="sxs-lookup"><span data-stu-id="0ade7-161">This function code returns a color category based on the sentiment score received in the request.</span></span> 

3. <span data-ttu-id="0ade7-162">若要測試函式，請按一下最右邊的 [測試]，將 [測試] 索引標籤展開。輸入 `0.2` 的值作為**要求本文**，然後按一下 [執行]。</span><span class="sxs-lookup"><span data-stu-id="0ade7-162">To test the function, click **Test** at the far right to expand the Test tab. Type a value of `0.2` for the **Request body**, and then click **Run**.</span></span> <span data-ttu-id="0ade7-163">會在回應本文中傳回**紅色**的值。</span><span class="sxs-lookup"><span data-stu-id="0ade7-163">A value of **RED** is returned in the body of the response.</span></span> 

    ![在 Azure 入口網站中測試函式](./media/functions-twitter-email/test.png)

<span data-ttu-id="0ade7-165">現在您的函式可將情感分數進行分類。</span><span class="sxs-lookup"><span data-stu-id="0ade7-165">Now you have a function that categorizes sentiment scores.</span></span> <span data-ttu-id="0ade7-166">接下來，您可以建立邏輯應用程式，將您的函式與 Twitter 和辨識服務帳戶進行。</span><span class="sxs-lookup"><span data-stu-id="0ade7-166">Next, you create a logic app that integrates your function with your Twitter and Cognitive Services accounts.</span></span> 

## <a name="create-a-logic-app"></a><span data-ttu-id="0ade7-167">建立邏輯應用程式</span><span class="sxs-lookup"><span data-stu-id="0ade7-167">Create a logic app</span></span>   

1. <span data-ttu-id="0ade7-168">在 Azure 入口網站中，按一下 Azure 入口網站左上角的 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="0ade7-168">In the Azure portal, click the **New** button found on the upper left-hand corner of the Azure portal.</span></span>

2. <span data-ttu-id="0ade7-169">按一下 [企業整合] > [邏輯應用程式]。</span><span class="sxs-lookup"><span data-stu-id="0ade7-169">Click **Enterprise Integration** > **Logic App**.</span></span> <span data-ttu-id="0ade7-170">然後，使用資料表中指定的設定、勾選 [釘選到儀表板]，然後按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="0ade7-170">Then, use the settings as specified in the table, check **Pin to dashboard**, and click **Create**.</span></span>
 
4. <span data-ttu-id="0ade7-171">然後，輸入**名稱** (例如 `TweetSentiment`)、使用資料表中指定的設定、接受條款，並勾選 [釘選到儀表板]。</span><span class="sxs-lookup"><span data-stu-id="0ade7-171">Then, type a **Name** like `TweetSentiment`,  use the settings as specified in the table, accept the terms, and check **Pin to dashboard**.</span></span>

    ![在 Azure 入口網站中建立邏輯應用程式](./media/functions-twitter-email/new_logicApp.png)

    | <span data-ttu-id="0ade7-173">設定</span><span class="sxs-lookup"><span data-stu-id="0ade7-173">Setting</span></span>      |  <span data-ttu-id="0ade7-174">建議的值</span><span class="sxs-lookup"><span data-stu-id="0ade7-174">Suggested value</span></span>   | <span data-ttu-id="0ade7-175">說明</span><span class="sxs-lookup"><span data-stu-id="0ade7-175">Description</span></span>                                        |
    | ----------------- | ------------ | ------------- |
    | <span data-ttu-id="0ade7-176">**名稱**</span><span class="sxs-lookup"><span data-stu-id="0ade7-176">**Name**</span></span> | <span data-ttu-id="0ade7-177">TweetSentiment</span><span class="sxs-lookup"><span data-stu-id="0ade7-177">TweetSentiment</span></span> | <span data-ttu-id="0ade7-178">為您的應用程式選擇適當名稱。</span><span class="sxs-lookup"><span data-stu-id="0ade7-178">Choose an appropriate name for your app.</span></span> |
    | <span data-ttu-id="0ade7-179">**資源群組**</span><span class="sxs-lookup"><span data-stu-id="0ade7-179">**Resource group**</span></span> | <span data-ttu-id="0ade7-180">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="0ade7-180">myResourceGroup</span></span> | <span data-ttu-id="0ade7-181">用來分析文字的 API。</span><span class="sxs-lookup"><span data-stu-id="0ade7-181">API used to analyze text.</span></span>  |
    | <span data-ttu-id="0ade7-182">**位置**</span><span class="sxs-lookup"><span data-stu-id="0ade7-182">**Location**</span></span> | <span data-ttu-id="0ade7-183">美國東部</span><span class="sxs-lookup"><span data-stu-id="0ade7-183">East US</span></span> | <span data-ttu-id="0ade7-184">選擇接近您的位置。</span><span class="sxs-lookup"><span data-stu-id="0ade7-184">Choose a location close to you.</span></span> |
    | <span data-ttu-id="0ade7-185">**資源群組**</span><span class="sxs-lookup"><span data-stu-id="0ade7-185">**Resource group**</span></span> | <span data-ttu-id="0ade7-186">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="0ade7-186">myResourceGroup</span></span> | <span data-ttu-id="0ade7-187">選擇與之前相同的現有資源群組。</span><span class="sxs-lookup"><span data-stu-id="0ade7-187">Choose the same existing resource group as before.</span></span>|

4. <span data-ttu-id="0ade7-188">按一下 [建立] 可建立邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="0ade7-188">Click **Create** to create your logic app.</span></span> <span data-ttu-id="0ade7-189">建立應用程式之後，按一下釘選到儀表板的新邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="0ade7-189">After the app is created, click your new logic app pinned to the dashboard.</span></span> <span data-ttu-id="0ade7-190">接著，在 Logic Apps 設計工具中，向下捲動並按一下 [空白的邏輯應用程式] 範本。</span><span class="sxs-lookup"><span data-stu-id="0ade7-190">Then in the Logic Apps Designer, scroll down and click the **Blank Logic App** template.</span></span> 

    ![空白的 Logic Apps 範本](media/functions-twitter-email/blank.png)

<span data-ttu-id="0ade7-192">您現在可以使用 Logic Apps 設計工具，將服務和觸發程序新增至您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="0ade7-192">You can now use the Logic Apps Designer to add services and triggers to your app.</span></span>

## <a name="connect-to-twitter"></a><span data-ttu-id="0ade7-193">連接到 Twitter</span><span class="sxs-lookup"><span data-stu-id="0ade7-193">Connect to Twitter</span></span>

<span data-ttu-id="0ade7-194">首先，建立您 Twitter 帳戶的連線。</span><span class="sxs-lookup"><span data-stu-id="0ade7-194">First, create a connection to your Twitter account.</span></span> <span data-ttu-id="0ade7-195">邏輯應用程式會輪詢推文，從而觸發應用程式加以執行。</span><span class="sxs-lookup"><span data-stu-id="0ade7-195">The logic app polls for tweets, which trigger the app to run.</span></span>

1. <span data-ttu-id="0ade7-196">在設計工具中，按一下 [Twitter] 服務，然後按一下 [張貼新推文時] 觸發程序。</span><span class="sxs-lookup"><span data-stu-id="0ade7-196">In the designer, click the **Twitter** service, and click the **When a new tweet is posted** trigger.</span></span> <span data-ttu-id="0ade7-197">登入您的 Twitter 帳戶，並授權 Logic Apps 以使用您的帳戶。</span><span class="sxs-lookup"><span data-stu-id="0ade7-197">Sign in to your Twitter account and authorize Logic Apps to use your account.</span></span>

2. <span data-ttu-id="0ade7-198">使用表格中指定的 Twitter 觸發程序設定。</span><span class="sxs-lookup"><span data-stu-id="0ade7-198">Use the Twitter trigger settings as specified in the table.</span></span> 

    ![Twitter 連接器設定](media/functions-twitter-email/azure_tweet.png)

    | <span data-ttu-id="0ade7-200">設定</span><span class="sxs-lookup"><span data-stu-id="0ade7-200">Setting</span></span>      |  <span data-ttu-id="0ade7-201">建議的值</span><span class="sxs-lookup"><span data-stu-id="0ade7-201">Suggested value</span></span>   | <span data-ttu-id="0ade7-202">說明</span><span class="sxs-lookup"><span data-stu-id="0ade7-202">Description</span></span>                                        |
    | ----------------- | ------------ | ------------- |
    | <span data-ttu-id="0ade7-203">**搜尋文字**</span><span class="sxs-lookup"><span data-stu-id="0ade7-203">**Search text**</span></span> | <span data-ttu-id="0ade7-204">#Azure</span><span class="sxs-lookup"><span data-stu-id="0ade7-204">#Azure</span></span> | <span data-ttu-id="0ade7-205">使用熱門程度足夠在指定間隔內產生新推文的雜湊標記。</span><span class="sxs-lookup"><span data-stu-id="0ade7-205">Use a hashtag that is popular enough for to generate new tweets in the chosen interval.</span></span> <span data-ttu-id="0ade7-206">當您是使用免費層且您的雜湊標記太熱門時，可能很快就會將辨識服務帳戶中的交易用完。</span><span class="sxs-lookup"><span data-stu-id="0ade7-206">When using the Free tier and your hashtag is too popular, you can quickly use up the transactions in your Cognitive Services account.</span></span> |
    | <span data-ttu-id="0ade7-207">**頻率**</span><span class="sxs-lookup"><span data-stu-id="0ade7-207">**Frequency**</span></span> | <span data-ttu-id="0ade7-208">分鐘</span><span class="sxs-lookup"><span data-stu-id="0ade7-208">Minute</span></span> | <span data-ttu-id="0ade7-209">用於輪詢 Twitter 的頻率單位。</span><span class="sxs-lookup"><span data-stu-id="0ade7-209">The frequency unit used for polling Twitter.</span></span>  |
    | <span data-ttu-id="0ade7-210">**間隔**</span><span class="sxs-lookup"><span data-stu-id="0ade7-210">**Interval**</span></span> | <span data-ttu-id="0ade7-211">15</span><span class="sxs-lookup"><span data-stu-id="0ade7-211">15</span></span> | <span data-ttu-id="0ade7-212">Twitter 要求之間所經過的時間 (以頻率為單位)。</span><span class="sxs-lookup"><span data-stu-id="0ade7-212">The time elapsed between Twitter requests, in frequency units.</span></span> |

3.  <span data-ttu-id="0ade7-213">按一下 [儲存]可連線到您的 Twitter 帳戶。</span><span class="sxs-lookup"><span data-stu-id="0ade7-213">Click **Save** to connect to your Twitter account.</span></span> 

<span data-ttu-id="0ade7-214">現在，您的應用程式已連線到 Twitter。</span><span class="sxs-lookup"><span data-stu-id="0ade7-214">Now your app is connected to Twitter.</span></span> <span data-ttu-id="0ade7-215">接下來，您要連線至文字分析來偵測收集推文的情感。</span><span class="sxs-lookup"><span data-stu-id="0ade7-215">Next, you connect to text analytics to detect the sentiment of collected tweets.</span></span>

## <a name="add-sentiment-detection"></a><span data-ttu-id="0ade7-216">新增情感偵測</span><span class="sxs-lookup"><span data-stu-id="0ade7-216">Add sentiment detection</span></span>

1. <span data-ttu-id="0ade7-217">依序按一下 [新增步驟]、[新增動作]。</span><span class="sxs-lookup"><span data-stu-id="0ade7-217">Click **New Step**, and then **Add an action**.</span></span>

    ![選取 [新增步驟]，然後選取 [新增動作]](media/functions-twitter-email/new_step.png)

2. <span data-ttu-id="0ade7-219">在 [選擇動作] 中，按一下 [文字分析]，然後按一下 [偵測情感] 動作。</span><span class="sxs-lookup"><span data-stu-id="0ade7-219">In **Choose an action**, click **Text Analytics**, and then click the **Detect sentiment** action.</span></span>

    ![偵測情感](media/functions-twitter-email/detect_sent.png)

3. <span data-ttu-id="0ade7-221">輸入連線名稱 (例如 `MyCognitiveServicesConnection`)、將您所儲存的辨識服務帳戶金鑰貼上，然後按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="0ade7-221">Type a connection name such as `MyCognitiveServicesConnection`, paste the key for your Cognitive Services account that you saved, and click **Create**.</span></span>  

4. <span data-ttu-id="0ade7-222">按一下 [要分析的文字] > [推文文字]，然後按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="0ade7-222">Click **Text to analyze** > **Tweet text**, and then click **Save**.</span></span>  

    ![偵測情感](media/functions-twitter-email/ds_tta.png)

<span data-ttu-id="0ade7-224">現在您已設定情感偵測，可將連線新增至使用情感分數輸出的函式。</span><span class="sxs-lookup"><span data-stu-id="0ade7-224">Now that sentiment detection is configured, you can add a connection to your function that consumes the sentiment score output.</span></span>

## <a name="connect-sentiment-output-to-your-function"></a><span data-ttu-id="0ade7-225">將情感輸出連線至您的函式</span><span class="sxs-lookup"><span data-stu-id="0ade7-225">Connect sentiment output to your function</span></span>

1. <span data-ttu-id="0ade7-226">在 Logic Apps 設計工具中，按一下 [新增步驟] > [新增動作]，然後按一下 [Azure Functions]。</span><span class="sxs-lookup"><span data-stu-id="0ade7-226">In the Logic Apps Designer, click **New step** > **Add an action**, and then click **Azure Functions**.</span></span> 

2. <span data-ttu-id="0ade7-227">按一下 [選擇 Azure 函式]，選取您稍早建立的 **CategorizeSentiment** 函式。</span><span class="sxs-lookup"><span data-stu-id="0ade7-227">Click **Choose an Azure function**, select the **CategorizeSentiment** function you created earlier.</span></span>  

    ![顯示 [選擇 Azure 函式] 的 Azure 函式方塊](media/functions-twitter-email/choose_fun.png)

3. <span data-ttu-id="0ade7-229">在**要求本文**中，依序按一下 [分數] 和 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="0ade7-229">In **Request Body**, click **Score** and then **Save**.</span></span>

    ![分數](media/functions-twitter-email/trigger_score.png)

<span data-ttu-id="0ade7-231">現在，當邏輯應用程式傳送出情感分數時，就會將您的函式觸發。</span><span class="sxs-lookup"><span data-stu-id="0ade7-231">Now, your function is triggered when a sentiment score is sent from the logic app.</span></span> <span data-ttu-id="0ade7-232">函式會將以色彩標示的類別傳回至邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="0ade7-232">A color-coded category is returned to the logic app by the function.</span></span> <span data-ttu-id="0ade7-233">接下來，您要將函式傳回**紅色**的情感值時所傳送的電子郵件通知加以新增。</span><span class="sxs-lookup"><span data-stu-id="0ade7-233">Next, you add an email notification that is sent when a sentiment value of **RED** is returned from the function.</span></span> 

## <a name="add-email-notifications"></a><span data-ttu-id="0ade7-234">新增電子郵件通知</span><span class="sxs-lookup"><span data-stu-id="0ade7-234">Add email notifications</span></span>

<span data-ttu-id="0ade7-235">工作流程的最後一個部分，是當情感計分為_紅色_時，要將電子郵件觸發。</span><span class="sxs-lookup"><span data-stu-id="0ade7-235">The last part of the workflow is to trigger an email when the sentiment is scored as _RED_.</span></span> <span data-ttu-id="0ade7-236">本主題是使用 Outlook.com 連接器。</span><span class="sxs-lookup"><span data-stu-id="0ade7-236">This topic uses an Outlook.com connector.</span></span> <span data-ttu-id="0ade7-237">您可以執行類似的步驟，來使用 Gmail 或 Office 365 Outlook 連接器。</span><span class="sxs-lookup"><span data-stu-id="0ade7-237">You can perform similar steps to use a Gmail or Office 365 Outlook connector.</span></span>   

1. <span data-ttu-id="0ade7-238">在 Logic Apps 設計工具中，按一下 [新增步驟] > [新增條件]。</span><span class="sxs-lookup"><span data-stu-id="0ade7-238">In the Logic Apps Designer, click **New step** > **Add a condition**.</span></span> 

2. <span data-ttu-id="0ade7-239">按一下 [選擇值]，然後按一下 [本文]。</span><span class="sxs-lookup"><span data-stu-id="0ade7-239">Click **Choose a value**, then click **Body**.</span></span> <span data-ttu-id="0ade7-240">選取 [等於]、按一下 [選擇值] 並輸入 `RED`，然後按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="0ade7-240">Select **is equal to**, click **Choose a value** and type `RED`, and click **Save**.</span></span> 

    ![將條件新增至邏輯應用程式。](media/functions-twitter-email/condition.png)

3. <span data-ttu-id="0ade7-242">在 [若為是，則不執行任何動作] 中、按一下 [新增動作]、搜尋 `outlook.com`、按一下 [傳送電子郵件]，然後登入您的 Outlook.com 帳戶。</span><span class="sxs-lookup"><span data-stu-id="0ade7-242">In **IF YES, DO NOTHING**, click **Add an action**, search for `outlook.com`, click **Send an email**, and sign in to your Outlook.com account.</span></span>
    
    ![選擇條件的動作。](media/functions-twitter-email/outlook.png)

    > [!NOTE]
    > <span data-ttu-id="0ade7-244">如果您沒有 Outlook.com 帳戶，可以選擇另一個連接器，例如 Gmail 或 Office 365 Outlook</span><span class="sxs-lookup"><span data-stu-id="0ade7-244">If you don't have an Outlook.com account, you can choose another connector, such as Gmail or Office 365 Outlook</span></span>

4. <span data-ttu-id="0ade7-245">在**傳送電子郵件**動作，使用資料表中指定的電子郵件設定。</span><span class="sxs-lookup"><span data-stu-id="0ade7-245">In the **Send an email** action, use the email settings as specified in the table.</span></span> 

    ![設定傳送電子郵件動作的電子郵件。](media/functions-twitter-email/sendemail.png)

    | <span data-ttu-id="0ade7-247">設定</span><span class="sxs-lookup"><span data-stu-id="0ade7-247">Setting</span></span>      |  <span data-ttu-id="0ade7-248">建議的值</span><span class="sxs-lookup"><span data-stu-id="0ade7-248">Suggested value</span></span>   | <span data-ttu-id="0ade7-249">說明</span><span class="sxs-lookup"><span data-stu-id="0ade7-249">Description</span></span>  |
    | ----------------- | ------------ | ------------- |
    | <span data-ttu-id="0ade7-250">**To**</span><span class="sxs-lookup"><span data-stu-id="0ade7-250">**To**</span></span> | <span data-ttu-id="0ade7-251">輸入您的電子郵件地址</span><span class="sxs-lookup"><span data-stu-id="0ade7-251">Type your email address</span></span> | <span data-ttu-id="0ade7-252">接收通知電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="0ade7-252">The email address that receives the notification.</span></span> |
    | <span data-ttu-id="0ade7-253">**主旨**</span><span class="sxs-lookup"><span data-stu-id="0ade7-253">**Subject**</span></span> | <span data-ttu-id="0ade7-254">偵測到負面的推文情感</span><span class="sxs-lookup"><span data-stu-id="0ade7-254">Negative tweet sentiment detected</span></span>  | <span data-ttu-id="0ade7-255">電子郵件通知的主旨列。</span><span class="sxs-lookup"><span data-stu-id="0ade7-255">The subject line of the email notification.</span></span>  |
    | <span data-ttu-id="0ade7-256">**內文**</span><span class="sxs-lookup"><span data-stu-id="0ade7-256">**Body**</span></span> | <span data-ttu-id="0ade7-257">推文文字、位置</span><span class="sxs-lookup"><span data-stu-id="0ade7-257">Tweet text, Location</span></span> | <span data-ttu-id="0ade7-258">按一下 [推文文字] 和 [位置] 參數。</span><span class="sxs-lookup"><span data-stu-id="0ade7-258">Click the **Tweet text** and **Location** parameters.</span></span> |

5.  <span data-ttu-id="0ade7-259">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="0ade7-259">Click **Save**.</span></span>

<span data-ttu-id="0ade7-260">現在，工作流程已完成，您可以啟用邏輯應用程式，並查看工作的函式。</span><span class="sxs-lookup"><span data-stu-id="0ade7-260">Now that the workflow is complete, you can enable the logic app and see the function at work.</span></span>

## <a name="test-the-workflow"></a><span data-ttu-id="0ade7-261">測試工作流程</span><span class="sxs-lookup"><span data-stu-id="0ade7-261">Test the workflow</span></span>

1. <span data-ttu-id="0ade7-262">在邏輯應用程式設計工具中，按一下 [執行] 可啟動應用程式。</span><span class="sxs-lookup"><span data-stu-id="0ade7-262">In the Logic App Designer, click **Run** to start the app.</span></span>

2. <span data-ttu-id="0ade7-263">在左欄中，按一下 [概觀] 可查看邏輯應用程式的狀態。</span><span class="sxs-lookup"><span data-stu-id="0ade7-263">In the left column, click **Overview** to see the status of the logic app.</span></span> 
 
    ![邏輯應用程式執行狀態](media/functions-twitter-email/over1.png)

3. <span data-ttu-id="0ade7-265">(選擇性) 按下其中一個執行，可查看執行的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="0ade7-265">(Optional) Click one of the runs to see details of the execution.</span></span>

4. <span data-ttu-id="0ade7-266">請移至您的函式、檢視記錄，並確認已收到情感值並已加以處理。</span><span class="sxs-lookup"><span data-stu-id="0ade7-266">Go to your function, view the logs, and verify that sentiment values were received and processed.</span></span>
 
    ![檢視函式記錄](media/functions-twitter-email/sent.png)

5. <span data-ttu-id="0ade7-268">偵測到潛在的負面情感時，您會收到一封電子郵件。</span><span class="sxs-lookup"><span data-stu-id="0ade7-268">When a potentially negative sentiment is detected, you receive an email.</span></span> <span data-ttu-id="0ade7-269">如果您尚未收到電子郵件，可以將函式程式碼變更為每次傳回「紅色」︰</span><span class="sxs-lookup"><span data-stu-id="0ade7-269">If you haven't received an email, you can change the function code to return RED every time:</span></span>

        return req.CreateResponse(HttpStatusCode.OK, "RED");

    <span data-ttu-id="0ade7-270">確認電子郵件通知之後，請變更回原始的程式碼︰</span><span class="sxs-lookup"><span data-stu-id="0ade7-270">After you have verified email notifications, change back to the original code:</span></span>

        return req.CreateResponse(HttpStatusCode.OK, category);

    > [!IMPORTANT]
    > <span data-ttu-id="0ade7-271">完成本教學課程之後，您應停用邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="0ade7-271">After you have completed this tutorial, you should disable the logic app.</span></span> <span data-ttu-id="0ade7-272">您可以透過停用應用程式，在執行及用完辨識服務帳戶中的交易時可避免支付費用。</span><span class="sxs-lookup"><span data-stu-id="0ade7-272">By disabling the app, you avoid being charged for executions and using up the transactions in your Cognitive Services account.</span></span>

<span data-ttu-id="0ade7-273">現在您已經知道要將 Functions 整合至 Logic Apps 工作流程有多麼輕鬆。</span><span class="sxs-lookup"><span data-stu-id="0ade7-273">Now you have seen how easy it is to integrate Functions into a Logic Apps workflow.</span></span>

## <a name="disable-the-logic-app"></a><span data-ttu-id="0ade7-274">停用邏輯應用程式</span><span class="sxs-lookup"><span data-stu-id="0ade7-274">Disable the logic app</span></span>

<span data-ttu-id="0ade7-275">若要停用邏輯應用程式，請依序按一下螢幕頂端的 [概觀] 及 [停用]。</span><span class="sxs-lookup"><span data-stu-id="0ade7-275">To disable the logic app, click **Overview** and then click **Disable** at the top of the screen.</span></span> <span data-ttu-id="0ade7-276">這樣無須刪除應用程式，就可以使邏輯應用程式停止執行及產生費用。</span><span class="sxs-lookup"><span data-stu-id="0ade7-276">This stops the logic app from running and incurring charges without deleting the app.</span></span> 

![函式記錄](media/functions-twitter-email/disable-logic-app.png)

## <a name="next-steps"></a><span data-ttu-id="0ade7-278">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0ade7-278">Next steps</span></span>

<span data-ttu-id="0ade7-279">在本教學課程中，您已了解如何：</span><span class="sxs-lookup"><span data-stu-id="0ade7-279">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="0ade7-280">建立辨識服務帳戶。</span><span class="sxs-lookup"><span data-stu-id="0ade7-280">Create a Cognitive Services account.</span></span>
> * <span data-ttu-id="0ade7-281">建立可將推文情感進行分類的函式。</span><span class="sxs-lookup"><span data-stu-id="0ade7-281">Create a function that categorizes tweet sentiment.</span></span>
> * <span data-ttu-id="0ade7-282">建立連線至 Twitter 的邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="0ade7-282">Create a logic app that connects to Twitter.</span></span>
> * <span data-ttu-id="0ade7-283">將情感偵測新增至邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="0ade7-283">Add sentiment detection to the logic app.</span></span> 
> * <span data-ttu-id="0ade7-284">將邏輯應用程式連線至函式。</span><span class="sxs-lookup"><span data-stu-id="0ade7-284">Connect the logic app to the function.</span></span>
> * <span data-ttu-id="0ade7-285">以函式的回應作為基礎來傳送電子郵件。</span><span class="sxs-lookup"><span data-stu-id="0ade7-285">Send an email based on the response from the function.</span></span>

<span data-ttu-id="0ade7-286">前進至下一個教學課程，了解如何針對函式建立無伺服器 API。</span><span class="sxs-lookup"><span data-stu-id="0ade7-286">Advance to the next tutorial to learn how to create a serverless API for your function.</span></span>

> [!div class="nextstepaction"] 
> [<span data-ttu-id="0ade7-287">使用 Azure Functions 建立無伺服器 API</span><span class="sxs-lookup"><span data-stu-id="0ade7-287">Create a serverless API using Azure Functions</span></span>](functions-create-serverless-api.md)

<span data-ttu-id="0ade7-288">若要深入了解 Logic Apps，請參閱 [Azure Logic Apps](../logic-apps/logic-apps-what-are-logic-apps.md)。</span><span class="sxs-lookup"><span data-stu-id="0ade7-288">To learn more about Logic Apps, see [Azure Logic Apps](../logic-apps/logic-apps-what-are-logic-apps.md).</span></span>

