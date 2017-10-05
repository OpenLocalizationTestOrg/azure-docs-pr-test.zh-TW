---
title: "透過 Azure 內容傳遞網路的媒體串流處理最佳化"
description: "將串流媒體檔案最佳化以便傳遞順暢"
services: cdn
documentationcenter: 
author: smcevoy
manager: erikre
editor: 
ms.assetid: 
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: v-semcev
ms.openlocfilehash: 1221f4f50b8b9c4b9f9f88be4d04a65375c36062
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="media-streaming-optimization-via-the-azure-content-delivery-network"></a><span data-ttu-id="7c613-103">透過 Azure 內容傳遞網路的媒體串流處理最佳化</span><span class="sxs-lookup"><span data-stu-id="7c613-103">Media streaming optimization via the Azure Content Delivery Network</span></span> 
 
<span data-ttu-id="7c613-104">網際網路使用高畫質影片的日益頻繁，造成有效率傳遞大型檔案的困難。</span><span class="sxs-lookup"><span data-stu-id="7c613-104">Use of high-definition video is increasing on the Internet, which creates difficulties for efficient delivery of large files.</span></span> <span data-ttu-id="7c613-105">客戶期待在世界各地的各種網路和用戶端上順暢播放點播視訊或即時影片資產。</span><span class="sxs-lookup"><span data-stu-id="7c613-105">Customers expect smooth playback of video on demand or live video assets on a variety of networks and clients all over the world.</span></span> <span data-ttu-id="7c613-106">快速且有效的媒體串流檔案傳遞機制，對於確保順暢且愉悅的取用者體驗極為重要。</span><span class="sxs-lookup"><span data-stu-id="7c613-106">A fast and efficient delivery mechanism for media streaming files is critical to ensure a smooth and enjoyable consumer experience.</span></span>  

<span data-ttu-id="7c613-107">即時串流處理媒體特別難傳遞，因為有大量的並行檢視者取用大型檔案。</span><span class="sxs-lookup"><span data-stu-id="7c613-107">Live streaming media is especially difficult to deliver because of the large sizes and number of concurrent viewers.</span></span> <span data-ttu-id="7c613-108">長時間延遲造成使用者出走。</span><span class="sxs-lookup"><span data-stu-id="7c613-108">Long delays cause users to leave.</span></span> <span data-ttu-id="7c613-109">因為即時串流無法預先進行快取，而且檢視者無法接受長時間延遲，因此必須及時傳遞影片片段。</span><span class="sxs-lookup"><span data-stu-id="7c613-109">Because live streams can't be cached ahead of time and large latencies aren't acceptable to viewers, video fragments must be delivered in a timely manner.</span></span> 

<span data-ttu-id="7c613-110">串流的要求模式也帶來一些新挑戰。</span><span class="sxs-lookup"><span data-stu-id="7c613-110">The request patterns of streaming also provide some new challenges.</span></span> <span data-ttu-id="7c613-111">當熱門的即時串流，或點播視訊發佈新的片段時，同一時間可能有數千到數百萬個檢視者要求資料流。</span><span class="sxs-lookup"><span data-stu-id="7c613-111">When a popular live stream or a new series is released for video on demand, thousands to millions of viewers might request the stream at the same time.</span></span> <span data-ttu-id="7c613-112">在此情況下，智慧要求彙總極為重要，因為在尚未快取資產時，它不會讓原始伺服器超過負荷。</span><span class="sxs-lookup"><span data-stu-id="7c613-112">In this case, smart request consolidation is vital to not overwhelm the origin servers when the assets aren't cached yet.</span></span>
 
