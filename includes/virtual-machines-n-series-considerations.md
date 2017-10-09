## <a name="deployment-considerations"></a><span data-ttu-id="89117-101">部署考量</span><span class="sxs-lookup"><span data-stu-id="89117-101">Deployment considerations</span></span>

* <span data-ttu-id="89117-102">如需了解 N 系列 VM 的可用性，請參閱[依區域提供的產品](https://azure.microsoft.com/en-us/regions/services/)。</span><span class="sxs-lookup"><span data-stu-id="89117-102">For availability of N-series VMs, see [Products available by region](https://azure.microsoft.com/en-us/regions/services/).</span></span>

* <span data-ttu-id="89117-103">N 系列 Vm 只能部署在 hello Resource Manager 部署模型。</span><span class="sxs-lookup"><span data-stu-id="89117-103">N-series VMs can only be deployed in hello Resource Manager deployment model.</span></span>

* <span data-ttu-id="89117-104">當 N 系列 VM 使用建立 hello Azure 入口網站上 hello**基本概念**刀鋒視窗中，選取**VM 磁碟類型**的**HDD**。</span><span class="sxs-lookup"><span data-stu-id="89117-104">When creating an N-series VM using hello Azure portal, on hello **Basics** blade, select a **VM disk type** of **HDD**.</span></span> <span data-ttu-id="89117-105">可用的 N 數列 toochoose 大小 hello**大小**刀鋒視窗中，按一下 **檢視所有**。</span><span class="sxs-lookup"><span data-stu-id="89117-105">toochoose an available N-series size, on hello **Size** blade, click **View all**.</span></span>

* <span data-ttu-id="89117-106">N 系列 VM 不支援以 Azure 進階儲存體為後盾的 VM 磁碟。</span><span class="sxs-lookup"><span data-stu-id="89117-106">N-series VMs do not support VM disks that are backed by Azure Premium storage.</span></span>

* <span data-ttu-id="89117-107">如果您想 toodeploy 多個 N 系列 Vm，請考慮隨用隨付訂用帳戶或其他購買選項。</span><span class="sxs-lookup"><span data-stu-id="89117-107">If you want toodeploy more than a few N-series VMs, consider a pay-as-you-go subscription or other purchase options.</span></span> <span data-ttu-id="89117-108">如果您使用 [Azure 免費帳戶](https://azure.microsoft.com/free/)，您只能使用有限數目的 Azure 計算核心。</span><span class="sxs-lookup"><span data-stu-id="89117-108">If you're using an [Azure free account](https://azure.microsoft.com/free/), you can use only a limited number of Azure compute cores.</span></span>

* <span data-ttu-id="89117-109">您可能會在您的 Azure 訂閱，需要 tooincrease hello 核心配額 （每個區域），並增加 hello 個別 NC 或 NV 核心配額。</span><span class="sxs-lookup"><span data-stu-id="89117-109">You might need tooincrease hello cores quota (per region) in your Azure subscription, and increase hello separate quota for NC or NV cores.</span></span> <span data-ttu-id="89117-110">toorequest 配額增加[開啟線上客戶支援要求](../articles/azure-supportability/how-to-create-azure-support-request.md)不收費。</span><span class="sxs-lookup"><span data-stu-id="89117-110">toorequest a quota increase, [open an online customer support request](../articles/azure-supportability/how-to-create-azure-support-request.md) at no charge.</span></span> <span data-ttu-id="89117-111">預設限制會視您的訂用帳戶類別而有所不同。</span><span class="sxs-lookup"><span data-stu-id="89117-111">Default limits may vary depending on your subscription category.</span></span>

* <span data-ttu-id="89117-112">您可以部署在 N 系列 Vm 的一個 VM 映像為 hello [Azure Data Science 虛擬機器](../articles/machine-learning/machine-learning-data-science-virtual-machine-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="89117-112">One VM image you can deploy on N-series VMs is hello [Azure Data Science Virtual Machine](../articles/machine-learning/machine-learning-data-science-virtual-machine-overview.md).</span></span> <span data-ttu-id="89117-113">hello Data Science 虛擬機器會預先安裝，以及設定許多常用的資料科學和深層學習工具。</span><span class="sxs-lookup"><span data-stu-id="89117-113">hello Data Science Virtual Machine preinstalls and configures many popular data science and deep learning tools.</span></span> <span data-ttu-id="89117-114">它也會針對 NC 執行個體預先安裝 NVIDIA Tesla GPU 驅動程式。</span><span class="sxs-lookup"><span data-stu-id="89117-114">It also preinstalls NVIDIA Tesla GPU drivers for NC instances.</span></span>





