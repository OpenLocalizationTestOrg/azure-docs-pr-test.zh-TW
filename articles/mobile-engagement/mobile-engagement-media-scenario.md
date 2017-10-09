---
title: "aaaAzure Mobile Engagement 應用程式的實作"
description: "媒體應用程式案例 tooimplement Azure Mobile Engagement"
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
ms.openlocfilehash: 6a495eb790993a30d5c03802aa9e6404fea983d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="implement-mobile-engagement-with-media-app"></a><span data-ttu-id="ddee5-103">對媒體應用程式實作 Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="ddee5-103">Implement Mobile Engagement with Media App</span></span>
## <a name="overview"></a><span data-ttu-id="ddee5-104">Overview</span><span class="sxs-lookup"><span data-stu-id="ddee5-104">Overview</span></span>
<span data-ttu-id="ddee5-105">John 是一家大型媒體公司的行動裝置專案經理。</span><span class="sxs-lookup"><span data-stu-id="ddee5-105">John is a mobile project manager for a big media company.</span></span> <span data-ttu-id="ddee5-106">他最近推出了一款新的應用程式，並獲得很高的下載次數。</span><span class="sxs-lookup"><span data-stu-id="ddee5-106">He recently launched a new app that has a very high download count.</span></span> <span data-ttu-id="ddee5-107">他已達成預定的下載次數目標，但從每位使用者身上所獲得的投資回報 (ROI) 卻未達要求。</span><span class="sxs-lookup"><span data-stu-id="ddee5-107">He has hit his goals for download but, still his Return On Investment(ROI) per user does not meet his requirements.</span></span> 

<span data-ttu-id="ddee5-108">John 已找到 ROI 太低的原因。</span><span class="sxs-lookup"><span data-stu-id="ddee5-108">John has already identified why his ROI is too low.</span></span> <span data-ttu-id="ddee5-109">使用者經常在短短 2 週後就停止使用他的應用程式，而且大多不會再回頭使用。</span><span class="sxs-lookup"><span data-stu-id="ddee5-109">Users frequently stop using his app after only 2 weeks and most of them never come back.</span></span> <span data-ttu-id="ddee5-110">他希望他的應用程式的 tooincrease hello 保留。</span><span class="sxs-lookup"><span data-stu-id="ddee5-110">He wants tooincrease hello retention of his app.</span></span>

<span data-ttu-id="ddee5-111">某些初始測試之後，他已取得他必須由他的使用者使用推播通知，他們傾向 toocontinue 使用他的應用程式。</span><span class="sxs-lookup"><span data-stu-id="ddee5-111">After some initial testing, he has learned when he engages his users with push notifications, they tend toocontinue using his app.</span></span> <span data-ttu-id="ddee5-112">也非使用中的使用者通常會傳回 toohello 根據他將傳送的通知的應用程式。</span><span class="sxs-lookup"><span data-stu-id="ddee5-112">Also users that were inactive will often return toohello app depending on notifications he sends them.</span></span> <span data-ttu-id="ddee5-113">John 會決定 tooinvest 某種 Engagement 程式中的使用進階的目標使用推播通知其應用程式。</span><span class="sxs-lookup"><span data-stu-id="ddee5-113">John decides tooinvest in some kind of Engagement Program for his app which uses advanced targeting with push notifications.</span></span>

<span data-ttu-id="ddee5-114">John 具有最近讀取 hello [Azure Mobile Engagement 入門指南最佳做法](mobile-engagement-getting-started-best-practices.md)，決定 hello 指南 tooimplement hello 建議。</span><span class="sxs-lookup"><span data-stu-id="ddee5-114">John has recently read hello [Azure Mobile Engagement - Getting Started Guide with Best practices](mobile-engagement-getting-started-best-practices.md) and has decided tooimplement hello recommendations from hello guide.</span></span>

