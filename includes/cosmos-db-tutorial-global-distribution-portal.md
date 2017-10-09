
<span data-ttu-id="f8b35-101">您可以在這段 Azure Friday 影片中，和 Scott Hanselman 與工程總經理 Karthik Raman 一起了解 Azure Cosmos DB 全域散發。</span><span class="sxs-lookup"><span data-stu-id="f8b35-101">You can learn about Azure Cosmos DB global distribution in this Azure Friday video with Scott Hanselman and Principal Engineering Manager Karthik Raman.</span></span>

>[!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Planet-Scale-NoSQL-with-DocumentDB/player]  

<span data-ttu-id="f8b35-102">如需有關 Cosmos DB 中全域資料庫複寫運作方式的詳細資訊，請參閱[使用 Cosmos DB 來全域散發資料](../articles/documentdb/documentdb-distribute-data-globally.md)。</span><span class="sxs-lookup"><span data-stu-id="f8b35-102">For more information about how global database replication works in Cosmos DB, see [Distribute data globally with Cosmos DB](../articles/documentdb/documentdb-distribute-data-globally.md).</span></span>

## <span data-ttu-id="f8b35-103"><a id="addregion"></a>新增使用 hello Azure 入口網站的全域資料庫區域</span><span class="sxs-lookup"><span data-stu-id="f8b35-103"><a id="addregion"></a>Add global database regions using hello Azure Portal</span></span>
<span data-ttu-id="f8b35-104">全球所有的 [Azure 區域][azureregions]均可使用 Azure Cosmos DB。</span><span class="sxs-lookup"><span data-stu-id="f8b35-104">Azure Cosmos DB is available in all [Azure regions][azureregions] world-wide.</span></span> <span data-ttu-id="f8b35-105">選取您的資料庫帳戶的 hello 預設一致性層級之後, 您可以將一或多個區域 （取決於您所選擇的預設一致性層級和全域發佈需求） 產生關聯。</span><span class="sxs-lookup"><span data-stu-id="f8b35-105">After selecting hello default consistency level for your database account, you can associate one or more regions (depending on your choice of default consistency level and global distribution needs).</span></span>

