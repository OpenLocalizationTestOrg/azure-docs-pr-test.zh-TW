---
title: "aaaEnabling 結束 tooend Azure 應用程式閘道上的 SSL |Microsoft 文件"
description: "此頁面提供 SSL 支援 hello 應用程式閘道結束 tooend 的概觀。"
documentationcenter: na
services: application-gateway
author: amsriva
manager: rossort
editor: amsriva
ms.assetid: 3976399b-25ad-45eb-8eb3-fdb736a598c5
ms.service: application-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.custom: H1Hack27Feb2017
ms.workload: infrastructure-services
ms.date: 07/19/2017
ms.author: amsriva
ms.openlocfilehash: c5cb398a1e7d9a08662a3120baad98edb5575917
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-end-tooend-ssl-with-application-gateway"></a><span data-ttu-id="6cde9-103">結束 tooend SSL 與應用程式閘道的概觀</span><span class="sxs-lookup"><span data-stu-id="6cde9-103">Overview of end tooend SSL with Application Gateway</span></span>

<span data-ttu-id="6cde9-104">應用程式閘道支援在 hello 閘道進行 SSL 終止後通常流動的流量加密 toohello 後端伺服器。</span><span class="sxs-lookup"><span data-stu-id="6cde9-104">Application gateway supports SSL termination at hello gateway, after which traffic typically flows unencrypted toohello backend servers.</span></span> <span data-ttu-id="6cde9-105">這項功能可讓 web 伺服器 toobe unburdened 從昂貴加密和解密的額外負荷。</span><span class="sxs-lookup"><span data-stu-id="6cde9-105">This feature allows web servers toobe unburdened from costly encryption and decryption overhead.</span></span> <span data-ttu-id="6cde9-106">但是對某些客戶未加密的通訊 toohello 後端伺服器不是可接受的選項。</span><span class="sxs-lookup"><span data-stu-id="6cde9-106">However for some customers unencrypted communication toohello backend servers is not an acceptable option.</span></span> <span data-ttu-id="6cde9-107">此未加密的通訊可能是因為 toosecurity 需求，相容性需求，或 hello 應用程式可能只接受安全的連線。</span><span class="sxs-lookup"><span data-stu-id="6cde9-107">This unencrypted communication could be due toosecurity requirements, compliance requirements, or hello application may only accept a secure connection.</span></span> <span data-ttu-id="6cde9-108">針對這類應用程式，應用程式閘道支援結束 tooend SSL 加密。</span><span class="sxs-lookup"><span data-stu-id="6cde9-108">For such applications, application gateway supports end tooend SSL encryption.</span></span>

## <a name="overview"></a><span data-ttu-id="6cde9-109">概觀</span><span class="sxs-lookup"><span data-stu-id="6cde9-109">Overview</span></span>

<span data-ttu-id="6cde9-110">結束 tooend SSL 可讓您 toosecurely 傳輸時仍利用 hello 7 層負載平衡功能的優點的應用程式閘道提供加密的敏感性資料 toohello 後端。</span><span class="sxs-lookup"><span data-stu-id="6cde9-110">End tooend SSL allows you toosecurely transmit sensitive data toohello backend encrypted while still taking advantage of hello benefits of Layer 7 load balancing features which application gateway provides.</span></span> <span data-ttu-id="6cde9-111">這其中部分功能會以 cookie 為基礎的工作階段親和性、 URL 為基礎的路由、 支援路由根據站台或能力 tooinject 轉寄-X * 標頭。</span><span class="sxs-lookup"><span data-stu-id="6cde9-111">Some of these features are cookie-based session affinity, URL-based routing, support for routing based on sites, or ability tooinject X-Forwarded-* headers.</span></span>

