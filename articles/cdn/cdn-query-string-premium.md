---
title: "使用查詢字串控制 Azure CDN 快取行為 - Premium | Microsoft Docs"
description: "Azure CDN 查詢字串快取可控制檔案內含查詢字串時的檔案快取方式。"
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 99db4a85-4f5f-431f-ac3a-69e05518c997
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 145067c2ce50b41c4783f4de4052c0e7cb529fc7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="control-azure-cdn-caching-behavior-with-query-strings---premium"></a><span data-ttu-id="3ca34-103">使用查詢字串控制 Azure CDN 快取行為 - Premium</span><span class="sxs-lookup"><span data-stu-id="3ca34-103">Control Azure CDN caching behavior with query strings - Premium</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="3ca34-104">標準</span><span class="sxs-lookup"><span data-stu-id="3ca34-104">Standard</span></span>](cdn-query-string.md)
> * [<span data-ttu-id="3ca34-105">來自 Verizon 的 Azure CDN 進階</span><span class="sxs-lookup"><span data-stu-id="3ca34-105">Azure CDN Premium from Verizon</span></span>](cdn-query-string-premium.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="3ca34-106">概觀</span><span class="sxs-lookup"><span data-stu-id="3ca34-106">Overview</span></span>
<span data-ttu-id="3ca34-107">查詢字串快取可控制檔案內含查詢字串時的檔案快取方式。</span><span class="sxs-lookup"><span data-stu-id="3ca34-107">Query string caching controls how files are to be cached when they contain query strings.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3ca34-108">「標準」與「進階」CDN 產品提供相同的查詢字串快取功能，但兩者的使用者介面不同。</span><span class="sxs-lookup"><span data-stu-id="3ca34-108">The Standard and Premium CDN products provide the same query string caching functionality, but the user interface differs.</span></span>  <span data-ttu-id="3ca34-109">本文件描述 **來自 Verizon 的 Azure CDN 進階**的介面。</span><span class="sxs-lookup"><span data-stu-id="3ca34-109">This document describes the interface for **Azure CDN Premium from Verizon**.</span></span>  <span data-ttu-id="3ca34-110">如需利用**來自 Akamai 的 Azure CDN 標準**和**來自 Verizon 的 Azure CDN 標準**查詢字串快取，請參閱[利用查詢字串控制 CDN 要求的快取行為](cdn-query-string.md)。</span><span class="sxs-lookup"><span data-stu-id="3ca34-110">For query string caching with **Azure CDN Standard from Akamai** and **Azure CDN Standard from Verizon**, see [Controlling caching behavior of CDN requests with query strings](cdn-query-string.md).</span></span>
> 
> 

<span data-ttu-id="3ca34-111">提供三種可用模式：</span><span class="sxs-lookup"><span data-stu-id="3ca34-111">Three modes are available:</span></span>

* <span data-ttu-id="3ca34-112">**標準快取**：此為預設模式。</span><span class="sxs-lookup"><span data-stu-id="3ca34-112">**standard-cache**:  This is the default mode.</span></span>  <span data-ttu-id="3ca34-113">CDN 邊緣節點會將要求者發出的查詢字串，傳遞至第一個要求的來源並快取資產。</span><span class="sxs-lookup"><span data-stu-id="3ca34-113">The CDN edge node will pass the query string from the requestor to the origin on the first request and cache the asset.</span></span>  <span data-ttu-id="3ca34-114">快取的資產到期之前，所有從邊緣節點提供且針對該資產的後續查詢皆會忽略查詢字串。</span><span class="sxs-lookup"><span data-stu-id="3ca34-114">All subsequent requests for that asset that are served from the edge node will ignore the query string until the cached asset expires.</span></span>
* <span data-ttu-id="3ca34-115">**無快取**：在此模式中，系統不會於 CDN 邊緣節點快取包含查詢字串的要求。</span><span class="sxs-lookup"><span data-stu-id="3ca34-115">**no-cache**:  In this mode, requests with query strings are not cached at the CDN edge node.</span></span>  <span data-ttu-id="3ca34-116">邊緣節點會直接從來源擷取資產，然後透過每個要求將其傳遞給要求者。</span><span class="sxs-lookup"><span data-stu-id="3ca34-116">The edge node retrieves the asset directly from the origin and passes it to the requestor with each request.</span></span>
* <span data-ttu-id="3ca34-117">**唯一快取**：此模式會將包含查詢字串的每個要求視為具有專屬快取的唯一資產。</span><span class="sxs-lookup"><span data-stu-id="3ca34-117">**unique-cache**:  This mode treats each request with a query string as a unique asset with its own cache.</span></span>  <span data-ttu-id="3ca34-118">例如，系統會於邊緣節點快取 *foo.ashx?q=bar* 要求的來源回應，並使用相同的查詢字串針對後續快取傳回。</span><span class="sxs-lookup"><span data-stu-id="3ca34-118">For example, the response from the origin for a request for *foo.ashx?q=bar* would be cached at the edge node and returned for subsequent caches with that same query string.</span></span>  <span data-ttu-id="3ca34-119">針對 *foo.ashx?q=somethingelse* 要求，系統會將其快取為具專屬存留時間的個別資產。</span><span class="sxs-lookup"><span data-stu-id="3ca34-119">A request for *foo.ashx?q=somethingelse* would be cached as a separate asset with its own time to live.</span></span>

## <a name="changing-query-string-caching-settings-for-premium-cdn-profiles"></a><span data-ttu-id="3ca34-120">變更進階 CDN 設定檔的查詢字串快取設定</span><span class="sxs-lookup"><span data-stu-id="3ca34-120">Changing query string caching settings for premium CDN profiles</span></span>
1. <span data-ttu-id="3ca34-121">在 [CDN 設定檔] 刀鋒視窗中，按一下 [管理]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="3ca34-121">From the CDN profile blade, click the **Manage** button.</span></span>
   
    ![[CDN 設定檔] 刀鋒視窗的 [管理] 按鈕](./media/cdn-query-string-premium/cdn-manage-btn.png)
   
    <span data-ttu-id="3ca34-123">隨即開啟 CDN 管理入口網站。</span><span class="sxs-lookup"><span data-stu-id="3ca34-123">The CDN management portal opens.</span></span>
2. <span data-ttu-id="3ca34-124">將滑鼠移至 [HTTP 大型] 索引標籤上，然後將滑鼠移至 [快取設定] 飛出視窗上。</span><span class="sxs-lookup"><span data-stu-id="3ca34-124">Hover over the **HTTP Large** tab, then hover over the **Cache Settings** flyout.</span></span>  <span data-ttu-id="3ca34-125">按一下 [ **查詢字串快取**]。</span><span class="sxs-lookup"><span data-stu-id="3ca34-125">Click on **Query-String Caching**.</span></span>
   
    <span data-ttu-id="3ca34-126">查詢字串快取選項隨即顯示。</span><span class="sxs-lookup"><span data-stu-id="3ca34-126">Query string caching options are displayed.</span></span>
   
    ![CDN 查詢字串快取選項](./media/cdn-query-string-premium/cdn-query-string.png)
3. <span data-ttu-id="3ca34-128">進行選擇後，按一下 [ **更新** ] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="3ca34-128">After making your selection, click the **Update** button.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3ca34-129">設定變更可能無法立即看見，因為註冊資訊需要一段時間才能傳遍 CDN。</span><span class="sxs-lookup"><span data-stu-id="3ca34-129">The settings changes may not be immediately visible, as it takes time for the registration to propagate through the CDN.</span></span>  <span data-ttu-id="3ca34-130">若為<b>來自 Verizon 的 Azure CDN</b> 設定檔，則通常會在 90 分鐘之內完成傳播，但在某些情況下可能會更久。</span><span class="sxs-lookup"><span data-stu-id="3ca34-130">For <b>Azure CDN from Verizon</b> profiles, propagation will usually complete within 90 minutes, but in some cases can take longer.</span></span>
> 
> 

