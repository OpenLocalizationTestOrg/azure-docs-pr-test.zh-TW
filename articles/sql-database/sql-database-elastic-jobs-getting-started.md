---
title: "使用彈性資料庫工作啟動 aaaGetting |Microsoft 文件"
description: "如何 toouse 彈性資料庫工作"
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
ms.assetid: 2540de0e-2235-4cdd-9b6a-b841adba00e5
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/06/2016
ms.author: ddove
ms.openlocfilehash: bc5894d2df4235738ab961db4f69c11cdf786cc6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-elastic-database-jobs"></a>開始使用彈性資料庫工作
彈性資料庫作業 （預覽） for Azure SQL Database 可讓您 tooreliability 執行時自動重試跨越多個資料庫的 T-SQL 指令碼，並提供最終完成保證。 如需有關 hello 彈性資料庫工作功能的詳細資訊，請參閱 hello[功能概觀頁面](sql-database-elastic-jobs-overview.md)。

本主題會延伸中找到的 hello 範例[彈性資料庫工具使用者入門](sql-database-elastic-scale-get-started.md)。 完成時，您將： 了解如何 toocreate 及管理管理群組的相關資料庫的工作。 不需要的 toouse hello 彈性延展工具的順序 tootake 利用的 hello 優點彈性的工作。

## <a name="prerequisites"></a>必要條件
下載並執行 hello[入門彈性資料庫工具範例](sql-database-elastic-scale-get-started.md)。

## <a name="create-a-shard-map-manager-using-hello-sample-app"></a>建立分區對應管理員使用 hello 範例應用程式
這裡您將建立的分區對應管理員以及數個分區，後面接著插入資料至 hello 分區。 如果您已經有使用分區化的資料，在其中設定分區，您可以略過下列步驟的 hello 和移動 toohello 下一節。

