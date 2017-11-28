---
title: "對媒體應用程式實作 Azure Mobile Engagement"
description: "對媒體應用程式實作 Azure Mobile Engagement 的案例"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 48201cc8-4e04-485c-a8dc-d6406d23f3ed
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: c1591c3e436981e621830916cf0cdc4b7f395d7b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="implement-mobile-engagement-with-media-app"></a><span data-ttu-id="7765d-103">對媒體應用程式實作 Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="7765d-103">Implement Mobile Engagement with Media App</span></span>
## <a name="overview"></a><span data-ttu-id="7765d-104">Overview</span><span class="sxs-lookup"><span data-stu-id="7765d-104">Overview</span></span>
<span data-ttu-id="7765d-105">John 是一家大型媒體公司的行動裝置專案經理。</span><span class="sxs-lookup"><span data-stu-id="7765d-105">John is a mobile project manager for a big media company.</span></span> <span data-ttu-id="7765d-106">他最近推出了一款新的應用程式，並獲得很高的下載次數。</span><span class="sxs-lookup"><span data-stu-id="7765d-106">He recently launched a new app that has a very high download count.</span></span> <span data-ttu-id="7765d-107">他已達成預定的下載次數目標，但從每位使用者身上所獲得的投資回報 (ROI) 卻未達要求。</span><span class="sxs-lookup"><span data-stu-id="7765d-107">He has hit his goals for download but, still his Return On Investment(ROI) per user does not meet his requirements.</span></span> 

<span data-ttu-id="7765d-108">John 已找到 ROI 太低的原因。</span><span class="sxs-lookup"><span data-stu-id="7765d-108">John has already identified why his ROI is too low.</span></span> <span data-ttu-id="7765d-109">使用者經常在短短 2 週後就停止使用他的應用程式，而且大多不會再回頭使用。</span><span class="sxs-lookup"><span data-stu-id="7765d-109">Users frequently stop using his app after only 2 weeks and most of them never come back.</span></span> <span data-ttu-id="7765d-110">他想要提升應用程式的保留期。</span><span class="sxs-lookup"><span data-stu-id="7765d-110">He wants to increase the retention of his app.</span></span>

<span data-ttu-id="7765d-111">他在做過初步測試後發現，當他利用推播通知吸引使用者注意時，他們往往會繼續使用這款應用程式。</span><span class="sxs-lookup"><span data-stu-id="7765d-111">After some initial testing, he has learned when he engages his users with push notifications, they tend to continue using his app.</span></span> <span data-ttu-id="7765d-112">而且原本已經沒在使用應用程式的使用者，經常也會因為某些傳送給他們的通知，而回頭繼續使用。</span><span class="sxs-lookup"><span data-stu-id="7765d-112">Also users that were inactive will often return to the app depending on notifications he sends them.</span></span> <span data-ttu-id="7765d-113">John 決定為他的應用程式投資某種形式的業務開發計劃，以便透過推播通知來使用進階的目標鎖定功能。</span><span class="sxs-lookup"><span data-stu-id="7765d-113">John decides to invest in some kind of Engagement Program for his app which uses advanced targeting with push notifications.</span></span>

<span data-ttu-id="7765d-114">John 最近看了 [Azure Mobile Engagement - 入門指南與最佳作法](mobile-engagement-getting-started-best-practices.md) 一文，因此決定實作指南中所提出的建議。</span><span class="sxs-lookup"><span data-stu-id="7765d-114">John has recently read the [Azure Mobile Engagement - Getting Started Guide with Best practices](mobile-engagement-getting-started-best-practices.md) and has decided to implement the recommendations from the guide.</span></span>

