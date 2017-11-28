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
# <a name="elastic-database-tools-faq"></a><span data-ttu-id="05a1e-103">彈性資料庫工具常見問題集</span><span class="sxs-lookup"><span data-stu-id="05a1e-103">Elastic database tools FAQ</span></span>
#### <a name="if-i-have-a-single-tenant-per-shard-and-no-sharding-key-how-do-i-populate-hello-sharding-key-for-hello-schema-info"></a><span data-ttu-id="05a1e-104">如果我有單一租用戶每個分區和任何分區化索引鍵時，我要如何填入 hello hello 結構描述資訊的分區化索引鍵？</span><span class="sxs-lookup"><span data-stu-id="05a1e-104">If I have a single-tenant per shard and no sharding key, how do I populate hello sharding key for hello schema info?</span></span>
<span data-ttu-id="05a1e-105">hello 結構描述資訊的物件是使用的 toosplit 合併案例。</span><span class="sxs-lookup"><span data-stu-id="05a1e-105">hello schema info object is only used toosplit merge scenarios.</span></span> <span data-ttu-id="05a1e-106">如果應用程式原本就是單一租用戶，然後不需要 hello 分割的合併工具，並因此沒有需要 toopopulate hello 結構描述資訊物件。</span><span class="sxs-lookup"><span data-stu-id="05a1e-106">If an application is inherently single-tenant, then it does not require hello Split Merge tool and thus there is no need toopopulate hello schema info object.</span></span>

#### <a name="ive-provisioned-a-database-and-i-already-have-a-shard-map-manager-how-do-i-register-this-new-database-as-a-shard"></a><span data-ttu-id="05a1e-107">我已佈建資料庫並已擁有分區對應管理員，要如何將這個新資料庫註冊為分區？</span><span class="sxs-lookup"><span data-stu-id="05a1e-107">I’ve provisioned a database and I already have a Shard Map Manager, how do I register this new database as a shard?</span></span>
<span data-ttu-id="05a1e-108">請參閱**[新增分區 tooan 應用程式使用 hello 彈性資料庫用戶端程式庫](sql-database-elastic-scale-add-a-shard.md)**。</span><span class="sxs-lookup"><span data-stu-id="05a1e-108">Please see **[Adding a shard tooan application using hello elastic database client library](sql-database-elastic-scale-add-a-shard.md)**.</span></span> 

#### <a name="how-much-do-elastic-database-tools-cost"></a><span data-ttu-id="05a1e-109">使用彈性資料庫的成本要多少？</span><span class="sxs-lookup"><span data-stu-id="05a1e-109">How much do elastic database tools cost?</span></span>
<span data-ttu-id="05a1e-110">使用 hello 彈性資料庫用戶端程式庫不會產生任何費用。</span><span class="sxs-lookup"><span data-stu-id="05a1e-110">Using hello elastic database client library does not incur any costs.</span></span> <span data-ttu-id="05a1e-111">只針對 hello Azure SQL database 用於分區與 hello 分區對應管理員，以及您佈建 hello 分割的合併工具 hello web/背景工作角色，都會產生成本。</span><span class="sxs-lookup"><span data-stu-id="05a1e-111">Costs accrue only for hello Azure SQL databases that you use for shards and hello Shard Map Manager, as well as hello web/worker roles you provision for hello Split Merge tool.</span></span>

#### <a name="why-are-my-credentials-not-working-when-i-add-a-shard-from-a-different-server"></a><span data-ttu-id="05a1e-112">為什麼從其他伺服器新增分區時我的認證無法使用？</span><span class="sxs-lookup"><span data-stu-id="05a1e-112">Why are my credentials not working when I add a shard from a different server?</span></span>
<span data-ttu-id="05a1e-113">Hello 形式不使用認證 」 使用者 ID =username@servername"，改為只使用 「 使用者識別碼 = 使用者名稱 」。</span><span class="sxs-lookup"><span data-stu-id="05a1e-113">Do not use credentials in hello form of “User ID=username@servername”, instead simply use “User ID = username”.</span></span>  <span data-ttu-id="05a1e-114">此外，請確定該 hello"username"登入對 hello 分區的權限。</span><span class="sxs-lookup"><span data-stu-id="05a1e-114">Also, be sure that hello “username” login has permissions on hello shard.</span></span>

