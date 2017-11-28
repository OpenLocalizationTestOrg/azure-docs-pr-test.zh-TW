---
title: "同步資料 (預覽) | Microsoft Docs"
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
ms.openlocfilehash: 926938a8ed20167e1f17a9883007cd993897f14a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="sync-data-across-multiple-cloud-and-on-premises-databases-with-sql-data-sync"></a><span data-ttu-id="598fb-103">使用 SQL 資料同步，跨多個雲端和內部部署資料庫同步資料</span><span class="sxs-lookup"><span data-stu-id="598fb-103">Sync data across multiple cloud and on-premises databases with SQL Data Sync</span></span>

<span data-ttu-id="598fb-104">「SQL 資料同步」是一種建置在 Azure SQL Database 上的服務，可讓您跨多個 SQL 資料庫和 SQL Server 執行個體，雙向同步您選取的資料。</span><span class="sxs-lookup"><span data-stu-id="598fb-104">SQL Data Sync is a service built on Azure SQL Database that lets you synchronize the data you select bi-directionally across multiple SQL databases and SQL Server instances.</span></span>

<span data-ttu-id="598fb-105">資料同步以「同步群組」的概念為基礎。</span><span class="sxs-lookup"><span data-stu-id="598fb-105">Data Sync is based around the concept of a Sync Group.</span></span> <span data-ttu-id="598fb-106">「同步群組」是您想要同步的資料庫群組。</span><span class="sxs-lookup"><span data-stu-id="598fb-106">A Sync Group is a group of databases that you want to synchronize.</span></span>

<span data-ttu-id="598fb-107">同步群組具有下列屬性：</span><span class="sxs-lookup"><span data-stu-id="598fb-107">A Sync Group has the following properties:</span></span>

-   <span data-ttu-id="598fb-108">**同步結構描述**說明要同步的資料。</span><span class="sxs-lookup"><span data-stu-id="598fb-108">The **Sync Schema** describes which data is being synchronized.</span></span>

-   <span data-ttu-id="598fb-109">**同步處理方向**可以是雙向或只有單向。</span><span class="sxs-lookup"><span data-stu-id="598fb-109">The **Sync Direction** can be bi-directional or can flow in only one direction.</span></span> <span data-ttu-id="598fb-110">也就是說，同步處理方向可以是*中樞到成員*或是*成員到中樞*，或兩者皆可。</span><span class="sxs-lookup"><span data-stu-id="598fb-110">That is, the Sync Direction can be *Hub to Member* or *Member to Hub*, or both.</span></span>

-   <span data-ttu-id="598fb-111">**同步處理間隔**是進行同步處理的頻率。</span><span class="sxs-lookup"><span data-stu-id="598fb-111">The **Sync Interval** is how often synchronization occurs.</span></span>

-   <span data-ttu-id="598fb-112">**衝突解決原則**是群組層級原則，可以是*中樞獲勝*或*成員獲勝*。</span><span class="sxs-lookup"><span data-stu-id="598fb-112">The **Conflict Resolution Policy** is a group level policy, which can be *Hub wins* or *Member wins*.</span></span>

