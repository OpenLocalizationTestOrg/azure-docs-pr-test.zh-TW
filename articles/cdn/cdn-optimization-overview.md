---
title: "最佳化您案例的 Azure 內容傳遞"
description: "如何最佳化特定案例的內容傳遞"
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
ms.openlocfilehash: 98941c49b057380b3ef9164515bcc2a63ccb56ce
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="optimize-azure-content-delivery-for-your-scenario"></a><span data-ttu-id="81f93-103">最佳化您案例的 Azure 內容傳遞</span><span class="sxs-lookup"><span data-stu-id="81f93-103">Optimize Azure content delivery for your scenario</span></span>

<span data-ttu-id="81f93-104">當您將內容傳遞給所有對象時，請務必確保最佳的傳遞內容。</span><span class="sxs-lookup"><span data-stu-id="81f93-104">When you deliver content to a large global audience, it's critical to ensure the optimized delivery of your content.</span></span> <span data-ttu-id="81f93-105">Azure 內容傳遞網路可以根據您的內容類型，最佳化傳遞體驗。</span><span class="sxs-lookup"><span data-stu-id="81f93-105">The Azure Content Delivery Network can optimize the delivery experience based on the type of content you have.</span></span> <span data-ttu-id="81f93-106">內容可以是網站、即時串流、影片或供下載的大型檔案。</span><span class="sxs-lookup"><span data-stu-id="81f93-106">Content can be a website, a live stream, a video, or a large file for download.</span></span> <span data-ttu-id="81f93-107">當您建立的內容傳遞網路 (CDN) 端點時，要在 [最佳化對象] 選項中指定案例。</span><span class="sxs-lookup"><span data-stu-id="81f93-107">When you create a content delivery network (CDN) endpoint, you specify a scenario in the **Optimized for** option.</span></span> <span data-ttu-id="81f93-108">您的選擇會決定從 CDN 端點傳送的內容套用哪一個最佳化。</span><span class="sxs-lookup"><span data-stu-id="81f93-108">Your choice determines which optimization is applied to the content delivered from the CDN endpoint.</span></span>

<span data-ttu-id="81f93-109">最佳化選項旨在使用最佳作法行為改善內容傳遞效能以及更好的原始卸載。</span><span class="sxs-lookup"><span data-stu-id="81f93-109">Optimization choices are designed to use best-practice behaviors to improve content delivery performance and better origin offload.</span></span> <span data-ttu-id="81f93-110">您案例的選擇會修改部分快取、物件區塊化和原始失敗重試原則的組態，進而影響效能。</span><span class="sxs-lookup"><span data-stu-id="81f93-110">Your scenario choices affect performance by modifying configurations for partial caching, object chunking, and the origin failure retry policy.</span></span> 

<span data-ttu-id="81f93-111">本文提供各種最佳化功能概觀和使用時機。</span><span class="sxs-lookup"><span data-stu-id="81f93-111">This article provides an overview of various optimization features and when you should use them.</span></span> <span data-ttu-id="81f93-112">如需功能和限制的詳細資訊，請參閱每個個別最佳化類型的各自文件。</span><span class="sxs-lookup"><span data-stu-id="81f93-112">For more information on features and limitations, see the respective articles on each individual optimization type.</span></span>

> [!NOTE]
> <span data-ttu-id="81f93-113">您的 [最佳化對象] 選項會隨著您選取的提供者而異。</span><span class="sxs-lookup"><span data-stu-id="81f93-113">Your **Optimized for** options can vary based on the provider you select.</span></span> <span data-ttu-id="81f93-114">CDN 提供者會以不同的方式套用增強功能，視案例而定。</span><span class="sxs-lookup"><span data-stu-id="81f93-114">CDN providers apply enhancement in different ways, depending on the scenario.</span></span> 

## <a name="provider-options"></a><span data-ttu-id="81f93-115">提供者選項</span><span class="sxs-lookup"><span data-stu-id="81f93-115">Provider options</span></span>

<span data-ttu-id="81f93-116">Akamai 的 Azure 內容傳遞網路支援：</span><span class="sxs-lookup"><span data-stu-id="81f93-116">The Azure Content Delivery Network from Akamai supports:</span></span>

* <span data-ttu-id="81f93-117">一般 Web 傳遞</span><span class="sxs-lookup"><span data-stu-id="81f93-117">General web delivery</span></span> 

