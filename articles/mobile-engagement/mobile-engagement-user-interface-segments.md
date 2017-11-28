---
title: "Azure Mobile Engagement 使用者介面 - 使用者分佈"
description: "了解如何使用 Azure Mobile Engagement 建立和管理使用者的使用者分佈以分辨使用模式"
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
ms.openlocfilehash: 087f4a1fef420abe9669f8dfe2b84c7a847ce263
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-create-and-manage-segments-of-users-to-identify-usage-patterns"></a><span data-ttu-id="fa43d-103">如何建立和管理使用者的使用者分佈以分辨使用模式</span><span class="sxs-lookup"><span data-stu-id="fa43d-103">How to create and manage segments of users to identify usage patterns</span></span>
<span data-ttu-id="fa43d-104">本文說明 **Mobile Engagement** 入口網站的 [區段]索引標籤。</span><span class="sxs-lookup"><span data-stu-id="fa43d-104">This article describes the **SEGMENTS** tab of the **Mobile Engagement** portal.</span></span> <span data-ttu-id="fa43d-105">使用 **Mobile Engagement** 入口網站可監視與管理您的行動應用程式。</span><span class="sxs-lookup"><span data-stu-id="fa43d-105">You use the **Mobile Engagement** portal to monitor and manage your mobile apps.</span></span>

<span data-ttu-id="fa43d-106">UI 的 [使用者分佈] 區段可讓您根據不同的行為和分析，對您的使用者進行分佈研究，這些行為和分析可從應用程式取得，也可透過「使用者分佈 API」存取。</span><span class="sxs-lookup"><span data-stu-id="fa43d-106">The Segments section of the UI allows you to work on segmenting your users based on the different behavior and analytics that you can get from the application and can also access through the Segments API.</span></span> <span data-ttu-id="fa43d-107">使用者分佈會在建立之後的 24 小時先計算一次，然後根據最新的分析資訊，每隔 24 小時重新計算一次。</span><span class="sxs-lookup"><span data-stu-id="fa43d-107">Segments are first computed 24 hours after they are created, and they are recomputed every 24 hours based on the latest analytics information.</span></span> <span data-ttu-id="fa43d-108">計算使用者分佈之後，它會每天顯示「每天變化的歷程記錄」圖表。</span><span class="sxs-lookup"><span data-stu-id="fa43d-108">Once a segment is calculated, it displays a "Day to day history" chart each day.</span></span>

> [!NOTE]
> <span data-ttu-id="fa43d-109">許多 **Mobile Engagement** 入口網站 UI 的區段含有 [顯示說明] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="fa43d-109">Many sections of the **Mobile Engagement** portal UI contain the **SHOW HELP** button.</span></span> <span data-ttu-id="fa43d-110">按該按鈕，可獲得關於區段的詳細內容資訊。</span><span class="sxs-lookup"><span data-stu-id="fa43d-110">Press this button to get more contextual information about a section.</span></span>
> 
> 

## <a name="create-segments"></a><span data-ttu-id="fa43d-111">建立使用者分佈</span><span class="sxs-lookup"><span data-stu-id="fa43d-111">Create Segments</span></span>
<span data-ttu-id="fa43d-112">您可以根據 [分析] 區段中過去最多 60 天的特定期間及最多 10 個準則來建立使用者分佈。</span><span class="sxs-lookup"><span data-stu-id="fa43d-112">You can create a segment based on up to 10 criteria on a specific period up to 60 days in the past from the analytics section.</span></span> <span data-ttu-id="fa43d-113">例如，您可以根據過去 10 天內在您的應用程式中檢視某些頁面或搜尋特定內容的人員，建立使用者分佈。</span><span class="sxs-lookup"><span data-stu-id="fa43d-113">For example, you can create a segment based on the people who have viewed certain pages or searched for specific content within your app within the last 10 days.</span></span> <span data-ttu-id="fa43d-114">您也可以在 [分析] 區段取得此資訊。</span><span class="sxs-lookup"><span data-stu-id="fa43d-114">This information is available in the analytics section.</span></span> <span data-ttu-id="fa43d-115">因此，您可以使用這項資訊來建立使用者分佈，然後再針對這一類使用者設定推送通知，讓他們再回到應用程式。</span><span class="sxs-lookup"><span data-stu-id="fa43d-115">So, you can use it to create a segment, and then set up a push notification to target this subset of users to get them to come back to the application.</span></span> 