## <a name="objectives-and-kpis"></a><span data-ttu-id="7765d-115">目標和 KPI</span><span class="sxs-lookup"><span data-stu-id="7765d-115">Objectives and KPIs</span></span>
<span data-ttu-id="7765d-116">John 所推出的應用程式的重要關係人聚在一起。</span><span class="sxs-lookup"><span data-stu-id="7765d-116">Key stakeholders for John's app meet.</span></span> <span data-ttu-id="7765d-117">當使用者使用他的媒體時，其中的廣告便會為他們帶來生意。</span><span class="sxs-lookup"><span data-stu-id="7765d-117">Business is generated from ads as users consume his media.</span></span> <span data-ttu-id="7765d-118">所以只要增加每位使用者使用的內容，John 就能增加營收。</span><span class="sxs-lookup"><span data-stu-id="7765d-118">By increasing content consumed per user, John increases his revenues.</span></span> <span data-ttu-id="7765d-119">所有人都同意一個主要目標，那就是將廣告所帶來的銷售量增加 25%。</span><span class="sxs-lookup"><span data-stu-id="7765d-119">All agree on one main objective: To increase sales from ads by 25%.</span></span> <span data-ttu-id="7765d-120">他們建立起業務關鍵效能指標 (KPI)，以便測量和推動這個目標。</span><span class="sxs-lookup"><span data-stu-id="7765d-120">They create Business Key Performance Indicators (KPIs) to measure and drive this objective</span></span>

* <span data-ttu-id="7765d-121">每位使用者點按的廣告數目</span><span class="sxs-lookup"><span data-stu-id="7765d-121">Number of ads clicked per user</span></span>
* <span data-ttu-id="7765d-122">(每位使用者/每個工作階段/每週/每月...) 瀏覽過多少文章頁面</span><span class="sxs-lookup"><span data-stu-id="7765d-122">How many article pages visited (per user/ per session/ per week / per month…)</span></span>
* <span data-ttu-id="7765d-123">最愛的類別有哪些</span><span class="sxs-lookup"><span data-stu-id="7765d-123">What are favorite categories</span></span>

<span data-ttu-id="7765d-124">John 根據他與重要關係人的會面結果，定義了他的業務 KPI。</span><span class="sxs-lookup"><span data-stu-id="7765d-124">Based on John's meeting with key stakeholders he has defined his Business KPIs.</span></span> <span data-ttu-id="7765d-125">他按照 [Azure Mobile Engagement - 入門指南與最佳作法](mobile-engagement-getting-started-best-practices.md)的第一部分進行。</span><span class="sxs-lookup"><span data-stu-id="7765d-125">He follows Part 1 of the [Azure Mobile Engagement - Getting Started Guide with Best practices](mobile-engagement-getting-started-best-practices.md).</span></span> 

<span data-ttu-id="7765d-126">接下來，他建立下列 Engagement KPI 來確定有達成目標：</span><span class="sxs-lookup"><span data-stu-id="7765d-126">Next, he creates the following Engagement KPIs to ensure that objectives are reached:</span></span>

* <span data-ttu-id="7765d-127">監視下列時間間隔的保留期：每日、每週、每兩週和每月。</span><span class="sxs-lookup"><span data-stu-id="7765d-127">Monitor retention across the following intervals: daily, weekly, bi-weekly and monthly.</span></span>
* <span data-ttu-id="7765d-128">活躍使用者人數</span><span class="sxs-lookup"><span data-stu-id="7765d-128">Active users counts</span></span>
* <span data-ttu-id="7765d-129">應用程式在應用程式市集內的評分</span><span class="sxs-lookup"><span data-stu-id="7765d-129">The app rating in the app stores</span></span>

<span data-ttu-id="7765d-130">根據 IT 團隊所提的建議，他新增了下列技術 KPI 來回答下列問題：</span><span class="sxs-lookup"><span data-stu-id="7765d-130">Based on recommendations from the IT team, the following Technical KPIs were added to answer the following questions:</span></span>

