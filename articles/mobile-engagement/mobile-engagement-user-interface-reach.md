---
title: "aaaAzure Mobile Engagement 使用者介面觸達"
description: "深入了解如何 tooreach toohello 使用者應用程式使用 Azure Mobile Engagement 的推播通知"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: d96e2590-08dd-4481-a352-2c18f26a1643
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 40d5162ddeccec82c2c9f5b0d72b4cb10c9ddc38
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooreach-out-toohello-users-of-your-application-with-push-notifications"></a>如何 tooreach toohello 的推播通知的應用程式的使用者
本文說明 hello**到達**] 索引標籤的 hello **Mobile Engagement**入口網站。 使用 hello **Mobile Engagement** toomonitor 入口網站和管理您的行動裝置應用程式。 請注意使用 hello 入口網站，您必須先 toocreate 該 toostart **Azure Mobile Engagement**帳戶。 如需詳細資訊，請參閱[建立 Azure Mobile Engagement 帳戶](mobile-engagement-create.md)。

hello 到達的 hello ui 段您也可以建立/編輯/啟動/完成/監視的 hello 推送活動管理工具，並取得推送通知活動和功能，也可以存取透過 hello 觸達 API （和 hello 低的某些項目上的統計資料層級推送應用程式開發介面）。 請記住，不論您使用 hello 應用程式開發介面或 hello UI，您將需要 toointegrate Azure Mobile Engagement 和觸達每個平台以 hello SDK，才能使用應用程式達到行銷活動。

> [!NOTE]
> 多區段的 hello **Mobile Engagement**入口網站 UI 包含 hello**顯示說明**] 按鈕。 按此按鈕 tooget 區段內容詳細資訊。
> 
> 

## <a name="four-types-of-push-notifications"></a>推播通知的四種類型
1. 公告功能-可讓您將他們重新導向 tooanother 位置內應用程式或 toosend toosend 廣告郵件 toousers 它們 tooa 網頁或儲存您的應用程式之外。 
2. 輪詢-可讓您從使用者 toogather 資訊來提問以它們。
3. 資料推送-可讓您 toosend 二進位或 base64 資料檔案。 資料推送中包含的 hello 資訊在應用程式中傳送 tooyour 應用程式 toomodify 您的使用者目前的體驗。 您的應用程式需要在資料推送的 toobe 無法 tooprocess hello 資料。

## <a name="campaign-details"></a>活動詳細資料
您可以編輯、 複製、 刪除或啟動具有尚未啟動其名稱為上方的活動或您可以按一下 tooopen 它們。 您可以複製已啟用由其名稱將滑鼠停留的活動，或者您可以按一下 tooopen 它們。 不過，活動一旦啟動，您就無法變更。

![Reach1][18]

## <a name="reach-feedback"></a>觸達意見反應
按一下**統計資料**toosee hello 觸達活動詳細資料。 hello**簡單**檢視提供的資料行的橫條圖，啟用活動之後發生了什麼事 hello 表單中的視覺表示法。 hello**進階**提供更細微的 hello 推播宣傳活動詳細資料檢視。 這些詳細資料將無法使用，如果您要傳送的測試活動也就推播傳送的 tooa 測試裝置。 以下是解譯這些詳細資料的方式：

1. **推入**-這會指定 hello 訊息推入 toohello 裝置數目。 此數目將取決於 hello 建立 hello 推播宣傳活動時，您指定的目標對象。 如果您未指定任何目標對象，然後此 push 會送出 tooall hello 註冊裝置。 如同其他所有推入服務，我們不執行推送 hello 通知直接 toohello 裝置，但改為將其推送 toohello 各平台特定的推播通知服務 (PNS-APNS/GCM/WNS)，讓它們可以傳送嗨通知 toohello 裝置。 
2. **傳遞**-這會指定為接收 Mobile Engagement SDK 的 hello 訊息成功傳送嗨 PNS toohello 裝置及認可的數目。 
   
   *已傳送計數小於已推送計數的原因：*
   
   1. 如果 hello 使用者解除 hello 應用程式安裝從 hello 裝置但 hello PNS 不知道它在 hello 階段，我們會傳送 hello 發送 toohello PNS 然後 hello 訊息皆會予以捨棄。
   2. 如果 hello 裝置 hello 應用程式，但 hello 裝置本身很長的時間期間已離線，則 hello PNS 會失敗 toodeliver hello 訊息 toohello 裝置。 
   3. 如果 hello 訊息傳遞 toohello 裝置取得但 hello Mobile Engagement SDK 在 hello 應用程式中的無法辨識 hello hello 訊息內容，它會捨棄該訊息。 如果 hello 通知 hello 應用程式中的 hello 自訂 hello SDK 和 drop hello 訊息中產生攔截的例外狀況，則會發生此問題。 這也可能會發生 hello hello 裝置上的應用程式是否使用版的 hello Mobile Engagement SDK 不能 toounderstand hello 較新版本的 hello 推播訊息寄件者 hello 平台，但 hello 應用程式已升級之後 hello 通知時，才發送 hello 服務平台。 hello**進階**] 索引標籤將會通知已卸除的訊息數量。 
   4. 在 iOS 裝置上訊息有時才傳送如果其中一個 hello 裝置位於電力偏低，或 hello 應用程式會耗用大量的電力，當處理遠端通知。 這是 hello 的 iOS 裝置的限制。   