> [!NOTE]
> <span data-ttu-id="fa43d-116">使用者分佈一旦計算之後，就無法進行編輯；它只能複製或終結 (刪除)。</span><span class="sxs-lookup"><span data-stu-id="fa43d-116">Once a segment has been calculated, it cannot be edited; it can only be cloned (copied) or destroyed (deleted).</span></span> <span data-ttu-id="fa43d-117">使用者分佈可以在同一個應用程式 (具有相同的 AppID) 內複製，也可以複製到其他應用程式 (具有不同的 AppID)。</span><span class="sxs-lookup"><span data-stu-id="fa43d-117">A segment can be cloned within the same application (with the same AppID), and it can also be cloned into other applications (with a different AppID).</span></span> 

 ![segments1][35] 

## <a name="examples-segments"></a><span data-ttu-id="fa43d-119">範例使用者分佈</span><span class="sxs-lookup"><span data-stu-id="fa43d-119">Examples Segments</span></span>
 ![segments2][36]

<span data-ttu-id="fa43d-121">使用者分佈可讓您對應用程式的使用者進行分佈研究。</span><span class="sxs-lookup"><span data-stu-id="fa43d-121">Segments allow you to segment the end-users of your application.</span></span>
<span data-ttu-id="fa43d-122">研究您的使用者分佈是很重要的行銷策略。</span><span class="sxs-lookup"><span data-stu-id="fa43d-122">Segmenting your users is an important marketing strategy.</span></span> <span data-ttu-id="fa43d-123">Azure Mobile Engagement 可讓您取得歷史資料，並建立自訂的使用者分佈。</span><span class="sxs-lookup"><span data-stu-id="fa43d-123">Azure Mobile Engagement allows you to get historic data and create custom segments.</span></span> <span data-ttu-id="fa43d-124">這個功能強大的工具可讓您深入了解客戶的應用程式體驗。</span><span class="sxs-lookup"><span data-stu-id="fa43d-124">This powerful tool enables you to learn about your customers’ experience in your application.</span></span> <span data-ttu-id="fa43d-125">您可以輕鬆地分析您的使用者分佈，並利用這些使用者分佈做為推送目標。</span><span class="sxs-lookup"><span data-stu-id="fa43d-125">You can easily analyze your segments and use your segments as push targets.</span></span>
<span data-ttu-id="fa43d-126">常見的使用案例是傳送推送通知，鼓勵使用者在市集中對應用程式評分。</span><span class="sxs-lookup"><span data-stu-id="fa43d-126">A common use-case is that you want to send a push a notification to encourage your end-users to rate your application in the store.</span></span> <span data-ttu-id="fa43d-127">您可以建立一個使用者分佈，指定過去一個月每天使用您的應用程式且有絕佳使用者體驗的使用者，針對這些使用者而不是所有使用者傳送通知。</span><span class="sxs-lookup"><span data-stu-id="fa43d-127">Rather than sending a notification to all your end-users, you can create a segment that would specify only users that have used your application every day for the last month and have had a great user experience.</span></span> <span data-ttu-id="fa43d-128">若您傳送比較少、目標更明確的推送通知，您就會獲得更好的 ROI。</span><span class="sxs-lookup"><span data-stu-id="fa43d-128">When you send fewer, highly targeted push notifications, you get a better ROI.</span></span>

 ![segments3][37]

### <a name="segments-you-can-create-based-on-the-major-azure-mobile-engagement-elements"></a><span data-ttu-id="fa43d-130">您可以根據主要 Azure Mobile Engagement 項目建立的使用者分佈：</span><span class="sxs-lookup"><span data-stu-id="fa43d-130">Segments you can create based on the major Azure Mobile Engagement elements:</span></span>
* <span data-ttu-id="fa43d-131">事件：建立一週內發生兩次以上某個應用程式特定事件的使用者分佈。</span><span class="sxs-lookup"><span data-stu-id="fa43d-131">Event: create a segment that targets one specific event of the application that happened more than twice a week.</span></span> 
* <span data-ttu-id="fa43d-132">工作階段：建立上週使用 5 次以上應用程式的使用者分佈。</span><span class="sxs-lookup"><span data-stu-id="fa43d-132">Session: create a segment of users that have used the application more than 5 times last week.</span></span>
* <span data-ttu-id="fa43d-133">活動：建立上個月使用多於或少於 10 次某一頁面或內容的使用者分佈。</span><span class="sxs-lookup"><span data-stu-id="fa43d-133">Activity: create a segment of users that have used one page or content more or less than 10 time last month.</span></span>
* <span data-ttu-id="fa43d-134">工作：建立一天完成兩次以上工作的使用者分佈。</span><span class="sxs-lookup"><span data-stu-id="fa43d-134">Job: create a segment of users that have completed a job more than twice a day.</span></span>
* <span data-ttu-id="fa43d-135">當機：建立上週當機 10 次以上的所有使用者分佈。</span><span class="sxs-lookup"><span data-stu-id="fa43d-135">Crash: create a segment of all the users that have had a crash more than 10 times last week.</span></span> <span data-ttu-id="fa43d-136">(您可以在推送此使用者分佈時包含道歉啟事或優待券！)</span><span class="sxs-lookup"><span data-stu-id="fa43d-136">(You could push this segment with an apology or even a coupon!)</span></span>
* <span data-ttu-id="fa43d-137">錯誤：建立過去 3 天發生 100 次以上錯誤的所有使用者分佈。</span><span class="sxs-lookup"><span data-stu-id="fa43d-137">Error: create a segment of all the users that have had an error more than 100 times last 3 days.</span></span>
* <span data-ttu-id="fa43d-138">應用程式資訊：建立過去 25 天內發生自訂「應用程式資訊」的使用者分佈。</span><span class="sxs-lookup"><span data-stu-id="fa43d-138">App Info: create a segment that targets a custom App Info that happened during the last 25 days.</span></span>
  
  ![segments4][38]

