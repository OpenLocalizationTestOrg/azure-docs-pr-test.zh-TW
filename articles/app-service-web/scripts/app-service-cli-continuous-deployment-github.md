---
title: "Azure CLI 指令碼範例 - 建立可從 GitHub 連續部署的 Web 應用程式 | Microsoft Docs"
description: "Azure CLI 指令碼範例 - 建立可從 GitHub 連續部署的 Web 應用程式"
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
ms.tgt_pltfrm: na
ms.topic: sample
ms.date: 06/19/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: a12085a7a8146c22d6b079381542d4fe3a8e6e87
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-web-app-with-continuous-deployment-from-github"></a><span data-ttu-id="71b26-103">建立可從 GitHub 連續部署的 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="71b26-103">Create a web app with continuous deployment from GitHub</span></span>

<span data-ttu-id="71b26-104">此範例指令碼會在 App Service 中建立 Web 應用程式及其相關資源，然後設定從 GitHub 存放庫進行的連續部署。</span><span class="sxs-lookup"><span data-stu-id="71b26-104">This sample script creates a web app in App Service with its related resources, and then sets up continuous deployment from a GitHub repository.</span></span> <span data-ttu-id="71b26-105">如需進行沒有連續部署的 GitHub 部署，請參閱[建立 Web 應用程式並從 GitHub 部署程式碼](app-service-cli-deploy-github.md)。</span><span class="sxs-lookup"><span data-stu-id="71b26-105">For GitHub deployment without continuous deployment, see [Create a web app and deploy code from GitHub](app-service-cli-deploy-github.md).</span></span> <span data-ttu-id="71b26-106">在此範例中，您將需要：</span><span class="sxs-lookup"><span data-stu-id="71b26-106">In this sample, you will need:</span></span>

* <span data-ttu-id="71b26-107">具有應用程式程式碼的 GitHub 存放庫 (您必須有此存放庫的系統管理權限)。</span><span class="sxs-lookup"><span data-stu-id="71b26-107">A GitHub repository with application code, that you have administrative permissions for.</span></span>
* <span data-ttu-id="71b26-108">您 GitHub 帳戶的[個人存取權杖 (PAT)](https://help.github.com/articles/creating-an-access-token-for-command-line-use)。</span><span class="sxs-lookup"><span data-stu-id="71b26-108">A [Personal Access Token (PAT)](https://help.github.com/articles/creating-an-access-token-for-command-line-use) for your GitHub account.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="71b26-109">如果您選擇在本機安裝和使用 CLI，本主題會要求您執行 Azure CLI 2.0 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="71b26-109">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="71b26-110">執行 `az --version` 以尋找版本。</span><span class="sxs-lookup"><span data-stu-id="71b26-110">Run `az --version` to find the version.</span></span> <span data-ttu-id="71b26-111">如果您需要安裝或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="71b26-111">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="71b26-112">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="71b26-112">Sample script</span></span>

<span data-ttu-id="71b26-113">[!code-azurecli-interactive[主要](../../../cli_scripts/app-service/deploy-github-continuous/deploy-github-continuous.sh?highlight=3-4 "建立可從 GitHub 連續部署的 Web 應用程式")]</span><span class="sxs-lookup"><span data-stu-id="71b26-113">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/deploy-github-continuous/deploy-github-continuous.sh?highlight=3-4 "Create a web app with continuous deployment from GitHub")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="71b26-114">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="71b26-114">Script explanation</span></span>

<span data-ttu-id="71b26-115">此指令碼會使用下列命令。</span><span class="sxs-lookup"><span data-stu-id="71b26-115">This script uses the following commands.</span></span> <span data-ttu-id="71b26-116">下表中的每個命令都會連結至命令特定的文件。</span><span class="sxs-lookup"><span data-stu-id="71b26-116">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="71b26-117">命令</span><span class="sxs-lookup"><span data-stu-id="71b26-117">Command</span></span> | <span data-ttu-id="71b26-118">注意事項</span><span class="sxs-lookup"><span data-stu-id="71b26-118">Notes</span></span> |
|---|---|
| [<span data-ttu-id="71b26-119">az group create</span><span class="sxs-lookup"><span data-stu-id="71b26-119">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="71b26-120">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="71b26-120">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="71b26-121">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="71b26-121">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="71b26-122">建立 App Service 方案。</span><span class="sxs-lookup"><span data-stu-id="71b26-122">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="71b26-123">az webapp create</span><span class="sxs-lookup"><span data-stu-id="71b26-123">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="71b26-124">建立 Azure Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="71b26-124">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="71b26-125">az webapp deployment source config</span><span class="sxs-lookup"><span data-stu-id="71b26-125">az webapp deployment source config</span></span>](https://docs.microsoft.com/cli/azure/webapp/deployment/source#config) | <span data-ttu-id="71b26-126">將 Azure Web 應用程式關聯到 Git 或 Mercurial 存放庫。</span><span class="sxs-lookup"><span data-stu-id="71b26-126">Associates an Azure web app with a Git or Mercurial repository.</span></span> |
| [<span data-ttu-id="71b26-127">az webapp browse</span><span class="sxs-lookup"><span data-stu-id="71b26-127">az webapp browse</span></span>](https://docs.microsoft.com/cli/azure/webapp#browse) | <span data-ttu-id="71b26-128">在瀏覽器中開啟 Azure Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="71b26-128">Open an Azure web app in a browser.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="71b26-129">後續步驟</span><span class="sxs-lookup"><span data-stu-id="71b26-129">Next steps</span></span>

<span data-ttu-id="71b26-130">如需 Azure CLI 的詳細資訊，請參閱 [Azure CLI 文件](https://docs.microsoft.com/cli/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="71b26-130">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="71b26-131">您可以在 [Azure App Service 文件](../app-service-cli-samples.md)中找到其他的 App Service CLI 指令碼範例。</span><span class="sxs-lookup"><span data-stu-id="71b26-131">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
