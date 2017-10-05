---
title: "SQL Database 中的擴充事件 | Microsoft Docs"
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
ms.openlocfilehash: 7e5da1c32484b0b94d2ad32ead6bb7c28f9744aa
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="extended-events-in-sql-database"></a><span data-ttu-id="abe37-103">SQL Database 中的擴充事件</span><span class="sxs-lookup"><span data-stu-id="abe37-103">Extended events in SQL Database</span></span>
[!INCLUDE [sql-database-xevents-selectors-1-include](../../includes/sql-database-xevents-selectors-1-include.md)]

<span data-ttu-id="abe37-104">本主題說明與 Microsoft SQL server 中的擴充事件相比，Azure SQL Database 中的擴充事件實作有何些微不同。</span><span class="sxs-lookup"><span data-stu-id="abe37-104">This topic explains how the implementation of extended events in Azure SQL Database is slightly different compared to extended events in Microsoft SQL Server.</span></span>

- <span data-ttu-id="abe37-105">SQL Database V12 在 2015 年行事曆下半年度獲得擴充事件功能。</span><span class="sxs-lookup"><span data-stu-id="abe37-105">SQL Database V12 gained the extended events feature in the second half of calendar 2015.</span></span>
- <span data-ttu-id="abe37-106">SQL Server 自 2008 開始即具有擴充事件。</span><span class="sxs-lookup"><span data-stu-id="abe37-106">SQL Server has had extended events since 2008.</span></span>
- <span data-ttu-id="abe37-107">SQL Database 上的擴充事件功能集是強大的 SQL Server 功能子集。</span><span class="sxs-lookup"><span data-stu-id="abe37-107">The feature set of extended events on SQL Database is a robust subset of the features on SQL Server.</span></span>

<span data-ttu-id="abe37-108">*XEvents* 是非正式暱稱，有時在部落格或其他非正式位置用於「擴充事件」。</span><span class="sxs-lookup"><span data-stu-id="abe37-108">*XEvents* is an informal nickname that is sometimes used for 'extended events' in blogs and other informal locations.</span></span>

<span data-ttu-id="abe37-109">如需有關 Azure SQL Database 和 Microsoft SQL Server 之擴充事件的其他資訊，請參閱：</span><span class="sxs-lookup"><span data-stu-id="abe37-109">Additional information about extended events, for Azure SQL Database and Microsoft SQL Server, is available at:</span></span>

