---
title: "以 Azure Cosmos DB aaaMulti master 資料庫架構 |Microsoft 文件"
description: "深入了解 toodesign 應用程式架構，與本機讀取及寫入到 Azure Cosmos db 的多個地理區域的方式。"
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
ms.openlocfilehash: 3269c8405afe16f75db69b42e576fe76e00a8e16
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="multi-master-globally-replicated-database-architectures-with-azure-cosmos-db"></a><span data-ttu-id="b40ef-103">使用 Azure Cosmos DB 的多重主機全域複寫資料庫架構</span><span class="sxs-lookup"><span data-stu-id="b40ef-103">Multi-master globally replicated database architectures with Azure Cosmos DB</span></span>
<span data-ttu-id="b40ef-104">Azure Cosmos DB 支援通行[全域複寫](distribute-data-globally.md)，可讓您 toodistribute 資料 toomultiple 區域具有低度延遲 hello 工作負載中任何位置的存取權。</span><span class="sxs-lookup"><span data-stu-id="b40ef-104">Azure Cosmos DB supports turnkey [global replication](distribute-data-globally.md), which allows you toodistribute data toomultiple regions with low latency access anywhere in hello workload.</span></span> <span data-ttu-id="b40ef-105">此模型通常用於發行者/取用者工作負載，寫入器在單一地理區域中，而讀取器 (讀取) 分散在世界各地的其他區域。</span><span class="sxs-lookup"><span data-stu-id="b40ef-105">This model is commonly used for publisher/consumer workloads where there is a writer in a single geographic region and globally distributed readers in other (read) regions.</span></span> 

<span data-ttu-id="b40ef-106">您也可以使用 Azure Cosmos DB 的全域複寫支援 toobuild 應用程式在其中寫入器和讀取器會全域散發。</span><span class="sxs-lookup"><span data-stu-id="b40ef-106">You can also use Azure Cosmos DB's global replication support toobuild applications in which writers and readers are globally distributed.</span></span> <span data-ttu-id="b40ef-107">本文概述的模式可讓使用 Azure Cosmos DB 的分散式寫入器達成本機寫入及本機讀取存取。</span><span class="sxs-lookup"><span data-stu-id="b40ef-107">This document outlines a pattern that enables achieving local write and local read access for distributed writers using Azure Cosmos DB.</span></span>

## <span data-ttu-id="b40ef-108"><a id="ExampleScenario"></a>內容發佈 - 範例案例</span><span class="sxs-lookup"><span data-stu-id="b40ef-108"><a id="ExampleScenario"></a>Content Publishing - an example scenario</span></span>
<span data-ttu-id="b40ef-109">讓我們看看真實世界案例 toodescribe 如何搭配 Azure Cosmos DB 使用全域散發 region 多/主多讀的寫模式。</span><span class="sxs-lookup"><span data-stu-id="b40ef-109">Let's look at a real world scenario toodescribe how you can use globally distributed multi-region/multi-master read write patterns with Azure Cosmos DB.</span></span> <span data-ttu-id="b40ef-110">以建置在 Azure Cosmos DB 上的內容發佈平台為例。</span><span class="sxs-lookup"><span data-stu-id="b40ef-110">Consider a content publishing platform built on Azure Cosmos DB.</span></span> <span data-ttu-id="b40ef-111">這個平台必須符合以下一些需求，才能獲得絕佳發行者和取用者使用者體驗。</span><span class="sxs-lookup"><span data-stu-id="b40ef-111">Here are some requirements that this platform must meet for a great user experience for both publishers and consumers.</span></span>

