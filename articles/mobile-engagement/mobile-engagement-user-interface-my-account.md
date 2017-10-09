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
# <a name="how-toomanage-your-account-profile-and-test-devices"></a><span data-ttu-id="6a71b-103">如何 toomanage 帳戶設定檔和測試裝置</span><span class="sxs-lookup"><span data-stu-id="6a71b-103">How toomanage your account profile and test devices</span></span>
<span data-ttu-id="6a71b-104">本文說明 hello**首頁**頁面 hello **Mobile Engagement**入口網站。</span><span class="sxs-lookup"><span data-stu-id="6a71b-104">This article describes hello **Home** page of hello **Mobile Engagement** portal.</span></span> <span data-ttu-id="6a71b-105">使用 hello **Mobile Engagement** toomonitor 入口網站和管理您的行動裝置應用程式。</span><span class="sxs-lookup"><span data-stu-id="6a71b-105">You use hello **Mobile Engagement** portal toomonitor and manage your mobile apps.</span></span> 

<span data-ttu-id="6a71b-106">tooget toohello**我的帳戶**頁面上，按一下您的帳戶上 hello hello 頁面的頂端。</span><span class="sxs-lookup"><span data-stu-id="6a71b-106">tooget toohello **my account** page, click on your account on hello top of hello page.</span></span>

<span data-ttu-id="6a71b-107">hello 我帳戶 區段中的 UI 是您可以在其中檢視和變更您的帳戶，包括您的設定檔相關聯的 hello 設定並測試裝置識別碼 hello。</span><span class="sxs-lookup"><span data-stu-id="6a71b-107">hello My Account section of hello UI is where you can view and change hello settings associated with your account, including your Profile settings and test Device IDs.</span></span> <span data-ttu-id="6a71b-108">這些設定包含項目，也可以透過 hello 裝置 API 存取。</span><span class="sxs-lookup"><span data-stu-id="6a71b-108">These settings contain items that can also be accessed via hello Device API.</span></span>

![MyAccount1][7]  

## <a name="profile"></a><span data-ttu-id="6a71b-110">設定檔：</span><span class="sxs-lookup"><span data-stu-id="6a71b-110">Profile:</span></span>
<span data-ttu-id="6a71b-111">您可以檢視或變更下列任何帳戶設定，如下所示。</span><span class="sxs-lookup"><span data-stu-id="6a71b-111">You can view or change any of your account settings shown below.</span></span> <span data-ttu-id="6a71b-112">您也可以提供另一個使用者的權限 toouse hello 從其電子郵件地址為基礎的應用程式[首頁](mobile-engagement-user-interface-home.md)。</span><span class="sxs-lookup"><span data-stu-id="6a71b-112">You can also give another user permission toouse your application based on their e-mail address from hello [Home](mobile-engagement-user-interface-home.md).</span></span>

![MyAccount2][8]  

## <a name="devices"></a><span data-ttu-id="6a71b-114">裝置：</span><span class="sxs-lookup"><span data-stu-id="6a71b-114">Devices:</span></span>
<span data-ttu-id="6a71b-115">您可以檢視、 新增或移除測試，您可以使用 tootest hello 測試裝置的裝置識別碼傳回您**到達**或**發送**行銷活動。</span><span class="sxs-lookup"><span data-stu-id="6a71b-115">You can view, add, or remove test Device ID's of hello test devices that you can use tootest your **reach** or **push** campaigns.</span></span> <span data-ttu-id="6a71b-116">內容指示如何 toofind hello 裝置識別碼的每個平台的裝置 (iOS、 Android、 Windows Phone 等) 會顯示當您按一下 [新裝置]。</span><span class="sxs-lookup"><span data-stu-id="6a71b-116">Contextual instructions for how toofind hello Device ID of devices for each platform (iOS, Android, Windows Phone, etc.) are displayed when you click "New Device".</span></span> 

![MyAccount3][9]  

<span data-ttu-id="6a71b-118">toouse 推送 API 或 Device API 需要 tooknow 使用者的唯一裝置識別碼 （hello deviceid 參數）。</span><span class="sxs-lookup"><span data-stu-id="6a71b-118">toouse Push API or Device API you need tooknow your users' unique device identifier (hello deviceid parameter).</span></span> <span data-ttu-id="6a71b-119">有數種方式 tooretrieve 它：</span><span class="sxs-lookup"><span data-stu-id="6a71b-119">There are several ways tooretrieve it:</span></span>

