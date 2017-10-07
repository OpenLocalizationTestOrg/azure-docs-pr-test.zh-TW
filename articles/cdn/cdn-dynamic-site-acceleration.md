---
title: "aaaDynamic 網站加速透過 Azure CDN"
description: "動態站台加速深入探討"
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
ms.date: 08/02/2017
ms.author: v-semcev
ms.openlocfilehash: 37e6312ae5e83448f2d87c95ef48c387355748bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="dynamic-site-acceleration-via-azure-cdn"></a><span data-ttu-id="0ce0f-103">透過 Azure CDN 進行動態網站加速</span><span class="sxs-lookup"><span data-stu-id="0ce0f-103">Dynamic Site Acceleration via Azure CDN</span></span>

<span data-ttu-id="0ce0f-104">社交媒體、 電子商務和 hello hyper-v 個人化 web hello 爆炸，快速增加的百分比表示 hello 內容提供 tooend 使用者即時產生。</span><span class="sxs-lookup"><span data-stu-id="0ce0f-104">With hello explosion of social media, electronic commerce, and hello hyper-personalized web, a rapidly increasing percentage of hello content served tooend users is generated in real time.</span></span> <span data-ttu-id="0ce0f-105">使用者期望獲得的快速、可靠且個人化 web 體驗，無關乎瀏覽器、位置、裝置或網路。</span><span class="sxs-lookup"><span data-stu-id="0ce0f-105">Users expect fast, reliable, and personalized web experiences, independent of their browser, location, device, or network.</span></span> <span data-ttu-id="0ce0f-106">不過，hello 非常創新，讓這些經驗也因此聘用緩慢頁面下載，而且 hello 經驗 hello 品質而面臨風險。</span><span class="sxs-lookup"><span data-stu-id="0ce0f-106">However, hello very innovations that make these experiences so engaging also slow page downloads and put hello quality of hello consumer experience at risk.</span></span> 

<span data-ttu-id="0ce0f-107">標準的 CDN 功能包含 hello 能力 toocache 檔案接近 tooend 使用者 toospeed 向上傳遞靜態檔案。</span><span class="sxs-lookup"><span data-stu-id="0ce0f-107">Standard CDN capability includes hello ability toocache files closer tooend users toospeed up delivery of static files.</span></span> <span data-ttu-id="0ce0f-108">不過，使用動態 web 應用程式，快取該內容中的邊緣位置無法 hello server 產生 hello 內容以回應 toouser 行為。</span><span class="sxs-lookup"><span data-stu-id="0ce0f-108">However, with dynamic web applications, caching that content in edge locations isn't possible because hello server generates hello content in response toouser behavior.</span></span> <span data-ttu-id="0ce0f-109">加速 hello 傳遞的這類內容比傳統的邊緣快取更為複雜，而且需要微調的每個項目從起始 toodelivery hello 整個資料路徑上的端對端解決方案。</span><span class="sxs-lookup"><span data-stu-id="0ce0f-109">Speeding up hello delivery of such content is more complex than traditional edge caching and requires an end-to-end solution that finely tunes each element along hello entire data path from inception toodelivery.</span></span> <span data-ttu-id="0ce0f-110">使用 Azure CDN 動態網站加速 (DSA)，hello 搭配動態內容的 web 網頁會適當地改善效能。</span><span class="sxs-lookup"><span data-stu-id="0ce0f-110">With Azure CDN Dynamic Site Acceleration (DSA), hello performance of web pages with dynamic content is measurably improved.</span></span>

<span data-ttu-id="0ce0f-111">從 Akamai 和 Verizon azure CDN 提供透過 hello 的 DSA 最佳化**適合**端點建立期間的功能表。</span><span class="sxs-lookup"><span data-stu-id="0ce0f-111">Azure CDN from Akamai and Verizon offers DSA optimization through hello **Optimized for** menu during endpoint creation.</span></span>

