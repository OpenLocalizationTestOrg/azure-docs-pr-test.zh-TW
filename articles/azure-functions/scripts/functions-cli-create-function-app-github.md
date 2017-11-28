---
title: "aaaCreate 函式應用程式和部署函式程式碼從 GitHub |Microsoft 文件"
description: "Azure CLI 指令碼範例 - 建立函式應用程式和從 GitHub 部署函式程式碼"
services: functions
keywords: 
author: syntaxc4
ms.author: cfowler
ms.date: 04/27/2017
ms.topic: sample
ms.service: functions
ms.custom: mvc
ms.openlocfilehash: 026886f11909149db695d9a52d0aa37f109f64e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-function-app-and-deploy-function-code-from-github"></a><span data-ttu-id="bc9f8-103">建立函式應用程式和從 GitHub 部署函式程式碼</span><span class="sxs-lookup"><span data-stu-id="bc9f8-103">Create a function app and deploy function code from GitHub</span></span>

<span data-ttu-id="bc9f8-104">這個範例指令碼建立函數應用程式使用 hello[耗用量計劃](../functions-scale.md#consumption-plan)及其相關資源，並部署您的函式程式碼 （而不連續的部署） 的公用 GitHub 儲存機制中。</span><span class="sxs-lookup"><span data-stu-id="bc9f8-104">This sample script creates a function app using hello [consumption plan](../functions-scale.md#consumption-plan) with its related resources, and deploys your function code from a public GitHub repository (without continuous deployment).</span></span> <span data-ttu-id="bc9f8-105">若要從 GitHub 持續傳遞函式程式碼，請參閱[建立函式應用程式和從 GitHub 持續部署](functions-cli-create-function-app-github-continuous.md)</span><span class="sxs-lookup"><span data-stu-id="bc9f8-105">For continuous delivery of function code from GitHub, read [Create a function app and continuously deploy from GitHub](functions-cli-create-function-app-github-continuous.md)</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="bc9f8-106">如果您選擇 tooinstall，並在本機上使用 hello CLI，本主題會需要您執行 hello Azure CLI 版本 2.0 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="bc9f8-106">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="bc9f8-107">執行`az --version`toofind hello 版本。</span><span class="sxs-lookup"><span data-stu-id="bc9f8-107">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="bc9f8-108">如果您需要 tooinstall 或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="bc9f8-108">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="bc9f8-109">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="bc9f8-109">Sample script</span></span>

<span data-ttu-id="bc9f8-110">此指令碼範例會建立 Azure 函式應用程式，並從 GitHub 部署函式程式碼。</span><span class="sxs-lookup"><span data-stu-id="bc9f8-110">This sample creates an Azure Function app and deploys function code from GitHub.</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/deploy-function-app-with-function-github/deploy-function-app-with-function-github.sh?highlight=3 "Create a function app with deployment from GitHub")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="bc9f8-111">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="bc9f8-111">Script explanation</span></span>

<span data-ttu-id="bc9f8-112">Hello 資料表連結 toocommand 特定文件中的每個命令。</span><span class="sxs-lookup"><span data-stu-id="bc9f8-112">Each command in hello table links toocommand specific documentation.</span></span> <span data-ttu-id="bc9f8-113">此指令碼會使用下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="bc9f8-113">This script uses hello following commands:</span></span>

| <span data-ttu-id="bc9f8-114">命令</span><span class="sxs-lookup"><span data-stu-id="bc9f8-114">Command</span></span> | <span data-ttu-id="bc9f8-115">注意事項</span><span class="sxs-lookup"><span data-stu-id="bc9f8-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="bc9f8-116">az group create</span><span class="sxs-lookup"><span data-stu-id="bc9f8-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="bc9f8-117">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="bc9f8-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="bc9f8-118">az storage account create</span><span class="sxs-lookup"><span data-stu-id="bc9f8-118">az storage account create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="bc9f8-119">建立 App Service 方案。</span><span class="sxs-lookup"><span data-stu-id="bc9f8-119">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="bc9f8-120">az functionapp create</span><span class="sxs-lookup"><span data-stu-id="bc9f8-120">az functionapp create</span></span>](https://docs.microsoft.com/cli/azure/appservice/web#delete) | <span data-ttu-id="bc9f8-121">建立 Azure 函式應用程式。</span><span class="sxs-lookup"><span data-stu-id="bc9f8-121">Creates an Azure Function app.</span></span> |
| [<span data-ttu-id="bc9f8-122">az appservice web source-control config</span><span class="sxs-lookup"><span data-stu-id="bc9f8-122">az appservice web source-control config</span></span>](https://docs.microsoft.com/cli/azure/appservice/web/source-control#config) | <span data-ttu-id="bc9f8-123">將函式應用程式關聯到 Git 或 Mercurial 存放庫。</span><span class="sxs-lookup"><span data-stu-id="bc9f8-123">Associates a function app with a Git or Mercurial repository.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="bc9f8-124">後續步驟</span><span class="sxs-lookup"><span data-stu-id="bc9f8-124">Next steps</span></span>

<span data-ttu-id="bc9f8-125">如需有關 Azure CLI hello 的詳細資訊，請參閱[Azure CLI 文件](https://docs.microsoft.com/cli/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="bc9f8-125">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="bc9f8-126">其他 Azure 函式 CLI 指令碼範例可以在 hello [Azure 函式文件](../functions-cli-samples.md)。</span><span class="sxs-lookup"><span data-stu-id="bc9f8-126">Additional Azure Functions CLI script samples can be found in hello [Azure Functions documentation](../functions-cli-samples.md).</span></span>
