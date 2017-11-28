---
title: "CLI 指令碼範例應用程式的高可用性的路由傳送流量 aaaAzure |Microsoft 文件"
description: "Azure CLI 指令碼範例：路由傳送流量以達到應用程式的高可用性"
services: traffic-manager
documentationcenter: traffic-manager
author: KumudD
manager: timlt
editor: tysonn
tags: azure-infrastructure
ms.assetid: 
ms.service: traffic-manager
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: traffic-manager
ms.date: 07/07/2017
ms.author: kumud
ms.openlocfilehash: 2142c8bbec1dffc2f12b5500df142a429393a145
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="route-traffic-for-high-availability-of-applications"></a><span data-ttu-id="fef53-103">路由傳送流量以達到應用程式的高可用性</span><span class="sxs-lookup"><span data-stu-id="fef53-103">Route traffic for high availability of applications</span></span>

<span data-ttu-id="fef53-104">這個指令碼會建立一個資源群組、兩個 App Service 方案、兩個 Web 應用程式、一個流量管理員設定檔和兩個流量管理員端點。</span><span class="sxs-lookup"><span data-stu-id="fef53-104">This script creates a resource group, two app service plans, two web apps, a traffic manager profile, and two traffic manager endpoints.</span></span> <span data-ttu-id="fef53-105">Hello hello 主要區域中的應用程式無法使用時，traffic Manager 將導向流量 toohello 應用程式與 hello 主要區域中，一個區域及 toohello 次要區域。</span><span class="sxs-lookup"><span data-stu-id="fef53-105">Traffic Manager directs traffic toohello application in one region as hello primary region, and toohello secondary region when hello application in hello primary region is unavailable.</span></span> <span data-ttu-id="fef53-106">在執行之前 hello 指令碼，您必須變更 hello MyWebApp，MyWebAppL1 和 MyWebAppL2 值 toounique 值在整個 Azure。</span><span class="sxs-lookup"><span data-stu-id="fef53-106">Before executing hello script, you must change hello MyWebApp, MyWebAppL1 and MyWebAppL2 values toounique values across Azure.</span></span> <span data-ttu-id="fef53-107">執行 hello 指令碼之後, 您可以存取與 hello URL mywebapp.trafficmanager.net hello 主要區域中的 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="fef53-107">After running hello script, you can access hello app in hello primary region with hello URL mywebapp.trafficmanager.net.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="fef53-108">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="fef53-108">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/traffic-manager/direct-traffic-for-increased-application-availability/direct-traffic-for-increased-application-availability.sh "Route traffic for high availability")]


## <a name="clean-up-deployment"></a><span data-ttu-id="fef53-109">清除部署</span><span class="sxs-lookup"><span data-stu-id="fef53-109">Clean up deployment</span></span> 

<span data-ttu-id="fef53-110">Hello 指令碼範例執行後，hello 後續命令可以使用的 tooremove hello 資源群組，App Service 應用程式，而且所有相關的資源。</span><span class="sxs-lookup"><span data-stu-id="fef53-110">After hello script sample has been run, hello follow command can be used tooremove hello resource group, App Service app, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup1 --yes
az group delete --name myResourceGroup2 --yes
```

## <a name="script-explanation"></a><span data-ttu-id="fef53-111">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="fef53-111">Script explanation</span></span>

<span data-ttu-id="fef53-112">此指令碼會使用下列命令 toocreate 資源群組、 web 應用程式、 流量管理員設定檔，hello 和所有相關聯的資源。</span><span class="sxs-lookup"><span data-stu-id="fef53-112">This script uses hello following commands toocreate a resource group, web app, traffic manager profile, and all related resources.</span></span> <span data-ttu-id="fef53-113">Hello 資料表連結 toocommand 特定文件中的每個命令。</span><span class="sxs-lookup"><span data-stu-id="fef53-113">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="fef53-114">命令</span><span class="sxs-lookup"><span data-stu-id="fef53-114">Command</span></span> | <span data-ttu-id="fef53-115">注意事項</span><span class="sxs-lookup"><span data-stu-id="fef53-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="fef53-116">az group create</span><span class="sxs-lookup"><span data-stu-id="fef53-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="fef53-117">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="fef53-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="fef53-118">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="fef53-118">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="fef53-119">建立 App Service 方案。</span><span class="sxs-lookup"><span data-stu-id="fef53-119">Creates an App Service plan.</span></span> <span data-ttu-id="fef53-120">這就像是 Azure Web 應用程式的伺服器陣列。</span><span class="sxs-lookup"><span data-stu-id="fef53-120">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="fef53-121">az appservice web create</span><span class="sxs-lookup"><span data-stu-id="fef53-121">az appservice web create</span></span>](https://docs.microsoft.com/cli/azure/appservice/web#create) | <span data-ttu-id="fef53-122">建立 Azure web 應用程式內 hello 應用程式服務方案。</span><span class="sxs-lookup"><span data-stu-id="fef53-122">Creates an Azure web app within hello App Service plan.</span></span> |
| [<span data-ttu-id="fef53-123">az network traffic-manager profile create</span><span class="sxs-lookup"><span data-stu-id="fef53-123">az network traffic-manager profile create</span></span>](https://docs.microsoft.com/cli/azure/network/traffic-manager/profile#create) | <span data-ttu-id="fef53-124">建立 Azure 流量管理員設定檔。</span><span class="sxs-lookup"><span data-stu-id="fef53-124">Creates an Azure Traffic Manager profile.</span></span> |
| [<span data-ttu-id="fef53-125">az network traffic-manager endpoint create</span><span class="sxs-lookup"><span data-stu-id="fef53-125">az network traffic-manager endpoint create</span></span>](https://docs.microsoft.com/cli/azure/network/traffic-manager/endpoint#create) | <span data-ttu-id="fef53-126">加入端點 tooan Azure 流量管理員設定檔。</span><span class="sxs-lookup"><span data-stu-id="fef53-126">Adds a endpoint tooan Azure Traffic Manager Profile.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="fef53-127">後續步驟</span><span class="sxs-lookup"><span data-stu-id="fef53-127">Next steps</span></span>

<span data-ttu-id="fef53-128">如需有關 Azure CLI hello 的詳細資訊，請參閱[Azure CLI 文件](https://docs.microsoft.com/cli/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="fef53-128">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="fef53-129">其他應用程式服務 CLI 指令碼範例可以在 hello [Azure 網路文件](../cli-samples.md)。</span><span class="sxs-lookup"><span data-stu-id="fef53-129">Additional App Service CLI script samples can be found in hello [Azure Networking documentation](../cli-samples.md).</span></span>