<span data-ttu-id="598fb-113">資料同步使用中樞和輪輻拓撲來同步資料。</span><span class="sxs-lookup"><span data-stu-id="598fb-113">Data Sync uses a hub and spoke topology to synchronize data.</span></span> <span data-ttu-id="598fb-114">您可以將群組中的其中一個資料庫定義為「中樞資料庫」。</span><span class="sxs-lookup"><span data-stu-id="598fb-114">You define one of the databases in the group as the Hub Database.</span></span> <span data-ttu-id="598fb-115">其餘的資料庫則是成員資料庫。</span><span class="sxs-lookup"><span data-stu-id="598fb-115">The rest of the databases are member databases.</span></span> <span data-ttu-id="598fb-116">只有中樞和個別成員之間才會進行同步。</span><span class="sxs-lookup"><span data-stu-id="598fb-116">Sync occurs only between the Hub and individual members.</span></span>
-   <span data-ttu-id="598fb-117">**中樞資料庫**必須是 Azure SQL Database。</span><span class="sxs-lookup"><span data-stu-id="598fb-117">The **Hub Database** must be an Azure SQL Database.</span></span>
-   <span data-ttu-id="598fb-118">**成員資料庫**可以是 SQL 資料庫、內部部署 SQL Server 資料庫，或是在 Azure 虛擬機器上的 SQL Server 執行個體。</span><span class="sxs-lookup"><span data-stu-id="598fb-118">The **member databases** can be either SQL Databases, on-premises SQL Server databases, or SQL Server instances on Azure virtual machines.</span></span>
-   <span data-ttu-id="598fb-119">**同步處理資料庫**包含「資料同步」的中繼資料和記錄。「同步處理資料庫」必須是與「中樞資料庫」位於相同區域的 Azure SQL Database。</span><span class="sxs-lookup"><span data-stu-id="598fb-119">The **Sync Database** contains the metadata and log for Data Sync. The Sync Database has to be an Azure SQL Database located in the same region as the Hub Database.</span></span> <span data-ttu-id="598fb-120">「同步處理資料庫」是由客戶建立，並由客戶擁有。</span><span class="sxs-lookup"><span data-stu-id="598fb-120">The Sync Database is customer created and customer owned.</span></span>

> [!NOTE]
> <span data-ttu-id="598fb-121">如果您使用內部部署資料庫，必須[設定本機代理程式](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-get-started-sql-data-sync)。</span><span class="sxs-lookup"><span data-stu-id="598fb-121">If you're using an on premises database, you have to [configure a local agent.](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-get-started-sql-data-sync)</span></span>

![資料庫之間的同步資料](media/sql-database-sync-data/sync-data-overview.png)

## <a name="when-to-use-data-sync"></a><span data-ttu-id="598fb-123">使用資料同步的時機</span><span class="sxs-lookup"><span data-stu-id="598fb-123">When to use Data Sync</span></span>

<span data-ttu-id="598fb-124">如果您需要讓多個 Azure SQL Database 或 SQL Server 資料庫之間的資料保持在最新狀態，資料同步就很有用。</span><span class="sxs-lookup"><span data-stu-id="598fb-124">Data Sync is useful in cases where data needs to be kept up to date across several Azure SQL Databases or SQL Server databases.</span></span> <span data-ttu-id="598fb-125">以下是資料同步主要的使用案例：</span><span class="sxs-lookup"><span data-stu-id="598fb-125">Here are the main use cases for Data Sync:</span></span>

-   <span data-ttu-id="598fb-126">**混合式資料同步：**使用資料同步，您可以讓內部部署資料庫與 Azure SQL Database 之間的資料保持同步，以啟用混合式應用程式。</span><span class="sxs-lookup"><span data-stu-id="598fb-126">**Hybrid Data Synchronization:** With Data Sync, you can keep data synchronized between your on-premises databases and Azure SQL Databases to enable hybrid applications.</span></span> <span data-ttu-id="598fb-127">此功能對於考慮移轉至雲端，而且想要將部分應用程式放在 Azure 的客戶很有吸引力。</span><span class="sxs-lookup"><span data-stu-id="598fb-127">This capability may appeal to customers who are considering moving to the cloud and would like to put some of their application in Azure.</span></span>

