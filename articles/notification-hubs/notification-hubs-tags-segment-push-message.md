---
title: "aaaRouting 和標記運算式"
description: "本主題說明 Azure 通知中樞的路由與標記運算式。"
services: notification-hubs
documentationcenter: .net
author: ysxu
manager: erikre
editor: 
ms.assetid: 0fffb3bb-8ed8-4e0f-89e8-0de24a47f644
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: dotnet
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: c2c60500f7469f1cb1a73a5cf63c221a9ad6cbb4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="routing-and-tag-expressions"></a><span data-ttu-id="ebe90-103">路由與標記運算式</span><span class="sxs-lookup"><span data-stu-id="ebe90-103">Routing and tag expressions</span></span>
## <a name="overview"></a><span data-ttu-id="ebe90-104">概觀</span><span class="sxs-lookup"><span data-stu-id="ebe90-104">Overview</span></span>
<span data-ttu-id="ebe90-105">標記運算式可讓您 tootarget 特定一組裝置或較特殊的註冊時傳送透過通知中樞推播通知。</span><span class="sxs-lookup"><span data-stu-id="ebe90-105">Tag expressions enable you tootarget specific sets of devices, or more specifically registrations, when sending a push notification through Notification Hubs.</span></span>

## <a name="targeting-specific-registrations"></a><span data-ttu-id="ebe90-106">指定特定的註冊</span><span class="sxs-lookup"><span data-stu-id="ebe90-106">Targeting specific registrations</span></span>
<span data-ttu-id="ebe90-107">hello 只方式 tootarget 特定通知註冊 tooassociate 標記，然後目標，這些標籤。</span><span class="sxs-lookup"><span data-stu-id="ebe90-107">hello only way tootarget specific notification registrations is tooassociate tags with them, then target those tags.</span></span> <span data-ttu-id="ebe90-108">中所述[註冊管理](notification-hubs-push-notification-registration-management.md)，在訂單 tooreceive 推播通知的應用程式具有 tooregister 裝置處理通知中樞上。</span><span class="sxs-lookup"><span data-stu-id="ebe90-108">As discussed in [Registration Management](notification-hubs-push-notification-registration-management.md), in order tooreceive push notifications an app has tooregister a device handle on a notification hub.</span></span> <span data-ttu-id="ebe90-109">一旦在通知中樞建立註冊之後，可以將推播通知 tooit 傳送 hello 應用程式後端。</span><span class="sxs-lookup"><span data-stu-id="ebe90-109">Once a registration is created on a notification hub, hello application backend can send push notifications tooit.</span></span>
<span data-ttu-id="ebe90-110">hello 應用程式後端可以選擇特定通知的 hello 註冊 tootarget 中 hello 下列方法：</span><span class="sxs-lookup"><span data-stu-id="ebe90-110">hello application backend can choose hello registrations tootarget with a specific notification in hello following ways:</span></span>

1. <span data-ttu-id="ebe90-111">**廣播**: hello 通知中樞的所有註冊會都收到 hello 通知。</span><span class="sxs-lookup"><span data-stu-id="ebe90-111">**Broadcast**: all registrations in hello notification hub receive hello notification.</span></span>
2. <span data-ttu-id="ebe90-112">**標記**： 包含指定的 hello 的所有註冊標記讀取通知 hello。</span><span class="sxs-lookup"><span data-stu-id="ebe90-112">**Tag**: all registrations that contain hello specified tag receive hello notification.</span></span>
3. <span data-ttu-id="ebe90-113">**標記運算式**： 集標記比對的 hello 指定的運算式的所有註冊會都收到 hello 通知。</span><span class="sxs-lookup"><span data-stu-id="ebe90-113">**Tag expression**: all registrations whose set of tags match hello specified expression receive hello notification.</span></span>

