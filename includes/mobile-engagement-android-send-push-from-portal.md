### <a name="grant-mobile-engagement-access-tooyour-gcm-api-key"></a><span data-ttu-id="bceb0-101">授與 Mobile Engagement 存取 tooyour GCM API 金鑰</span><span class="sxs-lookup"><span data-stu-id="bceb0-101">Grant Mobile Engagement access tooyour GCM API Key</span></span>
<span data-ttu-id="bceb0-102">tooallow Mobile Engagement toosend 推播通知您的身分，您需要 toogrant 它存取 tooyour API 金鑰。</span><span class="sxs-lookup"><span data-stu-id="bceb0-102">tooallow Mobile Engagement toosend push notifications on your behalf, you need toogrant it access tooyour API Key.</span></span> <span data-ttu-id="bceb0-103">這是藉由設定和 hello Mobile Engagement 入口網站中輸入您的金鑰。</span><span class="sxs-lookup"><span data-stu-id="bceb0-103">This is done by configuring and entering your key into hello Mobile Engagement portal.</span></span>

1. <span data-ttu-id="bceb0-104">從 Azure 傳統入口網站，請確定您在 hello 應用程式，我們要使用此專案中，，然後按一下hello **Engage** hello 底部的按鈕：</span><span class="sxs-lookup"><span data-stu-id="bceb0-104">From your Azure Classic Portal, ensure you're in hello app we're using for this project, and then click hello **Engage** button at hello bottom:</span></span>
   
    ![](./media/mobile-engagement-android-send-push/engage-button.png)
2. <span data-ttu-id="bceb0-105">然後按一下 hello**設定** -> **原生推送**區段 tooenter GCM 金鑰：</span><span class="sxs-lookup"><span data-stu-id="bceb0-105">Then click hello **Settings** -> **Native Push** section tooenter your GCM Key:</span></span>
   
    ![](./media/mobile-engagement-android-send-push/engagement-portal.png)
3. <span data-ttu-id="bceb0-106">按一下 hello**編輯**前面圖示**API 金鑰**在 hello **GCM 設定**區段如下所示：</span><span class="sxs-lookup"><span data-stu-id="bceb0-106">Click hello **Edit** icon in front of **API Key** in hello **GCM Settings** section as shown below:</span></span>
   
    ![](./media/mobile-engagement-android-send-push/native-push-settings.png)
4. <span data-ttu-id="bceb0-107">Hello 快顯視窗，在貼 hello 您之前取得 GCM 伺服器金鑰，然後再按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="bceb0-107">In hello pop-up, paste hello GCM Server Key you obtained before and then click **Ok**.</span></span>
   
    ![](./media/mobile-engagement-android-send-push/api-key.png)

## <span data-ttu-id="bceb0-108"><a id="send"></a>傳送通知 tooyour 應用程式</span><span class="sxs-lookup"><span data-stu-id="bceb0-108"><a id="send"></a>Send a notification tooyour app</span></span>
<span data-ttu-id="bceb0-109">現在，我們將建立簡單的推播通知活動所傳送的推播通知 tooour 應用程式。</span><span class="sxs-lookup"><span data-stu-id="bceb0-109">We will now create a simple push notification campaign that sends a push notification tooour app.</span></span>

1. <span data-ttu-id="bceb0-110">瀏覽 toohello**到達** 索引標籤中您的 Mobile Engagement 入口網站。</span><span class="sxs-lookup"><span data-stu-id="bceb0-110">Navigate toohello **REACH** tab in your Mobile Engagement portal.</span></span>
2. <span data-ttu-id="bceb0-111">按一下**新的 announcement** toocreate 您推播通知的活動。</span><span class="sxs-lookup"><span data-stu-id="bceb0-111">Click **New announcement** toocreate your push notification campaign.</span></span>
   
    ![](./media/mobile-engagement-android-send-push/new-announcement.png)
3. <span data-ttu-id="bceb0-112">設定您的活動，透過下列步驟的 hello hello 第一個欄位：</span><span class="sxs-lookup"><span data-stu-id="bceb0-112">Set up hello first field of your campaign through hello following steps:</span></span>
   
    ![](./media/mobile-engagement-android-send-push/campaign-first-params.png)
   
    <span data-ttu-id="bceb0-113">a.</span><span class="sxs-lookup"><span data-stu-id="bceb0-113">a.</span></span> <span data-ttu-id="bceb0-114">為您的活動命名。</span><span class="sxs-lookup"><span data-stu-id="bceb0-114">Name your campaign.</span></span>
   
    <span data-ttu-id="bceb0-115">b.</span><span class="sxs-lookup"><span data-stu-id="bceb0-115">b.</span></span> <span data-ttu-id="bceb0-116">選取 hello**傳遞類型**為*系統通知]-> [簡單*： 這是功能標題和小型的一行文字的 hello 簡單 Android 推播通知類型。</span><span class="sxs-lookup"><span data-stu-id="bceb0-116">Select hello **Delivery type** as *System notification -> Simple*: This is hello simple Android push notification type that features a title and a small line of text.</span></span>
   
    <span data-ttu-id="bceb0-117">c.</span><span class="sxs-lookup"><span data-stu-id="bceb0-117">c.</span></span> <span data-ttu-id="bceb0-118">選取**傳遞時間**為*隨時*tooallow hello 應用程式 tooreceive 通知，是否 hello 應用程式會啟動與否。</span><span class="sxs-lookup"><span data-stu-id="bceb0-118">Select **Delivery time** as *Any time* tooallow hello app tooreceive a notification whether hello app is started or not.</span></span>
   
    <span data-ttu-id="bceb0-119">d.</span><span class="sxs-lookup"><span data-stu-id="bceb0-119">d.</span></span> <span data-ttu-id="bceb0-120">在 hello 通知文字型別 hello**標題**，將會以粗體顯示在 hello 推入。</span><span class="sxs-lookup"><span data-stu-id="bceb0-120">In hello notification text type hello **Title** which will be in bold in hello push.</span></span>
   
    <span data-ttu-id="bceb0-121">e.</span><span class="sxs-lookup"><span data-stu-id="bceb0-121">e.</span></span> <span data-ttu-id="bceb0-122">然後輸入您的 [訊息]。</span><span class="sxs-lookup"><span data-stu-id="bceb0-122">Then type your **Message**</span></span>
4. <span data-ttu-id="bceb0-123">向下捲動，在 hello**內容**區段中，選取**僅限通知**。</span><span class="sxs-lookup"><span data-stu-id="bceb0-123">Scroll down, and in hello **Content** section, select **Notification only**.</span></span>
   
    ![](./media/mobile-engagement-android-send-push/campaign-content.png)
5. <span data-ttu-id="bceb0-124">您已完成設定 hello 最基本活動可能。</span><span class="sxs-lookup"><span data-stu-id="bceb0-124">You're done setting hello most basic campaign possible.</span></span> <span data-ttu-id="bceb0-125">現在，向下捲動並按一下 hello**建立**按鈕 toosave 您的活動。</span><span class="sxs-lookup"><span data-stu-id="bceb0-125">Now scroll down again and click hello **Create** button toosave your campaign.</span></span>
6. <span data-ttu-id="bceb0-126">最後一個步驟： 按一下**Activate** tooactivate 活動 toosend 推播通知。</span><span class="sxs-lookup"><span data-stu-id="bceb0-126">Last step: click **Activate** tooactivate your campaign toosend push notifications.</span></span>
   
    ![](./media/mobile-engagement-android-send-push/campaign-activate.png)

