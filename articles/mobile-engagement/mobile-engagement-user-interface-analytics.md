---
title: "aaaAzure Mobile Engagement 使用者介面的分析"
description: "深入了解如何使用 Azure Mobile Engagement 應用程式的相關 tooanalyze 歷程記錄資料"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: 6b2533ac-b8ec-4e35-872c-d563895bdc0c
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 4a9df11226fed6710cfb1337ae84ece7596d482f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooanalyze-historical-data-about-your-application"></a>如何 tooanalyze 應用程式的相關的歷程記錄資料
本文說明 hello**分析** 索引標籤的 hello **Mobile Engagement**入口網站。 使用 hello **Mobile Engagement** toomonitor 入口網站和管理您的行動裝置應用程式。 請注意使用 hello 入口網站，您必須先 toocreate 該 toostart **Azure Mobile Engagement**帳戶。

hello 分析 hello UI 段提供彙總每隔 24 小時更新一次的歷程資料為基礎的應用程式的相關資訊。 hello 資訊會顯示在不同的儀表板列/列/圓形圖、 格線和對應所組成。 hello 資料也可以下載為.csv 檔案。 大部分的相同資訊使用即時 hello hello UI，監視區段中，也可以存取從 hello 分析 API。

> [!NOTE]
> 多區段的 hello **Mobile Engagement**入口網站 UI 包含 hello**顯示說明** 按鈕。 按此按鈕 tooget 區段內容詳細資訊。

## <a name="standard-and-custom-analytics"></a>標準和自訂分析
Azure Mobile Engagement 提供一組 basic、 standard 分析您的應用程式整合 hello SDK 為可圖形化應用程式的相關資訊。 Azure Mobile Engagement 還提供 hello 能力 toogather 其他自訂分析有關您想要的使用者行為。 您可以從 [設定]  建立一個自訂「標記 (應用程式資訊)」的標記計畫，Azure Mobile Engagement 就可以為您收集這類額外資料。

## <a name="analytics"></a>Analytics
* 儀表板：顯示有關新使用者和作用中使用者及其趨勢的一般資訊。
* 使用者：會依據其裝置識別碼來識別使用者：每個裝置的識別碼都是唯一的 (一位新使用者實際上是一個新裝置)。 如果一位使用者在某個指定時間間隔內執行了第一個工作階段，就會在此時間間隔期間被視為新使用者。 使用者會將其視為保留如果執行了至少一個工作階段期間 hello 過去 7 天。 「作用中使用者」是在指定期間內至少建立了一個工作階段的使用者。 您可以依據每個月、每週、每天或每小時的期間加以排序。 Hello 圖表的所有看起來類似，但可讓您 toofilter 由不同的功能，例如您的應用程式，然後 toosort hello 版本的一段時間。 hello 標準藉由整合 hello SDK 所收集的資訊包括下列 hello： 作用中的使用者，新的使用者、 工作階段數目，length 的每個工作階段、 hello 國家/地區、 區域變數、 位置、 語言承運業者、 裝置、 韌體的技術資訊網路 (WIFI) hello 應用程式和 SDK，客戶使用的版本。 這項資訊可以從 hello 監視器 > 一節的即時檢視。

> [!NOTE]
> hello 時段日期為基礎 hello hello 使用者的裝置設定，讓的使用者的電話已設定不正確的 hello 日期無法顯示在 hello 錯誤時間週期。

