---
title: "Azure 通知中樞 - 診斷指導方針"
description: "有關如何診斷 Azure 通知中樞常見問題的指導方針。"
services: notification-hubs
documentationcenter: Mobile
author: ysxu
manager: erikre
editor: 
ms.assetid: b5c89a2a-63b8-46d2-bbed-924f5a4cce61
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: NA
ms.devlang: multiple
ms.topic: article
ms.date: 10/03/2016
ms.author: yuaxu
ms.openlocfilehash: 32e3a2e6f840afd865375a622cfae0d33ba65090
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="azure-notification-hubs---diagnosis-guidelines"></a><span data-ttu-id="9146c-103">Azure 通知中樞 - 診斷指導方針</span><span class="sxs-lookup"><span data-stu-id="9146c-103">Azure Notification Hubs - Diagnosis guidelines</span></span>
## <a name="overview"></a><span data-ttu-id="9146c-104">Overview</span><span class="sxs-lookup"><span data-stu-id="9146c-104">Overview</span></span>
<span data-ttu-id="9146c-105">最常從 Azure 通知中樞客戶口中聽到的其中一個問題是，如何得知從應用程式後端傳送的通知為什麼無法顯示於用戶端裝置上；這些通知在何處遭到捨棄，為什麼會遭到捨棄，該如何修正？</span><span class="sxs-lookup"><span data-stu-id="9146c-105">One of the most common questions we hear from Azure Notification Hubs customers is how to figure out why they don’t see a notification sent from their application backend appear on the client device - where and why notifications were dropped and how to fix this.</span></span> <span data-ttu-id="9146c-106">在本文章中，我們將探討通知遭到捨棄及未抵達裝置的各種原因。</span><span class="sxs-lookup"><span data-stu-id="9146c-106">In this article we will go through the various reasons why notifications may get dropped or do not end up on the devices.</span></span> <span data-ttu-id="9146c-107">我們也會探討用來分析及找出根本原因的方法。</span><span class="sxs-lookup"><span data-stu-id="9146c-107">We will also look through ways in which you can analyze and figure out the root cause.</span></span> 

<span data-ttu-id="9146c-108">首先，請務必了解 Azure 通知中樞如何將通知推送到裝置。</span><span class="sxs-lookup"><span data-stu-id="9146c-108">First of all, it is critical to understand how Azure Notification Hubs pushes out notifications to the devices.</span></span>
![][0]

<span data-ttu-id="9146c-109">在典型的傳送通知流程中，系統會從**應用程式後端**將訊息傳送到 **Azure 通知中樞 (NH)**。接著，Azure 通知中樞會處理所有涉及已設定之標記和標記運算式的註冊來判斷「目標」(亦即所有需要接收推播通知的註冊)。</span><span class="sxs-lookup"><span data-stu-id="9146c-109">In a typical send notification flow, the message is sent from the **application backend** to **Azure Notification Hub (NH)** which in turn does some processing on all the registrations taking into account the configured tags & tag expressions to determine "targets" i.e. all the registrations that need to receive the push notification.</span></span> <span data-ttu-id="9146c-110">這些註冊可以跨越任何或所有我們支援的平台，包括 iOS、Google、Windows、Windows Phone、Kindle 及用於中國 Android 的百度。</span><span class="sxs-lookup"><span data-stu-id="9146c-110">These registrations can span across any or all of our supported platforms - iOS, Google, Windows, Windows Phone, Kindle and Baidu for China Android.</span></span> <span data-ttu-id="9146c-111">建立目標後，NH 會將通知分配到多個註冊批次，然後再推送到裝置平台特有的**推播通知服務 (PNS)** (如 Apple 的 APNS、Google 的 GCM 等)。NH 會根據您在 [設定通知中樞] 頁面的 Azure 傳統入口網站中設定的認證來驗證個別 PNS。</span><span class="sxs-lookup"><span data-stu-id="9146c-111">Once the targets are established, NH then pushes out notifications, split across multiple batch of registrations, to the device platform specific **Push Notification Service (PNS)** - e.g. APNS for Apple, GCM for Google etc. NH authenticates with the respective PNS based on the credentials you set in the Azure Classic Portal on the Configure Notification Hub page.</span></span> <span data-ttu-id="9146c-112">隨後，PNS 會將通知轉送到各個**用戶端裝置**。</span><span class="sxs-lookup"><span data-stu-id="9146c-112">The PNS then forwards the notifications to the respective **client devices**.</span></span> <span data-ttu-id="9146c-113">以上是平台建議的推送通知傳遞方法。請注意，通知傳遞最終的旅程發生在平台 PNS 和裝置之間。</span><span class="sxs-lookup"><span data-stu-id="9146c-113">This is the platform recommended way to deliver push notifications and note that the final leg of notification delivery takes place between the platform PNS and the device.</span></span> <span data-ttu-id="9146c-114">因此我們有四個主要元件 - *用戶端*、*應用程式後端*、*Azure 通知中樞 (NH)* 和*推播通知服務 (PNS)*，而且其中任何一項可能會導致通知遭到捨棄。</span><span class="sxs-lookup"><span data-stu-id="9146c-114">Therefore we have four major components - *client*, *application backend*, *Azure Notification Hubs (NH)* and *Push Notification Services (PNS)* and any of these may cause notifications getting dropped.</span></span> <span data-ttu-id="9146c-115">如需此架構的詳細資料，請參閱[通知中樞概觀]。</span><span class="sxs-lookup"><span data-stu-id="9146c-115">More details on this architecture is available on [Notification Hubs Overview].</span></span>

<span data-ttu-id="9146c-116">通知傳遞失敗可能會發生在初始測試/執行階段，其可能代表組態問題；也有可能發生在所有或部分通知遭到捨棄的生產環境中，其代表較深層的應用程式或訊息模式問題。</span><span class="sxs-lookup"><span data-stu-id="9146c-116">Failure to deliver notifications may happen during the initial test/staging phase which may indicate a configuration issue or it may happen in production where either all or some of the notifications may be getting dropped indicating some deeper application or messaging pattern issue.</span></span> <span data-ttu-id="9146c-117">在本節的後續內容中，我們會探討各種通知捨棄案例 (常見和罕見)，有些案例是顯而易見的，有些案例則不太明顯。</span><span class="sxs-lookup"><span data-stu-id="9146c-117">In the section, below we will look at various dropped notifications scenarios ranging from common to the rarer kind, some of which you may find obvious and some others not so much.</span></span> 

