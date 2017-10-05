---
title: "適用於 Azure Cosmos DB 的 Azure PowerShell 範例 | Microsoft Docs"
description: "Azure PowerShell 範例：協助您建立和管理 Azure Cosmos DB 帳戶的指令碼。"
services: cosmos-db
author: mimig1
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: cosmos-db
ms.custom: mvc
ms.devlang: na
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: database
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: 7698e03c0dc8d1c6d1e926f45e903a909bfd0c93
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="azure-powershell-samples-for-azure-cosmos-db"></a><span data-ttu-id="62c0c-103">適用於 Azure Cosmos DB 的 Azure PowerShell 範例</span><span class="sxs-lookup"><span data-stu-id="62c0c-103">Azure PowerShell samples for Azure Cosmos DB</span></span>

<span data-ttu-id="62c0c-104">下表包含適用於 Azure Cosmos DB 之範例 Azure PowerShell 指令碼的連結。</span><span class="sxs-lookup"><span data-stu-id="62c0c-104">The following table includes links to sample Azure PowerShell scripts for Azure Cosmos DB.</span></span>

| |  |
|---|---|
|<span data-ttu-id="62c0c-105">**建立 Azure Cosmos DB 帳戶**</span><span class="sxs-lookup"><span data-stu-id="62c0c-105">**Create an Azure Cosmos DB account**</span></span>||
|[<span data-ttu-id="62c0c-106">建立 DocumentDB API 帳戶</span><span class="sxs-lookup"><span data-stu-id="62c0c-106">Create a DocumentDB API account</span></span>](scripts/create-database-account-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)| <span data-ttu-id="62c0c-107">建立單一 Azure Cosmos DB 帳戶以搭配 DocumentDB API 使用。</span><span class="sxs-lookup"><span data-stu-id="62c0c-107">Creates a single Azure Cosmos DB account to use with the DocumentDB API.</span></span> |
|<span data-ttu-id="62c0c-108">**調整 Azure Cosmos DB**</span><span class="sxs-lookup"><span data-stu-id="62c0c-108">**Scale Azure Cosmos DB**</span></span>||
|[<span data-ttu-id="62c0c-109">複寫多個區域中的 Azure Cosmos DB 帳戶和設定容錯移轉優先順序</span><span class="sxs-lookup"><span data-stu-id="62c0c-109">Replicate Azure Cosmos DB account in multiple regions and configure failover priorities</span></span>](scripts/scale-multiregion-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)|<span data-ttu-id="62c0c-110">使用指定的容錯移轉優先順序，將帳戶資料複寫到全球多個區域中。</span><span class="sxs-lookup"><span data-stu-id="62c0c-110">Globally replicates account data into multiple regions with a specified failover priority.</span></span>|
|<span data-ttu-id="62c0c-111">**保護 Azure Cosmos DB**</span><span class="sxs-lookup"><span data-stu-id="62c0c-111">**Secure Azure Cosmos DB**</span></span>||
| [<span data-ttu-id="62c0c-112">取得帳戶金鑰</span><span class="sxs-lookup"><span data-stu-id="62c0c-112">Get account keys</span></span>](scripts/secure-get-account-key-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="62c0c-113">取得帳戶主要和次要的主要 (master) 寫入金鑰，以及主要和次要唯讀金鑰。</span><span class="sxs-lookup"><span data-stu-id="62c0c-113">Gets the primary and secondary master write keys and primary and secondary read-only keys for the account.</span></span>|
| [<span data-ttu-id="62c0c-114">取得 MongoDB 連接字串</span><span class="sxs-lookup"><span data-stu-id="62c0c-114">Get MongoDB connection string</span></span>](scripts/secure-mongo-connection-string-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="62c0c-115">取得連接字串以將您的 MongoDB 應用程式連線到 Azure Cosmos DB 帳戶。</span><span class="sxs-lookup"><span data-stu-id="62c0c-115">Gets the connection string to connect your MongoDB app to your Azure Cosmos DB account.</span></span>|
|[<span data-ttu-id="62c0c-116">重新產生帳戶金鑰</span><span class="sxs-lookup"><span data-stu-id="62c0c-116">Regenerate account keys</span></span>](scripts/secure-regenerate-key-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)|<span data-ttu-id="62c0c-117">重新產生帳戶的主要或唯讀金鑰。</span><span class="sxs-lookup"><span data-stu-id="62c0c-117">Regenerates the master or read-only key for the account.</span></span>|
|[<span data-ttu-id="62c0c-118">建立防火牆</span><span class="sxs-lookup"><span data-stu-id="62c0c-118">Create a firewall</span></span>](scripts/create-firewall-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)| <span data-ttu-id="62c0c-119">建立輸入 IP 存取控制原則，以限制從核准的電腦集合和/或雲端服務存取帳戶。</span><span class="sxs-lookup"><span data-stu-id="62c0c-119">Creates an inbound IP access control policy to limit access to the account from an approved set of machines and/or cloud services.</span></span>|
|<span data-ttu-id="62c0c-120">**高可用性、災害復原、備份和還原**</span><span class="sxs-lookup"><span data-stu-id="62c0c-120">**High availability, disaster recovery, backup and restore**</span></span>||
|[<span data-ttu-id="62c0c-121">設定容錯移轉原則</span><span class="sxs-lookup"><span data-stu-id="62c0c-121">Configure failover policy</span></span>](scripts/ha-failover-policy-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)|<span data-ttu-id="62c0c-122">針對要在其中複寫帳戶的每個區域，設定容錯移轉優先順序。</span><span class="sxs-lookup"><span data-stu-id="62c0c-122">Sets the failover priority of each region in which the account is replicated.</span></span>|
|||