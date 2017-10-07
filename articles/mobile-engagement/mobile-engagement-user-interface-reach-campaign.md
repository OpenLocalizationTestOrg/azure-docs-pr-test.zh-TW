---
title: "aaaAzure Mobile Engagement 使用者介面為連線到活動"
description: "Laern 如何 toocreate 和管理使用 Azure Mobile Engagement 的推送通知活動"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: 2fe124a2-a86f-4136-81ba-a9d298ec798a
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 825e550ace63a34d1a90b10fa976a61eb15a6d04
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-and-manage-push-notification-campaigns"></a>如何 toocreate 和管理推送通知活動
您可以使用包含複雜公式的 hello hello UI toocreate 新的推播宣傳活動觸達一節提供您需要 toosend 推播通知的所有 hello 資訊。 hello 選項的推播宣傳活動會稍微不同視 hello 四個活動類型而定： 宣告、 投票、 資料推入和磚 (僅限 Windows Phone)。

### <a name="option-applies-to"></a>選項適用範圍：
* 語言：全部 (通知、投票、資料推送、圖格)
* 活動：全部 (通知、投票、資料推送、圖格)
* 通知：通知、投票
* 內容：每種活動類型都不同
* 對象：全部 (通知、投票、資料推送、圖格)
* 時間範圍：通知、投票、圖格
* 測試：全部 (通知、投票、資料推送、圖格)

![Reach-Campaign1][20]

## <a name="languages"></a>語言
您可以使用 hello 語言下拉式清單功能表 toosend 設定 toouse 不同語言程式推入 toodevices 的不同版本。 根據預設，所有的裝置將會收到的 hello 相同不論何種語言設定 toouse 推入。 使用其裝置設定 tooa 不同語言的使用者會收到 hello hello 推入預設語言版本。 Hello 推送活動選項中有許多可讓您 toospecify 替代內容為每個您所選取的 hello 其他語言。 

![Reach-Campaign2][21]

### <a name="language-differences-apply-to"></a>語言差異適用範圍：
* 語言： 可能在加法 toohello 預設語言中選取唯一的語言
* 活動：所有語言都相同
* 通知： 唯一的每一種語言此外 toohello 預設語言
* 內容： 唯一的每一種語言此外 toohello 預設語言
* 對象：可根據個別的語言準則來篩選
* 時間範圍：所有語言都相同
* 測試： 可能會傳送 tooeach 語言一次

### <a name="supported-languages"></a>支援的語言：
* 阿拉伯文 (ar) 
* 保加利亞文 (bg) 
* 卡達隆尼亞文 (ca) 
* 中文 (zh) 
* 克羅埃西亞文 (hr) 
* 捷克文 (cs) 
* 丹麥文 (da) 
* 荷蘭文 (nl) 
* 英文 (en) 
* 芬蘭文 (fi) 
* 法文 (fr) 
* 德文 (de) 
* 希臘文 (el) 
* 希伯來文 (he) 
* 印度文 (hi) 
* 匈牙利文 (hu) 
* 印尼文 (id) 
* 義大利文 (it) 
* 日文 (ja) 
* 韓文 (ko) 
* 拉脫維亞文 (lv) 
* 立陶宛文 (lt) 
* 馬來文 (macrolanguage) (ms) 
* 挪威文 (巴克摩) (nb) 
* 波蘭文 (pl) 
* 葡萄牙文 (pt) 
* 羅馬尼亞文 (ro) 
* 俄文 (ru) 
* 塞爾維亞文 (sr) 
* 斯洛伐克文 (sk) 
* 斯洛維尼亞文 (sl) 
* 西班牙文 (es) 
* 瑞典文 (sv) 
* 塔加拉族文 (tl) 
* 泰文 (th) 
* 土耳其文 (tr) 
* 烏克蘭文 (uk) 
* 越南文 (vi) 