* <span data-ttu-id="81f93-118">一般媒體串流處理</span><span class="sxs-lookup"><span data-stu-id="81f93-118">General media streaming</span></span>

* <span data-ttu-id="81f93-119">點播視訊媒體串流處理</span><span class="sxs-lookup"><span data-stu-id="81f93-119">Video-on-demand media streaming</span></span>

* <span data-ttu-id="81f93-120">大型檔案下載</span><span class="sxs-lookup"><span data-stu-id="81f93-120">Large file download</span></span>

* <span data-ttu-id="81f93-121">動態網站加速</span><span class="sxs-lookup"><span data-stu-id="81f93-121">Dynamic site acceleration</span></span> 

<span data-ttu-id="81f93-122">Verizon 的 Azure 內容傳遞網路僅支援一般 Web 傳遞。</span><span class="sxs-lookup"><span data-stu-id="81f93-122">The Azure Content Delivery Network from Verizon supports general web delivery only.</span></span> <span data-ttu-id="81f93-123">它可以用於點播視訊和大型檔案下載。</span><span class="sxs-lookup"><span data-stu-id="81f93-123">It can be used for video on demand and large file download.</span></span> <span data-ttu-id="81f93-124">您不必選取最佳化類型。</span><span class="sxs-lookup"><span data-stu-id="81f93-124">You don't have to select an optimization type.</span></span>

<span data-ttu-id="81f93-125">強烈建議您測試不同提供者之間的效能變化，以選取最佳的傳遞提供者。</span><span class="sxs-lookup"><span data-stu-id="81f93-125">We highly recommend that you test performance variations between different providers to select the optimal provider for your delivery.</span></span>

## <a name="select-and-configure-optimization-types"></a><span data-ttu-id="81f93-126">選取並設定最佳化類型</span><span class="sxs-lookup"><span data-stu-id="81f93-126">Select and configure optimization types</span></span>

<span data-ttu-id="81f93-127">若要建立新的端點，請選取最符合案例的最佳化類型，以及您想要端點傳送的內容類型。</span><span class="sxs-lookup"><span data-stu-id="81f93-127">To create a new endpoint, select an optimization type that best matches the scenario and type of content that you want the endpoint to deliver.</span></span> <span data-ttu-id="81f93-128">**一般 Web 傳遞**是預設選項。</span><span class="sxs-lookup"><span data-stu-id="81f93-128">**General web delivery** is the default selection.</span></span> <span data-ttu-id="81f93-129">您可以隨時更新任何現有 Akamai 端點的最佳化選項。</span><span class="sxs-lookup"><span data-stu-id="81f93-129">You can update the optimization option for any existing Akamai endpoint at any time.</span></span> <span data-ttu-id="81f93-130">這項變更不會干擾 CDN 傳遞。</span><span class="sxs-lookup"><span data-stu-id="81f93-130">This change doesn't interrupt delivery from the CDN.</span></span> 

1. <span data-ttu-id="81f93-131">選取標準 Akamai 設定檔中的端點。</span><span class="sxs-lookup"><span data-stu-id="81f93-131">Select an endpoint within a Standard Akamai profile.</span></span>

    ![<span data-ttu-id="81f93-132">端點選取範圍</span><span class="sxs-lookup"><span data-stu-id="81f93-132">Endpoint selection</span></span> ](./media/cdn-optimization-overview/01_Akamai.png)

2. <span data-ttu-id="81f93-133">在 [設定] 下選取 [最佳化]。</span><span class="sxs-lookup"><span data-stu-id="81f93-133">Under **SETTINGS**, select **Optimization**.</span></span> <span data-ttu-id="81f93-134">然後從 [最佳化對象] 下拉式清單選取類型。</span><span class="sxs-lookup"><span data-stu-id="81f93-134">Then select a type from the **Optimized for** drop-down list.</span></span>

    ![選取最佳化和類型](./media/cdn-optimization-overview/02_Select.png)

## <a name="optimization-for-specific-scenarios"></a><span data-ttu-id="81f93-136">特定案例最佳化</span><span class="sxs-lookup"><span data-stu-id="81f93-136">Optimization for specific scenarios</span></span>

<span data-ttu-id="81f93-137">您可以最佳化下列案例之一的 CDN 端點。</span><span class="sxs-lookup"><span data-stu-id="81f93-137">You can optimize the CDN endpoint for one of the following scenarios.</span></span> 

