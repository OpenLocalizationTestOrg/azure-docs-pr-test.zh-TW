---
title: "Azure CLI 指令碼範例 - 建立 Web 應用程式並從本機 Git 存放庫部署程式碼 | Microsoft Docs"
description: "Azure CLI 指令碼範例 - 建立 Web 應用程式並從本機 Git 存放庫部署程式碼"
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 048f98aa-f708-44cb-9b9e-953f67dc6da8
ms.service: app-service-web
ms.workload: web
ms.devlang: azurecli
ms.tgt_pltfrm: na
ms.topic: sample
ms.date: 06/19/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 50d69ac48438920ce59808ee79809235d8330b14
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-web-app-and-deploy-code-from-a-local-git-repository"></a><span data-ttu-id="ecfb5-103">建立 Web 應用程式並從本機 Git 存放庫部署程式碼</span><span class="sxs-lookup"><span data-stu-id="ecfb5-103">Create a web app and deploy code from a local Git repository</span></span>

<span data-ttu-id="ecfb5-104">此範例指令碼會在 App Service 中建立 Web 應用程式及其相關資源，然後在本機 Git 存放庫中部署 Web 應用程式程式碼。</span><span class="sxs-lookup"><span data-stu-id="ecfb5-104">This sample script creates a web app in App Service with its related resources, and then deploys your web app code in a local Git repository.</span></span>


[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="ecfb5-105">如果您選擇在本機安裝和使用 CLI，本主題會要求您執行 Azure CLI 2.0 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="ecfb5-105">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="ecfb5-106">執行 `az --version` 以尋找版本。</span><span class="sxs-lookup"><span data-stu-id="ecfb5-106">Run `az --version` to find the version.</span></span> <span data-ttu-id="ecfb5-107">如果您需要安裝或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="ecfb5-107">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="ecfb5-108">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="ecfb5-108">Sample script</span></span>

<span data-ttu-id="ecfb5-109">[!code-azurecli-interactive[主要](../../../cli_scripts/app-service/deploy-local-git/deploy-local-git.sh?highlight=3-5 "建立 Web 應用程式並從本機 Git 存放庫部署程式碼")]</span><span class="sxs-lookup"><span data-stu-id="ecfb5-109">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/deploy-local-git/deploy-local-git.sh?highlight=3-5 "Create a web app and deploy code from a local Git repository")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="ecfb5-110">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="ecfb5-110">Script explanation</span></span>

<span data-ttu-id="ecfb5-111">此指令碼會使用下列命令。</span><span class="sxs-lookup"><span data-stu-id="ecfb5-111">This script uses the following commands.</span></span> <span data-ttu-id="ecfb5-112">下表中的每個命令都會連結至命令特定的文件。</span><span class="sxs-lookup"><span data-stu-id="ecfb5-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="ecfb5-113">命令</span><span class="sxs-lookup"><span data-stu-id="ecfb5-113">Command</span></span> | <span data-ttu-id="ecfb5-114">注意事項</span><span class="sxs-lookup"><span data-stu-id="ecfb5-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="ecfb5-115">az group create</span><span class="sxs-lookup"><span data-stu-id="ecfb5-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="ecfb5-116">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="ecfb5-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="ecfb5-117">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="ecfb5-117">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="ecfb5-118">建立 App Service 方案。</span><span class="sxs-lookup"><span data-stu-id="ecfb5-118">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="ecfb5-119">az webapp create</span><span class="sxs-lookup"><span data-stu-id="ecfb5-119">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="ecfb5-120">建立 Azure Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="ecfb5-120">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="ecfb5-121">az webapp deployment user set</span><span class="sxs-lookup"><span data-stu-id="ecfb5-121">az webapp deployment user set</span></span>](https://review.docs.microsoft.com/cli/azure/webapp/deployment/user#set) | <span data-ttu-id="ecfb5-122">設定 App Service 的帳戶層級部署認證。</span><span class="sxs-lookup"><span data-stu-id="ecfb5-122">Sets the account-level deployment credentials for App Service.</span></span> |
| [<span data-ttu-id="ecfb5-123">az webapp deployment source config-local-git</span><span class="sxs-lookup"><span data-stu-id="ecfb5-123">az webapp deployment source config-local-git</span></span>](https://review.docs.microsoft.com/cli/azure/webapp/deployment/source#config-local-git) | <span data-ttu-id="ecfb5-124">建立本機 Git 存放庫的原始檔控制組態。</span><span class="sxs-lookup"><span data-stu-id="ecfb5-124">Creates a source control configuration for a local Git repository.</span></span> |
| [<span data-ttu-id="ecfb5-125">az webapp browse</span><span class="sxs-lookup"><span data-stu-id="ecfb5-125">az webapp browse</span></span>](https://docs.microsoft.com/cli/azure/webapp#browse) | <span data-ttu-id="ecfb5-126">在瀏覽器中開啟 Azure Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="ecfb5-126">Open an Azure web app in a browser.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="ecfb5-127">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ecfb5-127">Next steps</span></span>

<span data-ttu-id="ecfb5-128">如需 Azure CLI 的詳細資訊，請參閱 [Azure CLI 文件](https://docs.microsoft.com/cli/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="ecfb5-128">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="ecfb5-129">您可以在 [Azure App Service 文件](../app-service-cli-samples.md)中找到其他的 App Service CLI 指令碼範例。</span><span class="sxs-lookup"><span data-stu-id="ecfb5-129">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