- [<span data-ttu-id="abe37-110">Quick Start: Extended events in SQL Server (快速入門：SQL Server 中的擴充事件)</span><span class="sxs-lookup"><span data-stu-id="abe37-110">Quick Start: Extended events in SQL Server</span></span>](http://msdn.microsoft.com/library/mt733217.aspx)
- [<span data-ttu-id="abe37-111">擴充事件</span><span class="sxs-lookup"><span data-stu-id="abe37-111">Extended Events</span></span>](http://msdn.microsoft.com/library/bb630282.aspx)

## <a name="prerequisites"></a><span data-ttu-id="abe37-112">必要條件</span><span class="sxs-lookup"><span data-stu-id="abe37-112">Prerequisites</span></span>

<span data-ttu-id="abe37-113">本主題假設您已經有一些下列項目的知識：</span><span class="sxs-lookup"><span data-stu-id="abe37-113">This topic assumes you already have some knowledge of:</span></span>

- <span data-ttu-id="abe37-114">[Azure SQL Database 服務](https://azure.microsoft.com/services/sql-database/)。</span><span class="sxs-lookup"><span data-stu-id="abe37-114">[Azure SQL Database service](https://azure.microsoft.com/services/sql-database/).</span></span>
- <span data-ttu-id="abe37-115">[Extended events](http://msdn.microsoft.com/library/bb630282.aspx) 。</span><span class="sxs-lookup"><span data-stu-id="abe37-115">[Extended events](http://msdn.microsoft.com/library/bb630282.aspx) in Microsoft SQL Server.</span></span>

- <span data-ttu-id="abe37-116">我們的大部分文件是關於適用於 SQL Server 和 SQL Database 的擴充事件。</span><span class="sxs-lookup"><span data-stu-id="abe37-116">The bulk of our documentation about extended events applies to both SQL Server and SQL Database.</span></span>

<span data-ttu-id="abe37-117">當選擇事件檔案做為 [目標](#AzureXEventsTargets)時，事先公開下列項目很有幫助：</span><span class="sxs-lookup"><span data-stu-id="abe37-117">Prior exposure to the following items is helpful when choosing the Event File as the [target](#AzureXEventsTargets):</span></span>

- [<span data-ttu-id="abe37-118">Azure 儲存體服務</span><span class="sxs-lookup"><span data-stu-id="abe37-118">Azure Storage service</span></span>](https://azure.microsoft.com/services/storage/)


- <span data-ttu-id="abe37-119">PowerShell</span><span class="sxs-lookup"><span data-stu-id="abe37-119">PowerShell</span></span>
    - <span data-ttu-id="abe37-120">[搭配 Azure 儲存體使用 Azure PowerShell](../storage/common/storage-powershell-guide-full.md) - 提供 PowerShell 和 Azure 儲存體服務的完整資訊。</span><span class="sxs-lookup"><span data-stu-id="abe37-120">[Using Azure PowerShell with Azure Storage](../storage/common/storage-powershell-guide-full.md) - Provides comprehensive information about PowerShell and the Azure Storage service.</span></span>

## <a name="code-samples"></a><span data-ttu-id="abe37-121">程式碼範例</span><span class="sxs-lookup"><span data-stu-id="abe37-121">Code samples</span></span>

<span data-ttu-id="abe37-122">相關的主題提供兩個程式碼範例：</span><span class="sxs-lookup"><span data-stu-id="abe37-122">Related topics provide two code samples:</span></span>


- [<span data-ttu-id="abe37-123">SQL Database 中擴充事件的信號緩衝區目標程式碼</span><span class="sxs-lookup"><span data-stu-id="abe37-123">Ring Buffer target code for extended events in SQL Database</span></span>](sql-database-xevent-code-ring-buffer.md)
    - <span data-ttu-id="abe37-124">簡短的簡單 Transact-SQL 指令碼。</span><span class="sxs-lookup"><span data-stu-id="abe37-124">Short simple Transact-SQL script.</span></span>
    - <span data-ttu-id="abe37-125">我們在程式碼範例主題中強調，當您完成「信號緩衝區」目標的相關作業時，應該執行 alter-drop `ALTER EVENT SESSION ... ON DATABASE DROP TARGET ...;` 陳述式來釋出其資源。</span><span class="sxs-lookup"><span data-stu-id="abe37-125">We emphasize in the code sample topic that, when you are done with a Ring Buffer target, you should release its resources by executing an alter-drop `ALTER EVENT SESSION ... ON DATABASE DROP TARGET ...;` statement.</span></span> <span data-ttu-id="abe37-126">稍後您可以藉由 `ALTER EVENT SESSION ... ON DATABASE ADD TARGET ...`，加入信號緩衝區的另一個執行個體。</span><span class="sxs-lookup"><span data-stu-id="abe37-126">Later you can add another instance of Ring Buffer by `ALTER EVENT SESSION ... ON DATABASE ADD TARGET ...`.</span></span>


- [<span data-ttu-id="abe37-127">SQL Database 中擴充事件的事件檔案目標程式碼</span><span class="sxs-lookup"><span data-stu-id="abe37-127">Event File target code for extended events in SQL Database</span></span>](sql-database-xevent-code-event-file.md)
    - <span data-ttu-id="abe37-128">階段 1 是 PowerShell，建立 Azure 儲存體容器。</span><span class="sxs-lookup"><span data-stu-id="abe37-128">Phase 1 is PowerShell to create an Azure Storage container.</span></span>
    - <span data-ttu-id="abe37-129">階段 2 是 Transact-SQL，使用 Azure 儲存體容器。</span><span class="sxs-lookup"><span data-stu-id="abe37-129">Phase 2 is Transact-SQL that uses the Azure Storage container.</span></span>

## <a name="transact-sql-differences"></a><span data-ttu-id="abe37-130">Transact-SQL 差異</span><span class="sxs-lookup"><span data-stu-id="abe37-130">Transact-SQL differences</span></span>


- <span data-ttu-id="abe37-131">當您在 SQL Server 上執行 [CREATE EVENT SESSION](http://msdn.microsoft.com/library/bb677289.aspx) 命令時，您使用 **ON SERVER** 子句。</span><span class="sxs-lookup"><span data-stu-id="abe37-131">When you execute the [CREATE EVENT SESSION](http://msdn.microsoft.com/library/bb677289.aspx) command on SQL Server, you use the **ON SERVER** clause.</span></span> <span data-ttu-id="abe37-132">但是在 SQL Database 上，您改為使用 **ON DATABASE** 子句。</span><span class="sxs-lookup"><span data-stu-id="abe37-132">But on SQL Database you use the **ON DATABASE** clause instead.</span></span>


- <span data-ttu-id="abe37-133">**ON DATABASE** 子句也適用於 [ALTER EVENT SESSION](http://msdn.microsoft.com/library/bb630368.aspx) 和 [DROP EVENT SESSION](http://msdn.microsoft.com/library/bb630257.aspx) Transact-SQL 命令。</span><span class="sxs-lookup"><span data-stu-id="abe37-133">The **ON DATABASE** clause also applies to the [ALTER EVENT SESSION](http://msdn.microsoft.com/library/bb630368.aspx) and [DROP EVENT SESSION](http://msdn.microsoft.com/library/bb630257.aspx) Transact-SQL commands.</span></span>


- <span data-ttu-id="abe37-134">最佳做法是在您的 **CREATE EVENT SESSION** 或 **ALTER EVENT SESSION** 陳述式中包含 **STARTUP_STATE = ON** 的事件工作階段選項。</span><span class="sxs-lookup"><span data-stu-id="abe37-134">A best practice is to include the event session option of **STARTUP_STATE = ON** in your **CREATE EVENT SESSION**  or **ALTER EVENT SESSION** statements.</span></span>
    - <span data-ttu-id="abe37-135">**= ON** 值支援在由於容錯移轉而進行邏輯資料庫的重新設定之後，自動重新啟動。</span><span class="sxs-lookup"><span data-stu-id="abe37-135">The **= ON** value supports an automatic restart after a reconfiguration of the logical database due to a failover.</span></span>

## <a name="new-catalog-views"></a><span data-ttu-id="abe37-136">新的目錄檢視</span><span class="sxs-lookup"><span data-stu-id="abe37-136">New catalog views</span></span>

<span data-ttu-id="abe37-137">擴充事件功能受到多個 [目錄檢視](http://msdn.microsoft.com/library/ms174365.aspx)支援。</span><span class="sxs-lookup"><span data-stu-id="abe37-137">The extended events feature is supported by several [catalog views](http://msdn.microsoft.com/library/ms174365.aspx).</span></span> <span data-ttu-id="abe37-138">目錄檢視會告訴您目前資料庫中使用者建立事件工作階段的 *中繼資料或定義* 的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="abe37-138">Catalog views tell you about *metadata or definitions* of user-created event sessions in the current database.</span></span> <span data-ttu-id="abe37-139">檢視不會傳回作用中事件工作階段的執行個體的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="abe37-139">The views do not return information about instances of active event sessions.</span></span>

| <span data-ttu-id="abe37-140">名稱</span><span class="sxs-lookup"><span data-stu-id="abe37-140">Name of</span></span><br/><span data-ttu-id="abe37-141">目錄檢視的名稱</span><span class="sxs-lookup"><span data-stu-id="abe37-141">catalog view</span></span> | <span data-ttu-id="abe37-142">說明</span><span class="sxs-lookup"><span data-stu-id="abe37-142">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="abe37-143">**sys.database_event_session_actions**</span><span class="sxs-lookup"><span data-stu-id="abe37-143">**sys.database_event_session_actions**</span></span> |<span data-ttu-id="abe37-144">針對事件工作階段的每個事件上的每個動作傳回資料列。</span><span class="sxs-lookup"><span data-stu-id="abe37-144">Returns a row for each action on each event of an event session.</span></span> |
| <span data-ttu-id="abe37-145">**sys.database_event_session_events**</span><span class="sxs-lookup"><span data-stu-id="abe37-145">**sys.database_event_session_events**</span></span> |<span data-ttu-id="abe37-146">針對事件工作階段中的每個事件傳回資料列。</span><span class="sxs-lookup"><span data-stu-id="abe37-146">Returns a row for each event in an event session.</span></span> |
| <span data-ttu-id="abe37-147">**sys.database_event_session_fields**</span><span class="sxs-lookup"><span data-stu-id="abe37-147">**sys.database_event_session_fields**</span></span> |<span data-ttu-id="abe37-148">針對已在事件和目標上明確設定的每個可自訂資料行傳回資料列。</span><span class="sxs-lookup"><span data-stu-id="abe37-148">Returns a row for each customize-able column that was explicitly set on events and targets.</span></span> |
| <span data-ttu-id="abe37-149">**sys.database_event_session_targets**</span><span class="sxs-lookup"><span data-stu-id="abe37-149">**sys.database_event_session_targets**</span></span> |<span data-ttu-id="abe37-150">針對事件工作階段的每個事件目標傳回資料列。</span><span class="sxs-lookup"><span data-stu-id="abe37-150">Returns a row for each event target for an event session.</span></span> |
| <span data-ttu-id="abe37-151">**sys.database_event_sessions**</span><span class="sxs-lookup"><span data-stu-id="abe37-151">**sys.database_event_sessions**</span></span> |<span data-ttu-id="abe37-152">針對 SQL Database 資料庫中的每個事件工作階段傳回資料列。</span><span class="sxs-lookup"><span data-stu-id="abe37-152">Returns a row for each event session in the SQL Database database.</span></span> |

<span data-ttu-id="abe37-153">在 Microsoft SQL Server 中，類似的目錄檢視具有包含 .server_\_ 而不是 .database\_ 的名稱。</span><span class="sxs-lookup"><span data-stu-id="abe37-153">In Microsoft SQL Server, similar catalog views have names that include *.server\_* instead of *.database\_*.</span></span> <span data-ttu-id="abe37-154">名稱模式類似 **sys.server_event_%**。</span><span class="sxs-lookup"><span data-stu-id="abe37-154">The name pattern is like **sys.server_event_%**.</span></span>

## <a name="new-dynamic-management-views-dmvshttpmsdnmicrosoftcomlibraryms188754aspx"></a><span data-ttu-id="abe37-155">新的動態管理檢視 [(DMV)](http://msdn.microsoft.com/library/ms188754.aspx)</span><span class="sxs-lookup"><span data-stu-id="abe37-155">New dynamic management views [(DMVs)](http://msdn.microsoft.com/library/ms188754.aspx)</span></span>

<span data-ttu-id="abe37-156">Azure SQL Database 具有支援擴充事件的 [動態管理檢視 (DMV)](http://msdn.microsoft.com/library/bb677293.aspx) 。</span><span class="sxs-lookup"><span data-stu-id="abe37-156">Azure SQL Database has [dynamic management views (DMVs)](http://msdn.microsoft.com/library/bb677293.aspx) that support extended events.</span></span> <span data-ttu-id="abe37-157">DMV 會告訴您 *作用中* 事件工作階段的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="abe37-157">DMVs tell you about *active* event sessions.</span></span>

| <span data-ttu-id="abe37-158">DMV 的名稱</span><span class="sxs-lookup"><span data-stu-id="abe37-158">Name of DMV</span></span> | <span data-ttu-id="abe37-159">說明</span><span class="sxs-lookup"><span data-stu-id="abe37-159">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="abe37-160">**sys.dm_xe_database_session_event_actions**</span><span class="sxs-lookup"><span data-stu-id="abe37-160">**sys.dm_xe_database_session_event_actions**</span></span> |<span data-ttu-id="abe37-161">會傳回事件工作階段動作的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="abe37-161">Returns information about event session actions.</span></span> |
| <span data-ttu-id="abe37-162">**sys.dm_xe_database_session_events**</span><span class="sxs-lookup"><span data-stu-id="abe37-162">**sys.dm_xe_database_session_events**</span></span> |<span data-ttu-id="abe37-163">會傳回工作階段事件的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="abe37-163">Returns information about session events.</span></span> |
| <span data-ttu-id="abe37-164">**sys.dm_xe_database_session_object_columns**</span><span class="sxs-lookup"><span data-stu-id="abe37-164">**sys.dm_xe_database_session_object_columns**</span></span> |<span data-ttu-id="abe37-165">顯示繫結至工作階段的物件的組態值。</span><span class="sxs-lookup"><span data-stu-id="abe37-165">Shows the configuration values for objects that are bound to a session.</span></span> |
| <span data-ttu-id="abe37-166">**sys.dm_xe_database_session_targets**</span><span class="sxs-lookup"><span data-stu-id="abe37-166">**sys.dm_xe_database_session_targets**</span></span> |<span data-ttu-id="abe37-167">會傳回工作階段目標的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="abe37-167">Returns information about session targets.</span></span> |
| <span data-ttu-id="abe37-168">**sys.dm_xe_database_sessions**</span><span class="sxs-lookup"><span data-stu-id="abe37-168">**sys.dm_xe_database_sessions**</span></span> |<span data-ttu-id="abe37-169">針對範圍為目前資料庫的每個事件工作階段傳回資料列。</span><span class="sxs-lookup"><span data-stu-id="abe37-169">Returns a row for each event session that is scoped to the current database.</span></span> |

<span data-ttu-id="abe37-170">在 Microsoft SQL Server 中，類似的目錄檢視名稱不含 *database\_* 名稱部分，例如：</span><span class="sxs-lookup"><span data-stu-id="abe37-170">In Microsoft SQL Server, similar catalog views are named without the *\_database* portion of the name, such as:</span></span>

- <span data-ttu-id="abe37-171">**sys.dm_xe_sessions**，而不是</span><span class="sxs-lookup"><span data-stu-id="abe37-171">**sys.dm_xe_sessions**, instead of name</span></span><br/><span data-ttu-id="abe37-172">**sys.dm_xe_database_sessions** 名稱。</span><span class="sxs-lookup"><span data-stu-id="abe37-172">**sys.dm_xe_database_sessions**.</span></span>

### <a name="dmvs-common-to-both"></a><span data-ttu-id="abe37-173">兩者通用的 DMV</span><span class="sxs-lookup"><span data-stu-id="abe37-173">DMVs common to both</span></span>
<span data-ttu-id="abe37-174">對於擴充事件，有通用於 Azure SQL Database 和 Microsoft SQL Server 的其他 DMV：</span><span class="sxs-lookup"><span data-stu-id="abe37-174">For extended events there are additional DMVs that are common to both Azure SQL Database and Microsoft SQL Server:</span></span>

- <span data-ttu-id="abe37-175">**sys.dm_xe_map_values**</span><span class="sxs-lookup"><span data-stu-id="abe37-175">**sys.dm_xe_map_values**</span></span>
- <span data-ttu-id="abe37-176">**sys.dm_xe_object_columns**</span><span class="sxs-lookup"><span data-stu-id="abe37-176">**sys.dm_xe_object_columns**</span></span>
- <span data-ttu-id="abe37-177">**sys.dm_xe_objects**</span><span class="sxs-lookup"><span data-stu-id="abe37-177">**sys.dm_xe_objects**</span></span>
- <span data-ttu-id="abe37-178">**sys.dm_xe_packages**</span><span class="sxs-lookup"><span data-stu-id="abe37-178">**sys.dm_xe_packages**</span></span>

 <a name="sqlfindseventsactionstargets" id="sqlfindseventsactionstargets"></a>

## <a name="find-the-available-extended-events-actions-and-targets"></a><span data-ttu-id="abe37-179">尋找可用擴充事件、動作和目標</span><span class="sxs-lookup"><span data-stu-id="abe37-179">Find the available extended events, actions, and targets</span></span>

<span data-ttu-id="abe37-180">您可以執行簡單 SQL **SELECT** 以取得可用事件、動作和目標的清單。</span><span class="sxs-lookup"><span data-stu-id="abe37-180">You can run a simple SQL **SELECT** to obtain a list of the available events, actions, and target.</span></span>

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


<span data-ttu-id="abe37-181"><a name="AzureXEventsTargets" id="AzureXEventsTargets"></a> &nbsp;</span><span class="sxs-lookup"><span data-stu-id="abe37-181"><a name="AzureXEventsTargets" id="AzureXEventsTargets"></a> &nbsp;</span></span>

## <a name="targets-for-your-sql-database-event-sessions"></a><span data-ttu-id="abe37-182">您的 SQL Database 事件工作階段的目標</span><span class="sxs-lookup"><span data-stu-id="abe37-182">Targets for your SQL Database event sessions</span></span>

<span data-ttu-id="abe37-183">以下是可以從您的 SQL Database 上的事件工作階段擷取結果的目標：</span><span class="sxs-lookup"><span data-stu-id="abe37-183">Here are targets that can capture results from your event sessions on SQL Database:</span></span>

- <span data-ttu-id="abe37-184">[信號緩衝區目標](http://msdn.microsoft.com/library/ff878182.aspx) -在記憶體中簡短保留事件資料。</span><span class="sxs-lookup"><span data-stu-id="abe37-184">[Ring Buffer target](http://msdn.microsoft.com/library/ff878182.aspx) - Briefly holds event data in memory.</span></span>
- <span data-ttu-id="abe37-185">[事件計數器目標](http://msdn.microsoft.com/library/ff878025.aspx) -會計算在擴充事件工作階段期間發生的所有事件。</span><span class="sxs-lookup"><span data-stu-id="abe37-185">[Event Counter target](http://msdn.microsoft.com/library/ff878025.aspx) - Counts all events that occur during an extended events session.</span></span>
- <span data-ttu-id="abe37-186">[事件檔案目標](http://msdn.microsoft.com/library/ff878115.aspx) - 會將完整緩衝區寫入 Azure 儲存體容器。</span><span class="sxs-lookup"><span data-stu-id="abe37-186">[Event File target](http://msdn.microsoft.com/library/ff878115.aspx) - Writes complete buffers to an Azure Storage container.</span></span>

<span data-ttu-id="abe37-187">[Windows 事件追蹤 (ETW)](http://msdn.microsoft.com/library/ms751538.aspx) API 不適用於 SQL Database 上的擴充事件。</span><span class="sxs-lookup"><span data-stu-id="abe37-187">The [Event Tracing for Windows (ETW)](http://msdn.microsoft.com/library/ms751538.aspx) API is not available for extended events on SQL Database.</span></span>

## <a name="restrictions"></a><span data-ttu-id="abe37-188">限制</span><span class="sxs-lookup"><span data-stu-id="abe37-188">Restrictions</span></span>

<span data-ttu-id="abe37-189">有幾個適用於 SQL Database 雲端環境的安全性相關差異：</span><span class="sxs-lookup"><span data-stu-id="abe37-189">There are a couple of security-related differences befitting the cloud environment of SQL Database:</span></span>

- <span data-ttu-id="abe37-190">擴充事件是建構在單一租用戶隔離模型的基礎上。</span><span class="sxs-lookup"><span data-stu-id="abe37-190">Extended events are founded on the single-tenant isolation model.</span></span> <span data-ttu-id="abe37-191">一個資料庫中的事件工作階段無法從另一個資料庫存取資料或事件。</span><span class="sxs-lookup"><span data-stu-id="abe37-191">An event session in one database cannot access data or events from another database.</span></span>
- <span data-ttu-id="abe37-192">無法在 **master** 資料庫的內容中發出 **CREATE EVENT SESSION** 陳述式。</span><span class="sxs-lookup"><span data-stu-id="abe37-192">You cannot issue a **CREATE EVENT SESSION** statement in the context of the **master** database.</span></span>

## <a name="permission-model"></a><span data-ttu-id="abe37-193">權限模型</span><span class="sxs-lookup"><span data-stu-id="abe37-193">Permission model</span></span>

<span data-ttu-id="abe37-194">您必須擁有資料庫的**控制**權限，才能發出 **CREATE EVENT SESSION** 陳述式。</span><span class="sxs-lookup"><span data-stu-id="abe37-194">You must have **Control** permission on the database to issue a **CREATE EVENT SESSION** statement.</span></span> <span data-ttu-id="abe37-195">資料庫擁有者 (dbo) 有 **控制** 權限。</span><span class="sxs-lookup"><span data-stu-id="abe37-195">The database owner (dbo) has **Control** permission.</span></span>

### <a name="storage-container-authorizations"></a><span data-ttu-id="abe37-196">儲存體容器授權</span><span class="sxs-lookup"><span data-stu-id="abe37-196">Storage container authorizations</span></span>

<span data-ttu-id="abe37-197">您針對 Azure 儲存體容器產生的 SAS 權杖必須指定權限的 **rwl** 。</span><span class="sxs-lookup"><span data-stu-id="abe37-197">The SAS token you generate for your Azure Storage container must specify **rwl** for the permissions.</span></span> <span data-ttu-id="abe37-198">**rwl** 值會提供下列權限：</span><span class="sxs-lookup"><span data-stu-id="abe37-198">The **rwl** value provides the following permissions:</span></span>

- <span data-ttu-id="abe37-199">讀取</span><span class="sxs-lookup"><span data-stu-id="abe37-199">Read</span></span>
- <span data-ttu-id="abe37-200">寫入</span><span class="sxs-lookup"><span data-stu-id="abe37-200">Write</span></span>
- <span data-ttu-id="abe37-201">列出</span><span class="sxs-lookup"><span data-stu-id="abe37-201">List</span></span>

## <a name="performance-considerations"></a><span data-ttu-id="abe37-202">效能考量</span><span class="sxs-lookup"><span data-stu-id="abe37-202">Performance considerations</span></span>

<span data-ttu-id="abe37-203">有大量使用擴充事件會累積超出整體系統狀況良好所允許的更多作用中記憶體的案例。</span><span class="sxs-lookup"><span data-stu-id="abe37-203">There are scenarios where intensive use of extended events can accumulate more active memory than is healthy for the overall system.</span></span> <span data-ttu-id="abe37-204">因此，Azure SQL Database 系統動態設定和調整事件工作階段可以累積的作用中記憶體數量的限制。</span><span class="sxs-lookup"><span data-stu-id="abe37-204">Therefore the Azure SQL Database system dynamically sets and adjusts limits on the amount of active memory that can be accumulated by an event session.</span></span> <span data-ttu-id="abe37-205">許多因素會列入動態計算。</span><span class="sxs-lookup"><span data-stu-id="abe37-205">Many factors go into the dynamic calculation.</span></span>

<span data-ttu-id="abe37-206">如果您收到錯誤訊息，指出已強制執行記憶體最大值，您可以採取的一些更正動作為：</span><span class="sxs-lookup"><span data-stu-id="abe37-206">If you receive an error message that says a memory maximum was enforced, some corrective actions you can take are:</span></span>

- <span data-ttu-id="abe37-207">執行較少的並行事件工作階段。</span><span class="sxs-lookup"><span data-stu-id="abe37-207">Run fewer concurrent event sessions.</span></span>
- <span data-ttu-id="abe37-208">透過您對於事件工作階段的 **CREATE** 和 **ALTER** 陳述式，減少您在 **MAX\_MEMORY** 子句中指定的記憶體數量。</span><span class="sxs-lookup"><span data-stu-id="abe37-208">Through your **CREATE** and **ALTER** statements for event sessions, reduce the amount of memory you specify on the **MAX\_MEMORY** clause.</span></span>

### <a name="network-latency"></a><span data-ttu-id="abe37-209">網路延遲</span><span class="sxs-lookup"><span data-stu-id="abe37-209">Network latency</span></span>

<span data-ttu-id="abe37-210">**事件檔案** 目標在將資料保存到 Azure 儲存體 Blob 時可能會遇到網路延遲或失敗。</span><span class="sxs-lookup"><span data-stu-id="abe37-210">The **Event File** target might experience network latency or failures while persisting data to Azure Storage blobs.</span></span> <span data-ttu-id="abe37-211">SQL Database 中的其他事件可能會延遲，因為它們會等待網路通訊完成。</span><span class="sxs-lookup"><span data-stu-id="abe37-211">Other events in SQL Database might be delayed while they wait for the network communication to complete.</span></span> <span data-ttu-id="abe37-212">此延遲會降低您的工作負載。</span><span class="sxs-lookup"><span data-stu-id="abe37-212">This delay can slow your workload.</span></span>

- <span data-ttu-id="abe37-213">若要減輕這個效能風險，請避免在您的事件工作階段定義中將 **EVENT_RETENTION_MODE** 選項設為 **NO_EVENT_LOSS**。</span><span class="sxs-lookup"><span data-stu-id="abe37-213">To mitigate this performance risk, avoid setting the **EVENT_RETENTION_MODE** option to **NO_EVENT_LOSS** in your event session definitions.</span></span>

## <a name="related-links"></a><span data-ttu-id="abe37-214">相關連結</span><span class="sxs-lookup"><span data-stu-id="abe37-214">Related links</span></span>

- <span data-ttu-id="abe37-215">[搭配 Azure 儲存體使用 Azure PowerShell](../storage/common/storage-powershell-guide-full.md)</span><span class="sxs-lookup"><span data-stu-id="abe37-215">[Using Azure PowerShell with Azure Storage](../storage/common/storage-powershell-guide-full.md).</span></span>
- [<span data-ttu-id="abe37-216">Azure 儲存體 Cmdlet</span><span class="sxs-lookup"><span data-stu-id="abe37-216">Azure Storage Cmdlets</span></span>](http://msdn.microsoft.com/library/dn806401.aspx)
- <span data-ttu-id="abe37-217">[搭配 Azure 儲存體使用 Azure PowerShell](../storage/common/storage-powershell-guide-full.md) - 提供 PowerShell 和 Azure 儲存體服務的完整資訊。</span><span class="sxs-lookup"><span data-stu-id="abe37-217">[Using Azure PowerShell with Azure Storage](../storage/common/storage-powershell-guide-full.md) - Provides comprehensive information about PowerShell and the Azure Storage service.</span></span>
- [<span data-ttu-id="abe37-218">如何使用 .NET 的 Blob 儲存體</span><span class="sxs-lookup"><span data-stu-id="abe37-218">How to use Blob storage from .NET</span></span>](../storage/blobs/storage-dotnet-how-to-use-blobs.md)
- [<span data-ttu-id="abe37-219">CREATE CREDENTIAL (Transact-SQL)</span><span class="sxs-lookup"><span data-stu-id="abe37-219">CREATE CREDENTIAL (Transact-SQL)</span></span>](http://msdn.microsoft.com/library/ms189522.aspx)
- [<span data-ttu-id="abe37-220">CREATE EVENT SESSION (Transact-SQL)</span><span class="sxs-lookup"><span data-stu-id="abe37-220">CREATE EVENT SESSION (Transact-SQL)</span></span>](http://msdn.microsoft.com/library/bb677289.aspx)
- [<span data-ttu-id="abe37-221">關於 Microsoft SQL Server 中擴充事件的 Jonathan Kehayias 部落格文章</span><span class="sxs-lookup"><span data-stu-id="abe37-221">Jonathan Kehayias' blog posts about extended events in Microsoft SQL Server</span></span>](http://www.sqlskills.com/blogs/jonathan/category/extended-events/)


- <span data-ttu-id="abe37-222">Azure *服務更新*網頁，已透過參數將範圍縮小為 Azure SQL Database：</span><span class="sxs-lookup"><span data-stu-id="abe37-222">The Azure *Service Updates* webpage, narrowed by parameter to Azure SQL Database:</span></span>
    - [<span data-ttu-id="abe37-223">https://azure.microsoft.com/updates/?service=sql-database</span><span class="sxs-lookup"><span data-stu-id="abe37-223">https://azure.microsoft.com/updates/?service=sql-database</span></span>](https://azure.microsoft.com/updates/?service=sql-database)


<span data-ttu-id="abe37-224">下列連結提供擴充事件的其他程式碼範例主題。</span><span class="sxs-lookup"><span data-stu-id="abe37-224">Other code sample topics for extended events are available at the following links.</span></span> <span data-ttu-id="abe37-225">不過，您必須定期檢查所有範例以查看範例是否適用於 Microsoft SQL Server 與 Azure SQL Database。</span><span class="sxs-lookup"><span data-stu-id="abe37-225">However, you must routinely check any sample to see whether the sample targets Microsoft SQL Server versus Azure SQL Database.</span></span> <span data-ttu-id="abe37-226">然後您可以決定是否需要稍加變更來執行範例。</span><span class="sxs-lookup"><span data-stu-id="abe37-226">Then you can decide whether minor changes are needed to run the sample.</span></span>

<!--
('lock_acquired' event.)

- Code sample for SQL Server: [Determine Which Queries Are Holding Locks](http://msdn.microsoft.com/library/bb677357.aspx)
- Code sample for SQL Server: [Find the Objects That Have the Most Locks Taken on Them](http://msdn.microsoft.com/library/bb630355.aspx)
-->