-   <span data-ttu-id="598fb-128">**分散式應用程式：**在許多情況下，將不同的工作負載分散到不同的資料庫會有好處。</span><span class="sxs-lookup"><span data-stu-id="598fb-128">**Distributed Applications:** In many cases, it's beneficial to separate different workloads across different databases.</span></span> <span data-ttu-id="598fb-129">例如，如果您有大型的實際執行資料庫，但也必須針對這些資料執行報告或分析工作負載，此時有第二個資料庫分擔這額外的工作負載就很有幫助。</span><span class="sxs-lookup"><span data-stu-id="598fb-129">For example, if you have a large production database, but you also need to run a reporting or analytics workload on this data, it's helpful to have a second database for this additional workload.</span></span> <span data-ttu-id="598fb-130">這個方法可以減少對您實際執行工作負載的效能影響。</span><span class="sxs-lookup"><span data-stu-id="598fb-130">This approach minimizes the performance impact on your production workload.</span></span> <span data-ttu-id="598fb-131">您可以使用「資料同步」，讓這兩個資料庫保持同步。</span><span class="sxs-lookup"><span data-stu-id="598fb-131">You can use Data Sync to keep these two databases synchronized.</span></span>

-   <span data-ttu-id="598fb-132">**全域散發的應用程式：**許多企業的業務橫跨多個區域，甚至多個國家/地區。</span><span class="sxs-lookup"><span data-stu-id="598fb-132">**Globally Distributed Applications:** Many businesses span several regions and even several countries.</span></span> <span data-ttu-id="598fb-133">若要盡可能降低網路延遲，最好讓資料靠近您所在的區域。</span><span class="sxs-lookup"><span data-stu-id="598fb-133">To minimize network latency, it's best to have your data in a region close to you.</span></span> <span data-ttu-id="598fb-134">使用資料同步，您就可以輕鬆地讓全世界各個區域中的資料庫保持同步。</span><span class="sxs-lookup"><span data-stu-id="598fb-134">With Data Sync, you can easily keep databases in regions around the world synchronized.</span></span>

<span data-ttu-id="598fb-135">我們不建議在下列案例使用資料同步：</span><span class="sxs-lookup"><span data-stu-id="598fb-135">We don't recommend Data Sync for the following scenarios:</span></span>

-   <span data-ttu-id="598fb-136">災害復原</span><span class="sxs-lookup"><span data-stu-id="598fb-136">Disaster Recovery</span></span>

-   <span data-ttu-id="598fb-137">讀取級別</span><span class="sxs-lookup"><span data-stu-id="598fb-137">Read Scale</span></span>

-   <span data-ttu-id="598fb-138">ETL (OLTP 到 OLAP)</span><span class="sxs-lookup"><span data-stu-id="598fb-138">ETL (OLTP to OLAP)</span></span>

-   <span data-ttu-id="598fb-139">從內部部署 SQL Server 移轉至 Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="598fb-139">Migration from on-premises SQL Server to Azure SQL Database</span></span>

## <a name="how-does-data-sync-work"></a><span data-ttu-id="598fb-140">資料同步如何運作？</span><span class="sxs-lookup"><span data-stu-id="598fb-140">How does Data Sync work?</span></span> 

-   <span data-ttu-id="598fb-141">**追蹤資料變更：**資料同步使用 insert、update 和 delete 觸發程序追蹤變更。</span><span class="sxs-lookup"><span data-stu-id="598fb-141">**Tracking data changes:** Data Sync tracks changes using insert, update, and delete triggers.</span></span> <span data-ttu-id="598fb-142">變更會記錄在使用者資料庫中的資料表。</span><span class="sxs-lookup"><span data-stu-id="598fb-142">The changes are recorded in a side table in the user database.</span></span>

-   <span data-ttu-id="598fb-143">**同步處理資料：**資料同步是以「中樞和輪輻」的模型設計。</span><span class="sxs-lookup"><span data-stu-id="598fb-143">**Synchronizing data:** Data Sync is designed in a Hub and Spoke model.</span></span> <span data-ttu-id="598fb-144">中樞會與每個成員個別同步。</span><span class="sxs-lookup"><span data-stu-id="598fb-144">The Hub syncs with each member individually.</span></span> <span data-ttu-id="598fb-145">中樞的變更會下載到成員，然後成員的變更會上傳到中樞。</span><span class="sxs-lookup"><span data-stu-id="598fb-145">Changes from the Hub are downloaded to the member and then changes from the member are uploaded to the Hub.</span></span>

