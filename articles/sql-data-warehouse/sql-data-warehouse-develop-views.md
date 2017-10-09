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
# <a name="views-in-sql-data-warehouse"></a><span data-ttu-id="dc733-103">SQL 資料倉儲中的檢視</span><span class="sxs-lookup"><span data-stu-id="dc733-103">Views in SQL Data Warehouse</span></span>
<span data-ttu-id="dc733-104">在 SQL 資料倉儲中檢視特別有用。</span><span class="sxs-lookup"><span data-stu-id="dc733-104">Views are particularly useful in SQL Data Warehouse.</span></span> <span data-ttu-id="dc733-105">它們可以用於不同的方式 tooimprove hello 品質的方案的數字。</span><span class="sxs-lookup"><span data-stu-id="dc733-105">They can be used in a number of different ways tooimprove hello quality of your solution.</span></span>  <span data-ttu-id="dc733-106">本文章重點說明如何 tooenrich 檢視，以及需要 toobe hello 限制使用的方案考量的一些範例。</span><span class="sxs-lookup"><span data-stu-id="dc733-106">This article highlights a few examples of how tooenrich your solution with views, as well as hello limitations that need toobe considered.</span></span>

> [!NOTE]
> <span data-ttu-id="dc733-107">本文中不會討論 `CREATE VIEW` 的語法。</span><span class="sxs-lookup"><span data-stu-id="dc733-107">Syntax for `CREATE VIEW` is not discussed in this article.</span></span> <span data-ttu-id="dc733-108">請參閱 toohello [CREATE VIEW] [ CREATE VIEW] MSDN 上的文件，這項參考資訊。</span><span class="sxs-lookup"><span data-stu-id="dc733-108">Please refer toohello [CREATE VIEW][CREATE VIEW] article on MSDN for this reference information.</span></span>
> 
> 

## <a name="architectural-abstraction"></a><span data-ttu-id="dc733-109">架構抽象概念</span><span class="sxs-lookup"><span data-stu-id="dc733-109">Architectural abstraction</span></span>
<span data-ttu-id="dc733-110">很常見的應用程式模式是 toore-使用 建立資料表 AS 選取 (CTAS) 後面跟著物件重新命名模式，而載入的資料建立資料表。</span><span class="sxs-lookup"><span data-stu-id="dc733-110">A very common application pattern is toore-create tables using CREATE TABLE AS SELECT (CTAS) followed by an object renaming pattern whilst loading data.</span></span>

<span data-ttu-id="dc733-111">下列的 hello 範例會新增新的日期記錄 tooa 日期 維度。</span><span class="sxs-lookup"><span data-stu-id="dc733-111">hello example below adds new date records tooa date dimension.</span></span> <span data-ttu-id="dc733-112">請注意新 tabble，DimDate_New，第一次建立的方式，並重新命名的 hello 資料表 tooreplace hello 原始版本。</span><span class="sxs-lookup"><span data-stu-id="dc733-112">Note how a new tabble, DimDate_New, is first created and then renamed tooreplace hello original version of hello table.</span></span>

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

<span data-ttu-id="dc733-113">不過，此方法可能導致資料表在使用者的檢視中出現和消失，還有「資料表不存在」錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="dc733-113">However, this approach can result in tables appearing and disappearing from a user's view as well as "table does not exist" error messages.</span></span> <span data-ttu-id="dc733-114">檢視可以使用的 tooprovide 擁有一致的展示層，儘管 hello 基礎物件重新命名。</span><span class="sxs-lookup"><span data-stu-id="dc733-114">Views can be used tooprovide users with a consistent presentation layer whilst hello underlying objects are renamed.</span></span> <span data-ttu-id="dc733-115">藉由提供使用者存取 toohello 資料透過檢視中，表示使用者不需要 toohave hello 基礎資料表的可見性。</span><span class="sxs-lookup"><span data-stu-id="dc733-115">By providing users access toohello data through a views, means users don't need toohave visibility of hello underlying tables.</span></span> <span data-ttu-id="dc733-116">這提供一致的使用者體驗，同時確保 hello 資料倉儲的設計工具可以發展 hello 資料模型，以及使用 CTAS hello 資料載入程序期間的效能最大化。</span><span class="sxs-lookup"><span data-stu-id="dc733-116">This provides a consistent user experience while ensuring that hello data warehouse designers can evolve hello data model and maximize performance by using CTAS during hello data loading process.</span></span>    

