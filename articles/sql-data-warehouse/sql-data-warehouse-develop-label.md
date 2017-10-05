---
title: "在 SQL 資料倉儲中使用標籤來檢測查詢 | Microsoft Docs"
description: "在 Azure SQL 資料倉儲中使用標籤來檢測查詢以開發解決方案的秘訣。"
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
ms.openlocfilehash: 9e75bbe528a427724a623305fbd45e2277e9d0af
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="use-labels-to-instrument-queries-in-sql-data-warehouse"></a><span data-ttu-id="2b0a1-103">在 SQL 資料倉儲中使用標籤來檢測查詢</span><span class="sxs-lookup"><span data-stu-id="2b0a1-103">Use labels to instrument queries in SQL Data Warehouse</span></span>
<span data-ttu-id="2b0a1-104">SQL 資料倉儲支援稱為查詢標籤的概念。</span><span class="sxs-lookup"><span data-stu-id="2b0a1-104">SQL Data Warehouse supports a concept called query labels.</span></span> <span data-ttu-id="2b0a1-105">繼續進行之前，讓我們看看一個範例：</span><span class="sxs-lookup"><span data-stu-id="2b0a1-105">Before going into any depth let's look at an example of one:</span></span>

```sql
SELECT *
FROM sys.tables
OPTION (LABEL = 'My Query Label')
;
```

<span data-ttu-id="2b0a1-106">最後一行將字串 'My Query Label' 標記為查詢。</span><span class="sxs-lookup"><span data-stu-id="2b0a1-106">This last line tags the string 'My Query Label' to the query.</span></span> <span data-ttu-id="2b0a1-107">這是特別有幫助的動作，因為標籤可透過 DMV 查詢。</span><span class="sxs-lookup"><span data-stu-id="2b0a1-107">This is particularly helpful as the label is query-able through the DMVs.</span></span> <span data-ttu-id="2b0a1-108">這提供一種機制，可追蹤問題查詢，也可以協助透過 ETL 執行識別進度。</span><span class="sxs-lookup"><span data-stu-id="2b0a1-108">This provides us with a mechanism to track down problem queries and also to help identify progress through an ETL run.</span></span>

<span data-ttu-id="2b0a1-109">此時良好的命名慣例非常有幫助。</span><span class="sxs-lookup"><span data-stu-id="2b0a1-109">A good naming convention really helps here.</span></span> <span data-ttu-id="2b0a1-110">例如，類似 ' PROJECT : PROCEDURE : STATEMENT : COMMENT' 的項目有助於在原始檔控制中的幾乎所有程式碼中唯一識別查詢。</span><span class="sxs-lookup"><span data-stu-id="2b0a1-110">For example something like ' PROJECT : PROCEDURE : STATEMENT : COMMENT' would help to uniquely identify the query in amongst all the code in source control.</span></span>

<span data-ttu-id="2b0a1-111">若要根據標籤搜尋，您可以使用下列使用動態管理檢視的查詢：</span><span class="sxs-lookup"><span data-stu-id="2b0a1-111">To search by label you can use the following query that uses the dynamic management views:</span></span>

```sql
SELECT  *
FROM    sys.dm_pdw_exec_requests r
WHERE   r.[label] = 'My Query Label'
;
```

> [!NOTE]
> <span data-ttu-id="2b0a1-112">請務必在查詢時以方括弧或雙引號括住文字標籤。</span><span class="sxs-lookup"><span data-stu-id="2b0a1-112">It is essential that you wrap square brackets or double quotes around the word label when querying.</span></span> <span data-ttu-id="2b0a1-113">標籤是一個保留的文字，而且如果未分隔，就會造成錯誤。</span><span class="sxs-lookup"><span data-stu-id="2b0a1-113">Label is a reserved word and will caused an error if it has not been delimited.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="2b0a1-114">後續步驟</span><span class="sxs-lookup"><span data-stu-id="2b0a1-114">Next steps</span></span>
<span data-ttu-id="2b0a1-115">如需更多開發秘訣，請參閱[開發概觀][development overview]。</span><span class="sxs-lookup"><span data-stu-id="2b0a1-115">For more development tips, see [development overview][development overview].</span></span>

<!--Image references-->

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md

<!--MSDN references-->

<!--Other Web references-->