<span data-ttu-id="fa43d-140">若要以最佳方式利用使用者分佈，您必須先在具有「應用程式資訊」標記之標記計畫的應用程式中完成 SDK 的自訂整合。</span><span class="sxs-lookup"><span data-stu-id="fa43d-140">To use Segment in an optimal way, you must have done a customized integration of the SDK in your application with a tagging plan of "App Info" tags.</span></span>
<span data-ttu-id="fa43d-141">然後，移至介面的首頁上，選取您想要的應用程式，然後按一下 [使用者分佈] 區段。</span><span class="sxs-lookup"><span data-stu-id="fa43d-141">Then, go to the home page of the interface, select the application you want and click on the "Segments" section.</span></span>

1. <span data-ttu-id="fa43d-142">選取 [使用者分佈] 區段。</span><span class="sxs-lookup"><span data-stu-id="fa43d-142">Select the "Segments" section.</span></span>
2. <span data-ttu-id="fa43d-143">按一下 [新增使用者分佈] 按鈕，建立新的使用者分佈。</span><span class="sxs-lookup"><span data-stu-id="fa43d-143">Click on the "New segment" button to create a new segment.</span></span>

## <a name="real-life-example-create-a-simple-segment-based-on-session-information"></a><span data-ttu-id="fa43d-144">實際範例：根據「工作階段」資訊建立簡單的使用者分佈</span><span class="sxs-lookup"><span data-stu-id="fa43d-144">Real Life Example: Create a simple segment based on "Session" information</span></span>
<span data-ttu-id="fa43d-145">建立上週至少使用 50 次您的應用程式的所有使用者分佈。</span><span class="sxs-lookup"><span data-stu-id="fa43d-145">Create a segment of all the end-users that have used your app at least 50 times in the last week.</span></span> <span data-ttu-id="fa43d-146">從該處只尋找在應用程式中每個工作階段至少花費 30 秒的使用者。</span><span class="sxs-lookup"><span data-stu-id="fa43d-146">From there, find only the end-users that have spent at least 30 seconds in your app per session.</span></span> <span data-ttu-id="fa43d-147">這會顯示在您的應用程式中獲得正面體驗的所有使用者。</span><span class="sxs-lookup"><span data-stu-id="fa43d-147">This will show all the end-users who have a positive experience in your app.</span></span> <span data-ttu-id="fa43d-148">然後，建立的使用者分佈可用來推送通知給這些使用者，請他們在市集中對您的應用程式評分。</span><span class="sxs-lookup"><span data-stu-id="fa43d-148">Then, the segment created could be used to push a notification to these end-users to ask them to rate your app in the store.</span></span>

 ![segments5][39]

1. <span data-ttu-id="fa43d-150">您可以將使用者分佈命名，方便在 [使用者分佈] 清單中快速尋找。</span><span class="sxs-lookup"><span data-stu-id="fa43d-150">Give your segment a name in order to find it quickly in the "Segment" list.</span></span>
2. <span data-ttu-id="fa43d-151">按一下 [建立] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="fa43d-151">Click on the "Create" button.</span></span>
   
   ![segments6][40]

<span data-ttu-id="fa43d-153">選取 [工作階段]。</span><span class="sxs-lookup"><span data-stu-id="fa43d-153">Select Session.</span></span>

 ![segments7][41]

