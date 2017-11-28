<!--author=alkohli last changed: 05/19/16-->

#### <a name="to-download-hotfixes"></a><span data-ttu-id="ce424-101">下載 Hofix</span><span class="sxs-lookup"><span data-stu-id="ce424-101">To download hotfixes</span></span>
<span data-ttu-id="ce424-102">請執行下列步驟，從 Microsoft Update Catalog 下載軟體更新。</span><span class="sxs-lookup"><span data-stu-id="ce424-102">Perform the following steps to download the software update from the Microsoft Update Catalog.</span></span>

1. <span data-ttu-id="ce424-103">啟動 Internet Explorer 並瀏覽至 [http://catalog.update.microsoft.com](http://catalog.update.microsoft.com)。</span><span class="sxs-lookup"><span data-stu-id="ce424-103">Start Internet Explorer and navigate to [http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span></span>
2. <span data-ttu-id="ce424-104">如果這是您在此電腦上第一次使用 Microsoft Update Catalog，請在系統提示您安裝 Microsoft Update Catalog 附加元件時，按一下 [安裝]  。</span><span class="sxs-lookup"><span data-stu-id="ce424-104">If this is your first time using the Microsoft Update Catalog on this computer, click **Install** when prompted to install the Microsoft Update Catalog add-on.</span></span>
    <span data-ttu-id="ce424-105">![安裝目錄](./media/storsimple-install-update2-hotfix/HCS_InstallCatalog-include.png)</span><span class="sxs-lookup"><span data-stu-id="ce424-105">![Install catalog](./media/storsimple-install-update2-hotfix/HCS_InstallCatalog-include.png)</span></span>
3. <span data-ttu-id="ce424-106">在 Microsoft Update Catalog 的搜尋方塊中，輸入您要下載的 Hotfix 知識庫 (KB) 編號 (例如 **3179904**)，然後按一下 [搜尋]。</span><span class="sxs-lookup"><span data-stu-id="ce424-106">In the search box of the Microsoft Update Catalog, enter the Knowledge Base (KB) number of the hotfix you want to download, for example **3179904**, and then click **Search**.</span></span>
   
    <span data-ttu-id="ce424-107">Hotfix 清單隨即出現，例如 **適用於 StorSimple 8000 系列的累積軟體套件組合更新 2.2**。</span><span class="sxs-lookup"><span data-stu-id="ce424-107">The hotfix listing appears, for example, **Cumulative Software Bundle Update 2.2 for StorSimple 8000 Series**.</span></span>
   
    ![搜尋目錄](./media/storsimple-install-update2-hotfix/HCS_SearchCatalog1-include.png)
4. <span data-ttu-id="ce424-109">按一下 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="ce424-109">Click **Add**.</span></span> <span data-ttu-id="ce424-110">更新便會新增到購物籃中。</span><span class="sxs-lookup"><span data-stu-id="ce424-110">The update is added to the basket.</span></span>
5. <span data-ttu-id="ce424-111">搜尋上表中所列的其他任何 Hotfix (**3103616**、**3146621**)，然後將每個都加入購物籃。</span><span class="sxs-lookup"><span data-stu-id="ce424-111">Search for any additional hotfixes listed in the table above (**3103616**, **3146621**), and add each to the basket.</span></span>
6. <span data-ttu-id="ce424-112">按一下 [ **檢視購物籃**]。</span><span class="sxs-lookup"><span data-stu-id="ce424-112">Click **View Basket**.</span></span>
7. <span data-ttu-id="ce424-113">按一下 [下載] 。</span><span class="sxs-lookup"><span data-stu-id="ce424-113">Click **Download**.</span></span> <span data-ttu-id="ce424-114">指定或「瀏覽」  至您想要儲存下載項目的本機位置。</span><span class="sxs-lookup"><span data-stu-id="ce424-114">Specify or **Browse** to a local location where you want the downloads to appear.</span></span> <span data-ttu-id="ce424-115">更新便會下載到指定的位置，並放在與更新名稱相同的子資料夾中。</span><span class="sxs-lookup"><span data-stu-id="ce424-115">The updates are downloaded to the specified location and placed in a sub-folder with the same name as the update.</span></span> <span data-ttu-id="ce424-116">資料夾也可以複製到裝置可連線的網路共用位置。</span><span class="sxs-lookup"><span data-stu-id="ce424-116">The folder can also be copied to a network share that is reachable from the device.</span></span>

> [!NOTE]
> <span data-ttu-id="ce424-117">Hotfix 必須可同時從兩個控制器存取，以偵測來自對等控制器的任何潛在錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="ce424-117">The hotfixes must be accessible from both controllers to detect any potential error messages from the peer controller.</span></span>
> 
> 

#### <a name="to-install-and-verify-regular-mode-hotfixes"></a><span data-ttu-id="ce424-118">安裝及驗證一般模式 Hotfix</span><span class="sxs-lookup"><span data-stu-id="ce424-118">To install and verify regular mode hotfixes</span></span>
<span data-ttu-id="ce424-119">執行下列步驟來安裝及驗證一般模式 Hotfix。</span><span class="sxs-lookup"><span data-stu-id="ce424-119">Perform the following steps to install and verify regular-mode hotfixes.</span></span> <span data-ttu-id="ce424-120">如果您已使用 Azure 入口網站安裝這些 Hotfix，請直接跳到 [安裝及驗證維護模式 Hotfix](#to-install-and-verify-maintenance-mode-hotfixes)。</span><span class="sxs-lookup"><span data-stu-id="ce424-120">If you already installed them using the Azure Portal, skip ahead to [install and verify maintenance mode hotfixes](#to-install-and-verify-maintenance-mode-hotfixes).</span></span>

1. <span data-ttu-id="ce424-121">若要安裝 Hotfix，請存取 StorSimple 裝置序列主控台上的 Windows PowerShell 介面。</span><span class="sxs-lookup"><span data-stu-id="ce424-121">To install the hotfixes, access the Windows PowerShell interface on your StorSimple device serial console.</span></span> <span data-ttu-id="ce424-122">請依照[使用 PuTTy 連接到序列主控台](../articles/storsimple/storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console)中的詳細指示執行作業。</span><span class="sxs-lookup"><span data-stu-id="ce424-122">Follow the detailed instructions in [Use PuTTy to connect to the serial console](../articles/storsimple/storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span></span> <span data-ttu-id="ce424-123">在命令提示字元中，按 **Enter**鍵。</span><span class="sxs-lookup"><span data-stu-id="ce424-123">At the command prompt, press **Enter**.</span></span>
2. <span data-ttu-id="ce424-124">選取 [ **選項 1** ] 以使用完整的存取權限登入裝置。</span><span class="sxs-lookup"><span data-stu-id="ce424-124">Select **Option 1** to log on to the device with full access.</span></span> <span data-ttu-id="ce424-125">建議您先在被動控制站上安裝此 Hotfix。</span><span class="sxs-lookup"><span data-stu-id="ce424-125">We recommend that you install the hotfix on the passive controller first.</span></span>
3. <span data-ttu-id="ce424-126">若要安裝 Hotfix，請在命令提示字元中輸入：</span><span class="sxs-lookup"><span data-stu-id="ce424-126">To install the hotfix, at the command prompt, type:</span></span>
   
    `Start-HcsHotfix -Path <path to update file> -Credential <credentials in domain\username format>`
   
    <span data-ttu-id="ce424-127">在上述命令的共用路徑中使用 IP 而不是 DNS。</span><span class="sxs-lookup"><span data-stu-id="ce424-127">Use IP rather than DNS in share path in the above command.</span></span> <span data-ttu-id="ce424-128">只有當您要存取已驗證的共用位置時，才會用到認證參數。</span><span class="sxs-lookup"><span data-stu-id="ce424-128">The credential parameter is used only if you are accessing an authenticated share.</span></span>
   
    <span data-ttu-id="ce424-129">我們建議您使用認證參數來存取共用項目。</span><span class="sxs-lookup"><span data-stu-id="ce424-129">We recommend that you use the credential parameter to access shares.</span></span> <span data-ttu-id="ce424-130">即使是開放給「所有人」的共用項目，通常也不會開放給未經驗證的使用者。</span><span class="sxs-lookup"><span data-stu-id="ce424-130">Even shares that are open to “everyone” are typically not open to unauthenticated users.</span></span>
   
    <span data-ttu-id="ce424-131">在系統提示時提供密碼。</span><span class="sxs-lookup"><span data-stu-id="ce424-131">Supply the password when prompted.</span></span>
   
    <span data-ttu-id="ce424-132">下方顯示一項範例輸出。</span><span class="sxs-lookup"><span data-stu-id="ce424-132">A sample output is shown below.</span></span>
   
    ```
    Controller0>Start-HcsHotfix -Path \\10.100.100.100\share
    \hcsmdssoftwareupdate.exe -Credential contoso\John

    Confirm

    This operation starts the hotfix installation and could reboot one or
    both of the controllers. If the device is serving I/Os, these will not
    be disrupted. Are you sure you want to continue?
    [Y] Yes [N] No [?] Help (default is "Y"): Y
    ```

4. <span data-ttu-id="ce424-133">當系統提示您確認 Hotfix 安裝時，請輸入 **Y** 。</span><span class="sxs-lookup"><span data-stu-id="ce424-133">Type **Y** when prompted to confirm the hotfix installation.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="ce424-134">若安裝 Update 2.2，請只安裝開頭為 'all-hcsmdssoftwareudpate' 的二進位檔。</span><span class="sxs-lookup"><span data-stu-id="ce424-134">If installing Update 2.2, only install the binary file prefaced with 'all-hcsmdssoftwareudpate'.</span></span> <span data-ttu-id="ce424-135">不要安裝開頭為 all-cismdsagentupdatebundle 的 Cis 和 MDS 代理程式更新。</span><span class="sxs-lookup"><span data-stu-id="ce424-135">Do not install the Cis and the MDS agent update prefaced with all-cismdsagentupdatebundle.</span></span> <span data-ttu-id="ce424-136">若沒有這麼做，可能會導致發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="ce424-136">Failure to do so will result in an error.</span></span> 

5. <span data-ttu-id="ce424-137">使用 `Get-HcsUpdateStatus` Cmdlet 來監視更新。</span><span class="sxs-lookup"><span data-stu-id="ce424-137">Monitor the update by using the `Get-HcsUpdateStatus` cmdlet.</span></span> <span data-ttu-id="ce424-138">會先在被動控制站上完成更新。</span><span class="sxs-lookup"><span data-stu-id="ce424-138">The update will first complete on the passive controller.</span></span> <span data-ttu-id="ce424-139">更新被動控制器之後，將進行容錯移轉，然後更新將套用到另一個控制器。</span><span class="sxs-lookup"><span data-stu-id="ce424-139">Once the passive controller is updated, there will be a failover and the update will then get applied on the other controller.</span></span> <span data-ttu-id="ce424-140">兩個控制器皆更新後，即更新完畢。</span><span class="sxs-lookup"><span data-stu-id="ce424-140">The update is complete when both the controllers are updated.</span></span>
   
    <span data-ttu-id="ce424-141">下列範例輸出顯示更新進行中。</span><span class="sxs-lookup"><span data-stu-id="ce424-141">The following sample output shows the update in progress.</span></span> <span data-ttu-id="ce424-142">更新正在進行中時，`RunInprogress` 會是 `True`。</span><span class="sxs-lookup"><span data-stu-id="ce424-142">The `RunInprogress` will be `True` when the update is in progress.</span></span>
   
    ```
    Controller0>Get-HcsUpdateStatus
    RunInprogress       : True
    LastHotfixTimestamp :
    LastUpdateTimestamp : 5/5/2016 2:04:02 AM
    Controller0Events   :
    Controller1Events   :
    ```
   
     <span data-ttu-id="ce424-143">下列範例輸出指出更新已完成。</span><span class="sxs-lookup"><span data-stu-id="ce424-143">The following sample output indicates that the update is finished.</span></span> <span data-ttu-id="ce424-144">更新完成時，`RunInProgress` 將會是 `False`。</span><span class="sxs-lookup"><span data-stu-id="ce424-144">The `RunInProgress` will be `False` when the update has completed.</span></span>
   
    ```
    Controller0>Get-HcsUpdateStatus
    RunInprogress       : False
    LastHotfixTimestamp : 5/17/2016 9:15:55 AM
    LastUpdateTimestamp : 5/17/2016 9:06:07 AM
    Controller0Events   :
    Controller1Events   :
    ```

    > [!NOTE]
    > <span data-ttu-id="ce424-145">有時在更新進行期間，Cmdlet 會回報 `False`。</span><span class="sxs-lookup"><span data-stu-id="ce424-145">Occasionally, the cmdlet reports `False` when the update is still in progress.</span></span> <span data-ttu-id="ce424-146">若要確保此 Hotfix 已完成，請等待幾分鐘的時間、重新執行此命令並確認 `RunInProgress` 為 `False`。</span><span class="sxs-lookup"><span data-stu-id="ce424-146">To ensure that the hotfix is complete, wait for a few minutes, rerun this command and verify that the `RunInProgress` is `False`.</span></span> <span data-ttu-id="ce424-147">如果的確為 False 的話，則 Hotfix 已完成。</span><span class="sxs-lookup"><span data-stu-id="ce424-147">If it is, then the hotfix has completed.</span></span>

1. <span data-ttu-id="ce424-148">軟體更新完成後，請確認系統軟體版本。</span><span class="sxs-lookup"><span data-stu-id="ce424-148">After the software update is complete, verify the system software versions.</span></span> <span data-ttu-id="ce424-149">輸入：</span><span class="sxs-lookup"><span data-stu-id="ce424-149">Type:</span></span>
   
    `Get-HcsSystem`
   
    <span data-ttu-id="ce424-150">您應該會看見下列版本：</span><span class="sxs-lookup"><span data-stu-id="ce424-150">You should see the following versions:</span></span>
   
   * `HcsSoftwareVersion: 6.3.9600.17708`
   * `CisAgentVersion: 1.0.9299.0`
   * `MdsAgentVersion: 30.0.4698.16` 
     
     <span data-ttu-id="ce424-151">如果在套用更新後版本號碼並未變更，則表示此 Hotfix 未成功套用。</span><span class="sxs-lookup"><span data-stu-id="ce424-151">If the version numbers do not change after applying the update, it indicates that the hotfix has failed to apply.</span></span> <span data-ttu-id="ce424-152">若您看到這種情況，請連絡 [Microsoft 支援](../articles/storsimple/storsimple-contact-microsoft-support.md)以取得進一步的協助。</span><span class="sxs-lookup"><span data-stu-id="ce424-152">Should you see this, please contact [Microsoft Support](../articles/storsimple/storsimple-contact-microsoft-support.md) for further assistance.</span></span>
     
     > [!IMPORTANT]
     > <span data-ttu-id="ce424-153">您必須先透過 `Restart-HcsController` Cmdlet 重新啟動主動控制器，再套用其餘的更新。</span><span class="sxs-lookup"><span data-stu-id="ce424-153">You must restart the active controller via the `Restart-HcsController` cmdlet before applying the remaining updates.</span></span> 
     > 
     > 
2. <span data-ttu-id="ce424-154">重複步驟 3-5 來安裝剩餘的一般模式 Hotfix。</span><span class="sxs-lookup"><span data-stu-id="ce424-154">Repeat steps 3-5 to install the remaining regular-mode hotfixes.</span></span>
   
   * <span data-ttu-id="ce424-155">iSCSI 更新 KB3146621</span><span class="sxs-lookup"><span data-stu-id="ce424-155">The iSCSI update KB3146621</span></span>
   * <span data-ttu-id="ce424-156">WMI 更新 KB3103616</span><span class="sxs-lookup"><span data-stu-id="ce424-156">The WMI update KB3103616</span></span>
3. <span data-ttu-id="ce424-157">如果您要從 Update 2 進行更新，請略過此步驟。</span><span class="sxs-lookup"><span data-stu-id="ce424-157">Skip this step if you are updating from Update 2.</span></span> <span data-ttu-id="ce424-158">如果您要從 Update 2 之前的版本進行更新，則也必須下載︰</span><span class="sxs-lookup"><span data-stu-id="ce424-158">If you are updating from a version prior to Update 2, you will also need to download:</span></span>

    - <span data-ttu-id="ce424-159">LSI 驅動程式 KB3121900</span><span class="sxs-lookup"><span data-stu-id="ce424-159">The LSI driver KB3121900</span></span>

    - <span data-ttu-id="ce424-160">Spaceport 更新 KB3090322</span><span class="sxs-lookup"><span data-stu-id="ce424-160">The Spaceport update KB3090322</span></span>

    - <span data-ttu-id="ce424-161">Storport 更新 KB3080728</span><span class="sxs-lookup"><span data-stu-id="ce424-161">The Storport update KB3080728</span></span>

#### <a name="to-install-and-verify-maintenance-mode-hotfixes"></a><span data-ttu-id="ce424-162">安裝及驗證維護模式 Hotfix</span><span class="sxs-lookup"><span data-stu-id="ce424-162">To install and verify maintenance mode hotfixes</span></span>
<span data-ttu-id="ce424-163">請使用 KB3121899 來安裝磁碟韌體更新。</span><span class="sxs-lookup"><span data-stu-id="ce424-163">Use KB3121899 to install disk firmware updates.</span></span> <span data-ttu-id="ce424-164">這些是干擾性更新，且需要約 30 分鐘來完成。</span><span class="sxs-lookup"><span data-stu-id="ce424-164">These are disruptive updates and take around 30 minutes to complete.</span></span> <span data-ttu-id="ce424-165">您可以藉由連接至裝置序列主控台，以選擇在預計的維護視窗中安裝這些更新。</span><span class="sxs-lookup"><span data-stu-id="ce424-165">You can choose to install these in a planned maintenance window by connecting to the device serial console.</span></span>

<span data-ttu-id="ce424-166">請注意，如果您的磁碟韌體已是最新版本，便不需要安裝這些更新。</span><span class="sxs-lookup"><span data-stu-id="ce424-166">Note that if your disk firmware is already up-to-date, you won't need to install these updates.</span></span> <span data-ttu-id="ce424-167">從裝置序列主控台執行 `Get-HcsUpdateAvailability` Cmdlet，以檢查是否有可用的更新，以及更新是干擾性 (維護模式) 還是非干擾性 (一般模式) 更新。</span><span class="sxs-lookup"><span data-stu-id="ce424-167">Run the `Get-HcsUpdateAvailability` cmdlet from the device serial console to check if updates are available and whether the updates are disruptive (maintenance mode) or non-disruptive (regular mode) updates.</span></span>

<span data-ttu-id="ce424-168">若要安裝磁碟韌體更新，請依照下面的指示執行。</span><span class="sxs-lookup"><span data-stu-id="ce424-168">To install the disk firmware updates, follow the instructions below.</span></span>

1. <span data-ttu-id="ce424-169">使裝置處於維護模式。</span><span class="sxs-lookup"><span data-stu-id="ce424-169">Place the device in the Maintenance mode.</span></span> <span data-ttu-id="ce424-170">請注意，連線至處於維護模式的裝置時，您不應該使用 Windows PowerShell 遠端執行功能。</span><span class="sxs-lookup"><span data-stu-id="ce424-170">Note that you should not use Windows PowerShell remoting when connecting to a device in Maintenance mode.</span></span> <span data-ttu-id="ce424-171">透過裝置序列主控台連線時，請在裝置控制器上執行此 Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="ce424-171">Instead run this cmdlet on the device controller when connected through the device serial console.</span></span> <span data-ttu-id="ce424-172">輸入：</span><span class="sxs-lookup"><span data-stu-id="ce424-172">Type:</span></span>
   
    `Enter-HcsMaintenanceMode`
   
    <span data-ttu-id="ce424-173">下方顯示一項範例輸出。</span><span class="sxs-lookup"><span data-stu-id="ce424-173">A sample output is shown below.</span></span>
   
        Controller0>Enter-HcsMaintenanceMode
        Checking device state...
   
        In maintenance mode, your device will not service IOs and will be disconnected from the Microsoft Azure StorSimple Manager service. Entering maintenance mode will end the current session and reboot both controllers, which takes a few minutes to complete. Are you sure you want to enter maintenance mode?
        [Y] Yes [N] No (Default is "Y"): Y
   
        -----------------------MAINTENANCE MODE------------------------
        Microsoft Azure StorSimple Appliance Model 8100
        Name: Update2-8100-SHG0997879L76673
        Copyright (C) 2014 Microsoft Corporation. All rights reserved.
        You are connected to Controller0 - Passive
        ---------------------------------------------------------------
   
        Serial Console Menu
        [1] Log in with full access
        [2] Log into peer controller with full access
        [3] Connect with limited access
        [4] Change language
        Please enter your choice>
   
    <span data-ttu-id="ce424-174">接著，兩個控制器就會重新啟動以進入維護模式。</span><span class="sxs-lookup"><span data-stu-id="ce424-174">Both the controllers then restart into Maintenance mode.</span></span>
2. <span data-ttu-id="ce424-175">若要安裝磁碟韌體更新，請輸入：</span><span class="sxs-lookup"><span data-stu-id="ce424-175">To install the disk firmware update, type:</span></span>
   
    `Start-HcsHotfix -Path <path to update file> -Credential <credentials in domain\username format>`
   
    <span data-ttu-id="ce424-176">下方顯示一項範例輸出。</span><span class="sxs-lookup"><span data-stu-id="ce424-176">A sample output is shown below.</span></span>
   
        Controller1>Start-HcsHotfix -Path \\10.100.100.100\share\DiskFirmwarePackage.exe -Credential contoso\john
        Enter Password:
        WARNING: In maintenance mode, hotfixes should be installed on each controller sequentially. After the hotfix is installed on this controller, install it on the peer controller.
        Confirm
        This operation starts a hotfix installation and could reboot one or both of the controllers. By installing new updates you agree to, and accept any additional terms associated with, the new functionality listed in the release notes (https://go.microsoft.com/fwLink/?LinkID=613790). Are you sure you want to continue?
        [Y] Yes [N] No (Default is "Y"): Y
        WARNING: Installation is currently in progress. This operation can take several minutes to complete.
3. <span data-ttu-id="ce424-177">使用 `Get-HcsUpdateStatus` 命令監視安裝進度。</span><span class="sxs-lookup"><span data-stu-id="ce424-177">Monitor the install progress using `Get-HcsUpdateStatus` command.</span></span> <span data-ttu-id="ce424-178">當 `RunInProgress` 變成 `False` 時，代表更新完成。</span><span class="sxs-lookup"><span data-stu-id="ce424-178">The update is complete when the `RunInProgress` changes to `False`.</span></span>
4. <span data-ttu-id="ce424-179">安裝完成之後，維護模式 Hotfix 安裝所在的控制器將會重新開機。</span><span class="sxs-lookup"><span data-stu-id="ce424-179">After the installation is complete, the controller on which the maintenance mode hotfix was installed restarts.</span></span> <span data-ttu-id="ce424-180">以具有完整存取權的選項 1 登入，並驗證磁碟韌體版本。</span><span class="sxs-lookup"><span data-stu-id="ce424-180">Log in as option 1 with full access and verify the disk firmware version.</span></span> <span data-ttu-id="ce424-181">輸入：</span><span class="sxs-lookup"><span data-stu-id="ce424-181">Type:</span></span>
   
   `Get-HcsFirmwareVersion`
   
   <span data-ttu-id="ce424-182">預期的磁碟韌體版本為：</span><span class="sxs-lookup"><span data-stu-id="ce424-182">The expected disk firmware versions are:</span></span>
   
   `XMGG, XGEG, KZ50, F6C2, VR08`
   
   <span data-ttu-id="ce424-183">下方顯示一項範例輸出。</span><span class="sxs-lookup"><span data-stu-id="ce424-183">A sample output is shown below.</span></span>
   
       -----------------------MAINTENANCE MODE------------------------
       Microsoft Azure StorSimple Appliance Model 8100
       Name: Update2-8100-SHG0997879L76YD
       Software Version: 6.3.9600.17705
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
   
    <span data-ttu-id="ce424-184">在第二個控制站上執行 `Get-HcsFirmwareVersion` 命令來驗證軟體版本已經更新。</span><span class="sxs-lookup"><span data-stu-id="ce424-184">Run the `Get-HcsFirmwareVersion` command on the second controller to verify that the software version has been updated.</span></span> <span data-ttu-id="ce424-185">然後您就可以結束維護模式。</span><span class="sxs-lookup"><span data-stu-id="ce424-185">You can then exit the maintenance mode.</span></span> <span data-ttu-id="ce424-186">若要這麼做，請針對每個裝置控制器輸入以下命令：</span><span class="sxs-lookup"><span data-stu-id="ce424-186">To do so, type the following command for each device controller:</span></span>
   
   `Exit-HcsMaintenanceMode`
5. <span data-ttu-id="ce424-187">當您離開維護模式時，控制器便會重新啟動。</span><span class="sxs-lookup"><span data-stu-id="ce424-187">The controllers restart when you exit Maintenance mode.</span></span> <span data-ttu-id="ce424-188">在磁碟韌體更新已成功套用且裝置已結束維護模式後，返回 Azure 傳統入口網站。</span><span class="sxs-lookup"><span data-stu-id="ce424-188">After the disk firmware updates are successfully applied and the device has exited maintenance mode, return to the Azure classic portal.</span></span> <span data-ttu-id="ce424-189">請注意，入口網站可能有 24 小時的時間不會顯示您已安裝維護模式更新。</span><span class="sxs-lookup"><span data-stu-id="ce424-189">Note that the portal might not show that you installed the Maintenance mode updates for 24 hours.</span></span>