<span data-ttu-id="7c613-113">Akamai 的 Azure 內容傳遞網路現在提供一項功能，可將串流處理媒體資產有效傳遞給全球的使用者。</span><span class="sxs-lookup"><span data-stu-id="7c613-113">The Azure Content Delivery Network from Akamai now offers a feature that delivers streaming media assets efficiently to users across the globe at scale.</span></span> <span data-ttu-id="7c613-114">此功能會減少延遲，因為它可以降低來源伺服器上的負載。</span><span class="sxs-lookup"><span data-stu-id="7c613-114">The feature reduces latencies because it reduces the load on the origin servers.</span></span> <span data-ttu-id="7c613-115">使用標準 Akamai 定價層可取得這項功能。</span><span class="sxs-lookup"><span data-stu-id="7c613-115">This feature is available with the Standard Akamai pricing tier.</span></span> 

<span data-ttu-id="7c613-116">Verizon 的 Azure 內容傳遞網路會直接使用一般 Web 傳遞最佳化類型來傳遞串流處理媒體內容。</span><span class="sxs-lookup"><span data-stu-id="7c613-116">The Azure Content Delivery Network from Verizon delivers streaming media directly in the general web delivery optimization type.</span></span>
 
## <a name="configure-an-endpoint-to-optimize-media-streaming-in-the-azure-content-delivery-network-from-akamai"></a><span data-ttu-id="7c613-117">在 Akamai 的 Azure 內容傳遞網路中，設定端點以最佳化媒體串流處理。</span><span class="sxs-lookup"><span data-stu-id="7c613-117">Configure an endpoint to optimize media streaming in the Azure Content Delivery Network from Akamai</span></span>
 
<span data-ttu-id="7c613-118">您可以設定您的內容傳遞網路 (CDN) 端點，以最佳化透過 Azure 入口網站傳遞大型檔案。</span><span class="sxs-lookup"><span data-stu-id="7c613-118">You can configure your content delivery network (CDN) endpoint to optimize delivery for large files via the Azure portal.</span></span> <span data-ttu-id="7c613-119">若要這樣做，您也可以使用 REST API 或任何用戶端 SDK。</span><span class="sxs-lookup"><span data-stu-id="7c613-119">You can also use our REST APIs or any of the client SDKs to do this.</span></span> <span data-ttu-id="7c613-120">下列步驟示範透過 Azure 入口網站的程序：</span><span class="sxs-lookup"><span data-stu-id="7c613-120">The following steps show the process via the Azure portal:</span></span>

1. <span data-ttu-id="7c613-121">若要新增新的端點，請在 [CDN 設定檔] 頁面上選取 [端點]。</span><span class="sxs-lookup"><span data-stu-id="7c613-121">To add a new endpoint, on the **CDN profile** page, select **Endpoint**.</span></span>
  
    ![新增端點](./media/cdn-media-streaming-optimization/01_Adding.png)

2. <span data-ttu-id="7c613-123">在 [最佳化對象] 下拉式清單中，為點播視訊資產選取 [點播視訊媒體串流]。</span><span class="sxs-lookup"><span data-stu-id="7c613-123">In the **Optimized for** drop-down list, select **Video on demand media streaming** for video-on-demand assets.</span></span> <span data-ttu-id="7c613-124">如果您結合即時和點播視訊串流處理，請選取 [General media streaming] \(一般媒體串流處理)。</span><span class="sxs-lookup"><span data-stu-id="7c613-124">If you do a combination of live and video-on-demand streaming, select **General media streaming**.</span></span>

    ![選取的串流](./media/cdn-media-streaming-optimization/02_Creating.png) 
 
<span data-ttu-id="7c613-126">建立端點後，最佳化就會套用到符合特定準則的所有檔案。</span><span class="sxs-lookup"><span data-stu-id="7c613-126">After you create the endpoint, it applies the optimization for all files that match certain criteria.</span></span> <span data-ttu-id="7c613-127">下一節會說明此程序。</span><span class="sxs-lookup"><span data-stu-id="7c613-127">The following section describes this process.</span></span> 
 
## <a name="media-streaming-optimizations-for-the-azure-content-delivery-network-from-akamai"></a><span data-ttu-id="7c613-128">來自 Akamai 的 Azure 內容傳遞網路的媒體串流處理最佳化</span><span class="sxs-lookup"><span data-stu-id="7c613-128">Media streaming optimizations for the Azure Content Delivery Network from Akamai</span></span>
 
