---
title: "aaaAzure Cosmos DB 檢索原則 |Microsoft 文件"
description: "了解 Azure Cosmos DB 中編製索引的運作方式。 了解 tooconfigure 和變更 hello 編製索引原則可自動索引與提升效能。"
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
ms.openlocfilehash: 4f77b352b89382aa3352136038cb0e95c7588aac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-does-azure-cosmos-db-index-data"></a>Azure Cosmos DB 如何為資料編製索引？

根據預設，會為所有 Azure Cosmos DB 資料編製索引。 雖然許多客戶很高興 toolet Azure Cosmos DB 自動處理的編製索引的所有層面，Azure Cosmos DB 也支援指定自訂**編製索引原則**建立期間的集合。 在 Azure Cosmos DB 的檢索原則是更有彈性且功能強大，比在其他資料庫平台，提供次要索引，因為它們可讓您設計和自訂的 hello 索引 hello 圖形不會犧牲結構描述的彈性。 toolearn 編製索引的運作方式在 Azure Cosmos DB 中，您必須了解藉由管理編製索引原則，您可以進行索引儲存體的額外負荷、 寫入及查詢的輸送量，以及查詢一致性的更細緻取捨。  

在本文中，我們採用 Azure Cosmos DB 仔細查看編製索引原則中，如何自訂編製索引原則，並 hello 相關聯的利弊得失。 

閱讀這篇文章之後, 您將會無法 tooanswer hello 下列問題：

* 如何覆寫 hello 屬性 tooinclude 或排除索引？
* 如何設定 hello 索引，最後的更新？
* 我要如何設定檢索 tooperform Order By 或範圍查詢？
* 我要如何讓變更 tooa 集合的編製索引原則？
* 如何比較不同索引編製原則的儲存空間和效能？

## <a id="CustomizingIndexingPolicy"></a>自訂集合的 hello 編製索引原則
開發人員可以藉由覆寫 hello Azure Cosmos DB 集合上的預設檢索原則，並設定下列方面的 hello 自訂 hello 之間的利弊得失儲存體、 寫入/查詢效能和查詢一致性。

* **在索引中包含/排除文件和路徑**。 開發人員可以選擇特定的文件 toobe 排除或包含在 hello 索引中的插入或取代這些 toohello 集合 hello 次。 開發人員也可以選擇 tooinclude 或簡稱排除特定的 JSON 屬性 路徑 （包括萬用字元模式比對） toobe 跨文件索引中所包含的索引。
* **設定各種索引類型**。 針對每個包含 hello 路徑，開發人員也可以指定 hello 類型的集合，根據其資料，並預期的查詢工作負載和 hello 數值/字串"precision"的每個路徑上，它們需要的索引。
* **設定索引更新模式**。 Azure Cosmos DB 支援三個索引的模式，可透過 hello 檢索 Azure Cosmos DB 集合上的原則設定： 一致，Lazy 和 None。 

hello 下列.NET 程式碼片段會示範如何 tooset 期間 hello 集合建立自訂的編製索引原則。 這裡我們在 hello 最大有效位數設定 hello 原則具有範圍索引，如字串與數字。 此原則可讓我們對字串執行 Order By 查詢。

    DocumentCollection collection = new DocumentCollection { Id = "myCollection" };

    collection.IndexingPolicy = new IndexingPolicy(new RangeIndex(DataType.String) { Precision = -1 });
    collection.IndexingPolicy.IndexingMode = IndexingMode.Consistent;

    await client.CreateDocumentCollectionAsync(UriFactory.CreateDatabaseUri("db"), collection);   


> [!NOTE]
> hello 編製索引原則的 JSON 結構描述已變更的 REST API 版的 hello 版本 2015年-06-03 toosupport 範圍索引字串。 .NET SDK 1.2.0 和 Java、 Python 和 Node.js Sdk 1.1.0 支援 hello 新原則的結構描述。 較舊的 Sdk 使用 hello REST API 2015-04-08 版並支援 hello 編製索引原則的舊版結構描述。
> 
> 根據預設，Azure Cosmos DB 會使用雜湊索引為文件內的所有字串屬性一致地編製索引，並使用範圍索引為數值屬性編製索引。  
> 
> 

### <a name="customizing-hello-indexing-policy-using-hello-portal"></a>自訂使用 hello 入口網站的 hello 編製索引原則

