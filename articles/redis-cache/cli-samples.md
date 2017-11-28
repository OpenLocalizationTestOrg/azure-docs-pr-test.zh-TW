---
title: "Azure CLI Redis Cache 範例 | Microsoft Docs"
description: "Azure Redis Cache 的 Azure CLI 範例。"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 8d2de145-50c0-4f76-bf8f-fdf679f03698
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: azurecli
ms.topic: article
ms.date: 04/14/2017
ms.author: sdanie
ms.openlocfilehash: a3debf3380b57faa5b7b30f612698fe6de5b7067
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="azure-cli-samples-for-azure-redis-cache"></a><span data-ttu-id="9feae-103">Azure Redis Cache 的 Azure CLI 範例</span><span class="sxs-lookup"><span data-stu-id="9feae-103">Azure CLI Samples for Azure Redis Cache</span></span>

<span data-ttu-id="9feae-104">下表包含使用 Azure CLI 所建置之 Bash 指令碼的連結。</span><span class="sxs-lookup"><span data-stu-id="9feae-104">The following table includes links to bash scripts built using the Azure CLI.</span></span>

| | |
|---|---|
|<span data-ttu-id="9feae-105">**建立快取**</span><span class="sxs-lookup"><span data-stu-id="9feae-105">**Create cache**</span></span>||
| [<span data-ttu-id="9feae-106">建立快取</span><span class="sxs-lookup"><span data-stu-id="9feae-106">Create a cache</span></span>](./scripts/create-cache.md) | <span data-ttu-id="9feae-107">建立資源群組和基本層 Azure Redis Cache。</span><span class="sxs-lookup"><span data-stu-id="9feae-107">Creates a resource group and a basic tier Azure Redis Cache.</span></span> |
| [<span data-ttu-id="9feae-108">使用叢集建立高級快取</span><span class="sxs-lookup"><span data-stu-id="9feae-108">Create a premium cache with clustering</span></span>](./scripts/create-premium-cache-cluster.md) | <span data-ttu-id="9feae-109">透過啟用的叢集建立資源群組與高級層快取。</span><span class="sxs-lookup"><span data-stu-id="9feae-109">Creates a resource group and a premium tier cache with clustering enabled.</span></span>|
| [<span data-ttu-id="9feae-110">取得快取詳細資料</span><span class="sxs-lookup"><span data-stu-id="9feae-110">Get cache details</span></span>](./scripts/show-cache.md) | <span data-ttu-id="9feae-111">取得 Azure Redis Cache 執行個體的詳細資料，包括佈建狀態。</span><span class="sxs-lookup"><span data-stu-id="9feae-111">Gets details of an Azure Redis Cache instance, including provisioning status.</span></span> |
| [<span data-ttu-id="9feae-112">取得主機名稱、連接埠及金鑰</span><span class="sxs-lookup"><span data-stu-id="9feae-112">Get the hostname, ports, and keys</span></span>](./scripts/cache-keys-ports.md) | <span data-ttu-id="9feae-113">取得 Azure Redis Cache 執行個體的主機名稱、連接埠和金鑰。</span><span class="sxs-lookup"><span data-stu-id="9feae-113">Gets the hostname, ports, and keys for an Azure Redis Cache instance.</span></span> |
|<span data-ttu-id="9feae-114">**Web 應用程式加上快取**</span><span class="sxs-lookup"><span data-stu-id="9feae-114">**Web app plus cache**</span></span>||
| [<span data-ttu-id="9feae-115">將 Web 應用程式連線至 redis 快取</span><span class="sxs-lookup"><span data-stu-id="9feae-115">Connect a web app to a redis cache</span></span>](./../app-service-web/scripts/app-service-cli-app-service-redis.md) | <span data-ttu-id="9feae-116">建立 Azure Web 應用程式和 Redis Cache,，然後將 Redis 連線詳細資料新增至應用程式設定。</span><span class="sxs-lookup"><span data-stu-id="9feae-116">Creates an Azure web app and a redis cache, then adds the redis connection details to the app settings.</span></span> |
|<span data-ttu-id="9feae-117">**刪除快取**</span><span class="sxs-lookup"><span data-stu-id="9feae-117">**Delete cache**</span></span>||
| [<span data-ttu-id="9feae-118">刪除快取</span><span class="sxs-lookup"><span data-stu-id="9feae-118">Delete a cache</span></span>](./scripts/delete-cache.md) | <span data-ttu-id="9feae-119">刪除 Azure Redis Cache 執行個體</span><span class="sxs-lookup"><span data-stu-id="9feae-119">Deletes an Azure Redis Cache instance</span></span>  |
| | |

<span data-ttu-id="9feae-120">如需有關 Azure CLI 2.0 的詳細資訊，請參閱[安裝 Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli) (英文) 和[開始使用 Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli) (英文)。</span><span class="sxs-lookup"><span data-stu-id="9feae-120">For more information about Azure CLI 2.0, see [Install Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli) and [Get started with Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli).</span></span>