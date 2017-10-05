---
title: "搭配使用彈性資料庫用戶端程式庫與 Dapper | Microsoft Docs"
description: "搭配使用彈性資料庫用戶端程式庫與 Dapper。"
services: sql-database
documentationcenter: 
manager: jhubbard
author: torsteng
ms.assetid: 463d2676-3b19-47c2-83df-f8c50492c9d2
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/27/2016
ms.author: torsteng
ms.openlocfilehash: f0efd37a39c1a60eee7b47304483c27727ca8833
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="using-elastic-database-client-library-with-dapper"></a><span data-ttu-id="bc6f6-103">搭配使用彈性資料庫用戶端程式庫與 Dapper</span><span class="sxs-lookup"><span data-stu-id="bc6f6-103">Using elastic database client library with Dapper</span></span>
<span data-ttu-id="bc6f6-104">本文件適用於下列開發人員︰依賴 Dapper 建置應用程式，但也想利用 [彈性資料庫工具](sql-database-elastic-scale-introduction.md) 建立應用程式，經由實作分區化來相應放大資料層。</span><span class="sxs-lookup"><span data-stu-id="bc6f6-104">This document is for developers that rely on Dapper to build applications, but also want to embrace [elastic database tooling](sql-database-elastic-scale-introduction.md) to create applications that implement sharding to scale-out their data tier.</span></span>  <span data-ttu-id="bc6f6-105">這份文件說明為了與彈性資料庫工具整合，Dapper 應用程式中需要做的變更。</span><span class="sxs-lookup"><span data-stu-id="bc6f6-105">This document illustrates the changes in Dapper-based applications that are necessary to integrate with elastic database tools.</span></span> <span data-ttu-id="bc6f6-106">重點在於使用 Dapper 撰寫彈性資料庫分區管理和資料相依路由。</span><span class="sxs-lookup"><span data-stu-id="bc6f6-106">Our focus is on composing the elastic database shard management and data dependent routing with Dapper.</span></span> 

