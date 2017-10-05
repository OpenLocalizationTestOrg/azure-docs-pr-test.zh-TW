---
title: "使用 Azure CDN 透過 HTTPS 以自訂網域存取 blob"
description: "了解如何整合 Azure CDN 與 Blob 儲存體，以透過 HTTPS 使用自訂網域存取 blob"
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
ms.openlocfilehash: 6bad04df324a374f6e8473890345cf516322abd6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="using-the-azure-cdn-to-access-blobs-with-custom-domains-over-https"></a><span data-ttu-id="d50f7-103">使用 Azure CDN 透過 HTTPS 以自訂網域存取 blob</span><span class="sxs-lookup"><span data-stu-id="d50f7-103">Using the Azure CDN to access blobs with custom domains over HTTPS</span></span>

<span data-ttu-id="d50f7-104">Azure 內容傳遞網路 (CDN) 現在支援自訂網域名稱使用 HTTPS。</span><span class="sxs-lookup"><span data-stu-id="d50f7-104">Azure Content Delivery Network (CDN) now supports HTTPS for custom domain names.</span></span>
<span data-ttu-id="d50f7-105">您可以利用這個功能，使用您的自訂網域透過 HTTPS 存取儲存體 blob。</span><span class="sxs-lookup"><span data-stu-id="d50f7-105">You can leverage this feature to access storage blobs using your custom domain over HTTPS.</span></span> <span data-ttu-id="d50f7-106">若要這樣做，您必須先在您的 blob 端點啟用 Azure CDN，並將 CDN 對應至自訂網域名稱。</span><span class="sxs-lookup"><span data-stu-id="d50f7-106">To do so, you’ll first need to enable Azure CDN on your blob endpoint and map the CDN to a custom domain name.</span></span> <span data-ttu-id="d50f7-107">一旦您採取這些步驟，啟用自訂網域 HTTPS 就會簡化為一步啟用和完整憑證管理，而且不須要 CDN 價格以外的費用。</span><span class="sxs-lookup"><span data-stu-id="d50f7-107">Once you take these steps, enabling HTTPS for your custom domain is simplified via one-click enablement, complete certificate management, and all with no additional cost to normal CDN pricing.</span></span>

<span data-ttu-id="d50f7-108">這項功能很重要，因為它讓您可以在傳輸敏感的 Web 應用程式資料時保護隱私與資料完整性。</span><span class="sxs-lookup"><span data-stu-id="d50f7-108">This ability is important because it enables you to protect the privacy and data integrity of your sensitive web application data while in transit.</span></span> <span data-ttu-id="d50f7-109">使用 SSL 通訊協定透過 HTTPS 提供流量，可確保資料在網際網路上傳遞時已經過加密。</span><span class="sxs-lookup"><span data-stu-id="d50f7-109">Using the SSL protocol to serve traffic via HTTPS ensures that data is encrypted when it is sent across the internet.</span></span> <span data-ttu-id="d50f7-110">HTTPS 提供信任與認證，並保護您的 Web 應用程式免於攻擊。</span><span class="sxs-lookup"><span data-stu-id="d50f7-110">HTTPS provides trust and authentication, and protects your web applications from attacks.</span></span>

