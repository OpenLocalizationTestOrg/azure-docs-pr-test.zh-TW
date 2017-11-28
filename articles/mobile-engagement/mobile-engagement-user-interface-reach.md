---
title: "aaaAzure Mobile Engagement 使用者介面觸達"
description: "深入了解如何 tooreach toohello 使用者應用程式使用 Azure Mobile Engagement 的推播通知"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: d96e2590-08dd-4481-a352-2c18f26a1643
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 40d5162ddeccec82c2c9f5b0d72b4cb10c9ddc38
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooreach-out-toohello-users-of-your-application-with-push-notifications"></a><span data-ttu-id="263c3-103">如何 tooreach toohello 的推播通知的應用程式的使用者</span><span class="sxs-lookup"><span data-stu-id="263c3-103">How tooreach out toohello users of your application with push notifications</span></span>
<span data-ttu-id="263c3-104">本文說明 hello**到達**] 索引標籤的 hello **Mobile Engagement**入口網站。</span><span class="sxs-lookup"><span data-stu-id="263c3-104">This article describes hello **REACH** tab of hello **Mobile Engagement** portal.</span></span> <span data-ttu-id="263c3-105">使用 hello **Mobile Engagement** toomonitor 入口網站和管理您的行動裝置應用程式。</span><span class="sxs-lookup"><span data-stu-id="263c3-105">You use hello **Mobile Engagement** portal toomonitor and manage your mobile apps.</span></span> <span data-ttu-id="263c3-106">請注意使用 hello 入口網站，您必須先 toocreate 該 toostart **Azure Mobile Engagement**帳戶。</span><span class="sxs-lookup"><span data-stu-id="263c3-106">Note that toostart using hello portal you first need toocreate an **Azure Mobile Engagement** account.</span></span> <span data-ttu-id="263c3-107">如需詳細資訊，請參閱[建立 Azure Mobile Engagement 帳戶](mobile-engagement-create.md)。</span><span class="sxs-lookup"><span data-stu-id="263c3-107">For more information, see [Create an Azure Mobile Engagement account](mobile-engagement-create.md).</span></span>

<span data-ttu-id="263c3-108">hello 到達的 hello ui 段您也可以建立/編輯/啟動/完成/監視的 hello 推送活動管理工具，並取得推送通知活動和功能，也可以存取透過 hello 觸達 API （和 hello 低的某些項目上的統計資料層級推送應用程式開發介面）。</span><span class="sxs-lookup"><span data-stu-id="263c3-108">hello Reach section of hello UI is hello Push campaign management tool where you can create/edit/activate/finish/monitor and get statistics on Push notification campaigns and features that can also be accessed via hello Reach API (and some elements of hello low level Push API).</span></span> <span data-ttu-id="263c3-109">請記住，不論您使用 hello 應用程式開發介面或 hello UI，您將需要 toointegrate Azure Mobile Engagement 和觸達每個平台以 hello SDK，才能使用應用程式達到行銷活動。</span><span class="sxs-lookup"><span data-stu-id="263c3-109">Remember that whether you are using hello APIs or hello UI, you will need toointegrate both Azure Mobile Engagement and Reach into your application for each platform with hello SDK before you can use Reach campaigns.</span></span>

> [!NOTE]
> <span data-ttu-id="263c3-110">多區段的 hello **Mobile Engagement**入口網站 UI 包含 hello**顯示說明**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="263c3-110">Many sections of hello **Mobile Engagement** portal UI contain hello **SHOW HELP** button.</span></span> <span data-ttu-id="263c3-111">按此按鈕 tooget 區段內容詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="263c3-111">Press this button tooget more contextual information about a section.</span></span>
> 
> 

