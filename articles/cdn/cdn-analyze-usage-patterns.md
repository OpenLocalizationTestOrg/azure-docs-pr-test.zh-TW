---
title: "分析 Azure CDN 使用模式 | Microsoft Docs"
description: "您可以使用下列報告檢視 CDN 的使用模式：頻寬、傳輸的資料、點擊、快取狀態、快取點擊率、已傳輸的 IPV4/IPV6 資料。"
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 5a0d9018-8bdb-48ff-84df-23648ebcf763
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: aadbe872dd3384c8d337b432fb3be69422ca322b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="analyze-azure-cdn-usage-patterns"></a><span data-ttu-id="d8486-103">分析 Azure CDN 使用模式</span><span class="sxs-lookup"><span data-stu-id="d8486-103">Analyze Azure CDN usage patterns</span></span>

[!INCLUDE[cdn-verizon-only](../../includes/cdn-verizon-only.md)]

<span data-ttu-id="d8486-104">下方指南示範透過 Verizon 設定檔適用的管理入口網站來檢視核心報告的步驟。</span><span class="sxs-lookup"><span data-stu-id="d8486-104">The guide below goes through the steps to view the core reports via the Manage portal for Verizon profiles.</span></span> <span data-ttu-id="d8486-105">您也可以[透過 Azure 入口網站](cdn-log-analysis.md)將核心分析資料匯出到 Verizon 與 Akamai 設定檔皆適用的儲存體、事件中樞或 Log Analytics (OMS)。</span><span class="sxs-lookup"><span data-stu-id="d8486-105">You may also export core analytics data to storage, event hub, or log analytics (oms) for both Verizon and Akamai profiles [through the azure portal](cdn-log-analysis.md).</span></span>

<span data-ttu-id="d8486-106">您可以使用下列報告檢視 CDN 的使用模式：</span><span class="sxs-lookup"><span data-stu-id="d8486-106">You can view usage patterns for your CDN using the following reports:</span></span>

* <span data-ttu-id="d8486-107">頻寬</span><span class="sxs-lookup"><span data-stu-id="d8486-107">Bandwidth</span></span>
* <span data-ttu-id="d8486-108">傳輸的資料</span><span class="sxs-lookup"><span data-stu-id="d8486-108">Data Transferred</span></span>
* <span data-ttu-id="d8486-109">點擊</span><span class="sxs-lookup"><span data-stu-id="d8486-109">Hits</span></span>
* <span data-ttu-id="d8486-110">快取狀態</span><span class="sxs-lookup"><span data-stu-id="d8486-110">Cache Statuses</span></span>
* <span data-ttu-id="d8486-111">快取點擊率</span><span class="sxs-lookup"><span data-stu-id="d8486-111">Cache Hit Ratio</span></span>
* <span data-ttu-id="d8486-112">已轉送的 IPV4/IPV6 資料</span><span class="sxs-lookup"><span data-stu-id="d8486-112">IPV4/IPV6 Data Transferred</span></span>

## <a name="accessing-core-reports"></a><span data-ttu-id="d8486-113">存取核心報告</span><span class="sxs-lookup"><span data-stu-id="d8486-113">Accessing Core Reports</span></span>
1. <span data-ttu-id="d8486-114">在 [CDN 設定檔] 刀鋒視窗中，按一下 [管理]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="d8486-114">From the CDN profile blade, click the **Manage** button.</span></span>
   
    ![[CDN 設定檔] 刀鋒視窗的 [管理] 按鈕](./media/cdn-reports/cdn-manage-btn.png)
   
    <span data-ttu-id="d8486-116">隨即開啟 CDN 管理入口網站。</span><span class="sxs-lookup"><span data-stu-id="d8486-116">The CDN management portal opens.</span></span>
2. <span data-ttu-id="d8486-117">將滑鼠移至 [分析] 索引標籤上，然後將滑鼠移至 [核心報告] 飛出視窗上。</span><span class="sxs-lookup"><span data-stu-id="d8486-117">Hover over the **Analytics** tab, then hover over the **Core Reports** flyout.</span></span>  <span data-ttu-id="d8486-118">在功能表中按一下所需的報表。</span><span class="sxs-lookup"><span data-stu-id="d8486-118">Click on the desired report in the menu.</span></span>
   
    ![CDN 管理入口網站 - 核心報告功能表](./media/cdn-reports/cdn-core-reports.png)

