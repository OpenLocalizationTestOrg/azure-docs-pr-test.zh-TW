---
title: "Azure 網路基礎結構指導方針 - Linux | Microsoft Docs"
description: "了解適合用來在 Azure 基礎結構服務中部署虛擬網路的關鍵設計和實作指導方針。"
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
ms.openlocfilehash: 13e041956c05bec522c83587f8a7f99ac1ceb510
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="azure-networking-infrastructure-guidelines-for-linux-vms"></a><span data-ttu-id="7b339-103">適用於 Linux VM 的 Azure 網路基礎結構指導方針</span><span class="sxs-lookup"><span data-stu-id="7b339-103">Azure networking infrastructure guidelines for Linux VMs</span></span>

[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-intro](../../../includes/virtual-machines-linux-infrastructure-guidelines-intro.md)]

<span data-ttu-id="7b339-104">本文著重於了解 Azure 內虛擬網路的必要計畫步驟，以及現有內部部署環境之間的連線能力。</span><span class="sxs-lookup"><span data-stu-id="7b339-104">This article focuses on understanding the required planning steps for virtual networking within Azure and connectivity between existing on-prem environments.</span></span>

## <a name="implementation-guidelines-for-virtual-networks"></a><span data-ttu-id="7b339-105">虛擬網路的實作指導方針</span><span class="sxs-lookup"><span data-stu-id="7b339-105">Implementation guidelines for virtual networks</span></span>
<span data-ttu-id="7b339-106">决策：</span><span class="sxs-lookup"><span data-stu-id="7b339-106">Decisions:</span></span>

* <span data-ttu-id="7b339-107">您需要使用何種類型的虛擬網路來裝載 IT 工作負載或基礎結構 (僅限雲端或跨單位部署)？</span><span class="sxs-lookup"><span data-stu-id="7b339-107">What type of virtual network do you need to host your IT workload or infrastructure (cloud-only or cross-premises)?</span></span>
* <span data-ttu-id="7b339-108">如果是跨單位的虛擬網路，您現在需要多少位址空間來裝載子網路和 VM，並且在未來進行合理範圍的擴充？</span><span class="sxs-lookup"><span data-stu-id="7b339-108">For cross-premises virtual networks, how much address space do you need to host the subnets and VMs now and for reasonable expansion in the future?</span></span>
* <span data-ttu-id="7b339-109">您要建立集中式的虛擬網路，或是針對每個資源群組建立個別的虛擬網路？</span><span class="sxs-lookup"><span data-stu-id="7b339-109">Are you going to create centralized virtual networks or create individual virtual networks for each resource group?</span></span>

<span data-ttu-id="7b339-110">工作：</span><span class="sxs-lookup"><span data-stu-id="7b339-110">Tasks:</span></span>

* <span data-ttu-id="7b339-111">定義適要建立虛擬網路的位址空間。</span><span class="sxs-lookup"><span data-stu-id="7b339-111">Define the address space for the virtual networks to be created.</span></span>
* <span data-ttu-id="7b339-112">定義子網路組合以及適用於每個子網路的位址空間。</span><span class="sxs-lookup"><span data-stu-id="7b339-112">Define the set of subnets and the address space for each.</span></span>
* <span data-ttu-id="7b339-113">針對跨單位的虛擬網路，定義適用於內部部署位置的區域網路位址空間組合，而虛擬網路中的 VM 需要連接這類位置。</span><span class="sxs-lookup"><span data-stu-id="7b339-113">For cross-premises virtual networks, define the set of local network address spaces for the on-premises locations that the VMs in the virtual network need to reach.</span></span>
* <span data-ttu-id="7b339-114">與內部部署網路團隊合作，以確保在建立跨單位虛擬網路時設定適當的路由。</span><span class="sxs-lookup"><span data-stu-id="7b339-114">Work with on-premises networking team to ensure the appropriate routing is configured when creating cross-premises virtual networks.</span></span>
* <span data-ttu-id="7b339-115">使用您的命名慣例來建立虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="7b339-115">Create the virtual network using your naming convention.</span></span>

