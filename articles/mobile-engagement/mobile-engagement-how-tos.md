---
title: "aaaAzure Mobile Engagement 使用者介面為連線到 How To"
description: "Azure Mobile Engagement 的使用者介面概觀"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: 30af87e6-c816-4cce-8609-6cbd3e83de14
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 4b6dafd09d894214d4c386f5c6f157a77671606f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooget-started-using-and-managing-pushes-tooreach-out-tooyour-end-users"></a>如何 tooget 開始使用，並管理推播通知 tooreach 出 tooyour 使用者
一旦 hello SDK 已完全整合到您的應用程式，您可以開始使用 hello hello 觸達區段 hello UI tooPush 通知 toohello 使用者應用程式。  

## <a name="do-your-first-push-notification-campaign"></a>進行第一個推送通知活動
* 確認您的範圍已整合到應用程式與 hello SDK。 
* 選取您的應用程式

![First1][1]

* 移 toohello 「 觸達 」 區段，然後按一下 「 新的通知 」

![First2][2]

* 建立新的活動並將它命名
  
![First3][3]

* 選取如何 hello 應傳送通知，在應用程式只為

![First4][4]

* 建立您想要 toopush hello 訊息

![First5][5]

* 您可以撰寫一個標題 hello 通知 （選擇性）。
* 撰寫推送訊息內容。
* 您可以上傳影像。 請注意 hello hello 檔案大小不能超過 32,768 位元組。
* 您也可以 hello 能力 tooselect，取得進一步的選項，但 hello 焦點在這個教學課程，我們會看到更新版本。
* 只選取當做通知的 hello 內容類型

![First6][6]

* 建立推送活動，它會顯示在活動清單。

![First7][7]

## <a name="test-your-push-notification-campaign"></a>測試推送通知活動
![Test1][8]

* 登記裝置。
* 按一下您想 toopush 的 hello 裝置 hello 核取方塊。
* 按一下 hello 「 測試 」 按鈕 toosend hello 發送 toohello 裝置。

![Test2][9]

* 啟動 hello 活動

![Test3][10]

* 既然您已建立您的活動只需要 tooactivate 為 hello 通知 toobe 推入 tooyour 使用者。

## <a name="send-personalized-pushes"></a>傳送個人化的推送
* 這個範例會建立的發送 rebate 自訂程式碼輸入 hello 推播通知的位置。

![Personalize1][11]

個人化運作方式是取代從應用程式資訊標記所標記，因此，您必須確定 hello 使用者擁有 hello 適當應用程式資訊先定義 toomake。 在此範例 hello 目標的使用者都會將名為 rebate_code 定義的應用程式資訊標記。
您看到上述 hello 推播通知內容包括 hello 標記 ${rebate_code} 表示它是 toobe hello 應用程式資訊標記 hello 實際內容所取代。

> [!WARNING]
> Hello 應用程式資訊標記未定義 hello 使用者時，如果 hello 使用者不會收到 hello 推入。

* 結果

![Personalize2][12]

### <a name="you-can-further-personalize-hello-text-your-notification"></a>您可以進一步個人化的 hello 文字通知
![Personalize3][13]

* 包括 hello 通知的 hello 標題
* 和 hello hello 訊息的內容。
* 選擇 hello 公告 （文字檢視或 Web 檢視） 類型

![Personalize4][14]

### <a name="hello-body-of-an-announcement-may-also-be-personalized-with"></a>hello 公告主體也可能會與個人化：
* hello 動作 URL，您應該要 toocustomize hello 登陸頁面
* hello 標題
* hello hello 訊息本文。

## <a name="differentiate-your-push-notification-in-or-out-of-app"></a>區分您的推送通知 (在應用程式內外)
* 選擇 hello 類型的通知，您將推播選取您的應用程式、 toohello 「 觸達 」 一節中，選取或建立推播宣傳活動，請移 toohello 「 通知 」 一節。
* 按一下您想在 hello 「 傳遞模式 」。
* 按一下的 hello 當您想要 hello 通知的 「 限制的活動 」 核取方塊，就會發生在特定活動 （螢幕）。

![Differentiate1][15]

### <a name="out-of-app-only-delivery-mode"></a>「僅限應用程式外」傳遞模式
![Differentiate2][16]

