---
title: "Azure CLI 指令碼範例 - 在來自 Azure Container Registry 的 Docker 容器中建立 ASP.NET Core Web 應用程式 | Microsoft Docs"
description: "Azure CLI 指令碼範例 - 在來自 Azure Container Registry 的 Docker 容器中建立 ASP.NET Core Web 應用程式"
services: appservice
documentationcenter: appservice
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 3a2d1983-ff7b-476a-ac44-49ec2aabb31a
ms.service: app-service
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 06/19/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 2556947d7cdd1475ae82ac2e1d61ad30ebd0d29f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-aspnet-core-web-app-in-a-docker-container-from-azure-container-registry"></a><span data-ttu-id="5691b-103">在來自 Azure Container Registry 的 Docker 容器中建立 ASP.NET Core Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="5691b-103">Create an ASP.NET Core web app in a Docker container from Azure Container Registry</span></span>

<span data-ttu-id="5691b-104">在此案例中，您會學習如何建立資源群組、Linux App Service 方案和 Web 應用程式，並使用來自 Azure Container Registry 的 Docker 容器部署 ASP.NET Core 應用程式。</span><span class="sxs-lookup"><span data-stu-id="5691b-104">In this scenario you will learn how to create a resource group, Linux app service plan, and web app, and deploy an ASP.NET Core application using a Docker Container from the Azure Container Registry.</span></span>


[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="5691b-105">如果您選擇在本機安裝和使用 CLI，本主題會要求您執行 Azure CLI 2.0 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="5691b-105">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="5691b-106">執行 `az --version` 以尋找版本。</span><span class="sxs-lookup"><span data-stu-id="5691b-106">Run `az --version` to find the version.</span></span> <span data-ttu-id="5691b-107">如果您需要安裝或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="5691b-107">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="5691b-108">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="5691b-108">Sample script</span></span>

<span data-ttu-id="5691b-109">[!code-azurecli-interactive[主要](../../../cli_scripts/app-service/deploy-linux-acr/deploy-linux-acr.sh?highlight=6-9 "Linux Azure Container Registry")]</span><span class="sxs-lookup"><span data-stu-id="5691b-109">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/deploy-linux-acr/deploy-linux-acr.sh?highlight=6-9 "Linux Azure Container Registry")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="5691b-110">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="5691b-110">Script explanation</span></span>

<span data-ttu-id="5691b-111">此指令碼使用下列命令來建立資源群組、Web 應用程式和所有相關資源。</span><span class="sxs-lookup"><span data-stu-id="5691b-111">This script uses the following commands to create a resource group, web app, and all related resources.</span></span> <span data-ttu-id="5691b-112">下表中的每個命令都會連結至命令特定的文件。</span><span class="sxs-lookup"><span data-stu-id="5691b-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="5691b-113">命令</span><span class="sxs-lookup"><span data-stu-id="5691b-113">Command</span></span> | <span data-ttu-id="5691b-114">注意事項</span><span class="sxs-lookup"><span data-stu-id="5691b-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="5691b-115">az group create</span><span class="sxs-lookup"><span data-stu-id="5691b-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="5691b-116">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="5691b-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="5691b-117">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="5691b-117">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="5691b-118">建立 App Service 方案。</span><span class="sxs-lookup"><span data-stu-id="5691b-118">Creates an App Service plan.</span></span> <span data-ttu-id="5691b-119">這就像是 Azure Web 應用程式的伺服器陣列。</span><span class="sxs-lookup"><span data-stu-id="5691b-119">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="5691b-120">az webapp create</span><span class="sxs-lookup"><span data-stu-id="5691b-120">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="5691b-121">建立 Azure Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="5691b-121">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="5691b-122">az webapp config container set</span><span class="sxs-lookup"><span data-stu-id="5691b-122">az webapp config container set</span></span>](https://docs.microsoft.com/cli/azure/webapp/config/container#set) | <span data-ttu-id="5691b-123">設定 Azure Web 應用程式的 Docker 容器。</span><span class="sxs-lookup"><span data-stu-id="5691b-123">Sets the Docker container for the Azure web app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="5691b-124">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5691b-124">Next steps</span></span>

<span data-ttu-id="5691b-125">如需 Azure CLI 的詳細資訊，請參閱 [Azure CLI 文件](https://docs.microsoft.com/cli/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="5691b-125">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="5691b-126">您可以在 [Azure App Service 文件](../app-service-cli-samples.md)中找到其他的 App Service CLI 指令碼範例。</span><span class="sxs-lookup"><span data-stu-id="5691b-126">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