> [!NOTE]
> <span data-ttu-id="d50f7-111">除了提供自訂網域名稱的 SSL 支援，Azure CDN 也可協助您調整應用程式規模，以便在世界各地供應高頻寬內容。</span><span class="sxs-lookup"><span data-stu-id="d50f7-111">In addition to providing SSL support for custom domain names, the Azure CDN can help you scale your application to deliver high-bandwidth content around the world.</span></span>
> <span data-ttu-id="d50f7-112">若要深入了解，請參閱 [Azure CDN 概觀](../../cdn/cdn-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="d50f7-112">To learn more, check out [Overview of the Azure CDN](../../cdn/cdn-overview.md).</span></span>
>
>

## <a name="quick-start"></a><span data-ttu-id="d50f7-113">快速入門</span><span class="sxs-lookup"><span data-stu-id="d50f7-113">Quick start</span></span>

<span data-ttu-id="d50f7-114">以下是您的自訂 Blob 儲存體端點啟用 HTTPS 所需的步驟︰</span><span class="sxs-lookup"><span data-stu-id="d50f7-114">These are the steps required to enable HTTPS for your custom blob storage endpoint:</span></span>

1.  <span data-ttu-id="d50f7-115">[整合 Azure 儲存體帳戶與 Azure CDN](../../cdn/cdn-create-a-storage-account-with-cdn.md)。</span><span class="sxs-lookup"><span data-stu-id="d50f7-115">[Integrate an Azure storage account with Azure CDN](../../cdn/cdn-create-a-storage-account-with-cdn.md).</span></span>
    <span data-ttu-id="d50f7-116">如果您還沒有在 Azure 入口網站中建立儲存體帳戶，本文將逐步引導您。</span><span class="sxs-lookup"><span data-stu-id="d50f7-116">This article walks you through creating a storage account in the Azure Portal if you have not done so already.</span></span>
2.  <span data-ttu-id="d50f7-117">[將 Azure CDN 內容對應至自訂網域](../../cdn/cdn-map-content-to-custom-domain.md)。</span><span class="sxs-lookup"><span data-stu-id="d50f7-117">[Map Azure CDN content to a custom domain](../../cdn/cdn-map-content-to-custom-domain.md).</span></span>
3.  <span data-ttu-id="d50f7-118">[在 Azure CDN 自訂網域上啟用 HTTPS](../../cdn/cdn-custom-ssl.md)。</span><span class="sxs-lookup"><span data-stu-id="d50f7-118">[Enable HTTPS on an Azure CDN custom domain](../../cdn/cdn-custom-ssl.md).</span></span>

## <a name="shared-access-signatures"></a><span data-ttu-id="d50f7-119">共用存取簽章</span><span class="sxs-lookup"><span data-stu-id="d50f7-119">Shared Access Signatures</span></span>

<span data-ttu-id="d50f7-120">如果您的 Blob 儲存體端點設定為不允許匿名讀取權限，則必須在您對您的自訂網域提出的每個要求中提供[共用存取簽章 (SAS)](../common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json) 權杖。</span><span class="sxs-lookup"><span data-stu-id="d50f7-120">If your blob storage endpoint is configured to disallow anonymous read access, you will need to provide a [Shared Access Signature (SAS)](../common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json) token in each request you make to your custom domain.</span></span> <span data-ttu-id="d50f7-121">根據預設，Blob 儲存體端點不允許匿名讀取權限。</span><span class="sxs-lookup"><span data-stu-id="d50f7-121">By default, blob storage endpoints disallow anonymous read access.</span></span> <span data-ttu-id="d50f7-122">如需共用存取簽章的詳細資訊，請參閱[管理對容器與 blob 的匿名讀取權限](storage-manage-access-to-resources.md)。</span><span class="sxs-lookup"><span data-stu-id="d50f7-122">See [Managing anonymous read access to containers and blobs](storage-manage-access-to-resources.md) for more information on shared access signatures.</span></span>

<span data-ttu-id="d50f7-123">Azure CDN 不理會任何加在 SAS 權杖上的限制。</span><span class="sxs-lookup"><span data-stu-id="d50f7-123">Azure CDN does not respect any restrictions added to the SAS token.</span></span> <span data-ttu-id="d50f7-124">例如，所有 SAS 權杖都有到期時間。</span><span class="sxs-lookup"><span data-stu-id="d50f7-124">For example, all SAS tokens have an expiration time.</span></span> <span data-ttu-id="d50f7-125">這表示使用過期的 SAS 仍可存取內容，直到內容從 CDN 邊緣節點上被清除。</span><span class="sxs-lookup"><span data-stu-id="d50f7-125">This means that content can still be accessed with an expired SAS until that content is purged from the CDN edge nodes.</span></span> <span data-ttu-id="d50f7-126">您可以設定快取的回應標頭，以控制可在 CDN 上快取資料多久時間。</span><span class="sxs-lookup"><span data-stu-id="d50f7-126">You can control how long data is cached on the CDN by setting the cache response header.</span></span> <span data-ttu-id="d50f7-127">如需指示請參閱[在 Azure CDN 中管理 Azure 儲存體 Blob 的到期](../../cdn/cdn-manage-expiration-of-blob-content.md)。</span><span class="sxs-lookup"><span data-stu-id="d50f7-127">See [Managing expiration of Azure Storage blobs in Azure CDN](../../cdn/cdn-manage-expiration-of-blob-content.md) for instructions.</span></span>

<span data-ttu-id="d50f7-128">如果您為同一 blob 端點建立多個 SAS URL，建議您開啟 Azure CDN 的查詢字串快取。</span><span class="sxs-lookup"><span data-stu-id="d50f7-128">If you create multiple SAS URLs for the same blob endpoint, we recommend turning on query string caching for your Azure CDN.</span></span> <span data-ttu-id="d50f7-129">這是為了確保每個 URL 會被當作唯一實體。</span><span class="sxs-lookup"><span data-stu-id="d50f7-129">This is to ensure that each URL is treated as a unique entity.</span></span> <span data-ttu-id="d50f7-130">如需詳細資訊，請參閱[使用查詢字串控制 Azure CDN 快取行為](../../cdn/cdn-query-string.md)。</span><span class="sxs-lookup"><span data-stu-id="d50f7-130">See [Controlling Azure CDN caching behavior with query strings](../../cdn/cdn-query-string.md) for more information.</span></span>

## <a name="http-to-https-redirection"></a><span data-ttu-id="d50f7-131">HTTP 至 HTTPS 的重新導向</span><span class="sxs-lookup"><span data-stu-id="d50f7-131">HTTP to HTTPS redirection</span></span>

<span data-ttu-id="d50f7-132">您可以選擇將 HTTP 流量重新導向至 HTTPS。</span><span class="sxs-lookup"><span data-stu-id="d50f7-132">You can elect to redirect HTTP traffic to HTTPS.</span></span> <span data-ttu-id="d50f7-133">這需要使用 Verizon 上提供的 Azure CDN。</span><span class="sxs-lookup"><span data-stu-id="d50f7-133">This requires use of the Azure CDN premium offering from Verizon.</span></span> <span data-ttu-id="d50f7-134">您必須用下列規則[使用 Azure CDN 規則引擎覆寫 HTTP 行為](../../cdn/cdn-rules-engine.md)：</span><span class="sxs-lookup"><span data-stu-id="d50f7-134">You need to [Override HTTP behavior using the Azure CDN rules engine](../../cdn/cdn-rules-engine.md) with the following rule:</span></span>

![](./media/storage-https-custom-domain-cdn/redirect-to-https.png)

<span data-ttu-id="d50f7-135">cdn-endpoint-name 是指您為 CDN 端點設定的名稱。</span><span class="sxs-lookup"><span data-stu-id="d50f7-135">“Cdn-endpoint-name” refers to the name that you configured for your CDN endpoint.</span></span> <span data-ttu-id="d50f7-136">您可以從下拉式清單中選取其值。</span><span class="sxs-lookup"><span data-stu-id="d50f7-136">You can select this value from the dropdown.</span></span> <span data-ttu-id="d50f7-137">origin-path 指的是您的靜態內容所在的原始儲存體帳戶的路徑。</span><span class="sxs-lookup"><span data-stu-id="d50f7-137">“Origin-path” refers to the path within your origin storage account where your static content resides.</span></span>
<span data-ttu-id="d50f7-138">如果您將所有靜態內容裝載在單一容器中，則將 origin-path 取代為該容器的名稱。</span><span class="sxs-lookup"><span data-stu-id="d50f7-138">If you are hosting all static content in a single container, replace “origin-path” with the name of that container.</span></span>

<span data-ttu-id="d50f7-139">如需深入了解規則，請參閱 [Azure CDN 規則引擎功能](../../cdn/cdn-rules-engine-reference-features.md)。</span><span class="sxs-lookup"><span data-stu-id="d50f7-139">For a deeper dive into rules, please see the [Azure CDN rules engine features](../../cdn/cdn-rules-engine-reference-features.md).</span></span>

## <a name="pricing-and-billing"></a><span data-ttu-id="d50f7-140">價格和計費</span><span class="sxs-lookup"><span data-stu-id="d50f7-140">Pricing and billing</span></span>

<span data-ttu-id="d50f7-141">當您透過 Azure CDN 存取 blob 時，需支付邊緣節點和起點 (Blob 儲存體) 之間流量的 [Blob 儲存體價格](https://azure.microsoft.com/pricing/details/storage/blobs/)，以及從邊緣節點存取資料的 [CDN 價格](https://azure.microsoft.com/pricing/details/cdn/)。</span><span class="sxs-lookup"><span data-stu-id="d50f7-141">When you access blobs through an Azure CDN, you pay [Blob storage prices](https://azure.microsoft.com/pricing/details/storage/blobs/) for traffic between the edge nodes and the origin (Blob storage), and [CDN prices](https://azure.microsoft.com/pricing/details/cdn/) for data accessed from the edge nodes.</span></span>

<span data-ttu-id="d50f7-142">例如，假設您的儲存體帳戶在美國西部，且使用 Azure CDN 存取它。</span><span class="sxs-lookup"><span data-stu-id="d50f7-142">For example, say you have a storage account in West US that is being accessed using an Azure CDN.</span></span> <span data-ttu-id="d50f7-143">如果有人在英國嘗試透過 CDN 存取該儲存體帳戶中的其中一個 blob，Azure 會先檢查該 blob 最接近英國的邊緣節點。</span><span class="sxs-lookup"><span data-stu-id="d50f7-143">If someone in the UK tries to access one of the blobs in that storage account via the CDN, Azure first checks the edge node closest to the UK for that blob.</span></span> <span data-ttu-id="d50f7-144">如果找到，它會存取該 blob 複本且會使用 CDN 定價，因為是正在 CDN 上存取。</span><span class="sxs-lookup"><span data-stu-id="d50f7-144">If found, it accesses that copy of the blob and will use CDN pricing, because it is being accessed on the CDN.</span></span> <span data-ttu-id="d50f7-145">如果找不到，Azure 會將 blob 複製到邊緣節點，這會產生輸出和交易費用 (如「Blob 儲存體價格」中所述)，然後存取邊緣節點上的檔案，而這會產生 CDN 費用。</span><span class="sxs-lookup"><span data-stu-id="d50f7-145">If not found, Azure will copy the blob to the edge node, which will result in egress and transaction charges as specified in the Blob storage pricing, and then access the file on the edge node, which will result in CDN billing.</span></span>

<span data-ttu-id="d50f7-146">查看 [CDN 價格頁面](https://azure.microsoft.com/pricing/details/cdn/)時請注意，自訂網域名稱的 HTTPS 支援只適用於 Verizon 的 Azure CDN 產品 (「標準」和「進階」)。</span><span class="sxs-lookup"><span data-stu-id="d50f7-146">When looking at the [CDN pricing page](https://azure.microsoft.com/pricing/details/cdn/), note that HTTPS support for custom domain names is only available for Azure CDN from Verizon products (Standard and Premium).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d50f7-147">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d50f7-147">Next steps</span></span>

[<span data-ttu-id="d50f7-148">針對 Blob 儲存體端點設定自訂網域名稱</span><span class="sxs-lookup"><span data-stu-id="d50f7-148">Configure a custom domain name for your Blob storage endpoint</span></span>](storage-custom-domain-name.md)
