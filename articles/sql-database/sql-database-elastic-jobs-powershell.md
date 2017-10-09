---
title: "aaaCreate 及管理彈性的工作，使用 PowerShell |Microsoft 文件"
description: "使用 PowerShell toomanage Azure SQL Database 的集區"
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
ms.assetid: 737d8d13-5632-4e18-9cb0-4d3b8a19e495
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: f6c18aecfa7e8c0b102a3b7cd2f266f5542ae400
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-sql-database-elastic-jobs-using-powershell-preview"></a>使用 PowerShell 建立和管理 SQL Database 彈性作業 (預覽)

hello PowerShell Api 的**彈性資料庫工作**（處於預覽階段），可讓您定義指令碼可執行針對這個資料庫的群組。 本文將說明如何 toocreate 和管理**彈性資料庫工作**使用 PowerShell cmdlet。 請參閱 [彈性工作概觀](sql-database-elastic-jobs-overview.md)。 

## <a name="prerequisites"></a>必要條件
* Azure 訂用帳戶。 如需免費試用，請參閱 [免費試用一個月](https://azure.microsoft.com/pricing/free-trial/)。
* 一組使用 hello 彈性資料庫工具所建立的資料庫。 請參閱 [開始使用彈性資料庫工具](sql-database-elastic-scale-get-started.md)。
* Azure PowerShell。 如需詳細資訊，請參閱[如何 tooinstall 和設定 Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview)。
* **彈性資料庫工作** PowerShell 封裝：請參閱 [安裝彈性資料庫工作](sql-database-elastic-jobs-service-installation.md)

### <a name="select-your-azure-subscription"></a>選取您的 Azure 訂用帳戶
您需要您的訂用帳戶 Id tooselect hello 訂用帳戶 (**-SubscriptionId**) 或訂用帳戶名稱 (**-訂用帳戶名稱**)。 如果您有多個訂用帳戶，您就可以執行 hello **Get AzureRmSubscription** cmdlet，並複製 hello 預期從 hello 結果集的訂閱資訊。 訂用帳戶資訊之後，執行下列 commandlet tooset hello hello 預設為此訂用帳戶，也就是 hello 建立和管理作業的目標：

    Select-AzureRmSubscription -SubscriptionId {SubscriptionID}

hello [PowerShell ISE](https://technet.microsoft.com/library/dd315244.aspx)使用量 toodevelop 建議，並執行 PowerShell 指令碼針對 hello 彈性資料庫工作。

## <a name="elastic-database-jobs-objects"></a>彈性資料庫工作物件
下列表格列出所有 hello 物件類型的 hello**彈性資料庫工作**以及其描述和相關的 PowerShell Api。

<table style="width:100%">
  <tr>
    <th>物件類型</th>
    <th>說明</th>
    <th>相關 PowerShell API</th>
  </tr>
  <tr>
    <td>認證</td>
    <td>使用者名稱和密碼 toouse 連接執行的指令碼或應用程式的 Dacpac toodatabases 時。 <p>hello 密碼是之前傳送 tooand hello 彈性資料庫工作的資料庫中儲存加密。  hello 密碼是由 hello 彈性資料庫工作服務，透過建立及上傳 hello 安裝指令碼中的 hello 認證解密。</td>
    <td><p>Get-AzureSqlJobCredential</p>
    <p>New-AzureSqlJobCredential</p><p>Set-AzureSqlJobCredential</p></td></td>
  </tr>

  <tr>
    <td>指令碼</td>
    <td>TRANSACT-SQL 指令碼 toobe 跨資料庫執行時使用。  hello 指令碼應該撰寫的 toobe 具有等冪性，因為 hello 服務將會重試執行失敗時的 hello 指令碼。
    </td>
    <td>
    <p>Get-AzureSqlJobContent</p>
    <p>Get-AzureSqlJobContentDefinition</p>
    <p>New-AzureSqlJobContent</p>
    <p>Set-AzureSqlJobContentDefinition</p>
    </td>
  </tr>

  <tr>
    <td>DACPAC</td>
    <td><a href="https://msdn.microsoft.com/library/ee210546.aspx">資料層應用程式</a>封裝 toobe 套用於資料庫。

    </td>
    <td>
    <p>Get-AzureSqlJobContent</p>
    <p>New-AzureSqlJobContent</p>
    <p>Set-AzureSqlJobContentDefinition</p>
    </td>
  </tr>
  <tr>
    <td>資料庫目標</td>
    <td>資料庫和伺服器名稱的指標 tooan Azure SQL Database。

    </td>
    <td>
    <p>Get-AzureSqlJobTarget</p>
    <p>New-AzureSqlJobTarget</p>
    </td>
  </tr>
  <tr>
    <td>分區對應目標</td>
    <td>使用 toodetermine 資訊儲存在分區對應的彈性資料庫內的資料庫目標和認證 toobe 組合。
    </td>
    <td>
    <p>Get-AzureSqlJobTarget</p>
    <p>New-AzureSqlJobTarget</p>
    <p>Set-AzureSqlJobTarget</p>
    </td>
  </tr>
<tr>
    <td>自訂集合目標</td>
    <td>已定義的資料庫 toocollectively 群組使用來執行。</td>
    <td>
    <p>Get-AzureSqlJobTarget</p>
    <p>New-AzureSqlJobTarget</p>
    </td>
  </tr>
<tr>
    <td>自訂集合子目標</td>
    <td>從自訂集合參考的資料庫目標。</td>
    <td>
    <p>Add-AzureSqlJobChildTarget</p>
    <p>Remove-AzureSqlJobChildTarget</p>
    </td>
  </tr>

<tr>
    <td>作業</td>
    <td>
    <p>可以使用的 tootrigger 執行或 toofulfill 排程的作業參數的定義。</p>
    </td>
    <td>
    <p>Get-AzureSqlJob</p>
    <p>New-AzureSqlJob</p>
    <p>Set-AzureSqlJob</p>
    </td>
  </tr>

<tr>
    <td>工作執行</td>
    <td>
    <p>容器的可執行的指令碼，或套用使用認證的資料庫連線失敗與 DACPAC tooa 目標工作所需 toofulfill 處理素來 tooan 執行原則。</p>
    </td>
    <td>
    <p>Get-AzureSqlJobExecution</p>
    <p>Start-AzureSqlJobExecution</p>
    <p>Stop-AzureSqlJobExecution</p>
    <p>Wait-AzureSqlJobExecution</p>
  </tr>

<tr>
    <td>工作作業執行</td>
    <td>
    <p>單一工作 toofulfill 工作單位。</p>
    <p>如果作業工作不能 toosuccessfully 執行、 hello 產生的例外狀況訊息將會記錄和新的比對作業工作將會建立和執行素來 toohello 指定在執行原則。</p></p>
    </td>
    <td>
    <p>Get-AzureSqlJobExecution</p>
    <p>Start-AzureSqlJobExecution</p>
    <p>Stop-AzureSqlJobExecution</p>
    <p>Wait-AzureSqlJobExecution</p>
  </tr>

<tr>
    <td>工作執行原則</td>
    <td>
    <p>控制重試之間的工作執行逾時、重試限制和間隔。</p>
    <p>彈性資料庫工作包括預設工作執行原則，基本上會導致無限的工作作業失敗重試，每次重試之間具有間隔的指數輪詢。</p>
    </td>
    <td>
    <p>Get-AzureSqlJobExecutionPolicy</p>
    <p>New-AzureSqlJobExecutionPolicy</p>
    <p>Set-AzureSqlJobExecutionPolicy</p>
    </td>
  </tr>

<tr>
    <td>排程</td>
    <td>
    <p>時間基礎執行 tootake 位置上重複的間隔或一次的規格。</p>
    </td>
    <td>
    <p>Get-AzureSqlJobSchedule</p>
    <p>New-AzureSqlJobSchedule</p>
    <p>Set-AzureSqlJobSchedule</p>
    </td>
  </tr>

<tr>
    <td>工作觸發程序</td>
    <td>
    <p>作業和排程 tootrigger 作業執行根據 toohello 排程之間的對應。</p>
    </td>
    <td>
    <p>New-AzureSqlJobTrigger</p>
    <p>Remove-AzureSqlJobTrigger</p>
    </td>
  </tr>
</table>

## <a name="supported-elastic-database-jobs-group-types"></a>支援的彈性資料庫工作群組類型
hello 作業將整個群組的資料庫執行 TRANSACT-SQL (T-SQL) 指令碼或應用程式的 Dacpac。 工作執行時送出的 toobe 執行跨群組的資料庫，hello 工作 「 展開 」 hello 成子工作會在其中每個執行 hello 要求針對 hello 群組中的單一資料庫執行。 

您可以建立兩種群組： 

* [分區對應](sql-database-elastic-scale-shard-map-management.md)群組： hello 工作提交的 tootarget 分區對應作業時，查詢 hello 分區對應 toodetermine 其目前的分區集，並接著會建立子工作的每個分區 hello 分區對應中。
* 自訂集合群組：一組自訂定義的資料庫。 當作業目標的自訂集合時，它會建立子工作的每個資料庫目前 hello 自訂集合中。

## <a name="tooset-hello-elastic-database-jobs-connection"></a>tooset hello 彈性資料庫工作的連接
連線需要 toobe 設定 toohello 工作*控制資料庫*先前 toousing hello 作業 Api。 執行這個指令程式會觸發認證視窗 toopop 向上要求建立安裝彈性資料庫工作時 hello 使用者名稱和密碼。 本主題中提供的所有範例都假設已經執行第一個步驟。

開啟連接 toohello 彈性資料庫工作：

    Use-AzureSqlJobConnection -CurrentAzureSubscription 

## <a name="encrypted-credentials-within-hello-elastic-database-jobs"></a>Hello 彈性資料庫工作中的加密的認證
資料庫認證可以插入到 hello 作業*控制資料庫*及其密碼加密。 它是必要的 toostore 認證 tooenable 作業 toobe 稍後的時間，在執行 （使用作業排程）。

加密可以通過 hello 安裝指令碼的過程中建立的憑證。 hello 安裝指令碼建立和上傳 hello hello Azure 雲端服務的 hello 的解密憑證已儲存的加密的密碼。 稍後 hello Azure 雲端服務儲存 hello hello 作業內的公用金鑰*控制資料庫*而不需要 hello 憑證讓 hello PowerShell API 或 Azure 傳統入口網站介面 tooencrypt 提供的密碼在本機安裝 toobe。

hello 認證密碼會加密且安全的唯讀存取 tooElastic 資料庫作業物件的使用者。 但是，具有讀寫存取 tooElastic 資料庫工作物件 tooextract 密碼的惡意使用者可能會。 認證是設計的 toobe 重複用在作業執行。 建立連接時，會傳遞 tootarget 資料庫認證。 目前使用的每個認證的 hello 目標資料庫上沒有任何限制，惡意使用者無法加入資料庫目標 hello 惡意使用者的控制之下的資料庫。 hello 使用者之後無法啟動目標為此資料庫 toogain hello 認證密碼的工作。

彈性資料庫工作的安全性最佳作法包括：

* 限制的 hello Api tootrusted 個人的使用量。
* 憑證應該具有 hello 最低權限所需的 tooperform hello 作業工作。  如需詳細資訊，請參閱 [SQL Server 中的授權和權限](https://msdn.microsoft.com/library/bb669084.aspx) 這篇 MSDN 文章。

### <a name="toocreate-an-encrypted-credential-for-job-execution-across-databases"></a>toocreate 跨資料庫的工作執行的是加密的認證
toocreate 加密新認證，hello [ **Get-credential cmdlet** ](https://technet.microsoft.com/library/hh849815.aspx)提示輸入使用者名稱和密碼，可傳遞 toohello [**新增 AzureSqlJobCredentialcmdlet**](/powershell/module/elasticdatabasejobs/new-azuresqljobcredential)。

    $credentialName = "{Credential Name}"
    $databaseCredential = Get-Credential
    $credential = New-AzureSqlJobCredential -Credential $databaseCredential -CredentialName $credentialName
    Write-Output $credential

### <a name="tooupdate-credentials"></a>tooupdate 認證
當密碼變更時，使用 hello [**組 AzureSqlJobCredential cmdlet** ](/powershell/module/elasticdatabasejobs/set-azuresqljobcredential)組 hello 和**CredentialName**參數。

    $credentialName = "{Credential Name}"
    Set-AzureSqlJobCredential -CredentialName $credentialName -Credential $credential 

## <a name="toodefine-an-elastic-database-shard-map-target"></a>toodefine 的彈性資料庫分區對應目標
tooexecute 針對分區集中的所有資料庫作業 (使用建立[彈性資料庫用戶端程式庫](sql-database-elastic-database-client-library.md))，當做 hello 資料庫目標使用分區對應。 這個範例需要使用 hello 彈性資料庫用戶端程式庫建立的分區化應用程式。 請參閱 [開始使用彈性資料庫工具範例](sql-database-elastic-scale-get-started.md)。

hello 分區對應管理員資料庫必須設定為資料庫目標，則必須指定 hello 特定分區對應做為目標。

    $shardMapCredentialName = "{Credential Name}"
    $shardMapDatabaseName = "{ShardMapDatabaseName}" #example: ElasticScaleStarterKit_ShardMapManagerDb
    $shardMapDatabaseServerName = "{ShardMapServerName}"
    $shardMapName = "{MyShardMap}" #example: CustomerIDShardMap
    $shardMapDatabaseTarget = New-AzureSqlJobTarget -DatabaseName $shardMapDatabaseName -ServerName $shardMapDatabaseServerName
    $shardMapTarget = New-AzureSqlJobTarget -ShardMapManagerCredentialName $shardMapCredentialName -ShardMapManagerDatabaseName $shardMapDatabaseName -ShardMapManagerServerName $shardMapDatabaseServerName -ShardMapName $shardMapName
    Write-Output $shardMapTarget

## <a name="create-a-t-sql-script-for-execution-across-databases"></a>針對跨資料庫執行建立 T-SQL 指令碼
在建立時執行的 T-SQL 指令碼，強烈建議 toobuild 它們 toobe[等冪](https://en.wikipedia.org/wiki/Idempotence)和彈性地防止失敗。 彈性資料庫工作會重試執行指令碼，每當執行發生失敗，不論 hello 失敗的 hello 分類。

使用 hello [**新增 AzureSqlJobContent cmdlet** ](/powershell/module/elasticdatabasejobs/new-azuresqljobcontent) toocreate 和儲存指令碼執行，以及設定 hello **-ContentName**和**-CommandText**參數。

    $scriptName = "Create a TestTable"

    $scriptCommandText = "
    IF NOT EXISTS (SELECT name FROM sys.tables WHERE name = 'TestTable')
    BEGIN
        CREATE TABLE TestTable(
            TestTableId INT PRIMARY KEY IDENTITY,
            InsertionTime DATETIME2
        );
    END
    GO
    INSERT INTO TestTable(InsertionTime) VALUES (sysutcdatetime());
    GO"

    $script = New-AzureSqlJobContent -ContentName $scriptName -CommandText $scriptCommandText
    Write-Output $script

### <a name="create-a-new-script-from-a-file"></a>從檔案建立新的指令碼
如果檔案內定義 hello T-SQL 指令碼，則使用這個 tooimport hello 指令碼：

    $scriptName = "My Script Imported from a File"
    $scriptPath = "{Path tooSQL File}"
    $scriptCommandText = Get-Content -Path $scriptPath
    $script = New-AzureSqlJobContent -ContentName $scriptName -CommandText $scriptCommandText
    Write-Output $script

### <a name="tooupdate-a-t-sql-script-for-execution-across-databases"></a>跨資料庫執行的 tooupdate T-SQL 指令碼
這個 PowerShell 指令碼更新 hello 現有的指令碼的 T-SQL 命令文字。

下列設定變數的 tooreflect hello 預期指令碼定義 toobe 組 hello:

    $scriptName = "Create a TestTable"
    $scriptUpdateComment = "Adding AdditionalInformation column tooTestTable"
    $scriptCommandText = "
    IF NOT EXISTS (SELECT name FROM sys.tables WHERE name = 'TestTable')
    BEGIN
    CREATE TABLE TestTable(
        TestTableId INT PRIMARY KEY IDENTITY,
        InsertionTime DATETIME2
    );
    END
    GO

    IF NOT EXISTS (SELECT columns.name FROM sys.columns INNER JOIN sys.tables on columns.object_id = tables.object_id WHERE tables.name = 'TestTable' AND columns.name = 'AdditionalInformation')
    BEGIN
    ALTER TABLE TestTable
    ADD AdditionalInformation NVARCHAR(400);
    END
    GO

    INSERT INTO TestTable(InsertionTime, AdditionalInformation) VALUES (sysutcdatetime(), 'test');
    GO"

### <a name="tooupdate-hello-definition-tooan-existing-script"></a>tooupdate hello 定義 tooan 現有指令碼
    Set-AzureSqlJobContentDefinition -ContentName $scriptName -CommandText $scriptCommandText -Comment $scriptUpdateComment 

## <a name="toocreate-a-job-tooexecute-a-script-across-a-shard-map"></a>toocreate 作業 tooexecute 跨分區對應的指令碼
此 PowerShell 指令碼會啟動工作，以跨 Elastic Scale 分區對應中每個分區執行指令碼。

下列變數 tooreflect hello 組 hello 預期指令碼和目標：

    $jobName = "{Job Name}"
    $scriptName = "{Script Name}"
    $shardMapServerName = "{Shard Map Server Name}"
    $shardMapDatabaseName = "{Shard Map Database Name}"
    $shardMapName = "{Shard Map Name}"
    $credentialName = "{Credential Name}"
    $shardMapTarget = Get-AzureSqlJobTarget -ShardMapManagerDatabaseName $shardMapDatabaseName -ShardMapManagerServerName $shardMapServerName -ShardMapName $shardMapName 
    $job = New-AzureSqlJob -ContentName $scriptName -CredentialName $credentialName -JobName $jobName -TargetId $shardMapTarget.TargetId
    Write-Output $job

## <a name="tooexecute-a-job"></a>tooexecute 作業
此 PowerShell 指令碼會執行現有工作：

更新下列執行變數 tooreflect hello 需要工作名稱 toohave hello:

    $jobName = "{Job Name}"
    $jobExecution = Start-AzureSqlJobExecution -JobName $jobName 
    Write-Output $jobExecution

## <a name="tooretrieve-hello-state-of-a-single-job-execution"></a>單一作業執行 tooretrieve hello 狀態
使用 hello [ **Get AzureSqlJobExecution cmdlet** ](/powershell/module/elasticdatabasejobs/get-azuresqljobexecution)組 hello 和**JobExecutionId**參數 tooview hello 狀態的作業執行。

    $jobExecutionId = "{Job Execution Id}"
    $jobExecution = Get-AzureSqlJobExecution -JobExecutionId $jobExecutionId
    Write-Output $jobExecution

使用 hello 相同**Get AzureSqlJobExecution** cmdlet 搭配 hello **includechildren 要求**參數 tooview hello 狀態的子工作執行，也就是 hello 每次針對每個工作在執行特定的狀態hello 作業為目標資料庫。

    $jobExecutionId = "{Job Execution Id}"
    $jobExecutions = Get-AzureSqlJobExecution -JobExecutionId $jobExecutionId -IncludeChildren
    Write-Output $jobExecutions 

## <a name="tooview-hello-state-across-multiple-job-executions"></a>跨多個工作執行 tooview hello 狀態
hello [ **Get AzureSqlJobExecution cmdlet** ](/powershell/module/elasticdatabasejobs/new-azuresqljob)具有多個選擇性參數可能是使用的 toodisplay 多個工作執行，透過提供 hello 參數篩選。 hello 以下會示範一些 hello 的可能方法 toouse Get AzureSqlJobExecution:

擷取所有作用中最上層工作執行：

    Get-AzureSqlJobExecution

擷取所有最上層工作執行，包括非使用中工作執行：

    Get-AzureSqlJobExecution -IncludeInactive

擷取已提供工作執行 ID 的所有子工作執行，包括非使用中工作執行：

    $parentJobExecutionId = "{Job Execution Id}"
    Get-AzureSqlJobExecution -AzureSqlJobExecution -JobExecutionId $parentJobExecutionId -IncludeInactive -IncludeChildren

擷取使用排程/工作組合建立的所有工作執行，包括非使用中工作：

    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    Get-AzureSqlJobExecution -JobName $jobName -ScheduleName $scheduleName -IncludeInactive

擷取以指定的分區對應為目標的所有工作，包括非使用中工作：

    $shardMapServerName = "{Shard Map Server Name}"
    $shardMapDatabaseName = "{Shard Map Database Name}"
    $shardMapName = "{Shard Map Name}"
    $target = Get-AzureSqlJobTarget -ShardMapManagerDatabaseName $shardMapDatabaseName -ShardMapManagerServerName $shardMapServerName -ShardMapName $shardMapName
    Get-AzureSqlJobExecution -TargetId $target.TargetId -IncludeInactive

擷取以指定的自訂集合為目標的所有工作，包括非使用中工作：

    $customCollectionName = "{Custom Collection Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    Get-AzureSqlJobExecution -TargetId $target.TargetId -IncludeInactive

擷取作業在特定的工作執行的工作執行 hello 清單：

    $jobExecutionId = "{Job Execution Id}"
    $jobTaskExecutions = Get-AzureSqlJobTaskExecution -JobExecutionId $jobExecutionId
    Write-Output $jobTaskExecutions 

擷取工作作業執行詳細資料：

hello 下列 PowerShell 指令碼可以使用的 tooview hello 詳細資料的作業工作執行，這特別有用偵錯時執行失敗數目。

    $jobTaskExecutionId = "{Job Task Execution Id}"
    $jobTaskExecution = Get-AzureSqlJobTaskExecution -JobTaskExecutionId $jobTaskExecutionId
    Write-Output $jobTaskExecution

## <a name="tooretrieve-failures-within-job-task-executions"></a>作業的工作執行的 tooretrieve 失敗
hello **JobTaskExecution 物件**包含 hello 生命週期的 hello 工作，以及訊息屬性的屬性。 如果作業工作執行失敗，hello 生命週期的屬性會設定太*失敗*和 hello 訊息屬性會設定 toohello 產生的例外狀況訊息和其堆疊。 如果作業失敗，會針對給定的作業不成功的作業工作的重要 tooview hello 詳細資料。

    $jobExecutionId = "{Job Execution Id}"
    $jobTaskExecutions = Get-AzureSqlJobTaskExecution -JobExecutionId $jobExecutionId
    Foreach($jobTaskExecution in $jobTaskExecutions) 
        {
        if($jobTaskExecution.Lifecycle -ne 'Succeeded')
            {
            Write-Output $jobTaskExecution
            }
        }

## <a name="toowait-for-a-job-execution-toocomplete"></a>工作執行 toocomplete 的 toowait
下列 PowerShell 指令碼的 hello 可使用的作業工作 toocomplete toowait:

    $jobExecutionId = "{Job Execution Id}"
    Wait-AzureSqlJobExecution -JobExecutionId $jobExecutionId 

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

    $executionPolicyName = "{Execution Policy Name}"
    $initialRetryInterval = New-TimeSpan -Seconds 10
    $jobTimeout = New-TimeSpan -Minutes 30
    $maximumAttempts = 999999
    $maximumRetryInterval = New-TimeSpan -Minutes 1
    $retryIntervalBackoffCoefficient = 1.5
    $executionPolicy = New-AzureSqlJobExecutionPolicy -ExecutionPolicyName $executionPolicyName -InitialRetryInterval $initialRetryInterval -JobTimeout $jobTimeout -MaximumAttempts $maximumAttempts -MaximumRetryInterval $maximumRetryInterval 
    -RetryIntervalBackoffCoefficient $retryIntervalBackoffCoefficient
    Write-Output $executionPolicy

### <a name="update-a-custom-execution-policy"></a>更新自訂執行原則
更新所需的 hello 執行原則 tooupdate:

    $executionPolicyName = "{Execution Policy Name}"
    $initialRetryInterval = New-TimeSpan -Seconds 15
    $jobTimeout = New-TimeSpan -Minutes 30
    $maximumAttempts = 999999
    $maximumRetryInterval = New-TimeSpan -Minutes 1
    $retryIntervalBackoffCoefficient = 1.5
    $updatedExecutionPolicy = Set-AzureSqlJobExecutionPolicy -ExecutionPolicyName $executionPolicyName -InitialRetryInterval $initialRetryInterval -JobTimeout $jobTimeout -MaximumAttempts $maximumAttempts -MaximumRetryInterval $maximumRetryInterval -RetryIntervalBackoffCoefficient $retryIntervalBackoffCoefficient
    Write-Output $updatedExecutionPolicy

## <a name="cancel-a-job"></a>取消工作
彈性資料庫工作支援取消工作要求。  如果彈性資料庫工作偵測到目前正在執行工作的取消要求，它會嘗試 toostop hello 作業。

彈性資料庫工作有兩種不同的方式可以執行取消作業：

1. 取消目前正在執行工作 5d;: 如果當工作目前正在執行時偵測取消，則將會取消嘗試 hello 目前正在執行的層面 hello 工作內。  例如： 嘗試取消時，目前執行的長時間執行查詢時，會有嘗試 toocancel hello 查詢。
2. 取消工作重試： hello 控制執行緒啟動工作執行前，取消偵測到的 hello 控制執行緒，如果將避免啟動 hello 工作，並宣告 hello 要求為已取消。

如果作業取消父工作的要求，hello 父工作和所有其子工作會採用 hello 取消要求。

toosubmit 取消要求，使用 hello [**停止 AzureSqlJobExecution cmdlet** ](/powershell/module/elasticdatabasejobs/stop-azuresqljobexecution)組 hello 和**JobExecutionId**參數。

    $jobExecutionId = "{Job Execution Id}"
    Stop-AzureSqlJobExecution -JobExecutionId $jobExecutionId

## <a name="toodelete-a-job-and-job-history-asynchronously"></a>toodelete 作業，以非同步方式作業歷程記錄
彈性資料庫工作支援非同步刪除工作。 作業可以標示為刪除，而且 hello 系統刪除 hello 工作和其所有的作業記錄所有作業執行都完成 hello 工作之後。 hello 系統不會自動取消作用中的作業執行。  

叫用[**停止 AzureSqlJobExecution** ](/powershell/module/elasticdatabasejobs/stop-azuresqljobexecution) toocancel 作用中的作業執行。

tootrigger 作業刪除使用 hello [**移除 AzureSqlJob cmdlet** ](/powershell/module/elasticdatabasejobs/remove-azuresqljob)組 hello 和**JobName**參數。

    $jobName = "{Job Name}"
    Remove-AzureSqlJob -JobName $jobName

## <a name="toocreate-a-custom-database-target"></a>toocreate 自訂資料庫目標
您可以定義自訂資料庫目標以直接執行或包含在自訂資料庫群組內。 例如，因為**彈性集區**是尚不直接支援使用 PowerShell Api，您可以建立自訂資料庫的目標和其中包含所有 hello 集區中的 hello 資料庫自訂資料庫收集目標。

設定下列變數 tooreflect hello 預期資料庫資訊的 hello:

    $databaseName = "{Database Name}"
    $databaseServerName = "{Server Name}"
    New-AzureSqlJobDatabaseTarget -DatabaseName $databaseName -ServerName $databaseServerName 

## <a name="toocreate-a-custom-database-collection-target"></a>toocreate 自訂資料庫收集目標
使用 hello [**新增 AzureSqlJobTarget** ](/powershell/module/elasticdatabasejobs/new-azuresqljobtarget) cmdlet toodefine 跨多個定義的資料庫目標的自訂資料庫集合目標 tooenable 執行。 在建立資料庫群組之後，資料庫可以是聯 hello 自訂集合目標。

設定下列變數 tooreflect hello 所需的自訂集合目標組態 hello:

    $customCollectionName = "{Custom Database Collection Name}"
    New-AzureSqlJobTarget -CustomCollectionName $customCollectionName 

### <a name="tooadd-databases-tooa-custom-database-collection-target"></a>tooadd 資料庫 tooa 自訂資料庫收集目標
tooadd 資料庫 tooa 特定自訂集合使用 hello [**新增 AzureSqlJobChildTarget** ](/powershell/module/elasticdatabasejobs/add-azuresqljobchildtarget) cmdlet。

    $databaseServerName = "{Database Server Name}"
    $databaseName = "{Database Name}"
    $customCollectionName = "{Custom Database Collection Name}"
    Add-AzureSqlJobChildTarget -CustomCollectionName $customCollectionName -DatabaseName $databaseName -ServerName $databaseServerName 

#### <a name="review-hello-databases-within-a-custom-database-collection-target"></a>檢閱 hello 資料庫內的自訂資料庫收集目標
使用 hello [ **Get AzureSqlJobTarget** ](/powershell/module/elasticdatabasejobs/new-azuresqljobtarget) cmdlet tooretrieve hello 子資料庫內的自訂資料庫收集目標。 

    $customCollectionName = "{Custom Database Collection Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    $childTargets = Get-AzureSqlJobTarget -ParentTargetId $target.TargetId
    Write-Output $childTargets

### <a name="create-a-job-tooexecute-a-script-across-a-custom-database-collection-target"></a>建立指令碼工作 tooexecute 跨自訂資料庫收集目標
使用 hello [**新增 AzureSqlJob** ](/powershell/module/elasticdatabasejobs/new-azuresqljob) cmdlet toocreate 作業會每天針對資料庫定義的自訂資料庫收集目標的群組。 彈性資料庫工作會展開成多個子工作，每個對應的 tooa 資料庫與 hello 自訂資料庫收集目標關聯，並確保 hello 指令碼執行的每個資料庫的 hello 作業。 同樣地，請務必指令碼是等冪 toobe 彈性 tooretries。

    $jobName = "{Job Name}"
    $scriptName = "{Script Name}"
    $customCollectionName = "{Custom Collection Name}"
    $credentialName = "{Credential Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    $job = New-AzureSqlJob -JobName $jobName -CredentialName $credentialName -ContentName $scriptName -TargetId $target.TargetId
    Write-Output $job

## <a name="data-collection-across-databases"></a>跨資料庫的資料集合
您可以使用作業 tooexecute 查詢整個群組的資料庫，並傳送 hello 結果 tooa 特定資料表。 hello 資料表可以查詢之後每個資料庫的 hello 事實 toosee hello 查詢的結果。 這樣非同步方法 tooexecute 查詢跨多個資料庫。 嘗試失敗時自動經由重試來處理。

如果它尚未存在，就會自動建立 hello 指定的目的地資料表。 hello 新的資料表符合傳回的結果集的 hello hello 結構描述。 如果指令碼傳回多個結果集，彈性資料庫工作才會傳送 hello 第一個 toohello 目的地資料表。

hello 下列 PowerShell 指令碼執行指令碼，並會將其結果收集到指定的資料表。 此指令碼假設已建立一個會輸出單一結果集的 T-SQL 指令碼，也假設已建立自訂資料庫集合目標。

此指令碼使用 hello [ **Get AzureSqlJobTarget** ](/powershell/module/elasticdatabasejobs/new-azuresqljobtarget) cmdlet。 設定指令碼、 認證和執行目標的 hello 參數：

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

### <a name="toocreate-and-start-a-job-for-data-collection-scenarios"></a>toocreate 與開始的工作資料收集案例。
此指令碼使用 hello [**開始 AzureSqlJobExecution** ](/powershell/module/elasticdatabasejobs/start-azuresqljobexecution) cmdlet。

    $job = New-AzureSqlJob -JobName $jobName 
    -CredentialName $executionCredentialName 
    -ContentName $scriptName 
    -ResultSetDestinationServerName $destinationServerName 
    -ResultSetDestinationDatabaseName $destinationDatabaseName 
    -ResultSetDestinationSchemaName $destinationSchemaName 
    -ResultSetDestinationTableName $destinationTableName 
    -ResultSetDestinationCredentialName $destinationCredentialName 
    -TargetId $target.TargetId
    Write-Output $job
    $jobExecution = Start-AzureSqlJobExecution -JobName $jobName
    Write-Output $jobExecution

## <a name="tooschedule-a-job-execution-trigger"></a>tooschedule 工作執行觸發程序
hello 下列 PowerShell 指令碼可以使用的 toocreate 週期性的排程。 這個指令碼使用分鐘間隔，但是 [**New-AzureSqlJobSchedule**](/powershell/module/elasticdatabasejobs/new-azuresqljobschedule) 也支援 -DayInterval、-HourInterval、-MonthInterval 和 -WeekInterval 參數。 您可以藉由傳遞 -OneTime，建立僅執行一次的排程。

建立新的排程：

    $scheduleName = "Every one minute"
    $minuteInterval = 1
    $startTime = (Get-Date).ToUniversalTime()
    $schedule = New-AzureSqlJobSchedule 
    -MinuteInterval $minuteInterval 
    -ScheduleName $scheduleName 
    -StartTime $startTime 
    Write-Output $schedule

### <a name="tootrigger-a-job-executed-on-a-time-schedule"></a>tootrigger 的時間排程執行的工作
工作觸發程序可以定義的 toohave 作業執行相應 tooa 時間排程。 hello 下列 PowerShell 指令碼可以使用的 toocreate 工作觸發程序。

使用[新增 AzureSqlJobTrigger](/powershell/module/elasticdatabasejobs/new-azuresqljobtrigger)組 hello 遵循變數 toocorrespond toohello 所需的作業和排程：

    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    $jobTrigger = New-AzureSqlJobTrigger
    -ScheduleName $scheduleName
    -JobName $jobName
    Write-Output $jobTrigger

### <a name="tooremove-a-scheduled-association-toostop-job-from-executing-on-schedule"></a>tooremove 排程的關聯 toostop 作業依排程執行
可以移除 toodiscontinue 再度工作執行的工作觸發程序，hello 工作觸發程序。 移除工作觸發程序 toostop 工作正在執行使用 hello 相應 tooa 排程[**移除 AzureSqlJobTrigger cmdlet**](/powershell/module/elasticdatabasejobs/remove-azuresqljobtrigger)。

    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    Remove-AzureSqlJobTrigger 
    -ScheduleName $scheduleName 
    -JobName $jobName

### <a name="retrieve-job-triggers-bound-tooa-time-schedule"></a>擷取工作觸發程序繫結的 tooa 次的排程
hello 下列 PowerShell 指令碼可以使用的 tooobtain 和顯示 hello 工作觸發程序的已註冊的 tooa 特定時間排程。

    $scheduleName = "{Schedule Name}"
    $jobTriggers = Get-AzureSqlJobTrigger -ScheduleName $scheduleName
    Write-Output $jobTriggers

### <a name="tooretrieve-job-triggers-bound-tooa-job"></a>tooretrieve 工作觸發程序繫結的 tooa 工作
使用[Get AzureSqlJobTrigger](/powershell/module/elasticdatabasejobs/get-azuresqljobtrigger) tooobtain 並顯示包含已註冊的工作的排程。

    $jobName = "{Job Name}"
    $jobTriggers = Get-AzureSqlJobTrigger -JobName $jobName
    Write-Output $jobTriggers

## <a name="toocreate-a-data-tier-application-dacpac-for-execution-across-databases"></a>toocreate 執行跨資料庫的資料層應用程式 (DACPAC)
toocreate DACPAC，請參閱[資料層應用程式](https://msdn.microsoft.com/library/ee210546.aspx)。 toodeploy DACPAC 中，使用 hello[新增 AzureSqlJobContent cmdlet](/powershell/module/elasticdatabasejobs/new-azuresqljobcontent)。 hello DACPAC 必須是可存取 toohello 服務。 它會建議 tooupload 建立的 DACPAC tooAzure 儲存體，並建立[共用存取簽章](../storage/common/storage-dotnet-shared-access-signature-part-1.md)hello DACPAC。

    $dacpacUri = "{Uri}"
    $dacpacName = "{Dacpac Name}"
    $dacpac = New-AzureSqlJobContent -DacpacUri $dacpacUri -ContentName $dacpacName 
    Write-Output $dacpac

### <a name="tooupdate-a-data-tier-application-dacpac-for-execution-across-databases"></a>tooupdate 執行跨資料庫的資料層應用程式 (DACPAC)
彈性資料庫工作中註冊的現有 Dacpac 可以更新的 toopoint toonew Uri。 使用 hello [**組 AzureSqlJobContentDefinition cmdlet** ](/powershell/module/elasticdatabasejobs/set-azuresqljobcontentdefinition) tooupdate hello DACPAC URI 上的現有已註冊的 DACPAC:

    $dacpacName = "{Dacpac Name}"
    $newDacpacUri = "{Uri}"
    $updatedDacpac = Set-AzureSqlJobDacpacDefinition -ContentName $dacpacName -DacpacUri $newDacpacUri
    Write-Output $updatedDacpac

## <a name="toocreate-a-job-tooapply-a-data-tier-application-dacpac-across-databases"></a>toocreate 作業 tooapply 跨資料庫的資料層應用程式 (DACPAC)
DACPAC 彈性資料庫工作內建立之後，可以建立工作 tooapply hello DACPAC 跨資料庫的群組。 下列 PowerShell 指令碼的 hello 可在自訂集合的資料庫之間使用的 toocreate DACPAC 作業：

    $jobName = "{Job Name}"
    $dacpacName = "{Dacpac Name}"
    $customCollectionName = "{Custom Collection Name}"
    $credentialName = "{Credential Name}"
    $target = Get-AzureSqlJobTarget 
    -CustomCollectionName $customCollectionName
    $job = New-AzureSqlJob 
    -JobName $jobName 
    -CredentialName $credentialName 
    -ContentName $dacpacName -TargetId $target.TargetId
    Write-Output $job 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-jobs-powershell/cmd-prompt.png
[2]: ./media/sql-database-elastic-jobs-powershell/portal.png
<!--anchors-->