1. <span data-ttu-id="6a71b-120">從您的後端中，您可以使用 hello 裝置 API tooget hello 識別碼的完整清單裝置 hello 「 取得 」 的功能。</span><span class="sxs-lookup"><span data-stu-id="6a71b-120">From your backend, you can use hello "Get" feature of hello Device API tooget hello full list of device identifiers.</span></span>
2. <span data-ttu-id="6a71b-121">您可以從您的應用程式使用 hello SDK tooget 它。</span><span class="sxs-lookup"><span data-stu-id="6a71b-121">From your app, you can use hello SDK tooget it.</span></span> <span data-ttu-id="6a71b-122">（在 Android 上，呼叫 hello getDeviceID() 函式的 hello 代理程式類別，並在 iOS 上，閱讀 hello deviceid 屬性 hello 代理程式類別）。</span><span class="sxs-lookup"><span data-stu-id="6a71b-122">(On Android, call hello getDeviceID() function of hello Agent class, and on iOS, read hello deviceid property of hello Agent class.)</span></span>
3. <span data-ttu-id="6a71b-123">從觸達宣告，如果 hello 與 hello 公告相關聯的動作 URL 包含 hello {deviceid} 模式，它會自動取代為由觸發 hello 動作 hello 裝置 hello 識別項。</span><span class="sxs-lookup"><span data-stu-id="6a71b-123">From a Reach announcement, if hello action URL associated with hello announcement contains hello {deviceid} pattern, it will be automatically replaced by hello identifier of hello device triggering hello action.</span></span>
   <span data-ttu-id="6a71b-124">http://<example>.com/registeruser?deviceid={deviceid}&otherparam=myparamdata 將會取代為：http://<example>.com/registeruser?deviceid=XXXXXXXXXXXXXXXX&otherparam=myparamdata</span><span class="sxs-lookup"><span data-stu-id="6a71b-124">http://<example>.com/registeruser?deviceid={deviceid}&otherparam=myparamdata will be replaced by: http://<example>.com/registeruser?deviceid=XXXXXXXXXXXXXXXX&otherparam=myparamdata</span></span> 
4. <span data-ttu-id="6a71b-125">從觸達 web 宣告，如果 hello hello 公告的 HTML 程式碼包含 hello {deviceid} 模式中，它會自動取代為由顯示 hello web 宣告 hello 裝置 hello 識別碼。</span><span class="sxs-lookup"><span data-stu-id="6a71b-125">From a Reach web announcement, if hello HTML code of hello announcement contains hello {deviceid} pattern, it will be automatically replaced by hello identifier of hello device displaying hello web announcement.</span></span>
   <span data-ttu-id="6a71b-126">「以下是我的裝置識別碼: {deviceid}」將會替換為：「以下是我的裝置識別碼: XXXXXXXXXXXXXXXX」</span><span class="sxs-lookup"><span data-stu-id="6a71b-126">Here is my device identifier: {deviceid} will be replaced by: Here is my device identifier: XXXXXXXXXXXXXXXX</span></span>
5. <span data-ttu-id="6a71b-127">在您的裝置上開啟您的應用程式，然後執行應用程式中已被標記的事件。</span><span class="sxs-lookup"><span data-stu-id="6a71b-127">Open your application on your device and perform an Event in your app which has been tagged.</span></span>
   <span data-ttu-id="6a71b-128">從 [UI-您的應用程式的監視-事件的詳細資料]，尋找 hello 執行 hello 清單所述的事件。</span><span class="sxs-lookup"><span data-stu-id="6a71b-128">From "UI - your app - Monitor - Events - Details", find hello Event you performed in hello list.</span></span>
   <span data-ttu-id="6a71b-129">按一下 toothis hello 監視器中的事件。</span><span class="sxs-lookup"><span data-stu-id="6a71b-129">Click toothis event in hello Monitor.</span></span>
   <span data-ttu-id="6a71b-130">您應該在執行此事件之 hello 裝置 hello 清單中找到您的裝置識別碼。</span><span class="sxs-lookup"><span data-stu-id="6a71b-130">You should find your Device ID in hello list of hello devices that have performed this event.</span></span>
   <span data-ttu-id="6a71b-131">然後，您可以複製此裝置識別碼，而其註冊 hello 「 UI-我的帳戶-裝置的新裝置-選取您的裝置平台 」。</span><span class="sxs-lookup"><span data-stu-id="6a71b-131">Then, you can copy this Device ID and register it in hello "UI - My Account - Devices - New Device - Select your device platform".</span></span>
   ><span data-ttu-id="6a71b-132">（請注意，IDFA 已停用 iOS，當 hello 裝置識別碼會隨著 hello 時間變更，如果您解除安裝再重新安裝您的應用程式）。</span><span class="sxs-lookup"><span data-stu-id="6a71b-132">(Be aware that when IDFA is disabled for iOS, hello Device ID may change over hello time if you uninstall and reinstall your app.)</span></span>

## <a name="troubleshooting-guide"></a><span data-ttu-id="6a71b-133">疑難排解指南</span><span class="sxs-lookup"><span data-stu-id="6a71b-133">Troubleshooting Guide</span></span>
* <span data-ttu-id="6a71b-134">[疑難排解指南 - 服務][Link 24]</span><span class="sxs-lookup"><span data-stu-id="6a71b-134">[Troubleshooting Guide - Service][Link 24]</span></span>

## <a name="see-also"></a><span data-ttu-id="6a71b-135">另請參閱</span><span class="sxs-lookup"><span data-stu-id="6a71b-135">See also</span></span>
* <span data-ttu-id="6a71b-136">[UI 文件 – 首頁][Link 13]</span><span class="sxs-lookup"><span data-stu-id="6a71b-136">[UI Documentation - Home][Link 13]</span></span>

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