## <a name="azure-notifications-hub-mis-configuration"></a><span data-ttu-id="9146c-118">Azure 通知中樞組態錯誤</span><span class="sxs-lookup"><span data-stu-id="9146c-118">Azure Notifications Hub mis-configuration</span></span>
<span data-ttu-id="9146c-119">Azure 通知中樞需要在開發人員應用程式的內容中自行驗證，才能成功地將通知傳送到各個 PNS。</span><span class="sxs-lookup"><span data-stu-id="9146c-119">Azure Notification Hubs needs to authenticate itself in the context of the developer's application to be able to successfully send notifications to the respective PNS.</span></span> <span data-ttu-id="9146c-120">若要讓 Azure 通知中樞自行驗證，開發人員需要向各平台 (Google、Apple、Windows 等) 建立開發人員帳戶，然後在取得認證 (需要在入口網站的 [通知中樞組態] 區段中設定) 之處註冊應用程式。</span><span class="sxs-lookup"><span data-stu-id="9146c-120">This is made possible by the developer creating a developer account with the respective platform (Google, Apple, Windows etc) and then registering their application where they get credentials which need to be configured in the portal under Notification Hubs configuration section.</span></span> <span data-ttu-id="9146c-121">如果通知無法送出，第一個步驟應是確認於通知中樞內設定的認證是否正確，與在平台專屬開發人員帳戶下由應用程式建立的認證相符。</span><span class="sxs-lookup"><span data-stu-id="9146c-121">If no notifications are making through, first step should be to ensure that the correct credentials are configured in the Notification Hub matching them with the application created under their platform specific developer account.</span></span> <span data-ttu-id="9146c-122">[使用者入門教學課程] 的逐步教學法將有助於您檢驗此程序。</span><span class="sxs-lookup"><span data-stu-id="9146c-122">You will find our [Getting Started Tutorials] useful to go over this process in a step by step manner.</span></span> <span data-ttu-id="9146c-123">以下是一些常見的組態錯誤：</span><span class="sxs-lookup"><span data-stu-id="9146c-123">Here are some common mis-configurations:</span></span>

1. <span data-ttu-id="9146c-124">**一般**</span><span class="sxs-lookup"><span data-stu-id="9146c-124">**General**</span></span>
   
    <span data-ttu-id="9146c-125">a) 確認通知中樞名稱與以下各項相同 (無錯別字)：</span><span class="sxs-lookup"><span data-stu-id="9146c-125">a) Make sure that your notification hub name (without typos) is the same:</span></span>
   
   * <span data-ttu-id="9146c-126">從用戶端註冊之處</span><span class="sxs-lookup"><span data-stu-id="9146c-126">Where you are registering from the client,</span></span> 
   * <span data-ttu-id="9146c-127">從後端傳送通知之處</span><span class="sxs-lookup"><span data-stu-id="9146c-127">Where you are sending notifications from the backend,</span></span>  
   * <span data-ttu-id="9146c-128">設定 PNS 認證之處</span><span class="sxs-lookup"><span data-stu-id="9146c-128">Where you have configured the PNS credentials and</span></span> 
   * <span data-ttu-id="9146c-129">在用戶端和後端上設定 SAS 認證的通知中樞。</span><span class="sxs-lookup"><span data-stu-id="9146c-129">Whose SAS credentials you have configured on the client and the backend.</span></span> 
     
     <span data-ttu-id="9146c-130">b) 確認在用戶端和應用程式後端上使用正確的 SAS 組態字串。</span><span class="sxs-lookup"><span data-stu-id="9146c-130">b) Make sure that you are using the correct SAS configuration strings on the client and the application backend.</span></span> <span data-ttu-id="9146c-131">根據經驗法則，您必須在用戶端上使用 **DefaultListenSharedAccessSignature**，在應用程式後端上使用 **DefaultFullSharedAccessSignature** (賦予將通知傳送到 NH 的權限)。</span><span class="sxs-lookup"><span data-stu-id="9146c-131">As a rule of thumb, you must be using the **DefaultListenSharedAccessSignature** on the client and **DefaultFullSharedAccessSignature** on the application backend (which gives permission to be able to send notification to the NH)</span></span>
2. <span data-ttu-id="9146c-132">**Apple Push Notification Service (APNS) 組態**</span><span class="sxs-lookup"><span data-stu-id="9146c-132">**Apple Push Notification Service (APNS) configuration**</span></span>
   
    <span data-ttu-id="9146c-133">您必須維護兩個不同的中樞，一個供生產環境之用，另一個供測試之用。</span><span class="sxs-lookup"><span data-stu-id="9146c-133">You must maintain two different hubs - one for production and another for testing purpose.</span></span> <span data-ttu-id="9146c-134">這表示您需要將於沙箱環境中使用的憑證上載到某一個中樞，再將於生產環境中使用的憑證上載到另一個中樞。</span><span class="sxs-lookup"><span data-stu-id="9146c-134">This means uploading the certificate you are going to use in sandbox environment to a separate hub and the certificate you are going to use in production to a separate hub.</span></span> <span data-ttu-id="9146c-135">請勿嘗試將不同類型的憑證上載到同一個中樞，因為這樣會導致通知徹底失敗。</span><span class="sxs-lookup"><span data-stu-id="9146c-135">Do not try to upload different types of certificates to the same hub as it may cause notification failures down the line.</span></span> <span data-ttu-id="9146c-136">如果您發現自己意外地將不同類型的憑證上載到同一個中樞，建議您刪除中樞，重新開始。</span><span class="sxs-lookup"><span data-stu-id="9146c-136">If you do find yourself in a position where you have inadvertently uploaded different types of certificate to the same hub, it is recommended to delete the hub and start fresh.</span></span> <span data-ttu-id="9146c-137">如果您基於某些原因無法刪除中樞，至少必須刪除中樞內所有現有註冊。</span><span class="sxs-lookup"><span data-stu-id="9146c-137">If for some reason, you are not able to delete the hub then at the very least, you must delete all the existing registrations from the hub.</span></span> 