## <a name="objectives-and-kpis"></a><span data-ttu-id="ddee5-115">目標和 KPI</span><span class="sxs-lookup"><span data-stu-id="ddee5-115">Objectives and KPIs</span></span>
<span data-ttu-id="ddee5-116">John 所推出的應用程式的重要關係人聚在一起。</span><span class="sxs-lookup"><span data-stu-id="ddee5-116">Key stakeholders for John's app meet.</span></span> <span data-ttu-id="ddee5-117">當使用者使用他的媒體時，其中的廣告便會為他們帶來生意。</span><span class="sxs-lookup"><span data-stu-id="ddee5-117">Business is generated from ads as users consume his media.</span></span> <span data-ttu-id="ddee5-118">所以只要增加每位使用者使用的內容，John 就能增加營收。</span><span class="sxs-lookup"><span data-stu-id="ddee5-118">By increasing content consumed per user, John increases his revenues.</span></span> <span data-ttu-id="ddee5-119">所有同意上一個主要目標： tooincrease 銷售 25%的廣告。</span><span class="sxs-lookup"><span data-stu-id="ddee5-119">All agree on one main objective: tooincrease sales from ads by 25%.</span></span> <span data-ttu-id="ddee5-120">他們建立商務關鍵效能指標 (Kpi) toomeasure 和磁碟機此目標</span><span class="sxs-lookup"><span data-stu-id="ddee5-120">They create Business Key Performance Indicators (KPIs) toomeasure and drive this objective</span></span>

* <span data-ttu-id="ddee5-121">每位使用者點按的廣告數目</span><span class="sxs-lookup"><span data-stu-id="ddee5-121">Number of ads clicked per user</span></span>
* <span data-ttu-id="ddee5-122">(每位使用者/每個工作階段/每週/每月...) 瀏覽過多少文章頁面</span><span class="sxs-lookup"><span data-stu-id="ddee5-122">How many article pages visited (per user/ per session/ per week / per month…)</span></span>
* <span data-ttu-id="ddee5-123">最愛的類別有哪些</span><span class="sxs-lookup"><span data-stu-id="ddee5-123">What are favorite categories</span></span>

<span data-ttu-id="ddee5-124">John 根據他與重要關係人的會面結果，定義了他的業務 KPI。</span><span class="sxs-lookup"><span data-stu-id="ddee5-124">Based on John's meeting with key stakeholders he has defined his Business KPIs.</span></span> <span data-ttu-id="ddee5-125">他會遵循 hello 的第 1 部分[Azure Mobile Engagement 入門指南最佳做法](mobile-engagement-getting-started-best-practices.md)。</span><span class="sxs-lookup"><span data-stu-id="ddee5-125">He follows Part 1 of hello [Azure Mobile Engagement - Getting Started Guide with Best practices](mobile-engagement-getting-started-best-practices.md).</span></span> 

<span data-ttu-id="ddee5-126">接下來，他會建立下列達到目標的 Engagement Kpi tooensure hello:</span><span class="sxs-lookup"><span data-stu-id="ddee5-126">Next, he creates hello following Engagement KPIs tooensure that objectives are reached:</span></span>

* <span data-ttu-id="ddee5-127">監視保留跨 hello 下列間隔： 每日、 每週、 隔週和每月。</span><span class="sxs-lookup"><span data-stu-id="ddee5-127">Monitor retention across hello following intervals: daily, weekly, bi-weekly and monthly.</span></span>
* <span data-ttu-id="ddee5-128">活躍使用者人數</span><span class="sxs-lookup"><span data-stu-id="ddee5-128">Active users counts</span></span>
* <span data-ttu-id="ddee5-129">儲存在 hello 應用程式中的 hello 應用程式分級</span><span class="sxs-lookup"><span data-stu-id="ddee5-129">hello app rating in hello app stores</span></span>

<span data-ttu-id="ddee5-130">根據從 hello IT 團隊的建議，下列技術 Kpi hello 已加入 tooanswer hello 下列問題：</span><span class="sxs-lookup"><span data-stu-id="ddee5-130">Based on recommendations from hello IT team, hello following Technical KPIs were added tooanswer hello following questions:</span></span>

