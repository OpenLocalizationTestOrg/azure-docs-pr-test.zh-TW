---
title: "什麼是流量管理員 | Microsoft Docs"
description: "本文將協助您了解何謂流量管理員，以及它是否為您的應用程式的正確流量路由選擇"
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
editor: 
ms.assetid: 75d5ff9a-f4b9-4b05-af32-700e7bdfea5a
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/15/2017
ms.author: kumud
ms.openlocfilehash: 50d7f14d0d4234ee98d8a46e903b5f916cb02fab
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="overview-of-traffic-manager"></a><span data-ttu-id="82bfb-103">流量管理員概觀</span><span class="sxs-lookup"><span data-stu-id="82bfb-103">Overview of Traffic Manager</span></span>

<span data-ttu-id="82bfb-104">Microsoft Azure 流量管理員可讓您控制使用者流量，將流量分散到不同資料中心的服務端點。</span><span class="sxs-lookup"><span data-stu-id="82bfb-104">Microsoft Azure Traffic Manager allows you to control the distribution of user traffic for service endpoints in different datacenters.</span></span> <span data-ttu-id="82bfb-105">流量管理員支援的服務端點包括 Azure VM、Web Apps 和雲端服務。</span><span class="sxs-lookup"><span data-stu-id="82bfb-105">Service endpoints supported by Traffic Manager include Azure VMs, Web Apps, and cloud services.</span></span> <span data-ttu-id="82bfb-106">您也可以將流量管理員使用於外部、非 Azure 端點。</span><span class="sxs-lookup"><span data-stu-id="82bfb-106">You can also use Traffic Manager with external, non-Azure endpoints.</span></span>

<span data-ttu-id="82bfb-107">流量管理員會使用網域名稱系統 (DNS)，根據流量路由方法和端點的健康情況，將用戶端要求導向到最適當的端點。</span><span class="sxs-lookup"><span data-stu-id="82bfb-107">Traffic Manager uses the Domain Name System (DNS) to direct client requests to the most appropriate endpoint based on a traffic-routing method and the health of the endpoints.</span></span> <span data-ttu-id="82bfb-108">流量管理員提供[流量路由方法](traffic-manager-routing-methods.md)和[端點監視選項](traffic-manager-monitoring.md)的範圍，以符合不同的應用程式需求和自動容錯移轉模型。</span><span class="sxs-lookup"><span data-stu-id="82bfb-108">Traffic Manager provides a range of [traffic-routing methods](traffic-manager-routing-methods.md) and [endpoint monitoring options](traffic-manager-monitoring.md) to suit different application needs and automatic failover models.</span></span> <span data-ttu-id="82bfb-109">流量管理員可針對失敗彈性應變，包括整個 Azure 區域失敗。</span><span class="sxs-lookup"><span data-stu-id="82bfb-109">Traffic Manager is resilient to failure, including the failure of an entire Azure region.</span></span>

## <a name="traffic-manager-benefits"></a><span data-ttu-id="82bfb-110">流量管理員的優點</span><span class="sxs-lookup"><span data-stu-id="82bfb-110">Traffic Manager benefits</span></span>

<span data-ttu-id="82bfb-111">流量管理員可協助您：</span><span class="sxs-lookup"><span data-stu-id="82bfb-111">Traffic Manager can help you:</span></span>

* <span data-ttu-id="82bfb-112">**提高重要應用程式的可用性**</span><span class="sxs-lookup"><span data-stu-id="82bfb-112">**Improve availability of critical applications**</span></span>

    <span data-ttu-id="82bfb-113">流量管理員藉由監視端點，以及在端點停止運作時提供自動容錯移轉功能，為重要的應用程式提供高可用性。</span><span class="sxs-lookup"><span data-stu-id="82bfb-113">Traffic Manager delivers high availability for your applications by monitoring your endpoints and providing automatic failover when an endpoint goes down.</span></span>

