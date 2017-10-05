---
title: "Azure 入口網站：建立及管理 SQL Database 彈性集區 | Microsoft Docs"
description: "了解如何使用 Azure 入口網站和 SQL Database 的內建智慧功能來管理、監視及準確估量可調整的彈性集區，以期能最佳化資料庫效能和管理成本。"
keywords: 
services: sql-database
documentationcenter: 
author: ninarn
manager: jhubbard
editor: cgronlun
ms.assetid: 3dc9b7a3-4b10-423a-8e44-9174aca5cf3d
ms.service: sql-database
ms.custom: DBs & servers
ms.devlang: NA
ms.date: 06/06/2016
ms.author: ninarn
ms.workload: data-management
ms.topic: article
ms.tgt_pltfrm: NA
ms.openlocfilehash: 4ffd1db31f42967dc7f07aa979898dddbb333641
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-manage-an-elastic-pool-with-the-azure-portal"></a><span data-ttu-id="70540-103">使用 Azure 入口網站建立及管理彈性集區</span><span class="sxs-lookup"><span data-stu-id="70540-103">Create and manage an elastic pool with the Azure portal</span></span>
<span data-ttu-id="70540-104">本主題說明如何使用 Azure 入口網站來建立及管理可調整的[彈性集區](sql-database-elastic-pool.md)。</span><span class="sxs-lookup"><span data-stu-id="70540-104">This topic shows you how to create and manage scalable [elastic pools](sql-database-elastic-pool.md) with the Azure portal.</span></span> <span data-ttu-id="70540-105">您也可以使用 [PowerShell](sql-database-elastic-pool-manage-powershell.md)、REST API 或 [C#](sql-database-elastic-pool-manage-csharp.md) 來建立及管理 Azure 彈性集區。</span><span class="sxs-lookup"><span data-stu-id="70540-105">You can also create and manage an Azure elastic pool with [PowerShell](sql-database-elastic-pool-manage-powershell.md), the REST API, or [C#](sql-database-elastic-pool-manage-csharp.md).</span></span> <span data-ttu-id="70540-106">您也可以使用 [Transact-SQL](sql-database-elastic-pool-manage-tsql.md) 來建立資料庫並將它移入和移出彈性集區。</span><span class="sxs-lookup"><span data-stu-id="70540-106">You can also create and move databases into and out of elastic pools using [Transact-SQL](sql-database-elastic-pool-manage-tsql.md).</span></span>

## <a name="create-an-elastic-pool"></a><span data-ttu-id="70540-107">建立彈性集區</span><span class="sxs-lookup"><span data-stu-id="70540-107">Create an elastic pool</span></span> 

<span data-ttu-id="70540-108">彈性集區的建立方式有兩種。</span><span class="sxs-lookup"><span data-stu-id="70540-108">There are two ways you can create an elastic pool.</span></span> <span data-ttu-id="70540-109">如果您知道您要的集區設定則可從頭開始進行，或從服務的建議著手。</span><span class="sxs-lookup"><span data-stu-id="70540-109">You can do it from scratch if you know the pool setup you want, or start with a recommendation from the service.</span></span> <span data-ttu-id="70540-110">SQL Database 擁有的內建智慧功能會根據您資料庫過去的使用狀況遙測，為您建議更符合成本效益的彈性集區設定。</span><span class="sxs-lookup"><span data-stu-id="70540-110">SQL Database has built-in intelligence that recommends an elastic pool setup if it's more cost-efficient for you based on the past usage telemetry for your databases.</span></span>

<span data-ttu-id="70540-111">您可以在伺服器上建立多個集區，但無法將來自不同伺服器的資料庫新增到相同的集區。</span><span class="sxs-lookup"><span data-stu-id="70540-111">You can create multiple pools on a server, but you can't add databases from different servers into the same pool.</span></span> 

> [!NOTE]
> <span data-ttu-id="70540-112">彈性集區已在所有 Azure 區域中正式運作 (GA)，但印度西部除外，此區域目前提供預覽版。</span><span class="sxs-lookup"><span data-stu-id="70540-112">Elastic pools are generally available (GA) in all Azure regions except West India where it is currently in preview.</span></span>  <span data-ttu-id="70540-113">我們將儘速在此區域提供彈性集區的 GA。</span><span class="sxs-lookup"><span data-stu-id="70540-113">GA of elastic pools in this region will occur as soon as possible.</span></span>
>

### <a name="step-1-create-an-elastic-pool"></a><span data-ttu-id="70540-114">步驟 1：建立彈性集區</span><span class="sxs-lookup"><span data-stu-id="70540-114">Step 1: Create an elastic pool</span></span>

<span data-ttu-id="70540-115">從入口網站中的現有**伺服器** 刀鋒視窗建立彈性集區，是將現有資料庫移到彈性集區中的最簡單方式。</span><span class="sxs-lookup"><span data-stu-id="70540-115">Creating an elastic pool from an existing **server** blade in the portal is the easiest way to move existing databases into an elastic pool.</span></span>

> [!NOTE]
> <span data-ttu-id="70540-116">您也可以在 [Marketplace] 中搜尋 **SQL 彈性集區**，或按一下 [SQL 彈性集區] 瀏覽刀鋒視窗中的 [+新增]，以建立彈性集區。</span><span class="sxs-lookup"><span data-stu-id="70540-116">You can also create an elastic pool by searching **SQL elastic pool** in the **Marketplace** or clicking **+Add** in the **SQL elastic pools** browse blade.</span></span> <span data-ttu-id="70540-117">您可以透過此集區佈建工作流程來指定新的或現有的伺服器。</span><span class="sxs-lookup"><span data-stu-id="70540-117">You are able to specify a new or existing server through this pool provisioning workflow.</span></span>
>
>

1. <span data-ttu-id="70540-118">在 [Azure 入口網站](http://portal.azure.com/)中，按一下 [更多服務] **>** [SQL 伺服器]，然後按一下要新增到彈性集區之資料庫所在的伺服器。</span><span class="sxs-lookup"><span data-stu-id="70540-118">In the [Azure portal](http://portal.azure.com/), click **More services** **>** **SQL servers**, and then click the server that contains the databases you want to add to an elastic pool.</span></span>
2. <span data-ttu-id="70540-119">按一下 [新增集區] 。</span><span class="sxs-lookup"><span data-stu-id="70540-119">Click **New pool**.</span></span>

    ![將集區新增到伺服器](./media/sql-database-elastic-pool-create-portal/new-pool.png)

    <span data-ttu-id="70540-121">**-或-**</span><span class="sxs-lookup"><span data-stu-id="70540-121">**-OR-**</span></span>

    <span data-ttu-id="70540-122">您可能會看到一則訊息，表示伺服器有建議的彈性集區。</span><span class="sxs-lookup"><span data-stu-id="70540-122">You may see a message saying there are recommended elastic pools for the server.</span></span> <span data-ttu-id="70540-123">按一下訊息以查看系統根據資料庫的歷史使用量遙測資料所推薦的集區，然後按一下定價層以查看更多詳細資料並自訂集區。</span><span class="sxs-lookup"><span data-stu-id="70540-123">Click the message to see the recommended pools based on historical database usage telemetry, and then click the tier to see more details and customize the pool.</span></span> <span data-ttu-id="70540-124">若要了解系統是如何做出推薦的，請參閱本主題稍後的 [了解集區建議](#understand-elastic-pool-recommendations) 。</span><span class="sxs-lookup"><span data-stu-id="70540-124">See [Understand pool recommendations](#understand-elastic-pool-recommendations) later in this topic for how the recommendation is made.</span></span>

    ![建議的集區](./media/sql-database-elastic-pool-create-portal/recommended-pool.png)

3. <span data-ttu-id="70540-126">[彈性集區] 刀鋒視窗將會出現，您將在這裡指定集區的設定。</span><span class="sxs-lookup"><span data-stu-id="70540-126">The **elastic pool** blade appears, which is where you specify the settings for your pool.</span></span> <span data-ttu-id="70540-127">如果您在上一個步驟中按一下 [新增集區]，定價層預設會是 [標準]，而且未選取任何資料庫。</span><span class="sxs-lookup"><span data-stu-id="70540-127">If you clicked **New pool** in the previous step, the pricing tier is **Standard** by default and no databases is selected.</span></span> <span data-ttu-id="70540-128">您可以建立空的集區，或指定一組該伺服器的現有資料庫以移入集區。</span><span class="sxs-lookup"><span data-stu-id="70540-128">You can create an empty pool, or specify a set of existing databases from that server to move into the pool.</span></span> <span data-ttu-id="70540-129">如果您正在建立建議的集區，即會預先填入建議的定價層、效能設定與資料庫清單，但您仍然可以變更它們。</span><span class="sxs-lookup"><span data-stu-id="70540-129">If you are creating a recommended pool, the recommended pricing tier, performance settings, and list of databases are prepopulated, but you can still change them.</span></span>

    ![設定彈性集區](./media/sql-database-elastic-pool-create-portal/configure-elastic-pool.png)

4. <span data-ttu-id="70540-131">指定彈性集區的名稱，或保留預設值。</span><span class="sxs-lookup"><span data-stu-id="70540-131">Specify a name for the elastic pool, or leave it as the default.</span></span>

### <a name="step-2-choose-a-pricing-tier"></a><span data-ttu-id="70540-132">步驟 2：選擇定價層</span><span class="sxs-lookup"><span data-stu-id="70540-132">Step 2: Choose a pricing tier</span></span>

<span data-ttu-id="70540-133">集區的定價層決定了集區中彈性資料庫可用的功能，還有每個資料庫可用的 eDTU 數目上限 (eDTU MAX) 與儲存體 (GB)。</span><span class="sxs-lookup"><span data-stu-id="70540-133">The pool's pricing tier determines the features available to the elastics in the pool, and the maximum number of eDTUs (eDTU MAX), and storage (GBs) available to each database.</span></span> <span data-ttu-id="70540-134">如需詳細資訊，請參閱服務層。</span><span class="sxs-lookup"><span data-stu-id="70540-134">For details, see Service Tiers.</span></span>

<span data-ttu-id="70540-135">若要變更集區的定價層，請依序按一下 [定價層]、您想要的定價層及 [選取]。</span><span class="sxs-lookup"><span data-stu-id="70540-135">To change the pricing tier for the pool, click **Pricing tier**, click the pricing tier you want, and then click **Select**.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="70540-136">在最後一個步驟中選擇好定價層並按一下 [確定] 認可變更後，您就無法再變更集區的定價層。</span><span class="sxs-lookup"><span data-stu-id="70540-136">After you choose the pricing tier and commit your changes by clicking **OK** in the last step, you won't be able to change the pricing tier of the pool.</span></span> <span data-ttu-id="70540-137">若要變更現有彈性集區的定價層，在所需的定價層中建立一個彈性集區，並將資料庫移轉至這個新的集區。</span><span class="sxs-lookup"><span data-stu-id="70540-137">To change the pricing tier for an existing elastic pool, create an elastic pool in the desired pricing tier and migrate the databases to this new pool.</span></span>
>

![選取定價層](./media/sql-database-elastic-pool-create-portal/pricing-tier.png)

### <a name="step-3-configure-the-pool"></a><span data-ttu-id="70540-139">步驟 3︰設定集區</span><span class="sxs-lookup"><span data-stu-id="70540-139">Step 3: Configure the pool</span></span>

<span data-ttu-id="70540-140">設定定價層之後，請按一下 [設定集區]，即可新增資料庫、設定集區 eDTU 和儲存體 (集區 GB)，以及設定集區中彈性資料庫的最小和最大 eDTU。</span><span class="sxs-lookup"><span data-stu-id="70540-140">After setting the pricing tier, click Configure pool where you add databases, set pool eDTUs and storage (pool GBs), and where you set the min and max eDTUs for the elastics in the pool.</span></span>

1. <span data-ttu-id="70540-141">按一下 [設定集區] </span><span class="sxs-lookup"><span data-stu-id="70540-141">Click **Configure pool**</span></span>
2. <span data-ttu-id="70540-142">選取您要新增至集區的資料庫。</span><span class="sxs-lookup"><span data-stu-id="70540-142">Select the databases you want to add to the pool.</span></span> <span data-ttu-id="70540-143">建立集區時，這個步驟是選擇性步驟。</span><span class="sxs-lookup"><span data-stu-id="70540-143">This step is optional while creating the pool.</span></span> <span data-ttu-id="70540-144">建立集區後，可以新增資料庫。</span><span class="sxs-lookup"><span data-stu-id="70540-144">Databases can be added after the pool has been created.</span></span>
    <span data-ttu-id="70540-145">若要新增資料庫，請依序按一下 [新增資料庫]、您想要新增的資料庫以及 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="70540-145">To add databases, click **Add database**, click the databases that you want to add, and then click the **Select** button.</span></span>

    ![新增資料庫](./media/sql-database-elastic-pool-create-portal/add-databases.png)

    <span data-ttu-id="70540-147">如果您要使用的資料庫有足夠的歷史使用量遙測資料，[預估的 eDTU 和 GB 使用量] 圖形和 [實際的 eDTU 使用量] 長條圖便會更新以幫助您決定要使用的組態。</span><span class="sxs-lookup"><span data-stu-id="70540-147">If the databases you're working with have enough historical usage telemetry, the **Estimated eDTU and GB usage** graph and the **Actual eDTU usage** bar chart update to help you make configuration decisions.</span></span> <span data-ttu-id="70540-148">此外，該服務可能會提供您建議訊息，協助您決定集區的適當大小。</span><span class="sxs-lookup"><span data-stu-id="70540-148">Also, the service may give you a recommendation message to help you right-size the pool.</span></span> <span data-ttu-id="70540-149">請參閱 [動態建議](#understand-elastic-pool-recommendations)。</span><span class="sxs-lookup"><span data-stu-id="70540-149">See [Dynamic Recommendations](#understand-elastic-pool-recommendations).</span></span>

3. <span data-ttu-id="70540-150">使用 [設定集區]  頁面上的控制項，探索設定及設定您的集區。</span><span class="sxs-lookup"><span data-stu-id="70540-150">Use the controls on the **Configure pool** page to explore settings and configure your pool.</span></span> <span data-ttu-id="70540-151">如需各服務層限制的詳細資訊，請參閱[彈性集區限制](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools)；如需如何決定彈性集區適當大小的詳細指導方針，請參閱[彈性集區的價格和效能考量](sql-database-elastic-pool.md)。</span><span class="sxs-lookup"><span data-stu-id="70540-151">See [Elastic pools limits](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools) for more detail about limits for each service tier, and see [Price and performance considerations for elastic pools](sql-database-elastic-pool.md) for detailed guidance on right-sizing an elastic pool.</span></span> <span data-ttu-id="70540-152">如需集區設定的詳細資訊，請參閱[彈性集區屬性](sql-database-elastic-pool.md#database-properties-for-pooled-databases)。</span><span class="sxs-lookup"><span data-stu-id="70540-152">For more information about pool settings, see [Elastic pool properties](sql-database-elastic-pool.md#database-properties-for-pooled-databases).</span></span>

    ![設定彈性集區](./media/sql-database-elastic-pool-create-portal/configure-performance.png)

4. <span data-ttu-id="70540-154">變更設定之後，請按一下 [設定集區] 刀鋒視窗中的 [選取]。</span><span class="sxs-lookup"><span data-stu-id="70540-154">Click **Select** in the **Configure Pool** blade after changing settings.</span></span>
5. <span data-ttu-id="70540-155">按一下 [確定]  以建立集區。</span><span class="sxs-lookup"><span data-stu-id="70540-155">Click **OK** to create the pool.</span></span>

## <a name="understand-elastic-pool-recommendations"></a><span data-ttu-id="70540-156">了解彈性集區建議</span><span class="sxs-lookup"><span data-stu-id="70540-156">Understand elastic pool recommendations</span></span>

<span data-ttu-id="70540-157">SQL Database 服務會評估使用量的歷史資料，並為您推薦一或多個比使用單一資料庫更符合成本效益的集區。</span><span class="sxs-lookup"><span data-stu-id="70540-157">The SQL Database service evaluates usage history and recommends one or more pools when it is more cost-effective than using single databases.</span></span> <span data-ttu-id="70540-158">每個推薦集區都是以最適合該集區的伺服器資料庫唯一子集進行設定。</span><span class="sxs-lookup"><span data-stu-id="70540-158">Each recommendation is configured with a unique subset of the server's databases that best fit the pool.</span></span>

![建議的集區](./media/sql-database-elastic-pool-create-portal/recommended-pool.png)  

<span data-ttu-id="70540-160">集區建議包含下列內容︰</span><span class="sxs-lookup"><span data-stu-id="70540-160">The pool recommendation comprises:</span></span>

- <span data-ttu-id="70540-161">集區的定價層 (基本、標準、進階或進階 RS)</span><span class="sxs-lookup"><span data-stu-id="70540-161">A pricing tier for the pool (Basic, Standard, Premium, or Premium RS)</span></span>
- <span data-ttu-id="70540-162">適當的 [集區 eDTU]  \(也稱為每一集區的最大 eDTU)</span><span class="sxs-lookup"><span data-stu-id="70540-162">Appropriate **POOL eDTUs** (also called Max eDTUs per pool)</span></span>
- <span data-ttu-id="70540-163">每一資料庫的 [eDTU 上限] 和 [eDTU 下限]</span><span class="sxs-lookup"><span data-stu-id="70540-163">The **eDTU MAX** and **eDTU Min** per database</span></span>
- <span data-ttu-id="70540-164">集區的建議資料庫清單</span><span class="sxs-lookup"><span data-stu-id="70540-164">The list of recommended databases for the pool</span></span>

> [!IMPORTANT]
> <span data-ttu-id="70540-165">服務在建議集區時，會計算過去 30 天的遙測。</span><span class="sxs-lookup"><span data-stu-id="70540-165">The service takes the last 30 days of telemetry into account when recommending pools.</span></span> <span data-ttu-id="70540-166">為了讓資料庫被視為彈性集區的候選項目，它必須存在至少 7 天。</span><span class="sxs-lookup"><span data-stu-id="70540-166">For a database to be considered as a candidate for an elastic pool, it must exist for at least 7 days.</span></span> <span data-ttu-id="70540-167">已在彈性集區中的資料庫不會被視為彈性集區建議候選項目。</span><span class="sxs-lookup"><span data-stu-id="70540-167">Databases that are already in an elastic pool are not considered as candidates for elastic pool recommendations.</span></span>
>

<span data-ttu-id="70540-168">服務會評估將每個服務層中的單一資料庫移至同一層集區的資源需求和成本效益。</span><span class="sxs-lookup"><span data-stu-id="70540-168">The service evaluates resource needs and cost effectiveness of moving the single databases in each service tier into pools of the same tier.</span></span> <span data-ttu-id="70540-169">例如，會評估伺服器上的所有 Standard 資料庫是否適合 Standard 彈性集區。</span><span class="sxs-lookup"><span data-stu-id="70540-169">For example, all Standard databases on a server are assessed for their fit into a Standard Elastic Pool.</span></span> <span data-ttu-id="70540-170">這表示服務不會進行跨層建議，例如將 Standard 資料庫移到 Premium 集區。</span><span class="sxs-lookup"><span data-stu-id="70540-170">This means the service does not make cross-tier recommendations such as moving a Standard database into a Premium pool.</span></span>

<span data-ttu-id="70540-171">將資料庫新增至集區之後，會根據您所選資料庫的過去使用情況來動態產生建議。</span><span class="sxs-lookup"><span data-stu-id="70540-171">After adding databases to the pool, recommendations are dynamically generated based on the historical usage of the databases you have selected.</span></span> <span data-ttu-id="70540-172">這些建議會顯示在 eDTU 和 GB 使用情況圖表，以及 [設定集區] 刀鋒視窗頂端的建議橫幅中。</span><span class="sxs-lookup"><span data-stu-id="70540-172">These recommendations are shown in the eDTU and GB usage chart and in a recommendation banner at the top of the **Configure pool** blade.</span></span> <span data-ttu-id="70540-173">這些建議旨在協助您為特定的資料庫建立最佳化彈性集區。</span><span class="sxs-lookup"><span data-stu-id="70540-173">These recommendations are intended to assist you in creating an elastic pool optimized for your specific databases.</span></span>

![動態建議](./media/sql-database-elastic-pool-create-portal/dynamic-recommendation.png)

## <a name="manage-and-monitor-an-elastic-pool"></a><span data-ttu-id="70540-175">管理及監視彈性集區</span><span class="sxs-lookup"><span data-stu-id="70540-175">Manage and monitor an elastic pool</span></span>

<span data-ttu-id="70540-176">您可以使用 Azure 入口網站來監視及管理彈性集區和集區中的資料庫。</span><span class="sxs-lookup"><span data-stu-id="70540-176">You can use the Azure portal to monitor and manage an elastic pool and the databases in the pool.</span></span> <span data-ttu-id="70540-177">從入口網站，您可以監視彈性集區與集區內資料庫的使用率。</span><span class="sxs-lookup"><span data-stu-id="70540-177">From the portal, you can monitor the utilization of an elastic pool and the databases within that pool.</span></span> <span data-ttu-id="70540-178">也可以對彈性集區進行一些變更，並且一次提交所有的變更。</span><span class="sxs-lookup"><span data-stu-id="70540-178">You can also make a set of changes to your elastic pool and submit all changes at the same time.</span></span> <span data-ttu-id="70540-179">這些變更包括新增或移除資料庫、變更您的彈性集區設定，或變更您的資料庫設定。</span><span class="sxs-lookup"><span data-stu-id="70540-179">These changes include adding or removing databases, changing your elastic pool settings, or changing your database settings.</span></span>

<span data-ttu-id="70540-180">下圖顯示彈性集區範例。</span><span class="sxs-lookup"><span data-stu-id="70540-180">The following graphic shows an example elastic pool.</span></span> <span data-ttu-id="70540-181">此檢視包括︰</span><span class="sxs-lookup"><span data-stu-id="70540-181">The view includes:</span></span>

*  <span data-ttu-id="70540-182">圖表，可供監視彈性集區和集區中內含資料庫的資源使用量。</span><span class="sxs-lookup"><span data-stu-id="70540-182">Charts for monitoring resource usage of both the elastic pool and the databases contained in the pool.</span></span>
*  <span data-ttu-id="70540-183">[設定]  集區按鈕，以對彈性集區進行變更。</span><span class="sxs-lookup"><span data-stu-id="70540-183">The **Configure** pool button to make changes to the elastic pool.</span></span>
*  <span data-ttu-id="70540-184">[建立資料庫] 按鈕，以建立資料庫並將它加入至目前的彈性集區。</span><span class="sxs-lookup"><span data-stu-id="70540-184">The **Create database** button that creates a database and adds it to the current elastic pool.</span></span>
*  <span data-ttu-id="70540-185">彈性工作，可藉由對清單中的所有資料庫執行 Transact SQL 指令碼，協助您管理大量資料庫。</span><span class="sxs-lookup"><span data-stu-id="70540-185">Elastic jobs that help you manage large numbers of databases by running Transact SQL scripts against all databases in a list.</span></span>

![集區檢視][2]

<span data-ttu-id="70540-187">您可以移至特定集區，以查看其資源使用率。</span><span class="sxs-lookup"><span data-stu-id="70540-187">You can go to a particular pool to see its resource utilization.</span></span> <span data-ttu-id="70540-188">根據預設，集區已設定為顯示過去 1 小時內的儲存體和 eDTU 使用量。</span><span class="sxs-lookup"><span data-stu-id="70540-188">By default, the pool is configured to show storage and eDTU usage for the last hour.</span></span> <span data-ttu-id="70540-189">此圖表可以設定為顯示各種時間範圍的不同度量。</span><span class="sxs-lookup"><span data-stu-id="70540-189">The chart can be configured to show different metrics over various time windows.</span></span>

1. <span data-ttu-id="70540-190">選取要使用的彈性集區。</span><span class="sxs-lookup"><span data-stu-id="70540-190">Select an elastic pool to work with.</span></span>
2. <span data-ttu-id="70540-191">[彈性集區監視] 之下的是標示為 [資源使用率] 的圖表。</span><span class="sxs-lookup"><span data-stu-id="70540-191">Under **Elastic Pool Monitoring** is a chart labeled **Resource utilization**.</span></span> <span data-ttu-id="70540-192">按一下此圖表。</span><span class="sxs-lookup"><span data-stu-id="70540-192">Click the chart.</span></span>

    ![彈性集區監視][3]

    <span data-ttu-id="70540-194">[度量] 刀鋒視窗將會開啟，顯示指定時間範圍內指定度量的詳細檢視。</span><span class="sxs-lookup"><span data-stu-id="70540-194">The **Metric** blade opens, showing a detailed view of the specified metrics over the specified time window.</span></span>   

    ![[度量] 刀鋒視窗][9]

### <a name="to-customize-the-chart-display"></a><span data-ttu-id="70540-196">自訂圖表顯示</span><span class="sxs-lookup"><span data-stu-id="70540-196">To customize the chart display</span></span>

<span data-ttu-id="70540-197">您可以編輯此圖表和 [度量] 刀鋒視窗，以顯示其他度量，例如所用的 CPU 百分比、資料 IO 百分比和記錄 IO 百分比。</span><span class="sxs-lookup"><span data-stu-id="70540-197">You can edit the chart and the metric blade to display other metrics such as CPU percentage, data IO percentage, and log IO percentage used.</span></span>

1. <span data-ttu-id="70540-198">在 [度量] 刀鋒視窗上，按一下 [編輯] 。</span><span class="sxs-lookup"><span data-stu-id="70540-198">On the metric blade, click **Edit**.</span></span>

    ![按一下 [編輯]。][6]

2. <span data-ttu-id="70540-200">在 [編輯圖表] 刀鋒視窗中，選取一個時間範圍 (過去 1 小時、今天或上一週)，或按一下 [自訂] 以選取過去兩週內的任何日期範圍。</span><span class="sxs-lookup"><span data-stu-id="70540-200">In the **Edit Chart** blade, select a time range (past hour, today, or past week), or click **custom** to select any date range in the last two weeks.</span></span> <span data-ttu-id="70540-201">選取圖表類型 (長條圖或折線圖)，再選取要監視的資源。</span><span class="sxs-lookup"><span data-stu-id="70540-201">Select the chart type (bar or line), then select the resources to monitor.</span></span>

   > [!Note]
   > <span data-ttu-id="70540-202">圖表中只能同時顯示具有相同測量單位的度量。</span><span class="sxs-lookup"><span data-stu-id="70540-202">Only metrics with the same unit of measure can be displayed in the chart at the same time.</span></span> <span data-ttu-id="70540-203">例如，如果您選取 [eDTU 百分比]，則只能選取以百分比做為測量單位的其他度量。</span><span class="sxs-lookup"><span data-stu-id="70540-203">For example, if you select "eDTU percentage" then you can only select other metrics with percentage as the unit of measure.</span></span>
   >

    ![按一下 [編輯]。](./media/sql-database-elastic-pool-manage-portal/edit-chart.png)

3. <span data-ttu-id="70540-205">然後按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="70540-205">Then click **OK**.</span></span>

## <a name="manage-and-monitor-databases-in-an-elastic-pool"></a><span data-ttu-id="70540-206">管理及監視彈性集區中的資料庫</span><span class="sxs-lookup"><span data-stu-id="70540-206">Manage and monitor databases in an elastic pool</span></span>

<span data-ttu-id="70540-207">您也可以監視個別資料庫的潛在問題。</span><span class="sxs-lookup"><span data-stu-id="70540-207">Individual databases can also be monitored for potential trouble.</span></span>

1. <span data-ttu-id="70540-208">在 [彈性資料庫監視] 之下，有一個圖表可顯示五個資料庫的度量。</span><span class="sxs-lookup"><span data-stu-id="70540-208">Under **Elastic Database Monitoring**, there is a chart that displays metrics for five databases.</span></span> <span data-ttu-id="70540-209">根據預設，此圖表會依過去一小時內的平均 eDTU 使用量顯示集區中的前 5 個資料庫。</span><span class="sxs-lookup"><span data-stu-id="70540-209">By default, the chart displays the top 5 databases in the pool by average eDTU usage in the past hour.</span></span> <span data-ttu-id="70540-210">按一下此圖表。</span><span class="sxs-lookup"><span data-stu-id="70540-210">Click the chart.</span></span>

    ![彈性集區監視][4]

2. <span data-ttu-id="70540-212">[資料庫資源使用率]  刀鋒視窗隨即出現。</span><span class="sxs-lookup"><span data-stu-id="70540-212">The **Database Resource Utilization** blade appears.</span></span> <span data-ttu-id="70540-213">這會提供集區中資料庫使用量的詳細檢視。</span><span class="sxs-lookup"><span data-stu-id="70540-213">This provides a detailed view of the database usage in the pool.</span></span> <span data-ttu-id="70540-214">使用刀鋒視窗下半部中的方格，可以選取集區中的任何資料庫，以在圖表中顯示其使用情況 (最多 5 個資料庫)。</span><span class="sxs-lookup"><span data-stu-id="70540-214">Using the grid in the lower part of the blade, you can select any databases in the pool to display its usage in the chart (up to 5 databases).</span></span> <span data-ttu-id="70540-215">也可以按一下 [編輯圖表] ，自訂圖表中顯示的度量和時間範圍。</span><span class="sxs-lookup"><span data-stu-id="70540-215">You can also customize the metrics and time window displayed in the chart by clicking **Edit chart**.</span></span>

    ![資料庫資源使用率刀鋒視窗][8]

### <a name="to-customize-the-view"></a><span data-ttu-id="70540-217">自訂檢視</span><span class="sxs-lookup"><span data-stu-id="70540-217">To customize the view</span></span>

1. <span data-ttu-id="70540-218">在 [資料庫資源使用率] 刀鋒視窗中，按一下 [編輯圖表]。</span><span class="sxs-lookup"><span data-stu-id="70540-218">In the **Database resource utilization** blade, click **Edit chart**.</span></span>

    ![按一下編輯圖表](./media/sql-database-elastic-pool-manage-portal/db-utilization-blade.png)

2. <span data-ttu-id="70540-220">在 [編輯圖表] 刀鋒視窗中，選取一個時間範圍 (過去 1 小時或過去 24 小時)，或按一下 [自訂]以選取要顯示過去 2 週內的不同一天。</span><span class="sxs-lookup"><span data-stu-id="70540-220">In the **Edit** chart blade, select a time range (past hour or past 24 hours), or click **custom** to select a different day in the past 2 weeks to display.</span></span>

    ![按一下自訂](./media/sql-database-elastic-pool-manage-portal/editchart-date-time.png)

3. <span data-ttu-id="70540-222">按一下 [比較資料庫依據]  下拉式清單，選取比較資料庫時所要使用的不同度量。</span><span class="sxs-lookup"><span data-stu-id="70540-222">Click the **Compare databases by** dropdown to select a different metric to use when comparing databases.</span></span>

    ![編輯圖表](./media/sql-database-elastic-pool-manage-portal/edit-comparison-metric.png)

### <a name="to-select-databases-to-monitor"></a><span data-ttu-id="70540-224">選取要監視的資料庫</span><span class="sxs-lookup"><span data-stu-id="70540-224">To select databases to monitor</span></span>

<span data-ttu-id="70540-225">在 [資料庫資源使用率]  刀鋒視窗的資料庫清單中，瀏覽清單中的頁面或輸入資料庫的名稱，即可找到特定的資料庫。</span><span class="sxs-lookup"><span data-stu-id="70540-225">In the database list in the **Database Resource Utilization** blade, you can find particular databases by looking through the pages in the list or by typing in the name of a database.</span></span> <span data-ttu-id="70540-226">使用此核取方塊來選取資料庫。</span><span class="sxs-lookup"><span data-stu-id="70540-226">Use the checkbox to select the database.</span></span>

![搜尋要監視的資料庫][7]


## <a name="add-an-alert-to-an-elastic-pool-resource"></a><span data-ttu-id="70540-228">將警示新增到彈性集區資源</span><span class="sxs-lookup"><span data-stu-id="70540-228">Add an alert to an elastic pool resource</span></span>

<span data-ttu-id="70540-229">您可以將規則新增到彈性集區，以在當彈性集區達到您設定的使用率閾值時，傳送電子郵件給人員或傳送警示字串到 URL 端點。</span><span class="sxs-lookup"><span data-stu-id="70540-229">You can add rules to an elastic pool that send email to people or alert strings to URL endpoints when the elastic pool hits a utilization threshold that you set up.</span></span>

<span data-ttu-id="70540-230">**將警示加入任何資源：**</span><span class="sxs-lookup"><span data-stu-id="70540-230">**To add an alert to any resource:**</span></span>

1. <span data-ttu-id="70540-231">按一下 [資源使用率] 圖表以開啟 [度量] 刀鋒視窗，按一下 [加入警示]，然後在 [加入警示規則] 刀鋒視窗中填寫資訊 ([資源] 會自動設定為使用中的集區)。</span><span class="sxs-lookup"><span data-stu-id="70540-231">Click the **Resource utilization** chart to open the **Metric** blade, click **Add alert**, and then fill out the information in the **Add an alert rule** blade (**Resource** is automatically set up to be the pool you're working with).</span></span>
2. <span data-ttu-id="70540-232">輸入可供您和收件者辨別警示的 [名稱] 和 [描述]。</span><span class="sxs-lookup"><span data-stu-id="70540-232">Type a **Name** and **Description** that identifies the alert to you and the recipients.</span></span>
3. <span data-ttu-id="70540-233">從清單中選擇要警示的 [度量]  。</span><span class="sxs-lookup"><span data-stu-id="70540-233">Choose a **Metric** that you want to alert from the list.</span></span>

    <span data-ttu-id="70540-234">圖表會以動態方式顯示該度量的資源使用量，協助您選擇閾值。</span><span class="sxs-lookup"><span data-stu-id="70540-234">The chart dynamically shows resource utilization for that metric to help you choose a threshold.</span></span>

4. <span data-ttu-id="70540-235">選擇 [條件] \(大於、小於等等) 和 [臨界值]。</span><span class="sxs-lookup"><span data-stu-id="70540-235">Choose a **Condition** (greater than, less than, etc.) and a **Threshold**.</span></span>
5. <span data-ttu-id="70540-236">選擇警示觸發程序之前，計量規則必須滿足的 [期間]。</span><span class="sxs-lookup"><span data-stu-id="70540-236">Choose a **Period** of time that the metric rule must be satisfied before the alert triggers.</span></span>
6. <span data-ttu-id="70540-237">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="70540-237">Click **OK**.</span></span>

<span data-ttu-id="70540-238">如需詳細資訊，請參閱[在 Azure 入口網站中建立 SQL Database 警示](sql-database-insights-alerts-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="70540-238">For more information, see [create SQL Database alerts in Azure portal](sql-database-insights-alerts-portal.md).</span></span>

## <a name="move-a-database-into-an-elastic-pool"></a><span data-ttu-id="70540-239">將資料庫移入彈性集區</span><span class="sxs-lookup"><span data-stu-id="70540-239">Move a database into an elastic pool</span></span>

<span data-ttu-id="70540-240">您可以從現有的集區中新增或移除資料庫。</span><span class="sxs-lookup"><span data-stu-id="70540-240">You can add or remove databases from an existing pool.</span></span> <span data-ttu-id="70540-241">資料庫可以位於其他集區。</span><span class="sxs-lookup"><span data-stu-id="70540-241">The databases can be in other pools.</span></span> <span data-ttu-id="70540-242">不過，您只可以新增位於相同邏輯伺服器上的資料庫。</span><span class="sxs-lookup"><span data-stu-id="70540-242">However, you can only add databases that are on the same logical server.</span></span>

1. <span data-ttu-id="70540-243">在集區刀鋒視窗的 [彈性資料庫] 下，按一下 [設定集區]。</span><span class="sxs-lookup"><span data-stu-id="70540-243">In the blade for the pool, under **Elastic databases** click **Configure pool**.</span></span>

    ![按一下 [設定集區]][1]

2. <span data-ttu-id="70540-245">在 [設定集區] 刀鋒視窗中，按一下 [加入集區中]。</span><span class="sxs-lookup"><span data-stu-id="70540-245">In the **Configure pool** blade, click **Add to pool**.</span></span>

    ![按一下 [新增到集區]](./media/sql-database-elastic-pool-manage-portal/add-to-pool.png)


3. <span data-ttu-id="70540-247">在 [加入資料庫]  刀鋒視窗中，選取一或多個要加入集區的資料庫。</span><span class="sxs-lookup"><span data-stu-id="70540-247">In the **Add databases** blade, select the database or databases to add to the pool.</span></span> <span data-ttu-id="70540-248">然後按一下 [選取] 。</span><span class="sxs-lookup"><span data-stu-id="70540-248">Then click **Select**.</span></span>

    ![選取要新增的資料庫](./media/sql-database-elastic-pool-manage-portal/add-databases-pool.png)

    <span data-ttu-id="70540-250">[設定集區] 刀鋒視窗現在會列出您選取要加入的資料庫，其狀態設為 [暫止]。</span><span class="sxs-lookup"><span data-stu-id="70540-250">The **Configure pool** blade now lists the database you selected to be added, with its status set to **Pending**.</span></span>

    ![擱置中的新增集區](./media/sql-database-elastic-pool-manage-portal/pending-additions.png)

3. <span data-ttu-id="70540-252">在 [設定集區] 刀鋒視窗中，按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="70540-252">In the **Configure pool blade**, click **Save**.</span></span>

    ![按一下 [儲存]。](./media/sql-database-elastic-pool-manage-portal/click-save.png)

## <a name="move-a-database-out-of-an-elastic-pool"></a><span data-ttu-id="70540-254">將資料庫移出彈性集區</span><span class="sxs-lookup"><span data-stu-id="70540-254">Move a database out of an elastic pool</span></span>

1. <span data-ttu-id="70540-255">在 [設定集區]  刀鋒視窗中，選取一或多個要移除的資料庫。</span><span class="sxs-lookup"><span data-stu-id="70540-255">In the **Configure pool** blade, select the database or databases to remove.</span></span>

    ![資料庫清單](./media/sql-database-elastic-pool-manage-portal/select-pools-removal.png)

2. <span data-ttu-id="70540-257">按一下 [從集區移除] 。</span><span class="sxs-lookup"><span data-stu-id="70540-257">Click **Remove from pool**.</span></span>

    ![資料庫清單](./media/sql-database-elastic-pool-manage-portal/click-remove.png)

    <span data-ttu-id="70540-259">[設定集區] 刀鋒視窗現在會列出您選取要移除的資料庫，其狀態設為 [暫止]。</span><span class="sxs-lookup"><span data-stu-id="70540-259">The **Configure pool** blade now lists the database you selected to be removed with its status set to **Pending**.</span></span>

    ![預覽新增和移除的資料庫](./media/sql-database-elastic-pool-manage-portal/pending-removal.png)

3. <span data-ttu-id="70540-261">在 [設定集區] 刀鋒視窗中，按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="70540-261">In the **Configure pool blade**, click **Save**.</span></span>

    ![按一下 [Save] \(儲存)。](./media/sql-database-elastic-pool-manage-portal/click-save.png)

## <a name="change-performance-settings-of-an-elastic-pool"></a><span data-ttu-id="70540-263">變更彈性集區的效能設定</span><span class="sxs-lookup"><span data-stu-id="70540-263">Change performance settings of an elastic pool</span></span>

<span data-ttu-id="70540-264">當您監視彈性集區的資源使用率時，可能會發現需要一些調整。</span><span class="sxs-lookup"><span data-stu-id="70540-264">As you monitor the resource utilization of an elastic pool, you may discover that some adjustments are needed.</span></span> <span data-ttu-id="70540-265">也許集區的效能或儲存體限制需要變更。</span><span class="sxs-lookup"><span data-stu-id="70540-265">Maybe the pool needs a change in the performance or storage limits.</span></span> <span data-ttu-id="70540-266">您可能想要變更集區中的資料庫設定。</span><span class="sxs-lookup"><span data-stu-id="70540-266">Possibly you want to change the database settings in the pool.</span></span> <span data-ttu-id="70540-267">您可以隨時變更集區設定，以在效能和成本之間取得最佳平衡。</span><span class="sxs-lookup"><span data-stu-id="70540-267">You can change the setup of the pool at any time to get the best balance of performance and cost.</span></span> <span data-ttu-id="70540-268">如需詳細資訊，請參閱[何時應該使用彈性集區？](sql-database-elastic-pool.md)</span><span class="sxs-lookup"><span data-stu-id="70540-268">See [When should an elastic pool be used?](sql-database-elastic-pool.md) for more information.</span></span>

<span data-ttu-id="70540-269">若要變更每個集區的 eDTU 和儲存體限制，以及每個資料庫的 eDTU：</span><span class="sxs-lookup"><span data-stu-id="70540-269">To change the eDTUs or storage limits per pool, and eDTUs per database:</span></span>

1. <span data-ttu-id="70540-270">開啟 [設定集區]  刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="70540-270">Open the **Configure pool** blade.</span></span>

    <span data-ttu-id="70540-271">在 [彈性集區設定] 下，使用滑桿來變更集區設定。</span><span class="sxs-lookup"><span data-stu-id="70540-271">Under **elastic pool settings**, use either slider to change the pool settings.</span></span>

    ![彈性集區資源使用量](./media/sql-database-elastic-pool-manage-portal/resize-pool.png)

2. <span data-ttu-id="70540-273">當設定變更時，則會顯示變更的每月預估成本。</span><span class="sxs-lookup"><span data-stu-id="70540-273">When the setting changes, the display shows the estimated monthly cost of the change.</span></span>

    ![更新彈性集區和新的每月成本](./media/sql-database-elastic-pool-manage-portal/pool-change-edtu.png)

## <a name="latency-of-elastic-pool-operations"></a><span data-ttu-id="70540-275">彈性集區的作業延遲</span><span class="sxs-lookup"><span data-stu-id="70540-275">Latency of elastic pool operations</span></span>
* <span data-ttu-id="70540-276">每個資料庫的最小 eDTU 數或每個資料庫的最大 eDTU 數變更作業通常在 5 分鐘內即可完成。</span><span class="sxs-lookup"><span data-stu-id="70540-276">Changing the min eDTUs per database or max eDTUs per database typically completes in 5 minutes or less.</span></span>
* <span data-ttu-id="70540-277">集區的 eDTU 變更作業，需視集區中所有資料庫使用的總空間量而定。</span><span class="sxs-lookup"><span data-stu-id="70540-277">Changing the eDTUs per pool depends on the total amount of space used by all databases in the pool.</span></span> <span data-ttu-id="70540-278">變更作業平均每 100 GB 會在 90 分鐘以內完成。</span><span class="sxs-lookup"><span data-stu-id="70540-278">Changes average 90 minutes or less per 100 GB.</span></span> <span data-ttu-id="70540-279">舉例來說，如果集區中所有資料庫使用的總空間為 200 GB，則每集區 eDTU 變更作業的預期延遲時間會少於 3 小時。</span><span class="sxs-lookup"><span data-stu-id="70540-279">For example, if the total space used by all databases in the pool is 200 GB, then the expected latency for changing the pool eDTU per pool is 3 hours or less.</span></span>

## <a name="next-steps"></a><span data-ttu-id="70540-280">後續步驟</span><span class="sxs-lookup"><span data-stu-id="70540-280">Next steps</span></span>

- <span data-ttu-id="70540-281">若要了解什麼是彈性集區，請參閱 [SQL Database 彈性集區](sql-database-elastic-pool.md)。</span><span class="sxs-lookup"><span data-stu-id="70540-281">To understand what an elastic pool is, see [SQL Database elastic pool](sql-database-elastic-pool.md).</span></span>
- <span data-ttu-id="70540-282">如需使用彈性集區的相關指導方針，請參閱[彈性集區的價格和效能考量](sql-database-elastic-pool.md)。</span><span class="sxs-lookup"><span data-stu-id="70540-282">For guidance on using elastic pools, see [Price and performance considerations for elastic pools](sql-database-elastic-pool.md).</span></span>
- <span data-ttu-id="70540-283">若要使用彈性工作對集區中任意數目的資料庫執行 Transact-SQL 指令碼，請參閱[彈性工作概觀](sql-database-elastic-jobs-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="70540-283">To use elastic jobs to run Transact-SQL scripts against any number of databases in the pool, see [Elastic jobs overview](sql-database-elastic-jobs-overview.md).</span></span>
- <span data-ttu-id="70540-284">若要對跨集區中任意數目的資料庫執行查詢，請參閱[彈性查詢概觀](sql-database-elastic-query-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="70540-284">To query across any number of databases in the pool, see [Elastic query overview](sql-database-elastic-query-overview.md).</span></span>
- <span data-ttu-id="70540-285">如需集區中任意數目的資料庫的相關交易，請參閱[彈性交易](sql-database-elastic-transactions-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="70540-285">For transactions any number of databases in the pool, see [Elastic transactions](sql-database-elastic-transactions-overview.md).</span></span>


<!--Image references-->
[1]: ./media/sql-database-elastic-pool-manage-portal/configure-pool.png
[2]: ./media/sql-database-elastic-pool-manage-portal/basic.png
[3]: ./media/sql-database-elastic-pool-manage-portal/basic-2.png
[4]: ./media/sql-database-elastic-pool-manage-portal/basic-3.png
[5]: ./media/sql-database-elastic-pool-manage-portal/elastic-jobs.png
[6]: ./media/sql-database-elastic-pool-manage-portal/edit-metric.png
[7]: ./media/sql-database-elastic-pool-manage-portal/select-dbs.png
[8]: ./media/sql-database-elastic-pool-manage-portal/db-utilization.png
[9]: ./media/sql-database-elastic-pool-manage-portal/metric.png
