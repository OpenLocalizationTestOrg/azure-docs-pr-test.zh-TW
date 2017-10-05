---
title: "在 Azure CDN 中壓縮檔案以改善效能 | Microsoft Docs"
description: "了解如何藉由在 Azure CDN 中壓縮檔案來改善檔案傳輸速度並增加頁面載入效能。"
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
ms.openlocfilehash: 7546650e6096a880f4fb4d0c94dd4ecc00b70160
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="improve-performance-by-compressing-files-in-azure-cdn"></a><span data-ttu-id="54a99-103">在 Azure CDN 中壓縮檔案以改善效能</span><span class="sxs-lookup"><span data-stu-id="54a99-103">Improve performance by compressing files in Azure CDN</span></span>
<span data-ttu-id="54a99-104">壓縮是簡單且有效的方法，可提升檔案傳輸速度，並且在檔案從伺服器傳送出去之前先減少其大小，以增加頁面載入效能。</span><span class="sxs-lookup"><span data-stu-id="54a99-104">Compression is a simple and effective method to improve file transfer speed and increase page load performance by reducing file size before it is sent from the server.</span></span> <span data-ttu-id="54a99-105">它會降低頻寬成本，並提供回應速度更快的體驗給使用者。</span><span class="sxs-lookup"><span data-stu-id="54a99-105">It reduces bandwidth costs and provides a more responsive experience for your users.</span></span>

<span data-ttu-id="54a99-106">有兩種方式可啟用壓縮︰</span><span class="sxs-lookup"><span data-stu-id="54a99-106">There are two ways to enable compression:</span></span>

* <span data-ttu-id="54a99-107">您可以在原始伺服器上啟用壓縮，此時 CDN 會透過壓縮的檔案傳遞，並將壓縮的檔案傳送到提出要求的用戶端。</span><span class="sxs-lookup"><span data-stu-id="54a99-107">You can enable compression on your origin server, in which case the CDN passes through the compressed files and deliver compressed files to clients that request them.</span></span>
* <span data-ttu-id="54a99-108">您可以直接在 CDN Edge Server 上啟用壓縮，此時 CDN 會壓縮檔案並將其提供給終端使用者，即使原始伺服器未壓縮這些檔案也是如此。</span><span class="sxs-lookup"><span data-stu-id="54a99-108">You can enable compression directly on CDN edge servers, in which case the CDN compresses the files and serve them to end users, even if they are not compressed by the origin server.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="54a99-109">CDN 組態變更會需要一些時間才能傳播至整個網路。</span><span class="sxs-lookup"><span data-stu-id="54a99-109">CDN configuration changes take some time to propagate through the network.</span></span>  <span data-ttu-id="54a99-110">若為 <b>來自 Akamai 的 Azure CDN</b> 設定檔，通常會在一分鐘之內完成傳播。</span><span class="sxs-lookup"><span data-stu-id="54a99-110">For <b>Azure CDN from Akamai</b> profiles, propagation usually completes in under one minute.</span></span>  <span data-ttu-id="54a99-111">若為 <b>來自 Verizon 的 Azure CDN</b> 設定檔，您通常會在 90 分鐘之內看到變更套用。</span><span class="sxs-lookup"><span data-stu-id="54a99-111">For <b>Azure CDN from Verizon</b> profiles, you will usually see your changes apply within 90 minutes.</span></span>  <span data-ttu-id="54a99-112">如果這是您第一次設定 CDN 端點壓縮，您應該考慮先等候 1-2 小時，確定壓縮設定已傳播至 POP 再進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="54a99-112">If this is the first time you've set up compression for your CDN endpoint, you should consider waiting 1-2 hours to be sure the compression settings have propagated to the POPs before troubleshooting</span></span>
> 
> 

