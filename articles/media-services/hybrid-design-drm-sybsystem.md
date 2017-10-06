---
title: "使用 Azure Media Services 的 DRM 子系統 aaaHybrid 設計 |Microsoft 文件"
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
ms.openlocfilehash: 4206248420ccd4dbfc9a87a86f4763534c6254a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="hybrid-design-of-drm-subsystems"></a><span data-ttu-id="d1c4d-103">DRM 子系統的混合式設計</span><span class="sxs-lookup"><span data-stu-id="d1c4d-103">Hybrid design of DRM subsystem(s)</span></span>

<span data-ttu-id="d1c4d-104">本主題討論使用 Azure 媒體服務的 DRM 子系統混合式設計。</span><span class="sxs-lookup"><span data-stu-id="d1c4d-104">This topic discusses hybrid design of DRM subsystem(s) using Azure Media Services.</span></span>

## <a name="overview"></a><span data-ttu-id="d1c4d-105">概觀</span><span class="sxs-lookup"><span data-stu-id="d1c4d-105">Overview</span></span>

<span data-ttu-id="d1c4d-106">Azure Media Services 提供下列三個 DRM 系統 hello 支援：</span><span class="sxs-lookup"><span data-stu-id="d1c4d-106">Azure Media Services provides support for hello following three DRM system:</span></span>

* <span data-ttu-id="d1c4d-107">PlayReady</span><span class="sxs-lookup"><span data-stu-id="d1c4d-107">PlayReady</span></span>
* <span data-ttu-id="d1c4d-108">Widevine (模組)</span><span class="sxs-lookup"><span data-stu-id="d1c4d-108">Widevine (Modular)</span></span>
* <span data-ttu-id="d1c4d-109">FairPlay</span><span class="sxs-lookup"><span data-stu-id="d1c4d-109">FairPlay</span></span>

<span data-ttu-id="d1c4d-110">hello DRM 支援包括 DRM 加密 （動態加密） 和授權傳遞，使用 Azure Media Player 支援所有 3 DRMs 為瀏覽器播放程式 SDK。</span><span class="sxs-lookup"><span data-stu-id="d1c4d-110">hello DRM support includes DRM encryption (dynamic encryption) and license delivery, with Azure Media Player supporting all 3 DRMs as a browser player SDK.</span></span>

<span data-ttu-id="d1c4d-111">DRM/CENC 子系統設計和實作的詳細處理方式，請參閱標題為 hello 文件[存取控制與多重 DRM CENC](media-services-cenc-with-multidrm-access-control.md)。</span><span class="sxs-lookup"><span data-stu-id="d1c4d-111">For a detailed treatment of DRM/CENC subsystem design and implementation, please see hello document titled [CENC with Multi-DRM and Access Control](media-services-cenc-with-multidrm-access-control.md).</span></span>

<span data-ttu-id="d1c4d-112">雖然我們提供三種 DRM 系統的完整支援，有時候客戶必須 toouse 自己基礎結構/子系統加法 tooAzure Media Services toobuild 的混合式 DRM 子系統中的各個部分。</span><span class="sxs-lookup"><span data-stu-id="d1c4d-112">Although we offer complete support for three DRM systems, sometimes customers need toouse various parts of their own infrastructure/subsystems in addition tooAzure Media Services toobuild a hybrid DRM subsystem.</span></span>

<span data-ttu-id="d1c4d-113">以下是客戶常問的一些問題：</span><span class="sxs-lookup"><span data-stu-id="d1c4d-113">Below are some common questions asked by customers:</span></span>

* <span data-ttu-id="d1c4d-114">「我可以使用自己的 DRM 授權伺服器嗎？」</span><span class="sxs-lookup"><span data-stu-id="d1c4d-114">"Can I use my own DRM license servers?"</span></span> <span data-ttu-id="d1c4d-115">(在此例中，客戶投資了內嵌商務邏輯的 DRM 授權伺服器叢集。)</span><span class="sxs-lookup"><span data-stu-id="d1c4d-115">(In this case, customers have invested in DRM license server farm with embedded business logic).</span></span>
* <span data-ttu-id="d1c4d-116">「我可以只使用 Azure 媒體服務的 DRM 授權傳遞，但 AMS 中不裝載內容嗎？」</span><span class="sxs-lookup"><span data-stu-id="d1c4d-116">"Can I use only your DRM license delivery in Azure Media Services without hosting content in AMS?"</span></span>

