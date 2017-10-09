---
title: "aaaAzure Mobile Engagement 使用者介面-我的帳戶"
description: "深入了解如何 toomanage 使用 Azure Mobile Engagement 您帳戶設定檔和測試裝置"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: 22832678-3959-4b8c-9fb2-f2ff5974e5d1
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 1d85f0e87c43605f59f6536ae42a7fb6a99ee36b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-your-account-profile-and-test-devices"></a>如何 toomanage 帳戶設定檔和測試裝置
本文說明 hello**首頁**頁面 hello **Mobile Engagement**入口網站。 使用 hello **Mobile Engagement** toomonitor 入口網站和管理您的行動裝置應用程式。 

tooget toohello**我的帳戶**頁面上，按一下您的帳戶上 hello hello 頁面的頂端。

hello 我帳戶 區段中的 UI 是您可以在其中檢視和變更您的帳戶，包括您的設定檔相關聯的 hello 設定並測試裝置識別碼 hello。 這些設定包含項目，也可以透過 hello 裝置 API 存取。

![MyAccount1][7]  

## <a name="profile"></a>設定檔：
您可以檢視或變更下列任何帳戶設定，如下所示。 您也可以提供另一個使用者的權限 toouse hello 從其電子郵件地址為基礎的應用程式[首頁](mobile-engagement-user-interface-home.md)。

![MyAccount2][8]  

## <a name="devices"></a>裝置：
您可以檢視、 新增或移除測試，您可以使用 tootest hello 測試裝置的裝置識別碼傳回您**到達**或**發送**行銷活動。 內容指示如何 toofind hello 裝置識別碼的每個平台的裝置 (iOS、 Android、 Windows Phone 等) 會顯示當您按一下 [新裝置]。 

![MyAccount3][9]  

toouse 推送 API 或 Device API 需要 tooknow 使用者的唯一裝置識別碼 （hello deviceid 參數）。 有數種方式 tooretrieve 它：

1. 從您的後端中，您可以使用 hello 裝置 API tooget hello 識別碼的完整清單裝置 hello 「 取得 」 的功能。
2. 您可以從您的應用程式使用 hello SDK tooget 它。 （在 Android 上，呼叫 hello getDeviceID() 函式的 hello 代理程式類別，並在 iOS 上，閱讀 hello deviceid 屬性 hello 代理程式類別）。
3. 從觸達宣告，如果 hello 與 hello 公告相關聯的動作 URL 包含 hello {deviceid} 模式，它會自動取代為由觸發 hello 動作 hello 裝置 hello 識別項。
   http://<example>.com/registeruser?deviceid={deviceid}&otherparam=myparamdata 將會取代為：http://<example>.com/registeruser?deviceid=XXXXXXXXXXXXXXXX&otherparam=myparamdata 
4. 從觸達 web 宣告，如果 hello hello 公告的 HTML 程式碼包含 hello {deviceid} 模式中，它會自動取代為由顯示 hello web 宣告 hello 裝置 hello 識別碼。
   「以下是我的裝置識別碼: {deviceid}」將會替換為：「以下是我的裝置識別碼: XXXXXXXXXXXXXXXX」
5. 在您的裝置上開啟您的應用程式，然後執行應用程式中已被標記的事件。
   從 [UI-您的應用程式的監視-事件的詳細資料]，尋找 hello 執行 hello 清單所述的事件。
   按一下 toothis hello 監視器中的事件。
   您應該在執行此事件之 hello 裝置 hello 清單中找到您的裝置識別碼。
   然後，您可以複製此裝置識別碼，而其註冊 hello 「 UI-我的帳戶-裝置的新裝置-選取您的裝置平台 」。
   >（請注意，IDFA 已停用 iOS，當 hello 裝置識別碼會隨著 hello 時間變更，如果您解除安裝再重新安裝您的應用程式）。

## <a name="troubleshooting-guide"></a>疑難排解指南
* [疑難排解指南 - 服務][Link 24]

## <a name="see-also"></a>另請參閱
* [UI 文件 – 首頁][Link 13]

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




