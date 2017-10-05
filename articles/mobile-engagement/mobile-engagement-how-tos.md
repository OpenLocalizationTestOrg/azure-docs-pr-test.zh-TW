---
title: "Azure Mobile Engagement 使用者介面：觸達作法"
description: "Azure Mobile Engagement 的使用者介面概觀"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: 30af87e6-c816-4cce-8609-6cbd3e83de14
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 33a0a9d0c399cb7f0a791c4c16dde2e2d62364ca
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-get-started-using-and-managing-pushes-to-reach-out-to-your-end-users"></a><span data-ttu-id="08d4e-103">如何開始使用及管理推送通知以推送給使用者</span><span class="sxs-lookup"><span data-stu-id="08d4e-103">How to get started using and managing pushes to reach out to your end users</span></span>
<span data-ttu-id="08d4e-104">一旦 SDK 完全整合至應用程式後，您便可以開始使用 UI 的 [Reach] 區段，將通知推送給應用程式使用者。</span><span class="sxs-lookup"><span data-stu-id="08d4e-104">Once the SDK is fully integrated into your app, you can get started using the the Reach section of the UI to Push notifications to the users of your app.</span></span>  

## <a name="do-your-first-push-notification-campaign"></a><span data-ttu-id="08d4e-105">進行第一個推送通知活動</span><span class="sxs-lookup"><span data-stu-id="08d4e-105">Do Your First Push Notification Campaign</span></span>
* <span data-ttu-id="08d4e-106">確認您的 Reach 已藉由 SDK 整合到應用程式。</span><span class="sxs-lookup"><span data-stu-id="08d4e-106">Confirm that your Reach is integrated into your app with the SDK.</span></span> 
* <span data-ttu-id="08d4e-107">選取您的應用程式</span><span class="sxs-lookup"><span data-stu-id="08d4e-107">Select your application</span></span>

![First1][1]

* <span data-ttu-id="08d4e-109">前往 [Reach] 區段，並按一下 [新公告]</span><span class="sxs-lookup"><span data-stu-id="08d4e-109">Go to the "Reach" Section and Click "New announcement"</span></span>

![First2][2]

* <span data-ttu-id="08d4e-111">建立新的活動並將它命名</span><span class="sxs-lookup"><span data-stu-id="08d4e-111">Create a new campaign and name it</span></span>
  
![First3][3]

* <span data-ttu-id="08d4e-113">選取如何應該傳送通知，做為僅限應用程式內</span><span class="sxs-lookup"><span data-stu-id="08d4e-113">Select how the notification should be delivered, as In-app only</span></span>

![First4][4]

* <span data-ttu-id="08d4e-115">建立您想要推送的訊息</span><span class="sxs-lookup"><span data-stu-id="08d4e-115">Create the message you want to push</span></span>

![First5][5]

* <span data-ttu-id="08d4e-117">您可以撰寫通知標題 (選擇性)。</span><span class="sxs-lookup"><span data-stu-id="08d4e-117">You may write a title on the notification (Optional).</span></span>
* <span data-ttu-id="08d4e-118">撰寫推送訊息內容。</span><span class="sxs-lookup"><span data-stu-id="08d4e-118">Write push message content.</span></span>
* <span data-ttu-id="08d4e-119">您可以上傳影像。</span><span class="sxs-lookup"><span data-stu-id="08d4e-119">You can upload an image.</span></span> <span data-ttu-id="08d4e-120">請注意，檔案的大小不能超過 32,768 個位元組。</span><span class="sxs-lookup"><span data-stu-id="08d4e-120">Be aware that the size of the file cannot exceed 32,768 bytes.</span></span>
* <span data-ttu-id="08d4e-121">您也可以選取進一步的選項，但是由於本教學課程的焦點，我們稍後會看到。</span><span class="sxs-lookup"><span data-stu-id="08d4e-121">You also have the ability to select further options, but for the focus of this tutorial, we will see that later.</span></span>
* <span data-ttu-id="08d4e-122">將內容類型選取為僅限通知</span><span class="sxs-lookup"><span data-stu-id="08d4e-122">Select the content type as Notification only</span></span>

![First6][6]

* <span data-ttu-id="08d4e-124">建立推送活動，它會顯示在活動清單。</span><span class="sxs-lookup"><span data-stu-id="08d4e-124">Create your push campaign and it will appear in your campaign list.</span></span>

![First7][7]

## <a name="test-your-push-notification-campaign"></a><span data-ttu-id="08d4e-126">測試推送通知活動</span><span class="sxs-lookup"><span data-stu-id="08d4e-126">Test Your Push Notification Campaign</span></span>
![Test1][8]

