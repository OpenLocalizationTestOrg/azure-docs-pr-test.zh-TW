---
title: "CLI 指令碼範例-aaaAzure 連接 web 應用程式 tooa redis 快取 |Microsoft 文件"
description: "Azure CLI 指令碼範例-連接 web 應用程式 tooa redis 快取"
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
ms.openlocfilehash: b911e6643591b8f07aeb64d4d62876c0fa156a8a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="connect-a-web-app-tooa-redis-cache"></a><span data-ttu-id="0889c-103">連接 web 應用程式 tooa redis 快取</span><span class="sxs-lookup"><span data-stu-id="0889c-103">Connect a web app tooa redis cache</span></span>

<span data-ttu-id="0889c-104">在此案例中，您將學習如何 toocreate Azure redis 快取和 Azure web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="0889c-104">In this scenario you will learn how toocreate an Azure redis cache and an Azure web app.</span></span> <span data-ttu-id="0889c-105">然後，您將連結 hello redis 快取 toohello web 應用程式使用應用程式設定。</span><span class="sxs-lookup"><span data-stu-id="0889c-105">Then you will link hello redis cache toohello web app using app settings.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="0889c-106">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="0889c-106">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/connect-to-redis/connect-to-redis.sh "Azure Redis Cache")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="0889c-107">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="0889c-107">Script explanation</span></span>

<span data-ttu-id="0889c-108">此指令碼會使用下列命令 toocreate 資源群組、 web 應用程式，redis 快取和所有相關的資源的 hello。</span><span class="sxs-lookup"><span data-stu-id="0889c-108">This script uses hello following commands toocreate a resource group, web app, redis cache and all related resources.</span></span> <span data-ttu-id="0889c-109">Hello 資料表連結 toocommand 特定文件中的每個命令。</span><span class="sxs-lookup"><span data-stu-id="0889c-109">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="0889c-110">命令</span><span class="sxs-lookup"><span data-stu-id="0889c-110">Command</span></span> | <span data-ttu-id="0889c-111">注意事項</span><span class="sxs-lookup"><span data-stu-id="0889c-111">Notes</span></span> |
|---|---|
| [<span data-ttu-id="0889c-112">az group create</span><span class="sxs-lookup"><span data-stu-id="0889c-112">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="0889c-113">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="0889c-113">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="0889c-114">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="0889c-114">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="0889c-115">建立 App Service 方案。</span><span class="sxs-lookup"><span data-stu-id="0889c-115">Creates an App Service plan.</span></span> <span data-ttu-id="0889c-116">這就像是 Azure Web 應用程式的伺服器陣列。</span><span class="sxs-lookup"><span data-stu-id="0889c-116">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="0889c-117">az webapp create</span><span class="sxs-lookup"><span data-stu-id="0889c-117">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="0889c-118">建立 Azure Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="0889c-118">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="0889c-119">az redis create</span><span class="sxs-lookup"><span data-stu-id="0889c-119">az redis create</span></span>](https://docs.microsoft.com/en-us/cli/azure/redis#create) | <span data-ttu-id="0889c-120">建立新的 Redis 快取執行個體。</span><span class="sxs-lookup"><span data-stu-id="0889c-120">Create new Redis Cache instance.</span></span> <span data-ttu-id="0889c-121">這是 hello 資料儲存的位置。</span><span class="sxs-lookup"><span data-stu-id="0889c-121">This is where hello data will be stored.</span></span> |
| [<span data-ttu-id="0889c-122">az redis list-keys</span><span class="sxs-lookup"><span data-stu-id="0889c-122">az redis list-keys</span></span>](https://docs.microsoft.com/en-us/cli/azure/redis#list-keys) | <span data-ttu-id="0889c-123">列出 hello hello redis 快取執行個體的存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="0889c-123">Lists hello access keys for hello redis cache instance.</span></span> |
| [<span data-ttu-id="0889c-124">az webapp config appsettings set</span><span class="sxs-lookup"><span data-stu-id="0889c-124">az webapp config appsettings set</span></span>](https://docs.microsoft.com/cli/azure/webapp/config/appsettings#set) | <span data-ttu-id="0889c-125">建立或更新 Azure Web 應用程式的應用程式設定。</span><span class="sxs-lookup"><span data-stu-id="0889c-125">Creates or updates an app setting for an Azure web app.</span></span> <span data-ttu-id="0889c-126">應用程式設定會顯示為應用程式的環境變數。</span><span class="sxs-lookup"><span data-stu-id="0889c-126">App settings are exposed as environment variables for your app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="0889c-127">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0889c-127">Next steps</span></span>

<span data-ttu-id="0889c-128">如需有關 Azure CLI hello 的詳細資訊，請參閱[Azure CLI 文件](https://docs.microsoft.com/cli/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="0889c-128">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="0889c-129">其他應用程式服務 CLI 指令碼範例可以在 hello [Azure 應用程式服務文件](../app-service-cli-samples.md)。</span><span class="sxs-lookup"><span data-stu-id="0889c-129">Additional App Service CLI script samples can be found in hello [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
