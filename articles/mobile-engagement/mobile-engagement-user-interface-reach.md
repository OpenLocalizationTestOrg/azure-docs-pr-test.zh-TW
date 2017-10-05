---
title: "Azure Mobile Engagement 使用者介面 - 觸達"
description: "了解如何使用 Azure Mobile Engagement 透過推播通知觸及應用程式的使用者"
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
ms.openlocfilehash: ce30456e41ff1a2f4824bcb64246ee115fdd1ef7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-reach-out-to-the-users-of-your-application-with-push-notifications"></a><span data-ttu-id="fe75f-103">如何透過推播通知觸及應用程式的使用者</span><span class="sxs-lookup"><span data-stu-id="fe75f-103">How to reach out to the users of your application with push notifications</span></span>
<span data-ttu-id="fe75f-104">本文說明 **Mobile Engagement** 入口網站的 [觸達] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="fe75f-104">This article describes the **REACH** tab of the **Mobile Engagement** portal.</span></span> <span data-ttu-id="fe75f-105">使用 **Mobile Engagement** 入口網站可監視與管理您的行動應用程式。</span><span class="sxs-lookup"><span data-stu-id="fe75f-105">You use the **Mobile Engagement** portal to monitor and manage your mobile apps.</span></span> <span data-ttu-id="fe75f-106">請注意，若要開始使用入口網站，您必須先建立 **Azure Mobile Engagement** 帳戶。</span><span class="sxs-lookup"><span data-stu-id="fe75f-106">Note that to start using the portal you first need to create an **Azure Mobile Engagement** account.</span></span> <span data-ttu-id="fe75f-107">如需詳細資訊，請參閱[建立 Azure Mobile Engagement 帳戶](mobile-engagement-create.md)。</span><span class="sxs-lookup"><span data-stu-id="fe75f-107">For more information, see [Create an Azure Mobile Engagement account](mobile-engagement-create.md).</span></span>

<span data-ttu-id="fe75f-108">UI 的 [觸達] 區段是推送活動管理工具，您可以在此建立/編輯/啟動/完成/監視推播通知活動，並取得推播通知活動的統計資料，您也可以透過「觸達 API」(和低階推送 API 的部份元素) 存取這些功能。</span><span class="sxs-lookup"><span data-stu-id="fe75f-108">The Reach section of the UI is the Push campaign management tool where you can create/edit/activate/finish/monitor and get statistics on Push notification campaigns and features that can also be accessed via the Reach API (and some elements of the low level Push API).</span></span> <span data-ttu-id="fe75f-109">請記住，無論您使用 API 或 UI，都必須先使用 SDK 針對每個平台將 Azure Mobile Engagement 和觸達整合到您的應用程式，才能使用觸達活動。</span><span class="sxs-lookup"><span data-stu-id="fe75f-109">Remember that whether you are using the APIs or the UI, you will need to integrate both Azure Mobile Engagement and Reach into your application for each platform with the SDK before you can use Reach campaigns.</span></span>

> [!NOTE]
> <span data-ttu-id="fe75f-110">許多 **Mobile Engagement** 入口網站 UI 的區段含有 [顯示說明] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="fe75f-110">Many sections of the **Mobile Engagement** portal UI contain the **SHOW HELP** button.</span></span> <span data-ttu-id="fe75f-111">按該按鈕，可獲得關於區段的詳細內容資訊。</span><span class="sxs-lookup"><span data-stu-id="fe75f-111">Press this button to get more contextual information about a section.</span></span>
> 
> 

