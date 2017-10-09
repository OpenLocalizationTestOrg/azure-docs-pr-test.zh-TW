<!--author=alkohli last changed: 01/18/2017-->


#### <a name="tooconfigure-and-register-hello-device"></a><span data-ttu-id="07603-101">tooconfigure 和註冊 hello 裝置</span><span class="sxs-lookup"><span data-stu-id="07603-101">tooconfigure and register hello device</span></span>

1. <span data-ttu-id="07603-102">存取您 StorSimple 裝置序列主控台 hello Windows PowerShell 介面。</span><span class="sxs-lookup"><span data-stu-id="07603-102">Access hello Windows PowerShell interface on your StorSimple device serial console.</span></span> <span data-ttu-id="07603-103">請參閱[使用 PuTTY tooconnect toohello 裝置序列主控台](#use-putty-to-connect-to-the-device-serial-console)如需相關指示。</span><span class="sxs-lookup"><span data-stu-id="07603-103">See [Use PuTTY tooconnect toohello device serial console](#use-putty-to-connect-to-the-device-serial-console) for instructions.</span></span> <span data-ttu-id="07603-104">**剛好是確定 toofollow hello 程序，或將不會無法 tooaccess hello 主控台。**</span><span class="sxs-lookup"><span data-stu-id="07603-104">**Be sure toofollow hello procedure exactly or you will not be able tooaccess hello console.**</span></span>

2. <span data-ttu-id="07603-105">在開啟的 hello 工作階段，按**Enter**一個時間 tooget 命令提示字元。</span><span class="sxs-lookup"><span data-stu-id="07603-105">In hello session that opens up, press **Enter** one time tooget a command prompt.</span></span>

3. <span data-ttu-id="07603-106">您將會是您想要為您的裝置 tooset 提示的 toochoose hello 語言。</span><span class="sxs-lookup"><span data-stu-id="07603-106">You will be prompted toochoose hello language that you would like tooset for your device.</span></span> <span data-ttu-id="07603-107">指定 hello 語言，然後按下**Enter**。</span><span class="sxs-lookup"><span data-stu-id="07603-107">Specify hello language, and then press **Enter**.</span></span>

4. <span data-ttu-id="07603-108">在呈現的 hello 序列主控台功能表，選擇選項 1 太**登入的完整存取**。</span><span class="sxs-lookup"><span data-stu-id="07603-108">In hello serial console menu that is presented, choose option 1 too**log in with full access**.</span></span>
     <span data-ttu-id="07603-109">完成步驟 5-12 tooconfigure hello 最小必要的網路設定為您的裝置。</span><span class="sxs-lookup"><span data-stu-id="07603-109">Complete steps 5-12 tooconfigure hello minimum required network settings for your device.</span></span> <span data-ttu-id="07603-110">**這些設定步驟必須 toobe hello 裝置 hello 作用中控制器上執行。**</span><span class="sxs-lookup"><span data-stu-id="07603-110">**These configuration steps need toobe performed on hello active controller of hello device.**</span></span> <span data-ttu-id="07603-111">hello 序列主控台功能表會指出 hello 橫幅訊息中的 hello 控制器狀態。</span><span class="sxs-lookup"><span data-stu-id="07603-111">hello serial console menu indicates hello controller state in hello banner message.</span></span> <span data-ttu-id="07603-112">如果您未連接 toohello 主動控制器，就會中斷連線，並再連線 toohello 作用中控制器。</span><span class="sxs-lookup"><span data-stu-id="07603-112">If you are not connected toohello active controller, disconnect and then connect toohello active controller.</span></span>

5. <span data-ttu-id="07603-113">在 hello 命令提示字元中輸入您的密碼。</span><span class="sxs-lookup"><span data-stu-id="07603-113">At hello command prompt, type your password.</span></span> <span data-ttu-id="07603-114">hello 預設裝置密碼**Password1**。</span><span class="sxs-lookup"><span data-stu-id="07603-114">hello default device password is **Password1**.</span></span>

6. <span data-ttu-id="07603-115">下列命令的型別 hello: `Invoke-HcsSetupWizard`。</span><span class="sxs-lookup"><span data-stu-id="07603-115">Type hello following command: `Invoke-HcsSetupWizard`.</span></span>

7. <span data-ttu-id="07603-116">安裝精靈會出現 toohelp 設定 hello hello 裝置的網路設定。</span><span class="sxs-lookup"><span data-stu-id="07603-116">A setup wizard will appear toohelp you configure hello network settings for hello device.</span></span> <span data-ttu-id="07603-117">提供下列資訊的 hello hello:</span><span class="sxs-lookup"><span data-stu-id="07603-117">Supply hello hello following information:</span></span>
   
   * <span data-ttu-id="07603-118">Hello DATA 0 網路介面的 IP 位址</span><span class="sxs-lookup"><span data-stu-id="07603-118">IP address for hello DATA 0 network interface</span></span>
   * <span data-ttu-id="07603-119">子網路遮罩</span><span class="sxs-lookup"><span data-stu-id="07603-119">Subnet mask</span></span>
   * <span data-ttu-id="07603-120">閘道器</span><span class="sxs-lookup"><span data-stu-id="07603-120">Gateway</span></span>
   * <span data-ttu-id="07603-121">適用於主要 DNS 伺服器的 IP 位址</span><span class="sxs-lookup"><span data-stu-id="07603-121">IP address for Primary DNS server</span></span>

   <span data-ttu-id="07603-122">範例輸出顯示如下。</span><span class="sxs-lookup"><span data-stu-id="07603-122">A sample output is presented below.</span></span>

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
    <span data-ttu-id="07603-123">在 hello 前面範例輸出，您可以看到 hello 系統之後在 hello 程序中的每個步驟驗證網路設定。</span><span class="sxs-lookup"><span data-stu-id="07603-123">In hello preceding sample output, you can see that hello system is validating network settings after each step in hello process.</span></span>

     > [!NOTE]
     > <span data-ttu-id="07603-124">您可能必須 toowait hello 子網路遮罩和套用 hello DNS 設定 toobe 幾分鐘。</span><span class="sxs-lookup"><span data-stu-id="07603-124">You may have toowait for a few minutes for hello subnet mask and hello DNS settings toobe applied.</span></span> <span data-ttu-id="07603-125">如果您收到 「 檢查 hello 網路連線 tooData 0 」 錯誤訊息，請檢查 hello 實體網路連線 hello DATA 0 網路介面在主動控制站。</span><span class="sxs-lookup"><span data-stu-id="07603-125">If you get a "Check hello network connectivity tooData 0" error message, check hello physical network connection on hello DATA 0 network interface of your active controller.</span></span>

8. <span data-ttu-id="07603-126">(選用) 設定 Web Proxy 伺服器。</span><span class="sxs-lookup"><span data-stu-id="07603-126">(Optional) configure your web proxy server.</span></span> <span data-ttu-id="07603-127">雖然 Web Proxy 設定是選用的，但 **請注意，如果您使用 Web Proxy，就只能在此處設定它**。</span><span class="sxs-lookup"><span data-stu-id="07603-127">Although web proxy configuration is optional, **be aware that if you use a web proxy, you can only configure it here**.</span></span> <span data-ttu-id="07603-128">如需詳細資訊，請移至太[設定 web proxy 為您的裝置](../articles/storsimple/storsimple-8000-configure-web-proxy.md)。</span><span class="sxs-lookup"><span data-stu-id="07603-128">For more information, go too[Configure web proxy for your device](../articles/storsimple/storsimple-8000-configure-web-proxy.md).</span></span>
9. <span data-ttu-id="07603-129">為裝置設定主要 NTP 伺服器。</span><span class="sxs-lookup"><span data-stu-id="07603-129">Configure a Primary NTP server for your device.</span></span> <span data-ttu-id="07603-130">NTP 伺服器是必要項目，因為您的裝置必須同步處理時間，才能使用您的雲端服務提供者進行驗證。</span><span class="sxs-lookup"><span data-stu-id="07603-130">NTP servers are required, as your device must synchronize time so that it can authenticate with your cloud service providers.</span></span> <span data-ttu-id="07603-131">請確定您的網路允許 NTP 流量 toopass 從您的資料中心 toohello 網際網路。</span><span class="sxs-lookup"><span data-stu-id="07603-131">Ensure that your network allows NTP traffic toopass from your datacenter toohello Internet.</span></span> <span data-ttu-id="07603-132">如果不可行，請指定內部 NTP 伺服器。</span><span class="sxs-lookup"><span data-stu-id="07603-132">If this is not possible, specify an internal NTP server.</span></span>

    <span data-ttu-id="07603-133">下方顯示一項範例輸出。</span><span class="sxs-lookup"><span data-stu-id="07603-133">A sample output is shown below.</span></span>

    ```
        Would you like tooconfigure a web proxy?
        [Y] Yes [N] No (Default is "N"):N

        Primary NTP server [time.windows.com]:time.windows.com

    ```

10. <span data-ttu-id="07603-134">基於安全性理由，hello 裝置系統管理員密碼過期之後 hello 第一個工作階段，而且您將需要 toochange 現在 it。</span><span class="sxs-lookup"><span data-stu-id="07603-134">For security reasons, hello device administrator password expires after hello first session, and you will need toochange it now.</span></span> <span data-ttu-id="07603-135">出現提示時，請提供裝置系統管理員密碼。</span><span class="sxs-lookup"><span data-stu-id="07603-135">When prompted, provide a device administrator password.</span></span> <span data-ttu-id="07603-136">有效的裝置系統管理員密碼長度必須介於 8 到 15 個字元。</span><span class="sxs-lookup"><span data-stu-id="07603-136">A valid device administrator password must be between 8 and 15 characters.</span></span> <span data-ttu-id="07603-137">hello 密碼必須包含的 hello 下列三種： 小寫字母、 大寫字母、 數字及特殊字元。</span><span class="sxs-lookup"><span data-stu-id="07603-137">hello password must contain three of hello following: lowercase, uppercase, numeric, and special characters.</span></span>

    ```
        hello device administrator password must be between 8 and 15 characters. hello password must contain a combination of uppercase letters, lowercase letters, numbers and special characters.
        Administrator Password:********
        Confirm Administrator Password:********
    ```
11. <span data-ttu-id="07603-138">hello hello 安裝精靈中的最後一個步驟以 hello StorSimple 裝置 Manager 服務註冊您的裝置。</span><span class="sxs-lookup"><span data-stu-id="07603-138">hello final step in hello setup wizard registers your device with hello StorSimple Device Manager service.</span></span> <span data-ttu-id="07603-139">這麼做，您必須使用您在步驟 2 中取得的 hello 服務註冊金鑰。</span><span class="sxs-lookup"><span data-stu-id="07603-139">For this, you will need hello service registration key that you obtained in step 2.</span></span> <span data-ttu-id="07603-140">您提供 hello 註冊金鑰之後，您可能需要 toowait 2-3 分鐘，hello 裝置完成註冊。</span><span class="sxs-lookup"><span data-stu-id="07603-140">After you supply hello registration key, you may need toowait for 2-3 minutes before hello device is registered.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="07603-141">您可以按 Ctrl + C，在任何時間 tooexit hello 安裝精靈。</span><span class="sxs-lookup"><span data-stu-id="07603-141">You can press Ctrl + C at any time tooexit hello setup wizard.</span></span> <span data-ttu-id="07603-142">如果您輸入所有 hello 網路設定 （針對 Data 0、 子網路遮罩和閘道的 IP 位址），則會保留您的項目。</span><span class="sxs-lookup"><span data-stu-id="07603-142">If you have entered all hello network settings (IP address for Data 0, Subnet mask, and Gateway), your entries will be retained.</span></span>
    
    <span data-ttu-id="07603-143">下方顯示一項範例輸出。</span><span class="sxs-lookup"><span data-stu-id="07603-143">A sample output is shown below.</span></span>

    ```
        hello service registration key is available in hello StorSimple Manager service.
        Enter service registration key:**************************************
        Device registration is in progress. Please wait.

    ```

12. <span data-ttu-id="07603-144">Hello 裝置完成註冊之後，會出現服務資料加密金鑰。</span><span class="sxs-lookup"><span data-stu-id="07603-144">After hello device is registered, a Service Data Encryption key will appear.</span></span> <span data-ttu-id="07603-145">複製這個金鑰，並將它儲存在安全的位置。</span><span class="sxs-lookup"><span data-stu-id="07603-145">Copy this key and save it in a safe location.</span></span> <span data-ttu-id="07603-146">**此金鑰必須與 hello 服務註冊金鑰 tooregister 其他裝置以 hello StorSimple 裝置管理員服務。**</span><span class="sxs-lookup"><span data-stu-id="07603-146">**This key will be required with hello service registration key tooregister additional devices with hello StorSimple Device Manager service.**</span></span> <span data-ttu-id="07603-147">請參閱太[StorSimple 安全性](../articles/storsimple/storsimple-security.md)如需有關這個索引鍵。</span><span class="sxs-lookup"><span data-stu-id="07603-147">Refer too[StorSimple security](../articles/storsimple/storsimple-security.md) for more information about this key.</span></span>
    
    ![StorSimple 註冊裝置 7](./media/storsimple-8000-configure-and-register-device-u2/step3pssetup1.png)
    
    > [!NOTE]
    > <span data-ttu-id="07603-149">toocopy hello 文字從 hello 序列主控台視窗中，只需選取 hello 文字。</span><span class="sxs-lookup"><span data-stu-id="07603-149">toocopy hello text from hello serial console window, simply select hello text.</span></span> <span data-ttu-id="07603-150">接著，您應該就能 toopaste hello 剪貼簿或任何文字編輯器中。</span><span class="sxs-lookup"><span data-stu-id="07603-150">You should then be able toopaste it in hello clipboard or any text editor.</span></span> <span data-ttu-id="07603-151">不要使用 Ctrl + C toocopy hello 服務資料加密金鑰。</span><span class="sxs-lookup"><span data-stu-id="07603-151">DO NOT use Ctrl + C toocopy hello service data encryption key.</span></span> <span data-ttu-id="07603-152">使用 Ctrl + C 將導致您 tooexit hello 安裝精靈。</span><span class="sxs-lookup"><span data-stu-id="07603-152">Using Ctrl + C will cause you tooexit hello setup wizard.</span></span> <span data-ttu-id="07603-153">如此一來，不會變更 hello 裝置系統管理員密碼和 hello 裝置將會回復 toohello 預設密碼。</span><span class="sxs-lookup"><span data-stu-id="07603-153">As a result, hello device administrator password will not be changed and hello device will revert toohello default password.</span></span>
    
13. <span data-ttu-id="07603-154">結束 hello 序列主控台。</span><span class="sxs-lookup"><span data-stu-id="07603-154">Exit hello serial console.</span></span>
14. <span data-ttu-id="07603-155">傳回 toohello Azure 入口網站，並完成下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="07603-155">Return toohello Azure portal, and complete hello following steps:</span></span>
    
    1. <span data-ttu-id="07603-156">移 tooyour StorSimple 裝置管理員服務。</span><span class="sxs-lookup"><span data-stu-id="07603-156">Go tooyour StorSimple Device Manager service.</span></span>
    2. <span data-ttu-id="07603-157">按一下 [裝置]。</span><span class="sxs-lookup"><span data-stu-id="07603-157">Click **Devices**.</span></span>
    3. <span data-ttu-id="07603-158">在 hello 表格式的裝置清單，確認該 hello 裝置已成功連接 toohello 服務查閱 hello 狀態。</span><span class="sxs-lookup"><span data-stu-id="07603-158">In hello tabular listing of devices, verify that hello device has successfully connected toohello service by looking up hello status.</span></span> <span data-ttu-id="07603-159">hello 裝置狀態應為**已 tooset 準備註冊**。</span><span class="sxs-lookup"><span data-stu-id="07603-159">hello device status should be **Ready tooset up**.</span></span>
       
        ![StorSimple 裝置頁面](./media/storsimple-8000-configure-and-register-device-u2/step3pssetup2.png)
       
        <span data-ttu-id="07603-161">您可能需要幾分鐘的 hello 裝置狀態 toochange 的 toowait 太**已 tooset 準備註冊**。</span><span class="sxs-lookup"><span data-stu-id="07603-161">You may need toowait for a couple of minutes for hello device status toochange too**Ready tooset up**.</span></span>
       
        <span data-ttu-id="07603-162">如果 hello 裝置不會顯示在此清單中，則您需要確定網路防火牆已設定中所述的 toomake [StorSimple 裝置的網路需求](../articles/storsimple/storsimple-8000-system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="07603-162">If hello device does not show up in this list, then you need toomake sure that your firewall network was configured as described in [networking requirements for your StorSimple device](../articles/storsimple/storsimple-8000-system-requirements.md).</span></span> <span data-ttu-id="07603-163">請確認這供 hello 服務匯流排之 StorSimple 裝置管理員服務-裝置通訊，因此，已針對連出通訊開啟連接埠 9354。</span><span class="sxs-lookup"><span data-stu-id="07603-163">Verify that port 9354 is open for outbound communication as this is used by hello service bus for StorSimple Device Manager service-to-device communication.</span></span>

