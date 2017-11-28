---
title: "aaaAzure DNS 常見問題集 |Microsoft 文件"
description: "關於 Azure DNS 的常見問題集"
services: dns
documentationcenter: na
author: jtuliani
manager: timlt
editor: 
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/21/2017
ms.author: jonatul
ms.openlocfilehash: 55006e9d8b311f1e94678eb9d35ce3448b936488
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-dns-faq"></a><span data-ttu-id="6fc73-103">Azure DNS 常見問題集</span><span class="sxs-lookup"><span data-stu-id="6fc73-103">Azure DNS FAQ</span></span>

## <a name="about-azure-dns"></a><span data-ttu-id="6fc73-104">關於 Azure DNS</span><span class="sxs-lookup"><span data-stu-id="6fc73-104">About Azure DNS</span></span>

### <a name="what-is-azure-dns"></a><span data-ttu-id="6fc73-105">什麼是 Azure DNS？</span><span class="sxs-lookup"><span data-stu-id="6fc73-105">What is Azure DNS?</span></span>

<span data-ttu-id="6fc73-106">hello 網域名稱系統或 DNS，負責將轉譯 （或解決） 的網站或服務名稱 tooits IP 位址。</span><span class="sxs-lookup"><span data-stu-id="6fc73-106">hello Domain Name System, or DNS, is responsible for translating (or resolving) a website or service name tooits IP address.</span></span> <span data-ttu-id="6fc73-107">Azure DNS 是 DNS 網域的主機服務，採用 Microsoft Azure 基礎結構提供名稱解析。</span><span class="sxs-lookup"><span data-stu-id="6fc73-107">Azure DNS is a hosting service for DNS domains, providing name resolution using Microsoft Azure infrastructure.</span></span> <span data-ttu-id="6fc73-108">裝載您在 Azure 中的網域，您可以管理您的 DNS 記錄使用相同的認證、 Api、 工具和計費 hello 與其他 Azure 服務。</span><span class="sxs-lookup"><span data-stu-id="6fc73-108">By hosting your domains in Azure, you can manage your DNS records using hello same credentials, APIs, tools, and billing as your other Azure services.</span></span>

<span data-ttu-id="6fc73-109">Azure DNS 中的 DNS 網域裝載於 Azure 的 DNS 名稱伺服器全球網路。</span><span class="sxs-lookup"><span data-stu-id="6fc73-109">DNS domains in Azure DNS are hosted on Azure's global network of DNS name servers.</span></span> <span data-ttu-id="6fc73-110">我們使用任一傳播網路，讓每個 DNS 查詢由 hello 最接近可用 DNS 伺服器回應。</span><span class="sxs-lookup"><span data-stu-id="6fc73-110">We use Anycast networking so that each DNS query is answered by hello closest available DNS server.</span></span> <span data-ttu-id="6fc73-111">這為您的網域提供快速的效能與高可用性。</span><span class="sxs-lookup"><span data-stu-id="6fc73-111">This provides both fast performance and high availability for your domain.</span></span>

<span data-ttu-id="6fc73-112">hello Azure DNS 服務會採用 Azure 資源管理員。</span><span class="sxs-lookup"><span data-stu-id="6fc73-112">hello Azure DNS service is based on Azure Resource Manager.</span></span> <span data-ttu-id="6fc73-113">因此可得益於 Resource Manager 的功能，如角色型存取控制、稽核記錄檔、資源鎖定。</span><span class="sxs-lookup"><span data-stu-id="6fc73-113">As such, it benefits from Resource Manager features such as role-based access control, audit logs, and resource locking.</span></span> <span data-ttu-id="6fc73-114">您的網域和記錄可以透過 hello Azure 入口網站，Azure PowerShell cmdlet，管理和 hello 跨平台 Azure CLI。</span><span class="sxs-lookup"><span data-stu-id="6fc73-114">Your domains and records can be managed via hello Azure portal, Azure PowerShell cmdlets, and hello cross-platform Azure CLI.</span></span> <span data-ttu-id="6fc73-115">需要 DNS 的自動管理的應用程式可以整合透過 hello hello 服務 REST API 和 Sdk。</span><span class="sxs-lookup"><span data-stu-id="6fc73-115">Applications requiring automatic DNS management can integrate with hello service via hello REST API and SDKs.</span></span>

### <a name="how-much-does-azure-dns-cost"></a><span data-ttu-id="6fc73-116">Azure DNS 的費用是多少？</span><span class="sxs-lookup"><span data-stu-id="6fc73-116">How much does Azure DNS cost?</span></span>

