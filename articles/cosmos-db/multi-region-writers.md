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
# <a name="multi-master-globally-replicated-database-architectures-with-azure-cosmos-db"></a>使用 Azure Cosmos DB 的多重主機全域複寫資料庫架構
Azure Cosmos DB 支援通行[全域複寫](distribute-data-globally.md)，可讓您 toodistribute 資料 toomultiple 區域具有低度延遲 hello 工作負載中任何位置的存取權。 此模型通常用於發行者/取用者工作負載，寫入器在單一地理區域中，而讀取器 (讀取) 分散在世界各地的其他區域。 

您也可以使用 Azure Cosmos DB 的全域複寫支援 toobuild 應用程式在其中寫入器和讀取器會全域散發。 本文概述的模式可讓使用 Azure Cosmos DB 的分散式寫入器達成本機寫入及本機讀取存取。

## <a id="ExampleScenario"></a>內容發佈 - 範例案例
讓我們看看真實世界案例 toodescribe 如何搭配 Azure Cosmos DB 使用全域散發 region 多/主多讀的寫模式。 以建置在 Azure Cosmos DB 上的內容發佈平台為例。 這個平台必須符合以下一些需求，才能獲得絕佳發行者和取用者使用者體驗。

* 作者和訂閱者分散 hello world 
* 作者必須發佈 （寫入） 文章 tootheir （最接近） 區域
* 作者可讀取者/其文件的 「 訂閱者 」 的分散 hello 地球。 
* 發佈新文章時，訂閱者應該收到通知。
* 「 訂閱者 」 必須從其區域可以 tooread 文件。 它們也應該能夠 tooadd 檢閱 toothese 文件。 
* 包括 hello 作者的 hello 文件的任何人都應該可以檢視所有 hello 檢閱附加的 tooarticles 從區域。 

假設包含數百萬個取用者和發行者使用數十億個發行項，我們很快就能 tooconfront hello 問題，以及存取的位置，以及確保標尺。 如同大部分的延展性問題 hello 方案在於良好的資料分割策略。 接下來，讓我們看看如何 toomodel 文件、 檢閱及通知文件，以設定 Azure Cosmos DB 帳戶並實作資料存取層。 

如果您想要深入了解資料分割和資料分割索引鍵 toolearn，請參閱[資料分割和 Azure Cosmos DB 中的縮放比例](partition-data.md)。

## <a id="ModelingNotifications"></a>建立模型通知
通知是資料摘要 tooa 特定使用者。 因此，hello 通知文件的存取模式一律會在單一使用者 hello 內容。 比方說，您會"post 通知 tooa 使用者 」 或者 「 擷取指定使用者的所有通知 」。 因此，hello 的資料分割索引鍵，這種類型會最佳選擇`UserId`。

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

## <a id="ModelingSubscriptions"></a>建立模型訂閱
針對感興趣的特定文章類別或特定發行者的各種準則來建立訂閱。 因此 hello`SubscriptionFilter`是不錯的選擇的資料分割索引鍵。

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

## <a id="ModelingArticles"></a>建立模型文件
一旦識別發行項所在的通知，後續的查詢通常根據 hello `Article.Id`。 選擇`Article.Id`為分割區 hello 金鑰因此提供來儲存 Azure Cosmos DB 集合內的發行項的 hello 最佳散發。 

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

## <a id="ModelingReviews"></a>建立模型評論
發行項，例如檢閱大部分寫入並讀取 hello 內容的發行項中。 選擇 `ArticleId` 當成資料分割索引鍵，可提供和文章相關聯的評論最佳的發佈方式並有效存取。 

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

## <a id="DataAccessMethods"></a>資料存取層方法
現在讓我們看看 hello 主要資料存取方法，我們需要 tooimplement。 以下是 hello hello 的方法清單`ContentPublishDatabase`需要：

    class ContentPublishDatabase 
    { 
        public async Task CreateSubscriptionAsync(string userId, string category);
    
        public async Task<IEnumerable<Notification>> ReadNotificationFeedAsync(string userId);
    
        public async Task<Article> ReadArticleAsync(string articleId);
    
        public async Task WriteReviewAsync(string articleId, string userId, string reviewText, int rating);
    
        public async Task<IEnumerable<Review>> ReadReviewsAsync(string articleId); 
    }

