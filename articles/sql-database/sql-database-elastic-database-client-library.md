---
title: "aaaBuilding 可擴充的雲端資料庫 |Microsoft 文件"
description: "建置可延展資料庫應用程式的.NET 與 hello 彈性資料庫用戶端程式庫"
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
ms.openlocfilehash: ca34eff2078c0700dee1bc587f264bbfca979eb6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="building-scalable-cloud-databases"></a><span data-ttu-id="16fac-103">建置可調整的雲端資料庫</span><span class="sxs-lookup"><span data-stu-id="16fac-103">Building scalable cloud databases</span></span>
<span data-ttu-id="16fac-104">使用 Azure SQL Database 的可調整工具和功能，可以輕鬆地相應放大資料庫。</span><span class="sxs-lookup"><span data-stu-id="16fac-104">Scaling out databases can be easily accomplished using scalable tools and features for Azure SQL Database.</span></span> <span data-ttu-id="16fac-105">特別是，您可以使用 hello**彈性資料庫用戶端程式庫**toocreate 和管理向外延展資料庫。</span><span class="sxs-lookup"><span data-stu-id="16fac-105">In particular, you can use hello **Elastic Database client library** toocreate and manage scaled-out databases.</span></span> <span data-ttu-id="16fac-106">這項功能可讓您使用成百上千個 Azure SQL 資料庫，輕鬆地開發分區化應用程式。</span><span class="sxs-lookup"><span data-stu-id="16fac-106">This feature lets you easily develop sharded applications using hundreds—or even thousands—of Azure SQL databases.</span></span> <span data-ttu-id="16fac-107">[彈性作業](sql-database-elastic-jobs-powershell.md)接著可以使用的 toohelp 方便管理這些資料庫。</span><span class="sxs-lookup"><span data-stu-id="16fac-107">[Elastic jobs](sql-database-elastic-jobs-powershell.md) can then be used toohelp ease management of these databases.</span></span>

<span data-ttu-id="16fac-108">tooinstall hello 程式庫，請移太[Microsoft.Azure.SqlDatabase.ElasticScale.Client](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/)。</span><span class="sxs-lookup"><span data-stu-id="16fac-108">tooinstall hello library, go too[Microsoft.Azure.SqlDatabase.ElasticScale.Client](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/).</span></span> 

