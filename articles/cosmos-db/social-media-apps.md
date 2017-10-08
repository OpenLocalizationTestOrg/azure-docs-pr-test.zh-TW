---
title: "Azure Cosmos DB 的設計模式：社交媒體應用程式 | Microsoft Docs"
description: "深入了解的設計模式的社交網路利用 hello Azure Cosmos DB 和其他 Azure 服務的儲存體彈性。"
keywords: "社交媒體應用程式"
services: cosmos-db
author: ealsur
manager: jhubbard
editor: 
documentationcenter: 
ms.assetid: 2dbf83a7-512a-4993-bf1b-ea7d72e095d9
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/29/2017
ms.author: mimig
ms.openlocfilehash: 47a22f2c5762d62b176921c8052e7bd75d8cf6ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="going-social-with-azure-cosmos-db"></a>使用 Azure Cosmos DB 跨足社交
在當今大幅互連的社會當中，我們的生活或多或少都成為 **社交網路**的一部分。 我們會使用與朋友、 同事、 家人或有時 tooshare 社交網路 tookeep 我們熱情與具有共同興趣的人。

身為工程師或開發人員，我們可能會想如何進行這些網路儲存和互連，我們的資料，或可能有即使已工作的 toocreate 或架構特定的範圍之外的新社交網路市場好多。 這是當 hello 大問題，就會發生： 所有這些資料儲存方式？

好比說，我們要建立脫穎而出的全新社交網路，讓使用者可以張貼文章並內含相關媒體，例如圖片、影片，甚至音樂。 使用者可以評論貼文，並給予評等的點數。 將使用者將會看到，並且是可以 toointeract 與 hello 主要網站登陸頁面上的文章的摘要。 這樣不聽得很複雜 （在第一個），但為了簡單明瞭的 hello 起見，我們就此停止 （我們無法深入自訂使用者摘要受到關聯性，但超出本文的 hello 目標）。

那麼，這些資料到底要如何儲存，以及儲存在哪呢？

