---
title: "Azure Mobile Engagement 使用者介面 - 我的帳戶"
description: "了解如何使用 Azure Mobile Engagement 管理帳戶設定檔和測試裝置"
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
ms.openlocfilehash: 4e463e973dcfa1faa7b08e4738192161980b3aa2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-manage-your-account-profile-and-test-devices"></a><span data-ttu-id="a426e-103">如何管理帳戶設定檔和測試裝置</span><span class="sxs-lookup"><span data-stu-id="a426e-103">How to manage your account profile and test devices</span></span>
<span data-ttu-id="a426e-104">本文說明 **Mobile Engagement** 入口網站的**首頁**。</span><span class="sxs-lookup"><span data-stu-id="a426e-104">This article describes the **Home** page of the **Mobile Engagement** portal.</span></span> <span data-ttu-id="a426e-105">使用 **Mobile Engagement** 入口網站可監視與管理您的行動應用程式。</span><span class="sxs-lookup"><span data-stu-id="a426e-105">You use the **Mobile Engagement** portal to monitor and manage your mobile apps.</span></span> 

<span data-ttu-id="a426e-106">若要前往 [我的帳戶]  頁面上，按一下您位於頁面頂端的帳戶。</span><span class="sxs-lookup"><span data-stu-id="a426e-106">To get to the **my account** page, click on your account on the top of the page.</span></span>

<span data-ttu-id="a426e-107">您可以在 UI 的 [我的帳戶] 區段檢視和變更與您帳戶相關聯的設定，包括您的設定檔設定和測試裝置識別碼。</span><span class="sxs-lookup"><span data-stu-id="a426e-107">The My Account section of the UI is where you can view and change the settings associated with your account, including your Profile settings and test Device IDs.</span></span> <span data-ttu-id="a426e-108">這些設定所包含的項目，也可以透過裝置 API 存取。</span><span class="sxs-lookup"><span data-stu-id="a426e-108">These settings contain items that can also be accessed via the Device API.</span></span>

![MyAccount1][7]  

## <a name="profile"></a><span data-ttu-id="a426e-110">設定檔：</span><span class="sxs-lookup"><span data-stu-id="a426e-110">Profile:</span></span>
<span data-ttu-id="a426e-111">您可以檢視或變更下列任何帳戶設定，如下所示。</span><span class="sxs-lookup"><span data-stu-id="a426e-111">You can view or change any of your account settings shown below.</span></span> <span data-ttu-id="a426e-112">您也可以根據使用者的電子郵件地址，從 [首頁](mobile-engagement-user-interface-home.md)授與其他使用者使用您應用程式的權限。</span><span class="sxs-lookup"><span data-stu-id="a426e-112">You can also give another user permission to use your application based on their e-mail address from the [Home](mobile-engagement-user-interface-home.md).</span></span>

![MyAccount2][8]  

## <a name="devices"></a><span data-ttu-id="a426e-114">裝置：</span><span class="sxs-lookup"><span data-stu-id="a426e-114">Devices:</span></span>
<span data-ttu-id="a426e-115">您可以檢視、新增或移除用來測試**觸達**或**推送**活動之測試裝置的測試裝置識別碼。</span><span class="sxs-lookup"><span data-stu-id="a426e-115">You can view, add, or remove test Device ID's of the test devices that you can use to test your **reach** or **push** campaigns.</span></span> <span data-ttu-id="a426e-116">當您按一下 [新裝置] 時，會顯示如何針對每個平台 (iOS、Android、Windows Phone 等) 尋找裝置之裝置識別碼的內容說明。</span><span class="sxs-lookup"><span data-stu-id="a426e-116">Contextual instructions for how to find the Device ID of devices for each platform (iOS, Android, Windows Phone, etc.) are displayed when you click "New Device".</span></span> 

![MyAccount3][9]  

<span data-ttu-id="a426e-118">若要使用「推送 API」或「裝置 API」，您需要知道使用者的唯一裝置識別碼 (deviceid 參數)。</span><span class="sxs-lookup"><span data-stu-id="a426e-118">To use Push API or Device API you need to know your users' unique device identifier (the deviceid parameter).</span></span> <span data-ttu-id="a426e-119">有幾種方法可以取得此識別碼：</span><span class="sxs-lookup"><span data-stu-id="a426e-119">There are several ways to retrieve it:</span></span>

