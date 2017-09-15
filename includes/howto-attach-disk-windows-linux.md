


## <a name="attach-an-empty-disk"></a><span data-ttu-id="0535c-101">連接空的磁碟</span><span class="sxs-lookup"><span data-stu-id="0535c-101">Attach an empty disk</span></span>
<span data-ttu-id="0535c-102">連結空磁碟是一個新增資料磁碟的簡易方式，因為 Azure 會為您建立 .vhd 檔案並將它儲存在儲存體帳戶中。</span><span class="sxs-lookup"><span data-stu-id="0535c-102">Attaching an empty disk is a simple way to add a data disk, because Azure creates the .vhd file for you and stores it in the storage account.</span></span>

1. <span data-ttu-id="0535c-103">按一下 [虛擬機器 (傳統)]，然後選取適當的 VM。</span><span class="sxs-lookup"><span data-stu-id="0535c-103">Click **Virtual Machines (classic)**, and then select the appropriate VM.</span></span>

2. <span data-ttu-id="0535c-104">在 [設定] 功能表中，按一下 [磁碟]。</span><span class="sxs-lookup"><span data-stu-id="0535c-104">In the Settings menu, click **Disks**.</span></span>

   ![連接新的空磁碟](./media/howto-attach-disk-windows-linux/menudisksattachnew.png)

3. <span data-ttu-id="0535c-106">按一下命令列上的 [連結新項目]。</span><span class="sxs-lookup"><span data-stu-id="0535c-106">On the command bar, click **Attach new**.</span></span>  
    <span data-ttu-id="0535c-107">[連結新磁碟] 對話方塊隨即出現。</span><span class="sxs-lookup"><span data-stu-id="0535c-107">The **Attach new disk** dialog box appears.</span></span>

    ![附加新的磁碟](./media/howto-attach-disk-windows-linux/newdiskdetail.png)

    <span data-ttu-id="0535c-109">填寫下列資訊︰</span><span class="sxs-lookup"><span data-stu-id="0535c-109">Fill in the following information:</span></span>
    - <span data-ttu-id="0535c-110">在 [檔案名稱] 中，接受預設名稱，或是為 .vhd 檔案輸入另一個名稱。</span><span class="sxs-lookup"><span data-stu-id="0535c-110">In **File Name**, accept the default name or type another one for the .vhd file.</span></span> <span data-ttu-id="0535c-111">資料磁碟會使用自動產生的名稱，即使您為 .vhd 檔案輸入另一個名稱亦然。</span><span class="sxs-lookup"><span data-stu-id="0535c-111">The data disk uses an automatically generated name, even if you type another name for the .vhd file.</span></span>
    - <span data-ttu-id="0535c-112">選取資料磁碟的 [類型]。</span><span class="sxs-lookup"><span data-stu-id="0535c-112">Select the **Type** of the data disk.</span></span> <span data-ttu-id="0535c-113">所有虛擬機器皆支援標準磁碟。</span><span class="sxs-lookup"><span data-stu-id="0535c-113">All virtual machines support standard disks.</span></span> <span data-ttu-id="0535c-114">許多虛擬機器也支援進階磁碟。</span><span class="sxs-lookup"><span data-stu-id="0535c-114">Many virtual machines also support premium disks.</span></span>
    - <span data-ttu-id="0535c-115">選取資料磁碟的 [大小 (GB)]。</span><span class="sxs-lookup"><span data-stu-id="0535c-115">Select the **Size (GB)** of the data disk.</span></span>
    - <span data-ttu-id="0535c-116">在 [主機快取] 中選擇 [無] 或 [唯讀]。</span><span class="sxs-lookup"><span data-stu-id="0535c-116">For **Host caching**, choose none or Read Only.</span></span>
    - <span data-ttu-id="0535c-117">按一下 [確定] 以完成。</span><span class="sxs-lookup"><span data-stu-id="0535c-117">Click OK to finish.</span></span>

4. <span data-ttu-id="0535c-118">建立並連結資料磁碟之後，它就會列在 VM 的 [磁碟] 區段中。</span><span class="sxs-lookup"><span data-stu-id="0535c-118">After the data disk is created and attached, it's listed in the disks section of the VM.</span></span>

   ![成功連結新的空白資料磁碟](./media/howto-attach-disk-windows-linux/newdiskemptysuccessful.png)

> [!NOTE]
> <span data-ttu-id="0535c-120">新增資料磁碟之後，您將必須登入 VM 並將磁碟初始化，才能使用該磁碟。</span><span class="sxs-lookup"><span data-stu-id="0535c-120">After you add a data disk, you need to log on to the VM and initialize the disk so that it can be used.</span></span>

