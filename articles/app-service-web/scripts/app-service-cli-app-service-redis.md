---
title: "Azure CLI 指令碼範例 - 將 Web 應用程式連線至 redis 快取 | Microsoft Docs"
description: "Azure CLI 指令碼範例 - 將 Web 應用程式連線至 redis 快取"
services: appservice
documentationcenter: appservice
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: bc8345b2-8487-40c6-a91f-77414e8688e6
ms.service: app-service
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 06/19/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: b697c8508a6c3422b6b0d0ca36843a9c884b505f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="connect-a-web-app-to-a-redis-cache"></a><span data-ttu-id="5c99c-103">將 Web 應用程式連線至 redis 快取</span><span class="sxs-lookup"><span data-stu-id="5c99c-103">Connect a web app to a redis cache</span></span>

<span data-ttu-id="5c99c-104">在此案例中，您會了解如何建立 Azure redis 快取和 Azure Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="5c99c-104">In this scenario you will learn how to create an Azure redis cache and an Azure web app.</span></span> <span data-ttu-id="5c99c-105">然後，您會使用應用程式設定將 redis 快取連結至 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="5c99c-105">Then you will link the redis cache to the web app using app settings.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="5c99c-106">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="5c99c-106">Sample script</span></span>

<span data-ttu-id="5c99c-107">[!code-azurecli-interactive[主要](../../../cli_scripts/app-service/connect-to-redis/connect-to-redis.sh "Azure Redis 快取")]</span><span class="sxs-lookup"><span data-stu-id="5c99c-107">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/connect-to-redis/connect-to-redis.sh "Azure Redis Cache")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="5c99c-108">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="5c99c-108">Script explanation</span></span>

<span data-ttu-id="5c99c-109">此指令碼使用下列命令來建立資源群組、Web 應用程式、redis 快取和所有相關資源。</span><span class="sxs-lookup"><span data-stu-id="5c99c-109">This script uses the following commands to create a resource group, web app, redis cache and all related resources.</span></span> <span data-ttu-id="5c99c-110">下表中的每個命令都會連結至命令特定的文件。</span><span class="sxs-lookup"><span data-stu-id="5c99c-110">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="5c99c-111">命令</span><span class="sxs-lookup"><span data-stu-id="5c99c-111">Command</span></span> | <span data-ttu-id="5c99c-112">注意事項</span><span class="sxs-lookup"><span data-stu-id="5c99c-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="5c99c-113">az group create</span><span class="sxs-lookup"><span data-stu-id="5c99c-113">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="5c99c-114">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="5c99c-114">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="5c99c-115">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="5c99c-115">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="5c99c-116">建立 App Service 方案。</span><span class="sxs-lookup"><span data-stu-id="5c99c-116">Creates an App Service plan.</span></span> <span data-ttu-id="5c99c-117">這就像是 Azure Web 應用程式的伺服器陣列。</span><span class="sxs-lookup"><span data-stu-id="5c99c-117">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="5c99c-118">az webapp create</span><span class="sxs-lookup"><span data-stu-id="5c99c-118">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="5c99c-119">建立 Azure Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="5c99c-119">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="5c99c-120">az redis create</span><span class="sxs-lookup"><span data-stu-id="5c99c-120">az redis create</span></span>](https://docs.microsoft.com/en-us/cli/azure/redis#create) | <span data-ttu-id="5c99c-121">建立新的 Redis 快取執行個體。</span><span class="sxs-lookup"><span data-stu-id="5c99c-121">Create new Redis Cache instance.</span></span> <span data-ttu-id="5c99c-122">這是儲存資料的位置。</span><span class="sxs-lookup"><span data-stu-id="5c99c-122">This is where the data will be stored.</span></span> |
| [<span data-ttu-id="5c99c-123">az redis list-keys</span><span class="sxs-lookup"><span data-stu-id="5c99c-123">az redis list-keys</span></span>](https://docs.microsoft.com/en-us/cli/azure/redis#list-keys) | <span data-ttu-id="5c99c-124">列出 redis 快取執行個體的存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="5c99c-124">Lists the access keys for the redis cache instance.</span></span> |
| [<span data-ttu-id="5c99c-125">az webapp config appsettings set</span><span class="sxs-lookup"><span data-stu-id="5c99c-125">az webapp config appsettings set</span></span>](https://docs.microsoft.com/cli/azure/webapp/config/appsettings#set) | <span data-ttu-id="5c99c-126">建立或更新 Azure Web 應用程式的應用程式設定。</span><span class="sxs-lookup"><span data-stu-id="5c99c-126">Creates or updates an app setting for an Azure web app.</span></span> <span data-ttu-id="5c99c-127">應用程式設定會顯示為應用程式的環境變數。</span><span class="sxs-lookup"><span data-stu-id="5c99c-127">App settings are exposed as environment variables for your app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="5c99c-128">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5c99c-128">Next steps</span></span>

<span data-ttu-id="5c99c-129">如需 Azure CLI 的詳細資訊，請參閱 [Azure CLI 文件](https://docs.microsoft.com/cli/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="5c99c-129">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="5c99c-130">您可以在 [Azure App Service 文件](../app-service-cli-samples.md)中找到其他的 App Service CLI 指令碼範例。</span><span class="sxs-lookup"><span data-stu-id="5c99c-130">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
