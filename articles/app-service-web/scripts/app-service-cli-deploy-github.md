---
title: "aaaAzure CLI 指令碼範例-使用來自 GitHub 部署建立 web 應用程式 |Microsoft 文件"
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
ms.openlocfilehash: eb7231aa5c6a7e23d76885107e733008382f7487
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-web-app-with-deployment-from-github"></a><span data-ttu-id="01a35-103">建立可從 GitHub 部署的 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="01a35-103">Create a web app with deployment from GitHub</span></span>

<span data-ttu-id="01a35-104">此範例指令碼會在 App Service 中建立 Web 應用程式及其相關資源，然後從公用 GitHub 存放庫部署 Web 應用程式程式碼 (不使用連續部署)。</span><span class="sxs-lookup"><span data-stu-id="01a35-104">This sample script creates a web app in App Service with its related resources, and then deploys your web app code from a public GitHub repository (without continuous deployment).</span></span> <span data-ttu-id="01a35-105">如需進行使用連續部署的 GitHub 部署，請參閱[建立可從 GitHub 連續部署的 Web 應用程式](app-service-cli-continuous-deployment-github.md)。</span><span class="sxs-lookup"><span data-stu-id="01a35-105">For GitHub deployment with continuous deployment, see [Create a web app with continuous deployment from GitHub](app-service-cli-continuous-deployment-github.md).</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="01a35-106">如果您選擇 tooinstall，並在本機上使用 hello CLI，本主題會需要您執行 hello Azure CLI 版本 2.0 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="01a35-106">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="01a35-107">執行`az --version`toofind hello 版本。</span><span class="sxs-lookup"><span data-stu-id="01a35-107">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="01a35-108">如果您需要 tooinstall 或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="01a35-108">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="01a35-109">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="01a35-109">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/deploy-github/deploy-github.sh?highlight=3 "Create a web app with deployment from GitHub")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="01a35-110">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="01a35-110">Script explanation</span></span> 

<span data-ttu-id="01a35-111">此指令碼會使用下列命令的 hello。</span><span class="sxs-lookup"><span data-stu-id="01a35-111">This script uses hello following commands.</span></span> <span data-ttu-id="01a35-112">Hello 資料表連結 toocommand 特定文件中的每個命令。</span><span class="sxs-lookup"><span data-stu-id="01a35-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="01a35-113">命令</span><span class="sxs-lookup"><span data-stu-id="01a35-113">Command</span></span> | <span data-ttu-id="01a35-114">注意事項</span><span class="sxs-lookup"><span data-stu-id="01a35-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="01a35-115">az group create</span><span class="sxs-lookup"><span data-stu-id="01a35-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="01a35-116">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="01a35-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="01a35-117">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="01a35-117">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="01a35-118">建立 App Service 方案。</span><span class="sxs-lookup"><span data-stu-id="01a35-118">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="01a35-119">az webapp create</span><span class="sxs-lookup"><span data-stu-id="01a35-119">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="01a35-120">建立 Azure Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="01a35-120">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="01a35-121">az webapp deployment source config</span><span class="sxs-lookup"><span data-stu-id="01a35-121">az webapp deployment source config</span></span>](https://docs.microsoft.com/cli/azure/webapp/deployment/source#config) | <span data-ttu-id="01a35-122">將 Azure Web 應用程式關聯到 Git 或 Mercurial 存放庫。</span><span class="sxs-lookup"><span data-stu-id="01a35-122">Associates an Azure web app with a Git or Mercurial repository.</span></span> |
| [<span data-ttu-id="01a35-123">az webapp browse</span><span class="sxs-lookup"><span data-stu-id="01a35-123">az webapp browse</span></span>](https://docs.microsoft.com/cli/azure/webapp#browse) | <span data-ttu-id="01a35-124">在瀏覽器中開啟 Azure Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="01a35-124">Open an Azure web app in a browser.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="01a35-125">後續步驟</span><span class="sxs-lookup"><span data-stu-id="01a35-125">Next steps</span></span>

<span data-ttu-id="01a35-126">如需有關 Azure CLI hello 的詳細資訊，請參閱[Azure CLI 文件](https://docs.microsoft.com/cli/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="01a35-126">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="01a35-127">其他應用程式服務 CLI 指令碼範例可以在 hello [Azure 應用程式服務文件](../app-service-cli-samples.md)。</span><span class="sxs-lookup"><span data-stu-id="01a35-127">Additional App Service CLI script samples can be found in hello [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