1. <span data-ttu-id="f8b35-106">在 hello [Azure 入口網站](https://portal.azure.com/)，在 hello 左的工具列中按一下**Azure Cosmos DB**。</span><span class="sxs-lookup"><span data-stu-id="f8b35-106">In hello [Azure portal](https://portal.azure.com/), in hello left bar, click **Azure Cosmos DB**.</span></span>
2. <span data-ttu-id="f8b35-107">在 hello **Azure Cosmos DB**刀鋒視窗中，選取 hello 資料庫帳戶 toomodify。</span><span class="sxs-lookup"><span data-stu-id="f8b35-107">In hello **Azure Cosmos DB** blade, select hello database account toomodify.</span></span>
3. <span data-ttu-id="f8b35-108">在 hello 帳戶刀鋒視窗中，按一下 **資料會進行全域複寫**hello 功能表。</span><span class="sxs-lookup"><span data-stu-id="f8b35-108">In hello account blade, click **Replicate data globally** from hello menu.</span></span>
4. <span data-ttu-id="f8b35-109">在 hello**資料會進行全域複寫**刀鋒視窗中，選取 hello 區域 tooadd 或按一下區域 hello 對應中的移除，然後按一下**儲存**。</span><span class="sxs-lookup"><span data-stu-id="f8b35-109">In hello **Replicate data globally** blade, select hello regions tooadd or remove by clicking regions in hello map, and then click **Save**.</span></span> <span data-ttu-id="f8b35-110">沒有成本 tooadding 區域，請參閱 hello[定價頁面](https://azure.microsoft.com/pricing/details/documentdb/)或 hello[全域使用 DocumentDB 資料散發](../articles/documentdb/documentdb-distribute-data-globally.md)文件以取得詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="f8b35-110">There is a cost tooadding regions, see hello [pricing page](https://azure.microsoft.com/pricing/details/documentdb/) or hello [Distribute data globally with DocumentDB](../articles/documentdb/documentdb-distribute-data-globally.md) article for more information.</span></span>
   
    ![按一下 hello 對應 tooadd 中的 hello 區域，或將它們移除][1]
    
<span data-ttu-id="f8b35-112">一旦您加入第二個區域，hello**手動容錯移轉**hello 上已啟用選項**資料會進行全域複寫**hello 入口網站中的刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="f8b35-112">Once you add a second region, hello **Manual Failover** option is enabled on hello **Replicate data globally** blade in hello portal.</span></span> <span data-ttu-id="f8b35-113">您可以使用此選項 tootest hello 容錯移轉程序，或變更 hello 主要寫入區域。</span><span class="sxs-lookup"><span data-stu-id="f8b35-113">You can use this option tootest hello failover process or change hello primary write region.</span></span> <span data-ttu-id="f8b35-114">一旦您加入第三個區域，hello**容錯移轉優先權**上啟用選項 hello 相同刀鋒視窗，因此您可以變更為讀取 hello 容錯移轉順序。</span><span class="sxs-lookup"><span data-stu-id="f8b35-114">Once you add a third region, hello **Failover Priorities** option is enabled on hello same blade so that you can change hello failover order for reads.</span></span>  

### <a name="selecting-global-database-regions"></a><span data-ttu-id="f8b35-115">選取全球資料庫區域</span><span class="sxs-lookup"><span data-stu-id="f8b35-115">Selecting global database regions</span></span>
<span data-ttu-id="f8b35-116">設定兩個或更多區域有兩個常見案例︰</span><span class="sxs-lookup"><span data-stu-id="f8b35-116">There are two common scenarios for configuring two or more regions:</span></span>

1. <span data-ttu-id="f8b35-117">傳遞低延遲存取 toodata tooend 使用者，不論它們位於周圍 hello 球體</span><span class="sxs-lookup"><span data-stu-id="f8b35-117">Delivering low-latency access toodata tooend users no matter where they are located around hello globe</span></span>
2. <span data-ttu-id="f8b35-118">新增業務持續性和災害復原 (BCDR) 的區域性復原功能</span><span class="sxs-lookup"><span data-stu-id="f8b35-118">Adding regional resiliency for business continuity and disaster recovery (BCDR)</span></span>

<span data-ttu-id="f8b35-119">對於提供低延遲 tooend 位使用者，建議您使用的 toodeploy 兩者 hello 應用程式，然後新增位於 Azure Cosmos DB hello 區域中，它會對應 toowhere hello 應用程式的使用者。</span><span class="sxs-lookup"><span data-stu-id="f8b35-119">For delivering low-latency tooend-users, it is recommended toodeploy both hello application and add Azure Cosmos DB in hello regions thats correspond toowhere hello application's users are located.</span></span>

<span data-ttu-id="f8b35-120">Bcdr，建議您使用 hello 中所述的 hello 區域配對為基礎的 tooadd 區域[業務續航力和災害復原 (BCDR): Azure 配對區域][ bcdr]發行項。</span><span class="sxs-lookup"><span data-stu-id="f8b35-120">For BCDR, it is recommended tooadd regions based on hello region pairs described in hello [Business continuity and disaster recovery (BCDR): Azure Paired Regions][bcdr] article.</span></span>

<!--

## <a id="selectwriteregion"></a>Select hello write region

While all regions associated with your Cosmos DB database account can serve reads (both, single item as well as multi-item paginated reads) and queries, only one region can actively receive hello write (insert, upsert, replace, delete) requests. tooset hello active write region, do hello following  


1. In hello **Azure Cosmos DB** blade, select hello database account toomodify.
2. In hello account blade, click **Replicate data globally** from hello menu.
3. In hello **Replicate data globally** blade, click **Manual Failover** from hello top bar.
    ![Change hello write region under Azure Cosmos DB Account > Replicate data globally > Manual Failover][2]
4. Select a read region toobecome hello new write region, click hello checkbox tooconfirm triggering a failover, and click OK
    ![Change hello write region by selecting a new region in list under Azure Cosmos DB Account > Replicate data globally > Manual Failover][3]

--->

<!--Image references-->
[1]: ./media/cosmos-db-tutorial-global-distribution-portal/azure-cosmos-db-add-region.png
[2]: ./media/cosmos-db-tutorial-global-distribution-portal/azure-cosmos-db-manual-failover-1.png
[3]: ./media/cosmos-db-tutorial-global-distribution-portal/azure-cosmos-db-manual-failover-2.png

<!--Reference style links - using these makes hello source content way more readable than using inline links-->
[bcdr]: https://azure.microsoft.com/documentation/articles/best-practices-availability-paired-regions/
[consistency]: ../articles/cosmos-db/consistency-levels.md
[azureregions]: https://azure.microsoft.com/regions/#services
[offers]: https://azure.microsoft.com/pricing/details/cosmos-db/
