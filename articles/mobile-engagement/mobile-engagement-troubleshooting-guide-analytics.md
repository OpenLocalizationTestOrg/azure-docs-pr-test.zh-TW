---
title: "Azure Mobile Engagement 疑難排解指南 - 分析"
description: "Azure Mobile Engagement 中分析、監視、分割，以及儀表板問題的疑難排解指南"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: 04a7020a-ad74-4491-be69-0bd574890029
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: e30c9ac0a8421ffcf4fc3e2548cfd7ac49701900
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting-guide-for-analytics-monitoring-segmentation-and-dashboard-issues"></a><span data-ttu-id="87c94-103">分析、監視、分割，以及儀表板問題的疑難排解指南</span><span class="sxs-lookup"><span data-stu-id="87c94-103">Troubleshooting guide for Analytics, Monitoring, Segmentation, and Dashboard issues</span></span>
<span data-ttu-id="87c94-104">以下是您可能會遇到，有關 Azure Mobile Engagement 如何收集應用程式、裝置和使用者相關資訊的問題。</span><span class="sxs-lookup"><span data-stu-id="87c94-104">The following are possible issues you may encounter with how Azure Mobile Engagement gathers information about your applications, devices, and users.</span></span>

## <a name="missingdelayed-information"></a><span data-ttu-id="87c94-105">遺漏/延遲資訊</span><span class="sxs-lookup"><span data-stu-id="87c94-105">Missing/Delayed information</span></span>
### <a name="issue"></a><span data-ttu-id="87c94-106">問題</span><span class="sxs-lookup"><span data-stu-id="87c94-106">Issue</span></span>
* <span data-ttu-id="87c94-107">資訊在分析、分割或儀表板中會延遲出現。</span><span class="sxs-lookup"><span data-stu-id="87c94-107">Information is delayed in appearing in Analytics, Segmentation, or Dashboard.</span></span>
* <span data-ttu-id="87c94-108">監視中遺漏資訊。</span><span class="sxs-lookup"><span data-stu-id="87c94-108">Information is missing from Monitoring.</span></span>
* <span data-ttu-id="87c94-109">分析、分割或儀表板中遺漏資訊。</span><span class="sxs-lookup"><span data-stu-id="87c94-109">Information is missing from Analytics, Segmentation, or Dashboard.</span></span>
* <span data-ttu-id="87c94-110">達到分割限制。</span><span class="sxs-lookup"><span data-stu-id="87c94-110">Hitting segmentation limits.</span></span>

### <a name="causes"></a><span data-ttu-id="87c94-111">原因</span><span class="sxs-lookup"><span data-stu-id="87c94-111">Causes</span></span>
* <span data-ttu-id="87c94-112">您可以使用分析 API、監視 API 與區段 API，查看是否能透過 API 看到 UI 中遺漏的任何資料。</span><span class="sxs-lookup"><span data-stu-id="87c94-112">You can use the Analytics API, Monitor API, and Segments API to see if any data you are missing from the UI is visible through the APIs.</span></span>
* <span data-ttu-id="87c94-113">如果 Azure Mobile Engagement SDK 未正確地整合到您的應用程式中，您就無法查看分析、分割、監視或儀表板中的資訊。</span><span class="sxs-lookup"><span data-stu-id="87c94-113">If the Azure Mobile Engagement SDK is not correctly integrated into your app then you won't be able to see information in the Analytics, Segmentation, Monitoring, or Dashboards.</span></span>
* <span data-ttu-id="87c94-114">區段建立之後就無法變更，只能「再製」(複製) 或「終結」(刪除) 區段。</span><span class="sxs-lookup"><span data-stu-id="87c94-114">Segments can't be changed once they are created, segments can only be "cloned" (copied) or "destroyed" (deleted).</span></span> <span data-ttu-id="87c94-115">區段只能包含 10 個準則。</span><span class="sxs-lookup"><span data-stu-id="87c94-115">Segments can only contain 10 criteria.</span></span>
* <span data-ttu-id="87c94-116">測試監視中遺漏資訊的最佳方式是安裝測試裝置、解除安裝及/或重新安裝測試裝置上的應用程式。</span><span class="sxs-lookup"><span data-stu-id="87c94-116">The best way to test missing information from monitoring is to setup a test device, uninstall and/or reinstall the app on the test device.</span></span>
* <span data-ttu-id="87c94-117">每隔 24 小時會重新整理分析、分割或儀表板的資訊。</span><span class="sxs-lookup"><span data-stu-id="87c94-117">Information is refreshed every 24 hours for Analytics, Segmentation, or Dashboards.</span></span>
* <span data-ttu-id="87c94-118">在新區段建立 24 小時之後，新區段中的資訊才會顯示，即使該區段是以先前的資訊為根據。</span><span class="sxs-lookup"><span data-stu-id="87c94-118">Information in new segments may not be displayed until 24 hours after they are created even if the segment is based on previous information.</span></span>
* <span data-ttu-id="87c94-119">在 UI 中篩選您的分析資料，無論您的應用程式版本為何，將會顯示此類型的所有範例。(例如，依名稱篩選「當機」會從您的應用程式第 1 版和第 2 版顯示)。</span><span class="sxs-lookup"><span data-stu-id="87c94-119">Filtering your analytics data in the UI will show all examples of this type regardless of the version of your app (e.g. "Crashes" filtered by name will show from version 1 and version 2 of your app).</span></span>
* <span data-ttu-id="87c94-120">分析的時間週期是以使用者裝置設定的日期為依據，因此使用者的手機日期設定如果不正確，可能會顯示錯誤的時間週期。</span><span class="sxs-lookup"><span data-stu-id="87c94-120">The time period for Analytics is based on the date from the users' device settings, so a user whose phone has the date incorrectly set could show up in the wrong time period.</span></span>
* <span data-ttu-id="87c94-121">當您使用按鈕來「測試」推送時，不會記錄任何伺服器端的資料，只會記錄實際推送活動的資料。</span><span class="sxs-lookup"><span data-stu-id="87c94-121">No server side data is logged when you use the button to "test" pushes, data is only logged for real push campaigns.</span></span>

