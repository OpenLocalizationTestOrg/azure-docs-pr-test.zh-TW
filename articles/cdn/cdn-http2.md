---
title: "在 Azure CDN 的 aaaHTTP/2 支援 |Microsoft 文件"
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
ms.openlocfilehash: 2e5e5345e8cf5c40e080ebf18b4f13a239a5aac5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="http2-support-in-azure-cdn"></a><span data-ttu-id="f0bf3-103">Azure CDN 中的 HTTP/2 支援</span><span class="sxs-lookup"><span data-stu-id="f0bf3-103">HTTP/2 Support in Azure CDN</span></span>

<span data-ttu-id="f0bf3-104">HTTP/2 是重大修訂 tooHTTP/1.1\。</span><span class="sxs-lookup"><span data-stu-id="f0bf3-104">HTTP/2 is a major revision tooHTTP/1.1\.</span></span> <span data-ttu-id="f0bf3-105">它會提供更快速 web 效能、 降低的回應時間，以及改善的使用者體驗，同時維持 hello 熟悉的 HTTP 方法，狀態碼和語意。</span><span class="sxs-lookup"><span data-stu-id="f0bf3-105">It provides faster web performance, reduced response time, and improved user experience, while maintaining hello familiar HTTP methods, status codes, and semantics.</span></span> <span data-ttu-id="f0bf3-106">雖然 HTTP/2 是設計的 toowork HTTP 及 HTTPS，許多用戶端 web 瀏覽器僅支援 HTTP/2 5060，TLS。</span><span class="sxs-lookup"><span data-stu-id="f0bf3-106">Though HTTP/2 is designed toowork with HTTP and HTTPS, many client web browsers only support HTTP/2 over TLS.</span></span>

###<a name="http2-benefits"></a><span data-ttu-id="f0bf3-107">HTTP/2 的優點</span><span class="sxs-lookup"><span data-stu-id="f0bf3-107">HTTP/2 Benefits</span></span>

<span data-ttu-id="f0bf3-108">HTTP/2 hello 優點包括：</span><span class="sxs-lookup"><span data-stu-id="f0bf3-108">hello benefits of HTTP/2 include:</span></span>

*   <span data-ttu-id="f0bf3-109">**多工和並行**</span><span class="sxs-lookup"><span data-stu-id="f0bf3-109">**Multiplexing and concurrency**</span></span>

    <span data-ttu-id="f0bf3-110">使用 HTTP 1.1 時，多方提出多個資源要求需要多個 TCP 連線，每個連線都有其相關聯的效能負荷。</span><span class="sxs-lookup"><span data-stu-id="f0bf3-110">Using HTTP 1.1, multiple making multiple resource requests requires multiple TCP connections, and each connection has performance overhead associated with it.</span></span> <span data-ttu-id="f0bf3-111">HTTP/2 可讓多個資源 toobe 在單一 TCP 連接要求。</span><span class="sxs-lookup"><span data-stu-id="f0bf3-111">HTTP/2 allows multiple resources toobe requested on a single TCP connection.</span></span>

*   <span data-ttu-id="f0bf3-112">**標頭壓縮**</span><span class="sxs-lookup"><span data-stu-id="f0bf3-112">**Header compression**</span></span>

    <span data-ttu-id="f0bf3-113">藉由壓縮提供資源的 hello HTTP 標頭，已大幅降低 hello 網路上的時間。</span><span class="sxs-lookup"><span data-stu-id="f0bf3-113">By compressing hello HTTP headers for served resources, time on hello wire is reduced significantly.</span></span>

*   <span data-ttu-id="f0bf3-114">**資料流相依性**</span><span class="sxs-lookup"><span data-stu-id="f0bf3-114">**Stream dependencies**</span></span>

    <span data-ttu-id="f0bf3-115">資料流的相依性允許 hello 用戶端 tooindicate toohello 伺服器資源的優先順序。</span><span class="sxs-lookup"><span data-stu-id="f0bf3-115">Stream dependencies allow hello client tooindicate toohello server which of resources have priority.</span></span>


##<a name="http2-browser-support"></a><span data-ttu-id="f0bf3-116">HTTP/2 瀏覽器支援</span><span class="sxs-lookup"><span data-stu-id="f0bf3-116">HTTP/2 Browser Support</span></span>

<span data-ttu-id="f0bf3-117">所有主要瀏覽器 hello 未實作 HTTP/2 支援在其目前的版本。</span><span class="sxs-lookup"><span data-stu-id="f0bf3-117">All of hello major browsers have implemented HTTP/2 support in their current versions.</span></span> <span data-ttu-id="f0bf3-118">不支援的瀏覽器將會自動後援 tooHTTP/1.1。</span><span class="sxs-lookup"><span data-stu-id="f0bf3-118">Non-supported browsers will automatically fallback tooHTTP/1.1.</span></span>

