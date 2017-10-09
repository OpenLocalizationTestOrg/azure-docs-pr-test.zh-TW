---
title: "aaaSync 資料 （預覽） |Microsoft 文件"
description: "本概觀介紹 Azure SQL 資料同步 (預覽)。"
services: sql-database
documentationcenter: 
author: douglaslms
manager: craigg
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: load & move data
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: douglasl
ms.openlocfilehash: d5b2bbd6a502ba94dba7fb309a6583d2d95cc1d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="sync-data-across-multiple-cloud-and-on-premises-databases-with-sql-data-sync"></a><span data-ttu-id="e1b3b-103">使用 SQL 資料同步，跨多個雲端和內部部署資料庫同步資料</span><span class="sxs-lookup"><span data-stu-id="e1b3b-103">Sync data across multiple cloud and on-premises databases with SQL Data Sync</span></span>

<span data-ttu-id="e1b3b-104">SQL 資料同步處理是可讓您選取雙向跨多個 SQL database 和 SQL Server 執行個體的 hello 資料同步處理您的 Azure SQL Database 上建置的服務。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-104">SQL Data Sync is a service built on Azure SQL Database that lets you synchronize hello data you select bi-directionally across multiple SQL databases and SQL Server instances.</span></span>

<span data-ttu-id="e1b3b-105">資料同步會根據 hello 概念的同步處理群組。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-105">Data Sync is based around hello concept of a Sync Group.</span></span> <span data-ttu-id="e1b3b-106">同步處理群組是您想 toosynchronize 資料庫的群組。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-106">A Sync Group is a group of databases that you want toosynchronize.</span></span>

<span data-ttu-id="e1b3b-107">同步處理群組具有下列屬性的 hello:</span><span class="sxs-lookup"><span data-stu-id="e1b3b-107">A Sync Group has hello following properties:</span></span>

-   <span data-ttu-id="e1b3b-108">hello**同步處理結構描述**說明資料同步處理。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-108">hello **Sync Schema** describes which data is being synchronized.</span></span>

-   <span data-ttu-id="e1b3b-109">hello**同步處理方向**可以是雙向或可以只有一個方向流動。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-109">hello **Sync Direction** can be bi-directional or can flow in only one direction.</span></span> <span data-ttu-id="e1b3b-110">也就是說，可以是同步處理方向的 hello*中樞 tooMember*或*成員 tooHub*，或兩者。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-110">That is, hello Sync Direction can be *Hub tooMember* or *Member tooHub*, or both.</span></span>

-   <span data-ttu-id="e1b3b-111">hello**同步處理間隔**頻率進行同步處理。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-111">hello **Sync Interval** is how often synchronization occurs.</span></span>

-   <span data-ttu-id="e1b3b-112">hello**衝突解決原則**是群組層級原則，可以是*中樞獲勝*或*成員 wins*。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-112">hello **Conflict Resolution Policy** is a group level policy, which can be *Hub wins* or *Member wins*.</span></span>

<span data-ttu-id="e1b3b-113">資料同步會使用中樞和支點拓撲 toosynchronize 資料。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-113">Data Sync uses a hub and spoke topology toosynchronize data.</span></span> <span data-ttu-id="e1b3b-114">您定義的其中一個 hello 資料庫 hello 群組中為 hello 中樞資料庫。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-114">You define one of hello databases in hello group as hello Hub Database.</span></span> <span data-ttu-id="e1b3b-115">hello hello 資料庫其餘部分是成員資料庫。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-115">hello rest of hello databases are member databases.</span></span> <span data-ttu-id="e1b3b-116">只有之間 hello 中樞和個別成員進行同步處理。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-116">Sync occurs only between hello Hub and individual members.</span></span>
-   <span data-ttu-id="e1b3b-117">hello**中樞資料庫**必須是 Azure SQL Database。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-117">hello **Hub Database** must be an Azure SQL Database.</span></span>
-   <span data-ttu-id="e1b3b-118">hello**成員資料庫**可以是 SQL 資料庫、 在內部部署 SQL Server 資料庫或在 Azure 虛擬機器上的 SQL Server 執行個體。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-118">hello **member databases** can be either SQL Databases, on-premises SQL Server databases, or SQL Server instances on Azure virtual machines.</span></span>
-   <span data-ttu-id="e1b3b-119">hello**同步處理資料庫**包含 hello 中繼資料和記錄檔資料同步處理。 hello 同步處理資料庫有 toobe 位於 hello Azure SQL Database 與 hello 中樞資料庫相同的區域。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-119">hello **Sync Database** contains hello metadata and log for Data Sync. hello Sync Database has toobe an Azure SQL Database located in hello same region as hello Hub Database.</span></span> <span data-ttu-id="e1b3b-120">建立的客戶，而客戶擁有 hello 同步處理資料庫。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-120">hello Sync Database is customer created and customer owned.</span></span>

