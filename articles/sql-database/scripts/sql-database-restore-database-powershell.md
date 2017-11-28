---
title: "PowerShell 範例 - 備份 - 還原 - Azure SQL Database | Microsoft Docs"
description: "從異地備援備份還原 Azure SQL Database 的 Azure PowerShell 範例指令碼"
services: sql-database
documentationcenter: sql-database
author: janeng
manager: jstrauss
editor: carlrab
tags: azure-service-management
ms.assetid: 
ms.service: sql-database
ms.custom: business continuity
ms.devlang: PowerShell
ms.topic: sample
ms.tgt_pltfrm: sql-database
ms.workload: database
ms.date: 06/23/2017
ms.author: janeng
ms.openlocfilehash: ae1d0c828ae1e7e1e7e07dcc7d6157187a3859d3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="use-powershell-to-restore-an-azure-sql-database-from-backups"></a><span data-ttu-id="e8fda-103">使用 PowerShell 從備份還原 Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="e8fda-103">Use PowerShell to restore an Azure SQL database from backups</span></span>

<span data-ttu-id="e8fda-104">此 PowerShell 指令碼範例會從異地備援備份還原 Azure SQL Database、將已刪除的 Azure SQL Database 還原為最新的備份，以及將 Azure SQL Database 還原到特定時間點。</span><span class="sxs-lookup"><span data-stu-id="e8fda-104">This PowerShell script example restores an Azure SQL database from a geo-redundant backup, restores a deleted Azure SQL database to its latest backup, and restores an Azure SQL database to a specific point in time.</span></span>  

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="e8fda-105">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="e8fda-105">Sample script</span></span>

<span data-ttu-id="e8fda-106">[!code-powershell[主要](../../../powershell_scripts/sql-database/restore-database/restore-database.ps1?highlight=17-18 "建立 SQL Database")]</span><span class="sxs-lookup"><span data-stu-id="e8fda-106">[!code-powershell[main](../../../powershell_scripts/sql-database/restore-database/restore-database.ps1?highlight=17-18 "Create SQL Database")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="e8fda-107">清除部署</span><span class="sxs-lookup"><span data-stu-id="e8fda-107">Clean up deployment</span></span>

<span data-ttu-id="e8fda-108">在執行過指令碼範例之後，您可以使用下列命令來移除資源群組和所有與其相關聯的資源。</span><span class="sxs-lookup"><span data-stu-id="e8fda-108">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="e8fda-109">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="e8fda-109">Script explanation</span></span>

<span data-ttu-id="e8fda-110">此指令碼會使用下列命令。</span><span class="sxs-lookup"><span data-stu-id="e8fda-110">This script uses the following commands.</span></span> <span data-ttu-id="e8fda-111">下表中的每個命令都會連結至命令特定的文件。</span><span class="sxs-lookup"><span data-stu-id="e8fda-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="e8fda-112">命令</span><span class="sxs-lookup"><span data-stu-id="e8fda-112">Command</span></span> | <span data-ttu-id="e8fda-113">注意事項</span><span class="sxs-lookup"><span data-stu-id="e8fda-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="e8fda-114">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="e8fda-114">New-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/new-azurermresourcegroup) | <span data-ttu-id="e8fda-115">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="e8fda-115">Creates a resource group in which all resources are stored.</span></span> | [<span data-ttu-id="e8fda-116">New-AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="e8fda-116">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="e8fda-117">建立主機資料庫或彈性集區的邏輯伺服器。</span><span class="sxs-lookup"><span data-stu-id="e8fda-117">Creates a logical server that hosts a database or elastic pool.</span></span> | 
| [<span data-ttu-id="e8fda-118">New-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="e8fda-118">New-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabase) | <span data-ttu-id="e8fda-119">在邏輯伺服器中將資料庫建立為單一或集區的資料庫。</span><span class="sxs-lookup"><span data-stu-id="e8fda-119">Creates a database in a logical server as a single or a pooled database.</span></span> |
[<span data-ttu-id="e8fda-120">Get-AzureRmSqlDatabaseGeoBackup</span><span class="sxs-lookup"><span data-stu-id="e8fda-120">Get-AzureRmSqlDatabaseGeoBackup</span></span>](/powershell/module/azurerm.sql/get-azurermsqldatabasegeobackup) | <span data-ttu-id="e8fda-121">取得資料庫的異地備援備份。</span><span class="sxs-lookup"><span data-stu-id="e8fda-121">Gets a geo-redundant backup of a database.</span></span> |
| [<span data-ttu-id="e8fda-122">Restore-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="e8fda-122">Restore-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/restore-azurermsqldatabase) | <span data-ttu-id="e8fda-123">還原 SQL Database。</span><span class="sxs-lookup"><span data-stu-id="e8fda-123">Restores a SQL database.</span></span> |
|[<span data-ttu-id="e8fda-124">Remove-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="e8fda-124">Remove-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/remove-azurermsqldatabase) | <span data-ttu-id="e8fda-125">移除 Azure SQL Database。</span><span class="sxs-lookup"><span data-stu-id="e8fda-125">Removes an Azure SQL database.</span></span> |
| [<span data-ttu-id="e8fda-126">Get-AzureRmSqlDeletedDatabaseBackup</span><span class="sxs-lookup"><span data-stu-id="e8fda-126">Get-AzureRmSqlDeletedDatabaseBackup</span></span>](/powershell/module/azurerm.sql/get-azurermsqldeleteddatabasebackup) | <span data-ttu-id="e8fda-127">取得可還原的已刪除資料庫。</span><span class="sxs-lookup"><span data-stu-id="e8fda-127">Gets a deleted database that you can restore.</span></span> |
| [<span data-ttu-id="e8fda-128">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="e8fda-128">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="e8fda-129">刪除資源群組，包括所有的巢狀資源。</span><span class="sxs-lookup"><span data-stu-id="e8fda-129">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="e8fda-130">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e8fda-130">Next steps</span></span>

<span data-ttu-id="e8fda-131">如需有關 Azure PowerShell 的詳細資訊，請參閱 [Azure PowerShell 文件](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="e8fda-131">For more information on the Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="e8fda-132">其他的 SQL Database PowerShell 指令碼範例可於 [Azure SQL Database PowerShell 指令碼](../sql-database-powershell-samples.md)中找到。</span><span class="sxs-lookup"><span data-stu-id="e8fda-132">Additional SQL Database PowerShell script samples can be found in the [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
