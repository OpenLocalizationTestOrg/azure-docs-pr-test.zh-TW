---
title: "Azure CLI 指令碼範例 - 將自訂網域對應至 Web 應用程式 | Microsoft Docs"
description: "Azure CLI 指令碼範例 - 將自訂網域對應至 Web 應用程式"
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 5ac4a680-cc73-4578-bcd6-8668c08802c2
ms.service: app-service-web
ms.workload: web
ms.devlang: azurecli
ms.tgt_pltfrm: na
ms.topic: sample
ms.date: 06/19/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 6712be8a551731fbafd92ef19564e89399e23e76
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="map-a-custom-domain-to-a-web-app"></a><span data-ttu-id="eecf3-103">將自訂網域對應至 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="eecf3-103">Map a custom domain to a web app</span></span>

<span data-ttu-id="eecf3-104">此範例指令碼會在 App Service 中建立 Web 應用程式及其相關資源，然後將 `www.<yourdomain>` 與其對應。</span><span class="sxs-lookup"><span data-stu-id="eecf3-104">This sample script creates a web app in App Service with its related resources, and then maps `www.<yourdomain>` to it.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="eecf3-105">如果您選擇在本機安裝和使用 CLI，本主題會要求您執行 Azure CLI 2.0 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="eecf3-105">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="eecf3-106">執行 `az --version` 以尋找版本。</span><span class="sxs-lookup"><span data-stu-id="eecf3-106">Run `az --version` to find the version.</span></span> <span data-ttu-id="eecf3-107">如果您需要安裝或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="eecf3-107">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="eecf3-108">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="eecf3-108">Sample script</span></span>

<span data-ttu-id="eecf3-109">[!code-azurecli-interactive[主要](../../../cli_scripts/app-service/configure-custom-domain/configure-custom-domain.sh?highlight=3 "將自訂網域對應至 Web 應用程式")]</span><span class="sxs-lookup"><span data-stu-id="eecf3-109">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/configure-custom-domain/configure-custom-domain.sh?highlight=3 "Map a custom domain to a web app")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="eecf3-110">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="eecf3-110">Script explanation</span></span>

<span data-ttu-id="eecf3-111">此指令碼會使用下列命令。</span><span class="sxs-lookup"><span data-stu-id="eecf3-111">This script uses the following commands.</span></span> <span data-ttu-id="eecf3-112">下表中的每個命令都會連結至命令特定的文件。</span><span class="sxs-lookup"><span data-stu-id="eecf3-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="eecf3-113">命令</span><span class="sxs-lookup"><span data-stu-id="eecf3-113">Command</span></span> | <span data-ttu-id="eecf3-114">注意事項</span><span class="sxs-lookup"><span data-stu-id="eecf3-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="eecf3-115">az group create</span><span class="sxs-lookup"><span data-stu-id="eecf3-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="eecf3-116">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="eecf3-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="eecf3-117">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="eecf3-117">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="eecf3-118">建立 App Service 方案。</span><span class="sxs-lookup"><span data-stu-id="eecf3-118">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="eecf3-119">az webapp create</span><span class="sxs-lookup"><span data-stu-id="eecf3-119">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="eecf3-120">建立 Azure Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="eecf3-120">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="eecf3-121">az webapp config hostname add</span><span class="sxs-lookup"><span data-stu-id="eecf3-121">az webapp config hostname add</span></span>](https://docs.microsoft.com/cli/azure/webapp/config/hostname#add) | <span data-ttu-id="eecf3-122">將自訂網域對應至 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="eecf3-122">Maps a custom domain to a web app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="eecf3-123">後續步驟</span><span class="sxs-lookup"><span data-stu-id="eecf3-123">Next steps</span></span>

<span data-ttu-id="eecf3-124">如需 Azure CLI 的詳細資訊，請參閱 [Azure CLI 文件](https://docs.microsoft.com/cli/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="eecf3-124">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="eecf3-125">您可以在 [Azure App Service 文件](../app-service-cli-samples.md)中找到其他的 App Service CLI 指令碼範例。</span><span class="sxs-lookup"><span data-stu-id="eecf3-125">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
