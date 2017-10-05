---
title: "Azure Mobile Engagement 使用者介面 - 設定"
description: "了解如何使用 Azure Mobile Engagement 管理應用程式的全域設定"
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
ms.openlocfilehash: af5c81df2b9f288161b38625d3ac2adde8fb195d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-manage-the-global-settings-of-your-application"></a><span data-ttu-id="5cc70-103">如何管理應用程式的全域設定</span><span class="sxs-lookup"><span data-stu-id="5cc70-103">How to manage the global settings of your application</span></span>
<span data-ttu-id="5cc70-104">視應用程式平台和您所擁有的該應用程式權限而定，應用程式中所提供的 [ **設定** ] 功能表選項將有所不同。</span><span class="sxs-lookup"><span data-stu-id="5cc70-104">The **Settings** menu options available for an application vary, depending on the platform of the application and the permissions you have been granted for the application.</span></span> <span data-ttu-id="5cc70-105">設定中包含：[詳細資料]、[專案]、[原生推送]、[推送速度]、 [標記 (應用程式資訊)] 和 [商業壓力]。</span><span class="sxs-lookup"><span data-stu-id="5cc70-105">Settings include the following: Details, Projects, Native Push, Push Speed, Tag (app info), and Commercial Pressure.</span></span> <span data-ttu-id="5cc70-106">[設定] 區段中的 [標記 (應用程式資訊)] 功能表選項可透過您的應用程式 (使用 SDK) 或您的後端 (使用裝置 API) 管理。</span><span class="sxs-lookup"><span data-stu-id="5cc70-106">The Tag (app info) menu option of the Settings section can be managed by your application (using the SDK) or by your backend (using the Device API).</span></span> 

> [!NOTE]
> <span data-ttu-id="5cc70-107">許多 **Mobile Engagement** 入口網站 UI 的區段含有 [顯示說明] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="5cc70-107">Many sections of the **Mobile Engagement** portal UI contain the **SHOW HELP** button.</span></span> <span data-ttu-id="5cc70-108">按該按鈕，可獲得關於區段的詳細內容資訊。</span><span class="sxs-lookup"><span data-stu-id="5cc70-108">Press this button to get more contextual information about a section.</span></span>
> 
> 

## <a name="details"></a><span data-ttu-id="5cc70-109">詳細資料</span><span class="sxs-lookup"><span data-stu-id="5cc70-109">Details</span></span>
<span data-ttu-id="5cc70-110">可讓您變更您應用程式的名稱與說明。檢視您應用程式的擁有者與您的角色權限。</span><span class="sxs-lookup"><span data-stu-id="5cc70-110">Allows you to change the name and description of your application, view the owner of your application and your role permissions.</span></span> 

<span data-ttu-id="5cc70-111">分析組態可讓您檢視或變更每星期的第一天以及保留時間 (以天為單位)。</span><span class="sxs-lookup"><span data-stu-id="5cc70-111">Analytics configuration enables  you to view or change the day weeks start on and the retention time in day(s).</span></span>

  ![settings1][46]

## <a name="projects"></a><span data-ttu-id="5cc70-113">專案</span><span class="sxs-lookup"><span data-stu-id="5cc70-113">Projects</span></span>
<span data-ttu-id="5cc70-114">可讓您選取您要應用程式在其中出現的所有專案。</span><span class="sxs-lookup"><span data-stu-id="5cc70-114">Allows you to select all projects you want your application to appear in.</span></span> 

<span data-ttu-id="5cc70-115">您也可以搜尋專案及檢視您的應用程式所屬之任何專案的名稱、描述、擁有者及您的角色權限。</span><span class="sxs-lookup"><span data-stu-id="5cc70-115">You can also search for a project and view the name, description, owner and your role permissions of any project your application is part of.</span></span>

<span data-ttu-id="5cc70-116">如需詳細資訊，請參閱 [UI 文件 – 首頁][Link 13]</span><span class="sxs-lookup"><span data-stu-id="5cc70-116">For more information, see: [UI Documentation – Home][Link 13]</span></span>

  ![settings3][48]

