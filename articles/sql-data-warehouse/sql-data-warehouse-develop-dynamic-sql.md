---
title: "SQL 資料倉儲中的 SQL aaaDynamic |Microsoft 文件"
description: "使用 Azure SQL 資料倉儲中的動態 SQL 以開發解決方案的秘訣。"
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: a948c2c3-3cd1-4373-90a9-79e59414b778
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: queries
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: 4d66eecb37621510f657d1ec9a2a935daaa16052
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="dynamic-sql-in-sql-data-warehouse"></a>SQL 資料倉儲中的動態 SQL
SQL 資料倉儲，您可以開發應用程式程式碼時 toouse 動態 sql toohelp 需要提供彈性、 泛型且模組化的解決方案。 不過，SQL 資料倉儲目前不支援 Blob 資料類型。 這可能會限制字串 hello 大小做為 blob 類型包括 varchar （max） 和 nvarchar （max） 類型。 如果您已在應用程式程式碼中使用這些類型，建立非常大的字串時，您需要 toobreak hello 程式碼區塊和使用 hello EXEC 陳述式改為。

以下是簡單的範例：

```sql
DECLARE @sql_fragment1 VARCHAR(8000)=' SELECT name '
,       @sql_fragment2 VARCHAR(8000)=' FROM sys.system_views '
,       @sql_fragment3 VARCHAR(8000)=' WHERE name like ''%table%''';

EXEC( @sql_fragment1 + @sql_fragment2 + @sql_fragment3);
```

如果字串 hello 短，您可以使用[sp_executesql] [ sp_executesql]正常。

> [!NOTE]
> 執行當做動態 SQL 陳述式仍會主旨 tooall TSQL 驗證規則。
> 
> 

## <a name="next-steps"></a>後續步驟
如需更多開發秘訣，請參閱[開發概觀][development overview]。

<!--Image references-->

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md

<!--MSDN references-->
[sp_executesql]: https://msdn.microsoft.com/library/ms188001.aspx

<!--Other Web references-->
