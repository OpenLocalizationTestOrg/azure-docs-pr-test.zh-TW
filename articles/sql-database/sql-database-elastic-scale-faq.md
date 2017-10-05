---
title: "Azure SQL Elastic Scale 常見問題集 | Microsoft Docs"
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
ms.openlocfilehash: f0a7b5ce61feaead608d457465f64813737fa112
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="elastic-database-tools-faq"></a><span data-ttu-id="953b0-103">彈性資料庫工具常見問題集</span><span class="sxs-lookup"><span data-stu-id="953b0-103">Elastic database tools FAQ</span></span>
#### <a name="if-i-have-a-single-tenant-per-shard-and-no-sharding-key-how-do-i-populate-the-sharding-key-for-the-schema-info"></a><span data-ttu-id="953b0-104">如果我的每一分區各有單一租用戶，卻沒有分區化索引鍵，我要如何填入結構描述資訊的分區化索引鍵？</span><span class="sxs-lookup"><span data-stu-id="953b0-104">If I have a single-tenant per shard and no sharding key, how do I populate the sharding key for the schema info?</span></span>
<span data-ttu-id="953b0-105">結構描述資訊物件只是用來分割合併案例。</span><span class="sxs-lookup"><span data-stu-id="953b0-105">The schema info object is only used to split merge scenarios.</span></span> <span data-ttu-id="953b0-106">如果應用程式原本就是單一租用戶，則其並不需要分割合併工具，因此就不需要填入結構描述資訊物件。</span><span class="sxs-lookup"><span data-stu-id="953b0-106">If an application is inherently single-tenant, then it does not require the Split Merge tool and thus there is no need to populate the schema info object.</span></span>

#### <a name="ive-provisioned-a-database-and-i-already-have-a-shard-map-manager-how-do-i-register-this-new-database-as-a-shard"></a><span data-ttu-id="953b0-107">我已佈建資料庫並已擁有分區對應管理員，要如何將這個新資料庫註冊為分區？</span><span class="sxs-lookup"><span data-stu-id="953b0-107">I’ve provisioned a database and I already have a Shard Map Manager, how do I register this new database as a shard?</span></span>
<span data-ttu-id="953b0-108">請參閱**[用彈性資料庫用戶端程式庫新增分區到應用程式](sql-database-elastic-scale-add-a-shard.md)**。</span><span class="sxs-lookup"><span data-stu-id="953b0-108">Please see **[Adding a shard to an application using the elastic database client library](sql-database-elastic-scale-add-a-shard.md)**.</span></span> 

#### <a name="how-much-do-elastic-database-tools-cost"></a><span data-ttu-id="953b0-109">使用彈性資料庫的成本要多少？</span><span class="sxs-lookup"><span data-stu-id="953b0-109">How much do elastic database tools cost?</span></span>
<span data-ttu-id="953b0-110">使用彈性資料庫用戶端程式庫不會產生任何成本。</span><span class="sxs-lookup"><span data-stu-id="953b0-110">Using the elastic database client library does not incur any costs.</span></span> <span data-ttu-id="953b0-111">只有您使用於分區和分區對應管理員的 Azure SQL Database 和您為分割合併工具佈建的 Web/背景工作角色才會產生成本。</span><span class="sxs-lookup"><span data-stu-id="953b0-111">Costs accrue only for the Azure SQL databases that you use for shards and the Shard Map Manager, as well as the web/worker roles you provision for the Split Merge tool.</span></span>

#### <a name="why-are-my-credentials-not-working-when-i-add-a-shard-from-a-different-server"></a><span data-ttu-id="953b0-112">為什麼從其他伺服器新增分區時我的認證無法使用？</span><span class="sxs-lookup"><span data-stu-id="953b0-112">Why are my credentials not working when I add a shard from a different server?</span></span>
<span data-ttu-id="953b0-113">不使用認證的形式 」 使用者 ID =username@servername"，改為只使用 「 使用者識別碼 = 使用者名稱 」。</span><span class="sxs-lookup"><span data-stu-id="953b0-113">Do not use credentials in the form of “User ID=username@servername”, instead simply use “User ID = username”.</span></span>  <span data-ttu-id="953b0-114">此外，請確認 "username" 登入擁有分區的權限。</span><span class="sxs-lookup"><span data-stu-id="953b0-114">Also, be sure that the “username” login has permissions on the shard.</span></span>

