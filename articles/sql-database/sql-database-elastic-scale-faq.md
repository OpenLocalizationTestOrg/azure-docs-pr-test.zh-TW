---
title: "aaaAzure SQL 彈性延展常見問題集 |Microsoft 文件"
description: "有關 Azure SQL Database 彈性延展的常見問題集。"
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: e60dde9c-bb7b-4f2f-b52c-bdb506d49fcb
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: 8c77902e8ce9cbbc5e081cd9d2c911d4c8dc9e5f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="elastic-database-tools-faq"></a>彈性資料庫工具常見問題集
#### <a name="if-i-have-a-single-tenant-per-shard-and-no-sharding-key-how-do-i-populate-hello-sharding-key-for-hello-schema-info"></a>如果我有單一租用戶每個分區和任何分區化索引鍵時，我要如何填入 hello hello 結構描述資訊的分區化索引鍵？
hello 結構描述資訊的物件是使用的 toosplit 合併案例。 如果應用程式原本就是單一租用戶，然後不需要 hello 分割的合併工具，並因此沒有需要 toopopulate hello 結構描述資訊物件。

#### <a name="ive-provisioned-a-database-and-i-already-have-a-shard-map-manager-how-do-i-register-this-new-database-as-a-shard"></a>我已佈建資料庫並已擁有分區對應管理員，要如何將這個新資料庫註冊為分區？
請參閱**[新增分區 tooan 應用程式使用 hello 彈性資料庫用戶端程式庫](sql-database-elastic-scale-add-a-shard.md)**。 

#### <a name="how-much-do-elastic-database-tools-cost"></a>使用彈性資料庫的成本要多少？
使用 hello 彈性資料庫用戶端程式庫不會產生任何費用。 只針對 hello Azure SQL database 用於分區與 hello 分區對應管理員，以及您佈建 hello 分割的合併工具 hello web/背景工作角色，都會產生成本。

#### <a name="why-are-my-credentials-not-working-when-i-add-a-shard-from-a-different-server"></a>為什麼從其他伺服器新增分區時我的認證無法使用？
Hello 形式不使用認證 」 使用者 ID =username@servername"，改為只使用 「 使用者識別碼 = 使用者名稱 」。  此外，請確定該 hello"username"登入對 hello 分區的權限。

#### <a name="do-i-need-toocreate-a-shard-map-manager-and-populate-shards-every-time-i-start-my-applications"></a>我需要 toocreate 分區對應管理員及填入分區，每次啟動我的應用程式？
否-hello hello 分區對應管理員建立 (例如，  **[ShardMapManagerFactory.CreateSqlShardMapManager](http://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.createsqlshardmapmanager.aspx)**) 是一次性的操作。  您的應用程式應該使用 hello 呼叫 **[ShardMapManagerFactory.TryGetSqlShardMapManager()](http://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.trygetsqlshardmapmanager.aspx)** 在應用程式啟動時間。  每一應用程式網域應只有一個這類呼叫。

#### <a name="i-have-questions-about-using-elastic-database-tools-how-do-i-get-them-answered"></a>我有關於使用彈性資料庫工具的疑問，要如何尋求解答？
請聯繫 toous 上 hello [Azure SQL Database 論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=ssdsgetstarted)。

#### <a name="when-i-get-a-database-connection-using-a-sharding-key-i-can-still-query-data-for-other-sharding-keys-on-hello-same-shard--is-this-by-design"></a>當取得資料庫連接使用分區化索引鍵時，我還是可以查詢資料其他分區化索引鍵上 hello 相同分區。  這是原先的設計嗎？
hello Elastic Scale Api 讓您連接 toohello 正確的資料庫分區化索引鍵，但不是提供分區化索引鍵的篩選。  新增**其中**子句 tooyour 查詢 toorestrict hello 範圍 toohello 會提供分區化索引鍵，如有必要。

#### <a name="can-i-use-a-different-azure-database-edition-for-each-shard-in-my-shard-set"></a>我可以在分區集中針對個別的分區使用不同的 Azure Database 版本嗎？
可以，分區是個別的資料庫，因此可以有一個分區是「高階」版，另一個是「標準」版。 此外，分區 hello 版本可以多次 hello 分區 hello 存留期間相應增加或減少。

#### <a name="does-hello-split-merge-tool-provision-or-delete-a-database-during-a-split-or-merge-operation"></a>Hello 分割合併工具佈建 （或刪除） 分割或合併作業期間的資料庫？
否。 如**分割**作業 hello 目標資料庫必須存在於與 hello 適當的結構描述及向 hello 分區對應管理員。  如**合併**作業，您必須從 hello 分區對應管理員刪除 hello 分區，然後再刪除 hello 資料庫。

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

