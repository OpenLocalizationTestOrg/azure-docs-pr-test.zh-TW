


## <a name="attach-an-empty-disk"></a><span data-ttu-id="8fc65-101">連接空的磁碟</span><span class="sxs-lookup"><span data-stu-id="8fc65-101">Attach an empty disk</span></span>
<span data-ttu-id="8fc65-102">連接空磁碟是簡單的方式 tooadd 資料磁碟，因為 Azure 會為您建立 hello.vhd 檔案，並將它儲存在 hello 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="8fc65-102">Attaching an empty disk is a simple way tooadd a data disk, because Azure creates hello .vhd file for you and stores it in hello storage account.</span></span>

1. <span data-ttu-id="8fc65-103">按一下**虛擬機器 （傳統）**，，然後選取 hello 適當的 VM。</span><span class="sxs-lookup"><span data-stu-id="8fc65-103">Click **Virtual Machines (classic)**, and then select hello appropriate VM.</span></span>

2. <span data-ttu-id="8fc65-104">在 hello 設定 功能表，按一下 **磁碟**。</span><span class="sxs-lookup"><span data-stu-id="8fc65-104">In hello Settings menu, click **Disks**.</span></span>

   ![連接新的空磁碟](./media/howto-attach-disk-windows-linux/menudisksattachnew.png)

3. <span data-ttu-id="8fc65-106">Hello 命令列上，按一下**附加新**。</span><span class="sxs-lookup"><span data-stu-id="8fc65-106">On hello command bar, click **Attach new**.</span></span>  
    <span data-ttu-id="8fc65-107">hello**附加新磁碟** 對話方塊隨即出現。</span><span class="sxs-lookup"><span data-stu-id="8fc65-107">hello **Attach new disk** dialog box appears.</span></span>

    ![附加新的磁碟](./media/howto-attach-disk-windows-linux/newdiskdetail.png)

    <span data-ttu-id="8fc65-109">填寫下列資訊的 hello:</span><span class="sxs-lookup"><span data-stu-id="8fc65-109">Fill in hello following information:</span></span>
    - <span data-ttu-id="8fc65-110">在**檔案名稱**、 接受 hello 預設名稱，或輸入另一種用於 hello.vhd 檔案。</span><span class="sxs-lookup"><span data-stu-id="8fc65-110">In **File Name**, accept hello default name or type another one for hello .vhd file.</span></span> <span data-ttu-id="8fc65-111">hello 資料磁碟會使用自動產生的名稱，即使您輸入 hello.vhd 檔案的另一個名稱。</span><span class="sxs-lookup"><span data-stu-id="8fc65-111">hello data disk uses an automatically generated name, even if you type another name for hello .vhd file.</span></span>
    - <span data-ttu-id="8fc65-112">選取 hello**類型**hello 資料磁碟。</span><span class="sxs-lookup"><span data-stu-id="8fc65-112">Select hello **Type** of hello data disk.</span></span> <span data-ttu-id="8fc65-113">所有虛擬機器皆支援標準磁碟。</span><span class="sxs-lookup"><span data-stu-id="8fc65-113">All virtual machines support standard disks.</span></span> <span data-ttu-id="8fc65-114">許多虛擬機器也支援進階磁碟。</span><span class="sxs-lookup"><span data-stu-id="8fc65-114">Many virtual machines also support premium disks.</span></span>
    - <span data-ttu-id="8fc65-115">選取 hello**大小 (GB)** hello 資料磁碟。</span><span class="sxs-lookup"><span data-stu-id="8fc65-115">Select hello **Size (GB)** of hello data disk.</span></span>
    - <span data-ttu-id="8fc65-116">在 [主機快取] 中選擇 [無] 或 [唯讀]。</span><span class="sxs-lookup"><span data-stu-id="8fc65-116">For **Host caching**, choose none or Read Only.</span></span>
    - <span data-ttu-id="8fc65-117">按一下 [確定] toofinish。</span><span class="sxs-lookup"><span data-stu-id="8fc65-117">Click OK toofinish.</span></span>

4. <span data-ttu-id="8fc65-118">Hello 資料磁碟會建立並附加之後，它被列在 hello VM hello 磁碟 區段中。</span><span class="sxs-lookup"><span data-stu-id="8fc65-118">After hello data disk is created and attached, it's listed in hello disks section of hello VM.</span></span>

   ![成功連結新的空白資料磁碟](./media/howto-attach-disk-windows-linux/newdiskemptysuccessful.png)

> [!NOTE]
> <span data-ttu-id="8fc65-120">新增資料磁碟之後，您會需要 toolog toohello VM 上的，並使其可以用於初始化 hello 磁碟。</span><span class="sxs-lookup"><span data-stu-id="8fc65-120">After you add a data disk, you need toolog on toohello VM and initialize hello disk so that it can be used.</span></span>

