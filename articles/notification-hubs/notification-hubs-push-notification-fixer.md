---
title: "aaaAzure 通知中樞-診斷指導方針"
description: "如何 toodiagnose 常見問題與 Azure 通知中心的指導方針。"
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
ms.openlocfilehash: e374278f2bfdfad36ba091e8846059cd184c17ef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-notification-hubs---diagnosis-guidelines"></a><span data-ttu-id="da561-103">Azure 通知中樞 - 診斷指導方針</span><span class="sxs-lookup"><span data-stu-id="da561-103">Azure Notification Hubs - Diagnosis guidelines</span></span>
## <a name="overview"></a><span data-ttu-id="da561-104">概觀</span><span class="sxs-lookup"><span data-stu-id="da561-104">Overview</span></span>
<span data-ttu-id="da561-105">Hello 最常見的問題，我們了解 Azure 通知中心客戶之一是 hello 用戶端在裝置上-toofigure 出為什麼會看到其應用程式後端傳送通知的顯示方式為何，通知已被卸除及如何 toofix 這。</span><span class="sxs-lookup"><span data-stu-id="da561-105">One of hello most common questions we hear from Azure Notification Hubs customers is how toofigure out why they don’t see a notification sent from their application backend appear on hello client device - where and why notifications were dropped and how toofix this.</span></span> <span data-ttu-id="da561-106">本文章中我們將探討 hello 各種原因，通知可能取得卸除或不至於 hello 裝置上。</span><span class="sxs-lookup"><span data-stu-id="da561-106">In this article we will go through hello various reasons why notifications may get dropped or do not end up on hello devices.</span></span> <span data-ttu-id="da561-107">我們也會查看的方式可分析並找出 hello 根本原因。</span><span class="sxs-lookup"><span data-stu-id="da561-107">We will also look through ways in which you can analyze and figure out hello root cause.</span></span> 

<span data-ttu-id="da561-108">首先，它是關鍵 toounderstand Azure 通知中樞推播通知時通知 toohello 裝置。</span><span class="sxs-lookup"><span data-stu-id="da561-108">First of all, it is critical toounderstand how Azure Notification Hubs pushes out notifications toohello devices.</span></span>
![][0]

<span data-ttu-id="da561-109">資料流程中的一般傳送通知，傳送 hello 訊息從 hello**應用程式後端**太**Azure 通知中樞 (NH)**其接著會納入所有 hello 註冊某些處理程序帳戶 hello 設定標記 （& s） 標記運算式 toodetermine 「 目標 」 也就是所有 hello 註冊需要 tooreceive hello 推播通知。</span><span class="sxs-lookup"><span data-stu-id="da561-109">In a typical send notification flow, hello message is sent from hello **application backend** too**Azure Notification Hub (NH)** which in turn does some processing on all hello registrations taking into account hello configured tags & tag expressions toodetermine "targets" i.e. all hello registrations that need tooreceive hello push notification.</span></span> <span data-ttu-id="da561-110">這些註冊可以跨越任何或所有我們支援的平台，包括 iOS、Google、Windows、Windows Phone、Kindle 及用於中國 Android 的百度。</span><span class="sxs-lookup"><span data-stu-id="da561-110">These registrations can span across any or all of our supported platforms - iOS, Google, Windows, Windows Phone, Kindle and Baidu for China Android.</span></span> <span data-ttu-id="da561-111">NH 則推播通知，一旦建立 hello 目標，分成多個批次的註冊，toohello 裝置平台特定**推播通知服務 (PNS)** -例如 Apple 的 APNS、 GCM Google 等等。NH 向的 hello 個別 PNS 根據您在 hello 設定通知中樞 頁面上的 hello Azure 傳統入口網站中設定的 hello 認證。</span><span class="sxs-lookup"><span data-stu-id="da561-111">Once hello targets are established, NH then pushes out notifications, split across multiple batch of registrations, toohello device platform specific **Push Notification Service (PNS)** - e.g. APNS for Apple, GCM for Google etc. NH authenticates with hello respective PNS based on hello credentials you set in hello Azure Classic Portal on hello Configure Notification Hub page.</span></span> <span data-ttu-id="da561-112">hello PNS 接著會將轉送 hello 通知 toohello 個別**用戶端裝置**。</span><span class="sxs-lookup"><span data-stu-id="da561-112">hello PNS then forwards hello notifications toohello respective **client devices**.</span></span> <span data-ttu-id="da561-113">這是建議的方式 toodeliver 推播通知和通知傳送嗨最後階段所花費的 hello 平台 PNS 與 hello 裝置之間的附註的 hello 平台。</span><span class="sxs-lookup"><span data-stu-id="da561-113">This is hello platform recommended way toodeliver push notifications and note that hello final leg of notification delivery takes place between hello platform PNS and hello device.</span></span> <span data-ttu-id="da561-114">因此我們有四個主要元件 - *用戶端*、*應用程式後端*、*Azure 通知中樞 (NH)* 和*推播通知服務 (PNS)*，而且其中任何一項可能會導致通知遭到捨棄。</span><span class="sxs-lookup"><span data-stu-id="da561-114">Therefore we have four major components - *client*, *application backend*, *Azure Notification Hubs (NH)* and *Push Notification Services (PNS)* and any of these may cause notifications getting dropped.</span></span> <span data-ttu-id="da561-115">如需此架構的詳細資料，請參閱[通知中樞概觀]。</span><span class="sxs-lookup"><span data-stu-id="da561-115">More details on this architecture is available on [Notification Hubs Overview].</span></span>

