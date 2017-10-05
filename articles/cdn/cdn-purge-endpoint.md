---
title: "清除 Azure CDN 端點 | Microsoft Docs"
description: "了解如何清除 Azure CDN 端點的所有快取內容。"
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
ms.openlocfilehash: b035c232bb58d653960190d4974cc3789d55a51d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="purge-an-azure-cdn-endpoint"></a><span data-ttu-id="7ed04-103">清除 Azure CDN 端點</span><span class="sxs-lookup"><span data-stu-id="7ed04-103">Purge an Azure CDN endpoint</span></span>
## <a name="overview"></a><span data-ttu-id="7ed04-104">概觀</span><span class="sxs-lookup"><span data-stu-id="7ed04-104">Overview</span></span>
<span data-ttu-id="7ed04-105">Azure CDN 邊緣節點會快取資產，直到資產的存留時間 (TTL) 到期。</span><span class="sxs-lookup"><span data-stu-id="7ed04-105">Azure CDN edge nodes will cache assets until the asset's time-to-live (TTL) expires.</span></span>  <span data-ttu-id="7ed04-106">資產的 TTL 到期之後，當用戶端從邊緣節點要求資產時，邊緣節點會建立資產新的更新的複本以服務用戶端的要求並儲存重新整理快取。</span><span class="sxs-lookup"><span data-stu-id="7ed04-106">After the asset's TTL expires, when a client requests the asset from the edge node, the edge node will retrieve a new updated copy of the asset to serve the client request and store refresh the cache.</span></span>

<span data-ttu-id="7ed04-107">若要確定使用者一律會取得最新的資產複本，最佳作法是為每個更新設定資產版本，然後將它們發佈為新的 URL。</span><span class="sxs-lookup"><span data-stu-id="7ed04-107">The best practice to make sure your users always obtain the latest copy of your assets is to version your assets for each update and publish them as new URLs.</span></span>  <span data-ttu-id="7ed04-108">CDN 會立即為下一個用戶端要求擷取新的資產。</span><span class="sxs-lookup"><span data-stu-id="7ed04-108">CDN will immediately retrieve the new assets for the next client requests.</span></span>  <span data-ttu-id="7ed04-109">有時您可能想要清除所有邊緣節點的快取內容，並強制它們全部擷取新的更新的資產。</span><span class="sxs-lookup"><span data-stu-id="7ed04-109">Sometimes you may wish to purge cached content from all edge nodes and force them all to retrieve new updated assets.</span></span>  <span data-ttu-id="7ed04-110">可能是因為您的 Web 應用程式更新，或快速更新包含不正確資訊的資產。</span><span class="sxs-lookup"><span data-stu-id="7ed04-110">This might be due to updates to your web application, or to quickly update assets that contain incorrect information.</span></span>

> [!TIP]
> <span data-ttu-id="7ed04-111">請注意，清除只會清除 CDN 邊緣伺服器上的快取內容。</span><span class="sxs-lookup"><span data-stu-id="7ed04-111">Note that purging only clears the cached content on the CDN edge servers.</span></span>  <span data-ttu-id="7ed04-112">任何下游快取，例如 proxy 伺服器和本機瀏覽器快取，仍然可能含有檔案的快取複本。</span><span class="sxs-lookup"><span data-stu-id="7ed04-112">Any downstream caches, such as proxy servers and local browser caches, may still hold a cached copy of the file.</span></span>  <span data-ttu-id="7ed04-113">當您設定檔案的存留時間時，請務必記住這一點。</span><span class="sxs-lookup"><span data-stu-id="7ed04-113">It's important to remember this when you set a file's time-to-live.</span></span>  <span data-ttu-id="7ed04-114">您可以強制下游用戶端要求最新版本的檔案，方法是每次更新下游用戶端時提供唯一名稱給它，或是運用 [查詢字串快取](cdn-query-string.md)。</span><span class="sxs-lookup"><span data-stu-id="7ed04-114">You can force a downstream client to request the latest version of your file by giving it a unique name every time you update it, or by taking advantage of [query string caching](cdn-query-string.md).</span></span>  
> 
> 

<span data-ttu-id="7ed04-115">本教學會逐步引導您清除端點的所有邊緣節點的資產。</span><span class="sxs-lookup"><span data-stu-id="7ed04-115">This tutorial walks you through purging assets from all edge nodes of an endpoint.</span></span>

