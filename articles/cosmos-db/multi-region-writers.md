---
title: "使用 Azure Cosmos DB 的多重主機資料庫架構 | Microsoft Docs"
description: "了解如何設計應用程式架構，使用 Azure Cosmos DB 在多個地理區域進行本機讀取和寫入。"
services: cosmos-db
documentationcenter: 
author: arramac
manager: jhubbard
editor: 
ms.assetid: 706ced74-ea67-45dd-a7de-666c3c893687
ms.service: cosmos-db
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/23/2017
ms.author: arramac
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: cf1482ae7b1070023703f5dbe861d151f5d64fd8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="multi-master-globally-replicated-database-architectures-with-azure-cosmos-db"></a><span data-ttu-id="c73f1-103">使用 Azure Cosmos DB 的多重主機全域複寫資料庫架構</span><span class="sxs-lookup"><span data-stu-id="c73f1-103">Multi-master globally replicated database architectures with Azure Cosmos DB</span></span>
<span data-ttu-id="c73f1-104">Azure Cosmos DB 支援周全的[全域複寫](distribute-data-globally.md)，可讓您以低延遲存取工作負載中的任何位置，將資料散發到多個區域。</span><span class="sxs-lookup"><span data-stu-id="c73f1-104">Azure Cosmos DB supports turnkey [global replication](distribute-data-globally.md), which allows you to distribute data to multiple regions with low latency access anywhere in the workload.</span></span> <span data-ttu-id="c73f1-105">此模型通常用於發行者/取用者工作負載，寫入器在單一地理區域中，而讀取器 (讀取) 分散在世界各地的其他區域。</span><span class="sxs-lookup"><span data-stu-id="c73f1-105">This model is commonly used for publisher/consumer workloads where there is a writer in a single geographic region and globally distributed readers in other (read) regions.</span></span> 

<span data-ttu-id="c73f1-106">您也可以使用 Azure Cosmos DB 的全域複寫支援，建置其寫入器和讀取器遍布全球的應用程式。</span><span class="sxs-lookup"><span data-stu-id="c73f1-106">You can also use Azure Cosmos DB's global replication support to build applications in which writers and readers are globally distributed.</span></span> <span data-ttu-id="c73f1-107">本文概述的模式可讓使用 Azure Cosmos DB 的分散式寫入器達成本機寫入及本機讀取存取。</span><span class="sxs-lookup"><span data-stu-id="c73f1-107">This document outlines a pattern that enables achieving local write and local read access for distributed writers using Azure Cosmos DB.</span></span>

## <span data-ttu-id="c73f1-108"><a id="ExampleScenario"></a>內容發佈 - 範例案例</span><span class="sxs-lookup"><span data-stu-id="c73f1-108"><a id="ExampleScenario"></a>Content Publishing - an example scenario</span></span>
<span data-ttu-id="c73f1-109">讓我們看看真實世界的案例，說明如何利用 Azure Cosmos DB 使用分散在世界各地多重區域/多重主機讀寫模式。</span><span class="sxs-lookup"><span data-stu-id="c73f1-109">Let's look at a real world scenario to describe how you can use globally distributed multi-region/multi-master read write patterns with Azure Cosmos DB.</span></span> <span data-ttu-id="c73f1-110">以建置在 Azure Cosmos DB 上的內容發佈平台為例。</span><span class="sxs-lookup"><span data-stu-id="c73f1-110">Consider a content publishing platform built on Azure Cosmos DB.</span></span> <span data-ttu-id="c73f1-111">這個平台必須符合以下一些需求，才能獲得絕佳發行者和取用者使用者體驗。</span><span class="sxs-lookup"><span data-stu-id="c73f1-111">Here are some requirements that this platform must meet for a great user experience for both publishers and consumers.</span></span>

