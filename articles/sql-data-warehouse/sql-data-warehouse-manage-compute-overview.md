---
title: "aaaManage 的計算能力，在 Azure SQL 資料倉儲 （概觀） |Microsoft 文件"
description: "Azure SQL 資料倉儲中的效能相應放大功能。 向外延展藉由調整 Dwu 或暫停和繼續計算資源 toosave 成本。"
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: johnmac
editor: 
ms.assetid: e13a82b0-abfe-429f-ac3c-f2b6789a70c6
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: manage
ms.date: 03/22/2017
ms.author: elbutter
ms.openlocfilehash: 1ffbe8d694ac181eaeb6f585a2cee87a570ed7d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-compute-power-in-azure-sql-data-warehouse-overview"></a>管理 Azure SQL 資料倉儲中的計算能力 (概觀)
> [!div class="op_single_selector"]
> * [概觀](sql-data-warehouse-manage-compute-overview.md)
> * [入口網站](sql-data-warehouse-manage-compute-portal.md)
> * [PowerShell](sql-data-warehouse-manage-compute-powershell.md)
> * [REST](sql-data-warehouse-manage-compute-rest-api.md)
> * [TSQL](sql-data-warehouse-manage-compute-tsql.md)
>
>

儲存體和計算，分別讓每個 tooscale，區隔 hello 架構的 SQL 資料倉儲。 如此一來，計算可以是獨立的資料量 hello 縮放的 toomeet 效能需求。 這個架構的自然結果為計算[計費][billed]和儲存體無關。 

本概觀說明如何擴充適用於 SQL 資料倉儲，且 tooutilize hello 暫停、 繼續和 SQL 資料倉儲的延展功能的方式。 請參閱 hello[資料倉儲單位 (Dwu)] [ data warehouse units (DWUs)]頁面 toolearn 相關性 Dwu 和效能。 

## <a name="how-compute-management-operations-work-in-sql-data-warehouse"></a>計算管理作業如何在 SQL 資料倉儲中運作
SQL 資料倉儲的 hello 架構是由控制節點所組成，計算節點及分散到 60 分佈 hello 儲存層。 

在正常作用中工作階段期間在 SQL 資料倉儲中，系統的前端節點會管理 hello 中繼資料，並包含 hello 分散式查詢最佳化工具。 此前端節點以下為計算節點和儲存層。 DWU 400，系統會有一個前端節點、 四個計算節點，與 hello 儲存層，60 分佈所組成。 

當您使用小數位數或暫停作業時，hello 系統首先會清除所有傳入的查詢，然後回復交易 tooensure 一致的狀態。 針對調整作業，僅在這個交易回復完成後調整才會發生。 向上延展作業，請 hello 系統佈建 hello 額外需要的運算節點數，然後重新附加 hello 計算節點 toohello 儲存層。 向下調整作業，請 hello 不需要的節點會釋放，hello 其餘運算節點重新附加本身 toohello 適當數量的分佈。 暫停作業中，所有計算節點並釋出與您的系統將會進行各種不同的中繼資料作業 tooleave 最終穩定的狀態系統。

| DWU  | \# 個計算節點 | 每節點 \# 個散發 |
| ---- | ------------------ | ---------------------------- |
| 100  | 1                  | 60                           |
| 200  | 2                  | 30                           |
| 300  | 3                  | 20                           |
| 400  | 4                  | 15                           |
| 500  | 5                  | 12                           |
| 600  | 6                  | 10                           |
| 1000 | 10                 | 6                            |
| 1200 | 12                 | 5                            |
| 1500 | 15                 | 4                            |
| 2000 | 20                 | 3                            |
| 3000 | 30                 | 2                            |
| 6000 | 60                 | 1                            |

hello 三個主要的功能來管理計算為：

1. 暫停
2. 繼續
3. 調整

每項作業可能需要幾分鐘的時間 toocomplete。 如果您是調整/暫停/繼續自動，您可能想 tooimplement 邏輯 tooensure 某些作業完成之前繼續執行其他動作。 

核取 hello 資料庫狀態，透過不同的端點，可讓這類作業的 toocorrectly 實作自動化。 hello 入口網站會提供完成的作業與 hello 資料庫目前狀態的通知，但不允許以程式設計方式檢查有無狀態。 

>  [!NOTE]
>
>  計算管理功能並未跨所有端點存在。
>
>  

