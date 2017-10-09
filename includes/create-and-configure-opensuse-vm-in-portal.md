1. <span data-ttu-id="19a21-101">登入 toohello [Azure 傳統入口網站](http://manage.windowsazure.com)。</span><span class="sxs-lookup"><span data-stu-id="19a21-101">Sign in toohello [Azure classic portal](http://manage.windowsazure.com).</span></span>  
2. <span data-ttu-id="19a21-102">在 hello 在 hello hello 視窗底部的命令列中按一下**新增**。</span><span class="sxs-lookup"><span data-stu-id="19a21-102">On hello command bar at hello bottom of hello window, click **New**.</span></span>
3. <span data-ttu-id="19a21-103">在 [計算] 下，依序按一下 [虛擬機器] 及 [從映像庫]。</span><span class="sxs-lookup"><span data-stu-id="19a21-103">Under **Compute**, click **Virtual Machine**, and then click **From Gallery**.</span></span>
   
    ![建立新的虛擬機器][Image1]
4. <span data-ttu-id="19a21-105">在 hello **SUSE**群組，選取 OpenSUSE 虛擬機器映像，然後按一下hello 箭號 toocontinue。</span><span class="sxs-lookup"><span data-stu-id="19a21-105">Under hello **SUSE** group, select an OpenSUSE virtual machine image, and then click hello arrow toocontinue.</span></span>
5. <span data-ttu-id="19a21-106">在 hello 上第一個**虛擬機器組態**頁面：</span><span class="sxs-lookup"><span data-stu-id="19a21-106">On hello first **Virtual machine configuration** page:</span></span>
   
   * <span data-ttu-id="19a21-107">輸入 **虛擬機器名稱** (如 "testlinuxvm")。</span><span class="sxs-lookup"><span data-stu-id="19a21-107">Type a **Virtual Machine Name**, such as "testlinuxvm".</span></span> <span data-ttu-id="19a21-108">hello 名稱必須介於 3 到 15 個字元，可以包含字母、 數字和連字號，並且必須以字母開頭和結尾以字母或數字。</span><span class="sxs-lookup"><span data-stu-id="19a21-108">hello name must contain between 3 and 15 characters, can contain only letters, numbers, and hyphens, and must start with a letter and end with either a letter or number.</span></span>
   * <span data-ttu-id="19a21-109">確認 hello**層**並挑選**大小**。</span><span class="sxs-lookup"><span data-stu-id="19a21-109">Verify hello **Tier** and pick a **Size**.</span></span> <span data-ttu-id="19a21-110">hello 層會決定您可以選擇從 hello 大小。</span><span class="sxs-lookup"><span data-stu-id="19a21-110">hello tier determines hello sizes you can choose from.</span></span> <span data-ttu-id="19a21-111">hello 大小會影響 hello 成本使用它，以及組態選項，例如多少資料磁碟，您可以將附加。</span><span class="sxs-lookup"><span data-stu-id="19a21-111">hello size affects hello cost of using it, as well as configuration options such as how many data disks you can attach.</span></span> <span data-ttu-id="19a21-112">如需詳細資訊，請參閱 [虛擬機器的大小](../articles/virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="19a21-112">For details, see [Sizes for virtual machines](../articles/virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
   * <span data-ttu-id="19a21-113">輸入**新的使用者名稱**，或接受 hello 預設**azureuser**。</span><span class="sxs-lookup"><span data-stu-id="19a21-113">Type a **New User Name**, or accept hello default, **azureuser**.</span></span> <span data-ttu-id="19a21-114">這個名稱會加入 toohello Sudoers 清單檔案。</span><span class="sxs-lookup"><span data-stu-id="19a21-114">This name is added toohello Sudoers list file.</span></span>
   * <span data-ttu-id="19a21-115">決定哪一種類型**驗證**toouse。</span><span class="sxs-lookup"><span data-stu-id="19a21-115">Decide which type of **Authentication** toouse.</span></span> <span data-ttu-id="19a21-116">如需一般密碼指導方針，請參閱 [字串密碼](http://msdn.microsoft.com/library/ms161962.aspx)。</span><span class="sxs-lookup"><span data-stu-id="19a21-116">For general password guidelines, see [Strong passwords](http://msdn.microsoft.com/library/ms161962.aspx).</span></span>
6. <span data-ttu-id="19a21-117">在 hello 下一步**虛擬機器組態**頁面：</span><span class="sxs-lookup"><span data-stu-id="19a21-117">On hello next **Virtual machine configuration** page:</span></span>
   
   * <span data-ttu-id="19a21-118">使用預設的 hello**建立新的雲端服務**。</span><span class="sxs-lookup"><span data-stu-id="19a21-118">Use hello default **Create a new cloud service**.</span></span>
   * <span data-ttu-id="19a21-119">在 hello **DNS 名稱**方塊中，輸入唯一的 DNS 名稱 toouse hello 位址，例如"testlinuxvm 」 的一部分。</span><span class="sxs-lookup"><span data-stu-id="19a21-119">In hello **DNS Name** box, type a unique DNS name toouse as part of hello address, such as "testlinuxvm".</span></span>
   * <span data-ttu-id="19a21-120">在 hello**區域/同質群組/虛擬網路**方塊中，選取將託管這個虛擬映像的區域。</span><span class="sxs-lookup"><span data-stu-id="19a21-120">In hello **Region/Affinity Group/Virtual Network** box, select a region where this virtual image will be hosted.</span></span>
   * <span data-ttu-id="19a21-121">在下**端點**，保留 hello SSH 的端點。</span><span class="sxs-lookup"><span data-stu-id="19a21-121">Under **Endpoints**, keep hello SSH endpoint.</span></span> <span data-ttu-id="19a21-122">您可以現在，加入其他人或新增、 變更或 hello 虛擬機器建立後加以刪除。</span><span class="sxs-lookup"><span data-stu-id="19a21-122">You can add others now, or add, change, or delete them after hello virtual machine is created.</span></span>
     
     > [!NOTE]
     > <span data-ttu-id="19a21-123">如果您想要虛擬機器 toouse 虛擬網路，您**必須**指定 hello 虛擬網路，當您建立 hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="19a21-123">If you want a virtual machine toouse a virtual network, you **must** specify hello virtual network when you create hello virtual machine.</span></span> <span data-ttu-id="19a21-124">建立 hello 虛擬機器之後，您無法將虛擬機器 tooa 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="19a21-124">You can't add a virtual machine tooa virtual network after you create hello virtual machine.</span></span> <span data-ttu-id="19a21-125">如需詳細資訊，請參閱[虛擬網路概觀](../articles/virtual-network/virtual-networks-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="19a21-125">For more information, see [Virtual Network Overview](../articles/virtual-network/virtual-networks-overview.md).</span></span>
     > 
     > 
7. <span data-ttu-id="19a21-126">在 hello 上最後一個**虛擬機器組態**頁面上，保留 hello 預設設定，然後按一下hello 核取記號 toofinish。</span><span class="sxs-lookup"><span data-stu-id="19a21-126">On hello last **Virtual machine configuration** page, keep hello default settings and then click hello check mark toofinish.</span></span>

<span data-ttu-id="19a21-127">hello 網站列出下 hello 新虛擬機器**虛擬機器**。</span><span class="sxs-lookup"><span data-stu-id="19a21-127">hello portal lists hello new virtual machine under **Virtual Machines**.</span></span> <span data-ttu-id="19a21-128">雖然 hello 狀態報告為**（佈建）**，設定 hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="19a21-128">While hello status is reported as **(Provisioning)**, hello virtual machine is being set up.</span></span> <span data-ttu-id="19a21-129">當 hello 狀態報告為**執行**，您可以移 toohello 下一個步驟。</span><span class="sxs-lookup"><span data-stu-id="19a21-129">When hello status is reported as **Running**, you can move on toohello next step.</span></span>

## <a name="connect-toohello-virtual-machine"></a><span data-ttu-id="19a21-130">連接 toohello 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="19a21-130">Connect toohello Virtual Machine</span></span>
<span data-ttu-id="19a21-131">您將使用 SSH 或 PuTTY tooconnect toohello 虛擬機器，視您要從連接的 hello 電腦上的 hello 作業系統而定：</span><span class="sxs-lookup"><span data-stu-id="19a21-131">You'll use SSH or PuTTY tooconnect toohello virtual machine, depending on hello operating system on hello computer you'll connect from:</span></span>

* <span data-ttu-id="19a21-132">請從執行 Linux 的電腦使用 SSH。</span><span class="sxs-lookup"><span data-stu-id="19a21-132">From a computer running Linux, use SSH.</span></span> <span data-ttu-id="19a21-133">在 hello 命令提示字元中輸入：</span><span class="sxs-lookup"><span data-stu-id="19a21-133">At hello command prompt, type:</span></span>
  
    `$ ssh newuser@testlinuxvm.cloudapp.net -o ServerAliveInterval=180`
  
    <span data-ttu-id="19a21-134">輸入 hello 使用者的密碼。</span><span class="sxs-lookup"><span data-stu-id="19a21-134">Type hello user's password.</span></span>
* <span data-ttu-id="19a21-135">請從執行 Windows 的電腦使用 PuTTY。</span><span class="sxs-lookup"><span data-stu-id="19a21-135">From a computer running Windows, use PuTTY.</span></span> <span data-ttu-id="19a21-136">如果您沒有安裝它，從 hello 下載[PuTTY 下載頁面][PuTTYDownload]。</span><span class="sxs-lookup"><span data-stu-id="19a21-136">If you don't have it installed, download it from hello [PuTTY Download Page][PuTTYDownload].</span></span>
  
    <span data-ttu-id="19a21-137">儲存**putty.exe** tooa 目錄，在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="19a21-137">Save **putty.exe** tooa directory on your computer.</span></span> <span data-ttu-id="19a21-138">開啟命令提示字元，瀏覽 toothat 資料夾，並執行**putty.exe**。</span><span class="sxs-lookup"><span data-stu-id="19a21-138">Open a command prompt, navigate toothat folder, and run **putty.exe**.</span></span>
  
    <span data-ttu-id="19a21-139">輸入 hello 主機名稱，例如"testlinuxvm.cloudapp.net 」，然後輸入"22"hello**連接埠**。</span><span class="sxs-lookup"><span data-stu-id="19a21-139">Type hello host name, such as "testlinuxvm.cloudapp.net", and type "22" for hello **Port**.</span></span>
  
    ![PuTTY 畫面][Image6]  

## <a name="update-hello-virtual-machine-optional"></a><span data-ttu-id="19a21-141">更新 hello 虛擬機器 （選擇性）</span><span class="sxs-lookup"><span data-stu-id="19a21-141">Update hello Virtual Machine (optional)</span></span>
1. <span data-ttu-id="19a21-142">在連接的 toohello 虛擬機器之後，您可以選擇性地安裝系統更新和修補程式。</span><span class="sxs-lookup"><span data-stu-id="19a21-142">After you're connected toohello virtual machine, you can optionally install system updates and patches.</span></span> <span data-ttu-id="19a21-143">型別 toorun hello 更新：</span><span class="sxs-lookup"><span data-stu-id="19a21-143">toorun hello update, type:</span></span>
   
    `$ sudo zypper update`
2. <span data-ttu-id="19a21-144">選取**軟體**，然後**線上更新**toolist 可用的更新。</span><span class="sxs-lookup"><span data-stu-id="19a21-144">Select **Software**, then **Online Update** toolist available updates.</span></span> <span data-ttu-id="19a21-145">選取**接受**toostart hello 安裝，並套用所有新可用的修補程式 （除了 hello 選擇性的)。</span><span class="sxs-lookup"><span data-stu-id="19a21-145">Select **Accept** toostart hello installation and apply all new available patches (except hello optional ones).</span></span>
3. <span data-ttu-id="19a21-146">安裝完成之後，選取 [ **完成**]。</span><span class="sxs-lookup"><span data-stu-id="19a21-146">After installation is done, select **Finish**.</span></span>  <span data-ttu-id="19a21-147">系統現在是 toodate 組成。</span><span class="sxs-lookup"><span data-stu-id="19a21-147">Your system is now up toodate.</span></span>

[PuTTYDownload]: http://www.puttyssh.org/download.html

[Image1]: ./media/create-and-configure-opensuse-vm-in-portal/CreateVM.png

[Image6]: ./media/create-and-configure-opensuse-vm-in-portal/putty.png
