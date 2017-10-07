---
title: "aaaAzure Mobile Engagement 疑難排解指南"
description: "Azure Mobile Engagement 的疑難排解指南"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: 31134a29-a513-4e5e-b626-f6cf6fe04769
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: dd69bfd7019907c3e1da8df590db3b5f61606173
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-mobile-engagement---troubleshooting-guide"></a>Azure Mobile Engagement - 疑難排解指南
## <a name="introduction"></a>簡介
hello 疑難排解指南將協助您了解根本原因的一些常見的問題並且將可讓您自行 tootroubleshoot。 

## <a name="general"></a>一般
一般情況下，您一定要確定 hello 下列：

1. 請確定您已經完成中所述整合所需的所有 hello 步驟我們[快速入門教學課程](mobile-engagement-windows-store-dotnet-get-started.md)
2. 您使用 hello hello 平台 Sdk 的最新版本。 
3. 在實際裝置和模擬器上測試，因為有些問題是只有特定 tooemulator。 
4. 您並未達到 Mobile Engagement 的任何限制/節流，其相關內容記載在 [這裡](../azure-subscription-service-limits.md)
5. 如果您不能 tooconnect toohello Mobile Engagement 後端 」 或 「 不持續載入的資料服務，則請檢查確認沒有任何進行中的服務事件[這裡](https://azure.microsoft.com/status/)

## <a name="monitor-issues"></a>「監視」問題
### <a name="i-am-not-seeing-my-device-showing-up-on-hello-monitor-tab"></a>我沒有看到我的裝置 hello 監視] 索引標籤上顯示
監視索引標籤會顯示即時 hello 裝置連線的 tooyour Mobile Engagement 平台。 如果您正在模擬器和裝置上進行偵錯，您應該會在這裡看到至少一個工作階段。 如果已散發 hello 應用程式，您會看到 hello 量測計會反映 hello 裝置，也就是即時連線的 toohello 平台的作用中工作階段。 

如果看不到您的裝置 hello 監視] 索引標籤上，則可能 SDK 整合問題。 某些常見的步驟 tootake tootroubleshoot 如下所示：

1. 確定您使用 hello 正確的連接字串中的 hello 行動裝置應用程式，而且它是從 hello SDK 金鑰 > 一節和不 hello API 金鑰 > 一節。 hello 連接字串連接行動裝置應用程式 toohello hello Mobile Engagement 應用程式，您會看到您的裝置 hello 監視] 索引標籤的執行個體。 
2. 針對 Windows 平台-如果您的頁面會覆寫 hello`OnNavigatedTo`方法時，請確定 toocall `base.OnNavigatedTo(e)`。
3. 如果您要將 Mobile Engagement 整合到現有的行動裝置應用程式，則您也可以確保您沒有查看進階整合步驟的 hello 遺漏任何步驟[這裡](mobile-engagement-windows-store-integrate-engagement.md)
4. 請確定您要將一個以上的螢幕活動傳送藉由覆寫 hello 頁面與 EngagementActivity 取決於您正在 hello 中所述的 hello 平台[快速入門教學課程](mobile-engagement-windows-store-dotnet-get-started.md)。

### <a name="i-am-seeing-hello-monitor-tab-showing-a-session-even-when-i-have-disconnected-or-closed-my-app-emulator"></a>我看到 hello 監視] 索引標籤顯示在工作階段即使當我已中斷連接或關閉我的應用程式 / 模擬器。
如果您在此時是 hello 只能有一個連接的 toohello 平台，而且您使用模擬器 tooopen hello 應用程式這是可能的原因 tooemulator quirks。 一般情況下，您需要 tooensure，您回顧 hello 應用程式工作階段 toodisconnect 的 hello 模擬器上 toohello 首頁畫面成功。 此外，在 Windows 平台，使用 Visual Studio 中，偵錯時您可能需要在 Visual Studio 中，您會移 toohello tooensure**生命週期事件**功能表列並按一下**暫停**tooreally 關閉hello 工作階段。 如需詳細資訊，請參閱 [Windows 教學課程](mobile-engagement-windows-store-dotnet-get-started.md) 。 

