---
title: "Azure Mobile Engagement 使用者介面 - 分析"
description: "了解如何使用 Azure Mobile Engagement 分析應用程式的歷史資料"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: 6b2533ac-b8ec-4e35-872c-d563895bdc0c
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: ad05676919d6c254d60fd010c3f589f663c4745d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-analyze-historical-data-about-your-application"></a><span data-ttu-id="5e895-103">如何分析應用程式的歷史資料</span><span class="sxs-lookup"><span data-stu-id="5e895-103">How to analyze historical data about your application</span></span>
<span data-ttu-id="5e895-104">本文說明 **Mobile Engagement** 入口網站的**分析**。</span><span class="sxs-lookup"><span data-stu-id="5e895-104">This article describes the **ANALYTICS** tab of the **Mobile Engagement** portal.</span></span> <span data-ttu-id="5e895-105">使用 **Mobile Engagement** 入口網站可監視與管理您的行動應用程式。</span><span class="sxs-lookup"><span data-stu-id="5e895-105">You use the **Mobile Engagement** portal to monitor and manage your mobile apps.</span></span> <span data-ttu-id="5e895-106">請注意，若要開始使用入口網站，您必須先建立 **Azure Mobile Engagement** 帳戶。</span><span class="sxs-lookup"><span data-stu-id="5e895-106">Note that to start using the portal you first need to create an **Azure Mobile Engagement** account.</span></span>

<span data-ttu-id="5e895-107">UI 的 [分析] 區段根據每 24 小時更新一次的歷史資料，提供您應用程式的相關彙總資訊。</span><span class="sxs-lookup"><span data-stu-id="5e895-107">The Analytics section of the UI provides aggregated information about your application based on historic data that is updated every 24 hours.</span></span> <span data-ttu-id="5e895-108">這些資訊會顯示在由折線圖/橫條圖/圓餅圖、方格和地圖所組成的各種儀表板上。</span><span class="sxs-lookup"><span data-stu-id="5e895-108">The information is displayed on different dashboards composed of line/bar/pie charts, grids, and maps.</span></span> <span data-ttu-id="5e895-109">您也可以將資料下載為 .csv 檔案。</span><span class="sxs-lookup"><span data-stu-id="5e895-109">The data can also be downloaded as .csv files.</span></span> <span data-ttu-id="5e895-110">這些相同資訊大部分可從 UI 的 [監視] 區段即時取得，也可以從「分析 API」存取。</span><span class="sxs-lookup"><span data-stu-id="5e895-110">Most of this same information is available in real time in the Monitor section of the UI, and it can also be accessed from the Analytics API.</span></span>

> [!NOTE]
> <span data-ttu-id="5e895-111">許多 **Mobile Engagement** 入口網站 UI 的區段含有 [顯示說明] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="5e895-111">Many sections of the **Mobile Engagement** portal UI contain the **SHOW HELP** button.</span></span> <span data-ttu-id="5e895-112">按該按鈕，可獲得關於區段的詳細內容資訊。</span><span class="sxs-lookup"><span data-stu-id="5e895-112">Press this button to get more contextual information about a section.</span></span>

## <a name="standard-and-custom-analytics"></a><span data-ttu-id="5e895-113">標準和自訂分析</span><span class="sxs-lookup"><span data-stu-id="5e895-113">Standard and Custom Analytics</span></span>
<span data-ttu-id="5e895-114">您只要將應用程式與 SDK 整合，Azure Mobile Engagement 就可針對您的應用程式提供一組基本、標準的可圖形化分析資訊。</span><span class="sxs-lookup"><span data-stu-id="5e895-114">Azure Mobile Engagement provides a set of basic, standard analytic information about your applications that can be graphed as soon as you integrate your app with the SDK.</span></span> <span data-ttu-id="5e895-115">Azure Mobile Engagement 也能讓您收集有關使用者行為的其他自訂分析資訊。</span><span class="sxs-lookup"><span data-stu-id="5e895-115">Azure Mobile Engagement also provides the ability to gather additional custom analytics information that you want about your end-users' behavior.</span></span> <span data-ttu-id="5e895-116">您可以從 [設定]  建立一個自訂「標記 (應用程式資訊)」的標記計畫，Azure Mobile Engagement 就可以為您收集這類額外資料。</span><span class="sxs-lookup"><span data-stu-id="5e895-116">You can do this by creating a tag plan of custom "Tags (app info)", created from **Settings** so that Azure Mobile Engagement can collect this additional data for you.</span></span>

