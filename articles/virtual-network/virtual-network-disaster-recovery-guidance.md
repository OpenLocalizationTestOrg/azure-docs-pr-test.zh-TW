---
title: "發生影響 Azure 虛擬網路的 Azure 服務中斷事件時該怎麼辦 | Microsoft Docs"
description: "了解發生影響 Azure 虛擬網路的 Azure 服務中斷事件時該怎麼辦"
services: virtual-network
documentationcenter: 
author: NarayanAnnamalai
manager: jefco
editor: 
ms.assetid: ad260ab9-d873-43b3-8896-f9a1db9858a5
ms.service: virtual-network
ms.workload: virtual-network
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2016
ms.author: narayan;aglick
ms.openlocfilehash: 4e125406d2e798138c45e3fbbf61a610afab69fc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="virtual-network--business-continuity"></a><span data-ttu-id="610c8-103">虛擬網路 – 商務持續性</span><span class="sxs-lookup"><span data-stu-id="610c8-103">Virtual Network – Business Continuity</span></span>
## <a name="overview"></a><span data-ttu-id="610c8-104">概觀</span><span class="sxs-lookup"><span data-stu-id="610c8-104">Overview</span></span>
<span data-ttu-id="610c8-105">「虛擬網路」(VNet) 是您網路在雲端的邏輯呈現方式。</span><span class="sxs-lookup"><span data-stu-id="610c8-105">A Virtual Network (VNet) is a logical representation of your network in the cloud.</span></span> <span data-ttu-id="610c8-106">它可讓您定義自己的私人 IP 位址空間，並將網路分割成子網路。</span><span class="sxs-lookup"><span data-stu-id="610c8-106">It allows you to define your own private IP address space and segment the network into subnets.</span></span> <span data-ttu-id="610c8-107">VNet 可做為信任界限來裝載您的運算資源，例如「Azure 虛擬機器」和「雲端服務」(Web/背景工作角色)。</span><span class="sxs-lookup"><span data-stu-id="610c8-107">VNets serves as a trust boundary to host your compute resources such as Azure Virtual Machines and Cloud Services (web/worker roles).</span></span> <span data-ttu-id="610c8-108">VNet 可允許其裝載的資源之間進行直接私人 IP 通訊。</span><span class="sxs-lookup"><span data-stu-id="610c8-108">A VNet allows direct private IP communication between the resources hosted in it.</span></span> <span data-ttu-id="610c8-109">「虛擬網路」也可以透過其中一個混合式選項 (例如「VPN 閘道」或 ExpressRoute) 連結到內部部署網路。</span><span class="sxs-lookup"><span data-stu-id="610c8-109">A Virtual Network can also be linked to an on-premises network through one of the hybrid options such as a VPN Gateway or ExpressRoute.</span></span>

<span data-ttu-id="610c8-110">VNet 是在區域的範圍內建立。</span><span class="sxs-lookup"><span data-stu-id="610c8-110">A VNet is created within the scope of a region.</span></span> <span data-ttu-id="610c8-111">您可以在兩個不同的區域中建立具有相同位址空間的 VNet (亦即美國東部和美國西部，但無法讓它們直接連接到彼此)。</span><span class="sxs-lookup"><span data-stu-id="610c8-111">You can create VNets with same address space in two different regions (i.e. US East and US West but cannot connect them to one another directly).</span></span> 

## <a name="business-continuity"></a><span data-ttu-id="610c8-112">商務持續性</span><span class="sxs-lookup"><span data-stu-id="610c8-112">Business Continuity</span></span>
<span data-ttu-id="610c8-113">可能有數種不同的方式會讓您的應用程式中斷。</span><span class="sxs-lookup"><span data-stu-id="610c8-113">There could be several different ways that your application could be disrupted.</span></span> <span data-ttu-id="610c8-114">指定的區域可能會因天然災害而被完全切斷，或因多個裝置/服務失敗而導致部分損毀。</span><span class="sxs-lookup"><span data-stu-id="610c8-114">A given region could be completely cut off due to a natural disaster or a partial disaster due to a failure of multiple devices/services.</span></span> <span data-ttu-id="610c8-115">這每一種情況對 VNet 服務的影響各有不同。</span><span class="sxs-lookup"><span data-stu-id="610c8-115">The impact on the VNet service is different in each of these situations.</span></span>

<span data-ttu-id="610c8-116">**問︰整個區域發生中斷 (亦即，如果區域因天然災害而完全封閉) 時，該怎麼辦？該區域中所裝載的「虛擬網路」會發生什麼情況？**</span><span class="sxs-lookup"><span data-stu-id="610c8-116">**Q: What do you do in the event of an outage to an entire region? i.e. if a region is completely cutoff due to a natural disaster? What happens to the Virtual Networks hosted in the region?**</span></span>

