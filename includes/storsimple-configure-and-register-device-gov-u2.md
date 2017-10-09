<!--author=SharS last changed: 02/22/2016-->

### <a name="tooconfigure-and-register-hello-device"></a><span data-ttu-id="61b29-101">tooconfigure 和註冊 hello 裝置</span><span class="sxs-lookup"><span data-stu-id="61b29-101">tooconfigure and register hello device</span></span>
1. <span data-ttu-id="61b29-102">存取您 StorSimple 裝置序列主控台 hello Windows PowerShell 介面。</span><span class="sxs-lookup"><span data-stu-id="61b29-102">Access hello Windows PowerShell interface on your StorSimple device serial console.</span></span> <span data-ttu-id="61b29-103">請參閱[使用 PuTTY tooconnect toohello 裝置序列主控台](../articles/storsimple/storsimple-deployment-walkthrough-gov-u2.md#use-putty-to-connect-to-the-device-serial-console)如需相關指示。</span><span class="sxs-lookup"><span data-stu-id="61b29-103">See [Use PuTTY tooconnect toohello device serial console](../articles/storsimple/storsimple-deployment-walkthrough-gov-u2.md#use-putty-to-connect-to-the-device-serial-console) for instructions.</span></span> <span data-ttu-id="61b29-104">**剛好是確定 toofollow hello 程序，或將不會無法 tooaccess hello 主控台。**</span><span class="sxs-lookup"><span data-stu-id="61b29-104">**Be sure toofollow hello procedure exactly or you will not be able tooaccess hello console.**</span></span>
2. <span data-ttu-id="61b29-105">在開啟的 hello 工作階段，按下 Enter 一個時間 tooget 命令提示字元。</span><span class="sxs-lookup"><span data-stu-id="61b29-105">In hello session that opens up, press Enter one time tooget a command prompt.</span></span>
3. <span data-ttu-id="61b29-106">您將會是您想要為您的裝置 tooset 提示的 toochoose hello 語言。</span><span class="sxs-lookup"><span data-stu-id="61b29-106">You will be prompted toochoose hello language that you would like tooset for your device.</span></span> <span data-ttu-id="61b29-107">指定 hello 語言，然後按 Enter 鍵。</span><span class="sxs-lookup"><span data-stu-id="61b29-107">Specify hello language, and then press Enter.</span></span>
   
    ![StorSimple 設定和註冊裝置 1](./media/storsimple-configure-and-register-device-gov-u2/HCS_RegisterYourDevice1-gov-include.png)
4. <span data-ttu-id="61b29-109">在呈現的 hello 序列主控台功能表，選擇選項 1 toolog 上具有完整存取權。</span><span class="sxs-lookup"><span data-stu-id="61b29-109">In hello serial console menu that is presented, choose option 1 toolog on with full access.</span></span>
   
    ![StorSimple 註冊裝置 2](./media/storsimple-configure-and-register-device-gov-u2/HCS_RegisterYourDevice2-gov-include.png)
5. <span data-ttu-id="61b29-111">執行下列步驟 tooconfigure hello 最小必要的網路設定為您的裝置 hello。</span><span class="sxs-lookup"><span data-stu-id="61b29-111">Perform hello following steps tooconfigure hello minimum required network settings for your device.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="61b29-112">這些設定步驟必須 toobe hello 裝置 hello 作用中控制器上執行。</span><span class="sxs-lookup"><span data-stu-id="61b29-112">These configuration steps need toobe performed on hello active controller of hello device.</span></span> <span data-ttu-id="61b29-113">hello 序列主控台功能表會指出 hello 橫幅訊息中的 hello 控制器狀態。</span><span class="sxs-lookup"><span data-stu-id="61b29-113">hello serial console menu indicates hello controller state in hello banner message.</span></span> <span data-ttu-id="61b29-114">如果您不是連接 toohello 作用中控制器，中斷連線，然後連接 toohello 作用中控制器。</span><span class="sxs-lookup"><span data-stu-id="61b29-114">If you are not connect toohello active controller, disconnect and then connect toohello active controller.</span></span>
   > 
   > 
   
   1. <span data-ttu-id="61b29-115">在 hello 命令提示字元中輸入您的密碼。</span><span class="sxs-lookup"><span data-stu-id="61b29-115">At hello command prompt, type your password.</span></span> <span data-ttu-id="61b29-116">hello 預設裝置密碼**Password1**。</span><span class="sxs-lookup"><span data-stu-id="61b29-116">hello default device password is **Password1**.</span></span>
   2. <span data-ttu-id="61b29-117">輸入下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="61b29-117">Type hello following command:</span></span>
      
        `Invoke-HcsSetupWizard`
   3. <span data-ttu-id="61b29-118">安裝精靈會出現 toohelp 設定 hello hello 裝置的網路設定。</span><span class="sxs-lookup"><span data-stu-id="61b29-118">A setup wizard will appear toohelp you configure hello network settings for hello device.</span></span> <span data-ttu-id="61b29-119">提供下列資訊的 hello:</span><span class="sxs-lookup"><span data-stu-id="61b29-119">Supply hello following information:</span></span>
      
      * <span data-ttu-id="61b29-120">適用於 DATA 0 網路介面的 IP 位址</span><span class="sxs-lookup"><span data-stu-id="61b29-120">IP address for DATA 0 network interface</span></span>
      * <span data-ttu-id="61b29-121">子網路遮罩</span><span class="sxs-lookup"><span data-stu-id="61b29-121">Subnet mask</span></span>
      * <span data-ttu-id="61b29-122">閘道器</span><span class="sxs-lookup"><span data-stu-id="61b29-122">Gateway</span></span>
      * <span data-ttu-id="61b29-123">適用於主要 DNS 伺服器的 IP 位址</span><span class="sxs-lookup"><span data-stu-id="61b29-123">IP address for Primary DNS server</span></span>
      * <span data-ttu-id="61b29-124">適用於主要 NTP 伺服器的 IP 位址</span><span class="sxs-lookup"><span data-stu-id="61b29-124">IP address for Primary NTP server</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="61b29-125">您可能必須 toowait hello 子網路遮罩和 DNS 設定 toobe 套用幾分鐘。</span><span class="sxs-lookup"><span data-stu-id="61b29-125">You may have toowait for a few minutes for hello subnet mask and DNS settings toobe applied.</span></span>
      > 
      > 
   4. <span data-ttu-id="61b29-126">選擇性設定 Web Proxy 伺服器。</span><span class="sxs-lookup"><span data-stu-id="61b29-126">Optionally, configure your web proxy server.</span></span>
      
      > [!IMPORTANT]
      > <span data-ttu-id="61b29-127">雖然 Web Proxy 設定是選用的，但請注意，如果您使用 Web Proxy，就只能在此處設定它。</span><span class="sxs-lookup"><span data-stu-id="61b29-127">Although web proxy configuration is optional, be aware that if you use a web proxy, you can only configure it here.</span></span> <span data-ttu-id="61b29-128">如需詳細資訊，請移至太[設定 web proxy 為您的裝置](../articles/storsimple/storsimple-configure-web-proxy.md)。</span><span class="sxs-lookup"><span data-stu-id="61b29-128">For more information, go too[Configure web proxy for your device](../articles/storsimple/storsimple-configure-web-proxy.md).</span></span>
      > 
      > 
6. <span data-ttu-id="61b29-129">按 Ctrl + C tooexit hello 安裝精靈。</span><span class="sxs-lookup"><span data-stu-id="61b29-129">Press Ctrl + C tooexit hello setup wizard.</span></span>
7. <span data-ttu-id="61b29-130">安裝 hello 更新，如下所示：</span><span class="sxs-lookup"><span data-stu-id="61b29-130">Install hello updates as follows:</span></span>
   
   1. <span data-ttu-id="61b29-131">使用下列兩個 hello 控制器上的 cmdlet tooset Ip hello:</span><span class="sxs-lookup"><span data-stu-id="61b29-131">Use hello following cmdlet tooset IPs on both hello controllers:</span></span>
      
      `Set-HcsNetInterface -InterfaceAlias Data0 -Controller0IPv4Address <Controller0 IP> -Controller1IPv4Address <Controller1 IP>`
   2. <span data-ttu-id="61b29-132">在 hello 命令提示字元中執行`Get-HcsUpdateAvailability`。</span><span class="sxs-lookup"><span data-stu-id="61b29-132">At hello command prompt, run `Get-HcsUpdateAvailability`.</span></span> <span data-ttu-id="61b29-133">您應該會在更新可用時收到通知。</span><span class="sxs-lookup"><span data-stu-id="61b29-133">You should be notified that updates are available.</span></span>
   3. <span data-ttu-id="61b29-134">執行 `Start-HcsUpdate`。</span><span class="sxs-lookup"><span data-stu-id="61b29-134">Run `Start-HcsUpdate`.</span></span> <span data-ttu-id="61b29-135">您可以在任何模式中執行此命令。</span><span class="sxs-lookup"><span data-stu-id="61b29-135">You can run this command on any node.</span></span> <span data-ttu-id="61b29-136">將在 hello 第一個控制器上套用更新、 hello 控制器將會容錯移轉，和在套用更新的 hello 然後 hello 另一個控制器。</span><span class="sxs-lookup"><span data-stu-id="61b29-136">Updates will be applied on hello first controller, hello controller will fail over, and then hello updates will be applied on hello other controller.</span></span>
      
      <span data-ttu-id="61b29-137">您可以藉由執行監視 hello hello 更新進度`Get-HcsUpdateStatus`。</span><span class="sxs-lookup"><span data-stu-id="61b29-137">You can monitor hello progress of hello update by running `Get-HcsUpdateStatus`.</span></span>    
      
      <span data-ttu-id="61b29-138">hello 下列範例輸出顯示 hello 更新正在進行中。</span><span class="sxs-lookup"><span data-stu-id="61b29-138">hello following sample output shows hello update in progress.</span></span>
      
      ````
      Controller0>Get-HcsUpdateStatus
      RunInprogress       : True
      LastHotfixTimestamp : 4/13/2015 10:56:13 PM
      LastUpdateTimestamp : 4/13/2015 10:35:25 PM
      Controller0Events   :
      Controller1Events   :
      ````
      
      <span data-ttu-id="61b29-139">下列範例輸出的 hello 指出該 hello 更新已完成。</span><span class="sxs-lookup"><span data-stu-id="61b29-139">hello following sample output indicates that hello update is finished.</span></span>
      
      ```
      Controller1>Get-HcsUpdateStatus
      
      RunInprogress       : False
      LastHotfixTimestamp : 4/13/2015 10:56:13 PM
      LastUpdateTimestamp : 4/13/2015 10:35:25 PM
      Controller0Events   :
      Controller1Events   :
      ```
      
      <span data-ttu-id="61b29-140">它可能會佔用 too11 小時 tooapply 所有 hello 更新，包括 hello Windows 更新。</span><span class="sxs-lookup"><span data-stu-id="61b29-140">It may take up too11 hours tooapply all hello updates, including hello Windows Updates.</span></span>
8. <span data-ttu-id="61b29-141">執行下列 cmdlet toopoint hello 裝置 toohello Microsoft Azure 政府入口網站 （因為它所指 toohello 公用 Azure 傳統入口網站的預設值） 的 hello。</span><span class="sxs-lookup"><span data-stu-id="61b29-141">Run hello following cmdlet toopoint hello device toohello Microsoft Azure Government portal (because it points toohello public Azure classic portal by default).</span></span> <span data-ttu-id="61b29-142">這樣會重新啟動兩個控制器。</span><span class="sxs-lookup"><span data-stu-id="61b29-142">This will restart both controllers.</span></span> <span data-ttu-id="61b29-143">我們建議您使用兩個 toosimultaneously 連接 tooboth 控制站，以便您可以看到每個控制站何時會重新啟動的 PuTTY 工作階段。</span><span class="sxs-lookup"><span data-stu-id="61b29-143">We recommend that you use two PuTTY sessions toosimultaneously connect tooboth controllers so that you can see when each controller is restarted.</span></span>
   
    `Set-CloudPlatform -AzureGovt_US`
   
   <span data-ttu-id="61b29-144">您將會看見確認訊息。</span><span class="sxs-lookup"><span data-stu-id="61b29-144">You will see a confirmation message.</span></span> <span data-ttu-id="61b29-145">接受 hello 預設 (**Y**)。</span><span class="sxs-lookup"><span data-stu-id="61b29-145">Accept hello default (**Y**).</span></span>
9. <span data-ttu-id="61b29-146">執行下列 cmdlet tooresume 安裝 hello:</span><span class="sxs-lookup"><span data-stu-id="61b29-146">Run hello following cmdlet tooresume setup:</span></span>
   
    `Invoke-HcsSetupWizard`
   
    ![繼續設定精靈](./media/storsimple-configure-and-register-device-gov-u2/HCS_ResumeSetup-gov-include.png)
   
   <span data-ttu-id="61b29-148">當您繼續安裝時，hello 精靈將 hello Update 2 的版本。</span><span class="sxs-lookup"><span data-stu-id="61b29-148">When you resume setup, hello wizard will be hello Update 2 version.</span></span>
10. <span data-ttu-id="61b29-149">接受 hello 網路設定。</span><span class="sxs-lookup"><span data-stu-id="61b29-149">Accept hello network settings.</span></span> <span data-ttu-id="61b29-150">在您接受每個設定之後，您會看到驗證訊息。</span><span class="sxs-lookup"><span data-stu-id="61b29-150">You will see a validation message after you accept each setting.</span></span>
11. <span data-ttu-id="61b29-151">基於安全性理由，hello 裝置系統管理員密碼過期之後 hello 第一個工作階段，而且您將需要 toochange 現在 it。</span><span class="sxs-lookup"><span data-stu-id="61b29-151">For security reasons, hello device administrator password expires after hello first session, and you will need toochange it now.</span></span> <span data-ttu-id="61b29-152">出現提示時，請提供裝置系統管理員密碼。</span><span class="sxs-lookup"><span data-stu-id="61b29-152">When prompted, provide a device administrator password.</span></span> <span data-ttu-id="61b29-153">有效的裝置系統管理員密碼長度必須介於 8 到 15 個字元。</span><span class="sxs-lookup"><span data-stu-id="61b29-153">A valid device administrator password must be between 8 and 15 characters.</span></span> <span data-ttu-id="61b29-154">hello 密碼必須包含的 hello 下列三種： 小寫字母、 大寫字母、 數字及特殊字元。</span><span class="sxs-lookup"><span data-stu-id="61b29-154">hello password must contain three of hello following: lowercase, uppercase, numeric, and special characters.</span></span>
    
    <br/>![StorSimple 註冊裝置 5](./media/storsimple-configure-and-register-device-gov-u2/HCS_RegisterYourDevice5_gov-include.png)
12. <span data-ttu-id="61b29-156">hello hello 安裝精靈中的最後一個步驟以 hello StorSimple Manager 服務註冊您的裝置。</span><span class="sxs-lookup"><span data-stu-id="61b29-156">hello final step in hello setup wizard registers your device with hello StorSimple Manager service.</span></span> <span data-ttu-id="61b29-157">這麼做，您將需要 hello 中取得的服務註冊金鑰[步驟 2： 取得 hello 服務註冊金鑰](../articles/storsimple/storsimple-deployment-walkthrough-gov-u2.md#step-2-get-the-service-registration-key)。</span><span class="sxs-lookup"><span data-stu-id="61b29-157">For this, you will need hello service registration key that you obtained in [Step 2: Get hello service registration key](../articles/storsimple/storsimple-deployment-walkthrough-gov-u2.md#step-2-get-the-service-registration-key).</span></span> <span data-ttu-id="61b29-158">您提供 hello 註冊金鑰之後，您可能需要 toowait 2-3 分鐘，hello 裝置完成註冊。</span><span class="sxs-lookup"><span data-stu-id="61b29-158">After you supply hello registration key, you may need toowait for 2-3 minutes before hello device is registered.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="61b29-159">您可以按 Ctrl + C，在任何時間 tooexit hello 安裝精靈。</span><span class="sxs-lookup"><span data-stu-id="61b29-159">You can press Ctrl + C at any time tooexit hello setup wizard.</span></span> <span data-ttu-id="61b29-160">如果您輸入所有 hello 網路設定 （針對 Data 0、 子網路遮罩和閘道的 IP 位址），則會保留您的項目。</span><span class="sxs-lookup"><span data-stu-id="61b29-160">If you have entered all hello network settings (IP address for Data 0, Subnet mask, and Gateway), your entries will be retained.</span></span>
    > 
    > 
    
    ![StorSimple 註冊進度](./media/storsimple-configure-and-register-device-gov-u2/HCS_RegistrationProgress-gov-include.png)
13. <span data-ttu-id="61b29-162">Hello 裝置完成註冊之後，會出現服務資料加密金鑰。</span><span class="sxs-lookup"><span data-stu-id="61b29-162">After hello device is registered, a Service Data Encryption key will appear.</span></span> <span data-ttu-id="61b29-163">複製這個金鑰，並將它儲存在安全的位置。</span><span class="sxs-lookup"><span data-stu-id="61b29-163">Copy this key and save it in a safe location.</span></span> <span data-ttu-id="61b29-164">**此金鑰必須與 hello 服務註冊金鑰 tooregister 其他裝置以 hello StorSimple Manager 服務。**</span><span class="sxs-lookup"><span data-stu-id="61b29-164">**This key will be required with hello service registration key tooregister additional devices with hello StorSimple Manager service.**</span></span> <span data-ttu-id="61b29-165">請參閱太[StorSimple 安全性](../articles/storsimple/storsimple-security.md)如需有關這個索引鍵。</span><span class="sxs-lookup"><span data-stu-id="61b29-165">Refer too[StorSimple security](../articles/storsimple/storsimple-security.md) for more information about this key.</span></span>
    
    ![StorSimple 註冊裝置 7](./media/storsimple-configure-and-register-device-gov-u2/HCS_RegisterYourDevice7_gov-include.png)    
    
    > [!IMPORTANT]
    > <span data-ttu-id="61b29-167">toocopy hello 文字從 hello 序列主控台視窗中，只需選取 hello 文字。</span><span class="sxs-lookup"><span data-stu-id="61b29-167">toocopy hello text from hello serial console window, simply select hello text.</span></span> <span data-ttu-id="61b29-168">接著，您應該就能 toopaste hello 剪貼簿或任何文字編輯器中。</span><span class="sxs-lookup"><span data-stu-id="61b29-168">You should then be able toopaste it in hello clipboard or any text editor.</span></span>
    > 
    > <span data-ttu-id="61b29-169">不要使用 Ctrl + C toocopy hello 服務資料加密金鑰。</span><span class="sxs-lookup"><span data-stu-id="61b29-169">DO NOT use Ctrl + C toocopy hello service data encryption key.</span></span> <span data-ttu-id="61b29-170">使用 Ctrl + C 將導致您 tooexit hello 安裝精靈。</span><span class="sxs-lookup"><span data-stu-id="61b29-170">Using Ctrl + C will cause you tooexit hello setup wizard.</span></span> <span data-ttu-id="61b29-171">如此一來，不會變更 hello 裝置系統管理員密碼和 hello 裝置將會回復 toohello 預設密碼。</span><span class="sxs-lookup"><span data-stu-id="61b29-171">As a result, hello device administrator password will not be changed and hello device will revert toohello default password.</span></span>
    > 
    > 
14. <span data-ttu-id="61b29-172">結束 hello 序列主控台。</span><span class="sxs-lookup"><span data-stu-id="61b29-172">Exit hello serial console.</span></span>
15. <span data-ttu-id="61b29-173">傳回 toohello Azure 政府入口網站，並完成下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="61b29-173">Return toohello Azure Government Portal, and complete hello following steps:</span></span>
    
    1. <span data-ttu-id="61b29-174">按兩下您的 StorSimple Manager 服務 tooaccess hello**快速入門**頁面。</span><span class="sxs-lookup"><span data-stu-id="61b29-174">Double-click your StorSimple Manager service tooaccess hello **Quick Start** page.</span></span>
    2. <span data-ttu-id="61b29-175">按一下 [檢視連接的裝置] 。</span><span class="sxs-lookup"><span data-stu-id="61b29-175">Click **View connected devices**.</span></span>
    3. <span data-ttu-id="61b29-176">在 hello**裝置**頁面上，確認該 hello 裝置已成功連接 toohello 服務查閱 hello 狀態。</span><span class="sxs-lookup"><span data-stu-id="61b29-176">On hello **Devices** page, verify that hello device has successfully connected toohello service by looking up hello status.</span></span> <span data-ttu-id="61b29-177">hello 裝置狀態應為**線上**。</span><span class="sxs-lookup"><span data-stu-id="61b29-177">hello device status should be **Online**.</span></span>
       
        ![StorSimple 裝置頁面](./media/storsimple-configure-and-register-device-gov-u2/HCS_DeviceOnline-gov-include.png)
       
        <span data-ttu-id="61b29-179">如果 hello 裝置狀態是**離線**，等待幾分鐘的 hello 裝置 toocome 線上。</span><span class="sxs-lookup"><span data-stu-id="61b29-179">If hello device status is **Offline**, wait for a couple of minutes for hello device toocome online.</span></span>
       
        <span data-ttu-id="61b29-180">如果 hello 裝置依然為離線狀態後幾分鐘的時間，則您需要確定網路防火牆已設定中所述的 toomake [StorSimple 裝置的網路需求](../articles/storsimple/storsimple-system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="61b29-180">If hello device is still offline after a few minutes, then you need toomake sure that your firewall network was configured as described in [networking requirements for your StorSimple device](../articles/storsimple/storsimple-system-requirements.md).</span></span>
       
        <span data-ttu-id="61b29-181">請確認這供 hello 服務匯流排的 StorSimple Manager 服務的裝置通訊，因此，已針對連出通訊開啟連接埠 9354。</span><span class="sxs-lookup"><span data-stu-id="61b29-181">Verify that port 9354 is open for outbound communication as this is used by hello service bus for StorSimple Manager Service-to-device communication.</span></span>

