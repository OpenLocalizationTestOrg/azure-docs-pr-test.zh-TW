---
title: "aaaAzure Mobile Engagement 實作遊戲應用程式"
description: "遊戲應用程式案例 tooimplement Azure Mobile Engagement"
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
ms.openlocfilehash: b82b4a868a33f42e5b759e43e66103556c097f9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="implement-mobile-engagement-with-gaming-app"></a><span data-ttu-id="62181-103">對遊戲應用程式實作 Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="62181-103">Implement Mobile Engagement with Gaming App</span></span>
## <a name="overview"></a><span data-ttu-id="62181-104">Overview</span><span class="sxs-lookup"><span data-stu-id="62181-104">Overview</span></span>
<span data-ttu-id="62181-105">某家新創遊戲公司推出了一款新的釣魚角色扮演/策略遊戲應用程式。</span><span class="sxs-lookup"><span data-stu-id="62181-105">A gaming start-up has launched a new fishing based role-play/strategy game app.</span></span> <span data-ttu-id="62181-106">6 個月已啟動並執行 hello 遊戲。</span><span class="sxs-lookup"><span data-stu-id="62181-106">hello game has been up and running for 6 months.</span></span> <span data-ttu-id="62181-107">這個遊戲是大型成功時，它有數百萬個下載且 hello 保留是非常高的比較的 tooother 啟動遊戲應用程式。</span><span class="sxs-lookup"><span data-stu-id="62181-107">This game is a huge success, and it has millions of downloads and hello retention is very high compared tooother start-up game apps.</span></span> <span data-ttu-id="62181-108">在 hello 每季檢閱會議，專案關係人同意 tooincrease 每位使用者 (ARPU) 的平均營收。</span><span class="sxs-lookup"><span data-stu-id="62181-108">At hello quarterly review meeting, stakeholders agree they need tooincrease average revenue per user (ARPU).</span></span> <span data-ttu-id="62181-109">他們在遊戲中提供高階套件做為特殊優惠。</span><span class="sxs-lookup"><span data-stu-id="62181-109">Premium in-game packages are available as special offers.</span></span> <span data-ttu-id="62181-110">這些遊戲的組件可讓使用者 tooupgrade hello 外觀和效能其釣魚線條和 lures 或 tackles hello 遊戲中。</span><span class="sxs-lookup"><span data-stu-id="62181-110">These game packs allow users tooupgrade hello appearance and performance of their fishing lines and lures or tackles in hello game.</span></span> <span data-ttu-id="62181-111">不過，這些套件的銷售成績非常差。</span><span class="sxs-lookup"><span data-stu-id="62181-111">However, package sales are very low.</span></span> <span data-ttu-id="62181-112">因此他們決定第一個 tooanalyze hello 客戶體驗的分析工具，而且然後 toodevelop engagement 程式 tooincrease 銷售使用進階分割。</span><span class="sxs-lookup"><span data-stu-id="62181-112">So they decide first tooanalyze hello customer experience with an analytics tool, and then toodevelop an engagement program tooincrease sales using advanced segmentation.</span></span>

<span data-ttu-id="62181-113">根據 hello [Azure Mobile Engagement 入門指南最佳做法](mobile-engagement-getting-started-best-practices.md)他們建置 engagement 策略。</span><span class="sxs-lookup"><span data-stu-id="62181-113">Based on hello [Azure Mobile Engagement - Getting Started Guide with Best practices](mobile-engagement-getting-started-best-practices.md) they build an engagement strategy.</span></span>

