---
title: "Azure PowerShell 指令碼範例 - 將 Web 應用程式連線至 SQL 資料庫 | Microsoft Docs"
description: "Azure PowerShell 指令碼範例 - 將 Web 應用程式連線至 SQL 資料庫"
services: app-service\web
documentationcenter: 
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 055440a9-fff1-49b2-b964-9c95b364e533
ms.service: app-service
ms.devlang: multiple
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 03/20/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 5312bf6b81d1cc48490b71c3f77323cca23e1559
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="connect-a-web-app-to-a-sql-database"></a><span data-ttu-id="dfec6-103">將 Web 應用程式連接至 SQL Database</span><span class="sxs-lookup"><span data-stu-id="dfec6-103">Connect a web app to a SQL database</span></span>

<span data-ttu-id="dfec6-104">在此案例中，您會學習如何建立 Azure SQL Database 和 Azure Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="dfec6-104">In this scenario you will learn how to create an Azure SQL database and an Azure web app.</span></span> <span data-ttu-id="dfec6-105">然後，您會使用應用程式設定將 SQL Database 連結到 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="dfec6-105">Then you will link the SQL database to the web app using app settings.</span></span>

<span data-ttu-id="dfec6-106">您可以視需要使用 [Azure PowerShell 指南 (英文)](/powershell/azure/overview) 中的指示來安裝 Azure PowerShell，然後執行 `Login-AzureRmAccount` 來建立與 Azure 的連線。</span><span class="sxs-lookup"><span data-stu-id="dfec6-106">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` to create a connection with Azure.</span></span>

## <a name="sample-script"></a><span data-ttu-id="dfec6-107">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="dfec6-107">Sample script</span></span>

<span data-ttu-id="dfec6-108">[!code-powershell[主要](../../../powershell_scripts/app-service/connect-to-sql/connect-to-sql.ps1?highlight=13 "將 Web 應用程式連線至 SQL 資料庫")]</span><span class="sxs-lookup"><span data-stu-id="dfec6-108">[!code-powershell[main](../../../powershell_scripts/app-service/connect-to-sql/connect-to-sql.ps1?highlight=13 "Connect a web app to a SQL database")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="dfec6-109">清除部署</span><span class="sxs-lookup"><span data-stu-id="dfec6-109">Clean up deployment</span></span> 

<span data-ttu-id="dfec6-110">在執行過指令碼範例之後，您可以使用下列命令來移除資源群組、Web 應用程式和所有相關資源。</span><span class="sxs-lookup"><span data-stu-id="dfec6-110">After the script sample has been run, the following command can be used to remove the resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="dfec6-111">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="dfec6-111">Script explanation</span></span>

<span data-ttu-id="dfec6-112">此指令碼會使用下列命令。</span><span class="sxs-lookup"><span data-stu-id="dfec6-112">This script uses the following commands.</span></span> <span data-ttu-id="dfec6-113">下表中的每個命令都會連結至命令特定的文件。</span><span class="sxs-lookup"><span data-stu-id="dfec6-113">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="dfec6-114">命令</span><span class="sxs-lookup"><span data-stu-id="dfec6-114">Command</span></span> | <span data-ttu-id="dfec6-115">注意事項</span><span class="sxs-lookup"><span data-stu-id="dfec6-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="dfec6-116">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="dfec6-116">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="dfec6-117">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="dfec6-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="dfec6-118">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="dfec6-118">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="dfec6-119">建立 App Service 方案。</span><span class="sxs-lookup"><span data-stu-id="dfec6-119">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="dfec6-120">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="dfec6-120">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="dfec6-121">建立 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="dfec6-121">Creates a web app.</span></span> |
| [<span data-ttu-id="dfec6-122">New-AzureRMSQLServer</span><span class="sxs-lookup"><span data-stu-id="dfec6-122">New-AzureRMSQLServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="dfec6-123">建立 SQL Database 伺服器。</span><span class="sxs-lookup"><span data-stu-id="dfec6-123">Creates a SQL Database server.</span></span> |
| [<span data-ttu-id="dfec6-124">New-AzureRmSqlServerFirewallRule</span><span class="sxs-lookup"><span data-stu-id="dfec6-124">New-AzureRmSqlServerFirewallRule</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserverfirewallrule) | <span data-ttu-id="dfec6-125">建立 SQL Database 伺服器防火牆規則。</span><span class="sxs-lookup"><span data-stu-id="dfec6-125">Creates a firewall rule for a SQL Database server.</span></span> |
| [<span data-ttu-id="dfec6-126">New-AzureRMSQLDatabase</span><span class="sxs-lookup"><span data-stu-id="dfec6-126">New-AzureRMSQLDatabase</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabase) | <span data-ttu-id="dfec6-127">建立資料庫或彈性資料庫。</span><span class="sxs-lookup"><span data-stu-id="dfec6-127">Creates a database or an elastic database.</span></span> |
| [<span data-ttu-id="dfec6-128">Set-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="dfec6-128">Set-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/set-azurermwebapp) | <span data-ttu-id="dfec6-129">修改 Web 應用程式的組態。</span><span class="sxs-lookup"><span data-stu-id="dfec6-129">Modifies a web app's configuration.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="dfec6-130">後續步驟</span><span class="sxs-lookup"><span data-stu-id="dfec6-130">Next steps</span></span>

<span data-ttu-id="dfec6-131">如需有關 Azure PowerShell 模組的詳細資訊，請參閱 [Azure PowerShell 文件](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="dfec6-131">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="dfec6-132">您可以在 [Azure PowerShell 範例](../app-service-powershell-samples.md)中找到適用於 App Service Web Apps 的其他 Azure PowerShell 範例。</span><span class="sxs-lookup"><span data-stu-id="dfec6-132">Additional Azure Powershell samples for Azure App Service Web Apps can be found in the [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
