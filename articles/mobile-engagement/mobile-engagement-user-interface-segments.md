---
title: "aaaAzure Mobile Engagement 使用者介面的區段"
description: "深入了解如何 toocreate 和管理使用者 tooidentify 習慣使用 Azure Mobile Engagement 的區段"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: 6a4f2205-4a3c-406e-a04f-5e6f2a36653f
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: bb214c45d05ebfbf243978658a7e331d4a7c6e0e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-and-manage-segments-of-users-tooidentify-usage-patterns"></a><span data-ttu-id="d2031-103">如何 toocreate 和管理使用者 tooidentify 習慣的區段</span><span class="sxs-lookup"><span data-stu-id="d2031-103">How toocreate and manage segments of users tooidentify usage patterns</span></span>
<span data-ttu-id="d2031-104">本文說明 hello**區段** 索引標籤的 hello **Mobile Engagement**入口網站。</span><span class="sxs-lookup"><span data-stu-id="d2031-104">This article describes hello **SEGMENTS** tab of hello **Mobile Engagement** portal.</span></span> <span data-ttu-id="d2031-105">使用 hello **Mobile Engagement** toomonitor 入口網站和管理您的行動裝置應用程式。</span><span class="sxs-lookup"><span data-stu-id="d2031-105">You use hello **Mobile Engagement** portal toomonitor and manage your mobile apps.</span></span>

<span data-ttu-id="d2031-106">hello UI hello 區段區段可讓您 toowork 上切割您根據 hello 不同的行為和分析，您可以從 hello 應用程式取得，而且也可以存取透過 hello 區段 API 的使用者。</span><span class="sxs-lookup"><span data-stu-id="d2031-106">hello Segments section of hello UI allows you toowork on segmenting your users based on hello different behavior and analytics that you can get from hello application and can also access through hello Segments API.</span></span> <span data-ttu-id="d2031-107">區段會先計算 24 小時之後建立的它們會重新計算根據 hello 最新的分析資訊每隔 24 小時。</span><span class="sxs-lookup"><span data-stu-id="d2031-107">Segments are first computed 24 hours after they are created, and they are recomputed every 24 hours based on hello latest analytics information.</span></span> <span data-ttu-id="d2031-108">一旦計算區段，它就會 「 日 tooday 歷程記錄 」 圖表顯示每一天。</span><span class="sxs-lookup"><span data-stu-id="d2031-108">Once a segment is calculated, it displays a "Day tooday history" chart each day.</span></span>

> [!NOTE]
> <span data-ttu-id="d2031-109">多區段的 hello **Mobile Engagement**入口網站 UI 包含 hello**顯示說明** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="d2031-109">Many sections of hello **Mobile Engagement** portal UI contain hello **SHOW HELP** button.</span></span> <span data-ttu-id="d2031-110">按此按鈕 tooget 區段內容詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="d2031-110">Press this button tooget more contextual information about a section.</span></span>
> 
> 

## <a name="create-segments"></a><span data-ttu-id="d2031-111">建立使用者分佈</span><span class="sxs-lookup"><span data-stu-id="d2031-111">Create Segments</span></span>
<span data-ttu-id="d2031-112">您可以建立根據向上 too10 準則向上 hello too60 天的特定時間上的線段過去從 hello 分析區段。</span><span class="sxs-lookup"><span data-stu-id="d2031-112">You can create a segment based on up too10 criteria on a specific period up too60 days in hello past from hello analytics section.</span></span> <span data-ttu-id="d2031-113">例如，您可以建立根據 hello 人具有檢視特定頁面或搜尋最後 10 天內 hello 應用程式內的特定內容的區段。</span><span class="sxs-lookup"><span data-stu-id="d2031-113">For example, you can create a segment based on hello people who have viewed certain pages or searched for specific content within your app within hello last 10 days.</span></span> <span data-ttu-id="d2031-114">這項資訊可在 hello 分析區段。</span><span class="sxs-lookup"><span data-stu-id="d2031-114">This information is available in hello analytics section.</span></span> <span data-ttu-id="d2031-115">因此，您可以 toocreate 在區段中，使用它，然後再將推播通知 tootarget 這個子集使用者 tooget 它們 toocome 後 toohello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="d2031-115">So, you can use it toocreate a segment, and then set up a push notification tootarget this subset of users tooget them toocome back toohello application.</span></span> 