> [!NOTE]
> <span data-ttu-id="e1b3b-121">如果您使用上的內部部署資料庫，您有太[設定本機代理程式。](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-get-started-sql-data-sync)</span><span class="sxs-lookup"><span data-stu-id="e1b3b-121">If you're using an on premises database, you have too[configure a local agent.](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-get-started-sql-data-sync)</span></span>

![資料庫之間的同步資料](media/sql-database-sync-data/sync-data-overview.png)

## <a name="when-toouse-data-sync"></a><span data-ttu-id="e1b3b-123">當 toouse 資料同步處理</span><span class="sxs-lookup"><span data-stu-id="e1b3b-123">When toouse Data Sync</span></span>

<span data-ttu-id="e1b3b-124">資料同步處理是在需要資料 toobe 維持 toodate 最新狀態跨數個 Azure SQL Database 或 SQL Server 資料庫的情況下很有用。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-124">Data Sync is useful in cases where data needs toobe kept up toodate across several Azure SQL Databases or SQL Server databases.</span></span> <span data-ttu-id="e1b3b-125">以下是資料同步的 hello 主要的使用案例：</span><span class="sxs-lookup"><span data-stu-id="e1b3b-125">Here are hello main use cases for Data Sync:</span></span>

-   <span data-ttu-id="e1b3b-126">**混合式資料同步處理：**資料同步時，您可以保留在內部部署資料庫和 Azure SQL Database tooenable 混合式應用程式之間的同步處理的資料。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-126">**Hybrid Data Synchronization:** With Data Sync, you can keep data synchronized between your on-premises databases and Azure SQL Databases tooenable hybrid applications.</span></span> <span data-ttu-id="e1b3b-127">這項功能可能會吸引人考慮移動 toohello 雲端，而且想要 tooput toocustomers 他們在 Azure 中的應用程式部分。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-127">This capability may appeal toocustomers who are considering moving toohello cloud and would like tooput some of their application in Azure.</span></span>

-   <span data-ttu-id="e1b3b-128">**分散式應用程式：**在許多情況下，很有幫助 tooseparate 不同工作負載分散在不同的資料庫。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-128">**Distributed Applications:** In many cases, it's beneficial tooseparate different workloads across different databases.</span></span> <span data-ttu-id="e1b3b-129">例如，如果您有大型資料庫，但您也需要 toorun 報告或分析工作負載，此資料，很有幫助 toohave 此額外的工作負載的第二個資料庫。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-129">For example, if you have a large production database, but you also need toorun a reporting or analytics workload on this data, it's helpful toohave a second database for this additional workload.</span></span> <span data-ttu-id="e1b3b-130">這種方法 hello 對您的生產工作負載的效能影響降到最低。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-130">This approach minimizes hello performance impact on your production workload.</span></span> <span data-ttu-id="e1b3b-131">您可以使用這兩個資料庫同步處理的資料同步 tookeep。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-131">You can use Data Sync tookeep these two databases synchronized.</span></span>

-   <span data-ttu-id="e1b3b-132">**全域散發的應用程式：**許多企業的業務橫跨多個區域，甚至多個國家/地區。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-132">**Globally Distributed Applications:** Many businesses span several regions and even several countries.</span></span> <span data-ttu-id="e1b3b-133">toominimize 網路延遲，它會關閉您的資料區域中的最佳 toohave tooyou。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-133">toominimize network latency, it's best toohave your data in a region close tooyou.</span></span> <span data-ttu-id="e1b3b-134">資料同步時，您可以輕鬆地資料庫同步處理的 hello 世界各地的區域中。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-134">With Data Sync, you can easily keep databases in regions around hello world synchronized.</span></span>

