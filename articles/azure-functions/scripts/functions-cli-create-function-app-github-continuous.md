---
title: "aaaCreate 函式應用程式和部署函式程式碼從 GitHub |Microsoft 文件"
description: "建立函式應用程式和從 GitHub 部署函式程式碼"
services: functions
ms.service: functions
keywords: 
ms.devlang: azurecli
author: syntaxc4
ms.author: cfowler
ms.date: 04/27/2017
ms.topic: sample
ms.custom: mvc
ms.openlocfilehash: 4d44204b899b32af464260db51ed98bcf00eb2bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-app-service"></a><span data-ttu-id="cf60d-103">建立 App Service</span><span class="sxs-lookup"><span data-stu-id="cf60d-103">Create an App Service</span></span>

<span data-ttu-id="cf60d-104">這個範例指令碼建立函數應用程式使用 hello[耗用量計劃](../functions-scale.md#consumption-plan)及其相關資源，並持續部署您的 GitHub 儲存機制的函式程式碼。</span><span class="sxs-lookup"><span data-stu-id="cf60d-104">This sample script creates a function app using hello [consumption plan](../functions-scale.md#consumption-plan) with its related resources, and continuously deploys your function code from a GitHub repository.</span></span> <span data-ttu-id="cf60d-105">在此範例中，您需要：</span><span class="sxs-lookup"><span data-stu-id="cf60d-105">In this sample, you need:</span></span>

* <span data-ttu-id="cf60d-106">一個含有函式程式碼的 GitHub 存放庫 (您必須有此存放庫的系統管理權限)。</span><span class="sxs-lookup"><span data-stu-id="cf60d-106">A GitHub repository with functions code, that you have administrative permissions for.</span></span>
* <span data-ttu-id="cf60d-107">您 GitHub 帳戶的[個人存取權杖 (PAT)](https://help.github.com/articles/creating-an-access-token-for-command-line-use)。</span><span class="sxs-lookup"><span data-stu-id="cf60d-107">A [Personal Access Token (PAT)](https://help.github.com/articles/creating-an-access-token-for-command-line-use) for your GitHub account.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="cf60d-108">如果您選擇 tooinstall，並在本機上使用 hello CLI，本主題會需要您執行 hello Azure CLI 版本 2.0 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="cf60d-108">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="cf60d-109">執行`az --version`toofind hello 版本。</span><span class="sxs-lookup"><span data-stu-id="cf60d-109">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="cf60d-110">如果您需要 tooinstall 或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="cf60d-110">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="cf60d-111">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="cf60d-111">Sample script</span></span>

<span data-ttu-id="cf60d-112">此指令碼範例會建立 Azure 函式應用程式，並從 GitHub 部署函式程式碼。</span><span class="sxs-lookup"><span data-stu-id="cf60d-112">This sample creates an Azure Function app and deploys function code from GitHub.</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/deploy-function-app-with-function-github-continuous/deploy-function-app-with-function-github-continuous.sh?highlight=3-4 "Azure Service")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="cf60d-113">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="cf60d-113">Script explanation</span></span>

<span data-ttu-id="cf60d-114">Hello 資料表連結 toocommand 特定文件中的每個命令。</span><span class="sxs-lookup"><span data-stu-id="cf60d-114">Each command in hello table links toocommand specific documentation.</span></span> <span data-ttu-id="cf60d-115">此指令碼會使用 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="cf60d-115">This script uses hello following:</span></span>

| <span data-ttu-id="cf60d-116">命令</span><span class="sxs-lookup"><span data-stu-id="cf60d-116">Command</span></span> | <span data-ttu-id="cf60d-117">注意事項</span><span class="sxs-lookup"><span data-stu-id="cf60d-117">Notes</span></span> |
|---|---|
| [<span data-ttu-id="cf60d-118">az group create</span><span class="sxs-lookup"><span data-stu-id="cf60d-118">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="cf60d-119">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="cf60d-119">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="cf60d-120">az storage account create</span><span class="sxs-lookup"><span data-stu-id="cf60d-120">az storage account create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="cf60d-121">建立 App Service 方案。</span><span class="sxs-lookup"><span data-stu-id="cf60d-121">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="cf60d-122">az functionapp create</span><span class="sxs-lookup"><span data-stu-id="cf60d-122">az functionapp create</span></span>](https://docs.microsoft.com/cli/azure/appservice/web#delete) |
| [<span data-ttu-id="cf60d-123">az appservice web source-control config</span><span class="sxs-lookup"><span data-stu-id="cf60d-123">az appservice web source-control config</span></span>](https://docs.microsoft.com/cli/azure/appservice/web/source-control#config) | <span data-ttu-id="cf60d-124">將函式應用程式關聯到 Git 或 Mercurial 存放庫。</span><span class="sxs-lookup"><span data-stu-id="cf60d-124">Associates a function app with a Git or Mercurial repository.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="cf60d-125">後續步驟</span><span class="sxs-lookup"><span data-stu-id="cf60d-125">Next steps</span></span>

<span data-ttu-id="cf60d-126">如需有關 Azure CLI hello 的詳細資訊，請參閱[Azure CLI 文件](https://docs.microsoft.com/cli/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="cf60d-126">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="cf60d-127">其他 Azure 函式 CLI 指令碼範例可以在 hello [Azure 函式文件](../functions-cli-samples.md)。</span><span class="sxs-lookup"><span data-stu-id="cf60d-127">Additional Azure Functions CLI script samples can be found in hello [Azure Functions documentation](../functions-cli-samples.md).</span></span>
