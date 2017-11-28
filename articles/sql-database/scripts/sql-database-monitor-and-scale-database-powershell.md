---
title: "PowerShell 範例 - 監視 - 調整 - 單一 SQL Database | Microsoft Docs"
description: "監視和調整單一 Azure SQL Database 的 Azure PowerShell 範例指令碼"
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
ms.openlocfilehash: 5d08335f4b1d6c5c6a120cbfb86ab2c62b79bb9f
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="use-powershell-to-monitor-and-scale-a-single-sql-database"></a><span data-ttu-id="06b70-103">使用 PowerShell 來監視和調整單一 SQL 資料庫</span><span class="sxs-lookup"><span data-stu-id="06b70-103">Use PowerShell to monitor and scale a single SQL database</span></span>

<span data-ttu-id="06b70-104">此 PowerShell 指令碼範例會監視資料庫的效能計量、將其調整為較高的效能等級，並對其中一個效能計量建立警示規則。</span><span class="sxs-lookup"><span data-stu-id="06b70-104">This PowerShell script example monitors the performance metrics of a database, scales it to a higher performance level, and creates an alert rule on one of the performance metrics.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="06b70-105">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="06b70-105">Sample script</span></span>

<span data-ttu-id="06b70-106">[!code-powershell[主要](../../../powershell_scripts/sql-database/monitor-and-scale-database/monitor-and-scale-database.ps1?highlight=13-14 "監視和調整單一 SQL Database")]</span><span class="sxs-lookup"><span data-stu-id="06b70-106">[!code-powershell[main](../../../powershell_scripts/sql-database/monitor-and-scale-database/monitor-and-scale-database.ps1?highlight=13-14 "Monitor and scale single SQL Database")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="06b70-107">清除部署</span><span class="sxs-lookup"><span data-stu-id="06b70-107">Clean up deployment</span></span>

<span data-ttu-id="06b70-108">在執行過指令碼範例之後，您可以使用下列命令來移除資源群組和所有與其相關聯的資源。</span><span class="sxs-lookup"><span data-stu-id="06b70-108">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="06b70-109">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="06b70-109">Script explanation</span></span>

<span data-ttu-id="06b70-110">此指令碼會使用下列命令。</span><span class="sxs-lookup"><span data-stu-id="06b70-110">This script uses the following commands.</span></span> <span data-ttu-id="06b70-111">下表中的每個命令都會連結至命令特定的文件。</span><span class="sxs-lookup"><span data-stu-id="06b70-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="06b70-112">命令</span><span class="sxs-lookup"><span data-stu-id="06b70-112">Command</span></span> | <span data-ttu-id="06b70-113">注意事項</span><span class="sxs-lookup"><span data-stu-id="06b70-113">Notes</span></span> |
|---|---|
 [<span data-ttu-id="06b70-114">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="06b70-114">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="06b70-115">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="06b70-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="06b70-116">New-AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="06b70-116">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="06b70-117">建立主機資料庫或彈性集區的邏輯伺服器。</span><span class="sxs-lookup"><span data-stu-id="06b70-117">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="06b70-118">Get-AzureRmMetric</span><span class="sxs-lookup"><span data-stu-id="06b70-118">Get-AzureRmMetric</span></span>](/powershell/module/azurerm.insights/get-azurermmetric) | <span data-ttu-id="06b70-119">顯示資料庫的大小使用量資訊。</span><span class="sxs-lookup"><span data-stu-id="06b70-119">Shows the size usage information for the database.</span></span>|
| [<span data-ttu-id="06b70-120">Set-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="06b70-120">Set-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/set-azurermsqldatabase) | <span data-ttu-id="06b70-121">更新資料庫屬性，或將資料庫移入、移出彈性集區或在彈性集區之間移動資料庫。</span><span class="sxs-lookup"><span data-stu-id="06b70-121">Updates database properties or moves a database into, out of, or between elastic pools.</span></span> |
| [<span data-ttu-id="06b70-122">Add-AzureRMMetricAlertRule</span><span class="sxs-lookup"><span data-stu-id="06b70-122">Add-AzureRMMetricAlertRule</span></span>](/powershell/module/azurerm.insights/add-azurermmetricalertrule) | <span data-ttu-id="06b70-123">設定警示規則以自動在日後監視 DTU。</span><span class="sxs-lookup"><span data-stu-id="06b70-123">Sets an alert rule to automatically monitor DTUs in the future.</span></span> |
| [<span data-ttu-id="06b70-124">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="06b70-124">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="06b70-125">刪除資源群組，包括所有的巢狀資源。</span><span class="sxs-lookup"><span data-stu-id="06b70-125">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="06b70-126">後續步驟</span><span class="sxs-lookup"><span data-stu-id="06b70-126">Next steps</span></span>

<span data-ttu-id="06b70-127">如需有關 Azure PowerShell 的詳細資訊，請參閱 [Azure PowerShell 文件](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="06b70-127">For more information on the Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="06b70-128">其他的 SQL Database PowerShell 指令碼範例可於 [Azure SQL Database PowerShell 指令碼](../sql-database-powershell-samples.md)中找到。</span><span class="sxs-lookup"><span data-stu-id="06b70-128">Additional SQL Database PowerShell script samples can be found in the [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
