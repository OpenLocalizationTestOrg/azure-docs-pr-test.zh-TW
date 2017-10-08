---
title: "aaaCreate 函式應用程式和部署函式程式碼，從 Visual Studio Team Services |Microsoft 文件"
description: "建立函式應用程式和從 Visual Studio Team Services 部署函式程式碼"
services: functions
keywords: 
author: syntaxc4
ms.author: cfowler
ms.date: 04/28/2017
ms.topic: sample
ms.service: functions
ms.custom: mvc
ms.openlocfilehash: 774bee73025cc9ac46f8b2a6c10edbfa3c2d353b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-app-service"></a><span data-ttu-id="34424-103">建立 App Service</span><span class="sxs-lookup"><span data-stu-id="34424-103">Create an App Service</span></span>

<span data-ttu-id="34424-104">在此案例中您將學習如何 toocreate 函式的應用程式使用 hello[耗用量計劃](../functions-scale.md#consumption-plan)及其相關資源，並持續部署您的函式程式碼，從 Visual Studio Team Services (VSTS) 儲存機制。</span><span class="sxs-lookup"><span data-stu-id="34424-104">In this scenario you will learn how toocreate a function app using hello [consumption plan](../functions-scale.md#consumption-plan) with its related resources, and continuously deploys your function code from a Visual Studio Team Services (VSTS) repository.</span></span> <span data-ttu-id="34424-105">在此範例中，您將需要：</span><span class="sxs-lookup"><span data-stu-id="34424-105">In this sample, you will need:</span></span>

* <span data-ttu-id="34424-106">一個含有函式程式碼的 VSTS 存放庫 (您必須有此存放庫的系統管理權限)。</span><span class="sxs-lookup"><span data-stu-id="34424-106">A VSTS repository with functions code, that you have administrative permissions for.</span></span>
* <span data-ttu-id="34424-107">您 GitHub 帳戶的[個人存取權杖 (PAT)](https://help.github.com/articles/creating-an-access-token-for-command-line-use)。</span><span class="sxs-lookup"><span data-stu-id="34424-107">A [Personal Access Token (PAT)](https://help.github.com/articles/creating-an-access-token-for-command-line-use) for your GitHub account.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="34424-108">如果您選擇 tooinstall，並在本機上使用 hello CLI，本主題會需要您執行 hello Azure CLI 版本 2.0 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="34424-108">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="34424-109">執行`az --version`toofind hello 版本。</span><span class="sxs-lookup"><span data-stu-id="34424-109">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="34424-110">如果您需要 tooinstall 或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="34424-110">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="34424-111">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="34424-111">Sample script</span></span>

<span data-ttu-id="34424-112">此指令碼範例會建立 Azure 函數應用程式，並從 Visual Studio Team Services 部署函式程式碼。</span><span class="sxs-lookup"><span data-stu-id="34424-112">This sample creates an Azure Function app and deploys function code from Visual Studio Team Services.</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/deploy-function-app-with-function-vsts/deploy-function-app-with-function-vsts.sh?highlight=3-4 "Azure Service")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="34424-113">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="34424-113">Script explanation</span></span>

<span data-ttu-id="34424-114">此指令碼會使用下列命令 toocreate 資源群組、 web 應用程式中，documentdb 和所有相關的資源的 hello。</span><span class="sxs-lookup"><span data-stu-id="34424-114">This script uses hello following commands toocreate a resource group, web app, documentdb and all related resources.</span></span> <span data-ttu-id="34424-115">Hello 資料表連結 toocommand 特定文件中的每個命令。</span><span class="sxs-lookup"><span data-stu-id="34424-115">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="34424-116">命令</span><span class="sxs-lookup"><span data-stu-id="34424-116">Command</span></span> | <span data-ttu-id="34424-117">注意事項</span><span class="sxs-lookup"><span data-stu-id="34424-117">Notes</span></span> |
|---|---|
| [<span data-ttu-id="34424-118">az group create</span><span class="sxs-lookup"><span data-stu-id="34424-118">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="34424-119">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="34424-119">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="34424-120">az storage account create</span><span class="sxs-lookup"><span data-stu-id="34424-120">az storage account create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="34424-121">建立 App Service 方案。</span><span class="sxs-lookup"><span data-stu-id="34424-121">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="34424-122">az functionapp create</span><span class="sxs-lookup"><span data-stu-id="34424-122">az functionapp create</span></span>](https://docs.microsoft.com/cli/azure/appservice/web#delete) |
| [<span data-ttu-id="34424-123">az appservice web source-control config</span><span class="sxs-lookup"><span data-stu-id="34424-123">az appservice web source-control config</span></span>](https://docs.microsoft.com/cli/azure/appservice/web/source-control#config) | <span data-ttu-id="34424-124">將函式應用程式關聯到 Git 或 Mercurial 存放庫。</span><span class="sxs-lookup"><span data-stu-id="34424-124">Associates a function app with a Git or Mercurial repository.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="34424-125">後續步驟</span><span class="sxs-lookup"><span data-stu-id="34424-125">Next steps</span></span>

<span data-ttu-id="34424-126">如需有關 Azure CLI hello 的詳細資訊，請參閱[Azure CLI 文件](https://docs.microsoft.com/cli/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="34424-126">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="34424-127">其他 Azure 函式 CLI 指令碼範例可以在 hello [Azure 函式文件](../functions-cli-samples.md)。</span><span class="sxs-lookup"><span data-stu-id="34424-127">Additional Azure Functions CLI script samples can be found in hello [Azure Functions documentation](../functions-cli-samples.md).</span></span>
