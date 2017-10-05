---
title: "在 Azure 媒體服務中管理 Azure CDN 快取原則 | Microsoft Docs"
description: "了解如何在 Azure 媒體服務中管理 Azure CDN 快取原則。"
services: media-services,cdn
documentationcenter: .NET
author: juliako
manager: erikre
editor: 
ms.assetid: be33aecc-6dbe-43d7-a056-10ba911e0e94
ms.service: media-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/04/2017
ms.author: juliako
ms.openlocfilehash: 0c479a58f4158bb1a72dc43432507160f65d2791
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="manage-azure-cdn-caching-policy-in-azure-media-services"></a><span data-ttu-id="79df1-103">在 Azure 媒體服務中管理 Azure CDN 快取原則</span><span class="sxs-lookup"><span data-stu-id="79df1-103">Manage Azure CDN caching policy in Azure Media Services</span></span>
<span data-ttu-id="79df1-104">Azure 媒體服務提供 HTTP 式「彈性資料流」和漸進式下載功能。</span><span class="sxs-lookup"><span data-stu-id="79df1-104">Azure Media Services provides HTTP based Adaptive Streaming and progressive download.</span></span> <span data-ttu-id="79df1-105">HTTP 式資料流具有快取 Proxy 和 CDN 層，以及快取用戶端的優點，所以延展性極佳。</span><span class="sxs-lookup"><span data-stu-id="79df1-105">HTTP based streaming is highly scalable with benefits of caching in proxy and CDN layers as well as client side caching.</span></span> <span data-ttu-id="79df1-106">資料流端點提供一般串流功能，以及 HTTP 快取標頭的組態。</span><span class="sxs-lookup"><span data-stu-id="79df1-106">Streaming endpoints provides general streaming capabilities and also configuration for HTTP cache headers.</span></span> <span data-ttu-id="79df1-107">串流端點會設定 HTTP Cache-Control: max-age 和 Expires 標頭。</span><span class="sxs-lookup"><span data-stu-id="79df1-107">Streaming endpoints sets HTTP Cache-Control: max-age and Expires headers.</span></span> <span data-ttu-id="79df1-108">您可以從 [W3.org](http://www.w3.org/Protocols/rfc2616/rfc2616-sec13.html)(英文) 取得 HTTP 快取標頭的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="79df1-108">You can get more information for HTTP cache headers from [W3.org](http://www.w3.org/Protocols/rfc2616/rfc2616-sec13.html).</span></span>

## <a name="default-caching-headers"></a><span data-ttu-id="79df1-109">預設快取標頭</span><span class="sxs-lookup"><span data-stu-id="79df1-109">Default Caching headers</span></span>
<span data-ttu-id="79df1-110">根據預設，資料流端點會針對隨選資料流處理的資料 (實際的媒體片段/區塊) 和資訊清單 (播放清單) 套用 3 天快取標頭。</span><span class="sxs-lookup"><span data-stu-id="79df1-110">By default streaming-endpoints apply 3 day cache headers for on-demand streaming data (actual media fragments/chunks) and manifest(playlist).</span></span> <span data-ttu-id="79df1-111">如果是即時資料流，資料流端點會針對資料 (實際的媒體片段/區塊) 套用 3 天快取標頭，針對資訊清單 (播放清單) 要求套用 2 秒快取標頭。</span><span class="sxs-lookup"><span data-stu-id="79df1-111">For live streaming, streaming endpoints apply 3 day cache headers for data (actual media fragments/chunks) and 2 seconds cache header for manifest(playlist) requests.</span></span> <span data-ttu-id="79df1-112">當即時節目會變成隨選 (即時封存) 時，便會套用隨選資料流處理快取標頭。</span><span class="sxs-lookup"><span data-stu-id="79df1-112">When live program turns to on-demand (live archive) then on-demand streaming cache headers apply.</span></span>

## <a name="azure-cdn-integration"></a><span data-ttu-id="79df1-113">Azure CDN 整合</span><span class="sxs-lookup"><span data-stu-id="79df1-113">Azure CDN integration</span></span>
<span data-ttu-id="79df1-114">Azure 媒體服務為資料流端點提供 [整合式 CDN](https://azure.microsoft.com/updates/azure-media-services-now-fully-integrated-with-azure-cdn/) 。</span><span class="sxs-lookup"><span data-stu-id="79df1-114">Azure Media Services provides [integrated CDN](https://azure.microsoft.com/updates/azure-media-services-now-fully-integrated-with-azure-cdn/) for streaming-endpoints.</span></span> <span data-ttu-id="79df1-115">Cache-control 標頭的套用方式與將資料流端點套用支援 CDN 的資料流端點的方式相同。</span><span class="sxs-lookup"><span data-stu-id="79df1-115">Cache-control headers applies in the same way as streaming endpoints to CDN enabled streaming endpoints.</span></span> <span data-ttu-id="79df1-116">Azure CDN 使用資料流端點設定的快取值，定義內部快取物件的存留期，也用此值設定傳遞快取標頭。</span><span class="sxs-lookup"><span data-stu-id="79df1-116">Azure CDN uses streaming endpoint configured cache values to define the life time of the internally cached objects and also uses this value to set the delivery cache headers.</span></span> <span data-ttu-id="79df1-117">使用支援 CDN 的資料流端點時，不建議將快取值設得太小。</span><span class="sxs-lookup"><span data-stu-id="79df1-117">When using CDN enabled streaming endpoints it is not recommended to set small cache values.</span></span> <span data-ttu-id="79df1-118">將值設得太小會降低效能，並減少 CDN 帶來的好處。</span><span class="sxs-lookup"><span data-stu-id="79df1-118">Setting small values will decrease the performance and reduce the benefit of CDN.</span></span> <span data-ttu-id="79df1-119">支援 CDN 的資料流端點的快取標頭值不得設為 600 秒以下。</span><span class="sxs-lookup"><span data-stu-id="79df1-119">It is not allowed to set cache headers smaller than 600 seconds for CDN enabled streaming endpoints.</span></span>

> [!IMPORTANT]
><span data-ttu-id="79df1-120">Azure 媒體服務可與 Azure CDN 完整整合。</span><span class="sxs-lookup"><span data-stu-id="79df1-120">Azure Media Services has complete integration with Azure CDN.</span></span> <span data-ttu-id="79df1-121">只要按一下滑鼠，就能將所有可用的 Azure CDN 整合到您的串流端點，包括 CDN 標準和進階產品。</span><span class="sxs-lookup"><span data-stu-id="79df1-121">With a single click you can integrate all the available Azure CDN providers (Akamai and Verizon) to your streaming endpoint including CDN Standard and Premium products.</span></span> <span data-ttu-id="79df1-122">如需詳細資訊，請參閱[此公告](https://azure.microsoft.com/blog/standardstreamingendpoint/) 。</span><span class="sxs-lookup"><span data-stu-id="79df1-122">For more information, see this [announcement](https://azure.microsoft.com/blog/standardstreamingendpoint/).</span></span>
> 
> <span data-ttu-id="79df1-123">只有當 CDN 是透過串流端點 API 或是 Azure 管理入口網站的串流端點區段啟用時，才會停用串流端點對 CDN的資料傳輸費用。</span><span class="sxs-lookup"><span data-stu-id="79df1-123">Data charges from streaming endpoint to CDN only gets disabled if the CDN is enabled over streaming endpoint APIs or using Azure management portal's streaming endpoint section.</span></span> <span data-ttu-id="79df1-124">手動整合或使用 CDN API (或入口網站區段) 直接建立 CDN 端點不會停用資料傳輸費用。</span><span class="sxs-lookup"><span data-stu-id="79df1-124">Manual integration or directly creating a CDN endpoint using CDN APIs or portal section will not disable the data charges.</span></span>

## <a name="configuring-cache-headers-with-azure-media-services"></a><span data-ttu-id="79df1-125">使用 Azure 媒體服務設定快取標頭</span><span class="sxs-lookup"><span data-stu-id="79df1-125">Configuring cache headers with Azure Media Services</span></span>
<span data-ttu-id="79df1-126">您可以使用 Azure 管理入口網站或 Azure 媒體服務 API，設定快取標頭的值。</span><span class="sxs-lookup"><span data-stu-id="79df1-126">You can use Azure Management portal or Azure Media Services APIs to configure cache header values.</span></span>

1. <span data-ttu-id="79df1-127">若要透過管理入口網站設定快取標頭，請參閱＜ [如何管理資料流端點](../media-services/media-services-portal-manage-streaming-endpoints.md) ＞ (How to Manage Streaming Endpoints) 一節中的「設定資料流端點」中的。</span><span class="sxs-lookup"><span data-stu-id="79df1-127">To configure cache headers using management portal please refer to [How to Manage Streaming Endpoints](../media-services/media-services-portal-manage-streaming-endpoints.md) section Configuring the Streaming Endpoint.</span></span>
2. <span data-ttu-id="79df1-128">Azure 媒體服務 REST API， [StreamingEndpoint](https://msdn.microsoft.com/library/azure/dn783468.aspx#StreamingEndpointCacheControl)。</span><span class="sxs-lookup"><span data-stu-id="79df1-128">Azure Media Services REST API, [StreamingEndpoint](https://msdn.microsoft.com/library/azure/dn783468.aspx#StreamingEndpointCacheControl).</span></span>
3. <span data-ttu-id="79df1-129">Azure 媒體服務 .NET SDK， [StreamingEndpointCacheControl 屬性](http://go.microsoft.com/fwlink/?LinkId=615302)。</span><span class="sxs-lookup"><span data-stu-id="79df1-129">Azure Media Services .NET SDK, [StreamingEndpointCacheControl Properties](http://go.microsoft.com/fwlink/?LinkId=615302).</span></span>

## <a name="cache-configuration-precedence-order"></a><span data-ttu-id="79df1-130">快取組態的優先順序</span><span class="sxs-lookup"><span data-stu-id="79df1-130">Cache configuration precedence order</span></span>
1. <span data-ttu-id="79df1-131">Azure 媒體服務的已設定快取值會覆寫預設值。</span><span class="sxs-lookup"><span data-stu-id="79df1-131">Azure Media Services configured cache value overrides default value.</span></span>
2. <span data-ttu-id="79df1-132">如果沒有任何手動組態，系統會套用預設值。</span><span class="sxs-lookup"><span data-stu-id="79df1-132">If there is no manual configuration, default values applies.</span></span>
3. <span data-ttu-id="79df1-133">根據預設，2 秒快取標頭會套用至即時資料流資訊清單 (播放清單)，無論 Azure 媒體或 Azure 儲存體組態為何，且此值無法被覆寫。</span><span class="sxs-lookup"><span data-stu-id="79df1-133">By default 2 seconds cache headers applies to live streaming manifest(playlist) regardless of Azure Media or Azure Storage configuration and overriding of this value is not available.</span></span>

