### <a name="grant-access-to-your-push-certificate-to-mobile-engagement"></a><span data-ttu-id="1cb6d-101">將推播憑證的存取權授與給 Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="1cb6d-101">Grant access to your Push Certificate to Mobile Engagement</span></span>
<span data-ttu-id="1cb6d-102">若要讓 Mobile Engagement 以您的名義傳送推播通知，您需要授與它對您憑證的存取權。</span><span class="sxs-lookup"><span data-stu-id="1cb6d-102">To allow Mobile Engagement to send Push Notifications on your behalf, you need to grant it access to your certificate.</span></span> <span data-ttu-id="1cb6d-103">這是藉由設定和輸入您的憑證到 Mobile Engagement 入口網站中而完成。</span><span class="sxs-lookup"><span data-stu-id="1cb6d-103">This is done by configuring and entering your certificate into the Mobile Engagement portal.</span></span> <span data-ttu-id="1cb6d-104">請確定您已取得 .p12 憑證，如 [Apple 的文件](https://developer.apple.com/library/prerelease/ios/documentation/IDEs/Conceptual/AppDistributionGuide/AddingCapabilities/AddingCapabilities.html#//apple_ref/doc/uid/TP40012582-CH26-SW6)</span><span class="sxs-lookup"><span data-stu-id="1cb6d-104">Make sure you obtain your .p12 certificate as explained in [Apple's documentation](https://developer.apple.com/library/prerelease/ios/documentation/IDEs/Conceptual/AppDistributionGuide/AddingCapabilities/AddingCapabilities.html#//apple_ref/doc/uid/TP40012582-CH26-SW6)</span></span>

1. <span data-ttu-id="1cb6d-105">瀏覽至您的 Mobile Engagement 入口網站。</span><span class="sxs-lookup"><span data-stu-id="1cb6d-105">Navigate to your Mobile Engagement portal.</span></span> <span data-ttu-id="1cb6d-106">請確認您的所在位置正確無誤，然後按一下底部的 [接洽]  按鈕：</span><span class="sxs-lookup"><span data-stu-id="1cb6d-106">Ensure you're in the correct and then click on the **Engage** button at the bottom:</span></span>
   
    ![](./media/mobile-engagement-ios-send-push/engage-button.png)
2. <span data-ttu-id="1cb6d-107">請在 Engagement 入口網站中按一下 [設定]  頁面。</span><span class="sxs-lookup"><span data-stu-id="1cb6d-107">Click on the **Settings** page in your Engagement Portal.</span></span> <span data-ttu-id="1cb6d-108">從該處按一下 [原生推送]  區段以上傳 p12 憑證：</span><span class="sxs-lookup"><span data-stu-id="1cb6d-108">From there click on the **Native Push** section to upload your p12 certificate:</span></span>
   
    ![](./media/mobile-engagement-ios-send-push/engagement-portal.png)
3. <span data-ttu-id="1cb6d-109">選取您的 p12，將它上傳並輸入您的密碼：</span><span class="sxs-lookup"><span data-stu-id="1cb6d-109">Select your p12, upload it and type your password:</span></span>
   
    ![](./media/mobile-engagement-ios-send-push/native-push-settings.png)

## <span data-ttu-id="1cb6d-110"><a id="send"></a>傳送通知至應用程式</span><span class="sxs-lookup"><span data-stu-id="1cb6d-110"><a id="send"></a>Send a notification to your app</span></span>
<span data-ttu-id="1cb6d-111">現在，我們將建立簡單的推播通知活動，它會傳送推播至我們的應用程式：</span><span class="sxs-lookup"><span data-stu-id="1cb6d-111">We will now create a simple Push Notification campaign that will send a push to our app:</span></span>

1. <span data-ttu-id="1cb6d-112">瀏覽至您的 Mobile Engagement 入口網站中的 [Reach]  索引標籤</span><span class="sxs-lookup"><span data-stu-id="1cb6d-112">Navigate to the **Reach** tab in your Mobile Engagement portal.</span></span>
2. <span data-ttu-id="1cb6d-113">按一下 [新公告]  以建立您的推送行銷活動。</span><span class="sxs-lookup"><span data-stu-id="1cb6d-113">Click **New Announcement** to create your push campaign</span></span>
   
    ![](./media/mobile-engagement-ios-send-push/new-announcement.png)
3. <span data-ttu-id="1cb6d-114">設定行銷活動的第一個欄位：</span><span class="sxs-lookup"><span data-stu-id="1cb6d-114">Setup the first fields of your campaign:</span></span>
   
    ![](./media/mobile-engagement-ios-send-push/campaign-first-params.png)
   
   * <span data-ttu-id="1cb6d-115">提供您的行銷活動 **名稱** 。</span><span class="sxs-lookup"><span data-stu-id="1cb6d-115">Provide a **Name** for your campaign</span></span> 
   * <span data-ttu-id="1cb6d-116">將 [傳遞時間] 選取為 [僅從應用程式外]：這是主要為一些文字的簡單 Apple 推播通知類型。</span><span class="sxs-lookup"><span data-stu-id="1cb6d-116">Select the **Delivery time** as **Out of app only**: this is the simple Apple push notification type that features some text.</span></span>
   * <span data-ttu-id="1cb6d-117">在通知文字中，先輸入將成為推播第一行的 **標題** 。</span><span class="sxs-lookup"><span data-stu-id="1cb6d-117">In the notification text, type first the **Title** which will be the first line in the push.</span></span>
   * <span data-ttu-id="1cb6d-118">然後輸入將成為第二行的 **訊息** 。</span><span class="sxs-lookup"><span data-stu-id="1cb6d-118">Then type your **Message** which will be the second line</span></span>
4. <span data-ttu-id="1cb6d-119">向下捲動，在 [內容] 區段中選取 [僅限通知] </span><span class="sxs-lookup"><span data-stu-id="1cb6d-119">Scroll down, and in the content section select **Notification only**</span></span>
   
    ![](./media/mobile-engagement-ios-send-push/campaign-content.png)
5. <span data-ttu-id="1cb6d-120">您已完成最基本的行銷活動設定。</span><span class="sxs-lookup"><span data-stu-id="1cb6d-120">You're done setting the most basic campaign.</span></span> <span data-ttu-id="1cb6d-121">現在向下捲動，並按一下 [建立]  按鈕，以儲存推播通知行銷活動。</span><span class="sxs-lookup"><span data-stu-id="1cb6d-121">Now scroll down and click on **Create** button to save your push notification campaign.</span></span> 
6. <span data-ttu-id="1cb6d-122">最後，按一下 [啟用]  以傳送推播通知。</span><span class="sxs-lookup"><span data-stu-id="1cb6d-122">Finally - click on **Activate** to send push notification.</span></span> 
   
    ![](./media/mobile-engagement-ios-send-push/campaign-activate.png)
7. <span data-ttu-id="1cb6d-123">您會在 iOS 裝置上的通知中心中收到類似下列的通知：</span><span class="sxs-lookup"><span data-stu-id="1cb6d-123">You will be able receive the notification on your iOS device in the notification center like the following:</span></span>
   
    ![](./media/mobile-engagement-ios-send-push/iphone-notification.png)
8. <span data-ttu-id="1cb6d-124">若您擁有與此 iOS 裝置配對的 Apple Watch，您將會在 Apple Watch 上看見該通知：</span><span class="sxs-lookup"><span data-stu-id="1cb6d-124">If you have an Apple Watch paired with this iOS device then you will see the notification on your Apple Watch:</span></span>
   
    ![](./media/mobile-engagement-ios-send-push/apple-watch.png)

