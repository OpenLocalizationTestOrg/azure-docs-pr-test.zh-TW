---
title: "aaaPowerShell 範例地理複寫容錯移轉群組單一 Azure SQL Database |Microsoft 文件"
description: "Azure PowerShell 範例指令碼 tooset 總為單一的 Azure SQL database 的作用中地理複寫"
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
ms.openlocfilehash: 0ea7afb1125b95370811ef7f80cb9eb7391b2443
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-tooconfigure-an-active-geo-replication-failover-group-for-a-single-azure-sql-database"></a><span data-ttu-id="fd8ce-103">使用 PowerShell tooconfigure 作用中地理複寫容錯移轉群組為單一的 Azure SQL database</span><span class="sxs-lookup"><span data-stu-id="fd8ce-103">Use PowerShell tooconfigure an active geo-replication failover group for a single Azure SQL database</span></span>

<span data-ttu-id="fd8ce-104">這個 PowerShell 指令碼範例會設定為單一的 Azure SQL database 的作用中地理複寫容錯移轉群組，並容錯 tooa hello Azure SQL database 的次要複本。</span><span class="sxs-lookup"><span data-stu-id="fd8ce-104">This PowerShell script example configures an active geo-replication failover group for a single Azure SQL database and fails it over tooa secondary replica of hello Azure SQL database.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-scripts"></a><span data-ttu-id="fd8ce-105">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="fd8ce-105">Sample scripts</span></span>

[!code-powershell[main](../../../powershell_scripts/sql-database/setup-geodr-and-failover-database/setup-geodr-and-failover-database-failover-group.ps1?highlight=19-22 "Set up failover group for single database")]

## <a name="clean-up-deployment"></a><span data-ttu-id="fd8ce-106">清除部署</span><span class="sxs-lookup"><span data-stu-id="fd8ce-106">Clean up deployment</span></span>

<span data-ttu-id="fd8ce-107">Hello 指令碼範例執行後，下列命令的 hello 可以使用的 tooremove hello 資源群組和與其相關聯的所有資源。</span><span class="sxs-lookup"><span data-stu-id="fd8ce-107">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myPrimaryResourceGroup"
Remove-AzureRmResourceGroup -ResourceGroupName "mySecondaryResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="fd8ce-108">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="fd8ce-108">Script explanation</span></span>

<span data-ttu-id="fd8ce-109">此指令碼會使用下列命令的 hello。</span><span class="sxs-lookup"><span data-stu-id="fd8ce-109">This script uses hello following commands.</span></span> <span data-ttu-id="fd8ce-110">Hello 資料表連結 toocommand 特定文件中的每個命令。</span><span class="sxs-lookup"><span data-stu-id="fd8ce-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="fd8ce-111">命令</span><span class="sxs-lookup"><span data-stu-id="fd8ce-111">Command</span></span> | <span data-ttu-id="fd8ce-112">注意事項</span><span class="sxs-lookup"><span data-stu-id="fd8ce-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="fd8ce-113">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="fd8ce-113">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="fd8ce-114">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="fd8ce-114">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="fd8ce-115">New-AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="fd8ce-115">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="fd8ce-116">建立主機資料庫或彈性集區的邏輯伺服器。</span><span class="sxs-lookup"><span data-stu-id="fd8ce-116">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="fd8ce-117">New-AzureRmSqlElasticPool</span><span class="sxs-lookup"><span data-stu-id="fd8ce-117">New-AzureRmSqlElasticPool</span></span>](/powershell/module/azurerm.sql/new-azurermsqlelasticpool) | <span data-ttu-id="fd8ce-118">在邏輯伺服器內建立彈性集區。</span><span class="sxs-lookup"><span data-stu-id="fd8ce-118">Creates an elastic pool within a logical server.</span></span> |
| [<span data-ttu-id="fd8ce-119">Set-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="fd8ce-119">Set-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/set-azurermsqldatabase) | <span data-ttu-id="fd8ce-120">更新資料庫屬性，或將資料庫移入、移出彈性集區或在彈性集區之間移動資料庫。</span><span class="sxs-lookup"><span data-stu-id="fd8ce-120">Updates database properties or moves a database into, out of, or between elastic pools.</span></span> |
| [<span data-ttu-id="fd8ce-121">New-AzureRmSqlDatabaseSecondary</span><span class="sxs-lookup"><span data-stu-id="fd8ce-121">New-AzureRmSqlDatabaseSecondary</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabasesecondary)| <span data-ttu-id="fd8ce-122">針對現有資料庫建立次要資料庫並開始資料複寫。</span><span class="sxs-lookup"><span data-stu-id="fd8ce-122">Creates a secondary database for an existing database and starts data replication.</span></span> |
| [<span data-ttu-id="fd8ce-123">Get-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="fd8ce-123">Get-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/get-azurermsqldatabase)| <span data-ttu-id="fd8ce-124">取得一或多個資料庫。</span><span class="sxs-lookup"><span data-stu-id="fd8ce-124">Gets one or more databases.</span></span> |
| [<span data-ttu-id="fd8ce-125">Set-AzureRmSqlDatabaseSecondary</span><span class="sxs-lookup"><span data-stu-id="fd8ce-125">Set-AzureRmSqlDatabaseSecondary</span></span>](/powershell/module/azurerm.sql/set-azurermsqldatabasesecondary)| <span data-ttu-id="fd8ce-126">切換次要資料庫 toobe 主要 tooinitiate 容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="fd8ce-126">Switches a secondary database toobe primary tooinitiate failover.</span></span>|
| [<span data-ttu-id="fd8ce-127">Get-AzureRmSqlDatabaseReplicationLink</span><span class="sxs-lookup"><span data-stu-id="fd8ce-127">Get-AzureRmSqlDatabaseReplicationLink</span></span>](/powershell/module/azurerm.sql/get-azurermsqldatabasereplicationlink) | <span data-ttu-id="fd8ce-128">取得 Azure SQL Database 與資源群組或 SQL Server 之間的 hello 異地複寫連結。</span><span class="sxs-lookup"><span data-stu-id="fd8ce-128">Gets hello geo-replication links between an Azure SQL Database and a resource group or SQL Server.</span></span> |
| [<span data-ttu-id="fd8ce-129">Remove-AzureRmSqlDatabaseSecondary</span><span class="sxs-lookup"><span data-stu-id="fd8ce-129">Remove-AzureRmSqlDatabaseSecondary</span></span>](/powershell/module/azurerm.sql/remove-azurermsqldatabasesecondary) | <span data-ttu-id="fd8ce-130">終止 SQL Database 與 hello 指定的次要資料庫之間的資料複寫。</span><span class="sxs-lookup"><span data-stu-id="fd8ce-130">Terminates data replication between a SQL Database and hello specified secondary database.</span></span> |
| [<span data-ttu-id="fd8ce-131">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="fd8ce-131">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="fd8ce-132">刪除資源群組，包括所有的巢狀資源。</span><span class="sxs-lookup"><span data-stu-id="fd8ce-132">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="fd8ce-133">後續步驟</span><span class="sxs-lookup"><span data-stu-id="fd8ce-133">Next steps</span></span>

<span data-ttu-id="fd8ce-134">如需有關 hello Azure PowerShell 的詳細資訊，請參閱[Azure PowerShell 文件](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="fd8ce-134">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="fd8ce-135">其他的 SQL 資料庫的 PowerShell 指令碼範例可以在 hello [Azure SQL Database 的 PowerShell 指令碼](../sql-database-powershell-samples.md)。</span><span class="sxs-lookup"><span data-stu-id="fd8ce-135">Additional SQL Database PowerShell script samples can be found in hello [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
