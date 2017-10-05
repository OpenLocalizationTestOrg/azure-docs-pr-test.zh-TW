---
title: "Azure CLI 指令碼範例 - 建立具有叢集的 Premium Azure Redis 快取 | Microsoft Docs"
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
ms.openlocfilehash: 87d0fe4c3eaa8f7b75343a36a069ecdac8241d74
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-premium-azure-redis-cache-with-clustering"></a><span data-ttu-id="e4ac7-103">建立具有叢集的 Premium Azure Redis 快取</span><span class="sxs-lookup"><span data-stu-id="e4ac7-103">Create a Premium Azure Redis Cache with clustering</span></span>

<span data-ttu-id="e4ac7-104">在此案例中，您將學習如何建立啟用叢集和兩分區的 6 GB Premium 層 Azure Redis 快取。</span><span class="sxs-lookup"><span data-stu-id="e4ac7-104">In this scenario, you learn how to create a 6 GB Premium tier Azure Redis Cache with clustering enabled and two shards.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

## <a name="sample-script"></a><span data-ttu-id="e4ac7-105">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="e4ac7-105">Sample script</span></span>

<span data-ttu-id="e4ac7-106">[!code-azurecli[主要](../../../cli_scripts/redis-cache/create-premium-cache-cluster/create-premium-cache-cluster.sh "Azure Redis 快取")]</span><span class="sxs-lookup"><span data-stu-id="e4ac7-106">[!code-azurecli[main](../../../cli_scripts/redis-cache/create-premium-cache-cluster/create-premium-cache-cluster.sh "Azure Redis Cache")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/redis-cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="e4ac7-107">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="e4ac7-107">Script explanation</span></span>

<span data-ttu-id="e4ac7-108">此指令碼使用下列命令來建立資源群組和啟用叢集的 Premium 層 redis 快取。</span><span class="sxs-lookup"><span data-stu-id="e4ac7-108">This script uses the following commands to create a resource group and a Premium tier redis cache with clustering enable.</span></span> <span data-ttu-id="e4ac7-109">下表中的每個命令都會連結至命令特定的文件。</span><span class="sxs-lookup"><span data-stu-id="e4ac7-109">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="e4ac7-110">命令</span><span class="sxs-lookup"><span data-stu-id="e4ac7-110">Command</span></span> | <span data-ttu-id="e4ac7-111">注意事項</span><span class="sxs-lookup"><span data-stu-id="e4ac7-111">Notes</span></span> |
|---|---|
| [<span data-ttu-id="e4ac7-112">az group create</span><span class="sxs-lookup"><span data-stu-id="e4ac7-112">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="e4ac7-113">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="e4ac7-113">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="e4ac7-114">az redis create</span><span class="sxs-lookup"><span data-stu-id="e4ac7-114">az redis create</span></span>](https://docs.microsoft.com/cli/azure/redis#create) | <span data-ttu-id="e4ac7-115">建立 Redis 快取執行個體。</span><span class="sxs-lookup"><span data-stu-id="e4ac7-115">Create Redis Cache instance.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="e4ac7-116">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e4ac7-116">Next steps</span></span>

<span data-ttu-id="e4ac7-117">如需 Azure CLI 的詳細資訊，請參閱 [Azure CLI 文件](https://docs.microsoft.com/cli/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="e4ac7-117">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="e4ac7-118">您可以在 [Azure Redis Cache 文件](../cli-samples.md)中找到其他 Azure Redis Cache CLI 指令碼範例。</span><span class="sxs-lookup"><span data-stu-id="e4ac7-118">Additional Azure Redis Cache CLI script samples can be found in the [Azure Redis Cache documentation](../cli-samples.md).</span></span>