## <a name="four-types-of-push-notifications"></a><span data-ttu-id="fe75f-112">推播通知的四種類型</span><span class="sxs-lookup"><span data-stu-id="fe75f-112">Four types of Push notifications</span></span>
1. <span data-ttu-id="fe75f-113">宣告：可讓您傳送廣告訊息給使用者，將他們重新導向至您應用程式內的另一個位置，或者將他們傳送至您應用程式外的網頁或市集。</span><span class="sxs-lookup"><span data-stu-id="fe75f-113">Announcements - allow you to send advertising messages to users that redirect them to another location inside your app or to send them to a webpage or store outside of your app.</span></span> 
2. <span data-ttu-id="fe75f-114">輪詢：可讓您透過詢問使用者問題，從使用者收集資訊。</span><span class="sxs-lookup"><span data-stu-id="fe75f-114">Polls - allow you to gather information from end users by asking them questions.</span></span>
3. <span data-ttu-id="fe75f-115">資料推送：可讓您傳送二進位或 base64 資料檔案。</span><span class="sxs-lookup"><span data-stu-id="fe75f-115">Data Pushes - allow you to send a binary or base64 data file.</span></span> <span data-ttu-id="fe75f-116">資料推送中所包含的資訊會傳送至您的應用程式，以便調整您的使用者在應用程式中目前的體驗。</span><span class="sxs-lookup"><span data-stu-id="fe75f-116">The information contained in a data push is sent to your application to modify your users' current experience in your app.</span></span> <span data-ttu-id="fe75f-117">您的應用程式必須能夠處理資料推送中的資料。</span><span class="sxs-lookup"><span data-stu-id="fe75f-117">Your application needs to be able to process the data in a data push.</span></span>

## <a name="campaign-details"></a><span data-ttu-id="fe75f-118">活動詳細資料</span><span class="sxs-lookup"><span data-stu-id="fe75f-118">Campaign Details</span></span>
<span data-ttu-id="fe75f-119">您可以停留在活動名稱上或按一下以開啟活動，來編輯、複製、刪除活動或啟動尚未啟動的活動。</span><span class="sxs-lookup"><span data-stu-id="fe75f-119">You can edit, clone, delete, or activate campaigns that have not been activated yet by hovering over their names or you can click to open them.</span></span> <span data-ttu-id="fe75f-120">您可以停留在活動名稱上或按一下以開啟活動，來複製已經啟動的活動。</span><span class="sxs-lookup"><span data-stu-id="fe75f-120">You can clone campaigns that have already been activated by hovering over their names or you can click to open them.</span></span> <span data-ttu-id="fe75f-121">不過，活動一旦啟動，您就無法變更。</span><span class="sxs-lookup"><span data-stu-id="fe75f-121">However, you can't change a campaign once it has been activated.</span></span>

![Reach1][18]

## <a name="reach-feedback"></a><span data-ttu-id="fe75f-123">觸達意見反應</span><span class="sxs-lookup"><span data-stu-id="fe75f-123">Reach Feedback</span></span>
<span data-ttu-id="fe75f-124">按一下 [統計資料]  即可檢視觸達活動的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="fe75f-124">Click on **Statistics** to see the details of a Reach campaign.</span></span> <span data-ttu-id="fe75f-125">[簡單]  檢視能透過視覺方法，以直條圖形式表示啟用活動之後發生了什麼事。</span><span class="sxs-lookup"><span data-stu-id="fe75f-125">The **Simple** view provides a visual representation in the form of a column bar graph about what happened after a campaign was activated.</span></span> <span data-ttu-id="fe75f-126">[進階]  檢視則能提供更細部的推送活動詳細資料。</span><span class="sxs-lookup"><span data-stu-id="fe75f-126">The **Advanced** view provides more granular details about the push campaign.</span></span> <span data-ttu-id="fe75f-127">如果您傳送測試活動，也就是將推送活動傳送到測試裝置，則無法取得這些詳細資料。</span><span class="sxs-lookup"><span data-stu-id="fe75f-127">These details will not be available if you are sending a test campaign i.e. a push sent to a test device.</span></span> <span data-ttu-id="fe75f-128">以下是解譯這些詳細資料的方式：</span><span class="sxs-lookup"><span data-stu-id="fe75f-128">Here is how you should interpret these details:</span></span>

