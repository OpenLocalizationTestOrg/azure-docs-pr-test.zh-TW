<!--author=alkohli last changed: 01/18/2017-->


#### <a name="tooconfigure-and-register-hello-device"></a>tooconfigure 和註冊 hello 裝置

1. 存取您 StorSimple 裝置序列主控台 hello Windows PowerShell 介面。 請參閱[使用 PuTTY tooconnect toohello 裝置序列主控台](#use-putty-to-connect-to-the-device-serial-console)如需相關指示。 **剛好是確定 toofollow hello 程序，或將不會無法 tooaccess hello 主控台。**

2. 在開啟的 hello 工作階段，按**Enter**一個時間 tooget 命令提示字元。

3. 您將會是您想要為您的裝置 tooset 提示的 toochoose hello 語言。 指定 hello 語言，然後按下**Enter**。

4. 在呈現的 hello 序列主控台功能表，選擇選項 1 太**登入的完整存取**。
     完成步驟 5-12 tooconfigure hello 最小必要的網路設定為您的裝置。 **這些設定步驟必須 toobe hello 裝置 hello 作用中控制器上執行。** hello 序列主控台功能表會指出 hello 橫幅訊息中的 hello 控制器狀態。 如果您未連接 toohello 主動控制器，就會中斷連線，並再連線 toohello 作用中控制器。

5. 在 hello 命令提示字元中輸入您的密碼。 hello 預設裝置密碼**Password1**。

6. 下列命令的型別 hello: `Invoke-HcsSetupWizard`。

7. 安裝精靈會出現 toohelp 設定 hello hello 裝置的網路設定。 提供下列資訊的 hello hello:
   
   * Hello DATA 0 網路介面的 IP 位址
   * 子網路遮罩
   * 閘道器
   * 適用於主要 DNS 伺服器的 IP 位址

   範例輸出顯示如下。

    ```
        ---------------------------------------------------------------
        Microsoft Azure StorSimple Appliance Model 8100
        Name: 8100-SHX0991003G44MT
        Software Version: 6.3.9600.17759
        Copyright (C) 2014 Microsoft Corporation. All rights reserved.
        You are connected tooController0 - Active
        ---------------------------------------------------------------

        Your device needs toobe registered with hello Microsoft Azure StorSimple Manager service. Please run 'Invoke-HcsSetupWizard' tooset up your device.

        Controller0>Invoke-HcsSetupWizard

        Which IP address family would you like tooconfigure on interface Data0?
        [4] IPv4 [6] IPv6 [B] Both (Default is "4"): 4

        Data0 IPv4 address:10.111.111.00
        Data0 IPv4 subnet: 255.255.252.0
        Data0 IPv4 gateway: 10.111.111.11

        IPv4 primary DNS server [10.222.118.154]:10.222.222.111
    ```

    <br>
    在 hello 前面範例輸出，您可以看到 hello 系統之後在 hello 程序中的每個步驟驗證網路設定。

     > [!NOTE]
     > 您可能必須 toowait hello 子網路遮罩和套用 hello DNS 設定 toobe 幾分鐘。 如果您收到 「 檢查 hello 網路連線 tooData 0 」 錯誤訊息，請檢查 hello 實體網路連線 hello DATA 0 網路介面在主動控制站。

8. (選用) 設定 Web Proxy 伺服器。 雖然 Web Proxy 設定是選用的，但 **請注意，如果您使用 Web Proxy，就只能在此處設定它**。 如需詳細資訊，請移至太[設定 web proxy 為您的裝置](../articles/storsimple/storsimple-8000-configure-web-proxy.md)。
9. 為裝置設定主要 NTP 伺服器。 NTP 伺服器是必要項目，因為您的裝置必須同步處理時間，才能使用您的雲端服務提供者進行驗證。 請確定您的網路允許 NTP 流量 toopass 從您的資料中心 toohello 網際網路。 如果不可行，請指定內部 NTP 伺服器。

    下方顯示一項範例輸出。

    ```
        Would you like tooconfigure a web proxy?
        [Y] Yes [N] No (Default is "N"):N

        Primary NTP server [time.windows.com]:time.windows.com

    ```

10. 基於安全性理由，hello 裝置系統管理員密碼過期之後 hello 第一個工作階段，而且您將需要 toochange 現在 it。 出現提示時，請提供裝置系統管理員密碼。 有效的裝置系統管理員密碼長度必須介於 8 到 15 個字元。 hello 密碼必須包含的 hello 下列三種： 小寫字母、 大寫字母、 數字及特殊字元。

    ```
        hello device administrator password must be between 8 and 15 characters. hello password must contain a combination of uppercase letters, lowercase letters, numbers and special characters.
        Administrator Password:********
        Confirm Administrator Password:********
    ```
11. hello hello 安裝精靈中的最後一個步驟以 hello StorSimple 裝置 Manager 服務註冊您的裝置。 這麼做，您必須使用您在步驟 2 中取得的 hello 服務註冊金鑰。 您提供 hello 註冊金鑰之後，您可能需要 toowait 2-3 分鐘，hello 裝置完成註冊。
    
    > [!NOTE]
    > 您可以按 Ctrl + C，在任何時間 tooexit hello 安裝精靈。 如果您輸入所有 hello 網路設定 （針對 Data 0、 子網路遮罩和閘道的 IP 位址），則會保留您的項目。
    
    下方顯示一項範例輸出。

    ```
        hello service registration key is available in hello StorSimple Manager service.
        Enter service registration key:**************************************
        Device registration is in progress. Please wait.

    ```

12. Hello 裝置完成註冊之後，會出現服務資料加密金鑰。 複製這個金鑰，並將它儲存在安全的位置。 **此金鑰必須與 hello 服務註冊金鑰 tooregister 其他裝置以 hello StorSimple 裝置管理員服務。** 請參閱太[StorSimple 安全性](../articles/storsimple/storsimple-security.md)如需有關這個索引鍵。
    
    ![StorSimple 註冊裝置 7](./media/storsimple-8000-configure-and-register-device-u2/step3pssetup1.png)
    
    > [!NOTE]
    > toocopy hello 文字從 hello 序列主控台視窗中，只需選取 hello 文字。 接著，您應該就能 toopaste hello 剪貼簿或任何文字編輯器中。 不要使用 Ctrl + C toocopy hello 服務資料加密金鑰。 使用 Ctrl + C 將導致您 tooexit hello 安裝精靈。 如此一來，不會變更 hello 裝置系統管理員密碼和 hello 裝置將會回復 toohello 預設密碼。
    
13. 結束 hello 序列主控台。
14. 傳回 toohello Azure 入口網站，並完成下列步驟的 hello:
    
    1. 移 tooyour StorSimple 裝置管理員服務。
    2. 按一下 [裝置]。
    3. 在 hello 表格式的裝置清單，確認該 hello 裝置已成功連接 toohello 服務查閱 hello 狀態。 hello 裝置狀態應為**已 tooset 準備註冊**。
       
        ![StorSimple 裝置頁面](./media/storsimple-8000-configure-and-register-device-u2/step3pssetup2.png)
       
        您可能需要幾分鐘的 hello 裝置狀態 toochange 的 toowait 太**已 tooset 準備註冊**。
       
        如果 hello 裝置不會顯示在此清單中，則您需要確定網路防火牆已設定中所述的 toomake [StorSimple 裝置的網路需求](../articles/storsimple/storsimple-8000-system-requirements.md)。 請確認這供 hello 服務匯流排之 StorSimple 裝置管理員服務-裝置通訊，因此，已針對連出通訊開啟連接埠 9354。