#### <a name="do-i-need-toocreate-a-shard-map-manager-and-populate-shards-every-time-i-start-my-applications"></a><span data-ttu-id="05a1e-115">我需要 toocreate 分區對應管理員及填入分區，每次啟動我的應用程式？</span><span class="sxs-lookup"><span data-stu-id="05a1e-115">Do I need toocreate a Shard Map Manager and populate shards every time I start my applications?</span></span>
<span data-ttu-id="05a1e-116">否-hello hello 分區對應管理員建立 (例如，  **[ShardMapManagerFactory.CreateSqlShardMapManager](http://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.createsqlshardmapmanager.aspx)**) 是一次性的操作。</span><span class="sxs-lookup"><span data-stu-id="05a1e-116">No—hello creation of hello Shard Map Manager (for example, **[ShardMapManagerFactory.CreateSqlShardMapManager](http://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.createsqlshardmapmanager.aspx)**) is a one-time operation.</span></span>  <span data-ttu-id="05a1e-117">您的應用程式應該使用 hello 呼叫 **[ShardMapManagerFactory.TryGetSqlShardMapManager()](http://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.trygetsqlshardmapmanager.aspx)** 在應用程式啟動時間。</span><span class="sxs-lookup"><span data-stu-id="05a1e-117">Your application should use hello call **[ShardMapManagerFactory.TryGetSqlShardMapManager()](http://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.trygetsqlshardmapmanager.aspx)** at application start-up time.</span></span>  <span data-ttu-id="05a1e-118">每一應用程式網域應只有一個這類呼叫。</span><span class="sxs-lookup"><span data-stu-id="05a1e-118">There should only one such call per application domain.</span></span>

#### <a name="i-have-questions-about-using-elastic-database-tools-how-do-i-get-them-answered"></a><span data-ttu-id="05a1e-119">我有關於使用彈性資料庫工具的疑問，要如何尋求解答？</span><span class="sxs-lookup"><span data-stu-id="05a1e-119">I have questions about using elastic database tools, how do I get them answered?</span></span>
<span data-ttu-id="05a1e-120">請聯繫 toous 上 hello [Azure SQL Database 論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=ssdsgetstarted)。</span><span class="sxs-lookup"><span data-stu-id="05a1e-120">Please reach out toous on hello [Azure SQL Database forum](https://social.msdn.microsoft.com/forums/azure/home?forum=ssdsgetstarted).</span></span>

#### <a name="when-i-get-a-database-connection-using-a-sharding-key-i-can-still-query-data-for-other-sharding-keys-on-hello-same-shard--is-this-by-design"></a><span data-ttu-id="05a1e-121">當取得資料庫連接使用分區化索引鍵時，我還是可以查詢資料其他分區化索引鍵上 hello 相同分區。</span><span class="sxs-lookup"><span data-stu-id="05a1e-121">When I get a database connection using a sharding key, I can still query data for other sharding keys on hello same shard.</span></span>  <span data-ttu-id="05a1e-122">這是原先的設計嗎？</span><span class="sxs-lookup"><span data-stu-id="05a1e-122">Is this by design?</span></span>
<span data-ttu-id="05a1e-123">hello Elastic Scale Api 讓您連接 toohello 正確的資料庫分區化索引鍵，但不是提供分區化索引鍵的篩選。</span><span class="sxs-lookup"><span data-stu-id="05a1e-123">hello Elastic Scale APIs give you a connection toohello correct database for your sharding key, but do not provide sharding key filtering.</span></span>  <span data-ttu-id="05a1e-124">新增**其中**子句 tooyour 查詢 toorestrict hello 範圍 toohello 會提供分區化索引鍵，如有必要。</span><span class="sxs-lookup"><span data-stu-id="05a1e-124">Add **WHERE** clauses tooyour query toorestrict hello scope toohello provided sharding key, if necessary.</span></span>

#### <a name="can-i-use-a-different-azure-database-edition-for-each-shard-in-my-shard-set"></a><span data-ttu-id="05a1e-125">我可以在分區集中針對個別的分區使用不同的 Azure Database 版本嗎？</span><span class="sxs-lookup"><span data-stu-id="05a1e-125">Can I use a different Azure Database edition for each shard in my shard set?</span></span>
<span data-ttu-id="05a1e-126">可以，分區是個別的資料庫，因此可以有一個分區是「高階」版，另一個是「標準」版。</span><span class="sxs-lookup"><span data-stu-id="05a1e-126">Yes, a shard is an individual database, and thus one shard could be a Premium edition while another be a Standard edition.</span></span> <span data-ttu-id="05a1e-127">此外，分區 hello 版本可以多次 hello 分區 hello 存留期間相應增加或減少。</span><span class="sxs-lookup"><span data-stu-id="05a1e-127">Further, hello edition of a shard can scale up or down multiple times during hello lifetime of hello shard.</span></span>

#### <a name="does-hello-split-merge-tool-provision-or-delete-a-database-during-a-split-or-merge-operation"></a><span data-ttu-id="05a1e-128">Hello 分割合併工具佈建 （或刪除） 分割或合併作業期間的資料庫？</span><span class="sxs-lookup"><span data-stu-id="05a1e-128">Does hello Split Merge tool provision (or delete) a database during a split or merge operation?</span></span>
<span data-ttu-id="05a1e-129">否。</span><span class="sxs-lookup"><span data-stu-id="05a1e-129">No.</span></span> <span data-ttu-id="05a1e-130">如**分割**作業 hello 目標資料庫必須存在於與 hello 適當的結構描述及向 hello 分區對應管理員。</span><span class="sxs-lookup"><span data-stu-id="05a1e-130">For **split** operations, hello target database must exist with hello appropriate schema and be registered with hello Shard Map Manager.</span></span>  <span data-ttu-id="05a1e-131">如**合併**作業，您必須從 hello 分區對應管理員刪除 hello 分區，然後再刪除 hello 資料庫。</span><span class="sxs-lookup"><span data-stu-id="05a1e-131">For **merge** operations, you must delete hello shard from hello shard map manager and then delete hello database.</span></span>

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

