---
title: "aaaAzure Mobile Engagement 使用者介面的監視"
description: "深入了解如何使用 Azure Mobile Engagement 應用程式的 toomonitor 即時資料"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: b91ad89a-b89d-4377-abb0-cc2d16a2836d
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 3a581e4166bc88e6ee7aa784d4047c94533685b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomonitor-real-time-data-about-your-application"></a><span data-ttu-id="f8705-103">如何 toomonitor 您的應用程式的即時資料</span><span class="sxs-lookup"><span data-stu-id="f8705-103">How toomonitor real-time data about your application</span></span>
<span data-ttu-id="f8705-104">本文說明 hello**監視器** 索引標籤的 hello **Mobile Engagement**入口網站。</span><span class="sxs-lookup"><span data-stu-id="f8705-104">This article describes hello **MONITOR** tab of hello **Mobile Engagement** portal.</span></span> <span data-ttu-id="f8705-105">使用 hello **Mobile Engagement** toomonitor 入口網站和管理您的行動裝置應用程式。</span><span class="sxs-lookup"><span data-stu-id="f8705-105">You use hello **Mobile Engagement** portal toomonitor and manage your mobile apps.</span></span> <span data-ttu-id="f8705-106">請注意使用 hello 入口網站，您必須先 toocreate 該 toostart **Azure Mobile Engagement**帳戶。</span><span class="sxs-lookup"><span data-stu-id="f8705-106">Note that toostart using hello portal you first need toocreate an **Azure Mobile Engagement** account.</span></span> 

