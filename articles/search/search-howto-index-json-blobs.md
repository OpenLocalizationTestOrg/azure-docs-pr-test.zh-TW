---
title: "Azure 搜尋 blob 索引子的 aaaIndexing JSON blob"
description: "使用 Azure 搜尋服務 Blob 索引子編製索引 JSON Blob"
services: search
documentationcenter: 
author: chaosrealm
manager: pablocas
editor: 
ms.assetid: 57e32e51-9286-46da-9d59-31884650ba99
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 04/10/2017
ms.author: eugenesh
ms.openlocfilehash: 269968714358cd40ea66863b4dbb97766e1d77e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="indexing-json-blobs-with-azure-search-blob-indexer"></a>使用 Azure 搜尋服務 Blob 索引子編製索引 JSON Blob
本文示範 tooconfigure Azure 搜尋 blob 索引子 tooextract 結構從包含 JSON 的 blob 內容的方式。

## <a name="scenarios"></a>案例
根據預設， [Azure 搜尋服務 Blob 索引子](search-howto-indexing-azure-blob-storage.md) 會將 JSON Blob 剖析為單一的文字區塊。 通常，您會希望 toopreserve hello 結構的 JSON 文件。 例如，假設 hello JSON 文件

    {
        "article" : {
             "text" : "A hopefully useful article explaining how tooparse JSON blobs",
            "datePublished" : "2016-04-13"
            "tags" : [ "search", "storage", "howto" ]    
        }
    }

您可能想的 tooparse 到 Azure 搜尋包含"text"、"datePublished，」 和 「 標記 」 欄位的文件。

或者，當您的 blob 包含**JSON 物件陣列**，您可能會想 hello 陣列 toobecome 不同的 Azure 搜尋文件的每個項目。 例如，提供 Blob 此 JSON：  

    [
        { "id" : "1", "text" : "example 1" },
        { "id" : "2", "text" : "example 2" },
        { "id" : "3", "text" : "example 3" }
    ]

您可以將 Azure 搜尋服務索引填入三個不同的文件，每個都具有「識別碼」和「文字」欄位。

> [!IMPORTANT]
> hello JSON 陣列剖析功能目前為預覽狀態。 它是只用於使用版的 hello REST API **2015年-02-28-preview**。 請記住，預覽 API 是針對測試與評估，不應該用於生產環境。
>
>

## <a name="setting-up-json-indexing"></a>設定 JSON 編製索引
索引 JSON blob 時，是類似 toohello 一般文件擷取。 首先，建立 hello 資料來源，完全以正常方式： 

    POST https://[service name].search.windows.net/datasources?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
        "name" : "my-blob-datasource",
        "type" : "azureblob",
        "credentials" : { "connectionString" : "DefaultEndpointsProtocol=https;AccountName=<account name>;AccountKey=<account key>;" },
        "container" : { "name" : "my-container", "query" : "optional, my-folder" }
    }   

如果您還沒有其中一個，然後建立 hello 目標搜尋索引。 

最後，建立索引子，並設定 hello`parsingMode`參數太`json`(tooindex 每個 blob 做為單一文件) 或`jsonArray`（如果您的 blob 包含 JSON 陣列，您必須視為個別的文件陣列 toobe 的每個項目）：

    POST https://[service name].search.windows.net/indexers?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
      "name" : "my-json-indexer",
      "dataSourceName" : "my-blob-datasource",
      "targetIndexName" : "my-target-index",
      "schedule" : { "interval" : "PT2H" },
      "parameters" : { "configuration" : { "parsingMode" : "json" } }
    }

如果需要使用**欄位對應**toopick hello 的 hello 來源 JSON 文件使用 toopopulate 屬性目標搜尋索引 hello 下一節中所示。

