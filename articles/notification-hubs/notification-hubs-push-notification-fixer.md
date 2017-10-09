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
# <a name="azure-notification-hubs---diagnosis-guidelines"></a>Azure 通知中樞 - 診斷指導方針
## <a name="overview"></a>概觀
Hello 最常見的問題，我們了解 Azure 通知中心客戶之一是 hello 用戶端在裝置上-toofigure 出為什麼會看到其應用程式後端傳送通知的顯示方式為何，通知已被卸除及如何 toofix 這。 本文章中我們將探討 hello 各種原因，通知可能取得卸除或不至於 hello 裝置上。 我們也會查看的方式可分析並找出 hello 根本原因。 

首先，它是關鍵 toounderstand Azure 通知中樞推播通知時通知 toohello 裝置。
![][0]

資料流程中的一般傳送通知，傳送 hello 訊息從 hello**應用程式後端**太**Azure 通知中樞 (NH)**其接著會納入所有 hello 註冊某些處理程序帳戶 hello 設定標記 （& s） 標記運算式 toodetermine 「 目標 」 也就是所有 hello 註冊需要 tooreceive hello 推播通知。 這些註冊可以跨越任何或所有我們支援的平台，包括 iOS、Google、Windows、Windows Phone、Kindle 及用於中國 Android 的百度。 NH 則推播通知，一旦建立 hello 目標，分成多個批次的註冊，toohello 裝置平台特定**推播通知服務 (PNS)** -例如 Apple 的 APNS、 GCM Google 等等。NH 向的 hello 個別 PNS 根據您在 hello 設定通知中樞 頁面上的 hello Azure 傳統入口網站中設定的 hello 認證。 hello PNS 接著會將轉送 hello 通知 toohello 個別**用戶端裝置**。 這是建議的方式 toodeliver 推播通知和通知傳送嗨最後階段所花費的 hello 平台 PNS 與 hello 裝置之間的附註的 hello 平台。 因此我們有四個主要元件 - *用戶端*、*應用程式後端*、*Azure 通知中樞 (NH)* 和*推播通知服務 (PNS)*，而且其中任何一項可能會導致通知遭到捨棄。 如需此架構的詳細資料，請參閱[通知中樞概觀]。

失敗 toodeliver 通知可能會在 hello 初始測試執行階段也可能表示組態問題或是它可能會發生在所有或部分的 hello 通知的生產環境中可能會遭捨棄指出某些更深入的應用程式或傳訊模式的問題。 在 [hello] 區段中下, 面我們將探討各種範圍可從通用 toohello 更少見種類，其中有些可能會發現明顯和其他一些不太多的已卸除的通知案例。 

## <a name="azure-notifications-hub-mis-configuration"></a>Azure 通知中樞組態錯誤
Azure 通知中樞需要 tooauthenticate 本身 hello 內容中的 hello 開發人員應用程式 toobe toosuccessfully 無法傳送通知 toohello 個別 PNS。 這樣做可能 hello 開發人員建立 hello 各平台 （Google、 Apple、 Windows 等等） 的開發人員帳戶，並再註冊他們的應用程式，他們會取得需要 toobe hello 入口網站，在 [通知] 中設定的認證中樞的組態區段。 如果沒有通知要進行到第一個步驟應該 tooensure hello 通知中樞，其比對 hello 應用程式中設定的 hello 正確的認證建立其平台特定的開發人員帳戶。 您會發現我們[快速入門教學課程]有用 toogo 透過此程序，以逐步方式。 以下是一些常見的組態錯誤：

1. **一般**
   
    a） 請確定您的通知中樞名稱 （不含錯字） 是 hello 相同：
   
   * 您要註冊從 hello 用戶端， 
   * 您要將通知傳送嗨後端中從  
   * 您已在其中設定 hello PNS 認證和 
   * 您已經設定的 SAS 認證 hello 用戶端與 hello 後端。 
     
     b） 請確定您使用正確 SAS 組態字串 hello hello 用戶端和 hello 應用程式後端上。 根據經驗法則，為您必須使用 hello **DefaultListenSharedAccessSignature** hello 用戶端上和**DefaultFullSharedAccessSignature** （它將提供權限 toobe hello 應用程式後端無法 toosend 通知 toohello NH)
