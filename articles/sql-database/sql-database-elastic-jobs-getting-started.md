---
title: "開始使用彈性資料庫工作 | Microsoft Docs"
description: "如何使用彈性資料庫工作"
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
ms.openlocfilehash: 05c20e880d4eb1eacdecc0c4c7e7491dfe1e6a89
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="getting-started-with-elastic-database-jobs"></a><span data-ttu-id="e28d9-103">開始使用彈性資料庫工作</span><span class="sxs-lookup"><span data-stu-id="e28d9-103">Getting started with Elastic Database jobs</span></span>
<span data-ttu-id="e28d9-104">Azure SQL database 的彈性資料庫工作 (預覽) 可讓您跨越多個資料庫可靠地執行 T-SQL 指令碼，同時自動重試並提供最終完成保證。</span><span class="sxs-lookup"><span data-stu-id="e28d9-104">Elastic Database jobs (preview) for Azure SQL Database allows you to reliability execute T-SQL scripts that span multiple databases while automatically retrying and providing eventual completion guarantees.</span></span> <span data-ttu-id="e28d9-105">如需有關彈性資料庫工作功能的詳細資訊，請參閱 [功能概觀頁](sql-database-elastic-jobs-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="e28d9-105">For more information about the Elastic Database job feature, please see the [feature overview page](sql-database-elastic-jobs-overview.md).</span></span>

<span data-ttu-id="e28d9-106">本主題會延伸 [彈性資料庫工具入門](sql-database-elastic-scale-get-started.md)中可找到的範例。</span><span class="sxs-lookup"><span data-stu-id="e28d9-106">This topic extends the sample found in [Getting started with Elastic Database tools](sql-database-elastic-scale-get-started.md).</span></span> <span data-ttu-id="e28d9-107">完成時，您將會：了解如何建立和管理工作，該工作管理一組相關資料庫。</span><span class="sxs-lookup"><span data-stu-id="e28d9-107">When completed, you will: learn how to create and manage jobs that manage a group of related databases.</span></span> <span data-ttu-id="e28d9-108">您不需要使用「彈性延展」工具，就能善用彈性工作的優點。</span><span class="sxs-lookup"><span data-stu-id="e28d9-108">It is not required to use the Elastic Scale tools in order to take advantage of the benefits of Elastic jobs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e28d9-109">必要條件</span><span class="sxs-lookup"><span data-stu-id="e28d9-109">Prerequisites</span></span>
<span data-ttu-id="e28d9-110">下載並執行 [彈性資料庫工具範例入門](sql-database-elastic-scale-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="e28d9-110">Download and run the [Getting started with Elastic Database tools sample](sql-database-elastic-scale-get-started.md).</span></span>

## <a name="create-a-shard-map-manager-using-the-sample-app"></a><span data-ttu-id="e28d9-111">使用範例應用程式建立分區對應管理員</span><span class="sxs-lookup"><span data-stu-id="e28d9-111">Create a shard map manager using the sample app</span></span>
<span data-ttu-id="e28d9-112">在這裡，您將建立分區對應管理員以及數個分區，接著插入資料至分區。</span><span class="sxs-lookup"><span data-stu-id="e28d9-112">Here you will create a shard map manager along with several shards, followed by insertion of data into the shards.</span></span> <span data-ttu-id="e28d9-113">若您的分區設定中已有分區資料，則可以略過下列步驟並移至下一節。</span><span class="sxs-lookup"><span data-stu-id="e28d9-113">If you already have shards set up with sharded data in them, you can skip the following steps and move to the next section.</span></span>

1. <span data-ttu-id="e28d9-114">建置並執行 **彈性資料庫工具入門** 範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="e28d9-114">Build and run the **Getting started with Elastic Database tools** sample application.</span></span> <span data-ttu-id="e28d9-115">遵循步驟，直到[下載及執行範例應用程式](sql-database-elastic-scale-get-started.md#download-and-run-the-sample-app)小節的步驟 7。</span><span class="sxs-lookup"><span data-stu-id="e28d9-115">Follow the steps until step 7 in the section [Download and run the sample app](sql-database-elastic-scale-get-started.md#download-and-run-the-sample-app).</span></span> <span data-ttu-id="e28d9-116">在步驟 7 結束時，您會看到下列的命令提示字元：</span><span class="sxs-lookup"><span data-stu-id="e28d9-116">At the end of Step 7, you will see the following command prompt:</span></span>

   ![命令提示字元](./media/sql-database-elastic-query-getting-started/cmd-prompt.png)

2. <span data-ttu-id="e28d9-118">在命令視窗中，輸入 "1"，然後按 **Enter**。</span><span class="sxs-lookup"><span data-stu-id="e28d9-118">In the command window, type "1" and press **Enter**.</span></span> <span data-ttu-id="e28d9-119">這會建立分區對應管理員，並加入兩個分區到伺服器。</span><span class="sxs-lookup"><span data-stu-id="e28d9-119">This creates the shard map manager, and adds two shards to the server.</span></span> <span data-ttu-id="e28d9-120">接著輸入 "3"，然後按 **Enter**；重複此動作四次。</span><span class="sxs-lookup"><span data-stu-id="e28d9-120">Then type "3" and press **Enter**; repeat this action four times.</span></span> <span data-ttu-id="e28d9-121">這會在您的分區中插入範例資料列。</span><span class="sxs-lookup"><span data-stu-id="e28d9-121">This inserts sample data rows in your shards.</span></span>
3. <span data-ttu-id="e28d9-122">[Azure 入口網站](https://portal.azure.com)應該會顯示三個新的資料庫：</span><span class="sxs-lookup"><span data-stu-id="e28d9-122">The [Azure Portal](https://portal.azure.com) should show three new databases:</span></span>

   ![Visual Studio 確認](./media/sql-database-elastic-query-getting-started/portal.png)

   <span data-ttu-id="e28d9-124">目前，我們將建立自訂資料庫集合，反映分區對應中的所有資料庫。</span><span class="sxs-lookup"><span data-stu-id="e28d9-124">At this point, we will create a custom database collection that reflects all the databases in the shard map.</span></span> <span data-ttu-id="e28d9-125">這可讓我們建立和執行工作，跨分區新增新資料表。</span><span class="sxs-lookup"><span data-stu-id="e28d9-125">This will allow us to create and execute a job that add a new table across shards.</span></span>

<span data-ttu-id="e28d9-126">在這裡我們通常會建立分區對應目標，使用 **New-AzureSqlJobTarget** Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="e28d9-126">Here we would usually create a shard map target, using the **New-AzureSqlJobTarget** cmdlet.</span></span> <span data-ttu-id="e28d9-127">分區對應管理員資料庫必須設定為資料庫目標，然後將特定分區對應指定為目標。</span><span class="sxs-lookup"><span data-stu-id="e28d9-127">The shard map manager database must be set as a database target and then the specific shard map is specified as a target.</span></span> <span data-ttu-id="e28d9-128">相反地，我們列舉伺服器中的所有資料庫，並且將資料庫新增至 master 資料庫除外的新的自訂集合。</span><span class="sxs-lookup"><span data-stu-id="e28d9-128">Instead, we are going to enumerate all the databases in the server and add the databases to the new custom collection with the exception of master database.</span></span>

## <a name="creates-a-custom-collection-and-add-all-databases-in-the-server-to-the-custom-collection-target-with-the-exception-of-master"></a><span data-ttu-id="e28d9-129">建立自訂集合，然後將伺服器中的所有資料庫 (master 除外) 新增至自訂集合目標。</span><span class="sxs-lookup"><span data-stu-id="e28d9-129">Creates a custom collection and add all databases in the server to the custom collection target with the exception of master.</span></span>
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
             Write-Host $currentdb "is already in the custom collection target" $CustomCollectionName"."
        }

        else
        {
            throw $_
        }
    }
    $ErrorActionPreference = "Continue"
   }
   ```
## <a name="create-a-t-sql-script-for-execution-across-databases"></a><span data-ttu-id="e28d9-130">針對跨資料庫執行建立 T-SQL 指令碼</span><span class="sxs-lookup"><span data-stu-id="e28d9-130">Create a T-SQL Script for execution across databases</span></span>
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

## <a name="create-the-job-to-execute-a-script-across-the-custom-group-of-databases"></a><span data-ttu-id="e28d9-131">建立工作以跨自訂資料庫群組執行指令碼</span><span class="sxs-lookup"><span data-stu-id="e28d9-131">Create the job to execute a script across the custom group of databases</span></span>

   ```
    $jobName = "create on server dbs"
    $scriptName = "NewTable"
    $customCollectionName = "dbs_in_server"
    $credentialName = "ddove66"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    $job = New-AzureSqlJob -JobName $jobName -CredentialName $credentialName -ContentName $scriptName -TargetId $target.TargetId
    Write-Output $job
   ```

## <a name="execute-the-job"></a><span data-ttu-id="e28d9-132">執行工作</span><span class="sxs-lookup"><span data-stu-id="e28d9-132">Execute the job</span></span>
<span data-ttu-id="e28d9-133">下列 PowerShell 指令碼可以用來執行現有的工作：</span><span class="sxs-lookup"><span data-stu-id="e28d9-133">The following PowerShell script can be used to execute an existing job:</span></span>

<span data-ttu-id="e28d9-134">更新下列變數以反映要執行的所需工作名稱：</span><span class="sxs-lookup"><span data-stu-id="e28d9-134">Update the following variable to reflect the desired job name to have executed:</span></span>

   ```
    $jobName = "create on server dbs"
    $jobExecution = Start-AzureSqlJobExecution -JobName $jobName
    Write-Output $jobExecution
   ```

## <a name="retrieve-the-state-of-a-single-job-execution"></a><span data-ttu-id="e28d9-135">擷取單一工作執行狀態</span><span class="sxs-lookup"><span data-stu-id="e28d9-135">Retrieve the state of a single job execution</span></span>
<span data-ttu-id="e28d9-136">使用相同 **Get-AzureSqlJobExecution** Cmdlet 搭配 **IncludeChildren** 參數，以檢視子工作執行的狀態，也就是工作在每個目標資料庫上的每個工作執行的特定狀態。</span><span class="sxs-lookup"><span data-stu-id="e28d9-136">Use the same **Get-AzureSqlJobExecution** cmdlet with the **IncludeChildren** parameter to view the state of child job executions, namely the specific state for each job execution against each database targeted by the job.</span></span>

   ```
    $jobExecutionId = "{Job Execution Id}"
    $jobExecutions = Get-AzureSqlJobExecution -JobExecutionId $jobExecutionId -IncludeChildren
    Write-Output $jobExecutions
   ```

## <a name="view-the-state-across-multiple-job-executions"></a><span data-ttu-id="e28d9-137">檢視跨多個工作執行的狀態</span><span class="sxs-lookup"><span data-stu-id="e28d9-137">View the state across multiple job executions</span></span>
<span data-ttu-id="e28d9-138">**Get-AzureSqlJobExecution** Cmdlet 具有多個選用參數，可用來顯示多個工作執行、透過提供的參數篩選。</span><span class="sxs-lookup"><span data-stu-id="e28d9-138">The **Get-AzureSqlJobExecution** cmdlet has multiple optional parameters that can be used to display multiple job executions, filtered through the provided parameters.</span></span> <span data-ttu-id="e28d9-139">以下示範一些使用 Get-AzureSqlJobExecution 的可能方式：</span><span class="sxs-lookup"><span data-stu-id="e28d9-139">The following demonstrates some of the possible ways to use Get-AzureSqlJobExecution:</span></span>

<span data-ttu-id="e28d9-140">擷取所有作用中最上層工作執行：</span><span class="sxs-lookup"><span data-stu-id="e28d9-140">Retrieve all active top level job executions:</span></span>

   ```
    Get-AzureSqlJobExecution
   ```

<span data-ttu-id="e28d9-141">擷取所有最上層工作執行，包括非使用中工作執行：</span><span class="sxs-lookup"><span data-stu-id="e28d9-141">Retrieve all top level job executions, including inactive job executions:</span></span>

   ```
    Get-AzureSqlJobExecution -IncludeInactive
   ```

<span data-ttu-id="e28d9-142">擷取已提供工作執行 ID 的所有子工作執行，包括非使用中工作執行：</span><span class="sxs-lookup"><span data-stu-id="e28d9-142">Retrieve all child job executions of a provided job execution ID, including inactive job executions:</span></span>

   ```
    $parentJobExecutionId = "{Job Execution Id}"
    Get-AzureSqlJobExecution -AzureSqlJobExecution -JobExecutionId $parentJobExecutionId -IncludeInactive -IncludeChildren
   ```

<span data-ttu-id="e28d9-143">擷取使用排程/工作組合建立的所有工作執行，包括非使用中工作：</span><span class="sxs-lookup"><span data-stu-id="e28d9-143">Retrieve all job executions created using a schedule / job combination, including inactive jobs:</span></span>

   ```
    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    Get-AzureSqlJobExecution -JobName $jobName -ScheduleName $scheduleName -IncludeInactive
   ```

<span data-ttu-id="e28d9-144">擷取以指定的分區對應為目標的所有工作，包括非使用中工作：</span><span class="sxs-lookup"><span data-stu-id="e28d9-144">Retrieve all jobs targeting a specified shard map, including inactive jobs:</span></span>

   ```
    $shardMapServerName = "{Shard Map Server Name}"
    $shardMapDatabaseName = "{Shard Map Database Name}"
    $shardMapName = "{Shard Map Name}"
    $target = Get-AzureSqlJobTarget -ShardMapManagerDatabaseName $shardMapDatabaseName -ShardMapManagerServerName $shardMapServerName -ShardMapName $shardMapName
    Get-AzureSqlJobExecution -TargetId $target.TargetId -IncludeInactive
   ```

<span data-ttu-id="e28d9-145">擷取以指定的自訂集合為目標的所有工作，包括非使用中工作：</span><span class="sxs-lookup"><span data-stu-id="e28d9-145">Retrieve all jobs targeting a specified custom collection, including inactive jobs:</span></span>

   ```
    $customCollectionName = "{Custom Collection Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    Get-AzureSqlJobExecution -TargetId $target.TargetId -IncludeInactive
   ```

<span data-ttu-id="e28d9-146">擷取特定工作執行內的工作作業執行的清單：</span><span class="sxs-lookup"><span data-stu-id="e28d9-146">Retrieve the list of job task executions within a specific job execution:</span></span>

   ```
    $jobExecutionId = "{Job Execution Id}"
    $jobTaskExecutions = Get-AzureSqlJobTaskExecution -JobExecutionId $jobExecutionId
    Write-Output $jobTaskExecutions
   ```

<span data-ttu-id="e28d9-147">擷取工作作業執行詳細資料：</span><span class="sxs-lookup"><span data-stu-id="e28d9-147">Retrieve job task execution details:</span></span>

<span data-ttu-id="e28d9-148">下列 PowerShell 指令碼可用來檢視工作作業執行的詳細資料，在偵錯執行失敗時特別有用。</span><span class="sxs-lookup"><span data-stu-id="e28d9-148">The following PowerShell script can be used to view the details of a job task execution, which is particularly useful when debugging execution failures.</span></span>
   ```
    $jobTaskExecutionId = "{Job Task Execution Id}"
    $jobTaskExecution = Get-AzureSqlJobTaskExecution -JobTaskExecutionId $jobTaskExecutionId
    Write-Output $jobTaskExecution
   ```

## <a name="retrieve-failures-within-job-task-executions"></a><span data-ttu-id="e28d9-149">擷取工作作業執行內的失敗</span><span class="sxs-lookup"><span data-stu-id="e28d9-149">Retrieve failures within job task executions</span></span>
<span data-ttu-id="e28d9-150">JobTaskExecution 物件包括作業生命週期的屬性和訊息屬性。</span><span class="sxs-lookup"><span data-stu-id="e28d9-150">The JobTaskExecution object includes a property for the Lifecycle of the task along with a Message property.</span></span> <span data-ttu-id="e28d9-151">如果工作作業執行失敗，生命週期屬性將設為 *失敗* ，且訊息屬性將設為產生的例外狀況訊息和其堆疊。</span><span class="sxs-lookup"><span data-stu-id="e28d9-151">If a job task execution failed, the Lifecycle property will be set to *Failed* and the Message property will be set to the resulting exception message and its stack.</span></span> <span data-ttu-id="e28d9-152">如果工作不成功，務必檢視指定作業不成功的工作作業的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="e28d9-152">If a job did not succeed, it is important to view the details of job tasks that did not succeed for a given job.</span></span>

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

## <a name="waiting-for-a-job-execution-to-complete"></a><span data-ttu-id="e28d9-153">等候工作執行完成</span><span class="sxs-lookup"><span data-stu-id="e28d9-153">Waiting for a job execution to complete</span></span>
<span data-ttu-id="e28d9-154">下列 PowerShell 指令碼可以用來等候工作作業完成：</span><span class="sxs-lookup"><span data-stu-id="e28d9-154">The following PowerShell script can be used to wait for a job task to complete:</span></span>

   ```
    $jobExecutionId = "{Job Execution Id}"
    Wait-AzureSqlJobExecution -JobExecutionId $jobExecutionId
   ```

## <a name="create-a-custom-execution-policy"></a><span data-ttu-id="e28d9-155">建立自訂執行原則</span><span class="sxs-lookup"><span data-stu-id="e28d9-155">Create a custom execution policy</span></span>
<span data-ttu-id="e28d9-156">彈性資料庫工作支援建立自訂執行原則，可以在啟動作業時套用。</span><span class="sxs-lookup"><span data-stu-id="e28d9-156">Elastic Database jobs supports creating custom execution policies that can be applied when starting jobs.</span></span>

<span data-ttu-id="e28d9-157">執行原則目前允許定義：</span><span class="sxs-lookup"><span data-stu-id="e28d9-157">Execution policies currently allow for defining:</span></span>

* <span data-ttu-id="e28d9-158">名稱：執行原則的識別碼。</span><span class="sxs-lookup"><span data-stu-id="e28d9-158">Name: Identifier for the execution policy.</span></span>
* <span data-ttu-id="e28d9-159">工作逾時：彈性資料庫工作取消工作之前的總時間。</span><span class="sxs-lookup"><span data-stu-id="e28d9-159">Job Timeout: Total time before a job will be canceled by Elastic Database Jobs.</span></span>
* <span data-ttu-id="e28d9-160">初始重試間隔：第一次重試之前等候的間隔。</span><span class="sxs-lookup"><span data-stu-id="e28d9-160">Initial Retry Interval: Interval to wait before first retry.</span></span>
* <span data-ttu-id="e28d9-161">最大重試間隔：要使用的重試間隔端點。</span><span class="sxs-lookup"><span data-stu-id="e28d9-161">Maximum Retry Interval: Cap of retry intervals to use.</span></span>
* <span data-ttu-id="e28d9-162">重試間隔輪詢係數：用來計算重試之間下一個間隔的係數。</span><span class="sxs-lookup"><span data-stu-id="e28d9-162">Retry Interval Backoff Coefficient: Coefficient used to calculate the next interval between retries.</span></span>  <span data-ttu-id="e28d9-163">使用下列公式：(初始重試間隔) * Math.pow ((間隔輪詢係數), (重試次數) -2)。</span><span class="sxs-lookup"><span data-stu-id="e28d9-163">The following formula is used: (Initial Retry Interval) * Math.pow((Interval Backoff Coefficient), (Number of Retries) - 2).</span></span>
* <span data-ttu-id="e28d9-164">嘗試上限：工作內執行的重試嘗試數目上限。</span><span class="sxs-lookup"><span data-stu-id="e28d9-164">Maximum Attempts: The maximum number of retry attempts to perform within a job.</span></span>

<span data-ttu-id="e28d9-165">預設的執行原則會使用下列值：</span><span class="sxs-lookup"><span data-stu-id="e28d9-165">The default execution policy uses the following values:</span></span>

* <span data-ttu-id="e28d9-166">名稱：預設執行原則</span><span class="sxs-lookup"><span data-stu-id="e28d9-166">Name: Default execution policy</span></span>
* <span data-ttu-id="e28d9-167">工作逾時：1 週</span><span class="sxs-lookup"><span data-stu-id="e28d9-167">Job Timeout: 1 week</span></span>
* <span data-ttu-id="e28d9-168">初始重試間隔：100 毫秒</span><span class="sxs-lookup"><span data-stu-id="e28d9-168">Initial Retry Interval:  100 milliseconds</span></span>
* <span data-ttu-id="e28d9-169">最大重試間隔：30 分鐘</span><span class="sxs-lookup"><span data-stu-id="e28d9-169">Maximum Retry Interval: 30 minutes</span></span>
* <span data-ttu-id="e28d9-170">重試間隔係數：2</span><span class="sxs-lookup"><span data-stu-id="e28d9-170">Retry Interval Coefficient: 2</span></span>
* <span data-ttu-id="e28d9-171">嘗試上限：2,147,483,647</span><span class="sxs-lookup"><span data-stu-id="e28d9-171">Maximum Attempts: 2,147,483,647</span></span>

<span data-ttu-id="e28d9-172">建立想要的執行原則：</span><span class="sxs-lookup"><span data-stu-id="e28d9-172">Create the desired execution policy:</span></span>

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

### <a name="update-a-custom-execution-policy"></a><span data-ttu-id="e28d9-173">更新自訂執行原則</span><span class="sxs-lookup"><span data-stu-id="e28d9-173">Update a custom execution policy</span></span>
<span data-ttu-id="e28d9-174">更新要更新之想要的執行原則：</span><span class="sxs-lookup"><span data-stu-id="e28d9-174">Update the desired execution policy to update:</span></span>

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

## <a name="cancel-a-job"></a><span data-ttu-id="e28d9-175">取消工作</span><span class="sxs-lookup"><span data-stu-id="e28d9-175">Cancel a job</span></span>
<span data-ttu-id="e28d9-176">彈性資料庫工作支援取消工作要求。</span><span class="sxs-lookup"><span data-stu-id="e28d9-176">Elastic Database Jobs supports jobs cancellation requests.</span></span>  <span data-ttu-id="e28d9-177">如果彈性資料庫工作偵測到目前正在執行工作的取消要求，它會嘗試停止工作。</span><span class="sxs-lookup"><span data-stu-id="e28d9-177">If Elastic Database Jobs detects a cancellation request for a job currently being executed, it will attempt to stop the job.</span></span>

<span data-ttu-id="e28d9-178">彈性資料庫工作有兩種不同的方式可以執行取消作業：</span><span class="sxs-lookup"><span data-stu-id="e28d9-178">There are two different ways that Elastic Database Jobs can perform a cancellation:</span></span>

1. <span data-ttu-id="e28d9-179">取消目前正在執行的作業：如果在作業正在執行時偵測到取消，將會在目前正在執行的作業層面內嘗試取消。</span><span class="sxs-lookup"><span data-stu-id="e28d9-179">Canceling Currently Executing Tasks: If a cancellation is detected while a task is currently running, a cancellation will be attempted within the currently executing aspect of the task.</span></span>  <span data-ttu-id="e28d9-180">例如：當嘗試取消時，如果有長時間執行查詢目前正在執行，將會嘗試取消查詢。</span><span class="sxs-lookup"><span data-stu-id="e28d9-180">For example: If there is a long running query currently being performed when a cancellation is attempted, there will be an attempt to cancel the query.</span></span>
2. <span data-ttu-id="e28d9-181">取消作業重試：如果控制執行緒在啟動作業執行之前偵測到取消，控制執行緒會避免啟動作業，並且將要求宣告為已取消。</span><span class="sxs-lookup"><span data-stu-id="e28d9-181">Canceling Task Retries: If a cancellation is detected by the control thread before a task is launched for execution, the control thread will avoid launching the task and declare the request as canceled.</span></span>

<span data-ttu-id="e28d9-182">如果針對父工作要求工作取消，則會對父工作和其所有子工作執行取消要求。</span><span class="sxs-lookup"><span data-stu-id="e28d9-182">If a job cancellation is requested for a parent job, the cancellation request will be honored for the parent job and for all of its child jobs.</span></span>

<span data-ttu-id="e28d9-183">若要提交取消要求，請使用 **Stop-AzureSqlJobExecution** Cmdlet 並設定 **JobExecutionId** 參數。</span><span class="sxs-lookup"><span data-stu-id="e28d9-183">To submit a cancellation request, use the **Stop-AzureSqlJobExecution** cmdlet and set the **JobExecutionId** parameter.</span></span>

   ```
    $jobExecutionId = "{Job Execution Id}"
    Stop-AzureSqlJobExecution -JobExecutionId $jobExecutionId
   ```

## <a name="delete-a-job-by-name-and-the-jobs-history"></a><span data-ttu-id="e28d9-184">依據名稱和工作的歷程記錄刪除工作</span><span class="sxs-lookup"><span data-stu-id="e28d9-184">Delete a job by name and the job's history</span></span>
<span data-ttu-id="e28d9-185">彈性資料庫工作支援非同步刪除工作。</span><span class="sxs-lookup"><span data-stu-id="e28d9-185">Elastic Database jobs supports asynchronous deletion of jobs.</span></span> <span data-ttu-id="e28d9-186">工作可以標示為刪除，系統將會在工作的工作執行皆已完成之後，刪除工作和其所有工作歷程記錄。</span><span class="sxs-lookup"><span data-stu-id="e28d9-186">A job can be marked for deletion and the system will delete the job and all its job history after all job executions have completed for the job.</span></span> <span data-ttu-id="e28d9-187">系統不會自動取消作用中的工作執行。</span><span class="sxs-lookup"><span data-stu-id="e28d9-187">The system will not automatically cancel active job executions.</span></span>  

<span data-ttu-id="e28d9-188">而是必須叫用 Stop-AzureSqlJobExecution 以取消作用中的工作執行。</span><span class="sxs-lookup"><span data-stu-id="e28d9-188">Instead, Stop-AzureSqlJobExecution must be invoked to cancel active job executions.</span></span>

<span data-ttu-id="e28d9-189">若要觸發工作刪除，請使用 **Remove-AzureSqlJob** Cmdlet 並設定 **JobName** 參數。</span><span class="sxs-lookup"><span data-stu-id="e28d9-189">To trigger job deletion, use the **Remove-AzureSqlJob** cmdlet and set the **JobName** parameter.</span></span>

   ```
    $jobName = "{Job Name}"
    Remove-AzureSqlJob -JobName $jobName
   ```

## <a name="create-a-custom-database-target"></a><span data-ttu-id="e28d9-190">建立自訂資料庫目標</span><span class="sxs-lookup"><span data-stu-id="e28d9-190">Create a custom database target</span></span>
<span data-ttu-id="e28d9-191">自訂資料庫目標可以在彈性資料庫工作中定義，可用來直接執行或包含在自訂資料庫群組內。</span><span class="sxs-lookup"><span data-stu-id="e28d9-191">Custom database targets can be defined in Elastic Database jobs which can be used either for execution directly or for inclusion within a custom database group.</span></span> <span data-ttu-id="e28d9-192">由於透過 PowerShell API 還無法直接支援「彈性集區」，因此您只需建立自訂資料庫目標和自訂資料庫集合目標，以包含集區中的所有資料庫。</span><span class="sxs-lookup"><span data-stu-id="e28d9-192">Since **elastic pools** are not yet directly supported via the PowerShell APIs, you simply create a custom database target and custom database collection target which encompasses all the databases in the pool.</span></span>

<span data-ttu-id="e28d9-193">設定下列變數以反映所需的資料庫資訊：</span><span class="sxs-lookup"><span data-stu-id="e28d9-193">Set the following variables to reflect the desired database information:</span></span>

   ```
    $databaseName = "{Database Name}"
    $databaseServerName = "{Server Name}"
    New-AzureSqlJobDatabaseTarget -DatabaseName $databaseName -ServerName $databaseServerName
   ```

## <a name="create-a-custom-database-collection-target"></a><span data-ttu-id="e28d9-194">建立自訂資料庫集合目標</span><span class="sxs-lookup"><span data-stu-id="e28d9-194">Create a custom database collection target</span></span>
<span data-ttu-id="e28d9-195">可以定義自訂資料庫集合目標，以跨多個已定義資料庫目標執行。</span><span class="sxs-lookup"><span data-stu-id="e28d9-195">A custom database collection target can be defined to enable execution across multiple defined database targets.</span></span> <span data-ttu-id="e28d9-196">建立資料庫群組之後，資料庫可以與自訂集合目標相關聯。</span><span class="sxs-lookup"><span data-stu-id="e28d9-196">After a database group is created, databases can be associated to the custom collection target.</span></span>

<span data-ttu-id="e28d9-197">設定下列變數以反映所需的自訂集合目標組態：</span><span class="sxs-lookup"><span data-stu-id="e28d9-197">Set the following variables to reflect the desired custom collection target configuration:</span></span>

   ```
    $customCollectionName = "{Custom Database Collection Name}"
    New-AzureSqlJobTarget -CustomCollectionName $customCollectionName
   ```

### <a name="add-databases-to-a-custom-database-collection-target"></a><span data-ttu-id="e28d9-198">將資料庫新增至自訂資料庫集合目標</span><span class="sxs-lookup"><span data-stu-id="e28d9-198">Add databases to a custom database collection target</span></span>
<span data-ttu-id="e28d9-199">資料庫目標可以與自訂資料庫集合目標相關聯，以建立資料庫群組。</span><span class="sxs-lookup"><span data-stu-id="e28d9-199">Database targets can be associated with custom database collection targets to create a group of databases.</span></span> <span data-ttu-id="e28d9-200">每當建立以自訂資料庫集合目標為目標的工作時，都會擴展為以關聯至執行中的群組的資料庫為目標。</span><span class="sxs-lookup"><span data-stu-id="e28d9-200">Whenever a job is created that targets a custom database collection target, it will be expanded to target the databases associated to the group at the time of execution.</span></span>

<span data-ttu-id="e28d9-201">將所需的資料庫新增至特定自訂集合：</span><span class="sxs-lookup"><span data-stu-id="e28d9-201">Add the desired database to a specific custom collection:</span></span>

   ```
    $serverName = "{Database Server Name}"
    $databaseName = "{Database Name}"
    $customCollectionName = "{Custom Database Collection Name}"
    Add-AzureSqlJobChildTarget -CustomCollectionName $customCollectionName -DatabaseName $databaseName -ServerName $databaseServerName
   ```

#### <a name="review-the-databases-within-a-custom-database-collection-target"></a><span data-ttu-id="e28d9-202">檢閱自訂資料庫集合目標內的資料庫</span><span class="sxs-lookup"><span data-stu-id="e28d9-202">Review the databases within a custom database collection target</span></span>
<span data-ttu-id="e28d9-203">使用 **Get-AzureSqlJobTarget** Cmdlet 以擷取自訂資料庫集合目標內的子資料庫。</span><span class="sxs-lookup"><span data-stu-id="e28d9-203">Use the **Get-AzureSqlJobTarget** cmdlet to retrieve the child databases within a custom database collection target.</span></span>

   ```
    $customCollectionName = "{Custom Database Collection Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    $childTargets = Get-AzureSqlJobTarget -ParentTargetId $target.TargetId
    Write-Output $childTargets
   ```

### <a name="create-a-job-to-execute-a-script-across-a-custom-database-collection-target"></a><span data-ttu-id="e28d9-204">建立工作以跨自訂資料庫集合目標執行指令碼</span><span class="sxs-lookup"><span data-stu-id="e28d9-204">Create a job to execute a script across a custom database collection target</span></span>
<span data-ttu-id="e28d9-205">使用 **New-AzureSqlJob** Cmdlet 以根據自訂資料庫集合目標定義的資料庫群組建立工作。</span><span class="sxs-lookup"><span data-stu-id="e28d9-205">Use the **New-AzureSqlJob** cmdlet to create a job against a group of databases defined by a custom database collection target.</span></span> <span data-ttu-id="e28d9-206">彈性資料庫工作會將工作展開成多個子工作，每個子工作對應至與自訂資料庫集合目標相關聯的資料庫，並且確保指令碼會針對每個資料庫執行。</span><span class="sxs-lookup"><span data-stu-id="e28d9-206">Elastic Database jobs will expand the job into multiple child jobs each corresponding to a database associated with the custom database collection target and ensure that the script is executed against each database.</span></span> <span data-ttu-id="e28d9-207">再次重申，很重要的是指令碼具有等冪處理重試的彈性。</span><span class="sxs-lookup"><span data-stu-id="e28d9-207">Again, it is important that scripts are idempotent to be resilient to retries.</span></span>

   ```
    $jobName = "{Job Name}"
    $scriptName = "{Script Name}"
    $customCollectionName = "{Custom Collection Name}"
    $credentialName = "{Credential Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    $job = New-AzureSqlJob -JobName $jobName -CredentialName $credentialName -ContentName $scriptName -TargetId $target.TargetId
    Write-Output $job
   ```

## <a name="data-collection-across-databases"></a><span data-ttu-id="e28d9-208">跨資料庫的資料集合</span><span class="sxs-lookup"><span data-stu-id="e28d9-208">Data collection across databases</span></span>
<span data-ttu-id="e28d9-209">**彈性資料庫工作** 支援跨資料庫群組執行查詢，並將結果傳送至指定的資料庫資料表。</span><span class="sxs-lookup"><span data-stu-id="e28d9-209">**Elastic Database jobs** supports executing a query across a group of databases and sends the results to a specified database’s table.</span></span> <span data-ttu-id="e28d9-210">可以在事實之後查詢資料表，以查看每個資料庫的查詢結果。</span><span class="sxs-lookup"><span data-stu-id="e28d9-210">The table can be queried after the fact to see the query’s results from each database.</span></span> <span data-ttu-id="e28d9-211">這提供跨多個資料庫執行查詢的非同步機制。</span><span class="sxs-lookup"><span data-stu-id="e28d9-211">This provides an asynchronous mechanism to execute a query across many databases.</span></span> <span data-ttu-id="e28d9-212">例如其中一個資料庫暫時無法使用的失敗案例是透過重試自動處理。</span><span class="sxs-lookup"><span data-stu-id="e28d9-212">Failure cases such as one of the databases being temporarily unavailable are handled automatically via retries.</span></span>

<span data-ttu-id="e28d9-213">如果指定的目的地資料表尚未存在以對應於傳回的結果集的結構描述，則會自動建立。</span><span class="sxs-lookup"><span data-stu-id="e28d9-213">The specified destination table will be automatically created if it does not yet exist, matching the schema of the returned result set.</span></span> <span data-ttu-id="e28d9-214">如果指令碼執行傳回多個結果集，彈性資料庫工作只會將第一個傳送至提供的目的地資料表。</span><span class="sxs-lookup"><span data-stu-id="e28d9-214">If a script execution returns multiple result sets, Elastic Database jobs will only send the first one to the provided destination table.</span></span>

<span data-ttu-id="e28d9-215">下列 PowerShell 指令碼可以用來執行指令碼，將其結果收集至指定的資料表。</span><span class="sxs-lookup"><span data-stu-id="e28d9-215">The following PowerShell script can be used to execute a script collecting its results into a specified table.</span></span> <span data-ttu-id="e28d9-216">此指令碼假設已建立 T-SQL 指令碼，它會輸出單一結果集，且自訂資料庫集合目標已建立。</span><span class="sxs-lookup"><span data-stu-id="e28d9-216">This script assumes that a T-SQL script has been created which outputs a single result set and a custom database collection target has been created.</span></span>

<span data-ttu-id="e28d9-217">設定下列項目以反映所需的指令碼、認證和執行目標：</span><span class="sxs-lookup"><span data-stu-id="e28d9-217">Set the following to reflect the desired script, credentials, and execution target:</span></span>

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

### <a name="create-and-start-a-job-for-data-collection-scenarios"></a><span data-ttu-id="e28d9-218">建立和啟動資料庫集合案例的工作</span><span class="sxs-lookup"><span data-stu-id="e28d9-218">Create and start a job for data collection scenarios</span></span>
   ```
    $job = New-AzureSqlJob -JobName $jobName -CredentialName $executionCredentialName -ContentName $scriptName -ResultSetDestinationServerName $destinationServerName -ResultSetDestinationDatabaseName $destinationDatabaseName -ResultSetDestinationSchemaName $destinationSchemaName -ResultSetDestinationTableName $destinationTableName -ResultSetDestinationCredentialName $destinationCredentialName -TargetId $target.TargetId
    Write-Output $job
    $jobExecution = Start-AzureSqlJobExecution -JobName $jobName
    Write-Output $jobExecution
   ```

## <a name="create-a-schedule-for-job-execution-using-a-job-trigger"></a><span data-ttu-id="e28d9-219">使用工作觸發程序建立工作執行的排程</span><span class="sxs-lookup"><span data-stu-id="e28d9-219">Create a schedule for job execution using a job trigger</span></span>
<span data-ttu-id="e28d9-220">下列 PowerShell 指令碼可以用來建立重複排程。</span><span class="sxs-lookup"><span data-stu-id="e28d9-220">The following PowerShell script can be used to create a reoccurring schedule.</span></span> <span data-ttu-id="e28d9-221">這個指令碼使用分鐘間隔，但是 New-AzureSqlJobSchedule 也支援 -DayInterval、-HourInterval、-MonthInterval 和 -WeekInterval 參數。</span><span class="sxs-lookup"><span data-stu-id="e28d9-221">This script uses a one minute interval, but New-AzureSqlJobSchedule also supports -DayInterval, -HourInterval, -MonthInterval, and -WeekInterval parameters.</span></span> <span data-ttu-id="e28d9-222">您可以藉由傳遞 -OneTime，建立僅執行一次的排程。</span><span class="sxs-lookup"><span data-stu-id="e28d9-222">Schedules that execute only once can be created by passing -OneTime.</span></span>

<span data-ttu-id="e28d9-223">建立新的排程：</span><span class="sxs-lookup"><span data-stu-id="e28d9-223">Create a new schedule:</span></span>
   ```
    $scheduleName = "Every one minute"
    $minuteInterval = 1
    $startTime = (Get-Date).ToUniversalTime()
    $schedule = New-AzureSqlJobSchedule -MinuteInterval $minuteInterval -ScheduleName $scheduleName -StartTime $startTime
    Write-Output $schedule
   ```

### <a name="create-a-job-trigger-to-have-a-job-executed-on-a-time-schedule"></a><span data-ttu-id="e28d9-224">建立工作觸發程序，讓工作在時間排程時執行</span><span class="sxs-lookup"><span data-stu-id="e28d9-224">Create a job trigger to have a job executed on a time schedule</span></span>
<span data-ttu-id="e28d9-225">可以定義工作觸發程序，讓工作根據時間排程執行。</span><span class="sxs-lookup"><span data-stu-id="e28d9-225">A job trigger can be defined to have a job executed according to a time schedule.</span></span> <span data-ttu-id="e28d9-226">下列 PowerShell 指令碼可以用來建立工作觸發程序。</span><span class="sxs-lookup"><span data-stu-id="e28d9-226">The following PowerShell script can be used to create a job trigger.</span></span>

<span data-ttu-id="e28d9-227">設定下列變數以對應所需的工作和排程：</span><span class="sxs-lookup"><span data-stu-id="e28d9-227">Set the following variables to correspond to the desired job and schedule:</span></span>

   ```
    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    $jobTrigger = New-AzureSqlJobTrigger -ScheduleName $scheduleName -JobName $jobName
    Write-Output $jobTrigger
   ```

### <a name="remove-a-scheduled-association-to-stop-job-from-executing-on-schedule"></a><span data-ttu-id="e28d9-228">移除排程的關聯，以停止工作的排程執行</span><span class="sxs-lookup"><span data-stu-id="e28d9-228">Remove a scheduled association to stop job from executing on schedule</span></span>
<span data-ttu-id="e28d9-229">若要透過工作觸發程序中止工作重複執行，可以移除工作觸發程序。</span><span class="sxs-lookup"><span data-stu-id="e28d9-229">To discontinue reoccurring job execution through a job trigger, the job trigger can be removed.</span></span>
<span data-ttu-id="e28d9-230">使用 **Remove-AzureSqlJobTrigger** Cmdlet，移除工作觸發程序以停止工作根據排程執行。</span><span class="sxs-lookup"><span data-stu-id="e28d9-230">Remove a job trigger to stop a job from being executed according to a schedule using the **Remove-AzureSqlJobTrigger** cmdlet.</span></span>

   ```
    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    Remove-AzureSqlJobTrigger -ScheduleName $scheduleName -JobName $jobName
   ```

## <a name="import-elastic-database-query-results-to-excel"></a><span data-ttu-id="e28d9-231">匯入彈性資料庫查詢結果到 Excel</span><span class="sxs-lookup"><span data-stu-id="e28d9-231">Import elastic database query results to Excel</span></span>
 <span data-ttu-id="e28d9-232">您可以從查詢的結果匯入到 Excel 檔案。</span><span class="sxs-lookup"><span data-stu-id="e28d9-232">You can import the results from of a query to an Excel file.</span></span>

1. <span data-ttu-id="e28d9-233">啟動 Excel 2013。</span><span class="sxs-lookup"><span data-stu-id="e28d9-233">Launch Excel 2013.</span></span>
2. <span data-ttu-id="e28d9-234">瀏覽至 [ **資料** ] 功能區。</span><span class="sxs-lookup"><span data-stu-id="e28d9-234">Navigate to the **Data** ribbon.</span></span>
3. <span data-ttu-id="e28d9-235">按一下 [從其他來源]，然後按一下 [從 SQL Server]。</span><span class="sxs-lookup"><span data-stu-id="e28d9-235">Click **From Other Sources** and click **From SQL Server**.</span></span>

   ![從其他來源的 Excel 匯入](./media/sql-database-elastic-query-getting-started/exel-sources.png)

4. <span data-ttu-id="e28d9-237">在 [ **資料連線精靈** ] 中，輸入伺服器名稱和登入認證。</span><span class="sxs-lookup"><span data-stu-id="e28d9-237">In the **Data Connection Wizard** type the server name and login credentials.</span></span> <span data-ttu-id="e28d9-238">然後按 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="e28d9-238">Then click **Next**.</span></span>
5. <span data-ttu-id="e28d9-239">在對話方塊 [選取包含您想要的資料的資料庫] 中，選取 **ElasticDBQuery** 資料庫。</span><span class="sxs-lookup"><span data-stu-id="e28d9-239">In the dialog box **Select the database that contains the data you want**, select the **ElasticDBQuery** database.</span></span>
6. <span data-ttu-id="e28d9-240">在清單檢視中選取 [客戶] 資料表，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="e28d9-240">Select the **Customers** table in the list view and click **Next**.</span></span> <span data-ttu-id="e28d9-241">然後按一下 [ **完成**]。</span><span class="sxs-lookup"><span data-stu-id="e28d9-241">Then click **Finish**.</span></span>
7. <span data-ttu-id="e28d9-242">在 [匯入資料] 表單中，於 [選取您要在活頁簿中檢視此資料的方式] 下，選取 [資料表]，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="e28d9-242">In the **Import Data** form, under **Select how you want to view this data in your workbook**, select **Table** and click **OK**.</span></span>

<span data-ttu-id="e28d9-243">儲存在不同分區中、來自 [客戶]  資料表的所有資料列會填入 Excel 工作表。</span><span class="sxs-lookup"><span data-stu-id="e28d9-243">All the rows from **Customers** table, stored in different shards populate the Excel sheet.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e28d9-244">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e28d9-244">Next steps</span></span>
<span data-ttu-id="e28d9-245">您現在可以使用 Excel 的資料功能。</span><span class="sxs-lookup"><span data-stu-id="e28d9-245">You can now use Excel’s data functions.</span></span> <span data-ttu-id="e28d9-246">使用具備伺服器名稱、資料庫名稱和認證的連接字串，將您的 BI 和資料整合工具連接至彈性查詢資料庫。</span><span class="sxs-lookup"><span data-stu-id="e28d9-246">Use the connection string with your server name, database name and credentials to connect your BI and data integration tools to the elastic query database.</span></span> <span data-ttu-id="e28d9-247">請確定 SQL Server 可支援做為您的工具的資料來源。</span><span class="sxs-lookup"><span data-stu-id="e28d9-247">Make sure that SQL Server is supported as a data source for your tool.</span></span> <span data-ttu-id="e28d9-248">參考彈性查詢資料庫和外部資料表，就如同您會使用您的工具連接的任何其他 SQL Server 資料庫和 SQL Server 資料表。</span><span class="sxs-lookup"><span data-stu-id="e28d9-248">Refer to the elastic query database and external tables just like any other SQL Server database and SQL Server tables that you would connect to with your tool.</span></span>

### <a name="cost"></a><span data-ttu-id="e28d9-249">成本</span><span class="sxs-lookup"><span data-stu-id="e28d9-249">Cost</span></span>
<span data-ttu-id="e28d9-250">使用彈性資料庫的查詢功能不另行收費。</span><span class="sxs-lookup"><span data-stu-id="e28d9-250">There is no additional charge for using the Elastic Database query feature.</span></span> <span data-ttu-id="e28d9-251">不過，目前這項功能僅適用於 Premium 資料庫做為端點，但分區可以是任何服務層。</span><span class="sxs-lookup"><span data-stu-id="e28d9-251">However, at this time this feature is available only on premium databases as an end point, but the shards can be of any service tier.</span></span>

<span data-ttu-id="e28d9-252">如需價格資訊，請參閱 [SQL Database 價格詳細資料](https://azure.microsoft.com/pricing/details/sql-database/)。</span><span class="sxs-lookup"><span data-stu-id="e28d9-252">For pricing information see [SQL Database Pricing Details](https://azure.microsoft.com/pricing/details/sql-database/).</span></span>

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-query-getting-started/cmd-prompt.png
[2]: ./media/sql-database-elastic-query-getting-started/portal.png
[3]: ./media/sql-database-elastic-query-getting-started/tiers.png
[4]: ./media/sql-database-elastic-query-getting-started/details.png
[5]: ./media/sql-database-elastic-query-getting-started/exel-sources.png
<!--anchors-->
