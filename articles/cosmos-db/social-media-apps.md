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
# <a name="going-social-with-azure-cosmos-db"></a><span data-ttu-id="65bf3-104">使用 Azure Cosmos DB 跨足社交</span><span class="sxs-lookup"><span data-stu-id="65bf3-104">Going social with Azure Cosmos DB</span></span>
<span data-ttu-id="65bf3-105">在當今大幅互連的社會當中，我們的生活或多或少都成為 **社交網路**的一部分。</span><span class="sxs-lookup"><span data-stu-id="65bf3-105">Living in a massively-interconnected society means that, at some point in life, you become part of a **social network**.</span></span> <span data-ttu-id="65bf3-106">我們會使用與朋友、 同事、 家人或有時 tooshare 社交網路 tookeep 我們熱情與具有共同興趣的人。</span><span class="sxs-lookup"><span data-stu-id="65bf3-106">We use social networks tookeep in touch with friends, colleagues, family, or sometimes tooshare our passion with people with common interests.</span></span>

<span data-ttu-id="65bf3-107">身為工程師或開發人員，我們可能會想如何進行這些網路儲存和互連，我們的資料，或可能有即使已工作的 toocreate 或架構特定的範圍之外的新社交網路市場好多。</span><span class="sxs-lookup"><span data-stu-id="65bf3-107">As engineers or developers, we might have wondered how do these networks store and interconnect our data, or might have even been tasked toocreate or architect a new social network for a specific niche market yourselves.</span></span> <span data-ttu-id="65bf3-108">這是當 hello 大問題，就會發生： 所有這些資料儲存方式？</span><span class="sxs-lookup"><span data-stu-id="65bf3-108">That’s when hello big question arises: How is all this data stored?</span></span>

<span data-ttu-id="65bf3-109">好比說，我們要建立脫穎而出的全新社交網路，讓使用者可以張貼文章並內含相關媒體，例如圖片、影片，甚至音樂。</span><span class="sxs-lookup"><span data-stu-id="65bf3-109">Let’s suppose that we are creating a new and shiny social network, where our users can post articles with related media like, pictures, videos, or even music.</span></span> <span data-ttu-id="65bf3-110">使用者可以評論貼文，並給予評等的點數。</span><span class="sxs-lookup"><span data-stu-id="65bf3-110">Users can comment on posts and give points for ratings.</span></span> <span data-ttu-id="65bf3-111">將使用者將會看到，並且是可以 toointeract 與 hello 主要網站登陸頁面上的文章的摘要。</span><span class="sxs-lookup"><span data-stu-id="65bf3-111">There will be a feed of posts that users will see and be able toointeract with on hello main website landing page.</span></span> <span data-ttu-id="65bf3-112">這樣不聽得很複雜 （在第一個），但為了簡單明瞭的 hello 起見，我們就此停止 （我們無法深入自訂使用者摘要受到關聯性，但超出本文的 hello 目標）。</span><span class="sxs-lookup"><span data-stu-id="65bf3-112">This doesn’t sound really complex (at first), but for hello sake of simplicity, let’s stop there (we could delve into custom user feeds affected by relationships, but it exceeds hello goal of this article).</span></span>

<span data-ttu-id="65bf3-113">那麼，這些資料到底要如何儲存，以及儲存在哪呢？</span><span class="sxs-lookup"><span data-stu-id="65bf3-113">So, how do we store this and where?</span></span>

