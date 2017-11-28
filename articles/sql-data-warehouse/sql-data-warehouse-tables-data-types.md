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
# <a name="guidance-for-defining-data-types-for-tables-in-sql-data-warehouse"></a><span data-ttu-id="51ba2-103">定義 SQL 資料倉儲中資料表資料類型的指引</span><span class="sxs-lookup"><span data-stu-id="51ba2-103">Guidance for defining data types for tables in SQL Data Warehouse</span></span>
<span data-ttu-id="51ba2-104">使用 SQL 資料倉儲與相容這些建議 toodefine 資料表資料類型。</span><span class="sxs-lookup"><span data-stu-id="51ba2-104">Use these recommendations toodefine table data types that are compatible with SQL Data Warehouse.</span></span> <span data-ttu-id="51ba2-105">此外 toocompatibility，最小化的資料類型的 hello 大小可改善查詢效能。</span><span class="sxs-lookup"><span data-stu-id="51ba2-105">In addition toocompatibility, minimizing hello size of data types improves query performance.</span></span>

<span data-ttu-id="51ba2-106">SQL 資料倉儲支援 hello 最常使用的資料類型。</span><span class="sxs-lookup"><span data-stu-id="51ba2-106">SQL Data Warehouse supports hello most commonly used data types.</span></span> <span data-ttu-id="51ba2-107">如需支援的 hello 資料類型的清單，請參閱[資料型別](/sql/docs/t-sql/statements/create-table-azure-sql-data-warehouse.md#datatypes)hello CREATE TABLE 陳述式中。</span><span class="sxs-lookup"><span data-stu-id="51ba2-107">For a list of hello supported data types, see [data types](/sql/docs/t-sql/statements/create-table-azure-sql-data-warehouse.md#datatypes) in hello CREATE TABLE statement.</span></span> 


## <a name="minimize-row-length"></a><span data-ttu-id="51ba2-108">將資料列長度最小化</span><span class="sxs-lookup"><span data-stu-id="51ba2-108">Minimize row length</span></span>
<span data-ttu-id="51ba2-109">資料型別的 hello 大小降到最低，就會縮短 hello 資料列長度會導致 toobetter 查詢效能。</span><span class="sxs-lookup"><span data-stu-id="51ba2-109">Minimizing hello size of data types shortens hello row length, which leads toobetter query performance.</span></span> <span data-ttu-id="51ba2-110">使用 hello 最小資料類型，適用於您的資料。</span><span class="sxs-lookup"><span data-stu-id="51ba2-110">Use hello smallest data type that works for your data.</span></span> 

- <span data-ttu-id="51ba2-111">避免使用較大的預設長度來定義字元資料行。</span><span class="sxs-lookup"><span data-stu-id="51ba2-111">Avoid defining character columns with a large default length.</span></span> <span data-ttu-id="51ba2-112">例如，如果 hello 最長的值是 25 個字元，然後定義您的資料行為 VARCHAR(25)。</span><span class="sxs-lookup"><span data-stu-id="51ba2-112">For example, if hello longest value is 25 characters, then define your column as VARCHAR(25).</span></span> 
- <span data-ttu-id="51ba2-113">當您僅需要 VARCHAR 時，請避免使用 [NVARCHAR][NVARCHAR]。</span><span class="sxs-lookup"><span data-stu-id="51ba2-113">Avoid using [NVARCHAR][NVARCHAR] when you only need VARCHAR.</span></span>
- <span data-ttu-id="51ba2-114">儘可能使用 NVARCHAR(4000) 或 VARCHAR(8000)，而非 NVARCHAR(MAX) 或 VARCHAR(MAX)。</span><span class="sxs-lookup"><span data-stu-id="51ba2-114">When possible, use NVARCHAR(4000) or VARCHAR(8000) instead of NVARCHAR(MAX) or VARCHAR(MAX).</span></span>

<span data-ttu-id="51ba2-115">如果您要使用 Polybase tooload 資料表，定義 hello hello 資料表資料列長度不能超過 1 MB。</span><span class="sxs-lookup"><span data-stu-id="51ba2-115">If you are using Polybase tooload your tables, hello defined length of hello table row cannot exceed 1 MB.</span></span> <span data-ttu-id="51ba2-116">當具有可變長度資料的資料列超過 1 MB 時，您可以載入 hello 列 bcp，但不是使用 PolyBase。</span><span class="sxs-lookup"><span data-stu-id="51ba2-116">When a row with variable-length data exceeds 1 MB, you can load hello row with BCP, but not with PolyBase.</span></span>

## <a name="identify-unsupported-data-types"></a><span data-ttu-id="51ba2-117">識別不支援的資料類型</span><span class="sxs-lookup"><span data-stu-id="51ba2-117">Identify unsupported data types</span></span>
<span data-ttu-id="51ba2-118">如果您從另一個 SQL Database 移轉您的資料庫，可能會遇到 SQL 資料倉儲不支援的資料類型。</span><span class="sxs-lookup"><span data-stu-id="51ba2-118">If you are migrating your database from another SQL database, you might encounter data types that are not supported in SQL Data Warehouse.</span></span> <span data-ttu-id="51ba2-119">使用此查詢 toodiscover 不支援的資料類型現有的 SQL 結構描述中。</span><span class="sxs-lookup"><span data-stu-id="51ba2-119">Use this query toodiscover unsupported data types in your existing SQL schema.</span></span>

```sql
SELECT  t.[name], c.[name], c.[system_type_id], c.[user_type_id], y.[is_user_defined], y.[name]
FROM sys.tables  t
JOIN sys.columns c on t.[object_id]    = c.[object_id]
JOIN sys.types   y on c.[user_type_id] = y.[user_type_id]
WHERE y.[name] IN ('geography','geometry','hierarchyid','image','text','ntext','sql_variant','timestamp','xml')
 AND  y.[is_user_defined] = 1;
```


## <span data-ttu-id="51ba2-120"><a name="unsupported-data-types"></a>將因應措施用於不支援的資料類型</span><span class="sxs-lookup"><span data-stu-id="51ba2-120"><a name="unsupported-data-types"></a>Use workarounds for unsupported data types</span></span>

<span data-ttu-id="51ba2-121">hello 下列清單顯示 hello SQL 資料倉儲不支援的資料類型和提供的替代方案，您可以使用取代 hello 不支援的資料類型。</span><span class="sxs-lookup"><span data-stu-id="51ba2-121">hello following list shows hello data types that SQL Data Warehouse does not support and gives alternatives that you can use instead of hello unsupported data types.</span></span>

| <span data-ttu-id="51ba2-122">不支援的資料類型</span><span class="sxs-lookup"><span data-stu-id="51ba2-122">Unsupported data type</span></span> | <span data-ttu-id="51ba2-123">因應措施</span><span class="sxs-lookup"><span data-stu-id="51ba2-123">Workaround</span></span> |
| --- | --- |
| <span data-ttu-id="51ba2-124">[geometry][geometry]</span><span class="sxs-lookup"><span data-stu-id="51ba2-124">[geometry][geometry]</span></span> |<span data-ttu-id="51ba2-125">[varbinary][varbinary]</span><span class="sxs-lookup"><span data-stu-id="51ba2-125">[varbinary][varbinary]</span></span> |
| <span data-ttu-id="51ba2-126">[geography][geography]</span><span class="sxs-lookup"><span data-stu-id="51ba2-126">[geography][geography]</span></span> |<span data-ttu-id="51ba2-127">[varbinary][varbinary]</span><span class="sxs-lookup"><span data-stu-id="51ba2-127">[varbinary][varbinary]</span></span> |
| <span data-ttu-id="51ba2-128">[hierarchyid][hierarchyid]</span><span class="sxs-lookup"><span data-stu-id="51ba2-128">[hierarchyid][hierarchyid]</span></span> |<span data-ttu-id="51ba2-129">[nvarchar][nvarchar](4000)</span><span class="sxs-lookup"><span data-stu-id="51ba2-129">[nvarchar][nvarchar](4000)</span></span> |
| <span data-ttu-id="51ba2-130">[image][ntext,text,image]</span><span class="sxs-lookup"><span data-stu-id="51ba2-130">[image][ntext,text,image]</span></span> |<span data-ttu-id="51ba2-131">[varbinary][varbinary]</span><span class="sxs-lookup"><span data-stu-id="51ba2-131">[varbinary][varbinary]</span></span> |
| <span data-ttu-id="51ba2-132">[text][ntext,text,image]</span><span class="sxs-lookup"><span data-stu-id="51ba2-132">[text][ntext,text,image]</span></span> |<span data-ttu-id="51ba2-133">[varchar][varchar]</span><span class="sxs-lookup"><span data-stu-id="51ba2-133">[varchar][varchar]</span></span> |
| <span data-ttu-id="51ba2-134">[ntext][ntext,text,image]</span><span class="sxs-lookup"><span data-stu-id="51ba2-134">[ntext][ntext,text,image]</span></span> |<span data-ttu-id="51ba2-135">[nvarchar][nvarchar]</span><span class="sxs-lookup"><span data-stu-id="51ba2-135">[nvarchar][nvarchar]</span></span> |
| <span data-ttu-id="51ba2-136">[sql_variant][sql_variant]</span><span class="sxs-lookup"><span data-stu-id="51ba2-136">[sql_variant][sql_variant]</span></span> |<span data-ttu-id="51ba2-137">將資料行分割成數個強型別資料行。</span><span class="sxs-lookup"><span data-stu-id="51ba2-137">Split column into several strongly typed columns.</span></span> |
| <span data-ttu-id="51ba2-138">[table][table]</span><span class="sxs-lookup"><span data-stu-id="51ba2-138">[table][table]</span></span> |<span data-ttu-id="51ba2-139">將轉換 tootemporary 資料表。</span><span class="sxs-lookup"><span data-stu-id="51ba2-139">Convert tootemporary tables.</span></span> |
| <span data-ttu-id="51ba2-140">[timestamp][timestamp]</span><span class="sxs-lookup"><span data-stu-id="51ba2-140">[timestamp][timestamp]</span></span> |<span data-ttu-id="51ba2-141">重新撰寫程式碼 toouse [datetime2] [ datetime2]和`CURRENT_TIMESTAMP`函式。</span><span class="sxs-lookup"><span data-stu-id="51ba2-141">Rework code toouse [datetime2][datetime2] and `CURRENT_TIMESTAMP` function.</span></span>  <span data-ttu-id="51ba2-142">僅支援常數做為預設值，因此 current_timestamp 不可定義為預設條件約束。</span><span class="sxs-lookup"><span data-stu-id="51ba2-142">Only constants are supported as defaults, therefore current_timestamp cannot be defined as a default constraint.</span></span> <span data-ttu-id="51ba2-143">如果您需要時間戳記的具類型資料行從 toomigrate 資料列版本值，然後使用[二進位][BINARY](8) 或[VARBINARY][BINARY](8) 的 NOT NULL 或NULL 的資料列版本值。</span><span class="sxs-lookup"><span data-stu-id="51ba2-143">If you need toomigrate row version values from a timestamp typed column, then use [BINARY][BINARY](8) or [VARBINARY][BINARY](8) for NOT NULL or NULL row version values.</span></span> |
| <span data-ttu-id="51ba2-144">[xml][xml]</span><span class="sxs-lookup"><span data-stu-id="51ba2-144">[xml][xml]</span></span> |<span data-ttu-id="51ba2-145">[varchar][varchar]</span><span class="sxs-lookup"><span data-stu-id="51ba2-145">[varchar][varchar]</span></span> |
| <span data-ttu-id="51ba2-146">[使用者定義型別][user defined types]</span><span class="sxs-lookup"><span data-stu-id="51ba2-146">[user-defined type][user defined types]</span></span> |<span data-ttu-id="51ba2-147">轉換時可能回復 toohello 原生資料類型。</span><span class="sxs-lookup"><span data-stu-id="51ba2-147">Convert back toohello native data type when possible.</span></span> |
| <span data-ttu-id="51ba2-148">預設值</span><span class="sxs-lookup"><span data-stu-id="51ba2-148">default values</span></span> | <span data-ttu-id="51ba2-149">預設值僅支援常值和常數。</span><span class="sxs-lookup"><span data-stu-id="51ba2-149">Default values support literals and constants only.</span></span>  <span data-ttu-id="51ba2-150">不支援不具決定性的運算式或函式，例如 `GETDATE()` 或 `CURRENT_TIMESTAMP`。</span><span class="sxs-lookup"><span data-stu-id="51ba2-150">Non-deterministic expressions or functions, such as `GETDATE()` or `CURRENT_TIMESTAMP`, are not supported.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="51ba2-151">後續步驟</span><span class="sxs-lookup"><span data-stu-id="51ba2-151">Next steps</span></span>
<span data-ttu-id="51ba2-152">toolearn 詳細資訊，請參閱：</span><span class="sxs-lookup"><span data-stu-id="51ba2-152">toolearn more, see:</span></span>

- <span data-ttu-id="51ba2-153">[SQL 資料倉儲最佳做法][SQL Data Warehouse Best Practices]</span><span class="sxs-lookup"><span data-stu-id="51ba2-153">[SQL Data Warehouse Best Practices][SQL Data Warehouse Best Practices]</span></span>
- <span data-ttu-id="51ba2-154">[資料表概觀][Overview]</span><span class="sxs-lookup"><span data-stu-id="51ba2-154">[Table Overview][Overview]</span></span>
- <span data-ttu-id="51ba2-155">[發佈資料表][Distribute]</span><span class="sxs-lookup"><span data-stu-id="51ba2-155">[Distributing a Table][Distribute]</span></span>
- <span data-ttu-id="51ba2-156">[建立資料表索引][Index]</span><span class="sxs-lookup"><span data-stu-id="51ba2-156">[Indexing a Table][Index]</span></span>
- <span data-ttu-id="51ba2-157">[分割資料表][Partition]</span><span class="sxs-lookup"><span data-stu-id="51ba2-157">[Partitioning a Table][Partition]</span></span>
- <span data-ttu-id="51ba2-158">[維護資料表統計資料][Statistics]</span><span class="sxs-lookup"><span data-stu-id="51ba2-158">[Maintaining Table Statistics][Statistics]</span></span>
- <span data-ttu-id="51ba2-159">[暫存資料表][Temporary]</span><span class="sxs-lookup"><span data-stu-id="51ba2-159">[Temporary Tables][Temporary]</span></span>

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