<span data-ttu-id="610c8-117">答︰在服務中斷期間，受影響區域中的「虛擬網路」及資源都會保持無法供存取的狀態。</span><span class="sxs-lookup"><span data-stu-id="610c8-117">A: The Virtual Network and the resources in the affected region remains inaccessible during the time of the service disruption.</span></span>

![簡單的虛擬網路圖表](./media/virtual-network-disaster-recovery-guidance/vnet.png)

<span data-ttu-id="610c8-119">**問︰若要在不同的區域中重新建立相同的「虛擬網路」，該怎麼做？**</span><span class="sxs-lookup"><span data-stu-id="610c8-119">**Q: What can I to do re-create the same Virtual Network in a different region?**</span></span>

<span data-ttu-id="610c8-120">答︰「虛擬網路」(VNet) 是非常輕量型的資源。</span><span class="sxs-lookup"><span data-stu-id="610c8-120">A: Virtual Network (VNet) is fairly lightweight resource.</span></span> <span data-ttu-id="610c8-121">您可以叫用 Azure API，在不同的區域中建立具有相同位址空間的 VNet。</span><span class="sxs-lookup"><span data-stu-id="610c8-121">You can invoke Azure APIs to create a VNet with the same address space in a different region.</span></span> <span data-ttu-id="610c8-122">若要重新建立受影響區域中所具有的相同環境，您必須進行 API 呼叫來重新部署您的「雲端服務」(Web/背景工作角色) 和您所擁有的「虛擬機器」。</span><span class="sxs-lookup"><span data-stu-id="610c8-122">To re-create the same environment that was present in the affected region, you have to make API calls to re-deploy your Cloud Services (web/worker roles) and Virtual Machines that you had.</span></span> <span data-ttu-id="610c8-123">如果您有內部部署連線 (例如在混合式部署中)，您也必須備妥「VPN 閘道」並連接到內部部署網路。</span><span class="sxs-lookup"><span data-stu-id="610c8-123">You will also have to spin up a VPN Gateway and connect to your on-premises network if you had on-premises connectivity (such as in a hybrid deployment).</span></span>

<span data-ttu-id="610c8-124">[這裡](virtual-networks-create-vnet-arm-pportal.md)提供建立 VNet 的相關指示。</span><span class="sxs-lookup"><span data-stu-id="610c8-124">The instructions for creating a VNet are found [here](virtual-networks-create-vnet-arm-pportal.md).</span></span> 

<span data-ttu-id="610c8-125">**問︰是否可以事先在另一個區域中重新建立指定區域中的 VNet 複本？**</span><span class="sxs-lookup"><span data-stu-id="610c8-125">**Q: Can a replica of a VNet in a given region be re-created in another region ahead of time?**</span></span>

<span data-ttu-id="610c8-126">答︰是，您可以事先在兩個不同的區域中，使用相同的私人 IP 位址空間和資源來建立兩個 VNet。</span><span class="sxs-lookup"><span data-stu-id="610c8-126">A: Yes, you can create two VNets using the same private IP address space and resources in two different regions ahead of time.</span></span> <span data-ttu-id="610c8-127">如果客戶在 VNet 中裝載網際網路面向服務，他們可能已設定「流量管理員」將流量異地路由傳送至使用中的區域。</span><span class="sxs-lookup"><span data-stu-id="610c8-127">If a customer was hosting internet facing services in the VNet, they could have set up Traffic Manager to geo-route traffic to the region that is active.</span></span> <span data-ttu-id="610c8-128">不過，客戶無法將兩個具有相同位址空間的 VNet 連接到其內部部署網路，因為這會造成路由問題。</span><span class="sxs-lookup"><span data-stu-id="610c8-128">However, a customer cannot connect two VNets with the same address space to their on-premises network as it would cause routing issues.</span></span> <span data-ttu-id="610c8-129">當發生災害而失去一個區域中的 VNet 時，客戶可以將位於可用區域中具有相符位址空間的另一個 VNet 連接到其內部部署網路。</span><span class="sxs-lookup"><span data-stu-id="610c8-129">At the time of a disaster and loss of a VNet in one region, a customer can connect the other VNet in the available region with matching address space to their on-premises network.</span></span>

<span data-ttu-id="610c8-130">[這裡](virtual-networks-create-vnet-arm-pportal.md)提供建立 VNet 的相關指示。</span><span class="sxs-lookup"><span data-stu-id="610c8-130">The instructions for creating a VNet are found [here](virtual-networks-create-vnet-arm-pportal.md).</span></span>

