---
title: "SQL Database 的 XEvent 事件檔案程式碼 | Microsoft Docs"
description: "提供 PowerShell 和 Transact-SQL 的兩階段程式碼範例，示範 Azure SQL Database 上擴充事件中的事件檔案目標。 此案例必須要有 Azure 儲存體。"
services: sql-database
documentationcenter: 
author: MightyPen
manager: jhubbard
editor: 
tags: 
ms.assetid: bbb10ecc-739f-4159-b844-12b4be161231
ms.service: sql-database
ms.custom: monitor & tune
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/06/2017
ms.author: genemi
ms.openlocfilehash: e8c7a9af11ac4c22be00426337ab7c8b8ff0860f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="event-file-target-code-for-extended-events-in-sql-database"></a><span data-ttu-id="9ed27-104">SQL Database 中擴充事件的事件檔案目標程式碼</span><span class="sxs-lookup"><span data-stu-id="9ed27-104">Event File target code for extended events in SQL Database</span></span>

[!INCLUDE [sql-database-xevents-selectors-1-include](../../includes/sql-database-xevents-selectors-1-include.md)]

<span data-ttu-id="9ed27-105">您想要完整的程式碼範例以穩健方式擷取和報告擴充事件的資訊。</span><span class="sxs-lookup"><span data-stu-id="9ed27-105">You want a complete code sample for a robust way to capture and report information for an extended event.</span></span>

