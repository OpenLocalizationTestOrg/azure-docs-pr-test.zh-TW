---
title: "DevOps 適用的 Azure Application Insights 概觀 | Microsoft Docs"
description: "了解如何在 Dev Ops 環境中使用 Application Insights。"
author: CFreemanwa
services: application-insights
documentationcenter: 
manager: carmonm
ms.assetid: 6ccab5d4-34c4-4303-9d3b-a0f1b11e6651
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: bwren
ms.openlocfilehash: 4f9578fd39b80496a8de060b6cae8f5612e03aa7
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="overview-of-application-insights-for-devops"></a><span data-ttu-id="29015-103">DevOps 適用的 Application Insights 概觀</span><span class="sxs-lookup"><span data-stu-id="29015-103">Overview of Application Insights for DevOps</span></span>

<span data-ttu-id="29015-104">透過 [Application Insights](app-insights-overview.md)，您可以迅速瞭解您的應用程式在作用中時如何執行和使用。</span><span class="sxs-lookup"><span data-stu-id="29015-104">With [Application Insights](app-insights-overview.md), you can quickly find out how your app is performing and being used when it's live.</span></span> <span data-ttu-id="29015-105">如果發生問題，它可讓您了解、協助您評估影響，以及協助您判斷原因。</span><span class="sxs-lookup"><span data-stu-id="29015-105">If there's a problem, it lets you know about it, helps you assess the impact, and helps you determine the cause.</span></span>

<span data-ttu-id="29015-106">以下是某個開發 Web 應用程式的小組的敘述：</span><span class="sxs-lookup"><span data-stu-id="29015-106">Here's an account from a team that develops web applications:</span></span>

* <span data-ttu-id="29015-107">*「幾天前，我們部署了次要的 Hotfix。我們沒有執行廣泛測試階段，但很不幸地，有些未預期的變更被合併到裝載中，造成前端與後端之間的不相容。伺服器例外狀況隨即湧現，警報發出，我們便知道了這個情況。在按幾下 Application Insights 入口網站之後，我們從例外狀況堆疊取得了足夠的資訊，而得以縮小問題。我們立即復原並將損害降至最低。Application Insights 使得這個部分的開發作業週期變得非常輕鬆且可行。」*</span><span class="sxs-lookup"><span data-stu-id="29015-107">*"A couple of days ago, we deployed a 'minor' hotfix. We didn't run a broad test pass, but unfortunately some unexpected change got merged into the payload, causing incompatibility between the front and back ends. Immediately, server exceptions surged, our alert fired, and we were made aware of the situation. A few clicks away on the Application Insights portal, we got enough information from exception callstacks to narrow down the problem. We rolled back immediately and limited the damage. Application Insights has made this part of the devops cycle very easy and actionable."*</span></span>

<span data-ttu-id="29015-108">在本文中，我們追隨 Fabrikam Bank 中一個開發線上銀行系統 (OBS) 的團隊，了解他們如何使用 Application Insights 快速回應客戶和進行更新。</span><span class="sxs-lookup"><span data-stu-id="29015-108">In this article we follow a team in Fabrikam Bank that develops the online banking system (OBS) to see how they use Application Insights to quickly respond to customers and make updates.</span></span>  

<span data-ttu-id="29015-109">此團隊會處理下圖所示的 DevOps 循環：</span><span class="sxs-lookup"><span data-stu-id="29015-109">The team works on a DevOps cycle depicted in the following illustration:</span></span>

![DevOps 循環](./media/app-insights-detect-triage-diagnose/00-devcycle.png)

<span data-ttu-id="29015-111">送入其開發待處理項目 (工作清單) 的需求。</span><span class="sxs-lookup"><span data-stu-id="29015-111">Requirements feed into their development backlog (task list).</span></span> <span data-ttu-id="29015-112">小組努力工作，經常交付可行的軟體 - 通常是對現有的應用程式進行改進和延伸。</span><span class="sxs-lookup"><span data-stu-id="29015-112">They work in short sprints, which often deliver working software - usually in the form of improvements and extensions to the existing application.</span></span> <span data-ttu-id="29015-113">上線的 app 則會經常更新新功能。</span><span class="sxs-lookup"><span data-stu-id="29015-113">The live app is frequently updated with new features.</span></span> <span data-ttu-id="29015-114">雖然 app 已經上線，但小組會透過 Application Insights 的協助監視其效能和使用情況。</span><span class="sxs-lookup"><span data-stu-id="29015-114">While it's live, the team monitors it for performance and usage with the help of Application Insights.</span></span> <span data-ttu-id="29015-115">這項 APM 資料會餵送回其開發待處理項目。</span><span class="sxs-lookup"><span data-stu-id="29015-115">This APM data feeds back into their development backlog.</span></span>

<span data-ttu-id="29015-116">小組使用 Application Insights 密切監視上線 Web 應用程式的下列項目：</span><span class="sxs-lookup"><span data-stu-id="29015-116">The team uses Application Insights to monitor the live web application closely for:</span></span>

* <span data-ttu-id="29015-117">效能。</span><span class="sxs-lookup"><span data-stu-id="29015-117">Performance.</span></span> <span data-ttu-id="29015-118">他們想要了解回應時間如何隨著要求計數變化；使用多少 CPU、網路、磁碟和其他資源；以及瓶頸所在。</span><span class="sxs-lookup"><span data-stu-id="29015-118">They want to understand how response times vary with request count; how much CPU, network, disk, and other resources are being used; and where the bottlenecks are.</span></span>
* <span data-ttu-id="29015-119">失敗。</span><span class="sxs-lookup"><span data-stu-id="29015-119">Failures.</span></span> <span data-ttu-id="29015-120">如果有例外狀況或失敗的要求，或如果效能計數器超出其舒適範圍，小組必須快速知道以便採取動作。</span><span class="sxs-lookup"><span data-stu-id="29015-120">If there are exceptions or failed requests, or if a performance counter goes outside its comfortable range, the team needs to know rapidly so that they can take action.</span></span>
* <span data-ttu-id="29015-121">使用狀況。</span><span class="sxs-lookup"><span data-stu-id="29015-121">Usage.</span></span> <span data-ttu-id="29015-122">當發行新功能時，小組想要知道其使用程度，以及使用者在使用上是否有任何問題。</span><span class="sxs-lookup"><span data-stu-id="29015-122">Whenever a new feature is released, the team want to know to what extent it is used, and whether users have any difficulties with it.</span></span>

