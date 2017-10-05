---
title: "Azure CDN 中的即時統計資料 | Microsoft Docs"
description: "將內容傳遞給您的用戶端時，即時統計資料可提供關於 Azure CDN 效能的即時資料。"
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: c7989340-1172-4315-acbb-186ba34dd52a
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: e9b9522de6b2c54dc794b00100ffe358296ecfdd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="real-time-stats-in-microsoft-azure-cdn"></a><span data-ttu-id="c97f0-103">Microsoft Azure CDN 中的即時統計資料</span><span class="sxs-lookup"><span data-stu-id="c97f0-103">Real-time stats in Microsoft Azure CDN</span></span>
[!INCLUDE [cdn-premium-feature](../../includes/cdn-premium-feature.md)]

## <a name="overview"></a><span data-ttu-id="c97f0-104">Overview</span><span class="sxs-lookup"><span data-stu-id="c97f0-104">Overview</span></span>
<span data-ttu-id="c97f0-105">本文件說明 Microsoft Azure CDN 中的即時統計資料。</span><span class="sxs-lookup"><span data-stu-id="c97f0-105">This document explains real-time stats in Microsoft Azure CDN.</span></span>  <span data-ttu-id="c97f0-106">在將內容傳遞給您的用戶端時，這項功能會提供即時資料 (例如頻寬、快取狀態和並行連線) 給您的 CDN 設定檔。</span><span class="sxs-lookup"><span data-stu-id="c97f0-106">This functionality provides real-time data, such as bandwidth, cache statuses, and concurrent connections to your CDN profile when delivering content to your clients.</span></span> <span data-ttu-id="c97f0-107">這可讓您隨時連續監視服務的健全狀況，包括上線事件。</span><span class="sxs-lookup"><span data-stu-id="c97f0-107">This enables continuous monitoring of the health of your service at any time, including go-live events.</span></span>

<span data-ttu-id="c97f0-108">可用圖表如下︰</span><span class="sxs-lookup"><span data-stu-id="c97f0-108">The following graphs are available:</span></span>

