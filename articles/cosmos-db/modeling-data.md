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
# <a name="modeling-document-data-for-nosql-databases"></a>將 NoSQL 資料庫的文件資料模型化
無結構描述的資料庫，例如 Azure Cosmos DB，讓您輕鬆 super tooembrace 變更 tooyour 資料模型仍應該花費一些時間考慮您的資料。 

為資料要如何儲存 toobe？ 如何為應用程式進行 tooretrieve 和查詢資料？ 您的應用程式是大量讀取或大量寫入？ 

閱讀這篇文章之後, 您將無法 tooanswer hello 下列問題：

* 應如何考慮文件資料庫中的文件？
* 什麼是資料模型化，以及為什麼應該關心？ 
* 文件資料庫不同 tooa 關聯式資料庫中的模型化資料的方式？
* 如何表達非關聯式資料庫中的資料關聯性？
* 當內嵌資料，以及當連結 toodata？

## <a name="embedding-data"></a>內嵌資料
當您啟動文件存放區，例如 Azure Cosmos DB 中的資料模型化時再試一次 tootreat 做為實體**各自獨立的文件**在 JSON 中表示。

在我們更進一步深入探討之前，讓我們往回幾個步驟，看看我們在關聯式資料庫中如何建立某個項目的模型，這是許多人已熟悉的主題。 hello 下列範例顯示如何個人可能會儲存在關聯式資料庫。 

![關聯式資料庫模型](./media/documentdb-modeling-data/relational-data-model.png)

使用關聯式資料庫，我們已針對年 toonormalize 教正規化，正規化。

正規化資料通常包括建立實體，例如個人，，以及細分 toodiscrete 資料片段中。 在 hello 上述範例中，個人可擁有多個連絡人的詳細記錄，以及多個位址記錄。 我們甚至透過進一步擷取一般欄位 (像是類別)，更進一步細分連絡詳細資料。 地址也是如此，此處的每個記錄具有類型 (像是 [住家] 或 [商務]) 

當正規化資料太引導內部部署的 hello**避免儲存重複的資料**上每個記錄和而不是參考 toodata。 在此範例中，tooread 具有所有的連絡人詳細資料和地址的人員，您需要 toouse 聯結 tooeffectively 彙總您的資料在執行階段。

    SELECT p.FirstName, p.LastName, a.City, cd.Detail
    FROM Person p
    JOIN ContactDetail cd ON cd.PersonId = p.Id
    JOIN ContactDetailType on cdt ON cdt.Id = cd.TypeId
    JOIN Address a ON a.PersonId = p.Id

更新單一人員與其連絡詳細資料和地址需要跨許多個別資料表的寫入作業。 

現在讓我們看看我們如何將模型 hello 相同資料做為文件資料庫中的獨立實體。

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

使用 hello 上述方法我們現在有**反正規化**hello 個人記錄其中我們**內嵌**所有 hello toothis 人員，如他們的連絡人詳細資料和地址，單一 tooa 中的相關資訊JSON 文件。
此外，因為我們要在不限制 tooa 固定的結構描述我們有 hello 彈性 toodo 等完全具有不同的圖形的連絡人詳細資料。 

從 hello 資料庫擷取完整的人員記錄現在是單一讀取作業對單一集合與單一文件。 更新連絡詳細資料和地址等個人記錄，也是針對單一文件的單一寫入作業。

反正規化的資料，您的應用程式可能需要 tooissue 減少查詢與更新 toocomplete 常見的作業。 

### <a name="when-tooembed"></a>當 tooembed
一般而言，使用內嵌的資料模型的時機為：

* 實體之間有 **包含** 關聯性。
* 實體之間有 **一對一些** 關聯性。
* 內嵌的資料 **不常變更**。
* 內嵌的資料不會 **無限的成長**。
* 沒有內嵌的資料是**整數**toodata 文件中的。

> [!NOTE]
> 通常反正規化的資料模型可提供較佳的 **讀取** 效能。
> 
> 

### <a name="when-not-tooembed"></a>當不 tooembed
雖然 hello 的經驗法則文件資料庫中的所有項目是 toodenormalize 並 tooa 單一文件中內嵌的所有資料，這可能會導致 toosome 情況下應該避免的。

取得此 JSON 程式碼片段。

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

如果我們要模型化一般的部落格或 CMS 系統，這可能是具有內嵌註解的文章實體的外觀。 hello 與這個範例的問題是註解陣列是該 hello **unbounded**，這表示沒有任何單一 post 可以有註解 （實際） 限制 toohello 號碼。 當 hello hello 文件大小可能會大幅成長，這會成為問題。

因為 hello hello 大小文件會隨著 hello 能力 tootransmit hello 資料 hello 網路，以及讀取和更新的 hello 文件，在小數位數，將會受到影響。

在此情況下，它會遵循模型更好的 tooconsider hello。

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