## <a name="how-to-attach-an-existing-disk"></a><span data-ttu-id="8fc65-121">做法：連接現有磁碟</span><span class="sxs-lookup"><span data-stu-id="8fc65-121">How to: Attach an existing disk</span></span>
<span data-ttu-id="8fc65-122">連接現有磁碟要求您在儲存體帳戶中需要有可用的 .vhd。</span><span class="sxs-lookup"><span data-stu-id="8fc65-122">Attaching an existing disk requires that you have a .vhd available in a storage account.</span></span> <span data-ttu-id="8fc65-123">使用 hello [Add-azurevhd](https://msdn.microsoft.com/library/azure/dn495173.aspx) cmdlet tooupload hello.vhd 檔案 toohello 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="8fc65-123">Use hello [Add-AzureVhd](https://msdn.microsoft.com/library/azure/dn495173.aspx) cmdlet tooupload hello .vhd file toohello storage account.</span></span> <span data-ttu-id="8fc65-124">在您建立並上傳 hello.vhd 檔案之後，您可以將它附加 tooa VM。</span><span class="sxs-lookup"><span data-stu-id="8fc65-124">After you've created and uploaded hello .vhd file, you can attach it tooa VM.</span></span>

1. <span data-ttu-id="8fc65-125">按一下**虛擬機器 （傳統）**，，然後選取 hello 適當的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="8fc65-125">Click **Virtual Machines (classic)**, and then select hello appropriate virtual machine.</span></span>

2. <span data-ttu-id="8fc65-126">在 hello 設定 功能表，按一下 **磁碟**。</span><span class="sxs-lookup"><span data-stu-id="8fc65-126">In hello Settings menu, click **Disks**.</span></span>

3. <span data-ttu-id="8fc65-127">Hello 命令列上，按一下**附加現有**。</span><span class="sxs-lookup"><span data-stu-id="8fc65-127">On hello command bar, click **Attach existing**.</span></span>

    ![連結資料磁碟](./media/howto-attach-disk-windows-linux/menudisksattachexisting.png)

4. <span data-ttu-id="8fc65-129">按一下 [位置]。</span><span class="sxs-lookup"><span data-stu-id="8fc65-129">Click **Location**.</span></span> <span data-ttu-id="8fc65-130">顯示 hello 可用儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="8fc65-130">hello available storage accounts display.</span></span> <span data-ttu-id="8fc65-131">接下來，從所列帳戶中選取適當的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="8fc65-131">Next, select an appropriate storage account from those listed.</span></span>

    ![提供磁碟儲存體帳戶](./media/howto-attach-disk-windows-linux/existdiskstorageaccounts.png)

5. <span data-ttu-id="8fc65-133">**儲存體帳戶**會保有一或多個包含磁碟機 (VHD) 的容器。</span><span class="sxs-lookup"><span data-stu-id="8fc65-133">A **Storage account** holds one or more containers that contain disk drives (vhds).</span></span> <span data-ttu-id="8fc65-134">選取所列出 hello 適當的容器。</span><span class="sxs-lookup"><span data-stu-id="8fc65-134">Select hello appropriate container from those listed.</span></span>

    ![提供 virtual-machines-windows 的容器](./media/howto-attach-disk-windows-linux/existdiskcontainers.png)

6. <span data-ttu-id="8fc65-136">hello **vhd**窗格會列出保留在 hello 容器中的 hello 磁碟機。</span><span class="sxs-lookup"><span data-stu-id="8fc65-136">hello **vhds** panel lists hello disk drives held in hello container.</span></span> <span data-ttu-id="8fc65-137">按一下其中一個 hello 磁碟，然後按一下選取。</span><span class="sxs-lookup"><span data-stu-id="8fc65-137">Click one of hello disks, and then click Select.</span></span>

    ![提供 virtual-machines-windows 的磁碟映像](./media/howto-attach-disk-windows-linux/existdiskvhds.png)

7. <span data-ttu-id="8fc65-139">hello**將現有磁碟**面板同樣地，會顯示以 hello 位置包含 hello 儲存體帳戶、 容器和選取的硬碟 (vhd) tooadd toohello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="8fc65-139">hello **Attach existing disk** panel displays again, with hello location containing hello storage account, container, and selected hard disk (vhd) tooadd toohello virtual machine.</span></span>

  <span data-ttu-id="8fc65-140">設定**主機快取**toonone 或讀取，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="8fc65-140">Set **Host caching** toonone or Read only, then click OK.</span></span>

    ![成功連接資料磁碟](./media/howto-attach-disk-windows-linux/exisitingdisksuccessful.png)