-   <span data-ttu-id="598fb-146">**解決衝突：**資料同步提供兩個衝突解決選項：*中樞獲勝*或*成員獲勝*。</span><span class="sxs-lookup"><span data-stu-id="598fb-146">**Resolving conflicts:** Data Sync provides two options for conflict resolution, *Hub wins* or *Member wins*.</span></span>
    -   <span data-ttu-id="598fb-147">如果您選取 [中樞獲勝]，中樞的變更永遠會覆寫成員的變更。</span><span class="sxs-lookup"><span data-stu-id="598fb-147">If you select *Hub wins*, the changes in the hub always overwrite changes in the member.</span></span>
    -   <span data-ttu-id="598fb-148">如果您選取 [成員獲勝]，成員的變更永遠會覆寫中樞的變更。</span><span class="sxs-lookup"><span data-stu-id="598fb-148">If you select *Member wins*, the changes in the member overwrite changes in the hub.</span></span> <span data-ttu-id="598fb-149">如果有多個成員，最終的值則取決於哪一個成員先同步。</span><span class="sxs-lookup"><span data-stu-id="598fb-149">If there's more than one member, the final value depends on which member syncs first.</span></span>

## <a name="limitations-and-considerations"></a><span data-ttu-id="598fb-150">限制與注意事項</span><span class="sxs-lookup"><span data-stu-id="598fb-150">Limitations and considerations</span></span>

### <a name="performance-impact"></a><span data-ttu-id="598fb-151">效能影響</span><span class="sxs-lookup"><span data-stu-id="598fb-151">Performance impact</span></span>
<span data-ttu-id="598fb-152">資料同步使用 insert、update 和 delete 觸發程序追蹤變更。</span><span class="sxs-lookup"><span data-stu-id="598fb-152">Data Sync uses insert, update, and delete triggers to track changes.</span></span> <span data-ttu-id="598fb-153">其會在使用者資料庫中建立側邊資料表，以便進行變更追蹤。</span><span class="sxs-lookup"><span data-stu-id="598fb-153">It creates side tables in the user database for change tracking.</span></span> <span data-ttu-id="598fb-154">這些變更追蹤活動會影響您的資料庫工作負載。</span><span class="sxs-lookup"><span data-stu-id="598fb-154">These change tracking activities have an impact on your database workload.</span></span> <span data-ttu-id="598fb-155">請評估您的服務層，如有必要則請升級。</span><span class="sxs-lookup"><span data-stu-id="598fb-155">Assess your service tier and upgrade if needed.</span></span>

### <a name="eventual-consistency"></a><span data-ttu-id="598fb-156">最終一致性</span><span class="sxs-lookup"><span data-stu-id="598fb-156">Eventual consistency</span></span>
<span data-ttu-id="598fb-157">由於資料同步是以觸發程序為基礎，所以並不保證交易一致性。</span><span class="sxs-lookup"><span data-stu-id="598fb-157">Since Data Sync is trigger-based, transactional consistency is not guaranteed.</span></span> <span data-ttu-id="598fb-158">Microsoft 保證最終會進行所有變更，而且資料同步不會造成資料遺失。</span><span class="sxs-lookup"><span data-stu-id="598fb-158">Microsoft guarantees that all changes are made eventually and that Data Sync does not cause data loss.</span></span>

### <a name="unsupported-data-types"></a><span data-ttu-id="598fb-159">不支援的資料類型</span><span class="sxs-lookup"><span data-stu-id="598fb-159">Unsupported data types</span></span>

-   <span data-ttu-id="598fb-160">FileStream</span><span class="sxs-lookup"><span data-stu-id="598fb-160">FileStream</span></span>

-   <span data-ttu-id="598fb-161">SQL/CLR UDT</span><span class="sxs-lookup"><span data-stu-id="598fb-161">SQL/CLR UDT</span></span>