## <a name="enabling-compression"></a><span data-ttu-id="54a99-113">啟用壓縮</span><span class="sxs-lookup"><span data-stu-id="54a99-113">Enabling compression</span></span>
> [!NOTE]
> <span data-ttu-id="54a99-114">標準和高階 CDN 層提供相同的壓縮功能，但兩者的使用者介面不同。</span><span class="sxs-lookup"><span data-stu-id="54a99-114">The Standard and Premium CDN tiers provide the same compression functionality, but the user interface differs.</span></span>  <span data-ttu-id="54a99-115">如需有關標準和高階 CDN 層之間的差異的詳細資訊，請參閱 [Azure CDN 概觀](cdn-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="54a99-115">For more information about the differences between Standard and Premium CDN tiers, see [Azure CDN Overview](cdn-overview.md).</span></span>
> 
> 

### <a name="standard-tier"></a><span data-ttu-id="54a99-116">標準層</span><span class="sxs-lookup"><span data-stu-id="54a99-116">Standard tier</span></span>
> [!NOTE]
> <span data-ttu-id="54a99-117">本節適用於**來自 Verizon 的 Azure CDN 標準**和**來自 Akamai 的 Azure CDN 標準**設定檔。</span><span class="sxs-lookup"><span data-stu-id="54a99-117">This section applies to **Azure CDN Standard from Verizon** and **Azure CDN Standard from Akamai** profiles.</span></span>
> 
> 

1. <span data-ttu-id="54a99-118">在 [CDN 設定檔] 頁面中，按一下您要管理的 CDN 端點。</span><span class="sxs-lookup"><span data-stu-id="54a99-118">From the CDN profile page, click the CDN endpoint you wish to manage.</span></span>
   
    ![[CDN 設定檔] 頁面端點](./media/cdn-file-compression/cdn-endpoints.png)
   
    <span data-ttu-id="54a99-120">隨即開啟 [CDN 端點] 頁面。</span><span class="sxs-lookup"><span data-stu-id="54a99-120">The CDN endpoint page opens.</span></span>
2. <span data-ttu-id="54a99-121">按一下 [設定]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="54a99-121">Click the **Configure** button.</span></span>
   
    ![[CDN 設定檔] 頁面的 [管理] 按鈕](./media/cdn-file-compression/cdn-config-btn.png)
   
    <span data-ttu-id="54a99-123">隨即開啟 [CDN 組態] 頁面。</span><span class="sxs-lookup"><span data-stu-id="54a99-123">The CDN Configuration page opens.</span></span>
3. <span data-ttu-id="54a99-124">開啟 [ **壓縮**]。</span><span class="sxs-lookup"><span data-stu-id="54a99-124">Turn on **Compression**.</span></span>
   
    ![CDN 壓縮的選項](./media/cdn-file-compression/cdn-compress-standard.png)
4. <span data-ttu-id="54a99-126">請使用預設的類型，或者移除或新增檔案類型以修改清單。</span><span class="sxs-lookup"><span data-stu-id="54a99-126">Use the default types, or modify the list by removing or adding file types.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="54a99-127">如果可能，不建議對 ZIP、MP3、MP4、JPG 等壓縮格式套用壓縮。</span><span class="sxs-lookup"><span data-stu-id="54a99-127">While possible, it is not recommended to apply compression to compressed formats, such as ZIP, MP3, MP4, JPG, etc.</span></span>
   > 
   > 
5. <span data-ttu-id="54a99-128">完成變更之後，按一下 [ **儲存** ] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="54a99-128">After making your changes, click the **Save** button.</span></span>

### <a name="premium-tier"></a><span data-ttu-id="54a99-129">高階層</span><span class="sxs-lookup"><span data-stu-id="54a99-129">Premium tier</span></span>
> [!NOTE]
> <span data-ttu-id="54a99-130">本節適用於 **來自 Verizon 的 Azure CDN 進階** 設定檔。</span><span class="sxs-lookup"><span data-stu-id="54a99-130">This section applies to **Azure CDN Premium from Verizon** profiles.</span></span>
> 
> 

1. <span data-ttu-id="54a99-131">在 [CDN 設定檔] 頁面中，按一下 [管理] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="54a99-131">From the CDN profile page, click the **Manage** button.</span></span>
   
    ![[CDN 設定檔] 頁面的 [管理] 按鈕](./media/cdn-file-compression/cdn-manage-btn.png)
   
    <span data-ttu-id="54a99-133">隨即開啟 CDN 管理入口網站。</span><span class="sxs-lookup"><span data-stu-id="54a99-133">The CDN management portal opens.</span></span>
2. <span data-ttu-id="54a99-134">將滑鼠移至 [HTTP 大型] 索引標籤上，然後將滑鼠移至 [快取設定] 飛出視窗上。</span><span class="sxs-lookup"><span data-stu-id="54a99-134">Hover over the **HTTP Large** tab, then hover over the **Cache Settings** flyout.</span></span>  <span data-ttu-id="54a99-135">按一下 [ **壓縮**]。</span><span class="sxs-lookup"><span data-stu-id="54a99-135">Click on **Compression**.</span></span>

    ![檔案壓縮選項](./media/cdn-file-compression/cdn-compress-select.png)
   
    <span data-ttu-id="54a99-137">隨即顯示 [壓縮] 的選項。</span><span class="sxs-lookup"><span data-stu-id="54a99-137">Compression options are displayed.</span></span>
   
    ![檔案壓縮](./media/cdn-file-compression/cdn-compress-files.png)
3. <span data-ttu-id="54a99-139">按一下 [啟用壓縮]  選項按鈕以啟用壓縮。</span><span class="sxs-lookup"><span data-stu-id="54a99-139">Enable compression by clicking the **Compression Enabled** radio button.</span></span>  <span data-ttu-id="54a99-140">在 [檔案類型]  文字方塊中，輸入您想要壓縮成逗號分隔清單 (無空格) 的 MIME 類型。</span><span class="sxs-lookup"><span data-stu-id="54a99-140">Enter the MIME types you wish to compress as a comma-delimited list (no spaces) in the **File Types** textbox.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="54a99-141">如果可能，不建議對 ZIP、MP3、MP4、JPG 等壓縮格式套用壓縮。</span><span class="sxs-lookup"><span data-stu-id="54a99-141">While possible, it is not recommended to apply compression to compressed formats, such as ZIP, MP3, MP4, JPG, etc.</span></span> 
   > 
   > 
4. <span data-ttu-id="54a99-142">完成變更之後，按一下 [更新]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="54a99-142">After making your changes, click the **Update** button.</span></span>

## <a name="compression-rules"></a><span data-ttu-id="54a99-143">壓縮規則</span><span class="sxs-lookup"><span data-stu-id="54a99-143">Compression rules</span></span>
<span data-ttu-id="54a99-144">這些資料表描述每個案例的 Azure CDN 壓縮行為。</span><span class="sxs-lookup"><span data-stu-id="54a99-144">These tables describe Azure CDN compression behavior for every scenario.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="54a99-145">若為 **來自 Verizon 的 Azure CDN** (標準和進)，只會壓縮合格的檔案。</span><span class="sxs-lookup"><span data-stu-id="54a99-145">For **Azure CDN from Verizon** (Standard and Premium), only eligible files are compressed.</span></span>  <span data-ttu-id="54a99-146">若要符合壓縮，檔案必須︰</span><span class="sxs-lookup"><span data-stu-id="54a99-146">To be eligible for compression, a file must:</span></span>
> 
> * <span data-ttu-id="54a99-147">超過 128 個位元組。</span><span class="sxs-lookup"><span data-stu-id="54a99-147">Be larger than 128 bytes.</span></span>
> * <span data-ttu-id="54a99-148">小於 1 MB。</span><span class="sxs-lookup"><span data-stu-id="54a99-148">Be smaller than 1 MB.</span></span>
> 
> <span data-ttu-id="54a99-149">若為 **來自 Akamai 的 Azure CDN**，所有檔案都符合壓縮資格。</span><span class="sxs-lookup"><span data-stu-id="54a99-149">For **Azure CDN from Akamai**, all files are eligible for compression.</span></span>
> 
> <span data-ttu-id="54a99-150">對於所有的 Azure CDN 產品，檔案必須為已 [設定壓縮](#enabling-compression)的 MIME 類型。</span><span class="sxs-lookup"><span data-stu-id="54a99-150">For all Azure CDN products, a file must be a MIME type that has been [configured for compression](#enabling-compression).</span></span>
> 
> <span data-ttu-id="54a99-151">**來自 Verizon 的 Azure CDN** 設定檔 (標準和進階) 支援 **gzip** (GNU zip)、**deflate**、**bzip2** 或 **br** (Brotli) 編碼。</span><span class="sxs-lookup"><span data-stu-id="54a99-151">**Azure CDN from Verizon** profiles (Standard and Premium) support **gzip** (GNU zip), **deflate**, **bzip2**, or  **br** (Brotli) encoding.</span></span> <span data-ttu-id="54a99-152">對於 Brotli 編碼，壓縮只能在邊緣完成。</span><span class="sxs-lookup"><span data-stu-id="54a99-152">For Brotli encoding, the compression is done only at the edge.</span></span> <span data-ttu-id="54a99-153">用戶端/瀏覽器必須傳送 Brotli 編碼要求，而且壓縮的資產必須已事先在來源端經過壓縮。</span><span class="sxs-lookup"><span data-stu-id="54a99-153">The client/browser must send the request for Brotli encoding and the compressed asset must have been compressed on the origin side first.</span></span> 
>
><span data-ttu-id="54a99-154">**來自 Akamai 的 Azure CDN** 設定檔只支援 **gzip** 編碼。</span><span class="sxs-lookup"><span data-stu-id="54a99-154">**Azure CDN from Akamai** profiles support only **gzip** encoding.</span></span>
> 
> <span data-ttu-id="54a99-155">**來自 Akamai 的 Azure CDN** 端點一律要求來自原點的 **gzip** 編碼，不論用戶端是否提出要求。</span><span class="sxs-lookup"><span data-stu-id="54a99-155">**Azure CDN from Akamai** endpoints always request **gzip** encoded files from the origin, regardless of the client request.</span></span> 

### <a name="compression-disabled-or-file-is-ineligible-for-compression"></a><span data-ttu-id="54a99-156">已停用壓縮或檔案不適合進行壓縮</span><span class="sxs-lookup"><span data-stu-id="54a99-156">Compression disabled or file is ineligible for compression</span></span>
| <span data-ttu-id="54a99-157">用戶端要求的格式 (透過 Accept-encoding 標頭)</span><span class="sxs-lookup"><span data-stu-id="54a99-157">Client requested format (via Accept-Encoding header)</span></span> | <span data-ttu-id="54a99-158">快取的檔案格式</span><span class="sxs-lookup"><span data-stu-id="54a99-158">Cached file format</span></span> | <span data-ttu-id="54a99-159">CDN 對用戶端的回應</span><span class="sxs-lookup"><span data-stu-id="54a99-159">CDN response to the client</span></span> | <span data-ttu-id="54a99-160">注意事項</span><span class="sxs-lookup"><span data-stu-id="54a99-160">Notes</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="54a99-161">已壓縮</span><span class="sxs-lookup"><span data-stu-id="54a99-161">Compressed</span></span> |<span data-ttu-id="54a99-162">已壓縮</span><span class="sxs-lookup"><span data-stu-id="54a99-162">Compressed</span></span> |<span data-ttu-id="54a99-163">已壓縮</span><span class="sxs-lookup"><span data-stu-id="54a99-163">Compressed</span></span> | |
| <span data-ttu-id="54a99-164">已壓縮</span><span class="sxs-lookup"><span data-stu-id="54a99-164">Compressed</span></span> |<span data-ttu-id="54a99-165">未壓縮</span><span class="sxs-lookup"><span data-stu-id="54a99-165">Uncompressed</span></span> |<span data-ttu-id="54a99-166">未壓縮</span><span class="sxs-lookup"><span data-stu-id="54a99-166">Uncompressed</span></span> | |
| <span data-ttu-id="54a99-167">已壓縮</span><span class="sxs-lookup"><span data-stu-id="54a99-167">Compressed</span></span> |<span data-ttu-id="54a99-168">不快取</span><span class="sxs-lookup"><span data-stu-id="54a99-168">Not cached</span></span> |<span data-ttu-id="54a99-169">已壓縮或未壓縮</span><span class="sxs-lookup"><span data-stu-id="54a99-169">Compressed or Uncompressed</span></span> |<span data-ttu-id="54a99-170">取決於原始回應</span><span class="sxs-lookup"><span data-stu-id="54a99-170">Depends on origin response</span></span> |
| <span data-ttu-id="54a99-171">未壓縮</span><span class="sxs-lookup"><span data-stu-id="54a99-171">Uncompressed</span></span> |<span data-ttu-id="54a99-172">已壓縮</span><span class="sxs-lookup"><span data-stu-id="54a99-172">Compressed</span></span> |<span data-ttu-id="54a99-173">未壓縮</span><span class="sxs-lookup"><span data-stu-id="54a99-173">Uncompressed</span></span> | |
| <span data-ttu-id="54a99-174">未壓縮</span><span class="sxs-lookup"><span data-stu-id="54a99-174">Uncompressed</span></span> |<span data-ttu-id="54a99-175">未壓縮</span><span class="sxs-lookup"><span data-stu-id="54a99-175">Uncompressed</span></span> |<span data-ttu-id="54a99-176">未壓縮</span><span class="sxs-lookup"><span data-stu-id="54a99-176">Uncompressed</span></span> | |
| <span data-ttu-id="54a99-177">未壓縮</span><span class="sxs-lookup"><span data-stu-id="54a99-177">Uncompressed</span></span> |<span data-ttu-id="54a99-178">不快取</span><span class="sxs-lookup"><span data-stu-id="54a99-178">Not cached</span></span> |<span data-ttu-id="54a99-179">未壓縮</span><span class="sxs-lookup"><span data-stu-id="54a99-179">Uncompressed</span></span> | |

### <a name="compression-enabled-and-file-is-eligible-for-compression"></a><span data-ttu-id="54a99-180">啟用壓縮和檔案適合進行壓縮</span><span class="sxs-lookup"><span data-stu-id="54a99-180">Compression enabled and file is eligible for compression</span></span>
| <span data-ttu-id="54a99-181">用戶端要求的格式 (透過 Accept-encoding 標頭)</span><span class="sxs-lookup"><span data-stu-id="54a99-181">Client requested format (via Accept-Encoding header)</span></span> | <span data-ttu-id="54a99-182">快取的檔案格式</span><span class="sxs-lookup"><span data-stu-id="54a99-182">Cached file format</span></span> | <span data-ttu-id="54a99-183">CDN 對用戶端的回應</span><span class="sxs-lookup"><span data-stu-id="54a99-183">CDN response to the client</span></span> | <span data-ttu-id="54a99-184">注意事項</span><span class="sxs-lookup"><span data-stu-id="54a99-184">Notes</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="54a99-185">已壓縮</span><span class="sxs-lookup"><span data-stu-id="54a99-185">Compressed</span></span> |<span data-ttu-id="54a99-186">已壓縮</span><span class="sxs-lookup"><span data-stu-id="54a99-186">Compressed</span></span> |<span data-ttu-id="54a99-187">已壓縮</span><span class="sxs-lookup"><span data-stu-id="54a99-187">Compressed</span></span> |<span data-ttu-id="54a99-188">支援格式之間的 CDN 轉碼</span><span class="sxs-lookup"><span data-stu-id="54a99-188">CDN transcodes between supported formats</span></span> |
| <span data-ttu-id="54a99-189">已壓縮</span><span class="sxs-lookup"><span data-stu-id="54a99-189">Compressed</span></span> |<span data-ttu-id="54a99-190">未壓縮</span><span class="sxs-lookup"><span data-stu-id="54a99-190">Uncompressed</span></span> |<span data-ttu-id="54a99-191">已壓縮</span><span class="sxs-lookup"><span data-stu-id="54a99-191">Compressed</span></span> |<span data-ttu-id="54a99-192">CDN 執行壓縮</span><span class="sxs-lookup"><span data-stu-id="54a99-192">CDN performs compression</span></span> |
| <span data-ttu-id="54a99-193">已壓縮</span><span class="sxs-lookup"><span data-stu-id="54a99-193">Compressed</span></span> |<span data-ttu-id="54a99-194">不快取</span><span class="sxs-lookup"><span data-stu-id="54a99-194">Not cached</span></span> |<span data-ttu-id="54a99-195">已壓縮</span><span class="sxs-lookup"><span data-stu-id="54a99-195">Compressed</span></span> |<span data-ttu-id="54a99-196">如果來源傳回未壓縮，則 CDN 會執行壓縮。</span><span class="sxs-lookup"><span data-stu-id="54a99-196">CDN performs compression if origin returns uncompressed.</span></span>  <span data-ttu-id="54a99-197">**來自 Verizon 的 Azure CDN** 會傳遞第一次要求中的未壓縮檔案，然後壓縮及快取檔案以供後續要求之需。</span><span class="sxs-lookup"><span data-stu-id="54a99-197">**Azure CDN from Verizon** passes the uncompressed file on the first request and then compresses and caches the file for subsequent requests.</span></span>  <span data-ttu-id="54a99-198">具有 `Cache-Control: no-cache` 標頭的檔案永遠不會經過壓縮。</span><span class="sxs-lookup"><span data-stu-id="54a99-198">Files with `Cache-Control: no-cache` header will never be compressed.</span></span> |
| <span data-ttu-id="54a99-199">未壓縮</span><span class="sxs-lookup"><span data-stu-id="54a99-199">Uncompressed</span></span> |<span data-ttu-id="54a99-200">已壓縮</span><span class="sxs-lookup"><span data-stu-id="54a99-200">Compressed</span></span> |<span data-ttu-id="54a99-201">未壓縮</span><span class="sxs-lookup"><span data-stu-id="54a99-201">Uncompressed</span></span> |<span data-ttu-id="54a99-202">CDN 執行解壓縮</span><span class="sxs-lookup"><span data-stu-id="54a99-202">CDN performs decompression</span></span> |
| <span data-ttu-id="54a99-203">未壓縮</span><span class="sxs-lookup"><span data-stu-id="54a99-203">Uncompressed</span></span> |<span data-ttu-id="54a99-204">未壓縮</span><span class="sxs-lookup"><span data-stu-id="54a99-204">Uncompressed</span></span> |<span data-ttu-id="54a99-205">未壓縮</span><span class="sxs-lookup"><span data-stu-id="54a99-205">Uncompressed</span></span> | |
| <span data-ttu-id="54a99-206">未壓縮</span><span class="sxs-lookup"><span data-stu-id="54a99-206">Uncompressed</span></span> |<span data-ttu-id="54a99-207">不快取</span><span class="sxs-lookup"><span data-stu-id="54a99-207">Not cached</span></span> |<span data-ttu-id="54a99-208">未壓縮</span><span class="sxs-lookup"><span data-stu-id="54a99-208">Uncompressed</span></span> | |

## <a name="media-services-cdn-compression"></a><span data-ttu-id="54a99-209">媒體服務 CDN 壓縮</span><span class="sxs-lookup"><span data-stu-id="54a99-209">Media Services CDN Compression</span></span>
<span data-ttu-id="54a99-210">對於啟用媒體服務 CDN 的串流端點，壓縮功能依預設會針對下列內容類型啟用：application/vnd.ms-sstr+xml, application/dash+xml,application/vnd.apple.mpegurl, application/f4m+xml。</span><span class="sxs-lookup"><span data-stu-id="54a99-210">For Media Services CDN enabled streaming endpoints, compression is enabled by default for the following content types: application/vnd.ms-sstr+xml, application/dash+xml,application/vnd.apple.mpegurl, application/f4m+xml.</span></span> <span data-ttu-id="54a99-211">您不能使用 Azure 入口網站啟用/停用上述類型的壓縮。</span><span class="sxs-lookup"><span data-stu-id="54a99-211">You cannot enable/disable compression for the mentioned types using the Azure portal.</span></span>  

## <a name="see-also"></a><span data-ttu-id="54a99-212">另請參閱</span><span class="sxs-lookup"><span data-stu-id="54a99-212">See also</span></span>
* [<span data-ttu-id="54a99-213">CDN 檔案壓縮疑難排解</span><span class="sxs-lookup"><span data-stu-id="54a99-213">Troubleshooting CDN file compression</span></span>](cdn-troubleshoot-compression.md)    

