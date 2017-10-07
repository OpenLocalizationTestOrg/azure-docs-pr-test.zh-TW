---
title: "aaaAzure Mobile Engagement 疑難排解指南-分析"
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
ms.openlocfilehash: 69c6ff8f5c8540f8ba8b85b9ffec55acc59329fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-guide-for-analytics-monitoring-segmentation-and-dashboard-issues"></a><span data-ttu-id="62821-103">分析、監視、分割，以及儀表板問題的疑難排解指南</span><span class="sxs-lookup"><span data-stu-id="62821-103">Troubleshooting guide for Analytics, Monitoring, Segmentation, and Dashboard issues</span></span>
<span data-ttu-id="62821-104">hello 以下是可能的問題可能會遇到與 Azure Mobile Engagement 收集您的應用程式、 裝置和使用者的相關資訊的方式。</span><span class="sxs-lookup"><span data-stu-id="62821-104">hello following are possible issues you may encounter with how Azure Mobile Engagement gathers information about your applications, devices, and users.</span></span>

## <a name="missingdelayed-information"></a><span data-ttu-id="62821-105">遺漏/延遲資訊</span><span class="sxs-lookup"><span data-stu-id="62821-105">Missing/Delayed information</span></span>
### <a name="issue"></a><span data-ttu-id="62821-106">問題</span><span class="sxs-lookup"><span data-stu-id="62821-106">Issue</span></span>
* <span data-ttu-id="62821-107">資訊在分析、分割或儀表板中會延遲出現。</span><span class="sxs-lookup"><span data-stu-id="62821-107">Information is delayed in appearing in Analytics, Segmentation, or Dashboard.</span></span>
* <span data-ttu-id="62821-108">監視中遺漏資訊。</span><span class="sxs-lookup"><span data-stu-id="62821-108">Information is missing from Monitoring.</span></span>
* <span data-ttu-id="62821-109">分析、分割或儀表板中遺漏資訊。</span><span class="sxs-lookup"><span data-stu-id="62821-109">Information is missing from Analytics, Segmentation, or Dashboard.</span></span>
* <span data-ttu-id="62821-110">達到分割限制。</span><span class="sxs-lookup"><span data-stu-id="62821-110">Hitting segmentation limits.</span></span>

### <a name="causes"></a><span data-ttu-id="62821-111">原因</span><span class="sxs-lookup"><span data-stu-id="62821-111">Causes</span></span>
* <span data-ttu-id="62821-112">您可以使用 hello 分析 API，監視應用程式開發介面，和區段 API toosee，如果您是從 hello UI 遺失任何資料會顯示透過 hello 應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="62821-112">You can use hello Analytics API, Monitor API, and Segments API toosee if any data you are missing from hello UI is visible through hello APIs.</span></span>
* <span data-ttu-id="62821-113">如果 hello Azure Mobile Engagement SDK 未正確地整合到應用程式，您不是能 toosee hello 分析、 分割、 監視中] 或儀表板中的資訊。</span><span class="sxs-lookup"><span data-stu-id="62821-113">If hello Azure Mobile Engagement SDK is not correctly integrated into your app then you won't be able toosee information in hello Analytics, Segmentation, Monitoring, or Dashboards.</span></span>
* <span data-ttu-id="62821-114">區段建立之後就無法變更，只能「再製」(複製) 或「終結」(刪除) 區段。</span><span class="sxs-lookup"><span data-stu-id="62821-114">Segments can't be changed once they are created, segments can only be "cloned" (copied) or "destroyed" (deleted).</span></span> <span data-ttu-id="62821-115">區段只能包含 10 個準則。</span><span class="sxs-lookup"><span data-stu-id="62821-115">Segments can only contain 10 criteria.</span></span>
* <span data-ttu-id="62821-116">hello 遺失的監視資訊最佳方式 tootest 是 toosetup 測試裝置、 解除安裝和/或 hello 測試裝置上重新安裝 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="62821-116">hello best way tootest missing information from monitoring is toosetup a test device, uninstall and/or reinstall hello app on hello test device.</span></span>
* <span data-ttu-id="62821-117">每隔 24 小時會重新整理分析、分割或儀表板的資訊。</span><span class="sxs-lookup"><span data-stu-id="62821-117">Information is refreshed every 24 hours for Analytics, Segmentation, or Dashboards.</span></span>
* <span data-ttu-id="62821-118">等到 24 小時，即使 hello 區段根據先前的資訊建立之後，可能不會顯示新的區段中的資訊。</span><span class="sxs-lookup"><span data-stu-id="62821-118">Information in new segments may not be displayed until 24 hours after they are created even if hello segment is based on previous information.</span></span>
* <span data-ttu-id="62821-119">篩選 hello UI 中的分析資料會顯示所有的範例，這種應用程式的 hello 版本不限 （例如依名稱篩選「當機」會從您的應用程式第 1 版和第 2 版顯示)。</span><span class="sxs-lookup"><span data-stu-id="62821-119">Filtering your analytics data in hello UI will show all examples of this type regardless of hello version of your app (e.g. "Crashes" filtered by name will show from version 1 and version 2 of your app).</span></span>
* <span data-ttu-id="62821-120">hello 期間分析的日期為基礎 hello hello 使用者的裝置設定，讓的使用者的電話已設定不正確的 hello 日期無法顯示在 hello 錯誤時間週期。</span><span class="sxs-lookup"><span data-stu-id="62821-120">hello time period for Analytics is based on hello date from hello users' device settings, so a user whose phone has hello date incorrectly set could show up in hello wrong time period.</span></span>
* <span data-ttu-id="62821-121">當您使用 hello 按鈕時，會記錄資料的任何伺服器端太"test"推播通知，針對實際的推送活動只會記錄資料。</span><span class="sxs-lookup"><span data-stu-id="62821-121">No server side data is logged when you use hello button too"test" pushes, data is only logged for real push campaigns.</span></span>