* <span data-ttu-id="ddee5-131">我的使用者路徑為何 (所瀏覽的頁面、使用者在其中所花的時間長短)</span><span class="sxs-lookup"><span data-stu-id="ddee5-131">What is my user path (which page is visited, how many time users spend on it)</span></span>
* <span data-ttu-id="ddee5-132">每個工作階段發生當機或錯誤的次數？</span><span class="sxs-lookup"><span data-stu-id="ddee5-132">Number of crashes or bugs encountered per session?</span></span>
* <span data-ttu-id="ddee5-133">我的使用者執行哪些作業系統版本？</span><span class="sxs-lookup"><span data-stu-id="ddee5-133">What OS versions are my users running?</span></span>
* <span data-ttu-id="ddee5-134">Hello 畫面的 我的使用者的平均大小為何？</span><span class="sxs-lookup"><span data-stu-id="ddee5-134">What is hello average size of screen for my users?</span></span>
* <span data-ttu-id="ddee5-135">我的使用者擁有哪種網際網路連線？</span><span class="sxs-lookup"><span data-stu-id="ddee5-135">What kind of internet connections do my users have?</span></span>

<span data-ttu-id="ddee5-136">針對每一個 KPI，他複製 hello 資料所需的分類，他會加以記錄他腳本 hello 適當位置中。</span><span class="sxs-lookup"><span data-stu-id="ddee5-136">For each KPI, he classifies hello data required and he records it in hello proper location of his playbook.</span></span>

## <a name="engagement-program-and-integration"></a><span data-ttu-id="ddee5-137">業務開發計劃和整合</span><span class="sxs-lookup"><span data-stu-id="ddee5-137">Engagement program and integration</span></span>
<span data-ttu-id="ddee5-138">現在 John 已定義好 KPI，於是他開始進行業務開發策略階段，他定義 4 個業務開發計劃和計劃目標：![][1]</span><span class="sxs-lookup"><span data-stu-id="ddee5-138">Now that John has finished defining his KPIs, he starts his Engagement strategy phase by defining 4 engagement programs and their objectives: ![][1]</span></span>

<span data-ttu-id="ddee5-139">然後 John 更進一步，詳細說明每個計劃的推播通知。</span><span class="sxs-lookup"><span data-stu-id="ddee5-139">Then John goes deeper by detailing push notifications for each program.</span></span> <span data-ttu-id="ddee5-140">推播通知是由五個項目所定義而成：</span><span class="sxs-lookup"><span data-stu-id="ddee5-140">Push notification are defined by five elements:</span></span>

1. <span data-ttu-id="ddee5-141">目標： hello hello 通知目標為何</span><span class="sxs-lookup"><span data-stu-id="ddee5-141">Objective: what is hello objective of hello notification</span></span>
2. <span data-ttu-id="ddee5-142">如何將到達 hello 目標</span><span class="sxs-lookup"><span data-stu-id="ddee5-142">How hello objective will be reached</span></span>
3. <span data-ttu-id="ddee5-143">目標： 將會收到 hello 通知的人員？</span><span class="sxs-lookup"><span data-stu-id="ddee5-143">Target: who will receive hello notification?</span></span>
4. <span data-ttu-id="ddee5-144">何謂 hello 用語和 hello hello 通知 （在 App/Out 的應用程式） 格式的內容:</span><span class="sxs-lookup"><span data-stu-id="ddee5-144">Content: What is hello wording and hello format of hello notification (In App/Out of App)</span></span>
5. <span data-ttu-id="ddee5-145">當： 什麼是 hello 最佳時刻 toosend 此推播通知</span><span class="sxs-lookup"><span data-stu-id="ddee5-145">When: what is hello best moment toosend this push notification</span></span>
   
    ![][2]