## <a name="objectives-and-kpis"></a><span data-ttu-id="62181-114">目標和 KPI</span><span class="sxs-lookup"><span data-stu-id="62181-114">Objectives and KPIs</span></span>
<span data-ttu-id="62181-115">符合索引鍵的專案關係人 hello 遊戲。</span><span class="sxs-lookup"><span data-stu-id="62181-115">Key stakeholders for hello game meet.</span></span> <span data-ttu-id="62181-116">所有同意上一個主要目標-15%tooincrease premium 封裝銷售。</span><span class="sxs-lookup"><span data-stu-id="62181-116">All agree on one main objective - tooincrease premium package sales by 15%.</span></span> <span data-ttu-id="62181-117">他們建立商務關鍵效能指標 (Kpi) toomeasure 和磁碟機此目標</span><span class="sxs-lookup"><span data-stu-id="62181-117">They create Business Key Performance Indicators (KPIs) toomeasure and drive this objective</span></span>

* <span data-ttu-id="62181-118">這些封裝購買 hello 遊戲的層級上？</span><span class="sxs-lookup"><span data-stu-id="62181-118">On which level of hello game are these packages purchased?</span></span>
* <span data-ttu-id="62181-119">每個使用者、 每個工作階段、 每週和每個月的 hello 營收是什麼？</span><span class="sxs-lookup"><span data-stu-id="62181-119">What is hello revenue per user, per session, per week, and per month?</span></span>
* <span data-ttu-id="62181-120">Hello 最愛的採購類型為何？</span><span class="sxs-lookup"><span data-stu-id="62181-120">What are hello favorite purchase types?</span></span>

<span data-ttu-id="62181-121">第 1 部分 hello[入門指南](mobile-engagement-getting-started-best-practices.md)說明如何 toodefine hello 目標和 Kpi。</span><span class="sxs-lookup"><span data-stu-id="62181-121">Part 1 of hello [Getting Started Guide](mobile-engagement-getting-started-best-practices.md) explains how toodefine hello objectives and KPIs.</span></span> 

<span data-ttu-id="62181-122">現在已經定義了商務 Kpi hello，hello Mobile 產品 Manager 建立 Engagement Kpi toodetermine 新使用者趨勢和保留。</span><span class="sxs-lookup"><span data-stu-id="62181-122">With hello Business KPIs now defined, hello Mobile Product Manager creates Engagement KPIs toodetermine new user trends and retention.</span></span>

* <span data-ttu-id="62181-123">監視保留，並使用跨 hello 下列間隔： 每日、 每 2 天、 週、 每月和每 3 個月</span><span class="sxs-lookup"><span data-stu-id="62181-123">Monitor retention and use across hello following intervals: daily, every 2 days, weekly, monthly and every 3 months</span></span>
* <span data-ttu-id="62181-124">活躍使用者人數</span><span class="sxs-lookup"><span data-stu-id="62181-124">Active user counts</span></span>
* <span data-ttu-id="62181-125">儲存在 hello hello 應用程式分級</span><span class="sxs-lookup"><span data-stu-id="62181-125">hello app rating in hello store</span></span>

<span data-ttu-id="62181-126">根據從 hello IT 團隊的建議，下列技術 Kpi hello 已加入 tooanswer hello 下列問題：</span><span class="sxs-lookup"><span data-stu-id="62181-126">Based on recommendations from hello IT team, hello following technical KPIs were added tooanswer hello following questions:</span></span>

* <span data-ttu-id="62181-127">我的使用者路徑為何 (所瀏覽的頁面、使用者在其中所花的時間長短)</span><span class="sxs-lookup"><span data-stu-id="62181-127">What is my user path (which page is visited, how much time users spend on it)</span></span>
* <span data-ttu-id="62181-128">每個工作階段發生當機或錯誤的次數</span><span class="sxs-lookup"><span data-stu-id="62181-128">Number of crashes or bugs encountered per session</span></span>
* <span data-ttu-id="62181-129">我的使用者執行哪些作業系統版本？</span><span class="sxs-lookup"><span data-stu-id="62181-129">What OS versions are my users running?</span></span>
* <span data-ttu-id="62181-130">Hello 畫面的 我的使用者的平均大小為何？</span><span class="sxs-lookup"><span data-stu-id="62181-130">What is hello average size of screen for my users?</span></span>
* <span data-ttu-id="62181-131">我的使用者擁有哪種網際網路連線？</span><span class="sxs-lookup"><span data-stu-id="62181-131">What kind of internet connectivity do my users have?</span></span>