## <a name="analytics"></a><span data-ttu-id="5e895-117">Analytics</span><span class="sxs-lookup"><span data-stu-id="5e895-117">Analytics</span></span>
* <span data-ttu-id="5e895-118">儀表板：顯示有關新使用者和作用中使用者及其趨勢的一般資訊。</span><span class="sxs-lookup"><span data-stu-id="5e895-118">Dashboard: Shows general information about your new and actives users and their trends.</span></span>
* <span data-ttu-id="5e895-119">使用者：會依據其裝置識別碼來識別使用者：每個裝置的識別碼都是唯一的 (一位新使用者實際上是一個新裝置)。</span><span class="sxs-lookup"><span data-stu-id="5e895-119">Users: Users are identified by their device identifier: this identifier is unique for each device (one new user is actually one new device).</span></span> <span data-ttu-id="5e895-120">如果一位使用者在某個指定時間間隔內執行了第一個工作階段，就會在此時間間隔期間被視為新使用者。</span><span class="sxs-lookup"><span data-stu-id="5e895-120">A user is considered as new on a given time interval if he has performed his first session during this time interval.</span></span> <span data-ttu-id="5e895-121">如果一位使用者在過去 7 天內至少執行了一個工作階段，則會被視為保留使用者。</span><span class="sxs-lookup"><span data-stu-id="5e895-121">A user is considered as retained if he has performed at least one session during the last 7 days.</span></span> <span data-ttu-id="5e895-122">「作用中使用者」是在指定期間內至少建立了一個工作階段的使用者。</span><span class="sxs-lookup"><span data-stu-id="5e895-122">Active Users are users that made at least one session during a given period.</span></span> <span data-ttu-id="5e895-123">您可以依據每個月、每週、每天或每小時的期間加以排序。</span><span class="sxs-lookup"><span data-stu-id="5e895-123">You can sort by, monthly, weekly, daily, or hourly time periods.</span></span> <span data-ttu-id="5e895-124">所有圖表的外觀都很類似，但可讓您依據不同的功能 (例如您的應用程式版本) 進行篩選，然後依據一段時間排序。</span><span class="sxs-lookup"><span data-stu-id="5e895-124">All of the charts look similar but allow you to filter by different features, such as the version of your application, and then to sort by a period of time.</span></span> <span data-ttu-id="5e895-125">整合 SDK 時所蒐集到的標準資訊包括：作用中使用者、新使用者、工作階段數目、每個工作階段長度、國家 (地區) 的技術資訊、地區設定、位置、語言、電信業者、裝置、韌體、網路 (WIFI)、客戶使用的應用程式和 SDK 版本。</span><span class="sxs-lookup"><span data-stu-id="5e895-125">The standard information gathered by integrating the SDK includes the following: Active users, new user, number of sessions, length of each session, technical information about the country, locals, location, language carrier, devices, firmware, network (WIFI), versions of the app and SDK, used by customers.</span></span> <span data-ttu-id="5e895-126">這項資訊可以從 [監視] 區段即時檢視。</span><span class="sxs-lookup"><span data-stu-id="5e895-126">This information can be viewed in real time from the monitor section.</span></span>

> [!NOTE]
> <span data-ttu-id="5e895-127">時間間隔是根據使用者裝置設定的日期，所以如果使用者的電話設定的日期不正確，使用者可能會出現在錯誤的時間間隔。</span><span class="sxs-lookup"><span data-stu-id="5e895-127">The time period is based on the date from the users' device settings, so a user whose phone has the date incorrectly set could show up in the wrong time period.</span></span>

