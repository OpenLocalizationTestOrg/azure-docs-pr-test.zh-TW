---
title: "適用於 Azure Cosmos DB 的 CLI 範例 aaaAzure |Microsoft 文件"
description: "Azure CLI 範例：建立及管理 Azure Cosmos DB 帳戶、資料庫、容器、區域和防火牆。"
services: cosmos-db
author: mimig1
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: cosmos-db
ms.custom: mvc
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: database
ms.date: 06/07/2017
ms.author: mimig
ms.openlocfilehash: d6eefc3274e0b66eec4e69166bb7d4ddd58a522e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cli-samples-for-azure-cosmos-db"></a><span data-ttu-id="c03fc-103">適用於 Azure Cosmos DB 的 Azure CLI 範例</span><span class="sxs-lookup"><span data-stu-id="c03fc-103">Azure CLI samples for Azure Cosmos DB</span></span>

<span data-ttu-id="c03fc-104">hello 下表包含連結 toosample Azure CLI 指令碼的 Azure Cosmos DB。</span><span class="sxs-lookup"><span data-stu-id="c03fc-104">hello following table includes links toosample Azure CLI scripts for Azure Cosmos DB.</span></span> <span data-ttu-id="c03fc-105">所有 Azure Cosmos DB CLI 命令的參考頁面都使用 hello [Azure CLI 2.0 參考](https://docs.microsoft.com/cli/azure/cosmosdb)。</span><span class="sxs-lookup"><span data-stu-id="c03fc-105">Reference pages for all Azure Cosmos DB CLI commands are available in hello [Azure CLI 2.0 Reference](https://docs.microsoft.com/cli/azure/cosmosdb).</span></span>

| |  |
|---|---|
|<span data-ttu-id="c03fc-106">**建立 Azure Cosmos DB 帳戶、資料庫和容器**</span><span class="sxs-lookup"><span data-stu-id="c03fc-106">**Create Azure Cosmos DB account, database, and containers**</span></span>||
|[<span data-ttu-id="c03fc-107">建立 DocumentDB API、圖形或資料表 API 帳戶</span><span class="sxs-lookup"><span data-stu-id="c03fc-107">Create a DocumentDB API, Graph, or Table API account</span></span>](scripts/create-database-account-collections-cli.md?toc=%2fcli%2fazure%2ftoc.json)| <span data-ttu-id="c03fc-108">以 hello DocumentDB、 圖表或資料表的應用程式開發介面，會建立單一 Azure Cosmos DB API 帳戶、 資料庫和使用的容器。</span><span class="sxs-lookup"><span data-stu-id="c03fc-108">Creates a single Azure Cosmos DB API account, database, and container for use with hello DocumentDB, Graph, or Table APIs.</span></span> |
| [<span data-ttu-id="c03fc-109">建立 MongoDB API 帳戶</span><span class="sxs-lookup"><span data-stu-id="c03fc-109">Create a MongoDB API account</span></span>](scripts/create-mongodb-database-account-cli.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="c03fc-110">建立單一 Azure Cosmos DB MongoDB API 帳戶、資料庫和集合。</span><span class="sxs-lookup"><span data-stu-id="c03fc-110">Creates a single Azure Cosmos DB MongoDB API account, database, and collection.</span></span> |
|<span data-ttu-id="c03fc-111">**調整 Azure Cosmos DB**</span><span class="sxs-lookup"><span data-stu-id="c03fc-111">**Scale Azure Cosmos DB**</span></span>||
| [<span data-ttu-id="c03fc-112">調整容器輸送量</span><span class="sxs-lookup"><span data-stu-id="c03fc-112">Scale container throughput</span></span>](scripts/scale-collection-throughput-cli.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="c03fc-113">變更 hello 佈建 througput 在容器上。</span><span class="sxs-lookup"><span data-stu-id="c03fc-113">Changes hello provisioned througput on a container.</span></span>|
|[<span data-ttu-id="c03fc-114">複寫多個區域中的 Azure Cosmos DB 資料庫帳戶和設定容錯移轉優先順序</span><span class="sxs-lookup"><span data-stu-id="c03fc-114">Replicate Azure Cosmos DB database account in multiple regions and configure failover priorities</span></span>](scripts/scale-multiregion-cli.md?toc=%2fcli%2fazure%2ftoc.json)|<span data-ttu-id="c03fc-115">使用指定的容錯移轉優先順序，將帳戶資料複寫到全球多個區域中。</span><span class="sxs-lookup"><span data-stu-id="c03fc-115">Globally replicates account data into multiple regions with a specified failover priority.</span></span>|
|<span data-ttu-id="c03fc-116">**保護 Azure Cosmos DB**</span><span class="sxs-lookup"><span data-stu-id="c03fc-116">**Secure Azure Cosmos DB**</span></span>||
| [<span data-ttu-id="c03fc-117">取得帳戶金鑰</span><span class="sxs-lookup"><span data-stu-id="c03fc-117">Get account keys</span></span>](scripts/secure-get-account-key-cli.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="c03fc-118">取得 hello 主要和次要的主要寫入索引鍵和主要和次要唯讀金鑰 hello 帳戶。</span><span class="sxs-lookup"><span data-stu-id="c03fc-118">Gets hello primary and secondary master write keys and primary and secondary read-only keys for hello account.</span></span>|
| [<span data-ttu-id="c03fc-119">取得 MongoDB 連接字串</span><span class="sxs-lookup"><span data-stu-id="c03fc-119">Get MongoDB connection string</span></span>](scripts/secure-mongo-connection-string-cli.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="c03fc-120">取得 hello 連接字串 tooconnect 您 MongoDB 應用程式 tooyour Azure Cosmos DB 帳戶。</span><span class="sxs-lookup"><span data-stu-id="c03fc-120">Gets hello connection string tooconnect your MongoDB app tooyour Azure Cosmos DB account.</span></span>|
|[<span data-ttu-id="c03fc-121">重新產生帳戶金鑰</span><span class="sxs-lookup"><span data-stu-id="c03fc-121">Regenerate account keys</span></span>](scripts/secure-regenerate-key-cli.md?toc=%2fcli%2fazure%2ftoc.json)|<span data-ttu-id="c03fc-122">重新產生 hello 主要或唯讀 hello 帳戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="c03fc-122">Regenerates hello master or read-only key for hello account.</span></span>|
|[<span data-ttu-id="c03fc-123">建立防火牆</span><span class="sxs-lookup"><span data-stu-id="c03fc-123">Create a firewall</span></span>](scripts/create-firewall-cli.md?toc=%2fcli%2fazure%2ftoc.json)| <span data-ttu-id="c03fc-124">從機器及/或雲端服務的核准設定組中建立輸入的 IP 存取控制原則 toolimit 存取 toohello 帳戶。</span><span class="sxs-lookup"><span data-stu-id="c03fc-124">Creates an inbound IP access control policy toolimit access toohello account from an approved set of machines and/or cloud services.</span></span>|
|<span data-ttu-id="c03fc-125">**高可用性、災害復原、備份和還原**</span><span class="sxs-lookup"><span data-stu-id="c03fc-125">**High availability, disaster recovery, backup and restore**</span></span>||
|[<span data-ttu-id="c03fc-126">設定容錯移轉原則</span><span class="sxs-lookup"><span data-stu-id="c03fc-126">Configure failover policy</span></span>](scripts/ha-failover-policy-cli.md?toc=%2fcli%2fazure%2ftoc.json)|<span data-ttu-id="c03fc-127">設定 hello hello 帳戶複寫所在的每個區域的容錯移轉優先權。</span><span class="sxs-lookup"><span data-stu-id="c03fc-127">Sets hello failover priority of each region in which hello account is replicated.</span></span>|
|<span data-ttu-id="c03fc-128">**將 Azure Cosmos DB 連線到資源**</span><span class="sxs-lookup"><span data-stu-id="c03fc-128">**Connect Azure Cosmos DB to resources**</span></span>||
|[<span data-ttu-id="c03fc-129">連接 web 應用程式 tooAzure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="c03fc-129">Connect a web app tooAzure Cosmos DB</span></span>](https://docs.microsoft.com/azure/app-service-web/scripts/app-service-cli-app-service-documentdb?toc=%2fcli%2fazure%2ftoc.json)|<span data-ttu-id="c03fc-130">建立 Azure Cosmos DB 資料庫和 Azure Web 應用程式並將兩者連線。</span><span class="sxs-lookup"><span data-stu-id="c03fc-130">Create and connect an Azure Cosmos DB database and an Azure web app.</span></span>|
|||
