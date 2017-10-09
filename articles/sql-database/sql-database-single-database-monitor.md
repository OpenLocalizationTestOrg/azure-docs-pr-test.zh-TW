---
title: "Azure SQL Database 中的 aaaMonitoring 資料庫效能 |Microsoft 文件"
description: "深入了解 hello 選項來監視您的 Azure 工具和動態管理檢視的資料庫。"
keywords: "資料庫監視, 雲端資料庫效能"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: a2e47475-c955-4a8d-a65c-cbef9a6d9b9f
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 01/10/2017
ms.author: carlrab
ms.openlocfilehash: b13771183d4ccf37f58e2fc518b9b14de38212dc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="monitoring-database-performance-in-azure-sql-database"></a>監視 Azure SQL Database 中的資料庫效能
監視 Azure 中的 SQL 資料庫的效能，hello 開頭監視 hello 資源使用率相對 toohello 等級您選擇的資料庫效能。 監視可協助您判斷您的資料庫具有過多的容量或時發生問題，因為已超過資源，並決定是否時間 tooadjust hello 效能層級和[服務層](sql-database-service-tiers.md)您的資料庫。 您可以監視您的資料庫使用圖形化工具中 hello [Azure 入口網站](https://portal.azure.com)或使用 SQL[動態管理檢視](https://msdn.microsoft.com/library/ms188754.aspx)。

## <a name="monitor-databases-using-hello-azure-portal"></a>監視使用 hello Azure 入口網站的資料庫
在 hello [Azure 入口網站](https://portal.azure.com/)，您可以監視單一資料庫的使用率選取您的資料庫，然後按一下 hello**監視**圖表。 這會開啟**度量**視窗中，您可以按一下 hello**編輯圖表** 按鈕。 新增下列度量的 hello:

* CPU 百分比
* DTU 百分比
* 資料 IO 百分比
* 資料庫大小百分比

一旦您已經新增這些度量，您可以繼續 tooview 中 hello**監視**hello 上更多詳細資料圖表**度量**視窗。 所有四個度量顯示 hello 平均使用率百分比相對 toohello **DTU**您的資料庫。 請參閱 hello[服務層](sql-database-service-tiers.md)Dtu 的詳細資料的發行項。

![資料庫效能的服務層監視。](./media/sql-database-service-tiers/sqldb_service_tier_monitoring.png)

您也可以在 hello 效能度量上設定警示。 按一下 hello**新增警示**按鈕在 hello**度量**視窗。 請遵循 hello 精靈 tooconfigure 您的警示。 您擁有 hello 選項 tooalert hello 度量超出某個臨界值時，或 hello 低於特定臨界值。

例如，如果您預期資料庫 toogrow hello 工作負載，您可以選擇 tooconfigure 電子郵件警示每當資料庫達到 80%時任何 hello 效能計量。 您可以使用這個早期的警告 toofigure out 時，您可能必須 tooswitch toohello 下一個較高的效能層級。

hello 效能度量也可協助您判斷您是否能 toodowngrade tooa 低效能層級。 假設您使用標準 S2 」 資料庫，而平均 hello 資料庫的所有效能度量顯示不都使用任何給定的時間超過 10%。 很可能標準 S1 中的 hello 資料庫運作。 不過，請注意暴增或波動之前 hello 決策 toomove tooa 低效能層級的工作負載。

## <a name="monitor-databases-using-dmvs"></a>使用 DMV 監視資料庫
hello hello 入口網站中公開的相同度量也會提供透過系統檢視表： [sys.resource_stats](https://msdn.microsoft.com/library/dn269979.aspx) hello 邏輯中**主要**您伺服器的資料庫和[sys.dm_db_resource_stats](https://msdn.microsoft.com/library/dn800981.aspx) hello 使用者資料庫中。 使用**sys.resource_stats**如果您需要更精細的資料少 toomonitor 長的時間。 使用**sys.dm_db_resource_stats**如果您需要 toomonitor 較精細的資料較小的時間範圍內。 如需詳細資訊，請參閱 [Azure SQL Database 效能指引](sql-database-single-database-monitor.md#monitor-resource-use)。

> [!NOTE]
> 使用於 Web 和 Business Edition 資料庫 (已淘汰) 時，**sys.dm_db_resource_stats** 會傳回空的結果集。
>
>

### <a name="monitor-resource-use"></a>監視資源使用量

您可以使用 [SQL Database 查詢效能深入解析](sql-database-query-performance.md)和[查詢存放區](https://msdn.microsoft.com/library/dn817826.aspx)來監視資源用量。

您也可以使用以下兩種檢視來監視用量：

* [sys.dm_db_resource_stats](https://msdn.microsoft.com/library/dn800981.aspx)
* [sys.resource_stats](https://msdn.microsoft.com/library/dn269979.aspx)

#### <a name="sysdmdbresourcestats"></a>sys.dm_db_resource_stats
您可以使用 hello [sys.dm_db_resource_stats](https://msdn.microsoft.com/library/dn800981.aspx)每個 SQL database 中的檢視。 hello **sys.dm_db_resource_stats**檢視會顯示最近資源使用資料相對 toohello 服務層。 每隔 15 秒鐘就會記錄一次 CPU、資料 I/O、記錄檔寫入和記憶體的平均百分比，並且會維持 1 小時。

因為此檢視會提供更細微的資源使用量資訊，請先使用 **sys.dm_db_resource_stats** 來進行任何現狀分析或疑難排解。 比方說，此查詢會顯示 hello 平均值和最大資源用於 hello 目前資料庫上 hello 過去一小時：

    SELECT  
        AVG(avg_cpu_percent) AS 'Average CPU use in percent',
        MAX(avg_cpu_percent) AS 'Maximum CPU use in percent',
        AVG(avg_data_io_percent) AS 'Average data I/O in percent',
        MAX(avg_data_io_percent) AS 'Maximum data I/O in percent',
        AVG(avg_log_write_percent) AS 'Average log write use in percent',
        MAX(avg_log_write_percent) AS 'Maximum log write use in percent',
        AVG(avg_memory_usage_percent) AS 'Average memory use in percent',
        MAX(avg_memory_usage_percent) AS 'Maximum memory use in percent'
    FROM sys.dm_db_resource_stats;  

其他查詢，請參閱中的 hello 範例[sys.dm_db_resource_stats](https://msdn.microsoft.com/library/dn800981.aspx)。

#### <a name="sysresourcestats"></a>sys.resource_stats
hello [sys.resource_stats](https://msdn.microsoft.com/library/dn269979.aspx)  檢視中 hello**主要**資料庫具有可協助您監視您的 SQL database 在其特定的服務層和效能層級的 hello 效能的其他資訊. hello 資料會收集每隔 5 分鐘，並維護的大約可返回 35 天。 這個檢視適合用於進行 SQL Database 如何使用資源的長期歷史分析。

hello 下圖顯示 hello CPU 資源的使用以 hello P2 效能層級的 Premium 資料庫的每個小時一週。 下圖從星期一開始，顯示 5 個工作日，然後才顯示週末，當多小於 hello 應用程式上發生的狀況。

![SQL Database 的資源使用量](./media/sql-database-performance-guidance/sql_db_resource_utilization.png)

Hello 資料從這個資料庫目前的尖峰 CPU 負載剛好超過 50%的 CPU 使用相對 toohello P2 效能層級 （星期二中午）。 如果 CPU 是 hello 應用程式的資源設定檔中的 hello 主控項因素，您可能決定 P2 是右邊一律 hello 工作負載的效能層級 tooguarantee 符合 hello。 如果您預期應用程式 toogrow 經過一段時間，它是個不錯的主意 toohave 額外的資源緩衝，如此 hello 應用程式不會達到 hello 效能層級限制也一樣。 如果您增加 hello 效能層級，您可以協助避免客戶可見錯誤時資料庫沒有足夠的電力 tooprocess 要求有效，尤其是在延遲的環境可能會發生。 例如，資料庫可支援繪製根據資料庫呼叫 hello 結果的網頁應用程式。

其他應用程式類型可能解譯的 hello 相同圖形以不同的方式。 例如，如果應用程式嘗試 tooprocess 薪資資料每一天，而且具有 hello 相同的圖表，這種 「 批次作業 」 模型可能會正常執行 P1 效能層級。 hello P1 效能層級在 hello P2 效能層級有 100 Dtu 比較 too200 Dtu。 hello P1 效能層級提供 hello P2 效能層級的一半 hello 的效能。 因此，P2 中 50% 的 CPU 使用量等於 P1 中 100% 的 CPU 使用量。 如果 hello 應用程式沒有逾時，它可能不重要如果作業需要 2 小時或 2.5 個小時 toofinish 如果今天。 這個類別中的應用程式或許可以使用 P1 效能等級。 您可以利用 hello 事實是 hello 天資源使用量較低，使任何 「 高尖峰 」 可能會 「 溢出 」 的一個低谷 hello hello 天中稍後的時段。 只要 hello 作業可以在每日時間完成，可能適合使用該類型的應用程式，儲存金錢 hello P1 效能層級。

Azure SQL Database 會公開使用的資源資訊中每個作用中資料庫 hello **sys.resource_stats**檢視 hello**主要**每一部伺服器中的資料庫。 hello 資料表中的 hello 資料會彙總每隔 5 分鐘。 Hello Basic、 Standard 和 Premium 服務層時，hello 資料可能要花超過 5 分鐘 tooappear hello 資料表中，因此這項資料是歷程分析，而不是接近即時的分析更有用。 查詢 hello **sys.resource_stats** toosee hello 最近的資料庫和 toovalidate hello 保留您選擇傳送您想要在需要時 hello 效能歷程的檢視。

> [!NOTE]
> 您必須是連接的 toohello**主要**資料庫的邏輯的 SQL 資料庫伺服器 tooquery **sys.resource_stats** hello 遵循範例中。
> 
> 

此範例將示範如何將這個檢視中的 hello 資料會公開：

    SELECT TOP 10 *
    FROM sys.resource_stats
    WHERE database_name = 'resource1'
    ORDER BY start_time DESC

![hello sys.resource_stats 目錄檢視](./media/sql-database-performance-guidance/sys_resource_stats.png)

hello 下一個範例將示範不同的方式，您可以使用 hello **sys.resource_stats**目錄檢視有關您的 SQL 資料庫使用資源的方式 tooget 資訊：

1. 在過去一週的資源 hello toolook hello 資料庫 userdb1 使用，您可以執行這個查詢：
   
        SELECT *
        FROM sys.resource_stats
        WHERE database_name = 'userdb1' AND
              start_time > DATEADD(day, -7, GETDATE())
        ORDER BY start_time DESC;
2. tooevaluate 方式以及您的工作負載符合 hello 效能層級，您需要 toodrill 向下到 hello 資源度量的每個層面： CPU、 讀取、 寫入、 背景工作數目和工作階段數目。 以下是一個修訂過查詢使用**sys.resource_stats** tooreport hello 這些資源度量的平均值和最大值：
   
        SELECT
            avg(avg_cpu_percent) AS 'Average CPU use in percent',
            max(avg_cpu_percent) AS 'Maximum CPU use in percent',
            avg(avg_data_io_percent) AS 'Average physical data I/O use in percent',
            max(avg_data_io_percent) AS 'Maximum physical data I/O use in percent',
            avg(avg_log_write_percent) AS 'Average log write use in percent',
            max(avg_log_write_percent) AS 'Maximum log write use in percent',
            avg(max_session_percent) AS 'Average % of sessions',
            max(max_session_percent) AS 'Maximum % of sessions',
            avg(max_worker_percent) AS 'Average % of workers',
            max(max_worker_percent) AS 'Maximum % of workers'
        FROM sys.resource_stats
        WHERE database_name = 'userdb1' AND start_time > DATEADD(day, -7, GETDATE());
3. 使用各項資源度量的這個 hello 平均值和最大值相關的資訊，您可以評估您的工作負載符合您選擇的 hello 效能層級的程度。 通常，平均值從**sys.resource_stats**可讓您針對 hello 目標大小的理想基準 toouse。 它應該是您主要的量尺。 如需範例，您可能使用 hello Standard 服務層搭配 S2 效能層級。 hello 平均使用百分比的 CPU 和 I/O 讀取和寫入為 40%下方、 hello 平均背景工作數目低於 50，和 hello 平均工作階段數目低於 200。 您的工作負載可能符合 S1 效能層級 hello。 是，並輕鬆 toosee hello 背景工作和工作階段限制納入您的資料庫。 toosee tooCPU、 讀取和寫入時，資料庫是否符合較低的效能層級與目前 hello hello 較低效能層級的 DTU 數字除以 hello 目前的效能層級的 DTU 數目，然後再乘 100 hello 結果：
   
    **S1 DTU / S2 DTU * 100 = 20 / 50 * 100 = 40**
   
    hello 結果為 hello hello 兩個效能層級之間以百分比為單位的相對效能差異。 如果資源使用不超過此數量時，您的工作負載可能符合較低效能層級 hello。 不過，您需要的資源使用的值，所有範圍 toolook，並判斷您的資料庫工作負載會放入 hello 低效能層級的頻率，請依百分比。 hello 下列查詢會輸出 hello 適合每一資源維度，根據我們在此範例中計算出的 40%的 hello 臨界值百分比：
   
        SELECT
            (COUNT(database_name) - SUM(CASE WHEN avg_cpu_percent >= 40 THEN 1 ELSE 0 END) * 1.0) / COUNT(database_name) AS 'CPU Fit Percent'
            ,(COUNT(database_name) - SUM(CASE WHEN avg_log_write_percent >= 40 THEN 1 ELSE 0 END) * 1.0) / COUNT(database_name) AS 'Log Write Fit Percent'
            ,(COUNT(database_name) - SUM(CASE WHEN avg_data_io_percent >= 40 THEN 1 ELSE 0 END) * 1.0) / COUNT(database_name) AS 'Physical Data IO Fit Percent'
        FROM sys.resource_stats
        WHERE database_name = 'userdb1' AND start_time > DATEADD(day, -7, GETDATE());
   
    根據您的資料庫服務等級目標 (SLO)，您可以決定 hello 較低效能層級是否符合您的工作負載。 如果您的資料庫工作負載 SLO 是 99.9 %hello 上述查詢會傳回值大於 99.9%的所有三個資源維度，您的工作負載可能會納入 hello 低效能層級。
   
    查看符合 hello 百分比也可讓您深入了解是否應該一併移動 toohello 下一個較高的效能層級 toomeet 您的 SLO。 例如，userdb1 顯示 hello 下列過去一週的 CPU 使用量 hello:
   
   | 平均 CPU 百分比 | 最大 CPU 百分比 |
   | --- | --- |
   | 24.5 |100.00 |
   
    hello 平均 CPU 大約是一季的 hello 限制 hello 效能層級，它也會納入 hello hello 資料庫效能層級。 但是，hello 最大值會顯示該 hello 資料庫到達 hello hello 效能層級上限。 您需要 toomove toohello 下一個較高的效能層級嗎？ 查看如何多次工作負載達到 100%，然後比較 tooyour 資料庫工作負載 SLO。
   
        SELECT
        (COUNT(database_name) - SUM(CASE WHEN avg_cpu_percent >= 100 THEN 1 ELSE 0 END) * 1.0) / COUNT(database_name) AS 'CPU fit percent'
        ,(COUNT(database_name) - SUM(CASE WHEN avg_log_write_percent >= 100 THEN 1 ELSE 0 END) * 1.0) / COUNT(database_name) AS 'Log write fit percent'
        ,(COUNT(database_name) - SUM(CASE WHEN avg_data_io_percent >= 100 THEN 1 ELSE 0 END) * 1.0) / COUNT(database_name) AS 'Physical data I/O fit percent'
        FROM sys.resource_stats
        WHERE database_name = 'userdb1' AND start_time > DATEADD(day, -7, GETDATE());
   
    如果此查詢傳回的值小於 99.9%的任何 hello 三個資源維度，請考慮可能是移動 toohello 下一個效能層級，或 hello SQL 資料庫上使用應用程式微調技術 tooreduce hello 負載。
4. 這個練習中也會考慮 hello 您預計的工作負載增加未來。

彈性集區，您可以使用本節中所述的 hello 技巧監視 hello 集區中的個別資料庫。 但是，您也可以監視整體的 hello 集區。 如需詳細資訊，請參閱 [監視和管理彈性集區](sql-database-elastic-pool-manage-portal.md)。


### <a name="maximum-concurrent-requests"></a>並行要求數上限
toosee hello 並行要求數量，您的 SQL 資料庫上執行此 TRANSACT-SQL 查詢：

    SELECT COUNT(*) AS [Concurrent_Requests]
    FROM sys.dm_exec_requests R

tooanalyze hello 工作負載，在內部部署 SQL Server 資料庫，修改此查詢 toofilter 想 tooanalyze hello 特定資料庫上。 比方說，如果您擁有名為 MyDatabase 在內部部署資料庫時，此 Transact SQL 查詢會傳回 hello 計數的並行要求該資料庫中：

    SELECT COUNT(*) AS [Concurrent_Requests]
    FROM sys.dm_exec_requests R
    INNER JOIN sys.databases D ON D.database_id = R.database_id
    AND D.name = 'MyDatabase'

這只是單一時間點的快照。 tooget 進一步了解您的工作負載和並行要求的需求，您將需要 toocollect 經過一段時間的許多範例。

### <a name="maximum-concurrent-logins"></a>並行登入數上限
您可以分析您使用者和應用程式模式 tooget hello 頻率的登入的了解。 您也可以執行實際負載測試環境 toomake 確定您在不遇到這個或其他限制，我們在本文中討論。 沒有任何單一查詢或動態管理檢視 (DMV) 可以向您顯示並行登入計數或歷程記錄。

如果使用多個用戶端 hello 相同的連接字串 hello 服務會驗證每個登入。 如果 10 個使用者同時連接使用 tooa 資料庫 hello 相同使用者名稱和密碼，會有 10 個並行登入。 這項限制適用於僅 hello 登入與驗證 toohello 持續時間。 如果 hello 相同 10 使用者依序連接 toohello 資料庫，並行登入的 hello 數目會絕對不大於 1。

> [!NOTE]
> 目前，這項限制不適用 toodatabases 彈性集區中。
> 
> 

### <a name="maximum-sessions"></a>工作階段數上限
toosee hello 目前作用中工作階段數目，您的 SQL 資料庫上執行此 TRANSACT-SQL 查詢：

    SELECT COUNT(*) AS [Sessions]
    FROM sys.dm_exec_connections

如果您正在分析之內部部署 SQL Server 工作負載，修改 hello 查詢 toofocus 上特定資料庫。 此查詢可協助您判斷可能的工作階段需求 hello 資料庫，如果您考慮將它移 tooAzure SQL 資料庫。

    SELECT COUNT(*)  AS [Sessions]
    FROM sys.dm_exec_connections C
    INNER JOIN sys.dm_exec_sessions S ON (S.session_id = C.session_id)
    INNER JOIN sys.databases D ON (D.database_id = S.database_id)
    WHERE D.name = 'MyDatabase'

同樣地，這些查詢傳回的是某一時間點的計數。 如果您收集一段時間的多個範例，您就必須 hello 充分瞭解您的工作階段使用。

SQL Database 的分析，您可以取得歷程記錄統計資料工作階段藉由查詢 hello [sys.resource_stats](https://msdn.microsoft.com/library/dn269979.aspx)檢視和檢閱 hello **active_session_count**資料行。 
