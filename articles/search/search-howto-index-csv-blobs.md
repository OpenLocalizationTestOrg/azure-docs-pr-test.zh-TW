---
title: "Azure 搜尋 blob 索引子與 blob aaaIndexing CSV |Microsoft 文件"
description: "了解 tooindex CSV 與 Azure 搜尋的 blob"
services: search
documentationcenter: 
author: chaosrealm
manager: pablocas
editor: 
ms.assetid: ed3c9cff-1946-4af2-a05a-5e0b3d61eb25
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 12/15/2016
ms.author: eugenesh
ms.openlocfilehash: f2b1ce824e62c5b3f6155c6e88887897cf1a8eae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="indexing-csv-blobs-with-azure-search-blob-indexer"></a>使用 Azure 搜尋服務 Blob 索引子編製索引 CSV Blob
根據預設， [Azure 搜尋服務 Blob 索引子](search-howto-indexing-azure-blob-storage.md) 會將分隔符號文字 Blob 剖析為單一的文字區塊。 不過，使用包含 CSV 資料的 blob，您通常想 tootreat hello blob 中的每一行做為個別的文件。 例如，給定的 hello 下列分隔文字： 

    id, datePublished, tags
    1, 2016-01-12, "azure-search,azure,cloud" 
    2, 2016-07-07, "cloud,mobile" 

您可能會想 tooparse 它為 2 的文件，每個包含"id"、"datePublished 」 和 「 標記 」 欄位。

在本文中，您將學習 tooparse CSV 與 Azure 搜尋 blob 索引子的 blob。 

> [!IMPORTANT]
> 這項功能目前為預覽版本。 它是只用於使用版的 hello REST API **2015年-02-28-preview**。 請記住，預覽 API 是針對測試與評估，不應該用於生產環境。 
> 
> 

## <a name="setting-up-csv-indexing"></a>設定 CSV 編製索引
tooindex CSV blob 建立或更新索引子定義以 hello`delimitedText`剖析模式：  

    {
      "name" : "my-csv-indexer",
      ... other indexer properties
      "parameters" : { "configuration" : { "parsingMode" : "delimitedText", "firstLineContainsHeaders" : true } }
    }

如需有關 hello 建立索引子 API，請簽出[建立索引子](search-api-indexers-2015-02-28-preview.md#create-indexer)。

`firstLineContainsHeaders`表示每一個 blob 的 hello 第一個 （非空白） 列包含標頭。
如果 blob 不包含初始標頭行，應該指定 hello 標頭 hello indexer 組態： 

    "parameters" : { "configuration" : { "parsingMode" : "delimitedText", "delimitedTextHeaders" : "id,datePublished,tags" } } 

目前，只有 hello utf-8 編碼支援。 此外，只有 hello 逗號`','`支援為 hello 分隔符號字元。 如果您需要支援其他編碼或分隔符號，請在 [UserVoice 網站](https://feedback.azure.com/forums/263029-azure-search)讓我們知道。

> [!IMPORTANT]
> 當您使用分隔的 hello 文字剖析模式中，Azure 搜尋會假設您的資料來源中的所有 blob，將會都是 CSV。 如果您需要 toosupport 混用 CSV 和非 CSV 中的 blob，hello 相同資料來源，請讓我們知道上[我們的 UserVoice 網站](https://feedback.azure.com/forums/263029-azure-search)。
> 
> 

## <a name="request-examples"></a>要求範例
將這所有放在一起，以下是 hello 完整裝載範例。 

資料來源： 

    POST https://[service name].search.windows.net/datasources?api-version=2015-02-28-Preview
    Content-Type: application/json
    api-key: [admin key]

    {
        "name" : "my-blob-datasource",
        "type" : "azureblob",
        "credentials" : { "connectionString" : "DefaultEndpointsProtocol=https;AccountName=<account name>;AccountKey=<account key>;" },
        "container" : { "name" : "my-container", "query" : "<optional, my-folder>" }
    }   

索引子：

    POST https://[service name].search.windows.net/indexers?api-version=2015-02-28-Preview
    Content-Type: application/json
    api-key: [admin key]

    {
      "name" : "my-csv-indexer",
      "dataSourceName" : "my-blob-datasource",
      "targetIndexName" : "my-target-index",
      "parameters" : { "configuration" : { "parsingMode" : "delimitedText", "delimitedTextHeaders" : "id,datePublished,tags" } }
    }

## <a name="help-us-make-azure-search-better"></a>協助我們改進 Azure 搜尋服務
如果您有功能要求或增強功能的構想，請聯繫 toous 上我們[UserVoice 網站](https://feedback.azure.com/forums/263029-azure-search/)。