## <a name="documentation"></a><span data-ttu-id="16fac-109">文件</span><span class="sxs-lookup"><span data-stu-id="16fac-109">Documentation</span></span>
1. [<span data-ttu-id="16fac-110">開始使用彈性資料庫工具</span><span class="sxs-lookup"><span data-stu-id="16fac-110">Get started with Elastic Database tools</span></span>](sql-database-elastic-scale-get-started.md)
2. [<span data-ttu-id="16fac-111">彈性資料庫功能</span><span class="sxs-lookup"><span data-stu-id="16fac-111">Elastic Database features</span></span>](sql-database-elastic-scale-introduction.md)
3. [<span data-ttu-id="16fac-112">分區對應管理</span><span class="sxs-lookup"><span data-stu-id="16fac-112">Shard map management</span></span>](sql-database-elastic-scale-shard-map-management.md)
4. [<span data-ttu-id="16fac-113">移轉現有的資料庫 tooscale 外</span><span class="sxs-lookup"><span data-stu-id="16fac-113">Migrate existing databases tooscale-out</span></span>](sql-database-elastic-convert-to-use-elastic-tools.md)
5. [<span data-ttu-id="16fac-114">資料相依路由</span><span class="sxs-lookup"><span data-stu-id="16fac-114">Data dependent routing</span></span>](sql-database-elastic-scale-data-dependent-routing.md)
6. [<span data-ttu-id="16fac-115">多分區查詢</span><span class="sxs-lookup"><span data-stu-id="16fac-115">Multi-shard queries</span></span>](sql-database-elastic-scale-multishard-querying.md)
7. [<span data-ttu-id="16fac-116">使用彈性資料庫工具加入分區</span><span class="sxs-lookup"><span data-stu-id="16fac-116">Adding a shard using Elastic Database tools</span></span>](sql-database-elastic-scale-add-a-shard.md)
8. [<span data-ttu-id="16fac-117">使用彈性資料庫工具和資料列層級安全性的多租用戶應用程式</span><span class="sxs-lookup"><span data-stu-id="16fac-117">Multi-tenant applications with elastic database tools and row-level security</span></span>](sql-database-elastic-tools-multi-tenant-row-level-security.md)
9. [<span data-ttu-id="16fac-118">升級用戶端程式庫應用程式</span><span class="sxs-lookup"><span data-stu-id="16fac-118">Upgrade client library apps</span></span>](sql-database-elastic-scale-upgrade-client-library.md) 
10. [<span data-ttu-id="16fac-119">彈性查詢概觀</span><span class="sxs-lookup"><span data-stu-id="16fac-119">Elastic queries overview</span></span>](sql-database-elastic-query-overview.md)
11. [<span data-ttu-id="16fac-120">彈性資料庫工具字彙</span><span class="sxs-lookup"><span data-stu-id="16fac-120">Elastic database tools glossary</span></span>](sql-database-elastic-scale-glossary.md)
12. [<span data-ttu-id="16fac-121">搭配使用彈性資料庫用戶端程式庫與 Entity Framework</span><span class="sxs-lookup"><span data-stu-id="16fac-121">Elastic Database client library with Entity Framework</span></span>](sql-database-elastic-scale-use-entity-framework-applications-visual-studio.md)
13. [<span data-ttu-id="16fac-122">彈性資料庫用戶端程式庫與 Dapper</span><span class="sxs-lookup"><span data-stu-id="16fac-122">Elastic database client library with Dapper</span></span>](sql-database-elastic-scale-working-with-dapper.md)
14. [<span data-ttu-id="16fac-123">分割合併工具</span><span class="sxs-lookup"><span data-stu-id="16fac-123">Split-merge tool</span></span>](sql-database-elastic-scale-overview-split-and-merge.md)
15. [<span data-ttu-id="16fac-124">分區對應管理員的效能計數器</span><span class="sxs-lookup"><span data-stu-id="16fac-124">Performance counters for shard map manager</span></span>](sql-database-elastic-database-client-library.md) 
16. [<span data-ttu-id="16fac-125">彈性資料庫工具常見問題集</span><span class="sxs-lookup"><span data-stu-id="16fac-125">FAQ for Elastic database tools</span></span>](sql-database-elastic-scale-faq.md)

## <a name="client-capabilities"></a><span data-ttu-id="16fac-126">用戶端功能</span><span class="sxs-lookup"><span data-stu-id="16fac-126">Client capabilities</span></span>
<span data-ttu-id="16fac-127">向外延展應用程式使用*分區化*hello 開發人員以及 hello 系統管理員的挑戰。</span><span class="sxs-lookup"><span data-stu-id="16fac-127">Scaling out applications using *sharding* presents challenges for both hello developer as well as hello administrator.</span></span> <span data-ttu-id="16fac-128">hello 用戶端程式庫會簡化 hello 管理工作所提供的工具，可讓這兩種開發人員和系統管理員管理向外延展資料庫。</span><span class="sxs-lookup"><span data-stu-id="16fac-128">hello client library simplifies hello management tasks by providing tools that let both developers and administrators manage scaled-out databases.</span></span> <span data-ttu-id="16fac-129">在典型的範例中，有許多資料庫，又稱為 「 分區 」，toomanage。</span><span class="sxs-lookup"><span data-stu-id="16fac-129">In a typical example, there are many databases, known as "shards," toomanage.</span></span> <span data-ttu-id="16fac-130">客戶會共置於相同資料庫中的 hello 和一個資料庫，每個客戶 （單一租用戶配置）。</span><span class="sxs-lookup"><span data-stu-id="16fac-130">Customers are co-located in hello same database, and there is one database per customer (a single-tenant scheme).</span></span> <span data-ttu-id="16fac-131">hello 用戶端程式庫包含下列功能：</span><span class="sxs-lookup"><span data-stu-id="16fac-131">hello client library includes these features:</span></span>

