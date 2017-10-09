---
title: "在 Azure 搜尋 aaaIndexers |Microsoft 文件"
description: "搜耙 Azure SQL database、 Azure Cosmos DB 或 Azure 儲存體 tooextract 可搜尋的資料，然後填入 Azure 搜尋索引。"
services: search
documentationcenter: 
author: HeidiSteen
manager: jhubbard
editor: 
tags: azure-portal
ms.assetid: 34a7694c-8fd9-46b1-8900-cefdd7236323
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 05/01/2017
ms.author: heidist
ms.openlocfilehash: 6a816252ec5d6032491a12651c05cb1fe77d3d1a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="indexers-in-azure-search"></a>Azure 搜尋服務中的索引子
> [!div class="op_single_selector"]
>
> * [概觀](search-indexer-overview.md)
> * [入口網站](search-import-data-portal.md)
> * [Azure SQL](search-howto-connecting-azure-sql-database-to-azure-search-using-indexers.md)
> * [Azure Cosmos DB](search-howto-index-documentdb.md)
> * [Azure Blob 儲存體](search-howto-indexing-azure-blob-storage.md)
> * [Azure 資料表儲存體](search-howto-indexing-azure-tables.md)
>
>

**索引子**在 Azure 搜尋，會從外部資料來源中擷取可搜尋的資料和中繼資料並填入索引編目程式根據 hello 索引與資料來源之間的欄位的對應。 這個方法有時是參照的 tooas '提取模型'，因為在 hello 服務提取資料中的不需要您 toowrite 資料 tooan 索引推播通知的任何程式碼。

您可以使用索引子，因為 hello 唯一的方法，用於擷取資料，或使用，包括載入只是某些索引中的 hello 欄位的索引子的 hello 使用的技術的組合。

您可以依需要執行索引子，也可以依週期性的資料重新整理排程，最多每十五分鐘執行一次。 若想更頻繁地進行更新，則 Azure 搜尋服務和外部資料來源中都必須要有可同時更新資料的發送模型。

## <a name="approaches-for-creating-and-managing-indexers"></a>建立與管理索引子的方法
對於 Azure SQL 或 Azure Cosmos DB 等公開上市的索引子，您可以使用下列方法來建立及管理索引子︰

* [入口網站 > 匯入資料精靈](search-get-started-portal.md)
* [服務 REST API](https://msdn.microsoft.com/library/azure/dn946891.aspx)
* [.NET SDK](https://msdn.microsoft.com/library/azure/microsoft.azure.search.iindexersoperations.aspx)

## <a name="basic-configuration-steps"></a>基本組態步驟
索引子可以提供唯一 toohello 資料來源的功能。 在這方面，索引子或資料來源組態的某些層面會因索引子類型而所有不同。 不過，所有索引子共用 hello 相同基本的構成要素和需求。 以下涵蓋索引子，這種常見 tooall 步驟。

### <a name="step-1-create-an-index"></a>步驟 1：建立索引
索引子將用來自動化某些工作相關的 toodata 擷取，但建立索引不是其中一個。 若要滿足必要條件，您必須擁有預先定義的索引，且欄位必須與外部資料來源中的欄位相符。 如需建構索引的詳細資訊，請參閱 [建立索引 (Azure 搜尋服務 REST API)](https://msdn.microsoft.com/library/azure/dn798941.aspx)。

### <a name="step-2-create-a-data-source"></a>步驟 2：建立資料來源
索引子會從保有連接字串等資訊的 **資料來源** 提取資料。 目前支援下列資料來源的 hello:

* [Azure SQL Database 或 Azure 虛擬機器中的 SQL Server](search-howto-connecting-azure-sql-database-to-azure-search-using-indexers.md)
* [Azure Cosmos DB](search-howto-index-documentdb.md)
* [Azure Blob 儲存體](search-howto-indexing-azure-blob-storage.md)，使用 PDF、 Office 文件、 HTML 或 XML tooextract 文字
* [Azure 資料表儲存體](search-howto-indexing-azure-tables.md)

資料來源設定及與 hello 索引子使用它們一次一個以上的索引的也就是說，資料來源可供多個索引子 tooload 分開管理。

### <a name="step-3create-and-schedule-hello-indexer"></a>步驟 3： 建立和排程 hello 索引子
hello 索引子定義是指定 hello 索引、 資料來源和排程的建構。 索引子可以參考資料來源從另一個服務，只要該資料來源是來自 hello 相同訂用帳戶。 如需建構索引的詳細資訊，請參閱 [建立索引子 (Azure 搜尋服務 REST API)](https://msdn.microsoft.com/library/azure/dn946899.aspx)。

## <a name="next-steps"></a>後續步驟
現在您擁有 hello 的基本概念，hello 下一個步驟是 tooreview 需求和工作特定 tooeach 資料來源類型。

* [Azure SQL Database 或 Azure 虛擬機器中的 SQL Server](search-howto-connecting-azure-sql-database-to-azure-search-using-indexers.md)
* [Azure Cosmos DB](search-howto-index-documentdb.md)
* [Azure Blob 儲存體](search-howto-indexing-azure-blob-storage.md)，使用 PDF、 Office 文件、 HTML 或 XML tooextract 文字
* [Azure 資料表儲存體](search-howto-indexing-azure-tables.md)
* [索引使用 hello Azure 搜尋 Blob 索引子的 CSV blob](search-howto-index-csv-blobs.md)
* [使用 Azure 搜尋服務 Blob 索引子編製索引 JSON Blob](search-howto-index-json-blobs.md)
