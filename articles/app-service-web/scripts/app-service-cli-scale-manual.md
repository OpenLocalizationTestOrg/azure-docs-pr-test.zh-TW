---
title: "Azure CLI 指令碼範例 - 使用 Azure CLI 2.0 手動調整 Web 應用程式 | Microsoft Docs"
description: "Azure CLI 指令碼範例 - 使用 Azure CLI 2.0 手動調整 Web 應用程式"
services: appservice
documentationcenter: appservice
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 251d9074-8fff-4121-ad16-9eca9556ac96
ms.service: app-service
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 06/19/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: fe05661eb4e2d5c37aebdbfde002b34588db69e7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="scale-a-web-app-manually"></a><span data-ttu-id="b463b-103">手動調整 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="b463b-103">Scale a web app manually</span></span>

<span data-ttu-id="b463b-104">在此案例中，您會學習如何建立資源群組、App Service 方案和 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="b463b-104">In this scenario you will learn to create a resource group, app service plan and web app.</span></span> <span data-ttu-id="b463b-105">然後，您會將 App Service 方案從單一執行個體調整為多個執行個體。</span><span class="sxs-lookup"><span data-stu-id="b463b-105">You will then scale the App Service Plan from a single instance to multiple instances.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="b463b-106">如果您選擇在本機安裝和使用 CLI，本主題會要求您執行 Azure CLI 2.0 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="b463b-106">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="b463b-107">執行 `az --version` 以尋找版本。</span><span class="sxs-lookup"><span data-stu-id="b463b-107">Run `az --version` to find the version.</span></span> <span data-ttu-id="b463b-108">如果您需要安裝或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="b463b-108">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="b463b-109">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="b463b-109">Sample script</span></span>

<span data-ttu-id="b463b-110">[!code-azurecli-interactive[主要](../../../cli_scripts/app-service/scale-manual/scale-manual.sh "手動調整")]</span><span class="sxs-lookup"><span data-stu-id="b463b-110">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/scale-manual/scale-manual.sh "Manual Scale")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="b463b-111">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="b463b-111">Script explanation</span></span>

<span data-ttu-id="b463b-112">此指令碼使用下列命令來建立資源群組、Web 應用程式和所有相關資源。</span><span class="sxs-lookup"><span data-stu-id="b463b-112">This script uses the following commands to create a resource group, web app, and all related resources.</span></span> <span data-ttu-id="b463b-113">下表中的每個命令都會連結至命令特定的文件。</span><span class="sxs-lookup"><span data-stu-id="b463b-113">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="b463b-114">命令</span><span class="sxs-lookup"><span data-stu-id="b463b-114">Command</span></span> | <span data-ttu-id="b463b-115">注意事項</span><span class="sxs-lookup"><span data-stu-id="b463b-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="b463b-116">az group create</span><span class="sxs-lookup"><span data-stu-id="b463b-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="b463b-117">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="b463b-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="b463b-118">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="b463b-118">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="b463b-119">建立 App Service 方案。</span><span class="sxs-lookup"><span data-stu-id="b463b-119">Creates an App Service plan.</span></span> <span data-ttu-id="b463b-120">這就像是 Azure Web 應用程式的伺服器陣列。</span><span class="sxs-lookup"><span data-stu-id="b463b-120">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="b463b-121">az webapp create</span><span class="sxs-lookup"><span data-stu-id="b463b-121">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="b463b-122">建立 Azure Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="b463b-122">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="b463b-123">az appservice plan update</span><span class="sxs-lookup"><span data-stu-id="b463b-123">az appservice plan update</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#update) | <span data-ttu-id="b463b-124">更新 App Service 方案的屬性。</span><span class="sxs-lookup"><span data-stu-id="b463b-124">Updates properties of the App Service plan.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="b463b-125">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b463b-125">Next steps</span></span>

<span data-ttu-id="b463b-126">如需 Azure CLI 的詳細資訊，請參閱 [Azure CLI 文件](https://docs.microsoft.com/cli/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="b463b-126">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="b463b-127">您可以在 [Azure App Service 文件](../app-service-cli-samples.md)中找到其他的 App Service CLI 指令碼範例。</span><span class="sxs-lookup"><span data-stu-id="b463b-127">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