* <span data-ttu-id="82bfb-114">**提升高效能應用程式的回應能力**</span><span class="sxs-lookup"><span data-stu-id="82bfb-114">**Improve responsiveness for high-performance applications**</span></span>

    <span data-ttu-id="82bfb-115">Azure 可讓您在世界各地的資料中心內執行雲端服務或網站。</span><span class="sxs-lookup"><span data-stu-id="82bfb-115">Azure allows you to run cloud services or websites in datacenters located around the world.</span></span> <span data-ttu-id="82bfb-116">流量管理員藉由將流量導向用戶端網路延遲最低的端點，改善應用程式的回應性。</span><span class="sxs-lookup"><span data-stu-id="82bfb-116">Traffic Manager improves application responsiveness by directing traffic to the endpoint with the lowest network latency for the client.</span></span>

* <span data-ttu-id="82bfb-117">**在不需要停機的情況下執行服務維護**</span><span class="sxs-lookup"><span data-stu-id="82bfb-117">**Perform service maintenance without downtime**</span></span>

    <span data-ttu-id="82bfb-118">您可以在您的應用程式執行規劃的維護作業，而不需要停機。</span><span class="sxs-lookup"><span data-stu-id="82bfb-118">You can perform planned maintenance operations on your applications without downtime.</span></span> <span data-ttu-id="82bfb-119">當維護正在進行時，流量管理員會將流量導向替代的端點。</span><span class="sxs-lookup"><span data-stu-id="82bfb-119">Traffic Manager directs traffic to alternative endpoints while the maintenance is in progress.</span></span>

* <span data-ttu-id="82bfb-120">**結合內部部署和雲端應用程式**</span><span class="sxs-lookup"><span data-stu-id="82bfb-120">**Combine on-premises and Cloud-based applications**</span></span>

    <span data-ttu-id="82bfb-121">流量管理員支援外部、非 Azure 端點，並可搭配混合式雲端和內部部署使用，包括「高載至雲端」、「移轉至雲端」和「容錯移轉至雲端」案例。</span><span class="sxs-lookup"><span data-stu-id="82bfb-121">Traffic Manager supports external, non-Azure endpoints enabling it to be used with hybrid cloud and on-premises deployments, including the "burst-to-cloud," "migrate-to-cloud," and "failover-to-cloud" scenarios.</span></span>

* <span data-ttu-id="82bfb-122">**大型複雜部署的流量分配**</span><span class="sxs-lookup"><span data-stu-id="82bfb-122">**Distribute traffic for large, complex deployments**</span></span>

    <span data-ttu-id="82bfb-123">利用[巢狀的流量管理員設定檔](traffic-manager-nested-profiles.md)，可以組合流量路由方法，建立複雜且彈性的規則，以支援更大型且更複雜部署的需求。</span><span class="sxs-lookup"><span data-stu-id="82bfb-123">Using [nested Traffic Manager profiles](traffic-manager-nested-profiles.md), traffic-routing methods can be combined to create sophisticated and flexible rules to support the needs of larger, more complex deployments.</span></span>

## <a name="how-traffic-manager-works"></a><span data-ttu-id="82bfb-124">流量管理員的運作方式</span><span class="sxs-lookup"><span data-stu-id="82bfb-124">How Traffic Manager works</span></span>

<span data-ttu-id="82bfb-125">Azure 流量管理員可讓您控制流量分散到應用程式端點的方式。</span><span class="sxs-lookup"><span data-stu-id="82bfb-125">Azure Traffic Manager enables you to control the distribution of traffic across your application endpoints.</span></span> <span data-ttu-id="82bfb-126">端點是裝載於 Azure 內部或外部的任何網際網路對向服務。</span><span class="sxs-lookup"><span data-stu-id="82bfb-126">An endpoint is any Internet-facing service hosted inside or outside of Azure.</span></span>

<span data-ttu-id="82bfb-127">流量管理員提供兩大優點︰</span><span class="sxs-lookup"><span data-stu-id="82bfb-127">Traffic Manager provides two key benefits:</span></span>