許多您可能會有經驗的 SQL 資料庫，或至少具有概念[關聯式的資料模型化](https://en.wikipedia.org/wiki/Relational_model)，而且您可能想的 toostart 繪製結果類似這樣：

![說明相對關聯式模型的圖表](./media/social-media-apps/social-media-apps-sql.png) 

這麼正規且漂亮的資料結構... 卻無法調整。 

別誤會，我已經使用 SQL 資料庫很久了，知道它的確很棒，但它也跟其他的模式、做法和軟體平台一樣，不可能是萬能的。

為什麼無法在此案例中 SQL hello 最佳選擇？ 讓我們看看 hello 結構單一 post 要求，如果我想 tooshow 張貼在網站或應用程式時，我就得 toodo 的查詢... 8 資料表聯結 （！） 只是 tooshow 一個單一 post，現在，圖片的文章，以動態方式載入，並會出現在囉 」 畫面和您的資料流可能會看到我的重點。

我們可以當然，使用 humongous 的 SQL 執行個體具有足夠電源 toosolve 千分位的查詢與這些許多聯結 tooserve 我們的內容，但真正，我們更簡單的解決方案時要為什麼會存在嗎？

## <a name="hello-nosql-road"></a>hello NoSQL 路段圖
本文將引導您到 Azure 的 NoSQL 資料庫社交平台的資料模型化[Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/)符合成本效益的方式，同時利用其他 Azure Cosmos DB 功能，例如 hello [Gremlin Graph API](../cosmos-db/graph-introduction.md). 如果使用 [NoSQL](https://en.wikipedia.org/wiki/NoSQL) 方法，將資料以 JSON 格式儲存，並套用[反正規化](https://en.wikipedia.org/wiki/Denormalization)，即可將之前複雜的貼文轉換成單一[文件](https://en.wikipedia.org/wiki/Document-oriented_database)：


    {
        "id":"ew12-res2-234e-544f",
        "title":"post title",
        "date":"2016-01-01",
        "body":"this is an awesome post stored on NoSQL",
        "createdBy":User,
        "images":["http://myfirstimage.png","http://mysecondimage.png"],
        "videos":[
            {"url":"http://myfirstvideo.mp4", "title":"hello first video"},
            {"url":"http://mysecondvideo.mp4", "title":"hello second video"}
        ],
        "audios":[
            {"url":"http://myfirstaudio.mp3", "title":"hello first audio"},
            {"url":"http://mysecondaudio.mp3", "title":"hello second audio"}
        ]
    }

如此一來，即可利用單一查詢而不需要任何聯結，即可取得該文件。 這是更為簡單又直接，而且，budget-wise，需要較少的資源 tooachieve 更好的結果。

Azure Cosmos DB 可確保所有 hello 屬性都索引之使用其自動檢索，可能甚至會[自訂](indexing-policies.md)。 無結構描述的方法可讓我們以不同儲存文件和動態結構，或許明天我們想要處理的分類或 Cosmos DB 與其相關聯的雜湊標記清單文章 toohave hello 新文件以 hello hello 加入具有不需額外的屬性由我們所需的工作。

某篇文章的回應可視為含父屬性的其他貼文 (如此可簡化物件的對應)。 

    {
        "id":"1234-asd3-54ts-199a",
        "title":"Awesome post!",
        "date":"2016-01-02",
        "createdBy":User2,
        "parent":"ew12-res2-234e-544f"
    }

    {
        "id":"asd2-fee4-23gc-jh67",
        "title":"Ditto!",
        "date":"2016-01-03",
        "createdBy":User3,
        "parent":"ew12-res2-234e-544f"
    }

接著，即可將所有社交互動儲存為個別物件上的計數器︰

    {
        "id":"dfe3-thf5-232s-dse4",
        "post":"ew12-res2-234e-544f",
        "comments":2,
        "likes":10,
        "points":200
    }

若要建立摘要，只需建立文件，包含具有特定相關性順序的貼文識別碼清單即可︰

    [
        {"relevance":9, "post":"ew12-res2-234e-544f"},
        {"relevance":8, "post":"fer7-mnb6-fgh9-2344"},
        {"relevance":7, "post":"w34r-qeg6-ref6-8565"}
    ]

我們可能會根據建立日期排序的文章與有 「 最新 」 資料流、 文章詳細類似在 hello 與過去 24 小時的那些的 「 熱 」 資料流、 我們甚至無法實作根據邏輯實行項目與興趣，例如每個使用者自訂資料流和它仍會是一份 文章。 它是如何 toobuild 這些列出，但是 hello 讀取效能維持 unhindered。 一旦我們取得其中一個清單，我們就會發出單一查詢 tooCosmos DB 使用 hello[運算子中](documentdb-sql-query.md#WhereClause)tooobtain 頁面的文章，一次。

無法使用建立餵送資料流的 hello [Azure 應用程式服務的](https://azure.microsoft.com/services/app-service/)背景處理序： [Webjobs](../app-service-web/web-sites-create-web-jobs.md)。 背景處理 post 建立之後，可藉由使用[Azure 儲存體](https://azure.microsoft.com/services/storage/)[佇列](../storage/queues/storage-dotnet-how-to-use-queues.md)和 Webjob 觸發使用 hello [Azure Webjobs SDK](../app-service-web/websites-dotnet-webjobs-sdk.md)，它會實作hello 張貼根據自己的自訂邏輯的資料流內的傳播。 

延後的方式，使用這個相同的技巧 toocreate 最終一致性的環境可以處理點和透過 post 類似。

至於粉絲，則需要有更多的技巧來處理。 Cosmos DB 具有最大的文件大小限制，並讀取/寫入大型文件可能會影響應用程式的 hello 延展性。 因此，您可能會考慮使用下列結構，以文件形式儲存粉絲：

    {
        "id":"234d-sd23-rrf2-552d",
        "followersOf": "dse4-qwe2-ert4-aad2",
        "followers":[
            "ewr5-232d-tyrg-iuo2",
            "qejh-2345-sdf1-ytg5",
            //...
            "uie0-4tyg-3456-rwjh"
        ]
    }

這可能適用於具有少數數以千計的使用者實行項目，但如果某些名人聯結我們排列次序，這個方法會導致 tooa 大型文件大小，而且可能最後會叫用的 hello 文件大小限制。

toosolve，我們可以使用混合的方法。 Hello 使用者統計資料的文件的一部分，我們可以將儲存 hello 實行項目數目：

    {
        "id":"234d-sd23-rrf2-552d",
        "user": "dse4-qwe2-ert4-aad2",
        "followers":55230,
        "totalPosts":452,
        "totalPoints":11342
    }

而且可以使用 Azure Cosmos DB 儲存 hello 的實行項目實際的圖形[Gremlin Graph API](../cosmos-db/graph-introduction.md)，toocreate[頂點](http://mathworld.wolfram.com/GraphVertex.html)每位使用者和[邊緣](http://mathworld.wolfram.com/GraphEdge.html)來維護 hello"A 如下所示 B"關聯性。 hello Graph API 讓您取得特定使用者的 hello 實行項目不僅建立更複雜的查詢 tooeven 建議使用者在一般。 如果我們加入 toohello 圖形 hello 內容類別讓人喜歡或享受，我們可以開始 weaving 體驗，包括智慧內容探索，建議內容中，我們遵循所或尋找與其我們可能會有許多相同的人員。

hello 使用者統計資料的文件仍然可以使用的 toocreate 卡 hello UI 或快速分析 預覽中。

## <a name="hello-ladder-pattern-and-data-duplication"></a>hello"階梯 」 模式以及資料重複
您可能已經注意到參考 post hello JSON 文件中，沒有使用者的多個項目。 此外，您就已經猜到正確的這表示，代表使用者，提供此反正規化，hello 資訊可能會出現在多個位置。

在更快的查詢的順序 tooallow，我們會造成資料重複。 hello 問題具有此副作用是若某些動作，使用者的資料變更時，我們需要 toofind hello 的所有活動他曾未且更新全部。 聽起來不太實際，對吧？

我們會持續 toosolve 它藉由識別 hello 我們顯示在應用程式中的每個活動的使用者索引鍵屬性。 如果我們以視覺化方式顯示我們的應用程式中的文章，並顯示只要 hello 建立者的名稱與圖片，為什麼 hello 使用者資料的所有儲存 hello"createdby"屬性中？ 如果每個註解我們只會顯示 hello 使用者的圖片，我們不需要其資訊 hello 其餘部分。 這是其中呼叫 hello"階梯模式 」 的項目派上用場。

讓我們以使用者資訊當作範例︰

    {
        "id":"dse4-qwe2-ert4-aad2",
        "name":"John",
        "surname":"Doe",
        "address":"742 Evergreen Terrace",
        "birthday":"1983-05-07",
        "email":"john@doe.com",
        "twitterHandle":"@john",
        "username":"johndoe",
        "password":"some_encrypted_phrase",
        "totalPoints":100,
        "totalPosts":24
    }

查看此資訊可以快速偵測出哪些是重要資訊而哪些不是，以建立出一道「階梯」：

![階梯模式的圖表](./media/social-media-apps/social-media-apps-ladder.png)

hello 最小步驟稱為 UserChunk、 hello 可識別使用者資訊的最小的片段，它用於資料重複。 透過減少重複的 hello 資料 tooonly hello 資訊我們將 [顯示] hello 大小，我們會減少大量更新 hello 可能性。

hello 中間步驟呼叫 hello 使用者，它是最存取及最重要，hello hello Cosmos DB 上大部分的效能相依查詢將使用的完整資料。 其中包括 hello UserChunk 所代表的資訊。

hello 最大為 hello 擴充使用者。 它包含所有 hello 重大的使用者資訊加上不會真正快速需要 toobe 讀取其他資料，或它的使用方式 （例如 hello 登入程序） 最終。 這些資料可以儲存在 Cosmos DB 外部、Azure SQL Database 中或 Azure 儲存體資料表中。

為什麼我們會分割 hello 使用者，甚至將這項資訊存放在不同的地方嗎？ 因為從效能觀點來看，hello 更大的 hello 文件 hello costlier hello 查詢。 將文件輕薄 hello 與右資訊 toodo 所有您效能相關查詢以取得您的社交網路和存放區 hello 最終的案例，例如，完整設定檔的編輯，登入其他額外的資訊，甚至流量分析和大型的資料採礦資料開發案。 我們不在意 hello 資料收集的資料採礦時速度較慢，因為它正在 Azure SQL Database 上執行，我們不要有有關透過我們的使用者有快速而輕型的體驗。 儲存在 Cosmos DB 中的使用者，應類似如下︰

    {
        "id":"dse4-qwe2-ert4-aad2",
        "name":"John",
        "surname":"Doe",
        "username":"johndoe"
        "email":"john@doe.com",
        "twitterHandle":"@john"
    }

而貼文應該看起來像這樣：

    {
        "id":"1234-asd3-54ts-199a",
        "title":"Awesome post!",
        "date":"2016-01-02",
        "createdBy":{
            "id":"dse4-qwe2-ert4-aad2",
            "username":"johndoe"
        }
    }

當編輯就會發生影響其中一個 hello 區塊的 hello 屬性，它是簡單 toofind hello 影響文件使用點 toohello 編製索引屬性的查詢 (選取 * FROM 文章 p WHERE p.createdBy.id = ="edited_user_id")，然後更新hello 區塊。

## <a name="hello-search-box"></a>hello 搜尋方塊
一般來說，使用者都能很幸運地產生許多內容。 和我們應該能夠 tooprovide hello 能力 toosearch 並找到內容可能無法直接在其內容的資料流，可能因為我們未遵循 hello 建立者，或可能只有我們只想 toofind 我們所做的 6 個月前的舊 post。

幸好，因為我們使用 Azure Cosmos DB，我們可以輕鬆地實作搜尋引擎使用[Azure 搜尋](https://azure.microsoft.com/services/search/)需要幾分鐘的時間，而不需要輸入一行程式碼 （而不是很明顯地，hello 搜尋程序和 UI）。

為什麼可以這麼輕鬆？

Azure 搜尋實作它們的呼叫[索引子](https://msdn.microsoft.com/library/azure/dn946891.aspx)、 背景處理該攔截程序，在您的資料儲存機制中，自動新增、 更新或移除 hello 索引中的物件。 它們支援 [Azure SQL Database 索引子](https://blogs.msdn.microsoft.com/kaevans/2015/03/06/indexing-azure-sql-database-with-azure-search/)、[Azure Blob 索引子](../search/search-howto-indexing-azure-blob-storage.md)，甚至也支援 [Azure Cosmos DB 索引子](../search/search-howto-index-documentdb.md)。 hello 轉換 Cosmos DB tooAzure 搜尋中的資訊是那樣，這兩個存放區中的資訊 JSON 格式，我們只需要太[建立我們索引](../search/search-create-index-portal.md)，並將對應從我們的文件的屬性我們要編製索引，且它，在幾分鐘的時間 （取決於 hello 我們的資料大小），所有的內容將會使用 toobe 搜尋時，雲端基礎結構中 hello 最佳搜尋做為服務解決方案。 

如需 Azure 搜尋的詳細資訊，請造訪 hello [（英文) 的指南 tooSearch](https://blogs.msdn.microsoft.com/mvpawardprogram/2016/02/02/a-hitchhikers-guide-to-search/)。

## <a name="hello-underlying-knowledge"></a>hello 基礎知識
儲存這些所有內容之後，隨著內容每天不斷增長，我們可能會考慮到該怎麼運用這些使用者的資訊的串流？

hello 回應相當直接： 使其 toowork 並從中了解。

但是，我們可以學習到什麼呢？ 簡單的範例包括[情緒分析](https://en.wikipedia.org/wiki/Sentiment_analysis)，根據使用者的喜好設定的建議，或甚至自動化內容仲裁者，以確保所有 hello 發佈我們的社交網路的內容是安全的 hello 內容系列。

現在，我會收到您攔截，就可能會考慮您需要在數學科學 tooextract 某些博士這些模式和資訊從簡單的資料庫和檔案，但會發生錯誤。

[Azure Machine Learning](https://azure.microsoft.com/services/machine-learning/)，屬於 hello [Cortana 智慧套件](https://www.microsoft.com/en/server-cloud/cortana-analytics-suite/overview.aspx)，為 hello 完全受管理的雲端服務，可讓您建立簡單的拖放介面中使用的演算法的工作流程，您自己的演算法的程式碼在[R](https://en.wikipedia.org/wiki/R_\(programming_language\))或使用某些 hello 已經內建並就緒 toouse 應用程式開發介面，例如：[文字分析](https://gallery.cortanaanalytics.com/MachineLearningAPI/Text-Analytics-2)，[內容仲裁者](https://www.microsoft.com/moderator)或[建議](https://gallery.cortanaanalytics.com/MachineLearningAPI/Recommendations-2).

tooachieve 任何這些機器學習案例中，我們可以使用[Azure 資料湖](https://azure.microsoft.com/services/data-lake-store/)tooingest hello 不同來源的資訊，並使用[U-SQL](https://azure.microsoft.com/documentation/videos/data-lake-u-sql-query-execution/) tooprocess hello 資訊並產生輸出Azure Machine learning 可同時處理。

另一個可用的選項是 toouse [Microsoft 認知服務](https://www.microsoft.com/cognitive-services)tooanalyze 我們內容; 不只可以我們了解它們的使用者提供更好的 (透過分析這些寫入與[文字分析 API](https://www.microsoft.com/cognitive-services/en-us/text-analytics-api))，但我們無法偵測不想要或成熟的內容，並據此採取行動以[電腦願景 API](https://www.microsoft.com/cognitive-services/en-us/computer-vision-api)。 認知的服務包括大量不需要任何種類的機器學習知識 toouse 的全新的解決方案。

## <a name="a-planet-scale-social-experience"></a>全球規模的社交體驗
最後，我還有一項重要的主題必須和各位分享，那就是「延展性」。 設計相當重要的每個元件可以延展其本身，可能是因為我們需要更多資料 tooprocess 架構時，或因為我們想要 toohave 更大的地理涵蓋範圍 （或兩者 ！）。 幸好，透過 Cosmos DB，我們便能輕鬆完成如此複雜的工作。

Cosmos DB 支援[動態磁碟分割](https://azure.microsoft.com/blog/10-things-to-know-about-documentdb-partitioned-collections/)--蜪鎏藉由自動建立根據資料分割指定**資料分割索引鍵**（定義為文件中的 hello 屬性的其中之一）。 定義 hello 正確資料分割索引鍵必須以在設計階段和保留中注意 hello[最佳做法](../cosmos-db/partition-data.md#designing-for-partitioning)可用; 在社交體驗的 hello 情況下，資料分割策略必須對齊查詢 （讀取 hello 方法hello 內相同的資料分割都需要這樣做） 和寫入 （由多個資料分割上的寫入避免 「 作用點 」）。 某些選項： 暫時索引鍵為基礎 （日/月/週），依據內容的類別、 依地理區域，由使用者; 的磁碟分割所有它其實取決於如何查詢 hello 資料並顯示在您的社交體驗。 

其中一個值得一提的是有趣的一點是 Cosmos DB 將會執行您的查詢 (包括[彙總](https://azure.microsoft.com/blog/planet-scale-aggregates-with-azure-documentdb/)) 到您的資料分割以透明的方式，您不需要 tooadd 任何邏輯隨著您的資料。

流量最終會隨時間增長，而您的資源消耗 (以 [RU](request-units.md) (要求單位) 為單位) 也會增加。 您將讀寫更頻繁地為您 userbase 成長，同時會開始建立及讀取更多的內容。hello 能力**調整您的輸送量**而言非常重要。 增加我們 RUs 是非常簡單，我們可以按幾下 hello Azure 入口網站或藉由執行[發出命令 hello 應用程式開發介面透過](https://docs.microsoft.com/rest/api/documentdb/replace-an-offer)。

![相應增加及定義分割區索引鍵](./media/social-media-apps/social-media-apps-scaling.png)

如果很幸運地，有來自其他地區、國家或洲大陸的使用者注意到您的平台，並開始使用它，這還真是個好消息！

但稍候...您很快就了解他們的經驗與您的平台不是最佳選項。它們不在目前為止您操作區域 hello 延遲是可怕，，和您顯然不希望他們 tooquit。 要是有方法能輕鬆「觸達全球使用者」就好了。當然有！

Cosmos DB 可讓您[您的資料會進行全域複寫](../cosmos-db/tutorial-global-distribution-documentdb.md)以透明的方式有幾個動作，並自動選取 從 hello 可用地區之間和您[用戶端程式碼](../cosmos-db/tutorial-global-distribution-documentdb.md)。 這也表示您可以擁有[多個容錯移轉區域](regional-failover.md)。 

當您進行全域複寫您的資料時，您會需要 toomake 確定您的用戶端可以馬上使用該。 如果您使用的 web 前端或從行動用戶端存取 Api，您可以部署[Azure Traffic Manager](https://azure.microsoft.com/services/traffic-manager/)並複製到您的 Azure 應用程式服務上的所有預期的 hello 區域，使用[效能設定](../app-service-web/web-sites-traffic-manager.md)toosupport 擴充的全域涵蓋範圍。 當您的用戶端存取您的前端或應用程式開發介面時，就會路由的 toohello 最接近的應用程式服務，接著，將連接 toohello 本機 Cosmos DB 複本。

![正在將通用的涵蓋範圍 tooyour 社交平台](./media/social-media-apps/social-media-apps-global-replicate.png)

## <a name="conclusion"></a>結論
這篇文章會嘗試的 tooshed 某些淺 hello 替代方案的低成本服務與社交網路完全建立在 Azure 上，並提供絕佳的結果令人滿意的 hello 使用稱為 「 階梯"的多層的儲存體解決方案和資料發佈至。

![Azure 服務之間社交網路互動的圖表](./media/social-media-apps/social-media-apps-azure-solution.png)

hello 真為沒有靈丹這種情況下，它有 hello 的很好的服務可讓我們 toobuild 絕佳體驗的 hello 組合所建立的綜合設定： hello 速度和自由 Azure Cosmos DB tooprovide 絕佳的社交應用程式，hello 智慧背後的第一級的搜尋解決方案喜歡 Azure 搜尋時，Azure 應用程式服務 toohost hello 彈性不但功能強大的背景處理程序適用於多種語言的應用程式] 及 [hello 可展開的 Azure 儲存體和 Azure SQL Database。儲存大量的資料和 hello 分析電源的 Azure Machine Learning toocreate 知識和智慧，可提供意見反應 tooour 處理程序，並幫助我們傳遞 hello 右內容 toohello 適當的使用者。

## <a name="next-steps"></a>後續步驟
toolearn 有關 Cosmos DB 的使用案例的詳細資訊請參閱[常見 Cosmos DB 的使用案例](use-cases.md)。