<span data-ttu-id="da561-116">失敗 toodeliver 通知可能會在 hello 初始測試執行階段也可能表示組態問題或是它可能會發生在所有或部分的 hello 通知的生產環境中可能會遭捨棄指出某些更深入的應用程式或傳訊模式的問題。</span><span class="sxs-lookup"><span data-stu-id="da561-116">Failure toodeliver notifications may happen during hello initial test/staging phase which may indicate a configuration issue or it may happen in production where either all or some of hello notifications may be getting dropped indicating some deeper application or messaging pattern issue.</span></span> <span data-ttu-id="da561-117">在 [hello] 區段中下, 面我們將探討各種範圍可從通用 toohello 更少見種類，其中有些可能會發現明顯和其他一些不太多的已卸除的通知案例。</span><span class="sxs-lookup"><span data-stu-id="da561-117">In hello section, below we will look at various dropped notifications scenarios ranging from common toohello rarer kind, some of which you may find obvious and some others not so much.</span></span> 

## <a name="azure-notifications-hub-mis-configuration"></a><span data-ttu-id="da561-118">Azure 通知中樞組態錯誤</span><span class="sxs-lookup"><span data-stu-id="da561-118">Azure Notifications Hub mis-configuration</span></span>
<span data-ttu-id="da561-119">Azure 通知中樞需要 tooauthenticate 本身 hello 內容中的 hello 開發人員應用程式 toobe toosuccessfully 無法傳送通知 toohello 個別 PNS。</span><span class="sxs-lookup"><span data-stu-id="da561-119">Azure Notification Hubs needs tooauthenticate itself in hello context of hello developer's application toobe able toosuccessfully send notifications toohello respective PNS.</span></span> <span data-ttu-id="da561-120">這樣做可能 hello 開發人員建立 hello 各平台 （Google、 Apple、 Windows 等等） 的開發人員帳戶，並再註冊他們的應用程式，他們會取得需要 toobe hello 入口網站，在 [通知] 中設定的認證中樞的組態區段。</span><span class="sxs-lookup"><span data-stu-id="da561-120">This is made possible by hello developer creating a developer account with hello respective platform (Google, Apple, Windows etc) and then registering their application where they get credentials which need toobe configured in hello portal under Notification Hubs configuration section.</span></span> <span data-ttu-id="da561-121">如果沒有通知要進行到第一個步驟應該 tooensure hello 通知中樞，其比對 hello 應用程式中設定的 hello 正確的認證建立其平台特定的開發人員帳戶。</span><span class="sxs-lookup"><span data-stu-id="da561-121">If no notifications are making through, first step should be tooensure that hello correct credentials are configured in hello Notification Hub matching them with hello application created under their platform specific developer account.</span></span> <span data-ttu-id="da561-122">您會發現我們[快速入門教學課程]有用 toogo 透過此程序，以逐步方式。</span><span class="sxs-lookup"><span data-stu-id="da561-122">You will find our [Getting Started Tutorials] useful toogo over this process in a step by step manner.</span></span> <span data-ttu-id="da561-123">以下是一些常見的組態錯誤：</span><span class="sxs-lookup"><span data-stu-id="da561-123">Here are some common mis-configurations:</span></span>

1. <span data-ttu-id="da561-124">**一般**</span><span class="sxs-lookup"><span data-stu-id="da561-124">**General**</span></span>
   
    <span data-ttu-id="da561-125">a） 請確定您的通知中樞名稱 （不含錯字） 是 hello 相同：</span><span class="sxs-lookup"><span data-stu-id="da561-125">a) Make sure that your notification hub name (without typos) is hello same:</span></span>
   
   * <span data-ttu-id="da561-126">您要註冊從 hello 用戶端，</span><span class="sxs-lookup"><span data-stu-id="da561-126">Where you are registering from hello client,</span></span> 
   * <span data-ttu-id="da561-127">您要將通知傳送嗨後端中從</span><span class="sxs-lookup"><span data-stu-id="da561-127">Where you are sending notifications from hello backend,</span></span>  
   * <span data-ttu-id="da561-128">您已在其中設定 hello PNS 認證和</span><span class="sxs-lookup"><span data-stu-id="da561-128">Where you have configured hello PNS credentials and</span></span> 
   * <span data-ttu-id="da561-129">您已經設定的 SAS 認證 hello 用戶端與 hello 後端。</span><span class="sxs-lookup"><span data-stu-id="da561-129">Whose SAS credentials you have configured on hello client and hello backend.</span></span> 
     
     <span data-ttu-id="da561-130">b） 請確定您使用正確 SAS 組態字串 hello hello 用戶端和 hello 應用程式後端上。</span><span class="sxs-lookup"><span data-stu-id="da561-130">b) Make sure that you are using hello correct SAS configuration strings on hello client and hello application backend.</span></span> <span data-ttu-id="da561-131">根據經驗法則，為您必須使用 hello **DefaultListenSharedAccessSignature** hello 用戶端上和**DefaultFullSharedAccessSignature** （它將提供權限 toobe hello 應用程式後端無法 toosend 通知 toohello NH)</span><span class="sxs-lookup"><span data-stu-id="da561-131">As a rule of thumb, you must be using hello **DefaultListenSharedAccessSignature** on hello client and **DefaultFullSharedAccessSignature** on hello application backend (which gives permission toobe able toosend notification toohello NH)</span></span>
