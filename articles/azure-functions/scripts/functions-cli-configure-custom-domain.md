---
title: "aaaAzure CLI 指令碼範例-將對應的自訂網域 tooa 函式應用程式 |Microsoft 文件"
description: "Azure CLI 指令碼範例-在 Azure 中的自訂網域 tooa 函式應用程式的對應。"
services: functions
documentationcenter: 
author: ggailey777
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: d127e347-7581-47d7-b289-e0f51f2fbfbc
ms.service: functions
ms.workload: na
ms.devlang: azurecli
ms.tgt_pltfrm: na
ms.topic: sample
ms.date: 06/01/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: c7cb0a3e132b491250623b945aecf6aea4f57c4b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="map-a-custom-domain-tooa-function-app"></a><span data-ttu-id="9174d-103">對應的自訂網域 tooa 函式應用程式</span><span class="sxs-lookup"><span data-stu-id="9174d-103">Map a custom domain tooa function app</span></span>

<span data-ttu-id="9174d-104">這個範例指令碼相關的資源，建立函數應用程式，然後對應`www.<yourdomain>`tooit。</span><span class="sxs-lookup"><span data-stu-id="9174d-104">This sample script creates a function app with related resources, and then maps `www.<yourdomain>` tooit.</span></span> <span data-ttu-id="9174d-105">toomap tooa 自訂網域，必須建立函式應用程式，App Service 方案中，而不是在耗用量計劃。</span><span class="sxs-lookup"><span data-stu-id="9174d-105">toomap tooa custom domain, your function app must be created in an App Service plan and not in a consumption plan.</span></span> <span data-ttu-id="9174d-106">Azure Functions 只支援使用 A 記錄對應自訂網域。</span><span class="sxs-lookup"><span data-stu-id="9174d-106">Azure Functions only supports mapping a custom domain using an A record.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="9174d-107">如果您選擇 tooinstall，並在本機上使用 hello CLI，本主題會需要您執行 hello Azure CLI 版本 2.0 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="9174d-107">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="9174d-108">執行`az --version`toofind hello 版本。</span><span class="sxs-lookup"><span data-stu-id="9174d-108">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="9174d-109">如果您需要 tooinstall 或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="9174d-109">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 


## <a name="sample-script"></a><span data-ttu-id="9174d-110">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="9174d-110">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/configure-custom-domain/configure-custom-domain.sh?highlight=3 "Map a custom domain tooa function app")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="9174d-111">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="9174d-111">Script explanation</span></span>

<span data-ttu-id="9174d-112">此指令碼會使用下列命令的 hello。</span><span class="sxs-lookup"><span data-stu-id="9174d-112">This script uses hello following commands.</span></span> <span data-ttu-id="9174d-113">Hello 資料表連結 toocommand 特定文件中的每個命令。</span><span class="sxs-lookup"><span data-stu-id="9174d-113">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="9174d-114">命令</span><span class="sxs-lookup"><span data-stu-id="9174d-114">Command</span></span> | <span data-ttu-id="9174d-115">注意事項</span><span class="sxs-lookup"><span data-stu-id="9174d-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="9174d-116">az group create</span><span class="sxs-lookup"><span data-stu-id="9174d-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="9174d-117">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="9174d-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="9174d-118">az storage account create</span><span class="sxs-lookup"><span data-stu-id="9174d-118">az storage account create</span></span>](https://docs.microsoft.com/cli/azure/storage/account#create) | <span data-ttu-id="9174d-119">建立 hello 函式應用程式所需的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="9174d-119">Creates a storage account required by hello function app.</span></span> |
| [<span data-ttu-id="9174d-120">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="9174d-120">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="9174d-121">建立應用程式服務計劃所需 toomap 自訂網域。</span><span class="sxs-lookup"><span data-stu-id="9174d-121">Creates an App Service plan required toomap a custom domain.</span></span> |
| [<span data-ttu-id="9174d-122">az functionapp create</span><span class="sxs-lookup"><span data-stu-id="9174d-122">az functionapp create</span></span>]() | <span data-ttu-id="9174d-123">建立函式應用程式。</span><span class="sxs-lookup"><span data-stu-id="9174d-123">Creates a function app.</span></span> |
| [<span data-ttu-id="9174d-124">az appservice web config hostname add</span><span class="sxs-lookup"><span data-stu-id="9174d-124">az appservice web config hostname add</span></span>](https://docs.microsoft.com/cli/azure/appservice/web/config/hostname#add) | <span data-ttu-id="9174d-125">將對應的自訂網域 tooa 函式應用程式。</span><span class="sxs-lookup"><span data-stu-id="9174d-125">Maps a custom domain tooa function app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="9174d-126">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9174d-126">Next steps</span></span>

<span data-ttu-id="9174d-127">如需有關 Azure CLI hello 的詳細資訊，請參閱[Azure CLI 文件](https://docs.microsoft.com/cli/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="9174d-127">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="9174d-128">其他函式 CLI 指令碼範例可以在 hello [Azure 函式文件]()。</span><span class="sxs-lookup"><span data-stu-id="9174d-128">Additional Functions CLI script samples can be found in hello [Azure Functions documentation]().</span></span>
