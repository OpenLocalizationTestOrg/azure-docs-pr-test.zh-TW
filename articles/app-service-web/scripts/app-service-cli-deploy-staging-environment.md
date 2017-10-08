---
title: "CLI 指令碼範例-aaaAzure 建立 web 應用程式和部署程式碼 tooa 預備環境 |Microsoft 文件"
description: "Azure CLI 指令碼範例-建立 web 應用程式和部署程式碼 tooa 預備環境"
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
ms.openlocfilehash: cd07f5eda31041effd7b7334f5ecc04e6c1a0514
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-web-app-and-deploy-code-tooa-staging-environment"></a><span data-ttu-id="c1cbf-103">建立 web 應用程式和部署程式碼 tooa 預備環境</span><span class="sxs-lookup"><span data-stu-id="c1cbf-103">Create a web app and deploy code tooa staging environment</span></span>

<span data-ttu-id="c1cbf-104">這個範例指令碼應用程式服務中建立 web 應用程式呼叫 「 預備 」，其他的部署位置與，然後部署範例應用程式 toohello 「 預備 」 位置。</span><span class="sxs-lookup"><span data-stu-id="c1cbf-104">This sample script creates a web app in App Service with an additional deployment slot called "staging", and then deploys a sample app toohello "staging" slot.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="c1cbf-105">如果您選擇 tooinstall，並在本機上使用 hello CLI，本主題會需要您執行 hello Azure CLI 版本 2.0 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="c1cbf-105">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="c1cbf-106">執行`az --version`toofind hello 版本。</span><span class="sxs-lookup"><span data-stu-id="c1cbf-106">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="c1cbf-107">如果您需要 tooinstall 或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="c1cbf-107">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="c1cbf-108">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="c1cbf-108">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/deploy-deployment-slot/deploy-deployment-slot.sh "Create a web app and deploy code tooa staging environment")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="c1cbf-109">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="c1cbf-109">Script explanation</span></span>

<span data-ttu-id="c1cbf-110">此指令碼會使用下列命令的 hello。</span><span class="sxs-lookup"><span data-stu-id="c1cbf-110">This script uses hello following commands.</span></span> <span data-ttu-id="c1cbf-111">Hello 資料表連結 toocommand 特定文件中的每個命令。</span><span class="sxs-lookup"><span data-stu-id="c1cbf-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="c1cbf-112">命令</span><span class="sxs-lookup"><span data-stu-id="c1cbf-112">Command</span></span> | <span data-ttu-id="c1cbf-113">注意事項</span><span class="sxs-lookup"><span data-stu-id="c1cbf-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="c1cbf-114">az group create</span><span class="sxs-lookup"><span data-stu-id="c1cbf-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="c1cbf-115">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="c1cbf-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="c1cbf-116">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="c1cbf-116">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="c1cbf-117">建立 App Service 方案。</span><span class="sxs-lookup"><span data-stu-id="c1cbf-117">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="c1cbf-118">az webapp create</span><span class="sxs-lookup"><span data-stu-id="c1cbf-118">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="c1cbf-119">建立 Azure Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c1cbf-119">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="c1cbf-120">az webapp deployment slot create</span><span class="sxs-lookup"><span data-stu-id="c1cbf-120">az webapp deployment slot create</span></span>](https://docs.microsoft.com/cli/azure/webapp/deployment/slot#create) | <span data-ttu-id="c1cbf-121">建立部署位置。</span><span class="sxs-lookup"><span data-stu-id="c1cbf-121">Create a deployment slot.</span></span> |
| [<span data-ttu-id="c1cbf-122">az webapp deployment source config</span><span class="sxs-lookup"><span data-stu-id="c1cbf-122">az webapp deployment source config</span></span>](https://docs.microsoft.com/cli/azure/webapp/deployment/source#config) | <span data-ttu-id="c1cbf-123">將 Azure Web 應用程式關聯到 Git 或 Mercurial 存放庫。</span><span class="sxs-lookup"><span data-stu-id="c1cbf-123">Associates an Azure web app with a Git or Mercurial repository.</span></span> |
| [<span data-ttu-id="c1cbf-124">az webapp browse</span><span class="sxs-lookup"><span data-stu-id="c1cbf-124">az webapp browse</span></span>](https://docs.microsoft.com/cli/azure/webapp#browse) | <span data-ttu-id="c1cbf-125">在瀏覽器中開啟 Azure Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c1cbf-125">Open an Azure web app in a browser.</span></span> |
| [<span data-ttu-id="c1cbf-126">az webapp deployment slot swap</span><span class="sxs-lookup"><span data-stu-id="c1cbf-126">az webapp deployment slot swap</span></span>](https://docs.microsoft.com/cli/azure/webapp/deployment/slot#swap) | <span data-ttu-id="c1cbf-127">將指定的部署位置切換到生產環境。</span><span class="sxs-lookup"><span data-stu-id="c1cbf-127">Swap a specified deployment slot into production.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="c1cbf-128">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c1cbf-128">Next steps</span></span>

<span data-ttu-id="c1cbf-129">如需有關 Azure CLI hello 的詳細資訊，請參閱[Azure CLI 文件](https://docs.microsoft.com/cli/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="c1cbf-129">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="c1cbf-130">其他應用程式服務 CLI 指令碼範例可以在 hello [Azure 應用程式服務文件](../app-service-cli-samples.md)。</span><span class="sxs-lookup"><span data-stu-id="c1cbf-130">Additional App Service CLI script samples can be found in hello [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
