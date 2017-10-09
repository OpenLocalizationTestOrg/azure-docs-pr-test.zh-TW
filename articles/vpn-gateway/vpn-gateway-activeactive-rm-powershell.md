---
title: "設定 VPN 閘道的主動-主動 S2S VPN 連線：Azure Resource Manager: PowerShell | Microsoft Docs"
description: "本文將逐步引導您使用 Azure Resource Manager 和 PowerShell 來設定與 Azure VPN 閘道的主動-主動連線。"
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: 
tags: azure-resource-manager
ms.assetid: 238cd9b3-f1ce-4341-b18e-7390935604fa
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/16/2017
ms.author: yushwang
ms.openlocfilehash: 964eedc7698e42bf0e082f0105845f2a339daf57
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-active-active-s2s-vpn-connections-with-azure-vpn-gateways"></a><span data-ttu-id="d48bb-103">設定 Azure VPN 閘道的主動-主動 S2S VPN 連線</span><span class="sxs-lookup"><span data-stu-id="d48bb-103">Configure active-active S2S VPN connections with Azure VPN Gateways</span></span>

<span data-ttu-id="d48bb-104">這篇文章會引導您完成 hello 步驟 toocreate 主動-主動跨內部部署和使用 hello Resource Manager 部署模型和 PowerShell 的 VNet 對 VNet 連線。</span><span class="sxs-lookup"><span data-stu-id="d48bb-104">This article walks you through hello steps toocreate active-active cross-premises and VNet-to-VNet connections using hello Resource Manager deployment model and PowerShell.</span></span>

## <a name="about-highly-available-cross-premises-connections"></a><span data-ttu-id="d48bb-105">關於高可用性跨單位連線</span><span class="sxs-lookup"><span data-stu-id="d48bb-105">About Highly Available Cross-Premises Connections</span></span>
<span data-ttu-id="d48bb-106">tooachieve 高可用性的跨單位和 VNet 對 VNet 連線能力，您應該部署多個 VPN 閘道，並建立您的網路與 Azure 之間的多個平行連接。</span><span class="sxs-lookup"><span data-stu-id="d48bb-106">tooachieve high availability for cross-premises and VNet-to-VNet connectivity, you should deploy multiple VPN gateways and establish multiple parallel connections between your networks and Azure.</span></span> <span data-ttu-id="d48bb-107">如需連線能力選項和拓撲的概觀，請參閱 [高可用性跨單位和 VNet 對 VNet 連線能力](vpn-gateway-highlyavailable.md) 。</span><span class="sxs-lookup"><span data-stu-id="d48bb-107">Please see [Highly Available Cross-Premises and VNet-to-VNet Connectivity](vpn-gateway-highlyavailable.md) for an overview of connectivity options and topology.</span></span>

<span data-ttu-id="d48bb-108">本文章提供 hello 指示 tooset 主動-主動設定跨單位 VPN 連線和兩個虛擬網路之間的主動-主動連線：</span><span class="sxs-lookup"><span data-stu-id="d48bb-108">This article provides hello instructions tooset up an active-active cross-premises VPN connection, and active-active connection between two virtual networks:</span></span>