1. <span data-ttu-id="fa43d-155">選取 [上週] 的期間。</span><span class="sxs-lookup"><span data-stu-id="fa43d-155">Select the period of "Last week".</span></span>
2. <span data-ttu-id="fa43d-156">按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="fa43d-156">Click next.</span></span>
   
   ![segments8][42]
3. <span data-ttu-id="fa43d-158">在清單中選取相關的 [運算子]：=、≥、≤。</span><span class="sxs-lookup"><span data-stu-id="fa43d-158">Select the Operator that is relevant among the list: =; ≥, ≤.</span></span>
4. <span data-ttu-id="fa43d-159">輸入您想要的 [計數]。</span><span class="sxs-lookup"><span data-stu-id="fa43d-159">Enter the Count you want.</span></span>
5. <span data-ttu-id="fa43d-160">選取您想要的 [發生次數]。</span><span class="sxs-lookup"><span data-stu-id="fa43d-160">Select the Occurrence you want.</span></span> 
6. <span data-ttu-id="fa43d-161">按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="fa43d-161">Click next.</span></span>
   <span data-ttu-id="fa43d-162">此範例就設定為上週至少使用了 50 個工作階段的使用者。</span><span class="sxs-lookup"><span data-stu-id="fa43d-162">This example is set so that over the last week, match users that have made at least 50 sessions.</span></span>
   
   ![segments9][43]

<span data-ttu-id="fa43d-164">如果要查看「工作階段」的分佈方式，您可以選擇每個工作階段的長度做為準則。</span><span class="sxs-lookup"><span data-stu-id="fa43d-164">For the Session segmentation, you can choose the length per session as a criteria.</span></span>

1. <span data-ttu-id="fa43d-165">從清單中選取 [運算子]。</span><span class="sxs-lookup"><span data-stu-id="fa43d-165">Select the Operator from the list.</span></span>
2. <span data-ttu-id="fa43d-166">提供每個工作階段的 [長度]。</span><span class="sxs-lookup"><span data-stu-id="fa43d-166">Provide the Length per session.</span></span>
3. <span data-ttu-id="fa43d-167">按一下 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="fa43d-167">Click Next.</span></span>
   <span data-ttu-id="fa43d-168">此範例表示在根據發生區段計算而得的所有工作階段中，只選取在每個工作階段花費超過 30 秒的使用者。</span><span class="sxs-lookup"><span data-stu-id="fa43d-168">In this example, it says that over all the sessions that have been segmented on the occurrence section, select only the users that have spent more than 30 seconds per session.</span></span>
   
   ![segments10][44]

<span data-ttu-id="fa43d-170">將您的準則命名，以便在完整的漏斗圖中可以擷取準則，然後按一下 [完成]。</span><span class="sxs-lookup"><span data-stu-id="fa43d-170">Name your criterion in order to retrieve it in the complete funnel, and click Finish.</span></span>

 ![segments11][45]

<span data-ttu-id="fa43d-172">準則設定完成時，將會出現在使用者分佈漏斗圖中。</span><span class="sxs-lookup"><span data-stu-id="fa43d-172">When you have finished setting up your criterion, it will appear in the segment funnel.</span></span>
<span data-ttu-id="fa43d-173">因為使用者分佈是根據分析資料，所以使用者分佈也會每天計算一次。</span><span class="sxs-lookup"><span data-stu-id="fa43d-173">Because a segment is based on analytics data, segments are computed once per day.</span></span>
<span data-ttu-id="fa43d-174">在此範例中，總共有 47.7% 的使用者符合準則。</span><span class="sxs-lookup"><span data-stu-id="fa43d-174">In this example, 47,7% of the total end-users matched the criterion.</span></span> <span data-ttu-id="fa43d-175">這些是有良好體驗的使用者，所以如果推送通知請他們在市集中對應用程式評分，他們應該會提供比較高的評分。</span><span class="sxs-lookup"><span data-stu-id="fa43d-175">They should be the users who have had a good experience and will be likely to provide a higher rating if you push them a notification asking them to rate the app in the store.</span></span>

## <a name="see-also"></a><span data-ttu-id="fa43d-176">另請參閱</span><span class="sxs-lookup"><span data-stu-id="fa43d-176">See also</span></span>
* <span data-ttu-id="fa43d-177">[概念][Link 6]</span><span class="sxs-lookup"><span data-stu-id="fa43d-177">[Concepts][Link 6]</span></span>
* <span data-ttu-id="fa43d-178">[疑難排解指南服務][Link 24]</span><span class="sxs-lookup"><span data-stu-id="fa43d-178">[Troubleshooting Guide Service][Link 24]</span></span>

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

