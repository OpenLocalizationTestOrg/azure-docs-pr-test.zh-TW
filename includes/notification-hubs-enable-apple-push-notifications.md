

## <a name="generate-hello-certificate-signing-request-file"></a><span data-ttu-id="da31e-101">產生 hello 憑證簽署要求檔案</span><span class="sxs-lookup"><span data-stu-id="da31e-101">Generate hello Certificate Signing Request file</span></span>
<span data-ttu-id="da31e-102">hello Apple Push Notification Service (APNS) 會使用憑證 tooauthenticate 推播通知。</span><span class="sxs-lookup"><span data-stu-id="da31e-102">hello Apple Push Notification Service (APNS) uses certificates tooauthenticate your push notifications.</span></span> <span data-ttu-id="da31e-103">請遵循這些指示 toocreate hello 必要的推播憑證 toosend，接收通知。</span><span class="sxs-lookup"><span data-stu-id="da31e-103">Follow these instructions toocreate hello necessary push certificate toosend and receive notifications.</span></span> <span data-ttu-id="da31e-104">如需這些概念的詳細資訊，請參閱 hello 官方[Apple Push Notification Service](http://go.microsoft.com/fwlink/p/?LinkId=272584)文件。</span><span class="sxs-lookup"><span data-stu-id="da31e-104">For more information on these concepts see hello official [Apple Push Notification Service](http://go.microsoft.com/fwlink/p/?LinkId=272584) documentation.</span></span>

<span data-ttu-id="da31e-105">產生 hello 憑證簽署要求 (CSR) 檔案，它是由 Apple toogenerate 帶正負號的推播憑證。</span><span class="sxs-lookup"><span data-stu-id="da31e-105">Generate hello Certificate Signing Request (CSR) file, which is used by Apple toogenerate a signed push certificate.</span></span>

1. <span data-ttu-id="da31e-106">您在 Mac 上，執行 hello 金鑰鏈存取 工具。</span><span class="sxs-lookup"><span data-stu-id="da31e-106">On your Mac, run hello Keychain Access tool.</span></span> <span data-ttu-id="da31e-107">您可以開啟從 hello**公用程式**資料夾或 hello**其他**hello 啟動平台上的資料夾。</span><span class="sxs-lookup"><span data-stu-id="da31e-107">It can be opened from hello **Utilities** folder or hello **Other** folder on hello launch pad.</span></span>
2. <span data-ttu-id="da31e-108">按一下 [金鑰鏈存取]，並展開 [憑證助理]，然後按一下 [從憑證授權單位要求憑證...]。</span><span class="sxs-lookup"><span data-stu-id="da31e-108">Click **Keychain Access**, expand **Certificate Assistant**, then click **Request a Certificate from a Certificate Authority...**.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-request-cert-from-ca.png)
3. <span data-ttu-id="da31e-109">選取您**使用者電子郵件地址**和**一般名稱**，請確定**儲存 toodisk**已選取，然後按一下**繼續**。</span><span class="sxs-lookup"><span data-stu-id="da31e-109">Select your **User Email Address** and **Common Name** , make sure that **Saved toodisk** is selected, and then click **Continue**.</span></span> <span data-ttu-id="da31e-110">保留 hello **CA 電子郵件地址**空白，因為它不是必要欄位。</span><span class="sxs-lookup"><span data-stu-id="da31e-110">Leave hello **CA Email Address** field blank as it is not required.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-csr-info.png)
4. <span data-ttu-id="da31e-111">輸入中的 hello 憑證簽署要求 (CSR) 檔案的名稱**存**，hello 中選取位置**其中**，然後按一下 **儲存**。</span><span class="sxs-lookup"><span data-stu-id="da31e-111">Type a name for hello Certificate Signing Request (CSR) file in **Save As**, select hello location in **Where**, then click **Save**.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-save-csr.png)
   
      <span data-ttu-id="da31e-112">這樣可以節省 hello 選取位置; hello CSR 檔案hello 預設位置是在 hello 桌面。</span><span class="sxs-lookup"><span data-stu-id="da31e-112">This saves hello CSR file in hello selected location; hello default location is in hello Desktop.</span></span> <span data-ttu-id="da31e-113">請記住 hello 選擇此檔案的位置。</span><span class="sxs-lookup"><span data-stu-id="da31e-113">Remember hello location chosen for this file.</span></span>

