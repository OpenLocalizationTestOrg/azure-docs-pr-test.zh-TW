---
title: "aaaPowerShell 範例監視器位小數位數單一 Azure SQL 資料庫 |Microsoft 文件"
description: "Azure PowerShell 範例指令碼 toomonitor 和小數位數單一 Azure SQL 資料庫"
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
ms.openlocfilehash: bd8f880fb47b1360ae4962d2b039faa742de258e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-toomonitor-and-scale-a-single-sql-database"></a><span data-ttu-id="41cf0-103">使用 PowerShell toomonitor 並縮放單一的 SQL 資料庫</span><span class="sxs-lookup"><span data-stu-id="41cf0-103">Use PowerShell toomonitor and scale a single SQL database</span></span>

<span data-ttu-id="41cf0-104">監視 hello 效能度量資訊的資料庫，這個 PowerShell 指令碼範例會調整它 tooa 較高的效能層級，以及 hello 效能度量的其中一個上建立警示規則。</span><span class="sxs-lookup"><span data-stu-id="41cf0-104">This PowerShell script example monitors hello performance metrics of a database, scales it tooa higher performance level, and creates an alert rule on one of hello performance metrics.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="41cf0-105">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="41cf0-105">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/sql-database/monitor-and-scale-database/monitor-and-scale-database.ps1?highlight=13-14 "Monitor and scale single SQL Database")]

## <a name="clean-up-deployment"></a><span data-ttu-id="41cf0-106">清除部署</span><span class="sxs-lookup"><span data-stu-id="41cf0-106">Clean up deployment</span></span>

<span data-ttu-id="41cf0-107">Hello 指令碼範例執行後，下列命令的 hello 可以使用的 tooremove hello 資源群組和與其相關聯的所有資源。</span><span class="sxs-lookup"><span data-stu-id="41cf0-107">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="41cf0-108">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="41cf0-108">Script explanation</span></span>

<span data-ttu-id="41cf0-109">此指令碼會使用下列命令的 hello。</span><span class="sxs-lookup"><span data-stu-id="41cf0-109">This script uses hello following commands.</span></span> <span data-ttu-id="41cf0-110">Hello 資料表連結 toocommand 特定文件中的每個命令。</span><span class="sxs-lookup"><span data-stu-id="41cf0-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="41cf0-111">命令</span><span class="sxs-lookup"><span data-stu-id="41cf0-111">Command</span></span> | <span data-ttu-id="41cf0-112">注意事項</span><span class="sxs-lookup"><span data-stu-id="41cf0-112">Notes</span></span> |
|---|---|
 [<span data-ttu-id="41cf0-113">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="41cf0-113">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="41cf0-114">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="41cf0-114">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="41cf0-115">New-AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="41cf0-115">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="41cf0-116">建立主機資料庫或彈性集區的邏輯伺服器。</span><span class="sxs-lookup"><span data-stu-id="41cf0-116">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="41cf0-117">Get-AzureRmMetric</span><span class="sxs-lookup"><span data-stu-id="41cf0-117">Get-AzureRmMetric</span></span>](/powershell/module/azurerm.insights/get-azurermmetric) | <span data-ttu-id="41cf0-118">顯示 hello hello 資料庫的大小使用量資訊。</span><span class="sxs-lookup"><span data-stu-id="41cf0-118">Shows hello size usage information for hello database.</span></span>|
| [<span data-ttu-id="41cf0-119">Set-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="41cf0-119">Set-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/set-azurermsqldatabase) | <span data-ttu-id="41cf0-120">更新資料庫屬性，或將資料庫移入、移出彈性集區或在彈性集區之間移動資料庫。</span><span class="sxs-lookup"><span data-stu-id="41cf0-120">Updates database properties or moves a database into, out of, or between elastic pools.</span></span> |
| [<span data-ttu-id="41cf0-121">Add-AzureRMMetricAlertRule</span><span class="sxs-lookup"><span data-stu-id="41cf0-121">Add-AzureRMMetricAlertRule</span></span>](/powershell/module/azurerm.insights/add-azurermmetricalertrule) | <span data-ttu-id="41cf0-122">設定的警示規則 tooautomatically 監視 Dtu hello 未來。</span><span class="sxs-lookup"><span data-stu-id="41cf0-122">Sets an alert rule tooautomatically monitor DTUs in hello future.</span></span> |
| [<span data-ttu-id="41cf0-123">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="41cf0-123">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="41cf0-124">刪除資源群組，包括所有的巢狀資源。</span><span class="sxs-lookup"><span data-stu-id="41cf0-124">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="41cf0-125">後續步驟</span><span class="sxs-lookup"><span data-stu-id="41cf0-125">Next steps</span></span>

<span data-ttu-id="41cf0-126">如需有關 hello Azure PowerShell 的詳細資訊，請參閱[Azure PowerShell 文件](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="41cf0-126">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="41cf0-127">其他的 SQL 資料庫的 PowerShell 指令碼範例可以在 hello [Azure SQL Database 的 PowerShell 指令碼](../sql-database-powershell-samples.md)。</span><span class="sxs-lookup"><span data-stu-id="41cf0-127">Additional SQL Database PowerShell script samples can be found in hello [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
