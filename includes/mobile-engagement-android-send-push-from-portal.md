### <a name="grant-mobile-engagement-access-to-your-gcm-api-key"></a><span data-ttu-id="be388-101">授與 Mobile Engagement 的存取權給 GCM API 金鑰</span><span class="sxs-lookup"><span data-stu-id="be388-101">Grant Mobile Engagement access to your GCM API Key</span></span>
<span data-ttu-id="be388-102">若要讓 Mobile Engagement 以您的名義傳送推播通知，您必須授與 API 金鑰的存取權。</span><span class="sxs-lookup"><span data-stu-id="be388-102">To allow Mobile Engagement to send push notifications on your behalf, you need to grant it access to your API Key.</span></span> <span data-ttu-id="be388-103">完成此項作業的方法為在 Mobile Engagement 入口網站中設定並輸入您的金鑰。</span><span class="sxs-lookup"><span data-stu-id="be388-103">This is done by configuring and entering your key into the Mobile Engagement portal.</span></span>

1. <span data-ttu-id="be388-104">請從 Azure 傳統入口網站確認您在我們用於此專案的應用程式中，然後按一下底部的 [接洽]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="be388-104">From your Azure Classic Portal, ensure you're in the app we're using for this project, and then click the **Engage** button at the bottom:</span></span>
   
    ![](./media/mobile-engagement-android-send-push/engage-button.png)
2. <span data-ttu-id="be388-105">然後按一下 [設定]  ->  [原生推送] 區段來輸入 GCM 金鑰：</span><span class="sxs-lookup"><span data-stu-id="be388-105">Then click the **Settings** -> **Native Push** section to enter your GCM Key:</span></span>
   
    ![](./media/mobile-engagement-android-send-push/engagement-portal.png)
3. <span data-ttu-id="be388-106">在 [GCM 設定] 區段中，按一下 [API 金鑰] 前面的 [編輯]圖示，如下所示：</span><span class="sxs-lookup"><span data-stu-id="be388-106">Click the **Edit** icon in front of **API Key** in the **GCM Settings** section as shown below:</span></span>
   
    ![](./media/mobile-engagement-android-send-push/native-push-settings.png)
4. <span data-ttu-id="be388-107">在快顯視窗中，貼上您先前取得的 GCM 伺服器金鑰，然後按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="be388-107">In the pop-up, paste the GCM Server Key you obtained before and then click **Ok**.</span></span>
   
    ![](./media/mobile-engagement-android-send-push/api-key.png)

## <span data-ttu-id="be388-108"><a id="send"></a>傳送通知至應用程式</span><span class="sxs-lookup"><span data-stu-id="be388-108"><a id="send"></a>Send a notification to your app</span></span>
<span data-ttu-id="be388-109">我們將建立一個簡單的推播通知活動，它會將推播通知傳送至我們的應用程式。</span><span class="sxs-lookup"><span data-stu-id="be388-109">We will now create a simple push notification campaign that sends a push notification to our app.</span></span>

1. <span data-ttu-id="be388-110">瀏覽至您的 Mobile Engagement 入口網站中的 [觸達]  索引標籤</span><span class="sxs-lookup"><span data-stu-id="be388-110">Navigate to the **REACH** tab in your Mobile Engagement portal.</span></span>
2. <span data-ttu-id="be388-111">按一下 [新增宣告]  來建立您的推播通知活動。</span><span class="sxs-lookup"><span data-stu-id="be388-111">Click **New announcement** to create your push notification campaign.</span></span>
   
    ![](./media/mobile-engagement-android-send-push/new-announcement.png)
3. <span data-ttu-id="be388-112">透過下列步驟來設定活動的第一個欄位：</span><span class="sxs-lookup"><span data-stu-id="be388-112">Set up the first field of your campaign through the following steps:</span></span>
   
    ![](./media/mobile-engagement-android-send-push/campaign-first-params.png)
   
    <span data-ttu-id="be388-113">a.</span><span class="sxs-lookup"><span data-stu-id="be388-113">a.</span></span> <span data-ttu-id="be388-114">為您的活動命名。</span><span class="sxs-lookup"><span data-stu-id="be388-114">Name your campaign.</span></span>
   
    <span data-ttu-id="be388-115">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="be388-115">b.</span></span> <span data-ttu-id="be388-116">將 [傳遞類型] 選取為 [系統通知 -> 簡易]：這是 Android 的簡易推播通知類型，具備一個標題和一小行文字。</span><span class="sxs-lookup"><span data-stu-id="be388-116">Select the **Delivery type** as *System notification -> Simple*: This is the simple Android push notification type that features a title and a small line of text.</span></span>
   
    <span data-ttu-id="be388-117">c.</span><span class="sxs-lookup"><span data-stu-id="be388-117">c.</span></span> <span data-ttu-id="be388-118">將 [傳遞時間] 選取為 [任何時候]，讓應用程式無論是否啟動，都會接收通知。</span><span class="sxs-lookup"><span data-stu-id="be388-118">Select **Delivery time** as *Any time* to allow the app to receive a notification whether the app is started or not.</span></span>
   
    <span data-ttu-id="be388-119">d.</span><span class="sxs-lookup"><span data-stu-id="be388-119">d.</span></span> <span data-ttu-id="be388-120">在通知文字中，輸入 [標題]，這在推播中會以粗體顯示。</span><span class="sxs-lookup"><span data-stu-id="be388-120">In the notification text type the **Title** which will be in bold in the push.</span></span>
   
    <span data-ttu-id="be388-121">e.</span><span class="sxs-lookup"><span data-stu-id="be388-121">e.</span></span> <span data-ttu-id="be388-122">然後輸入您的 [訊息]。</span><span class="sxs-lookup"><span data-stu-id="be388-122">Then type your **Message**</span></span>
4. <span data-ttu-id="be388-123">向下捲動，在 [內容] 區段中選取 [僅限通知]。</span><span class="sxs-lookup"><span data-stu-id="be388-123">Scroll down, and in the **Content** section, select **Notification only**.</span></span>
   
    ![](./media/mobile-engagement-android-send-push/campaign-content.png)
5. <span data-ttu-id="be388-124">您已完成能做的最基本活動設定。</span><span class="sxs-lookup"><span data-stu-id="be388-124">You're done setting the most basic campaign possible.</span></span> <span data-ttu-id="be388-125">現在再次向下捲動，然後按一下 [建立]  按鈕來儲存活動。</span><span class="sxs-lookup"><span data-stu-id="be388-125">Now scroll down again and click the **Create** button to save your campaign.</span></span>
6. <span data-ttu-id="be388-126">最後一個步驟：按一下 [啟動]  來啟用活動以傳送推播通知。</span><span class="sxs-lookup"><span data-stu-id="be388-126">Last step: click **Activate** to activate your campaign to send push notifications.</span></span>
   
    ![](./media/mobile-engagement-android-send-push/campaign-activate.png)