## <a name="campaign"></a>活動
您可以使用 hello 活動區段 tooset hello 名稱，以及您的活動的類別以及您計劃的推播宣傳活動 tooignore hello 觀眾區段，並改為傳送 hello 觸達 API 透過此活動 （和 hello 低層級推送 API 的某些項目）。 類別可用於根據預先定義的設定自訂的通知範本 toocontrol 應用程式內通知。 您可以取得一份您現有 「 類別 」 透過 hello 觸達 API。

> [!WARNING]
> 如果您使用 hello"忽略受眾，推入將會傳送 hello 應用程式開發介面透過 toousers 」 選項 hello 「 活動 」 一節中的觸達活動，不會自動傳送 hello 行銷活動，您需要 toosend 它以手動方式透過 hello 觸達 API。

![Reach-Campaign3][22]

### <a name="option-applies-to"></a>選項適用範圍：
* 名稱：全部
* 類別：通知、投票
* 忽略受眾，推入將會傳送 hello 應用程式開發介面透過 toousers： 所有

## <a name="notification"></a>通知
您可以使用 hello 通知區段 tooset 基本設定，您的推播包括： hello 標題的 hello 推入，hello 訊息，在應用程式映像，或者如果它是可解除。 通知的許多設定都是裝置的特定 toohello 平台，您。 您可以選取要在「應用程式內」或「應用程式外」或兩者傳送您的推播。 (請記住，使用者就可以 「 選擇加入 」 或 「 退出 」 的 「 從應用程式 」 在 hello 作業系統層級將推入至他們的裝置，而且 Azure Mobile Engagement 不會是能 toooverride 這項設定。 也請記住，hello 觸達 API 「 以應用程式 「 處理 」 應用程式超出"推播通知。 hello 推送 API 可以是使用的 toohandle 太推入 」 的應用程式超出"）。使用圖片或 HTML 內容，包括深層連結來連結您的應用程式或 tooanother 位置，在您的應用程式 （Android SDK 2.1.0 或更新版本所需的意圖類別） 之外，您可以自訂推播通知。 您可以變更 hello 圖示或 iOS 徽章和文字或 web 內容 （html 內容，URL 連結 tooanother 位置 hello 應用程式內外的快顯） 傳送。 您也可以使 Android 裝置響鈴或震動以 hello 推入。 （請記住，您將需要 hello 正確 Android SDK 權限資訊清單檔案 tooring 或震動裝置）。Android 的「大型圖片」尺寸目前沒有任何業界標準，因為每個裝置使用不同的螢幕尺寸，不過 400x100 的圖片幾乎可在所有的螢幕尺寸上運作。

### <a name="delivery-types"></a>傳遞類型：
* 不在應用程式只： hello 使用者不使用 hello 應用程式時，就會傳送 hello 通知。
* 從應用程式僅通知的 hello 需要從 Apple 或 Google （APNS 或 GCM 憑證） 的憑證。
* 在應用程式只： 只有在執行 hello 應用程式時才出現 hello 通知。
* hello 通知使用 hello Capptain 傳送系統 tooreach hello 使用者。 您可以完全自訂 hello 配置/的視覺顯示發送。
* 任何時間： 此選項可確保您傳送的通知，或未執行其中一個 hello 應用程式。

![Reach-Campaign4][23]

### <a name="option-applies-to"></a>選項適用範圍：
* 通知：通知、投票

## <a name="content"></a>內容
您可以使用 hello 內容區段 toomodify hello 內容的宣告、 投票、 資料推播通知，以及磚 (僅限 Windows Phone)。 hello 內容設定的推送活動的是特定 toohello 活動類型。 

### <a name="see-also"></a>另請參閱
* [UI 文件 - 觸達 - 推送內容][Link 29]

![Reach-Campaign5][24]

## <a name="audience"></a>對象
您的行銷活動根據自訂準則的限制，您可以使用 hello 觀眾區段 toodefine 標準的項目 toolimit 清單。 hello 組標準的選項 tooLimit 觀眾可讓您 toopush tooeither 新或舊的使用者或僅限原生推送使用者。 您也可以設定使用者接收 hello 推播配額 toolimit hello 數字。 您可以手動編輯 hello 運算式活動的方式篩選的 tooinclude 一或多個準則 tootarget 使用者。 您可以手動輸入對象運算式。 這類運算式必須明確地定義 hello 準則之間的關聯性。 描述準則的識別項必須以大寫字母開頭，而且不能包含空格。 可以使用描述 hello hello 準則之間的關聯性 'and'、 'or'、 'not' 運算子以及 '（'，'）'。 範例："Criterion1 or (Criterion1 and not Criterion2)"。

> [!NOTE]
> 大型的對象，包含在活動中，與 hello 伺服器端為目標的掃描可能會降低，特別是當您嘗試 toostart 多個活動在 hello 相同的時間。

* 可能的話，一次只啟動一個活動。
* 在 hello 最多只能啟動四個活動一次。
* 推播 tooyour 作用中使用者 (核取方塊 」 僅連絡使用者可以使用原生推送連 」 和 「 僅連絡作用中的使用者 」)，因此只有您的使用者仍 hello 安裝的應用程式，並用它將需要 toobe 掃描。
  一旦您的對象定義之後，您可以使用 hello 模擬按鈕 toofind 出多少使用者會收到此 Push。 這會計算 hello 可能目標 （這是根據使用者隨機取樣估計） 此對象的已知使用者數。 請注意，已解除安裝 hello 應用程式的使用者也是算是此受眾的一部分，但無法觸達。

### <a name="see-also"></a>另請參閱
* [UI 文件 - 觸達 - 新增推播準則][Link 28]

![Reach-Campaign6][25]

### <a name="edit-expression"></a>編輯運算式
![Reach-Campaign7][26]

### <a name="limit-your-audience-option-applies-to"></a>限制對象選項適用範圍：
* 只吸引部份使用者：全部 (通知、投票、資料推送、圖格)
* 只讓舊使用者參與：全部 (通知、投票、資料推送、圖格)
* 只讓新使用者參與：全部 (通知、投票、資料推送、圖格)
* 只讓閒置使用者參與：通知、投票、圖格
* 只讓作用中的使用者參與：全部 (通知、投票、資料推送、圖格)
* 只吸引可使用原生推送觸達的使用者：宣告、投票

## <a name="time-frame"></a>時間範圍
將傳送嗨推入，或您可以立即讓 hello 時段空白 toostart hello 活動時，您可以使用 hello 時段區段 tooset。 請記住，使用 hello 一向 time zone 可能 hello 活動一天開始早於您預期使用者在亞洲和傳送的推播通知一次 hello world 相符 hello 時間範圍內的時區設定您的活動時，才小批次。 使用 hello 畷樾簅 time zone 也可能導致延遲活動中因為它有 toorequest hello 時間，從 hello 電話才開始 hello 推入。

> [!NOTE]
> 沒有結束日期的活動可能會在本機快取推送，甚至在您手動完成活動之後，仍然繼續顯示推送。 tooavoid 此行為的特定活動結束時間。

### <a name="see-also"></a>另請參閱
* [觸達 - 作法 – 排程][Link 3] 

![Reach-Campaign8][27]

### <a name="settings-apply-to"></a>設定適用範圍：
* 時間範圍：通知、投票、圖格

## <a name="test"></a>測試
您可以使用 hello 測試區段 toosend 此 push tooyour 自己的測試裝置，才能儲存 hello 行銷活動。 如果您已設定任何自訂的支援語言的這個活動，您可以在每個語言中測試 hello 推入。 您可以從 [我的帳戶] 設定測試裝置。

> [!NOTE]
> 當您使用 hello 按鈕時，會記錄資料的任何伺服器端太"test"推播通知，針對實際的推送活動只會記錄資料。

### <a name="see-also"></a>另請參閱
* [UI 文件 - 我的帳戶][Link 14]

![Reach-Campaign9][28]

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

