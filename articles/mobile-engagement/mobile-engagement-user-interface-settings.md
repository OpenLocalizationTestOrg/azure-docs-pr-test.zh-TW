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
# <a name="how-toomanage-hello-global-settings-of-your-application"></a><span data-ttu-id="f88cd-103">如何 toomanage hello 應用程式的全域設定</span><span class="sxs-lookup"><span data-stu-id="f88cd-103">How toomanage hello global settings of your application</span></span>
<span data-ttu-id="f88cd-104">hello**設定**功能表選項適用於應用程式會有所不同，視 hello hello 應用程式和 hello 權限，您已獲得 hello 應用程式的平台而定。</span><span class="sxs-lookup"><span data-stu-id="f88cd-104">hello **Settings** menu options available for an application vary, depending on hello platform of hello application and hello permissions you have been granted for hello application.</span></span> <span data-ttu-id="f88cd-105">設定包括下列 hello： 詳細資料、 專案、 原生推送，推入的速度、 標記 （應用程式資訊） 和置入廣告。</span><span class="sxs-lookup"><span data-stu-id="f88cd-105">Settings include hello following: Details, Projects, Native Push, Push Speed, Tag (app info), and Commercial Pressure.</span></span> <span data-ttu-id="f88cd-106">您的應用程式 （使用 hello SDK） 或後端 （使用 hello 裝置 API），可以管理 hello hello 設定 區段中的標記 （應用程式資訊） 功能表選項。</span><span class="sxs-lookup"><span data-stu-id="f88cd-106">hello Tag (app info) menu option of hello Settings section can be managed by your application (using hello SDK) or by your backend (using hello Device API).</span></span> 

> [!NOTE]
> <span data-ttu-id="f88cd-107">多區段的 hello **Mobile Engagement**入口網站 UI 包含 hello**顯示說明** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="f88cd-107">Many sections of hello **Mobile Engagement** portal UI contain hello **SHOW HELP** button.</span></span> <span data-ttu-id="f88cd-108">按此按鈕 tooget 區段內容詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="f88cd-108">Press this button tooget more contextual information about a section.</span></span>
> 
> 

## <a name="details"></a><span data-ttu-id="f88cd-109">詳細資料</span><span class="sxs-lookup"><span data-stu-id="f88cd-109">Details</span></span>
<span data-ttu-id="f88cd-110">可讓您 toochange hello 名稱和描述您的應用程式、 應用程式和您的角色權限檢視 hello 擁有者。</span><span class="sxs-lookup"><span data-stu-id="f88cd-110">Allows you toochange hello name and description of your application, view hello owner of your application and your role permissions.</span></span> 

<span data-ttu-id="f88cd-111">分析設定可讓您 tooview 或變更 hello 週開始日 hello 天中的保留時間。</span><span class="sxs-lookup"><span data-stu-id="f88cd-111">Analytics configuration enables  you tooview or change hello day weeks start on and hello retention time in day(s).</span></span>

  ![settings1][46]

## <a name="projects"></a><span data-ttu-id="f88cd-113">專案</span><span class="sxs-lookup"><span data-stu-id="f88cd-113">Projects</span></span>
<span data-ttu-id="f88cd-114">可讓您 tooselect 所有專案中您都要應用程式 tooappear。</span><span class="sxs-lookup"><span data-stu-id="f88cd-114">Allows you tooselect all projects you want your application tooappear in.</span></span> 

<span data-ttu-id="f88cd-115">您也可以搜尋專案和檢視 hello 名稱、 描述、 擁有者，且您的角色權限，任何專案的應用程式的一部分。</span><span class="sxs-lookup"><span data-stu-id="f88cd-115">You can also search for a project and view hello name, description, owner and your role permissions of any project your application is part of.</span></span>

<span data-ttu-id="f88cd-116">如需詳細資訊，請參閱 [UI 文件 – 首頁][Link 13]</span><span class="sxs-lookup"><span data-stu-id="f88cd-116">For more information, see: [UI Documentation – Home][Link 13]</span></span>

  ![settings3][48]