* <span data-ttu-id="5e895-128">保留：如果一位使用者在某個指定時間間隔內執行了第一個工作階段，就會在此時間間隔期間被視為保留使用者。</span><span class="sxs-lookup"><span data-stu-id="5e895-128">Retention: A user is considered as retained on a given time interval if he has performed his first session during this time interval.</span></span> <span data-ttu-id="5e895-129">您可以將保留使用者 (和新使用者) 的時間間隔計算變更為時數、天數、週數或月數。</span><span class="sxs-lookup"><span data-stu-id="5e895-129">You can change the time intervals during which retained users (and new users) are counted to hours, days, weeks, or months.</span></span> <span data-ttu-id="5e895-130">使用者保留分析會以同群使用者為基礎。</span><span class="sxs-lookup"><span data-stu-id="5e895-130">The user retention analytics is built on top of cohorts.</span></span> <span data-ttu-id="5e895-131">「同群使用者」是在指定期間內偵測到的所有新使用者集合 (亦即在此期間執行他們第一個工作階段的使用者集合)。</span><span class="sxs-lookup"><span data-stu-id="5e895-131">A cohort is the set of all the new users detected for a given period (i.e., the set of users performing their first session during this period).</span></span> <span data-ttu-id="5e895-132">我們使用 1 天、2 天、4 天、7 天或 1 個月的同群使用者。</span><span class="sxs-lookup"><span data-stu-id="5e895-132">We use cohorts of 1-day, 2-day, 4-day, 7-day, or 1-month.</span></span> <span data-ttu-id="5e895-133">指定每隔 1 天、2 天，4 天、7 天或 1 個月的同群使用者，Azure Mobile Engagement 會計算屬於該同群使用者且仍然作用中的所有使用者集合 (亦即，在期間內至少執行一個工作階段的使用者集合)。</span><span class="sxs-lookup"><span data-stu-id="5e895-133">Given a cohort, every 1-day, 2-day, 4-day, 7-day, or 1-month, Azure Mobile Engagement computes the set of all users who belong to the cohort and are still active (i.e., the set of users who performed at least one session during the period).</span></span> <span data-ttu-id="5e895-134">此類使用者集合稱為同群使用者版本</span><span class="sxs-lookup"><span data-stu-id="5e895-134">This set of users is called a cohort version.</span></span> <span data-ttu-id="5e895-135">(Azure Mobile Engagement 會向您顯示有多少使用者仍在使用您的應用程式，但是只有特定平台市集，例如 GooglePlay、iTunes、Windows 市集等，才能告訴您有多少使用者解除安裝您的應用程式)。</span><span class="sxs-lookup"><span data-stu-id="5e895-135">(Azure Mobile Engagement can show you how many of your users are still using your app, but only the platform specific store can tell you how many of your users uninstalled your app - for example, GooglePlay, iTunes, Windows Store, etc.).</span></span>
* <span data-ttu-id="5e895-136">工作階段：由一位使用者使用一個應用程式。</span><span class="sxs-lookup"><span data-stu-id="5e895-136">Sessions: One use of the application by a user.</span></span> <span data-ttu-id="5e895-137">工作階段是從使用者執行的活動序列所產生 (一個活動通常使用一個應用程式畫面，但這會根據 SDK 整合至應用程式的方式而有所不同)。</span><span class="sxs-lookup"><span data-stu-id="5e895-137">Sessions are generated from the sequence of activities performed by users (an activity is usually associated to the usage of one screen of the application, but this can vary depending on the way the SDK has been integrated in the application).</span></span> <span data-ttu-id="5e895-138">使用者一次只能執行一個活動：當使用者開始他的第一個活動時，工作階段就開始，當他完成他的最後一個活動時，工作階段就停止。</span><span class="sxs-lookup"><span data-stu-id="5e895-138">A user can only perform one activity at a time: a session starts as soon as the user starts his first activity and stops when he finishes his last activity.</span></span> <span data-ttu-id="5e895-139">如果使用者停留超過幾秒鐘的時間而沒有執行任何活動，他的活動序列會分成兩個不同的工作階段。</span><span class="sxs-lookup"><span data-stu-id="5e895-139">If a user stays more than a few seconds without performing any activity, then his sequence of activities is split into two distinct sessions.</span></span>
* <span data-ttu-id="5e895-140">活動：應用程式中的每個畫面名稱，以及使用者在每個畫面所花費的時間。</span><span class="sxs-lookup"><span data-stu-id="5e895-140">Activities: The names of each screen in your application and the length of time users spend on each screen.</span></span> <span data-ttu-id="5e895-141">活動是一種自訂的分析選項，會對應到您為自己的應用程式所設定的「應用程式資訊」標記：</span><span class="sxs-lookup"><span data-stu-id="5e895-141">Activities are a custom analytic option that will correspond to the "app info" tags you have set up for your own app:</span></span>
* <span data-ttu-id="5e895-142">使用者路徑：顯示使用者如何瀏覽您的應用程式活動 (畫面)。</span><span class="sxs-lookup"><span data-stu-id="5e895-142">User Path:  Shows how your users navigate through your application's activities (screens).</span></span> <span data-ttu-id="5e895-143">您可以移動滑桿調整詳細資料的層級。</span><span class="sxs-lookup"><span data-stu-id="5e895-143">You can move the slider to adjust the level of details.</span></span> <span data-ttu-id="5e895-144">藍色的節點代表您的應用程式活動。</span><span class="sxs-lookup"><span data-stu-id="5e895-144">Blue nodes represent your application's activities.</span></span> <span data-ttu-id="5e895-145">節點大小和使用者花費在節點的時間呈正比。</span><span class="sxs-lookup"><span data-stu-id="5e895-145">Their size is proportional to the time users spent in it.</span></span> <span data-ttu-id="5e895-146">白色的節點代表工作階段開始和停止。</span><span class="sxs-lookup"><span data-stu-id="5e895-146">White nodes represent session start and stop.</span></span> <span data-ttu-id="5e895-147">紅色的節點代表當機。</span><span class="sxs-lookup"><span data-stu-id="5e895-147">Red nodes represent crashes.</span></span> <span data-ttu-id="5e895-148">連結代表在應用程式活動之間 (或活動和當機之間) 轉換。</span><span class="sxs-lookup"><span data-stu-id="5e895-148">Links represent transitions between your application's activities (or between activities and crashes).</span></span> <span data-ttu-id="5e895-149">按一下節點或連結可顯示工具提示，其中包含資料的詳細資訊：在特定畫面中所花費的時間、轉換計數，以及從來源活動轉換為目的地活動的百分比</span><span class="sxs-lookup"><span data-stu-id="5e895-149">Click on a node or a link to display a tooltip with more information about your data: the time spent in a particular screen, the count of transitions, and the percentage of transitions from the source activity to the destination activity.</span></span> <span data-ttu-id="5e895-150">(A ---60% ---> B 表示在活動 A 的使用者移至活動 B 花費 60% 的時間)。如果想要更仔細研究，可以重新安排圖表；每次您進行變更時，都會儲存圖表的位置。</span><span class="sxs-lookup"><span data-stu-id="5e895-150">(A ---60% ---> B means that users being on activity A goes to activity B 60% of the time.) You can reorganize the graph as you want to clarify it; its position is saved every time you make a change.</span></span> <span data-ttu-id="5e895-151">您可以顯示或隱藏當機，來加強圖表。</span><span class="sxs-lookup"><span data-stu-id="5e895-151">You can show or hide the crashes to lighten the graph.</span></span>
* <span data-ttu-id="5e895-152">事件：使用者在應用程式中所採取的特定動作。</span><span class="sxs-lookup"><span data-stu-id="5e895-152">Events: Specific actions taken by a user in the application.</span></span> <span data-ttu-id="5e895-153">事件的分佈會以每個工作階段每位使用者的事件計數顯示。</span><span class="sxs-lookup"><span data-stu-id="5e895-153">The distribution of events is shown as the count of events per user per session.</span></span> <span data-ttu-id="5e895-154">一個事件表示一個立即動作，例如按一下按鈕或接收通知</span><span class="sxs-lookup"><span data-stu-id="5e895-154">An event represents an instant action, for example, a click on a button or the reception of a notification.</span></span> <span data-ttu-id="5e895-155">(事件的意義取決於 SDK 與應用程式整合的方式)。事件可能在工作階段或作業期間發生，也可以獨立存在。</span><span class="sxs-lookup"><span data-stu-id="5e895-155">(The meaning of events depends on how the SDK has been integrated in the application.) An event can occur during a session or a job or can be stand alone.</span></span>
* <span data-ttu-id="5e895-156">工作：與事件類似，只不過工作的重點在於動作的長度。</span><span class="sxs-lookup"><span data-stu-id="5e895-156">Jobs: Similar to events except they focus on the length of the action.</span></span> <span data-ttu-id="5e895-157">例如，工作可以告訴您載入內容或呼叫 Web 服務要花費多長時間的相關技術資訊。</span><span class="sxs-lookup"><span data-stu-id="5e895-157">For example, Jobs could tell you technical information about how long it takes content to load or a call to web service.</span></span> <span data-ttu-id="5e895-158">工作也可以顯示使用者填寫表單、建立帳戶或購買東西時所花費的時間。</span><span class="sxs-lookup"><span data-stu-id="5e895-158">It could also show how long it takes a user to fill out a form, create an account, or make a purchase.</span></span> <span data-ttu-id="5e895-159">工作代表某項工作的持續時間，例如，下載工作的持續時間或橫幅顯示在畫面上的時間</span><span class="sxs-lookup"><span data-stu-id="5e895-159">A job represents the duration of a task, for example, the duration of a download task or the time a banner is displayed on the screen.</span></span> <span data-ttu-id="5e895-160">(工作的意義取決於 SDK 與應用程式整合的方式)。工作通常與工作階段範圍之外所執行的背景工作相關 (亦即，不含任何使用者活動)。</span><span class="sxs-lookup"><span data-stu-id="5e895-160">(The meaning of Jobs depends on how the SDK has been integrated in the application.) Jobs are usually associated with background tasks that are performed outside of the scope of a session (i.e., without any user activity).</span></span>
* <span data-ttu-id="5e895-161">技術：您可以追蹤應用程式中有關使用者裝置的技術資訊，例如地區設定、電信業者、網路、裝置、韌體、使用者裝置的螢幕大小，以及您的應用程式版本和應用程式中使用的 SDK 版本。</span><span class="sxs-lookup"><span data-stu-id="5e895-161">Technicals: Technical information about the devices of the users of your app that you can track, such as the Locale, Carrier, Network, Device, Firmware, and Screen size of the users' devices, and the Version of your App and the SDK version used in your app.</span></span>
* <span data-ttu-id="5e895-162">錯誤：位於應用程式內部，且不會造成應用程式當機的技術錯誤相關資訊。</span><span class="sxs-lookup"><span data-stu-id="5e895-162">Errors: Information about technical errors inside the application that do not cause the application to crash.</span></span> <span data-ttu-id="5e895-163">錯誤表示立即的問題，例如網路錯誤或不正確的操作</span><span class="sxs-lookup"><span data-stu-id="5e895-163">An error represents an instant issue, for example, a network failure or a bad manipulation.</span></span> <span data-ttu-id="5e895-164">(事件的意義取決於 SDK 與應用程式整合的方式)。錯誤可能在工作階段或工作期間發生，也可以獨立存在。</span><span class="sxs-lookup"><span data-stu-id="5e895-164">(The meaning of events depends on how the SDK has been integrated in the application.) An error can occur during a session or a job or can be stand alone.</span></span>
* <span data-ttu-id="5e895-165">當機：造成應用程式當機的錯誤相關資訊。</span><span class="sxs-lookup"><span data-stu-id="5e895-165">Crashes: Information about errors that cause your application to crash.</span></span> <span data-ttu-id="5e895-166">當機是應用程式停止執行其預期的功能，且必須停止的非預期狀況。</span><span class="sxs-lookup"><span data-stu-id="5e895-166">A crash is an unexpected condition where the application stops performing its expected functions and must be stopped.</span></span> <span data-ttu-id="5e895-167">當機通常是應用程式中的錯誤 (bug) 所造成。</span><span class="sxs-lookup"><span data-stu-id="5e895-167">A crash is usually due to a bug in the application.</span></span>