* <span data-ttu-id="7765d-131">我的使用者路徑為何 (所瀏覽的頁面、使用者在其中所花的時間長短)</span><span class="sxs-lookup"><span data-stu-id="7765d-131">What is my user path (which page is visited, how many time users spend on it)</span></span>
* <span data-ttu-id="7765d-132">每個工作階段發生當機或錯誤的次數？</span><span class="sxs-lookup"><span data-stu-id="7765d-132">Number of crashes or bugs encountered per session?</span></span>
* <span data-ttu-id="7765d-133">我的使用者執行哪些作業系統版本？</span><span class="sxs-lookup"><span data-stu-id="7765d-133">What OS versions are my users running?</span></span>
* <span data-ttu-id="7765d-134">我的使用者所用螢幕的平均大小為何？</span><span class="sxs-lookup"><span data-stu-id="7765d-134">What is the average size of screen for my users?</span></span>
* <span data-ttu-id="7765d-135">我的使用者擁有哪種網際網路連線？</span><span class="sxs-lookup"><span data-stu-id="7765d-135">What kind of internet connections do my users have?</span></span>

<span data-ttu-id="7765d-136">他針對每個 KPI 分類出所需的資料，並將其記錄在腳本的適當位置。</span><span class="sxs-lookup"><span data-stu-id="7765d-136">For each KPI, he classifies the data required and he records it in the proper location of his playbook.</span></span>

## <a name="engagement-program-and-integration"></a><span data-ttu-id="7765d-137">業務開發計劃和整合</span><span class="sxs-lookup"><span data-stu-id="7765d-137">Engagement program and integration</span></span>
<span data-ttu-id="7765d-138">現在 John 已定義好 KPI，於是他開始進行業務開發策略階段，他定義 4 個業務開發計劃和計劃目標：![][1]</span><span class="sxs-lookup"><span data-stu-id="7765d-138">Now that John has finished defining his KPIs, he starts his Engagement strategy phase by defining 4 engagement programs and their objectives: ![][1]</span></span>

<span data-ttu-id="7765d-139">然後 John 更進一步，詳細說明每個計劃的推播通知。</span><span class="sxs-lookup"><span data-stu-id="7765d-139">Then John goes deeper by detailing push notifications for each program.</span></span> <span data-ttu-id="7765d-140">推播通知是由五個項目所定義而成：</span><span class="sxs-lookup"><span data-stu-id="7765d-140">Push notification are defined by five elements:</span></span>

1. <span data-ttu-id="7765d-141">目標：通知目標為何</span><span class="sxs-lookup"><span data-stu-id="7765d-141">Objective: what is the objective of the notification</span></span>
2. <span data-ttu-id="7765d-142">如何達成目標</span><span class="sxs-lookup"><span data-stu-id="7765d-142">How the objective will be reached</span></span>
3. <span data-ttu-id="7765d-143">目標：誰會收到通知？</span><span class="sxs-lookup"><span data-stu-id="7765d-143">Target: who will receive the notification?</span></span>
4. <span data-ttu-id="7765d-144">內容：通知的措辭和格式 (應用程式內/應用程式外)</span><span class="sxs-lookup"><span data-stu-id="7765d-144">Content: What is the wording and the format of the notification (In App/Out of App)</span></span>
5. <span data-ttu-id="7765d-145">何時：此推播通知的最佳傳送時機為何</span><span class="sxs-lookup"><span data-stu-id="7765d-145">When: what is the best moment to send this push notification</span></span>
   
    ![][2]