## <a name="modularity-of-hello-ams-drm-platform"></a><span data-ttu-id="d1c4d-117">Hello AMS DRM 平台的模組化</span><span class="sxs-lookup"><span data-stu-id="d1c4d-117">Modularity of hello AMS DRM platform</span></span>

<span data-ttu-id="d1c4d-118">Azure 媒體服務 DRM 是全面雲端視訊平台的一部分，設計富彈性和模組化。</span><span class="sxs-lookup"><span data-stu-id="d1c4d-118">As part of a comprehensive cloud video platform, Azure Media Services DRM has a design with flexibility and modularity in mind.</span></span> <span data-ttu-id="d1c4d-119">您可以使用 Azure Media Services 與任何 hello 遵循 hello 表 （遵循用於 hello 資料表中的 hello 標記法的說明） 中描述的不同組合。</span><span class="sxs-lookup"><span data-stu-id="d1c4d-119">You can use Azure Media Services with any of hello following different combinations described in hello table below (an explanation of hello notation used in hello table follows).</span></span> 

|<span data-ttu-id="d1c4d-120">**內容裝載與來源**</span><span class="sxs-lookup"><span data-stu-id="d1c4d-120">**Content hosting & origin**</span></span>|<span data-ttu-id="d1c4d-121">**內容加密**</span><span class="sxs-lookup"><span data-stu-id="d1c4d-121">**Content encryption**</span></span>|<span data-ttu-id="d1c4d-122">**DRM 授權傳遞**</span><span class="sxs-lookup"><span data-stu-id="d1c4d-122">**DRM license delivery**</span></span>|
|---|---|---|
|<span data-ttu-id="d1c4d-123">AMS</span><span class="sxs-lookup"><span data-stu-id="d1c4d-123">AMS</span></span>|<span data-ttu-id="d1c4d-124">AMS</span><span class="sxs-lookup"><span data-stu-id="d1c4d-124">AMS</span></span>|<span data-ttu-id="d1c4d-125">AMS</span><span class="sxs-lookup"><span data-stu-id="d1c4d-125">AMS</span></span>|
|<span data-ttu-id="d1c4d-126">AMS</span><span class="sxs-lookup"><span data-stu-id="d1c4d-126">AMS</span></span>|<span data-ttu-id="d1c4d-127">AMS</span><span class="sxs-lookup"><span data-stu-id="d1c4d-127">AMS</span></span>|<span data-ttu-id="d1c4d-128">協力廠商</span><span class="sxs-lookup"><span data-stu-id="d1c4d-128">Third-party</span></span>|
|<span data-ttu-id="d1c4d-129">AMS</span><span class="sxs-lookup"><span data-stu-id="d1c4d-129">AMS</span></span>|<span data-ttu-id="d1c4d-130">協力廠商</span><span class="sxs-lookup"><span data-stu-id="d1c4d-130">Third-party</span></span>|<span data-ttu-id="d1c4d-131">AMS</span><span class="sxs-lookup"><span data-stu-id="d1c4d-131">AMS</span></span>|
|<span data-ttu-id="d1c4d-132">AMS</span><span class="sxs-lookup"><span data-stu-id="d1c4d-132">AMS</span></span>|<span data-ttu-id="d1c4d-133">協力廠商</span><span class="sxs-lookup"><span data-stu-id="d1c4d-133">Third-party</span></span>|<span data-ttu-id="d1c4d-134">協力廠商</span><span class="sxs-lookup"><span data-stu-id="d1c4d-134">Third-party</span></span>|
|<span data-ttu-id="d1c4d-135">協力廠商</span><span class="sxs-lookup"><span data-stu-id="d1c4d-135">Third-party</span></span>|<span data-ttu-id="d1c4d-136">協力廠商</span><span class="sxs-lookup"><span data-stu-id="d1c4d-136">Third-party</span></span>|<span data-ttu-id="d1c4d-137">AMS</span><span class="sxs-lookup"><span data-stu-id="d1c4d-137">AMS</span></span>|

### <a name="content-hosting--origin"></a><span data-ttu-id="d1c4d-138">內容裝載與來源</span><span class="sxs-lookup"><span data-stu-id="d1c4d-138">Content hosting & origin</span></span>