### <a name="general-web-delivery"></a><span data-ttu-id="81f93-138">一般 Web 傳遞</span><span class="sxs-lookup"><span data-stu-id="81f93-138">General web delivery</span></span>

<span data-ttu-id="81f93-139">一般 Web 傳遞是最常見的最佳化選項。</span><span class="sxs-lookup"><span data-stu-id="81f93-139">General web delivery is the most common optimization option.</span></span> <span data-ttu-id="81f93-140">它是專為一般 Web 內容最佳化所設計，例如網頁和 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="81f93-140">It's designed for general web content optimization, such as webpages and web applications.</span></span> <span data-ttu-id="81f93-141">此最佳化也可用於檔案和視訊下載。</span><span class="sxs-lookup"><span data-stu-id="81f93-141">This optimization also can be used for file and video downloads.</span></span>

<span data-ttu-id="81f93-142">一般網站包含靜態和動態的內容。</span><span class="sxs-lookup"><span data-stu-id="81f93-142">A typical website contains static and dynamic content.</span></span> <span data-ttu-id="81f93-143">靜態內容包括可供不同使用者快取和傳遞的影像、JavaScript 程式庫和樣式表。</span><span class="sxs-lookup"><span data-stu-id="81f93-143">Static content includes images, JavaScript libraries, and style sheets that can be cached and delivered to different users.</span></span> <span data-ttu-id="81f93-144">動態內容則是個別使用者的個人化內容，例如針對使用者設定檔打造的新聞項目。</span><span class="sxs-lookup"><span data-stu-id="81f93-144">Dynamic content is personalized for an individual user, such as news items that are tailored to a user profile.</span></span> <span data-ttu-id="81f93-145">動態內容不會被快取，因為它是每位使用者的唯一內容，例如購物車內容。</span><span class="sxs-lookup"><span data-stu-id="81f93-145">Dynamic content isn't cached because it's unique to each user, such as shopping cart contents.</span></span> <span data-ttu-id="81f93-146">一般 Web 傳遞可以最佳化整個網站。</span><span class="sxs-lookup"><span data-stu-id="81f93-146">General web delivery can optimize your entire website.</span></span> 

> [!NOTE]
> <span data-ttu-id="81f93-147">如果您使用 Akamai 的 Azure 內容傳遞網路，當平均檔案大小小於 10 MB，您可能會想要使用此最佳化。</span><span class="sxs-lookup"><span data-stu-id="81f93-147">If you use the Azure Content Delivery Network from Akamai, you might want to use this optimization if your average file size is smaller than 10 MB.</span></span> <span data-ttu-id="81f93-148">如果您的平均檔案大小大於 10 MB，請從 [最佳化對象] 下拉式清單選取 [下載大型檔案]。</span><span class="sxs-lookup"><span data-stu-id="81f93-148">If your average file size is larger than 10 MB, select **Large file download** from the **Optimized for** drop-down list.</span></span>

### <a name="general-media-streaming"></a><span data-ttu-id="81f93-149">一般媒體串流處理</span><span class="sxs-lookup"><span data-stu-id="81f93-149">General media streaming</span></span>

<span data-ttu-id="81f93-150">如果您需要在即時串流和點播視訊串流處理使用端點，建議您使用一般媒體串流處理最佳化。</span><span class="sxs-lookup"><span data-stu-id="81f93-150">If you need to use the endpoint for live streaming and video-on-demand streaming, we recommend general media streaming optimization.</span></span>

<span data-ttu-id="81f93-151">媒體串流處理是有時效性的，因為封包晚抵達用戶端會造成檢視體驗降級，例如影片內容經常要緩衝處理。</span><span class="sxs-lookup"><span data-stu-id="81f93-151">Media streaming is time sensitive, because packets that arrive late on the client can cause a degraded viewing experience, such as frequent buffering of video content.</span></span> <span data-ttu-id="81f93-152">媒體串流處理最佳化可降低媒體內容傳遞的延遲，為使用者提供 Smooth Streaming 體驗。</span><span class="sxs-lookup"><span data-stu-id="81f93-152">Media streaming optimization reduces the latency of media content delivery and provides a smooth streaming experience for users.</span></span> 