|<span data-ttu-id="f0bf3-119">[瀏覽器]</span><span class="sxs-lookup"><span data-stu-id="f0bf3-119">Browser</span></span>|<span data-ttu-id="f0bf3-120">最低版本</span><span class="sxs-lookup"><span data-stu-id="f0bf3-120">Minimum Version</span></span>|
|-------------|------------|
|<span data-ttu-id="f0bf3-121">Microsoft Edge</span><span class="sxs-lookup"><span data-stu-id="f0bf3-121">Microsoft Edge</span></span>| <span data-ttu-id="f0bf3-122">12</span><span class="sxs-lookup"><span data-stu-id="f0bf3-122">12</span></span>|
|<span data-ttu-id="f0bf3-123">Google Chrome</span><span class="sxs-lookup"><span data-stu-id="f0bf3-123">Google Chrome</span></span>| <span data-ttu-id="f0bf3-124">43</span><span class="sxs-lookup"><span data-stu-id="f0bf3-124">43</span></span>|
|<span data-ttu-id="f0bf3-125">Mozilla Firefox</span><span class="sxs-lookup"><span data-stu-id="f0bf3-125">Mozilla Firefox</span></span>| <span data-ttu-id="f0bf3-126">38</span><span class="sxs-lookup"><span data-stu-id="f0bf3-126">38</span></span>|
|<span data-ttu-id="f0bf3-127">Opera</span><span class="sxs-lookup"><span data-stu-id="f0bf3-127">Opera</span></span>| <span data-ttu-id="f0bf3-128">32</span><span class="sxs-lookup"><span data-stu-id="f0bf3-128">32</span></span>|
|<span data-ttu-id="f0bf3-129">Safari</span><span class="sxs-lookup"><span data-stu-id="f0bf3-129">Safari</span></span>| <span data-ttu-id="f0bf3-130">9</span><span class="sxs-lookup"><span data-stu-id="f0bf3-130">9</span></span>|

##<a name="enabling-http2-support-in-azure-cdn"></a><span data-ttu-id="f0bf3-131">啟用 Azure CDN 中的 HTTP/2 支援</span><span class="sxs-lookup"><span data-stu-id="f0bf3-131">Enabling HTTP/2 Support in Azure CDN</span></span>

<span data-ttu-id="f0bf3-132">目前，**Akamai 的 Azure CDN** 和 **Verizon 的 Azure CDN** 設定檔已支援 HTTP/2。</span><span class="sxs-lookup"><span data-stu-id="f0bf3-132">Currently HTTP/2 support is active for **Azure CDN from Akamai** and **Azure CDN from Verizon** profiles.</span></span> <span data-ttu-id="f0bf3-133">客戶不需要採取任何動作。</span><span class="sxs-lookup"><span data-stu-id="f0bf3-133">No further action is required from customers.</span></span>

##<a name="next-steps"></a><span data-ttu-id="f0bf3-134">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f0bf3-134">Next Steps</span></span>

<span data-ttu-id="f0bf3-135">toosee hello 優點 HTTP/2 的動作，請參閱[Akamai 從這個示範](https://http2.akamai.com/demo)。</span><span class="sxs-lookup"><span data-stu-id="f0bf3-135">toosee hello benefits of HTTP/2 in action, see [this demo from Akamai](https://http2.akamai.com/demo).</span></span>

<span data-ttu-id="f0bf3-136">toolearn 深入了解 HTTP/2，請造訪 hello 下列資源：</span><span class="sxs-lookup"><span data-stu-id="f0bf3-136">toolearn more about HTTP/2, visit hello following resources:</span></span>

*   [<span data-ttu-id="f0bf3-137">HTTP/2 規格首頁</span><span class="sxs-lookup"><span data-stu-id="f0bf3-137">HTTP/2 specification homepage</span></span>](https://http2.github.io/)
*   [<span data-ttu-id="f0bf3-138">官方 HTTP/2 常見問題集</span><span class="sxs-lookup"><span data-stu-id="f0bf3-138">Official HTTP/2 FAQ</span></span>](https://http2.github.io/faq/)
*   [<span data-ttu-id="f0bf3-139">Akamai HTTP/2 資訊</span><span class="sxs-lookup"><span data-stu-id="f0bf3-139">Akamai HTTP/2 information</span></span>](https://http2.akamai.com/)

<span data-ttu-id="f0bf3-140">toolearn 進一步了解 Azure CDN 提供的功能，請參閱 hello [Azure CDN 概觀](https://azure.microsoft.com/documentation/articles/cdn-overview/)。</span><span class="sxs-lookup"><span data-stu-id="f0bf3-140">toolearn more about Azure CDN's available features, see hello [Azure CDN Overview](https://azure.microsoft.com/documentation/articles/cdn-overview/).</span></span>
