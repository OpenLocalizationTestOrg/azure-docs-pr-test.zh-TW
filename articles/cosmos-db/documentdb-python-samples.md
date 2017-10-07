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
# <a name="azure-cosmos-db-python-examples"></a><span data-ttu-id="19297-104">Azure Cosmos DB Python 範例</span><span class="sxs-lookup"><span data-stu-id="19297-104">Azure Cosmos DB Python examples</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="19297-105">.NET 範例</span><span class="sxs-lookup"><span data-stu-id="19297-105">.NET Examples</span></span>](documentdb-dotnet-samples.md)
> * [<span data-ttu-id="19297-106">Node.js 範例</span><span class="sxs-lookup"><span data-stu-id="19297-106">Node.js Examples</span></span>](documentdb-nodejs-samples.md)
> * [<span data-ttu-id="19297-107">Python 範例</span><span class="sxs-lookup"><span data-stu-id="19297-107">Python Examples</span></span>](documentdb-python-samples.md)
> * [<span data-ttu-id="19297-108">Azure 程式碼範例庫</span><span class="sxs-lookup"><span data-stu-id="19297-108">Azure Code Sample Gallery</span></span>](https://azure.microsoft.com/documentation/samples/?service=documentdb)
> 
> 

<span data-ttu-id="19297-109">執行 CRUD 作業及其他 Azure Cosmos DB 資源上的一般作業的範例方案隨附的 hello [azure-documentdb-python](https://github.com/Azure/azure-documentdb-python/tree/master/samples) GitHub 儲存機制。</span><span class="sxs-lookup"><span data-stu-id="19297-109">Sample solutions that perform CRUD operations and other common operations on Azure Cosmos DB resources are included in hello [azure-documentdb-python](https://github.com/Azure/azure-documentdb-python/tree/master/samples) GitHub repository.</span></span> <span data-ttu-id="19297-110">本文提供：</span><span class="sxs-lookup"><span data-stu-id="19297-110">This article provides:</span></span>

* <span data-ttu-id="19297-111">在 hello Python 範例專案檔中的連結 toohello 工作。</span><span class="sxs-lookup"><span data-stu-id="19297-111">Links toohello tasks in each of hello Python example project files.</span></span> 
* <span data-ttu-id="19297-112">連結 toohello 相關的應用程式開發介面參考內容。</span><span class="sxs-lookup"><span data-stu-id="19297-112">Links toohello related API reference content.</span></span>

<span data-ttu-id="19297-113">**必要條件**</span><span class="sxs-lookup"><span data-stu-id="19297-113">**Prerequisites**</span></span>

1. <span data-ttu-id="19297-114">您需要 Azure 帳戶 toouse 這些 Python 範例：</span><span class="sxs-lookup"><span data-stu-id="19297-114">You need an Azure account toouse these Python examples:</span></span>
   * <span data-ttu-id="19297-115">您可以[開啟免費的 Azure 帳戶](https://azure.microsoft.com/pricing/free-trial/)： 取得信用額度您可以使用 tootry 出支付 Azure 服務，而且即使他們用於之後您可以在最多保留 hello 帳戶，並使用免費的 Azure 服務，例如網站。</span><span class="sxs-lookup"><span data-stu-id="19297-115">You can [open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/): You get credits you can use tootry out paid Azure services, and even after they're used up you can keep hello account and use free Azure services, such as Websites.</span></span> <span data-ttu-id="19297-116">永遠不會將向您的信用卡，除非您明確地變更您的設定，並詢問 toobe 收費。</span><span class="sxs-lookup"><span data-stu-id="19297-116">Your credit card will never be charged, unless you explicitly change your settings and ask toobe charged.</span></span>
     * <span data-ttu-id="19297-117">您可以 [啟用 Visual Studio 訂閱者權益](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/)：您的 Visual Studio 訂用帳戶每個月都會提供額度，供您用在 Azure 付費服務。</span><span class="sxs-lookup"><span data-stu-id="19297-117">You can [activate Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/): Your Visual Studio subscription gives you credits every month that you can use for paid Azure services.</span></span>
2. <span data-ttu-id="19297-118">您也需要 hello [Python SDK](documentdb-sdk-python.md)。</span><span class="sxs-lookup"><span data-stu-id="19297-118">You also need hello [Python SDK](documentdb-sdk-python.md).</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="19297-119">每個範例都各自獨立，自己設定，並自行清理。</span><span class="sxs-lookup"><span data-stu-id="19297-119">Each sample is self-contained, it sets itself up and cleans up after itself.</span></span> <span data-ttu-id="19297-120">因此，hello 範例發出多個呼叫太[document_client。CreateCollection](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html)。</span><span class="sxs-lookup"><span data-stu-id="19297-120">As such, hello samples issue multiple calls too[document_client.CreateCollection](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html).</span></span> <span data-ttu-id="19297-121">這是您的訂用帳戶每次需要支付 1 小時內的每個 hello 效能層 hello 集合正在建立的使用量。</span><span class="sxs-lookup"><span data-stu-id="19297-121">Each time this is done your subscription will be billed for 1 hour of usage per hello performance tier of hello collection being created.</span></span> 
   > 
   > 

## <a name="database-examples"></a><span data-ttu-id="19297-122">資料庫範例</span><span class="sxs-lookup"><span data-stu-id="19297-122">Database examples</span></span>
<span data-ttu-id="19297-123">hello [Program.py](https://github.com/Azure/azure-documentdb-python/tree/master/samples/DatabaseManagement/Program.py)檔案的 hello [DatabaseManagement](https://github.com/Azure/azure-documentdb-python/tree/master/samples/DatabaseManagement)專案顯示影響 tooperform hello 下列工作。</span><span class="sxs-lookup"><span data-stu-id="19297-123">hello [Program.py](https://github.com/Azure/azure-documentdb-python/tree/master/samples/DatabaseManagement/Program.py) file of hello [DatabaseManagement](https://github.com/Azure/azure-documentdb-python/tree/master/samples/DatabaseManagement) project shows how tooperform hello following tasks.</span></span>

| <span data-ttu-id="19297-124">Task</span><span class="sxs-lookup"><span data-stu-id="19297-124">Task</span></span> | <span data-ttu-id="19297-125">API 參考資料</span><span class="sxs-lookup"><span data-stu-id="19297-125">API reference</span></span> |
| --- | --- |
| [<span data-ttu-id="19297-126">建立資料庫</span><span class="sxs-lookup"><span data-stu-id="19297-126">Create a database</span></span>](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/DatabaseManagement/Program.py#L65-L76) |[<span data-ttu-id="19297-127">document_client.CreateDatabase</span><span class="sxs-lookup"><span data-stu-id="19297-127">document_client.CreateDatabase</span></span>](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html) |
| [<span data-ttu-id="19297-128">查詢帳戶中的資料庫</span><span class="sxs-lookup"><span data-stu-id="19297-128">Query an account for a database</span></span>](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/DatabaseManagement/Program.py#L49-L62) |[<span data-ttu-id="19297-129">document_client.QueryDatabases</span><span class="sxs-lookup"><span data-stu-id="19297-129">document_client.QueryDatabases</span></span>](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html) |
| [<span data-ttu-id="19297-130">依識別碼讀取資料庫</span><span class="sxs-lookup"><span data-stu-id="19297-130">Read a database by Id</span></span>](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/DatabaseManagement/Program.py#L79-L96) |[<span data-ttu-id="19297-131">document_client.ReadDatabase</span><span class="sxs-lookup"><span data-stu-id="19297-131">document_client.ReadDatabase</span></span>](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html) |
| [<span data-ttu-id="19297-132">列出帳戶的資料庫</span><span class="sxs-lookup"><span data-stu-id="19297-132">List databases for an account</span></span>](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/DatabaseManagement/Program.py#L99-L110) |[<span data-ttu-id="19297-133">document_client.ReadDatabases</span><span class="sxs-lookup"><span data-stu-id="19297-133">document_client.ReadDatabases</span></span>](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html) |
| [<span data-ttu-id="19297-134">刪除資料庫</span><span class="sxs-lookup"><span data-stu-id="19297-134">Delete a database</span></span>](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/DatabaseManagement/Program.py#L113-L126) |[<span data-ttu-id="19297-135">document_client.DeleteDatabase</span><span class="sxs-lookup"><span data-stu-id="19297-135">document_client.DeleteDatabase</span></span>](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html) |

## <a name="collection-examples"></a><span data-ttu-id="19297-136">集合範例</span><span class="sxs-lookup"><span data-stu-id="19297-136">Collection examples</span></span>
<span data-ttu-id="19297-137">hello [Program.py](https://github.com/Azure/azure-documentdb-python/tree/master/samples/CollectionManagement/Program.py)檔案的 hello [CollectionManagement](https://github.com/Azure/azure-documentdb-python/tree/master/samples/CollectionManagement)專案顯示影響 tooperform hello 下列工作。</span><span class="sxs-lookup"><span data-stu-id="19297-137">hello [Program.py](https://github.com/Azure/azure-documentdb-python/tree/master/samples/CollectionManagement/Program.py) file of hello [CollectionManagement](https://github.com/Azure/azure-documentdb-python/tree/master/samples/CollectionManagement) project shows how tooperform hello following tasks.</span></span>

| <span data-ttu-id="19297-138">Task</span><span class="sxs-lookup"><span data-stu-id="19297-138">Task</span></span> | <span data-ttu-id="19297-139">API 參考資料</span><span class="sxs-lookup"><span data-stu-id="19297-139">API reference</span></span> |
| --- | --- |
| [<span data-ttu-id="19297-140">建立集合</span><span class="sxs-lookup"><span data-stu-id="19297-140">Create a collection</span></span>](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/CollectionManagement/Program.py#L84-L135) |[<span data-ttu-id="19297-141">document_client.CreateCollection</span><span class="sxs-lookup"><span data-stu-id="19297-141">document_client.CreateCollection</span></span>](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html#CreateCollection) |
| [<span data-ttu-id="19297-142">讀取資料庫中所有集合的清單</span><span class="sxs-lookup"><span data-stu-id="19297-142">Read a list of all collections in a database</span></span>](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/CollectionManagement/Program.py#L198-L225) |[<span data-ttu-id="19297-143">document_client.ListCollections</span><span class="sxs-lookup"><span data-stu-id="19297-143">document_client.ListCollections</span></span>](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html#CreateCollection) |
| [<span data-ttu-id="19297-144">依識別碼取得集合</span><span class="sxs-lookup"><span data-stu-id="19297-144">Get a collection by Id</span></span>](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/CollectionManagement/Program.py#L178-L195) |[<span data-ttu-id="19297-145">document_client.ReadCollection</span><span class="sxs-lookup"><span data-stu-id="19297-145">document_client.ReadCollection</span></span>](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html#CreateCollection) |
| [<span data-ttu-id="19297-146">取得集合的效能層</span><span class="sxs-lookup"><span data-stu-id="19297-146">Get performance tier of a collection</span></span>](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/CollectionManagement/Program.py#L139-L161) |[<span data-ttu-id="19297-147">DocumentQueryable.QueryOffers</span><span class="sxs-lookup"><span data-stu-id="19297-147">DocumentQueryable.QueryOffers</span></span>](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html#CreateCollection) |
| [<span data-ttu-id="19297-148">變更集合的效能層</span><span class="sxs-lookup"><span data-stu-id="19297-148">Change performance tier of a collection</span></span>](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/CollectionManagement/Program.py#L163-L175) |[<span data-ttu-id="19297-149">document_client.ReplaceOffer</span><span class="sxs-lookup"><span data-stu-id="19297-149">document_client.ReplaceOffer</span></span>](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html#CreateCollection) |
| [<span data-ttu-id="19297-150">刪除集合</span><span class="sxs-lookup"><span data-stu-id="19297-150">Delete a collection</span></span>](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/CollectionManagement/Program.py#L212-L225) |[<span data-ttu-id="19297-151">document_client.DeleteCollection</span><span class="sxs-lookup"><span data-stu-id="19297-151">document_client.DeleteCollection</span></span>](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html#CreateCollection) |

