---
title: "aaaCreate 函式可與 Azure 邏輯應用程式整合，|Microsoft 文件"
description: "建立 Azure 邏輯應用程式和 Azure 認知服務 toocategorize 推文人氣與整合的函式和人氣很低時，傳送通知。"
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
ms.openlocfilehash: e176bd946af9a3684b3ad0e4b1bed1c3ee344019
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-function-that-integrates-with-azure-logic-apps"></a><span data-ttu-id="9a3be-104">建立與 Azure Logic Apps 整合的函式</span><span class="sxs-lookup"><span data-stu-id="9a3be-104">Create a function that integrates with Azure Logic Apps</span></span>

<span data-ttu-id="9a3be-105">Azure 邏輯應用程式與整合 hello 邏輯應用程式的設計工具中，azure 函式。</span><span class="sxs-lookup"><span data-stu-id="9a3be-105">Azure Functions integrates with Azure Logic Apps in hello Logic Apps Designer.</span></span> <span data-ttu-id="9a3be-106">這項整合可讓您使用的運算能力函式與其他 Azure 和協力廠商服務的協調流程中的 hello。</span><span class="sxs-lookup"><span data-stu-id="9a3be-106">This integration lets you use hello computing power of Functions in orchestrations with other Azure and third-party services.</span></span> 

<span data-ttu-id="9a3be-107">此教學課程會示範如何 toouse 函式與從 Twitter 文章的 Logic Apps 和 Azure 認知服務 tooanalyze 人氣。</span><span class="sxs-lookup"><span data-stu-id="9a3be-107">This tutorial shows you how toouse Functions with Logic Apps and Azure Cognitive Services tooanalyze sentiment from Twitter posts.</span></span> <span data-ttu-id="9a3be-108">HTTP 觸發函式將分類為綠色、 黃色或紅色 hello 人氣分數為基礎的推文。</span><span class="sxs-lookup"><span data-stu-id="9a3be-108">An HTTP triggered function categorizes tweets as green, yellow, or red based on hello sentiment score.</span></span> <span data-ttu-id="9a3be-109">偵測到不佳的情感時，會傳送一封電子郵件。</span><span class="sxs-lookup"><span data-stu-id="9a3be-109">An email is sent when poor sentiment is detected.</span></span> 

![此映像顯示邏輯應用程式設計工具中應用程式的前兩個步驟](media/functions-twitter-email/designer1.png)

<span data-ttu-id="9a3be-111">在本教學課程中，您將了解如何：</span><span class="sxs-lookup"><span data-stu-id="9a3be-111">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="9a3be-112">建立辨識服務帳戶。</span><span class="sxs-lookup"><span data-stu-id="9a3be-112">Create a Cognitive Services account.</span></span>
> * <span data-ttu-id="9a3be-113">建立可將推文情感進行分類的函式。</span><span class="sxs-lookup"><span data-stu-id="9a3be-113">Create a function that categorizes tweet sentiment.</span></span>
> * <span data-ttu-id="9a3be-114">建立連接 tooTwitter 邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="9a3be-114">Create a logic app that connects tooTwitter.</span></span>
> * <span data-ttu-id="9a3be-115">加入 人氣偵測 toohello 邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="9a3be-115">Add sentiment detection toohello logic app.</span></span> 
> * <span data-ttu-id="9a3be-116">連接 hello 邏輯應用程式 toohello 函式。</span><span class="sxs-lookup"><span data-stu-id="9a3be-116">Connect hello logic app toohello function.</span></span>
> * <span data-ttu-id="9a3be-117">傳送 hello 回應 hello 函式為基礎的電子郵件。</span><span class="sxs-lookup"><span data-stu-id="9a3be-117">Send an email based on hello response from hello function.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9a3be-118">必要條件</span><span class="sxs-lookup"><span data-stu-id="9a3be-118">Prerequisites</span></span>