* <span data-ttu-id="08d4e-128">登記裝置。</span><span class="sxs-lookup"><span data-stu-id="08d4e-128">Register your device.</span></span>
* <span data-ttu-id="08d4e-129">按一下您想要推送的裝置的核取方塊。</span><span class="sxs-lookup"><span data-stu-id="08d4e-129">Click on the checkbox of the device you want to push.</span></span>
* <span data-ttu-id="08d4e-130">按一下 [測試] 按鈕以傳送推送到裝置。</span><span class="sxs-lookup"><span data-stu-id="08d4e-130">Click on the "Test" button to send the push to the device.</span></span>

![Test2][9]

* <span data-ttu-id="08d4e-132">啟動活動</span><span class="sxs-lookup"><span data-stu-id="08d4e-132">Activate the campaign</span></span>

![Test3][10]

* <span data-ttu-id="08d4e-134">既然您已建立活動，就只需要啟動它，以便將通知推送給您的使用者。</span><span class="sxs-lookup"><span data-stu-id="08d4e-134">Now that you have created your campaign you just need to activate it for the notification to be pushed to your users.</span></span>

## <a name="send-personalized-pushes"></a><span data-ttu-id="08d4e-135">傳送個人化的推送</span><span class="sxs-lookup"><span data-stu-id="08d4e-135">Send Personalized Pushes</span></span>
* <span data-ttu-id="08d4e-136">這個範例會建立推送，其中自訂的退款程式碼已輸入到推送通知中。</span><span class="sxs-lookup"><span data-stu-id="08d4e-136">This example creates a push where a custom rebate code is entered into the push notification.</span></span>

![Personalize1][11]

<span data-ttu-id="08d4e-138">個人化運作方式是取代應用程式資訊標記中的標記，因此，您必須確定使用者已先定義適當的應用程式資訊。</span><span class="sxs-lookup"><span data-stu-id="08d4e-138">Personalization works by replacing a marker by from an app info tag so, you'll have to make sure the user has the proper app-info defined first.</span></span> <span data-ttu-id="08d4e-139">在此範例中，目標使用者已定義名為 rebate_code 的應用程式資訊標記。</span><span class="sxs-lookup"><span data-stu-id="08d4e-139">In this example the targeted users will have an app info tag named rebate_code defined.</span></span>
<span data-ttu-id="08d4e-140">如您所見，在推送通知內容上方包含標記 ${rebate_code}，這表示它將由應用程式資訊標記的實際內容所取代。</span><span class="sxs-lookup"><span data-stu-id="08d4e-140">As you see above the push notification content includes the marker ${rebate_code} which will indicate that it is to be replaced by the actual content of the app info tag.</span></span>

> [!WARNING]
> <span data-ttu-id="08d4e-141">如果未定義使用者的應用程式資訊標記，使用者將不會收到推送。</span><span class="sxs-lookup"><span data-stu-id="08d4e-141">If the app info tag is not defined for the user, the user will not receive the push.</span></span>

* <span data-ttu-id="08d4e-142">結果</span><span class="sxs-lookup"><span data-stu-id="08d4e-142">Result</span></span>

![Personalize2][12]

### <a name="you-can-further-personalize-the-text-your-notification"></a><span data-ttu-id="08d4e-144">您可以進一步個人化通知的文字</span><span class="sxs-lookup"><span data-stu-id="08d4e-144">You can further personalize the text your notification</span></span>
![Personalize3][13]

* <span data-ttu-id="08d4e-146">包括通知的標題，</span><span class="sxs-lookup"><span data-stu-id="08d4e-146">Including the title of the notification,</span></span>
* <span data-ttu-id="08d4e-147">與訊息的內容。</span><span class="sxs-lookup"><span data-stu-id="08d4e-147">And the content of the message.</span></span>
* <span data-ttu-id="08d4e-148">選擇公告的類型 (文字檢視或網頁檢視)</span><span class="sxs-lookup"><span data-stu-id="08d4e-148">Choose the type of announcement (Text view or Web view)</span></span>

![Personalize4][14]

### <a name="the-body-of-an-announcement-may-also-be-personalized-with"></a><span data-ttu-id="08d4e-150">公告的內文也可以個人化：</span><span class="sxs-lookup"><span data-stu-id="08d4e-150">The body of an announcement may also be personalized with:</span></span>
* <span data-ttu-id="08d4e-151">動作 URL，如果您想要自訂登陸頁面的話</span><span class="sxs-lookup"><span data-stu-id="08d4e-151">The action URL, should you want to customize the landing page</span></span>
* <span data-ttu-id="08d4e-152">標題，</span><span class="sxs-lookup"><span data-stu-id="08d4e-152">The title,</span></span>
* <span data-ttu-id="08d4e-153">訊息內文。</span><span class="sxs-lookup"><span data-stu-id="08d4e-153">The body of the message.</span></span>