<span data-ttu-id="ddee5-146">如需詳細資訊，請參閱 toohello [Playbooks](https://github.com/Azure/azure-mobile-engagement-samples/tree/master/Playbooks)。</span><span class="sxs-lookup"><span data-stu-id="ddee5-146">For more information refer toohello [Playbooks](https://github.com/Azure/azure-mobile-engagement-samples/tree/master/Playbooks).</span></span>

<span data-ttu-id="ddee5-147">Toocollect 和寫入其標記共同計劃與 IT 小組 tooimplement hello 方案，請根據 toohello 第 2 部分的 hello John 會使用目標區段 toodefine 他有哪些資料的技術白皮書。</span><span class="sxs-lookup"><span data-stu-id="ddee5-147">According toohello part 2 of hello white paper John uses target section toodefine what data he has toocollect and writes his Tag Plan jointly with IT team tooimplement hello solution.</span></span> <span data-ttu-id="ddee5-148">經過一星期的實作和使用者接受度測試後，John 終於可以啟動他的計劃。</span><span class="sxs-lookup"><span data-stu-id="ddee5-148">After 1 week of implementation and user acceptance testing, John can finally launch his programs.</span></span>

## <a name="program-results"></a><span data-ttu-id="ddee5-149">計劃結果</span><span class="sxs-lookup"><span data-stu-id="ddee5-149">Program Results</span></span>
<span data-ttu-id="ddee5-150">四個月之後，John 檢閱計劃的成效。</span><span class="sxs-lookup"><span data-stu-id="ddee5-150">4 months later, John reviews performances of programs.</span></span> <span data-ttu-id="ddee5-151">hello  褖畫惎程式與 hello 每週程式達成其目標。</span><span class="sxs-lookup"><span data-stu-id="ddee5-151">hello Welcome Program and hello Weekly Program are meeting his goals.</span></span> <span data-ttu-id="ddee5-152">減少 hello 與只有一個工作階段的使用者數目、 hello 應用程式的多個功能的使用和 hello 每週的連線數目加倍。</span><span class="sxs-lookup"><span data-stu-id="ddee5-152">hello number of user with only one session decreases, more features of hello app are being used and hello number of connections per week has doubled.</span></span>

<span data-ttu-id="ddee5-153">hello**非作用中的程式**協助了解使用者勤者傾向 John。</span><span class="sxs-lookup"><span data-stu-id="ddee5-153">hello **Inactive Program** is helping John understand user tendencies.</span></span> <span data-ttu-id="ddee5-154">它會顯示 hello 非作用中使用者的 15%回來 toohello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="ddee5-154">It appears that 15% of hello inactive users come back toohello app.</span></span> <span data-ttu-id="ddee5-155">不過，這些人大多不會持續使用超過 1 個月。</span><span class="sxs-lookup"><span data-stu-id="ddee5-155">However most of them don’t stay active more than 1 month.</span></span> <span data-ttu-id="ddee5-156">John 預計在透過其他通知並擴大其內容的選擇性後，應該可以讓這個順序變成最好的情況。</span><span class="sxs-lookup"><span data-stu-id="ddee5-156">John foresees a potential optimization of this sequence with additional notifications and expanding his content choices.</span></span>

<span data-ttu-id="ddee5-157">hello**探索程式**不正常運作。</span><span class="sxs-lookup"><span data-stu-id="ddee5-157">hello **Discover Program** doesn’t work well.</span></span> <span data-ttu-id="ddee5-158">它就會增加交叉銷售，但沒有足夠 tooreach 他的目標。</span><span class="sxs-lookup"><span data-stu-id="ddee5-158">It increases cross selling but not enough tooreach his objectives.</span></span> <span data-ttu-id="ddee5-159">John 會識別他不具有足夠資料 toomake 相關目標，並提議適當的內容。</span><span class="sxs-lookup"><span data-stu-id="ddee5-159">John identifies that he doesn’t have enough data toomake relevant targeting and propose appropriate content.</span></span> <span data-ttu-id="ddee5-160">於是他停止這個計劃，並將重心放在使用 Azure Mobile Engagement 傳送「評論推播通知」。</span><span class="sxs-lookup"><span data-stu-id="ddee5-160">He stops this program and focuses on sending “editorial push notifications” with Azure Mobile Engagement.</span></span> <span data-ttu-id="ddee5-161">他記者已經 CMS 解決方案 toosend 推播通知，而且它們不想 toochange。</span><span class="sxs-lookup"><span data-stu-id="ddee5-161">His journalists already have a CMS solution toosend push notifications and they don’t want toochange.</span></span>

<span data-ttu-id="ddee5-162">John 會決定 toouse hello 觸達 API 也就是 HTTP 的 REST API，可讓您管理觸達活動，而不需要 toouse AZME Web 介面。</span><span class="sxs-lookup"><span data-stu-id="ddee5-162">John decides toouse hello Reach API which is an HTTP REST API that allows managing Reach campaigns without having toouse AZME Web interface.</span></span> <span data-ttu-id="ddee5-163">透過這種方式 John 可以收集 hello 資料他需要並讓他的寫入器 tookeep 使用 hello CMS 解決方案。</span><span class="sxs-lookup"><span data-stu-id="ddee5-163">With this approach John can collect hello data he needs and allow his writers tookeep using hello CMS solution.</span></span>

<span data-ttu-id="ddee5-164">正確功能如何運作的 tooensure，John 詢問 IT 小組 toobe 警覺 hello 遵循點上：</span><span class="sxs-lookup"><span data-stu-id="ddee5-164">tooensure that feature works correctly, John asks IT team toobe vigilant on hello following points:</span></span>

1. <span data-ttu-id="ddee5-165">**作業系統**： 它們具有自己的規則 tooadministrate 推播通知 」，所以 John 決定 toolist 所有情況下，檢查是否 hello Api 處理它。</span><span class="sxs-lookup"><span data-stu-id="ddee5-165">**Operation Systems** : They all have their own rules tooadministrate push notifications, so John decides toolist all cases and checks if hello APIs handle it.</span></span>
   <span data-ttu-id="ddee5-166">例如： Android 推播系統可讓不是使用 iOS 的 hello 情況大圖片。</span><span class="sxs-lookup"><span data-stu-id="ddee5-166">E.g : Android push system allows big picture which is not hello case with iOS.</span></span>
2. <span data-ttu-id="ddee5-167">**時間範圍**: John 想要的 API，以設定 hello 的時間範圍，並設定結束 toocampaigns。</span><span class="sxs-lookup"><span data-stu-id="ddee5-167">**Time frame**: John wants an API, which set hello time frame and set an end toocampaigns.</span></span> <span data-ttu-id="ddee5-168">他想從任何具有干擾性通知擊 toopreserve 使用者。</span><span class="sxs-lookup"><span data-stu-id="ddee5-168">He wants toopreserve users from any disruptive notification bombing.</span></span>
3. <span data-ttu-id="ddee5-169">**類別**：行銷小組準備了每種警示類型的範本。</span><span class="sxs-lookup"><span data-stu-id="ddee5-169">**Categories**: Marketing team prepares template for each type of alerting.</span></span> <span data-ttu-id="ddee5-170">John 會詢問 IT 小組 tooset 類別內 hello 應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="ddee5-170">John asks IT team tooset categories inside hello API.</span></span>

<span data-ttu-id="ddee5-171">在做過一些測試之後，John 感到非常滿意。</span><span class="sxs-lookup"><span data-stu-id="ddee5-171">After some tests John is satisfied.</span></span> <span data-ttu-id="ddee5-172">感謝您 toothis API，記者仍然可以傳送推播通知，以其 CMS 和 Azure Mobile Engagement 會為其收集行為的所有資料</span><span class="sxs-lookup"><span data-stu-id="ddee5-172">Thanks toothis API, journalists can still send push notifications with their CMS and Azure Mobile Engagement collects all behavioral data for them</span></span>

<span data-ttu-id="ddee5-173">在經過最初四個月後，所得到的結果顯示整體成效良好，這讓 John 和他的董事會成員深具信心，每個使用者的 ROI 增加 15%，行動銷售佔總銷售量 17.5%，僅僅四個月就增加了 7.5%。</span><span class="sxs-lookup"><span data-stu-id="ddee5-173">After these 4 first months, results reflect a good overall performance and gives confidence for John and his board, ROI per user increases per 15% and mobile sales represent 17.5 % of total sales, an increase of 7.5% in only four months.</span></span>

<!--Image references-->
[1]: ./media/mobile-engagement-media-scenario/engagement-strategy.png
[2]: ./media/mobile-engagement-media-scenario/push-scenarios.png

<!--Link references-->
[Media Playbook link]: https://github.com/Azure/azure-mobile-engagement-samples/tree/master/Playbooks
