---
title: "針對 Azure CDN 中的檔案壓縮進行疑難排解 | Microsoft Docs"
description: "針對 Azure CDN 檔案壓縮的問題進行疑難排解。"
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: a6624e65-1a77-4486-b473-8d720ce28f8b
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 5ef8a8262eb40aa827161764f03a63d031e43273
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting-cdn-file-compression"></a><span data-ttu-id="70925-103">CDN 檔案壓縮疑難排解</span><span class="sxs-lookup"><span data-stu-id="70925-103">Troubleshooting CDN file compression</span></span>
<span data-ttu-id="70925-104">這篇文章可協助您針對 [CDN 檔案壓縮](cdn-improve-performance.md)的問題進行疑難排解。</span><span class="sxs-lookup"><span data-stu-id="70925-104">This article helps you troubleshoot issues with [CDN file compression](cdn-improve-performance.md).</span></span>

<span data-ttu-id="70925-105">如果在本文章中有任何需要協助的地方，您可以連絡 [MSDN Azure 和 Stack Overflow 論壇](https://azure.microsoft.com/support/forums/)上的 Azure 專家。</span><span class="sxs-lookup"><span data-stu-id="70925-105">If you need more help at any point in this article, you can contact the Azure experts on [the MSDN Azure and the Stack Overflow forums](https://azure.microsoft.com/support/forums/).</span></span> <span data-ttu-id="70925-106">或者，您也可以提出 Azure 支援事件。</span><span class="sxs-lookup"><span data-stu-id="70925-106">Alternatively, you can also file an Azure support incident.</span></span> <span data-ttu-id="70925-107">請移至 [Azure 支援網站](https://azure.microsoft.com/support/options/)，然後按一下 [取得支援]。</span><span class="sxs-lookup"><span data-stu-id="70925-107">Go to the [Azure Support site](https://azure.microsoft.com/support/options/) and click **Get Support**.</span></span>

## <a name="symptom"></a><span data-ttu-id="70925-108">徵狀</span><span class="sxs-lookup"><span data-stu-id="70925-108">Symptom</span></span>
<span data-ttu-id="70925-109">已為您的端點啟用壓縮，但會傳回未壓縮的檔案。</span><span class="sxs-lookup"><span data-stu-id="70925-109">Compression for your endpoint is enabled, but files are being returned uncompressed.</span></span>

> [!TIP]
> <span data-ttu-id="70925-110">若要檢查傳回的檔案是否會壓縮，您需要使用 [Fiddler](http://www.telerik.com/fiddler) 之類的工具或您瀏覽器的[開發人員工具](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/)。</span><span class="sxs-lookup"><span data-stu-id="70925-110">To check whether your files are being returned compressed, you need to use a tool like [Fiddler](http://www.telerik.com/fiddler) or your browser's [developer tools](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/).</span></span>  <span data-ttu-id="70925-111">檢查隨快取的 CDN 內容傳回的 HTTP 回應標頭。</span><span class="sxs-lookup"><span data-stu-id="70925-111">Check the HTTP response headers returned with your cached CDN content.</span></span>  <span data-ttu-id="70925-112">如果名為 `Content-Encoding` 的標頭有 **gzip**、**bzip2** 或 **deflate** 值，內容會進行壓縮。</span><span class="sxs-lookup"><span data-stu-id="70925-112">If there is a header named `Content-Encoding` with a value of **gzip**, **bzip2**, or **deflate**, your content is compressed.</span></span>
> 
> ![Content-Encoding 標頭](./media/cdn-troubleshoot-compression/cdn-content-header.png)
> 
> 

## <a name="cause"></a><span data-ttu-id="70925-114">原因</span><span class="sxs-lookup"><span data-stu-id="70925-114">Cause</span></span>
<span data-ttu-id="70925-115">有幾個可能的原因，包括︰</span><span class="sxs-lookup"><span data-stu-id="70925-115">There are several possible causes, including:</span></span>

* <span data-ttu-id="70925-116">要求的內容不適合進行壓縮。</span><span class="sxs-lookup"><span data-stu-id="70925-116">The requested content is not eligible for compression.</span></span>
* <span data-ttu-id="70925-117">要求的檔案類型未啟用壓縮。</span><span class="sxs-lookup"><span data-stu-id="70925-117">Compression is not enabled for the requested file type.</span></span>
* <span data-ttu-id="70925-118">HTTP 要求未包含要求有效壓縮類型的標頭。</span><span class="sxs-lookup"><span data-stu-id="70925-118">The HTTP request did not include a header requesting a valid compression type.</span></span>

## <a name="troubleshooting-steps"></a><span data-ttu-id="70925-119">疑難排解步驟</span><span class="sxs-lookup"><span data-stu-id="70925-119">Troubleshooting steps</span></span>
> [!TIP]
> <span data-ttu-id="70925-120">隨著新端點的部署，CDN 組態變更會需要一些時間才能傳播至整個網路。</span><span class="sxs-lookup"><span data-stu-id="70925-120">As with deploying new endpoints, CDN configuration changes take some time to propagate through the network.</span></span>  <span data-ttu-id="70925-121">變更通常會在 90 分鐘內套用。</span><span class="sxs-lookup"><span data-stu-id="70925-121">Usually, changes are applied within 90 minutes.</span></span>  <span data-ttu-id="70925-122">如果這是您第一次設定 CDN 端點壓縮，您應該考慮先等候 1-2 小時，確定壓縮設定已傳播至 POP。</span><span class="sxs-lookup"><span data-stu-id="70925-122">If this is the first time you've set up compression for your CDN endpoint, you should consider waiting 1-2 hours to be sure the compression settings have propagated to the POPs.</span></span> 
> 
> 

### <a name="verify-the-request"></a><span data-ttu-id="70925-123">驗證要求</span><span class="sxs-lookup"><span data-stu-id="70925-123">Verify the request</span></span>
<span data-ttu-id="70925-124">首先，我們應該對要求進行快速的例行性檢查。</span><span class="sxs-lookup"><span data-stu-id="70925-124">First, we should do a quick sanity check on the request.</span></span>  <span data-ttu-id="70925-125">您可以使用瀏覽器的 [開發人員工具](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/) 來檢視所做的要求。</span><span class="sxs-lookup"><span data-stu-id="70925-125">You can use your browser's [developer tools](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/) to view the requests being made.</span></span>

* <span data-ttu-id="70925-126">驗證要求正傳送至您的端點 URL `<endpointname>.azureedge.net`，而不是您的來源。</span><span class="sxs-lookup"><span data-stu-id="70925-126">Verify the request is being sent to your endpoint URL, `<endpointname>.azureedge.net`, and not your origin.</span></span>
* <span data-ttu-id="70925-127">驗證要求包含 **Accept-Encoding** 標頭，且該標頭的值包含 **gzip**、**deflate** 或 **bzip2**。</span><span class="sxs-lookup"><span data-stu-id="70925-127">Verify the request contains an **Accept-Encoding** header, and the value for that header contains **gzip**, **deflate**, or **bzip2**.</span></span>

> [!NOTE]
> <span data-ttu-id="70925-128">**來自 Akamai 的 Azure CDN** 設定檔只支援 **gzip** 編碼。</span><span class="sxs-lookup"><span data-stu-id="70925-128">**Azure CDN from Akamai** profiles only support **gzip** encoding.</span></span>
> 
> 

![CDN 要求標頭](./media/cdn-troubleshoot-compression/cdn-request-headers.png)

### <a name="verify-compression-settings-standard-cdn-profile"></a><span data-ttu-id="70925-130">驗證壓縮設定 (標準 CDN 設定檔)</span><span class="sxs-lookup"><span data-stu-id="70925-130">Verify compression settings (Standard CDN profile)</span></span>
> [!NOTE]
> <span data-ttu-id="70925-131">如果您的 CDN 設定檔是**來自 Akamai 的 Azure CDN 標準**或**來自 Verizon 的 Azure CDN 標準**設定檔，才能套用此步驟。</span><span class="sxs-lookup"><span data-stu-id="70925-131">This step only applies if your CDN profile is an **Azure CDN Standard from Verizon** or **Azure CDN Standard from Akamai** profile.</span></span> 
> 
> 

<span data-ttu-id="70925-132">在 [Azure 入口網站](https://portal.azure.com)中瀏覽至您的端點，然後按一下 [設定] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="70925-132">Navigate to your endpoint in the [Azure portal](https://portal.azure.com) and click the **Configure** button.</span></span>

* <span data-ttu-id="70925-133">驗證已啟用壓縮。</span><span class="sxs-lookup"><span data-stu-id="70925-133">Verify compression is enabled.</span></span>
* <span data-ttu-id="70925-134">驗證要壓縮之內容的 MIME 類型已包含在壓縮格式清單中。</span><span class="sxs-lookup"><span data-stu-id="70925-134">Verify the MIME type for the content to be compressed is included in the list of compressed formats.</span></span>

![CDN 壓縮設定](./media/cdn-troubleshoot-compression/cdn-compression-settings.png)

### <a name="verify-compression-settings-premium-cdn-profile"></a><span data-ttu-id="70925-136">驗證壓縮設定 (進階 CDN 設定檔)</span><span class="sxs-lookup"><span data-stu-id="70925-136">Verify compression settings (Premium CDN profile)</span></span>
> [!NOTE]
> <span data-ttu-id="70925-137">如果您的 CDN 設定檔是 **來自 Verizon 的 Azure CDN 進階** 設定檔，才能套用此步驟。</span><span class="sxs-lookup"><span data-stu-id="70925-137">This step only applies if your CDN profile is an **Azure CDN Premium from Verizon** profile.</span></span>
> 
> 

<span data-ttu-id="70925-138">在 [Azure 入口網站](https://portal.azure.com)中瀏覽至您的端點，然後按一下 [管理] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="70925-138">Navigate to your endpoint in the [Azure portal](https://portal.azure.com) and click the **Manage** button.</span></span>  <span data-ttu-id="70925-139">即會開啟補充入口網站。</span><span class="sxs-lookup"><span data-stu-id="70925-139">The supplemental portal will open.</span></span>  <span data-ttu-id="70925-140">將滑鼠移至 [HTTP 大型] 索引標籤上，然後將滑鼠移至 [快取設定] 飛出視窗上。</span><span class="sxs-lookup"><span data-stu-id="70925-140">Hover over the **HTTP Large** tab, then hover over the **Cache Settings** flyout.</span></span>  <span data-ttu-id="70925-141">按一下 [壓縮]。</span><span class="sxs-lookup"><span data-stu-id="70925-141">Click **Compression**.</span></span> 

* <span data-ttu-id="70925-142">驗證已啟用壓縮。</span><span class="sxs-lookup"><span data-stu-id="70925-142">Verify compression is enabled.</span></span>
* <span data-ttu-id="70925-143">驗證 [檔案類型]  清單包含以逗號分隔 (無空格) 的 MIME 類型清單。</span><span class="sxs-lookup"><span data-stu-id="70925-143">Verify the **File Types** list contains a comma-separated list (no spaces) of MIME types.</span></span>
* <span data-ttu-id="70925-144">驗證要壓縮之內容的 MIME 類型已包含在壓縮格式清單中。</span><span class="sxs-lookup"><span data-stu-id="70925-144">Verify the MIME type for the content to be compressed is included in the list of compressed formats.</span></span>

![CDN 進階壓縮設定](./media/cdn-troubleshoot-compression/cdn-compression-settings-premium.png)

### <a name="verify-the-content-is-cached"></a><span data-ttu-id="70925-146">驗證已快取內容</span><span class="sxs-lookup"><span data-stu-id="70925-146">Verify the content is cached</span></span>
> [!NOTE]
> <span data-ttu-id="70925-147">如果您的 CDN 設定檔是 **來自 Verizon 的 Azure CDN** 設定檔 (標準或進階)，才能套用此步驟。</span><span class="sxs-lookup"><span data-stu-id="70925-147">This step only applies if your CDN profile is an **Azure CDN from Verizon** profile (Standard or Premium).</span></span>
> 
> 

<span data-ttu-id="70925-148">使用您瀏覽器的開發人員工具，檢查回應標頭以確保檔案會快取在要求它的區域中。</span><span class="sxs-lookup"><span data-stu-id="70925-148">Using your browser's developer tools, check the response headers to ensure the file is cached in the region where it is being requested.</span></span>

* <span data-ttu-id="70925-149">檢查 **Server** 回應標頭。</span><span class="sxs-lookup"><span data-stu-id="70925-149">Check the **Server** response header.</span></span>  <span data-ttu-id="70925-150">標頭應該具有格式 **平台 (POP/伺服器識別碼)**，如下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="70925-150">The header should have the format **Platform (POP/Server ID)**, as seen in the following example.</span></span>
* <span data-ttu-id="70925-151">檢查 **X-Cache** 回應標頭。</span><span class="sxs-lookup"><span data-stu-id="70925-151">Check the **X-Cache** response header.</span></span>  <span data-ttu-id="70925-152">標頭應為 **HIT**。</span><span class="sxs-lookup"><span data-stu-id="70925-152">The header should read **HIT**.</span></span>  

![CDN 回應標頭](./media/cdn-troubleshoot-compression/cdn-response-headers.png)

### <a name="verify-the-file-meets-the-size-requirements"></a><span data-ttu-id="70925-154">驗證檔案符合大小需求</span><span class="sxs-lookup"><span data-stu-id="70925-154">Verify the file meets the size requirements</span></span>
> [!NOTE]
> <span data-ttu-id="70925-155">如果您的 CDN 設定檔是 **來自 Verizon 的 Azure CDN** 設定檔 (標準或進階)，才能套用此步驟。</span><span class="sxs-lookup"><span data-stu-id="70925-155">This step only applies if your CDN profile is an **Azure CDN from Verizon** profile (Standard or Premium).</span></span>
> 
> 

<span data-ttu-id="70925-156">若要進行壓縮，檔案必須符合下列的大小需求︰</span><span class="sxs-lookup"><span data-stu-id="70925-156">To be eligible for compression, a file must meet the following size requirements:</span></span>

* <span data-ttu-id="70925-157">超過 128 個位元組。</span><span class="sxs-lookup"><span data-stu-id="70925-157">Larger than 128 bytes.</span></span>
* <span data-ttu-id="70925-158">小於 1 MB。</span><span class="sxs-lookup"><span data-stu-id="70925-158">Smaller than 1 MB.</span></span>

### <a name="check-the-request-at-the-origin-server-for-a-via-header"></a><span data-ttu-id="70925-159">在原始伺服器中檢查要求的 **Via** 標頭</span><span class="sxs-lookup"><span data-stu-id="70925-159">Check the request at the origin server for a **Via** header</span></span>
<span data-ttu-id="70925-160">**Via** HTTP 標頭會向 Web 伺服器指出正在由 Proxy 伺服器傳遞要求。</span><span class="sxs-lookup"><span data-stu-id="70925-160">The **Via** HTTP header indicates to the web server that the request is being passed by a proxy server.</span></span>  <span data-ttu-id="70925-161">Microsoft IIS Web 伺服器預設不會在要求包含 **Via** 標頭時壓縮回應。</span><span class="sxs-lookup"><span data-stu-id="70925-161">Microsoft IIS web servers by default do not compress responses when the request contains a **Via** header.</span></span>  <span data-ttu-id="70925-162">若要覆寫這個行為，請執行下列作業︰</span><span class="sxs-lookup"><span data-stu-id="70925-162">To override this behavior, perform the following:</span></span>

* <span data-ttu-id="70925-163">**IIS 6**： [在 IIS Metabase 屬性中設定 HcNoCompressionForProxies="FALSE"](https://msdn.microsoft.com/library/ms525390.aspx)</span><span class="sxs-lookup"><span data-stu-id="70925-163">**IIS 6**: [Set HcNoCompressionForProxies="FALSE" in the IIS Metabase properties](https://msdn.microsoft.com/library/ms525390.aspx)</span></span>
* <span data-ttu-id="70925-164">**IIS 7 和更新版本**：[在伺服器組態中將 **noCompressionForHttp10** 和 **noCompressionForProxies** 設定為 False](http://www.iis.net/configreference/system.webserver/httpcompression)</span><span class="sxs-lookup"><span data-stu-id="70925-164">**IIS 7 and up**: [Set both **noCompressionForHttp10** and **noCompressionForProxies** to False in the server configuration](http://www.iis.net/configreference/system.webserver/httpcompression)</span></span>

