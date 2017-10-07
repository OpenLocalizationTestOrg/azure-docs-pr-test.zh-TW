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
# <a name="extended-events-in-sql-database"></a>SQL Database 中的擴充事件
[!INCLUDE [sql-database-xevents-selectors-1-include](../../includes/sql-database-xevents-selectors-1-include.md)]

本主題說明如何擴充的事件，Azure SQL Database 中的 hello 實作稍有不同的比較的 tooextended Microsoft SQL Server 中的事件。

- SQL Database V12 獲得 hello hello 擴充的事件功能第二個行事曆 2015年的下半部。
- SQL Server 自 2008 開始即具有擴充事件。
- hello 功能集的 SQL 資料庫上的擴充事件是穩固的 SQL Server 上的 hello 功能子集。

*XEvents* 是非正式暱稱，有時在部落格或其他非正式位置用於「擴充事件」。

如需有關 Azure SQL Database 和 Microsoft SQL Server 之擴充事件的其他資訊，請參閱：

- [Quick Start: Extended events in SQL Server (快速入門：SQL Server 中的擴充事件)](http://msdn.microsoft.com/library/mt733217.aspx)
- [擴充事件](http://msdn.microsoft.com/library/bb630282.aspx)

## <a name="prerequisites"></a>必要條件

本主題假設您已經有一些下列項目的知識：

- [Azure SQL Database 服務](https://azure.microsoft.com/services/sql-database/)。
- [Extended events](http://msdn.microsoft.com/library/bb630282.aspx) 。

- 擴充事件的相關文件的 hello 大量適用於 tooboth SQL Server 和 SQL Database。

先前的曝光 toohello 下列項目時，很有幫助選擇 hello 事件檔案儲存為 hello[目標](#AzureXEventsTargets):

- [Azure 儲存體服務](https://azure.microsoft.com/services/storage/)


- PowerShell
    - [使用 Azure 儲存體的 Azure PowerShell](../storage/common/storage-powershell-guide-full.md) -提供 PowerShell 和 hello Azure 儲存體服務的完整資訊。

## <a name="code-samples"></a>程式碼範例

相關的主題提供兩個程式碼範例：


- [SQL Database 中擴充事件的信號緩衝區目標程式碼](sql-database-xevent-code-ring-buffer.md)
    - 簡短的簡單 Transact-SQL 指令碼。
    - 我們在 hello 程式碼範例主題中，當您完成的信號緩衝區目標之後，您應該釋放其資源執行 卸除 alter 強調`ALTER EVENT SESSION ... ON DATABASE DROP TARGET ...;`陳述式。 稍後您可以藉由 `ALTER EVENT SESSION ... ON DATABASE ADD TARGET ...`，加入信號緩衝區的另一個執行個體。


- [SQL Database 中擴充事件的事件檔案目標程式碼](sql-database-xevent-code-event-file.md)
    - 階段 1 是 PowerShell toocreate Azure 儲存體容器。
    - 階段 2 是使用 hello Azure 儲存體容器的 Transact SQL。

## <a name="transact-sql-differences"></a>Transact-SQL 差異


- 當您執行 hello [CREATE EVENT SESSION](http://msdn.microsoft.com/library/bb677289.aspx)命令在 SQL Server 上使用 hello **ON SERVER**子句。 但您可以在 SQL 資料庫上使用 hello **ON DATABASE**子句改為。


- hello **ON DATABASE**子句也適用於 toohello [ALTER EVENT SESSION](http://msdn.microsoft.com/library/bb630368.aspx)和[DROP EVENT SESSION](http://msdn.microsoft.com/library/bb630257.aspx) TRANSACT-SQL 命令。


- 最佳作法是 tooinclude hello 事件工作階段選項的**STARTUP_STATE = ON**中您**CREATE EVENT SESSION**或**ALTER EVENT SESSION**陳述式。
    - hello **= ON**值支援在 hello 邏輯資料庫，因為 tooa 容錯移轉的重新設定之後自動重新啟動。

## <a name="new-catalog-views"></a>新的目錄檢視

hello 擴充的事件功能支援數個[目錄檢視](http://msdn.microsoft.com/library/ms174365.aspx)。 目錄檢視會告訴您有關*中繼資料或定義*hello 目前資料庫中的使用者建立的事件工作階段。 hello 檢視不會傳回執行個體使用中的事件工作階段的相關資訊。

| 名稱<br/>目錄檢視的名稱 | 說明 |
|:--- |:--- |
| **sys.database_event_session_actions** |針對事件工作階段的每個事件上的每個動作傳回資料列。 |
| **sys.database_event_session_events** |針對事件工作階段中的每個事件傳回資料列。 |
| **sys.database_event_session_fields** |針對已在事件和目標上明確設定的每個可自訂資料行傳回資料列。 |
| **sys.database_event_session_targets** |針對事件工作階段的每個事件目標傳回資料列。 |
| **sys.database_event_sessions** |Hello SQL Database 的資料庫中每個事件工作階段傳回一個資料列。 |

在 Microsoft SQL Server 中，類似的目錄檢視具有包含 .server_\_ 而不是 .database\_ 的名稱。 hello 名稱模式就像是**sys.server_event_%**。

## <a name="new-dynamic-management-views-dmvshttpmsdnmicrosoftcomlibraryms188754aspx"></a>新的動態管理檢視 [(DMV)](http://msdn.microsoft.com/library/ms188754.aspx)

Azure SQL Database 具有支援擴充事件的 [動態管理檢視 (DMV)](http://msdn.microsoft.com/library/bb677293.aspx) 。 DMV 會告訴您 *作用中* 事件工作階段的相關資訊。

| DMV 的名稱 | 說明 |
|:--- |:--- |
| **sys.dm_xe_database_session_event_actions** |會傳回事件工作階段動作的相關資訊。 |
| **sys.dm_xe_database_session_events** |會傳回工作階段事件的相關資訊。 |
| **sys.dm_xe_database_session_object_columns** |顯示 hello 組態值是繫結的 tooa 工作階段物件。 |
| **sys.dm_xe_database_session_targets** |會傳回工作階段目標的相關資訊。 |
| **sys.dm_xe_database_sessions** |傳回一個資料列是已設定領域的 toohello 目前資料庫每個事件工作階段。 |

Microsoft SQL Server，在類似目錄檢視會命名為 hello 不*\_資料庫*hello 一部分名稱，例如：

- **sys.dm_xe_sessions**，而不是<br/>**sys.dm_xe_database_sessions** 名稱。

### <a name="dmvs-common-tooboth"></a>Dmv 常見 tooboth
擴充事件有更多 Dmv 的常見 tooboth Azure SQL Database 和 Microsoft SQL Server:

- **sys.dm_xe_map_values**
- **sys.dm_xe_object_columns**
- **sys.dm_xe_objects**
- **sys.dm_xe_packages**

 <a name="sqlfindseventsactionstargets" id="sqlfindseventsactionstargets"></a>

## <a name="find-hello-available-extended-events-actions-and-targets"></a>尋找 hello 可用的擴充的事件、 動作和目標

您可以執行簡單 SQL**選取**tooobtain hello 可用的事件、 動作和目標的清單。

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


<a name="AzureXEventsTargets" id="AzureXEventsTargets"></a> &nbsp;

## <a name="targets-for-your-sql-database-event-sessions"></a>您的 SQL Database 事件工作階段的目標

以下是可以從您的 SQL Database 上的事件工作階段擷取結果的目標：

- [信號緩衝區目標](http://msdn.microsoft.com/library/ff878182.aspx) -在記憶體中簡短保留事件資料。
- [事件計數器目標](http://msdn.microsoft.com/library/ff878025.aspx) -會計算在擴充事件工作階段期間發生的所有事件。
- [事件檔案目標](http://msdn.microsoft.com/library/ff878115.aspx)-寫入完整緩衝區 tooan Azure 儲存體容器。

hello[事件追蹤的 Windows (ETW)](http://msdn.microsoft.com/library/ms751538.aspx)應用程式開發介面不是適用於 SQL Database 上擴充的事件。

## <a name="restrictions"></a>限制

有兩個安全性相關的差異 befitting hello 雲端環境的 SQL 資料庫：

- 擴充的事件是在 hello 單一租用戶隔離模型上所建構。 一個資料庫中的事件工作階段無法從另一個資料庫存取資料或事件。
- 無法發出**CREATE EVENT SESSION** hello 內容中的 hello 的陳述式**主要**資料庫。

## <a name="permission-model"></a>權限模型

您必須擁有**控制項**權限 hello 資料庫 tooissue **CREATE EVENT SESSION**陳述式。 hello 資料庫擁有者 (dbo) 有**控制項**權限。

### <a name="storage-container-authorizations"></a>儲存體容器授權

hello 您產生必須同時指定 Azure 儲存體容器的 SAS 權杖**rwl** hello 權限。 hello **rwl**值會提供下列權限的 hello:

- 讀取
- 寫入
- 列出

## <a name="performance-considerations"></a>效能考量

有大量使用擴充的事件便會累積更多使用中的記憶體，而不是狀況良好的 hello 案例整體系統。 因此 hello Azure SQL Database 系統以動態方式設定，並調整 hello 中可以累積的事件工作階段的記憶體數量的限制。 許多因素而進入 hello 動態計算。

如果您收到錯誤訊息，指出已強制執行記憶體最大值，您可以採取的一些更正動作為：

- 執行較少的並行事件工作階段。
- 透過您**建立**和**ALTER**陳述式中的事件工作階段，減少 hello hello 指定的記憶體數量**MAX\_記憶體**子句。

### <a name="network-latency"></a>網路延遲

hello**事件檔案**目標可能會遇到網路延遲或儲存體 blob 的保存資料 tooAzure 時，發生失敗。 SQL Database 中的其他事件可能會延遲，等待 hello 網路通訊 toocomplete 而。 此延遲會降低您的工作負載。

- toomitigate 這種效能風險、 避免設定 hello **EVENT_RETENTION_MODE**太選項**NO_EVENT_LOSS**事件工作階段定義中。

## <a name="related-links"></a>相關連結

- [搭配 Azure 儲存體使用 Azure PowerShell](../storage/common/storage-powershell-guide-full.md)
- [Azure 儲存體 Cmdlet](http://msdn.microsoft.com/library/dn806401.aspx)
- [使用 Azure 儲存體的 Azure PowerShell](../storage/common/storage-powershell-guide-full.md) -提供 PowerShell 和 hello Azure 儲存體服務的完整資訊。
- [如何 toouse 與.NET 的 Blob 儲存體](../storage/blobs/storage-dotnet-how-to-use-blobs.md)
- [CREATE CREDENTIAL (Transact-SQL)](http://msdn.microsoft.com/library/ms189522.aspx)
- [CREATE EVENT SESSION (Transact-SQL)](http://msdn.microsoft.com/library/bb677289.aspx)
- [關於 Microsoft SQL Server 中擴充事件的 Jonathan Kehayias 部落格文章](http://www.sqlskills.com/blogs/jonathan/category/extended-events/)


- hello Azure*服務更新*網頁，縮小參數 tooAzure SQL 資料庫：
    - [https://azure.microsoft.com/updates/?service=sql-database](https://azure.microsoft.com/updates/?service=sql-database)


使用下列連結查看 hello 在擴充事件的其他程式碼範例主題。 不過，您必須定期檢查任何範例 toosee 是否 hello 範例以 Microsoft SQL Server 與 Azure SQL Database 為目標。 然後您可以決定是否需要的 toorun hello 範例次要變更。

<!--
('lock_acquired' event.)

- Code sample for SQL Server: [Determine Which Queries Are Holding Locks](http://msdn.microsoft.com/library/bb677357.aspx)
- Code sample for SQL Server: [Find hello Objects That Have hello Most Locks Taken on Them](http://msdn.microsoft.com/library/bb630355.aspx)
-->
