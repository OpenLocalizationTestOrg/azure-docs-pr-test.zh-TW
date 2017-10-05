---
title: "將 Azure 虛擬網路連接至另一個 VNet︰PowerShell | Microsoft Docs"
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
ms.openlocfilehash: 8c42c0046ccaa98c572134042fbbb7e883ef93c3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="configure-a-vnet-to-vnet-vpn-gateway-connection-using-powershell"></a><span data-ttu-id="7939f-103">使用 PowerShell 設定 VNet 對 VNet 的 VPN 閘道連線</span><span class="sxs-lookup"><span data-stu-id="7939f-103">Configure a VNet-to-VNet VPN gateway connection using PowerShell</span></span>

<span data-ttu-id="7939f-104">本文說明如何建立虛擬網路之間的VPN 閘道連線。</span><span class="sxs-lookup"><span data-stu-id="7939f-104">This article shows you how to create a VPN gateway connection between virtual networks.</span></span> <span data-ttu-id="7939f-105">虛擬網路可位於相同或不同的區域，以及來自相同或不同的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="7939f-105">The virtual networks can be in the same or different regions, and from the same or different subscriptions.</span></span> <span data-ttu-id="7939f-106">連線來自不同訂用帳戶的 VNet 時，訂用帳戶不需與相同的 Active Directory 租用戶相關聯。</span><span class="sxs-lookup"><span data-stu-id="7939f-106">When connecting VNets from different subscriptions, the subscriptions do not need to be associated with the same Active Directory tenant.</span></span> 

<span data-ttu-id="7939f-107">本文中的步驟適用於 Resource Manager 部署模型並使用 PowerShell。</span><span class="sxs-lookup"><span data-stu-id="7939f-107">The steps in this article apply to the Resource Manager deployment model and use PowerShell.</span></span> <span data-ttu-id="7939f-108">您也可從下列清單中選取不同的選項，以使用不同的部署工具或部署模型來建立此組態：</span><span class="sxs-lookup"><span data-stu-id="7939f-108">You can also create this configuration using a different deployment tool or deployment model by selecting a different option from the following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="7939f-109">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="7939f-109">Azure portal</span></span>](vpn-gateway-howto-vnet-vnet-resource-manager-portal.md)
> * [<span data-ttu-id="7939f-110">PowerShell</span><span class="sxs-lookup"><span data-stu-id="7939f-110">PowerShell</span></span>](vpn-gateway-vnet-vnet-rm-ps.md)
> * [<span data-ttu-id="7939f-111">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="7939f-111">Azure CLI</span></span>](vpn-gateway-howto-vnet-vnet-cli.md)
> * [<span data-ttu-id="7939f-112">Azure 入口網站 (傳統)</span><span class="sxs-lookup"><span data-stu-id="7939f-112">Azure portal (classic)</span></span>](vpn-gateway-howto-vnet-vnet-portal-classic.md)
> * [<span data-ttu-id="7939f-113">連線不同的部署模型 - Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="7939f-113">Connect different deployment models - Azure portal</span></span>](vpn-gateway-connect-different-deployment-models-portal.md)
> * [<span data-ttu-id="7939f-114">連線不同的部署模型 - PowerShell</span><span class="sxs-lookup"><span data-stu-id="7939f-114">Connect different deployment models - PowerShell</span></span>](vpn-gateway-connect-different-deployment-models-powershell.md)
>
>

