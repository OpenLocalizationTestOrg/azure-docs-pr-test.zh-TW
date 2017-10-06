---
title: "事件檔案的程式碼的 SQL Database aaaXEvent |Microsoft 文件"
description: "PowerShell 和 TRANSACT-SQL 提供兩階段的程式碼範例示範在 Azure SQL Database 的擴充事件中的 hello 事件檔案目標。 此案例必須要有 Azure 儲存體。"
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
ms.openlocfilehash: 4457bd3250f4644b54da2f7daddb9da12070e93a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="event-file-target-code-for-extended-events-in-sql-database"></a>SQL Database 中擴充事件的事件檔案目標程式碼

[!INCLUDE [sql-database-xevents-selectors-1-include](../../includes/sql-database-xevents-selectors-1-include.md)]

您想完整程式碼範例的擴充事件的穩固地 toocapture 和報告資訊。

在 Microsoft SQL Server，hello[事件檔案目標](http://msdn.microsoft.com/library/ff878115.aspx)是使用的 toostore 事件輸出到本機硬碟檔案。 但是這類檔案無法使用 tooAzure SQL 資料庫。 相反地，我們會使用 hello Azure 儲存體服務 toosupport hello 事件檔案目標。

本主題示範一個兩階段的程式碼範例：

* PowerShell toocreate hello 雲端中的 Azure 儲存體容器。
* Transact-SQL：
  
  * tooassign hello Azure 儲存體容器 tooan 事件檔案目標。
  * toocreate 並開始 hello 事件工作階段，依此類推。

## <a name="prerequisites"></a>必要條件

* Azure 帳戶和訂用帳戶。 您可以註冊 [免費試用](https://azure.microsoft.com/pricing/free-trial/)。
* 您可以在當中建立資料表的任何資料庫。
  
  * 您可以選擇性快速[建立 **AdventureWorksLT** 示範資料庫](sql-database-get-started.md)。
* SQL Server Management Studio (ssms.exe)，最好是最新的每月更新版本。 
  您可以下載從 hello 最新 ssms.exe:
  
  * 名稱為 [下載 SQL Server Management Studio](http://msdn.microsoft.com/library/mt238290.aspx)的主題。
  * [直接連結 toohello 下載。](http://go.microsoft.com/fwlink/?linkid=616025)
* 您必須擁有 hello [Azure PowerShell 模組](http://go.microsoft.com/?linkid=9811175)安裝。
  
  * 提供命令，例如-hello 模組**新增 AzureStorageAccount**。

## <a name="phase-1-powershell-code-for-azure-storage-container"></a>第 1 階段：Azure 儲存體容器的 PowerShell 程式碼

此 PowerShell 是 hello 兩階段的程式碼範例的第 1 階段。

hello 指令碼會啟動命令 tooclean 與先前可能執行，並 rerunnable 之後。

1. Hello PowerShell 指令碼貼到 Notepad.exe，例如簡單的文字編輯器，並將 hello 指令碼儲存為 hello 副檔名的檔案**.ps1**。
2. 以系統管理員身分啟動 PowerShell ISE。
3. 在 hello 提示字元中，輸入<br/>`Set-ExecutionPolicy -ExecutionPolicy Unrestricted -Scope CurrentUser`<br/>然後按 Enter 鍵。
4. 在 PowerShell ISE 中開啟您的 **.ps1** 檔案。 執行 hello 指令碼。
5. hello 指令碼第一次啟動新的視窗中登入 tooAzure。
   
   * 如果您重新執行 hello 指令碼，而不會中斷您的工作階段，您可以 hello 方便選擇標記為註解 hello **Add-azureaccount**命令。

![PowerShell ISE 中，使用 Azure 模組安裝，準備好 toorun 指令碼。][30_powershell_ise]


### <a name="powershell-code"></a>PowerShell 程式碼

```powershell
## TODO: Before running, find all 'TODO' and make each edit!!

#--------------- 1 -----------------------


# You can comment out or skip this Add-AzureAccount
# command after hello first run.
# Current PowerShell environment retains hello successful outcome.

'Expect a pop-up window in which you log in tooAzure.'


Add-AzureAccount

#-------------- 2 ------------------------


'
TODO: Edit hello values assigned toothese variables, especially hello first few!
'

# Ensure hello current date is between
# hello Expiry and Start time values that you edit here.

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


# hello ending display lists your Azure subscriptions.
# One should match hello $subscriptionName value you assigned
#   earlier in this PowerShell script. 

'Choose an existing subscription for hello current PowerShell environment.'


Select-AzureSubscription -SubscriptionName $subscriptionName


#-------------- 4 ------------------------


'
Clean up hello old Azure Storage Account after any previous run, 
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
Get hello primary access key for your storage account.
'


$primaryAccessKey_ForStorageAccount = `
    (Get-AzureStorageKey `
        -StorageAccountName $storageAccountName).Primary

"`$primaryAccessKey_ForStorageAccount = $primaryAccessKey_ForStorageAccount"

'Azure Storage Account cmdlet completed.
Remainder of PowerShell .ps1 script continues.
'

#--------------- 6 -----------------------


# hello context will be needed toocreate a container within hello storage account.

'Create a context object from hello storage account and its primary access key.
'

$context = New-AzureStorageContext `
    -StorageAccountName $storageAccountName `
    -StorageAccountKey  $primaryAccessKey_ForStorageAccount


'Create a container within hello storage account.
'


$containerObjectInStorageAccount = New-AzureStorageContainer `
    -Name    $containerName `
    -Context $context


'Create a security policy toobe applied toohello SAS token.
'

New-AzureStorageContainerStoredAccessPolicy `
    -Container  $containerName `
    -Context    $context `
    -Policy     $policySasToken `
    -Permission $policySasPermission `
    -ExpiryTime $policySasExpiryTime `
    -StartTime  $policySasStartTime 

'
Generate a SAS token for hello container.
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


'Display hello values that YOU must edit into hello Transact-SQL script next!:
'

"storageAccountName: $storageAccountName"
"containerName:      $containerName"
"sasTokenWithPolicy: $sasTokenWithPolicy"

'
REMINDER: sasTokenWithPolicy here might start with "?" character, which you must exclude from Transact-SQL.
'

'
(Later, return here toodelete your Azure Storage account. See hello preceding - Remove-AzureStorageAccount -StorageAccountName $storageAccountName)'

'
Now shift toohello Transact-SQL portion of hello two-part code sample!'

# EOFile
```


請注意 hello hello PowerShell 指令碼會列印結束時的幾個具名的值。 您必須編輯這些值到 hello 遵循第 2 個階段的 TRANSACT-SQL 指令碼。

## <a name="phase-2-transact-sql-code-that-uses-azure-storage-container"></a>第 2 階段：使用 Azure 儲存體容器的 Transact-SQL 程式碼

* 此程式碼範例的第 1 階段，在您執行 PowerShell 指令碼 toocreate Azure 儲存體容器。
* 接下來在階段 2 中，hello 下列 TRANSACT-SQL 指令碼必須使用 hello 容器。

hello 指令碼會啟動命令 tooclean 與先前可能執行，並 rerunnable 之後。

hello PowerShell 指令碼會列印幾個具名的值，結束時間。 您必須編輯 hello Transact SQL 指令碼 toouse 這些值。 尋找**TODO** hello Transact SQL 指令碼 toolocate hello 中編輯端點。

1. 開啟 SQL Server Management Studio (ssms.exe)。
2. 連接 tooyour Azure SQL Database 的資料庫。
3. 按一下 tooopen 新的查詢 窗格。
4. 貼上下列 TRANSACT-SQL 指令碼在 hello 查詢 窗格中的 hello。
5. 尋找每個**TODO**在 hello 指令碼並進行 hello 適當的編輯。
6. 儲存，然後再執行 hello 指令碼。


> [!WARNING]
> hello hello 上述 PowerShell 指令碼所產生的 SAS 金鑰值可能會開始使用 '？ '（問號）。 當您使用下列 T-SQL 指令碼的 hello hello SAS 金鑰時，您必須*移除 hello 前置字元 '？ '*. 否則您的動作可能會遭到安全性封鎖。


### <a name="transact-sql-code"></a>Transact-SQL 程式碼

```sql
---- TODO: First, run hello PowerShell portion of this two-part code sample.
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
        -- TODO: Assign AzureStorageAccount name, and hello associated Container name.
        WHERE name = 'https://gmstorageaccountxevent.blob.core.windows.net/gmcontainerxevent')
BEGIN
    DROP DATABASE SCOPED CREDENTIAL
        -- TODO: Assign AzureStorageAccount name, and hello associated Container name.
        [https://gmstorageaccountxevent.blob.core.windows.net/gmcontainerxevent] ;
END
GO


CREATE
    DATABASE SCOPED
    CREDENTIAL
        -- use '.blob.',   and not '.queue.' or '.table.' etc.
        -- TODO: Assign AzureStorageAccount name, and hello associated Container name.
        [https://gmstorageaccountxevent.blob.core.windows.net/gmcontainerxevent]
    WITH
        IDENTITY = 'SHARED ACCESS SIGNATURE',  -- "SAS" token.
        -- TODO: Paste in hello long SasToken string here for Secret, but exclude any leading '?'.
        SECRET = 'sv=2014-02-14&sr=c&si=gmpolicysastoken&sig=EjAqjo6Nu5xMLEZEkMkLbeF7TD9v1J8DNB2t8gOKTts%3D'
    ;
GO


------  Step 3.  Create (define) an event session.  --------
------  hello event session has an event with an action,
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
            -- TODO: Assign AzureStorageAccount name, and hello associated Container name.
            -- Also, tweak hello .xel file name at end, if you like.
            SET filename =
                'https://gmstorageaccountxevent.blob.core.windows.net/gmcontainerxevent/anyfilenamexel242b.xel'
            )
    WITH
        (MAX_MEMORY = 10 MB,
        MAX_DISPATCH_LATENCY = 3 SECONDS)
    ;
GO


------  Step 4.  Start hello event session.  ----------------
------  Issue hello SQL Update statements that will be traced.
------  Then stop hello session.

------  Note: If hello target fails tooattach,
------  hello session must be stopped and restarted.

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


-------------- Step 5.  Select hello results. ----------

SELECT
        *, 'CLICK_NEXT_CELL_TO_BROWSE_ITS_RESULTS!' as [CLICK_NEXT_CELL_TO_BROWSE_ITS_RESULTS],
        CAST(event_data AS XML) AS [event_data_XML]  -- TODO: In ssms.exe results grid, double-click this cell!
    FROM
        sys.fn_xe_file_target_read_file
            (
                -- TODO: Fill in Storage Account name, and hello associated Container name.
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
    -- TODO: Assign AzureStorageAccount name, and hello associated Container name.
    [https://gmstorageaccountxevent.blob.core.windows.net/gmcontainerxevent]
    ;
GO

DROP TABLE gmTabEmployee;
GO

PRINT 'Use PowerShell Remove-AzureStorageAccount toodelete your Azure Storage account!';
GO
```


如果 hello 目標失敗 tooattach，當您執行時，您必須停止並重新啟動 hello 事件工作階段：

```sql
ALTER EVENT SESSION ... STATE = STOP;
GO
ALTER EVENT SESSION ... STATE = START;
GO
```


## <a name="output"></a>輸出

Hello TRANSACT-SQL 指令碼完成時，按一下資料格底下 hello **event_data_XML**資料行標頭。 此時會顯示一個 **<event>** 元素，此元素會顯示一個 UPDATE 陳述式。

以下是測試期間所產生的一個 **<event>** 元素：


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


hello 下列系統函數 tooread hello event_file 上述 Transact SQL 指令碼使用 hello:

* [sys.fn_xe_file_target_read_file (Transact-SQL)](http://msdn.microsoft.com/library/cc280743.aspx)

擴充事件的資料進行 hello 檢視進階選項的說明位於：

* [進一步檢視擴充事件的目標資料](http://msdn.microsoft.com/library/mt752502.aspx)


## <a name="converting-hello-code-sample-toorun-on-sql-server"></a>轉換 SQL Server 上的 hello 程式碼範例 toorun

假設您想 toorun hello TRANSACT-SQL 範例之前在 Microsoft SQL Server。

* 為了簡單起見，您會想 hello Azure 儲存體容器 toocompletely 取代使用簡易檔案這類**C:\myeventdata.xel**。 hello 檔案會被寫入 toohello 本機電腦的硬碟機 hello 主控 SQL Server。
* 針對 **CREATE MASTER KEY** 和**CREATE CREDENTIAL**，您不需要任何類型的 Transact-SQL 陳述式。
* 在 hello **CREATE EVENT SESSION**陳述式，請在其**加入目標**子句，您必須取代 hello 分派的 Http 值所做過**filename =**具有完整路徑字串 like **C:\myfile.xel**。
  
  * 不需要牽涉到任何 Azure 儲存體帳戶。

## <a name="more-information"></a>詳細資訊

如需帳戶與 hello Azure 儲存體服務中的容器的詳細資訊，請參閱：

* [如何 toouse 與.NET 的 Blob 儲存體](../storage/blobs/storage-dotnet-how-to-use-blobs.md)
* [命名和參考容器、Blob 及中繼資料](http://msdn.microsoft.com/library/azure/dd135715.aspx)
* [使用 hello 根容器](http://msdn.microsoft.com/library/azure/ee395424.aspx)
* [第 1 課：在 Azure 容器上建立預存的存取原則和共用存取簽章](http://msdn.microsoft.com/library/dn466430.aspx)
  * [第 2 課：使用共用存取簽章建立 SQL Server 認證](http://msdn.microsoft.com/library/dn466435.aspx)

<!--
Image references.
-->

[30_powershell_ise]: ./media/sql-database-xevent-code-event-file/event-file-powershell-ise-b30.png

