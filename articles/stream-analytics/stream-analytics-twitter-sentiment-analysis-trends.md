---
title: "使用 Azure 串流分析執行即時 Twitter 情感分析 | Microsoft Docs"
description: "了解如何使用串流分析來執行即時 Twitter 情感分析。 從事件產生到即時儀表板資料的逐步指導。"
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
ms.openlocfilehash: 8de6850964700f5b3f71d144b40af927f2e52d7e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="real-time-twitter-sentiment-analysis-in-azure-stream-analytics"></a><span data-ttu-id="6b4bf-105">Azure 串流分析中的即時 Twitter 情感分析</span><span class="sxs-lookup"><span data-stu-id="6b4bf-105">Real-time Twitter sentiment analysis in Azure Stream Analytics</span></span>

<span data-ttu-id="6b4bf-106">本文將透過把即時的 Twitter 事件帶入 Azure 事件中樞，來讓您了解如何建立社交媒體分析的情感分析解決方案。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-106">Learn how to build a sentiment analysis solution for social media analytics by bringing real-time Twitter events into Azure Event Hubs.</span></span> <span data-ttu-id="6b4bf-107">接著，您可以撰寫 Azure 串流分析查詢來分析資料，並儲存結果以供稍後使用，或使用儀表板和 [Power BI](https://powerbi.com/) 來即時提供深入解析。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-107">You can then write an Azure Stream Analytics query to analyze the data and either store the results for later use or use a dashboard and [Power BI](https://powerbi.com/) to provide insights in real time.</span></span>

<span data-ttu-id="6b4bf-108">社交媒體分析工具可協助組織了解熱門話題。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-108">Social media analytics tools help organizations understand trending topics.</span></span> <span data-ttu-id="6b4bf-109">熱門話題就是在社交媒體中有大量文章的話題及意見。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-109">Trending topics are subjects and attitudes that have a high volume of posts in social media.</span></span> <span data-ttu-id="6b4bf-110">情感分析 (亦稱為*意見挖掘*) 會使用社交媒體分析工具來判斷使用者對產品、概念等等項目的態度。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-110">Sentiment analysis, which is also called *opinion mining*, uses social media analytics tools to determine attitudes toward a product, idea, and so on.</span></span> 

<span data-ttu-id="6b4bf-111">即時 Twitter 趨勢分析是分析工具的絕佳例子，因為主題標籤訂閱模型可讓您接聽摘要的特定關鍵字 (主題標籤)，並開發情感分析。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-111">Real-time Twitter trend analysis is a great example of an analytics tool, because the hashtag subscription model enables you to listen to specific keywords (hashtags) and develop sentiment analysis of the feed.</span></span>

## <a name="scenario-social-media-sentiment-analysis-in-real-time"></a><span data-ttu-id="6b4bf-112">案例：即時的社交媒體情感分析</span><span class="sxs-lookup"><span data-stu-id="6b4bf-112">Scenario: Social media sentiment analysis in real time</span></span>

<span data-ttu-id="6b4bf-113">擁有新聞媒體網站的公司提供與讀者有直接關聯的網站內容，試圖打敗競爭對手。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-113">A company that has a news media website is interested in gaining an advantage over its competitors by featuring site content that is immediately relevant to its readers.</span></span> <span data-ttu-id="6b4bf-114">公司透過對 Twitter 資料執行即時情感分析，來針對與讀者相關的話題使用社交媒體分析。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-114">The company uses social media analysis on topics that are relevant to readers by doing real-time sentiment analysis of Twitter data.</span></span>

<span data-ttu-id="6b4bf-115">為了在 Twitter 上即時找出熱門話題，公司需要即時分析重要話題的推文數量和情感。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-115">To identify trending topics in real time on Twitter, the company needs real-time analytics about the tweet volume and sentiment for key topics.</span></span> <span data-ttu-id="6b4bf-116">換言之，他們需要以該社交媒體摘要為基礎的情感分析分析引擎。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-116">In other words, the need is a sentiment analysis analytics engine that's based on this social media feed.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6b4bf-117">必要條件</span><span class="sxs-lookup"><span data-stu-id="6b4bf-117">Prerequisites</span></span>
<span data-ttu-id="6b4bf-118">在本教學課程中，您將會透過用戶端應用程式來連線到 Twitter，並尋找具有特定主題標籤 (可設定) 的推文。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-118">In this tutorial, you use a client application that connects to Twitter and looks for tweets that have certain hashtags (which you can set).</span></span> <span data-ttu-id="6b4bf-119">若要執行應用程式並使用 Azure 串流分析來分析推文，您必須具備下列項目：</span><span class="sxs-lookup"><span data-stu-id="6b4bf-119">In order to run the application and analyze the tweets using Azure Streaming Analytics, you must have the following:</span></span>

* <span data-ttu-id="6b4bf-120">Azure 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="6b4bf-120">An Azure subscription</span></span>
* <span data-ttu-id="6b4bf-121">Twitter 帳戶</span><span class="sxs-lookup"><span data-stu-id="6b4bf-121">A Twitter account</span></span> 
* <span data-ttu-id="6b4bf-122">Twitter 應用程式和該應用程式的 [OAuth 存取權杖](https://dev.twitter.com/oauth/overview/application-owner-access-tokens)。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-122">A Twitter application, and the [OAuth access token](https://dev.twitter.com/oauth/overview/application-owner-access-tokens) for that application.</span></span> <span data-ttu-id="6b4bf-123">稍後我們會提供如何建立 Twitter 應用程式的高層級指示。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-123">We provide high-level instructions for how to create a Twitter application later.</span></span>
* <span data-ttu-id="6b4bf-124">用來讀取 Twitter 摘要的 TwitterWPFClient 應用程式。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-124">The TwitterWPFClient application, which reads the Twitter feed.</span></span> <span data-ttu-id="6b4bf-125">若要取得此應用程式，請從 GitHub 下載[TwitterWPFClient.zip](https://github.com/Azure/azure-stream-analytics/blob/master/Samples/TwitterClient/TwitterWPFClient.zip) 檔案，然後將套件解壓縮至電腦上的資料夾。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-125">To get this application, download the [TwitterWPFClient.zip](https://github.com/Azure/azure-stream-analytics/blob/master/Samples/TwitterClient/TwitterWPFClient.zip) file from GitHub and then unzip the package into a folder on your computer.</span></span> <span data-ttu-id="6b4bf-126">如果您想要看到原始程式碼，並在偵錯工具中執行應用程式，您可以從 [GitHub](https://aka.ms/azure-stream-analytics-telcogenerator) 取得原始程式碼。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-126">If you want to see the source code and run the application in a debugger, you can get the source code from [GitHub](https://aka.ms/azure-stream-analytics-telcogenerator).</span></span> 

## <a name="create-an-event-hub-for-streaming-analytics-input"></a><span data-ttu-id="6b4bf-127">建立串流分析輸入的事件中樞</span><span class="sxs-lookup"><span data-stu-id="6b4bf-127">Create an event hub for Streaming Analytics input</span></span>

<span data-ttu-id="6b4bf-128">此範例應用程式會產生事件，並將事件發送至 Azure 事件中樞。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-128">The sample application generates events and pushes them to an Azure event hub.</span></span> <span data-ttu-id="6b4bf-129">Azure 事件中樞是串流分析擷取事件的慣用方法。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-129">Azure event hubs are the preferred method of event ingestion for Stream Analytics.</span></span> <span data-ttu-id="6b4bf-130">如需詳細資訊，請參閱 [Azure 事件中樞文件](../event-hubs/event-hubs-what-is-event-hubs.md)。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-130">For more information, see the [Azure Event Hubs documentation](../event-hubs/event-hubs-what-is-event-hubs.md).</span></span>


### <a name="create-an-event-hub-namespace-and-event-hub"></a><span data-ttu-id="6b4bf-131">建立事件中樞命名空間和事件中樞</span><span class="sxs-lookup"><span data-stu-id="6b4bf-131">Create an event hub namespace and event hub</span></span>
<span data-ttu-id="6b4bf-132">在此程序中，您需要先建立事件中樞命名空間，再將事件中樞新增至該命名空間。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-132">In this procedure, you first create an event hub namespace, and then you add an event hub to that namespace.</span></span> <span data-ttu-id="6b4bf-133">事件中樞命名空間可在邏輯上將相關的事件匯流排執行個體分組。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-133">Event hub namespaces are used to logically group related event bus instances.</span></span> 

1. <span data-ttu-id="6b4bf-134">登入 Azure 入口網站，按一下 [新增] > [物聯網] > [事件中樞]。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-134">Log  in to the Azure portal and click **New** > **Internet of Things** > **Event Hub**.</span></span> 

2. <span data-ttu-id="6b4bf-135">在 [建立命名空間] 刀鋒視窗中，輸入命名空間名稱，例如 `<yourname>-socialtwitter-eh-ns`。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-135">In the **Create namespace** blade, enter a namespace name such as `<yourname>-socialtwitter-eh-ns`.</span></span> <span data-ttu-id="6b4bf-136">您可以使用任何名稱作為命名空間，但名稱在 URL 中必須有效，而且在整個 Azure 內必須唯一的。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-136">You can use any name for the namespace, but the name must be valid for a URL and it must be unique across Azure.</span></span> 
    
3. <span data-ttu-id="6b4bf-137">選取訂用帳戶並建立或選擇資源群組，然後按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-137">Select a subscription and create or choose a resource group, then click **Create**.</span></span> 

    ![建立事件中樞命名空間](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-create-eventhub-namespace.png)
 
4. <span data-ttu-id="6b4bf-139">當命名空間完成部署時，請在 Azure 資源清單中尋找事件中樞命名空間。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-139">When the namespace has finished deploying, find the event hub namespace in your list of Azure resources.</span></span> 

5. <span data-ttu-id="6b4bf-140">按一下新的命名空間，然後在命名空間刀鋒視窗中，按一下 [+&nbsp;事件中樞]。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-140">Click the new namespace, and in the namespace blade, click **+&nbsp;Event Hub**.</span></span> 

    ![<span data-ttu-id="6b4bf-141">建立新事件中樞的 [新增事件中樞] 按鈕</span><span class="sxs-lookup"><span data-stu-id="6b4bf-141">The Add Event Hub button for creating a new event hub</span></span> ](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-create-eventhub-button.png)    
 
6. <span data-ttu-id="6b4bf-142">將新的事件中樞命名為 `socialtwitter-eh`。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-142">Name the new event hub `socialtwitter-eh`.</span></span> <span data-ttu-id="6b4bf-143">您可以使用不同的名稱。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-143">You can use a different name.</span></span> <span data-ttu-id="6b4bf-144">如果這樣做，請記下來，因為稍後需要用到此名稱。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-144">If you do, make a note of it, because you need the name later.</span></span> <span data-ttu-id="6b4bf-145">您不需要為事件中樞設定其他任何選項。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-145">You don't need to set any other options for the event hub.</span></span>

    ![建立新事件中樞的刀鋒視窗](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-create-eventhub.png)
 
7. <span data-ttu-id="6b4bf-147">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-147">Click **Create**.</span></span>


### <a name="grant-access-to-the-event-hub"></a><span data-ttu-id="6b4bf-148">授權存取事件中樞</span><span class="sxs-lookup"><span data-stu-id="6b4bf-148">Grant access to the event hub</span></span>

<span data-ttu-id="6b4bf-149">事件中樞必須有原則來允許適當的存取權，流程才能將資料傳送到事件中樞。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-149">Before a process can send data to an event hub, the event hub must have a policy that allows appropriate access.</span></span> <span data-ttu-id="6b4bf-150">存取原則會產生包含授權資訊的連接字串。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-150">The access policy produces a connection string that includes authorization information.</span></span>

1.  <span data-ttu-id="6b4bf-151">在事件命名空間刀鋒視窗中，按一下 [事件中樞]，然後按一下新事件中樞的名稱。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-151">In the event namespace blade, click **Event Hubs** and then click the name of your new event hub.</span></span>

2.  <span data-ttu-id="6b4bf-152">在事件中樞刀鋒視窗中，按一下 [共用存取原則]，然後按一下 [+&nbsp;新增]。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-152">In the event hub blade, click **Shared access policies** and then click **+&nbsp;Add**.</span></span>

    >[!NOTE]
    ><span data-ttu-id="6b4bf-153">請確定您正在使用事件中樞，而不是事件中樞命名空間。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-153">Make sure you're working with the event hub, not the event hub namespace.</span></span>

3.  <span data-ttu-id="6b4bf-154">新增名為 `socialtwitter-access` 的原則，然後在 [宣告] 中，選取 [管理]。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-154">Add a policy named `socialtwitter-access` and for **Claim**, select **Manage**.</span></span>

    ![建立新事件中樞存取原則的刀鋒視窗](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-create-shared-access-policy-manage.png)
 
4.  <span data-ttu-id="6b4bf-156">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-156">Click **Create**.</span></span>

5.  <span data-ttu-id="6b4bf-157">部署原則之後，在共用存取原則清單中按一下此原則。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-157">After the policy has been deployed, click it in the list of shared access policies.</span></span>

6.  <span data-ttu-id="6b4bf-158">找出標示為 [連接字串-主要索引鍵] 的方塊，按一下連接字串旁邊的複製按鈕。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-158">Find the box labeled **CONNECTION STRING-PRIMARY KEY** and click the copy button next to the connection string.</span></span> 
    
    ![從存取原則複製主要的連接字串索引鍵](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-shared-access-policy-copy-connection-string.png)
 
7.  <span data-ttu-id="6b4bf-160">將連接字串貼到文字編輯器。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-160">Paste the connection string into a text editor.</span></span> <span data-ttu-id="6b4bf-161">稍微編輯一下此連接字串，下一節需要用到它。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-161">You need this connection string for the next section, after you make some small edits to it.</span></span>

    <span data-ttu-id="6b4bf-162">連接字串如下所示：</span><span class="sxs-lookup"><span data-stu-id="6b4bf-162">The connection string looks like this:</span></span>

        Endpoint=sb://YOURNAME-socialtwitter-eh-ns.servicebus.windows.net/;SharedAccessKeyName=socialtwitter-access;SharedAccessKey=Gw2NFZw6r...FxKbXaC2op6a0ZsPkI=;EntityPath=socialtwitter-eh

    <span data-ttu-id="6b4bf-163">請注意，連接字串包含多個機碼值組，以分號分隔：`Endpoint`、`SharedAccessKeyName`、`SharedAccessKey` 和 `EntityPath`。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-163">Notice that the connection string contains multiple key-value pairs, separated with semicolons: `Endpoint`, `SharedAccessKeyName`, `SharedAccessKey`, and `EntityPath`.</span></span>  

    > [!NOTE]
    > <span data-ttu-id="6b4bf-164">基於安全考量，我們已移除範例中連接字串的某些部分。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-164">For security, parts of the connection string in the example have been removed.</span></span>

8.  <span data-ttu-id="6b4bf-165">在文字編輯器中，移除連接字串的 `EntityPath` 組 (別忘了移除前面的分號)。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-165">In the text editor, remove the `EntityPath` pair from the connection string (don't forget to remove the semicolon that precedes it).</span></span> <span data-ttu-id="6b4bf-166">完成時，連接字串會如下所示：</span><span class="sxs-lookup"><span data-stu-id="6b4bf-166">When you're done, the connection string looks like this:</span></span>

        Endpoint=sb://YOURNAME-socialtwitter-eh-ns.servicebus.windows.net/;SharedAccessKeyName=socialtwitter-access;SharedAccessKey=Gw2NFZw6r...FxKbXaC2op6a0ZsPkI=


## <a name="configure-and-start-the-twitter-client-application"></a><span data-ttu-id="6b4bf-167">設定並啟動 Twitter 用戶端應用程式</span><span class="sxs-lookup"><span data-stu-id="6b4bf-167">Configure and start the Twitter client application</span></span>
<span data-ttu-id="6b4bf-168">用戶端應用程式會直接從 Twitter 取得推文事件。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-168">The client application gets tweet events directly from Twitter.</span></span> <span data-ttu-id="6b4bf-169">為了這樣做，它需要權限來呼叫 Twitter 串流 API。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-169">In order to do so, it needs permission to call the Twitter Streaming APIs.</span></span> <span data-ttu-id="6b4bf-170">若要設定該權限，您需要在 Twitter 中建立應用程式，以產生唯一認證 (例如 OAuth 權杖)。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-170">To configure that permission, you create an application in Twitter, which generates unique credentials (such as an OAuth token).</span></span> <span data-ttu-id="6b4bf-171">然後，您可以設定用戶端應用程式在呼叫 API 時使用這些認證。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-171">You can then configure the client application to use these credentials when it makes API calls.</span></span> 

### <a name="create-a-twitter-application"></a><span data-ttu-id="6b4bf-172">建立 Twitter 應用程式</span><span class="sxs-lookup"><span data-stu-id="6b4bf-172">Create a Twitter application</span></span>
<span data-ttu-id="6b4bf-173">如果您還沒有可用於本教學課程的 Twitter 應用程式，您可以建立一個。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-173">If you do not already have a Twitter application that you can use for this tutorial, you can create one.</span></span> <span data-ttu-id="6b4bf-174">您必須已經有 Twitter 帳戶。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-174">You must already have a Twitter account.</span></span>

> [!NOTE]
> <span data-ttu-id="6b4bf-175">在 Twitter 中建立應用程式及取得金鑰、秘密和權杖的確切流程可能不同。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-175">The exact process in Twitter for creating an application and getting the keys, secrets, and token might change.</span></span> <span data-ttu-id="6b4bf-176">如果這些指示不符合您在 Twitter 網站上看到的內容，請參閱 Twitter 開發人員文件。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-176">If these instructions don't match what you see on the Twitter site, refer to the Twitter developer documentation.</span></span>

1. <span data-ttu-id="6b4bf-177">移至 [Twitter 應用程式管理網頁](https://apps.twitter.com/)。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-177">Go to the [Twitter application management page](https://apps.twitter.com/).</span></span> 

2. <span data-ttu-id="6b4bf-178">建立新的應用程式。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-178">Create a new application.</span></span> 

    * <span data-ttu-id="6b4bf-179">在網站 URL 中，指定有效的 URL。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-179">For the website URL, specify a valid URL.</span></span> <span data-ttu-id="6b4bf-180">不必是即時網站。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-180">It does not have to be a live site.</span></span> <span data-ttu-id="6b4bf-181">(您不能只指定 `localhost`。)</span><span class="sxs-lookup"><span data-stu-id="6b4bf-181">(You can't specify just `localhost`.)</span></span>
    * <span data-ttu-id="6b4bf-182">將回呼欄位保留空白。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-182">Leave the callback field blank.</span></span> <span data-ttu-id="6b4bf-183">您用於本教學課程的用戶端應用程式不需要回呼。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-183">The client application you use for this tutorial doesn't require callbacks.</span></span>

    ![在 Twitter 中建立應用程式](./media/stream-analytics-twitter-sentiment-analysis-trends/create-twitter-application.png)

3. <span data-ttu-id="6b4bf-185">(選擇性) 將應用程式的權限變更為唯讀。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-185">Optionally, change the application's permissions to read-only.</span></span>

4. <span data-ttu-id="6b4bf-186">建立應用程式後，移至 [金鑰和存取權杖]  網頁。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-186">When the application is created, go to the **Keys and Access Tokens** page.</span></span>

5. <span data-ttu-id="6b4bf-187">按一下按鈕可以產生存取權杖和存取權杖祕密。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-187">Click the button to generate an access token and access token secret.</span></span>

<span data-ttu-id="6b4bf-188">請備妥此資訊，在下一個程序中需要用到。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-188">Keep this information handy, because you will need it in the next procedure.</span></span>

>[!NOTE]
><span data-ttu-id="6b4bf-189">Twitter 應用程式的金鑰和秘密可用來存取您的 Twitter 帳戶。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-189">The keys and secrets for the Twitter application provide access to your Twitter account.</span></span> <span data-ttu-id="6b4bf-190">這項資訊要視為機密，就像看待您的 Twitter 密碼一樣。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-190">Treat this information as sensitive, the same as you do your Twitter password.</span></span> <span data-ttu-id="6b4bf-191">例如，請勿將這項資訊內嵌在您提供給其他人的應用程式中。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-191">For example, don't embed this information in an application that you give to others.</span></span> 


### <a name="configure-the-client-application"></a><span data-ttu-id="6b4bf-192">設定用戶端應用程式</span><span class="sxs-lookup"><span data-stu-id="6b4bf-192">Configure the client application</span></span>
<span data-ttu-id="6b4bf-193">我們已建立用戶端應用程式，可利用 [Twitter 的串流 API](https://dev.twitter.com/streaming/overview) 來連線至 Twitter 資料，以收集一組特定話題相關的推文事件。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-193">We've created a client application that connects to Twitter data using [Twitter's Streaming APIs](https://dev.twitter.com/streaming/overview) to collect tweet events about a specific set of topics.</span></span> <span data-ttu-id="6b4bf-194">該應用程式使用 [Sentiment140](http://help.sentiment140.com/) 開放原始碼工具，將下列情感值指派給每個推文：</span><span class="sxs-lookup"><span data-stu-id="6b4bf-194">The application uses the [Sentiment140](http://help.sentiment140.com/) open source tool, which assigns the following sentiment value to each tweet:</span></span>

* <span data-ttu-id="6b4bf-195">0 = 負值</span><span class="sxs-lookup"><span data-stu-id="6b4bf-195">0 = negative</span></span>
* <span data-ttu-id="6b4bf-196">2 = 中性</span><span class="sxs-lookup"><span data-stu-id="6b4bf-196">2 = neutral</span></span>
* <span data-ttu-id="6b4bf-197">4 = 正值</span><span class="sxs-lookup"><span data-stu-id="6b4bf-197">4 = positive</span></span>

<span data-ttu-id="6b4bf-198">在指派情感值給推文事件之後，推文事件就會發送至您稍早建立的事件中樞。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-198">After the tweet events have been assigned a sentiment value, they are pushed to the event hub that you created earlier.</span></span>

<span data-ttu-id="6b4bf-199">在應用程式執行之前，您需要提供一些資訊，例如 Twitter 金鑰和事件中樞連接字串。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-199">Before the application runs, it requires certain information from you, like the Twitter keys and the event hub connection string.</span></span> <span data-ttu-id="6b4bf-200">您可以依照這些方法來提供組態資訊：</span><span class="sxs-lookup"><span data-stu-id="6b4bf-200">You can provide the configuration information in these ways:</span></span>

* <span data-ttu-id="6b4bf-201">執行應用程式，然後使用應用程式的 UI 來輸入金鑰、祕密和連接字串。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-201">Run the application, and then use the application's UI to enter the keys, secrets, and connection string.</span></span> <span data-ttu-id="6b4bf-202">如果您這麼做，組態資訊會用於目前的工作階段，但不會儲存。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-202">If you do this, the configuration information is used for your current session, but it isn't saved.</span></span>
* <span data-ttu-id="6b4bf-203">編輯應用程式的 .config 檔案，在其中設定一些值。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-203">Edit the application's .config file and set the values there.</span></span> <span data-ttu-id="6b4bf-204">這種方法會保存組態資訊，但也表示這項潛在的敏感資訊會以純文字儲存在電腦上。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-204">This approach persists the configuration information, but it also means that this potentially sensitive information is stored in plain text on your computer.</span></span>

<span data-ttu-id="6b4bf-205">下列程序說明這兩種方法。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-205">The following procedure documents both approaches.</span></span> 

1. <span data-ttu-id="6b4bf-206">請確定您已下載並解壓縮 [TwitterWPFClient.zip](https://github.com/Azure/azure-stream-analytics/blob/master/Samples/TwitterClient/TwitterWPFClient.zip) 應用程式，如必要條件中所示。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-206">Make sure you've downloaded and unzipped the [TwitterWPFClient.zip](https://github.com/Azure/azure-stream-analytics/blob/master/Samples/TwitterClient/TwitterWPFClient.zip) application, as listed in the prerequisites.</span></span>

2. <span data-ttu-id="6b4bf-207">若要在執行階段設定值 (且僅針對目前工作階段)，請執行 `TwitterWPFClient.exe` 應用程式。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-207">To set the values at run time (and only for the current session), run the `TwitterWPFClient.exe` application.</span></span> <span data-ttu-id="6b4bf-208">當應用程式提示您時，請輸入下列值：</span><span class="sxs-lookup"><span data-stu-id="6b4bf-208">When the application prompts you, enter the following values:</span></span>

    * <span data-ttu-id="6b4bf-209">Twitter 取用者金鑰 (API 金鑰)。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-209">The Twitter Consumer Key (API Key).</span></span>
    * <span data-ttu-id="6b4bf-210">Twitter 取用者祕密 (API 祕密)。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-210">The Twitter Consumer Secret (API Secret).</span></span>
    * <span data-ttu-id="6b4bf-211">Twitter 存取權杖。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-211">The Twitter Access Token.</span></span>
    * <span data-ttu-id="6b4bf-212">Twitter 存取權杖祕密。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-212">The Twitter Access Token Secret.</span></span>
    * <span data-ttu-id="6b4bf-213">您稍早儲存的連接字串資訊。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-213">The connection string information that you saved earlier.</span></span> <span data-ttu-id="6b4bf-214">請確定您使用已移除 `EntityPath` 機碼值組的的連接字串。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-214">Make sure that you use the connection string that you removed the `EntityPath` key-value pair from.</span></span>
    * <span data-ttu-id="6b4bf-215">您用以判斷情感的 Twitter 關鍵字。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-215">The Twitter keywords that you want to determine sentiment for.</span></span>

   ![執行中的 TwitterWpfClient 應用程式，顯示隱藏的設定](./media/stream-analytics-twitter-sentiment-analysis-trends/wpfclientlines.png)

3. <span data-ttu-id="6b4bf-217">若要持續設定值，請使用文字編輯器開啟 TwitterWpfClient.exe.config 檔案。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-217">To set the values persistently, use a text editor to open the TwitterWpfClient.exe.config file.</span></span> <span data-ttu-id="6b4bf-218">然後在 `<appSettings>` 元素中，執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="6b4bf-218">Then in the `<appSettings>` element, do this:</span></span>

    * <span data-ttu-id="6b4bf-219">將 `oauth_consumer_key` 設為 Twitter 取用者金鑰 (API 金鑰)。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-219">Set `oauth_consumer_key` to the Twitter Consumer Key (API Key).</span></span> 
    * <span data-ttu-id="6b4bf-220">將 `oauth_consumer_secret` 設為 Twitter 取用者祕密 (API 祕密)。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-220">Set `oauth_consumer_secret` to the Twitter Consumer Secret (API Secret).</span></span>
    * <span data-ttu-id="6b4bf-221">將 `oauth_token` 設為 Twitter 存取權杖。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-221">Set `oauth_token` to the Twitter Access Token.</span></span>
    * <span data-ttu-id="6b4bf-222">將 `oauth_token_secret` 設為 Twitter 存取權杖祕密。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-222">Set `oauth_token_secret` to the Twitter Access Token Secret.</span></span>

    <span data-ttu-id="6b4bf-223">稍後在 `<appSettings>` 元素中，進行下列變更：</span><span class="sxs-lookup"><span data-stu-id="6b4bf-223">Later in the `<appSettings>` element, make these changes:</span></span>

    * <span data-ttu-id="6b4bf-224">將 `EventHubName` 設為事件中樞名稱 (也就是實體路徑的值)。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-224">Set `EventHubName` to the event hub name (that is, to the value of the entity path).</span></span>
    * <span data-ttu-id="6b4bf-225">將 `EventHubNameConnectionString` 設為連接字串。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-225">Set `EventHubNameConnectionString` to the connection string.</span></span> <span data-ttu-id="6b4bf-226">請確定您使用已移除 `EntityPath` 機碼值組的的連接字串。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-226">Make sure that you use the connection string that you removed the `EntityPath` key-value pair from.</span></span>

    <span data-ttu-id="6b4bf-227">`<appSettings>` 區段如下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-227">The `<appSettings>` section looks like the following example.</span></span> <span data-ttu-id="6b4bf-228">(為了清楚起見和基於安全考量，我們已遮蔽幾行並移除某些字元。)</span><span class="sxs-lookup"><span data-stu-id="6b4bf-228">(For clarity and security, we wrapped some lines and removed some characters.)</span></span>

    ![文字編輯器中的 TwitterWpfClient 應用程式組態檔，顯示 Twitter 金鑰和祕密，以及事件中樞連接字串資訊](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-tiwtter-app-config.png)
 
4. <span data-ttu-id="6b4bf-230">如果您尚未啟動此應用程式，現在就執行 TwitterWpfClient.exe。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-230">If you didn't already start the application, run TwitterWpfClient.exe now.</span></span> 

5. <span data-ttu-id="6b4bf-231">按一下綠色啟動按鈕來收集社交情感。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-231">Click the green start button to collect social sentiment.</span></span> <span data-ttu-id="6b4bf-232">您會看到推文事件連同 **CreatedAt**、**Topic** 和 **SentimentScore** 值，一起傳送到事件中樞。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-232">You see Tweet events with the **CreatedAt**, **Topic**, and **SentimentScore** values being sent to your event hub.</span></span>

    ![執行中的 TwitterWpfClient 應用程式，顯示推文清單](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-twitter-app-listing.png)

    >[!NOTE]
    ><span data-ttu-id="6b4bf-234">如果您看到錯誤，而且在視窗下半部沒有看到推文的資料流，請仔細檢查金鑰和祕密。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-234">If you see errors, and you don't see a stream of tweets displayed in the lower part of the window, double-check the keys and secrets.</span></span> <span data-ttu-id="6b4bf-235">也請檢查連接字串 (請確定不包含 `EntityPath` 索引鍵和值。)</span><span class="sxs-lookup"><span data-stu-id="6b4bf-235">Also check the connection string (make sure that it does not include the `EntityPath` key and value.)</span></span>


## <a name="create-a-stream-analytics-job"></a><span data-ttu-id="6b4bf-236">建立串流分析工作</span><span class="sxs-lookup"><span data-stu-id="6b4bf-236">Create a Stream Analytics job</span></span>

<span data-ttu-id="6b4bf-237">既然正在從 Twitter 即時串流推文事件，您可以設定串流分析作業來即時分析這些事件。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-237">Now that tweet events are streaming in real time from Twitter, you can set up a Stream Analytics job to analyze these events in real time.</span></span>

1. <span data-ttu-id="6b4bf-238">在 Azure 入口網站中，按一下 [新增] > [物聯網] > [串流分析作業]。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-238">In the Azure portal, click **New** > **Internet of Things** > **Stream Analytics job**.</span></span>

2. <span data-ttu-id="6b4bf-239">將作業命名為 `socialtwitter-sa-job`，並指定訂用帳戶、資源群組和位置。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-239">Name the job `socialtwitter-sa-job` and specify a subscription, resource group, and location.</span></span>

    <span data-ttu-id="6b4bf-240">最好將作業和事件中樞放在相同的區域，以達到最佳效能，在區域之間傳送資料也不需要付費。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-240">It's a good idea to place the job and the event hub in the same region for best performance and so that you don't pay to transfer data between regions.</span></span>

    ![建立新的串流分析作業](./media/stream-analytics-twitter-sentiment-analysis-trends/newjob.png)

3. <span data-ttu-id="6b4bf-242">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-242">Click **Create**.</span></span>

    <span data-ttu-id="6b4bf-243">即可建立作業，入口網站會顯示作業詳細資料。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-243">The job is created and the portal displays job details.</span></span>


## <a name="specify-the-job-input"></a><span data-ttu-id="6b4bf-244">指定工作輸入</span><span class="sxs-lookup"><span data-stu-id="6b4bf-244">Specify the job input</span></span>

1. <span data-ttu-id="6b4bf-245">在串流分析作業中，於作業刀鋒視窗中央的 [作業拓撲] 下，按一下 [輸入]。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-245">In your Stream Analytics job, under **Job Topology** in the middle of the job blade, click **Inputs**.</span></span> 

2. <span data-ttu-id="6b4bf-246">在 [輸入] 刀鋒視窗中，按一下 [+&nbsp;新增]，然後在刀鋒視窗中填入這些值：</span><span class="sxs-lookup"><span data-stu-id="6b4bf-246">In the **Inputs** blade, click **+&nbsp;Add** and then fill out the blade with these values:</span></span>

    * <span data-ttu-id="6b4bf-247">**輸入別名**：使用名稱 `TwitterStream`。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-247">**Input alias**: Use the name `TwitterStream`.</span></span> <span data-ttu-id="6b4bf-248">如果使用不同的名稱，請記下來，因為稍後需要用到。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-248">If you use a different name, make a note of it because you need it later.</span></span>
    * <span data-ttu-id="6b4bf-249">**來源類型**：選取 [資料流]。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-249">**Source type**: Select **Data stream**.</span></span>
    * <span data-ttu-id="6b4bf-250">**來源**：選取 [事件中樞]。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-250">**Source**: Select **Event hub**.</span></span>
    * <span data-ttu-id="6b4bf-251">**匯入選項**：選取 [使用目前訂用帳戶的事件中樞]。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-251">**Import option**: Select **Use event hub from current subscription**.</span></span> 
    * <span data-ttu-id="6b4bf-252">**服務匯流排命名空間**：選取您稍早建立的事件中樞命名空間 (`<yourname>-socialtwitter-eh-ns`)。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-252">**Service bus namespace**: Select the event hub namespace that you created earlier (`<yourname>-socialtwitter-eh-ns`).</span></span>
    * <span data-ttu-id="6b4bf-253">**事件中樞**：選取您稍早建立的事件中樞 (`socialtwitter-eh`)。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-253">**Event hub**: Select the event hub that you created earlier (`socialtwitter-eh`).</span></span>
    * <span data-ttu-id="6b4bf-254">**事件中樞原則名稱**：選取您稍早建立的存取原則 (`socialtwitter-access`)。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-254">**Event hub policy name**: Select the access policy that you created earlier (`socialtwitter-access`).</span></span>

    ![建立串流分析作業的新輸入](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-twitter-new-input.png)

3. <span data-ttu-id="6b4bf-256">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-256">Click **Create**.</span></span>


## <a name="specify-the-job-query"></a><span data-ttu-id="6b4bf-257">指定作業查詢</span><span class="sxs-lookup"><span data-stu-id="6b4bf-257">Specify the job query</span></span>

<span data-ttu-id="6b4bf-258">串流分析支援說明轉換的簡單、宣告式查詢模型。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-258">Stream Analytics supports a simple, declarative query model that describes transformations.</span></span> <span data-ttu-id="6b4bf-259">若要深入了解語言，請參閱 [Azure Stream Analytics 查詢語言參考](https://msdn.microsoft.com/library/azure/dn834998.aspx)。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-259">To learn more about the language, see the [Azure Stream Analytics Query Language Reference](https://msdn.microsoft.com/library/azure/dn834998.aspx).</span></span>  <span data-ttu-id="6b4bf-260">本教學課程可協助您撰寫以及測試數個 Twitter 資料查詢。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-260">This tutorial helps you author and test several queries over Twitter data.</span></span>

<span data-ttu-id="6b4bf-261">為了比較提及不同話題的次數，您可以使用[輪轉視窗](https://msdn.microsoft.com/library/azure/dn835055.aspx)，依話題每隔五秒取得一次提及次數。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-261">To compare the number of mentions among topics, you can use a [Tumbling window](https://msdn.microsoft.com/library/azure/dn835055.aspx) to get the count of mentions by topic every five seconds.</span></span>

1. <span data-ttu-id="6b4bf-262">關閉 [輸入] 刀鋒視窗 (如果尚未關閉)。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-262">Close the **Inputs** blade if you haven't already.</span></span>

2. <span data-ttu-id="6b4bf-263">在作業刀鋒視窗中，按一下 [查詢] 方塊。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-263">In the job blade, click the **Query** box.</span></span> <span data-ttu-id="6b4bf-264">Azure 會列出作業已設定的輸入和輸出，還可讓您建立查詢，在輸入資料流傳送至輸出時進行轉換。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-264">Azure lists the inputs and outputs that are configured for the job, and lets you create a query that lets you transform the input stream as it is sent to the output.</span></span>

3. <span data-ttu-id="6b4bf-265">請確定 TwitterWpfClient 應用程式正在執行。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-265">Make sure that the TwitterWpfClient application is running.</span></span> 

3. <span data-ttu-id="6b4bf-266">在 [查詢] 刀鋒視窗中，按一下 `TwitterStream` 輸入旁邊的點，然後選取 [來自輸入的範例資料]。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-266">In the **Query** blade, click the dots next to the `TwitterStream` input and then select **Sample data from input**.</span></span>

    ![用於在串流分析作業中輸入範例資料的功能表選項，已選取 [來自輸入的範例資料]](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-create-sample-data-from-input.png)

    <span data-ttu-id="6b4bf-268">這會開啟刀鋒視窗，讓您決定要花多少時間來讀取輸入資料流，以指定取得多少範例資料。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-268">This opens a blade that lets you specify how much sample data to get, defined in terms of how long to read the input stream.</span></span>

4. <span data-ttu-id="6b4bf-269">將 [分鐘] 設定為 3，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-269">Set **Minutes** to 3 and then click **OK**.</span></span> 
    
    ![輸入資料流的取樣選項，已選取 [3 分鐘]。](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-input-create-sample-data.png)

    <span data-ttu-id="6b4bf-271">Azure 會從輸入資料流取樣 3 分鐘的資料，備妥範例資料時會通知您。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-271">Azure samples 3 minutes' worth of data from the input stream and notifies you when the sample data is ready.</span></span> <span data-ttu-id="6b4bf-272">(這需要等一下。)</span><span class="sxs-lookup"><span data-stu-id="6b4bf-272">(This takes a short while.)</span></span> 

    <span data-ttu-id="6b4bf-273">範例資料會暫時儲存，開啟查詢視窗時即可使用。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-273">The sample data is stored temporarily and is available while you have the query window open.</span></span> <span data-ttu-id="6b4bf-274">如果您關閉查詢視窗，則會捨棄範例資料，您將必須建立一組新的範例資料。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-274">If you close the query window, the sample data is discarded, and you have to create a new set of sample data.</span></span> 

5. <span data-ttu-id="6b4bf-275">在程式碼編輯器中，將查詢變更如下：</span><span class="sxs-lookup"><span data-stu-id="6b4bf-275">Change the query in the code editor to the following:</span></span>

    ```
    SELECT System.Timestamp as Time, Topic, COUNT(*)
    FROM TwitterStream TIMESTAMP BY CreatedAt
    GROUP BY TUMBLINGWINDOW(s, 5), Topic
    ```

    <span data-ttu-id="6b4bf-276">如果您不是使用 `TwitterStream` 作為輸入的別名，請在查詢中以您的別名取代 `TwitterStream`。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-276">If didn't use `TwitterStream` as the alias for the input, substitute your alias for `TwitterStream` in the query.</span></span>  

    <span data-ttu-id="6b4bf-277">此查詢會使用 **TIMESTAMP BY** 關鍵字，在裝載中指定一個暫時運算時會用到的時間戳記欄位。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-277">This query uses the **TIMESTAMP BY** keyword to specify a timestamp field in the payload to be used in the temporal computation.</span></span> <span data-ttu-id="6b4bf-278">如果未指定這個欄位，則會使用每個事件到達事件中樞的時間，執行時間範圍設定作業。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-278">If this field isn't specified, the windowing operation is performed by using the time that each event arrived at the event hub.</span></span> <span data-ttu-id="6b4bf-279">若要深入了解，請參閱[串流分析查詢參考 (英文)](https://msdn.microsoft.com/library/azure/dn834998.aspx) 中的＜到達時間與應用程式時間之比較 (英文)＞一節。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-279">Learn more in the "Arrival Time vs Application Time" section of [Stream Analytics Query Reference](https://msdn.microsoft.com/library/azure/dn834998.aspx).</span></span>

    <span data-ttu-id="6b4bf-280">此查詢也可以使用 **System.Timestamp** 屬性存取每個視窗結束時的時間戳記。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-280">This query also accesses a timestamp for the end of each window by using the **System.Timestamp** property.</span></span>

5. <span data-ttu-id="6b4bf-281">按一下 [ **測試**]。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-281">Click **Test**.</span></span> <span data-ttu-id="6b4bf-282">這時會針對您已取樣的資料執行查詢。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-282">The query runs against the data that you sampled.</span></span>
    
6. <span data-ttu-id="6b4bf-283">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-283">Click **Save**.</span></span> <span data-ttu-id="6b4bf-284">這會將查詢儲存在串流分析作業中。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-284">This saves the query as part of the Streaming Analytics job.</span></span> <span data-ttu-id="6b4bf-285">(不會儲存範例資料。)</span><span class="sxs-lookup"><span data-stu-id="6b4bf-285">(It doesn't save the sample data.)</span></span>


## <a name="experiment-using-different-fields-from-the-stream"></a><span data-ttu-id="6b4bf-286">使用資料流中的不同欄位進行實驗</span><span class="sxs-lookup"><span data-stu-id="6b4bf-286">Experiment using different fields from the stream</span></span> 

<span data-ttu-id="6b4bf-287">下表列出屬於 JSON 串流資料的欄位。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-287">The following table lists the fields that are part of the JSON streaming data.</span></span> <span data-ttu-id="6b4bf-288">您可在查詢編輯器中自由進行試驗。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-288">Feel free to experiment in the query editor.</span></span>

|<span data-ttu-id="6b4bf-289">JSON 屬性</span><span class="sxs-lookup"><span data-stu-id="6b4bf-289">JSON property</span></span> | <span data-ttu-id="6b4bf-290">定義</span><span class="sxs-lookup"><span data-stu-id="6b4bf-290">Definition</span></span>|
|--- | ---|
|<span data-ttu-id="6b4bf-291">CreatedAt</span><span class="sxs-lookup"><span data-stu-id="6b4bf-291">CreatedAt</span></span> | <span data-ttu-id="6b4bf-292">建立推文的時間</span><span class="sxs-lookup"><span data-stu-id="6b4bf-292">The time that the tweet was created</span></span>|
|<span data-ttu-id="6b4bf-293">話題</span><span class="sxs-lookup"><span data-stu-id="6b4bf-293">Topic</span></span> | <span data-ttu-id="6b4bf-294">符合所指定關鍵字的話題</span><span class="sxs-lookup"><span data-stu-id="6b4bf-294">The topic that matches the specified keyword</span></span>|
|<span data-ttu-id="6b4bf-295">SentimentScore</span><span class="sxs-lookup"><span data-stu-id="6b4bf-295">SentimentScore</span></span> | <span data-ttu-id="6b4bf-296">來自 Sentiment140 的情感分數</span><span class="sxs-lookup"><span data-stu-id="6b4bf-296">The sentiment score from Sentiment140</span></span>|
|<span data-ttu-id="6b4bf-297">作者</span><span class="sxs-lookup"><span data-stu-id="6b4bf-297">Author</span></span> | <span data-ttu-id="6b4bf-298">傳送推文的 Twitter 控制代碼</span><span class="sxs-lookup"><span data-stu-id="6b4bf-298">The Twitter handle that sent the tweet</span></span>|
|<span data-ttu-id="6b4bf-299">文字</span><span class="sxs-lookup"><span data-stu-id="6b4bf-299">Text</span></span> | <span data-ttu-id="6b4bf-300">推文的全文</span><span class="sxs-lookup"><span data-stu-id="6b4bf-300">The full body of the tweet</span></span>|


## <a name="create-an-output-sink"></a><span data-ttu-id="6b4bf-301">建立輸出接收器</span><span class="sxs-lookup"><span data-stu-id="6b4bf-301">Create an output sink</span></span>

<span data-ttu-id="6b4bf-302">您現在已定義事件資料流、用來內嵌事件的事件中樞，以及用來轉換資料流的查詢。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-302">You have now defined an event stream, an event hub input to ingest events, and a query to perform a transformation over the stream.</span></span> <span data-ttu-id="6b4bf-303">最後一個步驟是定義作業的輸出接收。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-303">The last step is to define an output sink for the job.</span></span>  

<span data-ttu-id="6b4bf-304">在本教學課程中，您會將作業查詢所彙總的推文事件寫入 Azure Blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-304">In this tutorial, you write the aggregated tweet events from the job query to Azure Blob storage.</span></span>  <span data-ttu-id="6b4bf-305">根據您的應用程式需求，您也可以將結果發送至 Azure SQL Database、Azure 資料表儲存體、事件中樞或 Power BI。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-305">You can also push your results to Azure SQL Database, Azure Table storage, Event Hubs, or Power BI, depending on your application needs.</span></span>

## <a name="specify-the-job-output"></a><span data-ttu-id="6b4bf-306">指定作業輸出</span><span class="sxs-lookup"><span data-stu-id="6b4bf-306">Specify the job output</span></span>

1. <span data-ttu-id="6b4bf-307">在 [作業拓撲] 區段中，按一下 [輸出] 方塊。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-307">In the **Job Topology** section, click the **Output** box.</span></span> 

2. <span data-ttu-id="6b4bf-308">在 [輸出] 刀鋒視窗中，按一下 [+&nbsp;新增]，然後在刀鋒視窗中填入這些值：</span><span class="sxs-lookup"><span data-stu-id="6b4bf-308">In the **Outputs** blade, click **+&nbsp;Add** and then fill out the blade with these values:</span></span>

    * <span data-ttu-id="6b4bf-309">**輸出別名**：使用名稱 `TwitterStream-Output`。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-309">**Output alias**: Use the name `TwitterStream-Output`.</span></span> 
    * <span data-ttu-id="6b4bf-310">**接收器**：選取 [Blob 儲存體]。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-310">**Sink**: Select **Blob storage**.</span></span>
    * <span data-ttu-id="6b4bf-311">**匯入選項**：選取 [使用來自目前訂用帳戶的 Blob 儲存體]。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-311">**Import options**: Select **Use blob storage from current subscription**.</span></span>
    * <span data-ttu-id="6b4bf-312">**儲存體帳戶**。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-312">**Storage account**.</span></span> <span data-ttu-id="6b4bf-313">選取 [建立新儲存體帳戶]。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-313">Select **Create a new storage account.**</span></span>
    * <span data-ttu-id="6b4bf-314">**儲存體帳戶** (第二個方塊)。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-314">**Storage account** (second box).</span></span> <span data-ttu-id="6b4bf-315">輸入 `YOURNAMEsa`，其中 `YOURNAME` 是您的名稱或另一個唯一字串。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-315">Enter `YOURNAMEsa`, where `YOURNAME` is your name or another unique string.</span></span> <span data-ttu-id="6b4bf-316">名稱只能使用小寫字母和數字，而且在整個 Azure 中必須是唯一的。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-316">The name can use only lowercase letters and numbers, and it must be unique across Azure.</span></span> 
    * <span data-ttu-id="6b4bf-317">**容器**。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-317">**Container**.</span></span> <span data-ttu-id="6b4bf-318">輸入 `socialtwitter`。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-318">Enter `socialtwitter`.</span></span>
    <span data-ttu-id="6b4bf-319">儲存體帳戶名稱和容器名稱一起用來提供 blob 儲存體的 URI，例如：</span><span class="sxs-lookup"><span data-stu-id="6b4bf-319">The storage account name and container name are used together to provide a URI for the blob storage, like this:</span></span> 

    `http://YOURNAMEsa.blob.core.windows.net/socialtwitter/...`
    
    ![串流分析作業的 [新輸出] 刀鋒視窗](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-create-output-blob-storage.png)
    
4. <span data-ttu-id="6b4bf-321">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-321">Click **Create**.</span></span> 

    <span data-ttu-id="6b4bf-322">Azure 會建立儲存體帳戶，並自動產生金鑰。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-322">Azure creates the storage account and generates a key automatically.</span></span> 

5. <span data-ttu-id="6b4bf-323">關閉 [輸出] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-323">Close the **Outputs** blade.</span></span> 


## <a name="start-the-job"></a><span data-ttu-id="6b4bf-324">啟動工作</span><span class="sxs-lookup"><span data-stu-id="6b4bf-324">Start the job</span></span>

<span data-ttu-id="6b4bf-325">已指定作業輸入、查詢和輸出。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-325">A job input, query, and output are specified.</span></span> <span data-ttu-id="6b4bf-326">您已準備好啟動串流分析作業。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-326">You are ready to start the Stream Analytics job.</span></span>

1. <span data-ttu-id="6b4bf-327">請確定 TwitterWpfClient 應用程式正在執行。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-327">Make sure that the TwitterWpfClient application is running.</span></span> 

2. <span data-ttu-id="6b4bf-328">在作業刀鋒視窗中，按一下 [啟動]。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-328">In the job blade, click **Start**.</span></span>

    ![啟動串流分析工作](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-sa-job-start-output.png)

3. <span data-ttu-id="6b4bf-330">在 [啟動作業] 刀鋒視窗的 [作業輸出開始時間] 中，選取 [現在]，然後按一下 [啟動]。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-330">In the **Start job** blade, for **Job output start time**, select **Now** and then click **Start**.</span></span> 

    ![串流分析作業的 [啟動作業] 刀鋒視窗](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-sa-job-start-job-blade.png)

    <span data-ttu-id="6b4bf-332">作業啟動後，Azure 會通知您，在作業刀鋒視窗中，狀態會顯示為 [執行中]。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-332">Azure notifies you when the job has started, and in the job blade, the status is displayed as **Running**.</span></span>

    ![工作正在執行](./media/stream-analytics-twitter-sentiment-analysis-trends/jobrunning.png)

## <a name="view-output-for-sentiment-analysis"></a><span data-ttu-id="6b4bf-334">檢視情感分析輸出</span><span class="sxs-lookup"><span data-stu-id="6b4bf-334">View output for sentiment analysis</span></span>

<span data-ttu-id="6b4bf-335">在您的作業已開始執行並處理即時 Twitter 串流之後，您就可以檢視情感分析的輸出。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-335">After your job has started running and is processing the real-time Twitter stream, you can view the output for sentiment analysis.</span></span>

<span data-ttu-id="6b4bf-336">您可以使用 [Azure 儲存體總管](https://http://storageexplorer.com/)或 [Azure 總管](http://www.cerebrata.com/products/azure-explorer/introduction)之類的工具，即時檢視您的作業輸出。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-336">You can use a tool like [Azure Storage Explorer](https://http://storageexplorer.com/) or [Azure Explorer](http://www.cerebrata.com/products/azure-explorer/introduction) to view your job output in real time.</span></span> <span data-ttu-id="6b4bf-337">從這裡，您可以使用 [Power BI](https://powerbi.com/) 擴充您的應用程式來包含自訂儀表板，如下列螢幕擷取畫面所示：</span><span class="sxs-lookup"><span data-stu-id="6b4bf-337">From here, you can use [Power BI](https://powerbi.com/) to extend your application to include a customized dashboard like the one shown in the following screenshot:</span></span>

![Power BI](./media/stream-analytics-twitter-sentiment-analysis-trends/power-bi.png)


## <a name="create-another-query-to-identify-trending-topics"></a><span data-ttu-id="6b4bf-339">建立另一個查詢來識別熱門話題</span><span class="sxs-lookup"><span data-stu-id="6b4bf-339">Create another query to identify trending topics</span></span>

<span data-ttu-id="6b4bf-340">另一個可用來了解 Twitter 情緒的查詢是根據[滑動視窗](https://msdn.microsoft.com/library/azure/dn835051.aspx)。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-340">Another query you can use to understand Twitter sentiment is based on a [Sliding Window](https://msdn.microsoft.com/library/azure/dn835051.aspx).</span></span> <span data-ttu-id="6b4bf-341">若要識別熱門話題，您需要找出在指定的時間內提及次數超過臨界值的話題。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-341">To identify trending topics, you look for topics that cross a threshold value for mentions in a specified amount of time.</span></span>

<span data-ttu-id="6b4bf-342">基於本教學課程的目的，您將會找出過去 5 秒內提及次數超過 20 次的話題。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-342">For the purposes of this tutorial, you check for topics that are mentioned more than 20 times in the last 5 seconds.</span></span>

1. <span data-ttu-id="6b4bf-343">在作業刀鋒視窗中，按一下 [停止] 來停止作業。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-343">In the job blade, click **Stop** to stop the job.</span></span> 

2. <span data-ttu-id="6b4bf-344">在 [作業拓撲] 區段中，按一下 [查詢] 方塊。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-344">In the **Job Topology** section, click the **Query** box.</span></span> 

3. <span data-ttu-id="6b4bf-345">將查詢變更如下：</span><span class="sxs-lookup"><span data-stu-id="6b4bf-345">Change the query to the following:</span></span>

    ```    
    SELECT System.Timestamp as Time, Topic, COUNT(*) as Mentions
    FROM TwitterStream TIMESTAMP BY CreatedAt
    GROUP BY SLIDINGWINDOW(s, 5), topic
    HAVING COUNT(*) > 20
    ```

4. <span data-ttu-id="6b4bf-346">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-346">Click **Save**.</span></span>

5. <span data-ttu-id="6b4bf-347">請確定 TwitterWpfClient 應用程式正在執行。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-347">Make sure that the TwitterWpfClient application is running.</span></span> 

6. <span data-ttu-id="6b4bf-348">按一下 [啟動]，使用新的查詢來重新啟動作業。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-348">Click **Start** to restart the job using the new query.</span></span>


## <a name="get-support"></a><span data-ttu-id="6b4bf-349">取得支援</span><span class="sxs-lookup"><span data-stu-id="6b4bf-349">Get support</span></span>
<span data-ttu-id="6b4bf-350">如需進一步的協助，請參閱我們的 [Azure Stream Analytics 論壇](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)。</span><span class="sxs-lookup"><span data-stu-id="6b4bf-350">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="6b4bf-351">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6b4bf-351">Next steps</span></span>
* [<span data-ttu-id="6b4bf-352">Azure Stream Analytics 介紹</span><span class="sxs-lookup"><span data-stu-id="6b4bf-352">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="6b4bf-353">開始使用 Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="6b4bf-353">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="6b4bf-354">調整 Azure Stream Analytics 工作</span><span class="sxs-lookup"><span data-stu-id="6b4bf-354">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="6b4bf-355">Azure Stream Analytics 查詢語言參考</span><span class="sxs-lookup"><span data-stu-id="6b4bf-355">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="6b4bf-356">Azure 串流分析管理 REST API 參考</span><span class="sxs-lookup"><span data-stu-id="6b4bf-356">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)
