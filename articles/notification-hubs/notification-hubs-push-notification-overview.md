---
title: "Azure 通知中心"
description: "了解如何使用 Azure 通知中樞新增推播通知功能。"
author: ysxu
manager: erikre
editor: 
services: notification-hubs
documentationcenter: 
ms.assetid: fcfb0ce8-0e19-4fa8-b777-6b9f9cdda178
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: multiple
ms.devlang: multiple
ms.topic: article
ms.date: 1/17/2017
ms.author: yuaxu
ms.openlocfilehash: a1be0b13cd1feb582a23965df142e44d90ac6851
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="azure-notification-hubs"></a><span data-ttu-id="4a022-103">Azure 通知中心</span><span class="sxs-lookup"><span data-stu-id="4a022-103">Azure Notification Hubs</span></span>
## <a name="overview"></a><span data-ttu-id="4a022-104">概觀</span><span class="sxs-lookup"><span data-stu-id="4a022-104">Overview</span></span>
<span data-ttu-id="4a022-105">Azure 通知中樞提供方便使用、多平台、可相應放大的推播引擎。</span><span class="sxs-lookup"><span data-stu-id="4a022-105">Azure Notification Hubs provide an easy-to-use, multi-platform, scaled-out push engine.</span></span> <span data-ttu-id="4a022-106">利用單一的跨平台 API 呼叫，您就可以輕鬆地將鎖定目標且個人化的推播通知，從任何雲端或內部部署後端傳送到任何行動平台。</span><span class="sxs-lookup"><span data-stu-id="4a022-106">With a single cross-platform API call, you can easily send targeted and personalized push notifications to any mobile platform from any cloud or on-premises backend.</span></span>

<span data-ttu-id="4a022-107">通知中樞很適合企業和消費者案例。</span><span class="sxs-lookup"><span data-stu-id="4a022-107">Notification Hubs works great for both enterprise and consumer scenarios.</span></span> <span data-ttu-id="4a022-108">以下是一些客戶使用通知中樞之用途的範例︰</span><span class="sxs-lookup"><span data-stu-id="4a022-108">Here are a few examples customers use Notification Hubs for:</span></span>

* <span data-ttu-id="4a022-109">傳送即時新聞通知給數百萬人，且延遲時間很低。</span><span class="sxs-lookup"><span data-stu-id="4a022-109">Send breaking news notifications to millions with low latency.</span></span>
* <span data-ttu-id="4a022-110">將位置型折價券傳送給感興趣的使用者區段。</span><span class="sxs-lookup"><span data-stu-id="4a022-110">Send location-based coupons to interested user segments.</span></span>
* <span data-ttu-id="4a022-111">將事件相關通知傳送給媒體/運動/財金/遊戲應用程式的使用者或群組。</span><span class="sxs-lookup"><span data-stu-id="4a022-111">Send event-related notifications to users or groups for media/sports/finance/gaming applications.</span></span>
* <span data-ttu-id="4a022-112">將促銷內容推播到應用程式來吸引客戶並進行銷售。</span><span class="sxs-lookup"><span data-stu-id="4a022-112">Push promotional contents to apps to engage and market to customers.</span></span>
* <span data-ttu-id="4a022-113">對使用者發送企業事件通知，例如新訊息和工作項目。</span><span class="sxs-lookup"><span data-stu-id="4a022-113">Notify users of enterprise events like new messages and work items.</span></span>
* <span data-ttu-id="4a022-114">傳送 Multi-Factor Authentication 的程式碼。</span><span class="sxs-lookup"><span data-stu-id="4a022-114">Send codes for multi-factor authentication.</span></span>

## <a name="what-are-push-notifications"></a><span data-ttu-id="4a022-115">什麼是推播通知？</span><span class="sxs-lookup"><span data-stu-id="4a022-115">What are Push Notifications?</span></span>
<span data-ttu-id="4a022-116">推播通知是一種由應用程式對使用者發出的通訊形式，通常會以快顯視窗或對話方塊來對行動應用程式的使用者發出某些他們想要之資訊的通知。</span><span class="sxs-lookup"><span data-stu-id="4a022-116">Push notifications is a form of app-to-user communication where users of mobile apps are notified of certain desired information, usually in a pop-up or dialog box.</span></span> <span data-ttu-id="4a022-117">使用者一般可以選擇要檢視或關閉訊息，選擇前者便會開啟傳送通知的行動應用程式。</span><span class="sxs-lookup"><span data-stu-id="4a022-117">Users can generally choose to view or dismiss the message, and choosing the former will open the mobile app that had communicated the notification.</span></span>

