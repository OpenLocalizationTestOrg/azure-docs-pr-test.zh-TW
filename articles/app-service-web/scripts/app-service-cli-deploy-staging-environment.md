---
title: "Azure CLI 指令碼範例 - 建立 Web 應用程式並將程式碼部署至預備環境 | Microsoft Docs"
description: "Azure CLI 指令碼範例 - 建立 Web 應用程式並將程式碼部署至預備環境"
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 2b995dcd-e471-4355-9fda-00babcdb156e
ms.service: app-service-web
ms.workload: web
ms.devlang: azurecli
ms.tgt_pltfrm: na
ms.topic: sample
ms.date: 06/19/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: d586b50258c32e44f55859aad0a89475e9e4d2eb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-web-app-and-deploy-code-to-a-staging-environment"></a><span data-ttu-id="a6ca0-103">建立 Web 應用程式並將程式碼部署至預備環境</span><span class="sxs-lookup"><span data-stu-id="a6ca0-103">Create a web app and deploy code to a staging environment</span></span>

<span data-ttu-id="a6ca0-104">此範例指令碼會在 App Service 中建立 Web 應用程式以及稱為「預備」的其他部署位置，然後將範例應用程式部署至「預備」位置。</span><span class="sxs-lookup"><span data-stu-id="a6ca0-104">This sample script creates a web app in App Service with an additional deployment slot called "staging", and then deploys a sample app to the "staging" slot.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="a6ca0-105">如果您選擇在本機安裝和使用 CLI，本主題會要求您執行 Azure CLI 2.0 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="a6ca0-105">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="a6ca0-106">執行 `az --version` 以尋找版本。</span><span class="sxs-lookup"><span data-stu-id="a6ca0-106">Run `az --version` to find the version.</span></span> <span data-ttu-id="a6ca0-107">如果您需要安裝或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="a6ca0-107">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="a6ca0-108">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="a6ca0-108">Sample script</span></span>

<span data-ttu-id="a6ca0-109">[!code-azurecli-interactive[主要](../../../cli_scripts/app-service/deploy-deployment-slot/deploy-deployment-slot.sh "建立 Web 應用程式並將程式碼部署至預備環境")]</span><span class="sxs-lookup"><span data-stu-id="a6ca0-109">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/deploy-deployment-slot/deploy-deployment-slot.sh "Create a web app and deploy code to a staging environment")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="a6ca0-110">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="a6ca0-110">Script explanation</span></span>

<span data-ttu-id="a6ca0-111">此指令碼會使用下列命令。</span><span class="sxs-lookup"><span data-stu-id="a6ca0-111">This script uses the following commands.</span></span> <span data-ttu-id="a6ca0-112">下表中的每個命令都會連結至命令特定的文件。</span><span class="sxs-lookup"><span data-stu-id="a6ca0-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="a6ca0-113">命令</span><span class="sxs-lookup"><span data-stu-id="a6ca0-113">Command</span></span> | <span data-ttu-id="a6ca0-114">注意事項</span><span class="sxs-lookup"><span data-stu-id="a6ca0-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="a6ca0-115">az group create</span><span class="sxs-lookup"><span data-stu-id="a6ca0-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="a6ca0-116">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="a6ca0-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="a6ca0-117">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="a6ca0-117">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="a6ca0-118">建立 App Service 方案。</span><span class="sxs-lookup"><span data-stu-id="a6ca0-118">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="a6ca0-119">az webapp create</span><span class="sxs-lookup"><span data-stu-id="a6ca0-119">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="a6ca0-120">建立 Azure Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="a6ca0-120">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="a6ca0-121">az webapp deployment slot create</span><span class="sxs-lookup"><span data-stu-id="a6ca0-121">az webapp deployment slot create</span></span>](https://docs.microsoft.com/cli/azure/webapp/deployment/slot#create) | <span data-ttu-id="a6ca0-122">建立部署位置。</span><span class="sxs-lookup"><span data-stu-id="a6ca0-122">Create a deployment slot.</span></span> |
| [<span data-ttu-id="a6ca0-123">az webapp deployment source config</span><span class="sxs-lookup"><span data-stu-id="a6ca0-123">az webapp deployment source config</span></span>](https://docs.microsoft.com/cli/azure/webapp/deployment/source#config) | <span data-ttu-id="a6ca0-124">將 Azure Web 應用程式關聯到 Git 或 Mercurial 存放庫。</span><span class="sxs-lookup"><span data-stu-id="a6ca0-124">Associates an Azure web app with a Git or Mercurial repository.</span></span> |
| [<span data-ttu-id="a6ca0-125">az webapp browse</span><span class="sxs-lookup"><span data-stu-id="a6ca0-125">az webapp browse</span></span>](https://docs.microsoft.com/cli/azure/webapp#browse) | <span data-ttu-id="a6ca0-126">在瀏覽器中開啟 Azure Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="a6ca0-126">Open an Azure web app in a browser.</span></span> |
| [<span data-ttu-id="a6ca0-127">az webapp deployment slot swap</span><span class="sxs-lookup"><span data-stu-id="a6ca0-127">az webapp deployment slot swap</span></span>](https://docs.microsoft.com/cli/azure/webapp/deployment/slot#swap) | <span data-ttu-id="a6ca0-128">將指定的部署位置切換到生產環境。</span><span class="sxs-lookup"><span data-stu-id="a6ca0-128">Swap a specified deployment slot into production.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="a6ca0-129">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a6ca0-129">Next steps</span></span>

<span data-ttu-id="a6ca0-130">如需 Azure CLI 的詳細資訊，請參閱 [Azure CLI 文件](https://docs.microsoft.com/cli/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="a6ca0-130">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="a6ca0-131">您可以在 [Azure App Service 文件](../app-service-cli-samples.md)中找到其他的 App Service CLI 指令碼範例。</span><span class="sxs-lookup"><span data-stu-id="a6ca0-131">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
