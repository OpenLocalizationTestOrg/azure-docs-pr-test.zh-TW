---
title: "在 Azure CDN aaaTroubleshooting 檔案壓縮 |Microsoft 文件"
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
ms.openlocfilehash: f00b98beaf6b3b3cd30108ece65a8191edc06ff5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-cdn-file-compression"></a><span data-ttu-id="baf84-103">CDN 檔案壓縮疑難排解</span><span class="sxs-lookup"><span data-stu-id="baf84-103">Troubleshooting CDN file compression</span></span>
<span data-ttu-id="baf84-104">這篇文章可協助您針對 [CDN 檔案壓縮](cdn-improve-performance.md)的問題進行疑難排解。</span><span class="sxs-lookup"><span data-stu-id="baf84-104">This article helps you troubleshoot issues with [CDN file compression](cdn-improve-performance.md).</span></span>

<span data-ttu-id="baf84-105">如果您需要更多說明，在本文中的任何時間點，您可以連絡上 hello Azure 專家[hello MSDN Azure 和 hello 堆疊溢位論壇](https://azure.microsoft.com/support/forums/)。</span><span class="sxs-lookup"><span data-stu-id="baf84-105">If you need more help at any point in this article, you can contact hello Azure experts on [hello MSDN Azure and hello Stack Overflow forums](https://azure.microsoft.com/support/forums/).</span></span> <span data-ttu-id="baf84-106">或者，您也可以提出 Azure 支援事件。</span><span class="sxs-lookup"><span data-stu-id="baf84-106">Alternatively, you can also file an Azure support incident.</span></span> <span data-ttu-id="baf84-107">移 toohello [Azure 支援服務網站](https://azure.microsoft.com/support/options/)按一下**取得支援**。</span><span class="sxs-lookup"><span data-stu-id="baf84-107">Go toohello [Azure Support site](https://azure.microsoft.com/support/options/) and click **Get Support**.</span></span>

## <a name="symptom"></a><span data-ttu-id="baf84-108">徵狀</span><span class="sxs-lookup"><span data-stu-id="baf84-108">Symptom</span></span>
<span data-ttu-id="baf84-109">已為您的端點啟用壓縮，但會傳回未壓縮的檔案。</span><span class="sxs-lookup"><span data-stu-id="baf84-109">Compression for your endpoint is enabled, but files are being returned uncompressed.</span></span>

> [!TIP]
> <span data-ttu-id="baf84-110">toocheck 檔案會被傳回壓縮，是否需要一種工具要的 toouse [Fiddler](http://www.telerik.com/fiddler)或您的瀏覽器[開發人員工具](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/)。</span><span class="sxs-lookup"><span data-stu-id="baf84-110">toocheck whether your files are being returned compressed, you need toouse a tool like [Fiddler](http://www.telerik.com/fiddler) or your browser's [developer tools](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/).</span></span>  <span data-ttu-id="baf84-111">核取 hello HTTP 回應標頭傳回您的快取 CDN 內容。</span><span class="sxs-lookup"><span data-stu-id="baf84-111">Check hello HTTP response headers returned with your cached CDN content.</span></span>  <span data-ttu-id="baf84-112">如果名為 `Content-Encoding` 的標頭有 **gzip**、**bzip2** 或 **deflate** 值，內容會進行壓縮。</span><span class="sxs-lookup"><span data-stu-id="baf84-112">If there is a header named `Content-Encoding` with a value of **gzip**, **bzip2**, or **deflate**, your content is compressed.</span></span>
> 
> ![Content-Encoding 標頭](./media/cdn-troubleshoot-compression/cdn-content-header.png)
> 
> 

## <a name="cause"></a><span data-ttu-id="baf84-114">原因</span><span class="sxs-lookup"><span data-stu-id="baf84-114">Cause</span></span>
<span data-ttu-id="baf84-115">有幾個可能的原因，包括︰</span><span class="sxs-lookup"><span data-stu-id="baf84-115">There are several possible causes, including:</span></span>

* <span data-ttu-id="baf84-116">hello 要求內容不符合資格的壓縮。</span><span class="sxs-lookup"><span data-stu-id="baf84-116">hello requested content is not eligible for compression.</span></span>
* <span data-ttu-id="baf84-117">無法啟用壓縮 hello 要求的檔案類型。</span><span class="sxs-lookup"><span data-stu-id="baf84-117">Compression is not enabled for hello requested file type.</span></span>
* <span data-ttu-id="baf84-118">hello HTTP 要求不包含標頭要求有效的壓縮類型。</span><span class="sxs-lookup"><span data-stu-id="baf84-118">hello HTTP request did not include a header requesting a valid compression type.</span></span>

## <a name="troubleshooting-steps"></a><span data-ttu-id="baf84-119">疑難排解步驟</span><span class="sxs-lookup"><span data-stu-id="baf84-119">Troubleshooting steps</span></span>
> [!TIP]
> <span data-ttu-id="baf84-120">與部署新的端點，CDN 的設定變更都會透過 hello 網路某些時間 toopropagate。</span><span class="sxs-lookup"><span data-stu-id="baf84-120">As with deploying new endpoints, CDN configuration changes take some time toopropagate through hello network.</span></span>  <span data-ttu-id="baf84-121">變更通常會在 90 分鐘內套用。</span><span class="sxs-lookup"><span data-stu-id="baf84-121">Usually, changes are applied within 90 minutes.</span></span>  <span data-ttu-id="baf84-122">如果這是 hello 您為您的 CDN 端點設定壓縮的第一次，您應該考慮等候 1-2 小時 toobe 確定 hello 壓縮設定都已傳播 toohello 快顯。</span><span class="sxs-lookup"><span data-stu-id="baf84-122">If this is hello first time you've set up compression for your CDN endpoint, you should consider waiting 1-2 hours toobe sure hello compression settings have propagated toohello POPs.</span></span> 
> 
> 

### <a name="verify-hello-request"></a><span data-ttu-id="baf84-123">確認 hello 要求</span><span class="sxs-lookup"><span data-stu-id="baf84-123">Verify hello request</span></span>
<span data-ttu-id="baf84-124">首先，我們應該進行 hello 要求快速例行性檢查。</span><span class="sxs-lookup"><span data-stu-id="baf84-124">First, we should do a quick sanity check on hello request.</span></span>  <span data-ttu-id="baf84-125">您可以使用您的瀏覽器[開發人員工具](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/)tooview hello 提出的要求。</span><span class="sxs-lookup"><span data-stu-id="baf84-125">You can use your browser's [developer tools](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/) tooview hello requests being made.</span></span>

* <span data-ttu-id="baf84-126">請確認正在傳送嗨要求 tooyour 端點 URL， `<endpointname>.azureedge.net`，並不是您的原點。</span><span class="sxs-lookup"><span data-stu-id="baf84-126">Verify hello request is being sent tooyour endpoint URL, `<endpointname>.azureedge.net`, and not your origin.</span></span>
* <span data-ttu-id="baf84-127">請確認 hello 要求包含**Accept-encoding**該標頭包含標頭和 hello 值**gzip**， **deflate**，或**bzip2**.</span><span class="sxs-lookup"><span data-stu-id="baf84-127">Verify hello request contains an **Accept-Encoding** header, and hello value for that header contains **gzip**, **deflate**, or **bzip2**.</span></span>

> [!NOTE]
> <span data-ttu-id="baf84-128">**來自 Akamai 的 Azure CDN** 設定檔只支援 **gzip** 編碼。</span><span class="sxs-lookup"><span data-stu-id="baf84-128">**Azure CDN from Akamai** profiles only support **gzip** encoding.</span></span>
> 
> 

![CDN 要求標頭](./media/cdn-troubleshoot-compression/cdn-request-headers.png)

### <a name="verify-compression-settings-standard-cdn-profile"></a><span data-ttu-id="baf84-130">驗證壓縮設定 (標準 CDN 設定檔)</span><span class="sxs-lookup"><span data-stu-id="baf84-130">Verify compression settings (Standard CDN profile)</span></span>
> [!NOTE]
> <span data-ttu-id="baf84-131">如果您的 CDN 設定檔是**來自 Akamai 的 Azure CDN 標準**或**來自 Verizon 的 Azure CDN 標準**設定檔，才能套用此步驟。</span><span class="sxs-lookup"><span data-stu-id="baf84-131">This step only applies if your CDN profile is an **Azure CDN Standard from Verizon** or **Azure CDN Standard from Akamai** profile.</span></span> 
> 
> 

<span data-ttu-id="baf84-132">瀏覽在 hello tooyour 端點[Azure 入口網站](https://portal.azure.com)按一下 hello**設定** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="baf84-132">Navigate tooyour endpoint in hello [Azure portal](https://portal.azure.com) and click hello **Configure** button.</span></span>

* <span data-ttu-id="baf84-133">驗證已啟用壓縮。</span><span class="sxs-lookup"><span data-stu-id="baf84-133">Verify compression is enabled.</span></span>
* <span data-ttu-id="baf84-134">請確認 hello 內容 toobe 壓縮隨附的壓縮格式的 hello 清單中的 hello MIME 類型。</span><span class="sxs-lookup"><span data-stu-id="baf84-134">Verify hello MIME type for hello content toobe compressed is included in hello list of compressed formats.</span></span>

![CDN 壓縮設定](./media/cdn-troubleshoot-compression/cdn-compression-settings.png)

### <a name="verify-compression-settings-premium-cdn-profile"></a><span data-ttu-id="baf84-136">驗證壓縮設定 (進階 CDN 設定檔)</span><span class="sxs-lookup"><span data-stu-id="baf84-136">Verify compression settings (Premium CDN profile)</span></span>
> [!NOTE]
> <span data-ttu-id="baf84-137">如果您的 CDN 設定檔是 **來自 Verizon 的 Azure CDN 進階** 設定檔，才能套用此步驟。</span><span class="sxs-lookup"><span data-stu-id="baf84-137">This step only applies if your CDN profile is an **Azure CDN Premium from Verizon** profile.</span></span>
> 
> 

<span data-ttu-id="baf84-138">瀏覽在 hello tooyour 端點[Azure 入口網站](https://portal.azure.com)按一下 hello**管理** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="baf84-138">Navigate tooyour endpoint in hello [Azure portal](https://portal.azure.com) and click hello **Manage** button.</span></span>  <span data-ttu-id="baf84-139">hello 補充入口網站將會開啟。</span><span class="sxs-lookup"><span data-stu-id="baf84-139">hello supplemental portal will open.</span></span>  <span data-ttu-id="baf84-140">暫留在 hello **HTTP 大型** 索引標籤，然後暫留在 hello**快取設定**彈出式視窗。</span><span class="sxs-lookup"><span data-stu-id="baf84-140">Hover over hello **HTTP Large** tab, then hover over hello **Cache Settings** flyout.</span></span>  <span data-ttu-id="baf84-141">按一下 [壓縮]。</span><span class="sxs-lookup"><span data-stu-id="baf84-141">Click **Compression**.</span></span> 

* <span data-ttu-id="baf84-142">驗證已啟用壓縮。</span><span class="sxs-lookup"><span data-stu-id="baf84-142">Verify compression is enabled.</span></span>
* <span data-ttu-id="baf84-143">確認 hello**檔案類型**清單包含以逗號分隔清單 （無空格） 的 MIME 類型。</span><span class="sxs-lookup"><span data-stu-id="baf84-143">Verify hello **File Types** list contains a comma-separated list (no spaces) of MIME types.</span></span>
* <span data-ttu-id="baf84-144">請確認 hello 內容 toobe 壓縮隨附的壓縮格式的 hello 清單中的 hello MIME 類型。</span><span class="sxs-lookup"><span data-stu-id="baf84-144">Verify hello MIME type for hello content toobe compressed is included in hello list of compressed formats.</span></span>

![CDN 進階壓縮設定](./media/cdn-troubleshoot-compression/cdn-compression-settings-premium.png)

### <a name="verify-hello-content-is-cached"></a><span data-ttu-id="baf84-146">確認 hello 內容會快取</span><span class="sxs-lookup"><span data-stu-id="baf84-146">Verify hello content is cached</span></span>
> [!NOTE]
> <span data-ttu-id="baf84-147">如果您的 CDN 設定檔是 **來自 Verizon 的 Azure CDN** 設定檔 (標準或進階)，才能套用此步驟。</span><span class="sxs-lookup"><span data-stu-id="baf84-147">This step only applies if your CDN profile is an **Azure CDN from Verizon** profile (Standard or Premium).</span></span>
> 
> 

<span data-ttu-id="baf84-148">使用瀏覽器的開發人員工具，請檢查 hello 回應標頭 tooensure hello 檔案會快取，它所要求的 hello 區域中。</span><span class="sxs-lookup"><span data-stu-id="baf84-148">Using your browser's developer tools, check hello response headers tooensure hello file is cached in hello region where it is being requested.</span></span>

* <span data-ttu-id="baf84-149">檢查 hello**伺服器**回應標頭。</span><span class="sxs-lookup"><span data-stu-id="baf84-149">Check hello **Server** response header.</span></span>  <span data-ttu-id="baf84-150">hello 標頭應該具有 hello 格式**平台 (POP/伺服器 ID)**、 hello 下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="baf84-150">hello header should have hello format **Platform (POP/Server ID)**, as seen in hello following example.</span></span>
* <span data-ttu-id="baf84-151">檢查 hello **X 快取**回應標頭。</span><span class="sxs-lookup"><span data-stu-id="baf84-151">Check hello **X-Cache** response header.</span></span>  <span data-ttu-id="baf84-152">hello 標頭應該閱讀**叫用**。</span><span class="sxs-lookup"><span data-stu-id="baf84-152">hello header should read **HIT**.</span></span>  

![CDN 回應標頭](./media/cdn-troubleshoot-compression/cdn-response-headers.png)

### <a name="verify-hello-file-meets-hello-size-requirements"></a><span data-ttu-id="baf84-154">確認 hello 檔案符合 hello 大小需求</span><span class="sxs-lookup"><span data-stu-id="baf84-154">Verify hello file meets hello size requirements</span></span>
> [!NOTE]
> <span data-ttu-id="baf84-155">如果您的 CDN 設定檔是 **來自 Verizon 的 Azure CDN** 設定檔 (標準或進階)，才能套用此步驟。</span><span class="sxs-lookup"><span data-stu-id="baf84-155">This step only applies if your CDN profile is an **Azure CDN from Verizon** profile (Standard or Premium).</span></span>
> 
> 

<span data-ttu-id="baf84-156">toobe 能夠壓縮，檔案必須符合下列大小需求的 hello:</span><span class="sxs-lookup"><span data-stu-id="baf84-156">toobe eligible for compression, a file must meet hello following size requirements:</span></span>

* <span data-ttu-id="baf84-157">超過 128 個位元組。</span><span class="sxs-lookup"><span data-stu-id="baf84-157">Larger than 128 bytes.</span></span>
* <span data-ttu-id="baf84-158">小於 1 MB。</span><span class="sxs-lookup"><span data-stu-id="baf84-158">Smaller than 1 MB.</span></span>

### <a name="check-hello-request-at-hello-origin-server-for-a-via-header"></a><span data-ttu-id="baf84-159">檢查 hello 要求在原始伺服器 hello**透過**標頭</span><span class="sxs-lookup"><span data-stu-id="baf84-159">Check hello request at hello origin server for a **Via** header</span></span>
<span data-ttu-id="baf84-160">hello**透過**HTTP 標頭顯示由 proxy 伺服器傳遞 toohello hello 要求的網頁伺服器。</span><span class="sxs-lookup"><span data-stu-id="baf84-160">hello **Via** HTTP header indicates toohello web server that hello request is being passed by a proxy server.</span></span>  <span data-ttu-id="baf84-161">Microsoft IIS web 伺服器，預設不會壓縮回應 hello 要求包含當**透過**標頭。</span><span class="sxs-lookup"><span data-stu-id="baf84-161">Microsoft IIS web servers by default do not compress responses when hello request contains a **Via** header.</span></span>  <span data-ttu-id="baf84-162">toooverride 這種行為，執行下列 hello:</span><span class="sxs-lookup"><span data-stu-id="baf84-162">toooverride this behavior, perform hello following:</span></span>

* <span data-ttu-id="baf84-163">**IIS 6**:[設定 HcNoCompressionForProxies ="FALSE"hello IIS Metabase 內容中](https://msdn.microsoft.com/library/ms525390.aspx)</span><span class="sxs-lookup"><span data-stu-id="baf84-163">**IIS 6**: [Set HcNoCompressionForProxies="FALSE" in hello IIS Metabase properties](https://msdn.microsoft.com/library/ms525390.aspx)</span></span>
* <span data-ttu-id="baf84-164">**IIS 7 版與**:[同時設定**noCompressionForHttp10**和**noCompressionForProxies** tooFalse hello 伺服器設定中](http://www.iis.net/configreference/system.webserver/httpcompression)</span><span class="sxs-lookup"><span data-stu-id="baf84-164">**IIS 7 and up**: [Set both **noCompressionForHttp10** and **noCompressionForProxies** tooFalse in hello server configuration](http://www.iis.net/configreference/system.webserver/httpcompression)</span></span>

