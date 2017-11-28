---
title: "教學課程：使用 Entity Framework 和資料列層級安全性的 Web 應用程式搭配多租用戶資料庫"
description: "了解如何 toodevelop ASP.NET MVC 5 web 應用程式與 SQL Database backent，使用 Entity Framework 和資料列層級安全性的多租用戶。"
metakeywords: azure asp.net mvc entity framework multi tenant row level security rls sql database
services: app-service\web
documentationcenter: .net
manager: jeffreyg
author: tmullaney
ms.assetid: 8fdc47a5-6fc3-4d29-ab6a-33e79f50699f
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 04/25/2016
ms.author: thmullan
ms.openlocfilehash: 1b715e01807032c3f6497c374ce427dd762af141
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-web-app-with-a-multi-tenant-database-using-entity-framework-and-row-level-security"></a><span data-ttu-id="a49ea-103">教學課程：使用 Entity Framework 和資料列層級安全性的 Web 應用程式搭配多租用戶資料庫</span><span class="sxs-lookup"><span data-stu-id="a49ea-103">Tutorial: Web app with a multi-tenant database using Entity Framework and Row-Level Security</span></span>
<span data-ttu-id="a49ea-104">本教學課程示範如何 toobuild 多租用戶 web 應用程式與 「[共用的資料庫、 共用的結構描述](https://msdn.microsoft.com/library/aa479086.aspx)"租用戶模型，使用 Entity Framework 和[資料列層級安全性](https://msdn.microsoft.com/library/dn765131.aspx)。</span><span class="sxs-lookup"><span data-stu-id="a49ea-104">This tutorial shows how toobuild a multi-tenant web app with a "[shared database, shared schema](https://msdn.microsoft.com/library/aa479086.aspx)" tenancy model, using Entity Framework and [Row-Level Security](https://msdn.microsoft.com/library/dn765131.aspx).</span></span> <span data-ttu-id="a49ea-105">在此模型中，單一資料庫包含許多租用戶的資料，而且每個資料表中的每個資料列都有一個相關聯的「租用戶識別碼」。</span><span class="sxs-lookup"><span data-stu-id="a49ea-105">In this model, a single database contains data for many tenants, and each row in each table is associated with a "Tenant ID."</span></span> <span data-ttu-id="a49ea-106">資料列層級安全性 (RLS)，Azure SQL Database 的新功能是使用的 tooprevent 租用戶存取彼此的資料。</span><span class="sxs-lookup"><span data-stu-id="a49ea-106">Row-Level Security (RLS), a new feature for Azure SQL Database, is used tooprevent tenants from accessing each other's data.</span></span> <span data-ttu-id="a49ea-107">這需要只是單一，小幅變更 toohello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="a49ea-107">This requires just a single, small change toohello application.</span></span> <span data-ttu-id="a49ea-108">根據集中 hello 租用戶存取邏輯 hello 資料庫本身內，RLS 簡化 hello 應用程式程式碼，並減少 hello 的租用戶之間的資料不慎外洩的風險。</span><span class="sxs-lookup"><span data-stu-id="a49ea-108">By centralizing hello tenant access logic within hello database itself, RLS simplifies hello application code and reduces hello risk of accidental data leakage between tenants.</span></span>

<span data-ttu-id="a49ea-109">讓我們開始 hello 簡單連絡人管理員應用程式中使用[驗證與 SQL 資料庫建立 ASP.NET MVP 應用程式和部署 tooAzure App Service](web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database.md)。</span><span class="sxs-lookup"><span data-stu-id="a49ea-109">Let's start with hello simple Contact Manager application from [Create an ASP.NET MVP app with auth and SQL DB and deploy tooAzure App Service](web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database.md).</span></span> <span data-ttu-id="a49ea-110">權限，hello 應用程式允許所有使用者 （租用戶） toosee 所有連絡人：</span><span class="sxs-lookup"><span data-stu-id="a49ea-110">Right now, hello application allows all users (tenants) toosee all contacts:</span></span>

![啟用 RLS 之前的連絡人管理員應用程式](./media/web-sites-dotnet-entity-framework-row-level-security/ContactManagerApp-Before.png)

<span data-ttu-id="a49ea-112">有幾個小變更，我們將支援多租用戶，讓使用者能夠 toosee 只有 hello 連絡人隸屬 toothem。</span><span class="sxs-lookup"><span data-stu-id="a49ea-112">With just a few small changes, we will add support for multi-tenancy, so that users are able toosee only hello contacts that belong toothem.</span></span>

## <a name="step-1-add-an-interceptor-class-in-hello-application-tooset-hello-sessioncontext"></a><span data-ttu-id="a49ea-113">步驟 1： 加入在 hello 應用程式 tooset hello SESSION_CONTEXT 攔截器類別</span><span class="sxs-lookup"><span data-stu-id="a49ea-113">Step 1: Add an Interceptor class in hello application tooset hello SESSION_CONTEXT</span></span>
<span data-ttu-id="a49ea-114">沒有一個應用程式變更，我們需要 toomake。</span><span class="sxs-lookup"><span data-stu-id="a49ea-114">There is one application change we need toomake.</span></span> <span data-ttu-id="a49ea-115">因為所有的應用程式使用者連線 toohello 資料庫使用 hello 相同的連接字串 （也就是相同的 SQL 登入），目前沒有任何 RLS 原則 tooknow 它應該篩選使用者的方式。</span><span class="sxs-lookup"><span data-stu-id="a49ea-115">Because all application users connect toohello database using hello same connection string (i.e. same SQL login), there is currently no way for an RLS policy tooknow which user it should filter for.</span></span> <span data-ttu-id="a49ea-116">這個方法是在 web 應用程式中很常見，因為它可讓有效率的連接共用，但這表示我們需要另一個方式 tooidentify hello 目前應用程式的使用者 hello 資料庫內。</span><span class="sxs-lookup"><span data-stu-id="a49ea-116">This approach is very common in web applications because it enables efficient connection pooling, but it means we need another way tooidentify hello current application user within hello database.</span></span> <span data-ttu-id="a49ea-117">hello 解決方案是 toohave hello 應用程式集的索引鍵-值組 hello hello 中目前的使用者識別碼[SESSION_CONTEXT](https://msdn.microsoft.com/library/mt590806)之後立即開啟連接，之前它會執行任何查詢。</span><span class="sxs-lookup"><span data-stu-id="a49ea-117">hello solution is toohave hello application set a key-value pair for hello current UserId in hello [SESSION_CONTEXT](https://msdn.microsoft.com/library/mt590806) immediately after opening a connection, before it executes any queries.</span></span> <span data-ttu-id="a49ea-118">SESSION_CONTEXT 是工作階段範圍索引鍵-值存放區，且我們 RLS 原則將會使用使用者識別碼儲存在它的 hello tooidentify hello 目前的使用者。</span><span class="sxs-lookup"><span data-stu-id="a49ea-118">SESSION_CONTEXT is a session-scoped key-value store, and our RLS policy will use hello UserId stored in it tooidentify hello current user.</span></span>

<span data-ttu-id="a49ea-119">我們將會加入[攔截器](https://msdn.microsoft.com/data/dn469464.aspx)(特別是， [DbConnectionInterceptor](https://msdn.microsoft.com/library/system.data.entity.infrastructure.interception.idbconnectioninterceptor))，在 Entity Framework (EF) 6，tooautomatically 組的新功能藉由執行 hello hello SESSION_CONTEXT 中目前的使用者識別碼T-SQL 陳述式時 EF 開啟的連接。</span><span class="sxs-lookup"><span data-stu-id="a49ea-119">We will add an [interceptor](https://msdn.microsoft.com/data/dn469464.aspx) (in particular, a [DbConnectionInterceptor](https://msdn.microsoft.com/library/system.data.entity.infrastructure.interception.idbconnectioninterceptor)), a new feature in Entity Framework (EF) 6, tooautomatically set hello current UserId in hello SESSION_CONTEXT by executing a T-SQL statement whenever EF opens a connection.</span></span>

1. <span data-ttu-id="a49ea-120">開啟 Visual Studio 中的 hello ContactManager 專案。</span><span class="sxs-lookup"><span data-stu-id="a49ea-120">Open hello ContactManager project in Visual Studio.</span></span>
2. <span data-ttu-id="a49ea-121">Hello 方案總管] 中的 hello Models 資料夾上按一下滑鼠右鍵，然後選擇 [加入 > 類別。</span><span class="sxs-lookup"><span data-stu-id="a49ea-121">Right-click on hello Models folder in hello Solution Explorer, and choose Add > Class.</span></span>
3. <span data-ttu-id="a49ea-122">Hello 新類別命名為"SessionContextInterceptor.cs 」，並按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="a49ea-122">Name hello new class "SessionContextInterceptor.cs" and click Add.</span></span>
4. <span data-ttu-id="a49ea-123">取代下列程式碼的 hello SessionContextInterceptor.cs hello 內容。</span><span class="sxs-lookup"><span data-stu-id="a49ea-123">Replace hello contents of SessionContextInterceptor.cs with hello following code.</span></span>

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Web;
using System.Data.Common;
using System.Data.Entity;
using System.Data.Entity.Infrastructure.Interception;
using Microsoft.AspNet.Identity;

namespace ContactManager.Models
{
    public class SessionContextInterceptor : IDbConnectionInterceptor
    {
        public void Opened(DbConnection connection, DbConnectionInterceptionContext interceptionContext)
        {
            // Set SESSION_CONTEXT toocurrent UserId whenever EF opens a connection
            try
            {
                var userId = System.Web.HttpContext.Current.User.Identity.GetUserId();
                if (userId != null)
                {
                    DbCommand cmd = connection.CreateCommand();
                    cmd.CommandText = "EXEC sp_set_session_context @key=N'UserId', @value=@UserId";
                    DbParameter param = cmd.CreateParameter();
                    param.ParameterName = "@UserId";
                    param.Value = userId;
                    cmd.Parameters.Add(param);
                    cmd.ExecuteNonQuery();
                }
            }
            catch (System.NullReferenceException)
            {
                // If no user is logged in, leave SESSION_CONTEXT null (all rows will be filtered)
            }
        }

        public void Opening(DbConnection connection, DbConnectionInterceptionContext interceptionContext)
        {
        }

        public void BeganTransaction(DbConnection connection, BeginTransactionInterceptionContext interceptionContext)
        {
        }

        public void BeginningTransaction(DbConnection connection, BeginTransactionInterceptionContext interceptionContext)
        {
        }

        public void Closed(DbConnection connection, DbConnectionInterceptionContext interceptionContext)
        {
        }

        public void Closing(DbConnection connection, DbConnectionInterceptionContext interceptionContext)
        {
        }

        public void ConnectionStringGetting(DbConnection connection, DbConnectionInterceptionContext<string> interceptionContext)
        {
        }

        public void ConnectionStringGot(DbConnection connection, DbConnectionInterceptionContext<string> interceptionContext)
        {
        }

        public void ConnectionStringSet(DbConnection connection, DbConnectionPropertyInterceptionContext<string> interceptionContext)
        {
        }

        public void ConnectionStringSetting(DbConnection connection, DbConnectionPropertyInterceptionContext<string> interceptionContext)
        {
        }

        public void ConnectionTimeoutGetting(DbConnection connection, DbConnectionInterceptionContext<int> interceptionContext)
        {
        }

        public void ConnectionTimeoutGot(DbConnection connection, DbConnectionInterceptionContext<int> interceptionContext)
        {
        }

        public void DataSourceGetting(DbConnection connection, DbConnectionInterceptionContext<string> interceptionContext)
        {
        }

        public void DataSourceGot(DbConnection connection, DbConnectionInterceptionContext<string> interceptionContext)
        {
        }

        public void DatabaseGetting(DbConnection connection, DbConnectionInterceptionContext<string> interceptionContext)
        {
        }

        public void DatabaseGot(DbConnection connection, DbConnectionInterceptionContext<string> interceptionContext)
        {
        }

        public void Disposed(DbConnection connection, DbConnectionInterceptionContext interceptionContext)
        {
        }

        public void Disposing(DbConnection connection, DbConnectionInterceptionContext interceptionContext)
        {
        }

        public void EnlistedTransaction(DbConnection connection, EnlistTransactionInterceptionContext interceptionContext)
        {
        }

        public void EnlistingTransaction(DbConnection connection, EnlistTransactionInterceptionContext interceptionContext)
        {
        }

        public void ServerVersionGetting(DbConnection connection, DbConnectionInterceptionContext<string> interceptionContext)
        {
        }

        public void ServerVersionGot(DbConnection connection, DbConnectionInterceptionContext<string> interceptionContext)
        {
        }

        public void StateGetting(DbConnection connection, DbConnectionInterceptionContext<System.Data.ConnectionState> interceptionContext)
        {
        }

        public void StateGot(DbConnection connection, DbConnectionInterceptionContext<System.Data.ConnectionState> interceptionContext)
        {
        }
    }

    public class SessionContextConfiguration : DbConfiguration
    {
        public SessionContextConfiguration()
        {
            AddInterceptor(new SessionContextInterceptor());
        }
    }
}
```

<span data-ttu-id="a49ea-124">這是所需的 hello 唯一的應用程式變更。</span><span class="sxs-lookup"><span data-stu-id="a49ea-124">That's hello only application change required.</span></span> <span data-ttu-id="a49ea-125">請繼續進行建置和發佈 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="a49ea-125">Go ahead and build and publish hello application.</span></span>

## <a name="step-2-add-a-userid-column-toohello-database-schema"></a><span data-ttu-id="a49ea-126">步驟 2： 新增的使用者識別碼資料行 toohello 資料庫結構描述</span><span class="sxs-lookup"><span data-stu-id="a49ea-126">Step 2: Add a UserId column toohello database schema</span></span>
<span data-ttu-id="a49ea-127">接下來，我們需要使用者識別碼資料行 toohello 連絡人資料表 tooassociate tooadd 每個資料列與使用者 （租用戶）。</span><span class="sxs-lookup"><span data-stu-id="a49ea-127">Next, we need tooadd a UserId column toohello Contacts table tooassociate each row with a user (tenant).</span></span> <span data-ttu-id="a49ea-128">我們將直接在 hello 資料庫中的 hello 結構描述變更我們沒有 tooinclude 此欄位在我們的 EF 資料模型。</span><span class="sxs-lookup"><span data-stu-id="a49ea-128">We will alter hello schema directly in hello database, so that we don't have tooinclude this field in our EF data model.</span></span>

<span data-ttu-id="a49ea-129">Toohello 資料庫直接連線，使用 SQL Server Management Studio 或 Visual Studio 中，並接著執行下列 T-SQL hello:</span><span class="sxs-lookup"><span data-stu-id="a49ea-129">Connect toohello database directly, using either SQL Server Management Studio or Visual Studio, and then execute hello following T-SQL:</span></span>

```
ALTER TABLE Contacts ADD UserId nvarchar(128)
    DEFAULT CAST(SESSION_CONTEXT(N'UserId') AS nvarchar(128))
```

<span data-ttu-id="a49ea-130">這會將 「 使用者識別碼資料行 toohello 連絡人 」 資料表。</span><span class="sxs-lookup"><span data-stu-id="a49ea-130">This adds a UserId column toohello Contacts table.</span></span> <span data-ttu-id="a49ea-131">我們使用 hello nvarchar （128) 資料型別 toomatch hello hello AspNetUsers 資料表中儲存的使用者 Id，我們會建立預設條件約束，將會自動設定新插入的資料列 toobe hello 目前儲存在 SESSION_CONTEXT 中的使用者識別碼的使用者識別碼 hello。</span><span class="sxs-lookup"><span data-stu-id="a49ea-131">We use hello nvarchar(128) data type toomatch hello UserIds stored in hello AspNetUsers table, and we create a DEFAULT constraint that will automatically set hello UserId for newly inserted rows toobe hello UserId currently stored in SESSION_CONTEXT.</span></span>

<span data-ttu-id="a49ea-132">現在 hello 資料表看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="a49ea-132">Now hello table looks like this:</span></span>

![SSMS Contacts 資料表](./media/web-sites-dotnet-entity-framework-row-level-security/SSMS-Contacts.png)

<span data-ttu-id="a49ea-134">新的連絡人建立時，它們會自動指派給 hello 更正使用者識別碼。</span><span class="sxs-lookup"><span data-stu-id="a49ea-134">When new contacts are created, they'll automatically be assigned hello correct UserId.</span></span> <span data-ttu-id="a49ea-135">基於示範目的，不過，讓我們來指派這些現有使用者的現有連絡人 tooan 一些。</span><span class="sxs-lookup"><span data-stu-id="a49ea-135">For demo purposes, however, let's assign a few of these existing contacts tooan existing user.</span></span>

<span data-ttu-id="a49ea-136">如果您已在 hello 應用程式已經建立少數使用者 (例如，使用本機、 Google 或 Facebook 帳戶)，就可以看到它們 hello AspNetUsers 資料表中。</span><span class="sxs-lookup"><span data-stu-id="a49ea-136">If you've created a few users in hello application already (e.g., using local, Google, or Facebook accounts), you'll see them in hello AspNetUsers table.</span></span> <span data-ttu-id="a49ea-137">在 hello 以下螢幕擷取畫面，則只有一位使用者為止。</span><span class="sxs-lookup"><span data-stu-id="a49ea-137">In hello screenshot below, there is only one user so far.</span></span>

![SSMS AspNetUsers 資料表](./media/web-sites-dotnet-entity-framework-row-level-security/SSMS-AspNetUsers.png)

<span data-ttu-id="a49ea-139">複製 hello 識別碼的user1@contoso.com，並將它貼到下列 hello T-SQL 陳述式。</span><span class="sxs-lookup"><span data-stu-id="a49ea-139">Copy hello Id for user1@contoso.com, and paste it into hello T-SQL statement below.</span></span> <span data-ttu-id="a49ea-140">執行與此使用者識別碼 hello 連絡人此陳述式 tooassociate 三個。</span><span class="sxs-lookup"><span data-stu-id="a49ea-140">Execute this statement tooassociate three of hello Contacts with this UserId.</span></span>

```
UPDATE Contacts SET UserId = '19bc9b0d-28dd-4510-bd5e-d6b6d445f511'
WHERE ContactId IN (1, 2, 5)
```

## <a name="step-3-create-a-row-level-security-policy-in-hello-database"></a><span data-ttu-id="a49ea-141">步驟 3: Hello 資料庫中建立的資料列層級安全性原則</span><span class="sxs-lookup"><span data-stu-id="a49ea-141">Step 3: Create a Row-Level Security policy in hello database</span></span>
<span data-ttu-id="a49ea-142">hello 最後一個步驟是 toocreate 使用查詢所傳回的 SESSION_CONTEXT tooautomatically 篩選 hello 結果中的 hello UserId 的安全性原則。</span><span class="sxs-lookup"><span data-stu-id="a49ea-142">hello final step is toocreate a security policy that uses hello UserId in SESSION_CONTEXT tooautomatically filter hello results returned by queries.</span></span>

<span data-ttu-id="a49ea-143">仍然連接的 toohello 資料庫時執行下列 T-SQL hello:</span><span class="sxs-lookup"><span data-stu-id="a49ea-143">While still connected toohello database, execute hello following T-SQL:</span></span>

```
CREATE SCHEMA Security
go

CREATE FUNCTION Security.userAccessPredicate(@UserId nvarchar(128))
    RETURNS TABLE
    WITH SCHEMABINDING
AS
    RETURN SELECT 1 AS accessResult
    WHERE @UserId = CAST(SESSION_CONTEXT(N'UserId') AS nvarchar(128))
go

CREATE SECURITY POLICY Security.userSecurityPolicy
    ADD FILTER PREDICATE Security.userAccessPredicate(UserId) ON dbo.Contacts,
    ADD BLOCK PREDICATE Security.userAccessPredicate(UserId) ON dbo.Contacts
go

```

<span data-ttu-id="a49ea-144">此程式碼會執行三個動作。</span><span class="sxs-lookup"><span data-stu-id="a49ea-144">This code does three things.</span></span> <span data-ttu-id="a49ea-145">首先，它會建立新的結構描述集中和限制存取 toohello RLS 物件的最佳作法。</span><span class="sxs-lookup"><span data-stu-id="a49ea-145">First, it creates a new schema as a best practice for centralizing and limiting access toohello RLS objects.</span></span> <span data-ttu-id="a49ea-146">接下來，它會建立 hello 使用者識別碼的資料列符合 hello SESSION_CONTEXT 中的使用者識別碼時，會傳回 '1' 的述詞函式。</span><span class="sxs-lookup"><span data-stu-id="a49ea-146">Next, it creates a predicate function that will return '1' when hello UserId of a row matches hello UserId in SESSION_CONTEXT.</span></span> <span data-ttu-id="a49ea-147">最後，它會建立與 hello 連絡人 」 資料表上同時執行篩選及區塊述詞新增此函數的安全性原則。</span><span class="sxs-lookup"><span data-stu-id="a49ea-147">Finally, it creates a security policy that adds this function as both a filter and block predicate on hello Contacts table.</span></span> <span data-ttu-id="a49ea-148">hello 篩選器述詞會造成查詢 tooreturn 唯一資料列屬於 toohello 目前的使用者，並 hello block 述詞做為防護措施 tooprevent hello 應用程式永遠不小心插入 hello 錯誤的使用者的資料列。</span><span class="sxs-lookup"><span data-stu-id="a49ea-148">hello filter predicate causes queries tooreturn only rows that belong toohello current user, and hello block predicate acts as a safeguard tooprevent hello application from ever accidentally inserting a row for hello wrong user.</span></span>

<span data-ttu-id="a49ea-149">現在執行 hello 應用程式，並以登入user1@contoso.com。此使用者現在會看到我們指派 toothis UserId 先前只有 hello 連絡人：</span><span class="sxs-lookup"><span data-stu-id="a49ea-149">Now run hello application, and sign in as user1@contoso.com. This user now sees only hello Contacts we assigned toothis UserId earlier:</span></span>

![啟用 RLS 之前的連絡人管理員應用程式](./media/web-sites-dotnet-entity-framework-row-level-security/ContactManagerApp-After.png)

<span data-ttu-id="a49ea-151">toovalidate 這此外，請重試登錄新的使用者。</span><span class="sxs-lookup"><span data-stu-id="a49ea-151">toovalidate this further, try registering a new user.</span></span> <span data-ttu-id="a49ea-152">因為沒有任何已指派 toothem，他們會看到任何連絡人。</span><span class="sxs-lookup"><span data-stu-id="a49ea-152">They will see no contacts, because none have been assigned toothem.</span></span> <span data-ttu-id="a49ea-153">如果他們建立新的連絡人，則會指派 toothem，而且只將其無法 toosee 它。</span><span class="sxs-lookup"><span data-stu-id="a49ea-153">If they create a new contact, it will be assigned toothem, and only they will be able toosee it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a49ea-154">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a49ea-154">Next steps</span></span>
<span data-ttu-id="a49ea-155">就這麼簡單！</span><span class="sxs-lookup"><span data-stu-id="a49ea-155">That's it!</span></span> <span data-ttu-id="a49ea-156">hello 簡單連絡管理員 web 應用程式都已轉換成每個使用者擁有它自己的連絡人清單的其中一個多租用戶。</span><span class="sxs-lookup"><span data-stu-id="a49ea-156">hello simple Contact Manager web app has been converted into a multi-tenant one where each user has its own contact list.</span></span> <span data-ttu-id="a49ea-157">使用資料列層級安全性，我們已經可以避免 hello 複雜度強制執行應用程式的程式碼中的租用戶存取邏輯。</span><span class="sxs-lookup"><span data-stu-id="a49ea-157">By using Row-Level Security, we've avoided hello complexity of enforcing tenant access logic in our application code.</span></span> <span data-ttu-id="a49ea-158">此投影片允許 hello 應用程式 toofocus 手邊，hello 真實商務問題，並也會減少不慎洩漏資料，如 hello 應用程式的程式碼庫 hello 風險成長。</span><span class="sxs-lookup"><span data-stu-id="a49ea-158">This transparency allows hello application toofocus on hello real business problem at hand, and it also reduces hello risk of accidentally leaking data as hello application's codebase grows.</span></span>

<span data-ttu-id="a49ea-159">本教學課程有只刮傷的 hello 介面 rls 可行。</span><span class="sxs-lookup"><span data-stu-id="a49ea-159">This tutorial has only scratched hello surface of what's possible with RLS.</span></span> <span data-ttu-id="a49ea-160">比方說，它可能更複雜的 toohave 或細微的存取權邏輯和它的可能 toostore 而已 hello hello SESSION_CONTEXT 中目前的使用者識別碼。</span><span class="sxs-lookup"><span data-stu-id="a49ea-160">For instance, it's possible toohave more sophisticated or granular access logic, and it's possible toostore more than just hello current UserId in hello SESSION_CONTEXT.</span></span> <span data-ttu-id="a49ea-161">此外，也可以太[RLS 整合 hello 彈性資料庫工具用戶端程式庫](../sql-database/sql-database-elastic-tools-multi-tenant-row-level-security.md)toosupport 向外延展資料層中的多租用戶分區。</span><span class="sxs-lookup"><span data-stu-id="a49ea-161">It's also possible too[integrate RLS with hello elastic database tools client libraries](../sql-database/sql-database-elastic-tools-multi-tenant-row-level-security.md) toosupport multi-tenant shards in a scale-out data tier.</span></span>

<span data-ttu-id="a49ea-162">超出這些可能性，我們也正在 toomake RLS 更好。</span><span class="sxs-lookup"><span data-stu-id="a49ea-162">Beyond these possibilities, we're also working toomake RLS even better.</span></span> <span data-ttu-id="a49ea-163">如果您有任何問題、 意見或您想要 toosee 的項目，請讓我們知道 hello 註解中。</span><span class="sxs-lookup"><span data-stu-id="a49ea-163">If you have any questions, ideas, or things you'd like toosee, please let us know in hello comments.</span></span> <span data-ttu-id="a49ea-164">歡迎提供意見反應！</span><span class="sxs-lookup"><span data-stu-id="a49ea-164">We appreciate your feedback!</span></span>

