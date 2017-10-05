---
title: "內部負載平衡器概觀 | Microsoft Docs"
description: "內部負載平衡器與其功能的概觀。負載平衡器如何作用於 Azure 和可能案例，以設定內部端點"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: tysonn
ms.assetid: 36065bfe-0ef1-46f9-a9e1-80b229105c85
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: d324aaf8ec2c8766d5cf11452158d14c19cba4d9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="internal-load-balancer-overview"></a><span data-ttu-id="5bf72-103">內部負載平衡器概觀</span><span class="sxs-lookup"><span data-stu-id="5bf72-103">Internal load balancer overview</span></span>

<span data-ttu-id="5bf72-104">不同於網際網路面向的負載平衡器，內部負載平衡器 (ILB) 只會將流量引導到雲端服務內部的資源，或使用 VPN 來存取 Azure 基礎結構。</span><span class="sxs-lookup"><span data-stu-id="5bf72-104">Unlike the Internet facing load balancer, the internal load balancer (ILB) directs traffic only to resources inside the cloud service or using VPN to access the Azure infrastructure.</span></span> <span data-ttu-id="5bf72-105">基礎結構會限制對雲端服務或虛擬網路的負載平衡虛擬 IP 位址 (VIP) 的存取，因此絕對不會直接向網際網路端點公開這些 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="5bf72-105">The infrastructure restricts access to the load balanced virtual IP addresses (VIPs) of a Cloud Service or a Virtual Network so that they will never be directly exposed to an Internet endpoint.</span></span> <span data-ttu-id="5bf72-106">這可讓內部企業營運 (LOB) 應用程式在 Azure 中執行，而且可從雲端內或從內部部署資源存取。</span><span class="sxs-lookup"><span data-stu-id="5bf72-106">This enables internal line of business (LOB) applications to run in Azure and be accessed from within the cloud or from resources on-premises.</span></span>

## <a name="why-you-may-need-an-internal-load-balancer"></a><span data-ttu-id="5bf72-107">為何需要內部負載平衡器</span><span class="sxs-lookup"><span data-stu-id="5bf72-107">Why you may need an internal load balancer</span></span>

