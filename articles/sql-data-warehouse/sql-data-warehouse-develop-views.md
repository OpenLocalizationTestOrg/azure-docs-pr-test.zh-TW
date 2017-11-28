---
title: "在 Azure SQL 資料倉儲中使用 T-SQL 檢視 | Microsoft Docs"
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
ms.openlocfilehash: d2a03be810bd7f792876607ec735eb578b65a3b5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="views-in-sql-data-warehouse"></a><span data-ttu-id="17855-103">SQL 資料倉儲中的檢視</span><span class="sxs-lookup"><span data-stu-id="17855-103">Views in SQL Data Warehouse</span></span>
<span data-ttu-id="17855-104">在 SQL 資料倉儲中檢視特別有用。</span><span class="sxs-lookup"><span data-stu-id="17855-104">Views are particularly useful in SQL Data Warehouse.</span></span> <span data-ttu-id="17855-105">以許多不同的方式使用，可以提升您的方案品質。</span><span class="sxs-lookup"><span data-stu-id="17855-105">They can be used in a number of different ways to improve the quality of your solution.</span></span>  <span data-ttu-id="17855-106">本文特別強調幾個範例，說明如何以檢視來豐富您的解決方案，以及需要考量的限制。</span><span class="sxs-lookup"><span data-stu-id="17855-106">This article highlights a few examples of how to enrich your solution with views, as well as the limitations that need to be considered.</span></span>

> [!NOTE]
> <span data-ttu-id="17855-107">本文中不會討論 `CREATE VIEW` 的語法。</span><span class="sxs-lookup"><span data-stu-id="17855-107">Syntax for `CREATE VIEW` is not discussed in this article.</span></span> <span data-ttu-id="17855-108">如需此參考資訊，請參閱 MSDN 上的 [CREATE VIEW][CREATE VIEW] 文章。</span><span class="sxs-lookup"><span data-stu-id="17855-108">Please refer to the [CREATE VIEW][CREATE VIEW] article on MSDN for this reference information.</span></span>
> 
> 

## <a name="architectural-abstraction"></a><span data-ttu-id="17855-109">架構抽象概念</span><span class="sxs-lookup"><span data-stu-id="17855-109">Architectural abstraction</span></span>
<span data-ttu-id="17855-110">極為常見的應用程式模式就是在載入資料時，使用後面接著物件重新命名模式的 CREATE TABLE AS SELECT (CTAS) 來重建資料表。</span><span class="sxs-lookup"><span data-stu-id="17855-110">A very common application pattern is to re-create tables using CREATE TABLE AS SELECT (CTAS) followed by an object renaming pattern whilst loading data.</span></span>

<span data-ttu-id="17855-111">下列範例會將新的日期記錄加入至日期維度。</span><span class="sxs-lookup"><span data-stu-id="17855-111">The example below adds new date records to a date dimension.</span></span> <span data-ttu-id="17855-112">請注意新的資料表 DimDate_New 最初是如何建立，然後重新命名，以取代原始版本的資料表。</span><span class="sxs-lookup"><span data-stu-id="17855-112">Note how a new tabble, DimDate_New, is first created and then renamed to replace the original version of the table.</span></span>

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

RENAME OBJECT DimDate TO DimDate_Old;
RENAME OBJECT DimDate_New TO DimDate;