## <a id="Architecture"></a>Azure Cosmos DB 帳戶組態
tooguarantee 本機讀取和寫入，我們必須分割資料，不只是根據資料分割索引鍵，但也會根據成區域的 hello 地理位置的存取模式。 hello 模型會依賴擁有針對每個區域進行地理複寫 Azure Cosmos DB 資料庫帳戶。 以兩個區域為例，多重區域寫入設定如下︰

| 帳戶名稱 | 寫入區域 | 讀取區域 |
| --- | --- | --- |
| `contentpubdatabase-usa.documents.azure.com` | `West US` |`North Europe` |
| `contentpubdatabase-europe.documents.azure.com` | `North Europe` |`West US` |

hello 下圖顯示如何執行此安裝程式的一般應用程式中的讀取和寫入：

![Azure Cosmos DB 多重主機架構](./media/multi-region-writers/multi-master.png)

以下是程式碼片段顯示如何 tooinitialize hello DAL hello 在執行中的用戶端`West US`區域。
    
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

以 hello 之前安裝程式，hello 資料存取層可以轉送所有寫入 toohello 本機帳戶根據部署的位置。 藉由讀取資料這兩個帳戶 tooget hello 全域檢視執行的讀取。 這個方法可能擴充 tooas 所需的許多區域。 例如，以下是三個地區設定︰

| 帳戶名稱 | 寫入區域 | 讀取區域 1 | 讀取區域 2 |
| --- | --- | --- | --- |
| `contentpubdatabase-usa.documents.azure.com` | `West US` |`North Europe` |`Southeast Asia` |
| `contentpubdatabase-europe.documents.azure.com` | `North Europe` |`West US` |`Southeast Asia` |
| `contentpubdatabase-asia.documents.azure.com` | `Southeast Asia` |`North Europe` |`West US` |

## <a id="DataAccessImplementation"></a>資料存取層實作
現在讓我們看看 hello hello 資料存取層 (DAL) 具有兩個可寫入的區域的應用程式的實作。 hello DAL 必須實作 hello 下列步驟：

* 為每個帳戶建立 `DocumentClient` 的多個執行個體。 使用兩個區域，每個 DAL 執行個體會有一個 `writeClient` 和一個 `readClient`。 
* 根據部署的 hello 區域 hello 應用程式，設定的端點 hello`writeclient`和`readClient`。 比方說，hello DAL 部署在`West US`使用`contentpubdatabase-usa.documents.azure.com`執行寫入。 在中部署的 hello DAL`NorthEurope`使用`contentpubdatabase-europ.documents.azure.com`寫入。

以 hello 之前安裝程式，可以實作 hello 資料存取方法。 寫入作業轉寄 hello 寫入 toohello 對應`writeClient`。

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

讀取通知和評論，您必須從讀取區域和等位的 hello 結果 hello 下列程式碼片段所示：

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

因此，選擇良好的分割索引鍵和靜態帳戶型的資料分割，您就可以使用 Azure Cosmos DB 達到多重區域本機寫入和讀取。

## <a id="NextSteps"></a>接續步驟
我們會在本文說明如何使用發佈為範例案例的內容，利用 Azure Cosmos DB 使用分散在世界各地的多重區域讀取和寫入模式。

* 了解 Azure Cosmos DB 如何支援[全域發佈](distribute-data-globally.md)
* 了解 [Azure Cosmos DB 中的自動化和手動容錯移轉](regional-failover.md)
* 了解 [Azure Cosmos DB 的全域一致性](consistency-levels.md)
* 使用多個區域使用 hello 開發[Azure Cosmos DB DocumentDB API](tutorial-global-distribution-documentdb.md)
* 使用多個區域使用 hello 開發[Azure Cosmos DB MongoDB 應用程式開發介面](tutorial-global-distribution-MongoDB.md)
* 使用多個區域使用 hello 開發[Azure Cosmos DB 資料表 API](tutorial-global-distribution-table.md)