#### <a name="do-i-need-to-create-a-shard-map-manager-and-populate-shards-every-time-i-start-my-applications"></a><span data-ttu-id="953b0-115">每次啟動應用程式，都必須建立分區對應管理員和填入分區嗎？</span><span class="sxs-lookup"><span data-stu-id="953b0-115">Do I need to create a Shard Map Manager and populate shards every time I start my applications?</span></span>
<span data-ttu-id="953b0-116">否，建立分區對應管理員 (例如，**[ShardMapManagerFactory.CreateSqlShardMapManager](http://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.createsqlshardmapmanager.aspx)**) 是一次性作業。</span><span class="sxs-lookup"><span data-stu-id="953b0-116">No—the creation of the Shard Map Manager (for example, **[ShardMapManagerFactory.CreateSqlShardMapManager](http://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.createsqlshardmapmanager.aspx)**) is a one-time operation.</span></span>  <span data-ttu-id="953b0-117">您的應用程式應在應用程式啟動時使用 **[ShardMapManagerFactory.TryGetSqlShardMapManager()](http://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.trygetsqlshardmapmanager.aspx)** 呼叫。</span><span class="sxs-lookup"><span data-stu-id="953b0-117">Your application should use the call **[ShardMapManagerFactory.TryGetSqlShardMapManager()](http://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.trygetsqlshardmapmanager.aspx)** at application start-up time.</span></span>  <span data-ttu-id="953b0-118">每一應用程式網域應只有一個這類呼叫。</span><span class="sxs-lookup"><span data-stu-id="953b0-118">There should only one such call per application domain.</span></span>

#### <a name="i-have-questions-about-using-elastic-database-tools-how-do-i-get-them-answered"></a><span data-ttu-id="953b0-119">我有關於使用彈性資料庫工具的疑問，要如何尋求解答？</span><span class="sxs-lookup"><span data-stu-id="953b0-119">I have questions about using elastic database tools, how do I get them answered?</span></span>
<span data-ttu-id="953b0-120">請在 [Azure SQL Database 論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=ssdsgetstarted)上與我們聯繫。</span><span class="sxs-lookup"><span data-stu-id="953b0-120">Please reach out to us on the [Azure SQL Database forum](https://social.msdn.microsoft.com/forums/azure/home?forum=ssdsgetstarted).</span></span>

#### <a name="when-i-get-a-database-connection-using-a-sharding-key-i-can-still-query-data-for-other-sharding-keys-on-the-same-shard--is-this-by-design"></a><span data-ttu-id="953b0-121">當我使用分區化索引鍵連接資料庫時，我仍然可以在相同的分區上查詢其他分區化索引鍵的資料。</span><span class="sxs-lookup"><span data-stu-id="953b0-121">When I get a database connection using a sharding key, I can still query data for other sharding keys on the same shard.</span></span>  <span data-ttu-id="953b0-122">這是原先的設計嗎？</span><span class="sxs-lookup"><span data-stu-id="953b0-122">Is this by design?</span></span>
<span data-ttu-id="953b0-123">彈性延展 API 可讓您針對分區化索引鍵連接至正確的資料庫，但是不提供分區化索引鍵篩選。</span><span class="sxs-lookup"><span data-stu-id="953b0-123">The Elastic Scale APIs give you a connection to the correct database for your sharding key, but do not provide sharding key filtering.</span></span>  <span data-ttu-id="953b0-124">如有必要，請新增 **WHERE** 子句到您的查詢，以將範圍限制在提供的分區化索引鍵。</span><span class="sxs-lookup"><span data-stu-id="953b0-124">Add **WHERE** clauses to your query to restrict the scope to the provided sharding key, if necessary.</span></span>

#### <a name="can-i-use-a-different-azure-database-edition-for-each-shard-in-my-shard-set"></a><span data-ttu-id="953b0-125">我可以在分區集中針對個別的分區使用不同的 Azure Database 版本嗎？</span><span class="sxs-lookup"><span data-stu-id="953b0-125">Can I use a different Azure Database edition for each shard in my shard set?</span></span>
<span data-ttu-id="953b0-126">可以，分區是個別的資料庫，因此可以有一個分區是「高階」版，另一個是「標準」版。</span><span class="sxs-lookup"><span data-stu-id="953b0-126">Yes, a shard is an individual database, and thus one shard could be a Premium edition while another be a Standard edition.</span></span> <span data-ttu-id="953b0-127">此外，在分區存留期間，分區的版本可以多次相應增加或相應減少。</span><span class="sxs-lookup"><span data-stu-id="953b0-127">Further, the edition of a shard can scale up or down multiple times during the lifetime of the shard.</span></span>

#### <a name="does-the-split-merge-tool-provision-or-delete-a-database-during-a-split-or-merge-operation"></a><span data-ttu-id="953b0-128">分割合併工具會在分割或合併作業期間佈建 (或刪除) 資料庫嗎？</span><span class="sxs-lookup"><span data-stu-id="953b0-128">Does the Split Merge tool provision (or delete) a database during a split or merge operation?</span></span>
<span data-ttu-id="953b0-129">不會。</span><span class="sxs-lookup"><span data-stu-id="953b0-129">No.</span></span> <span data-ttu-id="953b0-130">如果是「分割」  作業，目標資料庫必須有適當的結構描述，而且必須向分區對應管理員登錄。</span><span class="sxs-lookup"><span data-stu-id="953b0-130">For **split** operations, the target database must exist with the appropriate schema and be registered with the Shard Map Manager.</span></span>  <span data-ttu-id="953b0-131">如果是「合併」  作業，您必須從分區對應管理員刪除分區，然後再刪除資料庫。</span><span class="sxs-lookup"><span data-stu-id="953b0-131">For **merge** operations, you must delete the shard from the shard map manager and then delete the database.</span></span>

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

