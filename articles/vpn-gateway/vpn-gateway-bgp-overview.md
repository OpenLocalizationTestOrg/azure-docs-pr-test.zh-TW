---
title: "與 Azure VPN 閘道的 BGP 的 aaaOverview |Microsoft 文件"
description: "本文提供 BGP 與 Azure VPN 閘道的概觀。"
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: 
tags: 
ms.assetid: f8c3985c-c128-4f34-835c-0e88742bf36e
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/12/2017
ms.author: yushwang
ms.openlocfilehash: ced3f77ecd791c84fb72b96447e839be3bf94846
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-bgp-with-azure-vpn-gateways"></a><span data-ttu-id="f3bcc-103">BGP 與 Azure VPN 閘道概觀</span><span class="sxs-lookup"><span data-stu-id="f3bcc-103">Overview of BGP with Azure VPN Gateways</span></span>
<span data-ttu-id="f3bcc-104">這篇文章提供 Azure VPN 閘道中的 BGP (邊界閘道協定) 支援概觀。</span><span class="sxs-lookup"><span data-stu-id="f3bcc-104">This article provides an overview of BGP (Border Gateway Protocol) support in Azure VPN Gateways.</span></span>

<span data-ttu-id="f3bcc-105">BGP 是 hello 標準路由通訊協定常用 hello 網際網路 tooexchange 路由和連線資訊中兩個或多個網路之間。</span><span class="sxs-lookup"><span data-stu-id="f3bcc-105">BGP is hello standard routing protocol commonly used in hello Internet tooexchange routing and reachability information between two or more networks.</span></span> <span data-ttu-id="f3bcc-106">當 hello Azure VPN 閘道和您的內部部署 VPN 裝置，稱為 BGP 對等體的使用 hello Azure 虛擬網路內容中，BGP 啟用或鄰近項目，tooexchange 「 路由 」，將這些通知 hello 可用性和連線的兩個閘道toogo 透過 hello 閘道或路由器所涉及的前置詞。</span><span class="sxs-lookup"><span data-stu-id="f3bcc-106">When used in hello context of Azure Virtual Networks, BGP enables hello Azure VPN Gateways and your on-premises VPN devices, called BGP peers or neighbors, tooexchange "routes" that will inform both gateways on hello availability and reachability for those prefixes toogo through hello gateways or routers involved.</span></span> <span data-ttu-id="f3bcc-107">BGP 也可以啟用傳輸多個網路之間路由傳播路由的 BGP 閘道會從一個 BGP 對等 tooall 學習其他 BGP 對等節點。</span><span class="sxs-lookup"><span data-stu-id="f3bcc-107">BGP can also enable transit routing among multiple networks by propagating routes a BGP gateway learns from one BGP peer tooall other BGP peers.</span></span> 

## <a name="why-use-bgp"></a><span data-ttu-id="f3bcc-108">為何要使用 BGP？</span><span class="sxs-lookup"><span data-stu-id="f3bcc-108">Why use BGP?</span></span>
<span data-ttu-id="f3bcc-109">BGP 是選用功能，可供您與 Azure 路由 VPN 閘道搭配使用。</span><span class="sxs-lookup"><span data-stu-id="f3bcc-109">BGP is an optional feature you can use with Azure Route-Based VPN gateways.</span></span> <span data-ttu-id="f3bcc-110">您也應該確定您在內部部署 VPN 裝置支援 BGP，然後再啟用 hello 功能。</span><span class="sxs-lookup"><span data-stu-id="f3bcc-110">You should also make sure your on-premises VPN devices support BGP before you enable hello feature.</span></span> <span data-ttu-id="f3bcc-111">您可以繼續 toouse Azure VPN 閘道和您在內部部署 VPN 裝置沒有 BGP。</span><span class="sxs-lookup"><span data-stu-id="f3bcc-111">You can continue toouse Azure VPN gateways and your on-premises VPN devices without BGP.</span></span> <span data-ttu-id="f3bcc-112">它是使用靜態路由 （不含 BGP) 對等的 hello*與*使用您的網路與 Azure 之間 bgp 動態路由。</span><span class="sxs-lookup"><span data-stu-id="f3bcc-112">It is hello equivalent of using static routes (without BGP) *vs.* using dynamic routing with BGP between your networks and Azure.</span></span>

<span data-ttu-id="f3bcc-113">BGP 具有數個優點和新功能：</span><span class="sxs-lookup"><span data-stu-id="f3bcc-113">There are several advantages and new capabilities with BGP:</span></span>

### <a name="support-automatic-and-flexible-prefix-updates"></a><span data-ttu-id="f3bcc-114">支援自動和彈性的前置詞更新</span><span class="sxs-lookup"><span data-stu-id="f3bcc-114">Support automatic and flexible prefix updates</span></span>
<span data-ttu-id="f3bcc-115">Bgp，您只需要最小的前置詞 tooa 特定 BGP 對等體 toodeclare 透過 hello IPsec S2S VPN 通道。</span><span class="sxs-lookup"><span data-stu-id="f3bcc-115">With BGP, you only need toodeclare a minimum prefix tooa specific BGP peer over hello IPsec S2S VPN tunnel.</span></span> <span data-ttu-id="f3bcc-116">它可以很小，例如主機首碼 （/ 32） 的 hello 在內部部署 VPN 裝置的 BGP 對等體 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="f3bcc-116">It can be as small as a host prefix (/32) of hello BGP peer IP address of your on-premises VPN device.</span></span> <span data-ttu-id="f3bcc-117">您可以控制其內部部署 Azure 虛擬網路 tooaccess 想 tooadvertise tooAzure tooallow 網路首碼。</span><span class="sxs-lookup"><span data-stu-id="f3bcc-117">You can control which on-premises network prefixes you want tooadvertise tooAzure tooallow your Azure Virtual Network tooaccess.</span></span>

