---
title: "連接 Azure 虛擬網路 tooanother VNet: PowerShell |Microsoft 文件"
description: "本文將逐步引導您使用 Azure 資源管理員和 PowerShell，將虛擬網路連接在一起。"
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 0683c664-9c03-40a4-b198-a6529bf1ce8b
ms.service: vpn-gateway
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/02/2017
ms.author: cherylmc
ms.openlocfilehash: 2da30c76867cc3f71d040e63e0dd15d153e15c10
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-vnet-to-vnet-vpn-gateway-connection-using-powershell"></a><span data-ttu-id="d4f05-103">使用 PowerShell 設定 VNet 對 VNet 的 VPN 閘道連線</span><span class="sxs-lookup"><span data-stu-id="d4f05-103">Configure a VNet-to-VNet VPN gateway connection using PowerShell</span></span>

<span data-ttu-id="d4f05-104">本文章將示範如何 toocreate 虛擬網路之間的 VPN 閘道連線。</span><span class="sxs-lookup"><span data-stu-id="d4f05-104">This article shows you how toocreate a VPN gateway connection between virtual networks.</span></span> <span data-ttu-id="d4f05-105">hello 虛擬網路可在 hello 相同或不同區域，並從 hello 相同或不同的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="d4f05-105">hello virtual networks can be in hello same or different regions, and from hello same or different subscriptions.</span></span> <span data-ttu-id="d4f05-106">當連接的 Vnet，從不同的訂用帳戶，hello 訂用帳戶不需要與相關聯的 toobe hello 相同的 Active Directory 租用戶。</span><span class="sxs-lookup"><span data-stu-id="d4f05-106">When connecting VNets from different subscriptions, hello subscriptions do not need toobe associated with hello same Active Directory tenant.</span></span> 

