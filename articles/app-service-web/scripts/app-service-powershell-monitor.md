---
title: "Azure PowerShell 指令碼範例 - 使用 Web 伺服器記錄監視 Web 應用程式 | Microsoft Docs"
description: "Azure PowerShell 指令碼範例 - 使用 Web 伺服器記錄監視 Web 應用程式"
services: app-service\web
documentationcenter: 
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 5805d7cd-9e56-4eba-bd85-75b013690ff5
ms.service: app-service
ms.devlang: multiple
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 03/20/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 34a3dd318cb9896342fce870922ecd113b3ed08d
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="monitor-a-web-app-with-web-server-logs"></a><span data-ttu-id="7a5ef-103">使用 Web 伺服器記錄監視 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="7a5ef-103">Monitor a web app with web server logs</span></span>

<span data-ttu-id="7a5ef-104">在此案例中，您會建立資源群組、App Service 方案、Web 應用程式，並設定 Web 應用程式來啟用 Web 伺服器記錄。</span><span class="sxs-lookup"><span data-stu-id="7a5ef-104">In this scenario you will create a resource group, app service plan, web app and configure the web app to enable web server logs.</span></span> <span data-ttu-id="7a5ef-105">然後，您會下載記錄檔來進行檢閱。</span><span class="sxs-lookup"><span data-stu-id="7a5ef-105">You will then download the log files for review.</span></span>

<span data-ttu-id="7a5ef-106">您可以視需要使用 [Azure PowerShell 指南 (英文)](/powershell/azure/overview) 中的指示來安裝 Azure PowerShell，然後執行 `Login-AzureRmAccount` 來建立與 Azure 的連線。</span><span class="sxs-lookup"><span data-stu-id="7a5ef-106">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` to create a connection with Azure.</span></span>

## <a name="sample-script"></a><span data-ttu-id="7a5ef-107">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="7a5ef-107">Sample script</span></span>

<span data-ttu-id="7a5ef-108">[!code-powershell[main](../../../powershell_scripts/app-service/monitor-with-logs/monitor-with-logs.ps1 "使用 Web 伺服器記錄監視 Web 應用程式")]</span><span class="sxs-lookup"><span data-stu-id="7a5ef-108">[!code-powershell[main](../../../powershell_scripts/app-service/monitor-with-logs/monitor-with-logs.ps1 "Monitor a web app with web server logs")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="7a5ef-109">清除部署</span><span class="sxs-lookup"><span data-stu-id="7a5ef-109">Clean up deployment</span></span> 

<span data-ttu-id="7a5ef-110">在執行過指令碼範例之後，您可以使用下列命令來移除資源群組、Web 應用程式和所有相關資源。</span><span class="sxs-lookup"><span data-stu-id="7a5ef-110">After the script sample has been run, the following command can be used to remove the resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="7a5ef-111">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="7a5ef-111">Script explanation</span></span>

<span data-ttu-id="7a5ef-112">此指令碼會使用下列命令。</span><span class="sxs-lookup"><span data-stu-id="7a5ef-112">This script uses the following commands.</span></span> <span data-ttu-id="7a5ef-113">下表中的每個命令都會連結至命令特定的文件。</span><span class="sxs-lookup"><span data-stu-id="7a5ef-113">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="7a5ef-114">命令</span><span class="sxs-lookup"><span data-stu-id="7a5ef-114">Command</span></span> | <span data-ttu-id="7a5ef-115">注意事項</span><span class="sxs-lookup"><span data-stu-id="7a5ef-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="7a5ef-116">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="7a5ef-116">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="7a5ef-117">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="7a5ef-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="7a5ef-118">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="7a5ef-118">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="7a5ef-119">建立 App Service 方案。</span><span class="sxs-lookup"><span data-stu-id="7a5ef-119">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="7a5ef-120">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="7a5ef-120">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="7a5ef-121">建立 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="7a5ef-121">Creates a web app.</span></span> |
| [<span data-ttu-id="7a5ef-122">Set-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="7a5ef-122">Set-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/set-azurermwebapp) | <span data-ttu-id="7a5ef-123">修改 Web 應用程式的組態。</span><span class="sxs-lookup"><span data-stu-id="7a5ef-123">Modifies a web app's configuration.</span></span> |
| [<span data-ttu-id="7a5ef-124">Get-AzureRMWebAppMetrics</span><span class="sxs-lookup"><span data-stu-id="7a5ef-124">Get-AzureRMWebAppMetrics</span></span>](/powershell/module/azurerm.websites/get-azurermwebappmetrics) | <span data-ttu-id="7a5ef-125">取得 Web 應用程式的計量。</span><span class="sxs-lookup"><span data-stu-id="7a5ef-125">Gets a web app's metrics.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="7a5ef-126">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7a5ef-126">Next steps</span></span>

<span data-ttu-id="7a5ef-127">如需有關 Azure PowerShell 模組的詳細資訊，請參閱 [Azure PowerShell 文件](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="7a5ef-127">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="7a5ef-128">您可以在 [Azure PowerShell 範例](../app-service-powershell-samples.md)中找到適用於 App Service Web Apps 的其他 Azure PowerShell 範例。</span><span class="sxs-lookup"><span data-stu-id="7a5ef-128">Additional Azure Powershell samples for Azure App Service Web Apps can be found in the [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