<span data-ttu-id="f8705-107">hello 監視器 hello UI 段提供即時分析的資訊，並讓您有 tooset 警示時到達臨界值對於大多數的 hello 相同資訊可在過去在 hello[分析](mobile-engagement-user-interface-analytics.md)區段hello UI。</span><span class="sxs-lookup"><span data-stu-id="f8705-107">hello Monitor section of hello UI provides real-time analytics information and allows you tooset alerts when thresholds are reached for most of hello same information that is available historically in hello [ANALYTICS](mobile-engagement-user-interface-analytics.md) section of hello UI.</span></span> <span data-ttu-id="f8705-108">請參閱 hello**詞彙**> 一節中 hello[概念](http://go.microsoft.com/fwlink/?LinkId=525555)定義的術語和縮寫分析和監視中的主題 (hello 如下： 作用中使用者，新的使用者，保留使用者、 工作階段，使用者路徑圖形、 使用者對應，追蹤 Url、 趨勢、 活動、 事件、 作業、 錯誤、 額外的資訊、 損毀，以及應用程式資訊）。</span><span class="sxs-lookup"><span data-stu-id="f8705-108">See hello **Glossary** section in hello [Concepts](http://go.microsoft.com/fwlink/?LinkId=525555) topic for definitions of terms and abbreviations in Analytics and Monitoring (such as hello following: Active User, New user, Retained User, Session, User Path Graph, Users Map, Tracking URLs, Trends, Activity, Event, Job, Error, Extra Info, Crash, and App-info).</span></span>

> [!NOTE]
> <span data-ttu-id="f8705-109">多區段的 hello **Mobile Engagement**入口網站 UI 包含 hello**顯示說明** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="f8705-109">Many sections of hello **Mobile Engagement** portal UI contain hello **SHOW HELP** button.</span></span> <span data-ttu-id="f8705-110">按此按鈕 tooget 區段內容詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="f8705-110">Press this button tooget more contextual information about a section.</span></span>
> 
> 

## <a name="monitor---sessions-jobs-events-errors-and-crashes"></a><span data-ttu-id="f8705-111">監視 - 工作階段、工作、事件、錯誤和損毀</span><span class="sxs-lookup"><span data-stu-id="f8705-111">Monitor - Sessions, Jobs, Events, Errors, and Crashes</span></span>
<span data-ttu-id="f8705-112">您可以看到工作階段中和特定螢幕上目前有多少位使用者，或是目前有多少位使用者執行特定動作。</span><span class="sxs-lookup"><span data-stu-id="f8705-112">You can see how many users are currently in session and on specific screens or doing specific actions.</span></span> <span data-ttu-id="f8705-113">您可以檢視除以「工作階段」、「工作」、「事件」、「錯誤」和「損毀」的使用者活動。</span><span class="sxs-lookup"><span data-stu-id="f8705-113">You can view user activity divided by Sessions, Jobs, Events, Errors, and Crashes.</span></span> <span data-ttu-id="f8705-114">您可以看到 hello 目前的資訊，並顯示 hello 資訊從 hello 過去一小時內，一天或週。</span><span class="sxs-lookup"><span data-stu-id="f8705-114">You can see hello current information and show hello information from hello last hour, day, or week.</span></span> <span data-ttu-id="f8705-115">您可以查看所有的每個類別中的 hello 資訊或排序 hello 特定工作階段、 作業、 事件、 錯誤和損毀。</span><span class="sxs-lookup"><span data-stu-id="f8705-115">You can see all of hello information in each category or sort by hello specific Session, Job, Event, Error, and Crash.</span></span>  <span data-ttu-id="f8705-116">即時監視是很有幫助 toouse 事件，例如推送活動 toosee 期間，如果正在攀升動作右之後傳送推播通知。</span><span class="sxs-lookup"><span data-stu-id="f8705-116">Live monitoring is helpful toouse during events such as a Push campaign toosee if there is an uptick in action right after you send your Push notification.</span></span>

![Monitor1][14]  

## <a name="troubleshooting-with-monitor---events---details"></a><span data-ttu-id="f8705-118">監視 - 事件 - 詳細資料疑難排解</span><span class="sxs-lookup"><span data-stu-id="f8705-118">Troubleshooting with Monitor - Events - Details</span></span>
<span data-ttu-id="f8705-119">從您的測試裝置的應用程式中產生事件及搜尋時間監視的事件的詳細資料中是其中一個 hello 您的裝置識別碼測試裝置與 tooconfirm 該 Azure Mobile Engagement 的整合分析、 監控，最簡單方式 toofind 和從您的應用程式正在區段。</span><span class="sxs-lookup"><span data-stu-id="f8705-119">Generating an event in your application from your test device and finding it in Monitor - Events - Details is one of hello easiest ways toofind your Device ID for your test device and tooconfirm that Azure Mobile Engagement integration of Analytics, Monitoring, and Segments is working from your application.</span></span> <span data-ttu-id="f8705-120">一旦您擁有 hello 測試裝置的裝置識別碼，您可以將它在"My 帳戶-Devices"tooyour 測試裝置。</span><span class="sxs-lookup"><span data-stu-id="f8705-120">Once you have hello Device ID of your test device, you can add it tooyour test devices in “My Account - Devices”.</span></span> <span data-ttu-id="f8705-121">如果您無法產生事件，請確定 Azure Mobile Engagement 已正確整合 Android/iOS/Web/Windows/Windows Phone 應用程式與 hello SDK 中。</span><span class="sxs-lookup"><span data-stu-id="f8705-121">If you can't generate an event, make sure that Azure Mobile Engagement is correctly integrated in your Android/iOS/Web/Windows/Windows Phone app with hello SDK.</span></span>

<span data-ttu-id="f8705-122">如需詳細資訊，請參閱 [SDK 文件][Link 5]</span><span class="sxs-lookup"><span data-stu-id="f8705-122">For more information, see:  [SDK Documentation][Link 5]</span></span>

![Monitor2][15]  

## <a name="troubleshooting-with-monitor---crashes---details"></a><span data-ttu-id="f8705-124">監視 - 損毀 - 詳細資料疑難排解</span><span class="sxs-lookup"><span data-stu-id="f8705-124">Troubleshooting with Monitor - Crashes - Details</span></span>
<span data-ttu-id="f8705-125">您可以檢閱損毀資訊有關應用程式從 toohelp 判斷為何損毀您的應用程式監視的當機的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="f8705-125">You can review crash information about your app from Monitor - Crashes - Details toohelp determine why your app is crashing.</span></span> <span data-ttu-id="f8705-126">您也應該查閱 hello SDK hello hello SDK for Android/iOS/Web/Windows/Windows Phone 的每個版本的版本資訊中的每個版本的已知問題。</span><span class="sxs-lookup"><span data-stu-id="f8705-126">You should also look up known issues with each version of hello SDK in hello release notes for each version of hello SDK for Android/iOS/Web/Windows/Windows Phone.</span></span>

<span data-ttu-id="f8705-127">如需詳細資訊，請參閱 [SDK 文件 - 版本資訊][Link 5]</span><span class="sxs-lookup"><span data-stu-id="f8705-127">For more information, see:  [SDK Documentation - Release notes][Link 5]</span></span>

![Monitor3][16]

## <a name="monitor---alerts"></a><span data-ttu-id="f8705-129">監視 - 警示</span><span class="sxs-lookup"><span data-stu-id="f8705-129">Monitor - Alerts</span></span>
<span data-ttu-id="f8705-130">您也可以指定要自動傳送 tooyou 透過電子郵件或立即訊息的警示狀況。</span><span class="sxs-lookup"><span data-stu-id="f8705-130">You can also specify conditions for Alerts that will be automatically sent tooyou via e-mail or instant message.</span></span> <span data-ttu-id="f8705-131">(支援任何 XMPP 相容服務，例如 Google 的 GTalk 或 Apple 的 iChat)。警示是根據一個預先定義的偵測臨界值，而此臨界值大於 (>) 或小於 (<) 每秒、分鐘或小時特定數目的工作階段、工作、事件、錯誤或損毀。</span><span class="sxs-lookup"><span data-stu-id="f8705-131">(Any XMPP-compliant services like Google's GTalk or Apple's iChat are supported.) Alerts are based on a pre-defined detection threshold greater than (>) or less than (<) a specific number of Sessions, Jobs, Events, Errors, or Crashes per second, minute, or hour.</span></span> <span data-ttu-id="f8705-132">警示可以監視某指定類型的所有活動，或只監視特定工作、事件或錯誤活動。</span><span class="sxs-lookup"><span data-stu-id="f8705-132">Alerts can monitor all activities of a given type, or just monitor a specific Job, Event, or Error activity.</span></span> 

<span data-ttu-id="f8705-133">您也可以指定偵測速率下限，這是 hello 最小數量會分隔兩個通知的相同警示 toomake 確定，您的警示觸發時，您將不會收到的 hello 研究 1 的通知，每個指定的間隔分鐘數。</span><span class="sxs-lookup"><span data-stu-id="f8705-133">You can also specify a Minimum Detection Rate, which is hello minimum amount of minutes that will separate two notifications for hello same alert toomake sure that when your alert is triggered, you will never receive more than 1 notification per interval specified.</span></span>

![Monitor4][17]

## <a name="see-also"></a><span data-ttu-id="f8705-135">另請參閱</span><span class="sxs-lookup"><span data-stu-id="f8705-135">See also</span></span>
* <span data-ttu-id="f8705-136">[概念][Link 6]</span><span class="sxs-lookup"><span data-stu-id="f8705-136">[Concepts][Link 6]</span></span>
* <span data-ttu-id="f8705-137">[疑難排解指南服務][Link 24]</span><span class="sxs-lookup"><span data-stu-id="f8705-137">[Troubleshooting Guide Service][Link 24]</span></span>

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
