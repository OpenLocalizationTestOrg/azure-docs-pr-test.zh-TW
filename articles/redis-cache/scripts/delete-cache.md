---
title: "Azure CLI 指令碼範例 - 刪除 Azure Redis 快取 | Microsoft Docs"
description: "Azure CLI 指令碼範例 - 刪除 Azure Redis 快取"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
tags: azure-service-management
ms.assetid: 7beded7a-d2c9-43a6-b3b4-b8079c11de4a
ms.service: cache-redis
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 04/14/2017
ms.author: sdanie
ms.openlocfilehash: f959823b3a7c5b0262f693ecad1e6efc4eec4f35
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="delete-an-azure-redis-cache"></a><span data-ttu-id="492f0-103">刪除 Azure Redis 快取</span><span class="sxs-lookup"><span data-stu-id="492f0-103">Delete an Azure Redis Cache</span></span>

<span data-ttu-id="492f0-104">在此案例中，您會了解如何刪除 Azure Redis 快取。</span><span class="sxs-lookup"><span data-stu-id="492f0-104">In this scenario, you learn how to delete an Azure Redis Cache.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

## <a name="sample-script"></a><span data-ttu-id="492f0-105">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="492f0-105">Sample script</span></span>

<span data-ttu-id="492f0-106">[!code-azurecli[主要](../../../cli_scripts/redis-cache/delete-cache/delete-cache.sh "Azure Redis 快取")]</span><span class="sxs-lookup"><span data-stu-id="492f0-106">[!code-azurecli[main](../../../cli_scripts/redis-cache/delete-cache/delete-cache.sh "Azure Redis Cache")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/redis-cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="492f0-107">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="492f0-107">Script explanation</span></span>

<span data-ttu-id="492f0-108">此指令碼會使用下列命令，刪除 Azure Redis 快取執行個體。</span><span class="sxs-lookup"><span data-stu-id="492f0-108">This script uses the following commands to delete an Azure Redis Cache instance.</span></span> <span data-ttu-id="492f0-109">下表中的每個命令都會連結至命令特定的文件。</span><span class="sxs-lookup"><span data-stu-id="492f0-109">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="492f0-110">命令</span><span class="sxs-lookup"><span data-stu-id="492f0-110">Command</span></span> | <span data-ttu-id="492f0-111">注意事項</span><span class="sxs-lookup"><span data-stu-id="492f0-111">Notes</span></span> |
|---|---|
| [<span data-ttu-id="492f0-112">az redis 刪除</span><span class="sxs-lookup"><span data-stu-id="492f0-112">az redis delete</span></span>](https://docs.microsoft.com/cli/azure/redis#delete) | <span data-ttu-id="492f0-113">刪除 Redis 快取執行個體。</span><span class="sxs-lookup"><span data-stu-id="492f0-113">Delete Redis Cache instance.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="492f0-114">後續步驟</span><span class="sxs-lookup"><span data-stu-id="492f0-114">Next steps</span></span>

<span data-ttu-id="492f0-115">如需 Azure CLI 的詳細資訊，請參閱 [Azure CLI 文件](https://docs.microsoft.com/cli/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="492f0-115">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="492f0-116">您可以在 [Azure Redis Cache 文件](../cli-samples.md)中找到其他 Azure Redis Cache CLI 指令碼範例。</span><span class="sxs-lookup"><span data-stu-id="492f0-116">Additional Azure Redis Cache CLI script samples can be found in the [Azure Redis Cache documentation](../cli-samples.md).</span></span>