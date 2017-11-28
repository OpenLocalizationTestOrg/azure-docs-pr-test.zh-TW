---
title: "SQL Database 中的 aaaExtended 事件 |Microsoft 文件"
description: "描述 Azure SQL Database 中的擴充事件 (XEvents)，以及事件工作階段與 Microsoft SQL Server 中的事件工作階段有如何的些微不同。"
services: sql-database
documentationcenter: 
author: MightyPen
manager: jhubbard
editor: 
tags: 
ms.assetid: 3b28cf15-f820-4b3c-8310-908d6d5b9d0c
ms.service: sql-database
ms.custom: monitor & tune
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/03/2017
ms.author: genemi
ms.openlocfilehash: 8c966a84412aa561c92b16e5c6902102483eb1bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="extended-events-in-sql-database"></a><span data-ttu-id="993a2-103">SQL Database 中的擴充事件</span><span class="sxs-lookup"><span data-stu-id="993a2-103">Extended events in SQL Database</span></span>
[!INCLUDE [sql-database-xevents-selectors-1-include](../../includes/sql-database-xevents-selectors-1-include.md)]

<span data-ttu-id="993a2-104">本主題說明如何擴充的事件，Azure SQL Database 中的 hello 實作稍有不同的比較的 tooextended Microsoft SQL Server 中的事件。</span><span class="sxs-lookup"><span data-stu-id="993a2-104">This topic explains how hello implementation of extended events in Azure SQL Database is slightly different compared tooextended events in Microsoft SQL Server.</span></span>

- <span data-ttu-id="993a2-105">SQL Database V12 獲得 hello hello 擴充的事件功能第二個行事曆 2015年的下半部。</span><span class="sxs-lookup"><span data-stu-id="993a2-105">SQL Database V12 gained hello extended events feature in hello second half of calendar 2015.</span></span>
- <span data-ttu-id="993a2-106">SQL Server 自 2008 開始即具有擴充事件。</span><span class="sxs-lookup"><span data-stu-id="993a2-106">SQL Server has had extended events since 2008.</span></span>
- <span data-ttu-id="993a2-107">hello 功能集的 SQL 資料庫上的擴充事件是穩固的 SQL Server 上的 hello 功能子集。</span><span class="sxs-lookup"><span data-stu-id="993a2-107">hello feature set of extended events on SQL Database is a robust subset of hello features on SQL Server.</span></span>

<span data-ttu-id="993a2-108">*XEvents* 是非正式暱稱，有時在部落格或其他非正式位置用於「擴充事件」。</span><span class="sxs-lookup"><span data-stu-id="993a2-108">*XEvents* is an informal nickname that is sometimes used for 'extended events' in blogs and other informal locations.</span></span>

<span data-ttu-id="993a2-109">如需有關 Azure SQL Database 和 Microsoft SQL Server 之擴充事件的其他資訊，請參閱：</span><span class="sxs-lookup"><span data-stu-id="993a2-109">Additional information about extended events, for Azure SQL Database and Microsoft SQL Server, is available at:</span></span>