* <span data-ttu-id="c73f1-112">作者與訂閱者都分散在世界各地</span><span class="sxs-lookup"><span data-stu-id="c73f1-112">Both authors and subscribers are spread over the world</span></span> 
* <span data-ttu-id="c73f1-113">作者必須將 (寫入) 文章發佈到其本機 (最接近) 的區域</span><span class="sxs-lookup"><span data-stu-id="c73f1-113">Authors must publish (write) articles to their local (closest) region</span></span>
* <span data-ttu-id="c73f1-114">作者文章的讀取器/訂閱者遍及全球。</span><span class="sxs-lookup"><span data-stu-id="c73f1-114">Authors have readers/subscribers of their articles who are distributed across the globe.</span></span> 
* <span data-ttu-id="c73f1-115">發佈新文章時，訂閱者應該收到通知。</span><span class="sxs-lookup"><span data-stu-id="c73f1-115">Subscribers should get a notification when new articles are published.</span></span>
* <span data-ttu-id="c73f1-116">訂閱者必須能從其本機區域讀取文章。</span><span class="sxs-lookup"><span data-stu-id="c73f1-116">Subscribers must be able to read articles from their local region.</span></span> <span data-ttu-id="c73f1-117">他們也能將評論加入這些文章。</span><span class="sxs-lookup"><span data-stu-id="c73f1-117">They should also be able to add reviews to these articles.</span></span> 
* <span data-ttu-id="c73f1-118">包括文章作者在內的任何人都可以從本機區域檢視所有文章附加的評論。</span><span class="sxs-lookup"><span data-stu-id="c73f1-118">Anyone including the author of the articles should be able view all the reviews attached to articles from a local region.</span></span> 

<span data-ttu-id="c73f1-119">假設有數百萬取用者與發行者，而文章有數十億篇，我們很快會面臨調整規模以及保證本機存取的問題。</span><span class="sxs-lookup"><span data-stu-id="c73f1-119">Assuming millions of consumers and publishers with billions of articles, soon we have to confront the problems of scale along with guaranteeing locality of access.</span></span> <span data-ttu-id="c73f1-120">和大部分擴充性問題一樣，解決方案就是要有良好的資料分割策略。</span><span class="sxs-lookup"><span data-stu-id="c73f1-120">As with most scalability problems, the solution lies in a good partitioning strategy.</span></span> <span data-ttu-id="c73f1-121">接下來，讓我們看看如何將文章、評論及通知的模型建立為文件、設定 Azure Cosmos DB 帳戶以及實作資料存取層。</span><span class="sxs-lookup"><span data-stu-id="c73f1-121">Next, let's look at how to model articles, review, and notifications as documents, configure Azure Cosmos DB accounts, and implement a data access layer.</span></span> 

<span data-ttu-id="c73f1-122">如果您想要深入了解資料分割和資料分割索引鍵，請參閱 [Azure Cosmos DB 的資料分割與調整規模](partition-data.md)。</span><span class="sxs-lookup"><span data-stu-id="c73f1-122">If you would like to learn more about partitioning and partition keys, see [Partitioning and Scaling in Azure Cosmos DB](partition-data.md).</span></span>

## <span data-ttu-id="c73f1-123"><a id="ModelingNotifications"></a>建立模型通知</span><span class="sxs-lookup"><span data-stu-id="c73f1-123"><a id="ModelingNotifications"></a>Modeling notifications</span></span>
<span data-ttu-id="c73f1-124">通知是使用者特有的資料輸入。</span><span class="sxs-lookup"><span data-stu-id="c73f1-124">Notifications are data feeds specific to a user.</span></span> <span data-ttu-id="c73f1-125">因此，通知文件的存取模式都是以單一使用者而言。</span><span class="sxs-lookup"><span data-stu-id="c73f1-125">Therefore, the access patterns for notifications documents are always in the context of single user.</span></span> <span data-ttu-id="c73f1-126">例如，您可以「發佈給使用者的通知」或「擷取指定使用者的所有通知」。</span><span class="sxs-lookup"><span data-stu-id="c73f1-126">For example, you would "post a notification to a user" or "fetch all notifications for a given user".</span></span> <span data-ttu-id="c73f1-127">因此，這類資料分割索引鍵的最佳選擇會是 `UserId`。</span><span class="sxs-lookup"><span data-stu-id="c73f1-127">So, the optimal choice of partitioning key for this type would be `UserId`.</span></span>

    class Notification 
    { 
        // Unique ID for Notification. 
        public string Id { get; set; }

        // The user Id for which notification is addressed to. 
        public string UserId { get; set; }

        // The partition Key for the resource. 
        public string PartitionKey 
        { 
            get 
            { 
                return this.UserId; 
            }
        }

        // Subscription for which this notification is raised. 
        public string SubscriptionFilter { get; set; }

        // Subject of the notification. 
        public string ArticleId { get; set; } 
    }

