---
title: "aaaAzure Mobile Engagement 使用者介面的區段"
description: "深入了解如何 toocreate 和管理使用者 tooidentify 習慣使用 Azure Mobile Engagement 的區段"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: 6a4f2205-4a3c-406e-a04f-5e6f2a36653f
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: bb214c45d05ebfbf243978658a7e331d4a7c6e0e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-and-manage-segments-of-users-tooidentify-usage-patterns"></a>如何 toocreate 和管理使用者 tooidentify 習慣的區段
本文說明 hello**區段** 索引標籤的 hello **Mobile Engagement**入口網站。 使用 hello **Mobile Engagement** toomonitor 入口網站和管理您的行動裝置應用程式。

hello UI hello 區段區段可讓您 toowork 上切割您根據 hello 不同的行為和分析，您可以從 hello 應用程式取得，而且也可以存取透過 hello 區段 API 的使用者。 區段會先計算 24 小時之後建立的它們會重新計算根據 hello 最新的分析資訊每隔 24 小時。 一旦計算區段，它就會 「 日 tooday 歷程記錄 」 圖表顯示每一天。

> [!NOTE]
> 多區段的 hello **Mobile Engagement**入口網站 UI 包含 hello**顯示說明** 按鈕。 按此按鈕 tooget 區段內容詳細資訊。
> 
> 

## <a name="create-segments"></a>建立使用者分佈
您可以建立根據向上 too10 準則向上 hello too60 天的特定時間上的線段過去從 hello 分析區段。 例如，您可以建立根據 hello 人具有檢視特定頁面或搜尋最後 10 天內 hello 應用程式內的特定內容的區段。 這項資訊可在 hello 分析區段。 因此，您可以 toocreate 在區段中，使用它，然後再將推播通知 tootarget 這個子集使用者 tooget 它們 toocome 後 toohello 應用程式。 

> [!NOTE]
> 使用者分佈一旦計算之後，就無法進行編輯；它只能複製或終結 (刪除)。 區段可以被複製 hello 內相同的應用程式 (與 hello 相同 AppID)，並也可以被複製到其他應用程式 （具有不同的 AppID)。 

 ![segments1][35] 

## <a name="examples-segments"></a>範例使用者分佈
 ![segments2][36]

區段可讓您 toosegment hello 使用者的應用程式。
研究您的使用者分佈是很重要的行銷策略。 Azure Mobile Engagement 可讓您 tooget 歷程資料，並建立自訂的區段。 此功能強大的工具可讓您 toolearn 有關您的客戶體驗您的應用程式中。 您可以輕鬆地分析您的使用者分佈，並利用這些使用者分佈做為推送目標。
常見的使用案例是您想 toosend 推播通知 tooencourage 使用者 toorate hello 存放區中的應用程式。 而不是傳送通知 tooall 您的使用者，您可以建立的區段時，會指定使用者的已使用您的應用程式每日 hello 上個月，而且有很好的使用者經驗。 若您傳送比較少、目標更明確的推送通知，您就會獲得更好的 ROI。

 ![segments3][37]

### <a name="segments-you-can-create-based-on-hello-major-azure-mobile-engagement-elements"></a>您可以建立的區段基礎 hello 主要 Azure Mobile Engagement 項目：
* 事件： 建立目標一個 hello 應用程式發生兩倍以上一週的特定事件的區段。 
* 工作階段： 建立的使用者使用 hello 應用程式超過 5 次過去一週的區段。
* 活動：建立上個月使用多於或少於 10 次某一頁面或內容的使用者分佈。
* 工作：建立一天完成兩次以上工作的使用者分佈。
* 損毀： 建立所有 hello 使用者已經損毀 10 次以上過去一週的區段。 (您可以在推送此使用者分佈時包含道歉啟事或優待券！)
* 錯誤： 建立的所有 hello 使用者有多個 100 次過去 3 天內發生了錯誤的區段。
* 應用程式資訊： 建立目標時發生 hello 25 天自訂應用程式資訊區段。
  
  ![segments4][38]

toouse 區段，以最佳方式，您必須完成 hello SDK 整合在自訂的應用程式的 [應用程式資訊] 標記的標記計劃中。
接著，移 hello 介面 toohello 首頁中，選取 hello 應用程式，然後按一下 hello 「 區段 」 一節。

1. 選取 hello 「 區段 」 一節。
2. 按一下 「 新的區段 」 hello 按鈕 toocreate 新的區段。

## <a name="real-life-example-create-a-simple-segment-based-on-session-information"></a>實際範例：根據「工作階段」資訊建立簡單的使用者分佈
建立所有 hello 使用者使用您的應用程式至少 50 次 hello 過去一週中的區段。 從該處，尋找只 hello 花了至少 30 秒，每個工作階段的應用程式中的使用者。 這會顯示所有 hello 的使用者在您的應用程式中有正面的體驗。 接下來，建立 hello 區段可能會使用的 toopush 通知 toothese 使用者 tooask 它們 toorate hello 中的應用程式存放區。

 ![segments5][39]

1. 名稱命名您的區段，在訂單 toofind 快速在 hello 「 區段 」 清單。
2. Hello 上按一下 [建立] 按鈕。
   
   ![segments6][40]

選取 [工作階段]。

 ![segments7][41]

1. 選取 最近一週"hello 期間。
2. 按 [下一步]。
   
   ![segments8][42]
3. 選取 hello 與 hello 清單之間的運算子: =;≥ ≤。
4. 輸入 hello 您想要的計數。
5. 選取 hello 出現您想要的項目。 
6. 按 [下一步]。
   這個範例會設定讓該 over hello 過去一週，已在至少 50 的工作階段的比對使用者。
   
   ![segments9][43]

Hello 分割工作階段，您可以選擇每個工作階段做為條件 hello 長度。

1. Hello 清單中選取 hello 運算子。
2. 提供每個工作階段的 hello 長度。
3. 按一下 [下一步]。
   在此範例中，該處會指示，透過所有 hello 有已 hello 出現項目區段中，區隔的工作階段選取只有 hello 所花 30 秒以上每個工作階段的使用者。
   
   ![segments10][44]

名稱在 hello 完成順序 tooretrieve 準則漏斗，並按一下 [完成]。

 ![segments11][45]

當您的準則設定完成時，它會出現在 hello 區段漏斗圖。
因為使用者分佈是根據分析資料，所以使用者分佈也會每天計算一次。
在此範例中，47,7 %hello 總使用者的比對 hello 準則。 它們應該 hello 使用者有良好的體驗，並將會更高評等如果推送通知可能 tooprovide 詢問他們 toorate hello 存放區中的 hello 應用程式。

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
[Link 27]: ../mobile-engagement-how-tos-first-push.md
[Link 28]: ../mobile-engagement-how-tos-test-campaign.md
[Link 29]: ../mobile-engagement-how-tos-personalize-push.md
[Link 30]: ../mobile-engagement-how-tos-differentiate-push.md
[Link 31]: ../mobile-engagement-how-tos-schedule-campaign.md
[Link 32]: ../mobile-engagement-how-tos-text-view.md
[Link 33]: ../mobile-engagement-how-tos-web-view.md

