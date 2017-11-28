---
title: "aaaMulti 租用戶應用程式的彈性資料庫工具和資料列層級安全性"
description: "了解 toouse 彈性資料庫工具，並搭配資料列層級安全性 toobuild 上支援多租用戶分區的 Azure SQL Database 高可擴充的資料層應用程式的方式。"
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
ms.openlocfilehash: e00076a8db4a295374993aedd49f2318bd4d701d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="multi-tenant-applications-with-elastic-database-tools-and-row-level-security"></a><span data-ttu-id="32c77-103">使用彈性資料庫工具和資料列層級安全性的多租用戶應用程式</span><span class="sxs-lookup"><span data-stu-id="32c77-103">Multi-tenant applications with elastic database tools and row-level security</span></span>
<span data-ttu-id="32c77-104">[彈性資料庫工具](sql-database-elastic-scale-get-started.md)和[資料列層級安全性 (RLS)](https://msdn.microsoft.com/library/dn765131)提供一組功能強大的功能，以更有彈性且有效率地調整多租用戶應用程式使用 Azure SQL Database hello 資料層。</span><span class="sxs-lookup"><span data-stu-id="32c77-104">[Elastic database tools](sql-database-elastic-scale-get-started.md) and [row-level security (RLS)](https://msdn.microsoft.com/library/dn765131) offer a powerful set of capabilities for flexibly and efficiently scaling hello data tier of a multi-tenant application with Azure SQL Database.</span></span> <span data-ttu-id="32c77-105">如需詳細資訊，請參閱 [多租用戶 SaaS 應用程式與 Azure SQL Database 的設計模式](sql-database-design-patterns-multi-tenancy-saas-applications.md) 。</span><span class="sxs-lookup"><span data-stu-id="32c77-105">See [Design Patterns for Multi-tenant SaaS Applications with Azure SQL Database](sql-database-design-patterns-multi-tenancy-saas-applications.md) for more information.</span></span> 

<span data-ttu-id="32c77-106">本文將說明如何 toouse 這些技術一起 toobuild 與支援多租用戶分區，使用高擴充性的資料層應用程式**ADO.NET SqlClient**及/或**Entity Framework**.</span><span class="sxs-lookup"><span data-stu-id="32c77-106">This article illustrates how toouse these technologies together toobuild an application with a highly scalable data tier that supports multi-tenant shards, using **ADO.NET SqlClient** and/or **Entity Framework**.</span></span>  

* <span data-ttu-id="32c77-107">**彈性資料庫工具**可讓開發人員 tooscale 出 hello 資料層應用程式，透過使用.NET 程式庫和 Azure 服務範本的一組業界標準的分區化作法。</span><span class="sxs-lookup"><span data-stu-id="32c77-107">**Elastic database tools** enables developers tooscale out hello data tier of an application via industry-standard sharding practices using a set of .NET libraries and Azure service templates.</span></span> <span data-ttu-id="32c77-108">管理與使用 hello 彈性資料庫用戶端程式庫的分區，可協助自動化及簡化許多 hello 實際上通常相關聯的工作與分區化。</span><span class="sxs-lookup"><span data-stu-id="32c77-108">Managing shards with using hello Elastic Database Client Library helps automate and streamline many of hello infrastructural tasks typically associated with sharding.</span></span> 
* <span data-ttu-id="32c77-109">**資料列層級安全性**hello 相同資料庫使用安全性原則 toofilter 出不屬於 toohello 租用戶執行查詢的資料列中的多個租用戶可以讓開發人員 toostore 資料。</span><span class="sxs-lookup"><span data-stu-id="32c77-109">**Row-level security** enables developers toostore data for multiple tenants in hello same database using security policies toofilter out rows that do not belong toohello tenant executing a query.</span></span> <span data-ttu-id="32c77-110">集中存取的邏輯與 RLS hello 資料庫而不是比在 hello 應用程式，可簡化維護和減少錯誤 hello 風險，因為應用程式的程式碼基底會成長。</span><span class="sxs-lookup"><span data-stu-id="32c77-110">Centralizing access logic with RLS inside hello database, rather than in hello application, simplifies maintenance and reduces hello risk of error as an application’s codebase grows.</span></span> 

<span data-ttu-id="32c77-111">一起使用這些功能，應用程式可以藉由儲存資料的多個租用戶中 hello 相同從成本的節省空間及效率提升獲益分區資料庫。</span><span class="sxs-lookup"><span data-stu-id="32c77-111">Using these features together, an application can benefit from cost savings and efficiency gains by storing data for multiple tenants in hello same shard database.</span></span> <span data-ttu-id="32c77-112">Hello 在同一時間，應用程式仍會具有 hello 彈性 toooffer 隔離，「 高階 」 租用戶需要更嚴格的效能保證，因為多租用戶分區不保證相同資源發佈在租用戶之間的單一租用戶分區。</span><span class="sxs-lookup"><span data-stu-id="32c77-112">At hello same time, an application still has hello flexibility toooffer isolated, single-tenant shards for “premium” tenants who require stricter performance guarantees since multi-tenant shards do not guarantee equal resource distribution among tenants.</span></span>  

<span data-ttu-id="32c77-113">簡單地說，hello 彈性資料庫用戶端程式庫的[資料依存路由](sql-database-elastic-scale-data-dependent-routing.md)Api 自動連線包含其分區化索引鍵 (通常"TenantId") 的租用戶 toohello 正確的分區化資料庫。</span><span class="sxs-lookup"><span data-stu-id="32c77-113">In short, hello elastic database client library’s [data dependent routing](sql-database-elastic-scale-data-dependent-routing.md) APIs automatically connect tenants toohello correct shard database containing their sharding key (generally a “TenantId”).</span></span> <span data-ttu-id="32c77-114">一旦連接之後，可確保租用戶只能存取資料列包含其 TenantId hello 資料庫內的 RLS 安全性原則。</span><span class="sxs-lookup"><span data-stu-id="32c77-114">Once connected, an RLS security policy within hello database ensures that tenants can only access rows that contain their TenantId.</span></span> <span data-ttu-id="32c77-115">它會假設所有的資料表包含的資料列屬於 tooeach 租用戶的 TenantId 資料行 tooindicate。</span><span class="sxs-lookup"><span data-stu-id="32c77-115">It is assumed that all tables contain a TenantId column tooindicate which rows belong tooeach tenant.</span></span> 

![部落格應用程式架構][1]

## <a name="download-hello-sample-project"></a><span data-ttu-id="32c77-117">下載 hello 範例專案</span><span class="sxs-lookup"><span data-stu-id="32c77-117">Download hello sample project</span></span>
### <a name="prerequisites"></a><span data-ttu-id="32c77-118">必要條件</span><span class="sxs-lookup"><span data-stu-id="32c77-118">Prerequisites</span></span>
* <span data-ttu-id="32c77-119">使用 Visual Studio (2012 或更新版本)</span><span class="sxs-lookup"><span data-stu-id="32c77-119">Use Visual Studio (2012 or higher)</span></span> 
* <span data-ttu-id="32c77-120">建立三個 Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="32c77-120">Create three Azure SQL Databases</span></span> 
* <span data-ttu-id="32c77-121">下載範例專案： [Azure SQL 的彈性資料庫工具：多租用戶分區](http://go.microsoft.com/?linkid=9888163)</span><span class="sxs-lookup"><span data-stu-id="32c77-121">Download sample project: [Elastic DB Tools for Azure SQL - Multi-Tenant Shards](http://go.microsoft.com/?linkid=9888163)</span></span>
  * <span data-ttu-id="32c77-122">填寫您的資料庫在 hello 開頭的 hello 資訊**Program.cs**</span><span class="sxs-lookup"><span data-stu-id="32c77-122">Fill in hello information for your databases at hello beginning of **Program.cs**</span></span> 

<span data-ttu-id="32c77-123">這個專案會擴充其中一個所述的 hello[彈性 DB 工具適用於 Azure SQL 的實體架構整合](sql-database-elastic-scale-use-entity-framework-applications-visual-studio.md)藉由新增多租用戶分區化資料庫的支援。</span><span class="sxs-lookup"><span data-stu-id="32c77-123">This project extends hello one described in [Elastic DB Tools for Azure SQL - Entity Framework Integration](sql-database-elastic-scale-use-entity-framework-applications-visual-studio.md) by adding support for multi-tenant shard databases.</span></span> <span data-ttu-id="32c77-124">它會建置簡單的主控台應用程式建立部落格和文章，具有四個租用戶和多租用戶分區的兩個資料庫 hello 上面圖表中所示。</span><span class="sxs-lookup"><span data-stu-id="32c77-124">It builds a simple console application for creating blogs and posts, with four tenants and two multi-tenant shard databases as illustrated in hello above diagram.</span></span> 

<span data-ttu-id="32c77-125">建置並執行 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="32c77-125">Build and run hello application.</span></span> <span data-ttu-id="32c77-126">這會啟動 hello 彈性資料庫工具的分區對應管理員和下列測試回合的 hello:</span><span class="sxs-lookup"><span data-stu-id="32c77-126">This will bootstrap hello elastic database tools’ shard map manager and run hello following tests:</span></span> 

1. <span data-ttu-id="32c77-127">使用 Entity Framework 和 LINQ，建立新的部落格，然後顯示每個租用戶的所有部落格</span><span class="sxs-lookup"><span data-stu-id="32c77-127">Using Entity Framework and LINQ, create a new blog and then display all blogs for each tenant</span></span>
2. <span data-ttu-id="32c77-128">使用 ADO.NET SqlClient，顯示某個租用戶的所有部落格</span><span class="sxs-lookup"><span data-stu-id="32c77-128">Using ADO.NET SqlClient, display all blogs for a tenant</span></span>
3. <span data-ttu-id="32c77-129">再試一次 tooinsert hello 錯誤租用戶 tooverify，所擲回錯誤的部落格</span><span class="sxs-lookup"><span data-stu-id="32c77-129">Try tooinsert a blog for hello wrong tenant tooverify that an error is thrown</span></span>  

<span data-ttu-id="32c77-130">請注意，因為 RLS 尚未啟用 hello 分區化資料庫中，這些測試會顯示問題： 租用戶可以 toosee 部落格不屬於 toothem，而且 hello 應用程式不阻止插入 hello 錯誤租用戶的部落格。</span><span class="sxs-lookup"><span data-stu-id="32c77-130">Notice that because RLS has not yet been enabled in hello shard databases, each of these tests reveals a problem: tenants are able toosee blogs that do not belong toothem, and hello application is not prevented from inserting a blog for hello wrong tenant.</span></span> <span data-ttu-id="32c77-131">hello 這篇文章的其餘部分描述如何 tooresolve 這些問題，方法是強制租用戶隔離 rls。</span><span class="sxs-lookup"><span data-stu-id="32c77-131">hello remainder of this article describes how tooresolve these problems by enforcing tenant isolation with RLS.</span></span> <span data-ttu-id="32c77-132">有兩個步驟：</span><span class="sxs-lookup"><span data-stu-id="32c77-132">There are two steps:</span></span> 

1. <span data-ttu-id="32c77-133">**應用程式層**: hello 應用程式程式碼修改 tooalways 集開啟連線後 hello hello SESSION_CONTEXT 中目前的 TenantId。</span><span class="sxs-lookup"><span data-stu-id="32c77-133">**Application tier**: Modify hello application code tooalways set hello current TenantId in hello SESSION_CONTEXT after opening a connection.</span></span> <span data-ttu-id="32c77-134">hello 範例專案已執行此作業。</span><span class="sxs-lookup"><span data-stu-id="32c77-134">hello sample project has already done this.</span></span> 
2. <span data-ttu-id="32c77-135">**資料層**: hello TenantId 為基礎的資料列儲存在 SESSION_CONTEXT 每個分區化資料庫 toofilter 中建立 RLS 安全性原則。</span><span class="sxs-lookup"><span data-stu-id="32c77-135">**Data tier**: Create an RLS security policy in each shard database toofilter rows based on hello TenantId stored in SESSION_CONTEXT.</span></span> <span data-ttu-id="32c77-136">您將需要 toodo 這針對每個分區化資料庫，否則不會篩選資料列，在多租用戶分區中。</span><span class="sxs-lookup"><span data-stu-id="32c77-136">You will need toodo this for each of your shard databases, otherwise rows in multi-tenant shards will not be filtered.</span></span> 

## <a name="step-1-application-tier-set-tenantid-in-hello-sessioncontext"></a><span data-ttu-id="32c77-137">步驟 1） 應用程式層： hello SESSION_CONTEXT 中設定的 TenantId</span><span class="sxs-lookup"><span data-stu-id="32c77-137">Step 1) Application tier: Set TenantId in hello SESSION_CONTEXT</span></span>
<span data-ttu-id="32c77-138">使用 hello 彈性資料庫用戶端程式庫的資料依存路由的 Api，hello 應用程式仍然連接 tooa 分區資料庫需要 tootell hello 資料庫之後的 TenantId 使用該連線，以便 RLS 安全性原則可以篩選掉資料列屬於 tooother 租用戶。</span><span class="sxs-lookup"><span data-stu-id="32c77-138">After connecting tooa shard database using hello elastic database client library’s data dependent routing APIs, hello application still needs tootell hello database which TenantId is using that connection so that an RLS security policy can filter out rows belonging tooother tenants.</span></span> <span data-ttu-id="32c77-139">hello 這項資訊的建議的方式 toopass toostore hello hello，在該連接的目前 TenantId [SESSION_CONTEXT](https://msdn.microsoft.com/library/mt590806.aspx)。</span><span class="sxs-lookup"><span data-stu-id="32c77-139">hello recommended way toopass this information is toostore hello current TenantId for that connection in hello [SESSION_CONTEXT](https://msdn.microsoft.com/library/mt590806.aspx).</span></span> <span data-ttu-id="32c77-140">(注意： 或者，您無法使用[CONTEXT_INFO](https://msdn.microsoft.com/library/ms180125.aspx)，但 SESSION_CONTEXT 是更好的選項，因為後者較容易 toouse、 依預設，會傳回 NULL 且支援索引鍵-值組。)</span><span class="sxs-lookup"><span data-stu-id="32c77-140">(Note: You could alternatively use [CONTEXT_INFO](https://msdn.microsoft.com/library/ms180125.aspx), but SESSION_CONTEXT is a better option because it is easier toouse, returns NULL by default, and supports key-value pairs.)</span></span>

### <a name="entity-framework"></a><span data-ttu-id="32c77-141">Entity Framework</span><span class="sxs-lookup"><span data-stu-id="32c77-141">Entity Framework</span></span>
<span data-ttu-id="32c77-142">使用 Entity Framework 應用程式，如 hello 最簡單方法是 SESSION_CONTEXT hello ElasticScaleContext 覆寫中的所述的 tooset hello[資料使用 EF DbContext 依存路由](sql-database-elastic-scale-use-entity-framework-applications-visual-studio.md#data-dependent-routing-using-ef-dbcontext)。</span><span class="sxs-lookup"><span data-stu-id="32c77-142">For applications using Entity Framework, hello easiest approach is tooset hello SESSION_CONTEXT within hello ElasticScaleContext override described in [Data Dependent Routing using EF DbContext](sql-database-elastic-scale-use-entity-framework-applications-visual-studio.md#data-dependent-routing-using-ef-dbcontext).</span></span> <span data-ttu-id="32c77-143">後再傳回由資料依存路由代理 hello 連接，只要建立並執行 hello SESSION_CONTEXT toohello shardingKey 指定該連接的設定 'TenantId' 的 SqlCommand。</span><span class="sxs-lookup"><span data-stu-id="32c77-143">Before returning hello connection brokered through data dependent routing, simply create and execute a SqlCommand that sets 'TenantId' in hello SESSION_CONTEXT toohello shardingKey specified for that connection.</span></span> <span data-ttu-id="32c77-144">如此一來，您只需要 toowrite 程式碼之後 tooset hello SESSION_CONTEXT。</span><span class="sxs-lookup"><span data-stu-id="32c77-144">This way, you only need toowrite code once tooset hello SESSION_CONTEXT.</span></span> 

```
// ElasticScaleContext.cs 
// ... 
// C'tor for data dependent routing. This call will open a validated connection routed toohello proper 
// shard by hello shard map manager. Note that hello base class c'tor call will fail for an open connection 
// if migrations need toobe done and SQL credentials are used. This is hello reason for hello  
// separation of c'tors into hello DDR case (this c'tor) and hello internal c'tor for new shards. 
public ElasticScaleContext(ShardMap shardMap, T shardingKey, string connectionStr)
    : base(OpenDDRConnection(shardMap, shardingKey, connectionStr), true /* contextOwnsConnection */)
{
}

public static SqlConnection OpenDDRConnection(ShardMap shardMap, T shardingKey, string connectionStr)
{
    // No initialization
    Database.SetInitializer<ElasticScaleContext<T>>(null);

    // Ask shard map toobroker a validated connection for hello given key
    SqlConnection conn = null;
    try
    {
        conn = shardMap.OpenConnectionForKey(shardingKey, connectionStr, ConnectionOptions.Validate);

        // Set TenantId in SESSION_CONTEXT tooshardingKey tooenable Row-Level Security filtering
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

<span data-ttu-id="32c77-145">現在使用自動設定 hello SESSION_CONTEXT hello ElasticScaleContext 叫用時，就會指定 TenantId:</span><span class="sxs-lookup"><span data-stu-id="32c77-145">Now hello SESSION_CONTEXT is automatically set with hello specified TenantId whenever ElasticScaleContext is invoked:</span></span> 

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

### <a name="adonet-sqlclient"></a><span data-ttu-id="32c77-146">ADO.NET SqlClient</span><span class="sxs-lookup"><span data-stu-id="32c77-146">ADO.NET SqlClient</span></span>
<span data-ttu-id="32c77-147">自動設定 'TenantId' hello SESSION_CONTEXT toohello ShardMap.OpenConnectionForKey() 周圍的包裝函數的應用程式使用 ADO.NET SqlClient hello 建議的作法是 toocreate 更正後再傳回 TenantId連接。</span><span class="sxs-lookup"><span data-stu-id="32c77-147">For applications using ADO.NET SqlClient, hello recommended approach is toocreate a wrapper function around ShardMap.OpenConnectionForKey() that automatically sets 'TenantId' in hello SESSION_CONTEXT toohello correct TenantId before returning a connection.</span></span> <span data-ttu-id="32c77-148">一定會設定 SESSION_CONTEXT 的 tooensure，您只應該開啟使用此包裝函式的函式的連線。</span><span class="sxs-lookup"><span data-stu-id="32c77-148">tooensure that SESSION_CONTEXT is always set, you should only open connections using this wrapper function.</span></span>

```
// Program.cs
// ...

// Wrapper function for ShardMap.OpenConnectionForKey() that automatically sets SESSION_CONTEXT with hello correct
// tenantId before returning a connection. As a best practice, you should only open connections using this 
// method tooensure that SESSION_CONTEXT is always set before executing a query.
public static SqlConnection OpenConnectionForTenant(ShardMap shardMap, int tenantId, string connectionStr)
{
    SqlConnection conn = null;
    try
    {
        // Ask shard map toobroker a validated connection for hello given key
        conn = shardMap.OpenConnectionForKey(tenantId, connectionStr, ConnectionOptions.Validate);

        // Set TenantId in SESSION_CONTEXT tooshardingKey tooenable Row-Level Security filtering
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

## <a name="step-2-data-tier-create-row-level-security-policy"></a><span data-ttu-id="32c77-149">步驟 2) 資料層：建立資料列層級的安全性原則</span><span class="sxs-lookup"><span data-stu-id="32c77-149">Step 2) Data tier: Create row-level security policy</span></span>
### <a name="create-a-security-policy-toofilter-hello-rows-each-tenant-can-access"></a><span data-ttu-id="32c77-150">建立安全性原則 toofilter hello 可以存取每個租用戶的資料列</span><span class="sxs-lookup"><span data-stu-id="32c77-150">Create a security policy toofilter hello rows each tenant can access</span></span>
<span data-ttu-id="32c77-151">既然 hello 應用程式設定 SESSION_CONTEXT 以 hello 目前 TenantId 查詢之前, 的 RLS 安全性原則篩選查詢以及排除具有不同的 TenantId 的資料列。</span><span class="sxs-lookup"><span data-stu-id="32c77-151">Now that hello application is setting SESSION_CONTEXT with hello current TenantId before querying, an RLS security policy can filter queries and exclude rows that have a different TenantId.</span></span>  

<span data-ttu-id="32c77-152">在 T-SQL 中實作 RLS： 使用者定義函式定義 hello 存取邏輯和安全性原則會將繫結資料表的這個函式 tooany 數字。</span><span class="sxs-lookup"><span data-stu-id="32c77-152">RLS is implemented in T-SQL: a user-defined function defines hello access logic, and a security policy binds this function tooany number of tables.</span></span> <span data-ttu-id="32c77-153">這個專案中，hello 函式只會驗證 hello 應用程式 （而非其他的 SQL 使用者） 是連接的 toohello 資料庫，則該 hello 'TenantId' 儲存在 hello SESSION_CONTEXT 符合指定之資料列的 TenantId hello。</span><span class="sxs-lookup"><span data-stu-id="32c77-153">For this project, hello function will simply verify that hello application (rather than some other SQL user) is connected toohello database, and that hello 'TenantId' stored in hello SESSION_CONTEXT matches hello TenantId of a given row.</span></span> <span data-ttu-id="32c77-154">篩選器述詞會允許符合這些條件 toopass 透過 SELECT、 UPDATE 及 DELETE 查詢; hello 篩選條件的資料列和 block 述詞會造成違反這些條件，插入或更新的資料列。</span><span class="sxs-lookup"><span data-stu-id="32c77-154">A filter predicate will allow rows that meet these conditions toopass through hello filter for SELECT, UPDATE, and DELETE queries; and a block predicate will prevent rows that violate these conditions from being INSERTed or UPDATEd.</span></span> <span data-ttu-id="32c77-155">如果尚未設定 SESSION_CONTEXT，它會傳回 NULL，而且沒有任何資料列將會是可見或無法 toobe 插入。</span><span class="sxs-lookup"><span data-stu-id="32c77-155">If SESSION_CONTEXT has not been set, it will return NULL and no rows will be visible or able toobe inserted.</span></span> 

<span data-ttu-id="32c77-156">tooenable RLS，執行下列 T-SQL 上使用其中一個 Visual Studio (SSDT)，SSMS 中的所有分區的 hello 或 hello hello 專案中包含的 PowerShell 指令碼 (或如果您使用[彈性資料庫工作](sql-database-elastic-jobs-overview.md)，您可以使用它 tooautomate 執行這個 T-SQL 的所有分區上）：</span><span class="sxs-lookup"><span data-stu-id="32c77-156">tooenable RLS, execute hello following T-SQL on all shards using either Visual Studio (SSDT), SSMS, or hello PowerShell script included in hello project (or if you are using [Elastic Database Jobs](sql-database-elastic-jobs-overview.md), you can use it tooautomate execution of this T-SQL on all shards):</span></span> 

```
CREATE SCHEMA rls -- separate schema tooorganize RLS objects 
GO

CREATE FUNCTION rls.fn_tenantAccessPredicate(@TenantId int)     
    RETURNS TABLE     
    WITH SCHEMABINDING
AS
    RETURN SELECT 1 AS fn_accessResult          
        WHERE DATABASE_PRINCIPAL_ID() = DATABASE_PRINCIPAL_ID('dbo') -- hello user in your application’s connection string (dbo is only for demo purposes!)         
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
> <span data-ttu-id="32c77-157">對於需要 tooadd hello 述詞，在數以百計的資料表上的複雜專案，您可以使用自動產生結構描述中的所有資料表上加入述詞的安全性原則的協助程式預存程序。</span><span class="sxs-lookup"><span data-stu-id="32c77-157">For more complex projects that need tooadd hello predicate on hundreds of tables, you can use a helper stored procedure that automatically generates a security policy adding a predicate on all tables in a schema.</span></span> <span data-ttu-id="32c77-158">請參閱[套用資料列層級安全性 tooall 資料表 helper 指令碼 （部落格）](http://blogs.msdn.com/b/sqlsecurity/archive/2015/03/31/apply-row-level-security-to-all-tables-helper-script)。</span><span class="sxs-lookup"><span data-stu-id="32c77-158">See [Apply Row-Level Security tooall tables - helper script (blog)](http://blogs.msdn.com/b/sqlsecurity/archive/2015/03/31/apply-row-level-security-to-all-tables-helper-script).</span></span>  
> 
> 

<span data-ttu-id="32c77-159">現在如果您執行一次 hello 範例應用程式時，租用戶將無法 toosee 屬於 toothem 唯一資料列。</span><span class="sxs-lookup"><span data-stu-id="32c77-159">Now if you run hello sample application again, tenants will able toosee only rows that belong toothem.</span></span> <span data-ttu-id="32c77-160">此外，hello 應用程式無法插入資料列屬於 tootenants 以外 hello 一個目前連接的 toohello 分區資料庫，而且它無法更新顯示的資料列 toohave 不同 TenantId。</span><span class="sxs-lookup"><span data-stu-id="32c77-160">In addition, hello application cannot insert rows that belong tootenants other than hello one currently connected toohello shard database, and it cannot update visible rows toohave a different TenantId.</span></span> <span data-ttu-id="32c77-161">如果 hello 應用程式可能是嘗試 toodo，就會引發 DbUpdateException。</span><span class="sxs-lookup"><span data-stu-id="32c77-161">If hello application attempts toodo either, a DbUpdateException will be raised.</span></span>

<span data-ttu-id="32c77-162">如果您在稍後加入新的資料表，只要是 ALTER hello 安全性原則和 hello 新的資料表上加入篩選器和區塊述詞：</span><span class="sxs-lookup"><span data-stu-id="32c77-162">If you add a new table later on, simply ALTER hello security policy and add filter and block predicates on hello new table:</span></span> 

```
ALTER SECURITY POLICY rls.tenantAccessPolicy     
    ADD FILTER PREDICATE rls.fn_tenantAccessPredicate(TenantId) ON dbo.MyNewTable,
    ADD BLOCK PREDICATE rls.fn_tenantAccessPredicate(TenantId) ON dbo.MyNewTable
GO 
```

### <a name="add-default-constraints-tooautomatically-populate-tenantid-for-inserts"></a><span data-ttu-id="32c77-163">新增預設條件約束 tooautomatically 填入插入的 TenantId</span><span class="sxs-lookup"><span data-stu-id="32c77-163">Add default constraints tooautomatically populate TenantId for INSERTs</span></span>
<span data-ttu-id="32c77-164">您可以將預設條件約束上每個資料表 tooautomatically 填入 hello 與 hello TenantId 值插入資料列時，目前儲存在 SESSION_CONTEXT。</span><span class="sxs-lookup"><span data-stu-id="32c77-164">You can put a default constraint on each table tooautomatically populate hello TenantId with hello value currently stored in SESSION_CONTEXT when inserting rows.</span></span> <span data-ttu-id="32c77-165">例如：</span><span class="sxs-lookup"><span data-stu-id="32c77-165">For example:</span></span> 

```
-- Create default constraints tooauto-populate TenantId with hello value of SESSION_CONTEXT for inserts 
ALTER TABLE Blogs     
    ADD CONSTRAINT df_TenantId_Blogs      
    DEFAULT CAST(SESSION_CONTEXT(N'TenantId') AS int) FOR TenantId 
GO

ALTER TABLE Posts     
    ADD CONSTRAINT df_TenantId_Posts      
    DEFAULT CAST(SESSION_CONTEXT(N'TenantId') AS int) FOR TenantId 
GO 
```

<span data-ttu-id="32c77-166">現在 hello 應用程式不需要 toospecify TenantId 插入資料列時：</span><span class="sxs-lookup"><span data-stu-id="32c77-166">Now hello application does not need toospecify a TenantId when inserting rows:</span></span> 

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
> <span data-ttu-id="32c77-167">如果您使用 Entity Framework 專案的預設條件約束，建議您不要在 EF 資料模型中包含 hello TenantId 資料行。</span><span class="sxs-lookup"><span data-stu-id="32c77-167">If you use default constraints for an Entity Framework project, it is recommended that you do NOT include hello TenantId column in your EF data model.</span></span> <span data-ttu-id="32c77-168">這是因為 Entity Framework 查詢自動提供預設值會覆寫 hello 預設條件約束建立 T-SQL 中，使用 SESSION_CONTEXT。</span><span class="sxs-lookup"><span data-stu-id="32c77-168">This is because Entity Framework queries automatically supply default values which will override hello default constraints created in T-SQL that use SESSION_CONTEXT.</span></span> <span data-ttu-id="32c77-169">hello toouse 預設條件約束的範例專案，比方說，您應該移除 TenantId DataClasses.cs （及 hello Package Manager Console 中的執行的新增移轉） 然後 hello 欄位的使用 T-SQL tooensure 僅存在於 hello 資料庫資料表。</span><span class="sxs-lookup"><span data-stu-id="32c77-169">toouse default constraints in hello sample project, for instance, you should remove TenantId from DataClasses.cs (and run Add-Migration in hello Package Manager Console) and use T-SQL tooensure that hello field only exists in hello database tables.</span></span> <span data-ttu-id="32c77-170">如此一來，EF 就不會在插入資料時，自動提供不正確的預設值。</span><span class="sxs-lookup"><span data-stu-id="32c77-170">This way, EF will not automatically supply incorrect default values when inserting data.</span></span> 
> 
> 

### <a name="optional-enable-a-superuser-tooaccess-all-rows"></a><span data-ttu-id="32c77-171">（選擇性）啟用 「 superuser"tooaccess 所有資料列</span><span class="sxs-lookup"><span data-stu-id="32c77-171">(Optional) Enable a "superuser" tooaccess all rows</span></span>
<span data-ttu-id="32c77-172">某些應用程式可能會想 toocreate"超級使用者 「 可以存取所有資料列，比方說，順序 tooenable 跨所有分區，在所有租用戶或牽涉到資料庫之間移動租用戶資料列的分區 tooperform 分割/合併作業報告。</span><span class="sxs-lookup"><span data-stu-id="32c77-172">Some applications may want toocreate a "superuser" who can access all rows, for instance, in order tooenable reporting across all tenants on all shards, or tooperform Split/Merge operations on shards that involve moving tenant rows between databases.</span></span> <span data-ttu-id="32c77-173">tooenable，您應該在每個分區化資料庫中建立新的 SQL 使用者 (在此範例中為"superuser")。</span><span class="sxs-lookup"><span data-stu-id="32c77-173">tooenable this, you should create a new SQL user ("superuser" in this example) in each shard database.</span></span> <span data-ttu-id="32c77-174">然後變更使用新的述詞函式，可讓此使用者 tooaccess 所有資料列的 hello 安全性原則：</span><span class="sxs-lookup"><span data-stu-id="32c77-174">Then alter hello security policy with a new predicate function that allows this user tooaccess all rows:</span></span>

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

-- Atomically swap in hello new predicate function on each table
ALTER SECURITY POLICY rls.tenantAccessPolicy
    ALTER FILTER PREDICATE rls.fn_tenantAccessPredicateWithSuperUser(TenantId) ON dbo.Blogs,
    ALTER BLOCK PREDICATE rls.fn_tenantAccessPredicateWithSuperUser(TenantId) ON dbo.Blogs,
    ALTER FILTER PREDICATE rls.fn_tenantAccessPredicateWithSuperUser(TenantId) ON dbo.Posts,
    ALTER BLOCK PREDICATE rls.fn_tenantAccessPredicateWithSuperUser(TenantId) ON dbo.Posts
GO
```


### <a name="maintenance"></a><span data-ttu-id="32c77-175">維護 </span><span class="sxs-lookup"><span data-stu-id="32c77-175">Maintenance</span></span>
* <span data-ttu-id="32c77-176">**加入新的分區**： 您必須在任何新的分區執行 hello T-SQL 指令碼 tooenable RLS，否則不會篩選這些分區的查詢。</span><span class="sxs-lookup"><span data-stu-id="32c77-176">**Adding new shards**: You must execute hello T-SQL script tooenable RLS on any new shards, otherwise queries on these shards will not be filtered.</span></span>
* <span data-ttu-id="32c77-177">**將新資料表加入**： 您必須新增篩選器，並封鎖述詞 toohello 安全性原則，在所有分區，每次建立新的資料表，否則不會篩選 hello 新的資料表上的查詢。</span><span class="sxs-lookup"><span data-stu-id="32c77-177">**Adding new tables**: You must add a filter and block predicate toohello security policy on all shards whenever a new table is created, otherwise queries on hello new table will not be filtered.</span></span> <span data-ttu-id="32c77-178">這可以使用自動化 DDL 觸發程序中所述[套用資料列層級安全性自動 toonewly 建立資料表 （部落格）](http://blogs.msdn.com/b/sqlsecurity/archive/2015/05/22/apply-row-level-security-automatically-to-newly-created-tables.aspx)。</span><span class="sxs-lookup"><span data-stu-id="32c77-178">This can be automated using a DDL trigger, as described in [Apply Row-Level Security automatically toonewly created tables (blog)](http://blogs.msdn.com/b/sqlsecurity/archive/2015/05/22/apply-row-level-security-automatically-to-newly-created-tables.aspx).</span></span>

## <a name="summary"></a><span data-ttu-id="32c77-179">摘要</span><span class="sxs-lookup"><span data-stu-id="32c77-179">Summary</span></span>
<span data-ttu-id="32c77-180">彈性資料庫工具和資料列層級安全性可使用的一起 tooscale 該層應用程式的資料，可以支援多租用戶和單一租用戶的分區。</span><span class="sxs-lookup"><span data-stu-id="32c77-180">Elastic database tools and row-level security can be used together tooscale out an application’s data tier with support for both multi-tenant and single-tenant shards.</span></span> <span data-ttu-id="32c77-181">多租用戶分區可以是使用的 toostore 資料更有效率 （特別是在情況中大量的租用戶有只有少數資料列的資料），在單一租用戶時可以使用的 toosupport premium 租用戶，提供更嚴格的效能和隔離分區。需求。</span><span class="sxs-lookup"><span data-stu-id="32c77-181">Multi-tenant shards can be used toostore data more efficiently (particularly in cases where a large number of tenants have only a few rows of data), while single-tenant shards can be used toosupport premium tenants with stricter performance and isolation requirements.</span></span>  <span data-ttu-id="32c77-182">如需詳細資訊，請參閱 [資料列層級安全性參考資料](https://msdn.microsoft.com/library/dn765131)。</span><span class="sxs-lookup"><span data-stu-id="32c77-182">For more information, see [Row-Level Security reference](https://msdn.microsoft.com/library/dn765131).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="32c77-183">其他資源</span><span class="sxs-lookup"><span data-stu-id="32c77-183">Additional resources</span></span>
* [<span data-ttu-id="32c77-184">什麼是 Azure 彈性集區？</span><span class="sxs-lookup"><span data-stu-id="32c77-184">What is an Azure elastic pool?</span></span>](sql-database-elastic-pool.md)
* [<span data-ttu-id="32c77-185">使用 Azure SQL Database 相應放大</span><span class="sxs-lookup"><span data-stu-id="32c77-185">Scaling out with Azure SQL Database</span></span>](sql-database-elastic-scale-introduction.md)
* [<span data-ttu-id="32c77-186">多租用戶 SaaS 應用程式與 Azure SQL Database 的設計模式</span><span class="sxs-lookup"><span data-stu-id="32c77-186">Design Patterns for Multi-tenant SaaS Applications with Azure SQL Database</span></span>](sql-database-design-patterns-multi-tenancy-saas-applications.md)
* [<span data-ttu-id="32c77-187">使用 Azure AD 和 OpenID Connect 的多租用戶應用程式驗證</span><span class="sxs-lookup"><span data-stu-id="32c77-187">Authentication in multitenant apps, using Azure AD and OpenID Connect</span></span>](../guidance/guidance-multitenant-identity-authenticate.md)
* [<span data-ttu-id="32c77-188">Tailspin Surveys 應用程式</span><span class="sxs-lookup"><span data-stu-id="32c77-188">Tailspin Surveys application</span></span>](../guidance/guidance-multitenant-identity-tailspin.md)

## <a name="questions-and-feature-requests"></a><span data-ttu-id="32c77-189">問題和功能要求</span><span class="sxs-lookup"><span data-stu-id="32c77-189">Questions and Feature Requests</span></span>
<span data-ttu-id="32c77-190">如有問題，請聯繫 toous 上 hello [SQL Database 論壇](http://social.msdn.microsoft.com/forums/azure/home?forum=ssdsgetstarted)和功能的要求，請將它們加入 toohello [SQL Database 意見反應論壇](https://feedback.azure.com/forums/217321-sql-database/)。</span><span class="sxs-lookup"><span data-stu-id="32c77-190">For questions, please reach out toous on hello [SQL Database forum](http://social.msdn.microsoft.com/forums/azure/home?forum=ssdsgetstarted) and for feature requests, please add them toohello [SQL Database feedback forum](https://feedback.azure.com/forums/217321-sql-database/).</span></span>

<!--Image references-->
[1]: ./media/sql-database-elastic-tools-multi-tenant-row-level-security/blogging-app.png
<!--anchors-->


