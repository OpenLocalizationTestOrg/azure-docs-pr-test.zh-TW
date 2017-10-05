---
title: "適用於 Azure Cosmos DB 的 DocumentDB API Python 範例 | Microsoft Docs"
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
ms.openlocfilehash: d1577eeeb8fe8007394431ce70a1c7a6ee61776b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="azure-cosmos-db-python-examples"></a><span data-ttu-id="7ae95-104">Azure Cosmos DB Python 範例</span><span class="sxs-lookup"><span data-stu-id="7ae95-104">Azure Cosmos DB Python examples</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="7ae95-105">.NET 範例</span><span class="sxs-lookup"><span data-stu-id="7ae95-105">.NET Examples</span></span>](documentdb-dotnet-samples.md)
> * [<span data-ttu-id="7ae95-106">Node.js 範例</span><span class="sxs-lookup"><span data-stu-id="7ae95-106">Node.js Examples</span></span>](documentdb-nodejs-samples.md)
> * [<span data-ttu-id="7ae95-107">Python 範例</span><span class="sxs-lookup"><span data-stu-id="7ae95-107">Python Examples</span></span>](documentdb-python-samples.md)
> * [<span data-ttu-id="7ae95-108">Azure 程式碼範例庫</span><span class="sxs-lookup"><span data-stu-id="7ae95-108">Azure Code Sample Gallery</span></span>](https://azure.microsoft.com/documentation/samples/?service=documentdb)
> 
> 

<span data-ttu-id="7ae95-109">[azure-documentdb-python](https://github.com/Azure/azure-documentdb-python/tree/master/samples) GitHub 存放庫中包含可對 Azure Cosmos DB 資源執行 CRUD 作業和其他常見作業的範例解決方案。</span><span class="sxs-lookup"><span data-stu-id="7ae95-109">Sample solutions that perform CRUD operations and other common operations on Azure Cosmos DB resources are included in the [azure-documentdb-python](https://github.com/Azure/azure-documentdb-python/tree/master/samples) GitHub repository.</span></span> <span data-ttu-id="7ae95-110">本文提供：</span><span class="sxs-lookup"><span data-stu-id="7ae95-110">This article provides:</span></span>

* <span data-ttu-id="7ae95-111">每個 Python 範例專案檔中各項工作的連結。</span><span class="sxs-lookup"><span data-stu-id="7ae95-111">Links to the tasks in each of the Python example project files.</span></span> 
* <span data-ttu-id="7ae95-112">相關 API 參考內容的連結。</span><span class="sxs-lookup"><span data-stu-id="7ae95-112">Links to the related API reference content.</span></span>

<span data-ttu-id="7ae95-113">**必要條件**</span><span class="sxs-lookup"><span data-stu-id="7ae95-113">**Prerequisites**</span></span>

1. <span data-ttu-id="7ae95-114">您必須要有 Azure 帳戶才能使用這些 Python 範例：</span><span class="sxs-lookup"><span data-stu-id="7ae95-114">You need an Azure account to use these Python examples:</span></span>
   * <span data-ttu-id="7ae95-115">您可以 [免費申請 Azure 帳戶](https://azure.microsoft.com/pricing/free-trial/)- 您將取得可試用付費 Azure 服務的額度，且即使在額度用完後，您仍可保留帳戶，並使用免費的 Azure 服務，例如「網站」。</span><span class="sxs-lookup"><span data-stu-id="7ae95-115">You can [open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/): You get credits you can use to try out paid Azure services, and even after they're used up you can keep the account and use free Azure services, such as Websites.</span></span> <span data-ttu-id="7ae95-116">除非您明確變更您的設定且同意付費，否則我們將不會從您的信用卡收取任何費用。</span><span class="sxs-lookup"><span data-stu-id="7ae95-116">Your credit card will never be charged, unless you explicitly change your settings and ask to be charged.</span></span>
     * <span data-ttu-id="7ae95-117">您可以 [啟用 Visual Studio 訂閱者權益](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/)：您的 Visual Studio 訂用帳戶每個月都會提供額度，供您用在 Azure 付費服務。</span><span class="sxs-lookup"><span data-stu-id="7ae95-117">You can [activate Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/): Your Visual Studio subscription gives you credits every month that you can use for paid Azure services.</span></span>
2. <span data-ttu-id="7ae95-118">您也需要 [Python SDK](documentdb-sdk-python.md)。</span><span class="sxs-lookup"><span data-stu-id="7ae95-118">You also need the [Python SDK](documentdb-sdk-python.md).</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="7ae95-119">每個範例都各自獨立，自己設定，並自行清理。</span><span class="sxs-lookup"><span data-stu-id="7ae95-119">Each sample is self-contained, it sets itself up and cleans up after itself.</span></span> <span data-ttu-id="7ae95-120">據此，這些範例對 [document_client.CreateCollection](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html) 發出多個呼叫。</span><span class="sxs-lookup"><span data-stu-id="7ae95-120">As such, the samples issue multiple calls to [document_client.CreateCollection](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html).</span></span> <span data-ttu-id="7ae95-121">每當執行此動作時，即會根據所建立之集合的效能層，對您的訂用帳戶計入一小時的使用量費用。</span><span class="sxs-lookup"><span data-stu-id="7ae95-121">Each time this is done your subscription will be billed for 1 hour of usage per the performance tier of the collection being created.</span></span> 
   > 
   > 

## <a name="database-examples"></a><span data-ttu-id="7ae95-122">資料庫範例</span><span class="sxs-lookup"><span data-stu-id="7ae95-122">Database examples</span></span>
<span data-ttu-id="7ae95-123">[DatabaseManagement](https://github.com/Azure/azure-documentdb-python/tree/master/samples/DatabaseManagement) 專案的 [Program.py](https://github.com/Azure/azure-documentdb-python/tree/master/samples/DatabaseManagement/Program.py) 檔案說明如何執行下列工作。</span><span class="sxs-lookup"><span data-stu-id="7ae95-123">The [Program.py](https://github.com/Azure/azure-documentdb-python/tree/master/samples/DatabaseManagement/Program.py) file of the [DatabaseManagement](https://github.com/Azure/azure-documentdb-python/tree/master/samples/DatabaseManagement) project shows how to perform the following tasks.</span></span>

| <span data-ttu-id="7ae95-124">Task</span><span class="sxs-lookup"><span data-stu-id="7ae95-124">Task</span></span> | <span data-ttu-id="7ae95-125">API 參考資料</span><span class="sxs-lookup"><span data-stu-id="7ae95-125">API reference</span></span> |
| --- | --- |
| [<span data-ttu-id="7ae95-126">建立資料庫</span><span class="sxs-lookup"><span data-stu-id="7ae95-126">Create a database</span></span>](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/DatabaseManagement/Program.py#L65-L76) |[<span data-ttu-id="7ae95-127">document_client.CreateDatabase</span><span class="sxs-lookup"><span data-stu-id="7ae95-127">document_client.CreateDatabase</span></span>](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html) |
| [<span data-ttu-id="7ae95-128">查詢帳戶中的資料庫</span><span class="sxs-lookup"><span data-stu-id="7ae95-128">Query an account for a database</span></span>](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/DatabaseManagement/Program.py#L49-L62) |[<span data-ttu-id="7ae95-129">document_client.QueryDatabases</span><span class="sxs-lookup"><span data-stu-id="7ae95-129">document_client.QueryDatabases</span></span>](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html) |
| [<span data-ttu-id="7ae95-130">依識別碼讀取資料庫</span><span class="sxs-lookup"><span data-stu-id="7ae95-130">Read a database by Id</span></span>](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/DatabaseManagement/Program.py#L79-L96) |[<span data-ttu-id="7ae95-131">document_client.ReadDatabase</span><span class="sxs-lookup"><span data-stu-id="7ae95-131">document_client.ReadDatabase</span></span>](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html) |
| [<span data-ttu-id="7ae95-132">列出帳戶的資料庫</span><span class="sxs-lookup"><span data-stu-id="7ae95-132">List databases for an account</span></span>](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/DatabaseManagement/Program.py#L99-L110) |[<span data-ttu-id="7ae95-133">document_client.ReadDatabases</span><span class="sxs-lookup"><span data-stu-id="7ae95-133">document_client.ReadDatabases</span></span>](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html) |
| [<span data-ttu-id="7ae95-134">刪除資料庫</span><span class="sxs-lookup"><span data-stu-id="7ae95-134">Delete a database</span></span>](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/DatabaseManagement/Program.py#L113-L126) |[<span data-ttu-id="7ae95-135">document_client.DeleteDatabase</span><span class="sxs-lookup"><span data-stu-id="7ae95-135">document_client.DeleteDatabase</span></span>](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html) |

## <a name="collection-examples"></a><span data-ttu-id="7ae95-136">集合範例</span><span class="sxs-lookup"><span data-stu-id="7ae95-136">Collection examples</span></span>
<span data-ttu-id="7ae95-137">[CollectionManagement](https://github.com/Azure/azure-documentdb-python/tree/master/samples/CollectionManagement) 專案的 [Program.py](https://github.com/Azure/azure-documentdb-python/tree/master/samples/CollectionManagement/Program.py) 檔案說明如何執行下列工作。</span><span class="sxs-lookup"><span data-stu-id="7ae95-137">The [Program.py](https://github.com/Azure/azure-documentdb-python/tree/master/samples/CollectionManagement/Program.py) file of the [CollectionManagement](https://github.com/Azure/azure-documentdb-python/tree/master/samples/CollectionManagement) project shows how to perform the following tasks.</span></span>

| <span data-ttu-id="7ae95-138">Task</span><span class="sxs-lookup"><span data-stu-id="7ae95-138">Task</span></span> | <span data-ttu-id="7ae95-139">API 參考資料</span><span class="sxs-lookup"><span data-stu-id="7ae95-139">API reference</span></span> |
| --- | --- |
| [<span data-ttu-id="7ae95-140">建立集合</span><span class="sxs-lookup"><span data-stu-id="7ae95-140">Create a collection</span></span>](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/CollectionManagement/Program.py#L84-L135) |[<span data-ttu-id="7ae95-141">document_client.CreateCollection</span><span class="sxs-lookup"><span data-stu-id="7ae95-141">document_client.CreateCollection</span></span>](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html#CreateCollection) |
| [<span data-ttu-id="7ae95-142">讀取資料庫中所有集合的清單</span><span class="sxs-lookup"><span data-stu-id="7ae95-142">Read a list of all collections in a database</span></span>](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/CollectionManagement/Program.py#L198-L225) |[<span data-ttu-id="7ae95-143">document_client.ListCollections</span><span class="sxs-lookup"><span data-stu-id="7ae95-143">document_client.ListCollections</span></span>](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html#CreateCollection) |
| [<span data-ttu-id="7ae95-144">依識別碼取得集合</span><span class="sxs-lookup"><span data-stu-id="7ae95-144">Get a collection by Id</span></span>](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/CollectionManagement/Program.py#L178-L195) |[<span data-ttu-id="7ae95-145">document_client.ReadCollection</span><span class="sxs-lookup"><span data-stu-id="7ae95-145">document_client.ReadCollection</span></span>](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html#CreateCollection) |
| [<span data-ttu-id="7ae95-146">取得集合的效能層</span><span class="sxs-lookup"><span data-stu-id="7ae95-146">Get performance tier of a collection</span></span>](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/CollectionManagement/Program.py#L139-L161) |[<span data-ttu-id="7ae95-147">DocumentQueryable.QueryOffers</span><span class="sxs-lookup"><span data-stu-id="7ae95-147">DocumentQueryable.QueryOffers</span></span>](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html#CreateCollection) |
| [<span data-ttu-id="7ae95-148">變更集合的效能層</span><span class="sxs-lookup"><span data-stu-id="7ae95-148">Change performance tier of a collection</span></span>](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/CollectionManagement/Program.py#L163-L175) |[<span data-ttu-id="7ae95-149">document_client.ReplaceOffer</span><span class="sxs-lookup"><span data-stu-id="7ae95-149">document_client.ReplaceOffer</span></span>](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html#CreateCollection) |
| [<span data-ttu-id="7ae95-150">刪除集合</span><span class="sxs-lookup"><span data-stu-id="7ae95-150">Delete a collection</span></span>](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/CollectionManagement/Program.py#L212-L225) |[<span data-ttu-id="7ae95-151">document_client.DeleteCollection</span><span class="sxs-lookup"><span data-stu-id="7ae95-151">document_client.DeleteCollection</span></span>](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html#CreateCollection) |