<span data-ttu-id="7c613-129">來自 Akamai 的媒體串流處理最佳化，適合使用媒體片段傳遞處理即時或點播視訊串流的媒體。</span><span class="sxs-lookup"><span data-stu-id="7c613-129">Media streaming optimization from Akamai is effective for live or video-on-demand streaming media that uses individual media fragments for delivery.</span></span> <span data-ttu-id="7c613-130">此程序不同於透過漸進式下載或使用位元組範圍要求的單一大型資產傳輸。</span><span class="sxs-lookup"><span data-stu-id="7c613-130">This process is different from a single large asset transferred via progressive download or by using byte-range requests.</span></span> <span data-ttu-id="7c613-131">如需該樣式的媒體傳遞相關資訊，請查看[大型檔案最佳化](cdn-large-file-optimization.md)。</span><span class="sxs-lookup"><span data-stu-id="7c613-131">For information on that style of media delivery, see [Large file optimization](cdn-large-file-optimization.md).</span></span>


<span data-ttu-id="7c613-132">一般媒體傳遞或點播視訊媒體傳遞最佳化類型，會使用 CDN 與後端最佳化以更快傳遞媒體資產。</span><span class="sxs-lookup"><span data-stu-id="7c613-132">The general media delivery or video-on-demand media delivery optimization types use a CDN with back-end optimizations to deliver media assets faster.</span></span> <span data-ttu-id="7c613-133">它們也會使用媒體資產組態，此組態是以經過一段時間學習的最佳作法為基礎。</span><span class="sxs-lookup"><span data-stu-id="7c613-133">They also use configurations for media assets based on best practices learned over time.</span></span>

### <a name="caching"></a><span data-ttu-id="7c613-134">快取</span><span class="sxs-lookup"><span data-stu-id="7c613-134">Caching</span></span>

<span data-ttu-id="7c613-135">如果 Akamai 的 Azure 內容傳遞網路偵測到資產是串流資訊清單或片段，它會使用與一般 Web 傳遞不同的快取到期時間。</span><span class="sxs-lookup"><span data-stu-id="7c613-135">If the Azure Content Delivery Network from Akamai detects that the asset is a streaming manifest or fragment, it uses different caching expiration times from general web delivery.</span></span> <span data-ttu-id="7c613-136">(請參閱下表中的完整清單。)如往常一樣接受從來源傳送的 cache-control 或 Expires 標頭。</span><span class="sxs-lookup"><span data-stu-id="7c613-136">(See the full list in the following table.) As always, cache-control or Expires headers sent from the origin are honored.</span></span> <span data-ttu-id="7c613-137">如果資產不是媒體資產，就會使用一般 Web 傳遞的逾期時間快取。</span><span class="sxs-lookup"><span data-stu-id="7c613-137">If the asset is not a media asset, it caches by using the expiration times for general web delivery.</span></span>

<span data-ttu-id="7c613-138">當許多使用者要求還不存在的片段時，短的負快取時間對來源卸載就很有用。</span><span class="sxs-lookup"><span data-stu-id="7c613-138">The short negative caching time is useful for origin offload when many users request a fragment that doesn’t exist yet.</span></span> <span data-ttu-id="7c613-139">例如該秒無法從原始伺服器取得封包的即時串流。</span><span class="sxs-lookup"><span data-stu-id="7c613-139">An example is a live stream where the packets aren't available from the origin that second.</span></span> <span data-ttu-id="7c613-140">較長的快取間隔也有助於卸載原始伺服器的要求，因為通常不會修改影片內容。</span><span class="sxs-lookup"><span data-stu-id="7c613-140">The longer caching interval also helps offload requests from the origin because video content isn't typically modified.</span></span>
 

