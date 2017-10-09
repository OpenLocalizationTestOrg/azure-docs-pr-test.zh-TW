<!--author=alkohli last changed: 12/01/15-->


#### <a name="tooconfigure-and-register-hello-device"></a>tooconfigure 和註冊 hello 裝置
1. 存取您 StorSimple 裝置序列主控台 hello Windows PowerShell 介面。 請參閱[使用 PuTTY tooconnect toohello 裝置序列主控台](#use-putty-to-connect-to-the-device-serial-console)如需相關指示。 **剛好是確定 toofollow hello 程序，或將不會無法 tooaccess hello 主控台。**
2. 在開啟的 hello 工作階段，按下 Enter 一個時間 tooget 命令提示字元。 
3. 您將會是您想要為您的裝置 tooset 提示的 toochoose hello 語言。 指定 hello 語言，然後按 Enter 鍵。 
   
    ![StorSimple 設定和註冊裝置 1](./media/storsimple-configure-and-register-device/HCS_RegisterYourDevice1-include.png)
4. 在呈現的 hello 序列主控台功能表，選擇選項 1 toolog 上具有完整存取權。 
   
    ![StorSimple 註冊裝置 2](./media/storsimple-configure-and-register-device/HCS_RegisterYourDevice2-include.png)
   
     完成步驟 5-12 tooconfigure hello 最小必要的網路設定為您的裝置。 **這些設定步驟必須 toobe hello 裝置 hello 作用中控制器上執行。** hello 序列主控台功能表會指出 hello 橫幅訊息中的 hello 控制器狀態。 如果您未連接 toohello 主動控制器，就會中斷連線，並再連線 toohello 作用中控制器。
5. 在 hello 命令提示字元中輸入您的密碼。 hello 預設裝置密碼**Password1**。
6. 輸入下列命令的 hello:
   
     `Invoke-HcsSetupWizard` 
7. 安裝精靈會出現 toohelp 設定 hello hello 裝置的網路設定。 提供下列資訊的 hello hello: 
   
   * Hello DATA 0 網路介面的 IP 位址
   * 子網路遮罩
   * 閘道器
   * 適用於主要 DNS 伺服器的 IP 位址
   * 適用於主要 NTP 伺服器的 IP 位址
     
     > [!NOTE]
     > 您可能必須 toowait hello 子網路遮罩和套用 hello DNS 設定 toobe 幾分鐘。 如果您收到 「 hello 裝置尚未就緒。 」 錯誤訊息中，核取 hello 實體網路上連線 hello DATA 0 網路介面在主動控制站。
     > 
     > 
8. (選用) 設定 Web Proxy 伺服器。 雖然 Web Proxy 設定是選用的，但 **請注意，如果您使用 Web Proxy，就只能在此處設定它**。 如需詳細資訊，請移至太[設定 web proxy 為您的裝置](../articles/storsimple/storsimple-configure-web-proxy.md)。 如果這個步驟時遇到任何問題，請參閱 tootroubleshooting 指導[web proxy 組態期間發生的錯誤](../articles/storsimple/storsimple-troubleshoot-deployment.md#errors-during-the-optional-web-proxy-settings)。

     > [!NOTE]
     > 您可以按 Ctrl + C，在任何時間 tooexit hello 安裝精靈。 您在發出此命令之前套用的所有設定都將保留。

1. 基於安全性理由，hello 裝置系統管理員密碼過期之後 hello 第一個工作階段，而且您將需要 toochange 它後續的工作階段。 出現提示時，請提供裝置系統管理員密碼。 有效的裝置系統管理員密碼長度必須介於 8 到 15 個字元。 hello 密碼必須包含小寫字元、 大寫字元、 數字和特殊字元的組合。
2. 這裡也會設 hello StorSimple Snapshot Manager 密碼。 向執行 StorSimple Snapshot Manager 的 Windows 主機驗證裝置時，您可以使用此密碼。 出現提示時，提供 14 too15 字元的密碼。 hello 密碼必須包含的組合中的 hello 下列三種： 小寫字母、 大寫字母、 數字及特殊字元。 
   
   ![StorSimple 註冊裝置 4](./media/storsimple-configure-and-register-device/HCS_RegisterYourDevice4-include.png)
   
   您可以重設 hello StorSimple Manager 服務介面中的 hello StorSimple Snapshot Manager 密碼。 如需詳細步驟，請移太[變更使用 hello StorSimple Manager 服務的 hello StorSimple 密碼](../articles/storsimple/storsimple-change-passwords.md)。
   
   tootroubleshoot 在此步驟中，任何問題，請參閱 tootroubleshooting 指導[錯誤相關 toopasswords](../articles/storsimple/storsimple-troubleshoot-deployment.md#errors-related-to-device-administrator-and-storsimple-snapshot-manager-passwords)。
3. hello hello 安裝精靈中的最後一個步驟以 hello StorSimple Manager 服務註冊您的裝置。 這麼做，您必須使用您在步驟 2 中取得的 hello 服務註冊金鑰。 您提供 hello 註冊金鑰之後，您可能需要 toowait 2-3 分鐘，hello 裝置完成註冊。
   
   tootroubleshoot 任何可能的裝置註冊失敗，請參閱太[裝置註冊期間發生的錯誤](../articles/storsimple/storsimple-troubleshoot-deployment.md#errors-during-device-registration)。 如需詳細的疑難排解，您也可以使用參照太[逐步疑難排解範例](../articles/storsimple/storsimple-troubleshoot-deployment.md#step-by-step-storsimple-troubleshooting-example)。
4. Hello 裝置完成註冊之後，會出現服務資料加密金鑰。 複製這個金鑰，並將它儲存在安全的位置。
   
   > [!WARNING]
   > 此金鑰必須與 hello 服務註冊金鑰 tooregister 其他裝置以 hello StorSimple Manager 服務。 請參閱太[StorSimple 安全性](../articles/storsimple/storsimple-security.md)如需有關這個索引鍵。
   > 
   > 
   
    ![StorSimple 註冊裝置 6](./media/storsimple-configure-and-register-device/HCS_RegisterYourDevice6-include.png)
   
    toocopy hello 文字從 hello 序列主控台視窗中，只需選取 hello 文字。 接著，您應該就能 toopaste hello 剪貼簿或任何文字編輯器中。 不要使用 Ctrl + C toocopy hello 服務資料加密金鑰。 使用 Ctrl + C 將導致您 tooexit hello 安裝精靈。 如此一來，hello 裝置系統管理員密碼和 hello StorSimple Snapshot Manager 密碼將不會變更和 hello 裝置將會回復 toohello 預設密碼。
5. 結束 hello 序列主控台。
6. 傳回 toohello Azure 傳統入口網站，並完成下列步驟的 hello:
   
   1. 按兩下您的 StorSimple Manager 服務 tooaccess hello**快速入門**頁面。
   2. 按一下 [檢視連接的裝置] 。
   3. 在 hello**裝置**頁面上，確認該 hello 裝置已成功連接 toohello 服務查閱 hello 狀態。 hello 裝置狀態應為**線上**。 如果 hello 裝置狀態是**離線**，等待幾分鐘的 hello 裝置 toocome 線上。
   
   ![StorSimple 裝置頁面](./media/storsimple-configure-and-register-device/HCS_DevicesPageM-include.png) 
   
   > [!IMPORTANT]
   > Hello 裝置為線上狀態之後，插入 hello 網路纜線，您必須在此步驟中的 hello 開頭拔除。
   > 
   > 

Hello 裝置註冊成功及不上線之後，您可以執行 hello `Test-HcsmConnection -Verbose` hello 網路連線的 tooensure 狀況良好。 Hello 詳細使用狀況，此 cmdlet，請移過[Test-hcsmconnection cmdlet 參考](https://technet.microsoft.com/library/dn715782.aspx)。

![提供的影片](./media/storsimple-configure-and-register-device/Video_icon.png) **提供的影片**

toowatch 的視訊示範，如何 tooconfigure 和註冊裝置透過 Windows PowerShell for StorSimple 中，按一下[這裡](https://azure.microsoft.com/documentation/videos/initialize-the-storsimple-appliance/)。

