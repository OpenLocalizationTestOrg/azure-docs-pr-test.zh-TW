---
title: "aaaModeling 文件資料的 NoSQL 資料庫 |Microsoft 文件"
description: "了解如何將 NoSQL 資料庫的資料模型化"
keywords: "模型化資料"
services: cosmos-db
author: arramac
manager: jhubbard
editor: mimig1
documentationcenter: 
ms.assetid: 69521eb9-590b-403c-9b36-98253a4c88b5
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/29/2016
ms.author: arramac
ms.openlocfilehash: 2e388c833f204287896dfa8e6f79c88073731b6b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="modeling-document-data-for-nosql-databases"></a><span data-ttu-id="2894a-104">將 NoSQL 資料庫的文件資料模型化</span><span class="sxs-lookup"><span data-stu-id="2894a-104">Modeling document data for NoSQL databases</span></span>
<span data-ttu-id="2894a-105">無結構描述的資料庫，例如 Azure Cosmos DB，讓您輕鬆 super tooembrace 變更 tooyour 資料模型仍應該花費一些時間考慮您的資料。</span><span class="sxs-lookup"><span data-stu-id="2894a-105">While schema-free databases, like Azure Cosmos DB, make it super easy tooembrace changes tooyour data model you should still spend some time thinking about your data.</span></span> 

<span data-ttu-id="2894a-106">為資料要如何儲存 toobe？</span><span class="sxs-lookup"><span data-stu-id="2894a-106">How is data going toobe stored?</span></span> <span data-ttu-id="2894a-107">如何為應用程式進行 tooretrieve 和查詢資料？</span><span class="sxs-lookup"><span data-stu-id="2894a-107">How is your application going tooretrieve and query data?</span></span> <span data-ttu-id="2894a-108">您的應用程式是大量讀取或大量寫入？</span><span class="sxs-lookup"><span data-stu-id="2894a-108">Is your application read heavy, or write heavy?</span></span> 

<span data-ttu-id="2894a-109">閱讀這篇文章之後, 您將無法 tooanswer hello 下列問題：</span><span class="sxs-lookup"><span data-stu-id="2894a-109">After reading this article, you will be able tooanswer hello following questions:</span></span>

* <span data-ttu-id="2894a-110">應如何考慮文件資料庫中的文件？</span><span class="sxs-lookup"><span data-stu-id="2894a-110">How should I think about a document in a document database?</span></span>
* <span data-ttu-id="2894a-111">什麼是資料模型化，以及為什麼應該關心？</span><span class="sxs-lookup"><span data-stu-id="2894a-111">What is data modeling and why should I care?</span></span> 
* <span data-ttu-id="2894a-112">文件資料庫不同 tooa 關聯式資料庫中的模型化資料的方式？</span><span class="sxs-lookup"><span data-stu-id="2894a-112">How is modeling data in a document database different tooa relational database?</span></span>
* <span data-ttu-id="2894a-113">如何表達非關聯式資料庫中的資料關聯性？</span><span class="sxs-lookup"><span data-stu-id="2894a-113">How do I express data relationships in a non-relational database?</span></span>
* <span data-ttu-id="2894a-114">當內嵌資料，以及當連結 toodata？</span><span class="sxs-lookup"><span data-stu-id="2894a-114">When do I embed data and when do I link toodata?</span></span>

## <a name="embedding-data"></a><span data-ttu-id="2894a-115">內嵌資料</span><span class="sxs-lookup"><span data-stu-id="2894a-115">Embedding data</span></span>
<span data-ttu-id="2894a-116">當您啟動文件存放區，例如 Azure Cosmos DB 中的資料模型化時再試一次 tootreat 做為實體**各自獨立的文件**在 JSON 中表示。</span><span class="sxs-lookup"><span data-stu-id="2894a-116">When you start modeling data in a document store, such as Azure Cosmos DB, try tootreat your entities as **self-contained documents** represented in JSON.</span></span>

<span data-ttu-id="2894a-117">在我們更進一步深入探討之前，讓我們往回幾個步驟，看看我們在關聯式資料庫中如何建立某個項目的模型，這是許多人已熟悉的主題。</span><span class="sxs-lookup"><span data-stu-id="2894a-117">Before we dive in too much further, let us take a few steps back and have a look at how we might model something in a relational database, a subject many of us are already familiar with.</span></span> <span data-ttu-id="2894a-118">hello 下列範例顯示如何個人可能會儲存在關聯式資料庫。</span><span class="sxs-lookup"><span data-stu-id="2894a-118">hello following example shows how a person might be stored in a relational database.</span></span> 

![關聯式資料庫模型](./media/documentdb-modeling-data/relational-data-model.png)

<span data-ttu-id="2894a-120">使用關聯式資料庫，我們已針對年 toonormalize 教正規化，正規化。</span><span class="sxs-lookup"><span data-stu-id="2894a-120">When working with relational databases, we've been taught for years toonormalize, normalize, normalize.</span></span>

<span data-ttu-id="2894a-121">正規化資料通常包括建立實體，例如個人，，以及細分 toodiscrete 資料片段中。</span><span class="sxs-lookup"><span data-stu-id="2894a-121">Normalizing your data typically involves taking an entity, such as a person, and breaking it down in toodiscrete pieces of data.</span></span> <span data-ttu-id="2894a-122">在 hello 上述範例中，個人可擁有多個連絡人的詳細記錄，以及多個位址記錄。</span><span class="sxs-lookup"><span data-stu-id="2894a-122">In hello example above, a person can have multiple contact detail records as well as multiple address records.</span></span> <span data-ttu-id="2894a-123">我們甚至透過進一步擷取一般欄位 (像是類別)，更進一步細分連絡詳細資料。</span><span class="sxs-lookup"><span data-stu-id="2894a-123">We even go one step further and break down contact details by further extracting common fields like a type.</span></span> <span data-ttu-id="2894a-124">地址也是如此，此處的每個記錄具有類型 (像是 [住家] 或 [商務])</span><span class="sxs-lookup"><span data-stu-id="2894a-124">Same for address, each record here has a type like *Home* or *Business*</span></span> 