## <a name="how-to-attach-an-existing-disk"></a><span data-ttu-id="0535c-121">做法：連接現有磁碟</span><span class="sxs-lookup"><span data-stu-id="0535c-121">How to: Attach an existing disk</span></span>
<span data-ttu-id="0535c-122">連接現有磁碟要求您在儲存體帳戶中需要有可用的 .vhd。</span><span class="sxs-lookup"><span data-stu-id="0535c-122">Attaching an existing disk requires that you have a .vhd available in a storage account.</span></span> <span data-ttu-id="0535c-123">請使用 [Add-AzureVhd](https://msdn.microsoft.com/library/azure/dn495173.aspx) Cmdlet，將 .vhd 檔案上傳至儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="0535c-123">Use the [Add-AzureVhd](https://msdn.microsoft.com/library/azure/dn495173.aspx) cmdlet to upload the .vhd file to the storage account.</span></span> <span data-ttu-id="0535c-124">在建立並上傳 .vhd 檔案之後，您就可將它連結至 VM。</span><span class="sxs-lookup"><span data-stu-id="0535c-124">After you've created and uploaded the .vhd file, you can attach it to a VM.</span></span>

1. <span data-ttu-id="0535c-125">按一下 [虛擬機器 (傳統)]，然後選取適當的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="0535c-125">Click **Virtual Machines (classic)**, and then select the appropriate virtual machine.</span></span>

2. <span data-ttu-id="0535c-126">在 [設定] 功能表中，按一下 [磁碟]。</span><span class="sxs-lookup"><span data-stu-id="0535c-126">In the Settings menu, click **Disks**.</span></span>

3. <span data-ttu-id="0535c-127">按一下命令列上的 [連結現有項目]。</span><span class="sxs-lookup"><span data-stu-id="0535c-127">On the command bar, click **Attach existing**.</span></span>

    ![連接資料磁碟](./media/howto-attach-disk-windows-linux/menudisksattachexisting.png)

4. <span data-ttu-id="0535c-129">按一下 [位置]。</span><span class="sxs-lookup"><span data-stu-id="0535c-129">Click **Location**.</span></span> <span data-ttu-id="0535c-130">隨即會顯示可用的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="0535c-130">The available storage accounts display.</span></span> <span data-ttu-id="0535c-131">接下來，從所列帳戶中選取適當的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="0535c-131">Next, select an appropriate storage account from those listed.</span></span>

    ![提供磁碟儲存體帳戶](./media/howto-attach-disk-windows-linux/existdiskstorageaccounts.png)

5. <span data-ttu-id="0535c-133">**儲存體帳戶**會保有一或多個包含磁碟機 (VHD) 的容器。</span><span class="sxs-lookup"><span data-stu-id="0535c-133">A **Storage account** holds one or more containers that contain disk drives (vhds).</span></span> <span data-ttu-id="0535c-134">從所列容器中選取適當的容器。</span><span class="sxs-lookup"><span data-stu-id="0535c-134">Select the appropriate container from those listed.</span></span>

    ![提供 virtual-machines-windows 的容器](./media/howto-attach-disk-windows-linux/existdiskcontainers.png)

6. <span data-ttu-id="0535c-136">[VHD] 面板會列出容器中保有的磁碟機。</span><span class="sxs-lookup"><span data-stu-id="0535c-136">The **vhds** panel lists the disk drives held in the container.</span></span> <span data-ttu-id="0535c-137">對其中一個磁碟按一下，然後按一下 [選取]。</span><span class="sxs-lookup"><span data-stu-id="0535c-137">Click one of the disks, and then click Select.</span></span>

    ![提供 virtual-machines-windows 的磁碟映像](./media/howto-attach-disk-windows-linux/existdiskvhds.png)

7. <span data-ttu-id="0535c-139">[連結現有磁碟] 面板會再次顯示，其中所列出的位置會包含要新增至虛擬機器的儲存體帳戶、容器和選取的硬碟 (VHD)。</span><span class="sxs-lookup"><span data-stu-id="0535c-139">The **Attach existing disk** panel displays again, with the location containing the storage account, container, and selected hard disk (vhd) to add to the virtual machine.</span></span>

  <span data-ttu-id="0535c-140">將 [主機快取] 設定為 [無] 或 [唯讀]，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="0535c-140">Set **Host caching** to none or Read only, then click OK.</span></span>

    ![成功連接資料磁碟](./media/howto-attach-disk-windows-linux/exisitingdisksuccessful.png)
