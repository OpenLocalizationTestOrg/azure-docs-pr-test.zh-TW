<!--author=alkohli last changed: 03/17/16-->

#### <a name="to-download-hotfixes"></a><span data-ttu-id="1a331-101">下載 Hofix</span><span class="sxs-lookup"><span data-stu-id="1a331-101">To download hotfixes</span></span>
<span data-ttu-id="1a331-102">請執行下列步驟，從 Microsoft Update Catalog 下載軟體更新。</span><span class="sxs-lookup"><span data-stu-id="1a331-102">Perform the following steps to download the software update from the Microsoft Update Catalog.</span></span>

1. <span data-ttu-id="1a331-103">啟動 Internet Explorer 並瀏覽至 [http://catalog.update.microsoft.com](http://catalog.update.microsoft.com)。</span><span class="sxs-lookup"><span data-stu-id="1a331-103">Start Internet Explorer and navigate to [http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span></span>
2. <span data-ttu-id="1a331-104">如果這是您在此電腦上第一次使用 Microsoft Update Catalog，請在系統提示您安裝 Microsoft Update Catalog 附加元件時，按一下 [安裝]  。</span><span class="sxs-lookup"><span data-stu-id="1a331-104">If this is your first time using the Microsoft Update Catalog on this computer, click **Install** when prompted to install the Microsoft Update Catalog add-on.</span></span>
    <span data-ttu-id="1a331-105">![安裝目錄](./media/storsimple-install-update2-hotfix/HCS_InstallCatalog-include.png)</span><span class="sxs-lookup"><span data-stu-id="1a331-105">![Install catalog](./media/storsimple-install-update2-hotfix/HCS_InstallCatalog-include.png)</span></span>
3. <span data-ttu-id="1a331-106">在 Microsoft Update Catalog 的搜尋方塊中，輸入您要下載的 Hotfix 知識庫 (KB) 編號 (例如 **3121901**)，然後按一下 [搜尋]。</span><span class="sxs-lookup"><span data-stu-id="1a331-106">In the search box of the Microsoft Update Catalog, enter the Knowledge Base (KB) number of the hotfix you want to download, for example **3121901**, and then click **Search**.</span></span>
   
    <span data-ttu-id="1a331-107">Hotfix 清單隨即出現，例如 **適用於 StorSimple 8000 系列的累積軟體套件組合更新 2.0**。</span><span class="sxs-lookup"><span data-stu-id="1a331-107">The hotfix listing appears, for example, **Cumulative Software Bundle Update 2.0 for StorSimple 8000 Series**.</span></span>
   
    ![搜尋目錄](./media/storsimple-install-update2-hotfix/HCS_SearchCatalog1-include.png)
4. <span data-ttu-id="1a331-109">按一下 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="1a331-109">Click **Add**.</span></span> <span data-ttu-id="1a331-110">更新便會新增到購物籃中。</span><span class="sxs-lookup"><span data-stu-id="1a331-110">The update is added to the basket.</span></span>
5. <span data-ttu-id="1a331-111">搜尋上表中所列的其他任何 Hotfix (**3121900**、**3080728**、**3090322** 和 **3121899**)，然後加入每個購物籃。</span><span class="sxs-lookup"><span data-stu-id="1a331-111">Search for any additional hotfixes listed in the table above (**3121900**, **3080728**, **3090322**, and **3121899**), and add each the basket.</span></span>
6. <span data-ttu-id="1a331-112">按一下 [ **檢視購物籃**]。</span><span class="sxs-lookup"><span data-stu-id="1a331-112">Click **View Basket**.</span></span>
7. <span data-ttu-id="1a331-113">按一下 [下載] 。</span><span class="sxs-lookup"><span data-stu-id="1a331-113">Click **Download**.</span></span> <span data-ttu-id="1a331-114">指定或「瀏覽」  至您想要儲存下載項目的本機位置。</span><span class="sxs-lookup"><span data-stu-id="1a331-114">Specify or **Browse** to a local location where you want the downloads to appear.</span></span> <span data-ttu-id="1a331-115">更新便會下載到指定的位置，並放在與更新名稱相同的子資料夾中。</span><span class="sxs-lookup"><span data-stu-id="1a331-115">The updates are downloaded to the specified location and placed in a subfolder with the same name as the update.</span></span> <span data-ttu-id="1a331-116">資料夾也可以複製到裝置可連線的網路共用位置。</span><span class="sxs-lookup"><span data-stu-id="1a331-116">The folder can also be copied to a network share that is reachable from the device.</span></span>

> [!NOTE]
> <span data-ttu-id="1a331-117">Hotfix 必須可同時從兩個控制器存取，以偵測來自對等控制器的任何潛在錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="1a331-117">The hotfixes must be accessible from both controllers to detect any potential error messages from the peer controller.</span></span>
> 
> 

#### <a name="to-install-and-verify-regular-mode-hotfixes"></a><span data-ttu-id="1a331-118">安裝及驗證一般模式 Hotfix</span><span class="sxs-lookup"><span data-stu-id="1a331-118">To install and verify regular mode hotfixes</span></span>
<span data-ttu-id="1a331-119">執行下列步驟來安裝及驗證一般模式 Hotfix。</span><span class="sxs-lookup"><span data-stu-id="1a331-119">Perform the following steps to install and verify regular-mode hotfixes.</span></span> <span data-ttu-id="1a331-120">如果您已使用 Azure 入口網站安裝這些 Hotfix，請直接跳到 [安裝及驗證維護模式 Hotfix](#to-install-and-verify-maintenance-mode-hotfixes)。</span><span class="sxs-lookup"><span data-stu-id="1a331-120">If you already installed them using the Azure Portal, skip ahead to [install and verify maintenance mode hotfixes](#to-install-and-verify-maintenance-mode-hotfixes).</span></span>

1. <span data-ttu-id="1a331-121">若要安裝 Hotfix，請存取 StorSimple 裝置序列主控台上的 Windows PowerShell 介面。</span><span class="sxs-lookup"><span data-stu-id="1a331-121">To install the hotfixes, access the Windows PowerShell interface on your StorSimple device serial console.</span></span> <span data-ttu-id="1a331-122">請依照[使用 PuTTy 連接到序列主控台](../articles/storsimple/storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console)中的詳細指示執行作業。</span><span class="sxs-lookup"><span data-stu-id="1a331-122">Follow the detailed instructions in [Use PuTTy to connect to the serial console](../articles/storsimple/storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span></span> <span data-ttu-id="1a331-123">在命令提示字元中，按 **Enter**鍵。</span><span class="sxs-lookup"><span data-stu-id="1a331-123">At the command prompt, press **Enter**.</span></span>
2. <span data-ttu-id="1a331-124">選取 [ **選項 1** ] 以使用完整的存取權限登入裝置。</span><span class="sxs-lookup"><span data-stu-id="1a331-124">Select **Option 1** to log on to the device with full access.</span></span>
3. <span data-ttu-id="1a331-125">若要安裝 Hotfix，請在命令提示字元中輸入：</span><span class="sxs-lookup"><span data-stu-id="1a331-125">To install the hotfix, at the command prompt, type:</span></span>
   
    `Start-HcsHotfix -Path <path to update file> -Credential <credentials in domain\username format>`
   
    <span data-ttu-id="1a331-126">在上述命令的共用路徑中使用 IP 而不是 DNS。</span><span class="sxs-lookup"><span data-stu-id="1a331-126">Use IP rather than DNS in share path in the above command.</span></span> <span data-ttu-id="1a331-127">只有當您要存取已驗證的共用位置時，才會用到認證參數。</span><span class="sxs-lookup"><span data-stu-id="1a331-127">The credential parameter is used only if you are accessing an authenticated share.</span></span>
   
    <span data-ttu-id="1a331-128">我們建議您使用認證參數來存取共用項目。</span><span class="sxs-lookup"><span data-stu-id="1a331-128">We recommend that you use the credential parameter to access shares.</span></span> <span data-ttu-id="1a331-129">即使是開放給「所有人」的共用項目，通常也不會開放給未經驗證的使用者。</span><span class="sxs-lookup"><span data-stu-id="1a331-129">Even shares that are open to “everyone” are typically not open to unauthenticated users.</span></span>
   
    <span data-ttu-id="1a331-130">下方顯示一項範例輸出。</span><span class="sxs-lookup"><span data-stu-id="1a331-130">A sample output is shown below.</span></span>
   
    ```
    Controller0>Start-HcsHotfix -Path \\10.100.100.100\share
    \hcsmdssoftwareupdate.exe -Credential contoso\John

    Confirm

    This operation starts the hotfix installation and could reboot one or
    both of the controllers. If the device is serving I/Os, these will not
    be disrupted. Are you sure you want to continue?
    [Y] Yes [N] No [?] Help (default is "Y"): Y
    ```
4. <span data-ttu-id="1a331-131">當系統提示您確認 Hotfix 安裝時，請輸入 **Y** 。</span><span class="sxs-lookup"><span data-stu-id="1a331-131">Type **Y** when prompted to confirm the hotfix installation.</span></span>
5. <span data-ttu-id="1a331-132">使用 `Get-HcsUpdateStatus` Cmdlet 來監視更新。</span><span class="sxs-lookup"><span data-stu-id="1a331-132">Monitor the update by using the `Get-HcsUpdateStatus` cmdlet.</span></span>
   
    <span data-ttu-id="1a331-133">下列範例輸出顯示更新進行中。</span><span class="sxs-lookup"><span data-stu-id="1a331-133">The following sample output shows the update in progress.</span></span> <span data-ttu-id="1a331-134">更新正在進行中時，`RunInprogress` 會是 `True`。</span><span class="sxs-lookup"><span data-stu-id="1a331-134">The `RunInprogress` will be `True` when the update is in progress.</span></span>
   
    ```
    Controller0>Get-HcsUpdateStatus
    RunInprogress       : True
    LastHotfixTimestamp : 12/21/2015 10:36:13 PM
    LastUpdateTimestamp : 12/21/2015 10:35:25 PM
    Controller0Events   :
    Controller1Events   :
    ```
   
     <span data-ttu-id="1a331-135">下列範例輸出指出更新已完成。</span><span class="sxs-lookup"><span data-stu-id="1a331-135">The following sample output indicates that the update is finished.</span></span> <span data-ttu-id="1a331-136">更新完成時，`RunInProgress` 將會是 `False`。</span><span class="sxs-lookup"><span data-stu-id="1a331-136">The `RunInProgress` will be `False` when the update has completed.</span></span>
   
    ```
    Controller1>Get-HcsUpdateStatus

    RunInprogress       : False
    LastHotfixTimestamp : 12/21/2015 10:59:13 PM
    LastUpdateTimestamp : 12/21/2015 10:35:25 PM
    Controller0Events   :
    Controller1Events   :
    ```
   
   > [!NOTE]
   > <span data-ttu-id="1a331-137">有時在更新進行期間，Cmdlet 會回報 `False`。</span><span class="sxs-lookup"><span data-stu-id="1a331-137">Occasionally, the cmdlet reports `False` when the update is still in progress.</span></span> <span data-ttu-id="1a331-138">若要確保此 Hotfix 已完成，請等待幾分鐘的時間、重新執行此命令並確認 `RunInProgress` 為 `False`。</span><span class="sxs-lookup"><span data-stu-id="1a331-138">To ensure that the hotfix is complete, wait for a few minutes, rerun this command and verify that the `RunInProgress` is `False`.</span></span> <span data-ttu-id="1a331-139">如果的確為 False 的話，則 Hotfix 已完成。</span><span class="sxs-lookup"><span data-stu-id="1a331-139">If it is, then the hotfix has completed.</span></span>

6. <span data-ttu-id="1a331-140">軟體更新完成之後，請重複步驟 3 至 5 來安裝及監視 SaaS 代理程式和 MDS 代理程式。</span><span class="sxs-lookup"><span data-stu-id="1a331-140">After the software update is complete, repeat steps 3-5 to install and monitor the SaaS agent and MDS agent .</span></span> <span data-ttu-id="1a331-141">請確保您是先安裝 `all-hcsmdssoftwareupdate_0b438ddf0d5b686aada2378b754fac8c7f2160e9.exe`，再安裝 `all-cismdsagentupdatebundle_f98e62f4d56c79e2a6644d027af7a2393a93827a.exe`。</span><span class="sxs-lookup"><span data-stu-id="1a331-141">Ensure that `all-hcsmdssoftwareupdate_0b438ddf0d5b686aada2378b754fac8c7f2160e9.exe` is installed before `all-cismdsagentupdatebundle_f98e62f4d56c79e2a6644d027af7a2393a93827a.exe`.</span></span>
7. <span data-ttu-id="1a331-142">驗證系統軟體版本。</span><span class="sxs-lookup"><span data-stu-id="1a331-142">Verify the system software versions.</span></span> <span data-ttu-id="1a331-143">輸入：</span><span class="sxs-lookup"><span data-stu-id="1a331-143">Type:</span></span>
   
    `Get-HcsSystem`
   
    <span data-ttu-id="1a331-144">您應該會看見下列版本：</span><span class="sxs-lookup"><span data-stu-id="1a331-144">You should see the following versions:</span></span>
   
   * <span data-ttu-id="1a331-145">HcsSoftwareVersion：6.3.9600.17673</span><span class="sxs-lookup"><span data-stu-id="1a331-145">HcsSoftwareVersion: 6.3.9600.17673</span></span>
   * <span data-ttu-id="1a331-146">CisAgentVersion：1.0.9150.0</span><span class="sxs-lookup"><span data-stu-id="1a331-146">CisAgentVersion: 1.0.9150.0</span></span>
   * <span data-ttu-id="1a331-147">MdsAgentVersion：30.0.4698.13</span><span class="sxs-lookup"><span data-stu-id="1a331-147">MdsAgentVersion: 30.0.4698.13</span></span>
     
     <span data-ttu-id="1a331-148">如果在套用更新後版本號碼並未變更，則表示此 Hotfix 未成功套用。</span><span class="sxs-lookup"><span data-stu-id="1a331-148">If the version numbers do not change after applying the update, it indicates that the hotfix has failed to apply.</span></span> <span data-ttu-id="1a331-149">若您看到這種情況，請連絡 [Microsoft 支援](../articles/storsimple/storsimple-contact-microsoft-support.md)以取得進一步的協助。</span><span class="sxs-lookup"><span data-stu-id="1a331-149">Should you see this, please contact [Microsoft Support](../articles/storsimple/storsimple-contact-microsoft-support.md) for further assistance.</span></span>
8. <span data-ttu-id="1a331-150">重複步驟 3-5 來安裝剩餘的一般模式 Hotfix。</span><span class="sxs-lookup"><span data-stu-id="1a331-150">Repeat steps 3-5 to install the remaining regular-mode hotfixes.</span></span>
   
   * <span data-ttu-id="1a331-151">LSI 驅動程式 - KB3121900</span><span class="sxs-lookup"><span data-stu-id="1a331-151">The LSI driver - KB3121900</span></span>
   * <span data-ttu-id="1a331-152">Storport 更新 - KB3080728</span><span class="sxs-lookup"><span data-stu-id="1a331-152">The Storport update - KB3080728</span></span>
   * <span data-ttu-id="1a331-153">Spaceport 更新 - KB3090322</span><span class="sxs-lookup"><span data-stu-id="1a331-153">The Spaceport update - KB3090322</span></span>

#### <a name="to-install-and-verify-maintenance-mode-hotfixes"></a><span data-ttu-id="1a331-154">安裝及驗證維護模式 Hotfix</span><span class="sxs-lookup"><span data-stu-id="1a331-154">To install and verify maintenance mode hotfixes</span></span>
<span data-ttu-id="1a331-155">請使用 KB3121899 來安裝磁碟韌體更新。</span><span class="sxs-lookup"><span data-stu-id="1a331-155">Use KB3121899 to install disk firmware updates.</span></span> <span data-ttu-id="1a331-156">這些是干擾性更新，且需要約 30 分鐘來完成。</span><span class="sxs-lookup"><span data-stu-id="1a331-156">These are disruptive updates and take around 30 minutes to complete.</span></span> <span data-ttu-id="1a331-157">您可以藉由連接至裝置序列主控台，以選擇在預計的維護視窗中安裝這些更新。</span><span class="sxs-lookup"><span data-stu-id="1a331-157">You can choose to install these in a planned maintenance window by connecting to the device serial console.</span></span>

<span data-ttu-id="1a331-158">請注意，如果您的磁碟韌體已是最新版本，便不需要安裝這些更新。</span><span class="sxs-lookup"><span data-stu-id="1a331-158">Note that if your disk firmware is already up-to-date, you won't need to install these updates.</span></span> <span data-ttu-id="1a331-159">從裝置序列主控台執行 `Get-HcsUpdateAvailability` Cmdlet，以檢查是否有可用的更新，以及更新是干擾性 (維護模式) 還是非干擾性 (一般模式) 更新。</span><span class="sxs-lookup"><span data-stu-id="1a331-159">Run the `Get-HcsUpdateAvailability` cmdlet from the device serial console to check if updates are available and whether the updates are disruptive (maintenance mode) or non-disruptive (regular mode) updates.</span></span>

<span data-ttu-id="1a331-160">若要安裝磁碟韌體更新，請依照下面的指示執行。</span><span class="sxs-lookup"><span data-stu-id="1a331-160">To install the disk firmware updates, follow the instructions below.</span></span>

1. <span data-ttu-id="1a331-161">使裝置處於維護模式。</span><span class="sxs-lookup"><span data-stu-id="1a331-161">Place the device in the Maintenance mode.</span></span> <span data-ttu-id="1a331-162">請注意，連線至處於維護模式的裝置時，您不應該使用 Windows PowerShell 遠端執行功能。</span><span class="sxs-lookup"><span data-stu-id="1a331-162">Note that you should not use Windows PowerShell remoting when connecting to a device in Maintenance mode.</span></span> <span data-ttu-id="1a331-163">透過裝置序列主控台連線時，請在裝置控制器上執行此 Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="1a331-163">Instead run this cmdlet on the device controller when connected through the device serial console.</span></span> <span data-ttu-id="1a331-164">輸入：</span><span class="sxs-lookup"><span data-stu-id="1a331-164">Type:</span></span>
   
    `Enter-HcsMaintenanceMode`
   
    <span data-ttu-id="1a331-165">下方顯示一項範例輸出。</span><span class="sxs-lookup"><span data-stu-id="1a331-165">A sample output is shown below.</span></span>
   
        Controller0>Enter-HcsMaintenanceMode
        Checking device state...
   
        In maintenance mode, your device will not service IOs and will be disconnected from the Microsoft Azure StorSimple Manager service. Entering maintenance mode will end the current session and reboot both controllers, which takes a few minutes to complete. Are you sure you want to enter maintenance mode?
        [Y] Yes [N] No (Default is "Y"): Y
   
        -----------------------MAINTENANCE MODE------------------------
        Microsoft Azure StorSimple Appliance Model 8100
        Name: Update2-8100-SHG0997879L76YD
        Software Version: 6.3.9600.17664
        Copyright (C) 2014 Microsoft Corporation. All rights reserved.
        You are connected to Controller0 - Passive
        ---------------------------------------------------------------
   
        Serial Console Menu
        [1] Log in with full access
        [2] Log into peer controller with full access
        [3] Connect with limited access
        [4] Change language
        Please enter your choice>
   
    <span data-ttu-id="1a331-166">接著，兩個控制器就會重新啟動以進入維護模式。</span><span class="sxs-lookup"><span data-stu-id="1a331-166">Both the controllers then restart into Maintenance mode.</span></span>
2. <span data-ttu-id="1a331-167">若要安裝磁碟韌體更新，請輸入：</span><span class="sxs-lookup"><span data-stu-id="1a331-167">To install the disk firmware update, type:</span></span>
   
    `Start-HcsHotfix -Path <path to update file> -Credential <credentials in domain\username format>`
   
    <span data-ttu-id="1a331-168">下方顯示一項範例輸出。</span><span class="sxs-lookup"><span data-stu-id="1a331-168">A sample output is shown below.</span></span>
   
        Controller1>Start-HcsHotfix -Path \\10.100.100.100\share\DiskFirmwarePackage.exe -Credential contoso\john
        Enter Password:
        WARNING: In maintenance mode, hotfixes should be installed on each controller sequentially. After the hotfix is installed on this controller, install it on the peer controller.
        Confirm
        This operation starts a hotfix installation and could reboot one or both of the controllers. By installing new updates you agree to, and accept any additional terms associated with, the new functionality listed in the release notes (https://go.microsoft.com/fwLink/?LinkID=613790). Are you sure you want to continue?
        [Y] Yes [N] No (Default is "Y"): Y
        WARNING: Installation is currently in progress. This operation can take several minutes to complete.
3. <span data-ttu-id="1a331-169">使用 `Get-HcsUpdateStatus` 命令監視安裝進度。</span><span class="sxs-lookup"><span data-stu-id="1a331-169">Monitor the install progress using `Get-HcsUpdateStatus` command.</span></span> <span data-ttu-id="1a331-170">當 `RunInProgress` 變成 `False` 時，代表更新完成。</span><span class="sxs-lookup"><span data-stu-id="1a331-170">The update is complete when the `RunInProgress` changes to `False`.</span></span>
4. <span data-ttu-id="1a331-171">安裝完成之後，維護模式 Hotfix 安裝所在的控制器將會重新開機。</span><span class="sxs-lookup"><span data-stu-id="1a331-171">After the installation is complete, the controller on which the maintenance mode hotfix was installed restarts.</span></span> <span data-ttu-id="1a331-172">以具有完整存取權的選項 1 登入，並驗證磁碟韌體版本。</span><span class="sxs-lookup"><span data-stu-id="1a331-172">Log in as option 1 with full access and verify the disk firmware version.</span></span> <span data-ttu-id="1a331-173">輸入：</span><span class="sxs-lookup"><span data-stu-id="1a331-173">Type:</span></span>
   
   `Get-HcsFirmwareVersion`
   
   <span data-ttu-id="1a331-174">預期的磁碟韌體版本為：</span><span class="sxs-lookup"><span data-stu-id="1a331-174">The expected disk firmware versions are:</span></span>
   
   `XMGG, XGEG, KZ50, F6C2, VR08`
   
   <span data-ttu-id="1a331-175">下方顯示一項範例輸出。</span><span class="sxs-lookup"><span data-stu-id="1a331-175">A sample output is shown below.</span></span>
   
       -----------------------MAINTENANCE MODE------------------------
       Microsoft Azure StorSimple Appliance Model 8100
       Name: Update2-8100-SHG0997879L76YD
       Software Version: 6.3.9600.17664
       Copyright (C) 2014 Microsoft Corporation. All rights reserved.
       You are connected to Controller1
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
   
    <span data-ttu-id="1a331-176">在第二個控制站上執行 `Get-HcsFirmwareVersion` 命令來驗證軟體版本已經更新。</span><span class="sxs-lookup"><span data-stu-id="1a331-176">Run the `Get-HcsFirmwareVersion` command on the second controller to verify that the software version has been updated.</span></span> <span data-ttu-id="1a331-177">然後您就可以結束維護模式。</span><span class="sxs-lookup"><span data-stu-id="1a331-177">You can then exit the maintenance mode.</span></span> <span data-ttu-id="1a331-178">若要這麼做，請針對每個裝置控制器輸入以下命令：</span><span class="sxs-lookup"><span data-stu-id="1a331-178">To do so, type the following command for each device controller:</span></span>
   
   `Exit-HcsMaintenanceMode`
5. <span data-ttu-id="1a331-179">當您離開維護模式時，控制器便會重新啟動。</span><span class="sxs-lookup"><span data-stu-id="1a331-179">The controllers restart when you exit Maintenance mode.</span></span> <span data-ttu-id="1a331-180">在磁碟韌體更新已成功套用且裝置已結束維護模式後，返回 Azure 傳統入口網站。</span><span class="sxs-lookup"><span data-stu-id="1a331-180">After the disk firmware updates are successfully applied and the device has exited maintenance mode, return to the Azure classic portal.</span></span> <span data-ttu-id="1a331-181">請注意，入口網站可能有 24 小時的時間不會顯示您已安裝維護模式更新。</span><span class="sxs-lookup"><span data-stu-id="1a331-181">Note that the portal might not show that you installed the Maintenance mode updates for 24 hours.</span></span>