## <a name="walkthrough"></a><span data-ttu-id="7ed04-116">逐步介紹</span><span class="sxs-lookup"><span data-stu-id="7ed04-116">Walkthrough</span></span>
1. <span data-ttu-id="7ed04-117">在 [Azure 入口網站](https://portal.azure.com)中，瀏覽到包含您希望清除之端點的 CDN 設定檔。</span><span class="sxs-lookup"><span data-stu-id="7ed04-117">In the [Azure Portal](https://portal.azure.com), browse to the CDN profile containing the endpoint you wish to purge.</span></span>
2. <span data-ttu-id="7ed04-118">在 [CDN 設定檔] 刀鋒視窗中，按一下 [清除] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="7ed04-118">From the CDN profile blade, click the purge button.</span></span>
   
    ![CDN 設定檔刀鋒視窗](./media/cdn-purge-endpoint/cdn-profile-blade.png)
   
    <span data-ttu-id="7ed04-120">會開啟 [清除] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="7ed04-120">The Purge blade opens.</span></span>
   
    ![CDN 清除刀鋒視窗](./media/cdn-purge-endpoint/cdn-purge-blade.png)
3. <span data-ttu-id="7ed04-122">在 [清除] 刀鋒視窗中，從 [URL] 下拉式清單中選取希望清除的服務位址。</span><span class="sxs-lookup"><span data-stu-id="7ed04-122">On the Purge blade, select the service address you wish to purge from the URL dropdown.</span></span>
   
    ![清除表單](./media/cdn-purge-endpoint/cdn-purge-form.png)
   
   > [!NOTE]
   > <span data-ttu-id="7ed04-124">您也可以按一下 [CDN 端點] 刀鋒視窗中的 [清除] 按鈕，來開啟 [清除] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="7ed04-124">You can also get to the Purge blade by clicking the **Purge** button on the CDN endpoint blade.</span></span>  <span data-ttu-id="7ed04-125">在此情況下，[URL]  欄位會預先填入該特定端點的服務位址。</span><span class="sxs-lookup"><span data-stu-id="7ed04-125">In that case, the **URL** field will be pre-populated with the service address of that specific endpoint.</span></span>
   > 
   > 
4. <span data-ttu-id="7ed04-126">選取您希望從邊緣節點清除的資產。</span><span class="sxs-lookup"><span data-stu-id="7ed04-126">Select what assets you wish to purge from the edge nodes.</span></span>  <span data-ttu-id="7ed04-127">如果您希望清除所有資產，請按一下 [清除]  核取方塊。</span><span class="sxs-lookup"><span data-stu-id="7ed04-127">If you wish to clear all assets, click the **Purge all** checkbox.</span></span>  <span data-ttu-id="7ed04-128">或者，在 [路徑] 文字方塊中輸入每個您想要清除之資產的路徑。</span><span class="sxs-lookup"><span data-stu-id="7ed04-128">Otherwise, type the path of each asset you wish to purge in the **Path** textbox.</span></span> <span data-ttu-id="7ed04-129">路徑支援下列格式。</span><span class="sxs-lookup"><span data-stu-id="7ed04-129">Below formats are supported in the path.</span></span>
    1. <span data-ttu-id="7ed04-130">**單一 URL 清除**︰藉由指定完整 URL (含或不含副檔名) 來清除個別資產，例如 `/pictures/strasbourg.png`、`/pictures/strasbourg`</span><span class="sxs-lookup"><span data-stu-id="7ed04-130">**Single URL purge**: Purge individual asset by specifying the full URL, with or without the file extension, e.g.,`/pictures/strasbourg.png`; `/pictures/strasbourg`</span></span>
    2. <span data-ttu-id="7ed04-131">**萬用字元清除**︰星號 (\*) 可作為萬用字元。</span><span class="sxs-lookup"><span data-stu-id="7ed04-131">**Wildcard purge**: Asterisk (\*) may be used as a wildcard.</span></span> <span data-ttu-id="7ed04-132">清除路徑中有 `/*` 之端點下的所有資料夾、子資料夾和檔案，或指定後接 `/*` 的資料夾來清除特定資料夾下的所有子資料夾和檔案，例如 `/pictures/*`。</span><span class="sxs-lookup"><span data-stu-id="7ed04-132">Purge all folders, sub-folders and files under an endpoint with `/*` in the path or purge all sub-folders and files under a specific folder by specifying the folder followed by `/*`, e.g.,`/pictures/*`.</span></span>  <span data-ttu-id="7ed04-133">請注意，來自 Akamai 的 Azure CDN 目前不支援萬用字元清除。</span><span class="sxs-lookup"><span data-stu-id="7ed04-133">Note that wildcard purge is not supported by Azure CDN from Akamai currently.</span></span> 
    3. <span data-ttu-id="7ed04-134">**根網域清除**︰清除路徑中有 "/" 之端點的根目錄。</span><span class="sxs-lookup"><span data-stu-id="7ed04-134">**Root domain purge**: Purge the root of the endpoint with "/" in the path.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="7ed04-135">路徑必須加以指定才能清除，且必須是符合下列[規則運算式](https://msdn.microsoft.com/library/az24scfc.aspx)的相對 URL。</span><span class="sxs-lookup"><span data-stu-id="7ed04-135">Paths must be specified for purge and must be a relative URL that fit the following [regular expression](https://msdn.microsoft.com/library/az24scfc.aspx).</span></span> <span data-ttu-id="7ed04-136">**來自 Akamai 的 Azure CDN** 目前不支援**全部清除**和**萬用字元清除**。</span><span class="sxs-lookup"><span data-stu-id="7ed04-136">**Purge all** and **Wildcard purge** not supported by **Azure CDN from Akamai** currently.</span></span>
   > > <span data-ttu-id="7ed04-137">單一 URL 清除 `@"^\/(?>(?:[a-zA-Z0-9-_.%=\(\)\u0020]+\/?)*)$";`</span><span class="sxs-lookup"><span data-stu-id="7ed04-137">Single URL purge `@"^\/(?>(?:[a-zA-Z0-9-_.%=\(\)\u0020]+\/?)*)$";`</span></span>  
   > > <span data-ttu-id="7ed04-138">查詢字串 `@"^(?:\?[-\@_a-zA-Z0-9\/%:;=!,.\+'&\(\)\u0020]*)?$";`</span><span class="sxs-lookup"><span data-stu-id="7ed04-138">Query string `@"^(?:\?[-\@_a-zA-Z0-9\/%:;=!,.\+'&\(\)\u0020]*)?$";`</span></span>  
   > > <span data-ttu-id="7ed04-139">萬用字元清除 `@"^\/(?:[a-zA-Z0-9-_.%=\(\)\u0020]+\/)*\*$";`。</span><span class="sxs-lookup"><span data-stu-id="7ed04-139">Wildcard purge `@"^\/(?:[a-zA-Z0-9-_.%=\(\)\u0020]+\/)*\*$";`.</span></span> 
   > 
   > <span data-ttu-id="7ed04-140">在您輸入文字之後會出現更多 [路徑] 文字方塊，讓您能夠建立多個資產的清單。</span><span class="sxs-lookup"><span data-stu-id="7ed04-140">More **Path** textboxes will appear after you enter text to allow you to build a list of multiple assets.</span></span>  <span data-ttu-id="7ed04-141">按一下刪節號 (...) 按鈕可以將資產從清單刪除。</span><span class="sxs-lookup"><span data-stu-id="7ed04-141">You can delete assets from the list by clicking the ellipsis (...) button.</span></span>
   > 
5. <span data-ttu-id="7ed04-142">按一下 [清除]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="7ed04-142">Click the **Purge** button.</span></span>
   
    ![清除按鈕](./media/cdn-purge-endpoint/cdn-purge-button.png)

> [!IMPORTANT]
> <span data-ttu-id="7ed04-144">清除要求需要大約 2-3 分鐘來處理**來自 Verizon 的 Azure CDN** (標準和進階)，大約 7 分鐘來處理**來自 Akamai 的 Azure CDN**。</span><span class="sxs-lookup"><span data-stu-id="7ed04-144">Purge requests take approximately 2-3 minutes to process with **Azure CDN from Verizon** (Standard and Premium), and approximately 7 minutes with **Azure CDN from Akamai**.</span></span>  <span data-ttu-id="7ed04-145">Azure CDN 隨時都有 50 個並行清除要求的限制。</span><span class="sxs-lookup"><span data-stu-id="7ed04-145">Azure CDN has a limit of 50 concurrent purge requests at any given time.</span></span> 
> 
> 

## <a name="see-also"></a><span data-ttu-id="7ed04-146">另請參閱</span><span class="sxs-lookup"><span data-stu-id="7ed04-146">See also</span></span>
* [<span data-ttu-id="7ed04-147">在 Azure CDN 端點上預先載入資產</span><span class="sxs-lookup"><span data-stu-id="7ed04-147">Pre-load assets on an Azure CDN endpoint</span></span>](cdn-preload-endpoint.md)
* [<span data-ttu-id="7ed04-148">Azure CDN REST API 參考資料 - 清除或預先載入端點</span><span class="sxs-lookup"><span data-stu-id="7ed04-148">Azure CDN REST API reference - Purge or Pre-Load an Endpoint</span></span>](https://msdn.microsoft.com/library/mt634451.aspx)

