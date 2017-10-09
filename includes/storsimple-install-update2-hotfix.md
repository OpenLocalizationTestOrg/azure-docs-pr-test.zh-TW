<!--author=alkohli last changed: 03/17/16-->

#### <a name="toodownload-hotfixes"></a><span data-ttu-id="769e2-101">toodownload hotfix</span><span class="sxs-lookup"><span data-stu-id="769e2-101">toodownload hotfixes</span></span>
<span data-ttu-id="769e2-102">執行 hello hello Microsoft Update 類別目錄中的下列步驟 toodownload hello 軟體更新。</span><span class="sxs-lookup"><span data-stu-id="769e2-102">Perform hello following steps toodownload hello software update from hello Microsoft Update Catalog.</span></span>

1. <span data-ttu-id="769e2-103">啟動 Internet Explorer 並瀏覽過[http://catalog.update.microsoft.com](http://catalog.update.microsoft.com)。</span><span class="sxs-lookup"><span data-stu-id="769e2-103">Start Internet Explorer and navigate too[http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span></span>
2. <span data-ttu-id="769e2-104">如果這是您第一次使用 hello Microsoft Update 類別目錄，在此電腦上，按一下**安裝**時提示的 tooinstall hello Microsoft Update 類別目錄的附加元件。</span><span class="sxs-lookup"><span data-stu-id="769e2-104">If this is your first time using hello Microsoft Update Catalog on this computer, click **Install** when prompted tooinstall hello Microsoft Update Catalog add-on.</span></span>
    <span data-ttu-id="769e2-105">![安裝目錄](./media/storsimple-install-update2-hotfix/HCS_InstallCatalog-include.png)</span><span class="sxs-lookup"><span data-stu-id="769e2-105">![Install catalog](./media/storsimple-install-update2-hotfix/HCS_InstallCatalog-include.png)</span></span>
3. <span data-ttu-id="769e2-106">在 hello hello Microsoft Update 類別目錄的搜尋方塊中輸入 hello 知識庫 (KB) 號碼 hello hotfix 您想讓 toodownload，例如**3121901**，然後按一下**搜尋**。</span><span class="sxs-lookup"><span data-stu-id="769e2-106">In hello search box of hello Microsoft Update Catalog, enter hello Knowledge Base (KB) number of hello hotfix you want toodownload, for example **3121901**, and then click **Search**.</span></span>
   
    <span data-ttu-id="769e2-107">hello hotfix 清單會出現，例如**StorSimple 8000 系列的累計軟體配套更新 2.0**。</span><span class="sxs-lookup"><span data-stu-id="769e2-107">hello hotfix listing appears, for example, **Cumulative Software Bundle Update 2.0 for StorSimple 8000 Series**.</span></span>
   
    ![搜尋目錄](./media/storsimple-install-update2-hotfix/HCS_SearchCatalog1-include.png)
4. <span data-ttu-id="769e2-109">按一下 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="769e2-109">Click **Add**.</span></span> <span data-ttu-id="769e2-110">hello 更新已新增 toohello 籃。</span><span class="sxs-lookup"><span data-stu-id="769e2-110">hello update is added toohello basket.</span></span>
5. <span data-ttu-id="769e2-111">Hello 上表中列出的搜尋任何其他的 hotfix (**3121900**， **3080728**， **3090322**，和**3121899**)，並將每個hello 購物籃中。</span><span class="sxs-lookup"><span data-stu-id="769e2-111">Search for any additional hotfixes listed in hello table above (**3121900**, **3080728**, **3090322**, and **3121899**), and add each hello basket.</span></span>
6. <span data-ttu-id="769e2-112">按一下 [ **檢視購物籃**]。</span><span class="sxs-lookup"><span data-stu-id="769e2-112">Click **View Basket**.</span></span>
7. <span data-ttu-id="769e2-113">按一下 [下載] 。</span><span class="sxs-lookup"><span data-stu-id="769e2-113">Click **Download**.</span></span> <span data-ttu-id="769e2-114">指定或**瀏覽**所在 hello 下載 tooappear tooa 本機位置。</span><span class="sxs-lookup"><span data-stu-id="769e2-114">Specify or **Browse** tooa local location where you want hello downloads tooappear.</span></span> <span data-ttu-id="769e2-115">hello 下載更新 toohello 指定的位置，並放在名稱為 「 hello 更新相同的 hello 與子資料夾中。</span><span class="sxs-lookup"><span data-stu-id="769e2-115">hello updates are downloaded toohello specified location and placed in a subfolder with hello same name as hello update.</span></span> <span data-ttu-id="769e2-116">hello 資料夾也可以複製的 tooa 從 hello 裝置的網路共用。</span><span class="sxs-lookup"><span data-stu-id="769e2-116">hello folder can also be copied tooa network share that is reachable from hello device.</span></span>

> [!NOTE]
> <span data-ttu-id="769e2-117">hello hotfix 必須能夠從這兩個控制器 toodetect，hello 同儕節點控制器的任何潛在的錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="769e2-117">hello hotfixes must be accessible from both controllers toodetect any potential error messages from hello peer controller.</span></span>
> 
> 

#### <a name="tooinstall-and-verify-regular-mode-hotfixes"></a><span data-ttu-id="769e2-118">tooinstall 並確認一般模式 hotfix</span><span class="sxs-lookup"><span data-stu-id="769e2-118">tooinstall and verify regular mode hotfixes</span></span>
<span data-ttu-id="769e2-119">執行下列步驟 tooinstall hello，並確認一般模式 hotfix。</span><span class="sxs-lookup"><span data-stu-id="769e2-119">Perform hello following steps tooinstall and verify regular-mode hotfixes.</span></span> <span data-ttu-id="769e2-120">如果您已安裝使用 hello Azure 入口網站中，跳過[安裝，並確認 維護模式 hotfix](#to-install-and-verify-maintenance-mode-hotfixes)。</span><span class="sxs-lookup"><span data-stu-id="769e2-120">If you already installed them using hello Azure Portal, skip ahead too[install and verify maintenance mode hotfixes](#to-install-and-verify-maintenance-mode-hotfixes).</span></span>

1. <span data-ttu-id="769e2-121">您的 StorSimple 裝置序列主控台存取 hello Windows PowerShell 介面 tooinstall hello hotfix。</span><span class="sxs-lookup"><span data-stu-id="769e2-121">tooinstall hello hotfixes, access hello Windows PowerShell interface on your StorSimple device serial console.</span></span> <span data-ttu-id="769e2-122">請遵循詳細指示中的 hello[使用 PuTTy tooconnect toohello 序列主控台](../articles/storsimple/storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console)。</span><span class="sxs-lookup"><span data-stu-id="769e2-122">Follow hello detailed instructions in [Use PuTTy tooconnect toohello serial console](../articles/storsimple/storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span></span> <span data-ttu-id="769e2-123">在 hello 命令提示字元中，按下**Enter**。</span><span class="sxs-lookup"><span data-stu-id="769e2-123">At hello command prompt, press **Enter**.</span></span>
2. <span data-ttu-id="769e2-124">選取**選項 1** toolog toohello 具有完整存取權的裝置上。</span><span class="sxs-lookup"><span data-stu-id="769e2-124">Select **Option 1** toolog on toohello device with full access.</span></span>
3. <span data-ttu-id="769e2-125">tooinstall hello hotfix，在 hello 命令提示字元，輸入：</span><span class="sxs-lookup"><span data-stu-id="769e2-125">tooinstall hello hotfix, at hello command prompt, type:</span></span>
   
    `Start-HcsHotfix -Path <path tooupdate file> -Credential <credentials in domain\username format>`
   
    <span data-ttu-id="769e2-126">Hello 上述命令中的共用路徑中使用 IP，而不是 DNS。</span><span class="sxs-lookup"><span data-stu-id="769e2-126">Use IP rather than DNS in share path in hello above command.</span></span> <span data-ttu-id="769e2-127">只有當您要存取已驗證的共用時，才使用 hello 認證參數。</span><span class="sxs-lookup"><span data-stu-id="769e2-127">hello credential parameter is used only if you are accessing an authenticated share.</span></span>
   
    <span data-ttu-id="769e2-128">我們建議您使用 hello 認證參數 tooaccess 共用。</span><span class="sxs-lookup"><span data-stu-id="769e2-128">We recommend that you use hello credential parameter tooaccess shares.</span></span> <span data-ttu-id="769e2-129">即使已開啟太"everyone"通常的共用開啟 toounauthenticated 使用者。</span><span class="sxs-lookup"><span data-stu-id="769e2-129">Even shares that are open too“everyone” are typically not open toounauthenticated users.</span></span>
   
    <span data-ttu-id="769e2-130">下方顯示一項範例輸出。</span><span class="sxs-lookup"><span data-stu-id="769e2-130">A sample output is shown below.</span></span>
   
    ```
    Controller0>Start-HcsHotfix -Path \\10.100.100.100\share
    \hcsmdssoftwareupdate.exe -Credential contoso\John

    Confirm

    This operation starts hello hotfix installation and could reboot one or
    both of hello controllers. If hello device is serving I/Os, these will not
    be disrupted. Are you sure you want toocontinue?
    [Y] Yes [N] No [?] Help (default is "Y"): Y
    ```
4. <span data-ttu-id="769e2-131">型別**Y**時提示的 tooconfirm hello hotfix 安裝。</span><span class="sxs-lookup"><span data-stu-id="769e2-131">Type **Y** when prompted tooconfirm hello hotfix installation.</span></span>
5. <span data-ttu-id="769e2-132">使用 hello 監視 hello 更新`Get-HcsUpdateStatus`cmdlet。</span><span class="sxs-lookup"><span data-stu-id="769e2-132">Monitor hello update by using hello `Get-HcsUpdateStatus` cmdlet.</span></span>
   
    <span data-ttu-id="769e2-133">hello 下列範例輸出顯示 hello 更新正在進行中。</span><span class="sxs-lookup"><span data-stu-id="769e2-133">hello following sample output shows hello update in progress.</span></span> <span data-ttu-id="769e2-134">hello`RunInprogress`將`True`hello 更新正在進行中。</span><span class="sxs-lookup"><span data-stu-id="769e2-134">hello `RunInprogress` will be `True` when hello update is in progress.</span></span>
   
    ```
    Controller0>Get-HcsUpdateStatus
    RunInprogress       : True
    LastHotfixTimestamp : 12/21/2015 10:36:13 PM
    LastUpdateTimestamp : 12/21/2015 10:35:25 PM
    Controller0Events   :
    Controller1Events   :
    ```
   
     <span data-ttu-id="769e2-135">下列範例輸出的 hello 指出該 hello 更新已完成。</span><span class="sxs-lookup"><span data-stu-id="769e2-135">hello following sample output indicates that hello update is finished.</span></span> <span data-ttu-id="769e2-136">hello`RunInProgress`將`False`hello 更新已完成時。</span><span class="sxs-lookup"><span data-stu-id="769e2-136">hello `RunInProgress` will be `False` when hello update has completed.</span></span>
   
    ```
    Controller1>Get-HcsUpdateStatus

    RunInprogress       : False
    LastHotfixTimestamp : 12/21/2015 10:59:13 PM
    LastUpdateTimestamp : 12/21/2015 10:35:25 PM
    Controller0Events   :
    Controller1Events   :
    ```
   
   > [!NOTE]
   > <span data-ttu-id="769e2-137">有時候，hello cmdlet 報告`False`hello 更新時仍在進行中。</span><span class="sxs-lookup"><span data-stu-id="769e2-137">Occasionally, hello cmdlet reports `False` when hello update is still in progress.</span></span> <span data-ttu-id="769e2-138">hello hotfix 的 tooensure 已完成、 等候幾分鐘的時間，重新執行此命令並確認該 hello`RunInProgress`是`False`。</span><span class="sxs-lookup"><span data-stu-id="769e2-138">tooensure that hello hotfix is complete, wait for a few minutes, rerun this command and verify that hello `RunInProgress` is `False`.</span></span> <span data-ttu-id="769e2-139">如果是，已完成 hello hotfix。</span><span class="sxs-lookup"><span data-stu-id="769e2-139">If it is, then hello hotfix has completed.</span></span>

6. <span data-ttu-id="769e2-140">之後 hello 的軟體更新已完成，重複執行步驟 3-5 tooinstall 和監視器 hello SaaS 代理程式與 MDS 代理程式。</span><span class="sxs-lookup"><span data-stu-id="769e2-140">After hello software update is complete, repeat steps 3-5 tooinstall and monitor hello SaaS agent and MDS agent .</span></span> <span data-ttu-id="769e2-141">請確保您是先安裝 `all-hcsmdssoftwareupdate_0b438ddf0d5b686aada2378b754fac8c7f2160e9.exe`，再安裝 `all-cismdsagentupdatebundle_f98e62f4d56c79e2a6644d027af7a2393a93827a.exe`。</span><span class="sxs-lookup"><span data-stu-id="769e2-141">Ensure that `all-hcsmdssoftwareupdate_0b438ddf0d5b686aada2378b754fac8c7f2160e9.exe` is installed before `all-cismdsagentupdatebundle_f98e62f4d56c79e2a6644d027af7a2393a93827a.exe`.</span></span>
7. <span data-ttu-id="769e2-142">請確認 hello 系統軟體版本。</span><span class="sxs-lookup"><span data-stu-id="769e2-142">Verify hello system software versions.</span></span> <span data-ttu-id="769e2-143">輸入：</span><span class="sxs-lookup"><span data-stu-id="769e2-143">Type:</span></span>
   
    `Get-HcsSystem`
   
    <span data-ttu-id="769e2-144">您應該會看到下列版本的 hello:</span><span class="sxs-lookup"><span data-stu-id="769e2-144">You should see hello following versions:</span></span>
   
   * <span data-ttu-id="769e2-145">HcsSoftwareVersion：6.3.9600.17673</span><span class="sxs-lookup"><span data-stu-id="769e2-145">HcsSoftwareVersion: 6.3.9600.17673</span></span>
   * <span data-ttu-id="769e2-146">CisAgentVersion：1.0.9150.0</span><span class="sxs-lookup"><span data-stu-id="769e2-146">CisAgentVersion: 1.0.9150.0</span></span>
   * <span data-ttu-id="769e2-147">MdsAgentVersion：30.0.4698.13</span><span class="sxs-lookup"><span data-stu-id="769e2-147">MdsAgentVersion: 30.0.4698.13</span></span>
     
     <span data-ttu-id="769e2-148">如果 hello 版本號碼不會變更 hello 項更新，則表示該 hello hotfix tooapply 失敗。</span><span class="sxs-lookup"><span data-stu-id="769e2-148">If hello version numbers do not change after applying hello update, it indicates that hello hotfix has failed tooapply.</span></span> <span data-ttu-id="769e2-149">若您看到這種情況，請連絡 [Microsoft 支援](../articles/storsimple/storsimple-contact-microsoft-support.md)以取得進一步的協助。</span><span class="sxs-lookup"><span data-stu-id="769e2-149">Should you see this, please contact [Microsoft Support](../articles/storsimple/storsimple-contact-microsoft-support.md) for further assistance.</span></span>
8. <span data-ttu-id="769e2-150">重複步驟 3-5 tooinstall hello 剩餘一般模式 hotfix。</span><span class="sxs-lookup"><span data-stu-id="769e2-150">Repeat steps 3-5 tooinstall hello remaining regular-mode hotfixes.</span></span>
   
   * <span data-ttu-id="769e2-151">hello LSI 驅動程式-KB3121900</span><span class="sxs-lookup"><span data-stu-id="769e2-151">hello LSI driver - KB3121900</span></span>
   * <span data-ttu-id="769e2-152">hello Storport 更新-KB3080728</span><span class="sxs-lookup"><span data-stu-id="769e2-152">hello Storport update - KB3080728</span></span>
   * <span data-ttu-id="769e2-153">hello 太空更新-KB3090322</span><span class="sxs-lookup"><span data-stu-id="769e2-153">hello Spaceport update - KB3090322</span></span>

#### <a name="tooinstall-and-verify-maintenance-mode-hotfixes"></a><span data-ttu-id="769e2-154">tooinstall 並確認 維護模式 hotfix</span><span class="sxs-lookup"><span data-stu-id="769e2-154">tooinstall and verify maintenance mode hotfixes</span></span>
<span data-ttu-id="769e2-155">使用 KB3121899 tooinstall 磁碟韌體更新。</span><span class="sxs-lookup"><span data-stu-id="769e2-155">Use KB3121899 tooinstall disk firmware updates.</span></span> <span data-ttu-id="769e2-156">這些更新具有干擾性，並採取 toocomplete 大約 30 分鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="769e2-156">These are disruptive updates and take around 30 minutes toocomplete.</span></span> <span data-ttu-id="769e2-157">您可以選擇 tooinstall 計劃性的維護視窗中的這些連接 toohello 裝置序列主控台。</span><span class="sxs-lookup"><span data-stu-id="769e2-157">You can choose tooinstall these in a planned maintenance window by connecting toohello device serial console.</span></span>

<span data-ttu-id="769e2-158">請注意，是否磁碟韌體已經是最新的就不需要 tooinstall 這些更新。</span><span class="sxs-lookup"><span data-stu-id="769e2-158">Note that if your disk firmware is already up-to-date, you won't need tooinstall these updates.</span></span> <span data-ttu-id="769e2-159">執行 hello `Get-HcsUpdateAvailability` hello 裝置序列主控台 toocheck 如果更新可用，以及是否 hello cmdlet 更新具有干擾性 （維護模式） 或非干擾性 （一般模式） 的更新。</span><span class="sxs-lookup"><span data-stu-id="769e2-159">Run hello `Get-HcsUpdateAvailability` cmdlet from hello device serial console toocheck if updates are available and whether hello updates are disruptive (maintenance mode) or non-disruptive (regular mode) updates.</span></span>

<span data-ttu-id="769e2-160">tooinstall hello 磁碟韌體更新，請遵循下列的 hello 指示。</span><span class="sxs-lookup"><span data-stu-id="769e2-160">tooinstall hello disk firmware updates, follow hello instructions below.</span></span>

1. <span data-ttu-id="769e2-161">將 hello 裝置放在 hello 維護模式。</span><span class="sxs-lookup"><span data-stu-id="769e2-161">Place hello device in hello Maintenance mode.</span></span> <span data-ttu-id="769e2-162">請注意，您不應該使用 Windows PowerShell 遠端連接 tooa 裝置處於維護模式時。</span><span class="sxs-lookup"><span data-stu-id="769e2-162">Note that you should not use Windows PowerShell remoting when connecting tooa device in Maintenance mode.</span></span> <span data-ttu-id="769e2-163">改為在 hello 裝置控制器透過 hello 裝置序列主控台連接時執行這個指令程式。</span><span class="sxs-lookup"><span data-stu-id="769e2-163">Instead run this cmdlet on hello device controller when connected through hello device serial console.</span></span> <span data-ttu-id="769e2-164">輸入：</span><span class="sxs-lookup"><span data-stu-id="769e2-164">Type:</span></span>
   
    `Enter-HcsMaintenanceMode`
   
    <span data-ttu-id="769e2-165">下方顯示一項範例輸出。</span><span class="sxs-lookup"><span data-stu-id="769e2-165">A sample output is shown below.</span></span>
   
        Controller0>Enter-HcsMaintenanceMode
        Checking device state...
   
        In maintenance mode, your device will not service IOs and will be disconnected from hello Microsoft Azure StorSimple Manager service. Entering maintenance mode will end hello current session and reboot both controllers, which takes a few minutes toocomplete. Are you sure you want tooenter maintenance mode?
        [Y] Yes [N] No (Default is "Y"): Y
   
        -----------------------MAINTENANCE MODE------------------------
        Microsoft Azure StorSimple Appliance Model 8100
        Name: Update2-8100-SHG0997879L76YD
        Software Version: 6.3.9600.17664
        Copyright (C) 2014 Microsoft Corporation. All rights reserved.
        You are connected tooController0 - Passive
        ---------------------------------------------------------------
   
        Serial Console Menu
        [1] Log in with full access
        [2] Log into peer controller with full access
        [3] Connect with limited access
        [4] Change language
        Please enter your choice>
   
    <span data-ttu-id="769e2-166">兩個 hello 控制器，然後重新啟動進入維護模式。</span><span class="sxs-lookup"><span data-stu-id="769e2-166">Both hello controllers then restart into Maintenance mode.</span></span>
2. <span data-ttu-id="769e2-167">tooinstall hello 磁碟韌體更新，類型：</span><span class="sxs-lookup"><span data-stu-id="769e2-167">tooinstall hello disk firmware update, type:</span></span>
   
    `Start-HcsHotfix -Path <path tooupdate file> -Credential <credentials in domain\username format>`
   
    <span data-ttu-id="769e2-168">下方顯示一項範例輸出。</span><span class="sxs-lookup"><span data-stu-id="769e2-168">A sample output is shown below.</span></span>
   
        Controller1>Start-HcsHotfix -Path \\10.100.100.100\share\DiskFirmwarePackage.exe -Credential contoso\john
        Enter Password:
        WARNING: In maintenance mode, hotfixes should be installed on each controller sequentially. After hello hotfix is installed on this controller, install it on hello peer controller.
        Confirm
        This operation starts a hotfix installation and could reboot one or both of hello controllers. By installing new updates you agree to, and accept any additional terms associated with, hello new functionality listed in hello release notes (https://go.microsoft.com/fwLink/?LinkID=613790). Are you sure you want toocontinue?
        [Y] Yes [N] No (Default is "Y"): Y
        WARNING: Installation is currently in progress. This operation can take several minutes toocomplete.
3. <span data-ttu-id="769e2-169">監視 hello 安裝進度使用`Get-HcsUpdateStatus`命令。</span><span class="sxs-lookup"><span data-stu-id="769e2-169">Monitor hello install progress using `Get-HcsUpdateStatus` command.</span></span> <span data-ttu-id="769e2-170">hello 更新已完成時 hello`RunInProgress`變更太`False`。</span><span class="sxs-lookup"><span data-stu-id="769e2-170">hello update is complete when hello `RunInProgress` changes too`False`.</span></span>
4. <span data-ttu-id="769e2-171">Hello 安裝完成後，重新啟動維護模式 hotfix 安裝在哪些 hello 的 hello 控制器。</span><span class="sxs-lookup"><span data-stu-id="769e2-171">After hello installation is complete, hello controller on which hello maintenance mode hotfix was installed restarts.</span></span> <span data-ttu-id="769e2-172">具有完整存取權的選項 1 身分登入，並確認 hello 磁碟韌體版本。</span><span class="sxs-lookup"><span data-stu-id="769e2-172">Log in as option 1 with full access and verify hello disk firmware version.</span></span> <span data-ttu-id="769e2-173">輸入：</span><span class="sxs-lookup"><span data-stu-id="769e2-173">Type:</span></span>
   
   `Get-HcsFirmwareVersion`
   
   <span data-ttu-id="769e2-174">hello 預期磁碟韌體版本：</span><span class="sxs-lookup"><span data-stu-id="769e2-174">hello expected disk firmware versions are:</span></span>
   
   `XMGG, XGEG, KZ50, F6C2, VR08`
   
   <span data-ttu-id="769e2-175">下方顯示一項範例輸出。</span><span class="sxs-lookup"><span data-stu-id="769e2-175">A sample output is shown below.</span></span>
   
       -----------------------MAINTENANCE MODE------------------------
       Microsoft Azure StorSimple Appliance Model 8100
       Name: Update2-8100-SHG0997879L76YD
       Software Version: 6.3.9600.17664
       Copyright (C) 2014 Microsoft Corporation. All rights reserved.
       You are connected tooController1
       ---------------------------------------------------------------
   
       Controller1>Get-HcsFirmwareVersion
   
       Controller0 : TalladegaFirmware
         ActiveBIOS:0.45.0006
         BackupBIOS:0.45.0008
         MainCPLD:17.0.0005
         ActiveBMCRoot:2.0.000E
         BackupBMCRoot:2.0.000E
         BMCBoot:2.0.0001
         LsiFirmware:19.00.00.00
         LsiBios:07.37.00.00
         Battery1Firmware:06.29
         Battery2Firmware:06.29
         DomFirmware:X231600
         CanisterFirmware:3.5.0.32
         CanisterBootloader:5.03
         CanisterConfigCRC:0xD1B030A4
         CanisterVPDStructure:0x06
         CanisterGEMCPLD:0x17
         CanisterVPDCRC:0xEE3504B4
         MidplaneVPDStructure:0x0C
         MidplaneVPDCRC:0xA6BD4F64
         MidplaneCPLD:0x10
         PCM1Firmware:1.00|1.05
         PCM1VPDStructure:0x05
         PCM1VPDCRC:0x41BEF99C
         PCM2Firmware:1.00|1.05
         PCM2VPDStructure:0x05
         PCM2VPDCRC:0x41BEF99C
   
         DisksFirmware
         SEAGATE:ST400FM0073:XGEG
         SEAGATE:ST400FM0073:XGEG
         SEAGATE:ST400FM0073:XGEG
         SEAGATE:ST400FM0073:XGEG
         SEAGATE:ST4000NM0023:XMGG
         SEAGATE:ST4000NM0023:XMGG
         SEAGATE:ST4000NM0023:XMGG
         SEAGATE:ST4000NM0023:XMGG
         SEAGATE:ST4000NM0023:XMGG
         SEAGATE:ST4000NM0023:XMGG
         SEAGATE:ST4000NM0023:XMGG
         SEAGATE:ST4000NM0023:XMGG
   
    <span data-ttu-id="769e2-176">執行 hello `Get-HcsFirmwareVersion` hello 第二個控制站 tooverify 的 hello 軟體版本上的命令已經過更新。</span><span class="sxs-lookup"><span data-stu-id="769e2-176">Run hello `Get-HcsFirmwareVersion` command on hello second controller tooverify that hello software version has been updated.</span></span> <span data-ttu-id="769e2-177">然後您就可以結束 hello 維護模式。</span><span class="sxs-lookup"><span data-stu-id="769e2-177">You can then exit hello maintenance mode.</span></span> <span data-ttu-id="769e2-178">toodo 因此，請輸入下列命令，每個裝置控制器的 hello:</span><span class="sxs-lookup"><span data-stu-id="769e2-178">toodo so, type hello following command for each device controller:</span></span>
   
   `Exit-HcsMaintenanceMode`
5. <span data-ttu-id="769e2-179">當您結束維護模式時，重新啟動 hello 控制站。</span><span class="sxs-lookup"><span data-stu-id="769e2-179">hello controllers restart when you exit Maintenance mode.</span></span> <span data-ttu-id="769e2-180">已成功套用之後 hello 磁碟韌體更新，而且 hello 裝置已離開維護模式，傳回 toohello Azure 傳統入口網站。</span><span class="sxs-lookup"><span data-stu-id="769e2-180">After hello disk firmware updates are successfully applied and hello device has exited maintenance mode, return toohello Azure classic portal.</span></span> <span data-ttu-id="769e2-181">請注意該 hello 入口網站可能不會顯示您安裝的 24 小時內的 hello 維護模式更新。</span><span class="sxs-lookup"><span data-stu-id="769e2-181">Note that hello portal might not show that you installed hello Maintenance mode updates for 24 hours.</span></span>

