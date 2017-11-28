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
# <a name="getting-started-with-elastic-database-jobs"></a><span data-ttu-id="0e64b-103">開始使用彈性資料庫工作</span><span class="sxs-lookup"><span data-stu-id="0e64b-103">Getting started with Elastic Database jobs</span></span>
<span data-ttu-id="0e64b-104">彈性資料庫作業 （預覽） for Azure SQL Database 可讓您 tooreliability 執行時自動重試跨越多個資料庫的 T-SQL 指令碼，並提供最終完成保證。</span><span class="sxs-lookup"><span data-stu-id="0e64b-104">Elastic Database jobs (preview) for Azure SQL Database allows you tooreliability execute T-SQL scripts that span multiple databases while automatically retrying and providing eventual completion guarantees.</span></span> <span data-ttu-id="0e64b-105">如需有關 hello 彈性資料庫工作功能的詳細資訊，請參閱 hello[功能概觀頁面](sql-database-elastic-jobs-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="0e64b-105">For more information about hello Elastic Database job feature, please see hello [feature overview page](sql-database-elastic-jobs-overview.md).</span></span>

<span data-ttu-id="0e64b-106">本主題會延伸中找到的 hello 範例[彈性資料庫工具使用者入門](sql-database-elastic-scale-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="0e64b-106">This topic extends hello sample found in [Getting started with Elastic Database tools](sql-database-elastic-scale-get-started.md).</span></span> <span data-ttu-id="0e64b-107">完成時，您將： 了解如何 toocreate 及管理管理群組的相關資料庫的工作。</span><span class="sxs-lookup"><span data-stu-id="0e64b-107">When completed, you will: learn how toocreate and manage jobs that manage a group of related databases.</span></span> <span data-ttu-id="0e64b-108">不需要的 toouse hello 彈性延展工具的順序 tootake 利用的 hello 優點彈性的工作。</span><span class="sxs-lookup"><span data-stu-id="0e64b-108">It is not required toouse hello Elastic Scale tools in order tootake advantage of hello benefits of Elastic jobs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0e64b-109">必要條件</span><span class="sxs-lookup"><span data-stu-id="0e64b-109">Prerequisites</span></span>
<span data-ttu-id="0e64b-110">下載並執行 hello[入門彈性資料庫工具範例](sql-database-elastic-scale-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="0e64b-110">Download and run hello [Getting started with Elastic Database tools sample](sql-database-elastic-scale-get-started.md).</span></span>

## <a name="create-a-shard-map-manager-using-hello-sample-app"></a><span data-ttu-id="0e64b-111">建立分區對應管理員使用 hello 範例應用程式</span><span class="sxs-lookup"><span data-stu-id="0e64b-111">Create a shard map manager using hello sample app</span></span>
<span data-ttu-id="0e64b-112">這裡您將建立的分區對應管理員以及數個分區，後面接著插入資料至 hello 分區。</span><span class="sxs-lookup"><span data-stu-id="0e64b-112">Here you will create a shard map manager along with several shards, followed by insertion of data into hello shards.</span></span> <span data-ttu-id="0e64b-113">如果您已經有使用分區化的資料，在其中設定分區，您可以略過下列步驟的 hello 和移動 toohello 下一節。</span><span class="sxs-lookup"><span data-stu-id="0e64b-113">If you already have shards set up with sharded data in them, you can skip hello following steps and move toohello next section.</span></span>

1. <span data-ttu-id="0e64b-114">建置並執行 hello**彈性資料庫工具使用者入門**範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="0e64b-114">Build and run hello **Getting started with Elastic Database tools** sample application.</span></span> <span data-ttu-id="0e64b-115">步驟 7 hello > 一節中的 hello 步驟[下載並執行 hello 範例應用程式](sql-database-elastic-scale-get-started.md#download-and-run-the-sample-app)。</span><span class="sxs-lookup"><span data-stu-id="0e64b-115">Follow hello steps until step 7 in hello section [Download and run hello sample app](sql-database-elastic-scale-get-started.md#download-and-run-the-sample-app).</span></span> <span data-ttu-id="0e64b-116">在步驟 7 hello 最後，您會看到下列命令提示字元中的 hello:</span><span class="sxs-lookup"><span data-stu-id="0e64b-116">At hello end of Step 7, you will see hello following command prompt:</span></span>

   ![命令提示字元](./media/sql-database-elastic-query-getting-started/cmd-prompt.png)

2. <span data-ttu-id="0e64b-118">在 hello 命令視窗中，輸入"1"，然後按**Enter**。</span><span class="sxs-lookup"><span data-stu-id="0e64b-118">In hello command window, type "1" and press **Enter**.</span></span> <span data-ttu-id="0e64b-119">這會建立 hello 分區對應管理員，並將這兩個分區 toohello 伺服器時。</span><span class="sxs-lookup"><span data-stu-id="0e64b-119">This creates hello shard map manager, and adds two shards toohello server.</span></span> <span data-ttu-id="0e64b-120">接著輸入 "3"，然後按 **Enter**；重複此動作四次。</span><span class="sxs-lookup"><span data-stu-id="0e64b-120">Then type "3" and press **Enter**; repeat this action four times.</span></span> <span data-ttu-id="0e64b-121">這會在您的分區中插入範例資料列。</span><span class="sxs-lookup"><span data-stu-id="0e64b-121">This inserts sample data rows in your shards.</span></span>
3. <span data-ttu-id="0e64b-122">hello [Azure 入口網站](https://portal.azure.com)應該會顯示三個新的資料庫：</span><span class="sxs-lookup"><span data-stu-id="0e64b-122">hello [Azure Portal](https://portal.azure.com) should show three new databases:</span></span>

   ![Visual Studio 確認](./media/sql-database-elastic-query-getting-started/portal.png)

   <span data-ttu-id="0e64b-124">此時，我們將建立自訂的資料庫集合，以反映 hello 分區對應中的所有 hello 資料庫。</span><span class="sxs-lookup"><span data-stu-id="0e64b-124">At this point, we will create a custom database collection that reflects all hello databases in hello shard map.</span></span> <span data-ttu-id="0e64b-125">這將會讓我們 toocreate 並執行的作業，跨分區加入新的資料表。</span><span class="sxs-lookup"><span data-stu-id="0e64b-125">This will allow us toocreate and execute a job that add a new table across shards.</span></span>

<span data-ttu-id="0e64b-126">這裡我們可以通常建立分區對應目標時，使用 hello**新增 AzureSqlJobTarget** cmdlet。</span><span class="sxs-lookup"><span data-stu-id="0e64b-126">Here we would usually create a shard map target, using hello **New-AzureSqlJobTarget** cmdlet.</span></span> <span data-ttu-id="0e64b-127">hello 分區對應管理員資料庫必須設定為資料庫目標，然後指定做為目標的 hello 特定分區對應。</span><span class="sxs-lookup"><span data-stu-id="0e64b-127">hello shard map manager database must be set as a database target and then hello specific shard map is specified as a target.</span></span> <span data-ttu-id="0e64b-128">相反地，我們會持續 tooenumerate hello 的所有資料庫都都在 hello 伺服器，並加入 hello 資料庫 toohello 新自訂集合的 master 資料庫的 hello 例外狀況。</span><span class="sxs-lookup"><span data-stu-id="0e64b-128">Instead, we are going tooenumerate all hello databases in hello server and add hello databases toohello new custom collection with hello exception of master database.</span></span>

## <a name="creates-a-custom-collection-and-add-all-databases-in-hello-server-toohello-custom-collection-target-with-hello-exception-of-master"></a><span data-ttu-id="0e64b-129">建立自訂的集合，並將所有的資料庫新增 hello 與 hello 例外狀況的主要伺服器 toohello 自訂集合目標。</span><span class="sxs-lookup"><span data-stu-id="0e64b-129">Creates a custom collection and add all databases in hello server toohello custom collection target with hello exception of master.</span></span>
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
## <a name="create-a-t-sql-script-for-execution-across-databases"></a><span data-ttu-id="0e64b-130">針對跨資料庫執行建立 T-SQL 指令碼</span><span class="sxs-lookup"><span data-stu-id="0e64b-130">Create a T-SQL Script for execution across databases</span></span>
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

## <a name="create-hello-job-tooexecute-a-script-across-hello-custom-group-of-databases"></a><span data-ttu-id="0e64b-131">建立 hello 作業 tooexecute hello 自訂群組的資料庫之間的指令碼</span><span class="sxs-lookup"><span data-stu-id="0e64b-131">Create hello job tooexecute a script across hello custom group of databases</span></span>

   ```
    $jobName = "create on server dbs"
    $scriptName = "NewTable"
    $customCollectionName = "dbs_in_server"
    $credentialName = "ddove66"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    $job = New-AzureSqlJob -JobName $jobName -CredentialName $credentialName -ContentName $scriptName -TargetId $target.TargetId
    Write-Output $job
   ```

## <a name="execute-hello-job"></a><span data-ttu-id="0e64b-132">執行 hello 工作</span><span class="sxs-lookup"><span data-stu-id="0e64b-132">Execute hello job</span></span>
<span data-ttu-id="0e64b-133">下列 PowerShell 指令碼的 hello 可以是使用的 tooexecute 現有的工作：</span><span class="sxs-lookup"><span data-stu-id="0e64b-133">hello following PowerShell script can be used tooexecute an existing job:</span></span>

<span data-ttu-id="0e64b-134">更新下列執行變數 tooreflect hello 需要工作名稱 toohave hello:</span><span class="sxs-lookup"><span data-stu-id="0e64b-134">Update hello following variable tooreflect hello desired job name toohave executed:</span></span>

   ```
    $jobName = "create on server dbs"
    $jobExecution = Start-AzureSqlJobExecution -JobName $jobName
    Write-Output $jobExecution
   ```

## <a name="retrieve-hello-state-of-a-single-job-execution"></a><span data-ttu-id="0e64b-135">擷取單一工作執行的 hello 狀態</span><span class="sxs-lookup"><span data-stu-id="0e64b-135">Retrieve hello state of a single job execution</span></span>
<span data-ttu-id="0e64b-136">使用 hello 相同**Get AzureSqlJobExecution** cmdlet 搭配 hello **includechildren 要求**參數 tooview hello 狀態的子工作執行，也就是 hello 每次針對每個工作在執行特定的狀態hello 作業為目標資料庫。</span><span class="sxs-lookup"><span data-stu-id="0e64b-136">Use hello same **Get-AzureSqlJobExecution** cmdlet with hello **IncludeChildren** parameter tooview hello state of child job executions, namely hello specific state for each job execution against each database targeted by hello job.</span></span>

   ```
    $jobExecutionId = "{Job Execution Id}"
    $jobExecutions = Get-AzureSqlJobExecution -JobExecutionId $jobExecutionId -IncludeChildren
    Write-Output $jobExecutions
   ```

## <a name="view-hello-state-across-multiple-job-executions"></a><span data-ttu-id="0e64b-137">跨多個工作執行檢視 hello 狀態</span><span class="sxs-lookup"><span data-stu-id="0e64b-137">View hello state across multiple job executions</span></span>
<span data-ttu-id="0e64b-138">hello **Get AzureSqlJobExecution** cmdlet 都有多個選擇性參數可能是使用的 toodisplay 多個工作執行，透過提供 hello 參數篩選。</span><span class="sxs-lookup"><span data-stu-id="0e64b-138">hello **Get-AzureSqlJobExecution** cmdlet has multiple optional parameters that can be used toodisplay multiple job executions, filtered through hello provided parameters.</span></span> <span data-ttu-id="0e64b-139">hello 以下會示範一些 hello 的可能方法 toouse Get AzureSqlJobExecution:</span><span class="sxs-lookup"><span data-stu-id="0e64b-139">hello following demonstrates some of hello possible ways toouse Get-AzureSqlJobExecution:</span></span>

<span data-ttu-id="0e64b-140">擷取所有作用中最上層工作執行：</span><span class="sxs-lookup"><span data-stu-id="0e64b-140">Retrieve all active top level job executions:</span></span>

   ```
    Get-AzureSqlJobExecution
   ```

<span data-ttu-id="0e64b-141">擷取所有最上層工作執行，包括非使用中工作執行：</span><span class="sxs-lookup"><span data-stu-id="0e64b-141">Retrieve all top level job executions, including inactive job executions:</span></span>

   ```
    Get-AzureSqlJobExecution -IncludeInactive
   ```

<span data-ttu-id="0e64b-142">擷取已提供工作執行 ID 的所有子工作執行，包括非使用中工作執行：</span><span class="sxs-lookup"><span data-stu-id="0e64b-142">Retrieve all child job executions of a provided job execution ID, including inactive job executions:</span></span>

   ```
    $parentJobExecutionId = "{Job Execution Id}"
    Get-AzureSqlJobExecution -AzureSqlJobExecution -JobExecutionId $parentJobExecutionId -IncludeInactive -IncludeChildren
   ```

<span data-ttu-id="0e64b-143">擷取使用排程/工作組合建立的所有工作執行，包括非使用中工作：</span><span class="sxs-lookup"><span data-stu-id="0e64b-143">Retrieve all job executions created using a schedule / job combination, including inactive jobs:</span></span>

   ```
    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    Get-AzureSqlJobExecution -JobName $jobName -ScheduleName $scheduleName -IncludeInactive
   ```

<span data-ttu-id="0e64b-144">擷取以指定的分區對應為目標的所有工作，包括非使用中工作：</span><span class="sxs-lookup"><span data-stu-id="0e64b-144">Retrieve all jobs targeting a specified shard map, including inactive jobs:</span></span>

   ```
    $shardMapServerName = "{Shard Map Server Name}"
    $shardMapDatabaseName = "{Shard Map Database Name}"
    $shardMapName = "{Shard Map Name}"
    $target = Get-AzureSqlJobTarget -ShardMapManagerDatabaseName $shardMapDatabaseName -ShardMapManagerServerName $shardMapServerName -ShardMapName $shardMapName
    Get-AzureSqlJobExecution -TargetId $target.TargetId -IncludeInactive
   ```

<span data-ttu-id="0e64b-145">擷取以指定的自訂集合為目標的所有工作，包括非使用中工作：</span><span class="sxs-lookup"><span data-stu-id="0e64b-145">Retrieve all jobs targeting a specified custom collection, including inactive jobs:</span></span>

   ```
    $customCollectionName = "{Custom Collection Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    Get-AzureSqlJobExecution -TargetId $target.TargetId -IncludeInactive
   ```

<span data-ttu-id="0e64b-146">擷取作業在特定的工作執行的工作執行 hello 清單：</span><span class="sxs-lookup"><span data-stu-id="0e64b-146">Retrieve hello list of job task executions within a specific job execution:</span></span>

   ```
    $jobExecutionId = "{Job Execution Id}"
    $jobTaskExecutions = Get-AzureSqlJobTaskExecution -JobExecutionId $jobExecutionId
    Write-Output $jobTaskExecutions
   ```

<span data-ttu-id="0e64b-147">擷取工作作業執行詳細資料：</span><span class="sxs-lookup"><span data-stu-id="0e64b-147">Retrieve job task execution details:</span></span>

<span data-ttu-id="0e64b-148">hello 下列 PowerShell 指令碼可以使用的 tooview hello 詳細資料的作業工作執行，這特別有用偵錯時執行失敗數目。</span><span class="sxs-lookup"><span data-stu-id="0e64b-148">hello following PowerShell script can be used tooview hello details of a job task execution, which is particularly useful when debugging execution failures.</span></span>
   ```
    $jobTaskExecutionId = "{Job Task Execution Id}"
    $jobTaskExecution = Get-AzureSqlJobTaskExecution -JobTaskExecutionId $jobTaskExecutionId
    Write-Output $jobTaskExecution
   ```

## <a name="retrieve-failures-within-job-task-executions"></a><span data-ttu-id="0e64b-149">擷取工作作業執行內的失敗</span><span class="sxs-lookup"><span data-stu-id="0e64b-149">Retrieve failures within job task executions</span></span>
<span data-ttu-id="0e64b-150">hello JobTaskExecution 物件包含 hello 訊息屬性以及 hello 工作的生命週期的屬性。</span><span class="sxs-lookup"><span data-stu-id="0e64b-150">hello JobTaskExecution object includes a property for hello Lifecycle of hello task along with a Message property.</span></span> <span data-ttu-id="0e64b-151">如果作業工作執行失敗，hello 生命週期的屬性會設定得*失敗*和 hello 訊息屬性將 toohello 產生的例外狀況訊息和其堆疊。</span><span class="sxs-lookup"><span data-stu-id="0e64b-151">If a job task execution failed, hello Lifecycle property will be set too*Failed* and hello Message property will be set toohello resulting exception message and its stack.</span></span> <span data-ttu-id="0e64b-152">如果作業失敗，會針對給定的作業不成功的作業工作的重要 tooview hello 詳細資料。</span><span class="sxs-lookup"><span data-stu-id="0e64b-152">If a job did not succeed, it is important tooview hello details of job tasks that did not succeed for a given job.</span></span>

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

## <a name="waiting-for-a-job-execution-toocomplete"></a><span data-ttu-id="0e64b-153">等候工作執行 toocomplete</span><span class="sxs-lookup"><span data-stu-id="0e64b-153">Waiting for a job execution toocomplete</span></span>
<span data-ttu-id="0e64b-154">下列 PowerShell 指令碼的 hello 可使用的作業工作 toocomplete toowait:</span><span class="sxs-lookup"><span data-stu-id="0e64b-154">hello following PowerShell script can be used toowait for a job task toocomplete:</span></span>

   ```
    $jobExecutionId = "{Job Execution Id}"
    Wait-AzureSqlJobExecution -JobExecutionId $jobExecutionId
   ```

## <a name="create-a-custom-execution-policy"></a><span data-ttu-id="0e64b-155">建立自訂執行原則</span><span class="sxs-lookup"><span data-stu-id="0e64b-155">Create a custom execution policy</span></span>
<span data-ttu-id="0e64b-156">彈性資料庫工作支援建立自訂執行原則，可以在啟動作業時套用。</span><span class="sxs-lookup"><span data-stu-id="0e64b-156">Elastic Database jobs supports creating custom execution policies that can be applied when starting jobs.</span></span>

<span data-ttu-id="0e64b-157">執行原則目前允許定義：</span><span class="sxs-lookup"><span data-stu-id="0e64b-157">Execution policies currently allow for defining:</span></span>

* <span data-ttu-id="0e64b-158">Hello 執行原則的名稱： 識別項。</span><span class="sxs-lookup"><span data-stu-id="0e64b-158">Name: Identifier for hello execution policy.</span></span>
* <span data-ttu-id="0e64b-159">工作逾時：彈性資料庫工作取消工作之前的總時間。</span><span class="sxs-lookup"><span data-stu-id="0e64b-159">Job Timeout: Total time before a job will be canceled by Elastic Database Jobs.</span></span>
* <span data-ttu-id="0e64b-160">初始重試間隔： 間隔 toowait 第一次重試之前。</span><span class="sxs-lookup"><span data-stu-id="0e64b-160">Initial Retry Interval: Interval toowait before first retry.</span></span>
* <span data-ttu-id="0e64b-161">重試間隔 toouse 的最大重試間隔： 端點。</span><span class="sxs-lookup"><span data-stu-id="0e64b-161">Maximum Retry Interval: Cap of retry intervals toouse.</span></span>
* <span data-ttu-id="0e64b-162">重試間隔輪詢： 係數使用係數 toocalculate hello 下一步 重試間隔。</span><span class="sxs-lookup"><span data-stu-id="0e64b-162">Retry Interval Backoff Coefficient: Coefficient used toocalculate hello next interval between retries.</span></span>  <span data-ttu-id="0e64b-163">hello 下列公式會使用: （初始的重試間隔） * Math.pow (（間隔輪詢係數） （數字的重試）-2)。</span><span class="sxs-lookup"><span data-stu-id="0e64b-163">hello following formula is used: (Initial Retry Interval) * Math.pow((Interval Backoff Coefficient), (Number of Retries) - 2).</span></span>
* <span data-ttu-id="0e64b-164">最大嘗試次數： hello 的數目上限重試嘗試 tooperform 工作內。</span><span class="sxs-lookup"><span data-stu-id="0e64b-164">Maximum Attempts: hello maximum number of retry attempts tooperform within a job.</span></span>

<span data-ttu-id="0e64b-165">hello 預設執行原則會使用下列值的 hello:</span><span class="sxs-lookup"><span data-stu-id="0e64b-165">hello default execution policy uses hello following values:</span></span>

* <span data-ttu-id="0e64b-166">名稱：預設執行原則</span><span class="sxs-lookup"><span data-stu-id="0e64b-166">Name: Default execution policy</span></span>
* <span data-ttu-id="0e64b-167">工作逾時：1 週</span><span class="sxs-lookup"><span data-stu-id="0e64b-167">Job Timeout: 1 week</span></span>
* <span data-ttu-id="0e64b-168">初始重試間隔：100 毫秒</span><span class="sxs-lookup"><span data-stu-id="0e64b-168">Initial Retry Interval:  100 milliseconds</span></span>
* <span data-ttu-id="0e64b-169">最大重試間隔：30 分鐘</span><span class="sxs-lookup"><span data-stu-id="0e64b-169">Maximum Retry Interval: 30 minutes</span></span>
* <span data-ttu-id="0e64b-170">重試間隔係數：2</span><span class="sxs-lookup"><span data-stu-id="0e64b-170">Retry Interval Coefficient: 2</span></span>
* <span data-ttu-id="0e64b-171">嘗試上限：2,147,483,647</span><span class="sxs-lookup"><span data-stu-id="0e64b-171">Maximum Attempts: 2,147,483,647</span></span>

<span data-ttu-id="0e64b-172">建立 hello 所需執行原則：</span><span class="sxs-lookup"><span data-stu-id="0e64b-172">Create hello desired execution policy:</span></span>

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

### <a name="update-a-custom-execution-policy"></a><span data-ttu-id="0e64b-173">更新自訂執行原則</span><span class="sxs-lookup"><span data-stu-id="0e64b-173">Update a custom execution policy</span></span>
<span data-ttu-id="0e64b-174">更新所需的 hello 執行原則 tooupdate:</span><span class="sxs-lookup"><span data-stu-id="0e64b-174">Update hello desired execution policy tooupdate:</span></span>

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

## <a name="cancel-a-job"></a><span data-ttu-id="0e64b-175">取消工作</span><span class="sxs-lookup"><span data-stu-id="0e64b-175">Cancel a job</span></span>
<span data-ttu-id="0e64b-176">彈性資料庫工作支援取消工作要求。</span><span class="sxs-lookup"><span data-stu-id="0e64b-176">Elastic Database Jobs supports jobs cancellation requests.</span></span>  <span data-ttu-id="0e64b-177">如果彈性資料庫工作偵測到目前正在執行工作的取消要求，它會嘗試 toostop hello 作業。</span><span class="sxs-lookup"><span data-stu-id="0e64b-177">If Elastic Database Jobs detects a cancellation request for a job currently being executed, it will attempt toostop hello job.</span></span>

<span data-ttu-id="0e64b-178">彈性資料庫工作有兩種不同的方式可以執行取消作業：</span><span class="sxs-lookup"><span data-stu-id="0e64b-178">There are two different ways that Elastic Database Jobs can perform a cancellation:</span></span>

1. <span data-ttu-id="0e64b-179">取消目前正在執行的工作： 如果當工作目前正在執行時偵測取消，則將會取消嘗試 hello 目前正在執行的層面 hello 工作內。</span><span class="sxs-lookup"><span data-stu-id="0e64b-179">Canceling Currently Executing Tasks: If a cancellation is detected while a task is currently running, a cancellation will be attempted within hello currently executing aspect of hello task.</span></span>  <span data-ttu-id="0e64b-180">例如： 嘗試取消時，目前執行的長時間執行查詢時，會有嘗試 toocancel hello 查詢。</span><span class="sxs-lookup"><span data-stu-id="0e64b-180">For example: If there is a long running query currently being performed when a cancellation is attempted, there will be an attempt toocancel hello query.</span></span>
2. <span data-ttu-id="0e64b-181">取消工作重試次數： 如果啟動工作執行前，取消偵測到的 hello 控制執行緒，hello 控制執行緒會避免啟動 hello 工作，並宣告 hello 要求為已取消。</span><span class="sxs-lookup"><span data-stu-id="0e64b-181">Canceling Task Retries: If a cancellation is detected by hello control thread before a task is launched for execution, hello control thread will avoid launching hello task and declare hello request as canceled.</span></span>

<span data-ttu-id="0e64b-182">如果作業取消父工作的要求，hello 父工作和所有其子工作會採用 hello 取消要求。</span><span class="sxs-lookup"><span data-stu-id="0e64b-182">If a job cancellation is requested for a parent job, hello cancellation request will be honored for hello parent job and for all of its child jobs.</span></span>

<span data-ttu-id="0e64b-183">toosubmit 取消要求，使用 hello**停止 AzureSqlJobExecution** cmdlet 和設定 hello **JobExecutionId**參數。</span><span class="sxs-lookup"><span data-stu-id="0e64b-183">toosubmit a cancellation request, use hello **Stop-AzureSqlJobExecution** cmdlet and set hello **JobExecutionId** parameter.</span></span>

   ```
    $jobExecutionId = "{Job Execution Id}"
    Stop-AzureSqlJobExecution -JobExecutionId $jobExecutionId
   ```

## <a name="delete-a-job-by-name-and-hello-jobs-history"></a><span data-ttu-id="0e64b-184">刪除作業的名稱和 hello 作業歷程記錄</span><span class="sxs-lookup"><span data-stu-id="0e64b-184">Delete a job by name and hello job's history</span></span>
<span data-ttu-id="0e64b-185">彈性資料庫工作支援非同步刪除工作。</span><span class="sxs-lookup"><span data-stu-id="0e64b-185">Elastic Database jobs supports asynchronous deletion of jobs.</span></span> <span data-ttu-id="0e64b-186">作業可以標示為刪除，而且 hello 系統刪除 hello 工作和其所有的作業記錄所有作業執行都完成 hello 工作之後。</span><span class="sxs-lookup"><span data-stu-id="0e64b-186">A job can be marked for deletion and hello system will delete hello job and all its job history after all job executions have completed for hello job.</span></span> <span data-ttu-id="0e64b-187">hello 系統不會自動取消作用中的作業執行。</span><span class="sxs-lookup"><span data-stu-id="0e64b-187">hello system will not automatically cancel active job executions.</span></span>  

<span data-ttu-id="0e64b-188">相反地，停止 AzureSqlJobExecution 必須叫用的 toocancel 作用中的作業執行。</span><span class="sxs-lookup"><span data-stu-id="0e64b-188">Instead, Stop-AzureSqlJobExecution must be invoked toocancel active job executions.</span></span>

<span data-ttu-id="0e64b-189">tootrigger 作業刪除使用 hello**移除 AzureSqlJob** cmdlet 和設定 hello **JobName**參數。</span><span class="sxs-lookup"><span data-stu-id="0e64b-189">tootrigger job deletion, use hello **Remove-AzureSqlJob** cmdlet and set hello **JobName** parameter.</span></span>

   ```
    $jobName = "{Job Name}"
    Remove-AzureSqlJob -JobName $jobName
   ```

## <a name="create-a-custom-database-target"></a><span data-ttu-id="0e64b-190">建立自訂資料庫目標</span><span class="sxs-lookup"><span data-stu-id="0e64b-190">Create a custom database target</span></span>
<span data-ttu-id="0e64b-191">自訂資料庫目標可以在彈性資料庫工作中定義，可用來直接執行或包含在自訂資料庫群組內。</span><span class="sxs-lookup"><span data-stu-id="0e64b-191">Custom database targets can be defined in Elastic Database jobs which can be used either for execution directly or for inclusion within a custom database group.</span></span> <span data-ttu-id="0e64b-192">因為**彈性集區**不尚未直接支援透過 hello PowerShell Api 中，您只要建立自訂資料庫的目標，其中包含所有 hello 集區中的 hello 資料庫自訂資料庫收集目標。</span><span class="sxs-lookup"><span data-stu-id="0e64b-192">Since **elastic pools** are not yet directly supported via hello PowerShell APIs, you simply create a custom database target and custom database collection target which encompasses all hello databases in hello pool.</span></span>

<span data-ttu-id="0e64b-193">設定下列變數 tooreflect hello 預期資料庫資訊的 hello:</span><span class="sxs-lookup"><span data-stu-id="0e64b-193">Set hello following variables tooreflect hello desired database information:</span></span>

   ```
    $databaseName = "{Database Name}"
    $databaseServerName = "{Server Name}"
    New-AzureSqlJobDatabaseTarget -DatabaseName $databaseName -ServerName $databaseServerName
   ```

## <a name="create-a-custom-database-collection-target"></a><span data-ttu-id="0e64b-194">建立自訂資料庫集合目標</span><span class="sxs-lookup"><span data-stu-id="0e64b-194">Create a custom database collection target</span></span>
<span data-ttu-id="0e64b-195">自訂資料庫收集目標可以跨多個定義的資料庫的目標是定義的 tooenable 執行。</span><span class="sxs-lookup"><span data-stu-id="0e64b-195">A custom database collection target can be defined tooenable execution across multiple defined database targets.</span></span> <span data-ttu-id="0e64b-196">建立資料庫群組之後，資料庫可以是相關聯的 toohello 自訂集合目標。</span><span class="sxs-lookup"><span data-stu-id="0e64b-196">After a database group is created, databases can be associated toohello custom collection target.</span></span>

<span data-ttu-id="0e64b-197">設定下列變數 tooreflect hello 所需的自訂集合目標組態 hello:</span><span class="sxs-lookup"><span data-stu-id="0e64b-197">Set hello following variables tooreflect hello desired custom collection target configuration:</span></span>

   ```
    $customCollectionName = "{Custom Database Collection Name}"
    New-AzureSqlJobTarget -CustomCollectionName $customCollectionName
   ```

### <a name="add-databases-tooa-custom-database-collection-target"></a><span data-ttu-id="0e64b-198">新增資料庫 tooa 自訂資料庫收集目標</span><span class="sxs-lookup"><span data-stu-id="0e64b-198">Add databases tooa custom database collection target</span></span>
<span data-ttu-id="0e64b-199">資料庫的目標可以是自訂的資料庫集合為目標 toocreate 資料庫的群組相關聯。</span><span class="sxs-lookup"><span data-stu-id="0e64b-199">Database targets can be associated with custom database collection targets toocreate a group of databases.</span></span> <span data-ttu-id="0e64b-200">每次建立工作目標為自訂的資料庫集合的目標，它會展開的 tootarget hello 資料庫相關聯的 toohello 群組在 hello 執行的時間。</span><span class="sxs-lookup"><span data-stu-id="0e64b-200">Whenever a job is created that targets a custom database collection target, it will be expanded tootarget hello databases associated toohello group at hello time of execution.</span></span>

<span data-ttu-id="0e64b-201">加入所需的 hello 資料庫 tooa 特定自訂集合：</span><span class="sxs-lookup"><span data-stu-id="0e64b-201">Add hello desired database tooa specific custom collection:</span></span>

   ```
    $serverName = "{Database Server Name}"
    $databaseName = "{Database Name}"
    $customCollectionName = "{Custom Database Collection Name}"
    Add-AzureSqlJobChildTarget -CustomCollectionName $customCollectionName -DatabaseName $databaseName -ServerName $databaseServerName
   ```

#### <a name="review-hello-databases-within-a-custom-database-collection-target"></a><span data-ttu-id="0e64b-202">檢閱 hello 資料庫內的自訂資料庫收集目標</span><span class="sxs-lookup"><span data-stu-id="0e64b-202">Review hello databases within a custom database collection target</span></span>
<span data-ttu-id="0e64b-203">使用 hello **Get AzureSqlJobTarget** cmdlet tooretrieve hello 子資料庫內的自訂資料庫收集目標。</span><span class="sxs-lookup"><span data-stu-id="0e64b-203">Use hello **Get-AzureSqlJobTarget** cmdlet tooretrieve hello child databases within a custom database collection target.</span></span>

   ```
    $customCollectionName = "{Custom Database Collection Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    $childTargets = Get-AzureSqlJobTarget -ParentTargetId $target.TargetId
    Write-Output $childTargets
   ```

### <a name="create-a-job-tooexecute-a-script-across-a-custom-database-collection-target"></a><span data-ttu-id="0e64b-204">建立指令碼工作 tooexecute 跨自訂資料庫收集目標</span><span class="sxs-lookup"><span data-stu-id="0e64b-204">Create a job tooexecute a script across a custom database collection target</span></span>
<span data-ttu-id="0e64b-205">使用 hello**新增 AzureSqlJob** cmdlet toocreate 作業會每天針對資料庫定義的自訂資料庫收集目標的群組。</span><span class="sxs-lookup"><span data-stu-id="0e64b-205">Use hello **New-AzureSqlJob** cmdlet toocreate a job against a group of databases defined by a custom database collection target.</span></span> <span data-ttu-id="0e64b-206">彈性資料庫工作會展開成多個子工作，每個對應的 tooa 資料庫與 hello 自訂資料庫收集目標關聯，並確保 hello 指令碼執行的每個資料庫的 hello 作業。</span><span class="sxs-lookup"><span data-stu-id="0e64b-206">Elastic Database jobs will expand hello job into multiple child jobs each corresponding tooa database associated with hello custom database collection target and ensure that hello script is executed against each database.</span></span> <span data-ttu-id="0e64b-207">同樣地，請務必指令碼是等冪 toobe 彈性 tooretries。</span><span class="sxs-lookup"><span data-stu-id="0e64b-207">Again, it is important that scripts are idempotent toobe resilient tooretries.</span></span>

   ```
    $jobName = "{Job Name}"
    $scriptName = "{Script Name}"
    $customCollectionName = "{Custom Collection Name}"
    $credentialName = "{Credential Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    $job = New-AzureSqlJob -JobName $jobName -CredentialName $credentialName -ContentName $scriptName -TargetId $target.TargetId
    Write-Output $job
   ```

## <a name="data-collection-across-databases"></a><span data-ttu-id="0e64b-208">跨資料庫的資料集合</span><span class="sxs-lookup"><span data-stu-id="0e64b-208">Data collection across databases</span></span>
<span data-ttu-id="0e64b-209">**彈性資料庫工作**支援跨資料庫的群組執行查詢，並傳送嗨結果 tooa 指定的資料庫資料表。</span><span class="sxs-lookup"><span data-stu-id="0e64b-209">**Elastic Database jobs** supports executing a query across a group of databases and sends hello results tooa specified database’s table.</span></span> <span data-ttu-id="0e64b-210">hello 資料表可以查詢之後每個資料庫的 hello 事實 toosee hello 查詢的結果。</span><span class="sxs-lookup"><span data-stu-id="0e64b-210">hello table can be queried after hello fact toosee hello query’s results from each database.</span></span> <span data-ttu-id="0e64b-211">這樣非同步機制 tooexecute 查詢跨多個資料庫。</span><span class="sxs-lookup"><span data-stu-id="0e64b-211">This provides an asynchronous mechanism tooexecute a query across many databases.</span></span> <span data-ttu-id="0e64b-212">失敗的情況下，例如其中一個 hello 暫時無法使用的資料庫會自動處理透過重試次數。</span><span class="sxs-lookup"><span data-stu-id="0e64b-212">Failure cases such as one of hello databases being temporarily unavailable are handled automatically via retries.</span></span>

<span data-ttu-id="0e64b-213">如果它尚未存在自動建立 hello 指定的目的地資料表，傳回結果集的比對的 hello 結構描述的 hello。</span><span class="sxs-lookup"><span data-stu-id="0e64b-213">hello specified destination table will be automatically created if it does not yet exist, matching hello schema of hello returned result set.</span></span> <span data-ttu-id="0e64b-214">如果指令碼執行傳回多個結果集，彈性資料庫工作才會傳送 hello 第一次一個 toohello 提供目的地資料表。</span><span class="sxs-lookup"><span data-stu-id="0e64b-214">If a script execution returns multiple result sets, Elastic Database jobs will only send hello first one toohello provided destination table.</span></span>

<span data-ttu-id="0e64b-215">hello 下列 PowerShell 指令碼可以使用的 tooexecute 收集其結果至指定資料表的指令碼。</span><span class="sxs-lookup"><span data-stu-id="0e64b-215">hello following PowerShell script can be used tooexecute a script collecting its results into a specified table.</span></span> <span data-ttu-id="0e64b-216">此指令碼假設已建立 T-SQL 指令碼，它會輸出單一結果集，且自訂資料庫集合目標已建立。</span><span class="sxs-lookup"><span data-stu-id="0e64b-216">This script assumes that a T-SQL script has been created which outputs a single result set and a custom database collection target has been created.</span></span>

<span data-ttu-id="0e64b-217">設定下列 tooreflect hello 預期指令碼、 認證和執行目標的 hello:</span><span class="sxs-lookup"><span data-stu-id="0e64b-217">Set hello following tooreflect hello desired script, credentials, and execution target:</span></span>

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

### <a name="create-and-start-a-job-for-data-collection-scenarios"></a><span data-ttu-id="0e64b-218">建立和啟動資料庫集合案例的工作</span><span class="sxs-lookup"><span data-stu-id="0e64b-218">Create and start a job for data collection scenarios</span></span>
   ```
    $job = New-AzureSqlJob -JobName $jobName -CredentialName $executionCredentialName -ContentName $scriptName -ResultSetDestinationServerName $destinationServerName -ResultSetDestinationDatabaseName $destinationDatabaseName -ResultSetDestinationSchemaName $destinationSchemaName -ResultSetDestinationTableName $destinationTableName -ResultSetDestinationCredentialName $destinationCredentialName -TargetId $target.TargetId
    Write-Output $job
    $jobExecution = Start-AzureSqlJobExecution -JobName $jobName
    Write-Output $jobExecution
   ```

## <a name="create-a-schedule-for-job-execution-using-a-job-trigger"></a><span data-ttu-id="0e64b-219">使用工作觸發程序建立工作執行的排程</span><span class="sxs-lookup"><span data-stu-id="0e64b-219">Create a schedule for job execution using a job trigger</span></span>
<span data-ttu-id="0e64b-220">hello 下列 PowerShell 指令碼可以使用的 toocreate 重複發生的排程。</span><span class="sxs-lookup"><span data-stu-id="0e64b-220">hello following PowerShell script can be used toocreate a reoccurring schedule.</span></span> <span data-ttu-id="0e64b-221">這個指令碼使用分鐘間隔，但是 New-AzureSqlJobSchedule 也支援 -DayInterval、-HourInterval、-MonthInterval 和 -WeekInterval 參數。</span><span class="sxs-lookup"><span data-stu-id="0e64b-221">This script uses a one minute interval, but New-AzureSqlJobSchedule also supports -DayInterval, -HourInterval, -MonthInterval, and -WeekInterval parameters.</span></span> <span data-ttu-id="0e64b-222">您可以藉由傳遞 -OneTime，建立僅執行一次的排程。</span><span class="sxs-lookup"><span data-stu-id="0e64b-222">Schedules that execute only once can be created by passing -OneTime.</span></span>

<span data-ttu-id="0e64b-223">建立新的排程：</span><span class="sxs-lookup"><span data-stu-id="0e64b-223">Create a new schedule:</span></span>
   ```
    $scheduleName = "Every one minute"
    $minuteInterval = 1
    $startTime = (Get-Date).ToUniversalTime()
    $schedule = New-AzureSqlJobSchedule -MinuteInterval $minuteInterval -ScheduleName $scheduleName -StartTime $startTime
    Write-Output $schedule
   ```

### <a name="create-a-job-trigger-toohave-a-job-executed-on-a-time-schedule"></a><span data-ttu-id="0e64b-224">建立工作觸發程序 toohave 作業的時間排程執行</span><span class="sxs-lookup"><span data-stu-id="0e64b-224">Create a job trigger toohave a job executed on a time schedule</span></span>
<span data-ttu-id="0e64b-225">工作觸發程序可以定義的 toohave 作業執行相應 tooa 時間排程。</span><span class="sxs-lookup"><span data-stu-id="0e64b-225">A job trigger can be defined toohave a job executed according tooa time schedule.</span></span> <span data-ttu-id="0e64b-226">hello 下列 PowerShell 指令碼可以使用的 toocreate 工作觸發程序。</span><span class="sxs-lookup"><span data-stu-id="0e64b-226">hello following PowerShell script can be used toocreate a job trigger.</span></span>

<span data-ttu-id="0e64b-227">下列變數 toocorrespond toohello 組 hello 預期作業和排程：</span><span class="sxs-lookup"><span data-stu-id="0e64b-227">Set hello following variables toocorrespond toohello desired job and schedule:</span></span>

   ```
    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    $jobTrigger = New-AzureSqlJobTrigger -ScheduleName $scheduleName -JobName $jobName
    Write-Output $jobTrigger
   ```

### <a name="remove-a-scheduled-association-toostop-job-from-executing-on-schedule"></a><span data-ttu-id="0e64b-228">移除排程的關聯 toostop 作業依排程執行</span><span class="sxs-lookup"><span data-stu-id="0e64b-228">Remove a scheduled association toostop job from executing on schedule</span></span>
<span data-ttu-id="0e64b-229">可以移除 toodiscontinue 再度工作執行的工作觸發程序，hello 工作觸發程序。</span><span class="sxs-lookup"><span data-stu-id="0e64b-229">toodiscontinue reoccurring job execution through a job trigger, hello job trigger can be removed.</span></span>
<span data-ttu-id="0e64b-230">移除工作觸發程序 toostop 工作正在執行使用 hello 相應 tooa 排程**移除 AzureSqlJobTrigger** cmdlet。</span><span class="sxs-lookup"><span data-stu-id="0e64b-230">Remove a job trigger toostop a job from being executed according tooa schedule using hello **Remove-AzureSqlJobTrigger** cmdlet.</span></span>

   ```
    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    Remove-AzureSqlJobTrigger -ScheduleName $scheduleName -JobName $jobName
   ```

## <a name="import-elastic-database-query-results-tooexcel"></a><span data-ttu-id="0e64b-231">匯入彈性資料庫查詢結果 tooExcel</span><span class="sxs-lookup"><span data-stu-id="0e64b-231">Import elastic database query results tooExcel</span></span>
 <span data-ttu-id="0e64b-232">您可以匯入 hello 結果的查詢 tooan Excel 檔案。</span><span class="sxs-lookup"><span data-stu-id="0e64b-232">You can import hello results from of a query tooan Excel file.</span></span>

1. <span data-ttu-id="0e64b-233">啟動 Excel 2013。</span><span class="sxs-lookup"><span data-stu-id="0e64b-233">Launch Excel 2013.</span></span>
2. <span data-ttu-id="0e64b-234">瀏覽 toohello**資料**功能區。</span><span class="sxs-lookup"><span data-stu-id="0e64b-234">Navigate toohello **Data** ribbon.</span></span>
3. <span data-ttu-id="0e64b-235">按一下 [從其他來源]，然後按一下 [從 SQL Server]。</span><span class="sxs-lookup"><span data-stu-id="0e64b-235">Click **From Other Sources** and click **From SQL Server**.</span></span>

   ![從其他來源的 Excel 匯入](./media/sql-database-elastic-query-getting-started/exel-sources.png)

4. <span data-ttu-id="0e64b-237">在 hello**資料連線精靈**輸入 hello 伺服器名稱和登入認證。</span><span class="sxs-lookup"><span data-stu-id="0e64b-237">In hello **Data Connection Wizard** type hello server name and login credentials.</span></span> <span data-ttu-id="0e64b-238">然後按 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="0e64b-238">Then click **Next**.</span></span>
5. <span data-ttu-id="0e64b-239">在 hello 對話方塊**選取 hello 資料庫包含您想要的 hello 資料**，選取 hello **ElasticDBQuery**資料庫。</span><span class="sxs-lookup"><span data-stu-id="0e64b-239">In hello dialog box **Select hello database that contains hello data you want**, select hello **ElasticDBQuery** database.</span></span>
6. <span data-ttu-id="0e64b-240">選取 hello**客戶**hello 清單檢視中資料表，並按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="0e64b-240">Select hello **Customers** table in hello list view and click **Next**.</span></span> <span data-ttu-id="0e64b-241">然後按一下 [ **完成**]。</span><span class="sxs-lookup"><span data-stu-id="0e64b-241">Then click **Finish**.</span></span>
7. <span data-ttu-id="0e64b-242">在 hello**匯入資料**底下形成**選取您要如何 tooview 這項資料在活頁簿中**，選取**資料表**按一下**[確定]**。</span><span class="sxs-lookup"><span data-stu-id="0e64b-242">In hello **Import Data** form, under **Select how you want tooview this data in your workbook**, select **Table** and click **OK**.</span></span>

<span data-ttu-id="0e64b-243">所有 hello 中的資料列**客戶**儲存在不同的分區中的資料表填入 hello Excel 工作表。</span><span class="sxs-lookup"><span data-stu-id="0e64b-243">All hello rows from **Customers** table, stored in different shards populate hello Excel sheet.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0e64b-244">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0e64b-244">Next steps</span></span>
<span data-ttu-id="0e64b-245">您現在可以使用 Excel 的資料功能。</span><span class="sxs-lookup"><span data-stu-id="0e64b-245">You can now use Excel’s data functions.</span></span> <span data-ttu-id="0e64b-246">使用您的伺服器名稱、 資料庫名稱 hello 連接字串和認證 tooconnect BI 和資料整合工具 toohello 彈性查詢資料庫。</span><span class="sxs-lookup"><span data-stu-id="0e64b-246">Use hello connection string with your server name, database name and credentials tooconnect your BI and data integration tools toohello elastic query database.</span></span> <span data-ttu-id="0e64b-247">請確定 SQL Server 可支援做為您的工具的資料來源。</span><span class="sxs-lookup"><span data-stu-id="0e64b-247">Make sure that SQL Server is supported as a data source for your tool.</span></span> <span data-ttu-id="0e64b-248">請參閱 toohello 彈性查詢資料庫，就像任何其他 SQL Server 資料庫的外部資料表和連線 toowith 工具的 SQL Server 資料表。</span><span class="sxs-lookup"><span data-stu-id="0e64b-248">Refer toohello elastic query database and external tables just like any other SQL Server database and SQL Server tables that you would connect toowith your tool.</span></span>

### <a name="cost"></a><span data-ttu-id="0e64b-249">成本</span><span class="sxs-lookup"><span data-stu-id="0e64b-249">Cost</span></span>
<span data-ttu-id="0e64b-250">沒有另收費用使用 hello 彈性資料庫查詢功能。</span><span class="sxs-lookup"><span data-stu-id="0e64b-250">There is no additional charge for using hello Elastic Database query feature.</span></span> <span data-ttu-id="0e64b-251">不過，此時這項功能僅適用於高階資料庫做為結束點，但 hello 分區可以是任何服務層。</span><span class="sxs-lookup"><span data-stu-id="0e64b-251">However, at this time this feature is available only on premium databases as an end point, but hello shards can be of any service tier.</span></span>

<span data-ttu-id="0e64b-252">如需價格資訊，請參閱 [SQL Database 價格詳細資料](https://azure.microsoft.com/pricing/details/sql-database/)。</span><span class="sxs-lookup"><span data-stu-id="0e64b-252">For pricing information see [SQL Database Pricing Details](https://azure.microsoft.com/pricing/details/sql-database/).</span></span>

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-query-getting-started/cmd-prompt.png
[2]: ./media/sql-database-elastic-query-getting-started/portal.png
[3]: ./media/sql-database-elastic-query-getting-started/tiers.png
[4]: ./media/sql-database-elastic-query-getting-started/details.png
[5]: ./media/sql-database-elastic-query-getting-started/exel-sources.png
<!--anchors-->
