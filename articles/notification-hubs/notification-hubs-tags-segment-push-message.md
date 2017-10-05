---
title: "路由與標記運算式"
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
ms.openlocfilehash: 18faa88641623e1248d6a33bc2d87099e1c9f624
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="routing-and-tag-expressions"></a><span data-ttu-id="2fa5f-103">路由與標記運算式</span><span class="sxs-lookup"><span data-stu-id="2fa5f-103">Routing and tag expressions</span></span>
## <a name="overview"></a><span data-ttu-id="2fa5f-104">概觀</span><span class="sxs-lookup"><span data-stu-id="2fa5f-104">Overview</span></span>
<span data-ttu-id="2fa5f-105">標記運算式可讓您在透過通知中樞傳送推播通知時，指定特定的目標裝置或更明確的註冊。</span><span class="sxs-lookup"><span data-stu-id="2fa5f-105">Tag expressions enable you to target specific sets of devices, or more specifically registrations, when sending a push notification through Notification Hubs.</span></span>

## <a name="targeting-specific-registrations"></a><span data-ttu-id="2fa5f-106">指定特定的註冊</span><span class="sxs-lookup"><span data-stu-id="2fa5f-106">Targeting specific registrations</span></span>
<span data-ttu-id="2fa5f-107">指定特定通知註冊的唯一方法，就是關聯標記與註冊，然後再指定這些標記。</span><span class="sxs-lookup"><span data-stu-id="2fa5f-107">The only way to target specific notification registrations is to associate tags with them, then target those tags.</span></span> <span data-ttu-id="2fa5f-108">一如 [註冊管理](notification-hubs-push-notification-registration-management.md)中所述，若要接收推播通知，應用程式必須向通知中樞註冊裝置。</span><span class="sxs-lookup"><span data-stu-id="2fa5f-108">As discussed in [Registration Management](notification-hubs-push-notification-registration-management.md), in order to receive push notifications an app has to register a device handle on a notification hub.</span></span> <span data-ttu-id="2fa5f-109">當在通知中樞建立註冊之後，應用程式後端便能傳送推播通知。</span><span class="sxs-lookup"><span data-stu-id="2fa5f-109">Once a registration is created on a notification hub, the application backend can send push notifications to it.</span></span>
<span data-ttu-id="2fa5f-110">應用程式後端可以下列方式，選擇特定通知的目標註冊：</span><span class="sxs-lookup"><span data-stu-id="2fa5f-110">The application backend can choose the registrations to target with a specific notification in the following ways:</span></span>

1. <span data-ttu-id="2fa5f-111">**廣播**：通知中樞中的所有註冊都會收到通知。</span><span class="sxs-lookup"><span data-stu-id="2fa5f-111">**Broadcast**: all registrations in the notification hub receive the notification.</span></span>
2. <span data-ttu-id="2fa5f-112">**標記**：所有包含指定標記的註冊都會收到通知。</span><span class="sxs-lookup"><span data-stu-id="2fa5f-112">**Tag**: all registrations that contain the specified tag receive the notification.</span></span>
3. <span data-ttu-id="2fa5f-113">**標記運算式**：所有標記設定符合指定運算式的註冊都會收到通知。</span><span class="sxs-lookup"><span data-stu-id="2fa5f-113">**Tag expression**: all registrations whose set of tags match the specified expression receive the notification.</span></span>

## <a name="tags"></a><span data-ttu-id="2fa5f-114">標記</span><span class="sxs-lookup"><span data-stu-id="2fa5f-114">Tags</span></span>
<span data-ttu-id="2fa5f-115">標記可以是任何字串，最多 120 個字元，包含英數字元以及下列非英數字元: '_'、 ' @'，'#'、 '。 '、':'，'-'。</span><span class="sxs-lookup"><span data-stu-id="2fa5f-115">A tag can be any string, up to 120 characters, containing alphanumeric and the following non-alphanumeric characters: ‘_’, ‘@’, ‘#’, ‘.’, ‘:’, ‘-’.</span></span> <span data-ttu-id="2fa5f-116">下列範例示範的應用程式可以讓您從中接收有關特定音樂群組的快顯通知。</span><span class="sxs-lookup"><span data-stu-id="2fa5f-116">The following example shows an application from which you can receive toast notifications about specific music groups.</span></span> <span data-ttu-id="2fa5f-117">在此案例中，一個簡單路由通知的方法是為註冊加上標記，以指出不同的樂團，如下列圖片所示。</span><span class="sxs-lookup"><span data-stu-id="2fa5f-117">In this scenario, a simple way to route notifications is to label registrations with tags that represent the different bands, as in the following picture.</span></span>

![](./media/notification-hubs-routing-tag-expressions/notification-hubs-tags.png)

<span data-ttu-id="2fa5f-118">在此圖片中，標記 **Beatles** 的訊息只會傳送到標記 **Beatles** 的平板電腦。</span><span class="sxs-lookup"><span data-stu-id="2fa5f-118">In this picture, the message tagged **Beatles** reaches only the tablet that registered with the tag **Beatles**.</span></span>

