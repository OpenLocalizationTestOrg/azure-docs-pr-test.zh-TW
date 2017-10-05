---
title: "使用查詢字串控制 Azure CDN 快取行為 | Microsoft Docs"
description: "Azure CDN 查詢字串快取可控制檔案內含查詢字串時的檔案快取方式。"
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 17410e4f-130e-489c-834e-7ca6d6f9778d
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 8d79626fa8516f226a82d3dac693c2033904c91d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="control-azure-cdn-caching-behavior-with-query-strings"></a><span data-ttu-id="dbdb3-103">使用查詢字串控制 Azure CDN 快取行為</span><span class="sxs-lookup"><span data-stu-id="dbdb3-103">Control Azure CDN caching behavior with query strings</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="dbdb3-104">標準</span><span class="sxs-lookup"><span data-stu-id="dbdb3-104">Standard</span></span>](cdn-query-string.md)
> * [<span data-ttu-id="dbdb3-105">來自 Verizon 的 Azure CDN 進階</span><span class="sxs-lookup"><span data-stu-id="dbdb3-105">Azure CDN Premium from Verizon</span></span>](cdn-query-string-premium.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="dbdb3-106">概觀</span><span class="sxs-lookup"><span data-stu-id="dbdb3-106">Overview</span></span>
<span data-ttu-id="dbdb3-107">查詢字串快取可控制檔案內含查詢字串時的檔案快取方式。</span><span class="sxs-lookup"><span data-stu-id="dbdb3-107">Query string caching controls how files are to be cached when they contain query strings.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="dbdb3-108">「標準」與「進階」CDN 產品提供相同的查詢字串快取功能，但兩者的使用者介面不同。</span><span class="sxs-lookup"><span data-stu-id="dbdb3-108">The Standard and Premium CDN products provide the same query string caching functionality, but the user interface differs.</span></span>  <span data-ttu-id="dbdb3-109">本文件描述**來自 Akamai 的 Azure CDN 標準**和**來自 Verizon 的 Azure CDN 標準**的介面。</span><span class="sxs-lookup"><span data-stu-id="dbdb3-109">This document describes the interface for **Azure CDN Standard from Akamai** and **Azure CDN Standard from Verizon**.</span></span>  <span data-ttu-id="dbdb3-110">如需利用 **來自 Verizon 的 Azure CDN 進階**查詢字串快取，請參閱 [利用查詢字串控制 CDN 要求的快取行為 - 進階](cdn-query-string-premium.md)。</span><span class="sxs-lookup"><span data-stu-id="dbdb3-110">For query string caching with **Azure CDN Premium from Verizon**, see [Controlling caching behavior of CDN requests with query strings - Premium](cdn-query-string-premium.md).</span></span>
> 
> 

<span data-ttu-id="dbdb3-111">提供三種可用模式：</span><span class="sxs-lookup"><span data-stu-id="dbdb3-111">Three modes are available:</span></span>

* <span data-ttu-id="dbdb3-112">**忽略查詢字串**：這是預設模式。</span><span class="sxs-lookup"><span data-stu-id="dbdb3-112">**Ignore query strings**:  This is the default mode.</span></span>  <span data-ttu-id="dbdb3-113">CDN 邊緣節點會將要求者發出的查詢字串，傳遞至第一個要求的來源並快取資產。</span><span class="sxs-lookup"><span data-stu-id="dbdb3-113">The CDN edge node will pass the query string from the requestor to the origin on the first request and cache the asset.</span></span>  <span data-ttu-id="dbdb3-114">快取的資產到期之前，所有從邊緣節點提供且針對該資產的後續查詢皆會忽略查詢字串。</span><span class="sxs-lookup"><span data-stu-id="dbdb3-114">All subsequent requests for that asset that are served from the edge node will ignore the query string until the cached asset expires.</span></span>
* <span data-ttu-id="dbdb3-115">**略過包含查詢字串之 URL 的快取**：在此模式中，系統不會於 CDN 邊緣節點快取包含查詢字串的要求。</span><span class="sxs-lookup"><span data-stu-id="dbdb3-115">**Bypass caching for URL with query strings**:  In this mode, requests with query strings are not cached at the CDN edge node.</span></span>  <span data-ttu-id="dbdb3-116">邊緣節點會直接從來源擷取資產，然後透過每個要求將其傳遞給要求者。</span><span class="sxs-lookup"><span data-stu-id="dbdb3-116">The edge node retrieves the asset directly from the origin and passes it to the requestor with each request.</span></span>
* <span data-ttu-id="dbdb3-117">**快取每個唯一 URL**：此模式會將包含查詢字串的每個要求視為具有專屬快取的唯一資產。</span><span class="sxs-lookup"><span data-stu-id="dbdb3-117">**Cache every unique URL**:  This mode treats each request with a query string as a unique asset with its own cache.</span></span>  <span data-ttu-id="dbdb3-118">例如，系統會於邊緣節點快取 *foo.ashx?q=bar* 要求的來源回應，並使用相同的查詢字串針對後續快取傳回。</span><span class="sxs-lookup"><span data-stu-id="dbdb3-118">For example, the response from the origin for a request for *foo.ashx?q=bar* would be cached at the edge node and returned for subsequent caches with that same query string.</span></span>  <span data-ttu-id="dbdb3-119">針對 *foo.ashx?q=somethingelse* 要求，系統會將其快取為具專屬存留時間的個別資產。</span><span class="sxs-lookup"><span data-stu-id="dbdb3-119">A request for *foo.ashx?q=somethingelse* would be cached as a separate asset with its own time to live.</span></span>

## <a name="changing-query-string-caching-settings-for-standard-cdn-profiles"></a><span data-ttu-id="dbdb3-120">變更標準 CDN 設定檔的查詢字串快取設定</span><span class="sxs-lookup"><span data-stu-id="dbdb3-120">Changing query string caching settings for standard CDN profiles</span></span>
1. <span data-ttu-id="dbdb3-121">在 [CDN 設定檔] 刀鋒視窗中，按一下您要管理的 CDN 端點。</span><span class="sxs-lookup"><span data-stu-id="dbdb3-121">From the CDN profile blade, click the CDN endpoint you wish to manage.</span></span>
   
    ![[CDN 設定檔] 刀鋒視窗端點](./media/cdn-query-string/cdn-endpoints.png)
   
    <span data-ttu-id="dbdb3-123">隨即開啟 [CDN 端點] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="dbdb3-123">The CDN endpoint blade opens.</span></span>
2. <span data-ttu-id="dbdb3-124">按一下 [設定]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="dbdb3-124">Click the **Configure** button.</span></span>
   
    ![[CDN 設定檔] 刀鋒視窗管理按鈕](./media/cdn-query-string/cdn-config-btn.png)
   
    <span data-ttu-id="dbdb3-126">[CDN 組態] 刀鋒視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="dbdb3-126">The CDN Configuration blade opens.</span></span>
3. <span data-ttu-id="dbdb3-127">從 [查詢字串快取行為]  下拉式清單選取設定。</span><span class="sxs-lookup"><span data-stu-id="dbdb3-127">Select a setting from the **Query string caching behavior** dropdown.</span></span>
   
    ![CDN 查詢字串快取選項](./media/cdn-query-string/cdn-query-string.png)
4. <span data-ttu-id="dbdb3-129">進行選擇後，按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="dbdb3-129">After making your selection, click the **Save** button.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="dbdb3-130">設定變更可能無法立即看見，因為註冊資訊需要一段時間才能傳遍 CDN。</span><span class="sxs-lookup"><span data-stu-id="dbdb3-130">The settings changes may not be immediately visible, as it takes time for the registration to propagate through the CDN.</span></span>  <span data-ttu-id="dbdb3-131">在 [通訊協定] <b>來自 Akamai 的 Azure CDN</b> 設定檔，通常會在一分鐘之內完成傳播。</span><span class="sxs-lookup"><span data-stu-id="dbdb3-131">For <b>Azure CDN from Akamai</b> profiles, propagation will usually complete within one minute.</span></span>  <span data-ttu-id="dbdb3-132">若為<b>來自 Verizon 的 Azure CDN</b> 設定檔，則通常會在 90 分鐘之內完成傳播，但在某些情況下可能會更久。</span><span class="sxs-lookup"><span data-stu-id="dbdb3-132">For <b>Azure CDN from Verizon</b> profiles, propagation will usually complete within 90 minutes, but in some cases can take longer.</span></span>
> 
> 