- [<span data-ttu-id="993a2-110">Quick Start: Extended events in SQL Server (快速入門：SQL Server 中的擴充事件)</span><span class="sxs-lookup"><span data-stu-id="993a2-110">Quick Start: Extended events in SQL Server</span></span>](http://msdn.microsoft.com/library/mt733217.aspx)
- [<span data-ttu-id="993a2-111">擴充事件</span><span class="sxs-lookup"><span data-stu-id="993a2-111">Extended Events</span></span>](http://msdn.microsoft.com/library/bb630282.aspx)

## <a name="prerequisites"></a><span data-ttu-id="993a2-112">必要條件</span><span class="sxs-lookup"><span data-stu-id="993a2-112">Prerequisites</span></span>

<span data-ttu-id="993a2-113">本主題假設您已經有一些下列項目的知識：</span><span class="sxs-lookup"><span data-stu-id="993a2-113">This topic assumes you already have some knowledge of:</span></span>

- <span data-ttu-id="993a2-114">[Azure SQL Database 服務](https://azure.microsoft.com/services/sql-database/)。</span><span class="sxs-lookup"><span data-stu-id="993a2-114">[Azure SQL Database service](https://azure.microsoft.com/services/sql-database/).</span></span>
- <span data-ttu-id="993a2-115">[Extended events](http://msdn.microsoft.com/library/bb630282.aspx) 。</span><span class="sxs-lookup"><span data-stu-id="993a2-115">[Extended events](http://msdn.microsoft.com/library/bb630282.aspx) in Microsoft SQL Server.</span></span>

- <span data-ttu-id="993a2-116">擴充事件的相關文件的 hello 大量適用於 tooboth SQL Server 和 SQL Database。</span><span class="sxs-lookup"><span data-stu-id="993a2-116">hello bulk of our documentation about extended events applies tooboth SQL Server and SQL Database.</span></span>

<span data-ttu-id="993a2-117">先前的曝光 toohello 下列項目時，很有幫助選擇 hello 事件檔案儲存為 hello[目標](#AzureXEventsTargets):</span><span class="sxs-lookup"><span data-stu-id="993a2-117">Prior exposure toohello following items is helpful when choosing hello Event File as hello [target](#AzureXEventsTargets):</span></span>

- [<span data-ttu-id="993a2-118">Azure 儲存體服務</span><span class="sxs-lookup"><span data-stu-id="993a2-118">Azure Storage service</span></span>](https://azure.microsoft.com/services/storage/)


- <span data-ttu-id="993a2-119">PowerShell</span><span class="sxs-lookup"><span data-stu-id="993a2-119">PowerShell</span></span>
    - <span data-ttu-id="993a2-120">[使用 Azure 儲存體的 Azure PowerShell](../storage/common/storage-powershell-guide-full.md) -提供 PowerShell 和 hello Azure 儲存體服務的完整資訊。</span><span class="sxs-lookup"><span data-stu-id="993a2-120">[Using Azure PowerShell with Azure Storage](../storage/common/storage-powershell-guide-full.md) - Provides comprehensive information about PowerShell and hello Azure Storage service.</span></span>

## <a name="code-samples"></a><span data-ttu-id="993a2-121">程式碼範例</span><span class="sxs-lookup"><span data-stu-id="993a2-121">Code samples</span></span>

<span data-ttu-id="993a2-122">相關的主題提供兩個程式碼範例：</span><span class="sxs-lookup"><span data-stu-id="993a2-122">Related topics provide two code samples:</span></span>


- [<span data-ttu-id="993a2-123">SQL Database 中擴充事件的信號緩衝區目標程式碼</span><span class="sxs-lookup"><span data-stu-id="993a2-123">Ring Buffer target code for extended events in SQL Database</span></span>](sql-database-xevent-code-ring-buffer.md)
    - <span data-ttu-id="993a2-124">簡短的簡單 Transact-SQL 指令碼。</span><span class="sxs-lookup"><span data-stu-id="993a2-124">Short simple Transact-SQL script.</span></span>
    - <span data-ttu-id="993a2-125">我們在 hello 程式碼範例主題中，當您完成的信號緩衝區目標之後，您應該釋放其資源執行 卸除 alter 強調`ALTER EVENT SESSION ... ON DATABASE DROP TARGET ...;`陳述式。</span><span class="sxs-lookup"><span data-stu-id="993a2-125">We emphasize in hello code sample topic that, when you are done with a Ring Buffer target, you should release its resources by executing an alter-drop `ALTER EVENT SESSION ... ON DATABASE DROP TARGET ...;` statement.</span></span> <span data-ttu-id="993a2-126">稍後您可以藉由 `ALTER EVENT SESSION ... ON DATABASE ADD TARGET ...`，加入信號緩衝區的另一個執行個體。</span><span class="sxs-lookup"><span data-stu-id="993a2-126">Later you can add another instance of Ring Buffer by `ALTER EVENT SESSION ... ON DATABASE ADD TARGET ...`.</span></span>


- [<span data-ttu-id="993a2-127">SQL Database 中擴充事件的事件檔案目標程式碼</span><span class="sxs-lookup"><span data-stu-id="993a2-127">Event File target code for extended events in SQL Database</span></span>](sql-database-xevent-code-event-file.md)
    - <span data-ttu-id="993a2-128">階段 1 是 PowerShell toocreate Azure 儲存體容器。</span><span class="sxs-lookup"><span data-stu-id="993a2-128">Phase 1 is PowerShell toocreate an Azure Storage container.</span></span>
    - <span data-ttu-id="993a2-129">階段 2 是使用 hello Azure 儲存體容器的 Transact SQL。</span><span class="sxs-lookup"><span data-stu-id="993a2-129">Phase 2 is Transact-SQL that uses hello Azure Storage container.</span></span>

## <a name="transact-sql-differences"></a><span data-ttu-id="993a2-130">Transact-SQL 差異</span><span class="sxs-lookup"><span data-stu-id="993a2-130">Transact-SQL differences</span></span>


- <span data-ttu-id="993a2-131">當您執行 hello [CREATE EVENT SESSION](http://msdn.microsoft.com/library/bb677289.aspx)命令在 SQL Server 上使用 hello **ON SERVER**子句。</span><span class="sxs-lookup"><span data-stu-id="993a2-131">When you execute hello [CREATE EVENT SESSION](http://msdn.microsoft.com/library/bb677289.aspx) command on SQL Server, you use hello **ON SERVER** clause.</span></span> <span data-ttu-id="993a2-132">但您可以在 SQL 資料庫上使用 hello **ON DATABASE**子句改為。</span><span class="sxs-lookup"><span data-stu-id="993a2-132">But on SQL Database you use hello **ON DATABASE** clause instead.</span></span>


- <span data-ttu-id="993a2-133">hello **ON DATABASE**子句也適用於 toohello [ALTER EVENT SESSION](http://msdn.microsoft.com/library/bb630368.aspx)和[DROP EVENT SESSION](http://msdn.microsoft.com/library/bb630257.aspx) TRANSACT-SQL 命令。</span><span class="sxs-lookup"><span data-stu-id="993a2-133">hello **ON DATABASE** clause also applies toohello [ALTER EVENT SESSION](http://msdn.microsoft.com/library/bb630368.aspx) and [DROP EVENT SESSION](http://msdn.microsoft.com/library/bb630257.aspx) Transact-SQL commands.</span></span>


- <span data-ttu-id="993a2-134">最佳作法是 tooinclude hello 事件工作階段選項的**STARTUP_STATE = ON**中您**CREATE EVENT SESSION**或**ALTER EVENT SESSION**陳述式。</span><span class="sxs-lookup"><span data-stu-id="993a2-134">A best practice is tooinclude hello event session option of **STARTUP_STATE = ON** in your **CREATE EVENT SESSION**  or **ALTER EVENT SESSION** statements.</span></span>
    - <span data-ttu-id="993a2-135">hello **= ON**值支援在 hello 邏輯資料庫，因為 tooa 容錯移轉的重新設定之後自動重新啟動。</span><span class="sxs-lookup"><span data-stu-id="993a2-135">hello **= ON** value supports an automatic restart after a reconfiguration of hello logical database due tooa failover.</span></span>

## <a name="new-catalog-views"></a><span data-ttu-id="993a2-136">新的目錄檢視</span><span class="sxs-lookup"><span data-stu-id="993a2-136">New catalog views</span></span>

<span data-ttu-id="993a2-137">hello 擴充的事件功能支援數個[目錄檢視](http://msdn.microsoft.com/library/ms174365.aspx)。</span><span class="sxs-lookup"><span data-stu-id="993a2-137">hello extended events feature is supported by several [catalog views](http://msdn.microsoft.com/library/ms174365.aspx).</span></span> <span data-ttu-id="993a2-138">目錄檢視會告訴您有關*中繼資料或定義*hello 目前資料庫中的使用者建立的事件工作階段。</span><span class="sxs-lookup"><span data-stu-id="993a2-138">Catalog views tell you about *metadata or definitions* of user-created event sessions in hello current database.</span></span> <span data-ttu-id="993a2-139">hello 檢視不會傳回執行個體使用中的事件工作階段的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="993a2-139">hello views do not return information about instances of active event sessions.</span></span>

| <span data-ttu-id="993a2-140">名稱</span><span class="sxs-lookup"><span data-stu-id="993a2-140">Name of</span></span><br/><span data-ttu-id="993a2-141">目錄檢視的名稱</span><span class="sxs-lookup"><span data-stu-id="993a2-141">catalog view</span></span> | <span data-ttu-id="993a2-142">說明</span><span class="sxs-lookup"><span data-stu-id="993a2-142">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="993a2-143">**sys.database_event_session_actions**</span><span class="sxs-lookup"><span data-stu-id="993a2-143">**sys.database_event_session_actions**</span></span> |<span data-ttu-id="993a2-144">針對事件工作階段的每個事件上的每個動作傳回資料列。</span><span class="sxs-lookup"><span data-stu-id="993a2-144">Returns a row for each action on each event of an event session.</span></span> |
| <span data-ttu-id="993a2-145">**sys.database_event_session_events**</span><span class="sxs-lookup"><span data-stu-id="993a2-145">**sys.database_event_session_events**</span></span> |<span data-ttu-id="993a2-146">針對事件工作階段中的每個事件傳回資料列。</span><span class="sxs-lookup"><span data-stu-id="993a2-146">Returns a row for each event in an event session.</span></span> |
| <span data-ttu-id="993a2-147">**sys.database_event_session_fields**</span><span class="sxs-lookup"><span data-stu-id="993a2-147">**sys.database_event_session_fields**</span></span> |<span data-ttu-id="993a2-148">針對已在事件和目標上明確設定的每個可自訂資料行傳回資料列。</span><span class="sxs-lookup"><span data-stu-id="993a2-148">Returns a row for each customize-able column that was explicitly set on events and targets.</span></span> |
| <span data-ttu-id="993a2-149">**sys.database_event_session_targets**</span><span class="sxs-lookup"><span data-stu-id="993a2-149">**sys.database_event_session_targets**</span></span> |<span data-ttu-id="993a2-150">針對事件工作階段的每個事件目標傳回資料列。</span><span class="sxs-lookup"><span data-stu-id="993a2-150">Returns a row for each event target for an event session.</span></span> |
| <span data-ttu-id="993a2-151">**sys.database_event_sessions**</span><span class="sxs-lookup"><span data-stu-id="993a2-151">**sys.database_event_sessions**</span></span> |<span data-ttu-id="993a2-152">Hello SQL Database 的資料庫中每個事件工作階段傳回一個資料列。</span><span class="sxs-lookup"><span data-stu-id="993a2-152">Returns a row for each event session in hello SQL Database database.</span></span> |

<span data-ttu-id="993a2-153">在 Microsoft SQL Server 中，類似的目錄檢視具有包含 .server_\_ 而不是 .database\_ 的名稱。</span><span class="sxs-lookup"><span data-stu-id="993a2-153">In Microsoft SQL Server, similar catalog views have names that include *.server\_* instead of *.database\_*.</span></span> <span data-ttu-id="993a2-154">hello 名稱模式就像是**sys.server_event_%**。</span><span class="sxs-lookup"><span data-stu-id="993a2-154">hello name pattern is like **sys.server_event_%**.</span></span>

## <a name="new-dynamic-management-views-dmvshttpmsdnmicrosoftcomlibraryms188754aspx"></a><span data-ttu-id="993a2-155">新的動態管理檢視 [(DMV)](http://msdn.microsoft.com/library/ms188754.aspx)</span><span class="sxs-lookup"><span data-stu-id="993a2-155">New dynamic management views [(DMVs)](http://msdn.microsoft.com/library/ms188754.aspx)</span></span>

<span data-ttu-id="993a2-156">Azure SQL Database 具有支援擴充事件的 [動態管理檢視 (DMV)](http://msdn.microsoft.com/library/bb677293.aspx) 。</span><span class="sxs-lookup"><span data-stu-id="993a2-156">Azure SQL Database has [dynamic management views (DMVs)](http://msdn.microsoft.com/library/bb677293.aspx) that support extended events.</span></span> <span data-ttu-id="993a2-157">DMV 會告訴您 *作用中* 事件工作階段的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="993a2-157">DMVs tell you about *active* event sessions.</span></span>

| <span data-ttu-id="993a2-158">DMV 的名稱</span><span class="sxs-lookup"><span data-stu-id="993a2-158">Name of DMV</span></span> | <span data-ttu-id="993a2-159">說明</span><span class="sxs-lookup"><span data-stu-id="993a2-159">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="993a2-160">**sys.dm_xe_database_session_event_actions**</span><span class="sxs-lookup"><span data-stu-id="993a2-160">**sys.dm_xe_database_session_event_actions**</span></span> |<span data-ttu-id="993a2-161">會傳回事件工作階段動作的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="993a2-161">Returns information about event session actions.</span></span> |
| <span data-ttu-id="993a2-162">**sys.dm_xe_database_session_events**</span><span class="sxs-lookup"><span data-stu-id="993a2-162">**sys.dm_xe_database_session_events**</span></span> |<span data-ttu-id="993a2-163">會傳回工作階段事件的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="993a2-163">Returns information about session events.</span></span> |
| <span data-ttu-id="993a2-164">**sys.dm_xe_database_session_object_columns**</span><span class="sxs-lookup"><span data-stu-id="993a2-164">**sys.dm_xe_database_session_object_columns**</span></span> |<span data-ttu-id="993a2-165">顯示 hello 組態值是繫結的 tooa 工作階段物件。</span><span class="sxs-lookup"><span data-stu-id="993a2-165">Shows hello configuration values for objects that are bound tooa session.</span></span> |
| <span data-ttu-id="993a2-166">**sys.dm_xe_database_session_targets**</span><span class="sxs-lookup"><span data-stu-id="993a2-166">**sys.dm_xe_database_session_targets**</span></span> |<span data-ttu-id="993a2-167">會傳回工作階段目標的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="993a2-167">Returns information about session targets.</span></span> |
| <span data-ttu-id="993a2-168">**sys.dm_xe_database_sessions**</span><span class="sxs-lookup"><span data-stu-id="993a2-168">**sys.dm_xe_database_sessions**</span></span> |<span data-ttu-id="993a2-169">傳回一個資料列是已設定領域的 toohello 目前資料庫每個事件工作階段。</span><span class="sxs-lookup"><span data-stu-id="993a2-169">Returns a row for each event session that is scoped toohello current database.</span></span> |

<span data-ttu-id="993a2-170">Microsoft SQL Server，在類似目錄檢視會命名為 hello 不*\_資料庫*hello 一部分名稱，例如：</span><span class="sxs-lookup"><span data-stu-id="993a2-170">In Microsoft SQL Server, similar catalog views are named without hello *\_database* portion of hello name, such as:</span></span>

- <span data-ttu-id="993a2-171">**sys.dm_xe_sessions**，而不是</span><span class="sxs-lookup"><span data-stu-id="993a2-171">**sys.dm_xe_sessions**, instead of name</span></span><br/><span data-ttu-id="993a2-172">**sys.dm_xe_database_sessions** 名稱。</span><span class="sxs-lookup"><span data-stu-id="993a2-172">**sys.dm_xe_database_sessions**.</span></span>

### <a name="dmvs-common-tooboth"></a><span data-ttu-id="993a2-173">Dmv 常見 tooboth</span><span class="sxs-lookup"><span data-stu-id="993a2-173">DMVs common tooboth</span></span>
<span data-ttu-id="993a2-174">擴充事件有更多 Dmv 的常見 tooboth Azure SQL Database 和 Microsoft SQL Server:</span><span class="sxs-lookup"><span data-stu-id="993a2-174">For extended events there are additional DMVs that are common tooboth Azure SQL Database and Microsoft SQL Server:</span></span>

- <span data-ttu-id="993a2-175">**sys.dm_xe_map_values**</span><span class="sxs-lookup"><span data-stu-id="993a2-175">**sys.dm_xe_map_values**</span></span>
- <span data-ttu-id="993a2-176">**sys.dm_xe_object_columns**</span><span class="sxs-lookup"><span data-stu-id="993a2-176">**sys.dm_xe_object_columns**</span></span>
- <span data-ttu-id="993a2-177">**sys.dm_xe_objects**</span><span class="sxs-lookup"><span data-stu-id="993a2-177">**sys.dm_xe_objects**</span></span>
- <span data-ttu-id="993a2-178">**sys.dm_xe_packages**</span><span class="sxs-lookup"><span data-stu-id="993a2-178">**sys.dm_xe_packages**</span></span>

 <a name="sqlfindseventsactionstargets" id="sqlfindseventsactionstargets"></a>

## <a name="find-hello-available-extended-events-actions-and-targets"></a><span data-ttu-id="993a2-179">尋找 hello 可用的擴充的事件、 動作和目標</span><span class="sxs-lookup"><span data-stu-id="993a2-179">Find hello available extended events, actions, and targets</span></span>

<span data-ttu-id="993a2-180">您可以執行簡單 SQL**選取**tooobtain hello 可用的事件、 動作和目標的清單。</span><span class="sxs-lookup"><span data-stu-id="993a2-180">You can run a simple SQL **SELECT** tooobtain a list of hello available events, actions, and target.</span></span>

```sql
SELECT
        o.object_type,
        p.name         AS [package_name],
        o.name         AS [db_object_name],
        o.description  AS [db_obj_description]
    FROM
                   sys.dm_xe_objects  AS o
        INNER JOIN sys.dm_xe_packages AS p  ON p.guid = o.package_guid
    WHERE
        o.object_type in
            (
            'action',  'event',  'target'
            )
    ORDER BY
        o.object_type,
        p.name,
        o.name;
```


<span data-ttu-id="993a2-181"><a name="AzureXEventsTargets" id="AzureXEventsTargets"></a> &nbsp;</span><span class="sxs-lookup"><span data-stu-id="993a2-181"><a name="AzureXEventsTargets" id="AzureXEventsTargets"></a> &nbsp;</span></span>

## <a name="targets-for-your-sql-database-event-sessions"></a><span data-ttu-id="993a2-182">您的 SQL Database 事件工作階段的目標</span><span class="sxs-lookup"><span data-stu-id="993a2-182">Targets for your SQL Database event sessions</span></span>

<span data-ttu-id="993a2-183">以下是可以從您的 SQL Database 上的事件工作階段擷取結果的目標：</span><span class="sxs-lookup"><span data-stu-id="993a2-183">Here are targets that can capture results from your event sessions on SQL Database:</span></span>

- <span data-ttu-id="993a2-184">[信號緩衝區目標](http://msdn.microsoft.com/library/ff878182.aspx) -在記憶體中簡短保留事件資料。</span><span class="sxs-lookup"><span data-stu-id="993a2-184">[Ring Buffer target](http://msdn.microsoft.com/library/ff878182.aspx) - Briefly holds event data in memory.</span></span>
- <span data-ttu-id="993a2-185">[事件計數器目標](http://msdn.microsoft.com/library/ff878025.aspx) -會計算在擴充事件工作階段期間發生的所有事件。</span><span class="sxs-lookup"><span data-stu-id="993a2-185">[Event Counter target](http://msdn.microsoft.com/library/ff878025.aspx) - Counts all events that occur during an extended events session.</span></span>
- <span data-ttu-id="993a2-186">[事件檔案目標](http://msdn.microsoft.com/library/ff878115.aspx)-寫入完整緩衝區 tooan Azure 儲存體容器。</span><span class="sxs-lookup"><span data-stu-id="993a2-186">[Event File target](http://msdn.microsoft.com/library/ff878115.aspx) - Writes complete buffers tooan Azure Storage container.</span></span>

<span data-ttu-id="993a2-187">hello[事件追蹤的 Windows (ETW)](http://msdn.microsoft.com/library/ms751538.aspx)應用程式開發介面不是適用於 SQL Database 上擴充的事件。</span><span class="sxs-lookup"><span data-stu-id="993a2-187">hello [Event Tracing for Windows (ETW)](http://msdn.microsoft.com/library/ms751538.aspx) API is not available for extended events on SQL Database.</span></span>

## <a name="restrictions"></a><span data-ttu-id="993a2-188">限制</span><span class="sxs-lookup"><span data-stu-id="993a2-188">Restrictions</span></span>

<span data-ttu-id="993a2-189">有兩個安全性相關的差異 befitting hello 雲端環境的 SQL 資料庫：</span><span class="sxs-lookup"><span data-stu-id="993a2-189">There are a couple of security-related differences befitting hello cloud environment of SQL Database:</span></span>

- <span data-ttu-id="993a2-190">擴充的事件是在 hello 單一租用戶隔離模型上所建構。</span><span class="sxs-lookup"><span data-stu-id="993a2-190">Extended events are founded on hello single-tenant isolation model.</span></span> <span data-ttu-id="993a2-191">一個資料庫中的事件工作階段無法從另一個資料庫存取資料或事件。</span><span class="sxs-lookup"><span data-stu-id="993a2-191">An event session in one database cannot access data or events from another database.</span></span>
- <span data-ttu-id="993a2-192">無法發出**CREATE EVENT SESSION** hello 內容中的 hello 的陳述式**主要**資料庫。</span><span class="sxs-lookup"><span data-stu-id="993a2-192">You cannot issue a **CREATE EVENT SESSION** statement in hello context of hello **master** database.</span></span>

## <a name="permission-model"></a><span data-ttu-id="993a2-193">權限模型</span><span class="sxs-lookup"><span data-stu-id="993a2-193">Permission model</span></span>

<span data-ttu-id="993a2-194">您必須擁有**控制項**權限 hello 資料庫 tooissue **CREATE EVENT SESSION**陳述式。</span><span class="sxs-lookup"><span data-stu-id="993a2-194">You must have **Control** permission on hello database tooissue a **CREATE EVENT SESSION** statement.</span></span> <span data-ttu-id="993a2-195">hello 資料庫擁有者 (dbo) 有**控制項**權限。</span><span class="sxs-lookup"><span data-stu-id="993a2-195">hello database owner (dbo) has **Control** permission.</span></span>

### <a name="storage-container-authorizations"></a><span data-ttu-id="993a2-196">儲存體容器授權</span><span class="sxs-lookup"><span data-stu-id="993a2-196">Storage container authorizations</span></span>

<span data-ttu-id="993a2-197">hello 您產生必須同時指定 Azure 儲存體容器的 SAS 權杖**rwl** hello 權限。</span><span class="sxs-lookup"><span data-stu-id="993a2-197">hello SAS token you generate for your Azure Storage container must specify **rwl** for hello permissions.</span></span> <span data-ttu-id="993a2-198">hello **rwl**值會提供下列權限的 hello:</span><span class="sxs-lookup"><span data-stu-id="993a2-198">hello **rwl** value provides hello following permissions:</span></span>

- <span data-ttu-id="993a2-199">讀取</span><span class="sxs-lookup"><span data-stu-id="993a2-199">Read</span></span>
- <span data-ttu-id="993a2-200">寫入</span><span class="sxs-lookup"><span data-stu-id="993a2-200">Write</span></span>
- <span data-ttu-id="993a2-201">列出</span><span class="sxs-lookup"><span data-stu-id="993a2-201">List</span></span>

## <a name="performance-considerations"></a><span data-ttu-id="993a2-202">效能考量</span><span class="sxs-lookup"><span data-stu-id="993a2-202">Performance considerations</span></span>

<span data-ttu-id="993a2-203">有大量使用擴充的事件便會累積更多使用中的記憶體，而不是狀況良好的 hello 案例整體系統。</span><span class="sxs-lookup"><span data-stu-id="993a2-203">There are scenarios where intensive use of extended events can accumulate more active memory than is healthy for hello overall system.</span></span> <span data-ttu-id="993a2-204">因此 hello Azure SQL Database 系統以動態方式設定，並調整 hello 中可以累積的事件工作階段的記憶體數量的限制。</span><span class="sxs-lookup"><span data-stu-id="993a2-204">Therefore hello Azure SQL Database system dynamically sets and adjusts limits on hello amount of active memory that can be accumulated by an event session.</span></span> <span data-ttu-id="993a2-205">許多因素而進入 hello 動態計算。</span><span class="sxs-lookup"><span data-stu-id="993a2-205">Many factors go into hello dynamic calculation.</span></span>

<span data-ttu-id="993a2-206">如果您收到錯誤訊息，指出已強制執行記憶體最大值，您可以採取的一些更正動作為：</span><span class="sxs-lookup"><span data-stu-id="993a2-206">If you receive an error message that says a memory maximum was enforced, some corrective actions you can take are:</span></span>

- <span data-ttu-id="993a2-207">執行較少的並行事件工作階段。</span><span class="sxs-lookup"><span data-stu-id="993a2-207">Run fewer concurrent event sessions.</span></span>
- <span data-ttu-id="993a2-208">透過您**建立**和**ALTER**陳述式中的事件工作階段，減少 hello hello 指定的記憶體數量**MAX\_記憶體**子句。</span><span class="sxs-lookup"><span data-stu-id="993a2-208">Through your **CREATE** and **ALTER** statements for event sessions, reduce hello amount of memory you specify on hello **MAX\_MEMORY** clause.</span></span>

### <a name="network-latency"></a><span data-ttu-id="993a2-209">網路延遲</span><span class="sxs-lookup"><span data-stu-id="993a2-209">Network latency</span></span>

<span data-ttu-id="993a2-210">hello**事件檔案**目標可能會遇到網路延遲或儲存體 blob 的保存資料 tooAzure 時，發生失敗。</span><span class="sxs-lookup"><span data-stu-id="993a2-210">hello **Event File** target might experience network latency or failures while persisting data tooAzure Storage blobs.</span></span> <span data-ttu-id="993a2-211">SQL Database 中的其他事件可能會延遲，等待 hello 網路通訊 toocomplete 而。</span><span class="sxs-lookup"><span data-stu-id="993a2-211">Other events in SQL Database might be delayed while they wait for hello network communication toocomplete.</span></span> <span data-ttu-id="993a2-212">此延遲會降低您的工作負載。</span><span class="sxs-lookup"><span data-stu-id="993a2-212">This delay can slow your workload.</span></span>

- <span data-ttu-id="993a2-213">toomitigate 這種效能風險、 避免設定 hello **EVENT_RETENTION_MODE**太選項**NO_EVENT_LOSS**事件工作階段定義中。</span><span class="sxs-lookup"><span data-stu-id="993a2-213">toomitigate this performance risk, avoid setting hello **EVENT_RETENTION_MODE** option too**NO_EVENT_LOSS** in your event session definitions.</span></span>

## <a name="related-links"></a><span data-ttu-id="993a2-214">相關連結</span><span class="sxs-lookup"><span data-stu-id="993a2-214">Related links</span></span>

- <span data-ttu-id="993a2-215">[搭配 Azure 儲存體使用 Azure PowerShell](../storage/common/storage-powershell-guide-full.md)</span><span class="sxs-lookup"><span data-stu-id="993a2-215">[Using Azure PowerShell with Azure Storage](../storage/common/storage-powershell-guide-full.md).</span></span>
- [<span data-ttu-id="993a2-216">Azure 儲存體 Cmdlet</span><span class="sxs-lookup"><span data-stu-id="993a2-216">Azure Storage Cmdlets</span></span>](http://msdn.microsoft.com/library/dn806401.aspx)
- <span data-ttu-id="993a2-217">[使用 Azure 儲存體的 Azure PowerShell](../storage/common/storage-powershell-guide-full.md) -提供 PowerShell 和 hello Azure 儲存體服務的完整資訊。</span><span class="sxs-lookup"><span data-stu-id="993a2-217">[Using Azure PowerShell with Azure Storage](../storage/common/storage-powershell-guide-full.md) - Provides comprehensive information about PowerShell and hello Azure Storage service.</span></span>
- [<span data-ttu-id="993a2-218">如何 toouse 與.NET 的 Blob 儲存體</span><span class="sxs-lookup"><span data-stu-id="993a2-218">How toouse Blob storage from .NET</span></span>](../storage/blobs/storage-dotnet-how-to-use-blobs.md)
- [<span data-ttu-id="993a2-219">CREATE CREDENTIAL (Transact-SQL)</span><span class="sxs-lookup"><span data-stu-id="993a2-219">CREATE CREDENTIAL (Transact-SQL)</span></span>](http://msdn.microsoft.com/library/ms189522.aspx)
- [<span data-ttu-id="993a2-220">CREATE EVENT SESSION (Transact-SQL)</span><span class="sxs-lookup"><span data-stu-id="993a2-220">CREATE EVENT SESSION (Transact-SQL)</span></span>](http://msdn.microsoft.com/library/bb677289.aspx)
- [<span data-ttu-id="993a2-221">關於 Microsoft SQL Server 中擴充事件的 Jonathan Kehayias 部落格文章</span><span class="sxs-lookup"><span data-stu-id="993a2-221">Jonathan Kehayias' blog posts about extended events in Microsoft SQL Server</span></span>](http://www.sqlskills.com/blogs/jonathan/category/extended-events/)


- <span data-ttu-id="993a2-222">hello Azure*服務更新*網頁，縮小參數 tooAzure SQL 資料庫：</span><span class="sxs-lookup"><span data-stu-id="993a2-222">hello Azure *Service Updates* webpage, narrowed by parameter tooAzure SQL Database:</span></span>
    - [<span data-ttu-id="993a2-223">https://azure.microsoft.com/updates/?service=sql-database</span><span class="sxs-lookup"><span data-stu-id="993a2-223">https://azure.microsoft.com/updates/?service=sql-database</span></span>](https://azure.microsoft.com/updates/?service=sql-database)


<span data-ttu-id="993a2-224">使用下列連結查看 hello 在擴充事件的其他程式碼範例主題。</span><span class="sxs-lookup"><span data-stu-id="993a2-224">Other code sample topics for extended events are available at hello following links.</span></span> <span data-ttu-id="993a2-225">不過，您必須定期檢查任何範例 toosee 是否 hello 範例以 Microsoft SQL Server 與 Azure SQL Database 為目標。</span><span class="sxs-lookup"><span data-stu-id="993a2-225">However, you must routinely check any sample toosee whether hello sample targets Microsoft SQL Server versus Azure SQL Database.</span></span> <span data-ttu-id="993a2-226">然後您可以決定是否需要的 toorun hello 範例次要變更。</span><span class="sxs-lookup"><span data-stu-id="993a2-226">Then you can decide whether minor changes are needed toorun hello sample.</span></span>

<!--
('lock_acquired' event.)

- Code sample for SQL Server: [Determine Which Queries Are Holding Locks](http://msdn.microsoft.com/library/bb677357.aspx)
- Code sample for SQL Server: [Find hello Objects That Have hello Most Locks Taken on Them](http://msdn.microsoft.com/library/bb630355.aspx)
-->
