#### <a name="tooinstall-mpio-on-hello-host"></a><span data-ttu-id="845bc-101">tooinstall MPIO hello 主機上</span><span class="sxs-lookup"><span data-stu-id="845bc-101">tooinstall MPIO on hello host</span></span>
1. <span data-ttu-id="845bc-102">在 Windows Server 主機上開啟 [伺服器管理員]。</span><span class="sxs-lookup"><span data-stu-id="845bc-102">Open Server Manager on your Windows Server host.</span></span> <span data-ttu-id="845bc-103">根據預設，伺服器管理員啟動的 hello Administrators 群組成員登入時 tooa 電腦執行 Windows Server 2012 R2 或 Windows Server 2012。</span><span class="sxs-lookup"><span data-stu-id="845bc-103">By default, Server Manager starts when a member of hello Administrators group logs on tooa computer that is running Windows Server 2012 R2 or Windows Server 2012.</span></span> <span data-ttu-id="845bc-104">如果 hello 伺服器管理員 尚未開啟，請按一下**開始 > 伺服器管理員**。</span><span class="sxs-lookup"><span data-stu-id="845bc-104">If hello Server Manager is not already open, click **Start > Server Manager**.</span></span>
   
    ![伺服器管理員](./media/storsimple-install-mpio-windows-server/IC740997.png)
2. <span data-ttu-id="845bc-106">按一下 [伺服器管理員] > [儀表板] > [新增角色及功能]。</span><span class="sxs-lookup"><span data-stu-id="845bc-106">Click **Server Manager > Dashboard > Add roles and features**.</span></span> <span data-ttu-id="845bc-107">這會啟動 hello**新增角色及功能**精靈。</span><span class="sxs-lookup"><span data-stu-id="845bc-107">This starts hello **Add Roles and Features** wizard.</span></span>
   
    ![新增角色及功能精靈 1](./media/storsimple-install-mpio-windows-server/IC740998.png)
3. <span data-ttu-id="845bc-109">在 hello**新增角色及功能**精靈 中，執行下列 hello:</span><span class="sxs-lookup"><span data-stu-id="845bc-109">In hello **Add Roles and Features** wizard, do hello following:</span></span>
   
   * <span data-ttu-id="845bc-110">在 hello**開始之前**頁面上，按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="845bc-110">On hello **Before you begin** page, click **Next**.</span></span>
   * <span data-ttu-id="845bc-111">在 hello**選取安裝類型**頁面上，接受預設設定 hello**角色型或功能型**安裝。</span><span class="sxs-lookup"><span data-stu-id="845bc-111">On hello **Select installation type** page, accept hello default setting of **Role-based or feature-based** installation.</span></span> <span data-ttu-id="845bc-112">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="845bc-112">Click **Next**.</span></span>
     
       ![新增角色及功能精靈 2](./media/storsimple-install-mpio-windows-server/IC740999.png)
   * <span data-ttu-id="845bc-114">在 hello**選取目的地伺服器**頁面上，選擇**從 hello 伺服器集區選取伺服器**。</span><span class="sxs-lookup"><span data-stu-id="845bc-114">On hello **Select destination server** page, choose **Select a server from hello server pool**.</span></span> <span data-ttu-id="845bc-115">應該會自動探索主機伺服器。</span><span class="sxs-lookup"><span data-stu-id="845bc-115">Your host server should be discovered automatically.</span></span> <span data-ttu-id="845bc-116">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="845bc-116">Click **Next**.</span></span>
   * <span data-ttu-id="845bc-117">在 hello**選取伺服器角色**頁面上，按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="845bc-117">On hello **Select server roles** page, click **Next**.</span></span>
   * <span data-ttu-id="845bc-118">在 hello**選取功能**頁面上，選取**多重路徑 I/O**，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="845bc-118">On hello **Select features** page, select **Multipath I/O**, and click **Next**.</span></span>
     
       ![新增角色及功能精靈 5](./media/storsimple-install-mpio-windows-server/IC741000.png)
   * <span data-ttu-id="845bc-120">在 hello**確認安裝選項**頁面上，確認 hello 選取項目，然後選取**必要時自動重新啟動 hello 目的地伺服器**，如下所示。</span><span class="sxs-lookup"><span data-stu-id="845bc-120">On hello **Confirm installation selections** page, confirm hello selection and then select **Restart hello destination server automatically if required**, as shown below.</span></span> <span data-ttu-id="845bc-121">按一下 [Install] 。</span><span class="sxs-lookup"><span data-stu-id="845bc-121">Click **Install**.</span></span>
     
       ![新增角色及功能精靈 8](./media/storsimple-install-mpio-windows-server/IC741001.png)
   * <span data-ttu-id="845bc-123">Hello 安裝已完成時，將會通知您。</span><span class="sxs-lookup"><span data-stu-id="845bc-123">You will be notified when hello installation is complete.</span></span> <span data-ttu-id="845bc-124">按一下**關閉**tooclose hello 精靈。</span><span class="sxs-lookup"><span data-stu-id="845bc-124">Click **Close** tooclose hello wizard.</span></span>
     
       ![新增角色及功能精靈 9](./media/storsimple-install-mpio-windows-server/IC741002.png)