1. <span data-ttu-id="a426e-120">從您的後端，可以使用裝置 API 的 "Get" 功能來取得裝置識別碼的完整清單。</span><span class="sxs-lookup"><span data-stu-id="a426e-120">From your backend, you can use the "Get" feature of the Device API to get the full list of device identifiers.</span></span>
2. <span data-ttu-id="a426e-121">從您的應用程式，可以使用 SDK 取得</span><span class="sxs-lookup"><span data-stu-id="a426e-121">From your app, you can use the SDK to get it.</span></span> <span data-ttu-id="a426e-122">(在 Android 上，呼叫 Agent 類別的 getDeviceID() 函數；在 iOS 上，讀取 Agent 類別的 deviceid 屬性)。</span><span class="sxs-lookup"><span data-stu-id="a426e-122">(On Android, call the getDeviceID() function of the Agent class, and on iOS, read the deviceid property of the Agent class.)</span></span>
3. <span data-ttu-id="a426e-123">在觸達公告中，如果與公告相關聯的動作 URL 包含 {deviceid} 模式，則會自動替換為觸發動作的裝置識別碼。</span><span class="sxs-lookup"><span data-stu-id="a426e-123">From a Reach announcement, if the action URL associated with the announcement contains the {deviceid} pattern, it will be automatically replaced by the identifier of the device triggering the action.</span></span>
   <span data-ttu-id="a426e-124">http://<example>.com/registeruser?deviceid={deviceid}&otherparam=myparamdata 將會取代為：http://<example>.com/registeruser?deviceid=XXXXXXXXXXXXXXXX&otherparam=myparamdata</span><span class="sxs-lookup"><span data-stu-id="a426e-124">http://<example>.com/registeruser?deviceid={deviceid}&otherparam=myparamdata will be replaced by: http://<example>.com/registeruser?deviceid=XXXXXXXXXXXXXXXX&otherparam=myparamdata</span></span> 
4. <span data-ttu-id="a426e-125">從觸達 Web 宣告，如果宣告的 HTML 程式碼包含 {deviceid} 模式，則會自動替換為顯示 Web 通知的裝置識別碼。</span><span class="sxs-lookup"><span data-stu-id="a426e-125">From a Reach web announcement, if the HTML code of the announcement contains the {deviceid} pattern, it will be automatically replaced by the identifier of the device displaying the web announcement.</span></span>
   <span data-ttu-id="a426e-126">「以下是我的裝置識別碼: {deviceid}」將會替換為：「以下是我的裝置識別碼: XXXXXXXXXXXXXXXX」</span><span class="sxs-lookup"><span data-stu-id="a426e-126">Here is my device identifier: {deviceid} will be replaced by: Here is my device identifier: XXXXXXXXXXXXXXXX</span></span>
5. <span data-ttu-id="a426e-127">在您的裝置上開啟您的應用程式，然後執行應用程式中已被標記的事件。</span><span class="sxs-lookup"><span data-stu-id="a426e-127">Open your application on your device and perform an Event in your app which has been tagged.</span></span>
   <span data-ttu-id="a426e-128">依序從 UI - 您的應用程式 - [監視] - [事件] - [詳細資料]，在清單中尋找執行的事件。</span><span class="sxs-lookup"><span data-stu-id="a426e-128">From "UI - your app - Monitor - Events - Details", find the Event you performed in the list.</span></span>
   <span data-ttu-id="a426e-129">在 [監視] 中按一下此事件。</span><span class="sxs-lookup"><span data-stu-id="a426e-129">Click to this event in the Monitor.</span></span>
   <span data-ttu-id="a426e-130">您應該會在已執行此事件的裝置清單中找到裝置識別碼。</span><span class="sxs-lookup"><span data-stu-id="a426e-130">You should find your Device ID in the list of the devices that have performed this event.</span></span>
   <span data-ttu-id="a426e-131">然後，您就可以複製此裝置識別碼，並且依序在 UI - [我的帳戶] - [裝置] - [新裝置] - [選取您的裝置平台] 中註冊此識別碼。</span><span class="sxs-lookup"><span data-stu-id="a426e-131">Then, you can copy this Device ID and register it in the "UI - My Account - Devices - New Device - Select your device platform".</span></span>
   ><span data-ttu-id="a426e-132">(請注意，當 iOS 停用 IDFA 時，如果您解除安裝後又重新安裝您的應用程式，裝置識別碼可能會隨時間而變更)。</span><span class="sxs-lookup"><span data-stu-id="a426e-132">(Be aware that when IDFA is disabled for iOS, the Device ID may change over the time if you uninstall and reinstall your app.)</span></span>

## <a name="troubleshooting-guide"></a><span data-ttu-id="a426e-133">疑難排解指南</span><span class="sxs-lookup"><span data-stu-id="a426e-133">Troubleshooting Guide</span></span>
* <span data-ttu-id="a426e-134">[疑難排解指南 - 服務][Link 24]</span><span class="sxs-lookup"><span data-stu-id="a426e-134">[Troubleshooting Guide - Service][Link 24]</span></span>

## <a name="see-also"></a><span data-ttu-id="a426e-135">另請參閱</span><span class="sxs-lookup"><span data-stu-id="a426e-135">See also</span></span>
* <span data-ttu-id="a426e-136">[UI 文件 – 首頁][Link 13]</span><span class="sxs-lookup"><span data-stu-id="a426e-136">[UI Documentation - Home][Link 13]</span></span>

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