<span data-ttu-id="e1b3b-135">我們不建議資料同步 hello 下列案例：</span><span class="sxs-lookup"><span data-stu-id="e1b3b-135">We don't recommend Data Sync for hello following scenarios:</span></span>

-   <span data-ttu-id="e1b3b-136">災害復原</span><span class="sxs-lookup"><span data-stu-id="e1b3b-136">Disaster Recovery</span></span>

-   <span data-ttu-id="e1b3b-137">讀取級別</span><span class="sxs-lookup"><span data-stu-id="e1b3b-137">Read Scale</span></span>

-   <span data-ttu-id="e1b3b-138">ETL (OLTP tooOLAP)</span><span class="sxs-lookup"><span data-stu-id="e1b3b-138">ETL (OLTP tooOLAP)</span></span>

-   <span data-ttu-id="e1b3b-139">從內部部署 SQL Server tooAzure SQL Database 移轉</span><span class="sxs-lookup"><span data-stu-id="e1b3b-139">Migration from on-premises SQL Server tooAzure SQL Database</span></span>

## <a name="how-does-data-sync-work"></a><span data-ttu-id="e1b3b-140">資料同步如何運作？</span><span class="sxs-lookup"><span data-stu-id="e1b3b-140">How does Data Sync work?</span></span> 

-   <span data-ttu-id="e1b3b-141">**追蹤資料變更：**資料同步使用 insert、update 和 delete 觸發程序追蹤變更。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-141">**Tracking data changes:** Data Sync tracks changes using insert, update, and delete triggers.</span></span> <span data-ttu-id="e1b3b-142">hello 變更會記錄在側邊資料表 hello 使用者資料庫中。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-142">hello changes are recorded in a side table in hello user database.</span></span>

-   <span data-ttu-id="e1b3b-143">**同步處理資料：**資料同步是以「中樞和輪輻」的模型設計。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-143">**Synchronizing data:** Data Sync is designed in a Hub and Spoke model.</span></span> <span data-ttu-id="e1b3b-144">個別 hello 與每個成員的中樞同步處理。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-144">hello Hub syncs with each member individually.</span></span> <span data-ttu-id="e1b3b-145">Hello 中樞的變更會下載的 toohello 成員，然後再從 hello 成員變更便會上載的 toohello 中樞。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-145">Changes from hello Hub are downloaded toohello member and then changes from hello member are uploaded toohello Hub.</span></span>

-   <span data-ttu-id="e1b3b-146">**解決衝突：**資料同步提供兩個衝突解決選項：*中樞獲勝*或*成員獲勝*。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-146">**Resolving conflicts:** Data Sync provides two options for conflict resolution, *Hub wins* or *Member wins*.</span></span>
    -   <span data-ttu-id="e1b3b-147">如果您選取*中樞獲勝*，hello 中樞中的 hello 變更一律會覆寫 hello 成員中的變更。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-147">If you select *Hub wins*, hello changes in hello hub always overwrite changes in hello member.</span></span>
    -   <span data-ttu-id="e1b3b-148">如果您選取*成員 wins*，hello hello 中樞中的 hello 成員覆寫變更的變更。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-148">If you select *Member wins*, hello changes in hello member overwrite changes in hello hub.</span></span> <span data-ttu-id="e1b3b-149">如果有多個成員，hello 最終值取決於哪一個成員是第一次同步。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-149">If there's more than one member, hello final value depends on which member syncs first.</span></span>

## <a name="limitations-and-considerations"></a><span data-ttu-id="e1b3b-150">限制與注意事項</span><span class="sxs-lookup"><span data-stu-id="e1b3b-150">Limitations and considerations</span></span>

### <a name="performance-impact"></a><span data-ttu-id="e1b3b-151">效能影響</span><span class="sxs-lookup"><span data-stu-id="e1b3b-151">Performance impact</span></span>
<span data-ttu-id="e1b3b-152">資料同步處理會使用插入、 更新和刪除觸發程序 tootrack 變更。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-152">Data Sync uses insert, update, and delete triggers tootrack changes.</span></span> <span data-ttu-id="e1b3b-153">它會變更追蹤的 hello 使用者資料庫中建立的側邊資料表。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-153">It creates side tables in hello user database for change tracking.</span></span> <span data-ttu-id="e1b3b-154">這些變更追蹤活動會影響您的資料庫工作負載。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-154">These change tracking activities have an impact on your database workload.</span></span> <span data-ttu-id="e1b3b-155">請評估您的服務層，如有必要則請升級。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-155">Assess your service tier and upgrade if needed.</span></span>

