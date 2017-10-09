---
title: "aaaPowerShell 範例移動 Azure SQL database-SQL 彈性集區 |Microsoft 文件"
description: "Azure PowerShell 範例指令碼 toomove SQL 資料庫之間使用 PowerShell 的彈性集區"
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
ms.openlocfilehash: 501e82ce93a31264d0625fb0243b4e44dcb2d007
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-toocreate-elastic-pools-and-move-databases-between-elastic-pools"></a><span data-ttu-id="6545c-103">使用 PowerShell toocreate 彈性集區和彈性集區之間移動資料庫</span><span class="sxs-lookup"><span data-stu-id="6545c-103">Use PowerShell toocreate elastic pools and move databases between elastic pools</span></span>

<span data-ttu-id="6545c-104">這個 PowerShell 指令碼範例會建立兩個彈性集區和將資料庫從一個彈性集區移到另一個彈性集區，並再將資料庫移超出彈性集區 tooa 單一資料庫效能層級。</span><span class="sxs-lookup"><span data-stu-id="6545c-104">This PowerShell script example creates two elastic pools and moves a database from one elastic pool into another elastic pool, and then moves a database out of an elastic pool tooa single database performance level.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="6545c-105">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="6545c-105">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/sql-database/move-database-between-pools-and-standalone/move-database-between-pools-and-standalone.ps1?highlight=17-18 "Move database between pools")]

## <a name="clean-up-deployment"></a><span data-ttu-id="6545c-106">清除部署</span><span class="sxs-lookup"><span data-stu-id="6545c-106">Clean up deployment</span></span>

<span data-ttu-id="6545c-107">Hello 指令碼範例執行後，下列命令的 hello 可以使用的 tooremove hello 資源群組和與其相關聯的所有資源。</span><span class="sxs-lookup"><span data-stu-id="6545c-107">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="6545c-108">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="6545c-108">Script explanation</span></span>

<span data-ttu-id="6545c-109">此指令碼會使用下列命令的 hello。</span><span class="sxs-lookup"><span data-stu-id="6545c-109">This script uses hello following commands.</span></span> <span data-ttu-id="6545c-110">Hello 資料表連結 toocommand 特定文件中的每個命令。</span><span class="sxs-lookup"><span data-stu-id="6545c-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="6545c-111">命令</span><span class="sxs-lookup"><span data-stu-id="6545c-111">Command</span></span> | <span data-ttu-id="6545c-112">注意事項</span><span class="sxs-lookup"><span data-stu-id="6545c-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="6545c-113">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="6545c-113">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="6545c-114">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="6545c-114">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="6545c-115">New-AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="6545c-115">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="6545c-116">建立主機資料庫或彈性集區的邏輯伺服器。</span><span class="sxs-lookup"><span data-stu-id="6545c-116">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="6545c-117">New-AzureRmSqlElasticPool</span><span class="sxs-lookup"><span data-stu-id="6545c-117">New-AzureRmSqlElasticPool</span></span>](/powershell/module/azurerm.sql/new-azurermsqlelasticpool) | <span data-ttu-id="6545c-118">在邏輯伺服器內建立彈性集區。</span><span class="sxs-lookup"><span data-stu-id="6545c-118">Creates an elastic pool within a logical server.</span></span> |
| [<span data-ttu-id="6545c-119">New-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="6545c-119">New-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabase) | <span data-ttu-id="6545c-120">在邏輯伺服器中將資料庫建立為單一或集區的資料庫。</span><span class="sxs-lookup"><span data-stu-id="6545c-120">Creates a database in a logical server as a single or a pooled database.</span></span> |
| [<span data-ttu-id="6545c-121">Set-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="6545c-121">Set-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/set-azurermsqldatabase) | <span data-ttu-id="6545c-122">更新資料庫屬性，或將資料庫移入、移出彈性集區或在彈性集區之間移動資料庫。</span><span class="sxs-lookup"><span data-stu-id="6545c-122">Updates database properties or moves a database into, out of, or between elastic pools.</span></span> |
| [<span data-ttu-id="6545c-123">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="6545c-123">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="6545c-124">刪除資源群組，包括所有的巢狀資源。</span><span class="sxs-lookup"><span data-stu-id="6545c-124">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="6545c-125">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6545c-125">Next steps</span></span>

<span data-ttu-id="6545c-126">如需有關 hello Azure PowerShell 的詳細資訊，請參閱[Azure PowerShell 文件](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="6545c-126">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="6545c-127">其他的 SQL 資料庫的 PowerShell 指令碼範例可以在 hello [Azure SQL Database 的 PowerShell 指令碼](../sql-database-powershell-samples.md)。</span><span class="sxs-lookup"><span data-stu-id="6545c-127">Additional SQL Database PowerShell script samples can be found in hello [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