2. <span data-ttu-id="da561-132">**Apple Push Notification Service (APNS) 組態**</span><span class="sxs-lookup"><span data-stu-id="da561-132">**Apple Push Notification Service (APNS) configuration**</span></span>
   
    <span data-ttu-id="da561-133">您必須維護兩個不同的中樞，一個供生產環境之用，另一個供測試之用。</span><span class="sxs-lookup"><span data-stu-id="da561-133">You must maintain two different hubs - one for production and another for testing purpose.</span></span> <span data-ttu-id="da561-134">這表示您將要 toouse 沙箱環境 tooa 個別中樞和您要在實際執行 tooa 個別中樞 toouse hello 憑證中的 hello 憑證上傳。</span><span class="sxs-lookup"><span data-stu-id="da561-134">This means uploading hello certificate you are going toouse in sandbox environment tooa separate hub and hello certificate you are going toouse in production tooa separate hub.</span></span> <span data-ttu-id="da561-135">請勿嘗試 tooupload 不同類型的憑證 toohello 相同的中樞，因為它可能會造成 hello 列關閉通知失敗。</span><span class="sxs-lookup"><span data-stu-id="da561-135">Do not try tooupload different types of certificates toohello same hub as it may cause notification failures down hello line.</span></span> <span data-ttu-id="da561-136">如果您發現自己已不小心上載憑證 toohello 種不同的位置相同的中樞建議 toodelete hello 中樞和全新的開始。</span><span class="sxs-lookup"><span data-stu-id="da561-136">If you do find yourself in a position where you have inadvertently uploaded different types of certificate toohello same hub, it is recommended toodelete hello hub and start fresh.</span></span> <span data-ttu-id="da561-137">如果基於某些原因，您不能 toodelete hello 集線器，然後在 hello 非常少，您必須刪除所有 hello 現有登錄從 hello 中樞。</span><span class="sxs-lookup"><span data-stu-id="da561-137">If for some reason, you are not able toodelete hello hub then at hello very least, you must delete all hello existing registrations from hello hub.</span></span> 
3. <span data-ttu-id="da561-138">**Google 雲端通訊 (GCM) 組態**</span><span class="sxs-lookup"><span data-stu-id="da561-138">**Google Cloud Messaging (GCM) configuration**</span></span> 
   
    <span data-ttu-id="da561-139">a) 確認您在雲端專案下啟用的是 "Google Cloud Messaging for Android"。</span><span class="sxs-lookup"><span data-stu-id="da561-139">a) Make sure that you are enabling "Google Cloud Messaging for Android" under your cloud project.</span></span> 
   
    ![][2]
   
    <span data-ttu-id="da561-140">b） 請確定您建立 「 伺服器金鑰 」，而哪些 NH 取得 hello 認證與要使用 tooauthenticate GCM。</span><span class="sxs-lookup"><span data-stu-id="da561-140">b) Make sure that you create a "Server Key" while obtaining hello credentials which NH will use tooauthenticate with GCM.</span></span> 
   
    ![][3]
   
    <span data-ttu-id="da561-141">c） 請確定您擁有 hello 用戶端，也就是您可以從 hello 儀表板取得完全數值實體上設定 「 專案識別碼 」:</span><span class="sxs-lookup"><span data-stu-id="da561-141">c) Make sure that you have configured "Project ID" on hello client which is an entirely numerical entity that you can obtain from hello dashboard:</span></span>
   
    ![][1]

## <a name="application-issues"></a><span data-ttu-id="da561-142">應用程式問題</span><span class="sxs-lookup"><span data-stu-id="da561-142">Application issues</span></span>
1) <span data-ttu-id="da561-143">**標記/ 標記運算式**</span><span class="sxs-lookup"><span data-stu-id="da561-143">**Tags/ Tag expressions**</span></span>

<span data-ttu-id="da561-144">如果您使用的標記或標記運算式 toosegment 您的對象，它仍然可以將傳送嗨通知時，沒有找到根據 hello 標記/標記運算式就您傳送的呼叫中指定任何目標。</span><span class="sxs-lookup"><span data-stu-id="da561-144">If you are using tags or tag expressions toosegment your audience, it is always possible that when you are sending hello notification, there is no target being found based on hello tags/tag expressions you are specifying in your send call.</span></span> <span data-ttu-id="da561-145">建議您最好 tooreview 有您註冊 tooensure 標記的相符項目時您傳送通知，然後檢查 只能從 hello 與這些註冊的用戶端 hello 通知回條。</span><span class="sxs-lookup"><span data-stu-id="da561-145">It is best tooreview your registrations tooensure that there are tags which match when you send notification and then verify hello notification receipt only from hello clients with those registrations.</span></span> <span data-ttu-id="da561-146">例如</span><span class="sxs-lookup"><span data-stu-id="da561-146">E.g.</span></span> <span data-ttu-id="da561-147">如果 NH 與您註冊已完成所有說 「 政治"標記，而且您要傳送標記通知 」 運動"，它將不會傳送 tooany 裝置。</span><span class="sxs-lookup"><span data-stu-id="da561-147">if all your registrations with NH were done with say tag "Politics" and you are sending a notification with tag "Sports", it will not be sent tooany device.</span></span> <span data-ttu-id="da561-148">複雜的案例可能涉及只註冊 "Tag A" OR "Tag B" 的標記運算式，然而在傳送通知時，您設定的目標為 "Tag A && Tag B"。</span><span class="sxs-lookup"><span data-stu-id="da561-148">A complex case could involve tag expressions where you only registered with "Tag A" OR "Tag B" but while sending notifications, you are targeting "Tag A && Tag B".</span></span> <span data-ttu-id="da561-149">Hello 自行診斷提示一節，您可以檢閱 hello 標籤它們擁有與您註冊的方式。</span><span class="sxs-lookup"><span data-stu-id="da561-149">In hello self-diagnose tips section below, there are ways in which you can review your registrations along with hello tags they have.</span></span> 

2) <span data-ttu-id="da561-150">**範本問題**</span><span class="sxs-lookup"><span data-stu-id="da561-150">**Template issues**</span></span>

<span data-ttu-id="da561-151">如果您使用範本則可確保您要遵照 hello 指導方針所述[範本指引]。</span><span class="sxs-lookup"><span data-stu-id="da561-151">If you are using templates then ensure that you are following hello guidelines described at [Template guidance].</span></span> 

3) <span data-ttu-id="da561-152">**無效的註冊**</span><span class="sxs-lookup"><span data-stu-id="da561-152">**Invalid registrations**</span></span>

<span data-ttu-id="da561-153">假設已正確設定通知中樞的 hello 和任何標記/標記運算式所使用的有效目標 toowhich hello 通知需要 toobe 傳送嗨尋找正確產生，以平行方式-每個批次的數個處理批次關閉引發 NH傳送訊息 tooa 登錄裝置集合。</span><span class="sxs-lookup"><span data-stu-id="da561-153">Assuming hello Notification Hub was configured correctly and any tags/tag expressions were used correctly resulting in hello find of valid targets toowhich hello notifications need toobe sent, NH fires off several processing batches in parallel - each batch sending messages tooa set of registrations.</span></span> 