1. <span data-ttu-id="fe75f-129">**已推送** - 這會指出推送至裝置的訊息數目。</span><span class="sxs-lookup"><span data-stu-id="fe75f-129">**Pushed** - This specifies the number of messages pushed to the devices.</span></span> <span data-ttu-id="fe75f-130">這個數目將取決於您在建立推送活動時所指定的目標對象。</span><span class="sxs-lookup"><span data-stu-id="fe75f-130">This number will depend on the target audience you specified while creating the push campaign.</span></span> <span data-ttu-id="fe75f-131">如果未指定任何目標對象，則會將此推送活動傳送至所有已註冊的裝置。</span><span class="sxs-lookup"><span data-stu-id="fe75f-131">If you do not specify any target audience, then this push will be sent out to all the registered devices.</span></span> <span data-ttu-id="fe75f-132">和其他所有推送服務一樣，我們並不會直接將通知推送到裝置上，而是會將其推送至各平台特定的推播通知服務 (PNS - APNS/GCM/WNS)，讓這些服務將通知傳送到裝置上。</span><span class="sxs-lookup"><span data-stu-id="fe75f-132">Like all other push services, we do not push the notifications directly to the devices but instead push them to the respective platform specific Push Notification Services (PNS - APNS/GCM/WNS) so that they can deliver the notifications to the devices.</span></span> 
2. <span data-ttu-id="fe75f-133">**已傳送** - 這會指出 PNS 成功傳送到裝置並且為 Mobile Engagement SDK 認可為已收到的訊息數目。</span><span class="sxs-lookup"><span data-stu-id="fe75f-133">**Delivered** - This specifies the number of messages which are successfully delivered by the PNS to the device and acknowledged as received by Mobile Engagement SDK.</span></span> 
   
   <span data-ttu-id="fe75f-134">*已傳送計數小於已推送計數的原因：*</span><span class="sxs-lookup"><span data-stu-id="fe75f-134">*Reasons for Delivered count being less than Pushed count:*</span></span>
   
   1. <span data-ttu-id="fe75f-135">如果使用者已在裝置上解除安裝應用程式，但在我們將推送活動傳送到 PNS 的當下，PNS 並不知道這一點，訊息會遭到捨棄。</span><span class="sxs-lookup"><span data-stu-id="fe75f-135">If the user has uninstalled the app from the device but the PNS doesn't know about it at the time we send the push to the PNS then the message will be dropped.</span></span>
   2. <span data-ttu-id="fe75f-136">如果裝置具有應用程式，但裝置本身已離線很久，PNS 就無法將訊息傳送至裝置。</span><span class="sxs-lookup"><span data-stu-id="fe75f-136">If the device has the app but the devices themselves were offline for long periods of time, then the PNS will fail to deliver the message to the device.</span></span> 
   3. <span data-ttu-id="fe75f-137">如果訊息確實已傳送給裝置，但應用程式中的 Mobile Engagement SDK 無法辨識訊息的內容，其便會捨棄該訊息。</span><span class="sxs-lookup"><span data-stu-id="fe75f-137">If the message does get delivered to the device but the Mobile Engagement SDK in the app doesn’t recognize the content of the message, then it drops that message.</span></span> <span data-ttu-id="fe75f-138">如果在應用程式中自訂通知時產生了在 SDK 中捕捉到並且會捨棄訊息的例外狀況，就會發生此問題。</span><span class="sxs-lookup"><span data-stu-id="fe75f-138">This could happen if the customization of the notification in the app generates an exception which we catch in the SDK and drop the message.</span></span> <span data-ttu-id="fe75f-139">如果裝置上的應用程式所使用的 Mobile Engagement SDK 版本不能夠解讀平台所傳送的較新版本推送訊息，則也會發生此問題，但是只會在服務平台分派通知後應用程式已升級時發生。</span><span class="sxs-lookup"><span data-stu-id="fe75f-139">This could also occur if the app on the device is using a version of the Mobile Engagement SDK which is not able to understand the newer version of the push message sent from the platform but this is only when the app was upgraded after the notification was dispatched from the service platform.</span></span> <span data-ttu-id="fe75f-140">[進階]  索引標籤會指出已捨棄的訊息數量。</span><span class="sxs-lookup"><span data-stu-id="fe75f-140">The **Advanced** tab will tell how many messages were dropped.</span></span> 
   4. <span data-ttu-id="fe75f-141">在 iOS 裝置上，如果裝置電力偏低或應用程式在處理遠端通知時耗用大量的電力，訊息有時會無法傳遞。</span><span class="sxs-lookup"><span data-stu-id="fe75f-141">On iOS devices, messages sometimes do not get delivered if either the device is on low battery or if the app is consuming significant amount of power when processing remote notifications.</span></span> <span data-ttu-id="fe75f-142">這是 iOS 裝置的一項限制。</span><span class="sxs-lookup"><span data-stu-id="fe75f-142">This is a limitation of the iOS devices.</span></span>   
