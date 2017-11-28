---
title: "PowerShell 範例，讓 Azure Cosmos DB aaaAzure |Microsoft 文件"
description: "Azure 的 PowerShell 範例-指令碼 toohelp 您建立及管理 Azure Cosmos DB 帳戶。"
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
ms.openlocfilehash: 8815e775f720226e98cc8dcf7743e481c213272b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-powershell-samples-for-azure-cosmos-db"></a><span data-ttu-id="85ef7-103">適用於 Azure Cosmos DB 的 Azure PowerShell 範例</span><span class="sxs-lookup"><span data-stu-id="85ef7-103">Azure PowerShell samples for Azure Cosmos DB</span></span>

<span data-ttu-id="85ef7-104">hello 下表包含連結 toosample Azure PowerShell 指令碼的 Azure Cosmos DB。</span><span class="sxs-lookup"><span data-stu-id="85ef7-104">hello following table includes links toosample Azure PowerShell scripts for Azure Cosmos DB.</span></span>

| |  |
|---|---|
|<span data-ttu-id="85ef7-105">**建立 Azure Cosmos DB 帳戶**</span><span class="sxs-lookup"><span data-stu-id="85ef7-105">**Create an Azure Cosmos DB account**</span></span>||
|[<span data-ttu-id="85ef7-106">建立 DocumentDB API 帳戶</span><span class="sxs-lookup"><span data-stu-id="85ef7-106">Create a DocumentDB API account</span></span>](scripts/create-database-account-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)| <span data-ttu-id="85ef7-107">建立單一的 Azure Cosmos DB 帳戶 toouse 以 hello DocumentDB API。</span><span class="sxs-lookup"><span data-stu-id="85ef7-107">Creates a single Azure Cosmos DB account toouse with hello DocumentDB API.</span></span> |
|<span data-ttu-id="85ef7-108">**調整 Azure Cosmos DB**</span><span class="sxs-lookup"><span data-stu-id="85ef7-108">**Scale Azure Cosmos DB**</span></span>||
|[<span data-ttu-id="85ef7-109">複寫多個區域中的 Azure Cosmos DB 帳戶和設定容錯移轉優先順序</span><span class="sxs-lookup"><span data-stu-id="85ef7-109">Replicate Azure Cosmos DB account in multiple regions and configure failover priorities</span></span>](scripts/scale-multiregion-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)|<span data-ttu-id="85ef7-110">使用指定的容錯移轉優先順序，將帳戶資料複寫到全球多個區域中。</span><span class="sxs-lookup"><span data-stu-id="85ef7-110">Globally replicates account data into multiple regions with a specified failover priority.</span></span>|
|<span data-ttu-id="85ef7-111">**保護 Azure Cosmos DB**</span><span class="sxs-lookup"><span data-stu-id="85ef7-111">**Secure Azure Cosmos DB**</span></span>||
| [<span data-ttu-id="85ef7-112">取得帳戶金鑰</span><span class="sxs-lookup"><span data-stu-id="85ef7-112">Get account keys</span></span>](scripts/secure-get-account-key-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="85ef7-113">取得 hello 主要和次要的主要寫入索引鍵和主要和次要唯讀金鑰 hello 帳戶。</span><span class="sxs-lookup"><span data-stu-id="85ef7-113">Gets hello primary and secondary master write keys and primary and secondary read-only keys for hello account.</span></span>|
| [<span data-ttu-id="85ef7-114">取得 MongoDB 連接字串</span><span class="sxs-lookup"><span data-stu-id="85ef7-114">Get MongoDB connection string</span></span>](scripts/secure-mongo-connection-string-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="85ef7-115">取得 hello 連接字串 tooconnect 您 MongoDB 應用程式 tooyour Azure Cosmos DB 帳戶。</span><span class="sxs-lookup"><span data-stu-id="85ef7-115">Gets hello connection string tooconnect your MongoDB app tooyour Azure Cosmos DB account.</span></span>|
|[<span data-ttu-id="85ef7-116">重新產生帳戶金鑰</span><span class="sxs-lookup"><span data-stu-id="85ef7-116">Regenerate account keys</span></span>](scripts/secure-regenerate-key-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)|<span data-ttu-id="85ef7-117">重新產生 hello 主要或唯讀 hello 帳戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="85ef7-117">Regenerates hello master or read-only key for hello account.</span></span>|
|[<span data-ttu-id="85ef7-118">建立防火牆</span><span class="sxs-lookup"><span data-stu-id="85ef7-118">Create a firewall</span></span>](scripts/create-firewall-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)| <span data-ttu-id="85ef7-119">從機器及/或雲端服務的核准設定組中建立輸入的 IP 存取控制原則 toolimit 存取 toohello 帳戶。</span><span class="sxs-lookup"><span data-stu-id="85ef7-119">Creates an inbound IP access control policy toolimit access toohello account from an approved set of machines and/or cloud services.</span></span>|
|<span data-ttu-id="85ef7-120">**高可用性、災害復原、備份和還原**</span><span class="sxs-lookup"><span data-stu-id="85ef7-120">**High availability, disaster recovery, backup and restore**</span></span>||
|[<span data-ttu-id="85ef7-121">設定容錯移轉原則</span><span class="sxs-lookup"><span data-stu-id="85ef7-121">Configure failover policy</span></span>](scripts/ha-failover-policy-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)|<span data-ttu-id="85ef7-122">設定 hello hello 帳戶複寫所在的每個區域的容錯移轉優先權。</span><span class="sxs-lookup"><span data-stu-id="85ef7-122">Sets hello failover priority of each region in which hello account is replicated.</span></span>|
|||