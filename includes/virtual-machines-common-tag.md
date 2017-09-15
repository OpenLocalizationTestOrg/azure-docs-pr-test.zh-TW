


## <a name="tagging-a-virtual-machine-through-templates"></a><span data-ttu-id="bb6c6-101">透過範本標記虛擬機器</span><span class="sxs-lookup"><span data-stu-id="bb6c6-101">Tagging a Virtual Machine through Templates</span></span>
<span data-ttu-id="bb6c6-102">首先，我們來看一下透過範本進行標記。</span><span class="sxs-lookup"><span data-stu-id="bb6c6-102">First, let’s look at tagging through templates.</span></span> <span data-ttu-id="bb6c6-103">[此範本](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-tags) 將標記置於下列資源上：運算 (虛擬機器)、儲存體 (儲存體帳戶) 和網路 (公用 IP 位址、虛擬網路和網路介面)。</span><span class="sxs-lookup"><span data-stu-id="bb6c6-103">[This template](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-tags) places tags on the following resources: Compute (Virtual Machine), Storage (Storage Account), and Network (Public IP Address, Virtual Network, and Network Interface).</span></span> <span data-ttu-id="bb6c6-104">這個範本適用於 Windows VM，但也可改寫成適用於 Linux VM。</span><span class="sxs-lookup"><span data-stu-id="bb6c6-104">This template is for a Windows VM but can be adapted for Linux VMs.</span></span>

<span data-ttu-id="bb6c6-105">按一下[範本連結](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-tags)中的 [部署至 Azure] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="bb6c6-105">Click the **Deploy to Azure** button from the [template link](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-tags).</span></span> <span data-ttu-id="bb6c6-106">這會瀏覽至 [Azure 入口網站](https://portal.azure.com/) ，以便您部署此範本。</span><span class="sxs-lookup"><span data-stu-id="bb6c6-106">This will navigate to the [Azure portal](https://portal.azure.com/) where you can deploy this template.</span></span>

![使用標記的簡單部署](./media/virtual-machines-common-tag/deploy-to-azure-tags.png)

<span data-ttu-id="bb6c6-108">此範本包含下列標記：「部門」、「應用程式」以及「建立者」。</span><span class="sxs-lookup"><span data-stu-id="bb6c6-108">This template includes the following tags: *Department*, *Application*, and *Created By*.</span></span> <span data-ttu-id="bb6c6-109">如果您想要不同的標記名稱，您可以直接在範本中新增/編輯這些標記。</span><span class="sxs-lookup"><span data-stu-id="bb6c6-109">You can add/edit these tags directly in the template if you would like different tag names.</span></span>

![範本中的 Azure 標記](./media/virtual-machines-common-tag/azure-tags-in-a-template.png)

<span data-ttu-id="bb6c6-111">如您所見，標記會定義為成對的「索引鍵/值」，並會以冒號 (:) 分隔。</span><span class="sxs-lookup"><span data-stu-id="bb6c6-111">As you can see, the tags are defined as key/value pairs, separated by a colon (:).</span></span> <span data-ttu-id="bb6c6-112">標記必須以這種格式定義：</span><span class="sxs-lookup"><span data-stu-id="bb6c6-112">The tags must be defined in this format:</span></span>

        “tags”: {
            “Key1” : ”Value1”,
            “Key2” : “Value2”
        }

<span data-ttu-id="bb6c6-113">在您使用您所選擇的標籤完成編輯後，儲存範本檔案。</span><span class="sxs-lookup"><span data-stu-id="bb6c6-113">Save the template file after you finish editing it with the tags of your choice.</span></span>

<span data-ttu-id="bb6c6-114">接著，在 [編輯參數  ] 區段中，您可以填寫標記的值。</span><span class="sxs-lookup"><span data-stu-id="bb6c6-114">Next, in the **Edit Parameters** section, you can fill out the values for your tags.</span></span>

![在 Azure 入口網站中編輯標記](./media/virtual-machines-common-tag/edit-tags-in-azure-portal.png)

<span data-ttu-id="bb6c6-116">按一下 [建立  ]，使用您的標記值來部署此範本。</span><span class="sxs-lookup"><span data-stu-id="bb6c6-116">Click **Create** to deploy this template with your tag values.</span></span>

## <a name="tagging-through-the-portal"></a><span data-ttu-id="bb6c6-117">透過入口網站進行標記</span><span class="sxs-lookup"><span data-stu-id="bb6c6-117">Tagging through the Portal</span></span>
<span data-ttu-id="bb6c6-118">使用標記建立您的資源之後，您可以在入口網站中檢視、新增和刪除標記。</span><span class="sxs-lookup"><span data-stu-id="bb6c6-118">After creating your resources with tags, you can view, add, and delete tags in the portal.</span></span>

<span data-ttu-id="bb6c6-119">選取標記圖示以檢視您的標記：</span><span class="sxs-lookup"><span data-stu-id="bb6c6-119">Select the tags icon to view your tags:</span></span>

![Azure 入口網站中的標記圖示](./media/virtual-machines-common-tag/azure-portal-tags-icon.png)

<span data-ttu-id="bb6c6-121">透過入口網站定義自己的索引鍵/值組，以加入新標記並加以儲存。</span><span class="sxs-lookup"><span data-stu-id="bb6c6-121">Add a new tag through the portal by defining your own Key/Value pair, and save it.</span></span>

![在 Azure 入口網站中新增標記](./media/virtual-machines-common-tag/azure-portal-add-new-tag.png)

<span data-ttu-id="bb6c6-123">新標籤現在應出現在您的資源的標記清單中。</span><span class="sxs-lookup"><span data-stu-id="bb6c6-123">Your new tag should now appear in the list of tags for your resource.</span></span>

![Azure 入口網站中儲存的新標記](./media/virtual-machines-common-tag/azure-portal-saved-new-tag.png)

