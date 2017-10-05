---
title: "Azure Cosmos DB 編製索引原則 | Microsoft Docs"
description: "了解 Azure Cosmos DB 中編製索引的運作方式。 了解如何設定編製索引原則，以自動編製索引並追求更高的效能。"
keywords: "編製索引運作方式, 自動編製索引, 為資料庫編製索引"
services: cosmos-db
documentationcenter: 
author: arramac
manager: jhubbard
editor: monicar
ms.assetid: d5e8f338-605d-4dff-8a61-7505d5fc46d7
ms.service: cosmos-db
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 08/17/2017
ms.author: arramac
ms.openlocfilehash: 2c03b498b1530388a48db4d2925debc2e03e30aa
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="how-does-azure-cosmos-db-index-data"></a>Azure Cosmos DB 如何為資料編製索引？

根據預設，會為所有 Azure Cosmos DB 資料編製索引。 儘管許多客戶都樂意讓 Azure Cosmos DB 自動處理所有編製索引層面，但 Azure Cosmos DB 也支援在建立時為集合指定自訂的**編製索引原則**。 相較於其他資料庫平台所提供的次要索引，Azure Cosmos DB 中的編製索引原則在彈性和功能上都更為強大，因為後者可讓您設計和自訂索引的圖形，而不會犧牲結構描述的靈活度。 若要了解編製索引如何在 Azure Cosmos DB 內運作，您必須了解透過管理編製索引原則，您可以在索引儲存空間負荷、寫入和查詢輸送量，以及查詢一致性之間進行細微的取捨。  

在本文中，我們將深入探討 Azure Cosmos DB 編製索引原則、自訂編製索引原則的方式及相關聯的取捨。 

閱讀本文後，您將能夠回答下列問題：

* 如何覆寫要在索引編製中包含或排除的屬性？
* 我要如何設定最終更新的索引？
* 如何設定索引編製來執行 Order By 或範圍查詢？
* 如何變更集合的索引編製原則？
* 如何比較不同索引編製原則的儲存空間和效能？

## <a id="CustomizingIndexingPolicy"></a> 自訂集合的索引編製原則
開發人員可以透過覆寫 Azure Cosmos DB 集合上的預設編製索引原則，並設定下列各方面，來自訂在儲存空間、寫入/查詢效能及查詢一致性之間的取捨。

* **在索引中包含/排除文件和路徑**。 開發人員可以在集合中插入或取代文件時，選擇要在索引中排除或包含的特定文件。 開發人員也可以選擇要包含或排除特定 JSON 屬性 (亦稱為 路徑，包括萬用字元模式)，以便跨索引中包含的文件編製索引。
* **設定各種索引類型**。 開發人員也可以針對每個包含的路徑，根據其資料和預期的查詢工作負載以及每個路徑的數值/字串「精確度」，指定它們在集合上所需的索引類型。
* **設定索引更新模式**。 Azure Cosmos DB 支援三個編製索引模式，這些模式可以透過 Azure Cosmos DB 集合的編製索引原則來設定：「一致」、「延遲」和「無」。 

下列.NET 程式碼片段示範如何在集合建立期間設定自訂索引原則。 在這裡，我們會以最大精確度及字串和數字的範圍索引來設定原則。 此原則可讓我們對字串執行 Order By 查詢。

    DocumentCollection collection = new DocumentCollection { Id = "myCollection" };

    collection.IndexingPolicy = new IndexingPolicy(new RangeIndex(DataType.String) { Precision = -1 });
    collection.IndexingPolicy.IndexingMode = IndexingMode.Consistent;

    await client.CreateDocumentCollectionAsync(UriFactory.CreateDatabaseUri("db"), collection);   


