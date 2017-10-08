---
title: "Azure CDN 習慣 aaaAnalyze |Microsoft 文件"
description: "您可以檢視您的 CDN 使用下列報表 hello 習慣： 頻寬、 傳輸資料，叫用、 快取狀態、 快取點擊率、 IPV4/IPV6 傳送的資料。"
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
ms.openlocfilehash: d27e6f60acaed66abb27d860c3a3e2e81c9f60cf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-azure-cdn-usage-patterns"></a><span data-ttu-id="221b5-103">分析 Azure CDN 使用模式</span><span class="sxs-lookup"><span data-stu-id="221b5-103">Analyze Azure CDN usage patterns</span></span>

[!INCLUDE[cdn-verizon-only](../../includes/cdn-verizon-only.md)]

<span data-ttu-id="221b5-104">hello 指南會經歷 hello 步驟 tooview hello 核心報表透過 Verizon 設定檔的 hello 管理網站。</span><span class="sxs-lookup"><span data-stu-id="221b5-104">hello guide below goes through hello steps tooview hello core reports via hello Manage portal for Verizon profiles.</span></span> <span data-ttu-id="221b5-105">您也可以匯出核心分析資料 toostorage、 事件中心或 Verizon 和 Akamai 設定檔的記錄分析 (oms) [hello azure 入口網站透過](cdn-log-analysis.md)。</span><span class="sxs-lookup"><span data-stu-id="221b5-105">You may also export core analytics data toostorage, event hub, or log analytics (oms) for both Verizon and Akamai profiles [through hello azure portal](cdn-log-analysis.md).</span></span>

<span data-ttu-id="221b5-106">您可以檢視您的 CDN 使用 hello 遵循報表使用模式：</span><span class="sxs-lookup"><span data-stu-id="221b5-106">You can view usage patterns for your CDN using hello following reports:</span></span>

* <span data-ttu-id="221b5-107">頻寬</span><span class="sxs-lookup"><span data-stu-id="221b5-107">Bandwidth</span></span>
* <span data-ttu-id="221b5-108">傳輸的資料</span><span class="sxs-lookup"><span data-stu-id="221b5-108">Data Transferred</span></span>
* <span data-ttu-id="221b5-109">點擊</span><span class="sxs-lookup"><span data-stu-id="221b5-109">Hits</span></span>
* <span data-ttu-id="221b5-110">快取狀態</span><span class="sxs-lookup"><span data-stu-id="221b5-110">Cache Statuses</span></span>
* <span data-ttu-id="221b5-111">快取點擊率</span><span class="sxs-lookup"><span data-stu-id="221b5-111">Cache Hit Ratio</span></span>
* <span data-ttu-id="221b5-112">已轉送的 IPV4/IPV6 資料</span><span class="sxs-lookup"><span data-stu-id="221b5-112">IPV4/IPV6 Data Transferred</span></span>

