---
title: "Azure CLI 指令碼範例 - 建立可從 Visual Studio Team Services 連續部署的 Web 應用程式 | Microsoft Docs"
description: "Azure CLI 指令碼範例 - 建立可從 Visual Studio Team Services 連續部署的 Web 應用程式"
services: app-service\web
documentationcenter: 
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 389d3bd3-cd8e-4715-a3a1-031ec061d385
ms.service: app-service-web
ms.workload: web
ms.devlang: azurecli
ms.tgt_pltfrm: na
ms.topic: sample
ms.date: 06/19/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 2b983616757ca3c4226c12876f5fd4c285067318
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-web-app-with-continuous-deployment-from-visual-studio-team-services"></a><span data-ttu-id="903cc-103">建立可從 Visual Studio Team Services 連續部署的 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="903cc-103">Create a web app with continuous deployment from Visual Studio Team Services</span></span>

<span data-ttu-id="903cc-104">此範例指令碼會在 App Service 中建立 Web 應用程式及其相關資源，然後設定從 Visual Studio Team Services 存放庫進行的連續部署。</span><span class="sxs-lookup"><span data-stu-id="903cc-104">This sample script creates a web app in App Service with its related resources, and then sets up continuous deployment from a Visual Studio Team Services repository.</span></span> <span data-ttu-id="903cc-105">針對此範例，您將需要：</span><span class="sxs-lookup"><span data-stu-id="903cc-105">For this sample, you will need:</span></span>

* <span data-ttu-id="903cc-106">具有應用程式程式碼的 Visual Studio Team Services 存放庫 (您必須有此存放庫的系統管理權限)。</span><span class="sxs-lookup"><span data-stu-id="903cc-106">A Visual Studio Team Services repository with application code, that you have administrative permissions for.</span></span>
* <span data-ttu-id="903cc-107">您 Visual Studio Team Services 帳戶的[個人存取權杖 (PAT)](https://www.visualstudio.com/docs/setup-admin/team-services/use-personal-access-tokens-to-authenticate)。</span><span class="sxs-lookup"><span data-stu-id="903cc-107">A [Personal Access Token (PAT)](https://www.visualstudio.com/docs/setup-admin/team-services/use-personal-access-tokens-to-authenticate) for your Visual Studio Team Services account.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="903cc-108">如果您選擇在本機安裝和使用 CLI，本主題會要求您執行 Azure CLI 2.0 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="903cc-108">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="903cc-109">執行 `az --version` 以尋找版本。</span><span class="sxs-lookup"><span data-stu-id="903cc-109">Run `az --version` to find the version.</span></span> <span data-ttu-id="903cc-110">如果您需要安裝或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="903cc-110">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="903cc-111">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="903cc-111">Sample script</span></span>

<span data-ttu-id="903cc-112">[!code-azurecli-interactive[主要](../../../cli_scripts/app-service/deploy-vsts-continuous/deploy-vsts-continuous.sh?highlight=3-4 "建立可從 Visual Studio Team Services 連續部署的 Web 應用程式")]</span><span class="sxs-lookup"><span data-stu-id="903cc-112">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/deploy-vsts-continuous/deploy-vsts-continuous.sh?highlight=3-4 "Create a web app with continuous deployment from Visual Studio Team Services")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="903cc-113">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="903cc-113">Script explanation</span></span>

<span data-ttu-id="903cc-114">此指令碼會使用下列命令。</span><span class="sxs-lookup"><span data-stu-id="903cc-114">This script uses the following commands.</span></span> <span data-ttu-id="903cc-115">下表中的每個命令都會連結至命令特定的文件。</span><span class="sxs-lookup"><span data-stu-id="903cc-115">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="903cc-116">命令</span><span class="sxs-lookup"><span data-stu-id="903cc-116">Command</span></span> | <span data-ttu-id="903cc-117">注意事項</span><span class="sxs-lookup"><span data-stu-id="903cc-117">Notes</span></span> |
|---|---|
| [<span data-ttu-id="903cc-118">az group create</span><span class="sxs-lookup"><span data-stu-id="903cc-118">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="903cc-119">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="903cc-119">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="903cc-120">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="903cc-120">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="903cc-121">建立 App Service 方案。</span><span class="sxs-lookup"><span data-stu-id="903cc-121">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="903cc-122">az webapp create</span><span class="sxs-lookup"><span data-stu-id="903cc-122">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="903cc-123">建立 Azure Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="903cc-123">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="903cc-124">az webapp deployment source config</span><span class="sxs-lookup"><span data-stu-id="903cc-124">az webapp deployment source config</span></span>](https://docs.microsoft.com/cli/azure/webapp/deployment/source#config) | <span data-ttu-id="903cc-125">將 Azure Web 應用程式關聯到 Git 或 Mercurial 存放庫。</span><span class="sxs-lookup"><span data-stu-id="903cc-125">Associates an Azure web app with a Git or Mercurial repository.</span></span> |
| [<span data-ttu-id="903cc-126">az webapp browse</span><span class="sxs-lookup"><span data-stu-id="903cc-126">az webapp browse</span></span>](https://docs.microsoft.com/cli/azure/webapp#browse) | <span data-ttu-id="903cc-127">在瀏覽器中開啟 Azure Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="903cc-127">Open an Azure web app in a browser.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="903cc-128">後續步驟</span><span class="sxs-lookup"><span data-stu-id="903cc-128">Next steps</span></span>

<span data-ttu-id="903cc-129">如需 Azure CLI 的詳細資訊，請參閱 [Azure CLI 文件](https://docs.microsoft.com/cli/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="903cc-129">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="903cc-130">您可以在 [Azure App Service 文件](../app-service-cli-samples.md)中找到其他的 App Service CLI 指令碼範例。</span><span class="sxs-lookup"><span data-stu-id="903cc-130">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
