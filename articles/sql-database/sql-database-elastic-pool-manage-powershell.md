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
# <a name="create-and-manage-an-elastic-pool-with-powershell"></a>使用 PowerShell 建立及管理彈性集區
本主題說明如何 toocreate 及管理可擴充[彈性集區](sql-database-elastic-pool.md)使用 PowerShell。  您也可以建立和管理 Azure 的彈性集區，以使用 hello [Azure 入口網站](https://portal.azure.com/)，REST API 或[C#](sql-database-elastic-pool-manage-csharp.md)。 您也可以使用 [Transact-SQL](sql-database-elastic-pool-manage-tsql.md) 來建立資料庫並將它移入和移出彈性集區。

[!INCLUDE [Start your PowerShell session](../../includes/sql-database-powershell.md)]

## <a name="create-an-elastic-pool"></a>建立彈性集區
hello[新增 AzureRmSqlElasticPool](/powershell/module/azurerm.sql/new-azurermsqlelasticpool) cmdlet 會建立彈性集區。 每個集區、 min 和 max Dtu eDTU hello 值受到 hello 的服務層值 （Basic、 Standard、 Premium 或 Premium RS）。 請參閱[彈性集區和集區資料庫的 eDTU 和儲存體限制](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools)。

```PowerShell
New-AzureRmSqlElasticPool -ResourceGroupName "resourcegroup1" -ServerName "server1" -ElasticPoolName "elasticpool1" -Edition "Standard" -Dtu 400 -DatabaseDtuMin 10 -DatabaseDtuMax 100
```

## <a name="create-a-pooled-database-in-an-elastic-pool"></a>在彈性集區中建立集區資料庫
使用 hello[新增 AzureRmSqlDatabase](/powershell/module/azurerm.sql/new-azurermsqldatabase) cmdlet 和設定 hello **ElasticPoolName**參數 toohello 目標集區。 toomove 現有的資料庫至彈性集區，請參閱[將資料庫移入彈性集區](sql-database-elastic-pool-manage-powershell.md#move-a-database-into-an-elastic-pool)。

```PowerShell
New-AzureRmSqlDatabase -ResourceGroupName "resourcegroup1" -ServerName "server1" -DatabaseName "database1" -ElasticPoolName "elasticpool1"
```

### <a name="complete-script"></a>完整的指令碼
此指令碼會建立 Azure 資源群組和伺服器。 出現提示時，提供系統管理員使用者名稱和密碼適用於 hello 新伺服器 （沒有您的 Azure 認證）。

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

## <a name="create-an-elastic-pool-and-add-multiple-pooled-databases"></a>建立彈性集區並新增多個集區資料庫
建立的彈性集區中的許多資料庫可能需要完成使用 hello 入口網站或 PowerShell cmdlet，一次建立單一資料庫時的時間。 tooautomate 建立成彈性集區，請參閱[CreateOrUpdateElasticPoolAndPopulate ](https://gist.github.com/billgib/d80c7687b17355d3c2ec8042323819ae)。

## <a name="move-a-database-into-an-elastic-pool"></a>將資料庫移入彈性集區
您可以將資料庫移入或移出 hello 的彈性集區[組 AzureRmSqlDatabase](/powershell/module/azurerm.sql/set-azurermsqlelasticpool)。

```PowerShell
Set-AzureRmSqlDatabase -ResourceGroupName "resourcegroup1" -ServerName "server1" -DatabaseName "database1" -ElasticPoolName "elasticpool1"
```

## <a name="change-performance-settings-of-an-elastic-pool"></a>變更彈性集區的效能設定
當效能將會降低時，您可以變更 hello hello 集區 tooaccommodate 成長設定。 使用 hello[組 AzureRmSqlElasticPool](/powershell/module/azurerm.sql/set-azurermsqlelasticpool) cmdlet。 每個集區設定 hello-Dtu 參數 toohello Edtu。 請參閱 [eDTU 和儲存體限制](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools)以了解有哪些可能的值。

```PowerShell
Set-AzureRmSqlElasticPool -ResourceGroupName “resourcegroup1” -ServerName “server1” -ElasticPoolName “elasticpool1” -Dtu 1200 -DatabaseDtuMax 100 -DatabaseDtuMin 50
```

## <a name="change-hello-storage-limit-for-an-elastic-pool"></a>變更 hello 彈性集區的存放裝置限制

使用 hello[組 AzureRmSqlElasticPool](/powershell/module/azurerm.sql/set-azurermsqlelasticpool) cmdlet tooset hello _-StorageMB_參數。 提供 hello 儲存限制 （mb） (例如，2097152 集 hello 儲存體限制 too2 TB)。 請參閱 [eDTU 和儲存體限制](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools)以了解有哪些可能的值。

> [!IMPORTANT]
> 每個 Premium 1500 Edtu 集區的集區的 hello 預設最大的資料儲存體或多個是 750 GB。 較高的 tooobtain hello_每個集區的資料儲存體大小上限_，必須明確設定 hello 儲存體限制。 Premium 750 GB 以上的儲存體集區目前為公開預覽，在下列區域的 hello： 美國東部 2、 美國西部、 美國 Gov 維吉尼亞州、 西歐、 德國中央、 東南亞、 日本東部、 澳洲東部、 加拿大中央和加拿大東部。

```PowerShell
Set-AzureRmSqlElasticPool -ServerName "server1" -ElasticPoolName “elasticpool1” -StorageMB 2097152
```

## <a name="get-hello-status-of-pool-operations"></a>取得集區作業的 hello 狀態
建立彈性集區可能會很耗時。 集區的作業包括建立和更新、 使用 hello tootrack hello 狀態[Get AzureRmSqlElasticPoolActivity](/powershell/module/azurerm.sql/get-azurermsqlelasticpoolactivity) cmdlet。

```PowerShell
Get-AzureRmSqlElasticPoolActivity -ResourceGroupName “resourcegroup1” -ServerName “server1” -ElasticPoolName “elasticpool1”
```

## <a name="get-hello-status-of-moving-a-database-into-and-out-of-an-elastic-pool"></a>取得彈性集區中來回移動資料庫 hello 狀態
移動資料庫可能會很耗時。 追蹤使用 hello 移動狀態[Get AzureRmSqlDatabaseActivity](/powershell/module/azurerm.sql/get-azurermsqldatabaseactivity) cmdlet。

```PowerShell
Get-AzureRmSqlDatabaseActivity -ResourceGroupName "resourcegroup1" -ServerName "server1" -DatabaseName "database1" -ElasticPoolName "elasticpool1"
```

## <a name="get-resource-usage-data-for-an-elastic-pool"></a>取得彈性集區的資源使用量資料
可以 hello 資源集區限制的百分比表示的形式擷取的計量：

| 度量名稱 | 說明 |
|:--- |:--- |
| cpu\_percent |平均計算使用率百分比 hello hello 集區限制。 |
| 實體\_資料\_讀取\_百分比 |計算平均 I/O 使用率，以根據 hello hello 集區限制的百分比表示。 |
| 記錄檔\_撰寫\_百分比 |平均寫入資源使用率 hello hello 集區限制的百分比表示。 |
| DTU\_耗用量\_百分比 |EDTU 平均使用率百分比 hello 集區 eDTU 限制 |
| 儲存體\_percent |平均的儲存體使用率百分比 hello hello 集區的儲存體限制。 |
| 背景工作角色\_百分比 |最大並行工作者 （要求），以根據 hello hello 集區限制的百分比表示。 |
| 工作階段\_百分比 |最大並行工作階段 hello hello 集區限制的百分比。 |
| eDTU_limit |間隔期間此彈性集區目前最大的彈性集區 DTU 設定。 |
| 儲存體\_限制 |間隔期間此彈性集區目前最大的彈性集區儲存體限制設定 (MB)。 |
| eDTU\_使用 |在這個間隔中的 hello 集區所使用的平均 Edtu。 |
| 儲存體\_使用 |平均 hello 集區，以位元組為單位的此時間間隔中所使用的儲存體 |

**度量資料粒度/保留期限：**

* 系統會以 5 分鐘的資料粒度傳回資料。  
* 資料會保留 35 天。  

此指令程式和應用程式開發介面可在一個呼叫 too1000 資料列 （大約 3 天在 5 分鐘的資料粒度的資料） 中擷取的資料列的 hello 數目的限制。 但此命令可呼叫多次以不同的開始/結束時間間隔 tooretrieve 詳細資料

tooretrieve hello 度量：

```PowerShell
$metrics = (Get-AzureRmMetric -ResourceId /subscriptions/<subscriptionId>/resourceGroups/FabrikamData01/providers/Microsoft.Sql/servers/fabrikamsqldb02/elasticPools/franchisepool -TimeGrain ([TimeSpan]::FromMinutes(5)) -StartTime "4/18/2015" -EndTime "4/21/2015")
```

## <a name="get-resource-usage-data-for-a-database-in-an-elastic-pool"></a>取得彈性集區中資料庫的資源使用量資料
這些 Api 會 hello 相同 hello 應用程式開發介面，用於監視的單一資料庫，除了下列語意差異的 hello hello 資源使用情況： 擷取的計量均會為每個資料庫最大的 edtu 數目 （或對等端點 hello 的百分比表示基礎度量，例如 CPU 或 IO） 之集區設定。 例如，任何這些度量的 50%使用率表示 hello 特定的資源耗用量並在每個資料庫上限會限制該資源 hello 父集區中的 hello 50%。

tooretrieve hello 度量：

```PowerShell
$metrics = (Get-AzureRmMetric -ResourceId /subscriptions/<subscriptionId>/resourceGroups/FabrikamData01/providers/Microsoft.Sql/servers/fabrikamsqldb02/databases/myDB -TimeGrain ([TimeSpan]::FromMinutes(5)) -StartTime "4/18/2015" -EndTime "4/21/2015")
```

## <a name="add-an-alert-tooan-elastic-pool-resource"></a>加入警示 tooan 彈性集區資源
您可以加入警示規則 tooan 彈性集區 toosend 電子郵件通知，或太警示字串[URL 端點](https://msdn.microsoft.com/library/mt718036.aspx)hello 彈性集區時叫用您設定使用率閾值。 使用 hello 新增 AzureRmMetricAlertRule 指令程式。

> [!IMPORTANT]
> 監視彈性集區的資源使用率至少有 5 分鐘的延遲。 目前不支援將彈性集區的警示設定為小於 10 分鐘。 彈性集區以句號的任何警示設定 (稱為參數"-WindowSize"PowerShell API 中) 的 10 分鐘內不一定會觸發。 請確定您針對彈性集區定義的任何警示都會使用 10 分鐘以上的期間 (WindowSize)。
>
>

此範例會新增一個可在彈性集區 eDTU 耗用量超過特定閾值時接獲通知的警示。

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

如需詳細資訊，請參閱[在 Azure 入口網站中建立 SQL Database 警示](sql-database-insights-alerts-portal.md)。

## <a name="add-alerts-tooall-databases-in-an-elastic-pool"></a>在彈性集區中新增警示 tooall 資料庫
您可以加入警示規則，在彈性集區 toosend tooall 資料庫電子郵件通知，或太警示字串[URL 端點](https://msdn.microsoft.com/library/mt718036.aspx)資源時達到 hello 警示所設定的使用率閾值。

> [!IMPORTANT]
> 監視彈性集區的資源使用率至少有 5 分鐘的延遲。 目前不支援將彈性集區的警示設定為小於 10 分鐘。 彈性集區以句號的任何警示設定 (稱為參數"-WindowSize"PowerShell API 中) 的 10 分鐘內不一定會觸發。 請確定您針對彈性集區定義的任何警示都會使用 10 分鐘以上的期間 (WindowSize)。
>

這個範例會將該資料庫的 DTU 耗用量超過特定閾值時獲得通知彈性集區中的 hello 資料庫警示 tooeach。

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

## <a name="collect-and-monitor-resource-usage-data-across-multiple-pools-in-a-subscription"></a>收集和監視訂用帳戶中多個集區的資源使用量資料
您的訂用帳戶中有多個資料庫，很麻煩 toomonitor 分別每個彈性集區。 相反地，SQL database 的 PowerShell cmdlet 和 T-SQL 查詢可以是結合的 toocollect 資源使用量資料從多個集區並將其資料庫的監視與分析的資源使用狀況。 A[範例實作](https://github.com/Microsoft/sql-server-samples/tree/master/samples/manage/azure-sql-db-elastic-pools)設定的 powershell 指令碼找不到在 hello GitHub SQL Server 範例儲存機制，以及在其用途的文件以及 toouse 它。

toouse 實作此範例，請遵循下列步驟。

1. 下載 hello[指令碼和文件](https://github.com/Microsoft/sql-server-samples/tree/master/samples/manage/azure-sql-db-elastic-pools):
2. 修改您的環境的 hello 指令碼。 指定裝載彈性集區的一或多部伺服器。
3. 請指定其中 hello 收集度量資訊是儲存 toobe 遙測資料庫。
4. 自訂 hello 指令碼 toospecify hello hello 指令碼的執行期間。

在高層級，hello 指令碼 hello 遵循：

* 列舉指定的 Azure 訂用帳戶 (或指定的伺服器清單) 中的所有伺服器。
* 執行每部伺服器的背景作業。 hello 作業會在迴圈中定期執行，並收集遙測資料 hello server 中的所有 hello 集區。 它然後 hello 收集資料載入 hello 指定的遙測的資料庫。
* 列舉中每個集區 toocollect hello 資料庫資源使用狀況資料的資料庫清單。 它然後 hello 收集資料載入 hello 遙測的資料庫。

hello hello 遙測的資料庫中的收集的度量可以分析的 toomonitor hello 彈性集區和資料庫健全狀況 hello 中。 hello 指令碼也會預先定義的資料表值函式 (TVF) 安裝在 hello 遙測資料庫 toohelp hello 彙總的度量資訊。 指定的時間間隔。 比方說，是 hello TVF 的結果可以用 tooshow 「 前 n 個彈性集區以指定的時段中的 hello eDTU 最大使用率。 」 （選擇性） 使用分析工具，例如 Excel 或 Power BI tooquery 和分析 hello 收集資料。

### <a name="example-retrieve-resource-consumption-metrics-for-an-elastic-pool-and-its-databases"></a>範例︰擷取彈性集區和其資料庫的資源消耗度量
這個範例會擷取指定之彈性集區和其所有資料庫的 hello 消耗度量。 收集的資料格式化並寫入 tooa.csv 格式的檔案。 可使用 Excel 瀏覽 hello 檔案。

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

## <a name="latency-of-elastic-pool-operations"></a>彈性集區的作業延遲
* 變更每個資料庫或最大每個資料庫的 Edtu hello min Edtu 通常完成在 5 分鐘或更短。
* 變更每個集區 edtu 數 （hello） 取決於 hello hello 集區中的所有資料庫所使用的空間數量總計。 變更作業平均每 100 GB 會在 90 分鐘以內完成。 比方說，如果使用的總空間的 hello hello 集區中的所有資料庫都為 200 GB，則 hello 預期的變更 hello 每個集區的集區 eDTU 延遲都為 3 小時或更少。



## <a name="next-steps"></a>後續步驟
* [建立彈性作業](sql-database-elastic-jobs-overview.md)彈性作業可讓您針對任意數目的 hello 集區中的資料庫執行 T-SQL 指令碼。
* 請參閱[使用 Azure SQL Database 向外延展](sql-database-elastic-scale-introduction.md)： 使用彈性的工具 tooscale 外，移動資料、 查詢或建立的交易。
