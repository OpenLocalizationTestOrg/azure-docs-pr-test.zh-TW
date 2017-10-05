---
title: "Azure CLI 指令碼範例：路由傳送流量以達到應用程式的高可用性 | Microsoft Docs"
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
ms.openlocfilehash: 0593d063a4935d02aae124d83b62b11e37aa3c33
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="route-traffic-for-high-availability-of-applications"></a><span data-ttu-id="63e28-103">路由傳送流量以達到應用程式的高可用性</span><span class="sxs-lookup"><span data-stu-id="63e28-103">Route traffic for high availability of applications</span></span>

<span data-ttu-id="63e28-104">這個指令碼會建立一個資源群組、兩個 App Service 方案、兩個 Web 應用程式、一個流量管理員設定檔和兩個流量管理員端點。</span><span class="sxs-lookup"><span data-stu-id="63e28-104">This script creates a resource group, two app service plans, two web apps, a traffic manager profile, and two traffic manager endpoints.</span></span> <span data-ttu-id="63e28-105">流量管理員會將流量導向主要區域中的應用程式，然後當主要區域中的應用程式無法使用時，將流量導向至次要區域。</span><span class="sxs-lookup"><span data-stu-id="63e28-105">Traffic Manager directs traffic to the application in one region as the primary region, and to the secondary region when the application in the primary region is unavailable.</span></span> <span data-ttu-id="63e28-106">在執行指令碼之前，您必須將 MyWebApp、MyWebAppL1 和 MyWebAppL2 值都變更為整個 Azure 中的唯一值。</span><span class="sxs-lookup"><span data-stu-id="63e28-106">Before executing the script, you must change the MyWebApp, MyWebAppL1 and MyWebAppL2 values to unique values across Azure.</span></span> <span data-ttu-id="63e28-107">在執行指令碼之後，您可以透過 URL mywebapp.trafficmanager.net 來存取主要區域中的應用程式。</span><span class="sxs-lookup"><span data-stu-id="63e28-107">After running the script, you can access the app in the primary region with the URL mywebapp.trafficmanager.net.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="63e28-108">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="63e28-108">Sample script</span></span>

<span data-ttu-id="63e28-109">[!code-azurecli-interactive[主要](../../../cli_scripts/traffic-manager/direct-traffic-for-increased-application-availability/direct-traffic-for-increased-application-availability.sh "路由傳送流量以達到高可用性")]</span><span class="sxs-lookup"><span data-stu-id="63e28-109">[!code-azurecli-interactive[main](../../../cli_scripts/traffic-manager/direct-traffic-for-increased-application-availability/direct-traffic-for-increased-application-availability.sh "Route traffic for high availability")]</span></span>


## <a name="clean-up-deployment"></a><span data-ttu-id="63e28-110">清除部署</span><span class="sxs-lookup"><span data-stu-id="63e28-110">Clean up deployment</span></span> 

<span data-ttu-id="63e28-111">在執行過指令碼範例之後，您可以使用下列命令來移除資源群組、App Service 應用程式和所有相關資源。</span><span class="sxs-lookup"><span data-stu-id="63e28-111">After the script sample has been run, the follow command can be used to remove the resource group, App Service app, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup1 --yes
az group delete --name myResourceGroup2 --yes
```

## <a name="script-explanation"></a><span data-ttu-id="63e28-112">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="63e28-112">Script explanation</span></span>

<span data-ttu-id="63e28-113">此指令碼使用下列命令來建立資源群組、Web 應用程式、流量管理員設定檔和所有相關資源。</span><span class="sxs-lookup"><span data-stu-id="63e28-113">This script uses the following commands to create a resource group, web app, traffic manager profile, and all related resources.</span></span> <span data-ttu-id="63e28-114">下表中的每個命令都會連結至命令特定的文件。</span><span class="sxs-lookup"><span data-stu-id="63e28-114">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="63e28-115">命令</span><span class="sxs-lookup"><span data-stu-id="63e28-115">Command</span></span> | <span data-ttu-id="63e28-116">注意事項</span><span class="sxs-lookup"><span data-stu-id="63e28-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="63e28-117">az group create</span><span class="sxs-lookup"><span data-stu-id="63e28-117">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="63e28-118">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="63e28-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="63e28-119">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="63e28-119">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="63e28-120">建立 App Service 方案。</span><span class="sxs-lookup"><span data-stu-id="63e28-120">Creates an App Service plan.</span></span> <span data-ttu-id="63e28-121">這就像是 Azure Web 應用程式的伺服器陣列。</span><span class="sxs-lookup"><span data-stu-id="63e28-121">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="63e28-122">az appservice web create</span><span class="sxs-lookup"><span data-stu-id="63e28-122">az appservice web create</span></span>](https://docs.microsoft.com/cli/azure/appservice/web#create) | <span data-ttu-id="63e28-123">在 App Service 方案內建立 Azure Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="63e28-123">Creates an Azure web app within the App Service plan.</span></span> |
| [<span data-ttu-id="63e28-124">az network traffic-manager profile create</span><span class="sxs-lookup"><span data-stu-id="63e28-124">az network traffic-manager profile create</span></span>](https://docs.microsoft.com/cli/azure/network/traffic-manager/profile#create) | <span data-ttu-id="63e28-125">建立 Azure 流量管理員設定檔。</span><span class="sxs-lookup"><span data-stu-id="63e28-125">Creates an Azure Traffic Manager profile.</span></span> |
| [<span data-ttu-id="63e28-126">az network traffic-manager endpoint create</span><span class="sxs-lookup"><span data-stu-id="63e28-126">az network traffic-manager endpoint create</span></span>](https://docs.microsoft.com/cli/azure/network/traffic-manager/endpoint#create) | <span data-ttu-id="63e28-127">新增端點至 Azure 流量管理員設定檔。</span><span class="sxs-lookup"><span data-stu-id="63e28-127">Adds a endpoint to an Azure Traffic Manager Profile.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="63e28-128">後續步驟</span><span class="sxs-lookup"><span data-stu-id="63e28-128">Next steps</span></span>

<span data-ttu-id="63e28-129">如需 Azure CLI 的詳細資訊，請參閱 [Azure CLI 文件](https://docs.microsoft.com/cli/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="63e28-129">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="63e28-130">您可以在 [Azure 網路文件](../cli-samples.md)中找到其他的 App Service CLI 指令碼範例。</span><span class="sxs-lookup"><span data-stu-id="63e28-130">Additional App Service CLI script samples can be found in the [Azure Networking documentation](../cli-samples.md).</span></span>
