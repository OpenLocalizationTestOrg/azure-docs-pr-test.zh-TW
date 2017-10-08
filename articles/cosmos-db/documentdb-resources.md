---
title: "aaaAzure Cosmos DB 資源模型和概念 |Microsoft 文件"
description: "深入了解的資料庫、 集合、 使用者定義函數 (UDF)、 文件、 權限 toomanage 資源和多個 Azure Cosmos DB 的階層式模型。"
keywords: "階層式模型, Hierarchical model, cosmosdb, azure, Microsoft azure"
services: cosmos-db
documentationcenter: 
author: AndrewHoh
manager: jhubbard
editor: monicar
ms.assetid: ef9d5c0c-0867-4317-bb1b-98e219799fd5
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/24/2017
ms.author: anhoh
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: fc3642232b86cc27901ebd97456c386829324632
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-hierarchical-resource-model-and-core-concepts"></a>Azure Cosmos DB 階層式資源模型和核心概念
hello Azure Cosmos DB 管理的資料庫實體會參照的 tooas**資源**。 每個資源可透過邏輯 URI 唯一識別。 您可以使用標準 HTTP 動詞命令、 要求/回應標頭和狀態碼的 hello 資源互動。 

讀取這份文件，您將會無法 tooanswer hello 下列問題：

* 什麼是 Cosmos DB 的資源模型？
* 什麼是系統為相對於的 toouser 定義資源定義的資源嗎？
* 如何處理資源？
* 如何使用集合？
* 如何使用預存程序、觸發程序和使用者定義函數 (UDF)？

## <a name="hierarchical-resource-model"></a>階層式資源模型
如 hello 如下圖所示，hello Cosmos DB 階層式**資源模型**帳戶資料庫，每個透過邏輯且穩定 URI 定址的資源集合所組成。 一組資源將會參考的 tooas**摘要**本文中。 

> [!NOTE]
> Azure Cosmos 資料庫提供高效率的 TCP 通訊協定也是在其通訊模型中，可透過 hello RESTful [DocumentDB.NET 用戶端應用程式開發介面](documentdb-sdk-dotnet.md)。
> 
> 

![Azure Cosmos DB 階層式資源模型][1]  
**階層式資源模型**   

toostart 使用資源，您必須[建立資料庫帳戶](create-documentdb-dotnet.md)使用您的 Azure 訂用帳戶。 資料庫帳戶包含一組「資料庫」，而每個資料庫都包含多個「集合」，且各集合因此包含「預存程序」、「觸發程序」、UDF、「文件」和相關「附件」。 資料庫也有相關聯的**使用者**，每個都有一組**權限**tooaccess 集合，預存程序、 觸發程序，Udf、 文件或附件。 雖然資料庫、使用者、權限和集合都是具有已知結構描述的系統定義資源，但是文件和附件包含任意使用者定義 JSON 內容。  