## <a name="differentiate-your-push-notification-in-or-out-of-app"></a><span data-ttu-id="08d4e-154">區分您的推送通知 (在應用程式內外)</span><span class="sxs-lookup"><span data-stu-id="08d4e-154">Differentiate Your Push Notification (in or out of app)</span></span>
* <span data-ttu-id="08d4e-155">選擇您要推送的通知類型、選取您的應用程式、前往 [Reach] 區段、選取或建立推送活動，然後前往 [通知] 區段。</span><span class="sxs-lookup"><span data-stu-id="08d4e-155">Choose the type of notification you will push, select your application, go to the "Reach" section, select or create a push campaign and go to the "Notification" section.</span></span>
* <span data-ttu-id="08d4e-156">按一下您要的「傳遞模式」。</span><span class="sxs-lookup"><span data-stu-id="08d4e-156">Click on the "delivery mode" you want.</span></span>
* <span data-ttu-id="08d4e-157">如果您希望通知發生在特定活動 (畫面)，便按一下 [限制活動] 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="08d4e-157">Click on the "Restrict Activities" checkbox when you want the notification occurs on specific activities (screens).</span></span>

![Differentiate1][15]

### <a name="out-of-app-only-delivery-mode"></a><span data-ttu-id="08d4e-159">「僅限應用程式外」傳遞模式</span><span class="sxs-lookup"><span data-stu-id="08d4e-159">"Out of App Only" delivery mode</span></span>
![Differentiate2][16]

<span data-ttu-id="08d4e-161">「僅限應用程式外」傳遞模式會在應用程式關閉時提供推送通知。</span><span class="sxs-lookup"><span data-stu-id="08d4e-161">"Out of App Only" delivery mode provides push notification when the application is closed.</span></span> <span data-ttu-id="08d4e-162">這是標準的推送通知。</span><span class="sxs-lookup"><span data-stu-id="08d4e-162">This is the standard push notification.</span></span>
<span data-ttu-id="08d4e-163">當您選取「僅限應用程式外」時，您必須已提供應用程式建置所在平台 (APN 或 GCM) 上的憑證。</span><span class="sxs-lookup"><span data-stu-id="08d4e-163">When you select "out of app only" ,you must have already provided the certificates from the platform that your application is building on (APNS or GCM).</span></span>

