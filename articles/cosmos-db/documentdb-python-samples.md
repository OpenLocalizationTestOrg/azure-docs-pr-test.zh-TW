---
title: "Azure Cosmos DB aaaDocumentDB API Python 範例 |Microsoft 文件"
description: "在 GitHub 上找到適用於 Azure Cosmos DB 中一般工作 (包括 CRUD 作業) 的 Python 範例。"
keywords: "Python 範例"
services: cosmos-db
author: moderakh
manager: jhubbard
editor: monicar
documentationcenter: python
ms.assetid: 7f4f8db3-e9db-4645-92ef-7819d486a349
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/24/2016
ms.author: moderakh
ms.openlocfilehash: d8f240782b0997f2d32b68d310dc6f4ff6cb36d0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-python-examples"></a>Azure Cosmos DB Python 範例
> [!div class="op_single_selector"]
> * [.NET 範例](documentdb-dotnet-samples.md)
> * [Node.js 範例](documentdb-nodejs-samples.md)
> * [Python 範例](documentdb-python-samples.md)
> * [Azure 程式碼範例庫](https://azure.microsoft.com/documentation/samples/?service=documentdb)
> 
> 

執行 CRUD 作業及其他 Azure Cosmos DB 資源上的一般作業的範例方案隨附的 hello [azure-documentdb-python](https://github.com/Azure/azure-documentdb-python/tree/master/samples) GitHub 儲存機制。 本文提供：

* 在 hello Python 範例專案檔中的連結 toohello 工作。 
* 連結 toohello 相關的應用程式開發介面參考內容。

**必要條件**

1. 您需要 Azure 帳戶 toouse 這些 Python 範例：
   * 您可以[開啟免費的 Azure 帳戶](https://azure.microsoft.com/pricing/free-trial/)： 取得信用額度您可以使用 tootry 出支付 Azure 服務，而且即使他們用於之後您可以在最多保留 hello 帳戶，並使用免費的 Azure 服務，例如網站。 永遠不會將向您的信用卡，除非您明確地變更您的設定，並詢問 toobe 收費。
     * 您可以 [啟用 Visual Studio 訂閱者權益](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/)：您的 Visual Studio 訂用帳戶每個月都會提供額度，供您用在 Azure 付費服務。
2. 您也需要 hello [Python SDK](documentdb-sdk-python.md)。 
   
   > [!NOTE]
   > 每個範例都各自獨立，自己設定，並自行清理。 因此，hello 範例發出多個呼叫太[document_client。CreateCollection](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html)。 這是您的訂用帳戶每次需要支付 1 小時內的每個 hello 效能層 hello 集合正在建立的使用量。 
   > 
   > 

## <a name="database-examples"></a>資料庫範例
hello [Program.py](https://github.com/Azure/azure-documentdb-python/tree/master/samples/DatabaseManagement/Program.py)檔案的 hello [DatabaseManagement](https://github.com/Azure/azure-documentdb-python/tree/master/samples/DatabaseManagement)專案顯示影響 tooperform hello 下列工作。

| Task | API 參考資料 |
| --- | --- |
| [建立資料庫](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/DatabaseManagement/Program.py#L65-L76) |[document_client.CreateDatabase](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html) |
| [查詢帳戶中的資料庫](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/DatabaseManagement/Program.py#L49-L62) |[document_client.QueryDatabases](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html) |
| [依識別碼讀取資料庫](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/DatabaseManagement/Program.py#L79-L96) |[document_client.ReadDatabase](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html) |
| [列出帳戶的資料庫](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/DatabaseManagement/Program.py#L99-L110) |[document_client.ReadDatabases](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html) |
| [刪除資料庫](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/DatabaseManagement/Program.py#L113-L126) |[document_client.DeleteDatabase](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html) |

## <a name="collection-examples"></a>集合範例
hello [Program.py](https://github.com/Azure/azure-documentdb-python/tree/master/samples/CollectionManagement/Program.py)檔案的 hello [CollectionManagement](https://github.com/Azure/azure-documentdb-python/tree/master/samples/CollectionManagement)專案顯示影響 tooperform hello 下列工作。

| Task | API 參考資料 |
| --- | --- |
| [建立集合](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/CollectionManagement/Program.py#L84-L135) |[document_client.CreateCollection](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html#CreateCollection) |
| [讀取資料庫中所有集合的清單](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/CollectionManagement/Program.py#L198-L225) |[document_client.ListCollections](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html#CreateCollection) |
| [依識別碼取得集合](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/CollectionManagement/Program.py#L178-L195) |[document_client.ReadCollection](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html#CreateCollection) |
| [取得集合的效能層](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/CollectionManagement/Program.py#L139-L161) |[DocumentQueryable.QueryOffers](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html#CreateCollection) |
| [變更集合的效能層](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/CollectionManagement/Program.py#L163-L175) |[document_client.ReplaceOffer](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html#CreateCollection) |
| [刪除集合](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/CollectionManagement/Program.py#L212-L225) |[document_client.DeleteCollection](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html#CreateCollection) |