+ <span data-ttu-id="9a3be-119">使用中的 [Twitter](https://twitter.com/) 帳戶。</span><span class="sxs-lookup"><span data-stu-id="9a3be-119">An active [Twitter](https://twitter.com/) account.</span></span> 
+ <span data-ttu-id="9a3be-120">[Outlook.com](https://outlook.com/) 帳戶 (用於傳送通知)。</span><span class="sxs-lookup"><span data-stu-id="9a3be-120">An [Outlook.com](https://outlook.com/) account (for sending notifications).</span></span>
+ <span data-ttu-id="9a3be-121">本主題以建立其起始點 hello 資源為[從 hello Azure 入口網站中建立您的第一個函式](functions-create-first-azure-function.md)。</span><span class="sxs-lookup"><span data-stu-id="9a3be-121">This topic uses as its starting point hello resources created in [Create your first function from hello Azure portal](functions-create-first-azure-function.md).</span></span>  
<span data-ttu-id="9a3be-122">如果您尚未這樣做，請完成這些步驟現在 toocreate 函式應用程式。</span><span class="sxs-lookup"><span data-stu-id="9a3be-122">If you haven't already done so, complete these steps now toocreate your function app.</span></span>

## <a name="create-a-cognitive-services-account"></a><span data-ttu-id="9a3be-123">建立辨識服務帳戶</span><span class="sxs-lookup"><span data-stu-id="9a3be-123">Create a Cognitive Services account</span></span>

<span data-ttu-id="9a3be-124">認知的服務帳戶是必要的 toodetect hello 人氣的受監視的推文。</span><span class="sxs-lookup"><span data-stu-id="9a3be-124">A Cognitive Services account is required toodetect hello sentiment of tweets being monitored.</span></span>

1. <span data-ttu-id="9a3be-125">登入 toohello [Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="9a3be-125">Sign in toohello [Azure portal](https://portal.azure.com/).</span></span>

2. <span data-ttu-id="9a3be-126">按一下 hello**新增**hello 的左上角 hello Azure 入口網站上找到的按鈕。</span><span class="sxs-lookup"><span data-stu-id="9a3be-126">Click hello **New** button found on hello upper left-hand corner of hello Azure portal.</span></span>

3. <span data-ttu-id="9a3be-127">按一下 [資料 + 分析] > **辨識服務**。</span><span class="sxs-lookup"><span data-stu-id="9a3be-127">Click **Data + Analytics** > **Cognitive  Services**.</span></span> <span data-ttu-id="9a3be-128">使用 hello 設定為在 hello 資料表中，指定接受 hello 條款，然後檢查**Pin toodashboard**。</span><span class="sxs-lookup"><span data-stu-id="9a3be-128">Then, use hello settings as specified in hello table, accept hello terms, and check **Pin toodashboard**.</span></span>

    ![[建立辨識帳戶] 刀鋒視窗](media/functions-twitter-email/cog_svcs_account.png)

    | <span data-ttu-id="9a3be-130">設定</span><span class="sxs-lookup"><span data-stu-id="9a3be-130">Setting</span></span>      |  <span data-ttu-id="9a3be-131">建議的值</span><span class="sxs-lookup"><span data-stu-id="9a3be-131">Suggested value</span></span>   | <span data-ttu-id="9a3be-132">說明</span><span class="sxs-lookup"><span data-stu-id="9a3be-132">Description</span></span>                                        |
    | --- | --- | --- |
    | <span data-ttu-id="9a3be-133">**名稱**</span><span class="sxs-lookup"><span data-stu-id="9a3be-133">**Name**</span></span> | <span data-ttu-id="9a3be-134">MyCognitiveServicesAccnt</span><span class="sxs-lookup"><span data-stu-id="9a3be-134">MyCognitiveServicesAccnt</span></span> | <span data-ttu-id="9a3be-135">請選擇唯一的帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="9a3be-135">Choose a unique account name.</span></span> |
    | <span data-ttu-id="9a3be-136">**API 類型**</span><span class="sxs-lookup"><span data-stu-id="9a3be-136">**API type**</span></span> | <span data-ttu-id="9a3be-137">文字分析 API</span><span class="sxs-lookup"><span data-stu-id="9a3be-137">Text Analytics API</span></span> | <span data-ttu-id="9a3be-138">應用程式開發介面使用 tooanalyze 文字。</span><span class="sxs-lookup"><span data-stu-id="9a3be-138">API used tooanalyze text.</span></span>  |
    | <span data-ttu-id="9a3be-139">**位置**</span><span class="sxs-lookup"><span data-stu-id="9a3be-139">**Location**</span></span> | <span data-ttu-id="9a3be-140">美國西部</span><span class="sxs-lookup"><span data-stu-id="9a3be-140">West US</span></span> | <span data-ttu-id="9a3be-141">目前，只有 [美國西部] 適用於文字分析。</span><span class="sxs-lookup"><span data-stu-id="9a3be-141">Currently, only **West US** is available for text analytics.</span></span> |
    | <span data-ttu-id="9a3be-142">**定價層**</span><span class="sxs-lookup"><span data-stu-id="9a3be-142">**Pricing tier**</span></span> | <span data-ttu-id="9a3be-143">F0</span><span class="sxs-lookup"><span data-stu-id="9a3be-143">F0</span></span> | <span data-ttu-id="9a3be-144">啟動與 hello 最低層。</span><span class="sxs-lookup"><span data-stu-id="9a3be-144">Start with hello lowest tier.</span></span> <span data-ttu-id="9a3be-145">如果您用盡呼叫時，調整 tooa 更高的層。</span><span class="sxs-lookup"><span data-stu-id="9a3be-145">If you run out of calls, scale tooa higher tier.</span></span>|
    | <span data-ttu-id="9a3be-146">**資源群組**</span><span class="sxs-lookup"><span data-stu-id="9a3be-146">**Resource group**</span></span> | <span data-ttu-id="9a3be-147">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="9a3be-147">myResourceGroup</span></span> | <span data-ttu-id="9a3be-148">使用 hello 相同資源群組，在本教學課程的所有服務。</span><span class="sxs-lookup"><span data-stu-id="9a3be-148">Use hello same resource group for all services in this tutorial.</span></span>|

4. <span data-ttu-id="9a3be-149">按一下**建立**toocreate 您的帳戶。</span><span class="sxs-lookup"><span data-stu-id="9a3be-149">Click **Create** toocreate your account.</span></span> <span data-ttu-id="9a3be-150">建立 hello 帳戶之後，按一下 新認知的服務帳戶已釘選的 toohello 儀表板。</span><span class="sxs-lookup"><span data-stu-id="9a3be-150">After hello account is created, click your new Cognitive Services account pinned toohello dashboard.</span></span> 

5. <span data-ttu-id="9a3be-151">Hello 帳戶中，按一下 **金鑰**，然後將複製的 hello 值**金鑰 1**並將其儲存。</span><span class="sxs-lookup"><span data-stu-id="9a3be-151">In hello account, click **Keys**, and then copy hello value of **Key 1** and save it.</span></span> <span data-ttu-id="9a3be-152">您使用此索引鍵 tooconnect hello 邏輯應用程式 tooyour 認知的服務帳戶。</span><span class="sxs-lookup"><span data-stu-id="9a3be-152">You use this key tooconnect hello logic app tooyour Cognitive Services account.</span></span> 
 
    ![之間的信任](media/functions-twitter-email/keys.png)

## <a name="create-hello-function"></a><span data-ttu-id="9a3be-154">建立 hello 函式</span><span class="sxs-lookup"><span data-stu-id="9a3be-154">Create hello function</span></span>

<span data-ttu-id="9a3be-155">函式提供了絕佳 toooffload 邏輯應用程式工作流程中的處理工作。</span><span class="sxs-lookup"><span data-stu-id="9a3be-155">Functions provides a great way toooffload processing tasks in a logic apps workflow.</span></span> <span data-ttu-id="9a3be-156">本教學課程會使用 HTTP 觸發函式 tooprocess 推文人氣分數認知服務及傳回分類值。</span><span class="sxs-lookup"><span data-stu-id="9a3be-156">This tutorial uses an HTTP triggered function tooprocess tweet sentiment scores from Cognitive Services and return a category value.</span></span>  

1. <span data-ttu-id="9a3be-157">展開 應用程式函式中，按一下 hello  **+** 太下一步按鈕**函式**，按一下 hello **HTTPTrigger**範本。</span><span class="sxs-lookup"><span data-stu-id="9a3be-157">Expand your function app, click hello **+** button next too**Functions**, click hello **HTTPTrigger** template.</span></span> <span data-ttu-id="9a3be-158">型別`CategorizeSentiment`hello 函式**名稱**按一下**建立**。</span><span class="sxs-lookup"><span data-stu-id="9a3be-158">Type `CategorizeSentiment` for hello function **Name** and click **Create**.</span></span>

    ![函式應用程式刀鋒視窗，Functions +](media/functions-twitter-email/add_fun.png)

2. <span data-ttu-id="9a3be-160">Hello，下列程式碼，以取代 hello hello run.csx 檔案內容，然後按一下 **儲存**:</span><span class="sxs-lookup"><span data-stu-id="9a3be-160">Replace hello contents of hello run.csx file with hello following code, then click **Save**:</span></span>

    ```c#
    using System.Net;
    
    public static async Task<HttpResponseMessage> Run(HttpRequestMessage req, TraceWriter log)
    {
        // hello sentiment category defaults too'GREEN'. 
        string category = "GREEN";
    
        // Get hello sentiment score from hello request body.
        double score = await req.Content.ReadAsAsync<double>();
        log.Info(string.Format("hello sentiment score received is '{0}'.",
                    score.ToString()));
    
        // Set hello category based on hello sentiment score.
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
    <span data-ttu-id="9a3be-161">此函式程式碼會傳回根據收到 hello 要求中的 hello 人氣分數色彩類別目錄。</span><span class="sxs-lookup"><span data-stu-id="9a3be-161">This function code returns a color category based on hello sentiment score received in hello request.</span></span> 

3. <span data-ttu-id="9a3be-162">tootest hello 函式中，按一下 [**測試**在 hello 最右側 tooexpand hello 測試] 索引標籤。輸入的值是`0.2`hello**要求本文**，然後按一下**執行**。</span><span class="sxs-lookup"><span data-stu-id="9a3be-162">tootest hello function, click **Test** at hello far right tooexpand hello Test tab. Type a value of `0.2` for hello **Request body**, and then click **Run**.</span></span> <span data-ttu-id="9a3be-163">值為**紅色**hello 回應 hello 主體中傳回。</span><span class="sxs-lookup"><span data-stu-id="9a3be-163">A value of **RED** is returned in hello body of hello response.</span></span> 

    ![測試 hello Azure 入口網站中的 hello 函式](./media/functions-twitter-email/test.png)

<span data-ttu-id="9a3be-165">現在您的函式可將情感分數進行分類。</span><span class="sxs-lookup"><span data-stu-id="9a3be-165">Now you have a function that categorizes sentiment scores.</span></span> <span data-ttu-id="9a3be-166">接下來，您可以建立邏輯應用程式，將您的函式與 Twitter 和辨識服務帳戶進行。</span><span class="sxs-lookup"><span data-stu-id="9a3be-166">Next, you create a logic app that integrates your function with your Twitter and Cognitive Services accounts.</span></span> 

## <a name="create-a-logic-app"></a><span data-ttu-id="9a3be-167">建立邏輯應用程式</span><span class="sxs-lookup"><span data-stu-id="9a3be-167">Create a logic app</span></span>   

1. <span data-ttu-id="9a3be-168">在 hello Azure 入口網站中按一下 hello**新增**hello 的左上角 hello Azure 入口網站上找到的按鈕。</span><span class="sxs-lookup"><span data-stu-id="9a3be-168">In hello Azure portal, click hello **New** button found on hello upper left-hand corner of hello Azure portal.</span></span>

2. <span data-ttu-id="9a3be-169">按一下 [企業整合] > [邏輯應用程式]。</span><span class="sxs-lookup"><span data-stu-id="9a3be-169">Click **Enterprise Integration** > **Logic App**.</span></span> <span data-ttu-id="9a3be-170">然後，使用 hello 設定做為資料表中指定 hello，請檢查**Pin toodashboard**，然後按一下**建立**。</span><span class="sxs-lookup"><span data-stu-id="9a3be-170">Then, use hello settings as specified in hello table, check **Pin toodashboard**, and click **Create**.</span></span>
 
4. <span data-ttu-id="9a3be-171">然後，輸入**名稱**像`TweetSentiment`、 hello 表指定方式使用 hello 設定、 接受 hello 條款，以及檢查**Pin toodashboard**。</span><span class="sxs-lookup"><span data-stu-id="9a3be-171">Then, type a **Name** like `TweetSentiment`,  use hello settings as specified in hello table, accept hello terms, and check **Pin toodashboard**.</span></span>

    ![在 hello Azure 入口網站中建立邏輯應用程式](./media/functions-twitter-email/new_logicApp.png)

    | <span data-ttu-id="9a3be-173">設定</span><span class="sxs-lookup"><span data-stu-id="9a3be-173">Setting</span></span>      |  <span data-ttu-id="9a3be-174">建議的值</span><span class="sxs-lookup"><span data-stu-id="9a3be-174">Suggested value</span></span>   | <span data-ttu-id="9a3be-175">說明</span><span class="sxs-lookup"><span data-stu-id="9a3be-175">Description</span></span>                                        |
    | ----------------- | ------------ | ------------- |
    | <span data-ttu-id="9a3be-176">**名稱**</span><span class="sxs-lookup"><span data-stu-id="9a3be-176">**Name**</span></span> | <span data-ttu-id="9a3be-177">TweetSentiment</span><span class="sxs-lookup"><span data-stu-id="9a3be-177">TweetSentiment</span></span> | <span data-ttu-id="9a3be-178">為您的應用程式選擇適當名稱。</span><span class="sxs-lookup"><span data-stu-id="9a3be-178">Choose an appropriate name for your app.</span></span> |
    | <span data-ttu-id="9a3be-179">**資源群組**</span><span class="sxs-lookup"><span data-stu-id="9a3be-179">**Resource group**</span></span> | <span data-ttu-id="9a3be-180">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="9a3be-180">myResourceGroup</span></span> | <span data-ttu-id="9a3be-181">應用程式開發介面使用 tooanalyze 文字。</span><span class="sxs-lookup"><span data-stu-id="9a3be-181">API used tooanalyze text.</span></span>  |
    | <span data-ttu-id="9a3be-182">**位置**</span><span class="sxs-lookup"><span data-stu-id="9a3be-182">**Location**</span></span> | <span data-ttu-id="9a3be-183">美國東部</span><span class="sxs-lookup"><span data-stu-id="9a3be-183">East US</span></span> | <span data-ttu-id="9a3be-184">選擇位置關閉 tooyou。</span><span class="sxs-lookup"><span data-stu-id="9a3be-184">Choose a location close tooyou.</span></span> |
    | <span data-ttu-id="9a3be-185">**資源群組**</span><span class="sxs-lookup"><span data-stu-id="9a3be-185">**Resource group**</span></span> | <span data-ttu-id="9a3be-186">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="9a3be-186">myResourceGroup</span></span> | <span data-ttu-id="9a3be-187">選擇與之前 hello 相同的現有資源群組。</span><span class="sxs-lookup"><span data-stu-id="9a3be-187">Choose hello same existing resource group as before.</span></span>|

4. <span data-ttu-id="9a3be-188">按一下**建立**toocreate 邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="9a3be-188">Click **Create** toocreate your logic app.</span></span> <span data-ttu-id="9a3be-189">建立 hello 應用程式之後，按一下 新邏輯應用程式已釘選的 toohello 儀表板。</span><span class="sxs-lookup"><span data-stu-id="9a3be-189">After hello app is created, click your new logic app pinned toohello dashboard.</span></span> <span data-ttu-id="9a3be-190">在 hello 邏輯應用程式的設計工具中，向下捲動，然後按一下 hello**空白邏輯應用程式**範本。</span><span class="sxs-lookup"><span data-stu-id="9a3be-190">Then in hello Logic Apps Designer, scroll down and click hello **Blank Logic App** template.</span></span> 

    ![空白的 Logic Apps 範本](media/functions-twitter-email/blank.png)

<span data-ttu-id="9a3be-192">您現在可以使用 hello 邏輯應用程式設計師 tooadd 服務和觸發程序 tooyour 應用程式。</span><span class="sxs-lookup"><span data-stu-id="9a3be-192">You can now use hello Logic Apps Designer tooadd services and triggers tooyour app.</span></span>

## <a name="connect-tootwitter"></a><span data-ttu-id="9a3be-193">連接 tooTwitter</span><span class="sxs-lookup"><span data-stu-id="9a3be-193">Connect tooTwitter</span></span>

<span data-ttu-id="9a3be-194">首先，建立連接 tooyour Twitter 帳戶。</span><span class="sxs-lookup"><span data-stu-id="9a3be-194">First, create a connection tooyour Twitter account.</span></span> <span data-ttu-id="9a3be-195">觸發 hello 應用程式 toorun 推文輪詢 hello 邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="9a3be-195">hello logic app polls for tweets, which trigger hello app toorun.</span></span>

1. <span data-ttu-id="9a3be-196">在 hello 設計工具中，按一下 hello **Twitter**服務，然後按一下 hello**新推文回傳時**觸發程序。</span><span class="sxs-lookup"><span data-stu-id="9a3be-196">In hello designer, click hello **Twitter** service, and click hello **When a new tweet is posted** trigger.</span></span> <span data-ttu-id="9a3be-197">登入 tooyour Twitter 帳戶，並授權 Logic Apps toouse 您的帳戶。</span><span class="sxs-lookup"><span data-stu-id="9a3be-197">Sign in tooyour Twitter account and authorize Logic Apps toouse your account.</span></span>

2. <span data-ttu-id="9a3be-198">Hello 表指定方式使用 hello Twitter 觸發程序設定。</span><span class="sxs-lookup"><span data-stu-id="9a3be-198">Use hello Twitter trigger settings as specified in hello table.</span></span> 

    ![Twitter 連接器設定](media/functions-twitter-email/azure_tweet.png)

    | <span data-ttu-id="9a3be-200">設定</span><span class="sxs-lookup"><span data-stu-id="9a3be-200">Setting</span></span>      |  <span data-ttu-id="9a3be-201">建議的值</span><span class="sxs-lookup"><span data-stu-id="9a3be-201">Suggested value</span></span>   | <span data-ttu-id="9a3be-202">說明</span><span class="sxs-lookup"><span data-stu-id="9a3be-202">Description</span></span>                                        |
    | ----------------- | ------------ | ------------- |
    | <span data-ttu-id="9a3be-203">**搜尋文字**</span><span class="sxs-lookup"><span data-stu-id="9a3be-203">**Search text**</span></span> | <span data-ttu-id="9a3be-204">#Azure</span><span class="sxs-lookup"><span data-stu-id="9a3be-204">#Azure</span></span> | <span data-ttu-id="9a3be-205">使用雜湊標記 hello 選擇間隔內的熱門的 toogenerate 新推文。</span><span class="sxs-lookup"><span data-stu-id="9a3be-205">Use a hashtag that is popular enough for toogenerate new tweets in hello chosen interval.</span></span> <span data-ttu-id="9a3be-206">時使用 hello 免費層和您的雜湊標記太受歡迎，您可以快速地使用向上 hello 交易認知的服務帳戶中。</span><span class="sxs-lookup"><span data-stu-id="9a3be-206">When using hello Free tier and your hashtag is too popular, you can quickly use up hello transactions in your Cognitive Services account.</span></span> |
    | <span data-ttu-id="9a3be-207">**頻率**</span><span class="sxs-lookup"><span data-stu-id="9a3be-207">**Frequency**</span></span> | <span data-ttu-id="9a3be-208">分鐘</span><span class="sxs-lookup"><span data-stu-id="9a3be-208">Minute</span></span> | <span data-ttu-id="9a3be-209">用來輪詢 Twitter hello 頻率單位。</span><span class="sxs-lookup"><span data-stu-id="9a3be-209">hello frequency unit used for polling Twitter.</span></span>  |
    | <span data-ttu-id="9a3be-210">**間隔**</span><span class="sxs-lookup"><span data-stu-id="9a3be-210">**Interval**</span></span> | <span data-ttu-id="9a3be-211">15</span><span class="sxs-lookup"><span data-stu-id="9a3be-211">15</span></span> | <span data-ttu-id="9a3be-212">中的頻率單位的 Twitter 要求之間所經過的 hello 時間。</span><span class="sxs-lookup"><span data-stu-id="9a3be-212">hello time elapsed between Twitter requests, in frequency units.</span></span> |

3.  <span data-ttu-id="9a3be-213">按一下**儲存**tooconnect tooyour Twitter 帳戶。</span><span class="sxs-lookup"><span data-stu-id="9a3be-213">Click **Save** tooconnect tooyour Twitter account.</span></span> 

<span data-ttu-id="9a3be-214">現在您的應用程式是已連線的 tooTwitter。</span><span class="sxs-lookup"><span data-stu-id="9a3be-214">Now your app is connected tooTwitter.</span></span> <span data-ttu-id="9a3be-215">接下來，您可以連接 tootext 分析 toodetect hello 人氣的收集推文。</span><span class="sxs-lookup"><span data-stu-id="9a3be-215">Next, you connect tootext analytics toodetect hello sentiment of collected tweets.</span></span>

## <a name="add-sentiment-detection"></a><span data-ttu-id="9a3be-216">新增情感偵測</span><span class="sxs-lookup"><span data-stu-id="9a3be-216">Add sentiment detection</span></span>

1. <span data-ttu-id="9a3be-217">依序按一下 [新增步驟]、[新增動作]。</span><span class="sxs-lookup"><span data-stu-id="9a3be-217">Click **New Step**, and then **Add an action**.</span></span>

    ![選取 [新增步驟]，然後選取 [新增動作]](media/functions-twitter-email/new_step.png)

2. <span data-ttu-id="9a3be-219">在**選擇動作**，按一下 **文字分析**，然後按一下hello**偵測人氣**動作。</span><span class="sxs-lookup"><span data-stu-id="9a3be-219">In **Choose an action**, click **Text Analytics**, and then click hello **Detect sentiment** action.</span></span>

    ![偵測情感](media/functions-twitter-email/detect_sent.png)

3. <span data-ttu-id="9a3be-221">輸入連線名稱，例如`MyCognitiveServicesConnection`，貼上 hello 金鑰，為您認知的服務帳戶儲存，然後按一下**建立**。</span><span class="sxs-lookup"><span data-stu-id="9a3be-221">Type a connection name such as `MyCognitiveServicesConnection`, paste hello key for your Cognitive Services account that you saved, and click **Create**.</span></span>  

4. <span data-ttu-id="9a3be-222">按一下**文字 tooanalyze** > **推文提供文字**，然後按一下**儲存**。</span><span class="sxs-lookup"><span data-stu-id="9a3be-222">Click **Text tooanalyze** > **Tweet text**, and then click **Save**.</span></span>  

    ![偵測情感](media/functions-twitter-email/ds_tta.png)

<span data-ttu-id="9a3be-224">人氣偵測設定時，您可以新增取用 hello 人氣分數輸出連線 tooyour 函式。</span><span class="sxs-lookup"><span data-stu-id="9a3be-224">Now that sentiment detection is configured, you can add a connection tooyour function that consumes hello sentiment score output.</span></span>

## <a name="connect-sentiment-output-tooyour-function"></a><span data-ttu-id="9a3be-225">連接 人氣輸出 tooyour 函式</span><span class="sxs-lookup"><span data-stu-id="9a3be-225">Connect sentiment output tooyour function</span></span>

1. <span data-ttu-id="9a3be-226">在 hello 邏輯應用程式的設計工具中，按一下 **新步驟** > **將動作加入**，然後按一下 **Azure 函式**。</span><span class="sxs-lookup"><span data-stu-id="9a3be-226">In hello Logic Apps Designer, click **New step** > **Add an action**, and then click **Azure Functions**.</span></span> 

2. <span data-ttu-id="9a3be-227">按一下**選擇 Azure 的函式**，選取 hello **CategorizeSentiment**您稍早建立的函式。</span><span class="sxs-lookup"><span data-stu-id="9a3be-227">Click **Choose an Azure function**, select hello **CategorizeSentiment** function you created earlier.</span></span>  

    ![顯示 [選擇 Azure 函式] 的 Azure 函式方塊](media/functions-twitter-email/choose_fun.png)

3. <span data-ttu-id="9a3be-229">在**要求本文**中，依序按一下 [分數] 和 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="9a3be-229">In **Request Body**, click **Score** and then **Save**.</span></span>

    ![分數](media/functions-twitter-email/trigger_score.png)

<span data-ttu-id="9a3be-231">現在，您的函式會從 hello 邏輯應用程式傳送的人氣分數時觸發。</span><span class="sxs-lookup"><span data-stu-id="9a3be-231">Now, your function is triggered when a sentiment score is sent from hello logic app.</span></span> <span data-ttu-id="9a3be-232">色彩編碼的類別目錄的 hello 函式，會傳回 toohello 邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="9a3be-232">A color-coded category is returned toohello logic app by hello function.</span></span> <span data-ttu-id="9a3be-233">接下來，您加入的人氣值時，會傳送電子郵件通知**紅色**hello 函式會傳回。</span><span class="sxs-lookup"><span data-stu-id="9a3be-233">Next, you add an email notification that is sent when a sentiment value of **RED** is returned from hello function.</span></span> 

## <a name="add-email-notifications"></a><span data-ttu-id="9a3be-234">新增電子郵件通知</span><span class="sxs-lookup"><span data-stu-id="9a3be-234">Add email notifications</span></span>

<span data-ttu-id="9a3be-235">hello 最後一部分 hello 工作流程時，tootrigger 電子郵件做為計分 hello 人氣_紅色_。</span><span class="sxs-lookup"><span data-stu-id="9a3be-235">hello last part of hello workflow is tootrigger an email when hello sentiment is scored as _RED_.</span></span> <span data-ttu-id="9a3be-236">本主題是使用 Outlook.com 連接器。</span><span class="sxs-lookup"><span data-stu-id="9a3be-236">This topic uses an Outlook.com connector.</span></span> <span data-ttu-id="9a3be-237">您可以執行類似的步驟 toouse Gmail 或 Office 365 Outlook 連接器。</span><span class="sxs-lookup"><span data-stu-id="9a3be-237">You can perform similar steps toouse a Gmail or Office 365 Outlook connector.</span></span>   

1. <span data-ttu-id="9a3be-238">在 hello 邏輯應用程式的設計工具中，按一下 **新步驟** > **加入條件**。</span><span class="sxs-lookup"><span data-stu-id="9a3be-238">In hello Logic Apps Designer, click **New step** > **Add a condition**.</span></span> 

2. <span data-ttu-id="9a3be-239">按一下 [選擇值]，然後按一下 [本文]。</span><span class="sxs-lookup"><span data-stu-id="9a3be-239">Click **Choose a value**, then click **Body**.</span></span> <span data-ttu-id="9a3be-240">選取 [等於]、按一下 [選擇值] 並輸入 `RED`，然後按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="9a3be-240">Select **is equal to**, click **Choose a value** and type `RED`, and click **Save**.</span></span> 

    ![加入條件 toohello 邏輯應用程式。](media/functions-twitter-email/condition.png)

3. <span data-ttu-id="9a3be-242">在**如果是，不執行任何動作**，按一下 **將動作加入**，搜尋`outlook.com`，按一下 **傳送電子郵件**，並登入 tooyour Outlook.com 帳戶。</span><span class="sxs-lookup"><span data-stu-id="9a3be-242">In **IF YES, DO NOTHING**, click **Add an action**, search for `outlook.com`, click **Send an email**, and sign in tooyour Outlook.com account.</span></span>
    
    ![選擇 hello 條件的動作。](media/functions-twitter-email/outlook.png)

    > [!NOTE]
    > <span data-ttu-id="9a3be-244">如果您沒有 Outlook.com 帳戶，可以選擇另一個連接器，例如 Gmail 或 Office 365 Outlook</span><span class="sxs-lookup"><span data-stu-id="9a3be-244">If you don't have an Outlook.com account, you can choose another connector, such as Gmail or Office 365 Outlook</span></span>

4. <span data-ttu-id="9a3be-245">在 hello**傳送電子郵件**hello 資料表中指定的動作，以使用 hello 電子郵件設定。</span><span class="sxs-lookup"><span data-stu-id="9a3be-245">In hello **Send an email** action, use hello email settings as specified in hello table.</span></span> 

    ![設定 hello 傳送電子郵件動作的 hello 電子郵件。](media/functions-twitter-email/sendemail.png)

    | <span data-ttu-id="9a3be-247">設定</span><span class="sxs-lookup"><span data-stu-id="9a3be-247">Setting</span></span>      |  <span data-ttu-id="9a3be-248">建議的值</span><span class="sxs-lookup"><span data-stu-id="9a3be-248">Suggested value</span></span>   | <span data-ttu-id="9a3be-249">說明</span><span class="sxs-lookup"><span data-stu-id="9a3be-249">Description</span></span>  |
    | ----------------- | ------------ | ------------- |
    | <span data-ttu-id="9a3be-250">**To**</span><span class="sxs-lookup"><span data-stu-id="9a3be-250">**To**</span></span> | <span data-ttu-id="9a3be-251">輸入您的電子郵件地址</span><span class="sxs-lookup"><span data-stu-id="9a3be-251">Type your email address</span></span> | <span data-ttu-id="9a3be-252">收到 hello 通知的 hello 電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="9a3be-252">hello email address that receives hello notification.</span></span> |
    | <span data-ttu-id="9a3be-253">**主旨**</span><span class="sxs-lookup"><span data-stu-id="9a3be-253">**Subject**</span></span> | <span data-ttu-id="9a3be-254">偵測到負面的推文情感</span><span class="sxs-lookup"><span data-stu-id="9a3be-254">Negative tweet sentiment detected</span></span>  | <span data-ttu-id="9a3be-255">hello hello 電子郵件通知的主旨列。</span><span class="sxs-lookup"><span data-stu-id="9a3be-255">hello subject line of hello email notification.</span></span>  |
    | <span data-ttu-id="9a3be-256">**內文**</span><span class="sxs-lookup"><span data-stu-id="9a3be-256">**Body**</span></span> | <span data-ttu-id="9a3be-257">推文文字、位置</span><span class="sxs-lookup"><span data-stu-id="9a3be-257">Tweet text, Location</span></span> | <span data-ttu-id="9a3be-258">按一下 hello**推文提供文字**和**位置**參數。</span><span class="sxs-lookup"><span data-stu-id="9a3be-258">Click hello **Tweet text** and **Location** parameters.</span></span> |

5.  <span data-ttu-id="9a3be-259">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="9a3be-259">Click **Save**.</span></span>

<span data-ttu-id="9a3be-260">既然 hello 工作流程已完成，您可以啟用 hello 邏輯應用程式，並查看工作的 hello 函式。</span><span class="sxs-lookup"><span data-stu-id="9a3be-260">Now that hello workflow is complete, you can enable hello logic app and see hello function at work.</span></span>

## <a name="test-hello-workflow"></a><span data-ttu-id="9a3be-261">測試 hello 工作流程</span><span class="sxs-lookup"><span data-stu-id="9a3be-261">Test hello workflow</span></span>

1. <span data-ttu-id="9a3be-262">在 hello 邏輯應用程式的設計工具中，按一下 **執行**toostart hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="9a3be-262">In hello Logic App Designer, click **Run** toostart hello app.</span></span>

2. <span data-ttu-id="9a3be-263">在 hello 左側資料行，按一下 **概觀**toosee hello hello 邏輯應用程式狀態。</span><span class="sxs-lookup"><span data-stu-id="9a3be-263">In hello left column, click **Overview** toosee hello status of hello logic app.</span></span> 
 
    ![邏輯應用程式執行狀態](media/functions-twitter-email/over1.png)

3. <span data-ttu-id="9a3be-265">（選擇性）按一下其中一個 hello hello 執行的執行 toosee 詳細資料。</span><span class="sxs-lookup"><span data-stu-id="9a3be-265">(Optional) Click one of hello runs toosee details of hello execution.</span></span>

4. <span data-ttu-id="9a3be-266">移 tooyour 函式、 檢視 hello 記錄檔，並確認人氣值已接收及處理。</span><span class="sxs-lookup"><span data-stu-id="9a3be-266">Go tooyour function, view hello logs, and verify that sentiment values were received and processed.</span></span>
 
    ![檢視函式記錄](media/functions-twitter-email/sent.png)

5. <span data-ttu-id="9a3be-268">偵測到潛在的負面情感時，您會收到一封電子郵件。</span><span class="sxs-lookup"><span data-stu-id="9a3be-268">When a potentially negative sentiment is detected, you receive an email.</span></span> <span data-ttu-id="9a3be-269">如果您尚未收到一封電子郵件，您可以變更 hello 函式程式碼 tooreturn 紅色每次：</span><span class="sxs-lookup"><span data-stu-id="9a3be-269">If you haven't received an email, you can change hello function code tooreturn RED every time:</span></span>

        return req.CreateResponse(HttpStatusCode.OK, "RED");

    <span data-ttu-id="9a3be-270">驗證電子郵件通知後，變更後 toohello 原始的程式碼：</span><span class="sxs-lookup"><span data-stu-id="9a3be-270">After you have verified email notifications, change back toohello original code:</span></span>

        return req.CreateResponse(HttpStatusCode.OK, category);

    > [!IMPORTANT]
    > <span data-ttu-id="9a3be-271">完成本教學課程之後，您應該停用 hello 邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="9a3be-271">After you have completed this tutorial, you should disable hello logic app.</span></span> <span data-ttu-id="9a3be-272">停用 hello 應用程式，您可以避免正在充電執行，並使用向上 hello 認知的服務帳戶中的交易。</span><span class="sxs-lookup"><span data-stu-id="9a3be-272">By disabling hello app, you avoid being charged for executions and using up hello transactions in your Cognitive Services account.</span></span>

<span data-ttu-id="9a3be-273">現在您已經知道是多麼的輕鬆成的 Logic Apps 工作流程的 toointegrate 函式。</span><span class="sxs-lookup"><span data-stu-id="9a3be-273">Now you have seen how easy it is toointegrate Functions into a Logic Apps workflow.</span></span>

## <a name="disable-hello-logic-app"></a><span data-ttu-id="9a3be-274">停用 hello 邏輯應用程式</span><span class="sxs-lookup"><span data-stu-id="9a3be-274">Disable hello logic app</span></span>

<span data-ttu-id="9a3be-275">toodisable hello 邏輯應用程式中，按一下 **概觀**，然後按一下**停用**頂端 hello 囉 」 畫面。</span><span class="sxs-lookup"><span data-stu-id="9a3be-275">toodisable hello logic app, click **Overview** and then click **Disable** at hello top of hello screen.</span></span> <span data-ttu-id="9a3be-276">這會停止執行，而且會產生費用，而不刪除 hello 應用程式中的 hello 邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="9a3be-276">This stops hello logic app from running and incurring charges without deleting hello app.</span></span> 

![函式記錄](media/functions-twitter-email/disable-logic-app.png)

## <a name="next-steps"></a><span data-ttu-id="9a3be-278">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9a3be-278">Next steps</span></span>

<span data-ttu-id="9a3be-279">在本教學課程中，您已了解如何：</span><span class="sxs-lookup"><span data-stu-id="9a3be-279">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="9a3be-280">建立辨識服務帳戶。</span><span class="sxs-lookup"><span data-stu-id="9a3be-280">Create a Cognitive Services account.</span></span>
> * <span data-ttu-id="9a3be-281">建立可將推文情感進行分類的函式。</span><span class="sxs-lookup"><span data-stu-id="9a3be-281">Create a function that categorizes tweet sentiment.</span></span>
> * <span data-ttu-id="9a3be-282">建立連接 tooTwitter 邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="9a3be-282">Create a logic app that connects tooTwitter.</span></span>
> * <span data-ttu-id="9a3be-283">加入 人氣偵測 toohello 邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="9a3be-283">Add sentiment detection toohello logic app.</span></span> 
> * <span data-ttu-id="9a3be-284">連接 hello 邏輯應用程式 toohello 函式。</span><span class="sxs-lookup"><span data-stu-id="9a3be-284">Connect hello logic app toohello function.</span></span>
> * <span data-ttu-id="9a3be-285">傳送 hello 回應 hello 函式為基礎的電子郵件。</span><span class="sxs-lookup"><span data-stu-id="9a3be-285">Send an email based on hello response from hello function.</span></span>

<span data-ttu-id="9a3be-286">如何前進 toohello 下一個教學課程 toolearn toocreate 無伺服器的應用程式開發介面，針對您的函式。</span><span class="sxs-lookup"><span data-stu-id="9a3be-286">Advance toohello next tutorial toolearn how toocreate a serverless API for your function.</span></span>

> [!div class="nextstepaction"] 
> [<span data-ttu-id="9a3be-287">使用 Azure Functions 建立無伺服器 API</span><span class="sxs-lookup"><span data-stu-id="9a3be-287">Create a serverless API using Azure Functions</span></span>](functions-create-serverless-api.md)

<span data-ttu-id="9a3be-288">toolearn 進一步了解邏輯應用程式，請參閱[Azure Logic Apps](../logic-apps/logic-apps-what-are-logic-apps.md)。</span><span class="sxs-lookup"><span data-stu-id="9a3be-288">toolearn more about Logic Apps, see [Azure Logic Apps](../logic-apps/logic-apps-what-are-logic-apps.md).</span></span>