<span data-ttu-id="7939f-115">將虛擬網路連接至另一個虛擬網路 (VNet 對 VNet)，類似於將 VNet 連接至內部部署網站位置。</span><span class="sxs-lookup"><span data-stu-id="7939f-115">Connecting a virtual network to another virtual network (VNet-to-VNet) is similar to connecting a VNet to an on-premises site location.</span></span> <span data-ttu-id="7939f-116">這兩種連線類型都使用 VPN 閘道提供使用 IPsec/IKE 的安全通道。</span><span class="sxs-lookup"><span data-stu-id="7939f-116">Both connectivity types use a VPN gateway to provide a secure tunnel using IPsec/IKE.</span></span> <span data-ttu-id="7939f-117">如果您的 Vnet 位在相同區域，您可能會考慮使用 VNet 對等互連來進行連線。</span><span class="sxs-lookup"><span data-stu-id="7939f-117">If your VNets are in the same region, you may want to consider connecting them using VNet Peering.</span></span> <span data-ttu-id="7939f-118">VNet 對等互連不會使用 VPN 閘道。</span><span class="sxs-lookup"><span data-stu-id="7939f-118">VNet peering does not use a VPN gateway.</span></span> <span data-ttu-id="7939f-119">如需詳細資訊，請參閱 [VNet 對等互連](../virtual-network/virtual-network-peering-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="7939f-119">For more information, see [VNet peering](../virtual-network/virtual-network-peering-overview.md).</span></span>

<span data-ttu-id="7939f-120">您可以將 VNet 對 VNet 通訊與多站台組態結合。</span><span class="sxs-lookup"><span data-stu-id="7939f-120">VNet-to-VNet communication can be combined with multi-site configurations.</span></span> <span data-ttu-id="7939f-121">這可讓您建立使用內部虛擬網路連線結合跨單位連線的網路拓撲，如下圖所示：</span><span class="sxs-lookup"><span data-stu-id="7939f-121">This lets you establish network topologies that combine cross-premises connectivity with inter-virtual network connectivity, as shown in the following diagram:</span></span>

![關於連線](./media/vpn-gateway-vnet-vnet-rm-ps/aboutconnections.png)

### <a name="why-connect-virtual-networks"></a><span data-ttu-id="7939f-123">為什麼要連接虛擬網路？</span><span class="sxs-lookup"><span data-stu-id="7939f-123">Why connect virtual networks?</span></span>

<span data-ttu-id="7939f-124">針對下列原因，您可能希望連接虛擬網路：</span><span class="sxs-lookup"><span data-stu-id="7939f-124">You may want to connect virtual networks for the following reasons:</span></span>

* <span data-ttu-id="7939f-125">**跨區域的異地備援和異地目前狀態**</span><span class="sxs-lookup"><span data-stu-id="7939f-125">**Cross region geo-redundancy and geo-presence**</span></span>

  * <span data-ttu-id="7939f-126">您可以使用安全連線設定自己的異地複寫或同步處理，而不用查看網際網路對向端點。</span><span class="sxs-lookup"><span data-stu-id="7939f-126">You can set up your own geo-replication or synchronization with secure connectivity without going over Internet-facing endpoints.</span></span>
  * <span data-ttu-id="7939f-127">您可以使用 Azure 流量管理員和負載平衡器，利用異地備援跨多個 Azure 區域設定高度可用的工作負載。</span><span class="sxs-lookup"><span data-stu-id="7939f-127">With Azure Traffic Manager and Load Balancer, you can set up highly available workload with geo-redundancy across multiple Azure regions.</span></span> <span data-ttu-id="7939f-128">其中一個重要的範例就是使用分散在多個 Azure 區域的可用性群組來設定 SQL Always On。</span><span class="sxs-lookup"><span data-stu-id="7939f-128">One important example is to set up SQL Always On with Availability Groups spreading across multiple Azure regions.</span></span>
* <span data-ttu-id="7939f-129">**具有隔離或管理界限的區域性多層式應用程式**</span><span class="sxs-lookup"><span data-stu-id="7939f-129">**Regional multi-tier applications with isolation or administrative boundary**</span></span>

  * <span data-ttu-id="7939f-130">在相同區域中，您可以因為隔離或管理需求，設定將多層式應用程式與多個虛擬網路連線在一起。</span><span class="sxs-lookup"><span data-stu-id="7939f-130">Within the same region, you can set up multi-tier applications with multiple virtual networks connected together due to isolation or administrative requirements.</span></span>

<span data-ttu-id="7939f-131">如需 VNet 對 VNet 連線的詳細資訊，請參閱本文結尾處的 [VNet 對 VNet 常見問題集](#faq) 。</span><span class="sxs-lookup"><span data-stu-id="7939f-131">For more information about VNet-to-VNet connections, see the [VNet-to-VNet FAQ](#faq) at the end of this article.</span></span>

## <a name="which-set-of-steps-should-i-use"></a><span data-ttu-id="7939f-132">我應該使用哪個步驟集？</span><span class="sxs-lookup"><span data-stu-id="7939f-132">Which set of steps should I use?</span></span>

<span data-ttu-id="7939f-133">在本文中，您會看到兩組不同的步驟。</span><span class="sxs-lookup"><span data-stu-id="7939f-133">In this article, you see two different sets of steps.</span></span> <span data-ttu-id="7939f-134">一組步驟適用於[位於相同訂用帳戶中的 VNet](#samesub)，而另一組步驟則適用於[位於不同訂用帳戶中的 VNet](#difsub)。</span><span class="sxs-lookup"><span data-stu-id="7939f-134">One set of steps for [VNets that reside in the same subscription](#samesub), and another for [VNets that reside in different subscriptions](#difsub).</span></span> <span data-ttu-id="7939f-135">兩組之間的主要差異在於您是否可以在相同的 PowerShell 工作階段內建立和設定所有的虛擬網路和閘道資源。</span><span class="sxs-lookup"><span data-stu-id="7939f-135">The key difference between the sets is whether you can create and configure all virtual network and gateway resources within the same PowerShell session.</span></span>

<span data-ttu-id="7939f-136">本文中的步驟會使用在每個區段開頭宣告的變數。</span><span class="sxs-lookup"><span data-stu-id="7939f-136">The steps in this article use variables that are declared at the beginning of each section.</span></span> <span data-ttu-id="7939f-137">如果您已經使用現有的 VNet，請修改變數，以在自己的環境中反映設定。</span><span class="sxs-lookup"><span data-stu-id="7939f-137">If you already are working with existing VNets, modify the variables to reflect the settings in your own environment.</span></span> <span data-ttu-id="7939f-138">如果您想要了解虛擬網路的名稱解析，請參閱[名稱解析](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md)。</span><span class="sxs-lookup"><span data-stu-id="7939f-138">If you want name resolution for your virtual networks, see [Name resolution](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).</span></span>

## <span data-ttu-id="7939f-139"><a name="samesub"></a>如何連接相同訂用帳戶中的 VNet</span><span class="sxs-lookup"><span data-stu-id="7939f-139"><a name="samesub"></a>How to connect VNets that are in the same subscription</span></span>

![v2v 圖表](./media/vpn-gateway-vnet-vnet-rm-ps/v2vrmps.png)

### <a name="before-you-begin"></a><span data-ttu-id="7939f-141">開始之前</span><span class="sxs-lookup"><span data-stu-id="7939f-141">Before you begin</span></span>

<span data-ttu-id="7939f-142">開始之前，您必須安裝最新版的 Azure Resource Manager PowerShell Cmdlet (至少 4.0 或更新版本)。</span><span class="sxs-lookup"><span data-stu-id="7939f-142">Before beginning, you need to install the latest version of the Azure Resource Manager PowerShell cmdlets, at least 4.0 or later.</span></span> <span data-ttu-id="7939f-143">如需如何安裝 PowerShell Cmdlet 的詳細資訊，請參閱[如何安裝和設定 Azure PowerShell](/powershell/azure/overview) 。</span><span class="sxs-lookup"><span data-stu-id="7939f-143">For more information about installing the PowerShell cmdlets, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

### <span data-ttu-id="7939f-144"><a name="Step1"></a>步驟 1 - 規劃 IP 位址範圍</span><span class="sxs-lookup"><span data-stu-id="7939f-144"><a name="Step1"></a>Step 1 - Plan your IP address ranges</span></span>

<span data-ttu-id="7939f-145">在下列步驟中，我們會建立兩個虛擬網路，以及它們各自的閘道子網路和組態。</span><span class="sxs-lookup"><span data-stu-id="7939f-145">In the following steps, we create two virtual networks along with their respective gateway subnets and configurations.</span></span> <span data-ttu-id="7939f-146">接著建立這兩個 VNet 之間的 VPN 連線。</span><span class="sxs-lookup"><span data-stu-id="7939f-146">We then create a VPN connection between the two VNets.</span></span> <span data-ttu-id="7939f-147">請務必規劃您的網路組態的 IP 位址範圍。</span><span class="sxs-lookup"><span data-stu-id="7939f-147">It’s important to plan the IP address ranges for your network configuration.</span></span> <span data-ttu-id="7939f-148">請記住，您必須先確定您的 VNet 範圍或區域網路範圍沒有以任何方式重疊。</span><span class="sxs-lookup"><span data-stu-id="7939f-148">Keep in mind that you must make sure that none of your VNet ranges or local network ranges overlap in any way.</span></span> <span data-ttu-id="7939f-149">在這些範例中，我們不會包含 DNS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="7939f-149">In these examples, we do not include a DNS server.</span></span> <span data-ttu-id="7939f-150">如果您想要了解虛擬網路的名稱解析，請參閱[名稱解析](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md)。</span><span class="sxs-lookup"><span data-stu-id="7939f-150">If you want name resolution for your virtual networks, see [Name resolution](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).</span></span>

<span data-ttu-id="7939f-151">我們會在範例中使用下列值：</span><span class="sxs-lookup"><span data-stu-id="7939f-151">We use the following values in the examples:</span></span>

<span data-ttu-id="7939f-152">**TestVNet1 的值︰**</span><span class="sxs-lookup"><span data-stu-id="7939f-152">**Values for TestVNet1:**</span></span>

* <span data-ttu-id="7939f-153">VNet 名稱︰TestVNet1</span><span class="sxs-lookup"><span data-stu-id="7939f-153">VNet Name: TestVNet1</span></span>
* <span data-ttu-id="7939f-154">資源群組︰TestRG1</span><span class="sxs-lookup"><span data-stu-id="7939f-154">Resource Group: TestRG1</span></span>
* <span data-ttu-id="7939f-155">位置：美國東部</span><span class="sxs-lookup"><span data-stu-id="7939f-155">Location: East US</span></span>
* <span data-ttu-id="7939f-156">TestVNet1：10.11.0.0/16 和 10.12.0.0/16</span><span class="sxs-lookup"><span data-stu-id="7939f-156">TestVNet1: 10.11.0.0/16 & 10.12.0.0/16</span></span>
* <span data-ttu-id="7939f-157">FrontEnd：10.11.0.0/24</span><span class="sxs-lookup"><span data-stu-id="7939f-157">FrontEnd: 10.11.0.0/24</span></span>
* <span data-ttu-id="7939f-158">BackEnd：10.12.0.0/24</span><span class="sxs-lookup"><span data-stu-id="7939f-158">BackEnd: 10.12.0.0/24</span></span>
* <span data-ttu-id="7939f-159">GatewaySubnet：10.12.255.0/27</span><span class="sxs-lookup"><span data-stu-id="7939f-159">GatewaySubnet: 10.12.255.0/27</span></span>
* <span data-ttu-id="7939f-160">GatewayName：VNet1GW</span><span class="sxs-lookup"><span data-stu-id="7939f-160">GatewayName: VNet1GW</span></span>
* <span data-ttu-id="7939f-161">公用 IP: VNet1GWIP</span><span class="sxs-lookup"><span data-stu-id="7939f-161">Public IP: VNet1GWIP</span></span>
* <span data-ttu-id="7939f-162">VPNType：RouteBased</span><span class="sxs-lookup"><span data-stu-id="7939f-162">VPNType: RouteBased</span></span>
* <span data-ttu-id="7939f-163">Connection(1to4)：VNet1toVNet4</span><span class="sxs-lookup"><span data-stu-id="7939f-163">Connection(1to4): VNet1toVNet4</span></span>
* <span data-ttu-id="7939f-164">Connection(1to5)：VNet1toVNet5</span><span class="sxs-lookup"><span data-stu-id="7939f-164">Connection(1to5): VNet1toVNet5</span></span>
* <span data-ttu-id="7939f-165">ConnectionType：VNet2VNet</span><span class="sxs-lookup"><span data-stu-id="7939f-165">ConnectionType: VNet2VNet</span></span>

<span data-ttu-id="7939f-166">**TestVNet4 的值︰**</span><span class="sxs-lookup"><span data-stu-id="7939f-166">**Values for TestVNet4:**</span></span>

* <span data-ttu-id="7939f-167">VNet 名稱︰TestVNet4</span><span class="sxs-lookup"><span data-stu-id="7939f-167">VNet Name: TestVNet4</span></span>
* <span data-ttu-id="7939f-168">TestVNet2：10.41.0.0/16 和 10.42.0.0/16</span><span class="sxs-lookup"><span data-stu-id="7939f-168">TestVNet2: 10.41.0.0/16 & 10.42.0.0/16</span></span>
* <span data-ttu-id="7939f-169">FrontEnd：10.41.0.0/24</span><span class="sxs-lookup"><span data-stu-id="7939f-169">FrontEnd: 10.41.0.0/24</span></span>
* <span data-ttu-id="7939f-170">BackEnd：10.42.0.0/24</span><span class="sxs-lookup"><span data-stu-id="7939f-170">BackEnd: 10.42.0.0/24</span></span>
* <span data-ttu-id="7939f-171">GatewaySubnet：10.42.255.0/27</span><span class="sxs-lookup"><span data-stu-id="7939f-171">GatewaySubnet: 10.42.255.0/27</span></span>
* <span data-ttu-id="7939f-172">資源群組：TestRG4</span><span class="sxs-lookup"><span data-stu-id="7939f-172">Resource Group: TestRG4</span></span>
* <span data-ttu-id="7939f-173">位置：美國西部</span><span class="sxs-lookup"><span data-stu-id="7939f-173">Location: West US</span></span>
* <span data-ttu-id="7939f-174">GatewayName：VNet4GW</span><span class="sxs-lookup"><span data-stu-id="7939f-174">GatewayName: VNet4GW</span></span>
* <span data-ttu-id="7939f-175">公用 IP：VNet4GWIP</span><span class="sxs-lookup"><span data-stu-id="7939f-175">Public IP: VNet4GWIP</span></span>
* <span data-ttu-id="7939f-176">VPNType：RouteBased</span><span class="sxs-lookup"><span data-stu-id="7939f-176">VPNType: RouteBased</span></span>
* <span data-ttu-id="7939f-177">連線︰VNet4toVNet1</span><span class="sxs-lookup"><span data-stu-id="7939f-177">Connection: VNet4toVNet1</span></span>
* <span data-ttu-id="7939f-178">ConnectionType：VNet2VNet</span><span class="sxs-lookup"><span data-stu-id="7939f-178">ConnectionType: VNet2VNet</span></span>


### <span data-ttu-id="7939f-179"><a name="Step2"></a>步驟 2 - 建立及設定 TestVNet1</span><span class="sxs-lookup"><span data-stu-id="7939f-179"><a name="Step2"></a>Step 2 - Create and configure TestVNet1</span></span>

1. <span data-ttu-id="7939f-180">宣告變數。</span><span class="sxs-lookup"><span data-stu-id="7939f-180">Declare your variables.</span></span> <span data-ttu-id="7939f-181">下列範例會使用此練習中的值來宣告變數。</span><span class="sxs-lookup"><span data-stu-id="7939f-181">This example declares the variables using the values for this exercise.</span></span> <span data-ttu-id="7939f-182">在大部分的情況下，您應將值取代為您自己的值。</span><span class="sxs-lookup"><span data-stu-id="7939f-182">In most cases, you should replace the values with your own.</span></span> <span data-ttu-id="7939f-183">不過，若您執行這些步驟是為了熟悉此類型的設定，則可以使用這些變數。</span><span class="sxs-lookup"><span data-stu-id="7939f-183">However, you can use these variables if you are running through the steps to become familiar with this type of configuration.</span></span> <span data-ttu-id="7939f-184">視需要修改變數，然後將其複製並貼到您的 PowerShell 主控台中。</span><span class="sxs-lookup"><span data-stu-id="7939f-184">Modify the variables if needed, then copy and paste them into your PowerShell console.</span></span>

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

2. <span data-ttu-id="7939f-185">連線至您的帳戶。</span><span class="sxs-lookup"><span data-stu-id="7939f-185">Connect to your account.</span></span> <span data-ttu-id="7939f-186">使用下列範例來協助您連接：</span><span class="sxs-lookup"><span data-stu-id="7939f-186">Use the following example to help you connect:</span></span>

  ```powershell
  Login-AzureRmAccount
  ```

  <span data-ttu-id="7939f-187">檢查帳戶的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="7939f-187">Check the subscriptions for the account.</span></span>

  ```powershell
  Get-AzureRmSubscription
  ```

  <span data-ttu-id="7939f-188">指定您要使用的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="7939f-188">Specify the subscription that you want to use.</span></span>

  ```powershell
  Select-AzureRmSubscription -SubscriptionName $Sub1
  ```
3. <span data-ttu-id="7939f-189">建立新的資源群組。</span><span class="sxs-lookup"><span data-stu-id="7939f-189">Create a new resource group.</span></span>

  ```powershell
  New-AzureRmResourceGroup -Name $RG1 -Location $Location1
  ```
4. <span data-ttu-id="7939f-190">建立 TestVNet1 的子網路設定。</span><span class="sxs-lookup"><span data-stu-id="7939f-190">Create the subnet configurations for TestVNet1.</span></span> <span data-ttu-id="7939f-191">此範例會建立一個名為 TestVNet1 的虛擬網路和三個子網路：一個名為 GatewaySubnet、一個名為 FrontEnd，另一個名為 Backend。</span><span class="sxs-lookup"><span data-stu-id="7939f-191">This example creates a virtual network named TestVNet1 and three subnets, one called GatewaySubnet, one called FrontEnd, and one called Backend.</span></span> <span data-ttu-id="7939f-192">替代值時，務必一律將您的閘道子網路特定命名為 GatewaySubnet。</span><span class="sxs-lookup"><span data-stu-id="7939f-192">When substituting values, it's important that you always name your gateway subnet specifically GatewaySubnet.</span></span> <span data-ttu-id="7939f-193">如果您將其命名為其他名稱，閘道建立會失敗。</span><span class="sxs-lookup"><span data-stu-id="7939f-193">If you name it something else, your gateway creation fails.</span></span>

  <span data-ttu-id="7939f-194">下列範例會使用您先前設定的變數。</span><span class="sxs-lookup"><span data-stu-id="7939f-194">The following example uses the variables that you set earlier.</span></span> <span data-ttu-id="7939f-195">在此範例中，閘道子網路使用 /27。</span><span class="sxs-lookup"><span data-stu-id="7939f-195">In this example, the gateway subnet is using a /27.</span></span> <span data-ttu-id="7939f-196">雖然您可以建立小至 /29 的閘道子網路，我們建議您選取至少 /28 或 /27，建立包含更多位址的較大子網路。</span><span class="sxs-lookup"><span data-stu-id="7939f-196">While it is possible to create a gateway subnet as small as /29, we recommend that you create a larger subnet that includes more addresses by selecting at least /28 or /27.</span></span> <span data-ttu-id="7939f-197">這將允許足夠的位址，以容納您未來可能需要的其他組態。</span><span class="sxs-lookup"><span data-stu-id="7939f-197">This will allow for enough addresses to accommodate possible additional configurations that you may want in the future.</span></span>

  ```powershell
  $fesub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName1 -AddressPrefix $FESubPrefix1
  $besub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName1 -AddressPrefix $BESubPrefix1
  $gwsub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName1 -AddressPrefix $GWSubPrefix1
  ```
5. <span data-ttu-id="7939f-198">建立 TestVNet1。</span><span class="sxs-lookup"><span data-stu-id="7939f-198">Create TestVNet1.</span></span>

  ```powershell
  New-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1 `
  -Location $Location1 -AddressPrefix $VNetPrefix11,$VNetPrefix12 -Subnet $fesub1,$besub1,$gwsub1
  ```
6. <span data-ttu-id="7939f-199">要求一個公用 IP 位址，以配置給您將建立給 VNet 使用的閘道。</span><span class="sxs-lookup"><span data-stu-id="7939f-199">Request a public IP address to be allocated to the gateway you will create for your VNet.</span></span> <span data-ttu-id="7939f-200">請注意，AllocationMethod 是動態的。</span><span class="sxs-lookup"><span data-stu-id="7939f-200">Notice that the AllocationMethod is Dynamic.</span></span> <span data-ttu-id="7939f-201">您無法指定想要使用的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="7939f-201">You cannot specify the IP address that you want to use.</span></span> <span data-ttu-id="7939f-202">該 IP 位址會以動態方式配置給您的閘道。</span><span class="sxs-lookup"><span data-stu-id="7939f-202">It's dynamically allocated to your gateway.</span></span> 

  ```powershell
  $gwpip1 = New-AzureRmPublicIpAddress -Name $GWIPName1 -ResourceGroupName $RG1 `
  -Location $Location1 -AllocationMethod Dynamic
  ```
7. <span data-ttu-id="7939f-203">建立閘道組態。</span><span class="sxs-lookup"><span data-stu-id="7939f-203">Create the gateway configuration.</span></span> <span data-ttu-id="7939f-204">閘道器組態定義要使用的子網路和公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="7939f-204">The gateway configuration defines the subnet and the public IP address to use.</span></span> <span data-ttu-id="7939f-205">使用下列範例來建立閘道組態。</span><span class="sxs-lookup"><span data-stu-id="7939f-205">Use the example to create your gateway configuration.</span></span>

  ```powershell
  $vnet1 = Get-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1
  $subnet1 = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet1
  $gwipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName1 `
  -Subnet $subnet1 -PublicIpAddress $gwpip1
  ```
8. <span data-ttu-id="7939f-206">建立 TestVNet1 的閘道。</span><span class="sxs-lookup"><span data-stu-id="7939f-206">Create the gateway for TestVNet1.</span></span> <span data-ttu-id="7939f-207">在此步驟中，您會建立 TestVNet1 的虛擬網路閘道。</span><span class="sxs-lookup"><span data-stu-id="7939f-207">In this step, you create the virtual network gateway for your TestVNet1.</span></span> <span data-ttu-id="7939f-208">VNet 對 VNet 組態需要 RouteBased VpnType。</span><span class="sxs-lookup"><span data-stu-id="7939f-208">VNet-to-VNet configurations require a RouteBased VpnType.</span></span> <span data-ttu-id="7939f-209">建立閘道通常可能需要 45 分鐘或更久，視選取的閘道 SKU 而定。</span><span class="sxs-lookup"><span data-stu-id="7939f-209">Creating a gateway can often take 45 minutes or more, depending on the selected gateway SKU.</span></span>

  ```powershell
  New-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1 `
  -Location $Location1 -IpConfigurations $gwipconf1 -GatewayType Vpn `
  -VpnType RouteBased -GatewaySku VpnGw1
  ```

### <a name="step-3---create-and-configure-testvnet4"></a><span data-ttu-id="7939f-210">步驟 3 - 建立及設定 TestVNet4</span><span class="sxs-lookup"><span data-stu-id="7939f-210">Step 3 - Create and configure TestVNet4</span></span>

<span data-ttu-id="7939f-211">設定 TestVNet1 後，請建立 TestVNet4。</span><span class="sxs-lookup"><span data-stu-id="7939f-211">Once you've configured TestVNet1, create TestVNet4.</span></span> <span data-ttu-id="7939f-212">遵循下方步驟，視需要替換成您自己的值。</span><span class="sxs-lookup"><span data-stu-id="7939f-212">Follow the steps below, replacing the values with your own when needed.</span></span> <span data-ttu-id="7939f-213">此步驟可以在相同的 PowerShell 工作階段中完成，因為其位於相同的訂用帳戶中。</span><span class="sxs-lookup"><span data-stu-id="7939f-213">This step can be done within the same PowerShell session because it is in the same subscription.</span></span>

1. <span data-ttu-id="7939f-214">宣告變數。</span><span class="sxs-lookup"><span data-stu-id="7939f-214">Declare your variables.</span></span> <span data-ttu-id="7939f-215">請務必使用您想用於設定的值來取代該值。</span><span class="sxs-lookup"><span data-stu-id="7939f-215">Be sure to replace the values with the ones that you want to use for your configuration.</span></span>

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
2. <span data-ttu-id="7939f-216">建立新的資源群組。</span><span class="sxs-lookup"><span data-stu-id="7939f-216">Create a new resource group.</span></span>

  ```powershell
  New-AzureRmResourceGroup -Name $RG4 -Location $Location4
  ```
3. <span data-ttu-id="7939f-217">建立 TestVNet4 的子網路設定。</span><span class="sxs-lookup"><span data-stu-id="7939f-217">Create the subnet configurations for TestVNet4.</span></span>

  ```powershell
  $fesub4 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName4 -AddressPrefix $FESubPrefix4
  $besub4 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName4 -AddressPrefix $BESubPrefix4
  $gwsub4 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName4 -AddressPrefix $GWSubPrefix4
  ```
4. <span data-ttu-id="7939f-218">建立 TestVNet4。</span><span class="sxs-lookup"><span data-stu-id="7939f-218">Create TestVNet4.</span></span>

  ```powershell
  New-AzureRmVirtualNetwork -Name $VnetName4 -ResourceGroupName $RG4 `
  -Location $Location4 -AddressPrefix $VnetPrefix41,$VnetPrefix42 -Subnet $fesub4,$besub4,$gwsub4
  ```
5. <span data-ttu-id="7939f-219">要求公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="7939f-219">Request a public IP address.</span></span>

  ```powershell
  $gwpip4 = New-AzureRmPublicIpAddress -Name $GWIPName4 -ResourceGroupName $RG4 `
  -Location $Location4 -AllocationMethod Dynamic
  ```
6. <span data-ttu-id="7939f-220">建立閘道組態。</span><span class="sxs-lookup"><span data-stu-id="7939f-220">Create the gateway configuration.</span></span>

  ```powershell
  $vnet4 = Get-AzureRmVirtualNetwork -Name $VnetName4 -ResourceGroupName $RG4
  $subnet4 = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet4
  $gwipconf4 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName4 -Subnet $subnet4 -PublicIpAddress $gwpip4
  ```
7. <span data-ttu-id="7939f-221">建立 TestVNet4 閘道。</span><span class="sxs-lookup"><span data-stu-id="7939f-221">Create the TestVNet4 gateway.</span></span> <span data-ttu-id="7939f-222">建立閘道通常可能需要 45 分鐘或更久，視選取的閘道 SKU 而定。</span><span class="sxs-lookup"><span data-stu-id="7939f-222">Creating a gateway can often take 45 minutes or more, depending on the selected gateway SKU.</span></span>

  ```powershell
  New-AzureRmVirtualNetworkGateway -Name $GWName4 -ResourceGroupName $RG4 `
  -Location $Location4 -IpConfigurations $gwipconf4 -GatewayType Vpn `
  -VpnType RouteBased -GatewaySku VpnGw1
  ```

### <a name="step-4---create-the-connections"></a><span data-ttu-id="7939f-223">步驟 4 - 建立連線</span><span class="sxs-lookup"><span data-stu-id="7939f-223">Step 4 - Create the connections</span></span>

1. <span data-ttu-id="7939f-224">取得這兩個虛擬網路閘道。</span><span class="sxs-lookup"><span data-stu-id="7939f-224">Get both virtual network gateways.</span></span> <span data-ttu-id="7939f-225">如果這兩個閘道皆位於相同的訂用帳戶中 (如同其在此範例中)，您可以在相同的 PowerShell 工作階段中完成此步驟。</span><span class="sxs-lookup"><span data-stu-id="7939f-225">If both of the gateways are in the same subscription, as they are in the example, you can complete this step in the same PowerShell session.</span></span>

  ```powershell
  $vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
  $vnet4gw = Get-AzureRmVirtualNetworkGateway -Name $GWName4 -ResourceGroupName $RG4
  ```
2. <span data-ttu-id="7939f-226">建立 TestVNet1 至 TestVNet4 的連線。</span><span class="sxs-lookup"><span data-stu-id="7939f-226">Create the TestVNet1 to TestVNet4 connection.</span></span> <span data-ttu-id="7939f-227">在此步驟中，您會從 TestVNet1 建立連線至 TestVNet4。</span><span class="sxs-lookup"><span data-stu-id="7939f-227">In this step, you create the connection from TestVNet1 to TestVNet4.</span></span> <span data-ttu-id="7939f-228">您會看到範例使用共用金鑰。</span><span class="sxs-lookup"><span data-stu-id="7939f-228">You'll see a shared key referenced in the examples.</span></span> <span data-ttu-id="7939f-229">您可以使用自己的值，作為共用金鑰。</span><span class="sxs-lookup"><span data-stu-id="7939f-229">You can use your own values for the shared key.</span></span> <span data-ttu-id="7939f-230">但請務必確認該共用金鑰必須適用於這兩個連線。</span><span class="sxs-lookup"><span data-stu-id="7939f-230">The important thing is that the shared key must match for both connections.</span></span> <span data-ttu-id="7939f-231">建立連線可能需要一段時間才能完成。</span><span class="sxs-lookup"><span data-stu-id="7939f-231">Creating a connection can take a short while to complete.</span></span>

  ```powershell
  New-AzureRmVirtualNetworkGatewayConnection -Name $Connection14 -ResourceGroupName $RG1 `
  -VirtualNetworkGateway1 $vnet1gw -VirtualNetworkGateway2 $vnet4gw -Location $Location1 `
  -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3'
  ```
3. <span data-ttu-id="7939f-232">建立 TestVNet4 至 TestVNet1 的連線。</span><span class="sxs-lookup"><span data-stu-id="7939f-232">Create the TestVNet4 to TestVNet1 connection.</span></span> <span data-ttu-id="7939f-233">此步驟類似上面的步驟，只不過您是建立 TestVNet4 至 TestVNet1 的連線。</span><span class="sxs-lookup"><span data-stu-id="7939f-233">This step is similar to the one above, except you are creating the connection from TestVNet4 to TestVNet1.</span></span> <span data-ttu-id="7939f-234">請確認共用的金鑰相符。</span><span class="sxs-lookup"><span data-stu-id="7939f-234">Make sure the shared keys match.</span></span> <span data-ttu-id="7939f-235">稍候幾分鐘就會建立連線。</span><span class="sxs-lookup"><span data-stu-id="7939f-235">The connection will be established after a few minutes.</span></span>

  ```powershell
  New-AzureRmVirtualNetworkGatewayConnection -Name $Connection41 -ResourceGroupName $RG4 `
  -VirtualNetworkGateway1 $vnet4gw -VirtualNetworkGateway2 $vnet1gw -Location $Location4 `
  -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3'
  ```
4. <span data-ttu-id="7939f-236">確認您的連線。</span><span class="sxs-lookup"><span data-stu-id="7939f-236">Verify your connection.</span></span> <span data-ttu-id="7939f-237">請參閱 [如何驗證您的連線](#verify)一節。</span><span class="sxs-lookup"><span data-stu-id="7939f-237">See the section [How to verify your connection](#verify).</span></span>

## <span data-ttu-id="7939f-238"><a name="difsub"></a>如何連接不同訂用帳戶中的 VNet</span><span class="sxs-lookup"><span data-stu-id="7939f-238"><a name="difsub"></a>How to connect VNets that are in different subscriptions</span></span>

![v2v 圖表](./media/vpn-gateway-vnet-vnet-rm-ps/v2vdiffsub.png)

<span data-ttu-id="7939f-240">在此案例中，我們會連接 TestVNet1 和 TestVNet5。</span><span class="sxs-lookup"><span data-stu-id="7939f-240">In this scenario, we connect TestVNet1 and TestVNet5.</span></span> <span data-ttu-id="7939f-241">TestVNet1 和 TestVNet5 位於不同的訂用帳戶中。</span><span class="sxs-lookup"><span data-stu-id="7939f-241">TestVNet1 and TestVNet5 reside in a different subscription.</span></span> <span data-ttu-id="7939f-242">訂用帳戶不需與相同的 Active Directory 租用戶相關聯。</span><span class="sxs-lookup"><span data-stu-id="7939f-242">The subscriptions do not need to be associated with the same Active Directory tenant.</span></span> <span data-ttu-id="7939f-243">這些步驟與前一組步驟的差別在於，第二個訂用帳戶的內容中有些設定步驟需在不同的 PowerShell 工作階段中執行。</span><span class="sxs-lookup"><span data-stu-id="7939f-243">The difference between these steps and the previous set is that some of the configuration steps need to be performed in a separate PowerShell session in the context of the second subscription.</span></span> <span data-ttu-id="7939f-244">尤其是當兩個訂用帳戶分屬不同的組織時。</span><span class="sxs-lookup"><span data-stu-id="7939f-244">Especially when the two subscriptions belong to different organizations.</span></span>

### <a name="step-5---create-and-configure-testvnet1"></a><span data-ttu-id="7939f-245">步驟 5 - 建立及設定 TestVNet1</span><span class="sxs-lookup"><span data-stu-id="7939f-245">Step 5 - Create and configure TestVNet1</span></span>

<span data-ttu-id="7939f-246">您必須完成前一節的[步驟 1](#Step1) 和[步驟 2](#Step2)，以建立並設定 TestVNet1 和 TestVNet1 的 VPN 閘道。</span><span class="sxs-lookup"><span data-stu-id="7939f-246">You must complete [Step 1](#Step1) and [Step 2](#Step2) from the previous section to create and configure TestVNet1 and the VPN Gateway for TestVNet1.</span></span> <span data-ttu-id="7939f-247">在此設定中，您不需要建立前一節的 TestVNet4 ，雖然您若建立它，它就不與這些步驟發生衝突。</span><span class="sxs-lookup"><span data-stu-id="7939f-247">For this configuration, you are not required to create TestVNet4 from the previous section, although if you do create it, it will not conflict with these steps.</span></span> <span data-ttu-id="7939f-248">完成步驟 1 和步驟 2 後，繼續進行步驟 6 以建立 TestVNet5。</span><span class="sxs-lookup"><span data-stu-id="7939f-248">Once you complete Step 1 and Step 2, continue with Step 6 to create TestVNet5.</span></span> 

### <a name="step-6---verify-the-ip-address-ranges"></a><span data-ttu-id="7939f-249">步驟 6 - 驗證 IP 位址範圍</span><span class="sxs-lookup"><span data-stu-id="7939f-249">Step 6 - Verify the IP address ranges</span></span>

<span data-ttu-id="7939f-250">請務必確定新虛擬網路的 IP 位址空間 TestVNet5 不會與任何 VNet 範圍或區域網路閘道範圍重疊。</span><span class="sxs-lookup"><span data-stu-id="7939f-250">It is important to make sure that the IP address space of the new virtual network, TestVNet5, does not overlap with any of your VNet ranges or local network gateway ranges.</span></span> <span data-ttu-id="7939f-251">在此範例中，虛擬網路可能屬於不同的組織。</span><span class="sxs-lookup"><span data-stu-id="7939f-251">In this example, the virtual networks may belong to different organizations.</span></span> <span data-ttu-id="7939f-252">在這個練習中，您可以對 TestVNet5 使用下列的值：</span><span class="sxs-lookup"><span data-stu-id="7939f-252">For this exercise, you can use the following values for the TestVNet5:</span></span>

<span data-ttu-id="7939f-253">**TestVNet5 的值︰**</span><span class="sxs-lookup"><span data-stu-id="7939f-253">**Values for TestVNet5:**</span></span>

* <span data-ttu-id="7939f-254">VNet 名稱︰TestVNet5</span><span class="sxs-lookup"><span data-stu-id="7939f-254">VNet Name: TestVNet5</span></span>
* <span data-ttu-id="7939f-255">資源群組：TestRG5</span><span class="sxs-lookup"><span data-stu-id="7939f-255">Resource Group: TestRG5</span></span>
* <span data-ttu-id="7939f-256">位置：日本東部</span><span class="sxs-lookup"><span data-stu-id="7939f-256">Location: Japan East</span></span>
* <span data-ttu-id="7939f-257">TestVNet5：10.51.0.0/16 和 10.52.0.0/16</span><span class="sxs-lookup"><span data-stu-id="7939f-257">TestVNet5: 10.51.0.0/16 & 10.52.0.0/16</span></span>
* <span data-ttu-id="7939f-258">FrontEnd：10.51.0.0/24</span><span class="sxs-lookup"><span data-stu-id="7939f-258">FrontEnd: 10.51.0.0/24</span></span>
* <span data-ttu-id="7939f-259">BackEnd：10.52.0.0/24</span><span class="sxs-lookup"><span data-stu-id="7939f-259">BackEnd: 10.52.0.0/24</span></span>
* <span data-ttu-id="7939f-260">GatewaySubnet：10.52.255.0.0/27</span><span class="sxs-lookup"><span data-stu-id="7939f-260">GatewaySubnet: 10.52.255.0.0/27</span></span>
* <span data-ttu-id="7939f-261">GatewayName：VNet5GW</span><span class="sxs-lookup"><span data-stu-id="7939f-261">GatewayName: VNet5GW</span></span>
* <span data-ttu-id="7939f-262">公用 IP：VNet5GWIP</span><span class="sxs-lookup"><span data-stu-id="7939f-262">Public IP: VNet5GWIP</span></span>
* <span data-ttu-id="7939f-263">VPNType：RouteBased</span><span class="sxs-lookup"><span data-stu-id="7939f-263">VPNType: RouteBased</span></span>
* <span data-ttu-id="7939f-264">連線︰VNet5toVNet1</span><span class="sxs-lookup"><span data-stu-id="7939f-264">Connection: VNet5toVNet1</span></span>
* <span data-ttu-id="7939f-265">ConnectionType：VNet2VNet</span><span class="sxs-lookup"><span data-stu-id="7939f-265">ConnectionType: VNet2VNet</span></span>

### <a name="step-7---create-and-configure-testvnet5"></a><span data-ttu-id="7939f-266">步驟 7 - 建立及設定 TestVNet5</span><span class="sxs-lookup"><span data-stu-id="7939f-266">Step 7 - Create and configure TestVNet5</span></span>

<span data-ttu-id="7939f-267">在新訂用帳戶的內容中，必須完成這個步驟。</span><span class="sxs-lookup"><span data-stu-id="7939f-267">This step must be done in the context of the new subscription.</span></span> <span data-ttu-id="7939f-268">此部分可能會由不同組織中擁有訂用帳戶的系統管理員執行。</span><span class="sxs-lookup"><span data-stu-id="7939f-268">This part may be performed by the administrator in a different organization that owns the subscription.</span></span>

1. <span data-ttu-id="7939f-269">宣告變數。</span><span class="sxs-lookup"><span data-stu-id="7939f-269">Declare your variables.</span></span> <span data-ttu-id="7939f-270">請務必使用您想用於設定的值來取代該值。</span><span class="sxs-lookup"><span data-stu-id="7939f-270">Be sure to replace the values with the ones that you want to use for your configuration.</span></span>

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
2. <span data-ttu-id="7939f-271">連線到訂用帳戶 5。</span><span class="sxs-lookup"><span data-stu-id="7939f-271">Connect to subscription 5.</span></span> <span data-ttu-id="7939f-272">開啟 PowerShell 主控台並連接到您的帳戶。</span><span class="sxs-lookup"><span data-stu-id="7939f-272">Open your PowerShell console and connect to your account.</span></span> <span data-ttu-id="7939f-273">使用下列範例來協助您連接：</span><span class="sxs-lookup"><span data-stu-id="7939f-273">Use the following sample to help you connect:</span></span>

  ```powershell
  Login-AzureRmAccount
  ```

  <span data-ttu-id="7939f-274">檢查帳戶的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="7939f-274">Check the subscriptions for the account.</span></span>

  ```powershell
  Get-AzureRmSubscription
  ```

  <span data-ttu-id="7939f-275">指定您要使用的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="7939f-275">Specify the subscription that you want to use.</span></span>

  ```powershell
  Select-AzureRmSubscription -SubscriptionName $Sub5
  ```
3. <span data-ttu-id="7939f-276">建立新的資源群組。</span><span class="sxs-lookup"><span data-stu-id="7939f-276">Create a new resource group.</span></span>

  ```powershell
  New-AzureRmResourceGroup -Name $RG5 -Location $Location5
  ```
4. <span data-ttu-id="7939f-277">建立 TestVNet5 的子網路設定。</span><span class="sxs-lookup"><span data-stu-id="7939f-277">Create the subnet configurations for TestVNet5.</span></span>

  ```powershell
  $fesub5 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName5 -AddressPrefix $FESubPrefix5
  $besub5 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName5 -AddressPrefix $BESubPrefix5
  $gwsub5 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName5 -AddressPrefix $GWSubPrefix5
  ```
5. <span data-ttu-id="7939f-278">建立 TestVNet5。</span><span class="sxs-lookup"><span data-stu-id="7939f-278">Create TestVNet5.</span></span>

  ```powershell
  New-AzureRmVirtualNetwork -Name $VnetName5 -ResourceGroupName $RG5 -Location $Location5 `
  -AddressPrefix $VnetPrefix51,$VnetPrefix52 -Subnet $fesub5,$besub5,$gwsub5
  ```
6. <span data-ttu-id="7939f-279">要求公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="7939f-279">Request a public IP address.</span></span>

  ```powershell
  $gwpip5 = New-AzureRmPublicIpAddress -Name $GWIPName5 -ResourceGroupName $RG5 `
  -Location $Location5 -AllocationMethod Dynamic
  ```
7. <span data-ttu-id="7939f-280">建立閘道組態。</span><span class="sxs-lookup"><span data-stu-id="7939f-280">Create the gateway configuration.</span></span>

  ```powershell
  $vnet5 = Get-AzureRmVirtualNetwork -Name $VnetName5 -ResourceGroupName $RG5
  $subnet5  = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet5
  $gwipconf5 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName5 -Subnet $subnet5 -PublicIpAddress $gwpip5
  ```
8. <span data-ttu-id="7939f-281">建立 TestVNet5 閘道。</span><span class="sxs-lookup"><span data-stu-id="7939f-281">Create the TestVNet5 gateway.</span></span>

  ```powershell
  New-AzureRmVirtualNetworkGateway -Name $GWName5 -ResourceGroupName $RG5 -Location $Location5 `
  -IpConfigurations $gwipconf5 -GatewayType Vpn -VpnType RouteBased -GatewaySku VpnGw1
  ```

### <a name="step-8---create-the-connections"></a><span data-ttu-id="7939f-282">步驟 8 - 建立連線</span><span class="sxs-lookup"><span data-stu-id="7939f-282">Step 8 - Create the connections</span></span>

<span data-ttu-id="7939f-283">在此範例中，因為閘道會在不同的訂用帳戶中，所以我們已將此步驟分作兩個 PowerShell 工作階段，其標示為 [訂用帳戶 1] 和 [訂用帳戶 5]。</span><span class="sxs-lookup"><span data-stu-id="7939f-283">In this example, because the gateways are in the different subscriptions, we've split this step into two PowerShell sessions marked as [Subscription 1] and [Subscription 5].</span></span>

1. <span data-ttu-id="7939f-284">**[訂用帳戶 1]** 取得訂用帳戶 1 的虛擬網路閘道。</span><span class="sxs-lookup"><span data-stu-id="7939f-284">**[Subscription 1]** Get the virtual network gateway for Subscription 1.</span></span> <span data-ttu-id="7939f-285">先登入並連線至訂用帳戶 1，再執行下列範例︰</span><span class="sxs-lookup"><span data-stu-id="7939f-285">Log in and connect to Subscription 1 before running the following example:</span></span>

  ```powershell
  $vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
  ```

  <span data-ttu-id="7939f-286">複製下列項目的輸出，並透過電子郵件或其他方法將其傳送到訂用帳戶 5 的系統管理員。</span><span class="sxs-lookup"><span data-stu-id="7939f-286">Copy the output of the following elements and send these to the administrator of Subscription 5 via email or another method.</span></span>

  ```powershell
  $vnet1gw.Name
  $vnet1gw.Id
  ```

  <span data-ttu-id="7939f-287">這兩個元素的值會類似下列範例的輸出︰</span><span class="sxs-lookup"><span data-stu-id="7939f-287">These two elements will have values similar to the following example output:</span></span>

  ```
  PS D:\> $vnet1gw.Name
  VNet1GW
  PS D:\> $vnet1gw.Id
  /subscriptions/b636ca99-6f88-4df4-a7c3-2f8dc4545509/resourceGroupsTestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW
  ```
2. <span data-ttu-id="7939f-288">**[訂用帳戶 5]** 取得訂用帳戶 5 的虛擬網路閘道。</span><span class="sxs-lookup"><span data-stu-id="7939f-288">**[Subscription 5]** Get the virtual network gateway for Subscription 5.</span></span> <span data-ttu-id="7939f-289">先登入並連線至訂用帳戶 5，再執行下列範例︰</span><span class="sxs-lookup"><span data-stu-id="7939f-289">Log in and connect to Subscription 5 before running the following example:</span></span>

  ```powershell
  $vnet5gw = Get-AzureRmVirtualNetworkGateway -Name $GWName5 -ResourceGroupName $RG5
  ```

  <span data-ttu-id="7939f-290">複製下列項目的輸出，並透過電子郵件或其他方法將其傳送到訂用帳戶 1 的系統管理員。</span><span class="sxs-lookup"><span data-stu-id="7939f-290">Copy the output of the following elements and send these to the administrator of Subscription 1 via email or another method.</span></span>

  ```powershell
  $vnet5gw.Name
  $vnet5gw.Id
  ```

  <span data-ttu-id="7939f-291">這兩個元素的值會類似下列範例的輸出︰</span><span class="sxs-lookup"><span data-stu-id="7939f-291">These two elements will have values similar to the following example output:</span></span>

  ```
  PS C:\> $vnet5gw.Name
  VNet5GW
  PS C:\> $vnet5gw.Id
  /subscriptions/66c8e4f1-ecd6-47ed-9de7-7e530de23994/resourceGroups/TestRG5/providers/Microsoft.Network/virtualNetworkGateways/VNet5GW
  ```
3. <span data-ttu-id="7939f-292">**[訂用帳戶 1]** 建立 TestVNet1 至 TestVNet5 的連線。</span><span class="sxs-lookup"><span data-stu-id="7939f-292">**[Subscription 1]** Create the TestVNet1 to TestVNet5 connection.</span></span> <span data-ttu-id="7939f-293">在此步驟中，您會從 TestVNet1 建立連線至 TestVNet5。</span><span class="sxs-lookup"><span data-stu-id="7939f-293">In this step, you create the connection from TestVNet1 to TestVNet5.</span></span> <span data-ttu-id="7939f-294">此處的差別為直接取得 $vnet5gw，因為其位於不同的訂用帳戶中。</span><span class="sxs-lookup"><span data-stu-id="7939f-294">The difference here is that $vnet5gw cannot be obtained directly because it is in a different subscription.</span></span> <span data-ttu-id="7939f-295">您必須使用上述步驟中從訂用帳戶 1 通訊的值來建立新的 PowerShell 物件。</span><span class="sxs-lookup"><span data-stu-id="7939f-295">You will need to create a new PowerShell object with the values communicated from Subscription 1 in the steps above.</span></span> <span data-ttu-id="7939f-296">請使用下方的範例。</span><span class="sxs-lookup"><span data-stu-id="7939f-296">Use the example below.</span></span> <span data-ttu-id="7939f-297">以您自己的值來取代名稱、識別碼和共用金鑰。</span><span class="sxs-lookup"><span data-stu-id="7939f-297">Replace the Name, Id, and shared key with your own values.</span></span> <span data-ttu-id="7939f-298">但請務必確認該共用金鑰必須適用於這兩個連線。</span><span class="sxs-lookup"><span data-stu-id="7939f-298">The important thing is that the shared key must match for both connections.</span></span> <span data-ttu-id="7939f-299">建立連線可能需要一段時間才能完成。</span><span class="sxs-lookup"><span data-stu-id="7939f-299">Creating a connection can take a short while to complete.</span></span>

  <span data-ttu-id="7939f-300">先連線至訂用帳戶 1，再執行下列範例︰</span><span class="sxs-lookup"><span data-stu-id="7939f-300">Connect to Subscription 1 before running the following example:</span></span>

  ```powershell
  $vnet5gw = New-Object Microsoft.Azure.Commands.Network.Models.PSVirtualNetworkGateway
  $vnet5gw.Name = "VNet5GW"
  $vnet5gw.Id   = "/subscriptions/66c8e4f1-ecd6-47ed-9de7-7e530de23994/resourceGroups/TestRG5/providers/Microsoft.Network/virtualNetworkGateways/VNet5GW"
  $Connection15 = "VNet1toVNet5"
  New-AzureRmVirtualNetworkGatewayConnection -Name $Connection15 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -VirtualNetworkGateway2 $vnet5gw -Location $Location1 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3'
  ```
4. <span data-ttu-id="7939f-301">**[訂用帳戶 5]** 建立 TestVNet5 至 TestVNet1 的連線。</span><span class="sxs-lookup"><span data-stu-id="7939f-301">**[Subscription 5]** Create the TestVNet5 to TestVNet1 connection.</span></span> <span data-ttu-id="7939f-302">此步驟類似上面的步驟，只不過您是建立 TestVNet5 至 TestVNet1 的連線。</span><span class="sxs-lookup"><span data-stu-id="7939f-302">This step is similar to the one above, except you are creating the connection from TestVNet5 to TestVNet1.</span></span> <span data-ttu-id="7939f-303">針對基於從訂用帳戶 1 所取得的值來建立 PowerShell 物件，該程序也適用於此處。</span><span class="sxs-lookup"><span data-stu-id="7939f-303">The same process of creating a PowerShell object based on the values obtained from Subscription 1 applies here as well.</span></span> <span data-ttu-id="7939f-304">在此步驟中，請確認共用金鑰相符。</span><span class="sxs-lookup"><span data-stu-id="7939f-304">In this step, be sure that the shared keys match.</span></span>

  <span data-ttu-id="7939f-305">先連線至訂用帳戶 5，再執行下列範例︰</span><span class="sxs-lookup"><span data-stu-id="7939f-305">Connect to Subscription 5 before running the following example:</span></span>

  ```powershell
  $vnet1gw = New-Object Microsoft.Azure.Commands.Network.Models.PSVirtualNetworkGateway
  $vnet1gw.Name = "VNet1GW"
  $vnet1gw.Id = "/subscriptions/b636ca99-6f88-4df4-a7c3-2f8dc4545509/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW "
  New-AzureRmVirtualNetworkGatewayConnection -Name $Connection51 -ResourceGroupName $RG5 -VirtualNetworkGateway1 $vnet5gw -VirtualNetworkGateway2 $vnet1gw -Location $Location5 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3'
  ```

## <span data-ttu-id="7939f-306"><a name="verify"></a>驗證連線</span><span class="sxs-lookup"><span data-stu-id="7939f-306"><a name="verify"></a>How to verify a connection</span></span>

[!INCLUDE [vpn-gateway-no-nsg-include](../../includes/vpn-gateway-no-nsg-include.md)]

[!INCLUDE [verify connections powershell](../../includes/vpn-gateway-verify-connection-ps-rm-include.md)]

## <span data-ttu-id="7939f-307"><a name="faq"></a>VNet 對 VNet 常見問題集</span><span class="sxs-lookup"><span data-stu-id="7939f-307"><a name="faq"></a>VNet-to-VNet FAQ</span></span>

[!INCLUDE [vpn-gateway-vnet-vnet-faq](../../includes/vpn-gateway-vnet-vnet-faq-include.md)]

## <a name="next-steps"></a><span data-ttu-id="7939f-308">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7939f-308">Next steps</span></span>

* <span data-ttu-id="7939f-309">一旦完成您的連接，就可以將虛擬機器加入您的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="7939f-309">Once your connection is complete, you can add virtual machines to your virtual networks.</span></span> <span data-ttu-id="7939f-310">如需詳細資訊，請參閱 [虛擬機器文件](https://docs.microsoft.com/azure/#pivot=services&panel=Compute) 。</span><span class="sxs-lookup"><span data-stu-id="7939f-310">See the [Virtual Machines documentation](https://docs.microsoft.com/azure/#pivot=services&panel=Compute) for more information.</span></span>
* <span data-ttu-id="7939f-311">如需 BGP 的相關資訊，請參閱 [BGP 概觀](vpn-gateway-bgp-overview.md)和[如何設定 BGP](vpn-gateway-bgp-resource-manager-ps.md)。</span><span class="sxs-lookup"><span data-stu-id="7939f-311">For information about BGP, see the [BGP Overview](vpn-gateway-bgp-overview.md) and [How to configure BGP](vpn-gateway-bgp-resource-manager-ps.md).</span></span>