## <a name="four-types-of-push-notifications"></a><span data-ttu-id="263c3-112">推播通知的四種類型</span><span class="sxs-lookup"><span data-stu-id="263c3-112">Four types of Push notifications</span></span>
1. <span data-ttu-id="263c3-113">公告功能-可讓您將他們重新導向 tooanother 位置內應用程式或 toosend toosend 廣告郵件 toousers 它們 tooa 網頁或儲存您的應用程式之外。</span><span class="sxs-lookup"><span data-stu-id="263c3-113">Announcements - allow you toosend advertising messages toousers that redirect them tooanother location inside your app or toosend them tooa webpage or store outside of your app.</span></span> 
2. <span data-ttu-id="263c3-114">輪詢-可讓您從使用者 toogather 資訊來提問以它們。</span><span class="sxs-lookup"><span data-stu-id="263c3-114">Polls - allow you toogather information from end users by asking them questions.</span></span>
3. <span data-ttu-id="263c3-115">資料推送-可讓您 toosend 二進位或 base64 資料檔案。</span><span class="sxs-lookup"><span data-stu-id="263c3-115">Data Pushes - allow you toosend a binary or base64 data file.</span></span> <span data-ttu-id="263c3-116">資料推送中包含的 hello 資訊在應用程式中傳送 tooyour 應用程式 toomodify 您的使用者目前的體驗。</span><span class="sxs-lookup"><span data-stu-id="263c3-116">hello information contained in a data push is sent tooyour application toomodify your users' current experience in your app.</span></span> <span data-ttu-id="263c3-117">您的應用程式需要在資料推送的 toobe 無法 tooprocess hello 資料。</span><span class="sxs-lookup"><span data-stu-id="263c3-117">Your application needs toobe able tooprocess hello data in a data push.</span></span>

## <a name="campaign-details"></a><span data-ttu-id="263c3-118">活動詳細資料</span><span class="sxs-lookup"><span data-stu-id="263c3-118">Campaign Details</span></span>
<span data-ttu-id="263c3-119">您可以編輯、 複製、 刪除或啟動具有尚未啟動其名稱為上方的活動或您可以按一下 tooopen 它們。</span><span class="sxs-lookup"><span data-stu-id="263c3-119">You can edit, clone, delete, or activate campaigns that have not been activated yet by hovering over their names or you can click tooopen them.</span></span> <span data-ttu-id="263c3-120">您可以複製已啟用由其名稱將滑鼠停留的活動，或者您可以按一下 tooopen 它們。</span><span class="sxs-lookup"><span data-stu-id="263c3-120">You can clone campaigns that have already been activated by hovering over their names or you can click tooopen them.</span></span> <span data-ttu-id="263c3-121">不過，活動一旦啟動，您就無法變更。</span><span class="sxs-lookup"><span data-stu-id="263c3-121">However, you can't change a campaign once it has been activated.</span></span>

![Reach1][18]

## <a name="reach-feedback"></a><span data-ttu-id="263c3-123">觸達意見反應</span><span class="sxs-lookup"><span data-stu-id="263c3-123">Reach Feedback</span></span>
<span data-ttu-id="263c3-124">按一下**統計資料**toosee hello 觸達活動詳細資料。</span><span class="sxs-lookup"><span data-stu-id="263c3-124">Click on **Statistics** toosee hello details of a Reach campaign.</span></span> <span data-ttu-id="263c3-125">hello**簡單**檢視提供的資料行的橫條圖，啟用活動之後發生了什麼事 hello 表單中的視覺表示法。</span><span class="sxs-lookup"><span data-stu-id="263c3-125">hello **Simple** view provides a visual representation in hello form of a column bar graph about what happened after a campaign was activated.</span></span> <span data-ttu-id="263c3-126">hello**進階**提供更細微的 hello 推播宣傳活動詳細資料檢視。</span><span class="sxs-lookup"><span data-stu-id="263c3-126">hello **Advanced** view provides more granular details about hello push campaign.</span></span> <span data-ttu-id="263c3-127">這些詳細資料將無法使用，如果您要傳送的測試活動也就推播傳送的 tooa 測試裝置。</span><span class="sxs-lookup"><span data-stu-id="263c3-127">These details will not be available if you are sending a test campaign i.e. a push sent tooa test device.</span></span> <span data-ttu-id="263c3-128">以下是解譯這些詳細資料的方式：</span><span class="sxs-lookup"><span data-stu-id="263c3-128">Here is how you should interpret these details:</span></span>