## <a name="tags"></a><span data-ttu-id="ebe90-114">標記</span><span class="sxs-lookup"><span data-stu-id="ebe90-114">Tags</span></span>
<span data-ttu-id="ebe90-115">標記可以是任何字串，向上 too120 字元，包含英數字元且 hello 下列非英數字元: '_'、 ' @'，'#'、 '。 '、':'，'-'。</span><span class="sxs-lookup"><span data-stu-id="ebe90-115">A tag can be any string, up too120 characters, containing alphanumeric and hello following non-alphanumeric characters: ‘_’, ‘@’, ‘#’, ‘.’, ‘:’, ‘-’.</span></span> <span data-ttu-id="ebe90-116">hello 下列範例示範您可以從中接收有關特定音樂群組的快顯通知的應用程式。</span><span class="sxs-lookup"><span data-stu-id="ebe90-116">hello following example shows an application from which you can receive toast notifications about specific music groups.</span></span> <span data-ttu-id="ebe90-117">在此案例中，簡單的方式 tooroute 通知是 toolabel 註冊具有代表 hello 不同樂團，如 hello 下列圖片所示的標記。</span><span class="sxs-lookup"><span data-stu-id="ebe90-117">In this scenario, a simple way tooroute notifications is toolabel registrations with tags that represent hello different bands, as in hello following picture.</span></span>

![](./media/notification-hubs-routing-tag-expressions/notification-hubs-tags.png)

<span data-ttu-id="ebe90-118">在此圖中，標記 hello 訊息**Beatles**到達只有 hello tablet 向 hello 標記**Beatles**。</span><span class="sxs-lookup"><span data-stu-id="ebe90-118">In this picture, hello message tagged **Beatles** reaches only hello tablet that registered with hello tag **Beatles**.</span></span>

<span data-ttu-id="ebe90-119">如需為標記建立註冊的詳細資訊，請參閱 [註冊管理](notification-hubs-push-notification-registration-management.md)。</span><span class="sxs-lookup"><span data-stu-id="ebe90-119">For more information about creating registrations for tags, see [Registration Management](notification-hubs-push-notification-registration-management.md).</span></span>

<span data-ttu-id="ebe90-120">您可以將傳送通知 tootags 使用 hello 傳送通知方法的 hello`Microsoft.Azure.NotificationHubs.NotificationHubClient`類別中 hello [Microsoft Azure 通知中樞](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/)SDK。</span><span class="sxs-lookup"><span data-stu-id="ebe90-120">You can send notifications tootags using hello send notifications methods of hello `Microsoft.Azure.NotificationHubs.NotificationHubClient` class in hello [Microsoft Azure Notification Hubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) SDK.</span></span> <span data-ttu-id="ebe90-121">您也可以使用 Node.js 或 hello 推播通知 REST Api。</span><span class="sxs-lookup"><span data-stu-id="ebe90-121">You can also use Node.js, or hello Push Notifications REST APIs.</span></span>  <span data-ttu-id="ebe90-122">以下是使用 hello SDK 範例。</span><span class="sxs-lookup"><span data-stu-id="ebe90-122">Here's an example using hello SDK.</span></span>

    Microsoft.Azure.NotificationHubs.NotificationOutcome outcome = null;

    // Windows 8.1 / Windows Phone 8.1
    var toast = @"<toast><visual><binding template=""ToastText01""><text id=""1"">" +
    "You requested a Beatles notification</text></binding></visual></toast>";
    outcome = await Notifications.Instance.Hub.SendWindowsNativeNotificationAsync(toast, "Beatles");

    // Windows 10
    toast = @"<toast><visual><binding template=""ToastGeneric""><text id=""1"">" +
    "You requested a Wailers notification</text></binding></visual></toast>";
    outcome = await Notifications.Instance.Hub.SendWindowsNativeNotificationAsync(toast, "Wailers");




