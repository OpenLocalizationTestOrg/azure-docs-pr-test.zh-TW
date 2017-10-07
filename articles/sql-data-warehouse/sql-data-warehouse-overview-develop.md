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
# <a name="design-decisions-and-coding-techniques-for-sql-data-warehouse"></a><span data-ttu-id="8e52d-103">SQL 資料倉儲的設計決策和程式碼撰寫技術</span><span class="sxs-lookup"><span data-stu-id="8e52d-103">Design decisions and coding techniques for SQL Data Warehouse</span></span>
<span data-ttu-id="8e52d-104">看 toobetter 了解這些開發文章關鍵設計決策、 建議和程式碼撰寫技術的 SQL 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="8e52d-104">Take a look through these development articles toobetter understand key design decisions, recommendations and coding techniques for SQL Data Warehouse.</span></span>

## <a name="key-design-decisions"></a><span data-ttu-id="8e52d-105">主要的設計決策</span><span class="sxs-lookup"><span data-stu-id="8e52d-105">Key design decisions</span></span>
<span data-ttu-id="8e52d-106">hello 下列文件會強調一些 hello 重要概念和您將需要 toounderstand hello 開發，您使用 SQL 資料倉儲的分散式的資料倉儲的設計決策：</span><span class="sxs-lookup"><span data-stu-id="8e52d-106">hello following articles highlight some of hello key concepts and design decisions you will need toounderstand for hello development of your distributed data warehouse using SQL Data Warehouse:</span></span>

* <span data-ttu-id="8e52d-107">[連線][connections]</span><span class="sxs-lookup"><span data-stu-id="8e52d-107">[connections][connections]</span></span>
* <span data-ttu-id="8e52d-108">[並行][concurrency]</span><span class="sxs-lookup"><span data-stu-id="8e52d-108">[concurrency][concurrency]</span></span>
* <span data-ttu-id="8e52d-109">[交易][transactions]</span><span class="sxs-lookup"><span data-stu-id="8e52d-109">[transactions][transactions]</span></span>
* <span data-ttu-id="8e52d-110">[使用者定義的結構描述][user-defined schemas]</span><span class="sxs-lookup"><span data-stu-id="8e52d-110">[user-defined schemas][user-defined schemas]</span></span>
* <span data-ttu-id="8e52d-111">[資料表散發][table distribution]</span><span class="sxs-lookup"><span data-stu-id="8e52d-111">[table distribution][table distribution]</span></span>
* <span data-ttu-id="8e52d-112">[資料表索引][table indexes]</span><span class="sxs-lookup"><span data-stu-id="8e52d-112">[table indexes][table indexes]</span></span>
* <span data-ttu-id="8e52d-113">[資料表分割][table partitions]</span><span class="sxs-lookup"><span data-stu-id="8e52d-113">[table partitions][table partitions]</span></span>
* <span data-ttu-id="8e52d-114">[CTAS][CTAS]</span><span class="sxs-lookup"><span data-stu-id="8e52d-114">[CTAS][CTAS]</span></span>
* <span data-ttu-id="8e52d-115">[統計資料][statistics]</span><span class="sxs-lookup"><span data-stu-id="8e52d-115">[statistics][statistics]</span></span>

## <a name="development-recommendations-and-coding-techniques"></a><span data-ttu-id="8e52d-116">開發建議和程式碼撰寫技術</span><span class="sxs-lookup"><span data-stu-id="8e52d-116">Development recommendations and coding techniques</span></span>
<span data-ttu-id="8e52d-117">這些文章會強調特定的程式碼撰寫技術、秘訣和建議，用於開發您的 SQL 資料倉儲：</span><span class="sxs-lookup"><span data-stu-id="8e52d-117">These articles highlight specific coding techniques, tips and recommendations for developing your SQL Data Warehouse:</span></span>

* <span data-ttu-id="8e52d-118">[預存程序][stored procedures]</span><span class="sxs-lookup"><span data-stu-id="8e52d-118">[stored procedures][stored procedures]</span></span>
* <span data-ttu-id="8e52d-119">[標籤][labels]</span><span class="sxs-lookup"><span data-stu-id="8e52d-119">[labels][labels]</span></span>
* <span data-ttu-id="8e52d-120">[檢視][views]</span><span class="sxs-lookup"><span data-stu-id="8e52d-120">[views][views]</span></span>
* <span data-ttu-id="8e52d-121">[暫存資料表][temporary tables]</span><span class="sxs-lookup"><span data-stu-id="8e52d-121">[temporary tables][temporary tables]</span></span>
* <span data-ttu-id="8e52d-122">[動態 SQL][dynamic SQL]</span><span class="sxs-lookup"><span data-stu-id="8e52d-122">[dynamic SQL][dynamic SQL]</span></span>
* <span data-ttu-id="8e52d-123">[迴圈][looping]</span><span class="sxs-lookup"><span data-stu-id="8e52d-123">[looping][looping]</span></span>
* <span data-ttu-id="8e52d-124">[依據選項分組][group by options]</span><span class="sxs-lookup"><span data-stu-id="8e52d-124">[group by options][group by options]</span></span>
* <span data-ttu-id="8e52d-125">[變數指派][variable assignment]</span><span class="sxs-lookup"><span data-stu-id="8e52d-125">[variable assignment][variable assignment]</span></span>

## <a name="next-steps"></a><span data-ttu-id="8e52d-126">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8e52d-126">Next steps</span></span>
<span data-ttu-id="8e52d-127">一旦您已透過 hello 開發文件看透過 hello [TRANSACT-SQL 參考][ Transact-SQL reference] SQL 資料倉儲的 hello 支援語法的詳細頁面。</span><span class="sxs-lookup"><span data-stu-id="8e52d-127">Once you have been through hello development articles take a look through hello [Transact-SQL reference][Transact-SQL reference] page for more details on hello supported syntax for SQL Data Warehouse.</span></span>

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
