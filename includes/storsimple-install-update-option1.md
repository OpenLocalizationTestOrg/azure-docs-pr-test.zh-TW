<!--author=SharS last changed: 03/17/2016-->

#### <a name="toodownload-hotfixes"></a>toodownload hotfix
執行下列步驟 toodownload hello 軟體更新的 hello。

1. 啟動 Internet Explorer 並瀏覽過[http://catalog.update.microsoft.com](http://catalog.update.microsoft.com)。
2. 如果這是您第一次使用 hello Microsoft Update 類別目錄，在此電腦上，按一下**安裝**時提示的 tooinstall hello Microsoft Update 類別目錄的附加元件。
    ![安裝目錄](./media/storsimple-install-update-option-1/HCS_InstallCatalog-include.png)
3. 在 hello hello Microsoft Update 類別目錄的搜尋方塊中輸入 hello 知識庫 (KB) 號碼 hello hotfix 您想讓 toodownload，例如**3063418**，然後按一下**搜尋**。
4. 您會看到 hello **StorSimple 更新 1.2 應用裝置更新**組合。 按一下 [新增] 。 hello 更新將會加入 toohello 籃。
5. Hello 上表中列出的搜尋任何其他的 hotfix (**3043005**和**3063416**)，並將每個 hello 購物籃。
6. 按一下 [ **檢視購物籃**]。
   
    ![檢視購物籃](./media/storsimple-install-update-option-1/HCS_InstallBasket-include.png)
7. 按一下 [下載] 。 指定或**瀏覽**所在 hello 下載 tooappear tooa 本機位置。 hello 下載更新 toohello 指定的位置，並放在名稱為 「 hello 更新相同的 hello 與子資料夾中。 hello 資料夾也可以複製的 tooa 從 hello 裝置的網路共用。

> [!NOTE]
> hello hotfix 必須能夠從這兩個控制器 toodetect，hello 同儕節點控制器的任何潛在的錯誤訊息。
> 
> 

#### <a name="tooinstall-and-verify-regular-mode-hotfixes"></a>tooinstall 並確認一般模式 hotfix
執行下列步驟 tooinstall hello，並確認 hello 一般模式 hotfix。 如果您已安裝使用 hello Azure 入口網站中，跳過[安裝，並確認 維護模式 hotfix](#to-install-and-verify-maintenance-mode-hotfixes)。

1. tooinstall hello 軟體更新，您的 StorSimple 裝置序列主控台存取 hello Windows PowerShell 介面。 請遵循詳細指示中的 hello[使用 PuTTy tooconnect toohello 序列主控台](../articles/storsimple/storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console)。 在 hello 命令提示字元中，按下**Enter**。
2. 選取**選項 1** toolog toohello 具有完整存取權的裝置上。
3. tooinstall hello 更新套件，在 hello 命令提示字元，輸入：
   
    `Start-HcsHotfix -Path <path tooupdate file> -Credential <credentials in domain\username format>`
   
    Hello 上述命令中的共用路徑中使用 IP，而不是 DNS。 只有當您要存取已驗證的共用時，才使用 hello 認證參數。
   
    我們建議您使用 hello 認證參數 tooaccess 共用。 即使已開啟太"everyone"通常的共用開啟 toounauthenticated 使用者。
   
    下方顯示一項範例輸出。
   
    ```
    Controller0>Start-HcsHotfix -Path \\10.100.100.100\share
    \hcsmdssoftwareupdate.exe -Credential contoso\John

    Confirm

    This operation starts hello hotfix installation and could reboot one or
    both of hello controllers. If hello device is serving I/Os, these will not
    be disrupted. Are you sure you want toocontinue?
    [Y] Yes [N] No [?] Help (default is "Y"): Y
    ```

4. 型別**Y**時提示的 tooconfirm hello hotfix 安裝。
5. 使用 hello 監視 hello 更新`Get-HcsUpdateStatus`cmdlet。
   
    hello 下列範例輸出顯示 hello 更新正在進行中。 hello`RunInprogress`將`True`hello 更新正在進行中。
   
    ```
    Controller0>Get-HcsUpdateStatus
    RunInprogress       : True
    LastHotfixTimestamp : 9/02/2015 10:36:13 PM
    LastUpdateTimestamp : 9/02/2015 10:35:25 PM
    Controller0Events   :
    Controller1Events   :
    ```
   
     下列範例輸出的 hello 指出該 hello 更新已完成。 hello`RunInProgress`將`False`hello 更新已完成時。

    ```
    Controller1>Get-HcsUpdateStatus

    RunInprogress       : False
    LastHotfixTimestamp : 9/02/2015 10:56:13 PM
    LastUpdateTimestamp : 9/02/2015 10:35:25 PM
    Controller0Events   :
    Controller1Events   :
    ```
   
   > [!NOTE]
   > 有時候，hello cmdlet 報告`False`hello 更新時仍在進行中。 hello hotfix 的 tooensure 已完成、 等候幾分鐘的時間，重新執行此命令並確認該 hello`RunInProgress`是`False`。 如果是，已完成 hello hotfix。
   > 
   > 
6. Hello 軟體更新已完成之後，請確認 hello 系統軟體版本。 輸入下列命令的 hello:
   
    `Get-HcsSystem`
   
    您應該會看到下列版本的 hello:
   
   * HcsSoftwareVersion：6.3.9600.17584
   * CisAgentVersion：1.0.9049.0
   * MdsAgentVersion：26.0.4696.1433
     
     如果 hello 版本號碼不會變更 hello 項更新，則表示該 hello hotfix tooapply 失敗。 若您看到這種情況，請連絡 [Microsoft 支援](../articles/storsimple/storsimple-contact-microsoft-support.md)以取得進一步的協助。
7. 重複步驟 3-5 tooinstall hello 剩餘一般模式 hotfix (KB3043005)。

#### <a name="tooinstall-and-verify-maintenance-mode-hotfixes"></a>tooinstall 並確認 維護模式 hotfix
使用 KB3063416 tooinstall 磁碟韌體更新。 這些更新具有干擾性，並採取 30-45 分鐘 toocomplete 周圍。 您可以選擇 tooinstall 計劃性的維護視窗中的這些連接 toohello 裝置序列主控台。

tooinstall hello 磁碟韌體更新，請遵循下列的 hello 指示。

1. 裝置 hello 置於維護模式。 請注意，您不應該使用 Windows PowerShell 遠端連接 tooa 裝置處於維護模式時。 您將需要 toorun hello 裝置控制器透過 hello 裝置序列主控台連接時這個指令程式。 輸入：
   
    `Enter-HcsMaintenanceMode`
   
    下方顯示一項範例輸出。
   
        Controller0>Enter-HcsMaintenanceMode
        Checking device state...
   
        In maintenance mode, your device will not service IOs and will be disconnected from hello Microsoft Azure StorSimple Manager service. Entering maintenance mode will end hello current session and reboot both controllers, which takes a few minutes toocomplete. Are you sure you want tooenter maintenance mode?
        [Y] Yes [N] No (Default is "Y"): Y
   
        -----------------------MAINTENANCE MODE------------------------
        Microsoft Azure StorSimple Appliance Model 8100
        Name: Update1-8100-SHG0997879L76YD
        Software Version: 6.3.9600.17584
        Copyright (C) 2014 Microsoft Corporation. All rights reserved.
        You are connected tooController0 - Passive
        ---------------------------------------------------------------
        Serial Console Menu
        [1] Log in with full access
        [2] Log into peer controller with full access
        [3] Connect with limited access
        [4] Change language
        Please enter your choice>
   
    兩個 hello 控制器，然後重新啟動進入維護模式。
2. tooinstall hello 磁碟韌體更新，類型：
   
    `Start-HcsHotfix -Path <path tooupdate file> -Credential <credentials in domain\username format>`
   
    下方顯示一項範例輸出。
   
        Controller1>Start-HcsHotfix -Path \\10.100.100.100\share\DiskFirmwarePackage.exe -Credential contoso\john
        Enter Password:
        WARNING: In maintenance mode, hotfixes should be installed on each controller sequentially. After hello hotfix is installed on this controller, install it on hello peer controller.
        Confirm
        This operation starts a hotfix installation and could reboot one or both of hello controllers. Are you sure you want toocontinue?
        [Y] Yes [N] No (Default is "Y"): Y
        WARNING: Installation is currently in progress. This operation can take several minutes toocomplete.
3. 監視 hello 安裝進度使用`Get-HcsUpdateStatus`命令。 hello 更新已完成時 hello`RunInProgress`變更太`False`。
4. Hello 安裝完成後，將會重新啟動 hello 維護模式 hotfix 安裝所在的 hello 控制站。 具有完整存取權的選項 1 身分登入，並確認 hello 磁碟韌體版本。 輸入：
   
   `Get-HcsFirmwareVersion`
   
   hello 預期磁碟韌體版本：
   
   `XMGG, XGEE, KZ50, F6C2, VR08`
   
   執行 hello `Get-HcsFirmwareVersion` hello 第二個控制站 tooverify 的 hello 軟體版本上的命令已經過更新。 然後您就可以結束 hello 維護模式。 輸入下列命令，每個裝置控制器的 hello:
   
   `Exit-HcsMaintenanceMode`
5. 當您結束維護模式時，重新啟動 hello 控制站。 已成功套用之後 hello 磁碟韌體更新，而且 hello 裝置已離開維護模式，傳回 toohello Azure 傳統入口網站。 請注意該 hello 入口網站可能不會顯示您安裝的 24 小時內的 hello 維護模式更新。

