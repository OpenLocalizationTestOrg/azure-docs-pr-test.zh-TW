
1. <span data-ttu-id="a2243-101">在 hello**混合式連線**刀鋒視窗中，按一下您剛 hello 混合式連接建立，然後按一下 **接聽程式的安裝程式**。</span><span class="sxs-lookup"><span data-stu-id="a2243-101">In hello **Hybrid connections** blade, click hello hybrid connection you just created, then click **Listener Setup**.</span></span>
   
    ![Click Listener Setup](./media/app-service-hybrid-connections-manager-install/D04ClickListenerSetup.png)
2. <span data-ttu-id="a2243-103">hello**混合式連接屬性**刀鋒視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="a2243-103">hello **Hybrid connection properties** blade opens.</span></span> <span data-ttu-id="a2243-104">在下**在內部部署混合式連線管理員**，選擇**手動下載及設定**，儲存下載的 hello HybridConnectionManager.msi 封裝，並將複製 hello 閘道連接字串。</span><span class="sxs-lookup"><span data-stu-id="a2243-104">Under **On-premises Hybrid Connection Manager**, choose **download and configure manually**, save hello downloaded HybridConnectionManager.msi package, and copy hello gateway connection string.</span></span>
   
    ![按一下這裡 tooinstall](./media/app-service-hybrid-connections-manager-install/D05ClickToInstallHCM.png)
3. <span data-ttu-id="a2243-106">系統管理員命令提示字元中，輸入下列命令 toostart hello installer hello:</span><span class="sxs-lookup"><span data-stu-id="a2243-106">From an administrator command prompt, type hello following command toostart hello installer:</span></span>
   
        start HybridConnectionManager.msi
4. <span data-ttu-id="a2243-107">Hello 之後執行安裝程式中，按一下**現在不要**，然後瀏覽 toohello %ProgramFiles%\Microsoft\HybridConnectionManager 資料夾中，執行 HCMConfigWizard.exe 並按一下**是**在 hello**使用者帳戶控制**對話方塊。</span><span class="sxs-lookup"><span data-stu-id="a2243-107">After hello installer runs, click **Not now**, then browse toohello %ProgramFiles%\Microsoft\HybridConnectionManager folder, run HCMConfigWizard.exe and click **Yes** in hello **User Account Control** dialog.</span></span>
5. <span data-ttu-id="a2243-108">貼上您之前複製的 hello 混合式連接字串，然後按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="a2243-108">Paste hello hybrid connection string that you copied earlier and click **OK**.</span></span> 
   
    ![安裝](./media/app-service-hybrid-connections-manager-install/D08aHCMInstallManual.png)
6. <span data-ttu-id="a2243-110">Hello 安裝完成時，按一下**關閉**。</span><span class="sxs-lookup"><span data-stu-id="a2243-110">When hello install completes, click **Close**.</span></span>
   
    ![Click Close](./media/app-service-hybrid-connections-manager-install/D09HCMInstallComplete.png)
   
    <span data-ttu-id="a2243-112">在 hello**混合式連線**刀鋒視窗，hello**狀態**資料行現在會顯示**已連接**。</span><span class="sxs-lookup"><span data-stu-id="a2243-112">On hello **Hybrid connections** blade, hello **Status** column now shows **Connected**.</span></span> 
   
    ![Connected Status](./media/app-service-hybrid-connections-manager-install/D10HCStatusConnected.png)

