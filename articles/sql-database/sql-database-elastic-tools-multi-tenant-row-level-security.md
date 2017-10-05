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
# <a name="multi-tenant-applications-with-elastic-database-tools-and-row-level-security"></a>使用彈性資料庫工具和資料列層級安全性的多租用戶應用程式
[彈性資料庫工具](sql-database-elastic-scale-get-started.md)和[資料列層級安全性 (RLS) ](https://msdn.microsoft.com/library/dn765131)提供一組強大的功能，能以具彈性且有效率的方式，透過 Azure SQL Database 調整多租用戶應用程式的資料層。 如需詳細資訊，請參閱 [多租用戶 SaaS 應用程式與 Azure SQL Database 的設計模式](sql-database-design-patterns-multi-tenancy-saas-applications.md) 。 

本文說明如何運用這些技術，透過 **ADO.NET SqlClient** 和/或 **Entity Framework** 建置應用程式，且讓此應用程式具有可支援多租用戶分區的高度可擴充資料層。  

*  彈性資料庫工具可讓開發人員藉由使用 .NET 程式庫和 Azure 服務範本的一套業界標準分區化作法，向外延展應用程式的資料層。 使用「彈性資料庫用戶端程式庫」管理分區，有助於自動化及簡化許多通常與分區化相關的基礎結構工作。 
* **資料列層級安全性** 可讓開發人員使用安全性原則來篩選掉一些資料列 (這些資料列不屬於執行查詢的租用戶)，藉此在同一個資料庫中儲存多個租用戶的資料。 在資料庫內 (而不是在應用程式內) 集中存取邏輯與 RLS，可簡化維護流程並降低發生錯誤的風險 (因為應用程式的程式碼基底會成長)。 

搭配使用這些功能時，由於在同一個分區資料庫中儲存多租用戶的資料可節省成本並提高效率，進而使應用程式受益。 在此同時，應用程式仍會為「高階」租用戶彈性地提供隔離的單一租用戶分區，因為這些租用戶需要更嚴格的效能保證，畢竟多租用戶分區並不保證能在租用戶間平均分配資源。  

簡單地說，彈性資料庫用戶端程式庫的 [資料依存路由](sql-database-elastic-scale-data-dependent-routing.md) API 會自動將租用戶連接到正確的分區資料庫，這些資料庫含有他們的分區化索引鍵 (通常為 "TenantId")。 一旦連接之後，在資料庫內的 RLS 安全性原則可確保租用戶只能存取含有其 TenantId 的資料列。 此原則會假設所有資料表都包含一個會指出哪些資料列屬於哪個租用戶的 TenantId 資料行。 

![部落格應用程式架構][1]

## <a name="download-the-sample-project"></a>下載範例專案
### <a name="prerequisites"></a>必要條件
* 使用 Visual Studio (2012 或更新版本) 
* 建立三個 Azure SQL Database 
* 下載範例專案： [Azure SQL 的彈性資料庫工具：多租用戶分區](http://go.microsoft.com/?linkid=9888163)
  * 在 **Program.cs** 

此專案會新增對多租用戶分區資料庫的支援，藉此擴充 [Azure SQL 的彈性資料庫工具：Entity Framework 整合](sql-database-elastic-scale-use-entity-framework-applications-visual-studio.md) 中所述的項目。 如上圖所示，這麼做可以建立具有四個租用戶與兩個多租用戶分區資料庫的簡單主控台應用程式，以用於建立部落格和文章。 

建置並執行應用程式。 這會啟動彈性資料庫工具的分區對應管理員，並執行下列測試： 

1. 使用 Entity Framework 和 LINQ，建立新的部落格，然後顯示每個租用戶的所有部落格
2. 使用 ADO.NET SqlClient，顯示某個租用戶的所有部落格
3. 嘗試插入錯誤的租用戶部落格，以確認是否擲回錯誤  

請注意，因為分區資料庫中尚未啟用 RLS，所以這些測試都會顯現出一個問題：租用戶能夠查看不屬於自己的部落格，且應用程式無法阻止插入錯誤的租用戶部落格。 本文的其餘部分會說明，如何藉由 RLS 強制執行租用戶隔離來解決這些問題。 有兩個步驟： 

1. **應用程式層**：修改應用程式程式碼，以便在開啟連線之後一律設定 SESSION_CONTEXT 中目前的 TenantId。 範例專案已經完成此步驟。 
2. **資料層**：在每個分區資料庫中建立 RLS 安全性原則，以便根據儲存在 SESSION_CONTEXT 中的 TenantId 來篩選資料列。 您需要對每個分區資料庫執行這個動作，否則將不會篩選多租用戶分區中的資料列。 

## <a name="step-1-application-tier-set-tenantid-in-the-sessioncontext"></a>步驟 1) 應用程式層：設定 SESSION_CONTEXT 中的 TenantId
在使用彈性資料庫用戶端程式庫的資料依存路由 API 連接到分區資料庫後，應用程式仍需告訴資料庫哪個 TenantId 使用該連接，然後 RLS 安全性原則才能篩選掉屬於其他租用戶的資料列。 我們建議您傳遞此資訊的方式，是在 [SESSION_CONTEXT](https://msdn.microsoft.com/library/mt590806.aspx) 中儲存該連線目前的 TenantId。 (注意：您也可以使用 [CONTEXT_INFO](https://msdn.microsoft.com/library/ms180125.aspx)，但 SESSION_CONTEXT 是比較理想的選項，因為它容易使用、預設會傳回 NULL，而且支援索引鍵-值組。)

### <a name="entity-framework"></a>Entity Framework
對於使用 Entity Framework 的應用程式，最簡單的方法是在[使用 EF DbContext 的資料相依路由](sql-database-elastic-scale-use-entity-framework-applications-visual-studio.md#data-dependent-routing-using-ef-dbcontext)一文中所述的 ElasticScaleContext 覆寫中設定 SESSION_CONTEXT。 在傳回透過資料相依路由來代理的連線之前，只要建立並執行 SqlCommand，來將 SESSION_CONTEXT 中的「TenantId」設定為該連線專用的 shardingKey 即可。 如此一來，您只需要編寫程式碼一次，就能設定 SESSION_CONTEXT。 

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

現在，每次叫用 ElasticScaleContext 時，就會使用指定的 TenantId 來自動設定 SESSION_CONTEXT： 

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

### <a name="adonet-sqlclient"></a>ADO.NET SqlClient
針對使用 ADO.NET SqlClient 的應用程式，我們建議您在 ShardMap.OpenConnectionForKey() 周圍建立包裝函式，以便在傳回連線之前自動把 SESSION_CONTEXT 中的「TenantId」設定為正確的 TenantId。 如要確保 SESSION_CONTEXT 一定是設定好的，請務必只使用此包裝函式來開啟連線。

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

## <a name="step-2-data-tier-create-row-level-security-policy"></a>步驟 2) 資料層：建立資料列層級的安全性原則
### <a name="create-a-security-policy-to-filter-the-rows-each-tenant-can-access"></a>建立安全性原則來篩選每個租用戶可以存取的資料列
現在應用程式會在查詢之前，使用目前的 TenantId 來設定 SESSION_CONTEXT，RLS 安全性原則也會篩選查詢，並排除有不同 TenantId 的資料列。  

RLS 已在 T-SQL 中實作 ：使用者定義的函數會定義存取邏輯，而安全性原則會將此函數繫結至任何數目的資料表。 就此專案而言，函數只會確認該應用程式 (而非其他的 SQL 使用者) 是否連線至資料庫，且儲存在 SESSION_CONTEXT 中的「TenantId」是否符合特定資料列的 TenantId。 篩選述詞可讓符合這些條件的資料列通過 SELECT、UPDATE 和 DELETE 查詢的篩選；而封鎖述詞會避免違反這些條件的資料列進行 INSERT 或 UPDATE。 如果尚未設定 SESSION_CONTEXT，它會傳回 NULL，而且看不見或無法插入任何資料列。 

若要啟用 RLS，可以使用 Visual Studio (SSDT)、SSMS 或包含在專案中的 PowerShell 指令碼，在所有分區上執行以下 T-SQL (或者，如果您使用 [彈性資料庫工作](sql-database-elastic-jobs-overview.md)，您可以用它在所有分區上自動執行此 T-SQL)： 

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
> 如果是更複雜的專案 (需要在數百個資料表上加入述詞)，您可以使用協助程式預存程序來自動產生安全性原則，藉此為結構描述中的所有資料表加入述詞。 請參閱[將資料列層級安全性套用至所有資料表 - 協助程式指令碼 (英文) (部落格)](http://blogs.msdn.com/b/sqlsecurity/archive/2015/03/31/apply-row-level-security-to-all-tables-helper-script)。  
> 
> 

現在，如果您再次執行範例應用程式，租用戶將只能看到屬於自己的資料列。 此外，應用程式無法插入目前沒有連線到分區資料庫的租用戶所屬的資料列，也無法更新擁有不同 TenantId 的可見資料列。 如果應用程式嘗試執行這兩項作業，就會引發 DbUpdateException。

如果您是在之後加入新的資料表，您只要「變更」安全性原則，並在新的資料表上加入篩選和封鎖述詞即可： 

```
ALTER SECURITY POLICY rls.tenantAccessPolicy     
    ADD FILTER PREDICATE rls.fn_tenantAccessPredicate(TenantId) ON dbo.MyNewTable,
    ADD BLOCK PREDICATE rls.fn_tenantAccessPredicate(TenantId) ON dbo.MyNewTable
GO 
```

### <a name="add-default-constraints-to-automatically-populate-tenantid-for-inserts"></a>加入預設條件約束來為插入自動填入 TenantId
您可以在每個資料表上放置預設條件約束，以在插入資料列時，以 SESSION_CONTEXT 中目前儲存的值自動填入 TenantId。 例如： 

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

現在應用程式不需要在插入資料列時指定 TenantId： 

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
> 如果您需要針對 Entity Framework 專案使用預設條件約束，建議您「不要」在 EF 資料模型中包含 TenantId 資料行。 這是因為 Entity Framework 查詢會自動提供預設值，來覆寫 T-SQL 中使用 SESSION_CONTEXT 建立的預設條件約束。 若要使用範例專案中的預設條件約束，舉例來說，您可以從 DataClasses.cs 移除 TenantId (並在 Package Manager Console 中執行 Add-Migration)，然後使用 T-SQL 確保欄位只存在於資料庫資料表中。 如此一來，EF 就不會在插入資料時，自動提供不正確的預設值。 
> 
> 

### <a name="optional-enable-a-superuser-to-access-all-rows"></a>(選擇性) 啟用「進階使用者」來存取所有資料列
有些應用程式可能需要建立一個能夠存取所有資料列的「進階使用者」，比方說，為了跨所有分區上的所有租用戶來產生報告，或在牽涉到資料庫之間移動租用戶資料列的分區上執行分割/合併作業。 為了達成此目的，您應該在每個分區資料庫中建立新的 SQL 使用者 (在本例中為 "superuser")。 然後使用新的述詞函式修改安全性原則，允許此使用者存取所有資料列：

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


### <a name="maintenance"></a>維護
* **新增分區**：您必須執行 T-SQL 指令碼來啟用所有新分區上的 RLS，否則系統不會篩選這些分區的查詢。
* **新增資料表**：您必須在每次有新的資料表建立時，將篩選和封鎖述詞新增到所有分區的安全性原則，否則系統將不會篩選針對新資料表的查詢。 如 [自動將資料列層級安全性套用至新建立的資料表 (部落格)](http://blogs.msdn.com/b/sqlsecurity/archive/2015/05/22/apply-row-level-security-automatically-to-newly-created-tables.aspx)中所述，這部分可以使用 DDL 觸發程序來自動執行。

## <a name="summary"></a>摘要
您可以將彈性資料庫工具與資料列層級安全性搭配使用，以支援多租用戶和單一租用戶的分區，藉此向外延展應用程式的資料層。 多租用戶分區可以用來更有效率地儲存資料 (特別是在有大量租用戶，卻只有些許資料列的情況)，而單一租用戶分區則可以用來支援高階租用戶，因為這類租用戶有更嚴格的效能和隔離需求。  如需詳細資訊，請參閱 [資料列層級安全性參考資料](https://msdn.microsoft.com/library/dn765131)。 

## <a name="additional-resources"></a>其他資源
* [什麼是 Azure 彈性集區？](sql-database-elastic-pool.md)
* [使用 Azure SQL Database 相應放大](sql-database-elastic-scale-introduction.md)
* [多租用戶 SaaS 應用程式與 Azure SQL Database 的設計模式](sql-database-design-patterns-multi-tenancy-saas-applications.md)
* [使用 Azure AD 和 OpenID Connect 的多租用戶應用程式驗證](../guidance/guidance-multitenant-identity-authenticate.md)
* [Tailspin Surveys 應用程式](../guidance/guidance-multitenant-identity-tailspin.md)

## <a name="questions-and-feature-requests"></a>問題和功能要求
如有問題，請透過 [SQL Database 論壇](http://social.msdn.microsoft.com/forums/azure/home?forum=ssdsgetstarted)與我們連絡，如需要求增加功能，請將這些功能新增至 [SQL Database 意見反應論壇](https://feedback.azure.com/forums/217321-sql-database/)。

<!--Image references-->
[1]: ./media/sql-database-elastic-tools-multi-tenant-row-level-security/blogging-app.png
<!--anchors-->