<span data-ttu-id="2fa5f-119">如需為標記建立註冊的詳細資訊，請參閱 [註冊管理](notification-hubs-push-notification-registration-management.md)。</span><span class="sxs-lookup"><span data-stu-id="2fa5f-119">For more information about creating registrations for tags, see [Registration Management](notification-hubs-push-notification-registration-management.md).</span></span>

<span data-ttu-id="2fa5f-120">您可以使用將通知傳送給 [Microsoft Azure 通知中樞](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) SDK 中之 `Microsoft.Azure.NotificationHubs.NotificationHubClient` 類別的方法，將通知傳送給標記。</span><span class="sxs-lookup"><span data-stu-id="2fa5f-120">You can send notifications to tags using the send notifications methods of the `Microsoft.Azure.NotificationHubs.NotificationHubClient` class in the [Microsoft Azure Notification Hubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) SDK.</span></span> <span data-ttu-id="2fa5f-121">您也可以使用 Node.js 或推播通知 REST API。</span><span class="sxs-lookup"><span data-stu-id="2fa5f-121">You can also use Node.js, or the Push Notifications REST APIs.</span></span>  <span data-ttu-id="2fa5f-122">以下是 SDK 的使用範例。</span><span class="sxs-lookup"><span data-stu-id="2fa5f-122">Here's an example using the SDK.</span></span>

    Microsoft.Azure.NotificationHubs.NotificationOutcome outcome = null;

    // Windows 8.1 / Windows Phone 8.1
    var toast = @"<toast><visual><binding template=""ToastText01""><text id=""1"">" +
    "You requested a Beatles notification</text></binding></visual></toast>";
    outcome = await Notifications.Instance.Hub.SendWindowsNativeNotificationAsync(toast, "Beatles");

    // Windows 10
    toast = @"<toast><visual><binding template=""ToastGeneric""><text id=""1"">" +
    "You requested a Wailers notification</text></binding></visual></toast>";
    outcome = await Notifications.Instance.Hub.SendWindowsNativeNotificationAsync(toast, "Wailers");




<span data-ttu-id="2fa5f-123">標記無須事先佈建，而且可以參考多個應用程式特有的概念。</span><span class="sxs-lookup"><span data-stu-id="2fa5f-123">Tags do not have to be pre-provisioned and can refer to multiple app-specific concepts.</span></span> <span data-ttu-id="2fa5f-124">例如，此範例應用程式的使用者可能想要對所有樂團發表評論，但不想只收到他們評論及喜愛之樂團的快顯通知，也想要收到來自他們朋友之所有評論的快顯通知。</span><span class="sxs-lookup"><span data-stu-id="2fa5f-124">For example, users of this example application can comment on bands and want to receive toasts, not only for the comments on their favorite bands, but also for all comments from their friends, regardless of the band on which they are commenting.</span></span> <span data-ttu-id="2fa5f-125">下圖顯示此案例的範例：</span><span class="sxs-lookup"><span data-stu-id="2fa5f-125">The following picture shows an example of this scenario:</span></span>

![](./media/notification-hubs-routing-tag-expressions/notification-hubs-tags2.png)

<span data-ttu-id="2fa5f-126">在此圖片中，Alice 關注的是 Beatles 的最新動態，Bob 關注的是 Wailers 的最新動態。</span><span class="sxs-lookup"><span data-stu-id="2fa5f-126">In this picture, Alice is interested in updates for the Beatles, and Bob is interested in updates for the Wailers.</span></span> <span data-ttu-id="2fa5f-127">Bob 也會關注 Charlie 的評論，而 Charlie 則會關注 Wailers。</span><span class="sxs-lookup"><span data-stu-id="2fa5f-127">Bob is also interested in Charlie’s comments, and Charlie is in interested in the Wailers.</span></span> <span data-ttu-id="2fa5f-128">當 Charlie 對 Beatles 發表評論時，Alice 與 Bob 都會收到該通知。</span><span class="sxs-lookup"><span data-stu-id="2fa5f-128">When a notification is sent for Charlie’s comment on the Beatles, both Alice and Bob receive it.</span></span>

<span data-ttu-id="2fa5f-129">雖然您可以在標記中編寫多項您所關注的事物 (例如 "band_Beatles" 或 "follows_Charlie")，標記仍屬於簡單字串，而不是具有屬性的值。</span><span class="sxs-lookup"><span data-stu-id="2fa5f-129">While you can encode multiple concerns in tags (for example, “band_Beatles” or “follows_Charlie”), tags are simple strings and not properties with values.</span></span> <span data-ttu-id="2fa5f-130">只有在指定有特定標記或未指定特定標記時，才會比對註冊。</span><span class="sxs-lookup"><span data-stu-id="2fa5f-130">A registration is matched only on the presence or absence of a specific tag.</span></span>

<span data-ttu-id="2fa5f-131">如何使用標記傳送到您所關注之群組的完整逐步教學課程，請參閱 [即時新聞](notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md)。</span><span class="sxs-lookup"><span data-stu-id="2fa5f-131">For a full step-by-step tutorial on how to use tags for sending to interest groups, see [Breaking News](notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md).</span></span>