> [!NOTE]
> <span data-ttu-id="d2031-116">使用者分佈一旦計算之後，就無法進行編輯；它只能複製或終結 (刪除)。</span><span class="sxs-lookup"><span data-stu-id="d2031-116">Once a segment has been calculated, it cannot be edited; it can only be cloned (copied) or destroyed (deleted).</span></span> <span data-ttu-id="d2031-117">區段可以被複製 hello 內相同的應用程式 (與 hello 相同 AppID)，並也可以被複製到其他應用程式 （具有不同的 AppID)。</span><span class="sxs-lookup"><span data-stu-id="d2031-117">A segment can be cloned within hello same application (with hello same AppID), and it can also be cloned into other applications (with a different AppID).</span></span> 

 ![segments1][35] 

## <a name="examples-segments"></a><span data-ttu-id="d2031-119">範例使用者分佈</span><span class="sxs-lookup"><span data-stu-id="d2031-119">Examples Segments</span></span>
 ![segments2][36]

<span data-ttu-id="d2031-121">區段可讓您 toosegment hello 使用者的應用程式。</span><span class="sxs-lookup"><span data-stu-id="d2031-121">Segments allow you toosegment hello end-users of your application.</span></span>
<span data-ttu-id="d2031-122">研究您的使用者分佈是很重要的行銷策略。</span><span class="sxs-lookup"><span data-stu-id="d2031-122">Segmenting your users is an important marketing strategy.</span></span> <span data-ttu-id="d2031-123">Azure Mobile Engagement 可讓您 tooget 歷程資料，並建立自訂的區段。</span><span class="sxs-lookup"><span data-stu-id="d2031-123">Azure Mobile Engagement allows you tooget historic data and create custom segments.</span></span> <span data-ttu-id="d2031-124">此功能強大的工具可讓您 toolearn 有關您的客戶體驗您的應用程式中。</span><span class="sxs-lookup"><span data-stu-id="d2031-124">This powerful tool enables you toolearn about your customers’ experience in your application.</span></span> <span data-ttu-id="d2031-125">您可以輕鬆地分析您的使用者分佈，並利用這些使用者分佈做為推送目標。</span><span class="sxs-lookup"><span data-stu-id="d2031-125">You can easily analyze your segments and use your segments as push targets.</span></span>
<span data-ttu-id="d2031-126">常見的使用案例是您想 toosend 推播通知 tooencourage 使用者 toorate hello 存放區中的應用程式。</span><span class="sxs-lookup"><span data-stu-id="d2031-126">A common use-case is that you want toosend a push a notification tooencourage your end-users toorate your application in hello store.</span></span> <span data-ttu-id="d2031-127">而不是傳送通知 tooall 您的使用者，您可以建立的區段時，會指定使用者的已使用您的應用程式每日 hello 上個月，而且有很好的使用者經驗。</span><span class="sxs-lookup"><span data-stu-id="d2031-127">Rather than sending a notification tooall your end-users, you can create a segment that would specify only users that have used your application every day for hello last month and have had a great user experience.</span></span> <span data-ttu-id="d2031-128">若您傳送比較少、目標更明確的推送通知，您就會獲得更好的 ROI。</span><span class="sxs-lookup"><span data-stu-id="d2031-128">When you send fewer, highly targeted push notifications, you get a better ROI.</span></span>

 ![segments3][37]

### <a name="segments-you-can-create-based-on-hello-major-azure-mobile-engagement-elements"></a><span data-ttu-id="d2031-130">您可以建立的區段基礎 hello 主要 Azure Mobile Engagement 項目：</span><span class="sxs-lookup"><span data-stu-id="d2031-130">Segments you can create based on hello major Azure Mobile Engagement elements:</span></span>
* <span data-ttu-id="d2031-131">事件： 建立目標一個 hello 應用程式發生兩倍以上一週的特定事件的區段。</span><span class="sxs-lookup"><span data-stu-id="d2031-131">Event: create a segment that targets one specific event of hello application that happened more than twice a week.</span></span> 
* <span data-ttu-id="d2031-132">工作階段： 建立的使用者使用 hello 應用程式超過 5 次過去一週的區段。</span><span class="sxs-lookup"><span data-stu-id="d2031-132">Session: create a segment of users that have used hello application more than 5 times last week.</span></span>
* <span data-ttu-id="d2031-133">活動：建立上個月使用多於或少於 10 次某一頁面或內容的使用者分佈。</span><span class="sxs-lookup"><span data-stu-id="d2031-133">Activity: create a segment of users that have used one page or content more or less than 10 time last month.</span></span>
* <span data-ttu-id="d2031-134">工作：建立一天完成兩次以上工作的使用者分佈。</span><span class="sxs-lookup"><span data-stu-id="d2031-134">Job: create a segment of users that have completed a job more than twice a day.</span></span>
* <span data-ttu-id="d2031-135">損毀： 建立所有 hello 使用者已經損毀 10 次以上過去一週的區段。</span><span class="sxs-lookup"><span data-stu-id="d2031-135">Crash: create a segment of all hello users that have had a crash more than 10 times last week.</span></span> <span data-ttu-id="d2031-136">(您可以在推送此使用者分佈時包含道歉啟事或優待券！)</span><span class="sxs-lookup"><span data-stu-id="d2031-136">(You could push this segment with an apology or even a coupon!)</span></span>
* <span data-ttu-id="d2031-137">錯誤： 建立的所有 hello 使用者有多個 100 次過去 3 天內發生了錯誤的區段。</span><span class="sxs-lookup"><span data-stu-id="d2031-137">Error: create a segment of all hello users that have had an error more than 100 times last 3 days.</span></span>
* <span data-ttu-id="d2031-138">應用程式資訊： 建立目標時發生 hello 25 天自訂應用程式資訊區段。</span><span class="sxs-lookup"><span data-stu-id="d2031-138">App Info: create a segment that targets a custom App Info that happened during hello last 25 days.</span></span>
  
  ![segments4][38]