<span data-ttu-id="da31e-114">接下來，您會註冊 Apple 應用程式、 啟用推播通知，並上傳此匯出的 CSR toocreate 推播憑證。</span><span class="sxs-lookup"><span data-stu-id="da31e-114">Next, you will register your app with Apple, enable push notifications, and upload this exported CSR toocreate a push certificate.</span></span>

## <a name="register-your-app-for-push-notifications"></a><span data-ttu-id="da31e-115">針對推播通知註冊應用程式</span><span class="sxs-lookup"><span data-stu-id="da31e-115">Register your app for push notifications</span></span>
<span data-ttu-id="da31e-116">toobe 無法 toosend 推播通知 tooan iOS 應用程式，您必須向 Apple 以及註冊推播通知註冊您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="da31e-116">toobe able toosend push notifications tooan iOS app, you must register your application with Apple and also register for push notifications.</span></span>  

1. <span data-ttu-id="da31e-117">如果您沒有註冊您的應用程式，請瀏覽 toohello <a href="http://go.microsoft.com/fwlink/p/?LinkId=272456" target="_blank">iOS 佈建入口網站</a>hello Apple 開發人員中心上的記錄檔，以您的 Apple ID，在按一下**識別碼**，然後按一下 **應用程式識別碼**，最後按一下 hello  **+** 簽署 tooregister 新的應用程式。</span><span class="sxs-lookup"><span data-stu-id="da31e-117">If you have not already registered your app, navigate toohello <a href="http://go.microsoft.com/fwlink/p/?LinkId=272456" target="_blank">iOS Provisioning Portal</a> at hello Apple Developer Center, log on with your Apple ID, click **Identifiers**, then click **App IDs**, and finally click on hello **+** sign tooregister a new app.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-ios-appids.png)
      
