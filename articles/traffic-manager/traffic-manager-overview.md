---
title: "aaaWhat 是 Traffic Manager |Microsoft 文件"
description: "本文將協助您了解流量管理員為何，以及它是否 hello 右流量路由適合您的應用程式"
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
ms.openlocfilehash: 8e63ed11cdcdc03ae9cd28f88f0d1f9dc2cd44ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-traffic-manager"></a><span data-ttu-id="75f51-103">流量管理員概觀</span><span class="sxs-lookup"><span data-stu-id="75f51-103">Overview of Traffic Manager</span></span>

<span data-ttu-id="75f51-104">Microsoft Azure Traffic Manager 可讓您 toocontrol hello 使用者流量分散的服務端點的不同資料中心內。</span><span class="sxs-lookup"><span data-stu-id="75f51-104">Microsoft Azure Traffic Manager allows you toocontrol hello distribution of user traffic for service endpoints in different datacenters.</span></span> <span data-ttu-id="75f51-105">流量管理員支援的服務端點包括 Azure VM、Web Apps 和雲端服務。</span><span class="sxs-lookup"><span data-stu-id="75f51-105">Service endpoints supported by Traffic Manager include Azure VMs, Web Apps, and cloud services.</span></span> <span data-ttu-id="75f51-106">您也可以將流量管理員使用於外部、非 Azure 端點。</span><span class="sxs-lookup"><span data-stu-id="75f51-106">You can also use Traffic Manager with external, non-Azure endpoints.</span></span>

<span data-ttu-id="75f51-107">Traffic Manager 會使用 hello 網域名稱系統 (DNS) toodirect 用戶端要求 toohello 最適當的端點和 hello 健全狀況的 hello 端點的流量路由方法為基礎。</span><span class="sxs-lookup"><span data-stu-id="75f51-107">Traffic Manager uses hello Domain Name System (DNS) toodirect client requests toohello most appropriate endpoint based on a traffic-routing method and hello health of hello endpoints.</span></span> <span data-ttu-id="75f51-108">Traffic Manager 所提供的範圍[流量路由方法](traffic-manager-routing-methods.md)和[端點監視選項](traffic-manager-monitoring.md)toosuit 不同的應用程式需求和自動容錯移轉模式。</span><span class="sxs-lookup"><span data-stu-id="75f51-108">Traffic Manager provides a range of [traffic-routing methods](traffic-manager-routing-methods.md) and [endpoint monitoring options](traffic-manager-monitoring.md) toosuit different application needs and automatic failover models.</span></span> <span data-ttu-id="75f51-109">Traffic Manager 是彈性 toofailure，包括整個 Azure 地區的 hello 失敗。</span><span class="sxs-lookup"><span data-stu-id="75f51-109">Traffic Manager is resilient toofailure, including hello failure of an entire Azure region.</span></span>

## <a name="traffic-manager-benefits"></a><span data-ttu-id="75f51-110">流量管理員的優點</span><span class="sxs-lookup"><span data-stu-id="75f51-110">Traffic Manager benefits</span></span>

<span data-ttu-id="75f51-111">流量管理員可協助您：</span><span class="sxs-lookup"><span data-stu-id="75f51-111">Traffic Manager can help you:</span></span>

* <span data-ttu-id="75f51-112">**提高重要應用程式的可用性**</span><span class="sxs-lookup"><span data-stu-id="75f51-112">**Improve availability of critical applications**</span></span>

    <span data-ttu-id="75f51-113">流量管理員藉由監視端點，以及在端點停止運作時提供自動容錯移轉功能，為重要的應用程式提供高可用性。</span><span class="sxs-lookup"><span data-stu-id="75f51-113">Traffic Manager delivers high availability for your applications by monitoring your endpoints and providing automatic failover when an endpoint goes down.</span></span>