* <span data-ttu-id="b40ef-112">作者和訂閱者分散 hello world</span><span class="sxs-lookup"><span data-stu-id="b40ef-112">Both authors and subscribers are spread over hello world</span></span> 
* <span data-ttu-id="b40ef-113">作者必須發佈 （寫入） 文章 tootheir （最接近） 區域</span><span class="sxs-lookup"><span data-stu-id="b40ef-113">Authors must publish (write) articles tootheir local (closest) region</span></span>
* <span data-ttu-id="b40ef-114">作者可讀取者/其文件的 「 訂閱者 」 的分散 hello 地球。</span><span class="sxs-lookup"><span data-stu-id="b40ef-114">Authors have readers/subscribers of their articles who are distributed across hello globe.</span></span> 
* <span data-ttu-id="b40ef-115">發佈新文章時，訂閱者應該收到通知。</span><span class="sxs-lookup"><span data-stu-id="b40ef-115">Subscribers should get a notification when new articles are published.</span></span>
* <span data-ttu-id="b40ef-116">「 訂閱者 」 必須從其區域可以 tooread 文件。</span><span class="sxs-lookup"><span data-stu-id="b40ef-116">Subscribers must be able tooread articles from their local region.</span></span> <span data-ttu-id="b40ef-117">它們也應該能夠 tooadd 檢閱 toothese 文件。</span><span class="sxs-lookup"><span data-stu-id="b40ef-117">They should also be able tooadd reviews toothese articles.</span></span> 
* <span data-ttu-id="b40ef-118">包括 hello 作者的 hello 文件的任何人都應該可以檢視所有 hello 檢閱附加的 tooarticles 從區域。</span><span class="sxs-lookup"><span data-stu-id="b40ef-118">Anyone including hello author of hello articles should be able view all hello reviews attached tooarticles from a local region.</span></span> 

<span data-ttu-id="b40ef-119">假設包含數百萬個取用者和發行者使用數十億個發行項，我們很快就能 tooconfront hello 問題，以及存取的位置，以及確保標尺。</span><span class="sxs-lookup"><span data-stu-id="b40ef-119">Assuming millions of consumers and publishers with billions of articles, soon we have tooconfront hello problems of scale along with guaranteeing locality of access.</span></span> <span data-ttu-id="b40ef-120">如同大部分的延展性問題 hello 方案在於良好的資料分割策略。</span><span class="sxs-lookup"><span data-stu-id="b40ef-120">As with most scalability problems, hello solution lies in a good partitioning strategy.</span></span> <span data-ttu-id="b40ef-121">接下來，讓我們看看如何 toomodel 文件、 檢閱及通知文件，以設定 Azure Cosmos DB 帳戶並實作資料存取層。</span><span class="sxs-lookup"><span data-stu-id="b40ef-121">Next, let's look at how toomodel articles, review, and notifications as documents, configure Azure Cosmos DB accounts, and implement a data access layer.</span></span> 

<span data-ttu-id="b40ef-122">如果您想要深入了解資料分割和資料分割索引鍵 toolearn，請參閱[資料分割和 Azure Cosmos DB 中的縮放比例](partition-data.md)。</span><span class="sxs-lookup"><span data-stu-id="b40ef-122">If you would like toolearn more about partitioning and partition keys, see [Partitioning and Scaling in Azure Cosmos DB](partition-data.md).</span></span>

## <span data-ttu-id="b40ef-123"><a id="ModelingNotifications"></a>建立模型通知</span><span class="sxs-lookup"><span data-stu-id="b40ef-123"><a id="ModelingNotifications"></a>Modeling notifications</span></span>
<span data-ttu-id="b40ef-124">通知是資料摘要 tooa 特定使用者。</span><span class="sxs-lookup"><span data-stu-id="b40ef-124">Notifications are data feeds specific tooa user.</span></span> <span data-ttu-id="b40ef-125">因此，hello 通知文件的存取模式一律會在單一使用者 hello 內容。</span><span class="sxs-lookup"><span data-stu-id="b40ef-125">Therefore, hello access patterns for notifications documents are always in hello context of single user.</span></span> <span data-ttu-id="b40ef-126">比方說，您會"post 通知 tooa 使用者 」 或者 「 擷取指定使用者的所有通知 」。</span><span class="sxs-lookup"><span data-stu-id="b40ef-126">For example, you would "post a notification tooa user" or "fetch all notifications for a given user".</span></span> <span data-ttu-id="b40ef-127">因此，hello 的資料分割索引鍵，這種類型會最佳選擇`UserId`。</span><span class="sxs-lookup"><span data-stu-id="b40ef-127">So, hello optimal choice of partitioning key for this type would be `UserId`.</span></span>

    class Notification 
    { 
        // Unique ID for Notification. 
        public string Id { get; set; }

        // hello user Id for which notification is addressed to. 
        public string UserId { get; set; }

        // hello partition Key for hello resource. 
        public string PartitionKey 
        { 
            get 
            { 
                return this.UserId; 
            }
        }

        // Subscription for which this notification is raised. 
        public string SubscriptionFilter { get; set; }

        // Subject of hello notification. 
        public string ArticleId { get; set; } 
    }