2. <span data-ttu-id="da31e-118">更新 hello 下列新的應用程式的三個欄位，然後按一下**繼續**:</span><span class="sxs-lookup"><span data-stu-id="da31e-118">Update hello following three fields for your new app and then click **Continue**:</span></span>
   
   * <span data-ttu-id="da31e-119">**名稱**： 輸入您的應用程式的描述性名稱在 hello**名稱**欄位 hello**應用程式識別碼說明**> 一節。</span><span class="sxs-lookup"><span data-stu-id="da31e-119">**Name**: Type a descriptive name for your app in hello **Name** field in hello **App ID Description** section.</span></span>
   * <span data-ttu-id="da31e-120">**套件組合識別碼**: hello 下**明確的應用程式識別碼**區段中，輸入**配套識別碼**hello 形式`<Organization Identifier>.<Product Name>`hello 中所述[應用程式發佈指南](https://developer.apple.com/library/mac/documentation/IDEs/Conceptual/AppDistributionGuide/ConfiguringYourApp/ConfiguringYourApp.html#//apple_ref/doc/uid/TP40012582-CH28-SW8)。</span><span class="sxs-lookup"><span data-stu-id="da31e-120">**Bundle Identifier**: Under hello **Explicit App ID** section, enter a **Bundle Identifier** in hello form `<Organization Identifier>.<Product Name>` as mentioned in hello [App Distribution Guide](https://developer.apple.com/library/mac/documentation/IDEs/Conceptual/AppDistributionGuide/ConfiguringYourApp/ConfiguringYourApp.html#//apple_ref/doc/uid/TP40012582-CH28-SW8).</span></span> <span data-ttu-id="da31e-121">hello*組織識別碼*和*產品名稱*使用必須符合 hello 組織識別碼和建立您的 XCode 專案時要使用的產品名稱。</span><span class="sxs-lookup"><span data-stu-id="da31e-121">hello *Organization Identifier* and *Product Name* you use must match hello organization identifier and product name you will use when you create your XCode project.</span></span> <span data-ttu-id="da31e-122">在下面的 hello screeshot*通知中樞*做為組織 idenitifier 和*GetStarted*作為 hello 產品名稱。</span><span class="sxs-lookup"><span data-stu-id="da31e-122">In hello screeshot below *NotificationHubs* is used as a organization idenitifier and *GetStarted* is used as hello product name.</span></span> <span data-ttu-id="da31e-123">確定這符合您將使用您的 XCode 專案中的 hello 值可讓您 toouse hello 正確發行設定檔使用 XCode。</span><span class="sxs-lookup"><span data-stu-id="da31e-123">Making sure this matches hello values you will use in your XCode project will allow you toouse hello correct publishing profile with XCode.</span></span> 
   * <span data-ttu-id="da31e-124">**推播通知**： 核取 hello**推播通知**hello 中的選項**應用程式服務**一節。</span><span class="sxs-lookup"><span data-stu-id="da31e-124">**Push Notifications**: Check hello **Push Notifications** option in hello **App Services** section, .</span></span>
     
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-new-appid-info.png)
     
      <span data-ttu-id="da31e-125">這樣會產生您應用程式識別碼，並要求您 tooconfirm hello 資訊。</span><span class="sxs-lookup"><span data-stu-id="da31e-125">This generates your App ID and requests you tooconfirm hello information.</span></span> <span data-ttu-id="da31e-126">按一下**註冊**tooconfirm hello 新應用程式識別碼。</span><span class="sxs-lookup"><span data-stu-id="da31e-126">Click **Register** tooconfirm hello new App ID.</span></span>
     
      <span data-ttu-id="da31e-127">一旦您按一下**註冊**，您會看到 hello**登錄完成**畫面上，如下所示。</span><span class="sxs-lookup"><span data-stu-id="da31e-127">Once you click **Register**, you will see hello **Registration complete** screen, as shown below.</span></span> <span data-ttu-id="da31e-128">按一下 [完成] 。</span><span class="sxs-lookup"><span data-stu-id="da31e-128">Click **Done**.</span></span>
      
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-appid-registration-complete.png)


1. <span data-ttu-id="da31e-129">在 hello 開發人員中心，在應用程式識別碼，找出 hello 應用程式識別碼，只需要建立，並按一下其資料列。</span><span class="sxs-lookup"><span data-stu-id="da31e-129">In hello Developer Center, under App IDs, locate hello app ID that you just created, and click on its row.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-ios-appids2.png)
   
      <span data-ttu-id="da31e-130">按一下 hello 應用程式識別碼會顯示 hello 應用程式詳細資料。</span><span class="sxs-lookup"><span data-stu-id="da31e-130">Clicking on hello app ID will display hello app details.</span></span> <span data-ttu-id="da31e-131">按一下 hello**編輯**hello 底部的按鈕。</span><span class="sxs-lookup"><span data-stu-id="da31e-131">Click hello **Edit** button at hello bottom.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-edit-appid.png)
      
2. <span data-ttu-id="da31e-132">捲動 toohello hello 螢幕底部，然後按一下 hello**建立憑證...** hello 區段下方的按鈕**開發推入的 SSL 憑證**。</span><span class="sxs-lookup"><span data-stu-id="da31e-132">Scroll toohello bottom of hello screen, and click hello **Create Certificate...** button under hello section **Development Push SSL Certificate**.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-appid-create-cert.png)
   
      <span data-ttu-id="da31e-133">這會顯示 hello 「 新增 iOS 憑證 」 小幫手。</span><span class="sxs-lookup"><span data-stu-id="da31e-133">This displays hello "Add iOS Certificate" assistant.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="da31e-134">本教學課程使用開發憑證。</span><span class="sxs-lookup"><span data-stu-id="da31e-134">This tutorial uses a development certificate.</span></span> <span data-ttu-id="da31e-135">hello 註冊生產憑證時，使用相同程序。</span><span class="sxs-lookup"><span data-stu-id="da31e-135">hello same process is used when registering a production certificate.</span></span> <span data-ttu-id="da31e-136">請確定您使用 hello 相同憑證時傳送通知的類型。</span><span class="sxs-lookup"><span data-stu-id="da31e-136">Just make sure that you use hello same certificate type when sending notifications.</span></span>
   > 
   > 
