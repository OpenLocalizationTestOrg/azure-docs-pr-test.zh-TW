---
title: "PowerShell 指令碼範例應用程式的高可用性的路由傳送流量 aaaAzure |Microsoft 文件"
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
ms.openlocfilehash: 11d15780403b4ed79e85d7b3495bc5d674bfdaee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="route-traffic-for-high-availability-of-applications"></a><span data-ttu-id="6778c-103">路由傳送流量以達到應用程式的高可用性</span><span class="sxs-lookup"><span data-stu-id="6778c-103">Route traffic for high availability of applications</span></span>

<span data-ttu-id="6778c-104">這個指令碼會建立一個資源群組、兩個 App Service 方案、兩個 Web 應用程式、一個流量管理員設定檔和兩個流量管理員端點。</span><span class="sxs-lookup"><span data-stu-id="6778c-104">This script creates a resource group, two app service plans, two web apps, a traffic manager profile, and two traffic manager endpoints.</span></span> <span data-ttu-id="6778c-105">Hello hello 主要區域中的應用程式無法使用時，traffic Manager 將導向流量 toohello 應用程式與 hello 主要區域中，一個區域及 toohello 次要區域。</span><span class="sxs-lookup"><span data-stu-id="6778c-105">Traffic Manager directs traffic toohello application in one region as hello primary region, and toohello secondary region when hello application in hello primary region is unavailable.</span></span> <span data-ttu-id="6778c-106">在執行之前 hello 指令碼，您必須變更 hello MyWebApp，MyWebAppL1 和 MyWebAppL2 值 toounique 值在整個 Azure。</span><span class="sxs-lookup"><span data-stu-id="6778c-106">Before executing hello script, you must change hello MyWebApp, MyWebAppL1 and MyWebAppL2 values toounique values across Azure.</span></span> <span data-ttu-id="6778c-107">執行 hello 指令碼之後, 您可以存取與 hello URL mywebapp.trafficmanager.net hello 主要區域中的 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="6778c-107">After running hello script, you can access hello app in hello primary region with hello URL mywebapp.trafficmanager.net.</span></span>

<span data-ttu-id="6778c-108">如有需要安裝 Azure PowerShell 中使用 hello 指令位於 hello hello [Azure PowerShell 指南](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/)，然後執行`Login-AzureRmAccount`toocreate 與 Azure 的連線。</span><span class="sxs-lookup"><span data-stu-id="6778c-108">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="6778c-109">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="6778c-109">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/traffic-manager/direct-traffic-for-increased-application-availability/direct-traffic-for-increased-application-availability.ps1 "Route traffic for high availability")]


<span data-ttu-id="6778c-110">執行下列命令 tooremove hello 資源群組、 VM 和所有相關的資源的 hello。</span><span class="sxs-lookup"><span data-stu-id="6778c-110">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup1
Remove-AzureRmResourceGroup -Name myResourceGroup2
```


## <a name="script-explanation"></a><span data-ttu-id="6778c-111">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="6778c-111">Script explanation</span></span>

<span data-ttu-id="6778c-112">此指令碼會使用下列命令 toocreate 資源群組、 web 應用程式、 流量管理員設定檔，hello 和所有相關聯的資源。</span><span class="sxs-lookup"><span data-stu-id="6778c-112">This script uses hello following commands toocreate a resource group, web app, traffic manager profile, and all related resources.</span></span> <span data-ttu-id="6778c-113">Hello 資料表連結 toocommand 特定文件中的每個命令。</span><span class="sxs-lookup"><span data-stu-id="6778c-113">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="6778c-114">命令</span><span class="sxs-lookup"><span data-stu-id="6778c-114">Command</span></span> | <span data-ttu-id="6778c-115">注意事項</span><span class="sxs-lookup"><span data-stu-id="6778c-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="6778c-116">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="6778c-116">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup)  | <span data-ttu-id="6778c-117">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="6778c-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="6778c-118">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="6778c-118">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="6778c-119">建立 App Service 方案。</span><span class="sxs-lookup"><span data-stu-id="6778c-119">Creates an App Service plan.</span></span> <span data-ttu-id="6778c-120">這就像是 Azure Web 應用程式的伺服器陣列。</span><span class="sxs-lookup"><span data-stu-id="6778c-120">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="6778c-121">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="6778c-121">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="6778c-122">建立 Azure web 應用程式內 hello 應用程式服務方案。</span><span class="sxs-lookup"><span data-stu-id="6778c-122">Creates an Azure web app within hello App Service plan.</span></span> |
| [<span data-ttu-id="6778c-123">Set-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="6778c-123">Set-AzureRmResource</span></span>](/powershell/module/azurerm.resources/new-azurermresource) | <span data-ttu-id="6778c-124">建立 Azure web 應用程式內 hello 應用程式服務方案。</span><span class="sxs-lookup"><span data-stu-id="6778c-124">Creates an Azure web app within hello App Service plan.</span></span> |
| [<span data-ttu-id="6778c-125">New-AzureRmTrafficManagerProfile</span><span class="sxs-lookup"><span data-stu-id="6778c-125">New-AzureRmTrafficManagerProfile</span></span>](/powershell/module/azurerm.trafficmanager/new-azurermtrafficmanagerprofile) | <span data-ttu-id="6778c-126">建立 Azure 流量管理員設定檔。</span><span class="sxs-lookup"><span data-stu-id="6778c-126">Creates an Azure Traffic Manager profile.</span></span> |
| [<span data-ttu-id="6778c-127">New-AzureRmTrafficManagerEndpoint</span><span class="sxs-lookup"><span data-stu-id="6778c-127">New-AzureRmTrafficManagerEndpoint</span></span>](/powershell/module/azurerm.trafficmanager/new-azurermtrafficmanagerendpoint) | <span data-ttu-id="6778c-128">加入端點 tooan Azure 流量管理員設定檔。</span><span class="sxs-lookup"><span data-stu-id="6778c-128">Adds a endpoint tooan Azure Traffic Manager Profile.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="6778c-129">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6778c-129">Next steps</span></span>

<span data-ttu-id="6778c-130">如需有關 hello Azure PowerShell 的詳細資訊，請參閱[Azure PowerShell 文件](https://docs.microsoft.com/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="6778c-130">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azure/overview).</span></span>

<span data-ttu-id="6778c-131">其他網路的 PowerShell 指令碼範例可以在 hello [Azure 網路概觀文件](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="6778c-131">Additional networking PowerShell script samples can be found in hello [Azure Networking Overview documentation](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span></span>
