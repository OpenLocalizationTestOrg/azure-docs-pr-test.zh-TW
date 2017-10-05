---
title: "PowerShell 範例 - 作用中異地複寫 - 集區 Azure SQL Database | Microsoft Docs"
description: "為集區 Azure SQL Database 設定作用中異地複寫的 Azure PowerShell 範例指令碼"
services: sql-database
documentationcenter: sql-database
author: CarlRabeler
manager: jhubbard
editor: carlrab
tags: azure-service-management
ms.assetid: 
ms.service: sql-database
ms.custom: business continuity
ms.devlang: PowerShell
ms.topic: sample
ms.tgt_pltfrm: sql-database
ms.workload: database
ms.date: 07/25/2017
ms.author: carlrab
ms.openlocfilehash: c1a495a8f9960ed60d8589dee9615e075f80c77b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="use-powershell-to-configure-active-geo-replication-for-a-pooled-azure-sql-database"></a><span data-ttu-id="0148c-103">使用 PowerShell 為集區 Azure SQL Database 設定作用中異地複寫</span><span class="sxs-lookup"><span data-stu-id="0148c-103">Use PowerShell to configure active geo-replication for a pooled Azure SQL database</span></span>

<span data-ttu-id="0148c-104">此 PowerShell 指令碼範例為彈性集區中的 Azure SQL Database 設定作用中異地複寫，並將其容錯移轉到 Azure SQL Database 的次要複本。</span><span class="sxs-lookup"><span data-stu-id="0148c-104">This PowerShell script example configures active geo-replication for an Azure SQL database in an elastic pool and fails it over to the secondary replica of the Azure SQL database.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-scripts"></a><span data-ttu-id="0148c-105">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="0148c-105">Sample scripts</span></span>

<span data-ttu-id="0148c-106">[!code-powershell[主要](../../../powershell_scripts/sql-database/setup-geodr-and-failover-pool/setup-geodr-and-failover-pool.ps1?highlight=16-19 "為彈性集區設定作用中異地複寫")]</span><span class="sxs-lookup"><span data-stu-id="0148c-106">[!code-powershell[main](../../../powershell_scripts/sql-database/setup-geodr-and-failover-pool/setup-geodr-and-failover-pool.ps1?highlight=16-19 "Set up active geo-replication for elastic pool")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="0148c-107">清除部署</span><span class="sxs-lookup"><span data-stu-id="0148c-107">Clean up deployment</span></span>

<span data-ttu-id="0148c-108">在執行過指令碼範例之後，您可以使用下列命令來移除資源群組和所有與其相關聯的資源。</span><span class="sxs-lookup"><span data-stu-id="0148c-108">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myPrimaryResourceGroup"
Remove-AzureRmResourceGroup -ResourceGroupName "mySecondaryResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="0148c-109">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="0148c-109">Script explanation</span></span>

<span data-ttu-id="0148c-110">此指令碼會使用下列命令。</span><span class="sxs-lookup"><span data-stu-id="0148c-110">This script uses the following commands.</span></span> <span data-ttu-id="0148c-111">下表中的每個命令都會連結至命令特定的文件。</span><span class="sxs-lookup"><span data-stu-id="0148c-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="0148c-112">命令</span><span class="sxs-lookup"><span data-stu-id="0148c-112">Command</span></span> | <span data-ttu-id="0148c-113">注意事項</span><span class="sxs-lookup"><span data-stu-id="0148c-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="0148c-114">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="0148c-114">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="0148c-115">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="0148c-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="0148c-116">New-AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="0148c-116">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="0148c-117">建立主機資料庫或彈性集區的邏輯伺服器。</span><span class="sxs-lookup"><span data-stu-id="0148c-117">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="0148c-118">New-AzureRmSqlElasticPool</span><span class="sxs-lookup"><span data-stu-id="0148c-118">New-AzureRmSqlElasticPool</span></span>](/powershell/module/azurerm.sql/new-azurermsqlelasticpool) | <span data-ttu-id="0148c-119">在邏輯伺服器內建立彈性集區。</span><span class="sxs-lookup"><span data-stu-id="0148c-119">Creates an elastic pool within a logical server.</span></span> |
| [<span data-ttu-id="0148c-120">New-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="0148c-120">New-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabase) | <span data-ttu-id="0148c-121">在邏輯伺服器中將資料庫建立為單一或集區的資料庫。</span><span class="sxs-lookup"><span data-stu-id="0148c-121">Creates a database in a logical server as a single or a pooled database.</span></span> |
| [<span data-ttu-id="0148c-122">Set-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="0148c-122">Set-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/set-azurermsqldatabase) | <span data-ttu-id="0148c-123">更新資料庫屬性，或將資料庫移入、移出彈性集區或在彈性集區之間移動資料庫。</span><span class="sxs-lookup"><span data-stu-id="0148c-123">Updates database properties or moves a database into, out of, or between elastic pools.</span></span> |
| [<span data-ttu-id="0148c-124">New-AzureRmSqlDatabaseSecondary</span><span class="sxs-lookup"><span data-stu-id="0148c-124">New-AzureRmSqlDatabaseSecondary</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabasesecondary)| <span data-ttu-id="0148c-125">針對現有資料庫建立次要資料庫並開始資料複寫。</span><span class="sxs-lookup"><span data-stu-id="0148c-125">Creates a secondary database for an existing database and starts data replication.</span></span> |
| [<span data-ttu-id="0148c-126">Get-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="0148c-126">Get-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/get-azurermsqldatabase)| <span data-ttu-id="0148c-127">取得一或多個資料庫。</span><span class="sxs-lookup"><span data-stu-id="0148c-127">Gets one or more databases.</span></span> |
| [<span data-ttu-id="0148c-128">Set-AzureRmSqlDatabaseSecondary</span><span class="sxs-lookup"><span data-stu-id="0148c-128">Set-AzureRmSqlDatabaseSecondary</span></span>](/powershell/module/azurerm.sql/set-azurermsqldatabasesecondary)| <span data-ttu-id="0148c-129">將次要資料庫切換為主要資料庫以便開始容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="0148c-129">Switches a secondary database to be primary in order to initiate failover.</span></span>|
| [<span data-ttu-id="0148c-130">Get-AzureRmSqlDatabaseReplicationLink</span><span class="sxs-lookup"><span data-stu-id="0148c-130">Get-AzureRmSqlDatabaseReplicationLink</span></span>](/powershell/module/azurerm.sql/get-azurermsqldatabasereplicationlink) | <span data-ttu-id="0148c-131">取得 Azure SQL Database 和資源群組或 SQL Server 之間的異地複寫連結。</span><span class="sxs-lookup"><span data-stu-id="0148c-131">Gets the geo-replication links between an Azure SQL Database and a resource group or SQL Server.</span></span> |
| [<span data-ttu-id="0148c-132">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="0148c-132">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="0148c-133">刪除資源群組，包括所有的巢狀資源。</span><span class="sxs-lookup"><span data-stu-id="0148c-133">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="0148c-134">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0148c-134">Next steps</span></span>

<span data-ttu-id="0148c-135">如需有關 Azure PowerShell 的詳細資訊，請參閱 [Azure PowerShell 文件](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="0148c-135">For more information on the Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="0148c-136">其他的 SQL Database PowerShell 指令碼範例可於 [Azure SQL Database PowerShell 指令碼](../sql-database-powershell-samples.md)中找到。</span><span class="sxs-lookup"><span data-stu-id="0148c-136">Additional SQL Database PowerShell script samples can be found in the [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