## <span data-ttu-id="b40ef-128"><a id="ModelingSubscriptions"></a>建立模型訂閱</span><span class="sxs-lookup"><span data-stu-id="b40ef-128"><a id="ModelingSubscriptions"></a>Modeling subscriptions</span></span>
<span data-ttu-id="b40ef-129">針對感興趣的特定文章類別或特定發行者的各種準則來建立訂閱。</span><span class="sxs-lookup"><span data-stu-id="b40ef-129">Subscriptions can be created for various criteria like a specific category of articles of interest, or a specific publisher.</span></span> <span data-ttu-id="b40ef-130">因此 hello`SubscriptionFilter`是不錯的選擇的資料分割索引鍵。</span><span class="sxs-lookup"><span data-stu-id="b40ef-130">Hence hello `SubscriptionFilter` is a good choice for partition key.</span></span>

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

## <span data-ttu-id="b40ef-131"><a id="ModelingArticles"></a>建立模型文件</span><span class="sxs-lookup"><span data-stu-id="b40ef-131"><a id="ModelingArticles"></a>Modeling articles</span></span>
<span data-ttu-id="b40ef-132">一旦識別發行項所在的通知，後續的查詢通常根據 hello `Article.Id`。</span><span class="sxs-lookup"><span data-stu-id="b40ef-132">Once an article is identified through notifications, subsequent queries are typically based on hello `Article.Id`.</span></span> <span data-ttu-id="b40ef-133">選擇`Article.Id`為分割區 hello 金鑰因此提供來儲存 Azure Cosmos DB 集合內的發行項的 hello 最佳散發。</span><span class="sxs-lookup"><span data-stu-id="b40ef-133">Choosing `Article.Id` as partition hello key thus provides hello best distribution for storing articles inside an Azure Cosmos DB collection.</span></span> 

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
        
        // Author of hello article
        public string Author { get; set; }

        // Category/genre of hello article
        public string Category { get; set; }

        // Tags associated with hello article
        public string[] Tags { get; set; }

        // Title of hello article
        public string Title { get; set; }
        
        //... 
    }