<span data-ttu-id="6fc73-117">hello Azure DNS 計費模型根據 Azure DNS 和 DNS 查詢他們收到的 hello 數量裝載的 DNS 區域的 hello 數目。</span><span class="sxs-lookup"><span data-stu-id="6fc73-117">hello Azure DNS billing model is based on hello number of DNS zones hosted in Azure DNS and hello number of DNS queries they receive.</span></span> <span data-ttu-id="6fc73-118">根據使用量會提供折扣。</span><span class="sxs-lookup"><span data-stu-id="6fc73-118">Discounts are provided based on usage.</span></span>

<span data-ttu-id="6fc73-119">如需詳細資訊，請參閱 hello [Azure DNS 定價頁面](https://azure.microsoft.com/pricing/details/dns/)。</span><span class="sxs-lookup"><span data-stu-id="6fc73-119">For more information, see hello [Azure DNS pricing page](https://azure.microsoft.com/pricing/details/dns/).</span></span>

### <a name="what-is-hello-sla-for-azure-dns"></a><span data-ttu-id="6fc73-120">Azure DNS 的 hello SLA 是什麼？</span><span class="sxs-lookup"><span data-stu-id="6fc73-120">What is hello SLA for Azure DNS?</span></span>

<span data-ttu-id="6fc73-121">我們保證，有效的 DNS 要求會從接收回應至少一個 Azure DNS 名稱伺服器至少 99.99%的 hello 時間。</span><span class="sxs-lookup"><span data-stu-id="6fc73-121">We guarantee that valid DNS requests will receive a response from at least one Azure DNS name server at least 99.99% of hello time.</span></span>

<span data-ttu-id="6fc73-122">如需詳細資訊，請參閱 hello [Azure DNS SLA 頁面](https://azure.microsoft.com/support/legal/sla/dns)。</span><span class="sxs-lookup"><span data-stu-id="6fc73-122">For more information, see hello [Azure DNS SLA page](https://azure.microsoft.com/support/legal/sla/dns).</span></span>

### <a name="what-is-a-dns-zone-is-it-hello-same-as-a-dns-domain"></a><span data-ttu-id="6fc73-123">什麼是「DNS 區域」？</span><span class="sxs-lookup"><span data-stu-id="6fc73-123">What is a ‘DNS zone’?</span></span> <span data-ttu-id="6fc73-124">是它做為 DNS 網域 hello 相同？</span><span class="sxs-lookup"><span data-stu-id="6fc73-124">Is it hello same as a DNS domain?</span></span> 

<span data-ttu-id="6fc73-125">網域在 hello 網域名稱系統中，例如 'contoso.com' 是唯一的名稱。</span><span class="sxs-lookup"><span data-stu-id="6fc73-125">A domain is a unique name in hello domain name system, for example ‘contoso.com’.</span></span>

<span data-ttu-id="6fc73-126">DNS 區域是使用的 toohost hello 針對特定網域的 DNS 記錄。</span><span class="sxs-lookup"><span data-stu-id="6fc73-126">A DNS zone is used toohost hello DNS records for a particular domain.</span></span> <span data-ttu-id="6fc73-127">例如，hello 網域 'contoso.com' 可能包含數個 DNS 記錄，例如 'mail.contoso.com' （適用於郵件伺服器） 和 'www.contoso.com' （適用於該網站）。</span><span class="sxs-lookup"><span data-stu-id="6fc73-127">For example, hello domain ‘contoso.com’ may contain several DNS records, such as ‘mail.contoso.com’ (for a mail server) and ‘www.contoso.com’ (for a web site).</span></span> <span data-ttu-id="6fc73-128">這些會裝載於 hello DNS 區域 'contoso.com'。</span><span class="sxs-lookup"><span data-stu-id="6fc73-128">These would be hosted in hello DNS zone 'contoso.com'.</span></span>

<span data-ttu-id="6fc73-129">網域名稱是*只有名稱*，而 DNS 區域是包含網域名稱的 hello DNS 記錄的資料資源。</span><span class="sxs-lookup"><span data-stu-id="6fc73-129">A domain name is *just a name*, whereas a DNS zone is a data resource containing hello DNS records for a domain name.</span></span> <span data-ttu-id="6fc73-130">Azure DNS 可讓您 toohost DNS 區域，並管理網域，以在 Azure 中的 hello DNS 記錄。</span><span class="sxs-lookup"><span data-stu-id="6fc73-130">Azure DNS allows you toohost a DNS zone and manage hello DNS records for a domain in Azure.</span></span> <span data-ttu-id="6fc73-131">它也提供 DNS 名稱伺服器 tooanswer hello 網際網路 DNS 查詢。</span><span class="sxs-lookup"><span data-stu-id="6fc73-131">It also provides DNS name servers tooanswer DNS queries from hello Internet.</span></span>

### <a name="do-i-need-toopurchase-a-dns-domain-name-toouse-azure-dns"></a><span data-ttu-id="6fc73-132">是否需要 DNS 網域名稱 toouse Azure DNS toopurchase？</span><span class="sxs-lookup"><span data-stu-id="6fc73-132">Do I need toopurchase a DNS domain name toouse Azure DNS?</span></span> 

<span data-ttu-id="6fc73-133">不一定。</span><span class="sxs-lookup"><span data-stu-id="6fc73-133">Not necessarily.</span></span>

<span data-ttu-id="6fc73-134">您不需要 toopurchase 網域 toohost Azure DNS 中的 DNS 區域。</span><span class="sxs-lookup"><span data-stu-id="6fc73-134">You do not need toopurchase a domain toohost a DNS zone in Azure DNS.</span></span> <span data-ttu-id="6fc73-135">您可以隨時建立 DNS 區域，但不擁有 hello 網域名稱。</span><span class="sxs-lookup"><span data-stu-id="6fc73-135">You can create a DNS zone at any time without owning hello domain name.</span></span> <span data-ttu-id="6fc73-136">此區域的 DNS 查詢只會解決是否它們會被導向 toohello Azure DNS 名稱伺服器指派 toohello 區域。</span><span class="sxs-lookup"><span data-stu-id="6fc73-136">DNS queries for this zone will only resolve if they are directed toohello Azure DNS name servers assigned toohello zone.</span></span>

<span data-ttu-id="6fc73-137">如果您想 toolink DNS 區域寫入 hello 通用 DNS 的階層 – 這個控制項可讓 DNS 查詢從任何地方 hello world toofind 中 DNS 區域，並回答您的 DNS 記錄，就會需要 toopurchase hello 網域名稱。</span><span class="sxs-lookup"><span data-stu-id="6fc73-137">You need toopurchase hello domain name if you want toolink your DNS zone into hello global DNS hierarchy – this enables DNS queries from anywhere in hello world toofind your DNS zone and be answered with your DNS records.</span></span>

## <a name="azure-dns-features"></a><span data-ttu-id="6fc73-138">Azure DNS 功能</span><span class="sxs-lookup"><span data-stu-id="6fc73-138">Azure DNS Features</span></span>

### <a name="does-azure-dns-support-dns-based-traffic-routing-or-endpoint-failover"></a><span data-ttu-id="6fc73-139">Azure DNS 是否支援 DNS 型流量路由或端點容錯移轉？</span><span class="sxs-lookup"><span data-stu-id="6fc73-139">Does Azure DNS support DNS-based traffic routing or endpoint failover?</span></span>

<span data-ttu-id="6fc73-140">DNS 型流量路由和端點容錯移轉是由「Azure 流量管理員」所提供。</span><span class="sxs-lookup"><span data-stu-id="6fc73-140">DNS-based traffic routing and endpoint failover are provided by Azure Traffic Manager.</span></span> <span data-ttu-id="6fc73-141">這是一項可以與 Azure DNS 一起使用的個別 Azure 服務。</span><span class="sxs-lookup"><span data-stu-id="6fc73-141">This is a separate Azure service that can be used together with Azure DNS.</span></span> <span data-ttu-id="6fc73-142">如需詳細資訊，請參閱 hello [Traffic Manager 概述](../traffic-manager/traffic-manager-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="6fc73-142">For more information, see hello [Traffic Manager overview](../traffic-manager/traffic-manager-overview.md).</span></span>

<span data-ttu-id="6fc73-143">Azure DNS 僅支援裝載 'static' 的 DNS 網域，每個指定的 DNS 記錄的 DNS 查詢永遠接收 hello 相同的 DNS 回應。</span><span class="sxs-lookup"><span data-stu-id="6fc73-143">Azure DNS only supports hosting 'static' DNS domains, where each DNS query for a given DNS record always receives hello same DNS response.</span></span>

### <a name="does-azure-dns-support-domain-name-registration"></a><span data-ttu-id="6fc73-144">Azure DNS 是否支援網域名稱註冊？</span><span class="sxs-lookup"><span data-stu-id="6fc73-144">Does Azure DNS support domain name registration?</span></span>

<span data-ttu-id="6fc73-145">否。</span><span class="sxs-lookup"><span data-stu-id="6fc73-145">No.</span></span> <span data-ttu-id="6fc73-146">Azure DNS 目前不支援購買網域名稱。</span><span class="sxs-lookup"><span data-stu-id="6fc73-146">Azure DNS does not currently support purchasing of domain names.</span></span> <span data-ttu-id="6fc73-147">如果您想 toopurchase 網域時，您會需要 toouse 第三方網域名稱註冊機構。</span><span class="sxs-lookup"><span data-stu-id="6fc73-147">If you want toopurchase domains, you need toouse a third-party domain name registrar.</span></span> <span data-ttu-id="6fc73-148">hello 註冊機構通常費用小年費。</span><span class="sxs-lookup"><span data-stu-id="6fc73-148">hello registrar typically charges a small annual fee.</span></span> <span data-ttu-id="6fc73-149">hello 網域的 DNS 記錄管理然後裝載在 Azure DNS。</span><span class="sxs-lookup"><span data-stu-id="6fc73-149">hello domains can then be hosted in Azure DNS for management of DNS records.</span></span> <span data-ttu-id="6fc73-150">請參閱[委派網域 tooAzure DNS](dns-domain-delegation.md)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="6fc73-150">See [Delegate a Domain tooAzure DNS](dns-domain-delegation.md) for details.</span></span>

<span data-ttu-id="6fc73-151">這是我們的待處理項目上所追蹤的一項功能。</span><span class="sxs-lookup"><span data-stu-id="6fc73-151">This is a feature we are tracking on our backlog.</span></span> <span data-ttu-id="6fc73-152">您也可以使用我們的意見反應網站[註冊您的支援這項功能以](https://feedback.azure.com/forums/217313-networking/suggestions/4996615-azure-should-be-its-own-domain-registrar)。</span><span class="sxs-lookup"><span data-stu-id="6fc73-152">You can use our feedback site too[register your support for this feature](https://feedback.azure.com/forums/217313-networking/suggestions/4996615-azure-should-be-its-own-domain-registrar).</span></span>

### <a name="does-azure-dns-support-private-domains"></a><span data-ttu-id="6fc73-153">Azure DNS 是否支援「私人」網域？</span><span class="sxs-lookup"><span data-stu-id="6fc73-153">Does Azure DNS support 'private' domains?</span></span>

<span data-ttu-id="6fc73-154">否。</span><span class="sxs-lookup"><span data-stu-id="6fc73-154">No.</span></span> <span data-ttu-id="6fc73-155">Azure DNS 目前只支援網際網路對向網域。</span><span class="sxs-lookup"><span data-stu-id="6fc73-155">Azure DNS currently only supports Internet-facing domains.</span></span>

<span data-ttu-id="6fc73-156">這是我們的待處理項目上所追蹤的一項功能。</span><span class="sxs-lookup"><span data-stu-id="6fc73-156">This is a feature we are tracking on our backlog.</span></span> <span data-ttu-id="6fc73-157">您也可以使用我們的意見反應網站[註冊您的支援這項功能以](https://feedback.azure.com/forums/217313-networking/suggestions/10737696-enable-split-dns-for-providing-both-public-and-int)。</span><span class="sxs-lookup"><span data-stu-id="6fc73-157">You can use our feedback site too[register your support for this feature](https://feedback.azure.com/forums/217313-networking/suggestions/10737696-enable-split-dns-for-providing-both-public-and-int).</span></span>

<span data-ttu-id="6fc73-158">如需有關 Azure 中內部 DNS 選項的資訊，請參閱 [VM 與角色執行個體的名稱解析](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md)。</span><span class="sxs-lookup"><span data-stu-id="6fc73-158">For information on internal DNS options in Azure, see [Name Resolution for VMs and Role Instances](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).</span></span>

### <a name="does-azure-dns-support-dnssec"></a><span data-ttu-id="6fc73-159">Azure DNS 是否支援 DNSSEC？</span><span class="sxs-lookup"><span data-stu-id="6fc73-159">Does Azure DNS support DNSSEC?</span></span>

<span data-ttu-id="6fc73-160">否。</span><span class="sxs-lookup"><span data-stu-id="6fc73-160">No.</span></span> <span data-ttu-id="6fc73-161">Azure DNS 目前不支援 DNSSEC。</span><span class="sxs-lookup"><span data-stu-id="6fc73-161">Azure DNS does not currently support DNSSEC.</span></span>

<span data-ttu-id="6fc73-162">這是我們的待處理項目上所追蹤的一項功能。</span><span class="sxs-lookup"><span data-stu-id="6fc73-162">This is a feature we are tracking on our backlog.</span></span> <span data-ttu-id="6fc73-163">您也可以使用我們的意見反應網站[註冊您的支援這項功能以](https://feedback.azure.com/forums/217313-networking/suggestions/13284393-azure-dns-needs-dnssec-support)。</span><span class="sxs-lookup"><span data-stu-id="6fc73-163">You can use our feedback site too[register your support for this feature](https://feedback.azure.com/forums/217313-networking/suggestions/13284393-azure-dns-needs-dnssec-support).</span></span>

### <a name="does-azure-dns-support-zone-transfers-axfrixfr"></a><span data-ttu-id="6fc73-164">Azure DNS 是否支援區域傳輸 (AXFR/IXFR)？</span><span class="sxs-lookup"><span data-stu-id="6fc73-164">Does Azure DNS support zone transfers (AXFR/IXFR)?</span></span>

<span data-ttu-id="6fc73-165">否。</span><span class="sxs-lookup"><span data-stu-id="6fc73-165">No.</span></span> <span data-ttu-id="6fc73-166">Azure DNS 目前不支援區域傳輸。</span><span class="sxs-lookup"><span data-stu-id="6fc73-166">Azure DNS does not currently support zone transfers.</span></span> <span data-ttu-id="6fc73-167">DNS 區域可以是[匯入至 Azure DNS 使用 hello Azure CLI](dns-import-export.md)。</span><span class="sxs-lookup"><span data-stu-id="6fc73-167">DNS zones can be [imported into Azure DNS using hello Azure CLI](dns-import-export.md).</span></span> <span data-ttu-id="6fc73-168">DNS 記錄管理透過 hello [Azure DNS 管理入口網站](dns-operations-recordsets-portal.md)，我們[REST API](https://docs.microsoft.com/powershell/module/azurerm.dns)， [SDK](dns-sdk.md)， [PowerShell cmdlet](dns-operations-recordsets.md)，或[CLI 工具](dns-operations-recordsets-cli.md)。</span><span class="sxs-lookup"><span data-stu-id="6fc73-168">DNS records can then be managed via hello [Azure DNS management portal](dns-operations-recordsets-portal.md), our [REST API](https://docs.microsoft.com/powershell/module/azurerm.dns), [SDK](dns-sdk.md), [PowerShell cmdlets](dns-operations-recordsets.md), or [CLI tool](dns-operations-recordsets-cli.md).</span></span>

<span data-ttu-id="6fc73-169">這是我們的待處理項目上所追蹤的一項功能。</span><span class="sxs-lookup"><span data-stu-id="6fc73-169">This is a feature we are tracking on our backlog.</span></span> <span data-ttu-id="6fc73-170">您也可以使用我們的意見反應網站[註冊您的支援這項功能以](https://feedback.azure.com/forums/217313-networking/suggestions/12925503-extend-azure-dns-to-support-zone-transfers-so-it-c)。</span><span class="sxs-lookup"><span data-stu-id="6fc73-170">You can use our feedback site too[register your support for this feature](https://feedback.azure.com/forums/217313-networking/suggestions/12925503-extend-azure-dns-to-support-zone-transfers-so-it-c).</span></span>

### <a name="does-azure-dns-support-url-redirects"></a><span data-ttu-id="6fc73-171">Azure DNS 是否支援 URL 重新導向？</span><span class="sxs-lookup"><span data-stu-id="6fc73-171">Does Azure DNS support URL redirects?</span></span>

<span data-ttu-id="6fc73-172">否。</span><span class="sxs-lookup"><span data-stu-id="6fc73-172">No.</span></span> <span data-ttu-id="6fc73-173">URL 重新導向服務不是實際的 DNS 服務-hello HTTP 層級，而非 hello DNS 層級運作。</span><span class="sxs-lookup"><span data-stu-id="6fc73-173">URL redirect services are not actually a DNS service - they work at hello HTTP level, rather than hello DNS level.</span></span> <span data-ttu-id="6fc73-174">某些 DNS 提供者 toobundle URL 重新導向服務做為其整體的供應項目的一部分。</span><span class="sxs-lookup"><span data-stu-id="6fc73-174">Some DNS providers toobundle a URL redirect service as part of their overall offering.</span></span> <span data-ttu-id="6fc73-175">Azure DNS 目前不支援此做法。</span><span class="sxs-lookup"><span data-stu-id="6fc73-175">This is not currently supported by Azure DNS.</span></span>

<span data-ttu-id="6fc73-176">這項功能列入我們的待處理項目追蹤。</span><span class="sxs-lookup"><span data-stu-id="6fc73-176">This feature is tracked on our backlog.</span></span> <span data-ttu-id="6fc73-177">您也可以使用我們的意見反應網站[註冊您的支援這項功能以](https://feedback.azure.com/forums/217313-networking/suggestions/10109736-provide-a-301-permanent-redirect-service-for-ape)。</span><span class="sxs-lookup"><span data-stu-id="6fc73-177">You can use our feedback site too[register your support for this feature](https://feedback.azure.com/forums/217313-networking/suggestions/10109736-provide-a-301-permanent-redirect-service-for-ape).</span></span>

## <a name="using-azure-dns"></a><span data-ttu-id="6fc73-178">使用 Azure DNS</span><span class="sxs-lookup"><span data-stu-id="6fc73-178">Using Azure DNS</span></span>

### <a name="can-i-co-host-a-domain-using-azure-dns-and-another-dns-provider"></a><span data-ttu-id="6fc73-179">我是否可以使用 Azure DNS 和另一個 DNS 提供者來共同裝載某個網域？</span><span class="sxs-lookup"><span data-stu-id="6fc73-179">Can I co-host a domain using Azure DNS and another DNS provider?</span></span>

<span data-ttu-id="6fc73-180">是。</span><span class="sxs-lookup"><span data-stu-id="6fc73-180">Yes.</span></span> <span data-ttu-id="6fc73-181">Azure DNS 支援與其他 DNS 服務共同裝載網域。</span><span class="sxs-lookup"><span data-stu-id="6fc73-181">Azure DNS supports co-hosting domains with other DNS services.</span></span>

<span data-ttu-id="6fc73-182">toodo 因此，您需要 toomodify hello NS 記錄 （哪一個控制項的提供者會收到 DNS 查詢以取得 hello 網域） 的 hello 網域 toopoint toohello 名稱伺服器的兩個提供者。</span><span class="sxs-lookup"><span data-stu-id="6fc73-182">toodo so, you need toomodify hello NS records for hello domain (which control which providers receive DNS queries for hello domain) toopoint toohello name servers of both providers.</span></span> <span data-ttu-id="6fc73-183">這些 NS 記錄需要修改 3 身處 toobe: Azure DNS 中的 在 hello 其他提供者，在 hello 上層區域 （透過 hello 網域名稱註冊機構通常會設定）。</span><span class="sxs-lookup"><span data-stu-id="6fc73-183">These NS records need toobe modified in 3 places: in Azure DNS, in hello other provider, and in hello parent zone (typically configured via hello domain name registrar).</span></span> <span data-ttu-id="6fc73-184">如需有關 DNS 委派的詳細資訊，請參閱 [DNS 網域委派](dns-domain-delegation.md)。</span><span class="sxs-lookup"><span data-stu-id="6fc73-184">For more information on DNS delegation, see [DNS domain delegation](dns-domain-delegation.md).</span></span>

<span data-ttu-id="6fc73-185">此外，您需要 tooensure hello hello 網域的 DNS 記錄是這兩個 DNS 提供者之間的同步處理。</span><span class="sxs-lookup"><span data-stu-id="6fc73-185">In addition, you need tooensure that hello DNS records for hello domain are in sync between both DNS providers.</span></span> <span data-ttu-id="6fc73-186">Azure DNS 目前不支援 DNS 區域傳輸。</span><span class="sxs-lookup"><span data-stu-id="6fc73-186">Azure DNS does not currently support DNS zone transfers.</span></span> <span data-ttu-id="6fc73-187">您必須使用其中一個 hello toosynchronize DNS 記錄[Azure DNS 管理入口網站](dns-operations-recordsets-portal.md)，我們[REST API](https://docs.microsoft.com/powershell/module/azurerm.dns)， [SDK](dns-sdk.md)， [PowerShell cmdlet](dns-operations-recordsets.md)或[CLI 工具](dns-operations-recordsets-cli.md)。</span><span class="sxs-lookup"><span data-stu-id="6fc73-187">You need toosynchronize DNS records using either hello [Azure DNS management portal](dns-operations-recordsets-portal.md), our [REST API](https://docs.microsoft.com/powershell/module/azurerm.dns), [SDK](dns-sdk.md), [PowerShell cmdlets](dns-operations-recordsets.md), or [CLI tool](dns-operations-recordsets-cli.md).</span></span>

### <a name="do-i-have-toodelegate-my-domain-tooall-4-azure-dns-name-servers"></a><span data-ttu-id="6fc73-188">我是否必須 toodelegate 我網域 tooall 4 Azure DNS 名稱伺服器？</span><span class="sxs-lookup"><span data-stu-id="6fc73-188">Do I have toodelegate my domain tooall 4 Azure DNS name servers?</span></span>

<span data-ttu-id="6fc73-189">是。</span><span class="sxs-lookup"><span data-stu-id="6fc73-189">Yes.</span></span> <span data-ttu-id="6fc73-190">Azure DNS 指派 4 名稱伺服器 tooeach DNS 區域，錯誤隔離和增加的恢復功能。</span><span class="sxs-lookup"><span data-stu-id="6fc73-190">Azure DNS assigns 4 name servers tooeach DNS zone, for fault isolation and increased resilience.</span></span> <span data-ttu-id="6fc73-191">如 tooqualify hello Azure DNS SLA，您需要 toodelegate 您網域 tooall 4 的名稱伺服器。</span><span class="sxs-lookup"><span data-stu-id="6fc73-191">tooqualify for hello Azure DNS SLA, you need toodelegate your domain tooall 4 name servers.</span></span>

### <a name="what-are-hello-usage-limits-for-azure-dns"></a><span data-ttu-id="6fc73-192">什麼是 Azure DNS 的 hello 使用量限制？</span><span class="sxs-lookup"><span data-stu-id="6fc73-192">What are hello usage limits for Azure DNS?</span></span>

<span data-ttu-id="6fc73-193">使用 Azure DNS 時，適用下列預設限制 hello:</span><span class="sxs-lookup"><span data-stu-id="6fc73-193">hello following default limits apply when using Azure DNS:</span></span>

[!INCLUDE [dns-limits](../../includes/dns-limits.md)]

### <a name="can-i-move-an-azure-dns-zone-between-resource-groups-or-between-subscriptions"></a><span data-ttu-id="6fc73-194">我是否可以在資源群組之間或訂用帳戶之間移動 Azure DNS 區域？</span><span class="sxs-lookup"><span data-stu-id="6fc73-194">Can I move an Azure DNS zone between resource groups or between subscriptions?</span></span>

<span data-ttu-id="6fc73-195">是。</span><span class="sxs-lookup"><span data-stu-id="6fc73-195">Yes.</span></span> <span data-ttu-id="6fc73-196">您可以在資源群組之間或訂用帳戶之間移動 DNS 區域。</span><span class="sxs-lookup"><span data-stu-id="6fc73-196">DNS zones can be moved between resource groups, or between subscriptions.</span></span>

<span data-ttu-id="6fc73-197">移動 DNS 區域時，對 DNS 查詢並沒有影響。</span><span class="sxs-lookup"><span data-stu-id="6fc73-197">There is no impact on DNS queries when moving a DNS zone.</span></span> <span data-ttu-id="6fc73-198">hello 分派 toohello 區域的名稱伺服器保持的 hello 與 DNS 查詢處理為整個標準。</span><span class="sxs-lookup"><span data-stu-id="6fc73-198">hello name servers assigned toohello zone remain hello same, and DNS queries are processed as normal throughout.</span></span>

<span data-ttu-id="6fc73-199">如需詳細資訊和指示 toomove DNS 區域，請參閱[移動資源 tooa 新資源群組或訂用帳戶](../azure-resource-manager/resource-group-move-resources.md)。</span><span class="sxs-lookup"><span data-stu-id="6fc73-199">For more information and instructions on how toomove DNS zones, see [Move resources tooa new resource group or subscription](../azure-resource-manager/resource-group-move-resources.md).</span></span>

### <a name="how-long-does-it-take-for-dns-changes-tootake-effect"></a><span data-ttu-id="6fc73-200">多久需要 DNS 變更 tootake 效果？</span><span class="sxs-lookup"><span data-stu-id="6fc73-200">How long does it take for DNS changes tootake effect?</span></span>

<span data-ttu-id="6fc73-201">新的 DNS 區域與 DNS 記錄會通常被反映在 hello Azure DNS 名稱伺服器快速，在幾秒鐘內。</span><span class="sxs-lookup"><span data-stu-id="6fc73-201">New DNS zones and DNS records are typically reflected on hello Azure DNS name servers quickly, within a few seconds.</span></span>

<span data-ttu-id="6fc73-202">變更 tooexisting DNS 記錄可能需要較長的時間，但應該仍會反映在 hello Azure DNS 名稱伺服器上 60 秒內。</span><span class="sxs-lookup"><span data-stu-id="6fc73-202">Changes tooexisting DNS records can take a little longer, but should still be reflected on hello Azure DNS name servers within 60 seconds.</span></span> <span data-ttu-id="6fc73-203">在此情況下，DNS 快取之外 Azure DNS （藉由 DNS 用戶端和 DNS 遞迴解析程式） 可能也會影響 hello 的時間 DNS 變更 toobe 有效。</span><span class="sxs-lookup"><span data-stu-id="6fc73-203">In this case, DNS caching outside of Azure DNS (by DNS clients and DNS recursive resolvers) can also impact hello time taken for a DNS change toobe effective.</span></span> <span data-ttu-id="6fc73-204">可以使用的每個資料錄集的 hello 存留時間 (TTL) 屬性來控制此快取持續時間。</span><span class="sxs-lookup"><span data-stu-id="6fc73-204">This cache duration can be controlled using hello Time-To-Live (TTL) property of each record set.</span></span>

### <a name="how-can-i-protect-my-dns-zones-against-accidental-deletion"></a><span data-ttu-id="6fc73-205">我要如何保護我的 DNS 區域免於遭到意外刪除？</span><span class="sxs-lookup"><span data-stu-id="6fc73-205">How can I protect my DNS zones against accidental deletion?</span></span>

<span data-ttu-id="6fc73-206">使用 Azure 資源管理員，來管理 azure DNS 及 hello 的存取控制功能的 Azure 資源管理員提供。</span><span class="sxs-lookup"><span data-stu-id="6fc73-206">Azure DNS is managed using Azure Resource Manager, and benefits from hello access control features that Azure Resource Manager provides.</span></span> <span data-ttu-id="6fc73-207">以角色為基礎的存取控制可以使用的 toocontrol 哪些使用者可以讀取或寫入存取 tooDNS 區域和資料錄集。</span><span class="sxs-lookup"><span data-stu-id="6fc73-207">Role-based access control can be used toocontrol which users have read or write access tooDNS zones and record sets.</span></span> <span data-ttu-id="6fc73-208">資源鎖定可以被套用的 tooprevent 意外修改或刪除 DNS 區域和資料錄集。</span><span class="sxs-lookup"><span data-stu-id="6fc73-208">Resource locks can be applied tooprevent accidental modification or deletion of DNS zones and record sets.</span></span>

<span data-ttu-id="6fc73-209">如需詳細資訊，請參閱[保護 DNS 區域和記錄](dns-protect-zones-recordsets.md)。</span><span class="sxs-lookup"><span data-stu-id="6fc73-209">For more information, see [Protecting DNS Zones and Records](dns-protect-zones-recordsets.md).</span></span>

### <a name="how-do-i-set-up-spf-records-in-azure-dns"></a><span data-ttu-id="6fc73-210">我要如何設定 Azure DNS 中的 SPF 記錄？</span><span class="sxs-lookup"><span data-stu-id="6fc73-210">How do I set up SPF records in Azure DNS?</span></span>

[!INCLUDE [dns-spf-include](../../includes/dns-spf-include.md)]

### <a name="how-do-i-set-up-an-international-domain-name-idn-in-azure-dns"></a><span data-ttu-id="6fc73-211">我要如何設定 Azure DNS 中的「國際網域名稱」(IDN)？</span><span class="sxs-lookup"><span data-stu-id="6fc73-211">How do I set up an International Domain Name (IDN) in Azure DNS?</span></span>

<span data-ttu-id="6fc73-212">「國際網域名稱」(IDN) 的運作方式是使用 '[Punycode](https://en.wikipedia.org/wiki/Punycode)' 將每個 DNS 名稱編碼。</span><span class="sxs-lookup"><span data-stu-id="6fc73-212">International Domain Names (IDNs) work by encoding each DNS name using '[punycode](https://en.wikipedia.org/wiki/Punycode)'.</span></span> <span data-ttu-id="6fc73-213">建立 DNS 查詢時，會使用這些以 Punycode 編碼的名稱來建立。</span><span class="sxs-lookup"><span data-stu-id="6fc73-213">DNS queries are made using these punycode-encoded names.</span></span>

<span data-ttu-id="6fc73-214">您可以在 Azure DNS 中設定國際網域名稱 (Idn) 的第一個轉換 hello 區域名稱或設定名稱 toopunycode 記錄。</span><span class="sxs-lookup"><span data-stu-id="6fc73-214">You can configure International Domain Names (IDNs) in Azure DNS by first converting hello zone name or record set name toopunycode.</span></span> <span data-ttu-id="6fc73-215">Azure DNS 目前不支援以 Punycode 作為轉換目標或來源的內建轉換。</span><span class="sxs-lookup"><span data-stu-id="6fc73-215">Azure DNS does not currently support built-in conversion to/from punycode.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6fc73-216">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6fc73-216">Next steps</span></span>

<span data-ttu-id="6fc73-217">[深入了解 Azure DNS](dns-overview.md)
</span><span class="sxs-lookup"><span data-stu-id="6fc73-217">[Learn more about Azure DNS](dns-overview.md)
</span></span><br><span data-ttu-id="6fc73-218">
[深入了解 DNS 區域和記錄](dns-zones-records.md)
</span><span class="sxs-lookup"><span data-stu-id="6fc73-218">
[Learn more about DNS zones and records](dns-zones-records.md)
</span></span><br><span data-ttu-id="6fc73-219">
[開始使用 Azure DNS](dns-getstarted-portal.md)</span><span class="sxs-lookup"><span data-stu-id="6fc73-219">
[Get started with Azure DNS](dns-getstarted-portal.md)</span></span>

