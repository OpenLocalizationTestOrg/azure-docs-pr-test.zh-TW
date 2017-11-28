---
title: "在 hello 事件影響到 Azure 虛擬網路的 Azure 服務中斷的 aaaWhat toodo |Microsoft 文件"
description: "了解哪些 toodo hello 影響到 Azure 虛擬網路的 Azure 服務中斷事件中。"
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
ms.openlocfilehash: db022d2a042d255cf8ec6afb68cd8436aeecfe08
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="virtual-network--business-continuity"></a><span data-ttu-id="dea7c-103">虛擬網路 – 商務持續性</span><span class="sxs-lookup"><span data-stu-id="dea7c-103">Virtual Network – Business Continuity</span></span>
## <a name="overview"></a><span data-ttu-id="dea7c-104">概觀</span><span class="sxs-lookup"><span data-stu-id="dea7c-104">Overview</span></span>
<span data-ttu-id="dea7c-105">虛擬網路 (VNet) 是網路的您 hello 雲端中的邏輯表示法。</span><span class="sxs-lookup"><span data-stu-id="dea7c-105">A Virtual Network (VNet) is a logical representation of your network in hello cloud.</span></span> <span data-ttu-id="dea7c-106">它可讓您 toodefine 自己私用 IP 位址空間與區段 hello 網路至子網路。</span><span class="sxs-lookup"><span data-stu-id="dea7c-106">It allows you toodefine your own private IP address space and segment hello network into subnets.</span></span> <span data-ttu-id="dea7c-107">Vnet 做為信任界限 toohost 您的計算資源，例如 Azure 虛擬機器和雲端服務 （web/背景工作角色）。</span><span class="sxs-lookup"><span data-stu-id="dea7c-107">VNets serves as a trust boundary toohost your compute resources such as Azure Virtual Machines and Cloud Services (web/worker roles).</span></span> <span data-ttu-id="dea7c-108">VNet 可讓您直接裝載於它的 hello 資源之間的私用 IP 通訊。</span><span class="sxs-lookup"><span data-stu-id="dea7c-108">A VNet allows direct private IP communication between hello resources hosted in it.</span></span> <span data-ttu-id="dea7c-109">虛擬網路也可以透過下列其中一 hello 混合式選項，例如 VPN 閘道或 ExpressRoute 連結的 tooan 在內部部署網路。</span><span class="sxs-lookup"><span data-stu-id="dea7c-109">A Virtual Network can also be linked tooan on-premises network through one of hello hybrid options such as a VPN Gateway or ExpressRoute.</span></span>

<span data-ttu-id="dea7c-110">VNet 建立區域的 hello 範圍內。</span><span class="sxs-lookup"><span data-stu-id="dea7c-110">A VNet is created within hello scope of a region.</span></span> <span data-ttu-id="dea7c-111">您可以使用相同的位址空間中兩個不同區域建立 Vnet (也就是美國東部和美國西部但無法連接它們 tooone 直接另一個)。</span><span class="sxs-lookup"><span data-stu-id="dea7c-111">You can create VNets with same address space in two different regions (i.e. US East and US West but cannot connect them tooone another directly).</span></span> 

## <a name="business-continuity"></a><span data-ttu-id="dea7c-112">商務持續性</span><span class="sxs-lookup"><span data-stu-id="dea7c-112">Business Continuity</span></span>
<span data-ttu-id="dea7c-113">可能有數種不同的方式會讓您的應用程式中斷。</span><span class="sxs-lookup"><span data-stu-id="dea7c-113">There could be several different ways that your application could be disrupted.</span></span> <span data-ttu-id="dea7c-114">給定的區域可能會被切斷到期 tooa 天然災害或由於多個裝置/伺服器 tooa 失敗部分損毀。</span><span class="sxs-lookup"><span data-stu-id="dea7c-114">A given region could be completely cut off due tooa natural disaster or a partial disaster due tooa failure of multiple devices/services.</span></span> <span data-ttu-id="dea7c-115">hello 對影響 hello VNet 服務會在每種情況不同。</span><span class="sxs-lookup"><span data-stu-id="dea7c-115">hello impact on hello VNet service is different in each of these situations.</span></span>

<span data-ttu-id="dea7c-116">**問： 該怎麼辦的中斷 tooan 整個地區的 hello 事件中？亦即，如果區域是完全截止 tooa 天然災害到期？發生什麼事的 toohello hello 區域中裝載的虛擬網路？**</span><span class="sxs-lookup"><span data-stu-id="dea7c-116">**Q: What do you do in hello event of an outage tooan entire region? i.e. if a region is completely cutoff due tooa natural disaster? What happens toohello Virtual Networks hosted in hello region?**</span></span>