![Analytics2][11]

## <a name="accessing-the-retention-overview"></a><span data-ttu-id="5e895-169">存取保留概觀</span><span class="sxs-lookup"><span data-stu-id="5e895-169">Accessing the Retention Overview</span></span>
![Analytics3][12]

<span data-ttu-id="5e895-171">保留概觀會在中間分成幾張卡片，每一張顯示特定保留期間的概觀。</span><span class="sxs-lookup"><span data-stu-id="5e895-171">The retention overview is broken down in the middle into several cards, each showing the overview for a certain retention period.</span></span> <span data-ttu-id="5e895-172">範例顯示的是為期 2 天的保留期間。</span><span class="sxs-lookup"><span data-stu-id="5e895-172">The 2-day retention period is seen in the example.</span></span> <span data-ttu-id="5e895-173">其他卡片則顯示 4 天和 7 天的保留期間。</span><span class="sxs-lookup"><span data-stu-id="5e895-173">The other cards show the 4-day and 7-day retention periods.</span></span>

## <a name="understanding-the-retention-overview-cards"></a><span data-ttu-id="5e895-174">了解保留概觀卡片</span><span class="sxs-lookup"><span data-stu-id="5e895-174">Understanding the Retention Overview cards</span></span>
![Analytics4][13]

### <a name="each-card-is-composed-of-3-main-parts"></a><span data-ttu-id="5e895-176">每張卡片由 3 個主要部分組成：</span><span class="sxs-lookup"><span data-stu-id="5e895-176">Each card is composed of 3 main parts:</span></span>
1. <span data-ttu-id="5e895-177">1：同群使用者和考慮的期間</span><span class="sxs-lookup"><span data-stu-id="5e895-177">1: The cohort and the period considered</span></span>
2. <span data-ttu-id="5e895-178">2-4：目前期間的保留</span><span class="sxs-lookup"><span data-stu-id="5e895-178">2-4: The retention for the current period</span></span>
3. <span data-ttu-id="5e895-179">5：歷程記錄的走勢圖</span><span class="sxs-lookup"><span data-stu-id="5e895-179">5: A Sparkline of the history</span></span>

