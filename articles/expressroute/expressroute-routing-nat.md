---
title: "適用於 Azure ExpressRoute 的 NAT | Microsoft Docs"
description: "此頁面提供用來設定和管理 ExpressRoute 循環路由的詳細需求。"
documentationcenter: na
services: expressroute
author: osamazia
manager: ganesr
editor: 
ms.assetid: eaaf0393-d384-4496-9a5c-328e94c262a7
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/12/2017
ms.author: osamam
ms.openlocfilehash: 7a8b760df90b545b5fbde2f614aef62dd3985bb6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="nat-for-expressroute"></a><span data-ttu-id="e655e-103">適用於 ExpressRoute 的 NAT</span><span class="sxs-lookup"><span data-stu-id="e655e-103">NAT for ExpressRoute</span></span>

<span data-ttu-id="e655e-104">使用 ExpressRoute tooconnect tooMicrosoft 雲端服務，您將需要 tooset 註冊和管理路由。</span><span class="sxs-lookup"><span data-stu-id="e655e-104">tooconnect tooMicrosoft cloud services using ExpressRoute, you’ll need tooset up and manage routing.</span></span> <span data-ttu-id="e655e-105">有些連線提供者會以受管理的服務形式提供路由的設定和管理。</span><span class="sxs-lookup"><span data-stu-id="e655e-105">Some connectivity providers offer setting up and managing routing as a managed service.</span></span> <span data-ttu-id="e655e-106">如果提供了這項服務，請洽詢您的連線提供者 toosee。</span><span class="sxs-lookup"><span data-stu-id="e655e-106">Check with your connectivity provider toosee if they offer this service.</span></span> <span data-ttu-id="e655e-107">如果沒有，您必須遵守下列需求的 toohello。</span><span class="sxs-lookup"><span data-stu-id="e655e-107">If they don't, you must adhere toohello following requirements.</span></span> 

<span data-ttu-id="e655e-108">請參閱 toohello[線路和路由網域](expressroute-circuit-peerings.md)hello 路由的說明文章需要 toobe 的工作階段中 toofacilitate 連線設定。</span><span class="sxs-lookup"><span data-stu-id="e655e-108">Refer toohello [Circuits and routing domains](expressroute-circuit-peerings.md) article for a description of hello routing sessions that need toobe set up in toofacilitate connectivity.</span></span>

> [!NOTE]
> <span data-ttu-id="e655e-109">Microsoft 不支援任何高可用性組態的路由器備援通訊協定 (如 HSRP、VRRP)。</span><span class="sxs-lookup"><span data-stu-id="e655e-109">Microsoft does not support any router redundancy protocols (e.g., HSRP, VRRP) for high availability configurations.</span></span> <span data-ttu-id="e655e-110">我們依賴每個對等互連的一組備援 BGP 工作階段來取得高可用性。</span><span class="sxs-lookup"><span data-stu-id="e655e-110">We rely on a redundant pair of BGP sessions per peering for high availability.</span></span>
> 
> 

## <a name="ip-addresses-used-for-peerings"></a><span data-ttu-id="e655e-111">用於對等互連的 IP 位址</span><span class="sxs-lookup"><span data-stu-id="e655e-111">IP addresses used for peerings</span></span>

<span data-ttu-id="e655e-112">您需要 tooreserve 幾個區塊的 IP 位址 tooconfigure 路由在網路與 Microsoft 的企業邊緣 (MSEEs) 路由器之間。</span><span class="sxs-lookup"><span data-stu-id="e655e-112">You need tooreserve a few blocks of IP addresses tooconfigure routing between your network and Microsoft's Enterprise edge (MSEEs) routers.</span></span> <span data-ttu-id="e655e-113">本節提供一份需求，並描述 hello 規則必須如何取得及使用這些 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="e655e-113">This section provides a list of requirements and describes hello rules regarding how these IP addresses must be acquired and used.</span></span>

### <a name="ip-addresses-used-for-azure-private-peering"></a><span data-ttu-id="e655e-114">用於 Azure 私人對等互連的 IP 位址</span><span class="sxs-lookup"><span data-stu-id="e655e-114">IP addresses used for Azure private peering</span></span>

<span data-ttu-id="e655e-115">您可以使用私人 IP 位址或公用 IP 位址 tooconfigure hello 對等互連。</span><span class="sxs-lookup"><span data-stu-id="e655e-115">You can use either private IP addresses or public IP addresses tooconfigure hello peerings.</span></span> <span data-ttu-id="e655e-116">hello 可用來設定路由的位址範圍不得與 Azure 中的位址範圍使用 toocreate 虛擬網路重疊。</span><span class="sxs-lookup"><span data-stu-id="e655e-116">hello address range used for configuring routes must not overlap with address ranges used toocreate virtual networks in Azure.</span></span> 

