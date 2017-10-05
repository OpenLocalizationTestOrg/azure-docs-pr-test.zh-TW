---
title: "建置可調整的雲端資料庫 | Microsoft Docs"
description: "使用彈性資料庫用戶端程式庫建置可調整的 .NET 資料庫應用程式"
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: 1f11c52d-13c1-4994-b9b1-5b1ae2f9255f
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/06/2016
ms.author: ddove
ms.openlocfilehash: 0128b333f04847ab646dcb0759fcef5f7e86ffd9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="building-scalable-cloud-databases"></a><span data-ttu-id="ee7ee-103">建置可調整的雲端資料庫</span><span class="sxs-lookup"><span data-stu-id="ee7ee-103">Building scalable cloud databases</span></span>
<span data-ttu-id="ee7ee-104">使用 Azure SQL Database 的可調整工具和功能，可以輕鬆地相應放大資料庫。</span><span class="sxs-lookup"><span data-stu-id="ee7ee-104">Scaling out databases can be easily accomplished using scalable tools and features for Azure SQL Database.</span></span> <span data-ttu-id="ee7ee-105">特別是，您可以使用 **彈性資料庫用戶端程式庫** 來建立和管理相應放大的資料庫。</span><span class="sxs-lookup"><span data-stu-id="ee7ee-105">In particular, you can use the **Elastic Database client library** to create and manage scaled-out databases.</span></span> <span data-ttu-id="ee7ee-106">這項功能可讓您使用成百上千個 Azure SQL 資料庫，輕鬆地開發分區化應用程式。</span><span class="sxs-lookup"><span data-stu-id="ee7ee-106">This feature lets you easily develop sharded applications using hundreds—or even thousands—of Azure SQL databases.</span></span> <span data-ttu-id="ee7ee-107">[彈性工作](sql-database-elastic-jobs-powershell.md) 則可用來協助簡化管理這些資料庫。</span><span class="sxs-lookup"><span data-stu-id="ee7ee-107">[Elastic jobs](sql-database-elastic-jobs-powershell.md) can then be used to help ease management of these databases.</span></span>

<span data-ttu-id="ee7ee-108">若要安裝程式庫，請移至 [Microsoft.Azure.SqlDatabase.ElasticScale.Client](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/)。</span><span class="sxs-lookup"><span data-stu-id="ee7ee-108">To install the library, go to [Microsoft.Azure.SqlDatabase.ElasticScale.Client](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/).</span></span> 

