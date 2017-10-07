---
title: "SQL 資料倉儲中的 aaaStored 程序 |Microsoft 文件"
description: "在 Azure SQL 資料倉儲中實作預存程序以便開發解決方案的秘訣。"
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: 9b238789-6efe-4820-bf77-5a5da2afa0e8
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: t-sql
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: 416252dd3dea95c66aa5e886860b933b22578002
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="stored-procedures-in-sql-data-warehouse"></a>SQL 資料倉儲中的預存程序
SQL 資料倉儲可支援許多 SQL Server 中的 hello TRANSACT-SQL 功能。 更重要的是有向外延展，我們將需要您的方案 tooleverage toomaximize hello 效能的特定功能。

不過，toomaintain hello 規模和 SQL 資料倉儲的效能有還有一些功能和已有些許差異，以及其他不支援的功能。

本文說明 tooimplement 儲存 SQL 資料倉儲內的程序的方式。

## <a name="introducing-stored-procedures"></a>預存程序簡介
預存程序很適合用來封裝您的 SQL 程式碼;它關閉 tooyour 將資料儲存在 hello 資料倉儲。 藉由 hello 程式碼封裝成可管理單位預存程序協助開發人員模塊化其方案中。促進大於 re-usability 的程式碼。 每個預存程序也可以接受參數 toomake 它們更有彈性。

SQL 資料倉儲提供簡化且更簡化的預存程序實作。 hello 最大差異比較的 tooSQL 伺服器 hello 預存程序，不是先行編譯的程式碼。 在資料倉儲我們關心通常較不 hello 編譯時間。 來得更重要的是針對大型資料磁碟區時，正確 optimised hello 預存程序程式碼。 hello 目標是 toosave 小時、 分鐘和秒鐘不毫秒為單位。 因此，是預存程序的更有幫助 toothink 做為 SQL 邏輯的容器。     

當 SQL 資料倉儲執行預存程序 hello SQL 陳述式會剖析、 轉譯和最佳化在執行階段。 在此過程中，每個陳述式都會轉換為分散式查詢。 提交的不同 toohello 查詢 hello hello 資料對實際執行的 SQL 程式碼。

## <a name="nesting-stored-procedures"></a>巢狀預存程序
當預存程序呼叫其他預存程序，或執行動態 sql，則 hello 內部預存程序或程式碼引動過程即稱為 toobe 巢狀。

SQL 資料倉儲最多支援 8 個巢狀層級。 這是稍有不同 tooSQL 伺服器。 SQL Server 中的 hello 巢狀層級為 32。

hello 上方層級的預存程序呼叫等同 toonest 層級 1

```sql
EXEC prc_nesting
```
如果 hello 預存程序也可以呼叫另一個 EXEC，則這會增加 hello 巢狀層級 too2

```sql
CREATE PROCEDURE prc_nesting
AS
EXEC prc_nesting_2  -- This call is nest level 2
GO
EXEC prc_nesting
```
如果 hello 第二個程序，然後執行一些動態 sql 然後這樣會增加 hello 巢狀層級 too3

```sql
CREATE PROCEDURE prc_nesting_2
AS
EXEC sp_executesql 'SELECT 'another nest level'  -- This call is nest level 2
GO
EXEC prc_nesting
```

請注意，SQL 資料倉儲目前不支援 @@NESTLEVEL。 您將自己需要 tookeep 您巢狀層級的追蹤記錄。 不太會叫用 hello 8 巢狀層級的限制，但如果您執行您將需要 toore 工作程式碼和 「 簡化 」 它，使其符合此限制內。

## <a name="insertexecute"></a>INSERT..EXECUTE
SQL 資料倉儲不允許您 tooconsume hello 結果集的 INSERT 陳述式的預存程序。 不過，您可以使用另一個方法。

請參閱下列文章 toohello[暫存資料表]如何例如 toodo 這。

## <a name="limitations"></a>限制
在 SQL 資料倉儲中不會實作 TRANSACT-SQL 預存程序的有些層面。

如下：

* 暫存預存程序
* 編號預存程序
* 擴充預存程序
* CLR 預存程序
* 加密選項
* 複寫選項
* 資料表值參數
* 唯讀參數
* 預設參數
* 執行內容
* return 陳述式

## <a name="next-steps"></a>後續步驟
如需更多開發秘訣，請參閱[開發概觀][development overview]。

<!--Image references-->

<!--Article references-->
[暫存資料表]: ./sql-data-warehouse-tables-temporary.md#modularizing-code
[development overview]: ./sql-data-warehouse-overview-develop.md

<!--MSDN references-->
[nest level]: https://msdn.microsoft.com/library/ms187371.aspx

<!--Other Web references-->