## <a name="bandwidth"></a><span data-ttu-id="d8486-120">頻寬</span><span class="sxs-lookup"><span data-stu-id="d8486-120">Bandwidth</span></span>
<span data-ttu-id="d8486-121">頻寬報告由圖形和資料表所組成，指出 HTTP 與 HTTPS 在特定期間的頻寬使用量。</span><span class="sxs-lookup"><span data-stu-id="d8486-121">The bandwidth report consists of a graph and data table indicating the bandwidth usage for HTTP and HTTPS over a particular time period.</span></span> <span data-ttu-id="d8486-122">您可以跨所有 CDN POP 或特定 POP 檢視頻寬使用量。</span><span class="sxs-lookup"><span data-stu-id="d8486-122">You can view the bandwidth usage across all CDN POPs or a particular POP.</span></span> <span data-ttu-id="d8486-123">這可讓您檢視整個 CDN POP流量尖峰與分佈 (以 Mbps 為單位)。</span><span class="sxs-lookup"><span data-stu-id="d8486-123">This allows you to view the traffic spikes and distribution across CDN POPs in Mbps.</span></span>

* <span data-ttu-id="d8486-124">選取所有邊緣節點，從所有節點查看流量，或從下拉式清單選擇特定的區域/節點。</span><span class="sxs-lookup"><span data-stu-id="d8486-124">Select All Edge Nodes to see traffic from all nodes or choose a specific region/node from the dropdown list.</span></span>
* <span data-ttu-id="d8486-125">選取日期範圍來檢視今天/本週/本月份等資料，或輸入自訂日期，然後按一下 [執行] 來確定已更新您的選擇。</span><span class="sxs-lookup"><span data-stu-id="d8486-125">Select Date range to view data for today/this week/this month, etc. or enter custom dates, then click "go" to make sure your selection is updated.</span></span>
* <span data-ttu-id="d8486-126">您可以藉由按一下 [執行] 旁的 excel 工作表圖示以匯出和下載資料。</span><span class="sxs-lookup"><span data-stu-id="d8486-126">You can export and download the data by clicking the excel sheet icon located next to "go".</span></span>

<span data-ttu-id="d8486-127">報告每 5 分鐘更新一次。</span><span class="sxs-lookup"><span data-stu-id="d8486-127">The report is updated every 5 minutes.</span></span>

![頻寬報告](./media/cdn-reports/cdn-bandwidth.png)

## <a name="data-transferred"></a><span data-ttu-id="d8486-129">傳輸的資料</span><span class="sxs-lookup"><span data-stu-id="d8486-129">Data transferred</span></span>
<span data-ttu-id="d8486-130">此報告由圖形和資料表所組成，指出 HTTP 與 HTTPS 在特定期間的流量使用量。</span><span class="sxs-lookup"><span data-stu-id="d8486-130">This report consists of a graph and data table indicating the traffic usage for HTTP and HTTPS over a particular time period.</span></span> <span data-ttu-id="d8486-131">您可以跨所有 CDN POP 或特定 POP 檢視流量使用量。</span><span class="sxs-lookup"><span data-stu-id="d8486-131">You can view the traffic usage across all CDN POPs or a particular POP.</span></span> <span data-ttu-id="d8486-132">這可讓您檢視整個 CDN POP流量尖峰與分佈 (以 GB 為單位)。</span><span class="sxs-lookup"><span data-stu-id="d8486-132">This allows you to view the traffic spikes and distribution across CDN POPs in GB.</span></span>

* <span data-ttu-id="d8486-133">選取所有邊緣節點，從所有注意事項查看流量，或從下拉式清單選擇特定的區域/節點。</span><span class="sxs-lookup"><span data-stu-id="d8486-133">Select All Edge Nodes to see traffic from all notes or choose a specific region/node from the dropdown list.</span></span>
* <span data-ttu-id="d8486-134">選取日期範圍來檢視今天/本週/本月份等資料，或輸入自訂日期，然後按一下 [執行] 來確定已更新您的選擇。</span><span class="sxs-lookup"><span data-stu-id="d8486-134">Select Date range to view data for today/this week/this month, etc. or enter custom dates, then click "go" to make sure your selection is updated.</span></span>
* <span data-ttu-id="d8486-135">您可以藉由按一下 [執行] 旁的 excel 工作表圖示以匯出和下載資料。</span><span class="sxs-lookup"><span data-stu-id="d8486-135">You can export and download the data by clicking the excel sheet icon located next to "go" .</span></span>