* <span data-ttu-id="75f51-114">**提升高效能應用程式的回應能力**</span><span class="sxs-lookup"><span data-stu-id="75f51-114">**Improve responsiveness for high-performance applications**</span></span>

    <span data-ttu-id="75f51-115">Azure 可讓您 toorun 雲端服務或網站在 hello 世界各地位於資料中心。</span><span class="sxs-lookup"><span data-stu-id="75f51-115">Azure allows you toorun cloud services or websites in datacenters located around hello world.</span></span> <span data-ttu-id="75f51-116">Traffic Manager 可以改善應用程式回應與 hello 網路延遲最小 hello 用戶端導向流量 toohello 端點。</span><span class="sxs-lookup"><span data-stu-id="75f51-116">Traffic Manager improves application responsiveness by directing traffic toohello endpoint with hello lowest network latency for hello client.</span></span>

* <span data-ttu-id="75f51-117">**在不需要停機的情況下執行服務維護**</span><span class="sxs-lookup"><span data-stu-id="75f51-117">**Perform service maintenance without downtime**</span></span>

    <span data-ttu-id="75f51-118">您可以在您的應用程式執行規劃的維護作業，而不需要停機。</span><span class="sxs-lookup"><span data-stu-id="75f51-118">You can perform planned maintenance operations on your applications without downtime.</span></span> <span data-ttu-id="75f51-119">Hello 維護進行中時，traffic Manager 將導向流量 tooalternative 端點。</span><span class="sxs-lookup"><span data-stu-id="75f51-119">Traffic Manager directs traffic tooalternative endpoints while hello maintenance is in progress.</span></span>

* <span data-ttu-id="75f51-120">**結合內部部署和雲端應用程式**</span><span class="sxs-lookup"><span data-stu-id="75f51-120">**Combine on-premises and Cloud-based applications**</span></span>

    <span data-ttu-id="75f51-121">Traffic Manager 支援的外部，非 Azure 端點，讓它 toobe 搭配混合式雲端和內部部署，包括 hello 「 高載到雲端，""移轉到雲端，」 和 「 容錯移轉到雲端 」 案例。</span><span class="sxs-lookup"><span data-stu-id="75f51-121">Traffic Manager supports external, non-Azure endpoints enabling it toobe used with hybrid cloud and on-premises deployments, including hello "burst-to-cloud," "migrate-to-cloud," and "failover-to-cloud" scenarios.</span></span>

* <span data-ttu-id="75f51-122">**大型複雜部署的流量分配**</span><span class="sxs-lookup"><span data-stu-id="75f51-122">**Distribute traffic for large, complex deployments**</span></span>

    <span data-ttu-id="75f51-123">使用[巢狀 流量管理員設定檔](traffic-manager-nested-profiles.md)、 流量路由方法可以結合的 toocreate 複雜和彈性的規則 toosupport hello 需要的較大且較為複雜的部署。</span><span class="sxs-lookup"><span data-stu-id="75f51-123">Using [nested Traffic Manager profiles](traffic-manager-nested-profiles.md), traffic-routing methods can be combined toocreate sophisticated and flexible rules toosupport hello needs of larger, more complex deployments.</span></span>

## <a name="how-traffic-manager-works"></a><span data-ttu-id="75f51-124">流量管理員的運作方式</span><span class="sxs-lookup"><span data-stu-id="75f51-124">How Traffic Manager works</span></span>

<span data-ttu-id="75f51-125">Azure Traffic Manager 可讓您的流量 toocontrol hello 分配在應用程式端點。</span><span class="sxs-lookup"><span data-stu-id="75f51-125">Azure Traffic Manager enables you toocontrol hello distribution of traffic across your application endpoints.</span></span> <span data-ttu-id="75f51-126">端點是裝載於 Azure 內部或外部的任何網際網路對向服務。</span><span class="sxs-lookup"><span data-stu-id="75f51-126">An endpoint is any Internet-facing service hosted inside or outside of Azure.</span></span>

<span data-ttu-id="75f51-127">流量管理員提供兩大優點︰</span><span class="sxs-lookup"><span data-stu-id="75f51-127">Traffic Manager provides two key benefits:</span></span>

