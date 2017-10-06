---
title: "aaaAzure CLI 指令碼範例-調整 web 應用程式與高可用性架構全球 |Microsoft 文件"
description: "Azure CLI 指令碼範例 - 透過高可用性架構將 Web 應用程式調整為全球可用"
services: appservice
documentationcenter: appservice
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: e4033a50-0e05-4505-8ce8-c876204b2acc
ms.service: app-service
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 06/19/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: b72fbccd7f2aaab58e4b4721e14dca14146c7c72
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="scale-a-web-app-worldwide-with-a-high-availability-architecture"></a><span data-ttu-id="b4c02-103">透過高可用性架構將 Web 應用程式調整為全球可用</span><span class="sxs-lookup"><span data-stu-id="b4c02-103">Scale a web app worldwide with a high-availability architecture</span></span>

<span data-ttu-id="b4c02-104">在此案例中，您會建立一個資源群組、兩個 App Service 方案、兩個 Web 應用程式、一個流量管理員設定檔和兩個流量管理員端點。</span><span class="sxs-lookup"><span data-stu-id="b4c02-104">In this scenario you will create a resource group, two app service plans, two web apps, a traffic manager profile, and two traffic manager endpoints.</span></span> <span data-ttu-id="b4c02-105">一旦完成 hello 練習會有高可用性的架構可讓提供全域 hello 最低的網路延遲為基礎的 web 應用程式的可用性。</span><span class="sxs-lookup"><span data-stu-id="b4c02-105">Once hello exercise is complete you will have a high-available architecture which allows provides global availability of your web app based on hello lowest network latency.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="b4c02-106">如果您選擇 tooinstall，並在本機上使用 hello CLI，本主題會需要您執行 hello Azure CLI 版本 2.0 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="b4c02-106">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="b4c02-107">執行`az --version`toofind hello 版本。</span><span class="sxs-lookup"><span data-stu-id="b4c02-107">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="b4c02-108">如果您需要 tooinstall 或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="b4c02-108">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 


## <a name="sample-script"></a><span data-ttu-id="b4c02-109">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="b4c02-109">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/scale-geographic/scale-geographic.sh "Geographic Scale")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="b4c02-110">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="b4c02-110">Script explanation</span></span>

<span data-ttu-id="b4c02-111">此指令碼會使用下列命令 toocreate 資源群組、 web 應用程式、 流量管理員設定檔，hello 和所有相關聯的資源。</span><span class="sxs-lookup"><span data-stu-id="b4c02-111">This script uses hello following commands toocreate a resource group, web app, traffic manager profile, and all related resources.</span></span> <span data-ttu-id="b4c02-112">Hello 資料表連結 toocommand 特定文件中的每個命令。</span><span class="sxs-lookup"><span data-stu-id="b4c02-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="b4c02-113">命令</span><span class="sxs-lookup"><span data-stu-id="b4c02-113">Command</span></span> | <span data-ttu-id="b4c02-114">注意事項</span><span class="sxs-lookup"><span data-stu-id="b4c02-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="b4c02-115">az group create</span><span class="sxs-lookup"><span data-stu-id="b4c02-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="b4c02-116">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="b4c02-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="b4c02-117">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="b4c02-117">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="b4c02-118">建立 App Service 方案。</span><span class="sxs-lookup"><span data-stu-id="b4c02-118">Creates an App Service plan.</span></span> <span data-ttu-id="b4c02-119">這就像是 Azure Web 應用程式的伺服器陣列。</span><span class="sxs-lookup"><span data-stu-id="b4c02-119">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="b4c02-120">az webapp create</span><span class="sxs-lookup"><span data-stu-id="b4c02-120">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="b4c02-121">建立 Azure Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="b4c02-121">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="b4c02-122">az network traffic-manager profile create</span><span class="sxs-lookup"><span data-stu-id="b4c02-122">az network traffic-manager profile create</span></span>](https://docs.microsoft.com/cli/azure/network/traffic-manager/profile#create) | <span data-ttu-id="b4c02-123">建立 Azure 流量管理員設定檔。</span><span class="sxs-lookup"><span data-stu-id="b4c02-123">Creates an Azure Traffic Manager profile.</span></span> |
| [<span data-ttu-id="b4c02-124">az network traffic-manager endpoint create</span><span class="sxs-lookup"><span data-stu-id="b4c02-124">az network traffic-manager endpoint create</span></span>](https://docs.microsoft.com/cli/azure/network/traffic-manager/endpoint#create) | <span data-ttu-id="b4c02-125">加入端點 tooan Azure 流量管理員設定檔。</span><span class="sxs-lookup"><span data-stu-id="b4c02-125">Adds a endpoint tooan Azure Traffic Manager Profile.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="b4c02-126">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b4c02-126">Next steps</span></span>

<span data-ttu-id="b4c02-127">如需有關 Azure CLI hello 的詳細資訊，請參閱[Azure CLI 文件](https://docs.microsoft.com/cli/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="b4c02-127">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="b4c02-128">其他應用程式服務 CLI 指令碼範例可以在 hello [Azure 應用程式服務文件](../app-service-cli-samples.md)。</span><span class="sxs-lookup"><span data-stu-id="b4c02-128">Additional App Service CLI script samples can be found in hello [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