-   <span data-ttu-id="598fb-162">XMLSchemaCollection (支援 XML)</span><span class="sxs-lookup"><span data-stu-id="598fb-162">XMLSchemaCollection (XML supported)</span></span>

-   <span data-ttu-id="598fb-163">Cursor、Timestamp、Hierarchyid</span><span class="sxs-lookup"><span data-stu-id="598fb-163">Cursor, Timestamp, Hierarchyid</span></span>

### <a name="requirements"></a><span data-ttu-id="598fb-164">需求</span><span class="sxs-lookup"><span data-stu-id="598fb-164">Requirements</span></span>

-   <span data-ttu-id="598fb-165">每個資料表都必須有主索引鍵。</span><span class="sxs-lookup"><span data-stu-id="598fb-165">Each table must have a primary key.</span></span>

-   <span data-ttu-id="598fb-166">資料表不能有非主索引鍵的識別欄位。</span><span class="sxs-lookup"><span data-stu-id="598fb-166">A table cannot have an identity column that is not the primary key.</span></span>

-   <span data-ttu-id="598fb-167">物件 (資料庫、資料表和資料行) 的名稱不能包含可列印的字元句點 (.)、左括弧 (\[\)，或右括弧 (\]\)。</span><span class="sxs-lookup"><span data-stu-id="598fb-167">The names of objects (databases, tables, and columns) cannot contain the printable characters period (.), left square bracket ([), or right square bracket (]).</span></span>

### <a name="limitations-on-service-and-database-dimensions"></a><span data-ttu-id="598fb-168">服務和資料庫維度的限制</span><span class="sxs-lookup"><span data-stu-id="598fb-168">Limitations on service and database dimensions</span></span>

|                                                                 |                        |                             |
|-----------------------------------------------------------------|------------------------|-----------------------------|
| <span data-ttu-id="598fb-169">**維度**</span><span class="sxs-lookup"><span data-stu-id="598fb-169">**Dimensions**</span></span>                                                      | <span data-ttu-id="598fb-170">**限制**</span><span class="sxs-lookup"><span data-stu-id="598fb-170">**Limit**</span></span>              | <span data-ttu-id="598fb-171">**因應措施**</span><span class="sxs-lookup"><span data-stu-id="598fb-171">**Workaround**</span></span>              |
| <span data-ttu-id="598fb-172">任何資料庫可以隸屬的同步群組數目上限。</span><span class="sxs-lookup"><span data-stu-id="598fb-172">Maximum number of sync groups any database can belong to.</span></span>       | <span data-ttu-id="598fb-173">5</span><span class="sxs-lookup"><span data-stu-id="598fb-173">5</span></span>                      |                             |
| <span data-ttu-id="598fb-174">單一同步群組中的端點數目上限</span><span class="sxs-lookup"><span data-stu-id="598fb-174">Maximum number of endpoints in a single sync group</span></span>              | <span data-ttu-id="598fb-175">30</span><span class="sxs-lookup"><span data-stu-id="598fb-175">30</span></span>                     | <span data-ttu-id="598fb-176">建立多個同步群組</span><span class="sxs-lookup"><span data-stu-id="598fb-176">Create multiple sync groups</span></span> |
| <span data-ttu-id="598fb-177">單一同步群組中的內部部署端點數目上限。</span><span class="sxs-lookup"><span data-stu-id="598fb-177">Maximum number of on-premises endpoints in a single sync group.</span></span> | <span data-ttu-id="598fb-178">5</span><span class="sxs-lookup"><span data-stu-id="598fb-178">5</span></span>                      | <span data-ttu-id="598fb-179">建立多個同步群組</span><span class="sxs-lookup"><span data-stu-id="598fb-179">Create multiple sync groups</span></span> |
| <span data-ttu-id="598fb-180">資料庫名稱、資料表名稱、結構描述名稱和資料行名稱</span><span class="sxs-lookup"><span data-stu-id="598fb-180">Database, table, schema, and column names</span></span>                       | <span data-ttu-id="598fb-181">每個名稱 50 個字元</span><span class="sxs-lookup"><span data-stu-id="598fb-181">50 characters per name</span></span> |                             |
| <span data-ttu-id="598fb-182">一個同步群組中的資料表</span><span class="sxs-lookup"><span data-stu-id="598fb-182">Tables in a sync group</span></span>                                          | <span data-ttu-id="598fb-183">500</span><span class="sxs-lookup"><span data-stu-id="598fb-183">500</span></span>                    | <span data-ttu-id="598fb-184">建立多個同步群組</span><span class="sxs-lookup"><span data-stu-id="598fb-184">Create multiple sync groups</span></span> |
| <span data-ttu-id="598fb-185">一個同步群組中一個資料表中的資料行</span><span class="sxs-lookup"><span data-stu-id="598fb-185">Columns in a table in a sync group</span></span>                              | <span data-ttu-id="598fb-186">1000</span><span class="sxs-lookup"><span data-stu-id="598fb-186">1000</span></span>                   |                             |
| <span data-ttu-id="598fb-187">一個資料表上的資料列大小</span><span class="sxs-lookup"><span data-stu-id="598fb-187">Data row size on a table</span></span>                                        | <span data-ttu-id="598fb-188">24 Mb</span><span class="sxs-lookup"><span data-stu-id="598fb-188">24 Mb</span></span>                  |                             |
| <span data-ttu-id="598fb-189">最小同步處理間隔</span><span class="sxs-lookup"><span data-stu-id="598fb-189">Minimum sync interval</span></span>                                           | <span data-ttu-id="598fb-190">5 分鐘</span><span class="sxs-lookup"><span data-stu-id="598fb-190">5 Minutes</span></span>              |                             |