* [<span data-ttu-id="c97f0-109">頻寬</span><span class="sxs-lookup"><span data-stu-id="c97f0-109">Bandwidth</span></span>](#bandwidth)
* [<span data-ttu-id="c97f0-110">狀態碼</span><span class="sxs-lookup"><span data-stu-id="c97f0-110">Status Codes</span></span>](#status-codes)
* [<span data-ttu-id="c97f0-111">快取狀態</span><span class="sxs-lookup"><span data-stu-id="c97f0-111">Cache Statuses</span></span>](#cache-statuses)
* [<span data-ttu-id="c97f0-112">連線</span><span class="sxs-lookup"><span data-stu-id="c97f0-112">Connections</span></span>](#connections)

## <a name="accessing-real-time-stats"></a><span data-ttu-id="c97f0-113">存取即時統計資料</span><span class="sxs-lookup"><span data-stu-id="c97f0-113">Accessing real-time stats</span></span>
1. <span data-ttu-id="c97f0-114">在 [Azure 入口網站](https://portal.azure.com)中，瀏覽到您的 CDN 設定檔。</span><span class="sxs-lookup"><span data-stu-id="c97f0-114">In the [Azure Portal](https://portal.azure.com), browse to your CDN profile.</span></span>
   
    ![CDN 設定檔刀鋒視窗](./media/cdn-real-time-stats/cdn-profile-blade.png)
2. <span data-ttu-id="c97f0-116">在 [CDN 設定檔] 刀鋒視窗中，按一下 [管理]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="c97f0-116">From the CDN profile blade, click the **Manage** button.</span></span>
   
    ![[CDN 設定檔] 刀鋒視窗的 [管理] 按鈕](./media/cdn-real-time-stats/cdn-manage-btn.png)
   
    <span data-ttu-id="c97f0-118">隨即開啟 CDN 管理入口網站。</span><span class="sxs-lookup"><span data-stu-id="c97f0-118">The CDN management portal opens.</span></span>
3. <span data-ttu-id="c97f0-119">將滑鼠移至 [分析] 索引標籤上，然後將滑鼠移至 [即時統計資料] 飛出視窗上。</span><span class="sxs-lookup"><span data-stu-id="c97f0-119">Hover over the **Analytics** tab, then hover over the **Real-Time Stats** flyout.</span></span>  <span data-ttu-id="c97f0-120">按一下 [HTTP 大型物件] 。</span><span class="sxs-lookup"><span data-stu-id="c97f0-120">Click on **HTTP Large Object**.</span></span>
   
    ![CDN 管理入口網站](./media/cdn-real-time-stats/cdn-premium-portal.png)
   
    <span data-ttu-id="c97f0-122">隨即會顯示即時統計資料圖表。</span><span class="sxs-lookup"><span data-stu-id="c97f0-122">The real-time stats graphs are displayed.</span></span>

<span data-ttu-id="c97f0-123">每個圖表都會顯示所選時間範圍內的即時統計資料，並在頁面載入時啟動。</span><span class="sxs-lookup"><span data-stu-id="c97f0-123">Each of the graphs displays real-time statistics for the selected time span, starting when the page loads.</span></span>  <span data-ttu-id="c97f0-124">圖表每隔幾秒鐘就會自動更新。</span><span class="sxs-lookup"><span data-stu-id="c97f0-124">The graphs update automatically every few seconds.</span></span>  <span data-ttu-id="c97f0-125">[重新整理圖表]  按鈕 (如果有) 將會清除圖表，然後只顯示選取的資料。</span><span class="sxs-lookup"><span data-stu-id="c97f0-125">The **Refresh Graph** button, if present, will clear the graph, after which it will only display the selected data.</span></span>

## <a name="bandwidth"></a><span data-ttu-id="c97f0-126">頻寬</span><span class="sxs-lookup"><span data-stu-id="c97f0-126">Bandwidth</span></span>
![頻寬圖表](./media/cdn-real-time-stats/cdn-bandwidth.png)

<span data-ttu-id="c97f0-128">**頻寬** 圖表會顯示所選時間範圍內，針對目前平台所使用的頻寬量。</span><span class="sxs-lookup"><span data-stu-id="c97f0-128">The **Bandwidth** graph displays the amount of bandwidth used for the current platform over the selected time span.</span></span> <span data-ttu-id="c97f0-129">圖表的陰影部分表示頻寬使用量。</span><span class="sxs-lookup"><span data-stu-id="c97f0-129">The shaded portion of the graph indicates bandwidth usage.</span></span> <span data-ttu-id="c97f0-130">目前使用的確切頻寬量會顯示於線條圖的正下方。</span><span class="sxs-lookup"><span data-stu-id="c97f0-130">The exact amount of bandwidth currently being used is displayed directly below the line graph.</span></span>

## <a name="status-codes"></a><span data-ttu-id="c97f0-131">狀態碼</span><span class="sxs-lookup"><span data-stu-id="c97f0-131">Status Codes</span></span>
![狀態碼圖表](./media/cdn-real-time-stats/cdn-status-codes.png)

<span data-ttu-id="c97f0-133">**狀態碼** 圖表會指出某些 HTTP 回應碼在所選時間範圍內的發生頻率。</span><span class="sxs-lookup"><span data-stu-id="c97f0-133">The **Status Codes** graph indicates how often certain HTTP response codes are occurring over the selected time span.</span></span>

> [!TIP]
> <span data-ttu-id="c97f0-134">如需每個 HTTP 狀態碼選項的說明，請參閱 [Azure CDN HTTP 狀態碼](https://msdn.microsoft.com/library/mt759238.aspx)。</span><span class="sxs-lookup"><span data-stu-id="c97f0-134">For a description of each HTTP status code option, see [Azure CDN HTTP Status Codes](https://msdn.microsoft.com/library/mt759238.aspx).</span></span>
> 
> 

<span data-ttu-id="c97f0-135">HTTP 狀態碼的清單會顯示於圖表正上方。</span><span class="sxs-lookup"><span data-stu-id="c97f0-135">A list of HTTP status codes is displayed directly above the graph.</span></span> <span data-ttu-id="c97f0-136">此清單表示每個可包含於線條圖中的狀態碼，以及該狀態碼目前每秒的發生次數。</span><span class="sxs-lookup"><span data-stu-id="c97f0-136">This list indicates each status code that can be included in the line graph and the current number of occurrences per second for that status code.</span></span> <span data-ttu-id="c97f0-137">根據預設，圖表中會針對這些狀態碼的每一個顯示一條線。</span><span class="sxs-lookup"><span data-stu-id="c97f0-137">By default, a line is displayed for each of these status codes in the graph.</span></span> <span data-ttu-id="c97f0-138">不過，您可以選擇只監視對您的 CDN 組態具有特殊意義的狀態碼。</span><span class="sxs-lookup"><span data-stu-id="c97f0-138">However, you can choose to only monitor the status codes that have special significance for your CDN configuration.</span></span> <span data-ttu-id="c97f0-139">若要這樣做，請檢查所需的狀態碼，並清除所有其他選項，然後按一下 [重新整理圖表] 。</span><span class="sxs-lookup"><span data-stu-id="c97f0-139">To do this, check the desired status codes and clear all other options, then click **Refresh Graph**.</span></span> 

<span data-ttu-id="c97f0-140">您可以暫時隱藏特定狀態碼的記錄資料。</span><span class="sxs-lookup"><span data-stu-id="c97f0-140">You can temporarily hide logged data for a particular status code.</span></span>  <span data-ttu-id="c97f0-141">從圖表正下方的圖例中，按一下您想要隱藏的狀態碼。</span><span class="sxs-lookup"><span data-stu-id="c97f0-141">From the legend directly below the graph, click the status code you want to hide.</span></span> <span data-ttu-id="c97f0-142">狀態碼將會立即從圖表中隱藏。</span><span class="sxs-lookup"><span data-stu-id="c97f0-142">The status code will be immediately hidden from the graph.</span></span> <span data-ttu-id="c97f0-143">再次按一下該狀態碼將導致該選項再次顯示。</span><span class="sxs-lookup"><span data-stu-id="c97f0-143">Clicking that status code again will cause that option to be displayed again.</span></span>

## <a name="cache-statuses"></a><span data-ttu-id="c97f0-144">快取狀態</span><span class="sxs-lookup"><span data-stu-id="c97f0-144">Cache Statuses</span></span>
![快取狀態圖表](./media/cdn-real-time-stats/cdn-cache-status.png)

<span data-ttu-id="c97f0-146">**快取狀態** 圖表會指出某些類型的快取狀態在所選時間範圍內的發生頻率。</span><span class="sxs-lookup"><span data-stu-id="c97f0-146">The **Cache Statuses** graph indicates how often certain types of cache statuses are occurring over the selected time span.</span></span> 

> [!TIP]
> <span data-ttu-id="c97f0-147">如需每個快取狀態碼選項的說明，請參閱 [Azure CDN 快取狀態碼](https://msdn.microsoft.com/library/mt759237.aspx)。</span><span class="sxs-lookup"><span data-stu-id="c97f0-147">For a description of each cache status code option, see [Azure CDN Cache Status Codes](https://msdn.microsoft.com/library/mt759237.aspx).</span></span>
> 
> 

<span data-ttu-id="c97f0-148">快取狀態碼的清單會顯示於圖表正上方。</span><span class="sxs-lookup"><span data-stu-id="c97f0-148">A list of cache status codes is displayed directly above the graph.</span></span> <span data-ttu-id="c97f0-149">此清單表示每個可包含於線條圖中的狀態碼，以及該狀態碼目前每秒的發生次數。</span><span class="sxs-lookup"><span data-stu-id="c97f0-149">This list indicates each status code that can be included in the line graph and the current number of occurrences per second for that status code.</span></span> <span data-ttu-id="c97f0-150">根據預設，圖表中會針對這些狀態碼的每一個顯示一條線。</span><span class="sxs-lookup"><span data-stu-id="c97f0-150">By default, a line is displayed for each of these status codes in the graph.</span></span> <span data-ttu-id="c97f0-151">不過，您可以選擇只監視對您的 CDN 組態具有特殊意義的狀態碼。</span><span class="sxs-lookup"><span data-stu-id="c97f0-151">However, you can choose to only monitor the status codes that have special significance for your CDN configuration.</span></span> <span data-ttu-id="c97f0-152">若要這樣做，請檢查所需的狀態碼，並清除所有其他選項，然後按一下 [重新整理圖表] 。</span><span class="sxs-lookup"><span data-stu-id="c97f0-152">To do this, check the desired status codes and clear all other options, then click **Refresh Graph**.</span></span> 

<span data-ttu-id="c97f0-153">您可以暫時隱藏特定狀態碼的記錄資料。</span><span class="sxs-lookup"><span data-stu-id="c97f0-153">You can temporarily hide logged data for a particular status code.</span></span>  <span data-ttu-id="c97f0-154">從圖表正下方的圖例中，按一下您想要隱藏的狀態碼。</span><span class="sxs-lookup"><span data-stu-id="c97f0-154">From the legend directly below the graph, click the status code you want to hide.</span></span> <span data-ttu-id="c97f0-155">狀態碼將會立即從圖表中隱藏。</span><span class="sxs-lookup"><span data-stu-id="c97f0-155">The status code will be immediately hidden from the graph.</span></span> <span data-ttu-id="c97f0-156">再次按一下該狀態碼將導致該選項再次顯示。</span><span class="sxs-lookup"><span data-stu-id="c97f0-156">Clicking that status code again will cause that option to be displayed again.</span></span>

## <a name="connections"></a><span data-ttu-id="c97f0-157">連線</span><span class="sxs-lookup"><span data-stu-id="c97f0-157">Connections</span></span>
![連線圖表](./media/cdn-real-time-stats/cdn-connections.png)

<span data-ttu-id="c97f0-159">此圖表會指出已為 Edge Server 建立的連線數。</span><span class="sxs-lookup"><span data-stu-id="c97f0-159">This graph indicates how many connections have been established to your edge servers.</span></span> <span data-ttu-id="c97f0-160">通過 CDN 的每個資產要求都會導致建立一個連線。</span><span class="sxs-lookup"><span data-stu-id="c97f0-160">Each request for an asset that passes through our CDN results in a connection.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c97f0-161">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c97f0-161">Next Steps</span></span>
* <span data-ttu-id="c97f0-162">透過 [Azure CDN 中的即時警示](cdn-real-time-alerts.md)</span><span class="sxs-lookup"><span data-stu-id="c97f0-162">Get notified with [Real-time alerts in Azure CDN](cdn-real-time-alerts.md)</span></span>
* <span data-ttu-id="c97f0-163">進一步了解 [進階 HTTP 報告](cdn-advanced-http-reports.md)</span><span class="sxs-lookup"><span data-stu-id="c97f0-163">Dig deeper with [advanced HTTP reports](cdn-advanced-http-reports.md)</span></span>
* <span data-ttu-id="c97f0-164">分析 [使用模式](cdn-analyze-usage-patterns.md)</span><span class="sxs-lookup"><span data-stu-id="c97f0-164">Analyze [usage patterns](cdn-analyze-usage-patterns.md)</span></span>