## <span data-ttu-id="c73f1-128"><a id="ModelingSubscriptions"></a>建立模型訂閱</span><span class="sxs-lookup"><span data-stu-id="c73f1-128"><a id="ModelingSubscriptions"></a>Modeling subscriptions</span></span>
<span data-ttu-id="c73f1-129">針對感興趣的特定文章類別或特定發行者的各種準則來建立訂閱。</span><span class="sxs-lookup"><span data-stu-id="c73f1-129">Subscriptions can be created for various criteria like a specific category of articles of interest, or a specific publisher.</span></span> <span data-ttu-id="c73f1-130">因此 `SubscriptionFilter` 會是不錯的資料分割索引鍵選擇。</span><span class="sxs-lookup"><span data-stu-id="c73f1-130">Hence the `SubscriptionFilter` is a good choice for partition key.</span></span>

    class Subscriptions 
    { 
        // Unique ID for Subscription 
        public string Id { get; set; }

        // Subscription source. Could be Author | Category etc. 
        public string SubscriptionFilter { get; set; }

        // subscribing User. 
        public string UserId { get; set; }

        public string PartitionKey 
        { 
            get 
            { 
                return this.SubscriptionFilter; 
            } 
        } 
    }

## <span data-ttu-id="c73f1-131"><a id="ModelingArticles"></a>建立模型文件</span><span class="sxs-lookup"><span data-stu-id="c73f1-131"><a id="ModelingArticles"></a>Modeling articles</span></span>
<span data-ttu-id="c73f1-132">一旦透過通知來識別文章，後續查詢通常會以 `Article.Id` 為基礎。</span><span class="sxs-lookup"><span data-stu-id="c73f1-132">Once an article is identified through notifications, subsequent queries are typically based on the `Article.Id`.</span></span> <span data-ttu-id="c73f1-133">因此選擇 `Article.Id` 當成資料分割索引鍵，可提供在 Azure Cosmos DB 集合內儲存文章最佳的發佈方式。</span><span class="sxs-lookup"><span data-stu-id="c73f1-133">Choosing `Article.Id` as partition the key thus provides the best distribution for storing articles inside an Azure Cosmos DB collection.</span></span> 

    class Article 
    { 
        // Unique ID for Article 
        public string Id { get; set; }
        
        public string PartitionKey 
        { 
            get 
            { 
                return this.Id; 
            } 
        }
        
        // Author of the article
        public string Author { get; set; }

        // Category/genre of the article
        public string Category { get; set; }

        // Tags associated with the article
        public string[] Tags { get; set; }

        // Title of the article
        public string Title { get; set; }
        
        //... 
    }

## <span data-ttu-id="c73f1-134"><a id="ModelingReviews"></a>建立模型評論</span><span class="sxs-lookup"><span data-stu-id="c73f1-134"><a id="ModelingReviews"></a>Modeling reviews</span></span>
<span data-ttu-id="c73f1-135">和文章一樣，評論大部分可在文章內容中撰寫和讀取。</span><span class="sxs-lookup"><span data-stu-id="c73f1-135">Like articles, reviews are mostly written and read in the context of article.</span></span> <span data-ttu-id="c73f1-136">選擇 `ArticleId` 當成資料分割索引鍵，可提供和文章相關聯的評論最佳的發佈方式並有效存取。</span><span class="sxs-lookup"><span data-stu-id="c73f1-136">Choosing `ArticleId` as a partition key provides best distribution and efficient access of reviews associated with article.</span></span> 

    class Review 
    { 
        // Unique ID for Review 
        public string Id { get; set; }

        // Article Id of the review 
        public string ArticleId { get; set; }

        public string PartitionKey 
        { 
            get 
            { 
                return this.ArticleId; 
            } 
        }
        
        //Reviewer Id 
        public string UserId { get; set; }
        public string ReviewText { get; set; }
        
        public int Rating { get; set; } }
    }