<span data-ttu-id="81f93-153">Azure 媒體服務的客戶經常發生此狀況。</span><span class="sxs-lookup"><span data-stu-id="81f93-153">This scenario is common for Azure media service customers.</span></span> <span data-ttu-id="81f93-154">當您使用 Azure 媒體服務時，您會取得一個串流端點，可用於即時和隨選資料流處理。</span><span class="sxs-lookup"><span data-stu-id="81f93-154">When you use Azure media services, you get one streaming endpoint that can be used for both live and on-demand streaming.</span></span> <span data-ttu-id="81f93-155">有了這個案例，客戶就不需要在從即時變更為隨選資料流處理時，切換到另一個端點。</span><span class="sxs-lookup"><span data-stu-id="81f93-155">With this scenario, customers don't need to switch to another endpoint when they change from live to on-demand streaming.</span></span> <span data-ttu-id="81f93-156">一般媒體串流處理最佳化支援這種情況。</span><span class="sxs-lookup"><span data-stu-id="81f93-156">General media streaming optimization supports this type of scenario.</span></span>

<span data-ttu-id="81f93-157">Verizon 的 Azure 內容傳遞網路會使用一般 Web 傳遞最佳化類型來傳遞串流處理媒體內容。</span><span class="sxs-lookup"><span data-stu-id="81f93-157">The Azure Content Delivery Network from Verizon uses the general web delivery optimization type to deliver streaming media content.</span></span>

<span data-ttu-id="81f93-158">若要深入了解媒體串流處理最佳化，請參閱[媒體串流處理最佳化](cdn-media-streaming-optimization.md)。</span><span class="sxs-lookup"><span data-stu-id="81f93-158">To learn more about media streaming optimization, see [Media streaming optimization](cdn-media-streaming-optimization.md).</span></span>

### <a name="video-on-demand-media-streaming"></a><span data-ttu-id="81f93-159">點播視訊媒體串流處理</span><span class="sxs-lookup"><span data-stu-id="81f93-159">Video-on-demand media streaming</span></span>

<span data-ttu-id="81f93-160">點播視訊媒體串流處理最佳化會改善點播視訊串流處理內容。</span><span class="sxs-lookup"><span data-stu-id="81f93-160">Video-on-demand media streaming optimization improves video-on-demand streaming content.</span></span> <span data-ttu-id="81f93-161">如果您在點播視訊串流處理使用端點，您可能想要使用此選項。</span><span class="sxs-lookup"><span data-stu-id="81f93-161">If you use an endpoint for video-on-demand streaming, you might want to use this option.</span></span>

<span data-ttu-id="81f93-162">Verizon 的 Azure 內容傳遞網路會使用一般 Web 傳遞最佳化類型來傳遞串流處理媒體內容。</span><span class="sxs-lookup"><span data-stu-id="81f93-162">The Azure Content Delivery Network from Verizon uses the general web delivery optimization type to deliver streaming media content.</span></span>

<span data-ttu-id="81f93-163">若要深入了解媒體串流處理最佳化，請參閱[媒體串流處理最佳化](cdn-media-streaming-optimization.md)。</span><span class="sxs-lookup"><span data-stu-id="81f93-163">To learn more about media streaming optimization, see [Media streaming optimization](cdn-media-streaming-optimization.md).</span></span>

> [!NOTE]
> <span data-ttu-id="81f93-164">如果端點主要是提供點播視訊內容，請使用此最佳化類型。</span><span class="sxs-lookup"><span data-stu-id="81f93-164">If the endpoint primarily serves video-on-demand content, use this optimization type.</span></span> <span data-ttu-id="81f93-165">此最佳化與一般媒體串流處理最佳化的主要差異是連線重試逾時。</span><span class="sxs-lookup"><span data-stu-id="81f93-165">The major difference between this optimization and the general media streaming optimization is the connection retry time-out.</span></span> <span data-ttu-id="81f93-166">逾時遠短於使用即時串流案例。</span><span class="sxs-lookup"><span data-stu-id="81f93-166">The time-out is much shorter to work with live streaming scenarios.</span></span>

### <a name="large-file-download"></a><span data-ttu-id="81f93-167">大型檔案下載</span><span class="sxs-lookup"><span data-stu-id="81f93-167">Large file download</span></span>

<span data-ttu-id="81f93-168">如果您使用 Akamai 的 Azure 內容傳遞網路，您必須使用大型檔案下載才能傳遞超過 1.8 GB 的檔案。</span><span class="sxs-lookup"><span data-stu-id="81f93-168">If you use the Azure Content Delivery Network from Akamai, you must use large file download to deliver files larger than 1.8 GB.</span></span> <span data-ttu-id="81f93-169">Verizon 的 Azure 內容傳遞網路不限制一般 Web 傳遞最佳化的檔案下載大小。</span><span class="sxs-lookup"><span data-stu-id="81f93-169">The Azure Content Delivery Network from Verizon doesn't have a limitation on file download size in its general web delivery optimization.</span></span>