## <a name="cant-locate-items-in-ui"></a><span data-ttu-id="87c94-122">在 UI 中找不到項目</span><span class="sxs-lookup"><span data-stu-id="87c94-122">Can't locate items in UI</span></span>
### <a name="issue"></a><span data-ttu-id="87c94-123">問題</span><span class="sxs-lookup"><span data-stu-id="87c94-123">Issue</span></span>
* <span data-ttu-id="87c94-124">無法建立以特定內建或自訂應用程式資訊標記準則為依據的區段。</span><span class="sxs-lookup"><span data-stu-id="87c94-124">Can't create segments based on certain built in or custom app info tag criteria.</span></span>
* <span data-ttu-id="87c94-125">分析、監視或儀表板中找不到特定內建或自訂應用程式資訊標記準則。</span><span class="sxs-lookup"><span data-stu-id="87c94-125">Can't find certain built in or custom app info tag criteria in Analytics, Monitoring, or Dashboards.</span></span>
* <span data-ttu-id="87c94-126">無法解譯分析、監視、分割或儀表板中的資料。</span><span class="sxs-lookup"><span data-stu-id="87c94-126">Can't interpret the data in Analytics, Monitoring, Segmentation, or Dashboards.</span></span>

### <a name="causes"></a><span data-ttu-id="87c94-127">原因</span><span class="sxs-lookup"><span data-stu-id="87c94-127">Causes</span></span>
* <span data-ttu-id="87c94-128">部分內建項目與應用程式資訊標記只能做為推送準則使用，無法新增至區段，或是顯示於分析、監視或儀表板中。</span><span class="sxs-lookup"><span data-stu-id="87c94-128">Some built in items and app info tags are only available as push criteria but may not be added to a segment or visible from Analytics, Monitoring, or Dashboard.</span></span> 
* <span data-ttu-id="87c94-129">對於無法新增至區段的內建項目與應用程式資訊標記，您必須在每個活動中設定目標準則的清單，來執行以區段為依據之目標的相同函式。</span><span class="sxs-lookup"><span data-stu-id="87c94-129">For built in items and app info tags that can't be added to a segment, you will need to setup list of targeting criteria in each campaign to perform the same function as targeting based on a segment.</span></span>
* <span data-ttu-id="87c94-130">請參閱 Azure Mobile Engagement UI 的分析、監視、分割及儀表板區段中的操作功能表，以取得更多協助與使用方式資訊。</span><span class="sxs-lookup"><span data-stu-id="87c94-130">See the context menus in the Analytics, Monitoring, Segmentation, and Dashboards sections of the Azure Mobile Engagement UI for more help and how to information.</span></span>

## <a name="crash-troubleshooting"></a><span data-ttu-id="87c94-131">當機疑難排解</span><span class="sxs-lookup"><span data-stu-id="87c94-131">Crash troubleshooting</span></span>
### <a name="issue"></a><span data-ttu-id="87c94-132">問題</span><span class="sxs-lookup"><span data-stu-id="87c94-132">Issue</span></span>
* <span data-ttu-id="87c94-133">分析、監視或儀表板中發生應用程式當機。</span><span class="sxs-lookup"><span data-stu-id="87c94-133">Application Crashes appearing in Analytics, Monitoring, or Dashboard.</span></span>

### <a name="causes"></a><span data-ttu-id="87c94-134">原因</span><span class="sxs-lookup"><span data-stu-id="87c94-134">Causes</span></span>
* <span data-ttu-id="87c94-135">如果要疑難排解分析、監視或儀表板中發生的應用程式當機，請務必查看版本資訊，了解舊版 SDK 的已知問題。</span><span class="sxs-lookup"><span data-stu-id="87c94-135">To troubleshoot Application Crashes seen in Analytics, Monitoring, or Dashboard make sure to check the release notes for known issues with previous versions of the SDK.</span></span>
* <span data-ttu-id="87c94-136">若要進一步疑難排解應用程式當機，請在已安裝您應用程式的測試裝置上執行事件，並在 Azure Mobile Engagement UI 的 [監視 – 事件] 區段中查詢您的裝置識別碼。</span><span class="sxs-lookup"><span data-stu-id="87c94-136">To further troubleshoot application crashes perform an event from a test device with your application installed and look up your device ID in the “Monitor – Events” section of the Azure Mobile Engagement UI.</span></span> <span data-ttu-id="87c94-137">然後執行造成應用程式當機的事件，並查詢 Azure Mobile Engagement UI 的 [監視 – 當機] 區段中的其他資訊。</span><span class="sxs-lookup"><span data-stu-id="87c94-137">Then perform the event that is causing your application to crash and look up additional information in the “Monitor – Crash” section of the Azure Mobile Engagement UI.</span></span> 