3. <span data-ttu-id="fe75f-143">**已顯示** - 這會指出已透過通知中心內的系統推送/應用程式外通知或行動應用程式內的應用程式內通知的形式，對裝置上的應用程式使用者成功顯示的訊息數。</span><span class="sxs-lookup"><span data-stu-id="fe75f-143">**Displayed** - This specifies the number of messages which are successfully shown to the app user on the device in the form of a system push/out-of-app notification in the notification center or an in-app notification within the mobile app.</span></span>  <span data-ttu-id="fe75f-144">[進階]  索引標籤會分別指出系統通知和應用程式內通知的數量。</span><span class="sxs-lookup"><span data-stu-id="fe75f-144">The **Advanced** tab will tell you how many were system notifications and how many were in-app notifications.</span></span> 
   
   <bpt id="p1">*</bpt>Reasons for Displayed count being less than Delivered count (waiting to be displayed)<ept id="p1">*</ept>
   
   1. <span data-ttu-id="fe75f-146">如果通知活動上有結束日期，有可能通知已傳遞，但到了開始時間並該顯示給應用程式使用者時就已經過期而永遠不會顯示。</span><span class="sxs-lookup"><span data-stu-id="fe75f-146">If the notification campaign had an end date on it then it is possible that the notification was delivered but when the time came to open and display it to the app user, it was already expired so it was never displayed.</span></span>   
   2. <span data-ttu-id="fe75f-147">如果通知是應用程式內通知，則只有在應用程式使用者開啟應用程式時，才會顯示通知。</span><span class="sxs-lookup"><span data-stu-id="fe75f-147">If the notification is an in-app notification then the notification is only displayed when the app user opens the app.</span></span> <span data-ttu-id="fe75f-148">在應用程式使用者尚未開啟應用程式的情況下，SDK 會回報為已傳遞通知，但直到應用程式開啟時才會顯示通知。</span><span class="sxs-lookup"><span data-stu-id="fe75f-148">In cases where the app user hasn't opened the app, the SDK will report that the notification was delivered but not yet displayed until the app is opened.</span></span> 
   3. <span data-ttu-id="fe75f-149">如果通知是應用程式內通知，並設定要顯示在特定活動/畫面上，系統也會將通知回報為已傳遞，但直到使用者開啟應用程式的特定畫面時才會顯示。</span><span class="sxs-lookup"><span data-stu-id="fe75f-149">If the notification is an in-app notification and configured to be shown on a specific activity/screen then also the notification will be reported as delivered but not yet delivered until the user opens the app on a specific screen.</span></span> 
