<!--author=alkohli last changed: 08/21/17-->

#### <a name="toodownload-hotfixes"></a><span data-ttu-id="de668-101">toodownload hotfix</span><span class="sxs-lookup"><span data-stu-id="de668-101">toodownload hotfixes</span></span>

<span data-ttu-id="de668-102">執行 hello hello Microsoft Update 類別目錄中的下列步驟 toodownload hello 軟體更新。</span><span class="sxs-lookup"><span data-stu-id="de668-102">Perform hello following steps toodownload hello software update from hello Microsoft Update Catalog.</span></span>

1. <span data-ttu-id="de668-103">啟動 Internet Explorer 並瀏覽過[http://catalog.update.microsoft.com](http://catalog.update.microsoft.com)。</span><span class="sxs-lookup"><span data-stu-id="de668-103">Start Internet Explorer and navigate too[http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span></span>
2. <span data-ttu-id="de668-104">如果這是您第一次使用 hello Microsoft Update 類別目錄，在此電腦上，按一下**安裝**時提示的 tooinstall hello Microsoft Update 類別目錄的附加元件。</span><span class="sxs-lookup"><span data-stu-id="de668-104">If this is your first time using hello Microsoft Update Catalog on this computer, click **Install** when prompted tooinstall hello Microsoft Update Catalog add-on.</span></span>

    ![安裝目錄](./media/storsimple-install-update2-hotfix/HCS_InstallCatalog-include.png)

3. <span data-ttu-id="de668-106">在 hello hello Microsoft Update 類別目錄的搜尋方塊中輸入 hello 知識庫 (KB) 號碼 hello hotfix 您想讓 toodownload，例如**4037264**，然後按一下**搜尋**。</span><span class="sxs-lookup"><span data-stu-id="de668-106">In hello search box of hello Microsoft Update Catalog, enter hello Knowledge Base (KB) number of hello hotfix you want toodownload, for example **4037264**, and then click **Search**.</span></span>
   
    <span data-ttu-id="de668-107">hello hotfix 清單會出現，例如**StorSimple 8000 系列的累計軟體配套更新 5.0**。</span><span class="sxs-lookup"><span data-stu-id="de668-107">hello hotfix listing appears, for example, **Cumulative Software Bundle Update 5.0 for StorSimple 8000 Series**.</span></span>
   
    ![搜尋目錄](./media/storsimple-install-update5-hotfix/update-catalog-search.png)

4. <span data-ttu-id="de668-109">按一下 [下載] 。</span><span class="sxs-lookup"><span data-stu-id="de668-109">Click **Download**.</span></span> <span data-ttu-id="de668-110">指定或**瀏覽**所在 hello 下載 tooappear tooa 本機位置。</span><span class="sxs-lookup"><span data-stu-id="de668-110">Specify or **Browse** tooa local location where you want hello downloads tooappear.</span></span> <span data-ttu-id="de668-111">按一下 hello 檔案 toodownload toohello 指定位置和資料夾。</span><span class="sxs-lookup"><span data-stu-id="de668-111">Click hello files toodownload toohello specified location and folder.</span></span> <span data-ttu-id="de668-112">hello 資料夾也可以複製的 tooa 從 hello 裝置的網路共用。</span><span class="sxs-lookup"><span data-stu-id="de668-112">hello folder can also be copied tooa network share that is reachable from hello device.</span></span>
5. <span data-ttu-id="de668-113">Hello 上表中列出的搜尋任何其他的 hotfix (**4037266**)，及下載 hello 對應檔案 toohello 特定資料夾如 hello 前面表格中所列。</span><span class="sxs-lookup"><span data-stu-id="de668-113">Search for any additional hotfixes listed in hello table above (**4037266**), and download hello corresponding files toohello specific folders as listed in hello preceding table.</span></span>

> [!NOTE]
> <span data-ttu-id="de668-114">hello hotfix 必須能夠從這兩個控制器 toodetect，hello 同儕節點控制器的任何潛在的錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="de668-114">hello hotfixes must be accessible from both controllers toodetect any potential error messages from hello peer controller.</span></span>
>
> <span data-ttu-id="de668-115">hello hotfix 必須複製 3 的個別資料夾中。</span><span class="sxs-lookup"><span data-stu-id="de668-115">hello hotfixes must be copied in 3 separate folders.</span></span> <span data-ttu-id="de668-116">Hello 裝置軟體/Ci/MDS 代理程式更新，例如可以在複製_FirstOrderUpdate_所有 hello 資料夾中，其他非干擾性更新無法複製在 hello _SecondOrderUpdate_資料夾，並在中複製的維護模式更新_ThirdOrderUpdate_資料夾。</span><span class="sxs-lookup"><span data-stu-id="de668-116">For example, hello device software/Cis/MDS agent update can be copied in _FirstOrderUpdate_ folder, all hello other non-disruptive updates could be copied in hello _SecondOrderUpdate_ folder, and maintenance mode updates copied in _ThirdOrderUpdate_ folder.</span></span>

#### <a name="tooinstall-and-verify-regular-mode-hotfixes"></a><span data-ttu-id="de668-117">tooinstall 並確認一般模式 hotfix</span><span class="sxs-lookup"><span data-stu-id="de668-117">tooinstall and verify regular mode hotfixes</span></span>

<span data-ttu-id="de668-118">執行下列步驟 tooinstall hello，並確認一般模式 hotfix。</span><span class="sxs-lookup"><span data-stu-id="de668-118">Perform hello following steps tooinstall and verify regular-mode hotfixes.</span></span> <span data-ttu-id="de668-119">如果您已安裝使用 hello Azure 入口網站，跳過[安裝，並確認 維護模式 hotfix](#to-install-and-verify-maintenance-mode-hotfixes)。</span><span class="sxs-lookup"><span data-stu-id="de668-119">If you already installed them using hello Azure portal, skip ahead too[install and verify maintenance mode hotfixes](#to-install-and-verify-maintenance-mode-hotfixes).</span></span>

1. <span data-ttu-id="de668-120">您的 StorSimple 裝置序列主控台存取 hello Windows PowerShell 介面 tooinstall hello hotfix。</span><span class="sxs-lookup"><span data-stu-id="de668-120">tooinstall hello hotfixes, access hello Windows PowerShell interface on your StorSimple device serial console.</span></span> <span data-ttu-id="de668-121">請遵循詳細指示中的 hello[使用 PuTTy tooconnect toohello 序列主控台](../articles/storsimple/storsimple-8000-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console)。</span><span class="sxs-lookup"><span data-stu-id="de668-121">Follow hello detailed instructions in [Use PuTTy tooconnect toohello serial console](../articles/storsimple/storsimple-8000-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).</span></span> <span data-ttu-id="de668-122">在 hello 命令提示字元中，按下**Enter**。</span><span class="sxs-lookup"><span data-stu-id="de668-122">At hello command prompt, press **Enter**.</span></span>
2. <span data-ttu-id="de668-123">選取**選項 1** toolog toohello 具有完整存取權的裝置上。</span><span class="sxs-lookup"><span data-stu-id="de668-123">Select **Option 1** toolog on toohello device with full access.</span></span> <span data-ttu-id="de668-124">我們建議您安裝 hello hotfix hello 被動控制站上第一次。</span><span class="sxs-lookup"><span data-stu-id="de668-124">We recommend that you install hello hotfix on hello passive controller first.</span></span>
3. <span data-ttu-id="de668-125">tooinstall hello hotfix，在 hello 命令提示字元，輸入：</span><span class="sxs-lookup"><span data-stu-id="de668-125">tooinstall hello hotfix, at hello command prompt, type:</span></span>
   
    `Start-HcsHotfix -Path <path tooupdate file> -Credential <credentials in domain\username format>`
   
    <span data-ttu-id="de668-126">Hello 上述命令中的共用路徑中使用 IP，而不是 DNS。</span><span class="sxs-lookup"><span data-stu-id="de668-126">Use IP rather than DNS in share path in hello above command.</span></span> <span data-ttu-id="de668-127">只有當您要存取已驗證的共用時，才使用 hello 認證參數。</span><span class="sxs-lookup"><span data-stu-id="de668-127">hello credential parameter is used only if you are accessing an authenticated share.</span></span>
   
    <span data-ttu-id="de668-128">我們建議您使用 hello 認證參數 tooaccess 共用。</span><span class="sxs-lookup"><span data-stu-id="de668-128">We recommend that you use hello credential parameter tooaccess shares.</span></span> <span data-ttu-id="de668-129">即使已開啟太"everyone"通常的共用開啟 toounauthenticated 使用者。</span><span class="sxs-lookup"><span data-stu-id="de668-129">Even shares that are open too“everyone” are typically not open toounauthenticated users.</span></span>
   
4. <span data-ttu-id="de668-130">提供 hello 密碼提示。</span><span class="sxs-lookup"><span data-stu-id="de668-130">Supply hello password when prompted.</span></span> <span data-ttu-id="de668-131">安裝第一個訂單更新 hello 的範例輸出如下所示。</span><span class="sxs-lookup"><span data-stu-id="de668-131">A sample output for installing hello first order updates is shown below.</span></span> <span data-ttu-id="de668-132">第一個訂單更新 hello，您需要 toopoint toohello 特定檔案。</span><span class="sxs-lookup"><span data-stu-id="de668-132">For hello first order update, you need toopoint toohello specific file.</span></span>

    >[!NOTE] 
    > <span data-ttu-id="de668-133">您應該安裝 hello _HcsSoftwareUpdate.exe_第一次。</span><span class="sxs-lookup"><span data-stu-id="de668-133">You should install hello _HcsSoftwareUpdate.exe_ first.</span></span> <span data-ttu-id="de668-134">在此安裝完成後，接著安裝 _CisMdsAgentUpdate.exe_。</span><span class="sxs-lookup"><span data-stu-id="de668-134">After this install has completed, then install _CisMdsAgentUpdate.exe_.</span></span>
   
        ````
        Controller0>Start-HcsHotfix -Path \\10.100.100.100\share
        \FirstOrderUpdate\HcsSoftwareUpdate.exe -Credential contoso\John
   
        Confirm
   
        This operation starts hello hotfix installation and could reboot one or
        both of hello controllers. If hello device is serving I/Os, these will not
        be disrupted. Are you sure you want toocontinue?
        [Y] Yes [N] No [?] Help (default is "Y"): Y
   
        ````
5. <span data-ttu-id="de668-135">型別**Y**時提示的 tooconfirm hello hotfix 安裝。</span><span class="sxs-lookup"><span data-stu-id="de668-135">Type **Y** when prompted tooconfirm hello hotfix installation.</span></span>
6. <span data-ttu-id="de668-136">使用 hello 監視 hello 更新`Get-HcsUpdateStatus`cmdlet。</span><span class="sxs-lookup"><span data-stu-id="de668-136">Monitor hello update by using hello `Get-HcsUpdateStatus` cmdlet.</span></span> <span data-ttu-id="de668-137">hello 更新將會先完成 hello 被動控制站上。</span><span class="sxs-lookup"><span data-stu-id="de668-137">hello update will first complete on hello passive controller.</span></span> <span data-ttu-id="de668-138">一旦更新 hello 被動控制器，將會在容錯移轉和 hello 更新然後會套用在 hello 另一個控制器。</span><span class="sxs-lookup"><span data-stu-id="de668-138">Once hello passive controller is updated, there will be a failover and hello update will then get applied on hello other controller.</span></span> <span data-ttu-id="de668-139">兩個 hello 控制器更新時，hello 更新已完成。</span><span class="sxs-lookup"><span data-stu-id="de668-139">hello update is complete when both hello controllers are updated.</span></span>
   
    <span data-ttu-id="de668-140">hello 下列範例輸出顯示 hello 更新正在進行中。</span><span class="sxs-lookup"><span data-stu-id="de668-140">hello following sample output shows hello update in progress.</span></span> <span data-ttu-id="de668-141">hello`RunInprogress`是`True`hello 更新正在進行中。</span><span class="sxs-lookup"><span data-stu-id="de668-141">hello `RunInprogress` is `True` when hello update is in progress.</span></span>

    ```
    Controller0>Get-HcsUpdateStatus
    RunInprogress       : True
    LastHotfixTimestamp :
    LastUpdateTimestamp : 07/28/2017 2:04:02 AM
    Controller0Events   :
    Controller1Events   :
    ```
   
     <span data-ttu-id="de668-142">下列範例輸出的 hello 指出該 hello 更新已完成。</span><span class="sxs-lookup"><span data-stu-id="de668-142">hello following sample output indicates that hello update is finished.</span></span> <span data-ttu-id="de668-143">hello`RunInProgress`是`False`hello 更新時完成。</span><span class="sxs-lookup"><span data-stu-id="de668-143">hello `RunInProgress` is `False` when hello update is complete.</span></span>
   
    ```
    Controller0>Get-HcsUpdateStatus
    RunInprogress       : False
    LastHotfixTimestamp : 07/28/2017 9:15:55 AM
    LastUpdateTimestamp : 07/28/2017 9:06:07 AM
    Controller0Events   :
    Controller1Events   :
    ```

    > [!NOTE]
    > <span data-ttu-id="de668-144">有時候，hello cmdlet 報告`False`hello 更新時仍在進行中。</span><span class="sxs-lookup"><span data-stu-id="de668-144">Occasionally, hello cmdlet reports `False` when hello update is still in progress.</span></span> <span data-ttu-id="de668-145">hello hotfix 的 tooensure 已完成、 等候幾分鐘的時間，重新執行此命令並確認該 hello`RunInProgress`是`False`。</span><span class="sxs-lookup"><span data-stu-id="de668-145">tooensure that hello hotfix is complete, wait for a few minutes, rerun this command and verify that hello `RunInProgress` is `False`.</span></span> <span data-ttu-id="de668-146">如果是，已完成 hello hotfix。</span><span class="sxs-lookup"><span data-stu-id="de668-146">If it is, then hello hotfix has completed.</span></span>

7. <span data-ttu-id="de668-147">Hello 軟體更新已完成之後，請確認 hello 系統軟體版本。</span><span class="sxs-lookup"><span data-stu-id="de668-147">After hello software update is complete, verify hello system software versions.</span></span> <span data-ttu-id="de668-148">輸入：</span><span class="sxs-lookup"><span data-stu-id="de668-148">Type:</span></span>
   
    `Get-HcsSystem`
   
    <span data-ttu-id="de668-149">您應該會看到下列版本的 hello:</span><span class="sxs-lookup"><span data-stu-id="de668-149">You should see hello following versions:</span></span>
   
   * `FriendlySoftwareVersion: StorSimple 8000 Series Update 5.0`
   *  `HcsSoftwareVersion: 6.3.9600.17845`
   
    <span data-ttu-id="de668-150">如果 hello 版本號碼套用 hello 更新後不會變更，則表示該 hello hotfix tooapply 失敗。</span><span class="sxs-lookup"><span data-stu-id="de668-150">If hello version number does not change after applying hello update, it indicates that hello hotfix has failed tooapply.</span></span> <span data-ttu-id="de668-151">若您看到這種情況，請連絡 [Microsoft 支援](../articles/storsimple/storsimple-8000-contact-microsoft-support.md)以取得進一步的協助。</span><span class="sxs-lookup"><span data-stu-id="de668-151">Should you see this, please contact [Microsoft Support](../articles/storsimple/storsimple-8000-contact-microsoft-support.md) for further assistance.</span></span>
     
    > [!IMPORTANT]
    > <span data-ttu-id="de668-152">您必須重新啟動 hello 作用中的控制器透過 hello `Restart-HcsController` cmdlet 然後才套用 hello 下次的更新。</span><span class="sxs-lookup"><span data-stu-id="de668-152">You must restart hello active controller via hello `Restart-HcsController` cmdlet before applying hello next update.</span></span>
     
8. <span data-ttu-id="de668-153">重複步驟 3-6 tooinstall hello _CisMDSAgentupdate.exe_代理程式下載 tooyour _FirstOrderUpdate_資料夾。</span><span class="sxs-lookup"><span data-stu-id="de668-153">Repeat steps 3-6 tooinstall hello _CisMDSAgentupdate.exe_ agent downloaded tooyour _FirstOrderUpdate_ folder.</span></span>
8. <span data-ttu-id="de668-154">重複步驟 3-6 tooinstall hello 第二個訂單更新。</span><span class="sxs-lookup"><span data-stu-id="de668-154">Repeat steps 3-6 tooinstall hello second order updates.</span></span> 

    > [!NOTE] 
    > <span data-ttu-id="de668-155">第二個訂單更新，多個更新可以安裝只執行 hello`Start-HcsHotfix cmdlet`和指向 toohello 第二個訂單更新所在資料夾。</span><span class="sxs-lookup"><span data-stu-id="de668-155">For second order updates, multiple updates can be installed by just running hello `Start-HcsHotfix cmdlet` and pointing toohello folder where second order updates are located.</span></span> <span data-ttu-id="de668-156">hello 指令程式會執行所有可用的 hello 更新 hello 資料夾中。</span><span class="sxs-lookup"><span data-stu-id="de668-156">hello cmdlet will execute all hello updates available in hello folder.</span></span> <span data-ttu-id="de668-157">如果已安裝的更新，將偵測出 hello 更新邏輯，並不會套用該更新。</span><span class="sxs-lookup"><span data-stu-id="de668-157">If an update is already installed, hello update logic will detect that and not apply that update.</span></span>

    <span data-ttu-id="de668-158">已安裝所有的 hello hotfix 之後，請使用 hello `Get-HcsSystem` cmdlet。</span><span class="sxs-lookup"><span data-stu-id="de668-158">After all hello hotfixes are installed, use hello `Get-HcsSystem` cmdlet.</span></span> <span data-ttu-id="de668-159">hello 版本應為：</span><span class="sxs-lookup"><span data-stu-id="de668-159">hello versions should be:</span></span>
    
    * `CisAgentVersion:  1.0.9724.0`
    * `MdsAgentVersion: 35.2.2.0`
    * `Lsisas2Version: 2.0.78.00`


#### <a name="tooinstall-and-verify-maintenance-mode-hotfixes"></a><span data-ttu-id="de668-160">tooinstall 並確認 維護模式 hotfix</span><span class="sxs-lookup"><span data-stu-id="de668-160">tooinstall and verify maintenance mode hotfixes</span></span>

<span data-ttu-id="de668-161">使用 KB4037263 tooinstall 磁碟韌體更新。</span><span class="sxs-lookup"><span data-stu-id="de668-161">Use KB4037263 tooinstall disk firmware updates.</span></span> <span data-ttu-id="de668-162">這些更新具有干擾性，並採取 toocomplete 大約 30 分鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="de668-162">These are disruptive updates and take around 30 minutes toocomplete.</span></span> <span data-ttu-id="de668-163">您可以選擇 tooinstall 計劃性的維護視窗中的這些連接 toohello 裝置序列主控台。</span><span class="sxs-lookup"><span data-stu-id="de668-163">You can choose tooinstall these in a planned maintenance window by connecting toohello device serial console.</span></span>

> [!NOTE] 
> <span data-ttu-id="de668-164">如果磁碟韌體已經是最新狀態，您不需要 tooinstall 這些更新。</span><span class="sxs-lookup"><span data-stu-id="de668-164">If your disk firmware is already up-to-date, you won't need tooinstall these updates.</span></span> <span data-ttu-id="de668-165">執行 hello `Get-HcsUpdateAvailability` hello 裝置序列主控台 toocheck 如果更新可用，以及是否 hello cmdlet 更新具有干擾性 （維護模式） 或非干擾性 （一般模式） 的更新。</span><span class="sxs-lookup"><span data-stu-id="de668-165">Run hello `Get-HcsUpdateAvailability` cmdlet from hello device serial console toocheck if updates are available and whether hello updates are disruptive (maintenance mode) or non-disruptive (regular mode) updates.</span></span>

<span data-ttu-id="de668-166">tooinstall hello 磁碟韌體更新，請遵循下列的 hello 指示。</span><span class="sxs-lookup"><span data-stu-id="de668-166">tooinstall hello disk firmware updates, follow hello instructions below.</span></span>

1. <span data-ttu-id="de668-167">將 hello 裝置放在 hello 維護模式。</span><span class="sxs-lookup"><span data-stu-id="de668-167">Place hello device in hello maintenance mode.</span></span> 

    > [!NOTE] 
    > <span data-ttu-id="de668-168">連接 tooa 裝置處於維護模式時，請勿使用 Windows PowerShell 遠端功能。</span><span class="sxs-lookup"><span data-stu-id="de668-168">Do not use Windows PowerShell remoting when connecting tooa device in maintenance mode.</span></span> <span data-ttu-id="de668-169">改為在 hello 裝置控制器透過 hello 裝置序列主控台連接時執行這個指令程式。</span><span class="sxs-lookup"><span data-stu-id="de668-169">Instead run this cmdlet on hello device controller when connected through hello device serial console.</span></span>

    <span data-ttu-id="de668-170">tooplace hello 控制器在維護模式中，輸入：</span><span class="sxs-lookup"><span data-stu-id="de668-170">tooplace hello controller in maintenance mode, type:</span></span>
   
    `Enter-HcsMaintenanceMode`
   
    <span data-ttu-id="de668-171">下方顯示一項範例輸出。</span><span class="sxs-lookup"><span data-stu-id="de668-171">A sample output is shown below.</span></span>
   
        Controller0>Enter-HcsMaintenanceMode
        Checking device state...
   
        In maintenance mode, your device will not service IOs and will be disconnected from hello Microsoft Azure StorSimple Manager service. Entering maintenance mode will end hello current session and reboot both controllers, which takes a few minutes toocomplete. Are you sure you want tooenter maintenance mode?
        [Y] Yes [N] No (Default is "Y"): Y
   
        -----------------------MAINTENANCE MODE------------------------
        Microsoft Azure StorSimple Appliance Model 8600
        Name: Update4-8600-mystorsimple
        Copyright (C) 2014 Microsoft Corporation. All rights reserved.
        You are connected tooController0 - Passive
        ---------------------------------------------------------------
   
        Serial Console Menu
        [1] Log in with full access
        [2] Log into peer controller with full access
        [3] Connect with limited access
        [4] Change language
        Please enter your choice>
   
    <span data-ttu-id="de668-172">兩個 hello 控制器，然後重新啟動進入維護模式。</span><span class="sxs-lookup"><span data-stu-id="de668-172">Both hello controllers then restart into maintenance mode.</span></span>
2. <span data-ttu-id="de668-173">tooinstall hello 磁碟韌體更新，類型：</span><span class="sxs-lookup"><span data-stu-id="de668-173">tooinstall hello disk firmware update, type:</span></span>
   
    `Start-HcsHotfix -Path <path tooupdate file> -Credential <credentials in domain\username format>`
   
    <span data-ttu-id="de668-174">下方顯示一項範例輸出。</span><span class="sxs-lookup"><span data-stu-id="de668-174">A sample output is shown below.</span></span>
   
        Controller1>Start-HcsHotfix -Path \\10.100.100.100\share\ThirdOrderUpdates\ -Credential contoso\john
        Enter Password:
        WARNING: In maintenance mode, hotfixes should be installed on each controller sequentially. After hello hotfix is installed on this controller, install it on hello peer controller.
        Confirm
        This operation starts a hotfix installation and could reboot one or both of hello controllers. By installing new updates you agree to, and accept any additional terms associated with, hello new functionality listed in hello release notes (https://go.microsoft.com/fwLink/?LinkID=613790). Are you sure you want toocontinue?
        [Y] Yes [N] No (Default is "Y"): Y
        WARNING: Installation is currently in progress. This operation can take several minutes toocomplete.
3. <span data-ttu-id="de668-175">監視 hello 安裝進度使用`Get-HcsUpdateStatus`命令。</span><span class="sxs-lookup"><span data-stu-id="de668-175">Monitor hello install progress using `Get-HcsUpdateStatus` command.</span></span> <span data-ttu-id="de668-176">hello 更新已完成時 hello`RunInProgress`變更太`False`。</span><span class="sxs-lookup"><span data-stu-id="de668-176">hello update is complete when hello `RunInProgress` changes too`False`.</span></span>
4. <span data-ttu-id="de668-177">Hello 安裝完成後，重新啟動維護模式 hotfix 安裝在哪些 hello 的 hello 控制器。</span><span class="sxs-lookup"><span data-stu-id="de668-177">After hello installation is complete, hello controller on which hello maintenance mode hotfix was installed restarts.</span></span> <span data-ttu-id="de668-178">具有完整存取權的選項 1 身分登入，並確認 hello 磁碟韌體版本。</span><span class="sxs-lookup"><span data-stu-id="de668-178">Log in as option 1 with full access and verify hello disk firmware version.</span></span> <span data-ttu-id="de668-179">輸入：</span><span class="sxs-lookup"><span data-stu-id="de668-179">Type:</span></span>
   
   `Get-HcsFirmwareVersion`
   
   <span data-ttu-id="de668-180">hello 預期磁碟韌體版本：</span><span class="sxs-lookup"><span data-stu-id="de668-180">hello expected disk firmware versions are:</span></span>
   
   `XMGJ, XGEG, KZ50, F6C2, VR08, N003, 0107`
   
   <span data-ttu-id="de668-181">下方顯示一項範例輸出。</span><span class="sxs-lookup"><span data-stu-id="de668-181">A sample output is shown below.</span></span>
   
       -----------------------MAINTENANCE MODE------------------------
       Microsoft Azure StorSimple Appliance Model 8600
       Name: Update4-8600-mystorsimple
       Software Version: 6.3.9600.17845
       Copyright (C) 2014 Microsoft Corporation. All rights reserved.
       You are connected tooController1
       ---------------------------------------------------------------
   
       Controller1>Get-HcsFirmwareVersion
   
       Controller0 : TalladegaFirmware
           ActiveBIOS:0.45.0010
              BackupBIOS:0.45.0006
              MainCPLD:17.0.000b
              ActiveBMCRoot:2.0.001F
              BackupBMCRoot:2.0.001F
              BMCBoot:2.0.0002
              LsiFirmware:20.00.04.00
              LsiBios:07.37.00.00
              Battery1Firmware:06.2C
              Battery2Firmware:06.2C
              DomFirmware:X231600
              CanisterFirmware:3.5.0.56
              CanisterBootloader:5.03
              CanisterConfigCRC:0x9134777A
              CanisterVPDStructure:0x06
              CanisterGEMCPLD:0x19
              CanisterVPDCRC:0x142F7DC2
              MidplaneVPDStructure:0x0C
              MidplaneVPDCRC:0xA6BD4F64
              MidplaneCPLD:0x10
              PCM1Firmware:1.00|1.05
              PCM1VPDStructure:0x05
              PCM1VPDCRC:0x41BEF99C
              PCM2Firmware:1.00|1.05
              PCM2VPDStructure:0x05
              PCM2VPDCRC:0x41BEF99C

           EbodFirmware
              CanisterFirmware:3.5.0.56
              CanisterBootloader:5.03
              CanisterConfigCRC:0xB23150F8
              CanisterVPDStructure:0x06
              CanisterGEMCPLD:0x14
              CanisterVPDCRC:0xBAA55828
              MidplaneVPDStructure:0x0C
              MidplaneVPDCRC:0xA6BD4F64
              MidplaneCPLD:0x10
              PCM1Firmware:3.11
              PCM1VPDStructure:0x03
              PCM1VPDCRC:0x6B58AD13
              PCM2Firmware:3.11
              PCM2VPDStructure:0x03
              PCM2VPDCRC:0x6B58AD13

           DisksFirmware
              SmrtStor:TXA2D20800GA6XYR:KZ50
              SmrtStor:TXA2D20800GA6XYR:KZ50
              SmrtStor:TXA2D20800GA6XYR:KZ50
              SmrtStor:TXA2D20800GA6XYR:KZ50
              SmrtStor:TXA2D20800GA6XYR:KZ50
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
   
    <span data-ttu-id="de668-182">執行 hello `Get-HcsFirmwareVersion` hello 第二個控制站 tooverify 的 hello 軟體版本上的命令已經過更新。</span><span class="sxs-lookup"><span data-stu-id="de668-182">Run hello `Get-HcsFirmwareVersion` command on hello second controller tooverify that hello software version has been updated.</span></span> <span data-ttu-id="de668-183">然後您就可以結束 hello 維護模式。</span><span class="sxs-lookup"><span data-stu-id="de668-183">You can then exit hello maintenance mode.</span></span> <span data-ttu-id="de668-184">toodo 因此，請輸入下列命令，每個裝置控制器的 hello:</span><span class="sxs-lookup"><span data-stu-id="de668-184">toodo so, type hello following command for each device controller:</span></span>
   
   `Exit-HcsMaintenanceMode`

5. <span data-ttu-id="de668-185">當您結束維護模式時，重新啟動 hello 控制站。</span><span class="sxs-lookup"><span data-stu-id="de668-185">hello controllers restart when you exit maintenance mode.</span></span> <span data-ttu-id="de668-186">已成功套用之後 hello 磁碟韌體更新，而且 hello 裝置已離開維護模式，傳回 toohello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="de668-186">After hello disk firmware updates are successfully applied and hello device has exited maintenance mode, return toohello Azure portal.</span></span> <span data-ttu-id="de668-187">請注意該 hello 入口網站可能不會顯示您安裝的 24 小時內的 hello 維護模式更新。</span><span class="sxs-lookup"><span data-stu-id="de668-187">Note that hello portal might not show that you installed hello maintenance mode updates for 24 hours.</span></span>

