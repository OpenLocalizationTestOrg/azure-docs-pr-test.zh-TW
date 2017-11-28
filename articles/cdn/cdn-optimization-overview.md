---
title: "aaaOptimize Azure 內容傳遞，您的案例"
description: "如何 toooptimize 傳遞您針對特定案例的內容"
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
ms.openlocfilehash: 922a92fdbf7e6e21f2b5ae9a2fb4ac32735fc15a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-azure-content-delivery-for-your-scenario"></a><span data-ttu-id="7fe39-103">最佳化您案例的 Azure 內容傳遞</span><span class="sxs-lookup"><span data-stu-id="7fe39-103">Optimize Azure content delivery for your scenario</span></span>

<span data-ttu-id="7fe39-104">傳遞內容 tooa 大型全球使用者時，很重要 tooensure hello 最佳化傳遞的內容。</span><span class="sxs-lookup"><span data-stu-id="7fe39-104">When you deliver content tooa large global audience, it's critical tooensure hello optimized delivery of your content.</span></span> <span data-ttu-id="7fe39-105">hello Azure 內容傳遞網路可以最佳化 hello 傳遞經驗 hello 您擁有的內容類型為基礎。</span><span class="sxs-lookup"><span data-stu-id="7fe39-105">hello Azure Content Delivery Network can optimize hello delivery experience based on hello type of content you have.</span></span> <span data-ttu-id="7fe39-106">內容可以是網站、即時串流、影片或供下載的大型檔案。</span><span class="sxs-lookup"><span data-stu-id="7fe39-106">Content can be a website, a live stream, a video, or a large file for download.</span></span> <span data-ttu-id="7fe39-107">當您建立的內容傳遞網路 (CDN) 端點時，指定情節中 hello**適合**選項。</span><span class="sxs-lookup"><span data-stu-id="7fe39-107">When you create a content delivery network (CDN) endpoint, you specify a scenario in hello **Optimized for** option.</span></span> <span data-ttu-id="7fe39-108">您的選擇會決定哪一個最佳化是套用的 toohello 內容傳遞從 hello CDN 端點。</span><span class="sxs-lookup"><span data-stu-id="7fe39-108">Your choice determines which optimization is applied toohello content delivered from hello CDN endpoint.</span></span>

<span data-ttu-id="7fe39-109">最佳化的選項為 toouse 設計的最佳作法行為 tooimprove 內容傳遞的效能和更佳的原始卸載。</span><span class="sxs-lookup"><span data-stu-id="7fe39-109">Optimization choices are designed toouse best-practice behaviors tooimprove content delivery performance and better origin offload.</span></span> <span data-ttu-id="7fe39-110">您案例的選擇會影響效能，藉由修改部分快取物件區塊化，和 hello 來源失敗重試原則的設定。</span><span class="sxs-lookup"><span data-stu-id="7fe39-110">Your scenario choices affect performance by modifying configurations for partial caching, object chunking, and hello origin failure retry policy.</span></span> 

<span data-ttu-id="7fe39-111">本文提供各種最佳化功能概觀和使用時機。</span><span class="sxs-lookup"><span data-stu-id="7fe39-111">This article provides an overview of various optimization features and when you should use them.</span></span> <span data-ttu-id="7fe39-112">如需有關的功能和限制的詳細資訊，請參閱 hello 個別文件的每個個別的最佳化類型。</span><span class="sxs-lookup"><span data-stu-id="7fe39-112">For more information on features and limitations, see hello respective articles on each individual optimization type.</span></span>

> [!NOTE]
> <span data-ttu-id="7fe39-113">您**適合**選項可以隨著您選取的 hello 提供者。</span><span class="sxs-lookup"><span data-stu-id="7fe39-113">Your **Optimized for** options can vary based on hello provider you select.</span></span> <span data-ttu-id="7fe39-114">CDN 提供者會套用不同的方式，視 hello 案例而定的增強功能。</span><span class="sxs-lookup"><span data-stu-id="7fe39-114">CDN providers apply enhancement in different ways, depending on hello scenario.</span></span> 

## <a name="provider-options"></a><span data-ttu-id="7fe39-115">提供者選項</span><span class="sxs-lookup"><span data-stu-id="7fe39-115">Provider options</span></span>

<span data-ttu-id="7fe39-116">Akamai 支援從 hello Azure 內容傳遞網路：</span><span class="sxs-lookup"><span data-stu-id="7fe39-116">hello Azure Content Delivery Network from Akamai supports:</span></span>

* <span data-ttu-id="7fe39-117">一般 Web 傳遞</span><span class="sxs-lookup"><span data-stu-id="7fe39-117">General web delivery</span></span> 