您可以變更 hello 編製索引的集合，使用 hello Azure 入口網站的原則。 開啟您的 Azure Cosmos DB 帳戶 hello Azure 入口網站中選取您的集合，在 hello 左的導覽功能表上，按一下**設定**，然後按一下**編製索引原則**。 在 hello**編製索引原則**刀鋒視窗中，變更您的編製索引原則，然後按一下**確定**toosave 您的變更。 

### <a id="indexing-modes"></a>資料庫編製索引模式
Azure Cosmos DB 支援三個索引模式，可透過 hello 編製索引原則 – Azure Cosmos DB 集合上的設定一致、 延遲和無。

**一致**: hello 查詢給定的 Azure Cosmos DB 集合後續的 Azure Cosmos DB 收集原則指定為 「 一致性 」，如果 hello 和 hello 點讀取 （也就是強式，繫結-失效，針對所指定的相同一致性層級工作階段或最終)。 hello 索引會以同步方式為 hello 文件更新 （也就是插入、 取代、 更新和刪除 Azure Cosmos DB 集合中的文件） 的部分更新。  一致的索引在支援一致 hello 成本的可能降低寫入輸送量。 此縮小是 hello 需要 toobe 編製索引的唯一路徑的函式和 hello 「 一致性層級 」。 一致的索引編製模式是針對「快速寫入、立即查詢」工作負載而設計。

**延遲**: tooallow 最大的文件擷取輸送量、 延遲一致性可設定的 Azure Cosmos DB 集合; 意義的查詢最終保持一致。 Azure Cosmos DB 時，集合就靜止也就是 hello 集合的輸送量容量不充分利用的 tooserve 使用者要求時，會以非同步方式更新 hello 索引。 對於需要文件擷取不受妨礙的「立即擷取、稍後查詢」工作負載，可能適合「延遲」索引編製模式。

**無**：標示為「無」索引模式的集合沒有任何與其相關聯的索引。 如果將 Azure Cosmos DB 做為索引鍵值儲存體，且只能依據文件的 ID 屬性來存取它們，常會使用此選項。 

> [!NOTE]
> 設定檢索原則具有 「 無 」 的 hello 有 hello 所造成的副作用卸除任何現有的索引。 如果您的存取模式只需要「識別碼」及/或「自我連結」，請使用此選項。
> 
> 

hello 下列範例顯示如何建立 Azure Cosmos DB 集合使用 hello.NET SDK 上所有的文件插入一致自動索引。

下表中的 hello 顯示 hello 一致性 hello 檢索模式 （一致和 Lazy） hello 集合和 hello 一致性層級指定 hello 查詢要求設定為基礎的查詢。 這適用於使用任何介面-REST API Sdk 進行 tooqueries，或從預存程序和觸發程序。 

|一致性|索引模式︰一致|索引模式：緩慢|
|---|---|---|
|重要事項|重要事項|最終|
|限定過期|限定過期|最終|
|工作階段|工作階段|最終|
|最終|最終|最終|

Azure Cosmos DB 會針對在集合上所進行、且編製索引模式為「無」的查詢傳回錯誤。 查詢仍然會執行為透過明確的 hello 掃描`x-ms-documentdb-enable-scan`標頭中 hello REST API 或 hello`EnableScanInQuery`選項使用 hello.NET SDK 的要求。 部分查詢功能 (例如 ORDER BY) 並不支援做為具有 `EnableScanInQuery`的掃描。

hello 下表顯示 hello 一致性 hello 檢索模式 （一致、 Lazy，和無） 為基礎的查詢指定 EnableScanInQuery 時。

|一致性|索引模式︰一致|索引模式：緩慢|索引模式：無|
|---|---|---|---|
|重要事項|重要事項|最終|重要事項|
|限定過期|限定過期|最終|限定過期|
|工作階段|工作階段|最終|工作階段|
|最終|最終|最終|最終|

hello，下列程式碼範例顯示如何建立具有一致的索引，在所有文件插入上使用.NET SDK hello Azure Cosmos DB 集合。

     // Default collection creates a hash index for all string fields and a range index for all numeric    
     // fields. Hash indexes are compact and offer efficient performance for equality queries.

     var collection = new DocumentCollection { Id ="defaultCollection" };

     collection.IndexingPolicy.IndexingMode = IndexingMode.Consistent;

     collection = await client.CreateDocumentCollectionAsync(UriFactory.CreateDatabaseUri("mydb"), collection);


