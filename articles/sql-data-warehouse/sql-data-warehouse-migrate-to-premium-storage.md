---
title: "aaaMigrate 您現有的 Azure 資料倉儲 toopremium 儲存體 |Microsoft 文件"
description: "移轉現有的資料倉儲 toopremium 存放裝置的指示"
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: barbkess
editor: 
ms.assetid: 04b05dea-c066-44a0-9751-0774eb84c689
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: migrate
ms.date: 11/29/2016
ms.author: elbutter;barbkess
ms.openlocfilehash: 145199c2da1f6f1fb8898626cd04886c42d82204
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-your-data-warehouse-toopremium-storage"></a>將資料倉儲 toopremium 存放裝置移轉
Azure SQL 資料倉儲最新引進了[進階儲存體，以獲得更高的效能可預測性][premium storage for greater performance predictability]。 現在可以在標準儲存體目前的倉儲的現有資料移轉 toopremium 儲存體。 您可以利用自動移轉，或如果您偏好 toocontrol 時 toomigrate （其中並未包含一些停機時間），您可以自行 hello 移轉。

如果您有一個以上的資料倉儲時，使用 hello[自動移轉排程][ automatic migration schedule] toodetermine 時也將會移轉。

## <a name="determine-storage-type"></a>決定儲存體類型
如果您建立資料倉儲 hello 下列日期之前，您目前使用標準儲存體。

| **區域** | **在此日期前建立的資料倉儲** |
|:--- |:--- |
| 澳洲東部 |尚未提供進階儲存體 |
| 中國東部 |2016 年 11 月 1 日 |
| 中國北部 |2016 年 11 月 1 日 |
| 德國中部 |2016 年 11 月 1 日 |
| 德國東北部 |2016 年 11 月 1 日 |
| 印度西部 |尚未提供進階儲存體 |
| 日本西部 |尚未提供進階儲存體 |
| 美國中北部 |2016 年 11 月 10 日 |

## <a name="automatic-migration-details"></a>自動移轉詳細資料
根據預設，我們將您的資料庫，下午 6:00 和上午 6:00 地區的當地時間之間期間移轉 hello[自動移轉排程][automatic migration schedule]。 Hello 移轉期間將無法使用現有的資料倉儲。 hello 移轉每個資料倉儲會每 tb 的儲存空間大約一小時。 您不收費 hello 自動移轉的任何部份。

> [!NOTE]
> Hello 移轉完成時，您的資料倉儲會回線上和可用性。
>
>

Microsoft 正在 hello 遷移步驟 toocomplete hello （這些不需要您採取任何介入）。 在此範例中，假設您在標準儲存體上的現有資料倉儲目前名為 “MyDW”。

1. Microsoft 會重新命名 「 MyDW 」 太"MyDW_DO_NOT_USE_ [時間戳記]"。
2. Microsoft 會暫停 “MyDW_DO_NOT_USE_[時間戳記]”。 系統會在此期間執行備份。 如果在過程中發生任何問題，您可能會看到多個暫停及繼續。
3. Microsoft 會建立名為"MyDW"高階儲存體的 hello 備份在步驟 2 中所採取的新資料倉儲。 不會出現 「 MyDW"直到 hello 還原完成之後。
4. 「 MyDW"hello 還原完成後，傳回的 toohello 相同的資料倉儲單位和狀態 （已暫停或使用中） 並將該 hello 移轉之前。
5. Hello 移轉完成之後，Microsoft 便會刪除 「 MyDW_DO_NOT_USE_ [時間戳記]"。

> [!NOTE]
> hello 下列設定不會延續 hello 移轉的一部分：
>
> * Hello 資料庫層級稽核需要 toobe 重新啟用。
> * Hello 資料庫層級防火牆規則需要 toobe 重新加入。 不會影響 hello 伺服器層級防火牆規則。
>
>

### <a name="automatic-migration-schedule"></a>自動移轉排程
期間之後中斷排程 hello，下午 6:00 和上午 6:00 （每個區域的本機時間） 之間發生自動移轉。

| **區域** | **預估開始日期** | **預估結束日期** |
|:--- |:--- |:--- |
| 澳洲東部 |尚未決定 |尚未決定 |
| 中國東部 |2017 年 1 月 9 日 |2017 年 1 月 13 日 |
| 中國北部 |2017 年 1 月 9 日 |2017 年 1 月 13 日 |
| 德國中部 |2017 年 1 月 9 日 |2017 年 1 月 13 日 |
| 德國東北部 |2017 年 1 月 9 日 |2017 年 1 月 13 日 |
| 印度西部 |尚未決定 |尚未決定 |
| 日本西部 |尚未決定 |尚未決定 |
| 美國中北部 |2017 年 1 月 9 日 |2017 年 1 月 13 日 |

## <a name="self-migration-toopremium-storage"></a>自我移轉 toopremium 儲存體
如果您想 toocontrol 將停機時間將會發生時，您可以使用下列步驟 toomigrate 現有的資料倉儲標準儲存體 toopremium 存放裝置上的 hello。 如果您選擇此選項時，您必須先完成 hello 自我移轉，才能開始在該區域中的 hello 自動移轉。 這可確保您避免 hello 自動移轉造成衝突的任何風險 (請參閱 toohello[自動移轉排程][automatic migration schedule])。