1. <span data-ttu-id="82bfb-128">根據幾個 [流量路由方法](traffic-manager-routing-methods.md)</span><span class="sxs-lookup"><span data-stu-id="82bfb-128">Distribution of traffic according to one of several [traffic-routing methods](traffic-manager-routing-methods.md)</span></span>
2. <span data-ttu-id="82bfb-129">[連續監視端點健康狀態](traffic-manager-monitoring.md) 以及在端點失敗時自動容錯移轉</span><span class="sxs-lookup"><span data-stu-id="82bfb-129">[Continuous monitoring of endpoint health](traffic-manager-monitoring.md) and automatic failover when endpoints fail</span></span>

<span data-ttu-id="82bfb-130">當用戶端嘗試連接至服務時，它必須先將服務的 DNS 名稱解析為 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="82bfb-130">When a client attempts to connect to a service, it must first resolve the DNS name of the service to an IP address.</span></span> <span data-ttu-id="82bfb-131">然後用戶端才能連接到該 IP 位址以存取服務。</span><span class="sxs-lookup"><span data-stu-id="82bfb-131">The client then connects to that IP address to access the service.</span></span>

<span data-ttu-id="82bfb-132">**最重要的一點是了解流量管理員是在 DNS 層級上運作。**</span><span class="sxs-lookup"><span data-stu-id="82bfb-132">**The most important point to understand is that Traffic Manager works at the DNS level.**</span></span>  <span data-ttu-id="82bfb-133">流量管理員會使用 DNS，根據流量路由方法的規則，將用戶端導向特定的服務端點。</span><span class="sxs-lookup"><span data-stu-id="82bfb-133">Traffic Manager uses DNS to direct clients to specific service endpoints based on the rules of the traffic-routing method.</span></span> <span data-ttu-id="82bfb-134">用戶端會**直接**連接至選取的端點。</span><span class="sxs-lookup"><span data-stu-id="82bfb-134">Clients connect to the selected endpoint **directly**.</span></span> <span data-ttu-id="82bfb-135">流量管理員不是 Proxy 或閘道。</span><span class="sxs-lookup"><span data-stu-id="82bfb-135">Traffic Manager is not a proxy or a gateway.</span></span> <span data-ttu-id="82bfb-136">流量管理員看不到在用戶端與服務之間傳遞的流量。</span><span class="sxs-lookup"><span data-stu-id="82bfb-136">Traffic Manager does not see the traffic passing between the client and the service.</span></span>

### <a name="traffic-manager-example"></a><span data-ttu-id="82bfb-137">流量管理員範例</span><span class="sxs-lookup"><span data-stu-id="82bfb-137">Traffic Manager example</span></span>

<span data-ttu-id="82bfb-138">Contoso Corp 開發出新的合作夥伴入口網站。</span><span class="sxs-lookup"><span data-stu-id="82bfb-138">Contoso Corp have developed a new partner portal.</span></span> <span data-ttu-id="82bfb-139">此入口網站的 URL 是 https://partners.contoso.com/login.aspx。</span><span class="sxs-lookup"><span data-stu-id="82bfb-139">The URL for this portal is https://partners.contoso.com/login.aspx.</span></span> <span data-ttu-id="82bfb-140">應用程式裝載於 Azure 的三個區域。</span><span class="sxs-lookup"><span data-stu-id="82bfb-140">The application is hosted in three regions of Azure.</span></span> <span data-ttu-id="82bfb-141">為了改善可用性和最佳化全域效能，他們使用流量管理員將用戶端流量分配給最靠近的可用端點。</span><span class="sxs-lookup"><span data-stu-id="82bfb-141">To improve availability and maximize global performance, they use Traffic Manager to distribute client traffic to the closest available endpoint.</span></span>

<span data-ttu-id="82bfb-142">若要達成這個設定，要完成下列步驟︰</span><span class="sxs-lookup"><span data-stu-id="82bfb-142">To achieve this configuration, they complete the following steps:</span></span>

