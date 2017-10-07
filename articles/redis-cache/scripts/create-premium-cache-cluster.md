---
title: "aaaAzure CLI 指令碼範例-建立 Premium Azure Redis 快取叢集 |Microsoft 文件"
description: "Azure CLI 指令碼範例 - 建立具有叢集的 Premium 層 Azure Redis 快取"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
tags: azure-service-management
ms.assetid: 07bcceae-2521-4fe3-b88f-ed833104ddd2
ms.service: cache-redis
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 04/14/2017
ms.author: sdanie
ms.openlocfilehash: ca34d40059b282cb2abc7e3e2b8771226029744c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-premium-azure-redis-cache-with-clustering"></a><span data-ttu-id="d0b8f-103">建立具有叢集的 Premium Azure Redis 快取</span><span class="sxs-lookup"><span data-stu-id="d0b8f-103">Create a Premium Azure Redis Cache with clustering</span></span>

<span data-ttu-id="d0b8f-104">在此案例中，您將學會如何 toocreate 6 GB Premium 層 Azure Redis 快取叢集啟用和兩個分區。</span><span class="sxs-lookup"><span data-stu-id="d0b8f-104">In this scenario, you learn how toocreate a 6 GB Premium tier Azure Redis Cache with clustering enabled and two shards.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

## <a name="sample-script"></a><span data-ttu-id="d0b8f-105">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="d0b8f-105">Sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/redis-cache/create-premium-cache-cluster/create-premium-cache-cluster.sh "Azure Redis Cache")]

[!INCLUDE [cli-script-clean-up](../../../includes/redis-cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="d0b8f-106">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="d0b8f-106">Script explanation</span></span>

<span data-ttu-id="d0b8f-107">此指令碼會使用下列命令 toocreate hello 資源群組和 Premium 層 redis 快取叢集啟用。</span><span class="sxs-lookup"><span data-stu-id="d0b8f-107">This script uses hello following commands toocreate a resource group and a Premium tier redis cache with clustering enable.</span></span> <span data-ttu-id="d0b8f-108">Hello 資料表連結 toocommand 特定文件中的每個命令。</span><span class="sxs-lookup"><span data-stu-id="d0b8f-108">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="d0b8f-109">命令</span><span class="sxs-lookup"><span data-stu-id="d0b8f-109">Command</span></span> | <span data-ttu-id="d0b8f-110">注意事項</span><span class="sxs-lookup"><span data-stu-id="d0b8f-110">Notes</span></span> |
|---|---|
| [<span data-ttu-id="d0b8f-111">az group create</span><span class="sxs-lookup"><span data-stu-id="d0b8f-111">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="d0b8f-112">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="d0b8f-112">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="d0b8f-113">az redis create</span><span class="sxs-lookup"><span data-stu-id="d0b8f-113">az redis create</span></span>](https://docs.microsoft.com/cli/azure/redis#create) | <span data-ttu-id="d0b8f-114">建立 Redis 快取執行個體。</span><span class="sxs-lookup"><span data-stu-id="d0b8f-114">Create Redis Cache instance.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="d0b8f-115">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d0b8f-115">Next steps</span></span>

<span data-ttu-id="d0b8f-116">如需有關 Azure CLI hello 的詳細資訊，請參閱[Azure CLI 文件](https://docs.microsoft.com/cli/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="d0b8f-116">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="d0b8f-117">其他的 Azure Redis 快取 CLI 指令碼範例可以在 hello [Azure Redis 快取文件](../cli-samples.md)。</span><span class="sxs-lookup"><span data-stu-id="d0b8f-117">Additional Azure Redis Cache CLI script samples can be found in hello [Azure Redis Cache documentation](../cli-samples.md).</span></span>
