---
title: "在 Azure VPN 閘道上設定 BGP：Resource Manager: PowerShell | Microsoft Docs"
description: "本文將逐步引導您使用 Azure Resource Manager 和 PowerShell 來設定 BGP 與 Azure VPN 閘道。"
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: 
tags: azure-resource-manager
ms.assetid: 905b11a7-1333-482c-820b-0fd0f44238e5
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/12/2017
ms.author: yushwang
ms.openlocfilehash: b00a3fe7ba4b12c2e9c486188c292cd6fafb60a3
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-configure-bgp-on-azure-vpn-gateways-using-powershell"></a><span data-ttu-id="73031-103">如何使用 PowerShell 在 Azure VPN 閘道上設定 BGP</span><span class="sxs-lookup"><span data-stu-id="73031-103">How to configure BGP on Azure VPN Gateways using PowerShell</span></span>
<span data-ttu-id="73031-104">本文將逐步引導您進行使用 Resource Manager 部署模型和 PowerShell 在跨單位網站間 (S2S) VPN 連線和 VNet 對 VNet 連線上啟用 BGP 的步驟。</span><span class="sxs-lookup"><span data-stu-id="73031-104">This article walks you through the steps to enable BGP on a cross-premises Site-to-Site (S2S) VPN connection and a VNet-to-VNet connection using the Resource Manager deployment model and PowerShell.</span></span>

## <a name="about-bgp"></a><span data-ttu-id="73031-105">關於 BGP</span><span class="sxs-lookup"><span data-stu-id="73031-105">About BGP</span></span>
<span data-ttu-id="73031-106">BGP 是常用於網際網路的標準路由通訊協定，可交換兩個或多個網路之間的路由和可執行性資訊。</span><span class="sxs-lookup"><span data-stu-id="73031-106">BGP is the standard routing protocol commonly used in the Internet to exchange routing and reachability information between two or more networks.</span></span> <span data-ttu-id="73031-107">BGP 會啟用 Azure VPN 閘道，以及內部部署 VPN 裝置 (稱為 BGP 對等或鄰近項目) 來交換「路由」，其會通知這兩個閘道對要通過閘道的首碼或所涉及之路由器的可用性和可執行性。</span><span class="sxs-lookup"><span data-stu-id="73031-107">BGP enables the Azure VPN Gateways and your on-premises VPN devices, called BGP peers or neighbors, to exchange "routes" that will inform both gateways on the availability and reachability for those prefixes to go through the gateways or routers involved.</span></span> <span data-ttu-id="73031-108">BGP 也可以傳播從一個 BGP 對等互連到所有其他 BGP 對等所識別的 BGP 閘道，來啟用多個網路之間的傳輸路由。</span><span class="sxs-lookup"><span data-stu-id="73031-108">BGP can also enable transit routing among multiple networks by propagating routes a BGP gateway learns from one BGP peer to all other BGP peers.</span></span>

