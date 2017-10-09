---
title: "aaaPowerShell 範例作用中地理複寫共用 Azure SQL 資料庫 |Microsoft 文件"
description: "Azure PowerShell 範例指令碼設定為管理的集區的 Azure SQL database 的作用中地理複寫 tooset"
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
ms.openlocfilehash: 9d183f08dcc07ba864e42fe70a562fef8bd572f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-tooconfigure-active-geo-replication-for-a-pooled-azure-sql-database"></a><span data-ttu-id="cce9b-103">使用 PowerShell tooconfigure 作用中異地複寫管理的集區的 Azure SQL database</span><span class="sxs-lookup"><span data-stu-id="cce9b-103">Use PowerShell tooconfigure active geo-replication for a pooled Azure SQL database</span></span>

<span data-ttu-id="cce9b-104">這個 PowerShell 指令碼範例會為 Azure SQL database 的作用中地理複寫設定彈性集區中，並容錯 toohello hello Azure SQL database 的次要複本。</span><span class="sxs-lookup"><span data-stu-id="cce9b-104">This PowerShell script example configures active geo-replication for an Azure SQL database in an elastic pool and fails it over toohello secondary replica of hello Azure SQL database.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-scripts"></a><span data-ttu-id="cce9b-105">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="cce9b-105">Sample scripts</span></span>

[!code-powershell[main](../../../powershell_scripts/sql-database/setup-geodr-and-failover-pool/setup-geodr-and-failover-pool.ps1?highlight=16-19 "Set up active geo-replication for elastic pool")]

## <a name="clean-up-deployment"></a><span data-ttu-id="cce9b-106">清除部署</span><span class="sxs-lookup"><span data-stu-id="cce9b-106">Clean up deployment</span></span>

<span data-ttu-id="cce9b-107">Hello 指令碼範例執行後，下列命令的 hello 可以使用的 tooremove hello 資源群組和與其相關聯的所有資源。</span><span class="sxs-lookup"><span data-stu-id="cce9b-107">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myPrimaryResourceGroup"
Remove-AzureRmResourceGroup -ResourceGroupName "mySecondaryResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="cce9b-108">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="cce9b-108">Script explanation</span></span>

<span data-ttu-id="cce9b-109">此指令碼會使用下列命令的 hello。</span><span class="sxs-lookup"><span data-stu-id="cce9b-109">This script uses hello following commands.</span></span> <span data-ttu-id="cce9b-110">Hello 資料表連結 toocommand 特定文件中的每個命令。</span><span class="sxs-lookup"><span data-stu-id="cce9b-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="cce9b-111">命令</span><span class="sxs-lookup"><span data-stu-id="cce9b-111">Command</span></span> | <span data-ttu-id="cce9b-112">注意事項</span><span class="sxs-lookup"><span data-stu-id="cce9b-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="cce9b-113">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="cce9b-113">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="cce9b-114">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="cce9b-114">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="cce9b-115">New-AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="cce9b-115">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="cce9b-116">建立主機資料庫或彈性集區的邏輯伺服器。</span><span class="sxs-lookup"><span data-stu-id="cce9b-116">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="cce9b-117">New-AzureRmSqlElasticPool</span><span class="sxs-lookup"><span data-stu-id="cce9b-117">New-AzureRmSqlElasticPool</span></span>](/powershell/module/azurerm.sql/new-azurermsqlelasticpool) | <span data-ttu-id="cce9b-118">在邏輯伺服器內建立彈性集區。</span><span class="sxs-lookup"><span data-stu-id="cce9b-118">Creates an elastic pool within a logical server.</span></span> |
| [<span data-ttu-id="cce9b-119">New-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="cce9b-119">New-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabase) | <span data-ttu-id="cce9b-120">在邏輯伺服器中將資料庫建立為單一或集區的資料庫。</span><span class="sxs-lookup"><span data-stu-id="cce9b-120">Creates a database in a logical server as a single or a pooled database.</span></span> |
| [<span data-ttu-id="cce9b-121">Set-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="cce9b-121">Set-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/set-azurermsqldatabase) | <span data-ttu-id="cce9b-122">更新資料庫屬性，或將資料庫移入、移出彈性集區或在彈性集區之間移動資料庫。</span><span class="sxs-lookup"><span data-stu-id="cce9b-122">Updates database properties or moves a database into, out of, or between elastic pools.</span></span> |
| [<span data-ttu-id="cce9b-123">New-AzureRmSqlDatabaseSecondary</span><span class="sxs-lookup"><span data-stu-id="cce9b-123">New-AzureRmSqlDatabaseSecondary</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabasesecondary)| <span data-ttu-id="cce9b-124">針對現有資料庫建立次要資料庫並開始資料複寫。</span><span class="sxs-lookup"><span data-stu-id="cce9b-124">Creates a secondary database for an existing database and starts data replication.</span></span> |
| [<span data-ttu-id="cce9b-125">Get-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="cce9b-125">Get-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/get-azurermsqldatabase)| <span data-ttu-id="cce9b-126">取得一或多個資料庫。</span><span class="sxs-lookup"><span data-stu-id="cce9b-126">Gets one or more databases.</span></span> |
| [<span data-ttu-id="cce9b-127">Set-AzureRmSqlDatabaseSecondary</span><span class="sxs-lookup"><span data-stu-id="cce9b-127">Set-AzureRmSqlDatabaseSecondary</span></span>](/powershell/module/azurerm.sql/set-azurermsqldatabasesecondary)| <span data-ttu-id="cce9b-128">切換為次要資料庫 toobe 主要順序 tooinitiate 容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="cce9b-128">Switches a secondary database toobe primary in order tooinitiate failover.</span></span>|
| [<span data-ttu-id="cce9b-129">Get-AzureRmSqlDatabaseReplicationLink</span><span class="sxs-lookup"><span data-stu-id="cce9b-129">Get-AzureRmSqlDatabaseReplicationLink</span></span>](/powershell/module/azurerm.sql/get-azurermsqldatabasereplicationlink) | <span data-ttu-id="cce9b-130">取得 Azure SQL Database 與資源群組或 SQL Server 之間的 hello 異地複寫連結。</span><span class="sxs-lookup"><span data-stu-id="cce9b-130">Gets hello geo-replication links between an Azure SQL Database and a resource group or SQL Server.</span></span> |
| [<span data-ttu-id="cce9b-131">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="cce9b-131">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="cce9b-132">刪除資源群組，包括所有的巢狀資源。</span><span class="sxs-lookup"><span data-stu-id="cce9b-132">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="cce9b-133">後續步驟</span><span class="sxs-lookup"><span data-stu-id="cce9b-133">Next steps</span></span>

<span data-ttu-id="cce9b-134">如需有關 hello Azure PowerShell 的詳細資訊，請參閱[Azure PowerShell 文件](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="cce9b-134">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="cce9b-135">其他的 SQL 資料庫的 PowerShell 指令碼範例可以在 hello [Azure SQL Database 的 PowerShell 指令碼](../sql-database-powershell-samples.md)。</span><span class="sxs-lookup"><span data-stu-id="cce9b-135">Additional SQL Database PowerShell script samples can be found in hello [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