> [!NOTE]
> 索引編製原則的 JSON 結構描述已隨著 REST API 2015-06-03 版的發行而變更，以支援字串的範圍索引。 .NET SDK 1.2.0 及 Java、Python 和 Node.js SDKs 1.1.0 支援新的原則結構描述。 較舊的 SDK 使用 REST API 2015-04-08 版，並支援舊版的索引編製原則結構描述。
> 
> 根據預設，Azure Cosmos DB 會使用雜湊索引為文件內的所有字串屬性一致地編製索引，並使用範圍索引為數值屬性編製索引。  
> 
> 

### <a name="customizing-the-indexing-policy-using-the-portal"></a>使用入口網站自訂編製索引原則

您可以使用 Azure 入口網站變更集合的編製索引原則。 在 Azure 入口網站中開啟您的 Azure Cosmos DB 帳戶，選取您的集合，在左側瀏覽功能表中按一下 [設定]，然後按一下 [編製索引原則]。 在 [編製索引原則] 刀鋒視窗中，變更您的編製索引原則，然後按一下 [確定] 以儲存變更。 

### <a id="indexing-modes"></a>資料庫編製索引模式
Azure Cosmos DB 支援三個編製索引模式，這些模式可以透過 Azure Cosmos DB 集合的編製索引原則來設定：「一致」、「延遲」和「無」。

**一致**：如果將 Azure Cosmos DB 集合的原則指定為「一致」，指定 Azure Cosmos DB 集合上的查詢會依照與針對讀數所指定的相同一致性層級 (也就是強式、限定過期、工作階段或最終) 進行。 索引會在文件更新 (亦即，在 Azure Cosmos DB 集合中插入、取代、更新和刪除文件) 時同步更新。  一致的索引編製支援一致的查詢，但代價可能是減少寫入輸送量。 這指的是減少需要編製索引的唯一路徑以及「一致性層級」的功能。 一致的索引編製模式是針對「快速寫入、立即查詢」工作負載而設計。

**延遲**：為允許最大的文件擷取輸送量，可以使用延遲一致性設定 Azure Cosmos DB 集合，也就是說，查詢最終是一致的。 索引會在 Azure Cosmos DB 集合靜止 (亦即，未充分利用集合的輸送量容量來處理使用者要求) 時，以非同步方式更新。 對於需要文件擷取不受妨礙的「立即擷取、稍後查詢」工作負載，可能適合「延遲」索引編製模式。

**無**：標示為「無」索引模式的集合沒有任何與其相關聯的索引。 如果將 Azure Cosmos DB 做為索引鍵值儲存體，且只能依據文件的 ID 屬性來存取它們，常會使用此選項。 

> [!NOTE]
> 將索引編製原則設定為「無」時，對於捨棄任何現有的索引具有副作用。 如果您的存取模式只需要「識別碼」及/或「自我連結」，請使用此選項。
> 
> 

下列範例示範如何在插入所有文件時，搭配使用 .NET SDK 與一致自動編製索引來建立 Azure Cosmos DB 集合。

下表顯示根據針對集合設定的索引編製模式 (「一致」和「延遲」)，以及針對查詢要求指定的一致性層級，顯示查詢的一致性。 這適用於使用任何介面 (REST API、SDK)，或從預存程序和觸發程序內進行的查詢。 

|一致性|索引模式︰一致|索引模式：緩慢|
|---|---|---|
|重要事項|重要事項|最終|
|限定過期|限定過期|最終|
|工作階段|工作階段|最終|
|最終|最終|最終|

Azure Cosmos DB 會針對在集合上所進行、且編製索引模式為「無」的查詢傳回錯誤。 透過 REST API 中的明確 `x-ms-documentdb-enable-scan` 標頭或使用 .NET SDK 的 `EnableScanInQuery` 要求選項，仍可以掃描形式執行查詢。 部分查詢功能 (例如 ORDER BY) 並不支援做為具有 `EnableScanInQuery`的掃描。

下表根據索引編製模式 (「一致」、「延遲」和「無」)，顯示指定 EnableScanInQuery 時，查詢的一致性。