### <a name="here-is-detailed-information-about-each-element"></a><span data-ttu-id="5e895-180">以下是每個項目的詳細資訊：</span><span class="sxs-lookup"><span data-stu-id="5e895-180">Here is detailed information about each element:</span></span>
1. <span data-ttu-id="5e895-181">同群使用者和期間：此標題提供同群使用者的類型。</span><span class="sxs-lookup"><span data-stu-id="5e895-181">Cohort and period: This headline gives the type of cohort.</span></span> <span data-ttu-id="5e895-182">此處的「2 天期間」表示我們要查看這 2 天的使用者行為、到達超過 2 天期間的使用者數目，以及使用者在接下來的 2 天是否連線。</span><span class="sxs-lookup"><span data-stu-id="5e895-182">Here "2-day period" means that we will look at the behavior of users over 2 days, Users that arrived over a period of 2 days, and whether they connect in the following blocks of 2 days.</span></span> <span data-ttu-id="5e895-183">上述範例考慮 11 月 21 日和 22 日之間的使用者活動。</span><span class="sxs-lookup"><span data-stu-id="5e895-183">The example above considers the activity of users between the 21st and 22nd of November.</span></span>
2. <span data-ttu-id="5e895-184">此處提供 11 月 19 日和 20 日到達的使用者到 11 月 21 日和 22 日的保留率。</span><span class="sxs-lookup"><span data-stu-id="5e895-184">This gives the retention rate over the 21 and 22 of November for the users arriving in 19 and 20 of November.</span></span> <span data-ttu-id="5e895-185">我們在 21 日和 22 日之間有 1 位作用中使用者，在 19 日和 20 日之間有 3 位新使用者。</span><span class="sxs-lookup"><span data-stu-id="5e895-185">Here we had 1 active user between the 21st and 22nd, over the 3 that were new users between the 19th and 20th.</span></span>
3. <span data-ttu-id="5e895-186">此視覺化指標提供的資訊與上面的圖表相同</span><span class="sxs-lookup"><span data-stu-id="5e895-186">This visual indicator gives the same information as above represented graphically.</span></span> <span data-ttu-id="5e895-187">(1/3 的圓形來自 33% 的數字)。色彩可提供其他資訊：綠色表示此數字與之前的計算值相比是增加的。</span><span class="sxs-lookup"><span data-stu-id="5e895-187">(The third of the circle is from the 33% number.) The color gives additional information: Green indicates this number is growing from the previous calculation.</span></span> <span data-ttu-id="5e895-188">黃色表示穩定，紅色表示減少。</span><span class="sxs-lookup"><span data-stu-id="5e895-188">Yellow means stable, and red means decreasing.</span></span>
4. <span data-ttu-id="5e895-189">這表示用來計算的值。</span><span class="sxs-lookup"><span data-stu-id="5e895-189">This indicates the values used for the calculation.</span></span>
5. <span data-ttu-id="5e895-190">這是保留值的歷程記錄走勢圖。</span><span class="sxs-lookup"><span data-stu-id="5e895-190">This is a Sparkline of the history of the retention values.</span></span> <span data-ttu-id="5e895-191">它可讓您查看過去的值，充分了解這些數值演進的方式。</span><span class="sxs-lookup"><span data-stu-id="5e895-191">It allows you to see the values in the past to have a broad view of how it evolved.</span></span>

## <a name="see-also"></a><span data-ttu-id="5e895-192">另請參閱</span><span class="sxs-lookup"><span data-stu-id="5e895-192">See also</span></span>
* <span data-ttu-id="5e895-193">[概念][Link 6]</span><span class="sxs-lookup"><span data-stu-id="5e895-193">[Concepts][Link 6]</span></span>
* <span data-ttu-id="5e895-194">[疑難排解指南服務][Link 24]</span><span class="sxs-lookup"><span data-stu-id="5e895-194">[Troubleshooting Guide Service][Link 24]</span></span>

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