## <a name="using-tags-to-target-users"></a><span data-ttu-id="2fa5f-132">使用標記指定使用者</span><span class="sxs-lookup"><span data-stu-id="2fa5f-132">Using tags to target users</span></span>
<span data-ttu-id="2fa5f-133">另一種使用標記的方法，是指定特定使用者的所有裝置。</span><span class="sxs-lookup"><span data-stu-id="2fa5f-133">Another way to use tags is to identify all the devices of a particular user.</span></span> <span data-ttu-id="2fa5f-134">註冊可以加上包含使用者識別碼的特殊標記，如圖所示：</span><span class="sxs-lookup"><span data-stu-id="2fa5f-134">Registrations can be tagged with a tag that contains a user id, as in the following picture:</span></span>

![](./media/notification-hubs-routing-tag-expressions/notification-hubs-tags3.png)

<span data-ttu-id="2fa5f-135">在此圖片中，標記 uid:Alice 的訊息會傳送給所有標記 uid:Alice 的註冊，也就是 Alice 的所有裝置。</span><span class="sxs-lookup"><span data-stu-id="2fa5f-135">In this picture, the message tagged uid:Alice reaches all registrations tagged uid:Alice; hence, all of Alice’s devices.</span></span>

## <a name="tag-expressions"></a><span data-ttu-id="2fa5f-136">標記運算式</span><span class="sxs-lookup"><span data-stu-id="2fa5f-136">Tag expressions</span></span>
<span data-ttu-id="2fa5f-137">在有些情況下，通知的目標是一組註冊，而這些註冊又不是以單一標記識別，而須透過標記上的布林運算式。</span><span class="sxs-lookup"><span data-stu-id="2fa5f-137">There are cases in which a notification has to target a set of registrations that is identified not by a single tag, but by a Boolean expression on tags.</span></span>

<span data-ttu-id="2fa5f-138">假設有一支運動應用程式會將提醒傳送給波士頓的每個人，告知他們有關於紅襪隊與紅雀隊之間的賽事訊息。</span><span class="sxs-lookup"><span data-stu-id="2fa5f-138">Consider a sports application that sends a reminder to everyone in Boston about a game between the Red Sox and Cardinals.</span></span> <span data-ttu-id="2fa5f-139">若用戶端應用程式註冊關於球隊與地點的標記，則通知的目標應為波士頓中位關注紅襪隊或紅雀隊的每個人。</span><span class="sxs-lookup"><span data-stu-id="2fa5f-139">If the client app registers tags about interest in teams and location, then the notification should be targeted to everyone in Boston who is interested in either the Red Sox or the Cardinals.</span></span> <span data-ttu-id="2fa5f-140">此條件可以下列布林運算式表示：</span><span class="sxs-lookup"><span data-stu-id="2fa5f-140">This condition can be expressed with the following Boolean expression:</span></span>

    (follows_RedSox || follows_Cardinals) && location_Boston


![](./media/notification-hubs-routing-tag-expressions/notification-hubs-tags4.png)

<span data-ttu-id="2fa5f-141">標記運算式可以包含所有布林運算子，例如 AND (&&)、OR (||) 及 NOT (!)。</span><span class="sxs-lookup"><span data-stu-id="2fa5f-141">Tag expressions can contain all Boolean operators, such as AND (&&), OR (||), and NOT (!).</span></span> <span data-ttu-id="2fa5f-142">其也可包含括號。</span><span class="sxs-lookup"><span data-stu-id="2fa5f-142">They can also contain parentheses.</span></span> <span data-ttu-id="2fa5f-143">標記運算式若只含 OR，最多可有 20 個標記，否則只可有 6 個標記。</span><span class="sxs-lookup"><span data-stu-id="2fa5f-143">Tag expressions are limited to 20 tags if they contain only ORs; otherwise they are limited to 6 tags.</span></span>

<span data-ttu-id="2fa5f-144">以下是使用 SDK 傳送採用標記運算式之通知的範例。</span><span class="sxs-lookup"><span data-stu-id="2fa5f-144">Here's an example for sending notifications with tag expressions using the SDK.</span></span>

    Microsoft.Azure.NotificationHubs.NotificationOutcome outcome = null;

    String userTag = "(location_Boston && !follows_Cardinals)";    

    // Windows 8.1 / Windows Phone 8.1
    var toast = @"<toast><visual><binding template=""ToastText01""><text id=""1"">" +
    "You want info on the Red Socks</text></binding></visual></toast>";
    outcome = await Notifications.Instance.Hub.SendWindowsNativeNotificationAsync(toast, userTag);

    // Windows 10
    toast = @"<toast><visual><binding template=""ToastGeneric""><text id=""1"">" +
    "You want info on the Red Socks</text></binding></visual></toast>";
    outcome = await Notifications.Instance.Hub.SendWindowsNativeNotificationAsync(toast, userTag);