|一致性|索引模式︰一致|索引模式：緩慢|索引模式：無|
|---|---|---|---|
|重要事項|重要事項|最終|重要事項|
|限定過期|限定過期|最終|限定過期|
|工作階段|工作階段|最終|工作階段|
|最終|最終|最終|最終|

下列程式碼範例示範如何在插入所有文件時，搭配使用 .NET SDK 與一致編製索引來建立 Azure Cosmos DB 集合。

     // Default collection creates a hash index for all string fields and a range index for all numeric    
     // fields. Hash indexes are compact and offer efficient performance for equality queries.

     var collection = new DocumentCollection { Id ="defaultCollection" };

     collection.IndexingPolicy.IndexingMode = IndexingMode.Consistent;

     collection = await client.CreateDocumentCollectionAsync(UriFactory.CreateDatabaseUri("mydb"), collection);


### <a name="index-paths"></a>索引路徑
Azure Cosmos DB 會將 JSON 文件和索引模型化為樹狀結構，並可讓您調整為適用於樹狀結構中之路徑的原則。 您可以選擇編製索引時必須包含或排除文件內的哪些路徑。 針對事先知道查詢模式的情況，這將可改善寫入效能並降低索引儲存。

索引路徑的開頭為根 (/)，且通常結尾為 ? 萬用字元運算子，代表有多個可能的首碼值。 例如，若要為 SELECT * FROM Families F WHERE F.familyName = "Andersen" 提供服務，您必須在集合的索引原則中包含 /familyName/? 的索引路徑。