## <a name="common-questions"></a><span data-ttu-id="598fb-191">常見問題</span><span class="sxs-lookup"><span data-stu-id="598fb-191">Common questions</span></span>

### <a name="how-frequently-can-data-sync-synchronize-my-data"></a><span data-ttu-id="598fb-192">資料同步多久會同步我的資料一次？</span><span class="sxs-lookup"><span data-stu-id="598fb-192">How frequently can Data Sync synchronize my data?</span></span> 
<span data-ttu-id="598fb-193">至少每隔五分鐘。</span><span class="sxs-lookup"><span data-stu-id="598fb-193">The minimum frequency is every five minutes.</span></span>

### <a name="can-i-use-data-sync-to-sync-between-sql-server-on-premises-databases-only"></a><span data-ttu-id="598fb-194">資料同步能否僅在 SQL Server 內部部署資料庫之間同步？</span><span class="sxs-lookup"><span data-stu-id="598fb-194">Can I use Data Sync to sync between SQL Server on-premises databases only?</span></span> 
<span data-ttu-id="598fb-195">無法直接進行。</span><span class="sxs-lookup"><span data-stu-id="598fb-195">Not directly.</span></span> <span data-ttu-id="598fb-196">您可以間接在 SQL Server 內部部署資料庫之間同步，不過，必須先在 Azure 建立中樞資料庫，然後將內部部署資料庫新增到同步群組。</span><span class="sxs-lookup"><span data-stu-id="598fb-196">You can sync between SQL Server on-premises databases indirectly, however, by creating a Hub database in Azure, and then adding the on-premises databases to the sync group.</span></span>
   
