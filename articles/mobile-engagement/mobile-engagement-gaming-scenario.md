---
title: "對遊戲應用程式實作 Azure Mobile Engagement"
description: "對遊戲應用程式實作 Azure Mobile Engagement 的案例"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 2cafc044-4902-4058-8037-49399bf6bf7f
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 0ca35a3d634db8eb5c63afacba046a35b8a3e7ed
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="implement-mobile-engagement-with-gaming-app"></a><span data-ttu-id="062cd-103">對遊戲應用程式實作 Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="062cd-103">Implement Mobile Engagement with Gaming App</span></span>
## <a name="overview"></a><span data-ttu-id="062cd-104">Overview</span><span class="sxs-lookup"><span data-stu-id="062cd-104">Overview</span></span>
<span data-ttu-id="062cd-105">某家新創遊戲公司推出了一款新的釣魚角色扮演/策略遊戲應用程式。</span><span class="sxs-lookup"><span data-stu-id="062cd-105">A gaming start-up has launched a new fishing based role-play/strategy game app.</span></span> <span data-ttu-id="062cd-106">該遊戲已上線運作 6 個月之久，</span><span class="sxs-lookup"><span data-stu-id="062cd-106">The game has been up and running for 6 months.</span></span> <span data-ttu-id="062cd-107">所創造的成績非常優異，下載人數已達數百萬，且相較於其他新創公司所推出的遊戲應用程式，這款遊戲的保留期相當高。</span><span class="sxs-lookup"><span data-stu-id="062cd-107">This game is a huge success, and it has millions of downloads and the retention is very high compared to other start-up game apps.</span></span> <span data-ttu-id="062cd-108">在每季檢討會議中，重要關係人一致認為他們需要增加每位使用者的平均營收 (ARPU)。</span><span class="sxs-lookup"><span data-stu-id="062cd-108">At the quarterly review meeting, stakeholders agree they need to increase average revenue per user (ARPU).</span></span> <span data-ttu-id="062cd-109">他們在遊戲中提供高階套件做為特殊優惠。</span><span class="sxs-lookup"><span data-stu-id="062cd-109">Premium in-game packages are available as special offers.</span></span> <span data-ttu-id="062cd-110">這些遊戲套件可讓使用者升級他們在遊戲中所用釣線和誘餌或釣具的外觀和效果。</span><span class="sxs-lookup"><span data-stu-id="062cd-110">These game packs allow users to upgrade the appearance and performance of their fishing lines and lures or tackles in the game.</span></span> <span data-ttu-id="062cd-111">不過，這些套件的銷售成績非常差。</span><span class="sxs-lookup"><span data-stu-id="062cd-111">However, package sales are very low.</span></span> <span data-ttu-id="062cd-112">因此他們決定先使用分析工具分析客戶在玩遊戲時的體驗，然後發展業務開發計劃，透過進一步劃分玩家來增加銷售額。</span><span class="sxs-lookup"><span data-stu-id="062cd-112">So they decide first to analyze the customer experience with an analytics tool, and then to develop an engagement program to increase sales using advanced segmentation.</span></span>

<span data-ttu-id="062cd-113">他們根據 [Azure Mobile Engagement - 入門指南與最佳作法](mobile-engagement-getting-started-best-practices.md) 建構了業務開發策略。</span><span class="sxs-lookup"><span data-stu-id="062cd-113">Based on the [Azure Mobile Engagement - Getting Started Guide with Best practices](mobile-engagement-getting-started-best-practices.md) they build an engagement strategy.</span></span>