<span data-ttu-id="d2031-140">toouse 區段，以最佳方式，您必須完成 hello SDK 整合在自訂的應用程式的 [應用程式資訊] 標記的標記計劃中。</span><span class="sxs-lookup"><span data-stu-id="d2031-140">toouse Segment in an optimal way, you must have done a customized integration of hello SDK in your application with a tagging plan of "App Info" tags.</span></span>
<span data-ttu-id="d2031-141">接著，移 hello 介面 toohello 首頁中，選取 hello 應用程式，然後按一下 hello 「 區段 」 一節。</span><span class="sxs-lookup"><span data-stu-id="d2031-141">Then, go toohello home page of hello interface, select hello application you want and click on hello "Segments" section.</span></span>

1. <span data-ttu-id="d2031-142">選取 hello 「 區段 」 一節。</span><span class="sxs-lookup"><span data-stu-id="d2031-142">Select hello "Segments" section.</span></span>
2. <span data-ttu-id="d2031-143">按一下 「 新的區段 」 hello 按鈕 toocreate 新的區段。</span><span class="sxs-lookup"><span data-stu-id="d2031-143">Click on hello "New segment" button toocreate a new segment.</span></span>

## <a name="real-life-example-create-a-simple-segment-based-on-session-information"></a><span data-ttu-id="d2031-144">實際範例：根據「工作階段」資訊建立簡單的使用者分佈</span><span class="sxs-lookup"><span data-stu-id="d2031-144">Real Life Example: Create a simple segment based on "Session" information</span></span>
<span data-ttu-id="d2031-145">建立所有 hello 使用者使用您的應用程式至少 50 次 hello 過去一週中的區段。</span><span class="sxs-lookup"><span data-stu-id="d2031-145">Create a segment of all hello end-users that have used your app at least 50 times in hello last week.</span></span> <span data-ttu-id="d2031-146">從該處，尋找只 hello 花了至少 30 秒，每個工作階段的應用程式中的使用者。</span><span class="sxs-lookup"><span data-stu-id="d2031-146">From there, find only hello end-users that have spent at least 30 seconds in your app per session.</span></span> <span data-ttu-id="d2031-147">這會顯示所有 hello 的使用者在您的應用程式中有正面的體驗。</span><span class="sxs-lookup"><span data-stu-id="d2031-147">This will show all hello end-users who have a positive experience in your app.</span></span> <span data-ttu-id="d2031-148">接下來，建立 hello 區段可能會使用的 toopush 通知 toothese 使用者 tooask 它們 toorate hello 中的應用程式存放區。</span><span class="sxs-lookup"><span data-stu-id="d2031-148">Then, hello segment created could be used toopush a notification toothese end-users tooask them toorate your app in hello store.</span></span>

 ![segments5][39]

1. <span data-ttu-id="d2031-150">名稱命名您的區段，在訂單 toofind 快速在 hello 「 區段 」 清單。</span><span class="sxs-lookup"><span data-stu-id="d2031-150">Give your segment a name in order toofind it quickly in hello "Segment" list.</span></span>
2. <span data-ttu-id="d2031-151">Hello 上按一下 [建立] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="d2031-151">Click on hello "Create" button.</span></span>
   
   ![segments6][40]

<span data-ttu-id="d2031-153">選取 [工作階段]。</span><span class="sxs-lookup"><span data-stu-id="d2031-153">Select Session.</span></span>

 ![segments7][41]