1. <span data-ttu-id="82bfb-143">部署三個服務執行個體。</span><span class="sxs-lookup"><span data-stu-id="82bfb-143">Deploy three instances of their service.</span></span> <span data-ttu-id="82bfb-144">這些部署的 DNS 名稱為 'contoso-us.cloudapp.net'、'contoso-eu.cloudapp.net' 和 'contoso-asia.cloudapp.net'。</span><span class="sxs-lookup"><span data-stu-id="82bfb-144">The DNS names of these deployments are 'contoso-us.cloudapp.net', 'contoso-eu.cloudapp.net', and 'contoso-asia.cloudapp.net'.</span></span>
2. <span data-ttu-id="82bfb-145">建立名為 'contoso.trafficmanager.net' 的流量管理員設定檔，並設定為在這三個端點之間使用「效能」流量路由方法。</span><span class="sxs-lookup"><span data-stu-id="82bfb-145">Create a Traffic Manager profile, named 'contoso.trafficmanager.net', and configure it to use the 'Performance' traffic-routing method across the three endpoints.</span></span>
* <span data-ttu-id="82bfb-146">使用 DNS CNAME 記錄，將虛名網域名稱 'partners.contoso.com' 設定成指向 'contoso.trafficmanager.net'。</span><span class="sxs-lookup"><span data-stu-id="82bfb-146">Configure their vanity domain name, 'partners.contoso.com', to point to 'contoso.trafficmanager.net', using a DNS CNAME record.</span></span>

![流量管理員 DNS 組態][1]

> [!NOTE]
> <span data-ttu-id="82bfb-148">虛名網域配合 Azure 流量管理員使用時，您必須使用 CNAME 將虛名網域名稱指向流量管理員網域名稱。</span><span class="sxs-lookup"><span data-stu-id="82bfb-148">When using a vanity domain with Azure Traffic Manager, you must use a CNAME to point your vanity domain name to your Traffic Manager domain name.</span></span> <span data-ttu-id="82bfb-149">DNS 標準不允許您在網域的「頂點」(或根) 上建立 CNAME。</span><span class="sxs-lookup"><span data-stu-id="82bfb-149">DNS standards do not allow you to create a CNAME at the 'apex' (or root) of a domain.</span></span> <span data-ttu-id="82bfb-150">因此，您無法建立 'contoso.com' 的 CNAME (有時稱為「裸」網域)。</span><span class="sxs-lookup"><span data-stu-id="82bfb-150">Thus you cannot create a CNAME for 'contoso.com' (sometimes called a 'naked' domain).</span></span> <span data-ttu-id="82bfb-151">您只能為 'contoso.com' 下的網域建立 CNAME，例如 'www.contoso.com'。</span><span class="sxs-lookup"><span data-stu-id="82bfb-151">You can only create a CNAME for a domain under 'contoso.com', such as 'www.contoso.com'.</span></span> <span data-ttu-id="82bfb-152">為了克服這項限制，我們建議使用簡單的 HTTP 重新導向，將 'contoso.com' 的要求導向替代名稱，例如 'www.contoso.com'。</span><span class="sxs-lookup"><span data-stu-id="82bfb-152">To work around this limitation, we recommend using a simple HTTP redirect to direct requests for 'contoso.com' to an alternative name such as 'www.contoso.com'.</span></span>

### <a name="how-clients-connect-using-traffic-manager"></a><span data-ttu-id="82bfb-153">用戶端連接如何使用流量管理員</span><span class="sxs-lookup"><span data-stu-id="82bfb-153">How clients connect using Traffic Manager</span></span>

<span data-ttu-id="82bfb-154">接續上述範例，當用戶端要求頁面 https://partners.contoso.com/login.aspx 時，用戶端會執行下列步驟來解析 DNS 名稱，然後建立連接︰</span><span class="sxs-lookup"><span data-stu-id="82bfb-154">Continuing from the previous example, when a client requests the page https://partners.contoso.com/login.aspx, the client performs the following steps to resolve the DNS name and establish a connection:</span></span>

![使用流量管理員建立連接][2]

