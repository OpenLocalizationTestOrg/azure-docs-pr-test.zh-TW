---
title: "Azure CLI 指令碼範例 - 建立可從 GitHub 部署的 Web 應用程式 | Microsoft Docs"
description: "Azure CLI 指令碼範例 - 建立可從 GitHub 部署的 Web 應用程式"
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 0205c991-0989-4ca3-bb41-237dcc964460
ms.service: app-service-web
ms.workload: web
ms.devlang: azurecli
ms.tgt_pltfrm: sample
ms.topic: sample
ms.date: 06/19/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 61e9d65319cecf3ea4e9152ebdf1035566aad74c
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-web-app-with-deployment-from-github"></a><span data-ttu-id="67233-103">建立可從 GitHub 部署的 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="67233-103">Create a web app with deployment from GitHub</span></span>

<span data-ttu-id="67233-104">此範例指令碼會在 App Service 中建立 Web 應用程式及其相關資源，然後從公用 GitHub 存放庫部署 Web 應用程式程式碼 (不使用連續部署)。</span><span class="sxs-lookup"><span data-stu-id="67233-104">This sample script creates a web app in App Service with its related resources, and then deploys your web app code from a public GitHub repository (without continuous deployment).</span></span> <span data-ttu-id="67233-105">如需進行使用連續部署的 GitHub 部署，請參閱[建立可從 GitHub 連續部署的 Web 應用程式](app-service-cli-continuous-deployment-github.md)。</span><span class="sxs-lookup"><span data-stu-id="67233-105">For GitHub deployment with continuous deployment, see [Create a web app with continuous deployment from GitHub](app-service-cli-continuous-deployment-github.md).</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="67233-106">如果您選擇在本機安裝和使用 CLI，本主題會要求您執行 Azure CLI 2.0 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="67233-106">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="67233-107">執行 `az --version` 以尋找版本。</span><span class="sxs-lookup"><span data-stu-id="67233-107">Run `az --version` to find the version.</span></span> <span data-ttu-id="67233-108">如果您需要安裝或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="67233-108">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="67233-109">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="67233-109">Sample script</span></span>

<span data-ttu-id="67233-110">[!code-azurecli-interactive[主要](../../../cli_scripts/app-service/deploy-github/deploy-github.sh?highlight=3 "建立可從 GitHub 部署的 Web 應用程式")]</span><span class="sxs-lookup"><span data-stu-id="67233-110">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/deploy-github/deploy-github.sh?highlight=3 "Create a web app with deployment from GitHub")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="67233-111">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="67233-111">Script explanation</span></span> 

<span data-ttu-id="67233-112">此指令碼會使用下列命令。</span><span class="sxs-lookup"><span data-stu-id="67233-112">This script uses the following commands.</span></span> <span data-ttu-id="67233-113">下表中的每個命令都會連結至命令特定的文件。</span><span class="sxs-lookup"><span data-stu-id="67233-113">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="67233-114">命令</span><span class="sxs-lookup"><span data-stu-id="67233-114">Command</span></span> | <span data-ttu-id="67233-115">注意事項</span><span class="sxs-lookup"><span data-stu-id="67233-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="67233-116">az group create</span><span class="sxs-lookup"><span data-stu-id="67233-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="67233-117">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="67233-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="67233-118">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="67233-118">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="67233-119">建立 App Service 方案。</span><span class="sxs-lookup"><span data-stu-id="67233-119">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="67233-120">az webapp create</span><span class="sxs-lookup"><span data-stu-id="67233-120">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="67233-121">建立 Azure Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="67233-121">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="67233-122">az webapp deployment source config</span><span class="sxs-lookup"><span data-stu-id="67233-122">az webapp deployment source config</span></span>](https://docs.microsoft.com/cli/azure/webapp/deployment/source#config) | <span data-ttu-id="67233-123">將 Azure Web 應用程式關聯到 Git 或 Mercurial 存放庫。</span><span class="sxs-lookup"><span data-stu-id="67233-123">Associates an Azure web app with a Git or Mercurial repository.</span></span> |
| [<span data-ttu-id="67233-124">az webapp browse</span><span class="sxs-lookup"><span data-stu-id="67233-124">az webapp browse</span></span>](https://docs.microsoft.com/cli/azure/webapp#browse) | <span data-ttu-id="67233-125">在瀏覽器中開啟 Azure Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="67233-125">Open an Azure web app in a browser.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="67233-126">後續步驟</span><span class="sxs-lookup"><span data-stu-id="67233-126">Next steps</span></span>

<span data-ttu-id="67233-127">如需 Azure CLI 的詳細資訊，請參閱 [Azure CLI 文件](https://docs.microsoft.com/cli/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="67233-127">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="67233-128">您可以在 [Azure App Service 文件](../app-service-cli-samples.md)中找到其他的 App Service CLI 指令碼範例。</span><span class="sxs-lookup"><span data-stu-id="67233-128">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
