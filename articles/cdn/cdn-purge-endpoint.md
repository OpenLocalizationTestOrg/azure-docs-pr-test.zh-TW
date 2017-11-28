---
title: "aaaPurge Azure CDN 端點 |Microsoft 文件"
description: "了解如何 toopurge 所有快取來自 Azure CDN 端點的內容。"
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 0b50230b-fe82-4740-90aa-95d4dde8bd4f
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: a09f4a49aa1e2d7655ecae44b5126c11c28fd599
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="purge-an-azure-cdn-endpoint"></a><span data-ttu-id="37171-103">清除 Azure CDN 端點</span><span class="sxs-lookup"><span data-stu-id="37171-103">Purge an Azure CDN endpoint</span></span>
## <a name="overview"></a><span data-ttu-id="37171-104">概觀</span><span class="sxs-lookup"><span data-stu-id="37171-104">Overview</span></span>
<span data-ttu-id="37171-105">Azure CDN 邊緣節點會快取資產，直到過期 hello 資產的存留時間 (TTL)。</span><span class="sxs-lookup"><span data-stu-id="37171-105">Azure CDN edge nodes will cache assets until hello asset's time-to-live (TTL) expires.</span></span>  <span data-ttu-id="37171-106">Hello 資產的 TTL 到期，用戶端要求來自 hello 邊緣節點的 hello 資產之後，會擷取已更新的全新的 hello 資產 tooserve hello 用戶端要求 hello 邊緣節點，並將其重新整理 hello 快取儲存。</span><span class="sxs-lookup"><span data-stu-id="37171-106">After hello asset's TTL expires, when a client requests hello asset from hello edge node, hello edge node will retrieve a new updated copy of hello asset tooserve hello client request and store refresh hello cache.</span></span>

<span data-ttu-id="37171-107">hello 最佳作法 toomake 確定您的使用者永遠取得 hello 您資產的最新的複本是的 tooversion 更新每個資產，並將其發行為新的 Url。</span><span class="sxs-lookup"><span data-stu-id="37171-107">hello best practice toomake sure your users always obtain hello latest copy of your assets is tooversion your assets for each update and publish them as new URLs.</span></span>  <span data-ttu-id="37171-108">CDN 將會立即擷取 hello hello 下一個用戶端要求新的資產。</span><span class="sxs-lookup"><span data-stu-id="37171-108">CDN will immediately retrieve hello new assets for hello next client requests.</span></span>  <span data-ttu-id="37171-109">有時候您可能希望 toopurge 快取來自所有邊緣節點的內容，強制其所有 tooretrieve 新更新的資產。</span><span class="sxs-lookup"><span data-stu-id="37171-109">Sometimes you may wish toopurge cached content from all edge nodes and force them all tooretrieve new updated assets.</span></span>  <span data-ttu-id="37171-110">這可能是由於 tooupdates tooyour web 應用程式或包含不正確的資訊的 tooquickly 更新資產。</span><span class="sxs-lookup"><span data-stu-id="37171-110">This might be due tooupdates tooyour web application, or tooquickly update assets that contain incorrect information.</span></span>

> [!TIP]
> <span data-ttu-id="37171-111">請注意，只清除清除 hello 快取 hello CDN 邊緣伺服器的內容。</span><span class="sxs-lookup"><span data-stu-id="37171-111">Note that purging only clears hello cached content on hello CDN edge servers.</span></span>  <span data-ttu-id="37171-112">任何下游快取 proxy 伺服器和本機瀏覽器快取中，例如可能仍會保留 hello 檔案的快取的副本。</span><span class="sxs-lookup"><span data-stu-id="37171-112">Any downstream caches, such as proxy servers and local browser caches, may still hold a cached copy of hello file.</span></span>  <span data-ttu-id="37171-113">它是重要的 tooremember 這樣當您將設定檔的存留時間。</span><span class="sxs-lookup"><span data-stu-id="37171-113">It's important tooremember this when you set a file's time-to-live.</span></span>  <span data-ttu-id="37171-114">您可以強制下游的用戶端 toorequest hello 最新版本的檔案，為它指定唯一的名稱，每次您更新，或藉由運用[查詢字串快取](cdn-query-string.md)。</span><span class="sxs-lookup"><span data-stu-id="37171-114">You can force a downstream client toorequest hello latest version of your file by giving it a unique name every time you update it, or by taking advantage of [query string caching](cdn-query-string.md).</span></span>  
> 
> 

<span data-ttu-id="37171-115">本教學會逐步引導您清除端點的所有邊緣節點的資產。</span><span class="sxs-lookup"><span data-stu-id="37171-115">This tutorial walks you through purging assets from all edge nodes of an endpoint.</span></span>