這個模型經 hello 三個最新的註解內嵌在 hello 張貼本身，也就是具有固定的繫結的陣列時間。 hello 其他註解分組 toobatches 100 的註解中，並儲存在個別的文件。 hello hello 批次大小被選為 100，因為我們的虛構應用程式允許 hello 使用者 tooload 100 註解一次。  

其中內嵌的資料不是最好的另一種情況是 hello 內嵌時，資料通常使用跨文件，而經常變更。 

取得此 JSON 程式碼片段。

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

這可以代表個人的股票組合。 我們已選擇 tooembed hello 股票資訊 tooeach portfolio 文件中。 在環境中相關的資料經常變更股市交易應用程式，例如內嵌經常變更的資料即將 toomean，您會經常更新每個 portfolio 文件每次會在黑市內建。

股票 *zaza* 可能在單一日交易數百次，而上千名使用者的組合上可能有 *zaza*。 資料模型，類似上述的 hello 我們必須 tooupdate 數千個 portfolio 文件開頭 tooa 系統將不會調整很好的每一天多次。 

## <a id="Refer"></a>參考資料
因此，內嵌資料於許多情況下可適用，但很明顯有時反正規化資料將會造成更多問題，使得適得其反。 那我們現在該怎麼辦？ 

關聯式資料庫未 hello 唯一的地方，您可以在其中建立實體之間的關聯性。 文件資料庫中您可以讓一個實際與相關 toodata 其他文件中的文件中的資訊。 現在，我不支援針對甚至一分鐘我們建置系統，會在 Azure Cosmos DB 中，更適合的 tooa 關聯式資料庫或其他任何文件資料庫，但簡單關聯性是正常的而且可以是非常有用。 

Hello 下列 JSON 中我們選擇稍早但這次我們 toohello 股票而不是內嵌的 hello 待辦項目從內建 portfolio toouse hello 的範例。 如此一來，hello 內建項目經常變更整 hello 天 hello 只有文件需要更新 toobe 時 hello 單一內建的文件。 

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


立即缺點 toothis 方法雖然是您的應用程式是否需要的 tooshow 顯示個人的公事包; 時，會保留每種股票資訊在此情況下您需要 toomake 多個往返 toohello 資料庫 tooload hello 資訊的每個內建的文件。 這裡我們讓決策 tooimprove hello 的效率 hello 天當中經常發生，但接著洩露 hello 讀取 hello 這個特定的系統效能可能較不會影響的作業上的寫入作業。

> [!NOTE]
> 正規化的資料模型**可能需要多個往返**toohello 伺服器。
> 
> 

### <a name="what-about-foreign-keys"></a>外部索引鍵呢？
目前沒有條件約束的概念，因為外部索引鍵或其他任何間的文件關聯性必須在文件中是有效的 「 弱式連結 」 與 hello 資料庫本身將不會驗證。 如果您想 hello 參考文件資料的 tooensure tooactually 存在，則您需要 toodo 這在您的應用程式，或透過 hello 使用伺服器端的觸發程序或預存程序，在 Azure Cosmos DB 上。

### <a name="when-tooreference"></a>當 tooreference
一般而言，使用正規化資料模型的時機為：

* 代表 **一對多** 關聯性。
* 代表 **多對多** 關聯性。
* 相關資料 **經常變更**。
* 參考資料可能是 **unbounded**。

> [!NOTE]
> 通常正規化可提供較佳的 **寫入** 效能。
> 
> 

### <a name="where-do-i-put-hello-relationship"></a>其中將放 hello 關聯性？
hello 成長 hello 關聯性可協助您判斷哪一個文件 toostore hello 參考中。

如果看一下 hello JSON 下之模型的發行者和活頁簿。

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

如果每個發行者的 hello 書籍的 hello 數目很小具有有限的成長，然後儲存 hello 發行者文件內的 hello 書籍參考可能很有用。 不過，如果每個發行者的書籍的 hello 數目未繫結，然後此資料模型會導致 toomutable，不斷增加的陣列，如 hello 範例發行者文件上方所示。 

切換項目位元會結果仍代表 hello 但現在相同的資料模型中避免這些大型的可變動集合。

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

在上述範例中的 hello，我們已卸除 hello hello 發行者文件上的未繫結的集合。 而是我們只需要每個活頁簿的文件的參考 toohello 發行者端。

### <a name="how-do-i-model-manymany-relationships"></a>如何建立多對多關聯性的模型？
在關聯式資料庫 *多對多* 關聯性中，通常是與聯結資料表模型化，其只是將記錄從其他資料表聯結在一起。 

![聯結資料表](./media/documentdb-modeling-data/join-table.png)

您可能會想的 tooreplicate hello 同一件事使用文件，並產生資料模型，看起來類似 toohello 下列。

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

這應該可行。 但是，載入可能是以其書籍，作者或載入活頁簿的作者，一律需要針對 hello 資料庫至少兩個額外的查詢。 加入文件和另一個查詢 toofetch hello 實際文件所要加入一個查詢 toohello。 