## <a name="analytics-issues"></a>「分析」問題
### <a name="i-am-not-seeing-any-data-refreshed-data-on-analytics-tab"></a>我在 [分析] 索引標籤上看不到任何資料/重新整理的資料
[分析] 資料會定期重新計算，最多可能需要 24 小時才能完成此重新整理作業。 這並非即時資料，您會在 24 小時的期間內看到它進行重新整理。
請務必要確定然而您要使用的其中一個覆寫至少一頁傳送至少一個螢幕或活動 toohello 平台後端`EngagementActivity`或呼叫`SendActivity`explcitly。 

### <a name="i-am-seeing-incorrectly-captured-datetime-for-a-device-on-hello-analytics-tab"></a>Hello 分析] 索引標籤上看到不正確地擷取的日期/時間的裝置
hello Analytics 的時段根據 hello hello 使用者的裝置設定的日期。 因此請確定該 hello 裝置有 hello 日期設定正確。 

## <a name="segment-issues"></a>「區段」問題
### <a name="i-created-a-segment-and-it-is-showing-up-as-greyed-out-or-not-showing-any-data"></a>我建立了一個區段，但它呈現灰色或未顯示任何資料
區段建立 hello 當時不是即時。 它是在 hello 計算相同的時間為 hello 分析資料彙總，因此可能需要高達 24 小時。 您應該稍後再回來查看，但同時您也應該確定您的行動裝置應用程式，會確實傳送 hello 資料 hello 為基礎，其中您會形成 hello 區段。 例如 如果事件說出 'foo' 不所傳送的任何行動裝置，則不會有任何區段的資料區段建立的事件名稱，= foo hello 準則。 您也應該檢查您的 SDK 整合 tooensure 行動應用程式會正確地傳送 hello 資料。 

## <a name="reach-or-push-notifications-issues"></a>「送達」或推播通知問題
### <a name="my-push-messages-are-not-being-delivered"></a>我的推播訊息未傳遞
1. 請嘗試傳送通知 tooa 測試裝置第一次 tooensure 所有 hello 元件-行動裝置應用程式、 SDK 和 hello 服務都都已正確連接，而且要能 toodeliver 推播通知。 
2. 一律傳送 hello 簡單 '-應用程式通知' 第一次透過未排程的活動，或它有任何指定的受眾準則。 這是第一次通知連線正常運作的 tooprove。 
3. 如果您有中傳遞應用程式內通知，也會更佳的問題，第一步 tootry 先傳送出應用程式通知。 
4. 請確定該 hello 原生推送 ' 的行動應用程式已正確設定。 根據 hello 平台它可能會涉及 （Android、 Windows） 的金鑰或憑證 (iOS)。 請參閱 [使用者介面設定](mobile-engagement-user-interface-settings.md)
5. 不在 hello 可以也被封鎖通知的應用程式使用者透過 hello 行動裝置作業系統因此請確定這不是 hello 案例。 
6. 請確定您未設定 hello*忽略受眾，推入將會傳送 hello 應用程式開發介面透過 toousers*中 hello 選項**活動**> 一節的觸達活動，因為這樣可確保該推播通知無法只透過傳送應用程式開發介面。 
7. 請確定您要測試您的推播宣傳活動與透過 WIFI 和 phone 運算子網路 tooeliminate hello 網路連線問題的可能來源連接這兩個裝置。
8. 請確定該 hello 系統在您的裝置/模擬器上的日期/時間是否正確，因為任何同步的裝置也會干擾 hello 推播通知服務的能力 toodeliver 通知。 

以下有更多平台特有的疑難排解指示：