1. <span data-ttu-id="75f51-128">根據數個 tooone 流量分散[流量路由方法](traffic-manager-routing-methods.md)</span><span class="sxs-lookup"><span data-stu-id="75f51-128">Distribution of traffic according tooone of several [traffic-routing methods](traffic-manager-routing-methods.md)</span></span>
2. <span data-ttu-id="75f51-129">[連續監視端點健康狀態](traffic-manager-monitoring.md) 以及在端點失敗時自動容錯移轉</span><span class="sxs-lookup"><span data-stu-id="75f51-129">[Continuous monitoring of endpoint health](traffic-manager-monitoring.md) and automatic failover when endpoints fail</span></span>

<span data-ttu-id="75f51-130">當用戶端嘗試 tooconnect tooa 服務時，它必須先解決 hello 的 hello 服務 tooan IP 位址的 DNS 名稱。</span><span class="sxs-lookup"><span data-stu-id="75f51-130">When a client attempts tooconnect tooa service, it must first resolve hello DNS name of hello service tooan IP address.</span></span> <span data-ttu-id="75f51-131">hello 用戶端接著會連線 toothat IP 位址 tooaccess hello 服務。</span><span class="sxs-lookup"><span data-stu-id="75f51-131">hello client then connects toothat IP address tooaccess hello service.</span></span>

<span data-ttu-id="75f51-132">**hello 最重要的點 toounderstand 是 Traffic Manager 可在 hello DNS 層級。**</span><span class="sxs-lookup"><span data-stu-id="75f51-132">**hello most important point toounderstand is that Traffic Manager works at hello DNS level.**</span></span>  <span data-ttu-id="75f51-133">Traffic Manager 會使用 DNS toodirect 用戶端 toospecific 服務端點的 hello 流量路由方法的 hello 規則為基礎。</span><span class="sxs-lookup"><span data-stu-id="75f51-133">Traffic Manager uses DNS toodirect clients toospecific service endpoints based on hello rules of hello traffic-routing method.</span></span> <span data-ttu-id="75f51-134">用戶端連線 toohello 選取端點**直接**。</span><span class="sxs-lookup"><span data-stu-id="75f51-134">Clients connect toohello selected endpoint **directly**.</span></span> <span data-ttu-id="75f51-135">流量管理員不是 Proxy 或閘道。</span><span class="sxs-lookup"><span data-stu-id="75f51-135">Traffic Manager is not a proxy or a gateway.</span></span> <span data-ttu-id="75f51-136">Traffic Manager 不會看到 hello hello 用戶端與 hello 服務之間傳送的流量。</span><span class="sxs-lookup"><span data-stu-id="75f51-136">Traffic Manager does not see hello traffic passing between hello client and hello service.</span></span>

### <a name="traffic-manager-example"></a><span data-ttu-id="75f51-137">流量管理員範例</span><span class="sxs-lookup"><span data-stu-id="75f51-137">Traffic Manager example</span></span>

<span data-ttu-id="75f51-138">Contoso Corp 開發出新的合作夥伴入口網站。</span><span class="sxs-lookup"><span data-stu-id="75f51-138">Contoso Corp have developed a new partner portal.</span></span> <span data-ttu-id="75f51-139">此入口網站中的 hello URL 為 https://partners.contoso.com/login.aspx。</span><span class="sxs-lookup"><span data-stu-id="75f51-139">hello URL for this portal is https://partners.contoso.com/login.aspx.</span></span> <span data-ttu-id="75f51-140">hello 應用程式裝載於 Azure 的三個區域。</span><span class="sxs-lookup"><span data-stu-id="75f51-140">hello application is hosted in three regions of Azure.</span></span> <span data-ttu-id="75f51-141">tooimprove 可用性和全域效能最大化時，它們使用 Traffic Manager toodistribute 用戶端流量 toohello 最接近可用端點。</span><span class="sxs-lookup"><span data-stu-id="75f51-141">tooimprove availability and maximize global performance, they use Traffic Manager toodistribute client traffic toohello closest available endpoint.</span></span>

<span data-ttu-id="75f51-142">tooachieve 此組態中，完成下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="75f51-142">tooachieve this configuration, they complete hello following steps:</span></span>

