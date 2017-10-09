
1. <span data-ttu-id="e66ca-101">瀏覽 toohello [Google 雲端主控台](https://console.developers.google.com/project)，使用您的 Google 帳戶認證登入。</span><span class="sxs-lookup"><span data-stu-id="e66ca-101">Navigate toohello [Google Cloud Console](https://console.developers.google.com/project), sign in with your Google account credentials.</span></span> 
2. <span data-ttu-id="e66ca-102">按一下 [建立專案]，輸入專案名稱，接著按 [建立]。</span><span class="sxs-lookup"><span data-stu-id="e66ca-102">Click **Create Project**, type a project name, then click **Create**.</span></span> <span data-ttu-id="e66ca-103">如果要求中，執行 hello SMS 驗證，並按一下**建立**一次。</span><span class="sxs-lookup"><span data-stu-id="e66ca-103">If requested, carry out hello SMS Verification, and click **Create** again.</span></span>
   
    ![建立新專案](./media/mobile-services-enable-google-cloud-messaging/mobile-services-google-new-project.png)   
   
     <span data-ttu-id="e66ca-105">輸入新的**專案名稱**並按一下 [建立專案]。</span><span class="sxs-lookup"><span data-stu-id="e66ca-105">Type in your new **Project name** and click **Create project**.</span></span>
3. <span data-ttu-id="e66ca-106">按一下 hello**公用程式及其他**按鈕，然後按一下**專案資訊**。</span><span class="sxs-lookup"><span data-stu-id="e66ca-106">Click hello **Utilities and More** button and then click **Project Information**.</span></span> <span data-ttu-id="e66ca-107">請記下 hello**專案編號**。</span><span class="sxs-lookup"><span data-stu-id="e66ca-107">Make a note of hello **Project Number**.</span></span> <span data-ttu-id="e66ca-108">您將需要 tooset 這個值為 hello `SenderId` hello 用戶端應用程式中的變數。</span><span class="sxs-lookup"><span data-stu-id="e66ca-108">You will need tooset this value as hello `SenderId` variable in hello client app.</span></span>
   
    ![公用程式及其他資訊](./media/mobile-services-enable-google-cloud-messaging/notification-hubs-utilities-and-more.png)
4. <span data-ttu-id="e66ca-110">在 hello 專案儀表板，在**Mobile Api**，按一下**Google Cloud Messaging**，然後在 hello 下一個頁面上按一下**啟用 API**並接受服務條款 hello。</span><span class="sxs-lookup"><span data-stu-id="e66ca-110">In hello project dashboard, under **Mobile APIs**, click **Google Cloud Messaging**, then on hello next page click **Enable API** and accept hello terms of service.</span></span> 
   
    ![啟用 GCM](./media/mobile-services-enable-google-cloud-messaging/enable-GCM.png)
   
    ![啟用 GCM](./media/mobile-services-enable-google-cloud-messaging/enable-gcm-2.png) 
5. <span data-ttu-id="e66ca-113">在 hello 專案儀表板中，按一下 **認證** > **Create Credential** > **API 金鑰**。</span><span class="sxs-lookup"><span data-stu-id="e66ca-113">In hello project dashboard, Click **Credentials** > **Create Credential** > **API Key**.</span></span> 
   
    ![](./media/mobile-services-enable-google-cloud-messaging/mobile-services-google-create-server-key.png)
6. <span data-ttu-id="e66ca-114">在 [建立新的金鑰] 中，按一下 [伺服器金鑰]，輸入金鑰的名稱，然後按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="e66ca-114">In **Create a new key**, click **Server key**, type a name for your key, then click **Create**.</span></span>
7. <span data-ttu-id="e66ca-115">請記下 hello **API 金鑰**值。</span><span class="sxs-lookup"><span data-stu-id="e66ca-115">Make a note of hello **API KEY** value.</span></span>
   
    <span data-ttu-id="e66ca-116">您將使用此 API 金鑰值 tooenable Azure tooauthenticate GCM，並代表您的應用程式中傳送推播通知。</span><span class="sxs-lookup"><span data-stu-id="e66ca-116">You will use this API key value tooenable Azure tooauthenticate with GCM and send push notifications on behalf of your app.</span></span>