<span data-ttu-id="d8486-136">報告每 5 分鐘更新一次。</span><span class="sxs-lookup"><span data-stu-id="d8486-136">The report is updated every 5 minutes.</span></span>

![傳輸的資料報告](./media/cdn-reports/cdn-data-transferred.png)

## <a name="hits-status-codes"></a><span data-ttu-id="d8486-138">點擊 (狀態碼)</span><span class="sxs-lookup"><span data-stu-id="d8486-138">Hits (status codes)</span></span>
<span data-ttu-id="d8486-139">這份報告描述內容之要求狀態碼的分佈。</span><span class="sxs-lookup"><span data-stu-id="d8486-139">This report describes the distribution of request status codes for your content.</span></span> <span data-ttu-id="d8486-140">內容的每個要求都會產生 HTTP 狀態碼。</span><span class="sxs-lookup"><span data-stu-id="d8486-140">Every request for content will generate an HTTP status code.</span></span> <span data-ttu-id="d8486-141">狀態碼描述邊緣 POP 如何處理要求。</span><span class="sxs-lookup"><span data-stu-id="d8486-141">The status code describes how edge POPs handled the request.</span></span> <span data-ttu-id="d8486-142">例如，2xx 狀態碼指出已成功向用戶端提出要求，而 4xx 狀態碼指出發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="d8486-142">For example, 2xx status codes indicate that the request was successfully served to a client, while a 4xx status code indicates an error occurred.</span></span> <span data-ttu-id="d8486-143">如需 HTTP 狀態碼的詳細資料，請參閱 [狀態碼](https://en.wikipedia.org/wiki/List_of_HTTP_status_codes)。</span><span class="sxs-lookup"><span data-stu-id="d8486-143">For more details about HTTP status code, see [status codes](https://en.wikipedia.org/wiki/List_of_HTTP_status_codes).</span></span>

* <span data-ttu-id="d8486-144">選取日期範圍來檢視今天/本週/本月份等資料，或輸入自訂日期，然後按一下 [執行] 來確定已更新您的選擇。</span><span class="sxs-lookup"><span data-stu-id="d8486-144">Select Date range to view data for today/this week/this month, etc. or enter custom dates, then click "go" to make sure your selection is updated.</span></span>
* <span data-ttu-id="d8486-145">您可以藉由按一下 [執行] 旁的 excel 工作表以匯出和下載資料。</span><span class="sxs-lookup"><span data-stu-id="d8486-145">You can export and download the data by clicking the excel sheet located next to "go".</span></span>

![點擊報告](./media/cdn-reports/cdn-hits.png)

## <a name="cache-statuses"></a><span data-ttu-id="d8486-147">快取狀態</span><span class="sxs-lookup"><span data-stu-id="d8486-147">Cache statuses</span></span>
<span data-ttu-id="d8486-148">這份報告描述快取點擊的分佈和用戶端要求的快取遺漏。</span><span class="sxs-lookup"><span data-stu-id="d8486-148">This report describes the distribution of cache hits and cache misses for client request.</span></span> <span data-ttu-id="d8486-149">由於最快的效能來自快取點擊，您可以將快取遺漏及過期快取點擊的情況降至最低，以最佳化資料傳送速度。</span><span class="sxs-lookup"><span data-stu-id="d8486-149">Since the fastest performance comes from cache hits, you can optimize data delivery speeds by minimizing cache misses and expired cache hits.</span></span> <span data-ttu-id="d8486-150">下列方式可減少快取遺漏：設定原始伺服器以避免指派 "no-cache" 回應標頭、避免除了絕對必要以外的查詢字串快取，以及避免不可快取的回應碼。</span><span class="sxs-lookup"><span data-stu-id="d8486-150">Cache misses can be reduced by configuring your origin server to avoid assigning "no-cache" response headers, by avoiding query-string caching except where strictly needed, and by avoiding non-cacheable response codes.</span></span> <span data-ttu-id="d8486-151">盡可能延長資產的 max-age 可避免過期的快取點擊，將對原始伺服器提出的要求數目降到最少。</span><span class="sxs-lookup"><span data-stu-id="d8486-151">Expired cache hits can be avoided by making an asset's max-age as long as possible to minimize the number of requests to the origin server.</span></span>

![快取狀態報告](./media/cdn-reports/cdn-cache-statuses.png)

### <a name="main-cache-statuses-include"></a><span data-ttu-id="d8486-153">主要的快取狀態包括：</span><span class="sxs-lookup"><span data-stu-id="d8486-153">Main cache statuses include:</span></span>
* <span data-ttu-id="d8486-154">TCP_HIT：從邊緣提供。</span><span class="sxs-lookup"><span data-stu-id="d8486-154">TCP_HIT: Served from Edge.</span></span> <span data-ttu-id="d8486-155">此物件在快取中且不超過其 max-age。</span><span class="sxs-lookup"><span data-stu-id="d8486-155">The object was in cache and had not exceeded its max-age.</span></span>
* <span data-ttu-id="d8486-156">TCP_MISS：從來源提供。</span><span class="sxs-lookup"><span data-stu-id="d8486-156">TCP_MISS: Served from Origin.</span></span> <span data-ttu-id="d8486-157">此物件不在快取中，但回應會回到來源。</span><span class="sxs-lookup"><span data-stu-id="d8486-157">The object was not in cache and the response was back to origin.</span></span>
* <span data-ttu-id="d8486-158">TCP_EXPIRED _MISS：利用來源重新驗證之後從來源提供。</span><span class="sxs-lookup"><span data-stu-id="d8486-158">TCP_EXPIRED _MISS: Served from origin after revalidation with origin.</span></span> <span data-ttu-id="d8486-159">此物件在快取中但超過其 max-age。</span><span class="sxs-lookup"><span data-stu-id="d8486-159">The object was in cache but had exceeded its max-age.</span></span> <span data-ttu-id="d8486-160">利用來源進行重新驗證會導致來自來源的新回應取代快取物件。</span><span class="sxs-lookup"><span data-stu-id="d8486-160">A revalidation with origin resulted in the cache object being replaced by a new response from origin.</span></span>
* <span data-ttu-id="d8486-161">TCP_EXPIRED _HIT：利用來源重新驗證之後從邊緣提供。</span><span class="sxs-lookup"><span data-stu-id="d8486-161">TCP_EXPIRED _HIT: Served from Edge after revalidation with origin.</span></span> <span data-ttu-id="d8486-162">此物件在快取中但超過其 max-age。</span><span class="sxs-lookup"><span data-stu-id="d8486-162">The object was in cache but had exceeded its max-age.</span></span> <span data-ttu-id="d8486-163">利用原始伺服器進行重新驗證會導致未經修改的快取物件。</span><span class="sxs-lookup"><span data-stu-id="d8486-163">A revalidation with the origin server resulted in the cache object being unmodified.</span></span>
* <span data-ttu-id="d8486-164">選取日期範圍來檢視今天/本週/本月份等資料，或輸入自訂日期，然後按一下 [執行] 來確定已更新您的選擇。</span><span class="sxs-lookup"><span data-stu-id="d8486-164">Select Date range to view data for today/this week/this month, etc. or enter custom dates, then click "go" to make sure your selection is updated.</span></span>
* <span data-ttu-id="d8486-165">您可以藉由按一下 [執行] 旁的 excel 工作表圖示以匯出和下載資料。</span><span class="sxs-lookup"><span data-stu-id="d8486-165">You can export and download the data by clicking the excel sheet icon located next to "go".</span></span>

### <a name="full-list-of-cache-statuses"></a><span data-ttu-id="d8486-166">快取狀態的完整清單</span><span class="sxs-lookup"><span data-stu-id="d8486-166">Full list of cache statuses</span></span>
* <span data-ttu-id="d8486-167">TCP_HIT - 直接從 POP 提供要求給用戶端時會回報此狀態。</span><span class="sxs-lookup"><span data-stu-id="d8486-167">TCP_HIT - This status is reported when a request is served directly from the POP to the client.</span></span> <span data-ttu-id="d8486-168">當資產在最接近用戶端的 POP 上快取且具有有效的存留時間 或 TTL 時，它會立即由 POP 提供。</span><span class="sxs-lookup"><span data-stu-id="d8486-168">An asset is immediately served from a POP when it is cached on the POP closest to the client and it has a valid time-to-live, or TTL.</span></span> <span data-ttu-id="d8486-169">TTL 由下列回應標頭決定：</span><span class="sxs-lookup"><span data-stu-id="d8486-169">TTL is determined by the following response headers:</span></span>
  
  * <span data-ttu-id="d8486-170">Cache-Control: s-maxage</span><span class="sxs-lookup"><span data-stu-id="d8486-170">Cache-Control: s-maxage</span></span>
  * <span data-ttu-id="d8486-171">Cache-Control: max-age</span><span class="sxs-lookup"><span data-stu-id="d8486-171">Cache-Control: max-age</span></span>
  * <span data-ttu-id="d8486-172">Expires</span><span class="sxs-lookup"><span data-stu-id="d8486-172">Expires</span></span>
* <span data-ttu-id="d8486-173">TCP_MISS - 這個狀態指出最接近用戶端的 POP 上找不到要求資產的快取版本。</span><span class="sxs-lookup"><span data-stu-id="d8486-173">TCP_MISS - This status indicates that a cached version of the requested asset was not found on the POP closest to the client.</span></span> <span data-ttu-id="d8486-174">資產會從原始伺服器或原始保護盾伺服器要求。</span><span class="sxs-lookup"><span data-stu-id="d8486-174">The asset will be requested from either an origin server or an origin shield server.</span></span> <span data-ttu-id="d8486-175">如果原始伺服器或原始保護盾伺服器傳回資產，它會提供給用戶端並在用戶端及邊緣伺服器上快取。</span><span class="sxs-lookup"><span data-stu-id="d8486-175">If the origin server or the origin shield server returns an asset, it will be served to the client and cached on both the client and the edge server.</span></span> <span data-ttu-id="d8486-176">否則，將會傳回非 200 狀態碼 (例如，403 禁止，404 找不到等)。</span><span class="sxs-lookup"><span data-stu-id="d8486-176">Otherwise, a non-200 status code (e.g., 403 Forbidden, 404 Not Found, etc.) will be returned.</span></span>
* <span data-ttu-id="d8486-177">TCP_EXPIRED _HIT - 當要求的目標是 TTL 已過期的資產 (例如，當資產的 max-age 已過期) 且該要求會直接從 POP 提供給用戶端時，就會回報此狀態。</span><span class="sxs-lookup"><span data-stu-id="d8486-177">TCP_EXPIRED _HIT -  This status is reported when a request that targeted an asset with an expired TTL, such as when the asset's max-age has expired, was served directly from the POP to the client.</span></span>
  
    <span data-ttu-id="d8486-178">過期的要求通常會導致對原始伺服器提出重新驗證要求。</span><span class="sxs-lookup"><span data-stu-id="d8486-178">An expired request typically results in a revalidation request to the origin server.</span></span> <span data-ttu-id="d8486-179">為了讓 TCP_EXPIRED _HIT 發生，原始伺服器必須指出較新版的資產不存在。</span><span class="sxs-lookup"><span data-stu-id="d8486-179">In order for a TCP_EXPIRED _HIT to occur, the origin server must indicate that a newer version of the asset does not exist.</span></span> <span data-ttu-id="d8486-180">這種情況通常會更新該資產的 Cache-Control 和 Expires 標頭。</span><span class="sxs-lookup"><span data-stu-id="d8486-180">This type of situation will typically update that asset's Cache-Control and Expires headers.</span></span>
* <span data-ttu-id="d8486-181">TCP_EXPIRED _MISS - 當較新版本的過期快取資產從 POP 提供給用戶端時，就會回報此狀態。</span><span class="sxs-lookup"><span data-stu-id="d8486-181">TCP_EXPIRED _MISS - This status is reported when a newer version of an expired cached asset is served from the POP to the client.</span></span> <span data-ttu-id="d8486-182">當快取資產的 TTL 過期 (例如過期的 max-age) 且原始伺服器傳回較新版本的資產時，就會發生此狀態。</span><span class="sxs-lookup"><span data-stu-id="d8486-182">This occurs when the TTL for a cached asset has expired (e.g., expired max-age) and the origin server returns a newer version of that asset.</span></span> <span data-ttu-id="d8486-183">新版的資產將提供給用戶端而不是快取版本。</span><span class="sxs-lookup"><span data-stu-id="d8486-183">This new version of the asset will be served to the client instead of the cached version.</span></span> <span data-ttu-id="d8486-184">此外，它將會在邊緣伺服器和用戶端上快取。</span><span class="sxs-lookup"><span data-stu-id="d8486-184">Additionally, it will be cached on the edge server and the client.</span></span>
* <span data-ttu-id="d8486-185">CONFIG_NOCACHE - 這個狀態指出邊緣 POP 上的客戶專屬組態會防止快取資產。</span><span class="sxs-lookup"><span data-stu-id="d8486-185">CONFIG_NOCACHE - This status indicates that a customer-specific configuration on our edge POP prevented the asset from being cached.</span></span>
* <span data-ttu-id="d8486-186">NONE - 這個狀態指出快取內容的有效性檢查並未執行。</span><span class="sxs-lookup"><span data-stu-id="d8486-186">NONE - This status indicates that a cache content freshness check was not performed.</span></span>
* <span data-ttu-id="d8486-187">TCP_ CLIENT_REFRESH _MISS - 當 HTTP 用戶端 (例如瀏覽器) 強制邊緣 POP 從原始伺服器擷取新版的過時資產時，就會傳回此狀態。</span><span class="sxs-lookup"><span data-stu-id="d8486-187">TCP_ CLIENT_REFRESH _MISS - This status is reported when an HTTP client (e.g., browser) forces an edge POP to retrieve a new version of a stale asset from the origin server.</span></span>
  
    <span data-ttu-id="d8486-188">根據預設，我們的伺服器可以防止 HTTP 用戶端強制我們的邊緣伺服器從原始伺服器擷取新版的資產。</span><span class="sxs-lookup"><span data-stu-id="d8486-188">By default, our servers prevent an HTTP client from forcing our edge servers to retrieve a new version of the asset from the origin server.</span></span>
* <span data-ttu-id="d8486-189">TCP_ PARTIAL_HIT - 當位元組範圍要求導致部分快取資產的點擊時，就會傳回此狀態。</span><span class="sxs-lookup"><span data-stu-id="d8486-189">TCP_ PARTIAL_HIT - This status is reported when a byte range request results in a hit for a partially cached asset.</span></span> <span data-ttu-id="d8486-190">要求的位元組範圍會立即從 POP 提供給用戶端。</span><span class="sxs-lookup"><span data-stu-id="d8486-190">The requested byte range is immediately served from the POP to the client.</span></span>
* <span data-ttu-id="d8486-191">UNCACHEABLE - 當資產的 Cache-Control 和 Expires 標頭指出不應該在 POP 上或由 HTTP 用戶端將其快取時，就會傳回此狀態。</span><span class="sxs-lookup"><span data-stu-id="d8486-191">UNCACHEABLE - This status is reported when an asset's Cache-Control and Expires headers indicate that it should not be cached on a POP or by the HTTP client.</span></span> <span data-ttu-id="d8486-192">這些要求類型會由原始伺服器提供</span><span class="sxs-lookup"><span data-stu-id="d8486-192">These types of requests are served from the origin server</span></span>

## <a name="cache-hit-ratio"></a><span data-ttu-id="d8486-193">快取點擊率</span><span class="sxs-lookup"><span data-stu-id="d8486-193">Cache Hit Ratio</span></span>
<span data-ttu-id="d8486-194">此報告指出直接從快取處理的快取要求百分比。</span><span class="sxs-lookup"><span data-stu-id="d8486-194">This report indicates the percentage of cached requests that were served directly from cache.</span></span>

<span data-ttu-id="d8486-195">此報告提供下列詳細資料：</span><span class="sxs-lookup"><span data-stu-id="d8486-195">The report provides the following details:</span></span>

* <span data-ttu-id="d8486-196">要求的內容是在最接近要求者的 POP 上加以快取。</span><span class="sxs-lookup"><span data-stu-id="d8486-196">The requested content was cached on the POP closest to the requester.</span></span>
* <span data-ttu-id="d8486-197">直接從網路邊緣處理要求。</span><span class="sxs-lookup"><span data-stu-id="d8486-197">The request was served directly from the edge of our network.</span></span>
* <span data-ttu-id="d8486-198">要求不需要利用原始伺服器重新驗證。</span><span class="sxs-lookup"><span data-stu-id="d8486-198">The request did not require revalidation with the origin server.</span></span>

<span data-ttu-id="d8486-199">報告不包含：</span><span class="sxs-lookup"><span data-stu-id="d8486-199">The report doesn't include:</span></span>

* <span data-ttu-id="d8486-200">因為國家 (地區) 篩選選項而拒絕的要求。</span><span class="sxs-lookup"><span data-stu-id="d8486-200">Requests that are denied due to country filtering options.</span></span>
* <span data-ttu-id="d8486-201">資產的要求，其標頭指出他們不應該快取。</span><span class="sxs-lookup"><span data-stu-id="d8486-201">Requests for assets whose headers indicate that they should not be cached.</span></span> <span data-ttu-id="d8486-202">例如，Cache-Control: private、Cache-Control: no-cache 或 Pragma: no-cache 等標頭會防止資產被快取。</span><span class="sxs-lookup"><span data-stu-id="d8486-202">For example, Cache-Control: private, Cache-Control: no-cache, or Pragma: no-cache headers will prevent an asset from being cached.</span></span>
* <span data-ttu-id="d8486-203">部分快取內容的位元組範圍要求。</span><span class="sxs-lookup"><span data-stu-id="d8486-203">Byte range requests for partially cached content.</span></span>

<span data-ttu-id="d8486-204">公式為：(TCP_ HIT/(TCP_ HIT+TCP_MISS))*100</span><span class="sxs-lookup"><span data-stu-id="d8486-204">The formula is: (TCP_ HIT/(TCP_ HIT+TCP_MISS))*100</span></span>

* <span data-ttu-id="d8486-205">選取日期範圍來檢視今天/本週/本月份等資料，或輸入自訂日期，然後按一下 [執行] 來確定已更新您的選擇。</span><span class="sxs-lookup"><span data-stu-id="d8486-205">Select Date range to view data for today/this week/this month, etc. or enter custom dates, then click "go" to make sure your selection is updated.</span></span>
* <span data-ttu-id="d8486-206">您可以藉由按一下 [執行] 旁的 excel 工作表圖示以匯出和下載資料。</span><span class="sxs-lookup"><span data-stu-id="d8486-206">You can export and download the data by clicking the excel sheet icon located next to "go" .</span></span>

![快取點擊率報告](./media/cdn-reports/cdn-cache-hit-ratio.png)

## <a name="ipv4ipv6-data-transferred"></a><span data-ttu-id="d8486-208">已轉送的 IPV4/IPV6 資料</span><span class="sxs-lookup"><span data-stu-id="d8486-208">IPV4/IPV6 Data transferred</span></span>
<span data-ttu-id="d8486-209">此報告會顯示在 IPV4 與 IPV6 中流量使用量的分佈。</span><span class="sxs-lookup"><span data-stu-id="d8486-209">This report shows the traffic usage distribution in IPV4 vs IPV6.</span></span>

![已轉送的 IPV4/IPV6 資料](./media/cdn-reports/cdn-ipv4-ipv6.png)

* <span data-ttu-id="d8486-211">選取日期範圍來檢視今天/本週/本月份等資料，或輸入自訂日期。</span><span class="sxs-lookup"><span data-stu-id="d8486-211">Select Date range to view data for today/this week/this month, etc. or enter custom dates.</span></span>
* <span data-ttu-id="d8486-212">然後按一下 [執行] 來確定已更新您的選擇。</span><span class="sxs-lookup"><span data-stu-id="d8486-212">Then, click "go" to make sure your selection is updated.</span></span>

## <a name="considerations"></a><span data-ttu-id="d8486-213">注意事項</span><span class="sxs-lookup"><span data-stu-id="d8486-213">Considerations</span></span>
<span data-ttu-id="d8486-214">報告只會產生於過去 18 個月內。</span><span class="sxs-lookup"><span data-stu-id="d8486-214">Reports can only be generated within the last 18 months.</span></span>