1. <span data-ttu-id="75f51-143">部署三個服務執行個體。</span><span class="sxs-lookup"><span data-stu-id="75f51-143">Deploy three instances of their service.</span></span> <span data-ttu-id="75f51-144">這些部署的 hello DNS 名稱為 'contoso us.cloudapp.net'、 'contoso eu.cloudapp.net' 和 'contoso asia.cloudapp.net'。</span><span class="sxs-lookup"><span data-stu-id="75f51-144">hello DNS names of these deployments are 'contoso-us.cloudapp.net', 'contoso-eu.cloudapp.net', and 'contoso-asia.cloudapp.net'.</span></span>
2. <span data-ttu-id="75f51-145">建立名為 'contoso.trafficmanager.net'，Traffic Manager 設定檔，並且設定該 toouse hello 「 效能 」 流量路由方法 hello 三個端點之間。</span><span class="sxs-lookup"><span data-stu-id="75f51-145">Create a Traffic Manager profile, named 'contoso.trafficmanager.net', and configure it toouse hello 'Performance' traffic-routing method across hello three endpoints.</span></span>
* <span data-ttu-id="75f51-146">設定其虛名網域名稱、 'partners.contoso.com'、 toopoint too'contoso.trafficmanager.net'，使用 DNS CNAME 記錄。</span><span class="sxs-lookup"><span data-stu-id="75f51-146">Configure their vanity domain name, 'partners.contoso.com', toopoint too'contoso.trafficmanager.net', using a DNS CNAME record.</span></span>

![流量管理員 DNS 組態][1]

> [!NOTE]
> <span data-ttu-id="75f51-148">使用虛名網域與 Azure 流量管理員時，您必須使用 CNAME toopoint 您虛名網域名稱 tooyour Traffic Manager 網域名稱。</span><span class="sxs-lookup"><span data-stu-id="75f51-148">When using a vanity domain with Azure Traffic Manager, you must use a CNAME toopoint your vanity domain name tooyour Traffic Manager domain name.</span></span> <span data-ttu-id="75f51-149">DNS 標準不允許您網域的 toocreate 在 hello 'apex' CNAME （或根）。</span><span class="sxs-lookup"><span data-stu-id="75f51-149">DNS standards do not allow you toocreate a CNAME at hello 'apex' (or root) of a domain.</span></span> <span data-ttu-id="75f51-150">因此，您無法建立 'contoso.com' 的 CNAME (有時稱為「裸」網域)。</span><span class="sxs-lookup"><span data-stu-id="75f51-150">Thus you cannot create a CNAME for 'contoso.com' (sometimes called a 'naked' domain).</span></span> <span data-ttu-id="75f51-151">您只能為 'contoso.com' 下的網域建立 CNAME，例如 'www.contoso.com'。</span><span class="sxs-lookup"><span data-stu-id="75f51-151">You can only create a CNAME for a domain under 'contoso.com', such as 'www.contoso.com'.</span></span> <span data-ttu-id="75f51-152">這項限制 toowork，建議您使用簡單 HTTP 要求重新導向 toodirect 'contoso.com' tooan 替代名稱，例如 'www.contoso.com'。</span><span class="sxs-lookup"><span data-stu-id="75f51-152">toowork around this limitation, we recommend using a simple HTTP redirect toodirect requests for 'contoso.com' tooan alternative name such as 'www.contoso.com'.</span></span>

### <a name="how-clients-connect-using-traffic-manager"></a><span data-ttu-id="75f51-153">用戶端連接如何使用流量管理員</span><span class="sxs-lookup"><span data-stu-id="75f51-153">How clients connect using Traffic Manager</span></span>

<span data-ttu-id="75f51-154">當用戶端要求 hello 頁面 https://partners.contoso.com/login.aspx 從 hello 上述範例中，繼續進行，hello 用戶端會執行下列步驟 tooresolve hello DNS 名稱的 hello，並建立連接：</span><span class="sxs-lookup"><span data-stu-id="75f51-154">Continuing from hello previous example, when a client requests hello page https://partners.contoso.com/login.aspx, hello client performs hello following steps tooresolve hello DNS name and establish a connection:</span></span>

![使用流量管理員建立連接][2]

