## <a name="incremental-and-complete-deployments"></a><span data-ttu-id="44696-101">累加部署與完整部署</span><span class="sxs-lookup"><span data-stu-id="44696-101">Incremental and complete deployments</span></span>
<span data-ttu-id="44696-102">在部署您的資源，您可以指定 hello 部署是累加式更新或完整更新。</span><span class="sxs-lookup"><span data-stu-id="44696-102">When deploying your resources, you specify that hello deployment is either an incremental update or a complete update.</span></span> <span data-ttu-id="44696-103">hello 這兩種模式之間的主要差異是資源管理員處理 hello 資源群組中的 hello 範本中的現有資源的方式：</span><span class="sxs-lookup"><span data-stu-id="44696-103">hello primary difference between these two modes is how Resource Manager handles existing resources in hello resource group that are not in hello template:</span></span>

* <span data-ttu-id="44696-104">在完整模式中，資源管理員**刪除**hello 資源群組中存在但 hello 範本中未指定的資源。</span><span class="sxs-lookup"><span data-stu-id="44696-104">In complete mode, Resource Manager **deletes** resources that exist in hello resource group but are not specified in hello template.</span></span> 
* <span data-ttu-id="44696-105">在累加式模式中，資源管理員**會保留不變**hello 資源群組中存在但 hello 範本中未指定的資源。</span><span class="sxs-lookup"><span data-stu-id="44696-105">In incremental mode, Resource Manager **leaves unchanged** resources that exist in hello resource group but are not specified in hello template.</span></span>

<span data-ttu-id="44696-106">這兩種模式中的資源管理員會嘗試 tooprovision hello 範本中指定的所有資源。</span><span class="sxs-lookup"><span data-stu-id="44696-106">For both modes, Resource Manager attempts tooprovision all resources specified in hello template.</span></span> <span data-ttu-id="44696-107">如果 hello 資源已存在於 hello 資源群組，而且其設定維持不變，hello 操作就會導致沒有變更。</span><span class="sxs-lookup"><span data-stu-id="44696-107">If hello resource already exists in hello resource group and its settings are unchanged, hello operation results in no change.</span></span> <span data-ttu-id="44696-108">如果您變更資源的 hello 設定，這些新的設定佈建 hello 資源。</span><span class="sxs-lookup"><span data-stu-id="44696-108">If you change hello settings for a resource, hello resource is provisioned with those new settings.</span></span> <span data-ttu-id="44696-109">如果您嘗試 tooupdate hello 位置或現有的資源類型，hello 部署會失敗並發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="44696-109">If you attempt tooupdate hello location or type of an existing resource, hello deployment fails with an error.</span></span> <span data-ttu-id="44696-110">相反地，部署新的資源與 hello 位置，或輸入您需要。</span><span class="sxs-lookup"><span data-stu-id="44696-110">Instead, deploy a new resource with hello location or type that you need.</span></span>

<span data-ttu-id="44696-111">根據預設，資源管理員會使用 hello 累加模式。</span><span class="sxs-lookup"><span data-stu-id="44696-111">By default, Resource Manager uses hello incremental mode.</span></span>

<span data-ttu-id="44696-112">tooillustrate hello 差異增量和完整模式，請考慮下列案例中的 hello。</span><span class="sxs-lookup"><span data-stu-id="44696-112">tooillustrate hello difference between incremental and complete modes, consider hello following scenario.</span></span>

<span data-ttu-id="44696-113">**現有資源群組**包含︰</span><span class="sxs-lookup"><span data-stu-id="44696-113">**Existing Resource Group** contains:</span></span>

* <span data-ttu-id="44696-114">資源 A</span><span class="sxs-lookup"><span data-stu-id="44696-114">Resource A</span></span>
* <span data-ttu-id="44696-115">資源 B</span><span class="sxs-lookup"><span data-stu-id="44696-115">Resource B</span></span>
* <span data-ttu-id="44696-116">資源 C</span><span class="sxs-lookup"><span data-stu-id="44696-116">Resource C</span></span>

<span data-ttu-id="44696-117">**範本**定義：</span><span class="sxs-lookup"><span data-stu-id="44696-117">**Template** defines:</span></span>

* <span data-ttu-id="44696-118">資源 A</span><span class="sxs-lookup"><span data-stu-id="44696-118">Resource A</span></span>
* <span data-ttu-id="44696-119">資源 B</span><span class="sxs-lookup"><span data-stu-id="44696-119">Resource B</span></span>
* <span data-ttu-id="44696-120">資源 D</span><span class="sxs-lookup"><span data-stu-id="44696-120">Resource D</span></span>

<span data-ttu-id="44696-121">在部署時**累加**模式中，hello 資源群組包含：</span><span class="sxs-lookup"><span data-stu-id="44696-121">When deployed in **incremental** mode, hello resource group contains:</span></span>

* <span data-ttu-id="44696-122">資源 A</span><span class="sxs-lookup"><span data-stu-id="44696-122">Resource A</span></span>
* <span data-ttu-id="44696-123">資源 B</span><span class="sxs-lookup"><span data-stu-id="44696-123">Resource B</span></span>
* <span data-ttu-id="44696-124">資源 C</span><span class="sxs-lookup"><span data-stu-id="44696-124">Resource C</span></span>
* <span data-ttu-id="44696-125">資源 D</span><span class="sxs-lookup"><span data-stu-id="44696-125">Resource D</span></span>

<span data-ttu-id="44696-126">若部署在**完整**模式中，資源 C 會遭到刪除。</span><span class="sxs-lookup"><span data-stu-id="44696-126">When deployed in **complete** mode, Resource C is deleted.</span></span> <span data-ttu-id="44696-127">hello 資源群組包含：</span><span class="sxs-lookup"><span data-stu-id="44696-127">hello resource group contains:</span></span>

* <span data-ttu-id="44696-128">資源 A</span><span class="sxs-lookup"><span data-stu-id="44696-128">Resource A</span></span>
* <span data-ttu-id="44696-129">資源 B</span><span class="sxs-lookup"><span data-stu-id="44696-129">Resource B</span></span>
* <span data-ttu-id="44696-130">資源 D</span><span class="sxs-lookup"><span data-stu-id="44696-130">Resource D</span></span>