3. <span data-ttu-id="9146c-138">**Google 雲端通訊 (GCM) 組態**</span><span class="sxs-lookup"><span data-stu-id="9146c-138">**Google Cloud Messaging (GCM) configuration**</span></span> 
   
    <span data-ttu-id="9146c-139">a) 確認您在雲端專案下啟用的是 "Google Cloud Messaging for Android"。</span><span class="sxs-lookup"><span data-stu-id="9146c-139">a) Make sure that you are enabling "Google Cloud Messaging for Android" under your cloud project.</span></span> 
   
    ![][2]
   
    <span data-ttu-id="9146c-140">b) 確認您正在建立「伺服器金鑰」，同時取得 NH 用來驗證 GCM 的認證。</span><span class="sxs-lookup"><span data-stu-id="9146c-140">b) Make sure that you create a "Server Key" while obtaining the credentials which NH will use to authenticate with GCM.</span></span> 
   
    ![][3]
   
    <span data-ttu-id="9146c-141">c) 確認您已在用戶端上設定「專案 ID」，其為可從儀表板取得的全數值實體。</span><span class="sxs-lookup"><span data-stu-id="9146c-141">c) Make sure that you have configured "Project ID" on the client which is an entirely numerical entity that you can obtain from the dashboard:</span></span>
   
    ![][1]

## <a name="application-issues"></a><span data-ttu-id="9146c-142">應用程式問題</span><span class="sxs-lookup"><span data-stu-id="9146c-142">Application issues</span></span>
1) <span data-ttu-id="9146c-143">**標記/ 標記運算式**</span><span class="sxs-lookup"><span data-stu-id="9146c-143">**Tags/ Tag expressions**</span></span>

<span data-ttu-id="9146c-144">如果您使用標記或標記運算式來區分對象，在傳送通知時，可能經常會找不到在傳送呼叫中指定之標記/標記運算式所代表的目標。</span><span class="sxs-lookup"><span data-stu-id="9146c-144">If you are using tags or tag expressions to segment your audience, it is always possible that when you are sending the notification, there is no target being found based on the tags/tag expressions you are specifying in your send call.</span></span> <span data-ttu-id="9146c-145">在傳送通知時，建議您最好檢閱註冊以確認標記相符，並且驗證通知回條僅來自具有這些註冊的用戶端。</span><span class="sxs-lookup"><span data-stu-id="9146c-145">It is best to review your registrations to ensure that there are tags which match when you send notification and then verify the notification receipt only from the clients with those registrations.</span></span> <span data-ttu-id="9146c-146">例如</span><span class="sxs-lookup"><span data-stu-id="9146c-146">E.g.</span></span> <span data-ttu-id="9146c-147">假設與 NH 相關的註冊均有 "Politics" 標記，如果您傳送具有 "Sports" 標記的通知，系統不會將該通知傳送到任何裝置。</span><span class="sxs-lookup"><span data-stu-id="9146c-147">if all your registrations with NH were done with say tag "Politics" and you are sending a notification with tag "Sports", it will not be sent to any device.</span></span> <span data-ttu-id="9146c-148">複雜的案例可能涉及只註冊 "Tag A" OR "Tag B" 的標記運算式，然而在傳送通知時，您設定的目標為 "Tag A && Tag B"。</span><span class="sxs-lookup"><span data-stu-id="9146c-148">A complex case could involve tag expressions where you only registered with "Tag A" OR "Tag B" but while sending notifications, you are targeting "Tag A && Tag B".</span></span> <span data-ttu-id="9146c-149">以下自我診斷秘訣小節提供檢閱註冊和註冊之標記的方法。</span><span class="sxs-lookup"><span data-stu-id="9146c-149">In the self-diagnose tips section below, there are ways in which you can review your registrations along with the tags they have.</span></span> 

2) <span data-ttu-id="9146c-150">**範本問題**</span><span class="sxs-lookup"><span data-stu-id="9146c-150">**Template issues**</span></span>

<span data-ttu-id="9146c-151">如果您使用範本，請務必遵守 [範本指引]所述的指導方針。</span><span class="sxs-lookup"><span data-stu-id="9146c-151">If you are using templates then ensure that you are following the guidelines described at [Template guidance].</span></span> 

3) <span data-ttu-id="9146c-152">**無效的註冊**</span><span class="sxs-lookup"><span data-stu-id="9146c-152">**Invalid registrations**</span></span>

<span data-ttu-id="9146c-153">假設通知傳送的適當目標搜尋起因於通知中樞設定正確且所有標記/標記運算式的用法正確，NH 會以平行方式引發數個處理批次，每個批次都會傳送訊息給一組註冊。</span><span class="sxs-lookup"><span data-stu-id="9146c-153">Assuming the Notification Hub was configured correctly and any tags/tag expressions were used correctly resulting in the find of valid targets to which the notifications need to be sent, NH fires off several processing batches in parallel - each batch sending messages to a set of registrations.</span></span> 

> [!NOTE]
> <span data-ttu-id="9146c-154">由於處理採平行方式進行，因此我們無法保證通知的傳遞順序。</span><span class="sxs-lookup"><span data-stu-id="9146c-154">Since we do the processing in parallel, we don’t guarantee the order in which the notifications will be delivered.</span></span> 
> 
> 

