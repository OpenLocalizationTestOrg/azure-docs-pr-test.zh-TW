---
title: "Azure CLI 指令碼範例 - 取得 Azure Redis 快取的詳細資料 | Microsoft Docs"
description: "Azure CLI 指令碼範例 - 取得 Azure Redis 快取的詳細資料"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
tags: azure-service-management
ms.assetid: 155924e6-00d5-4a8c-ba99-5189f300464a
ms.service: cache-redis
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 04/14/2017
ms.author: sdanie
ms.openlocfilehash: 9f4eb32227bd8a68837eabd58b9d058bc4995d17
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="get-details-of-an-azure-redis-cache"></a><span data-ttu-id="78853-103">取得 Azure Redis 快取的詳細資料</span><span class="sxs-lookup"><span data-stu-id="78853-103">Get details of an Azure Redis Cache</span></span>

<span data-ttu-id="78853-104">在此案例中，您將了解關於如何擷取 Azure Redis 快取執行個體 (包括其佈建狀態) 的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="78853-104">In this scenario, you learn how to retrieve the details of an Azure Redis Cache instance, including its provisioning status.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

## <a name="sample-script"></a><span data-ttu-id="78853-105">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="78853-105">Sample script</span></span>

<span data-ttu-id="78853-106">[!code-azurecli[主要](../../../cli_scripts/redis-cache/show-cache/show-cache.sh "Azure Redis 快取")]</span><span class="sxs-lookup"><span data-stu-id="78853-106">[!code-azurecli[main](../../../cli_scripts/redis-cache/show-cache/show-cache.sh "Azure Redis Cache")]</span></span>

## <a name="script-explanation"></a><span data-ttu-id="78853-107">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="78853-107">Script explanation</span></span>

<span data-ttu-id="78853-108">此指令碼會使用下列命令，擷取 Azure Redis 快取執行個體的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="78853-108">This script uses the following commands to retrieve the details of an Azure Redis Cache instance.</span></span> <span data-ttu-id="78853-109">下表中的每個命令都會連結至命令特定的文件。</span><span class="sxs-lookup"><span data-stu-id="78853-109">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="78853-110">命令</span><span class="sxs-lookup"><span data-stu-id="78853-110">Command</span></span> | <span data-ttu-id="78853-111">注意事項</span><span class="sxs-lookup"><span data-stu-id="78853-111">Notes</span></span> |
|---|---|
| [<span data-ttu-id="78853-112">az redis show</span><span class="sxs-lookup"><span data-stu-id="78853-112">az redis show</span></span>](https://docs.microsoft.com/cli/azure/redis#show) | <span data-ttu-id="78853-113">取得 Azure Redis Cache 執行個體的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="78853-113">Retrieve details of an Azure Redis Cache instance.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="78853-114">後續步驟</span><span class="sxs-lookup"><span data-stu-id="78853-114">Next steps</span></span>

<span data-ttu-id="78853-115">如需 Azure CLI 的詳細資訊，請參閱 [Azure CLI 文件](https://docs.microsoft.com/cli/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="78853-115">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="78853-116">您可以在 [Azure Redis Cache 文件](../cli-samples.md)中找到其他 Azure Redis Cache CLI 指令碼範例。</span><span class="sxs-lookup"><span data-stu-id="78853-116">Additional Azure Redis Cache CLI script samples can be found in the [Azure Redis Cache documentation](../cli-samples.md).</span></span>