「 不足應用程式只"hello 應用程式關閉時，傳遞模式提供推播通知。 這是 hello 標準的推播通知。
當您選取 「 不足只應用程式 」 時，您必須已提供 hello hello 平台建置您的應用程式 （APNS 或 GCM） 上的憑證。

### <a name="see-also"></a>另請參閱
* [Apple Push Notification Service – 憑證](http://developer.apple.com/library/mac/#documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/ApplePushService/ApplePushService.html#//apple_ref/doc/uid/TP40008194-CH100-SW9)、[Google 雲端通訊 – 憑證](http://developer.android.com/google/gcm/index.html) 

### <a name="in-app-only-delivery-mode"></a>「僅限應用程式內」傳遞模式
![Differentiate3][17]

Hello 應用程式執行時，「 應用程式內只"傳遞模式提供推播通知。
這項通知，您不需要透過 hello APNS toogo 和 GCM 系統。
您可以使用 hello 應用程式內傳遞系統 tooreach 您的使用者。
您完全可以自訂 hello 通知，並且決定 hello 通知會出現在哪一個活動 （螢幕）。

### <a name="anytime-delivery-mode"></a>「隨時」傳遞模式
您可以選擇 「 Anytime 」 傳遞模式，請確定您有您的使用者是否 hello 的 tooreach 是否執行應用程式。
當您選取 「 安裝 」 時，您必須已提供 hello 憑證從您的應用程式為建置基礎 （APNS 或 GCM） 的 hello 平台。 

## <a name="schedule-a-push-campaign"></a>排定推送活動
### <a name="plan-toostart-a-campaign"></a>計劃 tooStart 活動
![Shedule1][18]

為 hello 的年 3 月 21，而且您有公告 toomake 並已計畫 hello 22nd 年 3 月的午夜。 您不需要 toostay 前面 hello 介面 toodo 推入 ！ 您可以規劃事先 hello 確切分鐘會傳送通知。

* 取消核取 hello [無] 核取方塊並選取開始時間 
* 選擇 hello 日期和 hello 次想 toostart hello 推播宣傳活動。

### <a name="plan-tooend-a-campaign"></a>計劃 tooend 活動
![Shedule2][19]

您想要在 hello 您活動 toostop 25th 年 3 月的下午 3: 00，但您知道將有 toodo 它。
您不需要在 hello 介面 toopush 前面 toostay ！ 您可以規劃事先 hello 確切分鐘會停止您的活動。

* 按一下 hello 無 核取方塊，或選取 結束時間
* 選擇 hello 日期和 hello 次想 toofinish hello 推播宣傳活動。

### <a name="end-a-campaign-manually"></a>手動結束活動
![Shedule3][20]

根據預設，hello"None"，會選取核取方塊。
這表示 hello 活動會開始為您啟用在 hello 抵達部分，會結束，您會將其停止 hello 上達到 > 一節。

> [!NOTE]
> 沒有結束日期的情況下建立的活動在 hello 裝置上本機儲存 hello 推入並將其顯示 hello 即使手動結束 hello 活動開啟 hello 應用程式的下一次。

## <a name="enhance-a-push-notification-with-a-text-view"></a>使用文字檢視增強推送通知
### <a name="what-is-a-text-view"></a>什麼是文字檢視？
![TextView1][21]

文字檢視是具有文字內容的快顯視窗。 Hello 使用者已按一下 hello 推播通知之後，就會出現這個快顯視窗。
文字檢視可讓您 toopresent 更多內容 tooyour 使用者。 這也是 hello 機會 toopresent 例如跳躍 tooa 應用程式頁面，將重新導向 tooa 存放區中，開啟網頁，傳送電子郵件，啟動當地語系化搜尋等呼叫 tooaction...

### <a name="example-text-view"></a>範例：文字檢視
* Hello 「 連接 」 一節中建立您的推播通知活動，並提供您的活動名稱

![TextView2][22]

* 會出現的 hello 訊息寫入 hello 通知。
* 選取 hello 公告的內容類型為"text"

![TextView3][23]

> [!NOTE]
> 當您推送文字檢視時，它一律是先有通知。 

* 定義 hello 文字 （如果您之後需要選取 hello 文字公告的內容，hello 子區段會出現，讓您設定您想要顯示的 toobe toodefine hello 文字）。

![TextView4][24]

* 撰寫 hello 標題會出現在 hello hello 訊息最上方。
* 撰寫 hello hello 文字檢視主要內容。
* 撰寫 hello 內容將會出現在 hello 動作按鈕 （動作按鈕可讓 hello 應用程式 toomake 特定的動作，例如開啟的 hello 應用程式，重新導向 tooan 應用程式市集或任何一種來源，您可以提供網頁） 上。
* 會出現在 hello 結束 按鈕的寫入 hello 內容 （按一下 hello 結束 按鈕，hello 文字檢視將會消失）。
* 建立您的推播通知活動，它會出現在 hello 活動清單。

![TextView5][25]

* 啟用推播通知活動 toosend hello 文字檢視 tooyour 的使用者。

![TextView6][26]

* 結果

![TextView7][27]

* hello 使用者會收到 hello 通知並按一下它。
* hello 文字檢視會顯示為快顯的允許 hello 使用者 toointeract 與它。

## <a name="enhance-a-push-notification-with-a-web-view"></a>使用網頁檢視增強推送通知
### <a name="what-is-a-web-view"></a>什麼是網頁檢視？
![WebView1][28]

網頁檢視是具有網頁內容的快顯視窗。 Hello 使用者已按下 hello 推播通知時，會出現這個快顯視窗。
網頁檢視可讓您 toohave hello 使用者具有更多的互動。
這也是 hello 機會 toopresent 呼叫 tooaction，例如重新導向 tooApp 存放區中，開啟網頁，傳送電子郵件，啟動當地語系化搜尋等等...

### <a name="example-web-view"></a>範例：網頁檢視
* Hello 「 連接 」 一節中建立您的推播宣傳活動，並提供您的活動名稱。

![WebView2][29]

* 會出現的 hello 訊息寫入 hello 通知。
* 選取 hello 公告的內容類型為"web"

![WebView3][30]

### <a name="about-announcement-types"></a>關於公告類型：
* 僅通知：這是簡單的標準通知。 這表示如果使用者按一下它，會出現任何其他檢視，但只有 hello 動作相關聯 tooit 就會發生。
* 文字公告： 它是既定 hello 使用者 toohave 看一下文字檢視通知。
* Web 公告： 它是既定 hello 使用者 toohave 查看網頁檢視的通知。
  選取 hello"Web 宣告 」 內容。

> [!NOTE]
> 當您推送網頁檢視時，它一律是先有通知。

* 定義 hello web 內容 （如果您之後需要選取 hello 公告網頁，hello 子區段會出現，讓您設定您想要顯示的 toobe toodefine hello web 檢視內容）。

![WebView4][31]

* 撰寫 hello 標題會出現在 hello 頂端 hello 訊息 （選擇性）。
* 在這裡撰寫您的 HTML 程式碼。
* 按一下編輯模式按鈕 tooswitch 版的 hello 來源，並查看其外觀類似。
* 撰寫 hello 內容將會出現在 hello 動作按鈕 （動作按鈕可讓 hello 應用程式 toomake 特定的動作，例如開啟的 hello 應用程式，重新導向 tooa 存放區或任何一種來源，您可以提供網頁） 上。
* 會出現在 hello 結束 按鈕的寫入 hello 內容 （按一下 hello 結束 按鈕，hello 網頁檢視會消失）。
* 結果

![WebView5][32]

* hello 使用者收到 hello 通知，然後按一下它。
* hello 文字檢視會顯示為快顯的允許 hello 使用者 toointeract 與它。

<!--Image references-->
[1]: ./media/mobile-engagement-how-tos/First1.png
[2]: ./media/mobile-engagement-how-tos/First2.png
[3]: ./media/mobile-engagement-how-tos/First3.png
[4]: ./media/mobile-engagement-how-tos/First4.png
[5]: ./media/mobile-engagement-how-tos/First5.png
[6]: ./media/mobile-engagement-how-tos/First6.png
[7]: ./media/mobile-engagement-how-tos/First7.png
[8]: ./media/mobile-engagement-how-tos/Test1.png
[9]: ./media/mobile-engagement-how-tos/Test2.png
[10]: ./media/mobile-engagement-how-tos/Test3.png
[11]: ./media/mobile-engagement-how-tos/Personalize1.png
[12]: ./media/mobile-engagement-how-tos/Personalize2.png
[13]: ./media/mobile-engagement-how-tos/Personalize3.png
[14]: ./media/mobile-engagement-how-tos/Personalize4.png
[15]: ./media/mobile-engagement-how-tos/Differentiate1.png
[16]: ./media/mobile-engagement-how-tos/Differentiate2.png
[17]: ./media/mobile-engagement-how-tos/Differentiate3.png
[18]: ./media/mobile-engagement-how-tos/Schedule1.png
[19]: ./media/mobile-engagement-how-tos/Schedule2.png
[20]: ./media/mobile-engagement-how-tos/Schedule3.png
[21]: ./media/mobile-engagement-how-tos/TextView1.png
[22]: ./media/mobile-engagement-how-tos/TextView2.png
[23]: ./media/mobile-engagement-how-tos/TextView3.png
[24]: ./media/mobile-engagement-how-tos/TextView4.png
[25]: ./media/mobile-engagement-how-tos/TextView5.png
[26]: ./media/mobile-engagement-how-tos/TextView6.png
[27]: ./media/mobile-engagement-how-tos/TextView7.png
[28]: ./media/mobile-engagement-how-tos/WebView1.png
[29]: ./media/mobile-engagement-how-tos/WebView2.png
[30]: ./media/mobile-engagement-how-tos/WebView3.png
[31]: ./media/mobile-engagement-how-tos/WebView4.png
[32]: ./media/mobile-engagement-how-tos/WebView5.png

<!--Link references-->
[Link 1]: mobile-engagement-user-interface.md
[Link 2]: mobile-engagement-troubleshooting-guide.md
[Link 3]: mobile-engagement-how-tos.md
[Link 4]: http://go.microsoft.com/fwlink/?LinkID=525553
[Link 5]: http://go.microsoft.com/fwlink/?LinkID=525554
[Link 6]: http://go.microsoft.com/fwlink/?LinkId=525555
[Link 7]: https://account.windowsazure.com/PreviewFeatures
[Link 8]: https://social.msdn.microsoft.com/Forums/azure/home?forum=azuremobileengagement
[Link 9]: http://azure.microsoft.com/services/mobile-engagement/
[Link 10]: http://azure.microsoft.com/documentation/services/mobile-engagement/
[Link 11]: http://azure.microsoft.com/pricing/details/mobile-engagement/
[Link 12]: mobile-engagement-user-interface-navigation.md
[Link 13]: mobile-engagement-user-interface-home.md
[Link 14]: mobile-engagement-user-interface-my-account.md
[Link 15]: mobile-engagement-user-interface-analytics.md
[Link 16]: mobile-engagement-user-interface-monitor.md
[Link 17]: mobile-engagement-user-interface-reach.md
[Link 18]: mobile-engagement-user-interface-segments.md
[Link 19]: mobile-engagement-user-interface-dashboard.md
[Link 20]: mobile-engagement-user-interface-settings.md
[Link 21]: mobile-engagement-troubleshooting-guide-analytics.md
[Link 22]: mobile-engagement-troubleshooting-guide-apis.md
[Link 23]: mobile-engagement-troubleshooting-guide-push-reach.md
[Link 24]: mobile-engagement-troubleshooting-guide-service.md
[Link 25]: mobile-engagement-troubleshooting-guide-sdk.md
[Link 26]: mobile-engagement-troubleshooting-guide-sr-info.md
[Link 27]: ../mobile-engagement-how-tos-first-push.md
[Link 28]: ../mobile-engagement-how-tos-test-campaign.md
[Link 29]: ../mobile-engagement-how-tos-personalize-push.md
[Link 30]: ../mobile-engagement-how-tos-differentiate-push.md
[Link 31]: ../mobile-engagement-how-tos-schedule-campaign.md
[Link 32]: ../mobile-engagement-how-tos-text-view.md
[Link 33]: ../mobile-engagement-how-tos-web-view.md