<span data-ttu-id="4a022-118">推播通知是很重要的功能，對於消費者應用程式來說，可提高應用程式的參與和使用率，對於企業應用程式來說，則可傳送最新的企業資訊。</span><span class="sxs-lookup"><span data-stu-id="4a022-118">Push notifications is vital for consumer apps in increasing app engagement and usage, and for enterprise apps in communicating up-to-date business information.</span></span> <span data-ttu-id="4a022-119">此功能是最佳的應用程式對使用者通訊，因為它不會過度耗用行動裝置的電量、可讓通知傳送者保有彈性，並且可在對應的應用程式未執行時使用。</span><span class="sxs-lookup"><span data-stu-id="4a022-119">It is the best app-to-user communication because it is energy-efficient for  mobile devices, flexible for the notifications senders, and available while corresponding apps are not active.</span></span>

<span data-ttu-id="4a022-120">如需某些熱門平台的推播通知詳細資訊︰</span><span class="sxs-lookup"><span data-stu-id="4a022-120">For more information on push notifications for a few popular platforms:</span></span>
* [<span data-ttu-id="4a022-121">iOS</span><span class="sxs-lookup"><span data-stu-id="4a022-121">iOS</span></span>](https://developer.apple.com/notifications/)
* [<span data-ttu-id="4a022-122">Android</span><span class="sxs-lookup"><span data-stu-id="4a022-122">Android</span></span>](https://developer.android.com/guide/topics/ui/notifiers/notifications.html)
* [<span data-ttu-id="4a022-123">Windows</span><span class="sxs-lookup"><span data-stu-id="4a022-123">Windows</span></span>](http://msdn.microsoft.com/library/windows/apps/hh779725.aspx)

## <a name="how-push-notifications-work"></a><span data-ttu-id="4a022-124">推播通知的運作方式</span><span class="sxs-lookup"><span data-stu-id="4a022-124">How Push Notifications Work</span></span>
<span data-ttu-id="4a022-125">推播通知可透過名為「平台通知系統 (PNS)」的平台特定基礎結構來傳遞。</span><span class="sxs-lookup"><span data-stu-id="4a022-125">Push notifications are delivered through platform-specific infrastructures called *Platform Notification Systems* (PNSes).</span></span> <span data-ttu-id="4a022-126">其可提供簡易型推播功能，以所提供的控制代碼傳遞訊息至裝置，並且沒有通用介面。</span><span class="sxs-lookup"><span data-stu-id="4a022-126">They offer barebone push functionalities to delivery message to a device with a provided handle, and have no common interface.</span></span> <span data-ttu-id="4a022-127">若要跨 iOS、Android 和 Windows 版本的應用程式傳送通知給所有客戶，開發人員必須在批次處理傳送時使用 APNS (Apple Push Notification Service)、FCM (Firebase Cloud Messaging) 和 WNS (Windows 通知服務)。</span><span class="sxs-lookup"><span data-stu-id="4a022-127">To send a notification to all customers across the iOS, Android, and Windows versions of an app, the developer must work with APNS (Apple Push Notification Service), FCM (Firebase Cloud Messaging), and WNS (Windows Notification Service), while batching the sends.</span></span>

<span data-ttu-id="4a022-128">概括而言，以下是推播功能的運作方式︰</span><span class="sxs-lookup"><span data-stu-id="4a022-128">At a high level, here is how push works:</span></span>

1. <span data-ttu-id="4a022-129">用戶端應用程式決定它要接收推播，因此連絡對應的 PNS 以擷取其唯一且暫時的推播控制代碼。</span><span class="sxs-lookup"><span data-stu-id="4a022-129">The client app decides it wants to receive pushes hence contacts the corresponding PNS to retrieve its unique and temporary push handle.</span></span> <span data-ttu-id="4a022-130">控制代碼類型取決於系統 (例如 WNS 有 URI，APNS 則有權杖)。</span><span class="sxs-lookup"><span data-stu-id="4a022-130">The handle type depends on the system (e.g. WNS has URIs while APNS has tokens).</span></span>
2. <span data-ttu-id="4a022-131">用戶端應用程式會將此控制代碼儲存在應用程式後端或提供者。</span><span class="sxs-lookup"><span data-stu-id="4a022-131">The client app stores this handle in the app back-end or provider.</span></span>
3. <span data-ttu-id="4a022-132">若要傳送推播通知，應用程式後端必須使用控制代碼連絡 PNS，以將特定的用戶端應用程式定為目標。</span><span class="sxs-lookup"><span data-stu-id="4a022-132">To send a push notification, the app back-end contacts the PNS using the handle to target a specific client app.</span></span>
4. <span data-ttu-id="4a022-133">PNS 會將通知轉送至控制代碼所指定的裝置。</span><span class="sxs-lookup"><span data-stu-id="4a022-133">The PNS forwards the notification to the device specified by the handle.</span></span>

![][0]

## <a name="the-challenges-of-push-notifications"></a><span data-ttu-id="4a022-134">推播通知的挑戰</span><span class="sxs-lookup"><span data-stu-id="4a022-134">The Challenges of Push Notifications</span></span>
<span data-ttu-id="4a022-135">儘管 PNS 非常強大，但即便 App 開發人員想要實作一般的推播通知工作 (例如廣播或傳送推播通知給分段式使用者)，都有許多工作有待處理。</span><span class="sxs-lookup"><span data-stu-id="4a022-135">While PNSes are powerful, they leave much work to the app developer in order to implement even common push notification scenarios, such as broadcasting or sending push notifications to segmented users.</span></span>

<span data-ttu-id="4a022-136">推播是行動雲端服務中其中一項最常被要求的功能，因為它的運作需要與應用程式的主要商業邏輯沒有關聯的複雜基礎結構。</span><span class="sxs-lookup"><span data-stu-id="4a022-136">Push is one of the most requested features in mobile cloud services, because its working requires complex infrastructures that are unrelated to the app's main business logic.</span></span> <span data-ttu-id="4a022-137">基礎結構方面的某些挑戰包括︰</span><span class="sxs-lookup"><span data-stu-id="4a022-137">Some of the infrastructural challenges are:</span></span>

* <span data-ttu-id="4a022-138">**平台相依性**：</span><span class="sxs-lookup"><span data-stu-id="4a022-138">**Platform dependency**:</span></span> 

  * <span data-ttu-id="4a022-139">後端必須有複雜且難以維護之取決於平台的邏輯，才能將通知傳送給各種平台上的裝置，因為 PNS 並未統一。</span><span class="sxs-lookup"><span data-stu-id="4a022-139">The backend needs to have complex and hard-to-maintain platform-dependent logic to send notifications to devices on various platforms as PNSes are not unified.</span></span>
* <span data-ttu-id="4a022-140">**調整**：</span><span class="sxs-lookup"><span data-stu-id="4a022-140">**Scale**:</span></span>

  * <span data-ttu-id="4a022-141">根據 PNS 準則，在每次啟動應用程式時，都必須重新整理裝置權杖。</span><span class="sxs-lookup"><span data-stu-id="4a022-141">Per PNS guidelines, device tokens must be refreshed upon every app launch.</span></span> <span data-ttu-id="4a022-142">這表示後端會處理大量的流量以及資料庫的存取權，卻只是為了讓權杖保持最新狀態。</span><span class="sxs-lookup"><span data-stu-id="4a022-142">This means the backend is dealing with a large amount of traffic and database access just to keep the tokens up-to-date.</span></span> <span data-ttu-id="4a022-143">當裝置數目增加至數億和數十億時，建立及維護此基礎結構的成本將會很可觀。</span><span class="sxs-lookup"><span data-stu-id="4a022-143">When the number of devices grows to hundreds and thousands of millions, the cost of creating and maintaining this infrastructure is massive.</span></span>
  * <span data-ttu-id="4a022-144">大部分的 PNS 並不支援廣播至多個裝置。</span><span class="sxs-lookup"><span data-stu-id="4a022-144">Most PNSes do not support broadcast to multiple devices.</span></span> <span data-ttu-id="4a022-145">這表示單單是對百萬個裝置的廣播就會產生百萬個 PNS 呼叫。</span><span class="sxs-lookup"><span data-stu-id="4a022-145">This means a simple broadcast to a million devices results in a million calls to the PNSes.</span></span> <span data-ttu-id="4a022-146">想要擴增這種數量的流量卻又要將延遲降到最低並非易事。</span><span class="sxs-lookup"><span data-stu-id="4a022-146">Scaling this amount of traffic with minimal latency is nontrivial.</span></span>
* <span data-ttu-id="4a022-147">**路由**：</span><span class="sxs-lookup"><span data-stu-id="4a022-147">**Routing**:</span></span>
  
  * <span data-ttu-id="4a022-148">雖然 PNS 提供了將訊息傳送至裝置的方法，但大部分應用程式通知都是以使用者或相關群組為目標。</span><span class="sxs-lookup"><span data-stu-id="4a022-148">Though PNSes provide a way to send messages to devices, most apps notifications are targeted at users or interest groups.</span></span> <span data-ttu-id="4a022-149">這表示後端必須維護登錄，以將裝置關聯到相關群組、使用者、屬性等。這項額外工作將導致應用程式的上市時程延宕和維護成本提高。</span><span class="sxs-lookup"><span data-stu-id="4a022-149">This means the backend must maintain a registry to associate devices with interest groups, users, properties, etc. This overhead adds to the time to market and maintenance costs of an app.</span></span>

## <a name="why-use-notification-hubs"></a><span data-ttu-id="4a022-150">為何要使用通知中心？</span><span class="sxs-lookup"><span data-stu-id="4a022-150">Why Use Notification Hubs?</span></span>
<span data-ttu-id="4a022-151">通知中樞會消除所有與自行啟用推播相關聯的複雜工作。</span><span class="sxs-lookup"><span data-stu-id="4a022-151">Notification Hubs eliminates all complexities associated with enabling push on your own.</span></span> <span data-ttu-id="4a022-152">其多平台、可相應放大的推播通知基礎結構可減少推播相關程式碼，並簡化您的後端。</span><span class="sxs-lookup"><span data-stu-id="4a022-152">Its multi-platform, scaled-out push notification infrastructure reduces push-related codes and simplifies your backend.</span></span> <span data-ttu-id="4a022-153">使用通知中樞時，裝置只需負責向中樞註冊其 PNS 控制代碼，而由後端負責將訊息傳送給使用者或相關群組，如下圖所示︰</span><span class="sxs-lookup"><span data-stu-id="4a022-153">With Notification Hubs, devices are merely responsible for registering their PNS handles with a hub, while the backend sends messages to users or interest groups, as shown in the following figure:</span></span>

![][1]

<span data-ttu-id="4a022-154">通知中樞是立即可用的推播引擎，其具有下列優勢︰</span><span class="sxs-lookup"><span data-stu-id="4a022-154">Notification hubs is your ready-to-use push engine with the following advantages:</span></span>

* <span data-ttu-id="4a022-155">**跨平台**</span><span class="sxs-lookup"><span data-stu-id="4a022-155">**Cross platforms**</span></span>

  * <span data-ttu-id="4a022-156">支援所有主要的推播平台，包括 iOS、Android、Windows、Kindle 和百度。</span><span class="sxs-lookup"><span data-stu-id="4a022-156">Support for all major push platforms including iOS, Android, Windows, and Kindle and Baidu.</span></span>
  * <span data-ttu-id="4a022-157">具有通用介面，可以平台特定或平台無關的格式推播至所有平台，但不必進行平台特定工作。</span><span class="sxs-lookup"><span data-stu-id="4a022-157">A common interface to push to all platforms in platform-specific or platform-independent formats with no platform-specific work.</span></span>
  * <span data-ttu-id="4a022-158">集中在一個位置管理裝置控制代碼。</span><span class="sxs-lookup"><span data-stu-id="4a022-158">Device handle management in one place.</span></span>
* <span data-ttu-id="4a022-159">**跨後端**</span><span class="sxs-lookup"><span data-stu-id="4a022-159">**Cross backends**</span></span>
  
  * <span data-ttu-id="4a022-160">雲端或內部部署</span><span class="sxs-lookup"><span data-stu-id="4a022-160">Cloud or on-premises</span></span>
  * <span data-ttu-id="4a022-161">.NET、Node.js、Java 等</span><span class="sxs-lookup"><span data-stu-id="4a022-161">.NET, Node.js, Java, etc.</span></span>
* <span data-ttu-id="4a022-162">**豐富的傳遞模式集**：</span><span class="sxs-lookup"><span data-stu-id="4a022-162">**Rich set of delivery patterns**:</span></span>

  * <span data-ttu-id="4a022-163">*廣播到一個或多個平台*︰只要單一 API 呼叫，您就可以立即跨平台廣播到數百萬個裝置。</span><span class="sxs-lookup"><span data-stu-id="4a022-163">*Broadcast to one or multiple platforms*: You can instantly broadcast to millions of devices across platforms with a single API call.</span></span>
  * <span data-ttu-id="4a022-164">*推播到裝置*︰您可以將通知目標鎖定為個別裝置。</span><span class="sxs-lookup"><span data-stu-id="4a022-164">*Push to device*: You can target notifications to individual devices.</span></span>
  * <span data-ttu-id="4a022-165">*推播到使用者*︰標記和範本功能可協助您觸達某位使用者的所有跨平台裝置。</span><span class="sxs-lookup"><span data-stu-id="4a022-165">*Push to user*: Tags and templates features help you reach all cross-platform devices of a user.</span></span>
  * <span data-ttu-id="4a022-166">*以動態標記推播至區段*︰標記功能可協助您將裝置分區段，並根據您的需求推播至這些區段，不論您是要傳送給一個區段或一個運算式的區段 (例如 active AND lives in Seattle NOT new user)。</span><span class="sxs-lookup"><span data-stu-id="4a022-166">*Push to segment with dynamic tags*: Tags feature helps you segment devices and push to them according to your needs, whether you are sending to one segment or an expression of segments (e.g. active AND lives in Seattle NOT new user).</span></span> <span data-ttu-id="4a022-167">不必侷限於發行/訂閱模式，您可以隨時隨地更新裝置的標記。</span><span class="sxs-lookup"><span data-stu-id="4a022-167">Instead of being restricted to pub-sub, you can update device tags anywhere and anytime.</span></span>
  * <span data-ttu-id="4a022-168">*當地語系化的推播*︰範本功能可協助您實現當地語系化，又不影響後端程式碼。</span><span class="sxs-lookup"><span data-stu-id="4a022-168">*Localized push*: Templates feature helps achieve localization without affecting backend code.</span></span>
  * <span data-ttu-id="4a022-169">*無訊息推播*︰您可以將無訊息通知傳送至裝置，並觸發它們以完成特定提取或動作，以啟用推播到提取模式。</span><span class="sxs-lookup"><span data-stu-id="4a022-169">*Silent push*: You can enables the push-to-pull pattern by sending silent notifications to devices and triggering them to complete certain pulls or actions.</span></span>
  * <span data-ttu-id="4a022-170">*排定推播*︰您可以排程在任何時間傳送通知。</span><span class="sxs-lookup"><span data-stu-id="4a022-170">*Scheduled push*: You can schedule to send out notifications anytime.</span></span>
  * <span data-ttu-id="4a022-171">*直接推播*︰您可以略過向我們的服務註冊裝置的動作，並直接批次推播至裝置控制代碼清單。</span><span class="sxs-lookup"><span data-stu-id="4a022-171">*Direct push*: You can skip registering devices with our service and directly batch push to a list of device handles.</span></span>
  * <span data-ttu-id="4a022-172">*個人化推播*︰裝置推播變數可協助您以自訂的索引鍵/值組傳送裝置特定的個人化推播通知。</span><span class="sxs-lookup"><span data-stu-id="4a022-172">*Personalized push*: Device push variables helps you send device-specific personalized push notifications with customized key-value pairs.</span></span>
* <span data-ttu-id="4a022-173">**豐富的遙測**</span><span class="sxs-lookup"><span data-stu-id="4a022-173">**Rich telemetry**</span></span>
  
  * <span data-ttu-id="4a022-174">您可以在 Azure 入口網站或以程式設計方式取得一般的推播、裝置、錯誤和作業遙測。</span><span class="sxs-lookup"><span data-stu-id="4a022-174">General push, device, error, and operation telemetry is available in the Azure portal and programmatically.</span></span>
  * <span data-ttu-id="4a022-175">每一訊息遙測會追蹤每個推播從初始要求呼叫到我們的服務成功批次處理推播的過程。</span><span class="sxs-lookup"><span data-stu-id="4a022-175">Per Message Telemetry tracks each push from your initial request call to our service successfully batching the pushes out.</span></span>
  * <span data-ttu-id="4a022-176">平台通知系統意見反應會傳送平台通知系統的所有意見反應，以協助偵錯。</span><span class="sxs-lookup"><span data-stu-id="4a022-176">Platform Notification System Feedback communicates all feedback from Platfom Notification Systems to assist in debugging.</span></span>
* <span data-ttu-id="4a022-177">**延展性**</span><span class="sxs-lookup"><span data-stu-id="4a022-177">**Scalability**</span></span> 
  
  * <span data-ttu-id="4a022-178">將快速訊息傳送至數百萬個裝置，而不需要經過重新架構或裝置分區化程序。</span><span class="sxs-lookup"><span data-stu-id="4a022-178">Send fast messages to millions of devices without re-architecting or device sharding.</span></span>
* <span data-ttu-id="4a022-179">**安全性**</span><span class="sxs-lookup"><span data-stu-id="4a022-179">**Security**</span></span>

  * <span data-ttu-id="4a022-180">共用存取密碼 (SAS) 或同盟驗證。</span><span class="sxs-lookup"><span data-stu-id="4a022-180">Shared Access Secret (SAS) or federated authentication.</span></span>

## <a name="integration-with-app-service-mobile-apps"></a><span data-ttu-id="4a022-181">與 App Service Mobile Apps 整合</span><span class="sxs-lookup"><span data-stu-id="4a022-181">Integration with App Service Mobile Apps</span></span>
<span data-ttu-id="4a022-182">為了在 Azure 服務間促進完美且統一的體驗， [App Service Mobile Apps] 具備使用通知中樞提供推播通知的內建支援。</span><span class="sxs-lookup"><span data-stu-id="4a022-182">To facilitate a seamless and unifying experience across Azure services, [App Service Mobile Apps] has built-in support for push notifications using Notification Hubs.</span></span> <span data-ttu-id="4a022-183">[App Service Mobile Apps] 具有高擴充性且可供全球使用，是專為企業開發人員與系統整合人員設計的行動應用程式開發平台，能提供一組豐富的功能給行動應用程式開發人員。</span><span class="sxs-lookup"><span data-stu-id="4a022-183">[App Service Mobile Apps] offers a highly scalable, globally available mobile application development platform for Enterprise Developers and System Integrators that brings a rich set of capabilities to mobile developers.</span></span>

<span data-ttu-id="4a022-184">Mobile Apps 開發人員可以使用下列流程來利用通知中樞：</span><span class="sxs-lookup"><span data-stu-id="4a022-184">Mobile Apps developers can utilize Notification Hubs with the following workflow:</span></span>

1. <span data-ttu-id="4a022-185">擷取裝置 PNS 控制代碼</span><span class="sxs-lookup"><span data-stu-id="4a022-185">Retrieve device PNS handle</span></span>
2. <span data-ttu-id="4a022-186">透過便利的 Mobile Apps Client SDK 註冊 API，使用通知中樞註冊裝置</span><span class="sxs-lookup"><span data-stu-id="4a022-186">Register device with Notification Hubs through convenient Mobile Apps Client SDK register API</span></span>
   * <span data-ttu-id="4a022-187">請注意，Mobile Apps 會基於安全性考量，去除註冊上的所有標籤。</span><span class="sxs-lookup"><span data-stu-id="4a022-187">Note that Mobile Apps strips away all tags on registrations for security purposes.</span></span> <span data-ttu-id="4a022-188">直接從後端使用通知中樞，將標籤關聯至裝置。</span><span class="sxs-lookup"><span data-stu-id="4a022-188">Work with Notification Hubs from your backend directly to associate tags with devices.</span></span>
3. <span data-ttu-id="4a022-189">從 App 後端使用通知中樞傳送通知</span><span class="sxs-lookup"><span data-stu-id="4a022-189">Send notifications from your app backend with Notification Hubs</span></span>

<span data-ttu-id="4a022-190">以下是透過此註冊為開發人員帶來的一些便利性：</span><span class="sxs-lookup"><span data-stu-id="4a022-190">Here are some conveniences brought to developers with this integration:</span></span>

* <span data-ttu-id="4a022-191">**Mobile Apps 用戶端 SDK**︰這些多平台 SDK 提供簡單的 API 來進行註冊，然後會自動與連結到行動 App 的通知中樞聯繫。</span><span class="sxs-lookup"><span data-stu-id="4a022-191">**Mobile Apps Client SDKs**: These multi-platform SDKs provide simple APIs for registration and talk to the notification hub linked up with the mobile app automatically.</span></span> <span data-ttu-id="4a022-192">開發人員不需要透過通知中樞認證進行挖掘，以及使用其他服務。</span><span class="sxs-lookup"><span data-stu-id="4a022-192">Developers do not need to dig through Notification Hubs credentials and work with an additional service.</span></span>

  * <span data-ttu-id="4a022-193">*推播給使用者*：SDK 會使用 Mobile Apps 驗證的使用者識別碼自動標記指定的裝置，以啟用推播至使用者案例。</span><span class="sxs-lookup"><span data-stu-id="4a022-193">*Push to user*: The SDKs automatically tag the given device with Mobile Apps authenticated User ID to enable push to user scenario.</span></span>
  * <span data-ttu-id="4a022-194">*推播至裝置*：SDK 會自動使用 Mobile Apps 安裝識別碼做為 GUID 來向通知中樞註冊，省去開發人員維護多個服務 GUID 的麻煩。</span><span class="sxs-lookup"><span data-stu-id="4a022-194">*Push to device*: The SDKs automatically use the Mobile Apps Installation ID as GUID to register with Notification Hubs, saving developers the trouble of maintaining multiple service GUIDs.</span></span>
* <span data-ttu-id="4a022-195">**安裝模式**：Mobile Apps 會使用通知中樞的最新推送模型，來呈現 JSON 安裝中所有與裝置相關聯的推送屬性，其會與推播通知密切合作且易於使用。</span><span class="sxs-lookup"><span data-stu-id="4a022-195">**Installation model**: Mobile Apps works with Notification Hubs' latest push model to represent all push properties associated with a device in a JSON Installation that aligns with Push Notification Services and is easy to use.</span></span>
* <span data-ttu-id="4a022-196">**彈性**：即使已就地整合，開發人員一律還是可以選擇直接使用通知中樞。</span><span class="sxs-lookup"><span data-stu-id="4a022-196">**Flexibility**: Developers can always choose to work with Notification Hubs directly even with the integration in place.</span></span>
* <span data-ttu-id="4a022-197">**[Azure 入口網站]中的整合式體驗**：Mobile Apps 中會以視覺化方式呈現以功能形式出現的推送，而開發人員可以透過 Mobile Apps 輕鬆使用相關聯的通知中樞。</span><span class="sxs-lookup"><span data-stu-id="4a022-197">**Integrated experience in [Azure portal]**: Push as a capability is represented visually in Mobile Apps and developers can easily work with the associated notification hub through Mobile Apps.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4a022-198">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4a022-198">Next Steps</span></span>
<span data-ttu-id="4a022-199">您可以在以下主題找到「通知中樞」的詳細資訊：</span><span class="sxs-lookup"><span data-stu-id="4a022-199">You can find out more about Notification Hubs in these topics:</span></span>

* <span data-ttu-id="4a022-200">**[客戶如何使用通知中樞]**</span><span class="sxs-lookup"><span data-stu-id="4a022-200">**[How customers are using Notification Hubs]**</span></span>
* <span data-ttu-id="4a022-201">**[通知中樞教學課程和指南]**</span><span class="sxs-lookup"><span data-stu-id="4a022-201">**[Notification Hubs tutorials and guides]**</span></span>
* <span data-ttu-id="4a022-202">**通知中樞快速入門教學課程**：[iOS]、[Android]、[Windows Universal]、[Windows Phone]、[Kindle]、[Xamarin.iOS]、[Xamarin.Android]</span><span class="sxs-lookup"><span data-stu-id="4a022-202">**Notification Hubs Getting Started tutorials**: [iOS], [Android], [Windows Universal], [Windows Phone], [Kindle], [Xamarin.iOS], [Xamarin.Android]</span></span>

[0]: ./media/notification-hubs-overview/registration-diagram.png
[1]: ./media/notification-hubs-overview/notification-hub-diagram.png
<span data-ttu-id="4a022-203">[客戶如何使用通知中樞]: http://azure.microsoft.com/services/notification-hubs</span><span class="sxs-lookup"><span data-stu-id="4a022-203">[How customers are using Notification Hubs]: http://azure.microsoft.com/services/notification-hubs</span></span>
<span data-ttu-id="4a022-204">[通知中樞教學課程和指南]: http://azure.microsoft.com/documentation/services/notification-hubs</span><span class="sxs-lookup"><span data-stu-id="4a022-204">[Notification Hubs tutorials and guides]: http://azure.microsoft.com/documentation/services/notification-hubs</span></span>
<span data-ttu-id="4a022-205">[iOS]: http://azure.microsoft.com/documentation/articles/notification-hubs-ios-get-started</span><span class="sxs-lookup"><span data-stu-id="4a022-205">[iOS]: http://azure.microsoft.com/documentation/articles/notification-hubs-ios-get-started</span></span>
<span data-ttu-id="4a022-206">[Android]: http://azure.microsoft.com/documentation/articles/notification-hubs-android-get-started</span><span class="sxs-lookup"><span data-stu-id="4a022-206">[Android]: http://azure.microsoft.com/documentation/articles/notification-hubs-android-get-started</span></span>
<span data-ttu-id="4a022-207">[Windows Universal]: http://azure.microsoft.com/documentation/articles/notification-hubs-windows-store-dotnet-get-started</span><span class="sxs-lookup"><span data-stu-id="4a022-207">[Windows Universal]: http://azure.microsoft.com/documentation/articles/notification-hubs-windows-store-dotnet-get-started</span></span>
<span data-ttu-id="4a022-208">[Windows Phone]: http://azure.microsoft.com/documentation/articles/notification-hubs-windows-phone-get-started</span><span class="sxs-lookup"><span data-stu-id="4a022-208">[Windows Phone]: http://azure.microsoft.com/documentation/articles/notification-hubs-windows-phone-get-started</span></span>
<span data-ttu-id="4a022-209">[Kindle]: http://azure.microsoft.com/documentation/articles/notification-hubs-kindle-get-started</span><span class="sxs-lookup"><span data-stu-id="4a022-209">[Kindle]: http://azure.microsoft.com/documentation/articles/notification-hubs-kindle-get-started</span></span>
<span data-ttu-id="4a022-210">[Xamarin.iOS]: http://azure.microsoft.com/documentation/articles/partner-xamarin-notification-hubs-ios-get-started</span><span class="sxs-lookup"><span data-stu-id="4a022-210">[Xamarin.iOS]: http://azure.microsoft.com/documentation/articles/partner-xamarin-notification-hubs-ios-get-started</span></span>
<span data-ttu-id="4a022-211">[Xamarin.Android]: http://azure.microsoft.com/documentation/articles/partner-xamarin-notification-hubs-android-get-started</span><span class="sxs-lookup"><span data-stu-id="4a022-211">[Xamarin.Android]: http://azure.microsoft.com/documentation/articles/partner-xamarin-notification-hubs-android-get-started</span></span>
[Microsoft.WindowsAzure.Messaging.NotificationHub]: http://msdn.microsoft.com/library/microsoft.windowsazure.messaging.notificationhub.aspx
[Microsoft.ServiceBus.Notifications]: http://msdn.microsoft.com/library/microsoft.servicebus.notifications.aspx
<span data-ttu-id="4a022-212">[App Service Mobile Apps]: https://azure.microsoft.com/en-us/documentation/articles/app-service-mobile-value-prop/</span><span class="sxs-lookup"><span data-stu-id="4a022-212">[App Service Mobile Apps]: https://azure.microsoft.com/en-us/documentation/articles/app-service-mobile-value-prop/</span></span>
[templates]: notification-hubs-templates-cross-platform-push-messages.md
<span data-ttu-id="4a022-213">[Azure 入口網站]: https://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="4a022-213">[Azure portal]: https://portal.azure.com</span></span>
[tags]: (http://msdn.microsoft.com/library/azure/dn530749.aspx)
