---
title: "aaaAzure CLI 指令碼範例-建立無伺服器執行的函式應用程式 |Microsoft 文件"
description: "Azure CLI 指令碼範例 - 建立無伺服器也可執行的函式應用程式"
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
ms.openlocfilehash: 7ec872b642e50827896a73a9e43bcc87233e15c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-function-app-for-serverless-execution"></a><span data-ttu-id="16f25-103">建立無伺服器也可執行的函式應用程式</span><span class="sxs-lookup"><span data-stu-id="16f25-103">Create a Function App for serverless execution</span></span>

<span data-ttu-id="16f25-104">此範例指令碼會建立 Azure 函式應用程式，這是您的函式容器。</span><span class="sxs-lookup"><span data-stu-id="16f25-104">This sample script creates an Azure Function App, which is a container for your functions.</span></span> <span data-ttu-id="16f25-105">hello 函式建立應用程式使用 hello[耗用量計劃](../functions-scale.md#consumption-plan)，這很適合使用事件驅動的無伺服器工作負載。</span><span class="sxs-lookup"><span data-stu-id="16f25-105">hello Function App is created using hello [consumption plan](../functions-scale.md#consumption-plan), which is ideal for event-driven serverless workloads.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="16f25-106">如果您選擇 tooinstall，並在本機上使用 hello CLI，本主題會需要您執行 hello Azure CLI 版本 2.0 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="16f25-106">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="16f25-107">執行`az --version`toofind hello 版本。</span><span class="sxs-lookup"><span data-stu-id="16f25-107">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="16f25-108">如果您需要 tooinstall 或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="16f25-108">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="16f25-109">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="16f25-109">Sample script</span></span>

<span data-ttu-id="16f25-110">此指令碼會建立 Azure 函式應用程式使用 hello[耗用量計劃](../functions-scale.md#consumption-plan)。</span><span class="sxs-lookup"><span data-stu-id="16f25-110">This script creates an Azure Function app using hello [consumption plan](../functions-scale.md#consumption-plan).</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/create-function-app-consumption/create-function-app-consumption.sh "Create an Azure Function on a consumption plan")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="16f25-111">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="16f25-111">Script explanation</span></span>

<span data-ttu-id="16f25-112">Hello 資料表連結 toocommand 特定文件中的每個命令。</span><span class="sxs-lookup"><span data-stu-id="16f25-112">Each command in hello table links toocommand specific documentation.</span></span> <span data-ttu-id="16f25-113">此指令碼會使用下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="16f25-113">This script uses hello following commands:</span></span>

| <span data-ttu-id="16f25-114">命令</span><span class="sxs-lookup"><span data-stu-id="16f25-114">Command</span></span> | <span data-ttu-id="16f25-115">注意事項</span><span class="sxs-lookup"><span data-stu-id="16f25-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="16f25-116">az group create</span><span class="sxs-lookup"><span data-stu-id="16f25-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="16f25-117">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="16f25-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="16f25-118">az storage account create</span><span class="sxs-lookup"><span data-stu-id="16f25-118">az storage account create</span></span>](/cli/azure/storage/account#create) | <span data-ttu-id="16f25-119">建立 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="16f25-119">Creates an Azure Storage account.</span></span> |
| [<span data-ttu-id="16f25-120">az functionapp create</span><span class="sxs-lookup"><span data-stu-id="16f25-120">az functionapp create</span></span>](https://docs.microsoft.com/cli/azure/functionapp#create) | <span data-ttu-id="16f25-121">建立 Azure 函式。</span><span class="sxs-lookup"><span data-stu-id="16f25-121">Creates an Azure Function.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="16f25-122">後續步驟</span><span class="sxs-lookup"><span data-stu-id="16f25-122">Next steps</span></span>

<span data-ttu-id="16f25-123">如需有關 Azure CLI hello 的詳細資訊，請參閱[Azure CLI 文件](https://docs.microsoft.com/cli/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="16f25-123">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="16f25-124">其他 Azure 函式 CLI 指令碼範例可以在 hello [Azure 函式文件](../functions-cli-samples.md)。</span><span class="sxs-lookup"><span data-stu-id="16f25-124">Additional Azure Functions CLI script samples can be found in hello [Azure Functions documentation](../functions-cli-samples.md).</span></span>