<span data-ttu-id="bc6f6-107">**範例程式碼**： [Azure SQL Database - Dapper 整合的彈性資料庫工具](https://code.msdn.microsoft.com/Elastic-Scale-with-Azure-e19fc77f)。</span><span class="sxs-lookup"><span data-stu-id="bc6f6-107">**Sample Code**: [Elastic database tools for Azure SQL Database - Dapper integration](https://code.msdn.microsoft.com/Elastic-Scale-with-Azure-e19fc77f).</span></span>

<span data-ttu-id="bc6f6-108">整合 **Dapper** 和 **DapperExtensions** 與 Azure SQL Database 的彈性資料庫用戶端程式庫很容易。</span><span class="sxs-lookup"><span data-stu-id="bc6f6-108">Integrating **Dapper** and **DapperExtensions** with the elastic database client library for Azure SQL Database is easy.</span></span> <span data-ttu-id="bc6f6-109">將新的 [SqlConnection](http://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.aspx) 物件的建立和開啟作業變更為使用[用戶端程式庫](http://msdn.microsoft.com/library/azure/dn765902.aspx)的 [OpenConnectionForKey](http://msdn.microsoft.com/library/azure/dn807226.aspx) 呼叫，您的應用程式即可使用資料相依路由。</span><span class="sxs-lookup"><span data-stu-id="bc6f6-109">Your applications can use data dependent routing by changing the creation and opening of new [SqlConnection](http://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.aspx) objects to use the [OpenConnectionForKey](http://msdn.microsoft.com/library/azure/dn807226.aspx) call from the [client library](http://msdn.microsoft.com/library/azure/dn765902.aspx).</span></span> <span data-ttu-id="bc6f6-110">這會使應用程式中的變更侷限於建立和開啟新連線的位置。</span><span class="sxs-lookup"><span data-stu-id="bc6f6-110">This limits changes in your application to only where new connections are created and opened.</span></span> 

## <a name="dapper-overview"></a><span data-ttu-id="bc6f6-111">Dapper 概觀</span><span class="sxs-lookup"><span data-stu-id="bc6f6-111">Dapper overview</span></span>
<span data-ttu-id="bc6f6-112">**Dapper** 是物件關聯式對應程式。</span><span class="sxs-lookup"><span data-stu-id="bc6f6-112">**Dapper** is an object-relational mapper.</span></span> <span data-ttu-id="bc6f6-113">它可將應用程式的 .NET 物件對應到關聯式資料庫 (反之亦然) 。</span><span class="sxs-lookup"><span data-stu-id="bc6f6-113">It maps .NET objects from your application to a relational database (and vice versa).</span></span> <span data-ttu-id="bc6f6-114">範例程式碼的第一部分說明如何整合彈性資料庫用戶端程式庫與 Dapper 應用程式。</span><span class="sxs-lookup"><span data-stu-id="bc6f6-114">The first part of the sample code illustrates how you can integrate the elastic database client library with Dapper-based applications.</span></span> <span data-ttu-id="bc6f6-115">範例程式碼的第二部分說明如何在同時使用 Dapper 和 DapperExtensions 時進行整合。</span><span class="sxs-lookup"><span data-stu-id="bc6f6-115">The second part of the sample code illustrates how to integrate when using both Dapper and DapperExtensions.</span></span>  

<span data-ttu-id="bc6f6-116">Dapper 的對應程式功能提供資料庫連線的擴充方法，以簡化提交 T-SQL 陳述式以便執行或查詢資料庫。</span><span class="sxs-lookup"><span data-stu-id="bc6f6-116">The mapper functionality in Dapper provides extension methods on database connections that simplify submitting T-SQL statements for execution or querying the database.</span></span> <span data-ttu-id="bc6f6-117">比方說，Dapper 可輕鬆對應 .NET 物件與 **Execute** 呼叫的 SQL 陳述式參數，或取用您從 Dapper 使用 **Query** 呼叫對 .NET 物件進行 SQL 查詢的結果。</span><span class="sxs-lookup"><span data-stu-id="bc6f6-117">For instance, Dapper makes it easy to map between your .NET objects and the parameters of SQL statements for **Execute** calls, or to consume the results of your SQL queries into .NET objects using **Query** calls from Dapper.</span></span> 

<span data-ttu-id="bc6f6-118">使用 DapperExtensions，您不再需要提供 SQL 陳述式。</span><span class="sxs-lookup"><span data-stu-id="bc6f6-118">When using DapperExtensions, you no longer need to provide the SQL statements.</span></span> <span data-ttu-id="bc6f6-119">透過資料庫連接的延伸方法 (如 **GetList** 或 **Insert**) 可在幕後建立 SQL 陳述式。</span><span class="sxs-lookup"><span data-stu-id="bc6f6-119">Extensions methods such as **GetList** or **Insert** over the database connection create the SQL statements behind the scenes.</span></span>

<span data-ttu-id="bc6f6-120">Dapper 以及 DapperExtensions 的另一個好處就是應用程式可控制資料庫連線的建立。</span><span class="sxs-lookup"><span data-stu-id="bc6f6-120">Another benefit of Dapper and also DapperExtensions is that the application controls the creation of the database connection.</span></span> <span data-ttu-id="bc6f6-121">這有助於與彈性資料庫用戶端程式庫互動，該程式庫會根據 Shardlet 與資料庫的對應來代理資料庫連接。</span><span class="sxs-lookup"><span data-stu-id="bc6f6-121">This helps interact with the elastic database client library which brokers database connections based on the mapping of shardlets to databases.</span></span>

<span data-ttu-id="bc6f6-122">若要取得 Dapper 組件，請參閱 [Dapper dot net](http://www.nuget.org/packages/Dapper/)。</span><span class="sxs-lookup"><span data-stu-id="bc6f6-122">To get the Dapper assemblies, see [Dapper dot net](http://www.nuget.org/packages/Dapper/).</span></span> <span data-ttu-id="bc6f6-123">如需 Dapper 延伸模組，請參閱 [DapperExtensions](http://www.nuget.org/packages/DapperExtensions)。</span><span class="sxs-lookup"><span data-stu-id="bc6f6-123">For the Dapper extensions, see [DapperExtensions](http://www.nuget.org/packages/DapperExtensions).</span></span>

## <a name="a-quick-look-at-the-elastic-database-client-library"></a><span data-ttu-id="bc6f6-124">彈性資料庫用戶端程式庫的快速概覽</span><span class="sxs-lookup"><span data-stu-id="bc6f6-124">A quick Look at the elastic database client library</span></span>
<span data-ttu-id="bc6f6-125">透過彈性資料庫用戶端程式庫，您可以定義應用程式資料的資料分割 (稱為 *Shardlet*)、將它們對應到資料庫，以及利用*分區化索引鍵*加以識別。</span><span class="sxs-lookup"><span data-stu-id="bc6f6-125">With the elastic database client library, you define partitions of your application data called *shardlets* , map them to databases, and identify them by *sharding keys*.</span></span> <span data-ttu-id="bc6f6-126">您可以擁有所需數量的資料庫，並將 Shardlet 分散於這些資料庫。</span><span class="sxs-lookup"><span data-stu-id="bc6f6-126">You can have as many databases as you need and distribute your shardlets across these databases.</span></span> <span data-ttu-id="bc6f6-127">分區化索引鍵值到資料庫的對應，由程式庫的 API 所提供的分區對應來儲存。</span><span class="sxs-lookup"><span data-stu-id="bc6f6-127">The mapping of sharding key values to the databases is stored by a shard map provided by the library’s APIs.</span></span> <span data-ttu-id="bc6f6-128">這項功能稱為 **分區對應管理**。</span><span class="sxs-lookup"><span data-stu-id="bc6f6-128">This capability is called **shard map management**.</span></span> <span data-ttu-id="bc6f6-129">對於攜帶分區化索引鍵的要求，分區對應也充當資料庫連接的代理人。</span><span class="sxs-lookup"><span data-stu-id="bc6f6-129">The shard map also serves as the broker of database connections for requests that carry a sharding key.</span></span> <span data-ttu-id="bc6f6-130">這項功能稱為 **資料相依路由**。</span><span class="sxs-lookup"><span data-stu-id="bc6f6-130">This capability is referred to as **data dependent routing**.</span></span>

![分區對應和資料相依路由][1]

<span data-ttu-id="bc6f6-132">分區對應管理員可防止使用者檢視 Shardlet 資料時出現不一致，這種情況發生於資料庫正在進行並行 Shardlet 管理作業時。</span><span class="sxs-lookup"><span data-stu-id="bc6f6-132">The shard map manager protects users from inconsistent views into shardlet data that can occur when concurrent shardlet management operations are happening on the databases.</span></span> <span data-ttu-id="bc6f6-133">在作法上，分區對應會代理以程式庫建置的應用程式的資料庫連接。</span><span class="sxs-lookup"><span data-stu-id="bc6f6-133">To do so, the shard maps broker the database connections for an application built with the library.</span></span> <span data-ttu-id="bc6f6-134">當分區管理作業可能影響 Shardlet 時，即可允許分區對應功能自動終止資料庫連線。</span><span class="sxs-lookup"><span data-stu-id="bc6f6-134">When shard management operations could impact the shardlet, this allows the shard map functionality to automatically kill a database connection.</span></span> 

<span data-ttu-id="bc6f6-135">我們需要使用 [OpenConnectionForKey 方法](http://msdn.microsoft.com/library/azure/dn824099.aspx)來為 Dapper 建立連接，而不使用傳統的方式。</span><span class="sxs-lookup"><span data-stu-id="bc6f6-135">Instead of using the traditional way to create connections for Dapper, we need to use the [OpenConnectionForKey method](http://msdn.microsoft.com/library/azure/dn824099.aspx).</span></span> <span data-ttu-id="bc6f6-136">這可確保所有驗證都會發生，而且在分區之間移動任何資料時會適當地管理連線。</span><span class="sxs-lookup"><span data-stu-id="bc6f6-136">This ensures that all the validation takes place and connections are managed properly when any data moves between shards.</span></span>

### <a name="requirements-for-dapper-integration"></a><span data-ttu-id="bc6f6-137">Dapper 整合需求</span><span class="sxs-lookup"><span data-stu-id="bc6f6-137">Requirements for Dapper integration</span></span>
<span data-ttu-id="bc6f6-138">當使用彈性資料庫用戶端程式庫和 Dapper API 時，我們希望保留下列屬性：</span><span class="sxs-lookup"><span data-stu-id="bc6f6-138">When working with both the elastic database client library and the Dapper APIs, we want to retain the following properties:</span></span>

* <span data-ttu-id="bc6f6-139">**相應放大**：我們想要依需要在分區化應用程式資料層中新增或移除資料庫，以滿足應用程式的容量需求。</span><span class="sxs-lookup"><span data-stu-id="bc6f6-139">**Scaleout**: We want to add or remove databases from the data tier of the sharded application as necessary for the capacity demands of the application.</span></span> 
* <span data-ttu-id="bc6f6-140">**一致性**：由於使用分區化相應放大我們的應用程式，所以我們必須執行資料相依路由。</span><span class="sxs-lookup"><span data-stu-id="bc6f6-140">**Consistency**: Since our application is scaled out using sharding, we need to perform data dependent routing.</span></span> <span data-ttu-id="bc6f6-141">我們想使用程式庫的資料相依路由功能來執行此作業。</span><span class="sxs-lookup"><span data-stu-id="bc6f6-141">We want to use the Data dependent routing capabilities of the library to do so.</span></span> <span data-ttu-id="bc6f6-142">尤其是，我們想要保留透過分區對應管理員代理的連接所提供的驗證和一致性保證，以避免查詢結果損毀或錯誤。</span><span class="sxs-lookup"><span data-stu-id="bc6f6-142">In particular, we want to retain the validation and consistency guarantees provided by connections that are brokered through the shard map manager in order to avoid corruption or wrong query results.</span></span> <span data-ttu-id="bc6f6-143">這可確保如果 (例如) Shardlet 目前已使用分割/合併 API 移至不同的分區，則會拒絕或停止對特定 Shardlet 的連線。</span><span class="sxs-lookup"><span data-stu-id="bc6f6-143">This ensures that connections to a given shardlet are rejected or stopped if (for instance) the shardlet is currently moved to a different shard using Split/Merge APIs.</span></span>
* <span data-ttu-id="bc6f6-144">**物件對應**：我們想要保留 Dapper 所提供的對應便利性，以轉換應用程式和基礎資料庫結構中的類別。</span><span class="sxs-lookup"><span data-stu-id="bc6f6-144">**Object Mapping**: We want to retain the convenience of the mappings provided by Dapper to translate between classes in the application and the underlying database structures.</span></span> 

<span data-ttu-id="bc6f6-145">下一節針對以 **Dapper** 和 **DapperExtensions** 為基礎的應用程式，提供這些需求的指導。</span><span class="sxs-lookup"><span data-stu-id="bc6f6-145">The following section provides guidance for these requirements for applications based on **Dapper** and **DapperExtensions**.</span></span>

## <a name="technical-guidance"></a><span data-ttu-id="bc6f6-146">技術指導</span><span class="sxs-lookup"><span data-stu-id="bc6f6-146">Technical Guidance</span></span>
### <a name="data-dependent-routing-with-dapper"></a><span data-ttu-id="bc6f6-147">Dapper 的資料相依路由</span><span class="sxs-lookup"><span data-stu-id="bc6f6-147">Data dependent routing with Dapper</span></span>
<span data-ttu-id="bc6f6-148">有了 Dapper，應用程式通常負責建立和開啟對基礎資料庫的連線。</span><span class="sxs-lookup"><span data-stu-id="bc6f6-148">With Dapper, the application is typically responsible for creating and opening the connections to the underlying database.</span></span> <span data-ttu-id="bc6f6-149">如果應用程式指定型別 T，Dapper 會將查詢結果傳回為型別 T 的 .NET 集合。Dapper 會執行從 T-SQL 結果資料列到型別 T 物件的對應。同樣地，Dapper 會將 .NET 物件對應到資料操作語言 (DML) 陳述式的 SQL 值或參數。</span><span class="sxs-lookup"><span data-stu-id="bc6f6-149">Given a type T by the application, Dapper returns query results as .NET collections of type T. Dapper performs the mapping from the T-SQL result rows to the objects of type T. Similarly, Dapper maps .NET objects into SQL values or parameters for data manipulation language (DML) statements.</span></span> <span data-ttu-id="bc6f6-150">Dapper 透過延伸方法，在 ADO.NET SQL 用戶端程式庫中的標準 [SqlConnection](http://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.aspx) 物件上提供這項功能。</span><span class="sxs-lookup"><span data-stu-id="bc6f6-150">Dapper offers this functionality via extension methods on the regular [SqlConnection](http://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.aspx) object from the ADO .NET SQL Client libraries.</span></span> <span data-ttu-id="bc6f6-151">Elastic Scale DDR API 所傳回的 SQL 連接也是標準 [SqlConnection](http://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.aspx) 物件。</span><span class="sxs-lookup"><span data-stu-id="bc6f6-151">The SQL connection returned by the Elastic Scale APIs for DDR are also regular [SqlConnection](http://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.aspx) objects.</span></span> <span data-ttu-id="bc6f6-152">如此一來，我們即可透過用戶端程式庫的 DDR API 所傳回的型別，直接使用 Dapper 延伸模組，因為這也是簡單的 SQL 用戶端連接。</span><span class="sxs-lookup"><span data-stu-id="bc6f6-152">This allows us to directly use Dapper extensions over the type returned by the client library’s DDR API, as it is also a simple SQL Client connection.</span></span>

<span data-ttu-id="bc6f6-153">經過這些觀察，請直接使用 Dapper 的彈性資料庫用戶端程式庫所代理的連接。</span><span class="sxs-lookup"><span data-stu-id="bc6f6-153">These observations make it straightforward to use connections brokered by the elastic database client library for Dapper.</span></span>

<span data-ttu-id="bc6f6-154">此程式碼範例 (來自隨附的範例) 說明如何由應用程式提供分區化索引鍵給程式庫，以代理對適當分區的連接。</span><span class="sxs-lookup"><span data-stu-id="bc6f6-154">This code example (from the accompanying sample) illustrates the approach where the sharding key is provided by the application to the library to broker the connection to the right shard.</span></span>   

    using (SqlConnection sqlconn = shardingLayer.ShardMap.OpenConnectionForKey(
                     key: tenantId1, 
                     connectionString: connStrBldr.ConnectionString, 
                     options: ConnectionOptions.Validate))
    {
        var blog = new Blog { Name = name };
        sqlconn.Execute(@"
                      INSERT INTO
                            Blog (Name)
                            VALUES (@name)", new { name = blog.Name }
                        );
    }

<span data-ttu-id="bc6f6-155">呼叫 [OpenConnectionForKey](http://msdn.microsoft.com/library/azure/dn807226.aspx) API 可取代 SQL 用戶端連接的預設建立和開啟作業。</span><span class="sxs-lookup"><span data-stu-id="bc6f6-155">The call to the [OpenConnectionForKey](http://msdn.microsoft.com/library/azure/dn807226.aspx) API replaces the default creation and opening of a SQL Client connection.</span></span> <span data-ttu-id="bc6f6-156">[OpenConnectionForKey](http://msdn.microsoft.com/library/azure/dn807226.aspx) 呼叫接受資料相依路由所需的引數：</span><span class="sxs-lookup"><span data-stu-id="bc6f6-156">The [OpenConnectionForKey](http://msdn.microsoft.com/library/azure/dn807226.aspx) call takes the arguments that are required for data dependent routing:</span></span> 

* <span data-ttu-id="bc6f6-157">用來存取資料相依路由介面的分區對應</span><span class="sxs-lookup"><span data-stu-id="bc6f6-157">The shard map to access the data dependent routing interfaces</span></span>
* <span data-ttu-id="bc6f6-158">用來識別 Shardlet 的分區化索引鍵</span><span class="sxs-lookup"><span data-stu-id="bc6f6-158">The sharding key to identify the shardlet</span></span>
* <span data-ttu-id="bc6f6-159">用來連接到分區的認證 (使用者名稱和密碼)</span><span class="sxs-lookup"><span data-stu-id="bc6f6-159">The credentials (user name and password) to connect to the shard</span></span>

<span data-ttu-id="bc6f6-160">分區對應物件會建立分區的連線，而此分區保留給定分區化索引鍵的 Shardlet。</span><span class="sxs-lookup"><span data-stu-id="bc6f6-160">The shard map object creates a connection to the shard that holds the shardlet for the given sharding key.</span></span> <span data-ttu-id="bc6f6-161">彈性資料庫用戶端 API 也會標記此連接以履行其一致性保證。</span><span class="sxs-lookup"><span data-stu-id="bc6f6-161">The elastic database client APIs also tag the connection to implement its consistency guarantees.</span></span> <span data-ttu-id="bc6f6-162">由於呼叫 [OpenConnectionForKey](http://msdn.microsoft.com/library/azure/dn807226.aspx) 會傳回標準 SQL 用戶端連接物件，所以後續從 Dapper 呼叫 **Execute** 延伸方法時會遵循標準 Dapper 作法。</span><span class="sxs-lookup"><span data-stu-id="bc6f6-162">Since the call to [OpenConnectionForKey](http://msdn.microsoft.com/library/azure/dn807226.aspx) returns a regular SQL Client connection object, the subsequent call to the **Execute** extension method from Dapper follows the standard Dapper practice.</span></span>

<span data-ttu-id="bc6f6-163">查詢的運作方式幾乎完全相同 - 首先使用 [OpenConnectionForKey](http://msdn.microsoft.com/library/azure/dn807226.aspx) 從用戶端 API 開啟連線。</span><span class="sxs-lookup"><span data-stu-id="bc6f6-163">Queries work very much the same way - you first open the connection using [OpenConnectionForKey](http://msdn.microsoft.com/library/azure/dn807226.aspx) from the client API.</span></span> <span data-ttu-id="bc6f6-164">然後使用標準 Dapper 延伸方法，將 SQL 查詢的結果對應至 .NET 物件：</span><span class="sxs-lookup"><span data-stu-id="bc6f6-164">Then you use the regular Dapper extension methods to map the results of your SQL query into .NET objects:</span></span>

    using (SqlConnection sqlconn = shardingLayer.ShardMap.OpenConnectionForKey(
                    key: tenantId1, 
                    connectionString: connStrBldr.ConnectionString, 
                    options: ConnectionOptions.Validate ))
    {    
           // Display all Blogs for tenant 1
           IEnumerable<Blog> result = sqlconn.Query<Blog>(@"
                                SELECT * 
                                FROM Blog
                                ORDER BY Name");

           Console.WriteLine("All blogs for tenant id {0}:", tenantId1);
           foreach (var item in result)
           {
                Console.WriteLine(item.Name);
            }
    }

<span data-ttu-id="bc6f6-165">請注意，包含 DDR 連接的 **using** 區段，將區塊內的所有資料庫作業都放在保有 tenantId1 的一個分區中。</span><span class="sxs-lookup"><span data-stu-id="bc6f6-165">Note that the **using** block with the DDR connection scopes all database operations within the block to the one shard where tenantId1 is kept.</span></span> <span data-ttu-id="bc6f6-166">查詢只會傳回目前分區上儲存的部落格，但不會傳回任何其他分區上儲存的部落格。</span><span class="sxs-lookup"><span data-stu-id="bc6f6-166">The query only returns blogs stored on the current shard, but not the ones stored on any other shards.</span></span> 

## <a name="data-dependent-routing-with-dapper-and-dapperextensions"></a><span data-ttu-id="bc6f6-167">Dapper 和 DapperExtensions 的資料相依路由</span><span class="sxs-lookup"><span data-stu-id="bc6f6-167">Data dependent routing with Dapper and DapperExtensions</span></span>
<span data-ttu-id="bc6f6-168">Dapper 隨附其他延伸模組的生態系統，可在開發資料庫應用程式時從資料庫提供進一步的便利性和抽象概念。</span><span class="sxs-lookup"><span data-stu-id="bc6f6-168">Dapper comes with an ecosystem of additional extensions that can provide further convenience and abstraction from the database when developing database applications.</span></span> <span data-ttu-id="bc6f6-169">DapperExtensions 就是一個範例。</span><span class="sxs-lookup"><span data-stu-id="bc6f6-169">DapperExtensions is an example.</span></span> 

<span data-ttu-id="bc6f6-170">在您的應用程式中使用 DapperExtensions，不會改變建立和管理資料庫連線的方式。</span><span class="sxs-lookup"><span data-stu-id="bc6f6-170">Using DapperExtensions in your application does not change how database connections are created and managed.</span></span> <span data-ttu-id="bc6f6-171">仍然由應用程式負責開啟連線，而延伸方法預期會有標準 SQL 用戶端連線物件。</span><span class="sxs-lookup"><span data-stu-id="bc6f6-171">It is still the application’s responsibility to open connections, and regular SQL Client connection objects are expected by the extension methods.</span></span> <span data-ttu-id="bc6f6-172">我們可以如上所述依賴 [OpenConnectionForKey](http://msdn.microsoft.com/library/azure/dn807226.aspx) 。</span><span class="sxs-lookup"><span data-stu-id="bc6f6-172">We can rely on the [OpenConnectionForKey](http://msdn.microsoft.com/library/azure/dn807226.aspx) as outlined above.</span></span> <span data-ttu-id="bc6f6-173">如下列程式碼範例所示，唯一的改變就是我們不再需要撰寫 T-SQL 陳述式：</span><span class="sxs-lookup"><span data-stu-id="bc6f6-173">As the following code samples show, the only change is that we do no longer have to write the T-SQL statements:</span></span>

    using (SqlConnection sqlconn = shardingLayer.ShardMap.OpenConnectionForKey(
                    key: tenantId2, 
                    connectionString: connStrBldr.ConnectionString, 
                    options: ConnectionOptions.Validate))
    {
           var blog = new Blog { Name = name2 };
           sqlconn.Insert(blog);
    }

<span data-ttu-id="bc6f6-174">以下是查詢的程式碼範例：</span><span class="sxs-lookup"><span data-stu-id="bc6f6-174">And here is the code sample for the query:</span></span> 

    using (SqlConnection sqlconn = shardingLayer.ShardMap.OpenConnectionForKey(
                    key: tenantId2, 
                    connectionString: connStrBldr.ConnectionString, 
                    options: ConnectionOptions.Validate))
    {
           // Display all Blogs for tenant 2
           IEnumerable<Blog> result = sqlconn.GetList<Blog>();
           Console.WriteLine("All blogs for tenant id {0}:", tenantId2);
           foreach (var item in result)
           {
               Console.WriteLine(item.Name);
           }
    }

### <a name="handling-transient-faults"></a><span data-ttu-id="bc6f6-175">處理暫時性錯誤</span><span class="sxs-lookup"><span data-stu-id="bc6f6-175">Handling transient faults</span></span>
<span data-ttu-id="bc6f6-176">Microsoft 模式和作法小組已發佈[暫時性錯誤處理應用程式區塊](http://msdn.microsoft.com/library/hh680934.aspx)，以協助應用程式開發人員緩和在雲端執行時所遇到的常見暫時性錯誤狀況。</span><span class="sxs-lookup"><span data-stu-id="bc6f6-176">The Microsoft Patterns & Practices team published the [Transient Fault Handling Application Block](http://msdn.microsoft.com/library/hh680934.aspx) to help application developers mitigate common transient fault conditions encountered when running in the cloud.</span></span> <span data-ttu-id="bc6f6-177">如需詳細資訊，請參閱 [堅持，是所有成功的秘方：使用暫時性錯誤處理應用程式區塊](http://msdn.microsoft.com/library/dn440719.aspx)。</span><span class="sxs-lookup"><span data-stu-id="bc6f6-177">For more information, see [Perseverance, Secret of All Triumphs: Using the Transient Fault Handling Application Block](http://msdn.microsoft.com/library/dn440719.aspx).</span></span>

<span data-ttu-id="bc6f6-178">此程式碼範例依賴暫時性錯誤程式庫來防止暫時性錯誤。</span><span class="sxs-lookup"><span data-stu-id="bc6f6-178">The code sample relies on the transient fault library to protect against transient faults.</span></span> 

    SqlDatabaseUtils.SqlRetryPolicy.ExecuteAction(() =>
    {
       using (SqlConnection sqlconn = 
          shardingLayer.ShardMap.OpenConnectionForKey(tenantId2, connStrBldr.ConnectionString, ConnectionOptions.Validate))
          {
              var blog = new Blog { Name = name2 };
              sqlconn.Insert(blog);
          }
    });

<span data-ttu-id="bc6f6-179">上述程式碼中的 **SqlDatabaseUtils.SqlRetryPolicy** 定義為 **SqlDatabaseTransientErrorDetectionStrategy**，並指定重試計數 10，重試之間等待時間為 5 秒。</span><span class="sxs-lookup"><span data-stu-id="bc6f6-179">**SqlDatabaseUtils.SqlRetryPolicy** in the code above is defined as a **SqlDatabaseTransientErrorDetectionStrategy** with a retry count of 10, and 5 seconds wait time between retries.</span></span> <span data-ttu-id="bc6f6-180">如果您正在使用交易，請確定您的重試範圍會回到暫時性錯誤情況下的交易開頭。</span><span class="sxs-lookup"><span data-stu-id="bc6f6-180">If you are using transactions, make sure that your retry scope goes back to the beginning of the transaction in the case of a transient fault.</span></span>

## <a name="limitations"></a><span data-ttu-id="bc6f6-181">限制</span><span class="sxs-lookup"><span data-stu-id="bc6f6-181">Limitations</span></span>
<span data-ttu-id="bc6f6-182">這份文件中所述的方法有幾個限制：</span><span class="sxs-lookup"><span data-stu-id="bc6f6-182">The approaches outlined in this document entail a couple of limitations:</span></span>

* <span data-ttu-id="bc6f6-183">這份文件的範例程式碼不示範如何管理跨分區的結構描述。</span><span class="sxs-lookup"><span data-stu-id="bc6f6-183">The sample code for this document does not demonstrate how to manage schema across shards.</span></span>
* <span data-ttu-id="bc6f6-184">提出要求時，我們假定所有資料庫處理都包含在要求所提供的分區化索引鍵所識別的單一分區內。</span><span class="sxs-lookup"><span data-stu-id="bc6f6-184">Given a request, we assume that all its database processing is contained within a single shard as identified by the sharding key provided by the request.</span></span> <span data-ttu-id="bc6f6-185">不過，這項假設並未永遠維持，例如，不可能使用分區化索引鍵時。</span><span class="sxs-lookup"><span data-stu-id="bc6f6-185">However, this assumption does not always hold, for example, when it is not possible to make a sharding key available.</span></span> <span data-ttu-id="bc6f6-186">為了解決這個問題，彈性資料庫用戶端程式庫中提供 [MultiShardQuery 類別](http://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.query.multishardexception.aspx)。</span><span class="sxs-lookup"><span data-stu-id="bc6f6-186">To address this, the elastic database client library includes the [MultiShardQuery class](http://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.query.multishardexception.aspx).</span></span> <span data-ttu-id="bc6f6-187">此類別可實作透過數個分區查詢的連線抽象概念。</span><span class="sxs-lookup"><span data-stu-id="bc6f6-187">The class implements a connection abstraction for querying over several shards.</span></span> <span data-ttu-id="bc6f6-188">使用 MultiShardQuery 搭配 Dapper 已超出本文的範圍</span><span class="sxs-lookup"><span data-stu-id="bc6f6-188">Using MultiShardQuery in combination with Dapper is beyond the scope of this document.</span></span>

## <a name="conclusion"></a><span data-ttu-id="bc6f6-189">結論</span><span class="sxs-lookup"><span data-stu-id="bc6f6-189">Conclusion</span></span>
<span data-ttu-id="bc6f6-190">使用 Dapper 與 DapperExtensions 的應用程式可以輕易地受益於 Azure SQL Database 的彈性資料庫工具。</span><span class="sxs-lookup"><span data-stu-id="bc6f6-190">Applications using Dapper and DapperExtensions can easily benefit from elastic database tools for Azure SQL Database.</span></span> <span data-ttu-id="bc6f6-191">透過這份文件中所述的步驟，將新的 [SqlConnection](http://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.aspx) 物件的建立和開啟作業變更為使用彈性資料庫用戶端程式庫的 [OpenConnectionForKey](http://msdn.microsoft.com/library/azure/dn807226.aspx) 呼叫，這些應用程式即可使用工具的資料相依路由功能。</span><span class="sxs-lookup"><span data-stu-id="bc6f6-191">Through the steps outlined in this document, those applications can use the tool's capability for data dependent routing by changing the creation and opening of new [SqlConnection](http://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.aspx) objects to use the [OpenConnectionForKey](http://msdn.microsoft.com/library/azure/dn807226.aspx) call of the elastic database client library.</span></span> <span data-ttu-id="bc6f6-192">這會將所需的應用程式變更限制為建立及開啟新連線的位置。</span><span class="sxs-lookup"><span data-stu-id="bc6f6-192">This limits the application changes required to those places where new connections are created and opened.</span></span> 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-scale-working-with-dapper/dapperimage1.png
