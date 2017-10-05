---
title: "將 NoSQL 資料庫的文件資料模型化 | Microsoft Docs"
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
ms.openlocfilehash: 16c387fe574243544cf54cf283c7713ddcaa1942
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="modeling-document-data-for-nosql-databases"></a><span data-ttu-id="99f77-104">將 NoSQL 資料庫的文件資料模型化</span><span class="sxs-lookup"><span data-stu-id="99f77-104">Modeling document data for NoSQL databases</span></span>
<span data-ttu-id="99f77-105">雖然無結構描述的資料庫 (像是 Azure Cosmos DB)，讓您極容易運用資料模型變更，但是您仍然應該花一些時間來思考資料。</span><span class="sxs-lookup"><span data-stu-id="99f77-105">While schema-free databases, like Azure Cosmos DB, make it super easy to embrace changes to your data model you should still spend some time thinking about your data.</span></span> 

<span data-ttu-id="99f77-106">要如何儲存資料？</span><span class="sxs-lookup"><span data-stu-id="99f77-106">How is data going to be stored?</span></span> <span data-ttu-id="99f77-107">您的應用程式要如何擷取及查詢資料？</span><span class="sxs-lookup"><span data-stu-id="99f77-107">How is your application going to retrieve and query data?</span></span> <span data-ttu-id="99f77-108">您的應用程式是大量讀取或大量寫入？</span><span class="sxs-lookup"><span data-stu-id="99f77-108">Is your application read heavy, or write heavy?</span></span> 

<span data-ttu-id="99f77-109">閱讀本文後，您將能夠回答下列問題：</span><span class="sxs-lookup"><span data-stu-id="99f77-109">After reading this article, you will be able to answer the following questions:</span></span>

* <span data-ttu-id="99f77-110">應如何考慮文件資料庫中的文件？</span><span class="sxs-lookup"><span data-stu-id="99f77-110">How should I think about a document in a document database?</span></span>
* <span data-ttu-id="99f77-111">什麼是資料模型化，以及為什麼應該關心？</span><span class="sxs-lookup"><span data-stu-id="99f77-111">What is data modeling and why should I care?</span></span> 
* <span data-ttu-id="99f77-112">文件資料庫中的模型化資料與關聯式資料庫有何不同？</span><span class="sxs-lookup"><span data-stu-id="99f77-112">How is modeling data in a document database different to a relational database?</span></span>
* <span data-ttu-id="99f77-113">如何表達非關聯式資料庫中的資料關聯性？</span><span class="sxs-lookup"><span data-stu-id="99f77-113">How do I express data relationships in a non-relational database?</span></span>
* <span data-ttu-id="99f77-114">何時內嵌資料，以及何時連結至資料？</span><span class="sxs-lookup"><span data-stu-id="99f77-114">When do I embed data and when do I link to data?</span></span>

## <a name="embedding-data"></a><span data-ttu-id="99f77-115">內嵌資料</span><span class="sxs-lookup"><span data-stu-id="99f77-115">Embedding data</span></span>
<span data-ttu-id="99f77-116">當您開始在文件存放區 (例如 Azure Cosmos DB) 中將資料模型化時，請嘗試將您的實體視為 JSON 中呈現的 **獨立式文件**。</span><span class="sxs-lookup"><span data-stu-id="99f77-116">When you start modeling data in a document store, such as Azure Cosmos DB, try to treat your entities as **self-contained documents** represented in JSON.</span></span>

<span data-ttu-id="99f77-117">在我們更進一步深入探討之前，讓我們往回幾個步驟，看看我們在關聯式資料庫中如何建立某個項目的模型，這是許多人已熟悉的主題。</span><span class="sxs-lookup"><span data-stu-id="99f77-117">Before we dive in too much further, let us take a few steps back and have a look at how we might model something in a relational database, a subject many of us are already familiar with.</span></span> <span data-ttu-id="99f77-118">下列範例示範人員可能如何儲存在關聯式資料庫中。</span><span class="sxs-lookup"><span data-stu-id="99f77-118">The following example shows how a person might be stored in a relational database.</span></span> 

![關聯式資料庫模型](./media/documentdb-modeling-data/relational-data-model.png)

<span data-ttu-id="99f77-120">使用關聯式資料庫時，我們已多年被告知要進行正規化、正規化、正規化。</span><span class="sxs-lookup"><span data-stu-id="99f77-120">When working with relational databases, we've been taught for years to normalize, normalize, normalize.</span></span>