## <a name="performance-optimization"></a><span data-ttu-id="dc733-117">效能最佳化</span><span class="sxs-lookup"><span data-stu-id="dc733-117">Performance optimization</span></span>
<span data-ttu-id="dc733-118">檢視也可以利用的 tooenforce 效能最佳化的資料表之間的聯結。</span><span class="sxs-lookup"><span data-stu-id="dc733-118">Views can also be utilized tooenforce performance optimized joins between tables.</span></span> <span data-ttu-id="dc733-119">例如，檢視可以合併備援散發索引鍵一部分 hello 聯結準則 toominimize 資料移動。</span><span class="sxs-lookup"><span data-stu-id="dc733-119">For example, a view can incorporate a redundant distribution key as part of hello joining criteria toominimize data movement.</span></span>  <span data-ttu-id="dc733-120">Tooforce 特定查詢或聯結提示，可能是檢視的另一項優點。</span><span class="sxs-lookup"><span data-stu-id="dc733-120">Another benefit of a view could be tooforce a specific query or joining hint.</span></span> <span data-ttu-id="dc733-121">使用這種方式中的檢視，可確保聯結一律會以避免使用者 tooremember hello 正確建構其聯結 hello 需要最佳方式執行。</span><span class="sxs-lookup"><span data-stu-id="dc733-121">Using views in this manner guarantees that joins are always performed in an optimal fashion avoiding hello need for users tooremember hello correct construct for their joins.</span></span>

## <a name="limitations"></a><span data-ttu-id="dc733-122">限制</span><span class="sxs-lookup"><span data-stu-id="dc733-122">Limitations</span></span>
<span data-ttu-id="dc733-123">SQL 資料倉儲中的檢視僅限中繼資料使用。</span><span class="sxs-lookup"><span data-stu-id="dc733-123">Views in SQL Data Warehouse are metadata only.</span></span>  <span data-ttu-id="dc733-124">因此不可以使用下列選項的 hello:</span><span class="sxs-lookup"><span data-stu-id="dc733-124">Consequently hello following options are not available:</span></span>

* <span data-ttu-id="dc733-125">沒有結構描述繫結選項</span><span class="sxs-lookup"><span data-stu-id="dc733-125">There is no schema binding option</span></span>
* <span data-ttu-id="dc733-126">基底資料表無法透過 hello 檢視更新</span><span class="sxs-lookup"><span data-stu-id="dc733-126">Base tables cannot be updated through hello view</span></span>
* <span data-ttu-id="dc733-127">無法在暫存資料表上建立檢視</span><span class="sxs-lookup"><span data-stu-id="dc733-127">Views cannot be created over temporary tables</span></span>
* <span data-ttu-id="dc733-128">不支援 hello 展開 / NOEXPAND 提示</span><span class="sxs-lookup"><span data-stu-id="dc733-128">There is no support for hello EXPAND / NOEXPAND hints</span></span>
* <span data-ttu-id="dc733-129">SQL 資料倉儲中沒有索引檢視表</span><span class="sxs-lookup"><span data-stu-id="dc733-129">There are no indexed views in SQL Data Warehouse</span></span>

## <a name="next-steps"></a><span data-ttu-id="dc733-130">後續步驟</span><span class="sxs-lookup"><span data-stu-id="dc733-130">Next steps</span></span>
<span data-ttu-id="dc733-131">如需更多開發秘訣，請參閱 [SQL 資料倉儲開發概觀][SQL Data Warehouse development overview]。</span><span class="sxs-lookup"><span data-stu-id="dc733-131">For more development tips, see [SQL Data Warehouse development overview][SQL Data Warehouse development overview].</span></span>
<span data-ttu-id="dc733-132">如`CREATE VIEW`語法，請參閱太[CREATE VIEW][CREATE VIEW]。</span><span class="sxs-lookup"><span data-stu-id="dc733-132">For `CREATE VIEW` syntax please refer too[CREATE VIEW][CREATE VIEW].</span></span>

<!--Image references-->

<!--Article references-->
[SQL Data Warehouse development overview]: ./sql-data-warehouse-overview-develop.md

<!--MSDN references-->
[CREATE VIEW]: https://msdn.microsoft.com/en-us/library/ms187956.aspx

<!--Other Web references-->