4. <span data-ttu-id="fe75f-150">**使用者互動** - 這會指出應用程式使用者已產生互動的訊息數，其中也會包含已採取動作或已結束的訊息。</span><span class="sxs-lookup"><span data-stu-id="fe75f-150">**User Interactions** - This specifies the number of messages which the app user has interacted with and will include the messages which are either actioned or exited.</span></span> 
   
   * <span data-ttu-id="fe75f-151">*應用程式使用者可透過下列任一方式對通知採取動作：*</span><span class="sxs-lookup"><span data-stu-id="fe75f-151">*The app user can action a notification in either of the following ways:*</span></span>
     
     1. <span data-ttu-id="fe75f-152">如果是系統通知/應用程式外通知或以僅限通知形式傳送的應用程式內通知，應用程式使用者可以按一下通知。</span><span class="sxs-lookup"><span data-stu-id="fe75f-152">If the notification is a system/out-of-app notification or an in-app notification sent as notification-only then the app user clicks on the notification.</span></span>
     2. <span data-ttu-id="fe75f-153">如果是具有文字、網頁檢視或投票的應用程式內通知，應用程式使用者可以按一下通知中的 [動作] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="fe75f-153">If the notification is an in-app notification with a text or web-view or polls then the app user clicks on the Action button in the notification.</span></span>
     3. <span data-ttu-id="fe75f-154">如果是具有網頁檢視的應用程式內通知，則應用程式使用者可以按一下網頁檢視中的 URL [僅限 Android]</span><span class="sxs-lookup"><span data-stu-id="fe75f-154">If the notification is an in-app notification with a web-view then the app user clicks on a URL in the web view [Android Only]</span></span>
   * <span data-ttu-id="fe75f-155">*應用程式使用者可透過下列任一方式結束通知：*</span><span class="sxs-lookup"><span data-stu-id="fe75f-155">*The app user can exit a notification in either of the following ways:*</span></span>
     
     1. <span data-ttu-id="fe75f-156">直接按一下通知上的 [關閉] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="fe75f-156">Clicking the close button on the notification directly.</span></span> 
     2. <span data-ttu-id="fe75f-157">將通知撥開或刪除。</span><span class="sxs-lookup"><span data-stu-id="fe75f-157">Swiping away or deleting the notification.</span></span> 
     3. <span data-ttu-id="fe75f-158">具有文字/網頁內容和投票的應用程式內通知，通常會透過有兩個步驟的程序顯示給應用程式使用者。</span><span class="sxs-lookup"><span data-stu-id="fe75f-158">In-app notifications with text/web content and polls are typically displayed to the app user in a two-step process.</span></span> <span data-ttu-id="fe75f-159">他們會先看到通知，當他們按一下通知時，就會看到後續的文字/網頁/投票內容。</span><span class="sxs-lookup"><span data-stu-id="fe75f-159">They see a notification first and when they click on it, they see the subsequent text/web/poll content.</span></span> <span data-ttu-id="fe75f-160">應用程式使用者可以在任一步驟結束通知，[進階] 檢視中的詳細資料會捕捉此行為。</span><span class="sxs-lookup"><span data-stu-id="fe75f-160">The app user can exit a notification in either of these steps and the details in the Advanced view captures this.</span></span> 
5. <span data-ttu-id="fe75f-161">**已採取動作** - 這會指出應用程式使用者已明確採取動作的訊息數。</span><span class="sxs-lookup"><span data-stu-id="fe75f-161">**Actioned** - This specifies the number of messages which were explicitly actioned by the app user.</span></span> <span data-ttu-id="fe75f-162">這是最有意思的數字，因為這個數字會指出有多少應用程式使用者對您在通知中所推送的訊息感興趣。</span><span class="sxs-lookup"><span data-stu-id="fe75f-162">This is the most interesting number as this tells how many app users were interested by the message you pushed out in the notification.</span></span> 

> [!NOTE]
> <span data-ttu-id="fe75f-163">在 iOS 和 Windows 平台上，如果使用者開啟應用程式，且活動是「隨時」行銷活動，則可能會同時顯示應用程式外和應用程式內通知。</span><span class="sxs-lookup"><span data-stu-id="fe75f-163">On iOS & Windows platforms, if the user has the app open and the campaign was an "AnyTime" campaign then it is possible that both out of app and in-app notifications are displayed at the same time.</span></span> <span data-ttu-id="fe75f-164">這可能會造成「已顯示」計數高於「已傳送」計數。</span><span class="sxs-lookup"><span data-stu-id="fe75f-164">This may cause a Displayed count higher than the Delivered.</span></span> <span data-ttu-id="fe75f-165">如果使用者對通知產生互動或採取動作，則甚至是「使用者互動」/「已採取動作」計數也會大於「已傳送」計數。</span><span class="sxs-lookup"><span data-stu-id="fe75f-165">If the user interacts or actions the notification, then even the User Interactions/Actioned count could be greater than Delivered.</span></span> 
> 
> 

![Reach2][19]

## <a name="see-also"></a><span data-ttu-id="fe75f-167">另請參閱</span><span class="sxs-lookup"><span data-stu-id="fe75f-167">See also</span></span>
* <span data-ttu-id="fe75f-168">[概念][Link 6]</span><span class="sxs-lookup"><span data-stu-id="fe75f-168">[Concepts][Link 6]</span></span>
* <span data-ttu-id="fe75f-169">[疑難排解指南服務][Link 24]</span><span class="sxs-lookup"><span data-stu-id="fe75f-169">[Troubleshooting Guide Service][Link 24]</span></span>

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