* <span data-ttu-id="7fe39-118">一般媒體串流處理</span><span class="sxs-lookup"><span data-stu-id="7fe39-118">General media streaming</span></span>

* <span data-ttu-id="7fe39-119">點播視訊媒體串流處理</span><span class="sxs-lookup"><span data-stu-id="7fe39-119">Video-on-demand media streaming</span></span>

* <span data-ttu-id="7fe39-120">大型檔案下載</span><span class="sxs-lookup"><span data-stu-id="7fe39-120">Large file download</span></span>

* <span data-ttu-id="7fe39-121">動態網站加速</span><span class="sxs-lookup"><span data-stu-id="7fe39-121">Dynamic site acceleration</span></span> 

<span data-ttu-id="7fe39-122">hello Azure 內容傳遞網路從 Verizon 支援只有一般 web 傳遞。</span><span class="sxs-lookup"><span data-stu-id="7fe39-122">hello Azure Content Delivery Network from Verizon supports general web delivery only.</span></span> <span data-ttu-id="7fe39-123">它可以用於點播視訊和大型檔案下載。</span><span class="sxs-lookup"><span data-stu-id="7fe39-123">It can be used for video on demand and large file download.</span></span> <span data-ttu-id="7fe39-124">您不需要 tooselect 最佳化類型。</span><span class="sxs-lookup"><span data-stu-id="7fe39-124">You don't have tooselect an optimization type.</span></span>

<span data-ttu-id="7fe39-125">強烈建議您測試不同的提供者 tooselect hello 最佳提供者為您的傳遞之間的效能變化。</span><span class="sxs-lookup"><span data-stu-id="7fe39-125">We highly recommend that you test performance variations between different providers tooselect hello optimal provider for your delivery.</span></span>

## <a name="select-and-configure-optimization-types"></a><span data-ttu-id="7fe39-126">選取並設定最佳化類型</span><span class="sxs-lookup"><span data-stu-id="7fe39-126">Select and configure optimization types</span></span>

<span data-ttu-id="7fe39-127">toocreate 新端點，會選取最符合 hello 案例的最佳化類型以及您想要 hello 端點 toodeliver 的內容類型。</span><span class="sxs-lookup"><span data-stu-id="7fe39-127">toocreate a new endpoint, select an optimization type that best matches hello scenario and type of content that you want hello endpoint toodeliver.</span></span> <span data-ttu-id="7fe39-128">**一般 web 傳遞**hello 預設選取項目。</span><span class="sxs-lookup"><span data-stu-id="7fe39-128">**General web delivery** is hello default selection.</span></span> <span data-ttu-id="7fe39-129">您可以更新任何現有的 Akamai 端點在任何時間的 hello 最佳化選項。</span><span class="sxs-lookup"><span data-stu-id="7fe39-129">You can update hello optimization option for any existing Akamai endpoint at any time.</span></span> <span data-ttu-id="7fe39-130">這項變更不會干擾從 hello CDN 傳遞。</span><span class="sxs-lookup"><span data-stu-id="7fe39-130">This change doesn't interrupt delivery from hello CDN.</span></span> 

1. <span data-ttu-id="7fe39-131">選取標準 Akamai 設定檔中的端點。</span><span class="sxs-lookup"><span data-stu-id="7fe39-131">Select an endpoint within a Standard Akamai profile.</span></span>

    ![<span data-ttu-id="7fe39-132">端點選取範圍</span><span class="sxs-lookup"><span data-stu-id="7fe39-132">Endpoint selection</span></span> ](./media/cdn-optimization-overview/01_Akamai.png)

2. <span data-ttu-id="7fe39-133">在 [設定] 下選取 [最佳化]。</span><span class="sxs-lookup"><span data-stu-id="7fe39-133">Under **SETTINGS**, select **Optimization**.</span></span> <span data-ttu-id="7fe39-134">然後從 hello 選取類型**適合**下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="7fe39-134">Then select a type from hello **Optimized for** drop-down list.</span></span>

    ![選取最佳化和類型](./media/cdn-optimization-overview/02_Select.png)

## <a name="optimization-for-specific-scenarios"></a><span data-ttu-id="7fe39-136">特定案例最佳化</span><span class="sxs-lookup"><span data-stu-id="7fe39-136">Optimization for specific scenarios</span></span>

<span data-ttu-id="7fe39-137">您可以最佳化 hello CDN 端點，其中一個 hello 下列案例。</span><span class="sxs-lookup"><span data-stu-id="7fe39-137">You can optimize hello CDN endpoint for one of hello following scenarios.</span></span> 

