---
title: "開發 Azure 中的資料倉儲 aaaResources |Microsoft 文件"
description: "SQL 資料倉儲的開發概念、設計決策、建議和程式碼撰寫技巧。"
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: barbkess
editor: 
ms.assetid: 996e3afc-c21c-4e21-b9df-997f953f6dfd
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: develop
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: 67e3a6a3e2664919c3445ea5d5eba251054de020
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="design-decisions-and-coding-techniques-for-sql-data-warehouse"></a>SQL 資料倉儲的設計決策和程式碼撰寫技術
看 toobetter 了解這些開發文章關鍵設計決策、 建議和程式碼撰寫技術的 SQL 資料倉儲。

## <a name="key-design-decisions"></a>主要的設計決策
hello 下列文件會強調一些 hello 重要概念和您將需要 toounderstand hello 開發，您使用 SQL 資料倉儲的分散式的資料倉儲的設計決策：

* [連線][connections]
* [並行][concurrency]
* [交易][transactions]
* [使用者定義的結構描述][user-defined schemas]
* [資料表散發][table distribution]
* [資料表索引][table indexes]
* [資料表分割][table partitions]
* [CTAS][CTAS]
* [統計資料][statistics]

## <a name="development-recommendations-and-coding-techniques"></a>開發建議和程式碼撰寫技術
這些文章會強調特定的程式碼撰寫技術、秘訣和建議，用於開發您的 SQL 資料倉儲：

* [預存程序][stored procedures]
* [標籤][labels]
* [檢視][views]
* [暫存資料表][temporary tables]
* [動態 SQL][dynamic SQL]
* [迴圈][looping]
* [依據選項分組][group by options]
* [變數指派][variable assignment]

## <a name="next-steps"></a>後續步驟
一旦您已透過 hello 開發文件看透過 hello [TRANSACT-SQL 參考][ Transact-SQL reference] SQL 資料倉儲的 hello 支援語法的詳細頁面。

<!--Image references-->

<!--Article references-->
[concurrency]: ./sql-data-warehouse-develop-concurrency.md
[connections]: ./sql-data-warehouse-connect-overview.md
[CTAS]: ./sql-data-warehouse-develop-ctas.md
[dynamic SQL]: ./sql-data-warehouse-develop-dynamic-sql.md
[group by options]: ./sql-data-warehouse-develop-group-by-options.md
[labels]: ./sql-data-warehouse-develop-label.md
[looping]: ./sql-data-warehouse-develop-loops.md
[statistics]: ./sql-data-warehouse-tables-statistics.md
[stored procedures]: ./sql-data-warehouse-develop-stored-procedures.md
[table distribution]: ./sql-data-warehouse-tables-distribute.md
[table indexes]: ./sql-data-warehouse-tables-index.md
[table partitions]: ./sql-data-warehouse-tables-partition.md
[temporary tables]: ./sql-data-warehouse-tables-temporary.md
[transactions]: ./sql-data-warehouse-develop-transactions.md
[user-defined schemas]: ./sql-data-warehouse-develop-user-defined-schemas.md
[variable assignment]: ./sql-data-warehouse-develop-variable-assignment.md
[views]: ./sql-data-warehouse-develop-views.md
[Transact-SQL reference]: ./sql-data-warehouse-overview-reference.md

<!--MSDN references-->
[renaming objects]: https://msdn.microsoft.com/library/mt631611.aspx

<!--Other Web references-->
