---
title: "PowerShell：建立及管理 Azure SQL 彈性集區 | Microsoft Docs"
description: "了解如何使用 PowerShell 管理彈性集區。"
services: sql-database
documentationcenter: 
author: srinia
manager: jhubbard
editor: 
ms.assetid: 61289770-69b9-4ae3-9252-d0e94d709331
ms.service: sql-database
ms.custom: DBs & servers
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: powershell
ms.workload: data-management
ms.date: 06/06/2017
ms.author: srinia
ms.openlocfilehash: 5e76397c62e5a6ff7fb356bd81218c307f3fda31
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-manage-an-elastic-pool-with-powershell"></a><span data-ttu-id="7d0ef-103">使用 PowerShell 建立及管理彈性集區</span><span class="sxs-lookup"><span data-stu-id="7d0ef-103">Create and manage an elastic pool with PowerShell</span></span>
<span data-ttu-id="7d0ef-104">本主題說明如何使用 PowerShell 建立及管理可調整的[彈性集區](sql-database-elastic-pool.md)。</span><span class="sxs-lookup"><span data-stu-id="7d0ef-104">This topic shows you how to create and manage scalable [elastic pools](sql-database-elastic-pool.md) with PowerShell.</span></span>  <span data-ttu-id="7d0ef-105">您也可以使用 [Azure 入口網站](https://portal.azure.com/)、REST API 或 [C#](sql-database-elastic-pool-manage-csharp.md) 來建立及管理 Azure 彈性集區。</span><span class="sxs-lookup"><span data-stu-id="7d0ef-105">You can also create and manage an Azure elastic pool using the [Azure portal](https://portal.azure.com/), REST API, or [C#](sql-database-elastic-pool-manage-csharp.md).</span></span> <span data-ttu-id="7d0ef-106">您也可以使用 [Transact-SQL](sql-database-elastic-pool-manage-tsql.md) 來建立資料庫並將它移入和移出彈性集區。</span><span class="sxs-lookup"><span data-stu-id="7d0ef-106">You can also create and move databases into and out of elastic pools using [Transact-SQL](sql-database-elastic-pool-manage-tsql.md).</span></span>

[!INCLUDE [Start your PowerShell session](../../includes/sql-database-powershell.md)]

## <a name="create-an-elastic-pool"></a><span data-ttu-id="7d0ef-107">建立彈性集區</span><span class="sxs-lookup"><span data-stu-id="7d0ef-107">Create an elastic pool</span></span>
<span data-ttu-id="7d0ef-108">[New-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/new-azurermsqlelasticpool) Cmdlet 會建立彈性集區。</span><span class="sxs-lookup"><span data-stu-id="7d0ef-108">The [New-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/new-azurermsqlelasticpool) cmdlet creates an elastic pool.</span></span> <span data-ttu-id="7d0ef-109">每個集區的 eDTU 值、最小和最大 DTU 會受限於服務層值 (基本、標準、進階或進階 RS)。</span><span class="sxs-lookup"><span data-stu-id="7d0ef-109">The values for eDTU per pool, min, and max DTUs are constrained by the service tier value (Basic, Standard, Premium, or Premium RS).</span></span> <span data-ttu-id="7d0ef-110">請參閱[彈性集區和集區資料庫的 eDTU 和儲存體限制](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools)。</span><span class="sxs-lookup"><span data-stu-id="7d0ef-110">See [eDTU and storage limits for elastic pools and pooled databases](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools).</span></span>

```PowerShell
New-AzureRmSqlElasticPool -ResourceGroupName "resourcegroup1" -ServerName "server1" -ElasticPoolName "elasticpool1" -Edition "Standard" -Dtu 400 -DatabaseDtuMin 10 -DatabaseDtuMax 100
```

## <a name="create-a-pooled-database-in-an-elastic-pool"></a><span data-ttu-id="7d0ef-111">在彈性集區中建立集區資料庫</span><span class="sxs-lookup"><span data-stu-id="7d0ef-111">Create a pooled database in an elastic pool</span></span>
<span data-ttu-id="7d0ef-112">使用 [New-AzureRmSqlDatabase](/powershell/module/azurerm.sql/new-azurermsqldatabase) Cmdlet，並將 **ElasticPoolName** 參數設定為目標集區。</span><span class="sxs-lookup"><span data-stu-id="7d0ef-112">Use the [New-AzureRmSqlDatabase](/powershell/module/azurerm.sql/new-azurermsqldatabase) cmdlet and set the **ElasticPoolName** parameter to the target pool.</span></span> <span data-ttu-id="7d0ef-113">若要將現有的資料庫移入彈性集區，請參閱[將資料庫移入彈性集區](sql-database-elastic-pool-manage-powershell.md#move-a-database-into-an-elastic-pool)。</span><span class="sxs-lookup"><span data-stu-id="7d0ef-113">To move an existing database into an elastic pool, see [Move a database into an elastic pool](sql-database-elastic-pool-manage-powershell.md#move-a-database-into-an-elastic-pool).</span></span>

```PowerShell
New-AzureRmSqlDatabase -ResourceGroupName "resourcegroup1" -ServerName "server1" -DatabaseName "database1" -ElasticPoolName "elasticpool1"
```

### <a name="complete-script"></a><span data-ttu-id="7d0ef-114">完整的指令碼</span><span class="sxs-lookup"><span data-stu-id="7d0ef-114">Complete script</span></span>
<span data-ttu-id="7d0ef-115">此指令碼會建立 Azure 資源群組和伺服器。</span><span class="sxs-lookup"><span data-stu-id="7d0ef-115">This script creates an Azure resource group and a server.</span></span> <span data-ttu-id="7d0ef-116">出現提示時，提供適用於新伺服器的系統管理員使用者名稱和密碼 (而非您 Azure 認證)。</span><span class="sxs-lookup"><span data-stu-id="7d0ef-116">When prompted, supply an administrator username and password for the new server (not your Azure credentials).</span></span>

```PowerShell
$subscriptionId = '<your Azure subscription id>'
$resourceGroupName = '<resource group name>'
$location = '<datacenter location>'
$serverName = '<server name>'
$poolName = '<pool name>'
$databaseName = '<database name>'

Login-AzureRmAccount
Set-AzureRmContext -SubscriptionId $subscriptionId

New-AzureRmResourceGroup -Name $resourceGroupName -Location $location
New-AzureRmSqlServer -ResourceGroupName $resourceGroupName -ServerName $serverName -Location $location -ServerVersion "12.0"
New-AzureRmSqlServerFirewallRule -ResourceGroupName $resourceGroupName -ServerName $serverName -FirewallRuleName "rule1" -StartIpAddress "192.168.0.198" -EndIpAddress "192.168.0.199"

New-AzureRmSqlElasticPool -ResourceGroupName $resourceGroupName -ServerName $serverName -ElasticPoolName $poolName -Edition "Standard" -Dtu 400 -DatabaseDtuMin 10 -DatabaseDtuMax 100

New-AzureRmSqlDatabase -ResourceGroupName $resourceGroupName -ServerName $serverName -DatabaseName $databaseName -ElasticPoolName $poolName -MaxSizeBytes 10GB
```

## <a name="create-an-elastic-pool-and-add-multiple-pooled-databases"></a><span data-ttu-id="7d0ef-117">建立彈性集區並新增多個集區資料庫</span><span class="sxs-lookup"><span data-stu-id="7d0ef-117">Create an elastic pool and add multiple pooled databases</span></span>
<span data-ttu-id="7d0ef-118">使用入口網站或一次只建立單一資料庫的 PowerShell Cmdlet 在彈性集區中建立許多資料庫可能需要花費一些時間。</span><span class="sxs-lookup"><span data-stu-id="7d0ef-118">Creation of many databases in an elastic pool can take time when done using the portal or PowerShell cmdlets that create only a single database at a time.</span></span> <span data-ttu-id="7d0ef-119">若要自動建立成彈性集區，請參閱 [CreateOrUpdateElasticPoolAndPopulate ](https://gist.github.com/billgib/d80c7687b17355d3c2ec8042323819ae)。</span><span class="sxs-lookup"><span data-stu-id="7d0ef-119">To automate creation into an elastic pool, see [CreateOrUpdateElasticPoolAndPopulate ](https://gist.github.com/billgib/d80c7687b17355d3c2ec8042323819ae).</span></span>

## <a name="move-a-database-into-an-elastic-pool"></a><span data-ttu-id="7d0ef-120">將資料庫移入彈性集區</span><span class="sxs-lookup"><span data-stu-id="7d0ef-120">Move a database into an elastic pool</span></span>
<span data-ttu-id="7d0ef-121">您可以使用 [Set-AzureRmSqlDatabase](/powershell/module/azurerm.sql/set-azurermsqlelasticpool) 將資料庫移入或移出彈性集區。</span><span class="sxs-lookup"><span data-stu-id="7d0ef-121">You can move a database into or out of an elastic pool with the [Set-AzureRmSqlDatabase](/powershell/module/azurerm.sql/set-azurermsqlelasticpool).</span></span>

```PowerShell
Set-AzureRmSqlDatabase -ResourceGroupName "resourcegroup1" -ServerName "server1" -DatabaseName "database1" -ElasticPoolName "elasticpool1"
```

## <a name="change-performance-settings-of-an-elastic-pool"></a><span data-ttu-id="7d0ef-122">變更彈性集區的效能設定</span><span class="sxs-lookup"><span data-stu-id="7d0ef-122">Change performance settings of an elastic pool</span></span>
<span data-ttu-id="7d0ef-123">當犧牲效能時，您可以變更集區的設定，以配合效能成長。</span><span class="sxs-lookup"><span data-stu-id="7d0ef-123">When performance suffers, you can change the settings of the pool to accommodate growth.</span></span> <span data-ttu-id="7d0ef-124">使用 [Set-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/set-azurermsqlelasticpool) Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="7d0ef-124">Use the [Set-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/set-azurermsqlelasticpool) cmdlet.</span></span> <span data-ttu-id="7d0ef-125">為每個集區的 eDTU 設定 -Dtu 參數。</span><span class="sxs-lookup"><span data-stu-id="7d0ef-125">Set the -Dtu parameter to the eDTUs per pool.</span></span> <span data-ttu-id="7d0ef-126">請參閱 [eDTU 和儲存體限制](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools)以了解有哪些可能的值。</span><span class="sxs-lookup"><span data-stu-id="7d0ef-126">See [eDTU and storage limits](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools) for possible values.</span></span>

```PowerShell
Set-AzureRmSqlElasticPool -ResourceGroupName “resourcegroup1” -ServerName “server1” -ElasticPoolName “elasticpool1” -Dtu 1200 -DatabaseDtuMax 100 -DatabaseDtuMin 50
```

## <a name="change-the-storage-limit-for-an-elastic-pool"></a><span data-ttu-id="7d0ef-127">變更彈性集區的儲存體限制</span><span class="sxs-lookup"><span data-stu-id="7d0ef-127">Change the storage limit for an elastic pool</span></span>

<span data-ttu-id="7d0ef-128">使用 [Set-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/set-azurermsqlelasticpool) Cmdlet 來設定 _-StorageMB_ 參數。</span><span class="sxs-lookup"><span data-stu-id="7d0ef-128">Use the [Set-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/set-azurermsqlelasticpool) cmdlet to set the _-StorageMB_ parameter.</span></span> <span data-ttu-id="7d0ef-129">提供以 MB 為單位的儲存體限制 (例如，2097152 會將儲存體限制設定為 2 TB)。</span><span class="sxs-lookup"><span data-stu-id="7d0ef-129">Provide the storage limit in MB (for example, 2097152 sets the storage limit to 2 TB).</span></span> <span data-ttu-id="7d0ef-130">請參閱 [eDTU 和儲存體限制](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools)以了解有哪些可能的值。</span><span class="sxs-lookup"><span data-stu-id="7d0ef-130">See [eDTU and storage limits](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools) for possible values.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7d0ef-131">對於具有 1500 或更多 eDTU 的進階集區而言，每個集區的預設最大資料儲存體為 750 GB。</span><span class="sxs-lookup"><span data-stu-id="7d0ef-131">The default max data storage per pool for Premium pools with 1500 eDTUs or more is 750 GB.</span></span> <span data-ttu-id="7d0ef-132">若要取得較大的_每一集區之資料儲存體大小上限_，您必須明確設定儲存體限制。</span><span class="sxs-lookup"><span data-stu-id="7d0ef-132">To obtain the higher _max data storage size per pool_, the storage limit must be explicitly set.</span></span> <span data-ttu-id="7d0ef-133">儲存體超過 750 GB 的進階集區目前在下列區域為公開預覽狀態：美國東部 2、美國西部、美國維吉尼亞州政府、西歐、德國中部、東南亞、日本東部、澳大利亞東部、加拿大中部和加拿大東部。</span><span class="sxs-lookup"><span data-stu-id="7d0ef-133">Premium pools with more than 750 GB of storage is currently in public preview in the following regions: East US 2, West US, US Gov Virginia, West Europe, Germany Central, Southeast Asia, Japan East, Australia East, Canada Central, and Canada East.</span></span>

```PowerShell
Set-AzureRmSqlElasticPool -ServerName "server1" -ElasticPoolName “elasticpool1” -StorageMB 2097152
```

## <a name="get-the-status-of-pool-operations"></a><span data-ttu-id="7d0ef-134">取得集區作業的狀態</span><span class="sxs-lookup"><span data-stu-id="7d0ef-134">Get the status of pool operations</span></span>
<span data-ttu-id="7d0ef-135">建立彈性集區可能會很耗時。</span><span class="sxs-lookup"><span data-stu-id="7d0ef-135">Creating an elastic pool can take time.</span></span> <span data-ttu-id="7d0ef-136">要追蹤集區作業的狀態，包括建立及更新作業，請使用 [Get-AzureRmSqlElasticPoolActivity](/powershell/module/azurerm.sql/get-azurermsqlelasticpoolactivity) Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="7d0ef-136">To track the status of pool operations including creation and updates, use the [Get-AzureRmSqlElasticPoolActivity](/powershell/module/azurerm.sql/get-azurermsqlelasticpoolactivity) cmdlet.</span></span>

```PowerShell
Get-AzureRmSqlElasticPoolActivity -ResourceGroupName “resourcegroup1” -ServerName “server1” -ElasticPoolName “elasticpool1”
```

## <a name="get-the-status-of-moving-a-database-into-and-out-of-an-elastic-pool"></a><span data-ttu-id="7d0ef-137">取得將資料庫移入和移出彈性集區的狀態</span><span class="sxs-lookup"><span data-stu-id="7d0ef-137">Get the status of moving a database into and out of an elastic pool</span></span>
<span data-ttu-id="7d0ef-138">移動資料庫可能會很耗時。</span><span class="sxs-lookup"><span data-stu-id="7d0ef-138">Moving a database can take time.</span></span> <span data-ttu-id="7d0ef-139">使用 [Get-AzureRmSqlDatabaseActivity](/powershell/module/azurerm.sql/get-azurermsqldatabaseactivity) Cmdlet 追蹤移動狀態。</span><span class="sxs-lookup"><span data-stu-id="7d0ef-139">Track a move status using the [Get-AzureRmSqlDatabaseActivity](/powershell/module/azurerm.sql/get-azurermsqldatabaseactivity) cmdlet.</span></span>

```PowerShell
Get-AzureRmSqlDatabaseActivity -ResourceGroupName "resourcegroup1" -ServerName "server1" -DatabaseName "database1" -ElasticPoolName "elasticpool1"
```

## <a name="get-resource-usage-data-for-an-elastic-pool"></a><span data-ttu-id="7d0ef-140">取得彈性集區的資源使用量資料</span><span class="sxs-lookup"><span data-stu-id="7d0ef-140">Get resource usage data for an elastic pool</span></span>
<span data-ttu-id="7d0ef-141">可以用資源集區限制的百分比來擷取的度量：</span><span class="sxs-lookup"><span data-stu-id="7d0ef-141">Metrics that can be retrieved as a percentage of the resource pool limit:</span></span>

| <span data-ttu-id="7d0ef-142">度量名稱</span><span class="sxs-lookup"><span data-stu-id="7d0ef-142">Metric name</span></span> | <span data-ttu-id="7d0ef-143">說明</span><span class="sxs-lookup"><span data-stu-id="7d0ef-143">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="7d0ef-144">cpu\_percent</span><span class="sxs-lookup"><span data-stu-id="7d0ef-144">cpu\_percent</span></span> |<span data-ttu-id="7d0ef-145">集區限制的平均計算使用量百分比。</span><span class="sxs-lookup"><span data-stu-id="7d0ef-145">Average compute utilization in percentage of the limit of the pool.</span></span> |
| <span data-ttu-id="7d0ef-146">實體\_資料\_讀取\_百分比</span><span class="sxs-lookup"><span data-stu-id="7d0ef-146">physical\_data\_read\_percent</span></span> |<span data-ttu-id="7d0ef-147">集區限制的平均 I/O 使用量百分比。</span><span class="sxs-lookup"><span data-stu-id="7d0ef-147">Average I/O utilization in percentage based on the limit of the pool.</span></span> |
| <span data-ttu-id="7d0ef-148">記錄檔\_撰寫\_百分比</span><span class="sxs-lookup"><span data-stu-id="7d0ef-148">log\_write\_percent</span></span> |<span data-ttu-id="7d0ef-149">集區限制的平均寫入資源使用量百分比。</span><span class="sxs-lookup"><span data-stu-id="7d0ef-149">Average write resource utilization in percentage of the limit of the pool.</span></span> |
| <span data-ttu-id="7d0ef-150">DTU\_耗用量\_百分比</span><span class="sxs-lookup"><span data-stu-id="7d0ef-150">DTU\_consumption\_percent</span></span> |<span data-ttu-id="7d0ef-151">集區 eDTU 限制的平均 eDTU 使用量百分比。</span><span class="sxs-lookup"><span data-stu-id="7d0ef-151">Average eDTU utilization in percentage of eDTU limit for the pool</span></span> |
| <span data-ttu-id="7d0ef-152">儲存體\_percent</span><span class="sxs-lookup"><span data-stu-id="7d0ef-152">storage\_percent</span></span> |<span data-ttu-id="7d0ef-153">集區儲存體限制的平均儲存體使用量百分比。</span><span class="sxs-lookup"><span data-stu-id="7d0ef-153">Average storage utilization in percentage of the storage limit of the pool.</span></span> |
| <span data-ttu-id="7d0ef-154">背景工作角色\_百分比</span><span class="sxs-lookup"><span data-stu-id="7d0ef-154">workers\_percent</span></span> |<span data-ttu-id="7d0ef-155">集區限制的並行背景工作角色 (要求) 百分比。</span><span class="sxs-lookup"><span data-stu-id="7d0ef-155">Maximum concurrent workers (requests) in percentage based on the limit of the pool.</span></span> |
| <span data-ttu-id="7d0ef-156">工作階段\_百分比</span><span class="sxs-lookup"><span data-stu-id="7d0ef-156">sessions\_percent</span></span> |<span data-ttu-id="7d0ef-157">集區限制的並行工作階段百分比。</span><span class="sxs-lookup"><span data-stu-id="7d0ef-157">Maximum concurrent sessions in percentage based on the limit of the pool.</span></span> |
| <span data-ttu-id="7d0ef-158">eDTU_limit</span><span class="sxs-lookup"><span data-stu-id="7d0ef-158">eDTU_limit</span></span> |<span data-ttu-id="7d0ef-159">間隔期間此彈性集區目前最大的彈性集區 DTU 設定。</span><span class="sxs-lookup"><span data-stu-id="7d0ef-159">Current max elastic pool DTU setting for this elastic pool during this interval.</span></span> |
| <span data-ttu-id="7d0ef-160">儲存體\_限制</span><span class="sxs-lookup"><span data-stu-id="7d0ef-160">storage\_limit</span></span> |<span data-ttu-id="7d0ef-161">間隔期間此彈性集區目前最大的彈性集區儲存體限制設定 (MB)。</span><span class="sxs-lookup"><span data-stu-id="7d0ef-161">Current max elastic pool storage limit setting for this elastic pool in megabytes during this interval.</span></span> |
| <span data-ttu-id="7d0ef-162">eDTU\_使用</span><span class="sxs-lookup"><span data-stu-id="7d0ef-162">eDTU\_used</span></span> |<span data-ttu-id="7d0ef-163">此間隔期間集區使用的平均 eDTU。</span><span class="sxs-lookup"><span data-stu-id="7d0ef-163">Average eDTUs used by the pool in this interval.</span></span> |
| <span data-ttu-id="7d0ef-164">儲存體\_使用</span><span class="sxs-lookup"><span data-stu-id="7d0ef-164">storage\_used</span></span> |<span data-ttu-id="7d0ef-165">此間隔期間集區使用的平均儲存體位元組數。</span><span class="sxs-lookup"><span data-stu-id="7d0ef-165">Average storage used by the pool in this interval in bytes</span></span> |

<span data-ttu-id="7d0ef-166">**度量資料粒度/保留期限：**</span><span class="sxs-lookup"><span data-stu-id="7d0ef-166">**Metrics granularity/retention periods:**</span></span>

* <span data-ttu-id="7d0ef-167">系統會以 5 分鐘的資料粒度傳回資料。</span><span class="sxs-lookup"><span data-stu-id="7d0ef-167">Data is returned at 5-minute granularity.</span></span>  
* <span data-ttu-id="7d0ef-168">資料會保留 35 天。</span><span class="sxs-lookup"><span data-stu-id="7d0ef-168">Data retention is 35 days.</span></span>  

<span data-ttu-id="7d0ef-169">此 Cmdlet 和 API 會將一次呼叫中可擷取的資料列限制為 1000 個 (大約是 3 天份且資料粒度為 5 分鐘的資料)。</span><span class="sxs-lookup"><span data-stu-id="7d0ef-169">This cmdlet and API limits the number of rows that can be retrieved in one call to 1000 rows (about 3 days of data at 5-minute granularity).</span></span> <span data-ttu-id="7d0ef-170">但可以用不同的開始/結束時間間隔來多次呼叫此命令，以擷取更多資料。</span><span class="sxs-lookup"><span data-stu-id="7d0ef-170">But this command can be called multiple times with different start/end time intervals to retrieve more data</span></span>

<span data-ttu-id="7d0ef-171">擷取度量：</span><span class="sxs-lookup"><span data-stu-id="7d0ef-171">To retrieve the metrics:</span></span>

```PowerShell
$metrics = (Get-AzureRmMetric -ResourceId /subscriptions/<subscriptionId>/resourceGroups/FabrikamData01/providers/Microsoft.Sql/servers/fabrikamsqldb02/elasticPools/franchisepool -TimeGrain ([TimeSpan]::FromMinutes(5)) -StartTime "4/18/2015" -EndTime "4/21/2015")
```

## <a name="get-resource-usage-data-for-a-database-in-an-elastic-pool"></a><span data-ttu-id="7d0ef-172">取得彈性集區中資料庫的資源使用量資料</span><span class="sxs-lookup"><span data-stu-id="7d0ef-172">Get resource usage data for a database in an elastic pool</span></span>
<span data-ttu-id="7d0ef-173">這些 API 與用來監視單一資料庫之資源使用率的 API 相同，唯一的差別在於下列語意：擷取的度量是以為該集區設定的每個資料庫最大 eDTU 百分比形式表示 (或相等於 CPU 或 IO 等基礎度量的上限)。</span><span class="sxs-lookup"><span data-stu-id="7d0ef-173">These APIs are the same as the APIs used for monitoring the resource utilization of a single database, except for the following semantic difference: metrics retrieved are expressed as a percentage of the per database max eDTUs (or equivalent cap for the underlying metric like CPU or IO) set for that pool.</span></span> <span data-ttu-id="7d0ef-174">例如，這些度量有其中一項的使用率為 50%，則表示特定資源的消耗量佔該資源在父集區中，每個資料庫上限限制的 50%。</span><span class="sxs-lookup"><span data-stu-id="7d0ef-174">For example, 50% utilization of any of these metrics indicates that the specific resource consumption is at 50% of the per database cap limit for that resource in the parent pool.</span></span>

<span data-ttu-id="7d0ef-175">擷取度量：</span><span class="sxs-lookup"><span data-stu-id="7d0ef-175">To retrieve the metrics:</span></span>

```PowerShell
$metrics = (Get-AzureRmMetric -ResourceId /subscriptions/<subscriptionId>/resourceGroups/FabrikamData01/providers/Microsoft.Sql/servers/fabrikamsqldb02/databases/myDB -TimeGrain ([TimeSpan]::FromMinutes(5)) -StartTime "4/18/2015" -EndTime "4/21/2015")
```

## <a name="add-an-alert-to-an-elastic-pool-resource"></a><span data-ttu-id="7d0ef-176">將警示新增到彈性集區資源</span><span class="sxs-lookup"><span data-stu-id="7d0ef-176">Add an alert to an elastic pool resource</span></span>
<span data-ttu-id="7d0ef-177">您可以將警示規則新增到彈性集區中，以在彈性集區達到您設定的使用率閾值時，將電子郵件通知或警示字串傳送到 [URL 端點](https://msdn.microsoft.com/library/mt718036.aspx)。</span><span class="sxs-lookup"><span data-stu-id="7d0ef-177">You can add alert rules to an elastic pool to send email notifications or alert strings to [URL endpoints](https://msdn.microsoft.com/library/mt718036.aspx) when the elastic pool hits a utilization threshold that you set up.</span></span> <span data-ttu-id="7d0ef-178">使用 Add-AzureRmMetricAlertRule Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="7d0ef-178">Use the Add-AzureRmMetricAlertRule cmdlet.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7d0ef-179">監視彈性集區的資源使用率至少有 5 分鐘的延遲。</span><span class="sxs-lookup"><span data-stu-id="7d0ef-179">Resource utilization monitoring for elastic pools has a lag of at least 5 minutes.</span></span> <span data-ttu-id="7d0ef-180">目前不支援將彈性集區的警示設定為小於 10 分鐘。</span><span class="sxs-lookup"><span data-stu-id="7d0ef-180">Setting alerts of less than 10 minutes for elastic pools is not currently supported.</span></span> <span data-ttu-id="7d0ef-181">彈性集區以句號的任何警示設定 (稱為參數"-WindowSize"PowerShell API 中) 的 10 分鐘內不一定會觸發。</span><span class="sxs-lookup"><span data-stu-id="7d0ef-181">Any alerts set for elastic pools with a period (parameter called “-WindowSize” in PowerShell API) of less than 10 minutes may not be triggered.</span></span> <span data-ttu-id="7d0ef-182">請確定您針對彈性集區定義的任何警示都會使用 10 分鐘以上的期間 (WindowSize)。</span><span class="sxs-lookup"><span data-stu-id="7d0ef-182">Make sure that any alerts you define for elastic pools use a period (WindowSize) of 10 minutes or more.</span></span>
>
>

<span data-ttu-id="7d0ef-183">此範例會新增一個可在彈性集區 eDTU 耗用量超過特定閾值時接獲通知的警示。</span><span class="sxs-lookup"><span data-stu-id="7d0ef-183">This example adds an alert for getting notified when an elastic pool’s eDTU consumption goes above certain threshold.</span></span>

```PowerShell
# Set up your resource ID configurations
$subscriptionId = '<Azure subscription id>'      # Azure subscription ID
$location =  '<location'                         # Azure region
$resourceGroupName = '<resource group name>'     # Resource Group
$serverName = '<server name>'                    # server name
$poolName = '<elastic pool name>'                # pool name

#$Target Resource ID
$ResourceID = '/subscriptions/' + $subscriptionId + '/resourceGroups/' +$resourceGroupName + '/providers/Microsoft.Sql/servers/' + $serverName + '/elasticpools/' + $poolName

# Create an email action
$actionEmail = New-AzureRmAlertRuleEmail -SendToServiceOwners -CustomEmail JohnDoe@contoso.com

# create a unique rule name
$alertName = $poolName + "- DTU consumption rule"

# Create an alert rule for DTU_consumption_percent
Add-AzureRMMetricAlertRule -Name $alertName -Location $location -ResourceGroup $resourceGroupName -TargetResourceId $ResourceID -MetricName "DTU_consumption_percent"  -Operator GreaterThan -Threshold 80 -TimeAggregationOperator Average -WindowSize 00:60:00 -Actions $actionEmail
```

<span data-ttu-id="7d0ef-184">如需詳細資訊，請參閱[在 Azure 入口網站中建立 SQL Database 警示](sql-database-insights-alerts-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="7d0ef-184">For more information, see [create SQL Database alerts in Azure portal](sql-database-insights-alerts-portal.md).</span></span>

## <a name="add-alerts-to-all-databases-in-an-elastic-pool"></a><span data-ttu-id="7d0ef-185">將警示新增到彈性集區中的所有資料庫</span><span class="sxs-lookup"><span data-stu-id="7d0ef-185">Add alerts to all databases in an elastic pool</span></span>
<span data-ttu-id="7d0ef-186">您可以將警示規則新增到彈性集區中的所有資料庫，以在資源達到警示所設定的使用率臨界值時，將電子郵件通知或警示字串傳送到 [URL 端點](https://msdn.microsoft.com/library/mt718036.aspx) 。</span><span class="sxs-lookup"><span data-stu-id="7d0ef-186">You can add alert rules to all database in an elastic pool to send email notifications or alert strings to [URL endpoints](https://msdn.microsoft.com/library/mt718036.aspx) when a resource hits a utilization threshold set up by the alert.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7d0ef-187">監視彈性集區的資源使用率至少有 5 分鐘的延遲。</span><span class="sxs-lookup"><span data-stu-id="7d0ef-187">Resource utilization monitoring for elastic pools has a lag of at least 5 minutes.</span></span> <span data-ttu-id="7d0ef-188">目前不支援將彈性集區的警示設定為小於 10 分鐘。</span><span class="sxs-lookup"><span data-stu-id="7d0ef-188">Setting alerts of less than 10 minutes for elastic pools is not currently supported.</span></span> <span data-ttu-id="7d0ef-189">彈性集區以句號的任何警示設定 (稱為參數"-WindowSize"PowerShell API 中) 的 10 分鐘內不一定會觸發。</span><span class="sxs-lookup"><span data-stu-id="7d0ef-189">Any alerts set for elastic pools with a period (parameter called “-WindowSize” in PowerShell API) of less than 10 minutes may not be triggered.</span></span> <span data-ttu-id="7d0ef-190">請確定您針對彈性集區定義的任何警示都會使用 10 分鐘以上的期間 (WindowSize)。</span><span class="sxs-lookup"><span data-stu-id="7d0ef-190">Make sure that any alerts you define for elastic pools use a period (WindowSize) of 10 minutes or more.</span></span>
>

<span data-ttu-id="7d0ef-191">此範例會將警示新增到彈性集區中的每個資料庫，以在資料庫的 DTU 耗用量超過特定閾值時接獲通知。</span><span class="sxs-lookup"><span data-stu-id="7d0ef-191">This example adds an alert to each of the databases in an elastic pool for getting notified when that database’s DTU consumption goes above certain threshold.</span></span>

```PowerShell
# Set up your resource ID configurations
$subscriptionId = '<Azure subscription id>'      # Azure subscription ID
$location = '<location'                          # Azure region
$resourceGroupName = '<resource group name>'     # Resource Group
$serverName = '<server name>'                    # server name
$poolName = '<elastic pool name>'                # pool name

# Get the list of databases in this pool.
$dbList = Get-AzureRmSqlElasticPoolDatabase -ResourceGroupName $resourceGroupName -ServerName $serverName -ElasticPoolName $poolName

# Create an email action
$actionEmail = New-AzureRmAlertRuleEmail -SendToServiceOwners -CustomEmail JohnDoe@contoso.com

# Get resource usage metrics for a database in an elastic pool for the specified time interval.
foreach ($db in $dbList)
{
    $dbResourceId = '/subscriptions/' + $subscriptionId + '/resourceGroups/' + $resourceGroupName + '/providers/Microsoft.Sql/servers/' + $serverName + '/databases/' + $db.DatabaseName

    # create a unique rule name
    $alertName = $db.DatabaseName + "- DTU consumption rule"

    # Create an alert rule for DTU_consumption_percent
    Add-AzureRMMetricAlertRule -Name $alertName  -Location $location -ResourceGroup $resourceGroupName -TargetResourceId $dbResourceId -MetricName "dtu_consumption_percent"  -Operator GreaterThan -Threshold 80 -TimeAggregationOperator Average -WindowSize 00:60:00 -Actions $actionEmail

    # drop the alert rule
    #Remove-AzureRmAlertRule -ResourceGroup $resourceGroupName -Name $alertName
}
```

## <a name="collect-and-monitor-resource-usage-data-across-multiple-pools-in-a-subscription"></a><span data-ttu-id="7d0ef-192">收集和監視訂用帳戶中多個集區的資源使用量資料</span><span class="sxs-lookup"><span data-stu-id="7d0ef-192">Collect and monitor resource usage data across multiple pools in a subscription</span></span>
<span data-ttu-id="7d0ef-193">當訂用帳戶中有許多資料庫時，難以分開監視每個彈性集區。</span><span class="sxs-lookup"><span data-stu-id="7d0ef-193">When you have many databases in a subscription, it is cumbersome to monitor each elastic pool separately.</span></span> <span data-ttu-id="7d0ef-194">因此，可以結合 SQL Database PowerShell Cmdlet 和 T-SQL 查詢，從多個集區與其資料庫收集資源使用量資料，以便監視和分析資源使用量。</span><span class="sxs-lookup"><span data-stu-id="7d0ef-194">Instead, SQL database PowerShell cmdlets and T-SQL queries can be combined to collect resource usage data from multiple pools and their databases for monitoring and analysis of resource usage.</span></span> <span data-ttu-id="7d0ef-195">在 GitHub 上的 SQL Server 範例存放庫中，可以找到這樣一組 PowerShell 指令碼的 [範例實作](https://github.com/Microsoft/sql-server-samples/tree/master/samples/manage/azure-sql-db-elastic-pools) ，以及其作用和使用方式的相關文件。</span><span class="sxs-lookup"><span data-stu-id="7d0ef-195">A [sample implementation](https://github.com/Microsoft/sql-server-samples/tree/master/samples/manage/azure-sql-db-elastic-pools) of such a set of powershell scripts can be found in the GitHub SQL Server samples repository along with documentation on what it does and how to use it.</span></span>

<span data-ttu-id="7d0ef-196">若要使用此範例實作，請依照下列步驟執行。</span><span class="sxs-lookup"><span data-stu-id="7d0ef-196">To use this sample implementation, follow these steps.</span></span>

1. <span data-ttu-id="7d0ef-197">下載[指令碼和文件](https://github.com/Microsoft/sql-server-samples/tree/master/samples/manage/azure-sql-db-elastic-pools)：</span><span class="sxs-lookup"><span data-stu-id="7d0ef-197">Download the [scripts and documentation](https://github.com/Microsoft/sql-server-samples/tree/master/samples/manage/azure-sql-db-elastic-pools):</span></span>
2. <span data-ttu-id="7d0ef-198">為您的環境修改指令碼。</span><span class="sxs-lookup"><span data-stu-id="7d0ef-198">Modify the scripts for your environment.</span></span> <span data-ttu-id="7d0ef-199">指定裝載彈性集區的一或多部伺服器。</span><span class="sxs-lookup"><span data-stu-id="7d0ef-199">Specify one or more servers on which elastic pools are hosted.</span></span>
3. <span data-ttu-id="7d0ef-200">指定儲存所收集度量的遙測資料庫。</span><span class="sxs-lookup"><span data-stu-id="7d0ef-200">Specify a telemetry database where the collected metrics are to be stored.</span></span>
4. <span data-ttu-id="7d0ef-201">自訂指令碼，以指定指令碼的執行持續時間。</span><span class="sxs-lookup"><span data-stu-id="7d0ef-201">Customize the script to specify the duration of the scripts' execution.</span></span>

<span data-ttu-id="7d0ef-202">概括而言，指令碼會執行下列作業︰</span><span class="sxs-lookup"><span data-stu-id="7d0ef-202">At a high level, the scripts do the following:</span></span>

* <span data-ttu-id="7d0ef-203">列舉指定的 Azure 訂用帳戶 (或指定的伺服器清單) 中的所有伺服器。</span><span class="sxs-lookup"><span data-stu-id="7d0ef-203">Enumerates all servers in a given Azure subscription (or a specified list of servers).</span></span>
* <span data-ttu-id="7d0ef-204">執行每部伺服器的背景作業。</span><span class="sxs-lookup"><span data-stu-id="7d0ef-204">Runs a background job for each server.</span></span> <span data-ttu-id="7d0ef-205">作業會在迴圈中定期執行，並收集伺服器中所有集區的遙測資料。</span><span class="sxs-lookup"><span data-stu-id="7d0ef-205">The job runs in a loop at regular intervals and collects telemetry data for all the pools in the server.</span></span> <span data-ttu-id="7d0ef-206">然後將所收集的資料載入到指定的遙測資料庫。</span><span class="sxs-lookup"><span data-stu-id="7d0ef-206">It then loads the collected data into the specified telemetry database.</span></span>
* <span data-ttu-id="7d0ef-207">列舉每個集區中的資料庫清單，以收集資料庫資源使用量資料。</span><span class="sxs-lookup"><span data-stu-id="7d0ef-207">Enumerates a list of databases in each pool to collect the database resource usage data.</span></span> <span data-ttu-id="7d0ef-208">然後將所收集的資料載入到遙測資料庫。</span><span class="sxs-lookup"><span data-stu-id="7d0ef-208">It then loads the collected data into the telemetry database.</span></span>

<span data-ttu-id="7d0ef-209">您可以分析遙測資料庫中收集的度量，以監視彈性集區和資料庫的健康狀態。</span><span class="sxs-lookup"><span data-stu-id="7d0ef-209">The collected metrics in the telemetry database can be analyzed to monitor the health of elastic pools and the databases in it.</span></span> <span data-ttu-id="7d0ef-210">指令碼也會在遙測資料庫中安裝預先定義的資料表值函式 (TVF)，協助彙總指定時間範圍的度量。</span><span class="sxs-lookup"><span data-stu-id="7d0ef-210">The script also installs a pre-defined Table-Value function (TVF) in the telemetry database to help aggregate the metrics for a specified time window.</span></span> <span data-ttu-id="7d0ef-211">例如，TVF 的結果可用來顯示「在指定的時間範圍內具有最大 eDTU 使用率的前 N 個彈性集區」。</span><span class="sxs-lookup"><span data-stu-id="7d0ef-211">For example, results of the TVF can be used to show “top N elastic pools with the maximum eDTU utilization in a given time window.”</span></span> <span data-ttu-id="7d0ef-212">或者，使用分析工具 (例如 Excel 或 Power BI) 來查詢和分析所收集的資料。</span><span class="sxs-lookup"><span data-stu-id="7d0ef-212">Optionally, use analytic tools like Excel or Power BI to query and analyze the collected data.</span></span>

### <a name="example-retrieve-resource-consumption-metrics-for-an-elastic-pool-and-its-databases"></a><span data-ttu-id="7d0ef-213">範例︰擷取彈性集區和其資料庫的資源消耗度量</span><span class="sxs-lookup"><span data-stu-id="7d0ef-213">Example: retrieve resource consumption metrics for an elastic pool and its databases</span></span>
<span data-ttu-id="7d0ef-214">此範例會擷取指定彈性集區和其所有資料庫的耗用量度量資訊。</span><span class="sxs-lookup"><span data-stu-id="7d0ef-214">This example retrieves the consumption metrics for a given elastic pool and all its databases.</span></span> <span data-ttu-id="7d0ef-215">收集的資料會格式化並寫入.csv 格式檔案。</span><span class="sxs-lookup"><span data-stu-id="7d0ef-215">Collected data is formatted and written to a .csv formatted file.</span></span> <span data-ttu-id="7d0ef-216">可以使用 Excel 瀏覽檔案。</span><span class="sxs-lookup"><span data-stu-id="7d0ef-216">The file can be browsed with Excel.</span></span>

```PowerShell
$subscriptionId = '<Azure subscription id>'          # Azure subscription ID
$resourceGroupName = '<resource group name>'             # Resource Group
$serverName = <server name>                              # server name
$poolName = <elastic pool name>                          # pool name

# Login to Azure account and select the subscription.
Login-AzureRmAccount
Set-AzureRmContext -SubscriptionId $subscriptionId

# Get resource usage metrics for an elastic pool for the specified time interval.
$startTime = '4/27/2016 00:00:00'  # start time in UTC
$endTime = '4/27/2016 01:00:00'    # end time in UTC

# Construct the pool resource ID and retrive pool metrics at 5-minute granularity.
$poolResourceId = '/subscriptions/' + $subscriptionId + '/resourceGroups/' + $resourceGroupName + '/providers/Microsoft.Sql/servers/' + $serverName + '/elasticPools/' + $poolName
$poolMetrics = (Get-AzureRmMetric -ResourceId $poolResourceId -TimeGrain ([TimeSpan]::FromMinutes(5)) -StartTime $startTime -EndTime $endTime)

# Get the list of databases in this pool.
$dbList = Get-AzureRmSqlElasticPoolDatabase -ResourceGroupName $resourceGroupName -ServerName $serverName -ElasticPoolName $poolName

# Get resource usage metrics for a database in an elastic pool for the specified time interval.
$dbMetrics = @()
foreach ($db in $dbList)
{
     $dbResourceId = '/subscriptions/' + $subscriptionId + '/resourceGroups/' + $resourceGroupName + '/providers/Microsoft.Sql/servers/' + $serverName + '/databases/' + $db.DatabaseName
     $dbMetrics = $dbMetrics + (Get-AzureRmMetric -ResourceId $dbResourceId -TimeGrain ([TimeSpan]::FromMinutes(5)) -StartTime $startTime -EndTime $endTime)
}

#Optionally you can format the metrics and output as .csv file using the following script block.
$command = {
param($metricList, $outputFile)

# Format metrics into a table.
$table = @()
foreach($metric in $metricList) {
   foreach($metricValue in $metric.MetricValues) {
      $sx = New-Object PSObject -Property @{
      Timestamp = $metricValue.Timestamp.ToString()
      MetricName = $metric.Name;
      Average = $metricValue.Average;
      ResourceID = $metric.ResourceId
   }$table = $table += $sx
   }
}

# Output the metrics into a .csv file.
write-output $table | Export-csv -Path $outputFile -Append -NoTypeInformation
}

# Format and output pool metrics
Invoke-Command -ScriptBlock $command -ArgumentList $poolMetrics,c:\temp\poolmetrics.csv

# Format and output database metrics
Invoke-Command -ScriptBlock $command -ArgumentList $dbMetrics,c:\temp\dbmetrics.csv
```

## <a name="latency-of-elastic-pool-operations"></a><span data-ttu-id="7d0ef-217">彈性集區的作業延遲</span><span class="sxs-lookup"><span data-stu-id="7d0ef-217">Latency of elastic pool operations</span></span>
* <span data-ttu-id="7d0ef-218">每個資料庫的最小 eDTU 數或每個資料庫的最大 eDTU 數變更作業通常在 5 分鐘內即可完成。</span><span class="sxs-lookup"><span data-stu-id="7d0ef-218">Changing the min eDTUs per database or max eDTUs per database typically completes in 5 minutes or less.</span></span>
* <span data-ttu-id="7d0ef-219">集區的 eDTU 變更作業，需視集區中所有資料庫使用的總空間量而定。</span><span class="sxs-lookup"><span data-stu-id="7d0ef-219">Changing the eDTUs per pool depends on the total amount of space used by all databases in the pool.</span></span> <span data-ttu-id="7d0ef-220">變更作業平均每 100 GB 會在 90 分鐘以內完成。</span><span class="sxs-lookup"><span data-stu-id="7d0ef-220">Changes average 90 minutes or less per 100 GB.</span></span> <span data-ttu-id="7d0ef-221">舉例來說，如果集區中所有資料庫使用的總空間為 200 GB，則每集區 eDTU 變更作業的預期延遲時間會少於 3 小時。</span><span class="sxs-lookup"><span data-stu-id="7d0ef-221">For example, if the total space used by all databases in the pool is 200 GB, then the expected latency for changing the pool eDTU per pool is 3 hours or less.</span></span>



## <a name="next-steps"></a><span data-ttu-id="7d0ef-222">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7d0ef-222">Next steps</span></span>
* <span data-ttu-id="7d0ef-223">[建立彈性工作](sql-database-elastic-jobs-overview.md) ：彈性工作可讓您對集區中任意數目的資料庫執行 T-SQL 指令碼。</span><span class="sxs-lookup"><span data-stu-id="7d0ef-223">[Create elastic jobs](sql-database-elastic-jobs-overview.md) Elastic jobs let you run T-SQL scripts against any number of databases in the pool.</span></span>
* <span data-ttu-id="7d0ef-224">請參閱[使用 Azure SQL Database 相應放大](sql-database-elastic-scale-introduction.md)︰使用彈性工具相應放大、移動資料、查詢或建立交易。</span><span class="sxs-lookup"><span data-stu-id="7d0ef-224">See [Scaling out with Azure SQL Database](sql-database-elastic-scale-introduction.md): use elastic tools to scale out, move data, query, or create transactions.</span></span>