1. **iOS** 
   
   * 請確定 hello 憑證適用於 iOS 推播通知未到期且有效。 
   * 確定您有在 Mobile Engagement 應用程式中正確設定 [生產]  憑證。 
   * 請確定您要測試的是 *真正的實體裝置。* hello iOS 模擬器無法處理發送訊息。
   * 請確定該配套識別碼正確設定 hello 行動應用程式中的 hello。 請參閱 hello 指示[這裡](https://developer.apple.com/library/prerelease/ios/documentation/IDEs/Conceptual/AppDistributionGuide/AddingCapabilities/AddingCapabilities.html#//apple_ref/doc/uid/TP40012582-CH26-SW6)
   * 測試時，請使用行動佈建設定檔中的「臨機」發佈。 儘管使用 「 偵錯 」 進行編譯您的應用程式，您也不會無法 tooreceive 通知
2. **Android**
   
   * 請確認您指定正確的專案數目 hello \n 字元後面接著行動裝置應用程式的 AndroidManifest.xml 檔案中。 
     
           <meta-data android:name="engagement:gcm:sender" android:value="************\n" />
   * 請確認您沒有遺失或正確設定 hello Android 資訊清單檔案中的任何權限 
   * 請從您從哪裡取得 hello GCM 伺服器金鑰使用相同帳戶的 hello hello 您要加入 tooyour 用戶端應用程式的專案數目。 兩個 hello 之間任何不相符會防止您的推播通知送出。 
   * 如果您收到系統通知，但不是在應用程式然後檢閱 hello[指定圖示通知區段](mobile-engagement-android-get-started.md)為可能並不指定 hello 正確的圖示 hello Android 資訊清單檔案中。 
   * 如果您要傳送 BigPicture 通知，則確保，如果您有外部影像的伺服器，則他們需要 toobe 無法 toosupport HTTP"GET"和"HEAD"。
3. **Windows**
   
   * 確定您已使用有效的 Windows 市集應用程式關聯 hello 應用程式。 在 Visual Studio-您可以 tooright 按一下 hello 專案，然後選取 「 建立關聯的應用程式與存放區 」 選項，並選取 hello hello Windows 存放區中建立的應用程式。 這個 Windows 市集應用程式應該從其中您有 hello 原生推送認證 tooconfigure hello Mobile Engagement 入口網站中的 hello 同一個。
   * 如果有透過 `EngagementOverlay` 整合收到應用程式以外的推播通知，但未收到應用程式內通知，則請確定您的頁面中有根 Grid 元素。 EngagementOverlay 會使用在 xaml 檔案 tooadd 兩個 web 檢視上，您的網頁中找到 hello 第一個 「 方格 」 項目。 如果您想的 toolocate web 檢視設定的位置，您可以定義格線，像這樣名為"EngagementGrid"，但您將 tooensure 沒有足夠的高度和寬度為 hello 後續兩個 web 檢視會顯示 hello 通知並 hello 遵循為應用程式內通知的公告：
     
           <Grid x:Name="EngagementGrid"></Grid>

### <a name="i-created-a-push-notificationannouncement-campaign-and-even-after-it-sent-me-hello-notification-it-is-showing-as-active-what-does-it-mean"></a>我建立推播通知公告/的活動，而且即使它傳送給我 hello 通知之後，它會顯示為 'Active'。 這代表什麼意思？
hello**活動**您 Mobile Engagement 中建立會呼叫，因此當新裝置連線 tooyour 行動接洽平台，它會是長時間執行的推播通知意義，因為它們會自動傳送嗨通知您在此處設定，只要它們符合您設定在 hello 促銷活動中的 hello 準則。 這不是一次性的單一通知設定。 您必須按一下 hello toomanually**完成**按鈕 tooterminate hello 行銷活動，使它不會傳送通知。 

### <a name="i-created-a-push-campaign-and-i-am-receiving-notifications-successfully-however-whenever-i-open-up-hello-app-i-get-hello-same-notification-even-when-i-had-actioned-it-before"></a>我建立推播宣傳活動和我收到通知成功不過每當我開放 hello 應用程式時，我收到 hello 相同的通知，即使我已採取動作之前它嗎？
這是可能 toohappen 在測試期間，如果您使用模擬器或像是 TestFlight 某些測試架構。 這為什麼以下在每個應用程式中執行執行個體，它是取得新的 DeviceID，並將它傳送 tooour 後端，而使 hello Mobile Engagement 平台 tootreat 它做為新的裝置，以及傳送嗨通知。 

## <a name="getting-support"></a>取得支援
如果您無法 tooresolve hello 問題自行然後您可以：

1. 搜尋您的問題 hello StackOverflow 論壇上現有的執行緒和[MSDN 論壇](https://social.msdn.microsoft.com/Forums/windows/en-US/home?forum=azuremobileengagement)則不會再詢問那里問題。 
2. 如果您發現上遺漏然後加入/投票 hello 要求的功能我們[UserVoice 論壇](https://feedback.azure.com/forums/285737-mobile-engagement/)
3. 如果您有 Microsoft 支援開啟支援事件藉由提供下列詳細資料的 hello: 
   * Azure 訂用帳戶識別碼
   * 平台 (例如 iOS、Android 等)
   * 應用程式識別碼
   * 活動識別碼 (若為推播通知方面的問題)
   * 裝置識別碼
   * Mobile Engagement SDK 版本 (例如 Android SDK v2.1.0)
   * 附有確切錯誤訊息與狀況的錯誤詳細資料

