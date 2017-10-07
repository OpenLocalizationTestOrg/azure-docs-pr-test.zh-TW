---
title: "Azure 通知中樞：常見問題集 (FAQ) | Microsoft Docs"
description: "在通知中樞上設計/實作解決方案的常見問題集"
services: notification-hubs
documentationcenter: mobile
author: ysxu
manager: erikre
keywords: "推播通知, 推播通知, iOS 推播通知, android 推播通知, ios 推播, android 推播"
editor: 
ms.assetid: 7b385713-ef3b-4f01-8b1f-ffe3690bbd40
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: multiple
ms.topic: article
ms.date: 01/19/2017
ms.author: yuaxu
ms.openlocfilehash: a70efa7fc5954966847d5a173e9b10accf4b737e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="push-notifications-with-azure-notification-hubs-frequently-asked-questions"></a>使用 Azure 通知中樞推播通知：常見問題集 (FAQ)
## <a name="general"></a>一般
### <a name="what-is-hello-resource-structure-of-notification-hubs"></a>什麼是通知中樞的 hello 資源結構？

Azure 通知中樞有兩個資源層級：中樞和命名空間。 單次發送資源可以保存 hello 跨平台推送通知資訊的一個應用程式的中樞。 命名空間是一個區域中多個中樞的集合。

建議對應是一個應用程式搭配一個命名空間。 在命名空間內，您可以有一個生產中樞來與生產應用程式搭配運作，以及一個測試中樞來與測試應用程式搭配運作，依此類推。

### <a name="what-is-hello-price-model-for-notification-hubs"></a>通知中樞的 hello 價格模型是什麼？
hello 最新定價詳細資料位於 hello[通知中樞定價]頁面。 通知中心被計費 hello 命名空間層級。 （如需 hello 定義命名空間，請參閱 「 什麼是通知中樞的 hello 資源結構 」？）通知中心提供三個層級：

* **免費**：對探索推播功能來說，此層級是很好的起點。 但不建議用於生產應用程式。 每個月可取得 500 個裝置和 1 百萬個推播 (每個命名空間)，不包含服務等級協定 (SLA) 的保證。
* **基本**： 建議的較小的生產環境應用程式使用此層 （或 hello 標準層）。 每月可取得 200,000 個裝置和 1 千萬個推播 (以每個命名空間為基準)。 其中包含配額成長選項。
* **標準**： 這一層，建議您使用中型 toolarge 實際執行應用程式。 每月可取得 1 千萬個裝置和 1 千萬個推播 (以每個命名空間為基準)。 其中包含配額增加選項和豐富的遙測功能。

標準層級功能：
* **豐富型遙測**： 您可以使用每個訊息遙測通知中樞 tootrack 任何偵錯推播要求與平台通知系統意見反應。
* **多租用戶**：您可以在命名空間層級上使用平台通知系統認證。 此選項可讓您 tooeasily 分成中樞內 hello 租用戶相同的命名空間。
* **排程的推播**： 您可以排程通知 toobe anytime 送出。

