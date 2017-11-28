<!--author=alkohli last changed: 02/10/17-->

#### <a name="to-download-hotfixes"></a><span data-ttu-id="0775a-101">下載 Hofix</span><span class="sxs-lookup"><span data-stu-id="0775a-101">To download hotfixes</span></span>

<span data-ttu-id="0775a-102">請執行下列步驟，從 Microsoft Update Catalog 下載軟體更新。</span><span class="sxs-lookup"><span data-stu-id="0775a-102">Perform the following steps to download the software update from the Microsoft Update Catalog.</span></span>

1. <span data-ttu-id="0775a-103">啟動 Internet Explorer 並瀏覽至 [http://catalog.update.microsoft.com](http://catalog.update.microsoft.com)。</span><span class="sxs-lookup"><span data-stu-id="0775a-103">Start Internet Explorer and navigate to [http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span></span>
2. <span data-ttu-id="0775a-104">如果這是您第一次在此電腦上使用 Microsoft Update Catalog，請在系統提示您安裝 Microsoft Update Catalog 附加元件時，按一下 [安裝]  。</span><span class="sxs-lookup"><span data-stu-id="0775a-104">If this is your first time using the Microsoft Update Catalog on this computer, click **Install** when prompted to install the Microsoft Update Catalog add-on.</span></span>

    ![安裝目錄](./media/storsimple-install-update2-hotfix/HCS_InstallCatalog-include.png)

3. <span data-ttu-id="0775a-106">在 Microsoft Update Catalog 的搜尋方塊中，輸入您要下載的 Hotfix 知識庫 (KB) 編號 (例如 **4011839**)，然後按一下 [搜尋]。</span><span class="sxs-lookup"><span data-stu-id="0775a-106">In the search box of the Microsoft Update Catalog, enter the Knowledge Base (KB) number of the hotfix you want to download, for example **4011839**, and then click **Search**.</span></span>
   
    <span data-ttu-id="0775a-107">Hotfix 清單隨即出現，例如**適用於 StorSimple 8000 系列的累積軟體套件組合更新 4.0**。</span><span class="sxs-lookup"><span data-stu-id="0775a-107">The hotfix listing appears, for example, **Cumulative Software Bundle Update 4.0 for StorSimple 8000 Series**.</span></span>
   
    ![搜尋目錄](./media/storsimple-install-update2-hotfix/HCS_SearchCatalog1-include.png)

4. <span data-ttu-id="0775a-109">按一下 [下載] 。</span><span class="sxs-lookup"><span data-stu-id="0775a-109">Click **Download**.</span></span> <span data-ttu-id="0775a-110">指定或「瀏覽」  至您想要儲存下載項目的本機位置。</span><span class="sxs-lookup"><span data-stu-id="0775a-110">Specify or **Browse** to a local location where you want the downloads to appear.</span></span> <span data-ttu-id="0775a-111">按一下要下載到指定位置和資料夾的檔案。</span><span class="sxs-lookup"><span data-stu-id="0775a-111">Click the files to download to the specified location and folder.</span></span> <span data-ttu-id="0775a-112">資料夾也可以複製到裝置可連線的網路共用位置。</span><span class="sxs-lookup"><span data-stu-id="0775a-112">The folder can also be copied to a network share that is reachable from the device.</span></span>
5. <span data-ttu-id="0775a-113">搜尋上表所列的任何其他 Hotfix (**4011841**)，並將對應檔案下載到上表所列的特定資料夾。</span><span class="sxs-lookup"><span data-stu-id="0775a-113">Search for any additional hotfixes listed in the table above (**4011841**), and download the corresponding files to the specific folders as listed in the preceding table.</span></span>

> [!NOTE]
> <span data-ttu-id="0775a-114">Hotfix 必須可同時從兩個控制器存取，以偵測來自對等控制器的任何潛在錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="0775a-114">The hotfixes must be accessible from both controllers to detect any potential error messages from the peer controller.</span></span>
>
> <span data-ttu-id="0775a-115">Hotfix 必須複製到 3 個不同的資料夾。</span><span class="sxs-lookup"><span data-stu-id="0775a-115">The hotfixes must be copied in 3 separate folders.</span></span> <span data-ttu-id="0775a-116">例如，裝置軟體/Cis/MDS 代理程式更新可以複製到 _FirstOrderUpdate_ 資料夾，其他所有非干擾性更新應該複製到 _SecondOrderUpdate_ 資料夾，而維護模式更新則會複製到 _ThirdOrderUpdate_ 資料夾。</span><span class="sxs-lookup"><span data-stu-id="0775a-116">For example, the device software/Cis/MDS agent update can be copied in _FirstOrderUpdate_ folder, all the other non-disruptive updates could be copied in the _SecondOrderUpdate_ folder, and maintenance mode updates copied in _ThirdOrderUpdate_ folder.</span></span>

#### <a name="to-install-and-verify-regular-mode-hotfixes"></a><span data-ttu-id="0775a-117">安裝及驗證一般模式 Hotfix</span><span class="sxs-lookup"><span data-stu-id="0775a-117">To install and verify regular mode hotfixes</span></span>

<span data-ttu-id="0775a-118">執行下列步驟來安裝及驗證一般模式 Hotfix。</span><span class="sxs-lookup"><span data-stu-id="0775a-118">Perform the following steps to install and verify regular-mode hotfixes.</span></span> <span data-ttu-id="0775a-119">如果您已使用 Azure 傳統入口網站安裝這些 Hotfix，請直接跳到[安裝及驗證維護模式 Hotfix](#to-install-and-verify-maintenance-mode-hotfixes)。</span><span class="sxs-lookup"><span data-stu-id="0775a-119">If you already installed them using the Azure classic portal, skip ahead to [install and verify maintenance mode hotfixes](#to-install-and-verify-maintenance-mode-hotfixes).</span></span>

1. <span data-ttu-id="0775a-120">若要安裝 Hotfix，請存取 StorSimple 裝置序列主控台上的 Windows PowerShell 介面。</span><span class="sxs-lookup"><span data-stu-id="0775a-120">To install the hotfixes, access the Windows PowerShell interface on your StorSimple device serial console.</span></span> <span data-ttu-id="0775a-121">請依照[使用 PuTTy 連接到序列主控台](../articles/storsimple/storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console)中的詳細指示執行作業。</span><span class="sxs-lookup"><span data-stu-id="0775a-121">Follow the detailed instructions in [Use PuTTy to connect to the serial console](../articles/storsimple/storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span></span> <span data-ttu-id="0775a-122">在命令提示字元中，按 **Enter**鍵。</span><span class="sxs-lookup"><span data-stu-id="0775a-122">At the command prompt, press **Enter**.</span></span>
2. <span data-ttu-id="0775a-123">選取 [ **選項 1** ] 以使用完整的存取權限登入裝置。</span><span class="sxs-lookup"><span data-stu-id="0775a-123">Select **Option 1** to log on to the device with full access.</span></span> <span data-ttu-id="0775a-124">建議您先在被動控制站上安裝此 Hotfix。</span><span class="sxs-lookup"><span data-stu-id="0775a-124">We recommend that you install the hotfix on the passive controller first.</span></span>
3. <span data-ttu-id="0775a-125">若要安裝 Hotfix，請在命令提示字元中輸入：</span><span class="sxs-lookup"><span data-stu-id="0775a-125">To install the hotfix, at the command prompt, type:</span></span>
   
    `Start-HcsHotfix -Path <path to update file> -Credential <credentials in domain\username format>`
   
    <span data-ttu-id="0775a-126">在上述命令的共用路徑中使用 IP 而不是 DNS。</span><span class="sxs-lookup"><span data-stu-id="0775a-126">Use IP rather than DNS in share path in the above command.</span></span> <span data-ttu-id="0775a-127">只有當您要存取已驗證的共用位置時，才會用到認證參數。</span><span class="sxs-lookup"><span data-stu-id="0775a-127">The credential parameter is used only if you are accessing an authenticated share.</span></span>
   
    <span data-ttu-id="0775a-128">我們建議您使用認證參數來存取共用項目。</span><span class="sxs-lookup"><span data-stu-id="0775a-128">We recommend that you use the credential parameter to access shares.</span></span> <span data-ttu-id="0775a-129">即使是開放給「所有人」的共用項目，通常也不會開放給未經驗證的使用者。</span><span class="sxs-lookup"><span data-stu-id="0775a-129">Even shares that are open to “everyone” are typically not open to unauthenticated users.</span></span>
   
    <span data-ttu-id="0775a-130">在系統提示時提供密碼。</span><span class="sxs-lookup"><span data-stu-id="0775a-130">Supply the password when prompted.</span></span>
   
    <span data-ttu-id="0775a-131">下面會顯示安裝第一級更新的範例輸出。</span><span class="sxs-lookup"><span data-stu-id="0775a-131">A sample output for installing the first order updates is shown below.</span></span> <span data-ttu-id="0775a-132">對於第一級更新，您需要指向特定檔案。</span><span class="sxs-lookup"><span data-stu-id="0775a-132">For the first order update, you need to point to the specific file.</span></span>
   
        ````
        Controller0>Start-HcsHotfix -Path \\10.100.100.100\share
        \FirstOrderUpdate\HcsSoftwareUpdate.exe -Credential contoso\John
   
        Confirm
   
        This operation starts the hotfix installation and could reboot one or
        both of the controllers. If the device is serving I/Os, these will not
        be disrupted. Are you sure you want to continue?
        [Y] Yes [N] No [?] Help (default is "Y"): Y
   
        ````
4. <span data-ttu-id="0775a-133">當系統提示您確認 Hotfix 安裝時，請輸入 **Y** 。</span><span class="sxs-lookup"><span data-stu-id="0775a-133">Type **Y** when prompted to confirm the hotfix installation.</span></span>
5. <span data-ttu-id="0775a-134">使用 `Get-HcsUpdateStatus` Cmdlet 來監視更新。</span><span class="sxs-lookup"><span data-stu-id="0775a-134">Monitor the update by using the `Get-HcsUpdateStatus` cmdlet.</span></span> <span data-ttu-id="0775a-135">會先在被動控制站上完成更新。</span><span class="sxs-lookup"><span data-stu-id="0775a-135">The update will first complete on the passive controller.</span></span> <span data-ttu-id="0775a-136">更新被動控制器之後，將進行容錯移轉，然後更新將套用到另一個控制器。</span><span class="sxs-lookup"><span data-stu-id="0775a-136">Once the passive controller is updated, there will be a failover and the update will then get applied on the other controller.</span></span> <span data-ttu-id="0775a-137">兩個控制器皆更新後，即更新完畢。</span><span class="sxs-lookup"><span data-stu-id="0775a-137">The update is complete when both the controllers are updated.</span></span>
   
    <span data-ttu-id="0775a-138">下列範例輸出顯示更新進行中。</span><span class="sxs-lookup"><span data-stu-id="0775a-138">The following sample output shows the update in progress.</span></span> <span data-ttu-id="0775a-139">更新正在進行中時，`RunInprogress` 會是 `True`。</span><span class="sxs-lookup"><span data-stu-id="0775a-139">The `RunInprogress` will be `True` when the update is in progress.</span></span>

    ```
    Controller0>Get-HcsUpdateStatus
    RunInprogress       : True
    LastHotfixTimestamp :
    LastUpdateTimestamp : 02/03/2017 2:04:02 AM
    Controller0Events   :
    Controller1Events   :
    ```
   
     <span data-ttu-id="0775a-140">下列範例輸出指出更新已完成。</span><span class="sxs-lookup"><span data-stu-id="0775a-140">The following sample output indicates that the update is finished.</span></span> <span data-ttu-id="0775a-141">更新完成時，`RunInProgress` 將會是 `False`。</span><span class="sxs-lookup"><span data-stu-id="0775a-141">The `RunInProgress` will be `False` when the update has completed.</span></span>
   
    ```
    Controller0>Get-HcsUpdateStatus
    RunInprogress       : False
    LastHotfixTimestamp : 02/03/2017 9:15:55 AM
    LastUpdateTimestamp : 02/03/2017 9:06:07 AM
    Controller0Events   :
    Controller1Events   :
    ```

    > [!NOTE]
    > <span data-ttu-id="0775a-142">有時在更新進行期間，Cmdlet 會回報 `False`。</span><span class="sxs-lookup"><span data-stu-id="0775a-142">Occasionally, the cmdlet reports `False` when the update is still in progress.</span></span> <span data-ttu-id="0775a-143">若要確保此 Hotfix 已完成，請等待幾分鐘的時間、重新執行此命令並確認 `RunInProgress` 為 `False`。</span><span class="sxs-lookup"><span data-stu-id="0775a-143">To ensure that the hotfix is complete, wait for a few minutes, rerun this command and verify that the `RunInProgress` is `False`.</span></span> <span data-ttu-id="0775a-144">如果的確為 False 的話，則 Hotfix 已完成。</span><span class="sxs-lookup"><span data-stu-id="0775a-144">If it is, then the hotfix has completed.</span></span>

6. <span data-ttu-id="0775a-145">軟體更新完成後，請確認系統軟體版本。</span><span class="sxs-lookup"><span data-stu-id="0775a-145">After the software update is complete, verify the system software versions.</span></span> <span data-ttu-id="0775a-146">輸入：</span><span class="sxs-lookup"><span data-stu-id="0775a-146">Type:</span></span>
   
    `Get-HcsSystem`
   
    <span data-ttu-id="0775a-147">您應該會看見下列版本：</span><span class="sxs-lookup"><span data-stu-id="0775a-147">You should see the following versions:</span></span>
   
   * `FriendlySoftwareVersion: StorSimple 8000 Series Update 4.0`
   *  `HcsSoftwareVersion: 6.3.9600.17820`
   
    <span data-ttu-id="0775a-148">如果在套用更新後版本號碼並未變更，則表示此 Hotfix 未成功套用。</span><span class="sxs-lookup"><span data-stu-id="0775a-148">If the version number does not change after applying the update, it indicates that the hotfix has failed to apply.</span></span> <span data-ttu-id="0775a-149">若您看到這種情況，請連絡 [Microsoft 支援](../articles/storsimple/storsimple-contact-microsoft-support.md)以取得進一步的協助。</span><span class="sxs-lookup"><span data-stu-id="0775a-149">Should you see this, please contact [Microsoft Support](../articles/storsimple/storsimple-contact-microsoft-support.md) for further assistance.</span></span>
     
    > [!IMPORTANT]
    > <span data-ttu-id="0775a-150">您必須先透過 `Restart-HcsController` Cmdlet 重新啟動主動控制器，再套用下一個更新。</span><span class="sxs-lookup"><span data-stu-id="0775a-150">You must restart the active controller via the `Restart-HcsController` cmdlet before applying the next update.</span></span>
     
7. <span data-ttu-id="0775a-151">重複步驟 3 至 5，以安裝下載到 _FirstOrderUpdate_ 資料夾的 Cis/MDS 代理程式。</span><span class="sxs-lookup"><span data-stu-id="0775a-151">Repeat steps 3-5 to install the Cis/MDS agent downloaded to your _FirstOrderUpdate_ folder.</span></span> 
8. <span data-ttu-id="0775a-152">重複步驟 3-5 來安裝第二級更新。</span><span class="sxs-lookup"><span data-stu-id="0775a-152">Repeat steps 3-5 to install the second order updates.</span></span> <span data-ttu-id="0775a-153">**對於第二級更新，只要執行 `Start-HcsHotfix cmdlet` 並指向第二級更新所在的資料夾，即可安裝多個更新。此 Cmdlet 會執行資料夾中所有可用的更新。**</span><span class="sxs-lookup"><span data-stu-id="0775a-153">**For second order updates, multiple updates can be installed by just running the `Start-HcsHotfix cmdlet` and pointing to the folder where second order updates are located. The cmdlet will execute all the updates available in the folder.**</span></span> <span data-ttu-id="0775a-154">如果有已安裝的更新，更新邏輯會偵測到，而不套用該更新。</span><span class="sxs-lookup"><span data-stu-id="0775a-154">If an update is already installed, the update logic will detect that and not apply that update.</span></span> 

<span data-ttu-id="0775a-155">安裝所有 Hotfix 之後，請使用 `Get-HcsSystem` Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="0775a-155">After all the hotfixes are installed, use the `Get-HcsSystem` cmdlet.</span></span> <span data-ttu-id="0775a-156">版本應該是︰</span><span class="sxs-lookup"><span data-stu-id="0775a-156">The versions should be:</span></span>

   * `CisAgentVersion:  1.0.9441.0`
   * `MdsAgentVersion: 35.2.2.0`
   * `Lsisas2Version: 2.0.78.00`


#### <a name="to-install-and-verify-maintenance-mode-hotfixes"></a><span data-ttu-id="0775a-157">安裝及驗證維護模式 Hotfix</span><span class="sxs-lookup"><span data-stu-id="0775a-157">To install and verify maintenance mode hotfixes</span></span>
<span data-ttu-id="0775a-158">請使用 KB4011837 來安裝磁碟韌體更新。</span><span class="sxs-lookup"><span data-stu-id="0775a-158">Use KB4011837 to install disk firmware updates.</span></span> <span data-ttu-id="0775a-159">這些是干擾性更新，且需要約 30 分鐘來完成。</span><span class="sxs-lookup"><span data-stu-id="0775a-159">These are disruptive updates and take around 30 minutes to complete.</span></span> <span data-ttu-id="0775a-160">您可以藉由連接至裝置序列主控台，以選擇在預計的維護視窗中安裝這些更新。</span><span class="sxs-lookup"><span data-stu-id="0775a-160">You can choose to install these in a planned maintenance window by connecting to the device serial console.</span></span>

<span data-ttu-id="0775a-161">請注意，如果您的磁碟韌體已是最新版本，便不需要安裝這些更新。</span><span class="sxs-lookup"><span data-stu-id="0775a-161">Note that if your disk firmware is already up-to-date, you won't need to install these updates.</span></span> <span data-ttu-id="0775a-162">從裝置序列主控台執行 `Get-HcsUpdateAvailability` Cmdlet，以檢查是否有可用的更新，以及更新是干擾性 (維護模式) 還是非干擾性 (一般模式) 更新。</span><span class="sxs-lookup"><span data-stu-id="0775a-162">Run the `Get-HcsUpdateAvailability` cmdlet from the device serial console to check if updates are available and whether the updates are disruptive (maintenance mode) or non-disruptive (regular mode) updates.</span></span>

<span data-ttu-id="0775a-163">若要安裝磁碟韌體更新，請依照下面的指示執行。</span><span class="sxs-lookup"><span data-stu-id="0775a-163">To install the disk firmware updates, follow the instructions below.</span></span>

1. <span data-ttu-id="0775a-164">使裝置處於維護模式。</span><span class="sxs-lookup"><span data-stu-id="0775a-164">Place the device in the maintenance mode.</span></span> <span data-ttu-id="0775a-165">**請注意，連線至處於維護模式的裝置時，您不應該使用 Windows PowerShell 遠端執行功能。透過裝置序列主控台連線時，請在裝置控制器上執行此 Cmdlet。**</span><span class="sxs-lookup"><span data-stu-id="0775a-165">**Note that you should not use Windows PowerShell remoting when connecting to a device in maintenance mode. Instead run this cmdlet on the device controller when connected through the device serial console.**</span></span> <span data-ttu-id="0775a-166">輸入：</span><span class="sxs-lookup"><span data-stu-id="0775a-166">Type:</span></span>
   
    `Enter-HcsMaintenanceMode`
   
    <span data-ttu-id="0775a-167">下方顯示一項範例輸出。</span><span class="sxs-lookup"><span data-stu-id="0775a-167">A sample output is shown below.</span></span>
   
        Controller0>Enter-HcsMaintenanceMode
        Checking device state...
   
        In maintenance mode, your device will not service IOs and will be disconnected from the Microsoft Azure StorSimple Manager service. Entering maintenance mode will end the current session and reboot both controllers, which takes a few minutes to complete. Are you sure you want to enter maintenance mode?
        [Y] Yes [N] No (Default is "Y"): Y
   
        -----------------------MAINTENANCE MODE------------------------
        Microsoft Azure StorSimple Appliance Model 8600
        Name: Update4-8600-mystorsimple
        Copyright (C) 2014 Microsoft Corporation. All rights reserved.
        You are connected to Controller0 - Passive
        ---------------------------------------------------------------
   
        Serial Console Menu
        [1] Log in with full access
        [2] Log into peer controller with full access
        [3] Connect with limited access
        [4] Change language
        Please enter your choice>
   
    <span data-ttu-id="0775a-168">接著，兩個控制器就會重新啟動以進入維護模式。</span><span class="sxs-lookup"><span data-stu-id="0775a-168">Both the controllers then restart into maintenance mode.</span></span>
2. <span data-ttu-id="0775a-169">若要安裝磁碟韌體更新，請輸入：</span><span class="sxs-lookup"><span data-stu-id="0775a-169">To install the disk firmware update, type:</span></span>
   
    `Start-HcsHotfix -Path <path to update file> -Credential <credentials in domain\username format>`
   
    <span data-ttu-id="0775a-170">下方顯示一項範例輸出。</span><span class="sxs-lookup"><span data-stu-id="0775a-170">A sample output is shown below.</span></span>
   
        Controller1>Start-HcsHotfix -Path \\10.100.100.100\share\ThirdOrderUpdates\ -Credential contoso\john
        Enter Password:
        WARNING: In maintenance mode, hotfixes should be installed on each controller sequentially. After the hotfix is installed on this controller, install it on the peer controller.
        Confirm
        This operation starts a hotfix installation and could reboot one or both of the controllers. By installing new updates you agree to, and accept any additional terms associated with, the new functionality listed in the release notes (https://go.microsoft.com/fwLink/?LinkID=613790). Are you sure you want to continue?
        [Y] Yes [N] No (Default is "Y"): Y
        WARNING: Installation is currently in progress. This operation can take several minutes to complete.
3. <span data-ttu-id="0775a-171">使用 `Get-HcsUpdateStatus` 命令監視安裝進度。</span><span class="sxs-lookup"><span data-stu-id="0775a-171">Monitor the install progress using `Get-HcsUpdateStatus` command.</span></span> <span data-ttu-id="0775a-172">當 `RunInProgress` 變成 `False` 時，代表更新完成。</span><span class="sxs-lookup"><span data-stu-id="0775a-172">The update is complete when the `RunInProgress` changes to `False`.</span></span>
4. <span data-ttu-id="0775a-173">安裝完成之後，維護模式 Hotfix 安裝所在的控制器將會重新開機。</span><span class="sxs-lookup"><span data-stu-id="0775a-173">After the installation is complete, the controller on which the maintenance mode hotfix was installed restarts.</span></span> <span data-ttu-id="0775a-174">以具有完整存取權的選項 1 登入，並驗證磁碟韌體版本。</span><span class="sxs-lookup"><span data-stu-id="0775a-174">Log in as option 1 with full access and verify the disk firmware version.</span></span> <span data-ttu-id="0775a-175">輸入：</span><span class="sxs-lookup"><span data-stu-id="0775a-175">Type:</span></span>
   
   `Get-HcsFirmwareVersion`
   
   <span data-ttu-id="0775a-176">預期的磁碟韌體版本為：</span><span class="sxs-lookup"><span data-stu-id="0775a-176">The expected disk firmware versions are:</span></span>
   
   `XMGJ, XGEG, KZ50, F6C2, VR08, N002, 0106`
   
   <span data-ttu-id="0775a-177">下方顯示一項範例輸出。</span><span class="sxs-lookup"><span data-stu-id="0775a-177">A sample output is shown below.</span></span>
   
       -----------------------MAINTENANCE MODE------------------------
       Microsoft Azure StorSimple Appliance Model 8600
       Name: Update4-8600-mystorsimple
       Software Version: 6.3.9600.17820
       Copyright (C) 2014 Microsoft Corporation. All rights reserved.
       You are connected to Controller1
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
   
    <span data-ttu-id="0775a-178">在第二個控制站上執行 `Get-HcsFirmwareVersion` 命令來驗證軟體版本已經更新。</span><span class="sxs-lookup"><span data-stu-id="0775a-178">Run the `Get-HcsFirmwareVersion` command on the second controller to verify that the software version has been updated.</span></span> <span data-ttu-id="0775a-179">然後您就可以結束維護模式。</span><span class="sxs-lookup"><span data-stu-id="0775a-179">You can then exit the maintenance mode.</span></span> <span data-ttu-id="0775a-180">若要這麼做，請針對每個裝置控制器輸入以下命令：</span><span class="sxs-lookup"><span data-stu-id="0775a-180">To do so, type the following command for each device controller:</span></span>
   
   `Exit-HcsMaintenanceMode`

5. <span data-ttu-id="0775a-181">當您離開維護模式時，控制器便會重新啟動。</span><span class="sxs-lookup"><span data-stu-id="0775a-181">The controllers restart when you exit maintenance mode.</span></span> <span data-ttu-id="0775a-182">在磁碟韌體更新已成功套用且裝置已結束維護模式後，返回 Azure 傳統入口網站。</span><span class="sxs-lookup"><span data-stu-id="0775a-182">After the disk firmware updates are successfully applied and the device has exited maintenance mode, return to the Azure classic portal.</span></span> <span data-ttu-id="0775a-183">請注意，入口網站可能有 24 小時的時間不會顯示您已安裝維護模式更新。</span><span class="sxs-lookup"><span data-stu-id="0775a-183">Note that the portal might not show that you installed the maintenance mode updates for 24 hours.</span></span>