1. <span data-ttu-id="82bfb-156">用戶端會將 DNS 查詢傳送至已設定的遞迴 DNS 服務，以解析名稱 'partners.contoso.com'。</span><span class="sxs-lookup"><span data-stu-id="82bfb-156">The client sends a DNS query to its configured recursive DNS service to resolve the name 'partners.contoso.com'.</span></span> <span data-ttu-id="82bfb-157">遞迴 DNS 服務 (有時稱為「本機 DNS」服務) 不直接裝載 DNS 網域。</span><span class="sxs-lookup"><span data-stu-id="82bfb-157">A recursive DNS service, sometimes called a 'local DNS' service, does not host DNS domains directly.</span></span> <span data-ttu-id="82bfb-158">相反地，用戶端不負責連絡網際網路上解析 DNS 名稱所需的各種授權 DNS 服務。</span><span class="sxs-lookup"><span data-stu-id="82bfb-158">Rather, the client off-loads the work of contacting the various authoritative DNS services across the Internet needed to resolve a DNS name.</span></span>
2. <span data-ttu-id="82bfb-159">為了解析 DNS 名稱，遞迴 DNS 服務會尋找 'contoso.com' 網域的名稱伺服器。</span><span class="sxs-lookup"><span data-stu-id="82bfb-159">To resolve the DNS name, the recursive DNS service finds the name servers for the 'contoso.com' domain.</span></span> <span data-ttu-id="82bfb-160">然後，連絡這些名稱伺服器來要求 'partners.contoso.com' DNS 記錄。</span><span class="sxs-lookup"><span data-stu-id="82bfb-160">It then contacts those name servers to request the 'partners.contoso.com' DNS record.</span></span> <span data-ttu-id="82bfb-161">Contoso.com DNS 伺服器會傳回指向 contoso.trafficmanager.net 的 CNAME 記錄。</span><span class="sxs-lookup"><span data-stu-id="82bfb-161">The contoso.com DNS servers return the CNAME record that points to contoso.trafficmanager.net.</span></span>
3. <span data-ttu-id="82bfb-162">接下來，遞迴 DNS 服務會尋找 'trafficmanager.net' 網域的名稱伺服器 (由 Azure 流量管理員服務提供)。</span><span class="sxs-lookup"><span data-stu-id="82bfb-162">Next, the recursive DNS service finds the name servers for the 'trafficmanager.net' domain, which are provided by the Azure Traffic Manager service.</span></span> <span data-ttu-id="82bfb-163">然後，將 'contoso.trafficmanager.net' DNS 記錄的要求傳送至這些 DNS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="82bfb-163">It then sends a request for the 'contoso.trafficmanager.net' DNS record to those DNS servers.</span></span>
4. <span data-ttu-id="82bfb-164">流量管理員名稱伺服器接收要求。</span><span class="sxs-lookup"><span data-stu-id="82bfb-164">The Traffic Manager name servers receive the request.</span></span> <span data-ttu-id="82bfb-165">它們會根據下列項目來選擇端點︰</span><span class="sxs-lookup"><span data-stu-id="82bfb-165">They choose an endpoint based on:</span></span>

    - <span data-ttu-id="82bfb-166">每個端點已設定的狀態 (不會傳回已停用的端點)</span><span class="sxs-lookup"><span data-stu-id="82bfb-166">The configured state of each endpoint (disabled endpoints are not returned)</span></span>
    - <span data-ttu-id="82bfb-167">每個端點目前的健康狀態，由流量管理員健康狀態檢查所決定。</span><span class="sxs-lookup"><span data-stu-id="82bfb-167">The current health of each endpoint, as determined by the Traffic Manager health checks.</span></span> <span data-ttu-id="82bfb-168">如需詳細資訊，請參閱 [流量管理員端點監視](traffic-manager-monitoring.md)。</span><span class="sxs-lookup"><span data-stu-id="82bfb-168">For more information, see [Traffic Manager Endpoint Monitoring](traffic-manager-monitoring.md).</span></span>
    - <span data-ttu-id="82bfb-169">所選的流量路由方法。</span><span class="sxs-lookup"><span data-stu-id="82bfb-169">The chosen traffic-routing method.</span></span> <span data-ttu-id="82bfb-170">如需詳細資訊，請參閱[流量管理員路由方法](traffic-manager-routing-methods.md)。</span><span class="sxs-lookup"><span data-stu-id="82bfb-170">For more information, see [Traffic Manager Routing Methods](traffic-manager-routing-methods.md).</span></span>

