---
title: "Azure PowerShell 指令碼範例 - 手動調整 Web 應用程式 | Microsoft Docs"
description: "Azure PowerShell 指令碼範例 - 手動調整 Web 應用程式"
services: app-service\web
documentationcenter: 
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: de5d4285-9c7d-4735-a695-288264047375
ms.service: app-service
ms.devlang: multiple
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 03/20/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: e99dfc02b6ab4123cd5f95997285dca5cb686380
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="scale-a-web-app-manually"></a><span data-ttu-id="47b01-103">手動調整 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="47b01-103">Scale a web app manually</span></span>

<span data-ttu-id="47b01-104">在此案例中，您會學習如何建立資源群組、App Service 方案和 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="47b01-104">In this scenario you will learn to create a resource group, app service plan and web app.</span></span> <span data-ttu-id="47b01-105">然後，您會將 App Service 方案從單一執行個體調整為多個執行個體。</span><span class="sxs-lookup"><span data-stu-id="47b01-105">You will then scale the App Service Plan from a single instance to multiple instances.</span></span>

<span data-ttu-id="47b01-106">您可以視需要使用 [Azure PowerShell 指南 (英文)](/powershell/azure/overview) 中的指示來安裝 Azure PowerShell，然後執行 `Login-AzureRmAccount` 來建立與 Azure 的連線。</span><span class="sxs-lookup"><span data-stu-id="47b01-106">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` to create a connection with Azure.</span></span>

## <a name="sample-script"></a><span data-ttu-id="47b01-107">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="47b01-107">Sample script</span></span>

<span data-ttu-id="47b01-108">[!code-powershell[主要](../../../powershell_scripts/app-service/scale-manual/scale-manual.ps1 "手動調整 Web 應用程式")]</span><span class="sxs-lookup"><span data-stu-id="47b01-108">[!code-powershell[main](../../../powershell_scripts/app-service/scale-manual/scale-manual.ps1 "Scale a web app manually")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="47b01-109">清除部署</span><span class="sxs-lookup"><span data-stu-id="47b01-109">Clean up deployment</span></span> 

<span data-ttu-id="47b01-110">在執行過指令碼範例之後，您可以使用下列命令來移除資源群組、Web 應用程式和所有相關資源。</span><span class="sxs-lookup"><span data-stu-id="47b01-110">After the script sample has been run, the following command can be used to remove the resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="47b01-111">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="47b01-111">Script explanation</span></span>

<span data-ttu-id="47b01-112">此指令碼會使用下列命令。</span><span class="sxs-lookup"><span data-stu-id="47b01-112">This script uses the following commands.</span></span> <span data-ttu-id="47b01-113">下表中的每個命令都會連結至命令特定的文件。</span><span class="sxs-lookup"><span data-stu-id="47b01-113">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="47b01-114">命令</span><span class="sxs-lookup"><span data-stu-id="47b01-114">Command</span></span> | <span data-ttu-id="47b01-115">注意事項</span><span class="sxs-lookup"><span data-stu-id="47b01-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="47b01-116">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="47b01-116">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="47b01-117">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="47b01-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="47b01-118">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="47b01-118">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="47b01-119">建立 App Service 方案。</span><span class="sxs-lookup"><span data-stu-id="47b01-119">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="47b01-120">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="47b01-120">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="47b01-121">建立 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="47b01-121">Creates a web app.</span></span> |
| [<span data-ttu-id="47b01-122">Set-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="47b01-122">Set-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/set-azurermwebapp) | <span data-ttu-id="47b01-123">修改 Web 應用程式的組態。</span><span class="sxs-lookup"><span data-stu-id="47b01-123">Modifies a web app's configuration.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="47b01-124">後續步驟</span><span class="sxs-lookup"><span data-stu-id="47b01-124">Next steps</span></span>

<span data-ttu-id="47b01-125">如需有關 Azure PowerShell 模組的詳細資訊，請參閱 [Azure PowerShell 文件](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="47b01-125">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="47b01-126">您可以在 [Azure PowerShell 範例](../app-service-powershell-samples.md)中找到適用於 App Service Web Apps 的其他 Azure PowerShell 範例。</span><span class="sxs-lookup"><span data-stu-id="47b01-126">Additional Azure Powershell samples for Azure App Service Web Apps can be found in the [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