3. <span data-ttu-id="da31e-137">按一下**選擇檔案**，瀏覽 toohello 位置儲存在 hello 第一個工作中，您建立的 hello CSR 檔案的位置，然後按一下 **產生**。</span><span class="sxs-lookup"><span data-stu-id="da31e-137">Click **Choose File**, browse toohello location where you saved hello CSR file that you created in hello first task, then click **Generate**.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-appid-cert-choose-csr.png)
4. <span data-ttu-id="da31e-138">Hello 入口網站建立 hello 憑證之後，請按一下 hello**下載**按鈕，然後按一下**完成**。</span><span class="sxs-lookup"><span data-stu-id="da31e-138">After hello certificate is created by hello portal, click hello **Download** button, and click **Done**.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-appid-download-cert.png)
   
      <span data-ttu-id="da31e-139">此下載 hello 憑證，並儲存它 tooyour 電腦在下載資料夾中。</span><span class="sxs-lookup"><span data-stu-id="da31e-139">This downloads hello certificate and saves it tooyour computer in your Downloads folder.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-cert-downloaded.png)
   
   > [!NOTE]
   > <span data-ttu-id="da31e-140">根據預設，hello 下載的檔案開發憑證的名稱為**aps_development.cer**。</span><span class="sxs-lookup"><span data-stu-id="da31e-140">By default, hello downloaded file a development certificate is named **aps_development.cer**.</span></span>
   > 
   > 
5. <span data-ttu-id="da31e-141">按兩下 hello 下載推播憑證**aps_development.cer**。</span><span class="sxs-lookup"><span data-stu-id="da31e-141">Double-click hello downloaded push certificate **aps_development.cer**.</span></span>
   
      <span data-ttu-id="da31e-142">這會安裝新憑證的 hello hello 鑰匙圈，如下所示：</span><span class="sxs-lookup"><span data-stu-id="da31e-142">This installs hello new certificate in hello Keychain, as shown below:</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-cert-in-keychain.png)
   
   > [!NOTE]
   > <span data-ttu-id="da31e-143">您的憑證中的 hello 名稱可能會不同，但將會加**Apple 開發 iOS 推送服務：**。</span><span class="sxs-lookup"><span data-stu-id="da31e-143">hello name in your certificate might be different, but it will be prefixed with **Apple Development iOS Push Services:**.</span></span>
   > 
   > 
6. <span data-ttu-id="da31e-144">在 金鑰鏈存取，以滑鼠右鍵按一下 hello 新推播憑證在 hello 中建立**憑證**類別目錄。</span><span class="sxs-lookup"><span data-stu-id="da31e-144">In Keychain Access, right-click hello new push certificate that you created in hello **Certificates** category.</span></span> <span data-ttu-id="da31e-145">按一下**匯出**hello 檔案名稱、 選取 hello **.p12**格式，然後再按一下**儲存**。</span><span class="sxs-lookup"><span data-stu-id="da31e-145">Click **Export**, name hello file, select hello **.p12** format, and then click **Save**.</span></span>
   
    ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-export-cert-p12.png)
   
    <span data-ttu-id="da31e-146">請記下 hello 檔案名稱和 hello.p12 匯出的憑證的位置。</span><span class="sxs-lookup"><span data-stu-id="da31e-146">Make a note of hello file name and location of hello exported .p12 certificate.</span></span> <span data-ttu-id="da31e-147">它將會使用的 tooenable APNS 驗證。</span><span class="sxs-lookup"><span data-stu-id="da31e-147">It will be used tooenable authentication with APNS.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="da31e-148">本教學課程會建立 QuickStart.p12 檔案。</span><span class="sxs-lookup"><span data-stu-id="da31e-148">This tutorial creates a QuickStart.p12 file.</span></span> <span data-ttu-id="da31e-149">Your file name and location might be different.</span><span class="sxs-lookup"><span data-stu-id="da31e-149">Your file name and location might be different.</span></span>
   > 
   > 