- <span data-ttu-id="16fac-132">**分區對應管理**： 建立名為 hello"分區對應管理員 」 的特殊資料庫。</span><span class="sxs-lookup"><span data-stu-id="16fac-132">**Shard Map Management**: A special database called hello "shard map manager" is created.</span></span> <span data-ttu-id="16fac-133">分區對應管理是其分區相關應用程式 toomanage 中繼資料的 hello 功能。</span><span class="sxs-lookup"><span data-stu-id="16fac-133">Shard map management is hello ability for an application toomanage metadata about its shards.</span></span> <span data-ttu-id="16fac-134">開發人員可以使用此功能 tooregister 資料庫作為分區、 描述對應的個別分區化索引鍵或索引鍵範圍 toothose 資料庫，並維護此中繼資料當做 hello 數字及組合的資料庫中發展 tooreflect 容量變更。</span><span class="sxs-lookup"><span data-stu-id="16fac-134">Developers can use this functionality tooregister databases as shards, describe mappings of individual sharding keys or key ranges toothose databases, and maintain this metadata as hello number and composition of databases evolves tooreflect capacity changes.</span></span> <span data-ttu-id="16fac-135">沒有 hello 彈性資料庫用戶端程式庫，您就必須 toospend 大量撰寫 hello 管理程式碼實作分區化時的時間。</span><span class="sxs-lookup"><span data-stu-id="16fac-135">Without hello elastic database client library, you would need toospend a lot of time writing hello management code when implementing sharding.</span></span> <span data-ttu-id="16fac-136">如需詳細資訊，請參閱 [分區對應管理](sql-database-elastic-scale-shard-map-management.md)。</span><span class="sxs-lookup"><span data-stu-id="16fac-136">For details, see [Shard map management](sql-database-elastic-scale-shard-map-management.md).</span></span>

- <span data-ttu-id="16fac-137">**資料依存路由**： 假設傳入 hello 應用程式的要求。</span><span class="sxs-lookup"><span data-stu-id="16fac-137">**Data dependent routing**: Imagine a request coming into hello application.</span></span> <span data-ttu-id="16fac-138">根據 hello 分區化索引鍵值的 hello 要求，必須正確資料庫根據 hello 索引鍵值 toodetermine hello hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="16fac-138">Based on hello sharding key value of hello request, hello application needs toodetermine hello correct database based on hello key value.</span></span> <span data-ttu-id="16fac-139">接著，它會開啟連接 toohello 資料庫 tooprocess hello 要求。</span><span class="sxs-lookup"><span data-stu-id="16fac-139">It then opens a connection toohello database tooprocess hello request.</span></span> <span data-ttu-id="16fac-140">資料依存路由提供 hello 能力 tooopen 連線透過 hello 分區對應到單一輕鬆呼叫 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="16fac-140">Data dependent routing provides hello ability tooopen connections with a single easy call into hello shard map of hello application.</span></span> <span data-ttu-id="16fac-141">資料依存路由是現在 hello 彈性資料庫用戶端程式庫中的功能所涵蓋的基礎結構程式碼的其他區域。</span><span class="sxs-lookup"><span data-stu-id="16fac-141">Data dependent routing was another area of infrastructure code that is now covered by functionality in hello elastic database client library.</span></span> <span data-ttu-id="16fac-142">如需詳細資訊，請參閱 [資料相依路由](sql-database-elastic-scale-data-dependent-routing.md)。</span><span class="sxs-lookup"><span data-stu-id="16fac-142">For details, see [Data dependent routing](sql-database-elastic-scale-data-dependent-routing.md).</span></span>
- <span data-ttu-id="16fac-143">**多分區查詢 (MSQ)**：當要求牽涉到數個 (或所有) 分區時，多分區查詢就派上用場。</span><span class="sxs-lookup"><span data-stu-id="16fac-143">**Multi-shard queries (MSQ)**: Multi-shard querying works when a request involves several (or all) shards.</span></span> <span data-ttu-id="16fac-144">執行多個分區查詢 hello 所有分區或分區的一組相同的 T-SQL 程式碼。</span><span class="sxs-lookup"><span data-stu-id="16fac-144">A multi-shard query executes hello same T-SQL code on all shards or a set of shards.</span></span> <span data-ttu-id="16fac-145">從參與分區的 hello hello 結果會合併到整體的結果集使用 UNION ALL 的語意。</span><span class="sxs-lookup"><span data-stu-id="16fac-145">hello results from hello participating shards are merged into an overall result set using UNION ALL semantics.</span></span> <span data-ttu-id="16fac-146">hello 所透過 hello 用戶端程式庫公開的功能會處理許多工作，包括： 連線管理、 執行緒管理、 錯誤處理和處理的中繼結果。</span><span class="sxs-lookup"><span data-stu-id="16fac-146">hello functionality as exposed through hello client library handles many tasks, including: connection management, thread management, fault handling and intermediate results processing.</span></span> <span data-ttu-id="16fac-147">MSQ 可以向上 toohundreds 分區的查詢。</span><span class="sxs-lookup"><span data-stu-id="16fac-147">MSQ can query up toohundreds of shards.</span></span> <span data-ttu-id="16fac-148">如需詳細資訊，請參閱 [多分區查詢](sql-database-elastic-scale-multishard-querying.md)。</span><span class="sxs-lookup"><span data-stu-id="16fac-148">For details, see [Multi-shard querying](sql-database-elastic-scale-multishard-querying.md).</span></span>