## <a name="configuring-cdn-endpoint-tooaccelerate-delivery-of-dynamic-files"></a><span data-ttu-id="0ce0f-112">設定 CDN 端點 tooaccelerate 傳遞動態檔案</span><span class="sxs-lookup"><span data-stu-id="0ce0f-112">Configuring CDN endpoint tooaccelerate delivery of dynamic files</span></span>

<span data-ttu-id="0ce0f-113">您可以設定您的 CDN 端點 toooptimize 傳遞的動態透過 Azure 入口網站的檔案選取 hello**動態站台加速**hello 下的選項**適合**時的屬性選項建立 hello 端點。</span><span class="sxs-lookup"><span data-stu-id="0ce0f-113">You can configure your CDN endpoint toooptimize delivery of dynamic files via Azure portal by selecting hello **Dynamic site acceleration** option under hello **Optimized for** property selection during hello endpoint creation.</span></span> <span data-ttu-id="0ce0f-114">您也可以使用我們的 REST Api，或任何 hello 用戶端 Sdk toodo hello 以程式設計的方式相同。</span><span class="sxs-lookup"><span data-stu-id="0ce0f-114">You can also use our REST APIs or any of hello client SDKs toodo hello same thing programmatically.</span></span> 

### <a name="probe-path"></a><span data-ttu-id="0ce0f-115">探查路徑</span><span class="sxs-lookup"><span data-stu-id="0ce0f-115">Probe path</span></span>
<span data-ttu-id="0ce0f-116">探查路徑是功能特定 tooDynamic 網站加速，因此需要建立一份有效。</span><span class="sxs-lookup"><span data-stu-id="0ce0f-116">Probe path is a feature specific tooDynamic Site Acceleration, and a valid one is required for creation.</span></span> <span data-ttu-id="0ce0f-117">DSA 使用小型*探查路徑*檔案放在 hello 原點 toooptimize 網路的路由設定 hello CDN。</span><span class="sxs-lookup"><span data-stu-id="0ce0f-117">DSA uses a small *probe path* file placed on hello origin toooptimize network routing configurations for hello CDN.</span></span> <span data-ttu-id="0ce0f-118">您可以下載和上傳我們的範例檔案 tooyour 網站，或使用現有的資產上您為約 10 KB hello 探查路徑改為 hello 資產存在的原點。</span><span class="sxs-lookup"><span data-stu-id="0ce0f-118">You can download and upload our sample file tooyour site, or use an existing asset on your origin that is roughly 10 KB for hello probe path instead if hello asset exists.</span></span>