2. **Apple Push Notification Service (APNS) 組態**
   
    您必須維護兩個不同的中樞，一個供生產環境之用，另一個供測試之用。 這表示您將要 toouse 沙箱環境 tooa 個別中樞和您要在實際執行 tooa 個別中樞 toouse hello 憑證中的 hello 憑證上傳。 請勿嘗試 tooupload 不同類型的憑證 toohello 相同的中樞，因為它可能會造成 hello 列關閉通知失敗。 如果您發現自己已不小心上載憑證 toohello 種不同的位置相同的中樞建議 toodelete hello 中樞和全新的開始。 如果基於某些原因，您不能 toodelete hello 集線器，然後在 hello 非常少，您必須刪除所有 hello 現有登錄從 hello 中樞。 
3. **Google 雲端通訊 (GCM) 組態** 
   
    a) 確認您在雲端專案下啟用的是 "Google Cloud Messaging for Android"。 
   
    ![][2]
   
    b） 請確定您建立 「 伺服器金鑰 」，而哪些 NH 取得 hello 認證與要使用 tooauthenticate GCM。 
   
    ![][3]
   
    c） 請確定您擁有 hello 用戶端，也就是您可以從 hello 儀表板取得完全數值實體上設定 「 專案識別碼 」:
   
    ![][1]

## <a name="application-issues"></a>應用程式問題
1) **標記/ 標記運算式**

如果您使用的標記或標記運算式 toosegment 您的對象，它仍然可以將傳送嗨通知時，沒有找到根據 hello 標記/標記運算式就您傳送的呼叫中指定任何目標。 建議您最好 tooreview 有您註冊 tooensure 標記的相符項目時您傳送通知，然後檢查 只能從 hello 與這些註冊的用戶端 hello 通知回條。 例如 如果 NH 與您註冊已完成所有說 「 政治"標記，而且您要傳送標記通知 」 運動"，它將不會傳送 tooany 裝置。 複雜的案例可能涉及只註冊 "Tag A" OR "Tag B" 的標記運算式，然而在傳送通知時，您設定的目標為 "Tag A && Tag B"。 Hello 自行診斷提示一節，您可以檢閱 hello 標籤它們擁有與您註冊的方式。 

2) **範本問題**

如果您使用範本則可確保您要遵照 hello 指導方針所述[範本指引]。 

3) **無效的註冊**

假設已正確設定通知中樞的 hello 和任何標記/標記運算式所使用的有效目標 toowhich hello 通知需要 toobe 傳送嗨尋找正確產生，以平行方式-每個批次的數個處理批次關閉引發 NH傳送訊息 tooa 登錄裝置集合。 

> [!NOTE]
> 因為我們不要 hello 以平行方式處理，我們不保證 hello 順序中的 hello 將傳遞通知。 
> 
> 

現在我們已根據「最多一次」訊息傳遞模式將 Azure 通知中樞最佳化。 這表示我們嘗試刪除重複作業，以便通知會傳遞一次以上 tooa 裝置。 tooensure 這我們查看 hello 註冊，並且確保該只能有一個訊息是每秒傳送的實際傳送 hello 訊息 toohello PNS 之前的裝置識別碼。 每個批次傳送 toohello PNS，接著會接受並驗證 hello 註冊，所以該 hello PNS 批次中偵測到與一或多個 hello 註冊錯誤時，會傳回錯誤 tooAzure NH 並停止處理，藉此卸除完整的批次。 對於使用 TCP 串流通訊協定的 APNS 來說，這種情況尤其顯著。 雖然我們一次最佳化在大部分的傳遞，在此情況下，我們會移除 hello 我們資料庫，然後重試通知傳送該批次中的 hello 裝置 hello 其餘部分從失敗的註冊。