## <a name="documentation"></a><span data-ttu-id="ee7ee-109">文件</span><span class="sxs-lookup"><span data-stu-id="ee7ee-109">Documentation</span></span>
1. [<span data-ttu-id="ee7ee-110">開始使用彈性資料庫工具</span><span class="sxs-lookup"><span data-stu-id="ee7ee-110">Get started with Elastic Database tools</span></span>](sql-database-elastic-scale-get-started.md)
2. [<span data-ttu-id="ee7ee-111">彈性資料庫功能</span><span class="sxs-lookup"><span data-stu-id="ee7ee-111">Elastic Database features</span></span>](sql-database-elastic-scale-introduction.md)
3. [<span data-ttu-id="ee7ee-112">分區對應管理</span><span class="sxs-lookup"><span data-stu-id="ee7ee-112">Shard map management</span></span>](sql-database-elastic-scale-shard-map-management.md)
4. [<span data-ttu-id="ee7ee-113">轉換現有的資料庫以使用彈性資料庫工具</span><span class="sxs-lookup"><span data-stu-id="ee7ee-113">Migrate existing databases to scale-out</span></span>](sql-database-elastic-convert-to-use-elastic-tools.md)
5. [<span data-ttu-id="ee7ee-114">資料相依路由</span><span class="sxs-lookup"><span data-stu-id="ee7ee-114">Data dependent routing</span></span>](sql-database-elastic-scale-data-dependent-routing.md)
6. [<span data-ttu-id="ee7ee-115">多分區查詢</span><span class="sxs-lookup"><span data-stu-id="ee7ee-115">Multi-shard queries</span></span>](sql-database-elastic-scale-multishard-querying.md)
7. [<span data-ttu-id="ee7ee-116">使用彈性資料庫工具加入分區</span><span class="sxs-lookup"><span data-stu-id="ee7ee-116">Adding a shard using Elastic Database tools</span></span>](sql-database-elastic-scale-add-a-shard.md)
8. [<span data-ttu-id="ee7ee-117">使用彈性資料庫工具和資料列層級安全性的多租用戶應用程式</span><span class="sxs-lookup"><span data-stu-id="ee7ee-117">Multi-tenant applications with elastic database tools and row-level security</span></span>](sql-database-elastic-tools-multi-tenant-row-level-security.md)
9. [<span data-ttu-id="ee7ee-118">升級用戶端程式庫應用程式</span><span class="sxs-lookup"><span data-stu-id="ee7ee-118">Upgrade client library apps</span></span>](sql-database-elastic-scale-upgrade-client-library.md) 
10. [<span data-ttu-id="ee7ee-119">彈性查詢概觀</span><span class="sxs-lookup"><span data-stu-id="ee7ee-119">Elastic queries overview</span></span>](sql-database-elastic-query-overview.md)
11. [<span data-ttu-id="ee7ee-120">彈性資料庫工具字彙</span><span class="sxs-lookup"><span data-stu-id="ee7ee-120">Elastic database tools glossary</span></span>](sql-database-elastic-scale-glossary.md)
12. [<span data-ttu-id="ee7ee-121">搭配使用彈性資料庫用戶端程式庫與 Entity Framework</span><span class="sxs-lookup"><span data-stu-id="ee7ee-121">Elastic Database client library with Entity Framework</span></span>](sql-database-elastic-scale-use-entity-framework-applications-visual-studio.md)
13. [<span data-ttu-id="ee7ee-122">彈性資料庫用戶端程式庫與 Dapper</span><span class="sxs-lookup"><span data-stu-id="ee7ee-122">Elastic database client library with Dapper</span></span>](sql-database-elastic-scale-working-with-dapper.md)
14. [<span data-ttu-id="ee7ee-123">分割合併工具</span><span class="sxs-lookup"><span data-stu-id="ee7ee-123">Split-merge tool</span></span>](sql-database-elastic-scale-overview-split-and-merge.md)
15. [<span data-ttu-id="ee7ee-124">分區對應管理員的效能計數器</span><span class="sxs-lookup"><span data-stu-id="ee7ee-124">Performance counters for shard map manager</span></span>](sql-database-elastic-database-client-library.md) 
16. [<span data-ttu-id="ee7ee-125">彈性資料庫工具常見問題集</span><span class="sxs-lookup"><span data-stu-id="ee7ee-125">FAQ for Elastic database tools</span></span>](sql-database-elastic-scale-faq.md)

## <a name="client-capabilities"></a><span data-ttu-id="ee7ee-126">用戶端功能</span><span class="sxs-lookup"><span data-stu-id="ee7ee-126">Client capabilities</span></span>
<span data-ttu-id="ee7ee-127">使用分區化  來相應放大應用程式，對開發人員和系統管理員而言都是一項挑戰。</span><span class="sxs-lookup"><span data-stu-id="ee7ee-127">Scaling out applications using *sharding* presents challenges for both the developer as well as the administrator.</span></span> <span data-ttu-id="ee7ee-128">用戶端程式庫藉由提供工具讓開發人員和系統管理員管理相應放大的資料庫，簡化了管理工作。</span><span class="sxs-lookup"><span data-stu-id="ee7ee-128">The client library simplifies the management tasks by providing tools that let both developers and administrators manage scaled-out databases.</span></span> <span data-ttu-id="ee7ee-129">在典型的範例中，有許多稱為「分區」的資料庫要管理。</span><span class="sxs-lookup"><span data-stu-id="ee7ee-129">In a typical example, there are many databases, known as "shards," to manage.</span></span> <span data-ttu-id="ee7ee-130">客戶共置於同一資料庫，而每位客戶 (單一租用戶配置) 一個資料庫。</span><span class="sxs-lookup"><span data-stu-id="ee7ee-130">Customers are co-located in the same database, and there is one database per customer (a single-tenant scheme).</span></span> <span data-ttu-id="ee7ee-131">用戶端程式庫包含下列功能：</span><span class="sxs-lookup"><span data-stu-id="ee7ee-131">The client library includes these features:</span></span>