5. <span data-ttu-id="82bfb-171">選擇的端點會傳回成為另一筆 DNS CNAME 記錄。</span><span class="sxs-lookup"><span data-stu-id="82bfb-171">The chosen endpoint is returned as another DNS CNAME record.</span></span> <span data-ttu-id="82bfb-172">在此例子中，我們假設傳回 contoso us.cloudapp.net。</span><span class="sxs-lookup"><span data-stu-id="82bfb-172">In this case, let us suppose contoso-us.cloudapp.net is returned.</span></span>
6. <span data-ttu-id="82bfb-173">接下來，遞迴 DNS 服務會尋找 'cloudapp.net' 網域的名稱伺服器。</span><span class="sxs-lookup"><span data-stu-id="82bfb-173">Next, the recursive DNS service finds the name servers for the 'cloudapp.net' domain.</span></span> <span data-ttu-id="82bfb-174">它會連絡這些名稱伺服器，以要求 'contoso-us.cloudapp.net' DNS 記錄。</span><span class="sxs-lookup"><span data-stu-id="82bfb-174">It contacts those name servers to request the 'contoso-us.cloudapp.net' DNS record.</span></span> <span data-ttu-id="82bfb-175">將會傳回一筆 DNS 'A' 記錄，內含美國地區服務端點的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="82bfb-175">A DNS 'A' record containing the IP address of the US-based service endpoint is returned.</span></span>
7. <span data-ttu-id="82bfb-176">遞迴 DNS 服務會合併結果，並傳回單一 DNS 回應給用戶端。</span><span class="sxs-lookup"><span data-stu-id="82bfb-176">The recursive DNS service consolidates the results and returns a single DNS response to the client.</span></span>
8. <span data-ttu-id="82bfb-177">用戶端收到 DNS 結果，然後連接至指定的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="82bfb-177">The client receives the DNS results and connects to the given IP address.</span></span> <span data-ttu-id="82bfb-178">用戶端會直接連接至應用程式服務端點，而不透過流量管理員。</span><span class="sxs-lookup"><span data-stu-id="82bfb-178">The client connects to the application service endpoint directly, not through Traffic Manager.</span></span> <span data-ttu-id="82bfb-179">因為它是 HTTPS 端點，用戶端會執行必要的 SSL/TLS 交握，然後提出 '/login.aspx' 頁面的 HTTP GET 要求。</span><span class="sxs-lookup"><span data-stu-id="82bfb-179">Since it is an HTTPS endpoint, the client performs the necessary SSL/TLS handshake, and then makes an HTTP GET request for the '/login.aspx' page.</span></span>

