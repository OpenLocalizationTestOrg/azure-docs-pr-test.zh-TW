---
title: "Azure PowerShell 指令碼範例 - 建立 Web 應用程式並將程式碼部署至預備環境 | Microsoft Docs"
description: "Azure PowerShell 指令碼範例 - 建立 Web 應用程式並將程式碼部署至預備環境"
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 27cf0680-c3a9-4a58-9f71-6dec09f6b874
ms.service: app-service-web
ms.workload: web
ms.devlang: na
ms.topic: sample
ms.date: 03/20/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 55adc13350eb0f4711efa3c901f6e4e7755dfb27
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-web-app-and-deploy-code-to-a-staging-environment"></a><span data-ttu-id="7e32c-103">建立 Web 應用程式並將程式碼部署至預備環境</span><span class="sxs-lookup"><span data-stu-id="7e32c-103">Create a web app and deploy code to a staging environment</span></span>

<span data-ttu-id="7e32c-104">此範例指令碼會在 App Service 中建立 Web 應用程式以及稱為「預備」的其他部署位置，然後將範例應用程式部署至「預備」位置。</span><span class="sxs-lookup"><span data-stu-id="7e32c-104">This sample script creates a web app in App Service with an additional deployment slot called "staging", and then deploys a sample app to the "staging" slot.</span></span>

<span data-ttu-id="7e32c-105">您可以視需要使用 [Azure PowerShell 指南 (英文)](/powershell/azure/overview) 中的指示來安裝 Azure PowerShell，然後執行 `Login-AzureRmAccount` 來建立與 Azure 的連線。</span><span class="sxs-lookup"><span data-stu-id="7e32c-105">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` to create a connection with Azure.</span></span>

## <a name="sample-script"></a><span data-ttu-id="7e32c-106">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="7e32c-106">Sample script</span></span>

<span data-ttu-id="7e32c-107">[!code-powershell[主要](../../../powershell_scripts/app-service/deploy-deployment-slot/deploy-deployment-slot.ps1?highlight=1 "建立 Web 應用程式並將程式碼部署至預備環境")]</span><span class="sxs-lookup"><span data-stu-id="7e32c-107">[!code-powershell[main](../../../powershell_scripts/app-service/deploy-deployment-slot/deploy-deployment-slot.ps1?highlight=1 "Create a web app and deploy code to a staging environment")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="7e32c-108">清除部署</span><span class="sxs-lookup"><span data-stu-id="7e32c-108">Clean up deployment</span></span> 

<span data-ttu-id="7e32c-109">在執行過指令碼範例之後，您可以使用下列命令來移除資源群組、Web 應用程式和所有相關資源。</span><span class="sxs-lookup"><span data-stu-id="7e32c-109">After the script sample has been run, the following command can be used to remove the resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="7e32c-110">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="7e32c-110">Script explanation</span></span>

<span data-ttu-id="7e32c-111">此指令碼會使用下列命令。</span><span class="sxs-lookup"><span data-stu-id="7e32c-111">This script uses the following commands.</span></span> <span data-ttu-id="7e32c-112">下表中的每個命令都會連結至命令特定的文件。</span><span class="sxs-lookup"><span data-stu-id="7e32c-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="7e32c-113">命令</span><span class="sxs-lookup"><span data-stu-id="7e32c-113">Command</span></span> | <span data-ttu-id="7e32c-114">注意事項</span><span class="sxs-lookup"><span data-stu-id="7e32c-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="7e32c-115">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="7e32c-115">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="7e32c-116">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="7e32c-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="7e32c-117">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="7e32c-117">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="7e32c-118">建立 App Service 方案。</span><span class="sxs-lookup"><span data-stu-id="7e32c-118">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="7e32c-119">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="7e32c-119">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="7e32c-120">建立 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="7e32c-120">Creates a web app.</span></span> |
| [<span data-ttu-id="7e32c-121">Set-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="7e32c-121">Set-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/set-azurermappserviceplan) | <span data-ttu-id="7e32c-122">修改 App Service 方案來變更其定價層。</span><span class="sxs-lookup"><span data-stu-id="7e32c-122">Modifies an App Service plan to change its pricing tier.</span></span> |
| [<span data-ttu-id="7e32c-123">New-AzureRmWebAppSlot</span><span class="sxs-lookup"><span data-stu-id="7e32c-123">New-AzureRmWebAppSlot</span></span>](/powershell/module/azurerm.websites/new-azurermwebappslot) | <span data-ttu-id="7e32c-124">建立 Web 應用程式的部署位置。</span><span class="sxs-lookup"><span data-stu-id="7e32c-124">Creates a deployment slot for a web app.</span></span> |
| [<span data-ttu-id="7e32c-125">Set-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="7e32c-125">Set-AzureRmResource</span></span>](/powershell/module/azurerm.resources/set-azurermresource) | <span data-ttu-id="7e32c-126">修改資源群組中的資源。</span><span class="sxs-lookup"><span data-stu-id="7e32c-126">Modifies a resource in a resource group.</span></span> |
| [<span data-ttu-id="7e32c-127">Swap-AzureRmWebAppSlot</span><span class="sxs-lookup"><span data-stu-id="7e32c-127">Swap-AzureRmWebAppSlot</span></span>](/powershell/module/azurerm.websites/swap-azurermwebappslot) | <span data-ttu-id="7e32c-128">將 Web 應用程式的部署位置切換到生產環境。</span><span class="sxs-lookup"><span data-stu-id="7e32c-128">Swaps a web app's deployment slot into production.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="7e32c-129">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7e32c-129">Next steps</span></span>

<span data-ttu-id="7e32c-130">如需有關 Azure PowerShell 模組的詳細資訊，請參閱 [Azure PowerShell 文件](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="7e32c-130">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="7e32c-131">您可以在 [Azure PowerShell 範例](../app-service-powershell-samples.md)中找到適用於 App Service Web Apps 的其他 Azure PowerShell 範例。</span><span class="sxs-lookup"><span data-stu-id="7e32c-131">Additional Azure Powershell samples for Azure App Service Web Apps can be found in the [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
