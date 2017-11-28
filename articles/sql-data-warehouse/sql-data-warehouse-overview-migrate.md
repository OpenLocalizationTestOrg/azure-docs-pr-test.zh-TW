---
title: "aaaMigrate 您方案 tooSQL 資料倉儲 |Microsoft 文件"
description: "讓您的方案 tooAzure SQL 資料倉儲平台的移轉指導方針。"
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
ms.openlocfilehash: 27b51f15247603f054070f360ede7f24541c0288
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-your-solution-tooazure-sql-data-warehouse"></a><span data-ttu-id="90139-103">移轉您的方案 tooAzure SQL 資料倉儲</span><span class="sxs-lookup"><span data-stu-id="90139-103">Migrate your solution tooAzure SQL Data Warehouse</span></span>
<span data-ttu-id="90139-104">移轉現有的資料庫方案 tooAzure SQL 資料倉儲相關資訊，請參閱。</span><span class="sxs-lookup"><span data-stu-id="90139-104">See what's involved in migrating an existing database solution tooAzure SQL Data Warehouse.</span></span> 

## <a name="profile-your-workload"></a><span data-ttu-id="90139-105">分析工作負載</span><span class="sxs-lookup"><span data-stu-id="90139-105">Profile your workload</span></span>
<span data-ttu-id="90139-106">然後再移轉，您會想 toobe 特定 SQL 資料倉儲是 hello 絕佳的解決方案，您的工作負載。</span><span class="sxs-lookup"><span data-stu-id="90139-106">Before migrating, you want toobe certain SQL Data Warehouse is hello right solution for your workload.</span></span> <span data-ttu-id="90139-107">SQL 資料倉儲是針對大型資料進行分散式的系統設計 tooperform 分析。</span><span class="sxs-lookup"><span data-stu-id="90139-107">SQL Data Warehouse is a distributed system designed tooperform analytics on large data.</span></span>  <span data-ttu-id="90139-108">移轉 tooSQL 資料倉儲需要一些不太難 toounderstand，但可能需要一些時間 tooimplement 的設計變更。</span><span class="sxs-lookup"><span data-stu-id="90139-108">Migrating tooSQL Data Warehouse requires some design changes that are not too hard toounderstand but might take some time tooimplement.</span></span> <span data-ttu-id="90139-109">如果您的業務需求的企業級資料倉儲，hello 優點是值得 hello。</span><span class="sxs-lookup"><span data-stu-id="90139-109">If your business requires an enterprise-class data warehouse, hello benefits are worth hello effort.</span></span> <span data-ttu-id="90139-110">不過，如果您不需要的 SQL 資料倉儲的 hello 電源，則更多符合成本效益 toouse SQL Server 或 Azure SQL Database。</span><span class="sxs-lookup"><span data-stu-id="90139-110">However, if you don't need hello power of SQL Data Warehouse, it is more cost-effective toouse SQL Server or Azure SQL Database.</span></span>

<span data-ttu-id="90139-111">可考慮使用 SQL 資料倉儲的時機如下：</span><span class="sxs-lookup"><span data-stu-id="90139-111">Consider using SQL Data Warehouse when you:</span></span>
- <span data-ttu-id="90139-112">具有超過 1 TB 的資料</span><span class="sxs-lookup"><span data-stu-id="90139-112">Have one or more Terabytes of data</span></span>
- <span data-ttu-id="90139-113">計劃 toorun 分析大量資料</span><span class="sxs-lookup"><span data-stu-id="90139-113">Plan toorun analytics on large amounts of data</span></span>
- <span data-ttu-id="90139-114">需要 hello 能力 tooscale 運算和存放裝置</span><span class="sxs-lookup"><span data-stu-id="90139-114">Need hello ability tooscale compute and storage</span></span> 
- <span data-ttu-id="90139-115">想要暫停的成本 toosave 計算資源，您不需要它們時。</span><span class="sxs-lookup"><span data-stu-id="90139-115">Want toosave costs by pausing compute resources when you don't need them.</span></span>

<span data-ttu-id="90139-116">不要使用 SQL 資料倉儲進行具備以下條件的操作 (OLTP) 工作負載：</span><span class="sxs-lookup"><span data-stu-id="90139-116">Don't use SQL Data Warehouse for operational (OLTP) workloads that have:</span></span>
- <span data-ttu-id="90139-117">高頻率的讀取和寫入</span><span class="sxs-lookup"><span data-stu-id="90139-117">High frequency reads and writes</span></span>
- <span data-ttu-id="90139-118">大量的單一項目選取</span><span class="sxs-lookup"><span data-stu-id="90139-118">Large numbers of singleton selects</span></span>
- <span data-ttu-id="90139-119">大量的單一資料列插入</span><span class="sxs-lookup"><span data-stu-id="90139-119">High volumes of single row inserts</span></span>
- <span data-ttu-id="90139-120">逐一處理資料列的需求</span><span class="sxs-lookup"><span data-stu-id="90139-120">Row by row processing needs</span></span>
- <span data-ttu-id="90139-121">不相容的格式 (JSON、XML)</span><span class="sxs-lookup"><span data-stu-id="90139-121">Incompatible formats (JSON, XML)</span></span>