### <a name="index-paths"></a>索引路徑
Azure Cosmos DB 為樹狀目錄中，模型 JSON 文件和 hello 索引，並可讓您 tootune toopolicies hello 樹狀結構內的路徑。 您可以選擇編製索引時必須包含或排除文件內的哪些路徑。 事先知道 hello 查詢模式時，這可以提供改進的寫入效能和降低索引儲存體案例。

索引路徑開頭 hello 根 （/），而且通常結尾 hello？ 萬用字元運算子，表示有多個可能的值為 hello 前置詞。 比方說，tooserve 選取 * 從系列 F WHERE F.familyName ="Andersen 」，您必須包含 /familyName/ 的索引路徑？ 在 hello 集合索引的原則。

索引路徑也可以使用 hello * 萬用字元運算子 toospecify hello 行為路徑以遞迴方式在 hello 前置詞。 例如，內容 / * 可以是使用的 tooexclude 下方 hello 內容屬性的來源編製索引的所有內容。

以下是 hello 的指定索引路徑的一般模式：

| Path                | 描述/使用案例                                                                                                                                                                                                                                                                                         |
| ------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| /                   | 集合的預設路徑。 遞迴，並套用 toowhole 文件樹狀結構。                                                                                                                                                                                                                                   |
| /prop/?             | 索引路徑所需 tooserve hello 如下的查詢 （具有雜湊或範圍類型分別）：<br><br>SELECT FROM collection c WHERE c.prop = "value"<br><br>SELECT FROM collection c WHERE c.prop > 5<br><br>SELECT FROM collection c ORDER BY c.prop                                                                       |
| /"prop"/*             | 索引路徑 hello 指定標籤底下的所有路徑。 使用下列查詢的 hello<br><br>SELECT FROM collection c WHERE c.prop = "value"<br><br>SELECT FROM collection c WHERE c.prop.subprop > 5<br><br>SELECT FROM collection c WHERE c.prop.subprop.nextprop = "value"<br><br>SELECT FROM collection c ORDER BY c.prop         |
| /props/[]/?         | 索引路徑所需 tooserve 反覆項目和聯結查詢對的純量類似 ["a"、"b"，"c"] 陣列：<br><br>SELECT tag FROM tag IN collection.props WHERE tag = "value"<br><br>SELECT tag FROM collection c JOIN tag IN c.props WHERE tag > 5                                                                         |
| /props/[]/subprop/? | 索引路徑所需 tooserve 反覆項目，而且聯結查詢對物件的陣列會像 [{subprop:"a"}，{subprop:"b"}]:<br><br>SELECT tag FROM tag IN collection.props WHERE tag.subprop = "value"<br><br>SELECT tag FROM collection c JOIN tag IN c.props WHERE tag.subprop = "value"                                  |
| /prop/subprop/?     | 索引路徑所需 tooserve 查詢 （具有雜湊或範圍類型分別）：<br><br>SELECT FROM collection c WHERE c.prop.subprop = "value"<br><br>SELECT FROM collection c WHERE c.prop.subprop > 5                                                                                                                    |

> [!NOTE]
> 設定自訂的索引路徑，您是 hello 特殊路徑所表示的 hello 整份文件樹狀目錄的必要的 toospecify hello 預設索引規則"/ *"。 
> 
> 

hello 下列範例會設定特定的路徑具有範圍索引和自訂的有效位數的值 20 個位元組：

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
既然我們已經看看如何 toospecify 路徑，讓我們來看我們可以使用 hello 選項 tooconfigure hello 編製索引原則的路徑。 您可以為每個路徑指定一或多個編製索引的定義：

* 資料類型：**String**、**Number**、**Point**、**Polygon** 或 **LineString** (每個路徑每個資料類型只能包含一個項目)
* 索引類型：**雜湊** (相等查詢)、**範圍** (相等、範圍或 Order By 查詢) 或**空間** (空間查詢) 
* 有效位數： 雜湊索引的這不同於 1 too8 字串和數字預設值為 3。 至於範圍索引，此值可以是 -1 (最大有效位數)，字串或數字的值可在 1 到 100 之間變換 (最大有效位數)。

#### <a name="index-kind"></a>索引類型
Azure Cosmos DB 支援每個路徑的雜湊和範圍索引種類 (可針對字串、數字或兩者進行設定)。

* **雜湊** 支援有效率的相等查詢和 JOIN 查詢。 大部分的使用情況下，雜湊索引不需要更高的有效位數比 hello 的 3 個位元組的預設值。 DataType 可以是 String 或 Number。
* **範圍**支援有效率的相等查詢、範圍查詢 (使用 >、<、>=、<=、!=) 和 Order By 查詢。 根據預設，Order By 查詢也需要最大索引精確度 (-1)。 DataType 可以是 String 或 Number。

Azure Cosmos DB 也會針對每一個路徑，可指定 hello 點、 多邊形或 LineString 資料類型支援 hello 空間索引類型。 hello hello 指定路徑的值必須是有效的 GeoJSON 片段，例如`{"type": "Point", "coordinates": [0.0, 10.0]}`。

* **空間** 支援有效率的空間 (內部和距離) 查詢。 DataType 可以是 Point、Polygon 或 LineString。

> [!NOTE]
> Azure Cosmos DB 支援自動編製 Point、Polygon 及 LineString 的索引。
> 
> 

以下是支援的 hello 索引類型，它們可以是使用的 tooserve 查詢的範例：

| 索引類型 | 描述/使用案例                                                                                                                                                                                                                                                                                                                                                                                                              |
| ---------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 雜湊       | Hash over /prop/? (或 /) 可以使用的 tooserve hello 遵循查詢有效率地：<br><br>SELECT FROM collection c WHERE c.prop = "value"<br><br>Hash over /props/[]/? (或 / 或/props /) 可以使用的 tooserve hello 遵循查詢有效率地：<br><br>SELECT tag FROM collection c JOIN tag IN c.props WHERE tag = 5                                                                                                                       |
| 範圍      | Range over /prop/? (或 /) 可以使用的 tooserve hello 遵循查詢有效率地：<br><br>SELECT FROM collection c WHERE c.prop = "value"<br><br>SELECT FROM collection c WHERE c.prop > 5<br><br>SELECT FROM collection c ORDER BY c.prop                                                                                                                                                                                                              |
| 空間     | Range over /prop/? (或 /) 可以使用的 tooserve hello 遵循查詢有效率地：<br><br>SELECT FROM collection c<br><br>WHERE ST_DISTANCE(c.prop, {"type": "Point", "coordinates": [0.0, 10.0]}) < 40<br><br>SELECT FROM collection c WHERE ST_WITHIN(c.prop, {"type": "Polygon", ... }) --with indexing on points enabled<br><br>SELECT FROM collection c WHERE ST_WITHIN({"type": "Point", ... }, c.prop) --with indexing on polygons enabled              |

根據預設，則會傳回錯誤的包含查詢這類範圍運算子 > = 如果 （的任何有效位數） 沒有範圍索引順序 toosignal 掃描可能需要 tooserve hello 查詢中。 沒有範圍索引使用 hello REST API 中的 hello x-ms-documentdb-啟用-掃描標頭或 hello EnableScanInQuery 要求選項使用 hello.NET SDK 執行範圍查詢。 如果 Azure Cosmos DB 可以使用針對 hello 索引 toofilter hello 查詢中有任何其他篩選器，將會不傳回任何錯誤。

hello 相同規則適用於空間查詢。 根據預設，錯誤會傳回空間查詢，如果沒有空間索引，而且沒有其他可提供從 hello 索引的篩選。 您可以使用 x-ms-documentdb-enable-scan/EnableScanInQuery 將它們執行為掃描。

#### <a name="index-precision"></a>索引精確度
索引精確度可讓您在索引儲存空間額外負荷和查詢效能之間取捨。 數字，我們建議使用 hello 預設有效位數設定為-1 （「 最大 」）。 由於數字是在 JSON 中的 8 個位元組，這會是 8 個位元組的對等 tooa 組態。 挑選有效位數，例如 1-7，較低的值表示的相同值內某些範圍對應 toohello 索引項目。 因此您將會降低索引儲存空間，但查詢執行可能 tooprocess 多份文件，也因此也就是，使用更多的輸送量單位的要求。

索引精準度組態對於字串範圍有更實際的應用。 字串可以是任何任意長度，因為 hello hello 索引有效位數的選擇會影響字串範圍查詢和索引所需的儲存空間的影響 hello 數量的 hello 效能。 字串範圍索引可以設定為 1-100 或 -1 (「最大值」)。 如果您想要 tooperform Order By 查詢字串屬性，您必須指定有效位數為-1 代表 hello 對應路徑。

空間索引一律會用於所有類型 （點、 LineStrings 和多邊形） 中的 hello 預設索引的有效位數，而且不能已被覆寫。 

下列範例中的 hello 顯示 tooincrease hello 有效位數，範圍的集合，使用 hello.NET SDK 中的索引。 

**使用自訂索引精確度建立集合**

    var rangeDefault = new DocumentCollection { Id = "rangeCollection" };

    // Override hello default policy for Strings toorange indexing and "max" (-1) precision
    rangeDefault.IndexingPolicy = new IndexingPolicy(new RangeIndex(DataType.String) { Precision = -1 });

    await client.CreateDocumentCollectionAsync(UriFactory.CreateDatabaseUri("db"), rangeDefault);   


> [!NOTE]
> 當查詢使用 Order By，但沒有範圍索引對 hello 最大有效位數與 hello 查詢路徑時，azure Cosmos DB 會傳回錯誤。 
> 
> 

同樣地，可以從索引編製完全排除路徑。 hello 下一個範例顯示如何 tooexclude hello 的整個區段文件 （也稱為 子樹狀目錄中） 從索引使用 hello"*"萬用字元。

    var collection = new DocumentCollection { Id = "excludedPathCollection" };
    collection.IndexingPolicy.IncludedPaths.Add(new IncludedPath { Path = "/*" });
    collection.IndexingPolicy.ExcludedPaths.Add(new ExcludedPath { Path = "/nonIndexedContent/*" });

    collection = await client.CreateDocumentCollectionAsync(UriFactory.CreateDatabaseUri("db"), excluded);



## <a name="opting-in-and-opting-out-of-indexing"></a>開啟和關閉索引編製
您可以選擇是否要 hello 集合 tooautomatically 索引的所有文件。 根據預設，都會自動檢索所有文件，但您可以選擇 tooturn 它關閉。 關閉索引編製功能時，便只能透過文件自己的連結或使用識別碼透過查詢來存取文件。

您可以使用自動索引已關閉，仍會選擇性地新增特定的文件 toohello 索引。 相反地，您可以離開自動索引，並選擇性地選擇 tooexclude 只在特定文件。 您有需要 toobe 查詢的文件的子集時，開啟/關閉組態索引非常有用的。

例如，hello 以下範例將示範如何 tooinclude 的文件使用明確的 hello [DocumentDB API.NET SDK](https://docs.microsoft.com/en-us/azure/cosmos-db/documentdb-sdk-dotnet)和 hello [RequestOptions.IndexingDirective](http://msdn.microsoft.com/library/microsoft.azure.documents.client.requestoptions.indexingdirective.aspx)屬性。

    // If you want toooverride hello default collection behavior tooeither
    // exclude (or include) a Document from indexing,
    // use hello RequestOptions.IndexingDirective property.
    client.CreateDocumentAsync(UriFactory.CreateDocumentCollectionUri("db", "coll"),
        new { id = "AndersenFamily", isRegistered = true },
        new RequestOptions { IndexingDirective = IndexingDirective.Include });

## <a name="modifying-hello-indexing-policy-of-a-collection"></a>修改集合中的 hello 編製索引原則
Azure Cosmos DB 可讓您的集合的 toomake 變更 toohello 編製索引原則 hello 即時。 檢索原則的 Azure Cosmos DB 集合中的變更會導致 tooa 變更 hello 索引包括的 hello 路徑可以編製索引，其有效位數，以及 hello 一致性模型的 hello 索引本身的 hello 圖形中。 因此編製索引的原則中的變更實際上必須 hello 舊索引轉換成一個新。 

**線上索引轉換**

![編製索引的運作方式 – Azure Cosmos DB 線上索引轉換](./media/indexing-policies/index-transformations.png)

索引轉換進行連線，這表示每個 hello 舊原則編製索引的 hello 文件會有效率地轉換 hello 新原則**而不會影響 hello 寫入可用性或 hello 佈建的輸送量**的hello 集合。 hello 一致性的讀取和寫入作業使用 hello REST API Sdk 所建立，或從預存程序和觸發程序中不受影響的索引轉換期間。 這表示沒有任何效能降低或停機時間 tooyour 應用程式時做變更的編製索引原則。

不過，在索引轉換為進行 hello 期間，查詢會最終一致不管 hello 索引模式組態 （一致或 Lazy）。 還會套用 tooqueries 從所有介面 – REST API，Sdk，並從預存程序和觸發程序。 就像 Lazy 編製索引與索引轉換是以非同步方式 hello 上背景中執行 hello 複本 hello 可用的備用資源使用給定的複本。 

索引轉換也會一併變更**中 situ** （就地），也就是 Azure Cosmos DB 不會維護兩份 hello 索引和交換 hello 舊索引出以 hello 新。 也就是說，執行索引轉換時，您的集合中不需要也不會耗用其他任何磁碟空間。

當您變更編製索引原則時，如何 hello 變更就會套用的 toomove 從 hello 舊索引 toohello 新其中一個主要取決於 hello hello 比其他值，如包含/排除的路徑、 索引類型和有效位數而讓更多索引模式設定。 如果您的舊原則和新原則使用一致的編製索引模式，Azure Cosmos DB 就會執行線上索引轉換。 Hello 轉換正在進行時，無法套用另一個索引具有一致的檢索模式的原則變更。

不過您就可以移動 tooLazy 或無檢索模式轉換時正在進行中。 

* 當您移動 tooLazy 時，hello 索引原則變更生效立即和 Azure Cosmos DB 開始以非同步方式重新建立 hello 索引。 
* 當您移動 tooNone 時，然後 hello 索引會立即卸除有效。 移動您想 toocancel 正在進行中時，非常有用 tooNone 轉換和不同的編製索引原則重新開始。 

如果您使用 hello.NET SDK，您可以開始使用 hello 新索引的原則變更**ReplaceDocumentCollectionAsync**使用 hello hello 索引轉換的方法和追蹤 hello 百分比進度**IndexTransformationProgress** response 屬性從**ReadDocumentCollectionAsync**呼叫。 其他 Sdk 和 hello REST API 支援對等的屬性和方法來進行索引的原則變更。

以下是示範如何 toomodify 集合的檢索原則一致的檢索模式 tooLazy 從程式碼片段。

**從一致 tooLazy 修改編製索引原則**

    // Switch toolazy indexing.
    Console.WriteLine("Changing from Default tooLazy IndexingMode.");

    collection.IndexingPolicy.IndexingMode = IndexingMode.Lazy;

    await client.ReplaceDocumentCollectionAsync(collection);


您可以檢查呼叫 ReadDocumentCollectionAsync，例如，由索引轉換 hello 進度，如下所示。

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

若要卸除集合的 hello 索引，可以移動 toohello 無索引模式。 如果您想 toocancel 「 進行中 」 轉換，並立即開始一個新，可能很有用的操作工具。

**卸除 hello 索引集合**

    // Switch toolazy indexing.
    Console.WriteLine("Dropping index by changing tootoohello None IndexingMode.");

    collection.IndexingPolicy.IndexingMode = IndexingMode.None;

    await client.ReplaceDocumentCollectionAsync(collection);

何時您會對索引的原則變更 tooyour Azure Cosmos DB 集合？hello 下面是 hello 最常見的使用案例：

* 一般作業期間，提供一致的結果，但切換回 toolazy 大量資料匯入期間的索引
* 開始使用新的索引功能上目前 Azure Cosmos DB 集合中，例如，像地理空間查詢需要 hello 空間索引類型，或 Order By/字串需要 hello 字串範圍索引類型的範圍查詢
* 手動選取 hello 屬性 toobe 編製索引，並將其變更一段時間
* 微調索引的有效位數 tooimprove 查詢效能，或減少耗用儲存體

> [!NOTE]
> 檢索原則 toomodify 使用 ReplaceDocumentCollectionAsync，您需要版本 > = 的 hello.NET SDK 1.3.0
> 
> 對於索引轉換 toocomplete 成功，您必須確定沒有足夠的可用儲存空間可用 hello 集合上。 如果 hello 集合達到其儲存體配額，將會暫停 hello 索引轉換。 一旦有可用的儲存空間 (例如您刪除某些文件)，索引轉換會自動繼續。
> 
> 

## <a name="performance-tuning"></a>效能微調
hello DocumentDB Api 提供效能標準的相關資訊，例如 hello 索引儲存體使用，而且 hello 輸送量成本 （要求單位），針對每個作業。 這項資訊可以各種不同的檢索原則是使用的 toocompare 以及用來微調效能。

toocheck hello 儲存體配額和使用量集合的 hello 集合資源，對執行 HEAD 或 GET 要求，並檢查 hello x-ms-要求的配額和 hello x ms-要求使用標頭。 在 hello.NET SDK，hello [DocumentSizeQuota](http://msdn.microsoft.com/library/dn850325.aspx)和[DocumentSizeUsage](http://msdn.microsoft.com/library/azure/dn850324.aspx)中的屬性[ResourceResponse < T\> ](http://msdn.microsoft.com/library/dn799209.aspx)包含這些對應的值.

     // Measure hello document size usage (which includes hello index size) against   
     // different policies.
     ResourceResponse<DocumentCollection> collectionInfo = await client.ReadDocumentCollectionAsync(UriFactory.CreateDocumentCollectionUri("db", "coll"));  
     Console.WriteLine("Document size quota: {0}, usage: {1}", collectionInfo.DocumentQuota, collectionInfo.DocumentUsage);


toomeasure hello 負擔的索引的每一個寫入作業 （建立、 更新或刪除），檢查 hello x ms-要求免費標頭 (或對等的 hello [RequestCharge](http://msdn.microsoft.com/library/dn799099.aspx)屬性[ResourceResponse < T\>](http://msdn.microsoft.com/library/dn799209.aspx) hello.NET SDK 中) 的這些作業所使用的要求單位 toomeasure hello 數目。

     // Measure hello performance (request units) of writes.     
     ResourceResponse<Document> response = await client.CreateDocumentAsync(UriFactory.CreateDocumentCollectionUri("db", "coll"), myDocument);              
     Console.WriteLine("Insert of document consumed {0} request units", response.RequestCharge);

     // Measure hello performance (request units) of queries.    
     IDocumentQuery<dynamic> queryable =  client.CreateDocumentQuery(UriFactory.CreateDocumentCollectionUri("db", "coll"), queryString).AsDocumentQuery();

     double totalRequestCharge = 0;
     while (queryable.HasMoreResults)
     {
        FeedResponse<dynamic> queryResponse = await queryable.ExecuteNextAsync<dynamic>(); 
        Console.WriteLine("Query batch consumed {0} request units",queryResponse.RequestCharge);
        totalRequestCharge += queryResponse.RequestCharge;
     }

     Console.WriteLine("Query consumed {0} request units in total", totalRequestCharge);

## <a name="changes-toohello-indexing-policy-specification"></a>變更 toohello 編製索引原則規格
於 2015 年 7 月 7 日 REST api 2015-06-03 版引進了編製索引原則的 hello 結構描述的變更。 hello hello SDK 版本中的對應類別具有新實作 toomatch hello 結構描述。 

在 hello JSON 規格中實作 hello 下列變更：

* 索引編製原則支援字串的範圍索引
* 每個路徑可以有多個索引定義，一個定義用於一種資料類型
* 索引編製精確度針對數字支援 1-8、針對字串支援 1-100 和支援 -1 (最大精確度)
* 路徑區段不需要雙引號 tooescape 每個路徑。 例如，您可以針對 /title/? 新增路徑，而不是 /"title"/?
* 代表 「 所有路徑"hello 根路徑可以表示為 / * (除了太 /)

如果您有版本 1.1.0 以撰寫自訂的編製索引原則與佈建集合的程式碼 hello.NET SDK 或更舊版本，您將需要 toochange 您的應用程式程式碼 toohandle 這些變更的順序 toomove tooSDK 版本 1.2.0。 如果您不會編製索引的原則設定的程式碼或計劃 toocontinue 使用較舊的 SDK 版本，不不需要任何變更。

如需實用的比較，以下是一個使用撰寫自訂的編製索引原則 hello REST API 版本 2015年-06-03 的範例與 hello 先前的版本 2015年-04-08。

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
請遵循下列索引原則管理的範例和 toolearn 深入了解 Azure Cosmos DB 的查詢語言的 hello 連結。

1. [DocumentDB API .NET 索引管理程式碼範例](https://github.com/Azure/azure-documentdb-net/blob/master/samples/code-samples/IndexManagement/Program.cs)
2. [DocumentDB API REST 集合作業](https://msdn.microsoft.com/library/azure/dn782195.aspx)
3. [使用 SQL 查詢](documentdb-sql-query.md)

