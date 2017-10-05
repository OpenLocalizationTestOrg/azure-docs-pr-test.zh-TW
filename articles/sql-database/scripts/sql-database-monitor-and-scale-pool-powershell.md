---
title: "PowerShell 範例 - 監視 - 調整 SQL 彈性集區 - Azure SQL Database | Microsoft Docs"
description: "在 Azure SQL Database 中監視和調整 SQL 彈性集區的 Azure PowerShell 範例指令碼"
services: sql-database
documentationcenter: sql-database
author: janeng
manager: jstrauss
editor: carlrab
tags: azure-service-management
ms.assetid: 
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: PowerShell
ms.topic: sample
ms.tgt_pltfrm: sql-database
ms.workload: database
ms.date: 06/23/2017
ms.author: janeng
ms.openlocfilehash: 7b6a5bd43aadbed33882cf0736ec70436ffdb47b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="use-powershell-to-monitor-and-scale-a-sql-elastic-pool-in-azure-sql-database"></a><span data-ttu-id="72a0e-103">使用 PowerShell 在 Azure SQL Database 中監視和調整 SQL 彈性集區</span><span class="sxs-lookup"><span data-stu-id="72a0e-103">Use PowerShell to monitor and scale a SQL elastic pool in Azure SQL Database</span></span>

<span data-ttu-id="72a0e-104">此 PowerShell 指令碼範例會監視彈性集區的效能計量、將其調整為較高的效能等級，並對其中一個效能計量建立警示規則。</span><span class="sxs-lookup"><span data-stu-id="72a0e-104">This PowerShell script example monitors the performance metrics of an elastic pool, scales it to a higher performance level, and creates an alert rule on one of the performance metrics.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="72a0e-105">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="72a0e-105">Sample script</span></span>

<span data-ttu-id="72a0e-106">[!code-powershell[主要](../../../powershell_scripts/sql-database/monitor-and-scale-pool/monitor-and-scale-pool.ps1?highlight=16-17 "監視和調整單一 SQL Database")]</span><span class="sxs-lookup"><span data-stu-id="72a0e-106">[!code-powershell[main](../../../powershell_scripts/sql-database/monitor-and-scale-pool/monitor-and-scale-pool.ps1?highlight=16-17 "Monitor and scale single SQL Database")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="72a0e-107">清除部署</span><span class="sxs-lookup"><span data-stu-id="72a0e-107">Clean up deployment</span></span>

<span data-ttu-id="72a0e-108">在執行過指令碼範例之後，您可以使用下列命令來移除資源群組和所有與其相關聯的資源。</span><span class="sxs-lookup"><span data-stu-id="72a0e-108">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="72a0e-109">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="72a0e-109">Script explanation</span></span>

<span data-ttu-id="72a0e-110">此指令碼會使用下列命令。</span><span class="sxs-lookup"><span data-stu-id="72a0e-110">This script uses the following commands.</span></span> <span data-ttu-id="72a0e-111">下表中的每個命令都會連結至命令特定的文件。</span><span class="sxs-lookup"><span data-stu-id="72a0e-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="72a0e-112">命令</span><span class="sxs-lookup"><span data-stu-id="72a0e-112">Command</span></span> | <span data-ttu-id="72a0e-113">注意事項</span><span class="sxs-lookup"><span data-stu-id="72a0e-113">Notes</span></span> |
|---|---|
 [<span data-ttu-id="72a0e-114">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="72a0e-114">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="72a0e-115">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="72a0e-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="72a0e-116">New-AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="72a0e-116">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="72a0e-117">建立主機資料庫或彈性集區的邏輯伺服器。</span><span class="sxs-lookup"><span data-stu-id="72a0e-117">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="72a0e-118">New-AzureRmSqlElasticPool</span><span class="sxs-lookup"><span data-stu-id="72a0e-118">New-AzureRmSqlElasticPool</span></span>](/powershell/module/azurerm.sql/new-azurermsqlelasticpool) | <span data-ttu-id="72a0e-119">在邏輯伺服器內建立彈性集區。</span><span class="sxs-lookup"><span data-stu-id="72a0e-119">Creates an elastic pool within a logical server.</span></span> |
| [<span data-ttu-id="72a0e-120">New-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="72a0e-120">New-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabase) | <span data-ttu-id="72a0e-121">在邏輯伺服器中將資料庫建立為單一或集區的資料庫。</span><span class="sxs-lookup"><span data-stu-id="72a0e-121">Creates a database in a logical server as a single or a pooled database.</span></span> |
| [<span data-ttu-id="72a0e-122">Get-AzureRmMetric</span><span class="sxs-lookup"><span data-stu-id="72a0e-122">Get-AzureRmMetric</span></span>](/powershell/module/azurerm.insights/get-azurermmetric) | <span data-ttu-id="72a0e-123">顯示資料庫的大小使用量資訊。</span><span class="sxs-lookup"><span data-stu-id="72a0e-123">Shows the size usage information for the database.</span></span>|
| [<span data-ttu-id="72a0e-124">Add-AzureRMMetricAlertRule</span><span class="sxs-lookup"><span data-stu-id="72a0e-124">Add-AzureRMMetricAlertRule</span></span>](/powershell/module/azurerm.insights/add-azurermmetricalertrule) | <span data-ttu-id="72a0e-125">新增或更新以度量為基礎的警示規則。</span><span class="sxs-lookup"><span data-stu-id="72a0e-125">Adds or updates a metric-based alert rule.</span></span> |
| [<span data-ttu-id="72a0e-126">Set-AzureRmSqlElasticPool</span><span class="sxs-lookup"><span data-stu-id="72a0e-126">Set-AzureRmSqlElasticPool</span></span>](/powershell/module/azurerm.sql/set-azurermsqlelasticpool) | <span data-ttu-id="72a0e-127">更新彈性集區屬性</span><span class="sxs-lookup"><span data-stu-id="72a0e-127">Updates elastic pool properties</span></span> |
| [<span data-ttu-id="72a0e-128">Add-AzureRMMetricAlertRule</span><span class="sxs-lookup"><span data-stu-id="72a0e-128">Add-AzureRMMetricAlertRule</span></span>](/powershell/module/azurerm.insights/add-azurermmetricalertrule) | <span data-ttu-id="72a0e-129">設定警示規則以自動在日後監視 DTU。</span><span class="sxs-lookup"><span data-stu-id="72a0e-129">Sets an alert rule to automatically monitor DTUs in the future.</span></span> |
| [<span data-ttu-id="72a0e-130">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="72a0e-130">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="72a0e-131">刪除資源群組，包括所有的巢狀資源。</span><span class="sxs-lookup"><span data-stu-id="72a0e-131">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="72a0e-132">後續步驟</span><span class="sxs-lookup"><span data-stu-id="72a0e-132">Next steps</span></span>

<span data-ttu-id="72a0e-133">如需有關 Azure PowerShell 的詳細資訊，請參閱 [Azure PowerShell 文件](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="72a0e-133">For more information on the Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="72a0e-134">其他的 SQL Database PowerShell 指令碼範例可於 [Azure SQL Database PowerShell 指令碼](../sql-database-powershell-samples.md)中找到。</span><span class="sxs-lookup"><span data-stu-id="72a0e-134">Additional SQL Database PowerShell script samples can be found in the [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