## <span data-ttu-id="c73f1-137"><a id="DataAccessMethods"></a>資料存取層方法</span><span class="sxs-lookup"><span data-stu-id="c73f1-137"><a id="DataAccessMethods"></a>Data access layer methods</span></span>
<span data-ttu-id="c73f1-138">現在來看看我們必須實作的主要資料存取方法。</span><span class="sxs-lookup"><span data-stu-id="c73f1-138">Now let's look at the main data access methods we need to implement.</span></span> <span data-ttu-id="c73f1-139">以下是 `ContentPublishDatabase` 需要的方法清單︰</span><span class="sxs-lookup"><span data-stu-id="c73f1-139">Here's the list of methods that the `ContentPublishDatabase` needs:</span></span>

    class ContentPublishDatabase 
    { 
        public async Task CreateSubscriptionAsync(string userId, string category);
    
        public async Task<IEnumerable<Notification>> ReadNotificationFeedAsync(string userId);
    
        public async Task<Article> ReadArticleAsync(string articleId);
    
        public async Task WriteReviewAsync(string articleId, string userId, string reviewText, int rating);
    
        public async Task<IEnumerable<Review>> ReadReviewsAsync(string articleId); 
    }

## <span data-ttu-id="c73f1-140"><a id="Architecture"></a>Azure Cosmos DB 帳戶組態</span><span class="sxs-lookup"><span data-stu-id="c73f1-140"><a id="Architecture"></a>Azure Cosmos DB account configuration</span></span>
<span data-ttu-id="c73f1-141">若要保證本機讀取和寫入，不只要針對資料分割索引鍵，也要根據區域的地理存取模式來分割資料。</span><span class="sxs-lookup"><span data-stu-id="c73f1-141">To guarantee local reads and writes, we must partition data not just on partition key, but also based on the geographical access pattern into regions.</span></span> <span data-ttu-id="c73f1-142">模型依存於每個區域的異地複寫 Azure Cosmos DB 資料庫帳戶。</span><span class="sxs-lookup"><span data-stu-id="c73f1-142">The model relies on having a geo-replicated Azure Cosmos DB database account for each region.</span></span> <span data-ttu-id="c73f1-143">以兩個區域為例，多重區域寫入設定如下︰</span><span class="sxs-lookup"><span data-stu-id="c73f1-143">For example, with two regions, here's a setup for multi-region writes:</span></span>

| <span data-ttu-id="c73f1-144">帳戶名稱</span><span class="sxs-lookup"><span data-stu-id="c73f1-144">Account Name</span></span> | <span data-ttu-id="c73f1-145">寫入區域</span><span class="sxs-lookup"><span data-stu-id="c73f1-145">Write Region</span></span> | <span data-ttu-id="c73f1-146">讀取區域</span><span class="sxs-lookup"><span data-stu-id="c73f1-146">Read Region</span></span> |
| --- | --- | --- |
| `contentpubdatabase-usa.documents.azure.com` | `West US` |`North Europe` |
| `contentpubdatabase-europe.documents.azure.com` | `North Europe` |`West US` |

<span data-ttu-id="c73f1-147">下圖顯示如何以這種設定在一般應用程式中執行讀取和寫入︰</span><span class="sxs-lookup"><span data-stu-id="c73f1-147">The following diagram shows how reads and writes are performed in a typical application with this setup:</span></span>

![Azure Cosmos DB 多重主機架構](./media/multi-region-writers/multi-master.png)