<span data-ttu-id="81f93-170">如果您使用 Akamai 的 Azure 內容傳遞網路，最佳化的大型檔案下載適合超過 10 MB 的內容。</span><span class="sxs-lookup"><span data-stu-id="81f93-170">If you use the Azure Content Delivery Network from Akamai, large file downloads are optimized for content larger than 10 MB.</span></span> <span data-ttu-id="81f93-171">如果您的平均檔案大小小於 10 MB，您可能會想要使用一般 Web 傳遞。</span><span class="sxs-lookup"><span data-stu-id="81f93-171">If your average file size is smaller than 10 MB, you might want to use general web delivery.</span></span> <span data-ttu-id="81f93-172">如果您的平均檔案大小一直都大於 10 MB，為大型檔案分別建立端點可能更有效率。</span><span class="sxs-lookup"><span data-stu-id="81f93-172">If your average files sizes are consistently larger than 10 MB, it might be more efficient to create a separate endpoint for large files.</span></span> <span data-ttu-id="81f93-173">例如，韌體或軟體更新通常是大型檔案。</span><span class="sxs-lookup"><span data-stu-id="81f93-173">For example, firmware or software updates typically are large files.</span></span>

<span data-ttu-id="81f93-174">Verizon 的 Azure 內容傳遞網路會使用一般 Web 傳遞最佳化類型來傳遞串流處理媒體內容。</span><span class="sxs-lookup"><span data-stu-id="81f93-174">The Azure Content Delivery Network from Verizon uses the general web delivery optimization type to deliver streaming media content.</span></span>

<span data-ttu-id="81f93-175">若要深入了解大型檔案最佳化，請參閱[大型檔案最佳化](cdn-large-file-optimization.md)。</span><span class="sxs-lookup"><span data-stu-id="81f93-175">To learn more about large file optimization, see [Large file optimization](cdn-large-file-optimization.md).</span></span>

### <a name="dynamic-site-acceleration"></a><span data-ttu-id="81f93-176">動態網站加速</span><span class="sxs-lookup"><span data-stu-id="81f93-176">Dynamic site acceleration</span></span>

 <span data-ttu-id="81f93-177">Akamai 和 Verizon 的內容傳遞網路設定檔都提供動態網站加速。</span><span class="sxs-lookup"><span data-stu-id="81f93-177">Dynamic site acceleration is available from both Akamai and Verizon Content Delivery Network profiles.</span></span> <span data-ttu-id="81f93-178">此最佳化牽涉到額外使用費用。</span><span class="sxs-lookup"><span data-stu-id="81f93-178">This optimization involves an additional fee to use.</span></span> <span data-ttu-id="81f93-179">如需詳細資訊，請參閱價格頁面。</span><span class="sxs-lookup"><span data-stu-id="81f93-179">For more information, see the pricing page.</span></span>

<span data-ttu-id="81f93-180">動態網站加速包括有益於動態內容延遲和效能的各種技術。</span><span class="sxs-lookup"><span data-stu-id="81f93-180">Dynamic site acceleration includes various techniques that benefit the latency and performance of dynamic content.</span></span> <span data-ttu-id="81f93-181">相關技術包括路由和網路最佳化、TCP 最佳化等等。</span><span class="sxs-lookup"><span data-stu-id="81f93-181">Techniques include route and network optimization, TCP optimization, and more.</span></span> 

<span data-ttu-id="81f93-182">您可以使用此最佳化加速 Web 應用程式，它包含許多無法快取的回應。</span><span class="sxs-lookup"><span data-stu-id="81f93-182">You can use this optimization to accelerate a web app that includes numerous responses that aren't cacheable.</span></span> <span data-ttu-id="81f93-183">範例包括搜尋結果、簽出交易或即時資料。</span><span class="sxs-lookup"><span data-stu-id="81f93-183">Examples are search results, checkout transactions, or real-time data.</span></span> <span data-ttu-id="81f93-184">您可以繼續使用靜態資料的核心 CDN 快取功能。</span><span class="sxs-lookup"><span data-stu-id="81f93-184">You can continue to use core CDN caching capabilities for static data.</span></span> 



