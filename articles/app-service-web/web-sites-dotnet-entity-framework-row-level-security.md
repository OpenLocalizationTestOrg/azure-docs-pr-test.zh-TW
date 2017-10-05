---
title: "教學課程：使用 Entity Framework 和資料列層級安全性的 Web 應用程式搭配多租用戶資料庫"
description: "了解如何使用 Entity Framework 和資料列層級安全性，搭配多租用戶 SQL Database 後端來開發 ASP.NET MVC 5 Web 應用程式。"
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
ms.openlocfilehash: ba1bb3d84b462dfebbb2564569517d7336bf54fd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-web-app-with-a-multi-tenant-database-using-entity-framework-and-row-level-security"></a><span data-ttu-id="1cd83-103">教學課程：使用 Entity Framework 和資料列層級安全性的 Web 應用程式搭配多租用戶資料庫</span><span class="sxs-lookup"><span data-stu-id="1cd83-103">Tutorial: Web app with a multi-tenant database using Entity Framework and Row-Level Security</span></span>
<span data-ttu-id="1cd83-104">本教學課程示範如何使用 Entity Framework 和[資料列層級安全性](https://msdn.microsoft.com/library/dn765131.aspx)，搭配 "[共用的資料庫、共用的結構描述](https://msdn.microsoft.com/library/aa479086.aspx)" 租用模型，建置多租用戶 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="1cd83-104">This tutorial shows how to build a multi-tenant web app with a "[shared database, shared schema](https://msdn.microsoft.com/library/aa479086.aspx)" tenancy model, using Entity Framework and [Row-Level Security](https://msdn.microsoft.com/library/dn765131.aspx).</span></span> <span data-ttu-id="1cd83-105">在此模型中，單一資料庫包含許多租用戶的資料，而且每個資料表中的每個資料列都有一個相關聯的「租用戶識別碼」。</span><span class="sxs-lookup"><span data-stu-id="1cd83-105">In this model, a single database contains data for many tenants, and each row in each table is associated with a "Tenant ID."</span></span> <span data-ttu-id="1cd83-106">資料列層級安全性 (RLS) 是 Azure SQL Database 的新功能，用來防止租用戶存取彼此的資料。</span><span class="sxs-lookup"><span data-stu-id="1cd83-106">Row-Level Security (RLS), a new feature for Azure SQL Database, is used to prevent tenants from accessing each other's data.</span></span> <span data-ttu-id="1cd83-107">這只需要對應用程式進行一次微幅的變更即可。</span><span class="sxs-lookup"><span data-stu-id="1cd83-107">This requires just a single, small change to the application.</span></span> <span data-ttu-id="1cd83-108">RLS 將租用戶存取邏輯集中在資料庫本身之內，簡化應用程式碼並降低租用戶之間不慎洩露資料的風險。</span><span class="sxs-lookup"><span data-stu-id="1cd83-108">By centralizing the tenant access logic within the database itself, RLS simplifies the application code and reduces the risk of accidental data leakage between tenants.</span></span>

<span data-ttu-id="1cd83-109">我們就從 [使用驗證和 SQL DB 建立 ASP.NET MVC 應用程式並部署至 Azure App Service](web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database.md)中簡單的「連絡人管理員」應用程式開始。</span><span class="sxs-lookup"><span data-stu-id="1cd83-109">Let's start with the simple Contact Manager application from [Create an ASP.NET MVP app with auth and SQL DB and deploy to Azure App Service](web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database.md).</span></span> <span data-ttu-id="1cd83-110">現在，此應用程式允許所有使用者 (租用戶) 看見所有連絡人：</span><span class="sxs-lookup"><span data-stu-id="1cd83-110">Right now, the application allows all users (tenants) to see all contacts:</span></span>

![啟用 RLS 之前的連絡人管理員應用程式](./media/web-sites-dotnet-entity-framework-row-level-security/ContactManagerApp-Before.png)

<span data-ttu-id="1cd83-112">只要經過少數的微幅變更，我們就能支援多租用戶，讓使用者能夠看見屬於他們的連絡人。</span><span class="sxs-lookup"><span data-stu-id="1cd83-112">With just a few small changes, we will add support for multi-tenancy, so that users are able to see only the contacts that belong to them.</span></span>

## <a name="step-1-add-an-interceptor-class-in-the-application-to-set-the-sessioncontext"></a><span data-ttu-id="1cd83-113">步驟 1：在應用程式中加入「攔截器」類別來設定 SESSION_CONTEXT</span><span class="sxs-lookup"><span data-stu-id="1cd83-113">Step 1: Add an Interceptor class in the application to set the SESSION_CONTEXT</span></span>
<span data-ttu-id="1cd83-114">我們需要進行一項應用程式變更。</span><span class="sxs-lookup"><span data-stu-id="1cd83-114">There is one application change we need to make.</span></span> <span data-ttu-id="1cd83-115">因為所有應用程式使用者使用相同的連接字串 (也就是相同的 SQL 登入) 連線到資料庫，RLS 原則目前無法知道應該篩選哪一個使用者。</span><span class="sxs-lookup"><span data-stu-id="1cd83-115">Because all application users connect to the database using the same connection string (i.e. same SQL login), there is currently no way for an RLS policy to know which user it should filter for.</span></span> <span data-ttu-id="1cd83-116">這種方法在 Web 應用程式中很常見，因為可讓連接共用更有效率，但這表示我們需要另一種方式來識別資料庫內目前的應用程式使用者。</span><span class="sxs-lookup"><span data-stu-id="1cd83-116">This approach is very common in web applications because it enables efficient connection pooling, but it means we need another way to identify the current application user within the database.</span></span> <span data-ttu-id="1cd83-117">解決方法是在執行查詢之前，讓應用程式在開啟連接之後立即在 [SESSION_CONTEXT](https://msdn.microsoft.com/library/mt590806) 中設定目前 UserId 的機碼值組。</span><span class="sxs-lookup"><span data-stu-id="1cd83-117">The solution is to have the application set a key-value pair for the current UserId in the [SESSION_CONTEXT](https://msdn.microsoft.com/library/mt590806) immediately after opening a connection, before it executes any queries.</span></span> <span data-ttu-id="1cd83-118">SESSION_CONTEXT 是工作階段範圍的機碼值存放區，RLS 原則會使用其中儲存的 UserId 來識別目前的使用者。</span><span class="sxs-lookup"><span data-stu-id="1cd83-118">SESSION_CONTEXT is a session-scoped key-value store, and our RLS policy will use the UserId stored in it to identify the current user.</span></span>

<span data-ttu-id="1cd83-119">我們會加入[攔截器](https://msdn.microsoft.com/data/dn469464.aspx) (特別是 [DbConnectionInterceptor](https://msdn.microsoft.com/library/system.data.entity.infrastructure.interception.idbconnectioninterceptor))，這是 Entity Framework (EF) 6 中的新功能，可在 EF 開啟連接時執行 T-SQL 陳述式，以自動在 SESSION_CONTEXT 中設定目前的 UserId。</span><span class="sxs-lookup"><span data-stu-id="1cd83-119">We will add an [interceptor](https://msdn.microsoft.com/data/dn469464.aspx) (in particular, a [DbConnectionInterceptor](https://msdn.microsoft.com/library/system.data.entity.infrastructure.interception.idbconnectioninterceptor)), a new feature in Entity Framework (EF) 6, to automatically set the current UserId in the SESSION_CONTEXT by executing a T-SQL statement whenever EF opens a connection.</span></span>

1. <span data-ttu-id="1cd83-120">在 Visual Studio 中開啟 ContactManager 專案。</span><span class="sxs-lookup"><span data-stu-id="1cd83-120">Open the ContactManager project in Visual Studio.</span></span>
2. <span data-ttu-id="1cd83-121">在 [方案總管] 中，以滑鼠右鍵按一下 [模型] 資料夾，然後選擇 [新增] -> [類別]。</span><span class="sxs-lookup"><span data-stu-id="1cd83-121">Right-click on the Models folder in the Solution Explorer, and choose Add > Class.</span></span>
3. <span data-ttu-id="1cd83-122">將新類別命名為 "SessionContextInterceptor.cs"，按一下 [加入]。</span><span class="sxs-lookup"><span data-stu-id="1cd83-122">Name the new class "SessionContextInterceptor.cs" and click Add.</span></span>
4. <span data-ttu-id="1cd83-123">使用下列程式碼取代 SessionContextInterceptor.cs 的內容。</span><span class="sxs-lookup"><span data-stu-id="1cd83-123">Replace the contents of SessionContextInterceptor.cs with the following code.</span></span>

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
            // Set SESSION_CONTEXT to current UserId whenever EF opens a connection
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

<span data-ttu-id="1cd83-124">這是唯一需要的應用程式變更。</span><span class="sxs-lookup"><span data-stu-id="1cd83-124">That's the only application change required.</span></span> <span data-ttu-id="1cd83-125">接著開始建置並發佈應用程式。</span><span class="sxs-lookup"><span data-stu-id="1cd83-125">Go ahead and build and publish the application.</span></span>

## <a name="step-2-add-a-userid-column-to-the-database-schema"></a><span data-ttu-id="1cd83-126">步驟 2：將 UserId 資料行加入至資料庫結構描述</span><span class="sxs-lookup"><span data-stu-id="1cd83-126">Step 2: Add a UserId column to the database schema</span></span>
<span data-ttu-id="1cd83-127">接下來，我們需要將 UserId 資料行加入至 Contacts 資料表，使每個資料列與使用者 (租用戶) 相關聯。</span><span class="sxs-lookup"><span data-stu-id="1cd83-127">Next, we need to add a UserId column to the Contacts table to associate each row with a user (tenant).</span></span> <span data-ttu-id="1cd83-128">我們將直接在資料庫中變更結構描述，所以 EF 資料模型中不必包含此欄位。</span><span class="sxs-lookup"><span data-stu-id="1cd83-128">We will alter the schema directly in the database, so that we don't have to include this field in our EF data model.</span></span>

<span data-ttu-id="1cd83-129">使用 SQL Server Management Studio 或 Visual Studio，直接連接到資料庫，然後執行下列 T-SQL：</span><span class="sxs-lookup"><span data-stu-id="1cd83-129">Connect to the database directly, using either SQL Server Management Studio or Visual Studio, and then execute the following T-SQL:</span></span>

```
ALTER TABLE Contacts ADD UserId nvarchar(128)
    DEFAULT CAST(SESSION_CONTEXT(N'UserId') AS nvarchar(128))
```

<span data-ttu-id="1cd83-130">這會將 UserId 資料行加入至 Contacts 資料表。</span><span class="sxs-lookup"><span data-stu-id="1cd83-130">This adds a UserId column to the Contacts table.</span></span> <span data-ttu-id="1cd83-131">我們使用 nvarchar (128) 資料類型來比對儲存在 AspNetUsers 資料表中的 UserId，我們也建立 DEFAULT 條件約束，自動將新插入的資料列的 UserId 設定為目前儲存在 SESSION_CONTEXT 中的 UserId。</span><span class="sxs-lookup"><span data-stu-id="1cd83-131">We use the nvarchar(128) data type to match the UserIds stored in the AspNetUsers table, and we create a DEFAULT constraint that will automatically set the UserId for newly inserted rows to be the UserId currently stored in SESSION_CONTEXT.</span></span>

<span data-ttu-id="1cd83-132">現在，資料表如下所示：</span><span class="sxs-lookup"><span data-stu-id="1cd83-132">Now the table looks like this:</span></span>

![SSMS Contacts 資料表](./media/web-sites-dotnet-entity-framework-row-level-security/SSMS-Contacts.png)

<span data-ttu-id="1cd83-134">建立新的連絡人時，將會自動指派正確的 UserId 給他們。</span><span class="sxs-lookup"><span data-stu-id="1cd83-134">When new contacts are created, they'll automatically be assigned the correct UserId.</span></span> <span data-ttu-id="1cd83-135">但為了示範，我們還是指派幾個現有的連絡人給現有的使用者。</span><span class="sxs-lookup"><span data-stu-id="1cd83-135">For demo purposes, however, let's assign a few of these existing contacts to an existing user.</span></span>

<span data-ttu-id="1cd83-136">如果您已在應用程式建立一些使用者 (例如使用本機、Google 或 Facebook 帳戶)，就可以在 AspNetUsers 資料表中看見他們。</span><span class="sxs-lookup"><span data-stu-id="1cd83-136">If you've created a few users in the application already (e.g., using local, Google, or Facebook accounts), you'll see them in the AspNetUsers table.</span></span> <span data-ttu-id="1cd83-137">在以下的螢幕擷取畫面中，目前為止只有一個使用者。</span><span class="sxs-lookup"><span data-stu-id="1cd83-137">In the screenshot below, there is only one user so far.</span></span>

![SSMS AspNetUsers 資料表](./media/web-sites-dotnet-entity-framework-row-level-security/SSMS-AspNetUsers.png)

<span data-ttu-id="1cd83-139">複製 user1@contoso.com 的 Id，並貼到以下的 T-SQL 陳述式中。</span><span class="sxs-lookup"><span data-stu-id="1cd83-139">Copy the Id for user1@contoso.com, and paste it into the T-SQL statement below.</span></span> <span data-ttu-id="1cd83-140">執行此陳述式，將三個連絡人與此 UserId 相關聯。</span><span class="sxs-lookup"><span data-stu-id="1cd83-140">Execute this statement to associate three of the Contacts with this UserId.</span></span>

```
UPDATE Contacts SET UserId = '19bc9b0d-28dd-4510-bd5e-d6b6d445f511'
WHERE ContactId IN (1, 2, 5)
```

## <a name="step-3-create-a-row-level-security-policy-in-the-database"></a><span data-ttu-id="1cd83-141">步驟 3：在資料庫中建立資料列層級安全性原則</span><span class="sxs-lookup"><span data-stu-id="1cd83-141">Step 3: Create a Row-Level Security policy in the database</span></span>
<span data-ttu-id="1cd83-142">最後一個步驟是建立安全性原則，使用 SESSION_CONTEXT 中的 UserId 自動篩選查詢所傳回的結果。</span><span class="sxs-lookup"><span data-stu-id="1cd83-142">The final step is to create a security policy that uses the UserId in SESSION_CONTEXT to automatically filter the results returned by queries.</span></span>

<span data-ttu-id="1cd83-143">在仍然連接資料庫的情況下，執行下列 T-SQL：</span><span class="sxs-lookup"><span data-stu-id="1cd83-143">While still connected to the database, execute the following T-SQL:</span></span>

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

<span data-ttu-id="1cd83-144">此程式碼會執行三個動作。</span><span class="sxs-lookup"><span data-stu-id="1cd83-144">This code does three things.</span></span> <span data-ttu-id="1cd83-145">首先，建立新的結構描述，當作集中管理和限制 RLS 物件存取權的最佳作法。</span><span class="sxs-lookup"><span data-stu-id="1cd83-145">First, it creates a new schema as a best practice for centralizing and limiting access to the RLS objects.</span></span> <span data-ttu-id="1cd83-146">接著，建立述詞函數，當資料列的 UserId 符合 SESSION_CONTEXT 中的 UserId 時，將傳回 '1'。</span><span class="sxs-lookup"><span data-stu-id="1cd83-146">Next, it creates a predicate function that will return '1' when the UserId of a row matches the UserId in SESSION_CONTEXT.</span></span> <span data-ttu-id="1cd83-147">最後，建立安全性原則，在 Contacts 資料表上加入此函數作為篩選和封鎖述詞。</span><span class="sxs-lookup"><span data-stu-id="1cd83-147">Finally, it creates a security policy that adds this function as both a filter and block predicate on the Contacts table.</span></span> <span data-ttu-id="1cd83-148">篩選述詞可讓查詢只傳回屬於目前使用者的資料列，而封鎖述詞充當保護措施，防止應用程式不慎插入錯誤使用者的資料列。</span><span class="sxs-lookup"><span data-stu-id="1cd83-148">The filter predicate causes queries to return only rows that belong to the current user, and the block predicate acts as a safeguard to prevent the application from ever accidentally inserting a row for the wrong user.</span></span>

<span data-ttu-id="1cd83-149">現在執行應用程式，並以 user1@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="1cd83-149">Now run the application, and sign in as user1@contoso.com.</span></span> <span data-ttu-id="1cd83-150">這位使用者現在只會看到我們稍早指派給此 UserId 的連絡人：</span><span class="sxs-lookup"><span data-stu-id="1cd83-150">This user now sees only the Contacts we assigned to this UserId earlier:</span></span>

![啟用 RLS 之前的連絡人管理員應用程式](./media/web-sites-dotnet-entity-framework-row-level-security/ContactManagerApp-After.png)

<span data-ttu-id="1cd83-152">若要進一步驗證，請嘗試註冊新的使用者。</span><span class="sxs-lookup"><span data-stu-id="1cd83-152">To validate this further, try registering a new user.</span></span> <span data-ttu-id="1cd83-153">因為尚未指派連絡人給他們，他們看不到任何連絡人。</span><span class="sxs-lookup"><span data-stu-id="1cd83-153">They will see no contacts, because none have been assigned to them.</span></span> <span data-ttu-id="1cd83-154">如果他們建立新的連絡人，則會指派給他們，也只有他們才能看見這個連絡人。</span><span class="sxs-lookup"><span data-stu-id="1cd83-154">If they create a new contact, it will be assigned to them, and only they will be able to see it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1cd83-155">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1cd83-155">Next steps</span></span>
<span data-ttu-id="1cd83-156">就這麼簡單！</span><span class="sxs-lookup"><span data-stu-id="1cd83-156">That's it!</span></span> <span data-ttu-id="1cd83-157">這個簡單的連絡人管理員 Web 應用程式已轉換成多租用戶應用程式，每個使用者都有自己的連絡人清單。</span><span class="sxs-lookup"><span data-stu-id="1cd83-157">The simple Contact Manager web app has been converted into a multi-tenant one where each user has its own contact list.</span></span> <span data-ttu-id="1cd83-158">由於使用資料列層級安全性，我們已避免在應用程式碼中強制執行租用戶存取邏輯的複雜性。</span><span class="sxs-lookup"><span data-stu-id="1cd83-158">By using Row-Level Security, we've avoided the complexity of enforcing tenant access logic in our application code.</span></span> <span data-ttu-id="1cd83-159">這種透明度可讓應用程式專注於處理目前的實際商務問題，而隨著應用程式的程式碼基底不斷成長，也能降低意外洩漏資料的風險。</span><span class="sxs-lookup"><span data-stu-id="1cd83-159">This transparency allows the application to focus on the real business problem at hand, and it also reduces the risk of accidentally leaking data as the application's codebase grows.</span></span>

<span data-ttu-id="1cd83-160">本教學課程只是稍微示範一下 RLS 的功能。</span><span class="sxs-lookup"><span data-stu-id="1cd83-160">This tutorial has only scratched the surface of what's possible with RLS.</span></span> <span data-ttu-id="1cd83-161">比方說，存取邏輯可以更複雜或更精細，而 SESSION_CONTEXT 中也不僅止於只能儲存目前的 UserId 而已。</span><span class="sxs-lookup"><span data-stu-id="1cd83-161">For instance, it's possible to have more sophisticated or granular access logic, and it's possible to store more than just the current UserId in the SESSION_CONTEXT.</span></span> <span data-ttu-id="1cd83-162">也可以 [整合 RLS 與彈性資料庫工具用戶端程式庫](../sql-database/sql-database-elastic-tools-multi-tenant-row-level-security.md) ，在相應放大的資料層中支援多租用戶分區。</span><span class="sxs-lookup"><span data-stu-id="1cd83-162">It's also possible to [integrate RLS with the elastic database tools client libraries](../sql-database/sql-database-elastic-tools-multi-tenant-row-level-security.md) to support multi-tenant shards in a scale-out data tier.</span></span>

<span data-ttu-id="1cd83-163">除了這些可能性，我們也正在努力讓 RLS 更臻完美。</span><span class="sxs-lookup"><span data-stu-id="1cd83-163">Beyond these possibilities, we're also working to make RLS even better.</span></span> <span data-ttu-id="1cd83-164">如果您有任何疑問、構想或期望，請留下您的意見。</span><span class="sxs-lookup"><span data-stu-id="1cd83-164">If you have any questions, ideas, or things you'd like to see, please let us know in the comments.</span></span> <span data-ttu-id="1cd83-165">歡迎提供意見反應！</span><span class="sxs-lookup"><span data-stu-id="1cd83-165">We appreciate your feedback!</span></span>