<span data-ttu-id="ebe90-123">標記沒有 toobe 預先佈建，而且可以參考 toomultiple 應用程式專屬的概念。</span><span class="sxs-lookup"><span data-stu-id="ebe90-123">Tags do not have toobe pre-provisioned and can refer toomultiple app-specific concepts.</span></span> <span data-ttu-id="ebe90-124">比方說，此範例應用程式的使用者可以評論樂團，並想 tooreceive 快顯通知，不只對他們喜愛樂團，hello 註解，也包含來自朋友，不論在所在評論 hello 頻外的所有註解。</span><span class="sxs-lookup"><span data-stu-id="ebe90-124">For example, users of this example application can comment on bands and want tooreceive toasts, not only for hello comments on their favorite bands, but also for all comments from their friends, regardless of hello band on which they are commenting.</span></span> <span data-ttu-id="ebe90-125">hello 下列圖片顯示這種情況的範例：</span><span class="sxs-lookup"><span data-stu-id="ebe90-125">hello following picture shows an example of this scenario:</span></span>

![](./media/notification-hubs-routing-tag-expressions/notification-hubs-tags2.png)

<span data-ttu-id="ebe90-126">在此圖中，Alice 更新有興趣 hello Blackbird，而 Bob 興趣 hello Wailers 的更新。</span><span class="sxs-lookup"><span data-stu-id="ebe90-126">In this picture, Alice is interested in updates for hello Beatles, and Bob is interested in updates for hello Wailers.</span></span> <span data-ttu-id="ebe90-127">Bob 也有興趣關注 Charlie 的評論，且 Charlie 對 wailers hello 有感興趣。</span><span class="sxs-lookup"><span data-stu-id="ebe90-127">Bob is also interested in Charlie’s comments, and Charlie is in interested in hello Wailers.</span></span> <span data-ttu-id="ebe90-128">當通知傳送 hello Beatles 上關注 Charlie 的註解時，Alice 和 Bob 收到該通知。</span><span class="sxs-lookup"><span data-stu-id="ebe90-128">When a notification is sent for Charlie’s comment on hello Beatles, both Alice and Bob receive it.</span></span>

<span data-ttu-id="ebe90-129">雖然您可以在標記中編寫多項您所關注的事物 (例如 "band_Beatles" 或 "follows_Charlie")，標記仍屬於簡單字串，而不是具有屬性的值。</span><span class="sxs-lookup"><span data-stu-id="ebe90-129">While you can encode multiple concerns in tags (for example, “band_Beatles” or “follows_Charlie”), tags are simple strings and not properties with values.</span></span> <span data-ttu-id="ebe90-130">只能在 hello 存在特定的標記上時才符合註冊。</span><span class="sxs-lookup"><span data-stu-id="ebe90-130">A registration is matched only on hello presence or absence of a specific tag.</span></span>

<span data-ttu-id="ebe90-131">上如何 toouse 標記傳送 toointerest 群組的完整逐步教學課程，請參閱[即時新聞](notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md)。</span><span class="sxs-lookup"><span data-stu-id="ebe90-131">For a full step-by-step tutorial on how toouse tags for sending toointerest groups, see [Breaking News](notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md).</span></span>

## <a name="using-tags-tootarget-users"></a><span data-ttu-id="ebe90-132">使用標記 tootarget 使用者</span><span class="sxs-lookup"><span data-stu-id="ebe90-132">Using tags tootarget users</span></span>
<span data-ttu-id="ebe90-133">另一個方式 toouse 標記是 tooidentify 特定使用者的所有 hello 裝置。</span><span class="sxs-lookup"><span data-stu-id="ebe90-133">Another way toouse tags is tooidentify all hello devices of a particular user.</span></span> <span data-ttu-id="ebe90-134">註冊可以加上標記，其中包含使用者識別碼，如 hello 下列圖片所示：</span><span class="sxs-lookup"><span data-stu-id="ebe90-134">Registrations can be tagged with a tag that contains a user id, as in hello following picture:</span></span>

![](./media/notification-hubs-routing-tag-expressions/notification-hubs-tags3.png)

