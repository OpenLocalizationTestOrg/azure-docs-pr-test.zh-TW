---
title: "SQL Database 資源限制 aaaAzure |Microsoft 文件"
description: "此頁面描述一些 Azure SQL Database 常見的資源限制。"
services: sql-database
documentationcenter: na
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 884e519f-23bb-4b73-a718-00658629646a
ms.service: sql-database
ms.custom: DBs & servers
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 07/12/2017
ms.author: carlrab
ms.openlocfilehash: 3e7be4fdc74e802d37274690531caaf138bcedb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sql-database-resource-limits"></a>Azure SQL Database 資源限制
## <a name="overview"></a>概觀
Azure SQL Database 管理 hello 資源可用 tooa 資料庫使用兩個不同的機制：**資源控管**和**強制的限制**。 本主題將說明這兩種主要的資源管理方法。

## <a name="resource-governance"></a>資源管理
Hello hello Basic、 Standard、 Premium 和 RS Premium 服務層的設計目標是針對 Azure SQL Database toobehave hello 資料庫如同它自己的機器，隔離與其他資料庫上執行。 資源管理便會模擬這個行為。 如果 hello 彙總資源使用率達到 hello 最大可用 CPU、 記憶體、 記錄檔 I/O 和資料 I/O 資源指派的 toohello 資料庫、 資源控管執行中的佇列查詢，並將指派 toohello 排入佇列時的查詢釋出資源。

做為在專用電腦上，利用所有可用的資源結果中執行更久的目前執行的查詢，從而會導致 hello 用戶端上的命令逾時。 具有積極重試邏輯應用程式以及針對高頻率的 hello 資料庫執行查詢的應用程式時可能會出現錯誤訊息時已達到 hello 限制的並行要求嘗試 tooexecute 新查詢。

### <a name="recommendations"></a>建議：
接近 hello 資料庫最大使用率時，監視 hello 的資源使用率與 hello 平均回應時間的查詢。 查詢的延遲較高時，您通常可採取三種應對方式：

1. 減少 hello 連入要求 toohello 資料庫 tooprevent 逾時和 hello 以免要求次數。
2. 指派較高的效能層級 toohello 資料庫。
3. 最佳化查詢 tooreduce hello 的每個查詢的資源使用率。 如需詳細資訊，請參閱 hello hello Azure SQL Database 效能指引文件中的查詢微調/提示 > 一節。

## <a name="enforcement-of-limits"></a>限制強制執行
系統會在達到上限時拒絕新的要求，藉此強制執行 CPU、記憶體、記錄 I/O 和資料 I/O 以外的資源。 當資料庫到達 hello 設定大小上限、 插入和更新，可以提升資料的大小失敗，同時選取並刪除繼續 toowork。 用戶端接收[錯誤訊息](sql-database-develop-error-messages.md)根據 hello 已達到的限制。

例如，hello tooa SQL 資料庫的連接數目和 hello 可處理的並行要求數目會限制。 SQL Database 可讓連接 toohello 資料庫 toobe 的 hello 數目大於 hello 的並行要求 toosupport 連接共用。 Hello 應用程式可以輕鬆地控制 hello 可用的連接數目，而平行要求的 hello 數目通常是時間更難 tooestimate 和 toocontrol。 特別是在 hello 應用程式傳送太多要求或 hello 資料庫達到其資源限制，並開始堆積背景工作執行緒，因為 toolonger 執行查詢，可能會遇到錯誤時的尖峰負載。

## <a name="service-tiers-and-performance-levels"></a>服務層和效能等級
單一資料庫和彈性集區都有服務層和效能等級。

### <a name="single-databases"></a>單一資料庫
單一資料庫，資料庫的 hello 限制由 hello 資料庫服務層和效能層級定義。 hello 下表描述在不同的效能層級的 Basic、 Standard、 Premium 和 Premium RS 資料庫 hello 特性。

[!INCLUDE [SQL DB service tiers table](../../includes/sql-database-service-tiers-table.md)]

> [!IMPORTANT]
> 使用 P11 和 P15 效能層級的客戶可以使用向上 too4 TB，包括存放裝置，不另收費。 4 TB 則使用此選項目前在 hello 下列區域： 美國 East2、 美國西部、 美國 Gov 維吉尼亞州、 西歐、 德國中央、 南東亞、 日本東部、 澳洲東部、 加拿大中央和加拿大東部。
>

### <a name="elastic-pools"></a>彈性集區
[彈性集區](sql-database-elastic-pool.md)hello 集區中的資料庫之間共用資源。 下表中的 hello 說明 Basic、 Standard、 Premium 和 Premium RS 彈性集區 hello 特性。

[!INCLUDE [SQL DB service tiers table for elastic databases](../../includes/sql-database-service-tiers-table-elastic-pools.md)]

Hello 之前的表格中所列每項資源已展開定義，請參閱中的 hello 描述[服務層的功能以及限制](sql-database-performance-guidance.md#service-tier-capabilities-and-limits)。 如需服務層的概觀，請參閱 [Azure SQL Database 服務層和效能等級](sql-database-service-tiers.md)。

## <a name="other-sql-database-limits"></a>其他 SQL Database 限制
| 領域 | 限制 | 說明 |
| --- | --- | --- |
| 每個訂用帳戶使用自動匯出的資料庫 |10 |自動的匯出可讓您 toocreate 自訂的排程來備份 SQL 資料庫。 這項功能的 hello 預覽版即將結束 2017 年 3 月 1 上。  |
| 每一伺服器的資料庫 |向上 too5000 |向上 too5000 資料庫允許每一部伺服器。 |
| 每一部伺服器的 DTU |45000 |每一部伺服器允許 45000 個 DTU，以佈建獨立資料庫和彈性集區。 hello 總數的獨立資料庫與集區允許每個伺服器只會受到伺服器的 Dtu hello 號碼。  

> [!IMPORTANT]
> Azure SQL 資料庫自動匯出目前為預覽狀態，並會在 2017 年 3 月 1 日停用。 從 2016 年 12 月 1 日，您將不再能夠 tooconfigure 自動化匯出任何 SQL 資料庫。 您現有的自動的匯出作業將會繼續 toowork 2017 年 3 月 1 日。 2016 年 12 月 1 日之後，您可以使用[長期備份的保留](sql-database-long-term-retention.md)或[Azure 自動化](../automation/automation-intro.md)使用 PowerShell 定期，根據您選擇的 tooa 排程定期 tooarchive SQL 資料庫。 如需範例指令碼中，您可以下載 hello[範例指令碼從 GitHub](https://github.com/Microsoft/sql-server-samples/tree/master/samples/manage/azure-automation-automated-export)。
>


## <a name="resources"></a>資源
[Azure 訂用帳戶和服務限制、配額與限制](../azure-subscription-service-limits.md)

[Azure SQL Database 服務層和效能層級](sql-database-service-tiers.md)

[SQL Database 用戶端程式的錯誤訊息](sql-database-develop-error-messages.md)