### <a name="eventual-consistency"></a><span data-ttu-id="e1b3b-156">最終一致性</span><span class="sxs-lookup"><span data-stu-id="e1b3b-156">Eventual consistency</span></span>
<span data-ttu-id="e1b3b-157">由於資料同步是以觸發程序為基礎，所以並不保證交易一致性。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-157">Since Data Sync is trigger-based, transactional consistency is not guaranteed.</span></span> <span data-ttu-id="e1b3b-158">Microsoft 保證最終會進行所有變更，而且資料同步不會造成資料遺失。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-158">Microsoft guarantees that all changes are made eventually and that Data Sync does not cause data loss.</span></span>

### <a name="unsupported-data-types"></a><span data-ttu-id="e1b3b-159">不支援的資料類型</span><span class="sxs-lookup"><span data-stu-id="e1b3b-159">Unsupported data types</span></span>

-   <span data-ttu-id="e1b3b-160">FileStream</span><span class="sxs-lookup"><span data-stu-id="e1b3b-160">FileStream</span></span>

-   <span data-ttu-id="e1b3b-161">SQL/CLR UDT</span><span class="sxs-lookup"><span data-stu-id="e1b3b-161">SQL/CLR UDT</span></span>

-   <span data-ttu-id="e1b3b-162">XMLSchemaCollection (支援 XML)</span><span class="sxs-lookup"><span data-stu-id="e1b3b-162">XMLSchemaCollection (XML supported)</span></span>

-   <span data-ttu-id="e1b3b-163">Cursor、Timestamp、Hierarchyid</span><span class="sxs-lookup"><span data-stu-id="e1b3b-163">Cursor, Timestamp, Hierarchyid</span></span>

### <a name="requirements"></a><span data-ttu-id="e1b3b-164">需求</span><span class="sxs-lookup"><span data-stu-id="e1b3b-164">Requirements</span></span>

-   <span data-ttu-id="e1b3b-165">每個資料表都必須有主索引鍵。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-165">Each table must have a primary key.</span></span>

-   <span data-ttu-id="e1b3b-166">資料表不能有不是 hello 主索引鍵的識別資料行。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-166">A table cannot have an identity column that is not hello primary key.</span></span>

-   <span data-ttu-id="e1b3b-167">hello 物件 （資料庫、 資料表和資料行） 名稱不能包含 hello 可列印字元句點 （.）、 左方括弧 ([])，或右方括弧 (])。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-167">hello names of objects (databases, tables, and columns) cannot contain hello printable characters period (.), left square bracket ([), or right square bracket (]).</span></span>

### <a name="limitations-on-service-and-database-dimensions"></a><span data-ttu-id="e1b3b-168">服務和資料庫維度的限制</span><span class="sxs-lookup"><span data-stu-id="e1b3b-168">Limitations on service and database dimensions</span></span>