<span data-ttu-id="9ed27-106">在 Microsoft SQL Server 中， [事件檔案目標](http://msdn.microsoft.com/library/ff878115.aspx) 是用來將事件輸出儲存到本機硬碟機檔案中。</span><span class="sxs-lookup"><span data-stu-id="9ed27-106">In Microsoft SQL Server, the [Event File target](http://msdn.microsoft.com/library/ff878115.aspx) is used to store event outputs into a local hard drive file.</span></span> <span data-ttu-id="9ed27-107">但是這類檔案並不適用於 Azure SQL Database。</span><span class="sxs-lookup"><span data-stu-id="9ed27-107">But such files are not available to Azure SQL Database.</span></span> <span data-ttu-id="9ed27-108">我們改為使用 Azure 儲存體服務來支援事件檔案目標。</span><span class="sxs-lookup"><span data-stu-id="9ed27-108">Instead we use the Azure Storage service to support the Event File target.</span></span>

<span data-ttu-id="9ed27-109">本主題示範一個兩階段的程式碼範例：</span><span class="sxs-lookup"><span data-stu-id="9ed27-109">This topic presents a two-phase code sample:</span></span>

* <span data-ttu-id="9ed27-110">使用 PowerShell 在雲端中建立 Azure 儲存體容器</span><span class="sxs-lookup"><span data-stu-id="9ed27-110">PowerShell, to create an Azure Storage container in the cloud.</span></span>
* <span data-ttu-id="9ed27-111">Transact-SQL：</span><span class="sxs-lookup"><span data-stu-id="9ed27-111">Transact-SQL:</span></span>
  
  * <span data-ttu-id="9ed27-112">將 Azure 儲存體容器指定為事件檔案目標。</span><span class="sxs-lookup"><span data-stu-id="9ed27-112">To assign the Azure Storage container to an Event File target.</span></span>
  * <span data-ttu-id="9ed27-113">建立和啟動事件工作階段等等。</span><span class="sxs-lookup"><span data-stu-id="9ed27-113">To create and start the event session, and so on.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9ed27-114">必要條件</span><span class="sxs-lookup"><span data-stu-id="9ed27-114">Prerequisites</span></span>

* <span data-ttu-id="9ed27-115">Azure 帳戶和訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="9ed27-115">An Azure account and subscription.</span></span> <span data-ttu-id="9ed27-116">您可以註冊 [免費試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="9ed27-116">You can sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="9ed27-117">您可以在當中建立資料表的任何資料庫。</span><span class="sxs-lookup"><span data-stu-id="9ed27-117">Any database you can create a table in.</span></span>
  
  * <span data-ttu-id="9ed27-118">您可以選擇性快速[建立 **AdventureWorksLT** 示範資料庫](sql-database-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="9ed27-118">Optionally you can [create an **AdventureWorksLT** demonstration database](sql-database-get-started.md) in minutes.</span></span>
* <span data-ttu-id="9ed27-119">SQL Server Management Studio (ssms.exe)，最好是最新的每月更新版本。</span><span class="sxs-lookup"><span data-stu-id="9ed27-119">SQL Server Management Studio (ssms.exe), ideally its latest monthly update version.</span></span> 
  <span data-ttu-id="9ed27-120">您可以從下列位置下載最新的 ssms.exe：</span><span class="sxs-lookup"><span data-stu-id="9ed27-120">You can download the latest ssms.exe from:</span></span>
  
  * <span data-ttu-id="9ed27-121">名稱為 [下載 SQL Server Management Studio](http://msdn.microsoft.com/library/mt238290.aspx)的主題。</span><span class="sxs-lookup"><span data-stu-id="9ed27-121">Topic titled [Download SQL Server Management Studio](http://msdn.microsoft.com/library/mt238290.aspx).</span></span>
  * [<span data-ttu-id="9ed27-122">下載的直接連結。</span><span class="sxs-lookup"><span data-stu-id="9ed27-122">A direct link to the download.</span></span>](http://go.microsoft.com/fwlink/?linkid=616025)
* <span data-ttu-id="9ed27-123">您必須安裝 [Azure PowerShell 模組](http://go.microsoft.com/?linkid=9811175) 。</span><span class="sxs-lookup"><span data-stu-id="9ed27-123">You must have the [Azure PowerShell modules](http://go.microsoft.com/?linkid=9811175) installed.</span></span>
  
  * <span data-ttu-id="9ed27-124">模組提供 **New-AzureStorageAccount**這類的命令。</span><span class="sxs-lookup"><span data-stu-id="9ed27-124">The modules provide commands such as - **New-AzureStorageAccount**.</span></span>

## <a name="phase-1-powershell-code-for-azure-storage-container"></a><span data-ttu-id="9ed27-125">第 1 階段：Azure 儲存體容器的 PowerShell 程式碼</span><span class="sxs-lookup"><span data-stu-id="9ed27-125">Phase 1: PowerShell code for Azure Storage container</span></span>

<span data-ttu-id="9ed27-126">這個 PowerShell 是兩階段程式碼範例的第 1 階段。</span><span class="sxs-lookup"><span data-stu-id="9ed27-126">This PowerShell is phase 1 of the two-phase code sample.</span></span>

<span data-ttu-id="9ed27-127">此指令碼是以可清除先前可能之執行結果的命令為開頭，並且可重複執行。</span><span class="sxs-lookup"><span data-stu-id="9ed27-127">The script starts with commands to clean up after a possible previous run, and is rerunnable.</span></span>

1. <span data-ttu-id="9ed27-128">將 PowerShell 指令碼貼到如 Notepad.exe 的簡單文字編輯器，並將指令碼儲存為有 **.ps1**副檔名的檔案。</span><span class="sxs-lookup"><span data-stu-id="9ed27-128">Paste the PowerShell script into a simple text editor such as Notepad.exe, and save the script as a file with the extension **.ps1**.</span></span>
2. <span data-ttu-id="9ed27-129">以系統管理員身分啟動 PowerShell ISE。</span><span class="sxs-lookup"><span data-stu-id="9ed27-129">Start PowerShell ISE as an Administrator.</span></span>
3. <span data-ttu-id="9ed27-130">在提示中輸入</span><span class="sxs-lookup"><span data-stu-id="9ed27-130">At the prompt, type</span></span><br/>`Set-ExecutionPolicy -ExecutionPolicy Unrestricted -Scope CurrentUser`<br/><span data-ttu-id="9ed27-131">然後按 Enter 鍵。</span><span class="sxs-lookup"><span data-stu-id="9ed27-131">and then press Enter.</span></span>
4. <span data-ttu-id="9ed27-132">在 PowerShell ISE 中開啟您的 **.ps1** 檔案。</span><span class="sxs-lookup"><span data-stu-id="9ed27-132">In PowerShell ISE, open your **.ps1** file.</span></span> <span data-ttu-id="9ed27-133">執行指令碼。</span><span class="sxs-lookup"><span data-stu-id="9ed27-133">Run the script.</span></span>
5. <span data-ttu-id="9ed27-134">指令碼會先啟動新的視窗讓您登入 Azure。</span><span class="sxs-lookup"><span data-stu-id="9ed27-134">The script first starts a new window in which you log in to Azure.</span></span>
   
   * <span data-ttu-id="9ed27-135">如果您重複執行指令碼而不中斷您的工作階段，可以很方便地選擇將 **Add-AzureAccount** 命令標記為註解。</span><span class="sxs-lookup"><span data-stu-id="9ed27-135">If you rerun the script without disrupting your session, you have the convenient option of commenting out the **Add-AzureAccount** command.</span></span>

![準備好 PowerShell ISE 和安裝的 Azure 模組，以便執行指令碼。][30_powershell_ise]


### <a name="powershell-code"></a><span data-ttu-id="9ed27-137">PowerShell 程式碼</span><span class="sxs-lookup"><span data-stu-id="9ed27-137">PowerShell code</span></span>

```powershell
## TODO: Before running, find all 'TODO' and make each edit!!

#--------------- 1 -----------------------


# You can comment out or skip this Add-AzureAccount
# command after the first run.
# Current PowerShell environment retains the successful outcome.

'Expect a pop-up window in which you log in to Azure.'


Add-AzureAccount

#-------------- 2 ------------------------


'
TODO: Edit the values assigned to these variables, especially the first few!
'

# Ensure the current date is between
# the Expiry and Start time values that you edit here.

$subscriptionName    = 'YOUR_SUBSCRIPTION_NAME'
$policySasExpiryTime = '2016-01-28T23:44:56Z'
$policySasStartTime  = '2015-08-01'


$storageAccountName     = 'gmstorageaccountxevent'
$storageAccountLocation = 'West US'
$contextName            = 'gmcontext'
$containerName          = 'gmcontainerxevent'
$policySasToken         = 'gmpolicysastoken'


# Leave this value alone, as 'rwl'.
$policySasPermission = 'rwl'

#--------------- 3 -----------------------


# The ending display lists your Azure subscriptions.
# One should match the $subscriptionName value you assigned
#   earlier in this PowerShell script. 

'Choose an existing subscription for the current PowerShell environment.'


Select-AzureSubscription -SubscriptionName $subscriptionName


#-------------- 4 ------------------------


'
Clean up the old Azure Storage Account after any previous run, 
before continuing this new run.'


If ($storageAccountName)
{
    Remove-AzureStorageAccount -StorageAccountName $storageAccountName
}

#--------------- 5 -----------------------

[System.DateTime]::Now.ToString()

'
Create a storage account. 
This might take several minutes, will beep when ready.
  ...PLEASE WAIT...'

New-AzureStorageAccount `
    -StorageAccountName $storageAccountName `
    -Location           $storageAccountLocation

[System.DateTime]::Now.ToString()

[System.Media.SystemSounds]::Beep.Play()


'
Get the primary access key for your storage account.
'


$primaryAccessKey_ForStorageAccount = `
    (Get-AzureStorageKey `
        -StorageAccountName $storageAccountName).Primary

"`$primaryAccessKey_ForStorageAccount = $primaryAccessKey_ForStorageAccount"

'Azure Storage Account cmdlet completed.
Remainder of PowerShell .ps1 script continues.
'

#--------------- 6 -----------------------


# The context will be needed to create a container within the storage account.

'Create a context object from the storage account and its primary access key.
'

$context = New-AzureStorageContext `
    -StorageAccountName $storageAccountName `
    -StorageAccountKey  $primaryAccessKey_ForStorageAccount


'Create a container within the storage account.
'


$containerObjectInStorageAccount = New-AzureStorageContainer `
    -Name    $containerName `
    -Context $context


'Create a security policy to be applied to the SAS token.
'

New-AzureStorageContainerStoredAccessPolicy `
    -Container  $containerName `
    -Context    $context `
    -Policy     $policySasToken `
    -Permission $policySasPermission `
    -ExpiryTime $policySasExpiryTime `
    -StartTime  $policySasStartTime 

'
Generate a SAS token for the container.
'
Try
{
    $sasTokenWithPolicy = New-AzureStorageContainerSASToken `
        -Name    $containerName `
        -Context $context `
        -Policy  $policySasToken
}
Catch 
{
    $Error[0].Exception.ToString()
}

#-------------- 7 ------------------------


'Display the values that YOU must edit into the Transact-SQL script next!:
'

"storageAccountName: $storageAccountName"
"containerName:      $containerName"
"sasTokenWithPolicy: $sasTokenWithPolicy"

'
REMINDER: sasTokenWithPolicy here might start with "?" character, which you must exclude from Transact-SQL.
'

'
(Later, return here to delete your Azure Storage account. See the preceding - Remove-AzureStorageAccount -StorageAccountName $storageAccountName)'

'
Now shift to the Transact-SQL portion of the two-part code sample!'

# EOFile
```


<span data-ttu-id="9ed27-138">記下 PowerShell 指令碼結束時列印出的幾個具名值。</span><span class="sxs-lookup"><span data-stu-id="9ed27-138">Take note of the few named values that the PowerShell script prints when it ends.</span></span> <span data-ttu-id="9ed27-139">您必須將這些值寫入第 2 階段的 Transact-SQL 指令碼。</span><span class="sxs-lookup"><span data-stu-id="9ed27-139">You must edit those values into the Transact-SQL script that follows as phase 2.</span></span>

## <a name="phase-2-transact-sql-code-that-uses-azure-storage-container"></a><span data-ttu-id="9ed27-140">第 2 階段：使用 Azure 儲存體容器的 Transact-SQL 程式碼</span><span class="sxs-lookup"><span data-stu-id="9ed27-140">Phase 2: Transact-SQL code that uses Azure Storage container</span></span>

* <span data-ttu-id="9ed27-141">在此程式碼範例的第 1 階段中，您執行了 PowerShell 指令碼來建立「Azure 儲存體」容器。</span><span class="sxs-lookup"><span data-stu-id="9ed27-141">In phase 1 of this code sample, you ran a PowerShell script to create an Azure Storage container.</span></span>
* <span data-ttu-id="9ed27-142">接下來在第 2 階段中，下列 Transact-SQL 指令碼必須使用該容器。</span><span class="sxs-lookup"><span data-stu-id="9ed27-142">Next in phase 2, the following Transact-SQL script must use the container.</span></span>

<span data-ttu-id="9ed27-143">此指令碼是以可清除先前可能之執行結果的命令為開頭，並且可重複執行。</span><span class="sxs-lookup"><span data-stu-id="9ed27-143">The script starts with commands to clean up after a possible previous run, and is rerunnable.</span></span>

<span data-ttu-id="9ed27-144">PowerShell 指令碼在結束時列印出幾個具名的值。</span><span class="sxs-lookup"><span data-stu-id="9ed27-144">The PowerShell script printed a few named values when it ended.</span></span> <span data-ttu-id="9ed27-145">您必須編輯 Transact-SQL 指令碼以使用這些值。</span><span class="sxs-lookup"><span data-stu-id="9ed27-145">You must edit the Transact-SQL script to use those values.</span></span> <span data-ttu-id="9ed27-146">在 Transact-SQL 指令碼中尋找 **TODO** 找出編輯點。</span><span class="sxs-lookup"><span data-stu-id="9ed27-146">Find **TODO** in the Transact-SQL script to locate the edit points.</span></span>

1. <span data-ttu-id="9ed27-147">開啟 SQL Server Management Studio (ssms.exe)。</span><span class="sxs-lookup"><span data-stu-id="9ed27-147">Open SQL Server Management Studio (ssms.exe).</span></span>
2. <span data-ttu-id="9ed27-148">連接到您的 Azure SQL Database 資料庫。</span><span class="sxs-lookup"><span data-stu-id="9ed27-148">Connect to your Azure SQL Database database.</span></span>
3. <span data-ttu-id="9ed27-149">按一下以開啟新的查詢窗格。</span><span class="sxs-lookup"><span data-stu-id="9ed27-149">Click to open a new query pane.</span></span>
4. <span data-ttu-id="9ed27-150">將下列 Transact-SQL 指令碼貼入查詢窗格。</span><span class="sxs-lookup"><span data-stu-id="9ed27-150">Paste the following Transact-SQL script into the query pane.</span></span>
5. <span data-ttu-id="9ed27-151">在指令碼中尋找每個 **TODO** 並進行適當的編輯。</span><span class="sxs-lookup"><span data-stu-id="9ed27-151">Find every **TODO** in the script and make the appropriate edits.</span></span>
6. <span data-ttu-id="9ed27-152">儲存並執行指令碼。</span><span class="sxs-lookup"><span data-stu-id="9ed27-152">Save, and then run the script.</span></span>


> [!WARNING]
> <span data-ttu-id="9ed27-153">上述 PowerShell 指令碼所產生的 SAS 金鑰值可能會以 '?' (問號) 開頭。</span><span class="sxs-lookup"><span data-stu-id="9ed27-153">The SAS key value generated by the preceding PowerShell script might begin with a '?' (question mark).</span></span> <span data-ttu-id="9ed27-154">當您在下列 T-SQL 指令碼中使用 SAS 金鑰時，您必須「移除前置 '?'」 。</span><span class="sxs-lookup"><span data-stu-id="9ed27-154">When you use the SAS key in the following T-SQL script, you must *remove the leading '?'*.</span></span> <span data-ttu-id="9ed27-155">否則您的動作可能會遭到安全性封鎖。</span><span class="sxs-lookup"><span data-stu-id="9ed27-155">Otherwise your efforts might be blocked by security.</span></span>


### <a name="transact-sql-code"></a><span data-ttu-id="9ed27-156">Transact-SQL 程式碼</span><span class="sxs-lookup"><span data-stu-id="9ed27-156">Transact-SQL code</span></span>

```sql
---- TODO: First, run the PowerShell portion of this two-part code sample.
---- TODO: Second, find every 'TODO' in this Transact-SQL file, and edit each.

---- Transact-SQL code for Event File target on Azure SQL Database.


SET NOCOUNT ON;
GO


----  Step 1.  Establish one little table, and  ---------
----  insert one row of data.


IF EXISTS
    (SELECT * FROM sys.objects
        WHERE type = 'U' and name = 'gmTabEmployee')
BEGIN
    DROP TABLE gmTabEmployee;
END
GO


CREATE TABLE gmTabEmployee
(
    EmployeeGuid         uniqueIdentifier   not null  default newid()  primary key,
    EmployeeId           int                not null  identity(1,1),
    EmployeeKudosCount   int                not null  default 0,
    EmployeeDescr        nvarchar(256)          null
);
GO


INSERT INTO gmTabEmployee ( EmployeeDescr )
    VALUES ( 'Jane Doe' );
GO


------  Step 2.  Create key, and  ------------
------  Create credential (your Azure Storage container must already exist).


IF NOT EXISTS
    (SELECT * FROM sys.symmetric_keys
        WHERE symmetric_key_id = 101)
BEGIN
    CREATE MASTER KEY ENCRYPTION BY PASSWORD = '0C34C960-6621-4682-A123-C7EA08E3FC46' -- Or any newid().
END
GO


IF EXISTS
    (SELECT * FROM sys.database_scoped_credentials
        -- TODO: Assign AzureStorageAccount name, and the associated Container name.
        WHERE name = 'https://gmstorageaccountxevent.blob.core.windows.net/gmcontainerxevent')
BEGIN
    DROP DATABASE SCOPED CREDENTIAL
        -- TODO: Assign AzureStorageAccount name, and the associated Container name.
        [https://gmstorageaccountxevent.blob.core.windows.net/gmcontainerxevent] ;
END
GO


CREATE
    DATABASE SCOPED
    CREDENTIAL
        -- use '.blob.',   and not '.queue.' or '.table.' etc.
        -- TODO: Assign AzureStorageAccount name, and the associated Container name.
        [https://gmstorageaccountxevent.blob.core.windows.net/gmcontainerxevent]
    WITH
        IDENTITY = 'SHARED ACCESS SIGNATURE',  -- "SAS" token.
        -- TODO: Paste in the long SasToken string here for Secret, but exclude any leading '?'.
        SECRET = 'sv=2014-02-14&sr=c&si=gmpolicysastoken&sig=EjAqjo6Nu5xMLEZEkMkLbeF7TD9v1J8DNB2t8gOKTts%3D'
    ;
GO


------  Step 3.  Create (define) an event session.  --------
------  The event session has an event with an action,
------  and a has a target.

IF EXISTS
    (SELECT * from sys.database_event_sessions
        WHERE name = 'gmeventsessionname240b')
BEGIN
    DROP
        EVENT SESSION
            gmeventsessionname240b
        ON DATABASE;
END
GO


CREATE
    EVENT SESSION
        gmeventsessionname240b
    ON DATABASE

    ADD EVENT
        sqlserver.sql_statement_starting
            (
            ACTION (sqlserver.sql_text)
            WHERE statement LIKE 'UPDATE gmTabEmployee%'
            )
    ADD TARGET
        package0.event_file
            (
            -- TODO: Assign AzureStorageAccount name, and the associated Container name.
            -- Also, tweak the .xel file name at end, if you like.
            SET filename =
                'https://gmstorageaccountxevent.blob.core.windows.net/gmcontainerxevent/anyfilenamexel242b.xel'
            )
    WITH
        (MAX_MEMORY = 10 MB,
        MAX_DISPATCH_LATENCY = 3 SECONDS)
    ;
GO


------  Step 4.  Start the event session.  ----------------
------  Issue the SQL Update statements that will be traced.
------  Then stop the session.

------  Note: If the target fails to attach,
------  the session must be stopped and restarted.

ALTER
    EVENT SESSION
        gmeventsessionname240b
    ON DATABASE
    STATE = START;
GO


SELECT 'BEFORE_Updates', EmployeeKudosCount, * FROM gmTabEmployee;

UPDATE gmTabEmployee
    SET EmployeeKudosCount = EmployeeKudosCount + 2
    WHERE EmployeeDescr = 'Jane Doe';

UPDATE gmTabEmployee
    SET EmployeeKudosCount = EmployeeKudosCount + 13
    WHERE EmployeeDescr = 'Jane Doe';

SELECT 'AFTER__Updates', EmployeeKudosCount, * FROM gmTabEmployee;
GO


ALTER
    EVENT SESSION
        gmeventsessionname240b
    ON DATABASE
    STATE = STOP;
GO


-------------- Step 5.  Select the results. ----------

SELECT
        *, 'CLICK_NEXT_CELL_TO_BROWSE_ITS_RESULTS!' as [CLICK_NEXT_CELL_TO_BROWSE_ITS_RESULTS],
        CAST(event_data AS XML) AS [event_data_XML]  -- TODO: In ssms.exe results grid, double-click this cell!
    FROM
        sys.fn_xe_file_target_read_file
            (
                -- TODO: Fill in Storage Account name, and the associated Container name.
                'https://gmstorageaccountxevent.blob.core.windows.net/gmcontainerxevent/anyfilenamexel242b',
                null, null, null
            );
GO


-------------- Step 6.  Clean up. ----------

DROP
    EVENT SESSION
        gmeventsessionname240b
    ON DATABASE;
GO

DROP DATABASE SCOPED CREDENTIAL
    -- TODO: Assign AzureStorageAccount name, and the associated Container name.
    [https://gmstorageaccountxevent.blob.core.windows.net/gmcontainerxevent]
    ;
GO

DROP TABLE gmTabEmployee;
GO

PRINT 'Use PowerShell Remove-AzureStorageAccount to delete your Azure Storage account!';
GO
```


<span data-ttu-id="9ed27-157">如果目標在執行時無法附加，您就必須停止事件工作階段並重新啟動：</span><span class="sxs-lookup"><span data-stu-id="9ed27-157">If the target fails to attach when you run, you must stop and restart the event session:</span></span>

```sql
ALTER EVENT SESSION ... STATE = STOP;
GO
ALTER EVENT SESSION ... STATE = START;
GO
```


## <a name="output"></a><span data-ttu-id="9ed27-158">輸出</span><span class="sxs-lookup"><span data-stu-id="9ed27-158">Output</span></span>

<span data-ttu-id="9ed27-159">Transact-SQL 指令碼完成時，按一下 **event_data_XML** 資料欄標題下的儲存格。</span><span class="sxs-lookup"><span data-stu-id="9ed27-159">When the Transact-SQL script completes, click a cell under the **event_data_XML** column header.</span></span> <span data-ttu-id="9ed27-160">此時會顯示一個 **<event>** 元素，此元素會顯示一個 UPDATE 陳述式。</span><span class="sxs-lookup"><span data-stu-id="9ed27-160">One **<event>** element is displayed which shows one UPDATE statement.</span></span>

<span data-ttu-id="9ed27-161">以下是測試期間所產生的一個 **<event>** 元素：</span><span class="sxs-lookup"><span data-stu-id="9ed27-161">Here is one **<event>** element that was generated during testing:</span></span>


```xml
<event name="sql_statement_starting" package="sqlserver" timestamp="2015-09-22T19:18:45.420Z">
  <data name="state">
    <value>0</value>
    <text>Normal</text>
  </data>
  <data name="line_number">
    <value>5</value>
  </data>
  <data name="offset">
    <value>148</value>
  </data>
  <data name="offset_end">
    <value>368</value>
  </data>
  <data name="statement">
    <value>UPDATE gmTabEmployee
    SET EmployeeKudosCount = EmployeeKudosCount + 2
    WHERE EmployeeDescr = 'Jane Doe'</value>
  </data>
  <action name="sql_text" package="sqlserver">
    <value>

SELECT 'BEFORE_Updates', EmployeeKudosCount, * FROM gmTabEmployee;

UPDATE gmTabEmployee
    SET EmployeeKudosCount = EmployeeKudosCount + 2
    WHERE EmployeeDescr = 'Jane Doe';

UPDATE gmTabEmployee
    SET EmployeeKudosCount = EmployeeKudosCount + 13
    WHERE EmployeeDescr = 'Jane Doe';

SELECT 'AFTER__Updates', EmployeeKudosCount, * FROM gmTabEmployee;
</value>
  </action>
</event>
```


<span data-ttu-id="9ed27-162">上述 TRANSACT-SQL 指令碼使用下列系統函數讀取 event_file：</span><span class="sxs-lookup"><span data-stu-id="9ed27-162">The preceding Transact-SQL script used the following system function to read the event_file:</span></span>

* [<span data-ttu-id="9ed27-163">sys.fn_xe_file_target_read_file (Transact-SQL)</span><span class="sxs-lookup"><span data-stu-id="9ed27-163">sys.fn_xe_file_target_read_file (Transact-SQL)</span></span>](http://msdn.microsoft.com/library/cc280743.aspx)

<span data-ttu-id="9ed27-164">您可以在下列文章中取得進階選項的說明，這些選項可用來檢視擴充事件的資料：</span><span class="sxs-lookup"><span data-stu-id="9ed27-164">An explanation of advanced options for the viewing of data from extended events is available at:</span></span>

* [<span data-ttu-id="9ed27-165">進一步檢視擴充事件的目標資料</span><span class="sxs-lookup"><span data-stu-id="9ed27-165">Advanced Viewing of Target Data from Extended Events</span></span>](http://msdn.microsoft.com/library/mt752502.aspx)


## <a name="converting-the-code-sample-to-run-on-sql-server"></a><span data-ttu-id="9ed27-166">轉換程式碼範例在 SQL Server 上執行</span><span class="sxs-lookup"><span data-stu-id="9ed27-166">Converting the code sample to run on SQL Server</span></span>

<span data-ttu-id="9ed27-167">假設您想要在 Microsoft SQL Server 上執行上述的 Transact-SQL 範例。</span><span class="sxs-lookup"><span data-stu-id="9ed27-167">Suppose you wanted to run the preceding Transact-SQL sample on Microsoft SQL Server.</span></span>

* <span data-ttu-id="9ed27-168">為了簡單起見，您可以用簡單的檔案 (例如 **C:\myeventdata.xel**) 來取代「Azure 儲存體」容器的使用。</span><span class="sxs-lookup"><span data-stu-id="9ed27-168">For simplicity, you would want to completely replace use of the Azure Storage container with a simple file such as **C:\myeventdata.xel**.</span></span> <span data-ttu-id="9ed27-169">檔案會寫入裝載 SQL Server 之電腦的本機硬碟。</span><span class="sxs-lookup"><span data-stu-id="9ed27-169">The file would be written to the local hard drive of the computer that hosts SQL Server.</span></span>
* <span data-ttu-id="9ed27-170">針對 **CREATE MASTER KEY** 和**CREATE CREDENTIAL**，您不需要任何類型的 Transact-SQL 陳述式。</span><span class="sxs-lookup"><span data-stu-id="9ed27-170">You would not need any kind of Transact-SQL statements for **CREATE MASTER KEY** and **CREATE CREDENTIAL**.</span></span>
* <span data-ttu-id="9ed27-171">在 **CREATE EVENT SESSION** 陳述式的 **ADD TARGET** 子句中，您要將對 **filename=** 指派的 Http 值取代為完整路徑字串 (例如 **C:\myfile.xel**)。</span><span class="sxs-lookup"><span data-stu-id="9ed27-171">In the **CREATE EVENT SESSION** statement, in its **ADD TARGET** clause, you would replace the Http value assigned made to **filename=** with a full path string like **C:\myfile.xel**.</span></span>
  
  * <span data-ttu-id="9ed27-172">不需要牽涉到任何 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="9ed27-172">No Azure Storage account need be involved.</span></span>

## <a name="more-information"></a><span data-ttu-id="9ed27-173">詳細資訊</span><span class="sxs-lookup"><span data-stu-id="9ed27-173">More information</span></span>

<span data-ttu-id="9ed27-174">如需 Azure 儲存體服務中帳戶和容器的詳細資訊，請參閱：</span><span class="sxs-lookup"><span data-stu-id="9ed27-174">For more info about accounts and containers in the Azure Storage service, see:</span></span>

* [<span data-ttu-id="9ed27-175">如何使用 .NET 的 Blob 儲存體</span><span class="sxs-lookup"><span data-stu-id="9ed27-175">How to use Blob storage from .NET</span></span>](../storage/blobs/storage-dotnet-how-to-use-blobs.md)
* [<span data-ttu-id="9ed27-176">命名和參考容器、Blob 及中繼資料</span><span class="sxs-lookup"><span data-stu-id="9ed27-176">Naming and Referencing Containers, Blobs, and Metadata</span></span>](http://msdn.microsoft.com/library/azure/dd135715.aspx)
* [<span data-ttu-id="9ed27-177">使用根容器</span><span class="sxs-lookup"><span data-stu-id="9ed27-177">Working with the Root Container</span></span>](http://msdn.microsoft.com/library/azure/ee395424.aspx)
* [<span data-ttu-id="9ed27-178">第 1 課：在 Azure 容器上建立預存的存取原則和共用存取簽章</span><span class="sxs-lookup"><span data-stu-id="9ed27-178">Lesson 1: Create a stored access policy and a shared access signature on an Azure container</span></span>](http://msdn.microsoft.com/library/dn466430.aspx)
  * [<span data-ttu-id="9ed27-179">第 2 課：使用共用存取簽章建立 SQL Server 認證</span><span class="sxs-lookup"><span data-stu-id="9ed27-179">Lesson 2: Create a SQL Server credential using a shared access signature</span></span>](http://msdn.microsoft.com/library/dn466435.aspx)

<!--
Image references.
-->

[30_powershell_ise]: ./media/sql-database-xevent-code-event-file/event-file-powershell-ise-b30.png