## <a name="accessing-core-reports"></a><span data-ttu-id="221b5-113">存取核心報告</span><span class="sxs-lookup"><span data-stu-id="221b5-113">Accessing Core Reports</span></span>
1. <span data-ttu-id="221b5-114">從 hello CDN 設定檔刀鋒視窗中，按一下 [hello**管理**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="221b5-114">From hello CDN profile blade, click hello **Manage** button.</span></span>
   
    ![[CDN 設定檔] 刀鋒視窗的 [管理] 按鈕](./media/cdn-reports/cdn-manage-btn.png)
   
    <span data-ttu-id="221b5-116">hello CDN 管理入口網站隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="221b5-116">hello CDN management portal opens.</span></span>
2. <span data-ttu-id="221b5-117">暫留在 hello**分析** 索引標籤，然後暫留在 hello**核心報告**彈出式視窗。</span><span class="sxs-lookup"><span data-stu-id="221b5-117">Hover over hello **Analytics** tab, then hover over hello **Core Reports** flyout.</span></span>  <span data-ttu-id="221b5-118">按一下想要的 hello hello 功能表中的報表。</span><span class="sxs-lookup"><span data-stu-id="221b5-118">Click on hello desired report in hello menu.</span></span>
   
    ![CDN 管理入口網站 - 核心報告功能表](./media/cdn-reports/cdn-core-reports.png)

## <a name="bandwidth"></a><span data-ttu-id="221b5-120">頻寬</span><span class="sxs-lookup"><span data-stu-id="221b5-120">Bandwidth</span></span>
<span data-ttu-id="221b5-121">hello 頻寬 」 報表所組成的 HTTP 和 HTTPS 指出 hello 頻寬使用量，透過在特定時間週期圖表及資料表。</span><span class="sxs-lookup"><span data-stu-id="221b5-121">hello bandwidth report consists of a graph and data table indicating hello bandwidth usage for HTTP and HTTPS over a particular time period.</span></span> <span data-ttu-id="221b5-122">您可以跨所有 CDN 快顯或特定的快顯檢視 hello 頻寬使用量。</span><span class="sxs-lookup"><span data-stu-id="221b5-122">You can view hello bandwidth usage across all CDN POPs or a particular POP.</span></span> <span data-ttu-id="221b5-123">這可讓您 tooview hello 流量尖峰和發佈，CDN 快顯中 Mbps 之間。</span><span class="sxs-lookup"><span data-stu-id="221b5-123">This allows you tooview hello traffic spikes and distribution across CDN POPs in Mbps.</span></span>

* <span data-ttu-id="221b5-124">從所有節點選取所有邊緣節點 toosee 流量，或從 hello 下拉式清單中選擇特定地區/節點。</span><span class="sxs-lookup"><span data-stu-id="221b5-124">Select All Edge Nodes toosee traffic from all nodes or choose a specific region/node from hello dropdown list.</span></span>
* <span data-ttu-id="221b5-125">選取日期範圍 tooview 資料此今天/週/本月等或輸入自訂的日期，然後按一下"go"toomake 確認已更新您的選擇。</span><span class="sxs-lookup"><span data-stu-id="221b5-125">Select Date range tooview data for today/this week/this month, etc. or enter custom dates, then click "go" toomake sure your selection is updated.</span></span>
* <span data-ttu-id="221b5-126">您可以匯出和 hello，即可下載 hello 資料的 excel 工作表圖示位於 下一步太"go 的"。</span><span class="sxs-lookup"><span data-stu-id="221b5-126">You can export and download hello data by clicking hello excel sheet icon located next too"go".</span></span>

<span data-ttu-id="221b5-127">hello 報表並更新每隔 5 分鐘。</span><span class="sxs-lookup"><span data-stu-id="221b5-127">hello report is updated every 5 minutes.</span></span>

![頻寬報告](./media/cdn-reports/cdn-bandwidth.png)

## <a name="data-transferred"></a><span data-ttu-id="221b5-129">傳輸的資料</span><span class="sxs-lookup"><span data-stu-id="221b5-129">Data transferred</span></span>
<span data-ttu-id="221b5-130">此報表包含指出的 HTTP 和 HTTPS 的 hello 流量使用方式，透過在特定時間週期的圖形和資料表格。</span><span class="sxs-lookup"><span data-stu-id="221b5-130">This report consists of a graph and data table indicating hello traffic usage for HTTP and HTTPS over a particular time period.</span></span> <span data-ttu-id="221b5-131">您可以跨所有 CDN 快顯或特定的快顯檢視 hello 流量使用方式。</span><span class="sxs-lookup"><span data-stu-id="221b5-131">You can view hello traffic usage across all CDN POPs or a particular POP.</span></span> <span data-ttu-id="221b5-132">這可讓您 tooview hello 流量尖峰和散發，透過 CDN 快顯以 gb 為單位。</span><span class="sxs-lookup"><span data-stu-id="221b5-132">This allows you tooview hello traffic spikes and distribution across CDN POPs in GB.</span></span>

* <span data-ttu-id="221b5-133">從所有的便箋中選取所有邊緣節點 toosee 流量，或從 hello 下拉式清單中選擇特定地區/節點。</span><span class="sxs-lookup"><span data-stu-id="221b5-133">Select All Edge Nodes toosee traffic from all notes or choose a specific region/node from hello dropdown list.</span></span>
* <span data-ttu-id="221b5-134">選取日期範圍 tooview 資料此今天/週/本月等或輸入自訂的日期，然後按一下"go"toomake 確認已更新您的選擇。</span><span class="sxs-lookup"><span data-stu-id="221b5-134">Select Date range tooview data for today/this week/this month, etc. or enter custom dates, then click "go" toomake sure your selection is updated.</span></span>
* <span data-ttu-id="221b5-135">您可以匯出和 hello，即可下載 hello 資料的 excel 工作表圖示位於 下一步太"go 的"。</span><span class="sxs-lookup"><span data-stu-id="221b5-135">You can export and download hello data by clicking hello excel sheet icon located next too"go" .</span></span>

<span data-ttu-id="221b5-136">hello 報表並更新每隔 5 分鐘。</span><span class="sxs-lookup"><span data-stu-id="221b5-136">hello report is updated every 5 minutes.</span></span>

![傳輸的資料報告](./media/cdn-reports/cdn-data-transferred.png)

## <a name="hits-status-codes"></a><span data-ttu-id="221b5-138">點擊 (狀態碼)</span><span class="sxs-lookup"><span data-stu-id="221b5-138">Hits (status codes)</span></span>
<span data-ttu-id="221b5-139">此報表說明 hello 發佈的要求狀態碼為您的內容。</span><span class="sxs-lookup"><span data-stu-id="221b5-139">This report describes hello distribution of request status codes for your content.</span></span> <span data-ttu-id="221b5-140">內容的每個要求都會產生 HTTP 狀態碼。</span><span class="sxs-lookup"><span data-stu-id="221b5-140">Every request for content will generate an HTTP status code.</span></span> <span data-ttu-id="221b5-141">hello 狀態碼說明邊緣快顯的 hello 要求的處理方式。</span><span class="sxs-lookup"><span data-stu-id="221b5-141">hello status code describes how edge POPs handled hello request.</span></span> <span data-ttu-id="221b5-142">例如，2xx 狀態碼表示該 hello 成功處理要求 tooa 用戶端，而 4xx 狀態碼表示發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="221b5-142">For example, 2xx status codes indicate that hello request was successfully served tooa client, while a 4xx status code indicates an error occurred.</span></span> <span data-ttu-id="221b5-143">如需 HTTP 狀態碼的詳細資料，請參閱 [狀態碼](https://en.wikipedia.org/wiki/List_of_HTTP_status_codes)。</span><span class="sxs-lookup"><span data-stu-id="221b5-143">For more details about HTTP status code, see [status codes](https://en.wikipedia.org/wiki/List_of_HTTP_status_codes).</span></span>

* <span data-ttu-id="221b5-144">選取日期範圍 tooview 資料此今天/週/本月等或輸入自訂的日期，然後按一下"go"toomake 確認已更新您的選擇。</span><span class="sxs-lookup"><span data-stu-id="221b5-144">Select Date range tooview data for today/this week/this month, etc. or enter custom dates, then click "go" toomake sure your selection is updated.</span></span>
* <span data-ttu-id="221b5-145">您可以匯出，而且按一下 hello 下載 hello 資料 excel 工作表位於接下來太"go 的"。</span><span class="sxs-lookup"><span data-stu-id="221b5-145">You can export and download hello data by clicking hello excel sheet located next too"go".</span></span>

![點擊報告](./media/cdn-reports/cdn-hits.png)

## <a name="cache-statuses"></a><span data-ttu-id="221b5-147">快取狀態</span><span class="sxs-lookup"><span data-stu-id="221b5-147">Cache statuses</span></span>
<span data-ttu-id="221b5-148">此報表說明 hello 發佈的快取命中和快取遺漏憑藉 「 用戶端要求。</span><span class="sxs-lookup"><span data-stu-id="221b5-148">This report describes hello distribution of cache hits and cache misses for client request.</span></span> <span data-ttu-id="221b5-149">Hello 最快的效能來自快取叫用，因為可以最佳化資料傳送速度降至最低的快取遺漏和過期的快取點擊率。</span><span class="sxs-lookup"><span data-stu-id="221b5-149">Since hello fastest performance comes from cache hits, you can optimize data delivery speeds by minimizing cache misses and expired cache hits.</span></span> <span data-ttu-id="221b5-150">設定您指定 「 無快取 」 回應標頭的來源伺服器 tooavoid，避免在絕對必要，但快取查詢字串並避免非快取的回應碼，可能會降低快取遺漏。</span><span class="sxs-lookup"><span data-stu-id="221b5-150">Cache misses can be reduced by configuring your origin server tooavoid assigning "no-cache" response headers, by avoiding query-string caching except where strictly needed, and by avoiding non-cacheable response codes.</span></span> <span data-ttu-id="221b5-151">過期的快取點擊可以避免藉由將資產的最大存留期，只要可能 toominimize hello 要求 toohello 原始伺服器的數目。</span><span class="sxs-lookup"><span data-stu-id="221b5-151">Expired cache hits can be avoided by making an asset's max-age as long as possible toominimize hello number of requests toohello origin server.</span></span>

![快取狀態報告](./media/cdn-reports/cdn-cache-statuses.png)

### <a name="main-cache-statuses-include"></a><span data-ttu-id="221b5-153">主要的快取狀態包括：</span><span class="sxs-lookup"><span data-stu-id="221b5-153">Main cache statuses include:</span></span>
* <span data-ttu-id="221b5-154">TCP_HIT：從邊緣提供。</span><span class="sxs-lookup"><span data-stu-id="221b5-154">TCP_HIT: Served from Edge.</span></span> <span data-ttu-id="221b5-155">hello 物件已快取中，而且不超過最大期限。</span><span class="sxs-lookup"><span data-stu-id="221b5-155">hello object was in cache and had not exceeded its max-age.</span></span>
* <span data-ttu-id="221b5-156">TCP_MISS：從來源提供。</span><span class="sxs-lookup"><span data-stu-id="221b5-156">TCP_MISS: Served from Origin.</span></span> <span data-ttu-id="221b5-157">hello 物件不在快取中，hello 回應後 tooorigin。</span><span class="sxs-lookup"><span data-stu-id="221b5-157">hello object was not in cache and hello response was back tooorigin.</span></span>
* <span data-ttu-id="221b5-158">TCP_EXPIRED _MISS：利用來源重新驗證之後從來源提供。</span><span class="sxs-lookup"><span data-stu-id="221b5-158">TCP_EXPIRED _MISS: Served from origin after revalidation with origin.</span></span> <span data-ttu-id="221b5-159">hello 物件已快取中，但已超過其最大存留期。</span><span class="sxs-lookup"><span data-stu-id="221b5-159">hello object was in cache but had exceeded its max-age.</span></span> <span data-ttu-id="221b5-160">重新驗證與來源產生要取代原始的新回應 hello 快取物件。</span><span class="sxs-lookup"><span data-stu-id="221b5-160">A revalidation with origin resulted in hello cache object being replaced by a new response from origin.</span></span>
* <span data-ttu-id="221b5-161">TCP_EXPIRED _HIT：利用來源重新驗證之後從邊緣提供。</span><span class="sxs-lookup"><span data-stu-id="221b5-161">TCP_EXPIRED _HIT: Served from Edge after revalidation with origin.</span></span> <span data-ttu-id="221b5-162">hello 物件已快取中，但已超過其最大存留期。</span><span class="sxs-lookup"><span data-stu-id="221b5-162">hello object was in cache but had exceeded its max-age.</span></span> <span data-ttu-id="221b5-163">Hello 來源伺服器重新驗證會導致不想要修改的 hello 快取物件。</span><span class="sxs-lookup"><span data-stu-id="221b5-163">A revalidation with hello origin server resulted in hello cache object being unmodified.</span></span>
* <span data-ttu-id="221b5-164">選取日期範圍 tooview 資料此今天/週/本月等或輸入自訂的日期，然後按一下"go"toomake 確認已更新您的選擇。</span><span class="sxs-lookup"><span data-stu-id="221b5-164">Select Date range tooview data for today/this week/this month, etc. or enter custom dates, then click "go" toomake sure your selection is updated.</span></span>
* <span data-ttu-id="221b5-165">您可以匯出和 hello，即可下載 hello 資料的 excel 工作表圖示位於 下一步太"go 的"。</span><span class="sxs-lookup"><span data-stu-id="221b5-165">You can export and download hello data by clicking hello excel sheet icon located next too"go".</span></span>

### <a name="full-list-of-cache-statuses"></a><span data-ttu-id="221b5-166">快取狀態的完整清單</span><span class="sxs-lookup"><span data-stu-id="221b5-166">Full list of cache statuses</span></span>
* <span data-ttu-id="221b5-167">TCP_HIT-這個狀態報告時直接從 hello POP toohello 用戶端處理要求。</span><span class="sxs-lookup"><span data-stu-id="221b5-167">TCP_HIT - This status is reported when a request is served directly from hello POP toohello client.</span></span> <span data-ttu-id="221b5-168">從快顯當 hello POP 最接近 toohello 用戶端上快取，並且具有有效的存留時間或 TTL 立即提供資產。</span><span class="sxs-lookup"><span data-stu-id="221b5-168">An asset is immediately served from a POP when it is cached on hello POP closest toohello client and it has a valid time-to-live, or TTL.</span></span> <span data-ttu-id="221b5-169">TTL 取決於下列回應標頭的 hello:</span><span class="sxs-lookup"><span data-stu-id="221b5-169">TTL is determined by hello following response headers:</span></span>
  
  * <span data-ttu-id="221b5-170">Cache-Control: s-maxage</span><span class="sxs-lookup"><span data-stu-id="221b5-170">Cache-Control: s-maxage</span></span>
  * <span data-ttu-id="221b5-171">Cache-Control: max-age</span><span class="sxs-lookup"><span data-stu-id="221b5-171">Cache-Control: max-age</span></span>
  * <span data-ttu-id="221b5-172">Expires</span><span class="sxs-lookup"><span data-stu-id="221b5-172">Expires</span></span>
* <span data-ttu-id="221b5-173">TCP_MISS-這個狀態表示 hello 要求資產的快取的版本已找不到的 hello POP 最接近 toohello 用戶端上。</span><span class="sxs-lookup"><span data-stu-id="221b5-173">TCP_MISS - This status indicates that a cached version of hello requested asset was not found on hello POP closest toohello client.</span></span> <span data-ttu-id="221b5-174">hello 資產將會從來源伺服器或原始保護盾伺服器要求。</span><span class="sxs-lookup"><span data-stu-id="221b5-174">hello asset will be requested from either an origin server or an origin shield server.</span></span> <span data-ttu-id="221b5-175">如果 hello 原始伺服器或 hello 原始保護盾伺服器傳回資產，它會提供 toohello 用戶端和快取 hello 用戶端和 hello 邊緣伺服器。</span><span class="sxs-lookup"><span data-stu-id="221b5-175">If hello origin server or hello origin shield server returns an asset, it will be served toohello client and cached on both hello client and hello edge server.</span></span> <span data-ttu-id="221b5-176">否則，將會傳回非 200 狀態碼 (例如，403 禁止，404 找不到等)。</span><span class="sxs-lookup"><span data-stu-id="221b5-176">Otherwise, a non-200 status code (e.g., 403 Forbidden, 404 Not Found, etc.) will be returned.</span></span>
* <span data-ttu-id="221b5-177">TCP_EXPIRED _HIT-這個狀態報告目標 ttl 過期，例如當 hello 資產的最大存留期已到期，資產的要求已由提供直接從 hello POP toohello 用戶端時。</span><span class="sxs-lookup"><span data-stu-id="221b5-177">TCP_EXPIRED _HIT -  This status is reported when a request that targeted an asset with an expired TTL, such as when hello asset's max-age has expired, was served directly from hello POP toohello client.</span></span>
  
    <span data-ttu-id="221b5-178">過期的要求通常會導致重新驗證要求 toohello 原始伺服器。</span><span class="sxs-lookup"><span data-stu-id="221b5-178">An expired request typically results in a revalidation request toohello origin server.</span></span> <span data-ttu-id="221b5-179">為了讓 TCP_EXPIRED _HIT toooccur，hello 原始伺服器必須指出較新版的 hello 資產不存在。</span><span class="sxs-lookup"><span data-stu-id="221b5-179">In order for a TCP_EXPIRED _HIT toooccur, hello origin server must indicate that a newer version of hello asset does not exist.</span></span> <span data-ttu-id="221b5-180">這種情況通常會更新該資產的 Cache-Control 和 Expires 標頭。</span><span class="sxs-lookup"><span data-stu-id="221b5-180">This type of situation will typically update that asset's Cache-Control and Expires headers.</span></span>
* <span data-ttu-id="221b5-181">TCP_EXPIRED _MISS-這個狀態報告時從 hello POP toohello 用戶端提供較新版本已過期的快取資產。</span><span class="sxs-lookup"><span data-stu-id="221b5-181">TCP_EXPIRED _MISS - This status is reported when a newer version of an expired cached asset is served from hello POP toohello client.</span></span> <span data-ttu-id="221b5-182">快取資產 hello TTL 已經過期時，發生這種的情況 （例如過期保留時間上限） 和 hello 來源伺服器會傳回該資產的較新版本。</span><span class="sxs-lookup"><span data-stu-id="221b5-182">This occurs when hello TTL for a cached asset has expired (e.g., expired max-age) and hello origin server returns a newer version of that asset.</span></span> <span data-ttu-id="221b5-183">這個新版本的 hello 資產將會服務 toohello 用戶端，而不是 hello 快取版本。</span><span class="sxs-lookup"><span data-stu-id="221b5-183">This new version of hello asset will be served toohello client instead of hello cached version.</span></span> <span data-ttu-id="221b5-184">此外，它將會快取 hello 邊緣伺服器與 hello 用戶端。</span><span class="sxs-lookup"><span data-stu-id="221b5-184">Additionally, it will be cached on hello edge server and hello client.</span></span>
* <span data-ttu-id="221b5-185">CONFIG_NOCACHE-這個狀態表示客戶專屬的組態，在我們的邊緣快顯，導致無法快取的 hello 資產。</span><span class="sxs-lookup"><span data-stu-id="221b5-185">CONFIG_NOCACHE - This status indicates that a customer-specific configuration on our edge POP prevented hello asset from being cached.</span></span>
* <span data-ttu-id="221b5-186">NONE - 這個狀態指出快取內容的有效性檢查並未執行。</span><span class="sxs-lookup"><span data-stu-id="221b5-186">NONE - This status indicates that a cache content freshness check was not performed.</span></span>
* <span data-ttu-id="221b5-187">TCP_ CLIENT_REFRESH _MISS-HTTP 用戶端 （例如瀏覽器） 強制執行從 hello 原始伺服器的邊緣 POP tooretrieve 過時資產的新版本時，此狀態的報告。</span><span class="sxs-lookup"><span data-stu-id="221b5-187">TCP_ CLIENT_REFRESH _MISS - This status is reported when an HTTP client (e.g., browser) forces an edge POP tooretrieve a new version of a stale asset from hello origin server.</span></span>
  
    <span data-ttu-id="221b5-188">根據預設，我們的伺服器可以防止 HTTP 用戶端在從 hello 原始伺服器強制我們的邊緣伺服器 tooretrieve hello 資產的新版本。</span><span class="sxs-lookup"><span data-stu-id="221b5-188">By default, our servers prevent an HTTP client from forcing our edge servers tooretrieve a new version of hello asset from hello origin server.</span></span>
* <span data-ttu-id="221b5-189">TCP_ PARTIAL_HIT - 當位元組範圍要求導致部分快取資產的點擊時，就會傳回此狀態。</span><span class="sxs-lookup"><span data-stu-id="221b5-189">TCP_ PARTIAL_HIT - This status is reported when a byte range request results in a hit for a partially cached asset.</span></span> <span data-ttu-id="221b5-190">hello 要求立即從 hello POP toohello 用戶端提供的位元組範圍。</span><span class="sxs-lookup"><span data-stu-id="221b5-190">hello requested byte range is immediately served from hello POP toohello client.</span></span>
* <span data-ttu-id="221b5-191">快取-資產的快取控制項和 Expires 標頭指出，它應該不會快取彈出或 hello HTTP 用戶端時，會報告此狀態。</span><span class="sxs-lookup"><span data-stu-id="221b5-191">UNCACHEABLE - This status is reported when an asset's Cache-Control and Expires headers indicate that it should not be cached on a POP or by hello HTTP client.</span></span> <span data-ttu-id="221b5-192">這些類型的要求被由 hello 原始伺服器</span><span class="sxs-lookup"><span data-stu-id="221b5-192">These types of requests are served from hello origin server</span></span>

## <a name="cache-hit-ratio"></a><span data-ttu-id="221b5-193">快取點擊率</span><span class="sxs-lookup"><span data-stu-id="221b5-193">Cache Hit Ratio</span></span>
<span data-ttu-id="221b5-194">此報表指出 hello 直接從快取服務的快取要求百分比。</span><span class="sxs-lookup"><span data-stu-id="221b5-194">This report indicates hello percentage of cached requests that were served directly from cache.</span></span>

<span data-ttu-id="221b5-195">hello 報表會提供下列詳細資料的 hello:</span><span class="sxs-lookup"><span data-stu-id="221b5-195">hello report provides hello following details:</span></span>

* <span data-ttu-id="221b5-196">hello 要求上 hello POP 最接近 toohello 要求者已快取內容。</span><span class="sxs-lookup"><span data-stu-id="221b5-196">hello requested content was cached on hello POP closest toohello requester.</span></span>
* <span data-ttu-id="221b5-197">直接從 hello 網路邊緣的我們處理 hello 要求。</span><span class="sxs-lookup"><span data-stu-id="221b5-197">hello request was served directly from hello edge of our network.</span></span>
* <span data-ttu-id="221b5-198">hello 要求不需要重新驗證與 hello 原始伺服器。</span><span class="sxs-lookup"><span data-stu-id="221b5-198">hello request did not require revalidation with hello origin server.</span></span>

<span data-ttu-id="221b5-199">hello 報表不包含：</span><span class="sxs-lookup"><span data-stu-id="221b5-199">hello report doesn't include:</span></span>

* <span data-ttu-id="221b5-200">拒絕由於 toocountry 篩選選項的要求。</span><span class="sxs-lookup"><span data-stu-id="221b5-200">Requests that are denied due toocountry filtering options.</span></span>
* <span data-ttu-id="221b5-201">資產的要求，其標頭指出他們不應該快取。</span><span class="sxs-lookup"><span data-stu-id="221b5-201">Requests for assets whose headers indicate that they should not be cached.</span></span> <span data-ttu-id="221b5-202">例如，Cache-Control: private、Cache-Control: no-cache 或 Pragma: no-cache 等標頭會防止資產被快取。</span><span class="sxs-lookup"><span data-stu-id="221b5-202">For example, Cache-Control: private, Cache-Control: no-cache, or Pragma: no-cache headers will prevent an asset from being cached.</span></span>
* <span data-ttu-id="221b5-203">部分快取內容的位元組範圍要求。</span><span class="sxs-lookup"><span data-stu-id="221b5-203">Byte range requests for partially cached content.</span></span>

<span data-ttu-id="221b5-204">hello 公式是: (TCP_ 點擊 / (TCP_ 叫用 + TCP_MISS)) * 100</span><span class="sxs-lookup"><span data-stu-id="221b5-204">hello formula is: (TCP_ HIT/(TCP_ HIT+TCP_MISS))*100</span></span>

* <span data-ttu-id="221b5-205">選取日期範圍 tooview 資料此今天/週/本月等或輸入自訂的日期，然後按一下"go"toomake 確認已更新您的選擇。</span><span class="sxs-lookup"><span data-stu-id="221b5-205">Select Date range tooview data for today/this week/this month, etc. or enter custom dates, then click "go" toomake sure your selection is updated.</span></span>
* <span data-ttu-id="221b5-206">您可以匯出和 hello，即可下載 hello 資料的 excel 工作表圖示位於 下一步太"go 的"。</span><span class="sxs-lookup"><span data-stu-id="221b5-206">You can export and download hello data by clicking hello excel sheet icon located next too"go" .</span></span>

![快取點擊率報告](./media/cdn-reports/cdn-cache-hit-ratio.png)

## <a name="ipv4ipv6-data-transferred"></a><span data-ttu-id="221b5-208">已轉送的 IPV4/IPV6 資料</span><span class="sxs-lookup"><span data-stu-id="221b5-208">IPV4/IPV6 Data transferred</span></span>
<span data-ttu-id="221b5-209">此報告會顯示 hello 流量使用分布在 IPV4 與 IPV6。</span><span class="sxs-lookup"><span data-stu-id="221b5-209">This report shows hello traffic usage distribution in IPV4 vs IPV6.</span></span>

![已轉送的 IPV4/IPV6 資料](./media/cdn-reports/cdn-ipv4-ipv6.png)

* <span data-ttu-id="221b5-211">選取此今天/週/本月份日期範圍 tooview 資料等，或輸入自訂的日期。</span><span class="sxs-lookup"><span data-stu-id="221b5-211">Select Date range tooview data for today/this week/this month, etc. or enter custom dates.</span></span>
* <span data-ttu-id="221b5-212">然後，按一下"go"toomake 確認已更新您的選擇。</span><span class="sxs-lookup"><span data-stu-id="221b5-212">Then, click "go" toomake sure your selection is updated.</span></span>

## <a name="considerations"></a><span data-ttu-id="221b5-213">考量</span><span class="sxs-lookup"><span data-stu-id="221b5-213">Considerations</span></span>
<span data-ttu-id="221b5-214">報表只能產生 hello 內最後一個 18 個月。</span><span class="sxs-lookup"><span data-stu-id="221b5-214">Reports can only be generated within hello last 18 months.</span></span>