<span data-ttu-id="73031-109">如需 BGP 優點的討論並了解使用 BGP 的技術需求和考量，請參閱 [BGP 與 Azure VPN 閘道的概觀](vpn-gateway-bgp-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="73031-109">See [Overview of BGP with Azure VPN Gateways](vpn-gateway-bgp-overview.md) for more discussion on benefits of BGP and to understand the technical requirements and considerations of using BGP.</span></span>

## <a name="getting-started-with-bgp-on-azure-vpn-gateways"></a><span data-ttu-id="73031-110">開始在 Azure VPN 閘道上使用 BGP</span><span class="sxs-lookup"><span data-stu-id="73031-110">Getting started with BGP on Azure VPN gateways</span></span>

<span data-ttu-id="73031-111">本文將逐步引導您完成執行下列作業的步驟：</span><span class="sxs-lookup"><span data-stu-id="73031-111">This article walks you through the steps to do the following tasks:</span></span>

* [<span data-ttu-id="73031-112">第 1 部份 - 在 Azure VPN 閘道上啟用 BGP</span><span class="sxs-lookup"><span data-stu-id="73031-112">Part 1 - Enable BGP on your Azure VPN gateway</span></span>](#enablebgp)
* [<span data-ttu-id="73031-113">第 2 部份 – 建立與 BGP 的跨單位連線</span><span class="sxs-lookup"><span data-stu-id="73031-113">Part 2 - Establish a cross-premises connection with BGP</span></span>](#crossprembgp)
* [<span data-ttu-id="73031-114">第 3 部份 – 建立與 BGP 的 VNet 對 VNet 連線</span><span class="sxs-lookup"><span data-stu-id="73031-114">Part 3 - Establish a VNet-to-VNet connection with BGP</span></span>](#v2vbgp)

<span data-ttu-id="73031-115">指示的每個部分均構成基本建置組塊，可供在您的網路連線中啟用 BGP。</span><span class="sxs-lookup"><span data-stu-id="73031-115">Each part of the instructions forms a basic building block for enabling BGP in your network connectivity.</span></span> <span data-ttu-id="73031-116">如果您完成上述三個部分，將建置如下圖所示的拓撲︰</span><span class="sxs-lookup"><span data-stu-id="73031-116">If you complete all three parts, you build the topology as shown in the following diagram:</span></span>

![BGP 拓樸](./media/vpn-gateway-bgp-resource-manager-ps/bgp-crosspremv2v.png)

<span data-ttu-id="73031-118">您可以將多個部分結合起來，依您的需求建立更複雜的多重躍點傳輸網路。</span><span class="sxs-lookup"><span data-stu-id="73031-118">You can combine parts together to build a more complex, multi-hop, transit network that meets your needs.</span></span>

## <span data-ttu-id="73031-119"><a name ="enablebgp"></a>第 1 部分 - 在 Azure VPN 閘道上設定 BGP</span><span class="sxs-lookup"><span data-stu-id="73031-119"><a name ="enablebgp"></a>Part 1 - Configure BGP on the Azure VPN Gateway</span></span>
<span data-ttu-id="73031-120">設定步驟將會設定 Azure VPN 閘道的 BGP 參數，如下圖所示︰</span><span class="sxs-lookup"><span data-stu-id="73031-120">The configuration steps set up the BGP parameters of the Azure VPN gateway as shown in the following diagram:</span></span>

![BGP 閘道](./media/vpn-gateway-bgp-resource-manager-ps/bgp-gateway.png)

### <a name="before-you-begin"></a><span data-ttu-id="73031-122">開始之前</span><span class="sxs-lookup"><span data-stu-id="73031-122">Before you begin</span></span>
* <span data-ttu-id="73031-123">請確認您有 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="73031-123">Verify that you have an Azure subscription.</span></span> <span data-ttu-id="73031-124">如果您還沒有 Azure 訂用帳戶，則可以啟用 [MSDN 訂戶權益](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/)或註冊[免費帳戶](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="73031-124">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free account](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="73031-125">您必須安裝 Azure Resource Manager PowerShell Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="73031-125">Install the Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="73031-126">如需如何安裝 PowerShell Cmdlet 的詳細資訊，請參閱[如何安裝和設定 Azure PowerShell](/powershell/azure/overview) 。</span><span class="sxs-lookup"><span data-stu-id="73031-126">For more information about installing the PowerShell cmdlets, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span> 

### <a name="step-1---create-and-configure-vnet1"></a><span data-ttu-id="73031-127">步驟 1 - 建立及設定 VNet1</span><span class="sxs-lookup"><span data-stu-id="73031-127">Step 1 - Create and configure VNet1</span></span>
#### <a name="1-declare-your-variables"></a><span data-ttu-id="73031-128">1.宣告變數</span><span class="sxs-lookup"><span data-stu-id="73031-128">1. Declare your variables</span></span>
<span data-ttu-id="73031-129">對於此練習，我們一開始先宣告我們的變數。</span><span class="sxs-lookup"><span data-stu-id="73031-129">For this exercise, we start by declaring our variables.</span></span> <span data-ttu-id="73031-130">下列範例會使用此練習中的值來宣告變數。</span><span class="sxs-lookup"><span data-stu-id="73031-130">The following example declares the variables using the values for this exercise.</span></span> <span data-ttu-id="73031-131">請務必在設定生產環境時，使用您自己的值來取代該值。</span><span class="sxs-lookup"><span data-stu-id="73031-131">Be sure to replace the values with your own when configuring for production.</span></span> <span data-ttu-id="73031-132">若您執行這些步驟是為了熟悉此類型的設定，則可以使用這些變數。</span><span class="sxs-lookup"><span data-stu-id="73031-132">You can use these variables if you are running through the steps to become familiar with this type of configuration.</span></span> <span data-ttu-id="73031-133">修改變數，然後將其複製並貼到您的 PowerShell 主控台中。</span><span class="sxs-lookup"><span data-stu-id="73031-133">Modify the variables, and then copy and paste into your PowerShell console.</span></span>

```powershell
$Sub1 = "Replace_With_Your_Subcription_Name"
$RG1 = "TestBGPRG1"
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
$VNet1ASN = 65010
$DNS1 = "8.8.8.8"
$GWName1 = "VNet1GW"
$GWIPName1 = "VNet1GWIP"
$GWIPconfName1 = "gwipconf1"
$Connection12 = "VNet1toVNet2"
$Connection15 = "VNet1toSite5"
```

#### <a name="2-connect-to-your-subscription-and-create-a-new-resource-group"></a><span data-ttu-id="73031-134">2.連接至您的訂用帳戶並建立新的資源群組</span><span class="sxs-lookup"><span data-stu-id="73031-134">2. Connect to your subscription and create a new resource group</span></span>
<span data-ttu-id="73031-135">請確定您切換為 PowerShell 模式，以使用 Resource Manager Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="73031-135">To use the Resource Manager cmdlets, Make sure you switch to PowerShell mode.</span></span> <span data-ttu-id="73031-136">如需詳細資訊，請參閱 [搭配使用 Windows PowerShell 與 Resource Manager](../powershell-azure-resource-manager.md)。</span><span class="sxs-lookup"><span data-stu-id="73031-136">For more information, see [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

<span data-ttu-id="73031-137">開啟 PowerShell 主控台並連接到您的帳戶。</span><span class="sxs-lookup"><span data-stu-id="73031-137">Open your PowerShell console and connect to your account.</span></span> <span data-ttu-id="73031-138">使用下列範例來協助您連接：</span><span class="sxs-lookup"><span data-stu-id="73031-138">Use the following sample to help you connect:</span></span>

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionName $Sub1
New-AzureRmResourceGroup -Name $RG1 -Location $Location1
```

#### <a name="3-create-testvnet1"></a><span data-ttu-id="73031-139">3.建立 TestVNet1</span><span class="sxs-lookup"><span data-stu-id="73031-139">3. Create TestVNet1</span></span>
<span data-ttu-id="73031-140">下列範例會建立一個名為 TestVNet1 的虛擬網路和三個子網路：一個名為 GatewaySubnet、一個名為 FrontEnd，另一個名為 Backend。</span><span class="sxs-lookup"><span data-stu-id="73031-140">The following sample creates a virtual network named TestVNet1 and three subnets, one called GatewaySubnet, one called FrontEnd, and one called Backend.</span></span> <span data-ttu-id="73031-141">替代值時，務必一律將您的閘道子網路特定命名為 GatewaySubnet。</span><span class="sxs-lookup"><span data-stu-id="73031-141">When substituting values, it's important that you always name your gateway subnet specifically GatewaySubnet.</span></span> <span data-ttu-id="73031-142">如果您將其命名為其他名稱，閘道建立會失敗。</span><span class="sxs-lookup"><span data-stu-id="73031-142">If you name it something else, your gateway creation fails.</span></span>

```powershell
$fesub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName1 -AddressPrefix $FESubPrefix1 $besub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName1 -AddressPrefix $BESubPrefix1
$gwsub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName1 -AddressPrefix $GWSubPrefix1

New-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1 -Location $Location1 -AddressPrefix $VNetPrefix11,$VNetPrefix12 -Subnet $fesub1,$besub1,$gwsub1
```

### <a name="step-2---create-the-vpn-gateway-for-testvnet1-with-bgp-parameters"></a><span data-ttu-id="73031-143">步驟 2 - 使用 BGP 參數建立 TestVNet1 的 VPN 閘道</span><span class="sxs-lookup"><span data-stu-id="73031-143">Step 2 - Create the VPN Gateway for TestVNet1 with BGP parameters</span></span>
#### <a name="1-create-the-ip-and-subnet-configurations"></a><span data-ttu-id="73031-144">1.建立 IP 和子網路組態</span><span class="sxs-lookup"><span data-stu-id="73031-144">1. Create the IP and subnet configurations</span></span>
<span data-ttu-id="73031-145">要求一個公用 IP 位址，以配置給您將建立給 VNet 使用的閘道。</span><span class="sxs-lookup"><span data-stu-id="73031-145">Request a public IP address to be allocated to the gateway you will create for your VNet.</span></span> <span data-ttu-id="73031-146">您也會定義必要的子網路和 IP 組態。</span><span class="sxs-lookup"><span data-stu-id="73031-146">You'll also define the required subnet and IP configurations.</span></span>

```powershell
$gwpip1 = New-AzureRmPublicIpAddress -Name $GWIPName1 -ResourceGroupName $RG1 -Location $Location1 -AllocationMethod Dynamic

$vnet1 = Get-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1
$subnet1 = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet1
$gwipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName1 -Subnet $subnet1 -PublicIpAddress $gwpip1
```

#### <a name="2-create-the-vpn-gateway-with-the-as-number"></a><span data-ttu-id="73031-147">2.透過 AS 號碼建立 VPN 閘道</span><span class="sxs-lookup"><span data-stu-id="73031-147">2. Create the VPN gateway with the AS number</span></span>
<span data-ttu-id="73031-148">建立 TestVNet1 的虛擬網路閘道。</span><span class="sxs-lookup"><span data-stu-id="73031-148">Create the virtual network gateway for TestVNet1.</span></span> <span data-ttu-id="73031-149">BGP 需要路由式 VPN 閘道，以及額外參數 (-Asn) 才能設定 TestVNet1 的 ASN (AS 號碼)。</span><span class="sxs-lookup"><span data-stu-id="73031-149">BGP requires a Route-Based VPN gateway, and also the addition parameter, -Asn, to set the ASN (AS Number) for TestVNet1.</span></span> <span data-ttu-id="73031-150">如果您沒有設定 ASN 參數，系統會指派 ASN 65515。</span><span class="sxs-lookup"><span data-stu-id="73031-150">If you do not set the ASN parameter, ASN 65515 is assigned.</span></span> <span data-ttu-id="73031-151">建立閘道可能需要花費一段時間 (30 分鐘或更久)。</span><span class="sxs-lookup"><span data-stu-id="73031-151">Creating a gateway can take a while (30 minutes or more to complete).</span></span>

```powershell
New-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1 -Location $Location1 -IpConfigurations $gwipconf1 -GatewayType Vpn -VpnType RouteBased -GatewaySku HighPerformance -Asn $VNet1ASN
```

#### <a name="3-obtain-the-azure-bgp-peer-ip-address"></a><span data-ttu-id="73031-152">3.取得 Azure BGP 對等 IP 位址</span><span class="sxs-lookup"><span data-stu-id="73031-152">3. Obtain the Azure BGP Peer IP address</span></span>
<span data-ttu-id="73031-153">建立閘道後，您必須取得 Azure VPN 閘道上的 BGP 對等 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="73031-153">Once the gateway is created, you need to obtain the BGP Peer IP address on the Azure VPN Gateway.</span></span> <span data-ttu-id="73031-154">需要有此位址，才能將 Azure VPN 閘道設定為您的內部部署 VPN 裝置的 BGP 對等。</span><span class="sxs-lookup"><span data-stu-id="73031-154">This address is needed to configure the Azure VPN Gateway as a BGP Peer for your on-premises VPN devices.</span></span>

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
$vnet1gw.BgpSettingsText
```

<span data-ttu-id="73031-155">最後一個命令會顯示 Azure VPN 閘道上對應的 BGP 組態；例如︰</span><span class="sxs-lookup"><span data-stu-id="73031-155">The last command shows the corresponding BGP configurations on the Azure VPN Gateway; for example:</span></span>

```powershell
$vnet1gw.BgpSettingsText
{
    "Asn": 65010,
    "BgpPeeringAddress": "10.12.255.30",
    "PeerWeight": 0
}
```

<span data-ttu-id="73031-156">建立閘道後，您可以使用此閘道來建立跨單位連線或與 BGP 的 VNet 對 VNet 連線。</span><span class="sxs-lookup"><span data-stu-id="73031-156">Once the gateway is created, you can use this gateway to establish cross-premises connection or VNet-to-VNet connection with BGP.</span></span> <span data-ttu-id="73031-157">下列各節將逐步說明完成練習的步驟。</span><span class="sxs-lookup"><span data-stu-id="73031-157">The following sections walk through the steps to complete the exercise.</span></span>

## <span data-ttu-id="73031-158"><a name ="crossprembbgp"></a>第 2 部份 – 建立與 BGP 的跨單位連線</span><span class="sxs-lookup"><span data-stu-id="73031-158"><a name ="crossprembbgp"></a>Part 2 - Establish a cross-premises connection with BGP</span></span>

<span data-ttu-id="73031-159">若要建立跨單位連線，您需要建立區域網路閘道來代表您的內部部署 VPN 裝置，以及建立一個連線來連線 VPN 閘道與區域網路閘道。</span><span class="sxs-lookup"><span data-stu-id="73031-159">To establish a cross-premises connection, you need to create a Local Network Gateway to represent your on-premises VPN device, and a Connection to connect the VPN gateway with the local network gateway.</span></span> <span data-ttu-id="73031-160">許多文章會引導您完成這些步驟，本文則會包含指定 BGP 組態參數所需的其他屬性。</span><span class="sxs-lookup"><span data-stu-id="73031-160">While there are articles that walk you through these steps, this article contains the additional properties required to specify the BGP configuration parameters.</span></span>

![跨單位的 BGP](./media/vpn-gateway-bgp-resource-manager-ps/bgp-crossprem.png)

<span data-ttu-id="73031-162">在繼續之前，請確定您已完成本練習的[第 1 部分](#enablebgp)。</span><span class="sxs-lookup"><span data-stu-id="73031-162">Before proceeding, make sure you have completed [Part 1](#enablebgp) of this exercise.</span></span>

### <a name="step-1---create-and-configure-the-local-network-gateway"></a><span data-ttu-id="73031-163">步驟 1 - 建立及設定區域網路閘道</span><span class="sxs-lookup"><span data-stu-id="73031-163">Step 1 - Create and configure the local network gateway</span></span>

#### <a name="1-declare-your-variables"></a><span data-ttu-id="73031-164">1.宣告變數</span><span class="sxs-lookup"><span data-stu-id="73031-164">1. Declare your variables</span></span>

<span data-ttu-id="73031-165">本練習將繼續建置圖中所示的組態。</span><span class="sxs-lookup"><span data-stu-id="73031-165">This exercise continues to build the configuration shown in the diagram.</span></span> <span data-ttu-id="73031-166">請務必使用您想用於設定的值來取代該值。</span><span class="sxs-lookup"><span data-stu-id="73031-166">Be sure to replace the values with the ones that you want to use for your configuration.</span></span>

```powershell
$RG5 = "TestBGPRG5"
$Location5 = "East US 2"
$LNGName5 = "Site5"
$LNGPrefix50 = "10.52.255.254/32"
$LNGIP5 = "Your_VPN_Device_IP"
$LNGASN5 = 65050
$BGPPeerIP5 = "10.52.255.254"
```

<span data-ttu-id="73031-167">關於區域網路閘道參數，有幾件事要注意︰</span><span class="sxs-lookup"><span data-stu-id="73031-167">A couple of things to note regarding the local network gateway parameters:</span></span>

* <span data-ttu-id="73031-168">區域網路閘道可以位於與 VPN 閘道相同或不同的位置和資源群組中。</span><span class="sxs-lookup"><span data-stu-id="73031-168">The local network gateway can be in the same or different location and resource group as the VPN gateway.</span></span> <span data-ttu-id="73031-169">此範例會顯示它們位於不同位置的不同資源群組中。</span><span class="sxs-lookup"><span data-stu-id="73031-169">This example shows them in different resource groups in different locations.</span></span>
* <span data-ttu-id="73031-170">您需要針對區域網路閘道宣告的最小前置詞是 VPN 裝置上 BGP 對等 IP 位址的主機位址。</span><span class="sxs-lookup"><span data-stu-id="73031-170">The minimum prefix you need to declare for the local network gateway is the host address of your BGP Peer IP address on your VPN device.</span></span> <span data-ttu-id="73031-171">在此情況下是 "10.52.255.254/32" 的前置詞 /32。</span><span class="sxs-lookup"><span data-stu-id="73031-171">In this case, it's a /32 prefix of "10.52.255.254/32".</span></span>
* <span data-ttu-id="73031-172">提醒您，您必須在內部部署網路與 Azure VNet 之間使用不同的 BGP ASN。</span><span class="sxs-lookup"><span data-stu-id="73031-172">As a reminder, you must use different BGP ASNs between your on-premises networks and Azure VNet.</span></span> <span data-ttu-id="73031-173">在兩者相同的情況下，如果內部部署 VPN 裝置已經使用 ASN 來與其他 BGP 芳鄰建立對等連線，您就需要變更您的 VNet ASN。</span><span class="sxs-lookup"><span data-stu-id="73031-173">If they are the same, you need to change your VNet ASN if your on-premises VPN device already uses the ASN to peer with other BGP neighbors.</span></span>

<span data-ttu-id="73031-174">繼續之前，請先確定您仍然與訂用帳戶 1 保持連線。</span><span class="sxs-lookup"><span data-stu-id="73031-174">Before you continue, make sure you are still connected to Subscription 1.</span></span>

#### <a name="2-create-the-local-network-gateway-for-site5"></a><span data-ttu-id="73031-175">2.建立 Site5 的區域網路閘道</span><span class="sxs-lookup"><span data-stu-id="73031-175">2. Create the local network gateway for Site5</span></span>

<span data-ttu-id="73031-176">如果尚未建立資源群組，請務必加以建立，才能建立區域網路閘道。</span><span class="sxs-lookup"><span data-stu-id="73031-176">Be sure to create the resource group if it is not created, before you create the local network gateway.</span></span> <span data-ttu-id="73031-177">請注意，區域網路閘道的兩個額外參數︰Asn 與 BgpPeerAddress。</span><span class="sxs-lookup"><span data-stu-id="73031-177">Notice the two additional parameters for the local network gateway: Asn and BgpPeerAddress.</span></span>

```powershell
New-AzureRmResourceGroup -Name $RG5 -Location $Location5

New-AzureRmLocalNetworkGateway -Name $LNGName5 -ResourceGroupName $RG5 -Location $Location5 -GatewayIpAddress $LNGIP5 -AddressPrefix $LNGPrefix50 -Asn $LNGASN5 -BgpPeeringAddress $BGPPeerIP5
```

### <a name="step-2---connect-the-vnet-gateway-and-local-network-gateway"></a><span data-ttu-id="73031-178">步驟 2 - 連接 VNet 閘道與區域網路閘道</span><span class="sxs-lookup"><span data-stu-id="73031-178">Step 2 - Connect the VNet gateway and local network gateway</span></span>

#### <a name="1-get-the-two-gateways"></a><span data-ttu-id="73031-179">1.取得兩個閘道</span><span class="sxs-lookup"><span data-stu-id="73031-179">1. Get the two gateways</span></span>

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$lng5gw  = Get-AzureRmLocalNetworkGateway -Name $LNGName5 -ResourceGroupName $RG5
```

#### <a name="2-create-the-testvnet1-to-site5-connection"></a><span data-ttu-id="73031-180">2.建立 TestVNet1 至 Site5 的連線</span><span class="sxs-lookup"><span data-stu-id="73031-180">2. Create the TestVNet1 to Site5 connection</span></span>

<span data-ttu-id="73031-181">在此步驟中，您將建立從 TestVNet1 至 Site5 的連線。</span><span class="sxs-lookup"><span data-stu-id="73031-181">In this step, you create the connection from TestVNet1 to Site5.</span></span> <span data-ttu-id="73031-182">您必須指定 "-EnableBGP $True" 才能為此連線啟用 BGP。</span><span class="sxs-lookup"><span data-stu-id="73031-182">You must specify "-EnableBGP $True" to enable BGP for this connection.</span></span> <span data-ttu-id="73031-183">如先前所討論，相同的 Azure VPN 閘道可以同時有 BGP 和非 BGP 連線。</span><span class="sxs-lookup"><span data-stu-id="73031-183">As discussed earlier, it is possible to have both BGP and non-BGP connections for the same Azure VPN Gateway.</span></span> <span data-ttu-id="73031-184">除非已在連接屬性中啟用 BGP，否則即使已在兩個閘道上設定 BGP 參數，Azure 也不會為此連線啟用 BGP。</span><span class="sxs-lookup"><span data-stu-id="73031-184">Unless BGP is enabled in the connection property, Azure will not enable BGP for this connection even though BGP parameters are already configured on both gateways.</span></span>

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name $Connection15 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng5gw -Location $Location1 -ConnectionType IPsec -SharedKey 'AzureA1b2C3' -EnableBGP $True
```

<span data-ttu-id="73031-185">下列範例所列出的參數，是您要針對此練習，在內部部署 VPN 裝置的 BGP 組態區段中加以輸入︰</span><span class="sxs-lookup"><span data-stu-id="73031-185">The following example lists the parameters you enter into the BGP configuration section on your on-premises VPN device for this exercise:</span></span>

```

- Site5 ASN            : 65050
- Site5 BGP IP         : 10.52.255.254
- Prefixes to announce : (for example) 10.51.0.0/16 and 10.52.0.0/16
- Azure VNet ASN       : 65010
- Azure VNet BGP IP    : 10.12.255.30
- Static route         : Add a route for 10.12.255.30/32, with nexthop being the VPN tunnel interface on your device
- eBGP Multihop        : Ensure the "multihop" option for eBGP is enabled on your device if needed
```

<span data-ttu-id="73031-186">幾分鐘後就會建立連線，而一旦建立 IPsec 連線後，BGP 對等工作階段就會啟動。</span><span class="sxs-lookup"><span data-stu-id="73031-186">The connection is established after a few minutes, and the BGP peering session starts once the IPsec connection is established.</span></span>

## <span data-ttu-id="73031-187"><a name ="v2vbgp"></a>第 3 部份 – 建立與 BGP 的 VNet 對 VNet 連線</span><span class="sxs-lookup"><span data-stu-id="73031-187"><a name ="v2vbgp"></a>Part 3 - Establish a VNet-to-VNet connection with BGP</span></span>

<span data-ttu-id="73031-188">本節新增與 BGP 的 VNet 對 VNet 連線，如下圖所示：</span><span class="sxs-lookup"><span data-stu-id="73031-188">This section adds a VNet-to-VNet connection with BGP, as shown in the following diagram:</span></span>

![VNet 對 VNet 的 BGP](./media/vpn-gateway-bgp-resource-manager-ps/bgp-vnet2vnet.png)

<span data-ttu-id="73031-190">以下指示延續自從上面所列的先前步驟。</span><span class="sxs-lookup"><span data-stu-id="73031-190">The following instructions continue from the previous steps.</span></span> <span data-ttu-id="73031-191">您必須完成 [I 部分](#enablebgp) ，以建立並設定 TestVNet1 和採用 BGP 的 VPN 閘道。</span><span class="sxs-lookup"><span data-stu-id="73031-191">You must complete [Part I](#enablebgp) to create and configure TestVNet1 and the VPN Gateway with BGP.</span></span> 

### <a name="step-1---create-testvnet2-and-the-vpn-gateway"></a><span data-ttu-id="73031-192">步驟 1 - 建立 TestVNet2 和 VPN 閘道</span><span class="sxs-lookup"><span data-stu-id="73031-192">Step 1 - Create TestVNet2 and the VPN gateway</span></span>

<span data-ttu-id="73031-193">請務必確定新虛擬網路的 IP 位址空間 TestVNet2 不會與任何 VNet 範圍重疊。</span><span class="sxs-lookup"><span data-stu-id="73031-193">It is important to make sure that the IP address space of the new virtual network, TestVNet2, does not overlap with any of your VNet ranges.</span></span>

<span data-ttu-id="73031-194">在此範例中，虛擬網路屬於相同的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="73031-194">In this example, the virtual networks belong to the same subscription.</span></span> <span data-ttu-id="73031-195">您可以設定不同訂用帳戶之間的 VNet 對 VNet 連線。</span><span class="sxs-lookup"><span data-stu-id="73031-195">You can set up VNet-to-VNet connections between different subscriptions.</span></span> <span data-ttu-id="73031-196">如需詳細資訊，請參閱[設定 VNet 對 VNet 連線](vpn-gateway-vnet-vnet-rm-ps.md)。</span><span class="sxs-lookup"><span data-stu-id="73031-196">For more information, see [Configure a VNet-to-VNet connection](vpn-gateway-vnet-vnet-rm-ps.md).</span></span> <span data-ttu-id="73031-197">請務必在建立連線時新增 "-EnableBgp $True"，才能啟用 BGP。</span><span class="sxs-lookup"><span data-stu-id="73031-197">Make sure you add the "-EnableBgp $True" when creating the connections to enable BGP.</span></span>

#### <a name="1-declare-your-variables"></a><span data-ttu-id="73031-198">1.宣告變數</span><span class="sxs-lookup"><span data-stu-id="73031-198">1. Declare your variables</span></span>

<span data-ttu-id="73031-199">請務必使用您想用於設定的值來取代該值。</span><span class="sxs-lookup"><span data-stu-id="73031-199">Be sure to replace the values with the ones that you want to use for your configuration.</span></span>

```powershell
$RG2 = "TestBGPRG2"
$Location2 = "West US"
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
$GWIPName2 = "VNet2GWIP"
$GWIPconfName2 = "gwipconf2"
$Connection21 = "VNet2toVNet1"
$Connection12 = "VNet1toVNet2"
```

#### <a name="2-create-testvnet2-in-the-new-resource-group"></a><span data-ttu-id="73031-200">2.在新的資源群組中建立 TestVNet2</span><span class="sxs-lookup"><span data-stu-id="73031-200">2. Create TestVNet2 in the new resource group</span></span>

```powershell
New-AzureRmResourceGroup -Name $RG2 -Location $Location2

$fesub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName2 -AddressPrefix $FESubPrefix2
$besub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName2 -AddressPrefix $BESubPrefix2
$gwsub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName2 -AddressPrefix $GWSubPrefix2

New-AzureRmVirtualNetwork -Name $VNetName2 -ResourceGroupName $RG2 -Location $Location2 -AddressPrefix $VNetPrefix21,$VNetPrefix22 -Subnet $fesub2,$besub2,$gwsub2
```

#### <a name="3-create-the-vpn-gateway-for-testvnet2-with-bgp-parameters"></a><span data-ttu-id="73031-201">3.使用 BGP 參數建立 TestVNet2 的 VPN 閘道</span><span class="sxs-lookup"><span data-stu-id="73031-201">3. Create the VPN gateway for TestVNet2 with BGP parameters</span></span>

<span data-ttu-id="73031-202">要求一個公用 IP 位址，以配置給您將建立給 VNet 使用的閘道，並定義必要的子網路和 IP 組態。</span><span class="sxs-lookup"><span data-stu-id="73031-202">Request a public IP address to be allocated to the gateway you will create for your VNet and define the required subnet and IP configurations.</span></span>

```powershell
$gwpip2    = New-AzureRmPublicIpAddress -Name $GWIPName2 -ResourceGroupName $RG2 -Location $Location2 -AllocationMethod Dynamic

$vnet2     = Get-AzureRmVirtualNetwork -Name $VNetName2 -ResourceGroupName $RG2
$subnet2   = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet2
$gwipconf2 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName2 -Subnet $subnet2 -PublicIpAddress $gwpip2
```

<span data-ttu-id="73031-203">透過 AS 號碼建立 VPN 閘道。</span><span class="sxs-lookup"><span data-stu-id="73031-203">Create the VPN gateway with the AS number.</span></span> <span data-ttu-id="73031-204">您必須覆寫您 Azure VPN 閘道上的預設 ASN。</span><span class="sxs-lookup"><span data-stu-id="73031-204">You must override the default ASN on your Azure VPN gateways.</span></span> <span data-ttu-id="73031-205">已連接 VNet 的 ASN 必須不同，才能啟用 BGP 與傳輸路由。</span><span class="sxs-lookup"><span data-stu-id="73031-205">The ASNs for the connected VNets must be different to enable BGP and transit routing.</span></span>

```powershell
New-AzureRmVirtualNetworkGateway -Name $GWName2 -ResourceGroupName $RG2 -Location $Location2 -IpConfigurations $gwipconf2 -GatewayType Vpn -VpnType RouteBased -GatewaySku Standard -Asn $VNet2ASN
```

### <a name="step-2---connect-the-testvnet1-and-testvnet2-gateways"></a><span data-ttu-id="73031-206">步驟 2 - 連接 TestVNet1 與 TestVNet2 閘道</span><span class="sxs-lookup"><span data-stu-id="73031-206">Step 2 - Connect the TestVNet1 and TestVNet2 gateways</span></span>

<span data-ttu-id="73031-207">在此範例中，兩個閘道位於相同的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="73031-207">In this example, both gateways are in the same subscription.</span></span> <span data-ttu-id="73031-208">您可以在相同的 PowerShell 工作階段中完成此步驟。</span><span class="sxs-lookup"><span data-stu-id="73031-208">You can complete this step in the same PowerShell session.</span></span>

#### <a name="1-get-both-gateways"></a><span data-ttu-id="73031-209">1.取得兩個閘道</span><span class="sxs-lookup"><span data-stu-id="73031-209">1. Get both gateways</span></span>

<span data-ttu-id="73031-210">請確定您已登入並連接到訂用帳戶 1。</span><span class="sxs-lookup"><span data-stu-id="73031-210">Make sure you log in and connect to Subscription 1.</span></span>

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
$vnet2gw = Get-AzureRmVirtualNetworkGateway -Name $GWName2 -ResourceGroupName $RG2
```

#### <a name="2-create-both-connections"></a><span data-ttu-id="73031-211">2.建立兩個連線</span><span class="sxs-lookup"><span data-stu-id="73031-211">2. Create both connections</span></span>

<span data-ttu-id="73031-212">在此步驟中，您要建立從 TestVNet1 到 TestVNet2 的連線，以及從 TestVNet2 到 TestVNet1 的連線。</span><span class="sxs-lookup"><span data-stu-id="73031-212">In this step, you create the connection from TestVNet1 to TestVNet2, and the connection from TestVNet2 to TestVNet1.</span></span>

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name $Connection12 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -VirtualNetworkGateway2 $vnet2gw -Location $Location1 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3' -EnableBgp $True

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection21 -ResourceGroupName $RG2 -VirtualNetworkGateway1 $vnet2gw -VirtualNetworkGateway2 $vnet1gw -Location $Location2 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3' -EnableBgp $True
```

> [!IMPORTANT]
> <span data-ttu-id="73031-213">請務必對這兩個連線啟用 BGP。</span><span class="sxs-lookup"><span data-stu-id="73031-213">Be sure to enable BGP for BOTH connections.</span></span>
> 
> 

<span data-ttu-id="73031-214">完成這些步驟之後，會在幾分鐘後建立連線。</span><span class="sxs-lookup"><span data-stu-id="73031-214">After completing these steps, the connection is established after a few minutes.</span></span> <span data-ttu-id="73031-215">一旦 VNet 對 VNet 連線完成後，就會啟動 BGP 對等互連工作階段。</span><span class="sxs-lookup"><span data-stu-id="73031-215">The BGP peering session is up once the VNet-to-VNet connection is completed.</span></span>

<span data-ttu-id="73031-216">如果您完成此練習的上述三個部分，就已建立下列網路拓撲︰</span><span class="sxs-lookup"><span data-stu-id="73031-216">If you completed all three parts of this exercise, you have established the following network topology:</span></span>

![VNet 對 VNet 的 BGP](./media/vpn-gateway-bgp-resource-manager-ps/bgp-crosspremv2v.png)

## <a name="next-steps"></a><span data-ttu-id="73031-218">後續步驟</span><span class="sxs-lookup"><span data-stu-id="73031-218">Next steps</span></span>

<span data-ttu-id="73031-219">一旦完成您的連接，就可以將虛擬機器加入您的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="73031-219">Once your connection is complete, you can add virtual machines to your virtual networks.</span></span> <span data-ttu-id="73031-220">請參閱 [建立網站的虛擬機器](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) 以取得相關步驟。</span><span class="sxs-lookup"><span data-stu-id="73031-220">See [Create a Virtual Machine](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) for steps.</span></span>