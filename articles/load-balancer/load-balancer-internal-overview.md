---
title: "aaaInternal 負載平衡器概觀 |Microsoft 文件"
description: "內部負載平衡器和其功能的概觀。Azure 和可能的案例 tooconfigure 內部端點的負載平衡器的運作方式"
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
ms.openlocfilehash: 9a901aad224d8821c154e130e142699d57282b25
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="internal-load-balancer-overview"></a><span data-ttu-id="cc7f8-103">內部負載平衡器概觀</span><span class="sxs-lookup"><span data-stu-id="cc7f8-103">Internal load balancer overview</span></span>

<span data-ttu-id="cc7f8-104">不同於 hello 網際網路對向負載平衡器，hello 內部負載平衡器 (ILB) 會指示流量只有 tooresources hello 雲端服務，或使用 VPN tooaccess hello Azure 基礎結構內。</span><span class="sxs-lookup"><span data-stu-id="cc7f8-104">Unlike hello Internet facing load balancer, hello internal load balancer (ILB) directs traffic only tooresources inside hello cloud service or using VPN tooaccess hello Azure infrastructure.</span></span> <span data-ttu-id="cc7f8-105">hello 基礎結構會限制存取 toohello 負載平衡虛擬 IP 位址 (Vip 的雲端服務或虛擬網路)，讓它們絕對不會直接公開的 tooan 網際網路端點。</span><span class="sxs-lookup"><span data-stu-id="cc7f8-105">hello infrastructure restricts access toohello load balanced virtual IP addresses (VIPs) of a Cloud Service or a Virtual Network so that they will never be directly exposed tooan Internet endpoint.</span></span> <span data-ttu-id="cc7f8-106">這可讓在 Azure 中的企業營運 (LOB) 應用程式 toorun 內部一行，並從 hello 雲端內或從存取資源的內部。</span><span class="sxs-lookup"><span data-stu-id="cc7f8-106">This enables internal line of business (LOB) applications toorun in Azure and be accessed from within hello cloud or from resources on-premises.</span></span>

## <a name="why-you-may-need-an-internal-load-balancer"></a><span data-ttu-id="cc7f8-107">為何需要內部負載平衡器</span><span class="sxs-lookup"><span data-stu-id="cc7f8-107">Why you may need an internal load balancer</span></span>