* <span data-ttu-id="e655e-117">您必須為路由介面保留一個 /29 子網路或兩個 /30 子網路。</span><span class="sxs-lookup"><span data-stu-id="e655e-117">You must reserve a /29 subnet or two /30 subnets for routing interfaces.</span></span>
* <span data-ttu-id="e655e-118">用於路由傳送嗨子網路可以是私人 IP 位址或公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="e655e-118">hello subnets used for routing can be either private IP addresses or public IP addresses.</span></span>
* <span data-ttu-id="e655e-119">hello 子網路不必須與用於 hello Microsoft 雲端中的 hello 客戶所保留的 hello 範圍發生衝突。</span><span class="sxs-lookup"><span data-stu-id="e655e-119">hello subnets must not conflict with hello range reserved by hello customer for use in hello Microsoft cloud.</span></span>
* <span data-ttu-id="e655e-120">如果使用 /29 子網路，它就會分割成兩個 /30 子網路。</span><span class="sxs-lookup"><span data-stu-id="e655e-120">If a /29 subnet is used, it will be split into two /30 subnets.</span></span> 
  * <span data-ttu-id="e655e-121">第一次 hello/30 子網路將用於 hello 主要連結和 hello 第二個/30 子網路將用於 hello 次要連結。</span><span class="sxs-lookup"><span data-stu-id="e655e-121">hello first /30 subnet will be used for hello primary link and hello second /30 subnet will be used for hello secondary link.</span></span>
  * <span data-ttu-id="e655e-122">針對每個 hello/30 子網路，您必須在路由器上使用 hello/30 子網路的 hello 第一個 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="e655e-122">For each of hello /30 subnets, you must use hello first IP address of hello /30 subnet on your router.</span></span> <span data-ttu-id="e655e-123">Microsoft 會使用 BGP 工作階段的 hello/30 子網路 tooset hello 第二個 IP 的位址。</span><span class="sxs-lookup"><span data-stu-id="e655e-123">Microsoft will use hello second IP address of hello /30 subnet tooset up a BGP session.</span></span>
  * <span data-ttu-id="e655e-124">您必須設定兩個 BGP 工作階段，如我們[可用性 SLA](https://azure.microsoft.com/support/legal/sla/) toobe 有效。</span><span class="sxs-lookup"><span data-stu-id="e655e-124">You must set up both BGP sessions for our [availability SLA](https://azure.microsoft.com/support/legal/sla/) toobe valid.</span></span>  

#### <a name="example-for-private-peering"></a><span data-ttu-id="e655e-125">私人對等互連範例</span><span class="sxs-lookup"><span data-stu-id="e655e-125">Example for private peering</span></span>

<span data-ttu-id="e655e-126">如果您選擇 toouse a.b.c.d/29 tooset 向上 hello 對等互連，它會分成兩個的/30 子網路。</span><span class="sxs-lookup"><span data-stu-id="e655e-126">If you choose toouse a.b.c.d/29 tooset up hello peering, it will be split into two /30 subnets.</span></span> <span data-ttu-id="e655e-127">Hello 下列範例中，我們將探討如何使用 hello a.b.c.d/29 子網路。</span><span class="sxs-lookup"><span data-stu-id="e655e-127">In hello example below, we will look at how hello a.b.c.d/29 subnet is used.</span></span> 

<span data-ttu-id="e655e-128">a.b.c.d/29 會分割 tooa.b.c.d/30 而 a.b.c.d+4/30 和 hello 佈建應用程式開發介面透過 tooMicrosoft 中傳遞。</span><span class="sxs-lookup"><span data-stu-id="e655e-128">a.b.c.d/29 will be split tooa.b.c.d/30 and a.b.c.d+4/30 and passed down tooMicrosoft through hello provisioning APIs.</span></span> <span data-ttu-id="e655e-129">您將使用 a.b.c.d+1 hello VRF IP 的 hello 主要 PE 和 Microsoft 會耗用 a.b.c.d+2 為 hello VRF IP hello 主要 MSEE 如下。</span><span class="sxs-lookup"><span data-stu-id="e655e-129">You will use a.b.c.d+1 as hello VRF IP for hello Primary PE and Microsoft will consume a.b.c.d+2 as hello VRF IP for hello primary MSEE.</span></span> <span data-ttu-id="e655e-130">您將使用 a.b.c.d+5 hello VRF IP hello 次要 PE 和 Microsoft 將使用 a.b.c.d+6 為 hello VRF IP hello 次要 MSEE 如下。</span><span class="sxs-lookup"><span data-stu-id="e655e-130">You will use a.b.c.d+5 as hello VRF IP for hello secondary PE and Microsoft will use a.b.c.d+6 as hello VRF IP for hello secondary MSEE.</span></span>

<span data-ttu-id="e655e-131">試想一個情況，您在其中選取 192.168.100.128/29 tooset 註冊私用對等互連。</span><span class="sxs-lookup"><span data-stu-id="e655e-131">Consider a case where you select 192.168.100.128/29 tooset up private peering.</span></span> <span data-ttu-id="e655e-132">192.168.100.128/29 192.168.100.128 位址包含 too192.168.100.135，在這些：</span><span class="sxs-lookup"><span data-stu-id="e655e-132">192.168.100.128/29 includes addresses from 192.168.100.128 too192.168.100.135, among which:</span></span>

* <span data-ttu-id="e655e-133">192.168.100.128/30 會指派 toolink1，與使用 192.168.100.129 和 Microsoft 使用 192.168.100.130 的提供者。</span><span class="sxs-lookup"><span data-stu-id="e655e-133">192.168.100.128/30 will be assigned toolink1, with provider using 192.168.100.129 and Microsoft using 192.168.100.130.</span></span>
* <span data-ttu-id="e655e-134">192.168.100.132/30 會指派 toolink2，與使用 192.168.100.133 和 Microsoft 使用 192.168.100.134 的提供者。</span><span class="sxs-lookup"><span data-stu-id="e655e-134">192.168.100.132/30 will be assigned toolink2, with provider using 192.168.100.133 and Microsoft using 192.168.100.134.</span></span>

### <a name="ip-addresses-used-for-azure-public-and-microsoft-peering"></a><span data-ttu-id="e655e-135">用於 Azure 公用與 Microsoft 對等互連的 IP 位址</span><span class="sxs-lookup"><span data-stu-id="e655e-135">IP addresses used for Azure public and Microsoft peering</span></span>

<span data-ttu-id="e655e-136">您必須使用您自己的公用 IP 位址設定 hello BGP 工作階段。</span><span class="sxs-lookup"><span data-stu-id="e655e-136">You must use public IP addresses that you own for setting up hello BGP sessions.</span></span> <span data-ttu-id="e655e-137">Microsoft 必須能夠 tooverify hello 擁有權的 hello 透過路由網際網路登錄和網際網路路由所登錄的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="e655e-137">Microsoft must be able tooverify hello ownership of hello IP addresses through Routing Internet Registries and Internet Routing Registries.</span></span> 

* <span data-ttu-id="e655e-138">您必須使用唯一/29 子網路或兩個的/30 子網路 tooset 向上 hello BGP 對等每個對等互連每個 ExpressRoute 電路 （如果您有多個）。</span><span class="sxs-lookup"><span data-stu-id="e655e-138">You must use a unique /29 subnet or two /30 subnets tooset up hello BGP peering for each peering per ExpressRoute circuit (if you have more than one).</span></span> 
* <span data-ttu-id="e655e-139">如果使用 /29 子網路，它就會分割成兩個 /30 子網路。</span><span class="sxs-lookup"><span data-stu-id="e655e-139">If a /29 subnet is used, it will be split into two /30 subnets.</span></span> 
  * <span data-ttu-id="e655e-140">第一次 hello/30 子網路將用於 hello 主要連結和 hello 第二個/30 子網路將用於 hello 次要連結。</span><span class="sxs-lookup"><span data-stu-id="e655e-140">hello first /30 subnet will be used for hello primary link and hello second /30 subnet will be used for hello secondary link.</span></span>
  * <span data-ttu-id="e655e-141">針對每個 hello/30 子網路，您必須在路由器上使用 hello/30 子網路的 hello 第一個 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="e655e-141">For each of hello /30 subnets, you must use hello first IP address of hello /30 subnet on your router.</span></span> <span data-ttu-id="e655e-142">Microsoft 會使用 BGP 工作階段的 hello/30 子網路 tooset hello 第二個 IP 的位址。</span><span class="sxs-lookup"><span data-stu-id="e655e-142">Microsoft will use hello second IP address of hello /30 subnet tooset up a BGP session.</span></span>
  * <span data-ttu-id="e655e-143">您必須設定兩個 BGP 工作階段，如我們[可用性 SLA](https://azure.microsoft.com/support/legal/sla/) toobe 有效。</span><span class="sxs-lookup"><span data-stu-id="e655e-143">You must set up both BGP sessions for our [availability SLA](https://azure.microsoft.com/support/legal/sla/) toobe valid.</span></span>

## <a name="public-ip-address-requirement"></a><span data-ttu-id="e655e-144">公用 IP 位址需求</span><span class="sxs-lookup"><span data-stu-id="e655e-144">Public IP address requirement</span></span>

### <a name="private-peering"></a><span data-ttu-id="e655e-145">私人對等互連</span><span class="sxs-lookup"><span data-stu-id="e655e-145">Private Peering</span></span>

<span data-ttu-id="e655e-146">您可以選擇 toouse 用於私人互連的公用或私人 IPv4 位址。</span><span class="sxs-lookup"><span data-stu-id="e655e-146">You can choose toouse public or private IPv4 addresses for private peering.</span></span> <span data-ttu-id="e655e-147">我們會提供流量的端對端隔離，因此在私人對等互連的情況下不可能發生位址與其他客戶重疊。</span><span class="sxs-lookup"><span data-stu-id="e655e-147">We provide end-to-end isolation of your traffic so overlapping of addresses with other customers is not possible in case of private peering.</span></span> <span data-ttu-id="e655e-148">這些位址不是公告的 tooInternet。</span><span class="sxs-lookup"><span data-stu-id="e655e-148">These addresses are not advertised tooInternet.</span></span> 

### <a name="public-peering"></a><span data-ttu-id="e655e-149">公用對等互連</span><span class="sxs-lookup"><span data-stu-id="e655e-149">Public Peering</span></span>

<span data-ttu-id="e655e-150">hello Azure 公用互連路徑可讓您 tooconnect tooall 裝載的服務在 Azure 中透過其公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="e655e-150">hello Azure public peering path enables you tooconnect tooall services hosted in Azure over their public IP addresses.</span></span> <span data-ttu-id="e655e-151">其中包括服務列在 hello [ExpessRoute 常見問題集](expressroute-faqs.md)與任何由 Isv Microsoft Azure 上裝載的服務。</span><span class="sxs-lookup"><span data-stu-id="e655e-151">These include services listed in hello [ExpessRoute FAQ](expressroute-faqs.md) and any services hosted by ISVs on Microsoft Azure.</span></span> <span data-ttu-id="e655e-152">服務連線 tooMicrosoft Azure 公用對等互連一律從起始您的網路到 hello Microsoft 網路。</span><span class="sxs-lookup"><span data-stu-id="e655e-152">Connectivity tooMicrosoft Azure services on public peering is always initiated from your network into hello Microsoft network.</span></span> <span data-ttu-id="e655e-153">Hello 流量預定的 tooMicrosoft 網路，您必須使用公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="e655e-153">You must use Public IP addresses for hello traffic destined tooMicrosoft network.</span></span>

### <a name="microsoft-peering"></a><span data-ttu-id="e655e-154">Microsoft 對等互連</span><span class="sxs-lookup"><span data-stu-id="e655e-154">Microsoft Peering</span></span>

<span data-ttu-id="e655e-155">hello Microsoft 對等互連路徑可讓您透過 hello Azure 公用互連路徑連接 tooMicrosoft 不支援的雲端服務。</span><span class="sxs-lookup"><span data-stu-id="e655e-155">hello Microsoft peering path lets you connect tooMicrosoft cloud services that are not supported through hello Azure public peering path.</span></span> <span data-ttu-id="e655e-156">服務的 hello 清單包含 Office 365 服務，例如 Exchange Online、 SharePoint Online、 商務和 Dynamics 365 Skype。</span><span class="sxs-lookup"><span data-stu-id="e655e-156">hello list of services includes Office 365 services, such as Exchange Online, SharePoint Online, Skype for Business, and Dynamics 365.</span></span> <span data-ttu-id="e655e-157">Microsoft 在 hello Microsoft 對等互連支援雙向連線。</span><span class="sxs-lookup"><span data-stu-id="e655e-157">Microsoft supports bi-directional connectivity on hello Microsoft peering.</span></span> <span data-ttu-id="e655e-158">進入 hello Microsoft 網路之前，資料傳輸 tooMicrosoft 雲端服務必須使用有效的公用 IPv4 位址。</span><span class="sxs-lookup"><span data-stu-id="e655e-158">Traffic destined tooMicrosoft cloud services must use valid public IPv4 addresses before they enter hello Microsoft network.</span></span>

<span data-ttu-id="e655e-159">請確定您的 IP 位址和 AS 號碼會在下面所列的 hello 登錄的其中一個已註冊的 tooyou。</span><span class="sxs-lookup"><span data-stu-id="e655e-159">Make sure that your IP address and AS number are registered tooyou in one of hello registries listed below.</span></span>

* [<span data-ttu-id="e655e-160">ARIN</span><span class="sxs-lookup"><span data-stu-id="e655e-160">ARIN</span></span>](https://www.arin.net/)
* [<span data-ttu-id="e655e-161">APNIC</span><span class="sxs-lookup"><span data-stu-id="e655e-161">APNIC</span></span>](https://www.apnic.net/)
* [<span data-ttu-id="e655e-162">AFRINIC</span><span class="sxs-lookup"><span data-stu-id="e655e-162">AFRINIC</span></span>](https://www.afrinic.net/)
* [<span data-ttu-id="e655e-163">LACNIC</span><span class="sxs-lookup"><span data-stu-id="e655e-163">LACNIC</span></span>](http://www.lacnic.net/)
* [<span data-ttu-id="e655e-164">RIPENCC</span><span class="sxs-lookup"><span data-stu-id="e655e-164">RIPENCC</span></span>](https://www.ripe.net/)
* [<span data-ttu-id="e655e-165">RADB</span><span class="sxs-lookup"><span data-stu-id="e655e-165">RADB</span></span>](http://www.radb.net/)
* [<span data-ttu-id="e655e-166">ALTDB</span><span class="sxs-lookup"><span data-stu-id="e655e-166">ALTDB</span></span>](http://altdb.net/)

> [!IMPORTANT]
> <span data-ttu-id="e655e-167">公用 IP 位址通告透過 ExpressRoute tooMicrosoft 不得公告的 toohello 網際網路。</span><span class="sxs-lookup"><span data-stu-id="e655e-167">Public IP addresses advertised tooMicrosoft over ExpressRoute must not be advertised toohello Internet.</span></span> <span data-ttu-id="e655e-168">這可能會中斷連線 tooother Microsoft 服務。</span><span class="sxs-lookup"><span data-stu-id="e655e-168">This may break connectivity tooother Microsoft services.</span></span> <span data-ttu-id="e655e-169">不過，您的網路中伺服器用來與 Microsoft 內部 O365 端點進行通訊的公用 IP 位址可透過 ExpressRoute 公告。</span><span class="sxs-lookup"><span data-stu-id="e655e-169">However, Public IP addresses used by servers in your network that communicate with O365 endpoints within Microsoft may be advertised over ExpressRoute.</span></span> 
> 
> 

## <a name="dynamic-route-exchange"></a><span data-ttu-id="e655e-170">動態路由交換</span><span class="sxs-lookup"><span data-stu-id="e655e-170">Dynamic route exchange</span></span>

<span data-ttu-id="e655e-171">路由交換將會透過 eBGP 通訊協定。</span><span class="sxs-lookup"><span data-stu-id="e655e-171">Routing exchange will be over eBGP protocol.</span></span> <span data-ttu-id="e655e-172">Hello MSEEs 與您的路由器之間建立 EBGP 的工作階段。</span><span class="sxs-lookup"><span data-stu-id="e655e-172">EBGP sessions are established between hello MSEEs and your routers.</span></span> <span data-ttu-id="e655e-173">不一定需要驗證 BGP 工作階段。</span><span class="sxs-lookup"><span data-stu-id="e655e-173">Authentication of BGP sessions is not a requirement.</span></span> <span data-ttu-id="e655e-174">如有必要，也可以設定 MD5 雜湊。</span><span class="sxs-lookup"><span data-stu-id="e655e-174">If required, an MD5 hash can be configured.</span></span> <span data-ttu-id="e655e-175">請參閱 hello[設定路由](expressroute-howto-routing-classic.md)和[電路的佈建的工作流程和電路狀態](expressroute-workflows.md)設定 BGP 工作階段的資訊。</span><span class="sxs-lookup"><span data-stu-id="e655e-175">See hello [Configure routing](expressroute-howto-routing-classic.md) and [Circuit provisioning workflows and circuit states](expressroute-workflows.md) for information about configuring BGP sessions.</span></span>

## <a name="autonomous-system-numbers"></a><span data-ttu-id="e655e-176">自發系統號碼</span><span class="sxs-lookup"><span data-stu-id="e655e-176">Autonomous System numbers</span></span>

<span data-ttu-id="e655e-177">Microsoft 將使用 AS 12076 進行 Azure 公用、Azure 私人和 Microsoft 對等互連。</span><span class="sxs-lookup"><span data-stu-id="e655e-177">Microsoft will use AS 12076 for Azure public, Azure private and Microsoft peering.</span></span> <span data-ttu-id="e655e-178">我們已從 65515 too65520 供內部使用保留的 Asn。</span><span class="sxs-lookup"><span data-stu-id="e655e-178">We have reserved ASNs from 65515 too65520 for internal use.</span></span> <span data-ttu-id="e655e-179">同時支援 16 和 32 位元號碼。</span><span class="sxs-lookup"><span data-stu-id="e655e-179">Both 16 and 32 bit AS numbers are supported.</span></span>

<span data-ttu-id="e655e-180">資料傳輸對稱沒有任何相關需求。</span><span class="sxs-lookup"><span data-stu-id="e655e-180">There are no requirements around data transfer symmetry.</span></span> <span data-ttu-id="e655e-181">hello 正向和傳回路徑可能會跨越不同的路由器組。</span><span class="sxs-lookup"><span data-stu-id="e655e-181">hello forward and return paths may traverse different router pairs.</span></span> <span data-ttu-id="e655e-182">相同的路由必須從橫跨多個屬於您的循環配對的任一端公告。</span><span class="sxs-lookup"><span data-stu-id="e655e-182">Identical routes must be advertised from either sides across multiple circuit pairs belonging you.</span></span> <span data-ttu-id="e655e-183">路由公制不需要的 toobe 完全相同。</span><span class="sxs-lookup"><span data-stu-id="e655e-183">Route metrics are not required toobe identical.</span></span>

## <a name="route-aggregation-and-prefix-limits"></a><span data-ttu-id="e655e-184">路由彙總與前置詞限制</span><span class="sxs-lookup"><span data-stu-id="e655e-184">Route aggregation and prefix limits</span></span>

<span data-ttu-id="e655e-185">我們支援註冊 too4000 通告 toous 透過 hello Azure 私用對等的前置詞。</span><span class="sxs-lookup"><span data-stu-id="e655e-185">We support up too4000 prefixes advertised toous through hello Azure private peering.</span></span> <span data-ttu-id="e655e-186">這可以增加總 too10，如果已啟用 hello ExpressRoute premium add-on 000 的前置詞。</span><span class="sxs-lookup"><span data-stu-id="e655e-186">This can be increased up too10,000 prefixes if hello ExpressRoute premium add-on is enabled.</span></span> <span data-ttu-id="e655e-187">我們接受 too200 前置詞，每個公用 Azure 的 BGP 工作階段及 Microsoft 對等互連。</span><span class="sxs-lookup"><span data-stu-id="e655e-187">We accept up too200 prefixes per BGP session for Azure public and Microsoft peering.</span></span> 

<span data-ttu-id="e655e-188">如果 hello 前置詞數目超過 hello 限制，將會捨棄 hello BGP 工作階段。</span><span class="sxs-lookup"><span data-stu-id="e655e-188">hello BGP session will be dropped if hello number of prefixes exceeds hello limit.</span></span> <span data-ttu-id="e655e-189">我們將接受 hello 私用對等互連連結只預設路由。</span><span class="sxs-lookup"><span data-stu-id="e655e-189">We will accept default routes on hello private peering link only.</span></span> <span data-ttu-id="e655e-190">提供者必須篩選出預設路由和私人 IP 位址 (RFC 1918) 從 hello 公用 Azure 和 Microsoft 對等互連路徑。</span><span class="sxs-lookup"><span data-stu-id="e655e-190">Provider must filter out default route and private IP addresses (RFC 1918) from hello Azure public and Microsoft peering paths.</span></span> 

## <a name="transit-routing-and-cross-region-routing"></a><span data-ttu-id="e655e-191">傳輸路由和跨區域路由</span><span class="sxs-lookup"><span data-stu-id="e655e-191">Transit routing and cross-region routing</span></span>

<span data-ttu-id="e655e-192">ExpressRoute 不能設定為傳輸路由器。</span><span class="sxs-lookup"><span data-stu-id="e655e-192">ExpressRoute cannot be configured as transit routers.</span></span> <span data-ttu-id="e655e-193">您會有 toorely 連線的傳輸路由服務提供者。</span><span class="sxs-lookup"><span data-stu-id="e655e-193">You will have toorely on your connectivity provider for transit routing services.</span></span>

## <a name="advertising-default-routes"></a><span data-ttu-id="e655e-194">公告預設路由</span><span class="sxs-lookup"><span data-stu-id="e655e-194">Advertising default routes</span></span>

<span data-ttu-id="e655e-195">只有 Azure 私人對等互連工作階段允許預設路由。</span><span class="sxs-lookup"><span data-stu-id="e655e-195">Default routes are permitted only on Azure private peering sessions.</span></span> <span data-ttu-id="e655e-196">在這種情況下，我們會將所有來自 hello 相關聯的虛擬網路 tooyour 網路流量。</span><span class="sxs-lookup"><span data-stu-id="e655e-196">In such a case, we will route all traffic from hello associated virtual networks tooyour network.</span></span> <span data-ttu-id="e655e-197">通告預設路由至私用對等互連，將會導致 hello 網際網路路徑從 Azure 遭到封鎖。</span><span class="sxs-lookup"><span data-stu-id="e655e-197">Advertising default routes into private peering will result in hello internet path from Azure being blocked.</span></span> <span data-ttu-id="e655e-198">您必須依賴來自您公司的邊緣 tooroute 流量和 toohello 裝載於 Azure 的網際網路服務。</span><span class="sxs-lookup"><span data-stu-id="e655e-198">You must rely on your corporate edge tooroute traffic from and toohello internet for services hosted in Azure.</span></span> 

 <span data-ttu-id="e655e-199">tooenable 連線 tooother Azure 服務和基礎結構服務，您必須確定下列項目 hello 就地有：</span><span class="sxs-lookup"><span data-stu-id="e655e-199">tooenable connectivity tooother Azure services and infrastructure services, you must make sure one of hello following items is in place:</span></span>

* <span data-ttu-id="e655e-200">Azure 公用對等互連是啟用的 tooroute 流量 toopublic 端點</span><span class="sxs-lookup"><span data-stu-id="e655e-200">Azure public peering is enabled tooroute traffic toopublic endpoints</span></span>
* <span data-ttu-id="e655e-201">您可以使用使用者定義路由的 tooallow 網際網路連線的每一個子網路需要網際網路連線能力。</span><span class="sxs-lookup"><span data-stu-id="e655e-201">You use user-defined routing tooallow internet connectivity for every subnet requiring Internet connectivity.</span></span>

> [!NOTE]
> <span data-ttu-id="e655e-202">公告預設路由會中斷 Windows 和其他 VM 授權啟用。</span><span class="sxs-lookup"><span data-stu-id="e655e-202">Advertising default routes will break Windows and other VM license activation.</span></span> <span data-ttu-id="e655e-203">請依照下列指示[這裡](http://blogs.msdn.com/b/mast/archive/2015/05/20/use-azure-custom-routes-to-enable-kms-activation-with-forced-tunneling.aspx)toowork 解決這個問題。</span><span class="sxs-lookup"><span data-stu-id="e655e-203">Follow instructions [here](http://blogs.msdn.com/b/mast/archive/2015/05/20/use-azure-custom-routes-to-enable-kms-activation-with-forced-tunneling.aspx) toowork around this.</span></span>
> 
> 

## <a name="support-for-bgp-communities-preview"></a><span data-ttu-id="e655e-204">BGP 社群支援 (預覽)</span><span class="sxs-lookup"><span data-stu-id="e655e-204">Support for BGP communities (Preview)</span></span>

<span data-ttu-id="e655e-205">本節提供 BGP 社群如何搭配 ExpressRoute 使用的概觀。</span><span class="sxs-lookup"><span data-stu-id="e655e-205">This section provides an overview of how BGP communities will be used with ExpressRoute.</span></span> <span data-ttu-id="e655e-206">Microsoft 將通告公用 hello 與 Microsoft 對等互連路徑中加上適當的社群值路由的路由。</span><span class="sxs-lookup"><span data-stu-id="e655e-206">Microsoft will advertise routes in hello public and Microsoft peering paths with routes tagged with appropriate community values.</span></span> <span data-ttu-id="e655e-207">hello 這麼做的基本原理，hello 的社群以下將詳述值的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="e655e-207">hello rationale for doing so and hello details on community values are described below.</span></span> <span data-ttu-id="e655e-208">Microsoft，不過，不支援之任何群體值標記的 tooroutes 通告 tooMicrosoft。</span><span class="sxs-lookup"><span data-stu-id="e655e-208">Microsoft, however, will not honor any community values tagged tooroutes advertised tooMicrosoft.</span></span>

<span data-ttu-id="e655e-209">如果您要連接 tooMicrosoft 透過 ExpressRoute，在任何一個的對等互連位置地緣政治區域內，您必須存取 tooall Microsoft 雲端服務 hello 地緣政治界限內的所有區域。</span><span class="sxs-lookup"><span data-stu-id="e655e-209">If you are connecting tooMicrosoft through ExpressRoute at any one peering location within a geopolitical region, you will have access tooall Microsoft cloud services across all regions within hello geopolitical boundary.</span></span> 

<span data-ttu-id="e655e-210">例如，如果您透過 ExpressRoute 連接 tooMicrosoft 阿姆斯特丹中的，您必須存取 tooall Microsoft 雲端服務裝載於北歐和西歐。</span><span class="sxs-lookup"><span data-stu-id="e655e-210">For example, if you connected tooMicrosoft in Amsterdam through ExpressRoute, you will have access tooall Microsoft cloud services hosted in North Europe and West Europe.</span></span> 

<span data-ttu-id="e655e-211">請參閱 toohello [ExpressRoute 合作夥伴和互連位置](expressroute-locations.md)網頁地緣政治區域及相關聯的 Azure 區域對應 ExpressRoute 對等互連位置的詳細清單。</span><span class="sxs-lookup"><span data-stu-id="e655e-211">Refer toohello [ExpressRoute partners and peering locations](expressroute-locations.md) page for a detailed list of geopolitical regions, associated Azure regions, and corresponding ExpressRoute peering locations.</span></span>

<span data-ttu-id="e655e-212">您可以針對每個地理政治區域購買多個 ExpressRoute 循環。</span><span class="sxs-lookup"><span data-stu-id="e655e-212">You can purchase more than one ExpressRoute circuit per geopolitical region.</span></span> <span data-ttu-id="e655e-213">將多個連線提供極大的好處，高可用性到期 toogeo 備援。</span><span class="sxs-lookup"><span data-stu-id="e655e-213">Having multiple connections offers you significant benefits on high availability due toogeo-redundancy.</span></span> <span data-ttu-id="e655e-214">在您有多個 ExpressRoute 電路的情況下，您會收到的 hello 公告相同的前置詞集合 Microsoft 在 hello 公用對等互連，且 Microsoft 對等互連路徑。</span><span class="sxs-lookup"><span data-stu-id="e655e-214">In cases where you have multiple ExpressRoute circuits, you will receive hello same set of prefixes advertised from Microsoft on hello public peering and Microsoft peering paths.</span></span> <span data-ttu-id="e655e-215">這表示您將會有多個路徑可從您的網路連到 Microsoft。</span><span class="sxs-lookup"><span data-stu-id="e655e-215">This means you will have multiple paths from your network into Microsoft.</span></span> <span data-ttu-id="e655e-216">這可能會造成您的網路中進行的次佳路由決策 toobe。</span><span class="sxs-lookup"><span data-stu-id="e655e-216">This can potentially cause sub-optimal routing decisions toobe made within your network.</span></span> <span data-ttu-id="e655e-217">如此一來，您可能會遇到次佳的連線經驗 toodifferent 服務。</span><span class="sxs-lookup"><span data-stu-id="e655e-217">As a result, you may experience sub-optimal connectivity experiences toodifferent services.</span></span> 

<span data-ttu-id="e655e-218">Microsoft 會標記透過公用互連公告的首碼，並裝載於 Microsoft 對等互連以適當的 BGP 社群值，指出 hello 區域 hello 前置詞。</span><span class="sxs-lookup"><span data-stu-id="e655e-218">Microsoft will tag prefixes advertised through public peering and Microsoft peering with appropriate BGP community values indicating hello region hello prefixes are hosted in.</span></span> <span data-ttu-id="e655e-219">您可以依賴 hello 社群值 toomake 適當路由決策 toooffer[最佳路由 toocustomers](expressroute-optimize-routing.md)。</span><span class="sxs-lookup"><span data-stu-id="e655e-219">You can rely on hello community values toomake appropriate routing decisions toooffer [optimal routing toocustomers](expressroute-optimize-routing.md).</span></span>

| <span data-ttu-id="e655e-220">**地緣政治區域**</span><span class="sxs-lookup"><span data-stu-id="e655e-220">**Geopolitical Region**</span></span> | <span data-ttu-id="e655e-221">**Microsoft Azure 區域**</span><span class="sxs-lookup"><span data-stu-id="e655e-221">**Microsoft Azure region**</span></span> | <span data-ttu-id="e655e-222">**BGP 社群值**</span><span class="sxs-lookup"><span data-stu-id="e655e-222">**BGP community value**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e655e-223">**北美洲**</span><span class="sxs-lookup"><span data-stu-id="e655e-223">**North America**</span></span> | | |
| <span data-ttu-id="e655e-224">美國東部</span><span class="sxs-lookup"><span data-stu-id="e655e-224">East US</span></span> |<span data-ttu-id="e655e-225">12076:51004</span><span class="sxs-lookup"><span data-stu-id="e655e-225">12076:51004</span></span> | |
| <span data-ttu-id="e655e-226">美國東部 2</span><span class="sxs-lookup"><span data-stu-id="e655e-226">East US 2</span></span> |<span data-ttu-id="e655e-227">12076:51005</span><span class="sxs-lookup"><span data-stu-id="e655e-227">12076:51005</span></span> | |
| <span data-ttu-id="e655e-228">美國西部</span><span class="sxs-lookup"><span data-stu-id="e655e-228">West US</span></span> |<span data-ttu-id="e655e-229">12076:51006</span><span class="sxs-lookup"><span data-stu-id="e655e-229">12076:51006</span></span> | |
| <span data-ttu-id="e655e-230">美國西部 2</span><span class="sxs-lookup"><span data-stu-id="e655e-230">West US 2</span></span> |<span data-ttu-id="e655e-231">12076:51026</span><span class="sxs-lookup"><span data-stu-id="e655e-231">12076:51026</span></span> | |
| <span data-ttu-id="e655e-232">美國中西部</span><span class="sxs-lookup"><span data-stu-id="e655e-232">West Central US</span></span> |<span data-ttu-id="e655e-233">12076:51027</span><span class="sxs-lookup"><span data-stu-id="e655e-233">12076:51027</span></span> | |
| <span data-ttu-id="e655e-234">美國中北部</span><span class="sxs-lookup"><span data-stu-id="e655e-234">North Central US</span></span> |<span data-ttu-id="e655e-235">12076:51007</span><span class="sxs-lookup"><span data-stu-id="e655e-235">12076:51007</span></span> | |
| <span data-ttu-id="e655e-236">美國中南部</span><span class="sxs-lookup"><span data-stu-id="e655e-236">South Central US</span></span> |<span data-ttu-id="e655e-237">12076:51008</span><span class="sxs-lookup"><span data-stu-id="e655e-237">12076:51008</span></span> | |
| <span data-ttu-id="e655e-238">美國中部</span><span class="sxs-lookup"><span data-stu-id="e655e-238">Central US</span></span> |<span data-ttu-id="e655e-239">12076:51009</span><span class="sxs-lookup"><span data-stu-id="e655e-239">12076:51009</span></span> | |
| <span data-ttu-id="e655e-240">加拿大中部</span><span class="sxs-lookup"><span data-stu-id="e655e-240">Canada Central</span></span> |<span data-ttu-id="e655e-241">12076:51020</span><span class="sxs-lookup"><span data-stu-id="e655e-241">12076:51020</span></span> | |
| <span data-ttu-id="e655e-242">加拿大東部</span><span class="sxs-lookup"><span data-stu-id="e655e-242">Canada East</span></span> |<span data-ttu-id="e655e-243">12076:51021</span><span class="sxs-lookup"><span data-stu-id="e655e-243">12076:51021</span></span> | |
| <span data-ttu-id="e655e-244">**南美洲**</span><span class="sxs-lookup"><span data-stu-id="e655e-244">**South America**</span></span> | | |
| <span data-ttu-id="e655e-245">巴西南部</span><span class="sxs-lookup"><span data-stu-id="e655e-245">Brazil South</span></span> |<span data-ttu-id="e655e-246">12076:51014</span><span class="sxs-lookup"><span data-stu-id="e655e-246">12076:51014</span></span> | |
| <span data-ttu-id="e655e-247">**歐洲**</span><span class="sxs-lookup"><span data-stu-id="e655e-247">**Europe**</span></span> | | |
| <span data-ttu-id="e655e-248">北歐</span><span class="sxs-lookup"><span data-stu-id="e655e-248">North Europe</span></span> |<span data-ttu-id="e655e-249">12076:51003</span><span class="sxs-lookup"><span data-stu-id="e655e-249">12076:51003</span></span> | |
| <span data-ttu-id="e655e-250">西歐</span><span class="sxs-lookup"><span data-stu-id="e655e-250">West Europe</span></span> |<span data-ttu-id="e655e-251">12076:51002</span><span class="sxs-lookup"><span data-stu-id="e655e-251">12076:51002</span></span> | |
| <span data-ttu-id="e655e-252">**亞太地區**</span><span class="sxs-lookup"><span data-stu-id="e655e-252">**Asia Pacific**</span></span> | | |
| <span data-ttu-id="e655e-253">東亞</span><span class="sxs-lookup"><span data-stu-id="e655e-253">East Asia</span></span> |<span data-ttu-id="e655e-254">12076:51010</span><span class="sxs-lookup"><span data-stu-id="e655e-254">12076:51010</span></span> | |
| <span data-ttu-id="e655e-255">東南亞</span><span class="sxs-lookup"><span data-stu-id="e655e-255">Southeast Asia</span></span> |<span data-ttu-id="e655e-256">12076:51011</span><span class="sxs-lookup"><span data-stu-id="e655e-256">12076:51011</span></span> | |
| <span data-ttu-id="e655e-257">**日本**</span><span class="sxs-lookup"><span data-stu-id="e655e-257">**Japan**</span></span> | | |
| <span data-ttu-id="e655e-258">日本東部</span><span class="sxs-lookup"><span data-stu-id="e655e-258">Japan East</span></span> |<span data-ttu-id="e655e-259">12076:51012</span><span class="sxs-lookup"><span data-stu-id="e655e-259">12076:51012</span></span> | |
| <span data-ttu-id="e655e-260">日本西部</span><span class="sxs-lookup"><span data-stu-id="e655e-260">Japan West</span></span> |<span data-ttu-id="e655e-261">12076:51013</span><span class="sxs-lookup"><span data-stu-id="e655e-261">12076:51013</span></span> | |
| <span data-ttu-id="e655e-262">**澳大利亞**</span><span class="sxs-lookup"><span data-stu-id="e655e-262">**Australia**</span></span> | | |
| <span data-ttu-id="e655e-263">澳洲東部</span><span class="sxs-lookup"><span data-stu-id="e655e-263">Australia East</span></span> |<span data-ttu-id="e655e-264">12076:51015</span><span class="sxs-lookup"><span data-stu-id="e655e-264">12076:51015</span></span> | |
| <span data-ttu-id="e655e-265">澳洲東南部</span><span class="sxs-lookup"><span data-stu-id="e655e-265">Australia Southeast</span></span> |<span data-ttu-id="e655e-266">12076:51016</span><span class="sxs-lookup"><span data-stu-id="e655e-266">12076:51016</span></span> | |
| <span data-ttu-id="e655e-267">**印度**</span><span class="sxs-lookup"><span data-stu-id="e655e-267">**India**</span></span> | | |
| <span data-ttu-id="e655e-268">印度南部</span><span class="sxs-lookup"><span data-stu-id="e655e-268">India South</span></span> |<span data-ttu-id="e655e-269">12076:51019</span><span class="sxs-lookup"><span data-stu-id="e655e-269">12076:51019</span></span> | |
| <span data-ttu-id="e655e-270">印度西部</span><span class="sxs-lookup"><span data-stu-id="e655e-270">India West</span></span> |<span data-ttu-id="e655e-271">12076:51018</span><span class="sxs-lookup"><span data-stu-id="e655e-271">12076:51018</span></span> | |
| <span data-ttu-id="e655e-272">印度中部</span><span class="sxs-lookup"><span data-stu-id="e655e-272">India Central</span></span> |<span data-ttu-id="e655e-273">12076:51017</span><span class="sxs-lookup"><span data-stu-id="e655e-273">12076:51017</span></span> | |

<span data-ttu-id="e655e-274">所有 microsoft 通告的路由會標記 hello 社群的適當值。</span><span class="sxs-lookup"><span data-stu-id="e655e-274">All routes advertised from Microsoft will be tagged with hello appropriate community value.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="e655e-275">全域前置詞會加上適當的社群值，而且只會在啟用 ExpressRoute 進階附加元件時公告。</span><span class="sxs-lookup"><span data-stu-id="e655e-275">Global prefixes will be tagged with an appropriate community value and will be advertised only when ExpressRoute premium add-on is enabled.</span></span>
> 
> 

<span data-ttu-id="e655e-276">除了上述 toohello，Microsoft 將也標記它們屬於 hello 服務為基礎的前置詞。</span><span class="sxs-lookup"><span data-stu-id="e655e-276">In addition toohello above, Microsoft will also tag prefixes based on hello service they belong to.</span></span> <span data-ttu-id="e655e-277">這適用於只有 toohello Microsoft 對等互連。</span><span class="sxs-lookup"><span data-stu-id="e655e-277">This applies only toohello Microsoft peering.</span></span> <span data-ttu-id="e655e-278">hello 下表提供服務 tooBGP 社群值的對應。</span><span class="sxs-lookup"><span data-stu-id="e655e-278">hello table below provides a mapping of service tooBGP community value.</span></span>

| <span data-ttu-id="e655e-279">**服務**</span><span class="sxs-lookup"><span data-stu-id="e655e-279">**Service**</span></span> | <span data-ttu-id="e655e-280">**BGP 社群值**</span><span class="sxs-lookup"><span data-stu-id="e655e-280">**BGP community value**</span></span> |
| --- | --- |
| <span data-ttu-id="e655e-281">**Exchange**</span><span class="sxs-lookup"><span data-stu-id="e655e-281">**Exchange**</span></span> |<span data-ttu-id="e655e-282">12076:5010</span><span class="sxs-lookup"><span data-stu-id="e655e-282">12076:5010</span></span> |
| <span data-ttu-id="e655e-283">**SharePoint**</span><span class="sxs-lookup"><span data-stu-id="e655e-283">**SharePoint**</span></span> |<span data-ttu-id="e655e-284">12076:5020</span><span class="sxs-lookup"><span data-stu-id="e655e-284">12076:5020</span></span> |
| <span data-ttu-id="e655e-285">**商務用 Skype**</span><span class="sxs-lookup"><span data-stu-id="e655e-285">**Skype For Business**</span></span> |<span data-ttu-id="e655e-286">12076:5030</span><span class="sxs-lookup"><span data-stu-id="e655e-286">12076:5030</span></span> |
| <span data-ttu-id="e655e-287">**Dynamics 365**</span><span class="sxs-lookup"><span data-stu-id="e655e-287">**Dynamics 365**</span></span> |<span data-ttu-id="e655e-288">12076:5040</span><span class="sxs-lookup"><span data-stu-id="e655e-288">12076:5040</span></span> |
| <span data-ttu-id="e655e-289">**其他 Office 365 服務**</span><span class="sxs-lookup"><span data-stu-id="e655e-289">**Other Office 365 Services**</span></span> |<span data-ttu-id="e655e-290">12076:5100</span><span class="sxs-lookup"><span data-stu-id="e655e-290">12076:5100</span></span> |

> [!NOTE]
> <span data-ttu-id="e655e-291">Microsoft 不會接受您 hello 路由通告 tooMicrosoft 設定任何 BGP 社群值。</span><span class="sxs-lookup"><span data-stu-id="e655e-291">Microsoft does not honor any BGP community values that you set on hello routes advertised tooMicrosoft.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="e655e-292">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e655e-292">Next steps</span></span>

* <span data-ttu-id="e655e-293">設定 ExpressRoute 連線。</span><span class="sxs-lookup"><span data-stu-id="e655e-293">Configure your ExpressRoute connection.</span></span>
  
  * <span data-ttu-id="e655e-294">[建立 ExpressRoute 電路 hello 傳統部署模型](expressroute-howto-circuit-classic.md)或[建立及修改 ExpressRoute 電路使用 Azure 資源管理員](expressroute-howto-circuit-arm.md)</span><span class="sxs-lookup"><span data-stu-id="e655e-294">[Create an ExpressRoute circuit for hello classic deployment model](expressroute-howto-circuit-classic.md) or [Create and modify an ExpressRoute circuit using Azure Resource Manager](expressroute-howto-circuit-arm.md)</span></span>
  * <span data-ttu-id="e655e-295">[設定路由 hello 傳統部署模型](expressroute-howto-routing-classic.md)或[設定路由 hello Resource Manager 部署模型。](expressroute-howto-routing-arm.md)</span><span class="sxs-lookup"><span data-stu-id="e655e-295">[Configure routing for hello classic deployment model](expressroute-howto-routing-classic.md) or [Configure routing for hello Resource Manager deployment model](expressroute-howto-routing-arm.md)</span></span>
  * <span data-ttu-id="e655e-296">[連結傳統的 VNet tooan ExpressRoute 電路](expressroute-howto-linkvnet-classic.md)或[連結的資源管理員 VNet tooan ExpressRoute 電路](expressroute-howto-linkvnet-arm.md)</span><span class="sxs-lookup"><span data-stu-id="e655e-296">[Link a classic VNet tooan ExpressRoute circuit](expressroute-howto-linkvnet-classic.md) or [Link a Resource Manager VNet tooan ExpressRoute circuit](expressroute-howto-linkvnet-arm.md)</span></span>

