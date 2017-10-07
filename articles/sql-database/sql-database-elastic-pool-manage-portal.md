---
title: "Azure 入口網站：建立及管理 SQL Database 彈性集區 | Microsoft Docs"
description: "了解 toouse hello Azure 入口網站和 SQL Database 內建智慧 toomanage、 監視器和適當的大小可延展的彈性集區 toooptimize 資料庫效能和管理成本的方式。"
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
ms.openlocfilehash: e0de952bc0c91177f64c04363630783d72435741
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-an-elastic-pool-with-hello-azure-portal"></a><span data-ttu-id="e451b-103">建立及管理彈性集區以 hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="e451b-103">Create and manage an elastic pool with hello Azure portal</span></span>
<span data-ttu-id="e451b-104">本主題說明如何 toocreate 及管理可擴充[彈性集區](sql-database-elastic-pool.md)以 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="e451b-104">This topic shows you how toocreate and manage scalable [elastic pools](sql-database-elastic-pool.md) with hello Azure portal.</span></span> <span data-ttu-id="e451b-105">您也可以建立和管理 Azure 的彈性集區與[PowerShell](sql-database-elastic-pool-manage-powershell.md)，hello REST API 或[C#](sql-database-elastic-pool-manage-csharp.md)。</span><span class="sxs-lookup"><span data-stu-id="e451b-105">You can also create and manage an Azure elastic pool with [PowerShell](sql-database-elastic-pool-manage-powershell.md), hello REST API, or [C#](sql-database-elastic-pool-manage-csharp.md).</span></span> <span data-ttu-id="e451b-106">您也可以使用 [Transact-SQL](sql-database-elastic-pool-manage-tsql.md) 來建立資料庫並將它移入和移出彈性集區。</span><span class="sxs-lookup"><span data-stu-id="e451b-106">You can also create and move databases into and out of elastic pools using [Transact-SQL](sql-database-elastic-pool-manage-tsql.md).</span></span>

## <a name="create-an-elastic-pool"></a><span data-ttu-id="e451b-107">建立彈性集區</span><span class="sxs-lookup"><span data-stu-id="e451b-107">Create an elastic pool</span></span> 

<span data-ttu-id="e451b-108">彈性集區的建立方式有兩種。</span><span class="sxs-lookup"><span data-stu-id="e451b-108">There are two ways you can create an elastic pool.</span></span> <span data-ttu-id="e451b-109">您可以進行從頭如果您知道 hello 集區設定，或啟動從 hello 服務建議。</span><span class="sxs-lookup"><span data-stu-id="e451b-109">You can do it from scratch if you know hello pool setup you want, or start with a recommendation from hello service.</span></span> <span data-ttu-id="e451b-110">SQL Database 已內建建議的彈性集區設定，如果更符合成本效益根據過去的資料庫使用遙測 hello 為您的智慧。</span><span class="sxs-lookup"><span data-stu-id="e451b-110">SQL Database has built-in intelligence that recommends an elastic pool setup if it's more cost-efficient for you based on hello past usage telemetry for your databases.</span></span>

<span data-ttu-id="e451b-111">您可以建立多個集區的伺服器上，但您無法將資料庫從不同的伺服器新增到 hello 相同的集區。</span><span class="sxs-lookup"><span data-stu-id="e451b-111">You can create multiple pools on a server, but you can't add databases from different servers into hello same pool.</span></span> 

> [!NOTE]
> <span data-ttu-id="e451b-112">彈性集區已在所有 Azure 區域中正式運作 (GA)，但印度西部除外，此區域目前提供預覽版。</span><span class="sxs-lookup"><span data-stu-id="e451b-112">Elastic pools are generally available (GA) in all Azure regions except West India where it is currently in preview.</span></span>  <span data-ttu-id="e451b-113">我們將儘速在此區域提供彈性集區的 GA。</span><span class="sxs-lookup"><span data-stu-id="e451b-113">GA of elastic pools in this region will occur as soon as possible.</span></span>
>

### <a name="step-1-create-an-elastic-pool"></a><span data-ttu-id="e451b-114">步驟 1：建立彈性集區</span><span class="sxs-lookup"><span data-stu-id="e451b-114">Step 1: Create an elastic pool</span></span>

<span data-ttu-id="e451b-115">建立從現有的彈性集區**伺服器**hello 入口網站中的分頁是 hello 最簡單方式 toomove 現有的資料庫至彈性集區。</span><span class="sxs-lookup"><span data-stu-id="e451b-115">Creating an elastic pool from an existing **server** blade in hello portal is hello easiest way toomove existing databases into an elastic pool.</span></span>

> [!NOTE]
> <span data-ttu-id="e451b-116">您也可以建立彈性集區，藉由搜尋**SQL 彈性集區**在 hello **Marketplace** ，或按一下 [ **+ 加**在 hello **SQL 彈性集區**瀏覽] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="e451b-116">You can also create an elastic pool by searching **SQL elastic pool** in hello **Marketplace** or clicking **+Add** in hello **SQL elastic pools** browse blade.</span></span> <span data-ttu-id="e451b-117">您就可以 toospecify 新的或現有的伺服器，透過此集區佈建工作流程。</span><span class="sxs-lookup"><span data-stu-id="e451b-117">You are able toospecify a new or existing server through this pool provisioning workflow.</span></span>
>
>

1. <span data-ttu-id="e451b-118">在 hello [Azure 入口網站](http://portal.azure.com/)，按一下**更多服務**  **>**  **SQL 伺服器**，然後按一下包含 hello hello 伺服器您想要 tooadd tooan 彈性集區的資料庫。</span><span class="sxs-lookup"><span data-stu-id="e451b-118">In hello [Azure portal](http://portal.azure.com/), click **More services** **>** **SQL servers**, and then click hello server that contains hello databases you want tooadd tooan elastic pool.</span></span>
2. <span data-ttu-id="e451b-119">按一下 [新增集區] 。</span><span class="sxs-lookup"><span data-stu-id="e451b-119">Click **New pool**.</span></span>

    ![加入集區 tooa 伺服器](./media/sql-database-elastic-pool-create-portal/new-pool.png)

    <span data-ttu-id="e451b-121">**-或-**</span><span class="sxs-lookup"><span data-stu-id="e451b-121">**-OR-**</span></span>

    <span data-ttu-id="e451b-122">您可能會看到訊息，指出那里建議使用 hello 伺服器的彈性集區。</span><span class="sxs-lookup"><span data-stu-id="e451b-122">You may see a message saying there are recommended elastic pools for hello server.</span></span> <span data-ttu-id="e451b-123">按一下 hello 訊息 toosee hello 建議的集區根據歷程記錄資料庫使用量遙測，然後按一下 hello 層 toosee 更多詳細資料，來自訂 hello 集區。</span><span class="sxs-lookup"><span data-stu-id="e451b-123">Click hello message toosee hello recommended pools based on historical database usage telemetry, and then click hello tier toosee more details and customize hello pool.</span></span> <span data-ttu-id="e451b-124">請參閱[了解集區建議](#understand-elastic-pool-recommendations)本主題稍後的 hello 建議開放的方式。</span><span class="sxs-lookup"><span data-stu-id="e451b-124">See [Understand pool recommendations](#understand-elastic-pool-recommendations) later in this topic for how hello recommendation is made.</span></span>

    ![建議的集區](./media/sql-database-elastic-pool-create-portal/recommended-pool.png)

3. <span data-ttu-id="e451b-126">hello**彈性集區**刀鋒視窗隨即出現，這是用來指定 hello 設定集區。</span><span class="sxs-lookup"><span data-stu-id="e451b-126">hello **elastic pool** blade appears, which is where you specify hello settings for your pool.</span></span> <span data-ttu-id="e451b-127">如果您按下**新集區**hello 先前步驟中，在 hello 定價層是**標準**選取預設並沒有資料庫。</span><span class="sxs-lookup"><span data-stu-id="e451b-127">If you clicked **New pool** in hello previous step, hello pricing tier is **Standard** by default and no databases is selected.</span></span> <span data-ttu-id="e451b-128">您可以建立空的集區，或指定一組現有的資料庫，從該伺服器 toomove 到 hello 的集區。</span><span class="sxs-lookup"><span data-stu-id="e451b-128">You can create an empty pool, or specify a set of existing databases from that server toomove into hello pool.</span></span> <span data-ttu-id="e451b-129">如果您要建立建議的集區，hello 建議定價層，效能設定的資料庫清單預先填入，但您還是可以變更它們。</span><span class="sxs-lookup"><span data-stu-id="e451b-129">If you are creating a recommended pool, hello recommended pricing tier, performance settings, and list of databases are prepopulated, but you can still change them.</span></span>

    ![設定彈性集區](./media/sql-database-elastic-pool-create-portal/configure-elastic-pool.png)

4. <span data-ttu-id="e451b-131">指定 hello 彈性集區的名稱，或將它保留為 hello 預設值。</span><span class="sxs-lookup"><span data-stu-id="e451b-131">Specify a name for hello elastic pool, or leave it as hello default.</span></span>

### <a name="step-2-choose-a-pricing-tier"></a><span data-ttu-id="e451b-132">步驟 2：選擇定價層</span><span class="sxs-lookup"><span data-stu-id="e451b-132">Step 2: Choose a pricing tier</span></span>

<span data-ttu-id="e451b-133">hello 集區的定價層會決定 hello 功能可用 toohello elastics hello 集區，以及 hello 最大數目 (eDTU 最大值) 的 edtu 數目及儲存體 (Gb) 可用 tooeach 資料庫中。</span><span class="sxs-lookup"><span data-stu-id="e451b-133">hello pool's pricing tier determines hello features available toohello elastics in hello pool, and hello maximum number of eDTUs (eDTU MAX), and storage (GBs) available tooeach database.</span></span> <span data-ttu-id="e451b-134">如需詳細資訊，請參閱服務層。</span><span class="sxs-lookup"><span data-stu-id="e451b-134">For details, see Service Tiers.</span></span>

<span data-ttu-id="e451b-135">toochange hello 定價層級的 hello 集區中，按一下**定價層**，按一下 定價的層，然後再按一下 hello**選取**。</span><span class="sxs-lookup"><span data-stu-id="e451b-135">toochange hello pricing tier for hello pool, click **Pricing tier**, click hello pricing tier you want, and then click **Select**.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e451b-136">您選擇定價層的 hello，即可認可您的變更後，當**確定**在 hello 最後一個步驟中，您必須能夠 toochange hello 定價層的 hello 集區。</span><span class="sxs-lookup"><span data-stu-id="e451b-136">After you choose hello pricing tier and commit your changes by clicking **OK** in hello last step, you won't be able toochange hello pricing tier of hello pool.</span></span> <span data-ttu-id="e451b-137">toochange hello 現有彈性集區的定價層、 建立 hello 所需的定價層中的彈性集區及移轉 hello 資料庫 toothis 新集區。</span><span class="sxs-lookup"><span data-stu-id="e451b-137">toochange hello pricing tier for an existing elastic pool, create an elastic pool in hello desired pricing tier and migrate hello databases toothis new pool.</span></span>
>

![選取定價層](./media/sql-database-elastic-pool-create-portal/pricing-tier.png)

### <a name="step-3-configure-hello-pool"></a><span data-ttu-id="e451b-139">步驟 3： 設定 hello 集區</span><span class="sxs-lookup"><span data-stu-id="e451b-139">Step 3: Configure hello pool</span></span>

<span data-ttu-id="e451b-140">設定後 hello 定價層，請按一下設定集區，其中您加入資料庫、 設定集區 Edtu 與儲存體 (集區 Gb)，而且您設定 hello elastics 的 hello min 和 max Edtu hello 集區中。</span><span class="sxs-lookup"><span data-stu-id="e451b-140">After setting hello pricing tier, click Configure pool where you add databases, set pool eDTUs and storage (pool GBs), and where you set hello min and max eDTUs for hello elastics in hello pool.</span></span>

1. <span data-ttu-id="e451b-141">按一下 [設定集區] </span><span class="sxs-lookup"><span data-stu-id="e451b-141">Click **Configure pool**</span></span>
2. <span data-ttu-id="e451b-142">選取您想要 tooadd toohello 集區的 hello 資料庫。</span><span class="sxs-lookup"><span data-stu-id="e451b-142">Select hello databases you want tooadd toohello pool.</span></span> <span data-ttu-id="e451b-143">建立 hello 集區時，這個步驟是選擇性的。</span><span class="sxs-lookup"><span data-stu-id="e451b-143">This step is optional while creating hello pool.</span></span> <span data-ttu-id="e451b-144">建立 hello 集區之後，可以加入資料庫。</span><span class="sxs-lookup"><span data-stu-id="e451b-144">Databases can be added after hello pool has been created.</span></span>
    <span data-ttu-id="e451b-145">按一下 tooadd 資料庫**將資料庫加入**，按一下您想 tooadd，，，然後按一下hello hello 資料庫**選取** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="e451b-145">tooadd databases, click **Add database**, click hello databases that you want tooadd, and then click hello **Select** button.</span></span>

    ![新增資料庫](./media/sql-database-elastic-pool-create-portal/add-databases.png)

    <span data-ttu-id="e451b-147">如果您正在使用的 hello 資料庫的歷程記錄使用量遙測資料不足，hello**估計 eDTU 與 GB 使用量**圖形和 hello**實際 eDTU 使用量**橫條圖更新 toohelp 進行設定決策。</span><span class="sxs-lookup"><span data-stu-id="e451b-147">If hello databases you're working with have enough historical usage telemetry, hello **Estimated eDTU and GB usage** graph and hello **Actual eDTU usage** bar chart update toohelp you make configuration decisions.</span></span> <span data-ttu-id="e451b-148">此外，hello 服務可能會提供建議訊息 toohelp 您適當的大小 hello 集區。</span><span class="sxs-lookup"><span data-stu-id="e451b-148">Also, hello service may give you a recommendation message toohelp you right-size hello pool.</span></span> <span data-ttu-id="e451b-149">請參閱 [動態建議](#understand-elastic-pool-recommendations)。</span><span class="sxs-lookup"><span data-stu-id="e451b-149">See [Dynamic Recommendations](#understand-elastic-pool-recommendations).</span></span>

3. <span data-ttu-id="e451b-150">使用 hello hello 控制項**設定集區**tooexplore 設定頁面上，並設定您的集區。</span><span class="sxs-lookup"><span data-stu-id="e451b-150">Use hello controls on hello **Configure pool** page tooexplore settings and configure your pool.</span></span> <span data-ttu-id="e451b-151">如需各服務層限制的詳細資訊，請參閱[彈性集區限制](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools)；如需如何決定彈性集區適當大小的詳細指導方針，請參閱[彈性集區的價格和效能考量](sql-database-elastic-pool.md)。</span><span class="sxs-lookup"><span data-stu-id="e451b-151">See [Elastic pools limits](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools) for more detail about limits for each service tier, and see [Price and performance considerations for elastic pools](sql-database-elastic-pool.md) for detailed guidance on right-sizing an elastic pool.</span></span> <span data-ttu-id="e451b-152">如需集區設定的詳細資訊，請參閱[彈性集區屬性](sql-database-elastic-pool.md#database-properties-for-pooled-databases)。</span><span class="sxs-lookup"><span data-stu-id="e451b-152">For more information about pool settings, see [Elastic pool properties](sql-database-elastic-pool.md#database-properties-for-pooled-databases).</span></span>

    ![設定彈性集區](./media/sql-database-elastic-pool-create-portal/configure-performance.png)

4. <span data-ttu-id="e451b-154">按一下**選取**在 hello**設定集區**刀鋒視窗中的變更設定之後。</span><span class="sxs-lookup"><span data-stu-id="e451b-154">Click **Select** in hello **Configure Pool** blade after changing settings.</span></span>
5. <span data-ttu-id="e451b-155">按一下**確定**toocreate hello 集區。</span><span class="sxs-lookup"><span data-stu-id="e451b-155">Click **OK** toocreate hello pool.</span></span>

## <a name="understand-elastic-pool-recommendations"></a><span data-ttu-id="e451b-156">了解彈性集區建議</span><span class="sxs-lookup"><span data-stu-id="e451b-156">Understand elastic pool recommendations</span></span>

<span data-ttu-id="e451b-157">hello SQL Database 服務會評估使用量記錄，並且更符合成本效益比使用單一資料庫時，建議一或多個集區。</span><span class="sxs-lookup"><span data-stu-id="e451b-157">hello SQL Database service evaluates usage history and recommends one or more pools when it is more cost-effective than using single databases.</span></span> <span data-ttu-id="e451b-158">每個建議設定是最佳的方式調整 hello 集區的 hello 伺服器資料庫的唯一子集。</span><span class="sxs-lookup"><span data-stu-id="e451b-158">Each recommendation is configured with a unique subset of hello server's databases that best fit hello pool.</span></span>

![建議的集區](./media/sql-database-elastic-pool-create-portal/recommended-pool.png)  

<span data-ttu-id="e451b-160">hello 集區建議包含：</span><span class="sxs-lookup"><span data-stu-id="e451b-160">hello pool recommendation comprises:</span></span>

- <span data-ttu-id="e451b-161">（Basic、 Standard、 Premium 或 Premium RS） 的 hello 集區的定價層</span><span class="sxs-lookup"><span data-stu-id="e451b-161">A pricing tier for hello pool (Basic, Standard, Premium, or Premium RS)</span></span>
- <span data-ttu-id="e451b-162">適當的 [集區 eDTU]  \(也稱為每一集區的最大 eDTU)</span><span class="sxs-lookup"><span data-stu-id="e451b-162">Appropriate **POOL eDTUs** (also called Max eDTUs per pool)</span></span>
- <span data-ttu-id="e451b-163">hello **eDTU 最大**和**eDTU 下限**每個資料庫</span><span class="sxs-lookup"><span data-stu-id="e451b-163">hello **eDTU MAX** and **eDTU Min** per database</span></span>
- <span data-ttu-id="e451b-164">hello hello 集區的建議資料庫清單</span><span class="sxs-lookup"><span data-stu-id="e451b-164">hello list of recommended databases for hello pool</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e451b-165">hello 服務會 hello 前 30 天的遙測考量時，建議您將集區。</span><span class="sxs-lookup"><span data-stu-id="e451b-165">hello service takes hello last 30 days of telemetry into account when recommending pools.</span></span> <span data-ttu-id="e451b-166">彈性集區的候選項目會視為資料庫 toobe，它必須存在至少 7 天。</span><span class="sxs-lookup"><span data-stu-id="e451b-166">For a database toobe considered as a candidate for an elastic pool, it must exist for at least 7 days.</span></span> <span data-ttu-id="e451b-167">已在彈性集區中的資料庫不會被視為彈性集區建議候選項目。</span><span class="sxs-lookup"><span data-stu-id="e451b-167">Databases that are already in an elastic pool are not considered as candidates for elastic pool recommendations.</span></span>
>

<span data-ttu-id="e451b-168">hello 服務會評估資源需求和成本效益的移動 hello 單一資料庫中每個服務層到集區的 hello 相同階層。</span><span class="sxs-lookup"><span data-stu-id="e451b-168">hello service evaluates resource needs and cost effectiveness of moving hello single databases in each service tier into pools of hello same tier.</span></span> <span data-ttu-id="e451b-169">例如，會評估伺服器上的所有 Standard 資料庫是否適合 Standard 彈性集區。</span><span class="sxs-lookup"><span data-stu-id="e451b-169">For example, all Standard databases on a server are assessed for their fit into a Standard Elastic Pool.</span></span> <span data-ttu-id="e451b-170">這表示 hello 服務不會跨階層的建議，例如標準資料庫移動到 Premium 資料庫。</span><span class="sxs-lookup"><span data-stu-id="e451b-170">This means hello service does not make cross-tier recommendations such as moving a Standard database into a Premium pool.</span></span>

<span data-ttu-id="e451b-171">新增後資料庫 toohello 集區，建議動態產生 hello hello 資料庫，您已選取的歷程記錄的使用量為基礎。</span><span class="sxs-lookup"><span data-stu-id="e451b-171">After adding databases toohello pool, recommendations are dynamically generated based on hello historical usage of hello databases you have selected.</span></span> <span data-ttu-id="e451b-172">這些建議會出現在 hello eDTU 與 GB 使用量圖表，橫幅中的建議頂端的 hello hello**設定集區**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="e451b-172">These recommendations are shown in hello eDTU and GB usage chart and in a recommendation banner at hello top of hello **Configure pool** blade.</span></span> <span data-ttu-id="e451b-173">這些建議是預定的 tooassist 建立彈性集區中適合您特定的資料庫。</span><span class="sxs-lookup"><span data-stu-id="e451b-173">These recommendations are intended tooassist you in creating an elastic pool optimized for your specific databases.</span></span>

![動態建議](./media/sql-database-elastic-pool-create-portal/dynamic-recommendation.png)

## <a name="manage-and-monitor-an-elastic-pool"></a><span data-ttu-id="e451b-175">管理及監視彈性集區</span><span class="sxs-lookup"><span data-stu-id="e451b-175">Manage and monitor an elastic pool</span></span>

<span data-ttu-id="e451b-176">您可以使用 Azure 入口網站 toomonitor hello 和管理彈性集區和 hello hello 集區中的資料庫。</span><span class="sxs-lookup"><span data-stu-id="e451b-176">You can use hello Azure portal toomonitor and manage an elastic pool and hello databases in hello pool.</span></span> <span data-ttu-id="e451b-177">從 hello 入口網站，您可以監視 hello 善用彈性集區和該集區中的 hello 資料庫。</span><span class="sxs-lookup"><span data-stu-id="e451b-177">From hello portal, you can monitor hello utilization of an elastic pool and hello databases within that pool.</span></span> <span data-ttu-id="e451b-178">您也會使一組變更 tooyour 彈性集區並送出所有在 hello 變更相同的時間。</span><span class="sxs-lookup"><span data-stu-id="e451b-178">You can also make a set of changes tooyour elastic pool and submit all changes at hello same time.</span></span> <span data-ttu-id="e451b-179">這些變更包括新增或移除資料庫、變更您的彈性集區設定，或變更您的資料庫設定。</span><span class="sxs-lookup"><span data-stu-id="e451b-179">These changes include adding or removing databases, changing your elastic pool settings, or changing your database settings.</span></span>

<span data-ttu-id="e451b-180">hello 下列圖形顯示範例彈性集區。</span><span class="sxs-lookup"><span data-stu-id="e451b-180">hello following graphic shows an example elastic pool.</span></span> <span data-ttu-id="e451b-181">hello 檢視包括：</span><span class="sxs-lookup"><span data-stu-id="e451b-181">hello view includes:</span></span>

*  <span data-ttu-id="e451b-182">監視資源使用量的 hello 彈性集區和 hello 集區中所包含的 hello 資料庫圖表。</span><span class="sxs-lookup"><span data-stu-id="e451b-182">Charts for monitoring resource usage of both hello elastic pool and hello databases contained in hello pool.</span></span>
*  <span data-ttu-id="e451b-183">hello**設定**集區 按鈕 toomake 變更 toohello 彈性集區。</span><span class="sxs-lookup"><span data-stu-id="e451b-183">hello **Configure** pool button toomake changes toohello elastic pool.</span></span>
*  <span data-ttu-id="e451b-184">hello**建立資料庫**按鈕會建立資料庫，並將它加入 toohello 目前彈性集區。</span><span class="sxs-lookup"><span data-stu-id="e451b-184">hello **Create database** button that creates a database and adds it toohello current elastic pool.</span></span>
*  <span data-ttu-id="e451b-185">彈性工作，可藉由對清單中的所有資料庫執行 Transact SQL 指令碼，協助您管理大量資料庫。</span><span class="sxs-lookup"><span data-stu-id="e451b-185">Elastic jobs that help you manage large numbers of databases by running Transact SQL scripts against all databases in a list.</span></span>

![集區檢視][2]

<span data-ttu-id="e451b-187">您可以移 tooa 特定集區 toosee 其資源使用量。</span><span class="sxs-lookup"><span data-stu-id="e451b-187">You can go tooa particular pool toosee its resource utilization.</span></span> <span data-ttu-id="e451b-188">根據預設，hello 集區是已設定的 tooshow 儲存體和 eDTU 使用量 hello 過去一小時內。</span><span class="sxs-lookup"><span data-stu-id="e451b-188">By default, hello pool is configured tooshow storage and eDTU usage for hello last hour.</span></span> <span data-ttu-id="e451b-189">hello 圖表可以設定的 tooshow 不同度量經由各種時間視窗。</span><span class="sxs-lookup"><span data-stu-id="e451b-189">hello chart can be configured tooshow different metrics over various time windows.</span></span>

1. <span data-ttu-id="e451b-190">選取與彈性集區 toowork。</span><span class="sxs-lookup"><span data-stu-id="e451b-190">Select an elastic pool toowork with.</span></span>
2. <span data-ttu-id="e451b-191">[彈性集區監視] 之下的是標示為 [資源使用率] 的圖表。</span><span class="sxs-lookup"><span data-stu-id="e451b-191">Under **Elastic Pool Monitoring** is a chart labeled **Resource utilization**.</span></span> <span data-ttu-id="e451b-192">按一下 hello 圖表。</span><span class="sxs-lookup"><span data-stu-id="e451b-192">Click hello chart.</span></span>

    ![彈性集區監視][3]

    <span data-ttu-id="e451b-194">hello**度量**刀鋒視窗中開啟，顯示 hello 的詳細的檢視透過 hello 指定的時段指定度量。</span><span class="sxs-lookup"><span data-stu-id="e451b-194">hello **Metric** blade opens, showing a detailed view of hello specified metrics over hello specified time window.</span></span>   

    ![[度量] 刀鋒視窗][9]

### <a name="toocustomize-hello-chart-display"></a><span data-ttu-id="e451b-196">toocustomize hello 圖表顯示</span><span class="sxs-lookup"><span data-stu-id="e451b-196">toocustomize hello chart display</span></span>

<span data-ttu-id="e451b-197">您可以編輯 hello 圖表和 hello 計量刀鋒伺服器 toodisplay 其他度量資訊，例如 CPU 百分比、 資料 IO 百分比及使用的記錄 IO 百分比。</span><span class="sxs-lookup"><span data-stu-id="e451b-197">You can edit hello chart and hello metric blade toodisplay other metrics such as CPU percentage, data IO percentage, and log IO percentage used.</span></span>

1. <span data-ttu-id="e451b-198">在 hello 計量刀鋒伺服器上按一下**編輯**。</span><span class="sxs-lookup"><span data-stu-id="e451b-198">On hello metric blade, click **Edit**.</span></span>

    ![按一下 [編輯]。][6]

2. <span data-ttu-id="e451b-200">在 hello**編輯圖表**刀鋒視窗中，選取時間範圍 （過去一小時，目前或上週），或按一下**自訂**tooselect 任何日期範圍 hello 過去兩週。</span><span class="sxs-lookup"><span data-stu-id="e451b-200">In hello **Edit Chart** blade, select a time range (past hour, today, or past week), or click **custom** tooselect any date range in hello last two weeks.</span></span> <span data-ttu-id="e451b-201">選取 hello 圖表類型 （橫條或線條），然後選取 hello 資源 toomonitor。</span><span class="sxs-lookup"><span data-stu-id="e451b-201">Select hello chart type (bar or line), then select hello resources toomonitor.</span></span>

   > [!Note]
   > <span data-ttu-id="e451b-202">只有以 hello hello 中可顯示相同的量值單位的度量圖表 hello 在相同的時間。</span><span class="sxs-lookup"><span data-stu-id="e451b-202">Only metrics with hello same unit of measure can be displayed in hello chart at hello same time.</span></span> <span data-ttu-id="e451b-203">比方說，如果您選取 「 eDTU 百分比 」 然後您只能選取其他度量，以百分比為 hello 測量單位。</span><span class="sxs-lookup"><span data-stu-id="e451b-203">For example, if you select "eDTU percentage" then you can only select other metrics with percentage as hello unit of measure.</span></span>
   >

    ![按一下 [編輯]。](./media/sql-database-elastic-pool-manage-portal/edit-chart.png)

3. <span data-ttu-id="e451b-205">然後按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="e451b-205">Then click **OK**.</span></span>

## <a name="manage-and-monitor-databases-in-an-elastic-pool"></a><span data-ttu-id="e451b-206">管理及監視彈性集區中的資料庫</span><span class="sxs-lookup"><span data-stu-id="e451b-206">Manage and monitor databases in an elastic pool</span></span>

<span data-ttu-id="e451b-207">您也可以監視個別資料庫的潛在問題。</span><span class="sxs-lookup"><span data-stu-id="e451b-207">Individual databases can also be monitored for potential trouble.</span></span>

1. <span data-ttu-id="e451b-208">在 [彈性資料庫監視] 之下，有一個圖表可顯示五個資料庫的度量。</span><span class="sxs-lookup"><span data-stu-id="e451b-208">Under **Elastic Database Monitoring**, there is a chart that displays metrics for five databases.</span></span> <span data-ttu-id="e451b-209">根據預設，hello 圖表會顯示 hello 前 5 資料庫 hello 集區中 hello 平均 eDTU 使用量過去一小時。</span><span class="sxs-lookup"><span data-stu-id="e451b-209">By default, hello chart displays hello top 5 databases in hello pool by average eDTU usage in hello past hour.</span></span> <span data-ttu-id="e451b-210">按一下 hello 圖表。</span><span class="sxs-lookup"><span data-stu-id="e451b-210">Click hello chart.</span></span>

    ![彈性集區監視][4]

2. <span data-ttu-id="e451b-212">hello**資料庫資源使用量**刀鋒視窗隨即出現。</span><span class="sxs-lookup"><span data-stu-id="e451b-212">hello **Database Resource Utilization** blade appears.</span></span> <span data-ttu-id="e451b-213">這提供 hello hello 集區中的資料庫使用方式的詳細的檢視。</span><span class="sxs-lookup"><span data-stu-id="e451b-213">This provides a detailed view of hello database usage in hello pool.</span></span> <span data-ttu-id="e451b-214">使用 hello hello 的 hello 刀鋒視窗的下半部的方格，您可以選取任何資料庫中 hello 集區 toodisplay hello 圖表 （向上 too5 資料庫） 中的其使用情形。</span><span class="sxs-lookup"><span data-stu-id="e451b-214">Using hello grid in hello lower part of hello blade, you can select any databases in hello pool toodisplay its usage in hello chart (up too5 databases).</span></span> <span data-ttu-id="e451b-215">您也可以自訂 hello 度量和時間範圍顯示 hello 圖表中，依序按一下**編輯圖表**。</span><span class="sxs-lookup"><span data-stu-id="e451b-215">You can also customize hello metrics and time window displayed in hello chart by clicking **Edit chart**.</span></span>

    ![資料庫資源使用率刀鋒視窗][8]

### <a name="toocustomize-hello-view"></a><span data-ttu-id="e451b-217">toocustomize hello 檢視</span><span class="sxs-lookup"><span data-stu-id="e451b-217">toocustomize hello view</span></span>

1. <span data-ttu-id="e451b-218">在 hello**資料庫資源使用率**刀鋒視窗中，按一下 **編輯圖表**。</span><span class="sxs-lookup"><span data-stu-id="e451b-218">In hello **Database resource utilization** blade, click **Edit chart**.</span></span>

    ![按一下編輯圖表](./media/sql-database-elastic-pool-manage-portal/db-utilization-blade.png)

2. <span data-ttu-id="e451b-220">在 hello**編輯**圖表刀鋒視窗中，選取時間範圍 （過去一小時或過去 24 小時），或按一下**自訂**tooselect 不同每天在過去 2 週 toodisplay hello。</span><span class="sxs-lookup"><span data-stu-id="e451b-220">In hello **Edit** chart blade, select a time range (past hour or past 24 hours), or click **custom** tooselect a different day in hello past 2 weeks toodisplay.</span></span>

    ![按一下自訂](./media/sql-database-elastic-pool-manage-portal/editchart-date-time.png)

3. <span data-ttu-id="e451b-222">按一下 hello**比較資料庫**下拉式 tooselect 不同度量 toouse 比較資料庫時。</span><span class="sxs-lookup"><span data-stu-id="e451b-222">Click hello **Compare databases by** dropdown tooselect a different metric toouse when comparing databases.</span></span>

    ![編輯 hello 圖表](./media/sql-database-elastic-pool-manage-portal/edit-comparison-metric.png)

### <a name="tooselect-databases-toomonitor"></a><span data-ttu-id="e451b-224">tooselect 資料庫 toomonitor</span><span class="sxs-lookup"><span data-stu-id="e451b-224">tooselect databases toomonitor</span></span>

<span data-ttu-id="e451b-225">在 hello 資料庫清單中 hello**資料庫資源使用量**刀鋒視窗中，您可以找到特定的資料庫，藉由查詢透過 hello 清單中的 hello 頁面或在 hello 的資料庫名稱中輸入。</span><span class="sxs-lookup"><span data-stu-id="e451b-225">In hello database list in hello **Database Resource Utilization** blade, you can find particular databases by looking through hello pages in hello list or by typing in hello name of a database.</span></span> <span data-ttu-id="e451b-226">使用 hello 核取方塊 tooselect hello 資料庫。</span><span class="sxs-lookup"><span data-stu-id="e451b-226">Use hello checkbox tooselect hello database.</span></span>

![搜尋資料庫 toomonitor][7]


## <a name="add-an-alert-tooan-elastic-pool-resource"></a><span data-ttu-id="e451b-228">加入警示 tooan 彈性集區資源</span><span class="sxs-lookup"><span data-stu-id="e451b-228">Add an alert tooan elastic pool resource</span></span>

<span data-ttu-id="e451b-229">您可以加入規則 tooan 彈性集區 hello 彈性集區達到您設定使用率閾值時傳送電子郵件 toopeople 或警示字串 tooURL 端點。</span><span class="sxs-lookup"><span data-stu-id="e451b-229">You can add rules tooan elastic pool that send email toopeople or alert strings tooURL endpoints when hello elastic pool hits a utilization threshold that you set up.</span></span>

<span data-ttu-id="e451b-230">**tooadd 警示 tooany 資源：**</span><span class="sxs-lookup"><span data-stu-id="e451b-230">**tooadd an alert tooany resource:**</span></span>

1. <span data-ttu-id="e451b-231">按一下 hello**資源使用率**圖表 tooopen hello**度量**刀鋒視窗中，按一下 **新增警示**，然後填入 hello 中的 hello 資訊**加入警示規則**刀鋒視窗 (**資源**自動設定 toobe hello 集區正在使用)。</span><span class="sxs-lookup"><span data-stu-id="e451b-231">Click hello **Resource utilization** chart tooopen hello **Metric** blade, click **Add alert**, and then fill out hello information in hello **Add an alert rule** blade (**Resource** is automatically set up toobe hello pool you're working with).</span></span>
2. <span data-ttu-id="e451b-232">輸入**名稱**和**描述**可識別 hello 警示 tooyou 和 hello 收件者。</span><span class="sxs-lookup"><span data-stu-id="e451b-232">Type a **Name** and **Description** that identifies hello alert tooyou and hello recipients.</span></span>
3. <span data-ttu-id="e451b-233">選擇**度量**想 tooalert 從 hello 清單。</span><span class="sxs-lookup"><span data-stu-id="e451b-233">Choose a **Metric** that you want tooalert from hello list.</span></span>

    <span data-ttu-id="e451b-234">hello 圖表以動態方式顯示該度量 toohelp 資源使用情況選擇臨界值。</span><span class="sxs-lookup"><span data-stu-id="e451b-234">hello chart dynamically shows resource utilization for that metric toohelp you choose a threshold.</span></span>

4. <span data-ttu-id="e451b-235">選擇 [條件] \(大於、小於等等) 和 [臨界值]。</span><span class="sxs-lookup"><span data-stu-id="e451b-235">Choose a **Condition** (greater than, less than, etc.) and a **Threshold**.</span></span>
5. <span data-ttu-id="e451b-236">選擇**期間**的 hello 度量的時間必須符合規則之前 hello 警示觸發程序。</span><span class="sxs-lookup"><span data-stu-id="e451b-236">Choose a **Period** of time that hello metric rule must be satisfied before hello alert triggers.</span></span>
6. <span data-ttu-id="e451b-237">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="e451b-237">Click **OK**.</span></span>

<span data-ttu-id="e451b-238">如需詳細資訊，請參閱[在 Azure 入口網站中建立 SQL Database 警示](sql-database-insights-alerts-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="e451b-238">For more information, see [create SQL Database alerts in Azure portal](sql-database-insights-alerts-portal.md).</span></span>

## <a name="move-a-database-into-an-elastic-pool"></a><span data-ttu-id="e451b-239">將資料庫移入彈性集區</span><span class="sxs-lookup"><span data-stu-id="e451b-239">Move a database into an elastic pool</span></span>

<span data-ttu-id="e451b-240">您可以從現有的集區中新增或移除資料庫。</span><span class="sxs-lookup"><span data-stu-id="e451b-240">You can add or remove databases from an existing pool.</span></span> <span data-ttu-id="e451b-241">hello 資料庫可以位於其他集區。</span><span class="sxs-lookup"><span data-stu-id="e451b-241">hello databases can be in other pools.</span></span> <span data-ttu-id="e451b-242">不過，您只可以加入會在 hello 相同的資料庫邏輯伺服器。</span><span class="sxs-lookup"><span data-stu-id="e451b-242">However, you can only add databases that are on hello same logical server.</span></span>

1. <span data-ttu-id="e451b-243">在 hello 刀鋒視窗中的 hello 集區，在**彈性資料庫**按一下**設定集區**。</span><span class="sxs-lookup"><span data-stu-id="e451b-243">In hello blade for hello pool, under **Elastic databases** click **Configure pool**.</span></span>

    ![按一下 [設定集區]][1]

2. <span data-ttu-id="e451b-245">在 hello**設定集區**刀鋒視窗中，按一下 **新增 toopool**。</span><span class="sxs-lookup"><span data-stu-id="e451b-245">In hello **Configure pool** blade, click **Add toopool**.</span></span>

    ![按一下 新增 toopool](./media/sql-database-elastic-pool-manage-portal/add-to-pool.png)


3. <span data-ttu-id="e451b-247">在 hello**新增資料庫**刀鋒視窗中，選取 hello 資料庫或資料庫 tooadd toohello 集區。</span><span class="sxs-lookup"><span data-stu-id="e451b-247">In hello **Add databases** blade, select hello database or databases tooadd toohello pool.</span></span> <span data-ttu-id="e451b-248">然後按一下 [選取] 。</span><span class="sxs-lookup"><span data-stu-id="e451b-248">Then click **Select**.</span></span>

    ![選取資料庫 tooadd](./media/sql-database-elastic-pool-manage-portal/add-databases-pool.png)

    <span data-ttu-id="e451b-250">hello**設定集區**現在清單 hello 選取 toobe 加太設定其狀態的資料庫刀鋒視窗**暫止**。</span><span class="sxs-lookup"><span data-stu-id="e451b-250">hello **Configure pool** blade now lists hello database you selected toobe added, with its status set too**Pending**.</span></span>

    ![擱置中的新增集區](./media/sql-database-elastic-pool-manage-portal/pending-additions.png)

3. <span data-ttu-id="e451b-252">在 hello**設定集區 刀鋒視窗**，按一下 **儲存**。</span><span class="sxs-lookup"><span data-stu-id="e451b-252">In hello **Configure pool blade**, click **Save**.</span></span>

    ![按一下 [Save] \(儲存)。](./media/sql-database-elastic-pool-manage-portal/click-save.png)

## <a name="move-a-database-out-of-an-elastic-pool"></a><span data-ttu-id="e451b-254">將資料庫移出彈性集區</span><span class="sxs-lookup"><span data-stu-id="e451b-254">Move a database out of an elastic pool</span></span>

1. <span data-ttu-id="e451b-255">在 hello**設定集區**刀鋒視窗中，選取 hello 資料庫或資料庫 tooremove。</span><span class="sxs-lookup"><span data-stu-id="e451b-255">In hello **Configure pool** blade, select hello database or databases tooremove.</span></span>

    ![資料庫清單](./media/sql-database-elastic-pool-manage-portal/select-pools-removal.png)

2. <span data-ttu-id="e451b-257">按一下 [從集區移除] 。</span><span class="sxs-lookup"><span data-stu-id="e451b-257">Click **Remove from pool**.</span></span>

    ![資料庫清單](./media/sql-database-elastic-pool-manage-portal/click-remove.png)

    <span data-ttu-id="e451b-259">hello**設定集區**刀鋒視窗中列出 hello 選取 toobe 其狀態太設定中移除的資料庫現在**暫止**。</span><span class="sxs-lookup"><span data-stu-id="e451b-259">hello **Configure pool** blade now lists hello database you selected toobe removed with its status set too**Pending**.</span></span>

    ![預覽新增和移除的資料庫](./media/sql-database-elastic-pool-manage-portal/pending-removal.png)

3. <span data-ttu-id="e451b-261">在 hello**設定集區 刀鋒視窗**，按一下 **儲存**。</span><span class="sxs-lookup"><span data-stu-id="e451b-261">In hello **Configure pool blade**, click **Save**.</span></span>

    ![按一下 [Save] \(儲存)。](./media/sql-database-elastic-pool-manage-portal/click-save.png)

## <a name="change-performance-settings-of-an-elastic-pool"></a><span data-ttu-id="e451b-263">變更彈性集區的效能設定</span><span class="sxs-lookup"><span data-stu-id="e451b-263">Change performance settings of an elastic pool</span></span>

<span data-ttu-id="e451b-264">當您監視 hello 彈性集區的資源使用情況，您會發現一些調整所需。</span><span class="sxs-lookup"><span data-stu-id="e451b-264">As you monitor hello resource utilization of an elastic pool, you may discover that some adjustments are needed.</span></span> <span data-ttu-id="e451b-265">或許 hello 集區需要 hello 效能或存放裝置限制中的變更。</span><span class="sxs-lookup"><span data-stu-id="e451b-265">Maybe hello pool needs a change in hello performance or storage limits.</span></span> <span data-ttu-id="e451b-266">可能是您想 toochange hello hello 集區中的資料庫設定。</span><span class="sxs-lookup"><span data-stu-id="e451b-266">Possibly you want toochange hello database settings in hello pool.</span></span> <span data-ttu-id="e451b-267">您可以變更在任何時間 tooget hello 最佳平衡效能及成本的 hello 集區的 hello 安裝程式。</span><span class="sxs-lookup"><span data-stu-id="e451b-267">You can change hello setup of hello pool at any time tooget hello best balance of performance and cost.</span></span> <span data-ttu-id="e451b-268">如需詳細資訊，請參閱[何時應該使用彈性集區？](sql-database-elastic-pool.md)</span><span class="sxs-lookup"><span data-stu-id="e451b-268">See [When should an elastic pool be used?](sql-database-elastic-pool.md) for more information.</span></span>

<span data-ttu-id="e451b-269">toochange hello Edtu 或儲存體限制每個集區，以及每個資料庫的 edtu 數目：</span><span class="sxs-lookup"><span data-stu-id="e451b-269">toochange hello eDTUs or storage limits per pool, and eDTUs per database:</span></span>

1. <span data-ttu-id="e451b-270">開啟 hello**設定集區**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="e451b-270">Open hello **Configure pool** blade.</span></span>

    <span data-ttu-id="e451b-271">在下**彈性集區設定**，使用其中一個滑桿 toochange hello 集區設定。</span><span class="sxs-lookup"><span data-stu-id="e451b-271">Under **elastic pool settings**, use either slider toochange hello pool settings.</span></span>

    ![彈性集區資源使用量](./media/sql-database-elastic-pool-manage-portal/resize-pool.png)

2. <span data-ttu-id="e451b-273">當 hello 設定變更時，hello 顯示 hello 每月的估計成本 hello 變更。</span><span class="sxs-lookup"><span data-stu-id="e451b-273">When hello setting changes, hello display shows hello estimated monthly cost of hello change.</span></span>

    ![更新彈性集區和新的每月成本](./media/sql-database-elastic-pool-manage-portal/pool-change-edtu.png)

## <a name="latency-of-elastic-pool-operations"></a><span data-ttu-id="e451b-275">彈性集區的作業延遲</span><span class="sxs-lookup"><span data-stu-id="e451b-275">Latency of elastic pool operations</span></span>
* <span data-ttu-id="e451b-276">變更每個資料庫或最大每個資料庫的 Edtu hello min Edtu 通常完成在 5 分鐘或更短。</span><span class="sxs-lookup"><span data-stu-id="e451b-276">Changing hello min eDTUs per database or max eDTUs per database typically completes in 5 minutes or less.</span></span>
* <span data-ttu-id="e451b-277">變更每個集區 edtu 數 （hello） 取決於 hello hello 集區中的所有資料庫所使用的空間數量總計。</span><span class="sxs-lookup"><span data-stu-id="e451b-277">Changing hello eDTUs per pool depends on hello total amount of space used by all databases in hello pool.</span></span> <span data-ttu-id="e451b-278">變更作業平均每 100 GB 會在 90 分鐘以內完成。</span><span class="sxs-lookup"><span data-stu-id="e451b-278">Changes average 90 minutes or less per 100 GB.</span></span> <span data-ttu-id="e451b-279">比方說，如果使用的總空間的 hello hello 集區中的所有資料庫都為 200 GB，則 hello 預期的變更 hello 每個集區的集區 eDTU 延遲都為 3 小時或更少。</span><span class="sxs-lookup"><span data-stu-id="e451b-279">For example, if hello total space used by all databases in hello pool is 200 GB, then hello expected latency for changing hello pool eDTU per pool is 3 hours or less.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e451b-280">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e451b-280">Next steps</span></span>

- <span data-ttu-id="e451b-281">何種彈性集區，請參閱的 toounderstand [SQL Database 彈性集區](sql-database-elastic-pool.md)。</span><span class="sxs-lookup"><span data-stu-id="e451b-281">toounderstand what an elastic pool is, see [SQL Database elastic pool](sql-database-elastic-pool.md).</span></span>
- <span data-ttu-id="e451b-282">如需使用彈性集區的相關指導方針，請參閱[彈性集區的價格和效能考量](sql-database-elastic-pool.md)。</span><span class="sxs-lookup"><span data-stu-id="e451b-282">For guidance on using elastic pools, see [Price and performance considerations for elastic pools](sql-database-elastic-pool.md).</span></span>
- <span data-ttu-id="e451b-283">toouse 彈性作業 toorun Transact SQL 指令碼針對任意數目的資料庫中 hello 集區，請參閱[彈性的工作概觀](sql-database-elastic-jobs-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="e451b-283">toouse elastic jobs toorun Transact-SQL scripts against any number of databases in hello pool, see [Elastic jobs overview](sql-database-elastic-jobs-overview.md).</span></span>
- <span data-ttu-id="e451b-284">tooquery 跨任意數目的資料庫中 hello 集區，請參閱[彈性的查詢概觀](sql-database-elastic-query-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="e451b-284">tooquery across any number of databases in hello pool, see [Elastic query overview](sql-database-elastic-query-overview.md).</span></span>
- <span data-ttu-id="e451b-285">交易任意數目的資料庫中 hello 集區，請參閱[彈性交易](sql-database-elastic-transactions-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="e451b-285">For transactions any number of databases in hello pool, see [Elastic transactions](sql-database-elastic-transactions-overview.md).</span></span>


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