|              | 暫停/繼續 | 調整 | 檢查資料庫狀態 |
| ------------ | ------------ | ----- | -------------------- |
| Azure 入口網站 | 是          | 是   | **否**               |
| PowerShell   | 是          | 是   | 是                  |
| REST API     | 是          | 是   | 是                  |
| T-SQL        | **否**       | 是   | 是                  |



<a name="scale-compute-bk"></a>

## <a name="scale-compute"></a>調整計算

SQL 資料倉儲中的效能測量單位為[資料倉儲單位 (DWU)][data warehouse units (DWUs)]，這是計算資源的抽象量值，例如 CPU、記憶體和 I/O 頻寬。 希望 tooscale 他們的系統效能的使用者可以在透過各種方式，例如透過 hello 入口網站，T-SQL、 REST Api。 

### <a name="how-do-i-scale-compute"></a>如何調整計算？
運算能力您管理的 SQL 資料倉儲藉由變更 hello 的 DWU 設定。 隨著您針對特定作業新增更多的 DWU，效能會[以線性方式][linearly]提升。  當您將系統相應增加或減少時，我們提供的 DWU 供應項目可確保您的效能會明顯變更。 

tooadjust Dwu，您可以使用任何一種個別的方法。

* [使用 Azure 入口網站調整計算能力][Scale compute power with Azure portal]
* [使用 PowerShell 調整計算能力][Scale compute power with PowerShell]
* [使用 REST API 調整計算能力][Scale compute power with REST APIs]
* [使用 TSQL 調整計算能力][Scale compute power with TSQL]

### <a name="how-many-dwus-should-i-use"></a>應該使用多少 DWU 呢？

toounderstand 您理想 DWU 值為何，請嘗試向上和向下調整並執行幾個查詢載入資料之後。 由於調整很快速，您可以在一小時內嘗各種效能層級。 

> [!Note] 
> SQL 資料倉儲是設計的 tooprocess 大量的資料。 toosee 想 toouse 大型資料集接近或超過 1 TB 的縮放比例，尤其是在較大的 dwu 調整其 true 功能。

尋找建議 hello 最佳的 DWU，您的工作負載：

1. 若是開發過程中的資料倉儲，可選取較少的 DWU 效能等級。  DW400 或 DW200 是不錯的起點。
2. 監視您的應用程式效能，觀察選取的 Dwu 的 hello 數目比較 toohello 您觀察到的效能。
3. 判斷多少快或慢的效能應該是您 tooreach hello 最佳的效能層級為您的需求，假設線性標尺。
4. 增加或減少 hello 數目要 dwu 調整比例 toohow 更快或慢中的工作負載 tooperform。 
5. 繼續進行調整，直到達到您業務需求的最佳效能為止。

> [!NOTE]
>
> 如果 hello 工作可以分割為計算節點，則查詢效能就只會增加與多個平行化作業。 如果您發現縮放比例不會變更您的效能，請查看我們的效能微調文章 toocheck 是否平均地分散您的資料，或引進大量的資料移動。 

### <a name="when-should-i-scale-dwus"></a>何時調整 DWU？
調整 Dwu 改變 hello 下列重要案例：

1. 以線性方式變更的掃描、 彙總和 CTAS 陳述式的 hello 系統的效能
2. Hello 日益增加的讀取器和寫入器時載入使用 PolyBase
3. 並行查詢和並行存取插槽數目上限

建議當 tooscale dwu 調整：

1. 執行大量資料載入或轉換作業之前，相應增加 DWU 以使您的資料更快速可供使用。
2. 尖峰營業時間，調整 tooaccommodate 大量的並行查詢。 

<a name="pause-compute-bk"></a>

## <a name="pause-compute"></a>暫停計算
[!INCLUDE [SQL Data Warehouse pause description](../../includes/sql-data-warehouse-pause-description.md)]

toopause 資料庫，可使用任何一種個別的方法。

* [使用 Azure 入口網站暫停計算][Pause compute with Azure portal]
* [使用 PowerShell 暫停計算][Pause compute with PowerShell]
* [使用 REST API 暫停計算][Pause compute with REST APIs]

<a name="resume-compute-bk"></a>

## <a name="resume-compute"></a>繼續計算
[!INCLUDE [SQL Data Warehouse resume description](../../includes/sql-data-warehouse-resume-description.md)]

tooresume 資料庫，可使用任何一種個別的方法。

