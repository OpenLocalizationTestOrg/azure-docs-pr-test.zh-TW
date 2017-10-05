---
title: "使用 Azure 媒體服務的 DRM 子系統混合式設計 | Microsoft Docs"
description: "本主題討論使用 Azure 媒體服務的 DRM 子系統混合式設計。"
services: media-services
documentationcenter: 
author: willzhan
manager: cfowler
editor: 
ms.assetid: 18213fc1-74f5-4074-a32b-02846fe90601
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: willzhan;juliako
ms.openlocfilehash: 841b1164db6fd1a2c029b98392509c15f23158e2
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="hybrid-design-of-drm-subsystems"></a><span data-ttu-id="c3dcb-103">DRM 子系統的混合式設計</span><span class="sxs-lookup"><span data-stu-id="c3dcb-103">Hybrid design of DRM subsystem(s)</span></span>

<span data-ttu-id="c3dcb-104">本主題討論使用 Azure 媒體服務的 DRM 子系統混合式設計。</span><span class="sxs-lookup"><span data-stu-id="c3dcb-104">This topic discusses hybrid design of DRM subsystem(s) using Azure Media Services.</span></span>

## <a name="overview"></a><span data-ttu-id="c3dcb-105">概觀</span><span class="sxs-lookup"><span data-stu-id="c3dcb-105">Overview</span></span>

<span data-ttu-id="c3dcb-106">Azure 媒體服務提供下列三個 DRM 系統支援：</span><span class="sxs-lookup"><span data-stu-id="c3dcb-106">Azure Media Services provides support for the following three DRM system:</span></span>

* <span data-ttu-id="c3dcb-107">PlayReady</span><span class="sxs-lookup"><span data-stu-id="c3dcb-107">PlayReady</span></span>
* <span data-ttu-id="c3dcb-108">Widevine (模組)</span><span class="sxs-lookup"><span data-stu-id="c3dcb-108">Widevine (Modular)</span></span>
* <span data-ttu-id="c3dcb-109">FairPlay</span><span class="sxs-lookup"><span data-stu-id="c3dcb-109">FairPlay</span></span>

<span data-ttu-id="c3dcb-110">DRM 支援包括 DRM 加密 (動態加密) 和授權傳遞，加上當作瀏覽器玩家 SDK 的所有 3 DRM Azure 媒體播放器支援。</span><span class="sxs-lookup"><span data-stu-id="c3dcb-110">The DRM support includes DRM encryption (dynamic encryption) and license delivery, with Azure Media Player supporting all 3 DRMs as a browser player SDK.</span></span>

<span data-ttu-id="c3dcb-111">如需 DRM/CENC 子系統設計和實作的詳細處理方式，請參閱[使用多重 DRM 和存取控制的 CENC](media-services-cenc-with-multidrm-access-control.md) 一文。</span><span class="sxs-lookup"><span data-stu-id="c3dcb-111">For a detailed treatment of DRM/CENC subsystem design and implementation, please see the document titled [CENC with Multi-DRM and Access Control](media-services-cenc-with-multidrm-access-control.md).</span></span>

<span data-ttu-id="c3dcb-112">雖然我們為三種 DRM 系統提供完整的支援，但有時候客戶在 Azure 媒體服務之外，也需要使用自己的基礎結構/子系統的各種組件建置混合式的 DRM 子系統。</span><span class="sxs-lookup"><span data-stu-id="c3dcb-112">Although we offer complete support for three DRM systems, sometimes customers need to use various parts of their own infrastructure/subsystems in addition to Azure Media Services to build a hybrid DRM subsystem.</span></span>

<span data-ttu-id="c3dcb-113">以下是客戶常問的一些問題：</span><span class="sxs-lookup"><span data-stu-id="c3dcb-113">Below are some common questions asked by customers:</span></span>

* <span data-ttu-id="c3dcb-114">「我可以使用自己的 DRM 授權伺服器嗎？」</span><span class="sxs-lookup"><span data-stu-id="c3dcb-114">"Can I use my own DRM license servers?"</span></span> <span data-ttu-id="c3dcb-115">(在此例中，客戶投資了內嵌商務邏輯的 DRM 授權伺服器叢集。)</span><span class="sxs-lookup"><span data-stu-id="c3dcb-115">(In this case, customers have invested in DRM license server farm with embedded business logic).</span></span>
* <span data-ttu-id="c3dcb-116">「我可以只使用 Azure 媒體服務的 DRM 授權傳遞，但 AMS 中不裝載內容嗎？」</span><span class="sxs-lookup"><span data-stu-id="c3dcb-116">"Can I use only your DRM license delivery in Azure Media Services without hosting content in AMS?"</span></span>

