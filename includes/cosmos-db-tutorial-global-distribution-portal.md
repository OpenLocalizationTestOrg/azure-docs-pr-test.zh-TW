
<span data-ttu-id="e4ce4-101">您可以在這段 Azure Friday 影片中，和 Scott Hanselman 與工程總經理 Karthik Raman 一起了解 Azure Cosmos DB 全域散發。</span><span class="sxs-lookup"><span data-stu-id="e4ce4-101">You can learn about Azure Cosmos DB global distribution in this Azure Friday video with Scott Hanselman and Principal Engineering Manager Karthik Raman.</span></span>

>[!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Planet-Scale-NoSQL-with-DocumentDB/player]  

<span data-ttu-id="e4ce4-102">如需有關 Cosmos DB 中全域資料庫複寫運作方式的詳細資訊，請參閱[使用 Cosmos DB 來全域散發資料](../articles/documentdb/documentdb-distribute-data-globally.md)。</span><span class="sxs-lookup"><span data-stu-id="e4ce4-102">For more information about how global database replication works in Cosmos DB, see [Distribute data globally with Cosmos DB](../articles/documentdb/documentdb-distribute-data-globally.md).</span></span>

## <span data-ttu-id="e4ce4-103"><a id="addregion"></a>使用 Azure 入口網站新增全球資料庫區域</span><span class="sxs-lookup"><span data-stu-id="e4ce4-103"><a id="addregion"></a>Add global database regions using the Azure Portal</span></span>
<span data-ttu-id="e4ce4-104">全球所有的 [Azure 區域][azureregions]均可使用 Azure Cosmos DB。</span><span class="sxs-lookup"><span data-stu-id="e4ce4-104">Azure Cosmos DB is available in all [Azure regions][azureregions] world-wide.</span></span> <span data-ttu-id="e4ce4-105">選取資料庫帳戶的預設一致性層級之後，您可以關聯一或多個區域 (取決於您對於預設一致性層級和全球發佈需求的選擇)。</span><span class="sxs-lookup"><span data-stu-id="e4ce4-105">After selecting the default consistency level for your database account, you can associate one or more regions (depending on your choice of default consistency level and global distribution needs).</span></span>