1. <span data-ttu-id="d2031-155">選取 最近一週"hello 期間。</span><span class="sxs-lookup"><span data-stu-id="d2031-155">Select hello period of "Last week".</span></span>
2. <span data-ttu-id="d2031-156">按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="d2031-156">Click next.</span></span>
   
   ![segments8][42]
3. <span data-ttu-id="d2031-158">選取 hello 與 hello 清單之間的運算子: =;≥ ≤。</span><span class="sxs-lookup"><span data-stu-id="d2031-158">Select hello Operator that is relevant among hello list: =; ≥, ≤.</span></span>
4. <span data-ttu-id="d2031-159">輸入 hello 您想要的計數。</span><span class="sxs-lookup"><span data-stu-id="d2031-159">Enter hello Count you want.</span></span>
5. <span data-ttu-id="d2031-160">選取 hello 出現您想要的項目。</span><span class="sxs-lookup"><span data-stu-id="d2031-160">Select hello Occurrence you want.</span></span> 
6. <span data-ttu-id="d2031-161">按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="d2031-161">Click next.</span></span>
   <span data-ttu-id="d2031-162">這個範例會設定讓該 over hello 過去一週，已在至少 50 的工作階段的比對使用者。</span><span class="sxs-lookup"><span data-stu-id="d2031-162">This example is set so that over hello last week, match users that have made at least 50 sessions.</span></span>
   
   ![segments9][43]

<span data-ttu-id="d2031-164">Hello 分割工作階段，您可以選擇每個工作階段做為條件 hello 長度。</span><span class="sxs-lookup"><span data-stu-id="d2031-164">For hello Session segmentation, you can choose hello length per session as a criteria.</span></span>

1. <span data-ttu-id="d2031-165">Hello 清單中選取 hello 運算子。</span><span class="sxs-lookup"><span data-stu-id="d2031-165">Select hello Operator from hello list.</span></span>
2. <span data-ttu-id="d2031-166">提供每個工作階段的 hello 長度。</span><span class="sxs-lookup"><span data-stu-id="d2031-166">Provide hello Length per session.</span></span>
3. <span data-ttu-id="d2031-167">按一下 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="d2031-167">Click Next.</span></span>
   <span data-ttu-id="d2031-168">在此範例中，該處會指示，透過所有 hello 有已 hello 出現項目區段中，區隔的工作階段選取只有 hello 所花 30 秒以上每個工作階段的使用者。</span><span class="sxs-lookup"><span data-stu-id="d2031-168">In this example, it says that over all hello sessions that have been segmented on hello occurrence section, select only hello users that have spent more than 30 seconds per session.</span></span>
   
   ![segments10][44]

<span data-ttu-id="d2031-170">名稱在 hello 完成順序 tooretrieve 準則漏斗，並按一下 [完成]。</span><span class="sxs-lookup"><span data-stu-id="d2031-170">Name your criterion in order tooretrieve it in hello complete funnel, and click Finish.</span></span>

 ![segments11][45]

<span data-ttu-id="d2031-172">當您的準則設定完成時，它會出現在 hello 區段漏斗圖。</span><span class="sxs-lookup"><span data-stu-id="d2031-172">When you have finished setting up your criterion, it will appear in hello segment funnel.</span></span>
<span data-ttu-id="d2031-173">因為使用者分佈是根據分析資料，所以使用者分佈也會每天計算一次。</span><span class="sxs-lookup"><span data-stu-id="d2031-173">Because a segment is based on analytics data, segments are computed once per day.</span></span>
<span data-ttu-id="d2031-174">在此範例中，47,7 %hello 總使用者的比對 hello 準則。</span><span class="sxs-lookup"><span data-stu-id="d2031-174">In this example, 47,7% of hello total end-users matched hello criterion.</span></span> <span data-ttu-id="d2031-175">它們應該 hello 使用者有良好的體驗，並將會更高評等如果推送通知可能 tooprovide 詢問他們 toorate hello 存放區中的 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="d2031-175">They should be hello users who have had a good experience and will be likely tooprovide a higher rating if you push them a notification asking them toorate hello app in hello store.</span></span>

## <a name="see-also"></a><span data-ttu-id="d2031-176">另請參閱</span><span class="sxs-lookup"><span data-stu-id="d2031-176">See also</span></span>
* <span data-ttu-id="d2031-177">[概念][Link 6]</span><span class="sxs-lookup"><span data-stu-id="d2031-177">[Concepts][Link 6]</span></span>
* <span data-ttu-id="d2031-178">[疑難排解指南服務][Link 24]</span><span class="sxs-lookup"><span data-stu-id="d2031-178">[Troubleshooting Guide Service][Link 24]</span></span>

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