- <span data-ttu-id="ee7ee-132">**分區對應管理**︰建立了稱為「分區對應管理員」的特殊資料庫。</span><span class="sxs-lookup"><span data-stu-id="ee7ee-132">**Shard Map Management**: A special database called the "shard map manager" is created.</span></span> <span data-ttu-id="ee7ee-133">分區對應管理可讓應用程式管理其分區的中繼資料。</span><span class="sxs-lookup"><span data-stu-id="ee7ee-133">Shard map management is the ability for an application to manage metadata about its shards.</span></span> <span data-ttu-id="ee7ee-134">開發人員可利用此功能將資料庫註冊為分區 (描述個別分區化索引鍵或索引鍵範圍至這些資料庫的對應)，並隨著資料庫的數量和組成發展來維護此中繼資料，以反映容量變更。</span><span class="sxs-lookup"><span data-stu-id="ee7ee-134">Developers can use this functionality to register databases as shards, describe mappings of individual sharding keys or key ranges to those databases, and maintain this metadata as the number and composition of databases evolves to reflect capacity changes.</span></span> <span data-ttu-id="ee7ee-135">若沒有彈性資料庫用戶端程式庫，實作分區化時您必須花費大量時間撰寫管理程式碼。</span><span class="sxs-lookup"><span data-stu-id="ee7ee-135">Without the elastic database client library, you would need to spend a lot of time writing the management code when implementing sharding.</span></span> <span data-ttu-id="ee7ee-136">如需詳細資訊，請參閱 [分區對應管理](sql-database-elastic-scale-shard-map-management.md)。</span><span class="sxs-lookup"><span data-stu-id="ee7ee-136">For details, see [Shard map management](sql-database-elastic-scale-shard-map-management.md).</span></span>

- <span data-ttu-id="ee7ee-137">**資料相依路由**：想像有一個要求進入應用程式。</span><span class="sxs-lookup"><span data-stu-id="ee7ee-137">**Data dependent routing**: Imagine a request coming into the application.</span></span> <span data-ttu-id="ee7ee-138">以要求的分區化索引鍵值為基礎，應用程式必須根據索引鍵值判斷正確的資料庫。</span><span class="sxs-lookup"><span data-stu-id="ee7ee-138">Based on the sharding key value of the request, the application needs to determine the correct database based on the key value.</span></span> <span data-ttu-id="ee7ee-139">接著，它會開啟資料庫連線來處理要求。</span><span class="sxs-lookup"><span data-stu-id="ee7ee-139">It then opens a connection to the database to process the request.</span></span> <span data-ttu-id="ee7ee-140">資料相依路由可讓您輕鬆地呼叫一次應用程式的分區對應，就能開啟連接。</span><span class="sxs-lookup"><span data-stu-id="ee7ee-140">Data dependent routing provides the ability to open connections with a single easy call into the shard map of the application.</span></span> <span data-ttu-id="ee7ee-141">資料相依路由是基礎結構程式碼的另一個領域，現在由彈性資料庫用戶端程式庫中的功能所涵蓋。</span><span class="sxs-lookup"><span data-stu-id="ee7ee-141">Data dependent routing was another area of infrastructure code that is now covered by functionality in the elastic database client library.</span></span> <span data-ttu-id="ee7ee-142">如需詳細資訊，請參閱 [資料相依路由](sql-database-elastic-scale-data-dependent-routing.md)。</span><span class="sxs-lookup"><span data-stu-id="ee7ee-142">For details, see [Data dependent routing](sql-database-elastic-scale-data-dependent-routing.md).</span></span>
- <span data-ttu-id="ee7ee-143">**多分區查詢 (MSQ)**：當要求牽涉到數個 (或所有) 分區時，多分區查詢就派上用場。</span><span class="sxs-lookup"><span data-stu-id="ee7ee-143">**Multi-shard queries (MSQ)**: Multi-shard querying works when a request involves several (or all) shards.</span></span> <span data-ttu-id="ee7ee-144">多分區查詢在所有分區或一組分區上執行相同的 T-SQL 程式碼。</span><span class="sxs-lookup"><span data-stu-id="ee7ee-144">A multi-shard query executes the same T-SQL code on all shards or a set of shards.</span></span> <span data-ttu-id="ee7ee-145">使用 UNION ALL 語意可將參與分區的結果合併成整體的結果集。</span><span class="sxs-lookup"><span data-stu-id="ee7ee-145">The results from the participating shards are merged into an overall result set using UNION ALL semantics.</span></span> <span data-ttu-id="ee7ee-146">經由用戶端程式庫公開的功能可處理許多工作，包括：連接管理、執行緒管理、錯誤處理和中繼結果處理。</span><span class="sxs-lookup"><span data-stu-id="ee7ee-146">The functionality as exposed through the client library handles many tasks, including: connection management, thread management, fault handling and intermediate results processing.</span></span> <span data-ttu-id="ee7ee-147">MSQ 可以查詢多達數百個分區。</span><span class="sxs-lookup"><span data-stu-id="ee7ee-147">MSQ can query up to hundreds of shards.</span></span> <span data-ttu-id="ee7ee-148">如需詳細資訊，請參閱 [多分區查詢](sql-database-elastic-scale-multishard-querying.md)。</span><span class="sxs-lookup"><span data-stu-id="ee7ee-148">For details, see [Multi-shard querying](sql-database-elastic-scale-multishard-querying.md).</span></span>