|    | <span data-ttu-id="7c613-141">一般</span><span class="sxs-lookup"><span data-stu-id="7c613-141">General</span></span><br> <span data-ttu-id="7c613-142">Web</span><span class="sxs-lookup"><span data-stu-id="7c613-142">web</span></span><br><span data-ttu-id="7c613-143">偵錯</span><span class="sxs-lookup"><span data-stu-id="7c613-143">delivery</span></span> | <span data-ttu-id="7c613-144">一般</span><span class="sxs-lookup"><span data-stu-id="7c613-144">General</span></span><br> <span data-ttu-id="7c613-145">媒體</span><span class="sxs-lookup"><span data-stu-id="7c613-145">media</span></span><br> <span data-ttu-id="7c613-146">串流</span><span class="sxs-lookup"><span data-stu-id="7c613-146">streaming</span></span> | <span data-ttu-id="7c613-147">點播視訊</span><span class="sxs-lookup"><span data-stu-id="7c613-147">Video-on-demand</span></span> <br><span data-ttu-id="7c613-148">媒體</span><span class="sxs-lookup"><span data-stu-id="7c613-148">media</span></span><br> <span data-ttu-id="7c613-149">串流</span><span class="sxs-lookup"><span data-stu-id="7c613-149">streaming</span></span>  
--- | --- | --- | ---
<span data-ttu-id="7c613-150">快取：正向</span><span class="sxs-lookup"><span data-stu-id="7c613-150">Caching: Positive</span></span> <br> <span data-ttu-id="7c613-151">HTTP 200、203、300、</span><span class="sxs-lookup"><span data-stu-id="7c613-151">HTTP 200, 203, 300,</span></span> <br> <span data-ttu-id="7c613-152">301、302 和 410</span><span class="sxs-lookup"><span data-stu-id="7c613-152">301, 302, and 410</span></span> | <span data-ttu-id="7c613-153">7 天</span><span class="sxs-lookup"><span data-stu-id="7c613-153">7 days</span></span> |<span data-ttu-id="7c613-154">365 天</span><span class="sxs-lookup"><span data-stu-id="7c613-154">365 days</span></span> | <span data-ttu-id="7c613-155">365 天</span><span class="sxs-lookup"><span data-stu-id="7c613-155">365 days</span></span>   
<span data-ttu-id="7c613-156">快取：負向</span><span class="sxs-lookup"><span data-stu-id="7c613-156">Caching: Negative</span></span> <br> <span data-ttu-id="7c613-157">HTTP 204、305、404</span><span class="sxs-lookup"><span data-stu-id="7c613-157">HTTP 204, 305, 404,</span></span> <br> <span data-ttu-id="7c613-158">和 405</span><span class="sxs-lookup"><span data-stu-id="7c613-158">and 405</span></span> | <span data-ttu-id="7c613-159">None</span><span class="sxs-lookup"><span data-stu-id="7c613-159">None</span></span> | <span data-ttu-id="7c613-160">1 秒</span><span class="sxs-lookup"><span data-stu-id="7c613-160">1 second</span></span> | <span data-ttu-id="7c613-161">1 秒</span><span class="sxs-lookup"><span data-stu-id="7c613-161">1 second</span></span>
 
### <a name="deal-with-origin-failure"></a><span data-ttu-id="7c613-162">處理原始伺服器失敗</span><span class="sxs-lookup"><span data-stu-id="7c613-162">Deal with origin failure</span></span>  

<span data-ttu-id="7c613-163">一般媒體傳遞和點播視訊媒體傳遞也都有以典型要求模式的最佳做法為基礎的原始伺服器逾時和重試記錄。</span><span class="sxs-lookup"><span data-stu-id="7c613-163">General media delivery and video-on-demand media delivery also have origin time-out and a retry log based on best practices for typical request patterns.</span></span> <span data-ttu-id="7c613-164">例如，因為一般媒體傳遞適合即時和點播視訊媒體傳遞，所以會因為即時串流講求時效性而使用比較短的連線逾時。</span><span class="sxs-lookup"><span data-stu-id="7c613-164">For example, because general media delivery is for live and video-on-demand media delivery, it uses a shorter connection time-out due to the time-sensitive nature of live streaming.</span></span>

