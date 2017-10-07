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
# <a name="credentials-used-tooaccess-hello-elastic-database-client-library"></a>使用 tooaccess hello 彈性資料庫用戶端程式庫的認證。
hello[彈性資料庫用戶端程式庫](http://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/)使用三種不同的認證 tooaccess hello[分區對應管理員](sql-database-elastic-scale-shard-map-management.md)。 根據 hello 需要使用 hello 認證與 hello 存取可能的最低層級。

* **管理認證**：建立或操作分區對應管理員。 (請參閱 hello[詞彙](sql-database-elastic-scale-glossary.md)。) 
* **存取認證**: tooaccess 現有的分區對應管理員 tooobtain 資訊分區。
* **連接認證**: tooconnect tooshards。 

另請參閱 [在 Azure SQL Database 中管理資料庫與登入](sql-database-manage-logins.md)。 

## <a name="about-management-credentials"></a>關於管理認證
管理憑證是使用的 toocreate [ **ShardMapManager** ](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.aspx)操作分區對應的應用程式的物件。 (例如，請參閱[新增分區使用彈性資料庫工具](sql-database-elastic-scale-add-a-shard.md)和[資料依存路由](sql-database-elastic-scale-data-dependent-routing.md)) hello 彈性延展用戶端程式庫的 hello 使用者建立 hello SQL 使用者與 SQL 登入，並可確保每一個都是授與 hello 讀取/寫入權限 hello 全域分區對應資料庫及所有分區資料庫以及。 在執行變更 toohello 分區對應時，這些認證會為使用的 toomaintain hello 全域分區對應與 hello 本機分區對應。 例如，使用 hello 管理認證 toocreate hello 分區對應管理員物件 (使用[ **GetSqlShardMapManager**](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.getsqlshardmapmanager.aspx): 

    // Obtain a shard map manager. 
    ShardMapManager shardMapManager = ShardMapManagerFactory.GetSqlShardMapManager( 
            smmAdminConnectionString, 
            ShardMapManagerLoadPolicy.Lazy 
    ); 

hello 變數**smmAdminConnectionString**是包含 hello 管理認證的連接字串。 hello 使用者識別碼和密碼提供讀取/寫入存取 tooboth 分區對應資料庫和個別分區。 hello 管理連接字串也包含 hello 伺服器名稱和資料庫名稱 tooidentify hello 全域分區對應資料庫。 以下是針對該用途的一般連接字串：

     "Server=<yourserver>.database.windows.net;Database=<yourdatabase>;User ID=<yourmgmtusername>;Password=<yourmgmtpassword>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30;” 

請勿使用 hello 形式的值"username@server"— 改為使用 hello"username"值。  這是因為認證必須針對 hello 分區對應管理員資料庫及個別分區，可能會在不同伺服器作用。

## <a name="access-credentials"></a>存取認證
建立時分區對應管理員無法管理分區對應的應用程式中，使用在 hello 全域分區對應具有唯讀權限的認證。 hello hello 全域分區對應，這些認證從擷取的資訊會用於[資料依存路由](sql-database-elastic-scale-data-dependent-routing.md)和 toopopulate hello 分區對應 hello 用戶端上的快取。 hello 認證係透過 hello 相同呼叫模式太**GetSqlShardMapManager**如上所示： 

    // Obtain shard map manager. 
    ShardMapManager shardMapManager = ShardMapManagerFactory.GetSqlShardMapManager( 
            smmReadOnlyConnectionString, 
            ShardMapManagerLoadPolicy.Lazy
    );  

請記下的 hello hello 使用**smmReadOnlyConnectionString** tooreflect hello 使用不同的認證進行這項存取代表**非系統管理員**使用者： 這些認證不應提供寫入hello 全域分區對應的權限。 

## <a name="connection-credentials"></a>連接認證
當使用 hello 時，需要額外的認證[ **OpenConnectionForKey** ](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.openconnectionforkey.aspx)方法 tooaccess 分區，分區化索引鍵相關聯。 這些認證需要唯讀存取 toohello 本機分區對應資料表位於 hello 分區 tooprovide 權限。 這是資料依存路由上 hello 分區所需的 tooperform 連線驗證。 此程式碼片段資料依存路由 hello 內容中允許的資料存取： 

    using (SqlConnection conn = rangeMap.OpenConnectionForKey<int>( 
    targetWarehouse, smmUserConnectionString, ConnectionOptions.Validate)) 

在此範例中， **smmUserConnectionString**保存 hello 連接字串 hello 使用者認證。 在 Azure SQL DB 中，以下是使用者認證的一般連接字串： 

    "User ID=<yourusername>; Password=<youruserpassword>; Trusted_Connection=False; Encrypt=True; Connection Timeout=30;”  

Hello 形式不執行值如同 hello 系統管理員認證，「username@server"。 請改為只使用 "username"。  也請注意，hello 連接字串不包含伺服器名稱和資料庫名稱。 這是因為 hello **OpenConnectionForKey**呼叫會將自動導向 hello 連接 toohello 正確 hello 索引鍵為基礎的分區。 因此，並未提供 hello 資料庫名稱和伺服器名稱。 

## <a name="see-also"></a>另請參閱
[管理 Azure SQL Database 的資料庫和登入](sql-database-manage-logins.md)

[保護您的 SQL Database](sql-database-security-overview.md)

[開始使用彈性資料庫工作](sql-database-elastic-jobs-getting-started.md)

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

