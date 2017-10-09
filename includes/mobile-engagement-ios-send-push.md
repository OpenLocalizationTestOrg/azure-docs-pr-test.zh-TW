### <a name="grant-access-tooyour-push-certificate-toomobile-engagement"></a><span data-ttu-id="97288-101">授與存取 tooyour 推播憑證 tooMobile Engagement</span><span class="sxs-lookup"><span data-stu-id="97288-101">Grant access tooyour Push Certificate tooMobile Engagement</span></span>
<span data-ttu-id="97288-102">tooallow Mobile Engagement toosend 推播通知您的身分，您需要 toogrant 它存取 tooyour 憑證。</span><span class="sxs-lookup"><span data-stu-id="97288-102">tooallow Mobile Engagement toosend Push Notifications on your behalf, you need toogrant it access tooyour certificate.</span></span> <span data-ttu-id="97288-103">這是藉由設定和 hello Mobile Engagement 入口網站中輸入您的憑證。</span><span class="sxs-lookup"><span data-stu-id="97288-103">This is done by configuring and entering your certificate into hello Mobile Engagement portal.</span></span> <span data-ttu-id="97288-104">請確定您已取得 .p12 憑證，如 [Apple 的文件](https://developer.apple.com/library/prerelease/ios/documentation/IDEs/Conceptual/AppDistributionGuide/AddingCapabilities/AddingCapabilities.html#//apple_ref/doc/uid/TP40012582-CH26-SW6)</span><span class="sxs-lookup"><span data-stu-id="97288-104">Make sure you obtain your .p12 certificate as explained in [Apple's documentation](https://developer.apple.com/library/prerelease/ios/documentation/IDEs/Conceptual/AppDistributionGuide/AddingCapabilities/AddingCapabilities.html#//apple_ref/doc/uid/TP40012582-CH26-SW6)</span></span>

1. <span data-ttu-id="97288-105">瀏覽 tooyour Mobile Engagement 入口網站。</span><span class="sxs-lookup"><span data-stu-id="97288-105">Navigate tooyour Mobile Engagement portal.</span></span> <span data-ttu-id="97288-106">請確定您使用正確的 hello，然後按一下hello **Engage** hello 底部的按鈕：</span><span class="sxs-lookup"><span data-stu-id="97288-106">Ensure you're in hello correct and then click on hello **Engage** button at hello bottom:</span></span>
   
    ![](./media/mobile-engagement-ios-send-push/engage-button.png)
2. <span data-ttu-id="97288-107">按一下 hello**設定**Engagement 入口網站頁面。</span><span class="sxs-lookup"><span data-stu-id="97288-107">Click on hello **Settings** page in your Engagement Portal.</span></span> <span data-ttu-id="97288-108">從該處，按一下 hello**原生推送**區段 tooupload p12 憑證：</span><span class="sxs-lookup"><span data-stu-id="97288-108">From there click on hello **Native Push** section tooupload your p12 certificate:</span></span>
   
    ![](./media/mobile-engagement-ios-send-push/engagement-portal.png)
3. <span data-ttu-id="97288-109">選取您的 p12，將它上傳並輸入您的密碼：</span><span class="sxs-lookup"><span data-stu-id="97288-109">Select your p12, upload it and type your password:</span></span>
   
    ![](./media/mobile-engagement-ios-send-push/native-push-settings.png)

## <span data-ttu-id="97288-110"><a id="send"></a>傳送通知 tooyour 應用程式</span><span class="sxs-lookup"><span data-stu-id="97288-110"><a id="send"></a>Send a notification tooyour app</span></span>
<span data-ttu-id="97288-111">現在，我們將建立簡單的推播通知活動，則會傳送推播 tooour 應用程式：</span><span class="sxs-lookup"><span data-stu-id="97288-111">We will now create a simple Push Notification campaign that will send a push tooour app:</span></span>

1. <span data-ttu-id="97288-112">瀏覽 toohello**到達** 索引標籤中您的 Mobile Engagement 入口網站。</span><span class="sxs-lookup"><span data-stu-id="97288-112">Navigate toohello **Reach** tab in your Mobile Engagement portal.</span></span>
2. <span data-ttu-id="97288-113">按一下**新的 Announcement** toocreate 您的推播宣傳活動</span><span class="sxs-lookup"><span data-stu-id="97288-113">Click **New Announcement** toocreate your push campaign</span></span>
   
    ![](./media/mobile-engagement-ios-send-push/new-announcement.png)
3. <span data-ttu-id="97288-114">安裝程式 hello 第一個欄位的活動：</span><span class="sxs-lookup"><span data-stu-id="97288-114">Setup hello first fields of your campaign:</span></span>
   
    ![](./media/mobile-engagement-ios-send-push/campaign-first-params.png)
   
   * <span data-ttu-id="97288-115">提供您的行銷活動 **名稱** 。</span><span class="sxs-lookup"><span data-stu-id="97288-115">Provide a **Name** for your campaign</span></span> 
   * <span data-ttu-id="97288-116">選取 hello**傳遞時間**為**不在應用程式只**： 這是 hello 簡單 Apple 推播通知類型具有一些文字。</span><span class="sxs-lookup"><span data-stu-id="97288-116">Select hello **Delivery time** as **Out of app only**: this is hello simple Apple push notification type that features some text.</span></span>
   * <span data-ttu-id="97288-117">在 hello 通知文字中，輸入第一個 hello**標題**供 hello hello 推入中的第一行。</span><span class="sxs-lookup"><span data-stu-id="97288-117">In hello notification text, type first hello **Title** which will be hello first line in hello push.</span></span>
   * <span data-ttu-id="97288-118">然後輸入您**訊息**供 hello 第二行</span><span class="sxs-lookup"><span data-stu-id="97288-118">Then type your **Message** which will be hello second line</span></span>
4. <span data-ttu-id="97288-119">向下捲動，並在 hello 內容區段選取**僅限通知**</span><span class="sxs-lookup"><span data-stu-id="97288-119">Scroll down, and in hello content section select **Notification only**</span></span>
   
    ![](./media/mobile-engagement-ios-send-push/campaign-content.png)
5. <span data-ttu-id="97288-120">您已完成設定 hello 最基本活動。</span><span class="sxs-lookup"><span data-stu-id="97288-120">You're done setting hello most basic campaign.</span></span> <span data-ttu-id="97288-121">現在向下捲動並按一下**建立**按鈕 toosave 您推播通知的活動。</span><span class="sxs-lookup"><span data-stu-id="97288-121">Now scroll down and click on **Create** button toosave your push notification campaign.</span></span> 
6. <span data-ttu-id="97288-122">最後-按一下**Activate** toosend 推播通知。</span><span class="sxs-lookup"><span data-stu-id="97288-122">Finally - click on **Activate** toosend push notification.</span></span> 
   
    ![](./media/mobile-engagement-ios-send-push/campaign-activate.png)
7. <span data-ttu-id="97288-123">您可以在 hello 如下的 hello 通知中心收到 hello 通知，在您的 iOS 裝置上：</span><span class="sxs-lookup"><span data-stu-id="97288-123">You will be able receive hello notification on your iOS device in hello notification center like hello following:</span></span>
   
    ![](./media/mobile-engagement-ios-send-push/iphone-notification.png)
8. <span data-ttu-id="97288-124">如果您有搭配此 iOS 裝置的 Apple Watch 您會在 Apple Watch 上看到 hello 通知：</span><span class="sxs-lookup"><span data-stu-id="97288-124">If you have an Apple Watch paired with this iOS device then you will see hello notification on your Apple Watch:</span></span>
   
    ![](./media/mobile-engagement-ios-send-push/apple-watch.png)

