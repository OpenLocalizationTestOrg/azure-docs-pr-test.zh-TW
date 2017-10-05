---
title: "Azure PowerShell 指令碼範例 - 透過高可用性架構將 Web 應用程式調整為全球可用 | Microsoft Docs"
description: "Azure PowerShell 指令碼範例 - 透過高可用性架構將 Web 應用程式調整為全球可用"
services: app-service\web
documentationcenter: 
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 470f0129-1efe-462c-a029-5c66e04158a8
ms.service: app-service
ms.devlang: multiple
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 03/20/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 9acd1cf4d1a5705811c4dedc545505ec0ac55fc7
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="scale-a-web-app-worldwide-with-a-high-availability-architecture"></a><span data-ttu-id="c49a3-103">透過高可用性架構將 Web 應用程式調整為全球可用</span><span class="sxs-lookup"><span data-stu-id="c49a3-103">Scale a web app worldwide with a high-availability architecture</span></span>

<span data-ttu-id="c49a3-104">在此案例中，您會建立一個資源群組、兩個 App Service 方案、兩個 Web 應用程式、一個流量管理員設定檔和兩個流量管理員端點。</span><span class="sxs-lookup"><span data-stu-id="c49a3-104">In this scenario you will create a resource group, two app service plans, two web apps, a traffic manager profile, and two traffic manager endpoints.</span></span> <span data-ttu-id="c49a3-105">完成此練習後，您就會擁有高可用性架構，可根據最低網路延遲來全球提供 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c49a3-105">Once the exercise is complete you will have a high-available architecture which allows provides global availability of your web app based on the lowest network latency.</span></span>

<span data-ttu-id="c49a3-106">您可以視需要使用 [Azure PowerShell 指南 (英文)](/powershell/azure/overview) 中的指示來安裝 Azure PowerShell，然後執行 `Login-AzureRmAccount` 來建立與 Azure 的連線。</span><span class="sxs-lookup"><span data-stu-id="c49a3-106">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` to create a connection with Azure.</span></span>

## <a name="sample-script"></a><span data-ttu-id="c49a3-107">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="c49a3-107">Sample script</span></span>

<span data-ttu-id="c49a3-108">[!code-powershell[主要](../../../powershell_scripts/app-service/scale-geographic/scale-geographic.ps1 "透過高可用性架構將 Web 應用程式調整為全球可用")]</span><span class="sxs-lookup"><span data-stu-id="c49a3-108">[!code-powershell[main](../../../powershell_scripts/app-service/scale-geographic/scale-geographic.ps1 "Scale a web app worldwide with a high-availability architecture")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="c49a3-109">清除部署</span><span class="sxs-lookup"><span data-stu-id="c49a3-109">Clean up deployment</span></span> 

<span data-ttu-id="c49a3-110">在執行過指令碼範例之後，您可以使用下列命令來移除資源群組、Web 應用程式和所有相關資源。</span><span class="sxs-lookup"><span data-stu-id="c49a3-110">After the script sample has been run, the following command can be used to remove the resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="c49a3-111">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="c49a3-111">Script explanation</span></span>

<span data-ttu-id="c49a3-112">此指令碼會使用下列命令。</span><span class="sxs-lookup"><span data-stu-id="c49a3-112">This script uses the following commands.</span></span> <span data-ttu-id="c49a3-113">下表中的每個命令都會連結至命令特定的文件。</span><span class="sxs-lookup"><span data-stu-id="c49a3-113">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="c49a3-114">命令</span><span class="sxs-lookup"><span data-stu-id="c49a3-114">Command</span></span> | <span data-ttu-id="c49a3-115">注意事項</span><span class="sxs-lookup"><span data-stu-id="c49a3-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="c49a3-116">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="c49a3-116">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="c49a3-117">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="c49a3-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="c49a3-118">New-AzureRMTrafficManagerProfile</span><span class="sxs-lookup"><span data-stu-id="c49a3-118">New-AzureRMTrafficManagerProfile</span></span>](/powershell/module/azurerm.trafficmanager/new-azurermtrafficmanagerprofile) | <span data-ttu-id="c49a3-119">建立流量管理員設定檔。</span><span class="sxs-lookup"><span data-stu-id="c49a3-119">Creates a Traffic Manager profile.</span></span> |
| [<span data-ttu-id="c49a3-120">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="c49a3-120">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="c49a3-121">建立 App Service 方案。</span><span class="sxs-lookup"><span data-stu-id="c49a3-121">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="c49a3-122">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="c49a3-122">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="c49a3-123">建立 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c49a3-123">Creates a web app.</span></span> |
| [<span data-ttu-id="c49a3-124">New-AzureRMTrafficManagerEndpoint</span><span class="sxs-lookup"><span data-stu-id="c49a3-124">New-AzureRMTrafficManagerEndpoint</span></span>](/powershell/module/azurerm.trafficmanager/new-azurermtrafficmanagerendpoint) | <span data-ttu-id="c49a3-125">在流量管理員設定檔中建立端點。</span><span class="sxs-lookup"><span data-stu-id="c49a3-125">Creates an endpoint in a Traffic Manager profile.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="c49a3-126">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c49a3-126">Next steps</span></span>

<span data-ttu-id="c49a3-127">如需有關 Azure PowerShell 模組的詳細資訊，請參閱 [Azure PowerShell 文件](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="c49a3-127">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="c49a3-128">您可以在 [Azure PowerShell 範例](../app-service-powershell-samples.md)中找到適用於 App Service Web Apps 的其他 Azure PowerShell 範例。</span><span class="sxs-lookup"><span data-stu-id="c49a3-128">Additional Azure Powershell samples for Azure App Service Web Apps can be found in the [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