<span data-ttu-id="c73f1-149">如何在`West US`區域中執行的 DAL 中，初始化用戶端的程式碼片段如下。</span><span class="sxs-lookup"><span data-stu-id="c73f1-149">Here is a code snippet showing how to initialize the clients in a DAL running in the `West US` region.</span></span>
    
    ConnectionPolicy writeClientPolicy = new ConnectionPolicy { ConnectionMode = ConnectionMode.Direct, ConnectionProtocol = Protocol.Tcp };
    writeClientPolicy.PreferredLocations.Add(LocationNames.WestUS);
    writeClientPolicy.PreferredLocations.Add(LocationNames.NorthEurope);

    DocumentClient writeClient = new DocumentClient(
        new Uri("https://contentpubdatabase-usa.documents.azure.com"), 
        writeRegionAuthKey,
        writeClientPolicy);

    ConnectionPolicy readClientPolicy = new ConnectionPolicy { ConnectionMode = ConnectionMode.Direct, ConnectionProtocol = Protocol.Tcp };
    readClientPolicy.PreferredLocations.Add(LocationNames.NorthEurope);
    readClientPolicy.PreferredLocations.Add(LocationNames.WestUS);

    DocumentClient readClient = new DocumentClient(
        new Uri("https://contentpubdatabase-europe.documents.azure.com"),
        readRegionAuthKey,
        readClientPolicy);

<span data-ttu-id="c73f1-150">利用上述設定，資料存取層可以根據部署位置，將所有寫入轉送至本機帳戶。</span><span class="sxs-lookup"><span data-stu-id="c73f1-150">With the preceding setup, the data access layer can forward all writes to the local account based on where it is deployed.</span></span> <span data-ttu-id="c73f1-151">藉由讀取這兩個帳戶，以取得資料的整體觀點來執行讀取。</span><span class="sxs-lookup"><span data-stu-id="c73f1-151">Reads are performed by reading from both accounts to get the global view of data.</span></span> <span data-ttu-id="c73f1-152">這種方法可以擴充到所需的各個區域。</span><span class="sxs-lookup"><span data-stu-id="c73f1-152">This approach can be extended to as many regions as required.</span></span> <span data-ttu-id="c73f1-153">例如，以下是三個地區設定︰</span><span class="sxs-lookup"><span data-stu-id="c73f1-153">For example, here's a setup with three geographic regions:</span></span>

| <span data-ttu-id="c73f1-154">帳戶名稱</span><span class="sxs-lookup"><span data-stu-id="c73f1-154">Account Name</span></span> | <span data-ttu-id="c73f1-155">寫入區域</span><span class="sxs-lookup"><span data-stu-id="c73f1-155">Write Region</span></span> | <span data-ttu-id="c73f1-156">讀取區域 1</span><span class="sxs-lookup"><span data-stu-id="c73f1-156">Read Region 1</span></span> | <span data-ttu-id="c73f1-157">讀取區域 2</span><span class="sxs-lookup"><span data-stu-id="c73f1-157">Read Region 2</span></span> |
| --- | --- | --- | --- |
| `contentpubdatabase-usa.documents.azure.com` | `West US` |`North Europe` |`Southeast Asia` |
| `contentpubdatabase-europe.documents.azure.com` | `North Europe` |`West US` |`Southeast Asia` |
| `contentpubdatabase-asia.documents.azure.com` | `Southeast Asia` |`North Europe` |`West US` |

## <span data-ttu-id="c73f1-158"><a id="DataAccessImplementation"></a>資料存取層實作</span><span class="sxs-lookup"><span data-stu-id="c73f1-158"><a id="DataAccessImplementation"></a>Data access layer implementation</span></span>
<span data-ttu-id="c73f1-159">現在讓我們來對有兩個可寫入區域的應用程式實作資料存取層 (DAL)。</span><span class="sxs-lookup"><span data-stu-id="c73f1-159">Now let's look at the implementation of the data access layer (DAL) for an application with two writable regions.</span></span> <span data-ttu-id="c73f1-160">DAL 必須實作下列步驟︰</span><span class="sxs-lookup"><span data-stu-id="c73f1-160">The DAL must implement the following steps:</span></span>