<span data-ttu-id="2894a-125">當正規化資料太引導內部部署的 hello**避免儲存重複的資料**上每個記錄和而不是參考 toodata。</span><span class="sxs-lookup"><span data-stu-id="2894a-125">hello guiding premise when normalizing data is too**avoid storing redundant data** on each record and rather refer toodata.</span></span> <span data-ttu-id="2894a-126">在此範例中，tooread 具有所有的連絡人詳細資料和地址的人員，您需要 toouse 聯結 tooeffectively 彙總您的資料在執行階段。</span><span class="sxs-lookup"><span data-stu-id="2894a-126">In this example, tooread a person, with all their contact details and addresses, you need toouse JOINS tooeffectively aggregate your data at run time.</span></span>

    SELECT p.FirstName, p.LastName, a.City, cd.Detail
    FROM Person p
    JOIN ContactDetail cd ON cd.PersonId = p.Id
    JOIN ContactDetailType on cdt ON cdt.Id = cd.TypeId
    JOIN Address a ON a.PersonId = p.Id

<span data-ttu-id="2894a-127">更新單一人員與其連絡詳細資料和地址需要跨許多個別資料表的寫入作業。</span><span class="sxs-lookup"><span data-stu-id="2894a-127">Updating a single person with their contact details and addresses requires write operations across many individual tables.</span></span> 

