---
title: "aaaAzure 通知中樞"
description: "了解如何 tooadd 推播通知功能與 Azure 通知中心。"
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
ms.openlocfilehash: 78ce34b6b094b560c8002ab9652f7ba4563c5c74
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-notification-hubs"></a><span data-ttu-id="993dd-103">Azure 通知中心</span><span class="sxs-lookup"><span data-stu-id="993dd-103">Azure Notification Hubs</span></span>
## <a name="overview"></a><span data-ttu-id="993dd-104">概觀</span><span class="sxs-lookup"><span data-stu-id="993dd-104">Overview</span></span>
<span data-ttu-id="993dd-105">Azure 通知中樞提供方便使用、多平台、可相應放大的推播引擎。</span><span class="sxs-lookup"><span data-stu-id="993dd-105">Azure Notification Hubs provide an easy-to-use, multi-platform, scaled-out push engine.</span></span> <span data-ttu-id="993dd-106">透過單一跨平台 API 呼叫，您可以輕鬆地從任何雲端或內部部署的後端傳送目標及個人化的推播通知 tooany 行動平台。</span><span class="sxs-lookup"><span data-stu-id="993dd-106">With a single cross-platform API call, you can easily send targeted and personalized push notifications tooany mobile platform from any cloud or on-premises backend.</span></span>

<span data-ttu-id="993dd-107">通知中樞很適合企業和消費者案例。</span><span class="sxs-lookup"><span data-stu-id="993dd-107">Notification Hubs works great for both enterprise and consumer scenarios.</span></span> <span data-ttu-id="993dd-108">以下是一些客戶使用通知中樞之用途的範例︰</span><span class="sxs-lookup"><span data-stu-id="993dd-108">Here are a few examples customers use Notification Hubs for:</span></span>

* <span data-ttu-id="993dd-109">傳送重大消息通知 toomillions 與低度延遲。</span><span class="sxs-lookup"><span data-stu-id="993dd-109">Send breaking news notifications toomillions with low latency.</span></span>
* <span data-ttu-id="993dd-110">傳送以位置為基礎的優待券 toointerested 使用者區段。</span><span class="sxs-lookup"><span data-stu-id="993dd-110">Send location-based coupons toointerested user segments.</span></span>
* <span data-ttu-id="993dd-111">傳送事件相關的通知 toousers 或群組的媒體/運動/finance/遊戲應用程式。</span><span class="sxs-lookup"><span data-stu-id="993dd-111">Send event-related notifications toousers or groups for media/sports/finance/gaming applications.</span></span>
* <span data-ttu-id="993dd-112">推送促銷內容 tooapps tooengage 和市場 toocustomers。</span><span class="sxs-lookup"><span data-stu-id="993dd-112">Push promotional contents tooapps tooengage and market toocustomers.</span></span>
* <span data-ttu-id="993dd-113">對使用者發送企業事件通知，例如新訊息和工作項目。</span><span class="sxs-lookup"><span data-stu-id="993dd-113">Notify users of enterprise events like new messages and work items.</span></span>
* <span data-ttu-id="993dd-114">傳送 Multi-Factor Authentication 的程式碼。</span><span class="sxs-lookup"><span data-stu-id="993dd-114">Send codes for multi-factor authentication.</span></span>

## <a name="what-are-push-notifications"></a><span data-ttu-id="993dd-115">什麼是推播通知？</span><span class="sxs-lookup"><span data-stu-id="993dd-115">What are Push Notifications?</span></span>
<span data-ttu-id="993dd-116">推播通知是一種由應用程式對使用者發出的通訊形式，通常會以快顯視窗或對話方塊來對行動應用程式的使用者發出某些他們想要之資訊的通知。</span><span class="sxs-lookup"><span data-stu-id="993dd-116">Push notifications is a form of app-to-user communication where users of mobile apps are notified of certain desired information, usually in a pop-up or dialog box.</span></span> <span data-ttu-id="993dd-117">使用者通常可以選擇 tooview 或關閉 hello 訊息，並選擇 hello 前者會開啟傳 hello 通知 hello 行動裝置應用程式。</span><span class="sxs-lookup"><span data-stu-id="993dd-117">Users can generally choose tooview or dismiss hello message, and choosing hello former will open hello mobile app that had communicated hello notification.</span></span>

