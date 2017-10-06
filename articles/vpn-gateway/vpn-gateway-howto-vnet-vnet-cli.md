---
title: "連接虛擬網路 tooanother VNet: Azure CLI |Microsoft 文件"
description: "本文將逐步引導您使用 Azure Resource Manager 和 Azure CLI，將虛擬網路連線在一起。"
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
ms.openlocfilehash: 70113914bcae03c80f9ad133ff081d1cf37fc309
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-vnet-to-vnet-vpn-gateway-connection-using-azure-cli"></a><span data-ttu-id="07621-103">使用 Azure CLI 設定 VNet 對 VNet 的 VPN 閘道連線</span><span class="sxs-lookup"><span data-stu-id="07621-103">Configure a VNet-to-VNet VPN gateway connection using Azure CLI</span></span>

<span data-ttu-id="07621-104">本文章將示範如何 toocreate 虛擬網路之間的 VPN 閘道連線。</span><span class="sxs-lookup"><span data-stu-id="07621-104">This article shows you how toocreate a VPN gateway connection between virtual networks.</span></span> <span data-ttu-id="07621-105">hello 虛擬網路可在 hello 相同或不同區域，並從 hello 相同或不同的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="07621-105">hello virtual networks can be in hello same or different regions, and from hello same or different subscriptions.</span></span> <span data-ttu-id="07621-106">當連接的 Vnet，從不同的訂用帳戶，hello 訂用帳戶不需要與相關聯的 toobe hello 相同的 Active Directory 租用戶。</span><span class="sxs-lookup"><span data-stu-id="07621-106">When connecting VNets from different subscriptions, hello subscriptions do not need toobe associated with hello same Active Directory tenant.</span></span> 

<span data-ttu-id="07621-107">這篇文章中的 hello 步驟套用 toohello Resource Manager 部署模型，並使用 Azure CLI。</span><span class="sxs-lookup"><span data-stu-id="07621-107">hello steps in this article apply toohello Resource Manager deployment model and use Azure CLI.</span></span> <span data-ttu-id="07621-108">您也可以建立此組態使用不同的部署工具或部署模型，從下列清單中的 hello 選取不同的選項：</span><span class="sxs-lookup"><span data-stu-id="07621-108">You can also create this configuration using a different deployment tool or deployment model by selecting a different option from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="07621-109">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="07621-109">Azure portal</span></span>](vpn-gateway-howto-vnet-vnet-resource-manager-portal.md)
> * [<span data-ttu-id="07621-110">PowerShell</span><span class="sxs-lookup"><span data-stu-id="07621-110">PowerShell</span></span>](vpn-gateway-vnet-vnet-rm-ps.md)
> * [<span data-ttu-id="07621-111">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="07621-111">Azure CLI</span></span>](vpn-gateway-howto-vnet-vnet-cli.md)
> * [<span data-ttu-id="07621-112">Azure 入口網站 (傳統)</span><span class="sxs-lookup"><span data-stu-id="07621-112">Azure portal (classic)</span></span>](vpn-gateway-howto-vnet-vnet-portal-classic.md)
> * [<span data-ttu-id="07621-113">連線不同的部署模型 - Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="07621-113">Connect different deployment models - Azure portal</span></span>](vpn-gateway-connect-different-deployment-models-portal.md)
> * [<span data-ttu-id="07621-114">連線不同的部署模型 - PowerShell</span><span class="sxs-lookup"><span data-stu-id="07621-114">Connect different deployment models - PowerShell</span></span>](vpn-gateway-connect-different-deployment-models-powershell.md)
>
>