* <span data-ttu-id="c73f1-161">為每個帳戶建立 `DocumentClient` 的多個執行個體。</span><span class="sxs-lookup"><span data-stu-id="c73f1-161">Create multiple instances of `DocumentClient` for each account.</span></span> <span data-ttu-id="c73f1-162">使用兩個區域，每個 DAL 執行個體會有一個 `writeClient` 和一個 `readClient`。</span><span class="sxs-lookup"><span data-stu-id="c73f1-162">With two regions, each DAL instance has one `writeClient` and one `readClient`.</span></span> 
* <span data-ttu-id="c73f1-163">根據已部署應用程式的區域，設定 `writeclient` 和 `readClient` 的端點。</span><span class="sxs-lookup"><span data-stu-id="c73f1-163">Based on the deployed region of the application, configure the endpoints for `writeclient` and `readClient`.</span></span> <span data-ttu-id="c73f1-164">例如，部署在 `West US` 的 DAL 使用 `contentpubdatabase-usa.documents.azure.com` 執行寫入。</span><span class="sxs-lookup"><span data-stu-id="c73f1-164">For example, the DAL deployed in `West US` uses `contentpubdatabase-usa.documents.azure.com` for performing writes.</span></span> <span data-ttu-id="c73f1-165">部署在 `NorthEurope`的 DAL 使用 `contentpubdatabase-europ.documents.azure.com` 寫入。</span><span class="sxs-lookup"><span data-stu-id="c73f1-165">The DAL deployed in `NorthEurope` uses `contentpubdatabase-europ.documents.azure.com` for writes.</span></span>

<span data-ttu-id="c73f1-166">使用上述設定，就可以實作資料存取方法。</span><span class="sxs-lookup"><span data-stu-id="c73f1-166">With the preceding setup, the data access methods can be implemented.</span></span> <span data-ttu-id="c73f1-167">寫入作業會將寫入轉送到對應的 `writeClient`。</span><span class="sxs-lookup"><span data-stu-id="c73f1-167">Write operations forward the write to the corresponding `writeClient`.</span></span>

    public async Task CreateSubscriptionAsync(string userId, string category)
    {
        await this.writeClient.CreateDocumentAsync(this.contentCollection, new Subscriptions
        {
            UserId = userId,
            SubscriptionFilter = category
        });
    }

    public async Task WriteReviewAsync(string articleId, string userId, string reviewText, int rating)
    {
        await this.writeClient.CreateDocumentAsync(this.contentCollection, new Review
        {
            UserId = userId,
            ArticleId = articleId,
            ReviewText = reviewText,
            Rating = rating
        });
    }

<span data-ttu-id="c73f1-168">對於讀取通知和評論，您必須從區域和聯集兩者來讀取，結果如下列程式碼片段所示︰</span><span class="sxs-lookup"><span data-stu-id="c73f1-168">For reading notifications and reviews, you must read from both regions and union the results as shown in the following snippet:</span></span>

    public async Task<IEnumerable<Notification>> ReadNotificationFeedAsync(string userId)
    {
        IDocumentQuery<Notification> writeAccountNotification = (
            from notification in this.writeClient.CreateDocumentQuery<Notification>(this.contentCollection) 
            where notification.UserId == userId 
            select notification).AsDocumentQuery();
        
        IDocumentQuery<Notification> readAccountNotification = (
            from notification in this.readClient.CreateDocumentQuery<Notification>(this.contentCollection) 
            where notification.UserId == userId 
            select notification).AsDocumentQuery();

        List<Notification> notifications = new List<Notification>();

        while (writeAccountNotification.HasMoreResults || readAccountNotification.HasMoreResults)
        {
            IList<Task<FeedResponse<Notification>>> results = new List<Task<FeedResponse<Notification>>>();

            if (writeAccountNotification.HasMoreResults)
            {
                results.Add(writeAccountNotification.ExecuteNextAsync<Notification>());
            }

            if (readAccountNotification.HasMoreResults)
            {
                results.Add(readAccountNotification.ExecuteNextAsync<Notification>());
            }

            IList<FeedResponse<Notification>> notificationFeedResult = await Task.WhenAll(results);

            foreach (FeedResponse<Notification> feed in notificationFeedResult)
            {
                notifications.AddRange(feed);
            }
        }
        return notifications;
    }

    public async Task<IEnumerable<Review>> ReadReviewsAsync(string articleId)
    {
        IDocumentQuery<Review> writeAccountReviews = (
            from review in this.writeClient.CreateDocumentQuery<Review>(this.contentCollection) 
            where review.ArticleId == articleId 
            select review).AsDocumentQuery();
        
        IDocumentQuery<Review> readAccountReviews = (
            from review in this.readClient.CreateDocumentQuery<Review>(this.contentCollection) 
            where review.ArticleId == articleId 
            select review).AsDocumentQuery();

        List<Review> reviews = new List<Review>();
        
        while (writeAccountReviews.HasMoreResults || readAccountReviews.HasMoreResults)
        {
            IList<Task<FeedResponse<Review>>> results = new List<Task<FeedResponse<Review>>>();

            if (writeAccountReviews.HasMoreResults)
            {
                results.Add(writeAccountReviews.ExecuteNextAsync<Review>());
            }

            if (readAccountReviews.HasMoreResults)
            {
                results.Add(readAccountReviews.ExecuteNextAsync<Review>());
            }

            IList<FeedResponse<Review>> notificationFeedResult = await Task.WhenAll(results);

            foreach (FeedResponse<Review> feed in notificationFeedResult)
            {
                reviews.AddRange(feed);
            }
        }

        return reviews;
    }