## <a name="virtual-networks"></a><span data-ttu-id="7b339-116">虛擬網路</span><span class="sxs-lookup"><span data-stu-id="7b339-116">Virtual networks</span></span>
<span data-ttu-id="7b339-117">需要虛擬網路以支援虛擬機器 (VM) 之間的通訊。</span><span class="sxs-lookup"><span data-stu-id="7b339-117">Virtual networks are necessary to support communications between virtual machines (VMs).</span></span> <span data-ttu-id="7b339-118">和實體網路一樣，您可以定義子網路、自訂 IP 位址、DNS 設定、安全性篩選，以及負載平衡。</span><span class="sxs-lookup"><span data-stu-id="7b339-118">You can define subnets, custom IP address, DNS settings, security filtering, and load balancing, as with physical networks.</span></span> <span data-ttu-id="7b339-119">藉由使用[VPN 閘道](../../vpn-gateway/vpn-gateway-about-vpngateways.md)或 [Express Route 線路](../../expressroute/expressroute-introduction.md)，您可以將 Azure 虛擬網路連接到內部部署網路。</span><span class="sxs-lookup"><span data-stu-id="7b339-119">By using a [VPN Gateway](../../vpn-gateway/vpn-gateway-about-vpngateways.md) or [Express Route circuit](../../expressroute/expressroute-introduction.md), you can connect Azure virtual networks to your on-premises networks.</span></span> <span data-ttu-id="7b339-120">您可以深入了解 [虛擬網路及其元件](../../virtual-network/virtual-networks-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="7b339-120">You can read more about [virtual networks and their components](../../virtual-network/virtual-networks-overview.md).</span></span>

<span data-ttu-id="7b339-121">透過使用資源群組，您便能彈性地設計您的虛擬網路元件。</span><span class="sxs-lookup"><span data-stu-id="7b339-121">By using Resource Groups, you have flexibility in how you design your virtual networking components.</span></span> <span data-ttu-id="7b339-122">VM 可以連接到其資源群組之外的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="7b339-122">VMs can connect to virtual networks outside of their own resource group.</span></span> <span data-ttu-id="7b339-123">一個常見的設計方式，便是建立可由一般小組管理且包含核心網路基礎結構的集中式資源群組。</span><span class="sxs-lookup"><span data-stu-id="7b339-123">A common design approach would be to create centralized resource groups that contain your core networking infrastructure that can be managed by a common team.</span></span> <span data-ttu-id="7b339-124">將 VM 與其應用程式部署到其他的資源群組。</span><span class="sxs-lookup"><span data-stu-id="7b339-124">VMs and their applications deployed to separate resource groups.</span></span> <span data-ttu-id="7b339-125">這種方式可讓應用程式使用者存取包含其 VM 的資源群組，而不需開放存取更廣泛虛擬網路資源的設定。</span><span class="sxs-lookup"><span data-stu-id="7b339-125">This approach allows application owners access to the resource group that contains their VMs without opening up access to the configuration of the wider virtual networking resources.</span></span>

## <a name="site-connectivity"></a><span data-ttu-id="7b339-126">站台連線能力</span><span class="sxs-lookup"><span data-stu-id="7b339-126">Site connectivity</span></span>
### <a name="cloud-only-virtual-networks"></a><span data-ttu-id="7b339-127">僅限雲端虛擬網路</span><span class="sxs-lookup"><span data-stu-id="7b339-127">Cloud-only virtual networks</span></span>
<span data-ttu-id="7b339-128">如果內部部署的使用者和電腦不需持續連線到 Azure 虛擬網路中的 VM，表示您的虛擬網路設計是相當直覺的：</span><span class="sxs-lookup"><span data-stu-id="7b339-128">If on-premises users and computers do not require ongoing connectivity to VMs in an Azure virtual network, your virtual network design is straight forward:</span></span>

![基本僅雲端虛擬網路圖表](./media/infrastructure-networking-guidelines/vnet01.png)

<span data-ttu-id="7b339-130">這種方法通常適用於網際網路對應的工作負載，例如，以網際網路為基礎的 Web 伺服器。</span><span class="sxs-lookup"><span data-stu-id="7b339-130">This approach is typically for Internet-facing workloads, such as an Internet-based web server.</span></span> <span data-ttu-id="7b339-131">您可以使用 SSH 或點對站 VPN 連線來管理這些 VM。</span><span class="sxs-lookup"><span data-stu-id="7b339-131">You can manage these VMs using SSH or point-to-site VPN connections.</span></span>

<span data-ttu-id="7b339-132">由於它們不會連線到您的內部部署網路，因此，僅限 Azure 的虛擬網路可以使用任何部分的私人 IP 位址空間。</span><span class="sxs-lookup"><span data-stu-id="7b339-132">Because they do not connect to your on-premises network, Azure-only virtual networks can use any portion of the private IP address space.</span></span> <span data-ttu-id="7b339-133">位址空間可以是內部部署使用中的相同私用空間。</span><span class="sxs-lookup"><span data-stu-id="7b339-133">The address space can be the same private space that is in use on-premises.</span></span>

### <a name="cross-premises-virtual-networks"></a><span data-ttu-id="7b339-134">跨單位虛擬網路</span><span class="sxs-lookup"><span data-stu-id="7b339-134">Cross-premises virtual networks</span></span>
<span data-ttu-id="7b339-135">如果內部部署的使用者和電腦需要持續連線到 Azure 虛擬網路中的 VM，則可建立跨單位的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="7b339-135">If on-premises users and computers require ongoing connectivity to VMs in an Azure virtual network, create a cross-premises virtual network.</span></span> <span data-ttu-id="7b339-136">透過 ExpressRoute 或站對站 VPN 連線，將虛擬網路連接到您的內部部署網路。</span><span class="sxs-lookup"><span data-stu-id="7b339-136">Connect the virtual network to your on-premises network with an ExpressRoute or site-to-site VPN connection.</span></span>

![跨部署虛擬網路圖表](./media/infrastructure-networking-guidelines/vnet02.png)

<span data-ttu-id="7b339-138">在這個設定中，Azure 虛擬網路本質上是您的內部部署網路中具備雲端功能的延伸模組。</span><span class="sxs-lookup"><span data-stu-id="7b339-138">In this configuration, the Azure virtual network is essentially a cloud-based extension of your on-premises network.</span></span>

<span data-ttu-id="7b339-139">由於他們會連線到您的內部部署網路，跨單位虛擬網路必須使用您組織所用位址空間的一部分，且該部分必須是唯一的。</span><span class="sxs-lookup"><span data-stu-id="7b339-139">Because they connect to your on-premises network, cross-premises virtual networks must use a portion of the address space used by your organization that is unique.</span></span> <span data-ttu-id="7b339-140">與為不同的公司位置指派特定 IP 子網路相同，Azure 會隨著您擴充網路而成為另一個位置。</span><span class="sxs-lookup"><span data-stu-id="7b339-140">In the same way that different corporate locations are assigned a specific IP subnet, Azure becomes another location as you extend out your network.</span></span>

<span data-ttu-id="7b339-141">若要允許封包從跨單位的虛擬網路傳輸到內部部署網路，您必須設定相關的內部部署位址首碼組合，來做為適用於虛擬網路之區域網路定義的一部分。</span><span class="sxs-lookup"><span data-stu-id="7b339-141">To allow packets to travel from your cross-premises virtual network to your on-premises network, you must configure the set of relevant on-premises address prefixes as part of the local network definition for the virtual network.</span></span> <span data-ttu-id="7b339-142">根據虛擬網路的位址空間及相關的內部部署位置組合而定，區域網路中可以有多個位址首碼。</span><span class="sxs-lookup"><span data-stu-id="7b339-142">Depending on the address space of the virtual network and the set of relevant on-premises locations, there can be many address prefixes in the local network.</span></span>

<span data-ttu-id="7b339-143">您可以將僅限雲端的虛擬網路轉換為跨單位的虛擬網路，但是，它很可能會要求您為虛擬網路位址空間和 Azure 資源重新指派 IP。</span><span class="sxs-lookup"><span data-stu-id="7b339-143">You can convert a cloud-only virtual network to a cross-premises virtual network, but it most likely requires you to re-IP your virtual network address space and Azure resources.</span></span> <span data-ttu-id="7b339-144">因此，在指派 IP 子網路時，請仔細考慮虛擬網路是否需要連接到您的內部部署網路。</span><span class="sxs-lookup"><span data-stu-id="7b339-144">Therefore, carefully consider if a virtual network needs to be connected to your on-premises network when you assign an IP subnet.</span></span>

## <a name="subnets"></a><span data-ttu-id="7b339-145">子網路</span><span class="sxs-lookup"><span data-stu-id="7b339-145">Subnets</span></span>
<span data-ttu-id="7b339-146">子網路允許您組織相關的資源，可能是邏輯相關 (例如，針對與相同應用程式關聯的 VM 提供一個子網路)，或是實體相關 (例如，針對每個資源群組提供一個子網路)。</span><span class="sxs-lookup"><span data-stu-id="7b339-146">Subnets allow you to organize resources that are related, either logically (for example, one subnet for VMs associated to the same application), or physically (for example, one subnet per resource group).</span></span> <span data-ttu-id="7b339-147">您也可以採用子網路隔離技術來提高安全性。</span><span class="sxs-lookup"><span data-stu-id="7b339-147">You can also employ subnet isolation techniques for added security.</span></span>

<span data-ttu-id="7b339-148">對於跨單位虛擬網路，您應該利用您針對內部部署資源所使用的相同慣例來設計子網路。</span><span class="sxs-lookup"><span data-stu-id="7b339-148">For cross-premises virtual networks, you should design subnets with the same conventions that you use for on-premises resources.</span></span> <span data-ttu-id="7b339-149">**Azure 一律會針對每個子網路使用位址空間的前三個 IP 位址**。</span><span class="sxs-lookup"><span data-stu-id="7b339-149">**Azure always uses the first three IP addresses of the address space for each subnet**.</span></span> <span data-ttu-id="7b339-150">若要判斷子網路所需的位址數目，請從計算您現在需要的 VM 數目開始。</span><span class="sxs-lookup"><span data-stu-id="7b339-150">To determine the number of addresses needed for the subnet, start by counting the number of VMs that you need now.</span></span> <span data-ttu-id="7b339-151">估計未來成長量，接著使用下表來決定子網路的大小。</span><span class="sxs-lookup"><span data-stu-id="7b339-151">Estimate for future growth, and then use the following table to determine the size of the subnet.</span></span>

| <span data-ttu-id="7b339-152">所需的 VM 數目</span><span class="sxs-lookup"><span data-stu-id="7b339-152">Number of VMs needed</span></span> | <span data-ttu-id="7b339-153">所需的主機位元數</span><span class="sxs-lookup"><span data-stu-id="7b339-153">Number of host bits needed</span></span> | <span data-ttu-id="7b339-154">子網路的大小</span><span class="sxs-lookup"><span data-stu-id="7b339-154">Size of the subnet</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7b339-155">1–3</span><span class="sxs-lookup"><span data-stu-id="7b339-155">1–3</span></span> |<span data-ttu-id="7b339-156">3</span><span class="sxs-lookup"><span data-stu-id="7b339-156">3</span></span> |<span data-ttu-id="7b339-157">/29</span><span class="sxs-lookup"><span data-stu-id="7b339-157">/29</span></span> |
| <span data-ttu-id="7b339-158">4–11</span><span class="sxs-lookup"><span data-stu-id="7b339-158">4–11</span></span> |<span data-ttu-id="7b339-159">4</span><span class="sxs-lookup"><span data-stu-id="7b339-159">4</span></span> |<span data-ttu-id="7b339-160">/28</span><span class="sxs-lookup"><span data-stu-id="7b339-160">/28</span></span> |
| <span data-ttu-id="7b339-161">12–27</span><span class="sxs-lookup"><span data-stu-id="7b339-161">12–27</span></span> |<span data-ttu-id="7b339-162">5</span><span class="sxs-lookup"><span data-stu-id="7b339-162">5</span></span> |<span data-ttu-id="7b339-163">/27</span><span class="sxs-lookup"><span data-stu-id="7b339-163">/27</span></span> |
| <span data-ttu-id="7b339-164">28–59</span><span class="sxs-lookup"><span data-stu-id="7b339-164">28–59</span></span> |<span data-ttu-id="7b339-165">6</span><span class="sxs-lookup"><span data-stu-id="7b339-165">6</span></span> |<span data-ttu-id="7b339-166">/26</span><span class="sxs-lookup"><span data-stu-id="7b339-166">/26</span></span> |
| <span data-ttu-id="7b339-167">60–123</span><span class="sxs-lookup"><span data-stu-id="7b339-167">60–123</span></span> |<span data-ttu-id="7b339-168">7</span><span class="sxs-lookup"><span data-stu-id="7b339-168">7</span></span> |<span data-ttu-id="7b339-169">/25</span><span class="sxs-lookup"><span data-stu-id="7b339-169">/25</span></span> |

> [!NOTE]
> <span data-ttu-id="7b339-170">針對一般的內部部署子網路，適用於含有 n 個主機位元之子網路的主機位址數目上限是 2<sup>n</sup> – 2。</span><span class="sxs-lookup"><span data-stu-id="7b339-170">For normal on-premises subnets, the maximum number of host addresses for a subnet with n host bits is 2<sup>n</sup> – 2.</span></span> <span data-ttu-id="7b339-171">針對 Azure 子網路，適用於含有 n 個主機位元之子網路的主機位址數目上限是 2<sup>n</sup> – 5 (2 加 3 適用於 Azure 在每個子網路上使用的位址)。</span><span class="sxs-lookup"><span data-stu-id="7b339-171">For an Azure subnet, the maximum number of host addresses for a subnet with n host bits is 2<sup>n</sup> – 5 (2 plus 3 for the addresses that Azure uses on each subnet).</span></span>
> 
> 

<span data-ttu-id="7b339-172">如果您選擇的子網路大小太小，就必須在子網路中為 VM 重新指派 IP 並重新部署。</span><span class="sxs-lookup"><span data-stu-id="7b339-172">If you choose a subnet size that is too small, you have to re-IP and redeploy the VMs in the subnet.</span></span>

## <a name="network-security-groups"></a><span data-ttu-id="7b339-173">網路安全性群組</span><span class="sxs-lookup"><span data-stu-id="7b339-173">Network Security Groups</span></span>
<span data-ttu-id="7b339-174">您可以使用網路安全性群組，將篩選規則套用到流經您虛擬網路的流量。</span><span class="sxs-lookup"><span data-stu-id="7b339-174">You can apply filtering rules to the traffic that flows through your virtual networks by using Network Security Groups.</span></span> <span data-ttu-id="7b339-175">您可以建置細微的篩選規則來保護虛擬網路環境、控制傳入和傳出流量、來源和目的地 IP 範圍、允許的連接埠等等。網路安全性群組可以套用到虛擬網路內的子網路，或直接套用到特定的虛擬網路介面。</span><span class="sxs-lookup"><span data-stu-id="7b339-175">You can build granular filtering rules to secure your virtual networking environment, controlling inbound and outbound traffic, source and destination IP ranges, allowed ports, etc. Network Security Groups can be applied to subnets within a virtual network or directly to a given virtual network interface.</span></span> <span data-ttu-id="7b339-176">我們建議您在虛擬網路上擁有某種程度的網路安全性群組來篩選流量。</span><span class="sxs-lookup"><span data-stu-id="7b339-176">It is recommended to have some level of Network Security Group filtering traffic on your virtual networks.</span></span> <span data-ttu-id="7b339-177">您可以深入了解 [網路安全性群組](../../virtual-network/virtual-networks-nsg.md)。</span><span class="sxs-lookup"><span data-stu-id="7b339-177">You can read more about [Network Security Groups](../../virtual-network/virtual-networks-nsg.md).</span></span>

## <a name="additional-network-components"></a><span data-ttu-id="7b339-178">其他網路元件</span><span class="sxs-lookup"><span data-stu-id="7b339-178">Additional network components</span></span>
<span data-ttu-id="7b339-179">和內部部署實體網路基礎結構一樣，Azure 虛擬網路除了子網路和 IP 位址之外，還可以包含更多其他元件。</span><span class="sxs-lookup"><span data-stu-id="7b339-179">As with an on-premises physical networking infrastructure, Azure virtual networking can contain more than just subnets and IP addressing.</span></span> <span data-ttu-id="7b339-180">當您在設計應用程式基礎結構時，您應該納入某些下列的其他元件：</span><span class="sxs-lookup"><span data-stu-id="7b339-180">As you design your application infrastructure, you may want to incorporate some of these additional components:</span></span>

* <span data-ttu-id="7b339-181">[VPN 閘道](../../vpn-gateway/vpn-gateway-about-vpngateways.md) - 將 Azure 虛擬網路連接至其他 Azure 虛擬網路，或透過站對站 VPN 連線連接到內部部署網路。</span><span class="sxs-lookup"><span data-stu-id="7b339-181">[VPN gateways](../../vpn-gateway/vpn-gateway-about-vpngateways.md) - connect Azure virtual networks to other Azure virtual networks, or connect to on-premises networks through a Site-to-Site VPN connection.</span></span> <span data-ttu-id="7b339-182">實作 Express Route 連線以做為專用的安全連線。</span><span class="sxs-lookup"><span data-stu-id="7b339-182">Implement Express Route connections for dedicated, secure connections.</span></span> <span data-ttu-id="7b339-183">您也可以利用點對站 VPN 連線，來提供使用者直接存取。</span><span class="sxs-lookup"><span data-stu-id="7b339-183">You can also provide users direct access with Point-to-Site VPN connections.</span></span>
* <span data-ttu-id="7b339-184">[負載平衡器](../../load-balancer/load-balancer-overview.md) - 視需求針對外部和內部流量提供流量負載平衡。</span><span class="sxs-lookup"><span data-stu-id="7b339-184">[Load balancer](../../load-balancer/load-balancer-overview.md) - provides load balancing of traffic for both external and internal traffic as desired.</span></span>
* <span data-ttu-id="7b339-185">[應用程式閘道](../../application-gateway/application-gateway-introduction.md) - 應用程式層的 HTTP 負載平衡，除了部署 Azure 負載平衡器之外，還能為 Web 應用程式提供一些其他的好處。</span><span class="sxs-lookup"><span data-stu-id="7b339-185">[Application Gateway](../../application-gateway/application-gateway-introduction.md) - HTTP load-balancing at the application layer, providing some additional benefits for web applications rather than deploying the Azure load balancer.</span></span>
* <span data-ttu-id="7b339-186">[流量管理員](../../traffic-manager/traffic-manager-overview.md) - DNS 型流量散發以將終端使用者引導到最接近的可用應用程式端點，讓您可以在不同地區中於 Azure 資料中心之外裝載您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="7b339-186">[Traffic Manager](../../traffic-manager/traffic-manager-overview.md) - DNS-based traffic distribution to direct end-users to the closest available application endpoint, allowing you to host your application out of Azure datacenters in different regions.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7b339-187">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7b339-187">Next steps</span></span>
[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-next-steps](../../../includes/virtual-machines-linux-infrastructure-guidelines-next-steps.md)]

