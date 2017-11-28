---
title: "Azure CDN 端點上的 aaaPre 負載資產 |Microsoft 文件"
description: "了解如何 toopre 載入快取 Azure CDN 端點上的內容。"
services: cdn
documentationcenter: 
author: smcevoy
manager: erikre
editor: 
ms.assetid: 5ea3eba5-1335-413e-9af3-3918ce608a83
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 08ac4b834f1ac8ce59d22e65fa8adea11bafcf17
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="pre-load-assets-on-an-azure-cdn-endpoint"></a><span data-ttu-id="c5565-103">在 Azure CDN 端點上預先載入資產</span><span class="sxs-lookup"><span data-stu-id="c5565-103">Pre-load assets on an Azure CDN endpoint</span></span>
[!INCLUDE [cdn-verizon-only](../../includes/cdn-verizon-only.md)]

<span data-ttu-id="c5565-104">根據預設，資產被要求時會先快取。</span><span class="sxs-lookup"><span data-stu-id="c5565-104">By default, assets are first cached as they are requested.</span></span> <span data-ttu-id="c5565-105">這表示 hello 從每個區域的第一個要求可能需要較長，因為不會有 hello 邊緣伺服器 hello 內容快取，而且必須 tooforward hello 要求 toohello 原始伺服器。</span><span class="sxs-lookup"><span data-stu-id="c5565-105">This means that hello first request from each region may take longer, since hello edge servers will not have hello content cached and will need tooforward hello request toohello origin server.</span></span> <span data-ttu-id="c5565-106">預先載入內容以避免此第一次點擊的延遲。</span><span class="sxs-lookup"><span data-stu-id="c5565-106">Pre-loading content avoids this first hit latency.</span></span>

<span data-ttu-id="c5565-107">此外 tooproviding 較佳的客戶體驗，預先載入快取的資產也可降低 hello 原始伺服器上的網路流量。</span><span class="sxs-lookup"><span data-stu-id="c5565-107">In addition tooproviding a better customer experience, pre-loading your cached assets can also reduce network traffic on hello origin server.</span></span>

> [!NOTE]
> <span data-ttu-id="c5565-108">預先載入資產是適用於大量的事件，或成為同時可用 tooa 大量的使用者，例如新的影片版本或在軟體更新的內容。</span><span class="sxs-lookup"><span data-stu-id="c5565-108">Pre-loading assets is useful for  large events or content that becomes simultaneously available tooa large number of users, such as a new movie release or a software update.</span></span>
> 
> 

<span data-ttu-id="c5565-109">本教學課程將逐步引導您在 Azure CDN 邊緣節點上預先載入快取的所有內容。</span><span class="sxs-lookup"><span data-stu-id="c5565-109">This tutorial walks you through pre-loading cached content on all Azure CDN edge nodes.</span></span>