## <a name="modularity-of-the-ams-drm-platform"></a><span data-ttu-id="c3dcb-117">AMS DRM 平台的模組化</span><span class="sxs-lookup"><span data-stu-id="c3dcb-117">Modularity of the AMS DRM platform</span></span>

<span data-ttu-id="c3dcb-118">Azure 媒體服務 DRM 是全面雲端視訊平台的一部分，設計富彈性和模組化。</span><span class="sxs-lookup"><span data-stu-id="c3dcb-118">As part of a comprehensive cloud video platform, Azure Media Services DRM has a design with flexibility and modularity in mind.</span></span> <span data-ttu-id="c3dcb-119">您可以使用 Azure 媒體服務搭配下表所述的任何不同組合 (後文有資料表所用標記法說明)。</span><span class="sxs-lookup"><span data-stu-id="c3dcb-119">You can use Azure Media Services with any of the following different combinations described in the table below (an explanation of the notation used in the table follows).</span></span> 

|<span data-ttu-id="c3dcb-120">**內容裝載與來源**</span><span class="sxs-lookup"><span data-stu-id="c3dcb-120">**Content hosting & origin**</span></span>|<span data-ttu-id="c3dcb-121">**內容加密**</span><span class="sxs-lookup"><span data-stu-id="c3dcb-121">**Content encryption**</span></span>|<span data-ttu-id="c3dcb-122">**DRM 授權傳遞**</span><span class="sxs-lookup"><span data-stu-id="c3dcb-122">**DRM license delivery**</span></span>|
|---|---|---|
|<span data-ttu-id="c3dcb-123">AMS</span><span class="sxs-lookup"><span data-stu-id="c3dcb-123">AMS</span></span>|<span data-ttu-id="c3dcb-124">AMS</span><span class="sxs-lookup"><span data-stu-id="c3dcb-124">AMS</span></span>|<span data-ttu-id="c3dcb-125">AMS</span><span class="sxs-lookup"><span data-stu-id="c3dcb-125">AMS</span></span>|
|<span data-ttu-id="c3dcb-126">AMS</span><span class="sxs-lookup"><span data-stu-id="c3dcb-126">AMS</span></span>|<span data-ttu-id="c3dcb-127">AMS</span><span class="sxs-lookup"><span data-stu-id="c3dcb-127">AMS</span></span>|<span data-ttu-id="c3dcb-128">協力廠商</span><span class="sxs-lookup"><span data-stu-id="c3dcb-128">Third-party</span></span>|
|<span data-ttu-id="c3dcb-129">AMS</span><span class="sxs-lookup"><span data-stu-id="c3dcb-129">AMS</span></span>|<span data-ttu-id="c3dcb-130">協力廠商</span><span class="sxs-lookup"><span data-stu-id="c3dcb-130">Third-party</span></span>|<span data-ttu-id="c3dcb-131">AMS</span><span class="sxs-lookup"><span data-stu-id="c3dcb-131">AMS</span></span>|
|<span data-ttu-id="c3dcb-132">AMS</span><span class="sxs-lookup"><span data-stu-id="c3dcb-132">AMS</span></span>|<span data-ttu-id="c3dcb-133">協力廠商</span><span class="sxs-lookup"><span data-stu-id="c3dcb-133">Third-party</span></span>|<span data-ttu-id="c3dcb-134">協力廠商</span><span class="sxs-lookup"><span data-stu-id="c3dcb-134">Third-party</span></span>|
|<span data-ttu-id="c3dcb-135">協力廠商</span><span class="sxs-lookup"><span data-stu-id="c3dcb-135">Third-party</span></span>|<span data-ttu-id="c3dcb-136">協力廠商</span><span class="sxs-lookup"><span data-stu-id="c3dcb-136">Third-party</span></span>|<span data-ttu-id="c3dcb-137">AMS</span><span class="sxs-lookup"><span data-stu-id="c3dcb-137">AMS</span></span>|

