---
title: "建立函式應用程式和從 GitHub 部署函式程式碼 | Microsoft Docs"
description: "Azure CLI 指令碼範例 - 建立函式應用程式和從 GitHub 部署函式程式碼"
services: functions
keywords: 
author: syntaxc4
ms.author: cfowler
ms.date: 04/27/2017
ms.topic: sample
ms.service: functions
ms.custom: mvc
ms.openlocfilehash: d67e85f91c80efe464fceb1105243bedfba83a0f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-function-app-and-deploy-function-code-from-github"></a><span data-ttu-id="cc649-103">建立函式應用程式和從 GitHub 部署函式程式碼</span><span class="sxs-lookup"><span data-stu-id="cc649-103">Create a function app and deploy function code from GitHub</span></span>

<span data-ttu-id="cc649-104">此範例指令碼會使用[取用方案](../functions-scale.md#consumption-plan)建立函式應用程式及其相關資源，然後從公用 GitHub 存放庫部署您的函式程式碼 (沒有持續部署)。</span><span class="sxs-lookup"><span data-stu-id="cc649-104">This sample script creates a function app using the [consumption plan](../functions-scale.md#consumption-plan) with its related resources, and deploys your function code from a public GitHub repository (without continuous deployment).</span></span> <span data-ttu-id="cc649-105">若要從 GitHub 持續傳遞函式程式碼，請參閱[建立函式應用程式和從 GitHub 持續部署](functions-cli-create-function-app-github-continuous.md)</span><span class="sxs-lookup"><span data-stu-id="cc649-105">For continuous delivery of function code from GitHub, read [Create a function app and continuously deploy from GitHub](functions-cli-create-function-app-github-continuous.md)</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="cc649-106">如果您選擇在本機安裝和使用 CLI，本主題會要求您執行 Azure CLI 2.0 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="cc649-106">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="cc649-107">執行 `az --version` 以尋找版本。</span><span class="sxs-lookup"><span data-stu-id="cc649-107">Run `az --version` to find the version.</span></span> <span data-ttu-id="cc649-108">如果您需要安裝或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="cc649-108">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="cc649-109">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="cc649-109">Sample script</span></span>

<span data-ttu-id="cc649-110">此指令碼範例會建立 Azure 函式應用程式，並從 GitHub 部署函式程式碼。</span><span class="sxs-lookup"><span data-stu-id="cc649-110">This sample creates an Azure Function app and deploys function code from GitHub.</span></span>

<span data-ttu-id="cc649-111">[!code-azurecli-interactive[主要](../../../cli_scripts/azure-functions/deploy-function-app-with-function-github/deploy-function-app-with-function-github.sh?highlight=3 "建立可從 GitHub 部署的函式應用程式")]</span><span class="sxs-lookup"><span data-stu-id="cc649-111">[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/deploy-function-app-with-function-github/deploy-function-app-with-function-github.sh?highlight=3 "Create a function app with deployment from GitHub")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="cc649-112">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="cc649-112">Script explanation</span></span>

<span data-ttu-id="cc649-113">下表中的每個命令都會連結至命令特定的文件。</span><span class="sxs-lookup"><span data-stu-id="cc649-113">Each command in the table links to command specific documentation.</span></span> <span data-ttu-id="cc649-114">此指令碼會使用下列命令：</span><span class="sxs-lookup"><span data-stu-id="cc649-114">This script uses the following commands:</span></span>

| <span data-ttu-id="cc649-115">命令</span><span class="sxs-lookup"><span data-stu-id="cc649-115">Command</span></span> | <span data-ttu-id="cc649-116">注意事項</span><span class="sxs-lookup"><span data-stu-id="cc649-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="cc649-117">az group create</span><span class="sxs-lookup"><span data-stu-id="cc649-117">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="cc649-118">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="cc649-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="cc649-119">az storage account create</span><span class="sxs-lookup"><span data-stu-id="cc649-119">az storage account create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="cc649-120">建立 App Service 方案。</span><span class="sxs-lookup"><span data-stu-id="cc649-120">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="cc649-121">az functionapp create</span><span class="sxs-lookup"><span data-stu-id="cc649-121">az functionapp create</span></span>](https://docs.microsoft.com/cli/azure/appservice/web#delete) | <span data-ttu-id="cc649-122">建立 Azure 函式應用程式。</span><span class="sxs-lookup"><span data-stu-id="cc649-122">Creates an Azure Function app.</span></span> |
| [<span data-ttu-id="cc649-123">az appservice web source-control config</span><span class="sxs-lookup"><span data-stu-id="cc649-123">az appservice web source-control config</span></span>](https://docs.microsoft.com/cli/azure/appservice/web/source-control#config) | <span data-ttu-id="cc649-124">將函式應用程式關聯到 Git 或 Mercurial 存放庫。</span><span class="sxs-lookup"><span data-stu-id="cc649-124">Associates a function app with a Git or Mercurial repository.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="cc649-125">後續步驟</span><span class="sxs-lookup"><span data-stu-id="cc649-125">Next steps</span></span>

<span data-ttu-id="cc649-126">如需 Azure CLI 的詳細資訊，請參閱 [Azure CLI 文件](https://docs.microsoft.com/cli/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="cc649-126">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="cc649-127">您可以在 [Azure Functions 文件](../functions-cli-samples.md)中找到其他 Azure Functions CLI 指令碼範例。</span><span class="sxs-lookup"><span data-stu-id="cc649-127">Additional Azure Functions CLI script samples can be found in the [Azure Functions documentation](../functions-cli-samples.md).</span></span>