## <a name="native-push"></a><span data-ttu-id="5cc70-118">原生推送</span><span class="sxs-lookup"><span data-stu-id="5cc70-118">Native Push</span></span>
<span data-ttu-id="5cc70-119">可讓您註冊新憑證來與原生推送搭配使用，或刪除現有憑證。</span><span class="sxs-lookup"><span data-stu-id="5cc70-119">Allows you to register a new certificate or delete and existing certificate for use with native push.</span></span> <span data-ttu-id="5cc70-120">原生推送可讓 Azure Mobile Engagement 在任何時間 (甚至在它沒有執行時) 推送至您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="5cc70-120">Native Push enables Azure Mobile Engagement to push to your application at any time, even when it is not running.</span></span> 

<span data-ttu-id="5cc70-121">在為至少一項原生推送服務提供認證或憑證之後，您可以在建立觸達活動時選擇 [任何時間]，也可以使用 PUSH API 中的 "notifier" 參數。</span><span class="sxs-lookup"><span data-stu-id="5cc70-121">After providing credentials or certificates for at least one Native Push service, you can select "Any time" when creating Reach Campaigns, and also use the "notifier" parameter in the PUSH API.</span></span>

### <a name="apple-push-notification-service-apns"></a><span data-ttu-id="5cc70-122">Apple Push Notification Service (APNS)</span><span class="sxs-lookup"><span data-stu-id="5cc70-122">Apple Push Notification Service (APNS)</span></span>
<span data-ttu-id="5cc70-123">若要讓原生推送使用 Apple Push Notification Service，您必須註冊您的憑證。</span><span class="sxs-lookup"><span data-stu-id="5cc70-123">To enable Native Push using the Apple Push Notification Service you will need to register your certificate.</span></span> <span data-ttu-id="5cc70-124">您將需要指定憑證類型為開發 (DEV) 或生產 (PROD)。</span><span class="sxs-lookup"><span data-stu-id="5cc70-124">You will need to specify the type of certificate as either development (DEV) or production (PROD).</span></span> <span data-ttu-id="5cc70-125">然後您需要上傳您的憑證與密碼。</span><span class="sxs-lookup"><span data-stu-id="5cc70-125">Then you will need upload your certificate and the password.</span></span>

<span data-ttu-id="5cc70-126">如需詳細資訊，請參閱：[SDK 文件 - iOS - 如何準備您的應用程式以使用 Apple 推播通知][Link 5]</span><span class="sxs-lookup"><span data-stu-id="5cc70-126">For more information, see: [SDK Documentation - iOS - How to Prepare your Application for Apple Push notifications][Link 5]</span></span>

![settings4][49]

### <a name="windows-push-notification-service-wpns"></a><span data-ttu-id="5cc70-128">Windows 推播通知服務 (WPNS)</span><span class="sxs-lookup"><span data-stu-id="5cc70-128">Windows Push Notification Service (WPNS)</span></span>
<span data-ttu-id="5cc70-129">若要讓原生推送使用 Windows 推播通知，您必須提供應用程式的憑證。</span><span class="sxs-lookup"><span data-stu-id="5cc70-129">To enable Native Push using Windows Notification Service, you must provide your application's credentials.</span></span> <span data-ttu-id="5cc70-130">您將需要您的封裝安全性識別碼 (SID) 與您的秘密金鑰。</span><span class="sxs-lookup"><span data-stu-id="5cc70-130">You will need your Package security identifier (SID) and your Secret key.</span></span>

![settings5][50]

### <a name="google-cloud-messaging-for-android-gcm"></a><span data-ttu-id="5cc70-132">Google Cloud Messaging for Android (GCM)</span><span class="sxs-lookup"><span data-stu-id="5cc70-132">Google Cloud Messaging for Android (GCM)</span></span>
<span data-ttu-id="5cc70-133">若要讓原生推送使用 GCM，您必須依照 Google 的指示進行。</span><span class="sxs-lookup"><span data-stu-id="5cc70-133">To enable Native Push using GCM, you need to follow the instructions from Google.</span></span> <span data-ttu-id="5cc70-134">然後，您必須貼上在沒有 IP 限制下設定的伺服器簡易 API 金鑰。</span><span class="sxs-lookup"><span data-stu-id="5cc70-134">Then you must paste a server simple API key, configured without IP restrictions.</span></span> <span data-ttu-id="5cc70-135">需要與 SDK for Android 1.12.0 版以上整合。</span><span class="sxs-lookup"><span data-stu-id="5cc70-135">Requires integration with the SDK for Android v1.12.0+.</span></span>