### <a name="content-hosting--origin"></a><span data-ttu-id="c3dcb-138">內容裝載與來源</span><span class="sxs-lookup"><span data-stu-id="c3dcb-138">Content hosting & origin</span></span>

* <span data-ttu-id="c3dcb-139">AMS：影片資產裝載於 AMS 中，而資料流是透過 AMS 串流端點 (但不一定是動態封裝)。</span><span class="sxs-lookup"><span data-stu-id="c3dcb-139">AMS: video asset is hosted in AMS and streaming is through AMS streaming endpoints (but not necessarily dynamic packaging).</span></span>
* <span data-ttu-id="c3dcb-140">協力廠商：影片是在 AMS 之外的協力廠商資料流平台上裝載和傳遞。</span><span class="sxs-lookup"><span data-stu-id="c3dcb-140">Third-party: video is hosted and delivered on a third-party streaming platform outside of AMS.</span></span>

### <a name="content-encryption"></a><span data-ttu-id="c3dcb-141">內容加密</span><span class="sxs-lookup"><span data-stu-id="c3dcb-141">Content encryption</span></span>

* <span data-ttu-id="c3dcb-142">AMS：內容加密是由 AMS 動態加密動態/隨選執行。</span><span class="sxs-lookup"><span data-stu-id="c3dcb-142">AMS: content encryption is performed dynamically/on-demand by AMS dynamic encryption.</span></span>
* <span data-ttu-id="c3dcb-143">協力廠商：內容加密是使用前置處理工作流程在 AMS 之外執行。</span><span class="sxs-lookup"><span data-stu-id="c3dcb-143">Third-party: content encryption is performed outside of AMS using a pre-processing workflow.</span></span>

### <a name="drm-license-delivery"></a><span data-ttu-id="c3dcb-144">DRM 授權傳遞</span><span class="sxs-lookup"><span data-stu-id="c3dcb-144">DRM license delivery</span></span>

* <span data-ttu-id="c3dcb-145">AMS：DRM 授權是由 AMS 授權傳遞服務傳遞。</span><span class="sxs-lookup"><span data-stu-id="c3dcb-145">AMS: DRM license is delivered by AMS license delivery service.</span></span>
* <span data-ttu-id="c3dcb-146">協力廠商：DRM 授權是由 AMS 之外的協力廠商 DRM 授權伺服器傳遞。</span><span class="sxs-lookup"><span data-stu-id="c3dcb-146">Third-party: DRM license is delivered by a third-party DRM license server outside of AMS.</span></span>

## <a name="configure-based-on-your-hybrid-scenario"></a><span data-ttu-id="c3dcb-147">根據混合式案例設定</span><span class="sxs-lookup"><span data-stu-id="c3dcb-147">Configure based on your hybrid scenario</span></span>

### <a name="content-key"></a><span data-ttu-id="c3dcb-148">內容金鑰</span><span class="sxs-lookup"><span data-stu-id="c3dcb-148">Content key</span></span>

<span data-ttu-id="c3dcb-149">透過內容金鑰的設定，您可以控制 AMS 動態加密和 AMS 授權傳遞服務的下列屬性：</span><span class="sxs-lookup"><span data-stu-id="c3dcb-149">Through configuration of a content key, you can control the following attributes of both AMS dynamic encryption and AMS license delivery service:</span></span>

* <span data-ttu-id="c3dcb-150">用於動態 DRM 加密的內容金鑰。</span><span class="sxs-lookup"><span data-stu-id="c3dcb-150">The content key used for dynamic DRM encryption.</span></span>
* <span data-ttu-id="c3dcb-151">由授權傳遞服務所傳遞的 DRM 授權內容：權限、內容金鑰和限制。</span><span class="sxs-lookup"><span data-stu-id="c3dcb-151">DRM license content to be delivered by license delivery services: rights, content key and restrictions.</span></span>
* <span data-ttu-id="c3dcb-152">**內容金鑰授權原則限制**的類型：開啟、IP 或權杖限制。</span><span class="sxs-lookup"><span data-stu-id="c3dcb-152">Type of **content key authorization policy restriction**: open, IP, or token restriction.</span></span>
* <span data-ttu-id="c3dcb-153">如果**使用內容金鑰授權原則限制**的**權杖**類型，則必須符合**內容金鑰授權原則限制**才能簽發授權。</span><span class="sxs-lookup"><span data-stu-id="c3dcb-153">If **token** type of **content key authorization policy restriction is used**, the **content key authorization policy restriction** must be met before a license is issued.</span></span>

