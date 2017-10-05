---
title: "Azure CDN 中的 HTTP/2 支援 | Microsoft Docs"
description: "了解 HTTP/2 和 CDN 支援。"
services: cdn
documentationcenter: 
author: lichard
manager: erikre
editor: 
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 5/04/2017
ms.author: rli
ms.openlocfilehash: 4f8dd685c3ae89535217d7a17a01c5129ca7e6e4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="http2-support-in-azure-cdn"></a><span data-ttu-id="6eb9c-103">Azure CDN 中的 HTTP/2 支援</span><span class="sxs-lookup"><span data-stu-id="6eb9c-103">HTTP/2 Support in Azure CDN</span></span>

<span data-ttu-id="6eb9c-104">HTTP/2 是主要 HTTP/1.1\ 有所修訂。</span><span class="sxs-lookup"><span data-stu-id="6eb9c-104">HTTP/2 is a major revision to HTTP/1.1\.</span></span> <span data-ttu-id="6eb9c-105">它會提供更快速 web 效能、 降低的回應時間，以及改善的使用者體驗，同時維持類似的 HTTP 方法，狀態碼和語意。</span><span class="sxs-lookup"><span data-stu-id="6eb9c-105">It provides faster web performance, reduced response time, and improved user experience, while maintaining the familiar HTTP methods, status codes, and semantics.</span></span> <span data-ttu-id="6eb9c-106">雖然 HTTP/2 是設計來搭配 HTTP 和 HTTPS，但許多用戶端 Web 瀏覽器僅支援透過 TLS 使用 HTTP/2。</span><span class="sxs-lookup"><span data-stu-id="6eb9c-106">Though HTTP/2 is designed to work with HTTP and HTTPS, many client web browsers only support HTTP/2 over TLS.</span></span>

###<a name="http2-benefits"></a><span data-ttu-id="6eb9c-107">HTTP/2 的優點</span><span class="sxs-lookup"><span data-stu-id="6eb9c-107">HTTP/2 Benefits</span></span>

<span data-ttu-id="6eb9c-108">HTTP/2 的優點包括︰</span><span class="sxs-lookup"><span data-stu-id="6eb9c-108">The benefits of HTTP/2 include:</span></span>

*   <span data-ttu-id="6eb9c-109">**多工和並行**</span><span class="sxs-lookup"><span data-stu-id="6eb9c-109">**Multiplexing and concurrency**</span></span>

    <span data-ttu-id="6eb9c-110">使用 HTTP 1.1 時，多方提出多個資源要求需要多個 TCP 連線，每個連線都有其相關聯的效能負荷。</span><span class="sxs-lookup"><span data-stu-id="6eb9c-110">Using HTTP 1.1, multiple making multiple resource requests requires multiple TCP connections, and each connection has performance overhead associated with it.</span></span> <span data-ttu-id="6eb9c-111">HTTP/2 允許在單一 TCP 連線上要求多個資源。</span><span class="sxs-lookup"><span data-stu-id="6eb9c-111">HTTP/2 allows multiple resources to be requested on a single TCP connection.</span></span>

*   <span data-ttu-id="6eb9c-112">**標頭壓縮**</span><span class="sxs-lookup"><span data-stu-id="6eb9c-112">**Header compression**</span></span>

    <span data-ttu-id="6eb9c-113">將提供的資源壓縮 HTTP 標頭，可大幅縮短網路上的時間。</span><span class="sxs-lookup"><span data-stu-id="6eb9c-113">By compressing the HTTP headers for served resources, time on the wire is reduced significantly.</span></span>

*   <span data-ttu-id="6eb9c-114">**資料流相依性**</span><span class="sxs-lookup"><span data-stu-id="6eb9c-114">**Stream dependencies**</span></span>

    <span data-ttu-id="6eb9c-115">資料流相依性可讓用戶端向伺服器表示哪個資源最優先。</span><span class="sxs-lookup"><span data-stu-id="6eb9c-115">Stream dependencies allow the client to indicate to the server which of resources have priority.</span></span>


##<a name="http2-browser-support"></a><span data-ttu-id="6eb9c-116">HTTP/2 瀏覽器支援</span><span class="sxs-lookup"><span data-stu-id="6eb9c-116">HTTP/2 Browser Support</span></span>

<span data-ttu-id="6eb9c-117">所有主要瀏覽器都已在其目前的版本中實作 HTTP/2 支援。</span><span class="sxs-lookup"><span data-stu-id="6eb9c-117">All of the major browsers have implemented HTTP/2 support in their current versions.</span></span> <span data-ttu-id="6eb9c-118">不支援的瀏覽器會自動降回 HTTP/1.1。</span><span class="sxs-lookup"><span data-stu-id="6eb9c-118">Non-supported browsers will automatically fallback to HTTP/1.1.</span></span>

