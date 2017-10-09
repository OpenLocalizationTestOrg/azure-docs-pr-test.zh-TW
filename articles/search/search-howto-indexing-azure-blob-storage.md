---
title: "aaaIndexing Azure Blob 儲存體與 Azure 搜尋"
description: "了解如何 tooindex Azure Blob 儲存體和擷取的文字文件使用 Azure 搜尋"
services: search
documentationcenter: 
author: chaosrealm
manager: pablocas
editor: 
ms.assetid: 2a5968f4-6768-4e16-84d0-8b995592f36a
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 07/22/2017
ms.author: eugenesh
ms.openlocfilehash: 1bdd34e66a4a9192ed88cacbc7b8456d0dcdfeb6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="indexing-documents-in-azure-blob-storage-with-azure-search"></a>使用 Azure 搜尋服務在 Azure Blob 儲存體中對文件編制索引
本文將說明如何 toouse Azure 搜尋 tooindex 文件 (例如 Pdf、 Microsoft Office 文件和許多其他常見的格式) 儲存在 Azure Blob 儲存體。 首先，它會說明安裝及設定 blob 的索引子的 hello 基本的概念。 然後，它可提供行為與案例，您都可能 tooencounter 更深入瀏覽。

## <a name="supported-document-formats"></a>支援的文件格式
hello blob 索引子可以擷取下列文件格式的 hello 文字：

