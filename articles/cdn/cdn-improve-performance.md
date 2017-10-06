---
title: "壓縮檔案，在 Azure CDN aaaImprove 效能 |Microsoft 文件"
description: "了解 tooimprove 檔案壓縮 Azure CDN 中的檔案所傳輸的速度以及增加負載效能。"
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: af1cddff-78d8-476b-a9d0-8c2164e4de5d
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 9a1698b6c29233c2e2e6fb17cdd8e919ae8bfa1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="improve-performance-by-compressing-files-in-azure-cdn"></a><span data-ttu-id="166ff-103">在 Azure CDN 中壓縮檔案以改善效能</span><span class="sxs-lookup"><span data-stu-id="166ff-103">Improve performance by compressing files in Azure CDN</span></span>
<span data-ttu-id="166ff-104">壓縮是簡單且有效的方法 tooimprove 檔案傳輸速度以及增加網頁載入效能，藉由減少檔案大小之前從傳送 hello 伺服器。</span><span class="sxs-lookup"><span data-stu-id="166ff-104">Compression is a simple and effective method tooimprove file transfer speed and increase page load performance by reducing file size before it is sent from hello server.</span></span> <span data-ttu-id="166ff-105">它會降低頻寬成本，並提供回應速度更快的體驗給使用者。</span><span class="sxs-lookup"><span data-stu-id="166ff-105">It reduces bandwidth costs and provides a more responsive experience for your users.</span></span>

<span data-ttu-id="166ff-106">有兩種方式 tooenable 壓縮：</span><span class="sxs-lookup"><span data-stu-id="166ff-106">There are two ways tooenable compression:</span></span>

* <span data-ttu-id="166ff-107">在此情況下 hello CDN 通過 hello 壓縮的檔案和傳遞要求的壓縮的檔 tooclients，您可以在您的原始伺服器上啟用壓縮。</span><span class="sxs-lookup"><span data-stu-id="166ff-107">You can enable compression on your origin server, in which case hello CDN passes through hello compressed files and deliver compressed files tooclients that request them.</span></span>
* <span data-ttu-id="166ff-108">您可以啟用壓縮，直接在 CDN 邊緣伺服器案例的 hello CDN 壓縮 hello 檔案並提供服務給其 tooend 使用者，即使它們不會壓縮 hello 原始伺服器上。</span><span class="sxs-lookup"><span data-stu-id="166ff-108">You can enable compression directly on CDN edge servers, in which case hello CDN compresses hello files and serve them tooend users, even if they are not compressed by hello origin server.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="166ff-109">CDN 設定變更都會透過 hello 網路某些時間 toopropagate。</span><span class="sxs-lookup"><span data-stu-id="166ff-109">CDN configuration changes take some time toopropagate through hello network.</span></span>  <span data-ttu-id="166ff-110">若為 <b>來自 Akamai 的 Azure CDN</b> 設定檔，通常會在一分鐘之內完成傳播。</span><span class="sxs-lookup"><span data-stu-id="166ff-110">For <b>Azure CDN from Akamai</b> profiles, propagation usually completes in under one minute.</span></span>  <span data-ttu-id="166ff-111">若為 <b>來自 Verizon 的 Azure CDN</b> 設定檔，您通常會在 90 分鐘之內看到變更套用。</span><span class="sxs-lookup"><span data-stu-id="166ff-111">For <b>Azure CDN from Verizon</b> profiles, you will usually see your changes apply within 90 minutes.</span></span>  <span data-ttu-id="166ff-112">如果這是 hello 您為您的 CDN 端點設定壓縮的第一次，您應該考慮等候 1-2 小時 toobe 確定 hello 壓縮設定都已傳播 toohello 快顯的疑難排解</span><span class="sxs-lookup"><span data-stu-id="166ff-112">If this is hello first time you've set up compression for your CDN endpoint, you should consider waiting 1-2 hours toobe sure hello compression settings have propagated toohello POPs before troubleshooting</span></span>
> 
> 