```

<span data-ttu-id="17855-113">不過，此方法可能導致資料表在使用者的檢視中出現和消失，還有「資料表不存在」錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="17855-113">However, this approach can result in tables appearing and disappearing from a user's view as well as "table does not exist" error messages.</span></span> <span data-ttu-id="17855-114">儘管基礎物件已重新命名，檢視可為使用者提供一致的展示層。</span><span class="sxs-lookup"><span data-stu-id="17855-114">Views can be used to provide users with a consistent presentation layer whilst the underlying objects are renamed.</span></span> <span data-ttu-id="17855-115">透過檢視讓使用者存取資料，意味著使用者不需要看見基礎資料表。</span><span class="sxs-lookup"><span data-stu-id="17855-115">By providing users access to the data through a views, means users don't need to have visibility of the underlying tables.</span></span> <span data-ttu-id="17855-116">這會提供一致的使用者經驗，同時確保資料倉儲設計人員可以發展資料模型，也可在資料載入過程中使用 CTAS 充分發揮效能。</span><span class="sxs-lookup"><span data-stu-id="17855-116">This provides a consistent user experience while ensuring that the data warehouse designers can evolve the data model and maximize performance by using CTAS during the data loading process.</span></span>    

## <a name="performance-optimization"></a><span data-ttu-id="17855-117">效能最佳化</span><span class="sxs-lookup"><span data-stu-id="17855-117">Performance optimization</span></span>
<span data-ttu-id="17855-118">檢視也可用來強化資料表之間的效能最佳化聯結。</span><span class="sxs-lookup"><span data-stu-id="17855-118">Views can also be utilized to enforce performance optimized joins between tables.</span></span> <span data-ttu-id="17855-119">例如，檢視可以納入備援散發金鑰作為聯結準則的一部分，以將資料移動最小化。</span><span class="sxs-lookup"><span data-stu-id="17855-119">For example, a view can incorporate a redundant distribution key as part of the joining criteria to minimize data movement.</span></span>  <span data-ttu-id="17855-120">檢視的另一項好處是強制執行特定查詢或聯結提示。</span><span class="sxs-lookup"><span data-stu-id="17855-120">Another benefit of a view could be to force a specific query or joining hint.</span></span> <span data-ttu-id="17855-121">以這種方式使用檢視，可確保一律以最佳方式執行聯結，使用者不需要記住其聯結的正確建構。</span><span class="sxs-lookup"><span data-stu-id="17855-121">Using views in this manner guarantees that joins are always performed in an optimal fashion avoiding the need for users to remember the correct construct for their joins.</span></span>

## <a name="limitations"></a><span data-ttu-id="17855-122">限制</span><span class="sxs-lookup"><span data-stu-id="17855-122">Limitations</span></span>
<span data-ttu-id="17855-123">SQL 資料倉儲中的檢視僅限中繼資料使用。</span><span class="sxs-lookup"><span data-stu-id="17855-123">Views in SQL Data Warehouse are metadata only.</span></span>  <span data-ttu-id="17855-124">因此無法使用下列選項︰</span><span class="sxs-lookup"><span data-stu-id="17855-124">Consequently the following options are not available:</span></span>

* <span data-ttu-id="17855-125">沒有結構描述繫結選項</span><span class="sxs-lookup"><span data-stu-id="17855-125">There is no schema binding option</span></span>
* <span data-ttu-id="17855-126">無法透過檢視更新基底資料表</span><span class="sxs-lookup"><span data-stu-id="17855-126">Base tables cannot be updated through the view</span></span>
* <span data-ttu-id="17855-127">無法在暫存資料表上建立檢視</span><span class="sxs-lookup"><span data-stu-id="17855-127">Views cannot be created over temporary tables</span></span>
* <span data-ttu-id="17855-128">不支援 EXPAND / NOEXPAND 提示</span><span class="sxs-lookup"><span data-stu-id="17855-128">There is no support for the EXPAND / NOEXPAND hints</span></span>
* <span data-ttu-id="17855-129">SQL 資料倉儲中沒有索引檢視表</span><span class="sxs-lookup"><span data-stu-id="17855-129">There are no indexed views in SQL Data Warehouse</span></span>

## <a name="next-steps"></a><span data-ttu-id="17855-130">後續步驟</span><span class="sxs-lookup"><span data-stu-id="17855-130">Next steps</span></span>
<span data-ttu-id="17855-131">如需更多開發秘訣，請參閱 [SQL 資料倉儲開發概觀][SQL Data Warehouse development overview]。</span><span class="sxs-lookup"><span data-stu-id="17855-131">For more development tips, see [SQL Data Warehouse development overview][SQL Data Warehouse development overview].</span></span>
<span data-ttu-id="17855-132">如需 `CREATE VIEW` 語法，請參閱 [CREATE VIEW][CREATE VIEW]。</span><span class="sxs-lookup"><span data-stu-id="17855-132">For `CREATE VIEW` syntax please refer to [CREATE VIEW][CREATE VIEW].</span></span>

<!--Image references-->

<!--Article references-->
[SQL Data Warehouse development overview]: ./sql-data-warehouse-overview-develop.md

<!--MSDN references-->
[CREATE VIEW]: https://msdn.microsoft.com/en-us/library/ms187956.aspx

<!--Other Web references-->
