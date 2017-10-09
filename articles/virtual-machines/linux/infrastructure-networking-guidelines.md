---
title: "網路基礎結構指導方針-Linux aaaAzure |Microsoft 文件"
description: "深入了解 hello 金鑰設計和實作部署的指導方針 Azure 基礎結構服務中的虛擬網路。"
documentationcenter: 
services: virtual-machines-linux
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: a7ebd5da-3c62-45e8-ad90-6c73a37ebeb1
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f3f49b135b1f9bca3fd463e9ff27299fb97908c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-networking-infrastructure-guidelines-for-linux-vms"></a><span data-ttu-id="6ee20-103">適用於 Linux VM 的 Azure 網路基礎結構指導方針</span><span class="sxs-lookup"><span data-stu-id="6ee20-103">Azure networking infrastructure guidelines for Linux VMs</span></span>

[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-intro](../../../includes/virtual-machines-linux-infrastructure-guidelines-intro.md)]

<span data-ttu-id="6ee20-104">本文著重在規劃步驟適用於在 Azure 中的虛擬網路和連接現有的內部部署環境之間所需的了解 hello。</span><span class="sxs-lookup"><span data-stu-id="6ee20-104">This article focuses on understanding hello required planning steps for virtual networking within Azure and connectivity between existing on-prem environments.</span></span>

## <a name="implementation-guidelines-for-virtual-networks"></a><span data-ttu-id="6ee20-105">虛擬網路的實作指導方針</span><span class="sxs-lookup"><span data-stu-id="6ee20-105">Implementation guidelines for virtual networks</span></span>
<span data-ttu-id="6ee20-106">决策：</span><span class="sxs-lookup"><span data-stu-id="6ee20-106">Decisions:</span></span>

* <span data-ttu-id="6ee20-107">哪種類型的虛擬網路是否需要 toohost 您的 IT 工作負載或基礎結構 (僅限雲端或跨單位)？</span><span class="sxs-lookup"><span data-stu-id="6ee20-107">What type of virtual network do you need toohost your IT workload or infrastructure (cloud-only or cross-premises)?</span></span>
* <span data-ttu-id="6ee20-108">跨單位虛擬網路，用於多少位址空間您需要 toohost hello 子網路和 Vm 現在和合理擴充 hello 未來嗎？</span><span class="sxs-lookup"><span data-stu-id="6ee20-108">For cross-premises virtual networks, how much address space do you need toohost hello subnets and VMs now and for reasonable expansion in hello future?</span></span>
* <span data-ttu-id="6ee20-109">是您 toocreate 集中的虛擬網路，或是建立每個資源群組的個別虛擬網路？</span><span class="sxs-lookup"><span data-stu-id="6ee20-109">Are you going toocreate centralized virtual networks or create individual virtual networks for each resource group?</span></span>

<span data-ttu-id="6ee20-110">工作：</span><span class="sxs-lookup"><span data-stu-id="6ee20-110">Tasks:</span></span>

* <span data-ttu-id="6ee20-111">定義建立 hello 虛擬網路 toobe hello 位址空間。</span><span class="sxs-lookup"><span data-stu-id="6ee20-111">Define hello address space for hello virtual networks toobe created.</span></span>
* <span data-ttu-id="6ee20-112">定義子網路與 hello 位址空間的每個的 hello 組。</span><span class="sxs-lookup"><span data-stu-id="6ee20-112">Define hello set of subnets and hello address space for each.</span></span>
* <span data-ttu-id="6ee20-113">跨單位虛擬網路，定義 hello 組 hello Vm hello 虛擬網路需要 tooreach 中的 hello 在內部部署位置的本機網路位址空間。</span><span class="sxs-lookup"><span data-stu-id="6ee20-113">For cross-premises virtual networks, define hello set of local network address spaces for hello on-premises locations that hello VMs in hello virtual network need tooreach.</span></span>
* <span data-ttu-id="6ee20-114">在內部部署網路小組 tooensure hello 適當設定路由，在建立時使用跨單位虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="6ee20-114">Work with on-premises networking team tooensure hello appropriate routing is configured when creating cross-premises virtual networks.</span></span>
* <span data-ttu-id="6ee20-115">建立使用您的命名慣例的 hello 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="6ee20-115">Create hello virtual network using your naming convention.</span></span>

