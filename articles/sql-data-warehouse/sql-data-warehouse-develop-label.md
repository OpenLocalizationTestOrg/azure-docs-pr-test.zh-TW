---
title: "aaaUse 標籤 tooinstrument SQL 資料倉儲中的查詢 |Microsoft 文件"
description: "使用 Azure SQL 資料倉儲中的標籤 tooinstrument 查詢，來開發方案的秘訣。"
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: 44988de8-04c1-4fed-92be-e1935661a4e8
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: queries
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: 82e7ea98e1417134227f1d7c529fdaf2f1df3853
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-labels-tooinstrument-queries-in-sql-data-warehouse"></a>使用 SQL 資料倉儲中的標籤 tooinstrument 查詢
SQL 資料倉儲支援稱為查詢標籤的概念。 繼續進行之前，讓我們看看一個範例：

```sql
SELECT *
FROM sys.tables
OPTION (LABEL = 'My Query Label')
;
```

此最後一行標記 hello 字串 ' 我查詢 Label' toohello 查詢。 這是特別有用，因為 hello 標籤是可查詢透過 hello Dmv。 這提供問題的查詢機制 tootrack 和 toohelp 也識別出 ETL 執行的進度。

此時良好的命名慣例非常有幫助。 如需範例類似 '專案： 程序： 陳述式： 註解' 會有幫助 toouniquely 識別在原始檔控制中的所有 hello 程式碼中的 hello 查詢。

您可以使用下列查詢會使用 hello 標籤 toosearch hello 動態管理檢視：

```sql
SELECT  *
FROM    sys.dm_pdw_exec_requests r
WHERE   r.[label] = 'My Query Label'
;
```

> [!NOTE]
> 請務必查詢時，您包裝方括號或雙引號括住 hello 字的標籤。 標籤是一個保留的文字，而且如果未分隔，就會造成錯誤。
> 
> 

## <a name="next-steps"></a>後續步驟
如需更多開發秘訣，請參閱[開發概觀][development overview]。

<!--Image references-->

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md

<!--MSDN references-->

<!--Other Web references-->