## <a name="native-push"></a><span data-ttu-id="f88cd-118">原生推送</span><span class="sxs-lookup"><span data-stu-id="f88cd-118">Native Push</span></span>
<span data-ttu-id="f88cd-119">可讓您 tooregister 新憑證或刪除與現有憑證進行使用其原生推送。</span><span class="sxs-lookup"><span data-stu-id="f88cd-119">Allows you tooregister a new certificate or delete and existing certificate for use with native push.</span></span> <span data-ttu-id="f88cd-120">原生推送，可讓 Azure Mobile Engagement toopush tooyour 應用程式在任何時間，即使未執行。</span><span class="sxs-lookup"><span data-stu-id="f88cd-120">Native Push enables Azure Mobile Engagement toopush tooyour application at any time, even when it is not running.</span></span> 

<span data-ttu-id="f88cd-121">至少一個原生推送服務提供的認證或憑證之後, 您可以選取 [任何時間] 時建立觸達活動，以及使用 hello 「 通知 」 參數 hello 推送 API 中。</span><span class="sxs-lookup"><span data-stu-id="f88cd-121">After providing credentials or certificates for at least one Native Push service, you can select "Any time" when creating Reach Campaigns, and also use hello "notifier" parameter in hello PUSH API.</span></span>

### <a name="apple-push-notification-service-apns"></a><span data-ttu-id="f88cd-122">Apple Push Notification Service (APNS)</span><span class="sxs-lookup"><span data-stu-id="f88cd-122">Apple Push Notification Service (APNS)</span></span>
<span data-ttu-id="f88cd-123">原生推送使用 tooenable hello Apple Push Notification Service 必須 tooregister 您的憑證。</span><span class="sxs-lookup"><span data-stu-id="f88cd-123">tooenable Native Push using hello Apple Push Notification Service you will need tooregister your certificate.</span></span> <span data-ttu-id="f88cd-124">您將需要 toospecify hello 做為開發 (DEV) 或實際執行環境 （生產環境） 的憑證類型。</span><span class="sxs-lookup"><span data-stu-id="f88cd-124">You will need toospecify hello type of certificate as either development (DEV) or production (PROD).</span></span> <span data-ttu-id="f88cd-125">然後您會需要上傳憑證和 hello 的密碼。</span><span class="sxs-lookup"><span data-stu-id="f88cd-125">Then you will need upload your certificate and hello password.</span></span>

<span data-ttu-id="f88cd-126">如需詳細資訊，請參閱： [SDK 文件-iOS-如何 tooPrepare Apple 推播通知您的應用程式][Link 5]</span><span class="sxs-lookup"><span data-stu-id="f88cd-126">For more information, see: [SDK Documentation - iOS - How tooPrepare your Application for Apple Push notifications][Link 5]</span></span>

![settings4][49]

### <a name="windows-push-notification-service-wpns"></a><span data-ttu-id="f88cd-128">Windows 推播通知服務 (WPNS)</span><span class="sxs-lookup"><span data-stu-id="f88cd-128">Windows Push Notification Service (WPNS)</span></span>
<span data-ttu-id="f88cd-129">tooenable 使用 Windows 通知服務的原生推送，您必須提供應用程式的認證。</span><span class="sxs-lookup"><span data-stu-id="f88cd-129">tooenable Native Push using Windows Notification Service, you must provide your application's credentials.</span></span> <span data-ttu-id="f88cd-130">您將需要您的封裝安全性識別碼 (SID) 與您的秘密金鑰。</span><span class="sxs-lookup"><span data-stu-id="f88cd-130">You will need your Package security identifier (SID) and your Secret key.</span></span>

![settings5][50]

### <a name="google-cloud-messaging-for-android-gcm"></a><span data-ttu-id="f88cd-132">Google Cloud Messaging for Android (GCM)</span><span class="sxs-lookup"><span data-stu-id="f88cd-132">Google Cloud Messaging for Android (GCM)</span></span>
<span data-ttu-id="f88cd-133">原生推送使用 GCM，您需要將來自 Google 的 toofollow hello 指示 tooenable。</span><span class="sxs-lookup"><span data-stu-id="f88cd-133">tooenable Native Push using GCM, you need toofollow hello instructions from Google.</span></span> <span data-ttu-id="f88cd-134">然後，您必須貼上在沒有 IP 限制下設定的伺服器簡易 API 金鑰。</span><span class="sxs-lookup"><span data-stu-id="f88cd-134">Then you must paste a server simple API key, configured without IP restrictions.</span></span> <span data-ttu-id="f88cd-135">Android v1.12.0 + 需要與 hello SDK 整合。</span><span class="sxs-lookup"><span data-stu-id="f88cd-135">Requires integration with hello SDK for Android v1.12.0+.</span></span>