<span data-ttu-id="16fac-149">一般情況下，使用彈性資料庫工具的客戶可以預期 tooget 完整 T-SQL 功能，做為有自己的語意，但不要的 toocross 分區作業提交分區本機作業時。</span><span class="sxs-lookup"><span data-stu-id="16fac-149">In general, customers using elastic database tools can expect tooget full T-SQL functionality when submitting shard-local operations as opposed toocross-shard operations that have their own semantics.</span></span>

## <a name="next-steps"></a><span data-ttu-id="16fac-150">後續步驟</span><span class="sxs-lookup"><span data-stu-id="16fac-150">Next steps</span></span>
<span data-ttu-id="16fac-151">再試一次 hello[範例應用程式](sql-database-elastic-scale-get-started.md)示範 hello 用戶端功能。</span><span class="sxs-lookup"><span data-stu-id="16fac-151">Try hello [sample app](sql-database-elastic-scale-get-started.md) which demonstrates hello client functions.</span></span> 

<span data-ttu-id="16fac-152">tooinstall hello 程式庫，請移太[彈性資料庫用戶端程式庫](http://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/)。</span><span class="sxs-lookup"><span data-stu-id="16fac-152">tooinstall hello library, go too[Elastic Database Client Library](http://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/).</span></span>

<span data-ttu-id="16fac-153">如需使用 hello 分割合併工具的指示，請參閱 hello[分割合併工具概觀](sql-database-elastic-scale-overview-split-and-merge.md)。</span><span class="sxs-lookup"><span data-stu-id="16fac-153">For instructions on using hello split-merge tool, see hello [split-merge tool overview](sql-database-elastic-scale-overview-split-and-merge.md).</span></span>

[<span data-ttu-id="16fac-154">彈性資料庫用戶端程式庫現在已開放原始碼！</span><span class="sxs-lookup"><span data-stu-id="16fac-154">Elastic database client library is now open sourced!</span></span>](https://azure.microsoft.com/blog/elastic-database-client-library-is-now-open-sourced/)

<span data-ttu-id="16fac-155">使用 [彈性查詢](sql-database-elastic-query-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="16fac-155">Use [Elastic queries](sql-database-elastic-query-overview.md).</span></span>

<span data-ttu-id="16fac-156">hello 程式庫可做為開放原始碼軟體上[GitHub](https://github.com/Azure/elastic-db-tools)。</span><span class="sxs-lookup"><span data-stu-id="16fac-156">hello library is available as open source software on [GitHub](https://github.com/Azure/elastic-db-tools).</span></span> 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Anchors-->
<!--Image references-->
[1]:./media/sql-database-elastic-database-client-library/glossary.png