<span data-ttu-id="c73f1-169">因此，選擇良好的分割索引鍵和靜態帳戶型的資料分割，您就可以使用 Azure Cosmos DB 達到多重區域本機寫入和讀取。</span><span class="sxs-lookup"><span data-stu-id="c73f1-169">Thus, by choosing a good partitioning key and static account-based partitioning, you can achieve multi-region local writes and reads using Azure Cosmos DB.</span></span>

## <span data-ttu-id="c73f1-170"><a id="NextSteps"></a>接續步驟</span><span class="sxs-lookup"><span data-stu-id="c73f1-170"><a id="NextSteps"></a>Next steps</span></span>
<span data-ttu-id="c73f1-171">我們會在本文說明如何使用發佈為範例案例的內容，利用 Azure Cosmos DB 使用分散在世界各地的多重區域讀取和寫入模式。</span><span class="sxs-lookup"><span data-stu-id="c73f1-171">In this article, we described how you can use globally distributed multi-region read write patterns with Azure Cosmos DB using content publishing as a sample scenario.</span></span>

* <span data-ttu-id="c73f1-172">了解 Azure Cosmos DB 如何支援[全域發佈](distribute-data-globally.md)</span><span class="sxs-lookup"><span data-stu-id="c73f1-172">Learn about how Azure Cosmos DB supports [global distribution](distribute-data-globally.md)</span></span>
* <span data-ttu-id="c73f1-173">了解 [Azure Cosmos DB 中的自動化和手動容錯移轉](regional-failover.md)</span><span class="sxs-lookup"><span data-stu-id="c73f1-173">Learn about [automatic and manual failovers in Azure Cosmos DB](regional-failover.md)</span></span>
* <span data-ttu-id="c73f1-174">了解 [Azure Cosmos DB 的全域一致性](consistency-levels.md)</span><span class="sxs-lookup"><span data-stu-id="c73f1-174">Learn about [global consistency with Azure Cosmos DB](consistency-levels.md)</span></span>
* <span data-ttu-id="c73f1-175">使用 [Azure Cosmos DB - DocumentDB API](tutorial-global-distribution-documentdb.md) 進行多區域開發</span><span class="sxs-lookup"><span data-stu-id="c73f1-175">Develop with multiple regions using the [Azure Cosmos DB - DocumentDB API](tutorial-global-distribution-documentdb.md)</span></span>
* <span data-ttu-id="c73f1-176">使用 [Azure Cosmos DB - MongoDB API](tutorial-global-distribution-MongoDB.md) 進行多區域開發</span><span class="sxs-lookup"><span data-stu-id="c73f1-176">Develop with multiple regions using the [Azure Cosmos DB - MongoDB API](tutorial-global-distribution-MongoDB.md)</span></span>
* <span data-ttu-id="c73f1-177">使用 [Azure Cosmos DB - Table API](tutorial-global-distribution-table.md) 進行多區域開發</span><span class="sxs-lookup"><span data-stu-id="c73f1-177">Develop with multiple regions using the [Azure Cosmos DB - Table API](tutorial-global-distribution-table.md)</span></span>