<span data-ttu-id="9146c-155">現在我們已根據「最多一次」訊息傳遞模式將 Azure 通知中樞最佳化。</span><span class="sxs-lookup"><span data-stu-id="9146c-155">Now Azure Notifications Hub is optimized for an "at-most once" message delivery model.</span></span> <span data-ttu-id="9146c-156">這表示我們會嘗試刪除重複的項目，避免系統將通知多次傳遞給同一部裝置。</span><span class="sxs-lookup"><span data-stu-id="9146c-156">This means that we attempt a de-duplication so that no notifications are delivered more than once to a device.</span></span> <span data-ttu-id="9146c-157">為了確保功效，我們會先檢驗註冊並確認系統只會將一則訊息傳送給一個裝置識別項，然後再實際將訊息傳送給 PNS。</span><span class="sxs-lookup"><span data-stu-id="9146c-157">To ensure this we look through the registrations and make sure that only one message is sent per device identifier before actually sending the message to the PNS.</span></span> <span data-ttu-id="9146c-158">隨著系統將各個批次傳送到 PNS，PSN 會接受及驗證註冊。它可能會在批次的一或多個註冊中偵測到錯誤，再將錯誤傳回 Azure NH 並停止處理，全然捨棄該批次。</span><span class="sxs-lookup"><span data-stu-id="9146c-158">As each batch is sent to the PNS, which in turn is accepting and validating the registrations, it is possible that the PNS detects an error with one or more of the registrations in a batch, returns an error to Azure NH and stops processing thereby dropping that batch completely.</span></span> <span data-ttu-id="9146c-159">對於使用 TCP 串流通訊協定的 APNS 來說，這種情況尤其顯著。</span><span class="sxs-lookup"><span data-stu-id="9146c-159">This is especially true with APNS which uses a TCP stream protocol.</span></span> <span data-ttu-id="9146c-160">雖然我們已針對最多一次傳遞模式最佳化，而在此案例中我們在資料庫內移除了故障的註冊項目，接著在該批次中針對剩餘的裝置重新嘗試通知傳遞。</span><span class="sxs-lookup"><span data-stu-id="9146c-160">Although we are optimized for at-most once delivery, in this case we remove the faulting registration from our database and then retry notification delivery for the rest of the devices in that batch.</span></span>