### <a name="see-also"></a><span data-ttu-id="08d4e-164">另請參閱</span><span class="sxs-lookup"><span data-stu-id="08d4e-164">See also</span></span>
* <span data-ttu-id="08d4e-165">[Apple Push Notification Service – 憑證](http://developer.apple.com/library/mac/#documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/ApplePushService/ApplePushService.html#//apple_ref/doc/uid/TP40008194-CH100-SW9)、[Google 雲端通訊 – 憑證](http://developer.android.com/google/gcm/index.html)</span><span class="sxs-lookup"><span data-stu-id="08d4e-165">[Apple Push Notification Service – Certificates](http://developer.apple.com/library/mac/#documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/ApplePushService/ApplePushService.html#//apple_ref/doc/uid/TP40008194-CH100-SW9), [Google Cloud Messaging – Certificate](http://developer.android.com/google/gcm/index.html)</span></span> 

### <a name="in-app-only-delivery-mode"></a><span data-ttu-id="08d4e-166">「僅限應用程式內」傳遞模式</span><span class="sxs-lookup"><span data-stu-id="08d4e-166">"in-App Only" delivery mode</span></span>
![Differentiate3][17]

<span data-ttu-id="08d4e-168">「僅限應用程式內」傳遞模式會在應用程式執行時提供推送通知。</span><span class="sxs-lookup"><span data-stu-id="08d4e-168">"In-App Only" delivery mode provides push notification when the application is running.</span></span>
<span data-ttu-id="08d4e-169">針對此通知，您不需要經歷 APNS 和 GCM 系統。</span><span class="sxs-lookup"><span data-stu-id="08d4e-169">For this notification, you do not need to go through the APNS and GCM system.</span></span>
<span data-ttu-id="08d4e-170">您可以使用應用程式內傳遞系統來觸達使用者。</span><span class="sxs-lookup"><span data-stu-id="08d4e-170">You can use the in-app delivery system to reach your end-users.</span></span>
<span data-ttu-id="08d4e-171">您完全可以自訂通知，並決定通知將會出現在哪個活動 (畫面)。</span><span class="sxs-lookup"><span data-stu-id="08d4e-171">You can fully customize the notification and decide in which activity (screen) the notification will appear.</span></span>

### <a name="anytime-delivery-mode"></a><span data-ttu-id="08d4e-172">「隨時」傳遞模式</span><span class="sxs-lookup"><span data-stu-id="08d4e-172">"Anytime" delivery mode</span></span>
<span data-ttu-id="08d4e-173">您可以選擇「隨時」傳遞模式，確保您不論應用程式是否正在執行都可觸達使用者。</span><span class="sxs-lookup"><span data-stu-id="08d4e-173">You can choose an "Anytime" delivery mode, ensures you to reach your end-user whether the application is running or not.</span></span>
<span data-ttu-id="08d4e-174">當您選取「隨時」時，您必須已提供應用程式建置所在平台 (APN 或 GCM) 上的憑證。</span><span class="sxs-lookup"><span data-stu-id="08d4e-174">When you select "Anytime" , you must have already provided the certificates from the platform that your application is building upon (APNS or GCM).</span></span> 

## <a name="schedule-a-push-campaign"></a><span data-ttu-id="08d4e-175">排定推送活動</span><span class="sxs-lookup"><span data-stu-id="08d4e-175">Schedule a Push Campaign</span></span>
### <a name="plan-to-start-a-campaign"></a><span data-ttu-id="08d4e-176">計畫開始活動</span><span class="sxs-lookup"><span data-stu-id="08d4e-176">Plan to Start a campaign</span></span>
![Shedule1][18]

<span data-ttu-id="08d4e-178">時間是 3 月 21 日，您要進行公告，且計畫是在 3 月 22 日午夜。</span><span class="sxs-lookup"><span data-stu-id="08d4e-178">It is the 21st of March and you have an announcement to make and planed for the 22nd of March at midnight.</span></span> <span data-ttu-id="08d4e-179">您不需要待在介面前就可以推送！</span><span class="sxs-lookup"><span data-stu-id="08d4e-179">You don’t have to stay in front of the interface to do a push!</span></span> <span data-ttu-id="08d4e-180">您可以事先規劃確切在哪一分鐘會傳送通知。</span><span class="sxs-lookup"><span data-stu-id="08d4e-180">You can plan in advance the exact minute notifications will be sent.</span></span>

* <span data-ttu-id="08d4e-181">取消核取 [無] 核取方塊，然後選取開始時間</span><span class="sxs-lookup"><span data-stu-id="08d4e-181">Un-check the "None" checkbox and select a start time</span></span> 
* <span data-ttu-id="08d4e-182">選擇您想要開始推送活動的日期與時間。</span><span class="sxs-lookup"><span data-stu-id="08d4e-182">Choose the date and the time you want to start the push campaign.</span></span>

### <a name="plan-to-end-a-campaign"></a><span data-ttu-id="08d4e-183">計畫結束活動</span><span class="sxs-lookup"><span data-stu-id="08d4e-183">Plan to end a campaign</span></span>
![Shedule2][19]

<span data-ttu-id="08d4e-185">您想要在 3 月 25 日下午 3 點停止活動，但您知道您到時候不會在場。</span><span class="sxs-lookup"><span data-stu-id="08d4e-185">You want your campaign to stop on the 25th of March at 3.00 pm but you know you won't be there to do it.</span></span>
<span data-ttu-id="08d4e-186">您不需要待在介面前就可以推送！</span><span class="sxs-lookup"><span data-stu-id="08d4e-186">You don’t have to stay in front of the interface to push!</span></span> <span data-ttu-id="08d4e-187">您可以事先規劃活動確切在哪一分鐘停止。</span><span class="sxs-lookup"><span data-stu-id="08d4e-187">You can plan in advance the exact minute your campaign will stop.</span></span>

* <span data-ttu-id="08d4e-188">按一下 [無] 核取方塊，或選取結束時間</span><span class="sxs-lookup"><span data-stu-id="08d4e-188">Click on the "None" checkbox or select a end time</span></span>
* <span data-ttu-id="08d4e-189">選擇您想要完成推送活動的日期與時間。</span><span class="sxs-lookup"><span data-stu-id="08d4e-189">Choose the date and the time you want to finish the push campaign.</span></span>

### <a name="end-a-campaign-manually"></a><span data-ttu-id="08d4e-190">手動結束活動</span><span class="sxs-lookup"><span data-stu-id="08d4e-190">End a campaign manually</span></span>
![Shedule3][20]

<span data-ttu-id="08d4e-192">根據預設，已選取 [無] 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="08d4e-192">By default, the "None" check-boxes are selected.</span></span>
<span data-ttu-id="08d4e-193">這表示只要在 [Reach] 區段啟動活動它便會開始，在 [Reach] 區段停止它便會結束。</span><span class="sxs-lookup"><span data-stu-id="08d4e-193">This means that the campaign will start as soon as you activate it in the reach section and will end when you will stop it on the reach section.</span></span>

> [!NOTE]
> <span data-ttu-id="08d4e-194">建立時未設定結束日期的活動會將推送儲存在本機裝置上，並在下一次應用程式開啟時顯示，即使活動已手動結束。</span><span class="sxs-lookup"><span data-stu-id="08d4e-194">Campaigns created without an end date store the push locally on the device and show it the next time the app is opened even if the campaign is manually ended.</span></span>

## <a name="enhance-a-push-notification-with-a-text-view"></a><span data-ttu-id="08d4e-195">使用文字檢視增強推送通知</span><span class="sxs-lookup"><span data-stu-id="08d4e-195">Enhance a Push Notification with a Text View</span></span>
### <a name="what-is-a-text-view"></a><span data-ttu-id="08d4e-196">什麼是文字檢視？</span><span class="sxs-lookup"><span data-stu-id="08d4e-196">What is a Text View?</span></span>
![TextView1][21]

<span data-ttu-id="08d4e-198">文字檢視是具有文字內容的快顯視窗。</span><span class="sxs-lookup"><span data-stu-id="08d4e-198">A text view is a pop-up with text content.</span></span> <span data-ttu-id="08d4e-199">使用者按下推送通知之後，就會出現這個快顯視窗。</span><span class="sxs-lookup"><span data-stu-id="08d4e-199">This pop-up appears after the end-user has clicked on the push notification.</span></span>
<span data-ttu-id="08d4e-200">文字檢視可讓您呈現更多的內容給使用者。</span><span class="sxs-lookup"><span data-stu-id="08d4e-200">A text view allows you to present more content to your end-user.</span></span> <span data-ttu-id="08d4e-201">這也是呈現動作呼叫的機會，例如跳至您的應用程式頁面、重新導向至市集、開啟網頁、傳送電子郵件、開始地理當地語系化的搜尋等等...</span><span class="sxs-lookup"><span data-stu-id="08d4e-201">This is also the opportunity to present a call to action such as jumping to a page of your app, redirecting to a Store, opening a web page, sending an e-mail, starting a geo-localized search, etc...</span></span>

### <a name="example-text-view"></a><span data-ttu-id="08d4e-202">範例：文字檢視</span><span class="sxs-lookup"><span data-stu-id="08d4e-202">Example: Text View</span></span>
* <span data-ttu-id="08d4e-203">在 [Reach] 區段中建立推送通知活動，並為您的活動指定名稱。</span><span class="sxs-lookup"><span data-stu-id="08d4e-203">Create your Push notification campaign in the "Reach" section and give your campaign a name</span></span>

![TextView2][22]

* <span data-ttu-id="08d4e-205">撰寫將出現在通知的訊息。</span><span class="sxs-lookup"><span data-stu-id="08d4e-205">Write the message that will appear on the notification.</span></span>
* <span data-ttu-id="08d4e-206">將 [公告內容類型] 選取為 [文字]</span><span class="sxs-lookup"><span data-stu-id="08d4e-206">Select the Announcement Content Type of “text”</span></span>

![TextView3][23]

> [!NOTE]
> <span data-ttu-id="08d4e-208">當您推送文字檢視時，它一律是先有通知。</span><span class="sxs-lookup"><span data-stu-id="08d4e-208">When you push a text view, it always comes with a notification first.</span></span> 

* <span data-ttu-id="08d4e-209">定義文字 (選取文字公告內容之後，子區段會出現，可讓您定義您想要顯示的文字)。</span><span class="sxs-lookup"><span data-stu-id="08d4e-209">Define the text (After having selected the text announcement content, the sub-section will appear, allowing you to define the text you want to be displayed.)</span></span>

![TextView4][24]

* <span data-ttu-id="08d4e-211">撰寫將出現在訊息頂端的標題。</span><span class="sxs-lookup"><span data-stu-id="08d4e-211">Write the title that will appear at the top of the message.</span></span>
* <span data-ttu-id="08d4e-212">撰寫文字檢視的主要內容。</span><span class="sxs-lookup"><span data-stu-id="08d4e-212">Write the main content of the text view.</span></span>
* <span data-ttu-id="08d4e-213">撰寫將出現在動作按鈕的內容 (動作按鈕可讓應用程式做出特定的動作，例如開啟應用程式頁面、重新導向至應用程式市集，或您可以提供的任何類型來源)。</span><span class="sxs-lookup"><span data-stu-id="08d4e-213">Write the content that will appear on the action button (an action button enables the application to make a specific action such as opening a page of the application, redirecting to an App store or any kind of sources you can provide).</span></span>
* <span data-ttu-id="08d4e-214">撰寫將出現在結束按鈕的內容 (藉由按一下結束按鈕，文字檢視將會消失)。</span><span class="sxs-lookup"><span data-stu-id="08d4e-214">Write the content that will appear on the exit button (by clicking on the exit button, the text view will disappear.)</span></span>
* <span data-ttu-id="08d4e-215">建立推送通知活動，它會顯示在活動清單。</span><span class="sxs-lookup"><span data-stu-id="08d4e-215">Create your push notification campaign and it will appear on the campaign list.</span></span>

![TextView5][25]

* <span data-ttu-id="08d4e-217">啟動推送通知活動，將文字檢視傳送給使用者。</span><span class="sxs-lookup"><span data-stu-id="08d4e-217">Activate your push notification campaign to send the text view to your users.</span></span>

![TextView6][26]

* <span data-ttu-id="08d4e-219">結果</span><span class="sxs-lookup"><span data-stu-id="08d4e-219">Result</span></span>

![TextView7][27]

* <span data-ttu-id="08d4e-221">使用者會收到通知並按一下它。</span><span class="sxs-lookup"><span data-stu-id="08d4e-221">The user receives the notification and click on it.</span></span>
* <span data-ttu-id="08d4e-222">文字檢視顯示為快顯視窗，讓使用者能夠與它互動。</span><span class="sxs-lookup"><span data-stu-id="08d4e-222">The text view appears as a pop-up allowing the user to interact with it.</span></span>

## <a name="enhance-a-push-notification-with-a-web-view"></a><span data-ttu-id="08d4e-223">使用網頁檢視增強推送通知</span><span class="sxs-lookup"><span data-stu-id="08d4e-223">Enhance a Push Notification with a Web View</span></span>
### <a name="what-is-a-web-view"></a><span data-ttu-id="08d4e-224">什麼是網頁檢視？</span><span class="sxs-lookup"><span data-stu-id="08d4e-224">What is a Web View?</span></span>
![WebView1][28]

<span data-ttu-id="08d4e-226">網頁檢視是具有網頁內容的快顯視窗。</span><span class="sxs-lookup"><span data-stu-id="08d4e-226">A web view is a pop-up with web content.</span></span> <span data-ttu-id="08d4e-227">使用者按下推播通知時，就會出現這個快顯視窗。</span><span class="sxs-lookup"><span data-stu-id="08d4e-227">This pop-up appears when the end-user has clicked on the push notification.</span></span>
<span data-ttu-id="08d4e-228">網頁檢視可讓您與使用者有更多互動。</span><span class="sxs-lookup"><span data-stu-id="08d4e-228">A web view allows you to have more interaction with the end-user.</span></span>
<span data-ttu-id="08d4e-229">這也是呈現動作呼叫的機會，例如重新導向至應用程式市集、開啟網頁、傳送電子郵件、開始地理當地語系化的搜尋等等...</span><span class="sxs-lookup"><span data-stu-id="08d4e-229">This is also the opportunity to present a call to action such as redirection to App Store, opening a web page, sending an e-mail, starting a geo-localized search, etc...</span></span>

### <a name="example-web-view"></a><span data-ttu-id="08d4e-230">範例：網頁檢視</span><span class="sxs-lookup"><span data-stu-id="08d4e-230">Example: Web View</span></span>
* <span data-ttu-id="08d4e-231">在 [Reach] 區段中建立推送活動，並為您的活動指定名稱。</span><span class="sxs-lookup"><span data-stu-id="08d4e-231">Create your Push campaign in the "Reach" section and give your campaign a name.</span></span>

![WebView2][29]

* <span data-ttu-id="08d4e-233">撰寫將出現在通知的訊息。</span><span class="sxs-lookup"><span data-stu-id="08d4e-233">Write the message that will appear on the notification.</span></span>
* <span data-ttu-id="08d4e-234">將 [公告內容類型] 選取為 [網頁]</span><span class="sxs-lookup"><span data-stu-id="08d4e-234">Select the Announcement Content Type as “web”</span></span>

![WebView3][30]

### <a name="about-announcement-types"></a><span data-ttu-id="08d4e-236">關於公告類型：</span><span class="sxs-lookup"><span data-stu-id="08d4e-236">About Announcement types:</span></span>
* <span data-ttu-id="08d4e-237">僅通知：這是簡單的標準通知。</span><span class="sxs-lookup"><span data-stu-id="08d4e-237">Notification only: It is a simple standard notification.</span></span> <span data-ttu-id="08d4e-238">表示如果使用者按一下通知，不會出現任何其他檢視，但是會發生與它關聯的動作。</span><span class="sxs-lookup"><span data-stu-id="08d4e-238">Meaning that if a user clicks on it, no additional view will appear, but only the action associated to it will occur.</span></span>
* <span data-ttu-id="08d4e-239">文字通知：這是一種吸引使用者查看文字檢視的通知。</span><span class="sxs-lookup"><span data-stu-id="08d4e-239">Text announcement: It is a notification that engages the user to have a look at a text view.</span></span>
* <span data-ttu-id="08d4e-240">Web 通知：這是一種吸引使用者查看 Web 檢視的通知。</span><span class="sxs-lookup"><span data-stu-id="08d4e-240">Web announcement: It is a notification that engages the user to have a look at a web view.</span></span>
  <span data-ttu-id="08d4e-241">選取「網頁公告」內容。</span><span class="sxs-lookup"><span data-stu-id="08d4e-241">Select the "Web announcement" content.</span></span>

> [!NOTE]
> <span data-ttu-id="08d4e-242">當您推送網頁檢視時，它一律是先有通知。</span><span class="sxs-lookup"><span data-stu-id="08d4e-242">When you push a web view, it always comes with a notification first.</span></span>

* <span data-ttu-id="08d4e-243">定義網頁內容 (選取網頁公告內容之後，子區段會出現，可讓您定義您想要顯示的網頁檢視內容)。</span><span class="sxs-lookup"><span data-stu-id="08d4e-243">Define the web content (After having selected the web announcement content, the subsection will appear, allowing you to define the web view content you want to be displayed.)</span></span>

![WebView4][31]

* <span data-ttu-id="08d4e-245">撰寫將出現在訊息頂端的標題 (選擇性)。</span><span class="sxs-lookup"><span data-stu-id="08d4e-245">Write the title that will appear at the top of the message (optional).</span></span>
* <span data-ttu-id="08d4e-246">在這裡撰寫您的 HTML 程式碼。</span><span class="sxs-lookup"><span data-stu-id="08d4e-246">Write your HTML code here.</span></span>
* <span data-ttu-id="08d4e-247">按一下 [原始碼編輯模式] 按鈕以切換版本，並查看其外觀。</span><span class="sxs-lookup"><span data-stu-id="08d4e-247">Click on the source editing mode button to switch edition and see how it looks like.</span></span>
* <span data-ttu-id="08d4e-248">撰寫將出現在動作按鈕的內容 (動作按鈕可讓應用程式做出特定的動作，例如開啟應用程式頁面、重新導向至市集，或您可以提供的任何類型來源)。</span><span class="sxs-lookup"><span data-stu-id="08d4e-248">Write the content that will appear on the action button (an action button enables the application to make a specific action such as opening a page of the application, redirecting to a Store or any kind of sources you can provide).</span></span>
* <span data-ttu-id="08d4e-249">撰寫將出現在結束按鈕的內容 (藉由按一下結束按鈕，網頁檢視將會消失)。</span><span class="sxs-lookup"><span data-stu-id="08d4e-249">Write the content that will appear on the exit button (by clicking on the exit button, the web view will disappear).</span></span>
* <span data-ttu-id="08d4e-250">結果</span><span class="sxs-lookup"><span data-stu-id="08d4e-250">Result</span></span>

![WebView5][32]

* <span data-ttu-id="08d4e-252">使用者會收到通知，並按一下它。</span><span class="sxs-lookup"><span data-stu-id="08d4e-252">The user receive the notification and click on it.</span></span>
* <span data-ttu-id="08d4e-253">文字檢視顯示為快顯視窗，讓使用者能夠與它互動。</span><span class="sxs-lookup"><span data-stu-id="08d4e-253">The text view appears as a pop-up allowing the user to interact with it.</span></span>

<!--Image references-->
[1]: ./media/mobile-engagement-how-tos/First1.png
[2]: ./media/mobile-engagement-how-tos/First2.png
[3]: ./media/mobile-engagement-how-tos/First3.png
[4]: ./media/mobile-engagement-how-tos/First4.png
[5]: ./media/mobile-engagement-how-tos/First5.png
[6]: ./media/mobile-engagement-how-tos/First6.png
[7]: ./media/mobile-engagement-how-tos/First7.png
[8]: ./media/mobile-engagement-how-tos/Test1.png
[9]: ./media/mobile-engagement-how-tos/Test2.png
[10]: ./media/mobile-engagement-how-tos/Test3.png
[11]: ./media/mobile-engagement-how-tos/Personalize1.png
[12]: ./media/mobile-engagement-how-tos/Personalize2.png
[13]: ./media/mobile-engagement-how-tos/Personalize3.png
[14]: ./media/mobile-engagement-how-tos/Personalize4.png
[15]: ./media/mobile-engagement-how-tos/Differentiate1.png
[16]: ./media/mobile-engagement-how-tos/Differentiate2.png
[17]: ./media/mobile-engagement-how-tos/Differentiate3.png
[18]: ./media/mobile-engagement-how-tos/Schedule1.png
[19]: ./media/mobile-engagement-how-tos/Schedule2.png
[20]: ./media/mobile-engagement-how-tos/Schedule3.png
[21]: ./media/mobile-engagement-how-tos/TextView1.png
[22]: ./media/mobile-engagement-how-tos/TextView2.png
[23]: ./media/mobile-engagement-how-tos/TextView3.png
[24]: ./media/mobile-engagement-how-tos/TextView4.png
[25]: ./media/mobile-engagement-how-tos/TextView5.png
[26]: ./media/mobile-engagement-how-tos/TextView6.png
[27]: ./media/mobile-engagement-how-tos/TextView7.png
[28]: ./media/mobile-engagement-how-tos/WebView1.png
[29]: ./media/mobile-engagement-how-tos/WebView2.png
[30]: ./media/mobile-engagement-how-tos/WebView3.png
[31]: ./media/mobile-engagement-how-tos/WebView4.png
[32]: ./media/mobile-engagement-how-tos/WebView5.png

<!--Link references-->
[Link 1]: mobile-engagement-user-interface.md
[Link 2]: mobile-engagement-troubleshooting-guide.md
[Link 3]: mobile-engagement-how-tos.md
[Link 4]: http://go.microsoft.com/fwlink/?LinkID=525553
[Link 5]: http://go.microsoft.com/fwlink/?LinkID=525554
[Link 6]: http://go.microsoft.com/fwlink/?LinkId=525555
[Link 7]: https://account.windowsazure.com/PreviewFeatures
[Link 8]: https://social.msdn.microsoft.com/Forums/azure/home?forum=azuremobileengagement
[Link 9]: http://azure.microsoft.com/services/mobile-engagement/
[Link 10]: http://azure.microsoft.com/documentation/services/mobile-engagement/
[Link 11]: http://azure.microsoft.com/pricing/details/mobile-engagement/
[Link 12]: mobile-engagement-user-interface-navigation.md
[Link 13]: mobile-engagement-user-interface-home.md
[Link 14]: mobile-engagement-user-interface-my-account.md
[Link 15]: mobile-engagement-user-interface-analytics.md
[Link 16]: mobile-engagement-user-interface-monitor.md
[Link 17]: mobile-engagement-user-interface-reach.md
[Link 18]: mobile-engagement-user-interface-segments.md
[Link 19]: mobile-engagement-user-interface-dashboard.md
[Link 20]: mobile-engagement-user-interface-settings.md
[Link 21]: mobile-engagement-troubleshooting-guide-analytics.md
[Link 22]: mobile-engagement-troubleshooting-guide-apis.md
[Link 23]: mobile-engagement-troubleshooting-guide-push-reach.md
[Link 24]: mobile-engagement-troubleshooting-guide-service.md
[Link 25]: mobile-engagement-troubleshooting-guide-sdk.md
[Link 26]: mobile-engagement-troubleshooting-guide-sr-info.md
[Link 27]: ../mobile-engagement-how-tos-first-push.md
[Link 28]: ../mobile-engagement-how-tos-test-campaign.md
[Link 29]: ../mobile-engagement-how-tos-personalize-push.md
[Link 30]: ../mobile-engagement-how-tos-differentiate-push.md
[Link 31]: ../mobile-engagement-how-tos-schedule-campaign.md
[Link 32]: ../mobile-engagement-how-tos-text-view.md
[Link 33]: ../mobile-engagement-how-tos-web-view.md