1. <span data-ttu-id="75f51-156">傳送 DNS 查詢 tooits 設定遞迴 DNS 服務 tooresolve hello 名稱 'partners.contoso.com' hello 用戶端。</span><span class="sxs-lookup"><span data-stu-id="75f51-156">hello client sends a DNS query tooits configured recursive DNS service tooresolve hello name 'partners.contoso.com'.</span></span> <span data-ttu-id="75f51-157">遞迴 DNS 服務 (有時稱為「本機 DNS」服務) 不直接裝載 DNS 網域。</span><span class="sxs-lookup"><span data-stu-id="75f51-157">A recursive DNS service, sometimes called a 'local DNS' service, does not host DNS domains directly.</span></span> <span data-ttu-id="75f51-158">相反地，hello 用戶端 off-loads hello 工作的連絡 hello 各種授權的 DNS 服務 hello 所需的網際網路 tooresolve DNS 名稱。</span><span class="sxs-lookup"><span data-stu-id="75f51-158">Rather, hello client off-loads hello work of contacting hello various authoritative DNS services across hello Internet needed tooresolve a DNS name.</span></span>
2. <span data-ttu-id="75f51-159">tooresolve hello DNS 名稱，hello 遞迴 DNS 服務尋找 hello 'contoso.com' 網域 hello 名稱伺服器。</span><span class="sxs-lookup"><span data-stu-id="75f51-159">tooresolve hello DNS name, hello recursive DNS service finds hello name servers for hello 'contoso.com' domain.</span></span> <span data-ttu-id="75f51-160">然後，它會連絡這些名稱伺服器 toorequest hello 'partners.contoso.com' DNS 記錄。</span><span class="sxs-lookup"><span data-stu-id="75f51-160">It then contacts those name servers toorequest hello 'partners.contoso.com' DNS record.</span></span> <span data-ttu-id="75f51-161">hello contoso.com 的 DNS 伺服器會傳回指向 toocontoso.trafficmanager.net hello CNAME 記錄。</span><span class="sxs-lookup"><span data-stu-id="75f51-161">hello contoso.com DNS servers return hello CNAME record that points toocontoso.trafficmanager.net.</span></span>
3. <span data-ttu-id="75f51-162">接下來，hello 遞迴 DNS 服務會尋找 hello 名稱伺服器 hello 'trafficmanager.net' 網域中所提供的 hello Azure Traffic Manager 服務。</span><span class="sxs-lookup"><span data-stu-id="75f51-162">Next, hello recursive DNS service finds hello name servers for hello 'trafficmanager.net' domain, which are provided by hello Azure Traffic Manager service.</span></span> <span data-ttu-id="75f51-163">它接著會傳送 hello 'contoso.trafficmanager.net' DNS 記錄 toothose 要求 DNS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="75f51-163">It then sends a request for hello 'contoso.trafficmanager.net' DNS record toothose DNS servers.</span></span>
4. <span data-ttu-id="75f51-164">hello Traffic Manager 名稱伺服器接收 hello 要求。</span><span class="sxs-lookup"><span data-stu-id="75f51-164">hello Traffic Manager name servers receive hello request.</span></span> <span data-ttu-id="75f51-165">它們會根據下列項目來選擇端點︰</span><span class="sxs-lookup"><span data-stu-id="75f51-165">They choose an endpoint based on:</span></span>

    - <span data-ttu-id="75f51-166">每個端點設定的 hello 狀態 （已停用的端點不會傳回）</span><span class="sxs-lookup"><span data-stu-id="75f51-166">hello configured state of each endpoint (disabled endpoints are not returned)</span></span>
    - <span data-ttu-id="75f51-167">hello 的每個端點，由 hello Traffic Manager 健全狀況所決定的目前健全狀況檢查。</span><span class="sxs-lookup"><span data-stu-id="75f51-167">hello current health of each endpoint, as determined by hello Traffic Manager health checks.</span></span> <span data-ttu-id="75f51-168">如需詳細資訊，請參閱 [流量管理員端點監視](traffic-manager-monitoring.md)。</span><span class="sxs-lookup"><span data-stu-id="75f51-168">For more information, see [Traffic Manager Endpoint Monitoring](traffic-manager-monitoring.md).</span></span>
    - <span data-ttu-id="75f51-169">hello 選擇流量路由方法。</span><span class="sxs-lookup"><span data-stu-id="75f51-169">hello chosen traffic-routing method.</span></span> <span data-ttu-id="75f51-170">如需詳細資訊，請參閱[流量管理員路由方法](traffic-manager-routing-methods.md)。</span><span class="sxs-lookup"><span data-stu-id="75f51-170">For more information, see [Traffic Manager Routing Methods](traffic-manager-routing-methods.md).</span></span>

