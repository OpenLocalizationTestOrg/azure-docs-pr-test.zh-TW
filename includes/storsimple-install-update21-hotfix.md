<!--author=alkohli last changed: 05/19/16-->

#### <a name="toodownload-hotfixes"></a>toodownload hotfix
執行 hello hello Microsoft Update 類別目錄中的下列步驟 toodownload hello 軟體更新。

1. 啟動 Internet Explorer 並瀏覽過[http://catalog.update.microsoft.com](http://catalog.update.microsoft.com)。
2. 如果這是您第一次使用 hello Microsoft Update 類別目錄，在此電腦上，按一下**安裝**時提示的 tooinstall hello Microsoft Update 類別目錄的附加元件。
    ![安裝目錄](./media/storsimple-install-update2-hotfix/HCS_InstallCatalog-include.png)
3. 在 hello hello Microsoft Update 類別目錄的搜尋方塊中輸入 hello 知識庫 (KB) 號碼 hello hotfix 您想讓 toodownload，例如**3179904**，然後按一下**搜尋**。
   
    hello hotfix 清單會出現，例如**StorSimple 8000 系列的累計軟體配套更新 2.2**。
   
    ![搜尋目錄](./media/storsimple-install-update2-hotfix/HCS_SearchCatalog1-include.png)
4. 按一下 [新增] 。 hello 更新已新增 toohello 籃。
5. Hello 上表中列出的搜尋任何其他的 hotfix (**3103616**， **3146621**)，並將每個 toohello 購物籃。
6. 按一下 [ **檢視購物籃**]。
7. 按一下 [下載] 。 指定或**瀏覽**所在 hello 下載 tooappear tooa 本機位置。 hello 下載更新 toohello 指定的位置，並放在與名稱為 「 hello 更新相同的 hello 的子資料夾。 hello 資料夾也可以複製的 tooa 從 hello 裝置的網路共用。

> [!NOTE]
> hello hotfix 必須能夠從這兩個控制器 toodetect，hello 同儕節點控制器的任何潛在的錯誤訊息。
> 
> 

#### <a name="tooinstall-and-verify-regular-mode-hotfixes"></a>tooinstall 並確認一般模式 hotfix
執行下列步驟 tooinstall hello，並確認一般模式 hotfix。 如果您已安裝使用 hello Azure 入口網站中，跳過[安裝，並確認 維護模式 hotfix](#to-install-and-verify-maintenance-mode-hotfixes)。

1. 您的 StorSimple 裝置序列主控台存取 hello Windows PowerShell 介面 tooinstall hello hotfix。 請遵循詳細指示中的 hello[使用 PuTTy tooconnect toohello 序列主控台](../articles/storsimple/storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console)。 在 hello 命令提示字元中，按下**Enter**。
2. 選取**選項 1** toolog toohello 具有完整存取權的裝置上。 我們建議您安裝 hello hotfix hello 被動控制站上第一次。
3. tooinstall hello hotfix，在 hello 命令提示字元，輸入：
   
    `Start-HcsHotfix -Path <path tooupdate file> -Credential <credentials in domain\username format>`
   
    Hello 上述命令中的共用路徑中使用 IP，而不是 DNS。 只有當您要存取已驗證的共用時，才使用 hello 認證參數。
   
    我們建議您使用 hello 認證參數 tooaccess 共用。 即使已開啟太"everyone"通常的共用開啟 toounauthenticated 使用者。
   
    提供 hello 密碼提示。
   
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
   
   > [!IMPORTANT]
   > 如果安裝更新 2.2，只能安裝 hello 二進位檔案做為 ' all hcsmdssoftwareudpate' 開頭。 請勿安裝 hello Ci 和 hello MDS 代理程式更新做為所有 cismdsagentupdatebundle 開頭。 失敗 toodo 因此將會導致錯誤。 

5. 使用 hello 監視 hello 更新`Get-HcsUpdateStatus`cmdlet。 hello 更新將會先完成 hello 被動控制站上。 一旦更新 hello 被動控制器，將會在容錯移轉和 hello 更新然後會套用在 hello 另一個控制器。 兩個 hello 控制器更新時，hello 更新已完成。
   
    hello 下列範例輸出顯示 hello 更新正在進行中。 hello`RunInprogress`將`True`hello 更新正在進行中。
   
    ```
    Controller0>Get-HcsUpdateStatus
    RunInprogress       : True
    LastHotfixTimestamp :
    LastUpdateTimestamp : 5/5/2016 2:04:02 AM
    Controller0Events   :
    Controller1Events   :
    ```
   
     下列範例輸出的 hello 指出該 hello 更新已完成。 hello`RunInProgress`將`False`hello 更新已完成時。
   
    ```
    Controller0>Get-HcsUpdateStatus
    RunInprogress       : False
    LastHotfixTimestamp : 5/17/2016 9:15:55 AM
    LastUpdateTimestamp : 5/17/2016 9:06:07 AM
    Controller0Events   :
    Controller1Events   :
    ```

    > [!NOTE]
    > 有時候，hello cmdlet 報告`False`hello 更新時仍在進行中。 hello hotfix 的 tooensure 已完成、 等候幾分鐘的時間，重新執行此命令並確認該 hello`RunInProgress`是`False`。 如果是，已完成 hello hotfix。

1. Hello 軟體更新已完成之後，請確認 hello 系統軟體版本。 輸入：
   
    `Get-HcsSystem`
   
    您應該會看到下列版本的 hello:
   
   * `HcsSoftwareVersion: 6.3.9600.17708`
   * `CisAgentVersion: 1.0.9299.0`
   * `MdsAgentVersion: 30.0.4698.16` 
     
     如果 hello 版本號碼不會變更 hello 項更新，則表示該 hello hotfix tooapply 失敗。 若您看到這種情況，請連絡 [Microsoft 支援](../articles/storsimple/storsimple-contact-microsoft-support.md)以取得進一步的協助。
     
     > [!IMPORTANT]
     > 您必須重新啟動 hello 作用中的控制器透過 hello `Restart-HcsController` cmdlet 然後才套用 hello 剩餘的更新。 
     > 
     > 
2. 重複步驟 3-5 tooinstall hello 剩餘一般模式 hotfix。
   
   * hello iSCSI 更新 KB3146621
   * hello WMI 更新 KB3103616
3. 如果您要從 Update 2 進行更新，請略過此步驟。 如果您要更新的版本先前 tooUpdate 2，您也需要 toodownload:

    - hello LSI 驅動程式 KB3121900

    - hello 太空更新 KB3090322

    - hello Storport 更新 KB3080728

#### <a name="tooinstall-and-verify-maintenance-mode-hotfixes"></a>tooinstall 並確認 維護模式 hotfix
使用 KB3121899 tooinstall 磁碟韌體更新。 這些更新具有干擾性，並採取 toocomplete 大約 30 分鐘的時間。 您可以選擇 tooinstall 計劃性的維護視窗中的這些連接 toohello 裝置序列主控台。

請注意，是否磁碟韌體已經是最新的就不需要 tooinstall 這些更新。 執行 hello `Get-HcsUpdateAvailability` hello 裝置序列主控台 toocheck 如果更新可用，以及是否 hello cmdlet 更新具有干擾性 （維護模式） 或非干擾性 （一般模式） 的更新。

tooinstall hello 磁碟韌體更新，請遵循下列的 hello 指示。

1. 將 hello 裝置放在 hello 維護模式。 請注意，您不應該使用 Windows PowerShell 遠端連接 tooa 裝置處於維護模式時。 改為在 hello 裝置控制器透過 hello 裝置序列主控台連接時執行這個指令程式。 輸入：
   
    `Enter-HcsMaintenanceMode`
   
    下方顯示一項範例輸出。
   
        Controller0>Enter-HcsMaintenanceMode
        Checking device state...
   
        In maintenance mode, your device will not service IOs and will be disconnected from hello Microsoft Azure StorSimple Manager service. Entering maintenance mode will end hello current session and reboot both controllers, which takes a few minutes toocomplete. Are you sure you want tooenter maintenance mode?
        [Y] Yes [N] No (Default is "Y"): Y
   
        -----------------------MAINTENANCE MODE------------------------
        Microsoft Azure StorSimple Appliance Model 8100
        Name: Update2-8100-SHG0997879L76673
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
        This operation starts a hotfix installation and could reboot one or both of hello controllers. By installing new updates you agree to, and accept any additional terms associated with, hello new functionality listed in hello release notes (https://go.microsoft.com/fwLink/?LinkID=613790). Are you sure you want toocontinue?
        [Y] Yes [N] No (Default is "Y"): Y
        WARNING: Installation is currently in progress. This operation can take several minutes toocomplete.
3. 監視 hello 安裝進度使用`Get-HcsUpdateStatus`命令。 hello 更新已完成時 hello`RunInProgress`變更太`False`。
4. Hello 安裝完成後，重新啟動維護模式 hotfix 安裝在哪些 hello 的 hello 控制器。 具有完整存取權的選項 1 身分登入，並確認 hello 磁碟韌體版本。 輸入：
   
   `Get-HcsFirmwareVersion`
   
   hello 預期磁碟韌體版本：
   
   `XMGG, XGEG, KZ50, F6C2, VR08`
   
   下方顯示一項範例輸出。
   
       -----------------------MAINTENANCE MODE------------------------
       Microsoft Azure StorSimple Appliance Model 8100
       Name: Update2-8100-SHG0997879L76YD
       Software Version: 6.3.9600.17705
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
   
    執行 hello `Get-HcsFirmwareVersion` hello 第二個控制站 tooverify 的 hello 軟體版本上的命令已經過更新。 然後您就可以結束 hello 維護模式。 toodo 因此，請輸入下列命令，每個裝置控制器的 hello:
   
   `Exit-HcsMaintenanceMode`
5. 當您結束維護模式時，重新啟動 hello 控制站。 已成功套用之後 hello 磁碟韌體更新，而且 hello 裝置已離開維護模式，傳回 toohello Azure 傳統入口網站。 請注意該 hello 入口網站可能不會顯示您安裝的 24 小時內的 hello 維護模式更新。