<span data-ttu-id="7c613-165">當連線逾時，CDN 會先重試幾次，再向用戶端傳送「504 - 閘道逾時」錯誤。</span><span class="sxs-lookup"><span data-stu-id="7c613-165">When a connection times out, the CDN retries a number of times before it sends a "504 - Gateway Timeout" error to the client.</span></span> 

<span data-ttu-id="7c613-166">當檔案符合檔案類型和大小條件清單，CDN 會使用媒體串流處理的行為。</span><span class="sxs-lookup"><span data-stu-id="7c613-166">When a file matches the file type and size conditions list, the CDN uses the behavior for media streaming.</span></span> <span data-ttu-id="7c613-167">否則，會使用一般 Web 傳遞。</span><span class="sxs-lookup"><span data-stu-id="7c613-167">Otherwise, it uses general web delivery.</span></span>
   
### <a name="conditions-for-media-streaming-optimization"></a><span data-ttu-id="7c613-168">媒體串流最佳化的條件</span><span class="sxs-lookup"><span data-stu-id="7c613-168">Conditions for media streaming optimization</span></span> 

<span data-ttu-id="7c613-169">下表列出媒體串流處理最佳化需要滿足的準則集合：</span><span class="sxs-lookup"><span data-stu-id="7c613-169">The following table lists the set of criteria to be satisfied for media streaming optimization:</span></span> 
 
