---
title: "hello 彈性資料庫用戶端程式庫中的 aaaManaging 認證 |Microsoft 文件"
description: "如何 tooset hello 正確等級的認證，tooread 僅限彈性資料庫應用程式的系統管理員"
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
ms.openlocfilehash: 218783ca2a07e3c0a4b089aa92634f32c41386e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="credentials-used-tooaccess-hello-elastic-database-client-library"></a><span data-ttu-id="186cd-103">使用 tooaccess hello 彈性資料庫用戶端程式庫的認證。</span><span class="sxs-lookup"><span data-stu-id="186cd-103">Credentials used tooaccess hello Elastic Database client library</span></span>
<span data-ttu-id="186cd-104">hello[彈性資料庫用戶端程式庫](http://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/)使用三種不同的認證 tooaccess hello[分區對應管理員](sql-database-elastic-scale-shard-map-management.md)。</span><span class="sxs-lookup"><span data-stu-id="186cd-104">hello [Elastic Database client library](http://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/) uses three different kinds  of credentials tooaccess hello [shard map manager](sql-database-elastic-scale-shard-map-management.md).</span></span> <span data-ttu-id="186cd-105">根據 hello 需要使用 hello 認證與 hello 存取可能的最低層級。</span><span class="sxs-lookup"><span data-stu-id="186cd-105">Depending on hello need, use hello credential with  hello lowest level of access possible.</span></span>

* <span data-ttu-id="186cd-106">**管理認證**：建立或操作分區對應管理員。</span><span class="sxs-lookup"><span data-stu-id="186cd-106">**Management credentials**: for creating or manipulating a shard map manager.</span></span> <span data-ttu-id="186cd-107">(請參閱 hello[詞彙](sql-database-elastic-scale-glossary.md)。)</span><span class="sxs-lookup"><span data-stu-id="186cd-107">(See hello [glossary](sql-database-elastic-scale-glossary.md).)</span></span> 
* <span data-ttu-id="186cd-108">**存取認證**: tooaccess 現有的分區對應管理員 tooobtain 資訊分區。</span><span class="sxs-lookup"><span data-stu-id="186cd-108">**Access credentials**: tooaccess an existing shard map manager tooobtain information about shards.</span></span>
* <span data-ttu-id="186cd-109">**連接認證**: tooconnect tooshards。</span><span class="sxs-lookup"><span data-stu-id="186cd-109">**Connection credentials**: tooconnect tooshards.</span></span> 

<span data-ttu-id="186cd-110">另請參閱 [在 Azure SQL Database 中管理資料庫與登入](sql-database-manage-logins.md)。</span><span class="sxs-lookup"><span data-stu-id="186cd-110">See also [Managing databases and logins in Azure SQL Database](sql-database-manage-logins.md).</span></span> 

## <a name="about-management-credentials"></a><span data-ttu-id="186cd-111">關於管理認證</span><span class="sxs-lookup"><span data-stu-id="186cd-111">About management credentials</span></span>
<span data-ttu-id="186cd-112">管理憑證是使用的 toocreate [ **ShardMapManager** ](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.aspx)操作分區對應的應用程式的物件。</span><span class="sxs-lookup"><span data-stu-id="186cd-112">Management credentials are used toocreate a [**ShardMapManager**](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.aspx) object for applications that manipulate shard maps.</span></span> <span data-ttu-id="186cd-113">(例如，請參閱[新增分區使用彈性資料庫工具](sql-database-elastic-scale-add-a-shard.md)和[資料依存路由](sql-database-elastic-scale-data-dependent-routing.md)) hello 彈性延展用戶端程式庫的 hello 使用者建立 hello SQL 使用者與 SQL 登入，並可確保每一個都是授與 hello 讀取/寫入權限 hello 全域分區對應資料庫及所有分區資料庫以及。</span><span class="sxs-lookup"><span data-stu-id="186cd-113">(For example, see [Adding a shard using Elastic Database tools](sql-database-elastic-scale-add-a-shard.md) and [Data dependent routing](sql-database-elastic-scale-data-dependent-routing.md)) hello user of hello elastic scale client library creates hello SQL users and SQL logins and makes sure each is granted hello read/write permissions on hello global shard map database and all shard databases as well.</span></span> <span data-ttu-id="186cd-114">在執行變更 toohello 分區對應時，這些認證會為使用的 toomaintain hello 全域分區對應與 hello 本機分區對應。</span><span class="sxs-lookup"><span data-stu-id="186cd-114">These credentials are used toomaintain hello global shard map and hello local shard maps when changes toohello shard map are performed.</span></span> <span data-ttu-id="186cd-115">例如，使用 hello 管理認證 toocreate hello 分區對應管理員物件 (使用[ **GetSqlShardMapManager**](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.getsqlshardmapmanager.aspx):</span><span class="sxs-lookup"><span data-stu-id="186cd-115">For instance, use hello management credentials toocreate hello shard map manager object (using [**GetSqlShardMapManager**](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.getsqlshardmapmanager.aspx):</span></span> 

    // Obtain a shard map manager. 
    ShardMapManager shardMapManager = ShardMapManagerFactory.GetSqlShardMapManager( 
            smmAdminConnectionString, 
            ShardMapManagerLoadPolicy.Lazy 
    ); 

<span data-ttu-id="186cd-116">hello 變數**smmAdminConnectionString**是包含 hello 管理認證的連接字串。</span><span class="sxs-lookup"><span data-stu-id="186cd-116">hello variable **smmAdminConnectionString** is a connection string that contains hello management credentials.</span></span> <span data-ttu-id="186cd-117">hello 使用者識別碼和密碼提供讀取/寫入存取 tooboth 分區對應資料庫和個別分區。</span><span class="sxs-lookup"><span data-stu-id="186cd-117">hello user ID and password provides read/write access tooboth shard map database and individual shards.</span></span> <span data-ttu-id="186cd-118">hello 管理連接字串也包含 hello 伺服器名稱和資料庫名稱 tooidentify hello 全域分區對應資料庫。</span><span class="sxs-lookup"><span data-stu-id="186cd-118">hello management connection string also includes hello server name and database name tooidentify hello global shard map database.</span></span> <span data-ttu-id="186cd-119">以下是針對該用途的一般連接字串：</span><span class="sxs-lookup"><span data-stu-id="186cd-119">Here is a typical connection string for that purpose:</span></span>

     "Server=<yourserver>.database.windows.net;Database=<yourdatabase>;User ID=<yourmgmtusername>;Password=<yourmgmtpassword>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30;” 

<span data-ttu-id="186cd-120">請勿使用 hello 形式的值"username@server"— 改為使用 hello"username"值。</span><span class="sxs-lookup"><span data-stu-id="186cd-120">Do not use values in hello form of "username@server"—instead just use hello "username" value.</span></span>  <span data-ttu-id="186cd-121">這是因為認證必須針對 hello 分區對應管理員資料庫及個別分區，可能會在不同伺服器作用。</span><span class="sxs-lookup"><span data-stu-id="186cd-121">This is because credentials must work against both hello shard map manager database and individual shards, which may be on different servers.</span></span>

## <a name="access-credentials"></a><span data-ttu-id="186cd-122">存取認證</span><span class="sxs-lookup"><span data-stu-id="186cd-122">Access credentials</span></span>
<span data-ttu-id="186cd-123">建立時分區對應管理員無法管理分區對應的應用程式中，使用在 hello 全域分區對應具有唯讀權限的認證。</span><span class="sxs-lookup"><span data-stu-id="186cd-123">When creating a shard map manager in an application that does not administer shard maps, use credentials that have read-only permissions on hello global shard map.</span></span> <span data-ttu-id="186cd-124">hello hello 全域分區對應，這些認證從擷取的資訊會用於[資料依存路由](sql-database-elastic-scale-data-dependent-routing.md)和 toopopulate hello 分區對應 hello 用戶端上的快取。</span><span class="sxs-lookup"><span data-stu-id="186cd-124">hello information retrieved from hello global shard map under these credentials are used for [data-dependent routing](sql-database-elastic-scale-data-dependent-routing.md) and toopopulate hello shard map cache on hello client.</span></span> <span data-ttu-id="186cd-125">hello 認證係透過 hello 相同呼叫模式太**GetSqlShardMapManager**如上所示：</span><span class="sxs-lookup"><span data-stu-id="186cd-125">hello credentials are provided through hello same call pattern too**GetSqlShardMapManager** as shown above:</span></span> 

    // Obtain shard map manager. 
    ShardMapManager shardMapManager = ShardMapManagerFactory.GetSqlShardMapManager( 
            smmReadOnlyConnectionString, 
            ShardMapManagerLoadPolicy.Lazy
    );  

<span data-ttu-id="186cd-126">請記下的 hello hello 使用**smmReadOnlyConnectionString** tooreflect hello 使用不同的認證進行這項存取代表**非系統管理員**使用者： 這些認證不應提供寫入hello 全域分區對應的權限。</span><span class="sxs-lookup"><span data-stu-id="186cd-126">Note hello use of hello **smmReadOnlyConnectionString** tooreflect hello use of different credentials for this access on behalf of **non-admin** users: these credentials should not provide write permissions on hello global shard map.</span></span> 

## <a name="connection-credentials"></a><span data-ttu-id="186cd-127">連接認證</span><span class="sxs-lookup"><span data-stu-id="186cd-127">Connection credentials</span></span>
<span data-ttu-id="186cd-128">當使用 hello 時，需要額外的認證[ **OpenConnectionForKey** ](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.openconnectionforkey.aspx)方法 tooaccess 分區，分區化索引鍵相關聯。</span><span class="sxs-lookup"><span data-stu-id="186cd-128">Additional credentials are needed when using hello [**OpenConnectionForKey**](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.openconnectionforkey.aspx) method tooaccess a shard associated with a sharding key.</span></span> <span data-ttu-id="186cd-129">這些認證需要唯讀存取 toohello 本機分區對應資料表位於 hello 分區 tooprovide 權限。</span><span class="sxs-lookup"><span data-stu-id="186cd-129">These credentials need tooprovide permissions for read-only access toohello local shard map tables residing on hello shard.</span></span> <span data-ttu-id="186cd-130">這是資料依存路由上 hello 分區所需的 tooperform 連線驗證。</span><span class="sxs-lookup"><span data-stu-id="186cd-130">This is needed tooperform connection validation for data-dependent routing on hello shard.</span></span> <span data-ttu-id="186cd-131">此程式碼片段資料依存路由 hello 內容中允許的資料存取：</span><span class="sxs-lookup"><span data-stu-id="186cd-131">This code snippet allows data access in hello context of data dependent routing:</span></span> 

    using (SqlConnection conn = rangeMap.OpenConnectionForKey<int>( 
    targetWarehouse, smmUserConnectionString, ConnectionOptions.Validate)) 

<span data-ttu-id="186cd-132">在此範例中， **smmUserConnectionString**保存 hello 連接字串 hello 使用者認證。</span><span class="sxs-lookup"><span data-stu-id="186cd-132">In this example, **smmUserConnectionString** holds hello connection string for hello user credentials.</span></span> <span data-ttu-id="186cd-133">在 Azure SQL DB 中，以下是使用者認證的一般連接字串：</span><span class="sxs-lookup"><span data-stu-id="186cd-133">For Azure SQL DB, here is a typical connection string for user credentials:</span></span> 

    "User ID=<yourusername>; Password=<youruserpassword>; Trusted_Connection=False; Encrypt=True; Connection Timeout=30;”  

<span data-ttu-id="186cd-134">Hello 形式不執行值如同 hello 系統管理員認證，「username@server"。</span><span class="sxs-lookup"><span data-stu-id="186cd-134">As with hello admin credentials, do not values in hello form of "username@server".</span></span> <span data-ttu-id="186cd-135">請改為只使用 "username"。</span><span class="sxs-lookup"><span data-stu-id="186cd-135">Instead, just use "username".</span></span>  <span data-ttu-id="186cd-136">也請注意，hello 連接字串不包含伺服器名稱和資料庫名稱。</span><span class="sxs-lookup"><span data-stu-id="186cd-136">Also note that hello connection string does not contain a server name and database name.</span></span> <span data-ttu-id="186cd-137">這是因為 hello **OpenConnectionForKey**呼叫會將自動導向 hello 連接 toohello 正確 hello 索引鍵為基礎的分區。</span><span class="sxs-lookup"><span data-stu-id="186cd-137">That is because hello **OpenConnectionForKey** call will automatically direct hello connection toohello correct shard based on hello key.</span></span> <span data-ttu-id="186cd-138">因此，並未提供 hello 資料庫名稱和伺服器名稱。</span><span class="sxs-lookup"><span data-stu-id="186cd-138">Hence, hello database name and server name are not provided.</span></span> 

## <a name="see-also"></a><span data-ttu-id="186cd-139">另請參閱</span><span class="sxs-lookup"><span data-stu-id="186cd-139">See also</span></span>
[<span data-ttu-id="186cd-140">管理 Azure SQL Database 的資料庫和登入</span><span class="sxs-lookup"><span data-stu-id="186cd-140">Managing databases and logins in Azure SQL Database</span></span>](sql-database-manage-logins.md)

[<span data-ttu-id="186cd-141">保護您的 SQL Database</span><span class="sxs-lookup"><span data-stu-id="186cd-141">Securing your SQL Database</span></span>](sql-database-security-overview.md)

[<span data-ttu-id="186cd-142">開始使用彈性資料庫工作</span><span class="sxs-lookup"><span data-stu-id="186cd-142">Getting started with Elastic Database jobs</span></span>](sql-database-elastic-jobs-getting-started.md)

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