|<span data-ttu-id="6eb9c-119">[瀏覽器]</span><span class="sxs-lookup"><span data-stu-id="6eb9c-119">Browser</span></span>|<span data-ttu-id="6eb9c-120">最低版本</span><span class="sxs-lookup"><span data-stu-id="6eb9c-120">Minimum Version</span></span>|
|-------------|------------|
|<span data-ttu-id="6eb9c-121">Microsoft Edge</span><span class="sxs-lookup"><span data-stu-id="6eb9c-121">Microsoft Edge</span></span>| <span data-ttu-id="6eb9c-122">12</span><span class="sxs-lookup"><span data-stu-id="6eb9c-122">12</span></span>|
|<span data-ttu-id="6eb9c-123">Google Chrome</span><span class="sxs-lookup"><span data-stu-id="6eb9c-123">Google Chrome</span></span>| <span data-ttu-id="6eb9c-124">43</span><span class="sxs-lookup"><span data-stu-id="6eb9c-124">43</span></span>|
|<span data-ttu-id="6eb9c-125">Mozilla Firefox</span><span class="sxs-lookup"><span data-stu-id="6eb9c-125">Mozilla Firefox</span></span>| <span data-ttu-id="6eb9c-126">38</span><span class="sxs-lookup"><span data-stu-id="6eb9c-126">38</span></span>|
|<span data-ttu-id="6eb9c-127">Opera</span><span class="sxs-lookup"><span data-stu-id="6eb9c-127">Opera</span></span>| <span data-ttu-id="6eb9c-128">32</span><span class="sxs-lookup"><span data-stu-id="6eb9c-128">32</span></span>|
|<span data-ttu-id="6eb9c-129">Safari</span><span class="sxs-lookup"><span data-stu-id="6eb9c-129">Safari</span></span>| <span data-ttu-id="6eb9c-130">9</span><span class="sxs-lookup"><span data-stu-id="6eb9c-130">9</span></span>|

##<a name="enabling-http2-support-in-azure-cdn"></a><span data-ttu-id="6eb9c-131">啟用 Azure CDN 中的 HTTP/2 支援</span><span class="sxs-lookup"><span data-stu-id="6eb9c-131">Enabling HTTP/2 Support in Azure CDN</span></span>

<span data-ttu-id="6eb9c-132">目前，**Akamai 的 Azure CDN** 和 **Verizon 的 Azure CDN** 設定檔已支援 HTTP/2。</span><span class="sxs-lookup"><span data-stu-id="6eb9c-132">Currently HTTP/2 support is active for **Azure CDN from Akamai** and **Azure CDN from Verizon** profiles.</span></span> <span data-ttu-id="6eb9c-133">客戶不需要採取任何動作。</span><span class="sxs-lookup"><span data-stu-id="6eb9c-133">No further action is required from customers.</span></span>

##<a name="next-steps"></a><span data-ttu-id="6eb9c-134">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6eb9c-134">Next Steps</span></span>

<span data-ttu-id="6eb9c-135">若要了解 HTTP/2 在實務上的優點，請參閱 [Akamai 的這個示範](https://http2.akamai.com/demo)。</span><span class="sxs-lookup"><span data-stu-id="6eb9c-135">To see the benefits of HTTP/2 in action, see [this demo from Akamai](https://http2.akamai.com/demo).</span></span>

<span data-ttu-id="6eb9c-136">若要深入了解 HTTP/2，請瀏覽下列資源：</span><span class="sxs-lookup"><span data-stu-id="6eb9c-136">To learn more about HTTP/2, visit the following resources:</span></span>

*   [<span data-ttu-id="6eb9c-137">HTTP/2 規格首頁</span><span class="sxs-lookup"><span data-stu-id="6eb9c-137">HTTP/2 specification homepage</span></span>](https://http2.github.io/)
*   [<span data-ttu-id="6eb9c-138">官方 HTTP/2 常見問題集</span><span class="sxs-lookup"><span data-stu-id="6eb9c-138">Official HTTP/2 FAQ</span></span>](https://http2.github.io/faq/)
*   [<span data-ttu-id="6eb9c-139">Akamai HTTP/2 資訊</span><span class="sxs-lookup"><span data-stu-id="6eb9c-139">Akamai HTTP/2 information</span></span>](https://http2.akamai.com/)

<span data-ttu-id="6eb9c-140">若要深入了解 Azure CDN 提供的功能，請參閱 [Azure CDN 概觀](https://azure.microsoft.com/documentation/articles/cdn-overview/)。</span><span class="sxs-lookup"><span data-stu-id="6eb9c-140">To learn more about Azure CDN's available features, see the [Azure CDN Overview](https://azure.microsoft.com/documentation/articles/cdn-overview/).</span></span>