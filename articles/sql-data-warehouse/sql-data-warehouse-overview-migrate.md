---
title: "將您的解決方案移轉至 SQL 資料倉儲 | Microsoft Docs"
description: "將您的解決方案帶入 Azure SQL 資料倉儲平台的移轉指導。"
services: sql-data-warehouse
documentationcenter: NA
author: sqlmojo
manager: jhubbard
editor: 
ms.assetid: 198365eb-7451-4222-b99c-d1d9ef687f1b
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: migrate
ms.date: 06/27/2017
ms.author: joeyong;barbkess
ms.openlocfilehash: 771b9456e66b8a1e41f72340b695b19e2adaf793
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="migrate-your-solution-to-azure-sql-data-warehouse"></a><span data-ttu-id="9414d-103">將您的解決方案移轉至 Azure SQL 資料倉儲</span><span class="sxs-lookup"><span data-stu-id="9414d-103">Migrate your solution to Azure SQL Data Warehouse</span></span>
<span data-ttu-id="9414d-104">查看將現有資料庫解決方案移轉至 Azure SQL 資料倉儲所需採取的步驟。</span><span class="sxs-lookup"><span data-stu-id="9414d-104">See what's involved in migrating an existing database solution to Azure SQL Data Warehouse.</span></span> 

## <a name="profile-your-workload"></a><span data-ttu-id="9414d-105">分析工作負載</span><span class="sxs-lookup"><span data-stu-id="9414d-105">Profile your workload</span></span>
<span data-ttu-id="9414d-106">在移轉之前，您應該要確定 SQL 資料倉儲是您工作負載的正確解決方案。</span><span class="sxs-lookup"><span data-stu-id="9414d-106">Before migrating, you want to be certain SQL Data Warehouse is the right solution for your workload.</span></span> <span data-ttu-id="9414d-107">SQL 資料倉儲是分散式系統，是為了針對大型資料執行分析而設計。</span><span class="sxs-lookup"><span data-stu-id="9414d-107">SQL Data Warehouse is a distributed system designed to perform analytics on large data.</span></span>  <span data-ttu-id="9414d-108">移轉至 SQL 資料倉儲需要一些設計變更，這些變更並不會太難了解，但可能需要一些時間來實作。</span><span class="sxs-lookup"><span data-stu-id="9414d-108">Migrating to SQL Data Warehouse requires some design changes that are not too hard to understand but might take some time to implement.</span></span> <span data-ttu-id="9414d-109">但如果您的業務需要企業級的資料倉儲，它所帶來的優點將值得您投入時間和精力。</span><span class="sxs-lookup"><span data-stu-id="9414d-109">If your business requires an enterprise-class data warehouse, the benefits are worth the effort.</span></span> <span data-ttu-id="9414d-110">不過，如果您不需要 SQL 資料倉儲的功能，使用 SQL Server 或 Azure SQL Database 將會比較符合成本效益。</span><span class="sxs-lookup"><span data-stu-id="9414d-110">However, if you don't need the power of SQL Data Warehouse, it is more cost-effective to use SQL Server or Azure SQL Database.</span></span>

<span data-ttu-id="9414d-111">可考慮使用 SQL 資料倉儲的時機如下：</span><span class="sxs-lookup"><span data-stu-id="9414d-111">Consider using SQL Data Warehouse when you:</span></span>
- <span data-ttu-id="9414d-112">具有超過 1 TB 的資料</span><span class="sxs-lookup"><span data-stu-id="9414d-112">Have one or more Terabytes of data</span></span>
- <span data-ttu-id="9414d-113">規劃對大量資料執行分析</span><span class="sxs-lookup"><span data-stu-id="9414d-113">Plan to run analytics on large amounts of data</span></span>
- <span data-ttu-id="9414d-114">需要調整計算和儲存體的功能</span><span class="sxs-lookup"><span data-stu-id="9414d-114">Need the ability to scale compute and storage</span></span> 
- <span data-ttu-id="9414d-115">想要在不需要時暫停計算資源來節省成本。</span><span class="sxs-lookup"><span data-stu-id="9414d-115">Want to save costs by pausing compute resources when you don't need them.</span></span>

<span data-ttu-id="9414d-116">不要使用 SQL 資料倉儲進行具備以下條件的操作 (OLTP) 工作負載：</span><span class="sxs-lookup"><span data-stu-id="9414d-116">Don't use SQL Data Warehouse for operational (OLTP) workloads that have:</span></span>
- <span data-ttu-id="9414d-117">高頻率的讀取和寫入</span><span class="sxs-lookup"><span data-stu-id="9414d-117">High frequency reads and writes</span></span>
- <span data-ttu-id="9414d-118">大量的單一項目選取</span><span class="sxs-lookup"><span data-stu-id="9414d-118">Large numbers of singleton selects</span></span>
- <span data-ttu-id="9414d-119">大量的單一資料列插入</span><span class="sxs-lookup"><span data-stu-id="9414d-119">High volumes of single row inserts</span></span>
- <span data-ttu-id="9414d-120">逐一處理資料列的需求</span><span class="sxs-lookup"><span data-stu-id="9414d-120">Row by row processing needs</span></span>
- <span data-ttu-id="9414d-121">不相容的格式 (JSON、XML)</span><span class="sxs-lookup"><span data-stu-id="9414d-121">Incompatible formats (JSON, XML)</span></span>


