---
title: "在 Azure CDN aaaReal 時間統計資料 |Microsoft 文件"
description: "傳遞內容 tooyour 用戶端時，即時統計資料會提供 Azure CDN 的 hello 效能的即時資料。"
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
ms.openlocfilehash: 68900a5092b767e45c1fdf9cef2cd03f55f38a6e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="real-time-stats-in-microsoft-azure-cdn"></a><span data-ttu-id="0fd73-103">Microsoft Azure CDN 中的即時統計資料</span><span class="sxs-lookup"><span data-stu-id="0fd73-103">Real-time stats in Microsoft Azure CDN</span></span>
[!INCLUDE [cdn-premium-feature](../../includes/cdn-premium-feature.md)]

## <a name="overview"></a><span data-ttu-id="0fd73-104">Overview</span><span class="sxs-lookup"><span data-stu-id="0fd73-104">Overview</span></span>
<span data-ttu-id="0fd73-105">本文件說明 Microsoft Azure CDN 中的即時統計資料。</span><span class="sxs-lookup"><span data-stu-id="0fd73-105">This document explains real-time stats in Microsoft Azure CDN.</span></span>  <span data-ttu-id="0fd73-106">這項功能提供即時的資料，例如頻寬、 快取狀態和並行連接 tooyour CDN 設定檔傳遞內容 tooyour 用戶端時。</span><span class="sxs-lookup"><span data-stu-id="0fd73-106">This functionality provides real-time data, such as bandwidth, cache statuses, and concurrent connections tooyour CDN profile when delivering content tooyour clients.</span></span> <span data-ttu-id="0fd73-107">這可讓在任何時間，包括移至即時事件的 hello 健全狀況服務的持續監視。</span><span class="sxs-lookup"><span data-stu-id="0fd73-107">This enables continuous monitoring of hello health of your service at any time, including go-live events.</span></span>

<span data-ttu-id="0fd73-108">下列圖表中的 hello 可用：</span><span class="sxs-lookup"><span data-stu-id="0fd73-108">hello following graphs are available:</span></span>