5. <span data-ttu-id="75f51-171">選擇 hello 端點會傳回其他 DNS CNAME 記錄。</span><span class="sxs-lookup"><span data-stu-id="75f51-171">hello chosen endpoint is returned as another DNS CNAME record.</span></span> <span data-ttu-id="75f51-172">在此例子中，我們假設傳回 contoso us.cloudapp.net。</span><span class="sxs-lookup"><span data-stu-id="75f51-172">In this case, let us suppose contoso-us.cloudapp.net is returned.</span></span>
6. <span data-ttu-id="75f51-173">接下來，hello 遞迴 DNS 服務尋找 hello 'cloudapp.net' 網域 hello 名稱伺服器。</span><span class="sxs-lookup"><span data-stu-id="75f51-173">Next, hello recursive DNS service finds hello name servers for hello 'cloudapp.net' domain.</span></span> <span data-ttu-id="75f51-174">它會連絡這些名稱伺服器 toorequest hello 'contoso us.cloudapp.net' DNS 記錄。</span><span class="sxs-lookup"><span data-stu-id="75f51-174">It contacts those name servers toorequest hello 'contoso-us.cloudapp.net' DNS record.</span></span> <span data-ttu-id="75f51-175">會傳回包含 hello hello 美國為基礎的服務端點的 IP 位址的 DNS 'A' 記錄。</span><span class="sxs-lookup"><span data-stu-id="75f51-175">A DNS 'A' record containing hello IP address of hello US-based service endpoint is returned.</span></span>
7. <span data-ttu-id="75f51-176">hello 遞迴 DNS 服務會合併 hello 結果，並傳回單一的 DNS 回應 toohello 用戶端。</span><span class="sxs-lookup"><span data-stu-id="75f51-176">hello recursive DNS service consolidates hello results and returns a single DNS response toohello client.</span></span>
8. <span data-ttu-id="75f51-177">hello 用戶端收到 hello 的 DNS 結果，並連接 toohello IP 位址。</span><span class="sxs-lookup"><span data-stu-id="75f51-177">hello client receives hello DNS results and connects toohello given IP address.</span></span> <span data-ttu-id="75f51-178">hello 用戶端連線直接，未透過 Traffic Manager toohello 應用程式服務端點。</span><span class="sxs-lookup"><span data-stu-id="75f51-178">hello client connects toohello application service endpoint directly, not through Traffic Manager.</span></span> <span data-ttu-id="75f51-179">因為這是 HTTPS 端點，hello 用戶端執行 hello 必要的 SSL/TLS 信號交換，，然後提出 HTTP GET 要求 hello ' / login.aspx' 頁面。</span><span class="sxs-lookup"><span data-stu-id="75f51-179">Since it is an HTTPS endpoint, hello client performs hello necessary SSL/TLS handshake, and then makes an HTTP GET request for hello '/login.aspx' page.</span></span>