## <a name="objectives-and-kpis"></a><span data-ttu-id="062cd-114">目標和 KPI</span><span class="sxs-lookup"><span data-stu-id="062cd-114">Objectives and KPIs</span></span>
<span data-ttu-id="062cd-115">該遊戲的重要關係人齊聚一堂。</span><span class="sxs-lookup"><span data-stu-id="062cd-115">Key stakeholders for the game meet.</span></span> <span data-ttu-id="062cd-116">所有人都同意一個主要目標，那就是將高階套件的銷售量增加 15%。</span><span class="sxs-lookup"><span data-stu-id="062cd-116">All agree on one main objective - to increase premium package sales by 15%.</span></span> <span data-ttu-id="062cd-117">他們建立起業務關鍵效能指標 (KPI)，以便測量和推動這個目標。</span><span class="sxs-lookup"><span data-stu-id="062cd-117">They create Business Key Performance Indicators (KPIs) to measure and drive this objective</span></span>

* <span data-ttu-id="062cd-118">使用者會在到達哪個遊戲等級時購買這些套件？</span><span class="sxs-lookup"><span data-stu-id="062cd-118">On which level of the game are these packages purchased?</span></span>
* <span data-ttu-id="062cd-119">每位使用者、每個工作階段、每週和每月的營收為何？</span><span class="sxs-lookup"><span data-stu-id="062cd-119">What is the revenue per user, per session, per week, and per month?</span></span>
* <span data-ttu-id="062cd-120">最愛的購買類型為何？</span><span class="sxs-lookup"><span data-stu-id="062cd-120">What are the favorite purchase types?</span></span>

<span data-ttu-id="062cd-121">[入門指南](mobile-engagement-getting-started-best-practices.md) 的第 1 部分說明如何定義目標和 KPI。</span><span class="sxs-lookup"><span data-stu-id="062cd-121">Part 1 of the [Getting Started Guide](mobile-engagement-getting-started-best-practices.md) explains how to define the objectives and KPIs.</span></span> 

<span data-ttu-id="062cd-122">現在已定義好業務 KPI，行動裝置產品經理接著會建立業務開發 KPI，以確定新的使用者趨勢和保留期。</span><span class="sxs-lookup"><span data-stu-id="062cd-122">With the Business KPIs now defined, the Mobile Product Manager creates Engagement KPIs to determine new user trends and retention.</span></span>

* <span data-ttu-id="062cd-123">監視下列時間間隔的保留期和使用情形：每天、每 2 天、每週、每月和每 3 個月</span><span class="sxs-lookup"><span data-stu-id="062cd-123">Monitor retention and use across the following intervals: daily, every 2 days, weekly, monthly and every 3 months</span></span>
* <span data-ttu-id="062cd-124">活躍使用者人數</span><span class="sxs-lookup"><span data-stu-id="062cd-124">Active user counts</span></span>
* <span data-ttu-id="062cd-125">應用程式在市集內的評分</span><span class="sxs-lookup"><span data-stu-id="062cd-125">The app rating in the store</span></span>

<span data-ttu-id="062cd-126">根據 IT 團隊所提的建議，他新增了下列技術 KPI 來回答下列問題：</span><span class="sxs-lookup"><span data-stu-id="062cd-126">Based on recommendations from the IT team, the following technical KPIs were added to answer the following questions:</span></span>

* <span data-ttu-id="062cd-127">我的使用者路徑為何 (所瀏覽的頁面、使用者在其中所花的時間長短)</span><span class="sxs-lookup"><span data-stu-id="062cd-127">What is my user path (which page is visited, how much time users spend on it)</span></span>
* <span data-ttu-id="062cd-128">每個工作階段發生當機或錯誤的次數</span><span class="sxs-lookup"><span data-stu-id="062cd-128">Number of crashes or bugs encountered per session</span></span>
* <span data-ttu-id="062cd-129">我的使用者執行哪些作業系統版本？</span><span class="sxs-lookup"><span data-stu-id="062cd-129">What OS versions are my users running?</span></span>
* <span data-ttu-id="062cd-130">我的使用者所用螢幕的平均大小為何？</span><span class="sxs-lookup"><span data-stu-id="062cd-130">What is the average size of screen for my users?</span></span>
* <span data-ttu-id="062cd-131">我的使用者擁有哪種網際網路連線？</span><span class="sxs-lookup"><span data-stu-id="062cd-131">What kind of internet connectivity do my users have?</span></span>

