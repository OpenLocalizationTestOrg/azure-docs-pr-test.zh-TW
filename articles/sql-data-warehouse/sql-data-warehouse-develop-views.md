---
title: "Azure SQL 資料倉儲中的 aaaUsing T-SQL 檢視 |Microsoft 文件"
description: "在 Azure SQL 資料倉儲中使用 Transact-SQL 檢視開發解決方案的秘訣。"
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: b5208f32-8f4a-4056-8788-2adbb253d9fd
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: t-sql
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: 3990b133946621691bdfa4b09523d21867470c74
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="views-in-sql-data-warehouse"></a>SQL 資料倉儲中的檢視
在 SQL 資料倉儲中檢視特別有用。 它們可以用於不同的方式 tooimprove hello 品質的方案的數字。  本文章重點說明如何 tooenrich 檢視，以及需要 toobe hello 限制使用的方案考量的一些範例。

> [!NOTE]
> 本文中不會討論 `CREATE VIEW` 的語法。 請參閱 toohello [CREATE VIEW] [ CREATE VIEW] MSDN 上的文件，這項參考資訊。
> 
> 

## <a name="architectural-abstraction"></a>架構抽象概念
很常見的應用程式模式是 toore-使用 建立資料表 AS 選取 (CTAS) 後面跟著物件重新命名模式，而載入的資料建立資料表。

下列的 hello 範例會新增新的日期記錄 tooa 日期 維度。 請注意新 tabble，DimDate_New，第一次建立的方式，並重新命名的 hello 資料表 tooreplace hello 原始版本。

```sql
CREATE TABLE dbo.DimDate_New
WITH (DISTRIBUTION = ROUND_ROBIN
, CLUSTERED INDEX (DateKey ASC)
)
AS
SELECT *
FROM   dbo.DimDate  AS prod
UNION ALL
SELECT *
FROM   dbo.DimDate_stg AS stg
;

RENAME OBJECT DimDate tooDimDate_Old;
RENAME OBJECT DimDate_New tooDimDate;

```

不過，此方法可能導致資料表在使用者的檢視中出現和消失，還有「資料表不存在」錯誤訊息。 檢視可以使用的 tooprovide 擁有一致的展示層，儘管 hello 基礎物件重新命名。 藉由提供使用者存取 toohello 資料透過檢視中，表示使用者不需要 toohave hello 基礎資料表的可見性。 這提供一致的使用者體驗，同時確保 hello 資料倉儲的設計工具可以發展 hello 資料模型，以及使用 CTAS hello 資料載入程序期間的效能最大化。    

## <a name="performance-optimization"></a>效能最佳化
檢視也可以利用的 tooenforce 效能最佳化的資料表之間的聯結。 例如，檢視可以合併備援散發索引鍵一部分 hello 聯結準則 toominimize 資料移動。  Tooforce 特定查詢或聯結提示，可能是檢視的另一項優點。 使用這種方式中的檢視，可確保聯結一律會以避免使用者 tooremember hello 正確建構其聯結 hello 需要最佳方式執行。

## <a name="limitations"></a>限制
SQL 資料倉儲中的檢視僅限中繼資料使用。  因此不可以使用下列選項的 hello:

* 沒有結構描述繫結選項
* 基底資料表無法透過 hello 檢視更新
* 無法在暫存資料表上建立檢視
* 不支援 hello 展開 / NOEXPAND 提示
* SQL 資料倉儲中沒有索引檢視表

## <a name="next-steps"></a>後續步驟
如需更多開發秘訣，請參閱 [SQL 資料倉儲開發概觀][SQL Data Warehouse development overview]。
如`CREATE VIEW`語法，請參閱太[CREATE VIEW][CREATE VIEW]。

<!--Image references-->

<!--Article references-->
[SQL Data Warehouse development overview]: ./sql-data-warehouse-overview-develop.md

<!--MSDN references-->
[CREATE VIEW]: https://msdn.microsoft.com/en-us/library/ms187956.aspx

<!--Other Web references-->