1. <span data-ttu-id="263c3-129">**推入**-這會指定 hello 訊息推入 toohello 裝置數目。</span><span class="sxs-lookup"><span data-stu-id="263c3-129">**Pushed** - This specifies hello number of messages pushed toohello devices.</span></span> <span data-ttu-id="263c3-130">此數目將取決於 hello 建立 hello 推播宣傳活動時，您指定的目標對象。</span><span class="sxs-lookup"><span data-stu-id="263c3-130">This number will depend on hello target audience you specified while creating hello push campaign.</span></span> <span data-ttu-id="263c3-131">如果您未指定任何目標對象，然後此 push 會送出 tooall hello 註冊裝置。</span><span class="sxs-lookup"><span data-stu-id="263c3-131">If you do not specify any target audience, then this push will be sent out tooall hello registered devices.</span></span> <span data-ttu-id="263c3-132">如同其他所有推入服務，我們不執行推送 hello 通知直接 toohello 裝置，但改為將其推送 toohello 各平台特定的推播通知服務 (PNS-APNS/GCM/WNS)，讓它們可以傳送嗨通知 toohello 裝置。</span><span class="sxs-lookup"><span data-stu-id="263c3-132">Like all other push services, we do not push hello notifications directly toohello devices but instead push them toohello respective platform specific Push Notification Services (PNS - APNS/GCM/WNS) so that they can deliver hello notifications toohello devices.</span></span> 
2. <span data-ttu-id="263c3-133">**傳遞**-這會指定為接收 Mobile Engagement SDK 的 hello 訊息成功傳送嗨 PNS toohello 裝置及認可的數目。</span><span class="sxs-lookup"><span data-stu-id="263c3-133">**Delivered** - This specifies hello number of messages which are successfully delivered by hello PNS toohello device and acknowledged as received by Mobile Engagement SDK.</span></span> 
   
   <span data-ttu-id="263c3-134">*已傳送計數小於已推送計數的原因：*</span><span class="sxs-lookup"><span data-stu-id="263c3-134">*Reasons for Delivered count being less than Pushed count:*</span></span>
   
   1. <span data-ttu-id="263c3-135">如果 hello 使用者解除 hello 應用程式安裝從 hello 裝置但 hello PNS 不知道它在 hello 階段，我們會傳送 hello 發送 toohello PNS 然後 hello 訊息皆會予以捨棄。</span><span class="sxs-lookup"><span data-stu-id="263c3-135">If hello user has uninstalled hello app from hello device but hello PNS doesn't know about it at hello time we send hello push toohello PNS then hello message will be dropped.</span></span>
   2. <span data-ttu-id="263c3-136">如果 hello 裝置 hello 應用程式，但 hello 裝置本身很長的時間期間已離線，則 hello PNS 會失敗 toodeliver hello 訊息 toohello 裝置。</span><span class="sxs-lookup"><span data-stu-id="263c3-136">If hello device has hello app but hello devices themselves were offline for long periods of time, then hello PNS will fail toodeliver hello message toohello device.</span></span> 
   3. <span data-ttu-id="263c3-137">如果 hello 訊息傳遞 toohello 裝置取得但 hello Mobile Engagement SDK 在 hello 應用程式中的無法辨識 hello hello 訊息內容，它會捨棄該訊息。</span><span class="sxs-lookup"><span data-stu-id="263c3-137">If hello message does get delivered toohello device but hello Mobile Engagement SDK in hello app doesn’t recognize hello content of hello message, then it drops that message.</span></span> <span data-ttu-id="263c3-138">如果 hello 通知 hello 應用程式中的 hello 自訂 hello SDK 和 drop hello 訊息中產生攔截的例外狀況，則會發生此問題。</span><span class="sxs-lookup"><span data-stu-id="263c3-138">This could happen if hello customization of hello notification in hello app generates an exception which we catch in hello SDK and drop hello message.</span></span> <span data-ttu-id="263c3-139">這也可能會發生 hello hello 裝置上的應用程式是否使用版的 hello Mobile Engagement SDK 不能 toounderstand hello 較新版本的 hello 推播訊息寄件者 hello 平台，但 hello 應用程式已升級之後 hello 通知時，才發送 hello 服務平台。</span><span class="sxs-lookup"><span data-stu-id="263c3-139">This could also occur if hello app on hello device is using a version of hello Mobile Engagement SDK which is not able toounderstand hello newer version of hello push message sent from hello platform but this is only when hello app was upgraded after hello notification was dispatched from hello service platform.</span></span> <span data-ttu-id="263c3-140">hello**進階**] 索引標籤將會通知已卸除的訊息數量。</span><span class="sxs-lookup"><span data-stu-id="263c3-140">hello **Advanced** tab will tell how many messages were dropped.</span></span> 
   4. <span data-ttu-id="263c3-141">在 iOS 裝置上訊息有時才傳送如果其中一個 hello 裝置位於電力偏低，或 hello 應用程式會耗用大量的電力，當處理遠端通知。</span><span class="sxs-lookup"><span data-stu-id="263c3-141">On iOS devices, messages sometimes do not get delivered if either hello device is on low battery or if hello app is consuming significant amount of power when processing remote notifications.</span></span> <span data-ttu-id="263c3-142">這是 hello 的 iOS 裝置的限制。</span><span class="sxs-lookup"><span data-stu-id="263c3-142">This is a limitation of hello iOS devices.</span></span>   
