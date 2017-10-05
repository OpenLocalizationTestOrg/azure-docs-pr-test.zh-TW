---
title: "在 Azure 應用程式閘道上啟用端對端 SSL | Microsoft Docs"
description: "本頁面提供應用程式閘道端對端 SSL 支援的概觀。"
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
ms.openlocfilehash: 689ee54dc1db2ea371b08270718278fd98c65bb5
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="overview-of-end-to-end-ssl-with-application-gateway"></a><span data-ttu-id="11761-103">應用程式閘道端對端 SSL 的概觀</span><span class="sxs-lookup"><span data-stu-id="11761-103">Overview of end to end SSL with Application Gateway</span></span>

<span data-ttu-id="11761-104">應用程式閘道支援在閘道上終止 SSL，之後流量通常會以未加密狀態流至後端伺服器。</span><span class="sxs-lookup"><span data-stu-id="11761-104">Application gateway supports SSL termination at the gateway, after which traffic typically flows unencrypted to the backend servers.</span></span> <span data-ttu-id="11761-105">這項功能可讓 Web 伺服器不必再負擔昂貴的加密和解密成本。</span><span class="sxs-lookup"><span data-stu-id="11761-105">This feature allows web servers to be unburdened from costly encryption and decryption overhead.</span></span> <span data-ttu-id="11761-106">但對某些客戶來說，對後端伺服器進行未加密的通訊並非可接受的選項。</span><span class="sxs-lookup"><span data-stu-id="11761-106">However for some customers unencrypted communication to the backend servers is not an acceptable option.</span></span> <span data-ttu-id="11761-107">此未加密的通訊可能是有安全性需要、合規性需求，或應用程式可能只接受安全連線。</span><span class="sxs-lookup"><span data-stu-id="11761-107">This unencrypted communication could be due to security requirements, compliance requirements, or the application may only accept a secure connection.</span></span> <span data-ttu-id="11761-108">對於這類應用程式，應用程式閘道可支援端對端 SSL 加密。</span><span class="sxs-lookup"><span data-stu-id="11761-108">For such applications, application gateway supports end to end SSL encryption.</span></span>

## <a name="overview"></a><span data-ttu-id="11761-109">概觀</span><span class="sxs-lookup"><span data-stu-id="11761-109">Overview</span></span>

<span data-ttu-id="11761-110">端對端 SSL 可讓您將機密資料以加密方式安全地傳輸到後端，同時又可利用應用程式閘道提供的第 7 層負載平衡功能的好處。</span><span class="sxs-lookup"><span data-stu-id="11761-110">End to end SSL allows you to securely transmit sensitive data to the backend encrypted while still taking advantage of the benefits of Layer 7 load balancing features which application gateway provides.</span></span> <span data-ttu-id="11761-111">部分功能為 cookie 型工作階段親和性、URL 型路由、支援根據站台或能注入 X-Forwarded-* 標頭的路由。</span><span class="sxs-lookup"><span data-stu-id="11761-111">Some of these features are cookie-based session affinity, URL-based routing, support for routing based on sites, or ability to inject X-Forwarded-* headers.</span></span>