<span data-ttu-id="29015-123">接下來討論循環的回饋部分：</span><span class="sxs-lookup"><span data-stu-id="29015-123">Let's focus on the feedback part of the cycle:</span></span>

![偵測-分級-診斷](./media/app-insights-detect-triage-diagnose/01-pipe1.png)

## <a name="detect-poor-availability"></a><span data-ttu-id="29015-125">偵測可用性不佳</span><span class="sxs-lookup"><span data-stu-id="29015-125">Detect poor availability</span></span>
<span data-ttu-id="29015-126">Marcela Markova 是 OBS 小組的資深開發人員，主導線上效能監視。</span><span class="sxs-lookup"><span data-stu-id="29015-126">Marcela Markova is a senior developer on the OBS team, and takes the lead on monitoring online performance.</span></span> <span data-ttu-id="29015-127">她設定了數項[可用性測試](app-insights-monitor-web-app-availability.md)：</span><span class="sxs-lookup"><span data-stu-id="29015-127">She sets up several [availability tests](app-insights-monitor-web-app-availability.md):</span></span>

* <span data-ttu-id="29015-128">用於應用程式主要登陸頁面 (http://fabrikambank.com/onlinebanking/) 的單一 URL 測試。</span><span class="sxs-lookup"><span data-stu-id="29015-128">A single-URL test for the main landing page for the app, http://fabrikambank.com/onlinebanking/.</span></span> <span data-ttu-id="29015-129">她設定 HTTP 代碼 200 與文字「歡迎使用！」的準則。</span><span class="sxs-lookup"><span data-stu-id="29015-129">She sets criteria of HTTP code 200 and text 'Welcome!'.</span></span> <span data-ttu-id="29015-130">如果此測試失敗，表示網路或伺服器發生嚴重錯誤，或可能有部署問題。</span><span class="sxs-lookup"><span data-stu-id="29015-130">If this test fails, there's something seriously wrong with the network or the servers, or maybe a deployment issue.</span></span> <span data-ttu-id="29015-131">(或是有人變更了頁面上的「歡迎使用！」</span><span class="sxs-lookup"><span data-stu-id="29015-131">(Or someone has changed the Welcome!</span></span> <span data-ttu-id="29015-132">訊息，但沒讓她知道。)</span><span class="sxs-lookup"><span data-stu-id="29015-132">message on the page without letting her know.)</span></span>
* <span data-ttu-id="29015-133">更深入的多步驟測試將會記錄並取得目前帳戶清單，檢查每個頁面上的一些重要詳細資料。</span><span class="sxs-lookup"><span data-stu-id="29015-133">A deeper multi-step test, which logs in and gets a current account listing, checking a few key details on each page.</span></span> <span data-ttu-id="29015-134">此測試會驗證對帳戶資料庫的連結運作中。</span><span class="sxs-lookup"><span data-stu-id="29015-134">This test verifies that the link to the accounts database is working.</span></span> <span data-ttu-id="29015-135">她使用虛構的客戶識別碼：其中少數幾個保留供測試目的。</span><span class="sxs-lookup"><span data-stu-id="29015-135">She uses a fictitious customer id: a few of them are maintained for test purposes.</span></span>

<span data-ttu-id="29015-136">透過設定這些測試，Marcela 能確信若要任何中斷情況，小組將快速知道。</span><span class="sxs-lookup"><span data-stu-id="29015-136">With these tests set up, Marcela is confident that the team will quickly know about any outage.</span></span>  

<span data-ttu-id="29015-137">失敗在 Web 測試圖表上會以紅點顯示：</span><span class="sxs-lookup"><span data-stu-id="29015-137">Failures show up as red dots on the web test chart:</span></span>

![顯示對前一個期間執行的 Web 測試](./media/app-insights-detect-triage-diagnose/04-webtests.png)

<span data-ttu-id="29015-139">但更重要的是，任何失敗的相關警示會以電子郵件方式寄送給開發小組。</span><span class="sxs-lookup"><span data-stu-id="29015-139">But more importantly, an alert about any failure is emailed to the development team.</span></span> <span data-ttu-id="29015-140">以該方式，他們幾乎可在所有客戶之前便得知該情況。</span><span class="sxs-lookup"><span data-stu-id="29015-140">In that way, they know about it before nearly all the customers.</span></span>

## <a name="monitor-performance"></a><span data-ttu-id="29015-141">監視效能</span><span class="sxs-lookup"><span data-stu-id="29015-141">Monitor Performance</span></span>
<span data-ttu-id="29015-142">在 Application Insights 中的概觀頁面上，有一個顯示各種[重要度量](app-insights-web-monitor-performance.md)的圖表。</span><span class="sxs-lookup"><span data-stu-id="29015-142">On the overview page in Application Insights, there's a chart that shows a variety of [key metrics](app-insights-web-monitor-performance.md).</span></span>

![各種度量](./media/app-insights-detect-triage-diagnose/05-perfMetrics.png)

<span data-ttu-id="29015-144">瀏覽器頁面載入時間是從網頁直接傳送的遙測所衍生。</span><span class="sxs-lookup"><span data-stu-id="29015-144">Browser page load time is derived from telemetry sent directly from web pages.</span></span> <span data-ttu-id="29015-145">伺服器回應時間、伺服器要求計數和失敗的要求計數，都是在 Web 伺服器中測量，然後從該處傳送到 Application Insights。</span><span class="sxs-lookup"><span data-stu-id="29015-145">Server response time, server request count, and failed request count are all measured in the web server and sent to Application Insights from there.</span></span>

<span data-ttu-id="29015-146">Marcela 有些擔心伺服器回應圖形。</span><span class="sxs-lookup"><span data-stu-id="29015-146">Marcela is slightly concerned with the server response graph.</span></span> <span data-ttu-id="29015-147">此圖表會顯示伺服器自收到使用者瀏覽器的 HTTP 要求，直到傳回回應這段期間的平均時間。</span><span class="sxs-lookup"><span data-stu-id="29015-147">This graph shows the average time between when the server receives an HTTP request from a user's browser, and when it returns the response.</span></span> <span data-ttu-id="29015-148">在這個圖表中看到差異並無不尋常，因為各系統的負載不同。</span><span class="sxs-lookup"><span data-stu-id="29015-148">It isn't unusual to see a variation in this chart, as load on the system varies.</span></span> <span data-ttu-id="29015-149">但在此情況下，要求數量些微增加與回應時間大幅增加似乎有某種關係。</span><span class="sxs-lookup"><span data-stu-id="29015-149">But in this case, there seems to be a correlation between small rises in the count of requests, and big rises in the response time.</span></span> <span data-ttu-id="29015-150">這可能表示系統到達運作極限。</span><span class="sxs-lookup"><span data-stu-id="29015-150">That could indicate that the system is operating just at its limits.</span></span>

<span data-ttu-id="29015-151">她將「伺服器」圖表打開：</span><span class="sxs-lookup"><span data-stu-id="29015-151">She opens the Servers charts:</span></span>

![各種度量](./media/app-insights-detect-triage-diagnose/06.png)

<span data-ttu-id="29015-153">其中似乎沒有資源限制的徵兆，也許伺服器回應圖表中的起伏只是巧合。</span><span class="sxs-lookup"><span data-stu-id="29015-153">There seems to be no sign of resource limitation there, so maybe the bumps in the server response charts are just a coincidence.</span></span>

## <a name="set-alerts-to-meet-goals"></a><span data-ttu-id="29015-154">設定警示以符合目標</span><span class="sxs-lookup"><span data-stu-id="29015-154">Set alerts to meet goals</span></span>
<span data-ttu-id="29015-155">儘管如此，她還是會多加留意回應時間。</span><span class="sxs-lookup"><span data-stu-id="29015-155">Nevertheless, she'd like to keep an eye on the response times.</span></span> <span data-ttu-id="29015-156">如果它們變得太高，她想立即知道。</span><span class="sxs-lookup"><span data-stu-id="29015-156">If they go too high, she wants to know about it immediately.</span></span>

<span data-ttu-id="29015-157">因此，她針對回應時間大於一般臨界值的情況設定了一個[警示](app-insights-metrics-explorer.md)。</span><span class="sxs-lookup"><span data-stu-id="29015-157">So she sets an [alert](app-insights-metrics-explorer.md), for response times greater than a typical threshold.</span></span> <span data-ttu-id="29015-158">這可以確保當回應時間變慢時她就會知道。</span><span class="sxs-lookup"><span data-stu-id="29015-158">This gives her confidence that she'll know about it if response times are slow.</span></span>

![加入警示分頁](./media/app-insights-detect-triage-diagnose/07-alerts.png)

<span data-ttu-id="29015-160">您可以在其他各種不同的度量上設定警示。</span><span class="sxs-lookup"><span data-stu-id="29015-160">Alerts can be set on a wide variety of other metrics.</span></span> <span data-ttu-id="29015-161">例如，您可以在例外狀況計數變高或可用記憶體變低，或用戶端要求中有尖峰時收到電子郵件。</span><span class="sxs-lookup"><span data-stu-id="29015-161">For example, you can receive emails if the exception count becomes high, or the available memory goes low, or if there is a peak in client requests.</span></span>

## <a name="stay-informed-with-smart-detection-alerts"></a><span data-ttu-id="29015-162">獲得有關智慧型偵測警示的資訊</span><span class="sxs-lookup"><span data-stu-id="29015-162">Stay informed with Smart Detection Alerts</span></span>
<span data-ttu-id="29015-163">隔天，確實收到了一封來自 Application Insights 的電子郵件。</span><span class="sxs-lookup"><span data-stu-id="29015-163">Next day, an alert email does arrive from Application Insights.</span></span> <span data-ttu-id="29015-164">但是開啟郵件之後，她發現並不是她所設定的回應時間警示。</span><span class="sxs-lookup"><span data-stu-id="29015-164">But when she opens it, she finds it isn't the response time alert that she set.</span></span> <span data-ttu-id="29015-165">而是郵件告知她失敗的要求 (也就是傳回 500 或更高數字之失敗代碼的要求) 數目突然提高。</span><span class="sxs-lookup"><span data-stu-id="29015-165">Instead, it tells her there's been a sudden rise in failed requests - that is, requests that have returned failure codes of 500 or more.</span></span>

<span data-ttu-id="29015-166">發生失敗的要求時使用者會看到錯誤，通常是在程式碼中擲出例外狀況之後。</span><span class="sxs-lookup"><span data-stu-id="29015-166">Failed requests are where users have seen an error - typically following an exception thrown in the code.</span></span> <span data-ttu-id="29015-167">也許他們會看到訊息指出 「抱歉，我們現在無法更新您的詳細資料。 」</span><span class="sxs-lookup"><span data-stu-id="29015-167">Maybe they see a message saying "Sorry we couldn't update your details right now."</span></span> <span data-ttu-id="29015-168">或者，極度尷尬的是，使用者的螢幕上會顯示堆疊傾印 (出自於 Web 伺服器禮貌回應)。</span><span class="sxs-lookup"><span data-stu-id="29015-168">Or, at absolute embarrassing worst, a stack dump appears on the user's screen, courtesy of the web server.</span></span>

<span data-ttu-id="29015-169">這個警示令人驚訝，因為她上次查看時，失敗的要求計數很低，完全不用擔心。</span><span class="sxs-lookup"><span data-stu-id="29015-169">This alert is a surprise, because the last time she looked at it, the failed request count was encouragingly low.</span></span> <span data-ttu-id="29015-170">其中一小部分的失敗預期是在忙碌的伺服器中。</span><span class="sxs-lookup"><span data-stu-id="29015-170">A small number of failures is to be expected in a busy server.</span></span>

<span data-ttu-id="29015-171">這也讓她稍微感到驚訝，因為她之前並不需要設定這個警示。</span><span class="sxs-lookup"><span data-stu-id="29015-171">It was also a bit of a surprise for her because she didn't have to configure this alert.</span></span> <span data-ttu-id="29015-172">Application Insights 包含智慧型偵測。</span><span class="sxs-lookup"><span data-stu-id="29015-172">Application Insights include Smart Detection.</span></span> <span data-ttu-id="29015-173">它會自動調整至您 app 的一般失敗模式，並且「習慣」特定頁面、高負載或和其他計量連結的失敗。</span><span class="sxs-lookup"><span data-stu-id="29015-173">It automatically adjusts to your app's usual failure pattern, and "gets used to" failures on a particular page, or under high load, or linked to other metrics.</span></span> <span data-ttu-id="29015-174">只有當增加量超出預期的量時它才會發出警示。</span><span class="sxs-lookup"><span data-stu-id="29015-174">It raises the alarm only if there's a rise above what it comes to expect.</span></span>

![主動診斷電子郵件](./media/app-insights-detect-triage-diagnose/21.png)

<span data-ttu-id="29015-176">這封電子郵件非常有幫助。</span><span class="sxs-lookup"><span data-stu-id="29015-176">This is a very useful email.</span></span> <span data-ttu-id="29015-177">它不只是發出警示。</span><span class="sxs-lookup"><span data-stu-id="29015-177">It doesn't just raise an alarm.</span></span> <span data-ttu-id="29015-178">它也會進行許多分級和診斷工作。</span><span class="sxs-lookup"><span data-stu-id="29015-178">It does a lot of the triage and diagnostic work, too.</span></span>

<span data-ttu-id="29015-179">它會顯示有多少客戶，以及哪些網頁或作業受到影響。</span><span class="sxs-lookup"><span data-stu-id="29015-179">It shows how many customers are affected, and which web pages or operations.</span></span> <span data-ttu-id="29015-180">Marcela 可以決定是否需要動員整個小組來處理此問題，或者可以延後到下週再處理。</span><span class="sxs-lookup"><span data-stu-id="29015-180">Marcela can decide whether she needs to get the whole team working on this as a fire drill, or whether it can be ignored until next week.</span></span>

<span data-ttu-id="29015-181">該電子郵件也顯示發生的特定例外狀況，甚至 - 更有趣的 - 是與對特定資料庫呼叫失敗關聯的失敗。</span><span class="sxs-lookup"><span data-stu-id="29015-181">The email also shows that a particular exception occurred, and - even more interesting - that the failure is associated with failed calls to a particular database.</span></span> <span data-ttu-id="29015-182">這解釋了為何 Marcela 的團隊即使最近沒有部署任何更新也會突然發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="29015-182">This explains why the fault suddenly appeared even though Marcela's team has not deployed any updates recently.</span></span>

<span data-ttu-id="29015-183">Marcella 會根據這封電子郵件偵測資料庫團隊的主管。</span><span class="sxs-lookup"><span data-stu-id="29015-183">Marcella pings the leader of the database team based on this email.</span></span> <span data-ttu-id="29015-184">她發現他們在過去半小時釋出了 Hot Fix；而不巧的是，或許是基礎結構有些微小變更...</span><span class="sxs-lookup"><span data-stu-id="29015-184">She learns that they released a hot fix in the past half hour; and Oops, maybe there might have been a minor schema change....</span></span>

<span data-ttu-id="29015-185">因此，在問題發生後的 15 分鐘內，甚至是在檢查紀錄之前，就已經開始修正問題。</span><span class="sxs-lookup"><span data-stu-id="29015-185">So the problem is on the way to being fixed, even before investigating logs, and within 15 minutes of it arising.</span></span> <span data-ttu-id="29015-186">不過，Marcela 按了一下連結來開啟 Application Insights。</span><span class="sxs-lookup"><span data-stu-id="29015-186">However, Marcela clicks the link to open Application Insights.</span></span> <span data-ttu-id="29015-187">此時直接開啟了一個失敗的要求，而且她可以在相依性呼叫的關聯清單中看到失敗的資料庫呼叫。</span><span class="sxs-lookup"><span data-stu-id="29015-187">It opens straight onto a failed request, and she can see the failed database call in the associated list of dependency calls.</span></span>

![失敗的要求](./media/app-insights-detect-triage-diagnose/23.png)

## <a name="detect-exceptions"></a><span data-ttu-id="29015-189">偵測例外狀況</span><span class="sxs-lookup"><span data-stu-id="29015-189">Detect exceptions</span></span>
<span data-ttu-id="29015-190">只要一點點設定，就可以將 [例外狀況](app-insights-asp-net-exceptions.md) 自動報告給 Application Insights。</span><span class="sxs-lookup"><span data-stu-id="29015-190">With a little bit of setup, [exceptions](app-insights-asp-net-exceptions.md) are reported to Application Insights automatically.</span></span> <span data-ttu-id="29015-191">也可以在程式碼中呼叫 [TrackException()](app-insights-api-custom-events-metrics.md#trackexception) ，明確擷取這些例外狀況：</span><span class="sxs-lookup"><span data-stu-id="29015-191">They can also be captured explicitly by inserting calls to [TrackException()](app-insights-api-custom-events-metrics.md#trackexception) into the code:</span></span>  

    var telemetry = new TelemetryClient();
    ...
    try
    { ...
    }
    catch (Exception ex)
    {
       // Set up some properties:
       var properties = new Dictionary <string, string>
         {{"Game", currentGame.Name}};

       var measurements = new Dictionary <string, double>
         {{"Users", currentGame.Users.Count}};

       // Send the exception telemetry:
       telemetry.TrackException(ex, properties, measurements);
    }


<span data-ttu-id="29015-192">Fabrikam 銀行小組制定出一律在發生例外狀況時傳送遙測的作法，除非有明顯的恢復。</span><span class="sxs-lookup"><span data-stu-id="29015-192">The Fabrikam Bank team has evolved the practice of always sending telemetry on an exception, unless there's an obvious recovery.</span></span>  

<span data-ttu-id="29015-193">事實上，其策略甚至比此更為廣泛：他們會在每個客戶對要做的事感到挫折時便傳送遙測，而不論是否與程式碼中的例外狀況對應。</span><span class="sxs-lookup"><span data-stu-id="29015-193">In fact, their strategy is even broader than that: They send telemetry in every case where the customer is frustrated in what they wanted to do, whether it corresponds to an exception in the code or not.</span></span> <span data-ttu-id="29015-194">例如，如果外部的銀行內傳送系統因為某此作業原因 (不是客戶的錯誤) 而傳回「無法完成此交易」訊息，他們會追蹤該事件。</span><span class="sxs-lookup"><span data-stu-id="29015-194">For example, if the external inter-bank transfer system returns a "can't complete this transaction" message for some operational reason (no fault of the customer) then they track that event.</span></span>

    var successCode = AttemptTransfer(transferAmount, ...);
    if (successCode < 0)
    {
       var properties = new Dictionary <string, string>
            {{ "Code", returnCode, ... }};
       var measurements = new Dictionary <string, double>
         {{"Value", transferAmount}};
       telemetry.TrackEvent("transfer failed", properties, measurements);
    }

<span data-ttu-id="29015-195">TrackException 用來報告例外狀況，因為它會傳送堆疊的副本。</span><span class="sxs-lookup"><span data-stu-id="29015-195">TrackException is used to report exceptions because it sends a copy of the stack.</span></span> <span data-ttu-id="29015-196">TrackEvent 用來報告其他事件。</span><span class="sxs-lookup"><span data-stu-id="29015-196">TrackEvent is used to report other events.</span></span> <span data-ttu-id="29015-197">您可以在診斷中附加可能有幫助的任何屬性。</span><span class="sxs-lookup"><span data-stu-id="29015-197">You can attach any properties that might be useful in diagnosis.</span></span>

<span data-ttu-id="29015-198">例外狀況和事件會顯示在 [[診斷搜尋](app-insights-diagnostic-search.md)] 刀鋒視窗中。</span><span class="sxs-lookup"><span data-stu-id="29015-198">Exceptions and events show up in the [Diagnostic Search](app-insights-diagnostic-search.md) blade.</span></span> <span data-ttu-id="29015-199">您可以深入探索，以查看額外屬性和堆疊追蹤。</span><span class="sxs-lookup"><span data-stu-id="29015-199">You can drill into them to see the additional properties and stack trace.</span></span>

![在「診斷搜尋」中，請使用篩選器來顯示特定類型的資料](./media/app-insights-detect-triage-diagnose/appinsights-333facets.png)


## <a name="monitor-proactively"></a><span data-ttu-id="29015-201">主動監視</span><span class="sxs-lookup"><span data-stu-id="29015-201">Monitor proactively</span></span>
<span data-ttu-id="29015-202">Marcela 不會無所事事等候警示。</span><span class="sxs-lookup"><span data-stu-id="29015-202">Marcela doesn't just sit around waiting for alerts.</span></span> <span data-ttu-id="29015-203">在每次重新部署之後，她都會立即查看[回應時間](app-insights-web-monitor-performance.md) - 除了例外狀況計數之外，也查看整體數據和最緩慢的要求表。</span><span class="sxs-lookup"><span data-stu-id="29015-203">Soon after every redeployment, she takes a look at [response times](app-insights-web-monitor-performance.md) - both the overall figure and the table of slowest requests, as well as exception counts.</span></span>  

![回應時間圖及伺服器回應時間格線。](./media/app-insights-detect-triage-diagnose/09-dependencies.png)

<span data-ttu-id="29015-205">她可以評估每個部署的效能影響，通常是將每週與前一週比較。</span><span class="sxs-lookup"><span data-stu-id="29015-205">She can assess the performance effect of every deployment, typically comparing each week with the last.</span></span> <span data-ttu-id="29015-206">如果突然有變慢的情況，她會將該情況向相關的開發人員反應。</span><span class="sxs-lookup"><span data-stu-id="29015-206">If there's a sudden worsening, she raises that with the relevant developers.</span></span>

## <a name="triage-issues"></a><span data-ttu-id="29015-207">分級問題</span><span class="sxs-lookup"><span data-stu-id="29015-207">Triage issues</span></span>
<span data-ttu-id="29015-208">分級 - 評估問題的嚴重性和程度 - 是偵測後的第一個步驟。</span><span class="sxs-lookup"><span data-stu-id="29015-208">Triage - assessing the severity and extent of a problem - is the first step after detection.</span></span> <span data-ttu-id="29015-209">我們是否應該在半夜打電話給小組？</span><span class="sxs-lookup"><span data-stu-id="29015-209">Should we call out the team at midnight?</span></span> <span data-ttu-id="29015-210">或是問題可以留到累積的工作中下一次方便的時候？</span><span class="sxs-lookup"><span data-stu-id="29015-210">Or can it be left until the next convenient gap in the backlog?</span></span> <span data-ttu-id="29015-211">分級時有一些重要的問題。</span><span class="sxs-lookup"><span data-stu-id="29015-211">There are some key questions in triage.</span></span>

<span data-ttu-id="29015-212">發生頻率為何？</span><span class="sxs-lookup"><span data-stu-id="29015-212">How often is it happening?</span></span> <span data-ttu-id="29015-213">[概觀] 分頁的圖表可提供問題的某些觀點。</span><span class="sxs-lookup"><span data-stu-id="29015-213">The charts on the Overview blade give some perspective to a problem.</span></span> <span data-ttu-id="29015-214">例如，Fabrikam 應用程式在一個晚上產生了四個 Web 測試警示。</span><span class="sxs-lookup"><span data-stu-id="29015-214">For example, the Fabrikam application generated four web test alerts one night.</span></span> <span data-ttu-id="29015-215">小組在早上查看圖表，可以發現確實出現一些紅點，但多數的測試仍是綠色。</span><span class="sxs-lookup"><span data-stu-id="29015-215">Looking at the chart in the morning, the team could see that there were indeed some red dots, though still most of the tests were green.</span></span> <span data-ttu-id="29015-216">深入探索可用性圖表，很明顯地，這所有的間歇性問題都來自一個測試位置。</span><span class="sxs-lookup"><span data-stu-id="29015-216">Drilling into the availability chart, it was clear that all of these intermittent problems were from one test location.</span></span> <span data-ttu-id="29015-217">這顯然是僅影響一個路徑的網路問題，而且很可能可自行解決。</span><span class="sxs-lookup"><span data-stu-id="29015-217">This was obviously a network issue affecting only one route, and would most likely clear itself.</span></span>  

<span data-ttu-id="29015-218">相反地，例外狀況計數或回應時間圖表中明顯且穩定的上升則明顯有其他問題需要注意。</span><span class="sxs-lookup"><span data-stu-id="29015-218">By contrast, a dramatic and stable rise in the graph of exception counts or response times is obviously something to panic about.</span></span>

<span data-ttu-id="29015-219">實用的分級策略是「自己動手做」。</span><span class="sxs-lookup"><span data-stu-id="29015-219">A useful triage tactic is Try It Yourself.</span></span> <span data-ttu-id="29015-220">如果您遇到相同問題，就會知道它是真的。</span><span class="sxs-lookup"><span data-stu-id="29015-220">If you run into the same problem, you know it's real.</span></span>

<span data-ttu-id="29015-221">哪個部分的使用者受到影響？</span><span class="sxs-lookup"><span data-stu-id="29015-221">What fraction of users are affected?</span></span> <span data-ttu-id="29015-222">若要獲得約略的答案，請將失敗率除以工作階段計數。</span><span class="sxs-lookup"><span data-stu-id="29015-222">To obtain a rough answer, divide the failure rate by the session count.</span></span>

![失敗的要求和工作階段的圖表](./media/app-insights-detect-triage-diagnose/10-failureRate.png)

<span data-ttu-id="29015-224">在緩慢回應的情況中，將回應最緩慢的要求表與每個頁面的使用頻率相比較。</span><span class="sxs-lookup"><span data-stu-id="29015-224">When there are slow responses, compare the table of slowest-responding requests with the usage frequency of each page.</span></span>

<span data-ttu-id="29015-225">封鎖案例的重要性如何？</span><span class="sxs-lookup"><span data-stu-id="29015-225">How important is the blocked scenario?</span></span> <span data-ttu-id="29015-226">如果這是功能性問題，封鎖了特定的使用者劇本，有很大影響嗎？</span><span class="sxs-lookup"><span data-stu-id="29015-226">If this is a functional problem blocking a particular user story, does it matter much?</span></span> <span data-ttu-id="29015-227">如果客戶無法支付帳單，便很嚴重；如果客戶無法變更其畫面色彩喜好設定，也可以稍候再解決。</span><span class="sxs-lookup"><span data-stu-id="29015-227">If customers can't pay their bills, this is serious; if they can't change their screen color preferences, maybe it can wait.</span></span> <span data-ttu-id="29015-228">事件或例外狀況的詳細資料或緩慢頁面的身分識別，會告知您客戶發生問題的位置。</span><span class="sxs-lookup"><span data-stu-id="29015-228">The detail of the event or exception, or the identity of the slow page, tells you where customers are having trouble.</span></span>

## <a name="diagnose-issues"></a><span data-ttu-id="29015-229">診斷問題</span><span class="sxs-lookup"><span data-stu-id="29015-229">Diagnose issues</span></span>
<span data-ttu-id="29015-230">診斷與偵測不太一樣。</span><span class="sxs-lookup"><span data-stu-id="29015-230">Diagnosis isn't quite the same as debugging.</span></span> <span data-ttu-id="29015-231">開始追蹤程式碼之前，您應該對問題的原因、位置和發生時機有約略的構念。</span><span class="sxs-lookup"><span data-stu-id="29015-231">Before you start tracing through the code, you should have a rough idea of why, where and when the issue is occurring.</span></span>

<span data-ttu-id="29015-232">**發生時機為何？**</span><span class="sxs-lookup"><span data-stu-id="29015-232">**When does it happen?**</span></span> <span data-ttu-id="29015-233">事件和度量圖表提供的歷程檢視可讓您輕鬆將影響與可能原因產生相互關聯。</span><span class="sxs-lookup"><span data-stu-id="29015-233">The historical view provided by the event and metric charts makes it easy to correlate effects with possible causes.</span></span> <span data-ttu-id="29015-234">如果回應時間或例外狀況率中有間歇性的尖峰，請查看要求計數：如果尖峰是在相同時間，則可能是資源問題。</span><span class="sxs-lookup"><span data-stu-id="29015-234">If there are intermittent peaks in response time or exception rates, look at the request count: if it peaks at the same time, then it looks like a resource problem.</span></span> <span data-ttu-id="29015-235">您需要指派更多 CPU 或記憶體嗎？</span><span class="sxs-lookup"><span data-stu-id="29015-235">Do you need to assign more CPU or memory?</span></span> <span data-ttu-id="29015-236">或者它是無法管理負載的相依性？</span><span class="sxs-lookup"><span data-stu-id="29015-236">Or is it a dependency that can't manage the load?</span></span>

<span data-ttu-id="29015-237">**問題在於我們嗎？**</span><span class="sxs-lookup"><span data-stu-id="29015-237">**Is it us?**</span></span>  <span data-ttu-id="29015-238">如果特定類型的要求效能突然下降 - 例如客戶想要對帳單時 - 則可能是外部子系統而非 Web 應用程式有問題。</span><span class="sxs-lookup"><span data-stu-id="29015-238">If you have a sudden drop in performance of a particular type of request - for example when the customer wants an account statement - then there's a possibility it might be an external subsystem rather than your web application.</span></span> <span data-ttu-id="29015-239">在「計量瀏覽器」中，選取相依性失敗率和相依性期間率，並將其過去幾個小時或幾天的歷程記錄與您偵測到的問題比較。</span><span class="sxs-lookup"><span data-stu-id="29015-239">In Metrics Explorer, select the Dependency Failure rate and Dependency Duration rates and compare their histories over the past few hours or days with the problem you detected.</span></span> <span data-ttu-id="29015-240">如果有相互關聯的變更，則外部子系統可能是原因所在。</span><span class="sxs-lookup"><span data-stu-id="29015-240">If there are correlating changes, then an external subsystem might be to blame.</span></span>  

![相依性失敗和對相依性呼叫期間的圖表](./media/app-insights-detect-triage-diagnose/11-dependencies.png)

<span data-ttu-id="29015-242">有些緩慢相依性的問題是地理位置問題。</span><span class="sxs-lookup"><span data-stu-id="29015-242">Some slow dependency issues are geolocation problems.</span></span> <span data-ttu-id="29015-243">Fabrikam 銀行使用 Azure virtual 機器，並發現他們誤將 Web 伺服器和帳戶伺服器放置在不同國家/地區。</span><span class="sxs-lookup"><span data-stu-id="29015-243">Fabrikam Bank uses Azure virtual machines, and discovered that they had inadvertently located their web server and account server in different countries.</span></span> <span data-ttu-id="29015-244">透過移轉其中一部伺服器獲得明顯的改善。</span><span class="sxs-lookup"><span data-stu-id="29015-244">A dramatic improvement was brought about by migrating one of them.</span></span>

<span data-ttu-id="29015-245">**我們做了什麼？**</span><span class="sxs-lookup"><span data-stu-id="29015-245">**What did we do?**</span></span> <span data-ttu-id="29015-246">如果問題似乎不在於相依性，而且如果不是持續有問題，則可能是由於最近的變更而導致。</span><span class="sxs-lookup"><span data-stu-id="29015-246">If the issue doesn't appear to be in a dependency, and if it wasn't always there, it's probably caused by a recent change.</span></span> <span data-ttu-id="29015-247">度量和事件圖表提供的歷史觀點讓您輕鬆將任何突然的變更與部署產生相互關聯。</span><span class="sxs-lookup"><span data-stu-id="29015-247">The historical perspective provided by the metric and event charts makes it easy to correlate any sudden changes with deployments.</span></span> <span data-ttu-id="29015-248">它可縮小問題的搜尋範圍。</span><span class="sxs-lookup"><span data-stu-id="29015-248">That narrows down the search for the problem.</span></span>

<span data-ttu-id="29015-249">**發生什麼？**</span><span class="sxs-lookup"><span data-stu-id="29015-249">**What's going on?**</span></span> <span data-ttu-id="29015-250">有些問題很少發生，而且透過離線測試可能難以追蹤。</span><span class="sxs-lookup"><span data-stu-id="29015-250">Some problems occur only rarely and can be difficult to track down by testing offline.</span></span> <span data-ttu-id="29015-251">我們能做的是嘗試在問題發生時擷取錯誤。</span><span class="sxs-lookup"><span data-stu-id="29015-251">All we can do is to try to capture the bug when it occurs live.</span></span> <span data-ttu-id="29015-252">您可以在例外狀況報告中檢查堆疊傾印。</span><span class="sxs-lookup"><span data-stu-id="29015-252">You can inspect the stack dumps in exception reports.</span></span> <span data-ttu-id="29015-253">此外，您可以使用喜好的記錄架構或使用 TrackTrace() 或 TrackEvent() 來編寫追蹤呼叫。</span><span class="sxs-lookup"><span data-stu-id="29015-253">In addition, you can write tracing calls, either with your favorite logging framework or with TrackTrace() or TrackEvent().</span></span>  

<span data-ttu-id="29015-254">Fabrikam 的帳戶間轉送發生間歇性問題，但只有某些帳戶類型有此情況。</span><span class="sxs-lookup"><span data-stu-id="29015-254">Fabrikam had an intermittent problem with inter-account transfers, but only with certain account types.</span></span> <span data-ttu-id="29015-255">為了更加了解發生的情況，他們在程式碼中的重要點插入了 TrackTrace() 呼叫，附加帳戶類型作為每個呼叫的內容。</span><span class="sxs-lookup"><span data-stu-id="29015-255">To understand better what was happening, they inserted TrackTrace() calls at key points in the code, attaching the account type as a property to each call.</span></span> <span data-ttu-id="29015-256">那使得要在診斷搜尋中僅篩選掉這些追蹤更為輕鬆。</span><span class="sxs-lookup"><span data-stu-id="29015-256">That made it easy to filter out just those traces in Diagnostic Search.</span></span> <span data-ttu-id="29015-257">他們也將參數值附加為追蹤呼叫的屬性和測量。</span><span class="sxs-lookup"><span data-stu-id="29015-257">They also attached parameter values as properties and measures to the trace calls.</span></span>

## <a name="respond-to-discovered-issues"></a><span data-ttu-id="29015-258">回應所發現的問題</span><span class="sxs-lookup"><span data-stu-id="29015-258">Respond to discovered issues</span></span>
<span data-ttu-id="29015-259">診斷問題之後，您可以製訂修正問題的計劃。</span><span class="sxs-lookup"><span data-stu-id="29015-259">Once you've diagnosed the issue, you can make a plan to fix it.</span></span> <span data-ttu-id="29015-260">也許您需要復原最近的變更，或也許您可以繼續並修正它。</span><span class="sxs-lookup"><span data-stu-id="29015-260">Maybe you need to roll back a recent change, or maybe you can just go ahead and fix it.</span></span> <span data-ttu-id="29015-261">修正完成後，Application Insights 會告知您是否成功。</span><span class="sxs-lookup"><span data-stu-id="29015-261">Once the fix is done, Application Insights tells you whether you succeeded.</span></span>  

<span data-ttu-id="29015-262">Fabrikam 銀行的開發小組對效能測量採取較使用 Application Insights 之前更具結構的方法。</span><span class="sxs-lookup"><span data-stu-id="29015-262">Fabrikam Bank's development team take a more structured approach to performance measurement than they used to before they used Application Insights.</span></span>

* <span data-ttu-id="29015-263">他們會在 Application Insights 概觀頁面就特定度量設定效能目標。</span><span class="sxs-lookup"><span data-stu-id="29015-263">They set performance targets in terms of specific measures in the Application Insights overview page.</span></span>
* <span data-ttu-id="29015-264">他們從頭為應用程式設計效能度量，例如透過「漏斗」測量使用者進度的度量。</span><span class="sxs-lookup"><span data-stu-id="29015-264">They design performance measures into the application from the start, such as the metrics that measure user progress through 'funnels.'</span></span>  


## <a name="monitor-user-activity"></a><span data-ttu-id="29015-265">監視使用者活動</span><span class="sxs-lookup"><span data-stu-id="29015-265">Monitor user activity</span></span>
<span data-ttu-id="29015-266">當回應時間一直都不錯，而且例外狀況不多時，開發小組可以繼續往可用性的方向努力。</span><span class="sxs-lookup"><span data-stu-id="29015-266">When response time is consistently good and there are few exceptions, the dev team can move on to usability.</span></span> <span data-ttu-id="29015-267">他們可以思考如何改善使用者體驗，以及如何鼓勵更多使用者達到想要的目標。</span><span class="sxs-lookup"><span data-stu-id="29015-267">They can think about how to improve the users' experience, and how to encourage more users to achieve the desired goals.</span></span>

<span data-ttu-id="29015-268">Application Insights 也可以用來了解使用者在應用程式內執行的動作。</span><span class="sxs-lookup"><span data-stu-id="29015-268">Application Insights can also be used to learn what users do with an app.</span></span> <span data-ttu-id="29015-269">執行順暢時，小組會想要得知哪些功能最受歡迎、使用者喜歡或感到有困難的部份，以及使用者回來的頻率。</span><span class="sxs-lookup"><span data-stu-id="29015-269">Once it's running smoothly, the team would like to know which features are the most popular, what users like or have difficulty with, and how often they come back.</span></span> <span data-ttu-id="29015-270">這些資訊有助於將他們近期的工作排定優先順序。</span><span class="sxs-lookup"><span data-stu-id="29015-270">That will help them prioritize their upcoming work.</span></span> <span data-ttu-id="29015-271">而他們可以計劃測量每個功能的成功度，作為開發週期的一部份。</span><span class="sxs-lookup"><span data-stu-id="29015-271">And they can plan to measure the success of each feature as part of the development cycle.</span></span> 

<span data-ttu-id="29015-272">例如，使用者在網站上的典型使用者旅程是明確的「漏斗圖」。</span><span class="sxs-lookup"><span data-stu-id="29015-272">For example, a typical user journey through the web site has a clear "funnel."</span></span> <span data-ttu-id="29015-273">許多客戶會研究不同類型的貸款利率。</span><span class="sxs-lookup"><span data-stu-id="29015-273">Many customers look at the rates of different types of loan.</span></span> <span data-ttu-id="29015-274">少部分的客戶會繼續填寫報價單。</span><span class="sxs-lookup"><span data-stu-id="29015-274">A smaller number go on to fill in the quotation form.</span></span> <span data-ttu-id="29015-275">在取得報價單的客戶當中，有一部分會繼續，並取得貸款。</span><span class="sxs-lookup"><span data-stu-id="29015-275">Of those who get a quotation, a few go ahead and take out the loan.</span></span>

![頁面檢視計數](./media/app-insights-detect-triage-diagnose/12-funnel.png)

<span data-ttu-id="29015-277">透過找出最多客戶放棄的位置，企業可以思考如何讓更多使用者通過漏斗。</span><span class="sxs-lookup"><span data-stu-id="29015-277">By considering where the greatest numbers of customers drop out, the business can work out how to get more users through to the bottom of the funnel.</span></span> <span data-ttu-id="29015-278">在某些情況下，可能是使用者體驗 (UX) 失敗 - 例如，很難找到 [下一步] 按鈕，或者指示不太明顯。</span><span class="sxs-lookup"><span data-stu-id="29015-278">In some cases, there might be a user experience (UX) failure - for example, the 'next' button is hard to find, or the instructions aren't obvious.</span></span> <span data-ttu-id="29015-279">更有可能是因為重要的商業理由放棄：可能是貸款利率太高。</span><span class="sxs-lookup"><span data-stu-id="29015-279">More likely, there are more significant business reasons for drop-outs: maybe the loan rates are too high.</span></span>

<span data-ttu-id="29015-280">無論任何原因，資料都可協助團隊了解使用者在做什麼。</span><span class="sxs-lookup"><span data-stu-id="29015-280">Whatever the reasons, the data helps the team work out what users are doing.</span></span> <span data-ttu-id="29015-281">此時可以插入更多追蹤呼叫，了解更多細節。</span><span class="sxs-lookup"><span data-stu-id="29015-281">More tracking calls can be inserted to work out more detail.</span></span> <span data-ttu-id="29015-282">TrackEvent() 可以用來計算任何使用者動作，小至個別的按鈕點擊，大到如付清貸款等重要成果。</span><span class="sxs-lookup"><span data-stu-id="29015-282">TrackEvent() can be used to count any user actions, from the fine detail of individual button clicks, to significant achievements such as paying off a loan.</span></span>

<span data-ttu-id="29015-283">團隊一直都有使用者活動的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="29015-283">The team is getting used to having information about user activity.</span></span> <span data-ttu-id="29015-284">只是現在，每當設計出一個新功能時，就要思考如何取得其使用方式的意見反應。</span><span class="sxs-lookup"><span data-stu-id="29015-284">Nowadays, whenever they design a new feature, they work out how they will get feedback about its usage.</span></span> <span data-ttu-id="29015-285">團隊如果從一開始就在功能中設計追蹤呼叫，</span><span class="sxs-lookup"><span data-stu-id="29015-285">They design tracking calls into the feature from the start.</span></span> <span data-ttu-id="29015-286">就可以使用意見反應在每個開發週期中改進功能。</span><span class="sxs-lookup"><span data-stu-id="29015-286">They use the feedback to improve the feature in each development cycle.</span></span>

<span data-ttu-id="29015-287">[深入了解如何追蹤使用量](app-insights-usage-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="29015-287">[Read more about tracking usage](app-insights-usage-overview.md).</span></span>

## <a name="apply-the-devops-cycle"></a><span data-ttu-id="29015-288">套用 DevOps 週期</span><span class="sxs-lookup"><span data-stu-id="29015-288">Apply the DevOps cycle</span></span>
<span data-ttu-id="29015-289">以上就是一個小組如何使用 Application Insights 來不只是修正個別問題，還改善其開發週期的情況。</span><span class="sxs-lookup"><span data-stu-id="29015-289">So that's how one team use Application Insights not just to fix individual issues, but to improve their development lifecycle.</span></span> <span data-ttu-id="29015-290">希望這已提供您一些概念，讓您了解 Application Insights 如何協助您在自己的應用程式中進行應用程式效能管理。</span><span class="sxs-lookup"><span data-stu-id="29015-290">I hope it has given you some ideas about how Application Insights can help you with application performance management in your own applications.</span></span>

## <a name="video"></a><span data-ttu-id="29015-291">影片</span><span class="sxs-lookup"><span data-stu-id="29015-291">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="next-steps"></a><span data-ttu-id="29015-292">後續步驟</span><span class="sxs-lookup"><span data-stu-id="29015-292">Next steps</span></span>
<span data-ttu-id="29015-293">視您的應用程式特性而定，您可以從數種方式著手。</span><span class="sxs-lookup"><span data-stu-id="29015-293">You can get started in several ways, depending on the characteristics of your application.</span></span> <span data-ttu-id="29015-294">請挑選最適合您的方式：</span><span class="sxs-lookup"><span data-stu-id="29015-294">Pick what suits you best:</span></span>

* [<span data-ttu-id="29015-295">ASP.NET Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="29015-295">ASP.NET web application</span></span>](app-insights-asp-net.md)
* [<span data-ttu-id="29015-296">Java Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="29015-296">Java web application</span></span>](app-insights-java-get-started.md)
* [<span data-ttu-id="29015-297">Node.js Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="29015-297">Node.js web application</span></span>](app-insights-nodejs.md)
* <span data-ttu-id="29015-298">裝載於 [IIS](app-insights-monitor-web-app-availability.md)、[J2EE](app-insights-java-live.md) 或 [Azure](app-insights-azure.md) 上的已部署應用程式。</span><span class="sxs-lookup"><span data-stu-id="29015-298">Already deployed apps, hosted on [IIS](app-insights-monitor-web-app-availability.md), [J2EE](app-insights-java-live.md), or [Azure](app-insights-azure.md).</span></span>
* <span data-ttu-id="29015-299">[網頁](app-insights-javascript.md) - 單頁應用程式或一般網頁 - 單獨使用此選項或作為任何伺服器選項以外的附加選項。</span><span class="sxs-lookup"><span data-stu-id="29015-299">[Web pages](app-insights-javascript.md) - Single Page App or ordinary web page - use this on its own or in addition to any of the server options.</span></span>
* <span data-ttu-id="29015-300">可從公用網際網路測試您應用程式的[可用性測試](app-insights-monitor-web-app-availability.md)。</span><span class="sxs-lookup"><span data-stu-id="29015-300">[Availability tests](app-insights-monitor-web-app-availability.md) to test your app from the public internet.</span></span>