<span data-ttu-id="9146c-161">針對錯誤傳遞嘗試，您可以依照使用 Azure 通知中樞 REST API 的註冊來取得錯誤資訊：[每個訊息遙測︰取得通知訊息遙測](https://msdn.microsoft.com/library/azure/mt608135.aspx)以及 [PNS 回應](https://msdn.microsoft.com/library/azure/mt705560.aspx)。</span><span class="sxs-lookup"><span data-stu-id="9146c-161">You can get error information for the failed delivery attempt against a registration using the Azure Notification Hubs REST APIs: [Per Message Telemetry: Get Notification Message Telemetry](https://msdn.microsoft.com/library/azure/mt608135.aspx) and [PNS Feedback](https://msdn.microsoft.com/library/azure/mt705560.aspx).</span></span> <span data-ttu-id="9146c-162">請參閱 [SendRESTExample](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/SendRestExample) 以取得範例程式碼。</span><span class="sxs-lookup"><span data-stu-id="9146c-162">See the [SendRESTExample](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/SendRestExample) for example code.</span></span>

## <a name="pns-issues"></a><span data-ttu-id="9146c-163">PNS 問題</span><span class="sxs-lookup"><span data-stu-id="9146c-163">PNS issues</span></span>
<span data-ttu-id="9146c-164">待各個 PNS 接收到通知訊息後，它們必須負責將通知傳遞給裝置。</span><span class="sxs-lookup"><span data-stu-id="9146c-164">Once the notification message has been received by the respective PNS then it is its responsibility to deliver the notification to the device.</span></span> <span data-ttu-id="9146c-165">Azure 通知中樞與 PNS 的運作並不相關，也無法控制它們將通知傳遞給裝置的時間和成功與否。</span><span class="sxs-lookup"><span data-stu-id="9146c-165">Azure Notification Hubs is out of the picture here and has no control on when or if the notification is going to be delivered to the device.</span></span> <span data-ttu-id="9146c-166">由於平台通知服務已臻完備，因此通知經常能在幾秒鐘之內從 PNS 抵達裝置。</span><span class="sxs-lookup"><span data-stu-id="9146c-166">Since the platform notification services are pretty robust, notifications do tend to reach the devices in a few seconds from the PNS.</span></span> <span data-ttu-id="9146c-167">然而，如果 PNS 處於節流狀態，Azure 通知中樞會套用指數退回策略；如果 PNS 持續在 30 分鐘之內無法聯繫，我們將採取既定的原則讓這些訊息到期並永久捨棄。</span><span class="sxs-lookup"><span data-stu-id="9146c-167">If the PNS however is throttling then Azure Notification Hubs does apply an exponential back off strategy and if the PNS remains unreachable for 30 min then we have a policy in place to expire and drop those messages permanently.</span></span> 

<span data-ttu-id="9146c-168">如果 PNS 嘗試傳遞通知但裝置已離線，PNS 會在一段有限的時間內儲存通知，並在可聯繫裝置時再行傳遞。</span><span class="sxs-lookup"><span data-stu-id="9146c-168">If a PNS attempts to deliver a notification but the device is offline, the notification is stored by the PNS for a limited period of time, and delivered to the device when it becomes available.</span></span> <span data-ttu-id="9146c-169">PNS 只會針對每個應用程式儲存一則最近的通知。</span><span class="sxs-lookup"><span data-stu-id="9146c-169">Only one recent notification for a particular app is stored.</span></span> <span data-ttu-id="9146c-170">如果在裝置離線時傳送多則通知，每則新通知都會導致前一則通知遭到捨棄。</span><span class="sxs-lookup"><span data-stu-id="9146c-170">If multiple notifications are sent while the device is offline, each new notification causes the prior notification to be discarded.</span></span> <span data-ttu-id="9146c-171">這個只保留最新通知的行為在 APNS 中稱為聯合通知，在 GCM 中稱為摺疊 (使用摺疊索引鍵之故)。</span><span class="sxs-lookup"><span data-stu-id="9146c-171">This behavior of keeping only the newest notification is referred to as coalescing notifications in APNS and collapsing in GCM (which uses a collapsing key).</span></span> <span data-ttu-id="9146c-172">如果裝置長期處於離線狀態，針對該裝置儲存的所有通知都將遭到捨棄。</span><span class="sxs-lookup"><span data-stu-id="9146c-172">If the device remains offline for a long time, any notifications that were being stored for it are discarded.</span></span> <span data-ttu-id="9146c-173">資料來源 - [APNS 指引] & [GCM 指引]</span><span class="sxs-lookup"><span data-stu-id="9146c-173">Source - [APNS guidance] & [GCM guidance]</span></span>

<span data-ttu-id="9146c-174">有了 Azure 通知中樞，您可以使用泛型 `SendNotification` API (如適用於 .NET SDK 的 – `SendNotificationAsync`) 透過 HTTP 標頭傳送聯合索引鍵，該 API 也會採用以原狀傳送到各 PNS 的 HTTP 標頭。</span><span class="sxs-lookup"><span data-stu-id="9146c-174">With Azure Notification Hubs - you can pass a coalescing key via an HTTP header using the generic `SendNotification` API (e.g. for .NET SDK – `SendNotificationAsync`) which also takes HTTP headers which are passed as is to the respective PNS.</span></span> 

## <a name="self-diagnose-tips"></a><span data-ttu-id="9146c-175">自我診斷秘訣</span><span class="sxs-lookup"><span data-stu-id="9146c-175">Self-diagnose tips</span></span>
<span data-ttu-id="9146c-176">在以下內容中，我們將檢視各種診斷及找出通知中樞問題之根本原因的途徑：</span><span class="sxs-lookup"><span data-stu-id="9146c-176">Here we will examine the various avenues to diagnose and root cause any Notification Hub issues:</span></span>

### <a name="verify-credentials"></a><span data-ttu-id="9146c-177">驗證認證</span><span class="sxs-lookup"><span data-stu-id="9146c-177">Verify credentials</span></span>
1. <span data-ttu-id="9146c-178">**PNS 開發人員入口網站**</span><span class="sxs-lookup"><span data-stu-id="9146c-178">**PNS developer portal**</span></span>
   
    <span data-ttu-id="9146c-179">使用我們的 [使用者入門教學課程]於各個 PNS 開發人員入口網站 (APNS、GCM、WNS 等) 驗證認證。</span><span class="sxs-lookup"><span data-stu-id="9146c-179">Verify them at the respective PNS developer portal (APNS, GCM, WNS etc) using our [Getting Started Tutorials].</span></span>
2. <span data-ttu-id="9146c-180">**Azure 傳統入口網站**</span><span class="sxs-lookup"><span data-stu-id="9146c-180">**Azure Classic portal**</span></span>
   
    <span data-ttu-id="9146c-181">移至 [設定] 索引標籤以檢閱認證，以及與從 PNS 開發人員入口網站取得的認證比對。</span><span class="sxs-lookup"><span data-stu-id="9146c-181">Go to the Configure tab to review and match the credentials with those obtained from the PNS developer portal.</span></span> 
   
    ![][4]

### <a name="verify-registrations"></a><span data-ttu-id="9146c-182">驗證註冊</span><span class="sxs-lookup"><span data-stu-id="9146c-182">Verify registrations</span></span>
1. <span data-ttu-id="9146c-183">**Visual Studio**</span><span class="sxs-lookup"><span data-stu-id="9146c-183">**Visual Studio**</span></span>
   
    <span data-ttu-id="9146c-184">如果您使用 Visual Studio 來從事開發，可以連接 Microsoft Azure 來檢視及管理多種 Azure 服務，包括從伺服器總管檢視及管理通知中樞。</span><span class="sxs-lookup"><span data-stu-id="9146c-184">If you use Visual Studio for development then you can connect to Microsoft Azure and view and manage a bunch of Azure services including Notifications Hub from "Server Explorer".</span></span> <span data-ttu-id="9146c-185">這能為您的開發/測試環境帶來許多助益。</span><span class="sxs-lookup"><span data-stu-id="9146c-185">This is primarily useful for your dev/test environment.</span></span> 
   
    ![][9]
   
    <span data-ttu-id="9146c-186">您可檢視及管理中樞內已按照平台歸類的註冊、原生或範本註冊、任何標記、PNS 識別項、註冊 ID 及到期日。</span><span class="sxs-lookup"><span data-stu-id="9146c-186">You can view and manage all the registrations in your hub which are nicely categorized for platform, native or template registration, any tags, PNS identifier, registration id and the expiration date.</span></span> <span data-ttu-id="9146c-187">您也可以隨時編輯註冊；如果您想要編輯任何標記，這項功能便能派上用場。</span><span class="sxs-lookup"><span data-stu-id="9146c-187">You can also edit a registration on the fly - which is useful say if you want to edit any tags.</span></span> 
   
    ![][8]
   
   > [!NOTE]
   > <span data-ttu-id="9146c-188">Visual Studio 的編輯註冊功能僅應用於註冊數量有限的開發/測試期間。</span><span class="sxs-lookup"><span data-stu-id="9146c-188">Visual Studio functionality to edit registrations should only be used during dev/test with limited number of registrations.</span></span> <span data-ttu-id="9146c-189">如果您需要修正大量註冊，請考慮使用 [匯出/匯入註冊](https://msdn.microsoft.com/library/dn790624.aspx)</span><span class="sxs-lookup"><span data-stu-id="9146c-189">If there arises a need to fix your registrations in bulk, consider using the Export/Import registration functionality described here - [Export/Import Registrations](https://msdn.microsoft.com/library/dn790624.aspx)</span></span>
   > 
   > 
2. <span data-ttu-id="9146c-190">**服務匯流排總管**</span><span class="sxs-lookup"><span data-stu-id="9146c-190">**Service Bus explorer**</span></span>
   
    <span data-ttu-id="9146c-191">有許多客戶使用 [服務匯流排總管] 所述的服務匯流排總管來檢視及管理通知中樞。</span><span class="sxs-lookup"><span data-stu-id="9146c-191">Many customers use ServiceBus explorer described here - [ServiceBus Explorer] for viewing and managing their notification hub.</span></span> <span data-ttu-id="9146c-192">其為可從 code.microsoft.com - [服務匯流排總管程式碼]</span><span class="sxs-lookup"><span data-stu-id="9146c-192">It is an open source project available from code.microsoft.com - [ServiceBus Explorer code]</span></span>

### <a name="verify-message-notifications"></a><span data-ttu-id="9146c-193">驗證訊息通知</span><span class="sxs-lookup"><span data-stu-id="9146c-193">Verify message notifications</span></span>
1. <span data-ttu-id="9146c-194">**Azure 傳統入口網站**</span><span class="sxs-lookup"><span data-stu-id="9146c-194">**Azure Classic Portal**</span></span>
   
    <span data-ttu-id="9146c-195">您可以前往 [偵錯] 索引標籤傳送測試通知給用戶端，這樣操作不需要任何運作中的服務後端即可完成。</span><span class="sxs-lookup"><span data-stu-id="9146c-195">You can go to the "Debug" tab to send test notifications to your clients without needing any service backend up and running.</span></span> 
   
    ![][7]
2. <span data-ttu-id="9146c-196">**Visual Studio**</span><span class="sxs-lookup"><span data-stu-id="9146c-196">**Visual Studio**</span></span>
   
    <span data-ttu-id="9146c-197">Visual Studio 還能讓您輕鬆舒適的傳送測試通知：</span><span class="sxs-lookup"><span data-stu-id="9146c-197">You can also send test notifications from the comforts of Visual Studio:</span></span>
   
    ![][10]
   
    <span data-ttu-id="9146c-198">以下文章提供 Visual Studio 通知中樞 Azure 總管功能的詳細資料：</span><span class="sxs-lookup"><span data-stu-id="9146c-198">You can read more on the Visual Studio Notification Hub Azure explorer functionality here -</span></span> 
   
   * <span data-ttu-id="9146c-199">[VS 伺服器總管概觀]</span><span class="sxs-lookup"><span data-stu-id="9146c-199">[VS Server Explorer Overview]</span></span>
   * <span data-ttu-id="9146c-200">[VS 伺服器總管部落格文章 - 1]</span><span class="sxs-lookup"><span data-stu-id="9146c-200">[VS Server Explorer Blog post - 1]</span></span>
   * <span data-ttu-id="9146c-201">[VS 伺服器總管部落格文章 - 2]</span><span class="sxs-lookup"><span data-stu-id="9146c-201">[VS Server Explorer Blog post - 2]</span></span>

### <a name="debug-failed-notifications-review-notification-outcome"></a><span data-ttu-id="9146c-202">偵錯失敗的通知 / 檢閱通知結果</span><span class="sxs-lookup"><span data-stu-id="9146c-202">Debug failed notifications/ Review notification outcome</span></span>
<span data-ttu-id="9146c-203">**EnableTestSend 屬性**</span><span class="sxs-lookup"><span data-stu-id="9146c-203">**EnableTestSend property**</span></span>

<span data-ttu-id="9146c-204">當您透過通知中樞傳送通知時，最初系統只會將其加入佇列並等候 NH 處理，找出通知的所有目標，最後 NH 才會將通知傳送給 PNS。</span><span class="sxs-lookup"><span data-stu-id="9146c-204">When you send a notification via Notification Hubs, initially it just gets queued up for NH to do processing to figure out all its targets and then eventually NH sends it to the PNS.</span></span> <span data-ttu-id="9146c-205">這表示當您使用 REST API 或任何用戶端 SDK 時，成功傳回傳送呼叫只代表系統已將訊息順利地加入通知中樞的佇列。</span><span class="sxs-lookup"><span data-stu-id="9146c-205">This means that when you are using REST API or any of the client SDK, the successful return of your send call only means that the message has been successfully queued up with Notification Hub.</span></span> <span data-ttu-id="9146c-206">我們無從得知 NH 最終將訊息傳送給 PNS 時發生什麼事。</span><span class="sxs-lookup"><span data-stu-id="9146c-206">It doesn’t give an insight into what happened when NH eventually got to send the message to PNS.</span></span> <span data-ttu-id="9146c-207">如果通知未抵達用戶端裝置，有可能是當 NH 嘗試將訊息傳遞給 PNS 時發生錯誤 (如承載大小超出 PNS 允許的上限或在 NH 中設定的認證無效等)。為了深入了解 PNS 錯誤，我們推出名為 [EnableTestSend 功能]的屬性。</span><span class="sxs-lookup"><span data-stu-id="9146c-207">If your notification is not arriving at the client device, there is a possibility that when NH tried to deliver the message to PNS, there was an error e.g. the payload size exceeded the maximum allowed by the PNS or the credentials configured in NH are invalid etc. To get an insight into the PNS errors, we have introduced a property called [EnableTestSend feature].</span></span> <span data-ttu-id="9146c-208">當您從入口網站或 Visual Studio 用戶端傳送測試訊息時，該屬性會自動啟用，供您查看詳細的偵錯資訊。</span><span class="sxs-lookup"><span data-stu-id="9146c-208">This property is automatically enabled when you send test messages from the portal or Visual Studio client and therefore allows you to see detailed debugging information.</span></span> <span data-ttu-id="9146c-209">以 .NET SDK 為例，您可以透過近期推出的 API 使用該屬性，我們最終也會將該屬性加入所有用戶端 SDK 中。</span><span class="sxs-lookup"><span data-stu-id="9146c-209">You can use this via APIs taking the example of the .NET SDK where it is available now and will be added to all client SDKs eventually.</span></span> <span data-ttu-id="9146c-210">若要搭配使用該屬性與 REST 呼叫，只要在傳送呼叫結尾附加名為 "test" 的 QueryString 參數即可，例如：</span><span class="sxs-lookup"><span data-stu-id="9146c-210">To use this with the REST call, simply append a querystring parameter called "test" at the end of your send call e.g.</span></span> 

    https://mynamespace.servicebus.windows.net/mynotificationhub/messages?api-version=2013-10&test

<span data-ttu-id="9146c-211">*範例 (.NET SDK)*</span><span class="sxs-lookup"><span data-stu-id="9146c-211">*Example (.NET SDK)*</span></span>

<span data-ttu-id="9146c-212">假設您使用 .NET SDK 來傳送原生快顯通知：</span><span class="sxs-lookup"><span data-stu-id="9146c-212">Suppose you are using .NET SDK to send a native toast notification:</span></span>

    NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString(connString, hubName);
    var result = await hub.SendWindowsNativeNotificationAsync(toast);
    Console.WriteLine(result.State);

<span data-ttu-id="9146c-213">`result.State` 只會在執行結束時陳述 `Enqueued`，不提供任何有關推播的歷程資訊。</span><span class="sxs-lookup"><span data-stu-id="9146c-213">`result.State` will simply state `Enqueued` at the end of the execution without any insight into what happened to your push.</span></span> <span data-ttu-id="9146c-214">現在您可以使用 `EnableTestSend` 布林值屬性並將 `NotificationHubClient` 初始化，如此便能取得在傳送通知時遭遇之 PNS 錯誤的詳細狀態。</span><span class="sxs-lookup"><span data-stu-id="9146c-214">Now you can use the `EnableTestSend` boolean property while initializing the `NotificationHubClient` and can get detailed status about the PNS errors encountered while sending the notification.</span></span> <span data-ttu-id="9146c-215">此處的傳送呼叫必須在 NH 將通知傳遞給 PNS 來判斷結果後才會傳回，因此需要花費額外的時間才能傳回。</span><span class="sxs-lookup"><span data-stu-id="9146c-215">The send call here will take additional time to return because it is only returning after NH has delivered the notification to PNS to determine the outcome.</span></span> 

    bool enableTestSend = true;
    NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString(connString, hubName, enableTestSend);

    var outcome = await hub.SendWindowsNativeNotificationAsync(toast);
    Console.WriteLine(outcome.State);

    foreach (RegistrationResult result in outcome.Results)
    {
        Console.WriteLine(result.ApplicationPlatform + "\n" + result.RegistrationId + "\n" + result.Outcome);
    }

<span data-ttu-id="9146c-216">*範例輸出*</span><span class="sxs-lookup"><span data-stu-id="9146c-216">*Sample Output*</span></span>

    DetailedStateAvailable
    windows
    7619785862101227384-7840974832647865618-3
    The Token obtained from the Token Provider is wrong

<span data-ttu-id="9146c-217">此訊息指出在通知中樞內設定的認證無效或中樞內的註冊有問題，建議的途徑是刪除該註冊並讓用戶端重新建立，隨後再傳送訊息。</span><span class="sxs-lookup"><span data-stu-id="9146c-217">This message indicates either invalid credentials are configured in the notification hub or an issue with the registrations on the hub and the recommended course would be to delete this registration and let the client recreate it before sending the message.</span></span> 

> [!NOTE]
> <span data-ttu-id="9146c-218">請注意，該屬性需在嚴密節流的情況下使用，其僅適用於註冊集有限的開發/測試環境。</span><span class="sxs-lookup"><span data-stu-id="9146c-218">Note that the use of this property is heavily throttled and so you must only use this in dev/test environment with limited set of registrations.</span></span> <span data-ttu-id="9146c-219">我們只會傳送偵錯通知給 10 部裝置。</span><span class="sxs-lookup"><span data-stu-id="9146c-219">We only send debug notifications to 10 devices.</span></span> <span data-ttu-id="9146c-220">我們的處理中偵錯傳送次數也有每分鐘 10 次的限制。</span><span class="sxs-lookup"><span data-stu-id="9146c-220">We also have a limit of processing debug sends to be 10 per minute.</span></span> 
> 
> 

### <a name="review-telemetry"></a><span data-ttu-id="9146c-221">檢閱遙測</span><span class="sxs-lookup"><span data-stu-id="9146c-221">Review telemetry</span></span>
1. <span data-ttu-id="9146c-222">**使用 Azure 傳統入口網站**</span><span class="sxs-lookup"><span data-stu-id="9146c-222">**Use Azure Classic Portal**</span></span>
   
    <span data-ttu-id="9146c-223">入口網站能讓您取得通知中樞上所有活動的簡要概觀。</span><span class="sxs-lookup"><span data-stu-id="9146c-223">The portal enables you to get a quick overview of all the activity on your Notification Hub.</span></span> 
   
    <span data-ttu-id="9146c-224">a) 在 [儀表板] 索引標籤中，您可以利用彙總檢視查看各平台的註冊、通知及錯誤。</span><span class="sxs-lookup"><span data-stu-id="9146c-224">a) From the "dashboard" tab you can view an aggregated view of the registrations, notifications as well as errors per platform.</span></span> 
   
    ![][5]
   
    <span data-ttu-id="9146c-225">b) 您也可以從 [監視] 索引標籤加入其他多樣化的平台專用度量，以便深入了解當 NH 嘗試將通知傳送給 PNS 時傳回的任何 PNS 特有錯誤。</span><span class="sxs-lookup"><span data-stu-id="9146c-225">b) You can also add many other platform specific metrics from the "Monitor" tab to take a deeper look particularly at any PNS specific errors returned when NH tries to send the notification to the PNS.</span></span> 
   
    ![][6]
   
    <span data-ttu-id="9146c-226">c) 您應從檢閱 [傳入訊息]、[註冊作業]、[成功的通知] 開始，然後再移至各平台的索引標籤來檢閱 PNS 特有錯誤。</span><span class="sxs-lookup"><span data-stu-id="9146c-226">c) You should start with reviewing the **Incoming Messages**, **Registration Operations**, **Successful Notifications** and then go to per platform tab to review the PNS specific errors.</span></span> 
   
    <span data-ttu-id="9146c-227">d) 如果通知中樞的驗證設定錯誤，您會看見 PNS 驗證錯誤。</span><span class="sxs-lookup"><span data-stu-id="9146c-227">d) If you have the notification hub misconfigured with the authentication settings then you will see PNS Authentication Error.</span></span> <span data-ttu-id="9146c-228">這是提醒您檢查 PNS 認證的徵兆。</span><span class="sxs-lookup"><span data-stu-id="9146c-228">This is a good indication to check the PNS credentials.</span></span> 

