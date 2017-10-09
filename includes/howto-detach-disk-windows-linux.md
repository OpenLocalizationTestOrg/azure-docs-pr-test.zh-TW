<span data-ttu-id="a329a-101">當您不再需要的資料磁碟附加的 tooa 虛擬機器時，您可以輕易地中斷。</span><span class="sxs-lookup"><span data-stu-id="a329a-101">When you no longer need a data disk that's attached tooa virtual machine, you can easily detach it.</span></span> <span data-ttu-id="a329a-102">卸離磁碟 hello 磁碟移除 hello 虛擬機器，但不會從 hello Azure 儲存體帳戶刪除 hello 磁碟。</span><span class="sxs-lookup"><span data-stu-id="a329a-102">Detaching a disk removes hello disk from hello virtual machine, but doesn't delete hello disk from hello Azure storage account.</span></span>

<span data-ttu-id="a329a-103">若要再次 toouse hello 現有資料 hello 磁碟上的，您可以將它重新附加 toohello 相同的虛擬機器或另一個。</span><span class="sxs-lookup"><span data-stu-id="a329a-103">If you want toouse hello existing data on hello disk again, you can reattach it toohello same virtual machine, or another one.</span></span>  

> [!NOTE]
> <span data-ttu-id="a329a-104">toodetach 作業系統磁碟，您必須先 toodelete hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="a329a-104">toodetach an operating system disk, you first need toodelete hello virtual machine.</span></span>
>

## <a name="find-hello-disk"></a><span data-ttu-id="a329a-105">找不到 hello 磁碟</span><span class="sxs-lookup"><span data-stu-id="a329a-105">Find hello disk</span></span>
<span data-ttu-id="a329a-106">如果您不知道 hello 名稱 hello 磁碟，或想 tooverify 它然後再卸離資料庫，請遵循下列步驟。</span><span class="sxs-lookup"><span data-stu-id="a329a-106">If you don't know hello name of hello disk or want tooverify it before you detach it, follow these steps.</span></span>

1. <span data-ttu-id="a329a-107">登入 toohello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="a329a-107">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="a329a-108">按一下**虛擬機器**，，然後選取 hello 適當的 VM。</span><span class="sxs-lookup"><span data-stu-id="a329a-108">Click **Virtual Machines**, and then select hello appropriate VM.</span></span>

3. <span data-ttu-id="a329a-109">按一下**磁碟**沿著 hello 左邊緣的 hello 虛擬機器儀表板下方**設定**。</span><span class="sxs-lookup"><span data-stu-id="a329a-109">Click **Disks** along hello left edge of hello virtual machine dashboard, under **Settings**.</span></span>

 <span data-ttu-id="a329a-110">hello 虛擬機器儀表板列出 hello 名稱和類型的所有連接的磁碟。</span><span class="sxs-lookup"><span data-stu-id="a329a-110">hello virtual machine dashboard lists hello name and type of all attached disks.</span></span> <span data-ttu-id="a329a-111">例如，此畫面會顯示虛擬機器及一個作業系統 (OS) 磁碟和一個資料磁碟：</span><span class="sxs-lookup"><span data-stu-id="a329a-111">For example, this screen shows a virtual machine with one operating system (OS) disk and one data disk:</span></span>

    ![尋找資料磁碟](./media/howto-detach-disk-windows-linux/vmwithdisklist.png)

## <a name="detach-hello-disk"></a><span data-ttu-id="a329a-113">卸離 hello 磁碟</span><span class="sxs-lookup"><span data-stu-id="a329a-113">Detach hello disk</span></span>
1. <span data-ttu-id="a329a-114">從 hello Azure 入口網站，按一下 **虛擬機器**，然後按一下hello hello 具有您想 toodetach hello 資料磁碟的虛擬機器的名稱。</span><span class="sxs-lookup"><span data-stu-id="a329a-114">From hello Azure portal, click **Virtual Machines**, and then click hello name of hello virtual machine that has hello data disk you want toodetach.</span></span>

2. <span data-ttu-id="a329a-115">按一下**磁碟**沿著 hello 左邊緣的 hello 虛擬機器儀表板下方**設定**。</span><span class="sxs-lookup"><span data-stu-id="a329a-115">Click **Disks** along hello left edge of hello virtual machine dashboard, under **Settings**.</span></span>

3. <span data-ttu-id="a329a-116">按一下您想 toodetach 的 hello 磁碟。</span><span class="sxs-lookup"><span data-stu-id="a329a-116">Click hello disk you want toodetach.</span></span>

  ![識別 hello 磁碟 toodetach](./media/howto-detach-disk-windows-linux/disklist.png)

4. <span data-ttu-id="a329a-118">在 hello 命令列中，按一下**卸離**。</span><span class="sxs-lookup"><span data-stu-id="a329a-118">From hello command bar, click **Detach**.</span></span>

  ![找出 hello 卸離命令](./media/howto-detach-disk-windows-linux/diskdetachcommand.png)

5. <span data-ttu-id="a329a-120">在 hello 確認視窗中，按一下 **是**toodetach hello 磁碟。</span><span class="sxs-lookup"><span data-stu-id="a329a-120">In hello confirmation window, click **Yes** toodetach hello disk.</span></span>

  ![確認中斷連接的 hello 磁碟](./media/howto-detach-disk-windows-linux/confirmdetach.png)

<span data-ttu-id="a329a-122">hello 磁碟留在儲存體，但已不再附加的 tooa 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="a329a-122">hello disk remains in storage but is no longer attached tooa virtual machine.</span></span>