## <span data-ttu-id="b40ef-134"><a id="ModelingReviews"></a>建立模型評論</span><span class="sxs-lookup"><span data-stu-id="b40ef-134"><a id="ModelingReviews"></a>Modeling reviews</span></span>
<span data-ttu-id="b40ef-135">發行項，例如檢閱大部分寫入並讀取 hello 內容的發行項中。</span><span class="sxs-lookup"><span data-stu-id="b40ef-135">Like articles, reviews are mostly written and read in hello context of article.</span></span> <span data-ttu-id="b40ef-136">選擇 `ArticleId` 當成資料分割索引鍵，可提供和文章相關聯的評論最佳的發佈方式並有效存取。</span><span class="sxs-lookup"><span data-stu-id="b40ef-136">Choosing `ArticleId` as a partition key provides best distribution and efficient access of reviews associated with article.</span></span> 

    class Review 
    { 
        // Unique ID for Review 
        public string Id { get; set; }

        // Article Id of hello review 
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

## <span data-ttu-id="b40ef-137"><a id="DataAccessMethods"></a>資料存取層方法</span><span class="sxs-lookup"><span data-stu-id="b40ef-137"><a id="DataAccessMethods"></a>Data access layer methods</span></span>
<span data-ttu-id="b40ef-138">現在讓我們看看 hello 主要資料存取方法，我們需要 tooimplement。</span><span class="sxs-lookup"><span data-stu-id="b40ef-138">Now let's look at hello main data access methods we need tooimplement.</span></span> <span data-ttu-id="b40ef-139">以下是 hello hello 的方法清單`ContentPublishDatabase`需要：</span><span class="sxs-lookup"><span data-stu-id="b40ef-139">Here's hello list of methods that hello `ContentPublishDatabase` needs:</span></span>

    class ContentPublishDatabase 
    { 
        public async Task CreateSubscriptionAsync(string userId, string category);
    
        public async Task<IEnumerable<Notification>> ReadNotificationFeedAsync(string userId);
    
        public async Task<Article> ReadArticleAsync(string articleId);
    
        public async Task WriteReviewAsync(string articleId, string userId, string reviewText, int rating);
    
        public async Task<IEnumerable<Review>> ReadReviewsAsync(string articleId); 
    }

## <span data-ttu-id="b40ef-140"><a id="Architecture"></a>Azure Cosmos DB 帳戶組態</span><span class="sxs-lookup"><span data-stu-id="b40ef-140"><a id="Architecture"></a>Azure Cosmos DB account configuration</span></span>
<span data-ttu-id="b40ef-141">tooguarantee 本機讀取和寫入，我們必須分割資料，不只是根據資料分割索引鍵，但也會根據成區域的 hello 地理位置的存取模式。</span><span class="sxs-lookup"><span data-stu-id="b40ef-141">tooguarantee local reads and writes, we must partition data not just on partition key, but also based on hello geographical access pattern into regions.</span></span> <span data-ttu-id="b40ef-142">hello 模型會依賴擁有針對每個區域進行地理複寫 Azure Cosmos DB 資料庫帳戶。</span><span class="sxs-lookup"><span data-stu-id="b40ef-142">hello model relies on having a geo-replicated Azure Cosmos DB database account for each region.</span></span> <span data-ttu-id="b40ef-143">以兩個區域為例，多重區域寫入設定如下︰</span><span class="sxs-lookup"><span data-stu-id="b40ef-143">For example, with two regions, here's a setup for multi-region writes:</span></span>

| <span data-ttu-id="b40ef-144">帳戶名稱</span><span class="sxs-lookup"><span data-stu-id="b40ef-144">Account Name</span></span> | <span data-ttu-id="b40ef-145">寫入區域</span><span class="sxs-lookup"><span data-stu-id="b40ef-145">Write Region</span></span> | <span data-ttu-id="b40ef-146">讀取區域</span><span class="sxs-lookup"><span data-stu-id="b40ef-146">Read Region</span></span> |
| --- | --- | --- |
| `contentpubdatabase-usa.documents.azure.com` | `West US` |`North Europe` |
| `contentpubdatabase-europe.documents.azure.com` | `North Europe` |`West US` |

<span data-ttu-id="b40ef-147">hello 下圖顯示如何執行此安裝程式的一般應用程式中的讀取和寫入：</span><span class="sxs-lookup"><span data-stu-id="b40ef-147">hello following diagram shows how reads and writes are performed in a typical application with this setup:</span></span>

![Azure Cosmos DB 多重主機架構](./media/multi-region-writers/multi-master.png)

<span data-ttu-id="b40ef-149">以下是程式碼片段顯示如何 tooinitialize hello DAL hello 在執行中的用戶端`West US`區域。</span><span class="sxs-lookup"><span data-stu-id="b40ef-149">Here is a code snippet showing how tooinitialize hello clients in a DAL running in hello `West US` region.</span></span>
    
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

<span data-ttu-id="b40ef-150">以 hello 之前安裝程式，hello 資料存取層可以轉送所有寫入 toohello 本機帳戶根據部署的位置。</span><span class="sxs-lookup"><span data-stu-id="b40ef-150">With hello preceding setup, hello data access layer can forward all writes toohello local account based on where it is deployed.</span></span> <span data-ttu-id="b40ef-151">藉由讀取資料這兩個帳戶 tooget hello 全域檢視執行的讀取。</span><span class="sxs-lookup"><span data-stu-id="b40ef-151">Reads are performed by reading from both accounts tooget hello global view of data.</span></span> <span data-ttu-id="b40ef-152">這個方法可能擴充 tooas 所需的許多區域。</span><span class="sxs-lookup"><span data-stu-id="b40ef-152">This approach can be extended tooas many regions as required.</span></span> <span data-ttu-id="b40ef-153">例如，以下是三個地區設定︰</span><span class="sxs-lookup"><span data-stu-id="b40ef-153">For example, here's a setup with three geographic regions:</span></span>

| <span data-ttu-id="b40ef-154">帳戶名稱</span><span class="sxs-lookup"><span data-stu-id="b40ef-154">Account Name</span></span> | <span data-ttu-id="b40ef-155">寫入區域</span><span class="sxs-lookup"><span data-stu-id="b40ef-155">Write Region</span></span> | <span data-ttu-id="b40ef-156">讀取區域 1</span><span class="sxs-lookup"><span data-stu-id="b40ef-156">Read Region 1</span></span> | <span data-ttu-id="b40ef-157">讀取區域 2</span><span class="sxs-lookup"><span data-stu-id="b40ef-157">Read Region 2</span></span> |
| --- | --- | --- | --- |
| `contentpubdatabase-usa.documents.azure.com` | `West US` |`North Europe` |`Southeast Asia` |
| `contentpubdatabase-europe.documents.azure.com` | `North Europe` |`West US` |`Southeast Asia` |
| `contentpubdatabase-asia.documents.azure.com` | `Southeast Asia` |`North Europe` |`West US` |

## <span data-ttu-id="b40ef-158"><a id="DataAccessImplementation"></a>資料存取層實作</span><span class="sxs-lookup"><span data-stu-id="b40ef-158"><a id="DataAccessImplementation"></a>Data access layer implementation</span></span>
<span data-ttu-id="b40ef-159">現在讓我們看看 hello hello 資料存取層 (DAL) 具有兩個可寫入的區域的應用程式的實作。</span><span class="sxs-lookup"><span data-stu-id="b40ef-159">Now let's look at hello implementation of hello data access layer (DAL) for an application with two writable regions.</span></span> <span data-ttu-id="b40ef-160">hello DAL 必須實作 hello 下列步驟：</span><span class="sxs-lookup"><span data-stu-id="b40ef-160">hello DAL must implement hello following steps:</span></span>

* <span data-ttu-id="b40ef-161">為每個帳戶建立 `DocumentClient` 的多個執行個體。</span><span class="sxs-lookup"><span data-stu-id="b40ef-161">Create multiple instances of `DocumentClient` for each account.</span></span> <span data-ttu-id="b40ef-162">使用兩個區域，每個 DAL 執行個體會有一個 `writeClient` 和一個 `readClient`。</span><span class="sxs-lookup"><span data-stu-id="b40ef-162">With two regions, each DAL instance has one `writeClient` and one `readClient`.</span></span> 
* <span data-ttu-id="b40ef-163">根據部署的 hello 區域 hello 應用程式，設定的端點 hello`writeclient`和`readClient`。</span><span class="sxs-lookup"><span data-stu-id="b40ef-163">Based on hello deployed region of hello application, configure hello endpoints for `writeclient` and `readClient`.</span></span> <span data-ttu-id="b40ef-164">比方說，hello DAL 部署在`West US`使用`contentpubdatabase-usa.documents.azure.com`執行寫入。</span><span class="sxs-lookup"><span data-stu-id="b40ef-164">For example, hello DAL deployed in `West US` uses `contentpubdatabase-usa.documents.azure.com` for performing writes.</span></span> <span data-ttu-id="b40ef-165">在中部署的 hello DAL`NorthEurope`使用`contentpubdatabase-europ.documents.azure.com`寫入。</span><span class="sxs-lookup"><span data-stu-id="b40ef-165">hello DAL deployed in `NorthEurope` uses `contentpubdatabase-europ.documents.azure.com` for writes.</span></span>

<span data-ttu-id="b40ef-166">以 hello 之前安裝程式，可以實作 hello 資料存取方法。</span><span class="sxs-lookup"><span data-stu-id="b40ef-166">With hello preceding setup, hello data access methods can be implemented.</span></span> <span data-ttu-id="b40ef-167">寫入作業轉寄 hello 寫入 toohello 對應`writeClient`。</span><span class="sxs-lookup"><span data-stu-id="b40ef-167">Write operations forward hello write toohello corresponding `writeClient`.</span></span>

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

<span data-ttu-id="b40ef-168">讀取通知和評論，您必須從讀取區域和等位的 hello 結果 hello 下列程式碼片段所示：</span><span class="sxs-lookup"><span data-stu-id="b40ef-168">For reading notifications and reviews, you must read from both regions and union hello results as shown in hello following snippet:</span></span>

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

<span data-ttu-id="b40ef-169">因此，選擇良好的分割索引鍵和靜態帳戶型的資料分割，您就可以使用 Azure Cosmos DB 達到多重區域本機寫入和讀取。</span><span class="sxs-lookup"><span data-stu-id="b40ef-169">Thus, by choosing a good partitioning key and static account-based partitioning, you can achieve multi-region local writes and reads using Azure Cosmos DB.</span></span>

## <span data-ttu-id="b40ef-170"><a id="NextSteps"></a>接續步驟</span><span class="sxs-lookup"><span data-stu-id="b40ef-170"><a id="NextSteps"></a>Next steps</span></span>
<span data-ttu-id="b40ef-171">我們會在本文說明如何使用發佈為範例案例的內容，利用 Azure Cosmos DB 使用分散在世界各地的多重區域讀取和寫入模式。</span><span class="sxs-lookup"><span data-stu-id="b40ef-171">In this article, we described how you can use globally distributed multi-region read write patterns with Azure Cosmos DB using content publishing as a sample scenario.</span></span>

* <span data-ttu-id="b40ef-172">了解 Azure Cosmos DB 如何支援[全域發佈](distribute-data-globally.md)</span><span class="sxs-lookup"><span data-stu-id="b40ef-172">Learn about how Azure Cosmos DB supports [global distribution](distribute-data-globally.md)</span></span>
* <span data-ttu-id="b40ef-173">了解 [Azure Cosmos DB 中的自動化和手動容錯移轉](regional-failover.md)</span><span class="sxs-lookup"><span data-stu-id="b40ef-173">Learn about [automatic and manual failovers in Azure Cosmos DB](regional-failover.md)</span></span>
* <span data-ttu-id="b40ef-174">了解 [Azure Cosmos DB 的全域一致性](consistency-levels.md)</span><span class="sxs-lookup"><span data-stu-id="b40ef-174">Learn about [global consistency with Azure Cosmos DB](consistency-levels.md)</span></span>
* <span data-ttu-id="b40ef-175">使用多個區域使用 hello 開發[Azure Cosmos DB DocumentDB API](tutorial-global-distribution-documentdb.md)</span><span class="sxs-lookup"><span data-stu-id="b40ef-175">Develop with multiple regions using hello [Azure Cosmos DB - DocumentDB API](tutorial-global-distribution-documentdb.md)</span></span>
* <span data-ttu-id="b40ef-176">使用多個區域使用 hello 開發[Azure Cosmos DB MongoDB 應用程式開發介面](tutorial-global-distribution-MongoDB.md)</span><span class="sxs-lookup"><span data-stu-id="b40ef-176">Develop with multiple regions using hello [Azure Cosmos DB - MongoDB API](tutorial-global-distribution-MongoDB.md)</span></span>
* <span data-ttu-id="b40ef-177">使用多個區域使用 hello 開發[Azure Cosmos DB 資料表 API](tutorial-global-distribution-table.md)</span><span class="sxs-lookup"><span data-stu-id="b40ef-177">Develop with multiple regions using hello [Azure Cosmos DB - Table API](tutorial-global-distribution-table.md)</span></span>