<span data-ttu-id="5bf72-108">Azure 內部負載平衡 (ILB) 可在位於雲端服務或虛擬網路 (具有區域範圍) 中的虛擬機器之間提供負載平衡。</span><span class="sxs-lookup"><span data-stu-id="5bf72-108">Azure Internal Load Balancing (ILB) provides load balancing between virtual machines that reside inside of a cloud service or a virtual network with a regional scope.</span></span> <span data-ttu-id="5bf72-109">如需使用和設定具有區域範圍之虛擬網路的相關資訊，請參閱 Azure 部落格中的 [區域虛擬網路](https://azure.microsoft.com/blog/2014/05/14/regional-virtual-networks/) 。</span><span class="sxs-lookup"><span data-stu-id="5bf72-109">For information about the use and configuration of virtual networks with a regional scope, see [Regional Virtual Networks](https://azure.microsoft.com/blog/2014/05/14/regional-virtual-networks/) in the Azure blog.</span></span> <span data-ttu-id="5bf72-110">已針對同質群組設定的現有虛擬網路無法使用 ILB。</span><span class="sxs-lookup"><span data-stu-id="5bf72-110">Existing virtual networks that have been configured for an affinity group cannot use ILB.</span></span>

<span data-ttu-id="5bf72-111">ILB 可提供下列幾種負載平衡類型：</span><span class="sxs-lookup"><span data-stu-id="5bf72-111">ILB enables the following types of load balancing:</span></span>

* <span data-ttu-id="5bf72-112">在雲端服務中，從虛擬機器至一組位於相同雲端服務內的虛擬機器 (請參閱圖 1)。</span><span class="sxs-lookup"><span data-stu-id="5bf72-112">Within a cloud service, from virtual machines to a set of virtual machines that reside within the same cloud service (see Figure 1).</span></span>
* <span data-ttu-id="5bf72-113">在虛擬網路中，從虛擬網路中的虛擬機器至一組位於虛擬網路的相同雲端服務中的虛擬機器 (請參閱圖 2)。</span><span class="sxs-lookup"><span data-stu-id="5bf72-113">Within a virtual network, from virtual machines in the virtual network to a set of virtual machines that reside within the same cloud service of the virtual network (see Figure 2).</span></span>
* <span data-ttu-id="5bf72-114">在跨單位部署的虛擬網路中，從內部部署電腦至一組位於虛擬網路的相同雲端服務中的虛擬機器 (請參閱圖 3)。</span><span class="sxs-lookup"><span data-stu-id="5bf72-114">For a cross-premises virtual network, from on-premises computers to a set of virtual machines that reside within the same cloud service of the virtual network (see Figure 3).</span></span>
* <span data-ttu-id="5bf72-115">網際網路對向、多層式應用程式，其中後端層並非網際網路面向，但要求來自網際網路面向層的流量達到負載平衡。</span><span class="sxs-lookup"><span data-stu-id="5bf72-115">Internet-facing, multi-tier applications in which the back-end tiers are not Internet-facing but require load balancing for traffic from the Internet-facing tier.</span></span>
* <span data-ttu-id="5bf72-116">在不需要額外負載平衡器硬體或軟體的情況下，針對裝載於 Azure 中的 LOB 應用程式進行負載平衡。</span><span class="sxs-lookup"><span data-stu-id="5bf72-116">Load balancing for LOB applications hosted in Azure without requiring additional load balancer hardware or software.</span></span> <span data-ttu-id="5bf72-117">包括流量已負載平衡之電腦集合中的內部部署伺服器。</span><span class="sxs-lookup"><span data-stu-id="5bf72-117">Including on-premises servers in the set of computers whose traffic is load balanced.</span></span>

## <a name="internet-facing-multi-tier-applications"></a><span data-ttu-id="5bf72-118">網際網路面向的多層式應用程式</span><span class="sxs-lookup"><span data-stu-id="5bf72-118">Internet facing multi-tier applications</span></span>

<span data-ttu-id="5bf72-119">Web 層具有網際網路用戶端的網際網路面向端點，而且是負載平衡集合的一部分。</span><span class="sxs-lookup"><span data-stu-id="5bf72-119">The web tier has Internet facing endpoints for Internet clients and is part of a load-balanced set.</span></span> <span data-ttu-id="5bf72-120">負載平衡器會將來自 TCP 連接埠 443 (HTTPS) 的 Web 用戶端的連入流量分配給 Web 伺服器。</span><span class="sxs-lookup"><span data-stu-id="5bf72-120">The load balancer  distributes incoming traffic from web clients for TCP port 443 (HTTPS) to the web servers.</span></span>

<span data-ttu-id="5bf72-121">資料庫伺服器位於 Web 伺服器用於儲存的 ILB 端點之後。</span><span class="sxs-lookup"><span data-stu-id="5bf72-121">The database servers are behind an ILB endpoint which the web servers use for storage.</span></span> <span data-ttu-id="5bf72-122">這是資料庫服務負載平衡的端點，其流量會在 ILB 集合中的各資料庫伺服器上達到負載平衡。</span><span class="sxs-lookup"><span data-stu-id="5bf72-122">This database service load balanced endpoint, which traffic is load balanced across the database servers in the ILB set.</span></span>

<span data-ttu-id="5bf72-123">下圖顯示相同雲端服務中網際網路面向的多層式應用程式。</span><span class="sxs-lookup"><span data-stu-id="5bf72-123">The following image shows the Internet facing multi-tier application within the same cloud service.</span></span>

![單一雲端服務的內部負載平衡](./media/load-balancer-internal-overview/IC736321.png)

<span data-ttu-id="5bf72-125">圖 1 - 網際網路面向的多層式應用程式</span><span class="sxs-lookup"><span data-stu-id="5bf72-125">Figure 1 - Internet facing multi-tier application</span></span>

<span data-ttu-id="5bf72-126">多層式應用程式的另一個可能用途，是 ILB 部署到與取用 ILB 服務不同的雲端服務的情況。</span><span class="sxs-lookup"><span data-stu-id="5bf72-126">Another possible use for a multi-tier application is when the ILB deployed to a different cloud service than the one consuming the service for the ILB.</span></span>

<span data-ttu-id="5bf72-127">使用相同虛擬網路的雲端服務會有 ILB 端點的存取權。</span><span class="sxs-lookup"><span data-stu-id="5bf72-127">Cloud services using the same virtual network will have access to the ILB endpoint.</span></span> <span data-ttu-id="5bf72-128">下圖顯示前端 Web 伺服器與資料庫後端位於不同的雲端服務，並使用相同虛擬網路內的 ILB 端點。</span><span class="sxs-lookup"><span data-stu-id="5bf72-128">The following image shows front-end web servers are in a different cloud service from the database back-end and using the ILB endpoint within the same virtual network.</span></span>

![雲端服務之間的內部負載平衡](./media/load-balancer-internal-overview/IC744147.png)

<span data-ttu-id="5bf72-130">圖 2 - 位於不同雲端服務的前端伺服器</span><span class="sxs-lookup"><span data-stu-id="5bf72-130">Figure 2 - Front-end servers in a different cloud service</span></span>

## <a name="intranet-line-of-business-applications"></a><span data-ttu-id="5bf72-131">內部網路企業營運應用程式</span><span class="sxs-lookup"><span data-stu-id="5bf72-131">Intranet line of business applications</span></span>

<span data-ttu-id="5bf72-132">使用 Azure 網路的 VPN 連線，可讓 LOB 伺服器集合中來自內部部署網路上用戶端的流量達到負載平衡。</span><span class="sxs-lookup"><span data-stu-id="5bf72-132">Traffic from clients on the on-premises network get load-balanced across the set of LOB servers using VPN connection to Azure network.</span></span>

<span data-ttu-id="5bf72-133">用戶端電腦將能透過端點對站台 VPN 存取來自 Azure VPN 的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="5bf72-133">The client machine will have access to an IP address from Azure VPN service using point to site VPN.</span></span> <span data-ttu-id="5bf72-134">它能允許使用裝載於 ILB 端點後方的 LOB 應用程式。</span><span class="sxs-lookup"><span data-stu-id="5bf72-134">It allows the use the LOB application hosted behind the ILB endpoint.</span></span>

![使用端點對站台 VPN 的內部負載平衡](./media/load-balancer-internal-overview/IC744148.png)

<span data-ttu-id="5bf72-136">圖 3 - 裝載於 LB 端點後方的 LOB 應用程式</span><span class="sxs-lookup"><span data-stu-id="5bf72-136">Figure 3 - LOB applications hosted behind the LB endpoint</span></span>

<span data-ttu-id="5bf72-137">LOB 的另一個案例是有站台對站台 VPN 至 ILB 端點設定所在的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="5bf72-137">Another scenario for the LOB is to have a site to site VPN to the virtual network where the ILB endpoint is configured.</span></span> <span data-ttu-id="5bf72-138">這可讓內部部署網路流量路由傳送至 ILB 端點。</span><span class="sxs-lookup"><span data-stu-id="5bf72-138">This allows on-premises network traffic to be routed to the ILB endpoint.</span></span>

![使用站台對站台 VPN 的內部負載平衡](./media/load-balancer-internal-overview/IC744150.png)

<span data-ttu-id="5bf72-140">圖 4 - 內部部署網路流量路由傳送至 ILB 端點</span><span class="sxs-lookup"><span data-stu-id="5bf72-140">Figure 4 - On-premises network traffic routed to the ILB endpoint</span></span>

## <a name="limitations"></a><span data-ttu-id="5bf72-141">限制</span><span class="sxs-lookup"><span data-stu-id="5bf72-141">Limitations</span></span>

<span data-ttu-id="5bf72-142">內部負載平衡器組態不支援 SNAT。</span><span class="sxs-lookup"><span data-stu-id="5bf72-142">Internal Load Balancer configurations do not support SNAT.</span></span> <span data-ttu-id="5bf72-143">在此文件的內容中，SNAT 是指連接埠偽裝來源網路位址轉譯。</span><span class="sxs-lookup"><span data-stu-id="5bf72-143">In the context of this document, SNAT refers to port masquerading source  network address translation.</span></span>  <span data-ttu-id="5bf72-144">這適用於負載平衡器集區的 VM 需要連接個別內部負載平衡器前端 IP 位址的情況。</span><span class="sxs-lookup"><span data-stu-id="5bf72-144">This applies to scenarios where a VM in a load balancer pool needs to reach the respective internal Load Balancer's frontend IP address.</span></span> <span data-ttu-id="5bf72-145">內部負載平衡器不支援這種情況。</span><span class="sxs-lookup"><span data-stu-id="5bf72-145">This scenario is not supported for internal Load Balancer.</span></span> <span data-ttu-id="5bf72-146">流量經過負載平衡傳輸至起始流程的 VM 時，會發生連線失敗。</span><span class="sxs-lookup"><span data-stu-id="5bf72-146">Connection failures will occur when the flow is load balanced to the VM which originated the flow.</span></span> <span data-ttu-id="5bf72-147">對於這類情況，您必須使用 Proxy 形式負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="5bf72-147">You must use a proxy style load balancer for such scenarios.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5bf72-148">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5bf72-148">Next Steps</span></span>

[<span data-ttu-id="5bf72-149">Azure Resource Manager 的 Azure Load Balancer 支援</span><span class="sxs-lookup"><span data-stu-id="5bf72-149">Azure Resource Manager support for Azure Load Balancer</span></span>](load-balancer-arm.md)

[<span data-ttu-id="5bf72-150">開始設定網際網路面向的負載平衡器</span><span class="sxs-lookup"><span data-stu-id="5bf72-150">Get started configuring an Internet facing load balancer</span></span>](load-balancer-get-started-internet-arm-ps.md)

[<span data-ttu-id="5bf72-151">開始設定內部負載平衡器</span><span class="sxs-lookup"><span data-stu-id="5bf72-151">Get started configuring an Internal load balancer</span></span>](load-balancer-get-started-ilb-arm-ps.md)

[<span data-ttu-id="5bf72-152">設定負載平衡器分配模式</span><span class="sxs-lookup"><span data-stu-id="5bf72-152">Configure a Load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="5bf72-153">設定負載平衡器的閒置 TCP 逾時設定</span><span class="sxs-lookup"><span data-stu-id="5bf72-153">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