<span data-ttu-id="62181-132">針對每一個 KPI hello 行動產品管理員會指定需要而且會位於她腳本中的 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="62181-132">For each KPI hello Mobile Product Manager specifies hello data she needs and where it is located in her playbook.</span></span>

## <a name="engagement-program-and-integration"></a><span data-ttu-id="62181-133">業務開發計劃和整合</span><span class="sxs-lookup"><span data-stu-id="62181-133">Engagement program and integration</span></span>
<span data-ttu-id="62181-134">之前建立進階的 engagement 程式，負責 hello 專案 hello 行動專案導向器應該先深入了解如何及何時 hello 使用者所使用的產品。</span><span class="sxs-lookup"><span data-stu-id="62181-134">Before building an advanced engagement program, hello Mobile Project Director in charge of hello project should have a deep understanding of how and when products are consumed by hello users.</span></span>

<span data-ttu-id="62181-135">3 個月後 hello 行動專案導向器收集的足夠資料 tooenhance 他在應用程式的推播通知銷售。</span><span class="sxs-lookup"><span data-stu-id="62181-135">After 3 months, hello Mobile Project Director has collected enough data tooenhance his in-app push notification sales.</span></span> <span data-ttu-id="62181-136">他發現到：</span><span class="sxs-lookup"><span data-stu-id="62181-136">He learns that:</span></span>

* <span data-ttu-id="62181-137">hello 第一個訂單通常會發生在 hello 層級 14。</span><span class="sxs-lookup"><span data-stu-id="62181-137">hello first purchase generally happens at hello level 14.</span></span> <span data-ttu-id="62181-138">90%，這種情況下，針對 hello 採購是 $3 新傳奇武器。</span><span class="sxs-lookup"><span data-stu-id="62181-138">For 90% of those cases, hello purchase is new legendary weapons for $3.</span></span>
* <span data-ttu-id="62181-139">在 80%的這種情況下，使用者已購買與 hello 產品繼續並讓多個購買。</span><span class="sxs-lookup"><span data-stu-id="62181-139">In 80 % of those cases, users who have made a purchase, continue with hello product and make more purchases.</span></span>
* <span data-ttu-id="62181-140">使用者已通過 hello 層級 20，請啟動 toospend 多個 $10/週。</span><span class="sxs-lookup"><span data-stu-id="62181-140">Users who have passed hello level 20, start toospend more than $10/week.</span></span>
* <span data-ttu-id="62181-141">使用者通常 toobuy premium 封裝層級 16、 24 及 32。</span><span class="sxs-lookup"><span data-stu-id="62181-141">Users tend toobuy premium packages at level 16, 24 and 32.</span></span>

<span data-ttu-id="62181-142">謝謝 hello 行動專案導向器決定 toocreate 特定的推播通知的應用程式銷售的序列 tooincrease toothis 分析。</span><span class="sxs-lookup"><span data-stu-id="62181-142">Thanks toothis analysis hello Mobile Project Director decides toocreate specific push notification sequences tooincrease in app sales.</span></span> <span data-ttu-id="62181-143">他建立了三個他稱為「歡迎計劃」、「銷售計劃」和「無活動計劃」的推播順序。</span><span class="sxs-lookup"><span data-stu-id="62181-143">He creates three push sequences which he calls: Welcome program, Sales Program, and Inactive Program.</span></span> <span data-ttu-id="62181-144">如需詳細資訊，請參閱 toohello [Playbooks](https://github.com/Azure/azure-mobile-engagement-samples/tree/master/Playbooks)![][1]</span><span class="sxs-lookup"><span data-stu-id="62181-144">For more information refer toohello [Playbooks](https://github.com/Azure/azure-mobile-engagement-samples/tree/master/Playbooks) ![][1]</span></span>

<!--Image references-->

[1]: ./media/mobile-engagement-game-scenario/notification-scenario.png

<!--Link references-->