### <a name="general-web-delivery"></a><span data-ttu-id="7fe39-138">一般 Web 傳遞</span><span class="sxs-lookup"><span data-stu-id="7fe39-138">General web delivery</span></span>

<span data-ttu-id="7fe39-139">一般 web 傳遞是 hello 最常見的最佳化選項。</span><span class="sxs-lookup"><span data-stu-id="7fe39-139">General web delivery is hello most common optimization option.</span></span> <span data-ttu-id="7fe39-140">它是專為一般 Web 內容最佳化所設計，例如網頁和 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="7fe39-140">It's designed for general web content optimization, such as webpages and web applications.</span></span> <span data-ttu-id="7fe39-141">此最佳化也可用於檔案和視訊下載。</span><span class="sxs-lookup"><span data-stu-id="7fe39-141">This optimization also can be used for file and video downloads.</span></span>

<span data-ttu-id="7fe39-142">一般網站包含靜態和動態的內容。</span><span class="sxs-lookup"><span data-stu-id="7fe39-142">A typical website contains static and dynamic content.</span></span> <span data-ttu-id="7fe39-143">靜態內容包括影像、 JavaScript 程式庫和樣式表可以快取和傳遞 toodifferent 使用者。</span><span class="sxs-lookup"><span data-stu-id="7fe39-143">Static content includes images, JavaScript libraries, and style sheets that can be cached and delivered toodifferent users.</span></span> <span data-ttu-id="7fe39-144">動態內容是為個別的使用者個人化，例如新聞項目所量身訂做 tooa 使用者設定檔。</span><span class="sxs-lookup"><span data-stu-id="7fe39-144">Dynamic content is personalized for an individual user, such as news items that are tailored tooa user profile.</span></span> <span data-ttu-id="7fe39-145">動態內容不是快取，因為它是唯一的 tooeach 使用者，例如購物車內容。</span><span class="sxs-lookup"><span data-stu-id="7fe39-145">Dynamic content isn't cached because it's unique tooeach user, such as shopping cart contents.</span></span> <span data-ttu-id="7fe39-146">一般 Web 傳遞可以最佳化整個網站。</span><span class="sxs-lookup"><span data-stu-id="7fe39-146">General web delivery can optimize your entire website.</span></span> 

> [!NOTE]
> <span data-ttu-id="7fe39-147">如果您使用 hello Akamai 從 Azure 內容傳遞網路，您可能想 toouse 此最佳化如果平均檔案大小小於 10 MB。</span><span class="sxs-lookup"><span data-stu-id="7fe39-147">If you use hello Azure Content Delivery Network from Akamai, you might want toouse this optimization if your average file size is smaller than 10 MB.</span></span> <span data-ttu-id="7fe39-148">如果您的平均檔案大小大於 10 MB，請選取**大型檔案的下載**從 hello**適合**下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="7fe39-148">If your average file size is larger than 10 MB, select **Large file download** from hello **Optimized for** drop-down list.</span></span>

### <a name="general-media-streaming"></a><span data-ttu-id="7fe39-149">一般媒體串流處理</span><span class="sxs-lookup"><span data-stu-id="7fe39-149">General media streaming</span></span>

<span data-ttu-id="7fe39-150">如果您需要 toouse hello 端點的即時資料流和 video-on-demand 串流時，我們建議一般媒體資料流最佳化。</span><span class="sxs-lookup"><span data-stu-id="7fe39-150">If you need toouse hello endpoint for live streaming and video-on-demand streaming, we recommend general media streaming optimization.</span></span>

<span data-ttu-id="7fe39-151">媒體串流處理是區分大小寫的時間，因為封包抵達晚期 hello 用戶端上可能會造成降低的檢視經驗，例如經常緩衝處理的視訊內容。</span><span class="sxs-lookup"><span data-stu-id="7fe39-151">Media streaming is time sensitive, because packets that arrive late on hello client can cause a degraded viewing experience, such as frequent buffering of video content.</span></span> <span data-ttu-id="7fe39-152">媒體串流最佳化降低 hello 延遲的媒體內容傳遞，並提供使用者 smooth 串流處理體驗。</span><span class="sxs-lookup"><span data-stu-id="7fe39-152">Media streaming optimization reduces hello latency of media content delivery and provides a smooth streaming experience for users.</span></span> 