## <a name="plan-the-migration"></a><span data-ttu-id="9414d-122">規劃移轉</span><span class="sxs-lookup"><span data-stu-id="9414d-122">Plan the migration</span></span>

<span data-ttu-id="9414d-123">一旦您決定將現有解決方案移轉至 SQL 資料倉儲，在開始移轉之前，請務必事先規劃。</span><span class="sxs-lookup"><span data-stu-id="9414d-123">Once you have decided to migrate an existing solution to SQL Data Warehouse, it is important to plan the migration before getting started.</span></span> 

<span data-ttu-id="9414d-124">規劃的目標之一是為了確保您的資料、資料表結構描述，以及程式碼皆能與 SQL 資料倉儲相容。</span><span class="sxs-lookup"><span data-stu-id="9414d-124">One goal of planning is to ensure your data, your table schemas, and your code are compatible with SQL Data Warehouse.</span></span> <span data-ttu-id="9414d-125">您目前的系統與 SQL 資料倉儲之間有一些需要解決的相容性差異。</span><span class="sxs-lookup"><span data-stu-id="9414d-125">There are some compatibility differences to work around between your current system and SQL Data Warehouse.</span></span> <span data-ttu-id="9414d-126">此外，將大量資料移轉至 Azure 需花費大量的時間。</span><span class="sxs-lookup"><span data-stu-id="9414d-126">Plus, migrating large amounts of data to Azure takes time.</span></span> <span data-ttu-id="9414d-127">謹慎規劃可加快將資料移轉至 Azure 的速度。</span><span class="sxs-lookup"><span data-stu-id="9414d-127">Careful planning expedites getting your data to Azure.</span></span> 

<span data-ttu-id="9414d-128">規劃的另一個目標是做出設計上的調整，以確保您的解決方案能利用 SQL 資料倉儲的設計所提供的高查詢效能。</span><span class="sxs-lookup"><span data-stu-id="9414d-128">Another goal of planning is to make design adjustments to ensure your solution takes advantage of the high query performance SQL Data Warehouse is designed to provide.</span></span> <span data-ttu-id="9414d-129">由於針對延展性設計資料倉儲帶來了不同的設計模式，因此傳統的方法不一定最適合。</span><span class="sxs-lookup"><span data-stu-id="9414d-129">Designing data warehouses for scale introduces different design patterns and so traditional approaches aren't always the best.</span></span> <span data-ttu-id="9414d-130">雖然您可以在移轉之後做出一些設計上的調整，在程序中盡快做出變更將可節省日後時間。</span><span class="sxs-lookup"><span data-stu-id="9414d-130">Although you can make some design adjustments after migration, making changes sooner in the process will save time later.</span></span>

<span data-ttu-id="9414d-131">若要成功執行移轉，您必須移轉資料表結構描述、程式碼及資料。</span><span class="sxs-lookup"><span data-stu-id="9414d-131">To perform a successful migration, you need to migrate your table schemas, your code, and your data.</span></span> <span data-ttu-id="9414d-132">如需這些移轉主題的指引，請參閱：</span><span class="sxs-lookup"><span data-stu-id="9414d-132">For guidance on these migration topics, see:</span></span>

-  [<span data-ttu-id="9414d-133">移轉結構描述</span><span class="sxs-lookup"><span data-stu-id="9414d-133">Migrate your schemas</span></span>](sql-data-warehouse-migrate-schema.md)
-  [<span data-ttu-id="9414d-134">遷移程式碼</span><span class="sxs-lookup"><span data-stu-id="9414d-134">Migrate your code</span></span>](sql-data-warehouse-migrate-code.md)
-  <span data-ttu-id="9414d-135">[移轉資料](sql-data-warehouse-migrate-data.md)。</span><span class="sxs-lookup"><span data-stu-id="9414d-135">[Migrate your data](sql-data-warehouse-migrate-data.md).</span></span> 

<!--
## Perform the migration


## Deploy the solution


## Validate the migration

-->

## <a name="next-steps"></a><span data-ttu-id="9414d-136">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9414d-136">Next steps</span></span>
<span data-ttu-id="9414d-137">CAT (客戶諮詢小組) 也會透過部落格發佈一些實用的 SQL 資料倉儲指引。</span><span class="sxs-lookup"><span data-stu-id="9414d-137">The CAT (Customer Advisory Team) also has some great SQL Data Warehouse guidance, which they publish through blogs.</span></span>  <span data-ttu-id="9414d-138">請瀏覽他們的[將資料移轉到 Azure SQL 資料倉儲的實際作法][Migrating data to Azure SQL Data Warehouse in practice]一文，以取得關於移轉的額外指導方針。</span><span class="sxs-lookup"><span data-stu-id="9414d-138">Take a look at their article, [Migrating data to Azure SQL Data Warehouse in practice][Migrating data to Azure SQL Data Warehouse in practice] for additional guidance on migration.</span></span>

<!--Image references-->

<!--Article references-->

<!--MSDN references-->

<!--Other Web references-->
[Migrating data to Azure SQL Data Warehouse in practice]: https://blogs.msdn.microsoft.com/sqlcat/2016/08/18/migrating-data-to-azure-sql-data-warehouse-in-practice/