<span data-ttu-id="75f51-180">hello 遞迴 DNS 服務會快取收到 hello DNS 回應。</span><span class="sxs-lookup"><span data-stu-id="75f51-180">hello recursive DNS service caches hello DNS responses it receives.</span></span> <span data-ttu-id="75f51-181">hello hello 用戶端裝置上的 DNS 解析程式也會快取 hello 結果。</span><span class="sxs-lookup"><span data-stu-id="75f51-181">hello DNS resolver on hello client device also caches hello result.</span></span> <span data-ttu-id="75f51-182">快取可讓後續的 DNS 查詢 toobe 來使用 hello 快取中的資料，而非其他的名稱伺服器查詢更快速地回應。</span><span class="sxs-lookup"><span data-stu-id="75f51-182">Caching enables subsequent DNS queries toobe answered more quickly by using data from hello cache rather than querying other name servers.</span></span> <span data-ttu-id="75f51-183">hello hello 快取持續時間取決於每個 DNS 記錄 hello '-存留時間' (TTL) 屬性。</span><span class="sxs-lookup"><span data-stu-id="75f51-183">hello duration of hello cache is determined by hello 'time-to-live' (TTL) property of each DNS record.</span></span> <span data-ttu-id="75f51-184">較短的值造成更快的快取過期，因此多個往返 toohello Traffic Manager 名稱伺服器。</span><span class="sxs-lookup"><span data-stu-id="75f51-184">Shorter values result in faster cache expiry and thus more round-trips toohello Traffic Manager name servers.</span></span> <span data-ttu-id="75f51-185">較長的值，表示可能需要較長的 toodirect 流量從失敗的端點。</span><span class="sxs-lookup"><span data-stu-id="75f51-185">Longer values mean that it can take longer toodirect traffic away from a failed endpoint.</span></span> <span data-ttu-id="75f51-186">Traffic Manager 可讓您 tooconfigure hello TTL 用於 Traffic Manager DNS 回應 toobe 為 0 秒，最高為 2,147,483,647 秒 (hello 與相容的最大範圍[RFC 1035](https://www.ietf.org/rfc/rfc1035.txt))，讓您 toochoose hello 值最佳平衡 hello 應用程式的需求。</span><span class="sxs-lookup"><span data-stu-id="75f51-186">Traffic Manager allows you tooconfigure hello TTL used in Traffic Manager DNS responses toobe as low as 0 seconds and as high as 2,147,483,647 seconds (hello maximum range compliant with [RFC-1035](https://www.ietf.org/rfc/rfc1035.txt)), enabling you toochoose hello value that best balances hello needs of your application.</span></span>

## <a name="pricing"></a><span data-ttu-id="75f51-187">價格</span><span class="sxs-lookup"><span data-stu-id="75f51-187">Pricing</span></span>

<span data-ttu-id="75f51-188">如需定價資訊，請參閱[流量管理員定價](https://azure.microsoft.com/pricing/details/traffic-manager/)。</span><span class="sxs-lookup"><span data-stu-id="75f51-188">For pricing information, see [Traffic Manager Pricing](https://azure.microsoft.com/pricing/details/traffic-manager/).</span></span>

## <a name="faq"></a><span data-ttu-id="75f51-189">常見問題集</span><span class="sxs-lookup"><span data-stu-id="75f51-189">FAQ</span></span>

<span data-ttu-id="75f51-190">如需流量管理員的常見問題集，請參閱[流量管理員常見問題集](traffic-manager-FAQs.md)</span><span class="sxs-lookup"><span data-stu-id="75f51-190">For frequently asked questions about Traffic Manager, see [Traffic Manager FAQs](traffic-manager-FAQs.md)</span></span>

## <a name="next-steps"></a><span data-ttu-id="75f51-191">後續步驟</span><span class="sxs-lookup"><span data-stu-id="75f51-191">Next steps</span></span>

<span data-ttu-id="75f51-192">深入了解「流量管理員」的 [端點監視和自動容錯移轉](traffic-manager-monitoring.md)。</span><span class="sxs-lookup"><span data-stu-id="75f51-192">Learn more about Traffic Manager [endpoint monitoring and automatic failover](traffic-manager-monitoring.md).</span></span>

<span data-ttu-id="75f51-193">深入了解「流量管理員」的 [流量路由方法](traffic-manager-routing-methods.md)。</span><span class="sxs-lookup"><span data-stu-id="75f51-193">Learn more about Traffic Manager [traffic routing methods](traffic-manager-routing-methods.md).</span></span>

<span data-ttu-id="75f51-194">深入了解一些 hello 另一個索引鍵[網路功能](../networking/networking-overview.md)的 Azure。</span><span class="sxs-lookup"><span data-stu-id="75f51-194">Learn about some of hello other key [networking capabilities](../networking/networking-overview.md) of Azure.</span></span>

<!--Image references-->
[1]: ./media/traffic-manager-how-traffic-manager-works/dns-configuration.png
[2]: ./media/traffic-manager-how-traffic-manager-works/flow.png