1. 建置並執行 hello**彈性資料庫工具使用者入門**範例應用程式。 步驟 7 hello > 一節中的 hello 步驟[下載並執行 hello 範例應用程式](sql-database-elastic-scale-get-started.md#download-and-run-the-sample-app)。 在步驟 7 hello 最後，您會看到下列命令提示字元中的 hello:

   ![命令提示字元](./media/sql-database-elastic-query-getting-started/cmd-prompt.png)

2. 在 hello 命令視窗中，輸入"1"，然後按**Enter**。 這會建立 hello 分區對應管理員，並將這兩個分區 toohello 伺服器時。 接著輸入 "3"，然後按 **Enter**；重複此動作四次。 這會在您的分區中插入範例資料列。
3. hello [Azure 入口網站](https://portal.azure.com)應該會顯示三個新的資料庫：

   ![Visual Studio 確認](./media/sql-database-elastic-query-getting-started/portal.png)

   此時，我們將建立自訂的資料庫集合，以反映 hello 分區對應中的所有 hello 資料庫。 這將會讓我們 toocreate 並執行的作業，跨分區加入新的資料表。

這裡我們可以通常建立分區對應目標時，使用 hello**新增 AzureSqlJobTarget** cmdlet。 hello 分區對應管理員資料庫必須設定為資料庫目標，然後指定做為目標的 hello 特定分區對應。 相反地，我們會持續 tooenumerate hello 的所有資料庫都都在 hello 伺服器，並加入 hello 資料庫 toohello 新自訂集合的 master 資料庫的 hello 例外狀況。

## <a name="creates-a-custom-collection-and-add-all-databases-in-hello-server-toohello-custom-collection-target-with-hello-exception-of-master"></a>建立自訂的集合，並將所有的資料庫新增 hello 與 hello 例外狀況的主要伺服器 toohello 自訂集合目標。
   ```
    $customCollectionName = "dbs_in_server"
    New-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    $ResourceGroupName = "ddove_samples"
    $ServerName = "samples"
    $dbsinserver = Get-AzureRMSqlDatabase -ResourceGroupName $ResourceGroupName -ServerName $ServerName
    $dbsinserver | %{
    $currentdb = $_.DatabaseName
    $ErrorActionPreference = "Stop"
    Write-Output ""

    Try
    {
       New-AzureSqlJobTarget -ServerName $ServerName -DatabaseName $currentdb | Write-Output
    }
    Catch
    {
        $ErrorMessage = $_.Exception.Message
        $ErrorCategory = $_.CategoryInfo.Reason

        if ($ErrorCategory -eq 'UniqueConstraintViolatedException')
        {
             Write-Host $currentdb "is already a database target."
        }

        else
        {
            throw $_
        }

    }

    Try
    {
        if ($currentdb -eq "master")
        {
            Write-Host $currentdb "will not be added custom collection target" $CustomCollectionName "."
        }

        else
        {
            Add-AzureSqlJobChildTarget -CustomCollectionName $CustomCollectionName -ServerName $ServerName -DatabaseName $currentdb
            Write-Host $currentdb "was added to" $CustomCollectionName "."
        }

    }
    Catch
    {
        $ErrorMessage = $_.Exception.Message
        $ErrorCategory = $_.CategoryInfo.Reason

        if ($ErrorCategory -eq 'UniqueConstraintViolatedException')
        {
             Write-Host $currentdb "is already in hello custom collection target" $CustomCollectionName"."
        }

        else
        {
            throw $_
        }
    }
    $ErrorActionPreference = "Continue"
   }
   ```
## <a name="create-a-t-sql-script-for-execution-across-databases"></a>針對跨資料庫執行建立 T-SQL 指令碼
   ```
    $scriptName = "NewTable"
    $scriptCommandText = "
    IF NOT EXISTS (SELECT name FROM sys.tables WHERE name = 'Test')
    BEGIN
        CREATE TABLE Test(
            TestId INT PRIMARY KEY IDENTITY,
            InsertionTime DATETIME2
        );
    END
    GO
    INSERT INTO Test(InsertionTime) VALUES (sysutcdatetime());
    GO"

    $script = New-AzureSqlJobContent -ContentName $scriptName -CommandText $scriptCommandText
    Write-Output $script
   ```

## <a name="create-hello-job-tooexecute-a-script-across-hello-custom-group-of-databases"></a>建立 hello 作業 tooexecute hello 自訂群組的資料庫之間的指令碼

   ```
    $jobName = "create on server dbs"
    $scriptName = "NewTable"
    $customCollectionName = "dbs_in_server"
    $credentialName = "ddove66"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    $job = New-AzureSqlJob -JobName $jobName -CredentialName $credentialName -ContentName $scriptName -TargetId $target.TargetId
    Write-Output $job
   ```

## <a name="execute-hello-job"></a>執行 hello 工作
下列 PowerShell 指令碼的 hello 可以是使用的 tooexecute 現有的工作：

更新下列執行變數 tooreflect hello 需要工作名稱 toohave hello:

   ```
    $jobName = "create on server dbs"
    $jobExecution = Start-AzureSqlJobExecution -JobName $jobName
    Write-Output $jobExecution
   ```

## <a name="retrieve-hello-state-of-a-single-job-execution"></a>擷取單一工作執行的 hello 狀態
使用 hello 相同**Get AzureSqlJobExecution** cmdlet 搭配 hello **includechildren 要求**參數 tooview hello 狀態的子工作執行，也就是 hello 每次針對每個工作在執行特定的狀態hello 作業為目標資料庫。

   ```
    $jobExecutionId = "{Job Execution Id}"
    $jobExecutions = Get-AzureSqlJobExecution -JobExecutionId $jobExecutionId -IncludeChildren
    Write-Output $jobExecutions
   ```

## <a name="view-hello-state-across-multiple-job-executions"></a>跨多個工作執行檢視 hello 狀態
hello **Get AzureSqlJobExecution** cmdlet 都有多個選擇性參數可能是使用的 toodisplay 多個工作執行，透過提供 hello 參數篩選。 hello 以下會示範一些 hello 的可能方法 toouse Get AzureSqlJobExecution:

擷取所有作用中最上層工作執行：

   ```
    Get-AzureSqlJobExecution
   ```

擷取所有最上層工作執行，包括非使用中工作執行：

   ```
    Get-AzureSqlJobExecution -IncludeInactive
   ```

擷取已提供工作執行 ID 的所有子工作執行，包括非使用中工作執行：

   ```
    $parentJobExecutionId = "{Job Execution Id}"
    Get-AzureSqlJobExecution -AzureSqlJobExecution -JobExecutionId $parentJobExecutionId -IncludeInactive -IncludeChildren
   ```

擷取使用排程/工作組合建立的所有工作執行，包括非使用中工作：

   ```
    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    Get-AzureSqlJobExecution -JobName $jobName -ScheduleName $scheduleName -IncludeInactive
   ```

擷取以指定的分區對應為目標的所有工作，包括非使用中工作：

   ```
    $shardMapServerName = "{Shard Map Server Name}"
    $shardMapDatabaseName = "{Shard Map Database Name}"
    $shardMapName = "{Shard Map Name}"
    $target = Get-AzureSqlJobTarget -ShardMapManagerDatabaseName $shardMapDatabaseName -ShardMapManagerServerName $shardMapServerName -ShardMapName $shardMapName
    Get-AzureSqlJobExecution -TargetId $target.TargetId -IncludeInactive
   ```

擷取以指定的自訂集合為目標的所有工作，包括非使用中工作：

   ```
    $customCollectionName = "{Custom Collection Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    Get-AzureSqlJobExecution -TargetId $target.TargetId -IncludeInactive
   ```

擷取作業在特定的工作執行的工作執行 hello 清單：

   ```
    $jobExecutionId = "{Job Execution Id}"
    $jobTaskExecutions = Get-AzureSqlJobTaskExecution -JobExecutionId $jobExecutionId
    Write-Output $jobTaskExecutions
   ```

擷取工作作業執行詳細資料：

hello 下列 PowerShell 指令碼可以使用的 tooview hello 詳細資料的作業工作執行，這特別有用偵錯時執行失敗數目。
   ```
    $jobTaskExecutionId = "{Job Task Execution Id}"
    $jobTaskExecution = Get-AzureSqlJobTaskExecution -JobTaskExecutionId $jobTaskExecutionId
    Write-Output $jobTaskExecution
   ```

## <a name="retrieve-failures-within-job-task-executions"></a>擷取工作作業執行內的失敗
hello JobTaskExecution 物件包含 hello 訊息屬性以及 hello 工作的生命週期的屬性。 如果作業工作執行失敗，hello 生命週期的屬性會設定得*失敗*和 hello 訊息屬性將 toohello 產生的例外狀況訊息和其堆疊。 如果作業失敗，會針對給定的作業不成功的作業工作的重要 tooview hello 詳細資料。

   ```
    $jobExecutionId = "{Job Execution Id}"
    $jobTaskExecutions = Get-AzureSqlJobTaskExecution -JobExecutionId $jobExecutionId
    Foreach($jobTaskExecution in $jobTaskExecutions)
        {
        if($jobTaskExecution.Lifecycle -ne 'Succeeded')
            {
            Write-Output $jobTaskExecution
            }
        }
   ```

## <a name="waiting-for-a-job-execution-toocomplete"></a>等候工作執行 toocomplete
下列 PowerShell 指令碼的 hello 可使用的作業工作 toocomplete toowait:

   ```
    $jobExecutionId = "{Job Execution Id}"
    Wait-AzureSqlJobExecution -JobExecutionId $jobExecutionId
   ```

## <a name="create-a-custom-execution-policy"></a>建立自訂執行原則
彈性資料庫工作支援建立自訂執行原則，可以在啟動作業時套用。

執行原則目前允許定義：

* Hello 執行原則的名稱： 識別項。
* 工作逾時：彈性資料庫工作取消工作之前的總時間。
* 初始重試間隔： 間隔 toowait 第一次重試之前。
* 重試間隔 toouse 的最大重試間隔： 端點。
* 重試間隔輪詢： 係數使用係數 toocalculate hello 下一步 重試間隔。  hello 下列公式會使用: （初始的重試間隔） * Math.pow (（間隔輪詢係數） （數字的重試）-2)。
* 最大嘗試次數： hello 的數目上限重試嘗試 tooperform 工作內。

hello 預設執行原則會使用下列值的 hello:

* 名稱：預設執行原則
* 工作逾時：1 週
* 初始重試間隔：100 毫秒
* 最大重試間隔：30 分鐘
* 重試間隔係數：2
* 嘗試上限：2,147,483,647

建立 hello 所需執行原則：

   ```
    $executionPolicyName = "{Execution Policy Name}"
    $initialRetryInterval = New-TimeSpan -Seconds 10
    $jobTimeout = New-TimeSpan -Minutes 30
    $maximumAttempts = 999999
    $maximumRetryInterval = New-TimeSpan -Minutes 1
    $retryIntervalBackoffCoefficient = 1.5
    $executionPolicy = New-AzureSqlJobExecutionPolicy -ExecutionPolicyName $executionPolicyName -InitialRetryInterval $initialRetryInterval -JobTimeout $jobTimeout -MaximumAttempts $maximumAttempts -MaximumRetryInterval $maximumRetryInterval -RetryIntervalBackoffCoefficient $retryIntervalBackoffCoefficient
    Write-Output $executionPolicy
   ```

### <a name="update-a-custom-execution-policy"></a>更新自訂執行原則
更新所需的 hello 執行原則 tooupdate:

   ```
    $executionPolicyName = "{Execution Policy Name}"
    $initialRetryInterval = New-TimeSpan -Seconds 15
    $jobTimeout = New-TimeSpan -Minutes 30
    $maximumAttempts = 999999
    $maximumRetryInterval = New-TimeSpan -Minutes 1
    $retryIntervalBackoffCoefficient = 1.5
    $updatedExecutionPolicy = Set-AzureSqlJobExecutionPolicy -ExecutionPolicyName $executionPolicyName -InitialRetryInterval $initialRetryInterval -JobTimeout $jobTimeout -MaximumAttempts $maximumAttempts -MaximumRetryInterval $maximumRetryInterval -RetryIntervalBackoffCoefficient $retryIntervalBackoffCoefficient
    Write-Output $updatedExecutionPolicy
   ```

## <a name="cancel-a-job"></a>取消工作
彈性資料庫工作支援取消工作要求。  如果彈性資料庫工作偵測到目前正在執行工作的取消要求，它會嘗試 toostop hello 作業。

彈性資料庫工作有兩種不同的方式可以執行取消作業：

1. 取消目前正在執行的工作： 如果當工作目前正在執行時偵測取消，則將會取消嘗試 hello 目前正在執行的層面 hello 工作內。  例如： 嘗試取消時，目前執行的長時間執行查詢時，會有嘗試 toocancel hello 查詢。
2. 取消工作重試次數： 如果啟動工作執行前，取消偵測到的 hello 控制執行緒，hello 控制執行緒會避免啟動 hello 工作，並宣告 hello 要求為已取消。

如果作業取消父工作的要求，hello 父工作和所有其子工作會採用 hello 取消要求。

toosubmit 取消要求，使用 hello**停止 AzureSqlJobExecution** cmdlet 和設定 hello **JobExecutionId**參數。

   ```
    $jobExecutionId = "{Job Execution Id}"
    Stop-AzureSqlJobExecution -JobExecutionId $jobExecutionId
   ```

## <a name="delete-a-job-by-name-and-hello-jobs-history"></a>刪除作業的名稱和 hello 作業歷程記錄
彈性資料庫工作支援非同步刪除工作。 作業可以標示為刪除，而且 hello 系統刪除 hello 工作和其所有的作業記錄所有作業執行都完成 hello 工作之後。 hello 系統不會自動取消作用中的作業執行。  

相反地，停止 AzureSqlJobExecution 必須叫用的 toocancel 作用中的作業執行。

tootrigger 作業刪除使用 hello**移除 AzureSqlJob** cmdlet 和設定 hello **JobName**參數。

   ```
    $jobName = "{Job Name}"
    Remove-AzureSqlJob -JobName $jobName
   ```

## <a name="create-a-custom-database-target"></a>建立自訂資料庫目標
自訂資料庫目標可以在彈性資料庫工作中定義，可用來直接執行或包含在自訂資料庫群組內。 因為**彈性集區**不尚未直接支援透過 hello PowerShell Api 中，您只要建立自訂資料庫的目標，其中包含所有 hello 集區中的 hello 資料庫自訂資料庫收集目標。

設定下列變數 tooreflect hello 預期資料庫資訊的 hello:

   ```
    $databaseName = "{Database Name}"
    $databaseServerName = "{Server Name}"
    New-AzureSqlJobDatabaseTarget -DatabaseName $databaseName -ServerName $databaseServerName
   ```

## <a name="create-a-custom-database-collection-target"></a>建立自訂資料庫集合目標
自訂資料庫收集目標可以跨多個定義的資料庫的目標是定義的 tooenable 執行。 建立資料庫群組之後，資料庫可以是相關聯的 toohello 自訂集合目標。

設定下列變數 tooreflect hello 所需的自訂集合目標組態 hello:

   ```
    $customCollectionName = "{Custom Database Collection Name}"
    New-AzureSqlJobTarget -CustomCollectionName $customCollectionName
   ```

### <a name="add-databases-tooa-custom-database-collection-target"></a>新增資料庫 tooa 自訂資料庫收集目標
資料庫的目標可以是自訂的資料庫集合為目標 toocreate 資料庫的群組相關聯。 每次建立工作目標為自訂的資料庫集合的目標，它會展開的 tootarget hello 資料庫相關聯的 toohello 群組在 hello 執行的時間。

加入所需的 hello 資料庫 tooa 特定自訂集合：

   ```
    $serverName = "{Database Server Name}"
    $databaseName = "{Database Name}"
    $customCollectionName = "{Custom Database Collection Name}"
    Add-AzureSqlJobChildTarget -CustomCollectionName $customCollectionName -DatabaseName $databaseName -ServerName $databaseServerName
   ```

#### <a name="review-hello-databases-within-a-custom-database-collection-target"></a>檢閱 hello 資料庫內的自訂資料庫收集目標
使用 hello **Get AzureSqlJobTarget** cmdlet tooretrieve hello 子資料庫內的自訂資料庫收集目標。

   ```
    $customCollectionName = "{Custom Database Collection Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    $childTargets = Get-AzureSqlJobTarget -ParentTargetId $target.TargetId
    Write-Output $childTargets
   ```

### <a name="create-a-job-tooexecute-a-script-across-a-custom-database-collection-target"></a>建立指令碼工作 tooexecute 跨自訂資料庫收集目標
使用 hello**新增 AzureSqlJob** cmdlet toocreate 作業會每天針對資料庫定義的自訂資料庫收集目標的群組。 彈性資料庫工作會展開成多個子工作，每個對應的 tooa 資料庫與 hello 自訂資料庫收集目標關聯，並確保 hello 指令碼執行的每個資料庫的 hello 作業。 同樣地，請務必指令碼是等冪 toobe 彈性 tooretries。

   ```
    $jobName = "{Job Name}"
    $scriptName = "{Script Name}"
    $customCollectionName = "{Custom Collection Name}"
    $credentialName = "{Credential Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    $job = New-AzureSqlJob -JobName $jobName -CredentialName $credentialName -ContentName $scriptName -TargetId $target.TargetId
    Write-Output $job
   ```

## <a name="data-collection-across-databases"></a>跨資料庫的資料集合
**彈性資料庫工作**支援跨資料庫的群組執行查詢，並傳送嗨結果 tooa 指定的資料庫資料表。 hello 資料表可以查詢之後每個資料庫的 hello 事實 toosee hello 查詢的結果。 這樣非同步機制 tooexecute 查詢跨多個資料庫。 失敗的情況下，例如其中一個 hello 暫時無法使用的資料庫會自動處理透過重試次數。

如果它尚未存在自動建立 hello 指定的目的地資料表，傳回結果集的比對的 hello 結構描述的 hello。 如果指令碼執行傳回多個結果集，彈性資料庫工作才會傳送 hello 第一次一個 toohello 提供目的地資料表。

hello 下列 PowerShell 指令碼可以使用的 tooexecute 收集其結果至指定資料表的指令碼。 此指令碼假設已建立 T-SQL 指令碼，它會輸出單一結果集，且自訂資料庫集合目標已建立。

設定下列 tooreflect hello 預期指令碼、 認證和執行目標的 hello:

   ```
    $jobName = "{Job Name}"
    $scriptName = "{Script Name}"
    $executionCredentialName = "{Execution Credential Name}"
    $customCollectionName = "{Custom Collection Name}"
    $destinationCredentialName = "{Destination Credential Name}"
    $destinationServerName = "{Destination Server Name}"
    $destinationDatabaseName = "{Destination Database Name}"
    $destinationSchemaName = "{Destination Schema Name}"
    $destinationTableName = "{Destination Table Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
   ```

### <a name="create-and-start-a-job-for-data-collection-scenarios"></a>建立和啟動資料庫集合案例的工作
   ```
    $job = New-AzureSqlJob -JobName $jobName -CredentialName $executionCredentialName -ContentName $scriptName -ResultSetDestinationServerName $destinationServerName -ResultSetDestinationDatabaseName $destinationDatabaseName -ResultSetDestinationSchemaName $destinationSchemaName -ResultSetDestinationTableName $destinationTableName -ResultSetDestinationCredentialName $destinationCredentialName -TargetId $target.TargetId
    Write-Output $job
    $jobExecution = Start-AzureSqlJobExecution -JobName $jobName
    Write-Output $jobExecution
   ```

## <a name="create-a-schedule-for-job-execution-using-a-job-trigger"></a>使用工作觸發程序建立工作執行的排程
hello 下列 PowerShell 指令碼可以使用的 toocreate 重複發生的排程。 這個指令碼使用分鐘間隔，但是 New-AzureSqlJobSchedule 也支援 -DayInterval、-HourInterval、-MonthInterval 和 -WeekInterval 參數。 您可以藉由傳遞 -OneTime，建立僅執行一次的排程。

建立新的排程：
   ```
    $scheduleName = "Every one minute"
    $minuteInterval = 1
    $startTime = (Get-Date).ToUniversalTime()
    $schedule = New-AzureSqlJobSchedule -MinuteInterval $minuteInterval -ScheduleName $scheduleName -StartTime $startTime
    Write-Output $schedule
   ```

### <a name="create-a-job-trigger-toohave-a-job-executed-on-a-time-schedule"></a>建立工作觸發程序 toohave 作業的時間排程執行
工作觸發程序可以定義的 toohave 作業執行相應 tooa 時間排程。 hello 下列 PowerShell 指令碼可以使用的 toocreate 工作觸發程序。

下列變數 toocorrespond toohello 組 hello 預期作業和排程：

   ```
    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    $jobTrigger = New-AzureSqlJobTrigger -ScheduleName $scheduleName -JobName $jobName
    Write-Output $jobTrigger
   ```

### <a name="remove-a-scheduled-association-toostop-job-from-executing-on-schedule"></a>移除排程的關聯 toostop 作業依排程執行
可以移除 toodiscontinue 再度工作執行的工作觸發程序，hello 工作觸發程序。
移除工作觸發程序 toostop 工作正在執行使用 hello 相應 tooa 排程**移除 AzureSqlJobTrigger** cmdlet。

   ```
    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    Remove-AzureSqlJobTrigger -ScheduleName $scheduleName -JobName $jobName
   ```

## <a name="import-elastic-database-query-results-tooexcel"></a>匯入彈性資料庫查詢結果 tooExcel
 您可以匯入 hello 結果的查詢 tooan Excel 檔案。

1. 啟動 Excel 2013。
2. 瀏覽 toohello**資料**功能區。
3. 按一下 [從其他來源]，然後按一下 [從 SQL Server]。

   ![從其他來源的 Excel 匯入](./media/sql-database-elastic-query-getting-started/exel-sources.png)

4. 在 hello**資料連線精靈**輸入 hello 伺服器名稱和登入認證。 然後按 [下一步] 。
5. 在 hello 對話方塊**選取 hello 資料庫包含您想要的 hello 資料**，選取 hello **ElasticDBQuery**資料庫。
6. 選取 hello**客戶**hello 清單檢視中資料表，並按一下**下一步**。 然後按一下 [ **完成**]。
7. 在 hello**匯入資料**底下形成**選取您要如何 tooview 這項資料在活頁簿中**，選取**資料表**按一下**[確定]**。

所有 hello 中的資料列**客戶**儲存在不同的分區中的資料表填入 hello Excel 工作表。

## <a name="next-steps"></a>後續步驟
您現在可以使用 Excel 的資料功能。 使用您的伺服器名稱、 資料庫名稱 hello 連接字串和認證 tooconnect BI 和資料整合工具 toohello 彈性查詢資料庫。 請確定 SQL Server 可支援做為您的工具的資料來源。 請參閱 toohello 彈性查詢資料庫，就像任何其他 SQL Server 資料庫的外部資料表和連線 toowith 工具的 SQL Server 資料表。

### <a name="cost"></a>成本
沒有另收費用使用 hello 彈性資料庫查詢功能。 不過，此時這項功能僅適用於高階資料庫做為結束點，但 hello 分區可以是任何服務層。

如需價格資訊，請參閱 [SQL Database 價格詳細資料](https://azure.microsoft.com/pricing/details/sql-database/)。

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-query-getting-started/cmd-prompt.png
[2]: ./media/sql-database-elastic-query-getting-started/portal.png
[3]: ./media/sql-database-elastic-query-getting-started/tiers.png
[4]: ./media/sql-database-elastic-query-getting-started/details.png
[5]: ./media/sql-database-elastic-query-getting-started/exel-sources.png
<!--anchors-->