<span data-ttu-id="f88cd-136">如需詳細資訊，請參閱：</span><span class="sxs-lookup"><span data-stu-id="f88cd-136">For more information, see:</span></span> 

* <span data-ttu-id="f88cd-137">[SDK 文件 Android 如何 tooIntegrate GCM][Link 5]</span><span class="sxs-lookup"><span data-stu-id="f88cd-137">[SDK Documentation Android How tooIntegrate GCM][Link 5]</span></span>
* [<span data-ttu-id="f88cd-138">Google 開發人員 GCM 指南</span><span class="sxs-lookup"><span data-stu-id="f88cd-138">Google Developer GCM Guide</span></span>](http://developer.android.com/guide/google/gcm/gs.html)

### <a name="amazon-device-messaging-for-android-adm"></a><span data-ttu-id="f88cd-139">Android 的 Amazon 裝置傳訊 (ADM)</span><span class="sxs-lookup"><span data-stu-id="f88cd-139">Amazon Device Messaging for Android (ADM)</span></span>
<span data-ttu-id="f88cd-140">使用 ADM tooenable 原生推送，您必須提供 Amazon<OAuth credentials>用戶端識別碼和用戶端密碼 （需要與 SDK 相整合的 Android v2.1.0 +） 所組成。</span><span class="sxs-lookup"><span data-stu-id="f88cd-140">tooenable Native Push using ADM, you must provide Amazon <OAuth credentials> consisting of a Client ID and Client Secret (Requires integration with SDK for Android v2.1.0+).</span></span>

<span data-ttu-id="f88cd-141">如需詳細資訊，請參閱：</span><span class="sxs-lookup"><span data-stu-id="f88cd-141">For more information, see:</span></span> 

* <span data-ttu-id="f88cd-142">[SDK 文件 Android 如何 tooIntegrate ADM][Link 5]</span><span class="sxs-lookup"><span data-stu-id="f88cd-142">[SDK Documentation Android How tooIntegrate ADM][Link 5]</span></span>
* [<span data-ttu-id="f88cd-143">Amazon 開發人員 ADM 文件</span><span class="sxs-lookup"><span data-stu-id="f88cd-143">Amazon Developer ADM Documentation</span></span>](https://developer.amazon.com/sdk/adm/credentials.html#Getting)

![settings6][51]

## <a name="push-speed"></a><span data-ttu-id="f88cd-145">推送速度</span><span class="sxs-lookup"><span data-stu-id="f88cd-145">Push Speed</span></span>
<span data-ttu-id="f88cd-146">顯示應用程式的 hello 目前推送速度，並可讓您的應用程式的 toodefine hello 推送速度。</span><span class="sxs-lookup"><span data-stu-id="f88cd-146">Shows hello current push speed of your application and allows you toodefine hello push speed of your application.</span></span>

  ![settings7][52]

## <a name="tag-app-info"></a><span data-ttu-id="f88cd-148">標記 (應用程式資訊)</span><span class="sxs-lookup"><span data-stu-id="f88cd-148">Tag (app info)</span></span>
![settings11][56]

## <a name="commercial-pressure"></a><span data-ttu-id="f88cd-150">商業壓力</span><span class="sxs-lookup"><span data-stu-id="f88cd-150">Commercial Pressure</span></span>
![settings12][57]

## <a name="see-also"></a><span data-ttu-id="f88cd-152">另請參閱</span><span class="sxs-lookup"><span data-stu-id="f88cd-152">See also</span></span>
* <span data-ttu-id="f88cd-153">[概念][Link 6]</span><span class="sxs-lookup"><span data-stu-id="f88cd-153">[Concepts][Link 6]</span></span>
* <span data-ttu-id="f88cd-154">[疑難排解指南服務][Link 24]</span><span class="sxs-lookup"><span data-stu-id="f88cd-154">[Troubleshooting Guide Service][Link 24]</span></span>

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

