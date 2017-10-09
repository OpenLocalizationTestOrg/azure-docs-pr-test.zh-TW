<!--author=SharS last changed: 02/22/2016-->

### <a name="tooconfigure-and-register-hello-device"></a>tooconfigure 和註冊 hello 裝置
1. 存取您 StorSimple 裝置序列主控台 hello Windows PowerShell 介面。 請參閱[使用 PuTTY tooconnect toohello 裝置序列主控台](../articles/storsimple/storsimple-deployment-walkthrough-gov-u2.md#use-putty-to-connect-to-the-device-serial-console)如需相關指示。 **剛好是確定 toofollow hello 程序，或將不會無法 tooaccess hello 主控台。**
2. 在開啟的 hello 工作階段，按下 Enter 一個時間 tooget 命令提示字元。
3. 您將會是您想要為您的裝置 tooset 提示的 toochoose hello 語言。 指定 hello 語言，然後按 Enter 鍵。
   
    ![StorSimple 設定和註冊裝置 1](./media/storsimple-configure-and-register-device-gov-u2/HCS_RegisterYourDevice1-gov-include.png)
4. 在呈現的 hello 序列主控台功能表，選擇選項 1 toolog 上具有完整存取權。
   
    ![StorSimple 註冊裝置 2](./media/storsimple-configure-and-register-device-gov-u2/HCS_RegisterYourDevice2-gov-include.png)
5. 執行下列步驟 tooconfigure hello 最小必要的網路設定為您的裝置 hello。
   
   > [!IMPORTANT]
   > 這些設定步驟必須 toobe hello 裝置 hello 作用中控制器上執行。 hello 序列主控台功能表會指出 hello 橫幅訊息中的 hello 控制器狀態。 如果您不是連接 toohello 作用中控制器，中斷連線，然後連接 toohello 作用中控制器。
   > 
   > 
   
   1. 在 hello 命令提示字元中輸入您的密碼。 hello 預設裝置密碼**Password1**。
   2. 輸入下列命令的 hello:
      
        `Invoke-HcsSetupWizard`
   3. 安裝精靈會出現 toohelp 設定 hello hello 裝置的網路設定。 提供下列資訊的 hello:
      
      * 適用於 DATA 0 網路介面的 IP 位址
      * 子網路遮罩
      * 閘道器
      * 適用於主要 DNS 伺服器的 IP 位址
      * 適用於主要 NTP 伺服器的 IP 位址
      
      > [!NOTE]
      > 您可能必須 toowait hello 子網路遮罩和 DNS 設定 toobe 套用幾分鐘。
      > 
      > 
   4. 選擇性設定 Web Proxy 伺服器。
      
      > [!IMPORTANT]
      > 雖然 Web Proxy 設定是選用的，但請注意，如果您使用 Web Proxy，就只能在此處設定它。 如需詳細資訊，請移至太[設定 web proxy 為您的裝置](../articles/storsimple/storsimple-configure-web-proxy.md)。
      > 
      > 
6. 按 Ctrl + C tooexit hello 安裝精靈。
7. 安裝 hello 更新，如下所示：
   
   1. 使用下列兩個 hello 控制器上的 cmdlet tooset Ip hello:
      
      `Set-HcsNetInterface -InterfaceAlias Data0 -Controller0IPv4Address <Controller0 IP> -Controller1IPv4Address <Controller1 IP>`
   2. 在 hello 命令提示字元中執行`Get-HcsUpdateAvailability`。 您應該會在更新可用時收到通知。
   3. 執行 `Start-HcsUpdate`。 您可以在任何模式中執行此命令。 將在 hello 第一個控制器上套用更新、 hello 控制器將會容錯移轉，和在套用更新的 hello 然後 hello 另一個控制器。
      
      您可以藉由執行監視 hello hello 更新進度`Get-HcsUpdateStatus`。    
      
      hello 下列範例輸出顯示 hello 更新正在進行中。
      
      ````
      Controller0>Get-HcsUpdateStatus
      RunInprogress       : True
      LastHotfixTimestamp : 4/13/2015 10:56:13 PM
      LastUpdateTimestamp : 4/13/2015 10:35:25 PM
      Controller0Events   :
      Controller1Events   :
      ````
      
      下列範例輸出的 hello 指出該 hello 更新已完成。
      
      ```
      Controller1>Get-HcsUpdateStatus
      
      RunInprogress       : False
      LastHotfixTimestamp : 4/13/2015 10:56:13 PM
      LastUpdateTimestamp : 4/13/2015 10:35:25 PM
      Controller0Events   :
      Controller1Events   :
      ```
      
      它可能會佔用 too11 小時 tooapply 所有 hello 更新，包括 hello Windows 更新。
8. 執行下列 cmdlet toopoint hello 裝置 toohello Microsoft Azure 政府入口網站 （因為它所指 toohello 公用 Azure 傳統入口網站的預設值） 的 hello。 這樣會重新啟動兩個控制器。 我們建議您使用兩個 toosimultaneously 連接 tooboth 控制站，以便您可以看到每個控制站何時會重新啟動的 PuTTY 工作階段。
   
    `Set-CloudPlatform -AzureGovt_US`
   
   您將會看見確認訊息。 接受 hello 預設 (**Y**)。
9. 執行下列 cmdlet tooresume 安裝 hello:
   
    `Invoke-HcsSetupWizard`
   
    ![繼續設定精靈](./media/storsimple-configure-and-register-device-gov-u2/HCS_ResumeSetup-gov-include.png)
   
   當您繼續安裝時，hello 精靈將 hello Update 2 的版本。
10. 接受 hello 網路設定。 在您接受每個設定之後，您會看到驗證訊息。
11. 基於安全性理由，hello 裝置系統管理員密碼過期之後 hello 第一個工作階段，而且您將需要 toochange 現在 it。 出現提示時，請提供裝置系統管理員密碼。 有效的裝置系統管理員密碼長度必須介於 8 到 15 個字元。 hello 密碼必須包含的 hello 下列三種： 小寫字母、 大寫字母、 數字及特殊字元。
    
    <br/>![StorSimple 註冊裝置 5](./media/storsimple-configure-and-register-device-gov-u2/HCS_RegisterYourDevice5_gov-include.png)
12. hello hello 安裝精靈中的最後一個步驟以 hello StorSimple Manager 服務註冊您的裝置。 這麼做，您將需要 hello 中取得的服務註冊金鑰[步驟 2： 取得 hello 服務註冊金鑰](../articles/storsimple/storsimple-deployment-walkthrough-gov-u2.md#step-2-get-the-service-registration-key)。 您提供 hello 註冊金鑰之後，您可能需要 toowait 2-3 分鐘，hello 裝置完成註冊。
    
    > [!NOTE]
    > 您可以按 Ctrl + C，在任何時間 tooexit hello 安裝精靈。 如果您輸入所有 hello 網路設定 （針對 Data 0、 子網路遮罩和閘道的 IP 位址），則會保留您的項目。
    > 
    > 
    
    ![StorSimple 註冊進度](./media/storsimple-configure-and-register-device-gov-u2/HCS_RegistrationProgress-gov-include.png)
13. Hello 裝置完成註冊之後，會出現服務資料加密金鑰。 複製這個金鑰，並將它儲存在安全的位置。 **此金鑰必須與 hello 服務註冊金鑰 tooregister 其他裝置以 hello StorSimple Manager 服務。** 請參閱太[StorSimple 安全性](../articles/storsimple/storsimple-security.md)如需有關這個索引鍵。
    
    ![StorSimple 註冊裝置 7](./media/storsimple-configure-and-register-device-gov-u2/HCS_RegisterYourDevice7_gov-include.png)    
    
    > [!IMPORTANT]
    > toocopy hello 文字從 hello 序列主控台視窗中，只需選取 hello 文字。 接著，您應該就能 toopaste hello 剪貼簿或任何文字編輯器中。
    > 
    > 不要使用 Ctrl + C toocopy hello 服務資料加密金鑰。 使用 Ctrl + C 將導致您 tooexit hello 安裝精靈。 如此一來，不會變更 hello 裝置系統管理員密碼和 hello 裝置將會回復 toohello 預設密碼。
    > 
    > 
14. 結束 hello 序列主控台。
15. 傳回 toohello Azure 政府入口網站，並完成下列步驟的 hello:
    
    1. 按兩下您的 StorSimple Manager 服務 tooaccess hello**快速入門**頁面。
    2. 按一下 [檢視連接的裝置] 。
    3. 在 hello**裝置**頁面上，確認該 hello 裝置已成功連接 toohello 服務查閱 hello 狀態。 hello 裝置狀態應為**線上**。
       
        ![StorSimple 裝置頁面](./media/storsimple-configure-and-register-device-gov-u2/HCS_DeviceOnline-gov-include.png)
       
        如果 hello 裝置狀態是**離線**，等待幾分鐘的 hello 裝置 toocome 線上。
       
        如果 hello 裝置依然為離線狀態後幾分鐘的時間，則您需要確定網路防火牆已設定中所述的 toomake [StorSimple 裝置的網路需求](../articles/storsimple/storsimple-system-requirements.md)。
       
        請確認這供 hello 服務匯流排的 StorSimple Manager 服務的裝置通訊，因此，已針對連出通訊開啟連接埠 9354。