<span data-ttu-id="82bfb-180">遞迴 DNS 服務會快取它收到的 DNS 回應。</span><span class="sxs-lookup"><span data-stu-id="82bfb-180">The recursive DNS service caches the DNS responses it receives.</span></span> <span data-ttu-id="82bfb-181">用戶端裝置上的 DNS 解析程式也會快取結果。</span><span class="sxs-lookup"><span data-stu-id="82bfb-181">The DNS resolver on the client device also caches the result.</span></span> <span data-ttu-id="82bfb-182">快取功能會使用快取中的資料，而不查詢其他名稱伺服器，因而可以更快回應後續的 DNS 查詢。</span><span class="sxs-lookup"><span data-stu-id="82bfb-182">Caching enables subsequent DNS queries to be answered more quickly by using data from the cache rather than querying other name servers.</span></span> <span data-ttu-id="82bfb-183">快取持續時間取決於每一筆 DNS 記錄的「存留時間」(TTL) 屬性。</span><span class="sxs-lookup"><span data-stu-id="82bfb-183">The duration of the cache is determined by the 'time-to-live' (TTL) property of each DNS record.</span></span> <span data-ttu-id="82bfb-184">較短的值會導致快取更快到期，因此需要更多次往返於流量管理員的名稱伺服器。</span><span class="sxs-lookup"><span data-stu-id="82bfb-184">Shorter values result in faster cache expiry and thus more round-trips to the Traffic Manager name servers.</span></span> <span data-ttu-id="82bfb-185">較長的值表示從失敗端點引開流量會花費更長的時間。</span><span class="sxs-lookup"><span data-stu-id="82bfb-185">Longer values mean that it can take longer to direct traffic away from a failed endpoint.</span></span> <span data-ttu-id="82bfb-186">流量管理員允許您將流量管理員 DNS 回應中使用的 TTL，設定為最低是 0 秒及最高是 2,147,483,647 秒 (符合 [RFC-1035](https://www.ietf.org/rfc/rfc1035.txt) 的最大範圍)，讓您選擇最能平衡應用程式需求的值。</span><span class="sxs-lookup"><span data-stu-id="82bfb-186">Traffic Manager allows you to configure the TTL used in Traffic Manager DNS responses to be as low as 0 seconds and as high as 2,147,483,647 seconds (the maximum range compliant with [RFC-1035](https://www.ietf.org/rfc/rfc1035.txt)), enabling you to choose the value that best balances the needs of your application.</span></span>

## <a name="pricing"></a><span data-ttu-id="82bfb-187">價格</span><span class="sxs-lookup"><span data-stu-id="82bfb-187">Pricing</span></span>

<span data-ttu-id="82bfb-188">如需定價資訊，請參閱[流量管理員定價](https://azure.microsoft.com/pricing/details/traffic-manager/)。</span><span class="sxs-lookup"><span data-stu-id="82bfb-188">For pricing information, see [Traffic Manager Pricing](https://azure.microsoft.com/pricing/details/traffic-manager/).</span></span>

## <a name="faq"></a><span data-ttu-id="82bfb-189">常見問題集</span><span class="sxs-lookup"><span data-stu-id="82bfb-189">FAQ</span></span>

<span data-ttu-id="82bfb-190">如需流量管理員的常見問題集，請參閱[流量管理員常見問題集](traffic-manager-FAQs.md)</span><span class="sxs-lookup"><span data-stu-id="82bfb-190">For frequently asked questions about Traffic Manager, see [Traffic Manager FAQs](traffic-manager-FAQs.md)</span></span>

## <a name="next-steps"></a><span data-ttu-id="82bfb-191">後續步驟</span><span class="sxs-lookup"><span data-stu-id="82bfb-191">Next steps</span></span>

<span data-ttu-id="82bfb-192">深入了解「流量管理員」的 [端點監視和自動容錯移轉](traffic-manager-monitoring.md)。</span><span class="sxs-lookup"><span data-stu-id="82bfb-192">Learn more about Traffic Manager [endpoint monitoring and automatic failover](traffic-manager-monitoring.md).</span></span>

<span data-ttu-id="82bfb-193">深入了解「流量管理員」的 [流量路由方法](traffic-manager-routing-methods.md)。</span><span class="sxs-lookup"><span data-stu-id="82bfb-193">Learn more about Traffic Manager [traffic routing methods](traffic-manager-routing-methods.md).</span></span>

<span data-ttu-id="82bfb-194">深入了解 Azure 的一些其他重要[網路功能](../networking/networking-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="82bfb-194">Learn about some of the other key [networking capabilities](../networking/networking-overview.md) of Azure.</span></span>

<!--Image references-->
[1]: ./media/traffic-manager-how-traffic-manager-works/dns-configuration.png
[2]: ./media/traffic-manager-how-traffic-manager-works/flow.png