<span data-ttu-id="6cde9-112">設定為結束 tooend SSL 通訊模式時，應用程式閘道會終止在 hello 閘道 hello SSL 工作階段，並解密使用者流量。</span><span class="sxs-lookup"><span data-stu-id="6cde9-112">When configured with end tooend SSL communication mode, application gateway terminates hello SSL sessions at hello gateway and decrypts user traffic.</span></span> <span data-ttu-id="6cde9-113">然後再套用設定的 hello 規則 tooselect 適當的後端集區執行個體 tooroute 流量。</span><span class="sxs-lookup"><span data-stu-id="6cde9-113">It then applies hello configured rules tooselect an appropriate backend pool instance tooroute traffic to.</span></span> <span data-ttu-id="6cde9-114">應用程式閘道會起始新的 SSL 連接 toohello 後端伺服器，然後重新加密資料前傳送嗨要求 toohello 後端使用 hello 後端伺服器的公開金鑰憑證。</span><span class="sxs-lookup"><span data-stu-id="6cde9-114">Application gateway then initiates a new SSL connection toohello backend server and re-encrypts data using hello backend server's public key certificate before transmitting hello request toohello backend.</span></span> <span data-ttu-id="6cde9-115">結束 tooend BackendHTTPSetting tooHTTPS，接著在將通訊協定設定啟用 SSL 套用 tooa 後端集區。</span><span class="sxs-lookup"><span data-stu-id="6cde9-115">End tooend SSL is enabled by setting protocol setting in BackendHTTPSetting tooHTTPS, which is then applied tooa backend pool.</span></span> <span data-ttu-id="6cde9-116">Hello 與結束 tooend 啟用 SSL 的後端集區中每個後端伺服器必須設定憑證 tooallow 安全通訊。</span><span class="sxs-lookup"><span data-stu-id="6cde9-116">Each backend server in hello backend pool with end tooend SSL enabled must be configured with a certificate tooallow secure communication.</span></span>

![結束 tooend ssl 案例][1]

<span data-ttu-id="6cde9-118">在此範例中，使用 TLS1.2 的要求使用 SSL 的結束 tooend Pool1 中的路由的 toobackend 伺服器。</span><span class="sxs-lookup"><span data-stu-id="6cde9-118">In this example, requests using TLS1.2 are routed toobackend servers in Pool1 using end tooend SSL.</span></span>

## <a name="end-tooend-ssl-and-whitelisting-of-certificates"></a><span data-ttu-id="6cde9-119">結束 tooend SSL 和憑證的允許清單</span><span class="sxs-lookup"><span data-stu-id="6cde9-119">End tooend SSL and whitelisting of certificates</span></span>

<span data-ttu-id="6cde9-120">應用程式閘道只會與 hello 應用程式閘道使用其憑證有在允許清單中的已知的後端執行個體通訊。</span><span class="sxs-lookup"><span data-stu-id="6cde9-120">Application gateway only communicates with known backend instances that have whitelisted their certificate with hello application gateway.</span></span> <span data-ttu-id="6cde9-121">tooenable 允許清單的憑證，您必須上傳 hello 公開金鑰的後端伺服器憑證 toohello 應用程式閘道 （不 hello 根憑證）。</span><span class="sxs-lookup"><span data-stu-id="6cde9-121">tooenable whitelisting of certificates, you must upload hello public key of backend server certificates toohello application gateway (not hello root certificate).</span></span> <span data-ttu-id="6cde9-122">然後允許只有連線 tooknown 和白名單後端。</span><span class="sxs-lookup"><span data-stu-id="6cde9-122">Only connections tooknown and whitelisted backends are then allowed.</span></span> <span data-ttu-id="6cde9-123">hello 剩餘後端會導致閘道時發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="6cde9-123">hello remaining backends results in a gateway error.</span></span> <span data-ttu-id="6cde9-124">自我簽署憑證僅供測試之用，並不建議用於生產工作負載。</span><span class="sxs-lookup"><span data-stu-id="6cde9-124">Self-signed certificates are for test purposes only and not recommended for production workloads.</span></span> <span data-ttu-id="6cde9-125">這類憑證有 toobe 在允許清單與 hello 應用程式閘道 hello 才可以使用先前步驟中所述。</span><span class="sxs-lookup"><span data-stu-id="6cde9-125">Such certificates have toobe whitelisted with hello application gateway as described in hello preceding steps before they can be used.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6cde9-126">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6cde9-126">Next steps</span></span>

<span data-ttu-id="6cde9-127">在了解結束 tooend SSL 之後, 請繼續太[啟用應用程式閘道結束 tooend SSL](application-gateway-end-to-end-ssl-powershell.md) toocreate 應用程式閘道使用結束 tooend SSL。</span><span class="sxs-lookup"><span data-stu-id="6cde9-127">After learning about end tooend SSL, go too[enable end tooend SSL on application gateway](application-gateway-end-to-end-ssl-powershell.md) toocreate an application gateway using end tooend SSL.</span></span>

<!--Image references-->

[1]: ./media/application-gateway-backend-ssl/scenario.png