|                                                                 |                        |                             |
|-----------------------------------------------------------------|------------------------|-----------------------------|
| <span data-ttu-id="e1b3b-169">**維度**</span><span class="sxs-lookup"><span data-stu-id="e1b3b-169">**Dimensions**</span></span>                                                      | <span data-ttu-id="e1b3b-170">**限制**</span><span class="sxs-lookup"><span data-stu-id="e1b3b-170">**Limit**</span></span>              | <span data-ttu-id="e1b3b-171">**因應措施**</span><span class="sxs-lookup"><span data-stu-id="e1b3b-171">**Workaround**</span></span>              |
| <span data-ttu-id="e1b3b-172">任何資料庫可以隸屬的同步群組數目上限。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-172">Maximum number of sync groups any database can belong to.</span></span>       | <span data-ttu-id="e1b3b-173">5</span><span class="sxs-lookup"><span data-stu-id="e1b3b-173">5</span></span>                      |                             |
| <span data-ttu-id="e1b3b-174">單一同步群組中的端點數目上限</span><span class="sxs-lookup"><span data-stu-id="e1b3b-174">Maximum number of endpoints in a single sync group</span></span>              | <span data-ttu-id="e1b3b-175">30</span><span class="sxs-lookup"><span data-stu-id="e1b3b-175">30</span></span>                     | <span data-ttu-id="e1b3b-176">建立多個同步群組</span><span class="sxs-lookup"><span data-stu-id="e1b3b-176">Create multiple sync groups</span></span> |
| <span data-ttu-id="e1b3b-177">單一同步群組中的內部部署端點數目上限。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-177">Maximum number of on-premises endpoints in a single sync group.</span></span> | <span data-ttu-id="e1b3b-178">5</span><span class="sxs-lookup"><span data-stu-id="e1b3b-178">5</span></span>                      | <span data-ttu-id="e1b3b-179">建立多個同步群組</span><span class="sxs-lookup"><span data-stu-id="e1b3b-179">Create multiple sync groups</span></span> |
| <span data-ttu-id="e1b3b-180">資料庫名稱、資料表名稱、結構描述名稱和資料行名稱</span><span class="sxs-lookup"><span data-stu-id="e1b3b-180">Database, table, schema, and column names</span></span>                       | <span data-ttu-id="e1b3b-181">每個名稱 50 個字元</span><span class="sxs-lookup"><span data-stu-id="e1b3b-181">50 characters per name</span></span> |                             |
| <span data-ttu-id="e1b3b-182">一個同步群組中的資料表</span><span class="sxs-lookup"><span data-stu-id="e1b3b-182">Tables in a sync group</span></span>                                          | <span data-ttu-id="e1b3b-183">500</span><span class="sxs-lookup"><span data-stu-id="e1b3b-183">500</span></span>                    | <span data-ttu-id="e1b3b-184">建立多個同步群組</span><span class="sxs-lookup"><span data-stu-id="e1b3b-184">Create multiple sync groups</span></span> |
| <span data-ttu-id="e1b3b-185">一個同步群組中一個資料表中的資料行</span><span class="sxs-lookup"><span data-stu-id="e1b3b-185">Columns in a table in a sync group</span></span>                              | <span data-ttu-id="e1b3b-186">1000</span><span class="sxs-lookup"><span data-stu-id="e1b3b-186">1000</span></span>                   |                             |
| <span data-ttu-id="e1b3b-187">一個資料表上的資料列大小</span><span class="sxs-lookup"><span data-stu-id="e1b3b-187">Data row size on a table</span></span>                                        | <span data-ttu-id="e1b3b-188">24 Mb</span><span class="sxs-lookup"><span data-stu-id="e1b3b-188">24 Mb</span></span>                  |                             |
| <span data-ttu-id="e1b3b-189">最小同步處理間隔</span><span class="sxs-lookup"><span data-stu-id="e1b3b-189">Minimum sync interval</span></span>                                           | <span data-ttu-id="e1b3b-190">5 分鐘</span><span class="sxs-lookup"><span data-stu-id="e1b3b-190">5 Minutes</span></span>              |                             |

## <a name="common-questions"></a><span data-ttu-id="e1b3b-191">常見問題</span><span class="sxs-lookup"><span data-stu-id="e1b3b-191">Common questions</span></span>

### <a name="how-frequently-can-data-sync-synchronize-my-data"></a><span data-ttu-id="e1b3b-192">資料同步多久會同步我的資料一次？</span><span class="sxs-lookup"><span data-stu-id="e1b3b-192">How frequently can Data Sync synchronize my data?</span></span> 
<span data-ttu-id="e1b3b-193">hello 的最小頻率為每隔五分鐘。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-193">hello minimum frequency is every five minutes.</span></span>