<span data-ttu-id="ebe90-135">在此圖中，hello 訊息標記 alice 到達所有註冊標記的 alice;因此，所有的 Alice 的裝置。</span><span class="sxs-lookup"><span data-stu-id="ebe90-135">In this picture, hello message tagged uid:Alice reaches all registrations tagged uid:Alice; hence, all of Alice’s devices.</span></span>

## <a name="tag-expressions"></a><span data-ttu-id="ebe90-136">標記運算式</span><span class="sxs-lookup"><span data-stu-id="ebe90-136">Tag expressions</span></span>
<span data-ttu-id="ebe90-137">但是有些的狀況中，通知必須 tootarget 一組不是由單一標記，但在標記上的布林運算式所識別的註冊。</span><span class="sxs-lookup"><span data-stu-id="ebe90-137">There are cases in which a notification has tootarget a set of registrations that is identified not by a single tag, but by a Boolean expression on tags.</span></span>

<span data-ttu-id="ebe90-138">請考慮將有關隊 hello 紅襪隊和聖路易紅提醒 tooeveryone 波士頓中傳送一個運動應用程式。</span><span class="sxs-lookup"><span data-stu-id="ebe90-138">Consider a sports application that sends a reminder tooeveryone in Boston about a game between hello Red Sox and Cardinals.</span></span> <span data-ttu-id="ebe90-139">如果 hello 用戶端應用程式註冊有關球隊和位置感興趣的標記，hello 通知應該是目標的 tooeveryone 波士頓中對 hello 紅襪隊或 hello 紅雀隊感興趣。</span><span class="sxs-lookup"><span data-stu-id="ebe90-139">If hello client app registers tags about interest in teams and location, then hello notification should be targeted tooeveryone in Boston who is interested in either hello Red Sox or hello Cardinals.</span></span> <span data-ttu-id="ebe90-140">這種狀況可以以 hello 下列布林運算式表示：</span><span class="sxs-lookup"><span data-stu-id="ebe90-140">This condition can be expressed with hello following Boolean expression:</span></span>

    (follows_RedSox || follows_Cardinals) && location_Boston


![](./media/notification-hubs-routing-tag-expressions/notification-hubs-tags4.png)

<span data-ttu-id="ebe90-141">標記運算式可以包含所有布林運算子，例如 AND (&&)、OR (||) 及 NOT (!)。</span><span class="sxs-lookup"><span data-stu-id="ebe90-141">Tag expressions can contain all Boolean operators, such as AND (&&), OR (||), and NOT (!).</span></span> <span data-ttu-id="ebe90-142">其也可包含括號。</span><span class="sxs-lookup"><span data-stu-id="ebe90-142">They can also contain parentheses.</span></span> <span data-ttu-id="ebe90-143">標記運算式會限制的 too20 標籤它們只包含 Or; 如果否則，它們會限制的 too6 標記。</span><span class="sxs-lookup"><span data-stu-id="ebe90-143">Tag expressions are limited too20 tags if they contain only ORs; otherwise they are limited too6 tags.</span></span>

<span data-ttu-id="ebe90-144">以下是用於傳送通知使用標記運算式使用 hello SDK 範例。</span><span class="sxs-lookup"><span data-stu-id="ebe90-144">Here's an example for sending notifications with tag expressions using hello SDK.</span></span>

    Microsoft.Azure.NotificationHubs.NotificationOutcome outcome = null;

    String userTag = "(location_Boston && !follows_Cardinals)";    

    // Windows 8.1 / Windows Phone 8.1
    var toast = @"<toast><visual><binding template=""ToastText01""><text id=""1"">" +
    "You want info on hello Red Socks</text></binding></visual></toast>";
    outcome = await Notifications.Instance.Hub.SendWindowsNativeNotificationAsync(toast, userTag);

    // Windows 10
    toast = @"<toast><visual><binding template=""ToastGeneric""><text id=""1"">" +
    "You want info on hello Red Socks</text></binding></visual></toast>";
    outcome = await Notifications.Instance.Hub.SendWindowsNativeNotificationAsync(toast, userTag);
