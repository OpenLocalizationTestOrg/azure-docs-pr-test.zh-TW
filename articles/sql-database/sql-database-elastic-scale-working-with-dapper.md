---
title: "aaaUsing 彈性資料庫用戶端程式庫 Dapper |Microsoft 文件"
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
ms.openlocfilehash: c22ece2a977265e93850f0ad3f3ca48f0a8733ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="using-elastic-database-client-library-with-dapper"></a><span data-ttu-id="021cb-103">搭配使用彈性資料庫用戶端程式庫與 Dapper</span><span class="sxs-lookup"><span data-stu-id="021cb-103">Using elastic database client library with Dapper</span></span>
<span data-ttu-id="021cb-104">這份文件適用於不依賴 Dapper toobuild 應用程式，但也會想 tooembrace[彈性資料庫工具](sql-database-elastic-scale-introduction.md)toocreate 的實作分區化 tooscale 出其資料層應用程式。</span><span class="sxs-lookup"><span data-stu-id="021cb-104">This document is for developers that rely on Dapper toobuild applications, but also want tooembrace [elastic database tooling](sql-database-elastic-scale-introduction.md) toocreate applications that implement sharding tooscale-out their data tier.</span></span>  <span data-ttu-id="021cb-105">本文件說明的彈性資料庫工具的必要 toointegrate Dapper 架構應用程式中的 hello 變更。</span><span class="sxs-lookup"><span data-stu-id="021cb-105">This document illustrates hello changes in Dapper-based applications that are necessary toointegrate with elastic database tools.</span></span> <span data-ttu-id="021cb-106">我們將焦點在編寫 hello 彈性資料庫分區管理和資料依存路由與 Dapper。</span><span class="sxs-lookup"><span data-stu-id="021cb-106">Our focus is on composing hello elastic database shard management and data dependent routing with Dapper.</span></span> 

