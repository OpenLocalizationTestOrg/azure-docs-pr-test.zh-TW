---
title: "SQL Database 的 XEvent 信號緩衝區程式碼 | Microsoft Docs"
description: "提供 Transact-SQL 程式碼範例，可在 Azure SQL Database 中輕鬆又快速使用信號緩衝區目標。"
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
ms.openlocfilehash: 6fbefe151901ac3b15d93712422878fc4d6206f1
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="ring-buffer-target-code-for-extended-events-in-sql-database"></a><span data-ttu-id="246e1-103">SQL Database 中擴充事件的信號緩衝區目標程式碼</span><span class="sxs-lookup"><span data-stu-id="246e1-103">Ring Buffer target code for extended events in SQL Database</span></span>

[!INCLUDE [sql-database-xevents-selectors-1-include](../../includes/sql-database-xevents-selectors-1-include.md)]

<span data-ttu-id="246e1-104">您想要完整的程式碼範例以最簡單快速的方式在測試期間擷取和報告擴充事件的資訊。</span><span class="sxs-lookup"><span data-stu-id="246e1-104">You want a complete code sample for the easiest quick way to capture and report information for an extended event during a test.</span></span> <span data-ttu-id="246e1-105">擴充事件資料最簡單的目標是 [信號緩衝區目標](http://msdn.microsoft.com/library/ff878182.aspx)。</span><span class="sxs-lookup"><span data-stu-id="246e1-105">The easiest target for extended event data is the [Ring Buffer target](http://msdn.microsoft.com/library/ff878182.aspx).</span></span>

<span data-ttu-id="246e1-106">本主題提供會執行下列動作的 Transact-SQL 程式碼範例：</span><span class="sxs-lookup"><span data-stu-id="246e1-106">This topic presents a Transact-SQL code sample that:</span></span>

1. <span data-ttu-id="246e1-107">使用資料建立要示範的資料表。</span><span class="sxs-lookup"><span data-stu-id="246e1-107">Creates a table with data to demonstrate with.</span></span>
2. <span data-ttu-id="246e1-108">建立現有擴充事件的工作階段，名稱為 **sqlserver.sql_statement_starting**。</span><span class="sxs-lookup"><span data-stu-id="246e1-108">Creates a session for an existing extended event, namely **sqlserver.sql_statement_starting**.</span></span>
   
   * <span data-ttu-id="246e1-109">此事件僅限於包含特定 Update 字串的 SQL 陳述式： **statement LIKE '%UPDATE tabEmployee%'**。</span><span class="sxs-lookup"><span data-stu-id="246e1-109">The event is limited to SQL statements that contain a particular Update string: **statement LIKE '%UPDATE tabEmployee%'**.</span></span>
   * <span data-ttu-id="246e1-110">選擇要將事件的輸出傳送給信號緩衝區類型的目標，名稱為 **package0.ring_buffer**。</span><span class="sxs-lookup"><span data-stu-id="246e1-110">Chooses to send the output of the event to a target of type Ring Buffer, namely  **package0.ring_buffer**.</span></span>
3. <span data-ttu-id="246e1-111">啟動事件工作階段。</span><span class="sxs-lookup"><span data-stu-id="246e1-111">Starts the event session.</span></span>
4. <span data-ttu-id="246e1-112">發出幾個簡單的 SQL UPDATE 陳述式。</span><span class="sxs-lookup"><span data-stu-id="246e1-112">Issues a couple of simple SQL UPDATE statements.</span></span>
5. <span data-ttu-id="246e1-113">發出 SQL SELECT 陳述式擷取信號緩衝區的事件輸出。</span><span class="sxs-lookup"><span data-stu-id="246e1-113">Issues a SQL SELECT statement to retrieve event output from the Ring Buffer.</span></span>
   
   * <span data-ttu-id="246e1-114">**sys.dm_xe_database_session_targets** 和其他動態管理檢視 (DMV) 會聯結在一起。</span><span class="sxs-lookup"><span data-stu-id="246e1-114">**sys.dm_xe_database_session_targets** and other dynamic management views (DMVs) are joined.</span></span>
6. <span data-ttu-id="246e1-115">停止事件工作階段。</span><span class="sxs-lookup"><span data-stu-id="246e1-115">Stops the event session.</span></span>
7. <span data-ttu-id="246e1-116">卸除信號緩衝區目標以釋放其資源。</span><span class="sxs-lookup"><span data-stu-id="246e1-116">Drops the Ring Buffer target, to release its resources.</span></span>
8. <span data-ttu-id="246e1-117">卸除事件工作階段和示範資料表。</span><span class="sxs-lookup"><span data-stu-id="246e1-117">Drops the event session and the demo table.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="246e1-118">必要條件</span><span class="sxs-lookup"><span data-stu-id="246e1-118">Prerequisites</span></span>

* <span data-ttu-id="246e1-119">Azure 帳戶和訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="246e1-119">An Azure account and subscription.</span></span> <span data-ttu-id="246e1-120">您可以註冊 [免費試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="246e1-120">You can sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="246e1-121">您可以在當中建立資料表的任何資料庫。</span><span class="sxs-lookup"><span data-stu-id="246e1-121">Any database you can create a table in.</span></span>
  
  * <span data-ttu-id="246e1-122">您可以選擇性快速[建立 **AdventureWorksLT** 示範資料庫](sql-database-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="246e1-122">Optionally you can [create an **AdventureWorksLT** demonstration database](sql-database-get-started.md) in minutes.</span></span>
* <span data-ttu-id="246e1-123">SQL Server Management Studio (ssms.exe)，最好是最新的每月更新版本。</span><span class="sxs-lookup"><span data-stu-id="246e1-123">SQL Server Management Studio (ssms.exe), ideally its latest monthly update version.</span></span> 
  <span data-ttu-id="246e1-124">您可以從下列位置下載最新的 ssms.exe：</span><span class="sxs-lookup"><span data-stu-id="246e1-124">You can download the latest ssms.exe from:</span></span>
  
  * <span data-ttu-id="246e1-125">名稱為 [下載 SQL Server Management Studio](http://msdn.microsoft.com/library/mt238290.aspx)的主題。</span><span class="sxs-lookup"><span data-stu-id="246e1-125">Topic titled [Download SQL Server Management Studio](http://msdn.microsoft.com/library/mt238290.aspx).</span></span>
  * [<span data-ttu-id="246e1-126">下載的直接連結。</span><span class="sxs-lookup"><span data-stu-id="246e1-126">A direct link to the download.</span></span>](http://go.microsoft.com/fwlink/?linkid=616025)

## <a name="code-sample"></a><span data-ttu-id="246e1-127">程式碼範例</span><span class="sxs-lookup"><span data-stu-id="246e1-127">Code sample</span></span>

<span data-ttu-id="246e1-128">只要稍加修改，就可以在 Azure SQL Database 或 Microsoft SQL Server 上執行下列信號緩衝區的程式碼範例。</span><span class="sxs-lookup"><span data-stu-id="246e1-128">With very minor modification, the following Ring Buffer code sample can be run on either Azure SQL Database or Microsoft SQL Server.</span></span> <span data-ttu-id="246e1-129">不同之處在於有些動態管理檢視 (DMV) (步驟 5 的 FROM 子句中所使用) 的名稱中有 '_database' ()。</span><span class="sxs-lookup"><span data-stu-id="246e1-129">The difference is the presence of the node '_database' in the name of some dynamic management views (DMVs), used in the FROM clause in Step 5.</span></span> <span data-ttu-id="246e1-130">例如：</span><span class="sxs-lookup"><span data-stu-id="246e1-130">For example:</span></span>

* <span data-ttu-id="246e1-131">sys.dm_xe**_database**_session_targets</span><span class="sxs-lookup"><span data-stu-id="246e1-131">sys.dm_xe**_database**_session_targets</span></span>
* <span data-ttu-id="246e1-132">sys.dm_xe_session_targets</span><span class="sxs-lookup"><span data-stu-id="246e1-132">sys.dm_xe_session_targets</span></span>

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

## <a name="ring-buffer-contents"></a><span data-ttu-id="246e1-133">信號緩衝區內容</span><span class="sxs-lookup"><span data-stu-id="246e1-133">Ring Buffer contents</span></span>

<span data-ttu-id="246e1-134">我們使用了 ssms.exe 來執行程式碼範例。</span><span class="sxs-lookup"><span data-stu-id="246e1-134">We used ssms.exe to run the code sample.</span></span>

<span data-ttu-id="246e1-135">為了檢視結果，我們按了 **target_data_XML** 資料欄標題下的儲存格。</span><span class="sxs-lookup"><span data-stu-id="246e1-135">To view the results, we clicked the cell under the column header **target_data_XML**.</span></span>

<span data-ttu-id="246e1-136">然後在結果窗格中，我們按了 **target_data_XML** 資料欄標題下的儲存格。</span><span class="sxs-lookup"><span data-stu-id="246e1-136">Then in the results pane we clicked the cell under the column header **target_data_XML**.</span></span> <span data-ttu-id="246e1-137">這個點按動作在 ssms.exe 中以 XML 格式建立了另一個檔案索引標籤，其中顯示了結果儲存格的內容。</span><span class="sxs-lookup"><span data-stu-id="246e1-137">This click created another file tab in ssms.exe in which the content of the result cell was displayed, as XML.</span></span>

<span data-ttu-id="246e1-138">輸出如下列區塊所示。</span><span class="sxs-lookup"><span data-stu-id="246e1-138">The output is shown in the following block.</span></span> <span data-ttu-id="246e1-139">它看起來很長，但其實只是兩個 **<event>** 元素。</span><span class="sxs-lookup"><span data-stu-id="246e1-139">It looks long, but it is just two **<event>** elements.</span></span>

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


#### <a name="release-resources-held-by-your-ring-buffer"></a><span data-ttu-id="246e1-140">釋放信號緩衝區佔用的資源</span><span class="sxs-lookup"><span data-stu-id="246e1-140">Release resources held by your Ring Buffer</span></span>

<span data-ttu-id="246e1-141">當您處理完信號緩衝區時，可以發出 **ALTER** 將它移除並釋放其資源，如下所示：</span><span class="sxs-lookup"><span data-stu-id="246e1-141">When you are done with your Ring Buffer, you can remove it and release its resources issuing an **ALTER** like the following:</span></span>

```sql
ALTER EVENT SESSION eventsession_gm_azuresqldb51
    ON DATABASE
    DROP TARGET package0.ring_buffer;
GO
```


<span data-ttu-id="246e1-142">事件工作階段的定義會更新，但不會卸除。</span><span class="sxs-lookup"><span data-stu-id="246e1-142">The definition of your event session is updated, but not dropped.</span></span> <span data-ttu-id="246e1-143">稍後您可以將信號緩衝區的另一個執行個體加入事件工作階段：</span><span class="sxs-lookup"><span data-stu-id="246e1-143">Later you can add another instance of the Ring Buffer to your event session:</span></span>

```sql
ALTER EVENT SESSION eventsession_gm_azuresqldb51
    ON DATABASE
    ADD TARGET
        package0.ring_buffer
            (SET
                max_memory = 500   -- Units of KB.
            );
```


## <a name="more-information"></a><span data-ttu-id="246e1-144">詳細資訊</span><span class="sxs-lookup"><span data-stu-id="246e1-144">More information</span></span>

<span data-ttu-id="246e1-145">Azure SQL Database 上擴充事件的主要主題是：</span><span class="sxs-lookup"><span data-stu-id="246e1-145">The primary topic for extended events on Azure SQL Database is:</span></span>

* <span data-ttu-id="246e1-146">[SQL Database 中的擴充事件考量](sql-database-xevent-db-diff-from-svr.md)，對比 Azure SQL Database 與 Microsoft SQL Server 之間擴充事件的不同層面。</span><span class="sxs-lookup"><span data-stu-id="246e1-146">[Extended event considerations in SQL Database](sql-database-xevent-db-diff-from-svr.md), which contrasts some aspects of extended events that differ between Azure SQL Database versus Microsoft SQL Server.</span></span>

<span data-ttu-id="246e1-147">下列連結提供擴充事件的其他程式碼範例主題。</span><span class="sxs-lookup"><span data-stu-id="246e1-147">Other code sample topics for extended events are available at the following links.</span></span> <span data-ttu-id="246e1-148">不過，您必須定期檢查所有範例以查看範例是否適用於 Microsoft SQL Server 與 Azure SQL Database。</span><span class="sxs-lookup"><span data-stu-id="246e1-148">However, you must routinely check any sample to see whether the sample targets Microsoft SQL Server versus Azure SQL Database.</span></span> <span data-ttu-id="246e1-149">然後您可以決定是否需要稍加變更來執行範例。</span><span class="sxs-lookup"><span data-stu-id="246e1-149">Then you can decide whether minor changes are needed to run the sample.</span></span>

* <span data-ttu-id="246e1-150">Azure SQL Database 的程式碼範例： [SQL Database 中擴充事件的事件檔案目標程式碼](sql-database-xevent-code-event-file.md)</span><span class="sxs-lookup"><span data-stu-id="246e1-150">Code sample for Azure SQL Database: [Event File target code for extended events in SQL Database](sql-database-xevent-code-event-file.md)</span></span>

<!--
('lock_acquired' event.)

- Code sample for SQL Server: [Determine Which Queries Are Holding Locks](http://msdn.microsoft.com/library/bb677357.aspx)
- Code sample for SQL Server: [Find the Objects That Have the Most Locks Taken on Them](http://msdn.microsoft.com/library/bb630355.aspx)
-->
