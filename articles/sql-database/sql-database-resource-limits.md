---
title: "Azure SQL Database 資源限制 | Microsoft Docs"
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
ms.openlocfilehash: e75458db79e6c15f8d5155b71f04a20fa21818ff
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="azure-sql-database-resource-limits"></a>Azure SQL Database 資源限制
## <a name="overview"></a>概觀
Azure SQL Database 使用兩種不同機制來管理資料庫可使用的資源：**資源管理**和**限制強制執行**。 本主題將說明這兩種主要的資源管理方法。

## <a name="resource-governance"></a>資源管理
基本、標準、進階和進階 RS 服務層的設計目的之一，是讓 Azure SQL Database 彷彿在獨立的電腦上執行，而與其他資料庫隔離。 資源管理便會模擬這個行為。 如果彙總的資源使用率達到可用 CPU、記憶體、記錄 I/O 和資料 I/O 資源 (指派至資料庫) 的上限，資源管理會將查詢排入執行佇列中，並在系統釋出資源時，適時將資源指派給佇列中的查詢。

在專用的電腦上使用所有可用的資源，會導致目前正在執行的查詢花費更多執行時間，而這可能會使得用戶端上的命令逾時。 具備積極重試邏輯的應用程式，以及時常對資料庫執行查詢的應用程式，若在嘗試執行新查詢時達到並行要求的上限，便可能出現錯誤訊息。

### <a name="recommendations"></a>建議：
資料庫使用率接近上限時，監視資源使用率以及查詢的平均回應時間。 查詢的延遲較高時，您通常可採取三種應對方式：

1. 減少資料庫的傳入要求數目，以避免逾時和要求不斷累積。
2. 為資料庫指派更高的效能層級。
3. 將查詢最佳化，以降低每個查詢的資源使用率。 如需詳細資訊，請參閱＜Azure SQL Database 效能指南＞一文的「查詢微調/提示」章節。

## <a name="enforcement-of-limits"></a>限制強制執行
系統會在達到上限時拒絕新的要求，藉此強制執行 CPU、記憶體、記錄 I/O 和資料 I/O 以外的資源。 當資料庫達到設定的大小上限時，會使得資料大小增加的插入與更新作業將會失敗，但選取與刪除作業仍能繼續運作。 用戶端收到的[錯誤訊息](sql-database-develop-error-messages.md)會因達到的上限而有所不同。

例如，SQL Database 的連線數，以及可以處理的並行要求數目都將受到限制。 SQL Database 可允許資料庫的連接數大於並行要求的數目，以支援連接共用。 雖然應用程式能輕易控制可用的連接數目，但平行要求的數目通常難以預估及控制。 尤其在尖峰負載期間，應用程式往往傳送過多的要求，或是資料庫在達到資源上限後，因為執行耗時較長的查詢而開始累積背景工作執行緒，此時就可能發生錯誤。

## <a name="service-tiers-and-performance-levels"></a>服務層和效能等級
單一資料庫和彈性集區都有服務層和效能等級。

### <a name="single-databases"></a>單一資料庫
對於單一資料庫，資料庫的限制是由服務層級和效能等級所定義。 下表說明基本、標準、進階和進階 RS 資料庫在不同效能等級的特性。

[!INCLUDE [SQL DB service tiers table](../../includes/sql-database-service-tiers-table.md)]

> [!IMPORTANT]
> 使用 P11 和 P15 效能等級的客戶不需額外付費就能使用最多 4 TB 的內含儲存體。 這個 4 TB 選項目前已在下列區域提供：美國東部 2、美國西部、美國維吉尼亞州政府、西歐、德國中部、東南亞、日本東部、澳大利亞東部、加拿大中部和加拿大東部。
>

### <a name="elastic-pools"></a>彈性集區
[彈性集區](sql-database-elastic-pool.md) 可在集區中的資料庫之間共用資源。 下表說明基本、標準、進階和進階 RS 彈性集區的特性。

[!INCLUDE [SQL DB service tiers table for elastic databases](../../includes/sql-database-service-tiers-table-elastic-pools.md)]

如需上述表格所列之每項資源的擴充定義，請參閱[服務層功能和限制](sql-database-performance-guidance.md#service-tier-capabilities-and-limits)中的說明。 如需服務層的概觀，請參閱 [Azure SQL Database 服務層和效能等級](sql-database-service-tiers.md)。

## <a name="other-sql-database-limits"></a>其他 SQL Database 限制
| 領域 | 限制 | 說明 |
| --- | --- | --- |
| 每個訂用帳戶使用自動匯出的資料庫 |10 |自動匯出可讓您建立自訂排程以備份 SQL Database。 此功能的預覽將於 2017 年 3 月 1 日結束。  |
| 每一伺服器的資料庫 |最多 5000 個 |每一部伺服器最多允許 5000 個資料庫。 |
| 每一部伺服器的 DTU |45000 |每一部伺服器允許 45000 個 DTU，以佈建獨立資料庫和彈性集區。 每一伺服器允許的獨立資料庫和集區總數，僅受限於伺服器 DTU 數目。  

> [!IMPORTANT]
> Azure SQL 資料庫自動匯出目前為預覽狀態，並會在 2017 年 3 月 1 日停用。 從 2016 年 12 月 1 日開始，您將無法再於任何 SQL 資料庫上設定自動匯出。 所有現有的自動匯出作業會繼續運作至 2017 年 3 月 1 日。 2016 年 12 月 1 日之後，您可以使用[長期的備份保留](sql-database-long-term-retention.md)或 [Azure 自動化](../automation/automation-intro.md)，根據您選擇的排程使用 PowerShell 定期封存 SQL Database。 如需範例指令碼，您可以[從 GitHub 下載範例指令碼](https://github.com/Microsoft/sql-server-samples/tree/master/samples/manage/azure-automation-automated-export)。
>


## <a name="resources"></a>資源
[Azure 訂用帳戶和服務限制、配額與限制](../azure-subscription-service-limits.md)

[Azure SQL Database 服務層和效能層級](sql-database-service-tiers.md)

[SQL Database 用戶端程式的錯誤訊息](sql-database-develop-error-messages.md)
