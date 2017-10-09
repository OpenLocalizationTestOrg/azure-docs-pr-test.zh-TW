


## <a name="tagging-a-virtual-machine-through-templates"></a><span data-ttu-id="c331d-101">透過範本標記虛擬機器</span><span class="sxs-lookup"><span data-stu-id="c331d-101">Tagging a Virtual Machine through Templates</span></span>
<span data-ttu-id="c331d-102">首先，我們來看一下透過範本進行標記。</span><span class="sxs-lookup"><span data-stu-id="c331d-102">First, let’s look at tagging through templates.</span></span> <span data-ttu-id="c331d-103">[此範本](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-tags)標記置於 hello 下列資源： 運算 （虛擬機器）、 儲存體 （儲存體帳戶） 和網路 （公用 IP 位址、 虛擬網路，以及網路介面）。</span><span class="sxs-lookup"><span data-stu-id="c331d-103">[This template](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-tags) places tags on hello following resources: Compute (Virtual Machine), Storage (Storage Account), and Network (Public IP Address, Virtual Network, and Network Interface).</span></span> <span data-ttu-id="c331d-104">這個範本適用於 Windows VM，但也可改寫成適用於 Linux VM。</span><span class="sxs-lookup"><span data-stu-id="c331d-104">This template is for a Windows VM but can be adapted for Linux VMs.</span></span>

<span data-ttu-id="c331d-105">按一下 hello**部署 tooAzure**按鈕 hello[範本連結](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-tags)。</span><span class="sxs-lookup"><span data-stu-id="c331d-105">Click hello **Deploy tooAzure** button from hello [template link](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-tags).</span></span> <span data-ttu-id="c331d-106">這會瀏覽 toohello [Azure 入口網站](https://portal.azure.com/)您可以在其中部署此範本。</span><span class="sxs-lookup"><span data-stu-id="c331d-106">This will navigate toohello [Azure portal](https://portal.azure.com/) where you can deploy this template.</span></span>

![使用標記的簡單部署](./media/virtual-machines-common-tag/deploy-to-azure-tags.png)

<span data-ttu-id="c331d-108">此範本包含下列標記的 hello:*部門*，*應用程式*，和*建立者*。</span><span class="sxs-lookup"><span data-stu-id="c331d-108">This template includes hello following tags: *Department*, *Application*, and *Created By*.</span></span> <span data-ttu-id="c331d-109">您可以新增/編輯直接在 hello 範本中的這些標記如果您想要不同的標記名稱。</span><span class="sxs-lookup"><span data-stu-id="c331d-109">You can add/edit these tags directly in hello template if you would like different tag names.</span></span>

![範本中的 Azure 標記](./media/virtual-machines-common-tag/azure-tags-in-a-template.png)

<span data-ttu-id="c331d-111">如您所見，hello 標記會定義為索引鍵/值組，以冒號 （:） 分隔。</span><span class="sxs-lookup"><span data-stu-id="c331d-111">As you can see, hello tags are defined as key/value pairs, separated by a colon (:).</span></span> <span data-ttu-id="c331d-112">hello 標記必須先定義格式如下：</span><span class="sxs-lookup"><span data-stu-id="c331d-112">hello tags must be defined in this format:</span></span>

        “tags”: {
            “Key1” : ”Value1”,
            “Key2” : “Value2”
        }

<span data-ttu-id="c331d-113">在您完成編輯您所選擇的 hello 標記後，請儲存 hello 範本檔案。</span><span class="sxs-lookup"><span data-stu-id="c331d-113">Save hello template file after you finish editing it with hello tags of your choice.</span></span>

<span data-ttu-id="c331d-114">接下來，在 hello**編輯參數** 區段中，您可以填寫 hello 值的標籤。</span><span class="sxs-lookup"><span data-stu-id="c331d-114">Next, in hello **Edit Parameters** section, you can fill out hello values for your tags.</span></span>

![在 Azure 入口網站中編輯標記](./media/virtual-machines-common-tag/edit-tags-in-azure-portal.png)

<span data-ttu-id="c331d-116">按一下**建立**toodeploy 標記值與此範本。</span><span class="sxs-lookup"><span data-stu-id="c331d-116">Click **Create** toodeploy this template with your tag values.</span></span>

## <a name="tagging-through-hello-portal"></a><span data-ttu-id="c331d-117">標記透過 hello 入口網站</span><span class="sxs-lookup"><span data-stu-id="c331d-117">Tagging through hello Portal</span></span>
<span data-ttu-id="c331d-118">建立您的資源具有標記之後, 您可以檢視、 新增和刪除 hello 入口網站中的標記。</span><span class="sxs-lookup"><span data-stu-id="c331d-118">After creating your resources with tags, you can view, add, and delete tags in hello portal.</span></span>

<span data-ttu-id="c331d-119">選取 hello 標記圖示 tooview 標記：</span><span class="sxs-lookup"><span data-stu-id="c331d-119">Select hello tags icon tooview your tags:</span></span>

![Azure 入口網站中的標記圖示](./media/virtual-machines-common-tag/azure-portal-tags-icon.png)

<span data-ttu-id="c331d-121">透過 hello 入口網站的新標記新增定義您自己的索引鍵/值組，並將其儲存。</span><span class="sxs-lookup"><span data-stu-id="c331d-121">Add a new tag through hello portal by defining your own Key/Value pair, and save it.</span></span>

![在 Azure 入口網站中新增標記](./media/virtual-machines-common-tag/azure-portal-add-new-tag.png)

<span data-ttu-id="c331d-123">您的新標籤現在應該會出現在 hello 清單中的資源標記。</span><span class="sxs-lookup"><span data-stu-id="c331d-123">Your new tag should now appear in hello list of tags for your resource.</span></span>

![Azure 入口網站中儲存的新標記](./media/virtual-machines-common-tag/azure-portal-saved-new-tag.png)