<span data-ttu-id="11761-112">當設定為端對端 SSL 通訊模式時，應用程式閘道會在閘道上終止 SSL 工作階段，並解密使用者流量。</span><span class="sxs-lookup"><span data-stu-id="11761-112">When configured with end to end SSL communication mode, application gateway terminates the SSL sessions at the gateway and decrypts user traffic.</span></span> <span data-ttu-id="11761-113">然後，它會套用所設定的規則來選取要將流量路由傳送到的適當後端集區執行個體。</span><span class="sxs-lookup"><span data-stu-id="11761-113">It then applies the configured rules to select an appropriate backend pool instance to route traffic to.</span></span> <span data-ttu-id="11761-114">應用程式閘道接著再起始連往後端伺服器的新 SSL 連線，並先使　用後端伺服器的公開金鑰憑證重新加密資料，再將要求傳輸至後端。</span><span class="sxs-lookup"><span data-stu-id="11761-114">Application gateway then initiates a new SSL connection to the backend server and re-encrypts data using the backend server's public key certificate before transmitting the request to the backend.</span></span> <span data-ttu-id="11761-115">若要啟用端對端 SSL，請將 BackendHTTPSetting 中的通訊協定設為 HTTPS，接著再套用到後端集區。</span><span class="sxs-lookup"><span data-stu-id="11761-115">End to end SSL is enabled by setting protocol setting in BackendHTTPSetting to HTTPS, which is then applied to a backend pool.</span></span> <span data-ttu-id="11761-116">已啟用端對端 SSL 之後端集區中的每個後端伺服器，都必須設有憑證以便能夠進行安全通訊。</span><span class="sxs-lookup"><span data-stu-id="11761-116">Each backend server in the backend pool with end to end SSL enabled must be configured with a certificate to allow secure communication.</span></span>

![端對端 SSL 案例][1]

<span data-ttu-id="11761-118">在此範例中，使用端對端 SSL，將使用 TLS1.2 的要求路由傳送至 Pool1 中的後端伺服器。</span><span class="sxs-lookup"><span data-stu-id="11761-118">In this example, requests using TLS1.2 are routed to backend servers in Pool1 using end to end SSL.</span></span>

## <a name="end-to-end-ssl-and-whitelisting-of-certificates"></a><span data-ttu-id="11761-119">端對端 SSL 和憑證白名單</span><span class="sxs-lookup"><span data-stu-id="11761-119">End to end SSL and whitelisting of certificates</span></span>

<span data-ttu-id="11761-120">應用程式閘道只會與已知的後端執行個體通訊，後者已將其憑證加入到應用程式閘道的白名單。</span><span class="sxs-lookup"><span data-stu-id="11761-120">Application gateway only communicates with known backend instances that have whitelisted their certificate with the application gateway.</span></span> <span data-ttu-id="11761-121">若要啟用憑證白名單，您必須將後端伺服器憑證的公開金鑰上傳至應用程式閘道 (不是根憑證)。</span><span class="sxs-lookup"><span data-stu-id="11761-121">To enable whitelisting of certificates, you must upload the public key of backend server certificates to the application gateway (not the root certificate).</span></span> <span data-ttu-id="11761-122">於是，只允許連接至已知和白名單中的後端。</span><span class="sxs-lookup"><span data-stu-id="11761-122">Only connections to known and whitelisted backends are then allowed.</span></span> <span data-ttu-id="11761-123">其餘的後端會導致閘道錯誤。</span><span class="sxs-lookup"><span data-stu-id="11761-123">The remaining backends results in a gateway error.</span></span> <span data-ttu-id="11761-124">自我簽署憑證僅供測試之用，並不建議用於生產工作負載。</span><span class="sxs-lookup"><span data-stu-id="11761-124">Self-signed certificates are for test purposes only and not recommended for production workloads.</span></span> <span data-ttu-id="11761-125">這類憑證也必須如先前步驟所述，加入應用程式閘道的白名單之中，才能使用。</span><span class="sxs-lookup"><span data-stu-id="11761-125">Such certificates have to be whitelisted with the application gateway as described in the preceding steps before they can be used.</span></span>

## <a name="next-steps"></a><span data-ttu-id="11761-126">後續步驟</span><span class="sxs-lookup"><span data-stu-id="11761-126">Next steps</span></span>

<span data-ttu-id="11761-127">了解端對端 SSL 後，請移至 [在應用程式閘道上啟用端對端 SSL](application-gateway-end-to-end-ssl-powershell.md)，以使用端對端 SSL 建立應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="11761-127">After learning about end to end SSL, go to [enable end to end SSL on application gateway](application-gateway-end-to-end-ssl-powershell.md) to create an application gateway using end to end SSL.</span></span>

<!--Image references-->

[1]: ./media/application-gateway-backend-ssl/scenario.png