<span data-ttu-id="99f77-121">將您的資料正規化通常牽涉到取得實體 (例如：個人)，再劃分以顯示各個部分的資料。</span><span class="sxs-lookup"><span data-stu-id="99f77-121">Normalizing your data typically involves taking an entity, such as a person, and breaking it down in to discrete pieces of data.</span></span> <span data-ttu-id="99f77-122">在上述範例中，人員可以有多個連絡詳細資料記錄，以及多個地址記錄。</span><span class="sxs-lookup"><span data-stu-id="99f77-122">In the example above, a person can have multiple contact detail records as well as multiple address records.</span></span> <span data-ttu-id="99f77-123">我們甚至透過進一步擷取一般欄位 (像是類別)，更進一步細分連絡詳細資料。</span><span class="sxs-lookup"><span data-stu-id="99f77-123">We even go one step further and break down contact details by further extracting common fields like a type.</span></span> <span data-ttu-id="99f77-124">地址也是如此，此處的每個記錄具有類型 (像是 [住家] 或 [商務])</span><span class="sxs-lookup"><span data-stu-id="99f77-124">Same for address, each record here has a type like *Home* or *Business*</span></span> 

<span data-ttu-id="99f77-125">將資料正規化的引導前提是在每個記錄資料上 **避免儲存多餘的資料** ，而是參考資料。</span><span class="sxs-lookup"><span data-stu-id="99f77-125">The guiding premise when normalizing data is to **avoid storing redundant data** on each record and rather refer to data.</span></span> <span data-ttu-id="99f77-126">在此範例中，若要讀取人員以及其所有連絡詳細資料和地址，您需要使用「聯結」有效地在執行階段彙總資料。</span><span class="sxs-lookup"><span data-stu-id="99f77-126">In this example, to read a person, with all their contact details and addresses, you need to use JOINS to effectively aggregate your data at run time.</span></span>

    SELECT p.FirstName, p.LastName, a.City, cd.Detail
    FROM Person p
    JOIN ContactDetail cd ON cd.PersonId = p.Id
    JOIN ContactDetailType on cdt ON cdt.Id = cd.TypeId
    JOIN Address a ON a.PersonId = p.Id

<span data-ttu-id="99f77-127">更新單一人員與其連絡詳細資料和地址需要跨許多個別資料表的寫入作業。</span><span class="sxs-lookup"><span data-stu-id="99f77-127">Updating a single person with their contact details and addresses requires write operations across many individual tables.</span></span> 

<span data-ttu-id="99f77-128">現在讓我們看看如何將相同的資料模型化為文件資料庫中的獨立實體。</span><span class="sxs-lookup"><span data-stu-id="99f77-128">Now let's take a look at how we would model the same data as a self-contained entity in a document database.</span></span>

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

<span data-ttu-id="99f77-129">使用上述方法，我們現在已將人員記錄**反正規化**，在此**內嵌**與人員相關的所有資訊 (例如他們的連絡詳細資料和地址) 到單一 JSON 文件。</span><span class="sxs-lookup"><span data-stu-id="99f77-129">Using the approach above we have now **denormalized** the person record where we **embedded** all the information relating to this person, such as their contact details and addresses, in to a single JSON document.</span></span>
<span data-ttu-id="99f77-130">此外，因為我們不受限於固定的結構描述，我們有彈性可進行一些動作，像是讓連絡詳細資料不同的圖形。</span><span class="sxs-lookup"><span data-stu-id="99f77-130">In addition, because we're not confined to a fixed schema we have the flexibility to do things like having contact details of different shapes entirely.</span></span> 

<span data-ttu-id="99f77-131">從資料庫擷取完整的人員記錄現在是針對單一集合和單一文件的單一讀取作業。</span><span class="sxs-lookup"><span data-stu-id="99f77-131">Retrieving a complete person record from the database is now a single read operation against a single collection and for a single document.</span></span> <span data-ttu-id="99f77-132">更新連絡詳細資料和地址等個人記錄，也是針對單一文件的單一寫入作業。</span><span class="sxs-lookup"><span data-stu-id="99f77-132">Updating a person record, with their contact details and addresses, is also a single write operation against a single document.</span></span>

<span data-ttu-id="99f77-133">藉由反正規化資料，您的應用程式可能需要發出更少的查詢和更新以完成一般作業。</span><span class="sxs-lookup"><span data-stu-id="99f77-133">By denormalizing data, your application may need to issue fewer queries and updates to complete common operations.</span></span> 

### <a name="when-to-embed"></a><span data-ttu-id="99f77-134">內嵌的時機</span><span class="sxs-lookup"><span data-stu-id="99f77-134">When to embed</span></span>
<span data-ttu-id="99f77-135">一般而言，使用內嵌的資料模型的時機為：</span><span class="sxs-lookup"><span data-stu-id="99f77-135">In general, use embedded data models when:</span></span>

* <span data-ttu-id="99f77-136">實體之間有 **包含** 關聯性。</span><span class="sxs-lookup"><span data-stu-id="99f77-136">There are **contains** relationships between entities.</span></span>
* <span data-ttu-id="99f77-137">實體之間有 **一對一些** 關聯性。</span><span class="sxs-lookup"><span data-stu-id="99f77-137">There are **one-to-few** relationships between entities.</span></span>
* <span data-ttu-id="99f77-138">內嵌的資料 **不常變更**。</span><span class="sxs-lookup"><span data-stu-id="99f77-138">There is embedded data that **changes infrequently**.</span></span>
* <span data-ttu-id="99f77-139">內嵌的資料不會 **無限的成長**。</span><span class="sxs-lookup"><span data-stu-id="99f77-139">There is embedded data won't grow **without bound**.</span></span>
* <span data-ttu-id="99f77-140">內嵌的資料是文件中資料的 **整數** 。</span><span class="sxs-lookup"><span data-stu-id="99f77-140">There is embedded data that is **integral** to data in a document.</span></span>