### <a name="self-migration-instructions"></a>自行移轉指示
toomigrate 資料倉儲自行、 使用 hello 備份和還原功能。 hello 還原 hello 移轉部分是預期的 tootake 每 tb 的資料倉儲儲存空間大約一小時。 如果您想 tookeep hello 相同的名稱，在移轉完成之後，請遵循 hello[移轉期間的步驟 toorename][steps toorename during migration]。

1. [暫停][Pause] 資料倉儲。 這會進行自動備份。
2. 從最新的快照集[還原][Restore]。
3. 刪除標準儲存體上的現有資料倉儲。 **如果您無法 toodo 此步驟中，您將支付這兩個資料倉儲。**

> [!NOTE]
> hello 下列設定不會延續 hello 移轉的一部分：
>
> * Hello 資料庫層級稽核需要 toobe 重新啟用。
> * Hello 資料庫層級防火牆規則需要 toobe 重新加入。 不會影響 hello 伺服器層級防火牆規則。
>
>

#### <a name="rename-data-warehouse-during-migration-optional"></a>(選擇性) 在移轉期間重新命名資料倉儲
兩個資料庫上不能有相同的邏輯伺服器 hello hello 相同的名稱。 SQL 資料倉儲現在支援 hello 能力 toorename 資料倉儲。

在此範例中，假設您在標準儲存體上的現有資料倉儲目前名為 “MyDW”。

1. 使用下列 ALTER DATABASE 命令的 hello 重新命名 「 MyDW"。 （在此範例中，我們會將它重新命名 「 MyDW_BeforeMigration。"） 此命令會停止所有現有的交易，並必須 hello master 資料庫 toosucceed 中完成。
   ```
   ALTER DATABASE CurrentDatabasename MODIFY NAME = NewDatabaseName;
   ```
2. [暫停][Pause] "MyDW_BeforeMigration"。 這會進行自動備份。
3. [還原][ Restore]從最新快照集 hello 名稱的新資料庫，它使用 toobe (例如，"MyDW")。
4. 刪除 "MyDW_BeforeMigration"。 **如果您無法 toodo 此步驟中，您將支付這兩個資料倉儲。**


## <a name="next-steps"></a>後續步驟
以 hello toopremium 存放裝置的變更，您也可以在 hello 基礎架構中的資料倉儲資料庫的 blob 檔案的數目會增加。 toomaximize hello 效能優勢，這項變更，使用下列指令碼的 hello 來重建叢集資料行存放區索引。 hello 指令碼的運作方式強制執行某些現有的資料 toohello 其他 blob。 如果您不採取任何動作，hello 資料經過一段時間自然會重新發佈，當您將更多的資料載入資料表。

**先決條件：**

- hello 資料倉儲應執行 1,000 資料倉儲單位或更高版本 (請參閱[標尺的計算能力][scale compute power])。
- hello 執行 hello 指令碼的使用者應該在 hello [mediumrc 角色][ mediumrc role]或更高版本。 tooadd 使用者 toothis 角色，執行下列 hello:````EXEC sp_addrolemember 'xlargerc', 'MyUser'````

````sql
-------------------------------------------------------------------------------
-- Step 1: Create table toocontrol index rebuild
-- Run as user in mediumrc or higher
--------------------------------------------------------------------------------
create table sql_statements
WITH (distribution = round_robin)
as select
    'alter index all on ' + s.name + '.' + t.NAME + ' rebuild;' as statement,
    row_number() over (order by s.name, t.name) as sequence
from
    sys.schemas s
    inner join sys.tables t
        on s.schema_id = t.schema_id
where
    is_external = 0
;
go

--------------------------------------------------------------------------------
-- Step 2: Execute index rebuilds. If script fails, hello below can be re-run toorestart where last left off.
-- Run as user in mediumrc or higher
--------------------------------------------------------------------------------

declare @nbr_statements int = (select count(*) from sql_statements)
declare @i int = 1
while(@i <= @nbr_statements)
begin
      declare @statement nvarchar(1000)= (select statement from sql_statements where sequence = @i)
      print cast(getdate() as nvarchar(1000)) + ' Executing... ' + @statement
      exec (@statement)
      delete from sql_statements where sequence = @i
      set @i += 1
end;
go
-------------------------------------------------------------------------------
-- Step 3: Clean up table created in Step 1
--------------------------------------------------------------------------------
drop table sql_statements;
go
````

如果您遇到任何問題，與您的資料倉儲[建立支援票證][ create a support ticket]以及參考 「 移轉 toopremium 儲存體 」 為 hello 可能的原因。

<!--Image references-->

<!--Article references-->
[automatic migration schedule]: #automatic-migration-schedule
[self-migration tooPremium Storage]: #self-migration-to-premium-storage
[create a support ticket]: sql-data-warehouse-get-started-create-support-ticket.md
[Azure paired region]: best-practices-availability-paired-regions.md
[main documentation site]: services/sql-data-warehouse.md
[Pause]: sql-data-warehouse-manage-compute-portal.md#pause-compute
[Restore]: sql-data-warehouse-restore-database-portal.md
[steps toorename during migration]: #optional-steps-to-rename-during-migration
[scale compute power]: sql-data-warehouse-manage-compute-portal.md#scale-compute-power
[mediumrc role]: sql-data-warehouse-develop-concurrency.md

<!--MSDN references-->


<!--Other Web references-->
[Premium Storage for greater performance predictability]: https://azure.microsoft.com/en-us/blog/azure-sql-data-warehouse-introduces-premium-storage-for-greater-performance/
[Azure Portal]: https://portal.azure.com
