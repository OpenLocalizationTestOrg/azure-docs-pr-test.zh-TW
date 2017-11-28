---
title: "使用查詢字串的 Azure CDN 快取行為 aaaControl |Microsoft 文件"
description: "Azure CDN 查詢字串快取控制項檔案的 toobe 當其包含查詢字串快取的方式。"
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
ms.openlocfilehash: e7a138b2decec624a29eb703ad9a291d19c44ee8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="control-azure-cdn-caching-behavior-with-query-strings"></a><span data-ttu-id="04d72-103">使用查詢字串控制 Azure CDN 快取行為</span><span class="sxs-lookup"><span data-stu-id="04d72-103">Control Azure CDN caching behavior with query strings</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="04d72-104">標準</span><span class="sxs-lookup"><span data-stu-id="04d72-104">Standard</span></span>](cdn-query-string.md)
> * [<span data-ttu-id="04d72-105">來自 Verizon 的 Azure CDN 進階</span><span class="sxs-lookup"><span data-stu-id="04d72-105">Azure CDN Premium from Verizon</span></span>](cdn-query-string-premium.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="04d72-106">概觀</span><span class="sxs-lookup"><span data-stu-id="04d72-106">Overview</span></span>
<span data-ttu-id="04d72-107">查詢字串快取檔案的方式 toobe 當其包含查詢字串快取的控制項。</span><span class="sxs-lookup"><span data-stu-id="04d72-107">Query string caching controls how files are toobe cached when they contain query strings.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="04d72-108">hello Standard 和 Premium CDN 產品提供 hello 同樣的查詢字串快取功能，但 hello 使用者介面會不同。</span><span class="sxs-lookup"><span data-stu-id="04d72-108">hello Standard and Premium CDN products provide hello same query string caching functionality, but hello user interface differs.</span></span>  <span data-ttu-id="04d72-109">本文件說明 hello 介面**Azure 標準 Akamai CDN**和**Azure CDN 標準從 Verizon**。</span><span class="sxs-lookup"><span data-stu-id="04d72-109">This document describes hello interface for **Azure CDN Standard from Akamai** and **Azure CDN Standard from Verizon**.</span></span>  <span data-ttu-id="04d72-110">如需利用 **來自 Verizon 的 Azure CDN 進階**查詢字串快取，請參閱 [利用查詢字串控制 CDN 要求的快取行為 - 進階](cdn-query-string-premium.md)。</span><span class="sxs-lookup"><span data-stu-id="04d72-110">For query string caching with **Azure CDN Premium from Verizon**, see [Controlling caching behavior of CDN requests with query strings - Premium](cdn-query-string-premium.md).</span></span>
> 
> 

<span data-ttu-id="04d72-111">提供三種可用模式：</span><span class="sxs-lookup"><span data-stu-id="04d72-111">Three modes are available:</span></span>

* <span data-ttu-id="04d72-112">**忽略查詢字串**： 這是 hello 預設模式。</span><span class="sxs-lookup"><span data-stu-id="04d72-112">**Ignore query strings**:  This is hello default mode.</span></span>  <span data-ttu-id="04d72-113">hello CDN 邊緣節點將會從傳遞至 hello 查詢字串 hello 要求者 toohello 原點上 hello 第一個要求和快取 hello 資產。</span><span class="sxs-lookup"><span data-stu-id="04d72-113">hello CDN edge node will pass hello query string from hello requestor toohello origin on hello first request and cache hello asset.</span></span>  <span data-ttu-id="04d72-114">Hello 快取的資產到期之前，所有後續要求資產所服務的 hello 邊緣節點將會忽略 hello 查詢字串。</span><span class="sxs-lookup"><span data-stu-id="04d72-114">All subsequent requests for that asset that are served from hello edge node will ignore hello query string until hello cached asset expires.</span></span>
* <span data-ttu-id="04d72-115">**略過快取內含查詢字串 URL**： 在此模式中，查詢字串的要求不會快取在 hello CDN 邊緣節點。</span><span class="sxs-lookup"><span data-stu-id="04d72-115">**Bypass caching for URL with query strings**:  In this mode, requests with query strings are not cached at hello CDN edge node.</span></span>  <span data-ttu-id="04d72-116">hello 邊緣節點會直接從 hello 原點擷取 hello 資產，並將其傳遞 toohello 隨著每項要求的要求者。</span><span class="sxs-lookup"><span data-stu-id="04d72-116">hello edge node retrieves hello asset directly from hello origin and passes it toohello requestor with each request.</span></span>
* <span data-ttu-id="04d72-117">**快取每個唯一 URL**：此模式會將包含查詢字串的每個要求視為具有專屬快取的唯一資產。</span><span class="sxs-lookup"><span data-stu-id="04d72-117">**Cache every unique URL**:  This mode treats each request with a query string as a unique asset with its own cache.</span></span>  <span data-ttu-id="04d72-118">例如，hello 回應 hello 原點的要求*foo.ashx?q=bar*會在 hello 邊緣節點快取，後續的快取，以該相同的查詢字串傳回。</span><span class="sxs-lookup"><span data-stu-id="04d72-118">For example, hello response from hello origin for a request for *foo.ashx?q=bar* would be cached at hello edge node and returned for subsequent caches with that same query string.</span></span>  <span data-ttu-id="04d72-119">要求*foo.ashx?q=somethingelse*做為個別的資產 toolive 自己時間就會快取。</span><span class="sxs-lookup"><span data-stu-id="04d72-119">A request for *foo.ashx?q=somethingelse* would be cached as a separate asset with its own time toolive.</span></span>

## <a name="changing-query-string-caching-settings-for-standard-cdn-profiles"></a><span data-ttu-id="04d72-120">變更標準 CDN 設定檔的查詢字串快取設定</span><span class="sxs-lookup"><span data-stu-id="04d72-120">Changing query string caching settings for standard CDN profiles</span></span>
1. <span data-ttu-id="04d72-121">從 hello CDN 設定檔刀鋒視窗中，按一下您想 toomanage hello CDN 端點。</span><span class="sxs-lookup"><span data-stu-id="04d72-121">From hello CDN profile blade, click hello CDN endpoint you wish toomanage.</span></span>
   
    ![[CDN 設定檔] 刀鋒視窗端點](./media/cdn-query-string/cdn-endpoints.png)
   
    <span data-ttu-id="04d72-123">hello CDN 端點刀鋒視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="04d72-123">hello CDN endpoint blade opens.</span></span>
2. <span data-ttu-id="04d72-124">按一下 hello**設定** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="04d72-124">Click hello **Configure** button.</span></span>
   
    ![[CDN 設定檔] 刀鋒視窗的 [管理] 按鈕](./media/cdn-query-string/cdn-config-btn.png)
   
    <span data-ttu-id="04d72-126">hello CDN 組態刀鋒視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="04d72-126">hello CDN Configuration blade opens.</span></span>
3. <span data-ttu-id="04d72-127">選取的設定從 hello**查詢字串快取行為**下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="04d72-127">Select a setting from hello **Query string caching behavior** dropdown.</span></span>
   
    ![CDN 查詢字串快取選項](./media/cdn-query-string/cdn-query-string.png)
4. <span data-ttu-id="04d72-129">您的選取範圍之後，按一下 [hello**儲存**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="04d72-129">After making your selection, click hello **Save** button.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="04d72-130">當它需要花費一些時間透過 hello CDN hello 註冊 toopropagate，可能無法立即看到，hello 設定變更。</span><span class="sxs-lookup"><span data-stu-id="04d72-130">hello settings changes may not be immediately visible, as it takes time for hello registration toopropagate through hello CDN.</span></span>  <span data-ttu-id="04d72-131">在 [通訊協定] <b>來自 Akamai 的 Azure CDN</b> 設定檔，通常會在一分鐘之內完成傳播。</span><span class="sxs-lookup"><span data-stu-id="04d72-131">For <b>Azure CDN from Akamai</b> profiles, propagation will usually complete within one minute.</span></span>  <span data-ttu-id="04d72-132">若為<b>來自 Verizon 的 Azure CDN</b> 設定檔，則通常會在 90 分鐘之內完成傳播，但在某些情況下可能會更久。</span><span class="sxs-lookup"><span data-stu-id="04d72-132">For <b>Azure CDN from Verizon</b> profiles, propagation will usually complete within 90 minutes, but in some cases can take longer.</span></span>
> 
> 