<span data-ttu-id="f3bcc-118">您也可以公告可能包含一些您 VNet 位址首碼的較大首碼，例如大型私人 IP 位址空間 (例如 10.0.0.0/8)。</span><span class="sxs-lookup"><span data-stu-id="f3bcc-118">You can also advertise larger prefixes that may include some of your VNet address prefixes, such as a large private IP address space (for example, 10.0.0.0/8).</span></span> <span data-ttu-id="f3bcc-119">請注意，雖然 hello 前置詞不能與使用任何一種您的 VNet 前置詞。</span><span class="sxs-lookup"><span data-stu-id="f3bcc-119">Note though hello prefixes cannot be identical with any one of your VNet prefixes.</span></span> <span data-ttu-id="f3bcc-120">這些路由相同 tooyour VNet 前置詞會被拒絕。</span><span class="sxs-lookup"><span data-stu-id="f3bcc-120">Those routes identical tooyour VNet prefixes will be rejected.</span></span>

### <a name="support-multiple-tunnels-between-a-vnet-and-an-on-premises-site-with-automatic-failover-based-on-bgp"></a><span data-ttu-id="f3bcc-121">根據 BGP 使用自動容錯移轉，在 VNet 和內部部署站台之間支援多個通道</span><span class="sxs-lookup"><span data-stu-id="f3bcc-121">Support multiple tunnels between a VNet and an on-premises site with automatic failover based on BGP</span></span>
<span data-ttu-id="f3bcc-122">您可以建立多個 Azure VNet 與您在內部部署 VPN 裝置之間的連接 hello 相同的位置。</span><span class="sxs-lookup"><span data-stu-id="f3bcc-122">You can establish multiple connections between your Azure VNet and your on-premises VPN devices in hello same location.</span></span> <span data-ttu-id="f3bcc-123">這項功能在主動-主動組態中的 hello 兩個網路之間提供多個通道 （路徑）。</span><span class="sxs-lookup"><span data-stu-id="f3bcc-123">This capability provides multiple tunnels (paths) between hello two networks in an active-active configuration.</span></span> <span data-ttu-id="f3bcc-124">如果其中一個 hello 通道已中斷連接，hello 對應路由會撤回透過 BGP 和 hello 流量會自動移 toohello 其餘的通道。</span><span class="sxs-lookup"><span data-stu-id="f3bcc-124">If one of hello tunnels is disconnected, hello corresponding routes will be withdrawn via BGP and hello traffic automatically shifts toohello remaining tunnels.</span></span>

<span data-ttu-id="f3bcc-125">hello 下列圖表顯示這個高可用性的安裝程式的簡單範例：</span><span class="sxs-lookup"><span data-stu-id="f3bcc-125">hello following diagram shows a simple example of this highly available setup:</span></span>

![多個作用中路徑](./media/vpn-gateway-bgp-overview/multiple-active-tunnels.png)

### <a name="support-transit-routing-between-your-on-premises-networks-and-multiple-azure-vnets"></a><span data-ttu-id="f3bcc-127">支援內部部署網路與多個 Azure Vnet 之間的傳輸路由</span><span class="sxs-lookup"><span data-stu-id="f3bcc-127">Support transit routing between your on-premises networks and multiple Azure VNets</span></span>
<span data-ttu-id="f3bcc-128">BGP 可以讓多個閘道 toolearn 和傳播前置詞從不同的網路，無論它們直接或間接連接。</span><span class="sxs-lookup"><span data-stu-id="f3bcc-128">BGP enables multiple gateways toolearn and propagate prefixes from different networks, whether they are directly or indirectly connected.</span></span> <span data-ttu-id="f3bcc-129">這可以使用內部部署站台之間的 Azure VPN 閘道，或跨多個 Azure 虛擬網路啟用傳送路由。</span><span class="sxs-lookup"><span data-stu-id="f3bcc-129">This can enable transit routing with Azure VPN gateways between your on-premises sites or across multiple Azure Virtual Networks.</span></span>

<span data-ttu-id="f3bcc-130">hello 下列圖表顯示可以傳輸 hello 透過 Azure VPN 閘道 hello Microsoft 網路內的兩個內部部署網路之間流量的多個路徑的多重躍點拓撲的範例：</span><span class="sxs-lookup"><span data-stu-id="f3bcc-130">hello following diagram shows an example of a multi-hop topology with multiple paths that can transit traffic between hello two on-premises networks through Azure VPN gateways within hello Microsoft Networks:</span></span>

![多重躍點傳輸](./media/vpn-gateway-bgp-overview/full-mesh-transit.png)

## <a name="bgp-faq"></a><span data-ttu-id="f3bcc-132">BGP 常見問題集</span><span class="sxs-lookup"><span data-stu-id="f3bcc-132">BGP FAQ</span></span>
[!INCLUDE [vpn-gateway-bgp-faq-include](../../includes/vpn-gateway-bpg-faq-include.md)]

## <a name="next-steps"></a><span data-ttu-id="f3bcc-133">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f3bcc-133">Next steps</span></span>
<span data-ttu-id="f3bcc-134">請參閱[入門 Azure VPN 閘道的 BGP](vpn-gateway-bgp-resource-manager-ps.md)如步驟 tooconfigure BGP 的跨內部部署與 VNet 對 VNet 連線。</span><span class="sxs-lookup"><span data-stu-id="f3bcc-134">See [Getting started with BGP on Azure VPN gateways](vpn-gateway-bgp-resource-manager-ps.md) for steps tooconfigure BGP for your cross-premises and VNet-to-VNet connections.</span></span>