3. **顯示**-這會指定訊息已成功顯示 toohello 應用程式使用者的 hello 裝置 hello 形式系統推入/out 的-應用程式通知在 hello 通知中心或應用程式內通知內 hello 行動的 hello 數目應用程式。  hello**進階**多少了系統通知和多少應用程式內通知] 索引標籤也將會通知您。 
   
   *顯示原因計數小於傳遞的計數 (等候 toobe 顯示)*
   
   1. 如果 hello 通知活動的結束日期必須在其上，則很可能已傳送嗨通知，但當 hello 時間來源 tooopen 並將其顯示 toohello 應用程式的使用者，它是已經過期，永遠不會顯示。   
   2. 如果 hello 通知，則應用程式內通知 hello 通知只會顯示 hello 應用程式使用者開啟 hello 應用程式時。 在其中 hello 應用程式使用者還沒開啟過 hello 應用程式的情況下，hello SDK 會報告已傳送 hello 通知，但尚未顯示，直到開啟 hello 應用程式。 
   3. 如果 hello 通知是在應用程式通知，並設定 toobe 然後也 hello 通知將會報告為傳遞特定活動/螢幕上顯示，但尚未傳送之前 hello 使用者會開啟 hello 特定螢幕上的應用程式。 
4. **使用者互動**-這會指定 hello hello 應用程式使用者已互動，而且將包含 hello 訊息，也就是採取動作或結束的訊息數目。 
   
   * *hello 應用程式使用者可處理的通知 hello 下列方式之一：*
     
     1. 如果 hello 通知系統/out 的-應用程式通知或應用程式內通知傳送為僅限通知就 hello 應用程式使用者在 [hello 通知。
     2. 如果 hello 通知是應用程式內通知與文字或 web 檢視或輪詢然後 hello 應用程式使用者按一下 hello hello 通知中的 [動作] 按鈕。
     3. 如果 hello 通知，則 web 檢視的應用程式內通知然後 hello 應用程式使用者按一下 [僅 Android] hello web 檢視中的 URL
   * *hello 應用程式使用者可結束通知 hello 下列方式之一：*
     
     1. 直接按一下 hello hello 通知 [關閉] 按鈕。 
     2. 離開撥動或刪除 hello 通知。 
     3. 以文字/web 內容和輪詢的應用程式內通知是通常顯示的 toohello 兩步驟程序中的應用程式使用者。 第一次他們會看到通知，當使用者按一下它，他們會看到 hello 後續文字/web/輪詢內容。 hello 應用程式使用者可以結束在這些步驟的通知和 hello 進階檢視中的 hello 詳細資料擷取這。 
5. **已採取動作**-這會指定 hello 訊息已由 hello 應用程式使用者明確已採取動作的數目。 這是 hello 最有趣的數字，因為這樣做會告知應用程式的使用者人數不想要您推入 hello 通知中的 hello 訊息。 

> [!NOTE]
> IOS 和 Windows 平台，如果 hello 使用者具有 hello 應用程式開啟及 hello 行銷活動的"AnyTime"行銷活動則很可能同時從應用程式及應用程式內通知會顯示在 [hello 相同的時間。 這可能會導致顯示計數高於 hello 傳遞。 如果 hello 使用者互動或動作 hello 通知，然後甚至 hello 使用者互動/Actioned 計數可能會大於已傳遞。 
> 
> 

![Reach2][19]

## <a name="see-also"></a>另請參閱
* [概念][Link 6]
* [疑難排解指南服務][Link 24]

<!--Image references-->
[1]: ./media/mobile-engagement-user-interface-navigation/navigation1.png
[2]: ./media/mobile-engagement-user-interface-home/home1.png
[3]: ./media/mobile-engagement-user-interface-home/home2.png
[4]: ./media/mobile-engagement-user-interface-home/home3.png
[5]: ./media/mobile-engagement-user-interface-home/home4.png
[6]: ./media/mobile-engagement-user-interface-home/home5.png
[7]: ./media/mobile-engagement-user-interface-my-account/myaccount1.png
[8]: ./media/mobile-engagement-user-interface-my-account/myaccount2.png
[9]: ./media/mobile-engagement-user-interface-my-account/myaccount3.png
[10]: ./media/mobile-engagement-user-interface-analytics/analytics1.png
[11]: ./media/mobile-engagement-user-interface-analytics/analytics2.png
[12]: ./media/mobile-engagement-user-interface-analytics/analytics3.png
[13]: ./media/mobile-engagement-user-interface-analytics/analytics4.png
[14]: ./media/mobile-engagement-user-interface-monitor/monitor1.png
[15]: ./media/mobile-engagement-user-interface-monitor/monitor2.png
[16]: ./media/mobile-engagement-user-interface-monitor/monitor3.png
[17]: ./media/mobile-engagement-user-interface-monitor/monitor4.png
[18]: ./media/mobile-engagement-user-interface-reach/reach1.png
[19]: ./media/mobile-engagement-user-interface-reach/reach2.png
[20]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign1.png
[21]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign2.png
[22]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign3.png
[23]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign4.png
[24]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign5.png
[25]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign6.png
[26]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign7.png
[27]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign8.png
[28]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign9.png
[29]: ./media/mobile-engagement-user-interface-reach-criterion/Reach-Criterion1.png
[30]: ./media/mobile-engagement-user-interface-reach-content/Reach-Content1.png
[31]: ./media/mobile-engagement-user-interface-reach-content/Reach-Content2.png
[32]: ./media/mobile-engagement-user-interface-reach-content/Reach-Content3.png
[33]: ./media/mobile-engagement-user-interface-reach-content/Reach-Content4.png
[34]: ./media/mobile-engagement-user-interface-dashboard/dashboard1.png
[35]: ./media/mobile-engagement-user-interface-segments/segments1.png
[36]: ./media/mobile-engagement-user-interface-segments/segments2.png
[37]: ./media/mobile-engagement-user-interface-segments/segments3.png
[38]: ./media/mobile-engagement-user-interface-segments/segments4.png
[39]: ./media/mobile-engagement-user-interface-segments/segments5.png
[40]: ./media/mobile-engagement-user-interface-segments/segments6.png
[41]: ./media/mobile-engagement-user-interface-segments/segments7.png
[42]: ./media/mobile-engagement-user-interface-segments/segments8.png
[43]: ./media/mobile-engagement-user-interface-segments/segments9.png
[44]: ./media/mobile-engagement-user-interface-segments/segments10.png
[45]: ./media/mobile-engagement-user-interface-segments/segments11.png
[46]: ./media/mobile-engagement-user-interface-settings/settings1.png
[47]: ./media/mobile-engagement-user-interface-settings/settings2.png
[48]: ./media/mobile-engagement-user-interface-settings/settings3.png
[49]: ./media/mobile-engagement-user-interface-settings/settings4.png
[50]: ./media/mobile-engagement-user-interface-settings/settings5.png
[51]: ./media/mobile-engagement-user-interface-settings/settings6.png
[52]: ./media/mobile-engagement-user-interface-settings/settings7.png
[53]: ./media/mobile-engagement-user-interface-settings/settings8.png
[54]: ./media/mobile-engagement-user-interface-settings/settings9.png
[55]: ./media/mobile-engagement-user-interface-settings/settings10.png
[56]: ./media/mobile-engagement-user-interface-settings/settings11.png
[57]: ./media/mobile-engagement-user-interface-settings/settings12.png
[58]: ./media/mobile-engagement-user-interface-settings/settings13.png

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
[Link 27]: mobile-engagement-user-interface-reach-campaign.md
[Link 28]: mobile-engagement-user-interface-reach-criterion.md
[Link 29]: mobile-engagement-user-interface-reach-content.md