* <span data-ttu-id="d1c4d-139">AMS：影片資產裝載於 AMS 中，而資料流是透過 AMS 串流端點 (但不一定是動態封裝)。</span><span class="sxs-lookup"><span data-stu-id="d1c4d-139">AMS: video asset is hosted in AMS and streaming is through AMS streaming endpoints (but not necessarily dynamic packaging).</span></span>
* <span data-ttu-id="d1c4d-140">協力廠商：影片是在 AMS 之外的協力廠商資料流平台上裝載和傳遞。</span><span class="sxs-lookup"><span data-stu-id="d1c4d-140">Third-party: video is hosted and delivered on a third-party streaming platform outside of AMS.</span></span>

### <a name="content-encryption"></a><span data-ttu-id="d1c4d-141">內容加密</span><span class="sxs-lookup"><span data-stu-id="d1c4d-141">Content encryption</span></span>

* <span data-ttu-id="d1c4d-142">AMS：內容加密是由 AMS 動態加密動態/隨選執行。</span><span class="sxs-lookup"><span data-stu-id="d1c4d-142">AMS: content encryption is performed dynamically/on-demand by AMS dynamic encryption.</span></span>
* <span data-ttu-id="d1c4d-143">協力廠商：內容加密是使用前置處理工作流程在 AMS 之外執行。</span><span class="sxs-lookup"><span data-stu-id="d1c4d-143">Third-party: content encryption is performed outside of AMS using a pre-processing workflow.</span></span>

### <a name="drm-license-delivery"></a><span data-ttu-id="d1c4d-144">DRM 授權傳遞</span><span class="sxs-lookup"><span data-stu-id="d1c4d-144">DRM license delivery</span></span>

* <span data-ttu-id="d1c4d-145">AMS：DRM 授權是由 AMS 授權傳遞服務傳遞。</span><span class="sxs-lookup"><span data-stu-id="d1c4d-145">AMS: DRM license is delivered by AMS license delivery service.</span></span>
* <span data-ttu-id="d1c4d-146">協力廠商：DRM 授權是由 AMS 之外的協力廠商 DRM 授權伺服器傳遞。</span><span class="sxs-lookup"><span data-stu-id="d1c4d-146">Third-party: DRM license is delivered by a third-party DRM license server outside of AMS.</span></span>

## <a name="configure-based-on-your-hybrid-scenario"></a><span data-ttu-id="d1c4d-147">根據混合式案例設定</span><span class="sxs-lookup"><span data-stu-id="d1c4d-147">Configure based on your hybrid scenario</span></span>

### <a name="content-key"></a><span data-ttu-id="d1c4d-148">內容金鑰</span><span class="sxs-lookup"><span data-stu-id="d1c4d-148">Content key</span></span>

<span data-ttu-id="d1c4d-149">透過組態的內容金鑰，您可以控制下列屬性 AMS 動態加密和 AMS 授權傳遞服務的 hello:</span><span class="sxs-lookup"><span data-stu-id="d1c4d-149">Through configuration of a content key, you can control hello following attributes of both AMS dynamic encryption and AMS license delivery service:</span></span>

* <span data-ttu-id="d1c4d-150">hello 動態 DRM 加密所使用的內容金鑰。</span><span class="sxs-lookup"><span data-stu-id="d1c4d-150">hello content key used for dynamic DRM encryption.</span></span>
* <span data-ttu-id="d1c4d-151">由授權傳遞服務傳送 DRM 授權內容 toobe： 權限、 內容金鑰和限制。</span><span class="sxs-lookup"><span data-stu-id="d1c4d-151">DRM license content toobe delivered by license delivery services: rights, content key and restrictions.</span></span>
* <span data-ttu-id="d1c4d-152">**內容金鑰授權原則限制**的類型：開啟、IP 或權杖限制。</span><span class="sxs-lookup"><span data-stu-id="d1c4d-152">Type of **content key authorization policy restriction**: open, IP, or token restriction.</span></span>
* <span data-ttu-id="d1c4d-153">如果**語彙基元**類型**使用內容金鑰授權原則限制**，hello**內容金鑰授權原則限制**必須符合才能發出授權。</span><span class="sxs-lookup"><span data-stu-id="d1c4d-153">If **token** type of **content key authorization policy restriction is used**, hello **content key authorization policy restriction** must be met before a license is issued.</span></span>