* [<span data-ttu-id="d48bb-109">第 1 部分 - 建立 Azure VPN 閘道並將它設定為主動-主動模式</span><span class="sxs-lookup"><span data-stu-id="d48bb-109">Part 1 - Create and configure your Azure VPN gateway in active-active mode</span></span>](#aagateway)
* [<span data-ttu-id="d48bb-110">第 2 部分 - 建立主動-主動跨單位連線</span><span class="sxs-lookup"><span data-stu-id="d48bb-110">Part 2 - Establish active-active cross-premises connections</span></span>](#aacrossprem)
* [<span data-ttu-id="d48bb-111">第 3 部分 - 建立主動-主動 VNet 對 VNet 連線</span><span class="sxs-lookup"><span data-stu-id="d48bb-111">Part 3 - Establish active-active VNet-to-VNet connections</span></span>](#aav2v)
* [<span data-ttu-id="d48bb-112">第 4 部分 - 更新主動-主動和作用中-待命之間的現有閘道</span><span class="sxs-lookup"><span data-stu-id="d48bb-112">Part 4 - Update existing gateway between active-active and active-standby</span></span>](#aaupdate)

<span data-ttu-id="d48bb-113">您可以結合這些一起 toobuild 符合您需求的更複雜、 高可用性的網路拓撲。</span><span class="sxs-lookup"><span data-stu-id="d48bb-113">You can combine these together toobuild a more complex, highly available network topology that meets your needs.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d48bb-114">請注意該 hello 主動 / 主動模式會使用下列 Sku 的唯一 hello:</span><span class="sxs-lookup"><span data-stu-id="d48bb-114">Please note that hello active-active mode uses only hello following SKUs:</span></span> 
  * <span data-ttu-id="d48bb-115">VpnGw1、VpnGw2、VpnGw3</span><span class="sxs-lookup"><span data-stu-id="d48bb-115">VpnGw1, VpnGw2, VpnGw3</span></span>
  * <span data-ttu-id="d48bb-116">HighPerformance (對於舊版 SKU)</span><span class="sxs-lookup"><span data-stu-id="d48bb-116">HighPerformance (for old legacy SKUs)</span></span>
> 
> 

## <span data-ttu-id="d48bb-117"><a name ="aagateway"></a>第 1 部分 - 建立並設定主動-主動 VPN 閘道</span><span class="sxs-lookup"><span data-stu-id="d48bb-117"><a name ="aagateway"></a>Part 1 - Create and configure active-active VPN gateways</span></span>
<span data-ttu-id="d48bb-118">hello 下列步驟將在主動 / 主動模式中設定 Azure VPN 閘道。</span><span class="sxs-lookup"><span data-stu-id="d48bb-118">hello following steps will configure your Azure VPN gateway in active-active modes.</span></span> <span data-ttu-id="d48bb-119">hello hello 主動-主動和作用中-待命閘道之間的主要差異：</span><span class="sxs-lookup"><span data-stu-id="d48bb-119">hello key differences between hello active-active and active-standby gateways:</span></span>

* <span data-ttu-id="d48bb-120">您需要兩個公用 IP 位址與 toocreate 兩個閘道 IP 設定</span><span class="sxs-lookup"><span data-stu-id="d48bb-120">You need toocreate two Gateway IP configurations with two public IP addresses</span></span>
* <span data-ttu-id="d48bb-121">您需要設定 hello EnableActiveActiveFeature 旗標</span><span class="sxs-lookup"><span data-stu-id="d48bb-121">You need set hello EnableActiveActiveFeature flag</span></span>
* <span data-ttu-id="d48bb-122">hello 閘道 SKU 必須 VpnGw1、 VpnGw2、 VpnGw3 或高效能的分散式 (舊版 SKU)。</span><span class="sxs-lookup"><span data-stu-id="d48bb-122">hello gateway SKU must be VpnGw1, VpnGw2, VpnGw3, or HighPerformance (legacy SKU).</span></span>

<span data-ttu-id="d48bb-123">hello 其他屬性會 hello 與 hello 非主動-主動閘道相同。</span><span class="sxs-lookup"><span data-stu-id="d48bb-123">hello other properties are hello same as hello non-active-active gateways.</span></span> 

### <a name="before-you-begin"></a><span data-ttu-id="d48bb-124">開始之前</span><span class="sxs-lookup"><span data-stu-id="d48bb-124">Before you begin</span></span>
* <span data-ttu-id="d48bb-125">請確認您有 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="d48bb-125">Verify that you have an Azure subscription.</span></span> <span data-ttu-id="d48bb-126">如果您還沒有 Azure 訂用帳戶，則可以啟用 [MSDN 訂戶權益](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/)或註冊[免費帳戶](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="d48bb-126">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free account](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="d48bb-127">您將需要 tooinstall hello Azure 資源管理員 PowerShell cmdlet。</span><span class="sxs-lookup"><span data-stu-id="d48bb-127">You'll need tooinstall hello Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="d48bb-128">請參閱[Azure PowerShell 概觀](/powershell/azure/overview)如需安裝 hello PowerShell cmdlet 的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="d48bb-128">See [Overview of Azure PowerShell](/powershell/azure/overview) for more information about installing hello PowerShell cmdlets.</span></span>

### <a name="step-1---create-and-configure-vnet1"></a><span data-ttu-id="d48bb-129">步驟 1 - 建立及設定 VNet1</span><span class="sxs-lookup"><span data-stu-id="d48bb-129">Step 1 - Create and configure VNet1</span></span>
#### <a name="1-declare-your-variables"></a><span data-ttu-id="d48bb-130">1.宣告變數</span><span class="sxs-lookup"><span data-stu-id="d48bb-130">1. Declare your variables</span></span>
<span data-ttu-id="d48bb-131">對於此練習，我們一開始先宣告我們的變數。</span><span class="sxs-lookup"><span data-stu-id="d48bb-131">For this exercise, we'll start by declaring our variables.</span></span> <span data-ttu-id="d48bb-132">下列的 hello 範例宣告 hello 針對此練習使用 hello 值的變數。</span><span class="sxs-lookup"><span data-stu-id="d48bb-132">hello example below declares hello variables using hello values for this exercise.</span></span> <span data-ttu-id="d48bb-133">設定用於生產環境時，請以您自己是確定 tooreplace hello 值。</span><span class="sxs-lookup"><span data-stu-id="d48bb-133">Be sure tooreplace hello values with your own when configuring for production.</span></span> <span data-ttu-id="d48bb-134">如果您正在透過 hello 步驟 toobecome 熟悉這種設定，您可以使用這些變數。</span><span class="sxs-lookup"><span data-stu-id="d48bb-134">You can use these variables if you are running through hello steps toobecome familiar with this type of configuration.</span></span> <span data-ttu-id="d48bb-135">修改 hello 變數然後複製並貼到您的 PowerShell 主控台。</span><span class="sxs-lookup"><span data-stu-id="d48bb-135">Modify hello variables, and then copy and paste into your PowerShell console.</span></span>

```powershell
$Sub1 = "Ross"
$RG1 = "TestAARG1"
$Location1 = "West US"
$VNetName1 = "TestVNet1"
$FESubName1 = "FrontEnd"
$BESubName1 = "Backend"
$GWSubName1 = "GatewaySubnet"
$VNetPrefix11 = "10.11.0.0/16"
$VNetPrefix12 = "10.12.0.0/16"
$FESubPrefix1 = "10.11.0.0/24"
$BESubPrefix1 = "10.12.0.0/24"
$GWSubPrefix1 = "10.12.255.0/27"
$VNet1ASN = 65010
$DNS1 = "8.8.8.8"
$GWName1 = "VNet1GW"
$GW1IPName1 = "VNet1GWIP1"
$GW1IPName2 = "VNet1GWIP2"
$GW1IPconf1 = "gw1ipconf1"
$GW1IPconf2 = "gw1ipconf2"
$Connection12 = "VNet1toVNet2"
$Connection151 = "VNet1toSite5_1"
$Connection152 = "VNet1toSite5_2"
```

#### <a name="2-connect-tooyour-subscription-and-create-a-new-resource-group"></a><span data-ttu-id="d48bb-136">2.連接 tooyour 訂用帳戶，並建立新的資源群組</span><span class="sxs-lookup"><span data-stu-id="d48bb-136">2. Connect tooyour subscription and create a new resource group</span></span>
<span data-ttu-id="d48bb-137">請確定切換 tooPowerShell 模式 toouse hello 資源管理員 cmdlet。</span><span class="sxs-lookup"><span data-stu-id="d48bb-137">Make sure you switch tooPowerShell mode toouse hello Resource Manager cmdlets.</span></span> <span data-ttu-id="d48bb-138">如需詳細資訊，請參閱 [搭配使用 Windows PowerShell 與 Resource Manager](../powershell-azure-resource-manager.md)。</span><span class="sxs-lookup"><span data-stu-id="d48bb-138">For more information, see [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

<span data-ttu-id="d48bb-139">開啟 PowerShell 主控台並連接 tooyour 帳戶。</span><span class="sxs-lookup"><span data-stu-id="d48bb-139">Open your PowerShell console and connect tooyour account.</span></span> <span data-ttu-id="d48bb-140">使用下列範例 toohelp 您連接的 hello:</span><span class="sxs-lookup"><span data-stu-id="d48bb-140">Use hello following sample toohelp you connect:</span></span>

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionName $Sub1
New-AzureRmResourceGroup -Name $RG1 -Location $Location1
```

#### <a name="3-create-testvnet1"></a><span data-ttu-id="d48bb-141">3.建立 TestVNet1</span><span class="sxs-lookup"><span data-stu-id="d48bb-141">3. Create TestVNet1</span></span>
<span data-ttu-id="d48bb-142">hello 下面範例會建立名為 TestVNet1 三個子網路，一個稱為的 GatewaySubnet、 一個稱為的前端和一個被呼叫後端的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="d48bb-142">hello sample below creates a virtual network named TestVNet1 and three subnets, one called GatewaySubnet, one called FrontEnd, and one called Backend.</span></span> <span data-ttu-id="d48bb-143">替代值時，務必一律將您的閘道子網路特定命名為 GatewaySubnet。</span><span class="sxs-lookup"><span data-stu-id="d48bb-143">When substituting values, it's important that you always name your gateway subnet specifically GatewaySubnet.</span></span> <span data-ttu-id="d48bb-144">如果您將其命名為其他名稱，閘道將會建立失敗。</span><span class="sxs-lookup"><span data-stu-id="d48bb-144">If you name it something else, your gateway creation will fail.</span></span>

```powershell
$fesub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName1 -AddressPrefix $FESubPrefix1
$besub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName1 -AddressPrefix $BESubPrefix1
$gwsub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName1 -AddressPrefix $GWSubPrefix1

New-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1 -Location $Location1 -AddressPrefix $VNetPrefix11,$VNetPrefix12 -Subnet $fesub1,$besub1,$gwsub1
```

### <a name="step-2---create-hello-vpn-gateway-for-testvnet1-with-active-active-mode"></a><span data-ttu-id="d48bb-145">步驟 2-建立 TestVNet1 hello VPN 閘道，並主動 / 主動模式</span><span class="sxs-lookup"><span data-stu-id="d48bb-145">Step 2 - Create hello VPN gateway for TestVNet1 with active-active mode</span></span>
#### <a name="1-create-hello-public-ip-addresses-and-gateway-ip-configurations"></a><span data-ttu-id="d48bb-146">1.建立 hello 公用 IP 位址和閘道 IP 組態</span><span class="sxs-lookup"><span data-stu-id="d48bb-146">1. Create hello public IP addresses and gateway IP configurations</span></span>
<span data-ttu-id="d48bb-147">要求兩個公用 IP 位址 toobe 配置的 toohello 閘道您將建立您的 VNet。</span><span class="sxs-lookup"><span data-stu-id="d48bb-147">Request two public IP addresses toobe allocated toohello gateway you will create for your VNet.</span></span> <span data-ttu-id="d48bb-148">您也會定義 hello 子網路和 IP 所需的設定。</span><span class="sxs-lookup"><span data-stu-id="d48bb-148">You'll also define hello subnet and IP configurations required.</span></span>

```powershell
$gw1pip1 = New-AzureRmPublicIpAddress -Name $GW1IPName1 -ResourceGroupName $RG1 -Location $Location1 -AllocationMethod Dynamic
$gw1pip2 = New-AzureRmPublicIpAddress -Name $GW1IPName2 -ResourceGroupName $RG1 -Location $Location1 -AllocationMethod Dynamic

$vnet1 = Get-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1
$subnet1 = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet1
$gw1ipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GW1IPconf1 -Subnet $subnet1 -PublicIpAddress $gw1pip1
$gw1ipconf2 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GW1IPconf2 -Subnet $subnet1 -PublicIpAddress $gw1pip2
```

#### <a name="2-create-hello-vpn-gateway-with-active-active-configuration"></a><span data-ttu-id="d48bb-149">2.主動-主動組態建立 hello VPN 閘道</span><span class="sxs-lookup"><span data-stu-id="d48bb-149">2. Create hello VPN gateway with active-active configuration</span></span>
<span data-ttu-id="d48bb-150">建立 TestVNet1 hello 虛擬網路閘道。</span><span class="sxs-lookup"><span data-stu-id="d48bb-150">Create hello virtual network gateway for TestVNet1.</span></span> <span data-ttu-id="d48bb-151">請注意，兩個 GatewayIpConfig 項目，而且 hello EnableActiveActiveFeature 旗標設定。</span><span class="sxs-lookup"><span data-stu-id="d48bb-151">Note that there are two GatewayIpConfig entries, and hello EnableActiveActiveFeature flag is set.</span></span> <span data-ttu-id="d48bb-152">建立閘道可能需要一段 （45 分鐘或更多 toocomplete）。</span><span class="sxs-lookup"><span data-stu-id="d48bb-152">Creating a gateway can take a while (45 minutes or more toocomplete).</span></span>

```powershell
New-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1 -Location $Location1 -IpConfigurations $gw1ipconf1,$gw1ipconf2 -GatewayType Vpn -VpnType RouteBased -GatewaySku VpnGw1 -Asn $VNet1ASN -EnableActiveActiveFeature -Debug
```

#### <a name="3-obtain-hello-gateway-public-ip-addresses-and-hello-bgp-peer-ip-address"></a><span data-ttu-id="d48bb-153">3.取得 hello 閘道的公用 IP 位址和 hello BGP 對等 IP 位址</span><span class="sxs-lookup"><span data-stu-id="d48bb-153">3. Obtain hello gateway public IP addresses and hello BGP Peer IP address</span></span>
<span data-ttu-id="d48bb-154">一旦建立 hello 閘道之後，您必須上 hello Azure VPN 閘道的 tooobtain hello BGP 對等 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="d48bb-154">Once hello gateway is created, you will need tooobtain hello BGP Peer IP address on hello Azure VPN Gateway.</span></span> <span data-ttu-id="d48bb-155">這個位址會是需要的 tooconfigure hello Azure VPN 閘道的 BGP 對等內部部署 VPN 裝置為。</span><span class="sxs-lookup"><span data-stu-id="d48bb-155">This address is needed tooconfigure hello Azure VPN Gateway as a BGP Peer for your on-premises VPN devices.</span></span>

```powershell
$gw1pip1 = Get-AzureRmPublicIpAddress -Name $GW1IPName1 -ResourceGroupName $RG1
$gw1pip2 = Get-AzureRmPublicIpAddress -Name $GW1IPName2 -ResourceGroupName $RG1
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
```

<span data-ttu-id="d48bb-156">使用下列 cmdlet tooshow hello 兩個公用 IP 位址配置給您的 VPN 閘道，以及其對應的 BGP 對等 IP 位址，每個閘道執行個體的 hello:</span><span class="sxs-lookup"><span data-stu-id="d48bb-156">Use hello following cmdlets tooshow hello two public IP addresses allocated for your VPN gateway, and their corresponding BGP Peer IP addresses for each gateway instance:</span></span>

```powershell

    PS D:\> $gw1pip1.IpAddress
    40.112.190.5

    PS D:\> $gw1pip2.IpAddress
    138.91.156.129

    PS D:\> $vnet1gw.BgpSettingsText
    {
      "Asn": 65010,
      "BgpPeeringAddress": "10.12.255.4,10.12.255.5",
      "PeerWeight": 0
    }
```

<span data-ttu-id="d48bb-157">hello hello 公用 IP 位址和順序的 hello 閘道器執行個體對應的 BGP 對等互連位址的 hello hello 相同。</span><span class="sxs-lookup"><span data-stu-id="d48bb-157">hello order of hello public IP addresses for hello gateway instances and hello corresponding BGP Peering Addresses are hello same.</span></span> <span data-ttu-id="d48bb-158">在此範例中，hello 閘道具有公用 IP 的 40.112.190.5 VM 將會使用 10.12.255.4 做為其 BGP 對等互連位址，而 138.91.156.129 hello 閘道會使用 10.12.255.5。</span><span class="sxs-lookup"><span data-stu-id="d48bb-158">In this example, hello gateway VM with public IP of 40.112.190.5 will use 10.12.255.4 as its BGP Peering Address, and hello gateway with 138.91.156.129 will use 10.12.255.5.</span></span> <span data-ttu-id="d48bb-159">當您設定您的內部連線 toohello 主動-主動閘道的 VPN 裝置時需要此資訊。</span><span class="sxs-lookup"><span data-stu-id="d48bb-159">This information is needed when you set up your on premises VPN devices connecting toohello active-active gateway.</span></span> <span data-ttu-id="d48bb-160">具有所有位址的 hello 圖表下方顯示 hello 閘道：</span><span class="sxs-lookup"><span data-stu-id="d48bb-160">hello gateway is shown in hello diagram below with all addresses:</span></span>

![主動-主動閘道](./media/vpn-gateway-activeactive-rm-powershell/active-active-gw.png)

<span data-ttu-id="d48bb-162">一旦建立 hello 閘道之後，您可以使用此閘道 tooestablish 主動-主動跨內部部署或 VNet 對 VNet 連線。</span><span class="sxs-lookup"><span data-stu-id="d48bb-162">Once hello gateway is created, you can use this gateway tooestablish active-active cross-premises or VNet-to-VNet connection.</span></span> <span data-ttu-id="d48bb-163">hello 下列各節將逐步引導 hello 步驟 toocomplete hello 練習。</span><span class="sxs-lookup"><span data-stu-id="d48bb-163">hello following sections will walk through hello steps toocomplete hello exercise.</span></span>

## <span data-ttu-id="d48bb-164"><a name ="aacrossprem"></a>第 2 部分 - 建立主動-主動跨單位連線</span><span class="sxs-lookup"><span data-stu-id="d48bb-164"><a name ="aacrossprem"></a>Part 2 - Establish an active-active cross-premises connection</span></span>
<span data-ttu-id="d48bb-165">您需要 toocreate 本機網路閘道 toorepresent tooestablish 跨單位連線，在內部部署 VPN 裝置，並與 hello 本機網路閘道連線 tooconnect hello Azure VPN 閘道。</span><span class="sxs-lookup"><span data-stu-id="d48bb-165">tooestablish a cross-premises connection, you need toocreate a Local Network Gateway toorepresent your on-premises VPN device, and a Connection tooconnect hello Azure VPN gateway with hello local network gateway.</span></span> <span data-ttu-id="d48bb-166">在此範例中，hello Azure VPN 閘道為主動 / 主動模式。</span><span class="sxs-lookup"><span data-stu-id="d48bb-166">In this example, hello Azure VPN gateway is in active-active mode.</span></span> <span data-ttu-id="d48bb-167">如此一來，即使有一個內部部署 VPN 裝置 （區域網路閘道） 和一個連接資源，這兩個 Azure VPN 閘道器執行個體將會建立 S2S VPN 通道與 hello 在內部部署裝置。</span><span class="sxs-lookup"><span data-stu-id="d48bb-167">As a result, even though there is only one on-premises VPN device (local network gateway) and one connection resource, both Azure VPN gateway instances will establish S2S VPN tunnels with hello on-premises device.</span></span>

<span data-ttu-id="d48bb-168">在繼續之前，請確定您已完成本練習的 [第 1 部分](#aagateway) 。</span><span class="sxs-lookup"><span data-stu-id="d48bb-168">Before proceeding, please make sure you have completed [Part 1](#aagateway) of this exercise.</span></span>

### <a name="step-1---create-and-configure-hello-local-network-gateway"></a><span data-ttu-id="d48bb-169">步驟 1-建立和設定 hello 區域網路閘道</span><span class="sxs-lookup"><span data-stu-id="d48bb-169">Step 1 - Create and configure hello local network gateway</span></span>
#### <a name="1-declare-your-variables"></a><span data-ttu-id="d48bb-170">1.宣告變數</span><span class="sxs-lookup"><span data-stu-id="d48bb-170">1. Declare your variables</span></span>
<span data-ttu-id="d48bb-171">這個練習中，將會繼續 toobuild hello 組態 hello 圖所示。</span><span class="sxs-lookup"><span data-stu-id="d48bb-171">This exercise will continue toobuild hello configuration shown in hello diagram.</span></span> <span data-ttu-id="d48bb-172">為確定 tooreplace 以 hello 的 hello 值的 toouse 您的組態。</span><span class="sxs-lookup"><span data-stu-id="d48bb-172">Be sure tooreplace hello values with hello ones that you want toouse for your configuration.</span></span>

```powershell
$RG5 = "TestAARG5"
$Location5 = "West US"
$LNGName51 = "Site5_1"
$LNGPrefix51 = "10.52.255.253/32"
$LNGIP51 = "131.107.72.22"
$LNGASN5 = 65050
$BGPPeerIP51 = "10.52.255.253"
```

<span data-ttu-id="d48bb-173">幾個事項 toonote 有關 hello 本機網路閘道參數：</span><span class="sxs-lookup"><span data-stu-id="d48bb-173">A couple of things toonote regarding hello local network gateway parameters:</span></span>

* <span data-ttu-id="d48bb-174">hello 區域網路閘道可以是 hello 相同或不同的位置和資源群組為 hello VPN 閘道。</span><span class="sxs-lookup"><span data-stu-id="d48bb-174">hello local network gateway can be in hello same or different location and resource group as hello VPN gateway.</span></span> <span data-ttu-id="d48bb-175">這個範例會顯示它們在不同的資源群組，但在 hello 相同的 Azure 位置。</span><span class="sxs-lookup"><span data-stu-id="d48bb-175">This example shows them in different resource groups but in hello same Azure location.</span></span>
* <span data-ttu-id="d48bb-176">如果只有一個在內部部署 VPN 裝置如上所示，hello 主動-主動連線可使用或不 BGP 通訊協定。</span><span class="sxs-lookup"><span data-stu-id="d48bb-176">If there is only one on-premises VPN device as shown above, hello active-active connection can work with or without BGP protocol.</span></span> <span data-ttu-id="d48bb-177">這個範例會使用 BGP hello 跨單位連線。</span><span class="sxs-lookup"><span data-stu-id="d48bb-177">This example uses BGP for hello cross-premises connection.</span></span>
* <span data-ttu-id="d48bb-178">如果已啟用 BGP，您需要 toodeclare hello 本機網路閘道的 hello 前置詞是 hello 您 BGP 對等 IP 位址的 VPN 裝置上的主機位址。</span><span class="sxs-lookup"><span data-stu-id="d48bb-178">If BGP is enabled, hello prefix you need toodeclare for hello local network gateway is hello host address of your BGP Peer IP address on your VPN device.</span></span> <span data-ttu-id="d48bb-179">在此情況下是 "10.52.255.253/32" 的前置詞 /32。</span><span class="sxs-lookup"><span data-stu-id="d48bb-179">In this case, it's a /32 prefix of "10.52.255.253/32".</span></span>
* <span data-ttu-id="d48bb-180">提醒您，您必須在內部部署網路與 Azure VNet 之間使用不同的 BGP ASN。</span><span class="sxs-lookup"><span data-stu-id="d48bb-180">As a reminder, you must use different BGP ASNs between your on-premises networks and Azure VNet.</span></span> <span data-ttu-id="d48bb-181">如果它們是 hello 相同，則需要 toochange VNet ASN 在內部部署 VPN 裝置已使用 hello ASN toopeer 與其他 BGP 芳鄰。</span><span class="sxs-lookup"><span data-stu-id="d48bb-181">If they are hello same, you need toochange your VNet ASN if your on-premises VPN device already uses hello ASN toopeer with other BGP neighbors.</span></span>

#### <a name="2-create-hello-local-network-gateway-for-site5"></a><span data-ttu-id="d48bb-182">2.建立 Site5 hello 區域網路閘道</span><span class="sxs-lookup"><span data-stu-id="d48bb-182">2. Create hello local network gateway for Site5</span></span>
<span data-ttu-id="d48bb-183">您繼續之前，請先確認您仍連線的 tooSubscription 1。</span><span class="sxs-lookup"><span data-stu-id="d48bb-183">Before you continue, please make sure you are still connected tooSubscription 1.</span></span> <span data-ttu-id="d48bb-184">如果尚未建立，請建立 hello 資源群組。</span><span class="sxs-lookup"><span data-stu-id="d48bb-184">Create hello resource group if it is not yet created.</span></span>

```powershell
New-AzureRmResourceGroup -Name $RG5 -Location $Location5
New-AzureRmLocalNetworkGateway -Name $LNGName51 -ResourceGroupName $RG5 -Location $Location5 -GatewayIpAddress $LNGIP51 -AddressPrefix $LNGPrefix51 -Asn $LNGASN5 -BgpPeeringAddress $BGPPeerIP51
```

### <a name="step-2---connect-hello-vnet-gateway-and-local-network-gateway"></a><span data-ttu-id="d48bb-185">步驟 2-連接 hello VNet 閘道與區域網路閘道</span><span class="sxs-lookup"><span data-stu-id="d48bb-185">Step 2 - Connect hello VNet gateway and local network gateway</span></span>
#### <a name="1-get-hello-two-gateways"></a><span data-ttu-id="d48bb-186">1.取得 hello 這兩個閘道</span><span class="sxs-lookup"><span data-stu-id="d48bb-186">1. Get hello two gateways</span></span>

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$lng5gw1 = Get-AzureRmLocalNetworkGateway  -Name $LNGName51 -ResourceGroupName $RG5
```

#### <a name="2-create-hello-testvnet1-toosite5-connection"></a><span data-ttu-id="d48bb-187">2.建立 hello TestVNet1 tooSite5 連線</span><span class="sxs-lookup"><span data-stu-id="d48bb-187">2. Create hello TestVNet1 tooSite5 connection</span></span>
<span data-ttu-id="d48bb-188">在此步驟中，您將建立 hello 連接從 TestVNet1 tooSite5_1 與設定得 「 EnableBGP"$True。</span><span class="sxs-lookup"><span data-stu-id="d48bb-188">In this step, you will create hello connection from TestVNet1 tooSite5_1 with "EnableBGP" set too$True.</span></span>

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name $Connection151 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng5gw1 -Location $Location1 -ConnectionType IPsec -SharedKey 'AzureA1b2C3' -EnableBGP True
```

#### <a name="3-vpn-and-bgp-parameters-for-your-on-premises-vpn-device"></a><span data-ttu-id="d48bb-189">3.內部部署 VPN 裝置的 VPN 和 BGP 參數</span><span class="sxs-lookup"><span data-stu-id="d48bb-189">3. VPN and BGP parameters for your on-premises VPN device</span></span>
<span data-ttu-id="d48bb-190">hello 以下範例列出您將針對此練習在內部部署 VPN 裝置 hello BGP 設定區段在輸入的 hello 參數：</span><span class="sxs-lookup"><span data-stu-id="d48bb-190">hello example below lists hello parameters you will enter into hello BGP configuration section on your on-premises VPN device for this exercise:</span></span>

    - <span data-ttu-id="d48bb-191">Site5 ASN            : 65050</span><span class="sxs-lookup"><span data-stu-id="d48bb-191">Site5 ASN            : 65050</span></span>
    - <span data-ttu-id="d48bb-192">Site5 BGP IP         : 10.52.255.253</span><span class="sxs-lookup"><span data-stu-id="d48bb-192">Site5 BGP IP         : 10.52.255.253</span></span>
    - <span data-ttu-id="d48bb-193">前置詞 tooannounce: （例如） 10.51.0.0/16 和 10.52.0.0/16</span><span class="sxs-lookup"><span data-stu-id="d48bb-193">Prefixes tooannounce : (for example) 10.51.0.0/16 and 10.52.0.0/16</span></span>
    - <span data-ttu-id="d48bb-194">Azure VNet ASN       : 65010</span><span class="sxs-lookup"><span data-stu-id="d48bb-194">Azure VNet ASN       : 65010</span></span>
    - <span data-ttu-id="d48bb-195">通道 too40.112.190.5 的 azure VNet BGP IP 1: 10.12.255.4</span><span class="sxs-lookup"><span data-stu-id="d48bb-195">Azure VNet BGP IP 1  : 10.12.255.4 for tunnel too40.112.190.5</span></span>
    - <span data-ttu-id="d48bb-196">通道 too138.91.156.129 的 azure VNet BGP IP 2: 10.12.255.5</span><span class="sxs-lookup"><span data-stu-id="d48bb-196">Azure VNet BGP IP 2  : 10.12.255.5 for tunnel too138.91.156.129</span></span>
    - <span data-ttu-id="d48bb-197">靜態路由： 目的地 10.12.255.4/32 下, 一個躍點 hello VPN 通道介面 too40.112.190.5 目的地 10.12.255.5/32 下, 一個躍點 hello VPN 通道介面 too138.91.156.129</span><span class="sxs-lookup"><span data-stu-id="d48bb-197">Static routes        : Destination 10.12.255.4/32, nexthop hello VPN tunnel interface too40.112.190.5                        Destination 10.12.255.5/32, nexthop hello VPN tunnel interface too138.91.156.129</span></span>
    - <span data-ttu-id="d48bb-198">eBGP Multihop： 確定 hello"multihop 」 選項視您的裝置上啟用 eBGP</span><span class="sxs-lookup"><span data-stu-id="d48bb-198">eBGP Multihop        : Ensure hello "multihop" option for eBGP is enabled on your device if needed</span></span>

<span data-ttu-id="d48bb-199">後幾分鐘的時間和 hello BGP 對等互連工作階段，將會開始建立 hello IPsec 連線之後，應該要建立 hello 連線。</span><span class="sxs-lookup"><span data-stu-id="d48bb-199">hello connection should be established after a few minutes, and hello BGP peering session will start once hello IPsec connection is established.</span></span> <span data-ttu-id="d48bb-200">這個範例到目前為止已設定只能有一個在內部部署 VPN 裝置，導致 hello 圖表，如下所示：</span><span class="sxs-lookup"><span data-stu-id="d48bb-200">This example so far has configured only one on-premises VPN device, resulting in hello diagram shown below:</span></span>

![active-active-crossprem](./media/vpn-gateway-activeactive-rm-powershell/active-active.png)

### <a name="step-3---connect-two-on-premises-vpn-devices-toohello-active-active-vpn-gateway"></a><span data-ttu-id="d48bb-202">步驟 3-連接兩個內部部署 VPN 裝置 toohello 主動-主動 VPN 閘道</span><span class="sxs-lookup"><span data-stu-id="d48bb-202">Step 3 - Connect two on-premises VPN devices toohello active-active VPN gateway</span></span>
<span data-ttu-id="d48bb-203">如果您有兩個 VPN 裝置 hello 在相同的內部網路，您可以達到雙重備援連線 hello Azure VPN 閘道 toohello 第二個 VPN 裝置。</span><span class="sxs-lookup"><span data-stu-id="d48bb-203">If you have two VPN devices at hello same on-premises network, you can achieve dual redundancy by connecting hello Azure VPN gateway toohello second VPN device.</span></span>

#### <a name="1-create-hello-second-local-network-gateway-for-site5"></a><span data-ttu-id="d48bb-204">1.建立 Site5 hello 第二個本機網路閘道</span><span class="sxs-lookup"><span data-stu-id="d48bb-204">1. Create hello second local network gateway for Site5</span></span>
<span data-ttu-id="d48bb-205">請注意，hello 閘道 IP 位址、 位址首碼和 hello 第二個本機網路閘道的 BGP 對等位址不可重疊 hello 先前區域網路閘道使用相同的內部網路。</span><span class="sxs-lookup"><span data-stu-id="d48bb-205">Note that hello gateway IP address, address prefix, and BGP peering address for hello second local network gateway must not overlap with hello previous local network gateway for hello same on-premises network.</span></span>

```powershell
$LNGName52 = "Site5_2"
$LNGPrefix52 = "10.52.255.254/32"
$LNGIP52 = "131.107.72.23"
$BGPPeerIP52 = "10.52.255.254"

New-AzureRmLocalNetworkGateway -Name $LNGName52 -ResourceGroupName $RG5 -Location $Location5 -GatewayIpAddress $LNGIP52 -AddressPrefix $LNGPrefix52 -Asn $LNGASN5 -BgpPeeringAddress $BGPPeerIP52
```

#### <a name="2-connect-hello-vnet-gateway-and-hello-second-local-network-gateway"></a><span data-ttu-id="d48bb-206">2.Hello VNet 閘道和 hello 第二個本機網路閘道連接</span><span class="sxs-lookup"><span data-stu-id="d48bb-206">2. Connect hello VNet gateway and hello second local network gateway</span></span>
<span data-ttu-id="d48bb-207">從 TestVNet1 tooSite5_2 建立 hello 連接，與設定得 「 EnableBGP"$True</span><span class="sxs-lookup"><span data-stu-id="d48bb-207">Create hello connection from TestVNet1 tooSite5_2 with "EnableBGP" set too$True</span></span>

```powershell
$lng5gw2 = Get-AzureRmLocalNetworkGateway -Name $LNGName52 -ResourceGroupName $RG5

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection152 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng5gw2 -Location $Location1 -ConnectionType IPsec -SharedKey 'AzureA1b2C3' -EnableBGP True
```

#### <a name="3-vpn-and-bgp-parameters-for-your-second-on-premises-vpn-device"></a><span data-ttu-id="d48bb-208">3.第二個內部部署 VPN 裝置的 VPN 和 BGP 參數</span><span class="sxs-lookup"><span data-stu-id="d48bb-208">3. VPN and BGP parameters for your second on-premises VPN device</span></span>
<span data-ttu-id="d48bb-209">同樣地，以下列出 hello 參數，您會輸入到第二個 VPN 裝置 hello:</span><span class="sxs-lookup"><span data-stu-id="d48bb-209">Similarly, below lists hello parameters you will enter into hello second VPN device:</span></span>

```
- Site5 ASN            : 65050
- Site5 BGP IP         : 10.52.255.254
- Prefixes tooannounce : (for example) 10.51.0.0/16 and 10.52.0.0/16
- Azure VNet ASN       : 65010
- Azure VNet BGP IP 1  : 10.12.255.4 for tunnel too40.112.190.5
- Azure VNet BGP IP 2  : 10.12.255.5 for tunnel too138.91.156.129
- Static routes        : Destination 10.12.255.4/32, nexthop hello VPN tunnel interface too40.112.190.5
                         Destination 10.12.255.5/32, nexthop hello VPN tunnel interface too138.91.156.129
- eBGP Multihop        : Ensure hello "multihop" option for eBGP is enabled on your device if needed
```

<span data-ttu-id="d48bb-210">一旦建立 hello 連線 （通道），您將有雙重備援的 VPN 裝置與連接您的內部部署網路與 Azure 的通道：</span><span class="sxs-lookup"><span data-stu-id="d48bb-210">Once hello connection (tunnels) are established, you will have dual redundant VPN devices and tunnels connecting your on-premises network and Azure:</span></span>

![dual-redundancy-crossprem](./media/vpn-gateway-activeactive-rm-powershell/dual-redundancy.png)

## <span data-ttu-id="d48bb-212"><a name ="aav2v"></a>第 3 部分 - 建立主動-主動 VNet 對 VNet 連線</span><span class="sxs-lookup"><span data-stu-id="d48bb-212"><a name ="aav2v"></a>Part 3 - Establish an active-active VNet-to-VNet connection</span></span>
<span data-ttu-id="d48bb-213">本節會使用 BGP 建立主動-主動 VNet 對 VNet 連線。</span><span class="sxs-lookup"><span data-stu-id="d48bb-213">This section creates an active-active VNet-to-VNet connection with BGP.</span></span> 

<span data-ttu-id="d48bb-214">下列的 hello 指示繼續 hello 上面所列的上一個步驟。</span><span class="sxs-lookup"><span data-stu-id="d48bb-214">hello instructions below continue from hello previous steps listed above.</span></span> <span data-ttu-id="d48bb-215">您必須先完成[第 1 部分](#aagateway)toocreate 並設定 TestVNet1 hello bgp 的 VPN 閘道。</span><span class="sxs-lookup"><span data-stu-id="d48bb-215">You must complete [Part 1](#aagateway) toocreate and configure TestVNet1 and hello VPN Gateway with BGP.</span></span> 

### <a name="step-1---create-testvnet2-and-hello-vpn-gateway"></a><span data-ttu-id="d48bb-216">步驟 1-建立 TestVNet2 和 hello VPN 閘道</span><span class="sxs-lookup"><span data-stu-id="d48bb-216">Step 1 - Create TestVNet2 and hello VPN gateway</span></span>
<span data-ttu-id="d48bb-217">它是重要 toomake 確定 hello 新的虛擬網路，TestVNet2，hello IP 位址空間不與任何 VNet 範圍重疊。</span><span class="sxs-lookup"><span data-stu-id="d48bb-217">It is important toomake sure that hello IP address space of hello new virtual network, TestVNet2, does not overlap with any of your VNet ranges.</span></span>

<span data-ttu-id="d48bb-218">在此範例中，hello 虛擬網路屬於 toohello 相同訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="d48bb-218">In this example, hello virtual networks belong toohello same subscription.</span></span> <span data-ttu-id="d48bb-219">您可以設定不同的訂用帳戶; 之間的 VNet 對 VNet 連線請參閱太[設定 VNet 對 VNet 連線](vpn-gateway-vnet-vnet-rm-ps.md)toolearn 更多詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="d48bb-219">You can set up VNet-to-VNet connections between different subscriptions; please refer too[Configure a VNet-to-VNet connection](vpn-gateway-vnet-vnet-rm-ps.md) toolearn more details.</span></span> <span data-ttu-id="d48bb-220">請確定您新增 hello"的 EnableBgp $True 」 時建立 hello 連線 tooenable BGP。</span><span class="sxs-lookup"><span data-stu-id="d48bb-220">Make sure you add hello "-EnableBgp $True" when creating hello connections tooenable BGP.</span></span>

#### <a name="1-declare-your-variables"></a><span data-ttu-id="d48bb-221">1.宣告變數</span><span class="sxs-lookup"><span data-stu-id="d48bb-221">1. Declare your variables</span></span>
<span data-ttu-id="d48bb-222">為確定 tooreplace 以 hello 的 hello 值的 toouse 您的組態。</span><span class="sxs-lookup"><span data-stu-id="d48bb-222">Be sure tooreplace hello values with hello ones that you want toouse for your configuration.</span></span>

```powershell
$RG2 = "TestAARG2"
$Location2 = "East US"
$VNetName2 = "TestVNet2"
$FESubName2 = "FrontEnd"
$BESubName2 = "Backend"
$GWSubName2 = "GatewaySubnet"
$VNetPrefix21 = "10.21.0.0/16"
$VNetPrefix22 = "10.22.0.0/16"
$FESubPrefix2 = "10.21.0.0/24"
$BESubPrefix2 = "10.22.0.0/24"
$GWSubPrefix2 = "10.22.255.0/27"
$VNet2ASN = 65020
$DNS2 = "8.8.8.8"
$GWName2 = "VNet2GW"
$GW2IPName1 = "VNet2GWIP1"
$GW2IPconf1 = "gw2ipconf1"
$GW2IPName2 = "VNet2GWIP2"
$GW2IPconf2 = "gw2ipconf2"
$Connection21 = "VNet2toVNet1"
$Connection12 = "VNet1toVNet2"
```

#### <a name="2-create-testvnet2-in-hello-new-resource-group"></a><span data-ttu-id="d48bb-223">2.建立 TestVNet2 hello 新資源群組中</span><span class="sxs-lookup"><span data-stu-id="d48bb-223">2. Create TestVNet2 in hello new resource group</span></span>

```powershell
New-AzureRmResourceGroup -Name $RG2 -Location $Location2

$fesub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName2 -AddressPrefix $FESubPrefix2
$besub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName2 -AddressPrefix $BESubPrefix2
$gwsub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName2 -AddressPrefix $GWSubPrefix2

New-AzureRmVirtualNetwork -Name $VNetName2 -ResourceGroupName $RG2 -Location $Location2 -AddressPrefix $VNetPrefix21,$VNetPrefix22 -Subnet $fesub2,$besub2,$gwsub2
```

#### <a name="3-create-hello-active-active-vpn-gateway-for-testvnet2"></a><span data-ttu-id="d48bb-224">3.建立 TestVNet2 hello 主動-主動 VPN 閘道</span><span class="sxs-lookup"><span data-stu-id="d48bb-224">3. Create hello active-active VPN gateway for TestVNet2</span></span>
<span data-ttu-id="d48bb-225">要求兩個公用 IP 位址 toobe 配置的 toohello 閘道您將建立您的 VNet。</span><span class="sxs-lookup"><span data-stu-id="d48bb-225">Request two public IP addresses toobe allocated toohello gateway you will create for your VNet.</span></span> <span data-ttu-id="d48bb-226">您也會定義 hello 子網路和 IP 所需的設定。</span><span class="sxs-lookup"><span data-stu-id="d48bb-226">You'll also define hello subnet and IP configurations required.</span></span>

```powershell
$gw2pip1 = New-AzureRmPublicIpAddress -Name $GW2IPName1 -ResourceGroupName $RG2 -Location $Location2 -AllocationMethod Dynamic
$gw2pip2 = New-AzureRmPublicIpAddress -Name $GW2IPName2 -ResourceGroupName $RG2 -Location $Location2 -AllocationMethod Dynamic

$vnet2 = Get-AzureRmVirtualNetwork -Name $VNetName2 -ResourceGroupName $RG2
$subnet2 = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet2
$gw2ipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GW2IPconf1 -Subnet $subnet2 -PublicIpAddress $gw2pip1
$gw2ipconf2 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GW2IPconf2 -Subnet $subnet2 -PublicIpAddress $gw2pip2
```

<span data-ttu-id="d48bb-227">建立以 hello hello VPN 閘道，為號碼 」 和 「 hello 」 EnableActiveActiveFeature 」 旗標。</span><span class="sxs-lookup"><span data-stu-id="d48bb-227">Create hello VPN gateway with hello AS number and hello "EnableActiveActiveFeature" flag.</span></span> <span data-ttu-id="d48bb-228">請注意，您必須覆寫 hello 預設 ASN 在您的 Azure VPN 閘道。</span><span class="sxs-lookup"><span data-stu-id="d48bb-228">Note that you must override hello default ASN on your Azure VPN gateways.</span></span> <span data-ttu-id="d48bb-229">hello Asn hello 連線 Vnet 必須是不同 tooenable BGP 和傳輸路由。</span><span class="sxs-lookup"><span data-stu-id="d48bb-229">hello ASNs for hello connected VNets must be different tooenable BGP and transit routing.</span></span>

```powershell
New-AzureRmVirtualNetworkGateway -Name $GWName2 -ResourceGroupName $RG2 -Location $Location2 -IpConfigurations $gw2ipconf1,$gw2ipconf2 -GatewayType Vpn -VpnType RouteBased -GatewaySku VpnGw1 -Asn $VNet2ASN -EnableActiveActiveFeature
```

### <a name="step-2---connect-hello-testvnet1-and-testvnet2-gateways"></a><span data-ttu-id="d48bb-230">步驟 2-連接 hello TestVNet1 和 TestVNet2 閘道</span><span class="sxs-lookup"><span data-stu-id="d48bb-230">Step 2 - Connect hello TestVNet1 and TestVNet2 gateways</span></span>
<span data-ttu-id="d48bb-231">在此範例中，兩個閘道位於 hello 相同訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="d48bb-231">In this example, both gateways are in hello same subscription.</span></span> <span data-ttu-id="d48bb-232">您可以完成此步驟在 hello 同一個 PowerShell 工作階段。</span><span class="sxs-lookup"><span data-stu-id="d48bb-232">You can complete this step in hello same PowerShell session.</span></span>

#### <a name="1-get-both-gateways"></a><span data-ttu-id="d48bb-233">1.取得兩個閘道</span><span class="sxs-lookup"><span data-stu-id="d48bb-233">1. Get both gateways</span></span>
<span data-ttu-id="d48bb-234">請確定您登入，並連接 tooSubscription 1。</span><span class="sxs-lookup"><span data-stu-id="d48bb-234">Make sure you log in and connect tooSubscription 1.</span></span>

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
$vnet2gw = Get-AzureRmVirtualNetworkGateway -Name $GWName2 -ResourceGroupName $RG2
```

#### <a name="2-create-both-connections"></a><span data-ttu-id="d48bb-235">2.建立兩個連線</span><span class="sxs-lookup"><span data-stu-id="d48bb-235">2. Create both connections</span></span>
<span data-ttu-id="d48bb-236">在此步驟中，您將從 TestVNet2 tooTestVNet1 建立從 TestVNet1 tooTestVNet2 hello 連線與 hello 連線。</span><span class="sxs-lookup"><span data-stu-id="d48bb-236">In this step, you will create hello connection from TestVNet1 tooTestVNet2, and hello connection from TestVNet2 tooTestVNet1.</span></span>

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name $Connection12 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -VirtualNetworkGateway2 $vnet2gw -Location $Location1 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3' -EnableBgp $True

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection21 -ResourceGroupName $RG2 -VirtualNetworkGateway1 $vnet2gw -VirtualNetworkGateway2 $vnet1gw -Location $Location2 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3' -EnableBgp $True
```

> [!IMPORTANT]
> <span data-ttu-id="d48bb-237">這兩個連接是確定 tooenable BGP。</span><span class="sxs-lookup"><span data-stu-id="d48bb-237">Be sure tooenable BGP for BOTH connections.</span></span>
> 
> 

<span data-ttu-id="d48bb-238">完成這些步驟之後，將會建立 hello 連接在幾分鐘的時間，而且 hello BGP 對等互連工作階段會向上一旦完成雙重備援 hello VNet 對 VNet 連線：</span><span class="sxs-lookup"><span data-stu-id="d48bb-238">After completing these steps, hello connection will be establish in a few minutes, and hello BGP peering session will be up once hello VNet-to-VNet connection is completed with dual redundancy:</span></span>

![active-active-v2v](./media/vpn-gateway-activeactive-rm-powershell/vnet-to-vnet.png)

## <span data-ttu-id="d48bb-240"><a name ="aaupdate"></a>第 4 部分 - 更新主動-主動和作用中-待命之間的現有閘道</span><span class="sxs-lookup"><span data-stu-id="d48bb-240"><a name ="aaupdate"></a>Part 4 - Update existing gateway between active-active and active-standby</span></span>
<span data-ttu-id="d48bb-241">hello 最後一節將說明您可以設定現有的 Azure VPN 閘道的方式從作用中-待命 tooactive 主動模式，反之亦然。</span><span class="sxs-lookup"><span data-stu-id="d48bb-241">hello last section will describe how you can configure an existing Azure VPN gateway from active-standby tooactive-active mode, or vice versa.</span></span>

> [!NOTE]
> <span data-ttu-id="d48bb-242">本節包含從標準 tooHighPerformance 已建立 VPN 閘道的 hello 步驟 tooresize 舊版的 SKU (舊 SKU)。</span><span class="sxs-lookup"><span data-stu-id="d48bb-242">This section includes hello steps tooresize a legacy SKU (old SKU) of an already created VPN gateway from Standard tooHighPerformance.</span></span> <span data-ttu-id="d48bb-243">這些步驟，請勿升級 hello 舊舊版 SKU tooone 新 Sku。</span><span class="sxs-lookup"><span data-stu-id="d48bb-243">These steps do not upgrade an old legacy SKU tooone of hello new SKUs.</span></span>
> 
> 

### <a name="configure-an-active-standby-gateway-tooactive-active-gateway"></a><span data-ttu-id="d48bb-244">設定作用中-待命閘道 tooactive 主動閘道</span><span class="sxs-lookup"><span data-stu-id="d48bb-244">Configure an active-standby gateway tooactive-active gateway</span></span>
#### <a name="1-gateway-parameters"></a><span data-ttu-id="d48bb-245">1.閘道參數</span><span class="sxs-lookup"><span data-stu-id="d48bb-245">1. Gateway parameters</span></span>
<span data-ttu-id="d48bb-246">下列範例中的 hello 轉換主動-主動閘道的作用中-待命閘道。</span><span class="sxs-lookup"><span data-stu-id="d48bb-246">hello following example converts an active-standby gateway into an active-active gateway.</span></span> <span data-ttu-id="d48bb-247">您需要 toocreate 另一個公用 IP 位址，然後加入第二個閘道 IP 組態。</span><span class="sxs-lookup"><span data-stu-id="d48bb-247">You need toocreate another public IP address, then add a second Gateway IP configuration.</span></span> <span data-ttu-id="d48bb-248">以下顯示 hello 用的參數：</span><span class="sxs-lookup"><span data-stu-id="d48bb-248">Below shows hello parameters used:</span></span>

```powershell
$GWName = "TestVNetAA1GW"
$VNetName = "TestVNetAA1"
$RG = "TestVPNActiveActive01"
$GWIPName2 = "gwpip2"
$GWIPconf2 = "gw1ipconf2"

$vnet = Get-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $RG
$subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -VirtualNetwork $vnet
$gw = Get-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG
$location = $gw.Location
```

#### <a name="2-create-hello-public-ip-address-then-add-hello-second-gateway-ip-configuration"></a><span data-ttu-id="d48bb-249">2.建立 hello 公用 IP 位址，然後將第二個閘道 IP 設定 hello</span><span class="sxs-lookup"><span data-stu-id="d48bb-249">2. Create hello public IP address, then add hello second gateway IP configuration</span></span>

```powershell
$gwpip2 = New-AzureRmPublicIpAddress -Name $GWIPName2 -ResourceGroupName $RG -Location $location -AllocationMethod Dynamic
Add-AzureRmVirtualNetworkGatewayIpConfig -VirtualNetworkGateway $gw -Name $GWIPconf2 -Subnet $subnet -PublicIpAddress $gwpip2
```

#### <a name="3-enable-active-active-mode-and-update-hello-gateway"></a><span data-ttu-id="d48bb-250">3.啟用主動 / 主動模式和更新 hello 閘道</span><span class="sxs-lookup"><span data-stu-id="d48bb-250">3. Enable active-active mode and update hello gateway</span></span>
<span data-ttu-id="d48bb-251">PowerShell tootrigger hello 實際的更新中，您必須設定 hello 閘道物件。</span><span class="sxs-lookup"><span data-stu-id="d48bb-251">You must set hello gateway object in PowerShell tootrigger hello actual update.</span></span> <span data-ttu-id="d48bb-252">hello 的 hello 虛擬網路閘道 SKU 必須也變更 （調整大小） tooHighPerformance 先前建立的標準。</span><span class="sxs-lookup"><span data-stu-id="d48bb-252">hello SKU of hello virtual network gateway must also be changed (resized) tooHighPerformance since it was created previously as Standard.</span></span>

```powershell
Set-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw -EnableActiveActiveFeature -GatewaySku HighPerformance
```

<span data-ttu-id="d48bb-253">這項更新可能需要 30 的 too45 分鐘。</span><span class="sxs-lookup"><span data-stu-id="d48bb-253">This update can take 30 too45 minutes.</span></span>

### <a name="configure-an-active-active-gateway-tooactive-standby-gateway"></a><span data-ttu-id="d48bb-254">主動-主動閘道 tooactive 待命閘道設定</span><span class="sxs-lookup"><span data-stu-id="d48bb-254">Configure an active-active gateway tooactive-standby gateway</span></span>
#### <a name="1-gateway-parameters"></a><span data-ttu-id="d48bb-255">1.閘道參數</span><span class="sxs-lookup"><span data-stu-id="d48bb-255">1. Gateway parameters</span></span>
<span data-ttu-id="d48bb-256">使用 hello 相同參數做為上述項目，取得 hello IP 設定您想要的 hello 名稱 tooremove。</span><span class="sxs-lookup"><span data-stu-id="d48bb-256">Use hello same parameters as above, get hello name of hello IP configuration you want tooremove.</span></span>

```powershell
$GWName = "TestVNetAA1GW"
$RG = "TestVPNActiveActive01"

$gw = Get-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG
$ipconfname = $gw.IpConfigurations[1].Name
```

#### <a name="2-remove-hello-gateway-ip-configuration-and-disable-hello-active-active-mode"></a><span data-ttu-id="d48bb-257">2.請移除 hello 閘道 IP 組態，然後停用 hello 主動 / 主動模式</span><span class="sxs-lookup"><span data-stu-id="d48bb-257">2. Remove hello gateway IP configuration and disable hello active-active mode</span></span>
<span data-ttu-id="d48bb-258">同樣地，您必須設定 PowerShell tootrigger hello 實際更新 hello 閘道物件。</span><span class="sxs-lookup"><span data-stu-id="d48bb-258">Similarly, you must set hello gateway object in PowerShell tootrigger hello actual update.</span></span>

```powershell
Remove-AzureRmVirtualNetworkGatewayIpConfig -Name $ipconfname -VirtualNetworkGateway $gw
Set-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw -DisableActiveActiveFeature
```

<span data-ttu-id="d48bb-259">這項更新最多可能需要 too30 太 45 分鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="d48bb-259">This update can take up too30 too 45 minutes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d48bb-260">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d48bb-260">Next steps</span></span>
<span data-ttu-id="d48bb-261">一旦完成您的連線，您可以將虛擬機器 tooyour 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="d48bb-261">Once your connection is complete, you can add virtual machines tooyour virtual networks.</span></span> <span data-ttu-id="d48bb-262">請參閱 [建立網站的虛擬機器](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) 以取得相關步驟。</span><span class="sxs-lookup"><span data-stu-id="d48bb-262">See [Create a Virtual Machine](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) for steps.</span></span>