<span data-ttu-id="ee7ee-149">一般而言，使用彈性資料庫工具的客戶在提交分區內作業，而不是有其本身語意的跨分區作業時，就可以獲得完整的 T-SQL 功能。</span><span class="sxs-lookup"><span data-stu-id="ee7ee-149">In general, customers using elastic database tools can expect to get full T-SQL functionality when submitting shard-local operations as opposed to cross-shard operations that have their own semantics.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ee7ee-150">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ee7ee-150">Next steps</span></span>
<span data-ttu-id="ee7ee-151">請嘗試示範用戶端功能的 [範例應用程式](sql-database-elastic-scale-get-started.md) 。</span><span class="sxs-lookup"><span data-stu-id="ee7ee-151">Try the [sample app](sql-database-elastic-scale-get-started.md) which demonstrates the client functions.</span></span> 

<span data-ttu-id="ee7ee-152">若要安裝文件庫，請移至 [彈性資料庫用戶端程式庫](http://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/)。</span><span class="sxs-lookup"><span data-stu-id="ee7ee-152">To install the library, go to [Elastic Database Client Library](http://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/).</span></span>

<span data-ttu-id="ee7ee-153">如需有關使用分割合併工具的指示，請參閱 [分割合併工具概觀](sql-database-elastic-scale-overview-split-and-merge.md)。</span><span class="sxs-lookup"><span data-stu-id="ee7ee-153">For instructions on using the split-merge tool, see the [split-merge tool overview](sql-database-elastic-scale-overview-split-and-merge.md).</span></span>

[<span data-ttu-id="ee7ee-154">彈性資料庫用戶端程式庫現在已開放原始碼！</span><span class="sxs-lookup"><span data-stu-id="ee7ee-154">Elastic database client library is now open sourced!</span></span>](https://azure.microsoft.com/blog/elastic-database-client-library-is-now-open-sourced/)

<span data-ttu-id="ee7ee-155">使用 [彈性查詢](sql-database-elastic-query-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="ee7ee-155">Use [Elastic queries](sql-database-elastic-query-overview.md).</span></span>

<span data-ttu-id="ee7ee-156">[GitHub](https://github.com/Azure/elastic-db-tools)以開放原始碼軟體的形式提供程式庫。</span><span class="sxs-lookup"><span data-stu-id="ee7ee-156">The library is available as open source software on [GitHub](https://github.com/Azure/elastic-db-tools).</span></span> 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Anchors-->
<!--Image references-->
[1]:./media/sql-database-elastic-database-client-library/glossary.png

