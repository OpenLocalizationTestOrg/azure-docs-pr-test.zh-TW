---
title: "Azure CLI 指令碼範例 - 將自訂網域對應至函式應用程式 | Microsoft Docs"
description: "Azure CLI 指令碼範例 - 在 Azure 中將自訂網域對應至函式應用程式。"
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
ms.openlocfilehash: 6fcea6d32f9dd25b0fafb4f895f60d8320ac9df8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="map-a-custom-domain-to-a-function-app"></a><span data-ttu-id="96c23-103">將自訂網域對應至函式應用程式</span><span class="sxs-lookup"><span data-stu-id="96c23-103">Map a custom domain to a function app</span></span>

<span data-ttu-id="96c23-104">此範例指令碼會建立函式應用程式及相關資源，然後將 `www.<yourdomain>` 與其對應。</span><span class="sxs-lookup"><span data-stu-id="96c23-104">This sample script creates a function app with related resources, and then maps `www.<yourdomain>` to it.</span></span> <span data-ttu-id="96c23-105">若要對應至自訂網域，必須在 App Service 方案中建立函式應用程式，而不是在取用方案中建立。</span><span class="sxs-lookup"><span data-stu-id="96c23-105">To map to a custom domain, your function app must be created in an App Service plan and not in a consumption plan.</span></span> <span data-ttu-id="96c23-106">Azure Functions 只支援使用 A 記錄對應自訂網域。</span><span class="sxs-lookup"><span data-stu-id="96c23-106">Azure Functions only supports mapping a custom domain using an A record.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="96c23-107">如果您選擇在本機安裝和使用 CLI，本主題會要求您執行 Azure CLI 2.0 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="96c23-107">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="96c23-108">執行 `az --version` 以尋找版本。</span><span class="sxs-lookup"><span data-stu-id="96c23-108">Run `az --version` to find the version.</span></span> <span data-ttu-id="96c23-109">如果您需要安裝或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="96c23-109">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 


## <a name="sample-script"></a><span data-ttu-id="96c23-110">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="96c23-110">Sample script</span></span>

<span data-ttu-id="96c23-111">[!code-azurecli-interactive[主要](../../../cli_scripts/azure-functions/configure-custom-domain/configure-custom-domain.sh?highlight=3 "將自訂網域對應至函式應用程式")]</span><span class="sxs-lookup"><span data-stu-id="96c23-111">[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/configure-custom-domain/configure-custom-domain.sh?highlight=3 "Map a custom domain to a function app")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="96c23-112">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="96c23-112">Script explanation</span></span>

<span data-ttu-id="96c23-113">此指令碼會使用下列命令。</span><span class="sxs-lookup"><span data-stu-id="96c23-113">This script uses the following commands.</span></span> <span data-ttu-id="96c23-114">下表中的每個命令都會連結至命令特定的文件。</span><span class="sxs-lookup"><span data-stu-id="96c23-114">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="96c23-115">命令</span><span class="sxs-lookup"><span data-stu-id="96c23-115">Command</span></span> | <span data-ttu-id="96c23-116">注意事項</span><span class="sxs-lookup"><span data-stu-id="96c23-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="96c23-117">az group create</span><span class="sxs-lookup"><span data-stu-id="96c23-117">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="96c23-118">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="96c23-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="96c23-119">az storage account create</span><span class="sxs-lookup"><span data-stu-id="96c23-119">az storage account create</span></span>](https://docs.microsoft.com/cli/azure/storage/account#create) | <span data-ttu-id="96c23-120">建立函式應用程式所需的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="96c23-120">Creates a storage account required by the function app.</span></span> |
| [<span data-ttu-id="96c23-121">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="96c23-121">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="96c23-122">建立對應自訂網域所需的 App Service 方案。</span><span class="sxs-lookup"><span data-stu-id="96c23-122">Creates an App Service plan required to map a custom domain.</span></span> |
| [<span data-ttu-id="96c23-123">az functionapp create</span><span class="sxs-lookup"><span data-stu-id="96c23-123">az functionapp create</span></span>]() | <span data-ttu-id="96c23-124">建立函式應用程式。</span><span class="sxs-lookup"><span data-stu-id="96c23-124">Creates a function app.</span></span> |
| [<span data-ttu-id="96c23-125">az appservice web config hostname add</span><span class="sxs-lookup"><span data-stu-id="96c23-125">az appservice web config hostname add</span></span>](https://docs.microsoft.com/cli/azure/appservice/web/config/hostname#add) | <span data-ttu-id="96c23-126">將自訂網域對應至函式應用程式。</span><span class="sxs-lookup"><span data-stu-id="96c23-126">Maps a custom domain to a function app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="96c23-127">後續步驟</span><span class="sxs-lookup"><span data-stu-id="96c23-127">Next steps</span></span>

<span data-ttu-id="96c23-128">如需 Azure CLI 的詳細資訊，請參閱 [Azure CLI 文件](https://docs.microsoft.com/cli/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="96c23-128">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="96c23-129">您可以在 [Azure Functions 文件]()中找到其他 Functions CLI 指令碼範例。</span><span class="sxs-lookup"><span data-stu-id="96c23-129">Additional Functions CLI script samples can be found in the [Azure Functions documentation]().</span></span>