> [!NOTE]
> <span data-ttu-id="da561-154">因為我們不要 hello 以平行方式處理，我們不保證 hello 順序中的 hello 將傳遞通知。</span><span class="sxs-lookup"><span data-stu-id="da561-154">Since we do hello processing in parallel, we don’t guarantee hello order in which hello notifications will be delivered.</span></span> 
> 
> 

<span data-ttu-id="da561-155">現在我們已根據「最多一次」訊息傳遞模式將 Azure 通知中樞最佳化。</span><span class="sxs-lookup"><span data-stu-id="da561-155">Now Azure Notifications Hub is optimized for an "at-most once" message delivery model.</span></span> <span data-ttu-id="da561-156">這表示我們嘗試刪除重複作業，以便通知會傳遞一次以上 tooa 裝置。</span><span class="sxs-lookup"><span data-stu-id="da561-156">This means that we attempt a de-duplication so that no notifications are delivered more than once tooa device.</span></span> <span data-ttu-id="da561-157">tooensure 這我們查看 hello 註冊，並且確保該只能有一個訊息是每秒傳送的實際傳送 hello 訊息 toohello PNS 之前的裝置識別碼。</span><span class="sxs-lookup"><span data-stu-id="da561-157">tooensure this we look through hello registrations and make sure that only one message is sent per device identifier before actually sending hello message toohello PNS.</span></span> <span data-ttu-id="da561-158">每個批次傳送 toohello PNS，接著會接受並驗證 hello 註冊，所以該 hello PNS 批次中偵測到與一或多個 hello 註冊錯誤時，會傳回錯誤 tooAzure NH 並停止處理，藉此卸除完整的批次。</span><span class="sxs-lookup"><span data-stu-id="da561-158">As each batch is sent toohello PNS, which in turn is accepting and validating hello registrations, it is possible that hello PNS detects an error with one or more of hello registrations in a batch, returns an error tooAzure NH and stops processing thereby dropping that batch completely.</span></span> <span data-ttu-id="da561-159">對於使用 TCP 串流通訊協定的 APNS 來說，這種情況尤其顯著。</span><span class="sxs-lookup"><span data-stu-id="da561-159">This is especially true with APNS which uses a TCP stream protocol.</span></span> <span data-ttu-id="da561-160">雖然我們一次最佳化在大部分的傳遞，在此情況下，我們會移除 hello 我們資料庫，然後重試通知傳送該批次中的 hello 裝置 hello 其餘部分從失敗的註冊。</span><span class="sxs-lookup"><span data-stu-id="da561-160">Although we are optimized for at-most once delivery, in this case we remove hello faulting registration from our database and then retry notification delivery for hello rest of hello devices in that batch.</span></span>