### <a name="can-i-use-data-sync-toosync-between-sql-server-on-premises-databases-only"></a><span data-ttu-id="e1b3b-194">可以使用 SQL Server 在內部部署資料庫只之間資料同步 toosync 嗎？</span><span class="sxs-lookup"><span data-stu-id="e1b3b-194">Can I use Data Sync toosync between SQL Server on-premises databases only?</span></span> 
<span data-ttu-id="e1b3b-195">無法直接進行。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-195">Not directly.</span></span> <span data-ttu-id="e1b3b-196">您可以同步處理 SQL Server 在內部部署資料庫之間間接，不過，在 Azure 中建立的中樞資料庫，然後將加入 hello 在內部部署資料庫 toohello 同步處理群組。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-196">You can sync between SQL Server on-premises databases indirectly, however, by creating a Hub database in Azure, and then adding hello on-premises databases toohello sync group.</span></span>
   
### <a name="can-i-use-data-sync-tooseed-data-from-my-production-database-tooan-empty-database-and-then-keep-them-synchronized"></a><span data-ttu-id="e1b3b-197">我可以使用資料同步 tooseed 資料從實際執行資料庫 tooan 空白資料庫，並再讓它們保持同步嗎？</span><span class="sxs-lookup"><span data-stu-id="e1b3b-197">Can I use Data Sync tooseed data from my production database tooan empty database, and then keep them synchronized?</span></span> 
<span data-ttu-id="e1b3b-198">是。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-198">Yes.</span></span> <span data-ttu-id="e1b3b-199">指令從原始的 hello hello 新資料庫中手動建立 hello 結構描述。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-199">Create hello schema manually in hello new database by scripting it from hello original.</span></span> <span data-ttu-id="e1b3b-200">建立 hello 結構描述之後，加入 hello 資料表 tooa 同步處理群組 toocopy hello 資料，並保持同步。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-200">After you create hello schema, add hello tables tooa sync group toocopy hello data and keep it synced.</span></span>

### <a name="why-do-i-see-tables-that-i-did-not-create"></a><span data-ttu-id="e1b3b-201">為什麼我會看到並非自己建立的資料表？</span><span class="sxs-lookup"><span data-stu-id="e1b3b-201">Why do I see tables that I did not create?</span></span>  
<span data-ttu-id="e1b3b-202">資料同步會在資料庫中建立側邊資料表，以便進行變更追蹤。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-202">Data Sync creates side tables in your database for change tracking.</span></span> <span data-ttu-id="e1b3b-203">請勿刪除它們，否則資料同步無法正常運作。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-203">Don't delete them or Data Sync stops working.</span></span>
   
### <a name="i-got-an-error-message-that-said-cannot-insert-hello-value-null-into-hello-column-column-column-does-not-allow-nulls-what-does-this-mean-and-how-can-i-fix-hello-error"></a><span data-ttu-id="e1b3b-204">我收到錯誤訊息: 「 無法將 NULL 值的 hello 插入 hello 資料行\<資料行\>。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-204">I got an error message that said "cannot insert hello value NULL into hello column \<column\>.</span></span> <span data-ttu-id="e1b3b-205">資料行不允許 Null。」</span><span class="sxs-lookup"><span data-stu-id="e1b3b-205">Column does not allow nulls."</span></span> <span data-ttu-id="e1b3b-206">這是什麼意思，以及如何修正 hello 錯誤？</span><span class="sxs-lookup"><span data-stu-id="e1b3b-206">What does this mean, and how can I fix hello error?</span></span> 
<span data-ttu-id="e1b3b-207">這則錯誤訊息指出其中一個 hello 兩個下列問題：</span><span class="sxs-lookup"><span data-stu-id="e1b3b-207">This error message indicates one of hello two following issues:</span></span>
1.  <span data-ttu-id="e1b3b-208">資料表缺少主索引鍵。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-208">There may be a table without a primary key.</span></span> <span data-ttu-id="e1b3b-209">toofix 這個問題，請新增 hello 資料表的主索引鍵 tooall 正在同步處理。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-209">toofix this issue, add a primary key tooall hello tables you're syncing.</span></span>
2.  <span data-ttu-id="e1b3b-210">在 CREATE INDEX 陳述式中可能有 WHERE 子句。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-210">There may be a WHERE clause in your CREATE INDEX statement.</span></span> <span data-ttu-id="e1b3b-211">同步無法處理這種狀況。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-211">Sync does not handle this condition.</span></span> <span data-ttu-id="e1b3b-212">toofix 這個問題，請移除 hello WHERE 子句，或手動變更 hello tooall 資料庫。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-212">toofix this issue, remove hello WHERE clause or manually make hello changes tooall databases.</span></span> 
 
