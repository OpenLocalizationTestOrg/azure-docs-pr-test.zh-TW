#### <a name="to-install-mpio-on-the-host"></a><span data-ttu-id="a1d97-101">若要在主機上安裝 MPIO</span><span class="sxs-lookup"><span data-stu-id="a1d97-101">To install MPIO on the host</span></span>
1. <span data-ttu-id="a1d97-102">在 Windows Server 主機上開啟 [伺服器管理員]。</span><span class="sxs-lookup"><span data-stu-id="a1d97-102">Open Server Manager on your Windows Server host.</span></span> <span data-ttu-id="a1d97-103">根據預設，伺服器管理員會在 Administrators 群組成員登入執行 Windows Server 2012 R2 或 Windows Server 2012 的電腦時啟動。</span><span class="sxs-lookup"><span data-stu-id="a1d97-103">By default, Server Manager starts when a member of the Administrators group logs on to a computer that is running Windows Server 2012 R2 or Windows Server 2012.</span></span> <span data-ttu-id="a1d97-104">如果尚未開啟 [伺服器管理員]，請按一下 [開始] > [伺服器管理員]。</span><span class="sxs-lookup"><span data-stu-id="a1d97-104">If the Server Manager is not already open, click **Start > Server Manager**.</span></span>
   
    ![伺服器管理員](./media/storsimple-install-mpio-windows-server/IC740997.png)
2. <span data-ttu-id="a1d97-106">按一下 [伺服器管理員] > [儀表板] > [新增角色及功能]。</span><span class="sxs-lookup"><span data-stu-id="a1d97-106">Click **Server Manager > Dashboard > Add roles and features**.</span></span> <span data-ttu-id="a1d97-107">這樣會啟動 [新增角色及功能]  精靈。</span><span class="sxs-lookup"><span data-stu-id="a1d97-107">This starts the **Add Roles and Features** wizard.</span></span>
   
    ![新增角色及功能精靈 1](./media/storsimple-install-mpio-windows-server/IC740998.png)
3. <span data-ttu-id="a1d97-109">在 [新增角色及功能]  精靈中，執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="a1d97-109">In the **Add Roles and Features** wizard, do the following:</span></span>
   
   * <span data-ttu-id="a1d97-110">在 [開始之前] 頁面中按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="a1d97-110">On the **Before you begin** page, click **Next**.</span></span>
   * <span data-ttu-id="a1d97-111">在 [選取安裝類型] 頁面上，接受 [角色型或功能型安裝] 的預設值。</span><span class="sxs-lookup"><span data-stu-id="a1d97-111">On the **Select installation type** page, accept the default setting of **Role-based or feature-based** installation.</span></span> <span data-ttu-id="a1d97-112">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="a1d97-112">Click **Next**.</span></span>
     
       ![新增角色及功能精靈 2](./media/storsimple-install-mpio-windows-server/IC740999.png)
   * <span data-ttu-id="a1d97-114">在 [選取目的地伺服器] 頁面上，選擇 [從伺服器集區選取伺服器]。</span><span class="sxs-lookup"><span data-stu-id="a1d97-114">On the **Select destination server** page, choose **Select a server from the server pool**.</span></span> <span data-ttu-id="a1d97-115">應該會自動探索主機伺服器。</span><span class="sxs-lookup"><span data-stu-id="a1d97-115">Your host server should be discovered automatically.</span></span> <span data-ttu-id="a1d97-116">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="a1d97-116">Click **Next**.</span></span>
   * <span data-ttu-id="a1d97-117">在 [選取伺服器角色] 頁面上，按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="a1d97-117">On the **Select server roles** page, click **Next**.</span></span>
   * <span data-ttu-id="a1d97-118">在 [選取功能] 頁面上，選取 [多重路徑 I/O]，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="a1d97-118">On the **Select features** page, select **Multipath I/O**, and click **Next**.</span></span>
     
       ![新增角色及功能精靈 5](./media/storsimple-install-mpio-windows-server/IC741000.png)
   * <span data-ttu-id="a1d97-120">在 [確認安裝選項] 頁面上，確認選取項目，然後選取 [需要時自動重新啟動目的地伺服器]，如下所示。</span><span class="sxs-lookup"><span data-stu-id="a1d97-120">On the **Confirm installation selections** page, confirm the selection and then select **Restart the destination server automatically if required**, as shown below.</span></span> <span data-ttu-id="a1d97-121">按一下 [Install] 。</span><span class="sxs-lookup"><span data-stu-id="a1d97-121">Click **Install**.</span></span>
     
       ![新增角色及功能精靈 8](./media/storsimple-install-mpio-windows-server/IC741001.png)
   * <span data-ttu-id="a1d97-123">完成安裝時，您將會收到通知。</span><span class="sxs-lookup"><span data-stu-id="a1d97-123">You will be notified when the installation is complete.</span></span> <span data-ttu-id="a1d97-124">按一下 [關閉]  即可關閉精靈。</span><span class="sxs-lookup"><span data-stu-id="a1d97-124">Click **Close** to close the wizard.</span></span>
     
       ![新增角色及功能精靈 9](./media/storsimple-install-mpio-windows-server/IC741002.png)