<span data-ttu-id="da561-161">您可以取得 hello 傳遞失敗的嘗試針對使用 Azure 通知中心 REST Api hello 註冊資訊時發生錯誤：[每個訊息遙測： 取得通知訊息遙測](https://msdn.microsoft.com/library/azure/mt608135.aspx)和[PNS 意見反應](https://msdn.microsoft.com/library/azure/mt705560.aspx).</span><span class="sxs-lookup"><span data-stu-id="da561-161">You can get error information for hello failed delivery attempt against a registration using hello Azure Notification Hubs REST APIs: [Per Message Telemetry: Get Notification Message Telemetry](https://msdn.microsoft.com/library/azure/mt608135.aspx) and [PNS Feedback](https://msdn.microsoft.com/library/azure/mt705560.aspx).</span></span> <span data-ttu-id="da561-162">請參閱 hello [SendRESTExample](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/SendRestExample)例如程式碼。</span><span class="sxs-lookup"><span data-stu-id="da561-162">See hello [SendRESTExample](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/SendRestExample) for example code.</span></span>

## <a name="pns-issues"></a><span data-ttu-id="da561-163">PNS 問題</span><span class="sxs-lookup"><span data-stu-id="da561-163">PNS issues</span></span>
<span data-ttu-id="da561-164">一旦 hello 通知訊息已收到 hello 個別 PNS，則其責任 toodeliver hello 通知 toohello 裝置。</span><span class="sxs-lookup"><span data-stu-id="da561-164">Once hello notification message has been received by hello respective PNS then it is its responsibility toodeliver hello notification toohello device.</span></span> <span data-ttu-id="da561-165">Azure 通知中樞超出 hello 的圖片且沒有控制權時，或如果 hello 通知將會傳遞 toohello 裝置 toobe。</span><span class="sxs-lookup"><span data-stu-id="da561-165">Azure Notification Hubs is out of hello picture here and has no control on when or if hello notification is going toobe delivered toohello device.</span></span> <span data-ttu-id="da561-166">Hello 平台通知服務都很穩定，因為通知不要從 hello PNS 就在幾秒鐘的時間通常 tooreach hello 裝置。</span><span class="sxs-lookup"><span data-stu-id="da561-166">Since hello platform notification services are pretty robust, notifications do tend tooreach hello devices in a few seconds from hello PNS.</span></span> <span data-ttu-id="da561-167">如果 hello PNS 不過正在進行節流然後 Azure 通知中心會套用指數型停止策略，如果 hello PNS 會保留 30 分鐘無法連線到然後我們有的原則中放置 tooexpire 且永久卸除這些訊息。</span><span class="sxs-lookup"><span data-stu-id="da561-167">If hello PNS however is throttling then Azure Notification Hubs does apply an exponential back off strategy and if hello PNS remains unreachable for 30 min then we have a policy in place tooexpire and drop those messages permanently.</span></span> 

<span data-ttu-id="da561-168">如果 PNS 嘗試 toodeliver 通知，但 hello 裝置已離線，hello 通知是由 hello PNS 針對一段有限的時間，儲存和傳遞 toohello 裝置可供使用時。</span><span class="sxs-lookup"><span data-stu-id="da561-168">If a PNS attempts toodeliver a notification but hello device is offline, hello notification is stored by hello PNS for a limited period of time, and delivered toohello device when it becomes available.</span></span> <span data-ttu-id="da561-169">PNS 只會針對每個應用程式儲存一則最近的通知。</span><span class="sxs-lookup"><span data-stu-id="da561-169">Only one recent notification for a particular app is stored.</span></span> <span data-ttu-id="da561-170">如果多個通知會傳送 hello 裝置離線時，每個新的通知會導致捨棄 toobe hello 事先通知。</span><span class="sxs-lookup"><span data-stu-id="da561-170">If multiple notifications are sent while hello device is offline, each new notification causes hello prior notification toobe discarded.</span></span> <span data-ttu-id="da561-171">保持 hello 最新通知的這個行為是參照的 tooas 聯合中 APNS 通知和 GCM （這會使用摺疊的索引鍵） 在摺疊。</span><span class="sxs-lookup"><span data-stu-id="da561-171">This behavior of keeping only hello newest notification is referred tooas coalescing notifications in APNS and collapsing in GCM (which uses a collapsing key).</span></span> <span data-ttu-id="da561-172">如果 hello 裝置長時間保持離線狀態，則會捨棄它所儲存的任何通知。</span><span class="sxs-lookup"><span data-stu-id="da561-172">If hello device remains offline for a long time, any notifications that were being stored for it are discarded.</span></span> <span data-ttu-id="da561-173">資料來源 - [APNS 指引] & [GCM 指引]</span><span class="sxs-lookup"><span data-stu-id="da561-173">Source - [APNS guidance] & [GCM guidance]</span></span>

<span data-ttu-id="da561-174">與 Azure 通知中心-您可以傳遞聯合的索引鍵，透過 HTTP 標頭使用 hello 泛型`SendNotification`應用程式開發介面 (例如 for.NET SDK – `SendNotificationAsync`) 這也會採用傳遞做為 HTTP 標頭是 toohello 個別 PNS。</span><span class="sxs-lookup"><span data-stu-id="da561-174">With Azure Notification Hubs - you can pass a coalescing key via an HTTP header using hello generic `SendNotification` API (e.g. for .NET SDK – `SendNotificationAsync`) which also takes HTTP headers which are passed as is toohello respective PNS.</span></span> 

## <a name="self-diagnose-tips"></a><span data-ttu-id="da561-175">自我診斷秘訣</span><span class="sxs-lookup"><span data-stu-id="da561-175">Self-diagnose tips</span></span>
<span data-ttu-id="da561-176">我們將在這裡檢視 hello 各種途徑 toodiagnose 和根會造成任何通知中樞的問題：</span><span class="sxs-lookup"><span data-stu-id="da561-176">Here we will examine hello various avenues toodiagnose and root cause any Notification Hub issues:</span></span>

### <a name="verify-credentials"></a><span data-ttu-id="da561-177">驗證認證</span><span class="sxs-lookup"><span data-stu-id="da561-177">Verify credentials</span></span>
1. <span data-ttu-id="da561-178">**PNS 開發人員入口網站**</span><span class="sxs-lookup"><span data-stu-id="da561-178">**PNS developer portal**</span></span>
   
    <span data-ttu-id="da561-179">確認它們在 hello 個別 PNS 開發人員入口網站 （APNS、 GCM，WNS 等等） 使用我們[快速入門教學課程]。</span><span class="sxs-lookup"><span data-stu-id="da561-179">Verify them at hello respective PNS developer portal (APNS, GCM, WNS etc) using our [Getting Started Tutorials].</span></span>
2. <span data-ttu-id="da561-180">**Azure 傳統入口網站**</span><span class="sxs-lookup"><span data-stu-id="da561-180">**Azure Classic portal**</span></span>
   
    <span data-ttu-id="da561-181">Toohello 設定 索引標籤 tooreview 去符合 hello 認證與取自 hello PNS 開發人員入口網站。</span><span class="sxs-lookup"><span data-stu-id="da561-181">Go toohello Configure tab tooreview and match hello credentials with those obtained from hello PNS developer portal.</span></span> 
   
    ![][4]

### <a name="verify-registrations"></a><span data-ttu-id="da561-182">驗證註冊</span><span class="sxs-lookup"><span data-stu-id="da561-182">Verify registrations</span></span>
1. <span data-ttu-id="da561-183">**Visual Studio**</span><span class="sxs-lookup"><span data-stu-id="da561-183">**Visual Studio**</span></span>
   
    <span data-ttu-id="da561-184">如果您使用 Visual Studio 進行開發然後您可以連接 tooMicrosoft Azure 和檢視和管理 Azure 服務，包括來自 「 伺服器總管 」 的通知中樞的一大堆。</span><span class="sxs-lookup"><span data-stu-id="da561-184">If you use Visual Studio for development then you can connect tooMicrosoft Azure and view and manage a bunch of Azure services including Notifications Hub from "Server Explorer".</span></span> <span data-ttu-id="da561-185">這能為您的開發/測試環境帶來許多助益。</span><span class="sxs-lookup"><span data-stu-id="da561-185">This is primarily useful for your dev/test environment.</span></span> 
   
    ![][9]
   
    <span data-ttu-id="da561-186">您可以檢視和管理所有 hello 註冊您的中樞中正確地切割分類平台、 原生模式或範本的註冊任何標記，PNS 識別碼、 註冊 id 和 hello 到期日。</span><span class="sxs-lookup"><span data-stu-id="da561-186">You can view and manage all hello registrations in your hub which are nicely categorized for platform, native or template registration, any tags, PNS identifier, registration id and hello expiration date.</span></span> <span data-ttu-id="da561-187">您也可以編輯 hello 立即-這是假設如果您想 tooedit 任何標記時，才能註冊。</span><span class="sxs-lookup"><span data-stu-id="da561-187">You can also edit a registration on hello fly - which is useful say if you want tooedit any tags.</span></span> 
   
    ![][8]
   
   > [!NOTE]
   > <span data-ttu-id="da561-188">Visual Studio 功能 tooedit 註冊應該只用於開發/測試與有限數目的登錄期間。</span><span class="sxs-lookup"><span data-stu-id="da561-188">Visual Studio functionality tooedit registrations should only be used during dev/test with limited number of registrations.</span></span> <span data-ttu-id="da561-189">如果那里，就會發生需要 toofix 您註冊大量，請考慮使用 hello 所描述的匯出/匯入登錄功能這裡-[匯出/匯入登錄](https://msdn.microsoft.com/library/dn790624.aspx)</span><span class="sxs-lookup"><span data-stu-id="da561-189">If there arises a need toofix your registrations in bulk, consider using hello Export/Import registration functionality described here - [Export/Import Registrations](https://msdn.microsoft.com/library/dn790624.aspx)</span></span>
   > 
   > 
2. <span data-ttu-id="da561-190">**服務匯流排總管**</span><span class="sxs-lookup"><span data-stu-id="da561-190">**Service Bus explorer**</span></span>
   
    <span data-ttu-id="da561-191">有許多客戶使用 [服務匯流排總管] 所述的服務匯流排總管來檢視及管理通知中樞。</span><span class="sxs-lookup"><span data-stu-id="da561-191">Many customers use ServiceBus explorer described here - [ServiceBus Explorer] for viewing and managing their notification hub.</span></span> <span data-ttu-id="da561-192">其為可從 code.microsoft.com - [服務匯流排總管程式碼]</span><span class="sxs-lookup"><span data-stu-id="da561-192">It is an open source project available from code.microsoft.com - [ServiceBus Explorer code]</span></span>

### <a name="verify-message-notifications"></a><span data-ttu-id="da561-193">驗證訊息通知</span><span class="sxs-lookup"><span data-stu-id="da561-193">Verify message notifications</span></span>
1. <span data-ttu-id="da561-194">**Azure 傳統入口網站**</span><span class="sxs-lookup"><span data-stu-id="da561-194">**Azure Classic Portal**</span></span>
   
    <span data-ttu-id="da561-195">您可以移 toohello [偵錯] 索引標籤 toosend 測試通知 tooyour 用戶端，而不需要任何服務後端設定和執行。</span><span class="sxs-lookup"><span data-stu-id="da561-195">You can go toohello "Debug" tab toosend test notifications tooyour clients without needing any service backend up and running.</span></span> 
   
    ![][7]
2. <span data-ttu-id="da561-196">**Visual Studio**</span><span class="sxs-lookup"><span data-stu-id="da561-196">**Visual Studio**</span></span>
   
    <span data-ttu-id="da561-197">您也可以從 Visual Studio 的 hello comforts 傳送測試通知：</span><span class="sxs-lookup"><span data-stu-id="da561-197">You can also send test notifications from hello comforts of Visual Studio:</span></span>
   
    ![][10]
   
    <span data-ttu-id="da561-198">您可以閱讀更多在 hello Visual Studio 通知中樞 Azure 總管的功能這裡</span><span class="sxs-lookup"><span data-stu-id="da561-198">You can read more on hello Visual Studio Notification Hub Azure explorer functionality here -</span></span> 
   
   * <span data-ttu-id="da561-199">[VS 伺服器總管概觀]</span><span class="sxs-lookup"><span data-stu-id="da561-199">[VS Server Explorer Overview]</span></span>
   * <span data-ttu-id="da561-200">[VS 伺服器總管部落格文章 - 1]</span><span class="sxs-lookup"><span data-stu-id="da561-200">[VS Server Explorer Blog post - 1]</span></span>
   * <span data-ttu-id="da561-201">[VS 伺服器總管部落格文章 - 2]</span><span class="sxs-lookup"><span data-stu-id="da561-201">[VS Server Explorer Blog post - 2]</span></span>

### <a name="debug-failed-notifications-review-notification-outcome"></a><span data-ttu-id="da561-202">偵錯失敗的通知 / 檢閱通知結果</span><span class="sxs-lookup"><span data-stu-id="da561-202">Debug failed notifications/ Review notification outcome</span></span>
<span data-ttu-id="da561-203">**EnableTestSend 屬性**</span><span class="sxs-lookup"><span data-stu-id="da561-203">**EnableTestSend property**</span></span>

<span data-ttu-id="da561-204">當您傳送通知中樞通知時，一開始它只取得佇列中等待 NH toodo 處理 toofigure 出其所有的目標，然後最終 NH 傳送它 toohello PNS。</span><span class="sxs-lookup"><span data-stu-id="da561-204">When you send a notification via Notification Hubs, initially it just gets queued up for NH toodo processing toofigure out all its targets and then eventually NH sends it toohello PNS.</span></span> <span data-ttu-id="da561-205">這表示，當您使用 REST API 或任何 hello client SDK，hello 成功傳回時為您傳送呼叫只表示 hello 訊息已成功排搭配通知中樞。</span><span class="sxs-lookup"><span data-stu-id="da561-205">This means that when you are using REST API or any of hello client SDK, hello successful return of your send call only means that hello message has been successfully queued up with Notification Hub.</span></span> <span data-ttu-id="da561-206">它不會讓您瞭解 NH 最後收到 toosend hello 訊息 tooPNS 時，發生了什麼事。</span><span class="sxs-lookup"><span data-stu-id="da561-206">It doesn’t give an insight into what happened when NH eventually got toosend hello message tooPNS.</span></span> <span data-ttu-id="da561-207">如果您的通知，則不抵達 hello 用戶端裝置，當 NH 嘗試 toodeliver hello 訊息 tooPNS，時發生錯誤，例如 hello 承載大小可能超過允許的 hello PNS 的 hello 上限或是設定 NH 中的 hello 認證是深入了解 hello PNS 錯誤的無效等 tooget，我們引進的屬性，稱為[EnableTestSend 功能]。</span><span class="sxs-lookup"><span data-stu-id="da561-207">If your notification is not arriving at hello client device, there is a possibility that when NH tried toodeliver hello message tooPNS, there was an error e.g. hello payload size exceeded hello maximum allowed by hello PNS or hello credentials configured in NH are invalid etc. tooget an insight into hello PNS errors, we have introduced a property called [EnableTestSend feature].</span></span> <span data-ttu-id="da561-208">當您傳送測試訊息從 hello 入口網站或 Visual Studio 用戶端，並因此允許 toosee 詳細，這個屬性會自動啟用偵錯資訊。</span><span class="sxs-lookup"><span data-stu-id="da561-208">This property is automatically enabled when you send test messages from hello portal or Visual Studio client and therefore allows you toosee detailed debugging information.</span></span> <span data-ttu-id="da561-209">您可以使用這透過採取 hello 範例 hello 都能立即.NET SDK 的 Api，將會加入的 tooall 用戶端 Sdk 最後。</span><span class="sxs-lookup"><span data-stu-id="da561-209">You can use this via APIs taking hello example of hello .NET SDK where it is available now and will be added tooall client SDKs eventually.</span></span> <span data-ttu-id="da561-210">toouse hello REST 呼叫，這只是附加結尾 hello 傳送呼叫中例如稱為 「 測試 」 的 querystring 參數</span><span class="sxs-lookup"><span data-stu-id="da561-210">toouse this with hello REST call, simply append a querystring parameter called "test" at hello end of your send call e.g.</span></span> 

    https://mynamespace.servicebus.windows.net/mynotificationhub/messages?api-version=2013-10&test

<span data-ttu-id="da561-211">*範例 (.NET SDK)*</span><span class="sxs-lookup"><span data-stu-id="da561-211">*Example (.NET SDK)*</span></span>

<span data-ttu-id="da561-212">假設您使用.NET SDK toosend 原生快顯通知：</span><span class="sxs-lookup"><span data-stu-id="da561-212">Suppose you are using .NET SDK toosend a native toast notification:</span></span>

    NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString(connString, hubName);
    var result = await hub.SendWindowsNativeNotificationAsync(toast);
    Console.WriteLine(result.State);

<span data-ttu-id="da561-213">`result.State`將只狀態`Enqueued`結尾 hello hello 執行不含任何深入了解什麼發生 tooyour 推入。</span><span class="sxs-lookup"><span data-stu-id="da561-213">`result.State` will simply state `Enqueued` at hello end of hello execution without any insight into what happened tooyour push.</span></span> <span data-ttu-id="da561-214">現在您可以使用 hello `EnableTestSend` hello 進行初始化時的布林值屬性`NotificationHubClient`，並可以取得有關傳送嗨通知時發生 hello PNS 錯誤的詳細的狀態。</span><span class="sxs-lookup"><span data-stu-id="da561-214">Now you can use hello `EnableTestSend` boolean property while initializing hello `NotificationHubClient` and can get detailed status about hello PNS errors encountered while sending hello notification.</span></span> <span data-ttu-id="da561-215">需要額外的時間 tooreturn hello 傳送呼叫，因為它只會傳回 NH 已傳送嗨通知 tooPNS toodetermine hello 結果之後。</span><span class="sxs-lookup"><span data-stu-id="da561-215">hello send call here will take additional time tooreturn because it is only returning after NH has delivered hello notification tooPNS toodetermine hello outcome.</span></span> 

    bool enableTestSend = true;
    NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString(connString, hubName, enableTestSend);

    var outcome = await hub.SendWindowsNativeNotificationAsync(toast);
    Console.WriteLine(outcome.State);

    foreach (RegistrationResult result in outcome.Results)
    {
        Console.WriteLine(result.ApplicationPlatform + "\n" + result.RegistrationId + "\n" + result.Outcome);
    }

<span data-ttu-id="da561-216">*範例輸出*</span><span class="sxs-lookup"><span data-stu-id="da561-216">*Sample Output*</span></span>

    DetailedStateAvailable
    windows
    7619785862101227384-7840974832647865618-3
    hello Token obtained from hello Token Provider is wrong

<span data-ttu-id="da561-217">此訊息表示 hello 通知中樞的設定不正確的認證或 hello 中樞和 hello hello 註冊發生問題的建議課程會 toodelete 此登錄，讓重新建立之前傳送嗨 hello 用戶端訊息。</span><span class="sxs-lookup"><span data-stu-id="da561-217">This message indicates either invalid credentials are configured in hello notification hub or an issue with hello registrations on hello hub and hello recommended course would be toodelete this registration and let hello client recreate it before sending hello message.</span></span> 

> [!NOTE]
> <span data-ttu-id="da561-218">請注意，hello 使用此屬性有很大節流處理，因此您必須只使用這組有限的註冊開發/測試環境中。</span><span class="sxs-lookup"><span data-stu-id="da561-218">Note that hello use of this property is heavily throttled and so you must only use this in dev/test environment with limited set of registrations.</span></span> <span data-ttu-id="da561-219">我們只會傳送偵錯通知 too10 裝置。</span><span class="sxs-lookup"><span data-stu-id="da561-219">We only send debug notifications too10 devices.</span></span> <span data-ttu-id="da561-220">我們也會有處理每分鐘的偵錯傳送 toobe 10 的限制。</span><span class="sxs-lookup"><span data-stu-id="da561-220">We also have a limit of processing debug sends toobe 10 per minute.</span></span> 
> 
> 

### <a name="review-telemetry"></a><span data-ttu-id="da561-221">檢閱遙測</span><span class="sxs-lookup"><span data-stu-id="da561-221">Review telemetry</span></span>
1. <span data-ttu-id="da561-222">**使用 Azure 傳統入口網站**</span><span class="sxs-lookup"><span data-stu-id="da561-222">**Use Azure Classic Portal**</span></span>
   
    <span data-ttu-id="da561-223">hello 入口網站可讓您 tooget 通知中樞上的所有 hello 活動的快速概觀。</span><span class="sxs-lookup"><span data-stu-id="da561-223">hello portal enables you tooget a quick overview of all hello activity on your Notification Hub.</span></span> 
   
    <span data-ttu-id="da561-224">a） 從 hello 」 儀表板 索引標籤中，您可以檢視 hello 註冊、 通知，以及每個平台錯誤的彙總的檢視。</span><span class="sxs-lookup"><span data-stu-id="da561-224">a) From hello "dashboard" tab you can view an aggregated view of hello registrations, notifications as well as errors per platform.</span></span> 
   
    ![][5]
   
    <span data-ttu-id="da561-225">b） 您也可以從 hello 「 監視 」 索引標籤 tootake 更深入的探討，特別是在任何 PNS 特定的錯誤傳回 NH 嘗試 toosend hello 通知 toohello PNS 時加入許多其他平台特定的衡量標準。</span><span class="sxs-lookup"><span data-stu-id="da561-225">b) You can also add many other platform specific metrics from hello "Monitor" tab tootake a deeper look particularly at any PNS specific errors returned when NH tries toosend hello notification toohello PNS.</span></span> 
   
    ![][6]
   
    <span data-ttu-id="da561-226">c） 您的開頭應檢閱 hello**內送訊息**，**註冊作業**，**成功通知**並前往 tooper 平台 索引標籤 tooreview helloPNS 特定錯誤。</span><span class="sxs-lookup"><span data-stu-id="da561-226">c) You should start with reviewing hello **Incoming Messages**, **Registration Operations**, **Successful Notifications** and then go tooper platform tab tooreview hello PNS specific errors.</span></span> 
   
    <span data-ttu-id="da561-227">d） 如果您擁有 hello 通知中樞的設定不正確使用 hello 驗證設定然後您會看到 PNS 驗證錯誤。</span><span class="sxs-lookup"><span data-stu-id="da561-227">d) If you have hello notification hub misconfigured with hello authentication settings then you will see PNS Authentication Error.</span></span> <span data-ttu-id="da561-228">這是很好的指標 toocheck hello PNS 認證。</span><span class="sxs-lookup"><span data-stu-id="da561-228">This is a good indication toocheck hello PNS credentials.</span></span> 