> [!Note]
> <span data-ttu-id="0ce0f-119">DSA 會產生額外費用。</span><span class="sxs-lookup"><span data-stu-id="0ce0f-119">DSA incurs extra charges.</span></span> <span data-ttu-id="0ce0f-120">如需詳細資訊，請參閱 hello[定價頁面](https://azure.microsoft.com/pricing/details/cdn/)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="0ce0f-120">For more information, see hello [pricing page](https://azure.microsoft.com/pricing/details/cdn/) for more information.</span></span>

<span data-ttu-id="0ce0f-121">下列螢幕擷取畫面的 hello 說明 hello 程序，透過 Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="0ce0f-121">hello following screenshots illustrate hello process via Azure portal.</span></span>
 
![新增新的 CDN 端點](./media/cdn-dynamic-site-acceleration/01_Endpoint_Profile.png) 

<span data-ttu-id="0ce0f-123">*圖 1： 從 hello 的 CDN 設定檔中加入新的 CDN 端點*</span><span class="sxs-lookup"><span data-stu-id="0ce0f-123">*Figure 1: Adding a new CDN endpoint from hello CDN Profile*</span></span>
 
![使用 DSA 建立新的 CDN 端點](./media/cdn-dynamic-site-acceleration/02_Optimized_DSA.png)  

<span data-ttu-id="0ce0f-125">*圖 2：在已選取動態網站加速最佳化的情況下建立 CDN 端點*</span><span class="sxs-lookup"><span data-stu-id="0ce0f-125">*Figure 2: Creating a CDN Endpoint with Dynamic site acceleration Optimization selected*</span></span>

<span data-ttu-id="0ce0f-126">一旦建立 hello CDN 端點時，它適用於符合特定準則的所有檔案的 hello DSA 最佳化。</span><span class="sxs-lookup"><span data-stu-id="0ce0f-126">Once hello CDN endpoint is created, it applies hello DSA optimizations for all files that match certain criteria.</span></span> <span data-ttu-id="0ce0f-127">下列章節的 hello 描述 DSA 最佳化，在詳細資料。</span><span class="sxs-lookup"><span data-stu-id="0ce0f-127">hello following section describes DSA optimization in detail.</span></span>

## <a name="dsa-optimization-using-azure-cdn"></a><span data-ttu-id="0ce0f-128">使用 Azure CDN 將 DSA 最佳化</span><span class="sxs-lookup"><span data-stu-id="0ce0f-128">DSA Optimization using Azure CDN</span></span>

<span data-ttu-id="0ce0f-129">在 Azure CDN 的動態站台加速加速使用下列技巧 hello 動態資產的傳遞：</span><span class="sxs-lookup"><span data-stu-id="0ce0f-129">Dynamic Site Acceleration on Azure CDN speeds up delivery of dynamic assets using hello following techniques:</span></span>

-   <span data-ttu-id="0ce0f-130">路由最佳化</span><span class="sxs-lookup"><span data-stu-id="0ce0f-130">Route Optimization</span></span>
-   <span data-ttu-id="0ce0f-131">TCP 最佳化</span><span class="sxs-lookup"><span data-stu-id="0ce0f-131">TCP Optimizations</span></span>
-   <span data-ttu-id="0ce0f-132">物件預先擷取 (僅限 Akamai)</span><span class="sxs-lookup"><span data-stu-id="0ce0f-132">Object Prefetch (Akamai only)</span></span>
-   <span data-ttu-id="0ce0f-133">行動映像壓縮 (僅限 Akamai)</span><span class="sxs-lookup"><span data-stu-id="0ce0f-133">Mobile Image Compression (Akamai only)</span></span>

### <a name="route-optimization"></a><span data-ttu-id="0ce0f-134">路由最佳化</span><span class="sxs-lookup"><span data-stu-id="0ce0f-134">Route Optimization</span></span>

<span data-ttu-id="0ce0f-135">路線最佳化很重要的因為 hello 網際網路是動態的位置，其中流量並暫時中斷經常變更 hello 網路拓撲。</span><span class="sxs-lookup"><span data-stu-id="0ce0f-135">Route optimization is important because hello Internet is a dynamic place, where traffic and temporarily outages are constantly changing hello network topology.</span></span> <span data-ttu-id="0ce0f-136">hello 邊界閘道通訊協定 (BGP) 路由 hello hello 網際網路，通訊協定，但可能更快的路由，透過中繼點的目前狀態 (PoP) 伺服器。</span><span class="sxs-lookup"><span data-stu-id="0ce0f-136">hello Border Gateway Protocol (BGP) is hello routing protocol of hello Internet, but there may be faster routes via intermediary Point of Presence (PoP) servers.</span></span> 

<span data-ttu-id="0ce0f-137">Hello 最佳路徑 toohello 原點使站台會持續存取和動態內容傳遞 tooend 使用者透過 hello 最快速及最可靠的路由可能會選擇路線最佳化。</span><span class="sxs-lookup"><span data-stu-id="0ce0f-137">Route optimization chooses hello most optimal path toohello origin so that a site is continuously accessible and dynamic content is delivered tooend users via hello fastest and most reliable route possible.</span></span> 

<span data-ttu-id="0ce0f-138">hello Akamai 網路使用技術 toocollect 即時資料，以及比較 hello 開啟網際網路 toodetermine hello 最快速路由 hello 原點與 hello 之間的各種 hello Akamai 伺服器，以及 hello 預設 BGP 路由中的不同節點的路徑CDN 邊緣。</span><span class="sxs-lookup"><span data-stu-id="0ce0f-138">hello Akamai network uses techniques toocollect real-time data and compare various paths through different nodes in hello Akamai server, as well as hello default BGP route across hello open Internet toodetermine hello fastest route between hello origin and hello CDN edge.</span></span> <span data-ttu-id="0ce0f-139">這些技術可避開網際網路壅塞點和長途路由。</span><span class="sxs-lookup"><span data-stu-id="0ce0f-139">These techniques avoid Internet congestion points and long routes.</span></span> 

<span data-ttu-id="0ce0f-140">同樣地，任一傳播 DNS，高容量的組合支援快顯及健康情況檢查 toodetermine hello 最佳閘道 toobest 路由資料是從 hello Verizon 網路使用 hello 用戶端 toohello 原點。</span><span class="sxs-lookup"><span data-stu-id="0ce0f-140">Similarly, hello Verizon network uses a combination of Anycast DNS, high capacity support PoPs, and health checks, toodetermine hello best gateways toobest route data from hello client toohello origin.</span></span>
 
<span data-ttu-id="0ce0f-141">如此一來，完全動態和交易式傳遞內容的更快速且更可靠地 tooend 使用者，即使它是不可快取。</span><span class="sxs-lookup"><span data-stu-id="0ce0f-141">As a result, fully dynamic and transactional content is delivered more quickly and more reliably tooend users, even when it is uncacheable.</span></span> 

### <a name="tcp-optimizations"></a><span data-ttu-id="0ce0f-142">TCP 最佳化</span><span class="sxs-lookup"><span data-stu-id="0ce0f-142">TCP Optimizations</span></span>

<span data-ttu-id="0ce0f-143">傳輸控制通訊協定 (TCP) 是 hello 標準 hello 網際網路通訊協定使用 toodeliver IP 網路上的應用程式之間的資訊。</span><span class="sxs-lookup"><span data-stu-id="0ce0f-143">Transmission Control Protocol (TCP) is hello standard of hello Internet protocol suite used toodeliver information between applications on an IP network.</span></span>  <span data-ttu-id="0ce0f-144">根據預設，有數個後並提出要求所需 tooset 總 TCP 連線，以及限制 tooavoid 網路 congestions，這會導致在標尺的效率。</span><span class="sxs-lookup"><span data-stu-id="0ce0f-144">By default, there are several back and forth requests required tooset up a TCP connection, as well as limits tooavoid network congestions, which result in inefficiencies at scale.</span></span> <span data-ttu-id="0ce0f-145">Akamai 中的 Azure CDN 會處理這個問題，方法是將下列三個方面最佳化：</span><span class="sxs-lookup"><span data-stu-id="0ce0f-145">Azure CDN from Akamai deals with this problem by optimizing in three areas:</span></span> 

 - <span data-ttu-id="0ce0f-146">排除慢速啟動</span><span class="sxs-lookup"><span data-stu-id="0ce0f-146">eliminating slow start</span></span>
 - <span data-ttu-id="0ce0f-147">利用持續連線</span><span class="sxs-lookup"><span data-stu-id="0ce0f-147">leveraging persistent connections</span></span>
 - <span data-ttu-id="0ce0f-148">調整 TCP 封包參數 (僅限 Akamai)</span><span class="sxs-lookup"><span data-stu-id="0ce0f-148">tuning TCP packet parameters (Akamai only)</span></span>

#### <a name="eliminating-slow-start"></a><span data-ttu-id="0ce0f-149">排除慢速啟動</span><span class="sxs-lookup"><span data-stu-id="0ce0f-149">Eliminating slow start</span></span>

<span data-ttu-id="0ce0f-150">*緩慢開始*是限制 hello hello 網路上傳送的資料量，以防止網路壅塞的 hello TCP 通訊協定的一部分。</span><span class="sxs-lookup"><span data-stu-id="0ce0f-150">*Slow start* is a part of hello TCP protocol that prevents network congestion by limiting hello amount of data sent over hello network.</span></span> <span data-ttu-id="0ce0f-151">開始的寄件者與接收者之間的小壅塞視窗大小為止最大的 hello 或偵測到的封包遺失。</span><span class="sxs-lookup"><span data-stu-id="0ce0f-151">It starts off with small congestion window sizes between sender and receiver until hello maximum is reached or packet loss is detected.</span></span>

<span data-ttu-id="0ce0f-152">Akamai 和 Verizon 中的 Azure CDN 透過三個步驟來排除慢速啟動：</span><span class="sxs-lookup"><span data-stu-id="0ce0f-152">Azure CDN from Akamai and Verizon eliminates slow start in three steps:</span></span>

1.  <span data-ttu-id="0ce0f-153">Akamai 和 Verizon 的網路使用 「 狀況與監視 toomeasure hello 頻寬邊緣 PoP 伺服器之間的連線的頻寬。</span><span class="sxs-lookup"><span data-stu-id="0ce0f-153">Both Akamai and Verizon's network use health and bandwidth monitoring toomeasure hello bandwidth of connections between edge PoP servers.</span></span>
2. <span data-ttu-id="0ce0f-154">hello 度量會邊緣 PoP 伺服器之間共用，使每一部伺服器所知的 hello 網路狀況和伺服器健全狀況的 hello 其他周圍的快顯。</span><span class="sxs-lookup"><span data-stu-id="0ce0f-154">hello metrics are shared between edge PoP servers so that each server is aware of hello network conditions and server health of hello other PoPs around them.</span></span>  
3. <span data-ttu-id="0ce0f-155">hello CDN 邊緣伺服器現在都能 toomake 假設某些傳輸參數，例如與它靠近其他 CDN 邊緣伺服器通訊時，應該是 hello 最佳的視窗大小。</span><span class="sxs-lookup"><span data-stu-id="0ce0f-155">hello CDN edge servers are now able toomake assumptions about some transmission parameters, such as what hello optimal window size should be when communicating with other CDN edge servers in its proximity.</span></span> <span data-ttu-id="0ce0f-156">此步驟中，表示是否能夠更高的封包資料傳輸 hello hello hello CDN 邊緣伺服器之間的連線健全狀況，可以增加 hello 初始的壅塞視窗大小。</span><span class="sxs-lookup"><span data-stu-id="0ce0f-156">This step means that hello initial congestion window size can be increased if hello health of hello connection between hello CDN edge servers is capable of higher packet data transfers.</span></span>  

#### <a name="leveraging-persistent-connections"></a><span data-ttu-id="0ce0f-157">利用持續連線</span><span class="sxs-lookup"><span data-stu-id="0ce0f-157">Leveraging persistent connections</span></span>

<span data-ttu-id="0ce0f-158">使用 CDN，較少的唯一機器連接 tooyour 原始伺服器直接相較於直接連線 tooyour 來源的使用者。</span><span class="sxs-lookup"><span data-stu-id="0ce0f-158">Using a CDN, fewer unique machines connect tooyour origin server directly compared with users connecting directly tooyour origin.</span></span> <span data-ttu-id="0ce0f-159">從 Akamai 和 Verizon azure CDN 也加入集區使用者的要求一起 tooestablish hello 原點使用較少的連線。</span><span class="sxs-lookup"><span data-stu-id="0ce0f-159">Azure CDN from Akamai and Verizon also pools user requests together tooestablish fewer connections with hello origin.</span></span>

<span data-ttu-id="0ce0f-160">如先前所述，TCP 連線採取幾個要求來回交握 tooestablish 新的連接。</span><span class="sxs-lookup"><span data-stu-id="0ce0f-160">As mentioned earlier, TCP connections take several requests back and forth in a handshake tooestablish a new connection.</span></span> <span data-ttu-id="0ce0f-161">持續連線，也稱為 「 HTTP 保持運作，「 多個 HTTP 要求 toosave 來回行程時間的重複使用現有的 TCP 連線，並加速傳遞。</span><span class="sxs-lookup"><span data-stu-id="0ce0f-161">Persistent connections, also known as "HTTP Keep-Alive," reuse existing TCP connections for multiple HTTP requests toosave round-trip times and speed up delivery.</span></span> 

<span data-ttu-id="0ce0f-162">hello Verizon 網路也會傳送定期保持運作封包透過 hello TCP 連線 tooprevent 從正在關閉開啟的連接。</span><span class="sxs-lookup"><span data-stu-id="0ce0f-162">hello Verizon network also sends periodic keep-alive packets over hello TCP connection tooprevent an open connection from being closed.</span></span>

#### <a name="tuning-tcp-packet-parameters"></a><span data-ttu-id="0ce0f-163">調整 TCP 封包參數</span><span class="sxs-lookup"><span data-stu-id="0ce0f-163">Tuning TCP packet parameters</span></span>

<span data-ttu-id="0ce0f-164">Akamai 從 azure CDN 也微調 hello 參數，以管理伺服器對伺服器連線，並能減少 hello 使用下列技巧 hello hello 網站中內嵌的內容所需的往返 tooretrieve round 長時間牽引量：</span><span class="sxs-lookup"><span data-stu-id="0ce0f-164">Azure CDN from Akamai also tunes hello parameters that govern server-to-server connections, and reduces hello amount of long haul round trips required tooretrieve content embedded in hello site by using hello following techniques:</span></span>

1.  <span data-ttu-id="0ce0f-165">增加 hello 初始的壅塞視窗，以便能傳送多個封包，而不等候確認。</span><span class="sxs-lookup"><span data-stu-id="0ce0f-165">Increasing hello initial congestion window so that more packets can be sent without waiting for an acknowledgement.</span></span>
2.  <span data-ttu-id="0ce0f-166">以便在偵測到遺失時，並重新傳輸，就會發生更快速地減少 hello 初始重新傳輸逾時。</span><span class="sxs-lookup"><span data-stu-id="0ce0f-166">Decreasing hello initial retransmit timeout so that a loss is detected, and retransmission occurs more quickly.</span></span>
3.  <span data-ttu-id="0ce0f-167">遞減 hello 最小值和最大重新傳輸逾時 tooreduce hello 假設封包在傳輸中遺失之前的等待時間。</span><span class="sxs-lookup"><span data-stu-id="0ce0f-167">Decreasing hello minimum and maximum retransmit timeout tooreduce hello wait time before assuming packets were lost in transmission.</span></span>

### <a name="object-prefetch-akamai-only"></a><span data-ttu-id="0ce0f-168">物件預先擷取 (僅限 Akamai)</span><span class="sxs-lookup"><span data-stu-id="0ce0f-168">Object Prefetch (Akamai only)</span></span>

<span data-ttu-id="0ce0f-169">大多數網站是由參考諸如映像和指令碼等各種其他資源的 HTML 網頁所組成。</span><span class="sxs-lookup"><span data-stu-id="0ce0f-169">Most websites consist of an HTML page, which references various other resources such as images and scripts.</span></span> <span data-ttu-id="0ce0f-170">一般而言，當用戶端要求網頁，hello 瀏覽器會先下載並剖析 hello HTML 物件，並使 toolinked 資產之必要的 toofully hello 頁面載入的其他要求。</span><span class="sxs-lookup"><span data-stu-id="0ce0f-170">Typically, when a client requests a webpage, hello browser first downloads and parses hello HTML object, and then makes additional requests toolinked assets that are required toofully load hello page.</span></span> 

<span data-ttu-id="0ce0f-171">*預先擷取*是一種技術 tooretrieve 映像和指令碼內嵌在 hello HTML 網頁 hello HTML 提供 toohello 瀏覽器中，而之前 hello 瀏覽器甚至使這些物件的要求。</span><span class="sxs-lookup"><span data-stu-id="0ce0f-171">*Prefetch* is a technique tooretrieve images and scripts embedded in hello HTML page while hello HTML is served toohello browser, and before hello browser even makes these object requests.</span></span> 

<span data-ttu-id="0ce0f-172">以 hello**預先擷取**次 hello hello CDN 服務 hello HTML 基礎頁面 toohello 用戶端的瀏覽器中，當 hello CDN 開啟選項剖析 hello HTML 檔案和提出其他要求的任何連結的資源並將它存放在其快取。</span><span class="sxs-lookup"><span data-stu-id="0ce0f-172">With hello **prefetch** option turned on at hello time when hello CDN serves hello HTML base page toohello client’s browser, hello CDN parses hello HTML file and make additional requests for any linked resources and store it in its cache.</span></span> <span data-ttu-id="0ce0f-173">當 hello 戶端 hello 要求 hello 連結資產，hello CDN 邊緣伺服器已經有 hello 要求的物件，而且可以服務它們立即沒有往返 toohello 原點。</span><span class="sxs-lookup"><span data-stu-id="0ce0f-173">When hello client makes hello requests for hello linked assets, hello CDN edge server already has hello requested objects and can serve them immediately without a round trip toohello origin.</span></span> <span data-ttu-id="0ce0f-174">此最佳化有助於可快取和不可快取的內容。</span><span class="sxs-lookup"><span data-stu-id="0ce0f-174">This optimization benefits both cacheable and non-cacheable content.</span></span>

### <a name="adaptive-image-compression-akamai-only"></a><span data-ttu-id="0ce0f-175">調整映像壓縮 (僅限 Akamai)</span><span class="sxs-lookup"><span data-stu-id="0ce0f-175">Adaptive Image Compression (Akamai only)</span></span>

<span data-ttu-id="0ce0f-176">某些裝置，特別是行動電腦遇到時間 tootime 從較低的網路速度。</span><span class="sxs-lookup"><span data-stu-id="0ce0f-176">Some devices, especially mobile ones, experience slower network speeds from time tootime.</span></span> <span data-ttu-id="0ce0f-177">在這些情況中，會更有幫助他們的網頁中的 hello 使用者 tooreceive 小影像更快速而不是等待長時間的完整解析度的影像。</span><span class="sxs-lookup"><span data-stu-id="0ce0f-177">In these scenarios, it is more beneficial for hello user tooreceive smaller images in their webpage more quickly rather than waiting a long time for full resolution images.</span></span>

<span data-ttu-id="0ce0f-178">這項功能會自動監視網路品質，並採用標準 JPEG 壓縮方法，當網路速度慢 tooimprove 傳遞時間。</span><span class="sxs-lookup"><span data-stu-id="0ce0f-178">This feature automatically monitors network quality, and employs standard JPEG compression methods when network speeds are slower tooimprove delivery time.</span></span>

<span data-ttu-id="0ce0f-179">調整映像壓縮</span><span class="sxs-lookup"><span data-stu-id="0ce0f-179">Adaptive Image Compression</span></span> | <span data-ttu-id="0ce0f-180">副檔名</span><span class="sxs-lookup"><span data-stu-id="0ce0f-180">File Extensions</span></span>  
--- | ---  
<span data-ttu-id="0ce0f-181">JPEG 壓縮</span><span class="sxs-lookup"><span data-stu-id="0ce0f-181">JPEG compression</span></span> | <span data-ttu-id="0ce0f-182">.jpg、.jpeg、.jpe、.jig、.jgig、.jgi</span><span class="sxs-lookup"><span data-stu-id="0ce0f-182">.jpg, .jpeg, .jpe, .jig, .jgig, .jgi</span></span>

## <a name="caching"></a><span data-ttu-id="0ce0f-183">快取</span><span class="sxs-lookup"><span data-stu-id="0ce0f-183">Caching</span></span>

<span data-ttu-id="0ce0f-184">DSA，與快取已關閉預設會在 hello CDN，即使 hello 原點 hello 回應中包含快取控制項/到期的標頭。</span><span class="sxs-lookup"><span data-stu-id="0ce0f-184">With DSA, caching is turned off by default on hello CDN, even when hello origin includes cache-control/expires headers in hello response.</span></span> <span data-ttu-id="0ce0f-185">因為 DSA 通常用於動態的資產，應該不會快取因為它是唯一的 tooeach 用戶端，關閉此預設值，並開啟預設的快取可能會中斷這種行為。</span><span class="sxs-lookup"><span data-stu-id="0ce0f-185">This default is turned off because DSA is typically used for dynamic assets that should not be cached since they are unique tooeach client, and turning on caching by default can break this behavior.</span></span>

<span data-ttu-id="0ce0f-186">如果您有混合靜態和動態資產的網站時，它會是最佳 tootake 混合式方法 tooget hello 達到最佳效能。</span><span class="sxs-lookup"><span data-stu-id="0ce0f-186">If you have a website with a mix of static and dynamic assets, it is best tootake a hybrid approach tooget hello best performance.</span></span> 

<span data-ttu-id="0ce0f-187">如果您使用和 Verizon premium，您可以開啟回上特定的情況下使用 hello 規則引擎的快取。</span><span class="sxs-lookup"><span data-stu-id="0ce0f-187">If you are using ADN with Verizon Premium, you can turn caching back on for specific cases using hello Rules Engine.</span></span>  

<span data-ttu-id="0ce0f-188">替代方式是 toouse 兩個的 CDN 端點。</span><span class="sxs-lookup"><span data-stu-id="0ce0f-188">An alternative is toouse two CDN endpoints.</span></span> <span data-ttu-id="0ce0f-189">DSA toodeliver 動態資產的一個，另一個端點使用靜態的最佳化類型，例如一般 web 傳遞 toodelivery 可快取資產。</span><span class="sxs-lookup"><span data-stu-id="0ce0f-189">One with DSA toodeliver dynamic assets, and another endpoint with a static optimization type, such as general web delivery, toodelivery cacheable assets.</span></span> <span data-ttu-id="0ce0f-190">順序 tooaccomplish 此替代，在中，您將修改您的網頁 Url toolink 直接 toohello 資產上的 hello 您計劃 toouse 的 CDN 端點。</span><span class="sxs-lookup"><span data-stu-id="0ce0f-190">In order tooaccomplish this alternative, you will modify your webpage URLs toolink directly toohello asset on hello CDN endpoint you plan toouse.</span></span> 

<span data-ttu-id="0ce0f-191">例如：`mydynamic.azureedge.net/index.html`是動態，而且是從 hello DSA 端點載入。</span><span class="sxs-lookup"><span data-stu-id="0ce0f-191">For example: `mydynamic.azureedge.net/index.html` is a dynamic page and is loaded from hello DSA endpoint.</span></span>  <span data-ttu-id="0ce0f-192">hello html 頁面參考多個靜態資產，例如 JavaScript 程式庫，或從已載入的映像 hello 靜態 CDN 端點，例如`mystatic.azureedge.net/banner.jpg`和`mystatic.azureedge.net/scripts.js`。</span><span class="sxs-lookup"><span data-stu-id="0ce0f-192">hello html page references multiple static assets such as JavaScript libraries or images that are loaded from hello static CDN endpoint, such as `mystatic.azureedge.net/banner.jpg` and `mystatic.azureedge.net/scripts.js`.</span></span> 

<span data-ttu-id="0ce0f-193">您可以找到範例[這裡](https://docs.microsoft.com/azure/cdn/cdn-cloud-service-with-cdn#controller)上 toouse 控制站，在 ASP.NET web 應用程式 tooserve 內容，透過特定的 CDN URL 的方式。</span><span class="sxs-lookup"><span data-stu-id="0ce0f-193">You can find an example [here](https://docs.microsoft.com/azure/cdn/cdn-cloud-service-with-cdn#controller) on how toouse controllers in an ASP.NET web application tooserve content through a specific CDN URL.</span></span>