### <a name="asset-delivery-policy"></a><span data-ttu-id="d1c4d-154">資產傳遞原則</span><span class="sxs-lookup"><span data-stu-id="d1c4d-154">Asset delivery policy</span></span>

<span data-ttu-id="d1c4d-155">透過設定資產遞送原則，您可以控制 hello 下列 AMS 動態封裝程式和動態加密的 AMS 串流端點所使用的屬性：</span><span class="sxs-lookup"><span data-stu-id="d1c4d-155">Through configuration of an asset delivery policy, you can control hello following attributes used by AMS dynamic packager and dynamic encryption of an AMS streaming endpoint:</span></span>

* <span data-ttu-id="d1c4d-156">串流處理通訊協定和 DRM 加密的組合，例如 CENC (PlayReady 和 Widevine) 下的 DASH、PlayReady 下的 Smooth Streaming、Widevine 或 PlayReady 下的 HLS。</span><span class="sxs-lookup"><span data-stu-id="d1c4d-156">Streaming protocol and DRM encryption combination, such as DASH under CENC (PlayReady and Widevine), smooth streaming under PlayReady, HLS under Widevine or PlayReady.</span></span>
* <span data-ttu-id="d1c4d-157">每個 hello hello 預設/內嵌授權傳遞 Url 涉及 DRMs。</span><span class="sxs-lookup"><span data-stu-id="d1c4d-157">hello default/embedded license delivery URLs for each of hello involved DRMs.</span></span>
* <span data-ttu-id="d1c4d-158">無論 DASH MPD 或 HLS 播放清單的授權取得 URL (LA_URL) 是否分別包含 Widevine 和 FairPlay 的索引鍵識別碼 (KID) 查詢字串。</span><span class="sxs-lookup"><span data-stu-id="d1c4d-158">Whether license acquisition URLs (LA_URLs) in DASH MPD or HLS playlist contain query string of key ID (KID) for Widevine and FairPlay, respectively.</span></span>

## <a name="scenarios-and-samples"></a><span data-ttu-id="d1c4d-159">案例與範例</span><span class="sxs-lookup"><span data-stu-id="d1c4d-159">Scenarios and samples</span></span>

