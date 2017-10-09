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
ms.openlocfilehash: a9d13ae6b319e2efa8965dc2955c9b89ac3fd12b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-bgp-on-azure-vpn-gateways-using-powershell"></a><span data-ttu-id="5f713-103">如何 tooconfigure 上使用 PowerShell 的 Azure VPN 閘道的 BGP</span><span class="sxs-lookup"><span data-stu-id="5f713-103">How tooconfigure BGP on Azure VPN Gateways using PowerShell</span></span>
<span data-ttu-id="5f713-104">本文將告訴您 hello 步驟 tooenable BGP 跨內部部署站台對站 (S2S) VPN 連線和使用 hello Resource Manager 部署模型和 PowerShell 的 VNet 對 VNet 連線。</span><span class="sxs-lookup"><span data-stu-id="5f713-104">This article walks you through hello steps tooenable BGP on a cross-premises Site-to-Site (S2S) VPN connection and a VNet-to-VNet connection using hello Resource Manager deployment model and PowerShell.</span></span>

## <a name="about-bgp"></a><span data-ttu-id="5f713-105">關於 BGP</span><span class="sxs-lookup"><span data-stu-id="5f713-105">About BGP</span></span>
<span data-ttu-id="5f713-106">BGP 是 hello 標準路由通訊協定常用 hello 網際網路 tooexchange 路由和連線資訊中兩個或多個網路之間。</span><span class="sxs-lookup"><span data-stu-id="5f713-106">BGP is hello standard routing protocol commonly used in hello Internet tooexchange routing and reachability information between two or more networks.</span></span> <span data-ttu-id="5f713-107">BGP 啟用 hello Azure VPN 閘道和 BGP 對等體或鄰近項目呼叫您在內部部署 VPN 裝置、 tooexchange 「 路由 」，會通知這兩個閘道 hello 可用性，並且連線的前置詞 toogo 透過 hello 閘道或路由器相關。</span><span class="sxs-lookup"><span data-stu-id="5f713-107">BGP enables hello Azure VPN Gateways and your on-premises VPN devices, called BGP peers or neighbors, tooexchange "routes" that will inform both gateways on hello availability and reachability for those prefixes toogo through hello gateways or routers involved.</span></span> <span data-ttu-id="5f713-108">BGP 也可以啟用傳輸多個網路之間路由傳播路由的 BGP 閘道會從一個 BGP 對等 tooall 學習其他 BGP 對等節點。</span><span class="sxs-lookup"><span data-stu-id="5f713-108">BGP can also enable transit routing among multiple networks by propagating routes a BGP gateway learns from one BGP peer tooall other BGP peers.</span></span>

<span data-ttu-id="5f713-109">請參閱[概觀的 BGP 與 Azure VPN 閘道](vpn-gateway-bgp-overview.md)如需詳細資訊優點 BGP 和 toounderstand hello 技術需求，以及使用 BGP 的考量。</span><span class="sxs-lookup"><span data-stu-id="5f713-109">See [Overview of BGP with Azure VPN Gateways](vpn-gateway-bgp-overview.md) for more discussion on benefits of BGP and toounderstand hello technical requirements and considerations of using BGP.</span></span>

## <a name="getting-started-with-bgp-on-azure-vpn-gateways"></a><span data-ttu-id="5f713-110">開始在 Azure VPN 閘道上使用 BGP</span><span class="sxs-lookup"><span data-stu-id="5f713-110">Getting started with BGP on Azure VPN gateways</span></span>

<span data-ttu-id="5f713-111">這篇文章會引導您 hello 步驟 toodo hello 下列工作：</span><span class="sxs-lookup"><span data-stu-id="5f713-111">This article walks you through hello steps toodo hello following tasks:</span></span>