## <a name="walkthrough"></a><span data-ttu-id="c5565-110">逐步介紹</span><span class="sxs-lookup"><span data-stu-id="c5565-110">Walkthrough</span></span>
1. <span data-ttu-id="c5565-111">在 hello [Azure 入口網站](https://portal.azure.com)，瀏覽 toohello CDN 設定檔包含您想 toopre 負載 hello 端點。</span><span class="sxs-lookup"><span data-stu-id="c5565-111">In hello [Azure Portal](https://portal.azure.com), browse toohello CDN profile containing hello endpoint you wish toopre-load.</span></span>  <span data-ttu-id="c5565-112">hello 設定檔 刀鋒視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="c5565-112">hello profile blade opens.</span></span>
2. <span data-ttu-id="c5565-113">按一下 [hello] 清單中的 hello 端點。</span><span class="sxs-lookup"><span data-stu-id="c5565-113">Click hello endpoint in hello list.</span></span>  <span data-ttu-id="c5565-114">hello 端點刀鋒視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="c5565-114">hello endpoint blade opens.</span></span>
3. <span data-ttu-id="c5565-115">從 hello CDN 端點刀鋒視窗中，按一下 hello 載入 按鈕。</span><span class="sxs-lookup"><span data-stu-id="c5565-115">From hello CDN endpoint blade, click hello load button.</span></span>
   
    ![CDN 端點刀鋒視窗](./media/cdn-preload-endpoint/cdn-endpoint-blade.png)
   
    <span data-ttu-id="c5565-117">hello 負載刀鋒視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="c5565-117">hello Load blade opens.</span></span>
   
    ![CDN 載入刀鋒視窗](./media/cdn-preload-endpoint/cdn-load-blade.png)
4. <span data-ttu-id="c5565-119">輸入 hello 完整路徑的每個資產，您想 tooload (例如`/pictures/kitten.png`) 在 hello**路徑**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="c5565-119">Enter hello full path of each asset you wish tooload (e.g., `/pictures/kitten.png`) in hello **Path** textbox.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="c5565-120">多個**路徑**文字方塊會出現在輸入文字 tooallow 之後 toobuild 多個資產的清單。</span><span class="sxs-lookup"><span data-stu-id="c5565-120">More **Path** textboxes will appear after you enter text tooallow you toobuild a list of multiple assets.</span></span>  <span data-ttu-id="c5565-121">您可以在 hello 省略符號 （...） 按鈕，即可從 hello 清單刪除資產。</span><span class="sxs-lookup"><span data-stu-id="c5565-121">You can delete assets from hello list by clicking hello ellipsis (...) button.</span></span>
   > 
   > <span data-ttu-id="c5565-122">路徑必須符合下列 hello 相對 URL[規則運算式](https://msdn.microsoft.com/library/az24scfc.aspx):</span><span class="sxs-lookup"><span data-stu-id="c5565-122">Paths must be a relative URL that fits hello following [regular expression](https://msdn.microsoft.com/library/az24scfc.aspx):</span></span>  
   > ><span data-ttu-id="c5565-123">載入單一檔案路徑 `@"^(?:\/[a-zA-Z0-9-_.%=\u0020]+)+$"`；</span><span class="sxs-lookup"><span data-stu-id="c5565-123">Load a single file path `@"^(?:\/[a-zA-Z0-9-_.%=\u0020]+)+$"`;</span></span>  
   > ><span data-ttu-id="c5565-124">以查詢字串載入單一檔案 `@"^(?:\?[-_a-zA-Z0-9\/%:;=!,.\+'&\u0020]*)?$";`</span><span class="sxs-lookup"><span data-stu-id="c5565-124">Load a single file with query string `@"^(?:\?[-_a-zA-Z0-9\/%:;=!,.\+'&\u0020]*)?$";`</span></span>  
   > 
   > <span data-ttu-id="c5565-125">每個資產都必須有自己的路徑。</span><span class="sxs-lookup"><span data-stu-id="c5565-125">Each asset must have its own path.</span></span>  <span data-ttu-id="c5565-126">預先載入資產沒有萬用字元功能。</span><span class="sxs-lookup"><span data-stu-id="c5565-126">There is no wildcard functionality for pre-loading assets.</span></span>
   > 
   > 
   
    ![載入按鈕](./media/cdn-preload-endpoint/cdn-load-paths.png)
5. <span data-ttu-id="c5565-128">按一下 hello**負載** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="c5565-128">Click hello **Load** button.</span></span>
   
    ![載入按鈕](./media/cdn-preload-endpoint/cdn-load-button.png)

> [!NOTE]
> <span data-ttu-id="c5565-130">每個 CDN 設定檔都有每分鐘 10 個載入要求的限制。</span><span class="sxs-lookup"><span data-stu-id="c5565-130">There is a limitation of 10 load requests per minute per CDN profile.</span></span> <span data-ttu-id="c5565-131">每個要求允許 50 個路徑。</span><span class="sxs-lookup"><span data-stu-id="c5565-131">50 paths are allowed per request.</span></span> <span data-ttu-id="c5565-132">每個路徑都有 1024 個字元的路徑長度限制。</span><span class="sxs-lookup"><span data-stu-id="c5565-132">Each path has a path-length limit of 1024 characters.</span></span>
> 
> 

## <a name="see-also"></a><span data-ttu-id="c5565-133">另請參閱</span><span class="sxs-lookup"><span data-stu-id="c5565-133">See also</span></span>
* [<span data-ttu-id="c5565-134">清除 Azure CDN 端點</span><span class="sxs-lookup"><span data-stu-id="c5565-134">Purge an Azure CDN endpoint</span></span>](cdn-purge-endpoint.md)
* [<span data-ttu-id="c5565-135">Azure CDN REST API 參考資料 - 清除或預先載入端點</span><span class="sxs-lookup"><span data-stu-id="c5565-135">Azure CDN REST API reference - Purge or Pre-Load an Endpoint</span></span>](https://msdn.microsoft.com/library/mt634451.aspx)

