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
# <a name="azure-notification-hubs"></a>Azure 通知中心
## <a name="overview"></a>概觀
Azure 通知中樞提供方便使用、多平台、可相應放大的推播引擎。 透過單一跨平台 API 呼叫，您可以輕鬆地從任何雲端或內部部署的後端傳送目標及個人化的推播通知 tooany 行動平台。

通知中樞很適合企業和消費者案例。 以下是一些客戶使用通知中樞之用途的範例︰

* 傳送重大消息通知 toomillions 與低度延遲。
* 傳送以位置為基礎的優待券 toointerested 使用者區段。
* 傳送事件相關的通知 toousers 或群組的媒體/運動/finance/遊戲應用程式。
* 推送促銷內容 tooapps tooengage 和市場 toocustomers。
* 對使用者發送企業事件通知，例如新訊息和工作項目。
* 傳送 Multi-Factor Authentication 的程式碼。

## <a name="what-are-push-notifications"></a>什麼是推播通知？
推播通知是一種由應用程式對使用者發出的通訊形式，通常會以快顯視窗或對話方塊來對行動應用程式的使用者發出某些他們想要之資訊的通知。 使用者通常可以選擇 tooview 或關閉 hello 訊息，並選擇 hello 前者會開啟傳 hello 通知 hello 行動裝置應用程式。

推播通知是很重要的功能，對於消費者應用程式來說，可提高應用程式的參與和使用率，對於企業應用程式來說，則可傳送最新的企業資訊。 它是 hello 最佳應用程式對使用者的通訊，因為對應的應用程式都沒有作用時，它是能源的彈性 hello 通知寄件者和可用的行動裝置。