* [<span data-ttu-id="5f713-112">第 1 部份 - 在 Azure VPN 閘道上啟用 BGP</span><span class="sxs-lookup"><span data-stu-id="5f713-112">Part 1 - Enable BGP on your Azure VPN gateway</span></span>](#enablebgp)
* [<span data-ttu-id="5f713-113">第 2 部份 – 建立與 BGP 的跨單位連線</span><span class="sxs-lookup"><span data-stu-id="5f713-113">Part 2 - Establish a cross-premises connection with BGP</span></span>](#crossprembgp)
* [<span data-ttu-id="5f713-114">第 3 部份 – 建立與 BGP 的 VNet 對 VNet 連線</span><span class="sxs-lookup"><span data-stu-id="5f713-114">Part 3 - Establish a VNet-to-VNet connection with BGP</span></span>](#v2vbgp)

<span data-ttu-id="5f713-115">Hello 指示的每個部分會形成網路連線啟用 BGP 的基本建置組塊。</span><span class="sxs-lookup"><span data-stu-id="5f713-115">Each part of hello instructions forms a basic building block for enabling BGP in your network connectivity.</span></span> <span data-ttu-id="5f713-116">如果您完成所有三個部分，在您建立 hello 拓樸，hello 下列圖表所示：</span><span class="sxs-lookup"><span data-stu-id="5f713-116">If you complete all three parts, you build hello topology as shown in hello following diagram:</span></span>

![BGP 拓樸](./media/vpn-gateway-bgp-resource-manager-ps/bgp-crosspremv2v.png)

<span data-ttu-id="5f713-118">您可以結合部分一起 toobuild 符合您需求的更複雜、 多重躍點，傳輸網路。</span><span class="sxs-lookup"><span data-stu-id="5f713-118">You can combine parts together toobuild a more complex, multi-hop, transit network that meets your needs.</span></span>

## <span data-ttu-id="5f713-119"><a name ="enablebgp"></a>第 1 部-設定上 hello Azure VPN 閘道的 BGP</span><span class="sxs-lookup"><span data-stu-id="5f713-119"><a name ="enablebgp"></a>Part 1 - Configure BGP on hello Azure VPN Gateway</span></span>
<span data-ttu-id="5f713-120">hello 組態步驟將會設定 hello hello Azure VPN 閘道的 BGP 參數 hello 下列圖表所示：</span><span class="sxs-lookup"><span data-stu-id="5f713-120">hello configuration steps set up hello BGP parameters of hello Azure VPN gateway as shown in hello following diagram:</span></span>

![BGP 閘道](./media/vpn-gateway-bgp-resource-manager-ps/bgp-gateway.png)

### <a name="before-you-begin"></a><span data-ttu-id="5f713-122">開始之前</span><span class="sxs-lookup"><span data-stu-id="5f713-122">Before you begin</span></span>
* <span data-ttu-id="5f713-123">請確認您有 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="5f713-123">Verify that you have an Azure subscription.</span></span> <span data-ttu-id="5f713-124">如果您還沒有 Azure 訂用帳戶，則可以啟用 [MSDN 訂戶權益](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/)或註冊[免費帳戶](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="5f713-124">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free account](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="5f713-125">安裝 hello Azure 資源管理員 PowerShell cmdlet。</span><span class="sxs-lookup"><span data-stu-id="5f713-125">Install hello Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="5f713-126">如需安裝 hello PowerShell cmdlet 的詳細資訊，請參閱[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="5f713-126">For more information about installing hello PowerShell cmdlets, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span> 

### <a name="step-1---create-and-configure-vnet1"></a><span data-ttu-id="5f713-127">步驟 1 - 建立及設定 VNet1</span><span class="sxs-lookup"><span data-stu-id="5f713-127">Step 1 - Create and configure VNet1</span></span>
#### <a name="1-declare-your-variables"></a><span data-ttu-id="5f713-128">1.宣告變數</span><span class="sxs-lookup"><span data-stu-id="5f713-128">1. Declare your variables</span></span>
<span data-ttu-id="5f713-129">對於此練習，我們一開始先宣告我們的變數。</span><span class="sxs-lookup"><span data-stu-id="5f713-129">For this exercise, we start by declaring our variables.</span></span> <span data-ttu-id="5f713-130">hello 下列範例會宣告 hello 針對此練習使用 hello 值的變數。</span><span class="sxs-lookup"><span data-stu-id="5f713-130">hello following example declares hello variables using hello values for this exercise.</span></span> <span data-ttu-id="5f713-131">設定用於生產環境時，請以您自己是確定 tooreplace hello 值。</span><span class="sxs-lookup"><span data-stu-id="5f713-131">Be sure tooreplace hello values with your own when configuring for production.</span></span> <span data-ttu-id="5f713-132">如果您正在透過 hello 步驟 toobecome 熟悉這種設定，您可以使用這些變數。</span><span class="sxs-lookup"><span data-stu-id="5f713-132">You can use these variables if you are running through hello steps toobecome familiar with this type of configuration.</span></span> <span data-ttu-id="5f713-133">修改 hello 變數然後複製並貼到您的 PowerShell 主控台。</span><span class="sxs-lookup"><span data-stu-id="5f713-133">Modify hello variables, and then copy and paste into your PowerShell console.</span></span>

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

#### <a name="2-connect-tooyour-subscription-and-create-a-new-resource-group"></a><span data-ttu-id="5f713-134">2.連接 tooyour 訂用帳戶，並建立新的資源群組</span><span class="sxs-lookup"><span data-stu-id="5f713-134">2. Connect tooyour subscription and create a new resource group</span></span>
<span data-ttu-id="5f713-135">toouse hello 資源管理員 cmdlet，請確定切換 tooPowerShell 模式。</span><span class="sxs-lookup"><span data-stu-id="5f713-135">toouse hello Resource Manager cmdlets, Make sure you switch tooPowerShell mode.</span></span> <span data-ttu-id="5f713-136">如需詳細資訊，請參閱 [搭配使用 Windows PowerShell 與 Resource Manager](../powershell-azure-resource-manager.md)。</span><span class="sxs-lookup"><span data-stu-id="5f713-136">For more information, see [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

<span data-ttu-id="5f713-137">開啟 PowerShell 主控台並連接 tooyour 帳戶。</span><span class="sxs-lookup"><span data-stu-id="5f713-137">Open your PowerShell console and connect tooyour account.</span></span> <span data-ttu-id="5f713-138">使用下列範例 toohelp 您連接的 hello:</span><span class="sxs-lookup"><span data-stu-id="5f713-138">Use hello following sample toohelp you connect:</span></span>

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionName $Sub1
New-AzureRmResourceGroup -Name $RG1 -Location $Location1
```

#### <a name="3-create-testvnet1"></a><span data-ttu-id="5f713-139">3.建立 TestVNet1</span><span class="sxs-lookup"><span data-stu-id="5f713-139">3. Create TestVNet1</span></span>
<span data-ttu-id="5f713-140">hello 下列範例會建立名為 TestVNet1 三個子網路，一個稱為的 GatewaySubnet、 一個稱為的前端和一個被呼叫後端的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="5f713-140">hello following sample creates a virtual network named TestVNet1 and three subnets, one called GatewaySubnet, one called FrontEnd, and one called Backend.</span></span> <span data-ttu-id="5f713-141">替代值時，務必一律將您的閘道子網路特定命名為 GatewaySubnet。</span><span class="sxs-lookup"><span data-stu-id="5f713-141">When substituting values, it's important that you always name your gateway subnet specifically GatewaySubnet.</span></span> <span data-ttu-id="5f713-142">如果您將其命名為其他名稱，閘道建立會失敗。</span><span class="sxs-lookup"><span data-stu-id="5f713-142">If you name it something else, your gateway creation fails.</span></span>

```powershell
$fesub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName1 -AddressPrefix $FESubPrefix1 $besub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName1 -AddressPrefix $BESubPrefix1
$gwsub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName1 -AddressPrefix $GWSubPrefix1

New-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1 -Location $Location1 -AddressPrefix $VNetPrefix11,$VNetPrefix12 -Subnet $fesub1,$besub1,$gwsub1
```

### <a name="step-2---create-hello-vpn-gateway-for-testvnet1-with-bgp-parameters"></a><span data-ttu-id="5f713-143">步驟 2-建立 TestVNet1 hello VPN 閘道的 BGP 參數與</span><span class="sxs-lookup"><span data-stu-id="5f713-143">Step 2 - Create hello VPN Gateway for TestVNet1 with BGP parameters</span></span>
#### <a name="1-create-hello-ip-and-subnet-configurations"></a><span data-ttu-id="5f713-144">1.建立 hello IP 和子網路組態</span><span class="sxs-lookup"><span data-stu-id="5f713-144">1. Create hello IP and subnet configurations</span></span>
<span data-ttu-id="5f713-145">要求的公用 IP 位址 toobe 配置的 toohello 閘道您將建立您的 VNet。</span><span class="sxs-lookup"><span data-stu-id="5f713-145">Request a public IP address toobe allocated toohello gateway you will create for your VNet.</span></span> <span data-ttu-id="5f713-146">您也會定義所需的 hello 子網路和 IP 組態。</span><span class="sxs-lookup"><span data-stu-id="5f713-146">You'll also define hello required subnet and IP configurations.</span></span>

```powershell
$gwpip1 = New-AzureRmPublicIpAddress -Name $GWIPName1 -ResourceGroupName $RG1 -Location $Location1 -AllocationMethod Dynamic

$vnet1 = Get-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1
$subnet1 = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet1
$gwipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName1 -Subnet $subnet1 -PublicIpAddress $gwpip1
```

#### <a name="2-create-hello-vpn-gateway-with-hello-as-number"></a><span data-ttu-id="5f713-147">2.Hello VPN 閘道建立 hello 與數字</span><span class="sxs-lookup"><span data-stu-id="5f713-147">2. Create hello VPN gateway with hello AS number</span></span>
<span data-ttu-id="5f713-148">建立 TestVNet1 hello 虛擬網路閘道。</span><span class="sxs-lookup"><span data-stu-id="5f713-148">Create hello virtual network gateway for TestVNet1.</span></span> <span data-ttu-id="5f713-149">BGP TestVNet1 需要路由式 VPN 閘道，以及 hello 加入參數-Asn，tooset hello ASN （AS 號碼）。</span><span class="sxs-lookup"><span data-stu-id="5f713-149">BGP requires a Route-Based VPN gateway, and also hello addition parameter, -Asn, tooset hello ASN (AS Number) for TestVNet1.</span></span> <span data-ttu-id="5f713-150">如果您未設定 hello ASN 參數，會指派 ASN 65515。</span><span class="sxs-lookup"><span data-stu-id="5f713-150">If you do not set hello ASN parameter, ASN 65515 is assigned.</span></span> <span data-ttu-id="5f713-151">建立閘道可能需要一段 （30 分鐘或更多 toocomplete）。</span><span class="sxs-lookup"><span data-stu-id="5f713-151">Creating a gateway can take a while (30 minutes or more toocomplete).</span></span>

```powershell
New-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1 -Location $Location1 -IpConfigurations $gwipconf1 -GatewayType Vpn -VpnType RouteBased -GatewaySku HighPerformance -Asn $VNet1ASN
```

#### <a name="3-obtain-hello-azure-bgp-peer-ip-address"></a><span data-ttu-id="5f713-152">3.取得 hello Azure BGP 對等 IP 位址</span><span class="sxs-lookup"><span data-stu-id="5f713-152">3. Obtain hello Azure BGP Peer IP address</span></span>
<span data-ttu-id="5f713-153">一旦建立 hello 閘道之後，您會需要 hello Azure VPN 閘道 tooobtain hello BGP 對等 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="5f713-153">Once hello gateway is created, you need tooobtain hello BGP Peer IP address on hello Azure VPN Gateway.</span></span> <span data-ttu-id="5f713-154">這個位址會是需要的 tooconfigure hello Azure VPN 閘道的 BGP 對等內部部署 VPN 裝置為。</span><span class="sxs-lookup"><span data-stu-id="5f713-154">This address is needed tooconfigure hello Azure VPN Gateway as a BGP Peer for your on-premises VPN devices.</span></span>

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
$vnet1gw.BgpSettingsText
```

<span data-ttu-id="5f713-155">hello 最後一個命令會顯示 hello 對應 BGP 設定上 hello Azure VPN 閘道。例如：</span><span class="sxs-lookup"><span data-stu-id="5f713-155">hello last command shows hello corresponding BGP configurations on hello Azure VPN Gateway; for example:</span></span>

```powershell
$vnet1gw.BgpSettingsText
{
    "Asn": 65010,
    "BgpPeeringAddress": "10.12.255.30",
    "PeerWeight": 0
}
```

<span data-ttu-id="5f713-156">一旦建立 hello 閘道之後，您可以使用此閘道 tooestablish 跨單位連線或 VNet 對 VNet 連線 bgp。</span><span class="sxs-lookup"><span data-stu-id="5f713-156">Once hello gateway is created, you can use this gateway tooestablish cross-premises connection or VNet-to-VNet connection with BGP.</span></span> <span data-ttu-id="5f713-157">hello 下列各節逐步解說 hello 步驟 toocomplete hello 練習。</span><span class="sxs-lookup"><span data-stu-id="5f713-157">hello following sections walk through hello steps toocomplete hello exercise.</span></span>

## <span data-ttu-id="5f713-158"><a name ="crossprembbgp"></a>第 2 部份 – 建立與 BGP 的跨單位連線</span><span class="sxs-lookup"><span data-stu-id="5f713-158"><a name ="crossprembbgp"></a>Part 2 - Establish a cross-premises connection with BGP</span></span>

<span data-ttu-id="5f713-159">您需要 toocreate 本機網路閘道 toorepresent tooestablish 跨單位連線，在內部部署 VPN 裝置，以及與 hello 本機網路閘道連線 tooconnect hello VPN 閘道。</span><span class="sxs-lookup"><span data-stu-id="5f713-159">tooestablish a cross-premises connection, you need toocreate a Local Network Gateway toorepresent your on-premises VPN device, and a Connection tooconnect hello VPN gateway with hello local network gateway.</span></span> <span data-ttu-id="5f713-160">文章會引導您完成這些步驟時，本文章包含 hello 其他內容需要的 toospecify hello BGP 設定參數。</span><span class="sxs-lookup"><span data-stu-id="5f713-160">While there are articles that walk you through these steps, this article contains hello additional properties required toospecify hello BGP configuration parameters.</span></span>

![跨單位的 BGP](./media/vpn-gateway-bgp-resource-manager-ps/bgp-crossprem.png)

<span data-ttu-id="5f713-162">在繼續之前，請確定您已完成本練習的[第 1 部分](#enablebgp)。</span><span class="sxs-lookup"><span data-stu-id="5f713-162">Before proceeding, make sure you have completed [Part 1](#enablebgp) of this exercise.</span></span>

### <a name="step-1---create-and-configure-hello-local-network-gateway"></a><span data-ttu-id="5f713-163">步驟 1-建立和設定 hello 區域網路閘道</span><span class="sxs-lookup"><span data-stu-id="5f713-163">Step 1 - Create and configure hello local network gateway</span></span>

#### <a name="1-declare-your-variables"></a><span data-ttu-id="5f713-164">1.宣告變數</span><span class="sxs-lookup"><span data-stu-id="5f713-164">1. Declare your variables</span></span>

<span data-ttu-id="5f713-165">這個練習會繼續 toobuild hello 組態 hello 圖所示。</span><span class="sxs-lookup"><span data-stu-id="5f713-165">This exercise continues toobuild hello configuration shown in hello diagram.</span></span> <span data-ttu-id="5f713-166">為確定 tooreplace 以 hello 的 hello 值的 toouse 您的組態。</span><span class="sxs-lookup"><span data-stu-id="5f713-166">Be sure tooreplace hello values with hello ones that you want toouse for your configuration.</span></span>

```powershell
$RG5 = "TestBGPRG5"
$Location5 = "East US 2"
$LNGName5 = "Site5"
$LNGPrefix50 = "10.52.255.254/32"
$LNGIP5 = "Your_VPN_Device_IP"
$LNGASN5 = 65050
$BGPPeerIP5 = "10.52.255.254"
```

<span data-ttu-id="5f713-167">幾個事項 toonote 有關 hello 本機網路閘道參數：</span><span class="sxs-lookup"><span data-stu-id="5f713-167">A couple of things toonote regarding hello local network gateway parameters:</span></span>

* <span data-ttu-id="5f713-168">hello 區域網路閘道可以是 hello 相同或不同的位置和資源群組為 hello VPN 閘道。</span><span class="sxs-lookup"><span data-stu-id="5f713-168">hello local network gateway can be in hello same or different location and resource group as hello VPN gateway.</span></span> <span data-ttu-id="5f713-169">此範例會顯示它們位於不同位置的不同資源群組中。</span><span class="sxs-lookup"><span data-stu-id="5f713-169">This example shows them in different resource groups in different locations.</span></span>
* <span data-ttu-id="5f713-170">hello 區域網路閘道所需 toodeclare hello 最小前置詞是 hello 您 BGP 對等 IP 位址的 VPN 裝置上的主機位址。</span><span class="sxs-lookup"><span data-stu-id="5f713-170">hello minimum prefix you need toodeclare for hello local network gateway is hello host address of your BGP Peer IP address on your VPN device.</span></span> <span data-ttu-id="5f713-171">在此情況下是 "10.52.255.254/32" 的前置詞 /32。</span><span class="sxs-lookup"><span data-stu-id="5f713-171">In this case, it's a /32 prefix of "10.52.255.254/32".</span></span>
* <span data-ttu-id="5f713-172">提醒您，您必須在內部部署網路與 Azure VNet 之間使用不同的 BGP ASN。</span><span class="sxs-lookup"><span data-stu-id="5f713-172">As a reminder, you must use different BGP ASNs between your on-premises networks and Azure VNet.</span></span> <span data-ttu-id="5f713-173">如果它們是 hello 相同，則需要 toochange VNet ASN 在內部部署 VPN 裝置已使用 hello ASN toopeer 與其他 BGP 芳鄰。</span><span class="sxs-lookup"><span data-stu-id="5f713-173">If they are hello same, you need toochange your VNet ASN if your on-premises VPN device already uses hello ASN toopeer with other BGP neighbors.</span></span>

<span data-ttu-id="5f713-174">在繼續之前，請確認您仍連線的 tooSubscription 1。</span><span class="sxs-lookup"><span data-stu-id="5f713-174">Before you continue, make sure you are still connected tooSubscription 1.</span></span>

#### <a name="2-create-hello-local-network-gateway-for-site5"></a><span data-ttu-id="5f713-175">2.建立 Site5 hello 區域網路閘道</span><span class="sxs-lookup"><span data-stu-id="5f713-175">2. Create hello local network gateway for Site5</span></span>

<span data-ttu-id="5f713-176">如果它不建立，在建立 hello 區域網路閘道之前，是確定 toocreate hello 資源群組。</span><span class="sxs-lookup"><span data-stu-id="5f713-176">Be sure toocreate hello resource group if it is not created, before you create hello local network gateway.</span></span> <span data-ttu-id="5f713-177">請注意 hello 本機網路閘道的 hello 兩個額外的參數： Asn 與 BgpPeerAddress。</span><span class="sxs-lookup"><span data-stu-id="5f713-177">Notice hello two additional parameters for hello local network gateway: Asn and BgpPeerAddress.</span></span>

```powershell
New-AzureRmResourceGroup -Name $RG5 -Location $Location5

New-AzureRmLocalNetworkGateway -Name $LNGName5 -ResourceGroupName $RG5 -Location $Location5 -GatewayIpAddress $LNGIP5 -AddressPrefix $LNGPrefix50 -Asn $LNGASN5 -BgpPeeringAddress $BGPPeerIP5
```

### <a name="step-2---connect-hello-vnet-gateway-and-local-network-gateway"></a><span data-ttu-id="5f713-178">步驟 2-連接 hello VNet 閘道與區域網路閘道</span><span class="sxs-lookup"><span data-stu-id="5f713-178">Step 2 - Connect hello VNet gateway and local network gateway</span></span>

#### <a name="1-get-hello-two-gateways"></a><span data-ttu-id="5f713-179">1.取得 hello 這兩個閘道</span><span class="sxs-lookup"><span data-stu-id="5f713-179">1. Get hello two gateways</span></span>

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$lng5gw  = Get-AzureRmLocalNetworkGateway -Name $LNGName5 -ResourceGroupName $RG5
```

#### <a name="2-create-hello-testvnet1-toosite5-connection"></a><span data-ttu-id="5f713-180">2.建立 hello TestVNet1 tooSite5 連線</span><span class="sxs-lookup"><span data-stu-id="5f713-180">2. Create hello TestVNet1 tooSite5 connection</span></span>

<span data-ttu-id="5f713-181">在此步驟中，您會從 TestVNet1 tooSite5 建立 hello 連線。</span><span class="sxs-lookup"><span data-stu-id="5f713-181">In this step, you create hello connection from TestVNet1 tooSite5.</span></span> <span data-ttu-id="5f713-182">您必須指定"-EnableBGP $True"tooenable BGP 此連線。</span><span class="sxs-lookup"><span data-stu-id="5f713-182">You must specify "-EnableBGP $True" tooenable BGP for this connection.</span></span> <span data-ttu-id="5f713-183">如同先前討論，很可能 toohave BGP 和非 BGP 連接 hello 相同 Azure VPN 閘道。</span><span class="sxs-lookup"><span data-stu-id="5f713-183">As discussed earlier, it is possible toohave both BGP and non-BGP connections for hello same Azure VPN Gateway.</span></span> <span data-ttu-id="5f713-184">除非 hello 連接屬性中啟用 BGP，Azure 將不會啟用 BGP 此連線的即使已設定兩個閘道的 BGP 參數。</span><span class="sxs-lookup"><span data-stu-id="5f713-184">Unless BGP is enabled in hello connection property, Azure will not enable BGP for this connection even though BGP parameters are already configured on both gateways.</span></span>

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name $Connection15 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng5gw -Location $Location1 -ConnectionType IPsec -SharedKey 'AzureA1b2C3' -EnableBGP $True
```

<span data-ttu-id="5f713-185">hello 下列範例會列出您針對此練習在內部部署 VPN 裝置輸入 hello BGP 組態區段的 hello 參數：</span><span class="sxs-lookup"><span data-stu-id="5f713-185">hello following example lists hello parameters you enter into hello BGP configuration section on your on-premises VPN device for this exercise:</span></span>

```

- Site5 ASN            : 65050
- Site5 BGP IP         : 10.52.255.254
- Prefixes tooannounce : (for example) 10.51.0.0/16 and 10.52.0.0/16
- Azure VNet ASN       : 65010
- Azure VNet BGP IP    : 10.12.255.30
- Static route         : Add a route for 10.12.255.30/32, with nexthop being hello VPN tunnel interface on your device
- eBGP Multihop        : Ensure hello "multihop" option for eBGP is enabled on your device if needed
```

<span data-ttu-id="5f713-186">一旦建立之後 IPsec 連線 hello 幾分鐘的時間和 hello BGP 對等互連工作階段開始之後建立 hello 連接。</span><span class="sxs-lookup"><span data-stu-id="5f713-186">hello connection is established after a few minutes, and hello BGP peering session starts once hello IPsec connection is established.</span></span>

## <span data-ttu-id="5f713-187"><a name ="v2vbgp"></a>第 3 部份 – 建立與 BGP 的 VNet 對 VNet 連線</span><span class="sxs-lookup"><span data-stu-id="5f713-187"><a name ="v2vbgp"></a>Part 3 - Establish a VNet-to-VNet connection with BGP</span></span>

<span data-ttu-id="5f713-188">本節將 VNet 對 VNet 連線 bgp，新增 hello 下列圖表所示：</span><span class="sxs-lookup"><span data-stu-id="5f713-188">This section adds a VNet-to-VNet connection with BGP, as shown in hello following diagram:</span></span>

![VNet 對 VNet 的 BGP](./media/vpn-gateway-bgp-resource-manager-ps/bgp-vnet2vnet.png)

<span data-ttu-id="5f713-190">下列指示的 hello 繼續 hello 上一個步驟。</span><span class="sxs-lookup"><span data-stu-id="5f713-190">hello following instructions continue from hello previous steps.</span></span> <span data-ttu-id="5f713-191">您必須先完成[第 I 部分](#enablebgp)toocreate 並設定 TestVNet1 hello bgp 的 VPN 閘道。</span><span class="sxs-lookup"><span data-stu-id="5f713-191">You must complete [Part I](#enablebgp) toocreate and configure TestVNet1 and hello VPN Gateway with BGP.</span></span> 

### <a name="step-1---create-testvnet2-and-hello-vpn-gateway"></a><span data-ttu-id="5f713-192">步驟 1-建立 TestVNet2 和 hello VPN 閘道</span><span class="sxs-lookup"><span data-stu-id="5f713-192">Step 1 - Create TestVNet2 and hello VPN gateway</span></span>

<span data-ttu-id="5f713-193">它是重要 toomake 確定 hello 新的虛擬網路，TestVNet2，hello IP 位址空間不與任何 VNet 範圍重疊。</span><span class="sxs-lookup"><span data-stu-id="5f713-193">It is important toomake sure that hello IP address space of hello new virtual network, TestVNet2, does not overlap with any of your VNet ranges.</span></span>

<span data-ttu-id="5f713-194">在此範例中，hello 虛擬網路屬於 toohello 相同訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="5f713-194">In this example, hello virtual networks belong toohello same subscription.</span></span> <span data-ttu-id="5f713-195">您可以設定不同訂用帳戶之間的 VNet 對 VNet 連線。</span><span class="sxs-lookup"><span data-stu-id="5f713-195">You can set up VNet-to-VNet connections between different subscriptions.</span></span> <span data-ttu-id="5f713-196">如需詳細資訊，請參閱[設定 VNet 對 VNet 連線](vpn-gateway-vnet-vnet-rm-ps.md)。</span><span class="sxs-lookup"><span data-stu-id="5f713-196">For more information, see [Configure a VNet-to-VNet connection](vpn-gateway-vnet-vnet-rm-ps.md).</span></span> <span data-ttu-id="5f713-197">請確定您新增 hello"的 EnableBgp $True 」 時建立 hello 連線 tooenable BGP。</span><span class="sxs-lookup"><span data-stu-id="5f713-197">Make sure you add hello "-EnableBgp $True" when creating hello connections tooenable BGP.</span></span>

#### <a name="1-declare-your-variables"></a><span data-ttu-id="5f713-198">1.宣告變數</span><span class="sxs-lookup"><span data-stu-id="5f713-198">1. Declare your variables</span></span>

<span data-ttu-id="5f713-199">為確定 tooreplace 以 hello 的 hello 值的 toouse 您的組態。</span><span class="sxs-lookup"><span data-stu-id="5f713-199">Be sure tooreplace hello values with hello ones that you want toouse for your configuration.</span></span>

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

#### <a name="2-create-testvnet2-in-hello-new-resource-group"></a><span data-ttu-id="5f713-200">2.建立 TestVNet2 hello 新資源群組中</span><span class="sxs-lookup"><span data-stu-id="5f713-200">2. Create TestVNet2 in hello new resource group</span></span>

```powershell
New-AzureRmResourceGroup -Name $RG2 -Location $Location2

$fesub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName2 -AddressPrefix $FESubPrefix2
$besub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName2 -AddressPrefix $BESubPrefix2
$gwsub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName2 -AddressPrefix $GWSubPrefix2

New-AzureRmVirtualNetwork -Name $VNetName2 -ResourceGroupName $RG2 -Location $Location2 -AddressPrefix $VNetPrefix21,$VNetPrefix22 -Subnet $fesub2,$besub2,$gwsub2
```

#### <a name="3-create-hello-vpn-gateway-for-testvnet2-with-bgp-parameters"></a><span data-ttu-id="5f713-201">3.建立 TestVNet2 hello VPN 閘道的 BGP 參數與</span><span class="sxs-lookup"><span data-stu-id="5f713-201">3. Create hello VPN gateway for TestVNet2 with BGP parameters</span></span>

<span data-ttu-id="5f713-202">要求的公用 IP 位址 toobe 配置的 toohello 閘道您將為您的 VNet 建立並定義所需的 hello 子網路和 IP 組態。</span><span class="sxs-lookup"><span data-stu-id="5f713-202">Request a public IP address toobe allocated toohello gateway you will create for your VNet and define hello required subnet and IP configurations.</span></span>

```powershell
$gwpip2    = New-AzureRmPublicIpAddress -Name $GWIPName2 -ResourceGroupName $RG2 -Location $Location2 -AllocationMethod Dynamic

$vnet2     = Get-AzureRmVirtualNetwork -Name $VNetName2 -ResourceGroupName $RG2
$subnet2   = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet2
$gwipconf2 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName2 -Subnet $subnet2 -PublicIpAddress $gwpip2
```

<span data-ttu-id="5f713-203">Hello VPN 閘道建立 hello 與數字。</span><span class="sxs-lookup"><span data-stu-id="5f713-203">Create hello VPN gateway with hello AS number.</span></span> <span data-ttu-id="5f713-204">您必須在 Azure VPN 閘道上，以覆寫 hello 預設 ASN。</span><span class="sxs-lookup"><span data-stu-id="5f713-204">You must override hello default ASN on your Azure VPN gateways.</span></span> <span data-ttu-id="5f713-205">hello Asn hello 連線 Vnet 必須是不同 tooenable BGP 和傳輸路由。</span><span class="sxs-lookup"><span data-stu-id="5f713-205">hello ASNs for hello connected VNets must be different tooenable BGP and transit routing.</span></span>

```powershell
New-AzureRmVirtualNetworkGateway -Name $GWName2 -ResourceGroupName $RG2 -Location $Location2 -IpConfigurations $gwipconf2 -GatewayType Vpn -VpnType RouteBased -GatewaySku Standard -Asn $VNet2ASN
```

### <a name="step-2---connect-hello-testvnet1-and-testvnet2-gateways"></a><span data-ttu-id="5f713-206">步驟 2-連接 hello TestVNet1 和 TestVNet2 閘道</span><span class="sxs-lookup"><span data-stu-id="5f713-206">Step 2 - Connect hello TestVNet1 and TestVNet2 gateways</span></span>

<span data-ttu-id="5f713-207">在此範例中，兩個閘道位於 hello 相同訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="5f713-207">In this example, both gateways are in hello same subscription.</span></span> <span data-ttu-id="5f713-208">您可以完成此步驟在 hello 同一個 PowerShell 工作階段。</span><span class="sxs-lookup"><span data-stu-id="5f713-208">You can complete this step in hello same PowerShell session.</span></span>

#### <a name="1-get-both-gateways"></a><span data-ttu-id="5f713-209">1.取得兩個閘道</span><span class="sxs-lookup"><span data-stu-id="5f713-209">1. Get both gateways</span></span>

<span data-ttu-id="5f713-210">請確定您登入，並連接 tooSubscription 1。</span><span class="sxs-lookup"><span data-stu-id="5f713-210">Make sure you log in and connect tooSubscription 1.</span></span>

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
$vnet2gw = Get-AzureRmVirtualNetworkGateway -Name $GWName2 -ResourceGroupName $RG2
```

#### <a name="2-create-both-connections"></a><span data-ttu-id="5f713-211">2.建立兩個連線</span><span class="sxs-lookup"><span data-stu-id="5f713-211">2. Create both connections</span></span>

<span data-ttu-id="5f713-212">在此步驟中，您建立從 TestVNet1 tooTestVNet2 hello 連線與 hello 連線從 TestVNet2 tooTestVNet1。</span><span class="sxs-lookup"><span data-stu-id="5f713-212">In this step, you create hello connection from TestVNet1 tooTestVNet2, and hello connection from TestVNet2 tooTestVNet1.</span></span>

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name $Connection12 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -VirtualNetworkGateway2 $vnet2gw -Location $Location1 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3' -EnableBgp $True

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection21 -ResourceGroupName $RG2 -VirtualNetworkGateway1 $vnet2gw -VirtualNetworkGateway2 $vnet1gw -Location $Location2 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3' -EnableBgp $True
```

> [!IMPORTANT]
> <span data-ttu-id="5f713-213">這兩個連接是確定 tooenable BGP。</span><span class="sxs-lookup"><span data-stu-id="5f713-213">Be sure tooenable BGP for BOTH connections.</span></span>
> 
> 

<span data-ttu-id="5f713-214">完成這些步驟之後，會在幾分鐘後建立 hello 連線。</span><span class="sxs-lookup"><span data-stu-id="5f713-214">After completing these steps, hello connection is established after a few minutes.</span></span> <span data-ttu-id="5f713-215">hello BGP 對等互連工作階段已啟動，一旦完成 hello VNet 對 VNet 連線。</span><span class="sxs-lookup"><span data-stu-id="5f713-215">hello BGP peering session is up once hello VNet-to-VNet connection is completed.</span></span>

<span data-ttu-id="5f713-216">如果您已完成此練習中的所有三個部分，您已建立下列 網路拓樸 hello:</span><span class="sxs-lookup"><span data-stu-id="5f713-216">If you completed all three parts of this exercise, you have established hello following network topology:</span></span>

![VNet 對 VNet 的 BGP](./media/vpn-gateway-bgp-resource-manager-ps/bgp-crosspremv2v.png)

## <a name="next-steps"></a><span data-ttu-id="5f713-218">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5f713-218">Next steps</span></span>

<span data-ttu-id="5f713-219">一旦完成您的連線，您可以將虛擬機器 tooyour 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="5f713-219">Once your connection is complete, you can add virtual machines tooyour virtual networks.</span></span> <span data-ttu-id="5f713-220">請參閱 [建立網站的虛擬機器](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) 以取得相關步驟。</span><span class="sxs-lookup"><span data-stu-id="5f713-220">See [Create a Virtual Machine](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) for steps.</span></span>
