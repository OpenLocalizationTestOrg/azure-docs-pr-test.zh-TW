---
title: "aaaAzure Mobile Engagement 使用者介面的設定"
description: "了解如何 toomanage hello 使用 Azure Mobile Engagement 應用程式的全域設定"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: 858f4cb4-14de-4bb5-826f-28cadbfc928b
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 02d4a36c591fc5e097410b7e931d1c9ce81d68d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-hello-global-settings-of-your-application"></a>如何 toomanage hello 應用程式的全域設定
hello**設定**功能表選項適用於應用程式會有所不同，視 hello hello 應用程式和 hello 權限，您已獲得 hello 應用程式的平台而定。 設定包括下列 hello： 詳細資料、 專案、 原生推送，推入的速度、 標記 （應用程式資訊） 和置入廣告。 您的應用程式 （使用 hello SDK） 或後端 （使用 hello 裝置 API），可以管理 hello hello 設定 區段中的標記 （應用程式資訊） 功能表選項。 

> [!NOTE]
> 多區段的 hello **Mobile Engagement**入口網站 UI 包含 hello**顯示說明** 按鈕。 按此按鈕 tooget 區段內容詳細資訊。
> 
> 

## <a name="details"></a>詳細資料
可讓您 toochange hello 名稱和描述您的應用程式、 應用程式和您的角色權限檢視 hello 擁有者。 

分析設定可讓您 tooview 或變更 hello 週開始日 hello 天中的保留時間。

  ![settings1][46]

## <a name="projects"></a>專案
可讓您 tooselect 所有專案中您都要應用程式 tooappear。 

您也可以搜尋專案和檢視 hello 名稱、 描述、 擁有者，且您的角色權限，任何專案的應用程式的一部分。

如需詳細資訊，請參閱 [UI 文件 – 首頁][Link 13]

  ![settings3][48]

## <a name="native-push"></a>原生推送
可讓您 tooregister 新憑證或刪除與現有憑證進行使用其原生推送。 原生推送，可讓 Azure Mobile Engagement toopush tooyour 應用程式在任何時間，即使未執行。 

至少一個原生推送服務提供的認證或憑證之後, 您可以選取 [任何時間] 時建立觸達活動，以及使用 hello 「 通知 」 參數 hello 推送 API 中。

### <a name="apple-push-notification-service-apns"></a>Apple Push Notification Service (APNS)
原生推送使用 tooenable hello Apple Push Notification Service 必須 tooregister 您的憑證。 您將需要 toospecify hello 做為開發 (DEV) 或實際執行環境 （生產環境） 的憑證類型。 然後您會需要上傳憑證和 hello 的密碼。

如需詳細資訊，請參閱： [SDK 文件-iOS-如何 tooPrepare Apple 推播通知您的應用程式][Link 5]

![settings4][49]

### <a name="windows-push-notification-service-wpns"></a>Windows 推播通知服務 (WPNS)
tooenable 使用 Windows 通知服務的原生推送，您必須提供應用程式的認證。 您將需要您的封裝安全性識別碼 (SID) 與您的秘密金鑰。

![settings5][50]

### <a name="google-cloud-messaging-for-android-gcm"></a>Google Cloud Messaging for Android (GCM)
原生推送使用 GCM，您需要將來自 Google 的 toofollow hello 指示 tooenable。 然後，您必須貼上在沒有 IP 限制下設定的伺服器簡易 API 金鑰。 Android v1.12.0 + 需要與 hello SDK 整合。

如需詳細資訊，請參閱： 

* [SDK 文件 Android 如何 tooIntegrate GCM][Link 5]
* [Google 開發人員 GCM 指南](http://developer.android.com/guide/google/gcm/gs.html)

### <a name="amazon-device-messaging-for-android-adm"></a>Android 的 Amazon 裝置傳訊 (ADM)
使用 ADM tooenable 原生推送，您必須提供 Amazon<OAuth credentials>用戶端識別碼和用戶端密碼 （需要與 SDK 相整合的 Android v2.1.0 +） 所組成。

如需詳細資訊，請參閱： 

* [SDK 文件 Android 如何 tooIntegrate ADM][Link 5]
* [Amazon 開發人員 ADM 文件](https://developer.amazon.com/sdk/adm/credentials.html#Getting)

![settings6][51]

## <a name="push-speed"></a>推送速度
顯示應用程式的 hello 目前推送速度，並可讓您的應用程式的 toodefine hello 推送速度。

  ![settings7][52]

## <a name="tag-app-info"></a>標記 (應用程式資訊)
![settings11][56]

## <a name="commercial-pressure"></a>商業壓力
![settings12][57]

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

