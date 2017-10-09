---
title: "使用 Azure Stream Analytics aaaReal 時間 Twitter 情緒分析 |Microsoft 文件"
description: "深入了解如何 toouse 資料流分析的即時 Twitter 情緒分析。 從即時儀表板上的事件產生 toodata 的逐步指引。"
keywords: "即時的 twitter 趨勢分析, 情感分析, 社交媒體分析, 趨勢分析範例"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 42068691-074b-4c3b-a527-acafa484fda2
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: jeffstok
ms.openlocfilehash: 157790caa7ea6f5570dd9c9d3bd9694d437eb4c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="real-time-twitter-sentiment-analysis-in-azure-stream-analytics"></a><span data-ttu-id="b2ddd-105">Azure 串流分析中的即時 Twitter 情感分析</span><span class="sxs-lookup"><span data-stu-id="b2ddd-105">Real-time Twitter sentiment analysis in Azure Stream Analytics</span></span>

<span data-ttu-id="b2ddd-106">深入了解如何 toobuild 社交媒體分析透過將即時的人氣分析解決方案 Twitter 到 Azure 事件中心的事件。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-106">Learn how toobuild a sentiment analysis solution for social media analytics by bringing real-time Twitter events into Azure Event Hubs.</span></span> <span data-ttu-id="b2ddd-107">然後您可以撰寫 Azure Stream Analytics 查詢 tooanalyze hello 資料和其中一個存放區 hello 結果以供稍後使用，或使用 儀表板和[Power BI](https://powerbi.com/) tooprovide 即時的深入資訊。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-107">You can then write an Azure Stream Analytics query tooanalyze hello data and either store hello results for later use or use a dashboard and [Power BI](https://powerbi.com/) tooprovide insights in real time.</span></span>

<span data-ttu-id="b2ddd-108">社交媒體分析工具可協助組織了解熱門話題。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-108">Social media analytics tools help organizations understand trending topics.</span></span> <span data-ttu-id="b2ddd-109">熱門話題就是在社交媒體中有大量文章的話題及意見。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-109">Trending topics are subjects and attitudes that have a high volume of posts in social media.</span></span> <span data-ttu-id="b2ddd-110">情緒分析，也稱為*意見採礦*，會使用社交媒體分析工具 toodetermine 態度產品、 概念，和等等。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-110">Sentiment analysis, which is also called *opinion mining*, uses social media analytics tools toodetermine attitudes toward a product, idea, and so on.</span></span> 

<span data-ttu-id="b2ddd-111">即時 Twitter 趨勢分析會分析工具的絕佳範例，因為 hello 雜湊標記訂閱模型可讓您 toolisten toospecific 關鍵字 （雜湊標記），並開發情緒分析的 hello 摘要。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-111">Real-time Twitter trend analysis is a great example of an analytics tool, because hello hashtag subscription model enables you toolisten toospecific keywords (hashtags) and develop sentiment analysis of hello feed.</span></span>

## <a name="scenario-social-media-sentiment-analysis-in-real-time"></a><span data-ttu-id="b2ddd-112">案例：即時的社交媒體情感分析</span><span class="sxs-lookup"><span data-stu-id="b2ddd-112">Scenario: Social media sentiment analysis in real time</span></span>

<span data-ttu-id="b2ddd-113">具有新聞媒體網站的公司有興趣，藉以沿用立即相關 tooits 讀取器的站台內容取得競爭對手與眾不同的優勢。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-113">A company that has a news media website is interested in gaining an advantage over its competitors by featuring site content that is immediately relevant tooits readers.</span></span> <span data-ttu-id="b2ddd-114">hello 公司使用社交媒體分析上執行的 Twitter 資料的即時情緒分析 tooreaders 相關的主題。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-114">hello company uses social media analysis on topics that are relevant tooreaders by doing real-time sentiment analysis of Twitter data.</span></span>

<span data-ttu-id="b2ddd-115">在 Twitter 上的即時 tooidentify 趨勢主題 hello hello 推文中的磁碟區和人氣的重要主題的相關公司需求即時分析。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-115">tooidentify trending topics in real time on Twitter, hello company needs real-time analytics about hello tweet volume and sentiment for key topics.</span></span> <span data-ttu-id="b2ddd-116">換句話說，hello 需要是此摘要的社交媒體為基礎的人氣分析分析引擎。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-116">In other words, hello need is a sentiment analysis analytics engine that's based on this social media feed.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b2ddd-117">必要條件</span><span class="sxs-lookup"><span data-stu-id="b2ddd-117">Prerequisites</span></span>
<span data-ttu-id="b2ddd-118">在本教學課程中，您可以使用用戶端應用程式的連接 tooTwitter，尋找具有特定雜湊標記 （此您可以設定） 推文。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-118">In this tutorial, you use a client application that connects tooTwitter and looks for tweets that have certain hashtags (which you can set).</span></span> <span data-ttu-id="b2ddd-119">順序 toorun hello 應用程式，並分析使用 Azure 串流分析推文，您必須擁有 hello 下列 hello:</span><span class="sxs-lookup"><span data-stu-id="b2ddd-119">In order toorun hello application and analyze hello tweets using Azure Streaming Analytics, you must have hello following:</span></span>

* <span data-ttu-id="b2ddd-120">Azure 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="b2ddd-120">An Azure subscription</span></span>
* <span data-ttu-id="b2ddd-121">Twitter 帳戶</span><span class="sxs-lookup"><span data-stu-id="b2ddd-121">A Twitter account</span></span> 
* <span data-ttu-id="b2ddd-122">Twitter 應用程式和 hello [OAuth 存取權杖](https://dev.twitter.com/oauth/overview/application-owner-access-tokens)該應用程式。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-122">A Twitter application, and hello [OAuth access token](https://dev.twitter.com/oauth/overview/application-owner-access-tokens) for that application.</span></span> <span data-ttu-id="b2ddd-123">我們提供高層級的相關指示如何 toocreate Twitter 應用程式更新版本。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-123">We provide high-level instructions for how toocreate a Twitter application later.</span></span>
* <span data-ttu-id="b2ddd-124">hello TwitterWPFClient 應用程式，它會讀取 hello Twitter 摘要。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-124">hello TwitterWPFClient application, which reads hello Twitter feed.</span></span> <span data-ttu-id="b2ddd-125">tooget 此應用程式，下載 hello [TwitterWPFClient.zip](https://github.com/Azure/azure-stream-analytics/blob/master/Samples/TwitterClient/TwitterWPFClient.zip)從 GitHub 檔案，然後再將 hello 封裝解壓縮至您的電腦上的資料夾。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-125">tooget this application, download hello [TwitterWPFClient.zip](https://github.com/Azure/azure-stream-analytics/blob/master/Samples/TwitterClient/TwitterWPFClient.zip) file from GitHub and then unzip hello package into a folder on your computer.</span></span> <span data-ttu-id="b2ddd-126">如果您想 toosee hello 原始程式碼和 hello 中執行應用程式偵錯工具，就可以從 hello 原始程式碼[GitHub](https://aka.ms/azure-stream-analytics-telcogenerator)。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-126">If you want toosee hello source code and run hello application in a debugger, you can get hello source code from [GitHub](https://aka.ms/azure-stream-analytics-telcogenerator).</span></span> 

## <a name="create-an-event-hub-for-streaming-analytics-input"></a><span data-ttu-id="b2ddd-127">建立串流分析輸入的事件中樞</span><span class="sxs-lookup"><span data-stu-id="b2ddd-127">Create an event hub for Streaming Analytics input</span></span>

<span data-ttu-id="b2ddd-128">hello 範例應用程式會產生事件，並將它們推送 tooan Azure 事件中樞。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-128">hello sample application generates events and pushes them tooan Azure event hub.</span></span> <span data-ttu-id="b2ddd-129">Azure 事件中心是事件擷取的資料流分析 hello 慣用方法。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-129">Azure event hubs are hello preferred method of event ingestion for Stream Analytics.</span></span> <span data-ttu-id="b2ddd-130">如需詳細資訊，請參閱 hello [Azure 事件中心文件](../event-hubs/event-hubs-what-is-event-hubs.md)。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-130">For more information, see hello [Azure Event Hubs documentation](../event-hubs/event-hubs-what-is-event-hubs.md).</span></span>


### <a name="create-an-event-hub-namespace-and-event-hub"></a><span data-ttu-id="b2ddd-131">建立事件中樞命名空間和事件中樞</span><span class="sxs-lookup"><span data-stu-id="b2ddd-131">Create an event hub namespace and event hub</span></span>
<span data-ttu-id="b2ddd-132">在此程序，您先建立事件中樞命名空間中，並將事件中樞 toothat 命名空間。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-132">In this procedure, you first create an event hub namespace, and then you add an event hub toothat namespace.</span></span> <span data-ttu-id="b2ddd-133">事件中樞命名空間用 toologically 群組相關的事件匯流排執行個體。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-133">Event hub namespaces are used toologically group related event bus instances.</span></span> 

1. <span data-ttu-id="b2ddd-134">登入 toohello Azure 入口網站，然後按一下**新增** > **物聯網** > **事件中心**。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-134">Log  in toohello Azure portal and click **New** > **Internet of Things** > **Event Hub**.</span></span> 

2. <span data-ttu-id="b2ddd-135">在 hello**建立命名空間**刀鋒視窗中，輸入命名空間名稱，例如`<yourname>-socialtwitter-eh-ns`。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-135">In hello **Create namespace** blade, enter a namespace name such as `<yourname>-socialtwitter-eh-ns`.</span></span> <span data-ttu-id="b2ddd-136">您可以使用任何名稱，如 hello 命名空間，但是 hello 名稱必須是有效的 URL，而且它必須是唯一的 Azure。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-136">You can use any name for hello namespace, but hello name must be valid for a URL and it must be unique across Azure.</span></span> 
    
3. <span data-ttu-id="b2ddd-137">選取訂用帳戶並建立或選擇資源群組，然後按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-137">Select a subscription and create or choose a resource group, then click **Create**.</span></span> 

    ![建立事件中樞命名空間](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-create-eventhub-namespace.png)
 
4. <span data-ttu-id="b2ddd-139">當部署完成 hello 命名空間時，尋找 hello 事件中樞命名空間清單中的 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-139">When hello namespace has finished deploying, find hello event hub namespace in your list of Azure resources.</span></span> 

5. <span data-ttu-id="b2ddd-140">按一下 hello 新命名空間，然後在 hello 命名空間刀鋒視窗中，按一下 **+&nbsp;事件中心**。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-140">Click hello new namespace, and in hello namespace blade, click **+&nbsp;Event Hub**.</span></span> 

    ![<span data-ttu-id="b2ddd-141">hello 新增事件中樞按鈕建立新的事件中樞</span><span class="sxs-lookup"><span data-stu-id="b2ddd-141">hello Add Event Hub button for creating a new event hub</span></span> ](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-create-eventhub-button.png)    
 
6. <span data-ttu-id="b2ddd-142">名稱資料行 hello 新的事件中樞`socialtwitter-eh`。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-142">Name hello new event hub `socialtwitter-eh`.</span></span> <span data-ttu-id="b2ddd-143">您可以使用不同的名稱。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-143">You can use a different name.</span></span> <span data-ttu-id="b2ddd-144">如果您這樣做，請記錄下來，因為您稍後需要 hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-144">If you do, make a note of it, because you need hello name later.</span></span> <span data-ttu-id="b2ddd-145">您不需要 tooset 任何其他選項，hello 事件中心。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-145">You don't need tooset any other options for hello event hub.</span></span>

    ![建立新事件中樞的刀鋒視窗](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-create-eventhub.png)
 
7. <span data-ttu-id="b2ddd-147">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-147">Click **Create**.</span></span>


### <a name="grant-access-toohello-event-hub"></a><span data-ttu-id="b2ddd-148">授與存取 toohello 事件中樞</span><span class="sxs-lookup"><span data-stu-id="b2ddd-148">Grant access toohello event hub</span></span>

<span data-ttu-id="b2ddd-149">處理程序可以傳送資料 tooan 事件中心之前，hello 事件中心必須要有原則，可讓適當的存取權。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-149">Before a process can send data tooan event hub, hello event hub must have a policy that allows appropriate access.</span></span> <span data-ttu-id="b2ddd-150">hello 存取原則會產生包含授權資訊的連接字串。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-150">hello access policy produces a connection string that includes authorization information.</span></span>

1.  <span data-ttu-id="b2ddd-151">在 hello 事件命名空間刀鋒視窗中，按一下 **事件中心**，然後按一下新的事件中樞的 hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-151">In hello event namespace blade, click **Event Hubs** and then click hello name of your new event hub.</span></span>

2.  <span data-ttu-id="b2ddd-152">在 hello 事件中樞刀鋒視窗中，按一下 **共用存取原則**，然後按一下  **+&nbsp;新增**。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-152">In hello event hub blade, click **Shared access policies** and then click **+&nbsp;Add**.</span></span>

    >[!NOTE]
    ><span data-ttu-id="b2ddd-153">請確定您正在使用 hello 事件中心不 hello 事件中樞命名空間。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-153">Make sure you're working with hello event hub, not hello event hub namespace.</span></span>

3.  <span data-ttu-id="b2ddd-154">新增名為 `socialtwitter-access` 的原則，然後在 [宣告] 中，選取 [管理]。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-154">Add a policy named `socialtwitter-access` and for **Claim**, select **Manage**.</span></span>

    ![建立新事件中樞存取原則的刀鋒視窗](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-create-shared-access-policy-manage.png)
 
4.  <span data-ttu-id="b2ddd-156">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-156">Click **Create**.</span></span>

5.  <span data-ttu-id="b2ddd-157">Hello 原則已部署之後，請按一下它在 hello 清單中的共用的存取原則。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-157">After hello policy has been deployed, click it in hello list of shared access policies.</span></span>

6.  <span data-ttu-id="b2ddd-158">尋找 hello 方塊標示為**連接字串-主索引鍵**按一下 hello 複製按鈕下一步 toohello 連接字串。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-158">Find hello box labeled **CONNECTION STRING-PRIMARY KEY** and click hello copy button next toohello connection string.</span></span> 
    
    ![複製 hello 主要連接字串索引鍵與 hello 存取原則](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-shared-access-policy-copy-connection-string.png)
 
7.  <span data-ttu-id="b2ddd-160">貼入文字編輯器中的 hello 連接字串。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-160">Paste hello connection string into a text editor.</span></span> <span data-ttu-id="b2ddd-161">Hello 下一節中，進行一些稍微修改 tooit 之後，您需要開啟這個連接字串。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-161">You need this connection string for hello next section, after you make some small edits tooit.</span></span>

    <span data-ttu-id="b2ddd-162">hello 連接字串看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="b2ddd-162">hello connection string looks like this:</span></span>

        Endpoint=sb://YOURNAME-socialtwitter-eh-ns.servicebus.windows.net/;SharedAccessKeyName=socialtwitter-access;SharedAccessKey=Gw2NFZw6r...FxKbXaC2op6a0ZsPkI=;EntityPath=socialtwitter-eh

    <span data-ttu-id="b2ddd-163">請注意 hello 連接字串包含多個索引鍵-值組，並以分號分隔： `Endpoint`， `SharedAccessKeyName`， `SharedAccessKey`，和`EntityPath`。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-163">Notice that hello connection string contains multiple key-value pairs, separated with semicolons: `Endpoint`, `SharedAccessKeyName`, `SharedAccessKey`, and `EntityPath`.</span></span>  

    > [!NOTE]
    > <span data-ttu-id="b2ddd-164">為了安全性，已移除 hello hello 範例中的連接字串部分。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-164">For security, parts of hello connection string in hello example have been removed.</span></span>

8.  <span data-ttu-id="b2ddd-165">Hello 文字編輯器中，移除 hello`EntityPath`組來自 hello 連接字串 （別忘了在它之前的 tooremove hello 分號）。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-165">In hello text editor, remove hello `EntityPath` pair from hello connection string (don't forget tooremove hello semicolon that precedes it).</span></span> <span data-ttu-id="b2ddd-166">當您完成時，hello 連接字串看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="b2ddd-166">When you're done, hello connection string looks like this:</span></span>

        Endpoint=sb://YOURNAME-socialtwitter-eh-ns.servicebus.windows.net/;SharedAccessKeyName=socialtwitter-access;SharedAccessKey=Gw2NFZw6r...FxKbXaC2op6a0ZsPkI=


## <a name="configure-and-start-hello-twitter-client-application"></a><span data-ttu-id="b2ddd-167">設定並啟動 hello Twitter 用戶端應用程式</span><span class="sxs-lookup"><span data-stu-id="b2ddd-167">Configure and start hello Twitter client application</span></span>
<span data-ttu-id="b2ddd-168">hello 用戶端應用程式直接從 Twitter 取得推文中的事件。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-168">hello client application gets tweet events directly from Twitter.</span></span> <span data-ttu-id="b2ddd-169">在順序 toodo 因此，它需要的權限 toocall hello Twitter 串流處理應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-169">In order toodo so, it needs permission toocall hello Twitter Streaming APIs.</span></span> <span data-ttu-id="b2ddd-170">tooconfigure 權限，您的應用程式中建立 Twitter，會產生唯一的認證 （例如 OAuth 語彙基元）。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-170">tooconfigure that permission, you create an application in Twitter, which generates unique credentials (such as an OAuth token).</span></span> <span data-ttu-id="b2ddd-171">您可以設定 hello 用戶端應用程式 toouse 這些認證時讓它在應用程式開發介面呼叫。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-171">You can then configure hello client application toouse these credentials when it makes API calls.</span></span> 

### <a name="create-a-twitter-application"></a><span data-ttu-id="b2ddd-172">建立 Twitter 應用程式</span><span class="sxs-lookup"><span data-stu-id="b2ddd-172">Create a Twitter application</span></span>
<span data-ttu-id="b2ddd-173">如果您還沒有可用於本教學課程的 Twitter 應用程式，您可以建立一個。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-173">If you do not already have a Twitter application that you can use for this tutorial, you can create one.</span></span> <span data-ttu-id="b2ddd-174">您必須已經有 Twitter 帳戶。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-174">You must already have a Twitter account.</span></span>

> [!NOTE]
> <span data-ttu-id="b2ddd-175">在 Twitter 來建立應用程式，並取得 hello 金鑰、 密碼和語彙基元 hello 確切的程序可能會變更。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-175">hello exact process in Twitter for creating an application and getting hello keys, secrets, and token might change.</span></span> <span data-ttu-id="b2ddd-176">如果這些指示不符合 hello Twitter 網站上看到的內容，請參閱 toohello Twitter 開發人員文件。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-176">If these instructions don't match what you see on hello Twitter site, refer toohello Twitter developer documentation.</span></span>

1. <span data-ttu-id="b2ddd-177">移 toohello [Twitter 應用程式管理頁面](https://apps.twitter.com/)。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-177">Go toohello [Twitter application management page](https://apps.twitter.com/).</span></span> 

2. <span data-ttu-id="b2ddd-178">建立新的應用程式。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-178">Create a new application.</span></span> 

    * <span data-ttu-id="b2ddd-179">對於 hello 網站 URL，請指定有效的 URL。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-179">For hello website URL, specify a valid URL.</span></span> <span data-ttu-id="b2ddd-180">它並沒有 toobe 即時網站。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-180">It does not have toobe a live site.</span></span> <span data-ttu-id="b2ddd-181">(您不能只指定 `localhost`。)</span><span class="sxs-lookup"><span data-stu-id="b2ddd-181">(You can't specify just `localhost`.)</span></span>
    * <span data-ttu-id="b2ddd-182">將 hello 回呼欄位保留空白。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-182">Leave hello callback field blank.</span></span> <span data-ttu-id="b2ddd-183">您使用此教學課程中的 hello 用戶端應用程式不需要的回呼。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-183">hello client application you use for this tutorial doesn't require callbacks.</span></span>

    ![在 Twitter 中建立應用程式](./media/stream-analytics-twitter-sentiment-analysis-trends/create-twitter-application.png)

3. <span data-ttu-id="b2ddd-185">（選擇性） 變更 tooread 專用的 hello 應用程式的權限。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-185">Optionally, change hello application's permissions tooread-only.</span></span>

4. <span data-ttu-id="b2ddd-186">建立 hello 應用程式時，請移 toohello**機碼和存取權杖**頁面。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-186">When hello application is created, go toohello **Keys and Access Tokens** page.</span></span>

5. <span data-ttu-id="b2ddd-187">按一下 [hello] 按鈕 toogenerate 存取權杖和存取語彙基元秘項。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-187">Click hello button toogenerate an access token and access token secret.</span></span>

<span data-ttu-id="b2ddd-188">請保留這項資訊很方便，因為 hello 下一個程序中需要它。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-188">Keep this information handy, because you will need it in hello next procedure.</span></span>

>[!NOTE]
><span data-ttu-id="b2ddd-189">hello 金鑰和秘密 hello Twitter 應用程式提供存取 tooyour Twitter 帳戶。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-189">hello keys and secrets for hello Twitter application provide access tooyour Twitter account.</span></span> <span data-ttu-id="b2ddd-190">這項資訊視為機密，就像是您的 Twitter 密碼 hello 相同。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-190">Treat this information as sensitive, hello same as you do your Twitter password.</span></span> <span data-ttu-id="b2ddd-191">例如，不要內嵌應用程式中的，您必須提供 tooothers 此資訊。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-191">For example, don't embed this information in an application that you give tooothers.</span></span> 


### <a name="configure-hello-client-application"></a><span data-ttu-id="b2ddd-192">Hello 用戶端應用程式設定</span><span class="sxs-lookup"><span data-stu-id="b2ddd-192">Configure hello client application</span></span>
<span data-ttu-id="b2ddd-193">我們建立了連接 tooTwitter 資料使用的用戶端應用程式[Twitter 的資料流 Api](https://dev.twitter.com/streaming/overview) toocollect 推文中事件的相關一組特定的主題。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-193">We've created a client application that connects tooTwitter data using [Twitter's Streaming APIs](https://dev.twitter.com/streaming/overview) toocollect tweet events about a specific set of topics.</span></span> <span data-ttu-id="b2ddd-194">hello 應用程式會使用 hello [Sentiment140](http://help.sentiment140.com/)開放原始碼工具，指派下列人氣值 tooeach 推文中的 hello:</span><span class="sxs-lookup"><span data-stu-id="b2ddd-194">hello application uses hello [Sentiment140](http://help.sentiment140.com/) open source tool, which assigns hello following sentiment value tooeach tweet:</span></span>

* <span data-ttu-id="b2ddd-195">0 = 負值</span><span class="sxs-lookup"><span data-stu-id="b2ddd-195">0 = negative</span></span>
* <span data-ttu-id="b2ddd-196">2 = 中性</span><span class="sxs-lookup"><span data-stu-id="b2ddd-196">2 = neutral</span></span>
* <span data-ttu-id="b2ddd-197">4 = 正值</span><span class="sxs-lookup"><span data-stu-id="b2ddd-197">4 = positive</span></span>

<span data-ttu-id="b2ddd-198">Hello 推文事件已指派給人氣值之後，它們會推送至您稍早建立的 toohello 事件中心。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-198">After hello tweet events have been assigned a sentiment value, they are pushed toohello event hub that you created earlier.</span></span>

<span data-ttu-id="b2ddd-199">Hello 應用程式執行之前，它會需要某些您的資訊，例如 hello Twitter 索引鍵和 hello 事件中樞連接字串。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-199">Before hello application runs, it requires certain information from you, like hello Twitter keys and hello event hub connection string.</span></span> <span data-ttu-id="b2ddd-200">您可以提供下列方式 hello 組態資訊：</span><span class="sxs-lookup"><span data-stu-id="b2ddd-200">You can provide hello configuration information in these ways:</span></span>

* <span data-ttu-id="b2ddd-201">執行 hello 應用程式，，，然後使用 hello 應用程式的 UI tooenter hello 金鑰、 密碼和連接字串。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-201">Run hello application, and then use hello application's UI tooenter hello keys, secrets, and connection string.</span></span> <span data-ttu-id="b2ddd-202">如果您這樣做，hello 組態資訊用於目前的工作階段，但它不會儲存。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-202">If you do this, hello configuration information is used for your current session, but it isn't saved.</span></span>
* <span data-ttu-id="b2ddd-203">編輯 hello 應用程式的.config 檔案和設定 hello 值。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-203">Edit hello application's .config file and set hello values there.</span></span> <span data-ttu-id="b2ddd-204">這種方式保存 hello 組態資訊，但這也表示，此潛在的敏感資訊會儲存在您的電腦上以純文字。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-204">This approach persists hello configuration information, but it also means that this potentially sensitive information is stored in plain text on your computer.</span></span>

<span data-ttu-id="b2ddd-205">hello 下列程序說明這兩種方法。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-205">hello following procedure documents both approaches.</span></span> 

1. <span data-ttu-id="b2ddd-206">請確定您已下載並解壓縮 hello [TwitterWPFClient.zip](https://github.com/Azure/azure-stream-analytics/blob/master/Samples/TwitterClient/TwitterWPFClient.zip)應用程式，如下所示 hello 必要條件。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-206">Make sure you've downloaded and unzipped hello [TwitterWPFClient.zip](https://github.com/Azure/azure-stream-analytics/blob/master/Samples/TwitterClient/TwitterWPFClient.zip) application, as listed in hello prerequisites.</span></span>

2. <span data-ttu-id="b2ddd-207">tooset hello 值在執行階段 （並僅針對 hello 目前工作階段），執行 hello`TwitterWPFClient.exe`應用程式。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-207">tooset hello values at run time (and only for hello current session), run hello `TwitterWPFClient.exe` application.</span></span> <span data-ttu-id="b2ddd-208">當 hello 應用程式會提示您時，請輸入下列值的 hello:</span><span class="sxs-lookup"><span data-stu-id="b2ddd-208">When hello application prompts you, enter hello following values:</span></span>

    * <span data-ttu-id="b2ddd-209">hello Twitter 取用者金鑰 （應用程式開發介面）。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-209">hello Twitter Consumer Key (API Key).</span></span>
    * <span data-ttu-id="b2ddd-210">hello Twitter 使用者密碼 （應用程式開發介面機密）。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-210">hello Twitter Consumer Secret (API Secret).</span></span>
    * <span data-ttu-id="b2ddd-211">hello Twitter 存取語彙基元。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-211">hello Twitter Access Token.</span></span>
    * <span data-ttu-id="b2ddd-212">hello Twitter 存取語彙基元秘項。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-212">hello Twitter Access Token Secret.</span></span>
    * <span data-ttu-id="b2ddd-213">您稍早儲存 hello 連接字串資訊。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-213">hello connection string information that you saved earlier.</span></span> <span data-ttu-id="b2ddd-214">請確定您使用 hello 連接字串移除 hello`EntityPath`從索引鍵-值組。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-214">Make sure that you use hello connection string that you removed hello `EntityPath` key-value pair from.</span></span>
    * <span data-ttu-id="b2ddd-215">您想要針對 toodetermine 人氣的 hello Twitter 關鍵字。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-215">hello Twitter keywords that you want toodetermine sentiment for.</span></span>

   ![執行中的 TwitterWpfClient 應用程式，顯示隱藏的設定](./media/stream-analytics-twitter-sentiment-analysis-trends/wpfclientlines.png)

3. <span data-ttu-id="b2ddd-217">tooset hello 值持續，使用文字編輯器 tooopen hello TwitterWpfClient.exe.config 檔案。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-217">tooset hello values persistently, use a text editor tooopen hello TwitterWpfClient.exe.config file.</span></span> <span data-ttu-id="b2ddd-218">接著在 hello`<appSettings>`項目，執行這項操作：</span><span class="sxs-lookup"><span data-stu-id="b2ddd-218">Then in hello `<appSettings>` element, do this:</span></span>

    * <span data-ttu-id="b2ddd-219">設定`oauth_consumer_key`toohello Twitter 取用者金鑰 （應用程式開發介面）。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-219">Set `oauth_consumer_key` toohello Twitter Consumer Key (API Key).</span></span> 
    * <span data-ttu-id="b2ddd-220">設定`oauth_consumer_secret`toohello Twitter 使用者密碼 （應用程式開發介面機密）。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-220">Set `oauth_consumer_secret` toohello Twitter Consumer Secret (API Secret).</span></span>
    * <span data-ttu-id="b2ddd-221">設定`oauth_token`toohello Twitter 存取語彙基元。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-221">Set `oauth_token` toohello Twitter Access Token.</span></span>
    * <span data-ttu-id="b2ddd-222">設定`oauth_token_secret`toohello Twitter 存取語彙基元秘項。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-222">Set `oauth_token_secret` toohello Twitter Access Token Secret.</span></span>

    <span data-ttu-id="b2ddd-223">稍後 hello`<appSettings>`項目，進行這些變更：</span><span class="sxs-lookup"><span data-stu-id="b2ddd-223">Later in hello `<appSettings>` element, make these changes:</span></span>

    * <span data-ttu-id="b2ddd-224">設定`EventHubName`toohello 事件中樞名稱 （也就是 toohello 值 hello 實體路徑）。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-224">Set `EventHubName` toohello event hub name (that is, toohello value of hello entity path).</span></span>
    * <span data-ttu-id="b2ddd-225">設定`EventHubNameConnectionString`toohello 連接字串。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-225">Set `EventHubNameConnectionString` toohello connection string.</span></span> <span data-ttu-id="b2ddd-226">請確定您使用 hello 連接字串移除 hello`EntityPath`從索引鍵-值組。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-226">Make sure that you use hello connection string that you removed hello `EntityPath` key-value pair from.</span></span>

    <span data-ttu-id="b2ddd-227">hello`<appSettings>`區段看起來像下列範例中的 hello。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-227">hello `<appSettings>` section looks like hello following example.</span></span> <span data-ttu-id="b2ddd-228">(為了清楚起見和基於安全考量，我們已遮蔽幾行並移除某些字元。)</span><span class="sxs-lookup"><span data-stu-id="b2ddd-228">(For clarity and security, we wrapped some lines and removed some characters.)</span></span>

    ![在文字編輯器中，顯示 hello Twitter 金鑰及密碼，以及 hello 事件中樞連接字串資訊 TwitterWpfClient 應用程式組態檔](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-tiwtter-app-config.png)
 
4. <span data-ttu-id="b2ddd-230">如果您已經沒有啟動 hello 應用程式，現在就執行 TwitterWpfClient.exe。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-230">If you didn't already start hello application, run TwitterWpfClient.exe now.</span></span> 

5. <span data-ttu-id="b2ddd-231">按一下 hello 綠色開始按鈕 toocollect 社交人氣。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-231">Click hello green start button toocollect social sentiment.</span></span> <span data-ttu-id="b2ddd-232">您會看到推文事件以 hello **CreatedAt**，**主題**，和**SentimentScore**傳送 tooyour 事件中心的值。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-232">You see Tweet events with hello **CreatedAt**, **Topic**, and **SentimentScore** values being sent tooyour event hub.</span></span>

    ![執行中的 TwitterWpfClient 應用程式，顯示推文清單](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-twitter-app-listing.png)

    >[!NOTE]
    ><span data-ttu-id="b2ddd-234">如果您看到錯誤，而且您沒有看到推文顯示 hello hello 視窗下半部中的資料流，請仔細檢查 hello 金鑰和密碼。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-234">If you see errors, and you don't see a stream of tweets displayed in hello lower part of hello window, double-check hello keys and secrets.</span></span> <span data-ttu-id="b2ddd-235">也請檢查 hello 連接字串 (請確定它不包含 hello`EntityPath`索引鍵和值。)</span><span class="sxs-lookup"><span data-stu-id="b2ddd-235">Also check hello connection string (make sure that it does not include hello `EntityPath` key and value.)</span></span>


## <a name="create-a-stream-analytics-job"></a><span data-ttu-id="b2ddd-236">建立串流分析工作</span><span class="sxs-lookup"><span data-stu-id="b2ddd-236">Create a Stream Analytics job</span></span>

<span data-ttu-id="b2ddd-237">既然推文中的事件會從 Twitter 即時資料流處理，您可以設定串流分析工作 tooanalyze 這些事件即時。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-237">Now that tweet events are streaming in real time from Twitter, you can set up a Stream Analytics job tooanalyze these events in real time.</span></span>

1. <span data-ttu-id="b2ddd-238">在 hello Azure 入口網站，按一下 **新增** > **物聯網** > **資料流分析工作**。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-238">In hello Azure portal, click **New** > **Internet of Things** > **Stream Analytics job**.</span></span>

2. <span data-ttu-id="b2ddd-239">名稱 hello 工作`socialtwitter-sa-job`和指定的訂用帳戶、 資源群組和位置。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-239">Name hello job `socialtwitter-sa-job` and specify a subscription, resource group, and location.</span></span>

    <span data-ttu-id="b2ddd-240">它是個不錯的主意 tooplace hello 作業和 hello 事件中樞 hello，以免付出 tootransfer 資料區域之間的最佳效能，所以相同的區域。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-240">It's a good idea tooplace hello job and hello event hub in hello same region for best performance and so that you don't pay tootransfer data between regions.</span></span>

    ![建立新的串流分析作業](./media/stream-analytics-twitter-sentiment-analysis-trends/newjob.png)

3. <span data-ttu-id="b2ddd-242">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-242">Click **Create**.</span></span>

    <span data-ttu-id="b2ddd-243">建立 hello 工作，而 hello 入口網站會顯示工作詳細資料。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-243">hello job is created and hello portal displays job details.</span></span>


## <a name="specify-hello-job-input"></a><span data-ttu-id="b2ddd-244">指定 hello 作業輸入</span><span class="sxs-lookup"><span data-stu-id="b2ddd-244">Specify hello job input</span></span>

1. <span data-ttu-id="b2ddd-245">串流分析工作，在底下**作業拓撲**hello 中間的 hello 作業] 刀鋒視窗中，按一下 [**輸入**。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-245">In your Stream Analytics job, under **Job Topology** in hello middle of hello job blade, click **Inputs**.</span></span> 

2. <span data-ttu-id="b2ddd-246">在 hello**輸入**刀鋒視窗中，按一下 **+&nbsp;新增**然後填入 hello 刀鋒視窗包含下列值：</span><span class="sxs-lookup"><span data-stu-id="b2ddd-246">In hello **Inputs** blade, click **+&nbsp;Add** and then fill out hello blade with these values:</span></span>

    * <span data-ttu-id="b2ddd-247">**輸入的別名**： 使用 hello 名稱`TwitterStream`。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-247">**Input alias**: Use hello name `TwitterStream`.</span></span> <span data-ttu-id="b2ddd-248">如果使用不同的名稱，請記下來，因為稍後需要用到。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-248">If you use a different name, make a note of it because you need it later.</span></span>
    * <span data-ttu-id="b2ddd-249">**來源類型**：選取 [資料流]。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-249">**Source type**: Select **Data stream**.</span></span>
    * <span data-ttu-id="b2ddd-250">**來源**：選取 [事件中樞]。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-250">**Source**: Select **Event hub**.</span></span>
    * <span data-ttu-id="b2ddd-251">**匯入選項**：選取 [使用目前訂用帳戶的事件中樞]。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-251">**Import option**: Select **Use event hub from current subscription**.</span></span> 
    * <span data-ttu-id="b2ddd-252">**服務匯流排命名空間**： 選取 hello 事件中樞命名空間您稍早建立 (`<yourname>-socialtwitter-eh-ns`)。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-252">**Service bus namespace**: Select hello event hub namespace that you created earlier (`<yourname>-socialtwitter-eh-ns`).</span></span>
    * <span data-ttu-id="b2ddd-253">**事件中心**: hello 選取您稍早建立的事件中心 (`socialtwitter-eh`)。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-253">**Event hub**: Select hello event hub that you created earlier (`socialtwitter-eh`).</span></span>
    * <span data-ttu-id="b2ddd-254">**事件中樞原則名稱**： 選取您稍早建立的 hello 存取原則 (`socialtwitter-access`)。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-254">**Event hub policy name**: Select hello access policy that you created earlier (`socialtwitter-access`).</span></span>

    ![建立串流分析作業的新輸入](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-twitter-new-input.png)

3. <span data-ttu-id="b2ddd-256">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-256">Click **Create**.</span></span>


## <a name="specify-hello-job-query"></a><span data-ttu-id="b2ddd-257">指定 hello 工作查詢</span><span class="sxs-lookup"><span data-stu-id="b2ddd-257">Specify hello job query</span></span>

<span data-ttu-id="b2ddd-258">串流分析支援說明轉換的簡單、宣告式查詢模型。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-258">Stream Analytics supports a simple, declarative query model that describes transformations.</span></span> <span data-ttu-id="b2ddd-259">toolearn 進一步了解 hello 語言，請參閱 hello [Azure Stream Analytics 查詢語言參考](https://msdn.microsoft.com/library/azure/dn834998.aspx)。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-259">toolearn more about hello language, see hello [Azure Stream Analytics Query Language Reference](https://msdn.microsoft.com/library/azure/dn834998.aspx).</span></span>  <span data-ttu-id="b2ddd-260">本教學課程可協助您撰寫以及測試數個 Twitter 資料查詢。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-260">This tutorial helps you author and test several queries over Twitter data.</span></span>

<span data-ttu-id="b2ddd-261">您可以使用 toocompare hello 數目在主題之間提到，[輪轉視窗](https://msdn.microsoft.com/library/azure/dn835055.aspx)tooget hello 計數每五秒主題所提及。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-261">toocompare hello number of mentions among topics, you can use a [Tumbling window](https://msdn.microsoft.com/library/azure/dn835055.aspx) tooget hello count of mentions by topic every five seconds.</span></span>

1. <span data-ttu-id="b2ddd-262">關閉 hello**輸入**刀鋒視窗，如果您還沒有這麼做。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-262">Close hello **Inputs** blade if you haven't already.</span></span>

2. <span data-ttu-id="b2ddd-263">在 hello 作業刀鋒視窗中，按一下 hello**查詢**方塊。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-263">In hello job blade, click hello **Query** box.</span></span> <span data-ttu-id="b2ddd-264">Azure 會列出 hello 輸入及輸出，已設定為 hello 工作，並可讓您建立查詢，可讓您轉換 hello 輸入資料流傳送 toohello 輸出。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-264">Azure lists hello inputs and outputs that are configured for hello job, and lets you create a query that lets you transform hello input stream as it is sent toohello output.</span></span>

3. <span data-ttu-id="b2ddd-265">請確定該 hello TwitterWpfClient 應用程式正在執行。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-265">Make sure that hello TwitterWpfClient application is running.</span></span> 

3. <span data-ttu-id="b2ddd-266">在 hello**查詢**刀鋒視窗中，按一下 下一步 toohello 的 hello 點`TwitterStream`輸入，然後選取 **範例從輸入資料**。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-266">In hello **Query** blade, click hello dots next toohello `TwitterStream` input and then select **Sample data from input**.</span></span>

    ![功能表選項 toouse 的範例資料 hello 串流分析工作項目，如 「 範例資料從輸入 」 選取](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-create-sample-data-from-input.png)

    <span data-ttu-id="b2ddd-268">這會開啟可讓您指定以 tooread hello 多久輸入資料流定義多少範例資料 tooget 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-268">This opens a blade that lets you specify how much sample data tooget, defined in terms of how long tooread hello input stream.</span></span>

4. <span data-ttu-id="b2ddd-269">設定**分鐘**too3，然後按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-269">Set **Minutes** too3 and then click **OK**.</span></span> 
    
    ![取樣 hello 輸入資料流，與 「 3 分鐘 」，選取選項。](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-input-create-sample-data.png)

    <span data-ttu-id="b2ddd-271">Azure 範例 3 分鐘 hello 輸入資料流中的資料量與 hello 範例資料已就緒時通知您。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-271">Azure samples 3 minutes' worth of data from hello input stream and notifies you when hello sample data is ready.</span></span> <span data-ttu-id="b2ddd-272">(這需要等一下。)</span><span class="sxs-lookup"><span data-stu-id="b2ddd-272">(This takes a short while.)</span></span> 

    <span data-ttu-id="b2ddd-273">hello 範例資料會暫時存放，可同時有 hello 查詢視窗中開啟。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-273">hello sample data is stored temporarily and is available while you have hello query window open.</span></span> <span data-ttu-id="b2ddd-274">如果您關閉 hello 查詢視窗中，會捨棄 hello 範例資料，並可 toocreate 一組新的範例資料。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-274">If you close hello query window, hello sample data is discarded, and you have toocreate a new set of sample data.</span></span> 

5. <span data-ttu-id="b2ddd-275">變更 hello 編輯器 toohello 後面的程式碼中的 hello 查詢：</span><span class="sxs-lookup"><span data-stu-id="b2ddd-275">Change hello query in hello code editor toohello following:</span></span>

    ```
    SELECT System.Timestamp as Time, Topic, COUNT(*)
    FROM TwitterStream TIMESTAMP BY CreatedAt
    GROUP BY TUMBLINGWINDOW(s, 5), Topic
    ```

    <span data-ttu-id="b2ddd-276">如果沒有使用`TwitterStream`hello hello 輸入的別名，以取代您別名`TwitterStream`hello 查詢中。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-276">If didn't use `TwitterStream` as hello alias for hello input, substitute your alias for `TwitterStream` in hello query.</span></span>  

    <span data-ttu-id="b2ddd-277">此查詢會使用 hello **TIMESTAMP BY**關鍵字 toospecify hello 裝載 toobe hello 時態計算中使用的時間戳記欄位。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-277">This query uses hello **TIMESTAMP BY** keyword toospecify a timestamp field in hello payload toobe used in hello temporal computation.</span></span> <span data-ttu-id="b2ddd-278">如果未指定此欄位，hello 視窗化作業會使用每個事件抵達 hello 事件中心的 hello 時間執行。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-278">If this field isn't specified, hello windowing operation is performed by using hello time that each event arrived at hello event hub.</span></span> <span data-ttu-id="b2ddd-279">進一步了解 hello < 抵達時間與比較應用程式時間 > 一節中[串流分析查詢參考](https://msdn.microsoft.com/library/azure/dn834998.aspx)。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-279">Learn more in hello "Arrival Time vs Application Time" section of [Stream Analytics Query Reference](https://msdn.microsoft.com/library/azure/dn834998.aspx).</span></span>

    <span data-ttu-id="b2ddd-280">此查詢同時存取每個視窗的 hello 結束的時間戳記使用 hello **System.Timestamp**屬性。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-280">This query also accesses a timestamp for hello end of each window by using hello **System.Timestamp** property.</span></span>

5. <span data-ttu-id="b2ddd-281">按一下 [ **測試**]。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-281">Click **Test**.</span></span> <span data-ttu-id="b2ddd-282">hello 查詢會執行您所取樣的 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-282">hello query runs against hello data that you sampled.</span></span>
    
6. <span data-ttu-id="b2ddd-283">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-283">Click **Save**.</span></span> <span data-ttu-id="b2ddd-284">這可以節省 hello 查詢 hello 串流分析工作的一部分。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-284">This saves hello query as part of hello Streaming Analytics job.</span></span> <span data-ttu-id="b2ddd-285">（它不會儲存 hello 範例資料）。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-285">(It doesn't save hello sample data.)</span></span>


## <a name="experiment-using-different-fields-from-hello-stream"></a><span data-ttu-id="b2ddd-286">嘗試使用不同的欄位從 hello 資料流</span><span class="sxs-lookup"><span data-stu-id="b2ddd-286">Experiment using different fields from hello stream</span></span> 

<span data-ttu-id="b2ddd-287">hello 下表列出屬於 hello JSON 資料流資料的 hello 欄位。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-287">hello following table lists hello fields that are part of hello JSON streaming data.</span></span> <span data-ttu-id="b2ddd-288">您可用 tooexperiment hello 查詢編輯器中。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-288">Feel free tooexperiment in hello query editor.</span></span>

|<span data-ttu-id="b2ddd-289">JSON 屬性</span><span class="sxs-lookup"><span data-stu-id="b2ddd-289">JSON property</span></span> | <span data-ttu-id="b2ddd-290">定義</span><span class="sxs-lookup"><span data-stu-id="b2ddd-290">Definition</span></span>|
|--- | ---|
|<span data-ttu-id="b2ddd-291">CreatedAt</span><span class="sxs-lookup"><span data-stu-id="b2ddd-291">CreatedAt</span></span> | <span data-ttu-id="b2ddd-292">hello 時間建立該 hello 推文</span><span class="sxs-lookup"><span data-stu-id="b2ddd-292">hello time that hello tweet was created</span></span>|
|<span data-ttu-id="b2ddd-293">主題</span><span class="sxs-lookup"><span data-stu-id="b2ddd-293">Topic</span></span> | <span data-ttu-id="b2ddd-294">符合 hello hello 主題指定關鍵字</span><span class="sxs-lookup"><span data-stu-id="b2ddd-294">hello topic that matches hello specified keyword</span></span>|
|<span data-ttu-id="b2ddd-295">SentimentScore</span><span class="sxs-lookup"><span data-stu-id="b2ddd-295">SentimentScore</span></span> | <span data-ttu-id="b2ddd-296">從 Sentiment140 hello 人氣分數</span><span class="sxs-lookup"><span data-stu-id="b2ddd-296">hello sentiment score from Sentiment140</span></span>|
|<span data-ttu-id="b2ddd-297">作者</span><span class="sxs-lookup"><span data-stu-id="b2ddd-297">Author</span></span> | <span data-ttu-id="b2ddd-298">傳送嗨推文中的 hello Twitter 控點</span><span class="sxs-lookup"><span data-stu-id="b2ddd-298">hello Twitter handle that sent hello tweet</span></span>|
|<span data-ttu-id="b2ddd-299">文字</span><span class="sxs-lookup"><span data-stu-id="b2ddd-299">Text</span></span> | <span data-ttu-id="b2ddd-300">hello 推文中的 hello 完整主體</span><span class="sxs-lookup"><span data-stu-id="b2ddd-300">hello full body of hello tweet</span></span>|


## <a name="create-an-output-sink"></a><span data-ttu-id="b2ddd-301">建立輸出接收器</span><span class="sxs-lookup"><span data-stu-id="b2ddd-301">Create an output sink</span></span>

<span data-ttu-id="b2ddd-302">現在您已經定義的事件資料流、 事件中樞輸入的 tooingest 事件，以及查詢 tooperform 轉換 hello 資料流上。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-302">You have now defined an event stream, an event hub input tooingest events, and a query tooperform a transformation over hello stream.</span></span> <span data-ttu-id="b2ddd-303">hello 最後一個步驟是 toodefine hello 工作的輸出接收。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-303">hello last step is toodefine an output sink for hello job.</span></span>  

<span data-ttu-id="b2ddd-304">在本教學課程中，寫入彙總的 hello 推文事件從 hello 工作查詢 tooAzure Blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-304">In this tutorial, you write hello aggregated tweet events from hello job query tooAzure Blob storage.</span></span>  <span data-ttu-id="b2ddd-305">您也可以推送您的結果 tooAzure SQL Database、 Azure 資料表儲存體，事件中心或 Power BI 中，根據您的應用程式的需求。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-305">You can also push your results tooAzure SQL Database, Azure Table storage, Event Hubs, or Power BI, depending on your application needs.</span></span>

## <a name="specify-hello-job-output"></a><span data-ttu-id="b2ddd-306">指定 hello 作業輸出</span><span class="sxs-lookup"><span data-stu-id="b2ddd-306">Specify hello job output</span></span>

1. <span data-ttu-id="b2ddd-307">在 hello**作業拓撲**區段中，按一下 hello**輸出**方塊。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-307">In hello **Job Topology** section, click hello **Output** box.</span></span> 

2. <span data-ttu-id="b2ddd-308">在 hello**輸出**刀鋒視窗中，按一下 **+&nbsp;新增**然後填入 hello 刀鋒視窗包含下列值：</span><span class="sxs-lookup"><span data-stu-id="b2ddd-308">In hello **Outputs** blade, click **+&nbsp;Add** and then fill out hello blade with these values:</span></span>

    * <span data-ttu-id="b2ddd-309">**輸出別名**： 使用 hello 名稱`TwitterStream-Output`。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-309">**Output alias**: Use hello name `TwitterStream-Output`.</span></span> 
    * <span data-ttu-id="b2ddd-310">**接收器**：選取 [Blob 儲存體]。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-310">**Sink**: Select **Blob storage**.</span></span>
    * <span data-ttu-id="b2ddd-311">**匯入選項**：選取 [使用來自目前訂用帳戶的 Blob 儲存體]。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-311">**Import options**: Select **Use blob storage from current subscription**.</span></span>
    * <span data-ttu-id="b2ddd-312">**儲存體帳戶**。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-312">**Storage account**.</span></span> <span data-ttu-id="b2ddd-313">選取 [建立新儲存體帳戶]。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-313">Select **Create a new storage account.**</span></span>
    * <span data-ttu-id="b2ddd-314">**儲存體帳戶** (第二個方塊)。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-314">**Storage account** (second box).</span></span> <span data-ttu-id="b2ddd-315">輸入 `YOURNAMEsa`，其中 `YOURNAME` 是您的名稱或另一個唯一字串。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-315">Enter `YOURNAMEsa`, where `YOURNAME` is your name or another unique string.</span></span> <span data-ttu-id="b2ddd-316">hello 名稱可以使用小寫字母和數字，而且它必須是唯一整個 Azure。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-316">hello name can use only lowercase letters and numbers, and it must be unique across Azure.</span></span> 
    * <span data-ttu-id="b2ddd-317">**容器**。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-317">**Container**.</span></span> <span data-ttu-id="b2ddd-318">輸入 `socialtwitter`。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-318">Enter `socialtwitter`.</span></span>
    <span data-ttu-id="b2ddd-319">hello 儲存體帳戶名稱及容器名稱是使用同時 tooprovide hello blob 儲存體，像這樣的 URI:</span><span class="sxs-lookup"><span data-stu-id="b2ddd-319">hello storage account name and container name are used together tooprovide a URI for hello blob storage, like this:</span></span> 

    `http://YOURNAMEsa.blob.core.windows.net/socialtwitter/...`
    
    ![串流分析作業的 [新輸出] 刀鋒視窗](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-create-output-blob-storage.png)
    
4. <span data-ttu-id="b2ddd-321">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-321">Click **Create**.</span></span> 

    <span data-ttu-id="b2ddd-322">Azure 會建立 hello 儲存體帳戶，並會自動產生索引鍵。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-322">Azure creates hello storage account and generates a key automatically.</span></span> 

5. <span data-ttu-id="b2ddd-323">關閉 hello**輸出**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-323">Close hello **Outputs** blade.</span></span> 


## <a name="start-hello-job"></a><span data-ttu-id="b2ddd-324">啟動 hello 工作</span><span class="sxs-lookup"><span data-stu-id="b2ddd-324">Start hello job</span></span>

<span data-ttu-id="b2ddd-325">已指定作業輸入、查詢和輸出。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-325">A job input, query, and output are specified.</span></span> <span data-ttu-id="b2ddd-326">您已準備好 toostart hello 資料流分析工作。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-326">You are ready toostart hello Stream Analytics job.</span></span>

1. <span data-ttu-id="b2ddd-327">請確定該 hello TwitterWpfClient 應用程式正在執行。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-327">Make sure that hello TwitterWpfClient application is running.</span></span> 

2. <span data-ttu-id="b2ddd-328">在 hello 作業刀鋒視窗中，按一下 **啟動**。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-328">In hello job blade, click **Start**.</span></span>

    ![啟動 hello 資料流分析工作](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-sa-job-start-output.png)

3. <span data-ttu-id="b2ddd-330">在 hello**開始工作**刀鋒視窗中，針對**作業輸出的開始時間**，選取**現在**，然後按一下**啟動**。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-330">In hello **Start job** blade, for **Job output start time**, select **Now** and then click **Start**.</span></span> 

    ![「 啟動工作 」 刀鋒視窗中的 hello 資料流分析工作](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-sa-job-start-job-blade.png)

    <span data-ttu-id="b2ddd-332">Azure 通知您，當 hello 作業已啟動，而且 hello 作業刀鋒視窗中，在 hello 狀態會顯示為**執行**。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-332">Azure notifies you when hello job has started, and in hello job blade, hello status is displayed as **Running**.</span></span>

    ![工作正在執行](./media/stream-analytics-twitter-sentiment-analysis-trends/jobrunning.png)

## <a name="view-output-for-sentiment-analysis"></a><span data-ttu-id="b2ddd-334">檢視情感分析輸出</span><span class="sxs-lookup"><span data-stu-id="b2ddd-334">View output for sentiment analysis</span></span>

<span data-ttu-id="b2ddd-335">您的工作已開始執行，且正在處理 hello 即時 Twitter 資料流之後，您可以檢視 hello 情緒分析輸出。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-335">After your job has started running and is processing hello real-time Twitter stream, you can view hello output for sentiment analysis.</span></span>

<span data-ttu-id="b2ddd-336">您可以使用這類工具[Azure 儲存體總管](https://http://storageexplorer.com/)或[Azure 總管](http://www.cerebrata.com/products/azure-explorer/introduction)tooview 即時輸出您的工作。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-336">You can use a tool like [Azure Storage Explorer](https://http://storageexplorer.com/) or [Azure Explorer](http://www.cerebrata.com/products/azure-explorer/introduction) tooview your job output in real time.</span></span> <span data-ttu-id="b2ddd-337">從這裡，您可以使用[Power BI](https://powerbi.com/) tooextend 您自訂的儀表板的應用程式 tooinclude 喜歡 hello hello 下列螢幕擷取畫面所示：</span><span class="sxs-lookup"><span data-stu-id="b2ddd-337">From here, you can use [Power BI](https://powerbi.com/) tooextend your application tooinclude a customized dashboard like hello one shown in hello following screenshot:</span></span>

![Power BI](./media/stream-analytics-twitter-sentiment-analysis-trends/power-bi.png)


## <a name="create-another-query-tooidentify-trending-topics"></a><span data-ttu-id="b2ddd-339">建立另一個查詢 tooidentify 趨勢主題</span><span class="sxs-lookup"><span data-stu-id="b2ddd-339">Create another query tooidentify trending topics</span></span>

<span data-ttu-id="b2ddd-340">您可以使用 toounderstand Twitter 情緒的另一個查詢根據[滑動視窗](https://msdn.microsoft.com/library/azure/dn835051.aspx)。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-340">Another query you can use toounderstand Twitter sentiment is based on a [Sliding Window](https://msdn.microsoft.com/library/azure/dn835051.aspx).</span></span> <span data-ttu-id="b2ddd-341">tooidentify 趨勢的主題，您尋找跨提及中指定的時間量的臨界值的主題。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-341">tooidentify trending topics, you look for topics that cross a threshold value for mentions in a specified amount of time.</span></span>

<span data-ttu-id="b2ddd-342">基於 hello 本教學課程，您檢查主題所述 20 倍以上 hello 最後 5 秒。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-342">For hello purposes of this tutorial, you check for topics that are mentioned more than 20 times in hello last 5 seconds.</span></span>

1. <span data-ttu-id="b2ddd-343">在 hello 作業刀鋒視窗中，按一下 **停止**toostop hello 作業。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-343">In hello job blade, click **Stop** toostop hello job.</span></span> 

2. <span data-ttu-id="b2ddd-344">在 hello**作業拓撲**區段中，按一下 hello**查詢**方塊。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-344">In hello **Job Topology** section, click hello **Query** box.</span></span> 

3. <span data-ttu-id="b2ddd-345">變更 hello 查詢 toohello 下列：</span><span class="sxs-lookup"><span data-stu-id="b2ddd-345">Change hello query toohello following:</span></span>

    ```    
    SELECT System.Timestamp as Time, Topic, COUNT(*) as Mentions
    FROM TwitterStream TIMESTAMP BY CreatedAt
    GROUP BY SLIDINGWINDOW(s, 5), topic
    HAVING COUNT(*) > 20
    ```

4. <span data-ttu-id="b2ddd-346">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-346">Click **Save**.</span></span>

5. <span data-ttu-id="b2ddd-347">請確定該 hello TwitterWpfClient 應用程式正在執行。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-347">Make sure that hello TwitterWpfClient application is running.</span></span> 

6. <span data-ttu-id="b2ddd-348">按一下**啟動**toorestart hello 作業使用 hello 新查詢。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-348">Click **Start** toorestart hello job using hello new query.</span></span>


## <a name="get-support"></a><span data-ttu-id="b2ddd-349">取得支援</span><span class="sxs-lookup"><span data-stu-id="b2ddd-349">Get support</span></span>
<span data-ttu-id="b2ddd-350">如需進一步的協助，請參閱我們的 [Azure Stream Analytics 論壇](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)。</span><span class="sxs-lookup"><span data-stu-id="b2ddd-350">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="b2ddd-351">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b2ddd-351">Next steps</span></span>
* [<span data-ttu-id="b2ddd-352">簡介 tooAzure 資料流分析</span><span class="sxs-lookup"><span data-stu-id="b2ddd-352">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="b2ddd-353">開始使用 Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="b2ddd-353">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="b2ddd-354">調整 Azure Stream Analytics 工作</span><span class="sxs-lookup"><span data-stu-id="b2ddd-354">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="b2ddd-355">Azure Stream Analytics 查詢語言參考</span><span class="sxs-lookup"><span data-stu-id="b2ddd-355">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="b2ddd-356">Azure 串流分析管理 REST API 參考</span><span class="sxs-lookup"><span data-stu-id="b2ddd-356">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)