* 保留：如果一位使用者在某個指定時間間隔內執行了第一個工作階段，就會在此時間間隔期間被視為保留使用者。 您可以變更 hello 時間間隔期間保留的使用者 （和新的使用者） 會計算 toohours、 天、 週或月。 hello 使用者保留分析建置 cohorts 的頂端。 Cohort 是 hello 組給定的期間內 （亦即，使用者執行其第一個工作階段，在這段期間的 hello 集） 偵測到的所有 hello 新使用者。 我們使用 1 天、2 天、4 天、7 天或 1 個月的同群使用者。 指定的群組、 每隔 1 天、 2 天、 4 天的 7 天或 1 個月，Azure Mobile Engagement 計算 hello 的一組所有使用者所屬 toohello cohort，而且仍在作用中 (也就是，在執行期間 hello 至少一個工作階段的使用者的 hello set)。 此類使用者集合稱為同群使用者版本 (Azure Mobile Engagement 可以顯示您的使用者數量仍在使用您的應用程式，但只有 hello 平台特定的商店可以告訴您的使用者數量的解除安裝您的應用程式-例如，GooglePlay iTunes，Windows 市集等。)。
* Hello 應用程式的使用者工作階段： 一個使用。 工作階段會產生從 hello 序列的使用者所執行的活動 （活動是一個螢幕的 hello 應用程式，通常是相關聯的 toohello 使用量，但這根據 SDK 整合 hello 應用程式中的 hello 方式 hello 而有所不同）。 使用者只能執行一次一個活動： 工作階段時立即啟動 hello 使用者開始其第一個活動，他完成他的最後一個活動時，就會停止。 如果使用者停留超過幾秒鐘的時間而沒有執行任何活動，他的活動序列會分成兩個不同的工作階段。
* 活動： hello 的應用程式中的每個螢幕的名稱和使用者 hello 長度花費每個畫面。 活動是自訂的分析選項將會對應 toohello [應用程式資訊] 標記您自己的應用程式設定：
* 使用者路徑：顯示使用者如何瀏覽您的應用程式活動 (畫面)。 您可以移動 hello 滑桿 tooadjust hello 層級的詳細資料。 藍色的節點代表您的應用程式活動。 其大小是成比例 toohello 時間使用者花在其中。 白色的節點代表工作階段開始和停止。 紅色的節點代表當機。 連結代表在應用程式活動之間 (或活動和當機之間) 轉換。 按一下節點或連結 toodisplay 具有您資料的詳細資訊的工具提示： hello 所花費的時間在特定畫面中，hello 轉換計數，以及的 hello hello 來源活動 toohello 目的地活動的轉換百分比。 (---60%---> B 表示該上的使用者活動 A 關閉 tooactivity B 60%的 hello 時間。)您想要 tooclarify，您可以重新組織 hello 圖形。每次進行變更，都會儲存其位置。 您可以顯示或隱藏 hello 損毀 toolighten hello 圖形。
* 事件： Hello 應用程式中的使用者所採取的特定動作。 hello 發佈的事件會顯示為 hello 每位使用者每個工作階段的事件計數。 事件代表立即性的動作，例如按一下按鈕或 hello 收到通知。 （hello 的事件的意義取決於 hello SDK hello 應用程式中的整合方式）。事件可能在工作階段或作業期間發生，也可以獨立存在。
* 作業： 類似 tooevents 除了其焦點在於 hello 長度 hello 動作。 例如，工作可以告訴您內容 tooload 或呼叫 tooweb 服務要花多久的技術資訊。 它也無法顯示使用者 toofill 表單時要花多久、 建立帳戶，或進行購買。 工作代表 hello 工期的任務，hello 螢幕上所顯示的範例、 下載工作或 hello hello 期間時間橫幅。 （hello 意義的工作取決於 hello SDK hello 應用程式中的整合方式）。工作通常與相關聯的背景工作，hello （亦即，沒有任何使用者活動） 工作階段範圍以外執行。
* Technicals： 技術的相關資訊 hello 裝置 hello 使用者，您可以追蹤，例如 hello hello 使用者裝置的地區設定、 載波偵測、 網路、 裝置、 韌體與螢幕大小和版本的應用程式和使用的 SDK 版本 hello hello 應用程式中的應用程式。
* 錯誤： Hello 應用程式內技術並不會造成的錯誤的相關資訊 hello toocrash 應用程式。 錯誤表示立即的問題，例如網路錯誤或不正確的操作 （hello 的事件的意義取決於 hello SDK hello 應用程式中的整合方式）。錯誤可能在工作階段或工作期間發生，也可以獨立存在。
* 損毀： 錯誤，會造成您的應用程式 toocrash 資訊。 損毀是未預期的狀況 hello 應用程式停止執行預期的功能，必須停止的位置。 當機通常是因為 tooa hello 應用程式中的 bug。

![Analytics2][11]

## <a name="accessing-hello-retention-overview"></a>存取 hello 保留概觀
![Analytics3][12]

hello 保留概觀細分成幾個卡 hello 中間、 在特定的保留期間內每個顯示 hello 概觀。 hello 2 天的保留期限是 hello 範例所示。 hello 其他介面卡顯示 hello 4 天和 7 天的保留期限。

## <a name="understanding-hello-retention-overview-cards"></a>了解 hello 保留概觀卡
![Analytics4][13]

### <a name="each-card-is-composed-of-3-main-parts"></a>每張卡片由 3 個主要部分組成：
1. 1: hello cohort 和 hello 期間被視為
2. 2-4: hello 的 hello 保留目前期間
3. 5: hello 歷程記錄的走勢圖

### <a name="here-is-detailed-information-about-each-element"></a>以下是每個項目的詳細資訊：
1. 群組和期限： 這個標題會提供的 cohort hello 型別。 這裡 「 2 天期間 」 表示我們將探討 hello 行為的使用者超過 2 天，使用者已到達在一段 2 天，以及是否它們連線 hello 之後的 2 天區塊中。 hello 上述範例中會考量 hello 活動的使用者之間 hello 21 及年 11 月 22。
2. 提供 hello 保留速率透過 hello 21 歲到年 11 月 22 hello 抵達 19 和 20 年 11 月中的使用者。 這裡我們必須 1 作用中使用者之間 hello 21 和 22nd、 透過 hello 之間的新使用者的 3 hello 19th 和 20。
3. 與上述相同的資訊以圖形表示此視覺指標可讓 hello。 (第三個 hello hello 的圓形是 hello 33%的數字。)hello 色彩會提供其他資訊： 綠色表示這個數字會增加 hello 前次計算。 黃色表示穩定，紅色表示減少。
4. 這表示 hello 計算所用的 hello 值。
5. 這是走勢圖的 hello 歷程記錄的 hello 保留值。 它可讓您 toosee hello 值在 hello toohave 過去的方式，進而發展的廣泛的檢視。

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