<span data-ttu-id="dea7c-117">答： hello 虛擬網路和 hello 資源 hello 受影響區域會維持為 hello 服務中斷的 hello 期間無法存取。</span><span class="sxs-lookup"><span data-stu-id="dea7c-117">A: hello Virtual Network and hello resources in hello affected region remains inaccessible during hello time of hello service disruption.</span></span>

![簡單的虛擬網路圖表](./media/virtual-network-disaster-recovery-guidance/vnet.png)

<span data-ttu-id="dea7c-119">**問： 我可以 toodo 重新建立 hello 不同區域中的相同虛擬網路？**</span><span class="sxs-lookup"><span data-stu-id="dea7c-119">**Q: What can I toodo re-create hello same Virtual Network in a different region?**</span></span>

<span data-ttu-id="dea7c-120">答︰「虛擬網路」(VNet) 是非常輕量型的資源。</span><span class="sxs-lookup"><span data-stu-id="dea7c-120">A: Virtual Network (VNet) is fairly lightweight resource.</span></span> <span data-ttu-id="dea7c-121">您可以叫用 Azure Api toocreate VNet 與 hello 相同位址不同的區域中的空間。</span><span class="sxs-lookup"><span data-stu-id="dea7c-121">You can invoke Azure APIs toocreate a VNet with hello same address space in a different region.</span></span> <span data-ttu-id="dea7c-122">toore-建立 hello 相同的環境的 hello 在受影響的區域，您必須 toomake API 呼叫 toore-部署雲端服務 （web/背景工作角色） 和您所擁有的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="dea7c-122">toore-create hello same environment that was present in hello affected region, you have toomake API calls toore-deploy your Cloud Services (web/worker roles) and Virtual Machines that you had.</span></span> <span data-ttu-id="dea7c-123">您也必須 toospin VPN 閘道及 tooyour 在內部部署網路連線，如果您已在內部部署連線 （例如，在混合式部署）。</span><span class="sxs-lookup"><span data-stu-id="dea7c-123">You will also have toospin up a VPN Gateway and connect tooyour on-premises network if you had on-premises connectivity (such as in a hybrid deployment).</span></span>

<span data-ttu-id="dea7c-124">找到 hello 相關指示，來建立 VNet[這裡](virtual-networks-create-vnet-arm-pportal.md)。</span><span class="sxs-lookup"><span data-stu-id="dea7c-124">hello instructions for creating a VNet are found [here](virtual-networks-create-vnet-arm-pportal.md).</span></span> 

<span data-ttu-id="dea7c-125">**問︰是否可以事先在另一個區域中重新建立指定區域中的 VNet 複本？**</span><span class="sxs-lookup"><span data-stu-id="dea7c-125">**Q: Can a replica of a VNet in a given region be re-created in another region ahead of time?**</span></span>

<span data-ttu-id="dea7c-126">答: [是]，您可以建立兩個 Vnet 使用 hello 相同的私人 IP 位址空間和時間之前有兩個不同區域中的資源。</span><span class="sxs-lookup"><span data-stu-id="dea7c-126">A: Yes, you can create two VNets using hello same private IP address space and resources in two different regions ahead of time.</span></span> <span data-ttu-id="dea7c-127">如果客戶已裝載網際網路對向 hello VNet 中的服務，它們可能已設定為使用中的 Traffic Manager toogeo 路由流量 toohello 區域。</span><span class="sxs-lookup"><span data-stu-id="dea7c-127">If a customer was hosting internet facing services in hello VNet, they could have set up Traffic Manager toogeo-route traffic toohello region that is active.</span></span> <span data-ttu-id="dea7c-128">不過，客戶無法連接兩個 Vnet 與 hello 相同位址空間 tootheir 在內部部署網路將會造成路由問題。</span><span class="sxs-lookup"><span data-stu-id="dea7c-128">However, a customer cannot connect two VNets with hello same address space tootheir on-premises network as it would cause routing issues.</span></span> <span data-ttu-id="dea7c-129">客戶可以在 hello 發生災害時，在某個區域 VNet 遺失連接 hello hello 與相符的位址空間 tootheir 在內部部署網路的可用區域中的其他 VNet。</span><span class="sxs-lookup"><span data-stu-id="dea7c-129">At hello time of a disaster and loss of a VNet in one region, a customer can connect hello other VNet in hello available region with matching address space tootheir on-premises network.</span></span>

<span data-ttu-id="dea7c-130">找到 hello 相關指示，來建立 VNet[這裡](virtual-networks-create-vnet-arm-pportal.md)。</span><span class="sxs-lookup"><span data-stu-id="dea7c-130">hello instructions for creating a VNet are found [here](virtual-networks-create-vnet-arm-pportal.md).</span></span>