您可以取得 hello 傳遞失敗的嘗試針對使用 Azure 通知中心 REST Api hello 註冊資訊時發生錯誤：[每個訊息遙測： 取得通知訊息遙測](https://msdn.microsoft.com/library/azure/mt608135.aspx)和[PNS 意見反應](https://msdn.microsoft.com/library/azure/mt705560.aspx). 請參閱 hello [SendRESTExample](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/SendRestExample)例如程式碼。

## <a name="pns-issues"></a>PNS 問題
一旦 hello 通知訊息已收到 hello 個別 PNS，則其責任 toodeliver hello 通知 toohello 裝置。 Azure 通知中樞超出 hello 的圖片且沒有控制權時，或如果 hello 通知將會傳遞 toohello 裝置 toobe。 Hello 平台通知服務都很穩定，因為通知不要從 hello PNS 就在幾秒鐘的時間通常 tooreach hello 裝置。 如果 hello PNS 不過正在進行節流然後 Azure 通知中心會套用指數型停止策略，如果 hello PNS 會保留 30 分鐘無法連線到然後我們有的原則中放置 tooexpire 且永久卸除這些訊息。 

如果 PNS 嘗試 toodeliver 通知，但 hello 裝置已離線，hello 通知是由 hello PNS 針對一段有限的時間，儲存和傳遞 toohello 裝置可供使用時。 PNS 只會針對每個應用程式儲存一則最近的通知。 如果多個通知會傳送 hello 裝置離線時，每個新的通知會導致捨棄 toobe hello 事先通知。 保持 hello 最新通知的這個行為是參照的 tooas 聯合中 APNS 通知和 GCM （這會使用摺疊的索引鍵） 在摺疊。 如果 hello 裝置長時間保持離線狀態，則會捨棄它所儲存的任何通知。 資料來源 - [APNS 指引] & [GCM 指引]

與 Azure 通知中心-您可以傳遞聯合的索引鍵，透過 HTTP 標頭使用 hello 泛型`SendNotification`應用程式開發介面 (例如 for.NET SDK – `SendNotificationAsync`) 這也會採用傳遞做為 HTTP 標頭是 toohello 個別 PNS。 

## <a name="self-diagnose-tips"></a>自我診斷秘訣
我們將在這裡檢視 hello 各種途徑 toodiagnose 和根會造成任何通知中樞的問題：

### <a name="verify-credentials"></a>驗證認證
1. **PNS 開發人員入口網站**
   
    確認它們在 hello 個別 PNS 開發人員入口網站 （APNS、 GCM，WNS 等等） 使用我們[快速入門教學課程]。
2. **Azure 傳統入口網站**
   
    Toohello 設定 索引標籤 tooreview 去符合 hello 認證與取自 hello PNS 開發人員入口網站。 
   
    ![][4]

### <a name="verify-registrations"></a>驗證註冊
1. **Visual Studio**
   
    如果您使用 Visual Studio 進行開發然後您可以連接 tooMicrosoft Azure 和檢視和管理 Azure 服務，包括來自 「 伺服器總管 」 的通知中樞的一大堆。 這能為您的開發/測試環境帶來許多助益。 
   
    ![][9]
   
    您可以檢視和管理所有 hello 註冊您的中樞中正確地切割分類平台、 原生模式或範本的註冊任何標記，PNS 識別碼、 註冊 id 和 hello 到期日。 您也可以編輯 hello 立即-這是假設如果您想 tooedit 任何標記時，才能註冊。 
   
    ![][8]
   
   > [!NOTE]
   > Visual Studio 功能 tooedit 註冊應該只用於開發/測試與有限數目的登錄期間。 如果那里，就會發生需要 toofix 您註冊大量，請考慮使用 hello 所描述的匯出/匯入登錄功能這裡-[匯出/匯入登錄](https://msdn.microsoft.com/library/dn790624.aspx)
   > 
   > 
2. **服務匯流排總管**
   
    有許多客戶使用 [服務匯流排總管] 所述的服務匯流排總管來檢視及管理通知中樞。 其為可從 code.microsoft.com - [服務匯流排總管程式碼]

### <a name="verify-message-notifications"></a>驗證訊息通知
1. **Azure 傳統入口網站**
   
    您可以移 toohello [偵錯] 索引標籤 toosend 測試通知 tooyour 用戶端，而不需要任何服務後端設定和執行。 
   
    ![][7]
2. **Visual Studio**
   
    您也可以從 Visual Studio 的 hello comforts 傳送測試通知：
   
    ![][10]
   
    您可以閱讀更多在 hello Visual Studio 通知中樞 Azure 總管的功能這裡 
   
   * [VS 伺服器總管概觀]
   * [VS 伺服器總管部落格文章 - 1]
   * [VS 伺服器總管部落格文章 - 2]

### <a name="debug-failed-notifications-review-notification-outcome"></a>偵錯失敗的通知 / 檢閱通知結果
**EnableTestSend 屬性**

當您傳送通知中樞通知時，一開始它只取得佇列中等待 NH toodo 處理 toofigure 出其所有的目標，然後最終 NH 傳送它 toohello PNS。 這表示，當您使用 REST API 或任何 hello client SDK，hello 成功傳回時為您傳送呼叫只表示 hello 訊息已成功排搭配通知中樞。 它不會讓您瞭解 NH 最後收到 toosend hello 訊息 tooPNS 時，發生了什麼事。 如果您的通知，則不抵達 hello 用戶端裝置，當 NH 嘗試 toodeliver hello 訊息 tooPNS，時發生錯誤，例如 hello 承載大小可能超過允許的 hello PNS 的 hello 上限或是設定 NH 中的 hello 認證是深入了解 hello PNS 錯誤的無效等 tooget，我們引進的屬性，稱為[EnableTestSend 功能]。 當您傳送測試訊息從 hello 入口網站或 Visual Studio 用戶端，並因此允許 toosee 詳細，這個屬性會自動啟用偵錯資訊。 您可以使用這透過採取 hello 範例 hello 都能立即.NET SDK 的 Api，將會加入的 tooall 用戶端 Sdk 最後。 toouse hello REST 呼叫，這只是附加結尾 hello 傳送呼叫中例如稱為 「 測試 」 的 querystring 參數 

    https://mynamespace.servicebus.windows.net/mynotificationhub/messages?api-version=2013-10&test

*範例 (.NET SDK)*

假設您使用.NET SDK toosend 原生快顯通知：

    NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString(connString, hubName);
    var result = await hub.SendWindowsNativeNotificationAsync(toast);
    Console.WriteLine(result.State);

`result.State`將只狀態`Enqueued`結尾 hello hello 執行不含任何深入了解什麼發生 tooyour 推入。 現在您可以使用 hello `EnableTestSend` hello 進行初始化時的布林值屬性`NotificationHubClient`，並可以取得有關傳送嗨通知時發生 hello PNS 錯誤的詳細的狀態。 需要額外的時間 tooreturn hello 傳送呼叫，因為它只會傳回 NH 已傳送嗨通知 tooPNS toodetermine hello 結果之後。 

    bool enableTestSend = true;
    NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString(connString, hubName, enableTestSend);

    var outcome = await hub.SendWindowsNativeNotificationAsync(toast);
    Console.WriteLine(outcome.State);

    foreach (RegistrationResult result in outcome.Results)
    {
        Console.WriteLine(result.ApplicationPlatform + "\n" + result.RegistrationId + "\n" + result.Outcome);
    }

*範例輸出*

    DetailedStateAvailable
    windows
    7619785862101227384-7840974832647865618-3
    hello Token obtained from hello Token Provider is wrong

此訊息表示 hello 通知中樞的設定不正確的認證或 hello 中樞和 hello hello 註冊發生問題的建議課程會 toodelete 此登錄，讓重新建立之前傳送嗨 hello 用戶端訊息。 

> [!NOTE]
> 請注意，hello 使用此屬性有很大節流處理，因此您必須只使用這組有限的註冊開發/測試環境中。 我們只會傳送偵錯通知 too10 裝置。 我們也會有處理每分鐘的偵錯傳送 toobe 10 的限制。 
> 
> 

### <a name="review-telemetry"></a>檢閱遙測
1. **使用 Azure 傳統入口網站**
   
    hello 入口網站可讓您 tooget 通知中樞上的所有 hello 活動的快速概觀。 
   
    a） 從 hello 」 儀表板 索引標籤中，您可以檢視 hello 註冊、 通知，以及每個平台錯誤的彙總的檢視。 
   
    ![][5]
   
    b） 您也可以從 hello 「 監視 」 索引標籤 tootake 更深入的探討，特別是在任何 PNS 特定的錯誤傳回 NH 嘗試 toosend hello 通知 toohello PNS 時加入許多其他平台特定的衡量標準。 
   
    ![][6]
   
    c） 您的開頭應檢閱 hello**內送訊息**，**註冊作業**，**成功通知**並前往 tooper 平台 索引標籤 tooreview helloPNS 特定錯誤。 
   
    d） 如果您擁有 hello 通知中樞的設定不正確使用 hello 驗證設定然後您會看到 PNS 驗證錯誤。 這是很好的指標 toocheck hello PNS 認證。 

2) **程式設計存取**

以下文章提供更多詳細資料： 

* [程式設計遙測存取]
* [透過 API 存取遙測範例] 

> [!NOTE]
> 諸如**匯出/匯入註冊**、**透過 API 存取遙測**等數種遙測相關功能僅適用於 Standard 階層。 如果您嘗試 toouse 這些功能，如果您在免費層或基本層然後您會收到例外狀況訊息 toothis 效果時直接從 hello REST Api 中使用它們時使用 hello SDK 和 HTTP 403 （禁止）。 請確定您已透過 Azure 傳統入口網站移 tooStandard 階層。  
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