### <a name="asset-delivery-policy"></a><span data-ttu-id="c3dcb-154">資產傳遞原則</span><span class="sxs-lookup"><span data-stu-id="c3dcb-154">Asset delivery policy</span></span>

<span data-ttu-id="c3dcb-155">透過資產傳遞原則設定，您可以控制 AMS 動態封裝程式和 AMS 串流端點動態加密所使用的下列屬性：</span><span class="sxs-lookup"><span data-stu-id="c3dcb-155">Through configuration of an asset delivery policy, you can control the following attributes used by AMS dynamic packager and dynamic encryption of an AMS streaming endpoint:</span></span>

* <span data-ttu-id="c3dcb-156">串流處理通訊協定和 DRM 加密的組合，例如 CENC (PlayReady 和 Widevine) 下的 DASH、PlayReady 下的 Smooth Streaming、Widevine 或 PlayReady 下的 HLS。</span><span class="sxs-lookup"><span data-stu-id="c3dcb-156">Streaming protocol and DRM encryption combination, such as DASH under CENC (PlayReady and Widevine), smooth streaming under PlayReady, HLS under Widevine or PlayReady.</span></span>
* <span data-ttu-id="c3dcb-157">每個有關 DRM 的預設/內嵌授權傳遞 URL。</span><span class="sxs-lookup"><span data-stu-id="c3dcb-157">The default/embedded license delivery URLs for each of the involved DRMs.</span></span>
* <span data-ttu-id="c3dcb-158">無論 DASH MPD 或 HLS 播放清單的授權取得 URL (LA_URL) 是否分別包含 Widevine 和 FairPlay 的索引鍵識別碼 (KID) 查詢字串。</span><span class="sxs-lookup"><span data-stu-id="c3dcb-158">Whether license acquisition URLs (LA_URLs) in DASH MPD or HLS playlist contain query string of key ID (KID) for Widevine and FairPlay, respectively.</span></span>

## <a name="scenarios-and-samples"></a><span data-ttu-id="c3dcb-159">案例與範例</span><span class="sxs-lookup"><span data-stu-id="c3dcb-159">Scenarios and samples</span></span>

<span data-ttu-id="c3dcb-160">根據上一節的說明，下列五個混合式案例分別使用**內容金鑰**-**資產傳遞原則**設定組合 (資料表最後一個資料行中提及的範例)：</span><span class="sxs-lookup"><span data-stu-id="c3dcb-160">Based on the explanations in the previous section, the following five hybrid scenarios use respective **Content key**-**Asset delivery policy** configuration combinations (the samples mentioned in the last column follow the table):</span></span>