<span data-ttu-id="7fe39-153">Azure 媒體服務的客戶經常發生此狀況。</span><span class="sxs-lookup"><span data-stu-id="7fe39-153">This scenario is common for Azure media service customers.</span></span> <span data-ttu-id="7fe39-154">當您使用 Azure 媒體服務時，您會取得一個串流端點，可用於即時和隨選資料流處理。</span><span class="sxs-lookup"><span data-stu-id="7fe39-154">When you use Azure media services, you get one streaming endpoint that can be used for both live and on-demand streaming.</span></span> <span data-ttu-id="7fe39-155">此案例，客戶不需要 tooswitch tooanother 端點從即時 tooon 隨選串流其變更時。</span><span class="sxs-lookup"><span data-stu-id="7fe39-155">With this scenario, customers don't need tooswitch tooanother endpoint when they change from live tooon-demand streaming.</span></span> <span data-ttu-id="7fe39-156">一般媒體串流處理最佳化支援這種情況。</span><span class="sxs-lookup"><span data-stu-id="7fe39-156">General media streaming optimization supports this type of scenario.</span></span>

<span data-ttu-id="7fe39-157">hello Azure 內容傳遞網路從 Verizon 使用 hello 一般 web 傳遞最佳化類型 toodeliver 串流處理媒體內容。</span><span class="sxs-lookup"><span data-stu-id="7fe39-157">hello Azure Content Delivery Network from Verizon uses hello general web delivery optimization type toodeliver streaming media content.</span></span>

<span data-ttu-id="7fe39-158">toolearn 進一步了解媒體串流處理最佳化，請參閱[媒體串流最佳化](cdn-media-streaming-optimization.md)。</span><span class="sxs-lookup"><span data-stu-id="7fe39-158">toolearn more about media streaming optimization, see [Media streaming optimization](cdn-media-streaming-optimization.md).</span></span>

### <a name="video-on-demand-media-streaming"></a><span data-ttu-id="7fe39-159">點播視訊媒體串流處理</span><span class="sxs-lookup"><span data-stu-id="7fe39-159">Video-on-demand media streaming</span></span>

<span data-ttu-id="7fe39-160">點播視訊媒體串流處理最佳化會改善點播視訊串流處理內容。</span><span class="sxs-lookup"><span data-stu-id="7fe39-160">Video-on-demand media streaming optimization improves video-on-demand streaming content.</span></span> <span data-ttu-id="7fe39-161">如果您使用端點 video-on-demand 串流處理時，您可能想 toouse 此選項。</span><span class="sxs-lookup"><span data-stu-id="7fe39-161">If you use an endpoint for video-on-demand streaming, you might want toouse this option.</span></span>

<span data-ttu-id="7fe39-162">hello Azure 內容傳遞網路從 Verizon 使用 hello 一般 web 傳遞最佳化類型 toodeliver 串流處理媒體內容。</span><span class="sxs-lookup"><span data-stu-id="7fe39-162">hello Azure Content Delivery Network from Verizon uses hello general web delivery optimization type toodeliver streaming media content.</span></span>

<span data-ttu-id="7fe39-163">toolearn 進一步了解媒體串流處理最佳化，請參閱[媒體串流最佳化](cdn-media-streaming-optimization.md)。</span><span class="sxs-lookup"><span data-stu-id="7fe39-163">toolearn more about media streaming optimization, see [Media streaming optimization](cdn-media-streaming-optimization.md).</span></span>

> [!NOTE]
> <span data-ttu-id="7fe39-164">Hello 端點主要是提供 video-on-demand 內容，如果使用此最佳化類型。</span><span class="sxs-lookup"><span data-stu-id="7fe39-164">If hello endpoint primarily serves video-on-demand content, use this optimization type.</span></span> <span data-ttu-id="7fe39-165">hello 這個最佳化與 hello 一般媒體串流最佳化之間的主要差異是 hello 連線重試逾時。hello 逾時是使用即時資料流案例更短 toowork。</span><span class="sxs-lookup"><span data-stu-id="7fe39-165">hello major difference between this optimization and hello general media streaming optimization is hello connection retry time-out. hello time-out is much shorter toowork with live streaming scenarios.</span></span>

### <a name="large-file-download"></a><span data-ttu-id="7fe39-166">大型檔案下載</span><span class="sxs-lookup"><span data-stu-id="7fe39-166">Large file download</span></span>

<span data-ttu-id="7fe39-167">如果您使用 hello Akamai 從 Azure 內容傳遞網路，您必須使用大於 1.8 g b 的大型檔案下載 toodeliver 檔案。</span><span class="sxs-lookup"><span data-stu-id="7fe39-167">If you use hello Azure Content Delivery Network from Akamai, you must use large file download toodeliver files larger than 1.8 GB.</span></span> <span data-ttu-id="7fe39-168">hello Verizon 從 Azure 內容傳遞網路沒有檔案下載在其一般 web 傳遞最佳化的大小限制。</span><span class="sxs-lookup"><span data-stu-id="7fe39-168">hello Azure Content Delivery Network from Verizon doesn't have a limitation on file download size in its general web delivery optimization.</span></span>

