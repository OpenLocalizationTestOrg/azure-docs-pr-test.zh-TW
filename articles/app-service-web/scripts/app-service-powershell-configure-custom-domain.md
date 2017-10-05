---
title: "Azure PowerShell 指令碼範例 - 將自訂網域指派給 Web 應用程式 | Microsoft Docs"
description: "Azure PowerShell 指令碼範例 - 將自訂網域指派給 Web 應用程式"
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 356f5af9-f62e-411c-8b24-deba05214103
ms.service: app-service-web
ms.workload: web
ms.devlang: na
ms.topic: sample
ms.date: 03/20/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 6d25fe8098848fc69470c77e3200bee554c1f875
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="assign-a-custom-domain-to-a-web-app"></a><span data-ttu-id="8f954-103">將自訂網域指派給 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="8f954-103">Assign a custom domain to a web app</span></span>

<span data-ttu-id="8f954-104">此範例指令碼會在 App Service 中建立 Web 應用程式及其相關資源，然後將 `www.<yourdomain>` 與其對應。</span><span class="sxs-lookup"><span data-stu-id="8f954-104">This sample script creates a web app in App Service with its related resources, and then maps `www.<yourdomain>` to it.</span></span> 

<span data-ttu-id="8f954-105">您可以視需要使用 [Azure PowerShell 指南 (英文)](/powershell/azure/overview) 中的指示來安裝 Azure PowerShell，然後執行 `Login-AzureRmAccount` 來建立與 Azure 的連線。</span><span class="sxs-lookup"><span data-stu-id="8f954-105">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` to create a connection with Azure.</span></span> <span data-ttu-id="8f954-106">此外，您還需要網域註冊機構的 DNS 設定頁面的存取權。</span><span class="sxs-lookup"><span data-stu-id="8f954-106">Also, you need to have access to your domain registrar's DNS configuration page.</span></span>

## <a name="sample-script"></a><span data-ttu-id="8f954-107">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="8f954-107">Sample script</span></span>

<span data-ttu-id="8f954-108">[!code-powershell[主要](../../../powershell_scripts/app-service/map-custom-domain/map-custom-domain.ps1?highlight=1 "將自訂網域指派給 Web 應用程式")]</span><span class="sxs-lookup"><span data-stu-id="8f954-108">[!code-powershell[main](../../../powershell_scripts/app-service/map-custom-domain/map-custom-domain.ps1?highlight=1 "Assign a custom domain to a web app")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="8f954-109">清除部署</span><span class="sxs-lookup"><span data-stu-id="8f954-109">Clean up deployment</span></span> 

<span data-ttu-id="8f954-110">在執行過指令碼範例之後，您可以使用下列命令來移除資源群組、Web 應用程式和所有相關資源。</span><span class="sxs-lookup"><span data-stu-id="8f954-110">After the script sample has been run, the following command can be used to remove the resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="8f954-111">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="8f954-111">Script explanation</span></span>

<span data-ttu-id="8f954-112">此指令碼會使用下列命令。</span><span class="sxs-lookup"><span data-stu-id="8f954-112">This script uses the following commands.</span></span> <span data-ttu-id="8f954-113">下表中的每個命令都會連結至命令特定的文件。</span><span class="sxs-lookup"><span data-stu-id="8f954-113">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="8f954-114">命令</span><span class="sxs-lookup"><span data-stu-id="8f954-114">Command</span></span> | <span data-ttu-id="8f954-115">注意事項</span><span class="sxs-lookup"><span data-stu-id="8f954-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="8f954-116">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="8f954-116">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="8f954-117">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="8f954-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="8f954-118">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="8f954-118">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="8f954-119">建立 App Service 方案。</span><span class="sxs-lookup"><span data-stu-id="8f954-119">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="8f954-120">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="8f954-120">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="8f954-121">建立 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="8f954-121">Creates a web app.</span></span> |
| [<span data-ttu-id="8f954-122">Set-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="8f954-122">Set-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/set-azurermappserviceplan) | <span data-ttu-id="8f954-123">修改 App Service 方案來變更其定價層。</span><span class="sxs-lookup"><span data-stu-id="8f954-123">Modifies an App Service plan to change its pricing tier.</span></span> |
| [<span data-ttu-id="8f954-124">Set-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="8f954-124">Set-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/set-azurermwebapp) | <span data-ttu-id="8f954-125">修改 Web 應用程式的組態。</span><span class="sxs-lookup"><span data-stu-id="8f954-125">Modifies a web app's configuration.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="8f954-126">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8f954-126">Next steps</span></span>

<span data-ttu-id="8f954-127">如需有關 Azure PowerShell 模組的詳細資訊，請參閱 [Azure PowerShell 文件](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="8f954-127">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="8f954-128">您可以在 [Azure PowerShell 範例](../app-service-powershell-samples.md)中找到適用於 App Service Web Apps 的其他 Azure PowerShell 範例。</span><span class="sxs-lookup"><span data-stu-id="8f954-128">Additional Azure Powershell samples for Azure App Service Web Apps can be found in the [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
