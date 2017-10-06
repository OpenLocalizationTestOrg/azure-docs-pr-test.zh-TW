---
title: "aaaAzure CLI 指令碼範例-在 Docker 容器中建立 ASP.NET Core web 應用程式 |Microsoft 文件"
description: "Azure CLI 指令碼範例 - 在 Docker 容器中建立 ASP.NET Core Web 應用程式"
services: appservice
documentationcenter: appservice
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 3a2d1983-ff7b-476a-ac44-49ec2aabb31a
ms.service: app-service
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 06/19/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 23106345bfbbf1f68757d99010db98e7c9a7da49
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-aspnet-core-web-app-in-a-docker-container"></a><span data-ttu-id="ba628-103">在 Docker 容器中建立 ASP.NET Core Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="ba628-103">Create an ASP.NET Core web app in a Docker container</span></span>

<span data-ttu-id="ba628-104">在此案例中，您將學習如何 toocreate 資源群組、 Linux 應用程式服務計劃，以及 web 應用程式和部署使用 Docker 容器的 ASP.NET Core 應用程式。</span><span class="sxs-lookup"><span data-stu-id="ba628-104">In this scenario you will learn how toocreate a resource group, Linux app service plan, and web app, and deploy an ASP.NET Core application using a Docker Container.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="ba628-105">如果您選擇 tooinstall，並在本機上使用 hello CLI，本主題會需要您執行 hello Azure CLI 版本 2.0 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="ba628-105">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="ba628-106">執行`az --version`toofind hello 版本。</span><span class="sxs-lookup"><span data-stu-id="ba628-106">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="ba628-107">如果您需要 tooinstall 或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="ba628-107">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 


## <a name="sample-script"></a><span data-ttu-id="ba628-108">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="ba628-108">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/deploy-linux-docker/deploy-linux-docker.sh?highlight=6 "Linux Docker")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="ba628-109">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="ba628-109">Script explanation</span></span>

<span data-ttu-id="ba628-110">此指令碼會使用下列命令 toocreate 資源群組、 web 應用程式和所有相關的資源的 hello。</span><span class="sxs-lookup"><span data-stu-id="ba628-110">This script uses hello following commands toocreate a resource group, web app, and all related resources.</span></span> <span data-ttu-id="ba628-111">Hello 資料表連結 toocommand 特定文件中的每個命令。</span><span class="sxs-lookup"><span data-stu-id="ba628-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="ba628-112">命令</span><span class="sxs-lookup"><span data-stu-id="ba628-112">Command</span></span> | <span data-ttu-id="ba628-113">注意事項</span><span class="sxs-lookup"><span data-stu-id="ba628-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="ba628-114">az group create</span><span class="sxs-lookup"><span data-stu-id="ba628-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="ba628-115">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="ba628-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="ba628-116">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="ba628-116">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="ba628-117">建立 App Service 方案。</span><span class="sxs-lookup"><span data-stu-id="ba628-117">Creates an App Service plan.</span></span> <span data-ttu-id="ba628-118">這就像是 Azure Web 應用程式的伺服器陣列。</span><span class="sxs-lookup"><span data-stu-id="ba628-118">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="ba628-119">az webapp create</span><span class="sxs-lookup"><span data-stu-id="ba628-119">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="ba628-120">建立 Azure Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="ba628-120">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="ba628-121">az webapp config container set</span><span class="sxs-lookup"><span data-stu-id="ba628-121">az webapp config container set</span></span>](https://docs.microsoft.com/cli/azure/webapp/config/container#set) | <span data-ttu-id="ba628-122">設定 hello Azure web 應用程式的 hello Docker 容器。</span><span class="sxs-lookup"><span data-stu-id="ba628-122">Sets hello Docker container for hello Azure web app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="ba628-123">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ba628-123">Next steps</span></span>

<span data-ttu-id="ba628-124">如需有關 Azure CLI hello 的詳細資訊，請參閱[Azure CLI 文件](https://docs.microsoft.com/cli/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="ba628-124">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="ba628-125">其他應用程式服務 CLI 指令碼範例可以在 hello [Azure 應用程式服務文件](../app-service-cli-samples.md)。</span><span class="sxs-lookup"><span data-stu-id="ba628-125">Additional App Service CLI script samples can be found in hello [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