如需某些熱門平台的推播通知詳細資訊︰
* [iOS](https://developer.apple.com/notifications/)
* [Android](https://developer.android.com/guide/topics/ui/notifiers/notifications.html)
* [Windows](http://msdn.microsoft.com/library/windows/apps/hh779725.aspx)

## <a name="how-push-notifications-work"></a>推播通知的運作方式
推播通知可透過名為「平台通知系統 (PNS)」的平台特定基礎結構來傳遞。 它們提供 barebone 推播功能 toodelivery 訊息 tooa 裝置具有提供處理，且沒有通用介面。 toosend 通知 tooall 客戶跨 hello iOS、 Android 和 Windows 應用程式的版本中，hello 開發人員必須處理 APNS (Apple Push Notification Service)、 FCM (Firebase Cloud Messaging)，與 WNS （Windows 通知服務），同時批次處理會傳送 hello。

概括而言，以下是推播功能的運作方式︰

1. hello 用戶端應用程式會決定它想 tooreceive 推播通知因此連絡人 hello 對應 PNS tooretrieve 其唯一且暫時推送控制代碼。 hello 控制代碼類型取決於 hello 系統 （例如 WNS 有 Uri APNS 有語彙基元）。
2. hello 用戶端應用程式會將此控制代碼儲存在 hello 應用程式後端 」 或 「 提供者。
3. toosend 使用 hello PNS 處理 tootarget 特定用戶端應用程式的推播通知 hello 應用程式後端連絡人 hello。
4. hello PNS 轉送 hello 通知 toohello 裝置 hello 控制代碼所指定。

![][0]

## <a name="hello-challenges-of-push-notifications"></a>hello 的推播通知的挑戰
雖然 PNSes 強大，它們將保留在多工作 toohello 應用程式開發人員順序 tooimplement 甚至常見推播通知案例中，例如廣播或傳送推播通知 toosegmented 使用者。

推播是其中一個 hello 最常要求行動裝置的雲端服務的功能，因為它的工作需要複雜的基礎結構，是不相關的 toohello 應用程式的主要商務邏輯。 Hello 實際上挑戰的部分包括：

* **平台相依性**： 

  * hello 後端需要 toohave 複雜且困難維護平台相依邏輯 toosend 在各種平台上的通知 toodevices PNSes 將不一致。
* **調整**：

  * 根據 PNS 準則，在每次啟動應用程式時，都必須重新整理裝置權杖。 這表示 hello 後端處理大量的流量和資料庫存取只 tookeep hello 權杖保持最新狀態。 裝置 hello 數目成長 toohundreds 和無數百萬，建立並維護此基礎結構 hello 成本時，大量。
  * 大部分 PNSes 不支援廣播的 toomultiple 裝置。 這表示簡單的廣播的 tooa 百萬個呼叫 toohello PNSes 數百萬個裝置產生。 想要擴增這種數量的流量卻又要將延遲降到最低並非易事。
* **路由**：
  
  * 雖然 PNSes 方式 toosend 訊息 toodevices，大部分的應用程式通知的適用對象的使用者或利益群組。 這表示 hello 後端必須維護登錄 tooassociate 裝置與感興趣的群組、 使用者、 屬性等等。此項負擔會增加 toohello 階段 toomarket 和維護成本的應用程式。

## <a name="why-use-notification-hubs"></a>為何要使用通知中心？
通知中樞會消除所有與自行啟用推播相關聯的複雜工作。 其多平台、可相應放大的推播通知基礎結構可減少推播相關程式碼，並簡化您的後端。 與通知中樞的裝置是只負責註冊其 PNS 控制代碼集線器，雖然 hello 後端傳送訊息 toousers 或利益群組 hello 遵循圖所示：

![][1]

通知中心是您已備妥要使用推播引擎以 hello 下列優點：

* **跨平台**

  * 支援所有主要的推播平台，包括 iOS、Android、Windows、Kindle 和百度。
  * 通用介面 toopush tooall 平台特定平台上的任何平台專屬或平台無關的格式。
  * 集中在一個位置管理裝置控制代碼。
* **跨後端**
  
  * 雲端或內部部署
  * .NET、Node.js、Java 等
* **豐富的傳遞模式集**：

  * *廣播 tooone 或多個平台*： 您立即可以廣播 toomillions 裝置的跨平台，透過單一 API 呼叫。
  * *推播 toodevice*： 您可以通知 tooindividual 裝置為目標。
  * *推播 toouser*： 標記和範本的功能可協助您達成所有跨平台裝置的使用者。
  * *推送的動態標籤 toosegment*： 標記功能可協助您裝置分割並推送 toothem 根據 tooyour 需求，是否要傳送 tooone 區段或區段 （例如 active AND 生活同等程度不西雅圖新使用者） 的運算式。 而不是受限制的 toopub sub，您可以更新裝置的標記任何地方和任何時候。
  * *當地語系化的推播*︰範本功能可協助您實現當地語系化，又不影響後端程式碼。
  * *無訊息推入*： 您可以透過傳送無訊息的通知 toodevices 和觸發它們 toocomplete 啟用 hello 推入來提取模式，某些提取或動作。
  * *排程的推播*： 您可以隨時排程 toosend 通知。
  * *直接推送*： 您可以略過註冊裝置，與我們服務直接的裝置控制代碼的批次發送 tooa 清單。
  * *個人化推播*︰裝置推播變數可協助您以自訂的索引鍵/值組傳送裝置特定的個人化推播通知。
* **豐富的遙測**
  
  * 目前不提供 hello Azure 入口網站中一般的推播、 裝置、 錯誤和作業遙測和以程式設計的方式。
  * 每個訊息遙測追蹤每個推送您的初始要求呼叫 tooour 服務成功批次處理 hello 推播通知。
  * 平台通知系統意見反應通訊平台通知系統 tooassist 偵錯中的所有意見。
* **延展性** 
  
  * 傳送快速訊息 toomillions 個裝置，不重新架構或裝置的分區化。
* **安全性**

  * 共用存取密碼 (SAS) 或同盟驗證。

## <a name="integration-with-app-service-mobile-apps"></a>與 App Service Mobile Apps 整合
toofacilitate 順暢且統一的體驗，Azure 服務間[App Service Mobile App]具有內建支援，使用通知中樞推播通知。 [App Service Mobile App]企業開發人員和系統整合者可將一組豐富的功能帶 toomobile 開發人員提供可高度擴充、 全域可用的行動應用程式開發平台。

行動應用程式開發人員可以利用通知中樞，以下列工作流程的 hello:

1. 擷取裝置 PNS 控制代碼
2. 透過便利的 Mobile Apps Client SDK 註冊 API，使用通知中樞註冊裝置
   * 請注意，Mobile Apps 會基於安全性考量，去除註冊上的所有標籤。 搭配通知中樞從您的後端直接 tooassociate 標記與裝置。
3. 從 App 後端使用通知中樞傳送通知

以下是一些便利，回到 toodevelopers 與這項整合：

* **行動應用程式的用戶端 Sdk**： 這些多平台 Sdk 提供註冊的簡單應用程式開發介面和溝通 toohello 通知中樞與 hello 行動裝置應用程式會自動連結。 開發人員不需要透過通知中樞認證 toodig 作業，並與其他服務搭配使用。

  * *推播 toouser*: hello Sdk 自動標記 hello 給定裝置進行行動應用程式已驗證使用者識別碼 tooenable 發送 toouser 的案例。
  * *推播 toodevice*: hello Sdk 自動使用與通知中樞，節省開發人員維護多個服務 Guid hello 麻煩 GUID tooregister hello 行動應用程式的安裝識別碼。
* **安裝模型**： 搭配通知中樞的最新推入模型 toorepresent 所有推入內容中的推播通知服務與對齊且容易 toouse JSON 安裝的裝置相關聯的行動應用程式。
* **彈性**： 開發人員可以隨時甚至與 hello 整合通知中心直接與 toowork 備妥。
* **整合式體驗中的[Azure 入口網站]**： 推播一項功能會在行動裝置應用程式中以視覺化方式表示以及開發人員可以輕鬆地與行動應用程式透過 hello 關聯的通知中樞。

## <a name="next-steps"></a>後續步驟
您可以在以下主題找到「通知中樞」的詳細資訊：

* **[客戶如何使用通知中樞]**
* **[通知中樞教學課程和指南]**
* **通知中樞快速入門教學課程**：[iOS]、[Android]、[Windows Universal]、[Windows Phone]、[Kindle]、[Xamarin.iOS]、[Xamarin.Android]

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
