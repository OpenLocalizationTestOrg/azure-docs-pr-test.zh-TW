---
title: "Azure CLI 指令碼範例 - 透過高可用性架構將 Web 應用程式調整為全球可用 | Microsoft Docs"
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
ms.openlocfilehash: c368bdc48f197ff5b491d1796d85abfd339051a6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="scale-a-web-app-worldwide-with-a-high-availability-architecture"></a><span data-ttu-id="f3464-103">透過高可用性架構將 Web 應用程式調整為全球可用</span><span class="sxs-lookup"><span data-stu-id="f3464-103">Scale a web app worldwide with a high-availability architecture</span></span>

<span data-ttu-id="f3464-104">在此案例中，您會建立一個資源群組、兩個 App Service 方案、兩個 Web 應用程式、一個流量管理員設定檔和兩個流量管理員端點。</span><span class="sxs-lookup"><span data-stu-id="f3464-104">In this scenario you will create a resource group, two app service plans, two web apps, a traffic manager profile, and two traffic manager endpoints.</span></span> <span data-ttu-id="f3464-105">完成此練習後，您就會擁有高可用性架構，可根據最低網路延遲來全球提供 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="f3464-105">Once the exercise is complete you will have a high-available architecture which allows provides global availability of your web app based on the lowest network latency.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="f3464-106">如果您選擇在本機安裝和使用 CLI，本主題會要求您執行 Azure CLI 2.0 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="f3464-106">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="f3464-107">執行 `az --version` 以尋找版本。</span><span class="sxs-lookup"><span data-stu-id="f3464-107">Run `az --version` to find the version.</span></span> <span data-ttu-id="f3464-108">如果您需要安裝或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="f3464-108">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 


## <a name="sample-script"></a><span data-ttu-id="f3464-109">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="f3464-109">Sample script</span></span>

<span data-ttu-id="f3464-110">[!code-azurecli-interactive[主要](../../../cli_scripts/app-service/scale-geographic/scale-geographic.sh "地理調整")]</span><span class="sxs-lookup"><span data-stu-id="f3464-110">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/scale-geographic/scale-geographic.sh "Geographic Scale")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="f3464-111">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="f3464-111">Script explanation</span></span>

<span data-ttu-id="f3464-112">此指令碼使用下列命令來建立資源群組、Web 應用程式、流量管理員設定檔和所有相關資源。</span><span class="sxs-lookup"><span data-stu-id="f3464-112">This script uses the following commands to create a resource group, web app, traffic manager profile, and all related resources.</span></span> <span data-ttu-id="f3464-113">下表中的每個命令都會連結至命令特定的文件。</span><span class="sxs-lookup"><span data-stu-id="f3464-113">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="f3464-114">命令</span><span class="sxs-lookup"><span data-stu-id="f3464-114">Command</span></span> | <span data-ttu-id="f3464-115">注意事項</span><span class="sxs-lookup"><span data-stu-id="f3464-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="f3464-116">az group create</span><span class="sxs-lookup"><span data-stu-id="f3464-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="f3464-117">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="f3464-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="f3464-118">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="f3464-118">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="f3464-119">建立 App Service 方案。</span><span class="sxs-lookup"><span data-stu-id="f3464-119">Creates an App Service plan.</span></span> <span data-ttu-id="f3464-120">這就像是 Azure Web 應用程式的伺服器陣列。</span><span class="sxs-lookup"><span data-stu-id="f3464-120">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="f3464-121">az webapp create</span><span class="sxs-lookup"><span data-stu-id="f3464-121">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="f3464-122">建立 Azure Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="f3464-122">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="f3464-123">az network traffic-manager profile create</span><span class="sxs-lookup"><span data-stu-id="f3464-123">az network traffic-manager profile create</span></span>](https://docs.microsoft.com/cli/azure/network/traffic-manager/profile#create) | <span data-ttu-id="f3464-124">建立 Azure 流量管理員設定檔。</span><span class="sxs-lookup"><span data-stu-id="f3464-124">Creates an Azure Traffic Manager profile.</span></span> |
| [<span data-ttu-id="f3464-125">az network traffic-manager endpoint create</span><span class="sxs-lookup"><span data-stu-id="f3464-125">az network traffic-manager endpoint create</span></span>](https://docs.microsoft.com/cli/azure/network/traffic-manager/endpoint#create) | <span data-ttu-id="f3464-126">新增端點至 Azure 流量管理員設定檔。</span><span class="sxs-lookup"><span data-stu-id="f3464-126">Adds a endpoint to an Azure Traffic Manager Profile.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="f3464-127">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f3464-127">Next steps</span></span>

<span data-ttu-id="f3464-128">如需 Azure CLI 的詳細資訊，請參閱 [Azure CLI 文件](https://docs.microsoft.com/cli/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="f3464-128">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="f3464-129">您可以在 [Azure App Service 文件](../app-service-cli-samples.md)中找到其他的 App Service CLI 指令碼範例。</span><span class="sxs-lookup"><span data-stu-id="f3464-129">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