<span data-ttu-id="062cd-132">行動裝置產品經理針對每個 KPI 指定她需要的資料，以及其在腳本中的位置。</span><span class="sxs-lookup"><span data-stu-id="062cd-132">For each KPI the Mobile Product Manager specifies the data she needs and where it is located in her playbook.</span></span>

## <a name="engagement-program-and-integration"></a><span data-ttu-id="062cd-133">業務開發計劃和整合</span><span class="sxs-lookup"><span data-stu-id="062cd-133">Engagement program and integration</span></span>
<span data-ttu-id="062cd-134">在建置進階業務開發計劃之前，負責該項專案的行動裝置專案主任應該先深入了解使用者使用產品的方式和時間。</span><span class="sxs-lookup"><span data-stu-id="062cd-134">Before building an advanced engagement program, the Mobile Project Director in charge of the project should have a deep understanding of how and when products are consumed by the users.</span></span>

<span data-ttu-id="062cd-135">3 個月過後，行動裝置專案主任已收集足夠的資料，可以加強他的應用程式內推播通知銷售額。</span><span class="sxs-lookup"><span data-stu-id="062cd-135">After 3 months, the Mobile Project Director has collected enough data to enhance his in-app push notification sales.</span></span> <span data-ttu-id="062cd-136">他發現到：</span><span class="sxs-lookup"><span data-stu-id="062cd-136">He learns that:</span></span>

* <span data-ttu-id="062cd-137">第一次購買通常發生在 14 級，</span><span class="sxs-lookup"><span data-stu-id="062cd-137">The first purchase generally happens at the level 14.</span></span> <span data-ttu-id="062cd-138">其中有 90% 會購買價格 3 美元的新傳說級武器，</span><span class="sxs-lookup"><span data-stu-id="062cd-138">For 90% of those cases, the purchase is new legendary weapons for $3.</span></span>
* <span data-ttu-id="062cd-139">而購買過的使用者中有 80% 會繼續使用產品並購買其他裝備。</span><span class="sxs-lookup"><span data-stu-id="062cd-139">In 80 % of those cases, users who have made a purchase, continue with the product and make more purchases.</span></span>
* <span data-ttu-id="062cd-140">超過 20 級的使用者會開始每週花費超過 10 美元。</span><span class="sxs-lookup"><span data-stu-id="062cd-140">Users who have passed the level 20, start to spend more than $10/week.</span></span>
* <span data-ttu-id="062cd-141">使用者往往會在 16 級、24 級和 32 級時購買高階套件。</span><span class="sxs-lookup"><span data-stu-id="062cd-141">Users tend to buy premium packages at level 16, 24 and 32.</span></span>

<span data-ttu-id="062cd-142">多虧了這項分析，行動裝置專案主任決定建立特定的推播通知順序，以增加應用程式內銷售額。</span><span class="sxs-lookup"><span data-stu-id="062cd-142">Thanks to this analysis the Mobile Project Director decides to create specific push notification sequences to increase in app sales.</span></span> <span data-ttu-id="062cd-143">他建立了三個他稱為「歡迎計劃」、「銷售計劃」和「無活動計劃」的推播順序。</span><span class="sxs-lookup"><span data-stu-id="062cd-143">He creates three push sequences which he calls: Welcome program, Sales Program, and Inactive Program.</span></span> <span data-ttu-id="062cd-144">如需詳細資訊請參閱[Playbooks](https://github.com/Azure/azure-mobile-engagement-samples/tree/master/Playbooks)![][1]</span><span class="sxs-lookup"><span data-stu-id="062cd-144">For more information refer to the [Playbooks](https://github.com/Azure/azure-mobile-engagement-samples/tree/master/Playbooks) ![][1]</span></span>

<!--Image references-->

[1]: ./media/mobile-engagement-game-scenario/notification-scenario.png

<!--Link references-->
