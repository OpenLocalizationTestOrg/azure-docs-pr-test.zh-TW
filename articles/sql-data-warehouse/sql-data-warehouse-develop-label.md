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
# <a name="use-labels-tooinstrument-queries-in-sql-data-warehouse"></a><span data-ttu-id="0d4be-103">使用 SQL 資料倉儲中的標籤 tooinstrument 查詢</span><span class="sxs-lookup"><span data-stu-id="0d4be-103">Use labels tooinstrument queries in SQL Data Warehouse</span></span>
<span data-ttu-id="0d4be-104">SQL 資料倉儲支援稱為查詢標籤的概念。</span><span class="sxs-lookup"><span data-stu-id="0d4be-104">SQL Data Warehouse supports a concept called query labels.</span></span> <span data-ttu-id="0d4be-105">繼續進行之前，讓我們看看一個範例：</span><span class="sxs-lookup"><span data-stu-id="0d4be-105">Before going into any depth let's look at an example of one:</span></span>

```sql
SELECT *
FROM sys.tables
OPTION (LABEL = 'My Query Label')
;
```

<span data-ttu-id="0d4be-106">此最後一行標記 hello 字串 ' 我查詢 Label' toohello 查詢。</span><span class="sxs-lookup"><span data-stu-id="0d4be-106">This last line tags hello string 'My Query Label' toohello query.</span></span> <span data-ttu-id="0d4be-107">這是特別有用，因為 hello 標籤是可查詢透過 hello Dmv。</span><span class="sxs-lookup"><span data-stu-id="0d4be-107">This is particularly helpful as hello label is query-able through hello DMVs.</span></span> <span data-ttu-id="0d4be-108">這提供問題的查詢機制 tootrack 和 toohelp 也識別出 ETL 執行的進度。</span><span class="sxs-lookup"><span data-stu-id="0d4be-108">This provides us with a mechanism tootrack down problem queries and also toohelp identify progress through an ETL run.</span></span>

<span data-ttu-id="0d4be-109">此時良好的命名慣例非常有幫助。</span><span class="sxs-lookup"><span data-stu-id="0d4be-109">A good naming convention really helps here.</span></span> <span data-ttu-id="0d4be-110">如需範例類似 '專案： 程序： 陳述式： 註解' 會有幫助 toouniquely 識別在原始檔控制中的所有 hello 程式碼中的 hello 查詢。</span><span class="sxs-lookup"><span data-stu-id="0d4be-110">For example something like ' PROJECT : PROCEDURE : STATEMENT : COMMENT' would help toouniquely identify hello query in amongst all hello code in source control.</span></span>

<span data-ttu-id="0d4be-111">您可以使用下列查詢會使用 hello 標籤 toosearch hello 動態管理檢視：</span><span class="sxs-lookup"><span data-stu-id="0d4be-111">toosearch by label you can use hello following query that uses hello dynamic management views:</span></span>

```sql
SELECT  *
FROM    sys.dm_pdw_exec_requests r
WHERE   r.[label] = 'My Query Label'
;
```

> [!NOTE]
> <span data-ttu-id="0d4be-112">請務必查詢時，您包裝方括號或雙引號括住 hello 字的標籤。</span><span class="sxs-lookup"><span data-stu-id="0d4be-112">It is essential that you wrap square brackets or double quotes around hello word label when querying.</span></span> <span data-ttu-id="0d4be-113">標籤是一個保留的文字，而且如果未分隔，就會造成錯誤。</span><span class="sxs-lookup"><span data-stu-id="0d4be-113">Label is a reserved word and will caused an error if it has not been delimited.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="0d4be-114">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0d4be-114">Next steps</span></span>
<span data-ttu-id="0d4be-115">如需更多開發秘訣，請參閱[開發概觀][development overview]。</span><span class="sxs-lookup"><span data-stu-id="0d4be-115">For more development tips, see [development overview][development overview].</span></span>

<!--Image references-->

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md

<!--MSDN references-->

<!--Other Web references-->
