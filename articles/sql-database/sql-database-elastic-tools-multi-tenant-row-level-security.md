---
title: "使用彈性資料庫工具和資料列層級安全性的多租用戶應用程式"
description: "了解如何搭配資料列層級安全性使用彈性資料庫工具建置應用程式，且讓此應用程式在 Azure SQL Database 上具有可支援多租用戶分區的高度可擴充資料層。"
metakeywords: azure sql database elastic tools multi tenant row level security rls
services: sql-database
documentationcenter: 
manager: jhubbard
author: tmullaney
ms.assetid: e72d3cfe-e9be-4326-b776-9c6d96c0a18e
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/27/2016
ms.author: thmullan;torsteng
ms.openlocfilehash: 73f1210b8d1f5ceca8fac9534d498bdc23d96d48
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="multi-tenant-applications-with-elastic-database-tools-and-row-level-security"></a><span data-ttu-id="c4248-103">使用彈性資料庫工具和資料列層級安全性的多租用戶應用程式</span><span class="sxs-lookup"><span data-stu-id="c4248-103">Multi-tenant applications with elastic database tools and row-level security</span></span>
<span data-ttu-id="c4248-104">[彈性資料庫工具](sql-database-elastic-scale-get-started.md)和[資料列層級安全性 (RLS) ](https://msdn.microsoft.com/library/dn765131)提供一組強大的功能，能以具彈性且有效率的方式，透過 Azure SQL Database 調整多租用戶應用程式的資料層。</span><span class="sxs-lookup"><span data-stu-id="c4248-104">[Elastic database tools](sql-database-elastic-scale-get-started.md) and [row-level security (RLS)](https://msdn.microsoft.com/library/dn765131) offer a powerful set of capabilities for flexibly and efficiently scaling the data tier of a multi-tenant application with Azure SQL Database.</span></span> <span data-ttu-id="c4248-105">如需詳細資訊，請參閱 [多租用戶 SaaS 應用程式與 Azure SQL Database 的設計模式](sql-database-design-patterns-multi-tenancy-saas-applications.md) 。</span><span class="sxs-lookup"><span data-stu-id="c4248-105">See [Design Patterns for Multi-tenant SaaS Applications with Azure SQL Database](sql-database-design-patterns-multi-tenancy-saas-applications.md) for more information.</span></span> 

<span data-ttu-id="c4248-106">本文說明如何運用這些技術，透過 **ADO.NET SqlClient** 和/或 **Entity Framework** 建置應用程式，且讓此應用程式具有可支援多租用戶分區的高度可擴充資料層。</span><span class="sxs-lookup"><span data-stu-id="c4248-106">This article illustrates how to use these technologies together to build an application with a highly scalable data tier that supports multi-tenant shards, using **ADO.NET SqlClient** and/or **Entity Framework**.</span></span>  

* <span data-ttu-id="c4248-107"> 彈性資料庫工具可讓開發人員藉由使用 .NET 程式庫和 Azure 服務範本的一套業界標準分區化作法，向外延展應用程式的資料層。</span><span class="sxs-lookup"><span data-stu-id="c4248-107">**Elastic database tools** enables developers to scale out the data tier of an application via industry-standard sharding practices using a set of .NET libraries and Azure service templates.</span></span> <span data-ttu-id="c4248-108">使用「彈性資料庫用戶端程式庫」管理分區，有助於自動化及簡化許多通常與分區化相關的基礎結構工作。</span><span class="sxs-lookup"><span data-stu-id="c4248-108">Managing shards with using the Elastic Database Client Library helps automate and streamline many of the infrastructural tasks typically associated with sharding.</span></span> 
* <span data-ttu-id="c4248-109">**資料列層級安全性** 可讓開發人員使用安全性原則來篩選掉一些資料列 (這些資料列不屬於執行查詢的租用戶)，藉此在同一個資料庫中儲存多個租用戶的資料。</span><span class="sxs-lookup"><span data-stu-id="c4248-109">**Row-level security** enables developers to store data for multiple tenants in the same database using security policies to filter out rows that do not belong to the tenant executing a query.</span></span> <span data-ttu-id="c4248-110">在資料庫內 (而不是在應用程式內) 集中存取邏輯與 RLS，可簡化維護流程並降低發生錯誤的風險 (因為應用程式的程式碼基底會成長)。</span><span class="sxs-lookup"><span data-stu-id="c4248-110">Centralizing access logic with RLS inside the database, rather than in the application, simplifies maintenance and reduces the risk of error as an application’s codebase grows.</span></span> 

<span data-ttu-id="c4248-111">搭配使用這些功能時，由於在同一個分區資料庫中儲存多租用戶的資料可節省成本並提高效率，進而使應用程式受益。</span><span class="sxs-lookup"><span data-stu-id="c4248-111">Using these features together, an application can benefit from cost savings and efficiency gains by storing data for multiple tenants in the same shard database.</span></span> <span data-ttu-id="c4248-112">在此同時，應用程式仍會為「高階」租用戶彈性地提供隔離的單一租用戶分區，因為這些租用戶需要更嚴格的效能保證，畢竟多租用戶分區並不保證能在租用戶間平均分配資源。</span><span class="sxs-lookup"><span data-stu-id="c4248-112">At the same time, an application still has the flexibility to offer isolated, single-tenant shards for “premium” tenants who require stricter performance guarantees since multi-tenant shards do not guarantee equal resource distribution among tenants.</span></span>  

<span data-ttu-id="c4248-113">簡單地說，彈性資料庫用戶端程式庫的 [資料依存路由](sql-database-elastic-scale-data-dependent-routing.md) API 會自動將租用戶連接到正確的分區資料庫，這些資料庫含有他們的分區化索引鍵 (通常為 "TenantId")。</span><span class="sxs-lookup"><span data-stu-id="c4248-113">In short, the elastic database client library’s [data dependent routing](sql-database-elastic-scale-data-dependent-routing.md) APIs automatically connect tenants to the correct shard database containing their sharding key (generally a “TenantId”).</span></span> <span data-ttu-id="c4248-114">一旦連接之後，在資料庫內的 RLS 安全性原則可確保租用戶只能存取含有其 TenantId 的資料列。</span><span class="sxs-lookup"><span data-stu-id="c4248-114">Once connected, an RLS security policy within the database ensures that tenants can only access rows that contain their TenantId.</span></span> <span data-ttu-id="c4248-115">此原則會假設所有資料表都包含一個會指出哪些資料列屬於哪個租用戶的 TenantId 資料行。</span><span class="sxs-lookup"><span data-stu-id="c4248-115">It is assumed that all tables contain a TenantId column to indicate which rows belong to each tenant.</span></span> 

![部落格應用程式架構][1]

## <a name="download-the-sample-project"></a><span data-ttu-id="c4248-117">下載範例專案</span><span class="sxs-lookup"><span data-stu-id="c4248-117">Download the sample project</span></span>
### <a name="prerequisites"></a><span data-ttu-id="c4248-118">必要條件</span><span class="sxs-lookup"><span data-stu-id="c4248-118">Prerequisites</span></span>
* <span data-ttu-id="c4248-119">使用 Visual Studio (2012 或更新版本)</span><span class="sxs-lookup"><span data-stu-id="c4248-119">Use Visual Studio (2012 or higher)</span></span> 
* <span data-ttu-id="c4248-120">建立三個 Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="c4248-120">Create three Azure SQL Databases</span></span> 
* <span data-ttu-id="c4248-121">下載範例專案： [Azure SQL 的彈性資料庫工具：多租用戶分區](http://go.microsoft.com/?linkid=9888163)</span><span class="sxs-lookup"><span data-stu-id="c4248-121">Download sample project: [Elastic DB Tools for Azure SQL - Multi-Tenant Shards](http://go.microsoft.com/?linkid=9888163)</span></span>
  * <span data-ttu-id="c4248-122">在 **Program.cs**</span><span class="sxs-lookup"><span data-stu-id="c4248-122">Fill in the information for your databases at the beginning of **Program.cs**</span></span> 

<span data-ttu-id="c4248-123">此專案會新增對多租用戶分區資料庫的支援，藉此擴充 [Azure SQL 的彈性資料庫工具：Entity Framework 整合](sql-database-elastic-scale-use-entity-framework-applications-visual-studio.md) 中所述的項目。</span><span class="sxs-lookup"><span data-stu-id="c4248-123">This project extends the one described in [Elastic DB Tools for Azure SQL - Entity Framework Integration](sql-database-elastic-scale-use-entity-framework-applications-visual-studio.md) by adding support for multi-tenant shard databases.</span></span> <span data-ttu-id="c4248-124">如上圖所示，這麼做可以建立具有四個租用戶與兩個多租用戶分區資料庫的簡單主控台應用程式，以用於建立部落格和文章。</span><span class="sxs-lookup"><span data-stu-id="c4248-124">It builds a simple console application for creating blogs and posts, with four tenants and two multi-tenant shard databases as illustrated in the above diagram.</span></span> 

<span data-ttu-id="c4248-125">建置並執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="c4248-125">Build and run the application.</span></span> <span data-ttu-id="c4248-126">這會啟動彈性資料庫工具的分區對應管理員，並執行下列測試：</span><span class="sxs-lookup"><span data-stu-id="c4248-126">This will bootstrap the elastic database tools’ shard map manager and run the following tests:</span></span> 

1. <span data-ttu-id="c4248-127">使用 Entity Framework 和 LINQ，建立新的部落格，然後顯示每個租用戶的所有部落格</span><span class="sxs-lookup"><span data-stu-id="c4248-127">Using Entity Framework and LINQ, create a new blog and then display all blogs for each tenant</span></span>
2. <span data-ttu-id="c4248-128">使用 ADO.NET SqlClient，顯示某個租用戶的所有部落格</span><span class="sxs-lookup"><span data-stu-id="c4248-128">Using ADO.NET SqlClient, display all blogs for a tenant</span></span>
3. <span data-ttu-id="c4248-129">嘗試插入錯誤的租用戶部落格，以確認是否擲回錯誤</span><span class="sxs-lookup"><span data-stu-id="c4248-129">Try to insert a blog for the wrong tenant to verify that an error is thrown</span></span>  

<span data-ttu-id="c4248-130">請注意，因為分區資料庫中尚未啟用 RLS，所以這些測試都會顯現出一個問題：租用戶能夠查看不屬於自己的部落格，且應用程式無法阻止插入錯誤的租用戶部落格。</span><span class="sxs-lookup"><span data-stu-id="c4248-130">Notice that because RLS has not yet been enabled in the shard databases, each of these tests reveals a problem: tenants are able to see blogs that do not belong to them, and the application is not prevented from inserting a blog for the wrong tenant.</span></span> <span data-ttu-id="c4248-131">本文的其餘部分會說明，如何藉由 RLS 強制執行租用戶隔離來解決這些問題。</span><span class="sxs-lookup"><span data-stu-id="c4248-131">The remainder of this article describes how to resolve these problems by enforcing tenant isolation with RLS.</span></span> <span data-ttu-id="c4248-132">有兩個步驟：</span><span class="sxs-lookup"><span data-stu-id="c4248-132">There are two steps:</span></span> 

1. <span data-ttu-id="c4248-133">**應用程式層**：修改應用程式程式碼，以便在開啟連線之後一律設定 SESSION_CONTEXT 中目前的 TenantId。</span><span class="sxs-lookup"><span data-stu-id="c4248-133">**Application tier**: Modify the application code to always set the current TenantId in the SESSION_CONTEXT after opening a connection.</span></span> <span data-ttu-id="c4248-134">範例專案已經完成此步驟。</span><span class="sxs-lookup"><span data-stu-id="c4248-134">The sample project has already done this.</span></span> 
2. <span data-ttu-id="c4248-135">**資料層**：在每個分區資料庫中建立 RLS 安全性原則，以便根據儲存在 SESSION_CONTEXT 中的 TenantId 來篩選資料列。</span><span class="sxs-lookup"><span data-stu-id="c4248-135">**Data tier**: Create an RLS security policy in each shard database to filter rows based on the TenantId stored in SESSION_CONTEXT.</span></span> <span data-ttu-id="c4248-136">您需要對每個分區資料庫執行這個動作，否則將不會篩選多租用戶分區中的資料列。</span><span class="sxs-lookup"><span data-stu-id="c4248-136">You will need to do this for each of your shard databases, otherwise rows in multi-tenant shards will not be filtered.</span></span> 

## <a name="step-1-application-tier-set-tenantid-in-the-sessioncontext"></a><span data-ttu-id="c4248-137">步驟 1) 應用程式層：設定 SESSION_CONTEXT 中的 TenantId</span><span class="sxs-lookup"><span data-stu-id="c4248-137">Step 1) Application tier: Set TenantId in the SESSION_CONTEXT</span></span>
<span data-ttu-id="c4248-138">在使用彈性資料庫用戶端程式庫的資料依存路由 API 連接到分區資料庫後，應用程式仍需告訴資料庫哪個 TenantId 使用該連接，然後 RLS 安全性原則才能篩選掉屬於其他租用戶的資料列。</span><span class="sxs-lookup"><span data-stu-id="c4248-138">After connecting to a shard database using the elastic database client library’s data dependent routing APIs, the application still needs to tell the database which TenantId is using that connection so that an RLS security policy can filter out rows belonging to other tenants.</span></span> <span data-ttu-id="c4248-139">我們建議您傳遞此資訊的方式，是在 [SESSION_CONTEXT](https://msdn.microsoft.com/library/mt590806.aspx) 中儲存該連線目前的 TenantId。</span><span class="sxs-lookup"><span data-stu-id="c4248-139">The recommended way to pass this information is to store the current TenantId for that connection in the [SESSION_CONTEXT](https://msdn.microsoft.com/library/mt590806.aspx).</span></span> <span data-ttu-id="c4248-140">(注意：您也可以使用 [CONTEXT_INFO](https://msdn.microsoft.com/library/ms180125.aspx)，但 SESSION_CONTEXT 是比較理想的選項，因為它容易使用、預設會傳回 NULL，而且支援索引鍵-值組。)</span><span class="sxs-lookup"><span data-stu-id="c4248-140">(Note: You could alternatively use [CONTEXT_INFO](https://msdn.microsoft.com/library/ms180125.aspx), but SESSION_CONTEXT is a better option because it is easier to use, returns NULL by default, and supports key-value pairs.)</span></span>

### <a name="entity-framework"></a><span data-ttu-id="c4248-141">Entity Framework</span><span class="sxs-lookup"><span data-stu-id="c4248-141">Entity Framework</span></span>
<span data-ttu-id="c4248-142">對於使用 Entity Framework 的應用程式，最簡單的方法是在[使用 EF DbContext 的資料相依路由](sql-database-elastic-scale-use-entity-framework-applications-visual-studio.md#data-dependent-routing-using-ef-dbcontext)一文中所述的 ElasticScaleContext 覆寫中設定 SESSION_CONTEXT。</span><span class="sxs-lookup"><span data-stu-id="c4248-142">For applications using Entity Framework, the easiest approach is to set the SESSION_CONTEXT within the ElasticScaleContext override described in [Data Dependent Routing using EF DbContext](sql-database-elastic-scale-use-entity-framework-applications-visual-studio.md#data-dependent-routing-using-ef-dbcontext).</span></span> <span data-ttu-id="c4248-143">在傳回透過資料相依路由來代理的連線之前，只要建立並執行 SqlCommand，來將 SESSION_CONTEXT 中的「TenantId」設定為該連線專用的 shardingKey 即可。</span><span class="sxs-lookup"><span data-stu-id="c4248-143">Before returning the connection brokered through data dependent routing, simply create and execute a SqlCommand that sets 'TenantId' in the SESSION_CONTEXT to the shardingKey specified for that connection.</span></span> <span data-ttu-id="c4248-144">如此一來，您只需要編寫程式碼一次，就能設定 SESSION_CONTEXT。</span><span class="sxs-lookup"><span data-stu-id="c4248-144">This way, you only need to write code once to set the SESSION_CONTEXT.</span></span> 

```
// ElasticScaleContext.cs 
// ... 
// C'tor for data dependent routing. This call will open a validated connection routed to the proper 
// shard by the shard map manager. Note that the base class c'tor call will fail for an open connection 
// if migrations need to be done and SQL credentials are used. This is the reason for the  
// separation of c'tors into the DDR case (this c'tor) and the internal c'tor for new shards. 
public ElasticScaleContext(ShardMap shardMap, T shardingKey, string connectionStr)
    : base(OpenDDRConnection(shardMap, shardingKey, connectionStr), true /* contextOwnsConnection */)
{
}

public static SqlConnection OpenDDRConnection(ShardMap shardMap, T shardingKey, string connectionStr)
{
    // No initialization
    Database.SetInitializer<ElasticScaleContext<T>>(null);

    // Ask shard map to broker a validated connection for the given key
    SqlConnection conn = null;
    try
    {
        conn = shardMap.OpenConnectionForKey(shardingKey, connectionStr, ConnectionOptions.Validate);

        // Set TenantId in SESSION_CONTEXT to shardingKey to enable Row-Level Security filtering
        SqlCommand cmd = conn.CreateCommand();
        cmd.CommandText = @"exec sp_set_session_context @key=N'TenantId', @value=@shardingKey";
        cmd.Parameters.AddWithValue("@shardingKey", shardingKey);
        cmd.ExecuteNonQuery();

        return conn;
    }
    catch (Exception)
    {
        if (conn != null)
        {
            conn.Dispose();
        }

        throw;
    }
} 
// ... 
```

<span data-ttu-id="c4248-145">現在，每次叫用 ElasticScaleContext 時，就會使用指定的 TenantId 來自動設定 SESSION_CONTEXT：</span><span class="sxs-lookup"><span data-stu-id="c4248-145">Now the SESSION_CONTEXT is automatically set with the specified TenantId whenever ElasticScaleContext is invoked:</span></span> 

```
// Program.cs 
SqlDatabaseUtils.SqlRetryPolicy.ExecuteAction(() => 
{   
    using (var db = new ElasticScaleContext<int>(sharding.ShardMap, tenantId, connStrBldr.ConnectionString))   
    {     
        var query = from b in db.Blogs
                    orderby b.Name
                    select b;

        Console.WriteLine("All blogs for TenantId {0}:", tenantId);     
        foreach (var item in query)     
        {       
            Console.WriteLine(item.Name);     
        }   
    } 
}); 
```

### <a name="adonet-sqlclient"></a><span data-ttu-id="c4248-146">ADO.NET SqlClient</span><span class="sxs-lookup"><span data-stu-id="c4248-146">ADO.NET SqlClient</span></span>
<span data-ttu-id="c4248-147">針對使用 ADO.NET SqlClient 的應用程式，我們建議您在 ShardMap.OpenConnectionForKey() 周圍建立包裝函式，以便在傳回連線之前自動把 SESSION_CONTEXT 中的「TenantId」設定為正確的 TenantId。</span><span class="sxs-lookup"><span data-stu-id="c4248-147">For applications using ADO.NET SqlClient, the recommended approach is to create a wrapper function around ShardMap.OpenConnectionForKey() that automatically sets 'TenantId' in the SESSION_CONTEXT to the correct TenantId before returning a connection.</span></span> <span data-ttu-id="c4248-148">如要確保 SESSION_CONTEXT 一定是設定好的，請務必只使用此包裝函式來開啟連線。</span><span class="sxs-lookup"><span data-stu-id="c4248-148">To ensure that SESSION_CONTEXT is always set, you should only open connections using this wrapper function.</span></span>

```
// Program.cs
// ...

// Wrapper function for ShardMap.OpenConnectionForKey() that automatically sets SESSION_CONTEXT with the correct
// tenantId before returning a connection. As a best practice, you should only open connections using this 
// method to ensure that SESSION_CONTEXT is always set before executing a query.
public static SqlConnection OpenConnectionForTenant(ShardMap shardMap, int tenantId, string connectionStr)
{
    SqlConnection conn = null;
    try
    {
        // Ask shard map to broker a validated connection for the given key
        conn = shardMap.OpenConnectionForKey(tenantId, connectionStr, ConnectionOptions.Validate);

        // Set TenantId in SESSION_CONTEXT to shardingKey to enable Row-Level Security filtering
        SqlCommand cmd = conn.CreateCommand();
        cmd.CommandText = @"exec sp_set_session_context @key=N'TenantId', @value=@shardingKey";
        cmd.Parameters.AddWithValue("@shardingKey", tenantId);
        cmd.ExecuteNonQuery();

        return conn;
    }
    catch (Exception)
    {
        if (conn != null)
        {
            conn.Dispose();
        }

        throw;
    }
}

// ...

// Example query via ADO.NET SqlClient
// If row-level security is enabled, only Tenant 4's blogs will be listed
SqlDatabaseUtils.SqlRetryPolicy.ExecuteAction(() =>
{
    using (SqlConnection conn = OpenConnectionForTenant(sharding.ShardMap, tenantId4, connStrBldr.ConnectionString))
    {
        SqlCommand cmd = conn.CreateCommand();
        cmd.CommandText = @"SELECT * FROM Blogs";

        Console.WriteLine("--\nAll blogs for TenantId {0} (using ADO.NET SqlClient):", tenantId4);
        SqlDataReader reader = cmd.ExecuteReader();
        while (reader.Read())
        {
            Console.WriteLine("{0}", reader["Name"]);
        }
    }
});

```

## <a name="step-2-data-tier-create-row-level-security-policy"></a><span data-ttu-id="c4248-149">步驟 2) 資料層：建立資料列層級的安全性原則</span><span class="sxs-lookup"><span data-stu-id="c4248-149">Step 2) Data tier: Create row-level security policy</span></span>
### <a name="create-a-security-policy-to-filter-the-rows-each-tenant-can-access"></a><span data-ttu-id="c4248-150">建立安全性原則來篩選每個租用戶可以存取的資料列</span><span class="sxs-lookup"><span data-stu-id="c4248-150">Create a security policy to filter the rows each tenant can access</span></span>
<span data-ttu-id="c4248-151">現在應用程式會在查詢之前，使用目前的 TenantId 來設定 SESSION_CONTEXT，RLS 安全性原則也會篩選查詢，並排除有不同 TenantId 的資料列。</span><span class="sxs-lookup"><span data-stu-id="c4248-151">Now that the application is setting SESSION_CONTEXT with the current TenantId before querying, an RLS security policy can filter queries and exclude rows that have a different TenantId.</span></span>  

<span data-ttu-id="c4248-152">RLS 已在 T-SQL 中實作 ：使用者定義的函數會定義存取邏輯，而安全性原則會將此函數繫結至任何數目的資料表。</span><span class="sxs-lookup"><span data-stu-id="c4248-152">RLS is implemented in T-SQL: a user-defined function defines the access logic, and a security policy binds this function to any number of tables.</span></span> <span data-ttu-id="c4248-153">就此專案而言，函數只會確認該應用程式 (而非其他的 SQL 使用者) 是否連線至資料庫，且儲存在 SESSION_CONTEXT 中的「TenantId」是否符合特定資料列的 TenantId。</span><span class="sxs-lookup"><span data-stu-id="c4248-153">For this project, the function will simply verify that the application (rather than some other SQL user) is connected to the database, and that the 'TenantId' stored in the SESSION_CONTEXT matches the TenantId of a given row.</span></span> <span data-ttu-id="c4248-154">篩選述詞可讓符合這些條件的資料列通過 SELECT、UPDATE 和 DELETE 查詢的篩選；而封鎖述詞會避免違反這些條件的資料列進行 INSERT 或 UPDATE。</span><span class="sxs-lookup"><span data-stu-id="c4248-154">A filter predicate will allow rows that meet these conditions to pass through the filter for SELECT, UPDATE, and DELETE queries; and a block predicate will prevent rows that violate these conditions from being INSERTed or UPDATEd.</span></span> <span data-ttu-id="c4248-155">如果尚未設定 SESSION_CONTEXT，它會傳回 NULL，而且看不見或無法插入任何資料列。</span><span class="sxs-lookup"><span data-stu-id="c4248-155">If SESSION_CONTEXT has not been set, it will return NULL and no rows will be visible or able to be inserted.</span></span> 

<span data-ttu-id="c4248-156">若要啟用 RLS，可以使用 Visual Studio (SSDT)、SSMS 或包含在專案中的 PowerShell 指令碼，在所有分區上執行以下 T-SQL (或者，如果您使用 [彈性資料庫工作](sql-database-elastic-jobs-overview.md)，您可以用它在所有分區上自動執行此 T-SQL)：</span><span class="sxs-lookup"><span data-stu-id="c4248-156">To enable RLS, execute the following T-SQL on all shards using either Visual Studio (SSDT), SSMS, or the PowerShell script included in the project (or if you are using [Elastic Database Jobs](sql-database-elastic-jobs-overview.md), you can use it to automate execution of this T-SQL on all shards):</span></span> 

```
CREATE SCHEMA rls -- separate schema to organize RLS objects 
GO

CREATE FUNCTION rls.fn_tenantAccessPredicate(@TenantId int)     
    RETURNS TABLE     
    WITH SCHEMABINDING
AS
    RETURN SELECT 1 AS fn_accessResult          
        WHERE DATABASE_PRINCIPAL_ID() = DATABASE_PRINCIPAL_ID('dbo') -- the user in your application’s connection string (dbo is only for demo purposes!)         
        AND CAST(SESSION_CONTEXT(N'TenantId') AS int) = @TenantId
GO

CREATE SECURITY POLICY rls.tenantAccessPolicy
    ADD FILTER PREDICATE rls.fn_tenantAccessPredicate(TenantId) ON dbo.Blogs,
    ADD BLOCK PREDICATE rls.fn_tenantAccessPredicate(TenantId) ON dbo.Blogs,
    ADD FILTER PREDICATE rls.fn_tenantAccessPredicate(TenantId) ON dbo.Posts,
    ADD BLOCK PREDICATE rls.fn_tenantAccessPredicate(TenantId) ON dbo.Posts
GO 
```

> [!TIP]
> <span data-ttu-id="c4248-157">如果是更複雜的專案 (需要在數百個資料表上加入述詞)，您可以使用協助程式預存程序來自動產生安全性原則，藉此為結構描述中的所有資料表加入述詞。</span><span class="sxs-lookup"><span data-stu-id="c4248-157">For more complex projects that need to add the predicate on hundreds of tables, you can use a helper stored procedure that automatically generates a security policy adding a predicate on all tables in a schema.</span></span> <span data-ttu-id="c4248-158">請參閱[將資料列層級安全性套用至所有資料表 - 協助程式指令碼 (英文) (部落格)](http://blogs.msdn.com/b/sqlsecurity/archive/2015/03/31/apply-row-level-security-to-all-tables-helper-script)。</span><span class="sxs-lookup"><span data-stu-id="c4248-158">See [Apply Row-Level Security to all tables - helper script (blog)](http://blogs.msdn.com/b/sqlsecurity/archive/2015/03/31/apply-row-level-security-to-all-tables-helper-script).</span></span>  
> 
> 

<span data-ttu-id="c4248-159">現在，如果您再次執行範例應用程式，租用戶將只能看到屬於自己的資料列。</span><span class="sxs-lookup"><span data-stu-id="c4248-159">Now if you run the sample application again, tenants will able to see only rows that belong to them.</span></span> <span data-ttu-id="c4248-160">此外，應用程式無法插入目前沒有連線到分區資料庫的租用戶所屬的資料列，也無法更新擁有不同 TenantId 的可見資料列。</span><span class="sxs-lookup"><span data-stu-id="c4248-160">In addition, the application cannot insert rows that belong to tenants other than the one currently connected to the shard database, and it cannot update visible rows to have a different TenantId.</span></span> <span data-ttu-id="c4248-161">如果應用程式嘗試執行這兩項作業，就會引發 DbUpdateException。</span><span class="sxs-lookup"><span data-stu-id="c4248-161">If the application attempts to do either, a DbUpdateException will be raised.</span></span>

<span data-ttu-id="c4248-162">如果您是在之後加入新的資料表，您只要「變更」安全性原則，並在新的資料表上加入篩選和封鎖述詞即可：</span><span class="sxs-lookup"><span data-stu-id="c4248-162">If you add a new table later on, simply ALTER the security policy and add filter and block predicates on the new table:</span></span> 

```
ALTER SECURITY POLICY rls.tenantAccessPolicy     
    ADD FILTER PREDICATE rls.fn_tenantAccessPredicate(TenantId) ON dbo.MyNewTable,
    ADD BLOCK PREDICATE rls.fn_tenantAccessPredicate(TenantId) ON dbo.MyNewTable
GO 
```

### <a name="add-default-constraints-to-automatically-populate-tenantid-for-inserts"></a><span data-ttu-id="c4248-163">加入預設條件約束來為插入自動填入 TenantId</span><span class="sxs-lookup"><span data-stu-id="c4248-163">Add default constraints to automatically populate TenantId for INSERTs</span></span>
<span data-ttu-id="c4248-164">您可以在每個資料表上放置預設條件約束，以在插入資料列時，以 SESSION_CONTEXT 中目前儲存的值自動填入 TenantId。</span><span class="sxs-lookup"><span data-stu-id="c4248-164">You can put a default constraint on each table to automatically populate the TenantId with the value currently stored in SESSION_CONTEXT when inserting rows.</span></span> <span data-ttu-id="c4248-165">例如：</span><span class="sxs-lookup"><span data-stu-id="c4248-165">For example:</span></span> 

```
-- Create default constraints to auto-populate TenantId with the value of SESSION_CONTEXT for inserts 
ALTER TABLE Blogs     
    ADD CONSTRAINT df_TenantId_Blogs      
    DEFAULT CAST(SESSION_CONTEXT(N'TenantId') AS int) FOR TenantId 
GO

ALTER TABLE Posts     
    ADD CONSTRAINT df_TenantId_Posts      
    DEFAULT CAST(SESSION_CONTEXT(N'TenantId') AS int) FOR TenantId 
GO 
```

<span data-ttu-id="c4248-166">現在應用程式不需要在插入資料列時指定 TenantId：</span><span class="sxs-lookup"><span data-stu-id="c4248-166">Now the application does not need to specify a TenantId when inserting rows:</span></span> 

```
SqlDatabaseUtils.SqlRetryPolicy.ExecuteAction(() => 
{   
    using (var db = new ElasticScaleContext<int>(sharding.ShardMap, tenantId, connStrBldr.ConnectionString))
    {
        var blog = new Blog { Name = name }; // default constraint sets TenantId automatically     
        db.Blogs.Add(blog);     
        db.SaveChanges();   
    } 
}); 
```

> [!NOTE]
> <span data-ttu-id="c4248-167">如果您需要針對 Entity Framework 專案使用預設條件約束，建議您「不要」在 EF 資料模型中包含 TenantId 資料行。</span><span class="sxs-lookup"><span data-stu-id="c4248-167">If you use default constraints for an Entity Framework project, it is recommended that you do NOT include the TenantId column in your EF data model.</span></span> <span data-ttu-id="c4248-168">這是因為 Entity Framework 查詢會自動提供預設值，來覆寫 T-SQL 中使用 SESSION_CONTEXT 建立的預設條件約束。</span><span class="sxs-lookup"><span data-stu-id="c4248-168">This is because Entity Framework queries automatically supply default values which will override the default constraints created in T-SQL that use SESSION_CONTEXT.</span></span> <span data-ttu-id="c4248-169">若要使用範例專案中的預設條件約束，舉例來說，您可以從 DataClasses.cs 移除 TenantId (並在 Package Manager Console 中執行 Add-Migration)，然後使用 T-SQL 確保欄位只存在於資料庫資料表中。</span><span class="sxs-lookup"><span data-stu-id="c4248-169">To use default constraints in the sample project, for instance, you should remove TenantId from DataClasses.cs (and run Add-Migration in the Package Manager Console) and use T-SQL to ensure that the field only exists in the database tables.</span></span> <span data-ttu-id="c4248-170">如此一來，EF 就不會在插入資料時，自動提供不正確的預設值。</span><span class="sxs-lookup"><span data-stu-id="c4248-170">This way, EF will not automatically supply incorrect default values when inserting data.</span></span> 
> 
> 

### <a name="optional-enable-a-superuser-to-access-all-rows"></a><span data-ttu-id="c4248-171">(選擇性) 啟用「進階使用者」來存取所有資料列</span><span class="sxs-lookup"><span data-stu-id="c4248-171">(Optional) Enable a "superuser" to access all rows</span></span>
<span data-ttu-id="c4248-172">有些應用程式可能需要建立一個能夠存取所有資料列的「進階使用者」，比方說，為了跨所有分區上的所有租用戶來產生報告，或在牽涉到資料庫之間移動租用戶資料列的分區上執行分割/合併作業。</span><span class="sxs-lookup"><span data-stu-id="c4248-172">Some applications may want to create a "superuser" who can access all rows, for instance, in order to enable reporting across all tenants on all shards, or to perform Split/Merge operations on shards that involve moving tenant rows between databases.</span></span> <span data-ttu-id="c4248-173">為了達成此目的，您應該在每個分區資料庫中建立新的 SQL 使用者 (在本例中為 "superuser")。</span><span class="sxs-lookup"><span data-stu-id="c4248-173">To enable this, you should create a new SQL user ("superuser" in this example) in each shard database.</span></span> <span data-ttu-id="c4248-174">然後使用新的述詞函式修改安全性原則，允許此使用者存取所有資料列：</span><span class="sxs-lookup"><span data-stu-id="c4248-174">Then alter the security policy with a new predicate function that allows this user to access all rows:</span></span>

```
-- New predicate function that adds superuser logic
CREATE FUNCTION rls.fn_tenantAccessPredicateWithSuperUser(@TenantId int)
    RETURNS TABLE
    WITH SCHEMABINDING
AS
    RETURN SELECT 1 AS fn_accessResult 
        WHERE 
        (
            DATABASE_PRINCIPAL_ID() = DATABASE_PRINCIPAL_ID('dbo') -- note, should not be dbo!
            AND CAST(SESSION_CONTEXT(N'TenantId') AS int) = @TenantId
        ) 
        OR
        (
            DATABASE_PRINCIPAL_ID() = DATABASE_PRINCIPAL_ID('superuser')
        )
GO

-- Atomically swap in the new predicate function on each table
ALTER SECURITY POLICY rls.tenantAccessPolicy
    ALTER FILTER PREDICATE rls.fn_tenantAccessPredicateWithSuperUser(TenantId) ON dbo.Blogs,
    ALTER BLOCK PREDICATE rls.fn_tenantAccessPredicateWithSuperUser(TenantId) ON dbo.Blogs,
    ALTER FILTER PREDICATE rls.fn_tenantAccessPredicateWithSuperUser(TenantId) ON dbo.Posts,
    ALTER BLOCK PREDICATE rls.fn_tenantAccessPredicateWithSuperUser(TenantId) ON dbo.Posts
GO
```


### <a name="maintenance"></a><span data-ttu-id="c4248-175">維護</span><span class="sxs-lookup"><span data-stu-id="c4248-175">Maintenance</span></span>
* <span data-ttu-id="c4248-176">**新增分區**：您必須執行 T-SQL 指令碼來啟用所有新分區上的 RLS，否則系統不會篩選這些分區的查詢。</span><span class="sxs-lookup"><span data-stu-id="c4248-176">**Adding new shards**: You must execute the T-SQL script to enable RLS on any new shards, otherwise queries on these shards will not be filtered.</span></span>
* <span data-ttu-id="c4248-177">**新增資料表**：您必須在每次有新的資料表建立時，將篩選和封鎖述詞新增到所有分區的安全性原則，否則系統將不會篩選針對新資料表的查詢。</span><span class="sxs-lookup"><span data-stu-id="c4248-177">**Adding new tables**: You must add a filter and block predicate to the security policy on all shards whenever a new table is created, otherwise queries on the new table will not be filtered.</span></span> <span data-ttu-id="c4248-178">如 [自動將資料列層級安全性套用至新建立的資料表 (部落格)](http://blogs.msdn.com/b/sqlsecurity/archive/2015/05/22/apply-row-level-security-automatically-to-newly-created-tables.aspx)中所述，這部分可以使用 DDL 觸發程序來自動執行。</span><span class="sxs-lookup"><span data-stu-id="c4248-178">This can be automated using a DDL trigger, as described in [Apply Row-Level Security automatically to newly created tables (blog)](http://blogs.msdn.com/b/sqlsecurity/archive/2015/05/22/apply-row-level-security-automatically-to-newly-created-tables.aspx).</span></span>

## <a name="summary"></a><span data-ttu-id="c4248-179">摘要</span><span class="sxs-lookup"><span data-stu-id="c4248-179">Summary</span></span>
<span data-ttu-id="c4248-180">您可以將彈性資料庫工具與資料列層級安全性搭配使用，以支援多租用戶和單一租用戶的分區，藉此向外延展應用程式的資料層。</span><span class="sxs-lookup"><span data-stu-id="c4248-180">Elastic database tools and row-level security can be used together to scale out an application’s data tier with support for both multi-tenant and single-tenant shards.</span></span> <span data-ttu-id="c4248-181">多租用戶分區可以用來更有效率地儲存資料 (特別是在有大量租用戶，卻只有些許資料列的情況)，而單一租用戶分區則可以用來支援高階租用戶，因為這類租用戶有更嚴格的效能和隔離需求。</span><span class="sxs-lookup"><span data-stu-id="c4248-181">Multi-tenant shards can be used to store data more efficiently (particularly in cases where a large number of tenants have only a few rows of data), while single-tenant shards can be used to support premium tenants with stricter performance and isolation requirements.</span></span>  <span data-ttu-id="c4248-182">如需詳細資訊，請參閱 [資料列層級安全性參考資料](https://msdn.microsoft.com/library/dn765131)。</span><span class="sxs-lookup"><span data-stu-id="c4248-182">For more information, see [Row-Level Security reference](https://msdn.microsoft.com/library/dn765131).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="c4248-183">其他資源</span><span class="sxs-lookup"><span data-stu-id="c4248-183">Additional resources</span></span>
* [<span data-ttu-id="c4248-184">什麼是 Azure 彈性集區？</span><span class="sxs-lookup"><span data-stu-id="c4248-184">What is an Azure elastic pool?</span></span>](sql-database-elastic-pool.md)
* [<span data-ttu-id="c4248-185">使用 Azure SQL Database 相應放大</span><span class="sxs-lookup"><span data-stu-id="c4248-185">Scaling out with Azure SQL Database</span></span>](sql-database-elastic-scale-introduction.md)
* [<span data-ttu-id="c4248-186">多租用戶 SaaS 應用程式與 Azure SQL Database 的設計模式</span><span class="sxs-lookup"><span data-stu-id="c4248-186">Design Patterns for Multi-tenant SaaS Applications with Azure SQL Database</span></span>](sql-database-design-patterns-multi-tenancy-saas-applications.md)
* [<span data-ttu-id="c4248-187">使用 Azure AD 和 OpenID Connect 的多租用戶應用程式驗證</span><span class="sxs-lookup"><span data-stu-id="c4248-187">Authentication in multitenant apps, using Azure AD and OpenID Connect</span></span>](../guidance/guidance-multitenant-identity-authenticate.md)
* [<span data-ttu-id="c4248-188">Tailspin Surveys 應用程式</span><span class="sxs-lookup"><span data-stu-id="c4248-188">Tailspin Surveys application</span></span>](../guidance/guidance-multitenant-identity-tailspin.md)

## <a name="questions-and-feature-requests"></a><span data-ttu-id="c4248-189">問題和功能要求</span><span class="sxs-lookup"><span data-stu-id="c4248-189">Questions and Feature Requests</span></span>
<span data-ttu-id="c4248-190">如有問題，請透過 [SQL Database 論壇](http://social.msdn.microsoft.com/forums/azure/home?forum=ssdsgetstarted)與我們連絡，如需要求增加功能，請將這些功能新增至 [SQL Database 意見反應論壇](https://feedback.azure.com/forums/217321-sql-database/)。</span><span class="sxs-lookup"><span data-stu-id="c4248-190">For questions, please reach out to us on the [SQL Database forum](http://social.msdn.microsoft.com/forums/azure/home?forum=ssdsgetstarted) and for feature requests, please add them to the [SQL Database feedback forum](https://feedback.azure.com/forums/217321-sql-database/).</span></span>

<!--Image references-->
[1]: ./media/sql-database-elastic-tools-multi-tenant-row-level-security/blogging-app.png
<!--anchors-->


