---
title: "aaaAzure Mobile Engagement 使用者介面-內容連接"
description: "了解如何在 Azure Mobile Engagement toomanage hello 唯一內容推播通知的 hello 不同類型的活動"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: add64f06-43c9-475c-8722-51cd00bb844b
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: de389eb4368d986ef00135036c26e26a2464663e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-hello-unique-content-of-hello-different-types-of-push-notification-campaigns"></a>如何 toomanage hello hello 的推播通知活動的不同類型的唯一內容
您可以使用 hello 新觸達活動 toomodify hello 內容的宣告、 投票、 資料推入和磚 (僅限 Windows Phone) 的內容 > 一節。 hello 內容設定的推送活動的是特定 toohello 活動類型。 

### <a name="content-types"></a>內容類型：
* 通知
* 投票
* 資料推送
* 磚 (僅限 Windows Phone)

## <a name="content-of-announcements"></a>通知的內容
 ![Reach-Content1][30] 

### <a name="choose-hello-type-of-your-announcement"></a>選擇宣告的 hello 類型：
* 僅通知：這是簡單的標準通知。 這表示如果使用者按一下它，會出現任何其他檢視，但只有 hello 動作相關聯 tooit 就會發生。
* 文字公告： 它是既定 hello 使用者 toohave 看一下文字檢視通知。
* Web 公告： 它是既定 hello 使用者 toohave 查看網頁檢視的通知。

### <a name="see-also"></a>另請參閱
* [觸達 - 作法 - 通知][Link 3] 

