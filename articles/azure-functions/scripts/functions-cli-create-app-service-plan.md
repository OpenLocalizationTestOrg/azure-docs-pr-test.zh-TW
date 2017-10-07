---
title: "aaaAzure CLI 指令碼範例-應用程式服務方案中建立函式的應用程式 |Microsoft 文件"
description: "Azure CLI 指令碼範例 - 在 App Service 方案中建立函式應用程式"
services: functions
documentationcenter: functions
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 0e221db6-ee2d-4e16-9bf6-a456cd05b6e7
ms.service: functions
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 04/11/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: c0ffbbbf022e5680e5ae3141e784e7c7bced0bc0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-function-app-in-an-app-service-plan"></a><span data-ttu-id="ee542-103">在 App Service 方案中建立函式應用程式</span><span class="sxs-lookup"><span data-stu-id="ee542-103">Create a Function App in an App Service plan</span></span>

<span data-ttu-id="ee542-104">此範例指令碼會建立 Azure 函式應用程式，這是您的函式容器。</span><span class="sxs-lookup"><span data-stu-id="ee542-104">This sample script creates an Azure Function App, which is a container for your functions.</span></span> <span data-ttu-id="ee542-105">使用專用的應用程式服務方案，這表示您的伺服器資源都在建立 hello 函式應用程式。</span><span class="sxs-lookup"><span data-stu-id="ee542-105">hello Function App is created using a dedicated App Service plan, which means your server resources are always on.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="ee542-106">如果您選擇 tooinstall，並在本機上使用 hello CLI，本主題會需要您執行 hello Azure CLI 版本 2.0 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="ee542-106">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="ee542-107">執行`az --version`toofind hello 版本。</span><span class="sxs-lookup"><span data-stu-id="ee542-107">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="ee542-108">如果您需要 tooinstall 或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="ee542-108">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="ee542-109">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="ee542-109">Sample script</span></span>

<span data-ttu-id="ee542-110">此指令碼會使用專用的 [App Service 方案](../functions-scale.md#app-service-plan)建立 Azure 函數應用程式。</span><span class="sxs-lookup"><span data-stu-id="ee542-110">This script creates an Azure Function app using a dedicated [App Service plan](../functions-scale.md#app-service-plan).</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/create-function-app-app-service-plan/create-function-app-app-service-plan.sh "Create an Azure Function on an App Service plan")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="ee542-111">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="ee542-111">Script explanation</span></span>

<span data-ttu-id="ee542-112">Hello 資料表連結 toocommand 特定文件中的每個命令。</span><span class="sxs-lookup"><span data-stu-id="ee542-112">Each command in hello table links toocommand specific documentation.</span></span> <span data-ttu-id="ee542-113">此指令碼會使用下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="ee542-113">This script uses hello following commands:</span></span>

| <span data-ttu-id="ee542-114">命令</span><span class="sxs-lookup"><span data-stu-id="ee542-114">Command</span></span> | <span data-ttu-id="ee542-115">注意事項</span><span class="sxs-lookup"><span data-stu-id="ee542-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="ee542-116">az group create</span><span class="sxs-lookup"><span data-stu-id="ee542-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="ee542-117">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="ee542-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="ee542-118">az storage account create</span><span class="sxs-lookup"><span data-stu-id="ee542-118">az storage account create</span></span>](https://docs.microsoft.com/cli/azure/storage/account#create) | <span data-ttu-id="ee542-119">建立 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="ee542-119">Creates an Azure Storage account.</span></span> |
| [<span data-ttu-id="ee542-120">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="ee542-120">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appserviceplan#create) | <span data-ttu-id="ee542-121">建立 App Service 方案。</span><span class="sxs-lookup"><span data-stu-id="ee542-121">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="ee542-122">az functionapp create</span><span class="sxs-lookup"><span data-stu-id="ee542-122">az functionapp create</span></span>](https://docs.microsoft.com/cli/azure/functionapp#delete) | <span data-ttu-id="ee542-123">建立 Azure 函式應用程式。</span><span class="sxs-lookup"><span data-stu-id="ee542-123">Creates an Azure Function app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="ee542-124">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ee542-124">Next steps</span></span>

<span data-ttu-id="ee542-125">如需有關 Azure CLI hello 的詳細資訊，請參閱[Azure CLI 文件](https://docs.microsoft.com/cli/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="ee542-125">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="ee542-126">其他 Azure 函式 CLI 指令碼範例可以在 hello [Azure 函式文件](../functions-cli-samples.md)。</span><span class="sxs-lookup"><span data-stu-id="ee542-126">Additional Azure Functions CLI script samples can be found in hello [Azure Functions documentation](../functions-cli-samples.md).</span></span>