> [!IMPORTANT]
> 當您使用 `json` 或 `jsonArray` 剖析模式時，Azure 搜尋服務會假設資料來源中的所有 blob 都包含 JSON。 如果您需要 toosupport JSON 混用，而且非 JSON 中的 blob，hello 相同資料來源，讓我們知道上[我們的 UserVoice 網站](https://feedback.azure.com/forums/263029-azure-search)。
>
>

## <a name="using-field-mappings-toobuild-search-documents"></a>使用欄位對應 toobuild 搜尋文件
目前，Azure 搜尋服務無法直接編製索引任意 JSON 文件，因為它只支援基本資料類型、字串陣列和 GeoJSON 點。 不過，您可以使用**欄位對應**toopick 部分您的 JSON 文件，而且 「 增益 」 它們 hello 搜尋文件的最上層欄位中。 toolearn 需欄位對應的基本概念，請參閱[Azure 搜尋索引子的欄位對應的橋接的資料來源和搜尋索引的 hello 差異](search-indexer-field-mappings.md)。

返回 tooour 範例 JSON 文件：

    {
        "article" : {
             "text" : "A hopefully useful article explaining how tooparse JSON blobs",
            "datePublished" : "2016-04-13"
            "tags" : [ "search", "storage", "howto" ]    
        }
    }

假設您有搜尋索引以 hello 下列欄位：`text`型別的`Edm.String`，`date`型別的`Edm.DateTimeOffset`，和`tags`型別的`Collection(Edm.String)`。 toomap hello 您 JSON 所需的圖形，請使用下列欄位對應的 hello:

    "fieldMappings" : [
        { "sourceFieldName" : "/article/text", "targetFieldName" : "text" },
        { "sourceFieldName" : "/article/datePublished", "targetFieldName" : "date" },
        { "sourceFieldName" : "/article/tags", "targetFieldName" : "tags" }
      ]

hello hello 對應中的來源欄位名稱使用指定的 hello [JSON 指標](http://tools.ietf.org/html/rfc6901)標記法。 您一開始使用正斜線 toorefer toohello 根目錄的 JSON 文件，然後挑選 （層級任意的巢狀結構） 所需的 hello 屬性使用正斜線分隔的路徑。

您也可以使用以零為起始的索引參照 tooindividual 陣列項目。 比方說，toopick hello 第一個陣列的元素 hello"tags"hello，上述範例中，從使用欄位的對應如下：

    { "sourceFieldName" : "/article/tags/0", "targetFieldName" : "firstTag" }

> [!NOTE]
> 如果欄位的對應路徑中的來源欄位名稱參考 tooa 屬性，可在 JSON 中不存在，該對應會略過不會產生錯誤。 這麼做是為了讓我們可支援具有不同結構描述 (這是常見的使用案例) 的文件。 因為沒有任何驗證，您會需要您欄位的對應規格中 tootake 照護 tooavoid 錯字。
>
>

如果您的 JSON 文件只包含簡單的最上層屬性，可能完全不需要欄位對應。 例如，如果您的 JSON 外觀類似，hello 最上層屬性"text"，"datePublished 」 和 「 標記 」 直接對應 toohello hello 搜尋索引中的對應欄位：

    {
       "text" : "A hopefully useful article explaining how tooparse JSON blobs",
       "datePublished" : "2016-04-13"
       "tags" : [ "search", "storage", "howto" ]    
     }

以下是包含欄位對應的完整索引子承載︰

    POST https://[service name].search.windows.net/indexers?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
      "name" : "my-json-indexer",
      "dataSourceName" : "my-blob-datasource",
      "targetIndexName" : "my-target-index",
      "schedule" : { "interval" : "PT2H" },
      "parameters" : { "configuration" : { "parsingMode" : "json" } },
      "fieldMappings" : [
        { "sourceFieldName" : "/article/text", "targetFieldName" : "text" },
        { "sourceFieldName" : "/article/datePublished", "targetFieldName" : "date" },
        { "sourceFieldName" : "/article/tags", "targetFieldName" : "tags" }
        ]
    }

## <a name="indexing-nested-json-arrays"></a>編製巢狀 JSON 陣列索引
如果您想 tooindex JSON 物件的陣列，但該陣列是巢狀某處 hello 文件中？ 您可以挑選哪些屬性包含使用 hello hello 陣列`documentRoot`組態屬性。 例如，如果您的 Blob 看起來像這樣︰

    {
        "level1" : {
            "level2" : [
                { "id" : "1", "text" : "Use hello documentRoot property" },
                { "id" : "2", "text" : "toopluck hello array you want tooindex" },
                { "id" : "3", "text" : "even if it's nested inside hello document" }  
            ]
        }
    }

使用包含在 hello 這個組態 tooindex hello 陣列`level2`屬性：

    {
        "name" : "my-json-array-indexer",
        ... other indexer properties
        "parameters" : { "configuration" : { "parsingMode" : "jsonArray", "documentRoot" : "/level1/level2" } }
    }

## <a name="help-us-make-azure-search-better"></a>協助我們改進 Azure 搜尋服務
如果您有功能要求或進行改善的想法，連接上 toous 我們[UserVoice 網站](https://feedback.azure.com/forums/263029-azure-search/)。