### <a name="how-does-data-sync-handle-circular-references-that-is-when-hello-same-data-is-synced-in-multiple-sync-groups-and-keeps-changing-as-a-result"></a><span data-ttu-id="e1b3b-213">資料同步如何處理循環參考？</span><span class="sxs-lookup"><span data-stu-id="e1b3b-213">How does Data Sync handle circular references?</span></span> <span data-ttu-id="e1b3b-214">也就是當 hello 相同的資料已同步處理在多個同步處理群組，並持續變更的結果嗎？</span><span class="sxs-lookup"><span data-stu-id="e1b3b-214">That is, when hello same data is synced in multiple sync groups, and keeps changing as a result?</span></span>
<span data-ttu-id="e1b3b-215">資料同步不會處理循環參考。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-215">Data Sync doesn’t handle circular references.</span></span> <span data-ttu-id="e1b3b-216">要確定 tooavoid 它們。</span><span class="sxs-lookup"><span data-stu-id="e1b3b-216">Be sure tooavoid them.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="e1b3b-217">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e1b3b-217">Next steps</span></span>

<span data-ttu-id="e1b3b-218">如需 SQL 資料同步的詳細資訊，請參閱：</span><span class="sxs-lookup"><span data-stu-id="e1b3b-218">For more info about SQL Data Sync, see:</span></span>

-   [<span data-ttu-id="e1b3b-219">開始使用 SQL 資料同步</span><span class="sxs-lookup"><span data-stu-id="e1b3b-219">Getting Started with SQL Data Sync</span></span>](sql-database-get-started-sql-data-sync.md)

-   <span data-ttu-id="e1b3b-220">完成 PowerShell 範例，說明如何 tooconfigure SQL 資料同步：</span><span class="sxs-lookup"><span data-stu-id="e1b3b-220">Complete PowerShell examples that show how tooconfigure SQL Data Sync:</span></span>
    -   [<span data-ttu-id="e1b3b-221">使用多個 Azure SQL database 之間的 PowerShell toosync</span><span class="sxs-lookup"><span data-stu-id="e1b3b-221">Use PowerShell toosync between multiple Azure SQL databases</span></span>](scripts/sql-database-sync-data-between-sql-databases.md)
    -   [<span data-ttu-id="e1b3b-222">使用 Azure SQL Database 和 SQL Server 在內部部署資料庫之間的 PowerShell toosync</span><span class="sxs-lookup"><span data-stu-id="e1b3b-222">Use PowerShell toosync between an Azure SQL Database and a SQL Server on-premises database</span></span>](scripts/sql-database-sync-data-between-azure-onprem.md)

-   [<span data-ttu-id="e1b3b-223">下載 hello 完整 SQL 資料同步技術文件</span><span class="sxs-lookup"><span data-stu-id="e1b3b-223">Download hello complete SQL Data Sync technical documentation</span></span>](https://github.com/Microsoft/sql-server-samples/raw/master/samples/features/sql-data-sync/Data_Sync_Preview_full_documentation.pdf?raw=true)

-   [<span data-ttu-id="e1b3b-224">下載 SQL 資料同步處理的 REST API 文件以 hello</span><span class="sxs-lookup"><span data-stu-id="e1b3b-224">Download hello SQL Data Sync REST API documentation</span></span>](https://github.com/Microsoft/sql-server-samples/raw/master/samples/features/sql-data-sync/Data_Sync_Preview_REST_API.pdf?raw=true)

<span data-ttu-id="e1b3b-225">如需 SQL Database 的詳細資訊，請參閱：</span><span class="sxs-lookup"><span data-stu-id="e1b3b-225">For more info about SQL Database, see:</span></span>

-   [<span data-ttu-id="e1b3b-226">SQL Database 概觀</span><span class="sxs-lookup"><span data-stu-id="e1b3b-226">SQL Database Overview</span></span>](sql-database-technical-overview.md)

-   [<span data-ttu-id="e1b3b-227">資料庫生命週期管理</span><span class="sxs-lookup"><span data-stu-id="e1b3b-227">Database Lifecycle Management</span></span>](https://msdn.microsoft.com/library/jj907294.aspx)