<span data-ttu-id="021cb-107">**範例程式碼**： [Azure SQL Database - Dapper 整合的彈性資料庫工具](https://code.msdn.microsoft.com/Elastic-Scale-with-Azure-e19fc77f)。</span><span class="sxs-lookup"><span data-stu-id="021cb-107">**Sample Code**: [Elastic database tools for Azure SQL Database - Dapper integration](https://code.msdn.microsoft.com/Elastic-Scale-with-Azure-e19fc77f).</span></span>

<span data-ttu-id="021cb-108">整合**Dapper**和**DapperExtensions** hello 與 Azure SQL Database 的彈性資料庫用戶端程式庫很容易。</span><span class="sxs-lookup"><span data-stu-id="021cb-108">Integrating **Dapper** and **DapperExtensions** with hello elastic database client library for Azure SQL Database is easy.</span></span> <span data-ttu-id="021cb-109">您的應用程式可以使用資料依存路由，方法是變更 hello 建立和開啟新[SqlConnection](http://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.aspx)物件 toouse hello [OpenConnectionForKey](http://msdn.microsoft.com/library/azure/dn807226.aspx) hello 從呼叫[用戶端程式庫](http://msdn.microsoft.com/library/azure/dn765902.aspx)。</span><span class="sxs-lookup"><span data-stu-id="021cb-109">Your applications can use data dependent routing by changing hello creation and opening of new [SqlConnection](http://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.aspx) objects toouse hello [OpenConnectionForKey](http://msdn.microsoft.com/library/azure/dn807226.aspx) call from hello [client library](http://msdn.microsoft.com/library/azure/dn765902.aspx).</span></span> <span data-ttu-id="021cb-110">這會限制您的應用程式 tooonly 其中建立並開啟新的連接中的變更。</span><span class="sxs-lookup"><span data-stu-id="021cb-110">This limits changes in your application tooonly where new connections are created and opened.</span></span> 

## <a name="dapper-overview"></a><span data-ttu-id="021cb-111">Dapper 概觀</span><span class="sxs-lookup"><span data-stu-id="021cb-111">Dapper overview</span></span>
<span data-ttu-id="021cb-112">**Dapper** 是物件關聯式對應程式。</span><span class="sxs-lookup"><span data-stu-id="021cb-112">**Dapper** is an object-relational mapper.</span></span> <span data-ttu-id="021cb-113">它對應來自您應用程式 tooa 關聯式資料庫 （反之亦然） 的.NET 物件。</span><span class="sxs-lookup"><span data-stu-id="021cb-113">It maps .NET objects from your application tooa relational database (and vice versa).</span></span> <span data-ttu-id="021cb-114">hello 的 hello 範例程式碼的第一個部分說明您可以將 hello 彈性資料庫用戶端程式庫整合與 Dapper 為基礎的應用程式的方式。</span><span class="sxs-lookup"><span data-stu-id="021cb-114">hello first part of hello sample code illustrates how you can integrate hello elastic database client library with Dapper-based applications.</span></span> <span data-ttu-id="021cb-115">hello 的 hello 範例程式碼的第二個部分將說明如何使用 Dapper 和 DapperExtensions 時 toointegrate。</span><span class="sxs-lookup"><span data-stu-id="021cb-115">hello second part of hello sample code illustrates how toointegrate when using both Dapper and DapperExtensions.</span></span>  

<span data-ttu-id="021cb-116">Dapper hello 對應工具功能會提供擴充方法，簡化執行或查詢 hello 資料庫正在提交 T-SQL 陳述式的資料庫連線。</span><span class="sxs-lookup"><span data-stu-id="021cb-116">hello mapper functionality in Dapper provides extension methods on database connections that simplify submitting T-SQL statements for execution or querying hello database.</span></span> <span data-ttu-id="021cb-117">比方說，Dapper 可讓您的.NET 物件與 hello 參數的 SQL 陳述式之間的簡單 toomap **Execute**呼叫或 tooconsume hello 您的 SQL 查詢結果為.NET 物件使用**查詢**Dapper 的呼叫。</span><span class="sxs-lookup"><span data-stu-id="021cb-117">For instance, Dapper makes it easy toomap between your .NET objects and hello parameters of SQL statements for **Execute** calls, or tooconsume hello results of your SQL queries into .NET objects using **Query** calls from Dapper.</span></span> 

<span data-ttu-id="021cb-118">使用 DapperExtensions，當您不再需要 tooprovide hello SQL 陳述式。</span><span class="sxs-lookup"><span data-stu-id="021cb-118">When using DapperExtensions, you no longer need tooprovide hello SQL statements.</span></span> <span data-ttu-id="021cb-119">擴充方法，例如**GetList**或**插入**hello 資料庫連線建立 hello hello 幕後的 SQL 陳述式。</span><span class="sxs-lookup"><span data-stu-id="021cb-119">Extensions methods such as **GetList** or **Insert** over hello database connection create hello SQL statements behind hello scenes.</span></span>

<span data-ttu-id="021cb-120">Dapper 以及 DapperExtensions 的另一個優點是 hello 應用程式控制項 hello 建立 hello 資料庫連接。</span><span class="sxs-lookup"><span data-stu-id="021cb-120">Another benefit of Dapper and also DapperExtensions is that hello application controls hello creation of hello database connection.</span></span> <span data-ttu-id="021cb-121">這有助於互動 hello 彈性資料庫用戶端程式庫的 broker 資料庫為基礎的 shardlet toodatabases hello 對應的連接。</span><span class="sxs-lookup"><span data-stu-id="021cb-121">This helps interact with hello elastic database client library which brokers database connections based on hello mapping of shardlets toodatabases.</span></span>

<span data-ttu-id="021cb-122">tooget hello Dapper 組件，請參閱[Dapper 點 net](http://www.nuget.org/packages/Dapper/)。</span><span class="sxs-lookup"><span data-stu-id="021cb-122">tooget hello Dapper assemblies, see [Dapper dot net](http://www.nuget.org/packages/Dapper/).</span></span> <span data-ttu-id="021cb-123">針對 hello Dapper 擴充功能，請參閱[DapperExtensions](http://www.nuget.org/packages/DapperExtensions)。</span><span class="sxs-lookup"><span data-stu-id="021cb-123">For hello Dapper extensions, see [DapperExtensions](http://www.nuget.org/packages/DapperExtensions).</span></span>

## <a name="a-quick-look-at-hello-elastic-database-client-library"></a><span data-ttu-id="021cb-124">快速查看 hello 彈性資料庫用戶端程式庫</span><span class="sxs-lookup"><span data-stu-id="021cb-124">A quick Look at hello elastic database client library</span></span>
<span data-ttu-id="021cb-125">與 hello 彈性資料庫用戶端程式庫，您會定義呼叫的應用程式資料的資料分割*shardlet* 、 將它們對應 toodatabases，和它們所識別*分區化索引鍵*。</span><span class="sxs-lookup"><span data-stu-id="021cb-125">With hello elastic database client library, you define partitions of your application data called *shardlets* , map them toodatabases, and identify them by *sharding keys*.</span></span> <span data-ttu-id="021cb-126">您可以擁有所需數量的資料庫，並將 Shardlet 分散於這些資料庫。</span><span class="sxs-lookup"><span data-stu-id="021cb-126">You can have as many databases as you need and distribute your shardlets across these databases.</span></span> <span data-ttu-id="021cb-127">hello 對應的分區化索引鍵值 toohello 資料庫儲存 hello 程式庫的應用程式開發介面所提供的分區對應。</span><span class="sxs-lookup"><span data-stu-id="021cb-127">hello mapping of sharding key values toohello databases is stored by a shard map provided by hello library’s APIs.</span></span> <span data-ttu-id="021cb-128">這項功能稱為 **分區對應管理**。</span><span class="sxs-lookup"><span data-stu-id="021cb-128">This capability is called **shard map management**.</span></span> <span data-ttu-id="021cb-129">hello 分區對應也可做為 hello broker 的要求進行分區化索引鍵的資料庫連線。</span><span class="sxs-lookup"><span data-stu-id="021cb-129">hello shard map also serves as hello broker of database connections for requests that carry a sharding key.</span></span> <span data-ttu-id="021cb-130">這項功能會參考的 tooas**資料依存路由**。</span><span class="sxs-lookup"><span data-stu-id="021cb-130">This capability is referred tooas **data dependent routing**.</span></span>

![分區對應和資料相依路由][1]

<span data-ttu-id="021cb-132">hello 分區對應管理員防止不一致的檢視為 shardlet 資料 hello 資料庫上發生並行的 shardlet 管理作業時可能發生的使用者。</span><span class="sxs-lookup"><span data-stu-id="021cb-132">hello shard map manager protects users from inconsistent views into shardlet data that can occur when concurrent shardlet management operations are happening on hello databases.</span></span> <span data-ttu-id="021cb-133">toodo，hello 分區對應 broker hello 資料庫連接，以便與 hello 程式庫所建置的應用程式。</span><span class="sxs-lookup"><span data-stu-id="021cb-133">toodo so, hello shard maps broker hello database connections for an application built with hello library.</span></span> <span data-ttu-id="021cb-134">當分區管理作業可能會影響 hello shardlet 時，這樣 hello 分區對應功能 tooautomatically 終止資料庫連接。</span><span class="sxs-lookup"><span data-stu-id="021cb-134">When shard management operations could impact hello shardlet, this allows hello shard map functionality tooautomatically kill a database connection.</span></span> 

<span data-ttu-id="021cb-135">而不是使用 Dapper hello 傳統方式 toocreate 連接，我們需要 toouse hello [OpenConnectionForKey 方法](http://msdn.microsoft.com/library/azure/dn824099.aspx)。</span><span class="sxs-lookup"><span data-stu-id="021cb-135">Instead of using hello traditional way toocreate connections for Dapper, we need toouse hello [OpenConnectionForKey method](http://msdn.microsoft.com/library/azure/dn824099.aspx).</span></span> <span data-ttu-id="021cb-136">這樣可以確保所有 hello 驗證都進行連接都管理正確分區之間的任何資料移動時。</span><span class="sxs-lookup"><span data-stu-id="021cb-136">This ensures that all hello validation takes place and connections are managed properly when any data moves between shards.</span></span>

### <a name="requirements-for-dapper-integration"></a><span data-ttu-id="021cb-137">Dapper 整合需求</span><span class="sxs-lookup"><span data-stu-id="021cb-137">Requirements for Dapper integration</span></span>
<span data-ttu-id="021cb-138">當使用 hello 彈性資料庫用戶端程式庫和 hello Dapper 應用程式開發介面，我們想要 tooretain hello 下列屬性：</span><span class="sxs-lookup"><span data-stu-id="021cb-138">When working with both hello elastic database client library and hello Dapper APIs, we want tooretain hello following properties:</span></span>

* <span data-ttu-id="021cb-139">**向外延展**： 我們想 tooadd 或 hello 資料 hello 分區化應用程式層的視 hello 容量需求的 hello 應用程式中移除資料庫。</span><span class="sxs-lookup"><span data-stu-id="021cb-139">**Scaleout**: We want tooadd or remove databases from hello data tier of hello sharded application as necessary for hello capacity demands of hello application.</span></span> 
* <span data-ttu-id="021cb-140">**一致性**： 由於我們的應用程式會向外延展使用分區化中，我們需要 tooperform 資料依存路由。</span><span class="sxs-lookup"><span data-stu-id="021cb-140">**Consistency**: Since our application is scaled out using sharding, we need tooperform data dependent routing.</span></span> <span data-ttu-id="021cb-141">因此，我們想 toouse hello 資料依存路由功能 hello 文件庫 toodo。</span><span class="sxs-lookup"><span data-stu-id="021cb-141">We want toouse hello Data dependent routing capabilities of hello library toodo so.</span></span> <span data-ttu-id="021cb-142">特別是，我們想 tooretain hello 驗證，而且透過順序 tooavoid 損毀或不正確的查詢結果中的 hello 分區對應管理員代理的連接所提供的一致性保證。</span><span class="sxs-lookup"><span data-stu-id="021cb-142">In particular, we want tooretain hello validation and consistency guarantees provided by connections that are brokered through hello shard map manager in order tooavoid corruption or wrong query results.</span></span> <span data-ttu-id="021cb-143">這可確保該給定 shardlet 的連線 tooa 拒絕或停止時 （例如） hello shardlet 目前移動的 tooa 不同分區使用分割/合併 Api。</span><span class="sxs-lookup"><span data-stu-id="021cb-143">This ensures that connections tooa given shardlet are rejected or stopped if (for instance) hello shardlet is currently moved tooa different shard using Split/Merge APIs.</span></span>
* <span data-ttu-id="021cb-144">**物件對應**： 我們想要 tooretain hello 的方便性，不論 hello Dapper tootranslate hello 應用程式中的類別和基礎資料庫結構的 hello 之間所提供的對應。</span><span class="sxs-lookup"><span data-stu-id="021cb-144">**Object Mapping**: We want tooretain hello convenience of hello mappings provided by Dapper tootranslate between classes in hello application and hello underlying database structures.</span></span> 

<span data-ttu-id="021cb-145">hello 下節提供這些需求為基礎的應用程式的指引**Dapper**和**DapperExtensions**。</span><span class="sxs-lookup"><span data-stu-id="021cb-145">hello following section provides guidance for these requirements for applications based on **Dapper** and **DapperExtensions**.</span></span>

## <a name="technical-guidance"></a><span data-ttu-id="021cb-146">技術指導</span><span class="sxs-lookup"><span data-stu-id="021cb-146">Technical Guidance</span></span>
### <a name="data-dependent-routing-with-dapper"></a><span data-ttu-id="021cb-147">Dapper 的資料相依路由</span><span class="sxs-lookup"><span data-stu-id="021cb-147">Data dependent routing with Dapper</span></span>
<span data-ttu-id="021cb-148">Dapper，與 hello 應用程式是通常負責建立及開啟 hello 連線 toohello 基礎資料庫。</span><span class="sxs-lookup"><span data-stu-id="021cb-148">With Dapper, hello application is typically responsible for creating and opening hello connections toohello underlying database.</span></span> <span data-ttu-id="021cb-149">Hello 應用程式所指定型別 T，Dapper 傳回查詢結果的型別 T Dapper.NET 集合執行 hello 對應從 hello T-SQL 結果資料列 toohello 物件為類型 t。同樣地，Dapper 將.NET 物件對應至 SQL 值或資料操作語言 (DML) 陳述式的參數。</span><span class="sxs-lookup"><span data-stu-id="021cb-149">Given a type T by hello application, Dapper returns query results as .NET collections of type T. Dapper performs hello mapping from hello T-SQL result rows toohello objects of type T. Similarly, Dapper maps .NET objects into SQL values or parameters for data manipulation language (DML) statements.</span></span> <span data-ttu-id="021cb-150">Dapper 提供這項功能透過 hello 規則的擴充方法[SqlConnection](http://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.aspx) hello ADO.NET SQL 用戶端程式庫中的物件。</span><span class="sxs-lookup"><span data-stu-id="021cb-150">Dapper offers this functionality via extension methods on hello regular [SqlConnection](http://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.aspx) object from hello ADO .NET SQL Client libraries.</span></span> <span data-ttu-id="021cb-151">hello hello Elastic Scale Api 所傳回的 DDR 的 SQL 連接也會定期[SqlConnection](http://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.aspx)物件。</span><span class="sxs-lookup"><span data-stu-id="021cb-151">hello SQL connection returned by hello Elastic Scale APIs for DDR are also regular [SqlConnection](http://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.aspx) objects.</span></span> <span data-ttu-id="021cb-152">這可讓我們 toodirectly 使用 Dapper 延伸 hello hello 用戶端程式庫的 DDR API，所傳回的類型，所以也是簡單的 SQL 用戶端連接。</span><span class="sxs-lookup"><span data-stu-id="021cb-152">This allows us toodirectly use Dapper extensions over hello type returned by hello client library’s DDR API, as it is also a simple SQL Client connection.</span></span>

<span data-ttu-id="021cb-153">這些觀察後讓直接 toouse 連線的 Dapper 代理 hello 彈性資料庫用戶端程式庫。</span><span class="sxs-lookup"><span data-stu-id="021cb-153">These observations make it straightforward toouse connections brokered by hello elastic database client library for Dapper.</span></span>

<span data-ttu-id="021cb-154">（從 hello 隨附的範例) 這個程式碼範例將示範 hello 方法其中 hello 分區化索引鍵由 hello 應用程式 toohello 文件庫 toobroker hello 連接 toohello 正確分區。</span><span class="sxs-lookup"><span data-stu-id="021cb-154">This code example (from hello accompanying sample) illustrates hello approach where hello sharding key is provided by hello application toohello library toobroker hello connection toohello right shard.</span></span>   

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

<span data-ttu-id="021cb-155">hello 呼叫 toohello [OpenConnectionForKey](http://msdn.microsoft.com/library/azure/dn807226.aspx) API 取代 hello 預設建立及開啟 SQL 用戶端連接。</span><span class="sxs-lookup"><span data-stu-id="021cb-155">hello call toohello [OpenConnectionForKey](http://msdn.microsoft.com/library/azure/dn807226.aspx) API replaces hello default creation and opening of a SQL Client connection.</span></span> <span data-ttu-id="021cb-156">hello [OpenConnectionForKey](http://msdn.microsoft.com/library/azure/dn807226.aspx)呼叫採用所需的資料依存路由 hello 引數：</span><span class="sxs-lookup"><span data-stu-id="021cb-156">hello [OpenConnectionForKey](http://msdn.microsoft.com/library/azure/dn807226.aspx) call takes hello arguments that are required for data dependent routing:</span></span> 

* <span data-ttu-id="021cb-157">hello 分區對應 tooaccess hello 資料依存路由介面</span><span class="sxs-lookup"><span data-stu-id="021cb-157">hello shard map tooaccess hello data dependent routing interfaces</span></span>
* <span data-ttu-id="021cb-158">hello 分區化索引鍵 tooidentify hello shardlet</span><span class="sxs-lookup"><span data-stu-id="021cb-158">hello sharding key tooidentify hello shardlet</span></span>
* <span data-ttu-id="021cb-159">hello 認證 （使用者名稱和密碼） tooconnect toohello 分區</span><span class="sxs-lookup"><span data-stu-id="021cb-159">hello credentials (user name and password) tooconnect toohello shard</span></span>

<span data-ttu-id="021cb-160">hello 分區對應物件會建立保留 hello 指定分區化索引鍵的 hello shardlet 連線 toohello 分區。</span><span class="sxs-lookup"><span data-stu-id="021cb-160">hello shard map object creates a connection toohello shard that holds hello shardlet for hello given sharding key.</span></span> <span data-ttu-id="021cb-161">hello 彈性資料庫用戶端應用程式開發介面也標記 hello 連接 tooimplement 其一致性保證。</span><span class="sxs-lookup"><span data-stu-id="021cb-161">hello elastic database client APIs also tag hello connection tooimplement its consistency guarantees.</span></span> <span data-ttu-id="021cb-162">因為 hello 呼叫太[OpenConnectionForKey](http://msdn.microsoft.com/library/azure/dn807226.aspx)傳回規則的 SQL 用戶端連線物件、 hello 後續呼叫 toohello **Execute**從 Dapper 如下所示的擴充方法 hello 標準 Dapper練習。</span><span class="sxs-lookup"><span data-stu-id="021cb-162">Since hello call too[OpenConnectionForKey](http://msdn.microsoft.com/library/azure/dn807226.aspx) returns a regular SQL Client connection object, hello subsequent call toohello **Execute** extension method from Dapper follows hello standard Dapper practice.</span></span>

<span data-ttu-id="021cb-163">查詢工作非常 hello 相同方式-您第一次開啟 hello 連線使用[OpenConnectionForKey](http://msdn.microsoft.com/library/azure/dn807226.aspx)從 hello 用戶端應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="021cb-163">Queries work very much hello same way - you first open hello connection using [OpenConnectionForKey](http://msdn.microsoft.com/library/azure/dn807226.aspx) from hello client API.</span></span> <span data-ttu-id="021cb-164">然後您可以使用 hello 一般 Dapper 擴充功能方法 toomap hello SQL 查詢結果為.NET 物件：</span><span class="sxs-lookup"><span data-stu-id="021cb-164">Then you use hello regular Dapper extension methods toomap hello results of your SQL query into .NET objects:</span></span>

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

<span data-ttu-id="021cb-165">請注意該 hello**使用**與 hello DDR 連接範圍會封鎖 hello 區塊 toohello 一個分區處於 tenantId1 內的所有資料庫作業。</span><span class="sxs-lookup"><span data-stu-id="021cb-165">Note that hello **using** block with hello DDR connection scopes all database operations within hello block toohello one shard where tenantId1 is kept.</span></span> <span data-ttu-id="021cb-166">hello 查詢只會傳回儲存在 hello 目前分區，但是 hello 儲存在任何其他分區上的項目上的部落格。</span><span class="sxs-lookup"><span data-stu-id="021cb-166">hello query only returns blogs stored on hello current shard, but not hello ones stored on any other shards.</span></span> 

## <a name="data-dependent-routing-with-dapper-and-dapperextensions"></a><span data-ttu-id="021cb-167">Dapper 和 DapperExtensions 的資料相依路由</span><span class="sxs-lookup"><span data-stu-id="021cb-167">Data dependent routing with Dapper and DapperExtensions</span></span>
<span data-ttu-id="021cb-168">Dapper 隨附的其他擴充功能時，可以提供進一步的方便以及抽象從 hello 資料庫開發資料庫應用程式的生態系統。</span><span class="sxs-lookup"><span data-stu-id="021cb-168">Dapper comes with an ecosystem of additional extensions that can provide further convenience and abstraction from hello database when developing database applications.</span></span> <span data-ttu-id="021cb-169">DapperExtensions 就是一個範例。</span><span class="sxs-lookup"><span data-stu-id="021cb-169">DapperExtensions is an example.</span></span> 

<span data-ttu-id="021cb-170">在您的應用程式中使用 DapperExtensions，不會改變建立和管理資料庫連線的方式。</span><span class="sxs-lookup"><span data-stu-id="021cb-170">Using DapperExtensions in your application does not change how database connections are created and managed.</span></span> <span data-ttu-id="021cb-171">它仍然是 hello 應用程式的責任 tooopen 連線，以及一般的 SQL 用戶端連線物件會預期收到 hello 擴充方法。</span><span class="sxs-lookup"><span data-stu-id="021cb-171">It is still hello application’s responsibility tooopen connections, and regular SQL Client connection objects are expected by hello extension methods.</span></span> <span data-ttu-id="021cb-172">我們可以依賴 hello [OpenConnectionForKey](http://msdn.microsoft.com/library/azure/dn807226.aspx)如上面所述。</span><span class="sxs-lookup"><span data-stu-id="021cb-172">We can rely on hello [OpenConnectionForKey](http://msdn.microsoft.com/library/azure/dn807226.aspx) as outlined above.</span></span> <span data-ttu-id="021cb-173">Hello 為下列程式碼範例會顯示 hello 唯一的變更是，我們不會再有 toowrite hello T-SQL 陳述式：</span><span class="sxs-lookup"><span data-stu-id="021cb-173">As hello following code samples show, hello only change is that we do no longer have toowrite hello T-SQL statements:</span></span>

    using (SqlConnection sqlconn = shardingLayer.ShardMap.OpenConnectionForKey(
                    key: tenantId2, 
                    connectionString: connStrBldr.ConnectionString, 
                    options: ConnectionOptions.Validate))
    {
           var blog = new Blog { Name = name2 };
           sqlconn.Insert(blog);
    }

<span data-ttu-id="021cb-174">此外，這裡有 hello hello 查詢的程式碼範例：</span><span class="sxs-lookup"><span data-stu-id="021cb-174">And here is hello code sample for hello query:</span></span> 

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

### <a name="handling-transient-faults"></a><span data-ttu-id="021cb-175">處理暫時性錯誤</span><span class="sxs-lookup"><span data-stu-id="021cb-175">Handling transient faults</span></span>
<span data-ttu-id="021cb-176">hello Microsoft Patterns & Practices 團隊發行的 hello[暫時性錯誤處理應用程式區塊](http://msdn.microsoft.com/library/hh680934.aspx)toohelp 應用程式開發人員降低 hello 雲端中執行時所遇到的常見暫時性錯誤狀況。</span><span class="sxs-lookup"><span data-stu-id="021cb-176">hello Microsoft Patterns & Practices team published hello [Transient Fault Handling Application Block](http://msdn.microsoft.com/library/hh680934.aspx) toohelp application developers mitigate common transient fault conditions encountered when running in hello cloud.</span></span> <span data-ttu-id="021cb-177">如需詳細資訊，請參閱[堅持不懈、 所有勝利密碼： 使用暫時性錯誤處理應用程式區塊 hello](http://msdn.microsoft.com/library/dn440719.aspx)。</span><span class="sxs-lookup"><span data-stu-id="021cb-177">For more information, see [Perseverance, Secret of All Triumphs: Using hello Transient Fault Handling Application Block](http://msdn.microsoft.com/library/dn440719.aspx).</span></span>

<span data-ttu-id="021cb-178">hello 程式碼範例會依賴 hello 暫時性錯誤文件庫 tooprotect 針對暫時性錯誤。</span><span class="sxs-lookup"><span data-stu-id="021cb-178">hello code sample relies on hello transient fault library tooprotect against transient faults.</span></span> 

    SqlDatabaseUtils.SqlRetryPolicy.ExecuteAction(() =>
    {
       using (SqlConnection sqlconn = 
          shardingLayer.ShardMap.OpenConnectionForKey(tenantId2, connStrBldr.ConnectionString, ConnectionOptions.Validate))
          {
              var blog = new Blog { Name = name2 };
              sqlconn.Insert(blog);
          }
    });

<span data-ttu-id="021cb-179">**SqlDatabaseUtils.SqlRetryPolicy** hello 在上述程式碼會定義為**SqlDatabaseTransientErrorDetectionStrategy** 10，和 5 秒的重試計數等候重試之間的時間。</span><span class="sxs-lookup"><span data-stu-id="021cb-179">**SqlDatabaseUtils.SqlRetryPolicy** in hello code above is defined as a **SqlDatabaseTransientErrorDetectionStrategy** with a retry count of 10, and 5 seconds wait time between retries.</span></span> <span data-ttu-id="021cb-180">如果您正在使用交易，請確定您重試的範圍會回到 toohello 之暫時性錯誤的 hello 案例中的 hello 交易的開頭。</span><span class="sxs-lookup"><span data-stu-id="021cb-180">If you are using transactions, make sure that your retry scope goes back toohello beginning of hello transaction in hello case of a transient fault.</span></span>

## <a name="limitations"></a><span data-ttu-id="021cb-181">限制</span><span class="sxs-lookup"><span data-stu-id="021cb-181">Limitations</span></span>
<span data-ttu-id="021cb-182">這份文件中所述的 hello 方法需要有幾項限制：</span><span class="sxs-lookup"><span data-stu-id="021cb-182">hello approaches outlined in this document entail a couple of limitations:</span></span>

* <span data-ttu-id="021cb-183">本文件的 hello 範例程式碼不會示範如何跨分區 toomanage 結構描述。</span><span class="sxs-lookup"><span data-stu-id="021cb-183">hello sample code for this document does not demonstrate how toomanage schema across shards.</span></span>
* <span data-ttu-id="021cb-184">指定要求，我們假設其所有資料庫處理都包含在單一分區中的 hello hello 要求所提供的分區化索引鍵識別。</span><span class="sxs-lookup"><span data-stu-id="021cb-184">Given a request, we assume that all its database processing is contained within a single shard as identified by hello sharding key provided by hello request.</span></span> <span data-ttu-id="021cb-185">不過，這項假設不一定包含，比方說，不可能 toomake 分區化索引鍵可用時。</span><span class="sxs-lookup"><span data-stu-id="021cb-185">However, this assumption does not always hold, for example, when it is not possible toomake a sharding key available.</span></span> <span data-ttu-id="021cb-186">tooaddress，hello 彈性資料庫用戶端程式庫包含 hello [MultiShardQuery 類別](http://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.query.multishardexception.aspx)。</span><span class="sxs-lookup"><span data-stu-id="021cb-186">tooaddress this, hello elastic database client library includes hello [MultiShardQuery class](http://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.query.multishardexception.aspx).</span></span> <span data-ttu-id="021cb-187">hello 類別會實作抽象的查詢數個分區的連線。</span><span class="sxs-lookup"><span data-stu-id="021cb-187">hello class implements a connection abstraction for querying over several shards.</span></span> <span data-ttu-id="021cb-188">使用搭配 Dapper MultiShardQuery 已超出本文件 hello 範圍。</span><span class="sxs-lookup"><span data-stu-id="021cb-188">Using MultiShardQuery in combination with Dapper is beyond hello scope of this document.</span></span>

## <a name="conclusion"></a><span data-ttu-id="021cb-189">結論</span><span class="sxs-lookup"><span data-stu-id="021cb-189">Conclusion</span></span>
<span data-ttu-id="021cb-190">使用 Dapper 與 DapperExtensions 的應用程式可以輕易地受益於 Azure SQL Database 的彈性資料庫工具。</span><span class="sxs-lookup"><span data-stu-id="021cb-190">Applications using Dapper and DapperExtensions can easily benefit from elastic database tools for Azure SQL Database.</span></span> <span data-ttu-id="021cb-191">Hello 這份文件中所述的步驟，透過這些應用程式可用於 hello 工具的功能資料依存路由，方法是變更 hello 建立和開啟新[SqlConnection](http://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.aspx)物件 toouse hello [OpenConnectionForKey](http://msdn.microsoft.com/library/azure/dn807226.aspx) hello 彈性資料庫用戶端程式庫的呼叫。</span><span class="sxs-lookup"><span data-stu-id="021cb-191">Through hello steps outlined in this document, those applications can use hello tool's capability for data dependent routing by changing hello creation and opening of new [SqlConnection](http://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.aspx) objects toouse hello [OpenConnectionForKey](http://msdn.microsoft.com/library/azure/dn807226.aspx) call of hello elastic database client library.</span></span> <span data-ttu-id="021cb-192">這會限制 hello 應用程式的變更需要的 toothose 數位其中建立並開啟新的連接。</span><span class="sxs-lookup"><span data-stu-id="021cb-192">This limits hello application changes required toothose places where new connections are created and opened.</span></span> 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-scale-working-with-dapper/dapperimage1.png
