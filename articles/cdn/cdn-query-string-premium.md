---
title: "Azure CDN 快取行為，與查詢字串-Premium aaaControl |Microsoft 文件"
description: "Azure CDN 查詢字串快取控制項檔案的 toobe 當其包含查詢字串快取的方式。"
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
ms.openlocfilehash: 5c97cf0230ae13fd378bfce49481f3135a5ef101
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="control-azure-cdn-caching-behavior-with-query-strings---premium"></a><span data-ttu-id="fb2a3-103">使用查詢字串控制 Azure CDN 快取行為 - Premium</span><span class="sxs-lookup"><span data-stu-id="fb2a3-103">Control Azure CDN caching behavior with query strings - Premium</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="fb2a3-104">標準</span><span class="sxs-lookup"><span data-stu-id="fb2a3-104">Standard</span></span>](cdn-query-string.md)
> * [<span data-ttu-id="fb2a3-105">來自 Verizon 的 Azure CDN 進階</span><span class="sxs-lookup"><span data-stu-id="fb2a3-105">Azure CDN Premium from Verizon</span></span>](cdn-query-string-premium.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="fb2a3-106">概觀</span><span class="sxs-lookup"><span data-stu-id="fb2a3-106">Overview</span></span>
<span data-ttu-id="fb2a3-107">查詢字串快取檔案的方式 toobe 當其包含查詢字串快取的控制項。</span><span class="sxs-lookup"><span data-stu-id="fb2a3-107">Query string caching controls how files are toobe cached when they contain query strings.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fb2a3-108">hello Standard 和 Premium CDN 產品提供 hello 同樣的查詢字串快取功能，但 hello 使用者介面會不同。</span><span class="sxs-lookup"><span data-stu-id="fb2a3-108">hello Standard and Premium CDN products provide hello same query string caching functionality, but hello user interface differs.</span></span>  <span data-ttu-id="fb2a3-109">本文件說明 hello 介面**Verizon 從 Azure CDN Premium**。</span><span class="sxs-lookup"><span data-stu-id="fb2a3-109">This document describes hello interface for **Azure CDN Premium from Verizon**.</span></span>  <span data-ttu-id="fb2a3-110">如需利用**來自 Akamai 的 Azure CDN 標準**和**來自 Verizon 的 Azure CDN 標準**查詢字串快取，請參閱[利用查詢字串控制 CDN 要求的快取行為](cdn-query-string.md)。</span><span class="sxs-lookup"><span data-stu-id="fb2a3-110">For query string caching with **Azure CDN Standard from Akamai** and **Azure CDN Standard from Verizon**, see [Controlling caching behavior of CDN requests with query strings](cdn-query-string.md).</span></span>
> 
> 

<span data-ttu-id="fb2a3-111">提供三種可用模式：</span><span class="sxs-lookup"><span data-stu-id="fb2a3-111">Three modes are available:</span></span>

* <span data-ttu-id="fb2a3-112">**標準快取**： 這是 hello 預設模式。</span><span class="sxs-lookup"><span data-stu-id="fb2a3-112">**standard-cache**:  This is hello default mode.</span></span>  <span data-ttu-id="fb2a3-113">hello CDN 邊緣節點將會從傳遞至 hello 查詢字串 hello 要求者 toohello 原點上 hello 第一個要求和快取 hello 資產。</span><span class="sxs-lookup"><span data-stu-id="fb2a3-113">hello CDN edge node will pass hello query string from hello requestor toohello origin on hello first request and cache hello asset.</span></span>  <span data-ttu-id="fb2a3-114">Hello 快取的資產到期之前，所有後續要求資產所服務的 hello 邊緣節點將會忽略 hello 查詢字串。</span><span class="sxs-lookup"><span data-stu-id="fb2a3-114">All subsequent requests for that asset that are served from hello edge node will ignore hello query string until hello cached asset expires.</span></span>
* <span data-ttu-id="fb2a3-115">**無快取**： 在此模式中，查詢字串的要求不會快取在 hello CDN 邊緣節點。</span><span class="sxs-lookup"><span data-stu-id="fb2a3-115">**no-cache**:  In this mode, requests with query strings are not cached at hello CDN edge node.</span></span>  <span data-ttu-id="fb2a3-116">hello 邊緣節點會直接從 hello 原點擷取 hello 資產，並將其傳遞 toohello 隨著每項要求的要求者。</span><span class="sxs-lookup"><span data-stu-id="fb2a3-116">hello edge node retrieves hello asset directly from hello origin and passes it toohello requestor with each request.</span></span>
* <span data-ttu-id="fb2a3-117">**唯一快取**：此模式會將包含查詢字串的每個要求視為具有專屬快取的唯一資產。</span><span class="sxs-lookup"><span data-stu-id="fb2a3-117">**unique-cache**:  This mode treats each request with a query string as a unique asset with its own cache.</span></span>  <span data-ttu-id="fb2a3-118">例如，hello 回應 hello 原點的要求*foo.ashx?q=bar*會在 hello 邊緣節點快取，後續的快取，以該相同的查詢字串傳回。</span><span class="sxs-lookup"><span data-stu-id="fb2a3-118">For example, hello response from hello origin for a request for *foo.ashx?q=bar* would be cached at hello edge node and returned for subsequent caches with that same query string.</span></span>  <span data-ttu-id="fb2a3-119">要求*foo.ashx?q=somethingelse*做為個別的資產 toolive 自己時間就會快取。</span><span class="sxs-lookup"><span data-stu-id="fb2a3-119">A request for *foo.ashx?q=somethingelse* would be cached as a separate asset with its own time toolive.</span></span>

## <a name="changing-query-string-caching-settings-for-premium-cdn-profiles"></a><span data-ttu-id="fb2a3-120">變更進階 CDN 設定檔的查詢字串快取設定</span><span class="sxs-lookup"><span data-stu-id="fb2a3-120">Changing query string caching settings for premium CDN profiles</span></span>
1. <span data-ttu-id="fb2a3-121">從 hello CDN 設定檔刀鋒視窗中，按一下 [hello**管理**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="fb2a3-121">From hello CDN profile blade, click hello **Manage** button.</span></span>
   
    ![[CDN 設定檔] 刀鋒視窗的 [管理] 按鈕](./media/cdn-query-string-premium/cdn-manage-btn.png)
   
    <span data-ttu-id="fb2a3-123">hello CDN 管理入口網站隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="fb2a3-123">hello CDN management portal opens.</span></span>
2. <span data-ttu-id="fb2a3-124">暫留在 hello **HTTP 大型** 索引標籤，然後暫留在 hello**快取設定**彈出式視窗。</span><span class="sxs-lookup"><span data-stu-id="fb2a3-124">Hover over hello **HTTP Large** tab, then hover over hello **Cache Settings** flyout.</span></span>  <span data-ttu-id="fb2a3-125">按一下 [ **查詢字串快取**]。</span><span class="sxs-lookup"><span data-stu-id="fb2a3-125">Click on **Query-String Caching**.</span></span>
   
    <span data-ttu-id="fb2a3-126">查詢字串快取選項隨即顯示。</span><span class="sxs-lookup"><span data-stu-id="fb2a3-126">Query string caching options are displayed.</span></span>
   
    ![CDN 查詢字串快取選項](./media/cdn-query-string-premium/cdn-query-string.png)
3. <span data-ttu-id="fb2a3-128">您的選取範圍之後，按一下 [hello**更新**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="fb2a3-128">After making your selection, click hello **Update** button.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fb2a3-129">當它需要花費一些時間透過 hello CDN hello 註冊 toopropagate，可能無法立即看到，hello 設定變更。</span><span class="sxs-lookup"><span data-stu-id="fb2a3-129">hello settings changes may not be immediately visible, as it takes time for hello registration toopropagate through hello CDN.</span></span>  <span data-ttu-id="fb2a3-130">若為<b>來自 Verizon 的 Azure CDN</b> 設定檔，則通常會在 90 分鐘之內完成傳播，但在某些情況下可能會更久。</span><span class="sxs-lookup"><span data-stu-id="fb2a3-130">For <b>Azure CDN from Verizon</b> profiles, propagation will usually complete within 90 minutes, but in some cases can take longer.</span></span>
> 
> 