## <a name="plan-hello-migration"></a><span data-ttu-id="90139-122">計劃 hello 移轉</span><span class="sxs-lookup"><span data-stu-id="90139-122">Plan hello migration</span></span>

<span data-ttu-id="90139-123">一旦您已決定 toomigrate 現有的方案 tooSQL 資料倉儲，就是開始使用之前的重要 tooplan hello 移轉。</span><span class="sxs-lookup"><span data-stu-id="90139-123">Once you have decided toomigrate an existing solution tooSQL Data Warehouse, it is important tooplan hello migration before getting started.</span></span> 

<span data-ttu-id="90139-124">計劃的其中一個目標是 tooensure 您的資料，您的資料表結構描述，且您的程式碼與 SQL 資料倉儲相容。</span><span class="sxs-lookup"><span data-stu-id="90139-124">One goal of planning is tooensure your data, your table schemas, and your code are compatible with SQL Data Warehouse.</span></span> <span data-ttu-id="90139-125">有一些相容性的差異 toowork 周圍您目前的系統與 SQL 資料倉儲之間。</span><span class="sxs-lookup"><span data-stu-id="90139-125">There are some compatibility differences toowork around between your current system and SQL Data Warehouse.</span></span> <span data-ttu-id="90139-126">此外，移轉大量資料 tooAzure 花費的時間。</span><span class="sxs-lookup"><span data-stu-id="90139-126">Plus, migrating large amounts of data tooAzure takes time.</span></span> <span data-ttu-id="90139-127">務必先謹慎規劃，可以加速取得資料 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="90139-127">Careful planning expedites getting your data tooAzure.</span></span> 

<span data-ttu-id="90139-128">另一個計劃的目標是您的方案會利用 SQL 資料倉儲是 hello 高的查詢效能調整 tooensure 設計 tooprovide toomake 設計。</span><span class="sxs-lookup"><span data-stu-id="90139-128">Another goal of planning is toomake design adjustments tooensure your solution takes advantage of hello high query performance SQL Data Warehouse is designed tooprovide.</span></span> <span data-ttu-id="90139-129">設計資料倉儲，標尺的介紹不同的設計模式，因此傳統方法不一定 hello 最佳。</span><span class="sxs-lookup"><span data-stu-id="90139-129">Designing data warehouses for scale introduces different design patterns and so traditional approaches aren't always hello best.</span></span> <span data-ttu-id="90139-130">雖然您可以在移轉之後進行一些設計調整，更快地 hello 程序中進行變更會儲存之後的時間。</span><span class="sxs-lookup"><span data-stu-id="90139-130">Although you can make some design adjustments after migration, making changes sooner in hello process will save time later.</span></span>

<span data-ttu-id="90139-131">您需要 toomigrate tooperform 移轉成功，您的資料表結構描述、 程式碼和您的資料。</span><span class="sxs-lookup"><span data-stu-id="90139-131">tooperform a successful migration, you need toomigrate your table schemas, your code, and your data.</span></span> <span data-ttu-id="90139-132">如需這些移轉主題的指引，請參閱：</span><span class="sxs-lookup"><span data-stu-id="90139-132">For guidance on these migration topics, see:</span></span>

-  [<span data-ttu-id="90139-133">移轉結構描述</span><span class="sxs-lookup"><span data-stu-id="90139-133">Migrate your schemas</span></span>](sql-data-warehouse-migrate-schema.md)
-  [<span data-ttu-id="90139-134">遷移程式碼</span><span class="sxs-lookup"><span data-stu-id="90139-134">Migrate your code</span></span>](sql-data-warehouse-migrate-code.md)
-  <span data-ttu-id="90139-135">[移轉資料](sql-data-warehouse-migrate-data.md)。</span><span class="sxs-lookup"><span data-stu-id="90139-135">[Migrate your data](sql-data-warehouse-migrate-data.md).</span></span> 

<!--
## Perform hello migration


## Deploy hello solution


## Validate hello migration

-->

## <a name="next-steps"></a><span data-ttu-id="90139-136">後續步驟</span><span class="sxs-lookup"><span data-stu-id="90139-136">Next steps</span></span>
<span data-ttu-id="90139-137">hello CAT （客戶諮詢小組） 也會有它們透過部落格發行一些很棒 SQL 資料倉儲指引。</span><span class="sxs-lookup"><span data-stu-id="90139-137">hello CAT (Customer Advisory Team) also has some great SQL Data Warehouse guidance, which they publish through blogs.</span></span>  <span data-ttu-id="90139-138">看看他們的文件：[移轉資料 tooAzure SQL 資料倉儲實際上][ Migrating data tooAzure SQL Data Warehouse in practice]如需有關移轉的其他指引。</span><span class="sxs-lookup"><span data-stu-id="90139-138">Take a look at their article, [Migrating data tooAzure SQL Data Warehouse in practice][Migrating data tooAzure SQL Data Warehouse in practice] for additional guidance on migration.</span></span>

<!--Image references-->

<!--Article references-->

<!--MSDN references-->

<!--Other Web references-->
[Migrating data tooAzure SQL Data Warehouse in practice]: https://blogs.msdn.microsoft.com/sqlcat/2016/08/18/migrating-data-to-azure-sql-data-warehouse-in-practice/
