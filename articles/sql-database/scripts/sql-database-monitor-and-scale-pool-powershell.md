---
title: "aaaPowerShell 範例監視器位小數位數 SQL 彈性集區-Azure SQL 資料庫 |Microsoft 文件"
description: "Azure PowerShell 範例指令碼 toomonitor 和小數位數 Azure SQL Database 中的 SQL 彈性集區"
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
ms.openlocfilehash: 149a45174ccb8072ea21753364196c7f98fd4101
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-toomonitor-and-scale-a-sql-elastic-pool-in-azure-sql-database"></a><span data-ttu-id="a5a3a-103">使用 PowerShell toomonitor 及擴充 Azure SQL Database 中的 SQL 彈性集區</span><span class="sxs-lookup"><span data-stu-id="a5a3a-103">Use PowerShell toomonitor and scale a SQL elastic pool in Azure SQL Database</span></span>

<span data-ttu-id="a5a3a-104">監視 hello 效能度量的彈性集區，這個 PowerShell 指令碼範例會調整它 tooa 較高的效能層級，以及 hello 效能度量的其中一個上建立警示規則。</span><span class="sxs-lookup"><span data-stu-id="a5a3a-104">This PowerShell script example monitors hello performance metrics of an elastic pool, scales it tooa higher performance level, and creates an alert rule on one of hello performance metrics.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="a5a3a-105">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="a5a3a-105">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/sql-database/monitor-and-scale-pool/monitor-and-scale-pool.ps1?highlight=16-17 "Monitor and scale single SQL Database")]

## <a name="clean-up-deployment"></a><span data-ttu-id="a5a3a-106">清除部署</span><span class="sxs-lookup"><span data-stu-id="a5a3a-106">Clean up deployment</span></span>

<span data-ttu-id="a5a3a-107">Hello 指令碼範例執行後，下列命令的 hello 可以使用的 tooremove hello 資源群組和與其相關聯的所有資源。</span><span class="sxs-lookup"><span data-stu-id="a5a3a-107">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="a5a3a-108">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="a5a3a-108">Script explanation</span></span>

<span data-ttu-id="a5a3a-109">此指令碼會使用下列命令的 hello。</span><span class="sxs-lookup"><span data-stu-id="a5a3a-109">This script uses hello following commands.</span></span> <span data-ttu-id="a5a3a-110">Hello 資料表連結 toocommand 特定文件中的每個命令。</span><span class="sxs-lookup"><span data-stu-id="a5a3a-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="a5a3a-111">命令</span><span class="sxs-lookup"><span data-stu-id="a5a3a-111">Command</span></span> | <span data-ttu-id="a5a3a-112">注意事項</span><span class="sxs-lookup"><span data-stu-id="a5a3a-112">Notes</span></span> |
|---|---|
 [<span data-ttu-id="a5a3a-113">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="a5a3a-113">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="a5a3a-114">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="a5a3a-114">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="a5a3a-115">New-AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="a5a3a-115">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="a5a3a-116">建立主機資料庫或彈性集區的邏輯伺服器。</span><span class="sxs-lookup"><span data-stu-id="a5a3a-116">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="a5a3a-117">New-AzureRmSqlElasticPool</span><span class="sxs-lookup"><span data-stu-id="a5a3a-117">New-AzureRmSqlElasticPool</span></span>](/powershell/module/azurerm.sql/new-azurermsqlelasticpool) | <span data-ttu-id="a5a3a-118">在邏輯伺服器內建立彈性集區。</span><span class="sxs-lookup"><span data-stu-id="a5a3a-118">Creates an elastic pool within a logical server.</span></span> |
| [<span data-ttu-id="a5a3a-119">New-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="a5a3a-119">New-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabase) | <span data-ttu-id="a5a3a-120">在邏輯伺服器中將資料庫建立為單一或集區的資料庫。</span><span class="sxs-lookup"><span data-stu-id="a5a3a-120">Creates a database in a logical server as a single or a pooled database.</span></span> |
| [<span data-ttu-id="a5a3a-121">Get-AzureRmMetric</span><span class="sxs-lookup"><span data-stu-id="a5a3a-121">Get-AzureRmMetric</span></span>](/powershell/module/azurerm.insights/get-azurermmetric) | <span data-ttu-id="a5a3a-122">顯示 hello hello 資料庫的大小使用量資訊。</span><span class="sxs-lookup"><span data-stu-id="a5a3a-122">Shows hello size usage information for hello database.</span></span>|
| [<span data-ttu-id="a5a3a-123">Add-AzureRMMetricAlertRule</span><span class="sxs-lookup"><span data-stu-id="a5a3a-123">Add-AzureRMMetricAlertRule</span></span>](/powershell/module/azurerm.insights/add-azurermmetricalertrule) | <span data-ttu-id="a5a3a-124">新增或更新以度量為基礎的警示規則。</span><span class="sxs-lookup"><span data-stu-id="a5a3a-124">Adds or updates a metric-based alert rule.</span></span> |
| [<span data-ttu-id="a5a3a-125">Set-AzureRmSqlElasticPool</span><span class="sxs-lookup"><span data-stu-id="a5a3a-125">Set-AzureRmSqlElasticPool</span></span>](/powershell/module/azurerm.sql/set-azurermsqlelasticpool) | <span data-ttu-id="a5a3a-126">更新彈性集區屬性</span><span class="sxs-lookup"><span data-stu-id="a5a3a-126">Updates elastic pool properties</span></span> |
| [<span data-ttu-id="a5a3a-127">Add-AzureRMMetricAlertRule</span><span class="sxs-lookup"><span data-stu-id="a5a3a-127">Add-AzureRMMetricAlertRule</span></span>](/powershell/module/azurerm.insights/add-azurermmetricalertrule) | <span data-ttu-id="a5a3a-128">設定的警示規則 tooautomatically 監視 Dtu hello 未來。</span><span class="sxs-lookup"><span data-stu-id="a5a3a-128">Sets an alert rule tooautomatically monitor DTUs in hello future.</span></span> |
| [<span data-ttu-id="a5a3a-129">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="a5a3a-129">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="a5a3a-130">刪除資源群組，包括所有的巢狀資源。</span><span class="sxs-lookup"><span data-stu-id="a5a3a-130">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="a5a3a-131">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a5a3a-131">Next steps</span></span>

<span data-ttu-id="a5a3a-132">如需有關 hello Azure PowerShell 的詳細資訊，請參閱[Azure PowerShell 文件](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="a5a3a-132">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="a5a3a-133">其他的 SQL 資料庫的 PowerShell 指令碼範例可以在 hello [Azure SQL Database 的 PowerShell 指令碼](../sql-database-powershell-samples.md)。</span><span class="sxs-lookup"><span data-stu-id="a5a3a-133">Additional SQL Database PowerShell script samples can be found in hello [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