<span data-ttu-id="65bf3-114">許多您可能會有經驗的 SQL 資料庫，或至少具有概念[關聯式的資料模型化](https://en.wikipedia.org/wiki/Relational_model)，而且您可能想的 toostart 繪製結果類似這樣：</span><span class="sxs-lookup"><span data-stu-id="65bf3-114">Many of you might have experience on SQL databases or at least have notion of [relational modeling of data](https://en.wikipedia.org/wiki/Relational_model) and you might be tempted toostart drawing something like this:</span></span>

![說明相對關聯式模型的圖表](./media/social-media-apps/social-media-apps-sql.png) 

<span data-ttu-id="65bf3-116">這麼正規且漂亮的資料結構...</span><span class="sxs-lookup"><span data-stu-id="65bf3-116">A perfectly normalized and pretty data structure…</span></span> <span data-ttu-id="65bf3-117">卻無法調整。</span><span class="sxs-lookup"><span data-stu-id="65bf3-117">that doesn't scale.</span></span> 

<span data-ttu-id="65bf3-118">別誤會，我已經使用 SQL 資料庫很久了，知道它的確很棒，但它也跟其他的模式、做法和軟體平台一樣，不可能是萬能的。</span><span class="sxs-lookup"><span data-stu-id="65bf3-118">Don’t get me wrong, I’ve worked with SQL databases all my life, they are great, but like every pattern, practice and software platform, it’s not perfect for every scenario.</span></span>

<span data-ttu-id="65bf3-119">為什麼無法在此案例中 SQL hello 最佳選擇？</span><span class="sxs-lookup"><span data-stu-id="65bf3-119">Why isn't SQL hello best choice in this scenario?</span></span> <span data-ttu-id="65bf3-120">讓我們看看 hello 結構單一 post 要求，如果我想 tooshow 張貼在網站或應用程式時，我就得 toodo 的查詢...</span><span class="sxs-lookup"><span data-stu-id="65bf3-120">Let’s look at hello structure of a single post, if I wanted tooshow that post in a website or application, I’d have toodo a query with…</span></span> <span data-ttu-id="65bf3-121">8 資料表聯結 （！） 只是 tooshow 一個單一 post，現在，圖片的文章，以動態方式載入，並會出現在囉 」 畫面和您的資料流可能會看到我的重點。</span><span class="sxs-lookup"><span data-stu-id="65bf3-121">8 table joins (!) just tooshow one single post, now, picture a stream of posts that dynamically load and appear on hello screen and you might see where I am going.</span></span>

<span data-ttu-id="65bf3-122">我們可以當然，使用 humongous 的 SQL 執行個體具有足夠電源 toosolve 千分位的查詢與這些許多聯結 tooserve 我們的內容，但真正，我們更簡單的解決方案時要為什麼會存在嗎？</span><span class="sxs-lookup"><span data-stu-id="65bf3-122">We could, of course, use a humongous SQL instance with enough power toosolve thousands of queries with these many joins tooserve our content, but truly, why would we when a simpler solution exists?</span></span>

## <a name="hello-nosql-road"></a><span data-ttu-id="65bf3-123">hello NoSQL 路段圖</span><span class="sxs-lookup"><span data-stu-id="65bf3-123">hello NoSQL road</span></span>
<span data-ttu-id="65bf3-124">本文將引導您到 Azure 的 NoSQL 資料庫社交平台的資料模型化[Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/)符合成本效益的方式，同時利用其他 Azure Cosmos DB 功能，例如 hello [Gremlin Graph API](../cosmos-db/graph-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="65bf3-124">This article will guide you into modeling your social platform's data with Azure's NoSQL database [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) in a cost-effective way while leveraging other Azure Cosmos DB features like hello  [Gremlin Graph API](../cosmos-db/graph-introduction.md).</span></span> <span data-ttu-id="65bf3-125">如果使用 [NoSQL](https://en.wikipedia.org/wiki/NoSQL) 方法，將資料以 JSON 格式儲存，並套用[反正規化](https://en.wikipedia.org/wiki/Denormalization)，即可將之前複雜的貼文轉換成單一[文件](https://en.wikipedia.org/wiki/Document-oriented_database)：</span><span class="sxs-lookup"><span data-stu-id="65bf3-125">Using a [NoSQL](https://en.wikipedia.org/wiki/NoSQL) approach, storing data in JSON format and applying [denormalization](https://en.wikipedia.org/wiki/Denormalization), our previously complicated post can be transformed into a single [Document](https://en.wikipedia.org/wiki/Document-oriented_database):</span></span>


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

<span data-ttu-id="65bf3-126">如此一來，即可利用單一查詢而不需要任何聯結，即可取得該文件。</span><span class="sxs-lookup"><span data-stu-id="65bf3-126">And it can be obtained with a single query, and with no joins.</span></span> <span data-ttu-id="65bf3-127">這是更為簡單又直接，而且，budget-wise，需要較少的資源 tooachieve 更好的結果。</span><span class="sxs-lookup"><span data-stu-id="65bf3-127">This is much more simple and straightforward, and, budget-wise, it requires fewer resources tooachieve a better result.</span></span>

<span data-ttu-id="65bf3-128">Azure Cosmos DB 可確保所有 hello 屬性都索引之使用其自動檢索，可能甚至會[自訂](indexing-policies.md)。</span><span class="sxs-lookup"><span data-stu-id="65bf3-128">Azure Cosmos DB makes sure that all hello properties are indexed with its automatic indexing, which can even be [customized](indexing-policies.md).</span></span> <span data-ttu-id="65bf3-129">無結構描述的方法可讓我們以不同儲存文件和動態結構，或許明天我們想要處理的分類或 Cosmos DB 與其相關聯的雜湊標記清單文章 toohave hello 新文件以 hello hello 加入具有不需額外的屬性由我們所需的工作。</span><span class="sxs-lookup"><span data-stu-id="65bf3-129">hello schema-free approach lets us store Documents with different and dynamic structures, maybe tomorrow we want posts toohave a list of categories or hashtags associated with them, Cosmos DB will handle hello new Documents with hello added attributes with no extra work required by us.</span></span>

<span data-ttu-id="65bf3-130">某篇文章的回應可視為含父屬性的其他貼文 (如此可簡化物件的對應)。</span><span class="sxs-lookup"><span data-stu-id="65bf3-130">Comments on a post can be treated as just other posts with a parent property (this simplifies our object mapping).</span></span> 

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

<span data-ttu-id="65bf3-131">接著，即可將所有社交互動儲存為個別物件上的計數器︰</span><span class="sxs-lookup"><span data-stu-id="65bf3-131">And all social interactions can be stored on a separate object as counters:</span></span>

    {
        "id":"dfe3-thf5-232s-dse4",
        "post":"ew12-res2-234e-544f",
        "comments":2,
        "likes":10,
        "points":200
    }

<span data-ttu-id="65bf3-132">若要建立摘要，只需建立文件，包含具有特定相關性順序的貼文識別碼清單即可︰</span><span class="sxs-lookup"><span data-stu-id="65bf3-132">Creating feeds is just a matter of creating documents that can hold a list of post ids with a given relevance order:</span></span>

    [
        {"relevance":9, "post":"ew12-res2-234e-544f"},
        {"relevance":8, "post":"fer7-mnb6-fgh9-2344"},
        {"relevance":7, "post":"w34r-qeg6-ref6-8565"}
    ]

<span data-ttu-id="65bf3-133">我們可能會根據建立日期排序的文章與有 「 最新 」 資料流、 文章詳細類似在 hello 與過去 24 小時的那些的 「 熱 」 資料流、 我們甚至無法實作根據邏輯實行項目與興趣，例如每個使用者自訂資料流和它仍會是一份 文章。</span><span class="sxs-lookup"><span data-stu-id="65bf3-133">We could have a “latest” stream with posts ordered by creation date, a “hottest” stream with those posts with more likes in hello last 24 hours, we could even implement a custom stream for each user based on logic like followers and interests, and it would still be a list of posts.</span></span> <span data-ttu-id="65bf3-134">它是如何 toobuild 這些列出，但是 hello 讀取效能維持 unhindered。</span><span class="sxs-lookup"><span data-stu-id="65bf3-134">It’s a matter of how toobuild these lists, but hello reading performance remains unhindered.</span></span> <span data-ttu-id="65bf3-135">一旦我們取得其中一個清單，我們就會發出單一查詢 tooCosmos DB 使用 hello[運算子中](documentdb-sql-query.md#WhereClause)tooobtain 頁面的文章，一次。</span><span class="sxs-lookup"><span data-stu-id="65bf3-135">Once we acquire one of these lists, we issue a single query tooCosmos DB using hello [IN operator](documentdb-sql-query.md#WhereClause) tooobtain pages of posts at a time.</span></span>

<span data-ttu-id="65bf3-136">無法使用建立餵送資料流的 hello [Azure 應用程式服務的](https://azure.microsoft.com/services/app-service/)背景處理序： [Webjobs](../app-service-web/web-sites-create-web-jobs.md)。</span><span class="sxs-lookup"><span data-stu-id="65bf3-136">hello feed streams could be built using [Azure App Services’](https://azure.microsoft.com/services/app-service/) background processes: [Webjobs](../app-service-web/web-sites-create-web-jobs.md).</span></span> <span data-ttu-id="65bf3-137">背景處理 post 建立之後，可藉由使用[Azure 儲存體](https://azure.microsoft.com/services/storage/)[佇列](../storage/queues/storage-dotnet-how-to-use-queues.md)和 Webjob 觸發使用 hello [Azure Webjobs SDK](../app-service-web/websites-dotnet-webjobs-sdk.md)，它會實作hello 張貼根據自己的自訂邏輯的資料流內的傳播。</span><span class="sxs-lookup"><span data-stu-id="65bf3-137">Once a post is created, background processing can be triggered by using [Azure Storage](https://azure.microsoft.com/services/storage/) [Queues](../storage/queues/storage-dotnet-how-to-use-queues.md) and Webjobs triggered using hello [Azure Webjobs SDK](../app-service-web/websites-dotnet-webjobs-sdk.md), implementing hello post propagation inside streams based on our own custom logic.</span></span> 

<span data-ttu-id="65bf3-138">延後的方式，使用這個相同的技巧 toocreate 最終一致性的環境可以處理點和透過 post 類似。</span><span class="sxs-lookup"><span data-stu-id="65bf3-138">Points and likes over a post can be processed in a deferred manner using this same technique toocreate an eventually consistent environment.</span></span>

<span data-ttu-id="65bf3-139">至於粉絲，則需要有更多的技巧來處理。</span><span class="sxs-lookup"><span data-stu-id="65bf3-139">Followers are trickier.</span></span> <span data-ttu-id="65bf3-140">Cosmos DB 具有最大的文件大小限制，並讀取/寫入大型文件可能會影響應用程式的 hello 延展性。</span><span class="sxs-lookup"><span data-stu-id="65bf3-140">Cosmos DB has a maximum document size limit, and reading/writing large documents can impact hello scalability of your application.</span></span> <span data-ttu-id="65bf3-141">因此，您可能會考慮使用下列結構，以文件形式儲存粉絲：</span><span class="sxs-lookup"><span data-stu-id="65bf3-141">So you may think about storing followers as a document with this structure:</span></span>

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

<span data-ttu-id="65bf3-142">這可能適用於具有少數數以千計的使用者實行項目，但如果某些名人聯結我們排列次序，這個方法會導致 tooa 大型文件大小，而且可能最後會叫用的 hello 文件大小限制。</span><span class="sxs-lookup"><span data-stu-id="65bf3-142">This might work for a user with a few thousands followers, but if some celebrity joins our ranks, this approach will lead tooa large document size, and might eventually hit hello document size cap.</span></span>

<span data-ttu-id="65bf3-143">toosolve，我們可以使用混合的方法。</span><span class="sxs-lookup"><span data-stu-id="65bf3-143">toosolve this, we can use a mixed approach.</span></span> <span data-ttu-id="65bf3-144">Hello 使用者統計資料的文件的一部分，我們可以將儲存 hello 實行項目數目：</span><span class="sxs-lookup"><span data-stu-id="65bf3-144">As part of hello User Statistics document we can store hello number of followers:</span></span>

    {
        "id":"234d-sd23-rrf2-552d",
        "user": "dse4-qwe2-ert4-aad2",
        "followers":55230,
        "totalPosts":452,
        "totalPoints":11342
    }

<span data-ttu-id="65bf3-145">而且可以使用 Azure Cosmos DB 儲存 hello 的實行項目實際的圖形[Gremlin Graph API](../cosmos-db/graph-introduction.md)，toocreate[頂點](http://mathworld.wolfram.com/GraphVertex.html)每位使用者和[邊緣](http://mathworld.wolfram.com/GraphEdge.html)來維護 hello"A 如下所示 B"關聯性。</span><span class="sxs-lookup"><span data-stu-id="65bf3-145">And hello actual graph of followers can be stored using Azure Cosmos DB [Gremlin Graph API](../cosmos-db/graph-introduction.md), toocreate [vertexes](http://mathworld.wolfram.com/GraphVertex.html) for each user and [edges](http://mathworld.wolfram.com/GraphEdge.html) that maintain hello "A-follows-B" relationships.</span></span> <span data-ttu-id="65bf3-146">hello Graph API 讓您取得特定使用者的 hello 實行項目不僅建立更複雜的查詢 tooeven 建議使用者在一般。</span><span class="sxs-lookup"><span data-stu-id="65bf3-146">hello Graph API let's you not only obtain hello followers of a certain user but create more complex queries tooeven suggest people in common.</span></span> <span data-ttu-id="65bf3-147">如果我們加入 toohello 圖形 hello 內容類別讓人喜歡或享受，我們可以開始 weaving 體驗，包括智慧內容探索，建議內容中，我們遵循所或尋找與其我們可能會有許多相同的人員。</span><span class="sxs-lookup"><span data-stu-id="65bf3-147">If we add toohello graph hello Content Categories that people like or enjoy, we can start weaving experiences that include smart content discovery, suggesting content that those we follow like, or finding people with whom we might have much in common.</span></span>

<span data-ttu-id="65bf3-148">hello 使用者統計資料的文件仍然可以使用的 toocreate 卡 hello UI 或快速分析 預覽中。</span><span class="sxs-lookup"><span data-stu-id="65bf3-148">hello User Statistics document can still be used toocreate cards in hello UI or quick profile previews.</span></span>

## <a name="hello-ladder-pattern-and-data-duplication"></a><span data-ttu-id="65bf3-149">hello"階梯 」 模式以及資料重複</span><span class="sxs-lookup"><span data-stu-id="65bf3-149">hello “Ladder” pattern and data duplication</span></span>
<span data-ttu-id="65bf3-150">您可能已經注意到參考 post hello JSON 文件中，沒有使用者的多個項目。</span><span class="sxs-lookup"><span data-stu-id="65bf3-150">As you might have noticed in hello JSON document that references a post, there are multiple occurrences of a user.</span></span> <span data-ttu-id="65bf3-151">此外，您就已經猜到正確的這表示，代表使用者，提供此反正規化，hello 資訊可能會出現在多個位置。</span><span class="sxs-lookup"><span data-stu-id="65bf3-151">And you’d have guessed right, this means that hello information that represents a user, given this denormalization, might be present in more than one place.</span></span>

<span data-ttu-id="65bf3-152">在更快的查詢的順序 tooallow，我們會造成資料重複。</span><span class="sxs-lookup"><span data-stu-id="65bf3-152">In order tooallow for faster queries, we incur data duplication.</span></span> <span data-ttu-id="65bf3-153">hello 問題具有此副作用是若某些動作，使用者的資料變更時，我們需要 toofind hello 的所有活動他曾未且更新全部。</span><span class="sxs-lookup"><span data-stu-id="65bf3-153">hello problem with this side-effect is that if by some action, a user’s data changes, we need toofind all hello activities he ever did and update them all.</span></span> <span data-ttu-id="65bf3-154">聽起來不太實際，對吧？</span><span class="sxs-lookup"><span data-stu-id="65bf3-154">Doesn’t sound very practical, right?</span></span>

<span data-ttu-id="65bf3-155">我們會持續 toosolve 它藉由識別 hello 我們顯示在應用程式中的每個活動的使用者索引鍵屬性。</span><span class="sxs-lookup"><span data-stu-id="65bf3-155">We are going toosolve it by identifying hello Key attributes of a user that we show in our application for each activity.</span></span> <span data-ttu-id="65bf3-156">如果我們以視覺化方式顯示我們的應用程式中的文章，並顯示只要 hello 建立者的名稱與圖片，為什麼 hello 使用者資料的所有儲存 hello"createdby"屬性中？</span><span class="sxs-lookup"><span data-stu-id="65bf3-156">If we visually show a post in our application and show just hello creator’s name and picture, why store all of hello user’s data in hello “createdBy” attribute?</span></span> <span data-ttu-id="65bf3-157">如果每個註解我們只會顯示 hello 使用者的圖片，我們不需要其資訊 hello 其餘部分。</span><span class="sxs-lookup"><span data-stu-id="65bf3-157">If for each comment we just show hello user’s picture, we don’t really need hello rest of his information.</span></span> <span data-ttu-id="65bf3-158">這是其中呼叫 hello"階梯模式 」 的項目派上用場。</span><span class="sxs-lookup"><span data-stu-id="65bf3-158">That’s where something I call hello “Ladder pattern” comes into play.</span></span>

<span data-ttu-id="65bf3-159">讓我們以使用者資訊當作範例︰</span><span class="sxs-lookup"><span data-stu-id="65bf3-159">Let’s take user information as an example:</span></span>

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

<span data-ttu-id="65bf3-160">查看此資訊可以快速偵測出哪些是重要資訊而哪些不是，以建立出一道「階梯」：</span><span class="sxs-lookup"><span data-stu-id="65bf3-160">By looking at this information, we can quickly detect which is critical information and which isn’t, thus creating a “Ladder”:</span></span>

![階梯模式的圖表](./media/social-media-apps/social-media-apps-ladder.png)

<span data-ttu-id="65bf3-162">hello 最小步驟稱為 UserChunk、 hello 可識別使用者資訊的最小的片段，它用於資料重複。</span><span class="sxs-lookup"><span data-stu-id="65bf3-162">hello smallest step is called a UserChunk, hello minimal piece of information that identifies a user and it’s used for data duplication.</span></span> <span data-ttu-id="65bf3-163">透過減少重複的 hello 資料 tooonly hello 資訊我們將 [顯示] hello 大小，我們會減少大量更新 hello 可能性。</span><span class="sxs-lookup"><span data-stu-id="65bf3-163">By reducing hello size of hello duplicated data tooonly hello information we will “show”, we reduce hello possibility of massive updates.</span></span>

<span data-ttu-id="65bf3-164">hello 中間步驟呼叫 hello 使用者，它是最存取及最重要，hello hello Cosmos DB 上大部分的效能相依查詢將使用的完整資料。</span><span class="sxs-lookup"><span data-stu-id="65bf3-164">hello middle step is called hello user, it’s hello full data that will be used on most performance-dependent queries on Cosmos DB, hello most accessed and critical.</span></span> <span data-ttu-id="65bf3-165">其中包括 hello UserChunk 所代表的資訊。</span><span class="sxs-lookup"><span data-stu-id="65bf3-165">It includes hello information represented by a UserChunk.</span></span>

<span data-ttu-id="65bf3-166">hello 最大為 hello 擴充使用者。</span><span class="sxs-lookup"><span data-stu-id="65bf3-166">hello largest is hello Extended User.</span></span> <span data-ttu-id="65bf3-167">它包含所有 hello 重大的使用者資訊加上不會真正快速需要 toobe 讀取其他資料，或它的使用方式 （例如 hello 登入程序） 最終。</span><span class="sxs-lookup"><span data-stu-id="65bf3-167">It includes all hello critical user information plus other data that doesn’t really require toobe read quickly or it’s usage is eventual (like hello login process).</span></span> <span data-ttu-id="65bf3-168">這些資料可以儲存在 Cosmos DB 外部、Azure SQL Database 中或 Azure 儲存體資料表中。</span><span class="sxs-lookup"><span data-stu-id="65bf3-168">This data can be stored outside of Cosmos DB, in Azure SQL Database or Azure Storage Tables.</span></span>

<span data-ttu-id="65bf3-169">為什麼我們會分割 hello 使用者，甚至將這項資訊存放在不同的地方嗎？</span><span class="sxs-lookup"><span data-stu-id="65bf3-169">Why would we split hello user and even store this information in different places?</span></span> <span data-ttu-id="65bf3-170">因為從效能觀點來看，hello 更大的 hello 文件 hello costlier hello 查詢。</span><span class="sxs-lookup"><span data-stu-id="65bf3-170">Because from a performance point of view, hello bigger hello documents, hello costlier hello queries.</span></span> <span data-ttu-id="65bf3-171">將文件輕薄 hello 與右資訊 toodo 所有您效能相關查詢以取得您的社交網路和存放區 hello 最終的案例，例如，完整設定檔的編輯，登入其他額外的資訊，甚至流量分析和大型的資料採礦資料開發案。</span><span class="sxs-lookup"><span data-stu-id="65bf3-171">Keep documents slim, with hello right information toodo all your performance-dependent queries for your social network, and store hello other extra information for eventual scenarios like, full profile edits, logins, even data mining for usage analytics and Big Data initiatives.</span></span> <span data-ttu-id="65bf3-172">我們不在意 hello 資料收集的資料採礦時速度較慢，因為它正在 Azure SQL Database 上執行，我們不要有有關透過我們的使用者有快速而輕型的體驗。</span><span class="sxs-lookup"><span data-stu-id="65bf3-172">We really don’t care if hello data gathering for data mining is slower because it’s running on Azure SQL Database, we do have concern though that our users have a fast and slim experience.</span></span> <span data-ttu-id="65bf3-173">儲存在 Cosmos DB 中的使用者，應類似如下︰</span><span class="sxs-lookup"><span data-stu-id="65bf3-173">A user, stored on Cosmos DB, would look like this:</span></span>

    {
        "id":"dse4-qwe2-ert4-aad2",
        "name":"John",
        "surname":"Doe",
        "username":"johndoe"
        "email":"john@doe.com",
        "twitterHandle":"@john"
    }

<span data-ttu-id="65bf3-174">而貼文應該看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="65bf3-174">And a Post would look like:</span></span>

    {
        "id":"1234-asd3-54ts-199a",
        "title":"Awesome post!",
        "date":"2016-01-02",
        "createdBy":{
            "id":"dse4-qwe2-ert4-aad2",
            "username":"johndoe"
        }
    }

<span data-ttu-id="65bf3-175">當編輯就會發生影響其中一個 hello 區塊的 hello 屬性，它是簡單 toofind hello 影響文件使用點 toohello 編製索引屬性的查詢 (選取 * FROM 文章 p WHERE p.createdBy.id = ="edited_user_id")，然後更新hello 區塊。</span><span class="sxs-lookup"><span data-stu-id="65bf3-175">And when an edit arises where one of hello attributes of hello chunk is affected, it’s easy toofind hello affected documents by using queries that point toohello indexed attributes (SELECT * FROM posts p WHERE p.createdBy.id == “edited_user_id”) and then updating hello chunks.</span></span>

## <a name="hello-search-box"></a><span data-ttu-id="65bf3-176">hello 搜尋方塊</span><span class="sxs-lookup"><span data-stu-id="65bf3-176">hello search box</span></span>
<span data-ttu-id="65bf3-177">一般來說，使用者都能很幸運地產生許多內容。</span><span class="sxs-lookup"><span data-stu-id="65bf3-177">Users will generate, luckily, a lot of content.</span></span> <span data-ttu-id="65bf3-178">和我們應該能夠 tooprovide hello 能力 toosearch 並找到內容可能無法直接在其內容的資料流，可能因為我們未遵循 hello 建立者，或可能只有我們只想 toofind 我們所做的 6 個月前的舊 post。</span><span class="sxs-lookup"><span data-stu-id="65bf3-178">And we should be able tooprovide hello ability toosearch and find content that might not be directly in their content streams, maybe because we don’t follow hello creators, or maybe we are just trying toofind that old post we did 6 months ago.</span></span>

<span data-ttu-id="65bf3-179">幸好，因為我們使用 Azure Cosmos DB，我們可以輕鬆地實作搜尋引擎使用[Azure 搜尋](https://azure.microsoft.com/services/search/)需要幾分鐘的時間，而不需要輸入一行程式碼 （而不是很明顯地，hello 搜尋程序和 UI）。</span><span class="sxs-lookup"><span data-stu-id="65bf3-179">Thankfully, and because we are using Azure Cosmos DB, we can easily implement a search engine using [Azure Search](https://azure.microsoft.com/services/search/) in a couple of minutes and without typing a single line of code (other than obviously, hello search process and UI).</span></span>

<span data-ttu-id="65bf3-180">為什麼可以這麼輕鬆？</span><span class="sxs-lookup"><span data-stu-id="65bf3-180">Why is this so easy?</span></span>

<span data-ttu-id="65bf3-181">Azure 搜尋實作它們的呼叫[索引子](https://msdn.microsoft.com/library/azure/dn946891.aspx)、 背景處理該攔截程序，在您的資料儲存機制中，自動新增、 更新或移除 hello 索引中的物件。</span><span class="sxs-lookup"><span data-stu-id="65bf3-181">Azure Search implements what they call [Indexers](https://msdn.microsoft.com/library/azure/dn946891.aspx), background processes that hook in your data repositories and automagically add, update or remove your objects in hello indexes.</span></span> <span data-ttu-id="65bf3-182">它們支援 [Azure SQL Database 索引子](https://blogs.msdn.microsoft.com/kaevans/2015/03/06/indexing-azure-sql-database-with-azure-search/)、[Azure Blob 索引子](../search/search-howto-indexing-azure-blob-storage.md)，甚至也支援 [Azure Cosmos DB 索引子](../search/search-howto-index-documentdb.md)。</span><span class="sxs-lookup"><span data-stu-id="65bf3-182">They support an [Azure SQL Database indexers](https://blogs.msdn.microsoft.com/kaevans/2015/03/06/indexing-azure-sql-database-with-azure-search/), [Azure Blobs indexers](../search/search-howto-indexing-azure-blob-storage.md) and thankfully, [Azure Cosmos DB indexers](../search/search-howto-index-documentdb.md).</span></span> <span data-ttu-id="65bf3-183">hello 轉換 Cosmos DB tooAzure 搜尋中的資訊是那樣，這兩個存放區中的資訊 JSON 格式，我們只需要太[建立我們索引](../search/search-create-index-portal.md)，並將對應從我們的文件的屬性我們要編製索引，且它，在幾分鐘的時間 （取決於 hello 我們的資料大小），所有的內容將會使用 toobe 搜尋時，雲端基礎結構中 hello 最佳搜尋做為服務解決方案。</span><span class="sxs-lookup"><span data-stu-id="65bf3-183">hello transition of information from Cosmos DB tooAzure Search is straightforward, as both store information in JSON format, we just need too[create our Index](../search/search-create-index-portal.md) and map which attributes from our Documents we want indexed and that’s it, in a matter of minutes (depends on hello size of our data), all our content will be available toobe searched upon, by hello best Search-as-a-Service solution in cloud infrastructure.</span></span> 

<span data-ttu-id="65bf3-184">如需 Azure 搜尋的詳細資訊，請造訪 hello [（英文) 的指南 tooSearch](https://blogs.msdn.microsoft.com/mvpawardprogram/2016/02/02/a-hitchhikers-guide-to-search/)。</span><span class="sxs-lookup"><span data-stu-id="65bf3-184">For more information about Azure Search, you can visit hello [Hitchhiker’s Guide tooSearch](https://blogs.msdn.microsoft.com/mvpawardprogram/2016/02/02/a-hitchhikers-guide-to-search/).</span></span>

## <a name="hello-underlying-knowledge"></a><span data-ttu-id="65bf3-185">hello 基礎知識</span><span class="sxs-lookup"><span data-stu-id="65bf3-185">hello underlying knowledge</span></span>
<span data-ttu-id="65bf3-186">儲存這些所有內容之後，隨著內容每天不斷增長，我們可能會考慮到該怎麼運用這些使用者的資訊的串流？</span><span class="sxs-lookup"><span data-stu-id="65bf3-186">After storing all this content that grows and grows every day, we might find ourselves thinking: What can I do with all this stream of information from my users?</span></span>

<span data-ttu-id="65bf3-187">hello 回應相當直接： 使其 toowork 並從中了解。</span><span class="sxs-lookup"><span data-stu-id="65bf3-187">hello answer is straightforward: Put it toowork and learn from it.</span></span>

<span data-ttu-id="65bf3-188">但是，我們可以學習到什麼呢？</span><span class="sxs-lookup"><span data-stu-id="65bf3-188">But, what can we learn?</span></span> <span data-ttu-id="65bf3-189">簡單的範例包括[情緒分析](https://en.wikipedia.org/wiki/Sentiment_analysis)，根據使用者的喜好設定的建議，或甚至自動化內容仲裁者，以確保所有 hello 發佈我們的社交網路的內容是安全的 hello 內容系列。</span><span class="sxs-lookup"><span data-stu-id="65bf3-189">A few easy examples include [sentiment analysis](https://en.wikipedia.org/wiki/Sentiment_analysis), content recommendations based on a user’s preferences or even an automated content moderator that ensures that all hello content published by our social network is safe for hello family.</span></span>

<span data-ttu-id="65bf3-190">現在，我會收到您攔截，就可能會考慮您需要在數學科學 tooextract 某些博士這些模式和資訊從簡單的資料庫和檔案，但會發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="65bf3-190">Now that I got you hooked, you’ll probably think you need some PhD in math science tooextract these patterns and information out of simple databases and files, but you’d be wrong.</span></span>

<span data-ttu-id="65bf3-191">[Azure Machine Learning](https://azure.microsoft.com/services/machine-learning/)，屬於 hello [Cortana 智慧套件](https://www.microsoft.com/en/server-cloud/cortana-analytics-suite/overview.aspx)，為 hello 完全受管理的雲端服務，可讓您建立簡單的拖放介面中使用的演算法的工作流程，您自己的演算法的程式碼在[R](https://en.wikipedia.org/wiki/R_\(programming_language\))或使用某些 hello 已經內建並就緒 toouse 應用程式開發介面，例如：[文字分析](https://gallery.cortanaanalytics.com/MachineLearningAPI/Text-Analytics-2)，[內容仲裁者](https://www.microsoft.com/moderator)或[建議](https://gallery.cortanaanalytics.com/MachineLearningAPI/Recommendations-2).</span><span class="sxs-lookup"><span data-stu-id="65bf3-191">[Azure Machine Learning](https://azure.microsoft.com/services/machine-learning/), part of hello [Cortana Intelligence Suite](https://www.microsoft.com/en/server-cloud/cortana-analytics-suite/overview.aspx), is hello a fully managed cloud service that lets you create workflows using algorithms in a simple drag-and-drop interface, code your own algorithms in [R](https://en.wikipedia.org/wiki/R_\(programming_language\)) or use some of hello already-built and ready toouse APIs such as: [Text Analytics](https://gallery.cortanaanalytics.com/MachineLearningAPI/Text-Analytics-2),  [Content Moderator](https://www.microsoft.com/moderator) or [Recommendations](https://gallery.cortanaanalytics.com/MachineLearningAPI/Recommendations-2).</span></span>

<span data-ttu-id="65bf3-192">tooachieve 任何這些機器學習案例中，我們可以使用[Azure 資料湖](https://azure.microsoft.com/services/data-lake-store/)tooingest hello 不同來源的資訊，並使用[U-SQL](https://azure.microsoft.com/documentation/videos/data-lake-u-sql-query-execution/) tooprocess hello 資訊並產生輸出Azure Machine learning 可同時處理。</span><span class="sxs-lookup"><span data-stu-id="65bf3-192">tooachieve any of these Machine Learning scenarios, we can use [Azure Data Lake](https://azure.microsoft.com/services/data-lake-store/) tooingest hello information from different sources, and use [U-SQL](https://azure.microsoft.com/documentation/videos/data-lake-u-sql-query-execution/) tooprocess hello information and generate an output that can be processed by Azure Machine Learning.</span></span>

<span data-ttu-id="65bf3-193">另一個可用的選項是 toouse [Microsoft 認知服務](https://www.microsoft.com/cognitive-services)tooanalyze 我們內容; 不只可以我們了解它們的使用者提供更好的 (透過分析這些寫入與[文字分析 API](https://www.microsoft.com/cognitive-services/en-us/text-analytics-api))，但我們無法偵測不想要或成熟的內容，並據此採取行動以[電腦願景 API](https://www.microsoft.com/cognitive-services/en-us/computer-vision-api)。</span><span class="sxs-lookup"><span data-stu-id="65bf3-193">Another available option is toouse [Microsoft Cognitive Services](https://www.microsoft.com/cognitive-services) tooanalyze our users content; not only can we understand them better (through analyzing what they write with [Text Analytics API](https://www.microsoft.com/cognitive-services/en-us/text-analytics-api)) , but we could also detect unwanted or mature content and act accordingly with [Computer Vision API](https://www.microsoft.com/cognitive-services/en-us/computer-vision-api).</span></span> <span data-ttu-id="65bf3-194">認知的服務包括大量不需要任何種類的機器學習知識 toouse 的全新的解決方案。</span><span class="sxs-lookup"><span data-stu-id="65bf3-194">Cognitive Services include a lot of out-of-the-box solutions that don't require any kind of Machine Learning knowledge toouse.</span></span>

## <a name="a-planet-scale-social-experience"></a><span data-ttu-id="65bf3-195">全球規模的社交體驗</span><span class="sxs-lookup"><span data-stu-id="65bf3-195">A planet-scale social experience</span></span>
<span data-ttu-id="65bf3-196">最後，我還有一項重要的主題必須和各位分享，那就是「延展性」。</span><span class="sxs-lookup"><span data-stu-id="65bf3-196">There is a last, but not least, important topic I must address: **scalability**.</span></span> <span data-ttu-id="65bf3-197">設計相當重要的每個元件可以延展其本身，可能是因為我們需要更多資料 tooprocess 架構時，或因為我們想要 toohave 更大的地理涵蓋範圍 （或兩者 ！）。</span><span class="sxs-lookup"><span data-stu-id="65bf3-197">When designing an architecture it's crucial that each component can scale on its own, either because we need tooprocess more data or because we want toohave a bigger geographical coverage (or both!).</span></span> <span data-ttu-id="65bf3-198">幸好，透過 Cosmos DB，我們便能輕鬆完成如此複雜的工作。</span><span class="sxs-lookup"><span data-stu-id="65bf3-198">Thankfully, achieving such a complex task is a **turnkey experience** with Cosmos DB.</span></span>

<span data-ttu-id="65bf3-199">Cosmos DB 支援[動態磁碟分割](https://azure.microsoft.com/blog/10-things-to-know-about-documentdb-partitioned-collections/)--蜪鎏藉由自動建立根據資料分割指定**資料分割索引鍵**（定義為文件中的 hello 屬性的其中之一）。</span><span class="sxs-lookup"><span data-stu-id="65bf3-199">Cosmos DB supports [dynamic partitioning](https://azure.microsoft.com/blog/10-things-to-know-about-documentdb-partitioned-collections/) out-of-the-box by automatically creating partitions based on a given **partition key** (defined as one of hello attributes in your documents).</span></span> <span data-ttu-id="65bf3-200">定義 hello 正確資料分割索引鍵必須以在設計階段和保留中注意 hello[最佳做法](../cosmos-db/partition-data.md#designing-for-partitioning)可用; 在社交體驗的 hello 情況下，資料分割策略必須對齊查詢 （讀取 hello 方法hello 內相同的資料分割都需要這樣做） 和寫入 （由多個資料分割上的寫入避免 「 作用點 」）。</span><span class="sxs-lookup"><span data-stu-id="65bf3-200">Defining hello correct partition key must be done at design time and keeping in mind hello [best practices](../cosmos-db/partition-data.md#designing-for-partitioning) available; in hello case of a social experience, your partitioning strategy must be aligned with hello way you query (reads within hello same partition are desirable) and write (avoid "hot spots" by spreading writes on multiple partitions).</span></span> <span data-ttu-id="65bf3-201">某些選項： 暫時索引鍵為基礎 （日/月/週），依據內容的類別、 依地理區域，由使用者; 的磁碟分割所有它其實取決於如何查詢 hello 資料並顯示在您的社交體驗。</span><span class="sxs-lookup"><span data-stu-id="65bf3-201">Some options are: partitions based on a temporal key (day/month/week), by content category, by geographical region, by user; it all really depends on how you will query hello data and show it in your social experience.</span></span> 

<span data-ttu-id="65bf3-202">其中一個值得一提的是有趣的一點是 Cosmos DB 將會執行您的查詢 (包括[彙總](https://azure.microsoft.com/blog/planet-scale-aggregates-with-azure-documentdb/)) 到您的資料分割以透明的方式，您不需要 tooadd 任何邏輯隨著您的資料。</span><span class="sxs-lookup"><span data-stu-id="65bf3-202">One interesting point worth mentioning is that Cosmos DB will run your queries (including [aggregates](https://azure.microsoft.com/blog/planet-scale-aggregates-with-azure-documentdb/)) across all your partitions transparently, you don't need tooadd any logic as your data grows.</span></span>

<span data-ttu-id="65bf3-203">流量最終會隨時間增長，而您的資源消耗 (以 [RU](request-units.md) (要求單位) 為單位) 也會增加。</span><span class="sxs-lookup"><span data-stu-id="65bf3-203">With time, you will eventually grow in traffic and your resource consumption (measured in [RUs](request-units.md), or Request Units) will increase.</span></span> <span data-ttu-id="65bf3-204">您將讀寫更頻繁地為您 userbase 成長，同時會開始建立及讀取更多的內容。hello 能力**調整您的輸送量**而言非常重要。</span><span class="sxs-lookup"><span data-stu-id="65bf3-204">You will read and write more frequently as your userbase grows and they will start creating and reading more content; hello ability of **scaling your throughput** is vital.</span></span> <span data-ttu-id="65bf3-205">增加我們 RUs 是非常簡單，我們可以按幾下 hello Azure 入口網站或藉由執行[發出命令 hello 應用程式開發介面透過](https://docs.microsoft.com/rest/api/documentdb/replace-an-offer)。</span><span class="sxs-lookup"><span data-stu-id="65bf3-205">Increasing our RUs is very easy, we can do it with a few clicks on hello Azure Portal or by [issuing commands through hello API](https://docs.microsoft.com/rest/api/documentdb/replace-an-offer).</span></span>

![相應增加及定義分割區索引鍵](./media/social-media-apps/social-media-apps-scaling.png)

<span data-ttu-id="65bf3-207">如果很幸運地，有來自其他地區、國家或洲大陸的使用者注意到您的平台，並開始使用它，這還真是個好消息！</span><span class="sxs-lookup"><span data-stu-id="65bf3-207">What happens if things keep getting better and users from another region, country or continent, notice your platform and start using it, what a great surprise!</span></span>

<span data-ttu-id="65bf3-208">但稍候...您很快就了解他們的經驗與您的平台不是最佳選項。它們不在目前為止您操作區域 hello 延遲是可怕，，和您顯然不希望他們 tooquit。</span><span class="sxs-lookup"><span data-stu-id="65bf3-208">But wait... you soon realize their experience with your platform is not optimal; they are so far away from your operational region that hello latency is terrible, and you obviously don't want them tooquit.</span></span> <span data-ttu-id="65bf3-209">要是有方法能輕鬆「觸達全球使用者」就好了。當然有！</span><span class="sxs-lookup"><span data-stu-id="65bf3-209">If only there was an easy way of **extending your global reach**... but there is!</span></span>

<span data-ttu-id="65bf3-210">Cosmos DB 可讓您[您的資料會進行全域複寫](../cosmos-db/tutorial-global-distribution-documentdb.md)以透明的方式有幾個動作，並自動選取 從 hello 可用地區之間和您[用戶端程式碼](../cosmos-db/tutorial-global-distribution-documentdb.md)。</span><span class="sxs-lookup"><span data-stu-id="65bf3-210">Cosmos DB lets you [replicate your data globally](../cosmos-db/tutorial-global-distribution-documentdb.md) and transparently with a couple of clicks and automatically select among hello available regions from your [client code](../cosmos-db/tutorial-global-distribution-documentdb.md).</span></span> <span data-ttu-id="65bf3-211">這也表示您可以擁有[多個容錯移轉區域](regional-failover.md)。</span><span class="sxs-lookup"><span data-stu-id="65bf3-211">This also means that you can have [multiple failover regions](regional-failover.md).</span></span> 

<span data-ttu-id="65bf3-212">當您進行全域複寫您的資料時，您會需要 toomake 確定您的用戶端可以馬上使用該。</span><span class="sxs-lookup"><span data-stu-id="65bf3-212">When you replicate your data globally, you need toomake sure that your clients can take advantage of it.</span></span> <span data-ttu-id="65bf3-213">如果您使用的 web 前端或從行動用戶端存取 Api，您可以部署[Azure Traffic Manager](https://azure.microsoft.com/services/traffic-manager/)並複製到您的 Azure 應用程式服務上的所有預期的 hello 區域，使用[效能設定](../app-service-web/web-sites-traffic-manager.md)toosupport 擴充的全域涵蓋範圍。</span><span class="sxs-lookup"><span data-stu-id="65bf3-213">If you are using a web frontend or accesing APIs from mobile clients, you can deploy [Azure Traffic Manager](https://azure.microsoft.com/services/traffic-manager/) and clone your Azure App Service on all hello desired regions, using a [Performance configuration](../app-service-web/web-sites-traffic-manager.md) toosupport your extended global coverage.</span></span> <span data-ttu-id="65bf3-214">當您的用戶端存取您的前端或應用程式開發介面時，就會路由的 toohello 最接近的應用程式服務，接著，將連接 toohello 本機 Cosmos DB 複本。</span><span class="sxs-lookup"><span data-stu-id="65bf3-214">When your clients access your frontend or APIs, they will be routed toohello closest App Service, which in turn, will connect toohello local Cosmos DB replica.</span></span>

![正在將通用的涵蓋範圍 tooyour 社交平台](./media/social-media-apps/social-media-apps-global-replicate.png)

## <a name="conclusion"></a><span data-ttu-id="65bf3-216">結論</span><span class="sxs-lookup"><span data-stu-id="65bf3-216">Conclusion</span></span>
<span data-ttu-id="65bf3-217">這篇文章會嘗試的 tooshed 某些淺 hello 替代方案的低成本服務與社交網路完全建立在 Azure 上，並提供絕佳的結果令人滿意的 hello 使用稱為 「 階梯"的多層的儲存體解決方案和資料發佈至。</span><span class="sxs-lookup"><span data-stu-id="65bf3-217">This article tries tooshed some light into hello alternatives of creating social networks completely on Azure with low-cost services and providing great results by encouraging hello use of a multi-layered storage solution and data distribution called “Ladder”.</span></span>

![Azure 服務之間社交網路互動的圖表](./media/social-media-apps/social-media-apps-azure-solution.png)

<span data-ttu-id="65bf3-219">hello 真為沒有靈丹這種情況下，它有 hello 的很好的服務可讓我們 toobuild 絕佳體驗的 hello 組合所建立的綜合設定： hello 速度和自由 Azure Cosmos DB tooprovide 絕佳的社交應用程式，hello 智慧背後的第一級的搜尋解決方案喜歡 Azure 搜尋時，Azure 應用程式服務 toohost hello 彈性不但功能強大的背景處理程序適用於多種語言的應用程式] 及 [hello 可展開的 Azure 儲存體和 Azure SQL Database。儲存大量的資料和 hello 分析電源的 Azure Machine Learning toocreate 知識和智慧，可提供意見反應 tooour 處理程序，並幫助我們傳遞 hello 右內容 toohello 適當的使用者。</span><span class="sxs-lookup"><span data-stu-id="65bf3-219">hello truth is that there is no silver bullet for this kind of scenarios, it’s hello synergy created by hello combination of great services that allow us toobuild great experiences: hello speed and freedom of Azure Cosmos DB tooprovide a great social application, hello intelligence behind a first-class search solution like Azure Search, hello flexibility of Azure App Services toohost not even language-agnostic applications but powerful background processes and hello expandable Azure Storage and Azure SQL Database for storing massive amounts of data and hello analytic power of Azure Machine Learning toocreate knowledge and intelligence that can provide feedback tooour processes and help us deliver hello right content toohello right users.</span></span>

## <a name="next-steps"></a><span data-ttu-id="65bf3-220">後續步驟</span><span class="sxs-lookup"><span data-stu-id="65bf3-220">Next steps</span></span>
<span data-ttu-id="65bf3-221">toolearn 有關 Cosmos DB 的使用案例的詳細資訊請參閱[常見 Cosmos DB 的使用案例](use-cases.md)。</span><span class="sxs-lookup"><span data-stu-id="65bf3-221">toolearn more about use cases for Cosmos DB, see [Common Cosmos DB use cases](use-cases.md).</span></span>