3. <span data-ttu-id="263c3-143">**顯示**-這會指定訊息已成功顯示 toohello 應用程式使用者的 hello 裝置 hello 形式系統推入/out 的-應用程式通知在 hello 通知中心或應用程式內通知內 hello 行動的 hello 數目應用程式。</span><span class="sxs-lookup"><span data-stu-id="263c3-143">**Displayed** - This specifies hello number of messages which are successfully shown toohello app user on hello device in hello form of a system push/out-of-app notification in hello notification center or an in-app notification within hello mobile app.</span></span>  <span data-ttu-id="263c3-144">hello**進階**多少了系統通知和多少應用程式內通知] 索引標籤也將會通知您。</span><span class="sxs-lookup"><span data-stu-id="263c3-144">hello **Advanced** tab will tell you how many were system notifications and how many were in-app notifications.</span></span> 
   
   <span data-ttu-id="263c3-145">*顯示原因計數小於傳遞的計數 (等候 toobe 顯示)*</span><span class="sxs-lookup"><span data-stu-id="263c3-145">*Reasons for Displayed count being less than Delivered count (waiting toobe displayed)*</span></span>
   
   1. <span data-ttu-id="263c3-146">如果 hello 通知活動的結束日期必須在其上，則很可能已傳送嗨通知，但當 hello 時間來源 tooopen 並將其顯示 toohello 應用程式的使用者，它是已經過期，永遠不會顯示。</span><span class="sxs-lookup"><span data-stu-id="263c3-146">If hello notification campaign had an end date on it then it is possible that hello notification was delivered but when hello time came tooopen and display it toohello app user, it was already expired so it was never displayed.</span></span>   
   2. <span data-ttu-id="263c3-147">如果 hello 通知，則應用程式內通知 hello 通知只會顯示 hello 應用程式使用者開啟 hello 應用程式時。</span><span class="sxs-lookup"><span data-stu-id="263c3-147">If hello notification is an in-app notification then hello notification is only displayed when hello app user opens hello app.</span></span> <span data-ttu-id="263c3-148">在其中 hello 應用程式使用者還沒開啟過 hello 應用程式的情況下，hello SDK 會報告已傳送 hello 通知，但尚未顯示，直到開啟 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="263c3-148">In cases where hello app user hasn't opened hello app, hello SDK will report that hello notification was delivered but not yet displayed until hello app is opened.</span></span> 
   3. <span data-ttu-id="263c3-149">如果 hello 通知是在應用程式通知，並設定 toobe 然後也 hello 通知將會報告為傳遞特定活動/螢幕上顯示，但尚未傳送之前 hello 使用者會開啟 hello 特定螢幕上的應用程式。</span><span class="sxs-lookup"><span data-stu-id="263c3-149">If hello notification is an in-app notification and configured toobe shown on a specific activity/screen then also hello notification will be reported as delivered but not yet delivered until hello user opens hello app on a specific screen.</span></span> 