### <a name="can-i-use-data-sync-to-seed-data-from-my-production-database-to-an-empty-database-and-then-keep-them-synchronized"></a><span data-ttu-id="598fb-197">能否使用資料同步將生產環境資料庫的資料植入空白資料庫，然後讓資料保持同步？</span><span class="sxs-lookup"><span data-stu-id="598fb-197">Can I use Data Sync to seed data from my production database to an empty database, and then keep them synchronized?</span></span> 
<span data-ttu-id="598fb-198">是。</span><span class="sxs-lookup"><span data-stu-id="598fb-198">Yes.</span></span> <span data-ttu-id="598fb-199">請從原始結構描述編寫結構描述，藉此在新的資料庫中手動建立結構描述。</span><span class="sxs-lookup"><span data-stu-id="598fb-199">Create the schema manually in the new database by scripting it from the original.</span></span> <span data-ttu-id="598fb-200">建立結構描述之後，請將資料表新增到同步群組，以複製資料並讓資料保持同步。</span><span class="sxs-lookup"><span data-stu-id="598fb-200">After you create the schema, add the tables to a sync group to copy the data and keep it synced.</span></span>

### <a name="why-do-i-see-tables-that-i-did-not-create"></a><span data-ttu-id="598fb-201">為什麼我會看到並非自己建立的資料表？</span><span class="sxs-lookup"><span data-stu-id="598fb-201">Why do I see tables that I did not create?</span></span>  
<span data-ttu-id="598fb-202">資料同步會在資料庫中建立側邊資料表，以便進行變更追蹤。</span><span class="sxs-lookup"><span data-stu-id="598fb-202">Data Sync creates side tables in your database for change tracking.</span></span> <span data-ttu-id="598fb-203">請勿刪除它們，否則資料同步無法正常運作。</span><span class="sxs-lookup"><span data-stu-id="598fb-203">Don't delete them or Data Sync stops working.</span></span>
   
### <a name="i-got-an-error-message-that-said-cannot-insert-the-value-null-into-the-column-column-column-does-not-allow-nulls-what-does-this-mean-and-how-can-i-fix-the-error"></a><span data-ttu-id="598fb-204">我看見錯誤訊息顯示「無法將 NULL 值插入資料行\<資料行\>。</span><span class="sxs-lookup"><span data-stu-id="598fb-204">I got an error message that said "cannot insert the value NULL into the column \<column\>.</span></span> <span data-ttu-id="598fb-205">資料行不允許 Null。」</span><span class="sxs-lookup"><span data-stu-id="598fb-205">Column does not allow nulls."</span></span> <span data-ttu-id="598fb-206">這是什麼意思，該如何修正錯誤？</span><span class="sxs-lookup"><span data-stu-id="598fb-206">What does this mean, and how can I fix the error?</span></span> 
<span data-ttu-id="598fb-207">此錯誤訊息表示發生了下列兩種問題的其中之一：</span><span class="sxs-lookup"><span data-stu-id="598fb-207">This error message indicates one of the two following issues:</span></span>
1.  <span data-ttu-id="598fb-208">資料表缺少主索引鍵。</span><span class="sxs-lookup"><span data-stu-id="598fb-208">There may be a table without a primary key.</span></span> <span data-ttu-id="598fb-209">若要修正此問題，請將主索引鍵新增至要同步的所有資料表。</span><span class="sxs-lookup"><span data-stu-id="598fb-209">To fix this issue, add a primary key to all the tables you're syncing.</span></span>
2.  <span data-ttu-id="598fb-210">在 CREATE INDEX 陳述式中可能有 WHERE 子句。</span><span class="sxs-lookup"><span data-stu-id="598fb-210">There may be a WHERE clause in your CREATE INDEX statement.</span></span> <span data-ttu-id="598fb-211">同步無法處理這種狀況。</span><span class="sxs-lookup"><span data-stu-id="598fb-211">Sync does not handle this condition.</span></span> <span data-ttu-id="598fb-212">若要修正此問題，請移除 WHERE 子句或手動變更所有資料庫。</span><span class="sxs-lookup"><span data-stu-id="598fb-212">To fix this issue, remove the WHERE clause or manually make the changes to all databases.</span></span> 
 