> [!NOTE]
> <span data-ttu-id="99f77-141">通常反正規化的資料模型可提供較佳的 **讀取** 效能。</span><span class="sxs-lookup"><span data-stu-id="99f77-141">Typically denormalized data models provide better **read** performance.</span></span>
> 
> 

### <a name="when-not-to-embed"></a><span data-ttu-id="99f77-142">不要內嵌的時機</span><span class="sxs-lookup"><span data-stu-id="99f77-142">When not to embed</span></span>
<span data-ttu-id="99f77-143">雖然在文件資料庫中的經驗法則是反正規化所有項目，並內嵌所有資料至單一文件，這可能導致應該避免的某些情況。</span><span class="sxs-lookup"><span data-stu-id="99f77-143">While the rule of thumb in a document database is to denormalize everything and embed all data in to a single document, this can lead to some situations that should be avoided.</span></span>

<span data-ttu-id="99f77-144">取得此 JSON 程式碼片段。</span><span class="sxs-lookup"><span data-stu-id="99f77-144">Take this JSON snippet.</span></span>

    {
        "id": "1",
        "name": "What's new in the coolest Cloud",
        "summary": "A blog post by someone real famous",
        "comments": [
            {"id": 1, "author": "anon", "comment": "something useful, I'm sure"},
            {"id": 2, "author": "bob", "comment": "wisdom from the interwebs"},
            …
            {"id": 100001, "author": "jane", "comment": "and on we go ..."},
            …
            {"id": 1000000001, "author": "angry", "comment": "blah angry blah angry"},
            …
            {"id": ∞ + 1, "author": "bored", "comment": "oh man, will this ever end?"},
        ]
    }

<span data-ttu-id="99f77-145">如果我們要模型化一般的部落格或 CMS 系統，這可能是具有內嵌註解的文章實體的外觀。</span><span class="sxs-lookup"><span data-stu-id="99f77-145">This might be what a post entity with embedded comments would look like if we were modeling a typical blog, or CMS, system.</span></span> <span data-ttu-id="99f77-146">此範例的問題在於註解陣列是 **unbounded**，表示任何單一文章可以具備的註解數目沒有 (實際) 的限制。</span><span class="sxs-lookup"><span data-stu-id="99f77-146">The problem with this example is that the comments array is **unbounded**, meaning that there is no (practical) limit to the number of comments any single post can have.</span></span> <span data-ttu-id="99f77-147">因為文件的大小可能會大幅成長，這會成為問題。</span><span class="sxs-lookup"><span data-stu-id="99f77-147">This will become a problem as the size of the document could grow significantly.</span></span>

<span data-ttu-id="99f77-148">隨著文件大小的增加，透過網路傳輸資料以及大規模讀取和更新文件的能力，將會受到影響。</span><span class="sxs-lookup"><span data-stu-id="99f77-148">As the size of the document grows the ability to transmit the data over the wire as well as reading and updating the document, at scale, will be impacted.</span></span>