4. <span data-ttu-id="263c3-150">**使用者互動**-這會指定 hello hello 應用程式使用者已互動，而且將包含 hello 訊息，也就是採取動作或結束的訊息數目。</span><span class="sxs-lookup"><span data-stu-id="263c3-150">**User Interactions** - This specifies hello number of messages which hello app user has interacted with and will include hello messages which are either actioned or exited.</span></span> 
   
   * <span data-ttu-id="263c3-151">*hello 應用程式使用者可處理的通知 hello 下列方式之一：*</span><span class="sxs-lookup"><span data-stu-id="263c3-151">*hello app user can action a notification in either of hello following ways:*</span></span>
     
     1. <span data-ttu-id="263c3-152">如果 hello 通知系統/out 的-應用程式通知或應用程式內通知傳送為僅限通知就 hello 應用程式使用者在 [hello 通知。</span><span class="sxs-lookup"><span data-stu-id="263c3-152">If hello notification is a system/out-of-app notification or an in-app notification sent as notification-only then hello app user clicks on hello notification.</span></span>
     2. <span data-ttu-id="263c3-153">如果 hello 通知是應用程式內通知與文字或 web 檢視或輪詢然後 hello 應用程式使用者按一下 hello hello 通知中的 [動作] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="263c3-153">If hello notification is an in-app notification with a text or web-view or polls then hello app user clicks on hello Action button in hello notification.</span></span>
     3. <span data-ttu-id="263c3-154">如果 hello 通知，則 web 檢視的應用程式內通知然後 hello 應用程式使用者按一下 [僅 Android] hello web 檢視中的 URL</span><span class="sxs-lookup"><span data-stu-id="263c3-154">If hello notification is an in-app notification with a web-view then hello app user clicks on a URL in hello web view [Android Only]</span></span>
   * <span data-ttu-id="263c3-155">*hello 應用程式使用者可結束通知 hello 下列方式之一：*</span><span class="sxs-lookup"><span data-stu-id="263c3-155">*hello app user can exit a notification in either of hello following ways:*</span></span>
     
     1. <span data-ttu-id="263c3-156">直接按一下 hello hello 通知 [關閉] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="263c3-156">Clicking hello close button on hello notification directly.</span></span> 
     2. <span data-ttu-id="263c3-157">離開撥動或刪除 hello 通知。</span><span class="sxs-lookup"><span data-stu-id="263c3-157">Swiping away or deleting hello notification.</span></span> 
     3. <span data-ttu-id="263c3-158">以文字/web 內容和輪詢的應用程式內通知是通常顯示的 toohello 兩步驟程序中的應用程式使用者。</span><span class="sxs-lookup"><span data-stu-id="263c3-158">In-app notifications with text/web content and polls are typically displayed toohello app user in a two-step process.</span></span> <span data-ttu-id="263c3-159">第一次他們會看到通知，當使用者按一下它，他們會看到 hello 後續文字/web/輪詢內容。</span><span class="sxs-lookup"><span data-stu-id="263c3-159">They see a notification first and when they click on it, they see hello subsequent text/web/poll content.</span></span> <span data-ttu-id="263c3-160">hello 應用程式使用者可以結束在這些步驟的通知和 hello 進階檢視中的 hello 詳細資料擷取這。</span><span class="sxs-lookup"><span data-stu-id="263c3-160">hello app user can exit a notification in either of these steps and hello details in hello Advanced view captures this.</span></span> 
5. <span data-ttu-id="263c3-161">**已採取動作**-這會指定 hello 訊息已由 hello 應用程式使用者明確已採取動作的數目。</span><span class="sxs-lookup"><span data-stu-id="263c3-161">**Actioned** - This specifies hello number of messages which were explicitly actioned by hello app user.</span></span> <span data-ttu-id="263c3-162">這是 hello 最有趣的數字，因為這樣做會告知應用程式的使用者人數不想要您推入 hello 通知中的 hello 訊息。</span><span class="sxs-lookup"><span data-stu-id="263c3-162">This is hello most interesting number as this tells how many app users were interested by hello message you pushed out in hello notification.</span></span> 

> [!NOTE]
> <span data-ttu-id="263c3-163">IOS 和 Windows 平台，如果 hello 使用者具有 hello 應用程式開啟及 hello 行銷活動的"AnyTime"行銷活動則很可能同時從應用程式及應用程式內通知會顯示在 [hello 相同的時間。</span><span class="sxs-lookup"><span data-stu-id="263c3-163">On iOS & Windows platforms, if hello user has hello app open and hello campaign was an "AnyTime" campaign then it is possible that both out of app and in-app notifications are displayed at hello same time.</span></span> <span data-ttu-id="263c3-164">這可能會導致顯示計數高於 hello 傳遞。</span><span class="sxs-lookup"><span data-stu-id="263c3-164">This may cause a Displayed count higher than hello Delivered.</span></span> <span data-ttu-id="263c3-165">如果 hello 使用者互動或動作 hello 通知，然後甚至 hello 使用者互動/Actioned 計數可能會大於已傳遞。</span><span class="sxs-lookup"><span data-stu-id="263c3-165">If hello user interacts or actions hello notification, then even hello User Interactions/Actioned count could be greater than Delivered.</span></span> 
> 
> 

![Reach2][19]

## <a name="see-also"></a><span data-ttu-id="263c3-167">另請參閱</span><span class="sxs-lookup"><span data-stu-id="263c3-167">See also</span></span>
* <span data-ttu-id="263c3-168">[概念][Link 6]</span><span class="sxs-lookup"><span data-stu-id="263c3-168">[Concepts][Link 6]</span></span>
* <span data-ttu-id="263c3-169">[疑難排解指南服務][Link 24]</span><span class="sxs-lookup"><span data-stu-id="263c3-169">[Troubleshooting Guide Service][Link 24]</span></span>

<!--Image references-->
[1]: ./media/mobile-engagement-user-interface-navigation/navigation1.png
[2]: ./media/mobile-engagement-user-interface-home/home1.png
[3]: ./media/mobile-engagement-user-interface-home/home2.png
[4]: ./media/mobile-engagement-user-interface-home/home3.png
[5]: ./media/mobile-engagement-user-interface-home/home4.png
[6]: ./media/mobile-engagement-user-interface-home/home5.png
[7]: ./media/mobile-engagement-user-interface-my-account/myaccount1.png
[8]: ./media/mobile-engagement-user-interface-my-account/myaccount2.png
[9]: ./media/mobile-engagement-user-interface-my-account/myaccount3.png
[10]: ./media/mobile-engagement-user-interface-analytics/analytics1.png
[11]: ./media/mobile-engagement-user-interface-analytics/analytics2.png
[12]: ./media/mobile-engagement-user-interface-analytics/analytics3.png
[13]: ./media/mobile-engagement-user-interface-analytics/analytics4.png
[14]: ./media/mobile-engagement-user-interface-monitor/monitor1.png
[15]: ./media/mobile-engagement-user-interface-monitor/monitor2.png
[16]: ./media/mobile-engagement-user-interface-monitor/monitor3.png
[17]: ./media/mobile-engagement-user-interface-monitor/monitor4.png
[18]: ./media/mobile-engagement-user-interface-reach/reach1.png
[19]: ./media/mobile-engagement-user-interface-reach/reach2.png
[20]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign1.png
[21]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign2.png
[22]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign3.png
[23]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign4.png
[24]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign5.png
[25]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign6.png
[26]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign7.png
[27]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign8.png
[28]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign9.png
[29]: ./media/mobile-engagement-user-interface-reach-criterion/Reach-Criterion1.png
[30]: ./media/mobile-engagement-user-interface-reach-content/Reach-Content1.png
[31]: ./media/mobile-engagement-user-interface-reach-content/Reach-Content2.png
[32]: ./media/mobile-engagement-user-interface-reach-content/Reach-Content3.png
[33]: ./media/mobile-engagement-user-interface-reach-content/Reach-Content4.png
[34]: ./media/mobile-engagement-user-interface-dashboard/dashboard1.png
[35]: ./media/mobile-engagement-user-interface-segments/segments1.png
[36]: ./media/mobile-engagement-user-interface-segments/segments2.png
[37]: ./media/mobile-engagement-user-interface-segments/segments3.png
[38]: ./media/mobile-engagement-user-interface-segments/segments4.png
[39]: ./media/mobile-engagement-user-interface-segments/segments5.png
[40]: ./media/mobile-engagement-user-interface-segments/segments6.png
[41]: ./media/mobile-engagement-user-interface-segments/segments7.png
[42]: ./media/mobile-engagement-user-interface-segments/segments8.png
[43]: ./media/mobile-engagement-user-interface-segments/segments9.png
[44]: ./media/mobile-engagement-user-interface-segments/segments10.png
[45]: ./media/mobile-engagement-user-interface-segments/segments11.png
[46]: ./media/mobile-engagement-user-interface-settings/settings1.png
[47]: ./media/mobile-engagement-user-interface-settings/settings2.png
[48]: ./media/mobile-engagement-user-interface-settings/settings3.png
[49]: ./media/mobile-engagement-user-interface-settings/settings4.png
[50]: ./media/mobile-engagement-user-interface-settings/settings5.png
[51]: ./media/mobile-engagement-user-interface-settings/settings6.png
[52]: ./media/mobile-engagement-user-interface-settings/settings7.png
[53]: ./media/mobile-engagement-user-interface-settings/settings8.png
[54]: ./media/mobile-engagement-user-interface-settings/settings9.png
[55]: ./media/mobile-engagement-user-interface-settings/settings10.png
[56]: ./media/mobile-engagement-user-interface-settings/settings11.png
[57]: ./media/mobile-engagement-user-interface-settings/settings12.png
[58]: ./media/mobile-engagement-user-interface-settings/settings13.png

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
[Link 27]: mobile-engagement-user-interface-reach-campaign.md
[Link 28]: mobile-engagement-user-interface-reach-criterion.md
[Link 29]: mobile-engagement-user-interface-reach-content.md