## <a name="create-a-provisioning-profile-for-hello-app"></a><span data-ttu-id="da31e-150">建立 hello 應用程式的佈建設定檔</span><span class="sxs-lookup"><span data-stu-id="da31e-150">Create a provisioning profile for hello app</span></span>
1. <span data-ttu-id="da31e-151">在 hello <a href="http://go.microsoft.com/fwlink/p/?LinkId=272456" target="_blank">iOS 佈建入口網站</a>，選取**佈建的設定檔**，選取**所有**，然後按一下hello  **+** 按鈕 toocreate 新的設定檔。</span><span class="sxs-lookup"><span data-stu-id="da31e-151">Back in hello <a href="http://go.microsoft.com/fwlink/p/?LinkId=272456" target="_blank">iOS Provisioning Portal</a>, select **Provisioning Profiles**, select **All**, and then click hello **+** button toocreate a new profile.</span></span> <span data-ttu-id="da31e-152">這會啟動 hello**新增 iOS Provisiong 設定檔**精靈</span><span class="sxs-lookup"><span data-stu-id="da31e-152">This launches hello **Add iOS Provisiong Profile** Wizard</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-new-provisioning-profile.png)
2. <span data-ttu-id="da31e-153">選取**iOS 應用程式開發**下**開發**為 hello provisiong 設定檔類型，然後按**繼續**。</span><span class="sxs-lookup"><span data-stu-id="da31e-153">Select **iOS App Development** under **Development** as hello provisiong profile type, and click **Continue**.</span></span> 
3. <span data-ttu-id="da31e-154">接下來，選取您剛才建立的 hello hello 應用程式識別碼**應用程式識別碼**下拉式清單，然後按一下**繼續**</span><span class="sxs-lookup"><span data-stu-id="da31e-154">Next, select hello app ID you just created from hello **App ID** drop-down list, and click **Continue**</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-select-appid-for-provisioning.png)
4. <span data-ttu-id="da31e-155">在 hello**選取憑證**畫面上，選取您的一般開發憑證用於簽章的程式碼，然後按一下**繼續**。</span><span class="sxs-lookup"><span data-stu-id="da31e-155">In hello **Select certificates** screen, select your usual development certificate used for code signing, and click **Continue**.</span></span> <span data-ttu-id="da31e-156">這不是您剛才建立的 hello 推播憑證。</span><span class="sxs-lookup"><span data-stu-id="da31e-156">This is not hello push certificate you just created.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-provisioning-select-cert.png)
5. <span data-ttu-id="da31e-157">接下來，選取 hello**裝置**測試，然後按一下 toouse**繼續**</span><span class="sxs-lookup"><span data-stu-id="da31e-157">Next, select hello **Devices** toouse for testing, and click **Continue**</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-provisioning-select-devices.png)
6. <span data-ttu-id="da31e-158">最後，挑選 hello 設定檔中的名稱**設定檔名稱**，按一下 **產生**。</span><span class="sxs-lookup"><span data-stu-id="da31e-158">Finally, pick a name for hello profile in **Profile Name**, click **Generate**.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-provisioning-name-profile.png)
7. <span data-ttu-id="da31e-159">建立新的佈建設定檔的 hello 時按一下 toodownload 它並安裝它在 Xcode 開發電腦上。</span><span class="sxs-lookup"><span data-stu-id="da31e-159">When hello new provisioning profile is created click toodownload it and install it on your Xcode development machine.</span></span> <span data-ttu-id="da31e-160">然後按一下 [完成]。</span><span class="sxs-lookup"><span data-stu-id="da31e-160">Then click **Done**.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-provisioning-profile-ready.png)
