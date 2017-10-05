---
title: "PowerShell 範例 - 作用中異地複寫 - 單一 Azure SQL Database | Microsoft Docs"
description: "為單一 Azure SQL Database 設定作用中異地複寫的 Azure PowerShell 範例指令碼"
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
ms.openlocfilehash: b25bc02acda7905cd4c08bbafee1d9b29907d332
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="use-powershell-to-configure-active-geo-replication-for-a-single-azure-sql-database"></a><span data-ttu-id="8a3a9-103">使用 PowerShell 為單一 Azure SQL Database 設定作用中異地複寫</span><span class="sxs-lookup"><span data-stu-id="8a3a9-103">Use PowerShell to configure active geo-replication for a single Azure SQL database</span></span>

<span data-ttu-id="8a3a9-104">此 PowerShell 指令碼範例為單一 Azure SQL Database 設定作用中異地複寫，並將其容錯移轉到 Azure SQL Database 的次要複本。</span><span class="sxs-lookup"><span data-stu-id="8a3a9-104">This PowerShell script example configures active geo-replication for a single Azure SQL database and fails it over to a secondary replica of the Azure SQL database.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-scripts"></a><span data-ttu-id="8a3a9-105">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="8a3a9-105">Sample scripts</span></span>

<span data-ttu-id="8a3a9-106">[!code-powershell[主要](../../../powershell_scripts/sql-database/setup-geodr-and-failover-database/setup-geodr-and-failover-database.ps1?highlight=17-20 "為單一資料庫設定作用中異地複寫")]</span><span class="sxs-lookup"><span data-stu-id="8a3a9-106">[!code-powershell[main](../../../powershell_scripts/sql-database/setup-geodr-and-failover-database/setup-geodr-and-failover-database.ps1?highlight=17-20 "Set up active geo-replication for single database")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="8a3a9-107">清除部署</span><span class="sxs-lookup"><span data-stu-id="8a3a9-107">Clean up deployment</span></span>

<span data-ttu-id="8a3a9-108">在執行過指令碼範例之後，您可以使用下列命令來移除資源群組和所有與其相關聯的資源。</span><span class="sxs-lookup"><span data-stu-id="8a3a9-108">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myPrimaryResourceGroup"
Remove-AzureRmResourceGroup -ResourceGroupName "mySecondaryResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="8a3a9-109">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="8a3a9-109">Script explanation</span></span>

<span data-ttu-id="8a3a9-110">此指令碼會使用下列命令。</span><span class="sxs-lookup"><span data-stu-id="8a3a9-110">This script uses the following commands.</span></span> <span data-ttu-id="8a3a9-111">下表中的每個命令都會連結至命令特定的文件。</span><span class="sxs-lookup"><span data-stu-id="8a3a9-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="8a3a9-112">命令</span><span class="sxs-lookup"><span data-stu-id="8a3a9-112">Command</span></span> | <span data-ttu-id="8a3a9-113">注意事項</span><span class="sxs-lookup"><span data-stu-id="8a3a9-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="8a3a9-114">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="8a3a9-114">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="8a3a9-115">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="8a3a9-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="8a3a9-116">New-AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="8a3a9-116">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="8a3a9-117">建立主機資料庫或彈性集區的邏輯伺服器。</span><span class="sxs-lookup"><span data-stu-id="8a3a9-117">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="8a3a9-118">New-AzureRmSqlElasticPool</span><span class="sxs-lookup"><span data-stu-id="8a3a9-118">New-AzureRmSqlElasticPool</span></span>](/powershell/module/azurerm.sql/new-azurermsqlelasticpool) | <span data-ttu-id="8a3a9-119">在邏輯伺服器內建立彈性集區。</span><span class="sxs-lookup"><span data-stu-id="8a3a9-119">Creates an elastic pool within a logical server.</span></span> |
| [<span data-ttu-id="8a3a9-120">Set-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="8a3a9-120">Set-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/set-azurermsqldatabase) | <span data-ttu-id="8a3a9-121">更新資料庫屬性，或將資料庫移入、移出彈性集區或在彈性集區之間移動資料庫。</span><span class="sxs-lookup"><span data-stu-id="8a3a9-121">Updates database properties or moves a database into, out of, or between elastic pools.</span></span> |
| [<span data-ttu-id="8a3a9-122">New-AzureRmSqlDatabaseSecondary</span><span class="sxs-lookup"><span data-stu-id="8a3a9-122">New-AzureRmSqlDatabaseSecondary</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabasesecondary)| <span data-ttu-id="8a3a9-123">針對現有資料庫建立次要資料庫並開始資料複寫。</span><span class="sxs-lookup"><span data-stu-id="8a3a9-123">Creates a secondary database for an existing database and starts data replication.</span></span> |
| [<span data-ttu-id="8a3a9-124">Get-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="8a3a9-124">Get-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/get-azurermsqldatabase)| <span data-ttu-id="8a3a9-125">取得一或多個資料庫。</span><span class="sxs-lookup"><span data-stu-id="8a3a9-125">Gets one or more databases.</span></span> |
| [<span data-ttu-id="8a3a9-126">Set-AzureRmSqlDatabaseSecondary</span><span class="sxs-lookup"><span data-stu-id="8a3a9-126">Set-AzureRmSqlDatabaseSecondary</span></span>](/powershell/module/azurerm.sql/set-azurermsqldatabasesecondary)| <span data-ttu-id="8a3a9-127">將次要資料庫切換為主要資料庫以開始容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="8a3a9-127">Switches a secondary database to be primary to initiate failover.</span></span>|
| [<span data-ttu-id="8a3a9-128">Get-AzureRmSqlDatabaseReplicationLink</span><span class="sxs-lookup"><span data-stu-id="8a3a9-128">Get-AzureRmSqlDatabaseReplicationLink</span></span>](/powershell/module/azurerm.sql/get-azurermsqldatabasereplicationlink) | <span data-ttu-id="8a3a9-129">取得 Azure SQL Database 和資源群組或 SQL Server 之間的異地複寫連結。</span><span class="sxs-lookup"><span data-stu-id="8a3a9-129">Gets the geo-replication links between an Azure SQL Database and a resource group or SQL Server.</span></span> |
| [<span data-ttu-id="8a3a9-130">Remove-AzureRmSqlDatabaseSecondary</span><span class="sxs-lookup"><span data-stu-id="8a3a9-130">Remove-AzureRmSqlDatabaseSecondary</span></span>](/powershell/module/azurerm.sql/remove-azurermsqldatabasesecondary) | <span data-ttu-id="8a3a9-131">終止 SQL Database 和指定次要資料庫間的資料複寫。</span><span class="sxs-lookup"><span data-stu-id="8a3a9-131">Terminates data replication between a SQL Database and the specified secondary database.</span></span> |
| [<span data-ttu-id="8a3a9-132">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="8a3a9-132">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="8a3a9-133">刪除資源群組，包括所有的巢狀資源。</span><span class="sxs-lookup"><span data-stu-id="8a3a9-133">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="8a3a9-134">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8a3a9-134">Next steps</span></span>

<span data-ttu-id="8a3a9-135">如需有關 Azure PowerShell 的詳細資訊，請參閱 [Azure PowerShell 文件](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="8a3a9-135">For more information on the Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="8a3a9-136">其他的 SQL Database PowerShell 指令碼範例可於 [Azure SQL Database PowerShell 指令碼](../sql-database-powershell-samples.md)中找到。</span><span class="sxs-lookup"><span data-stu-id="8a3a9-136">Additional SQL Database PowerShell script samples can be found in the [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
