---
title: "aaaUsing hello Azure CDN tooaccess blob 使用透過 HTTPS 的自訂網域"
description: "了解如何使用 blob 儲存體 tooaccess toointegrate hello Azure CDN 的 blob 使用自訂網域透過 HTTPS"
services: storage
documentationcenter: 
author: michaelhauss
manager: vamshik
editor: tysonn
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: mihauss
ms.openlocfilehash: f6cee36ca5495983545f2f6a8ff140677cf6914b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-azure-cdn-tooaccess-blobs-with-custom-domains-over-https"></a><span data-ttu-id="91337-103">使用自訂網域中的 hello Azure CDN tooaccess blob，透過 HTTPS</span><span class="sxs-lookup"><span data-stu-id="91337-103">Using hello Azure CDN tooaccess blobs with custom domains over HTTPS</span></span>

<span data-ttu-id="91337-104">Azure 內容傳遞網路 (CDN) 現在支援自訂網域名稱使用 HTTPS。</span><span class="sxs-lookup"><span data-stu-id="91337-104">Azure Content Delivery Network (CDN) now supports HTTPS for custom domain names.</span></span>
<span data-ttu-id="91337-105">您可以利用此在 HTTPS 上使用自訂網域的功能 tooaccess 儲存體 blob。</span><span class="sxs-lookup"><span data-stu-id="91337-105">You can leverage this feature tooaccess storage blobs using your custom domain over HTTPS.</span></span> <span data-ttu-id="91337-106">toodo 因此，您必須先 tooenable Azure CDN 的 blob 端點和對應 hello CDN tooa 自訂網域名稱。</span><span class="sxs-lookup"><span data-stu-id="91337-106">toodo so, you’ll first need tooenable Azure CDN on your blob endpoint and map hello CDN tooa custom domain name.</span></span> <span data-ttu-id="91337-107">一旦您採取下列步驟，啟用 HTTPS 的自訂網域已經過簡化透過一種單鍵啟用，完成憑證管理，以及所有的任何額外的成本 toonormal CDN 定價。</span><span class="sxs-lookup"><span data-stu-id="91337-107">Once you take these steps, enabling HTTPS for your custom domain is simplified via one-click enablement, complete certificate management, and all with no additional cost toonormal CDN pricing.</span></span>

<span data-ttu-id="91337-108">這項功能非常重要的因為它可讓您 tooprotect hello 隱私權和機密的 web 應用程式資料在傳輸過程中的資料完整性。</span><span class="sxs-lookup"><span data-stu-id="91337-108">This ability is important because it enables you tooprotect hello privacy and data integrity of your sensitive web application data while in transit.</span></span> <span data-ttu-id="91337-109">使用 hello SSL 通訊協定 tooserve 流量透過 HTTPS 可確保已加密資料，當傳送 hello 跨網際網路。</span><span class="sxs-lookup"><span data-stu-id="91337-109">Using hello SSL protocol tooserve traffic via HTTPS ensures that data is encrypted when it is sent across hello internet.</span></span> <span data-ttu-id="91337-110">HTTPS 提供信任與認證，並保護您的 Web 應用程式免於攻擊。</span><span class="sxs-lookup"><span data-stu-id="91337-110">HTTPS provides trust and authentication, and protects your web applications from attacks.</span></span>