2) <span data-ttu-id="9146c-229">**程式設計存取**</span><span class="sxs-lookup"><span data-stu-id="9146c-229">**Programmatic access**</span></span>

<span data-ttu-id="9146c-230">以下文章提供更多詳細資料：</span><span class="sxs-lookup"><span data-stu-id="9146c-230">More details here -</span></span> 

* <span data-ttu-id="9146c-231">[程式設計遙測存取]</span><span class="sxs-lookup"><span data-stu-id="9146c-231">[Programmatic Telemetry Access]</span></span>
* <span data-ttu-id="9146c-232">[透過 API 存取遙測範例]</span><span class="sxs-lookup"><span data-stu-id="9146c-232">[Telemetry Access via APIs sample]</span></span> 

> [!NOTE]
> <span data-ttu-id="9146c-233">諸如**匯出/匯入註冊**、**透過 API 存取遙測**等數種遙測相關功能僅適用於 Standard 階層。</span><span class="sxs-lookup"><span data-stu-id="9146c-233">Several telemetry related features like **Export/Import Registrations**, **Telemetry Access via APIs** etc are only available in Standard tier.</span></span> <span data-ttu-id="9146c-234">如果您使用 Free 或 Basic 階層但嘗試使用以上功能，系統會顯示與此效果相關的例外狀況訊息 (使用 SDK 時) 和 HTTP 403 (禁止) (直接從 REST API 使用時)。</span><span class="sxs-lookup"><span data-stu-id="9146c-234">If you attempt to use these features if you are in Free or Basic tier then you will get exception message to this effect while using the SDK and an HTTP 403 (Forbidden) when using them directly from the REST APIs.</span></span> <span data-ttu-id="9146c-235">請務必透過 Azure 傳統入口網站上移至 Standard 階層。</span><span class="sxs-lookup"><span data-stu-id="9146c-235">Make sure that you have moved up to Standard tier via Azure Classic Portal.</span></span>  
> 
> 