2) <span data-ttu-id="da561-229">**程式設計存取**</span><span class="sxs-lookup"><span data-stu-id="da561-229">**Programmatic access**</span></span>

<span data-ttu-id="da561-230">以下文章提供更多詳細資料：</span><span class="sxs-lookup"><span data-stu-id="da561-230">More details here -</span></span> 

* <span data-ttu-id="da561-231">[程式設計遙測存取]</span><span class="sxs-lookup"><span data-stu-id="da561-231">[Programmatic Telemetry Access]</span></span>
* <span data-ttu-id="da561-232">[透過 API 存取遙測範例]</span><span class="sxs-lookup"><span data-stu-id="da561-232">[Telemetry Access via APIs sample]</span></span> 

> [!NOTE]
> <span data-ttu-id="da561-233">諸如**匯出/匯入註冊**、**透過 API 存取遙測**等數種遙測相關功能僅適用於 Standard 階層。</span><span class="sxs-lookup"><span data-stu-id="da561-233">Several telemetry related features like **Export/Import Registrations**, **Telemetry Access via APIs** etc are only available in Standard tier.</span></span> <span data-ttu-id="da561-234">如果您嘗試 toouse 這些功能，如果您在免費層或基本層然後您會收到例外狀況訊息 toothis 效果時直接從 hello REST Api 中使用它們時使用 hello SDK 和 HTTP 403 （禁止）。</span><span class="sxs-lookup"><span data-stu-id="da561-234">If you attempt toouse these features if you are in Free or Basic tier then you will get exception message toothis effect while using hello SDK and an HTTP 403 (Forbidden) when using them directly from hello REST APIs.</span></span> <span data-ttu-id="da561-235">請確定您已透過 Azure 傳統入口網站移 tooStandard 階層。</span><span class="sxs-lookup"><span data-stu-id="da561-235">Make sure that you have moved up tooStandard tier via Azure Classic Portal.</span></span>  
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
[通知中樞概觀]: notification-hubs-push-notification-overview.md
[快速入門教學課程]: notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md
[範本指引]: https://msdn.microsoft.com/library/dn530748.aspx 
[APNS 指引]: https://developer.apple.com/library/ios/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/Chapters/ApplePushService.html#//apple_ref/doc/uid/TP40008194-CH100-SW4
[GCM 指引]: http://developer.android.com/google/gcm/adv.html
[Export/Import Registrations]: http://msdn.microsoft.com/library/dn790624.aspx
[服務匯流排總管]: http://msdn.microsoft.com/library/dn530751.aspx
[服務匯流排總管程式碼]: https://code.msdn.microsoft.com/windowsazure/Service-Bus-Explorer-f2abca5a
[VS 伺服器總管概觀]: http://msdn.microsoft.com/library/windows/apps/xaml/dn792122.aspx 
[VS 伺服器總管部落格文章 - 1]: http://azure.microsoft.com/blog/2014/04/09/deep-dive-visual-studio-2013-update-2-rc-and-azure-sdk-2-3/#NotificationHubs 
[VS 伺服器總管部落格文章 - 2]: http://azure.microsoft.com/blog/2014/08/04/announcing-release-of-visual-studio-2013-update-3-and-azure-sdk-2-4/ 
[EnableTestSend 功能]: http://msdn.microsoft.com/library/microsoft.servicebus.notifications.notificationhubclient.enabletestsend.aspx
[程式設計遙測存取]: http://msdn.microsoft.com/library/azure/dn458823.aspx
[透過 API 存取遙測範例]: https://github.com/Azure/azure-notificationhubs-samples/tree/master/FetchNHTelemetryInExcel

