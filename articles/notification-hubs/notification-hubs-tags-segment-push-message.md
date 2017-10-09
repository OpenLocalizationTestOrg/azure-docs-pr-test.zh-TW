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
# <a name="routing-and-tag-expressions"></a>路由與標記運算式
## <a name="overview"></a>概觀
標記運算式可讓您 tootarget 特定一組裝置或較特殊的註冊時傳送透過通知中樞推播通知。

## <a name="targeting-specific-registrations"></a>指定特定的註冊
hello 只方式 tootarget 特定通知註冊 tooassociate 標記，然後目標，這些標籤。 中所述[註冊管理](notification-hubs-push-notification-registration-management.md)，在訂單 tooreceive 推播通知的應用程式具有 tooregister 裝置處理通知中樞上。 一旦在通知中樞建立註冊之後，可以將推播通知 tooit 傳送 hello 應用程式後端。
hello 應用程式後端可以選擇特定通知的 hello 註冊 tootarget 中 hello 下列方法：

1. **廣播**: hello 通知中樞的所有註冊會都收到 hello 通知。
2. **標記**： 包含指定的 hello 的所有註冊標記讀取通知 hello。
3. **標記運算式**： 集標記比對的 hello 指定的運算式的所有註冊會都收到 hello 通知。

## <a name="tags"></a>標記
標記可以是任何字串，向上 too120 字元，包含英數字元且 hello 下列非英數字元: '_'、 ' @'，'#'、 '。 '、':'，'-'。 hello 下列範例示範您可以從中接收有關特定音樂群組的快顯通知的應用程式。 在此案例中，簡單的方式 tooroute 通知是 toolabel 註冊具有代表 hello 不同樂團，如 hello 下列圖片所示的標記。

![](./media/notification-hubs-routing-tag-expressions/notification-hubs-tags.png)

在此圖中，標記 hello 訊息**Beatles**到達只有 hello tablet 向 hello 標記**Beatles**。

如需為標記建立註冊的詳細資訊，請參閱 [註冊管理](notification-hubs-push-notification-registration-management.md)。

您可以將傳送通知 tootags 使用 hello 傳送通知方法的 hello`Microsoft.Azure.NotificationHubs.NotificationHubClient`類別中 hello [Microsoft Azure 通知中樞](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/)SDK。 您也可以使用 Node.js 或 hello 推播通知 REST Api。  以下是使用 hello SDK 範例。

    Microsoft.Azure.NotificationHubs.NotificationOutcome outcome = null;

    // Windows 8.1 / Windows Phone 8.1
    var toast = @"<toast><visual><binding template=""ToastText01""><text id=""1"">" +
    "You requested a Beatles notification</text></binding></visual></toast>";
    outcome = await Notifications.Instance.Hub.SendWindowsNativeNotificationAsync(toast, "Beatles");

    // Windows 10
    toast = @"<toast><visual><binding template=""ToastGeneric""><text id=""1"">" +
    "You requested a Wailers notification</text></binding></visual></toast>";
    outcome = await Notifications.Instance.Hub.SendWindowsNativeNotificationAsync(toast, "Wailers");




標記沒有 toobe 預先佈建，而且可以參考 toomultiple 應用程式專屬的概念。 比方說，此範例應用程式的使用者可以評論樂團，並想 tooreceive 快顯通知，不只對他們喜愛樂團，hello 註解，也包含來自朋友，不論在所在評論 hello 頻外的所有註解。 hello 下列圖片顯示這種情況的範例：

![](./media/notification-hubs-routing-tag-expressions/notification-hubs-tags2.png)

在此圖中，Alice 更新有興趣 hello Blackbird，而 Bob 興趣 hello Wailers 的更新。 Bob 也有興趣關注 Charlie 的評論，且 Charlie 對 wailers hello 有感興趣。 當通知傳送 hello Beatles 上關注 Charlie 的註解時，Alice 和 Bob 收到該通知。

雖然您可以在標記中編寫多項您所關注的事物 (例如 "band_Beatles" 或 "follows_Charlie")，標記仍屬於簡單字串，而不是具有屬性的值。 只能在 hello 存在特定的標記上時才符合註冊。

上如何 toouse 標記傳送 toointerest 群組的完整逐步教學課程，請參閱[即時新聞](notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md)。

## <a name="using-tags-tootarget-users"></a>使用標記 tootarget 使用者
另一個方式 toouse 標記是 tooidentify 特定使用者的所有 hello 裝置。 註冊可以加上標記，其中包含使用者識別碼，如 hello 下列圖片所示：

![](./media/notification-hubs-routing-tag-expressions/notification-hubs-tags3.png)

在此圖中，hello 訊息標記 alice 到達所有註冊標記的 alice;因此，所有的 Alice 的裝置。

## <a name="tag-expressions"></a>標記運算式
但是有些的狀況中，通知必須 tootarget 一組不是由單一標記，但在標記上的布林運算式所識別的註冊。

請考慮將有關隊 hello 紅襪隊和聖路易紅提醒 tooeveryone 波士頓中傳送一個運動應用程式。 如果 hello 用戶端應用程式註冊有關球隊和位置感興趣的標記，hello 通知應該是目標的 tooeveryone 波士頓中對 hello 紅襪隊或 hello 紅雀隊感興趣。 這種狀況可以以 hello 下列布林運算式表示：

    (follows_RedSox || follows_Cardinals) && location_Boston


![](./media/notification-hubs-routing-tag-expressions/notification-hubs-tags4.png)

標記運算式可以包含所有布林運算子，例如 AND (&&)、OR (||) 及 NOT (!)。 其也可包含括號。 標記運算式會限制的 too20 標籤它們只包含 Or; 如果否則，它們會限制的 too6 標記。

以下是用於傳送通知使用標記運算式使用 hello SDK 範例。

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