<span data-ttu-id="7fe39-169">如果您使用 hello Akamai 從 Azure 內容傳遞網路，下載大型檔案適合用於內容大於 10 MB。</span><span class="sxs-lookup"><span data-stu-id="7fe39-169">If you use hello Azure Content Delivery Network from Akamai, large file downloads are optimized for content larger than 10 MB.</span></span> <span data-ttu-id="7fe39-170">如果您的平均檔案大小小於 10 MB，您可能想 toouse 一般 web 傳遞。</span><span class="sxs-lookup"><span data-stu-id="7fe39-170">If your average file size is smaller than 10 MB, you might want toouse general web delivery.</span></span> <span data-ttu-id="7fe39-171">如果平均檔案大小會持續大於 10 MB，可能是更有效率的 toocreate 大型檔案的個別端點。</span><span class="sxs-lookup"><span data-stu-id="7fe39-171">If your average files sizes are consistently larger than 10 MB, it might be more efficient toocreate a separate endpoint for large files.</span></span> <span data-ttu-id="7fe39-172">例如，韌體或軟體更新通常是大型檔案。</span><span class="sxs-lookup"><span data-stu-id="7fe39-172">For example, firmware or software updates typically are large files.</span></span>

<span data-ttu-id="7fe39-173">hello Azure 內容傳遞網路從 Verizon 使用 hello 一般 web 傳遞最佳化類型 toodeliver 串流處理媒體內容。</span><span class="sxs-lookup"><span data-stu-id="7fe39-173">hello Azure Content Delivery Network from Verizon uses hello general web delivery optimization type toodeliver streaming media content.</span></span>

<span data-ttu-id="7fe39-174">toolearn 進一步了解大型的檔案最佳化功能，請參閱[大型檔案最佳化](cdn-large-file-optimization.md)。</span><span class="sxs-lookup"><span data-stu-id="7fe39-174">toolearn more about large file optimization, see [Large file optimization](cdn-large-file-optimization.md).</span></span>

### <a name="dynamic-site-acceleration"></a><span data-ttu-id="7fe39-175">動態網站加速</span><span class="sxs-lookup"><span data-stu-id="7fe39-175">Dynamic site acceleration</span></span>

 <span data-ttu-id="7fe39-176">Akamai 和 Verizon 的內容傳遞網路設定檔都提供動態網站加速。</span><span class="sxs-lookup"><span data-stu-id="7fe39-176">Dynamic site acceleration is available from both Akamai and Verizon Content Delivery Network profiles.</span></span> <span data-ttu-id="7fe39-177">此最佳化牽涉到額外的費用 toouse。</span><span class="sxs-lookup"><span data-stu-id="7fe39-177">This optimization involves an additional fee toouse.</span></span> <span data-ttu-id="7fe39-178">如需詳細資訊，請參閱 hello 定價頁面。</span><span class="sxs-lookup"><span data-stu-id="7fe39-178">For more information, see hello pricing page.</span></span>

<span data-ttu-id="7fe39-179">動態站台加速包括 hello 延遲和動態內容的效能獲益的各種技術。</span><span class="sxs-lookup"><span data-stu-id="7fe39-179">Dynamic site acceleration includes various techniques that benefit hello latency and performance of dynamic content.</span></span> <span data-ttu-id="7fe39-180">相關技術包括路由和網路最佳化、TCP 最佳化等等。</span><span class="sxs-lookup"><span data-stu-id="7fe39-180">Techniques include route and network optimization, TCP optimization, and more.</span></span> 

<span data-ttu-id="7fe39-181">您可以使用此最佳化 tooaccelerate web 應用程式，其中包含許多不是可快取的回應。</span><span class="sxs-lookup"><span data-stu-id="7fe39-181">You can use this optimization tooaccelerate a web app that includes numerous responses that aren't cacheable.</span></span> <span data-ttu-id="7fe39-182">範例包括搜尋結果、簽出交易或即時資料。</span><span class="sxs-lookup"><span data-stu-id="7fe39-182">Examples are search results, checkout transactions, or real-time data.</span></span> <span data-ttu-id="7fe39-183">您可以繼續靜態資料的 toouse 核心 CDN 快取的功能。</span><span class="sxs-lookup"><span data-stu-id="7fe39-183">You can continue toouse core CDN caching capabilities for static data.</span></span> 