<span data-ttu-id="99f77-149">在此情況下，最好請考慮下列模型。</span><span class="sxs-lookup"><span data-stu-id="99f77-149">In this case it would be better to consider the following model.</span></span>

    Post document:
    {
        "id": "1",
        "name": "What's new in the coolest Cloud",
        "summary": "A blog post by someone real famous",
        "recentComments": [
            {"id": 1, "author": "anon", "comment": "something useful, I'm sure"},
            {"id": 2, "author": "bob", "comment": "wisdom from the interwebs"},
            {"id": 3, "author": "jane", "comment": "....."}
        ]
    }

    Comment documents:
    {
        "postId": "1"
        "comments": [
            {"id": 4, "author": "anon", "comment": "more goodness"},
            {"id": 5, "author": "bob", "comment": "tails from the field"},
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

<span data-ttu-id="99f77-150">此模型的文章本身內嵌有三個最新註解，也就是目前具有固定繫結的陣列。</span><span class="sxs-lookup"><span data-stu-id="99f77-150">This model has the three most recent comments embedded on the post itself, which is an array with a fixed bound this time.</span></span> <span data-ttu-id="99f77-151">其他註解會分組為 100 個註解的批次，並儲存在個別的文件。</span><span class="sxs-lookup"><span data-stu-id="99f77-151">The other comments are grouped in to batches of 100 comments and stored in separate documents.</span></span> <span data-ttu-id="99f77-152">因為我們虛構的應用程式可讓使用者一次載入 100 個註解，因此已將批次大小選擇為 100。</span><span class="sxs-lookup"><span data-stu-id="99f77-152">The size of the batch was chosen as 100 because our fictitious application allows the user to load 100 comments at a time.</span></span>  

<span data-ttu-id="99f77-153">內嵌資料並不是好主意的另一種情況是在內嵌的資料經常跨文件使用，而且會經常變更時。</span><span class="sxs-lookup"><span data-stu-id="99f77-153">Another case where embedding data is not a good idea is when the embedded data is used often across documents and will change frequently.</span></span> 

<span data-ttu-id="99f77-154">取得此 JSON 程式碼片段。</span><span class="sxs-lookup"><span data-stu-id="99f77-154">Take this JSON snippet.</span></span>

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

<span data-ttu-id="99f77-155">這可以代表個人的股票組合。</span><span class="sxs-lookup"><span data-stu-id="99f77-155">This could represent a person's stock portfolio.</span></span> <span data-ttu-id="99f77-156">我們已選擇內嵌股票資料到每個組合文件。</span><span class="sxs-lookup"><span data-stu-id="99f77-156">We have chosen to embed the stock information in to each portfolio document.</span></span> <span data-ttu-id="99f77-157">在相關資料經常會變更的環境中，像是股票交易應用程式，內嵌經常變更的資料表示，每次交易股票時您便經常更新每個組合文件。</span><span class="sxs-lookup"><span data-stu-id="99f77-157">In an environment where related data is changing frequently, like a stock trading application, embedding data that changes frequently is going to mean that you are constantly updating each portfolio document every time a stock is traded.</span></span>

<span data-ttu-id="99f77-158">股票 *zaza* 可能在單一日交易數百次，而上千名使用者的組合上可能有 *zaza*。</span><span class="sxs-lookup"><span data-stu-id="99f77-158">Stock *zaza* may be traded many hundreds of times in a single day and thousands of users could have *zaza* on their portfolio.</span></span> <span data-ttu-id="99f77-159">有鑑於如上所示的資料模型，我們每天必須更新數千個組合文件許多次，導致系統無法妥善延展。</span><span class="sxs-lookup"><span data-stu-id="99f77-159">With a data model like the above we would have to update many thousands of portfolio documents many times every day leading to a system that won't scale very well.</span></span> 

## <span data-ttu-id="99f77-160"><a id="Refer"></a>參考資料</span><span class="sxs-lookup"><span data-stu-id="99f77-160"><a id="Refer"></a>Referencing data</span></span>
<span data-ttu-id="99f77-161">因此，內嵌資料於許多情況下可適用，但很明顯有時反正規化資料將會造成更多問題，使得適得其反。</span><span class="sxs-lookup"><span data-stu-id="99f77-161">So, embedding data works nicely for many cases but it is clear that there are scenarios when denormalizing your data will cause more problems than it is worth.</span></span> <span data-ttu-id="99f77-162">那我們現在該怎麼辦？</span><span class="sxs-lookup"><span data-stu-id="99f77-162">So what do we do now?</span></span> 

<span data-ttu-id="99f77-163">關聯式資料庫不是您可以建立實體之間的關聯性的唯一位置。</span><span class="sxs-lookup"><span data-stu-id="99f77-163">Relational databases are not the only place where you can create relationships between entities.</span></span> <span data-ttu-id="99f77-164">在文件資料庫中，您的文件中可以有實際上與其他文件中的資料相關的資訊。</span><span class="sxs-lookup"><span data-stu-id="99f77-164">In a document database you can have information in one document that actually relates to data in other documents.</span></span> <span data-ttu-id="99f77-165">現在，我不是要多用一分鐘來提倡我們建置的系統會更適合 Azure Cosmos DB 中的關聯式資料庫或任何其他文件資料庫，但是簡單的關聯性很好而且可能非常有用。</span><span class="sxs-lookup"><span data-stu-id="99f77-165">Now, I am not advocating for even one minute that we build systems that would be better suited to a relational database in Azure Cosmos DB, or any other document database, but simple relationships are fine and can be very useful.</span></span> 

<span data-ttu-id="99f77-166">在以下的 JSON 中，我們選擇使用先前的股票組合範例，但這次我們參考組合上的股票項目而不是加以內嵌。</span><span class="sxs-lookup"><span data-stu-id="99f77-166">In the JSON below we chose to use the example of a stock portfolio from earlier but this time we refer to the stock item on the portfolio instead of embedding it.</span></span> <span data-ttu-id="99f77-167">如此一來，經常全天變更的股票項目，需要更新的唯一文件是單一股票文件。</span><span class="sxs-lookup"><span data-stu-id="99f77-167">This way, when the stock item changes frequently throughout the day the only document that needs to be updated is the single stock document.</span></span> 

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


<span data-ttu-id="99f77-168">不過，這個方法目前的缺點是您的應用程式是否需要在顯示人員的組合時顯示持有的每個股票的相關資訊；在此情況下，您必須對資料庫中進行多個來回行程，才能載入每個股票文件的資訊。</span><span class="sxs-lookup"><span data-stu-id="99f77-168">An immediate downside to this approach though is if your application is required to show information about each stock that is held when displaying a person's portfolio; in this case you would need to make multiple trips to the database to load the information for each stock document.</span></span> <span data-ttu-id="99f77-169">在這裡，我們決定提升全天經常發生之寫入作業的效率，但反而對此特定的系統效能影響較小的讀取作業有害。</span><span class="sxs-lookup"><span data-stu-id="99f77-169">Here we've made a decision to improve the efficiency of write operations, which happen frequently throughout the day, but in turn compromised on the read operations that potentially have less impact on the performance of this particular system.</span></span>

> [!NOTE]
> <span data-ttu-id="99f77-170">正規化的資料模型 **可能需要更多來回行程** 到伺服器。</span><span class="sxs-lookup"><span data-stu-id="99f77-170">Normalized data models **can require more round trips** to the server.</span></span>
> 
> 

### <a name="what-about-foreign-keys"></a><span data-ttu-id="99f77-171">外部索引鍵呢？</span><span class="sxs-lookup"><span data-stu-id="99f77-171">What about foreign keys?</span></span>
<span data-ttu-id="99f77-172">因為目前沒有條件約束、外部索引鍵之類的概念，您在文件中具有的任何文件間關聯性實際上是「弱式連結」，並且將不會由資料庫本身驗證。</span><span class="sxs-lookup"><span data-stu-id="99f77-172">Because there is currently no concept of a constraint, foreign-key or otherwise, any inter-document relationships that you have in documents are effectively "weak links" and will not be verified by the database itself.</span></span> <span data-ttu-id="99f77-173">如果您想要確定文件所參考的資料真的存在，您就需要在您的應用程式中這麼做，或在 Azure Cosmos DB 上透過使用伺服器端觸發程序或預存程序。</span><span class="sxs-lookup"><span data-stu-id="99f77-173">If you want to ensure that the data a document is referring to actually exists, then you need to do this in your application, or through the use of server-side triggers or stored procedures on Azure Cosmos DB.</span></span>

### <a name="when-to-reference"></a><span data-ttu-id="99f77-174">參考時機</span><span class="sxs-lookup"><span data-stu-id="99f77-174">When to reference</span></span>
<span data-ttu-id="99f77-175">一般而言，使用正規化資料模型的時機為：</span><span class="sxs-lookup"><span data-stu-id="99f77-175">In general, use normalized data models when:</span></span>

* <span data-ttu-id="99f77-176">代表 **一對多** 關聯性。</span><span class="sxs-lookup"><span data-stu-id="99f77-176">Representing **one-to-many** relationships.</span></span>
* <span data-ttu-id="99f77-177">代表 **多對多** 關聯性。</span><span class="sxs-lookup"><span data-stu-id="99f77-177">Representing **many-to-many** relationships.</span></span>
* <span data-ttu-id="99f77-178">相關資料 **經常變更**。</span><span class="sxs-lookup"><span data-stu-id="99f77-178">Related data **changes frequently**.</span></span>
* <span data-ttu-id="99f77-179">參考資料可能是 **unbounded**。</span><span class="sxs-lookup"><span data-stu-id="99f77-179">Referenced data could be **unbounded**.</span></span>

> [!NOTE]
> <span data-ttu-id="99f77-180">通常正規化可提供較佳的 **寫入** 效能。</span><span class="sxs-lookup"><span data-stu-id="99f77-180">Typically normalizing provides better **write** performance.</span></span>
> 
> 

### <a name="where-do-i-put-the-relationship"></a><span data-ttu-id="99f77-181">放置關聯性的位置為何？</span><span class="sxs-lookup"><span data-stu-id="99f77-181">Where do I put the relationship?</span></span>
<span data-ttu-id="99f77-182">關聯性的成長將有助於判斷用來儲存參考的文件。</span><span class="sxs-lookup"><span data-stu-id="99f77-182">The growth of the relationship will help determine in which document to store the reference.</span></span>

<span data-ttu-id="99f77-183">如果我們看看下面會建立發行者和書籍模型的 JSON。</span><span class="sxs-lookup"><span data-stu-id="99f77-183">If we look at the JSON below that models publishers and books.</span></span>

    Publisher document:
    {
        "id": "mspress",
        "name": "Microsoft Press",
        "books": [ 1, 2, 3, ..., 100, ..., 1000]
    }

    Book documents:
    {"id": "1", "name": "Azure Cosmos DB 101" }
    {"id": "2", "name": "Azure Cosmos DB for RDBMS Users" }
    {"id": "3", "name": "Taking over the world one JSON doc at a time" }
    ...
    {"id": "100", "name": "Learn about Azure Cosmos DB" }
    ...
    {"id": "1000", "name": "Deep Dive in to Azure Cosmos DB" }

<span data-ttu-id="99f77-184">如果每個發行者書籍的數量很少而且成長有限，那麼，將書籍參考儲存在發行者文件內可能很有用。</span><span class="sxs-lookup"><span data-stu-id="99f77-184">If the number of the books per publisher is small with limited growth, then storing the book reference inside the publisher document may be useful.</span></span> <span data-ttu-id="99f77-185">不過，如果每個發行者的書籍數量無限，此資料模型會導致可變動、成長的陣列，如上述的範例發行者文件所示。</span><span class="sxs-lookup"><span data-stu-id="99f77-185">However, if the number of books per publisher is unbounded, then this data model would lead to mutable, growing arrays, as in the example publisher document above.</span></span> 

<span data-ttu-id="99f77-186">切換項目位元會導致模型仍代表相同的資料，但現在可避免這些大型的可變動集合。</span><span class="sxs-lookup"><span data-stu-id="99f77-186">Switching things around a bit would result in a model that still represents the same data but now avoids these large mutable collections.</span></span>

    Publisher document: 
    {
        "id": "mspress",
        "name": "Microsoft Press"
    }

    Book documents: 
    {"id": "1","name": "Azure Cosmos DB 101", "pub-id": "mspress"}
    {"id": "2","name": "Azure Cosmos DB for RDBMS Users", "pub-id": "mspress"}
    {"id": "3","name": "Taking over the world one JSON doc at a time"}
    ...
    {"id": "100","name": "Learn about Azure Cosmos DB", "pub-id": "mspress"}
    ...
    {"id": "1000","name": "Deep Dive in to Azure Cosmos DB", "pub-id": "mspress"}

<span data-ttu-id="99f77-187">在上述範例中，我們在發行者文件上捨棄無限制的集合。</span><span class="sxs-lookup"><span data-stu-id="99f77-187">In the above example, we have dropped the unbounded collection on the publisher document.</span></span> <span data-ttu-id="99f77-188">而我們在每個書籍文件上只有發行者的參考。</span><span class="sxs-lookup"><span data-stu-id="99f77-188">Instead we just have a a reference to the publisher on each book document.</span></span>

### <a name="how-do-i-model-manymany-relationships"></a><span data-ttu-id="99f77-189">如何建立多對多關聯性的模型？</span><span class="sxs-lookup"><span data-stu-id="99f77-189">How do I model many:many relationships?</span></span>
<span data-ttu-id="99f77-190">在關聯式資料庫 *多對多* 關聯性中，通常是與聯結資料表模型化，其只是將記錄從其他資料表聯結在一起。</span><span class="sxs-lookup"><span data-stu-id="99f77-190">In a relational database *many:many* relationships are often modeled with join tables, which just join records from other tables together.</span></span> 

![聯結資料表](./media/documentdb-modeling-data/join-table.png)

<span data-ttu-id="99f77-192">您可能會想要使用文件複寫相同的項目，並產生看起來如下所示的資料模型。</span><span class="sxs-lookup"><span data-stu-id="99f77-192">You might be tempted to replicate the same thing using documents and produce a data model that looks similar to the following.</span></span>

    Author documents: 
    {"id": "a1", "name": "Thomas Andersen" }
    {"id": "a2", "name": "William Wakefield" }

    Book documents:
    {"id": "b1", "name": "Azure Cosmos DB 101" }
    {"id": "b2", "name": "Azure Cosmos DB for RDBMS Users" }
    {"id": "b3", "name": "Taking over the world one JSON doc at a time" }
    {"id": "b4", "name": "Learn about Azure Cosmos DB" }
    {"id": "b5", "name": "Deep Dive in to Azure Cosmos DB" }

    Joining documents: 
    {"authorId": "a1", "bookId": "b1" }
    {"authorId": "a2", "bookId": "b1" }
    {"authorId": "a1", "bookId": "b2" }
    {"authorId": "a1", "bookId": "b3" }

<span data-ttu-id="99f77-193">這應該可行。</span><span class="sxs-lookup"><span data-stu-id="99f77-193">This would work.</span></span> <span data-ttu-id="99f77-194">不過，載入其中一個作者的書籍，或載入書籍的作者，一律需要對資料庫進行至少兩個其他查詢。</span><span class="sxs-lookup"><span data-stu-id="99f77-194">However, loading either an author with their books, or loading a book with its author, would always require at least two additional queries against the database.</span></span> <span data-ttu-id="99f77-195">一個對聯結文件的查詢，另一個查詢則用來擷取實際聯結的文件。</span><span class="sxs-lookup"><span data-stu-id="99f77-195">One query to the joining document and then another query to fetch the actual document being joined.</span></span> 

<span data-ttu-id="99f77-196">如果此聯結資料表的作用完全是在結合兩組資料在一起，那麼為何不完全捨棄它？</span><span class="sxs-lookup"><span data-stu-id="99f77-196">If all this join table is doing is gluing together two pieces of data, then why not drop it completely?</span></span>
<span data-ttu-id="99f77-197">請考慮下列。</span><span class="sxs-lookup"><span data-stu-id="99f77-197">Consider the following.</span></span>

    Author documents:
    {"id": "a1", "name": "Thomas Andersen", "books": ["b1, "b2", "b3"]}
    {"id": "a2", "name": "William Wakefield", "books": ["b1", "b4"]}

    Book documents: 
    {"id": "b1", "name": "Azure Cosmos DB 101", "authors": ["a1", "a2"]}
    {"id": "b2", "name": "Azure Cosmos DB for RDBMS Users", "authors": ["a1"]}
    {"id": "b3", "name": "Learn about Azure Cosmos DB", "authors": ["a1"]}
    {"id": "b4", "name": "Deep Dive in to Azure Cosmos DB", "authors": ["a2"]}

<span data-ttu-id="99f77-198">現在，如果我有作者，我立即會知道他們的書籍，而反之，如果我載入書籍文件，我就知道作者的識別碼。</span><span class="sxs-lookup"><span data-stu-id="99f77-198">Now, if I had an author, I immediately know which books they have written, and conversely if I had a book document loaded I would know the ids of the author(s).</span></span> <span data-ttu-id="99f77-199">這樣可以省下對聯結資料表的中繼查詢，減少您的應用程式必須進行的伺服器來回行程數目。</span><span class="sxs-lookup"><span data-stu-id="99f77-199">This saves that intermediary query against the join table reducing the number of server round trips your application has to make.</span></span> 

## <span data-ttu-id="99f77-200"><a id="WrapUp"></a>混合式資料模型</span><span class="sxs-lookup"><span data-stu-id="99f77-200"><a id="WrapUp"></a>Hybrid data models</span></span>
<span data-ttu-id="99f77-201">我們現在已看過內嵌 (或反正規化) 和參考 (或正規化) 資料，如我們所見，各有其優缺點。</span><span class="sxs-lookup"><span data-stu-id="99f77-201">We've now looked embedding (or denormalizing) and referencing (or normalizing) data, each have their upsides and each have compromises as we have seen.</span></span> 

<span data-ttu-id="99f77-202">不必害怕採行不同的方式。</span><span class="sxs-lookup"><span data-stu-id="99f77-202">It doesn't always have to be either or, don't be scared to mix things up a little.</span></span> 

<span data-ttu-id="99f77-203">根據您的應用程式特定的使用模式和工作負載，可能有時候混用內嵌和參考的資料有意義，而可能導致較簡單的應用程式邏輯與較少的伺服器來回行程，同時維持良好的效能等級。</span><span class="sxs-lookup"><span data-stu-id="99f77-203">Based on your application's specific usage patterns and workloads there may be cases where mixing embedded and referenced data makes sense and could lead to simpler application logic with fewer server round trips while still maintaining a good level of performance.</span></span>

<span data-ttu-id="99f77-204">請考慮下列 JSON。</span><span class="sxs-lookup"><span data-stu-id="99f77-204">Consider the following JSON.</span></span> 

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

<span data-ttu-id="99f77-205">這裡我們 (差不多) 看完了內嵌的模型，即來自其他實體的資料會內嵌在最上層的文件中，但參考其他資料。</span><span class="sxs-lookup"><span data-stu-id="99f77-205">Here we've (mostly) followed the embedded model, where data from other entities are embedded in the top-level document, but other data is referenced.</span></span> 

<span data-ttu-id="99f77-206">如果您查看書籍文件，在查看作者陣列時就會看到一些有趣的欄位。</span><span class="sxs-lookup"><span data-stu-id="99f77-206">If you look at the book document, we can see a few interesting fields when we look at the array of authors.</span></span> <span data-ttu-id="99f77-207">有一個 *id* 欄位，這是我們用來往回參考作者文件的欄位，正規化的模型中的標準作法，然後我們也有 *name* 和 *thumbnailUrl*。</span><span class="sxs-lookup"><span data-stu-id="99f77-207">There is an *id* field which is the field we use to refer back to an author document, standard practice in a normalized model, but then we also have *name* and *thumbnailUrl*.</span></span> <span data-ttu-id="99f77-208">我們可能已受限在 *id* 並讓應用程式使用「連結」向個別作者文件取得其所需的任何其他資訊，但因為我們的應用程式會顯示每個書籍作者的名稱和縮圖圖片，我們可以省下對伺服器就清單中的每個書籍的來回行程由，方法是反正規化 **某些** 作者的資料。</span><span class="sxs-lookup"><span data-stu-id="99f77-208">We could've just stuck with *id* and left the application to get any additional information it needed from the respective author document using the "link", but because our application displays the author's name and a thumbnail picture with every book displayed we can save a round trip to the server per book in a list by denormalizing **some** data from the author.</span></span>

<span data-ttu-id="99f77-209">當然，如果作者的名稱變更，或他們想要更新其相片，我們得更新曾經發行的每個書籍，但對我們的應用程式，根據作者不常變更其名稱的假設，這是可接受的設計決策。</span><span class="sxs-lookup"><span data-stu-id="99f77-209">Sure, if the author's name changed or they wanted to update their photo we'd have to go an update every book they ever published but for our application, based on the assumption that authors don't change their names very often, this is an acceptable design decision.</span></span>  

<span data-ttu-id="99f77-210">在範例中，有 **預先計算彙總** 值可節省讀取作業費用高昂的處理。</span><span class="sxs-lookup"><span data-stu-id="99f77-210">In the example there are **pre-calculated aggregates** values to save expensive processing on a read operation.</span></span> <span data-ttu-id="99f77-211">在範例中，作者文件中內嵌的有些資料是在執行階段計算的資料。</span><span class="sxs-lookup"><span data-stu-id="99f77-211">In the example, some of the data embedded in the author document is data that is calculated at run-time.</span></span> <span data-ttu-id="99f77-212">每次發行新的書籍時，會建立書籍的文件 **並且** 將 countOfBooks 欄位設定為根據某位特定作者存在的書籍文件數目計算值。</span><span class="sxs-lookup"><span data-stu-id="99f77-212">Every time a new book is published, a book document is created **and** the countOfBooks field is set to a calculated value based on the number of book documents that exist for a particular author.</span></span> <span data-ttu-id="99f77-213">在讀取繁重的系統中 (我們可以負擔執行寫入計算以最佳化讀取)，這項最佳化將很適合。</span><span class="sxs-lookup"><span data-stu-id="99f77-213">This optimization would be good in read heavy systems where we can afford to do computations on writes in order to optimize reads.</span></span>

<span data-ttu-id="99f77-214">由於 Azure Cosmos DB 支援**多文件交易**，因此模型現在能夠具有預先計算的欄位。</span><span class="sxs-lookup"><span data-stu-id="99f77-214">The ability to have a model with pre-calculated fields is made possible because Azure Cosmos DB supports **multi-document transactions**.</span></span> <span data-ttu-id="99f77-215">許多 NoSQL 存放區無法跨文件中執行交易，而因為這項限制而提倡「一律內嵌一切」的設計決策。</span><span class="sxs-lookup"><span data-stu-id="99f77-215">Many NoSQL stores cannot do transactions across documents and therefore advocate design decisions, such as "always embed everything", due to this limitation.</span></span> <span data-ttu-id="99f77-216">藉由 Azure Cosmos DB，您可以使用伺服器端觸發程序或預存程序，插入書籍並更新作者，全都在 ACID 交易內完成。</span><span class="sxs-lookup"><span data-stu-id="99f77-216">With Azure Cosmos DB, you can use server-side triggers, or stored procedures, that insert books and update authors all within an ACID transaction.</span></span> <span data-ttu-id="99f77-217">現在您不 **需** 在一份文件內嵌所有內容，只需要確保您的資料保持一致。</span><span class="sxs-lookup"><span data-stu-id="99f77-217">Now you don't **have** to embed everything in to one document just to be sure that your data remains consistent.</span></span>

## <span data-ttu-id="99f77-218"><a name="NextSteps"></a>後續步驟</span><span class="sxs-lookup"><span data-stu-id="99f77-218"><a name="NextSteps"></a>Next steps</span></span>
<span data-ttu-id="99f77-219">從這篇文章獲得的最大的心得是了解在無結構描述的環境中的資料模型化與以往一樣重要。</span><span class="sxs-lookup"><span data-stu-id="99f77-219">The biggest takeaways from this article is to understand that data modeling in a schema-free world is just as important as ever.</span></span> 

<span data-ttu-id="99f77-220">正如同沒有單一方法可表示螢幕上的資料片段，沒有單一方法可為您的資料建立模型。</span><span class="sxs-lookup"><span data-stu-id="99f77-220">Just as there is no single way to represent a piece of data on a screen, there is no single way to model your data.</span></span> <span data-ttu-id="99f77-221">您需要了解您的應用程式，以及它將如何產生、取用及處理資料。</span><span class="sxs-lookup"><span data-stu-id="99f77-221">You need to understand your application and how it will produce, consume, and process the data.</span></span> <span data-ttu-id="99f77-222">然後，藉由套用一些此處所提供的指導方針，您可以設定相關的建立模型，來處理您的應用程式的立即需求。</span><span class="sxs-lookup"><span data-stu-id="99f77-222">Then, by applying some of the guidelines presented here you can set about creating a model that addresses the immediate needs of your application.</span></span> <span data-ttu-id="99f77-223">當您的應用程式需要進行變更時，您可以利用無結構描述之資料庫的彈性來納入變更，並輕鬆進化您的資料模型。</span><span class="sxs-lookup"><span data-stu-id="99f77-223">When your applications need to change, you can leverage the flexibility of a schema-free database to embrace that change and evolve your data model easily.</span></span> 

<span data-ttu-id="99f77-224">若要深入了解 Azure Cosmos DB，請參閱服務的[文件 (英文)](https://azure.microsoft.com/documentation/services/cosmos-db/)頁面。</span><span class="sxs-lookup"><span data-stu-id="99f77-224">To learn more about Azure Cosmos DB, refer to the service's [documentation](https://azure.microsoft.com/documentation/services/cosmos-db/) page.</span></span> 

<span data-ttu-id="99f77-225">若要了解如何跨多個分割將您的資料分區，請參閱[在 Azure Cosmos DB 中分割資料](documentdb-partition-data.md)。</span><span class="sxs-lookup"><span data-stu-id="99f77-225">To understand how to shard your data across multiple partitions, refer to [Partitioning Data in Azure Cosmos DB](documentdb-partition-data.md).</span></span> 