<span data-ttu-id="d4f05-107">這篇文章中的 hello 步驟套用 toohello Resource Manager 部署模型，並使用 PowerShell。</span><span class="sxs-lookup"><span data-stu-id="d4f05-107">hello steps in this article apply toohello Resource Manager deployment model and use PowerShell.</span></span> <span data-ttu-id="d4f05-108">您也可以建立此組態使用不同的部署工具或部署模型，從下列清單中的 hello 選取不同的選項：</span><span class="sxs-lookup"><span data-stu-id="d4f05-108">You can also create this configuration using a different deployment tool or deployment model by selecting a different option from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="d4f05-109">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="d4f05-109">Azure portal</span></span>](vpn-gateway-howto-vnet-vnet-resource-manager-portal.md)
> * [<span data-ttu-id="d4f05-110">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d4f05-110">PowerShell</span></span>](vpn-gateway-vnet-vnet-rm-ps.md)
> * [<span data-ttu-id="d4f05-111">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="d4f05-111">Azure CLI</span></span>](vpn-gateway-howto-vnet-vnet-cli.md)
> * [<span data-ttu-id="d4f05-112">Azure 入口網站 (傳統)</span><span class="sxs-lookup"><span data-stu-id="d4f05-112">Azure portal (classic)</span></span>](vpn-gateway-howto-vnet-vnet-portal-classic.md)
> * [<span data-ttu-id="d4f05-113">連線不同的部署模型 - Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="d4f05-113">Connect different deployment models - Azure portal</span></span>](vpn-gateway-connect-different-deployment-models-portal.md)
> * [<span data-ttu-id="d4f05-114">連線不同的部署模型 - PowerShell</span><span class="sxs-lookup"><span data-stu-id="d4f05-114">Connect different deployment models - PowerShell</span></span>](vpn-gateway-connect-different-deployment-models-powershell.md)
>
>

<span data-ttu-id="d4f05-115">連接虛擬網路 tooanother 虛擬網路 (VNet 對 VNet) 是類似 tooconnecting VNet tooan 在內部部署站台位置。</span><span class="sxs-lookup"><span data-stu-id="d4f05-115">Connecting a virtual network tooanother virtual network (VNet-to-VNet) is similar tooconnecting a VNet tooan on-premises site location.</span></span> <span data-ttu-id="d4f05-116">這兩種連線類型使用的 VPN 閘道 tooprovide 採用 IPsec/IKE 的安全通道。</span><span class="sxs-lookup"><span data-stu-id="d4f05-116">Both connectivity types use a VPN gateway tooprovide a secure tunnel using IPsec/IKE.</span></span> <span data-ttu-id="d4f05-117">如果您的 Vnet hello 中相同的區域，您可能會想 tooconsider 它們使用對等互連的 VNet 連接。</span><span class="sxs-lookup"><span data-stu-id="d4f05-117">If your VNets are in hello same region, you may want tooconsider connecting them using VNet Peering.</span></span> <span data-ttu-id="d4f05-118">VNet 對等互連不會使用 VPN 閘道。</span><span class="sxs-lookup"><span data-stu-id="d4f05-118">VNet peering does not use a VPN gateway.</span></span> <span data-ttu-id="d4f05-119">如需詳細資訊，請參閱 [VNet 對等互連](../virtual-network/virtual-network-peering-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="d4f05-119">For more information, see [VNet peering](../virtual-network/virtual-network-peering-overview.md).</span></span>

<span data-ttu-id="d4f05-120">您可以將 VNet 對 VNet 通訊與多站台組態結合。</span><span class="sxs-lookup"><span data-stu-id="d4f05-120">VNet-to-VNet communication can be combined with multi-site configurations.</span></span> <span data-ttu-id="d4f05-121">這可讓您建立結合內部虛擬網路連線使用跨單位連線的網路拓樸 hello 下列圖表所示：</span><span class="sxs-lookup"><span data-stu-id="d4f05-121">This lets you establish network topologies that combine cross-premises connectivity with inter-virtual network connectivity, as shown in hello following diagram:</span></span>

![關於連線](./media/vpn-gateway-vnet-vnet-rm-ps/aboutconnections.png)

### <a name="why-connect-virtual-networks"></a><span data-ttu-id="d4f05-123">為什麼要連接虛擬網路？</span><span class="sxs-lookup"><span data-stu-id="d4f05-123">Why connect virtual networks?</span></span>

<span data-ttu-id="d4f05-124">您可以遵循原因 hello tooconnect 虛擬網路：</span><span class="sxs-lookup"><span data-stu-id="d4f05-124">You may want tooconnect virtual networks for hello following reasons:</span></span>

* <span data-ttu-id="d4f05-125">**跨區域的異地備援和異地目前狀態**</span><span class="sxs-lookup"><span data-stu-id="d4f05-125">**Cross region geo-redundancy and geo-presence**</span></span>

  * <span data-ttu-id="d4f05-126">您可以使用安全連線設定自己的異地複寫或同步處理，而不用查看網際網路對向端點。</span><span class="sxs-lookup"><span data-stu-id="d4f05-126">You can set up your own geo-replication or synchronization with secure connectivity without going over Internet-facing endpoints.</span></span>
  * <span data-ttu-id="d4f05-127">您可以使用 Azure 流量管理員和負載平衡器，利用異地備援跨多個 Azure 區域設定高度可用的工作負載。</span><span class="sxs-lookup"><span data-stu-id="d4f05-127">With Azure Traffic Manager and Load Balancer, you can set up highly available workload with geo-redundancy across multiple Azure regions.</span></span> <span data-ttu-id="d4f05-128">重要的一個例子是 tooset 設定 SQL Always On 與分配到多個 Azure 區域的可用性群組。</span><span class="sxs-lookup"><span data-stu-id="d4f05-128">One important example is tooset up SQL Always On with Availability Groups spreading across multiple Azure regions.</span></span>
* <span data-ttu-id="d4f05-129">**具有隔離或管理界限的區域性多層式應用程式**</span><span class="sxs-lookup"><span data-stu-id="d4f05-129">**Regional multi-tier applications with isolation or administrative boundary**</span></span>

  * <span data-ttu-id="d4f05-130">在 hello 相同區域中，您可以設定多層應用程式與多個虛擬網路連接在一起，因為 tooisolation 或系統管理需求。</span><span class="sxs-lookup"><span data-stu-id="d4f05-130">Within hello same region, you can set up multi-tier applications with multiple virtual networks connected together due tooisolation or administrative requirements.</span></span>

<span data-ttu-id="d4f05-131">如需 VNet 對 VNet 連線的詳細資訊，請參閱 hello [VNet 對 VNet 常見問題集](#faq)hello 本文結尾處。</span><span class="sxs-lookup"><span data-stu-id="d4f05-131">For more information about VNet-to-VNet connections, see hello [VNet-to-VNet FAQ](#faq) at hello end of this article.</span></span>

## <a name="which-set-of-steps-should-i-use"></a><span data-ttu-id="d4f05-132">我應該使用哪個步驟集？</span><span class="sxs-lookup"><span data-stu-id="d4f05-132">Which set of steps should I use?</span></span>

<span data-ttu-id="d4f05-133">在本文中，您會看到兩組不同的步驟。</span><span class="sxs-lookup"><span data-stu-id="d4f05-133">In this article, you see two different sets of steps.</span></span> <span data-ttu-id="d4f05-134">一組步驟[Vnet 中的 hello 相同訂用帳戶](#samesub)，而另一個用於[位於不同的訂用帳戶中的 Vnet](#difsub)。</span><span class="sxs-lookup"><span data-stu-id="d4f05-134">One set of steps for [VNets that reside in hello same subscription](#samesub), and another for [VNets that reside in different subscriptions](#difsub).</span></span> <span data-ttu-id="d4f05-135">hello hello 組之間的主要差異是您可以在建立及設定中的所有虛擬網路和閘道資源 hello 同一個 PowerShell 工作階段。</span><span class="sxs-lookup"><span data-stu-id="d4f05-135">hello key difference between hello sets is whether you can create and configure all virtual network and gateway resources within hello same PowerShell session.</span></span>

<span data-ttu-id="d4f05-136">hello 本文章中的步驟使用會在每個區段的 hello 開頭宣告的變數。</span><span class="sxs-lookup"><span data-stu-id="d4f05-136">hello steps in this article use variables that are declared at hello beginning of each section.</span></span> <span data-ttu-id="d4f05-137">如果您已經使用現有的 Vnet，修改 hello 變數 tooreflect hello 中設定您自己的環境。</span><span class="sxs-lookup"><span data-stu-id="d4f05-137">If you already are working with existing VNets, modify hello variables tooreflect hello settings in your own environment.</span></span> <span data-ttu-id="d4f05-138">如果您想要了解虛擬網路的名稱解析，請參閱[名稱解析](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md)。</span><span class="sxs-lookup"><span data-stu-id="d4f05-138">If you want name resolution for your virtual networks, see [Name resolution](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).</span></span>

## <span data-ttu-id="d4f05-139"><a name="samesub"></a>如何 tooconnect Vnet 處於 hello 相同訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="d4f05-139"><a name="samesub"></a>How tooconnect VNets that are in hello same subscription</span></span>

![v2v 圖表](./media/vpn-gateway-vnet-vnet-rm-ps/v2vrmps.png)

### <a name="before-you-begin"></a><span data-ttu-id="d4f05-141">開始之前</span><span class="sxs-lookup"><span data-stu-id="d4f05-141">Before you begin</span></span>

<span data-ttu-id="d4f05-142">在開始之前，您需要 tooinstall hello 最新版本的 hello Azure 資源管理員 PowerShell cmdlet，至少 4.0 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="d4f05-142">Before beginning, you need tooinstall hello latest version of hello Azure Resource Manager PowerShell cmdlets, at least 4.0 or later.</span></span> <span data-ttu-id="d4f05-143">如需安裝 hello PowerShell cmdlet 的詳細資訊，請參閱[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="d4f05-143">For more information about installing hello PowerShell cmdlets, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

### <span data-ttu-id="d4f05-144"><a name="Step1"></a>步驟 1 - 規劃 IP 位址範圍</span><span class="sxs-lookup"><span data-stu-id="d4f05-144"><a name="Step1"></a>Step 1 - Plan your IP address ranges</span></span>

<span data-ttu-id="d4f05-145">在 hello 下列步驟，我們會建立兩個虛擬網路，以及其個別的閘道子網路和設定。</span><span class="sxs-lookup"><span data-stu-id="d4f05-145">In hello following steps, we create two virtual networks along with their respective gateway subnets and configurations.</span></span> <span data-ttu-id="d4f05-146">我們再建立 hello 之間的 VPN 連線兩個 Vnet。</span><span class="sxs-lookup"><span data-stu-id="d4f05-146">We then create a VPN connection between hello two VNets.</span></span> <span data-ttu-id="d4f05-147">它是您的網路設定的重要 tooplan hello IP 位址範圍。</span><span class="sxs-lookup"><span data-stu-id="d4f05-147">It’s important tooplan hello IP address ranges for your network configuration.</span></span> <span data-ttu-id="d4f05-148">請記住，您必須先確定您的 VNet 範圍或區域網路範圍沒有以任何方式重疊。</span><span class="sxs-lookup"><span data-stu-id="d4f05-148">Keep in mind that you must make sure that none of your VNet ranges or local network ranges overlap in any way.</span></span> <span data-ttu-id="d4f05-149">在這些範例中，我們不會包含 DNS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="d4f05-149">In these examples, we do not include a DNS server.</span></span> <span data-ttu-id="d4f05-150">如果您想要了解虛擬網路的名稱解析，請參閱[名稱解析](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md)。</span><span class="sxs-lookup"><span data-stu-id="d4f05-150">If you want name resolution for your virtual networks, see [Name resolution](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).</span></span>

<span data-ttu-id="d4f05-151">我們使用下列值 hello 範例中的 hello:</span><span class="sxs-lookup"><span data-stu-id="d4f05-151">We use hello following values in hello examples:</span></span>

<span data-ttu-id="d4f05-152">**TestVNet1 的值︰**</span><span class="sxs-lookup"><span data-stu-id="d4f05-152">**Values for TestVNet1:**</span></span>

* <span data-ttu-id="d4f05-153">VNet 名稱︰TestVNet1</span><span class="sxs-lookup"><span data-stu-id="d4f05-153">VNet Name: TestVNet1</span></span>
* <span data-ttu-id="d4f05-154">資源群組︰TestRG1</span><span class="sxs-lookup"><span data-stu-id="d4f05-154">Resource Group: TestRG1</span></span>
* <span data-ttu-id="d4f05-155">位置：美國東部</span><span class="sxs-lookup"><span data-stu-id="d4f05-155">Location: East US</span></span>
* <span data-ttu-id="d4f05-156">TestVNet1：10.11.0.0/16 和 10.12.0.0/16</span><span class="sxs-lookup"><span data-stu-id="d4f05-156">TestVNet1: 10.11.0.0/16 & 10.12.0.0/16</span></span>
* <span data-ttu-id="d4f05-157">FrontEnd：10.11.0.0/24</span><span class="sxs-lookup"><span data-stu-id="d4f05-157">FrontEnd: 10.11.0.0/24</span></span>
* <span data-ttu-id="d4f05-158">BackEnd：10.12.0.0/24</span><span class="sxs-lookup"><span data-stu-id="d4f05-158">BackEnd: 10.12.0.0/24</span></span>
* <span data-ttu-id="d4f05-159">GatewaySubnet：10.12.255.0/27</span><span class="sxs-lookup"><span data-stu-id="d4f05-159">GatewaySubnet: 10.12.255.0/27</span></span>
* <span data-ttu-id="d4f05-160">GatewayName：VNet1GW</span><span class="sxs-lookup"><span data-stu-id="d4f05-160">GatewayName: VNet1GW</span></span>
* <span data-ttu-id="d4f05-161">公用 IP: VNet1GWIP</span><span class="sxs-lookup"><span data-stu-id="d4f05-161">Public IP: VNet1GWIP</span></span>
* <span data-ttu-id="d4f05-162">VPNType：RouteBased</span><span class="sxs-lookup"><span data-stu-id="d4f05-162">VPNType: RouteBased</span></span>
* <span data-ttu-id="d4f05-163">Connection(1to4)：VNet1toVNet4</span><span class="sxs-lookup"><span data-stu-id="d4f05-163">Connection(1to4): VNet1toVNet4</span></span>
* <span data-ttu-id="d4f05-164">Connection(1to5)：VNet1toVNet5</span><span class="sxs-lookup"><span data-stu-id="d4f05-164">Connection(1to5): VNet1toVNet5</span></span>
* <span data-ttu-id="d4f05-165">ConnectionType：VNet2VNet</span><span class="sxs-lookup"><span data-stu-id="d4f05-165">ConnectionType: VNet2VNet</span></span>

<span data-ttu-id="d4f05-166">**TestVNet4 的值︰**</span><span class="sxs-lookup"><span data-stu-id="d4f05-166">**Values for TestVNet4:**</span></span>

* <span data-ttu-id="d4f05-167">VNet 名稱︰TestVNet4</span><span class="sxs-lookup"><span data-stu-id="d4f05-167">VNet Name: TestVNet4</span></span>
* <span data-ttu-id="d4f05-168">TestVNet2：10.41.0.0/16 和 10.42.0.0/16</span><span class="sxs-lookup"><span data-stu-id="d4f05-168">TestVNet2: 10.41.0.0/16 & 10.42.0.0/16</span></span>
* <span data-ttu-id="d4f05-169">FrontEnd：10.41.0.0/24</span><span class="sxs-lookup"><span data-stu-id="d4f05-169">FrontEnd: 10.41.0.0/24</span></span>
* <span data-ttu-id="d4f05-170">BackEnd：10.42.0.0/24</span><span class="sxs-lookup"><span data-stu-id="d4f05-170">BackEnd: 10.42.0.0/24</span></span>
* <span data-ttu-id="d4f05-171">GatewaySubnet：10.42.255.0/27</span><span class="sxs-lookup"><span data-stu-id="d4f05-171">GatewaySubnet: 10.42.255.0/27</span></span>
* <span data-ttu-id="d4f05-172">資源群組：TestRG4</span><span class="sxs-lookup"><span data-stu-id="d4f05-172">Resource Group: TestRG4</span></span>
* <span data-ttu-id="d4f05-173">位置：美國西部</span><span class="sxs-lookup"><span data-stu-id="d4f05-173">Location: West US</span></span>
* <span data-ttu-id="d4f05-174">GatewayName：VNet4GW</span><span class="sxs-lookup"><span data-stu-id="d4f05-174">GatewayName: VNet4GW</span></span>
* <span data-ttu-id="d4f05-175">公用 IP：VNet4GWIP</span><span class="sxs-lookup"><span data-stu-id="d4f05-175">Public IP: VNet4GWIP</span></span>
* <span data-ttu-id="d4f05-176">VPNType：RouteBased</span><span class="sxs-lookup"><span data-stu-id="d4f05-176">VPNType: RouteBased</span></span>
* <span data-ttu-id="d4f05-177">連線︰VNet4toVNet1</span><span class="sxs-lookup"><span data-stu-id="d4f05-177">Connection: VNet4toVNet1</span></span>
* <span data-ttu-id="d4f05-178">ConnectionType：VNet2VNet</span><span class="sxs-lookup"><span data-stu-id="d4f05-178">ConnectionType: VNet2VNet</span></span>


### <span data-ttu-id="d4f05-179"><a name="Step2"></a>步驟 2 - 建立及設定 TestVNet1</span><span class="sxs-lookup"><span data-stu-id="d4f05-179"><a name="Step2"></a>Step 2 - Create and configure TestVNet1</span></span>

1. <span data-ttu-id="d4f05-180">宣告變數。</span><span class="sxs-lookup"><span data-stu-id="d4f05-180">Declare your variables.</span></span> <span data-ttu-id="d4f05-181">這個範例會宣告 hello 針對此練習使用 hello 值的變數。</span><span class="sxs-lookup"><span data-stu-id="d4f05-181">This example declares hello variables using hello values for this exercise.</span></span> <span data-ttu-id="d4f05-182">在大部分情況下，您應該 hello 值取代您自己。</span><span class="sxs-lookup"><span data-stu-id="d4f05-182">In most cases, you should replace hello values with your own.</span></span> <span data-ttu-id="d4f05-183">不過，您可以使用這些變數，如果您正在透過 hello 步驟 toobecome 熟悉這種類型的組態。</span><span class="sxs-lookup"><span data-stu-id="d4f05-183">However, you can use these variables if you are running through hello steps toobecome familiar with this type of configuration.</span></span> <span data-ttu-id="d4f05-184">修改 hello 變數，如有需要然後複製並貼至 PowerShell 主控台。</span><span class="sxs-lookup"><span data-stu-id="d4f05-184">Modify hello variables if needed, then copy and paste them into your PowerShell console.</span></span>

  ```powershell
  $Sub1 = "Replace_With_Your_Subcription_Name"
  $RG1 = "TestRG1"
  $Location1 = "East US"
  $VNetName1 = "TestVNet1"
  $FESubName1 = "FrontEnd"
  $BESubName1 = "Backend"
  $GWSubName1 = "GatewaySubnet"
  $VNetPrefix11 = "10.11.0.0/16"
  $VNetPrefix12 = "10.12.0.0/16"
  $FESubPrefix1 = "10.11.0.0/24"
  $BESubPrefix1 = "10.12.0.0/24"
  $GWSubPrefix1 = "10.12.255.0/27"
  $GWName1 = "VNet1GW"
  $GWIPName1 = "VNet1GWIP"
  $GWIPconfName1 = "gwipconf1"
  $Connection14 = "VNet1toVNet4"
  $Connection15 = "VNet1toVNet5"
  ```

2. <span data-ttu-id="d4f05-185">Tooyour 帳戶連接。</span><span class="sxs-lookup"><span data-stu-id="d4f05-185">Connect tooyour account.</span></span> <span data-ttu-id="d4f05-186">使用下列範例 toohelp 您連接的 hello:</span><span class="sxs-lookup"><span data-stu-id="d4f05-186">Use hello following example toohelp you connect:</span></span>

  ```powershell
  Login-AzureRmAccount
  ```

  <span data-ttu-id="d4f05-187">請檢查 hello hello 帳戶的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="d4f05-187">Check hello subscriptions for hello account.</span></span>

  ```powershell
  Get-AzureRmSubscription
  ```

  <span data-ttu-id="d4f05-188">指定您想 toouse hello 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="d4f05-188">Specify hello subscription that you want toouse.</span></span>

  ```powershell
  Select-AzureRmSubscription -SubscriptionName $Sub1
  ```
3. <span data-ttu-id="d4f05-189">建立新的資源群組。</span><span class="sxs-lookup"><span data-stu-id="d4f05-189">Create a new resource group.</span></span>

  ```powershell
  New-AzureRmResourceGroup -Name $RG1 -Location $Location1
  ```
4. <span data-ttu-id="d4f05-190">建立 hello TestVNet1 的子網路組態。</span><span class="sxs-lookup"><span data-stu-id="d4f05-190">Create hello subnet configurations for TestVNet1.</span></span> <span data-ttu-id="d4f05-191">此範例會建立一個名為 TestVNet1 的虛擬網路和三個子網路：一個名為 GatewaySubnet、一個名為 FrontEnd，另一個名為 Backend。</span><span class="sxs-lookup"><span data-stu-id="d4f05-191">This example creates a virtual network named TestVNet1 and three subnets, one called GatewaySubnet, one called FrontEnd, and one called Backend.</span></span> <span data-ttu-id="d4f05-192">替代值時，務必一律將您的閘道子網路特定命名為 GatewaySubnet。</span><span class="sxs-lookup"><span data-stu-id="d4f05-192">When substituting values, it's important that you always name your gateway subnet specifically GatewaySubnet.</span></span> <span data-ttu-id="d4f05-193">如果您將其命名為其他名稱，閘道建立會失敗。</span><span class="sxs-lookup"><span data-stu-id="d4f05-193">If you name it something else, your gateway creation fails.</span></span>

  <span data-ttu-id="d4f05-194">hello 下列範例會使用您先前設定的 hello 變數。</span><span class="sxs-lookup"><span data-stu-id="d4f05-194">hello following example uses hello variables that you set earlier.</span></span> <span data-ttu-id="d4f05-195">在此範例中，使用 /27 hello 閘道子網路。</span><span class="sxs-lookup"><span data-stu-id="d4f05-195">In this example, hello gateway subnet is using a /27.</span></span> <span data-ttu-id="d4f05-196">雖然可能 toocreate 閘道子網路為/29，我們建議您建立較大的子網路選取至少是/28 或 /27 包含多個位址。</span><span class="sxs-lookup"><span data-stu-id="d4f05-196">While it is possible toocreate a gateway subnet as small as /29, we recommend that you create a larger subnet that includes more addresses by selecting at least /28 or /27.</span></span> <span data-ttu-id="d4f05-197">這可讓足夠位址 tooaccommodate 可能其他組態，您可能想在 hello 未來。</span><span class="sxs-lookup"><span data-stu-id="d4f05-197">This will allow for enough addresses tooaccommodate possible additional configurations that you may want in hello future.</span></span>

  ```powershell
  $fesub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName1 -AddressPrefix $FESubPrefix1
  $besub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName1 -AddressPrefix $BESubPrefix1
  $gwsub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName1 -AddressPrefix $GWSubPrefix1
  ```
5. <span data-ttu-id="d4f05-198">建立 TestVNet1。</span><span class="sxs-lookup"><span data-stu-id="d4f05-198">Create TestVNet1.</span></span>

  ```powershell
  New-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1 `
  -Location $Location1 -AddressPrefix $VNetPrefix11,$VNetPrefix12 -Subnet $fesub1,$besub1,$gwsub1
  ```
6. <span data-ttu-id="d4f05-199">要求的公用 IP 位址 toobe 配置的 toohello 閘道您將建立您的 VNet。</span><span class="sxs-lookup"><span data-stu-id="d4f05-199">Request a public IP address toobe allocated toohello gateway you will create for your VNet.</span></span> <span data-ttu-id="d4f05-200">請注意該 hello AllocationMethod 是動態。</span><span class="sxs-lookup"><span data-stu-id="d4f05-200">Notice that hello AllocationMethod is Dynamic.</span></span> <span data-ttu-id="d4f05-201">您無法指定您想 toouse hello IP 位址。</span><span class="sxs-lookup"><span data-stu-id="d4f05-201">You cannot specify hello IP address that you want toouse.</span></span> <span data-ttu-id="d4f05-202">它是動態配置的 tooyour 閘道。</span><span class="sxs-lookup"><span data-stu-id="d4f05-202">It's dynamically allocated tooyour gateway.</span></span> 

  ```powershell
  $gwpip1 = New-AzureRmPublicIpAddress -Name $GWIPName1 -ResourceGroupName $RG1 `
  -Location $Location1 -AllocationMethod Dynamic
  ```
7. <span data-ttu-id="d4f05-203">建立 hello 閘道設定。</span><span class="sxs-lookup"><span data-stu-id="d4f05-203">Create hello gateway configuration.</span></span> <span data-ttu-id="d4f05-204">hello 閘道組態會定義 hello 子網路和公用 IP 位址 toouse hello。</span><span class="sxs-lookup"><span data-stu-id="d4f05-204">hello gateway configuration defines hello subnet and hello public IP address toouse.</span></span> <span data-ttu-id="d4f05-205">使用 hello 範例 toocreate 閘道設定。</span><span class="sxs-lookup"><span data-stu-id="d4f05-205">Use hello example toocreate your gateway configuration.</span></span>

  ```powershell
  $vnet1 = Get-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1
  $subnet1 = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet1
  $gwipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName1 `
  -Subnet $subnet1 -PublicIpAddress $gwpip1
  ```
8. <span data-ttu-id="d4f05-206">建立 TestVNet1 hello 閘道。</span><span class="sxs-lookup"><span data-stu-id="d4f05-206">Create hello gateway for TestVNet1.</span></span> <span data-ttu-id="d4f05-207">在此步驟中，您建立您 TestVNet1 hello 虛擬網路閘道。</span><span class="sxs-lookup"><span data-stu-id="d4f05-207">In this step, you create hello virtual network gateway for your TestVNet1.</span></span> <span data-ttu-id="d4f05-208">VNet 對 VNet 組態需要 RouteBased VpnType。</span><span class="sxs-lookup"><span data-stu-id="d4f05-208">VNet-to-VNet configurations require a RouteBased VpnType.</span></span> <span data-ttu-id="d4f05-209">建立閘道可以通常要花費 45 分鐘以上，視 hello 選取的閘道 SKU。</span><span class="sxs-lookup"><span data-stu-id="d4f05-209">Creating a gateway can often take 45 minutes or more, depending on hello selected gateway SKU.</span></span>

  ```powershell
  New-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1 `
  -Location $Location1 -IpConfigurations $gwipconf1 -GatewayType Vpn `
  -VpnType RouteBased -GatewaySku VpnGw1
  ```

### <a name="step-3---create-and-configure-testvnet4"></a><span data-ttu-id="d4f05-210">步驟 3 - 建立及設定 TestVNet4</span><span class="sxs-lookup"><span data-stu-id="d4f05-210">Step 3 - Create and configure TestVNet4</span></span>

<span data-ttu-id="d4f05-211">設定 TestVNet1 後，請建立 TestVNet4。</span><span class="sxs-lookup"><span data-stu-id="d4f05-211">Once you've configured TestVNet1, create TestVNet4.</span></span> <span data-ttu-id="d4f05-212">請遵循下面取代您自己時所需 hello 值 hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="d4f05-212">Follow hello steps below, replacing hello values with your own when needed.</span></span> <span data-ttu-id="d4f05-213">此步驟即可 hello 內相同的 PowerShell 工作階段因為它處於 hello 相同訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="d4f05-213">This step can be done within hello same PowerShell session because it is in hello same subscription.</span></span>

1. <span data-ttu-id="d4f05-214">宣告變數。</span><span class="sxs-lookup"><span data-stu-id="d4f05-214">Declare your variables.</span></span> <span data-ttu-id="d4f05-215">為確定 tooreplace 以 hello 的 hello 值的 toouse 您的組態。</span><span class="sxs-lookup"><span data-stu-id="d4f05-215">Be sure tooreplace hello values with hello ones that you want toouse for your configuration.</span></span>

  ```powershell
  $RG4 = "TestRG4"
  $Location4 = "West US"
  $VnetName4 = "TestVNet4"
  $FESubName4 = "FrontEnd"
  $BESubName4 = "Backend"
  $GWSubName4 = "GatewaySubnet"
  $VnetPrefix41 = "10.41.0.0/16"
  $VnetPrefix42 = "10.42.0.0/16"
  $FESubPrefix4 = "10.41.0.0/24"
  $BESubPrefix4 = "10.42.0.0/24"
  $GWSubPrefix4 = "10.42.255.0/27"
  $GWName4 = "VNet4GW"
  $GWIPName4 = "VNet4GWIP"
  $GWIPconfName4 = "gwipconf4"
  $Connection41 = "VNet4toVNet1"
  ```
2. <span data-ttu-id="d4f05-216">建立新的資源群組。</span><span class="sxs-lookup"><span data-stu-id="d4f05-216">Create a new resource group.</span></span>

  ```powershell
  New-AzureRmResourceGroup -Name $RG4 -Location $Location4
  ```
3. <span data-ttu-id="d4f05-217">建立 hello TestVNet4 的子網路組態。</span><span class="sxs-lookup"><span data-stu-id="d4f05-217">Create hello subnet configurations for TestVNet4.</span></span>

  ```powershell
  $fesub4 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName4 -AddressPrefix $FESubPrefix4
  $besub4 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName4 -AddressPrefix $BESubPrefix4
  $gwsub4 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName4 -AddressPrefix $GWSubPrefix4
  ```
4. <span data-ttu-id="d4f05-218">建立 TestVNet4。</span><span class="sxs-lookup"><span data-stu-id="d4f05-218">Create TestVNet4.</span></span>

  ```powershell
  New-AzureRmVirtualNetwork -Name $VnetName4 -ResourceGroupName $RG4 `
  -Location $Location4 -AddressPrefix $VnetPrefix41,$VnetPrefix42 -Subnet $fesub4,$besub4,$gwsub4
  ```
5. <span data-ttu-id="d4f05-219">要求公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="d4f05-219">Request a public IP address.</span></span>

  ```powershell
  $gwpip4 = New-AzureRmPublicIpAddress -Name $GWIPName4 -ResourceGroupName $RG4 `
  -Location $Location4 -AllocationMethod Dynamic
  ```
6. <span data-ttu-id="d4f05-220">建立 hello 閘道設定。</span><span class="sxs-lookup"><span data-stu-id="d4f05-220">Create hello gateway configuration.</span></span>

  ```powershell
  $vnet4 = Get-AzureRmVirtualNetwork -Name $VnetName4 -ResourceGroupName $RG4
  $subnet4 = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet4
  $gwipconf4 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName4 -Subnet $subnet4 -PublicIpAddress $gwpip4
  ```
7. <span data-ttu-id="d4f05-221">建立 hello TestVNet4 閘道。</span><span class="sxs-lookup"><span data-stu-id="d4f05-221">Create hello TestVNet4 gateway.</span></span> <span data-ttu-id="d4f05-222">建立閘道可以通常要花費 45 分鐘以上，視 hello 選取的閘道 SKU。</span><span class="sxs-lookup"><span data-stu-id="d4f05-222">Creating a gateway can often take 45 minutes or more, depending on hello selected gateway SKU.</span></span>

  ```powershell
  New-AzureRmVirtualNetworkGateway -Name $GWName4 -ResourceGroupName $RG4 `
  -Location $Location4 -IpConfigurations $gwipconf4 -GatewayType Vpn `
  -VpnType RouteBased -GatewaySku VpnGw1
  ```

### <a name="step-4---create-hello-connections"></a><span data-ttu-id="d4f05-223">步驟 4-建立 hello 連線</span><span class="sxs-lookup"><span data-stu-id="d4f05-223">Step 4 - Create hello connections</span></span>

1. <span data-ttu-id="d4f05-224">取得這兩個虛擬網路閘道。</span><span class="sxs-lookup"><span data-stu-id="d4f05-224">Get both virtual network gateways.</span></span> <span data-ttu-id="d4f05-225">如果 hello 閘道 hello 中都相同的訂用帳戶，和它們在 hello 範例中，您可以完成此步驟在 hello 同一個 PowerShell 工作階段。</span><span class="sxs-lookup"><span data-stu-id="d4f05-225">If both of hello gateways are in hello same subscription, as they are in hello example, you can complete this step in hello same PowerShell session.</span></span>

  ```powershell
  $vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
  $vnet4gw = Get-AzureRmVirtualNetworkGateway -Name $GWName4 -ResourceGroupName $RG4
  ```
2. <span data-ttu-id="d4f05-226">建立 hello TestVNet1 tooTestVNet4 連線。</span><span class="sxs-lookup"><span data-stu-id="d4f05-226">Create hello TestVNet1 tooTestVNet4 connection.</span></span> <span data-ttu-id="d4f05-227">在此步驟中，您會從 TestVNet1 tooTestVNet4 建立 hello 連線。</span><span class="sxs-lookup"><span data-stu-id="d4f05-227">In this step, you create hello connection from TestVNet1 tooTestVNet4.</span></span> <span data-ttu-id="d4f05-228">您會看見 hello 範例中所參考的共用的金鑰。</span><span class="sxs-lookup"><span data-stu-id="d4f05-228">You'll see a shared key referenced in hello examples.</span></span> <span data-ttu-id="d4f05-229">您可以使用您自己的值為 hello 共用金鑰。</span><span class="sxs-lookup"><span data-stu-id="d4f05-229">You can use your own values for hello shared key.</span></span> <span data-ttu-id="d4f05-230">hello 很重要的是該 hello 共用的金鑰必須符合這兩個連接。</span><span class="sxs-lookup"><span data-stu-id="d4f05-230">hello important thing is that hello shared key must match for both connections.</span></span> <span data-ttu-id="d4f05-231">建立連接，可能會同時 toocomplete 短。</span><span class="sxs-lookup"><span data-stu-id="d4f05-231">Creating a connection can take a short while toocomplete.</span></span>

  ```powershell
  New-AzureRmVirtualNetworkGatewayConnection -Name $Connection14 -ResourceGroupName $RG1 `
  -VirtualNetworkGateway1 $vnet1gw -VirtualNetworkGateway2 $vnet4gw -Location $Location1 `
  -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3'
  ```
3. <span data-ttu-id="d4f05-232">建立 hello TestVNet4 tooTestVNet1 連線。</span><span class="sxs-lookup"><span data-stu-id="d4f05-232">Create hello TestVNet4 tooTestVNet1 connection.</span></span> <span data-ttu-id="d4f05-233">除了您要建立 hello 連線從 TestVNet4 tooTestVNet1 類似 toohello 一個以上版本，則此步驟。</span><span class="sxs-lookup"><span data-stu-id="d4f05-233">This step is similar toohello one above, except you are creating hello connection from TestVNet4 tooTestVNet1.</span></span> <span data-ttu-id="d4f05-234">請確定 hello 共用金鑰相符。</span><span class="sxs-lookup"><span data-stu-id="d4f05-234">Make sure hello shared keys match.</span></span> <span data-ttu-id="d4f05-235">幾分鐘後，就會建立 hello 連線。</span><span class="sxs-lookup"><span data-stu-id="d4f05-235">hello connection will be established after a few minutes.</span></span>

  ```powershell
  New-AzureRmVirtualNetworkGatewayConnection -Name $Connection41 -ResourceGroupName $RG4 `
  -VirtualNetworkGateway1 $vnet4gw -VirtualNetworkGateway2 $vnet1gw -Location $Location4 `
  -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3'
  ```
4. <span data-ttu-id="d4f05-236">確認您的連線。</span><span class="sxs-lookup"><span data-stu-id="d4f05-236">Verify your connection.</span></span> <span data-ttu-id="d4f05-237">請參閱 hello 節[如何 tooverify 連線](#verify)。</span><span class="sxs-lookup"><span data-stu-id="d4f05-237">See hello section [How tooverify your connection](#verify).</span></span>

## <span data-ttu-id="d4f05-238"><a name="difsub"></a>如何 tooconnect Vnet 位於不同的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="d4f05-238"><a name="difsub"></a>How tooconnect VNets that are in different subscriptions</span></span>

![v2v 圖表](./media/vpn-gateway-vnet-vnet-rm-ps/v2vdiffsub.png)

<span data-ttu-id="d4f05-240">在此案例中，我們會連接 TestVNet1 和 TestVNet5。</span><span class="sxs-lookup"><span data-stu-id="d4f05-240">In this scenario, we connect TestVNet1 and TestVNet5.</span></span> <span data-ttu-id="d4f05-241">TestVNet1 和 TestVNet5 位於不同的訂用帳戶中。</span><span class="sxs-lookup"><span data-stu-id="d4f05-241">TestVNet1 and TestVNet5 reside in a different subscription.</span></span> <span data-ttu-id="d4f05-242">hello 訂用帳戶不需要與 hello 相關聯的 toobe 相同的 Active Directory 租用戶。</span><span class="sxs-lookup"><span data-stu-id="d4f05-242">hello subscriptions do not need toobe associated with hello same Active Directory tenant.</span></span> <span data-ttu-id="d4f05-243">這些步驟與 hello 先前設定的 hello 差異是部分 hello 組態步驟需要 toobe hello 第二個訂閱 hello 內容中的個別 PowerShell 工作階段中執行。</span><span class="sxs-lookup"><span data-stu-id="d4f05-243">hello difference between these steps and hello previous set is that some of hello configuration steps need toobe performed in a separate PowerShell session in hello context of hello second subscription.</span></span> <span data-ttu-id="d4f05-244">特別是當 hello 兩個訂用帳戶屬於 toodifferent 組織。</span><span class="sxs-lookup"><span data-stu-id="d4f05-244">Especially when hello two subscriptions belong toodifferent organizations.</span></span>

### <a name="step-5---create-and-configure-testvnet1"></a><span data-ttu-id="d4f05-245">步驟 5 - 建立及設定 TestVNet1</span><span class="sxs-lookup"><span data-stu-id="d4f05-245">Step 5 - Create and configure TestVNet1</span></span>

<span data-ttu-id="d4f05-246">您必須先完成[步驟 1](#Step1)和[步驟 2](#Step2) hello 先前從區段 toocreate 並設定 TestVNet1 hello TestVNet1 VPN 閘道。</span><span class="sxs-lookup"><span data-stu-id="d4f05-246">You must complete [Step 1](#Step1) and [Step 2](#Step2) from hello previous section toocreate and configure TestVNet1 and hello VPN Gateway for TestVNet1.</span></span> <span data-ttu-id="d4f05-247">此組態中，您不需要的 toocreate TestVNet4 hello 前一節，雖然如果您建立它，它不會衝突進行這些步驟。</span><span class="sxs-lookup"><span data-stu-id="d4f05-247">For this configuration, you are not required toocreate TestVNet4 from hello previous section, although if you do create it, it will not conflict with these steps.</span></span> <span data-ttu-id="d4f05-248">一旦您完成步驟 1 和步驟 2，繼續進行步驟 6 toocreate TestVNet5。</span><span class="sxs-lookup"><span data-stu-id="d4f05-248">Once you complete Step 1 and Step 2, continue with Step 6 toocreate TestVNet5.</span></span> 

### <a name="step-6---verify-hello-ip-address-ranges"></a><span data-ttu-id="d4f05-249">步驟 6-確認 hello IP 位址範圍</span><span class="sxs-lookup"><span data-stu-id="d4f05-249">Step 6 - Verify hello IP address ranges</span></span>

<span data-ttu-id="d4f05-250">它是重要 toomake 確定 hello 新的虛擬網路，TestVNet5，hello IP 位址空間不與任何 VNet 範圍或區域網路閘道的範圍重疊。</span><span class="sxs-lookup"><span data-stu-id="d4f05-250">It is important toomake sure that hello IP address space of hello new virtual network, TestVNet5, does not overlap with any of your VNet ranges or local network gateway ranges.</span></span> <span data-ttu-id="d4f05-251">在此範例中，hello 虛擬網路可能屬於 toodifferent 組織。</span><span class="sxs-lookup"><span data-stu-id="d4f05-251">In this example, hello virtual networks may belong toodifferent organizations.</span></span> <span data-ttu-id="d4f05-252">針對此練習，您可以使用下列值 hello TestVNet5 hello:</span><span class="sxs-lookup"><span data-stu-id="d4f05-252">For this exercise, you can use hello following values for hello TestVNet5:</span></span>

<span data-ttu-id="d4f05-253">**TestVNet5 的值︰**</span><span class="sxs-lookup"><span data-stu-id="d4f05-253">**Values for TestVNet5:**</span></span>

* <span data-ttu-id="d4f05-254">VNet 名稱︰TestVNet5</span><span class="sxs-lookup"><span data-stu-id="d4f05-254">VNet Name: TestVNet5</span></span>
* <span data-ttu-id="d4f05-255">資源群組：TestRG5</span><span class="sxs-lookup"><span data-stu-id="d4f05-255">Resource Group: TestRG5</span></span>
* <span data-ttu-id="d4f05-256">位置：日本東部</span><span class="sxs-lookup"><span data-stu-id="d4f05-256">Location: Japan East</span></span>
* <span data-ttu-id="d4f05-257">TestVNet5：10.51.0.0/16 和 10.52.0.0/16</span><span class="sxs-lookup"><span data-stu-id="d4f05-257">TestVNet5: 10.51.0.0/16 & 10.52.0.0/16</span></span>
* <span data-ttu-id="d4f05-258">FrontEnd：10.51.0.0/24</span><span class="sxs-lookup"><span data-stu-id="d4f05-258">FrontEnd: 10.51.0.0/24</span></span>
* <span data-ttu-id="d4f05-259">BackEnd：10.52.0.0/24</span><span class="sxs-lookup"><span data-stu-id="d4f05-259">BackEnd: 10.52.0.0/24</span></span>
* <span data-ttu-id="d4f05-260">GatewaySubnet：10.52.255.0.0/27</span><span class="sxs-lookup"><span data-stu-id="d4f05-260">GatewaySubnet: 10.52.255.0.0/27</span></span>
* <span data-ttu-id="d4f05-261">GatewayName：VNet5GW</span><span class="sxs-lookup"><span data-stu-id="d4f05-261">GatewayName: VNet5GW</span></span>
* <span data-ttu-id="d4f05-262">公用 IP：VNet5GWIP</span><span class="sxs-lookup"><span data-stu-id="d4f05-262">Public IP: VNet5GWIP</span></span>
* <span data-ttu-id="d4f05-263">VPNType：RouteBased</span><span class="sxs-lookup"><span data-stu-id="d4f05-263">VPNType: RouteBased</span></span>
* <span data-ttu-id="d4f05-264">連線︰VNet5toVNet1</span><span class="sxs-lookup"><span data-stu-id="d4f05-264">Connection: VNet5toVNet1</span></span>
* <span data-ttu-id="d4f05-265">ConnectionType：VNet2VNet</span><span class="sxs-lookup"><span data-stu-id="d4f05-265">ConnectionType: VNet2VNet</span></span>

### <a name="step-7---create-and-configure-testvnet5"></a><span data-ttu-id="d4f05-266">步驟 7 - 建立及設定 TestVNet5</span><span class="sxs-lookup"><span data-stu-id="d4f05-266">Step 7 - Create and configure TestVNet5</span></span>

<span data-ttu-id="d4f05-267">Hello hello 新訂用帳戶內容中，必須完成此步驟。</span><span class="sxs-lookup"><span data-stu-id="d4f05-267">This step must be done in hello context of hello new subscription.</span></span> <span data-ttu-id="d4f05-268">此組件可能會由擁有 hello 訂用帳戶的另一個組織中的 hello 系統管理員執行。</span><span class="sxs-lookup"><span data-stu-id="d4f05-268">This part may be performed by hello administrator in a different organization that owns hello subscription.</span></span>

1. <span data-ttu-id="d4f05-269">宣告變數。</span><span class="sxs-lookup"><span data-stu-id="d4f05-269">Declare your variables.</span></span> <span data-ttu-id="d4f05-270">為確定 tooreplace 以 hello 的 hello 值的 toouse 您的組態。</span><span class="sxs-lookup"><span data-stu-id="d4f05-270">Be sure tooreplace hello values with hello ones that you want toouse for your configuration.</span></span>

  ```powershell
  $Sub5 = "Replace_With_the_New_Subcription_Name"
  $RG5 = "TestRG5"
  $Location5 = "Japan East"
  $VnetName5 = "TestVNet5"
  $FESubName5 = "FrontEnd"
  $BESubName5 = "Backend"
  $GWSubName5 = "GatewaySubnet"
  $VnetPrefix51 = "10.51.0.0/16"
  $VnetPrefix52 = "10.52.0.0/16"
  $FESubPrefix5 = "10.51.0.0/24"
  $BESubPrefix5 = "10.52.0.0/24"
  $GWSubPrefix5 = "10.52.255.0/27"
  $GWName5 = "VNet5GW"
  $GWIPName5 = "VNet5GWIP"
  $GWIPconfName5 = "gwipconf5"
  $Connection51 = "VNet5toVNet1"
  ```
2. <span data-ttu-id="d4f05-271">連接 toosubscription 5。</span><span class="sxs-lookup"><span data-stu-id="d4f05-271">Connect toosubscription 5.</span></span> <span data-ttu-id="d4f05-272">開啟 PowerShell 主控台並連接 tooyour 帳戶。</span><span class="sxs-lookup"><span data-stu-id="d4f05-272">Open your PowerShell console and connect tooyour account.</span></span> <span data-ttu-id="d4f05-273">使用下列範例 toohelp 您連接的 hello:</span><span class="sxs-lookup"><span data-stu-id="d4f05-273">Use hello following sample toohelp you connect:</span></span>

  ```powershell
  Login-AzureRmAccount
  ```

  <span data-ttu-id="d4f05-274">請檢查 hello hello 帳戶的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="d4f05-274">Check hello subscriptions for hello account.</span></span>

  ```powershell
  Get-AzureRmSubscription
  ```

  <span data-ttu-id="d4f05-275">指定您想 toouse hello 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="d4f05-275">Specify hello subscription that you want toouse.</span></span>

  ```powershell
  Select-AzureRmSubscription -SubscriptionName $Sub5
  ```
3. <span data-ttu-id="d4f05-276">建立新的資源群組。</span><span class="sxs-lookup"><span data-stu-id="d4f05-276">Create a new resource group.</span></span>

  ```powershell
  New-AzureRmResourceGroup -Name $RG5 -Location $Location5
  ```
4. <span data-ttu-id="d4f05-277">建立 hello TestVNet5 的子網路組態。</span><span class="sxs-lookup"><span data-stu-id="d4f05-277">Create hello subnet configurations for TestVNet5.</span></span>

  ```powershell
  $fesub5 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName5 -AddressPrefix $FESubPrefix5
  $besub5 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName5 -AddressPrefix $BESubPrefix5
  $gwsub5 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName5 -AddressPrefix $GWSubPrefix5
  ```
5. <span data-ttu-id="d4f05-278">建立 TestVNet5。</span><span class="sxs-lookup"><span data-stu-id="d4f05-278">Create TestVNet5.</span></span>

  ```powershell
  New-AzureRmVirtualNetwork -Name $VnetName5 -ResourceGroupName $RG5 -Location $Location5 `
  -AddressPrefix $VnetPrefix51,$VnetPrefix52 -Subnet $fesub5,$besub5,$gwsub5
  ```
6. <span data-ttu-id="d4f05-279">要求公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="d4f05-279">Request a public IP address.</span></span>

  ```powershell
  $gwpip5 = New-AzureRmPublicIpAddress -Name $GWIPName5 -ResourceGroupName $RG5 `
  -Location $Location5 -AllocationMethod Dynamic
  ```
7. <span data-ttu-id="d4f05-280">建立 hello 閘道設定。</span><span class="sxs-lookup"><span data-stu-id="d4f05-280">Create hello gateway configuration.</span></span>

  ```powershell
  $vnet5 = Get-AzureRmVirtualNetwork -Name $VnetName5 -ResourceGroupName $RG5
  $subnet5  = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet5
  $gwipconf5 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName5 -Subnet $subnet5 -PublicIpAddress $gwpip5
  ```
8. <span data-ttu-id="d4f05-281">建立 hello TestVNet5 閘道。</span><span class="sxs-lookup"><span data-stu-id="d4f05-281">Create hello TestVNet5 gateway.</span></span>

  ```powershell
  New-AzureRmVirtualNetworkGateway -Name $GWName5 -ResourceGroupName $RG5 -Location $Location5 `
  -IpConfigurations $gwipconf5 -GatewayType Vpn -VpnType RouteBased -GatewaySku VpnGw1
  ```

### <a name="step-8---create-hello-connections"></a><span data-ttu-id="d4f05-282">步驟 8-建立 hello 連線</span><span class="sxs-lookup"><span data-stu-id="d4f05-282">Step 8 - Create hello connections</span></span>

<span data-ttu-id="d4f05-283">在此範例中，因為 hello 閘道在 hello 不同訂用帳戶，我們已分割此步驟中兩個 PowerShell 工作階段標示為 [訂用帳戶 1] 和 [訂用帳戶 5]。</span><span class="sxs-lookup"><span data-stu-id="d4f05-283">In this example, because hello gateways are in hello different subscriptions, we've split this step into two PowerShell sessions marked as [Subscription 1] and [Subscription 5].</span></span>

1. <span data-ttu-id="d4f05-284">**[訂用帳戶 1]**訂用帳戶 1 的 get hello 虛擬網路閘道。</span><span class="sxs-lookup"><span data-stu-id="d4f05-284">**[Subscription 1]** Get hello virtual network gateway for Subscription 1.</span></span> <span data-ttu-id="d4f05-285">登入，然後再執行下列範例中的 hello 連接 tooSubscription 1:</span><span class="sxs-lookup"><span data-stu-id="d4f05-285">Log in and connect tooSubscription 1 before running hello following example:</span></span>

  ```powershell
  $vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
  ```

  <span data-ttu-id="d4f05-286">複製下列項目 hello hello 輸出，並傳送訂用帳戶 5 這些 toohello 系統管理員，透過電子郵件或其他方法。</span><span class="sxs-lookup"><span data-stu-id="d4f05-286">Copy hello output of hello following elements and send these toohello administrator of Subscription 5 via email or another method.</span></span>

  ```powershell
  $vnet1gw.Name
  $vnet1gw.Id
  ```

  <span data-ttu-id="d4f05-287">這兩個元素會有值類似 toohello 下列範例輸出：</span><span class="sxs-lookup"><span data-stu-id="d4f05-287">These two elements will have values similar toohello following example output:</span></span>

  ```
  PS D:\> $vnet1gw.Name
  VNet1GW
  PS D:\> $vnet1gw.Id
  /subscriptions/b636ca99-6f88-4df4-a7c3-2f8dc4545509/resourceGroupsTestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW
  ```
2. <span data-ttu-id="d4f05-288">**[訂用帳戶 5]**訂用帳戶 5 get hello 虛擬網路閘道。</span><span class="sxs-lookup"><span data-stu-id="d4f05-288">**[Subscription 5]** Get hello virtual network gateway for Subscription 5.</span></span> <span data-ttu-id="d4f05-289">登入，然後再執行下列範例中的 hello 連接 tooSubscription 5:</span><span class="sxs-lookup"><span data-stu-id="d4f05-289">Log in and connect tooSubscription 5 before running hello following example:</span></span>

  ```powershell
  $vnet5gw = Get-AzureRmVirtualNetworkGateway -Name $GWName5 -ResourceGroupName $RG5
  ```

  <span data-ttu-id="d4f05-290">複製下列項目 hello hello 輸出，並傳送訂用帳戶 1 這些 toohello 系統管理員，透過電子郵件或其他方法。</span><span class="sxs-lookup"><span data-stu-id="d4f05-290">Copy hello output of hello following elements and send these toohello administrator of Subscription 1 via email or another method.</span></span>

  ```powershell
  $vnet5gw.Name
  $vnet5gw.Id
  ```

  <span data-ttu-id="d4f05-291">這兩個元素會有值類似 toohello 下列範例輸出：</span><span class="sxs-lookup"><span data-stu-id="d4f05-291">These two elements will have values similar toohello following example output:</span></span>

  ```
  PS C:\> $vnet5gw.Name
  VNet5GW
  PS C:\> $vnet5gw.Id
  /subscriptions/66c8e4f1-ecd6-47ed-9de7-7e530de23994/resourceGroups/TestRG5/providers/Microsoft.Network/virtualNetworkGateways/VNet5GW
  ```
3. <span data-ttu-id="d4f05-292">**[訂用帳戶 1]**建立 hello TestVNet1 tooTestVNet5 連線。</span><span class="sxs-lookup"><span data-stu-id="d4f05-292">**[Subscription 1]** Create hello TestVNet1 tooTestVNet5 connection.</span></span> <span data-ttu-id="d4f05-293">在此步驟中，您會從 TestVNet1 tooTestVNet5 建立 hello 連線。</span><span class="sxs-lookup"><span data-stu-id="d4f05-293">In this step, you create hello connection from TestVNet1 tooTestVNet5.</span></span> <span data-ttu-id="d4f05-294">這裡的 hello 差異是因為它是不同的訂用帳戶中的 $vnet5gw 也無法直接取得。</span><span class="sxs-lookup"><span data-stu-id="d4f05-294">hello difference here is that $vnet5gw cannot be obtained directly because it is in a different subscription.</span></span> <span data-ttu-id="d4f05-295">您將需要 toocreate 新的 PowerShell 物件的 hello hello 前面步驟中，用以表示從訂用帳戶 1 的值。</span><span class="sxs-lookup"><span data-stu-id="d4f05-295">You will need toocreate a new PowerShell object with hello values communicated from Subscription 1 in hello steps above.</span></span> <span data-ttu-id="d4f05-296">使用下列的 hello 範例。</span><span class="sxs-lookup"><span data-stu-id="d4f05-296">Use hello example below.</span></span> <span data-ttu-id="d4f05-297">取代您自己的值為 hello 名稱、 識別碼和共用的金鑰。</span><span class="sxs-lookup"><span data-stu-id="d4f05-297">Replace hello Name, Id, and shared key with your own values.</span></span> <span data-ttu-id="d4f05-298">hello 很重要的是該 hello 共用的金鑰必須符合這兩個連接。</span><span class="sxs-lookup"><span data-stu-id="d4f05-298">hello important thing is that hello shared key must match for both connections.</span></span> <span data-ttu-id="d4f05-299">建立連接，可能會同時 toocomplete 短。</span><span class="sxs-lookup"><span data-stu-id="d4f05-299">Creating a connection can take a short while toocomplete.</span></span>

  <span data-ttu-id="d4f05-300">連接 tooSubscription 1，才能執行下列範例中的 hello:</span><span class="sxs-lookup"><span data-stu-id="d4f05-300">Connect tooSubscription 1 before running hello following example:</span></span>

  ```powershell
  $vnet5gw = New-Object Microsoft.Azure.Commands.Network.Models.PSVirtualNetworkGateway
  $vnet5gw.Name = "VNet5GW"
  $vnet5gw.Id   = "/subscriptions/66c8e4f1-ecd6-47ed-9de7-7e530de23994/resourceGroups/TestRG5/providers/Microsoft.Network/virtualNetworkGateways/VNet5GW"
  $Connection15 = "VNet1toVNet5"
  New-AzureRmVirtualNetworkGatewayConnection -Name $Connection15 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -VirtualNetworkGateway2 $vnet5gw -Location $Location1 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3'
  ```
4. <span data-ttu-id="d4f05-301">**[訂用帳戶 5]**建立 hello TestVNet5 tooTestVNet1 連線。</span><span class="sxs-lookup"><span data-stu-id="d4f05-301">**[Subscription 5]** Create hello TestVNet5 tooTestVNet1 connection.</span></span> <span data-ttu-id="d4f05-302">除了您要建立 hello 連線從 TestVNet5 tooTestVNet1 類似 toohello 一個以上版本，則此步驟。</span><span class="sxs-lookup"><span data-stu-id="d4f05-302">This step is similar toohello one above, except you are creating hello connection from TestVNet5 tooTestVNet1.</span></span> <span data-ttu-id="d4f05-303">建立根據 hello 值取自訂用帳戶 1 的 PowerShell 物件的相同程序也適用於此處也 hello。</span><span class="sxs-lookup"><span data-stu-id="d4f05-303">hello same process of creating a PowerShell object based on hello values obtained from Subscription 1 applies here as well.</span></span> <span data-ttu-id="d4f05-304">在此步驟中，請確定 hello 共用索引鍵的符合。</span><span class="sxs-lookup"><span data-stu-id="d4f05-304">In this step, be sure that hello shared keys match.</span></span>

  <span data-ttu-id="d4f05-305">連接 tooSubscription 5，才能執行下列範例中的 hello:</span><span class="sxs-lookup"><span data-stu-id="d4f05-305">Connect tooSubscription 5 before running hello following example:</span></span>

  ```powershell
  $vnet1gw = New-Object Microsoft.Azure.Commands.Network.Models.PSVirtualNetworkGateway
  $vnet1gw.Name = "VNet1GW"
  $vnet1gw.Id = "/subscriptions/b636ca99-6f88-4df4-a7c3-2f8dc4545509/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW "
  New-AzureRmVirtualNetworkGatewayConnection -Name $Connection51 -ResourceGroupName $RG5 -VirtualNetworkGateway1 $vnet5gw -VirtualNetworkGateway2 $vnet1gw -Location $Location5 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3'
  ```

## <span data-ttu-id="d4f05-306"><a name="verify"></a>如何 tooverify 連接</span><span class="sxs-lookup"><span data-stu-id="d4f05-306"><a name="verify"></a>How tooverify a connection</span></span>

[!INCLUDE [vpn-gateway-no-nsg-include](../../includes/vpn-gateway-no-nsg-include.md)]

[!INCLUDE [verify connections powershell](../../includes/vpn-gateway-verify-connection-ps-rm-include.md)]

## <span data-ttu-id="d4f05-307"><a name="faq"></a>VNet 對 VNet 常見問題集</span><span class="sxs-lookup"><span data-stu-id="d4f05-307"><a name="faq"></a>VNet-to-VNet FAQ</span></span>

[!INCLUDE [vpn-gateway-vnet-vnet-faq](../../includes/vpn-gateway-vnet-vnet-faq-include.md)]

## <a name="next-steps"></a><span data-ttu-id="d4f05-308">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d4f05-308">Next steps</span></span>

* <span data-ttu-id="d4f05-309">一旦完成您的連線，您可以將虛擬機器 tooyour 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="d4f05-309">Once your connection is complete, you can add virtual machines tooyour virtual networks.</span></span> <span data-ttu-id="d4f05-310">請參閱 hello[虛擬機器文件](https://docs.microsoft.com/azure/#pivot=services&panel=Compute)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="d4f05-310">See hello [Virtual Machines documentation](https://docs.microsoft.com/azure/#pivot=services&panel=Compute) for more information.</span></span>
* <span data-ttu-id="d4f05-311">BGP 的相關資訊，請參閱 hello [BGP 概觀](vpn-gateway-bgp-overview.md)和[如何 tooconfigure BGP](vpn-gateway-bgp-resource-manager-ps.md)。</span><span class="sxs-lookup"><span data-stu-id="d4f05-311">For information about BGP, see hello [BGP Overview](vpn-gateway-bgp-overview.md) and [How tooconfigure BGP](vpn-gateway-bgp-resource-manager-ps.md).</span></span>
