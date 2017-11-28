---
title: "Azure 應用程式閘道常見問題 aaaFrequently |Microsoft 文件"
description: "此頁面提供的解答 toofrequently 常見問題解答 Azure 應用程式閘道"
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: d54ee7ec-4d6b-4db7-8a17-6513fda7e392
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/19/2017
ms.author: gwallace
ms.openlocfilehash: b2df3a82a71a3264d3d34d317d08e4b4f72c6e3e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-questions-for-application-gateway"></a><span data-ttu-id="eb0b3-103">應用程式閘道的常見問題集</span><span class="sxs-lookup"><span data-stu-id="eb0b3-103">Frequently asked questions for Application Gateway</span></span>

## <a name="general"></a><span data-ttu-id="eb0b3-104">一般</span><span class="sxs-lookup"><span data-stu-id="eb0b3-104">General</span></span>

<span data-ttu-id="eb0b3-105">**問：什麼是應用程式閘道？**</span><span class="sxs-lookup"><span data-stu-id="eb0b3-105">**Q. What is Application Gateway?**</span></span>

<span data-ttu-id="eb0b3-106">Azure 應用程式閘道是服務形式的應用程式傳遞控制器 (ADC)，可為您的應用程式提供各種第 7 層負載平衡功能。</span><span class="sxs-lookup"><span data-stu-id="eb0b3-106">Azure Application Gateway is an Application Delivery Controller (ADC) as a service, offering various layer 7 load balancing capabilities for your applications.</span></span> <span data-ttu-id="eb0b3-107">它提供高度可用並可調整的服務，這完全由 Azure 管理。</span><span class="sxs-lookup"><span data-stu-id="eb0b3-107">It offers highly available and scalable service, which is fully managed by Azure.</span></span>

<span data-ttu-id="eb0b3-108">**問：應用程式閘道支援哪些功能？**</span><span class="sxs-lookup"><span data-stu-id="eb0b3-108">**Q. What features does Application Gateway support?**</span></span>

