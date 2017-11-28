---
title: "Azure CLI 指令碼範例 - 建立 Azure Redis 快取 | Microsoft Docs"
description: "Azure CLI 指令碼範例 - 建立 Azure Redis 快取"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
tags: azure-service-management
ms.assetid: afd7f6e0-9297-4c98-a95e-597be939cef7
ms.service: cache-redis
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 04/14/2017
ms.author: sdanie
ms.openlocfilehash: c6b153d80de4cbf2bec1bc70d67be7befa0c5ec3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-azure-redis-cache"></a><span data-ttu-id="fa9ca-103">建立 Azure Redis 快取</span><span class="sxs-lookup"><span data-stu-id="fa9ca-103">Create an Azure Redis Cache</span></span>

<span data-ttu-id="fa9ca-104">在此案例中，您會了解如何建立 Azure Redis 快取。</span><span class="sxs-lookup"><span data-stu-id="fa9ca-104">In this scenario, you learn how to create an Azure Redis Cache.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

## <a name="sample-script"></a><span data-ttu-id="fa9ca-105">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="fa9ca-105">Sample script</span></span>

<span data-ttu-id="fa9ca-106">[!code-azurecli[主要](../../../cli_scripts/redis-cache/create-cache/create-cache.sh "Azure Redis 快取")]</span><span class="sxs-lookup"><span data-stu-id="fa9ca-106">[!code-azurecli[main](../../../cli_scripts/redis-cache/create-cache/create-cache.sh "Azure Redis Cache")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/redis-cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="fa9ca-107">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="fa9ca-107">Script explanation</span></span>

<span data-ttu-id="fa9ca-108">此指令碼使用下列命令來建立資源群組與 redis 快取。</span><span class="sxs-lookup"><span data-stu-id="fa9ca-108">This script uses the following commands to create a resource group and a redis cache.</span></span> <span data-ttu-id="fa9ca-109">下表中的每個命令都會連結至命令特定的文件。</span><span class="sxs-lookup"><span data-stu-id="fa9ca-109">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="fa9ca-110">命令</span><span class="sxs-lookup"><span data-stu-id="fa9ca-110">Command</span></span> | <span data-ttu-id="fa9ca-111">注意事項</span><span class="sxs-lookup"><span data-stu-id="fa9ca-111">Notes</span></span> |
|---|---|
| [<span data-ttu-id="fa9ca-112">az group create</span><span class="sxs-lookup"><span data-stu-id="fa9ca-112">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="fa9ca-113">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="fa9ca-113">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="fa9ca-114">az redis create</span><span class="sxs-lookup"><span data-stu-id="fa9ca-114">az redis create</span></span>](https://docs.microsoft.com/cli/azure/redis#create) | <span data-ttu-id="fa9ca-115">建立 Redis 快取執行個體。</span><span class="sxs-lookup"><span data-stu-id="fa9ca-115">Create Redis Cache instance.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="fa9ca-116">後續步驟</span><span class="sxs-lookup"><span data-stu-id="fa9ca-116">Next steps</span></span>

<span data-ttu-id="fa9ca-117">如需 Azure CLI 的詳細資訊，請參閱 [Azure CLI 文件](https://docs.microsoft.com/cli/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="fa9ca-117">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="fa9ca-118">您可以在 [Azure Redis Cache 文件](../cli-samples.md)中找到其他 Azure Redis Cache CLI 指令碼範例。</span><span class="sxs-lookup"><span data-stu-id="fa9ca-118">Additional Azure Redis Cache CLI script samples can be found in the [Azure Redis Cache documentation](../cli-samples.md).</span></span>