## <a name="cant-locate-items-in-ui"></a><span data-ttu-id="62821-122">在 UI 中找不到項目</span><span class="sxs-lookup"><span data-stu-id="62821-122">Can't locate items in UI</span></span>
### <a name="issue"></a><span data-ttu-id="62821-123">問題</span><span class="sxs-lookup"><span data-stu-id="62821-123">Issue</span></span>
* <span data-ttu-id="62821-124">無法建立以特定內建或自訂應用程式資訊標記準則為依據的區段。</span><span class="sxs-lookup"><span data-stu-id="62821-124">Can't create segments based on certain built in or custom app info tag criteria.</span></span>
* <span data-ttu-id="62821-125">分析、監視或儀表板中找不到特定內建或自訂應用程式資訊標記準則。</span><span class="sxs-lookup"><span data-stu-id="62821-125">Can't find certain built in or custom app info tag criteria in Analytics, Monitoring, or Dashboards.</span></span>
* <span data-ttu-id="62821-126">無法解譯分析、 監視、 分割或儀表板中的 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="62821-126">Can't interpret hello data in Analytics, Monitoring, Segmentation, or Dashboards.</span></span>

### <a name="causes"></a><span data-ttu-id="62821-127">原因</span><span class="sxs-lookup"><span data-stu-id="62821-127">Causes</span></span>
* <span data-ttu-id="62821-128">某些內建的項目和應用程式資訊只可用為推入準則標記，但可能不會新增 tooa 區段或看到從分析、 監視中] 或儀表板。</span><span class="sxs-lookup"><span data-stu-id="62821-128">Some built in items and app info tags are only available as push criteria but may not be added tooa segment or visible from Analytics, Monitoring, or Dashboard.</span></span> 
* <span data-ttu-id="62821-129">建立項目和應用程式資訊標記不能加入 tooa 區段中，您將需要 toosetup 清單針對每個活動 tooperform hello 相同函式做為目標為根據的區段中的準則。</span><span class="sxs-lookup"><span data-stu-id="62821-129">For built in items and app info tags that can't be added tooa segment, you will need toosetup list of targeting criteria in each campaign tooperform hello same function as targeting based on a segment.</span></span>
* <span data-ttu-id="62821-130">請參閱 hello 的內容功能表中的 hello Azure Mobile Engagement UI 更多協助以 hello 分析、 監控、 分割及儀表板區段以及 tooinformation。</span><span class="sxs-lookup"><span data-stu-id="62821-130">See hello context menus in hello Analytics, Monitoring, Segmentation, and Dashboards sections of hello Azure Mobile Engagement UI for more help and how tooinformation.</span></span>

## <a name="crash-troubleshooting"></a><span data-ttu-id="62821-131">當機疑難排解</span><span class="sxs-lookup"><span data-stu-id="62821-131">Crash troubleshooting</span></span>
### <a name="issue"></a><span data-ttu-id="62821-132">問題</span><span class="sxs-lookup"><span data-stu-id="62821-132">Issue</span></span>
* <span data-ttu-id="62821-133">分析、監視或儀表板中發生應用程式當機。</span><span class="sxs-lookup"><span data-stu-id="62821-133">Application Crashes appearing in Analytics, Monitoring, or Dashboard.</span></span>

### <a name="causes"></a><span data-ttu-id="62821-134">原因</span><span class="sxs-lookup"><span data-stu-id="62821-134">Causes</span></span>
* <span data-ttu-id="62821-135">tootroubleshoot 應用程式當機分析 」、 「 監視 」 或 「 儀表板中所見，請確定 toocheck hello 版本和舊版的 hello SDK 的已知問題的資訊。</span><span class="sxs-lookup"><span data-stu-id="62821-135">tootroubleshoot Application Crashes seen in Analytics, Monitoring, or Dashboard make sure toocheck hello release notes for known issues with previous versions of hello SDK.</span></span>
* <span data-ttu-id="62821-136">toofurther 疑難排解應用程式當機事件執行從測試裝置，您已安裝的應用程式和查閱您的裝置識別碼 hello Azure Mobile Engagement UI hello < 監視器 – 事件 > 一節中。</span><span class="sxs-lookup"><span data-stu-id="62821-136">toofurther troubleshoot application crashes perform an event from a test device with your application installed and look up your device ID in hello “Monitor – Events” section of hello Azure Mobile Engagement UI.</span></span> <span data-ttu-id="62821-137">然後執行造成您的應用程式 toocrash hello 事件，並且查閱 hello hello Azure Mobile Engagement UI 「 監視器 – 當機 」 一節中的其他資訊。</span><span class="sxs-lookup"><span data-stu-id="62821-137">Then perform hello event that is causing your application toocrash and look up additional information in hello “Monitor – Crash” section of hello Azure Mobile Engagement UI.</span></span> 