<span data-ttu-id="5cc70-136">如需詳細資訊，請參閱：</span><span class="sxs-lookup"><span data-stu-id="5cc70-136">For more information, see:</span></span> 

* <span data-ttu-id="5cc70-137">[SDK 文件 Android 如何整合 GCM][Link 5]</span><span class="sxs-lookup"><span data-stu-id="5cc70-137">[SDK Documentation Android How to Integrate GCM][Link 5]</span></span>
* [<span data-ttu-id="5cc70-138">Google 開發人員 GCM 指南</span><span class="sxs-lookup"><span data-stu-id="5cc70-138">Google Developer GCM Guide</span></span>](http://developer.android.com/guide/google/gcm/gs.html)

### <a name="amazon-device-messaging-for-android-adm"></a><span data-ttu-id="5cc70-139">Android 的 Amazon 裝置傳訊 (ADM)</span><span class="sxs-lookup"><span data-stu-id="5cc70-139">Amazon Device Messaging for Android (ADM)</span></span>
<span data-ttu-id="5cc70-140">若要讓原生推送使用 ADM，您必須提供由用戶端識別碼和用戶端密碼組成的 <OAuth credentials> (需要與 Android 2.1.0 版以上的 SDK 整合)。</span><span class="sxs-lookup"><span data-stu-id="5cc70-140">To enable Native Push using ADM, you must provide Amazon <OAuth credentials> consisting of a Client ID and Client Secret (Requires integration with SDK for Android v2.1.0+).</span></span>

<span data-ttu-id="5cc70-141">如需詳細資訊，請參閱：</span><span class="sxs-lookup"><span data-stu-id="5cc70-141">For more information, see:</span></span> 

* <span data-ttu-id="5cc70-142">[SDK 文件 Android 如何整合 ADM][Link 5]</span><span class="sxs-lookup"><span data-stu-id="5cc70-142">[SDK Documentation Android How to Integrate ADM][Link 5]</span></span>
* [<span data-ttu-id="5cc70-143">Amazon 開發人員 ADM 文件</span><span class="sxs-lookup"><span data-stu-id="5cc70-143">Amazon Developer ADM Documentation</span></span>](https://developer.amazon.com/sdk/adm/credentials.html#Getting)

![settings6][51]

## <a name="push-speed"></a><span data-ttu-id="5cc70-145">推送速度</span><span class="sxs-lookup"><span data-stu-id="5cc70-145">Push Speed</span></span>
<span data-ttu-id="5cc70-146">顯示您的應用程式目前的推送速度，而且可讓您定義應用程式的推送速度。</span><span class="sxs-lookup"><span data-stu-id="5cc70-146">Shows the current push speed of your application and allows you to define the push speed of your application.</span></span>

  ![settings7][52]

## <a name="tag-app-info"></a><span data-ttu-id="5cc70-148">標記 (應用程式資訊)</span><span class="sxs-lookup"><span data-stu-id="5cc70-148">Tag (app info)</span></span>
![settings11][56]

## <a name="commercial-pressure"></a><span data-ttu-id="5cc70-150">商業壓力</span><span class="sxs-lookup"><span data-stu-id="5cc70-150">Commercial Pressure</span></span>
![settings12][57]

## <a name="see-also"></a><span data-ttu-id="5cc70-152">另請參閱</span><span class="sxs-lookup"><span data-stu-id="5cc70-152">See also</span></span>
* <span data-ttu-id="5cc70-153">[概念][Link 6]</span><span class="sxs-lookup"><span data-stu-id="5cc70-153">[Concepts][Link 6]</span></span>
* <span data-ttu-id="5cc70-154">[疑難排解指南服務][Link 24]</span><span class="sxs-lookup"><span data-stu-id="5cc70-154">[Troubleshooting Guide Service][Link 24]</span></span>

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