1. <span data-ttu-id="e4ce4-106">在 [Azure 入口網站](https://portal.azure.com/)的左列中，按一下 [Azure Cosmos DB]。</span><span class="sxs-lookup"><span data-stu-id="e4ce4-106">In the [Azure portal](https://portal.azure.com/), in the left bar, click **Azure Cosmos DB**.</span></span>
2. <span data-ttu-id="e4ce4-107">在 [Azure Cosmos DB] 刀鋒視窗中，選取要修改的資料庫帳戶。</span><span class="sxs-lookup"><span data-stu-id="e4ce4-107">In the **Azure Cosmos DB** blade, select the database account to modify.</span></span>
3. <span data-ttu-id="e4ce4-108">在帳戶刀鋒視窗中，從功能表中按一下 [全域複寫資料]。</span><span class="sxs-lookup"><span data-stu-id="e4ce4-108">In the account blade, click **Replicate data globally** from the menu.</span></span>
4. <span data-ttu-id="e4ce4-109">在 [全域複寫資料] 刀鋒視窗中，按一下地圖中的區域以選取要新增或移除的區域，然後按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="e4ce4-109">In the **Replicate data globally** blade, select the regions to add or remove by clicking regions in the map, and then click **Save**.</span></span> <span data-ttu-id="e4ce4-110">新增區域需要費用，如需詳細資訊，請參閱[定價頁面](https://azure.microsoft.com/pricing/details/documentdb/)或[使用 DocumentDB 全球發佈資料](../articles/documentdb/documentdb-distribute-data-globally.md)一文。</span><span class="sxs-lookup"><span data-stu-id="e4ce4-110">There is a cost to adding regions, see the [pricing page](https://azure.microsoft.com/pricing/details/documentdb/) or the [Distribute data globally with DocumentDB](../articles/documentdb/documentdb-distribute-data-globally.md) article for more information.</span></span>
   
    ![按一下地圖中的區域以新增或移除它們][1]
    
<span data-ttu-id="e4ce4-112">一旦您加入第二個區域，就會在入口網站中的 [全域複寫資料] 刀鋒視窗上啟用 [手動容錯移轉] 選項。</span><span class="sxs-lookup"><span data-stu-id="e4ce4-112">Once you add a second region, the **Manual Failover** option is enabled on the **Replicate data globally** blade in the portal.</span></span> <span data-ttu-id="e4ce4-113">您可以使用此選項來測試容錯移轉程序，或變更主要寫入區域。</span><span class="sxs-lookup"><span data-stu-id="e4ce4-113">You can use this option to test the failover process or change the primary write region.</span></span> <span data-ttu-id="e4ce4-114">一旦您加入第三個區域，會在相同的刀鋒視窗上啟用 [容錯移轉優先順序] 選項，因此您可以變更讀取的容錯移轉順序。</span><span class="sxs-lookup"><span data-stu-id="e4ce4-114">Once you add a third region, the **Failover Priorities** option is enabled on the same blade so that you can change the failover order for reads.</span></span>  

### <a name="selecting-global-database-regions"></a><span data-ttu-id="e4ce4-115">選取全球資料庫區域</span><span class="sxs-lookup"><span data-stu-id="e4ce4-115">Selecting global database regions</span></span>
<span data-ttu-id="e4ce4-116">設定兩個或更多區域有兩個常見案例︰</span><span class="sxs-lookup"><span data-stu-id="e4ce4-116">There are two common scenarios for configuring two or more regions:</span></span>

1. <span data-ttu-id="e4ce4-117">為使用者提供低延遲的資料存取 (無論使用者位於世界何處)</span><span class="sxs-lookup"><span data-stu-id="e4ce4-117">Delivering low-latency access to data to end users no matter where they are located around the globe</span></span>
2. <span data-ttu-id="e4ce4-118">新增業務持續性和災害復原 (BCDR) 的區域性復原功能</span><span class="sxs-lookup"><span data-stu-id="e4ce4-118">Adding regional resiliency for business continuity and disaster recovery (BCDR)</span></span>

<span data-ttu-id="e4ce4-119">若要為使用者提供低延遲，建議部署應用程式，並且在應用程式使用者所在位置的對應區域中新增 Azure Cosmos DB。</span><span class="sxs-lookup"><span data-stu-id="e4ce4-119">For delivering low-latency to end-users, it is recommended to deploy both the application and add Azure Cosmos DB in the regions thats correspond to where the application's users are located.</span></span>

<span data-ttu-id="e4ce4-120">對於 BCDR，建議根據[業務持續性和災害復原 (BCDR)：Azure 配對區域][bcdr]一文中所述的區域配對來新增區域。</span><span class="sxs-lookup"><span data-stu-id="e4ce4-120">For BCDR, it is recommended to add regions based on the region pairs described in the [Business continuity and disaster recovery (BCDR): Azure Paired Regions][bcdr] article.</span></span>

<!--

## <a id="selectwriteregion"></a>Select the write region

While all regions associated with your Cosmos DB database account can serve reads (both, single item as well as multi-item paginated reads) and queries, only one region can actively receive the write (insert, upsert, replace, delete) requests. To set the active write region, do the following  


1. In the **Azure Cosmos DB** blade, select the database account to modify.
2. In the account blade, click **Replicate data globally** from the menu.
3. In the **Replicate data globally** blade, click **Manual Failover** from the top bar.
    ![Change the write region under Azure Cosmos DB Account > Replicate data globally > Manual Failover][2]
4. Select a read region to become the new write region, click the checkbox to confirm triggering a failover, and click OK
    ![Change the write region by selecting a new region in list under Azure Cosmos DB Account > Replicate data globally > Manual Failover][3]

--->

<!--Image references-->
[1]: ./media/cosmos-db-tutorial-global-distribution-portal/azure-cosmos-db-add-region.png
[2]: ./media/cosmos-db-tutorial-global-distribution-portal/azure-cosmos-db-manual-failover-1.png
[3]: ./media/cosmos-db-tutorial-global-distribution-portal/azure-cosmos-db-manual-failover-2.png

<!--Reference style links - using these makes the source content way more readable than using inline links-->
[bcdr]: https://azure.microsoft.com/documentation/articles/best-practices-availability-paired-regions/
[consistency]: ../articles/cosmos-db/consistency-levels.md
[azureregions]: https://azure.microsoft.com/regions/#services
[offers]: https://azure.microsoft.com/pricing/details/cosmos-db/
