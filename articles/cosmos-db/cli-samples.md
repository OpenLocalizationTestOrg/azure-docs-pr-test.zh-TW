---
title: "適用於 Azure Cosmos DB 的 Azure CLI 範例 | Microsoft Docs"
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
ms.openlocfilehash: 709d2ccce0f4b9827a8076f683c7e0f74cbdd4ea
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="azure-cli-samples-for-azure-cosmos-db"></a><span data-ttu-id="90b5a-103">適用於 Azure Cosmos DB 的 Azure CLI 範例</span><span class="sxs-lookup"><span data-stu-id="90b5a-103">Azure CLI samples for Azure Cosmos DB</span></span>

<span data-ttu-id="90b5a-104">下表包含適用於 Azure Cosmos DB 之範例 Azure CLI 指令碼的連結。</span><span class="sxs-lookup"><span data-stu-id="90b5a-104">The following table includes links to sample Azure CLI scripts for Azure Cosmos DB.</span></span> <span data-ttu-id="90b5a-105">您可以在 [Azure CLI 2.0 參考](https://docs.microsoft.com/cli/azure/cosmosdb)中取得所有 Azure Cosmos DB CLI 命令的參考頁面。</span><span class="sxs-lookup"><span data-stu-id="90b5a-105">Reference pages for all Azure Cosmos DB CLI commands are available in the [Azure CLI 2.0 Reference](https://docs.microsoft.com/cli/azure/cosmosdb).</span></span>

| |  |
|---|---|
|<span data-ttu-id="90b5a-106">**建立 Azure Cosmos DB 帳戶、資料庫和容器**</span><span class="sxs-lookup"><span data-stu-id="90b5a-106">**Create Azure Cosmos DB account, database, and containers**</span></span>||
|[<span data-ttu-id="90b5a-107">建立 DocumentDB API、圖形或資料表 API 帳戶</span><span class="sxs-lookup"><span data-stu-id="90b5a-107">Create a DocumentDB API, Graph, or Table API account</span></span>](scripts/create-database-account-collections-cli.md?toc=%2fcli%2fazure%2ftoc.json)| <span data-ttu-id="90b5a-108">建立單一 Azure Cosmos DB API 帳戶、資料庫和容器，以便與 DocumentDB、圖形或資料表 API 搭配使用。</span><span class="sxs-lookup"><span data-stu-id="90b5a-108">Creates a single Azure Cosmos DB API account, database, and container for use with the DocumentDB, Graph, or Table APIs.</span></span> |
| [<span data-ttu-id="90b5a-109">建立 MongoDB API 帳戶</span><span class="sxs-lookup"><span data-stu-id="90b5a-109">Create a MongoDB API account</span></span>](scripts/create-mongodb-database-account-cli.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="90b5a-110">建立單一 Azure Cosmos DB MongoDB API 帳戶、資料庫和集合。</span><span class="sxs-lookup"><span data-stu-id="90b5a-110">Creates a single Azure Cosmos DB MongoDB API account, database, and collection.</span></span> |
|<span data-ttu-id="90b5a-111">**調整 Azure Cosmos DB**</span><span class="sxs-lookup"><span data-stu-id="90b5a-111">**Scale Azure Cosmos DB**</span></span>||
| [<span data-ttu-id="90b5a-112">調整容器輸送量</span><span class="sxs-lookup"><span data-stu-id="90b5a-112">Scale container throughput</span></span>](scripts/scale-collection-throughput-cli.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="90b5a-113">變更容器的已佈建輸送量。</span><span class="sxs-lookup"><span data-stu-id="90b5a-113">Changes the provisioned througput on a container.</span></span>|
|[<span data-ttu-id="90b5a-114">複寫多個區域中的 Azure Cosmos DB 資料庫帳戶和設定容錯移轉優先順序</span><span class="sxs-lookup"><span data-stu-id="90b5a-114">Replicate Azure Cosmos DB database account in multiple regions and configure failover priorities</span></span>](scripts/scale-multiregion-cli.md?toc=%2fcli%2fazure%2ftoc.json)|<span data-ttu-id="90b5a-115">使用指定的容錯移轉優先順序，將帳戶資料複寫到全球多個區域中。</span><span class="sxs-lookup"><span data-stu-id="90b5a-115">Globally replicates account data into multiple regions with a specified failover priority.</span></span>|
|<span data-ttu-id="90b5a-116">**保護 Azure Cosmos DB**</span><span class="sxs-lookup"><span data-stu-id="90b5a-116">**Secure Azure Cosmos DB**</span></span>||
| [<span data-ttu-id="90b5a-117">取得帳戶金鑰</span><span class="sxs-lookup"><span data-stu-id="90b5a-117">Get account keys</span></span>](scripts/secure-get-account-key-cli.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="90b5a-118">取得帳戶主要和次要的主要 (master) 寫入金鑰，以及主要和次要唯讀金鑰。</span><span class="sxs-lookup"><span data-stu-id="90b5a-118">Gets the primary and secondary master write keys and primary and secondary read-only keys for the account.</span></span>|
| [<span data-ttu-id="90b5a-119">取得 MongoDB 連接字串</span><span class="sxs-lookup"><span data-stu-id="90b5a-119">Get MongoDB connection string</span></span>](scripts/secure-mongo-connection-string-cli.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="90b5a-120">取得連接字串以將您的 MongoDB 應用程式連線到 Azure Cosmos DB 帳戶。</span><span class="sxs-lookup"><span data-stu-id="90b5a-120">Gets the connection string to connect your MongoDB app to your Azure Cosmos DB account.</span></span>|
|[<span data-ttu-id="90b5a-121">重新產生帳戶金鑰</span><span class="sxs-lookup"><span data-stu-id="90b5a-121">Regenerate account keys</span></span>](scripts/secure-regenerate-key-cli.md?toc=%2fcli%2fazure%2ftoc.json)|<span data-ttu-id="90b5a-122">重新產生帳戶的主要或唯讀金鑰。</span><span class="sxs-lookup"><span data-stu-id="90b5a-122">Regenerates the master or read-only key for the account.</span></span>|
|[<span data-ttu-id="90b5a-123">建立防火牆</span><span class="sxs-lookup"><span data-stu-id="90b5a-123">Create a firewall</span></span>](scripts/create-firewall-cli.md?toc=%2fcli%2fazure%2ftoc.json)| <span data-ttu-id="90b5a-124">建立輸入 IP 存取控制原則，以限制從核准的電腦集合和/或雲端服務存取帳戶。</span><span class="sxs-lookup"><span data-stu-id="90b5a-124">Creates an inbound IP access control policy to limit access to the account from an approved set of machines and/or cloud services.</span></span>|
|<span data-ttu-id="90b5a-125">**高可用性、災害復原、備份和還原**</span><span class="sxs-lookup"><span data-stu-id="90b5a-125">**High availability, disaster recovery, backup and restore**</span></span>||
|[<span data-ttu-id="90b5a-126">設定容錯移轉原則</span><span class="sxs-lookup"><span data-stu-id="90b5a-126">Configure failover policy</span></span>](scripts/ha-failover-policy-cli.md?toc=%2fcli%2fazure%2ftoc.json)|<span data-ttu-id="90b5a-127">針對要在其中複寫帳戶的每個區域，設定容錯移轉優先順序。</span><span class="sxs-lookup"><span data-stu-id="90b5a-127">Sets the failover priority of each region in which the account is replicated.</span></span>|
|<span data-ttu-id="90b5a-128">**將 Azure Cosmos DB 連線到資源**</span><span class="sxs-lookup"><span data-stu-id="90b5a-128">**Connect Azure Cosmos DB to resources**</span></span>||
|[<span data-ttu-id="90b5a-129">將 Web 應用程式連線到 Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="90b5a-129">Connect a web app to Azure Cosmos DB</span></span>](https://docs.microsoft.com/azure/app-service-web/scripts/app-service-cli-app-service-documentdb?toc=%2fcli%2fazure%2ftoc.json)|<span data-ttu-id="90b5a-130">建立 Azure Cosmos DB 資料庫和 Azure Web 應用程式並將兩者連線。</span><span class="sxs-lookup"><span data-stu-id="90b5a-130">Create and connect an Azure Cosmos DB database and an Azure web app.</span></span>|
|||