### <a name="what-is-hello-notification-hubs-sla"></a>Hello 通知中樞的 SLA 是什麼？
基本和標準的通知中樞層已正確設定的應用程式可以傳送推播通知，或至少 99.9%的 hello 時間執行註冊管理作業。 深入了解 hello SLA、 移 toohello toolearn[通知中樞 SLA](https://azure.microsoft.com/support/legal/sla/notification-hubs/)頁面。

> [!NOTE]
> 推播通知相依於第三方平台通知系統 （例如 Apple APNS 和 Google FCM），因為沒有 SLA 保證 hello 傳送這些訊息。 通知中樞傳送嗨批次 tooPlatform 通知系統 (保證的 SLA) 之後，它是 hello 平台通知系統 toodeliver hello hello 責任推播通知 (不保證的 SLA)。

### <a name="which-customers-are-using-notification-hubs"></a>客戶如何使用通知中樞？
許多客戶都使用通知中樞。 此處列出一些值得注意的︰

* Sochi 2014︰兩周內有數百個感興趣的群組、3 百萬個以上的裝置和 1.5 億個以上的通知需進行分派。 [案例研究：Sochi]
* Skanska：[案例研究：Skanska]
* Seattle Times：[案例研究：Seattle Times]
* Mural.ly：[案例研究：Mural.ly]
* 7Digital：[案例研究：7Digital]
* Bing 應用程式：1 千萬部以上的裝置每日傳送 3 百萬則通知。

### <a name="how-do-i-upgrade-or-downgrade-my-hub-or-namespace-tooa-different-tier"></a>如何升級或降級我集線器或命名空間 tooa 不同的階層嗎？
移 toohello  **[Azure 入口網站]** > **通知中樞命名空間**或**通知中樞**。 選取您想 tooupdate，並跳過的 hello 資源**定價層**。 請注意下列需求的 hello:

* hello 定價層更新為適用於太*所有*hello 您正在使用的命名空間中的中樞。
* 如果裝置計數超過 hello 層限制的 hello 您正在降級至，您需要 toodelete 裝置之前，您將降級。


## <a name="design-and-development"></a>設計與開發
### <a name="which-server-side-platforms-do-you-support"></a>支援哪些伺服器端平台？
伺服器 SDK 適用於 .NET、Java、Node.js、PHP 和 Python。 通知中樞 API 是以 REST 介面為根據，因此如果您要使用不同平台或不想要額外的相依性，則可以直接使用 REST API。 如需詳細資訊，請移至 toohello[通知中心 REST Api]頁面。

### <a name="which-client-platforms-do-you-support"></a>支援哪些用戶端平台？
推播通知支援 [iOS](notification-hubs-ios-apple-push-notification-apns-get-started.md)、[Android](notification-hubs-android-push-notification-google-gcm-get-started.md)[Windows Universal](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md)[Windows Phone](notification-hubs-windows-mobile-push-notifications-mpns.md)[Kindle](notification-hubs-kindle-amazon-adm-push-notification.md)[Android China (由百度開發)](notification-hubs-baidu-china-android-notifications-get-started.md)、Xamarin ([iOS](xamarin-notification-hubs-ios-push-notification-apns-get-started.md)和 [Android](xamarin-notification-hubs-push-notifications-android-gcm.md))、[Chrome Apps](notification-hubs-chrome-push-notifications-get-started.md)和 [Safari](https://github.com/Azure/azure-notificationhubs-samples/tree/master/PushToSafari)。 如需詳細資訊，請移至 toohello[通知中心入門教學課程]頁面。

### <a name="do-you-support-text-message-email-or-web-notifications"></a>你們是否支援簡訊、電子郵件、或 Web 通知？
通知中心是主要是設計的 toosend 通知 toomobile 應用程式。 不提供電子郵件或簡訊功能。 不過，第三方平台提供這些功能可以與整合通知中心 toosend 原生推送通知使用[行動應用程式]。

通知中樞也不提供現成 hello 瀏覽器中的推播通知傳遞服務。 客戶可以實作這項功能使用 SignalR hello 支援伺服器端平台之上。 如果您想在 hello Chrome 沙箱 toosend 通知 toobrowser 應用程式，請參閱 hello [Chrome 應用程式教學課程]。

### <a name="how-are-mobile-apps-and-azure-notification-hubs-related-and-when-do-i-use-them"></a>Mobile Apps 和 Azure 通知中樞如何相關？以及何時使用這兩者？
如果您有現有行動回應用程式結束和您想 tooadd 只有 hello 功能 toosend 推播通知，您可以使用 Azure 通知中樞。 如果要 tooset 從頭您行動裝置應用程式後端，請考慮使用 hello Azure App Service 行動應用程式功能。 行動裝置應用程式會自動佈建通知中樞，以便您可以輕鬆地傳送推播通知從 hello 行動裝置應用程式後端。 行動應用程式的價格包含通知中樞的 hello 基本費。 您必須支付只有當您超出 hello 包含推播通知。 如需成本的詳細資訊，請移至 toohello[應用程式服務定價]頁面。

### <a name="how-many-devices-can-i-support-if-i-send-push-notifications-via-notification-hubs"></a>如果透過通知中樞傳送推播通知，可以支援多少個裝置？
請參閱 toohello[通知中樞定價]hello 支援的裝置數目的詳細資料頁面。

如果您需要支援超過 1 千萬個已註冊的裝置，請直接 [與我們連絡](https://azure.microsoft.com/overview/contact-us/) ，我們將協助您調整您的解決方案。

### <a name="how-many-push-notifications-can-i-send-out"></a>我可以傳送多少推播通知？
Hello 選取的階層，根據 Azure 通知中樞自動向上延展根據 hello 流經 hello 系統通知數目。

> [!NOTE]
> hello 整體使用量成本會增加根據提供的推播通知的 hello 數目。 確定您已經知道恪守 hello hello 層限制[通知中樞定價]頁面。
> 
> 

我們的客戶每日使用通知中樞 toosend 數百萬則的推播通知。 您沒有 toodo 特殊 tooscale hello 到達的推播通知，只要您使用 Azure 通知中樞的任何項目。

### <a name="how-long-does-it-take-for-sent-push-notifications-tooreach-my-device"></a>多久運作的 take 傳送推播通知 tooreach 我的裝置？
在一般使用案例中，其中是一致的 hello 連入負載而奇數，Azure 通知中心可以至少處理*1 百萬個推播通知會傳送一分鐘*。 此速率可能會因 hello 標記數目、 hello 本質傳入傳送嗨和其他外部因素而定。

Hello 預估的傳遞時間，在 hello 服務會計算每個平台的 hello 目標，並會路由傳送訊息 toohello 推播通知服務 (PNS) 根據 hello 註冊標記或標記運算式。 它負責 hello hello PNS toosend 通知 toohello 裝置。

hello PNS 傳遞通知，並不保證任何 SLA。 不過，大部分的推播通知傳遞 tootarget 裝置幾分鐘的時間 （通常是在 10 分鐘） 內從 hello tooNotification 中樞傳送的時間。 有些通知可能需要更多時間。

> [!NOTE]
> Azure 通知中樞原則中有位置 toodrop 未在 30 分鐘內傳遞 toohello PNS 任何推播通知。 多種原因，可能發生這種延遲，但大部分通常因為 hello PNS 節流處理您的應用程式。
> 
> 

### <a name="is-there-any-latency-guarantee"></a>是否有任何延遲保證？
基於 hello 本質的推播通知 （它們由外部的平台專屬的 PNS 傳遞），也不會延遲保證。 一般而言，幾分鐘的時間內傳送 hello 多數的推播通知。

### <a name="what-do-i-need-tooconsider-when-designing-a-solution-with-namespaces-and-notification-hubs"></a>怎麼設計與命名空間和通知中樞的解決方案時，我會需要 tooconsider？
#### <a name="mobile-appenvironment"></a>行動裝置應用程式/環境
* 每個環境的每個行動裝置應用程式都使用一個通知中樞。
* 在多租用戶案例中，每個租用戶都應該有個別的中樞。
* 永遠不會共用 hello 生產和測試環境中相同的通知中樞。 這種做法可能會在傳送通知時造成問題。 (Apple 提供「沙箱」與「生產推播」端點，而這兩者有個別的認證。)
* 根據預設，您可以傳送測試通知 tooyour 註冊裝置，透過 hello Azure 入口網站或 hello Visual Studio 中的 Azure 整合的元件。 hello 閾值設定 too10 從 hello 註冊集區中隨機選取的裝置。

> [!NOTE]
> 如果您的中樞最初設定與 Apple 沙箱憑證，然後被重新設定的 toouse Apple 生產憑證是無效的 hello 原始裝置權杖。 無效的語彙基元會導致 toofail 推播通知。 請將生產與測試環境分開，並針對不同的環境使用不同的中樞。
> 
> 

#### <a name="pns-credentials"></a>PNS 認證
當行動裝置應用程式透過平台的開發人員入口網站 (例如 Apple 或 Google) 進行註冊時，系統會傳送應用程式識別碼和安全性權杖。 hello 應用程式後端提供這些語彙基元 toohello 平台的 PNS 以便 toodevices 能傳送推播通知。 安全性權杖可以在 hello 形式的憑證 （例如，Apple iOS 或 Windows Phone） 」 或 「 安全金鑰 （例如，Google Android 或 Windows）。 並且必須在通知中樞加以設定。 組態通常是在 hello 通知中樞的層級，但也可以透過在多租用戶的案例中的 hello 命名空間層級。

#### <a name="namespaces"></a>命名空間
命名空間可以用於部署分組。 也可以使用的 toorepresent 所有租用戶的所有通知中樞 hello 相同的應用程式中的多租用戶的案例。

#### <a name="geo-distribution"></a>地理分散
在推播通知案例中，地理分散不一定是關鍵。 傳送推播通知 toodevices 的各種 PNSes （例如 APNS 或 GCM） 不是平均分佈。

如果您全域使用的應用程式，您可以建立不同的命名空間中集線器 hello 通知中心服務使用 hello 世界各地的不同 Azure 區域中。

> [!NOTE]
> 但我們不建議此安排，因為這會增加您的管理成本，特別是對註冊而言。 建議只在確實有此需求時這麼做。
> 
> 

### <a name="should-i-do-registrations-from-hello-app-back-end-or-directly-through-client-devices"></a>做登錄從 hello 應用程式後端，或直接透過用戶端裝置？
當您建立 hello 註冊之前有 tooauthenticate 用戶端，從 hello 應用程式後端註冊很有用。 它們也很有用時，必須建立或修改 hello 應用程式後端應用程式邏輯為基礎的標記。 如需詳細資訊，請移至 toohello[後端註冊指引]和[後端註冊指引 2]頁面。

### <a name="what-is-hello-push-notification-delivery-security-model"></a>Hello 推播通知傳遞安全性模型是什麼？
Azure 通知中樞使用[共用存取簽章](../storage/common/storage-dotnet-shared-access-signature-part-1.md) 型資訊安全模型。 在 hello 根命名空間層級或 hello 細微的通知中樞層級，您可以使用 hello 共用存取簽章權杖。 共用的存取簽章權杖可以設定 toofollow 不同授權規則，例如 toosend 訊息權限或 toolisten 通知權限。 如需詳細資訊，請參閱 hello[通知中心的安全性模型]文件。

### <a name="how-should-i-handle-sensitive-payload-in-push-notifications"></a>應如何處理推播通知中的機密承載？
所有通知會透過平台 hello PNS 都傳遞 tootarget 裝置。 當 tooAzure 通知中樞時，會傳送通知時，它會處理並傳遞 toohello 個別 PNS。

所有的連線，從 hello 寄件者 toohello Azure 通知中樞 toohello PNS，使用 HTTPS。

> [!NOTE]
> Azure 通知中心不會以任何方式記錄 hello 訊息裝載。
> 
> 

toosend 機密內容，我們建議使用的安全推入模式。 hello 寄件者與訊息識別項 toohello 裝置 hello 機密承載不傳遞 ping 通知。 當 hello hello 裝置上的應用程式收到 hello 的內容時，hello 應用程式會呼叫安全的應用程式開發介面直接 toofetch hello 訊息詳細資料。 在此模式 tooimplement 方式的指引，請移 toohello[集線器安全推播通知的教學課程]頁面。

## <a name="operations"></a>作業
### <a name="what-support-is-provided-for-disaster-recovery"></a>我可以得到哪些災害復原支援？
我們提供中繼資料損毀復原的涵蓋範圍，我們這一端 （hello 通知中樞名稱、 hello 連接字串和其他重要資訊）。 註冊資料觸發嚴重損壞修復案例時，為 hello*只區段*hello 通知中心基礎結構，將會遺失。 您需要 tooimplement 方案 toorepopulate 這項資料到新的中樞後復原：

1. 在不同的資料中心建立次要通知中樞。 我們建議您建立從 hello 開頭 tooshield 您從嚴重損壞修復事件可能會影響您的管理功能。 您也可以建立一個 hello 事件時間的 hello 災害復原。

2. 填入 hello 次要的通知中樞，以從您的主要的通知中樞的 hello 註冊。 我們不建議嘗試 toomaintain 這兩個集線器上的登錄裝置，並保持它們同步時有登錄。 這種做法不適用於的 hello PNS 端也因為 hello 註冊 tooexpire 的固有的趨勢。 當我們收到有關已到期或無效註冊的 PNS 回應時，通知中樞會將它們清除。  

我們有兩個應用程式後端的建議︰

* 使用在本身後端維護一組指定註冊的應用程式後端。 它接著可以執行大量插入到 hello 次要通知中心。

* 使用從 hello 主要的通知中樞，以當作備份取得規則的傾印的註冊應用程式後端。 它接著可以執行大量插入到 hello 次要通知中心。

> [!NOTE]
> 匯出/匯入登錄功能，適用於標準層次的 hello 述 hello[登錄匯出/匯入]文件。
> 
> 

如果您不需要後端，目標裝置上的 hello 應用程式啟動時，它們會執行 hello 次要的通知中樞的新註冊。 最終 hello 次要的通知中樞將會有所有 hello 作用中裝置已註冊。

但如果裝置上有未開啟的應用程式時，會有一段期間收不到通知。

### <a name="is-there-audit-log-capability"></a>是否有稽核記錄功能？
通知中樞的所有管理作業都移 toooperation 記錄檔，這樣會公開在 hello [Azure 傳統入口網站]。

## <a name="monitoring-and-troubleshooting"></a>監視與疑難排解
### <a name="what-troubleshooting-capabilities-are-available"></a>可用的疑難排解功能有哪些？
Azure 通知中樞提供許多功能進行疑難排解，特別是針對最常見的案例 hello 的已卸除的通知。 如需詳細資訊，請參閱 hello[通知中心疑難排解]技術白皮書。

### <a name="what-telemetry-features-are-available"></a>可用的遙測功能有哪些？
Azure 通知中樞啟用遙測資料檢視中 hello [Azure 傳統入口網站]。 Hello 度量的詳細資料位於 hello[通知中樞度量]頁面。

> [!NOTE]
> 成功通知只是表示推播通知，已傳遞 toohello 外部 PNS (例如，apple 的 APNS) 或 google 的 GCM。 它負責 hello hello PNS toodeliver hello 通知 tootarget 裝置。 一般而言，hello PNS 不會公開傳送度量 toothird 合作對象。  
> 
> 

我們也提供 hello 功能 tooexport hello 遙測資料，以程式設計方式 （hello 標準層）。 如需詳細資訊，請參閱 hello[通知中樞度量範例]。

[Azure 傳統入口網站]: https://manage.windowsazure.com
[通知中樞定價]: http://azure.microsoft.com/pricing/details/notification-hubs/
[Notification Hubs SLA]: http://azure.microsoft.com/support/legal/sla/
[案例研究：Sochi]: https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=7942
[案例研究：Skanska]: https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=5847
[案例研究：Seattle Times]: https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=8354
[案例研究：Mural.ly]: https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=11592
[案例研究：7Digital]: https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=3684
[通知中心 REST Api]: https://msdn.microsoft.com/library/azure/dn530746.aspx
[通知中心入門教學課程]: http://azure.microsoft.com/documentation/articles/notification-hubs-ios-get-started/
[Chrome 應用程式教學課程]: http://azure.microsoft.com/documentation/articles/notification-hubs-chrome-get-started/
[Mobile Services Pricing]: http://azure.microsoft.com/pricing/details/mobile-services/
[後端註冊指引]: https://msdn.microsoft.com/library/azure/dn743807.aspx
[後端註冊指引 2]: https://msdn.microsoft.com/library/azure/dn530747.aspx
[通知中心的安全性模型]: https://msdn.microsoft.com/library/azure/dn495373.aspx
[集線器安全推播通知的教學課程]: http://azure.microsoft.com/documentation/articles/notification-hubs-aspnet-backend-ios-secure-push/
[通知中心疑難排解]: http://azure.microsoft.com/documentation/articles/notification-hubs-diagnosing/
[通知中樞度量]: https://msdn.microsoft.com/library/dn458822.aspx
[通知中樞度量範例]: https://github.com/Azure/azure-notificationhubs-samples/tree/master/FetchNHTelemetryInExcel
[登錄匯出/匯入]: https://msdn.microsoft.com/library/dn790624.aspx
[Azure 入口網站]: https://portal.azure.com
[complete samples]: https://github.com/Azure/azure-notificationhubs-samples
[行動應用程式]: https://azure.microsoft.com/services/app-service/mobile/
[應用程式服務定價]: https://azure.microsoft.com/pricing/details/app-service/