> [!NOTE]
> <span data-ttu-id="91337-111">此外 tooproviding SSL 支援自訂網域名稱，hello Azure CDN 可協助您調整應用程式 toodeliver 高頻寬內容 hello 世界各地。</span><span class="sxs-lookup"><span data-stu-id="91337-111">In addition tooproviding SSL support for custom domain names, hello Azure CDN can help you scale your application toodeliver high-bandwidth content around hello world.</span></span>
> <span data-ttu-id="91337-112">toolearn 詳細資訊，請參閱[hello Azure CDN 概觀](../../cdn/cdn-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="91337-112">toolearn more, check out [Overview of hello Azure CDN](../../cdn/cdn-overview.md).</span></span>
>
>

## <a name="quick-start"></a><span data-ttu-id="91337-113">快速入門</span><span class="sxs-lookup"><span data-stu-id="91337-113">Quick start</span></span>

<span data-ttu-id="91337-114">這些是您自訂的 blob 儲存體端點的 hello 步驟需要的 tooenable HTTPS:</span><span class="sxs-lookup"><span data-stu-id="91337-114">These are hello steps required tooenable HTTPS for your custom blob storage endpoint:</span></span>

1.  <span data-ttu-id="91337-115">[整合 Azure 儲存體帳戶與 Azure CDN](../../cdn/cdn-create-a-storage-account-with-cdn.md)。</span><span class="sxs-lookup"><span data-stu-id="91337-115">[Integrate an Azure storage account with Azure CDN](../../cdn/cdn-create-a-storage-account-with-cdn.md).</span></span>
    <span data-ttu-id="91337-116">這篇文章會引導您在 hello Azure 入口網站中建立儲存體帳戶，如果您有尚未完成操作。</span><span class="sxs-lookup"><span data-stu-id="91337-116">This article walks you through creating a storage account in hello Azure Portal if you have not done so already.</span></span>
2.  <span data-ttu-id="91337-117">[對應的 Azure CDN 內容 tooa 自訂網域](../../cdn/cdn-map-content-to-custom-domain.md)。</span><span class="sxs-lookup"><span data-stu-id="91337-117">[Map Azure CDN content tooa custom domain](../../cdn/cdn-map-content-to-custom-domain.md).</span></span>
3.  <span data-ttu-id="91337-118">[在 Azure CDN 自訂網域上啟用 HTTPS](../../cdn/cdn-custom-ssl.md)。</span><span class="sxs-lookup"><span data-stu-id="91337-118">[Enable HTTPS on an Azure CDN custom domain](../../cdn/cdn-custom-ssl.md).</span></span>

## <a name="shared-access-signatures"></a><span data-ttu-id="91337-119">共用存取簽章</span><span class="sxs-lookup"><span data-stu-id="91337-119">Shared Access Signatures</span></span>

<span data-ttu-id="91337-120">如果您的 blob 儲存體端點設定的 toodisallow 匿名讀取權限，您將需要 tooprovide[共用存取簽章 (SAS)](../common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)語彙基元，在每個要求您進行 tooyour 自訂網域。</span><span class="sxs-lookup"><span data-stu-id="91337-120">If your blob storage endpoint is configured toodisallow anonymous read access, you will need tooprovide a [Shared Access Signature (SAS)](../common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json) token in each request you make tooyour custom domain.</span></span> <span data-ttu-id="91337-121">根據預設，Blob 儲存體端點不允許匿名讀取權限。</span><span class="sxs-lookup"><span data-stu-id="91337-121">By default, blob storage endpoints disallow anonymous read access.</span></span> <span data-ttu-id="91337-122">如需共用存取簽章的詳細資訊，請參閱[管理對容器與 blob 的匿名讀取權限](storage-manage-access-to-resources.md)。</span><span class="sxs-lookup"><span data-stu-id="91337-122">See [Managing anonymous read access to containers and blobs](storage-manage-access-to-resources.md) for more information on shared access signatures.</span></span>

<span data-ttu-id="91337-123">Azure CDN 不會遵守任何限制加入的 toohello SAS 權杖。</span><span class="sxs-lookup"><span data-stu-id="91337-123">Azure CDN does not respect any restrictions added toohello SAS token.</span></span> <span data-ttu-id="91337-124">例如，所有 SAS 權杖都有到期時間。</span><span class="sxs-lookup"><span data-stu-id="91337-124">For example, all SAS tokens have an expiration time.</span></span> <span data-ttu-id="91337-125">這表示內容仍然使用過期的 SAS 存取，直到該內容會清除從 hello CDN 邊緣節點。</span><span class="sxs-lookup"><span data-stu-id="91337-125">This means that content can still be accessed with an expired SAS until that content is purged from hello CDN edge nodes.</span></span> <span data-ttu-id="91337-126">您可以控制多久快取資料 hello CDN 上所設定的 hello 快取的回應標頭。</span><span class="sxs-lookup"><span data-stu-id="91337-126">You can control how long data is cached on hello CDN by setting hello cache response header.</span></span> <span data-ttu-id="91337-127">如需指示請參閱[在 Azure CDN 中管理 Azure 儲存體 Blob 的到期](../../cdn/cdn-manage-expiration-of-blob-content.md)。</span><span class="sxs-lookup"><span data-stu-id="91337-127">See [Managing expiration of Azure Storage blobs in Azure CDN](../../cdn/cdn-manage-expiration-of-blob-content.md) for instructions.</span></span>

<span data-ttu-id="91337-128">如果您要建立 hello 的多個 SAS Url 相同的 blob 端點，我們建議您開啟您的 Azure CDN 的快取的查詢字串。</span><span class="sxs-lookup"><span data-stu-id="91337-128">If you create multiple SAS URLs for hello same blob endpoint, we recommend turning on query string caching for your Azure CDN.</span></span> <span data-ttu-id="91337-129">這是 tooensure，每個 URL 會被視為唯一的實體。</span><span class="sxs-lookup"><span data-stu-id="91337-129">This is tooensure that each URL is treated as a unique entity.</span></span> <span data-ttu-id="91337-130">如需詳細資訊，請參閱[使用查詢字串控制 Azure CDN 快取行為](../../cdn/cdn-query-string.md)。</span><span class="sxs-lookup"><span data-stu-id="91337-130">See [Controlling Azure CDN caching behavior with query strings](../../cdn/cdn-query-string.md) for more information.</span></span>

## <a name="http-toohttps-redirection"></a><span data-ttu-id="91337-131">HTTP tooHTTPS 重新導向</span><span class="sxs-lookup"><span data-stu-id="91337-131">HTTP tooHTTPS redirection</span></span>

<span data-ttu-id="91337-132">您可以選擇 tooredirect HTTP 流量 tooHTTPS。</span><span class="sxs-lookup"><span data-stu-id="91337-132">You can elect tooredirect HTTP traffic tooHTTPS.</span></span> <span data-ttu-id="91337-133">這需要從 Verizon hello Azure CDN premium 供應項目的使用。</span><span class="sxs-lookup"><span data-stu-id="91337-133">This requires use of hello Azure CDN premium offering from Verizon.</span></span> <span data-ttu-id="91337-134">您需要[覆寫 HTTP 使用的 Azure CDN 規則引擎的行為](../../cdn/cdn-rules-engine.md)下列規則：</span><span class="sxs-lookup"><span data-stu-id="91337-134">You need too[Override HTTP behavior using the Azure CDN rules engine](../../cdn/cdn-rules-engine.md) with the following rule:</span></span>

![](./media/storage-https-custom-domain-cdn/redirect-to-https.png)

<span data-ttu-id="91337-135">"Cdn 的端點名稱的"是指在您設定您的 CDN 端點的 toohello 名稱。</span><span class="sxs-lookup"><span data-stu-id="91337-135">“Cdn-endpoint-name” refers toohello name that you configured for your CDN endpoint.</span></span> <span data-ttu-id="91337-136">您可以從 hello 下拉式清單中選取此值。</span><span class="sxs-lookup"><span data-stu-id="91337-136">You can select this value from hello dropdown.</span></span> <span data-ttu-id="91337-137">[來源路徑] 是指您靜態內容所在來源儲存體帳戶中的 hello 路徑。</span><span class="sxs-lookup"><span data-stu-id="91337-137">“Origin-path” refers to hello path within your origin storage account where your static content resides.</span></span>
<span data-ttu-id="91337-138">如果您裝載單一容器中的所有靜態內容，取代 hello 名稱，該容器的 [來源路徑]。</span><span class="sxs-lookup"><span data-stu-id="91337-138">If you are hosting all static content in a single container, replace “origin-path” with hello name of that container.</span></span>

<span data-ttu-id="91337-139">規則深入剖析，請參閱 hello [Azure CDN 規則引擎功能](../../cdn/cdn-rules-engine-reference-features.md)。</span><span class="sxs-lookup"><span data-stu-id="91337-139">For a deeper dive into rules, please see hello [Azure CDN rules engine features](../../cdn/cdn-rules-engine-reference-features.md).</span></span>

## <a name="pricing-and-billing"></a><span data-ttu-id="91337-140">價格和計費</span><span class="sxs-lookup"><span data-stu-id="91337-140">Pricing and billing</span></span>

<span data-ttu-id="91337-141">當您透過 Azure CDN 存取 blob 時，您必須支付[Blob 儲存體價格](https://azure.microsoft.com/pricing/details/storage/blobs/)hello 邊緣節點與 hello 原點 （Blob 儲存） 之間的流量和[CDN 價格](https://azure.microsoft.com/pricing/details/cdn/)從 hello 邊緣節點存取的資料。</span><span class="sxs-lookup"><span data-stu-id="91337-141">When you access blobs through an Azure CDN, you pay [Blob storage prices](https://azure.microsoft.com/pricing/details/storage/blobs/) for traffic between hello edge nodes and hello origin (Blob storage), and [CDN prices](https://azure.microsoft.com/pricing/details/cdn/) for data accessed from hello edge nodes.</span></span>

<span data-ttu-id="91337-142">例如，假設您的儲存體帳戶在美國西部，且使用 Azure CDN 存取它。</span><span class="sxs-lookup"><span data-stu-id="91337-142">For example, say you have a storage account in West US that is being accessed using an Azure CDN.</span></span> <span data-ttu-id="91337-143">如果有人在 hello 英國嘗試的 tooaccess hello 的其中一個 hello CDN 透過該儲存體帳戶中的 blob，Azure 會先檢查最接近該 blob hello 英國 hello 邊緣節點。</span><span class="sxs-lookup"><span data-stu-id="91337-143">If someone in hello UK tries tooaccess one of hello blobs in that storage account via hello CDN, Azure first checks hello edge node closest to hello UK for that blob.</span></span> <span data-ttu-id="91337-144">如果找到，它會存取該副本 hello blob，並會使用 CDN 定價，因為它正在存取 hello CDN 上。</span><span class="sxs-lookup"><span data-stu-id="91337-144">If found, it accesses that copy of hello blob and will use CDN pricing, because it is being accessed on hello CDN.</span></span> <span data-ttu-id="91337-145">如果找不到，Azure 將會複製 hello blob toohello 邊緣節點，這會導致輸出和交易費用，以指定在 hello Blob 儲存體定價，並存取 hello 邊緣節點上，而導致 CDN 計費 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="91337-145">If not found, Azure will copy hello blob toohello edge node, which will result in egress and transaction charges as specified in hello Blob storage pricing, and then access hello file on hello edge node, which will result in CDN billing.</span></span>

<span data-ttu-id="91337-146">查看 hello 時[CDN 定價頁面](https://azure.microsoft.com/pricing/details/cdn/)，請注意，HTTPS 支援的自訂網域名稱只適用於 Azure CDN 從 Verizon 產品 （Standard 和 Premium）。</span><span class="sxs-lookup"><span data-stu-id="91337-146">When looking at hello [CDN pricing page](https://azure.microsoft.com/pricing/details/cdn/), note that HTTPS support for custom domain names is only available for Azure CDN from Verizon products (Standard and Premium).</span></span>

## <a name="next-steps"></a><span data-ttu-id="91337-147">後續步驟</span><span class="sxs-lookup"><span data-stu-id="91337-147">Next steps</span></span>

[<span data-ttu-id="91337-148">針對 Blob 儲存體端點設定自訂網域名稱</span><span class="sxs-lookup"><span data-stu-id="91337-148">Configure a custom domain name for your Blob storage endpoint</span></span>](storage-custom-domain-name.md)
