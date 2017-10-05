---
title: "Azure CLI 指令碼範例 - 在 App Service 方案中建立函式應用程式 | Microsoft Docs"
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
ms.openlocfilehash: 40c3fa6fa6c07d59e4bf55531e116ba50aa92b91
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-function-app-in-an-app-service-plan"></a><span data-ttu-id="3d056-103">在 App Service 方案中建立函式應用程式</span><span class="sxs-lookup"><span data-stu-id="3d056-103">Create a Function App in an App Service plan</span></span>

<span data-ttu-id="3d056-104">此範例指令碼會建立 Azure 函式應用程式，這是您的函式容器。</span><span class="sxs-lookup"><span data-stu-id="3d056-104">This sample script creates an Azure Function App, which is a container for your functions.</span></span> <span data-ttu-id="3d056-105">系統會使用專用的 App Service 方案建立函數應用程式，這表示您的伺服器資源會永遠啟用。</span><span class="sxs-lookup"><span data-stu-id="3d056-105">The Function App is created using a dedicated App Service plan, which means your server resources are always on.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="3d056-106">如果您選擇在本機安裝和使用 CLI，本主題會要求您執行 Azure CLI 2.0 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="3d056-106">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="3d056-107">執行 `az --version` 以尋找版本。</span><span class="sxs-lookup"><span data-stu-id="3d056-107">Run `az --version` to find the version.</span></span> <span data-ttu-id="3d056-108">如果您需要安裝或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="3d056-108">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="3d056-109">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="3d056-109">Sample script</span></span>

<span data-ttu-id="3d056-110">此指令碼會使用專用的 [App Service 方案](../functions-scale.md#app-service-plan)建立 Azure 函數應用程式。</span><span class="sxs-lookup"><span data-stu-id="3d056-110">This script creates an Azure Function app using a dedicated [App Service plan](../functions-scale.md#app-service-plan).</span></span>

<span data-ttu-id="3d056-111">[!code-azurecli-interactive[主要](../../../cli_scripts/azure-functions/create-function-app-app-service-plan/create-function-app-app-service-plan.sh "在 App Service 方案上建立 Azure 函式")]</span><span class="sxs-lookup"><span data-stu-id="3d056-111">[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/create-function-app-app-service-plan/create-function-app-app-service-plan.sh "Create an Azure Function on an App Service plan")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="3d056-112">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="3d056-112">Script explanation</span></span>

<span data-ttu-id="3d056-113">下表中的每個命令都會連結至命令特定的文件。</span><span class="sxs-lookup"><span data-stu-id="3d056-113">Each command in the table links to command specific documentation.</span></span> <span data-ttu-id="3d056-114">此指令碼會使用下列命令：</span><span class="sxs-lookup"><span data-stu-id="3d056-114">This script uses the following commands:</span></span>

| <span data-ttu-id="3d056-115">命令</span><span class="sxs-lookup"><span data-stu-id="3d056-115">Command</span></span> | <span data-ttu-id="3d056-116">注意事項</span><span class="sxs-lookup"><span data-stu-id="3d056-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="3d056-117">az group create</span><span class="sxs-lookup"><span data-stu-id="3d056-117">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="3d056-118">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="3d056-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="3d056-119">az storage account create</span><span class="sxs-lookup"><span data-stu-id="3d056-119">az storage account create</span></span>](https://docs.microsoft.com/cli/azure/storage/account#create) | <span data-ttu-id="3d056-120">建立 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="3d056-120">Creates an Azure Storage account.</span></span> |
| [<span data-ttu-id="3d056-121">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="3d056-121">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appserviceplan#create) | <span data-ttu-id="3d056-122">建立 App Service 方案。</span><span class="sxs-lookup"><span data-stu-id="3d056-122">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="3d056-123">az functionapp create</span><span class="sxs-lookup"><span data-stu-id="3d056-123">az functionapp create</span></span>](https://docs.microsoft.com/cli/azure/functionapp#delete) | <span data-ttu-id="3d056-124">建立 Azure 函式應用程式。</span><span class="sxs-lookup"><span data-stu-id="3d056-124">Creates an Azure Function app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="3d056-125">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3d056-125">Next steps</span></span>

<span data-ttu-id="3d056-126">如需 Azure CLI 的詳細資訊，請參閱 [Azure CLI 文件](https://docs.microsoft.com/cli/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="3d056-126">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="3d056-127">您可以在 [Azure Functions 文件](../functions-cli-samples.md)中找到其他 Azure Functions CLI 指令碼範例。</span><span class="sxs-lookup"><span data-stu-id="3d056-127">Additional Azure Functions CLI script samples can be found in the [Azure Functions documentation](../functions-cli-samples.md).</span></span>