|<span data-ttu-id="c3dcb-161">**內容裝載與來源**</span><span class="sxs-lookup"><span data-stu-id="c3dcb-161">**Content hosting & origin**</span></span>|<span data-ttu-id="c3dcb-162">**DRM 加密**</span><span class="sxs-lookup"><span data-stu-id="c3dcb-162">**DRM encryption**</span></span>|<span data-ttu-id="c3dcb-163">**DRM 授權傳遞**</span><span class="sxs-lookup"><span data-stu-id="c3dcb-163">**DRM license delivery**</span></span>|<span data-ttu-id="c3dcb-164">**設定內容金鑰**</span><span class="sxs-lookup"><span data-stu-id="c3dcb-164">**Configure content key**</span></span>|<span data-ttu-id="c3dcb-165">**設定資產傳遞原則**</span><span class="sxs-lookup"><span data-stu-id="c3dcb-165">**Configure asset delivery policy**</span></span>|<span data-ttu-id="c3dcb-166">**範例**</span><span class="sxs-lookup"><span data-stu-id="c3dcb-166">**Sample**</span></span>|
|---|---|---|---|---|---|
|<span data-ttu-id="c3dcb-167">AMS</span><span class="sxs-lookup"><span data-stu-id="c3dcb-167">AMS</span></span>|<span data-ttu-id="c3dcb-168">AMS</span><span class="sxs-lookup"><span data-stu-id="c3dcb-168">AMS</span></span>|<span data-ttu-id="c3dcb-169">AMS</span><span class="sxs-lookup"><span data-stu-id="c3dcb-169">AMS</span></span>|<span data-ttu-id="c3dcb-170">是</span><span class="sxs-lookup"><span data-stu-id="c3dcb-170">Yes</span></span>|<span data-ttu-id="c3dcb-171">是</span><span class="sxs-lookup"><span data-stu-id="c3dcb-171">Yes</span></span>|<span data-ttu-id="c3dcb-172">範例 1</span><span class="sxs-lookup"><span data-stu-id="c3dcb-172">Sample 1</span></span>|
|<span data-ttu-id="c3dcb-173">AMS</span><span class="sxs-lookup"><span data-stu-id="c3dcb-173">AMS</span></span>|<span data-ttu-id="c3dcb-174">AMS</span><span class="sxs-lookup"><span data-stu-id="c3dcb-174">AMS</span></span>|<span data-ttu-id="c3dcb-175">協力廠商</span><span class="sxs-lookup"><span data-stu-id="c3dcb-175">Third-party</span></span>|<span data-ttu-id="c3dcb-176">是</span><span class="sxs-lookup"><span data-stu-id="c3dcb-176">Yes</span></span>|<span data-ttu-id="c3dcb-177">是</span><span class="sxs-lookup"><span data-stu-id="c3dcb-177">Yes</span></span>|<span data-ttu-id="c3dcb-178">範例 2</span><span class="sxs-lookup"><span data-stu-id="c3dcb-178">Sample 2</span></span>|
|<span data-ttu-id="c3dcb-179">AMS</span><span class="sxs-lookup"><span data-stu-id="c3dcb-179">AMS</span></span>|<span data-ttu-id="c3dcb-180">協力廠商</span><span class="sxs-lookup"><span data-stu-id="c3dcb-180">Third-party</span></span>|<span data-ttu-id="c3dcb-181">AMS</span><span class="sxs-lookup"><span data-stu-id="c3dcb-181">AMS</span></span>|<span data-ttu-id="c3dcb-182">是</span><span class="sxs-lookup"><span data-stu-id="c3dcb-182">Yes</span></span>|<span data-ttu-id="c3dcb-183">否</span><span class="sxs-lookup"><span data-stu-id="c3dcb-183">No</span></span>|<span data-ttu-id="c3dcb-184">範例 3</span><span class="sxs-lookup"><span data-stu-id="c3dcb-184">Sample 3</span></span>|
|<span data-ttu-id="c3dcb-185">AMS</span><span class="sxs-lookup"><span data-stu-id="c3dcb-185">AMS</span></span>|<span data-ttu-id="c3dcb-186">協力廠商</span><span class="sxs-lookup"><span data-stu-id="c3dcb-186">Third-party</span></span>|<span data-ttu-id="c3dcb-187">外部</span><span class="sxs-lookup"><span data-stu-id="c3dcb-187">Outside</span></span>|<span data-ttu-id="c3dcb-188">否</span><span class="sxs-lookup"><span data-stu-id="c3dcb-188">No</span></span>|<span data-ttu-id="c3dcb-189">否</span><span class="sxs-lookup"><span data-stu-id="c3dcb-189">No</span></span>|<span data-ttu-id="c3dcb-190">範例 4</span><span class="sxs-lookup"><span data-stu-id="c3dcb-190">Sample 4</span></span>|
|<span data-ttu-id="c3dcb-191">協力廠商</span><span class="sxs-lookup"><span data-stu-id="c3dcb-191">Third-party</span></span>|<span data-ttu-id="c3dcb-192">協力廠商</span><span class="sxs-lookup"><span data-stu-id="c3dcb-192">Third-party</span></span>|<span data-ttu-id="c3dcb-193">AMS</span><span class="sxs-lookup"><span data-stu-id="c3dcb-193">AMS</span></span>|<span data-ttu-id="c3dcb-194">是</span><span class="sxs-lookup"><span data-stu-id="c3dcb-194">Yes</span></span>|<span data-ttu-id="c3dcb-195">否</span><span class="sxs-lookup"><span data-stu-id="c3dcb-195">No</span></span>|    