<span data-ttu-id="2894a-128">現在讓我們看看我們如何將模型 hello 相同資料做為文件資料庫中的獨立實體。</span><span class="sxs-lookup"><span data-stu-id="2894a-128">Now let's take a look at how we would model hello same data as a self-contained entity in a document database.</span></span>

    {
        "id": "1",
        "firstName": "Thomas",
        "lastName": "Andersen",
        "addresses": [
            {            
                "line1": "100 Some Street",
                "line2": "Unit 1",
                "city": "Seattle",
                "state": "WA",
                "zip": 98012
            }
        ],
        "contactDetails": [
            {"email: "thomas@andersen.com"},
            {"phone": "+1 555 555-5555", "extension": 5555}
        ] 
    }

<span data-ttu-id="2894a-129">使用 hello 上述方法我們現在有**反正規化**hello 個人記錄其中我們**內嵌**所有 hello toothis 人員，如他們的連絡人詳細資料和地址，單一 tooa 中的相關資訊JSON 文件。</span><span class="sxs-lookup"><span data-stu-id="2894a-129">Using hello approach above we have now **denormalized** hello person record where we **embedded** all hello information relating toothis person, such as their contact details and addresses, in tooa single JSON document.</span></span>
<span data-ttu-id="2894a-130">此外，因為我們要在不限制 tooa 固定的結構描述我們有 hello 彈性 toodo 等完全具有不同的圖形的連絡人詳細資料。</span><span class="sxs-lookup"><span data-stu-id="2894a-130">In addition, because we're not confined tooa fixed schema we have hello flexibility toodo things like having contact details of different shapes entirely.</span></span> 

<span data-ttu-id="2894a-131">從 hello 資料庫擷取完整的人員記錄現在是單一讀取作業對單一集合與單一文件。</span><span class="sxs-lookup"><span data-stu-id="2894a-131">Retrieving a complete person record from hello database is now a single read operation against a single collection and for a single document.</span></span> <span data-ttu-id="2894a-132">更新連絡詳細資料和地址等個人記錄，也是針對單一文件的單一寫入作業。</span><span class="sxs-lookup"><span data-stu-id="2894a-132">Updating a person record, with their contact details and addresses, is also a single write operation against a single document.</span></span>

<span data-ttu-id="2894a-133">反正規化的資料，您的應用程式可能需要 tooissue 減少查詢與更新 toocomplete 常見的作業。</span><span class="sxs-lookup"><span data-stu-id="2894a-133">By denormalizing data, your application may need tooissue fewer queries and updates toocomplete common operations.</span></span> 

### <a name="when-tooembed"></a><span data-ttu-id="2894a-134">當 tooembed</span><span class="sxs-lookup"><span data-stu-id="2894a-134">When tooembed</span></span>
<span data-ttu-id="2894a-135">一般而言，使用內嵌的資料模型的時機為：</span><span class="sxs-lookup"><span data-stu-id="2894a-135">In general, use embedded data models when:</span></span>

* <span data-ttu-id="2894a-136">實體之間有 **包含** 關聯性。</span><span class="sxs-lookup"><span data-stu-id="2894a-136">There are **contains** relationships between entities.</span></span>
* <span data-ttu-id="2894a-137">實體之間有 **一對一些** 關聯性。</span><span class="sxs-lookup"><span data-stu-id="2894a-137">There are **one-to-few** relationships between entities.</span></span>
* <span data-ttu-id="2894a-138">內嵌的資料 **不常變更**。</span><span class="sxs-lookup"><span data-stu-id="2894a-138">There is embedded data that **changes infrequently**.</span></span>
* <span data-ttu-id="2894a-139">內嵌的資料不會 **無限的成長**。</span><span class="sxs-lookup"><span data-stu-id="2894a-139">There is embedded data won't grow **without bound**.</span></span>
* <span data-ttu-id="2894a-140">沒有內嵌的資料是**整數**toodata 文件中的。</span><span class="sxs-lookup"><span data-stu-id="2894a-140">There is embedded data that is **integral** toodata in a document.</span></span>

> [!NOTE]
> <span data-ttu-id="2894a-141">通常反正規化的資料模型可提供較佳的 **讀取** 效能。</span><span class="sxs-lookup"><span data-stu-id="2894a-141">Typically denormalized data models provide better **read** performance.</span></span>
> 
> 

### <a name="when-not-tooembed"></a><span data-ttu-id="2894a-142">當不 tooembed</span><span class="sxs-lookup"><span data-stu-id="2894a-142">When not tooembed</span></span>
<span data-ttu-id="2894a-143">雖然 hello 的經驗法則文件資料庫中的所有項目是 toodenormalize 並 tooa 單一文件中內嵌的所有資料，這可能會導致 toosome 情況下應該避免的。</span><span class="sxs-lookup"><span data-stu-id="2894a-143">While hello rule of thumb in a document database is toodenormalize everything and embed all data in tooa single document, this can lead toosome situations that should be avoided.</span></span>

<span data-ttu-id="2894a-144">取得此 JSON 程式碼片段。</span><span class="sxs-lookup"><span data-stu-id="2894a-144">Take this JSON snippet.</span></span>

    {
        "id": "1",
        "name": "What's new in hello coolest Cloud",
        "summary": "A blog post by someone real famous",
        "comments": [
            {"id": 1, "author": "anon", "comment": "something useful, I'm sure"},
            {"id": 2, "author": "bob", "comment": "wisdom from hello interwebs"},
            …
            {"id": 100001, "author": "jane", "comment": "and on we go ..."},
            …
            {"id": 1000000001, "author": "angry", "comment": "blah angry blah angry"},
            …
            {"id": ∞ + 1, "author": "bored", "comment": "oh man, will this ever end?"},
        ]
    }

<span data-ttu-id="2894a-145">如果我們要模型化一般的部落格或 CMS 系統，這可能是具有內嵌註解的文章實體的外觀。</span><span class="sxs-lookup"><span data-stu-id="2894a-145">This might be what a post entity with embedded comments would look like if we were modeling a typical blog, or CMS, system.</span></span> <span data-ttu-id="2894a-146">hello 與這個範例的問題是註解陣列是該 hello **unbounded**，這表示沒有任何單一 post 可以有註解 （實際） 限制 toohello 號碼。</span><span class="sxs-lookup"><span data-stu-id="2894a-146">hello problem with this example is that hello comments array is **unbounded**, meaning that there is no (practical) limit toohello number of comments any single post can have.</span></span> <span data-ttu-id="2894a-147">當 hello hello 文件大小可能會大幅成長，這會成為問題。</span><span class="sxs-lookup"><span data-stu-id="2894a-147">This will become a problem as hello size of hello document could grow significantly.</span></span>

<span data-ttu-id="2894a-148">因為 hello hello 大小文件會隨著 hello 能力 tootransmit hello 資料 hello 網路，以及讀取和更新的 hello 文件，在小數位數，將會受到影響。</span><span class="sxs-lookup"><span data-stu-id="2894a-148">As hello size of hello document grows hello ability tootransmit hello data over hello wire as well as reading and updating hello document, at scale, will be impacted.</span></span>

<span data-ttu-id="2894a-149">在此情況下，它會遵循模型更好的 tooconsider hello。</span><span class="sxs-lookup"><span data-stu-id="2894a-149">In this case it would be better tooconsider hello following model.</span></span>

    Post document:
    {
        "id": "1",
        "name": "What's new in hello coolest Cloud",
        "summary": "A blog post by someone real famous",
        "recentComments": [
            {"id": 1, "author": "anon", "comment": "something useful, I'm sure"},
            {"id": 2, "author": "bob", "comment": "wisdom from hello interwebs"},
            {"id": 3, "author": "jane", "comment": "....."}
        ]
    }

    Comment documents:
    {
        "postId": "1"
        "comments": [
            {"id": 4, "author": "anon", "comment": "more goodness"},
            {"id": 5, "author": "bob", "comment": "tails from hello field"},
            ...
            {"id": 99, "author": "angry", "comment": "blah angry blah angry"}
        ]
    },
    {
        "postId": "1"
        "comments": [
            {"id": 100, "author": "anon", "comment": "yet more"},
            ...
            {"id": 199, "author": "bored", "comment": "will this ever end?"}
        ]
    }

<span data-ttu-id="2894a-150">這個模型經 hello 三個最新的註解內嵌在 hello 張貼本身，也就是具有固定的繫結的陣列時間。</span><span class="sxs-lookup"><span data-stu-id="2894a-150">This model has hello three most recent comments embedded on hello post itself, which is an array with a fixed bound this time.</span></span> <span data-ttu-id="2894a-151">hello 其他註解分組 toobatches 100 的註解中，並儲存在個別的文件。</span><span class="sxs-lookup"><span data-stu-id="2894a-151">hello other comments are grouped in toobatches of 100 comments and stored in separate documents.</span></span> <span data-ttu-id="2894a-152">hello hello 批次大小被選為 100，因為我們的虛構應用程式允許 hello 使用者 tooload 100 註解一次。</span><span class="sxs-lookup"><span data-stu-id="2894a-152">hello size of hello batch was chosen as 100 because our fictitious application allows hello user tooload 100 comments at a time.</span></span>  

<span data-ttu-id="2894a-153">其中內嵌的資料不是最好的另一種情況是 hello 內嵌時，資料通常使用跨文件，而經常變更。</span><span class="sxs-lookup"><span data-stu-id="2894a-153">Another case where embedding data is not a good idea is when hello embedded data is used often across documents and will change frequently.</span></span> 

<span data-ttu-id="2894a-154">取得此 JSON 程式碼片段。</span><span class="sxs-lookup"><span data-stu-id="2894a-154">Take this JSON snippet.</span></span>

    {
        "id": "1",
        "firstName": "Thomas",
        "lastName": "Andersen",
        "holdings": [
            {
                "numberHeld": 100,
                "stock": { "symbol": "zaza", "open": 1, "high": 2, "low": 0.5 }
            },
            {
                "numberHeld": 50,
                "stock": { "symbol": "xcxc", "open": 89, "high": 93.24, "low": 88.87 }
            }
        ]
    }

<span data-ttu-id="2894a-155">這可以代表個人的股票組合。</span><span class="sxs-lookup"><span data-stu-id="2894a-155">This could represent a person's stock portfolio.</span></span> <span data-ttu-id="2894a-156">我們已選擇 tooembed hello 股票資訊 tooeach portfolio 文件中。</span><span class="sxs-lookup"><span data-stu-id="2894a-156">We have chosen tooembed hello stock information in tooeach portfolio document.</span></span> <span data-ttu-id="2894a-157">在環境中相關的資料經常變更股市交易應用程式，例如內嵌經常變更的資料即將 toomean，您會經常更新每個 portfolio 文件每次會在黑市內建。</span><span class="sxs-lookup"><span data-stu-id="2894a-157">In an environment where related data is changing frequently, like a stock trading application, embedding data that changes frequently is going toomean that you are constantly updating each portfolio document every time a stock is traded.</span></span>

<span data-ttu-id="2894a-158">股票 *zaza* 可能在單一日交易數百次，而上千名使用者的組合上可能有 *zaza*。</span><span class="sxs-lookup"><span data-stu-id="2894a-158">Stock *zaza* may be traded many hundreds of times in a single day and thousands of users could have *zaza* on their portfolio.</span></span> <span data-ttu-id="2894a-159">資料模型，類似上述的 hello 我們必須 tooupdate 數千個 portfolio 文件開頭 tooa 系統將不會調整很好的每一天多次。</span><span class="sxs-lookup"><span data-stu-id="2894a-159">With a data model like hello above we would have tooupdate many thousands of portfolio documents many times every day leading tooa system that won't scale very well.</span></span> 

## <span data-ttu-id="2894a-160"><a id="Refer"></a>參考資料</span><span class="sxs-lookup"><span data-stu-id="2894a-160"><a id="Refer"></a>Referencing data</span></span>
<span data-ttu-id="2894a-161">因此，內嵌資料於許多情況下可適用，但很明顯有時反正規化資料將會造成更多問題，使得適得其反。</span><span class="sxs-lookup"><span data-stu-id="2894a-161">So, embedding data works nicely for many cases but it is clear that there are scenarios when denormalizing your data will cause more problems than it is worth.</span></span> <span data-ttu-id="2894a-162">那我們現在該怎麼辦？</span><span class="sxs-lookup"><span data-stu-id="2894a-162">So what do we do now?</span></span> 

<span data-ttu-id="2894a-163">關聯式資料庫未 hello 唯一的地方，您可以在其中建立實體之間的關聯性。</span><span class="sxs-lookup"><span data-stu-id="2894a-163">Relational databases are not hello only place where you can create relationships between entities.</span></span> <span data-ttu-id="2894a-164">文件資料庫中您可以讓一個實際與相關 toodata 其他文件中的文件中的資訊。</span><span class="sxs-lookup"><span data-stu-id="2894a-164">In a document database you can have information in one document that actually relates toodata in other documents.</span></span> <span data-ttu-id="2894a-165">現在，我不支援針對甚至一分鐘我們建置系統，會在 Azure Cosmos DB 中，更適合的 tooa 關聯式資料庫或其他任何文件資料庫，但簡單關聯性是正常的而且可以是非常有用。</span><span class="sxs-lookup"><span data-stu-id="2894a-165">Now, I am not advocating for even one minute that we build systems that would be better suited tooa relational database in Azure Cosmos DB, or any other document database, but simple relationships are fine and can be very useful.</span></span> 

<span data-ttu-id="2894a-166">Hello 下列 JSON 中我們選擇稍早但這次我們 toohello 股票而不是內嵌的 hello 待辦項目從內建 portfolio toouse hello 的範例。</span><span class="sxs-lookup"><span data-stu-id="2894a-166">In hello JSON below we chose toouse hello example of a stock portfolio from earlier but this time we refer toohello stock item on hello portfolio instead of embedding it.</span></span> <span data-ttu-id="2894a-167">如此一來，hello 內建項目經常變更整 hello 天 hello 只有文件需要更新 toobe 時 hello 單一內建的文件。</span><span class="sxs-lookup"><span data-stu-id="2894a-167">This way, when hello stock item changes frequently throughout hello day hello only document that needs toobe updated is hello single stock document.</span></span> 

    Person document:
    {
        "id": "1",
        "firstName": "Thomas",
        "lastName": "Andersen",
        "holdings": [
            { "numberHeld":  100, "stockId": 1},
            { "numberHeld":  50, "stockId": 2}
        ]
    }

    Stock documents:
    {
        "id": "1",
        "symbol": "zaza",
        "open": 1,
        "high": 2,
        "low": 0.5,
        "vol": 11970000,
        "mkt-cap": 42000000,
        "pe": 5.89
    },
    {
        "id": "2",
        "symbol": "xcxc",
        "open": 89,
        "high": 93.24,
        "low": 88.87,
        "vol": 2970200,
        "mkt-cap": 1005000,
        "pe": 75.82
    }


<span data-ttu-id="2894a-168">立即缺點 toothis 方法雖然是您的應用程式是否需要的 tooshow 顯示個人的公事包; 時，會保留每種股票資訊在此情況下您需要 toomake 多個往返 toohello 資料庫 tooload hello 資訊的每個內建的文件。</span><span class="sxs-lookup"><span data-stu-id="2894a-168">An immediate downside toothis approach though is if your application is required tooshow information about each stock that is held when displaying a person's portfolio; in this case you would need toomake multiple trips toohello database tooload hello information for each stock document.</span></span> <span data-ttu-id="2894a-169">這裡我們讓決策 tooimprove hello 的效率 hello 天當中經常發生，但接著洩露 hello 讀取 hello 這個特定的系統效能可能較不會影響的作業上的寫入作業。</span><span class="sxs-lookup"><span data-stu-id="2894a-169">Here we've made a decision tooimprove hello efficiency of write operations, which happen frequently throughout hello day, but in turn compromised on hello read operations that potentially have less impact on hello performance of this particular system.</span></span>

> [!NOTE]
> <span data-ttu-id="2894a-170">正規化的資料模型**可能需要多個往返**toohello 伺服器。</span><span class="sxs-lookup"><span data-stu-id="2894a-170">Normalized data models **can require more round trips** toohello server.</span></span>
> 
> 

### <a name="what-about-foreign-keys"></a><span data-ttu-id="2894a-171">外部索引鍵呢？</span><span class="sxs-lookup"><span data-stu-id="2894a-171">What about foreign keys?</span></span>
<span data-ttu-id="2894a-172">目前沒有條件約束的概念，因為外部索引鍵或其他任何間的文件關聯性必須在文件中是有效的 「 弱式連結 」 與 hello 資料庫本身將不會驗證。</span><span class="sxs-lookup"><span data-stu-id="2894a-172">Because there is currently no concept of a constraint, foreign-key or otherwise, any inter-document relationships that you have in documents are effectively "weak links" and will not be verified by hello database itself.</span></span> <span data-ttu-id="2894a-173">如果您想 hello 參考文件資料的 tooensure tooactually 存在，則您需要 toodo 這在您的應用程式，或透過 hello 使用伺服器端的觸發程序或預存程序，在 Azure Cosmos DB 上。</span><span class="sxs-lookup"><span data-stu-id="2894a-173">If you want tooensure that hello data a document is referring tooactually exists, then you need toodo this in your application, or through hello use of server-side triggers or stored procedures on Azure Cosmos DB.</span></span>

### <a name="when-tooreference"></a><span data-ttu-id="2894a-174">當 tooreference</span><span class="sxs-lookup"><span data-stu-id="2894a-174">When tooreference</span></span>
<span data-ttu-id="2894a-175">一般而言，使用正規化資料模型的時機為：</span><span class="sxs-lookup"><span data-stu-id="2894a-175">In general, use normalized data models when:</span></span>

* <span data-ttu-id="2894a-176">代表 **一對多** 關聯性。</span><span class="sxs-lookup"><span data-stu-id="2894a-176">Representing **one-to-many** relationships.</span></span>
* <span data-ttu-id="2894a-177">代表 **多對多** 關聯性。</span><span class="sxs-lookup"><span data-stu-id="2894a-177">Representing **many-to-many** relationships.</span></span>
* <span data-ttu-id="2894a-178">相關資料 **經常變更**。</span><span class="sxs-lookup"><span data-stu-id="2894a-178">Related data **changes frequently**.</span></span>
* <span data-ttu-id="2894a-179">參考資料可能是 **unbounded**。</span><span class="sxs-lookup"><span data-stu-id="2894a-179">Referenced data could be **unbounded**.</span></span>

> [!NOTE]
> <span data-ttu-id="2894a-180">通常正規化可提供較佳的 **寫入** 效能。</span><span class="sxs-lookup"><span data-stu-id="2894a-180">Typically normalizing provides better **write** performance.</span></span>
> 
> 

### <a name="where-do-i-put-hello-relationship"></a><span data-ttu-id="2894a-181">其中將放 hello 關聯性？</span><span class="sxs-lookup"><span data-stu-id="2894a-181">Where do I put hello relationship?</span></span>
<span data-ttu-id="2894a-182">hello 成長 hello 關聯性可協助您判斷哪一個文件 toostore hello 參考中。</span><span class="sxs-lookup"><span data-stu-id="2894a-182">hello growth of hello relationship will help determine in which document toostore hello reference.</span></span>

<span data-ttu-id="2894a-183">如果看一下 hello JSON 下之模型的發行者和活頁簿。</span><span class="sxs-lookup"><span data-stu-id="2894a-183">If we look at hello JSON below that models publishers and books.</span></span>

    Publisher document:
    {
        "id": "mspress",
        "name": "Microsoft Press",
        "books": [ 1, 2, 3, ..., 100, ..., 1000]
    }

    Book documents:
    {"id": "1", "name": "Azure Cosmos DB 101" }
    {"id": "2", "name": "Azure Cosmos DB for RDBMS Users" }
    {"id": "3", "name": "Taking over hello world one JSON doc at a time" }
    ...
    {"id": "100", "name": "Learn about Azure Cosmos DB" }
    ...
    {"id": "1000", "name": "Deep Dive in tooAzure Cosmos DB" }

<span data-ttu-id="2894a-184">如果每個發行者的 hello 書籍的 hello 數目很小具有有限的成長，然後儲存 hello 發行者文件內的 hello 書籍參考可能很有用。</span><span class="sxs-lookup"><span data-stu-id="2894a-184">If hello number of hello books per publisher is small with limited growth, then storing hello book reference inside hello publisher document may be useful.</span></span> <span data-ttu-id="2894a-185">不過，如果每個發行者的書籍的 hello 數目未繫結，然後此資料模型會導致 toomutable，不斷增加的陣列，如 hello 範例發行者文件上方所示。</span><span class="sxs-lookup"><span data-stu-id="2894a-185">However, if hello number of books per publisher is unbounded, then this data model would lead toomutable, growing arrays, as in hello example publisher document above.</span></span> 

<span data-ttu-id="2894a-186">切換項目位元會結果仍代表 hello 但現在相同的資料模型中避免這些大型的可變動集合。</span><span class="sxs-lookup"><span data-stu-id="2894a-186">Switching things around a bit would result in a model that still represents hello same data but now avoids these large mutable collections.</span></span>

    Publisher document: 
    {
        "id": "mspress",
        "name": "Microsoft Press"
    }

    Book documents: 
    {"id": "1","name": "Azure Cosmos DB 101", "pub-id": "mspress"}
    {"id": "2","name": "Azure Cosmos DB for RDBMS Users", "pub-id": "mspress"}
    {"id": "3","name": "Taking over hello world one JSON doc at a time"}
    ...
    {"id": "100","name": "Learn about Azure Cosmos DB", "pub-id": "mspress"}
    ...
    {"id": "1000","name": "Deep Dive in tooAzure Cosmos DB", "pub-id": "mspress"}

<span data-ttu-id="2894a-187">在上述範例中的 hello，我們已卸除 hello hello 發行者文件上的未繫結的集合。</span><span class="sxs-lookup"><span data-stu-id="2894a-187">In hello above example, we have dropped hello unbounded collection on hello publisher document.</span></span> <span data-ttu-id="2894a-188">而是我們只需要每個活頁簿的文件的參考 toohello 發行者端。</span><span class="sxs-lookup"><span data-stu-id="2894a-188">Instead we just have a a reference toohello publisher on each book document.</span></span>

### <a name="how-do-i-model-manymany-relationships"></a><span data-ttu-id="2894a-189">如何建立多對多關聯性的模型？</span><span class="sxs-lookup"><span data-stu-id="2894a-189">How do I model many:many relationships?</span></span>
<span data-ttu-id="2894a-190">在關聯式資料庫 *多對多* 關聯性中，通常是與聯結資料表模型化，其只是將記錄從其他資料表聯結在一起。</span><span class="sxs-lookup"><span data-stu-id="2894a-190">In a relational database *many:many* relationships are often modeled with join tables, which just join records from other tables together.</span></span> 

![聯結資料表](./media/documentdb-modeling-data/join-table.png)

<span data-ttu-id="2894a-192">您可能會想的 tooreplicate hello 同一件事使用文件，並產生資料模型，看起來類似 toohello 下列。</span><span class="sxs-lookup"><span data-stu-id="2894a-192">You might be tempted tooreplicate hello same thing using documents and produce a data model that looks similar toohello following.</span></span>

    Author documents: 
    {"id": "a1", "name": "Thomas Andersen" }
    {"id": "a2", "name": "William Wakefield" }

    Book documents:
    {"id": "b1", "name": "Azure Cosmos DB 101" }
    {"id": "b2", "name": "Azure Cosmos DB for RDBMS Users" }
    {"id": "b3", "name": "Taking over hello world one JSON doc at a time" }
    {"id": "b4", "name": "Learn about Azure Cosmos DB" }
    {"id": "b5", "name": "Deep Dive in tooAzure Cosmos DB" }

    Joining documents: 
    {"authorId": "a1", "bookId": "b1" }
    {"authorId": "a2", "bookId": "b1" }
    {"authorId": "a1", "bookId": "b2" }
    {"authorId": "a1", "bookId": "b3" }

<span data-ttu-id="2894a-193">這應該可行。</span><span class="sxs-lookup"><span data-stu-id="2894a-193">This would work.</span></span> <span data-ttu-id="2894a-194">但是，載入可能是以其書籍，作者或載入活頁簿的作者，一律需要針對 hello 資料庫至少兩個額外的查詢。</span><span class="sxs-lookup"><span data-stu-id="2894a-194">However, loading either an author with their books, or loading a book with its author, would always require at least two additional queries against hello database.</span></span> <span data-ttu-id="2894a-195">加入文件和另一個查詢 toofetch hello 實際文件所要加入一個查詢 toohello。</span><span class="sxs-lookup"><span data-stu-id="2894a-195">One query toohello joining document and then another query toofetch hello actual document being joined.</span></span> 

<span data-ttu-id="2894a-196">如果此聯結資料表的作用完全是在結合兩組資料在一起，那麼為何不完全捨棄它？</span><span class="sxs-lookup"><span data-stu-id="2894a-196">If all this join table is doing is gluing together two pieces of data, then why not drop it completely?</span></span>
<span data-ttu-id="2894a-197">請考慮下列 hello。</span><span class="sxs-lookup"><span data-stu-id="2894a-197">Consider hello following.</span></span>

    Author documents:
    {"id": "a1", "name": "Thomas Andersen", "books": ["b1, "b2", "b3"]}
    {"id": "a2", "name": "William Wakefield", "books": ["b1", "b4"]}

    Book documents: 
    {"id": "b1", "name": "Azure Cosmos DB 101", "authors": ["a1", "a2"]}
    {"id": "b2", "name": "Azure Cosmos DB for RDBMS Users", "authors": ["a1"]}
    {"id": "b3", "name": "Learn about Azure Cosmos DB", "authors": ["a1"]}
    {"id": "b4", "name": "Deep Dive in tooAzure Cosmos DB", "authors": ["a2"]}

<span data-ttu-id="2894a-198">現在，如果我有一位作者，立即知道哪些書籍，它們還編寫了，並相反如果我有載入的活頁簿文件會知道 hello 識別碼 hello 作者。</span><span class="sxs-lookup"><span data-stu-id="2894a-198">Now, if I had an author, I immediately know which books they have written, and conversely if I had a book document loaded I would know hello ids of hello author(s).</span></span> <span data-ttu-id="2894a-199">這可以節省針對減少伺服器 hello 號碼 hello 聯結資料表的中繼查詢您的應用程式具有 toomake 的往返。</span><span class="sxs-lookup"><span data-stu-id="2894a-199">This saves that intermediary query against hello join table reducing hello number of server round trips your application has toomake.</span></span> 

## <span data-ttu-id="2894a-200"><a id="WrapUp"></a>混合式資料模型</span><span class="sxs-lookup"><span data-stu-id="2894a-200"><a id="WrapUp"></a>Hybrid data models</span></span>
<span data-ttu-id="2894a-201">我們現在已看過內嵌 (或反正規化) 和參考 (或正規化) 資料，如我們所見，各有其優缺點。</span><span class="sxs-lookup"><span data-stu-id="2894a-201">We've now looked embedding (or denormalizing) and referencing (or normalizing) data, each have their upsides and each have compromises as we have seen.</span></span> 

<span data-ttu-id="2894a-202">它不一定有 toobe 是或，不是害怕得的 toomix 事項 up 一點。</span><span class="sxs-lookup"><span data-stu-id="2894a-202">It doesn't always have toobe either or, don't be scared toomix things up a little.</span></span> 

<span data-ttu-id="2894a-203">根據您的應用程式特定的使用模式和工作負載，有時可能無法在混用內嵌和參考的資料有意義無法負責人 toosimpler 應用程式邏輯，以更少的伺服器往返同時仍維持良好的效能層級.</span><span class="sxs-lookup"><span data-stu-id="2894a-203">Based on your application's specific usage patterns and workloads there may be cases where mixing embedded and referenced data makes sense and could lead toosimpler application logic with fewer server round trips while still maintaining a good level of performance.</span></span>

<span data-ttu-id="2894a-204">請考慮下列 JSON hello。</span><span class="sxs-lookup"><span data-stu-id="2894a-204">Consider hello following JSON.</span></span> 

    Author documents: 
    {
        "id": "a1",
        "firstName": "Thomas",
        "lastName": "Andersen",        
        "countOfBooks": 3,
         "books": ["b1", "b2", "b3"],
        "images": [
            {"thumbnail": "http://....png"}
            {"profile": "http://....png"}
            {"large": "http://....png"}
        ]
    },
    {
        "id": "a2",
        "firstName": "William",
        "lastName": "Wakefield",
        "countOfBooks": 1,
        "books": ["b1"],
        "images": [
            {"thumbnail": "http://....png"}
        ]
    }

    Book documents:
    {
        "id": "b1",
        "name": "Azure Cosmos DB 101",
        "authors": [
            {"id": "a1", "name": "Thomas Andersen", "thumbnailUrl": "http://....png"},
            {"id": "a2", "name": "William Wakefield", "thumbnailUrl": "http://....png"}
        ]
    },
    {
        "id": "b2",
        "name": "Azure Cosmos DB for RDBMS Users",
        "authors": [
            {"id": "a1", "name": "Thomas Andersen", "thumbnailUrl": "http://....png"},
        ]
    }

<span data-ttu-id="2894a-205">這裡我們 （大多數） 瀏覽過 hello 內嵌的模型，從其他實體的資料會內嵌在 hello 最上層文件，但參考其他資料。</span><span class="sxs-lookup"><span data-stu-id="2894a-205">Here we've (mostly) followed hello embedded model, where data from other entities are embedded in hello top-level document, but other data is referenced.</span></span> 

<span data-ttu-id="2894a-206">如果您看一下 hello 活頁簿的文件，我們可以看到一些有趣的欄位時，我們會審視 hello 陣列的作者。</span><span class="sxs-lookup"><span data-stu-id="2894a-206">If you look at hello book document, we can see a few interesting fields when we look at hello array of authors.</span></span> <span data-ttu-id="2894a-207">沒有*識別碼*欄位，也就是我們也使用 toorefer 後 tooan 作者文件、 標準化的模型，但接著我們的標準作法 hello 欄位有*名稱*和*thumbnailUrl*.</span><span class="sxs-lookup"><span data-stu-id="2894a-207">There is an *id* field which is hello field we use toorefer back tooan author document, standard practice in a normalized model, but then we also have *name* and *thumbnailUrl*.</span></span> <span data-ttu-id="2894a-208">我們無法了只卡*識別碼*並留下 hello 應用程式 tooget hello 個別作者文件使用 hello 「 連結 」，從它所需的任何其他資訊，但因為我們的應用程式會顯示 hello 作者名稱和縮圖圖片中的顯示每個活頁簿，我們可以儲存每個活頁簿的來回行程 toohello 伺服器清單中所反正規化**某些**hello 作者的資料。</span><span class="sxs-lookup"><span data-stu-id="2894a-208">We could've just stuck with *id* and left hello application tooget any additional information it needed from hello respective author document using hello "link", but because our application displays hello author's name and a thumbnail picture with every book displayed we can save a round trip toohello server per book in a list by denormalizing **some** data from hello author.</span></span>

<span data-ttu-id="2894a-209">當然，如果 hello 作者名稱變更，或他們想 tooupdate 其相片我們可能會 toogo 更新每一本書它們曾發行，但我們的應用程式中，然後再根據 hello 假設作者不常變更其名稱，這是可接受的設計決策。</span><span class="sxs-lookup"><span data-stu-id="2894a-209">Sure, if hello author's name changed or they wanted tooupdate their photo we'd have toogo an update every book they ever published but for our application, based on hello assumption that authors don't change their names very often, this is an acceptable design decision.</span></span>  

<span data-ttu-id="2894a-210">在 hello 範例有**預先計算的彙總**值 toosave 高度耗費資源的讀取作業上處理。</span><span class="sxs-lookup"><span data-stu-id="2894a-210">In hello example there are **pre-calculated aggregates** values toosave expensive processing on a read operation.</span></span> <span data-ttu-id="2894a-211">在 hello 範例中，某些 hello hello 作者文件中內嵌的資料是在執行階段計算的資料。</span><span class="sxs-lookup"><span data-stu-id="2894a-211">In hello example, some of hello data embedded in hello author document is data that is calculated at run-time.</span></span> <span data-ttu-id="2894a-212">每次發行新的活頁簿時，會建立活頁簿的文件**和**hello countOfBooks 欄位設定為 tooa 計算值根據 hello 存在某位特定作者的書籍文件數目。</span><span class="sxs-lookup"><span data-stu-id="2894a-212">Every time a new book is published, a book document is created **and** hello countOfBooks field is set tooa calculated value based on hello number of book documents that exist for a particular author.</span></span> <span data-ttu-id="2894a-213">我們可以在其中負擔中順序 toooptimize 讀取寫入 toodo 計算此最佳化會將很讀取大量的系統中。</span><span class="sxs-lookup"><span data-stu-id="2894a-213">This optimization would be good in read heavy systems where we can afford toodo computations on writes in order toooptimize reads.</span></span>

<span data-ttu-id="2894a-214">hello 的模型包含預先計算的欄位做的原因，因為 Azure Cosmos DB 支援能力 toohave**多重文件交易**。</span><span class="sxs-lookup"><span data-stu-id="2894a-214">hello ability toohave a model with pre-calculated fields is made possible because Azure Cosmos DB supports **multi-document transactions**.</span></span> <span data-ttu-id="2894a-215">許多 NoSQL 存放區無法跨文件中執行的交易，並因此主張的設計決策，例如"一律內嵌的所有項目 」，因為 toothis 限制。</span><span class="sxs-lookup"><span data-stu-id="2894a-215">Many NoSQL stores cannot do transactions across documents and therefore advocate design decisions, such as "always embed everything", due toothis limitation.</span></span> <span data-ttu-id="2894a-216">藉由 Azure Cosmos DB，您可以使用伺服器端觸發程序或預存程序，插入書籍並更新作者，全都在 ACID 交易內完成。</span><span class="sxs-lookup"><span data-stu-id="2894a-216">With Azure Cosmos DB, you can use server-side triggers, or stored procedures, that insert books and update authors all within an ACID transaction.</span></span> <span data-ttu-id="2894a-217">現在您不要**有**tooembed tooone 中的所有文件只 toobe 確定您的資料保持一致。</span><span class="sxs-lookup"><span data-stu-id="2894a-217">Now you don't **have** tooembed everything in tooone document just toobe sure that your data remains consistent.</span></span>

## <span data-ttu-id="2894a-218"><a name="NextSteps"></a>接續步驟</span><span class="sxs-lookup"><span data-stu-id="2894a-218"><a name="NextSteps"></a>Next steps</span></span>
<span data-ttu-id="2894a-219">這篇文章 hello 最大心得是 toounderstand，資料模型中的無結構描述的世界時一樣重要。</span><span class="sxs-lookup"><span data-stu-id="2894a-219">hello biggest takeaways from this article is toounderstand that data modeling in a schema-free world is just as important as ever.</span></span> 

<span data-ttu-id="2894a-220">就像沒有任何單一方法 toorepresent 一段螢幕上的資料，任何單一方法 toomodel 您的資料。</span><span class="sxs-lookup"><span data-stu-id="2894a-220">Just as there is no single way toorepresent a piece of data on a screen, there is no single way toomodel your data.</span></span> <span data-ttu-id="2894a-221">您需要 toounderstand 您的應用程式，它將會產生，耗用，以及處理 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="2894a-221">You need toounderstand your application and how it will produce, consume, and process hello data.</span></span> <span data-ttu-id="2894a-222">然後，藉由套用一些 hello 介紹您的指導方針可以建立模型，以解決 hello 即時應用程式需求的相關設定。</span><span class="sxs-lookup"><span data-stu-id="2894a-222">Then, by applying some of hello guidelines presented here you can set about creating a model that addresses hello immediate needs of your application.</span></span> <span data-ttu-id="2894a-223">當您的應用程式需要 toochange 時，您可以變更而且發展您的資料模型，輕鬆地利用無結構描述的資料庫 tooembrace hello 彈性。</span><span class="sxs-lookup"><span data-stu-id="2894a-223">When your applications need toochange, you can leverage hello flexibility of a schema-free database tooembrace that change and evolve your data model easily.</span></span> 

<span data-ttu-id="2894a-224">深入了解 Azure Cosmos DB toolearn 參考 toohello 服務[文件](https://azure.microsoft.com/documentation/services/cosmos-db/)頁面。</span><span class="sxs-lookup"><span data-stu-id="2894a-224">toolearn more about Azure Cosmos DB, refer toohello service's [documentation](https://azure.microsoft.com/documentation/services/cosmos-db/) page.</span></span> 

<span data-ttu-id="2894a-225">toounderstand 如何 tooshard 跨多個資料分割，您的資料，請參閱太[Azure Cosmos DB 中的資料分割資料](documentdb-partition-data.md)。</span><span class="sxs-lookup"><span data-stu-id="2894a-225">toounderstand how tooshard your data across multiple partitions, refer too[Partitioning Data in Azure Cosmos DB](documentdb-partition-data.md).</span></span> 
