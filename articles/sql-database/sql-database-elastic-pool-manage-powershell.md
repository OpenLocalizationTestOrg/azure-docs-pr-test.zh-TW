---
title: "PowerShell：建立及管理 Azure SQL 彈性集區 | Microsoft Docs"
description: "深入了解如何 toouse PowerShell toomanage 彈性集區。"
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
ms.openlocfilehash: 92de2a4b243dcc74502064e9d2c31682691753d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-an-elastic-pool-with-powershell"></a><span data-ttu-id="4d6ec-103">使用 PowerShell 建立及管理彈性集區</span><span class="sxs-lookup"><span data-stu-id="4d6ec-103">Create and manage an elastic pool with PowerShell</span></span>
<span data-ttu-id="4d6ec-104">本主題說明如何 toocreate 及管理可擴充[彈性集區](sql-database-elastic-pool.md)使用 PowerShell。</span><span class="sxs-lookup"><span data-stu-id="4d6ec-104">This topic shows you how toocreate and manage scalable [elastic pools](sql-database-elastic-pool.md) with PowerShell.</span></span>  <span data-ttu-id="4d6ec-105">您也可以建立和管理 Azure 的彈性集區，以使用 hello [Azure 入口網站](https://portal.azure.com/)，REST API 或[C#](sql-database-elastic-pool-manage-csharp.md)。</span><span class="sxs-lookup"><span data-stu-id="4d6ec-105">You can also create and manage an Azure elastic pool using hello [Azure portal](https://portal.azure.com/), REST API, or [C#](sql-database-elastic-pool-manage-csharp.md).</span></span> <span data-ttu-id="4d6ec-106">您也可以使用 [Transact-SQL](sql-database-elastic-pool-manage-tsql.md) 來建立資料庫並將它移入和移出彈性集區。</span><span class="sxs-lookup"><span data-stu-id="4d6ec-106">You can also create and move databases into and out of elastic pools using [Transact-SQL](sql-database-elastic-pool-manage-tsql.md).</span></span>

[!INCLUDE [Start your PowerShell session](../../includes/sql-database-powershell.md)]

## <a name="create-an-elastic-pool"></a><span data-ttu-id="4d6ec-107">建立彈性集區</span><span class="sxs-lookup"><span data-stu-id="4d6ec-107">Create an elastic pool</span></span>
<span data-ttu-id="4d6ec-108">hello[新增 AzureRmSqlElasticPool](/powershell/module/azurerm.sql/new-azurermsqlelasticpool) cmdlet 會建立彈性集區。</span><span class="sxs-lookup"><span data-stu-id="4d6ec-108">hello [New-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/new-azurermsqlelasticpool) cmdlet creates an elastic pool.</span></span> <span data-ttu-id="4d6ec-109">每個集區、 min 和 max Dtu eDTU hello 值受到 hello 的服務層值 （Basic、 Standard、 Premium 或 Premium RS）。</span><span class="sxs-lookup"><span data-stu-id="4d6ec-109">hello values for eDTU per pool, min, and max DTUs are constrained by hello service tier value (Basic, Standard, Premium, or Premium RS).</span></span> <span data-ttu-id="4d6ec-110">請參閱[彈性集區和集區資料庫的 eDTU 和儲存體限制](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools)。</span><span class="sxs-lookup"><span data-stu-id="4d6ec-110">See [eDTU and storage limits for elastic pools and pooled databases](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools).</span></span>

```PowerShell
New-AzureRmSqlElasticPool -ResourceGroupName "resourcegroup1" -ServerName "server1" -ElasticPoolName "elasticpool1" -Edition "Standard" -Dtu 400 -DatabaseDtuMin 10 -DatabaseDtuMax 100
```

## <a name="create-a-pooled-database-in-an-elastic-pool"></a><span data-ttu-id="4d6ec-111">在彈性集區中建立集區資料庫</span><span class="sxs-lookup"><span data-stu-id="4d6ec-111">Create a pooled database in an elastic pool</span></span>
<span data-ttu-id="4d6ec-112">使用 hello[新增 AzureRmSqlDatabase](/powershell/module/azurerm.sql/new-azurermsqldatabase) cmdlet 和設定 hello **ElasticPoolName**參數 toohello 目標集區。</span><span class="sxs-lookup"><span data-stu-id="4d6ec-112">Use hello [New-AzureRmSqlDatabase](/powershell/module/azurerm.sql/new-azurermsqldatabase) cmdlet and set hello **ElasticPoolName** parameter toohello target pool.</span></span> <span data-ttu-id="4d6ec-113">toomove 現有的資料庫至彈性集區，請參閱[將資料庫移入彈性集區](sql-database-elastic-pool-manage-powershell.md#move-a-database-into-an-elastic-pool)。</span><span class="sxs-lookup"><span data-stu-id="4d6ec-113">toomove an existing database into an elastic pool, see [Move a database into an elastic pool](sql-database-elastic-pool-manage-powershell.md#move-a-database-into-an-elastic-pool).</span></span>

```PowerShell
New-AzureRmSqlDatabase -ResourceGroupName "resourcegroup1" -ServerName "server1" -DatabaseName "database1" -ElasticPoolName "elasticpool1"
```

### <a name="complete-script"></a><span data-ttu-id="4d6ec-114">完整的指令碼</span><span class="sxs-lookup"><span data-stu-id="4d6ec-114">Complete script</span></span>
<span data-ttu-id="4d6ec-115">此指令碼會建立 Azure 資源群組和伺服器。</span><span class="sxs-lookup"><span data-stu-id="4d6ec-115">This script creates an Azure resource group and a server.</span></span> <span data-ttu-id="4d6ec-116">出現提示時，提供系統管理員使用者名稱和密碼適用於 hello 新伺服器 （沒有您的 Azure 認證）。</span><span class="sxs-lookup"><span data-stu-id="4d6ec-116">When prompted, supply an administrator username and password for hello new server (not your Azure credentials).</span></span>

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

## <a name="create-an-elastic-pool-and-add-multiple-pooled-databases"></a><span data-ttu-id="4d6ec-117">建立彈性集區並新增多個集區資料庫</span><span class="sxs-lookup"><span data-stu-id="4d6ec-117">Create an elastic pool and add multiple pooled databases</span></span>
<span data-ttu-id="4d6ec-118">建立的彈性集區中的許多資料庫可能需要完成使用 hello 入口網站或 PowerShell cmdlet，一次建立單一資料庫時的時間。</span><span class="sxs-lookup"><span data-stu-id="4d6ec-118">Creation of many databases in an elastic pool can take time when done using hello portal or PowerShell cmdlets that create only a single database at a time.</span></span> <span data-ttu-id="4d6ec-119">tooautomate 建立成彈性集區，請參閱[CreateOrUpdateElasticPoolAndPopulate ](https://gist.github.com/billgib/d80c7687b17355d3c2ec8042323819ae)。</span><span class="sxs-lookup"><span data-stu-id="4d6ec-119">tooautomate creation into an elastic pool, see [CreateOrUpdateElasticPoolAndPopulate ](https://gist.github.com/billgib/d80c7687b17355d3c2ec8042323819ae).</span></span>

## <a name="move-a-database-into-an-elastic-pool"></a><span data-ttu-id="4d6ec-120">將資料庫移入彈性集區</span><span class="sxs-lookup"><span data-stu-id="4d6ec-120">Move a database into an elastic pool</span></span>
<span data-ttu-id="4d6ec-121">您可以將資料庫移入或移出 hello 的彈性集區[組 AzureRmSqlDatabase](/powershell/module/azurerm.sql/set-azurermsqlelasticpool)。</span><span class="sxs-lookup"><span data-stu-id="4d6ec-121">You can move a database into or out of an elastic pool with hello [Set-AzureRmSqlDatabase](/powershell/module/azurerm.sql/set-azurermsqlelasticpool).</span></span>

```PowerShell
Set-AzureRmSqlDatabase -ResourceGroupName "resourcegroup1" -ServerName "server1" -DatabaseName "database1" -ElasticPoolName "elasticpool1"
```

## <a name="change-performance-settings-of-an-elastic-pool"></a><span data-ttu-id="4d6ec-122">變更彈性集區的效能設定</span><span class="sxs-lookup"><span data-stu-id="4d6ec-122">Change performance settings of an elastic pool</span></span>
<span data-ttu-id="4d6ec-123">當效能將會降低時，您可以變更 hello hello 集區 tooaccommodate 成長設定。</span><span class="sxs-lookup"><span data-stu-id="4d6ec-123">When performance suffers, you can change hello settings of hello pool tooaccommodate growth.</span></span> <span data-ttu-id="4d6ec-124">使用 hello[組 AzureRmSqlElasticPool](/powershell/module/azurerm.sql/set-azurermsqlelasticpool) cmdlet。</span><span class="sxs-lookup"><span data-stu-id="4d6ec-124">Use hello [Set-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/set-azurermsqlelasticpool) cmdlet.</span></span> <span data-ttu-id="4d6ec-125">每個集區設定 hello-Dtu 參數 toohello Edtu。</span><span class="sxs-lookup"><span data-stu-id="4d6ec-125">Set hello -Dtu parameter toohello eDTUs per pool.</span></span> <span data-ttu-id="4d6ec-126">請參閱 [eDTU 和儲存體限制](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools)以了解有哪些可能的值。</span><span class="sxs-lookup"><span data-stu-id="4d6ec-126">See [eDTU and storage limits](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools) for possible values.</span></span>

```PowerShell
Set-AzureRmSqlElasticPool -ResourceGroupName “resourcegroup1” -ServerName “server1” -ElasticPoolName “elasticpool1” -Dtu 1200 -DatabaseDtuMax 100 -DatabaseDtuMin 50
```

## <a name="change-hello-storage-limit-for-an-elastic-pool"></a><span data-ttu-id="4d6ec-127">變更 hello 彈性集區的存放裝置限制</span><span class="sxs-lookup"><span data-stu-id="4d6ec-127">Change hello storage limit for an elastic pool</span></span>

<span data-ttu-id="4d6ec-128">使用 hello[組 AzureRmSqlElasticPool](/powershell/module/azurerm.sql/set-azurermsqlelasticpool) cmdlet tooset hello _-StorageMB_參數。</span><span class="sxs-lookup"><span data-stu-id="4d6ec-128">Use hello [Set-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/set-azurermsqlelasticpool) cmdlet tooset hello _-StorageMB_ parameter.</span></span> <span data-ttu-id="4d6ec-129">提供 hello 儲存限制 （mb） (例如，2097152 集 hello 儲存體限制 too2 TB)。</span><span class="sxs-lookup"><span data-stu-id="4d6ec-129">Provide hello storage limit in MB (for example, 2097152 sets hello storage limit too2 TB).</span></span> <span data-ttu-id="4d6ec-130">請參閱 [eDTU 和儲存體限制](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools)以了解有哪些可能的值。</span><span class="sxs-lookup"><span data-stu-id="4d6ec-130">See [eDTU and storage limits](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools) for possible values.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4d6ec-131">每個 Premium 1500 Edtu 集區的集區的 hello 預設最大的資料儲存體或多個是 750 GB。</span><span class="sxs-lookup"><span data-stu-id="4d6ec-131">hello default max data storage per pool for Premium pools with 1500 eDTUs or more is 750 GB.</span></span> <span data-ttu-id="4d6ec-132">較高的 tooobtain hello_每個集區的資料儲存體大小上限_，必須明確設定 hello 儲存體限制。</span><span class="sxs-lookup"><span data-stu-id="4d6ec-132">tooobtain hello higher _max data storage size per pool_, hello storage limit must be explicitly set.</span></span> <span data-ttu-id="4d6ec-133">Premium 750 GB 以上的儲存體集區目前為公開預覽，在下列區域的 hello： 美國東部 2、 美國西部、 美國 Gov 維吉尼亞州、 西歐、 德國中央、 東南亞、 日本東部、 澳洲東部、 加拿大中央和加拿大東部。</span><span class="sxs-lookup"><span data-stu-id="4d6ec-133">Premium pools with more than 750 GB of storage is currently in public preview in hello following regions: East US 2, West US, US Gov Virginia, West Europe, Germany Central, Southeast Asia, Japan East, Australia East, Canada Central, and Canada East.</span></span>

```PowerShell
Set-AzureRmSqlElasticPool -ServerName "server1" -ElasticPoolName “elasticpool1” -StorageMB 2097152
```

## <a name="get-hello-status-of-pool-operations"></a><span data-ttu-id="4d6ec-134">取得集區作業的 hello 狀態</span><span class="sxs-lookup"><span data-stu-id="4d6ec-134">Get hello status of pool operations</span></span>
<span data-ttu-id="4d6ec-135">建立彈性集區可能會很耗時。</span><span class="sxs-lookup"><span data-stu-id="4d6ec-135">Creating an elastic pool can take time.</span></span> <span data-ttu-id="4d6ec-136">集區的作業包括建立和更新、 使用 hello tootrack hello 狀態[Get AzureRmSqlElasticPoolActivity](/powershell/module/azurerm.sql/get-azurermsqlelasticpoolactivity) cmdlet。</span><span class="sxs-lookup"><span data-stu-id="4d6ec-136">tootrack hello status of pool operations including creation and updates, use hello [Get-AzureRmSqlElasticPoolActivity](/powershell/module/azurerm.sql/get-azurermsqlelasticpoolactivity) cmdlet.</span></span>

```PowerShell
Get-AzureRmSqlElasticPoolActivity -ResourceGroupName “resourcegroup1” -ServerName “server1” -ElasticPoolName “elasticpool1”
```

## <a name="get-hello-status-of-moving-a-database-into-and-out-of-an-elastic-pool"></a><span data-ttu-id="4d6ec-137">取得彈性集區中來回移動資料庫 hello 狀態</span><span class="sxs-lookup"><span data-stu-id="4d6ec-137">Get hello status of moving a database into and out of an elastic pool</span></span>
<span data-ttu-id="4d6ec-138">移動資料庫可能會很耗時。</span><span class="sxs-lookup"><span data-stu-id="4d6ec-138">Moving a database can take time.</span></span> <span data-ttu-id="4d6ec-139">追蹤使用 hello 移動狀態[Get AzureRmSqlDatabaseActivity](/powershell/module/azurerm.sql/get-azurermsqldatabaseactivity) cmdlet。</span><span class="sxs-lookup"><span data-stu-id="4d6ec-139">Track a move status using hello [Get-AzureRmSqlDatabaseActivity](/powershell/module/azurerm.sql/get-azurermsqldatabaseactivity) cmdlet.</span></span>

```PowerShell
Get-AzureRmSqlDatabaseActivity -ResourceGroupName "resourcegroup1" -ServerName "server1" -DatabaseName "database1" -ElasticPoolName "elasticpool1"
```

## <a name="get-resource-usage-data-for-an-elastic-pool"></a><span data-ttu-id="4d6ec-140">取得彈性集區的資源使用量資料</span><span class="sxs-lookup"><span data-stu-id="4d6ec-140">Get resource usage data for an elastic pool</span></span>
<span data-ttu-id="4d6ec-141">可以 hello 資源集區限制的百分比表示的形式擷取的計量：</span><span class="sxs-lookup"><span data-stu-id="4d6ec-141">Metrics that can be retrieved as a percentage of hello resource pool limit:</span></span>

| <span data-ttu-id="4d6ec-142">度量名稱</span><span class="sxs-lookup"><span data-stu-id="4d6ec-142">Metric name</span></span> | <span data-ttu-id="4d6ec-143">說明</span><span class="sxs-lookup"><span data-stu-id="4d6ec-143">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="4d6ec-144">cpu\_percent</span><span class="sxs-lookup"><span data-stu-id="4d6ec-144">cpu\_percent</span></span> |<span data-ttu-id="4d6ec-145">平均計算使用率百分比 hello hello 集區限制。</span><span class="sxs-lookup"><span data-stu-id="4d6ec-145">Average compute utilization in percentage of hello limit of hello pool.</span></span> |
| <span data-ttu-id="4d6ec-146">實體\_資料\_讀取\_百分比</span><span class="sxs-lookup"><span data-stu-id="4d6ec-146">physical\_data\_read\_percent</span></span> |<span data-ttu-id="4d6ec-147">計算平均 I/O 使用率，以根據 hello hello 集區限制的百分比表示。</span><span class="sxs-lookup"><span data-stu-id="4d6ec-147">Average I/O utilization in percentage based on hello limit of hello pool.</span></span> |
| <span data-ttu-id="4d6ec-148">記錄檔\_撰寫\_百分比</span><span class="sxs-lookup"><span data-stu-id="4d6ec-148">log\_write\_percent</span></span> |<span data-ttu-id="4d6ec-149">平均寫入資源使用率 hello hello 集區限制的百分比表示。</span><span class="sxs-lookup"><span data-stu-id="4d6ec-149">Average write resource utilization in percentage of hello limit of hello pool.</span></span> |
| <span data-ttu-id="4d6ec-150">DTU\_耗用量\_百分比</span><span class="sxs-lookup"><span data-stu-id="4d6ec-150">DTU\_consumption\_percent</span></span> |<span data-ttu-id="4d6ec-151">EDTU 平均使用率百分比 hello 集區 eDTU 限制</span><span class="sxs-lookup"><span data-stu-id="4d6ec-151">Average eDTU utilization in percentage of eDTU limit for hello pool</span></span> |
| <span data-ttu-id="4d6ec-152">儲存體\_percent</span><span class="sxs-lookup"><span data-stu-id="4d6ec-152">storage\_percent</span></span> |<span data-ttu-id="4d6ec-153">平均的儲存體使用率百分比 hello hello 集區的儲存體限制。</span><span class="sxs-lookup"><span data-stu-id="4d6ec-153">Average storage utilization in percentage of hello storage limit of hello pool.</span></span> |
| <span data-ttu-id="4d6ec-154">背景工作角色\_百分比</span><span class="sxs-lookup"><span data-stu-id="4d6ec-154">workers\_percent</span></span> |<span data-ttu-id="4d6ec-155">最大並行工作者 （要求），以根據 hello hello 集區限制的百分比表示。</span><span class="sxs-lookup"><span data-stu-id="4d6ec-155">Maximum concurrent workers (requests) in percentage based on hello limit of hello pool.</span></span> |
| <span data-ttu-id="4d6ec-156">工作階段\_百分比</span><span class="sxs-lookup"><span data-stu-id="4d6ec-156">sessions\_percent</span></span> |<span data-ttu-id="4d6ec-157">最大並行工作階段 hello hello 集區限制的百分比。</span><span class="sxs-lookup"><span data-stu-id="4d6ec-157">Maximum concurrent sessions in percentage based on hello limit of hello pool.</span></span> |
| <span data-ttu-id="4d6ec-158">eDTU_limit</span><span class="sxs-lookup"><span data-stu-id="4d6ec-158">eDTU_limit</span></span> |<span data-ttu-id="4d6ec-159">間隔期間此彈性集區目前最大的彈性集區 DTU 設定。</span><span class="sxs-lookup"><span data-stu-id="4d6ec-159">Current max elastic pool DTU setting for this elastic pool during this interval.</span></span> |
| <span data-ttu-id="4d6ec-160">儲存體\_限制</span><span class="sxs-lookup"><span data-stu-id="4d6ec-160">storage\_limit</span></span> |<span data-ttu-id="4d6ec-161">間隔期間此彈性集區目前最大的彈性集區儲存體限制設定 (MB)。</span><span class="sxs-lookup"><span data-stu-id="4d6ec-161">Current max elastic pool storage limit setting for this elastic pool in megabytes during this interval.</span></span> |
| <span data-ttu-id="4d6ec-162">eDTU\_使用</span><span class="sxs-lookup"><span data-stu-id="4d6ec-162">eDTU\_used</span></span> |<span data-ttu-id="4d6ec-163">在這個間隔中的 hello 集區所使用的平均 Edtu。</span><span class="sxs-lookup"><span data-stu-id="4d6ec-163">Average eDTUs used by hello pool in this interval.</span></span> |
| <span data-ttu-id="4d6ec-164">儲存體\_使用</span><span class="sxs-lookup"><span data-stu-id="4d6ec-164">storage\_used</span></span> |<span data-ttu-id="4d6ec-165">平均 hello 集區，以位元組為單位的此時間間隔中所使用的儲存體</span><span class="sxs-lookup"><span data-stu-id="4d6ec-165">Average storage used by hello pool in this interval in bytes</span></span> |

<span data-ttu-id="4d6ec-166">**度量資料粒度/保留期限：**</span><span class="sxs-lookup"><span data-stu-id="4d6ec-166">**Metrics granularity/retention periods:**</span></span>

* <span data-ttu-id="4d6ec-167">系統會以 5 分鐘的資料粒度傳回資料。</span><span class="sxs-lookup"><span data-stu-id="4d6ec-167">Data is returned at 5-minute granularity.</span></span>  
* <span data-ttu-id="4d6ec-168">資料會保留 35 天。</span><span class="sxs-lookup"><span data-stu-id="4d6ec-168">Data retention is 35 days.</span></span>  

<span data-ttu-id="4d6ec-169">此指令程式和應用程式開發介面可在一個呼叫 too1000 資料列 （大約 3 天在 5 分鐘的資料粒度的資料） 中擷取的資料列的 hello 數目的限制。</span><span class="sxs-lookup"><span data-stu-id="4d6ec-169">This cmdlet and API limits hello number of rows that can be retrieved in one call too1000 rows (about 3 days of data at 5-minute granularity).</span></span> <span data-ttu-id="4d6ec-170">但此命令可呼叫多次以不同的開始/結束時間間隔 tooretrieve 詳細資料</span><span class="sxs-lookup"><span data-stu-id="4d6ec-170">But this command can be called multiple times with different start/end time intervals tooretrieve more data</span></span>

<span data-ttu-id="4d6ec-171">tooretrieve hello 度量：</span><span class="sxs-lookup"><span data-stu-id="4d6ec-171">tooretrieve hello metrics:</span></span>

```PowerShell
$metrics = (Get-AzureRmMetric -ResourceId /subscriptions/<subscriptionId>/resourceGroups/FabrikamData01/providers/Microsoft.Sql/servers/fabrikamsqldb02/elasticPools/franchisepool -TimeGrain ([TimeSpan]::FromMinutes(5)) -StartTime "4/18/2015" -EndTime "4/21/2015")
```

## <a name="get-resource-usage-data-for-a-database-in-an-elastic-pool"></a><span data-ttu-id="4d6ec-172">取得彈性集區中資料庫的資源使用量資料</span><span class="sxs-lookup"><span data-stu-id="4d6ec-172">Get resource usage data for a database in an elastic pool</span></span>
<span data-ttu-id="4d6ec-173">這些 Api 會 hello 相同 hello 應用程式開發介面，用於監視的單一資料庫，除了下列語意差異的 hello hello 資源使用情況： 擷取的計量均會為每個資料庫最大的 edtu 數目 （或對等端點 hello 的百分比表示基礎度量，例如 CPU 或 IO） 之集區設定。</span><span class="sxs-lookup"><span data-stu-id="4d6ec-173">These APIs are hello same as hello APIs used for monitoring hello resource utilization of a single database, except for hello following semantic difference: metrics retrieved are expressed as a percentage of hello per database max eDTUs (or equivalent cap for hello underlying metric like CPU or IO) set for that pool.</span></span> <span data-ttu-id="4d6ec-174">例如，任何這些度量的 50%使用率表示 hello 特定的資源耗用量並在每個資料庫上限會限制該資源 hello 父集區中的 hello 50%。</span><span class="sxs-lookup"><span data-stu-id="4d6ec-174">For example, 50% utilization of any of these metrics indicates that hello specific resource consumption is at 50% of hello per database cap limit for that resource in hello parent pool.</span></span>

<span data-ttu-id="4d6ec-175">tooretrieve hello 度量：</span><span class="sxs-lookup"><span data-stu-id="4d6ec-175">tooretrieve hello metrics:</span></span>

```PowerShell
$metrics = (Get-AzureRmMetric -ResourceId /subscriptions/<subscriptionId>/resourceGroups/FabrikamData01/providers/Microsoft.Sql/servers/fabrikamsqldb02/databases/myDB -TimeGrain ([TimeSpan]::FromMinutes(5)) -StartTime "4/18/2015" -EndTime "4/21/2015")
```

## <a name="add-an-alert-tooan-elastic-pool-resource"></a><span data-ttu-id="4d6ec-176">加入警示 tooan 彈性集區資源</span><span class="sxs-lookup"><span data-stu-id="4d6ec-176">Add an alert tooan elastic pool resource</span></span>
<span data-ttu-id="4d6ec-177">您可以加入警示規則 tooan 彈性集區 toosend 電子郵件通知，或太警示字串[URL 端點](https://msdn.microsoft.com/library/mt718036.aspx)hello 彈性集區時叫用您設定使用率閾值。</span><span class="sxs-lookup"><span data-stu-id="4d6ec-177">You can add alert rules tooan elastic pool toosend email notifications or alert strings too[URL endpoints](https://msdn.microsoft.com/library/mt718036.aspx) when hello elastic pool hits a utilization threshold that you set up.</span></span> <span data-ttu-id="4d6ec-178">使用 hello 新增 AzureRmMetricAlertRule 指令程式。</span><span class="sxs-lookup"><span data-stu-id="4d6ec-178">Use hello Add-AzureRmMetricAlertRule cmdlet.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4d6ec-179">監視彈性集區的資源使用率至少有 5 分鐘的延遲。</span><span class="sxs-lookup"><span data-stu-id="4d6ec-179">Resource utilization monitoring for elastic pools has a lag of at least 5 minutes.</span></span> <span data-ttu-id="4d6ec-180">目前不支援將彈性集區的警示設定為小於 10 分鐘。</span><span class="sxs-lookup"><span data-stu-id="4d6ec-180">Setting alerts of less than 10 minutes for elastic pools is not currently supported.</span></span> <span data-ttu-id="4d6ec-181">彈性集區以句號的任何警示設定 (稱為參數"-WindowSize"PowerShell API 中) 的 10 分鐘內不一定會觸發。</span><span class="sxs-lookup"><span data-stu-id="4d6ec-181">Any alerts set for elastic pools with a period (parameter called “-WindowSize” in PowerShell API) of less than 10 minutes may not be triggered.</span></span> <span data-ttu-id="4d6ec-182">請確定您針對彈性集區定義的任何警示都會使用 10 分鐘以上的期間 (WindowSize)。</span><span class="sxs-lookup"><span data-stu-id="4d6ec-182">Make sure that any alerts you define for elastic pools use a period (WindowSize) of 10 minutes or more.</span></span>
>
>

<span data-ttu-id="4d6ec-183">此範例會新增一個可在彈性集區 eDTU 耗用量超過特定閾值時接獲通知的警示。</span><span class="sxs-lookup"><span data-stu-id="4d6ec-183">This example adds an alert for getting notified when an elastic pool’s eDTU consumption goes above certain threshold.</span></span>

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

<span data-ttu-id="4d6ec-184">如需詳細資訊，請參閱[在 Azure 入口網站中建立 SQL Database 警示](sql-database-insights-alerts-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="4d6ec-184">For more information, see [create SQL Database alerts in Azure portal](sql-database-insights-alerts-portal.md).</span></span>

## <a name="add-alerts-tooall-databases-in-an-elastic-pool"></a><span data-ttu-id="4d6ec-185">在彈性集區中新增警示 tooall 資料庫</span><span class="sxs-lookup"><span data-stu-id="4d6ec-185">Add alerts tooall databases in an elastic pool</span></span>
<span data-ttu-id="4d6ec-186">您可以加入警示規則，在彈性集區 toosend tooall 資料庫電子郵件通知，或太警示字串[URL 端點](https://msdn.microsoft.com/library/mt718036.aspx)資源時達到 hello 警示所設定的使用率閾值。</span><span class="sxs-lookup"><span data-stu-id="4d6ec-186">You can add alert rules tooall database in an elastic pool toosend email notifications or alert strings too[URL endpoints](https://msdn.microsoft.com/library/mt718036.aspx) when a resource hits a utilization threshold set up by hello alert.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4d6ec-187">監視彈性集區的資源使用率至少有 5 分鐘的延遲。</span><span class="sxs-lookup"><span data-stu-id="4d6ec-187">Resource utilization monitoring for elastic pools has a lag of at least 5 minutes.</span></span> <span data-ttu-id="4d6ec-188">目前不支援將彈性集區的警示設定為小於 10 分鐘。</span><span class="sxs-lookup"><span data-stu-id="4d6ec-188">Setting alerts of less than 10 minutes for elastic pools is not currently supported.</span></span> <span data-ttu-id="4d6ec-189">彈性集區以句號的任何警示設定 (稱為參數"-WindowSize"PowerShell API 中) 的 10 分鐘內不一定會觸發。</span><span class="sxs-lookup"><span data-stu-id="4d6ec-189">Any alerts set for elastic pools with a period (parameter called “-WindowSize” in PowerShell API) of less than 10 minutes may not be triggered.</span></span> <span data-ttu-id="4d6ec-190">請確定您針對彈性集區定義的任何警示都會使用 10 分鐘以上的期間 (WindowSize)。</span><span class="sxs-lookup"><span data-stu-id="4d6ec-190">Make sure that any alerts you define for elastic pools use a period (WindowSize) of 10 minutes or more.</span></span>
>

<span data-ttu-id="4d6ec-191">這個範例會將該資料庫的 DTU 耗用量超過特定閾值時獲得通知彈性集區中的 hello 資料庫警示 tooeach。</span><span class="sxs-lookup"><span data-stu-id="4d6ec-191">This example adds an alert tooeach of hello databases in an elastic pool for getting notified when that database’s DTU consumption goes above certain threshold.</span></span>

```PowerShell
# Set up your resource ID configurations
$subscriptionId = '<Azure subscription id>'      # Azure subscription ID
$location = '<location'                          # Azure region
$resourceGroupName = '<resource group name>'     # Resource Group
$serverName = '<server name>'                    # server name
$poolName = '<elastic pool name>'                # pool name

# Get hello list of databases in this pool.
$dbList = Get-AzureRmSqlElasticPoolDatabase -ResourceGroupName $resourceGroupName -ServerName $serverName -ElasticPoolName $poolName

# Create an email action
$actionEmail = New-AzureRmAlertRuleEmail -SendToServiceOwners -CustomEmail JohnDoe@contoso.com

# Get resource usage metrics for a database in an elastic pool for hello specified time interval.
foreach ($db in $dbList)
{
    $dbResourceId = '/subscriptions/' + $subscriptionId + '/resourceGroups/' + $resourceGroupName + '/providers/Microsoft.Sql/servers/' + $serverName + '/databases/' + $db.DatabaseName

    # create a unique rule name
    $alertName = $db.DatabaseName + "- DTU consumption rule"

    # Create an alert rule for DTU_consumption_percent
    Add-AzureRMMetricAlertRule -Name $alertName  -Location $location -ResourceGroup $resourceGroupName -TargetResourceId $dbResourceId -MetricName "dtu_consumption_percent"  -Operator GreaterThan -Threshold 80 -TimeAggregationOperator Average -WindowSize 00:60:00 -Actions $actionEmail

    # drop hello alert rule
    #Remove-AzureRmAlertRule -ResourceGroup $resourceGroupName -Name $alertName
}
```

## <a name="collect-and-monitor-resource-usage-data-across-multiple-pools-in-a-subscription"></a><span data-ttu-id="4d6ec-192">收集和監視訂用帳戶中多個集區的資源使用量資料</span><span class="sxs-lookup"><span data-stu-id="4d6ec-192">Collect and monitor resource usage data across multiple pools in a subscription</span></span>
<span data-ttu-id="4d6ec-193">您的訂用帳戶中有多個資料庫，很麻煩 toomonitor 分別每個彈性集區。</span><span class="sxs-lookup"><span data-stu-id="4d6ec-193">When you have many databases in a subscription, it is cumbersome toomonitor each elastic pool separately.</span></span> <span data-ttu-id="4d6ec-194">相反地，SQL database 的 PowerShell cmdlet 和 T-SQL 查詢可以是結合的 toocollect 資源使用量資料從多個集區並將其資料庫的監視與分析的資源使用狀況。</span><span class="sxs-lookup"><span data-stu-id="4d6ec-194">Instead, SQL database PowerShell cmdlets and T-SQL queries can be combined toocollect resource usage data from multiple pools and their databases for monitoring and analysis of resource usage.</span></span> <span data-ttu-id="4d6ec-195">A[範例實作](https://github.com/Microsoft/sql-server-samples/tree/master/samples/manage/azure-sql-db-elastic-pools)設定的 powershell 指令碼找不到在 hello GitHub SQL Server 範例儲存機制，以及在其用途的文件以及 toouse 它。</span><span class="sxs-lookup"><span data-stu-id="4d6ec-195">A [sample implementation](https://github.com/Microsoft/sql-server-samples/tree/master/samples/manage/azure-sql-db-elastic-pools) of such a set of powershell scripts can be found in hello GitHub SQL Server samples repository along with documentation on what it does and how toouse it.</span></span>

<span data-ttu-id="4d6ec-196">toouse 實作此範例，請遵循下列步驟。</span><span class="sxs-lookup"><span data-stu-id="4d6ec-196">toouse this sample implementation, follow these steps.</span></span>

1. <span data-ttu-id="4d6ec-197">下載 hello[指令碼和文件](https://github.com/Microsoft/sql-server-samples/tree/master/samples/manage/azure-sql-db-elastic-pools):</span><span class="sxs-lookup"><span data-stu-id="4d6ec-197">Download hello [scripts and documentation](https://github.com/Microsoft/sql-server-samples/tree/master/samples/manage/azure-sql-db-elastic-pools):</span></span>
2. <span data-ttu-id="4d6ec-198">修改您的環境的 hello 指令碼。</span><span class="sxs-lookup"><span data-stu-id="4d6ec-198">Modify hello scripts for your environment.</span></span> <span data-ttu-id="4d6ec-199">指定裝載彈性集區的一或多部伺服器。</span><span class="sxs-lookup"><span data-stu-id="4d6ec-199">Specify one or more servers on which elastic pools are hosted.</span></span>
3. <span data-ttu-id="4d6ec-200">請指定其中 hello 收集度量資訊是儲存 toobe 遙測資料庫。</span><span class="sxs-lookup"><span data-stu-id="4d6ec-200">Specify a telemetry database where hello collected metrics are toobe stored.</span></span>
4. <span data-ttu-id="4d6ec-201">自訂 hello 指令碼 toospecify hello hello 指令碼的執行期間。</span><span class="sxs-lookup"><span data-stu-id="4d6ec-201">Customize hello script toospecify hello duration of hello scripts' execution.</span></span>

<span data-ttu-id="4d6ec-202">在高層級，hello 指令碼 hello 遵循：</span><span class="sxs-lookup"><span data-stu-id="4d6ec-202">At a high level, hello scripts do hello following:</span></span>

* <span data-ttu-id="4d6ec-203">列舉指定的 Azure 訂用帳戶 (或指定的伺服器清單) 中的所有伺服器。</span><span class="sxs-lookup"><span data-stu-id="4d6ec-203">Enumerates all servers in a given Azure subscription (or a specified list of servers).</span></span>
* <span data-ttu-id="4d6ec-204">執行每部伺服器的背景作業。</span><span class="sxs-lookup"><span data-stu-id="4d6ec-204">Runs a background job for each server.</span></span> <span data-ttu-id="4d6ec-205">hello 作業會在迴圈中定期執行，並收集遙測資料 hello server 中的所有 hello 集區。</span><span class="sxs-lookup"><span data-stu-id="4d6ec-205">hello job runs in a loop at regular intervals and collects telemetry data for all hello pools in hello server.</span></span> <span data-ttu-id="4d6ec-206">它然後 hello 收集資料載入 hello 指定的遙測的資料庫。</span><span class="sxs-lookup"><span data-stu-id="4d6ec-206">It then loads hello collected data into hello specified telemetry database.</span></span>
* <span data-ttu-id="4d6ec-207">列舉中每個集區 toocollect hello 資料庫資源使用狀況資料的資料庫清單。</span><span class="sxs-lookup"><span data-stu-id="4d6ec-207">Enumerates a list of databases in each pool toocollect hello database resource usage data.</span></span> <span data-ttu-id="4d6ec-208">它然後 hello 收集資料載入 hello 遙測的資料庫。</span><span class="sxs-lookup"><span data-stu-id="4d6ec-208">It then loads hello collected data into hello telemetry database.</span></span>

<span data-ttu-id="4d6ec-209">hello hello 遙測的資料庫中的收集的度量可以分析的 toomonitor hello 彈性集區和資料庫健全狀況 hello 中。</span><span class="sxs-lookup"><span data-stu-id="4d6ec-209">hello collected metrics in hello telemetry database can be analyzed toomonitor hello health of elastic pools and hello databases in it.</span></span> <span data-ttu-id="4d6ec-210">hello 指令碼也會預先定義的資料表值函式 (TVF) 安裝在 hello 遙測資料庫 toohelp hello 彙總的度量資訊。 指定的時間間隔。</span><span class="sxs-lookup"><span data-stu-id="4d6ec-210">hello script also installs a pre-defined Table-Value function (TVF) in hello telemetry database toohelp aggregate hello metrics for a specified time window.</span></span> <span data-ttu-id="4d6ec-211">比方說，是 hello TVF 的結果可以用 tooshow 「 前 n 個彈性集區以指定的時段中的 hello eDTU 最大使用率。 」</span><span class="sxs-lookup"><span data-stu-id="4d6ec-211">For example, results of hello TVF can be used tooshow “top N elastic pools with hello maximum eDTU utilization in a given time window.”</span></span> <span data-ttu-id="4d6ec-212">（選擇性） 使用分析工具，例如 Excel 或 Power BI tooquery 和分析 hello 收集資料。</span><span class="sxs-lookup"><span data-stu-id="4d6ec-212">Optionally, use analytic tools like Excel or Power BI tooquery and analyze hello collected data.</span></span>

### <a name="example-retrieve-resource-consumption-metrics-for-an-elastic-pool-and-its-databases"></a><span data-ttu-id="4d6ec-213">範例︰擷取彈性集區和其資料庫的資源消耗度量</span><span class="sxs-lookup"><span data-stu-id="4d6ec-213">Example: retrieve resource consumption metrics for an elastic pool and its databases</span></span>
<span data-ttu-id="4d6ec-214">這個範例會擷取指定之彈性集區和其所有資料庫的 hello 消耗度量。</span><span class="sxs-lookup"><span data-stu-id="4d6ec-214">This example retrieves hello consumption metrics for a given elastic pool and all its databases.</span></span> <span data-ttu-id="4d6ec-215">收集的資料格式化並寫入 tooa.csv 格式的檔案。</span><span class="sxs-lookup"><span data-stu-id="4d6ec-215">Collected data is formatted and written tooa .csv formatted file.</span></span> <span data-ttu-id="4d6ec-216">可使用 Excel 瀏覽 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="4d6ec-216">hello file can be browsed with Excel.</span></span>

```PowerShell
$subscriptionId = '<Azure subscription id>'          # Azure subscription ID
$resourceGroupName = '<resource group name>'             # Resource Group
$serverName = <server name>                              # server name
$poolName = <elastic pool name>                          # pool name

# Login tooAzure account and select hello subscription.
Login-AzureRmAccount
Set-AzureRmContext -SubscriptionId $subscriptionId

# Get resource usage metrics for an elastic pool for hello specified time interval.
$startTime = '4/27/2016 00:00:00'  # start time in UTC
$endTime = '4/27/2016 01:00:00'    # end time in UTC

# Construct hello pool resource ID and retrive pool metrics at 5-minute granularity.
$poolResourceId = '/subscriptions/' + $subscriptionId + '/resourceGroups/' + $resourceGroupName + '/providers/Microsoft.Sql/servers/' + $serverName + '/elasticPools/' + $poolName
$poolMetrics = (Get-AzureRmMetric -ResourceId $poolResourceId -TimeGrain ([TimeSpan]::FromMinutes(5)) -StartTime $startTime -EndTime $endTime)

# Get hello list of databases in this pool.
$dbList = Get-AzureRmSqlElasticPoolDatabase -ResourceGroupName $resourceGroupName -ServerName $serverName -ElasticPoolName $poolName

# Get resource usage metrics for a database in an elastic pool for hello specified time interval.
$dbMetrics = @()
foreach ($db in $dbList)
{
     $dbResourceId = '/subscriptions/' + $subscriptionId + '/resourceGroups/' + $resourceGroupName + '/providers/Microsoft.Sql/servers/' + $serverName + '/databases/' + $db.DatabaseName
     $dbMetrics = $dbMetrics + (Get-AzureRmMetric -ResourceId $dbResourceId -TimeGrain ([TimeSpan]::FromMinutes(5)) -StartTime $startTime -EndTime $endTime)
}

#Optionally you can format hello metrics and output as .csv file using hello following script block.
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

# Output hello metrics into a .csv file.
write-output $table | Export-csv -Path $outputFile -Append -NoTypeInformation
}

# Format and output pool metrics
Invoke-Command -ScriptBlock $command -ArgumentList $poolMetrics,c:\temp\poolmetrics.csv

# Format and output database metrics
Invoke-Command -ScriptBlock $command -ArgumentList $dbMetrics,c:\temp\dbmetrics.csv
```

## <a name="latency-of-elastic-pool-operations"></a><span data-ttu-id="4d6ec-217">彈性集區的作業延遲</span><span class="sxs-lookup"><span data-stu-id="4d6ec-217">Latency of elastic pool operations</span></span>
* <span data-ttu-id="4d6ec-218">變更每個資料庫或最大每個資料庫的 Edtu hello min Edtu 通常完成在 5 分鐘或更短。</span><span class="sxs-lookup"><span data-stu-id="4d6ec-218">Changing hello min eDTUs per database or max eDTUs per database typically completes in 5 minutes or less.</span></span>
* <span data-ttu-id="4d6ec-219">變更每個集區 edtu 數 （hello） 取決於 hello hello 集區中的所有資料庫所使用的空間數量總計。</span><span class="sxs-lookup"><span data-stu-id="4d6ec-219">Changing hello eDTUs per pool depends on hello total amount of space used by all databases in hello pool.</span></span> <span data-ttu-id="4d6ec-220">變更作業平均每 100 GB 會在 90 分鐘以內完成。</span><span class="sxs-lookup"><span data-stu-id="4d6ec-220">Changes average 90 minutes or less per 100 GB.</span></span> <span data-ttu-id="4d6ec-221">比方說，如果使用的總空間的 hello hello 集區中的所有資料庫都為 200 GB，則 hello 預期的變更 hello 每個集區的集區 eDTU 延遲都為 3 小時或更少。</span><span class="sxs-lookup"><span data-stu-id="4d6ec-221">For example, if hello total space used by all databases in hello pool is 200 GB, then hello expected latency for changing hello pool eDTU per pool is 3 hours or less.</span></span>



## <a name="next-steps"></a><span data-ttu-id="4d6ec-222">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4d6ec-222">Next steps</span></span>
* <span data-ttu-id="4d6ec-223">[建立彈性作業](sql-database-elastic-jobs-overview.md)彈性作業可讓您針對任意數目的 hello 集區中的資料庫執行 T-SQL 指令碼。</span><span class="sxs-lookup"><span data-stu-id="4d6ec-223">[Create elastic jobs](sql-database-elastic-jobs-overview.md) Elastic jobs let you run T-SQL scripts against any number of databases in hello pool.</span></span>
* <span data-ttu-id="4d6ec-224">請參閱[使用 Azure SQL Database 向外延展](sql-database-elastic-scale-introduction.md)： 使用彈性的工具 tooscale 外，移動資料、 查詢或建立的交易。</span><span class="sxs-lookup"><span data-stu-id="4d6ec-224">See [Scaling out with Azure SQL Database](sql-database-elastic-scale-introduction.md): use elastic tools tooscale out, move data, query, or create transactions.</span></span>
