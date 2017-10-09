---
title: "aaaXEvent 信號緩衝區對 SQL 資料庫的程式碼 |Microsoft 文件"
description: "提供使用 Azure SQL Database 中的 hello 信號緩衝區目標來進行簡單，且快速的 TRANSACT-SQL 程式碼範例。"
services: sql-database
documentationcenter: 
author: MightyPen
manager: jhubbard
editor: 
tags: 
ms.assetid: 2510fb3f-c8f2-437a-8f49-9d5f6c96e75b
ms.service: sql-database
ms.custom: monitor & tune
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/03/2017
ms.author: genemi
ms.openlocfilehash: 21df748d9999d6837d2b5bbe4a3f47fb351b4633
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="ring-buffer-target-code-for-extended-events-in-sql-database"></a><span data-ttu-id="ee329-103">SQL Database 中擴充事件的信號緩衝區目標程式碼</span><span class="sxs-lookup"><span data-stu-id="ee329-103">Ring Buffer target code for extended events in SQL Database</span></span>

[!INCLUDE [sql-database-xevents-selectors-1-include](../../includes/sql-database-xevents-selectors-1-include.md)]

<span data-ttu-id="ee329-104">您想完整程式碼範例 hello 最簡單快速的方式 toocapture 和報表資訊的擴充的事件在測試期間。</span><span class="sxs-lookup"><span data-stu-id="ee329-104">You want a complete code sample for hello easiest quick way toocapture and report information for an extended event during a test.</span></span> <span data-ttu-id="ee329-105">hello 擴充的事件資料的最簡單的目標為 hello[信號緩衝區目標](http://msdn.microsoft.com/library/ff878182.aspx)。</span><span class="sxs-lookup"><span data-stu-id="ee329-105">hello easiest target for extended event data is hello [Ring Buffer target](http://msdn.microsoft.com/library/ff878182.aspx).</span></span>

<span data-ttu-id="ee329-106">本主題提供會執行下列動作的 Transact-SQL 程式碼範例：</span><span class="sxs-lookup"><span data-stu-id="ee329-106">This topic presents a Transact-SQL code sample that:</span></span>

1. <span data-ttu-id="ee329-107">建立包含的資料表與資料 toodemonstrate。</span><span class="sxs-lookup"><span data-stu-id="ee329-107">Creates a table with data toodemonstrate with.</span></span>
2. <span data-ttu-id="ee329-108">建立現有擴充事件的工作階段，名稱為 **sqlserver.sql_statement_starting**。</span><span class="sxs-lookup"><span data-stu-id="ee329-108">Creates a session for an existing extended event, namely **sqlserver.sql_statement_starting**.</span></span>
   
   * <span data-ttu-id="ee329-109">hello 事件是否包含特定更新字串的有限的 tooSQL 陳述式： **LIKE '%更新 tabEmployee %' 陳述式**。</span><span class="sxs-lookup"><span data-stu-id="ee329-109">hello event is limited tooSQL statements that contain a particular Update string: **statement LIKE '%UPDATE tabEmployee%'**.</span></span>
   * <span data-ttu-id="ee329-110">也就是選擇 toosend hello 輸出類型信號緩衝區 hello 事件 tooa 目標**package0.ring_buffer**。</span><span class="sxs-lookup"><span data-stu-id="ee329-110">Chooses toosend hello output of hello event tooa target of type Ring Buffer, namely  **package0.ring_buffer**.</span></span>
3. <span data-ttu-id="ee329-111">啟動 hello 事件工作階段。</span><span class="sxs-lookup"><span data-stu-id="ee329-111">Starts hello event session.</span></span>
4. <span data-ttu-id="ee329-112">發出幾個簡單的 SQL UPDATE 陳述式。</span><span class="sxs-lookup"><span data-stu-id="ee329-112">Issues a couple of simple SQL UPDATE statements.</span></span>
5. <span data-ttu-id="ee329-113">發出的 SQL SELECT 陳述式 tooretrieve 事件輸出 hello 信號緩衝區。</span><span class="sxs-lookup"><span data-stu-id="ee329-113">Issues a SQL SELECT statement tooretrieve event output from hello Ring Buffer.</span></span>
   
   * <span data-ttu-id="ee329-114">**sys.dm_xe_database_session_targets** 和其他動態管理檢視 (DMV) 會聯結在一起。</span><span class="sxs-lookup"><span data-stu-id="ee329-114">**sys.dm_xe_database_session_targets** and other dynamic management views (DMVs) are joined.</span></span>
6. <span data-ttu-id="ee329-115">停止 hello 事件工作階段。</span><span class="sxs-lookup"><span data-stu-id="ee329-115">Stops hello event session.</span></span>
7. <span data-ttu-id="ee329-116">卸除 hello 信號緩衝區目標，toorelease 及其資源。</span><span class="sxs-lookup"><span data-stu-id="ee329-116">Drops hello Ring Buffer target, toorelease its resources.</span></span>
8. <span data-ttu-id="ee329-117">卸除 hello 事件工作階段和 hello 示範資料表。</span><span class="sxs-lookup"><span data-stu-id="ee329-117">Drops hello event session and hello demo table.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ee329-118">必要條件</span><span class="sxs-lookup"><span data-stu-id="ee329-118">Prerequisites</span></span>

* <span data-ttu-id="ee329-119">Azure 帳戶和訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="ee329-119">An Azure account and subscription.</span></span> <span data-ttu-id="ee329-120">您可以註冊 [免費試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="ee329-120">You can sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="ee329-121">您可以在當中建立資料表的任何資料庫。</span><span class="sxs-lookup"><span data-stu-id="ee329-121">Any database you can create a table in.</span></span>
  
  * <span data-ttu-id="ee329-122">您可以選擇性快速[建立 **AdventureWorksLT** 示範資料庫](sql-database-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="ee329-122">Optionally you can [create an **AdventureWorksLT** demonstration database](sql-database-get-started.md) in minutes.</span></span>
* <span data-ttu-id="ee329-123">SQL Server Management Studio (ssms.exe)，最好是最新的每月更新版本。</span><span class="sxs-lookup"><span data-stu-id="ee329-123">SQL Server Management Studio (ssms.exe), ideally its latest monthly update version.</span></span> 
  <span data-ttu-id="ee329-124">您可以下載從 hello 最新 ssms.exe:</span><span class="sxs-lookup"><span data-stu-id="ee329-124">You can download hello latest ssms.exe from:</span></span>
  
  * <span data-ttu-id="ee329-125">名稱為 [下載 SQL Server Management Studio](http://msdn.microsoft.com/library/mt238290.aspx)的主題。</span><span class="sxs-lookup"><span data-stu-id="ee329-125">Topic titled [Download SQL Server Management Studio](http://msdn.microsoft.com/library/mt238290.aspx).</span></span>
  * [<span data-ttu-id="ee329-126">直接連結 toohello 下載。</span><span class="sxs-lookup"><span data-stu-id="ee329-126">A direct link toohello download.</span></span>](http://go.microsoft.com/fwlink/?linkid=616025)

## <a name="code-sample"></a><span data-ttu-id="ee329-127">程式碼範例</span><span class="sxs-lookup"><span data-stu-id="ee329-127">Code sample</span></span>

<span data-ttu-id="ee329-128">非常稍微修改，與 hello 下列信號緩衝區的程式碼範例可以執行 Azure SQL Database 或 Microsoft SQL Server 上。</span><span class="sxs-lookup"><span data-stu-id="ee329-128">With very minor modification, hello following Ring Buffer code sample can be run on either Azure SQL Database or Microsoft SQL Server.</span></span> <span data-ttu-id="ee329-129">hello 差異在於使用在步驟 5 中的 hello FROM 子句中的 hello 節點 '（_d）' hello 某些動態管理檢視 (Dmv)，名稱中的 hello 存在。</span><span class="sxs-lookup"><span data-stu-id="ee329-129">hello difference is hello presence of hello node '_database' in hello name of some dynamic management views (DMVs), used in hello FROM clause in Step 5.</span></span> <span data-ttu-id="ee329-130">例如：</span><span class="sxs-lookup"><span data-stu-id="ee329-130">For example:</span></span>

* <span data-ttu-id="ee329-131">sys.dm_xe**_database**_session_targets</span><span class="sxs-lookup"><span data-stu-id="ee329-131">sys.dm_xe**_database**_session_targets</span></span>
* <span data-ttu-id="ee329-132">sys.dm_xe_session_targets</span><span class="sxs-lookup"><span data-stu-id="ee329-132">sys.dm_xe_session_targets</span></span>

&nbsp;

```sql
GO
----  Transact-SQL.
---- Step set 1.

SET NOCOUNT ON;
GO


IF EXISTS
    (SELECT * FROM sys.objects
        WHERE type = 'U' and name = 'tabEmployee')
BEGIN
    DROP TABLE tabEmployee;
END
GO


CREATE TABLE tabEmployee
(
    EmployeeGuid         uniqueIdentifier   not null  default newid()  primary key,
    EmployeeId           int                not null  identity(1,1),
    EmployeeKudosCount   int                not null  default 0,
    EmployeeDescr        nvarchar(256)          null
);
GO


INSERT INTO tabEmployee ( EmployeeDescr )
    VALUES ( 'Jane Doe' );
GO

---- Step set 2.


IF EXISTS
    (SELECT * from sys.database_event_sessions
        WHERE name = 'eventsession_gm_azuresqldb51')
BEGIN
    DROP EVENT SESSION eventsession_gm_azuresqldb51
        ON DATABASE;
END
GO


CREATE
    EVENT SESSION eventsession_gm_azuresqldb51
    ON DATABASE
    ADD EVENT
        sqlserver.sql_statement_starting
            (
            ACTION (sqlserver.sql_text)
            WHERE statement LIKE '%UPDATE tabEmployee%'
            )
    ADD TARGET
        package0.ring_buffer
            (SET
                max_memory = 500   -- Units of KB.
            );
GO

---- Step set 3.


ALTER EVENT SESSION eventsession_gm_azuresqldb51
    ON DATABASE
    STATE = START;
GO

---- Step set 4.


SELECT 'BEFORE_Updates', EmployeeKudosCount, * FROM tabEmployee;

UPDATE tabEmployee
    SET EmployeeKudosCount = EmployeeKudosCount + 102;

UPDATE tabEmployee
    SET EmployeeKudosCount = EmployeeKudosCount + 1015;

SELECT 'AFTER__Updates', EmployeeKudosCount, * FROM tabEmployee;
GO

---- Step set 5.


SELECT
    se.name                      AS [session-name],
    ev.event_name,
    ac.action_name,
    st.target_name,
    se.session_source,
    st.target_data,
    CAST(st.target_data AS XML)  AS [target_data_XML]
FROM
               sys.dm_xe_database_session_event_actions  AS ac

    INNER JOIN sys.dm_xe_database_session_events         AS ev  ON ev.event_name = ac.event_name
        AND CAST(ev.event_session_address AS BINARY(8)) = CAST(ac.event_session_address AS BINARY(8))

    INNER JOIN sys.dm_xe_database_session_object_columns AS oc
         ON CAST(oc.event_session_address AS BINARY(8)) = CAST(ac.event_session_address AS BINARY(8))

    INNER JOIN sys.dm_xe_database_session_targets        AS st
         ON CAST(st.event_session_address AS BINARY(8)) = CAST(ac.event_session_address AS BINARY(8))

    INNER JOIN sys.dm_xe_database_sessions               AS se
         ON CAST(ac.event_session_address AS BINARY(8)) = CAST(se.address AS BINARY(8))
WHERE
        oc.column_name = 'occurrence_number'
    AND
        se.name        = 'eventsession_gm_azuresqldb51'
    AND
        ac.action_name = 'sql_text'
ORDER BY
    se.name,
    ev.event_name,
    ac.action_name,
    st.target_name,
    se.session_source
;
GO

---- Step set 6.


ALTER EVENT SESSION eventsession_gm_azuresqldb51
    ON DATABASE
    STATE = STOP;
GO

---- Step set 7.


ALTER EVENT SESSION eventsession_gm_azuresqldb51
    ON DATABASE
    DROP TARGET package0.ring_buffer;
GO

---- Step set 8.


DROP EVENT SESSION eventsession_gm_azuresqldb51
    ON DATABASE;
GO

DROP TABLE tabEmployee;
GO
```


&nbsp;

## <a name="ring-buffer-contents"></a><span data-ttu-id="ee329-133">信號緩衝區內容</span><span class="sxs-lookup"><span data-stu-id="ee329-133">Ring Buffer contents</span></span>

<span data-ttu-id="ee329-134">我們使用 ssms.exe toorun hello 程式碼範例。</span><span class="sxs-lookup"><span data-stu-id="ee329-134">We used ssms.exe toorun hello code sample.</span></span>

<span data-ttu-id="ee329-135">tooview hello 結果，我們在下按下 hello 儲存格 hello 資料行標頭**target_data_XML**。</span><span class="sxs-lookup"><span data-stu-id="ee329-135">tooview hello results, we clicked hello cell under hello column header **target_data_XML**.</span></span>

<span data-ttu-id="ee329-136">之後您 hello [結果] 窗格中按一下 hello 資料格底下 hello 資料行標頭**target_data_XML**。</span><span class="sxs-lookup"><span data-stu-id="ee329-136">Then in hello results pane we clicked hello cell under hello column header **target_data_XML**.</span></span> <span data-ttu-id="ee329-137">按一下 [在 ssms.exe 中的 hello hello 結果資料格的內容已顯示，以 XML 中建立另一個檔案] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="ee329-137">This click created another file tab in ssms.exe in which hello content of hello result cell was displayed, as XML.</span></span>

<span data-ttu-id="ee329-138">hello 輸出所示 hello 區塊後面。</span><span class="sxs-lookup"><span data-stu-id="ee329-138">hello output is shown in hello following block.</span></span> <span data-ttu-id="ee329-139">它看起來很長，但其實只是兩個 **<event>** 元素。</span><span class="sxs-lookup"><span data-stu-id="ee329-139">It looks long, but it is just two **<event>** elements.</span></span>

&nbsp;

```
<RingBufferTarget truncated="0" processingTime="0" totalEventsProcessed="2" eventCount="2" droppedCount="0" memoryUsed="1728">
  <event name="sql_statement_starting" package="sqlserver" timestamp="2015-09-22T15:29:31.317Z">
    <data name="state">
      <type name="statement_starting_state" package="sqlserver" />
      <value>0</value>
      <text>Normal</text>
    </data>
    <data name="line_number">
      <type name="int32" package="package0" />
      <value>7</value>
    </data>
    <data name="offset">
      <type name="int32" package="package0" />
      <value>184</value>
    </data>
    <data name="offset_end">
      <type name="int32" package="package0" />
      <value>328</value>
    </data>
    <data name="statement">
      <type name="unicode_string" package="package0" />
      <value>UPDATE tabEmployee
    SET EmployeeKudosCount = EmployeeKudosCount + 102</value>
    </data>
    <action name="sql_text" package="sqlserver">
      <type name="unicode_string" package="package0" />
      <value>
---- Step set 4.


SELECT 'BEFORE_Updates', EmployeeKudosCount, * FROM tabEmployee;

UPDATE tabEmployee
    SET EmployeeKudosCount = EmployeeKudosCount + 102;

UPDATE tabEmployee
    SET EmployeeKudosCount = EmployeeKudosCount + 1015;

SELECT 'AFTER__Updates', EmployeeKudosCount, * FROM tabEmployee;
</value>
    </action>
  </event>
  <event name="sql_statement_starting" package="sqlserver" timestamp="2015-09-22T15:29:31.327Z">
    <data name="state">
      <type name="statement_starting_state" package="sqlserver" />
      <value>0</value>
      <text>Normal</text>
    </data>
    <data name="line_number">
      <type name="int32" package="package0" />
      <value>10</value>
    </data>
    <data name="offset">
      <type name="int32" package="package0" />
      <value>340</value>
    </data>
    <data name="offset_end">
      <type name="int32" package="package0" />
      <value>486</value>
    </data>
    <data name="statement">
      <type name="unicode_string" package="package0" />
      <value>UPDATE tabEmployee
    SET EmployeeKudosCount = EmployeeKudosCount + 1015</value>
    </data>
    <action name="sql_text" package="sqlserver">
      <type name="unicode_string" package="package0" />
      <value>
---- Step set 4.


SELECT 'BEFORE_Updates', EmployeeKudosCount, * FROM tabEmployee;

UPDATE tabEmployee
    SET EmployeeKudosCount = EmployeeKudosCount + 102;

UPDATE tabEmployee
    SET EmployeeKudosCount = EmployeeKudosCount + 1015;

SELECT 'AFTER__Updates', EmployeeKudosCount, * FROM tabEmployee;
</value>
    </action>
  </event>
</RingBufferTarget>
```


#### <a name="release-resources-held-by-your-ring-buffer"></a><span data-ttu-id="ee329-140">釋放信號緩衝區佔用的資源</span><span class="sxs-lookup"><span data-stu-id="ee329-140">Release resources held by your Ring Buffer</span></span>

<span data-ttu-id="ee329-141">當您完成使用信號緩衝區中時，您可以將它移除，並釋放其資源發出**ALTER**像 hello 面這樣：</span><span class="sxs-lookup"><span data-stu-id="ee329-141">When you are done with your Ring Buffer, you can remove it and release its resources issuing an **ALTER** like hello following:</span></span>

```sql
ALTER EVENT SESSION eventsession_gm_azuresqldb51
    ON DATABASE
    DROP TARGET package0.ring_buffer;
GO
```


<span data-ttu-id="ee329-142">hello 定義的事件工作階段已更新，但不是會卸除。</span><span class="sxs-lookup"><span data-stu-id="ee329-142">hello definition of your event session is updated, but not dropped.</span></span> <span data-ttu-id="ee329-143">稍後您可以加入 hello 信號緩衝區 tooyour 事件工作階段的另一個執行個體：</span><span class="sxs-lookup"><span data-stu-id="ee329-143">Later you can add another instance of hello Ring Buffer tooyour event session:</span></span>

```sql
ALTER EVENT SESSION eventsession_gm_azuresqldb51
    ON DATABASE
    ADD TARGET
        package0.ring_buffer
            (SET
                max_memory = 500   -- Units of KB.
            );
```


## <a name="more-information"></a><span data-ttu-id="ee329-144">詳細資訊</span><span class="sxs-lookup"><span data-stu-id="ee329-144">More information</span></span>

<span data-ttu-id="ee329-145">是 hello Azure SQL database 的擴充事件的主要主題：</span><span class="sxs-lookup"><span data-stu-id="ee329-145">hello primary topic for extended events on Azure SQL Database is:</span></span>

* <span data-ttu-id="ee329-146">[SQL Database 中的擴充事件考量](sql-database-xevent-db-diff-from-svr.md)，對比 Azure SQL Database 與 Microsoft SQL Server 之間擴充事件的不同層面。</span><span class="sxs-lookup"><span data-stu-id="ee329-146">[Extended event considerations in SQL Database](sql-database-xevent-db-diff-from-svr.md), which contrasts some aspects of extended events that differ between Azure SQL Database versus Microsoft SQL Server.</span></span>

<span data-ttu-id="ee329-147">使用下列連結查看 hello 在擴充事件的其他程式碼範例主題。</span><span class="sxs-lookup"><span data-stu-id="ee329-147">Other code sample topics for extended events are available at hello following links.</span></span> <span data-ttu-id="ee329-148">不過，您必須定期檢查任何範例 toosee 是否 hello 範例以 Microsoft SQL Server 與 Azure SQL Database 為目標。</span><span class="sxs-lookup"><span data-stu-id="ee329-148">However, you must routinely check any sample toosee whether hello sample targets Microsoft SQL Server versus Azure SQL Database.</span></span> <span data-ttu-id="ee329-149">然後您可以決定是否需要的 toorun hello 範例次要變更。</span><span class="sxs-lookup"><span data-stu-id="ee329-149">Then you can decide whether minor changes are needed toorun hello sample.</span></span>

* <span data-ttu-id="ee329-150">Azure SQL Database 的程式碼範例： [SQL Database 中擴充事件的事件檔案目標程式碼](sql-database-xevent-code-event-file.md)</span><span class="sxs-lookup"><span data-stu-id="ee329-150">Code sample for Azure SQL Database: [Event File target code for extended events in SQL Database](sql-database-xevent-code-event-file.md)</span></span>

<!--
('lock_acquired' event.)

- Code sample for SQL Server: [Determine Which Queries Are Holding Locks](http://msdn.microsoft.com/library/bb677357.aspx)
- Code sample for SQL Server: [Find hello Objects That Have hello Most Locks Taken on Them](http://msdn.microsoft.com/library/bb630355.aspx)
-->