### <a name="about-web-view-announcements"></a>關於 Web 檢視通知：
Hello 模式 {"deviceid}"hello HTML 程式碼或 JavaScript 程式碼您在此處提供的項目會自動取代為由顯示 hello 公告 hello 裝置 hello 識別項。 這是外部輕鬆 tooretrieve Azure Mobile Engagement 裝置識別碼 web 程式後端辦公室託管的服務。
如果您想 toocreate 完整螢幕 web 檢視 （不含 hello 動作並結束提供預設按鈕我們） 您可以使用 hello web 檢視宣告的 JavaScript 程式碼中的下列功能： 

* 執行 hello 公告： ReachContent.actionContent()
* 結束 hello 公告： ReachContent.exitContent()

### <a name="choose-your-action"></a>選擇您的動作：
### <a name="about-action-urls"></a>關於動作 URL：
可由目標裝置的作業系統解譯的任何 URL 都可以用來做為動作 URL。
可能您的應用程式的所有專用 URL （例如 toomake 使用者跳 tooa 特定畫面） 的支援也可用以做為動作 URL。
Hello {deviceid} 模式每次發生自動取代為執行 hello hello 裝置 hello 識別項。 這可以是透過您的後端辦公室託管的外部 web 服務使用的 tooeasily 擷取 Azure Mobile Engagement 裝置識別碼。

* **Android + iOS 動作**
  * 開啟網頁
  * http://\[web-site-domain\] 
  * 範例︰http://www.azure.com
  * 傳送電子郵件
  * mailto:\[e-mail-recipient\]?subject=\[subject\]&body=\[message\] 
  * Example:mailto:foo@example.com?subject=Greetings%20from%20Azure%20Mobile%20Engagement!&body=Good%20stuff!
  * 傳送簡訊
  * sms:\[phone-number\] 
  * 範例：sms:2125551212
  * 撥電話號碼
  * tel:\[phone-number\] 
  * 範例：tel:2125551212
* **僅限 Android 的動作**
  * 下載 hello Play Store 上的應用程式
  * market://details?id=\[應用程式套件\] 
  * 範例：market://details?id=com.microsoft.office.word
  * 開始地理當地化的搜尋
  * geo:0,0?q=\[搜尋查詢\] 
  * 範例：geo:0,0?q=starbucks,paris
* **僅限 iOS 的動作**
  * 下載 hello App Store 上的應用程式
  * http://itunes.apple.com/[country]/app/[app name]/id[app id]?mt=8 
  * 範例︰http://itunes.apple.com/fr/app/briquet-virtuel/id430154748?mt=8
  * Windows 動作
  * 開啟網頁
  * http://\[web-site-domain\] 
  * 範例︰http://www.azure.com
  * 傳送電子郵件
  * mailto:\[e-mail-recipient\]?subject=\[subject\]&body=\[message\] 
  * Example:mailto:foo@example.com?subject=Greetings%20from%20Azure%20Mobile%20Engagement!&body=Good%20stuff!
  * 傳送簡訊 (需要 Skype 市集應用程式)
  * sms:\[phone-number\] 
  * 範例：sms:2125551212
  * 撥電話號碼 (需要 Skype 市集應用程式)
  * tel:\[phone-number\] 
  * 範例：tel:2125551212
  * 下載 hello Play Store 上的應用程式
  * ms-windows-store:PDP?PFN=\[app package ID\] 
  * 範例：ms-windows-store:PDP?PFN=4d91298a-07cb-40fb-aecc-4cb5615d53c1
  * 開始 bingmaps 搜尋
  * bingmaps:?q=\[search query\] 
  * 範例：bingmaps:?q=starbucks,paris
  * 使用自訂配置
  * \[custom scheme\]://\[custom scheme params\] 
  * 範例：myCustomProtocol://myCustomParams
  * 使用套件資料 (需要副檔名讀取的市集應用程式)
  * \[folder\]\[data\].\[extension\] 
  * 範例：myfolderdata.txt

### <a name="build-a-tracking-url"></a>建置追蹤 URL：
* 請參閱 hello 的 < 設定 > 一節的 hello<UI Documentation>的建置追蹤 URL 的指示，可讓使用者 toodownload 其中一個其他的應用程式。

### <a name="define-hello-texts-of-your-announcement"></a>定義宣告的 hello 文字
填寫 hello 標題、 內容和宣告的按鈕文字。 您可以針對未來的活動，根據的使用者已 toothis 行銷活動的回應 hello 觸達意見反應的對象。 目標對象可以根據 hello 意見反應是否這個活動只推入，回覆，採取動作，或結束。

### <a name="see-also"></a>另請參閱
* [UI 文件 - 觸達 - 新增推播準則][Link 28]

## <a name="content-of-polls"></a>投票的內容
![Reach-Content2][31] 

填寫 hello 標題、 描述和宣告的按鈕文字。 接著，新增問題和選擇 hello 答案 tooyour 問題。
您可以針對未來的活動，根據的使用者已 toothis 行銷活動的回應 hello 觸達意見反應的對象。 選取目標對象時可以根據此活動是否已推送、回覆、採取動作或離開。 目標對象也可以根據輪詢回答意見反應，hello 問題與解答的選擇，當做準則。

### <a name="see-also"></a>另請參閱
* [UI 文件 - 觸達 - 新增推播準則][Link 28]

## <a name="content-of-data-pushes"></a>資料推送的內容
![Reach-Content3][32] 

### <a name="choose-hello-type-of-your-data"></a>選擇資料的 hello 類型：
* 文字
* 二進位資料
* Base64 資料

### <a name="define-hello-content-of-your-data"></a>定義資料的 hello 內容
* 如果您選取 toopush 文字資料，複製並貼上 hello 「 內容 」 中的 hello 文字。
* 如果您選取 toopush 二進位或 base64 資料，請使用 [上傳您的檔案] 按鈕 tooupload hello 您的檔案。
* 您可以針對未來的活動，根據的使用者已 toothis 行銷活動的回應 hello 觸達意見反應的對象。 選取目標對象時可以根據此活動是否已推送、回覆、採取動作或離開。

### <a name="see-also"></a>另請參閱
* [UI 文件 - 觸達 - 新增推播準則][Link 28]

## <a name="content-of-tiles-windows-phone-only"></a>磚的內容 (僅限 Windows Phone)
![Reach-Content4][33]

### <a name="define-hello-content-of-your-tile"></a>定義磚的 hello 內容
hello 磚裝載是顯示在 Windows Phone 裝置上的應用程式的 hello 磚中的 hello 文字 toobe。
圖格發送是適用於 Windows Phone 的原生推送 hello Microsoft 推播通知服務 (MPNS) 版本。 hello 磚推入型別是 hello 唯一發送類型沒有回應，因此 hello 觀眾的未來的活動無法建置 hello 結果的並排顯示推播宣傳活動。 

### <a name="see-also"></a>另請參閱
* [API 文件 - 觸達 API - 原生推送][Link 4]

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

