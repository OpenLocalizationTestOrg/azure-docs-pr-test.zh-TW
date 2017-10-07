---
title: "CLI 指令碼範例-aaaAzure 建立 web 應用程式並部署從本機 Git 儲存機制的程式碼 |Microsoft 文件"
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
ms.openlocfilehash: 5ad75394c40025d8941282eabeaf34c19c72ee1a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-web-app-and-deploy-code-from-a-local-git-repository"></a><span data-ttu-id="4fdad-103">建立 Web 應用程式並從本機 Git 存放庫部署程式碼</span><span class="sxs-lookup"><span data-stu-id="4fdad-103">Create a web app and deploy code from a local Git repository</span></span>

<span data-ttu-id="4fdad-104">此範例指令碼會在 App Service 中建立 Web 應用程式及其相關資源，然後在本機 Git 存放庫中部署 Web 應用程式程式碼。</span><span class="sxs-lookup"><span data-stu-id="4fdad-104">This sample script creates a web app in App Service with its related resources, and then deploys your web app code in a local Git repository.</span></span>


[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="4fdad-105">如果您選擇 tooinstall，並在本機上使用 hello CLI，本主題會需要您執行 hello Azure CLI 版本 2.0 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="4fdad-105">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="4fdad-106">執行`az --version`toofind hello 版本。</span><span class="sxs-lookup"><span data-stu-id="4fdad-106">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="4fdad-107">如果您需要 tooinstall 或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="4fdad-107">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="4fdad-108">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="4fdad-108">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/deploy-local-git/deploy-local-git.sh?highlight=3-5 "Create a web app and deploy code from a local Git repository")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="4fdad-109">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="4fdad-109">Script explanation</span></span>

<span data-ttu-id="4fdad-110">此指令碼會使用下列命令的 hello。</span><span class="sxs-lookup"><span data-stu-id="4fdad-110">This script uses hello following commands.</span></span> <span data-ttu-id="4fdad-111">Hello 資料表連結 toocommand 特定文件中的每個命令。</span><span class="sxs-lookup"><span data-stu-id="4fdad-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="4fdad-112">命令</span><span class="sxs-lookup"><span data-stu-id="4fdad-112">Command</span></span> | <span data-ttu-id="4fdad-113">注意事項</span><span class="sxs-lookup"><span data-stu-id="4fdad-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="4fdad-114">az group create</span><span class="sxs-lookup"><span data-stu-id="4fdad-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="4fdad-115">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="4fdad-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="4fdad-116">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="4fdad-116">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="4fdad-117">建立 App Service 方案。</span><span class="sxs-lookup"><span data-stu-id="4fdad-117">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="4fdad-118">az webapp create</span><span class="sxs-lookup"><span data-stu-id="4fdad-118">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="4fdad-119">建立 Azure Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="4fdad-119">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="4fdad-120">az webapp deployment user set</span><span class="sxs-lookup"><span data-stu-id="4fdad-120">az webapp deployment user set</span></span>](https://review.docs.microsoft.com/cli/azure/webapp/deployment/user#set) | <span data-ttu-id="4fdad-121">設定應用程式服務的 hello 帳戶層級部署認證。</span><span class="sxs-lookup"><span data-stu-id="4fdad-121">Sets hello account-level deployment credentials for App Service.</span></span> |
| [<span data-ttu-id="4fdad-122">az webapp deployment source config-local-git</span><span class="sxs-lookup"><span data-stu-id="4fdad-122">az webapp deployment source config-local-git</span></span>](https://review.docs.microsoft.com/cli/azure/webapp/deployment/source#config-local-git) | <span data-ttu-id="4fdad-123">建立本機 Git 存放庫的原始檔控制組態。</span><span class="sxs-lookup"><span data-stu-id="4fdad-123">Creates a source control configuration for a local Git repository.</span></span> |
| [<span data-ttu-id="4fdad-124">az webapp browse</span><span class="sxs-lookup"><span data-stu-id="4fdad-124">az webapp browse</span></span>](https://docs.microsoft.com/cli/azure/webapp#browse) | <span data-ttu-id="4fdad-125">在瀏覽器中開啟 Azure Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="4fdad-125">Open an Azure web app in a browser.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="4fdad-126">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4fdad-126">Next steps</span></span>

<span data-ttu-id="4fdad-127">如需有關 Azure CLI hello 的詳細資訊，請參閱[Azure CLI 文件](https://docs.microsoft.com/cli/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="4fdad-127">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="4fdad-128">其他應用程式服務 CLI 指令碼範例可以在 hello [Azure 應用程式服務文件](../app-service-cli-samples.md)。</span><span class="sxs-lookup"><span data-stu-id="4fdad-128">Additional App Service CLI script samples can be found in hello [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
