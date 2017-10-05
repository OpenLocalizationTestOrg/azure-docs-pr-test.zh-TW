---
title: "在彈性資料庫用戶端程式庫中管理認證 | Microsoft Docs"
description: "如何設定彈性資料庫應用程式的正確認證層級 (管理員到唯讀)"
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: 72e0edaf-795e-4856-84a5-6594f735fb7e
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: 46908be2846062a0520d21e06db3091a4d711b0b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="credentials-used-to-access-the-elastic-database-client-library"></a><span data-ttu-id="e7e30-103">用來存取彈性資料庫用戶端程式庫的認證</span><span class="sxs-lookup"><span data-stu-id="e7e30-103">Credentials used to access the Elastic Database client library</span></span>
<span data-ttu-id="e7e30-104">[彈性資料庫用戶端程式庫](http://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/)使用三種不同的認證存取[分區對應管理員](sql-database-elastic-scale-shard-map-management.md)。</span><span class="sxs-lookup"><span data-stu-id="e7e30-104">The [Elastic Database client library](http://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/) uses three different kinds  of credentials to access the [shard map manager](sql-database-elastic-scale-shard-map-management.md).</span></span> <span data-ttu-id="e7e30-105">視需要使用盡可能低的存取層級認證。</span><span class="sxs-lookup"><span data-stu-id="e7e30-105">Depending on the need, use the credential with  the lowest level of access possible.</span></span>

* <span data-ttu-id="e7e30-106">**管理認證**：建立或操作分區對應管理員。</span><span class="sxs-lookup"><span data-stu-id="e7e30-106">**Management credentials**: for creating or manipulating a shard map manager.</span></span> <span data-ttu-id="e7e30-107">(請參閱[詞彙](sql-database-elastic-scale-glossary.md)。)</span><span class="sxs-lookup"><span data-stu-id="e7e30-107">(See the [glossary](sql-database-elastic-scale-glossary.md).)</span></span> 
* <span data-ttu-id="e7e30-108">**存取認證**：存取現有的分區對應管理員，以取得分區的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="e7e30-108">**Access credentials**: to access an existing shard map manager to obtain information about shards.</span></span>
* <span data-ttu-id="e7e30-109">**連接認證**：連接到分區。</span><span class="sxs-lookup"><span data-stu-id="e7e30-109">**Connection credentials**: to connect to shards.</span></span> 

<span data-ttu-id="e7e30-110">另請參閱 [在 Azure SQL Database 中管理資料庫與登入](sql-database-manage-logins.md)。</span><span class="sxs-lookup"><span data-stu-id="e7e30-110">See also [Managing databases and logins in Azure SQL Database](sql-database-manage-logins.md).</span></span> 

## <a name="about-management-credentials"></a><span data-ttu-id="e7e30-111">關於管理認證</span><span class="sxs-lookup"><span data-stu-id="e7e30-111">About management credentials</span></span>
<span data-ttu-id="e7e30-112">管理認證會用來建立操作分區對應之應用程式的 [**ShardMapManager**](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.aspx) 物件。</span><span class="sxs-lookup"><span data-stu-id="e7e30-112">Management credentials are used to create a [**ShardMapManager**](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.aspx) object for applications that manipulate shard maps.</span></span> <span data-ttu-id="e7e30-113">(如需範例，請參閱[使用彈性資料庫工具加入分區](sql-database-elastic-scale-add-a-shard.md)和[資料相依路由](sql-database-elastic-scale-data-dependent-routing.md)) 彈性級別用戶端程式庫的使用者可建立 SQL 使用者和 SQL 登入，也要確定將全域分區對應資料庫及所有分區資料庫的讀取/寫入權限授與給每個人。</span><span class="sxs-lookup"><span data-stu-id="e7e30-113">(For example, see [Adding a shard using Elastic Database tools](sql-database-elastic-scale-add-a-shard.md) and [Data dependent routing](sql-database-elastic-scale-data-dependent-routing.md)) The user of the elastic scale client library creates the SQL users and SQL logins and makes sure each is granted the read/write permissions on the global shard map database and all shard databases as well.</span></span> <span data-ttu-id="e7e30-114">在分區對應上執行變更時，這些認證用來維護全域分區對應和本機分區對應。</span><span class="sxs-lookup"><span data-stu-id="e7e30-114">These credentials are used to maintain the global shard map and the local shard maps when changes to the shard map are performed.</span></span> <span data-ttu-id="e7e30-115">例如，使用管理認證來建立分區對應管理員物件 (使用 [**GetSqlShardMapManager**](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.getsqlshardmapmanager.aspx)：</span><span class="sxs-lookup"><span data-stu-id="e7e30-115">For instance, use the management credentials to create the shard map manager object (using [**GetSqlShardMapManager**](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.getsqlshardmapmanager.aspx):</span></span> 

    // Obtain a shard map manager. 
    ShardMapManager shardMapManager = ShardMapManagerFactory.GetSqlShardMapManager( 
            smmAdminConnectionString, 
            ShardMapManagerLoadPolicy.Lazy 
    ); 

<span data-ttu-id="e7e30-116">變數 **smmAdminConnectionString** 是包含管理認證的連接字串。</span><span class="sxs-lookup"><span data-stu-id="e7e30-116">The variable **smmAdminConnectionString** is a connection string that contains the management credentials.</span></span> <span data-ttu-id="e7e30-117">使用者識別碼和密碼提供分區對應資料庫以及個別分區的讀取/寫入存取權。</span><span class="sxs-lookup"><span data-stu-id="e7e30-117">The user ID and password provides read/write access to both shard map database and individual shards.</span></span> <span data-ttu-id="e7e30-118">管理連接字串也包含伺服器名稱和資料庫名稱，以識別全域分區對應資料庫。</span><span class="sxs-lookup"><span data-stu-id="e7e30-118">The management connection string also includes the server name and database name to identify the global shard map database.</span></span> <span data-ttu-id="e7e30-119">以下是針對該用途的一般連接字串：</span><span class="sxs-lookup"><span data-stu-id="e7e30-119">Here is a typical connection string for that purpose:</span></span>

     "Server=<yourserver>.database.windows.net;Database=<yourdatabase>;User ID=<yourmgmtusername>;Password=<yourmgmtpassword>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30;” 

<span data-ttu-id="e7e30-120">請勿使用值的形式"username@server"— 改為使用"username"值。</span><span class="sxs-lookup"><span data-stu-id="e7e30-120">Do not use values in the form of "username@server"—instead just use the "username" value.</span></span>  <span data-ttu-id="e7e30-121">這是因為認證必須同時適用於入分區對應管理員資料庫和個別分區 (可能位於不同的伺服器上)。</span><span class="sxs-lookup"><span data-stu-id="e7e30-121">This is because credentials must work against both the shard map manager database and individual shards, which may be on different servers.</span></span>

## <a name="access-credentials"></a><span data-ttu-id="e7e30-122">存取認證</span><span class="sxs-lookup"><span data-stu-id="e7e30-122">Access credentials</span></span>
<span data-ttu-id="e7e30-123">在不管理分區對應的應用程式中建立分區對應管理員時，請使用在全域分區對應上具有唯讀權限的認證。</span><span class="sxs-lookup"><span data-stu-id="e7e30-123">When creating a shard map manager in an application that does not administer shard maps, use credentials that have read-only permissions on the global shard map.</span></span> <span data-ttu-id="e7e30-124">在這些認證下，從全域分區對應所擷取的資訊用於 [資料相依路由](sql-database-elastic-scale-data-dependent-routing.md) ，以及填入用戶端的分區對應快取。</span><span class="sxs-lookup"><span data-stu-id="e7e30-124">The information retrieved from the global shard map under these credentials are used for [data-dependent routing](sql-database-elastic-scale-data-dependent-routing.md) and to populate the shard map cache on the client.</span></span> <span data-ttu-id="e7e30-125">認證是透過 **GetSqlShardMapManager** 的相同呼叫模式來提供，如上所示：</span><span class="sxs-lookup"><span data-stu-id="e7e30-125">The credentials are provided through the same call pattern to **GetSqlShardMapManager** as shown above:</span></span> 

    // Obtain shard map manager. 
    ShardMapManager shardMapManager = ShardMapManagerFactory.GetSqlShardMapManager( 
            smmReadOnlyConnectionString, 
            ShardMapManagerLoadPolicy.Lazy
    );  

<span data-ttu-id="e7e30-126">請注意，我們使用 **smmReadOnlyConnectionString**，以反映使用不同的認證以代表**非管理員**使用者進行此存取：這些認證不應提供全域分區對應上的寫入權限。</span><span class="sxs-lookup"><span data-stu-id="e7e30-126">Note the use of the **smmReadOnlyConnectionString** to reflect the use of different credentials for this access on behalf of **non-admin** users: these credentials should not provide write permissions on the global shard map.</span></span> 

## <a name="connection-credentials"></a><span data-ttu-id="e7e30-127">連接認證</span><span class="sxs-lookup"><span data-stu-id="e7e30-127">Connection credentials</span></span>
<span data-ttu-id="e7e30-128">使用 [**OpenConnectionForKey**](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.openconnectionforkey.aspx) 方法來存取與分區索引鍵相關聯的分區時，需要額外的認證。</span><span class="sxs-lookup"><span data-stu-id="e7e30-128">Additional credentials are needed when using the [**OpenConnectionForKey**](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.openconnectionforkey.aspx) method to access a shard associated with a sharding key.</span></span> <span data-ttu-id="e7e30-129">這些認證必須提供唯讀權限來存取分區上的本機分區對應資料表。</span><span class="sxs-lookup"><span data-stu-id="e7e30-129">These credentials need to provide permissions for read-only access to the local shard map tables residing on the shard.</span></span> <span data-ttu-id="e7e30-130">在分區上執行資料相依路由的連線驗證時，這是必要的。</span><span class="sxs-lookup"><span data-stu-id="e7e30-130">This is needed to perform connection validation for data-dependent routing on the shard.</span></span> <span data-ttu-id="e7e30-131">此程式碼片段允許資料依存路由內容中的資料存取：</span><span class="sxs-lookup"><span data-stu-id="e7e30-131">This code snippet allows data access in the context of data dependent routing:</span></span> 

    using (SqlConnection conn = rangeMap.OpenConnectionForKey<int>( 
    targetWarehouse, smmUserConnectionString, ConnectionOptions.Validate)) 

<span data-ttu-id="e7e30-132">在此範例中， **smmUserConnectionString** 保留使用者認證的連接字串。</span><span class="sxs-lookup"><span data-stu-id="e7e30-132">In this example, **smmUserConnectionString** holds the connection string for the user credentials.</span></span> <span data-ttu-id="e7e30-133">在 Azure SQL DB 中，以下是使用者認證的一般連接字串：</span><span class="sxs-lookup"><span data-stu-id="e7e30-133">For Azure SQL DB, here is a typical connection string for user credentials:</span></span> 

    "User ID=<yourusername>; Password=<youruserpassword>; Trusted_Connection=False; Encrypt=True; Connection Timeout=30;”  

<span data-ttu-id="e7e30-134">如同管理認證，請勿不中的值形式的"username@server"。</span><span class="sxs-lookup"><span data-stu-id="e7e30-134">As with the admin credentials, do not values in the form of "username@server".</span></span> <span data-ttu-id="e7e30-135">請改為只使用 "username"。</span><span class="sxs-lookup"><span data-stu-id="e7e30-135">Instead, just use "username".</span></span>  <span data-ttu-id="e7e30-136">另請注意，連接字串不包含伺服器名稱和資料庫名稱。</span><span class="sxs-lookup"><span data-stu-id="e7e30-136">Also note that the connection string does not contain a server name and database name.</span></span> <span data-ttu-id="e7e30-137">這是因為 **OpenConnectionForKey** 呼叫會根據索引鍵自動將連接導向至正確的分區。</span><span class="sxs-lookup"><span data-stu-id="e7e30-137">That is because the **OpenConnectionForKey** call will automatically direct the connection to the correct shard based on the key.</span></span> <span data-ttu-id="e7e30-138">因此，不會提供資料庫名稱和伺服器名稱。</span><span class="sxs-lookup"><span data-stu-id="e7e30-138">Hence, the database name and server name are not provided.</span></span> 

## <a name="see-also"></a><span data-ttu-id="e7e30-139">另請參閱</span><span class="sxs-lookup"><span data-stu-id="e7e30-139">See also</span></span>
[<span data-ttu-id="e7e30-140">管理 Azure SQL Database 的資料庫和登入</span><span class="sxs-lookup"><span data-stu-id="e7e30-140">Managing databases and logins in Azure SQL Database</span></span>](sql-database-manage-logins.md)

[<span data-ttu-id="e7e30-141">保護您的 SQL Database</span><span class="sxs-lookup"><span data-stu-id="e7e30-141">Securing your SQL Database</span></span>](sql-database-security-overview.md)

[<span data-ttu-id="e7e30-142">開始使用彈性資料庫工作</span><span class="sxs-lookup"><span data-stu-id="e7e30-142">Getting started with Elastic Database jobs</span></span>](sql-database-elastic-jobs-getting-started.md)

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

