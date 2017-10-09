---
title: "aaaPowerShell 範例還原備份的 Azure SQL 資料庫 |Microsoft 文件"
description: "Azure PowerShell 範例指令碼 toorestore 從異地備援備份 Azure SQL database"
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
ms.openlocfilehash: 68becb89e8a8680aa2efc3de8ad947e674c5fc35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-toorestore-an-azure-sql-database-from-backups"></a><span data-ttu-id="ea5fe-103">使用 PowerShell toorestore Azure SQL database 備份</span><span class="sxs-lookup"><span data-stu-id="ea5fe-103">Use PowerShell toorestore an Azure SQL database from backups</span></span>

<span data-ttu-id="ea5fe-104">這個 PowerShell 指令碼範例從異地備援備份還原 Azure SQL database、 還原已刪除的 Azure SQL database tooits 最新備份，並會還原 Azure SQL database tooa 特定點。</span><span class="sxs-lookup"><span data-stu-id="ea5fe-104">This PowerShell script example restores an Azure SQL database from a geo-redundant backup, restores a deleted Azure SQL database tooits latest backup, and restores an Azure SQL database tooa specific point in time.</span></span>  

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="ea5fe-105">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="ea5fe-105">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/sql-database/restore-database/restore-database.ps1?highlight=17-18 "Create SQL Database")]

## <a name="clean-up-deployment"></a><span data-ttu-id="ea5fe-106">清除部署</span><span class="sxs-lookup"><span data-stu-id="ea5fe-106">Clean up deployment</span></span>

<span data-ttu-id="ea5fe-107">Hello 指令碼範例執行後，下列命令的 hello 可以使用的 tooremove hello 資源群組和與其相關聯的所有資源。</span><span class="sxs-lookup"><span data-stu-id="ea5fe-107">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="ea5fe-108">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="ea5fe-108">Script explanation</span></span>

<span data-ttu-id="ea5fe-109">此指令碼會使用下列命令的 hello。</span><span class="sxs-lookup"><span data-stu-id="ea5fe-109">This script uses hello following commands.</span></span> <span data-ttu-id="ea5fe-110">Hello 資料表連結 toocommand 特定文件中的每個命令。</span><span class="sxs-lookup"><span data-stu-id="ea5fe-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="ea5fe-111">命令</span><span class="sxs-lookup"><span data-stu-id="ea5fe-111">Command</span></span> | <span data-ttu-id="ea5fe-112">注意事項</span><span class="sxs-lookup"><span data-stu-id="ea5fe-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="ea5fe-113">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="ea5fe-113">New-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/new-azurermresourcegroup) | <span data-ttu-id="ea5fe-114">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="ea5fe-114">Creates a resource group in which all resources are stored.</span></span> | [<span data-ttu-id="ea5fe-115">New-AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="ea5fe-115">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="ea5fe-116">建立主機資料庫或彈性集區的邏輯伺服器。</span><span class="sxs-lookup"><span data-stu-id="ea5fe-116">Creates a logical server that hosts a database or elastic pool.</span></span> | 
| [<span data-ttu-id="ea5fe-117">New-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="ea5fe-117">New-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabase) | <span data-ttu-id="ea5fe-118">在邏輯伺服器中將資料庫建立為單一或集區的資料庫。</span><span class="sxs-lookup"><span data-stu-id="ea5fe-118">Creates a database in a logical server as a single or a pooled database.</span></span> |
[<span data-ttu-id="ea5fe-119">Get-AzureRmSqlDatabaseGeoBackup</span><span class="sxs-lookup"><span data-stu-id="ea5fe-119">Get-AzureRmSqlDatabaseGeoBackup</span></span>](/powershell/module/azurerm.sql/get-azurermsqldatabasegeobackup) | <span data-ttu-id="ea5fe-120">取得資料庫的異地備援備份。</span><span class="sxs-lookup"><span data-stu-id="ea5fe-120">Gets a geo-redundant backup of a database.</span></span> |
| [<span data-ttu-id="ea5fe-121">Restore-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="ea5fe-121">Restore-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/restore-azurermsqldatabase) | <span data-ttu-id="ea5fe-122">還原 SQL Database。</span><span class="sxs-lookup"><span data-stu-id="ea5fe-122">Restores a SQL database.</span></span> |
|[<span data-ttu-id="ea5fe-123">Remove-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="ea5fe-123">Remove-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/remove-azurermsqldatabase) | <span data-ttu-id="ea5fe-124">移除 Azure SQL Database。</span><span class="sxs-lookup"><span data-stu-id="ea5fe-124">Removes an Azure SQL database.</span></span> |
| [<span data-ttu-id="ea5fe-125">Get-AzureRmSqlDeletedDatabaseBackup</span><span class="sxs-lookup"><span data-stu-id="ea5fe-125">Get-AzureRmSqlDeletedDatabaseBackup</span></span>](/powershell/module/azurerm.sql/get-azurermsqldeleteddatabasebackup) | <span data-ttu-id="ea5fe-126">取得可還原的已刪除資料庫。</span><span class="sxs-lookup"><span data-stu-id="ea5fe-126">Gets a deleted database that you can restore.</span></span> |
| [<span data-ttu-id="ea5fe-127">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="ea5fe-127">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="ea5fe-128">刪除資源群組，包括所有的巢狀資源。</span><span class="sxs-lookup"><span data-stu-id="ea5fe-128">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="ea5fe-129">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ea5fe-129">Next steps</span></span>

<span data-ttu-id="ea5fe-130">如需有關 hello Azure PowerShell 的詳細資訊，請參閱[Azure PowerShell 文件](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="ea5fe-130">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="ea5fe-131">其他的 SQL 資料庫的 PowerShell 指令碼範例可以在 hello [Azure SQL Database 的 PowerShell 指令碼](../sql-database-powershell-samples.md)。</span><span class="sxs-lookup"><span data-stu-id="ea5fe-131">Additional SQL Database PowerShell script samples can be found in hello [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