<span data-ttu-id="c3dcb-196">在範例中，PlayReady 保護對 DASH 和 Smooth Streaming 都有效。</span><span class="sxs-lookup"><span data-stu-id="c3dcb-196">In the samples, PlayReady protection works for both DASH and smooth streaming.</span></span> <span data-ttu-id="c3dcb-197">下列的影片 URL 是 Smooth Streaming URL。</span><span class="sxs-lookup"><span data-stu-id="c3dcb-197">The video URLs below are smooth streaming URLs.</span></span> <span data-ttu-id="c3dcb-198">若要取得對應的 DASH URL，只要加上 "(format=mpd-time-csf)" 即可。</span><span class="sxs-lookup"><span data-stu-id="c3dcb-198">To get the corresponding DASH URLs, just append "(format=mpd-time-csf)".</span></span> <span data-ttu-id="c3dcb-199">您可以使用 [Azure 媒體測試播放器](http://aka.ms/amtest)在瀏覽器中測試。</span><span class="sxs-lookup"><span data-stu-id="c3dcb-199">You could use the [azure media test player](http://aka.ms/amtest) to test in a browser.</span></span> <span data-ttu-id="c3dcb-200">它可讓您設定要在哪些技術之下使用哪一個串流處理通訊協定。</span><span class="sxs-lookup"><span data-stu-id="c3dcb-200">It allows you to configure which streaming protocol to use, under which tech.</span></span> <span data-ttu-id="c3dcb-201">Windows 10 的 IE11 和 MS Edge 都透過 EME 支援 PlayReady。</span><span class="sxs-lookup"><span data-stu-id="c3dcb-201">IE11 and MS Edge on Windows 10 support PlayReady through EME.</span></span> <span data-ttu-id="c3dcb-202">如需詳細資訊，請參閱[測試工具的詳細資料](https://blogs.msdn.microsoft.com/playready4/2016/02/28/azure-media-test-tool/)。</span><span class="sxs-lookup"><span data-stu-id="c3dcb-202">For more information, see [details about the test tool](https://blogs.msdn.microsoft.com/playready4/2016/02/28/azure-media-test-tool/).</span></span>

### <a name="sample-1"></a><span data-ttu-id="c3dcb-203">範例 1</span><span class="sxs-lookup"><span data-stu-id="c3dcb-203">Sample 1</span></span>

* <span data-ttu-id="c3dcb-204">來源 (基底) URL：https://willzhanmswest.streaming.mediaservices.windows.net/1efbd6bb-1e66-4e53-88c3-f7e5657a9bbd/RussianWaltz.ism/manifest</span><span class="sxs-lookup"><span data-stu-id="c3dcb-204">Source (base) URL: https://willzhanmswest.streaming.mediaservices.windows.net/1efbd6bb-1e66-4e53-88c3-f7e5657a9bbd/RussianWaltz.ism/manifest</span></span> 
* <span data-ttu-id="c3dcb-205">PlayReady LA_URL (DASH & Smooth)：https://willzhanmswest.keydelivery.mediaservices.windows.net/PlayReady/</span><span class="sxs-lookup"><span data-stu-id="c3dcb-205">PlayReady LA_URL (DASH & smooth): https://willzhanmswest.keydelivery.mediaservices.windows.net/PlayReady/</span></span> 
* <span data-ttu-id="c3dcb-206">Widevine LA_URL (DASH)：https://willzhanmswest.keydelivery.mediaservices.windows.net/Widevine/?kid=78de73ae-6d0f-470a-8f13-5c91f7c4</span><span class="sxs-lookup"><span data-stu-id="c3dcb-206">Widevine LA_URL (DASH): https://willzhanmswest.keydelivery.mediaservices.windows.net/Widevine/?kid=78de73ae-6d0f-470a-8f13-5c91f7c4</span></span> 
* <span data-ttu-id="c3dcb-207">FairPlay LA_URL (HLS)：https://willzhanmswest.keydelivery.mediaservices.windows.net/FairPlay/?kid=ba7e8fb0-ee22-4291-9654-6222ac611bd8</span><span class="sxs-lookup"><span data-stu-id="c3dcb-207">FairPlay LA_URL (HLS): https://willzhanmswest.keydelivery.mediaservices.windows.net/FairPlay/?kid=ba7e8fb0-ee22-4291-9654-6222ac611bd8</span></span> 

### <a name="sample-2"></a><span data-ttu-id="c3dcb-208">範例 2</span><span class="sxs-lookup"><span data-stu-id="c3dcb-208">Sample 2</span></span>

* <span data-ttu-id="c3dcb-209">來源 (基底) URL：http://willzhanmswest.streaming.mediaservices.windows.net/1a670626-4515-49ee-9e7f-cd50853e41d8/Microsoft_HoloLens_TransformYourWorld_816p23.ism/Manifest</span><span class="sxs-lookup"><span data-stu-id="c3dcb-209">Source (base) URL: http://willzhanmswest.streaming.mediaservices.windows.net/1a670626-4515-49ee-9e7f-cd50853e41d8/Microsoft_HoloLens_TransformYourWorld_816p23.ism/Manifest</span></span> 
* <span data-ttu-id="c3dcb-210">PlayReady LA_URL (DASH & Smooth)：http://willzhan12.cloudapp.net/PlayReady/RightsManager.asmx</span><span class="sxs-lookup"><span data-stu-id="c3dcb-210">PlayReady LA_URL (DASH & smooth): http://willzhan12.cloudapp.net/PlayReady/RightsManager.asmx</span></span> 

### <a name="sample-3"></a><span data-ttu-id="c3dcb-211">範例 3</span><span class="sxs-lookup"><span data-stu-id="c3dcb-211">Sample 3</span></span>

* <span data-ttu-id="c3dcb-212">來源 URL：https://willzhanmswest.streaming.mediaservices.windows.net/8d078cf8-d621-406c-84ca-88e6b9454acc/20150807-bridges-2500.ism/manifest</span><span class="sxs-lookup"><span data-stu-id="c3dcb-212">Source URL: https://willzhanmswest.streaming.mediaservices.windows.net/8d078cf8-d621-406c-84ca-88e6b9454acc/20150807-bridges-2500.ism/manifest</span></span> 
* <span data-ttu-id="c3dcb-213">PlayReady LA_URL (DASH & Smooth)：https://willzhanmswest.keydelivery.mediaservices.windows.net/PlayReady/</span><span class="sxs-lookup"><span data-stu-id="c3dcb-213">PlayReady LA_URL (DASH & smooth): https://willzhanmswest.keydelivery.mediaservices.windows.net/PlayReady/</span></span> 

### <a name="sample-4"></a><span data-ttu-id="c3dcb-214">範例 4</span><span class="sxs-lookup"><span data-stu-id="c3dcb-214">Sample 4</span></span>

* <span data-ttu-id="c3dcb-215">來源 URL：https://willzhanmswest.streaming.mediaservices.windows.net/7c085a59-ae9a-411e-842c-ef10f96c3f89/20150807-bridges-2500.ism/manifest</span><span class="sxs-lookup"><span data-stu-id="c3dcb-215">Source URL: https://willzhanmswest.streaming.mediaservices.windows.net/7c085a59-ae9a-411e-842c-ef10f96c3f89/20150807-bridges-2500.ism/manifest</span></span> 
* <span data-ttu-id="c3dcb-216">PlayReady LA_URL (DASH & Smooth)：https://willzhan12.cloudapp.net/playready/rightsmanager.asmx</span><span class="sxs-lookup"><span data-stu-id="c3dcb-216">PlayReady LA_URL (DASH & smooth): https://willzhan12.cloudapp.net/playready/rightsmanager.asmx</span></span> 

## <a name="summary"></a><span data-ttu-id="c3dcb-217">摘要</span><span class="sxs-lookup"><span data-stu-id="c3dcb-217">Summary</span></span>

<span data-ttu-id="c3dcb-218">總而言之，Azure 媒體服務 DRM 元件富有彈性，只要如本主題所述正確設定內容金鑰與資產傳遞原則，就可以在混合式案例中使用它們。</span><span class="sxs-lookup"><span data-stu-id="c3dcb-218">In summary, Azure Media Services DRM components are flexible, you can use them in a hybrid scenario by properly configuring content key and asset delivery policy, as described in this topic.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c3dcb-219">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c3dcb-219">Next steps</span></span>
<span data-ttu-id="c3dcb-220">檢視媒體服務學習路徑。</span><span class="sxs-lookup"><span data-stu-id="c3dcb-220">View Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="c3dcb-221">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="c3dcb-221">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