* PDF
* Microsoft Office 格式：DOCX/DOC、XLSX/XLS、PPTX/PPT、MSG (Outlook 電子郵件)  
* HTML
* XML
* ZIP
* EML
* RTF
* 純文字檔案 (另請參閱[編制純文字的索引](#IndexingPlainText))
* JSON (請參閱[編製 JSON Blob 的索引](search-howto-index-json-blobs.md))
* CSV (請參閱[編製 CSV Blob 的索引](search-howto-index-csv-blobs.md) 預覽功能)

> [!IMPORTANT]
> CSV 和 JSON 的陣列支援目前屬於預覽功能。 這些格式是只使用版**2016年-09-01-預覽**的 hello REST API 或版本 2.x 預覽的 hello.NET SDK。 請記住，預覽 API 是針對測試與評估，不應該用於生產環境。
>
>

## <a name="setting-up-blob-indexing"></a>設定 blob 編製索引
您可以使用下列項目設定 Azure Blob 儲存體索引子︰

* [Azure 入口網站](https://ms.portal.azure.com)
* Azure 搜尋服務 [REST API](https://docs.microsoft.com/rest/api/searchservice/Indexer-operations)
* Azure 搜尋服務 [.NET SDK](https://aka.ms/search-sdk)

> [!NOTE]
> 某些功能 （例如，欄位對應） 尚無法使用在 hello 入口網站，而且提供 toobe 以程式設計方式使用。
>
>

在這裡，我們會示範使用 hello REST API 的 hello 流程。

### <a name="step-1-create-a-data-source"></a>步驟 1：建立資料來源
資料來源會指定哪些資料 tooindex、 所需認證 tooaccess hello 資料，以及原則 tooefficiently 識別 hello 資料 （新增、 修改或刪除資料列） 中的變更。 使用資料來源的多個索引子在 hello 相同搜尋服務。

對於 blob 編製索引 hello 資料來源必須包含下列必要的屬性的 hello:

* **名稱**是 hello hello 搜尋服務中的資料來源的唯一名稱。
* **類型**必須是 `azureblob`。
* **認證**提供 hello 儲存體帳戶連接字串 hello 做`credentials.connectionString`參數。 請參閱[如何 toospecify 認證](#Credentials)下方如需詳細資訊。
* **容器**會指定儲存體帳戶中的容器。 根據預設，hello 容器內的所有 blob 都都可擷取。 如果您只想在特定的虛擬目錄中的 tooindex blob，您可以指定使用選用的 hello 該目錄**查詢**參數。

toocreate 資料來源：

    POST https://[service name].search.windows.net/datasources?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
        "name" : "blob-datasource",
        "type" : "azureblob",
        "credentials" : { "connectionString" : "DefaultEndpointsProtocol=https;AccountName=<account name>;AccountKey=<account key>;" },
        "container" : { "name" : "my-container", "query" : "<optional-virtual-directory-name>" }
    }   

如需 hello 建立資料來源應用程式開發介面的詳細資訊，請參閱[建立資料來源](https://docs.microsoft.com/rest/api/searchservice/create-data-source)。

<a name="Credentials"></a>
#### <a name="how-toospecify-credentials"></a>如何 toospecify 認證 ####

您可以提供一種方式中的 hello blob 容器的 hello 認證：

- **完整存取儲存體帳戶連接字串**：`DefaultEndpointsProtocol=https;AccountName=<your storage account>;AccountKey=<your account key>`。 您可以從 hello Azure 入口網站瀏覽 toohello 儲存體帳戶 刀鋒視窗來取得 hello 連接字串 > 的設定 > （適用於傳統儲存體帳戶） 的索引鍵或設定 > 存取金鑰 （適用於 Azure Resource Manager 儲存體帳戶）。
- **儲存體帳戶的共用的存取簽章**(SAS) 連接字串： `BlobEndpoint=https://<your account>.blob.core.windows.net/;SharedAccessSignature=?sv=2016-05-31&sig=<hello signature>&spr=https&se=<hello validity end time>&srt=co&ss=b&sp=rl` hello SAS 應有 hello 清單和讀取容器和物件的權限 (在此情況下 blob)。
-  **容器的共用的存取簽章**: `ContainerSharedAccessUri=https://<your storage account>.blob.core.windows.net/<container name>?sv=2016-05-31&sr=c&sig=<hello signature>&se=<hello validity end time>&sp=rl` hello SAS 應有 hello 清單和讀取 hello 容器的權限。

如需儲存體共用存取簽章的詳細資訊，請參閱[使用共用存取簽章](../storage/common/storage-dotnet-shared-access-signature-part-1.md)。

> [!NOTE]
> 如果您使用 SAS 認證時，您必須定期與更新的簽章 tooprevent tooupdate hello 資料來源認證其到期時間。 如果 SAS 認證過期，hello 索引子將會失敗並出現類似的錯誤訊息太`Credentials provided in hello connection string are invalid or have expired.`。  

### <a name="step-2-create-an-index"></a>步驟 2：建立索引
hello 索引指定 hello 欄位中的文件屬性，以及其他建構該圖形 hello 搜尋經驗。

以下是如何 toocreate 具有可搜尋的索引`content`欄位從 blob 擷取 toostore hello 文字：   

    POST https://[service name].search.windows.net/indexes?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
          "name" : "my-target-index",
          "fields": [
            { "name": "id", "type": "Edm.String", "key": true, "searchable": false },
            { "name": "content", "type": "Edm.String", "searchable": true, "filterable": false, "sortable": false, "facetable": false }
          ]
    }

如需建立索引的詳細資訊，請參閱[建立索引](https://docs.microsoft.com/rest/api/searchservice/create-index)

### <a name="step-3-create-an-indexer"></a>步驟 3：建立索引子
索引子連接的資料來源與目標搜尋索引，並提供排程 tooautomate hello 資料重新整理。

一旦已建立 hello 索引和資料來源，就要準備好 toocreate hello 索引子：

    POST https://[service name].search.windows.net/indexers?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
      "name" : "blob-indexer",
      "dataSourceName" : "blob-datasource",
      "targetIndexName" : "my-target-index",
      "schedule" : { "interval" : "PT2H" }
    }

這個索引子會執行每隔兩小時 (排程間隔設定得 「 PT2H")。 索引子 toorun 每隔 30 分鐘、 設定 hello 間隔太"PT30M"。 hello 最短支援的間隔是 5 分鐘。 hello 排程是選用-如果省略，索引子會執行一次建立時。 不過，您隨時都可依需求執行索引子。   

如需有關 hello 建立索引子 API，請簽出[建立索引子](https://docs.microsoft.com/rest/api/searchservice/create-indexer)。

## <a name="how-azure-search-indexes-blobs"></a>Azure 搜尋服務如何編製 blob 的索引

根據 hello [indexer 組態](#PartsOfBlobToIndex)，hello blob 索引子可以編製索引只儲存中繼資料 (當您只有照顧大約 hello 中繼資料，而且不需要 tooindex 時很有用 hello blob 的內容)，儲存和內容的中繼資料，或兩者中繼資料和文字內容。 根據預設，hello 索引子會擷取中繼資料和內容。

> [!NOTE]
> 根據預設，結構化內容 (例如 JSON 或CSV) 的 Blob 會以單一區塊文字編製索引。 如果您想 tooindex JSON 和 CSV blob 結構化的方式，請參閱[索引 JSON blob](search-howto-index-json-blobs.md)和[編製索引的 CSV blob](search-howto-index-csv-blobs.md)預覽功能。
>
> 複合或內嵌文件 (例如 ZIP 封存或具有內嵌 Outlook 電子郵件 (內含附件) 的 Word 文件) 也會編制索引為單一文件。

* hello 文件的 hello 文字內容擷取至名為的字串欄位`content`。

> [!NOTE]
> Azure 搜尋會限制它根據 hello 定價層會擷取多少文字： 32000 個字元的免費層，64000 basic，以及 4 百萬 Standard、 Standard S2 和 S3 標準層。 警告會包含在 hello 截斷的文件的索引子狀態回應。  

* 使用者指定的中繼資料屬性出現在 hello blob 上如果有的話，會擷取逐字。
* 標準 blob 中繼資料屬性會被擷取到 hello 下列欄位：

  * **中繼資料\_儲存體\_名稱**(Edm.String)-hello hello blob 檔案名稱。 例如，如果您有 blob /my-container/my-folder/subfolder/resume.pdf，hello 這個欄位的值是`resume.pdf`。
  * **中繼資料\_儲存體\_路徑**(Edm.String)-hello hello blob，包括 hello 儲存體帳戶的完整 URI。 例如， `https://myaccount.blob.core.windows.net/my-container/my-folder/subfolder/resume.pdf`
  * **中繼資料\_儲存體\_內容\_類型**(Edm.String)-hello 程式碼所指定的內容類型使用 tooupload hello blob。 例如： `application/octet-stream`。
  * **中繼資料\_儲存體\_最後\_修改**(Edm.DateTimeOffset)-上次修改時間戳記 hello blob。 Azure 搜尋會使用此時間戳記變更 tooidentify blob tooavoid 重新 hello 初始建立索引之後的所有項目。
  * **metadata\_storage\_size** (Edm.Int64) - blob 大小 (位元組)。
  * **中繼資料\_儲存體\_內容\_md5** (Edm.String) 的 MD5 雜湊 hello blob 內容，如果有的話。
* 中繼資料屬性特定 tooeach 文件格式會被擷取到所列的 hello 欄位[這裡](#ContentSpecificMetadata)。

您不需要 toodefine 欄位 hello 屬性上方的所有搜尋索引中，只擷取您的應用程式所需的 hello 屬性。

> [!NOTE]
> 通常，您現有的索引中的 hello 欄位名稱會不同於在文件擷取期間所產生的 hello 欄位名稱。 您可以使用**欄位對應**toomap hello 屬性名稱中搜尋索引的 Azure 搜尋 toohello 欄位名稱所提供。 您會在下面看到使用欄位對應的範例。
>
>

<a name="DocumentKeys"></a>
### <a name="defining-document-keys-and-field-mappings"></a>定義文件索引鍵和欄位對應
在 Azure 搜尋 hello 文件索引鍵會唯一識別文件。 每個搜尋索引必須確實具有一個 Edm.String 類型的索引鍵欄位。 正在 toohello 索引 （它是實際 hello 唯一必要的欄位） 加入每份文件需要 hello 索引鍵欄位。  

您應該仔細考量哪一個擷取的欄位應該對應 toohello 索引鍵欄位，您的索引。 hello 的候選方式為：

* **中繼資料\_儲存體\_名稱**-這可能是方便的候選項目，但是請注意，1) hello 名稱可能不是唯一的因為您可能會有相同的名稱，在不同的資料夾中的 hello 的 blob 和 2) hello 名稱可能包含的字元，不適用於文件索引鍵，例如連字號。 您可以使用 hello 處理無效的字元`base64Encode`[欄位對應的函式](search-indexer-field-mappings.md#base64EncodeFunction)-如果您這樣做，請記住 tooencode 文件索引鍵時查閱例如傳入 API 呼叫。 (例如，在.NET 中您可以使用 hello [UrlTokenEncode 方法](https://msdn.microsoft.com/library/system.web.httpserverutility.urltokenencode.aspx)針對該用途)。
* **中繼資料\_儲存體\_路徑**-使用 hello 完整路徑，以確保唯一性，但 hello 路徑明確包含`/`字元[無效文件索引鍵中](https://docs.microsoft.com/rest/api/searchservice/naming-rules)。  如前所述，您擁有 hello 選項的編碼使用 hello hello 金鑰`base64Encode`[函式](search-indexer-field-mappings.md#base64EncodeFunction)。
* 如果任何上述的 hello 選項為您的工作，您可以加入自訂中繼資料屬性 toohello blob。 此選項，不過，需要您的 blob 上傳程序 tooadd 該中繼資料屬性 tooall blob。 Hello 索引鍵是必要的屬性，因為沒有該屬性的所有 blob 會都失敗 toobe 編製索引。

> [!IMPORTANT]
> 如果沒有明確的 hello hello 索引中的索引鍵欄位對應，Azure 搜尋會自動使用`metadata_storage_path`為 hello 和 base 64 編碼的索引鍵值 （hello 第二個選項上述）。
>
>

例如，讓我們挑選 hello `metadata_storage_name` hello 文件索引鍵欄位。 我們也假設您的索引具有索引鍵欄位，名為`key`和欄位`fileSize`儲存 hello 文件大小。 toowire 進行視需要指定下列欄位對應時建立或更新您的索引子的 hello:

    "fieldMappings" : [
      { "sourceFieldName" : "metadata_storage_name", "targetFieldName" : "key", "mappingFunction" : { "name" : "base64Encode" } },
      { "sourceFieldName" : "metadata_storage_size", "targetFieldName" : "fileSize" }
    ]

toobring 整體而言，這裡的如何新增欄位對應，並啟用 base 64 編碼的現有的索引子的索引鍵：

    PUT https://[service name].search.windows.net/indexers/blob-indexer?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
      "dataSourceName" : " blob-datasource ",
      "targetIndexName" : "my-target-index",
      "schedule" : { "interval" : "PT2H" },
      "fieldMappings" : [
        { "sourceFieldName" : "metadata_storage_name", "targetFieldName" : "key", "mappingFunction" : { "name" : "base64Encode" } },
        { "sourceFieldName" : "metadata_storage_size", "targetFieldName" : "fileSize" }
      ]
    }

> [!NOTE]
> toolearn 詳細資料欄位對應，請參閱[本文](search-indexer-field-mappings.md)。
>
>

<a name="WhichBlobsAreIndexed"></a>
## <a name="controlling-which-blobs-are-indexed"></a>控制要編製哪些 blob 的索引
您可以控制要編製哪些 blob 的索引，以及哪些要略過。

### <a name="index-only-hello-blobs-with-specific-file-extensions"></a>索引只具有特定副檔名的 hello blob
您可以建立索引 hello 檔案名稱副檔名，而您使用 hello 指定唯一的 hello blob`indexedFileNameExtensions`索引子 」 組態參數。 hello 值為字串，包含以逗號分隔的副檔名清單 （以前置句點）。 例如，tooindex 只有 hello。PDF 和。DOCX blob 時，執行下列動作：

    PUT https://[service name].search.windows.net/indexers/[indexer name]?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
      ... other parts of indexer definition
      "parameters" : { "configuration" : { "indexedFileNameExtensions" : ".pdf,.docx" } }
    }

### <a name="exclude-blobs-with-specific-file-extensions"></a>排除具有特定副檔名的 Blob
您可以從使用 hello 索引排除特定副檔名的 blob`excludedFileNameExtensions`組態參數。 hello 值為字串，包含以逗號分隔的副檔名清單 （以前置句點）。 例如，所有 tooindex 都 blob hello 除外。PNG 和。JPEG 擴充功能，執行下列動作：

    PUT https://[service name].search.windows.net/indexers/[indexer name]?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
      ... other parts of indexer definition
      "parameters" : { "configuration" : { "excludedFileNameExtensions" : ".png,.jpeg" } }
    }

如果同時有 `indexedFileNameExtensions` 和 `excludedFileNameExtensions` 參數，Azure 搜尋服務會先查看 `indexedFileNameExtensions`，再查看 `excludedFileNameExtensions`。 這表示，如果 hello 相同的副檔名存在於這兩個清單中，它將會排除編製索引。

### <a name="dealing-with-unsupported-content-types"></a>處理不受支援的內容類型

根據預設，當它遇到不支援的內容類型 （例如影像） 的 blob，就會停止 hello blob 索引子。 當然，您可以使用 hello`excludedFileNameExtensions`參數 tooskip 特定內容類型。 不過，您可能需要 tooindex blob，而不需要事先知道所有 hello 可能的內容類型。 toocontinue 編製索引，當遇到不支援的內容型別時，設定 hello`failOnUnsupportedContentType`組態參數太`false`:

    PUT https://[service name].search.windows.net/indexers/[indexer name]?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
      ... other parts of indexer definition
      "parameters" : { "configuration" : { "failOnUnsupportedContentType" : false } }
    }

### <a name="ignoring-parsing-errors"></a>忽略剖析錯誤

Azure 搜尋文件擷取邏輯並不完美，而且有時候會這類失敗 tooparse 文件支援的內容類型。DOCX 或。PDF。 如果您不想 toointerrupt hello 編製索引，在此情況下，設定 hello`maxFailedItems`和`maxFailedItemsPerBatch`組態參數 toosome 合理的值。 例如：

    {
      ... other parts of indexer definition
      "parameters" : { "maxFailedItems" : 10, "maxFailedItemsPerBatch" : 10 }
    }

<a name="PartsOfBlobToIndex"></a>
## <a name="controlling-which-parts-of-hello-blob-are-indexed"></a>控制 hello blob 的哪些部分會編製索引

您可以控制 hello blob 的哪些部分會編製索引使用 hello`dataToExtract`組態參數。 它可以接受下列值的 hello:

* `storageMetadata`-指定該只有 hello[標準 blob 屬性和使用者指定的中繼資料](../storage/blobs/storage-properties-metadata.md)會編製索引。
* `allMetadata`-指定儲存體的中繼資料和 hello[特定內容類型的中繼資料](#ContentSpecificMetadata)擷取從 hello blob 內容會編製索引。
* `contentAndMetadata`-指定所有的中繼資料和文字內容擷取自 hello blob 會編制索引。 這是 hello 預設值。

例如，tooindex 只有 hello 儲存中繼資料，使用：

    PUT https://[service name].search.windows.net/indexers/[indexer name]?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
      ... other parts of indexer definition
      "parameters" : { "configuration" : { "dataToExtract" : "storageMetadata" } }
    }

### <a name="using-blob-metadata-toocontrol-how-blobs-are-indexed"></a>使用 blob 中繼資料 toocontrol 如何 blob 會編製索引

套用 tooall blob 上面所述的 hello 組態參數。 有時候，您可能會想 toocontrol 如何*個別 blob*會編製索引。 您可以藉由新增 hello 下列 blob 中繼資料屬性和值：

| 屬性名稱 | 屬性值 | 說明 |
| --- | --- | --- |
| AzureSearch_Skip |"true" |指示 hello blob 索引子 toocompletely 略過 hello blob。 不會嘗試擷取中繼資料或內容。 特定的 blob，但是一再失敗和中斷 hello 索引處理程序時，這非常有用。 |
| AzureSearch_SkipContent |"true" |這是相當於`"dataToExtract" : "allMetadata"`設定描述[上方](#PartsOfBlobToIndex)已設定領域的 tooa 特定 blob。 |

## <a name="incremental-indexing-and-deletion-detection"></a>增量編製索引和刪除偵測
當您設定排程 blob 索引子 toorun 時，它重新編製索引僅由 hello blob 的 blob，已變更的 hello`LastModified`時間戳記。

> [!NOTE]
> 您不需要 toospecify 變更偵測原則-累加索引會為您自動啟用。

toosupport 刪除文件，請使用 「 虛刪除 」 方法。 如果您刪除 hello blob 徹底，對應的文件將不會從 hello 搜尋索引。 請改用 hello 下列步驟：  

1. 新增自訂中繼資料屬性 toohello blob tooindicate tooAzure 搜尋以邏輯方式刪除
2. Hello 資料來源上設定虛刪除偵測原則
3. 一旦 hello 索引子具有處理 hello blob （如的 hello 索引子狀態 API 所示），您可以實際刪除 hello blob

例如，下列原則 hello 考慮 blob toobe 刪除有中繼資料屬性`IsDeleted`hello 值`true`:

    PUT https://[service name].search.windows.net/datasources/blob-datasource?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
        "name" : "blob-datasource",
        "type" : "azureblob",
        "credentials" : { "connectionString" : "<your storage connection string>" },
        "container" : { "name" : "my-container", "query" : "my-folder" },
        "dataDeletionDetectionPolicy" : {
            "@odata.type" :"#Microsoft.Azure.Search.SoftDeleteColumnDeletionDetectionPolicy",     
            "softDeleteColumnName" : "IsDeleted",
            "softDeleteMarkerValue" : "true"
        }
    }   

## <a name="indexing-large-datasets"></a>編製索引大型資料集

編製 blob 的索引可能會是耗時的程序。 在您有數百萬個 blob tooindex 的情況下，您可以加速將資料分割，並使用多個索引子 tooprocess hello 資料以平行方式編製索引。 下列是您可以如此設定的方式：

- 將資料分割成多個 blob 容器或虛擬資料夾
- 設定數個 Azure 搜尋服務資料來源，每個容器或資料夾一個。 toopoint tooa blob 資料夾中，使用 hello`query`參數：

    ```
    {
        "name" : "blob-datasource",
        "type" : "azureblob",
        "credentials" : { "connectionString" : "<your storage connection string>" },
        "container" : { "name" : "my-container", "query" : "my-folder" }
    }
    ```

- 針對每個資料來源建立對應的索引子。 所有 hello 索引子可以點 toohello 相同目標搜尋索引。  

- 服務中的單一搜尋單位一次只能執行一個索引子。 以上述方式建立多個索引子，只有在這些索引子都以平行的方式執行時才會有幫助。 toorun 多個索引子以平行方式，向外延展您的搜尋服務藉由建立適當的資料分割和複本數目。 例如，如果您的搜尋服務有 6 個搜尋單位 （例如，2 個資料分割 x 3 複本），然後 6 的索引子可以同時執行，造成 six-fold hello 索引輸送量增加。 toolearn 深入了解縮放比例和容量計劃，請參閱[調整 查詢和索引在 Azure 搜尋中的工作負載的資源層級](search-capacity-planning.md)。

## <a name="indexing-documents-along-with-related-data"></a>為文件及相關資料編製索引

您可能想太 「 組合 」 文件索引中的多個來源。 比方說，您可以從 blob toomerge 文字與 Cosmos DB 中儲存其他中繼資料。 您甚至可以使用的 hello 推送索引 API，以及各種索引子太建置搜尋文件，從多個部分。 

此 toowork，所有索引子和其他元件需要 tooagree hello 文件索引鍵上。 如需詳細的逐步解說，請參閱這篇外部文章：[在 Azure 搜尋服務中將文件與其他資料組合在一起](http://blog.lytzen.name/2017/01/combine-documents-with-other-data-in.html) \(英文\)。

<a name="IndexingPlainText"></a>
## <a name="indexing-plain-text"></a>編制純文字的索引 

如果您的 blob 包含純文字中所有 hello 相同的編碼方式，您可以使用，大幅改善索引效能**文字剖析模式**。 剖析模式中，設定 hello toouse 文字`parsingMode`組態屬性太`text`:

    PUT https://[service name].search.windows.net/indexers/[indexer name]?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
      ... other parts of indexer definition
      "parameters" : { "configuration" : { "parsingMode" : "text" } }
    }

根據預設，hello`UTF-8`則假設編碼方式。 toospecify 不同的編碼，使用 hello`encoding`組態屬性： 

    {
      ... other parts of indexer definition
      "parameters" : { "configuration" : { "parsingMode" : "text", "encoding" : "windows-1252" } }
    }


<a name="ContentSpecificMetadata"></a>
## <a name="content-type-specific-metadata-properties"></a>內容類型特定的中繼資料屬性
hello 下表摘要說明程序完成每個文件格式，並說明 hello Azure 搜尋擷取的中繼資料屬性。

| 文件格式/內容類型 | 內容類型特定的中繼資料屬性 | 處理詳細資料 |
| --- | --- | --- |
| HTML (`text/html`) |`metadata_content_encoding`<br/>`metadata_content_type`<br/>`metadata_language`<br/>`metadata_description`<br/>`metadata_keywords`<br/>`metadata_title` |移除 HTML 標記並且擷取文字 |
| PDF (`application/pdf`) |`metadata_content_type`<br/>`metadata_language`<br/>`metadata_author`<br/>`metadata_title` |擷取文字，包括內嵌文件 (不含影像) |
| DOCX (application/vnd.openxmlformats-officedocument.wordprocessingml.document) |`metadata_content_type`<br/>`metadata_author`<br/>`metadata_character_count`<br/>`metadata_creation_date`<br/>`metadata_last_modified`<br/>`metadata_page_count`<br/>`metadata_word_count` |擷取文字，包括內嵌文件 |
| DOC (application/msword) |`metadata_content_type`<br/>`metadata_author`<br/>`metadata_character_count`<br/>`metadata_creation_date`<br/>`metadata_last_modified`<br/>`metadata_page_count`<br/>`metadata_word_count` |擷取文字，包括內嵌文件 |
| XLSX (application/vnd.openxmlformats-officedocument.spreadsheetml.sheet) |`metadata_content_type`<br/>`metadata_author`<br/>`metadata_creation_date`<br/>`metadata_last_modified` |擷取文字，包括內嵌文件 |
| XLS (application/vnd.ms-excel) |`metadata_content_type`<br/>`metadata_author`<br/>`metadata_creation_date`<br/>`metadata_last_modified` |擷取文字，包括內嵌文件 |
| PPTX (application/vnd.openxmlformats-officedocument.presentationml.presentation) |`metadata_content_type`<br/>`metadata_author`<br/>`metadata_creation_date`<br/>`metadata_last_modified`<br/>`metadata_slide_count`<br/>`metadata_title` |擷取文字，包括內嵌文件 |
| PPT (application/vnd.ms-powerpoint) |`metadata_content_type`<br/>`metadata_author`<br/>`metadata_creation_date`<br/>`metadata_last_modified`<br/>`metadata_slide_count`<br/>`metadata_title` |擷取文字，包括內嵌文件 |
| MSG (application/vnd.ms-outlook) |`metadata_content_type`<br/>`metadata_message_from`<br/>`metadata_message_to`<br/>`metadata_message_cc`<br/>`metadata_message_bcc`<br/>`metadata_creation_date`<br/>`metadata_last_modified`<br/>`metadata_subject` |擷取文字，包括附件 |
| ZIP (application/zip) |`metadata_content_type` |從 hello 封存中的所有文件中擷取文字 |
| XML (application/xml) |`metadata_content_type`</br>`metadata_content_encoding`</br> |移除 XML 標記並且擷取文字 |
| JSON (application/json) |`metadata_content_type`</br>`metadata_content_encoding` |擷取文字<br/>注意： 如果您需要的 tooextract 多重文件欄位從 JSON blob，請參閱[索引 JSON blob](search-howto-index-json-blobs.md)如需詳細資訊 |
| EML (message/rfc822) |`metadata_content_type`<br/>`metadata_message_from`<br/>`metadata_message_to`<br/>`metadata_message_cc`<br/>`metadata_creation_date`<br/>`metadata_subject` |擷取文字，包括附件 |
| RTF (應用程式/rtf) |`metadata_content_type`</br>`metadata_author`</br>`metadata_character_count`</br>`metadata_creation_date`</br>`metadata_page_count`</br>`metadata_word_count`</br> | 擷取文字|
| 純文字 (text/plain) |`metadata_content_type`</br>`metadata_content_encoding`</br> | 擷取文字|


## <a name="help-us-make-azure-search-better"></a>協助我們改進 Azure 搜尋服務
如果您有功能要求或改進的想法，請在我們的 [UserVoice 網站](https://feedback.azure.com/forums/263029-azure-search/)與我們連絡。