<span data-ttu-id="7c613-170">支援的串流類型</span><span class="sxs-lookup"><span data-stu-id="7c613-170">Supported streaming types</span></span> | <span data-ttu-id="7c613-171">副檔名</span><span class="sxs-lookup"><span data-stu-id="7c613-171">File extensions</span></span>  
--- | ---  
<span data-ttu-id="7c613-172">Apple HLS</span><span class="sxs-lookup"><span data-stu-id="7c613-172">Apple HLS</span></span> | <span data-ttu-id="7c613-173">m3u8、m3u、m3ub、key、ts、aac</span><span class="sxs-lookup"><span data-stu-id="7c613-173">m3u8, m3u, m3ub, key, ts, aac</span></span>
<span data-ttu-id="7c613-174">Adobe HDS</span><span class="sxs-lookup"><span data-stu-id="7c613-174">Adobe HDS</span></span> | <span data-ttu-id="7c613-175">f4m、f4x、drmmeta、bootstrap、f4f、</span><span class="sxs-lookup"><span data-stu-id="7c613-175">f4m, f4x, drmmeta, bootstrap, f4f,</span></span><br><span data-ttu-id="7c613-176">Seg-Frag URL 結構</span><span class="sxs-lookup"><span data-stu-id="7c613-176">Seg-Frag URL structure</span></span> <br> <span data-ttu-id="7c613-177">(matching regex: ^(/.*)Seq(\d+)-Frag(\d+)</span><span class="sxs-lookup"><span data-stu-id="7c613-177">(matching regex: ^(/.*)Seq(\d+)-Frag(\d+)</span></span>
<span data-ttu-id="7c613-178">DASH</span><span class="sxs-lookup"><span data-stu-id="7c613-178">DASH</span></span> | <span data-ttu-id="7c613-179">mpd、dash、divx、ismv、m4s、m4v、mp4、mp4v、</span><span class="sxs-lookup"><span data-stu-id="7c613-179">mpd, dash, divx, ismv, m4s, m4v, mp4, mp4v,</span></span> <br> <span data-ttu-id="7c613-180">sidx、webm、mp4a、m4a、isma</span><span class="sxs-lookup"><span data-stu-id="7c613-180">sidx, webm, mp4a, m4a, isma</span></span>
<span data-ttu-id="7c613-181">Smooth Streaming</span><span class="sxs-lookup"><span data-stu-id="7c613-181">Smooth streaming</span></span> | <span data-ttu-id="7c613-182">/manifest/,/QualityLevels/Fragments/</span><span class="sxs-lookup"><span data-stu-id="7c613-182">/manifest/,/QualityLevels/Fragments/</span></span>
  

 
## <a name="media-streaming-optimizations-for-the-azure-content-delivery-network-from-verizon"></a><span data-ttu-id="7c613-183">Verizon 的 Azure 內容傳遞網路的媒體串流處理最佳化</span><span class="sxs-lookup"><span data-stu-id="7c613-183">Media streaming optimizations for the Azure Content Delivery Network from Verizon</span></span>

<span data-ttu-id="7c613-184">Verizon 的 Azure 內容傳遞網路會直接使用一般 Web 傳遞最佳化類型來傳遞串流處理媒體資產。</span><span class="sxs-lookup"><span data-stu-id="7c613-184">The Azure Content Delivery Network from Verizon delivers streaming media assets directly by using the general web delivery optimization type.</span></span> <span data-ttu-id="7c613-185">CDN 有一些功能預設可直接協助傳遞媒體資產。</span><span class="sxs-lookup"><span data-stu-id="7c613-185">A few features on the CDN directly assist in delivering media assets by default.</span></span>

### <a name="partial-cache-sharing"></a><span data-ttu-id="7c613-186">部分快取共用</span><span class="sxs-lookup"><span data-stu-id="7c613-186">Partial cache sharing</span></span>

<span data-ttu-id="7c613-187">部分快取共用，可讓 CDN 向新要求提供部分的快取內容。</span><span class="sxs-lookup"><span data-stu-id="7c613-187">Partial cache sharing allows the CDN to serve partially cached content to new requests.</span></span> <span data-ttu-id="7c613-188">例如，如果對 CDN 的第一個要求導致快取遺漏，該要求即會傳送到原始伺服器。</span><span class="sxs-lookup"><span data-stu-id="7c613-188">For example, if the first request to the CDN results in a cache miss, the request is sent to the origin.</span></span> <span data-ttu-id="7c613-189">雖然此不完整的內容會載入到 CDN 快取中，但是對 CDN 的其他要求可以開始取得此資料。</span><span class="sxs-lookup"><span data-stu-id="7c613-189">Although this incomplete content is loaded into the CDN cache, other requests to the CDN can start getting this data.</span></span> 

### <a name="cache-fill-wait-time"></a><span data-ttu-id="7c613-190">快取填滿等候時間</span><span class="sxs-lookup"><span data-stu-id="7c613-190">Cache fill wait time</span></span>

 <span data-ttu-id="7c613-191">快取填滿等候時間功能會強迫邊緣伺服器保存相同資源的所有後續要求，直到原始伺服器的 HTTP 回應標頭送達為止。</span><span class="sxs-lookup"><span data-stu-id="7c613-191">The cache fill wait time feature forces the edge server to hold any subsequent requests for the same resource until HTTP response headers arrive from the origin server.</span></span> <span data-ttu-id="7c613-192">如果原始伺服器的 HTTP 回應標頭在計時器終止前送達，則會在成長中快取之外為所有暫停的要求提供服務。</span><span class="sxs-lookup"><span data-stu-id="7c613-192">If HTTP response headers from the origin  arrive before the timer expires, all requests that were put on hold are served out of the growing cache.</span></span> <span data-ttu-id="7c613-193">同時，快取會填入原始伺服器的資料。</span><span class="sxs-lookup"><span data-stu-id="7c613-193">At the same time, the cache is filled by data from the origin.</span></span> <span data-ttu-id="7c613-194">根據預設，快取填滿等候時間會設定為 3,000 毫秒。</span><span class="sxs-lookup"><span data-stu-id="7c613-194">By default, the cache fill wait time is set to 3,000 milliseconds.</span></span> 