<span data-ttu-id="07621-115">連接虛擬網路 tooanother 虛擬網路 (VNet 對 VNet) 是類似 tooconnecting VNet tooan 在內部部署站台位置。</span><span class="sxs-lookup"><span data-stu-id="07621-115">Connecting a virtual network tooanother virtual network (VNet-to-VNet) is similar tooconnecting a VNet tooan on-premises site location.</span></span> <span data-ttu-id="07621-116">這兩種連線類型使用的 VPN 閘道 tooprovide 採用 IPsec/IKE 的安全通道。</span><span class="sxs-lookup"><span data-stu-id="07621-116">Both connectivity types use a VPN gateway tooprovide a secure tunnel using IPsec/IKE.</span></span> <span data-ttu-id="07621-117">如果您的 Vnet hello 中相同的區域，您可能會想 tooconsider 它們使用對等互連的 VNet 連接。</span><span class="sxs-lookup"><span data-stu-id="07621-117">If your VNets are in hello same region, you may want tooconsider connecting them using VNet Peering.</span></span> <span data-ttu-id="07621-118">VNet 對等互連不會使用 VPN 閘道。</span><span class="sxs-lookup"><span data-stu-id="07621-118">VNet peering does not use a VPN gateway.</span></span> <span data-ttu-id="07621-119">如需詳細資訊，請參閱 [VNet 對等互連](../virtual-network/virtual-network-peering-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="07621-119">For more information, see [VNet peering](../virtual-network/virtual-network-peering-overview.md).</span></span>

<span data-ttu-id="07621-120">您可以將 VNet 對 VNet 通訊與多站台組態結合。</span><span class="sxs-lookup"><span data-stu-id="07621-120">VNet-to-VNet communication can be combined with multi-site configurations.</span></span> <span data-ttu-id="07621-121">這可讓您建立結合內部虛擬網路連線使用跨單位連線的網路拓樸 hello 下列圖表所示：</span><span class="sxs-lookup"><span data-stu-id="07621-121">This lets you establish network topologies that combine cross-premises connectivity with inter-virtual network connectivity, as shown in hello following diagram:</span></span>

![關於連線](./media/vpn-gateway-howto-vnet-vnet-cli/aboutconnections.png)

### <span data-ttu-id="07621-123"><a name="why"></a>為什麼要連線虛擬網路？</span><span class="sxs-lookup"><span data-stu-id="07621-123"><a name="why"></a>Why connect virtual networks?</span></span>

<span data-ttu-id="07621-124">您可以遵循原因 hello tooconnect 虛擬網路：</span><span class="sxs-lookup"><span data-stu-id="07621-124">You may want tooconnect virtual networks for hello following reasons:</span></span>

* <span data-ttu-id="07621-125">**跨區域的異地備援和異地目前狀態**</span><span class="sxs-lookup"><span data-stu-id="07621-125">**Cross region geo-redundancy and geo-presence**</span></span>

  * <span data-ttu-id="07621-126">您可以使用安全連線設定自己的異地複寫或同步處理，而不用查看網際網路對向端點。</span><span class="sxs-lookup"><span data-stu-id="07621-126">You can set up your own geo-replication or synchronization with secure connectivity without going over Internet-facing endpoints.</span></span>
  * <span data-ttu-id="07621-127">您可以使用 Azure 流量管理員和負載平衡器，利用異地備援跨多個 Azure 區域設定高度可用的工作負載。</span><span class="sxs-lookup"><span data-stu-id="07621-127">With Azure Traffic Manager and Load Balancer, you can set up highly available workload with geo-redundancy across multiple Azure regions.</span></span> <span data-ttu-id="07621-128">重要的一個例子是 tooset 設定 SQL Always On 與分配到多個 Azure 區域的可用性群組。</span><span class="sxs-lookup"><span data-stu-id="07621-128">One important example is tooset up SQL Always On with Availability Groups spreading across multiple Azure regions.</span></span>
* <span data-ttu-id="07621-129">**具有隔離或管理界限的區域性多層式應用程式**</span><span class="sxs-lookup"><span data-stu-id="07621-129">**Regional multi-tier applications with isolation or administrative boundary**</span></span>

  * <span data-ttu-id="07621-130">在 hello 相同區域中，您可以設定多層應用程式與多個虛擬網路連接在一起，因為 tooisolation 或系統管理需求。</span><span class="sxs-lookup"><span data-stu-id="07621-130">Within hello same region, you can set up multi-tier applications with multiple virtual networks connected together due tooisolation or administrative requirements.</span></span>

<span data-ttu-id="07621-131">如需 VNet 對 VNet 連線的詳細資訊，請參閱 hello [VNet 對 VNet 常見問題集](#faq)hello 本文結尾處。</span><span class="sxs-lookup"><span data-stu-id="07621-131">For more information about VNet-to-VNet connections, see hello [VNet-to-VNet FAQ](#faq) at hello end of this article.</span></span>

### <a name="which-set-of-steps-should-i-use"></a><span data-ttu-id="07621-132">我應該使用哪個步驟集？</span><span class="sxs-lookup"><span data-stu-id="07621-132">Which set of steps should I use?</span></span>

<span data-ttu-id="07621-133">在本文中，您會看到兩組不同的步驟。</span><span class="sxs-lookup"><span data-stu-id="07621-133">In this article, you see two different sets of steps.</span></span> <span data-ttu-id="07621-134">一組步驟[Vnet 中的 hello 相同訂用帳戶](#samesub)，而另一個用於[位於不同的訂用帳戶中的 Vnet](#difsub)。</span><span class="sxs-lookup"><span data-stu-id="07621-134">One set of steps for [VNets that reside in hello same subscription](#samesub), and another for [VNets that reside in different subscriptions](#difsub).</span></span>

## <span data-ttu-id="07621-135"><a name="samesub"></a>連線 Vnet 中 hello 相同訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="07621-135"><a name="samesub"></a>Connect VNets that are in hello same subscription</span></span>

![v2v 圖表](./media/vpn-gateway-howto-vnet-vnet-cli/v2vrmps.png)

### <a name="before-you-begin"></a><span data-ttu-id="07621-137">開始之前</span><span class="sxs-lookup"><span data-stu-id="07621-137">Before you begin</span></span>

<span data-ttu-id="07621-138">在開始之前，安裝 hello 最新版本 （2.0 或更新版本） 的 hello CLI 命令。</span><span class="sxs-lookup"><span data-stu-id="07621-138">Before beginning, install hello latest version of hello CLI commands (2.0 or later).</span></span> <span data-ttu-id="07621-139">如需安裝 hello CLI 命令的資訊，請參閱[安裝 Azure CLI 2.0](/cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="07621-139">For information about installing hello CLI commands, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli).</span></span>

### <span data-ttu-id="07621-140"><a name="Plan"></a>規劃 IP 位址範圍</span><span class="sxs-lookup"><span data-stu-id="07621-140"><a name="Plan"></a>Plan your IP address ranges</span></span>

<span data-ttu-id="07621-141">在 hello 下列步驟，我們會建立兩個虛擬網路，以及其個別的閘道子網路和設定。</span><span class="sxs-lookup"><span data-stu-id="07621-141">In hello following steps, we create two virtual networks along with their respective gateway subnets and configurations.</span></span> <span data-ttu-id="07621-142">我們再建立 hello 之間的 VPN 連線兩個 Vnet。</span><span class="sxs-lookup"><span data-stu-id="07621-142">We then create a VPN connection between hello two VNets.</span></span> <span data-ttu-id="07621-143">它是您的網路設定的重要 tooplan hello IP 位址範圍。</span><span class="sxs-lookup"><span data-stu-id="07621-143">It’s important tooplan hello IP address ranges for your network configuration.</span></span> <span data-ttu-id="07621-144">請記住，您必須先確定您的 VNet 範圍或區域網路範圍沒有以任何方式重疊。</span><span class="sxs-lookup"><span data-stu-id="07621-144">Keep in mind that you must make sure that none of your VNet ranges or local network ranges overlap in any way.</span></span> <span data-ttu-id="07621-145">在這些範例中，我們不會包含 DNS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="07621-145">In these examples, we do not include a DNS server.</span></span> <span data-ttu-id="07621-146">如果您想要了解虛擬網路的名稱解析，請參閱[名稱解析](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md)。</span><span class="sxs-lookup"><span data-stu-id="07621-146">If you want name resolution for your virtual networks, see [Name resolution](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).</span></span>

<span data-ttu-id="07621-147">我們使用下列值 hello 範例中的 hello:</span><span class="sxs-lookup"><span data-stu-id="07621-147">We use hello following values in hello examples:</span></span>

<span data-ttu-id="07621-148">**TestVNet1 的值︰**</span><span class="sxs-lookup"><span data-stu-id="07621-148">**Values for TestVNet1:**</span></span>

* <span data-ttu-id="07621-149">VNet 名稱︰TestVNet1</span><span class="sxs-lookup"><span data-stu-id="07621-149">VNet Name: TestVNet1</span></span>
* <span data-ttu-id="07621-150">資源群組︰TestRG1</span><span class="sxs-lookup"><span data-stu-id="07621-150">Resource Group: TestRG1</span></span>
* <span data-ttu-id="07621-151">位置：美國東部</span><span class="sxs-lookup"><span data-stu-id="07621-151">Location: East US</span></span>
* <span data-ttu-id="07621-152">TestVNet1：10.11.0.0/16 和 10.12.0.0/16</span><span class="sxs-lookup"><span data-stu-id="07621-152">TestVNet1: 10.11.0.0/16 & 10.12.0.0/16</span></span>
* <span data-ttu-id="07621-153">FrontEnd：10.11.0.0/24</span><span class="sxs-lookup"><span data-stu-id="07621-153">FrontEnd: 10.11.0.0/24</span></span>
* <span data-ttu-id="07621-154">BackEnd：10.12.0.0/24</span><span class="sxs-lookup"><span data-stu-id="07621-154">BackEnd: 10.12.0.0/24</span></span>
* <span data-ttu-id="07621-155">GatewaySubnet：10.12.255.0/27</span><span class="sxs-lookup"><span data-stu-id="07621-155">GatewaySubnet: 10.12.255.0/27</span></span>
* <span data-ttu-id="07621-156">GatewayName：VNet1GW</span><span class="sxs-lookup"><span data-stu-id="07621-156">GatewayName: VNet1GW</span></span>
* <span data-ttu-id="07621-157">公用 IP: VNet1GWIP</span><span class="sxs-lookup"><span data-stu-id="07621-157">Public IP: VNet1GWIP</span></span>
* <span data-ttu-id="07621-158">VPNType：RouteBased</span><span class="sxs-lookup"><span data-stu-id="07621-158">VPNType: RouteBased</span></span>
* <span data-ttu-id="07621-159">Connection(1to4)：VNet1toVNet4</span><span class="sxs-lookup"><span data-stu-id="07621-159">Connection(1to4): VNet1toVNet4</span></span>
* <span data-ttu-id="07621-160">Connection(1to5)：VNet1toVNet5</span><span class="sxs-lookup"><span data-stu-id="07621-160">Connection(1to5): VNet1toVNet5</span></span>
* <span data-ttu-id="07621-161">ConnectionType：VNet2VNet</span><span class="sxs-lookup"><span data-stu-id="07621-161">ConnectionType: VNet2VNet</span></span>

<span data-ttu-id="07621-162">**TestVNet4 的值︰**</span><span class="sxs-lookup"><span data-stu-id="07621-162">**Values for TestVNet4:**</span></span>

* <span data-ttu-id="07621-163">VNet 名稱︰TestVNet4</span><span class="sxs-lookup"><span data-stu-id="07621-163">VNet Name: TestVNet4</span></span>
* <span data-ttu-id="07621-164">TestVNet2：10.41.0.0/16 和 10.42.0.0/16</span><span class="sxs-lookup"><span data-stu-id="07621-164">TestVNet2: 10.41.0.0/16 & 10.42.0.0/16</span></span>
* <span data-ttu-id="07621-165">FrontEnd：10.41.0.0/24</span><span class="sxs-lookup"><span data-stu-id="07621-165">FrontEnd: 10.41.0.0/24</span></span>
* <span data-ttu-id="07621-166">BackEnd：10.42.0.0/24</span><span class="sxs-lookup"><span data-stu-id="07621-166">BackEnd: 10.42.0.0/24</span></span>
* <span data-ttu-id="07621-167">GatewaySubnet：10.42.255.0/27</span><span class="sxs-lookup"><span data-stu-id="07621-167">GatewaySubnet: 10.42.255.0/27</span></span>
* <span data-ttu-id="07621-168">資源群組：TestRG4</span><span class="sxs-lookup"><span data-stu-id="07621-168">Resource Group: TestRG4</span></span>
* <span data-ttu-id="07621-169">位置：美國西部</span><span class="sxs-lookup"><span data-stu-id="07621-169">Location: West US</span></span>
* <span data-ttu-id="07621-170">GatewayName：VNet4GW</span><span class="sxs-lookup"><span data-stu-id="07621-170">GatewayName: VNet4GW</span></span>
* <span data-ttu-id="07621-171">公用 IP：VNet4GWIP</span><span class="sxs-lookup"><span data-stu-id="07621-171">Public IP: VNet4GWIP</span></span>
* <span data-ttu-id="07621-172">VPNType：RouteBased</span><span class="sxs-lookup"><span data-stu-id="07621-172">VPNType: RouteBased</span></span>
* <span data-ttu-id="07621-173">連線︰VNet4toVNet1</span><span class="sxs-lookup"><span data-stu-id="07621-173">Connection: VNet4toVNet1</span></span>
* <span data-ttu-id="07621-174">ConnectionType：VNet2VNet</span><span class="sxs-lookup"><span data-stu-id="07621-174">ConnectionType: VNet2VNet</span></span>


### <span data-ttu-id="07621-175"><a name="Connect"></a>步驟 1-連接 tooyour 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="07621-175"><a name="Connect"></a>Step 1 - Connect tooyour subscription</span></span>

[!INCLUDE [CLI login](../../includes/vpn-gateway-cli-login-numbers-include.md)]

### <span data-ttu-id="07621-176"><a name="TestVNet1"></a>步驟 2 - 建立及設定 TestVNet1</span><span class="sxs-lookup"><span data-stu-id="07621-176"><a name="TestVNet1"></a>Step 2 - Create and configure TestVNet1</span></span>

1. <span data-ttu-id="07621-177">建立資源群組。</span><span class="sxs-lookup"><span data-stu-id="07621-177">Create a resource group.</span></span>

  ```azurecli
  az group create -n TestRG1  -l eastus
  ```
2. <span data-ttu-id="07621-178">建立 TestVNet1 TestVNet1 和 hello 子網路。</span><span class="sxs-lookup"><span data-stu-id="07621-178">Create TestVNet1 and hello subnets for TestVNet1.</span></span> <span data-ttu-id="07621-179">此範例會建立名為 TestVNet1 的虛擬網路和名為 FrontEnd 的子網路。</span><span class="sxs-lookup"><span data-stu-id="07621-179">This example creates a virtual network named TestVNet1 and a subnet named FrontEnd.</span></span>

  ```azurecli
  az network vnet create -n TestVNet1 -g TestRG1 --address-prefix 10.11.0.0/16 -l eastus --subnet-name FrontEnd --subnet-prefix 10.11.0.0/24
  ```
3. <span data-ttu-id="07621-180">建立 hello 後端子網路的其他位址空間。</span><span class="sxs-lookup"><span data-stu-id="07621-180">Create an additional address space for hello backend subnet.</span></span> <span data-ttu-id="07621-181">請注意，在此步驟中，我們指定我們稍早建立這兩個 hello 位址空間 hello 我們想要 tooadd 其他位址空間。</span><span class="sxs-lookup"><span data-stu-id="07621-181">Notice that in this step, we specify both hello address space that we created earlier, and hello additional address space that we want tooadd.</span></span> <span data-ttu-id="07621-182">這是因為 hello [az 網路 vnet 更新](https://docs.microsoft.com/cli/azure/network/vnet#update)命令會覆寫 hello 先前的設定。</span><span class="sxs-lookup"><span data-stu-id="07621-182">This is because hello [az network vnet update](https://docs.microsoft.com/cli/azure/network/vnet#update) command overwrites hello previous settings.</span></span> <span data-ttu-id="07621-183">請確定 toospecify hello 位址首碼的所有使用這個命令時。</span><span class="sxs-lookup"><span data-stu-id="07621-183">Make sure toospecify all of hello address prefixes when using this command.</span></span>

  ```azurecli
  az network vnet update -n TestVNet1 --address-prefixes 10.11.0.0/16 10.12.0.0/16 -g TestRG1
  ```
4. <span data-ttu-id="07621-184">建立 hello 後端子網路。</span><span class="sxs-lookup"><span data-stu-id="07621-184">Create hello backend subnet.</span></span>
  
  ```azurecli
  az network vnet subnet create --vnet-name TestVNet1 -n BackEnd -g TestRG1 --address-prefix 10.12.0.0/24 
  ```
5. <span data-ttu-id="07621-185">建立 hello 閘道子網路。</span><span class="sxs-lookup"><span data-stu-id="07621-185">Create hello gateway subnet.</span></span> <span data-ttu-id="07621-186">請注意該 hello 閘道子網路名稱為 'GatewaySubnet'。</span><span class="sxs-lookup"><span data-stu-id="07621-186">Notice that hello gateway subnet is named 'GatewaySubnet'.</span></span> <span data-ttu-id="07621-187">此名稱是必要的。</span><span class="sxs-lookup"><span data-stu-id="07621-187">This name is required.</span></span> <span data-ttu-id="07621-188">在此範例中，使用 /27 hello 閘道子網路。</span><span class="sxs-lookup"><span data-stu-id="07621-188">In this example, hello gateway subnet is using a /27.</span></span> <span data-ttu-id="07621-189">雖然可能 toocreate 閘道子網路為/29，我們建議您建立較大的子網路選取至少是/28 或 /27 包含多個位址。</span><span class="sxs-lookup"><span data-stu-id="07621-189">While it is possible toocreate a gateway subnet as small as /29, we recommend that you create a larger subnet that includes more addresses by selecting at least /28 or /27.</span></span> <span data-ttu-id="07621-190">這可讓足夠位址 tooaccommodate 可能其他組態，您可能想在 hello 未來。</span><span class="sxs-lookup"><span data-stu-id="07621-190">This will allow for enough addresses tooaccommodate possible additional configurations that you may want in hello future.</span></span>

  ```azurecli 
  az network vnet subnet create --vnet-name TestVNet1 -n GatewaySubnet -g TestRG1 --address-prefix 10.12.255.0/27
  ```
6. <span data-ttu-id="07621-191">要求的公用 IP 位址 toobe 配置的 toohello 閘道您將建立您的 VNet。</span><span class="sxs-lookup"><span data-stu-id="07621-191">Request a public IP address toobe allocated toohello gateway you will create for your VNet.</span></span> <span data-ttu-id="07621-192">請注意該 hello AllocationMethod 是動態。</span><span class="sxs-lookup"><span data-stu-id="07621-192">Notice that hello AllocationMethod is Dynamic.</span></span> <span data-ttu-id="07621-193">您無法指定您想 toouse hello IP 位址。</span><span class="sxs-lookup"><span data-stu-id="07621-193">You cannot specify hello IP address that you want toouse.</span></span> <span data-ttu-id="07621-194">它是動態配置的 tooyour 閘道。</span><span class="sxs-lookup"><span data-stu-id="07621-194">It's dynamically allocated tooyour gateway.</span></span>

  ```azurecli
  az network public-ip create -n VNet1GWIP -g TestRG1 --allocation-method Dynamic
  ```
7. <span data-ttu-id="07621-195">建立 TestVNet1 hello 虛擬網路閘道。</span><span class="sxs-lookup"><span data-stu-id="07621-195">Create hello virtual network gateway for TestVNet1.</span></span> <span data-ttu-id="07621-196">VNet 對 VNet 組態需要 RouteBased VpnType。</span><span class="sxs-lookup"><span data-stu-id="07621-196">VNet-to-VNet configurations require a RouteBased VpnType.</span></span> <span data-ttu-id="07621-197">如果您執行此命令使用 hello '-沒有-wait' 參數，您沒有看到任何意見反應或輸出。</span><span class="sxs-lookup"><span data-stu-id="07621-197">If you run this command using hello '--no-wait' parameter, you don't see any feedback or output.</span></span> <span data-ttu-id="07621-198">hello '-沒有-wait' 參數可讓 hello 閘道 toocreate hello 背景。</span><span class="sxs-lookup"><span data-stu-id="07621-198">hello '--no-wait' parameter allows hello gateway toocreate in hello background.</span></span> <span data-ttu-id="07621-199">它並不表示該 hello VPN 閘道完成立即建立。</span><span class="sxs-lookup"><span data-stu-id="07621-199">It does not mean that hello VPN gateway finishes creating immediately.</span></span> <span data-ttu-id="07621-200">建立閘道可以通常要花費 45 分鐘或更多，根據 hello 閘道使用的 SKU。</span><span class="sxs-lookup"><span data-stu-id="07621-200">Creating a gateway can often take 45 minutes or more, depending on hello gateway SKU that you use.</span></span>

  ```azurecli
  az network vnet-gateway create -n VNet1GW -l eastus --public-ip-address VNet1GWIP -g TestRG1 --vnet TestVNet1 --gateway-type Vpn --sku VpnGw1 --vpn-type RouteBased --no-wait
  ```

### <span data-ttu-id="07621-201"><a name="TestVNet4"></a>步驟 3 - 建立及設定 TestVNet4</span><span class="sxs-lookup"><span data-stu-id="07621-201"><a name="TestVNet4"></a>Step 3 - Create and configure TestVNet4</span></span>

1. <span data-ttu-id="07621-202">建立資源群組。</span><span class="sxs-lookup"><span data-stu-id="07621-202">Create a resource group.</span></span>

  ```azurecli
  az group create -n TestRG4  -l westus
  ```
2. <span data-ttu-id="07621-203">建立 TestVNet4。</span><span class="sxs-lookup"><span data-stu-id="07621-203">Create TestVNet4.</span></span>

  ```azurecli
  az network vnet create -n TestVNet4 -g TestRG4 --address-prefix 10.41.0.0/16 -l westus --subnet-name FrontEnd --subnet-prefix 10.41.0.0/24
  ```

3. <span data-ttu-id="07621-204">為 TestVNet4 建立其他子網路。</span><span class="sxs-lookup"><span data-stu-id="07621-204">Create additional subnets for TestVNet4.</span></span>

  ```azurecli
  az network vnet update -n TestVNet4 --address-prefixes 10.41.0.0/16 10.42.0.0/16 -g TestRG4 
  az network vnet subnet create --vnet-name TestVNet4 -n BackEnd -g TestRG4 --address-prefix 10.42.0.0/24 
  ```
4. <span data-ttu-id="07621-205">建立 hello 閘道子網路。</span><span class="sxs-lookup"><span data-stu-id="07621-205">Create hello gateway subnet.</span></span>

  ```azurecli
   az network vnet subnet create --vnet-name TestVNet4 -n GatewaySubnet -g TestRG4 --address-prefix 10.42.255.0/27
  ```
5. <span data-ttu-id="07621-206">要求公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="07621-206">Request a Public IP address.</span></span>

  ```azurecli
  az network public-ip create -n VNet4GWIP -g TestRG4 --allocation-method Dynamic
  ```
6. <span data-ttu-id="07621-207">建立 hello TestVNet4 虛擬網路閘道。</span><span class="sxs-lookup"><span data-stu-id="07621-207">Create hello TestVNet4 virtual network gateway.</span></span>

  ```azurecli
  az network vnet-gateway create -n VNet4GW -l westus --public-ip-address VNet4GWIP -g TestRG4 --vnet TestVNet4 --gateway-type Vpn --sku VpnGw1 --vpn-type RouteBased --no-wait
  ```

### <span data-ttu-id="07621-208"><a name="createconnect"></a>步驟 4-建立 hello 連線</span><span class="sxs-lookup"><span data-stu-id="07621-208"><a name="createconnect"></a>Step 4 - Create hello connections</span></span>

<span data-ttu-id="07621-209">您現在有兩個具有 VPN 閘道的 VNet。</span><span class="sxs-lookup"><span data-stu-id="07621-209">You now have two VNets with VPN gateways.</span></span> <span data-ttu-id="07621-210">hello 下一個步驟是 hello 虛擬網路閘道之間的 toocreate VPN 閘道連線。</span><span class="sxs-lookup"><span data-stu-id="07621-210">hello next step is toocreate VPN gateway connections between hello virtual network gateways.</span></span> <span data-ttu-id="07621-211">如果您使用上述的 hello 範例，VNet 閘道位於不同的資源群組中。</span><span class="sxs-lookup"><span data-stu-id="07621-211">If you used hello examples above, your VNet gateways are in different resource groups.</span></span> <span data-ttu-id="07621-212">在不同的資源群組中閘道時，您需要 tooidentify，並建立連接時指定每個閘道的 hello 資源 Id。</span><span class="sxs-lookup"><span data-stu-id="07621-212">When gateways are in different resource groups, you need tooidentify and specify hello resource IDs for each gateway when making a connection.</span></span> <span data-ttu-id="07621-213">如果您的 Vnet 中 hello 相同資源群組中，您可以使用 hello[第二個集合的指示](#samerg)因為您不需要 toospecify hello 資源 Id。</span><span class="sxs-lookup"><span data-stu-id="07621-213">If your VNets are in hello same resource group, you can use hello [second set of instructions](#samerg) because you don't need toospecify hello resource IDs.</span></span>

### <span data-ttu-id="07621-214"><a name="diffrg"></a>tooconnect 位於不同的資源群組中的 Vnet</span><span class="sxs-lookup"><span data-stu-id="07621-214"><a name="diffrg"></a>tooconnect VNets that reside in different resource groups</span></span>

1. <span data-ttu-id="07621-215">取得 hello 的 VNet1GW 資源識別碼 hello 輸出 hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="07621-215">Get hello Resource ID of VNet1GW from hello output of hello following command:</span></span>

  ```azurecli
  az network vnet-gateway show -n VNet1GW -g TestRG1
  ```

  <span data-ttu-id="07621-216">Hello 輸出中尋找 hello"識別碼:"行。</span><span class="sxs-lookup"><span data-stu-id="07621-216">In hello output, find hello "id:" line.</span></span> <span data-ttu-id="07621-217">hello 並用引號括住的 hello 值為 hello 下一節中所需的 toocreate hello 連線。</span><span class="sxs-lookup"><span data-stu-id="07621-217">hello values within hello quotes are needed toocreate hello connection in hello next section.</span></span> <span data-ttu-id="07621-218">使您可以輕鬆地將其貼在建立您的連線時，請複製這些值 tooa 文字編輯器，例如 [記事本]。</span><span class="sxs-lookup"><span data-stu-id="07621-218">Copy these values tooa text editor, such as Notepad, so that you can easily paste them when creating your connection.</span></span>

  <span data-ttu-id="07621-219">範例輸出︰</span><span class="sxs-lookup"><span data-stu-id="07621-219">Example output:</span></span>

  ```
  "activeActive": false, 
  "bgpSettings": { 
    "asn": 65515, 
    "bgpPeeringAddress": "10.12.255.30", 
    "peerWeight": 0 
   }, 
  "enableBgp": false, 
  "etag": "W/\"ecb42bc5-c176-44e1-802f-b0ce2962ac04\"", 
  "gatewayDefaultSite": null, 
  "gatewayType": "Vpn", 
  "id": "/subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW", 
  "ipConfigurations":
  ```

  <span data-ttu-id="07621-220">Hello 值之後，複製**「 識別碼 」:** hello 括在引號內。</span><span class="sxs-lookup"><span data-stu-id="07621-220">Copy hello values after **"id":** within hello quotes.</span></span>

  ```
  "id": "/subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW"
 ```

2. <span data-ttu-id="07621-221">收到 hello 的 VNet4GW 資源識別碼和複製 hello 值 tooa 文字編輯器。</span><span class="sxs-lookup"><span data-stu-id="07621-221">Get hello Resource ID of VNet4GW and copy hello values tooa text editor.</span></span>

  ```azurecli
  az network vnet-gateway show -n VNet4GW -g TestRG4
  ```

3. <span data-ttu-id="07621-222">建立 hello TestVNet1 tooTestVNet4 連線。</span><span class="sxs-lookup"><span data-stu-id="07621-222">Create hello TestVNet1 tooTestVNet4 connection.</span></span> <span data-ttu-id="07621-223">在此步驟中，您會從 TestVNet1 tooTestVNet4 建立 hello 連線。</span><span class="sxs-lookup"><span data-stu-id="07621-223">In this step, you create hello connection from TestVNet1 tooTestVNet4.</span></span> <span data-ttu-id="07621-224">沒有 hello 範例中所參考的共用的金鑰。</span><span class="sxs-lookup"><span data-stu-id="07621-224">There is a shared key referenced in hello examples.</span></span> <span data-ttu-id="07621-225">您可以使用您自己的值為 hello 共用金鑰。</span><span class="sxs-lookup"><span data-stu-id="07621-225">You can use your own values for hello shared key.</span></span> <span data-ttu-id="07621-226">hello 很重要的是該 hello 共用的金鑰必須符合這兩個連接。</span><span class="sxs-lookup"><span data-stu-id="07621-226">hello important thing is that hello shared key must match for both connections.</span></span> <span data-ttu-id="07621-227">建立連線需要時 toocomplete 短。</span><span class="sxs-lookup"><span data-stu-id="07621-227">Creating a connection takes a short while toocomplete.</span></span>

  ```azurecli
  az network vpn-connection create -n VNet1ToVNet4 -g TestRG1 --vnet-gateway1 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW -l eastus --shared-key "aabbcc" --vnet-gateway2 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG4/providers/Microsoft.Network/virtualNetworkGateways/VNet4GW 
  ```
4. <span data-ttu-id="07621-228">建立 hello TestVNet4 tooTestVNet1 連線。</span><span class="sxs-lookup"><span data-stu-id="07621-228">Create hello TestVNet4 tooTestVNet1 connection.</span></span> <span data-ttu-id="07621-229">除了您要建立 hello 連線從 TestVNet4 tooTestVNet1 類似 toohello 一個以上版本，則此步驟。</span><span class="sxs-lookup"><span data-stu-id="07621-229">This step is similar toohello one above, except you are creating hello connection from TestVNet4 tooTestVNet1.</span></span> <span data-ttu-id="07621-230">請確定 hello 共用金鑰相符。</span><span class="sxs-lookup"><span data-stu-id="07621-230">Make sure hello shared keys match.</span></span> <span data-ttu-id="07621-231">花幾分鐘的時間 tooestablish hello 連線。</span><span class="sxs-lookup"><span data-stu-id="07621-231">It takes a few minutes tooestablish hello connection.</span></span>

  ```azurecli
  az network vpn-connection create -n VNet4ToVNet1 -g TestRG4 --vnet-gateway1 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG4/providers/Microsoft.Network/virtualNetworkGateways/VNet4GW -l westus --shared-key "aabbcc" --vnet-gateway2 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1G
  ```
5. <span data-ttu-id="07621-232">確認您的連線。</span><span class="sxs-lookup"><span data-stu-id="07621-232">Verify your connections.</span></span> <span data-ttu-id="07621-233">請參閱[驗證您的連線](#verify)。</span><span class="sxs-lookup"><span data-stu-id="07621-233">See [Verify your connection](#verify).</span></span>

### <span data-ttu-id="07621-234"><a name="samerg"></a>tooconnect Vnet 中的 hello 相同資源群組</span><span class="sxs-lookup"><span data-stu-id="07621-234"><a name="samerg"></a>tooconnect VNets that reside in hello same resource group</span></span>

1. <span data-ttu-id="07621-235">建立 hello TestVNet1 tooTestVNet4 連線。</span><span class="sxs-lookup"><span data-stu-id="07621-235">Create hello TestVNet1 tooTestVNet4 connection.</span></span> <span data-ttu-id="07621-236">在此步驟中，您會從 TestVNet1 tooTestVNet4 建立 hello 連線。</span><span class="sxs-lookup"><span data-stu-id="07621-236">In this step, you create hello connection from TestVNet1 tooTestVNet4.</span></span> <span data-ttu-id="07621-237">請注意 hello 資源群組是 hello hello 範例中相同。</span><span class="sxs-lookup"><span data-stu-id="07621-237">Notice hello resource groups are hello same in hello examples.</span></span> <span data-ttu-id="07621-238">您也會看見 hello 範例中所參考的共用的金鑰。</span><span class="sxs-lookup"><span data-stu-id="07621-238">You also see a shared key referenced in hello examples.</span></span> <span data-ttu-id="07621-239">您可以使用您自己的值為 hello 共用金鑰，不過，hello 共用的金鑰必須符合這兩個連接。</span><span class="sxs-lookup"><span data-stu-id="07621-239">You can use your own values for hello shared key, however, hello shared key must match for both connections.</span></span> <span data-ttu-id="07621-240">建立連線需要時 toocomplete 短。</span><span class="sxs-lookup"><span data-stu-id="07621-240">Creating a connection takes a short while toocomplete.</span></span>

  ```azurecli
  az network vpn-connection create -n VNet1ToVNet4 -g TestRG1 --vnet-gateway1 VNet1GW -l eastus --shared-key "eeffgg" --vnet-gateway2 VNet4GW
  ```
2. <span data-ttu-id="07621-241">建立 hello TestVNet4 tooTestVNet1 連線。</span><span class="sxs-lookup"><span data-stu-id="07621-241">Create hello TestVNet4 tooTestVNet1 connection.</span></span> <span data-ttu-id="07621-242">除了您要建立 hello 連線從 TestVNet4 tooTestVNet1 類似 toohello 一個以上版本，則此步驟。</span><span class="sxs-lookup"><span data-stu-id="07621-242">This step is similar toohello one above, except you are creating hello connection from TestVNet4 tooTestVNet1.</span></span> <span data-ttu-id="07621-243">請確定 hello 共用金鑰相符。</span><span class="sxs-lookup"><span data-stu-id="07621-243">Make sure hello shared keys match.</span></span> <span data-ttu-id="07621-244">花幾分鐘的時間 tooestablish hello 連線。</span><span class="sxs-lookup"><span data-stu-id="07621-244">It takes a few minutes tooestablish hello connection.</span></span>

  ```azurecli
  az network vpn-connection create -n VNet4ToVNet1 -g TestRG1 --vnet-gateway1 VNet4GW -l eastus --shared-key "eeffgg" --vnet-gateway2 VNet1GW
  ```
3. <span data-ttu-id="07621-245">確認您的連線。</span><span class="sxs-lookup"><span data-stu-id="07621-245">Verify your connections.</span></span> <span data-ttu-id="07621-246">請參閱[驗證您的連線](#verify)。</span><span class="sxs-lookup"><span data-stu-id="07621-246">See [Verify your connection](#verify).</span></span>

## <span data-ttu-id="07621-247"><a name="difsub"></a>與位於不同訂用帳戶的 VNet 連線</span><span class="sxs-lookup"><span data-stu-id="07621-247"><a name="difsub"></a>Connect VNets that are in different subscriptions</span></span>

![v2v 圖表](./media/vpn-gateway-howto-vnet-vnet-cli/v2vdiffsub.png)

<span data-ttu-id="07621-249">在此案例中，我們會連接 TestVNet1 和 TestVNet5。</span><span class="sxs-lookup"><span data-stu-id="07621-249">In this scenario, we connect TestVNet1 and TestVNet5.</span></span> <span data-ttu-id="07621-250">hello Vnet 可位於不同的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="07621-250">hello VNets reside different subscriptions.</span></span> <span data-ttu-id="07621-251">hello 訂用帳戶不需要與 hello 相關聯的 toobe 相同的 Active Directory 租用戶。</span><span class="sxs-lookup"><span data-stu-id="07621-251">hello subscriptions do not need toobe associated with hello same Active Directory tenant.</span></span> <span data-ttu-id="07621-252">此設定的 hello 步驟順序 tooconnect TestVNet1 tooTestVNet5 中加入額外的 VNet 對 VNet 連線。</span><span class="sxs-lookup"><span data-stu-id="07621-252">hello steps for this configuration add an additional VNet-to-VNet connection in order tooconnect TestVNet1 tooTestVNet5.</span></span>

### <span data-ttu-id="07621-253"><a name="TestVNet1diff"></a>步驟 5 - 建立及設定 TestVNet1</span><span class="sxs-lookup"><span data-stu-id="07621-253"><a name="TestVNet1diff"></a>Step 5 - Create and configure TestVNet1</span></span>

<span data-ttu-id="07621-254">從 hello 前幾節中的 hello 步驟繼續執行這些指示。</span><span class="sxs-lookup"><span data-stu-id="07621-254">These instructions continue from hello steps in hello preceding sections.</span></span> <span data-ttu-id="07621-255">您必須先完成[步驟 1](#Connect)和[步驟 2](#TestVNet1) toocreate 並設定 TestVNet1 hello TestVNet1 VPN 閘道。</span><span class="sxs-lookup"><span data-stu-id="07621-255">You must complete [Step 1](#Connect) and [Step 2](#TestVNet1) toocreate and configure TestVNet1 and hello VPN Gateway for TestVNet1.</span></span> <span data-ttu-id="07621-256">此組態中，您不需要的 toocreate TestVNet4 hello 前一節，雖然如果您建立它，它不會衝突進行這些步驟。</span><span class="sxs-lookup"><span data-stu-id="07621-256">For this configuration, you are not required toocreate TestVNet4 from hello previous section, although if you do create it, it will not conflict with these steps.</span></span> <span data-ttu-id="07621-257">完成步驟 1 和步驟 2 後，繼續進行下面的步驟 6。</span><span class="sxs-lookup"><span data-stu-id="07621-257">Once you complete Step 1 and Step 2, continue with Step 6 (below).</span></span>

### <span data-ttu-id="07621-258"><a name="verifyranges"></a>步驟 6-確認 hello IP 位址範圍</span><span class="sxs-lookup"><span data-stu-id="07621-258"><a name="verifyranges"></a>Step 6 - Verify hello IP address ranges</span></span>

<span data-ttu-id="07621-259">在建立其他連接時，很重要 tooverify hello 的 hello 新的虛擬網路的 IP 位址空間未與任何其他 VNet 範圍或區域網路閘道的範圍重疊。</span><span class="sxs-lookup"><span data-stu-id="07621-259">When creating additional connections, it's important tooverify that hello IP address space of hello new virtual network does not overlap with any of your other VNet ranges or local network gateway ranges.</span></span> <span data-ttu-id="07621-260">針對此練習，您可以使用下列值 hello TestVNet5 hello:</span><span class="sxs-lookup"><span data-stu-id="07621-260">For this exercise, you can use hello following values for hello TestVNet5:</span></span>

<span data-ttu-id="07621-261">**TestVNet5 的值︰**</span><span class="sxs-lookup"><span data-stu-id="07621-261">**Values for TestVNet5:**</span></span>

* <span data-ttu-id="07621-262">VNet 名稱︰TestVNet5</span><span class="sxs-lookup"><span data-stu-id="07621-262">VNet Name: TestVNet5</span></span>
* <span data-ttu-id="07621-263">資源群組：TestRG5</span><span class="sxs-lookup"><span data-stu-id="07621-263">Resource Group: TestRG5</span></span>
* <span data-ttu-id="07621-264">位置：日本東部</span><span class="sxs-lookup"><span data-stu-id="07621-264">Location: Japan East</span></span>
* <span data-ttu-id="07621-265">TestVNet5：10.51.0.0/16 和 10.52.0.0/16</span><span class="sxs-lookup"><span data-stu-id="07621-265">TestVNet5: 10.51.0.0/16 & 10.52.0.0/16</span></span>
* <span data-ttu-id="07621-266">FrontEnd：10.51.0.0/24</span><span class="sxs-lookup"><span data-stu-id="07621-266">FrontEnd: 10.51.0.0/24</span></span>
* <span data-ttu-id="07621-267">BackEnd：10.52.0.0/24</span><span class="sxs-lookup"><span data-stu-id="07621-267">BackEnd: 10.52.0.0/24</span></span>
* <span data-ttu-id="07621-268">GatewaySubnet：10.52.255.0.0/27</span><span class="sxs-lookup"><span data-stu-id="07621-268">GatewaySubnet: 10.52.255.0.0/27</span></span>
* <span data-ttu-id="07621-269">GatewayName：VNet5GW</span><span class="sxs-lookup"><span data-stu-id="07621-269">GatewayName: VNet5GW</span></span>
* <span data-ttu-id="07621-270">公用 IP：VNet5GWIP</span><span class="sxs-lookup"><span data-stu-id="07621-270">Public IP: VNet5GWIP</span></span>
* <span data-ttu-id="07621-271">VPNType：RouteBased</span><span class="sxs-lookup"><span data-stu-id="07621-271">VPNType: RouteBased</span></span>
* <span data-ttu-id="07621-272">連線︰VNet5toVNet1</span><span class="sxs-lookup"><span data-stu-id="07621-272">Connection: VNet5toVNet1</span></span>
* <span data-ttu-id="07621-273">ConnectionType：VNet2VNet</span><span class="sxs-lookup"><span data-stu-id="07621-273">ConnectionType: VNet2VNet</span></span>

### <span data-ttu-id="07621-274"><a name="TestVNet5"></a>步驟 7 - 建立及設定 TestVNet5</span><span class="sxs-lookup"><span data-stu-id="07621-274"><a name="TestVNet5"></a>Step 7 - Create and configure TestVNet5</span></span>

<span data-ttu-id="07621-275">Hello 新訂用帳戶，訂用帳戶 5 hello 內容中，必須完成此步驟。</span><span class="sxs-lookup"><span data-stu-id="07621-275">This step must be done in hello context of hello new subscription, Subscription 5.</span></span> <span data-ttu-id="07621-276">此組件可能會由擁有 hello 訂用帳戶的另一個組織中的 hello 系統管理員執行。</span><span class="sxs-lookup"><span data-stu-id="07621-276">This part may be performed by hello administrator in a different organization that owns hello subscription.</span></span> <span data-ttu-id="07621-277">訂用帳戶使用之間 tooswitch 'az 帳戶清單--所有' toolist hello 訂用帳戶可用 tooyour 帳戶，然後使用 'az 帳戶集--訂用帳戶<subscriptionID>' 想 toouse tooswitch toohello 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="07621-277">tooswitch between subscriptions use 'az account list --all' toolist hello subscriptions available tooyour account, then use 'az account set --subscription <subscriptionID>' tooswitch toohello subscription that you want toouse.</span></span>

1. <span data-ttu-id="07621-278">請確定您已連線的 tooSubscription 5，則建立的資源群組。</span><span class="sxs-lookup"><span data-stu-id="07621-278">Make sure you are connected tooSubscription 5, then create a resource group.</span></span>

  ```azurecli
  az group create -n TestRG5  -l japaneast
  ```
2. <span data-ttu-id="07621-279">建立 TestVNet5。</span><span class="sxs-lookup"><span data-stu-id="07621-279">Create TestVNet5.</span></span>

  ```azurecli
  az network vnet create -n TestVNet5 -g TestRG5 --address-prefix 10.51.0.0/16 -l japaneast --subnet-name FrontEnd --subnet-prefix 10.51.0.0/24
  ```

3. <span data-ttu-id="07621-280">新增子網路。</span><span class="sxs-lookup"><span data-stu-id="07621-280">Add subnets.</span></span>

  ```azurecli
  az network vnet update -n TestVNet5 --address-prefixes 10.51.0.0/16 10.52.0.0/16 -g TestRG5
  az network vnet subnet create --vnet-name TestVNet5 -n BackEnd -g TestRG5 --address-prefix 10.52.0.0/24
  ```

4. <span data-ttu-id="07621-281">加入 hello 閘道子網路。</span><span class="sxs-lookup"><span data-stu-id="07621-281">Add hello gateway subnet.</span></span>

  ```azurecli
  az network vnet subnet create --vnet-name TestVNet5 -n GatewaySubnet -g TestRG5 --address-prefix 10.52.255.0/27
  ```

5. <span data-ttu-id="07621-282">要求公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="07621-282">Request a public IP address.</span></span>

  ```azurecli
  az network public-ip create -n VNet5GWIP -g TestRG5 --allocation-method Dynamic
  ```
6. <span data-ttu-id="07621-283">建立 hello TestVNet5 閘道</span><span class="sxs-lookup"><span data-stu-id="07621-283">Create hello TestVNet5 gateway</span></span>

  ```azurecli
  az network vnet-gateway create -n VNet5GW -l japaneast --public-ip-address VNet5GWIP -g TestRG5 --vnet TestVNet5 --gateway-type Vpn --sku VpnGw1 --vpn-type RouteBased --no-wait
  ```

### <span data-ttu-id="07621-284"><a name="connections5"></a>步驟 8-建立 hello 連線</span><span class="sxs-lookup"><span data-stu-id="07621-284"><a name="connections5"></a>Step 8 - Create hello connections</span></span>

<span data-ttu-id="07621-285">我們會分割成兩個標示的 CLI 工作階段的這個步驟**[訂用帳戶 1]**，和**[訂用帳戶 5]**因為 hello 閘道 hello 不同訂用帳戶中。</span><span class="sxs-lookup"><span data-stu-id="07621-285">We split this step into two CLI sessions marked as **[Subscription 1]**, and **[Subscription 5]** because hello gateways are in hello different subscriptions.</span></span> <span data-ttu-id="07621-286">訂用帳戶使用之間 tooswitch 'az 帳戶清單--所有' toolist hello 訂用帳戶可用 tooyour 帳戶，然後使用 'az 帳戶集--訂用帳戶<subscriptionID>' 想 toouse tooswitch toohello 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="07621-286">tooswitch between subscriptions use 'az account list --all' toolist hello subscriptions available tooyour account, then use 'az account set --subscription <subscriptionID>' tooswitch toohello subscription that you want toouse.</span></span>

1. <span data-ttu-id="07621-287">**[訂用帳戶 1]**登入，並連接 tooSubscription 1。</span><span class="sxs-lookup"><span data-stu-id="07621-287">**[Subscription 1]** Log in and connect tooSubscription 1.</span></span> <span data-ttu-id="07621-288">Hello 執行的下列命令 tooget hello 名稱和識別碼 hello hello 輸出的閘道：</span><span class="sxs-lookup"><span data-stu-id="07621-288">Run hello following command tooget hello name and ID of hello Gateway from hello output:</span></span>

  ```azurecli
  az network vnet-gateway show -n VNet1GW -g TestRG1
  ```

  <span data-ttu-id="07621-289">複製 hello 輸出 」 識別碼:"。</span><span class="sxs-lookup"><span data-stu-id="07621-289">Copy hello output for "id:".</span></span> <span data-ttu-id="07621-290">傳送 hello 識別碼和 hello hello VNet 閘道 (VNet1GW) toohello 管理員的訂用帳戶 5 透過電子郵件或其他方法的名稱。</span><span class="sxs-lookup"><span data-stu-id="07621-290">Send hello ID and hello name of hello VNet gateway (VNet1GW) toohello administrator of Subscription 5 via email or another method.</span></span>

  <span data-ttu-id="07621-291">範例輸出︰</span><span class="sxs-lookup"><span data-stu-id="07621-291">Example output:</span></span>

  ```
  "id": "/subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW"
  ```

2. <span data-ttu-id="07621-292">**[訂用帳戶 5]**登入，並連接 tooSubscription 5。</span><span class="sxs-lookup"><span data-stu-id="07621-292">**[Subscription 5]** Log in and connect tooSubscription 5.</span></span> <span data-ttu-id="07621-293">Hello 執行的下列命令 tooget hello 名稱和識別碼 hello hello 輸出的閘道：</span><span class="sxs-lookup"><span data-stu-id="07621-293">Run hello following command tooget hello name and ID of hello Gateway from hello output:</span></span>

  ```azurecli
  az network vnet-gateway show -n VNet5GW -g TestRG5
  ```

  <span data-ttu-id="07621-294">複製 hello 輸出 」 識別碼:"。</span><span class="sxs-lookup"><span data-stu-id="07621-294">Copy hello output for "id:".</span></span> <span data-ttu-id="07621-295">傳送 hello 識別碼和 hello hello VNet 閘道 (VNet5GW) toohello 管理員的訂用帳戶 1 透過電子郵件或其他方法的名稱。</span><span class="sxs-lookup"><span data-stu-id="07621-295">Send hello ID and hello name of hello VNet gateway (VNet5GW) toohello administrator of Subscription 1 via email or another method.</span></span>

3. <span data-ttu-id="07621-296">**[訂用帳戶 1]**在此步驟中，您建立從 TestVNet1 tooTestVNet5 hello 連線。</span><span class="sxs-lookup"><span data-stu-id="07621-296">**[Subscription 1]** In this step, you create hello connection from TestVNet1 tooTestVNet5.</span></span> <span data-ttu-id="07621-297">您可以使用您自己的值為 hello 共用金鑰，不過，hello 共用的金鑰必須符合這兩個連接。</span><span class="sxs-lookup"><span data-stu-id="07621-297">You can use your own values for hello shared key, however, hello shared key must match for both connections.</span></span> <span data-ttu-id="07621-298">建立連接，可能會同時 toocomplete 短。</span><span class="sxs-lookup"><span data-stu-id="07621-298">Creating a connection can take a short while toocomplete.</span></span> <span data-ttu-id="07621-299">請確定您連接 tooSubscription 1。</span><span class="sxs-lookup"><span data-stu-id="07621-299">Make sure you connect tooSubscription 1.</span></span>

  ```azurecli
  az network vpn-connection create -n VNet1ToVNet5 -g TestRG1 --vnet-gateway1 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW -l eastus --shared-key "eeffgg" --vnet-gateway2 /subscriptions/e7e33b39-fe28-4822-b65c-a4db8bbff7cb/resourceGroups/TestRG5/providers/Microsoft.Network/virtualNetworkGateways/VNet5GW
  ```

4. <span data-ttu-id="07621-300">**[訂用帳戶 5]**這個步驟是上述其中一個類似 toohello，除了您要建立 hello 連線從 TestVNet5 tooTestVNet1。</span><span class="sxs-lookup"><span data-stu-id="07621-300">**[Subscription 5]** This step is similar toohello one above, except you are creating hello connection from TestVNet5 tooTestVNet1.</span></span> <span data-ttu-id="07621-301">請確定該 hello 共用金鑰相符，而且您連線 tooSubscription 5。</span><span class="sxs-lookup"><span data-stu-id="07621-301">Make sure that hello shared keys match and that you connect tooSubscription 5.</span></span>

  ```azurecli
  az network vpn-connection create -n VNet5ToVNet1 -g TestRG5 --vnet-gateway1 /subscriptions/e7e33b39-fe28-4822-b65c-a4db8bbff7cb/resourceGroups/TestRG5/providers/Microsoft.Network/virtualNetworkGateways/VNet5GW -l japaneast --shared-key "eeffgg" --vnet-gateway2 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW
  ```

## <span data-ttu-id="07621-302"><a name="verify"></a>確認 hello 的連接</span><span class="sxs-lookup"><span data-stu-id="07621-302"><a name="verify"></a>Verify hello connections</span></span>
[!INCLUDE [vpn-gateway-no-nsg-include](../../includes/vpn-gateway-no-nsg-include.md)]

[!INCLUDE [verify connections v2v cli](../../includes/vpn-gateway-verify-connection-cli-rm-include.md)]

## <span data-ttu-id="07621-303"><a name="faq"></a>VNet 對 VNet 常見問題集</span><span class="sxs-lookup"><span data-stu-id="07621-303"><a name="faq"></a>VNet-to-VNet FAQ</span></span>
[!INCLUDE [vpn-gateway-vnet-vnet-faq](../../includes/vpn-gateway-vnet-vnet-faq-include.md)]

## <a name="next-steps"></a><span data-ttu-id="07621-304">後續步驟</span><span class="sxs-lookup"><span data-stu-id="07621-304">Next steps</span></span>

* <span data-ttu-id="07621-305">一旦完成您的連線，您可以將虛擬機器 tooyour 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="07621-305">Once your connection is complete, you can add virtual machines tooyour virtual networks.</span></span> <span data-ttu-id="07621-306">如需詳細資訊，請參閱 hello[虛擬機器文件](https://docs.microsoft.com/azure/#pivot=services&panel=Compute)。</span><span class="sxs-lookup"><span data-stu-id="07621-306">For more information, see hello [Virtual Machines documentation](https://docs.microsoft.com/azure/#pivot=services&panel=Compute).</span></span>
* <span data-ttu-id="07621-307">BGP 的相關資訊，請參閱 hello [BGP 概觀](vpn-gateway-bgp-overview.md)和[如何 tooconfigure BGP](vpn-gateway-bgp-resource-manager-ps.md)。</span><span class="sxs-lookup"><span data-stu-id="07621-307">For information about BGP, see hello [BGP Overview](vpn-gateway-bgp-overview.md) and [How tooconfigure BGP](vpn-gateway-bgp-resource-manager-ps.md).</span></span>