<span data-ttu-id="cc7f8-108">Azure 內部負載平衡 (ILB) 可在位於雲端服務或虛擬網路 (具有區域範圍) 中的虛擬機器之間提供負載平衡。</span><span class="sxs-lookup"><span data-stu-id="cc7f8-108">Azure Internal Load Balancing (ILB) provides load balancing between virtual machines that reside inside of a cloud service or a virtual network with a regional scope.</span></span> <span data-ttu-id="cc7f8-109">如需使用 hello 和具有區域範圍的虛擬網路的組態資訊，請參閱[地區虛擬網路](https://azure.microsoft.com/blog/2014/05/14/regional-virtual-networks/)在 hello Azure 部落格。</span><span class="sxs-lookup"><span data-stu-id="cc7f8-109">For information about hello use and configuration of virtual networks with a regional scope, see [Regional Virtual Networks](https://azure.microsoft.com/blog/2014/05/14/regional-virtual-networks/) in hello Azure blog.</span></span> <span data-ttu-id="cc7f8-110">已針對同質群組設定的現有虛擬網路無法使用 ILB。</span><span class="sxs-lookup"><span data-stu-id="cc7f8-110">Existing virtual networks that have been configured for an affinity group cannot use ILB.</span></span>

<span data-ttu-id="cc7f8-111">ILB 能夠達到下列類型的負載平衡的 hello:</span><span class="sxs-lookup"><span data-stu-id="cc7f8-111">ILB enables hello following types of load balancing:</span></span>

* <span data-ttu-id="cc7f8-112">在雲端服務中，從虛擬機器 tooa 集位於 hello 內的虛擬機器的相同雲端服務 （請參閱圖 1）。</span><span class="sxs-lookup"><span data-stu-id="cc7f8-112">Within a cloud service, from virtual machines tooa set of virtual machines that reside within hello same cloud service (see Figure 1).</span></span>
* <span data-ttu-id="cc7f8-113">虛擬網路內的虛擬機器位於 hello hello 虛擬網路 tooa 集合中的虛擬機器從相同雲端服務的 hello 虛擬網路 （請參閱圖 2）。</span><span class="sxs-lookup"><span data-stu-id="cc7f8-113">Within a virtual network, from virtual machines in hello virtual network tooa set of virtual machines that reside within hello same cloud service of hello virtual network (see Figure 2).</span></span>
* <span data-ttu-id="cc7f8-114">跨單位虛擬網路中，從內部部署電腦 tooa 組位於 hello 內的虛擬機器的相同雲端服務的 hello 虛擬網路 （請參閱圖 3）。</span><span class="sxs-lookup"><span data-stu-id="cc7f8-114">For a cross-premises virtual network, from on-premises computers tooa set of virtual machines that reside within hello same cloud service of hello virtual network (see Figure 3).</span></span>
* <span data-ttu-id="cc7f8-115">網際網路對向、 多層式應用程式中 hello 後端層並非網際網路對向，但需要的負載平衡流量從 hello 網際網路對向層。</span><span class="sxs-lookup"><span data-stu-id="cc7f8-115">Internet-facing, multi-tier applications in which hello back-end tiers are not Internet-facing but require load balancing for traffic from hello Internet-facing tier.</span></span>
* <span data-ttu-id="cc7f8-116">在不需要額外負載平衡器硬體或軟體的情況下，針對裝載於 Azure 中的 LOB 應用程式進行負載平衡。</span><span class="sxs-lookup"><span data-stu-id="cc7f8-116">Load balancing for LOB applications hosted in Azure without requiring additional load balancer hardware or software.</span></span> <span data-ttu-id="cc7f8-117">在內部部署伺服器納入 hello 的一組電腦的流量進行負載平衡。</span><span class="sxs-lookup"><span data-stu-id="cc7f8-117">Including on-premises servers in hello set of computers whose traffic is load balanced.</span></span>

## <a name="internet-facing-multi-tier-applications"></a><span data-ttu-id="cc7f8-118">網際網路面向的多層式應用程式</span><span class="sxs-lookup"><span data-stu-id="cc7f8-118">Internet facing multi-tier applications</span></span>

<span data-ttu-id="cc7f8-119">hello web 層有網際網路用戶端的網際網路對向端點，而且是一組負載平衡的一部分。</span><span class="sxs-lookup"><span data-stu-id="cc7f8-119">hello web tier has Internet facing endpoints for Internet clients and is part of a load-balanced set.</span></span> <span data-ttu-id="cc7f8-120">hello 負載平衡器會將連入流量的 TCP 連接埠 443 (HTTPS) toohello 網頁伺服器的 web 用戶端。</span><span class="sxs-lookup"><span data-stu-id="cc7f8-120">hello load balancer  distributes incoming traffic from web clients for TCP port 443 (HTTPS) toohello web servers.</span></span>

<span data-ttu-id="cc7f8-121">hello 資料庫伺服器位於 ILB 端點 hello 網頁伺服器用於儲存體。</span><span class="sxs-lookup"><span data-stu-id="cc7f8-121">hello database servers are behind an ILB endpoint which hello web servers use for storage.</span></span> <span data-ttu-id="cc7f8-122">此資料庫服務的負載平衡的端點的流量進行負載平衡到 hello ILB 集合中的 hello 的資料庫伺服器。</span><span class="sxs-lookup"><span data-stu-id="cc7f8-122">This database service load balanced endpoint, which traffic is load balanced across hello database servers in hello ILB set.</span></span>

<span data-ttu-id="cc7f8-123">下列影像顯示 hello hello 網際網路對向多層式應用程式內 hello 相同雲端服務。</span><span class="sxs-lookup"><span data-stu-id="cc7f8-123">hello following image shows hello Internet facing multi-tier application within hello same cloud service.</span></span>

![單一雲端服務的內部負載平衡](./media/load-balancer-internal-overview/IC736321.png)

<span data-ttu-id="cc7f8-125">圖 1 - 網際網路面向的多層式應用程式</span><span class="sxs-lookup"><span data-stu-id="cc7f8-125">Figure 1 - Internet facing multi-tier application</span></span>

<span data-ttu-id="cc7f8-126">Hello ILB 部署 tooa 不同雲端服務，比 hello hello ILB 取用一個 hello 服務時的多層式應用程式的另一個可能的使用。</span><span class="sxs-lookup"><span data-stu-id="cc7f8-126">Another possible use for a multi-tier application is when hello ILB deployed tooa different cloud service than hello one consuming hello service for hello ILB.</span></span>

<span data-ttu-id="cc7f8-127">雲端服務使用相同的虛擬網路將會有的 hello 存取 toohello ILB 端點。</span><span class="sxs-lookup"><span data-stu-id="cc7f8-127">Cloud services using hello same virtual network will have access toohello ILB endpoint.</span></span> <span data-ttu-id="cc7f8-128">下列影像顯示前端 web 伺服器位於不同雲端服務從 hello 資料庫後端，並使用 hello hello hello 中的只剩下 ILB 端點相同虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="cc7f8-128">hello following image shows front-end web servers are in a different cloud service from hello database back-end and using hello ILB endpoint within hello same virtual network.</span></span>

![雲端服務之間的內部負載平衡](./media/load-balancer-internal-overview/IC744147.png)

<span data-ttu-id="cc7f8-130">圖 2 - 位於不同雲端服務的前端伺服器</span><span class="sxs-lookup"><span data-stu-id="cc7f8-130">Figure 2 - Front-end servers in a different cloud service</span></span>

## <a name="intranet-line-of-business-applications"></a><span data-ttu-id="cc7f8-131">內部網路企業營運應用程式</span><span class="sxs-lookup"><span data-stu-id="cc7f8-131">Intranet line of business applications</span></span>

<span data-ttu-id="cc7f8-132">從用戶端 hello 與內部網路上的流量達到負載平衡的 LOB 伺服器使用 VPN 連線 tooAzure 網路 hello 組。</span><span class="sxs-lookup"><span data-stu-id="cc7f8-132">Traffic from clients on hello on-premises network get load-balanced across hello set of LOB servers using VPN connection tooAzure network.</span></span>

<span data-ttu-id="cc7f8-133">hello 用戶端電腦會從 Azure VPN 服務使用點 toosite VPN 存取 tooan IP 位址。</span><span class="sxs-lookup"><span data-stu-id="cc7f8-133">hello client machine will have access tooan IP address from Azure VPN service using point toosite VPN.</span></span> <span data-ttu-id="cc7f8-134">它可讓 hello 使用 hello hello ILB 端點之後託管的 LOB 應用程式。</span><span class="sxs-lookup"><span data-stu-id="cc7f8-134">It allows hello use hello LOB application hosted behind hello ILB endpoint.</span></span>

![內部負載平衡使用點 toosite VPN](./media/load-balancer-internal-overview/IC744148.png)

<span data-ttu-id="cc7f8-136">圖 3: hello LB 端點之後託管的 LOB 應用程式</span><span class="sxs-lookup"><span data-stu-id="cc7f8-136">Figure 3 - LOB applications hosted behind hello LB endpoint</span></span>

<span data-ttu-id="cc7f8-137">Hello LOB 的另一個案例是 toohave 站 toosite VPN toohello 虛擬網路已 hello ILB 端點。</span><span class="sxs-lookup"><span data-stu-id="cc7f8-137">Another scenario for hello LOB is toohave a site toosite VPN toohello virtual network where hello ILB endpoint is configured.</span></span> <span data-ttu-id="cc7f8-138">這可讓內部網路流量路由傳送 toobe toohello ILB 端點。</span><span class="sxs-lookup"><span data-stu-id="cc7f8-138">This allows on-premises network traffic toobe routed toohello ILB endpoint.</span></span>

![內部負載平衡使用站台 toosite VPN](./media/load-balancer-internal-overview/IC744150.png)

<span data-ttu-id="cc7f8-140">圖 4-在內部部署網路流量路由傳送 toohello ILB 端點</span><span class="sxs-lookup"><span data-stu-id="cc7f8-140">Figure 4 - On-premises network traffic routed toohello ILB endpoint</span></span>

## <a name="limitations"></a><span data-ttu-id="cc7f8-141">限制</span><span class="sxs-lookup"><span data-stu-id="cc7f8-141">Limitations</span></span>

<span data-ttu-id="cc7f8-142">內部負載平衡器組態不支援 SNAT。</span><span class="sxs-lookup"><span data-stu-id="cc7f8-142">Internal Load Balancer configurations do not support SNAT.</span></span> <span data-ttu-id="cc7f8-143">在 hello 本文內容，SNAT 是指 tooport 偽裝來源網路位址轉譯。</span><span class="sxs-lookup"><span data-stu-id="cc7f8-143">In hello context of this document, SNAT refers tooport masquerading source  network address translation.</span></span>  <span data-ttu-id="cc7f8-144">這適用於的 tooscenarios 負載平衡器集區中的 VM 需要 tooreach hello 個別內部負載平衡器的前端 IP 位址的地方。</span><span class="sxs-lookup"><span data-stu-id="cc7f8-144">This applies tooscenarios where a VM in a load balancer pool needs tooreach hello respective internal Load Balancer's frontend IP address.</span></span> <span data-ttu-id="cc7f8-145">內部負載平衡器不支援這種情況。</span><span class="sxs-lookup"><span data-stu-id="cc7f8-145">This scenario is not supported for internal Load Balancer.</span></span> <span data-ttu-id="cc7f8-146">負載平衡 toohello 引發 hello 流程 VM hello 流程時，會發生連接失敗。</span><span class="sxs-lookup"><span data-stu-id="cc7f8-146">Connection failures will occur when hello flow is load balanced toohello VM which originated hello flow.</span></span> <span data-ttu-id="cc7f8-147">對於這類情況，您必須使用 Proxy 形式負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="cc7f8-147">You must use a proxy style load balancer for such scenarios.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cc7f8-148">後續步驟</span><span class="sxs-lookup"><span data-stu-id="cc7f8-148">Next Steps</span></span>

[<span data-ttu-id="cc7f8-149">Azure Resource Manager 的 Azure Load Balancer 支援</span><span class="sxs-lookup"><span data-stu-id="cc7f8-149">Azure Resource Manager support for Azure Load Balancer</span></span>](load-balancer-arm.md)

[<span data-ttu-id="cc7f8-150">開始設定網際網路面向的負載平衡器</span><span class="sxs-lookup"><span data-stu-id="cc7f8-150">Get started configuring an Internet facing load balancer</span></span>](load-balancer-get-started-internet-arm-ps.md)

[<span data-ttu-id="cc7f8-151">開始設定內部負載平衡器</span><span class="sxs-lookup"><span data-stu-id="cc7f8-151">Get started configuring an Internal load balancer</span></span>](load-balancer-get-started-ilb-arm-ps.md)

[<span data-ttu-id="cc7f8-152">設定負載平衡器分配模式</span><span class="sxs-lookup"><span data-stu-id="cc7f8-152">Configure a Load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="cc7f8-153">設定負載平衡器的閒置 TCP 逾時設定</span><span class="sxs-lookup"><span data-stu-id="cc7f8-153">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