## <a name="enabling-compression"></a><span data-ttu-id="166ff-113">啟用壓縮</span><span class="sxs-lookup"><span data-stu-id="166ff-113">Enabling compression</span></span>
> [!NOTE]
> <span data-ttu-id="166ff-114">hello Standard 和 Premium CDN 層提供 hello 相同的壓縮功能，但是 hello 使用者介面有所不同。</span><span class="sxs-lookup"><span data-stu-id="166ff-114">hello Standard and Premium CDN tiers provide hello same compression functionality, but hello user interface differs.</span></span>  <span data-ttu-id="166ff-115">如需 hello Standard 和 Premium CDN 的各層之間的差異的詳細資訊，請參閱[Azure CDN 概觀](cdn-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="166ff-115">For more information about hello differences between Standard and Premium CDN tiers, see [Azure CDN Overview](cdn-overview.md).</span></span>
> 
> 

### <a name="standard-tier"></a><span data-ttu-id="166ff-116">標準層</span><span class="sxs-lookup"><span data-stu-id="166ff-116">Standard tier</span></span>
> [!NOTE]
> <span data-ttu-id="166ff-117">本章節適用於太**Azure CDN 標準從 Verizon**和**Azure 標準 Akamai CDN**設定檔。</span><span class="sxs-lookup"><span data-stu-id="166ff-117">This section applies too**Azure CDN Standard from Verizon** and **Azure CDN Standard from Akamai** profiles.</span></span>
> 
> 

1. <span data-ttu-id="166ff-118">從 hello CDN 設定檔 頁面上，按一下您想 toomanage hello CDN 端點。</span><span class="sxs-lookup"><span data-stu-id="166ff-118">From hello CDN profile page, click hello CDN endpoint you wish toomanage.</span></span>
   
    ![[CDN 設定檔] 頁面端點](./media/cdn-file-compression/cdn-endpoints.png)
   
    <span data-ttu-id="166ff-120">hello CDN 端點頁面隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="166ff-120">hello CDN endpoint page opens.</span></span>
2. <span data-ttu-id="166ff-121">按一下 hello**設定** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="166ff-121">Click hello **Configure** button.</span></span>
   
    ![[CDN 設定檔] 頁面的 [管理] 按鈕](./media/cdn-file-compression/cdn-config-btn.png)
   
    <span data-ttu-id="166ff-123">hello CDN 組態 頁面隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="166ff-123">hello CDN Configuration page opens.</span></span>
3. <span data-ttu-id="166ff-124">開啟 [ **壓縮**]。</span><span class="sxs-lookup"><span data-stu-id="166ff-124">Turn on **Compression**.</span></span>
   
    ![CDN 壓縮的選項](./media/cdn-file-compression/cdn-compress-standard.png)
4. <span data-ttu-id="166ff-126">使用 hello 預設類型，或修改 hello 清單移除或新增檔案類型。</span><span class="sxs-lookup"><span data-stu-id="166ff-126">Use hello default types, or modify hello list by removing or adding file types.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="166ff-127">While 可行的建議您不要 tooapply 壓縮 toocompressed 格式，例如 ZIP、 MP3、 MP4、 JPG 等等。</span><span class="sxs-lookup"><span data-stu-id="166ff-127">While possible, it is not recommended tooapply compression toocompressed formats, such as ZIP, MP3, MP4, JPG, etc.</span></span>
   > 
   > 
5. <span data-ttu-id="166ff-128">在您的變更後，按一下 [hello**儲存**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="166ff-128">After making your changes, click hello **Save** button.</span></span>

### <a name="premium-tier"></a><span data-ttu-id="166ff-129">高階層</span><span class="sxs-lookup"><span data-stu-id="166ff-129">Premium tier</span></span>
> [!NOTE]
> <span data-ttu-id="166ff-130">本章節適用於太**Verizon 從 Azure CDN Premium**設定檔。</span><span class="sxs-lookup"><span data-stu-id="166ff-130">This section applies too**Azure CDN Premium from Verizon** profiles.</span></span>
> 
> 

1. <span data-ttu-id="166ff-131">從 hello CDN 設定檔 頁面上，按一下 hello**管理** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="166ff-131">From hello CDN profile page, click hello **Manage** button.</span></span>
   
    ![[CDN 設定檔] 頁面的 [管理] 按鈕](./media/cdn-file-compression/cdn-manage-btn.png)
   
    <span data-ttu-id="166ff-133">hello CDN 管理入口網站隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="166ff-133">hello CDN management portal opens.</span></span>
2. <span data-ttu-id="166ff-134">暫留在 hello **HTTP 大型** 索引標籤，然後暫留在 hello**快取設定**彈出式視窗。</span><span class="sxs-lookup"><span data-stu-id="166ff-134">Hover over hello **HTTP Large** tab, then hover over hello **Cache Settings** flyout.</span></span>  <span data-ttu-id="166ff-135">按一下 [ **壓縮**]。</span><span class="sxs-lookup"><span data-stu-id="166ff-135">Click on **Compression**.</span></span>

    ![檔案壓縮選項](./media/cdn-file-compression/cdn-compress-select.png)
   
    <span data-ttu-id="166ff-137">隨即顯示 [壓縮] 的選項。</span><span class="sxs-lookup"><span data-stu-id="166ff-137">Compression options are displayed.</span></span>
   
    ![檔案壓縮](./media/cdn-file-compression/cdn-compress-files.png)
3. <span data-ttu-id="166ff-139">啟用壓縮，依序按一下 hello**啟用壓縮**選項按鈕。</span><span class="sxs-lookup"><span data-stu-id="166ff-139">Enable compression by clicking hello **Compression Enabled** radio button.</span></span>  <span data-ttu-id="166ff-140">輸入 hello MIME 型別想成以逗號分隔清單 （無空格） 在 hello toocompress**檔案類型**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="166ff-140">Enter hello MIME types you wish toocompress as a comma-delimited list (no spaces) in hello **File Types** textbox.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="166ff-141">While 可行的建議您不要 tooapply 壓縮 toocompressed 格式，例如 ZIP、 MP3、 MP4、 JPG 等等。</span><span class="sxs-lookup"><span data-stu-id="166ff-141">While possible, it is not recommended tooapply compression toocompressed formats, such as ZIP, MP3, MP4, JPG, etc.</span></span> 
   > 
   > 
4. <span data-ttu-id="166ff-142">在您的變更後，按一下 [hello**更新**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="166ff-142">After making your changes, click hello **Update** button.</span></span>

## <a name="compression-rules"></a><span data-ttu-id="166ff-143">壓縮規則</span><span class="sxs-lookup"><span data-stu-id="166ff-143">Compression rules</span></span>
<span data-ttu-id="166ff-144">這些資料表描述每個案例的 Azure CDN 壓縮行為。</span><span class="sxs-lookup"><span data-stu-id="166ff-144">These tables describe Azure CDN compression behavior for every scenario.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="166ff-145">若為 **來自 Verizon 的 Azure CDN** (標準和進)，只會壓縮合格的檔案。</span><span class="sxs-lookup"><span data-stu-id="166ff-145">For **Azure CDN from Verizon** (Standard and Premium), only eligible files are compressed.</span></span>  <span data-ttu-id="166ff-146">toobe 能夠壓縮，檔案必須：</span><span class="sxs-lookup"><span data-stu-id="166ff-146">toobe eligible for compression, a file must:</span></span>
> 
> * <span data-ttu-id="166ff-147">超過 128 個位元組。</span><span class="sxs-lookup"><span data-stu-id="166ff-147">Be larger than 128 bytes.</span></span>
> * <span data-ttu-id="166ff-148">小於 1 MB。</span><span class="sxs-lookup"><span data-stu-id="166ff-148">Be smaller than 1 MB.</span></span>
> 
> <span data-ttu-id="166ff-149">若為 **來自 Akamai 的 Azure CDN**，所有檔案都符合壓縮資格。</span><span class="sxs-lookup"><span data-stu-id="166ff-149">For **Azure CDN from Akamai**, all files are eligible for compression.</span></span>
> 
> <span data-ttu-id="166ff-150">對於所有的 Azure CDN 產品，檔案必須為已 [設定壓縮](#enabling-compression)的 MIME 類型。</span><span class="sxs-lookup"><span data-stu-id="166ff-150">For all Azure CDN products, a file must be a MIME type that has been [configured for compression](#enabling-compression).</span></span>
> 
> <span data-ttu-id="166ff-151">**來自 Verizon 的 Azure CDN** 設定檔 (標準和進階) 支援 **gzip** (GNU zip)、**deflate**、**bzip2** 或 **br** (Brotli) 編碼。</span><span class="sxs-lookup"><span data-stu-id="166ff-151">**Azure CDN from Verizon** profiles (Standard and Premium) support **gzip** (GNU zip), **deflate**, **bzip2**, or  **br** (Brotli) encoding.</span></span> <span data-ttu-id="166ff-152">Brotli 編碼方式，是只在 hello 邊緣完成 hello 壓縮。</span><span class="sxs-lookup"><span data-stu-id="166ff-152">For Brotli encoding, hello compression is done only at hello edge.</span></span> <span data-ttu-id="166ff-153">hello 用戶端瀏覽器必須傳送嗨要求 Brotli 編碼方式和 hello 壓縮的資產必須已壓縮 hello 原點端上第一次。</span><span class="sxs-lookup"><span data-stu-id="166ff-153">hello client/browser must send hello request for Brotli encoding and hello compressed asset must have been compressed on hello origin side first.</span></span> 
>
><span data-ttu-id="166ff-154">**來自 Akamai 的 Azure CDN** 設定檔只支援 **gzip** 編碼。</span><span class="sxs-lookup"><span data-stu-id="166ff-154">**Azure CDN from Akamai** profiles support only **gzip** encoding.</span></span>
> 
> <span data-ttu-id="166ff-155">**Azure CDN 從 Akamai**端點永遠要求**gzip**編碼 hello 原點，不論 hello 用戶端要求中的檔案。</span><span class="sxs-lookup"><span data-stu-id="166ff-155">**Azure CDN from Akamai** endpoints always request **gzip** encoded files from hello origin, regardless of hello client request.</span></span> 

### <a name="compression-disabled-or-file-is-ineligible-for-compression"></a><span data-ttu-id="166ff-156">已停用壓縮或檔案不適合進行壓縮</span><span class="sxs-lookup"><span data-stu-id="166ff-156">Compression disabled or file is ineligible for compression</span></span>
| <span data-ttu-id="166ff-157">用戶端要求的格式 (透過 Accept-encoding 標頭)</span><span class="sxs-lookup"><span data-stu-id="166ff-157">Client requested format (via Accept-Encoding header)</span></span> | <span data-ttu-id="166ff-158">快取的檔案格式</span><span class="sxs-lookup"><span data-stu-id="166ff-158">Cached file format</span></span> | <span data-ttu-id="166ff-159">CDN 回應 toohello 用戶端</span><span class="sxs-lookup"><span data-stu-id="166ff-159">CDN response toohello client</span></span> | <span data-ttu-id="166ff-160">注意事項</span><span class="sxs-lookup"><span data-stu-id="166ff-160">Notes</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="166ff-161">已壓縮</span><span class="sxs-lookup"><span data-stu-id="166ff-161">Compressed</span></span> |<span data-ttu-id="166ff-162">已壓縮</span><span class="sxs-lookup"><span data-stu-id="166ff-162">Compressed</span></span> |<span data-ttu-id="166ff-163">已壓縮</span><span class="sxs-lookup"><span data-stu-id="166ff-163">Compressed</span></span> | |
| <span data-ttu-id="166ff-164">已壓縮</span><span class="sxs-lookup"><span data-stu-id="166ff-164">Compressed</span></span> |<span data-ttu-id="166ff-165">未壓縮</span><span class="sxs-lookup"><span data-stu-id="166ff-165">Uncompressed</span></span> |<span data-ttu-id="166ff-166">未壓縮</span><span class="sxs-lookup"><span data-stu-id="166ff-166">Uncompressed</span></span> | |
| <span data-ttu-id="166ff-167">已壓縮</span><span class="sxs-lookup"><span data-stu-id="166ff-167">Compressed</span></span> |<span data-ttu-id="166ff-168">不快取</span><span class="sxs-lookup"><span data-stu-id="166ff-168">Not cached</span></span> |<span data-ttu-id="166ff-169">已壓縮或未壓縮</span><span class="sxs-lookup"><span data-stu-id="166ff-169">Compressed or Uncompressed</span></span> |<span data-ttu-id="166ff-170">取決於原始回應</span><span class="sxs-lookup"><span data-stu-id="166ff-170">Depends on origin response</span></span> |
| <span data-ttu-id="166ff-171">未壓縮</span><span class="sxs-lookup"><span data-stu-id="166ff-171">Uncompressed</span></span> |<span data-ttu-id="166ff-172">已壓縮</span><span class="sxs-lookup"><span data-stu-id="166ff-172">Compressed</span></span> |<span data-ttu-id="166ff-173">未壓縮</span><span class="sxs-lookup"><span data-stu-id="166ff-173">Uncompressed</span></span> | |
| <span data-ttu-id="166ff-174">未壓縮</span><span class="sxs-lookup"><span data-stu-id="166ff-174">Uncompressed</span></span> |<span data-ttu-id="166ff-175">未壓縮</span><span class="sxs-lookup"><span data-stu-id="166ff-175">Uncompressed</span></span> |<span data-ttu-id="166ff-176">未壓縮</span><span class="sxs-lookup"><span data-stu-id="166ff-176">Uncompressed</span></span> | |
| <span data-ttu-id="166ff-177">未壓縮</span><span class="sxs-lookup"><span data-stu-id="166ff-177">Uncompressed</span></span> |<span data-ttu-id="166ff-178">不快取</span><span class="sxs-lookup"><span data-stu-id="166ff-178">Not cached</span></span> |<span data-ttu-id="166ff-179">未壓縮</span><span class="sxs-lookup"><span data-stu-id="166ff-179">Uncompressed</span></span> | |

### <a name="compression-enabled-and-file-is-eligible-for-compression"></a><span data-ttu-id="166ff-180">啟用壓縮和檔案適合進行壓縮</span><span class="sxs-lookup"><span data-stu-id="166ff-180">Compression enabled and file is eligible for compression</span></span>
| <span data-ttu-id="166ff-181">用戶端要求的格式 (透過 Accept-encoding 標頭)</span><span class="sxs-lookup"><span data-stu-id="166ff-181">Client requested format (via Accept-Encoding header)</span></span> | <span data-ttu-id="166ff-182">快取的檔案格式</span><span class="sxs-lookup"><span data-stu-id="166ff-182">Cached file format</span></span> | <span data-ttu-id="166ff-183">CDN 回應 toohello 用戶端</span><span class="sxs-lookup"><span data-stu-id="166ff-183">CDN response toohello client</span></span> | <span data-ttu-id="166ff-184">注意事項</span><span class="sxs-lookup"><span data-stu-id="166ff-184">Notes</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="166ff-185">已壓縮</span><span class="sxs-lookup"><span data-stu-id="166ff-185">Compressed</span></span> |<span data-ttu-id="166ff-186">已壓縮</span><span class="sxs-lookup"><span data-stu-id="166ff-186">Compressed</span></span> |<span data-ttu-id="166ff-187">已壓縮</span><span class="sxs-lookup"><span data-stu-id="166ff-187">Compressed</span></span> |<span data-ttu-id="166ff-188">支援格式之間的 CDN 轉碼</span><span class="sxs-lookup"><span data-stu-id="166ff-188">CDN transcodes between supported formats</span></span> |
| <span data-ttu-id="166ff-189">已壓縮</span><span class="sxs-lookup"><span data-stu-id="166ff-189">Compressed</span></span> |<span data-ttu-id="166ff-190">未壓縮</span><span class="sxs-lookup"><span data-stu-id="166ff-190">Uncompressed</span></span> |<span data-ttu-id="166ff-191">已壓縮</span><span class="sxs-lookup"><span data-stu-id="166ff-191">Compressed</span></span> |<span data-ttu-id="166ff-192">CDN 執行壓縮</span><span class="sxs-lookup"><span data-stu-id="166ff-192">CDN performs compression</span></span> |
| <span data-ttu-id="166ff-193">已壓縮</span><span class="sxs-lookup"><span data-stu-id="166ff-193">Compressed</span></span> |<span data-ttu-id="166ff-194">不快取</span><span class="sxs-lookup"><span data-stu-id="166ff-194">Not cached</span></span> |<span data-ttu-id="166ff-195">已壓縮</span><span class="sxs-lookup"><span data-stu-id="166ff-195">Compressed</span></span> |<span data-ttu-id="166ff-196">如果來源傳回未壓縮，則 CDN 會執行壓縮。</span><span class="sxs-lookup"><span data-stu-id="166ff-196">CDN performs compression if origin returns uncompressed.</span></span>  <span data-ttu-id="166ff-197">**Azure CDN 從 Verizon**傳遞 hello 上 hello 第一個要求，然後壓縮未壓縮的檔案和快取 hello 的後續要求的檔案。</span><span class="sxs-lookup"><span data-stu-id="166ff-197">**Azure CDN from Verizon** passes hello uncompressed file on hello first request and then compresses and caches hello file for subsequent requests.</span></span>  <span data-ttu-id="166ff-198">具有 `Cache-Control: no-cache` 標頭的檔案永遠不會經過壓縮。</span><span class="sxs-lookup"><span data-stu-id="166ff-198">Files with `Cache-Control: no-cache` header will never be compressed.</span></span> |
| <span data-ttu-id="166ff-199">未壓縮</span><span class="sxs-lookup"><span data-stu-id="166ff-199">Uncompressed</span></span> |<span data-ttu-id="166ff-200">已壓縮</span><span class="sxs-lookup"><span data-stu-id="166ff-200">Compressed</span></span> |<span data-ttu-id="166ff-201">未壓縮</span><span class="sxs-lookup"><span data-stu-id="166ff-201">Uncompressed</span></span> |<span data-ttu-id="166ff-202">CDN 執行解壓縮</span><span class="sxs-lookup"><span data-stu-id="166ff-202">CDN performs decompression</span></span> |
| <span data-ttu-id="166ff-203">未壓縮</span><span class="sxs-lookup"><span data-stu-id="166ff-203">Uncompressed</span></span> |<span data-ttu-id="166ff-204">未壓縮</span><span class="sxs-lookup"><span data-stu-id="166ff-204">Uncompressed</span></span> |<span data-ttu-id="166ff-205">未壓縮</span><span class="sxs-lookup"><span data-stu-id="166ff-205">Uncompressed</span></span> | |
| <span data-ttu-id="166ff-206">未壓縮</span><span class="sxs-lookup"><span data-stu-id="166ff-206">Uncompressed</span></span> |<span data-ttu-id="166ff-207">不快取</span><span class="sxs-lookup"><span data-stu-id="166ff-207">Not cached</span></span> |<span data-ttu-id="166ff-208">未壓縮</span><span class="sxs-lookup"><span data-stu-id="166ff-208">Uncompressed</span></span> | |

## <a name="media-services-cdn-compression"></a><span data-ttu-id="166ff-209">媒體服務 CDN 壓縮</span><span class="sxs-lookup"><span data-stu-id="166ff-209">Media Services CDN Compression</span></span>
<span data-ttu-id="166ff-210">依預設，下列內容類型的 hello Media Services CDN 啟用的串流端點，啟用壓縮： 應用程式/vnd.ms-sstr + xml、 application/dash+xml,application/vnd.apple.mpegurl、 應用程式/f4m + xml。</span><span class="sxs-lookup"><span data-stu-id="166ff-210">For Media Services CDN enabled streaming endpoints, compression is enabled by default for hello following content types: application/vnd.ms-sstr+xml, application/dash+xml,application/vnd.apple.mpegurl, application/f4m+xml.</span></span> <span data-ttu-id="166ff-211">您無法啟用/停用壓縮 hello 提及使用 hello Azure 入口網站的類型。</span><span class="sxs-lookup"><span data-stu-id="166ff-211">You cannot enable/disable compression for hello mentioned types using hello Azure portal.</span></span>  

## <a name="see-also"></a><span data-ttu-id="166ff-212">另請參閱</span><span class="sxs-lookup"><span data-stu-id="166ff-212">See also</span></span>
* [<span data-ttu-id="166ff-213">CDN 檔案壓縮疑難排解</span><span class="sxs-lookup"><span data-stu-id="166ff-213">Troubleshooting CDN file compression</span></span>](cdn-troubleshoot-compression.md)    

