---
title: "aaaData 類型指南-Azure SQL 資料倉儲 |Microsoft 文件"
description: "建議 toodefine 資料型別都相容 SQL 資料倉儲。"
services: sql-data-warehouse
documentationcenter: NA
author: shivaniguptamsft
manager: barbkess
editor: 
ms.assetid: d4a1f0a3-ba9f-44b9-95f6-16a4f30746d6
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: tables
ms.date: 06/02/2017
ms.author: shigu;barbkess
ms.openlocfilehash: a2f7a394feb73d273b25101735b00eb12db2b292
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="guidance-for-defining-data-types-for-tables-in-sql-data-warehouse"></a>定義 SQL 資料倉儲中資料表資料類型的指引
使用 SQL 資料倉儲與相容這些建議 toodefine 資料表資料類型。 此外 toocompatibility，最小化的資料類型的 hello 大小可改善查詢效能。

SQL 資料倉儲支援 hello 最常使用的資料類型。 如需支援的 hello 資料類型的清單，請參閱[資料型別](/sql/docs/t-sql/statements/create-table-azure-sql-data-warehouse.md#datatypes)hello CREATE TABLE 陳述式中。 


## <a name="minimize-row-length"></a>將資料列長度最小化
資料型別的 hello 大小降到最低，就會縮短 hello 資料列長度會導致 toobetter 查詢效能。 使用 hello 最小資料類型，適用於您的資料。 

- 避免使用較大的預設長度來定義字元資料行。 例如，如果 hello 最長的值是 25 個字元，然後定義您的資料行為 VARCHAR(25)。 
- 當您僅需要 VARCHAR 時，請避免使用 [NVARCHAR][NVARCHAR]。
- 儘可能使用 NVARCHAR(4000) 或 VARCHAR(8000)，而非 NVARCHAR(MAX) 或 VARCHAR(MAX)。

如果您要使用 Polybase tooload 資料表，定義 hello hello 資料表資料列長度不能超過 1 MB。 當具有可變長度資料的資料列超過 1 MB 時，您可以載入 hello 列 bcp，但不是使用 PolyBase。

## <a name="identify-unsupported-data-types"></a>識別不支援的資料類型
如果您從另一個 SQL Database 移轉您的資料庫，可能會遇到 SQL 資料倉儲不支援的資料類型。 使用此查詢 toodiscover 不支援的資料類型現有的 SQL 結構描述中。

```sql
SELECT  t.[name], c.[name], c.[system_type_id], c.[user_type_id], y.[is_user_defined], y.[name]
FROM sys.tables  t
JOIN sys.columns c on t.[object_id]    = c.[object_id]
JOIN sys.types   y on c.[user_type_id] = y.[user_type_id]
WHERE y.[name] IN ('geography','geometry','hierarchyid','image','text','ntext','sql_variant','timestamp','xml')
 AND  y.[is_user_defined] = 1;
```


## <a name="unsupported-data-types"></a>將因應措施用於不支援的資料類型

hello 下列清單顯示 hello SQL 資料倉儲不支援的資料類型和提供的替代方案，您可以使用取代 hello 不支援的資料類型。

| 不支援的資料類型 | 因應措施 |
| --- | --- |
| [geometry][geometry] |[varbinary][varbinary] |
| [geography][geography] |[varbinary][varbinary] |
| [hierarchyid][hierarchyid] |[nvarchar][nvarchar](4000) |
| [image][ntext,text,image] |[varbinary][varbinary] |
| [text][ntext,text,image] |[varchar][varchar] |
| [ntext][ntext,text,image] |[nvarchar][nvarchar] |
| [sql_variant][sql_variant] |將資料行分割成數個強型別資料行。 |
| [table][table] |將轉換 tootemporary 資料表。 |
| [timestamp][timestamp] |重新撰寫程式碼 toouse [datetime2] [ datetime2]和`CURRENT_TIMESTAMP`函式。  僅支援常數做為預設值，因此 current_timestamp 不可定義為預設條件約束。 如果您需要時間戳記的具類型資料行從 toomigrate 資料列版本值，然後使用[二進位][BINARY](8) 或[VARBINARY][BINARY](8) 的 NOT NULL 或NULL 的資料列版本值。 |
| [xml][xml] |[varchar][varchar] |
| [使用者定義型別][user defined types] |轉換時可能回復 toohello 原生資料類型。 |
| 預設值 | 預設值僅支援常值和常數。  不支援不具決定性的運算式或函式，例如 `GETDATE()` 或 `CURRENT_TIMESTAMP`。 |


## <a name="next-steps"></a>後續步驟
toolearn 詳細資訊，請參閱：

- [SQL 資料倉儲最佳做法][SQL Data Warehouse Best Practices]
- [資料表概觀][Overview]
- [發佈資料表][Distribute]
- [建立資料表索引][Index]
- [分割資料表][Partition]
- [維護資料表統計資料][Statistics]
- [暫存資料表][Temporary]

<!--Image references-->

<!--Article references-->
[Overview]: ./sql-data-warehouse-tables-overview.md
[Data Types]: ./sql-data-warehouse-tables-data-types.md
[Distribute]: ./sql-data-warehouse-tables-distribute.md
[Index]: ./sql-data-warehouse-tables-index.md
[Partition]: ./sql-data-warehouse-tables-partition.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md
[Temporary]: ./sql-data-warehouse-tables-temporary.md
[SQL Data Warehouse Best Practices]: ./sql-data-warehouse-best-practices.md

<!--MSDN references-->

<!--Other Web references-->
[create table]: https://msdn.microsoft.com/library/mt203953.aspx
[bigint]: https://msdn.microsoft.com/library/ms187745.aspx
[binary]: https://msdn.microsoft.com/library/ms188362.aspx
[bit]: https://msdn.microsoft.com/library/ms177603.aspx
[char]: https://msdn.microsoft.com/library/ms176089.aspx
[date]: https://msdn.microsoft.com/library/bb630352.aspx
[datetime]: https://msdn.microsoft.com/library/ms187819.aspx
[datetime2]: https://msdn.microsoft.com/library/bb677335.aspx
[datetimeoffset]: https://msdn.microsoft.com/library/bb630289.aspx
[decimal]: https://msdn.microsoft.com/library/ms187746.aspx
[float]: https://msdn.microsoft.com/library/ms173773.aspx
[geometry]: https://msdn.microsoft.com/library/cc280487.aspx
[geography]: https://msdn.microsoft.com/library/cc280766.aspx
[hierarchyid]: https://msdn.microsoft.com/library/bb677290.aspx
[int]: https://msdn.microsoft.com/library/ms187745.aspx
[money]: https://msdn.microsoft.com/library/ms179882.aspx
[nchar]: https://msdn.microsoft.com/library/ms186939.aspx
[nvarchar]: https://msdn.microsoft.com/library/ms186939.aspx
[ntext,text,image]: https://msdn.microsoft.com/library/ms187993.aspx
[real]: https://msdn.microsoft.com/library/ms173773.aspx
[smalldatetime]: https://msdn.microsoft.com/library/ms182418.aspx
[smallint]: https://msdn.microsoft.com/library/ms187745.aspx
[smallmoney]: https://msdn.microsoft.com/library/ms179882.aspx
[sql_variant]: https://msdn.microsoft.com/library/ms173829.aspx
[sysname]: https://msdn.microsoft.com/library/ms186939.aspx
[table]: https://msdn.microsoft.com/library/ms175010.aspx
[time]: https://msdn.microsoft.com/library/bb677243.aspx
[timestamp]: https://msdn.microsoft.com/library/ms182776.aspx
[tinyint]: https://msdn.microsoft.com/library/ms187745.aspx
[uniqueidentifier]: https://msdn.microsoft.com/library/ms187942.aspx
[varbinary]: https://msdn.microsoft.com/library/ms188362.aspx
[varchar]: https://msdn.microsoft.com/library/ms186939.aspx
[xml]: https://msdn.microsoft.com/library/ms187339.aspx
[user defined types]: https://msdn.microsoft.com/library/ms131694.aspx
