---
title: "Azure 媒體服務中的 Azure CDN 快取原則 aaaManage |Microsoft 文件"
description: "深入了解如何 toomanage Azure 媒體服務中的 Azure CDN 快取原則。"
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
ms.openlocfilehash: 4c7ee2922fcbb5727e10fbe44fc6e61b79f6917c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-cdn-caching-policy-in-azure-media-services"></a><span data-ttu-id="6abcd-103">在 Azure 媒體服務中管理 Azure CDN 快取原則</span><span class="sxs-lookup"><span data-stu-id="6abcd-103">Manage Azure CDN caching policy in Azure Media Services</span></span>
<span data-ttu-id="6abcd-104">Azure 媒體服務提供 HTTP 式「彈性資料流」和漸進式下載功能。</span><span class="sxs-lookup"><span data-stu-id="6abcd-104">Azure Media Services provides HTTP based Adaptive Streaming and progressive download.</span></span> <span data-ttu-id="6abcd-105">HTTP 式資料流具有快取 Proxy 和 CDN 層，以及快取用戶端的優點，所以延展性極佳。</span><span class="sxs-lookup"><span data-stu-id="6abcd-105">HTTP based streaming is highly scalable with benefits of caching in proxy and CDN layers as well as client side caching.</span></span> <span data-ttu-id="6abcd-106">資料流端點提供一般串流功能，以及 HTTP 快取標頭的組態。</span><span class="sxs-lookup"><span data-stu-id="6abcd-106">Streaming endpoints provides general streaming capabilities and also configuration for HTTP cache headers.</span></span> <span data-ttu-id="6abcd-107">串流端點會設定 HTTP Cache-Control: max-age 和 Expires 標頭。</span><span class="sxs-lookup"><span data-stu-id="6abcd-107">Streaming endpoints sets HTTP Cache-Control: max-age and Expires headers.</span></span> <span data-ttu-id="6abcd-108">您可以從 [W3.org](http://www.w3.org/Protocols/rfc2616/rfc2616-sec13.html)(英文) 取得 HTTP 快取標頭的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="6abcd-108">You can get more information for HTTP cache headers from [W3.org](http://www.w3.org/Protocols/rfc2616/rfc2616-sec13.html).</span></span>

## <a name="default-caching-headers"></a><span data-ttu-id="6abcd-109">預設快取標頭</span><span class="sxs-lookup"><span data-stu-id="6abcd-109">Default Caching headers</span></span>
<span data-ttu-id="6abcd-110">根據預設，資料流端點會針對隨選資料流處理的資料 (實際的媒體片段/區塊) 和資訊清單 (播放清單) 套用 3 天快取標頭。</span><span class="sxs-lookup"><span data-stu-id="6abcd-110">By default streaming-endpoints apply 3 day cache headers for on-demand streaming data (actual media fragments/chunks) and manifest(playlist).</span></span> <span data-ttu-id="6abcd-111">如果是即時資料流，資料流端點會針對資料 (實際的媒體片段/區塊) 套用 3 天快取標頭，針對資訊清單 (播放清單) 要求套用 2 秒快取標頭。</span><span class="sxs-lookup"><span data-stu-id="6abcd-111">For live streaming, streaming endpoints apply 3 day cache headers for data (actual media fragments/chunks) and 2 seconds cache header for manifest(playlist) requests.</span></span> <span data-ttu-id="6abcd-112">當即時計劃 tooon 隨 （即時封存） 然後套用點播串流處理快取標頭。</span><span class="sxs-lookup"><span data-stu-id="6abcd-112">When live program turns tooon-demand (live archive) then on-demand streaming cache headers apply.</span></span>

## <a name="azure-cdn-integration"></a><span data-ttu-id="6abcd-113">Azure CDN 整合</span><span class="sxs-lookup"><span data-stu-id="6abcd-113">Azure CDN integration</span></span>
<span data-ttu-id="6abcd-114">Azure 媒體服務為資料流端點提供 [整合式 CDN](https://azure.microsoft.com/updates/azure-media-services-now-fully-integrated-with-azure-cdn/) 。</span><span class="sxs-lookup"><span data-stu-id="6abcd-114">Azure Media Services provides [integrated CDN](https://azure.microsoft.com/updates/azure-media-services-now-fully-integrated-with-azure-cdn/) for streaming-endpoints.</span></span> <span data-ttu-id="6abcd-115">快取控制標頭套用 hello 相同方式與資料流端點 tooCDN 啟用串流端點。</span><span class="sxs-lookup"><span data-stu-id="6abcd-115">Cache-control headers applies in hello same way as streaming endpoints tooCDN enabled streaming endpoints.</span></span> <span data-ttu-id="6abcd-116">內部資料流端點設定快取值 toodefine hello 存留時間 hello azure CDN 會使用快取物件，而且也會使用此值 tooset hello 傳遞快取標頭。</span><span class="sxs-lookup"><span data-stu-id="6abcd-116">Azure CDN uses streaming endpoint configured cache values toodefine hello life time of hello internally cached objects and also uses this value tooset hello delivery cache headers.</span></span> <span data-ttu-id="6abcd-117">使用 CDN 啟用的串流端點時，不建議您使用 tooset 小型的快取值。</span><span class="sxs-lookup"><span data-stu-id="6abcd-117">When using CDN enabled streaming endpoints it is not recommended tooset small cache values.</span></span> <span data-ttu-id="6abcd-118">設定較小的值將降低 hello 效能並減少 hello CDN 的優點。</span><span class="sxs-lookup"><span data-stu-id="6abcd-118">Setting small values will decrease hello performance and reduce hello benefit of CDN.</span></span> <span data-ttu-id="6abcd-119">不允許小於 600 秒 cdn 的 tooset 快取標頭啟用串流端點。</span><span class="sxs-lookup"><span data-stu-id="6abcd-119">It is not allowed tooset cache headers smaller than 600 seconds for CDN enabled streaming endpoints.</span></span>

> [!IMPORTANT]
><span data-ttu-id="6abcd-120">Azure 媒體服務可與 Azure CDN 完整整合。</span><span class="sxs-lookup"><span data-stu-id="6abcd-120">Azure Media Services has complete integration with Azure CDN.</span></span> <span data-ttu-id="6abcd-121">只要按一下，您可以整合所有 hello 提供 Azure CDN 提供者 （Akamai 和 Verizon） tooyour 串流端點包括 CDN 標準和進階版的產品。</span><span class="sxs-lookup"><span data-stu-id="6abcd-121">With a single click you can integrate all hello available Azure CDN providers (Akamai and Verizon) tooyour streaming endpoint including CDN Standard and Premium products.</span></span> <span data-ttu-id="6abcd-122">如需詳細資訊，請參閱[此公告](https://azure.microsoft.com/blog/standardstreamingendpoint/) 。</span><span class="sxs-lookup"><span data-stu-id="6abcd-122">For more information, see this [announcement](https://azure.microsoft.com/blog/standardstreamingendpoint/).</span></span>
> 
> <span data-ttu-id="6abcd-123">如果 hello CDN，透過啟用串流端點應用程式開發介面或使用 Azure 管理入口網站的資料流端點區段從串流端點 tooCDN 資料費用只取得停用。</span><span class="sxs-lookup"><span data-stu-id="6abcd-123">Data charges from streaming endpoint tooCDN only gets disabled if hello CDN is enabled over streaming endpoint APIs or using Azure management portal's streaming endpoint section.</span></span> <span data-ttu-id="6abcd-124">手動整合，或直接建立 CDN 端點使用 CDN Api 或入口網站 區段，將會不停用 hello 資料費用。</span><span class="sxs-lookup"><span data-stu-id="6abcd-124">Manual integration or directly creating a CDN endpoint using CDN APIs or portal section will not disable hello data charges.</span></span>

## <a name="configuring-cache-headers-with-azure-media-services"></a><span data-ttu-id="6abcd-125">使用 Azure 媒體服務設定快取標頭</span><span class="sxs-lookup"><span data-stu-id="6abcd-125">Configuring cache headers with Azure Media Services</span></span>
<span data-ttu-id="6abcd-126">您可以使用 Azure 管理入口網站或 Azure Media Services Api tooconfigure 快取標頭值。</span><span class="sxs-lookup"><span data-stu-id="6abcd-126">You can use Azure Management portal or Azure Media Services APIs tooconfigure cache header values.</span></span>

1. <span data-ttu-id="6abcd-127">使用 management tooconfigure 快取標頭入口網站，請參閱太[如何 tooManage 資料流端點](../media-services/media-services-portal-manage-streaming-endpoints.md)區段設定 hello 串流端點。</span><span class="sxs-lookup"><span data-stu-id="6abcd-127">tooconfigure cache headers using management portal please refer too[How tooManage Streaming Endpoints](../media-services/media-services-portal-manage-streaming-endpoints.md) section Configuring hello Streaming Endpoint.</span></span>
2. <span data-ttu-id="6abcd-128">Azure 媒體服務 REST API， [StreamingEndpoint](https://msdn.microsoft.com/library/azure/dn783468.aspx#StreamingEndpointCacheControl)。</span><span class="sxs-lookup"><span data-stu-id="6abcd-128">Azure Media Services REST API, [StreamingEndpoint](https://msdn.microsoft.com/library/azure/dn783468.aspx#StreamingEndpointCacheControl).</span></span>
3. <span data-ttu-id="6abcd-129">Azure 媒體服務 .NET SDK， [StreamingEndpointCacheControl 屬性](http://go.microsoft.com/fwlink/?LinkId=615302)。</span><span class="sxs-lookup"><span data-stu-id="6abcd-129">Azure Media Services .NET SDK, [StreamingEndpointCacheControl Properties](http://go.microsoft.com/fwlink/?LinkId=615302).</span></span>

## <a name="cache-configuration-precedence-order"></a><span data-ttu-id="6abcd-130">快取組態的優先順序</span><span class="sxs-lookup"><span data-stu-id="6abcd-130">Cache configuration precedence order</span></span>
1. <span data-ttu-id="6abcd-131">Azure 媒體服務的已設定快取值會覆寫預設值。</span><span class="sxs-lookup"><span data-stu-id="6abcd-131">Azure Media Services configured cache value overrides default value.</span></span>
2. <span data-ttu-id="6abcd-132">如果沒有任何手動組態，系統會套用預設值。</span><span class="sxs-lookup"><span data-stu-id="6abcd-132">If there is no manual configuration, default values applies.</span></span>
3. <span data-ttu-id="6abcd-133">根據預設 2 秒 toolive 串流 manifest(playlist) 不論 Azure 媒體或 Azure 儲存體組態和覆寫此值，適用於快取標頭無法使用。</span><span class="sxs-lookup"><span data-stu-id="6abcd-133">By default 2 seconds cache headers applies toolive streaming manifest(playlist) regardless of Azure Media or Azure Storage configuration and overriding of this value is not available.</span></span>

