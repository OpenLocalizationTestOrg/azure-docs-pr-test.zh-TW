---
title: "Azure PowerShell 指令碼範例 - 路由傳送流量以達到應用程式的高可用性 | Microsoft Docs"
description: "Azure PowerShell 指令碼範例 - 路由傳送流量以達到應用程式的高可用性"
services: traffic-manager
documentationcenter: traffic-manager
author: KumudD
manager: timlt
editor: georgewallace
tags: azure-infrastructure
ms.assetid: 
ms.service: traffic-manager
ms.devlang: powershell
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: traffic-manager
ms.date: 05/16/2017
ms.author: gwallace
ms.openlocfilehash: 2f0ac4fd1779661aab04bafb217e64af5d619a2f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="route-traffic-for-high-availability-of-applications"></a><span data-ttu-id="b3ac0-103">路由傳送流量以達到應用程式的高可用性</span><span class="sxs-lookup"><span data-stu-id="b3ac0-103">Route traffic for high availability of applications</span></span>

<span data-ttu-id="b3ac0-104">這個指令碼會建立一個資源群組、兩個 App Service 方案、兩個 Web 應用程式、一個流量管理員設定檔和兩個流量管理員端點。</span><span class="sxs-lookup"><span data-stu-id="b3ac0-104">This script creates a resource group, two app service plans, two web apps, a traffic manager profile, and two traffic manager endpoints.</span></span> <span data-ttu-id="b3ac0-105">流量管理員會將流量導向主要區域中的應用程式，然後當主要區域中的應用程式無法使用時，將流量導向至次要區域。</span><span class="sxs-lookup"><span data-stu-id="b3ac0-105">Traffic Manager directs traffic to the application in one region as the primary region, and to the secondary region when the application in the primary region is unavailable.</span></span> <span data-ttu-id="b3ac0-106">在執行指令碼之前，您必須將 MyWebApp、MyWebAppL1 和 MyWebAppL2 值都變更為整個 Azure 中的唯一值。</span><span class="sxs-lookup"><span data-stu-id="b3ac0-106">Before executing the script, you must change the MyWebApp, MyWebAppL1 and MyWebAppL2 values to unique values across Azure.</span></span> <span data-ttu-id="b3ac0-107">在執行指令碼之後，您可以透過 URL mywebapp.trafficmanager.net 來存取主要區域中的應用程式。</span><span class="sxs-lookup"><span data-stu-id="b3ac0-107">After running the script, you can access the app in the primary region with the URL mywebapp.trafficmanager.net.</span></span>

<span data-ttu-id="b3ac0-108">您可以視需要使用 [Azure PowerShell 指南 (英文)](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/) 中的指示來安裝 Azure PowerShell，然後執行 `Login-AzureRmAccount` 來建立與 Azure 的連線。</span><span class="sxs-lookup"><span data-stu-id="b3ac0-108">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), and then run `Login-AzureRmAccount` to create a connection with Azure.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="b3ac0-109">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="b3ac0-109">Sample script</span></span>

<span data-ttu-id="b3ac0-110">[!code-powershell[主要](../../../powershell_scripts/traffic-manager/direct-traffic-for-increased-application-availability/direct-traffic-for-increased-application-availability.ps1 "路由傳送流量以達到高可用性")]</span><span class="sxs-lookup"><span data-stu-id="b3ac0-110">[!code-powershell[main](../../../powershell_scripts/traffic-manager/direct-traffic-for-increased-application-availability/direct-traffic-for-increased-application-availability.ps1 "Route traffic for high availability")]</span></span>


<span data-ttu-id="b3ac0-111">執行下列命令來移除資源群組、VM 和所有相關資源。</span><span class="sxs-lookup"><span data-stu-id="b3ac0-111">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup1
Remove-AzureRmResourceGroup -Name myResourceGroup2
```


## <a name="script-explanation"></a><span data-ttu-id="b3ac0-112">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="b3ac0-112">Script explanation</span></span>

<span data-ttu-id="b3ac0-113">此指令碼使用下列命令來建立資源群組、Web 應用程式、流量管理員設定檔和所有相關資源。</span><span class="sxs-lookup"><span data-stu-id="b3ac0-113">This script uses the following commands to create a resource group, web app, traffic manager profile, and all related resources.</span></span> <span data-ttu-id="b3ac0-114">下表中的每個命令都會連結至命令特定的文件。</span><span class="sxs-lookup"><span data-stu-id="b3ac0-114">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="b3ac0-115">命令</span><span class="sxs-lookup"><span data-stu-id="b3ac0-115">Command</span></span> | <span data-ttu-id="b3ac0-116">注意事項</span><span class="sxs-lookup"><span data-stu-id="b3ac0-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="b3ac0-117">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="b3ac0-117">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup)  | <span data-ttu-id="b3ac0-118">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="b3ac0-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="b3ac0-119">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="b3ac0-119">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="b3ac0-120">建立 App Service 方案。</span><span class="sxs-lookup"><span data-stu-id="b3ac0-120">Creates an App Service plan.</span></span> <span data-ttu-id="b3ac0-121">這就像是 Azure Web 應用程式的伺服器陣列。</span><span class="sxs-lookup"><span data-stu-id="b3ac0-121">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="b3ac0-122">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="b3ac0-122">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="b3ac0-123">在 App Service 方案內建立 Azure Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="b3ac0-123">Creates an Azure web app within the App Service plan.</span></span> |
| [<span data-ttu-id="b3ac0-124">Set-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="b3ac0-124">Set-AzureRmResource</span></span>](/powershell/module/azurerm.resources/new-azurermresource) | <span data-ttu-id="b3ac0-125">在 App Service 方案內建立 Azure Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="b3ac0-125">Creates an Azure web app within the App Service plan.</span></span> |
| [<span data-ttu-id="b3ac0-126">New-AzureRmTrafficManagerProfile</span><span class="sxs-lookup"><span data-stu-id="b3ac0-126">New-AzureRmTrafficManagerProfile</span></span>](/powershell/module/azurerm.trafficmanager/new-azurermtrafficmanagerprofile) | <span data-ttu-id="b3ac0-127">建立 Azure 流量管理員設定檔。</span><span class="sxs-lookup"><span data-stu-id="b3ac0-127">Creates an Azure Traffic Manager profile.</span></span> |
| [<span data-ttu-id="b3ac0-128">New-AzureRmTrafficManagerEndpoint</span><span class="sxs-lookup"><span data-stu-id="b3ac0-128">New-AzureRmTrafficManagerEndpoint</span></span>](/powershell/module/azurerm.trafficmanager/new-azurermtrafficmanagerendpoint) | <span data-ttu-id="b3ac0-129">新增端點至 Azure 流量管理員設定檔。</span><span class="sxs-lookup"><span data-stu-id="b3ac0-129">Adds a endpoint to an Azure Traffic Manager Profile.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="b3ac0-130">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b3ac0-130">Next steps</span></span>

<span data-ttu-id="b3ac0-131">如需有關 Azure PowerShell 的詳細資訊，請參閱 [Azure PowerShell 文件](https://docs.microsoft.com/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="b3ac0-131">For more information on the Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azure/overview).</span></span>

<span data-ttu-id="b3ac0-132">您可以在 [Azure 網路概觀文件](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json)中找到其他網路 PowerShell 指令碼範例。</span><span class="sxs-lookup"><span data-stu-id="b3ac0-132">Additional networking PowerShell script samples can be found in the [Azure Networking Overview documentation](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span></span>