<span data-ttu-id="eb0b3-109">應用程式閘道支援 SSL 卸載和結束 tooend SSL、 Web 應用程式防火牆、 cookie 架構工作階段親和性、 url 路徑架構路由、 多站台裝載和其他人。</span><span class="sxs-lookup"><span data-stu-id="eb0b3-109">Application Gateway supports SSL offloading and end tooend SSL, Web Application Firewall, cookie-based session affinity, url path-based routing, multi site hosting, and others.</span></span> <span data-ttu-id="eb0b3-110">如需支援功能的完整清單，請瀏覽[簡介 tooApplication 閘道](application-gateway-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="eb0b3-110">For a full list of supported features, visit [Introduction tooApplication Gateway](application-gateway-introduction.md)</span></span>

<span data-ttu-id="eb0b3-111">**問：Hello 應用程式閘道與 Azure 負載平衡器之間的差異為何？**</span><span class="sxs-lookup"><span data-stu-id="eb0b3-111">**Q. What is hello difference between Application Gateway and Azure Load Balancer?**</span></span>

<span data-ttu-id="eb0b3-112">應用程式閘道是第 7 層負載平衡器，這表示它只會使用網路流量 (HTTP/HTTPS/WebSocket)。</span><span class="sxs-lookup"><span data-stu-id="eb0b3-112">Application Gateway is a layer 7 load balancer, which means it works with web traffic only (HTTP/HTTPS/WebSocket).</span></span> <span data-ttu-id="eb0b3-113">它支援功能，例如 SSL 終止、以 cookie 為基礎的工作階段親和性，以及用於平衡流量負載的循環配置資源。</span><span class="sxs-lookup"><span data-stu-id="eb0b3-113">It supports capabilities such as SSL termination, cookie-based session affinity, and round robin for load balancing traffic.</span></span> <span data-ttu-id="eb0b3-114">負載平衡器，平衡第 4 層 (TCP/UDP) 的流量負載。</span><span class="sxs-lookup"><span data-stu-id="eb0b3-114">Load Balancer, load balances traffic at layer 4 (TCP/UDP).</span></span>

<span data-ttu-id="eb0b3-115">**問：應用程式閘道支援哪些通訊協定？**</span><span class="sxs-lookup"><span data-stu-id="eb0b3-115">**Q. What protocols does Application Gateway support?**</span></span>

<span data-ttu-id="eb0b3-116">Azure 應用程式閘道支援 HTTP、HTTPS 和 WebSocket。</span><span class="sxs-lookup"><span data-stu-id="eb0b3-116">Application Gateway supports HTTP, HTTPS, and WebSocket.</span></span>

<span data-ttu-id="eb0b3-117">**問：目前支援哪些資源做為後端集區的一部分？**</span><span class="sxs-lookup"><span data-stu-id="eb0b3-117">**Q. What resources are supported today as part of backend pool?**</span></span>

<span data-ttu-id="eb0b3-118">後端集區可以包含 NIC、虛擬機器擴展集、公用 IP、內部 IP、完整的網域名稱 (FQDN)，以及如 Azure Web 應用程式的多租用戶後端。</span><span class="sxs-lookup"><span data-stu-id="eb0b3-118">Backend pools can be composed of NICs, virtual machine scale sets, public IPs, internal IPs, fully qualified domain names (FQDN), and multi-tenant back-ends like Azure Web Apps.</span></span> <span data-ttu-id="eb0b3-119">應用程式閘道後端集區成員不會繫結 tooan 可用性設定組。</span><span class="sxs-lookup"><span data-stu-id="eb0b3-119">Application Gateway backend pool members are not tied tooan availability set.</span></span> <span data-ttu-id="eb0b3-120">只要後端集區成員具有 IP 連線能力，就可以跨越叢集、資料中心或在 Azure 外部。</span><span class="sxs-lookup"><span data-stu-id="eb0b3-120">Members of backend pools can be across clusters, data centers, or outside of Azure as long as they have IP connectivity.</span></span>

<span data-ttu-id="eb0b3-121">**問：哪些區域位於 hello 服務？**</span><span class="sxs-lookup"><span data-stu-id="eb0b3-121">**Q. What regions is hello service available in?**</span></span>

<span data-ttu-id="eb0b3-122">應用程式閘道適用於全域 Azure 的所有區域。</span><span class="sxs-lookup"><span data-stu-id="eb0b3-122">Application Gateway is available in all regions of global Azure.</span></span> <span data-ttu-id="eb0b3-123">它也適用於 [Azure China](https://www.azure.cn/) 和 [Azure Government](https://azure.microsoft.com/en-us/overview/clouds/government/)</span><span class="sxs-lookup"><span data-stu-id="eb0b3-123">It is also available in [Azure China](https://www.azure.cn/) and [Azure Government](https://azure.microsoft.com/en-us/overview/clouds/government/)</span></span>

<span data-ttu-id="eb0b3-124">**問：這是我的訂用帳戶專用的部署，還是所有客戶共用？**</span><span class="sxs-lookup"><span data-stu-id="eb0b3-124">**Q. Is this a dedicated deployment for my subscription or is it shared across customers?**</span></span>

<span data-ttu-id="eb0b3-125">應用程式閘道是您虛擬網路中專用的部署。</span><span class="sxs-lookup"><span data-stu-id="eb0b3-125">Application Gateway is a dedicated deployment in your virtual network.</span></span>

<span data-ttu-id="eb0b3-126">**問：是否支援 HTTP->HTTPS 重新導向？**</span><span class="sxs-lookup"><span data-stu-id="eb0b3-126">**Q. Is HTTP->HTTPS redirection supported?**</span></span>

<span data-ttu-id="eb0b3-127">支援重新導向。</span><span class="sxs-lookup"><span data-stu-id="eb0b3-127">Redirection is supported.</span></span> <span data-ttu-id="eb0b3-128">請瀏覽[應用程式閘道重新導向概觀](application-gateway-redirect-overview.md)toolearn 更多。</span><span class="sxs-lookup"><span data-stu-id="eb0b3-128">Visit [Application Gateway redirect overview](application-gateway-redirect-overview.md) toolearn more.</span></span>

<span data-ttu-id="eb0b3-129">**問：接聽程式的處理順序為何？**</span><span class="sxs-lookup"><span data-stu-id="eb0b3-129">**Q. In what order are listeners processed?**</span></span>

<span data-ttu-id="eb0b3-130">接聽程式的處理順序 hello 它們會顯示。</span><span class="sxs-lookup"><span data-stu-id="eb0b3-130">Listeners are processed in hello order they are shown.</span></span> <span data-ttu-id="eb0b3-131">因此，如果基本接聽程式符合傳入的要求，就會先處理它。</span><span class="sxs-lookup"><span data-stu-id="eb0b3-131">For that reason if a basic listener matches an incoming request it processes it first.</span></span>  <span data-ttu-id="eb0b3-132">基本的接聽程式 tooensure 流量路由的 toohello 正確後端之前，應該設定多站台接聽程式。</span><span class="sxs-lookup"><span data-stu-id="eb0b3-132">Multi-site listeners should be configured before a basic listener tooensure traffic is routed toohello correct back-end.</span></span>

<span data-ttu-id="eb0b3-133">**問：哪裡可找到應用程式閘道的 IP 和 DNS？**</span><span class="sxs-lookup"><span data-stu-id="eb0b3-133">**Q. Where do I find Application Gateway’s IP and DNS?**</span></span>

<span data-ttu-id="eb0b3-134">時使用的公用 IP 位址做為端點，這項資訊可以 hello 入口網站中的 hello 應用程式閘道 hello 公用 IP 位址資源或 hello 概觀 頁面上找到。</span><span class="sxs-lookup"><span data-stu-id="eb0b3-134">When using a public IP address as an endpoint, this information can be found on hello public IP address resource or on hello Overview page for hello Application Gateway in hello portal.</span></span> <span data-ttu-id="eb0b3-135">內部 IP 位址，這可以找到 hello 概觀 頁面上。</span><span class="sxs-lookup"><span data-stu-id="eb0b3-135">For internal IP addresses, this can be found on hello Overview page.</span></span>

<span data-ttu-id="eb0b3-136">**問：沒有 hello IP 或 DNS 變更 hello 存留期的 hello 應用程式閘道嗎？**</span><span class="sxs-lookup"><span data-stu-id="eb0b3-136">**Q. Does hello IP or DNS change over hello lifetime of hello Application Gateway?**</span></span>

<span data-ttu-id="eb0b3-137">如果 hello 閘道就會停止並啟動 hello 客戶，可以變更 hello VIP。</span><span class="sxs-lookup"><span data-stu-id="eb0b3-137">hello VIP can change if hello gateway is stopped and started by hello customer.</span></span> <span data-ttu-id="eb0b3-138">hello 與應用程式閘道相關聯的 DNS 不會變更在 hello 生命週期的 hello 閘道。</span><span class="sxs-lookup"><span data-stu-id="eb0b3-138">hello DNS associated with Application Gateway does not change over hello lifecycle of hello gateway.</span></span> <span data-ttu-id="eb0b3-139">基於這個理由，是建議 toouse CNAME 別名，而且它指向 hello 應用程式閘道 toohello DNS 位址。</span><span class="sxs-lookup"><span data-stu-id="eb0b3-139">For this reason, it is recommended toouse a CNAME alias and point it toohello DNS address of hello Application Gateway.</span></span>

<span data-ttu-id="eb0b3-140">**問：應用程式閘道是否支援靜態 IP？**</span><span class="sxs-lookup"><span data-stu-id="eb0b3-140">**Q. Does Application Gateway support static IP?**</span></span>

<span data-ttu-id="eb0b3-141">否，應用程式閘道不支援靜態公用 IP 位址，但是支援靜態內部 IP。</span><span class="sxs-lookup"><span data-stu-id="eb0b3-141">No, Application Gateway does not support static public IP addresses, but it does support static internal IPs.</span></span>

<span data-ttu-id="eb0b3-142">**問：應用程式閘道支援在多個公用 Ip 上 hello 閘道嗎？**</span><span class="sxs-lookup"><span data-stu-id="eb0b3-142">**Q. Does Application Gateway support multiple public IPs on hello gateway?**</span></span>

<span data-ttu-id="eb0b3-143">應用程式閘道只支援一個公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="eb0b3-143">Only one public IP address is supported on an Application Gateway.</span></span>

<span data-ttu-id="eb0b3-144">**問：應用程式閘道是否支援 x-forwarded-for 標頭？**</span><span class="sxs-lookup"><span data-stu-id="eb0b3-144">**Q. Does Application Gateway support x-forwarded-for headers?**</span></span>

<span data-ttu-id="eb0b3-145">是，應用程式閘道插入 x 轉送如，x-轉送-通訊協定，且 x 轉送埠 hello 要求標頭轉送 toohello 後端。</span><span class="sxs-lookup"><span data-stu-id="eb0b3-145">Yes, Application Gateway inserts x-forwarded-for, x-forwarded-proto, and x-forwarded-port headers into hello request forwarded toohello backend.</span></span> <span data-ttu-id="eb0b3-146">x 轉送的標頭的 hello 格式是 IP:Port 的逗號分隔清單。</span><span class="sxs-lookup"><span data-stu-id="eb0b3-146">hello format for x-forwarded-for header is a comma-separated list of IP:Port.</span></span> <span data-ttu-id="eb0b3-147">hello x 轉送 proto 有效值為 http 或 https。</span><span class="sxs-lookup"><span data-stu-id="eb0b3-147">hello valid values for x-forwarded-proto are http or https.</span></span> <span data-ttu-id="eb0b3-148">X 轉送埠指定 hello 達 hello 應用程式閘道的 hello 要求連接埠。</span><span class="sxs-lookup"><span data-stu-id="eb0b3-148">X-forwarded-port specifies hello port at which hello request reached at hello Application Gateway.</span></span>

<span data-ttu-id="eb0b3-149">**問：多久花費 toodeploy 應用程式閘道？進行更新時，我的應用程式閘道是否仍有作用？**</span><span class="sxs-lookup"><span data-stu-id="eb0b3-149">**Q. How long does it take toodeploy an Application Gateway? Does my Application Gateway still work when being updated?**</span></span>

<span data-ttu-id="eb0b3-150">新的應用程式閘道部署可能會佔用 too20 分鐘 tooprovision。</span><span class="sxs-lookup"><span data-stu-id="eb0b3-150">New Application Gateway deployments can take up too20 minutes tooprovision.</span></span> <span data-ttu-id="eb0b3-151">變更 tooinstance 大小/計數不會干擾性，而且 hello 閘道會在這段期間保持使用中。</span><span class="sxs-lookup"><span data-stu-id="eb0b3-151">Changes tooinstance size/count are not disruptive, and hello gateway remains active during this time.</span></span>

## <a name="configuration"></a><span data-ttu-id="eb0b3-152">組態</span><span class="sxs-lookup"><span data-stu-id="eb0b3-152">Configuration</span></span>

<span data-ttu-id="eb0b3-153">**問：應用程式閘道一律部署在虛擬網路中？**</span><span class="sxs-lookup"><span data-stu-id="eb0b3-153">**Q. Is Application Gateway always deployed in a virtual network?**</span></span>

<span data-ttu-id="eb0b3-154">是，應用程式閘道一律部署在虛擬網路子網路中。</span><span class="sxs-lookup"><span data-stu-id="eb0b3-154">Yes, Application Gateway is always deployed in a virtual network subnet.</span></span> <span data-ttu-id="eb0b3-155">這個子網路只包含應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="eb0b3-155">This subnet can only contain Application Gateways.</span></span>

<span data-ttu-id="eb0b3-156">**問：應用程式閘道可以討論其虛擬網路外的 tooinstances 嗎？**</span><span class="sxs-lookup"><span data-stu-id="eb0b3-156">**Q. Can Application Gateway talk tooinstances outside its virtual network?**</span></span>

<span data-ttu-id="eb0b3-157">應用程式閘道可以與 tooinstances hello 處於只要 IP 連線的虛擬網路外部通訊。</span><span class="sxs-lookup"><span data-stu-id="eb0b3-157">Application Gateway can talk tooinstances outside of hello virtual network that it is in as long as there is IP connectivity.</span></span> <span data-ttu-id="eb0b3-158">如果您計劃 toouse 內部 Ip 後端集區的成員，則需要[對等互連的 VNET](../virtual-network/virtual-network-peering-overview.md)或[VPN 閘道](../vpn-gateway/vpn-gateway-about-vpngateways.md)。</span><span class="sxs-lookup"><span data-stu-id="eb0b3-158">If you plan toouse internal IPs as backend pool members, then it requires [VNET Peering](../virtual-network/virtual-network-peering-overview.md) or [VPN Gateway](../vpn-gateway/vpn-gateway-about-vpngateways.md).</span></span>

<span data-ttu-id="eb0b3-159">**問：我可以部署 hello 應用程式閘道子網路中的其他任何項目嗎？**</span><span class="sxs-lookup"><span data-stu-id="eb0b3-159">**Q. Can I deploy anything else in hello Application Gateway subnet?**</span></span>

<span data-ttu-id="eb0b3-160">否，但您可以部署 hello 子網路中的其他應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="eb0b3-160">No, but you can deploy other application gateways in hello subnet.</span></span>

<span data-ttu-id="eb0b3-161">**問：為支援 hello 應用程式閘道子網路上的網路安全性群組？**</span><span class="sxs-lookup"><span data-stu-id="eb0b3-161">**Q. Are Network Security Groups supported on hello Application Gateway subnet?**</span></span>

<span data-ttu-id="eb0b3-162">Hello 應用程式閘道子網路都支援網路安全性群組以 hello 下列限制：</span><span class="sxs-lookup"><span data-stu-id="eb0b3-162">Network Security Groups are supported on hello Application Gateway subnet with hello following restrictions:</span></span>

* <span data-ttu-id="eb0b3-163">例外狀況必須放在連入流量的連接埠 65503 65534 的後端健全狀況 toowork 正確。</span><span class="sxs-lookup"><span data-stu-id="eb0b3-163">Exceptions must be put in for incoming traffic on ports 65503-65534 for backend health toowork correctly.</span></span>

* <span data-ttu-id="eb0b3-164">不會封鎖輸出網際網路連線。</span><span class="sxs-lookup"><span data-stu-id="eb0b3-164">Outbound internet connectivity can not be blocked.</span></span>

* <span data-ttu-id="eb0b3-165">必須允許從 hello AzureLoadBalancer 標記的流量。</span><span class="sxs-lookup"><span data-stu-id="eb0b3-165">Traffic from hello AzureLoadBalancer tag must be allowed.</span></span>

<span data-ttu-id="eb0b3-166">**問：Hello 限制應用程式閘道有哪些？是否可以增加這些限制？**</span><span class="sxs-lookup"><span data-stu-id="eb0b3-166">**Q. What are hello limits on Application Gateway? Can I increase these limits?**</span></span>

<span data-ttu-id="eb0b3-167">請瀏覽[應用程式閘道限制](../azure-subscription-service-limits.md#application-gateway-limits)tooview hello 限制。</span><span class="sxs-lookup"><span data-stu-id="eb0b3-167">Visit [Application Gateway Limits](../azure-subscription-service-limits.md#application-gateway-limits) tooview hello limits.</span></span>

<span data-ttu-id="eb0b3-168">**問：是否可以同時對外部和內部流量使用應用程式閘道？**</span><span class="sxs-lookup"><span data-stu-id="eb0b3-168">**Q. Can I use Application Gateway for both external and internal traffic simultaneously?**</span></span>

<span data-ttu-id="eb0b3-169">是，應用程式閘道支援每個應用程式閘道擁有具有一個內部 IP 和一個外部 IP。</span><span class="sxs-lookup"><span data-stu-id="eb0b3-169">Yes, Application Gateway supports having one internal IP and one external IP per Application Gateway.</span></span>

<span data-ttu-id="eb0b3-170">**問：是否支援 VNet 對等互連？**</span><span class="sxs-lookup"><span data-stu-id="eb0b3-170">**Q. Is VNet peering supported?**</span></span>

<span data-ttu-id="eb0b3-171">是，支援 VNet 對等互連，這對於平衡其他虛擬網路中的流量負載很有幫助。</span><span class="sxs-lookup"><span data-stu-id="eb0b3-171">Yes, VNet peering is supported and is beneficial for load balancing traffic in other virtual networks.</span></span>

<span data-ttu-id="eb0b3-172">**問：當他們透過 ExpressRoute 或 VPN 通道連接時可以說話 tooon 內部部署伺服器嗎？**</span><span class="sxs-lookup"><span data-stu-id="eb0b3-172">**Q. Can I talk tooon-premises servers when they are connected by ExpressRoute or VPN tunnels?**</span></span>

<span data-ttu-id="eb0b3-173">是，只有流量允許即可。</span><span class="sxs-lookup"><span data-stu-id="eb0b3-173">Yes, as long as traffic is allowed.</span></span>

<span data-ttu-id="eb0b3-174">**問：是否可有一個為不同連接埠上的許多應用程式提供服務的後端集區？**</span><span class="sxs-lookup"><span data-stu-id="eb0b3-174">**Q. Can I have one backend pool serving many applications on different ports?**</span></span>

<span data-ttu-id="eb0b3-175">支援微服務架構。</span><span class="sxs-lookup"><span data-stu-id="eb0b3-175">Micro service architecture is supported.</span></span> <span data-ttu-id="eb0b3-176">您必須在不同的連接埠上的多個 http 設定 tooprobe。</span><span class="sxs-lookup"><span data-stu-id="eb0b3-176">You would need multiple http settings configured tooprobe on different ports.</span></span>

<span data-ttu-id="eb0b3-177">**問：自訂探查是否支援回應資料使用萬用字元/regex？**</span><span class="sxs-lookup"><span data-stu-id="eb0b3-177">**Q. Do custom probes support wildcards/regex on response data?**</span></span>

<span data-ttu-id="eb0b3-178">自訂探查不支援回應資料使用萬用字元或 regex。</span><span class="sxs-lookup"><span data-stu-id="eb0b3-178">Custom probes do not support wildcard or regex on response data.</span></span> 

<span data-ttu-id="eb0b3-179">**問：規則的處理方式為何？**</span><span class="sxs-lookup"><span data-stu-id="eb0b3-179">**Q. How are rules processed?**</span></span>

<span data-ttu-id="eb0b3-180">規則的處理順序 hello 設定。</span><span class="sxs-lookup"><span data-stu-id="eb0b3-180">Rules are processed in hello order they are configured.</span></span> <span data-ttu-id="eb0b3-181">建議先流量的基本規則 tooreduce hello 機率為 hello 的基本規則將會比對所評估的連接埠先前 toohello 多站台規則為基礎的流量路由傳送 toohello 不適當的後端設定的多站台規則。</span><span class="sxs-lookup"><span data-stu-id="eb0b3-181">It is recommended that multi-site rules are configured before basic rules tooreduce hello chance that traffic is routed toohello inappropriate backend as hello basic rule would match traffic based on port prior toohello multi-site rule being evaluated.</span></span>

<span data-ttu-id="eb0b3-182">**問：規則的處理方式為何？**</span><span class="sxs-lookup"><span data-stu-id="eb0b3-182">**Q. How are rules processed?**</span></span>

<span data-ttu-id="eb0b3-183">規則的處理順序 hello 建立。</span><span class="sxs-lookup"><span data-stu-id="eb0b3-183">Rules are processed in hello order they are created.</span></span> <span data-ttu-id="eb0b3-184">建議在基本規則前面設定多網站規則。</span><span class="sxs-lookup"><span data-stu-id="eb0b3-184">It is recommended that multi-site rules are configured before basic rules.</span></span> <span data-ttu-id="eb0b3-185">藉由第一次設定多站台接聽程式，此組態可以減少流量是路由的 toohello 不適當的後端的 hello 機會。</span><span class="sxs-lookup"><span data-stu-id="eb0b3-185">By configuring multi-site listeners first, this configuration reduces hello chance that traffic is routed toohello inappropriate backend.</span></span> <span data-ttu-id="eb0b3-186">此路由問題可能是因為 hello 的基本規則將會比對所評估的連接埠先前 toohello 多站台規則為基礎的流量。</span><span class="sxs-lookup"><span data-stu-id="eb0b3-186">This routing issue can occur as hello basic rule would match traffic based on port prior toohello multi-site rule being evaluated.</span></span>

<span data-ttu-id="eb0b3-187">**問：自訂探查 hello [主機] 欄位代表什麼？**</span><span class="sxs-lookup"><span data-stu-id="eb0b3-187">**Q. What does hello Host field for custom probes signify?**</span></span>

<span data-ttu-id="eb0b3-188">主機 欄位指定用於 hello 名稱 toosend hello 探查。</span><span class="sxs-lookup"><span data-stu-id="eb0b3-188">Host field specifies hello name toosend hello probe to.</span></span> <span data-ttu-id="eb0b3-189">只有當應用程式閘道上設定多站台時適用，否則請使用 '127.0.0.1'。</span><span class="sxs-lookup"><span data-stu-id="eb0b3-189">Applicable only when multi-site is configured on Application Gateway, otherwise use '127.0.0.1'.</span></span> <span data-ttu-id="eb0b3-190">此值與 VM 主機名稱不同，其格式為 \<protocol\>://\<host\>:\<port\>\<path\>。</span><span class="sxs-lookup"><span data-stu-id="eb0b3-190">This value is different from VM host name and is in format \<protocol\>://\<host\>:\<port\>\<path\>.</span></span>

<span data-ttu-id="eb0b3-191">**問：我可以白名單應用程式閘道存取 tooa 少來源 Ip？**</span><span class="sxs-lookup"><span data-stu-id="eb0b3-191">**Q. Can I whitelist Application Gateway access tooa few source IPs?**</span></span>

<span data-ttu-id="eb0b3-192">使用應用程式閘道子網路上的 NSG 可以完成此案例。</span><span class="sxs-lookup"><span data-stu-id="eb0b3-192">This scenario can be done using NSGs on Application Gateway subnet.</span></span> <span data-ttu-id="eb0b3-193">依優先順序列出 hello hello 子網路上應 hello 下列限制：</span><span class="sxs-lookup"><span data-stu-id="eb0b3-193">hello following restrictions should be put on hello subnet in hello listed order of priority:</span></span>

* <span data-ttu-id="eb0b3-194">允許來源 IP/IP 範圍的傳入流量。</span><span class="sxs-lookup"><span data-stu-id="eb0b3-194">Allow incoming traffic from source IP/IP range.</span></span>

* <span data-ttu-id="eb0b3-195">允許來自所有來源 tooports 65503 65534 的連入要求[後端健全狀況通訊](application-gateway-diagnostics.md)。</span><span class="sxs-lookup"><span data-stu-id="eb0b3-195">Allow incoming requests from all sources tooports 65503-65534 for [backend health communication](application-gateway-diagnostics.md).</span></span>

* <span data-ttu-id="eb0b3-196">允許連入的 Azure 負載平衡器探查 （AzureLoadBalancer 標籤），輸入虛擬網路流量 （VirtualNetwork 標籤） 上 hello [NSG](../virtual-network/virtual-networks-nsg.md)。</span><span class="sxs-lookup"><span data-stu-id="eb0b3-196">Allow incoming Azure Load Balancer probes (AzureLoadBalancer tag) and inbound virtual network traffic (VirtualNetwork tag) on hello [NSG](../virtual-network/virtual-networks-nsg.md).</span></span>

* <span data-ttu-id="eb0b3-197">使用「全部拒絕」規則封鎖所有其他傳入流量。</span><span class="sxs-lookup"><span data-stu-id="eb0b3-197">Block all other incoming traffic with a Deny all rule.</span></span>

* <span data-ttu-id="eb0b3-198">允許輸出流量 toohello 所有目的地的網際網路。</span><span class="sxs-lookup"><span data-stu-id="eb0b3-198">Allow outbound traffic toohello internet for all destinations.</span></span>

## <a name="performance"></a><span data-ttu-id="eb0b3-199">效能</span><span class="sxs-lookup"><span data-stu-id="eb0b3-199">Performance</span></span>

<span data-ttu-id="eb0b3-200">**問：應用程式閘道如何支援高可用性和延展性？**</span><span class="sxs-lookup"><span data-stu-id="eb0b3-200">**Q. How does Application Gateway support high availability and scalability?**</span></span>

<span data-ttu-id="eb0b3-201">如果您已部署 2 個以上的執行個體，應用程式閘道即可支援高可用性案例。</span><span class="sxs-lookup"><span data-stu-id="eb0b3-201">Application Gateway supports high availability scenarios when you have two or more instances deployed.</span></span> <span data-ttu-id="eb0b3-202">Azure 會將這些執行個體分散到所有執行個體不會在 hello 失敗的更新和錯誤網域 tooensure 相同的時間。</span><span class="sxs-lookup"><span data-stu-id="eb0b3-202">Azure distributes these instances across update and fault domains tooensure that all instances do not fail at hello same time.</span></span> <span data-ttu-id="eb0b3-203">應用程式閘道支援延展性 hello 多個執行個體加入相同的閘道 tooshare hello 負載。</span><span class="sxs-lookup"><span data-stu-id="eb0b3-203">Application Gateway supports scalability by adding multiple instances of hello same gateway tooshare hello load.</span></span>

<span data-ttu-id="eb0b3-204">**問：如何利用應用程式閘道跨越資料中心封存 DR 案例？**</span><span class="sxs-lookup"><span data-stu-id="eb0b3-204">**Q. How do I achieve DR scenario across data centers with Application Gateway?**</span></span>

<span data-ttu-id="eb0b3-205">客戶可以使用 Traffic Manager toodistribute 流量，跨不同資料中心內的多個應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="eb0b3-205">Customers can use Traffic Manager toodistribute traffic across multiple Application Gateways in different datacenters.</span></span>

<span data-ttu-id="eb0b3-206">**問：是否支援自動調整大小？**</span><span class="sxs-lookup"><span data-stu-id="eb0b3-206">**Q. Is auto scaling supported?**</span></span>

<span data-ttu-id="eb0b3-207">否，但應用程式閘道有可能是使用的 tooalert 輸送量度量達到臨界值時。</span><span class="sxs-lookup"><span data-stu-id="eb0b3-207">No, but Application Gateway has a throughput metric that can be used tooalert you when a threshold is reached.</span></span> <span data-ttu-id="eb0b3-208">手動新增執行個體，或變更大小不會重新啟動 hello 閘道，並不會影響現有的流量。</span><span class="sxs-lookup"><span data-stu-id="eb0b3-208">Manually adding instances or changing size does not restart hello gateway and does not impact existing traffic.</span></span>

<span data-ttu-id="eb0b3-209">**問：手動相應增加/相應減少會造成停機嗎？**</span><span class="sxs-lookup"><span data-stu-id="eb0b3-209">**Q. Does manual scale up/down cause downtime?**</span></span>

<span data-ttu-id="eb0b3-210">不會停機，執行個體已分散於升級網域和容錯網域。</span><span class="sxs-lookup"><span data-stu-id="eb0b3-210">There is no downtime, instances are distributed across upgrade domains and fault domains.</span></span>

<span data-ttu-id="eb0b3-211">**問：可以變更執行個體大小而不中斷的中型 toolarge 從嗎？**</span><span class="sxs-lookup"><span data-stu-id="eb0b3-211">**Q. Can I change instance size from medium toolarge without disruption?**</span></span>

<span data-ttu-id="eb0b3-212">是，Azure 將執行個體分散到所有執行個體不會在 hello 失敗的更新和錯誤網域 tooensure 相同的時間。</span><span class="sxs-lookup"><span data-stu-id="eb0b3-212">Yes, Azure distributes instances across update and fault domains tooensure that all instances do not fail at hello same time.</span></span> <span data-ttu-id="eb0b3-213">藉由新增多個執行個體調整應用程式閘道支援 hello 相同閘道 tooshare hello 負載。</span><span class="sxs-lookup"><span data-stu-id="eb0b3-213">Application Gateway supports scaling by adding multiple instances of hello same gateway tooshare hello load.</span></span>

## <a name="ssl-configuration"></a><span data-ttu-id="eb0b3-214">SSL 組態</span><span class="sxs-lookup"><span data-stu-id="eb0b3-214">SSL Configuration</span></span>

<span data-ttu-id="eb0b3-215">**問：應用程式閘道支援哪些憑證？**</span><span class="sxs-lookup"><span data-stu-id="eb0b3-215">**Q. What certificates are supported on Application Gateway?**</span></span>

<span data-ttu-id="eb0b3-216">支援自我簽署憑證、CA 憑證和萬用字元憑證。</span><span class="sxs-lookup"><span data-stu-id="eb0b3-216">Self signed certs, CA certs, and wild-card certs are supported.</span></span> <span data-ttu-id="eb0b3-217">不支援 EV 憑證。</span><span class="sxs-lookup"><span data-stu-id="eb0b3-217">EV certs are not supported.</span></span>

<span data-ttu-id="eb0b3-218">**問：Hello 目前的加密套件支援的應用程式閘道有哪些？**</span><span class="sxs-lookup"><span data-stu-id="eb0b3-218">**Q. What are hello current cipher suites supported by Application Gateway?**</span></span>

<span data-ttu-id="eb0b3-219">hello 下面是 hello 應用程式閘道支援目前的加密套件。</span><span class="sxs-lookup"><span data-stu-id="eb0b3-219">hello following are hello current cipher suites supported by application gateway.</span></span> <span data-ttu-id="eb0b3-220">請造訪：[設定 SSL 的原則版本和應用程式閘道上的加密套件](application-gateway-configure-ssl-policy-powershell.md)toolearn 如何 toocustomize SSL 選項。</span><span class="sxs-lookup"><span data-stu-id="eb0b3-220">Visit: [Configure SSL policy versions and cipher suites on Application Gateway](application-gateway-configure-ssl-policy-powershell.md) toolearn how toocustomize SSL options.</span></span>

- <span data-ttu-id="eb0b3-221">TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384</span><span class="sxs-lookup"><span data-stu-id="eb0b3-221">TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384</span></span>
- <span data-ttu-id="eb0b3-222">TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256</span><span class="sxs-lookup"><span data-stu-id="eb0b3-222">TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256</span></span>
- <span data-ttu-id="eb0b3-223">TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="eb0b3-223">TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA</span></span>
- <span data-ttu-id="eb0b3-224">TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="eb0b3-224">TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA</span></span>
- <span data-ttu-id="eb0b3-225">TLS_DHE_RSA_WITH_AES_256_GCM_SHA384</span><span class="sxs-lookup"><span data-stu-id="eb0b3-225">TLS_DHE_RSA_WITH_AES_256_GCM_SHA384</span></span>
- <span data-ttu-id="eb0b3-226">TLS_DHE_RSA_WITH_AES_128_GCM_SHA256</span><span class="sxs-lookup"><span data-stu-id="eb0b3-226">TLS_DHE_RSA_WITH_AES_128_GCM_SHA256</span></span>
- <span data-ttu-id="eb0b3-227">TLS_DHE_RSA_WITH_AES_256_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="eb0b3-227">TLS_DHE_RSA_WITH_AES_256_CBC_SHA</span></span>
- <span data-ttu-id="eb0b3-228">TLS_DHE_RSA_WITH_AES_128_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="eb0b3-228">TLS_DHE_RSA_WITH_AES_128_CBC_SHA</span></span>
- <span data-ttu-id="eb0b3-229">TLS_RSA_WITH_AES_256_GCM_SHA384</span><span class="sxs-lookup"><span data-stu-id="eb0b3-229">TLS_RSA_WITH_AES_256_GCM_SHA384</span></span>
- <span data-ttu-id="eb0b3-230">TLS_RSA_WITH_AES_128_GCM_SHA256</span><span class="sxs-lookup"><span data-stu-id="eb0b3-230">TLS_RSA_WITH_AES_128_GCM_SHA256</span></span>
- <span data-ttu-id="eb0b3-231">TLS_RSA_WITH_AES_256_CBC_SHA256</span><span class="sxs-lookup"><span data-stu-id="eb0b3-231">TLS_RSA_WITH_AES_256_CBC_SHA256</span></span>
- <span data-ttu-id="eb0b3-232">TLS_RSA_WITH_AES_128_CBC_SHA256</span><span class="sxs-lookup"><span data-stu-id="eb0b3-232">TLS_RSA_WITH_AES_128_CBC_SHA256</span></span>
- <span data-ttu-id="eb0b3-233">TLS_RSA_WITH_AES_256_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="eb0b3-233">TLS_RSA_WITH_AES_256_CBC_SHA</span></span>
- <span data-ttu-id="eb0b3-234">TLS_RSA_WITH_AES_128_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="eb0b3-234">TLS_RSA_WITH_AES_128_CBC_SHA</span></span>
- <span data-ttu-id="eb0b3-235">TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384</span><span class="sxs-lookup"><span data-stu-id="eb0b3-235">TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384</span></span>
- <span data-ttu-id="eb0b3-236">TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256</span><span class="sxs-lookup"><span data-stu-id="eb0b3-236">TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256</span></span>
- <span data-ttu-id="eb0b3-237">TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA384</span><span class="sxs-lookup"><span data-stu-id="eb0b3-237">TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA384</span></span>
- <span data-ttu-id="eb0b3-238">TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA256</span><span class="sxs-lookup"><span data-stu-id="eb0b3-238">TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA256</span></span>
- <span data-ttu-id="eb0b3-239">TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="eb0b3-239">TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA</span></span>
- <span data-ttu-id="eb0b3-240">TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="eb0b3-240">TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA</span></span>
- <span data-ttu-id="eb0b3-241">TLS_DHE_DSS_WITH_AES_256_CBC_SHA256</span><span class="sxs-lookup"><span data-stu-id="eb0b3-241">TLS_DHE_DSS_WITH_AES_256_CBC_SHA256</span></span>
- <span data-ttu-id="eb0b3-242">TLS_DHE_DSS_WITH_AES_128_CBC_SHA256</span><span class="sxs-lookup"><span data-stu-id="eb0b3-242">TLS_DHE_DSS_WITH_AES_128_CBC_SHA256</span></span>
- <span data-ttu-id="eb0b3-243">TLS_DHE_DSS_WITH_AES_256_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="eb0b3-243">TLS_DHE_DSS_WITH_AES_256_CBC_SHA</span></span>
- <span data-ttu-id="eb0b3-244">TLS_DHE_DSS_WITH_AES_128_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="eb0b3-244">TLS_DHE_DSS_WITH_AES_128_CBC_SHA</span></span>
- <span data-ttu-id="eb0b3-245">TLS_RSA_WITH_3DES_EDE_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="eb0b3-245">TLS_RSA_WITH_3DES_EDE_CBC_SHA</span></span>
- <span data-ttu-id="eb0b3-246">TLS_DHE_DSS_WITH_3DES_EDE_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="eb0b3-246">TLS_DHE_DSS_WITH_3DES_EDE_CBC_SHA</span></span>

<span data-ttu-id="eb0b3-247">**問：應用程式閘道也支援流量 toohello 後端重新加密？**</span><span class="sxs-lookup"><span data-stu-id="eb0b3-247">**Q. Does Application Gateway also support re-encryption of traffic toohello backend?**</span></span>

<span data-ttu-id="eb0b3-248">[是]，應用程式閘道支援 SSL 卸載，並結束 tooend SSL，重新加密 hello 流量 toohello 後端。</span><span class="sxs-lookup"><span data-stu-id="eb0b3-248">Yes, Application Gateway supports SSL offload, and end tooend SSL, which re-encrypts hello traffic toohello backend.</span></span>

<span data-ttu-id="eb0b3-249">**問：可以設定 SSL 原則 toocontrol SSL 通訊協定版本嗎？**</span><span class="sxs-lookup"><span data-stu-id="eb0b3-249">**Q. Can I configure SSL policy toocontrol SSL Protocol versions?**</span></span>

<span data-ttu-id="eb0b3-250">是，您可以設定應用程式閘道 toodeny TLS1.0、 TLS1.1 和 TLS1.2。</span><span class="sxs-lookup"><span data-stu-id="eb0b3-250">Yes, you can configure Application Gateway toodeny TLS1.0, TLS1.1, and TLS1.2.</span></span> <span data-ttu-id="eb0b3-251">SSL 2.0 和 3.0 都已預設停用並，無法加以設定。</span><span class="sxs-lookup"><span data-stu-id="eb0b3-251">SSL 2.0 and 3.0 are already disabled by default and are not configurable.</span></span>

<span data-ttu-id="eb0b3-252">**問：可以設定加密套件和原則的順序嗎？**</span><span class="sxs-lookup"><span data-stu-id="eb0b3-252">**Q. Can I configure cipher suites and policy order?**</span></span>

<span data-ttu-id="eb0b3-253">是，支援[加密套件的設定](application-gateway-ssl-policy-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="eb0b3-253">Yes, [configuration of cipher suites](application-gateway-ssl-policy-overview.md) is supported.</span></span> <span data-ttu-id="eb0b3-254">定義自訂的原則，必須啟用至少一個 hello 遵循加密套件。</span><span class="sxs-lookup"><span data-stu-id="eb0b3-254">When defining a custom policy, at least one of hello following cipher suites must be enabled.</span></span> <span data-ttu-id="eb0b3-255">應用程式閘道會使用 SHA256 toofor 後端管理。</span><span class="sxs-lookup"><span data-stu-id="eb0b3-255">Application gateway uses SHA256 toofor backend management.</span></span>

* <span data-ttu-id="eb0b3-256">TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256</span><span class="sxs-lookup"><span data-stu-id="eb0b3-256">TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256</span></span> 
* <span data-ttu-id="eb0b3-257">TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256</span><span class="sxs-lookup"><span data-stu-id="eb0b3-257">TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256</span></span>
* <span data-ttu-id="eb0b3-258">TLS_DHE_RSA_WITH_AES_128_GCM_SHA256</span><span class="sxs-lookup"><span data-stu-id="eb0b3-258">TLS_DHE_RSA_WITH_AES_128_GCM_SHA256</span></span>
* <span data-ttu-id="eb0b3-259">TLS_RSA_WITH_AES_128_GCM_SHA256</span><span class="sxs-lookup"><span data-stu-id="eb0b3-259">TLS_RSA_WITH_AES_128_GCM_SHA256</span></span>
* <span data-ttu-id="eb0b3-260">TLS_RSA_WITH_AES_256_CBC_SHA256</span><span class="sxs-lookup"><span data-stu-id="eb0b3-260">TLS_RSA_WITH_AES_256_CBC_SHA256</span></span>
* <span data-ttu-id="eb0b3-261">TLS_RSA_WITH_AES_128_CBC_SHA256</span><span class="sxs-lookup"><span data-stu-id="eb0b3-261">TLS_RSA_WITH_AES_128_CBC_SHA256</span></span>

<span data-ttu-id="eb0b3-262">**問：支援多少個 SSL 憑證？**</span><span class="sxs-lookup"><span data-stu-id="eb0b3-262">**Q. How many SSL certificates are supported?**</span></span>

<span data-ttu-id="eb0b3-263">向上 too20 SSL 憑證支援。</span><span class="sxs-lookup"><span data-stu-id="eb0b3-263">Up too20 SSL certificates are supported.</span></span>

<span data-ttu-id="eb0b3-264">**問：針對後端重新加密支援多少個驗證憑證？**</span><span class="sxs-lookup"><span data-stu-id="eb0b3-264">**Q. How many authentication certificates for backend re-encryption are supported?**</span></span>

<span data-ttu-id="eb0b3-265">向上 too10 驗證憑證支援的預設值是 5。</span><span class="sxs-lookup"><span data-stu-id="eb0b3-265">Up too10 authentication certificates are supported with a default of 5.</span></span>

<span data-ttu-id="eb0b3-266">**問：應用程式閘道是否原本就與 Azure Key Vault 整合？**</span><span class="sxs-lookup"><span data-stu-id="eb0b3-266">**Q. Does Application Gateway integrate with Azure Key Vault natively?**</span></span>

<span data-ttu-id="eb0b3-267">不，它並未與 Azure Key Vault 整合。</span><span class="sxs-lookup"><span data-stu-id="eb0b3-267">No, it is not integrated with Azure Key Vault.</span></span>

## <a name="web-application-firewall-waf-configuration"></a><span data-ttu-id="eb0b3-268">Web 應用程式防火牆 (WAF) 組態</span><span class="sxs-lookup"><span data-stu-id="eb0b3-268">Web Application Firewall (WAF) Configuration</span></span>

<span data-ttu-id="eb0b3-269">**問：Hello WAF SKU 是否提供以 hello 標準 SKU 所有 hello 功能？**</span><span class="sxs-lookup"><span data-stu-id="eb0b3-269">**Q. Does hello WAF SKU offer all hello features available with hello Standard SKU?**</span></span>

<span data-ttu-id="eb0b3-270">是，WAF 支援所有的 hello 功能 hello 標準 SKU 中。</span><span class="sxs-lookup"><span data-stu-id="eb0b3-270">Yes, WAF supports all hello features in hello Standard SKU.</span></span>

<span data-ttu-id="eb0b3-271">**問：什麼是應用程式閘道支援的 hello CRS 版本？**</span><span class="sxs-lookup"><span data-stu-id="eb0b3-271">**Q. What is hello CRS version Application Gateway supports?**</span></span>

<span data-ttu-id="eb0b3-272">應用程式閘道支援 CRS [2.2.9](application-gateway-crs-rulegroups-rules.md#owasp229) 和 CRS [3.0](application-gateway-crs-rulegroups-rules.md#owasp30)。</span><span class="sxs-lookup"><span data-stu-id="eb0b3-272">Application Gateway supports CRS [2.2.9](application-gateway-crs-rulegroups-rules.md#owasp229) and CRS [3.0](application-gateway-crs-rulegroups-rules.md#owasp30).</span></span>

<span data-ttu-id="eb0b3-273">**問：如何監視 WAF？**</span><span class="sxs-lookup"><span data-stu-id="eb0b3-273">**Q. How do I monitor WAF?**</span></span>

<span data-ttu-id="eb0b3-274">WAF 是透過診斷記錄功能來監視，如需診斷記錄的詳細資訊，請參閱[應用程式閘道的診斷記錄和計量](application-gateway-diagnostics.md)</span><span class="sxs-lookup"><span data-stu-id="eb0b3-274">WAF is monitored through diagnostic logging, more information on diagnostic logging can be found at [Diagnostics Logging and Metrics for Application Gateway](application-gateway-diagnostics.md)</span></span>

<span data-ttu-id="eb0b3-275">**問：偵測模式是否會封鎖流量？**</span><span class="sxs-lookup"><span data-stu-id="eb0b3-275">**Q. Does detection mode block traffic?**</span></span>

<span data-ttu-id="eb0b3-276">否，偵測模式只會記錄觸發 WAF 規則的流量。</span><span class="sxs-lookup"><span data-stu-id="eb0b3-276">No, detection mode only logs traffic, which triggered a WAF rule.</span></span>

<span data-ttu-id="eb0b3-277">**問：如何自訂 WAF 規則？**</span><span class="sxs-lookup"><span data-stu-id="eb0b3-277">**Q. How do I customize WAF rules?**</span></span>

<span data-ttu-id="eb0b3-278">是，WAF 規則都可自訂的如需有關如何 toocustomize 它們瀏覽[自訂 WAF 規則群組與規則](application-gateway-customize-waf-rules-portal.md)</span><span class="sxs-lookup"><span data-stu-id="eb0b3-278">Yes, WAF rules are customizable, for more information on how toocustomize them visit [Customize WAF rule groups and rules](application-gateway-customize-waf-rules-portal.md)</span></span>

<span data-ttu-id="eb0b3-279">**問：目前可使用哪些規則？**</span><span class="sxs-lookup"><span data-stu-id="eb0b3-279">**Q. What rules are currently available?**</span></span>

<span data-ttu-id="eb0b3-280">WAF 目前支援 CRS [2.2.9](application-gateway-crs-rulegroups-rules.md#owasp229)和[3.0](application-gateway-crs-rulegroups-rules.md#owasp30)，提供對大部分的 hello 的基準安全性 hello 開啟 Web 應用程式安全性專案 (OWASP)，請參閱所識別的前 10 個弱點[OWASP 前 10 個弱點](https://www.owasp.org/index.php/Top10#OWASP_Top_10_for_2013)</span><span class="sxs-lookup"><span data-stu-id="eb0b3-280">WAF currently supports CRS [2.2.9](application-gateway-crs-rulegroups-rules.md#owasp229) and [3.0](application-gateway-crs-rulegroups-rules.md#owasp30), which provide baseline security against most of hello top 10 vulnerabilities identified by hello Open Web Application Security Project (OWASP) found here [OWASP top 10 Vulnerabilities](https://www.owasp.org/index.php/Top10#OWASP_Top_10_for_2013)</span></span>

* <span data-ttu-id="eb0b3-281">SQL 插入式攻擊保護</span><span class="sxs-lookup"><span data-stu-id="eb0b3-281">SQL injection protection</span></span>

* <span data-ttu-id="eb0b3-282">跨網站指令碼保護</span><span class="sxs-lookup"><span data-stu-id="eb0b3-282">Cross site scripting protection</span></span>

* <span data-ttu-id="eb0b3-283">常見 Web 攻擊保護，例如命令插入式攻擊、HTTP 要求走私、HTTP 回應分割和遠端檔案包含攻擊</span><span class="sxs-lookup"><span data-stu-id="eb0b3-283">Common Web Attacks Protection such as command injection, HTTP request smuggling, HTTP response splitting, and remote file inclusion attack</span></span>

* <span data-ttu-id="eb0b3-284">防範 HTTP 通訊協定違規</span><span class="sxs-lookup"><span data-stu-id="eb0b3-284">Protection against HTTP protocol violations</span></span>

* <span data-ttu-id="eb0b3-285">防範 HTTP 通訊協定異常行為，例如遺漏主機使用者代理程式和接受標頭</span><span class="sxs-lookup"><span data-stu-id="eb0b3-285">Protection against HTTP protocol anomalies such as missing host user-agent and accept headers</span></span>

* <span data-ttu-id="eb0b3-286">防範 Bot、編目程式和掃描器</span><span class="sxs-lookup"><span data-stu-id="eb0b3-286">Prevention against bots, crawlers, and scanners</span></span>

* <span data-ttu-id="eb0b3-287">偵測一般應用程式錯誤組態 (也就是 Apache、IIS 等)</span><span class="sxs-lookup"><span data-stu-id="eb0b3-287">Detection of common application misconfigurations (that is, Apache, IIS, etc.)</span></span>

<span data-ttu-id="eb0b3-288">**問：WAF 是否也支援 DDoS 預防？**</span><span class="sxs-lookup"><span data-stu-id="eb0b3-288">**Q. Does WAF also support DDoS prevention?**</span></span>

<span data-ttu-id="eb0b3-289">否，WAF 不提供 DDoS 預防。</span><span class="sxs-lookup"><span data-stu-id="eb0b3-289">No, WAF does not provide DDoS prevention.</span></span>

## <a name="diagnostics-and-logging"></a><span data-ttu-id="eb0b3-290">診斷和記錄</span><span class="sxs-lookup"><span data-stu-id="eb0b3-290">Diagnostics and Logging</span></span>

<span data-ttu-id="eb0b3-291">**問：應用程式閘道可使用哪些記錄檔類型？**</span><span class="sxs-lookup"><span data-stu-id="eb0b3-291">**Q. What types of logs are available with Application Gateway?**</span></span>

<span data-ttu-id="eb0b3-292">應用程式閘道可使用三種記錄檔。</span><span class="sxs-lookup"><span data-stu-id="eb0b3-292">There are three logs available for Application Gateway.</span></span> <span data-ttu-id="eb0b3-293">如需有關這些記錄和其他診斷功能的詳細資訊，請瀏覽[應用程式閘道的後端健康情況、診斷記錄和計量](application-gateway-diagnostics.md)。</span><span class="sxs-lookup"><span data-stu-id="eb0b3-293">For more information on these logs and other diagnostic capabilities, visit [Backend health, diagnostics logs, and metrics for Application Gateway](application-gateway-diagnostics.md).</span></span>

- <span data-ttu-id="eb0b3-294">**ApplicationGatewayAccessLog** -hello 存取記錄檔包含每個要求送出 toohello 應用程式閘道前端。</span><span class="sxs-lookup"><span data-stu-id="eb0b3-294">**ApplicationGatewayAccessLog** - hello access log contains each request submitted toohello Application Gateway frontend.</span></span> <span data-ttu-id="eb0b3-295">hello 資料包括 hello 呼叫者的 IP，URL 要求，回應延遲，和縮小傳回碼，位元組。每隔 300 秒會收集一次存取記錄檔。</span><span class="sxs-lookup"><span data-stu-id="eb0b3-295">hello data includes hello caller's IP, URL requested, response latency, return code, bytes in and out. Access log is collected every 300 seconds.</span></span> <span data-ttu-id="eb0b3-296">此記錄檔包含每個應用程式閘道執行個體的一筆記錄。</span><span class="sxs-lookup"><span data-stu-id="eb0b3-296">This log contains one record per instance of Application Gateway.</span></span>
- <span data-ttu-id="eb0b3-297">**ApplicationGatewayPerformanceLog** -hello 效能記錄檔擷取針對每個執行個體包括總計要求提供服務，以位元組為單位的輸送量效能資訊、 總計要求提供服務的失敗的要求計數，狀況良好和狀況不良後端執行個體計數。</span><span class="sxs-lookup"><span data-stu-id="eb0b3-297">**ApplicationGatewayPerformanceLog** - hello performance log captures performance information on per instance basis including total request served, throughput in bytes, total requests served, failed request count, healthy and unhealthy back-end instance count.</span></span>
- <span data-ttu-id="eb0b3-298">**ApplicationGatewayFirewallLog** -hello 防火牆記錄檔包含透過偵測或防止應用程式閘道以 web 應用程式的防火牆設定的模式所記錄的要求。</span><span class="sxs-lookup"><span data-stu-id="eb0b3-298">**ApplicationGatewayFirewallLog** - hello firewall log contains requests that are logged through either detection or prevention mode of an application gateway that is configured with web application firewall.</span></span>

<span data-ttu-id="eb0b3-299">**問：如何知道我的後端集區成員狀態良好？**</span><span class="sxs-lookup"><span data-stu-id="eb0b3-299">**Q. How do I know if my backend pool members are healthy?**</span></span>

<span data-ttu-id="eb0b3-300">您可以使用 hello PowerShell cmdlet`Get-AzureRmApplicationGatewayBackendHealth`或透過 hello 入口網站的健全狀況驗證造訪[應用程式閘道診斷](application-gateway-diagnostics.md)</span><span class="sxs-lookup"><span data-stu-id="eb0b3-300">You can use hello PowerShell cmdlet `Get-AzureRmApplicationGatewayBackendHealth` or verify health through hello portal by visiting [Application Gateway Diagnostics](application-gateway-diagnostics.md)</span></span>

<span data-ttu-id="eb0b3-301">**問：Hello hello 診斷記錄檔上的保留原則是什麼？**</span><span class="sxs-lookup"><span data-stu-id="eb0b3-301">**Q. What is hello retention policy on hello diagnostics logs?**</span></span>

<span data-ttu-id="eb0b3-302">診斷記錄流程 toohello 客戶儲存體帳戶和客戶可以設定 hello 保留原則，根據其喜好設定。</span><span class="sxs-lookup"><span data-stu-id="eb0b3-302">Diagnostic logs flow toohello customers storage account and customers can set hello retention policy based on their preference.</span></span> <span data-ttu-id="eb0b3-303">診斷記錄檔也可以傳送 tooan 事件中心] 或 [記錄分析。</span><span class="sxs-lookup"><span data-stu-id="eb0b3-303">Diagnostic logs can also be sent tooan Event Hub or Log Analytics.</span></span> <span data-ttu-id="eb0b3-304">如需詳細資訊，請瀏覽[應用程式閘道診斷](application-gateway-diagnostics.md)。</span><span class="sxs-lookup"><span data-stu-id="eb0b3-304">Visit [Application Gateway Diagnostics](application-gateway-diagnostics.md) for more details.</span></span>

<span data-ttu-id="eb0b3-305">**問：如何取得應用程式閘道的稽核記錄檔？**</span><span class="sxs-lookup"><span data-stu-id="eb0b3-305">**Q. How do I get audit logs for Application Gateway?**</span></span>

<span data-ttu-id="eb0b3-306">稽核記錄檔可用於應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="eb0b3-306">Audit logs are available for Application Gateway.</span></span> <span data-ttu-id="eb0b3-307">在 hello 入口網站中，按一下 **活動記錄檔**在 hello 功能表刀鋒視窗中的應用程式閘道 tooaccess hello 稽核記錄檔。</span><span class="sxs-lookup"><span data-stu-id="eb0b3-307">In hello portal, click **Activity Log** in hello menu blade of an Application Gateway tooaccess hello audit log.</span></span> 

<span data-ttu-id="eb0b3-308">**問：是否可以設定應用程式閘道的警示？**</span><span class="sxs-lookup"><span data-stu-id="eb0b3-308">**Q. Can I set alerts with Application Gateway?**</span></span>

<span data-ttu-id="eb0b3-309">是，應用程式閘道可以支援警示，並可將警示設定為關閉計量。</span><span class="sxs-lookup"><span data-stu-id="eb0b3-309">Yes, Application Gateway does support alerts, alerts are configured off metrics.</span></span>  <span data-ttu-id="eb0b3-310">應用程式閘道目前沒有 「"輸送量，輸送量的可設定的 tooalert 公制。</span><span class="sxs-lookup"><span data-stu-id="eb0b3-310">Application Gateway currently has a metric of "throughput", which can be configured tooalert.</span></span> <span data-ttu-id="eb0b3-311">toolearn 進一步了解警示，請瀏覽[接收警示通知](../monitoring-and-diagnostics/insights-receive-alert-notifications.md)。</span><span class="sxs-lookup"><span data-stu-id="eb0b3-311">toolearn more about alerts, visit [Receive alert notifications](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span></span>

<span data-ttu-id="eb0b3-312">**問：後端健康情況傳回不明狀態，什麼導致這個狀態？**</span><span class="sxs-lookup"><span data-stu-id="eb0b3-312">**Q. Backend health returns unknown status, what could be causing this status?**</span></span>

<span data-ttu-id="eb0b3-313">hello 最常見的原因是 NSG 或自訂 DNS 正在封鎖存取 toohello 後端。</span><span class="sxs-lookup"><span data-stu-id="eb0b3-313">hello most common reason is access toohello backend is being blocked by an NSG or custom DNS.</span></span> <span data-ttu-id="eb0b3-314">請瀏覽[後端健全狀況、 診斷記錄和度量的應用程式閘道](application-gateway-diagnostics.md)toolearn 更多。</span><span class="sxs-lookup"><span data-stu-id="eb0b3-314">Visit [Backend health, diagnostics logging, and metrics for Application Gateway](application-gateway-diagnostics.md) toolearn more.</span></span>

## <a name="next-steps"></a><span data-ttu-id="eb0b3-315">後續步驟</span><span class="sxs-lookup"><span data-stu-id="eb0b3-315">Next Steps</span></span>

<span data-ttu-id="eb0b3-316">有關應用程式閘道的詳細資訊請造訪的 toolearn[簡介 tooApplication 閘道](application-gateway-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="eb0b3-316">toolearn more about Application Gateway visit [Introduction tooApplication Gateway](application-gateway-introduction.md).</span></span>
