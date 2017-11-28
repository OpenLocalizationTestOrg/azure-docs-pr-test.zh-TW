<!--author=SharS last changed: 06/22/2016-->

### <a name="to-configure-and-register-the-device"></a><span data-ttu-id="565ee-101">設定和註冊裝置</span><span class="sxs-lookup"><span data-stu-id="565ee-101">To configure and register the device</span></span>
1. <span data-ttu-id="565ee-102">存取 StorSimple 裝置序列主控台上的 Windows PowerShell 介面。</span><span class="sxs-lookup"><span data-stu-id="565ee-102">Access the Windows PowerShell interface on your StorSimple device serial console.</span></span> <span data-ttu-id="565ee-103">如需相關指示，請參閱 [使用 PuTTY 來連接至裝置序列主控台](../articles/storsimple/storsimple-8000-deployment-walkthrough-gov-u2.md#use-putty-to-connect-to-the-device-serial-console) 。</span><span class="sxs-lookup"><span data-stu-id="565ee-103">See [Use PuTTY to connect to the device serial console](../articles/storsimple/storsimple-8000-deployment-walkthrough-gov-u2.md#use-putty-to-connect-to-the-device-serial-console) for instructions.</span></span> <span data-ttu-id="565ee-104">**請務必確實依照此程序，否則將無法存取主控台。**</span><span class="sxs-lookup"><span data-stu-id="565ee-104">**Be sure to follow the procedure exactly or you will not be able to access the console.**</span></span>
2. <span data-ttu-id="565ee-105">在開啟的工作階段中，按 **Enter** 鍵一次可取得命令提示字元。</span><span class="sxs-lookup"><span data-stu-id="565ee-105">In the session that opens up, press **Enter** one time to get a command prompt.</span></span>
3. <span data-ttu-id="565ee-106">系統將提示您選擇想要為裝置設定的語言。</span><span class="sxs-lookup"><span data-stu-id="565ee-106">You will be prompted to choose the language that you would like to set for your device.</span></span> <span data-ttu-id="565ee-107">指定語言，然後按 **Enter** 鍵。</span><span class="sxs-lookup"><span data-stu-id="565ee-107">Specify the language, and then press **Enter**.</span></span>
   
    ![StorSimple 設定和註冊裝置 1](./media/storsimple-configure-and-register-device-gov-u2/HCS_RegisterYourDevice1-gov-include.png)
4. <span data-ttu-id="565ee-109">在顯示的序列主控台功能表中，選擇選項 1 以使用完整存取權進行登入。</span><span class="sxs-lookup"><span data-stu-id="565ee-109">In the serial console menu that is presented, choose option 1 to log on with full access.</span></span>
   
    ![StorSimple 註冊裝置 2](./media/storsimple-configure-and-register-device-gov-u2/HCS_RegisterYourDevice2-gov-include.png)
5. <span data-ttu-id="565ee-111">執行下列步驟，為裝置設定最小的必要網路設定。</span><span class="sxs-lookup"><span data-stu-id="565ee-111">Perform the following steps to configure the minimum required network settings for your device.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="565ee-112">這些設定步驟必須在裝置的主動控制器上執行。</span><span class="sxs-lookup"><span data-stu-id="565ee-112">These configuration steps need to be performed on the active controller of the device.</span></span> <span data-ttu-id="565ee-113">序列主控台功能表會在橫幅訊息中指出控制站狀態。</span><span class="sxs-lookup"><span data-stu-id="565ee-113">The serial console menu indicates the controller state in the banner message.</span></span> <span data-ttu-id="565ee-114">如果您未連接到主動控制器，請中斷連線，然後連接到主動控制器。</span><span class="sxs-lookup"><span data-stu-id="565ee-114">If you are not connect to the active controller, disconnect and then connect to the active controller.</span></span>
   
   1. <span data-ttu-id="565ee-115">在命令提示字元中，輸入您的密碼。</span><span class="sxs-lookup"><span data-stu-id="565ee-115">At the command prompt, type your password.</span></span> <span data-ttu-id="565ee-116">預設裝置密碼是 **Password1**。</span><span class="sxs-lookup"><span data-stu-id="565ee-116">The default device password is **Password1**.</span></span>
   2. <span data-ttu-id="565ee-117">輸入以下命令：</span><span class="sxs-lookup"><span data-stu-id="565ee-117">Type the following command:</span></span>
      
        `Invoke-HcsSetupWizard`
   3. <span data-ttu-id="565ee-118">安裝精靈將協助您設定裝置的網路設定。</span><span class="sxs-lookup"><span data-stu-id="565ee-118">A setup wizard will appear to help you configure the network settings for the device.</span></span> <span data-ttu-id="565ee-119">請提供下列資訊：</span><span class="sxs-lookup"><span data-stu-id="565ee-119">Supply the following information:</span></span>
      
      * <span data-ttu-id="565ee-120">適用於 DATA 0 網路介面的 IP 位址</span><span class="sxs-lookup"><span data-stu-id="565ee-120">IP address for DATA 0 network interface</span></span>
      * <span data-ttu-id="565ee-121">子網路遮罩</span><span class="sxs-lookup"><span data-stu-id="565ee-121">Subnet mask</span></span>
      * <span data-ttu-id="565ee-122">閘道器</span><span class="sxs-lookup"><span data-stu-id="565ee-122">Gateway</span></span>
      * <span data-ttu-id="565ee-123">適用於主要 DNS 伺服器的 IP 位址</span><span class="sxs-lookup"><span data-stu-id="565ee-123">IP address for Primary DNS server</span></span>
      * <span data-ttu-id="565ee-124">適用於主要 NTP 伺服器的 IP 位址</span><span class="sxs-lookup"><span data-stu-id="565ee-124">IP address for Primary NTP server</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="565ee-125">您可能需要等候幾分鐘，以套用子網路遮罩和 DNS 設定。</span><span class="sxs-lookup"><span data-stu-id="565ee-125">You may have to wait for a few minutes for the subnet mask and DNS settings to be applied.</span></span>
    
   4. <span data-ttu-id="565ee-126">選擇性設定 Web Proxy 伺服器。</span><span class="sxs-lookup"><span data-stu-id="565ee-126">Optionally, configure your web proxy server.</span></span>
      
      > [!IMPORTANT]
      > <span data-ttu-id="565ee-127">雖然 Web Proxy 設定是選用的，但請注意，如果您使用 Web Proxy，就只能在此處設定它。</span><span class="sxs-lookup"><span data-stu-id="565ee-127">Although web proxy configuration is optional, be aware that if you use a web proxy, you can only configure it here.</span></span> <span data-ttu-id="565ee-128">如需詳細資訊，請參閱 [設定裝置的 Web Proxy](../articles/storsimple/storsimple-configure-web-proxy.md)。</span><span class="sxs-lookup"><span data-stu-id="565ee-128">For more information, go to [Configure web proxy for your device](../articles/storsimple/storsimple-configure-web-proxy.md).</span></span>
     
6. <span data-ttu-id="565ee-129">按 Ctrl + C 來結束安裝精靈。</span><span class="sxs-lookup"><span data-stu-id="565ee-129">Press Ctrl + C to exit the setup wizard.</span></span>
8. <span data-ttu-id="565ee-130">執行下列 Cmdlet，將裝置指向 Microsoft Azure Government 入口網站 (因為預設指向公用 Azure 傳統入口網站)。</span><span class="sxs-lookup"><span data-stu-id="565ee-130">Run the following cmdlet to point the device to the Microsoft Azure Government portal (because it points to the public Azure classic portal by default).</span></span> <span data-ttu-id="565ee-131">這樣會重新啟動兩個控制器。</span><span class="sxs-lookup"><span data-stu-id="565ee-131">This will restart both controllers.</span></span> <span data-ttu-id="565ee-132">建議您使用兩個 PuTTY 工作階段以同時連線至兩個控制器，這樣您就可以看見每個控制器是何時重新啟動。</span><span class="sxs-lookup"><span data-stu-id="565ee-132">We recommend that you use two PuTTY sessions to simultaneously connect to both controllers so that you can see when each controller is restarted.</span></span>
   
    `Set-CloudPlatform -AzureGovt_US`
   
   <span data-ttu-id="565ee-133">您將會看見確認訊息。</span><span class="sxs-lookup"><span data-stu-id="565ee-133">You will see a confirmation message.</span></span> <span data-ttu-id="565ee-134">接受預設值 (**Y**)。</span><span class="sxs-lookup"><span data-stu-id="565ee-134">Accept the default (**Y**).</span></span>
9. <span data-ttu-id="565ee-135">執行下列 Cmdlet 以繼續設定：</span><span class="sxs-lookup"><span data-stu-id="565ee-135">Run the following cmdlet to resume setup:</span></span>
   
    `Invoke-HcsSetupWizard`
   
    ![繼續設定精靈](./media/storsimple-configure-and-register-device-gov-u2/HCS_ResumeSetup-gov-include.png)
   
10. <span data-ttu-id="565ee-137">接受網路設定。</span><span class="sxs-lookup"><span data-stu-id="565ee-137">Accept the network settings.</span></span> <span data-ttu-id="565ee-138">在您接受每個設定之後，您會看到驗證訊息。</span><span class="sxs-lookup"><span data-stu-id="565ee-138">You will see a validation message after you accept each setting.</span></span>
11. <span data-ttu-id="565ee-139">基於安全性理由，裝置系統管理員密碼會在第一個工作階段之後過期，您必須立即變更。</span><span class="sxs-lookup"><span data-stu-id="565ee-139">For security reasons, the device administrator password expires after the first session, and you will need to change it now.</span></span> <span data-ttu-id="565ee-140">出現提示時，請提供裝置系統管理員密碼。</span><span class="sxs-lookup"><span data-stu-id="565ee-140">When prompted, provide a device administrator password.</span></span> <span data-ttu-id="565ee-141">有效的裝置系統管理員密碼長度必須介於 8 到 15 個字元。</span><span class="sxs-lookup"><span data-stu-id="565ee-141">A valid device administrator password must be between 8 and 15 characters.</span></span> <span data-ttu-id="565ee-142">密碼必須包含下列其中三項：大寫、小寫、數字和特殊字元。</span><span class="sxs-lookup"><span data-stu-id="565ee-142">The password must contain three of the following: lowercase, uppercase, numeric, and special characters.</span></span>
    
    <br/>![StorSimple 註冊裝置 5](./media/storsimple-configure-and-register-device-gov-u2/HCS_RegisterYourDevice5_gov-include.png)
12. <span data-ttu-id="565ee-144">安裝精靈的最後一個步驟，是向 StorSimple 裝置管理員服務註冊您的裝置。</span><span class="sxs-lookup"><span data-stu-id="565ee-144">The final step in the setup wizard registers your device with the StorSimple Device Manager service.</span></span> <span data-ttu-id="565ee-145">基於此因素，您需要在[步驟 2：取得服務註冊金鑰中取得的服務註冊金鑰](../articles/storsimple/storsimple-8000-deployment-walkthrough-gov-u2.md#step-2-get-the-service-registration-key)。</span><span class="sxs-lookup"><span data-stu-id="565ee-145">For this, you will need the service registration key that you obtained in [Step 2: Get the service registration key](../articles/storsimple/storsimple-8000-deployment-walkthrough-gov-u2.md#step-2-get-the-service-registration-key).</span></span> <span data-ttu-id="565ee-146">提供註冊金鑰之後，您可能需要等待 2-3 分鐘，才能註冊裝置。</span><span class="sxs-lookup"><span data-stu-id="565ee-146">After you supply the registration key, you may need to wait for 2-3 minutes before the device is registered.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="565ee-147">您可以隨時按 Ctrl + C 來結束安裝精靈。</span><span class="sxs-lookup"><span data-stu-id="565ee-147">You can press Ctrl + C at any time to exit the setup wizard.</span></span> <span data-ttu-id="565ee-148">如果您輸入所有網路設定 (Data 0 的 IP 位址、子網路遮罩和閘道器)，則會保留您的項目。</span><span class="sxs-lookup"><span data-stu-id="565ee-148">If you have entered all the network settings (IP address for Data 0, Subnet mask, and Gateway), your entries will be retained.</span></span>
    
    ![StorSimple 註冊進度](./media/storsimple-configure-and-register-device-gov-u2/HCS_RegistrationProgress-gov-include.png)
13. <span data-ttu-id="565ee-150">註冊裝置之後，隨即會出現服務資料加密金鑰。</span><span class="sxs-lookup"><span data-stu-id="565ee-150">After the device is registered, a Service Data Encryption key will appear.</span></span> <span data-ttu-id="565ee-151">複製這個金鑰，並將它儲存在安全的位置。</span><span class="sxs-lookup"><span data-stu-id="565ee-151">Copy this key and save it in a safe location.</span></span> <span data-ttu-id="565ee-152">**這個金鑰需要與服務註冊金鑰搭配使用，才能向 StorSimple 裝置管理員服務註冊其他裝置。**</span><span class="sxs-lookup"><span data-stu-id="565ee-152">**This key is required with the service registration key to register additional devices with the StorSimple Device Manager service.**</span></span> <span data-ttu-id="565ee-153">如需這個金鑰的詳細資訊，請參閱 [StorSimple 安全性](../articles/storsimple/storsimple-8000-security.md) 。</span><span class="sxs-lookup"><span data-stu-id="565ee-153">Refer to [StorSimple security](../articles/storsimple/storsimple-8000-security.md) for more information about this key.</span></span>
    
    ![StorSimple 註冊裝置 7](./media/storsimple-configure-and-register-device-gov-u2/HCS_RegisterYourDevice7_gov-include.png)
    > [!IMPORTANT]
    > <span data-ttu-id="565ee-155">若要從序列主控台視窗複製文字，只需選取該文字。</span><span class="sxs-lookup"><span data-stu-id="565ee-155">To copy the text from the serial console window, simply select the text.</span></span> <span data-ttu-id="565ee-156">然後您應該能夠將它貼到剪貼簿或任何文字編輯器中。</span><span class="sxs-lookup"><span data-stu-id="565ee-156">You should then be able to paste it in the clipboard or any text editor.</span></span>
    > 
    > <span data-ttu-id="565ee-157">請勿使用 **Ctrl + C** 來複製服務資料加密金鑰。</span><span class="sxs-lookup"><span data-stu-id="565ee-157">DO NOT use **Ctrl + C** to copy the service data encryption key.</span></span> <span data-ttu-id="565ee-158">使用 **Ctrl + C** 將導致安裝精靈結束。</span><span class="sxs-lookup"><span data-stu-id="565ee-158">Using **Ctrl + C** will cause you to exit the setup wizard.</span></span> <span data-ttu-id="565ee-159">如此一來，裝置系統管理員密碼將不會變更，而裝置將還原為預設密碼。</span><span class="sxs-lookup"><span data-stu-id="565ee-159">As a result, the device administrator password will not be changed and the device will revert to the default password.</span></span>
    
14. <span data-ttu-id="565ee-160">結束序列主控台。</span><span class="sxs-lookup"><span data-stu-id="565ee-160">Exit the serial console.</span></span>
15. <span data-ttu-id="565ee-161">返回 Azure Government 入口網站，並完成下列步驟：</span><span class="sxs-lookup"><span data-stu-id="565ee-161">Return to the Azure Government Portal, and complete the following steps:</span></span>
    
    1. <span data-ttu-id="565ee-162">移至您的 StorSimple 裝置管理員服務。</span><span class="sxs-lookup"><span data-stu-id="565ee-162">Go to your StorSimple Device Manager service.</span></span>
    2. <span data-ttu-id="565ee-163">按一下 [裝置]。</span><span class="sxs-lookup"><span data-stu-id="565ee-163">Click **Devices**.</span></span> <span data-ttu-id="565ee-164">從裝置清單中找出您正在部署的裝置。</span><span class="sxs-lookup"><span data-stu-id="565ee-164">From the list of devices, identify the device that you are ddeploying.</span></span> <span data-ttu-id="565ee-165">藉由查閱狀態來確認裝置已成功連線到服務。</span><span class="sxs-lookup"><span data-stu-id="565ee-165">Verify that the device has successfully connected to the service by looking up the status.</span></span> <span data-ttu-id="565ee-166">裝置狀態應該是 [線上] 。</span><span class="sxs-lookup"><span data-stu-id="565ee-166">The device status should be **Online**.</span></span>
            
        <span data-ttu-id="565ee-167">如果裝置狀態為 [離線] ，請等待數分鐘，讓裝置上線。</span><span class="sxs-lookup"><span data-stu-id="565ee-167">If the device status is **Offline**, wait for a couple of minutes for the device to come online.</span></span>
       
        <span data-ttu-id="565ee-168">如果數分鐘之後裝置仍然離線，請確定您的防火牆網路已依照 [StorSimple 裝置網路需求](../articles/storsimple/storsimple-8000-system-requirements.md)中的說明加以設定。</span><span class="sxs-lookup"><span data-stu-id="565ee-168">If the device is still offline after a few minutes, then you need to make sure that your firewall network was configured as described in [networking requirements for your StorSimple device](../articles/storsimple/storsimple-8000-system-requirements.md).</span></span>
       
        <span data-ttu-id="565ee-169">請確認連接埠 9354 已開啟可供輸出通訊使用，因為 StorSimple 裝置管理員服務對裝置的服務匯流排也是使用此連接埠進行通訊。</span><span class="sxs-lookup"><span data-stu-id="565ee-169">Verify that port 9354 is open for outbound communication as this is used by the service bus for StorSimple Device Manager Service-to-device communication.</span></span>