如果此聯結資料表的作用完全是在結合兩組資料在一起，那麼為何不完全捨棄它？
請考慮下列 hello。

    Author documents:
    {"id": "a1", "name": "Thomas Andersen", "books": ["b1, "b2", "b3"]}
    {"id": "a2", "name": "William Wakefield", "books": ["b1", "b4"]}

    Book documents: 
    {"id": "b1", "name": "Azure Cosmos DB 101", "authors": ["a1", "a2"]}
    {"id": "b2", "name": "Azure Cosmos DB for RDBMS Users", "authors": ["a1"]}
    {"id": "b3", "name": "Learn about Azure Cosmos DB", "authors": ["a1"]}
    {"id": "b4", "name": "Deep Dive in tooAzure Cosmos DB", "authors": ["a2"]}

現在，如果我有一位作者，立即知道哪些書籍，它們還編寫了，並相反如果我有載入的活頁簿文件會知道 hello 識別碼 hello 作者。 這可以節省針對減少伺服器 hello 號碼 hello 聯結資料表的中繼查詢您的應用程式具有 toomake 的往返。 

## <a id="WrapUp"></a>混合式資料模型
我們現在已看過內嵌 (或反正規化) 和參考 (或正規化) 資料，如我們所見，各有其優缺點。 

它不一定有 toobe 是或，不是害怕得的 toomix 事項 up 一點。 

根據您的應用程式特定的使用模式和工作負載，有時可能無法在混用內嵌和參考的資料有意義無法負責人 toosimpler 應用程式邏輯，以更少的伺服器往返同時仍維持良好的效能層級.

請考慮下列 JSON hello。 

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

這裡我們 （大多數） 瀏覽過 hello 內嵌的模型，從其他實體的資料會內嵌在 hello 最上層文件，但參考其他資料。 

如果您看一下 hello 活頁簿的文件，我們可以看到一些有趣的欄位時，我們會審視 hello 陣列的作者。 沒有*識別碼*欄位，也就是我們也使用 toorefer 後 tooan 作者文件、 標準化的模型，但接著我們的標準作法 hello 欄位有*名稱*和*thumbnailUrl*. 我們無法了只卡*識別碼*並留下 hello 應用程式 tooget hello 個別作者文件使用 hello 「 連結 」，從它所需的任何其他資訊，但因為我們的應用程式會顯示 hello 作者名稱和縮圖圖片中的顯示每個活頁簿，我們可以儲存每個活頁簿的來回行程 toohello 伺服器清單中所反正規化**某些**hello 作者的資料。

當然，如果 hello 作者名稱變更，或他們想 tooupdate 其相片我們可能會 toogo 更新每一本書它們曾發行，但我們的應用程式中，然後再根據 hello 假設作者不常變更其名稱，這是可接受的設計決策。  

在 hello 範例有**預先計算的彙總**值 toosave 高度耗費資源的讀取作業上處理。 在 hello 範例中，某些 hello hello 作者文件中內嵌的資料是在執行階段計算的資料。 每次發行新的活頁簿時，會建立活頁簿的文件**和**hello countOfBooks 欄位設定為 tooa 計算值根據 hello 存在某位特定作者的書籍文件數目。 我們可以在其中負擔中順序 toooptimize 讀取寫入 toodo 計算此最佳化會將很讀取大量的系統中。

hello 的模型包含預先計算的欄位做的原因，因為 Azure Cosmos DB 支援能力 toohave**多重文件交易**。 許多 NoSQL 存放區無法跨文件中執行的交易，並因此主張的設計決策，例如"一律內嵌的所有項目 」，因為 toothis 限制。 藉由 Azure Cosmos DB，您可以使用伺服器端觸發程序或預存程序，插入書籍並更新作者，全都在 ACID 交易內完成。 現在您不要**有**tooembed tooone 中的所有文件只 toobe 確定您的資料保持一致。

## <a name="NextSteps"></a>接續步驟
這篇文章 hello 最大心得是 toounderstand，資料模型中的無結構描述的世界時一樣重要。 

就像沒有任何單一方法 toorepresent 一段螢幕上的資料，任何單一方法 toomodel 您的資料。 您需要 toounderstand 您的應用程式，它將會產生，耗用，以及處理 hello 資料。 然後，藉由套用一些 hello 介紹您的指導方針可以建立模型，以解決 hello 即時應用程式需求的相關設定。 當您的應用程式需要 toochange 時，您可以變更而且發展您的資料模型，輕鬆地利用無結構描述的資料庫 tooembrace hello 彈性。 

深入了解 Azure Cosmos DB toolearn 參考 toohello 服務[文件](https://azure.microsoft.com/documentation/services/cosmos-db/)頁面。 

toounderstand 如何 tooshard 跨多個資料分割，您的資料，請參閱太[Azure Cosmos DB 中的資料分割資料](documentdb-partition-data.md)。 