<span data-ttu-id="d1c4d-160">根據 hello hello 前一節中的說明，下列五個混合式案例的 hello 使用個別**內容金鑰**-**資產傳遞原則**組態的組合 (hellohello 最後一個資料行中所述的範例遵循 hello 資料表）：</span><span class="sxs-lookup"><span data-stu-id="d1c4d-160">Based on hello explanations in hello previous section, hello following five hybrid scenarios use respective **Content key**-**Asset delivery policy** configuration combinations (hello samples mentioned in hello last column follow hello table):</span></span>

|<span data-ttu-id="d1c4d-161">**內容裝載與來源**</span><span class="sxs-lookup"><span data-stu-id="d1c4d-161">**Content hosting & origin**</span></span>|<span data-ttu-id="d1c4d-162">**DRM 加密**</span><span class="sxs-lookup"><span data-stu-id="d1c4d-162">**DRM encryption**</span></span>|<span data-ttu-id="d1c4d-163">**DRM 授權傳遞**</span><span class="sxs-lookup"><span data-stu-id="d1c4d-163">**DRM license delivery**</span></span>|<span data-ttu-id="d1c4d-164">**設定內容金鑰**</span><span class="sxs-lookup"><span data-stu-id="d1c4d-164">**Configure content key**</span></span>|<span data-ttu-id="d1c4d-165">**設定資產傳遞原則**</span><span class="sxs-lookup"><span data-stu-id="d1c4d-165">**Configure asset delivery policy**</span></span>|<span data-ttu-id="d1c4d-166">**範例**</span><span class="sxs-lookup"><span data-stu-id="d1c4d-166">**Sample**</span></span>|
|---|---|---|---|---|---|
|<span data-ttu-id="d1c4d-167">AMS</span><span class="sxs-lookup"><span data-stu-id="d1c4d-167">AMS</span></span>|<span data-ttu-id="d1c4d-168">AMS</span><span class="sxs-lookup"><span data-stu-id="d1c4d-168">AMS</span></span>|<span data-ttu-id="d1c4d-169">AMS</span><span class="sxs-lookup"><span data-stu-id="d1c4d-169">AMS</span></span>|<span data-ttu-id="d1c4d-170">是</span><span class="sxs-lookup"><span data-stu-id="d1c4d-170">Yes</span></span>|<span data-ttu-id="d1c4d-171">是</span><span class="sxs-lookup"><span data-stu-id="d1c4d-171">Yes</span></span>|<span data-ttu-id="d1c4d-172">範例 1</span><span class="sxs-lookup"><span data-stu-id="d1c4d-172">Sample 1</span></span>|
|<span data-ttu-id="d1c4d-173">AMS</span><span class="sxs-lookup"><span data-stu-id="d1c4d-173">AMS</span></span>|<span data-ttu-id="d1c4d-174">AMS</span><span class="sxs-lookup"><span data-stu-id="d1c4d-174">AMS</span></span>|<span data-ttu-id="d1c4d-175">協力廠商</span><span class="sxs-lookup"><span data-stu-id="d1c4d-175">Third-party</span></span>|<span data-ttu-id="d1c4d-176">是</span><span class="sxs-lookup"><span data-stu-id="d1c4d-176">Yes</span></span>|<span data-ttu-id="d1c4d-177">是</span><span class="sxs-lookup"><span data-stu-id="d1c4d-177">Yes</span></span>|<span data-ttu-id="d1c4d-178">範例 2</span><span class="sxs-lookup"><span data-stu-id="d1c4d-178">Sample 2</span></span>|
|<span data-ttu-id="d1c4d-179">AMS</span><span class="sxs-lookup"><span data-stu-id="d1c4d-179">AMS</span></span>|<span data-ttu-id="d1c4d-180">協力廠商</span><span class="sxs-lookup"><span data-stu-id="d1c4d-180">Third-party</span></span>|<span data-ttu-id="d1c4d-181">AMS</span><span class="sxs-lookup"><span data-stu-id="d1c4d-181">AMS</span></span>|<span data-ttu-id="d1c4d-182">是</span><span class="sxs-lookup"><span data-stu-id="d1c4d-182">Yes</span></span>|<span data-ttu-id="d1c4d-183">否</span><span class="sxs-lookup"><span data-stu-id="d1c4d-183">No</span></span>|<span data-ttu-id="d1c4d-184">範例 3</span><span class="sxs-lookup"><span data-stu-id="d1c4d-184">Sample 3</span></span>|
|<span data-ttu-id="d1c4d-185">AMS</span><span class="sxs-lookup"><span data-stu-id="d1c4d-185">AMS</span></span>|<span data-ttu-id="d1c4d-186">協力廠商</span><span class="sxs-lookup"><span data-stu-id="d1c4d-186">Third-party</span></span>|<span data-ttu-id="d1c4d-187">外部</span><span class="sxs-lookup"><span data-stu-id="d1c4d-187">Outside</span></span>|<span data-ttu-id="d1c4d-188">否</span><span class="sxs-lookup"><span data-stu-id="d1c4d-188">No</span></span>|<span data-ttu-id="d1c4d-189">否</span><span class="sxs-lookup"><span data-stu-id="d1c4d-189">No</span></span>|<span data-ttu-id="d1c4d-190">範例 4</span><span class="sxs-lookup"><span data-stu-id="d1c4d-190">Sample 4</span></span>|
|<span data-ttu-id="d1c4d-191">協力廠商</span><span class="sxs-lookup"><span data-stu-id="d1c4d-191">Third-party</span></span>|<span data-ttu-id="d1c4d-192">協力廠商</span><span class="sxs-lookup"><span data-stu-id="d1c4d-192">Third-party</span></span>|<span data-ttu-id="d1c4d-193">AMS</span><span class="sxs-lookup"><span data-stu-id="d1c4d-193">AMS</span></span>|<span data-ttu-id="d1c4d-194">是</span><span class="sxs-lookup"><span data-stu-id="d1c4d-194">Yes</span></span>|<span data-ttu-id="d1c4d-195">否</span><span class="sxs-lookup"><span data-stu-id="d1c4d-195">No</span></span>|    

<span data-ttu-id="d1c4d-196">在 hello 範例 PlayReady 保護適用於虛線和 smooth streaming。</span><span class="sxs-lookup"><span data-stu-id="d1c4d-196">In hello samples, PlayReady protection works for both DASH and smooth streaming.</span></span> <span data-ttu-id="d1c4d-197">下列 hello 視訊 Url 是 smooth streaming Url。</span><span class="sxs-lookup"><span data-stu-id="d1c4d-197">hello video URLs below are smooth streaming URLs.</span></span> <span data-ttu-id="d1c4d-198">tooget hello 對應 DASH Url，只要附加"(格式 = mpd-時間-csf) 」。</span><span class="sxs-lookup"><span data-stu-id="d1c4d-198">tooget hello corresponding DASH URLs, just append "(format=mpd-time-csf)".</span></span> <span data-ttu-id="d1c4d-199">您可以使用 hello [azure 媒體測試 player](http://aka.ms/amtest) tootest 瀏覽器中的。</span><span class="sxs-lookup"><span data-stu-id="d1c4d-199">You could use hello [azure media test player](http://aka.ms/amtest) tootest in a browser.</span></span> <span data-ttu-id="d1c4d-200">它可讓您 tooconfigure 的串流處理通訊協定 toouse，底下的技術。</span><span class="sxs-lookup"><span data-stu-id="d1c4d-200">It allows you tooconfigure which streaming protocol toouse, under which tech.</span></span> <span data-ttu-id="d1c4d-201">Windows 10 的 IE11 和 MS Edge 都透過 EME 支援 PlayReady。</span><span class="sxs-lookup"><span data-stu-id="d1c4d-201">IE11 and MS Edge on Windows 10 support PlayReady through EME.</span></span> <span data-ttu-id="d1c4d-202">如需詳細資訊，請參閱[hello 詳細測試工具](https://blogs.msdn.microsoft.com/playready4/2016/02/28/azure-media-test-tool/)。</span><span class="sxs-lookup"><span data-stu-id="d1c4d-202">For more information, see [details about hello test tool](https://blogs.msdn.microsoft.com/playready4/2016/02/28/azure-media-test-tool/).</span></span>

### <a name="sample-1"></a><span data-ttu-id="d1c4d-203">範例 1</span><span class="sxs-lookup"><span data-stu-id="d1c4d-203">Sample 1</span></span>

* <span data-ttu-id="d1c4d-204">來源 (基底) URL：https://willzhanmswest.streaming.mediaservices.windows.net/1efbd6bb-1e66-4e53-88c3-f7e5657a9bbd/RussianWaltz.ism/manifest</span><span class="sxs-lookup"><span data-stu-id="d1c4d-204">Source (base) URL: https://willzhanmswest.streaming.mediaservices.windows.net/1efbd6bb-1e66-4e53-88c3-f7e5657a9bbd/RussianWaltz.ism/manifest</span></span> 
* <span data-ttu-id="d1c4d-205">PlayReady LA_URL (DASH & Smooth)：https://willzhanmswest.keydelivery.mediaservices.windows.net/PlayReady/</span><span class="sxs-lookup"><span data-stu-id="d1c4d-205">PlayReady LA_URL (DASH & smooth): https://willzhanmswest.keydelivery.mediaservices.windows.net/PlayReady/</span></span> 
* <span data-ttu-id="d1c4d-206">Widevine LA_URL (DASH)：https://willzhanmswest.keydelivery.mediaservices.windows.net/Widevine/?kid=78de73ae-6d0f-470a-8f13-5c91f7c4</span><span class="sxs-lookup"><span data-stu-id="d1c4d-206">Widevine LA_URL (DASH): https://willzhanmswest.keydelivery.mediaservices.windows.net/Widevine/?kid=78de73ae-6d0f-470a-8f13-5c91f7c4</span></span> 
* <span data-ttu-id="d1c4d-207">FairPlay LA_URL (HLS)：https://willzhanmswest.keydelivery.mediaservices.windows.net/FairPlay/?kid=ba7e8fb0-ee22-4291-9654-6222ac611bd8</span><span class="sxs-lookup"><span data-stu-id="d1c4d-207">FairPlay LA_URL (HLS): https://willzhanmswest.keydelivery.mediaservices.windows.net/FairPlay/?kid=ba7e8fb0-ee22-4291-9654-6222ac611bd8</span></span> 

### <a name="sample-2"></a><span data-ttu-id="d1c4d-208">範例 2</span><span class="sxs-lookup"><span data-stu-id="d1c4d-208">Sample 2</span></span>

* <span data-ttu-id="d1c4d-209">來源 (基底) URL：http://willzhanmswest.streaming.mediaservices.windows.net/1a670626-4515-49ee-9e7f-cd50853e41d8/Microsoft_HoloLens_TransformYourWorld_816p23.ism/Manifest</span><span class="sxs-lookup"><span data-stu-id="d1c4d-209">Source (base) URL: http://willzhanmswest.streaming.mediaservices.windows.net/1a670626-4515-49ee-9e7f-cd50853e41d8/Microsoft_HoloLens_TransformYourWorld_816p23.ism/Manifest</span></span> 
* <span data-ttu-id="d1c4d-210">PlayReady LA_URL (DASH & Smooth)：http://willzhan12.cloudapp.net/PlayReady/RightsManager.asmx</span><span class="sxs-lookup"><span data-stu-id="d1c4d-210">PlayReady LA_URL (DASH & smooth): http://willzhan12.cloudapp.net/PlayReady/RightsManager.asmx</span></span> 

### <a name="sample-3"></a><span data-ttu-id="d1c4d-211">範例 3</span><span class="sxs-lookup"><span data-stu-id="d1c4d-211">Sample 3</span></span>

* <span data-ttu-id="d1c4d-212">來源 URL：https://willzhanmswest.streaming.mediaservices.windows.net/8d078cf8-d621-406c-84ca-88e6b9454acc/20150807-bridges-2500.ism/manifest</span><span class="sxs-lookup"><span data-stu-id="d1c4d-212">Source URL: https://willzhanmswest.streaming.mediaservices.windows.net/8d078cf8-d621-406c-84ca-88e6b9454acc/20150807-bridges-2500.ism/manifest</span></span> 
* <span data-ttu-id="d1c4d-213">PlayReady LA_URL (DASH & Smooth)：https://willzhanmswest.keydelivery.mediaservices.windows.net/PlayReady/</span><span class="sxs-lookup"><span data-stu-id="d1c4d-213">PlayReady LA_URL (DASH & smooth): https://willzhanmswest.keydelivery.mediaservices.windows.net/PlayReady/</span></span> 

### <a name="sample-4"></a><span data-ttu-id="d1c4d-214">範例 4</span><span class="sxs-lookup"><span data-stu-id="d1c4d-214">Sample 4</span></span>

* <span data-ttu-id="d1c4d-215">來源 URL：https://willzhanmswest.streaming.mediaservices.windows.net/7c085a59-ae9a-411e-842c-ef10f96c3f89/20150807-bridges-2500.ism/manifest</span><span class="sxs-lookup"><span data-stu-id="d1c4d-215">Source URL: https://willzhanmswest.streaming.mediaservices.windows.net/7c085a59-ae9a-411e-842c-ef10f96c3f89/20150807-bridges-2500.ism/manifest</span></span> 
* <span data-ttu-id="d1c4d-216">PlayReady LA_URL (DASH & Smooth)：https://willzhan12.cloudapp.net/playready/rightsmanager.asmx</span><span class="sxs-lookup"><span data-stu-id="d1c4d-216">PlayReady LA_URL (DASH & smooth): https://willzhan12.cloudapp.net/playready/rightsmanager.asmx</span></span> 

## <a name="summary"></a><span data-ttu-id="d1c4d-217">摘要</span><span class="sxs-lookup"><span data-stu-id="d1c4d-217">Summary</span></span>

<span data-ttu-id="d1c4d-218">總而言之，Azure 媒體服務 DRM 元件富有彈性，只要如本主題所述正確設定內容金鑰與資產傳遞原則，就可以在混合式案例中使用它們。</span><span class="sxs-lookup"><span data-stu-id="d1c4d-218">In summary, Azure Media Services DRM components are flexible, you can use them in a hybrid scenario by properly configuring content key and asset delivery policy, as described in this topic.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d1c4d-219">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d1c4d-219">Next steps</span></span>
<span data-ttu-id="d1c4d-220">檢視媒體服務學習路徑。</span><span class="sxs-lookup"><span data-stu-id="d1c4d-220">View Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="d1c4d-221">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="d1c4d-221">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