* [<span data-ttu-id="0fd73-109">頻寬</span><span class="sxs-lookup"><span data-stu-id="0fd73-109">Bandwidth</span></span>](#bandwidth)
* [<span data-ttu-id="0fd73-110">狀態碼</span><span class="sxs-lookup"><span data-stu-id="0fd73-110">Status Codes</span></span>](#status-codes)
* [<span data-ttu-id="0fd73-111">快取狀態</span><span class="sxs-lookup"><span data-stu-id="0fd73-111">Cache Statuses</span></span>](#cache-statuses)
* [<span data-ttu-id="0fd73-112">連線</span><span class="sxs-lookup"><span data-stu-id="0fd73-112">Connections</span></span>](#connections)

## <a name="accessing-real-time-stats"></a><span data-ttu-id="0fd73-113">存取即時統計資料</span><span class="sxs-lookup"><span data-stu-id="0fd73-113">Accessing real-time stats</span></span>
1. <span data-ttu-id="0fd73-114">在 hello [Azure 入口網站](https://portal.azure.com)，瀏覽 tooyour 的 CDN 設定檔。</span><span class="sxs-lookup"><span data-stu-id="0fd73-114">In hello [Azure Portal](https://portal.azure.com), browse tooyour CDN profile.</span></span>
   
    ![CDN 設定檔刀鋒視窗](./media/cdn-real-time-stats/cdn-profile-blade.png)
2. <span data-ttu-id="0fd73-116">從 hello CDN 設定檔刀鋒視窗中，按一下 [hello**管理**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="0fd73-116">From hello CDN profile blade, click hello **Manage** button.</span></span>
   
    ![[CDN 設定檔] 刀鋒視窗的 [管理] 按鈕](./media/cdn-real-time-stats/cdn-manage-btn.png)
   
    <span data-ttu-id="0fd73-118">hello CDN 管理入口網站隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="0fd73-118">hello CDN management portal opens.</span></span>
3. <span data-ttu-id="0fd73-119">暫留在 hello**分析** 索引標籤，然後暫留在 hello**即時統計資料**彈出式視窗。</span><span class="sxs-lookup"><span data-stu-id="0fd73-119">Hover over hello **Analytics** tab, then hover over hello **Real-Time Stats** flyout.</span></span>  <span data-ttu-id="0fd73-120">按一下 [HTTP 大型物件] 。</span><span class="sxs-lookup"><span data-stu-id="0fd73-120">Click on **HTTP Large Object**.</span></span>
   
    ![CDN 管理入口網站](./media/cdn-real-time-stats/cdn-premium-portal.png)
   
    <span data-ttu-id="0fd73-122">hello 即時統計資料圖形會顯示。</span><span class="sxs-lookup"><span data-stu-id="0fd73-122">hello real-time stats graphs are displayed.</span></span>

<span data-ttu-id="0fd73-123">每個 hello 圖形會顯示 hello 選取時間範圍內，hello 網頁載入時啟動的即時統計資料。</span><span class="sxs-lookup"><span data-stu-id="0fd73-123">Each of hello graphs displays real-time statistics for hello selected time span, starting when hello page loads.</span></span>  <span data-ttu-id="0fd73-124">hello 圖形會自動更新每隔幾秒。</span><span class="sxs-lookup"><span data-stu-id="0fd73-124">hello graphs update automatically every few seconds.</span></span>  <span data-ttu-id="0fd73-125">hello**重新整理圖形**按鈕時，如果有的話，將會清除 hello 圖形中，其後它只會顯示 hello 選取資料。</span><span class="sxs-lookup"><span data-stu-id="0fd73-125">hello **Refresh Graph** button, if present, will clear hello graph, after which it will only display hello selected data.</span></span>

## <a name="bandwidth"></a><span data-ttu-id="0fd73-126">頻寬</span><span class="sxs-lookup"><span data-stu-id="0fd73-126">Bandwidth</span></span>
![頻寬圖表](./media/cdn-real-time-stats/cdn-bandwidth.png)

<span data-ttu-id="0fd73-128">hello**頻寬**圖表顯示 hello 量 hello 目前平台透過 hello 選取時間範圍所用的頻寬。</span><span class="sxs-lookup"><span data-stu-id="0fd73-128">hello **Bandwidth** graph displays hello amount of bandwidth used for hello current platform over hello selected time span.</span></span> <span data-ttu-id="0fd73-129">hello 陰影的一部分 hello 圖形表示頻寬使用量。</span><span class="sxs-lookup"><span data-stu-id="0fd73-129">hello shaded portion of hello graph indicates bandwidth usage.</span></span> <span data-ttu-id="0fd73-130">hello 目前正在使用的頻寬數量確實會顯示 hello 折線圖的正下方。</span><span class="sxs-lookup"><span data-stu-id="0fd73-130">hello exact amount of bandwidth currently being used is displayed directly below hello line graph.</span></span>

## <a name="status-codes"></a><span data-ttu-id="0fd73-131">狀態碼</span><span class="sxs-lookup"><span data-stu-id="0fd73-131">Status Codes</span></span>
![狀態碼圖表](./media/cdn-real-time-stats/cdn-status-codes.png)

<span data-ttu-id="0fd73-133">hello**狀態碼**圖形表示透過 hello 選取時間範圍中發生特定 HTTP 回應碼的頻率。</span><span class="sxs-lookup"><span data-stu-id="0fd73-133">hello **Status Codes** graph indicates how often certain HTTP response codes are occurring over hello selected time span.</span></span>

> [!TIP]
> <span data-ttu-id="0fd73-134">如需每個 HTTP 狀態碼選項的說明，請參閱 [Azure CDN HTTP 狀態碼](https://msdn.microsoft.com/library/mt759238.aspx)。</span><span class="sxs-lookup"><span data-stu-id="0fd73-134">For a description of each HTTP status code option, see [Azure CDN HTTP Status Codes](https://msdn.microsoft.com/library/mt759238.aspx).</span></span>
> 
> 

<span data-ttu-id="0fd73-135">HTTP 狀態碼的清單會顯示 hello 圖形上方的直接。</span><span class="sxs-lookup"><span data-stu-id="0fd73-135">A list of HTTP status codes is displayed directly above hello graph.</span></span> <span data-ttu-id="0fd73-136">這份清單表示可以包含在 hello 折線圖和 hello 目前發生次數的每秒該狀態碼的每個狀態碼。</span><span class="sxs-lookup"><span data-stu-id="0fd73-136">This list indicates each status code that can be included in hello line graph and hello current number of occurrences per second for that status code.</span></span> <span data-ttu-id="0fd73-137">根據預設，一條線會顯示每個這些 hello 圖形中的狀態碼。</span><span class="sxs-lookup"><span data-stu-id="0fd73-137">By default, a line is displayed for each of these status codes in hello graph.</span></span> <span data-ttu-id="0fd73-138">不過，您可以選擇 tooonly 有特殊意義，您的 CDN 組態的監視 hello 狀態碼。</span><span class="sxs-lookup"><span data-stu-id="0fd73-138">However, you can choose tooonly monitor hello status codes that have special significance for your CDN configuration.</span></span> <span data-ttu-id="0fd73-139">toodo，檢查所需的 hello 狀態碼和清除所有其他選項]，然後按 [**重新整理圖形**。</span><span class="sxs-lookup"><span data-stu-id="0fd73-139">toodo this, check hello desired status codes and clear all other options, then click **Refresh Graph**.</span></span> 

<span data-ttu-id="0fd73-140">您可以暫時隱藏特定狀態碼的記錄資料。</span><span class="sxs-lookup"><span data-stu-id="0fd73-140">You can temporarily hide logged data for a particular status code.</span></span>  <span data-ttu-id="0fd73-141">從 hello 圖例 hello 圖形正下方，按一下您想要 toohide hello 狀態碼。</span><span class="sxs-lookup"><span data-stu-id="0fd73-141">From hello legend directly below hello graph, click hello status code you want toohide.</span></span> <span data-ttu-id="0fd73-142">hello 狀態碼將會立即隱藏 hello 圖形中。</span><span class="sxs-lookup"><span data-stu-id="0fd73-142">hello status code will be immediately hidden from hello graph.</span></span> <span data-ttu-id="0fd73-143">再次按一下該狀態碼將會再次顯示該選項 toobe。</span><span class="sxs-lookup"><span data-stu-id="0fd73-143">Clicking that status code again will cause that option toobe displayed again.</span></span>

## <a name="cache-statuses"></a><span data-ttu-id="0fd73-144">快取狀態</span><span class="sxs-lookup"><span data-stu-id="0fd73-144">Cache Statuses</span></span>
![快取狀態圖表](./media/cdn-real-time-stats/cdn-cache-status.png)

<span data-ttu-id="0fd73-146">hello**快取狀態**圖形表示透過 hello 選取時間範圍中發生特定類型的快取狀態的頻率。</span><span class="sxs-lookup"><span data-stu-id="0fd73-146">hello **Cache Statuses** graph indicates how often certain types of cache statuses are occurring over hello selected time span.</span></span> 

> [!TIP]
> <span data-ttu-id="0fd73-147">如需每個快取狀態碼選項的說明，請參閱 [Azure CDN 快取狀態碼](https://msdn.microsoft.com/library/mt759237.aspx)。</span><span class="sxs-lookup"><span data-stu-id="0fd73-147">For a description of each cache status code option, see [Azure CDN Cache Status Codes](https://msdn.microsoft.com/library/mt759237.aspx).</span></span>
> 
> 

<span data-ttu-id="0fd73-148">快取的狀態碼清單會顯示 hello 圖形上方的直接。</span><span class="sxs-lookup"><span data-stu-id="0fd73-148">A list of cache status codes is displayed directly above hello graph.</span></span> <span data-ttu-id="0fd73-149">這份清單表示可以包含在 hello 折線圖和 hello 目前發生次數的每秒該狀態碼的每個狀態碼。</span><span class="sxs-lookup"><span data-stu-id="0fd73-149">This list indicates each status code that can be included in hello line graph and hello current number of occurrences per second for that status code.</span></span> <span data-ttu-id="0fd73-150">根據預設，一條線會顯示每個這些 hello 圖形中的狀態碼。</span><span class="sxs-lookup"><span data-stu-id="0fd73-150">By default, a line is displayed for each of these status codes in hello graph.</span></span> <span data-ttu-id="0fd73-151">不過，您可以選擇 tooonly 有特殊意義，您的 CDN 組態的監視 hello 狀態碼。</span><span class="sxs-lookup"><span data-stu-id="0fd73-151">However, you can choose tooonly monitor hello status codes that have special significance for your CDN configuration.</span></span> <span data-ttu-id="0fd73-152">toodo，檢查所需的 hello 狀態碼和清除所有其他選項]，然後按 [**重新整理圖形**。</span><span class="sxs-lookup"><span data-stu-id="0fd73-152">toodo this, check hello desired status codes and clear all other options, then click **Refresh Graph**.</span></span> 

<span data-ttu-id="0fd73-153">您可以暫時隱藏特定狀態碼的記錄資料。</span><span class="sxs-lookup"><span data-stu-id="0fd73-153">You can temporarily hide logged data for a particular status code.</span></span>  <span data-ttu-id="0fd73-154">從 hello 圖例 hello 圖形正下方，按一下您想要 toohide hello 狀態碼。</span><span class="sxs-lookup"><span data-stu-id="0fd73-154">From hello legend directly below hello graph, click hello status code you want toohide.</span></span> <span data-ttu-id="0fd73-155">hello 狀態碼將會立即隱藏 hello 圖形中。</span><span class="sxs-lookup"><span data-stu-id="0fd73-155">hello status code will be immediately hidden from hello graph.</span></span> <span data-ttu-id="0fd73-156">再次按一下該狀態碼將會再次顯示該選項 toobe。</span><span class="sxs-lookup"><span data-stu-id="0fd73-156">Clicking that status code again will cause that option toobe displayed again.</span></span>

## <a name="connections"></a><span data-ttu-id="0fd73-157">連線</span><span class="sxs-lookup"><span data-stu-id="0fd73-157">Connections</span></span>
![連線圖表](./media/cdn-real-time-stats/cdn-connections.png)

<span data-ttu-id="0fd73-159">此圖表指出多少的連線已建立的 tooyour 邊緣伺服器。</span><span class="sxs-lookup"><span data-stu-id="0fd73-159">This graph indicates how many connections have been established tooyour edge servers.</span></span> <span data-ttu-id="0fd73-160">通過 CDN 的每個資產要求都會導致建立一個連線。</span><span class="sxs-lookup"><span data-stu-id="0fd73-160">Each request for an asset that passes through our CDN results in a connection.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0fd73-161">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0fd73-161">Next Steps</span></span>
* <span data-ttu-id="0fd73-162">透過 [Azure CDN 中的即時警示](cdn-real-time-alerts.md)</span><span class="sxs-lookup"><span data-stu-id="0fd73-162">Get notified with [Real-time alerts in Azure CDN](cdn-real-time-alerts.md)</span></span>
* <span data-ttu-id="0fd73-163">進一步了解 [進階 HTTP 報告](cdn-advanced-http-reports.md)</span><span class="sxs-lookup"><span data-stu-id="0fd73-163">Dig deeper with [advanced HTTP reports](cdn-advanced-http-reports.md)</span></span>
* <span data-ttu-id="0fd73-164">分析 [使用模式](cdn-analyze-usage-patterns.md)</span><span class="sxs-lookup"><span data-stu-id="0fd73-164">Analyze [usage patterns](cdn-analyze-usage-patterns.md)</span></span>

