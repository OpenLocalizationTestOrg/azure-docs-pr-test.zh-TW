---
title: "CLI 指令碼範例-aaaAzure 對應自訂網域 tooa web 應用程式 |Microsoft 文件"
description: "Azure CLI 指令碼範例的對應自訂網域 tooa web 應用程式"
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
ms.openlocfilehash: 49d6be092e438a63c0a43e3207080ca4cd5ff3fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="map-a-custom-domain-tooa-web-app"></a><span data-ttu-id="c7e08-103">對應的自訂網域 tooa web 應用程式</span><span class="sxs-lookup"><span data-stu-id="c7e08-103">Map a custom domain tooa web app</span></span>

<span data-ttu-id="c7e08-104">這個範例指令碼應用程式服務中建立 web 應用程式及其相關的資源，然後對應`www.<yourdomain>`tooit。</span><span class="sxs-lookup"><span data-stu-id="c7e08-104">This sample script creates a web app in App Service with its related resources, and then maps `www.<yourdomain>` tooit.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="c7e08-105">如果您選擇 tooinstall，並在本機上使用 hello CLI，本主題會需要您執行 hello Azure CLI 版本 2.0 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="c7e08-105">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="c7e08-106">執行`az --version`toofind hello 版本。</span><span class="sxs-lookup"><span data-stu-id="c7e08-106">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="c7e08-107">如果您需要 tooinstall 或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="c7e08-107">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="c7e08-108">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="c7e08-108">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/configure-custom-domain/configure-custom-domain.sh?highlight=3 "Map a custom domain tooa web app")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="c7e08-109">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="c7e08-109">Script explanation</span></span>

<span data-ttu-id="c7e08-110">此指令碼會使用下列命令的 hello。</span><span class="sxs-lookup"><span data-stu-id="c7e08-110">This script uses hello following commands.</span></span> <span data-ttu-id="c7e08-111">Hello 資料表連結 toocommand 特定文件中的每個命令。</span><span class="sxs-lookup"><span data-stu-id="c7e08-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="c7e08-112">命令</span><span class="sxs-lookup"><span data-stu-id="c7e08-112">Command</span></span> | <span data-ttu-id="c7e08-113">注意事項</span><span class="sxs-lookup"><span data-stu-id="c7e08-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="c7e08-114">az group create</span><span class="sxs-lookup"><span data-stu-id="c7e08-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="c7e08-115">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="c7e08-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="c7e08-116">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="c7e08-116">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="c7e08-117">建立 App Service 方案。</span><span class="sxs-lookup"><span data-stu-id="c7e08-117">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="c7e08-118">az webapp create</span><span class="sxs-lookup"><span data-stu-id="c7e08-118">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="c7e08-119">建立 Azure Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c7e08-119">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="c7e08-120">az webapp config hostname add</span><span class="sxs-lookup"><span data-stu-id="c7e08-120">az webapp config hostname add</span></span>](https://docs.microsoft.com/cli/azure/webapp/config/hostname#add) | <span data-ttu-id="c7e08-121">將自訂網域 tooa web 應用程式的對應。</span><span class="sxs-lookup"><span data-stu-id="c7e08-121">Maps a custom domain tooa web app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="c7e08-122">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c7e08-122">Next steps</span></span>

<span data-ttu-id="c7e08-123">如需有關 Azure CLI hello 的詳細資訊，請參閱[Azure CLI 文件](https://docs.microsoft.com/cli/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="c7e08-123">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="c7e08-124">其他應用程式服務 CLI 指令碼範例可以在 hello [Azure 應用程式服務文件](../app-service-cli-samples.md)。</span><span class="sxs-lookup"><span data-stu-id="c7e08-124">Additional App Service CLI script samples can be found in hello [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
