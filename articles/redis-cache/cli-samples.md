---
title: "aaaAzure CLI Redis 快取範例 |Microsoft 文件"
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
ms.openlocfilehash: a2eb6f7267951faca599a43ff29b46beb05fea6d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cli-samples-for-azure-redis-cache"></a><span data-ttu-id="626fd-103">Azure Redis Cache 的 Azure CLI 範例</span><span class="sxs-lookup"><span data-stu-id="626fd-103">Azure CLI Samples for Azure Redis Cache</span></span>

<span data-ttu-id="626fd-104">hello 下表包含使用 Azure CLI hello 建置連結 toobash 指令碼。</span><span class="sxs-lookup"><span data-stu-id="626fd-104">hello following table includes links toobash scripts built using hello Azure CLI.</span></span>

| | |
|---|---|
|<span data-ttu-id="626fd-105">**建立快取**</span><span class="sxs-lookup"><span data-stu-id="626fd-105">**Create cache**</span></span>||
| [<span data-ttu-id="626fd-106">建立快取</span><span class="sxs-lookup"><span data-stu-id="626fd-106">Create a cache</span></span>](./scripts/create-cache.md) | <span data-ttu-id="626fd-107">建立資源群組和基本層 Azure Redis Cache。</span><span class="sxs-lookup"><span data-stu-id="626fd-107">Creates a resource group and a basic tier Azure Redis Cache.</span></span> |
| [<span data-ttu-id="626fd-108">使用叢集建立高級快取</span><span class="sxs-lookup"><span data-stu-id="626fd-108">Create a premium cache with clustering</span></span>](./scripts/create-premium-cache-cluster.md) | <span data-ttu-id="626fd-109">透過啟用的叢集建立資源群組與高級層快取。</span><span class="sxs-lookup"><span data-stu-id="626fd-109">Creates a resource group and a premium tier cache with clustering enabled.</span></span>|
| [<span data-ttu-id="626fd-110">取得快取詳細資料</span><span class="sxs-lookup"><span data-stu-id="626fd-110">Get cache details</span></span>](./scripts/show-cache.md) | <span data-ttu-id="626fd-111">取得 Azure Redis Cache 執行個體的詳細資料，包括佈建狀態。</span><span class="sxs-lookup"><span data-stu-id="626fd-111">Gets details of an Azure Redis Cache instance, including provisioning status.</span></span> |
| [<span data-ttu-id="626fd-112">取得 hello 主機名稱、 連接埠，以及索引鍵</span><span class="sxs-lookup"><span data-stu-id="626fd-112">Get hello hostname, ports, and keys</span></span>](./scripts/cache-keys-ports.md) | <span data-ttu-id="626fd-113">取得 hello 主機名稱、 通訊埠，以及 Azure Redis 快取執行個體金鑰。</span><span class="sxs-lookup"><span data-stu-id="626fd-113">Gets hello hostname, ports, and keys for an Azure Redis Cache instance.</span></span> |
|<span data-ttu-id="626fd-114">**Web 應用程式加上快取**</span><span class="sxs-lookup"><span data-stu-id="626fd-114">**Web app plus cache**</span></span>||
| [<span data-ttu-id="626fd-115">連接 web 應用程式 tooa redis 快取</span><span class="sxs-lookup"><span data-stu-id="626fd-115">Connect a web app tooa redis cache</span></span>](./../app-service-web/scripts/app-service-cli-app-service-redis.md) | <span data-ttu-id="626fd-116">建立 Azure web 應用程式和 redis 快取，然後加入 hello redis 連線詳細資料 toohello 應用程式的設定。</span><span class="sxs-lookup"><span data-stu-id="626fd-116">Creates an Azure web app and a redis cache, then adds hello redis connection details toohello app settings.</span></span> |
|<span data-ttu-id="626fd-117">**刪除快取**</span><span class="sxs-lookup"><span data-stu-id="626fd-117">**Delete cache**</span></span>||
| [<span data-ttu-id="626fd-118">刪除快取</span><span class="sxs-lookup"><span data-stu-id="626fd-118">Delete a cache</span></span>](./scripts/delete-cache.md) | <span data-ttu-id="626fd-119">刪除 Azure Redis Cache 執行個體</span><span class="sxs-lookup"><span data-stu-id="626fd-119">Deletes an Azure Redis Cache instance</span></span>  |
| | |

<span data-ttu-id="626fd-120">如需有關 Azure CLI 2.0 的詳細資訊，請參閱[安裝 Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli) (英文) 和[開始使用 Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli) (英文)。</span><span class="sxs-lookup"><span data-stu-id="626fd-120">For more information about Azure CLI 2.0, see [Install Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli) and [Get started with Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli).</span></span>