索引路徑也可以使用 * 萬用字元運算子來指定路徑首碼底下的遞迴行為。 例如，使用 /payload/* 可將 payload 屬性下的所有項目自編製索引作業中排除。

以下是指定索引路徑的常見模式：

| 路徑                | 描述/使用案例                                                                                                                                                                                                                                                                                         |
| ------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| /                   | 集合的預設路徑。 遞迴並套用至整個文件樹狀結構。                                                                                                                                                                                                                                   |
| /prop/?             | 為類似下列的查詢 (類型分別為雜湊或範圍) 提供服務而必要的索引路徑：<br><br>SELECT FROM collection c WHERE c.prop = "value"<br><br>SELECT FROM collection c WHERE c.prop > 5<br><br>SELECT FROM collection c ORDER BY c.prop                                                                       |
| /"prop"/*             | 指定之標籤底下所有路徑的索引路徑。 使用下列查詢<br><br>SELECT FROM collection c WHERE c.prop = "value"<br><br>SELECT FROM collection c WHERE c.prop.subprop > 5<br><br>SELECT FROM collection c WHERE c.prop.subprop.nextprop = "value"<br><br>SELECT FROM collection c ORDER BY c.prop         |
| /props/[]/?         | 為反覆項目及針對 ["a"、"b"、"c"] 等純量陣列進行之聯結查詢提供服務所需的索引路徑：<br><br>SELECT tag FROM tag IN collection.props WHERE tag = "value"<br><br>SELECT tag FROM collection c JOIN tag IN c.props WHERE tag > 5                                                                         |
| /props/[]/subprop/? | 為反覆項目及針對 [{subprop: "a"}, {subprop: "b"}] 等物件陣列進行之聯結查詢提供服務所需的索引路徑：<br><br>SELECT tag FROM tag IN collection.props WHERE tag.subprop = "value"<br><br>SELECT tag FROM collection c JOIN tag IN c.props WHERE tag.subprop = "value"                                  |
| /prop/subprop/?     | 為查詢 (類型分別為雜湊或範圍) 提供服務而必要的索引路徑：<br><br>SELECT FROM collection c WHERE c.prop.subprop = "value"<br><br>SELECT FROM collection c WHERE c.prop.subprop > 5                                                                                                                    |

> [!NOTE]
> 設定自訂的索引路徑時，您必須為由特殊路徑 "/" 所表示的整份文件樹狀目錄指定預設的索引規則。 
> 
> 

下列範例會設定一個採用範圍索引編製且自訂的有效位數值為 20 個位元組：

    var collection = new DocumentCollection { Id = "rangeSinglePathCollection" };    

    collection.IndexingPolicy.IncludedPaths.Add(
        new IncludedPath { 
            Path = "/Title/?", 
            Indexes = new Collection<Index> { 
                new RangeIndex(DataType.String) { Precision = 20 } } 
            });

    // Default for everything else
    collection.IndexingPolicy.IncludedPaths.Add(
        new IncludedPath { 
            Path = "/*" ,
            Indexes = new Collection<Index> {
                new HashIndex(DataType.String) { Precision = 3 }, 
                new RangeIndex(DataType.Number) { Precision = -1 } 
            }
        });

    collection = await client.CreateDocumentCollectionAsync(UriFactory.CreateDatabaseUri("db"), pathRange);


### <a name="index-data-types-kinds-and-precisions"></a>索引資料類型、類型和精確度
探討如何指定路徑之後，讓我們看看我們可以使用那些選項來設定路徑的編製索引原則。 您可以為每個路徑指定一或多個編製索引的定義：

* 資料類型：**String**、**Number**、**Point**、**Polygon** 或 **LineString** (每個路徑每個資料類型只能包含一個項目)
* 索引類型：**雜湊** (相等查詢)、**範圍** (相等、範圍或 Order By 查詢) 或**空間** (空間查詢) 
* 有效位數：字串和數字預設值為 3 的雜湊索引有效位數，會在 1 到 8 之間變換。 至於範圍索引，此值可以是 -1 (最大有效位數)，字串或數字的值可在 1 到 100 之間變換 (最大有效位數)。

#### <a name="index-kind"></a>索引類型
Azure Cosmos DB 支援每個路徑的雜湊和範圍索引種類 (可針對字串、數字或兩者進行設定)。

* **雜湊** 支援有效率的相等查詢和 JOIN 查詢。 針對大多數使用案例，雜湊索引並不需要比預設值 (3 個位元組) 更高的精確度。 DataType 可以是 String 或 Number。
* **範圍**支援有效率的相等查詢、範圍查詢 (使用 >、<、>=、<=、!=) 和 Order By 查詢。 根據預設，Order By 查詢也需要最大索引精確度 (-1)。 DataType 可以是 String 或 Number。

Azure Cosmos DB 針對每個路徑也支援空間索引類型 (可針對 Point、Polygon 或 LineString 資料類型加以指定)。 位於指定路徑的值必須是有效的 GeoJSON 片段，例如 `{"type": "Point", "coordinates": [0.0, 10.0]}`。

* **空間** 支援有效率的空間 (內部和距離) 查詢。 DataType 可以是 Point、Polygon 或 LineString。

> [!NOTE]
> Azure Cosmos DB 支援自動編製 Point、Polygon 及 LineString 的索引。
> 
> 

以下是支援的索引種類和可用來處理的查詢的範例：

| 索引類型 | 描述/使用案例                                                                                                                                                                                                                                                                                                                                                                                                              |
| ---------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 雜湊       | Hash over /prop/? (或 /) 可用來有效率地處理下列查詢︰<br><br>SELECT FROM collection c WHERE c.prop = "value"<br><br>Hash over /props/[]/? (或 / 或 /props/) 可用來有效率地處理下列查詢︰<br><br>SELECT tag FROM collection c JOIN tag IN c.props WHERE tag = 5                                                                                                                       |
| 範圍      | Range over /prop/? (或 /) 可用來有效率地處理下列查詢︰<br><br>SELECT FROM collection c WHERE c.prop = "value"<br><br>SELECT FROM collection c WHERE c.prop > 5<br><br>SELECT FROM collection c ORDER BY c.prop                                                                                                                                                                                                              |
| 空間     | Range over /prop/? (或 /) 可用來有效率地處理下列查詢︰<br><br>SELECT FROM collection c<br><br>WHERE ST_DISTANCE(c.prop, {"type": "Point", "coordinates": [0.0, 10.0]}) < 40<br><br>SELECT FROM collection c WHERE ST_WITHIN(c.prop, {"type": "Polygon", ... }) --with indexing on points enabled<br><br>SELECT FROM collection c WHERE ST_WITHIN({"type": "Point", ... }, c.prop) --with indexing on polygons enabled              |

根據預設，如果沒有 (任何精確度的) 範圍索引，以發出可能需要掃描才能進行查詢的訊號，則所有查詢都會傳回錯誤。 只要在 REST API 中使用 x-ms-documentdb-enable-scans 標頭，或使用 .NET SDK 利用 EnableScanInQuery 要求選項，仍然可以在沒有範圍索引的情況下執行範圍查詢。 如果在查詢中有 Azure Cosmos DB 可以使用索引據以篩選的其他任何篩選，就不會傳回任何錯誤。

相同的規則適用於空間查詢。 根據預設，如果沒有空間索引，而且沒有可從索引提供服務的其他篩選，則會針對空間查詢傳回錯誤。 您可以使用 x-ms-documentdb-enable-scan/EnableScanInQuery 將它們執行為掃描。

#### <a name="index-precision"></a>索引精確度
索引精確度可讓您在索引儲存空間額外負荷和查詢效能之間取捨。 對於數字，建議使用預設精準度組態 -1 (「最大值」)。 因為數字在 JSON 中為 8 個位元組，相當於 8 個位元組的組態。 挑選較低值的精準度，例如 1-7，表示在某個範圍內的值可對應至相同的索引項目。 因此，您將會減少索引儲存空間，但查詢執行可能必須處理更多文件，並且耗用更多輸送量，也就是要求單位。

索引精準度組態對於字串範圍有更實際的應用。 因為字串可以是任意長度，索引精準度的選擇可能會影響字串範圍查詢的效能，並影響所需的索引儲存空間量。 字串範圍索引可以設定為 1-100 或 -1 (「最大值」)。 如果您想要針對字串屬性執行 Order By 查詢，則必須為對應的路徑，將精確度指定為 -1。

空間索引針對所有類型 (Points、LineString 及 Polygon) 一律都使用預設的索引精準度，且無法被覆寫。 

下列範例示範如何使用 .NET SDK 提高集合中範圍索引的精確度。 

**使用自訂索引精確度建立集合**

    var rangeDefault = new DocumentCollection { Id = "rangeCollection" };

    // Override the default policy for Strings to range indexing and "max" (-1) precision
    rangeDefault.IndexingPolicy = new IndexingPolicy(new RangeIndex(DataType.String) { Precision = -1 });

    await client.CreateDocumentCollectionAsync(UriFactory.CreateDatabaseUri("db"), rangeDefault);   


> [!NOTE]
> 當查詢使用 Order By，但沒有針對所查詢路徑之最大精確度的範圍索引時，Azure Cosmos DB 就會傳回錯誤。 
> 
> 

同樣地，可以從索引編製完全排除路徑。 下一個範例示範如何將文件的整個區段 (也稱為 樹狀子目錄) 自索引編製作業中排除 (透過使用 "*" 萬用字元)。

    var collection = new DocumentCollection { Id = "excludedPathCollection" };
    collection.IndexingPolicy.IncludedPaths.Add(new IncludedPath { Path = "/*" });
    collection.IndexingPolicy.ExcludedPaths.Add(new ExcludedPath { Path = "/nonIndexedContent/*" });

    collection = await client.CreateDocumentCollectionAsync(UriFactory.CreateDatabaseUri("db"), excluded);



## <a name="opting-in-and-opting-out-of-indexing"></a>開啟和關閉索引編製
您可以選擇是否要讓集合自動編製所有文件的索引。 根據預設，會自動索引所有文件，但您可以選擇將它關閉。 關閉索引編製功能時，便只能透過文件自己的連結或使用識別碼透過查詢來存取文件。

在關閉自動索引編製功能的情況下，您仍然可以選擇性地只將特定的文件新增到索引中。 相反地，您也可以讓自動索引編製功能保持開啟，並選擇性地只排除特定的文件。 當您只需要查詢文件的子集時，索引編製功能開/關組態相當有用。

例如，下列範例示範如何使用 [DocumentDB API .NET SDK](https://docs.microsoft.com/en-us/azure/cosmos-db/documentdb-sdk-dotnet) 和 [RequestOptions.IndexingDirective](http://msdn.microsoft.com/library/microsoft.azure.documents.client.requestoptions.indexingdirective.aspx) 屬性來明確地包含文件。

    // If you want to override the default collection behavior to either
    // exclude (or include) a Document from indexing,
    // use the RequestOptions.IndexingDirective property.
    client.CreateDocumentAsync(UriFactory.CreateDocumentCollectionUri("db", "coll"),
        new { id = "AndersenFamily", isRegistered = true },
        new RequestOptions { IndexingDirective = IndexingDirective.Include });

## <a name="modifying-the-indexing-policy-of-a-collection"></a>修改集合的索引編製原則
Azure Cosmos DB 可讓您即時對集合的編製索引原則進行變更。 Azure Cosmos DB 集合內編製索引原則中的變更，會導致索引圖形變更，包括可編製索引的路徑、其精確度，以及索引本身的一致性模型。 因此，索引編製原則變更時，需要將舊的索引有效率地轉換成新的索引。 

**線上索引轉換**

![編製索引的運作方式 – Azure Cosmos DB 線上索引轉換](./media/indexing-policies/index-transformations.png)

索引轉換是在線上進行，也就是說，每個舊原則編製的文件索引會根據每個新原則有效率地轉換， **而不會影響集合的寫入可用性或佈建的輸送量** 。 使用 REST API、SDK 或從預存程序和觸發程序中建立的讀取和寫入作業一致性在索引轉換期間不會受到影響。 也就是說，當您進行索引編製原則變更時，您的 App 效能不會降低，也不需要停機時間。

不過，在索引轉換進行期間，不論索引編製模式設定 (「一致」或「延遲」) 為何，查詢最終會是一致的。 這適用於來自所有介面 (REST API、SDK) 的查詢，以及來自預存程序和觸發程序內的查詢。 索引轉換就像延遲索引編製一樣，是以非同步方式，使用適用於指定複本的備用資源，在複本背景執行。 

索引轉換也會在**原位** (就地) 進行，亦即，Azure Cosmos DB 不會保留兩份索引複本，而是將舊索引換成新索引。 也就是說，執行索引轉換時，您的集合中不需要也不會耗用其他任何磁碟空間。

當您變更索引編製原則時，套用變更以便從舊索引移到新索引的方式主要取決於索引編製模式設定，而非其他值，例如，包含/排除的路徑、索引種類和精確度。 如果您的舊原則和新原則使用一致的編製索引模式，Azure Cosmos DB 就會執行線上索引轉換。 您無法在轉換進行時，使用一致的索引編製模式套用另一個索引編製原則變更。

不過，您可以在轉換進行時，移到「延遲」或「無」索引編製模式。 

* 當您移到「延遲」時，所進行的編製索引原則變更就會立即生效，而且 Azure Cosmos DB 會開始以非同步方式重新建立索引。 
* 當您移到「無」時，索引會立即失效。 當您想要取消進行中的轉換，並重新開始其他索引編製原則時，移至「無」相當實用。 

如果您要使用 .NET SDK，可以使用新的 **ReplaceDocumentCollectionAsync** 方法，開始進行索引編製原則變更，並使用 **ReadDocumentCollectionAsync** 呼叫中的 **IndexTransformationProgress** 回應屬性，追蹤索引轉換進度百分比。 其他 SDK 和 REST API 支援對等屬性和方法，以進行索引編製原則變更。

以下是說明如何將集合的索引編製原則從「一致」索引編製模式修改為「延遲」的程式碼片段。

**將索引編製原則從一致修改為延遲**

    // Switch to lazy indexing.
    Console.WriteLine("Changing from Default to Lazy IndexingMode.");

    collection.IndexingPolicy.IndexingMode = IndexingMode.Lazy;

    await client.ReplaceDocumentCollectionAsync(collection);


例如，您可以呼叫 ReadDocumentCollectionAsync 以檢查索引轉換的進度，如下所示。

**追蹤索引轉換的進度**

    long smallWaitTimeMilliseconds = 1000;
    long progress = 0;

    while (progress < 100)
    {
        ResourceResponse<DocumentCollection> collectionReadResponse = await client.ReadDocumentCollectionAsync(
            UriFactory.CreateDocumentCollectionUri("db", "coll"));

        progress = collectionReadResponse.IndexTransformationProgress;

        await Task.Delay(TimeSpan.FromMilliseconds(smallWaitTimeMilliseconds));
    }

您可以移動到「無」索引編製模式，以卸除集合的索引。 如果您想要取消進行中的轉換，並立即開始新的轉換，這可能是實用的操作工具。

**卸除集合的索引**

    // Switch to lazy indexing.
    Console.WriteLine("Dropping index by changing to to the None IndexingMode.");

    collection.IndexingPolicy.IndexingMode = IndexingMode.None;

    await client.ReplaceDocumentCollectionAsync(collection);

您什麼時候會對 Azure Cosmos DB 集合進行編製索引原則變更？ 以下是最常見的使用案例：

* 在正常操作期間提供一致的結果，但在大量資料匯入期間，改回延遲索引編製
* 開始使用目前 Azure Cosmos DB 集合上新的編製索引功能，例如，需要空間索引類型的地理空間查詢，或者需要字串範圍索引類型的 Order By/字串範圍查詢
* 手動選取要編製索引的屬性，並在一段時間後變更
* 調整索引編製精確度，以改善查詢效能或減少耗用的儲存空間

> [!NOTE]
> 若要使用 ReplaceDocumentCollectionAsync 修改索引編製原則，您需要 .NET SDK 1.3.0 版或更新版本
> 
> 為使索引轉換順利完成，您必須確定集合上有足夠的可用儲存空間。 如果集合已達到其儲存配額，將會暫停索引轉換。 一旦有可用的儲存空間 (例如您刪除某些文件)，索引轉換會自動繼續。
> 
> 

## <a name="performance-tuning"></a>效能微調
DocumentDB API 會提供效能度量 (像是已使用的索引儲存體)，以及每個作業的輸送量成本 (要求單位) 等相關資訊。 這項資訊可以用來比較各種編製索引的原則以及用來微調效能。

若要檢查集合的儲存體配額和使用量，請對集合資源執行 HEAD 或 GET 要求，並檢查 x-ms-request-quota 和 x-ms-request-usage 標頭。 在 .NET SDK 中，[ResourceResponse<T\>](http://msdn.microsoft.com/library/dn799209.aspx) 中的 [DocumentSizeQuota](http://msdn.microsoft.com/library/dn850325.aspx) 和 [DocumentSizeUsage](http://msdn.microsoft.com/library/azure/dn850324.aspx) 屬性包含這些對應的值。

     // Measure the document size usage (which includes the index size) against   
     // different policies.
     ResourceResponse<DocumentCollection> collectionInfo = await client.ReadDocumentCollectionAsync(UriFactory.CreateDocumentCollectionUri("db", "coll"));  
     Console.WriteLine("Document size quota: {0}, usage: {1}", collectionInfo.DocumentQuota, collectionInfo.DocumentUsage);


若要測量每一個寫入作業 (建立、更新或刪除) 的索引編製負荷，請檢查 x-ms-request-charge 標頭 (或 .NET SDK 的 [ResourceResponse<T\>](http://msdn.microsoft.com/library/dn799209.aspx) 中同等的 [RequestCharge](http://msdn.microsoft.com/library/dn799099.aspx) 屬性) 來測量這些作業所耗用的要求單位數量。

     // Measure the performance (request units) of writes.     
     ResourceResponse<Document> response = await client.CreateDocumentAsync(UriFactory.CreateDocumentCollectionUri("db", "coll"), myDocument);              
     Console.WriteLine("Insert of document consumed {0} request units", response.RequestCharge);

     // Measure the performance (request units) of queries.    
     IDocumentQuery<dynamic> queryable =  client.CreateDocumentQuery(UriFactory.CreateDocumentCollectionUri("db", "coll"), queryString).AsDocumentQuery();

     double totalRequestCharge = 0;
     while (queryable.HasMoreResults)
     {
        FeedResponse<dynamic> queryResponse = await queryable.ExecuteNextAsync<dynamic>(); 
        Console.WriteLine("Query batch consumed {0} request units",queryResponse.RequestCharge);
        totalRequestCharge += queryResponse.RequestCharge;
     }

     Console.WriteLine("Query consumed {0} request units in total", totalRequestCharge);

## <a name="changes-to-the-indexing-policy-specification"></a>索引編製原則規格的變更
在 2015 年 7 月 7 日的 REST API 2015-06-03 版引進索引編製原則結構描述中的變更。 SDK 版本中的對應類別具有符合結構描述的新實作。 

在 JSON 規格中實作下列變更：

* 索引編製原則支援字串的範圍索引
* 每個路徑可以有多個索引定義，一個定義用於一種資料類型
* 索引編製精確度針對數字支援 1-8、針對字串支援 1-100 和支援 -1 (最大精確度)
* 路徑區段不需要雙引號來逸出每個路徑。 例如，您可以針對 /title/? 新增路徑，而不是 /"title"/?
* 代表「所有路徑」的根路徑可以表示為 /* (除了 / 以外)

如果您有程式碼，會佈建具有以 .NET SDK 1.1.0 版或較舊的版本撰寫的自訂索引編製原則的集合，您必須變更您的應用程式程式碼，處理這些變更以移至 SDK 1.2.0 版。 如果您沒有會設定索引編製原則的程式碼，或打算繼續使用舊的 SDK 版本，則不需要任何變更。

如需實用的比較，以下為使用 REST API 2015-06-03 版及先前的 2015-04-08 版撰寫自訂編製索引原則的範例。

**先前的索引編製原則 JSON**

    {
       "automatic":true,
       "indexingMode":"Consistent",
       "IncludedPaths":[
          {
             "IndexType":"Hash",
             "Path":"/",
             "NumericPrecision":7,
             "StringPrecision":3
          }
       ],
       "ExcludedPaths":[
          "/\"nonIndexedContent\"/*"
       ]
    }

**目前的索引編製原則 JSON**

    {
       "automatic":true,
       "indexingMode":"Consistent",
       "includedPaths":[
          {
             "path":"/*",
             "indexes":[
                {
                   "kind":"Hash",
                   "dataType":"String",
                   "precision":3
                },
                {
                   "kind":"Hash",
                   "dataType":"Number",
                   "precision":7
                }
             ]
          }
       ],
       "ExcludedPaths":[
          {
             "path":"/nonIndexedContent/*"
          }
       ]
    }

## <a name="next-steps"></a>後續步驟
請遵循下列連結以取得索引原則管理範例，以及深入了解 Azure Cosmos DB 的查詢語言。

1. [DocumentDB API .NET 索引管理程式碼範例](https://github.com/Azure/azure-documentdb-net/blob/master/samples/code-samples/IndexManagement/Program.cs)
2. [DocumentDB API REST 集合作業](https://msdn.microsoft.com/library/azure/dn782195.aspx)
3. [使用 SQL 查詢](documentdb-sql-query.md)