<!-- IMAGES -->
[0]: ./media/notification-hubs-diagnosing/Architecture.png
[1]: ./media/notification-hubs-diagnosing/GCMConfigure.png
[2]: ./media/notification-hubs-diagnosing/GCMEnable.png
[3]: ./media/notification-hubs-diagnosing/GCMServerKey.png
[4]: ./media/notification-hubs-diagnosing/PortalConfigure.png
[5]: ./media/notification-hubs-diagnosing/PortalDashboard.png
[6]: ./media/notification-hubs-diagnosing/PortalMonitoring.png
[7]: ./media/notification-hubs-diagnosing/PortalTestNotification.png
[8]: ./media/notification-hubs-diagnosing/VSRegistrations.png
[9]: ./media/notification-hubs-diagnosing/VSServerExplorer.png
[10]: ./media/notification-hubs-diagnosing/VSTestNotification.png

<!-- LINKS -->
<span data-ttu-id="9146c-236">[通知中樞概觀]: notification-hubs-push-notification-overview.md</span><span class="sxs-lookup"><span data-stu-id="9146c-236">[Notification Hubs Overview]: notification-hubs-push-notification-overview.md</span></span>
<span data-ttu-id="9146c-237">[使用者入門教學課程]: notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md</span><span class="sxs-lookup"><span data-stu-id="9146c-237">[Getting Started Tutorials]: notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md</span></span>
<span data-ttu-id="9146c-238">[範本指引]: https://msdn.microsoft.com/library/dn530748.aspx </span><span class="sxs-lookup"><span data-stu-id="9146c-238">[Template guidance]: https://msdn.microsoft.com/library/dn530748.aspx </span></span>
<span data-ttu-id="9146c-239">[APNS 指引]: https://developer.apple.com/library/ios/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/Chapters/ApplePushService.html#//apple_ref/doc/uid/TP40008194-CH100-SW4</span><span class="sxs-lookup"><span data-stu-id="9146c-239">[APNS guidance]: https://developer.apple.com/library/ios/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/Chapters/ApplePushService.html#//apple_ref/doc/uid/TP40008194-CH100-SW4</span></span>
<span data-ttu-id="9146c-240">[GCM 指引]: http://developer.android.com/google/gcm/adv.html</span><span class="sxs-lookup"><span data-stu-id="9146c-240">[GCM guidance]: http://developer.android.com/google/gcm/adv.html</span></span>
[Export/Import Registrations]: http://msdn.microsoft.com/library/dn790624.aspx
<span data-ttu-id="9146c-241">[服務匯流排總管]: http://msdn.microsoft.com/library/dn530751.aspx</span><span class="sxs-lookup"><span data-stu-id="9146c-241">[ServiceBus Explorer]: http://msdn.microsoft.com/library/dn530751.aspx</span></span>
<span data-ttu-id="9146c-242">[服務匯流排總管程式碼]: https://code.msdn.microsoft.com/windowsazure/Service-Bus-Explorer-f2abca5a</span><span class="sxs-lookup"><span data-stu-id="9146c-242">[ServiceBus Explorer code]: https://code.msdn.microsoft.com/windowsazure/Service-Bus-Explorer-f2abca5a</span></span>
<span data-ttu-id="9146c-243">[VS 伺服器總管概觀]: http://msdn.microsoft.com/library/windows/apps/xaml/dn792122.aspx </span><span class="sxs-lookup"><span data-stu-id="9146c-243">[VS Server Explorer Overview]: http://msdn.microsoft.com/library/windows/apps/xaml/dn792122.aspx </span></span>
<span data-ttu-id="9146c-244">[VS 伺服器總管部落格文章 - 1]: http://azure.microsoft.com/blog/2014/04/09/deep-dive-visual-studio-2013-update-2-rc-and-azure-sdk-2-3/#NotificationHubs </span><span class="sxs-lookup"><span data-stu-id="9146c-244">[VS Server Explorer Blog post - 1]: http://azure.microsoft.com/blog/2014/04/09/deep-dive-visual-studio-2013-update-2-rc-and-azure-sdk-2-3/#NotificationHubs </span></span>
<span data-ttu-id="9146c-245">[VS 伺服器總管部落格文章 - 2]: http://azure.microsoft.com/blog/2014/08/04/announcing-release-of-visual-studio-2013-update-3-and-azure-sdk-2-4/ </span><span class="sxs-lookup"><span data-stu-id="9146c-245">[VS Server Explorer Blog post - 2]: http://azure.microsoft.com/blog/2014/08/04/announcing-release-of-visual-studio-2013-update-3-and-azure-sdk-2-4/ </span></span>
<span data-ttu-id="9146c-246">[EnableTestSend 功能]: http://msdn.microsoft.com/library/microsoft.servicebus.notifications.notificationhubclient.enabletestsend.aspx</span><span class="sxs-lookup"><span data-stu-id="9146c-246">[EnableTestSend feature]: http://msdn.microsoft.com/library/microsoft.servicebus.notifications.notificationhubclient.enabletestsend.aspx</span></span>
<span data-ttu-id="9146c-247">[程式設計遙測存取]: http://msdn.microsoft.com/library/azure/dn458823.aspx</span><span class="sxs-lookup"><span data-stu-id="9146c-247">[Programmatic Telemetry Access]: http://msdn.microsoft.com/library/azure/dn458823.aspx</span></span>
<span data-ttu-id="9146c-248">[透過 API 存取遙測範例]: https://github.com/Azure/azure-notificationhubs-samples/tree/master/FetchNHTelemetryInExcel</span><span class="sxs-lookup"><span data-stu-id="9146c-248">[Telemetry Access via APIs sample]: https://github.com/Azure/azure-notificationhubs-samples/tree/master/FetchNHTelemetryInExcel</span></span>