| 資源 | 說明 |
| --- | --- |
| 資料庫帳戶 |資料庫帳戶會與一組資料庫及附件之固定數目的 Blob 儲存體相關聯。 您可以使用 Azure 訂用帳戶建立一或多個資料庫帳戶。 如需詳細資訊，請瀏覽我們的 [定價頁面](https://azure.microsoft.com/pricing/details/cosmos-db/)。 |
| 資料庫 |資料庫是分割給多個集合之文件儲存體的邏輯容器。 同時也是使用者容器。 |
| User |hello 邏輯命名空間範圍的權限。 |
| 權限 |授權權杖存取 tooa 特定資源的使用者相關聯。 |
| 集合 |集合是 JSON 文件的容器與 hello JavaScript 應用程式邏輯。 集合是一個可計費的實體，其中 hello[成本](performance-levels.md)取決於 hello 與 hello 集合相關聯的效能層級。 集合可以跨一個或多個資料分割/伺服器，而且可以延展 toohandle 幾乎沒有限制的磁碟區的儲存體或輸送量。 |
| 預存程序 |這是向集合註冊，且 hello 資料庫引擎內以交易方式執行的 JavaScript 撰寫的應用程式邏輯。 |
| 觸發程序 |以 JavaScript 撰寫的應用程式邏輯，會在插入、取代或刪除作業之前或之後執行。 |
| UDF |以 JavaScript 撰寫的應用程式邏輯。 Udf 啟用 toomodel 自訂查詢運算子，並藉此擴充 hello 核心 DocumentDB API 查詢語言。 |
| 文件 |使用者定義的 (任意) JSON 內容。 根據預設，沒有結構描述需要 toobe 定義也沒有次要索引 toobe 提供所有 hello 文件加入 tooa 集合。 |
| 附件 |附件是含有外部 Blob/媒體之參考資料和相關聯中繼資料的特殊文件。 hello 開發人員可以選擇管理 Cosmos DB toohave hello blob，或將它儲存例如 OneDrive、 Dropbox 等外部 blob 服務提供者。 |

## <a name="system-vs-user-defined-resources"></a>系統與使用者定義的資源
資料庫帳戶、資料庫、集合、使用者、權限、預存程序、觸發程序和 UDF 等資源的結構描述都是固定不變的，因此稱為「系統資源」。 相反地，例如文件和附件資源沒有任何限制 hello 結構描述，是使用者定義資源的範例。 在 Cosmos DB 中，系統和使用者定義資源都會呈現和管理為標準相符 JSON。 系統或使用者定義的所有資源都有 hello 下列常見的屬性。

> [!NOTE]
> 請注意，系統產生的資源屬性在以 JSON 形式表示時，前面都會加上底線 (_)。
> 
> 

<table>
    <tbody>
        <tr>
            <td valign="top"><p><strong>屬性</strong></p></td>
            <td valign="top"><p><strong>可由使用者設定或由系統產生？</strong></p></td>
            <td valign="top"><p><strong>用途</strong></p></td>
        </tr>
        <tr>
            <td valign="top"><p>_rid</p></td>
            <td valign="top"><p>由系統產生</p></td>
            <td valign="top"><p>系統產生，hello 資源的唯一且階層式識別項</p></td>
        </tr>
        <tr>
            <td valign="top"><p>_etag</p></td>
            <td valign="top"><p>由系統產生</p></td>
            <td valign="top"><p>開放式並行存取控制所需的 hello 資源的 etag</p></td>
        </tr>
        <tr>
            <td valign="top"><p>_ts</p></td>
            <td valign="top"><p>由系統產生</p></td>
            <td valign="top"><p>Hello 資源上次更新時間戳記</p></td>
        </tr>
        <tr>
            <td valign="top"><p>_self</p></td>
            <td valign="top"><p>由系統產生</p></td>
            <td valign="top"><p>Hello 資源的唯一可定址 URI</p></td>
        </tr>
        <tr>
            <td valign="top"><p>id</p></td>
            <td valign="top"><p>由系統產生</p></td>
            <td valign="top"><p>使用者定義的 hello 資源的唯一名稱 （hello 與相同資料分割索引鍵的值）。 如果 hello 使用者未指定的識別碼，識別碼會是系統產生</p></td>
        </tr>
    </tbody>
</table>

### <a name="wire-representation-of-resources"></a>以線路表示資源
Cosmos DB 不會要求任何專屬延伸模組 toohello JSON 標準或特殊編碼。它可搭配標準相容的 JSON 文件。  

### <a name="addressing-a-resource"></a>資源定址
所有資源都能以 URI 定址。 hello 值 hello **_self**屬性的資源代表 hello hello 資源的相對 URI。 hello hello URI 的格式包含 hello /\<摘要\>/ {_rid} 路徑片段：  

| 值為 hello （_s） | 說明 |
| --- | --- |
| /dbs |資料庫帳戶下的資料庫摘要 |
| /dbs/{dbName} |資料庫識別碼的事件符合 hello 值 {dbName} |
| /dbs/{dbName}/colls/ |在資料庫底下的集合摘要 |
| /dbs/{dbName}/colls/{collName} |集合識別碼的事件符合 hello 值 {collName} |
| /dbs/{dbName}/colls/{collName}/docs |在集合底下的文件摘要 |
| /dbs/{dbName}/colls/{collName}/docs/{docId} |使用識別碼 hello 值 {文件} 比對文件 |
| /dbs/{dbName}/users/ |在資料庫底下的使用者摘要 |
| /dbs/{dbName}/users/{userId} |使用者識別碼的事件符合 hello 值 {user} |
| /dbs/{dbName}/users/{userId}/permissions |在使用者底下的權限摘要 |
| /dbs/{dbName}/users/{userId}/permissions/{permissionId} |權限識別碼的事件符合 hello 值 {權限。 |

每個資源都有唯一的使用者定義名稱透過 hello id 屬性公開。 注意： 對於文件，如果 hello 使用者未指定的識別碼，我們支援的 Sdk 會自動產生 hello 文件的唯一識別碼。 hello 識別碼是使用者定義字串，向上 too256 hello 特定父系資源內容內是唯一的字元。 

每個資源也有系統產生的階層式的資源識別碼 (也參考 tooas RID)，並透過 hello _rid 屬性。 hello RID 編碼 hello 整個階層的特定資源，而且很方便的內部表示法的分散式方式使用 tooenforce 參考完整性。 hello RID 內是唯一的資料庫帳戶，它會在內部用於 Cosmos db 有效率的路由，而不需要跨磁碟分割查閱。 hello hello （_s） 及 hello _rid 屬性值會替代與標準格式的資源的表示法。 

hello REST Api 支援的資源定址及路由的要求識別碼 hello 和 hello _rid 屬性。

## <a name="database-accounts"></a>資料庫帳戶
您可以使用 Azure 訂用帳戶佈建一或多個 Cosmos DB 資料庫帳戶。

您可以建立及管理透過 hello Azure 入口網站的 Cosmos DB 資料庫帳戶在[http://portal.azure.com/](https://portal.azure.com/)。 建立和管理資料庫帳戶都需要管理存取權，而且只有在 Azure 訂用帳戶下才能執行。 

### <a name="database-account-properties"></a>資料庫帳戶屬性
佈建和管理資料庫帳戶的過程中，您可以設定和讀取 hello 下列屬性：  

<table border="0" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td valign="top"><p><strong>屬性名稱</strong></p></td>
            <td valign="top"><p><strong>說明</strong></p></td>
        </tr>
        <tr>
            <td valign="top"><p>一致性原則</p></td>
            <td valign="top"><p>設定此屬性 tooconfigure hello 預設一致性層級的資料庫帳戶下的所有 hello 集合。 您可以覆寫 hello 依每個要求來使用 hello [x 層 ms-一致性層級] 要求標頭的一致性層級。 <p><p>請注意，這個屬性只適用於 toohello<i>使用者定義資源</i>。 系統定義的所有資源都是設定的 toosupport 讀取/查詢具有強式一致性。</p></td>
        </tr>
        <tr>
            <td valign="top"><p>授權金鑰</p></td>
            <td valign="top"><p>這些是 hello 主要和次要 master 和 readonly 金鑰提供系統管理存取 tooall hello 資料庫帳戶下的 hello 資源。</p></td>
        </tr>
    </tbody>
</table>

請注意，在加法 tooprovisioning，設定和管理您的資料庫帳戶從 hello Azure 入口網站中，您可以也以程式設計方式建立及管理 Cosmos DB 資料庫帳戶使用 hello [Azure Cosmos DB REST Api](/rest/api/documentdb/)為以及[用戶端 Sdk](documentdb-sdk-dotnet.md)。  

## <a name="databases"></a>資料庫
Cosmos DB 資料庫是一個或多個集合和使用者的邏輯容器 hello 下列圖表所示。 您可以建立任意數目的資料庫下 Cosmos DB 資料庫帳戶主體 toooffer 限制。  

![資料庫帳戶和集合階層式模型][2]  
**資料庫是使用者和集合的邏輯容器**

資料庫可包含集合內分割的文件儲存體數量幾乎不受限制。

### <a name="elastic-scale-of-a-cosmos-db-database"></a>Cosmos DB 資料庫靈活的擴充能力
依預設 – 範圍從幾 GB toopetabytes SSD 支援文件儲存體和佈建的輸送量彈性 Cosmos DB 資料庫。 

不同於傳統的 RDBMS 中的資料庫，Cosmos DB 中的資料庫不是已設定領域的 tooa 單一機器。 以 Cosmos DB 應用程式的小數位數必須 toogrow，您可以建立更多的集合、 資料庫或兩者。 的確，Microsoft 中的各種第一方應用程式都是依消費者規模來使用 Cosmos DB，建立極大的 Cosmos DB 資料庫，每個資料庫各包含數千個具有好幾 TB 文件儲存體的集合。 您可以成長或壓縮資料庫，藉由新增或移除集合 toomeet 應用程式的小數位數的需求。 

您可以建立任意數目的資料庫主體 toohello 優惠中的集合。 每個集合有支援的 SSD 儲存體和佈建以供您根據 hello 選的效能層的輸送量。

Cosmos DB 資料庫同時也是使用者的容器。 使用者，在 [開啟] 是一組權限提供更細緻的授權和存取 toocollections、 文件和附加檔案的邏輯命名空間。  

與 hello Cosmos DB 資源模型中的其他資源，可以建立資料庫，取代、 刪除、 讀取或列舉輕鬆地使用任一 hello [REST Api](/rest/api/documentdb/)或任何 hello[用戶端 Sdk](documentdb-sdk-dotnet.md)。 Cosmos DB 保證讀取或查詢 hello 中繼資料的資料庫資源的強式一致性。 自動刪除資料庫，可確保您無法存取任何 hello 集合或其中包含的使用者。   

## <a name="collections"></a>集合
Cosmos DB 集合是 JSON 文件的容器。 

### <a name="elastic-ssd-backed-document-storage"></a>彈性 SSD 支持文件儲存體
集合本質上是彈性的 - 它會隨著您新增或移除文件自動成長和縮減。 集合是邏輯資源，可以跨一或多個實體分割或伺服器。 在集合中的資料分割的 hello 數目取決於 Cosmos DB 根據 hello 儲存大小和 hello 佈建的輸送量的集合。 Cosmos DB 中的每個分割都有其相關聯的固定 SSD 支援儲存體數量，並且複寫以提供高可用性。 資料分割管理完全受 Azure Cosmos DB，且您沒有 toowrite 複雜的程式碼或管理您的資料分割。 從儲存體和輸送量的角度來看，Cosmos DB 集合「實際上並無限制」。 

### <a name="automatic-indexing-of-collections"></a>集合的自動編製索引
Cosmos DB 是真正不具結構描述的資料庫系統。 它不會假設或 hello JSON 文件所需的任何結構描述。 當您加入文件 tooa 集合，Cosmos DB 自動建立它們的索引，而且它們可供您 tooquery。 在不需要結構描述或次要索引的情況下自動編製文件索引是 Cosmos DB 的重要功能，並且會啟用以獲得寫入最佳化、無鎖定和記錄結構化索引維護技術。 Cosmos DB 支援極快速持續寫入量，同時仍然提供一致的查詢。 文件和索引的儲存體是使用每個集合所耗用的 toocalculate hello 存放裝置。 您可以控制 hello 儲存和效能取捨相關聯索引所設定之集合的 hello 編製索引原則。 

### <a name="configuring-hello-indexing-policy-of-a-collection"></a>設定集合中的 hello 編製索引原則
檢索原則的每個集合的 hello 可讓您 toomake 效能和儲存體的利弊得失與索引相關聯。 hello 下列選項可使用 tooyou 索引組態的一部分：  

* 選擇是否 hello 集合會自動索引 hello 文件的所有與否。 預設會自動編製所有文件的索引。 您可以選擇關閉自動檢索 tooturn，並選擇性地新增特定的文件 toohello 索引。 相反地，您可以選擇性地選擇 tooexclude 只有特定的文件。 您可以藉由設定在集合中的 hello indexingPolicy hello 自動屬性 toobe true 或 false，並使用 hello [x-ms-indexingdirective] 要求標頭時插入、 取代或刪除文件來達到這個目的。  
* 選擇 tooinclude 或排除特定的路徑或從您的文件中的模式 hello 索引。 您可以達到此目的設定 includedPaths 並在集合中的 hello indexingPolicy excludedPaths 分別。 您也可以設定 hello 儲存和效能取捨範圍，再雜湊的特定路徑模式的查詢。 
* 選擇同步 (一致) 與非同步 (緩慢) 索引更新。 根據預設，hello 索引會以同步方式在每個插入、 取代或刪除文件 toohello 集合中的更新。 這可讓 hello 查詢 toohonor hello 相同一致性層級的 hello 文件讀取。 雖然 Cosmos DB 有防寫最佳化，並支援持續性磁碟區的文件寫入，以及同步索引維護和服務一致的查詢，您可以設定特定集合 tooupdate 其索引延遲的方式。 延遲索引進一步 hello 寫入效能的提升，且適合用來大量擷取案例主要是大量讀取的集合。

hello 集合上執行 PUT 可以變更 hello 編製索引原則。 這可能是達成方式是透過 hello[用戶端 SDK](documentdb-sdk-dotnet.md)，hello [Azure 入口網站](https://portal.azure.com)或 hello [REST Api](/rest/api/documentdb/)。

### <a name="querying-a-collection"></a>查詢集合
在集合中的 hello 文件可以有任意的結構描述，您可以查詢集合中的文件，但未提供任何結構描述或預先次要索引。 您可以查詢使用 hello hello 集合[Azure Cosmos DB DocumentDB API: SQL 語法參考](https://msdn.microsoft.com/library/azure/dn782250.aspx)，這樣會提供豐富的階層式、 關聯式及空間運算子，並透過 JavaScript 為基礎的 Udf 的擴充性。 JSON 的文法，可讓模型 JSON 文件以 hello 樹狀目錄節點的標籤與樹狀目錄。 這會同時應用 DocumentDB API 的自動編製索引技術與 DocumentDB API 的 SQL 方言。 hello DocumetDB API 查詢語言包含三個主要層面：   

1. 較少的自然對應 toohello 樹狀結構，包括階層式查詢和預測的查詢作業。 
2. 關聯式作業 (包括複合、篩選、投射、彙總和自我聯結) 的子集。 
3. 可與 (1) 和 (2) 搭配使用的純 JavaScript 型 UDF。  

hello Cosmos DB 查詢模型嘗試 toostrike 功能、 效率和簡化之間取得平衡。 hello Cosmos DB 資料庫引擎原生會編譯並執行 hello SQL 查詢陳述式。 您可以查詢集合，使用 hello [REST Api](/rest/api/documentdb/)或任何 hello[用戶端 Sdk](documentdb-sdk-dotnet.md)。 hello.NET SDK 隨附 LINQ 提供者。

> [!TIP]
> 您可以試用 hello DocumentDB API，並對我們 hello 中的資料集執行 SQL 查詢[查詢遊樂場](https://www.documentdb.com/sql/demo)。
> 
> 

## <a name="multi-document-transactions"></a>多文件交易
資料庫交易提供安全且可預測的程式設計模型處理並行的變更 toohello 資料。 在 RDBMS，hello 傳統方式 toowrite 商務邏輯是 toowrite**預存程序**及/或**觸發程序**和出貨它 toohello 交易執行的資料庫伺服器。 RDBMS，在 hello 應用程式設計人員會是與兩個不同的程式設計語言的必要的 toodeal: 

* hello （非交易式） 應用程式的程式語言 （例如 JavaScript、 Python、 C#、 Java 等）
* T-SQL、 hello 異動程式設計語言的原生執行方式是 hello 資料庫

由於其深層承諾 tooJavaScript 和 JSON 直接在 hello 資料庫引擎內，Cosmos DB 會提供直覺式的程式設計模型執行的 JavaScript hello 集合以預存程序中直接根據應用程式邏輯和觸發程序。 這可讓這兩個 hello 下列：

* 有效率的並行實作控制項，復原時，自動編製索引的直接在 hello 資料庫引擎中的 hello JSON 物件圖形
* 自然表達 控制流程、 變數範圍，指派和例外狀況處理基本類型與直接以 hello JavaScript 的程式設計語言的資料庫交易的整合

hello JavaScript 邏輯在集合層級註冊可以再發出 hello 文件上的資料庫作業的指定集合的 hello。 Cosmos DB 隱含包裝 hello JavaScript 基礎預存程序和觸發程序與跨快照集隔離的環境 ACID 交易內文件集合內。 在其執行中，hello 過程期間如果 hello JavaScript 會擲回的例外狀況，然後 hello 整筆交易便會中止。 hello 產生的程式設計模型是非常簡單但強大。 JavaScript 開發人員會取得「持續性」程式設計模型，同時仍然使用其熟悉的語言建構和程式庫基本。   

hello 直接 hello 資料庫內的能力 tooexecute JavaScript 引擎在 hello 相同位址空間，因為如此 hello 緩衝集區可以高效能和交易式資料庫對 hello 文件中的作業集合的執行。 此外，Cosmos DB 資料庫引擎進行深層承諾 toohello JSON 及 JavaScript 排除任何 hello 的型別系統的應用程式與 hello 資料庫之間的阻抗不相符。   

建立集合之後, 您可以向預存程序、 觸發程序和 Udf 集合使用 hello [REST Api](/rest/api/documentdb/)或任何 hello[用戶端 Sdk](documentdb-sdk-dotnet.md)。 註冊之後，您就可以參考和執行它們。 請考慮 hello 下列預存程序完全以 JavaScript 撰寫 hello 的下列程式碼會採用兩個引數 （書籍名稱和作者名稱） 和建立新的文件、 文件的查詢，然後更新它 – 所有隱含的 ACID 交易中。 在任何時間點 hello 執行期間，如果擲回 JavaScript 例外狀況，hello 整個交易中止。

    function businessLogic(name, author) {
        var context = getContext();
        var collectionManager = context.getCollection();        
        var collectionLink = collectionManager.getSelfLink()

        // create a new document.
        collectionManager.createDocument(collectionLink,
            {id: name, author: author},
            function(err, documentCreated) {
                if(err) throw new Error(err.message);

                // filter documents by author
                var filterQuery = "SELECT * from root r WHERE r.author = 'George R.'";
                collectionManager.queryDocuments(collectionLink,
                    filterQuery,
                    function(err, matchingDocuments) {
                        if(err) throw new Error(err.message);

                        context.getResponse().setBody(matchingDocuments.length);

                        // Replace hello author name for all documents that satisfied hello query.
                        for (var i = 0; i < matchingDocuments.length; i++) {
                            matchingDocuments[i].author = "George R. R. Martin";
                            // we don’t need tooexecute a callback because they are in parallel
                            collectionManager.replaceDocument(matchingDocuments[i]._self,
                                matchingDocuments[i]);   
                        }
                    })
            })
    };

hello 用戶端可以"ship"hello 上方 JavaScript 邏輯 toohello 資料庫進行透過 HTTP POST 的交易式執行。 如需關於使用 HTTP 方法的詳細資訊，請參閱[與 Azure Cosmos DB 資源進行 RESTful 互動 (英文)](https://msdn.microsoft.com/library/azure/mt622086.aspx)。 

    client.createStoredProcedureAsync(collection._self, {id: "CRUDProc", body: businessLogic})
       .then(function(createdStoredProcedure) {
            return client.executeStoredProcedureAsync(createdStoredProcedure.resource._self,
                "NoSQL Distilled",
                "Martin Fowler");
        })
        .then(function(result) {
            console.log(result);
        },
        function(error) {
            console.log(error);
        });


請注意，JSON 及 JavaScript，原本即了解 hello 資料庫，因為沒有任何型別系統不符，「 OR 對應 」 或所需的程式碼產生識別常數。   

預存程序和觸發程序互動集合和 hello 文件集合透過妥善定義的物件模型，公開 hello 目前集合的內容中。  

集合中 hello DocumentDB API 建立、 刪除、 讀取或列舉輕鬆地使用任一 hello [REST Api](/rest/api/documentdb/)或任何 hello[用戶端 Sdk](documentdb-sdk-dotnet.md)。 hello DocumentDB API 一律會提供強式一致性的讀取或查詢集合中的 hello 中繼資料。 刪除集合時，會自動以確保您無法存取任何 hello 文件、 附件、 預存程序、 觸發程序和 Udf 包含在其中。   

## <a name="stored-procedures-triggers-and-user-defined-functions-udf"></a>預存程序、觸發程序和使用者定義函數 (UDF)
Hello 上一節所述，您可以撰寫應用程式邏輯 toorun 直接在交易內 hello 資料庫引擎內。 hello 應用程式邏輯可以完全以 JavaScript 撰寫並為預存程序、 觸發程序或 UDF 可以模式化。 hello 預存程序或觸發程序中的 JavaScript 程式碼可以插入、 取代、 刪除集合中的讀取或查詢文件。 在 hello 另一方面，hello JavaScript UDF 內無法插入、 取代或刪除文件。 Udf 列舉查詢的結果集的 hello 文件，並會產生另一個結果集。 若是多重租用，Cosmos DB 會強制執行嚴謹的保留型資源管理。 每個預存程序、 觸發程序或 UDF 取得固定的配量的作業系統資源 toodo 其工作。 此外，預存程序、 觸發程序或 Udf 無法針對外部的 JavaScript 程式庫連結，並會列入黑名單中而如果超過配置 toothem hello 資源預算。 您可以註冊、 取消註冊預存程序、 觸發程序或 Udf，使用集合與 hello REST Api。  註冊時，預存程序、觸發程序或 UDF 會預先編譯並儲存為位元組程式碼，以在稍後執行。 hello 下列章節說明如何使用 hello Cosmos DB JavaScript SDK tooregister、 執行和取消註冊預存程序、 觸發程序和 UDF。 hello JavaScript SDK 是簡單的包裝函式透過 hello [REST Api](/rest/api/documentdb/)。 

### <a name="registering-a-stored-procedure"></a>註冊預存程序
透過 HTTP POST 在集合上建立新的預存程序資源，即可註冊預存程序。  

    var storedProc = {
        id: "validateAndCreate",
        body: function (documentToCreate) {
            documentToCreate.id = documentToCreate.id.toUpperCase();

            var collectionManager = getContext().getCollection();
            collectionManager.createDocument(collectionManager.getSelfLink(),
                documentToCreate,
                function(err, documentCreated) {
                    if(err) throw new Error('Error while creating document: ' + err.message;
                    getContext().getResponse().setBody('success - created ' + 
                            documentCreated.name);
                });
        }
    };

    client.createStoredProcedureAsync(collection._self, storedProc)
        .then(function (createdStoredProcedure) {
            console.log("Successfully created stored procedure");
        }, function(error) {
            console.log("Error");
        });

### <a name="executing-a-stored-procedure"></a>執行預存程序
預存程序的執行方式是藉由 hello 要求主體中傳遞參數 toohello 程序發出 HTTP POST 對現有的預存程序資源。

    var inputDocument = {id : "document1", author: "G. G. Marquez"};
    client.executeStoredProcedureAsync(createdStoredProcedure.resource._self, inputDocument)
        .then(function(executionResult) {
            assert.equal(executionResult, "success - created DOCUMENT1");
        }, function(error) {
            console.log("Error");
        });

### <a name="unregistering-a-stored-procedure"></a>取消註冊預存程序
只要對現有預存程序資源發出 HTTP DELETE，即可取消註冊預存程序。   

    client.deleteStoredProcedureAsync(createdStoredProcedure.resource._self)
        .then(function (response) {
            return;
        }, function(error) {
            console.log("Error");
        });


### <a name="registering-a-pre-trigger"></a>註冊預先觸發程序
透過 HTTP POST 在集合上建立新的觸發程序資源，即可註冊觸發程序。 您可以指定是否 hello 觸發程序會預先或是張貼觸發程序和 hello 類型的作業 （例如建立、 取代、 刪除或所有） 相關聯。   

    var preTrigger = {
        id: "upperCaseId",
        body: function() {
                var item = getContext().getRequest().getBody();
                item.id = item.id.toUpperCase();
                getContext().getRequest().setBody(item);
        },
        triggerType: TriggerType.Pre,
        triggerOperation: TriggerOperation.All
    }

    client.createTriggerAsync(collection._self, preTrigger)
        .then(function (createdPreTrigger) {
            console.log("Successfully created trigger");
        }, function(error) {
            console.log("Error");
        });

### <a name="executing-a-pre-trigger"></a>執行預先觸發程序
觸發程序的執行方式是在 hello 時間發出 hello 透過 hello 要求標頭的文件資源的 POST/PUT/DEKETE 要求指定 hello 現有觸發程序的名稱。  

    client.createDocumentAsync(collection._self, { id: "doc1", key: "Love in hello Time of Cholera" }, { preTriggerInclude: "upperCaseId" })
        .then(function(createdDocument) {
            assert.equal(createdDocument.resource.id, "DOC1");
        }, function(error) {
            console.log("Error");
        });

### <a name="unregistering-a-pre-trigger"></a>取消註冊預先觸發程序
只要對現有觸發程序資源發出 HTTP DELETE，即可取消註冊觸發程序。  

    client.deleteTriggerAsync(createdPreTrigger._self);
        .then(function(response) {
            return;
        }, function(error) {
            console.log("Error");
        });

### <a name="registering-a-udf"></a>註冊 UDF
透過 HTTP POST 在集合上建立新的 UDF 資源，即可註冊 UDF。  

    var udf = { 
        id: "mathSqrt",
        body: function(number) {
                return Math.sqrt(number);
        },
    };
    client.createUserDefinedFunctionAsync(collection._self, udf)
        .then(function (createdUdf) {
            console.log("Successfully created stored procedure");
        }, function(error) {
            console.log("Error");
        });

### <a name="executing-a-udf-as-part-of-hello-query"></a>執行 hello 查詢 UDF
UDF 可以指定為 hello SQL 查詢的一部份，並做為方法 tooextend hello 核心[hello DocumentDB API 的 SQL 查詢語言](https://msdn.microsoft.com/library/azure/dn782250.aspx)。

    var filterQuery = "SELECT udf.mathSqrt(r.Age) AS sqrtAge FROM root r WHERE r.FirstName='John'";
    client.queryDocuments(collection._self, filterQuery).toArrayAsync();
        .then(function(queryResponse) {
            var queryResponseDocuments = queryResponse.feed;
        }, function(error) {
            console.log("Error");
        });

### <a name="unregistering-a-udf"></a>取消註冊 UDF
只要對現有 UDF 資源發出 HTTP DELETE，即可取消註冊 UDF。  

    client.deleteUserDefinedFunctionAsync(createdUdf._self)
        .then(function(response) {
            return;
        }, function(error) {
            console.log("Error");
        });

雖然上述 hello 片段顯示 hello 註冊 (POST)、 取消註冊 (PUT)、 讀取/列出 (GET) 和執行 (POST) 透過 hello [JavaScript SDK](https://github.com/Azure/azure-documentdb-js)，您也可以使用 hello [REST Api](/rest/api/documentdb/)或其他[用戶端 Sdk](documentdb-sdk-dotnet.md)。 

## <a name="documents"></a>文件
您可以在集合中插入、取代、刪除、讀取、列舉和查詢任意 JSON 文件。 Cosmos DB 不會要求任何結構描述，而且不需要在順序 toosupport 查詢集合中的文件上的次要索引。 hello 文件的大小上限為 2 MB。   

Cosmos DB 是真正開放的資料庫服務，不會發明 JSON 文件的任何特殊資料類型 (例如日期時間) 或特定編碼。 請注意 Cosmos DB 不需要任何特殊 JSON 慣例 toocodify hello 之間的關聯性各種文件。hello Cosmos DB SQL 語法提供強大的階層式和關聯式查詢運算子 tooquery 和專案的文件，而不需要任何特殊的註解或文件使用辨別的屬性之間需要 toocodify 關聯性。  

與所有其他資源，可以建立文件，取代、 刪除、 讀取、 列舉和輕鬆地使用 REST Api 或任何 hello 查詢[用戶端 Sdk](documentdb-sdk-dotnet.md)。 刪除文件會立即釋出 hello 配額對應 tooall 的巢狀的 hello 附件。 hello 讀取的文件的一致性層級會遵循 hello 一致性原則的 hello 資料庫帳戶。 根據您應用程式的資料一致性需求，可以覆寫每個要求的這個原則。 當查詢文件，hello 讀取一致性如下所示 hello 索引 hello 集合上設定的模式。 對於 「 一致性 」，這會遵循 hello 帳戶一致性原則。 

## <a name="attachments-and-media"></a>附件和媒體
Cosmos DB 可讓您 toostore 二進位 blob/媒體 Cosmos DB （每個帳戶最多 2 gb） 或 tooyour 自己的遠端媒體存放區。 它也可讓您的媒體稱為附件的特殊文件方面的 toorepresent hello 中繼資料。 附件 Cosmos DB 中的參考 hello 媒體 /blob 儲存其他地方的特殊 (JSON) 文件。 附件的只是特殊文件，擷取 hello 中繼資料 （例如位置、 作者等） 的遠端媒體儲存體中儲存媒體。 

請考慮使用 Cosmos DB toostore 筆跡註釋，社交讀取應用程式和中繼資料包括註解，反白顯示，書籤、 分級、 類似 dislikes 等相關聯的特定使用者的電子書。   

* hello hello 活頁簿本身的內容會儲存在 hello 媒體儲存體是可從 Cosmos DB 資料庫帳戶的一部分或遠端媒體存放區。 
* 應用程式可能會將每個使用者的中繼資料儲存為不同的文件 (例如 Joe 的 book1 中繼資料儲存在 /colls/joe/docs/book1 所參考的文件中)。 
* 指向 toohello 內容頁面的使用者指定書籍的附件儲存在 hello 對應文件例如 /colls/joe/docs/book1/chapter1 /colls/joe/docs/book1/chapter2 等等。 

請注意，上面所列的 hello 範例會使用易記識別碼 tooconvey hello 資源階層。 透過 hello REST Api，透過唯一的資源 id 所存取的資源。 

Hello Cosmos DB 受的媒體，hello 附件 hello _media 屬性會參考 hello 媒體依其 URI。 Cosmos DB 將可確保 toogarbage 收集 hello 媒體時卸除所有 hello 未完成的參考。 Cosmos DB 自動上傳 hello 新的媒體時，會產生 hello 附件，並於其中填入 hello _media toopoint toohello 新增的媒體。 如果您選擇 toostore hello 媒體受您 （例如 OneDrive，Azure 儲存體、 DropBox 等） 的遠端 blob 存放區中，您仍然可以使用 附件 tooreference hello 媒體。 在此情況下，您會自行建立 hello 附件，並擴展其 _media 屬性。   

如同所有其他資源，附件可以建立、 取代、 刪除、 讀取或列舉輕鬆地使用 REST Api 或任何 hello 用戶端 Sdk。 文件，與 hello 讀取附件的一致性層級會遵循 hello 一致性原則的 hello 資料庫帳戶。 根據您應用程式的資料一致性需求，可以覆寫每個要求的這個原則。 查詢時的附件，hello 讀取一致性如下所示 hello 索引 hello 集合上設定的模式。 對於 「 一致性 」，這會遵循 hello 帳戶一致性原則。 
 

## <a name="users"></a>使用者
Cosmos DB 使用者代表用於分組權限的邏輯命名空間。 Cosmos DB 使用者可能對應 tooa 使用者的身分識別管理系統或預先定義的應用程式角色。 Cosmos DB 使用者只代表抽象 toogroup 資料庫下的權限集。   

實作多租用戶應用程式中，您可以在 Cosmos DB 對應 tooyour 實際使用者或應用程式的 hello 租用戶中建立使用者。 然後，您可以建立針對指定的使用者對應 toohello 各種集合、 文件、 附件和其他內容的存取控制的權限。   

為您的應用程式需要與使用者成長 tooscale，可以採用不同的方式 tooshard 您的資料。 您可以建立每位使用者的模型，如下所示：   

* 每個使用者對應 tooa 資料庫。
* 每個使用者對應 tooa 集合。 
* 文件對應 toomultiple 使用者移 tooa 專用的集合。 
* 文件對應 toomultiple 使用者移 tooa 組集合。   

不論您選擇的 hello 特定分區化策略，您可以建立實際使用者模型為 Cosmos DB 資料庫中的使用者，並沒問題的更細緻權限 tooeach 使用者建立關聯。  

![使用者集合][3]  
**分區化策略和模型化使用者**

如同其他資源，Cosmos DB 中的使用者可以建立、 取代、 刪除、 讀取或列舉輕鬆地使用 REST Api 或任何 hello 用戶端 Sdk。 Cosmos DB 一定會提供強式一致性的讀取或查詢 hello 中繼資料的使用者資源。 很值得，自動刪除使用者可確保您無法存取任何內含的 hello 權限。 即使 hello Cosmos DB 一部分 hello 刪除使用者 hello 背景回收 hello hello 使用權限配額，hello 刪除權限為可用立即再次您 toouse。  

## <a name="permissions"></a>權限
從存取控制觀點來看，系統會將資源 (例如資料庫帳戶、資料庫、使用者和權限) 視為「管理」  資源，因為這些都需要管理權限。 在 hello 另一方面資源包括 hello 集合、 文件、 附件、 預存程序、 觸發程序和 Udf 為範圍下指定的資料庫，並視為*應用程式資源*。 對應的資源與 hello 角色存取它們 （也就是 hello 系統管理員和使用者） 的 toohello 兩種類型的 hello 授權模型會定義兩種類型的*存取金鑰*:*主要金鑰*和*資源索引鍵*。 hello 主要金鑰屬於 hello 資料庫帳戶和 toohello 開發人員 （或管理員） 提供者佈建 hello 資料庫帳戶。 此主要金鑰具有系統管理員語意，可以使用的 tooauthorize 存取 tooboth 系統管理和應用程式資源。 資源索引鍵相較之下，會允許存取 tooa 細微的存取金鑰*特定*應用程式資源。 因此，它會擷取 hello hello 使用者的資料庫之間的關聯性，hello 權限 hello 使用者擁有特定資源 （例如集合、 文件、 附件、 預存程序、 觸發程序或 UDF）。   

hello 唯一方式 tooobtain 資源索引鍵是建立在指定的使用者權限資源。 請注意，在訂單 toocreate 或擷取權限、 主要金鑰必須呈現 hello 授權標頭中。 權限資源繫結合作對 hello 資源、 存取和 hello 使用者。 建立權限資源之後, hello 使用者只需要 toopresent hello 相關聯的資源索引鍵順序 toogain 存取 toohello 相關資源。 因此，資源索引鍵可視為邏輯和 compact hello 權限資源的表示方式。  

如同所有其他資源，Cosmos DB 中的權限可以建立、 取代、 刪除、 讀取或列舉輕鬆地使用 REST Api 或任何 hello 用戶端 Sdk。 Cosmos DB 一定會提供強式一致性的讀取或查詢 hello 中繼資料的權限。 

## <a name="next-steps"></a>後續步驟
深入了解如何使用 HTTP 命令來使用資源，請參閱[與 Cosmos DB 資源進行 RESTful 互動 (英文)](https://msdn.microsoft.com/library/azure/mt622086.aspx)。

[1]: media/documentdb-resources/resources1.png
[2]: media/documentdb-resources/resources2.png
[3]: media/documentdb-resources/resources3.png

