---
title: "aaaAzure Mobile Engagement 使用者介面為連線到準則"
description: "了解如何 toouse 目標準則 toosend 推送活動 tooa 選取您的使用者使用 Azure Mobile Engagement 的子集"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: a4ed03a0-55b1-4dd8-b0bd-c475005afb66
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: d956add1b7edc1d49451596019c5a4dec098d724
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-targeting-criteria-toosend-push-campaigns-tooa-select-subset-of-your-users"></a>Toouse 目標準則 toosend 推送活動 tooa 如何選取您的使用者子集
目標觀眾使用 hello 「 新準則 」 按鈕的特定準則是其中一個 hello 最強大的概念 Azure Mobile Engagement 可協助您傳送相關推播 hello 客戶會回應的濫發 everyone tooinstead 的通知。 您可以限制觀眾根據標準的準則，並模擬推播通知 toodetermine 很多人會收到 hello 通知。

**另請參閱：**

* [UI 文件 - 觸達 - 新的推播活動][Link 27]

## <a name="audience-criteria-can-include"></a>對象準則可以包括：
* * * Technicals: * * 您可鎖定目標根據的 hello hello 分析和監視章節中可以看到相同的技術資訊。 **另請參閱：** [UI 文件 - 分析][Link 15]、[UI 文件 - 監視器][Link 16]
* **位置：**應用程式，使用 「 即時位置回報 「 地理圍欄可作為準則 tootarget 從 hello GPS 位置的對象的地理位置。 「 延遲區域位置報告 」 呼叫也會使用的 tootarget 從 hello 手機位置的對象 （「 即時位置回報 」 和 「 延遲區域位置回報 」 必須從啟動 hello SDK）。 **另請參閱：** [SDK 文件 - iOS - 整合][Link 5]、[SDK 文件 - Android - 整合][Link 5]
* **觸達意見反應：** 您可以根據他們上一個透過觸達意見反應的通知、投票和資料推送的觸達意見反應來選擇目標對象。 這可讓您 toobetter 目標觀眾兩個或三個到達您的行銷活動之後無法 hello 第一次。 它也可以用出使用者已經收到一則通知類似內容，藉由設定活動 tooNOT toofilter 傳送 toousers 已經已收到特定的上一個活動。 您甚至可以排除包含特定有效活動的使用者收到新的推播。 **另請參閱：** [UI 文件 - 觸達 - 推播內容][Link 29]
* **安裝追蹤：** 您可以追蹤根據使用者安裝您應用程式之位置所建立的資訊。 **另請參閱：** [UI 文件 - 設定][Link 20]
* **使用者設定檔：**您可以根據標準使用者資訊的目標，您可以根據您所建立的 hello 自訂的應用程式資訊的目標。 這包括使用者目前登入而回答您要求其相關的 tooset hello 應用程式本身而不是只如何它們所作的反應 tooprevious 活動中的特定問題的使用者。 所有為您應用程式定義的應用程式資訊都顯示在這個清單。
* 區隔：您也可以根據依特定使用者行為 (包含多個準則) 建立的區隔來選擇目標。 所有為您應用程式定義的區隔都顯示在這個清單。 **另請參閱：** [UI 文件 -區隔][Link 18]
* **應用程式資訊：**可以從 [設定] tootrack 使用者行為建立自訂應用程式資訊標記。 **另請參閱：** [UI 文件 - 設定][Link 20]

## <a name="example"></a>範例：
如果您想 toopush 公告只有 toohello 子集使用者執行應用程式內購買動作。

1. 移 tooyour 應用程式設定頁面上，選取 hello"應用程式資訊 功能表，然後選取 新應用程式資訊
2. 註冊一個稱為 "inAppPurchase" 的新布林值應用程式資訊
3. 讓您設定此應用程式資訊的應用程式太"，則為 true 」 時 hello 使用者成功執行應用程式內購買 (使用 hello sendAppInfo (「 inAppPurchase"，...) 函式)
4. 如果您不想 toodo 這從您的應用程式，您可以從您的後端執行使用 hello 裝置 API）
5. 然後，您只需要您的通知，限制您的觀眾 toousers 具有"inAppPurchase"的準則設定太 」 為 true 」 toocreate）

> [!NOTE]
> 目標應用程式資訊標記以外的準則為根據需要 Azure Mobile Engagement toogather 資訊從您的使用者裝置，才會傳送 hello 推入，並可能會導致延遲。 複雜的推送設定選項 (例如更新徽章) 可能也會延遲推送。 使用 hello 推送 API 中的 「 一次完成 「 活動是 hello 絕對最快推入的方法在 Azure Mobile Engagement 中。 使用應用程式資訊標記為推入準則觸達活動 （是使用從 hello 觸達 API 或 hello UI） 是 hello 下一個最快的方法，因為應用程式資訊標記會儲存在 hello 伺服器端上。 使用其他目標條件的推播宣傳活動為 hello 最有彈性，但最慢的推入方法，因為 Azure Mobile Engagement tooquery hello 裝置順序 toosend hello 促銷活動中。

![Reach-Criterion1][29] 

## <a name="criterion-options-apply-to"></a>準則選項適用範圍：
* **技術**     
* 韌體名稱：韌體名稱
* 韌體版本：韌體版本
* 裝置型號：裝置型號
* 裝置製造商：裝置製造商
* 應用程式版本：應用程式版本
* 電信業者名稱：電信業者名稱、未定義
* 電信業者國家/地區：電信業者國家/地區、未定義
* 網路類型：網路類型
* 地區設定：地區設定
* 螢幕大小：螢幕大小
* **位置**      
* 上一個已知區域：國家/地區、區域、位置
* 即時地理柵欄：POI 清單 (名稱、動作)、圓形 POI (名稱、緯度、經度、以公尺為單位的半徑)
* **觸達意見反應**     
* 通知意見反應：通知、意見反應
* 投票意見反應：投票、意見反應
* 投票答案意見反應：投票答案意見反應、問題、選項
* 資料推送意見反應：資料推送、意見反應
* **安裝追蹤**     
* 市集：市集、未定義
* 來源：來源
* **使用者個人檔案**     
* 性別：男性或女性、未定義
* 生日：運算子、日期、未定義
* 選擇加入：true 或 false、未定義
* **應用程式資訊**      
* 字串：字串、未定義
* 日期：運算子、日期、未定義
* 整數：運算子、數字、未定義
* 布林值：true 或 false、未定義
* **區隔**    
* 區隔的名稱 (從下拉式清單)、排除 (不屬於此區隔的目標使用者)。

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

