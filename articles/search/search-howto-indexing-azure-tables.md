---
title: "Azure 資料表儲存體與 Azure 搜尋 aaaIndexing |Microsoft 文件"
description: "了解 tooindex 資料如何儲存在 Azure 資料表儲存體與 Azure 搜尋"
services: search
documentationcenter: 
author: chaosrealm
manager: pablocas
editor: 
ms.assetid: 1cc27411-d0cc-40ed-8aed-c7cb9ab402b9
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 04/10/2017
ms.author: eugenesh
ms.openlocfilehash: abb01a4d807cede310246b34775d8059fceb4456
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="index-azure-table-storage-with-azure-search"></a>使用 Azure 搜尋服務對 Azure 表格儲存體編制索引
這篇文章會示範如何 toouse Azure 搜尋 tooindex 資料儲存在 Azure 資料表儲存體。

## <a name="set-up-azure-table-storage-indexing"></a>設定 Azure 表格儲存體編制索引

您可以使用下列資源設定 Azure 表格儲存體索引子︰

* [Azure 入口網站](https://ms.portal.azure.com)
* Azure 搜尋服務 [REST API](https://docs.microsoft.com/rest/api/searchservice/Indexer-operations)
* Azure 搜尋服務 [.NET SDK](https://aka.ms/search-sdk)

這裡我們使用 hello REST API 示範 hello 流程。 

### <a name="step-1-create-a-datasource"></a>步驟 1：建立資料來源

資料來源指定哪些資料 tooindex、 hello 需要認證 tooaccess hello 資料，並可讓 Azure 搜尋 tooefficiently hello 原則識別 hello 資料中的變更。

資料表索引，hello 資料來源必須具有下列屬性的 hello:

- **名稱**是 hello hello 搜尋服務中的資料來源的唯一名稱。
- **類型**必須是 `azuretable`。
- **認證**參數包含 hello 儲存體帳戶連接字串。 請參閱 hello[指定認證](#Credentials)如需詳細資訊。
- **容器**集 hello 資料表名稱和選擇性的查詢。
    - 指定 hello 資料表名稱使用 hello`name`參數。
    - （選擇性） 指定查詢使用 hello`query`參數。 

> [!IMPORTANT] 
> 可能的話，在 Partitionkey 使用篩選以提升效能。 任何其他查詢會進行完整的資料表掃描，導致大型資料表的效能不佳。 請參閱 hello[效能考量](#Performance)> 一節。


toocreate 資料來源：

    POST https://[service name].search.windows.net/datasources?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
        "name" : "table-datasource",
        "type" : "azuretable",
        "credentials" : { "connectionString" : "DefaultEndpointsProtocol=https;AccountName=<account name>;AccountKey=<account key>;" },
        "container" : { "name" : "my-table", "query" : "PartitionKey eq '123'" }
    }   

如需有關 hello 建立資料來源應用程式開發介面的詳細資訊，請參閱[建立資料來源](https://docs.microsoft.com/rest/api/searchservice/create-data-source)。

<a name="Credentials"></a>
#### <a name="ways-toospecify-credentials"></a>方式 toospecify 認證 ####

您可以在其中一種方式中的 hello 資料表提供 hello 認證： 

- **完整存取儲存體帳戶連接字串**:`DefaultEndpointsProtocol=https;AccountName=<your storage account>;AccountKey=<your account key>`您可以取得 hello 連接字串從 hello Azure 入口網站移 toohello**儲存體帳戶 刀鋒視窗** > **設定**  > **金鑰**（適用於傳統儲存體帳戶） 或**設定** > **存取金鑰**（適用於 Azure 資源管理員儲存體帳戶）。
- **共用存取簽章的連接字串儲存體帳戶**: `TableEndpoint=https://<your account>.table.core.windows.net/;SharedAccessSignature=?sv=2016-05-31&sig=<hello signature>&spr=https&se=<hello validity end time>&srt=co&ss=t&sp=rl` hello 共用的存取簽章應有 hello 清單和讀取權限 （在此情況下的表格） 的容器和物件 （資料表資料列）。
-  **資料表的共用的存取簽章**: `ContainerSharedAccessUri=https://<your storage account>.table.core.windows.net/<table name>?tn=<table name>&sv=2016-05-31&sig=<hello signature>&se=<hello validity end time>&sp=r` hello 共用的存取簽章應具備 hello 資料表上的查詢 （讀取） 權限。

如需儲存體共用存取簽章的詳細資訊，請參閱[使用共用存取簽章](../storage/common/storage-dotnet-shared-access-signature-part-1.md)。

> [!NOTE]
> 如果您使用共用的存取簽章憑證，您必須定期與更新的簽章 tooprevent tooupdate hello 資料來源的認證其到期時間。 如果共用的存取簽章憑證過期，hello 索引子失敗並出現錯誤訊息類似太"hello 連接字串中提供的認證無效或已過期。 」  

### <a name="step-2-create-an-index"></a>步驟 2：建立索引
hello 索引文件，hello 屬性中指定 hello 欄位，和其他建構該圖形 hello 搜尋經驗。

toocreate 索引：

    POST https://[service name].search.windows.net/indexes?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
          "name" : "my-target-index",
          "fields": [
            { "name": "key", "type": "Edm.String", "key": true, "searchable": false },
            { "name": "SomeColumnInMyTable", "type": "Edm.String", "searchable": true }
          ]
    }

如需建立索引的詳細資訊，請參閱[建立索引](https://docs.microsoft.com/rest/api/searchservice/create-index)。

### <a name="step-3-create-an-indexer"></a>步驟 3：建立索引子
索引子連接的資料來源與目標搜尋索引，並提供排程 tooautomate hello 資料重新整理。 

建立 hello 索引和資料來源之後，您便準備好 toocreate hello 索引子：

    POST https://[service name].search.windows.net/indexers?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
      "name" : "table-indexer",
      "dataSourceName" : "table-datasource",
      "targetIndexName" : "my-target-index",
      "schedule" : { "interval" : "PT2H" }
    }

這個索引子會每隔兩小時執行一次。 (hello 排程間隔設定得 「 PT2H"。)索引子 toorun 每隔 30 分鐘、 設定 hello 間隔太"PT30M"。 hello 最短支援的間隔為 5 分鐘。 hello 排程是選擇性的。如果省略，則索引子會執行一次建立時。 不過，您隨時都可依需求執行索引子。   

如需有關 hello 建立索引子 API 的詳細資訊，請參閱[建立索引子](https://docs.microsoft.com/rest/api/searchservice/create-indexer)。

## <a name="deal-with-different-field-names"></a>處理不同的欄位名稱
有時候，您現有的索引中的 hello 欄位名稱會與不同資料表中的 hello 屬性名稱。 您可以使用欄位對應 toomap hello 屬性名稱從 hello 資料表 toohello 欄位名稱中搜尋索引。 toolearn 詳細資料欄位對應，請參閱[Azure 搜尋索引子的欄位對應的橋接 hello datasources 和搜尋索引之間的差異](search-indexer-field-mappings.md)。

## <a name="handle-document-keys"></a>處理文件索引鍵
在 Azure 搜尋 hello 文件索引鍵會唯一識別文件。 每個搜尋索引必須確實具有一個 `Edm.String`類型的索引鍵欄位。 正在加入 toohello 索引每份文件需要 hello 索引鍵欄位。 （事實上，它的 hello 只需具備欄位）。

因為資料表資料列有複合索引鍵，Azure 搜尋服務會產生名為 `Key` 的綜合欄位，該欄位為資料分割索引鍵與資料列索引鍵值的串連。 例如，如果資料列的 PartitionKey 是`PK1`和 RowKey 是`RK1`，然後 hello`Key`欄位的值是`PK1RK1`。

> [!NOTE]
> hello`Key`值可能包含文件索引鍵，例如虛線中無效的字元。 您可以使用 hello 處理無效的字元`base64Encode`[欄位對應的函式](search-indexer-field-mappings.md#base64EncodeFunction)。 如果您這樣做，請記得 tooalso 使用 URL 安全 Base64 編碼，例如查閱文件索引鍵傳入應用程式開發介面呼叫時。
>
>

## <a name="incremental-indexing-and-deletion-detection"></a>增量編製索引和刪除偵測
當您設定資料表索引子 toorun 排程時，它會 reindexes 只有新的或更新資料列，一個資料列所決定`Timestamp`值。 您不需要 toospecify 變更偵測原則。 系統會自動為您啟用增量編制索引。

tooindicate 某些必須從 hello 索引中移除文件，您可以使用虛刪除的策略。 不刪除資料列，以新增屬性 tooindicate 它刪除，並設定 hello 資料來源上虛刪除偵測原則。 例如，下列原則 hello 考慮是否 hello 資料列的屬性，就會刪除資料列`IsDeleted`hello 值`"true"`:

    PUT https://[service name].search.windows.net/datasources?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
        "name" : "my-table-datasource",
        "type" : "azuretable",
        "credentials" : { "connectionString" : "<your storage connection string>" },
        "container" : { "name" : "table name", "query" : "<query>" },
        "dataDeletionDetectionPolicy" : { "@odata.type" : "#Microsoft.Azure.Search.SoftDeleteColumnDeletionDetectionPolicy", "softDeleteColumnName" : "IsDeleted", "softDeleteMarkerValue" : "true" }
    }   

<a name="Performance"></a>
## <a name="performance-considerations"></a>效能考量

根據預設，Azure 搜尋會使用下列查詢篩選器的 hello: `Timestamp >= HighWaterMarkValue`。 因為 Azure 資料表不需要次要索引上 hello`Timestamp`欄位，這種類型的查詢需要完整資料表掃描，因此對於大型資料表變慢。


以下是加強資料表索引效能兩個可能的做法。 這兩種做法都依賴使用資料表資料分割︰ 

- 如果您的資料可以自然地分割成幾個資料分割範圍，請建立資料來源以及與每個資料分割範圍對應的索引子。 每個索引子現在有 tooprocess 只有特定資料分割範圍，導致更好的查詢效能。 如果需要 toobe 編製索引的 hello 資料有少量固定的資料分割，甚至更好： 每個索引子，才會執行資料分割掃描。 例如，toocreate 處理分割區範圍與資料來源索引鍵從`000`太`100`，使用類似的查詢： 
    ```
    "container" : { "name" : "my-table", "query" : "PartitionKey ge '000' and PartitionKey lt '100' " }
    ```

- 如果您的資料依時間分割 （例如，建立新的磁碟分割每一天或週），請考慮遵循方法 hello: 
    - 使用 hello 形式的查詢： `(PartitionKey ge <TimeStamp>) and (other filters)`。 
    - 監視使用的索引子進度[取得索引子狀態 API](https://docs.microsoft.com/rest/api/searchservice/get-indexer-status)，並定期更新 hello `<TimeStamp>` hello 查詢是根據 hello 最新成功高上限標記值的條件。 
    - 使用此方法時，如果您需要 tootrigger 完整重新索引，您需要 tooreset hello 資料來源查詢中加入 tooresetting hello 索引子。 


## <a name="help-us-make-azure-search-better"></a>協助我們改進 Azure 搜尋服務
如果您有功能要求或改進的想法，請在我們的 [UserVoice 網站](https://feedback.azure.com/forums/263029-azure-search/)提出。