### <a name="how-does-data-sync-handle-circular-references-that-is-when-the-same-data-is-synced-in-multiple-sync-groups-and-keeps-changing-as-a-result"></a><span data-ttu-id="598fb-213">資料同步如何處理循環參考？</span><span class="sxs-lookup"><span data-stu-id="598fb-213">How does Data Sync handle circular references?</span></span> <span data-ttu-id="598fb-214">也就是，相同的資料已在多個同步群組中同步，且因此持續變更？</span><span class="sxs-lookup"><span data-stu-id="598fb-214">That is, when the same data is synced in multiple sync groups, and keeps changing as a result?</span></span>
<span data-ttu-id="598fb-215">資料同步不會處理循環參考。</span><span class="sxs-lookup"><span data-stu-id="598fb-215">Data Sync doesn’t handle circular references.</span></span> <span data-ttu-id="598fb-216">請務必避免。</span><span class="sxs-lookup"><span data-stu-id="598fb-216">Be sure to avoid them.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="598fb-217">後續步驟</span><span class="sxs-lookup"><span data-stu-id="598fb-217">Next steps</span></span>

<span data-ttu-id="598fb-218">如需 SQL 資料同步的詳細資訊，請參閱：</span><span class="sxs-lookup"><span data-stu-id="598fb-218">For more info about SQL Data Sync, see:</span></span>

-   [<span data-ttu-id="598fb-219">開始使用 SQL 資料同步</span><span class="sxs-lookup"><span data-stu-id="598fb-219">Getting Started with SQL Data Sync</span></span>](sql-database-get-started-sql-data-sync.md)

-   <span data-ttu-id="598fb-220">示範如何設定 SQL 資料同步的完整 PowerShell 範例：</span><span class="sxs-lookup"><span data-stu-id="598fb-220">Complete PowerShell examples that show how to configure SQL Data Sync:</span></span>
    -   [<span data-ttu-id="598fb-221">使用 PowerShell 在多個 Azure SQL Database 之間進行同步處理</span><span class="sxs-lookup"><span data-stu-id="598fb-221">Use PowerShell to sync between multiple Azure SQL databases</span></span>](scripts/sql-database-sync-data-between-sql-databases.md)
    -   [<span data-ttu-id="598fb-222">使用 PowerShell 設定「資料同步」在內部部署的 Azure SQL Database 和 SQL Server 之間進行同步處理</span><span class="sxs-lookup"><span data-stu-id="598fb-222">Use PowerShell to sync between an Azure SQL Database and a SQL Server on-premises database</span></span>](scripts/sql-database-sync-data-between-azure-onprem.md)

-   [<span data-ttu-id="598fb-223">下載完整的 SQL 資料同步技術文件</span><span class="sxs-lookup"><span data-stu-id="598fb-223">Download the complete SQL Data Sync technical documentation</span></span>](https://github.com/Microsoft/sql-server-samples/raw/master/samples/features/sql-data-sync/Data_Sync_Preview_full_documentation.pdf?raw=true)

-   [<span data-ttu-id="598fb-224">下載 SQL 資料同步 REST API 文件</span><span class="sxs-lookup"><span data-stu-id="598fb-224">Download the SQL Data Sync REST API documentation</span></span>](https://github.com/Microsoft/sql-server-samples/raw/master/samples/features/sql-data-sync/Data_Sync_Preview_REST_API.pdf?raw=true)

<span data-ttu-id="598fb-225">如需 SQL Database 的詳細資訊，請參閱：</span><span class="sxs-lookup"><span data-stu-id="598fb-225">For more info about SQL Database, see:</span></span>

-   [<span data-ttu-id="598fb-226">SQL Database 概觀</span><span class="sxs-lookup"><span data-stu-id="598fb-226">SQL Database Overview</span></span>](sql-database-technical-overview.md)

-   [<span data-ttu-id="598fb-227">資料庫生命週期管理</span><span class="sxs-lookup"><span data-stu-id="598fb-227">Database Lifecycle Management</span></span>](https://msdn.microsoft.com/library/jj907294.aspx)
