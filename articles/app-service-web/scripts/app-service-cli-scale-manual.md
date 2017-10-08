---
title: "CLI 指令碼範例-aaaAzure 調整 Web 應用程式使用 Azure CLI 2.0 手動 |Microsoft 文件"
description: "Azure CLI 指令碼範例 - 使用 Azure CLI 2.0 手動調整 Web 應用程式"
services: appservice
documentationcenter: appservice
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 251d9074-8fff-4121-ad16-9eca9556ac96
ms.service: app-service
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 06/19/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 64464c8a44522fdc2c8f3d0192388302a1d12667
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="scale-a-web-app-manually"></a><span data-ttu-id="fb275-103">手動調整 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="fb275-103">Scale a web app manually</span></span>

<span data-ttu-id="fb275-104">在此案例中，您將學習 toocreate 資源群組、 應用程式服務方案和 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="fb275-104">In this scenario you will learn toocreate a resource group, app service plan and web app.</span></span> <span data-ttu-id="fb275-105">然後，您會縮放 hello App Service 方案，從單一執行個體 toomultiple 執行個體。</span><span class="sxs-lookup"><span data-stu-id="fb275-105">You will then scale hello App Service Plan from a single instance toomultiple instances.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="fb275-106">如果您選擇 tooinstall，並在本機上使用 hello CLI，本主題會需要您執行 hello Azure CLI 版本 2.0 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="fb275-106">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="fb275-107">執行`az --version`toofind hello 版本。</span><span class="sxs-lookup"><span data-stu-id="fb275-107">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="fb275-108">如果您需要 tooinstall 或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="fb275-108">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="fb275-109">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="fb275-109">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/scale-manual/scale-manual.sh "Manual Scale")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="fb275-110">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="fb275-110">Script explanation</span></span>

<span data-ttu-id="fb275-111">此指令碼會使用下列命令 toocreate 資源群組、 web 應用程式和所有相關的資源的 hello。</span><span class="sxs-lookup"><span data-stu-id="fb275-111">This script uses hello following commands toocreate a resource group, web app, and all related resources.</span></span> <span data-ttu-id="fb275-112">Hello 資料表連結 toocommand 特定文件中的每個命令。</span><span class="sxs-lookup"><span data-stu-id="fb275-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="fb275-113">命令</span><span class="sxs-lookup"><span data-stu-id="fb275-113">Command</span></span> | <span data-ttu-id="fb275-114">注意事項</span><span class="sxs-lookup"><span data-stu-id="fb275-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="fb275-115">az group create</span><span class="sxs-lookup"><span data-stu-id="fb275-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="fb275-116">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="fb275-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="fb275-117">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="fb275-117">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="fb275-118">建立 App Service 方案。</span><span class="sxs-lookup"><span data-stu-id="fb275-118">Creates an App Service plan.</span></span> <span data-ttu-id="fb275-119">這就像是 Azure Web 應用程式的伺服器陣列。</span><span class="sxs-lookup"><span data-stu-id="fb275-119">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="fb275-120">az webapp create</span><span class="sxs-lookup"><span data-stu-id="fb275-120">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="fb275-121">建立 Azure Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="fb275-121">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="fb275-122">az appservice plan update</span><span class="sxs-lookup"><span data-stu-id="fb275-122">az appservice plan update</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#update) | <span data-ttu-id="fb275-123">更新 hello 應用程式服務方案的屬性。</span><span class="sxs-lookup"><span data-stu-id="fb275-123">Updates properties of hello App Service plan.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="fb275-124">後續步驟</span><span class="sxs-lookup"><span data-stu-id="fb275-124">Next steps</span></span>

<span data-ttu-id="fb275-125">如需有關 Azure CLI hello 的詳細資訊，請參閱[Azure CLI 文件](https://docs.microsoft.com/cli/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="fb275-125">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="fb275-126">其他應用程式服務 CLI 指令碼範例可以在 hello [Azure 應用程式服務文件](../app-service-cli-samples.md)。</span><span class="sxs-lookup"><span data-stu-id="fb275-126">Additional App Service CLI script samples can be found in hello [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
