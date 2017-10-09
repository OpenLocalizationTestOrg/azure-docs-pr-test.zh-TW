---
title: "SQL 資料倉儲中的 aaaAssign 變數 |Microsoft 文件"
description: "在 Azure SQL 資料倉儲中指派 TRANSACT-SQL 變數以便開發解決方案的秘訣。"
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: 81ddc7cf-a6ba-4585-91a3-b6ea50f49227
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: t-sql
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: 9de48739bb0af80ff2a117704b31512c680f78d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="assign-variables-in-sql-data-warehouse"></a>在 SQL 資料倉儲中指派變數
SQL 資料倉儲中的變數會設定使用 hello`DECLARE`陳述式或 hello`SET`陳述式。

所有 hello 下列都是正常的方式 tooset 變數的值：

## <a name="setting-variables-with-declare"></a>使用 DECLARE 設定宣告
初始化與宣告的變數是其中一個最有彈性的方式 tooset hello SQL 資料倉儲中的變數值。

```sql
DECLARE @v  int = 0
;
```

您也可以使用 DECLARE tooset 多個變數一次。 您無法使用`SELECT`或`UPDATE`toodo 這樣：

```sql
DECLARE @v  INT = (SELECT TOP 1 c_customer_sk FROM Customer where c_last_name = 'Smith')
,       @v1 INT = (SELECT TOP 1 c_customer_sk FROM Customer where c_last_name = 'Jones')
;
```

您無法初始化，並使用 hello 中的變數相同的 DECLARE 陳述式。 tooillustrate hello 點 hello 下列範例是**不**允許做為@p1已初始化並 hello 中使用相同的 DECLARE 陳述式。 這會導致錯誤。

```sql
DECLARE @p1 int = 0
,       @p2 int = (SELECT COUNT (*) FROM sys.types where is_user_defined = @p1 )
;
```

## <a name="setting-values-with-set"></a>使用 SET 設定值
SET 是設定單一變數時很常見的方法。

以下的 hello 範例均使用設定來設定變數的有效方法：

```sql
SET     @v = (Select max(database_id) from sys.databases);
SET     @v = 1;
SET     @v = @v+1;
SET     @v +=1;
```

您一次只能使用 SET 設定一個變數。 不過，如上所示，可允許複合運算子。

## <a name="limitations"></a>限制
您無法使用 SELECT 或 UPDATE 進行變數指派。

## <a name="next-steps"></a>後續步驟
如需更多開發秘訣，請參閱[開發概觀][development overview]。

<!--Image references-->

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md

<!--MSDN references-->

<!--Other Web references-->
