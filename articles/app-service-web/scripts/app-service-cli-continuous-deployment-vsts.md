---
title: "aaaAzure CLI 指令碼範例-使用 Visual Studio Team Services 中的連續部署建立 web 應用程式 |Microsoft 文件"
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
ms.openlocfilehash: f8d0c2645ec5311296ca9b2df20f97e77bab2283
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-web-app-with-continuous-deployment-from-visual-studio-team-services"></a><span data-ttu-id="269c3-103">建立可從 Visual Studio Team Services 連續部署的 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="269c3-103">Create a web app with continuous deployment from Visual Studio Team Services</span></span>

<span data-ttu-id="269c3-104">此範例指令碼會在 App Service 中建立 Web 應用程式及其相關資源，然後設定從 Visual Studio Team Services 存放庫進行的連續部署。</span><span class="sxs-lookup"><span data-stu-id="269c3-104">This sample script creates a web app in App Service with its related resources, and then sets up continuous deployment from a Visual Studio Team Services repository.</span></span> <span data-ttu-id="269c3-105">針對此範例，您將需要：</span><span class="sxs-lookup"><span data-stu-id="269c3-105">For this sample, you will need:</span></span>

* <span data-ttu-id="269c3-106">具有應用程式程式碼的 Visual Studio Team Services 存放庫 (您必須有此存放庫的系統管理權限)。</span><span class="sxs-lookup"><span data-stu-id="269c3-106">A Visual Studio Team Services repository with application code, that you have administrative permissions for.</span></span>
* <span data-ttu-id="269c3-107">您 Visual Studio Team Services 帳戶的[個人存取權杖 (PAT)](https://www.visualstudio.com/docs/setup-admin/team-services/use-personal-access-tokens-to-authenticate)。</span><span class="sxs-lookup"><span data-stu-id="269c3-107">A [Personal Access Token (PAT)](https://www.visualstudio.com/docs/setup-admin/team-services/use-personal-access-tokens-to-authenticate) for your Visual Studio Team Services account.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="269c3-108">如果您選擇 tooinstall，並在本機上使用 hello CLI，本主題會需要您執行 hello Azure CLI 版本 2.0 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="269c3-108">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="269c3-109">執行`az --version`toofind hello 版本。</span><span class="sxs-lookup"><span data-stu-id="269c3-109">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="269c3-110">如果您需要 tooinstall 或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="269c3-110">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="269c3-111">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="269c3-111">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/deploy-vsts-continuous/deploy-vsts-continuous.sh?highlight=3-4 "Create a web app with continuous deployment from Visual Studio Team Services")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="269c3-112">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="269c3-112">Script explanation</span></span>

<span data-ttu-id="269c3-113">此指令碼會使用下列命令的 hello。</span><span class="sxs-lookup"><span data-stu-id="269c3-113">This script uses hello following commands.</span></span> <span data-ttu-id="269c3-114">Hello 資料表連結 toocommand 特定文件中的每個命令。</span><span class="sxs-lookup"><span data-stu-id="269c3-114">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="269c3-115">命令</span><span class="sxs-lookup"><span data-stu-id="269c3-115">Command</span></span> | <span data-ttu-id="269c3-116">注意事項</span><span class="sxs-lookup"><span data-stu-id="269c3-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="269c3-117">az group create</span><span class="sxs-lookup"><span data-stu-id="269c3-117">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="269c3-118">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="269c3-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="269c3-119">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="269c3-119">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="269c3-120">建立 App Service 方案。</span><span class="sxs-lookup"><span data-stu-id="269c3-120">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="269c3-121">az webapp create</span><span class="sxs-lookup"><span data-stu-id="269c3-121">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="269c3-122">建立 Azure Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="269c3-122">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="269c3-123">az webapp deployment source config</span><span class="sxs-lookup"><span data-stu-id="269c3-123">az webapp deployment source config</span></span>](https://docs.microsoft.com/cli/azure/webapp/deployment/source#config) | <span data-ttu-id="269c3-124">將 Azure Web 應用程式關聯到 Git 或 Mercurial 存放庫。</span><span class="sxs-lookup"><span data-stu-id="269c3-124">Associates an Azure web app with a Git or Mercurial repository.</span></span> |
| [<span data-ttu-id="269c3-125">az webapp browse</span><span class="sxs-lookup"><span data-stu-id="269c3-125">az webapp browse</span></span>](https://docs.microsoft.com/cli/azure/webapp#browse) | <span data-ttu-id="269c3-126">在瀏覽器中開啟 Azure Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="269c3-126">Open an Azure web app in a browser.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="269c3-127">後續步驟</span><span class="sxs-lookup"><span data-stu-id="269c3-127">Next steps</span></span>

<span data-ttu-id="269c3-128">如需有關 Azure CLI hello 的詳細資訊，請參閱[Azure CLI 文件](https://docs.microsoft.com/cli/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="269c3-128">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="269c3-129">其他應用程式服務 CLI 指令碼範例可以在 hello [Azure 應用程式服務文件](../app-service-cli-samples.md)。</span><span class="sxs-lookup"><span data-stu-id="269c3-129">Additional App Service CLI script samples can be found in hello [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
