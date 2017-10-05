---
title: "建立函式應用程式和從 Visual Studio Team Services 部署函式程式碼 | Microsoft Docs"
description: "建立函式應用程式和從 Visual Studio Team Services 部署函式程式碼"
services: functions
keywords: 
author: syntaxc4
ms.author: cfowler
ms.date: 04/28/2017
ms.topic: sample
ms.service: functions
ms.custom: mvc
ms.openlocfilehash: 2ef177b55ad7ffd351156821f429e6ff8fbeccc7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-app-service"></a><span data-ttu-id="c6398-103">建立 App Service</span><span class="sxs-lookup"><span data-stu-id="c6398-103">Create an App Service</span></span>

<span data-ttu-id="c6398-104">在此案例中，您將學習如何使用[取用方案](../functions-scale.md#consumption-plan)建立函式應用程式及其相關資源，然後從 Visual Studio Team Services (VSTS) 存放庫持續部署您的函式程式碼。</span><span class="sxs-lookup"><span data-stu-id="c6398-104">In this scenario you will learn how to create a function app using the [consumption plan](../functions-scale.md#consumption-plan) with its related resources, and continuously deploys your function code from a Visual Studio Team Services (VSTS) repository.</span></span> <span data-ttu-id="c6398-105">在此範例中，您將需要：</span><span class="sxs-lookup"><span data-stu-id="c6398-105">In this sample, you will need:</span></span>

* <span data-ttu-id="c6398-106">一個含有函式程式碼的 VSTS 存放庫 (您必須有此存放庫的系統管理權限)。</span><span class="sxs-lookup"><span data-stu-id="c6398-106">A VSTS repository with functions code, that you have administrative permissions for.</span></span>
* <span data-ttu-id="c6398-107">您 GitHub 帳戶的[個人存取權杖 (PAT)](https://help.github.com/articles/creating-an-access-token-for-command-line-use)。</span><span class="sxs-lookup"><span data-stu-id="c6398-107">A [Personal Access Token (PAT)](https://help.github.com/articles/creating-an-access-token-for-command-line-use) for your GitHub account.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="c6398-108">如果您選擇在本機安裝和使用 CLI，本主題會要求您執行 Azure CLI 2.0 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="c6398-108">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="c6398-109">執行 `az --version` 以尋找版本。</span><span class="sxs-lookup"><span data-stu-id="c6398-109">Run `az --version` to find the version.</span></span> <span data-ttu-id="c6398-110">如果您需要安裝或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="c6398-110">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="c6398-111">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="c6398-111">Sample script</span></span>

<span data-ttu-id="c6398-112">此指令碼範例會建立 Azure 函數應用程式，並從 Visual Studio Team Services 部署函式程式碼。</span><span class="sxs-lookup"><span data-stu-id="c6398-112">This sample creates an Azure Function app and deploys function code from Visual Studio Team Services.</span></span>

<span data-ttu-id="c6398-113">[!code-azurecli-interactive[主要](../../../cli_scripts/azure-functions/deploy-function-app-with-function-vsts/deploy-function-app-with-function-vsts.sh?highlight=3-4 "Azure 服務")]</span><span class="sxs-lookup"><span data-stu-id="c6398-113">[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/deploy-function-app-with-function-vsts/deploy-function-app-with-function-vsts.sh?highlight=3-4 "Azure Service")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="c6398-114">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="c6398-114">Script explanation</span></span>

<span data-ttu-id="c6398-115">此指令碼使用下列命令來建立資源群組、Web 應用程式、documentdb 和所有相關資源。</span><span class="sxs-lookup"><span data-stu-id="c6398-115">This script uses the following commands to create a resource group, web app, documentdb and all related resources.</span></span> <span data-ttu-id="c6398-116">下表中的每個命令都會連結至命令特定的文件。</span><span class="sxs-lookup"><span data-stu-id="c6398-116">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="c6398-117">命令</span><span class="sxs-lookup"><span data-stu-id="c6398-117">Command</span></span> | <span data-ttu-id="c6398-118">注意事項</span><span class="sxs-lookup"><span data-stu-id="c6398-118">Notes</span></span> |
|---|---|
| [<span data-ttu-id="c6398-119">az group create</span><span class="sxs-lookup"><span data-stu-id="c6398-119">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="c6398-120">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="c6398-120">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="c6398-121">az storage account create</span><span class="sxs-lookup"><span data-stu-id="c6398-121">az storage account create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="c6398-122">建立 App Service 方案。</span><span class="sxs-lookup"><span data-stu-id="c6398-122">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="c6398-123">az functionapp create</span><span class="sxs-lookup"><span data-stu-id="c6398-123">az functionapp create</span></span>](https://docs.microsoft.com/cli/azure/appservice/web#delete) |
| [<span data-ttu-id="c6398-124">az appservice web source-control config</span><span class="sxs-lookup"><span data-stu-id="c6398-124">az appservice web source-control config</span></span>](https://docs.microsoft.com/cli/azure/appservice/web/source-control#config) | <span data-ttu-id="c6398-125">將函式應用程式關聯到 Git 或 Mercurial 存放庫。</span><span class="sxs-lookup"><span data-stu-id="c6398-125">Associates a function app with a Git or Mercurial repository.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="c6398-126">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c6398-126">Next steps</span></span>

<span data-ttu-id="c6398-127">如需 Azure CLI 的詳細資訊，請參閱 [Azure CLI 文件](https://docs.microsoft.com/cli/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="c6398-127">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="c6398-128">您可以在 [Azure Functions 文件](../functions-cli-samples.md)中找到其他 Azure Functions CLI 指令碼範例。</span><span class="sxs-lookup"><span data-stu-id="c6398-128">Additional Azure Functions CLI script samples can be found in the [Azure Functions documentation](../functions-cli-samples.md).</span></span>