<span data-ttu-id="993dd-118">推播通知是很重要的功能，對於消費者應用程式來說，可提高應用程式的參與和使用率，對於企業應用程式來說，則可傳送最新的企業資訊。</span><span class="sxs-lookup"><span data-stu-id="993dd-118">Push notifications is vital for consumer apps in increasing app engagement and usage, and for enterprise apps in communicating up-to-date business information.</span></span> <span data-ttu-id="993dd-119">它是 hello 最佳應用程式對使用者的通訊，因為對應的應用程式都沒有作用時，它是能源的彈性 hello 通知寄件者和可用的行動裝置。</span><span class="sxs-lookup"><span data-stu-id="993dd-119">It is hello best app-to-user communication because it is energy-efficient for  mobile devices, flexible for hello notifications senders, and available while corresponding apps are not active.</span></span>

<span data-ttu-id="993dd-120">如需某些熱門平台的推播通知詳細資訊︰</span><span class="sxs-lookup"><span data-stu-id="993dd-120">For more information on push notifications for a few popular platforms:</span></span>
* [<span data-ttu-id="993dd-121">iOS</span><span class="sxs-lookup"><span data-stu-id="993dd-121">iOS</span></span>](https://developer.apple.com/notifications/)
* [<span data-ttu-id="993dd-122">Android</span><span class="sxs-lookup"><span data-stu-id="993dd-122">Android</span></span>](https://developer.android.com/guide/topics/ui/notifiers/notifications.html)
* [<span data-ttu-id="993dd-123">Windows</span><span class="sxs-lookup"><span data-stu-id="993dd-123">Windows</span></span>](http://msdn.microsoft.com/library/windows/apps/hh779725.aspx)

## <a name="how-push-notifications-work"></a><span data-ttu-id="993dd-124">推播通知的運作方式</span><span class="sxs-lookup"><span data-stu-id="993dd-124">How Push Notifications Work</span></span>
<span data-ttu-id="993dd-125">推播通知可透過名為「平台通知系統 (PNS)」的平台特定基礎結構來傳遞。</span><span class="sxs-lookup"><span data-stu-id="993dd-125">Push notifications are delivered through platform-specific infrastructures called *Platform Notification Systems* (PNSes).</span></span> <span data-ttu-id="993dd-126">它們提供 barebone 推播功能 toodelivery 訊息 tooa 裝置具有提供處理，且沒有通用介面。</span><span class="sxs-lookup"><span data-stu-id="993dd-126">They offer barebone push functionalities toodelivery message tooa device with a provided handle, and have no common interface.</span></span> <span data-ttu-id="993dd-127">toosend 通知 tooall 客戶跨 hello iOS、 Android 和 Windows 應用程式的版本中，hello 開發人員必須處理 APNS (Apple Push Notification Service)、 FCM (Firebase Cloud Messaging)，與 WNS （Windows 通知服務），同時批次處理會傳送 hello。</span><span class="sxs-lookup"><span data-stu-id="993dd-127">toosend a notification tooall customers across hello iOS, Android, and Windows versions of an app, hello developer must work with APNS (Apple Push Notification Service), FCM (Firebase Cloud Messaging), and WNS (Windows Notification Service), while batching hello sends.</span></span>

<span data-ttu-id="993dd-128">概括而言，以下是推播功能的運作方式︰</span><span class="sxs-lookup"><span data-stu-id="993dd-128">At a high level, here is how push works:</span></span>

1. <span data-ttu-id="993dd-129">hello 用戶端應用程式會決定它想 tooreceive 推播通知因此連絡人 hello 對應 PNS tooretrieve 其唯一且暫時推送控制代碼。</span><span class="sxs-lookup"><span data-stu-id="993dd-129">hello client app decides it wants tooreceive pushes hence contacts hello corresponding PNS tooretrieve its unique and temporary push handle.</span></span> <span data-ttu-id="993dd-130">hello 控制代碼類型取決於 hello 系統 （例如 WNS 有 Uri APNS 有語彙基元）。</span><span class="sxs-lookup"><span data-stu-id="993dd-130">hello handle type depends on hello system (e.g. WNS has URIs while APNS has tokens).</span></span>
2. <span data-ttu-id="993dd-131">hello 用戶端應用程式會將此控制代碼儲存在 hello 應用程式後端 」 或 「 提供者。</span><span class="sxs-lookup"><span data-stu-id="993dd-131">hello client app stores this handle in hello app back-end or provider.</span></span>
3. <span data-ttu-id="993dd-132">toosend 使用 hello PNS 處理 tootarget 特定用戶端應用程式的推播通知 hello 應用程式後端連絡人 hello。</span><span class="sxs-lookup"><span data-stu-id="993dd-132">toosend a push notification, hello app back-end contacts hello PNS using hello handle tootarget a specific client app.</span></span>
4. <span data-ttu-id="993dd-133">hello PNS 轉送 hello 通知 toohello 裝置 hello 控制代碼所指定。</span><span class="sxs-lookup"><span data-stu-id="993dd-133">hello PNS forwards hello notification toohello device specified by hello handle.</span></span>

![][0]

## <a name="hello-challenges-of-push-notifications"></a><span data-ttu-id="993dd-134">hello 的推播通知的挑戰</span><span class="sxs-lookup"><span data-stu-id="993dd-134">hello Challenges of Push Notifications</span></span>
<span data-ttu-id="993dd-135">雖然 PNSes 強大，它們將保留在多工作 toohello 應用程式開發人員順序 tooimplement 甚至常見推播通知案例中，例如廣播或傳送推播通知 toosegmented 使用者。</span><span class="sxs-lookup"><span data-stu-id="993dd-135">While PNSes are powerful, they leave much work toohello app developer in order tooimplement even common push notification scenarios, such as broadcasting or sending push notifications toosegmented users.</span></span>

<span data-ttu-id="993dd-136">推播是其中一個 hello 最常要求行動裝置的雲端服務的功能，因為它的工作需要複雜的基礎結構，是不相關的 toohello 應用程式的主要商務邏輯。</span><span class="sxs-lookup"><span data-stu-id="993dd-136">Push is one of hello most requested features in mobile cloud services, because its working requires complex infrastructures that are unrelated toohello app's main business logic.</span></span> <span data-ttu-id="993dd-137">Hello 實際上挑戰的部分包括：</span><span class="sxs-lookup"><span data-stu-id="993dd-137">Some of hello infrastructural challenges are:</span></span>

* <span data-ttu-id="993dd-138">**平台相依性**：</span><span class="sxs-lookup"><span data-stu-id="993dd-138">**Platform dependency**:</span></span> 

  * <span data-ttu-id="993dd-139">hello 後端需要 toohave 複雜且困難維護平台相依邏輯 toosend 在各種平台上的通知 toodevices PNSes 將不一致。</span><span class="sxs-lookup"><span data-stu-id="993dd-139">hello backend needs toohave complex and hard-to-maintain platform-dependent logic toosend notifications toodevices on various platforms as PNSes are not unified.</span></span>
* <span data-ttu-id="993dd-140">**調整**：</span><span class="sxs-lookup"><span data-stu-id="993dd-140">**Scale**:</span></span>

  * <span data-ttu-id="993dd-141">根據 PNS 準則，在每次啟動應用程式時，都必須重新整理裝置權杖。</span><span class="sxs-lookup"><span data-stu-id="993dd-141">Per PNS guidelines, device tokens must be refreshed upon every app launch.</span></span> <span data-ttu-id="993dd-142">這表示 hello 後端處理大量的流量和資料庫存取只 tookeep hello 權杖保持最新狀態。</span><span class="sxs-lookup"><span data-stu-id="993dd-142">This means hello backend is dealing with a large amount of traffic and database access just tookeep hello tokens up-to-date.</span></span> <span data-ttu-id="993dd-143">裝置 hello 數目成長 toohundreds 和無數百萬，建立並維護此基礎結構 hello 成本時，大量。</span><span class="sxs-lookup"><span data-stu-id="993dd-143">When hello number of devices grows toohundreds and thousands of millions, hello cost of creating and maintaining this infrastructure is massive.</span></span>
  * <span data-ttu-id="993dd-144">大部分 PNSes 不支援廣播的 toomultiple 裝置。</span><span class="sxs-lookup"><span data-stu-id="993dd-144">Most PNSes do not support broadcast toomultiple devices.</span></span> <span data-ttu-id="993dd-145">這表示簡單的廣播的 tooa 百萬個呼叫 toohello PNSes 數百萬個裝置產生。</span><span class="sxs-lookup"><span data-stu-id="993dd-145">This means a simple broadcast tooa million devices results in a million calls toohello PNSes.</span></span> <span data-ttu-id="993dd-146">想要擴增這種數量的流量卻又要將延遲降到最低並非易事。</span><span class="sxs-lookup"><span data-stu-id="993dd-146">Scaling this amount of traffic with minimal latency is nontrivial.</span></span>
* <span data-ttu-id="993dd-147">**路由**：</span><span class="sxs-lookup"><span data-stu-id="993dd-147">**Routing**:</span></span>
  
  * <span data-ttu-id="993dd-148">雖然 PNSes 方式 toosend 訊息 toodevices，大部分的應用程式通知的適用對象的使用者或利益群組。</span><span class="sxs-lookup"><span data-stu-id="993dd-148">Though PNSes provide a way toosend messages toodevices, most apps notifications are targeted at users or interest groups.</span></span> <span data-ttu-id="993dd-149">這表示 hello 後端必須維護登錄 tooassociate 裝置與感興趣的群組、 使用者、 屬性等等。此項負擔會增加 toohello 階段 toomarket 和維護成本的應用程式。</span><span class="sxs-lookup"><span data-stu-id="993dd-149">This means hello backend must maintain a registry tooassociate devices with interest groups, users, properties, etc. This overhead adds toohello time toomarket and maintenance costs of an app.</span></span>

## <a name="why-use-notification-hubs"></a><span data-ttu-id="993dd-150">為何要使用通知中心？</span><span class="sxs-lookup"><span data-stu-id="993dd-150">Why Use Notification Hubs?</span></span>
<span data-ttu-id="993dd-151">通知中樞會消除所有與自行啟用推播相關聯的複雜工作。</span><span class="sxs-lookup"><span data-stu-id="993dd-151">Notification Hubs eliminates all complexities associated with enabling push on your own.</span></span> <span data-ttu-id="993dd-152">其多平台、可相應放大的推播通知基礎結構可減少推播相關程式碼，並簡化您的後端。</span><span class="sxs-lookup"><span data-stu-id="993dd-152">Its multi-platform, scaled-out push notification infrastructure reduces push-related codes and simplifies your backend.</span></span> <span data-ttu-id="993dd-153">與通知中樞的裝置是只負責註冊其 PNS 控制代碼集線器，雖然 hello 後端傳送訊息 toousers 或利益群組 hello 遵循圖所示：</span><span class="sxs-lookup"><span data-stu-id="993dd-153">With Notification Hubs, devices are merely responsible for registering their PNS handles with a hub, while hello backend sends messages toousers or interest groups, as shown in hello following figure:</span></span>

![][1]

<span data-ttu-id="993dd-154">通知中心是您已備妥要使用推播引擎以 hello 下列優點：</span><span class="sxs-lookup"><span data-stu-id="993dd-154">Notification hubs is your ready-to-use push engine with hello following advantages:</span></span>

* <span data-ttu-id="993dd-155">**跨平台**</span><span class="sxs-lookup"><span data-stu-id="993dd-155">**Cross platforms**</span></span>

  * <span data-ttu-id="993dd-156">支援所有主要的推播平台，包括 iOS、Android、Windows、Kindle 和百度。</span><span class="sxs-lookup"><span data-stu-id="993dd-156">Support for all major push platforms including iOS, Android, Windows, and Kindle and Baidu.</span></span>
  * <span data-ttu-id="993dd-157">通用介面 toopush tooall 平台特定平台上的任何平台專屬或平台無關的格式。</span><span class="sxs-lookup"><span data-stu-id="993dd-157">A common interface toopush tooall platforms in platform-specific or platform-independent formats with no platform-specific work.</span></span>
  * <span data-ttu-id="993dd-158">集中在一個位置管理裝置控制代碼。</span><span class="sxs-lookup"><span data-stu-id="993dd-158">Device handle management in one place.</span></span>
* <span data-ttu-id="993dd-159">**跨後端**</span><span class="sxs-lookup"><span data-stu-id="993dd-159">**Cross backends**</span></span>
  
  * <span data-ttu-id="993dd-160">雲端或內部部署</span><span class="sxs-lookup"><span data-stu-id="993dd-160">Cloud or on-premises</span></span>
  * <span data-ttu-id="993dd-161">.NET、Node.js、Java 等</span><span class="sxs-lookup"><span data-stu-id="993dd-161">.NET, Node.js, Java, etc.</span></span>
* <span data-ttu-id="993dd-162">**豐富的傳遞模式集**：</span><span class="sxs-lookup"><span data-stu-id="993dd-162">**Rich set of delivery patterns**:</span></span>

  * <span data-ttu-id="993dd-163">*廣播 tooone 或多個平台*： 您立即可以廣播 toomillions 裝置的跨平台，透過單一 API 呼叫。</span><span class="sxs-lookup"><span data-stu-id="993dd-163">*Broadcast tooone or multiple platforms*: You can instantly broadcast toomillions of devices across platforms with a single API call.</span></span>
  * <span data-ttu-id="993dd-164">*推播 toodevice*： 您可以通知 tooindividual 裝置為目標。</span><span class="sxs-lookup"><span data-stu-id="993dd-164">*Push toodevice*: You can target notifications tooindividual devices.</span></span>
  * <span data-ttu-id="993dd-165">*推播 toouser*： 標記和範本的功能可協助您達成所有跨平台裝置的使用者。</span><span class="sxs-lookup"><span data-stu-id="993dd-165">*Push toouser*: Tags and templates features help you reach all cross-platform devices of a user.</span></span>
  * <span data-ttu-id="993dd-166">*推送的動態標籤 toosegment*： 標記功能可協助您裝置分割並推送 toothem 根據 tooyour 需求，是否要傳送 tooone 區段或區段 （例如 active AND 生活同等程度不西雅圖新使用者） 的運算式。</span><span class="sxs-lookup"><span data-stu-id="993dd-166">*Push toosegment with dynamic tags*: Tags feature helps you segment devices and push toothem according tooyour needs, whether you are sending tooone segment or an expression of segments (e.g. active AND lives in Seattle NOT new user).</span></span> <span data-ttu-id="993dd-167">而不是受限制的 toopub sub，您可以更新裝置的標記任何地方和任何時候。</span><span class="sxs-lookup"><span data-stu-id="993dd-167">Instead of being restricted toopub-sub, you can update device tags anywhere and anytime.</span></span>
  * <span data-ttu-id="993dd-168">*當地語系化的推播*︰範本功能可協助您實現當地語系化，又不影響後端程式碼。</span><span class="sxs-lookup"><span data-stu-id="993dd-168">*Localized push*: Templates feature helps achieve localization without affecting backend code.</span></span>
  * <span data-ttu-id="993dd-169">*無訊息推入*： 您可以透過傳送無訊息的通知 toodevices 和觸發它們 toocomplete 啟用 hello 推入來提取模式，某些提取或動作。</span><span class="sxs-lookup"><span data-stu-id="993dd-169">*Silent push*: You can enables hello push-to-pull pattern by sending silent notifications toodevices and triggering them toocomplete certain pulls or actions.</span></span>
  * <span data-ttu-id="993dd-170">*排程的推播*： 您可以隨時排程 toosend 通知。</span><span class="sxs-lookup"><span data-stu-id="993dd-170">*Scheduled push*: You can schedule toosend out notifications anytime.</span></span>
  * <span data-ttu-id="993dd-171">*直接推送*： 您可以略過註冊裝置，與我們服務直接的裝置控制代碼的批次發送 tooa 清單。</span><span class="sxs-lookup"><span data-stu-id="993dd-171">*Direct push*: You can skip registering devices with our service and directly batch push tooa list of device handles.</span></span>
  * <span data-ttu-id="993dd-172">*個人化推播*︰裝置推播變數可協助您以自訂的索引鍵/值組傳送裝置特定的個人化推播通知。</span><span class="sxs-lookup"><span data-stu-id="993dd-172">*Personalized push*: Device push variables helps you send device-specific personalized push notifications with customized key-value pairs.</span></span>
* <span data-ttu-id="993dd-173">**豐富的遙測**</span><span class="sxs-lookup"><span data-stu-id="993dd-173">**Rich telemetry**</span></span>
  
  * <span data-ttu-id="993dd-174">目前不提供 hello Azure 入口網站中一般的推播、 裝置、 錯誤和作業遙測和以程式設計的方式。</span><span class="sxs-lookup"><span data-stu-id="993dd-174">General push, device, error, and operation telemetry is available in hello Azure portal and programmatically.</span></span>
  * <span data-ttu-id="993dd-175">每個訊息遙測追蹤每個推送您的初始要求呼叫 tooour 服務成功批次處理 hello 推播通知。</span><span class="sxs-lookup"><span data-stu-id="993dd-175">Per Message Telemetry tracks each push from your initial request call tooour service successfully batching hello pushes out.</span></span>
  * <span data-ttu-id="993dd-176">平台通知系統意見反應通訊平台通知系統 tooassist 偵錯中的所有意見。</span><span class="sxs-lookup"><span data-stu-id="993dd-176">Platform Notification System Feedback communicates all feedback from Platfom Notification Systems tooassist in debugging.</span></span>
* <span data-ttu-id="993dd-177">**延展性**</span><span class="sxs-lookup"><span data-stu-id="993dd-177">**Scalability**</span></span> 
  
  * <span data-ttu-id="993dd-178">傳送快速訊息 toomillions 個裝置，不重新架構或裝置的分區化。</span><span class="sxs-lookup"><span data-stu-id="993dd-178">Send fast messages toomillions of devices without re-architecting or device sharding.</span></span>
* <span data-ttu-id="993dd-179">**安全性**</span><span class="sxs-lookup"><span data-stu-id="993dd-179">**Security**</span></span>

  * <span data-ttu-id="993dd-180">共用存取密碼 (SAS) 或同盟驗證。</span><span class="sxs-lookup"><span data-stu-id="993dd-180">Shared Access Secret (SAS) or federated authentication.</span></span>

## <a name="integration-with-app-service-mobile-apps"></a><span data-ttu-id="993dd-181">與 App Service Mobile Apps 整合</span><span class="sxs-lookup"><span data-stu-id="993dd-181">Integration with App Service Mobile Apps</span></span>
<span data-ttu-id="993dd-182">toofacilitate 順暢且統一的體驗，Azure 服務間[App Service Mobile App]具有內建支援，使用通知中樞推播通知。</span><span class="sxs-lookup"><span data-stu-id="993dd-182">toofacilitate a seamless and unifying experience across Azure services, [App Service Mobile Apps] has built-in support for push notifications using Notification Hubs.</span></span> <span data-ttu-id="993dd-183">[App Service Mobile App]企業開發人員和系統整合者可將一組豐富的功能帶 toomobile 開發人員提供可高度擴充、 全域可用的行動應用程式開發平台。</span><span class="sxs-lookup"><span data-stu-id="993dd-183">[App Service Mobile Apps] offers a highly scalable, globally available mobile application development platform for Enterprise Developers and System Integrators that brings a rich set of capabilities toomobile developers.</span></span>

<span data-ttu-id="993dd-184">行動應用程式開發人員可以利用通知中樞，以下列工作流程的 hello:</span><span class="sxs-lookup"><span data-stu-id="993dd-184">Mobile Apps developers can utilize Notification Hubs with hello following workflow:</span></span>

1. <span data-ttu-id="993dd-185">擷取裝置 PNS 控制代碼</span><span class="sxs-lookup"><span data-stu-id="993dd-185">Retrieve device PNS handle</span></span>
2. <span data-ttu-id="993dd-186">透過便利的 Mobile Apps Client SDK 註冊 API，使用通知中樞註冊裝置</span><span class="sxs-lookup"><span data-stu-id="993dd-186">Register device with Notification Hubs through convenient Mobile Apps Client SDK register API</span></span>
   * <span data-ttu-id="993dd-187">請注意，Mobile Apps 會基於安全性考量，去除註冊上的所有標籤。</span><span class="sxs-lookup"><span data-stu-id="993dd-187">Note that Mobile Apps strips away all tags on registrations for security purposes.</span></span> <span data-ttu-id="993dd-188">搭配通知中樞從您的後端直接 tooassociate 標記與裝置。</span><span class="sxs-lookup"><span data-stu-id="993dd-188">Work with Notification Hubs from your backend directly tooassociate tags with devices.</span></span>
3. <span data-ttu-id="993dd-189">從 App 後端使用通知中樞傳送通知</span><span class="sxs-lookup"><span data-stu-id="993dd-189">Send notifications from your app backend with Notification Hubs</span></span>

<span data-ttu-id="993dd-190">以下是一些便利，回到 toodevelopers 與這項整合：</span><span class="sxs-lookup"><span data-stu-id="993dd-190">Here are some conveniences brought toodevelopers with this integration:</span></span>

* <span data-ttu-id="993dd-191">**行動應用程式的用戶端 Sdk**： 這些多平台 Sdk 提供註冊的簡單應用程式開發介面和溝通 toohello 通知中樞與 hello 行動裝置應用程式會自動連結。</span><span class="sxs-lookup"><span data-stu-id="993dd-191">**Mobile Apps Client SDKs**: These multi-platform SDKs provide simple APIs for registration and talk toohello notification hub linked up with hello mobile app automatically.</span></span> <span data-ttu-id="993dd-192">開發人員不需要透過通知中樞認證 toodig 作業，並與其他服務搭配使用。</span><span class="sxs-lookup"><span data-stu-id="993dd-192">Developers do not need toodig through Notification Hubs credentials and work with an additional service.</span></span>

  * <span data-ttu-id="993dd-193">*推播 toouser*: hello Sdk 自動標記 hello 給定裝置進行行動應用程式已驗證使用者識別碼 tooenable 發送 toouser 的案例。</span><span class="sxs-lookup"><span data-stu-id="993dd-193">*Push toouser*: hello SDKs automatically tag hello given device with Mobile Apps authenticated User ID tooenable push toouser scenario.</span></span>
  * <span data-ttu-id="993dd-194">*推播 toodevice*: hello Sdk 自動使用與通知中樞，節省開發人員維護多個服務 Guid hello 麻煩 GUID tooregister hello 行動應用程式的安裝識別碼。</span><span class="sxs-lookup"><span data-stu-id="993dd-194">*Push toodevice*: hello SDKs automatically use hello Mobile Apps Installation ID as GUID tooregister with Notification Hubs, saving developers hello trouble of maintaining multiple service GUIDs.</span></span>
* <span data-ttu-id="993dd-195">**安裝模型**： 搭配通知中樞的最新推入模型 toorepresent 所有推入內容中的推播通知服務與對齊且容易 toouse JSON 安裝的裝置相關聯的行動應用程式。</span><span class="sxs-lookup"><span data-stu-id="993dd-195">**Installation model**: Mobile Apps works with Notification Hubs' latest push model toorepresent all push properties associated with a device in a JSON Installation that aligns with Push Notification Services and is easy toouse.</span></span>
* <span data-ttu-id="993dd-196">**彈性**： 開發人員可以隨時甚至與 hello 整合通知中心直接與 toowork 備妥。</span><span class="sxs-lookup"><span data-stu-id="993dd-196">**Flexibility**: Developers can always choose toowork with Notification Hubs directly even with hello integration in place.</span></span>
* <span data-ttu-id="993dd-197">**整合式體驗中的[Azure 入口網站]**： 推播一項功能會在行動裝置應用程式中以視覺化方式表示以及開發人員可以輕鬆地與行動應用程式透過 hello 關聯的通知中樞。</span><span class="sxs-lookup"><span data-stu-id="993dd-197">**Integrated experience in [Azure portal]**: Push as a capability is represented visually in Mobile Apps and developers can easily work with hello associated notification hub through Mobile Apps.</span></span>

## <a name="next-steps"></a><span data-ttu-id="993dd-198">後續步驟</span><span class="sxs-lookup"><span data-stu-id="993dd-198">Next Steps</span></span>
<span data-ttu-id="993dd-199">您可以在以下主題找到「通知中樞」的詳細資訊：</span><span class="sxs-lookup"><span data-stu-id="993dd-199">You can find out more about Notification Hubs in these topics:</span></span>

* <span data-ttu-id="993dd-200">**[客戶如何使用通知中樞]**</span><span class="sxs-lookup"><span data-stu-id="993dd-200">**[How customers are using Notification Hubs]**</span></span>
* <span data-ttu-id="993dd-201">**[通知中樞教學課程和指南]**</span><span class="sxs-lookup"><span data-stu-id="993dd-201">**[Notification Hubs tutorials and guides]**</span></span>
* <span data-ttu-id="993dd-202">**通知中樞快速入門教學課程**：[iOS]、[Android]、[Windows Universal]、[Windows Phone]、[Kindle]、[Xamarin.iOS]、[Xamarin.Android]</span><span class="sxs-lookup"><span data-stu-id="993dd-202">**Notification Hubs Getting Started tutorials**: [iOS], [Android], [Windows Universal], [Windows Phone], [Kindle], [Xamarin.iOS], [Xamarin.Android]</span></span>

[0]: ./media/notification-hubs-overview/registration-diagram.png
[1]: ./media/notification-hubs-overview/notification-hub-diagram.png
[客戶如何使用通知中樞]: http://azure.microsoft.com/services/notification-hubs
[通知中樞教學課程和指南]: http://azure.microsoft.com/documentation/services/notification-hubs
[iOS]: http://azure.microsoft.com/documentation/articles/notification-hubs-ios-get-started
[Android]: http://azure.microsoft.com/documentation/articles/notification-hubs-android-get-started
[Windows Universal]: http://azure.microsoft.com/documentation/articles/notification-hubs-windows-store-dotnet-get-started
[Windows Phone]: http://azure.microsoft.com/documentation/articles/notification-hubs-windows-phone-get-started
[Kindle]: http://azure.microsoft.com/documentation/articles/notification-hubs-kindle-get-started
[Xamarin.iOS]: http://azure.microsoft.com/documentation/articles/partner-xamarin-notification-hubs-ios-get-started
[Xamarin.Android]: http://azure.microsoft.com/documentation/articles/partner-xamarin-notification-hubs-android-get-started
[Microsoft.WindowsAzure.Messaging.NotificationHub]: http://msdn.microsoft.com/library/microsoft.windowsazure.messaging.notificationhub.aspx
[Microsoft.ServiceBus.Notifications]: http://msdn.microsoft.com/library/microsoft.servicebus.notifications.aspx
[App Service Mobile App]: https://azure.microsoft.com/en-us/documentation/articles/app-service-mobile-value-prop/
[templates]: notification-hubs-templates-cross-platform-push-messages.md
[Azure 入口網站]: https://portal.azure.com
[tags]: (http://msdn.microsoft.com/library/azure/dn530749.aspx)