## <a name="walkthrough"></a><span data-ttu-id="37171-116">逐步介紹</span><span class="sxs-lookup"><span data-stu-id="37171-116">Walkthrough</span></span>
1. <span data-ttu-id="37171-117">在 hello [Azure 入口網站](https://portal.azure.com)，瀏覽 toohello CDN 設定檔包含您想 toopurge hello 端點。</span><span class="sxs-lookup"><span data-stu-id="37171-117">In hello [Azure Portal](https://portal.azure.com), browse toohello CDN profile containing hello endpoint you wish toopurge.</span></span>
2. <span data-ttu-id="37171-118">從 hello CDN 設定檔刀鋒視窗中，按一下 hello 清除 按鈕。</span><span class="sxs-lookup"><span data-stu-id="37171-118">From hello CDN profile blade, click hello purge button.</span></span>
   
    ![CDN 設定檔刀鋒視窗](./media/cdn-purge-endpoint/cdn-profile-blade.png)
   
    <span data-ttu-id="37171-120">hello 清除刀鋒視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="37171-120">hello Purge blade opens.</span></span>
   
    ![CDN 清除刀鋒視窗](./media/cdn-purge-endpoint/cdn-purge-blade.png)
3. <span data-ttu-id="37171-122">Hello 上清除刀鋒視窗中，選取您想 toopurge 從 hello URL 下拉式清單中的 hello 服務位址。</span><span class="sxs-lookup"><span data-stu-id="37171-122">On hello Purge blade, select hello service address you wish toopurge from hello URL dropdown.</span></span>
   
    ![清除表單](./media/cdn-purge-endpoint/cdn-purge-form.png)
   
   > [!NOTE]
   > <span data-ttu-id="37171-124">您也可以取得 toohello 清除刀鋒視窗中，依序按一下 hello**清除**hello CDN 端點刀鋒視窗上的按鈕。</span><span class="sxs-lookup"><span data-stu-id="37171-124">You can also get toohello Purge blade by clicking hello **Purge** button on hello CDN endpoint blade.</span></span>  <span data-ttu-id="37171-125">在此情況下，hello **URL**欄位會預先填入該特定端點 hello 服務位址。</span><span class="sxs-lookup"><span data-stu-id="37171-125">In that case, hello **URL** field will be pre-populated with hello service address of that specific endpoint.</span></span>
   > 
   > 
4. <span data-ttu-id="37171-126">選取的資產您想從 hello toopurge 邊緣節點。</span><span class="sxs-lookup"><span data-stu-id="37171-126">Select what assets you wish toopurge from hello edge nodes.</span></span>  <span data-ttu-id="37171-127">如果您想 tooclear 所有資產，按一下 hello **全部清除**核取方塊。</span><span class="sxs-lookup"><span data-stu-id="37171-127">If you wish tooclear all assets, click hello **Purge all** checkbox.</span></span>  <span data-ttu-id="37171-128">否則，每個資產的型別 hello 路徑想 toopurge 在 hello**路徑**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="37171-128">Otherwise, type hello path of each asset you wish toopurge in hello **Path** textbox.</span></span> <span data-ttu-id="37171-129">下面格式支援 hello 路徑中。</span><span class="sxs-lookup"><span data-stu-id="37171-129">Below formats are supported in hello path.</span></span>
    1. <span data-ttu-id="37171-130">**單一 URL 清除**: hello 副檔名，例如，含指定 hello 完整的 URL，來清除個別資產`/pictures/strasbourg.png`;`/pictures/strasbourg`</span><span class="sxs-lookup"><span data-stu-id="37171-130">**Single URL purge**: Purge individual asset by specifying hello full URL, with or without hello file extension, e.g.,`/pictures/strasbourg.png`; `/pictures/strasbourg`</span></span>
    2. <span data-ttu-id="37171-131">**萬用字元清除**︰星號 (\*) 可作為萬用字元。</span><span class="sxs-lookup"><span data-stu-id="37171-131">**Wildcard purge**: Asterisk (\*) may be used as a wildcard.</span></span> <span data-ttu-id="37171-132">清除所有資料夾、 子資料夾和檔案底下的端點`/*`hello 路徑或都清除所有的子資料夾和特定資料夾下的檔案，藉由指定後面的 hello 資料夾`/*`，例如，`/pictures/*`。</span><span class="sxs-lookup"><span data-stu-id="37171-132">Purge all folders, sub-folders and files under an endpoint with `/*` in hello path or purge all sub-folders and files under a specific folder by specifying hello folder followed by `/*`, e.g.,`/pictures/*`.</span></span>  <span data-ttu-id="37171-133">請注意，來自 Akamai 的 Azure CDN 目前不支援萬用字元清除。</span><span class="sxs-lookup"><span data-stu-id="37171-133">Note that wildcard purge is not supported by Azure CDN from Akamai currently.</span></span> 
    3. <span data-ttu-id="37171-134">**根網域清除**: hello 端點以"/"hello 路徑中的清除 hello 根。</span><span class="sxs-lookup"><span data-stu-id="37171-134">**Root domain purge**: Purge hello root of hello endpoint with "/" in hello path.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="37171-135">路徑必須指定清除，而且必須是相對的 URL 納入 hello 下列[規則運算式](https://msdn.microsoft.com/library/az24scfc.aspx)。</span><span class="sxs-lookup"><span data-stu-id="37171-135">Paths must be specified for purge and must be a relative URL that fit hello following [regular expression](https://msdn.microsoft.com/library/az24scfc.aspx).</span></span> <span data-ttu-id="37171-136">**來自 Akamai 的 Azure CDN** 目前不支援**全部清除**和**萬用字元清除**。</span><span class="sxs-lookup"><span data-stu-id="37171-136">**Purge all** and **Wildcard purge** not supported by **Azure CDN from Akamai** currently.</span></span>
   > > <span data-ttu-id="37171-137">單一 URL 清除 `@"^\/(?>(?:[a-zA-Z0-9-_.%=\(\)\u0020]+\/?)*)$";`</span><span class="sxs-lookup"><span data-stu-id="37171-137">Single URL purge `@"^\/(?>(?:[a-zA-Z0-9-_.%=\(\)\u0020]+\/?)*)$";`</span></span>  
   > > <span data-ttu-id="37171-138">查詢字串 `@"^(?:\?[-\@_a-zA-Z0-9\/%:;=!,.\+'&\(\)\u0020]*)?$";`</span><span class="sxs-lookup"><span data-stu-id="37171-138">Query string `@"^(?:\?[-\@_a-zA-Z0-9\/%:;=!,.\+'&\(\)\u0020]*)?$";`</span></span>  
   > > <span data-ttu-id="37171-139">萬用字元清除 `@"^\/(?:[a-zA-Z0-9-_.%=\(\)\u0020]+\/)*\*$";`。</span><span class="sxs-lookup"><span data-stu-id="37171-139">Wildcard purge `@"^\/(?:[a-zA-Z0-9-_.%=\(\)\u0020]+\/)*\*$";`.</span></span> 
   > 
   > <span data-ttu-id="37171-140">多個**路徑**文字方塊會出現在輸入文字 tooallow 之後 toobuild 多個資產的清單。</span><span class="sxs-lookup"><span data-stu-id="37171-140">More **Path** textboxes will appear after you enter text tooallow you toobuild a list of multiple assets.</span></span>  <span data-ttu-id="37171-141">您可以在 hello 省略符號 （...） 按鈕，即可從 hello 清單刪除資產。</span><span class="sxs-lookup"><span data-stu-id="37171-141">You can delete assets from hello list by clicking hello ellipsis (...) button.</span></span>
   > 
5. <span data-ttu-id="37171-142">按一下 hello**清除** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="37171-142">Click hello **Purge** button.</span></span>
   
    ![清除按鈕](./media/cdn-purge-endpoint/cdn-purge-button.png)

> [!IMPORTANT]
> <span data-ttu-id="37171-144">清除要求需要大約 2-3 分鐘 tooprocess 與**Verizon 從 Azure CDN** （Standard 和 Premium） 和大約 7 分鐘與**Akamai 從 Azure CDN**。</span><span class="sxs-lookup"><span data-stu-id="37171-144">Purge requests take approximately 2-3 minutes tooprocess with **Azure CDN from Verizon** (Standard and Premium), and approximately 7 minutes with **Azure CDN from Akamai**.</span></span>  <span data-ttu-id="37171-145">Azure CDN 隨時都有 50 個並行清除要求的限制。</span><span class="sxs-lookup"><span data-stu-id="37171-145">Azure CDN has a limit of 50 concurrent purge requests at any given time.</span></span> 
> 
> 

## <a name="see-also"></a><span data-ttu-id="37171-146">另請參閱</span><span class="sxs-lookup"><span data-stu-id="37171-146">See also</span></span>
* [<span data-ttu-id="37171-147">在 Azure CDN 端點上預先載入資產</span><span class="sxs-lookup"><span data-stu-id="37171-147">Pre-load assets on an Azure CDN endpoint</span></span>](cdn-preload-endpoint.md)
* [<span data-ttu-id="37171-148">Azure CDN REST API 參考資料 - 清除或預先載入端點</span><span class="sxs-lookup"><span data-stu-id="37171-148">Azure CDN REST API reference - Purge or Pre-Load an Endpoint</span></span>](https://msdn.microsoft.com/library/mt634451.aspx)