<span data-ttu-id="7765d-146">如需詳細資訊，請參閱 [腳本](https://github.com/Azure/azure-mobile-engagement-samples/tree/master/Playbooks)。</span><span class="sxs-lookup"><span data-stu-id="7765d-146">For more information refer to the [Playbooks](https://github.com/Azure/azure-mobile-engagement-samples/tree/master/Playbooks).</span></span>

<span data-ttu-id="7765d-147">根據白皮書的第二部分，John 會使用目標區段來定義他必須收集的資料，並與 IT 小組共同撰寫標記計劃來實作解決方案。</span><span class="sxs-lookup"><span data-stu-id="7765d-147">According to the part 2 of the white paper John uses target section to define what data he has to collect and writes his Tag Plan jointly with IT team to implement the solution.</span></span> <span data-ttu-id="7765d-148">經過一星期的實作和使用者接受度測試後，John 終於可以啟動他的計劃。</span><span class="sxs-lookup"><span data-stu-id="7765d-148">After 1 week of implementation and user acceptance testing, John can finally launch his programs.</span></span>

## <a name="program-results"></a><span data-ttu-id="7765d-149">計劃結果</span><span class="sxs-lookup"><span data-stu-id="7765d-149">Program Results</span></span>
<span data-ttu-id="7765d-150">四個月之後，John 檢閱計劃的成效。</span><span class="sxs-lookup"><span data-stu-id="7765d-150">4 months later, John reviews performances of programs.</span></span> <span data-ttu-id="7765d-151">歡迎計劃和每週計劃有達成他的目標。</span><span class="sxs-lookup"><span data-stu-id="7765d-151">The Welcome Program and the Weekly Program are meeting his goals.</span></span> <span data-ttu-id="7765d-152">只有一個工作階段的使用者數目減少、受到使用的應用程式功能變多，而且每週的連線數目翻倍。</span><span class="sxs-lookup"><span data-stu-id="7765d-152">The number of user with only one session decreases, more features of the app are being used and the number of connections per week has doubled.</span></span>

<span data-ttu-id="7765d-153">**無活動計劃** 協助 John 了解了使用者的喜好傾向。</span><span class="sxs-lookup"><span data-stu-id="7765d-153">The **Inactive Program** is helping John understand user tendencies.</span></span> <span data-ttu-id="7765d-154">看來有 15% 的無活動使用者回來使用應用程式。</span><span class="sxs-lookup"><span data-stu-id="7765d-154">It appears that 15% of the inactive users come back to the app.</span></span> <span data-ttu-id="7765d-155">不過，這些人大多不會持續使用超過 1 個月。</span><span class="sxs-lookup"><span data-stu-id="7765d-155">However most of them don’t stay active more than 1 month.</span></span> <span data-ttu-id="7765d-156">John 預計在透過其他通知並擴大其內容的選擇性後，應該可以讓這個順序變成最好的情況。</span><span class="sxs-lookup"><span data-stu-id="7765d-156">John foresees a potential optimization of this sequence with additional notifications and expanding his content choices.</span></span>

<span data-ttu-id="7765d-157">**探索計劃** 的效果不好。</span><span class="sxs-lookup"><span data-stu-id="7765d-157">The **Discover Program** doesn’t work well.</span></span> <span data-ttu-id="7765d-158">交叉銷售量是增加了，但不足以達到其目標。</span><span class="sxs-lookup"><span data-stu-id="7765d-158">It increases cross selling but not enough to reach his objectives.</span></span> <span data-ttu-id="7765d-159">John 發現他沒有足夠資料能夠鎖定相關目標並提出適當內容。</span><span class="sxs-lookup"><span data-stu-id="7765d-159">John identifies that he doesn’t have enough data to make relevant targeting and propose appropriate content.</span></span> <span data-ttu-id="7765d-160">於是他停止這個計劃，並將重心放在使用 Azure Mobile Engagement 傳送「評論推播通知」。</span><span class="sxs-lookup"><span data-stu-id="7765d-160">He stops this program and focuses on sending “editorial push notifications” with Azure Mobile Engagement.</span></span> <span data-ttu-id="7765d-161">他手下的記者已經有 CMS 解決方案可用來傳送推播通知，所以不想做改變。</span><span class="sxs-lookup"><span data-stu-id="7765d-161">His journalists already have a CMS solution to send push notifications and they don’t want to change.</span></span>

<span data-ttu-id="7765d-162">John 決定使用觸達 API，這種 HTTP REST API 可讓他們管理觸達活動，但又不需要使用 AZME Web 介面。</span><span class="sxs-lookup"><span data-stu-id="7765d-162">John decides to use the Reach API which is an HTTP REST API that allows managing Reach campaigns without having to use AZME Web interface.</span></span> <span data-ttu-id="7765d-163">透過這種方式，John 就可以收集所需資料，並讓他的撰稿人能夠繼續使用 CMS 解決方案。</span><span class="sxs-lookup"><span data-stu-id="7765d-163">With this approach John can collect the data he needs and allow his writers to keep using the CMS solution.</span></span>

<span data-ttu-id="7765d-164">為了確保該功能正常運作，John 要求 IT 小組注意下列事項：</span><span class="sxs-lookup"><span data-stu-id="7765d-164">To ensure that feature works correctly, John asks IT team to be vigilant on the following points:</span></span>

1. <span data-ttu-id="7765d-165">**作業系統** ：他們各有自己的推播通知管理規則，因此 John 決定列出所有情形，並看看 API 是否能夠處理得來。</span><span class="sxs-lookup"><span data-stu-id="7765d-165">**Operation Systems** : They all have their own rules to administrate push notifications, so John decides to list all cases and checks if the APIs handle it.</span></span>
   <span data-ttu-id="7765d-166">例如：Android 推播系統允許大型圖片，但 iOS 則不行。</span><span class="sxs-lookup"><span data-stu-id="7765d-166">E.g : Android push system allows big picture which is not the case with iOS.</span></span>
2. <span data-ttu-id="7765d-167">**時間範圍**：John 所想要的 API 要能夠設定時間範圍，並設定活動的結束時間。</span><span class="sxs-lookup"><span data-stu-id="7765d-167">**Time frame**: John wants an API, which set the time frame and set an end to campaigns.</span></span> <span data-ttu-id="7765d-168">他不希望使用者因為收到接二連三的通知而感覺受到打擾。</span><span class="sxs-lookup"><span data-stu-id="7765d-168">He wants to preserve users from any disruptive notification bombing.</span></span>
3. <span data-ttu-id="7765d-169">**類別**：行銷小組準備了每種警示類型的範本。</span><span class="sxs-lookup"><span data-stu-id="7765d-169">**Categories**: Marketing team prepares template for each type of alerting.</span></span> <span data-ttu-id="7765d-170">John 要求 IT 小組在 API 內設定類別。</span><span class="sxs-lookup"><span data-stu-id="7765d-170">John asks IT team to set categories inside the API.</span></span>

<span data-ttu-id="7765d-171">在做過一些測試之後，John 感到非常滿意。</span><span class="sxs-lookup"><span data-stu-id="7765d-171">After some tests John is satisfied.</span></span> <span data-ttu-id="7765d-172">多虧有這個 API，記者們仍然可以使用他們的 CMS 傳送推播通知，而 Azure Mobile Engagement 會幫他們收集所有使用行為資料。</span><span class="sxs-lookup"><span data-stu-id="7765d-172">Thanks to this API, journalists can still send push notifications with their CMS and Azure Mobile Engagement collects all behavioral data for them</span></span>

<span data-ttu-id="7765d-173">在經過最初四個月後，所得到的結果顯示整體成效良好，這讓 John 和他的董事會成員深具信心，每個使用者的 ROI 增加 15%，行動銷售佔總銷售量 17.5%，僅僅四個月就增加了 7.5%。</span><span class="sxs-lookup"><span data-stu-id="7765d-173">After these 4 first months, results reflect a good overall performance and gives confidence for John and his board, ROI per user increases per 15% and mobile sales represent 17.5 % of total sales, an increase of 7.5% in only four months.</span></span>

<!--Image references-->
[1]: ./media/mobile-engagement-media-scenario/engagement-strategy.png
[2]: ./media/mobile-engagement-media-scenario/push-scenarios.png

<!--Link references-->
[Media Playbook link]: https://github.com/Azure/azure-mobile-engagement-samples/tree/master/Playbooks
