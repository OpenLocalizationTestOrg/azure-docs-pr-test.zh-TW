---
title: "CLI 指令碼範例-取得 hello 主機名稱、 通訊埠，以及 Azure Redis 快取的索引鍵 aaaAzure |Microsoft 文件"
description: "Azure CLI 指令碼範例-取得 hello 主機名稱、 通訊埠，以及 Azure Redis 快取執行個體的金鑰"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
tags: azure-service-management
ms.assetid: 761eb24e-2ba7-418d-8fc3-431153e69a90
ms.service: cache-redis
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 04/14/2017
ms.author: sdanie
ms.openlocfilehash: e6e794558087d6568438c439e2bf99fc46eeb8bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-hostname-ports-and-keys-for-azure-redis-cache"></a><span data-ttu-id="b8651-103">Azure Redis 快取中取得 hello 主機名稱、 通訊埠，以及索引鍵</span><span class="sxs-lookup"><span data-stu-id="b8651-103">Get hello hostname, ports, and keys for Azure Redis Cache</span></span>

<span data-ttu-id="b8651-104">在此案例中，您學會 tooretrieve hello 主機名稱、 連接埠和金鑰使用方式 tooconnect tooan Azure Redis 快取執行個體。</span><span class="sxs-lookup"><span data-stu-id="b8651-104">In this scenario, you learn how tooretrieve hello hostname, ports, and keys used tooconnect tooan Azure Redis Cache instance.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

## <a name="sample-script"></a><span data-ttu-id="b8651-105">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="b8651-105">Sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/redis-cache/cache-keys-ports/cache-keys-ports.sh "Azure Redis Cache")]


## <a name="script-explanation"></a><span data-ttu-id="b8651-106">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="b8651-106">Script explanation</span></span>

<span data-ttu-id="b8651-107">此指令碼會使用下列命令 tooretrieve hello 主機名稱、 金鑰和 Azure Redis 快取執行個體的連接埠的 hello。</span><span class="sxs-lookup"><span data-stu-id="b8651-107">This script uses hello following commands tooretrieve hello hostname, keys, and ports of an Azure Redis Cache instance.</span></span> <span data-ttu-id="b8651-108">Hello 資料表連結 toocommand 特定文件中的每個命令。</span><span class="sxs-lookup"><span data-stu-id="b8651-108">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="b8651-109">命令</span><span class="sxs-lookup"><span data-stu-id="b8651-109">Command</span></span> | <span data-ttu-id="b8651-110">注意事項</span><span class="sxs-lookup"><span data-stu-id="b8651-110">Notes</span></span> |
|---|---|
| [<span data-ttu-id="b8651-111">az redis show</span><span class="sxs-lookup"><span data-stu-id="b8651-111">az redis show</span></span>](https://docs.microsoft.com/cli/azure/redis#show) | <span data-ttu-id="b8651-112">取得 Azure Redis Cache 執行個體的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="b8651-112">Retrieve details of an Azure Redis Cache instance.</span></span> |
| [<span data-ttu-id="b8651-113">az redis list-keys</span><span class="sxs-lookup"><span data-stu-id="b8651-113">az redis list-keys</span></span>](https://docs.microsoft.com/cli/azure/redis#list-keys) | <span data-ttu-id="b8651-114">取得 Azure Redis Cache 執行個體的存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="b8651-114">Retrieve access keys for an Azure Redis Cache instance.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="b8651-115">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b8651-115">Next steps</span></span>

<span data-ttu-id="b8651-116">如需有關 Azure CLI hello 的詳細資訊，請參閱[Azure CLI 文件](https://docs.microsoft.com/cli/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="b8651-116">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="b8651-117">其他的 Azure Redis 快取 CLI 指令碼範例可以在 hello [Azure Redis 快取文件](../cli-samples.md)。</span><span class="sxs-lookup"><span data-stu-id="b8651-117">Additional Azure Redis Cache CLI script samples can be found in hello [Azure Redis Cache documentation](../cli-samples.md).</span></span>