## <a name="virtual-networks"></a><span data-ttu-id="6ee20-116">虛擬網路</span><span class="sxs-lookup"><span data-stu-id="6ee20-116">Virtual networks</span></span>
<span data-ttu-id="6ee20-117">虛擬網路是必要 toosupport 虛擬機器 (Vm) 之間的通訊。</span><span class="sxs-lookup"><span data-stu-id="6ee20-117">Virtual networks are necessary toosupport communications between virtual machines (VMs).</span></span> <span data-ttu-id="6ee20-118">和實體網路一樣，您可以定義子網路、自訂 IP 位址、DNS 設定、安全性篩選，以及負載平衡。</span><span class="sxs-lookup"><span data-stu-id="6ee20-118">You can define subnets, custom IP address, DNS settings, security filtering, and load balancing, as with physical networks.</span></span> <span data-ttu-id="6ee20-119">使用[VPN 閘道](../../vpn-gateway/vpn-gateway-about-vpngateways.md)或[Express Route 電路](../../expressroute/expressroute-introduction.md)，您可以將 Azure 虛擬網路 tooyour 在內部部署網路連接。</span><span class="sxs-lookup"><span data-stu-id="6ee20-119">By using a [VPN Gateway](../../vpn-gateway/vpn-gateway-about-vpngateways.md) or [Express Route circuit](../../expressroute/expressroute-introduction.md), you can connect Azure virtual networks tooyour on-premises networks.</span></span> <span data-ttu-id="6ee20-120">您可以深入了解 [虛擬網路及其元件](../../virtual-network/virtual-networks-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="6ee20-120">You can read more about [virtual networks and their components](../../virtual-network/virtual-networks-overview.md).</span></span>

<span data-ttu-id="6ee20-121">透過使用資源群組，您便能彈性地設計您的虛擬網路元件。</span><span class="sxs-lookup"><span data-stu-id="6ee20-121">By using Resource Groups, you have flexibility in how you design your virtual networking components.</span></span> <span data-ttu-id="6ee20-122">Vm 可以將自己的資源群組外的 toovirtual 網路連接。</span><span class="sxs-lookup"><span data-stu-id="6ee20-122">VMs can connect toovirtual networks outside of their own resource group.</span></span> <span data-ttu-id="6ee20-123">常見的設計方式是包含您的核心網路基礎結構會受到一般小組 toocreate 集中式資源群組。</span><span class="sxs-lookup"><span data-stu-id="6ee20-123">A common design approach would be toocreate centralized resource groups that contain your core networking infrastructure that can be managed by a common team.</span></span> <span data-ttu-id="6ee20-124">Vm 和其應用程式部署 tooseparate 資源群組。</span><span class="sxs-lookup"><span data-stu-id="6ee20-124">VMs and their applications deployed tooseparate resource groups.</span></span> <span data-ttu-id="6ee20-125">這個方法可讓應用程式擁有者存取 toohello 包含其 Vm 而不需要開啟設定存取 toohello hello 廣虛擬網路資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="6ee20-125">This approach allows application owners access toohello resource group that contains their VMs without opening up access toohello configuration of hello wider virtual networking resources.</span></span>

## <a name="site-connectivity"></a><span data-ttu-id="6ee20-126">站台連線能力</span><span class="sxs-lookup"><span data-stu-id="6ee20-126">Site connectivity</span></span>
### <a name="cloud-only-virtual-networks"></a><span data-ttu-id="6ee20-127">僅限雲端虛擬網路</span><span class="sxs-lookup"><span data-stu-id="6ee20-127">Cloud-only virtual networks</span></span>
<span data-ttu-id="6ee20-128">如果在內部部署使用者和電腦不需要持續連線 tooVMs Azure 的虛擬網路中，您的虛擬網路設計是直接的：</span><span class="sxs-lookup"><span data-stu-id="6ee20-128">If on-premises users and computers do not require ongoing connectivity tooVMs in an Azure virtual network, your virtual network design is straight forward:</span></span>

![基本僅雲端虛擬網路圖表](./media/infrastructure-networking-guidelines/vnet01.png)

<span data-ttu-id="6ee20-130">這種方法通常適用於網際網路對應的工作負載，例如，以網際網路為基礎的 Web 伺服器。</span><span class="sxs-lookup"><span data-stu-id="6ee20-130">This approach is typically for Internet-facing workloads, such as an Internet-based web server.</span></span> <span data-ttu-id="6ee20-131">您可以使用 SSH 或點對站 VPN 連線來管理這些 VM。</span><span class="sxs-lookup"><span data-stu-id="6ee20-131">You can manage these VMs using SSH or point-to-site VPN connections.</span></span>

<span data-ttu-id="6ee20-132">因為它們並未連接 tooyour 在內部部署網路，僅限 Azure 虛擬網路可以使用 hello 私人 IP 位址空間的任何部分。</span><span class="sxs-lookup"><span data-stu-id="6ee20-132">Because they do not connect tooyour on-premises network, Azure-only virtual networks can use any portion of hello private IP address space.</span></span> <span data-ttu-id="6ee20-133">hello 位址空間可以是 hello 相同的私用空間中使用內部部署。</span><span class="sxs-lookup"><span data-stu-id="6ee20-133">hello address space can be hello same private space that is in use on-premises.</span></span>

### <a name="cross-premises-virtual-networks"></a><span data-ttu-id="6ee20-134">跨單位虛擬網路</span><span class="sxs-lookup"><span data-stu-id="6ee20-134">Cross-premises virtual networks</span></span>
<span data-ttu-id="6ee20-135">如果在內部部署使用者和電腦需要持續連線 tooVMs Azure 的虛擬網路中，建立跨單位虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="6ee20-135">If on-premises users and computers require ongoing connectivity tooVMs in an Azure virtual network, create a cross-premises virtual network.</span></span> <span data-ttu-id="6ee20-136">Hello 虛擬網路 tooyour 在內部部署網路連線與 ExpressRoute 或站對站 VPN 連線。</span><span class="sxs-lookup"><span data-stu-id="6ee20-136">Connect hello virtual network tooyour on-premises network with an ExpressRoute or site-to-site VPN connection.</span></span>

![跨部署虛擬網路圖表](./media/infrastructure-networking-guidelines/vnet02.png)

<span data-ttu-id="6ee20-138">此設定會 hello Azure 虛擬網路是基本上的雲端擴充功能在內部部署網路。</span><span class="sxs-lookup"><span data-stu-id="6ee20-138">In this configuration, hello Azure virtual network is essentially a cloud-based extension of your on-premises network.</span></span>

<span data-ttu-id="6ee20-139">因為它們連接 tooyour 內部網路，跨單位虛擬網路必須使用 hello 位址空間是唯一的組織所使用的一部分。</span><span class="sxs-lookup"><span data-stu-id="6ee20-139">Because they connect tooyour on-premises network, cross-premises virtual networks must use a portion of hello address space used by your organization that is unique.</span></span> <span data-ttu-id="6ee20-140">在 hello 相同方式，不同公司的位置指派特定的 IP 子網路中，當您擴充出您的網路，Azure 會變成另一個位置。</span><span class="sxs-lookup"><span data-stu-id="6ee20-140">In hello same way that different corporate locations are assigned a specific IP subnet, Azure becomes another location as you extend out your network.</span></span>

<span data-ttu-id="6ee20-141">tooallow 封包 tootravel 從跨單位虛擬網路 tooyour 在內部部署網路，您必須設定 hello 組相關的內部部署位址前置詞為 hello hello 虛擬網路的區域網路定義的一部分。</span><span class="sxs-lookup"><span data-stu-id="6ee20-141">tooallow packets tootravel from your cross-premises virtual network tooyour on-premises network, you must configure hello set of relevant on-premises address prefixes as part of hello local network definition for hello virtual network.</span></span> <span data-ttu-id="6ee20-142">根據 hello 位址空間 hello 虛擬網路和 hello 集相關的內部部署位置，hello 本機網路中可以有多個位址前置詞。</span><span class="sxs-lookup"><span data-stu-id="6ee20-142">Depending on hello address space of hello virtual network and hello set of relevant on-premises locations, there can be many address prefixes in hello local network.</span></span>

<span data-ttu-id="6ee20-143">您可以將轉換僅限雲端的虛擬網路 tooa 跨單位虛擬網路，但最有可能需要您 toore IP 您的虛擬網路位址空間和 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="6ee20-143">You can convert a cloud-only virtual network tooa cross-premises virtual network, but it most likely requires you toore-IP your virtual network address space and Azure resources.</span></span> <span data-ttu-id="6ee20-144">因此，請仔細考慮虛擬網路是否需要 toobe tooyour 連線在內部部署網路，當您指派的 IP 子網路。</span><span class="sxs-lookup"><span data-stu-id="6ee20-144">Therefore, carefully consider if a virtual network needs toobe connected tooyour on-premises network when you assign an IP subnet.</span></span>

## <a name="subnets"></a><span data-ttu-id="6ee20-145">子網路</span><span class="sxs-lookup"><span data-stu-id="6ee20-145">Subnets</span></span>
<span data-ttu-id="6ee20-146">子網路可讓您 tooorganize 相關資源的可能是以邏輯方式 (例如，一個 Vm 子網路相關聯 toohello 相同的應用程式)，或實體 （例如，每個資源群組的一個子網路）。</span><span class="sxs-lookup"><span data-stu-id="6ee20-146">Subnets allow you tooorganize resources that are related, either logically (for example, one subnet for VMs associated toohello same application), or physically (for example, one subnet per resource group).</span></span> <span data-ttu-id="6ee20-147">您也可以採用子網路隔離技術來提高安全性。</span><span class="sxs-lookup"><span data-stu-id="6ee20-147">You can also employ subnet isolation techniques for added security.</span></span>

<span data-ttu-id="6ee20-148">針對跨單位虛擬網路，您應該設計以 hello 的子網路用於內部部署資源的相同慣例。</span><span class="sxs-lookup"><span data-stu-id="6ee20-148">For cross-premises virtual networks, you should design subnets with hello same conventions that you use for on-premises resources.</span></span> <span data-ttu-id="6ee20-149">**Azure 會使用一律 hello hello 每個子網路的位址空間的前三個 IP 位址**。</span><span class="sxs-lookup"><span data-stu-id="6ee20-149">**Azure always uses hello first three IP addresses of hello address space for each subnet**.</span></span> <span data-ttu-id="6ee20-150">toodetermine hello 數目所需的位址 hello 子網路，啟動透過計算 hello 現在您需要的 Vm 數目。</span><span class="sxs-lookup"><span data-stu-id="6ee20-150">toodetermine hello number of addresses needed for hello subnet, start by counting hello number of VMs that you need now.</span></span> <span data-ttu-id="6ee20-151">供未來成長估計，然後使用 hello 下列資料表 toodetermine hello 大小 hello 子網路。</span><span class="sxs-lookup"><span data-stu-id="6ee20-151">Estimate for future growth, and then use hello following table toodetermine hello size of hello subnet.</span></span>

| <span data-ttu-id="6ee20-152">所需的 VM 數目</span><span class="sxs-lookup"><span data-stu-id="6ee20-152">Number of VMs needed</span></span> | <span data-ttu-id="6ee20-153">所需的主機位元數</span><span class="sxs-lookup"><span data-stu-id="6ee20-153">Number of host bits needed</span></span> | <span data-ttu-id="6ee20-154">Hello 子網路的大小</span><span class="sxs-lookup"><span data-stu-id="6ee20-154">Size of hello subnet</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6ee20-155">1–3</span><span class="sxs-lookup"><span data-stu-id="6ee20-155">1–3</span></span> |<span data-ttu-id="6ee20-156">3</span><span class="sxs-lookup"><span data-stu-id="6ee20-156">3</span></span> |<span data-ttu-id="6ee20-157">/29</span><span class="sxs-lookup"><span data-stu-id="6ee20-157">/29</span></span> |
| <span data-ttu-id="6ee20-158">4–11</span><span class="sxs-lookup"><span data-stu-id="6ee20-158">4–11</span></span> |<span data-ttu-id="6ee20-159">4</span><span class="sxs-lookup"><span data-stu-id="6ee20-159">4</span></span> |<span data-ttu-id="6ee20-160">/28</span><span class="sxs-lookup"><span data-stu-id="6ee20-160">/28</span></span> |
| <span data-ttu-id="6ee20-161">12–27</span><span class="sxs-lookup"><span data-stu-id="6ee20-161">12–27</span></span> |<span data-ttu-id="6ee20-162">5</span><span class="sxs-lookup"><span data-stu-id="6ee20-162">5</span></span> |<span data-ttu-id="6ee20-163">/27</span><span class="sxs-lookup"><span data-stu-id="6ee20-163">/27</span></span> |
| <span data-ttu-id="6ee20-164">28–59</span><span class="sxs-lookup"><span data-stu-id="6ee20-164">28–59</span></span> |<span data-ttu-id="6ee20-165">6</span><span class="sxs-lookup"><span data-stu-id="6ee20-165">6</span></span> |<span data-ttu-id="6ee20-166">/26</span><span class="sxs-lookup"><span data-stu-id="6ee20-166">/26</span></span> |
| <span data-ttu-id="6ee20-167">60–123</span><span class="sxs-lookup"><span data-stu-id="6ee20-167">60–123</span></span> |<span data-ttu-id="6ee20-168">7</span><span class="sxs-lookup"><span data-stu-id="6ee20-168">7</span></span> |<span data-ttu-id="6ee20-169">/25</span><span class="sxs-lookup"><span data-stu-id="6ee20-169">/25</span></span> |

> [!NOTE]
> <span data-ttu-id="6ee20-170">一般在內部部署子網路，hello n 主機位元與子網路的主機位址數目上限是 2<sup> n </sup> -2。</span><span class="sxs-lookup"><span data-stu-id="6ee20-170">For normal on-premises subnets, hello maximum number of host addresses for a subnet with n host bits is 2<sup>n</sup> – 2.</span></span> <span data-ttu-id="6ee20-171">Azure 子網路，hello n 主機位元與子網路的主機位址數目上限是 2<sup> n </sup> – 5 （2 及 3，Azure 會使用每個子網路上的 hello 位址）。</span><span class="sxs-lookup"><span data-stu-id="6ee20-171">For an Azure subnet, hello maximum number of host addresses for a subnet with n host bits is 2<sup>n</sup> – 5 (2 plus 3 for hello addresses that Azure uses on each subnet).</span></span>
> 
> 

<span data-ttu-id="6ee20-172">如果您選擇的子網路大小太小，您會有 toore IP，並重新部署 hello 子網路中的 hello Vm。</span><span class="sxs-lookup"><span data-stu-id="6ee20-172">If you choose a subnet size that is too small, you have toore-IP and redeploy hello VMs in hello subnet.</span></span>

## <a name="network-security-groups"></a><span data-ttu-id="6ee20-173">網路安全性群組</span><span class="sxs-lookup"><span data-stu-id="6ee20-173">Network Security Groups</span></span>
<span data-ttu-id="6ee20-174">您可以套用到您的虛擬網路的流動的篩選規則 toohello 流量使用網路安全性群組。</span><span class="sxs-lookup"><span data-stu-id="6ee20-174">You can apply filtering rules toohello traffic that flows through your virtual networks by using Network Security Groups.</span></span> <span data-ttu-id="6ee20-175">您可以建立更細微的篩選規則 toosecure 虛擬網路環境，控制傳入和傳出流量，來源和目的地 IP 範圍，允許連接埠等。網路安全性群組可以是虛擬網路或直接指定虛擬網路介面的 tooa 內套用的 toosubnets。</span><span class="sxs-lookup"><span data-stu-id="6ee20-175">You can build granular filtering rules toosecure your virtual networking environment, controlling inbound and outbound traffic, source and destination IP ranges, allowed ports, etc. Network Security Groups can be applied toosubnets within a virtual network or directly tooa given virtual network interface.</span></span> <span data-ttu-id="6ee20-176">它會建議 toohave 某種程度的篩選您的虛擬網路上的流量的網路安全性群組。</span><span class="sxs-lookup"><span data-stu-id="6ee20-176">It is recommended toohave some level of Network Security Group filtering traffic on your virtual networks.</span></span> <span data-ttu-id="6ee20-177">您可以深入了解 [網路安全性群組](../../virtual-network/virtual-networks-nsg.md)。</span><span class="sxs-lookup"><span data-stu-id="6ee20-177">You can read more about [Network Security Groups](../../virtual-network/virtual-networks-nsg.md).</span></span>

## <a name="additional-network-components"></a><span data-ttu-id="6ee20-178">其他網路元件</span><span class="sxs-lookup"><span data-stu-id="6ee20-178">Additional network components</span></span>
<span data-ttu-id="6ee20-179">和內部部署實體網路基礎結構一樣，Azure 虛擬網路除了子網路和 IP 位址之外，還可以包含更多其他元件。</span><span class="sxs-lookup"><span data-stu-id="6ee20-179">As with an on-premises physical networking infrastructure, Azure virtual networking can contain more than just subnets and IP addressing.</span></span> <span data-ttu-id="6ee20-180">當您設計您的應用程式基礎結構，您可能會想 tooincorporate 部分這些額外的元件：</span><span class="sxs-lookup"><span data-stu-id="6ee20-180">As you design your application infrastructure, you may want tooincorporate some of these additional components:</span></span>

* <span data-ttu-id="6ee20-181">[VPN 閘道](../../vpn-gateway/vpn-gateway-about-vpngateways.md)-連接 Azure 虛擬網路 tooother Azure 虛擬網路，或透過站對站 VPN 連線連線 tooon 內部部署網路。</span><span class="sxs-lookup"><span data-stu-id="6ee20-181">[VPN gateways](../../vpn-gateway/vpn-gateway-about-vpngateways.md) - connect Azure virtual networks tooother Azure virtual networks, or connect tooon-premises networks through a Site-to-Site VPN connection.</span></span> <span data-ttu-id="6ee20-182">實作 Express Route 連線以做為專用的安全連線。</span><span class="sxs-lookup"><span data-stu-id="6ee20-182">Implement Express Route connections for dedicated, secure connections.</span></span> <span data-ttu-id="6ee20-183">您也可以利用點對站 VPN 連線，來提供使用者直接存取。</span><span class="sxs-lookup"><span data-stu-id="6ee20-183">You can also provide users direct access with Point-to-Site VPN connections.</span></span>
* <span data-ttu-id="6ee20-184">[負載平衡器](../../load-balancer/load-balancer-overview.md) - 視需求針對外部和內部流量提供流量負載平衡。</span><span class="sxs-lookup"><span data-stu-id="6ee20-184">[Load balancer](../../load-balancer/load-balancer-overview.md) - provides load balancing of traffic for both external and internal traffic as desired.</span></span>
* <span data-ttu-id="6ee20-185">[應用程式閘道](../../application-gateway/application-gateway-introduction.md)-HTTP hello 應用程式層進行負載平衡，為 web 應用程式提供某些額外的好處，而不要部署 hello Azure 負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="6ee20-185">[Application Gateway](../../application-gateway/application-gateway-introduction.md) - HTTP load-balancing at hello application layer, providing some additional benefits for web applications rather than deploying hello Azure load balancer.</span></span>
* <span data-ttu-id="6ee20-186">[Traffic Manager](../../traffic-manager/traffic-manager-overview.md) -DNS 架構流量發佈 toodirect 使用者 toohello 最接近可用的應用程式端點，允許您 toohost 超出不同地區的 Azure 資料中心的應用程式。</span><span class="sxs-lookup"><span data-stu-id="6ee20-186">[Traffic Manager](../../traffic-manager/traffic-manager-overview.md) - DNS-based traffic distribution toodirect end-users toohello closest available application endpoint, allowing you toohost your application out of Azure datacenters in different regions.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6ee20-187">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6ee20-187">Next steps</span></span>
[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-next-steps](../../../includes/virtual-machines-linux-infrastructure-guidelines-next-steps.md)]

