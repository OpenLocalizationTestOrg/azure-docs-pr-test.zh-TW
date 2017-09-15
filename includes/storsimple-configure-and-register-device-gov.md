<!--author=SharS last changed: 02/22/16-->

### <a name="to-configure-and-register-the-device"></a><span data-ttu-id="77287-101">設定和註冊裝置</span><span class="sxs-lookup"><span data-stu-id="77287-101">To configure and register the device</span></span>
1. <span data-ttu-id="77287-102">存取 StorSimple 裝置序列主控台上的 Windows PowerShell 介面。</span><span class="sxs-lookup"><span data-stu-id="77287-102">Access the Windows PowerShell interface on your StorSimple device serial console.</span></span> <span data-ttu-id="77287-103">如需相關指示，請參閱 [使用 PuTTY 來連接至裝置序列主控台](#use-putty-to-connect-to-the-device-serial-console) 。</span><span class="sxs-lookup"><span data-stu-id="77287-103">See [Use PuTTY to connect to the device serial console](#use-putty-to-connect-to-the-device-serial-console) for instructions.</span></span> <span data-ttu-id="77287-104">**請務必確實依照此程序，否則將無法存取主控台。**</span><span class="sxs-lookup"><span data-stu-id="77287-104">**Be sure to follow the procedure exactly or you will not be able to access the console.**</span></span>
2. <span data-ttu-id="77287-105">在開啟的工作階段中，按 Enter 鍵一次以取得命令提示字元。</span><span class="sxs-lookup"><span data-stu-id="77287-105">In the session that opens up, press Enter one time to get a command prompt.</span></span> 
3. <span data-ttu-id="77287-106">系統將提示您選擇想要為裝置設定的語言。</span><span class="sxs-lookup"><span data-stu-id="77287-106">You will be prompted to choose the language that you would like to set for your device.</span></span> <span data-ttu-id="77287-107">指定語言，然後按 Enter 鍵。</span><span class="sxs-lookup"><span data-stu-id="77287-107">Specify the language, and then press Enter.</span></span> 
   
    ![StorSimple 設定和註冊裝置 1](./media/storsimple-configure-and-register-device-gov/HCS_RegisterYourDevice1-gov-include.png)
4. <span data-ttu-id="77287-109">在顯示的序列主控台功能表中，選擇選項 1 以使用完整存取權進行登入。</span><span class="sxs-lookup"><span data-stu-id="77287-109">In the serial console menu that is presented, choose option 1 to log on with full access.</span></span> 
   
    ![StorSimple 註冊裝置 2](./media/storsimple-configure-and-register-device-gov/HCS_RegisterYourDevice2-gov-include.png)
5. <span data-ttu-id="77287-111">執行下列步驟，為裝置設定最小的必要網路設定。</span><span class="sxs-lookup"><span data-stu-id="77287-111">Perform the following steps to configure the minimum required network settings for your device.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="77287-112">這些設定步驟必須在裝置的主動控制器上執行。</span><span class="sxs-lookup"><span data-stu-id="77287-112">These configuration steps need to be performed on the active controller of the device.</span></span> <span data-ttu-id="77287-113">序列主控台功能表會在橫幅訊息中指出控制站狀態。</span><span class="sxs-lookup"><span data-stu-id="77287-113">The serial console menu indicates the controller state in the banner message.</span></span> <span data-ttu-id="77287-114">如果您未連接到主動控制器，請中斷連線，然後連接到主動控制器。</span><span class="sxs-lookup"><span data-stu-id="77287-114">If you are not connect to the active controller, disconnect and then connect to the active controller.</span></span>
   > 
   > 
   
   1. <span data-ttu-id="77287-115">在命令提示字元中，輸入您的密碼。</span><span class="sxs-lookup"><span data-stu-id="77287-115">At the command prompt, type your password.</span></span> <span data-ttu-id="77287-116">預設裝置密碼是 **Password1**。</span><span class="sxs-lookup"><span data-stu-id="77287-116">The default device password is **Password1**.</span></span>
   2. <span data-ttu-id="77287-117">輸入以下命令：</span><span class="sxs-lookup"><span data-stu-id="77287-117">Type the following command:</span></span>
      
        `Invoke-HcsSetupWizard`
   3. <span data-ttu-id="77287-118">安裝精靈將協助您設定裝置的網路設定。</span><span class="sxs-lookup"><span data-stu-id="77287-118">A setup wizard will appear to help you configure the network settings for the device.</span></span> <span data-ttu-id="77287-119">請提供下列資訊：</span><span class="sxs-lookup"><span data-stu-id="77287-119">Supply the following information:</span></span> 
      
      * <span data-ttu-id="77287-120">適用於 DATA 0 網路介面的 IP 位址</span><span class="sxs-lookup"><span data-stu-id="77287-120">IP address for DATA 0 network interface</span></span>
      * <span data-ttu-id="77287-121">子網路遮罩</span><span class="sxs-lookup"><span data-stu-id="77287-121">Subnet mask</span></span>
      * <span data-ttu-id="77287-122">閘道器</span><span class="sxs-lookup"><span data-stu-id="77287-122">Gateway</span></span>
      * <span data-ttu-id="77287-123">適用於主要 DNS 伺服器的 IP 位址</span><span class="sxs-lookup"><span data-stu-id="77287-123">IP address for Primary DNS server</span></span>
      * <span data-ttu-id="77287-124">適用於主要 NTP 伺服器的 IP 位址</span><span class="sxs-lookup"><span data-stu-id="77287-124">IP address for Primary NTP server</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="77287-125">您可能需要等候幾分鐘，以套用子網路遮罩和 DNS 設定。</span><span class="sxs-lookup"><span data-stu-id="77287-125">You may have to wait for a few minutes for the subnet mask and DNS settings to be applied.</span></span> 
      > 
      > 
   4. <span data-ttu-id="77287-126">選擇性設定 Web Proxy 伺服器。</span><span class="sxs-lookup"><span data-stu-id="77287-126">Optionally, configure your web proxy server.</span></span>
      
      > [!IMPORTANT]
      > <span data-ttu-id="77287-127">雖然 Web Proxy 設定是選用的，但請注意，如果您使用 Web Proxy，就只能在此處設定它。</span><span class="sxs-lookup"><span data-stu-id="77287-127">Although web proxy configuration is optional, be aware that if you use a web proxy, you can only configure it here.</span></span> <span data-ttu-id="77287-128">如需詳細資訊，請參閱 [設定裝置的 Web Proxy](../articles/storsimple/storsimple-configure-web-proxy.md)。</span><span class="sxs-lookup"><span data-stu-id="77287-128">For more information, go to [Configure web proxy for your device](../articles/storsimple/storsimple-configure-web-proxy.md).</span></span> 
      > 
      > 
6. <span data-ttu-id="77287-129">按 Ctrl + C 來結束安裝精靈。</span><span class="sxs-lookup"><span data-stu-id="77287-129">Press Ctrl + C to exit the setup wizard.</span></span>
7. <span data-ttu-id="77287-130">安裝更新，如下所示：</span><span class="sxs-lookup"><span data-stu-id="77287-130">Install the updates as follows:</span></span>
   
   1. <span data-ttu-id="77287-131">使用下列 Cmdlet 在兩個控制器上設定 IP：</span><span class="sxs-lookup"><span data-stu-id="77287-131">Use the following cmdlet to set IPs on both the controllers:</span></span>
      
      `Set-HcsNetInterface -InterfaceAlias Data0 -Controller0IPv4Address <Controller0 IP> -Controller1IPv4Address <Controller1 IP>`
   2. <span data-ttu-id="77287-132">在命令提示字元下，執行 `Get-HcsUpdateAvailability`。</span><span class="sxs-lookup"><span data-stu-id="77287-132">At the command prompt, run `Get-HcsUpdateAvailability`.</span></span> <span data-ttu-id="77287-133">您應該會在更新可用時收到通知。</span><span class="sxs-lookup"><span data-stu-id="77287-133">You should be notified that updates are available.</span></span>
   3. <span data-ttu-id="77287-134">執行 `Start-HcsUpdate`。</span><span class="sxs-lookup"><span data-stu-id="77287-134">Run `Start-HcsUpdate`.</span></span> <span data-ttu-id="77287-135">您可以在任何模式中執行此命令。</span><span class="sxs-lookup"><span data-stu-id="77287-135">You can run this command on any node.</span></span> <span data-ttu-id="77287-136">更新會套用至第一個控制器，控制器會容錯移轉，然後更新會套用至其他控制器。</span><span class="sxs-lookup"><span data-stu-id="77287-136">Updates will be applied on the first controller, the controller will fail over, and then the updates will be applied on the other controller.</span></span>
      
      <span data-ttu-id="77287-137">您可以執行 `Get-HcsUpdateStatus` 以監視更新進度。</span><span class="sxs-lookup"><span data-stu-id="77287-137">You can monitor the progress of the update by running `Get-HcsUpdateStatus`.</span></span>    
      
      <span data-ttu-id="77287-138">下列範例輸出顯示更新進行中。</span><span class="sxs-lookup"><span data-stu-id="77287-138">The following sample output shows the update in progress.</span></span>
      
      ````
      Controller0>Get-HcsUpdateStatus
      RunInprogress       : True
      LastHotfixTimestamp : 4/13/2015 10:56:13 PM
      LastUpdateTimestamp : 4/13/2015 10:35:25 PM
      Controller0Events   :
      Controller1Events   : 
      ````
      
      <span data-ttu-id="77287-139">下列範例輸出指出更新已完成。</span><span class="sxs-lookup"><span data-stu-id="77287-139">The following sample output indicates that the update is finished.</span></span>
      
      ````
      Controller1>Get-HcsUpdateStatus
      
      RunInprogress       : False
      LastHotfixTimestamp : 4/13/2015 10:56:13 PM
      LastUpdateTimestamp : 4/13/2015 10:35:25 PM
      Controller0Events   :
      Controller1Events   :
      
      ````
      
      <span data-ttu-id="77287-140">可能需要多達 11 個小時來套用所有更新，包括 Windows Updates。</span><span class="sxs-lookup"><span data-stu-id="77287-140">It may take up to 11 hours to apply all the updates, including the Windows Updates.</span></span>

8. <span data-ttu-id="77287-141">已成功安裝所有更新之後，執行下列 Cmdlet，確認已正確套用軟體更新：</span><span class="sxs-lookup"><span data-stu-id="77287-141">After all the updates are successfully installed, run the following cmdlet to confirm that the software updates were applied correctly:</span></span>
   
     `Get-HcsSystem`
   
    <span data-ttu-id="77287-142">您應該會看見下列版本：</span><span class="sxs-lookup"><span data-stu-id="77287-142">You should see the following versions:</span></span>
   
   * <span data-ttu-id="77287-143">HcsSoftwareVersion：6.3.9600.17491</span><span class="sxs-lookup"><span data-stu-id="77287-143">HcsSoftwareVersion: 6.3.9600.17491</span></span>
   * <span data-ttu-id="77287-144">CisAgentVersion：1.0.9037.0</span><span class="sxs-lookup"><span data-stu-id="77287-144">CisAgentVersion: 1.0.9037.0</span></span>
   * <span data-ttu-id="77287-145">MdsAgentVersion：26.0.4696.1433</span><span class="sxs-lookup"><span data-stu-id="77287-145">MdsAgentVersion: 26.0.4696.1433</span></span>
9. <span data-ttu-id="77287-146">執行下列 Cmdlet 以確認已正確套用韌體更新：</span><span class="sxs-lookup"><span data-stu-id="77287-146">Run the following cmdlet to confirm that the firmware update was applied correctly:</span></span>
   
    <span data-ttu-id="77287-147">`Start-HcsFirmwareCheck`。</span><span class="sxs-lookup"><span data-stu-id="77287-147">`Start-HcsFirmwareCheck`.</span></span>
   
     <span data-ttu-id="77287-148">韌體狀態應該是 **UpToDate**。</span><span class="sxs-lookup"><span data-stu-id="77287-148">The firmware status should be **UpToDate**.</span></span>
10. <span data-ttu-id="77287-149">執行下列 Cmdlet，將裝置指向 Microsoft Azure Government 入口網站 (因為預設指向公用 Azure 傳統入口網站)。</span><span class="sxs-lookup"><span data-stu-id="77287-149">Run the following cmdlet to point the device to the Microsoft Azure Government portal (because it points to the public Azure classic portal by default).</span></span> <span data-ttu-id="77287-150">這樣會重新啟動兩個控制器。</span><span class="sxs-lookup"><span data-stu-id="77287-150">This will restart both controllers.</span></span> <span data-ttu-id="77287-151">建議您使用兩個 PuTTY 工作階段以同時連線至兩個控制器，這樣您就可以看見每個控制器是何時重新啟動。</span><span class="sxs-lookup"><span data-stu-id="77287-151">We recommend that you use two PuTTY sessions to simultaneously connect to both controllers so that you can see when each controller is restarted.</span></span>
    
     `Set-CloudPlatform -AzureGovt_US`
    
    <span data-ttu-id="77287-152">您將會看見確認訊息。</span><span class="sxs-lookup"><span data-stu-id="77287-152">You will see a confirmation message.</span></span> <span data-ttu-id="77287-153">接受預設值 (**Y**)。</span><span class="sxs-lookup"><span data-stu-id="77287-153">Accept the default (**Y**).</span></span>
11. <span data-ttu-id="77287-154">執行下列 Cmdlet 以繼續設定：</span><span class="sxs-lookup"><span data-stu-id="77287-154">Run the following cmdlet to resume setup:</span></span>
    
     `Invoke-HcsSetupWizard`
    
     ![繼續設定精靈](./media/storsimple-configure-and-register-device-gov/HCS_ResumeSetup-gov-include.png)
    
    <span data-ttu-id="77287-156">當您繼續設定時，精靈會是 Update 1 版本 (其對應至版本 17469)。</span><span class="sxs-lookup"><span data-stu-id="77287-156">When you resume setup, the wizard will be the Update 1 version (which corresponds to version 17469).</span></span> 
12. <span data-ttu-id="77287-157">接受網路設定。</span><span class="sxs-lookup"><span data-stu-id="77287-157">Accept the network settings.</span></span> <span data-ttu-id="77287-158">在您接受每個設定之後，您會看到驗證訊息。</span><span class="sxs-lookup"><span data-stu-id="77287-158">You will see a validation message after you accept each setting.</span></span>
13. <span data-ttu-id="77287-159">基於安全性理由，裝置系統管理員密碼會在第一個工作階段之後過期，您必須立即變更。</span><span class="sxs-lookup"><span data-stu-id="77287-159">For security reasons, the device administrator password expires after the first session, and you will need to change it now.</span></span> <span data-ttu-id="77287-160">出現提示時，請提供裝置系統管理員密碼。</span><span class="sxs-lookup"><span data-stu-id="77287-160">When prompted, provide a device administrator password.</span></span> <span data-ttu-id="77287-161">有效的裝置系統管理員密碼長度必須介於 8 到 15 個字元。</span><span class="sxs-lookup"><span data-stu-id="77287-161">A valid device administrator password must be between 8 and 15 characters.</span></span> <span data-ttu-id="77287-162">密碼必須包含下列其中三項：大寫、小寫、數字和特殊字元。</span><span class="sxs-lookup"><span data-stu-id="77287-162">The password must contain three of the following: lowercase, uppercase, numeric, and special characters.</span></span>
    
    <br/>![StorSimple 註冊裝置 5](./media/storsimple-configure-and-register-device-gov/HCS_RegisterYourDevice5_gov-include.png)
14. <span data-ttu-id="77287-164">安裝精靈的最後一個步驟是向 StorSimple Manager 服務註冊您的裝置。</span><span class="sxs-lookup"><span data-stu-id="77287-164">The final step in the setup wizard registers your device with the StorSimple Manager service.</span></span> <span data-ttu-id="77287-165">基於此因素，您需要在[步驟 2：取得服務註冊金鑰中取得的服務註冊金鑰](#step-2-get-the-service-registration-key)。</span><span class="sxs-lookup"><span data-stu-id="77287-165">For this, you will need the service registration key that you obtained in [Step 2: Get the service registration key](#step-2-get-the-service-registration-key).</span></span> <span data-ttu-id="77287-166">提供註冊金鑰之後，您可能需要等待 2-3 分鐘，才能註冊裝置。</span><span class="sxs-lookup"><span data-stu-id="77287-166">After you supply the registration key, you may need to wait for 2-3 minutes before the device is registered.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="77287-167">您可以隨時按 Ctrl + C 來結束安裝精靈。</span><span class="sxs-lookup"><span data-stu-id="77287-167">You can press Ctrl + C at any time to exit the setup wizard.</span></span> <span data-ttu-id="77287-168">如果您輸入所有網路設定 (Data 0 的 IP 位址、子網路遮罩和閘道器)，則會保留您的項目。</span><span class="sxs-lookup"><span data-stu-id="77287-168">If you have entered all the network settings (IP address for Data 0, Subnet mask, and Gateway), your entries will be retained.</span></span>
    > 
    > 
    
    ![StorSimple 註冊進度](./media/storsimple-configure-and-register-device-gov/HCS_RegistrationProgress-gov-include.png)
15. <span data-ttu-id="77287-170">註冊裝置之後，隨即會出現服務資料加密金鑰。</span><span class="sxs-lookup"><span data-stu-id="77287-170">After the device is registered, a Service Data Encryption key will appear.</span></span> <span data-ttu-id="77287-171">複製這個金鑰，並將它儲存在安全的位置。</span><span class="sxs-lookup"><span data-stu-id="77287-171">Copy this key and save it in a safe location.</span></span> <span data-ttu-id="77287-172">**這個金鑰需要與服務註冊金鑰搭配使用，來向 StorSimple Manager 服務註冊其他裝置。**</span><span class="sxs-lookup"><span data-stu-id="77287-172">**This key will be required with the service registration key to register additional devices with the StorSimple Manager service.**</span></span> <span data-ttu-id="77287-173">如需這個金鑰的詳細資訊，請參閱 [StorSimple 安全性](../articles/storsimple/storsimple-security.md) 。</span><span class="sxs-lookup"><span data-stu-id="77287-173">Refer to [StorSimple security](../articles/storsimple/storsimple-security.md) for more information about this key.</span></span>
    
    ![StorSimple 註冊裝置 7](./media/storsimple-configure-and-register-device-gov/HCS_RegisterYourDevice7_gov-include.png)    
    
    > [!IMPORTANT]
    > <span data-ttu-id="77287-175">若要從序列主控台視窗複製文字，只需選取該文字。</span><span class="sxs-lookup"><span data-stu-id="77287-175">To copy the text from the serial console window, simply select the text.</span></span> <span data-ttu-id="77287-176">然後您應該能夠將它貼到剪貼簿或任何文字編輯器中。</span><span class="sxs-lookup"><span data-stu-id="77287-176">You should then be able to paste it in the clipboard or any text editor.</span></span> 
    > 
    > <span data-ttu-id="77287-177">請勿使用 Ctrl + C 來複製服務資料加密金鑰。</span><span class="sxs-lookup"><span data-stu-id="77287-177">DO NOT use Ctrl + C to copy the service data encryption key.</span></span> <span data-ttu-id="77287-178">使用 Ctrl + C 將導致安裝精靈結束。</span><span class="sxs-lookup"><span data-stu-id="77287-178">Using Ctrl + C will cause you to exit the setup wizard.</span></span> <span data-ttu-id="77287-179">如此一來，裝置系統管理員密碼將不會變更，而裝置將還原為預設密碼。</span><span class="sxs-lookup"><span data-stu-id="77287-179">As a result, the device administrator password will not be changed and the device will revert to the default password.</span></span>
    > 
    > 
16. <span data-ttu-id="77287-180">結束序列主控台。</span><span class="sxs-lookup"><span data-stu-id="77287-180">Exit the serial console.</span></span>
17. <span data-ttu-id="77287-181">返回 Azure Government 入口網站，並完成下列步驟：</span><span class="sxs-lookup"><span data-stu-id="77287-181">Return to the Azure Government Portal, and complete the following steps:</span></span>
    
    1. <span data-ttu-id="77287-182">按兩下 StorSimple Manager 服務以存取 [快速入門]  頁面。</span><span class="sxs-lookup"><span data-stu-id="77287-182">Double-click your StorSimple Manager service to access the **Quick Start** page.</span></span>
    2. <span data-ttu-id="77287-183">按一下 [檢視連接的裝置] 。</span><span class="sxs-lookup"><span data-stu-id="77287-183">Click **View connected devices**.</span></span>
    3. <span data-ttu-id="77287-184">在 [裝置]  頁面上，藉由查閱狀態來確認裝置已成功連接到服務。</span><span class="sxs-lookup"><span data-stu-id="77287-184">On the **Devices** page, verify that the device has successfully connected to the service by looking up the status.</span></span> <span data-ttu-id="77287-185">裝置狀態應該是 [線上] 。</span><span class="sxs-lookup"><span data-stu-id="77287-185">The device status should be **Online**.</span></span>
       
        ![StorSimple 裝置頁面](./media/storsimple-configure-and-register-device-gov/HCS_DeviceOnline-gov-include.png) 
       
        <span data-ttu-id="77287-187">如果裝置狀態為 [離線] ，請等待數分鐘，讓裝置上線。</span><span class="sxs-lookup"><span data-stu-id="77287-187">If the device status is **Offline**, wait for a couple of minutes for the device to come online.</span></span> 
       
        <span data-ttu-id="77287-188">如果數分鐘之後裝置仍然離線，請確定您的防火牆網路已依照 [StorSimple 裝置網路需求](../articles/storsimple/storsimple-system-requirements.md)中的說明加以設定。</span><span class="sxs-lookup"><span data-stu-id="77287-188">If the device is still offline after a few minutes, then you need to make sure that your firewall network was configured as described in [networking requirements for your StorSimple device](../articles/storsimple/storsimple-system-requirements.md).</span></span> 
       
        <span data-ttu-id="77287-189">請確認連接埠 9354 已開啟供輸出通訊使用，因為 StorSimple Manager 服務對裝置服務匯流排通訊也使用此連接埠。</span><span class="sxs-lookup"><span data-stu-id="77287-189">Verify that port 9354 is open for outbound communication as this is used by the service bus for StorSimple Manager service-to-device communication.</span></span>