* [使用 Azure 入口網站繼續計算][Resume compute with Azure portal]
* [使用 PowerShell 繼續計算][Resume compute with PowerShell]
* [使用 REST API 繼續計算][Resume compute with REST APIs]

<a name="check-compute-bk"></a>

## <a name="check-database-state"></a>檢查資料庫狀態 

tooresume 資料庫，可使用任何一種個別的方法。

- [使用 T-SQL 檢查資料庫狀態][Check database state with T-SQL]
- [使用 PowerShell 檢查資料庫狀態][Check database state with PowerShell]
- [使用 REST API 檢查資料庫狀態][Check database state with REST APIs]

## <a name="permissions"></a>權限

縮放比例的 hello 資料庫需要 hello 中所述的權限[ALTER DATABASE][ALTER DATABASE]。  暫停及繼續需要 hello [SQL DB 參與者][ SQL DB Contributor]權限，特別是 Microsoft.Sql/servers/databases/action。

<a name="next-steps-bk"></a>

## <a name="next-steps"></a>後續步驟
請參閱下列文章 toohelp 您了解一些額外的關鍵效能概念 toohello:

* [工作負載和並行管理][Workload and concurrency management]
* [資料表設計概觀][Table design overview]
* [資料表散發][Table distribution]
* [索引資料表的編製][Table indexing]
* [資料表分割][Table partitioning]
* [資料表統計資料][Table statistics]
* [最佳作法][Best practices]

<!--Image reference-->

<!--Article references-->
[data warehouse units (DWUs)]: ./sql-data-warehouse-overview-what-is.md#predictable-and-scalable-performance-with-data-warehouse-units
[billed]: https://azure.microsoft.com/en-us/pricing/details/sql-data-warehouse/
[linearly]: ./sql-data-warehouse-overview-what-is.md#predictable-and-scalable-performance-with-data-warehouse-units
[Scale compute power with Azure portal]: ./sql-data-warehouse-manage-compute-portal.md#scale-compute-power
[Scale compute power with PowerShell]: ./sql-data-warehouse-manage-compute-powershell.md#scale-compute-bk
[Scale compute power with REST APIs]: ./sql-data-warehouse-manage-compute-rest-api.md#scale-compute-bk
[Scale compute power with TSQL]: ./sql-data-warehouse-manage-compute-tsql.md#scale-compute-bk

[capacity limits]: ./sql-data-warehouse-service-capacity-limits.md

[Pause compute with Azure portal]:  ./sql-data-warehouse-manage-compute-portal.md#pause-compute-bk
[Pause compute with PowerShell]: ./sql-data-warehouse-manage-compute-powershell.md#pause-compute-bk
[Pause compute with REST APIs]: ./sql-data-warehouse-manage-compute-rest-api.md#pause-compute-bk

[Resume compute with Azure portal]:  ./sql-data-warehouse-manage-compute-portal.md#resume-compute-bk
[Resume compute with PowerShell]: ./sql-data-warehouse-manage-compute-powershell.md#resume-compute-bk
[Resume compute with REST APIs]: ./sql-data-warehouse-manage-compute-rest-api.md#resume-compute-bk

[Check database state with T-SQL]: ./sql-data-warehouse-manage-compute-tsql.md#check-database-state-and-operation-progress
[Check database state with PowerShell]: ./sql-data-warehouse-manage-compute-powershell.md#check-database-state
[Check database state with REST APIs]: ./sql-data-warehouse-manage-compute-rest-api.md#check-database-state

[Workload and concurrency management]: ./sql-data-warehouse-develop-concurrency.md
[Table design overview]: ./sql-data-warehouse-tables-overview.md
[Table distribution]: ./sql-data-warehouse-tables-distribute.md
[Table indexing]: ./sql-data-warehouse-tables-index.md
[Table partitioning]: ./sql-data-warehouse-tables-partition.md
[Table statistics]: ./sql-data-warehouse-tables-statistics.md
[Best practices]: ./sql-data-warehouse-best-practices.md
[development overview]: ./sql-data-warehouse-overview-develop.md

[SQL DB Contributor]: ../active-directory/role-based-access-built-in-roles.md#sql-db-contributor

<!--MSDN references-->
[ALTER DATABASE]: https://msdn.microsoft.com/library/mt204042.aspx

<!--Other Web references-->
[Azure portal]: http://portal.azure.com/
