---
title: "連接您在內部部署網路 tooan Azure 虛擬網路： 站對站 VPN: PowerShell |Microsoft 文件"
description: "IPsec 連線從您內部網路 tooan Azure 虛擬網路上的步驟 toocreate hello 公用網際網路。 這些步驟可協助您使用 PowerShell 建立跨單位的站對站 VPN 閘道連線。"
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: fcc2fda5-4493-4c15-9436-84d35adbda8e
ms.service: vpn-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/09/2017
ms.author: cherylmc
ms.openlocfilehash: cb8db1dab3a5488816a7f7e8e63908a4c02f55db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vnet-with-a-site-to-site-vpn-connection-using-powershell"></a><span data-ttu-id="f21b6-104">使用 PowerShell 建立具有站對站 VPN 連接的 VNet</span><span class="sxs-lookup"><span data-stu-id="f21b6-104">Create a VNet with a Site-to-Site VPN connection using PowerShell</span></span>

<span data-ttu-id="f21b6-105">本文章將示範如何 toouse PowerShell toocreate 網站-站台 VPN 閘道連線在內部網路 toohello VNet。</span><span class="sxs-lookup"><span data-stu-id="f21b6-105">This article shows you how toouse PowerShell toocreate a Site-to-Site VPN gateway connection from your on-premises network toohello VNet.</span></span> <span data-ttu-id="f21b6-106">本文章中的 hello 步驟適用於 toohello Resource Manager 部署模型。</span><span class="sxs-lookup"><span data-stu-id="f21b6-106">hello steps in this article apply toohello Resource Manager deployment model.</span></span> <span data-ttu-id="f21b6-107">您也可以建立此組態使用不同的部署工具或部署模型，從下列清單中的 hello 選取不同的選項：</span><span class="sxs-lookup"><span data-stu-id="f21b6-107">You can also create this configuration using a different deployment tool or deployment model by selecting a different option from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="f21b6-108">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="f21b6-108">Azure portal</span></span>](vpn-gateway-howto-site-to-site-resource-manager-portal.md)
> * [<span data-ttu-id="f21b6-109">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f21b6-109">PowerShell</span></span>](vpn-gateway-create-site-to-site-rm-powershell.md)
> * [<span data-ttu-id="f21b6-110">CLI</span><span class="sxs-lookup"><span data-stu-id="f21b6-110">CLI</span></span>](vpn-gateway-howto-site-to-site-resource-manager-cli.md)
> * [<span data-ttu-id="f21b6-111">Azure 入口網站 (傳統)</span><span class="sxs-lookup"><span data-stu-id="f21b6-111">Azure portal (classic)</span></span>](vpn-gateway-howto-site-to-site-classic-portal.md)
> * [<span data-ttu-id="f21b6-112">傳統入口網站 (傳統)</span><span class="sxs-lookup"><span data-stu-id="f21b6-112">Classic portal (classic)</span></span>](vpn-gateway-site-to-site-create.md)
> 
>


<span data-ttu-id="f21b6-113">站對站 VPN 閘道連線是使用的 tooconnect 您內部網路 tooan Azure 虛擬網路透過 VPN IPsec/IKE （IKEv1 或 IKEv2） 通道。</span><span class="sxs-lookup"><span data-stu-id="f21b6-113">A Site-to-Site VPN gateway connection is used tooconnect your on-premises network tooan Azure virtual network over an IPsec/IKE (IKEv1 or IKEv2) VPN tunnel.</span></span> <span data-ttu-id="f21b6-114">這種類型的連線需要 VPN 裝置位於內部部署具有對外開放的公用 IP 位址指派 tooit。</span><span class="sxs-lookup"><span data-stu-id="f21b6-114">This type of connection requires a VPN device located on-premises that has an externally facing public IP address assigned tooit.</span></span> <span data-ttu-id="f21b6-115">如需 VPN 閘道的詳細資訊，請參閱[關於 VPN 閘道](vpn-gateway-about-vpngateways.md)。</span><span class="sxs-lookup"><span data-stu-id="f21b6-115">For more information about VPN gateways, see [About VPN gateway](vpn-gateway-about-vpngateways.md).</span></span>

![站對站 VPN 閘道跨單位連線圖表](./media/vpn-gateway-create-site-to-site-rm-powershell/site-to-site-diagram.png)

## <span data-ttu-id="f21b6-117"><a name="before"></a>開始之前</span><span class="sxs-lookup"><span data-stu-id="f21b6-117"><a name="before"></a>Before you begin</span></span>

<span data-ttu-id="f21b6-118">請確認您已符合下列準則，開始您的組態之前 hello:</span><span class="sxs-lookup"><span data-stu-id="f21b6-118">Verify that you have met hello following criteria before beginning your configuration:</span></span>

* <span data-ttu-id="f21b6-119">請確定您擁有相容的 VPN 裝置和人能夠 tooconfigure 它。</span><span class="sxs-lookup"><span data-stu-id="f21b6-119">Make sure you have a compatible VPN device and someone who is able tooconfigure it.</span></span> <span data-ttu-id="f21b6-120">如需相容 VPN 裝置和裝置組態的詳細資訊，請參閱[關於 VPN 裝置](vpn-gateway-about-vpn-devices.md)。</span><span class="sxs-lookup"><span data-stu-id="f21b6-120">For more information about compatible VPN devices and device configuration, see [About VPN Devices](vpn-gateway-about-vpn-devices.md).</span></span>
* <span data-ttu-id="f21b6-121">確認您的 VPN 裝置有對外開放的公用 IPv4 位址。</span><span class="sxs-lookup"><span data-stu-id="f21b6-121">Verify that you have an externally facing public IPv4 address for your VPN device.</span></span> <span data-ttu-id="f21b6-122">此 IP 位址不能位於 NAT 後方。</span><span class="sxs-lookup"><span data-stu-id="f21b6-122">This IP address cannot be located behind a NAT.</span></span>
* <span data-ttu-id="f21b6-123">如果您不熟悉 hello IP 位址範圍位於內部網路組態，您需要 toocoordinate 的人可以為您提供這些詳細資料。</span><span class="sxs-lookup"><span data-stu-id="f21b6-123">If you are unfamiliar with hello IP address ranges located in your on-premises network configuration, you need toocoordinate with someone who can provide those details for you.</span></span> <span data-ttu-id="f21b6-124">當您建立此設定時，您必須指定 hello IP 位址範圍前置詞，則 Azure 會路由傳送 tooyour 在內部部署位置。</span><span class="sxs-lookup"><span data-stu-id="f21b6-124">When you create this configuration, you must specify hello IP address range prefixes that Azure will route tooyour on-premises location.</span></span> <span data-ttu-id="f21b6-125">無 hello 的內部部署網路的子網路可以透過圈具有您想要 tooconnect hello 虛擬網路子網路。</span><span class="sxs-lookup"><span data-stu-id="f21b6-125">None of hello subnets of your on-premises network can over lap with hello virtual network subnets that you want tooconnect to.</span></span>
* <span data-ttu-id="f21b6-126">安裝 hello hello Azure 資源管理員的 PowerShell 指令程式最新版本。</span><span class="sxs-lookup"><span data-stu-id="f21b6-126">Install hello latest version of hello Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="f21b6-127">PowerShell 指令程式會經常更新，您通常需要 tooupdate 您 PowerShell cmdlet tooget hello 最新功能的功能。</span><span class="sxs-lookup"><span data-stu-id="f21b6-127">PowerShell cmdlets are updated frequently and you will typically need tooupdate your PowerShell cmdlets tooget hello latest feature functionality.</span></span> <span data-ttu-id="f21b6-128">如果您沒有更新您的 PowerShell cmdlet，指定 hello 值可能會失敗。</span><span class="sxs-lookup"><span data-stu-id="f21b6-128">If you don't update your PowerShell cmdlets, hello values specified may fail.</span></span> <span data-ttu-id="f21b6-129">請參閱[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)如需有關下載和安裝 PowerShell cmdlet。</span><span class="sxs-lookup"><span data-stu-id="f21b6-129">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for more information about downloading and installing PowerShell cmdlets.</span></span>

### <span data-ttu-id="f21b6-130"><a name="example"></a>範例值</span><span class="sxs-lookup"><span data-stu-id="f21b6-130"><a name="example"></a>Example values</span></span>

<span data-ttu-id="f21b6-131">本文章中的 hello 範例會使用下列值的 hello。</span><span class="sxs-lookup"><span data-stu-id="f21b6-131">hello examples in this article use hello following values.</span></span> <span data-ttu-id="f21b6-132">您可以使用這些值 toocreate 測試環境中，或參閱 toothem toobetter 了解這篇文章中的 hello 範例。</span><span class="sxs-lookup"><span data-stu-id="f21b6-132">You can use these values toocreate a test environment, or refer toothem toobetter understand hello examples in this article.</span></span>

```
#Example values

VnetName                = TestVNet1
ResourceGroup           = TestRG1
Location                = East US 
AddressSpace            = 10.11.0.0/16 
SubnetName              = Subnet1 
Subnet                  = 10.11.1.0/28 
GatewaySubnet           = 10.11.0.0/27
LocalNetworkGatewayName = Site2
LNG Public IP           = <VPN device IP address> 
Local Address Prefixes  = 10.0.0.0/24, 20.0.0.0/24
Gateway Name            = VNet1GW
PublicIP                = VNet1GWIP
Gateway IP Config       = gwipconfig1 
VPNType                 = RouteBased 
GatewayType             = Vpn 
ConnectionName          = VNet1toSite2

```


## <span data-ttu-id="f21b6-133"><a name="Login"></a>1.連接 tooyour 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="f21b6-133"><a name="Login"></a>1. Connect tooyour subscription</span></span>

[!INCLUDE [PowerShell login](../../includes/vpn-gateway-ps-login-include.md)]

## <span data-ttu-id="f21b6-134"><a name="VNet"></a>2.建立虛擬網路和閘道器子網路</span><span class="sxs-lookup"><span data-stu-id="f21b6-134"><a name="VNet"></a>2. Create a virtual network and a gateway subnet</span></span>

<span data-ttu-id="f21b6-135">如果您還沒有虛擬網路，請建立一個。</span><span class="sxs-lookup"><span data-stu-id="f21b6-135">If you don't already have a virtual network, create one.</span></span> <span data-ttu-id="f21b6-136">當建立虛擬網路，請確定 hello 您指定的位址空間不將任何您已在內部部署網路的 hello 位址空間重疊。</span><span class="sxs-lookup"><span data-stu-id="f21b6-136">When creating a virtual network, make sure that hello address spaces you specify don't overlap any of hello address spaces that you have on your on-premises network.</span></span>

[!INCLUDE [About gateway subnets](../../includes/vpn-gateway-about-gwsubnet-include.md)]

[!INCLUDE [No NSG warning](../../includes/vpn-gateway-no-nsg-include.md)]

### <span data-ttu-id="f21b6-137"><a name="vnet"></a>toocreate 虛擬網路和閘道子網路</span><span class="sxs-lookup"><span data-stu-id="f21b6-137"><a name="vnet"></a>toocreate a virtual network and a gateway subnet</span></span>

<span data-ttu-id="f21b6-138">此範例會建立虛擬網路和閘道子網路。</span><span class="sxs-lookup"><span data-stu-id="f21b6-138">This example creates a virtual network and a gateway subnet.</span></span> <span data-ttu-id="f21b6-139">如果您已經有虛擬網路，您需要閘道子網路，請參閱 tooadd [tooadd 閘道子網路 tooa 虛擬網路已經建立](#gatewaysubnet)。</span><span class="sxs-lookup"><span data-stu-id="f21b6-139">If you already have a virtual network that you need tooadd a gateway subnet to, see [tooadd a gateway subnet tooa virtual network you have already created](#gatewaysubnet).</span></span>

<span data-ttu-id="f21b6-140">建立資源群組：</span><span class="sxs-lookup"><span data-stu-id="f21b6-140">Create a resource group:</span></span>

```powershell
New-AzureRmResourceGroup -Name TestRG1 -Location 'East US'
```

<span data-ttu-id="f21b6-141">建立虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="f21b6-141">Create your virtual network.</span></span>

1. <span data-ttu-id="f21b6-142">設定 hello 變數。</span><span class="sxs-lookup"><span data-stu-id="f21b6-142">Set hello variables.</span></span>

  ```powershell
  $subnet1 = New-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -AddressPrefix 10.11.0.0/27
  $subnet2 = New-AzureRmVirtualNetworkSubnetConfig -Name 'Subnet1' -AddressPrefix 10.11.1.0/28
  ```
2. <span data-ttu-id="f21b6-143">建立 hello VNet。</span><span class="sxs-lookup"><span data-stu-id="f21b6-143">Create hello VNet.</span></span>

  ```powershell
  New-AzureRmVirtualNetwork -Name TestVNet1 -ResourceGroupName TestRG1 `
  -Location 'East US' -AddressPrefix 10.11.0.0/16 -Subnet $subnet1, $subnet2
  ```

### <span data-ttu-id="f21b6-144"><a name="gatewaysubnet"></a>tooadd 閘道子網路 tooa 虛擬網路已經建立</span><span class="sxs-lookup"><span data-stu-id="f21b6-144"><a name="gatewaysubnet"></a>tooadd a gateway subnet tooa virtual network you have already created</span></span>

1. <span data-ttu-id="f21b6-145">設定 hello 變數。</span><span class="sxs-lookup"><span data-stu-id="f21b6-145">Set hello variables.</span></span>

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -ResourceGroupName TestRG1 -Name TestVet1
  ```
2. <span data-ttu-id="f21b6-146">建立 hello 閘道子網路。</span><span class="sxs-lookup"><span data-stu-id="f21b6-146">Create hello gateway subnet.</span></span>

  ```powershell
  Add-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -AddressPrefix 10.11.0.0/27 -VirtualNetwork $vnet
  ```
3. <span data-ttu-id="f21b6-147">將 hello 組態設定。</span><span class="sxs-lookup"><span data-stu-id="f21b6-147">Set hello configuration.</span></span>

  ```powershell
  Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
  ```

## <span data-ttu-id="f21b6-148">3.<a name="localnet"></a>建立 hello 區域網路閘道</span><span class="sxs-lookup"><span data-stu-id="f21b6-148">3. <a name="localnet"></a>Create hello local network gateway</span></span>

<span data-ttu-id="f21b6-149">hello 區域網路閘道通常是指 tooyour 在內部部署位置。</span><span class="sxs-lookup"><span data-stu-id="f21b6-149">hello local network gateway typically refers tooyour on-premises location.</span></span> <span data-ttu-id="f21b6-150">您提供 hello 站台的名稱之 Azure 可以參考 tooit，然後指定 hello IP 位址的 hello 在內部部署 VPN 裝置 toowhich 中，您將建立連接。</span><span class="sxs-lookup"><span data-stu-id="f21b6-150">You give hello site a name by which Azure can refer tooit, then specify hello IP address of hello on-premises VPN device toowhich you will create a connection.</span></span> <span data-ttu-id="f21b6-151">您也指定 hello 而必須路由傳送透過 hello VPN 閘道 toohello VPN 裝置 IP 位址首碼。</span><span class="sxs-lookup"><span data-stu-id="f21b6-151">You also specify hello IP address prefixes that will be routed through hello VPN gateway toohello VPN device.</span></span> <span data-ttu-id="f21b6-152">您指定的 hello 位址前置詞是在內部部署網路上的 hello 前置詞。</span><span class="sxs-lookup"><span data-stu-id="f21b6-152">hello address prefixes you specify are hello prefixes located on your on-premises network.</span></span> <span data-ttu-id="f21b6-153">如果您在內部部署網路變更時，您可以輕鬆地更新 hello 前置詞。</span><span class="sxs-lookup"><span data-stu-id="f21b6-153">If your on-premises network changes, you can easily update hello prefixes.</span></span>

<span data-ttu-id="f21b6-154">使用下列值的 hello:</span><span class="sxs-lookup"><span data-stu-id="f21b6-154">Use hello following values:</span></span>

* <span data-ttu-id="f21b6-155">hello *GatewayIPAddress*是 hello 在內部部署 VPN 裝置 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="f21b6-155">hello *GatewayIPAddress* is hello IP address of your on-premises VPN device.</span></span> <span data-ttu-id="f21b6-156">VPN 裝置不能位於 NAT 後方。</span><span class="sxs-lookup"><span data-stu-id="f21b6-156">Your VPN device cannot be located behind a NAT.</span></span>
* <span data-ttu-id="f21b6-157">hello *AddressPrefix*是內部位址空間。</span><span class="sxs-lookup"><span data-stu-id="f21b6-157">hello *AddressPrefix* is your on-premises address space.</span></span>

<span data-ttu-id="f21b6-158">tooadd 區域網路閘道與單一位址前置詞：</span><span class="sxs-lookup"><span data-stu-id="f21b6-158">tooadd a local network gateway with a single address prefix:</span></span>

  ```powershell
  New-AzureRmLocalNetworkGateway -Name Site2 -ResourceGroupName TestRG1 `
  -Location 'East US' -GatewayIpAddress '23.99.221.164' -AddressPrefix '10.0.0.0/24'
  ```

<span data-ttu-id="f21b6-159">tooadd 區域網路閘道與多個位址前置詞：</span><span class="sxs-lookup"><span data-stu-id="f21b6-159">tooadd a local network gateway with multiple address prefixes:</span></span>

  ```powershell
  New-AzureRmLocalNetworkGateway -Name Site2 -ResourceGroupName TestRG1 `
  -Location 'East US' -GatewayIpAddress '23.99.221.164' -AddressPrefix @('10.0.0.0/24','20.0.0.0/24')
  ```

<span data-ttu-id="f21b6-160">toomodify 區域網路閘道的 IP 位址前置詞：</span><span class="sxs-lookup"><span data-stu-id="f21b6-160">toomodify IP address prefixes for your local network gateway:</span></span><br>
<span data-ttu-id="f21b6-161">有時候您的區域網路閘道首碼會有所變更。</span><span class="sxs-lookup"><span data-stu-id="f21b6-161">Sometimes your local network gateway prefixes change.</span></span> <span data-ttu-id="f21b6-162">hello 您採取步驟 toomodify 您前置詞，取決於您是否建立 VPN 閘道連線的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="f21b6-162">hello steps you take toomodify your IP address prefixes depend on whether you have created a VPN gateway connection.</span></span> <span data-ttu-id="f21b6-163">請參閱 hello[修改 IP 位址首碼的區域網路閘道](#modify)本文一節。</span><span class="sxs-lookup"><span data-stu-id="f21b6-163">See hello [Modify IP address prefixes for a local network gateway](#modify) section of this article.</span></span>

## <span data-ttu-id="f21b6-164"><a name="PublicIP"></a>4.要求公用 IP 位址</span><span class="sxs-lookup"><span data-stu-id="f21b6-164"><a name="PublicIP"></a>4. Request a Public IP address</span></span>

<span data-ttu-id="f21b6-165">VPN 閘道必須具有公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="f21b6-165">A VPN gateway must have a Public IP address.</span></span> <span data-ttu-id="f21b6-166">您第一次要求 hello IP 位址資源，並建立您的虛擬網路閘道時參考 tooit。</span><span class="sxs-lookup"><span data-stu-id="f21b6-166">You first request hello IP address resource, and then refer tooit when creating your virtual network gateway.</span></span> <span data-ttu-id="f21b6-167">hello IP 位址建立 hello VPN 閘道時，會動態指定 toohello 資源。</span><span class="sxs-lookup"><span data-stu-id="f21b6-167">hello IP address is dynamically assigned toohello resource when hello VPN gateway is created.</span></span> <span data-ttu-id="f21b6-168">VPN 閘道目前僅支援*動態*公用 IP 位址配置。</span><span class="sxs-lookup"><span data-stu-id="f21b6-168">VPN Gateway currently only supports *Dynamic* Public IP address allocation.</span></span> <span data-ttu-id="f21b6-169">您無法要求靜態公用 IP 位址指派。</span><span class="sxs-lookup"><span data-stu-id="f21b6-169">You cannot request a Static Public IP address assignment.</span></span> <span data-ttu-id="f21b6-170">不過，這不表示 hello IP 位址變更之後已被指派 tooyour VPN 閘道。</span><span class="sxs-lookup"><span data-stu-id="f21b6-170">However, this does not mean that hello IP address changes after it has been assigned tooyour VPN gateway.</span></span> <span data-ttu-id="f21b6-171">hello 公用 IP 位址變更為當 hello 閘道 hello 才會刪除並重新建立。</span><span class="sxs-lookup"><span data-stu-id="f21b6-171">hello only time hello Public IP address changes is when hello gateway is deleted and re-created.</span></span> <span data-ttu-id="f21b6-172">它不會因為重新調整、重設或 VPN 閘道的其他內部維護/升級而變更。</span><span class="sxs-lookup"><span data-stu-id="f21b6-172">It doesn't change across resizing, resetting, or other internal maintenance/upgrades of your VPN gateway.</span></span>

<span data-ttu-id="f21b6-173">要求將會指派 tooyour 虛擬網路 VPN 閘道的公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="f21b6-173">Request a Public IP address that will be assigned tooyour virtual network VPN gateway.</span></span>

```powershell
$gwpip= New-AzureRmPublicIpAddress -Name gwpip -ResourceGroupName TestRG1 -Location 'East US' -AllocationMethod Dynamic
```

## <span data-ttu-id="f21b6-174"><a name="GatewayIPConfig"></a>5.建立 hello 閘道 IP 位址組態</span><span class="sxs-lookup"><span data-stu-id="f21b6-174"><a name="GatewayIPConfig"></a>5. Create hello gateway IP addressing configuration</span></span>

<span data-ttu-id="f21b6-175">hello 閘道組態會定義 hello 子網路和公用 IP 位址 toouse hello。</span><span class="sxs-lookup"><span data-stu-id="f21b6-175">hello gateway configuration defines hello subnet and hello public IP address toouse.</span></span> <span data-ttu-id="f21b6-176">使用下列範例 toocreate hello 閘道組態：</span><span class="sxs-lookup"><span data-stu-id="f21b6-176">Use hello following example toocreate your gateway configuration:</span></span>

```powershell
$vnet = Get-AzureRmVirtualNetwork -Name TestVNet1 -ResourceGroupName TestRG1
$subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -VirtualNetwork $vnet
$gwipconfig = New-AzureRmVirtualNetworkGatewayIpConfig -Name gwipconfig1 -SubnetId $subnet.Id -PublicIpAddressId $gwpip.Id
```

## <span data-ttu-id="f21b6-177"><a name="CreateGateway"></a>6.建立 hello VPN 閘道</span><span class="sxs-lookup"><span data-stu-id="f21b6-177"><a name="CreateGateway"></a>6. Create hello VPN gateway</span></span>

<span data-ttu-id="f21b6-178">建立 hello 虛擬網路 VPN 閘道。</span><span class="sxs-lookup"><span data-stu-id="f21b6-178">Create hello virtual network VPN gateway.</span></span> <span data-ttu-id="f21b6-179">建立 VPN 閘道可能佔用 too45 分鐘或更多 toocomplete。</span><span class="sxs-lookup"><span data-stu-id="f21b6-179">Creating a VPN gateway can take up too45 minutes or more toocomplete.</span></span>

<span data-ttu-id="f21b6-180">使用下列值的 hello:</span><span class="sxs-lookup"><span data-stu-id="f21b6-180">Use hello following values:</span></span>

* <span data-ttu-id="f21b6-181">hello *-gatewaytype 的授權*網站-站台組態是*Vpn*。</span><span class="sxs-lookup"><span data-stu-id="f21b6-181">hello *-GatewayType* for a Site-to-Site configuration is *Vpn*.</span></span> <span data-ttu-id="f21b6-182">hello 閘道類型一律為您實作的特定 toohello 組態。</span><span class="sxs-lookup"><span data-stu-id="f21b6-182">hello gateway type is always specific toohello configuration that you are implementing.</span></span> <span data-ttu-id="f21b6-183">例如，其他閘道器組態可能需要 -GatewayType ExpressRoute。</span><span class="sxs-lookup"><span data-stu-id="f21b6-183">For example, other gateway configurations may require -GatewayType ExpressRoute.</span></span>
* <span data-ttu-id="f21b6-184">hello *-VpnType*可以*RouteBased* （又稱為 tooas 某些文件中的動態閘道），或*PolicyBased* （又稱為 tooas 某些文件中的靜態閘道).</span><span class="sxs-lookup"><span data-stu-id="f21b6-184">hello *-VpnType* can be *RouteBased* (referred tooas a Dynamic Gateway in some documentation), or *PolicyBased* (referred tooas a Static Gateway in some documentation).</span></span> <span data-ttu-id="f21b6-185">如需 VPN 閘道類型的詳細資訊，請參閱[關於 VPN 閘道](vpn-gateway-about-vpngateways.md)。</span><span class="sxs-lookup"><span data-stu-id="f21b6-185">For more information about VPN gateway types, see [About VPN Gateway](vpn-gateway-about-vpngateways.md).</span></span>
* <span data-ttu-id="f21b6-186">選取您想 toouse 的閘道 SKU hello。</span><span class="sxs-lookup"><span data-stu-id="f21b6-186">Select hello Gateway SKU that you want toouse.</span></span> <span data-ttu-id="f21b6-187">某些 SKU 有組態限制。</span><span class="sxs-lookup"><span data-stu-id="f21b6-187">There are configuration limitations for certain SKUs.</span></span> <span data-ttu-id="f21b6-188">如需詳細資訊，請參閱[閘道 SKU](vpn-gateway-about-vpn-gateway-settings.md#gwsku)。</span><span class="sxs-lookup"><span data-stu-id="f21b6-188">For more information, see [Gateway SKUs](vpn-gateway-about-vpn-gateway-settings.md#gwsku).</span></span> <span data-ttu-id="f21b6-189">如果您建立有關 hello hello VPN 閘道時收到錯誤-GatewaySku，請確認您已安裝 hello hello PowerShell 指令程式的最新版本。</span><span class="sxs-lookup"><span data-stu-id="f21b6-189">If you get an error when creating hello VPN gateway regarding hello -GatewaySku, verify that you have installed hello latest version of hello PowerShell cmdlets.</span></span>

```powershell
New-AzureRmVirtualNetworkGateway -Name VNet1GW -ResourceGroupName TestRG1 `
-Location 'East US' -IpConfigurations $gwipconfig -GatewayType Vpn `
-VpnType RouteBased -GatewaySku VpnGw1
```

## <span data-ttu-id="f21b6-190"><a name="ConfigureVPNDevice"></a>7.設定 VPN 裝置</span><span class="sxs-lookup"><span data-stu-id="f21b6-190"><a name="ConfigureVPNDevice"></a>7. Configure your VPN device</span></span>

<span data-ttu-id="f21b6-191">站台對站連線 tooan 在內部部署網路需要 VPN 裝置。</span><span class="sxs-lookup"><span data-stu-id="f21b6-191">Site-to-Site connections tooan on-premises network require a VPN device.</span></span> <span data-ttu-id="f21b6-192">在此步驟中，設定 VPN 裝置。</span><span class="sxs-lookup"><span data-stu-id="f21b6-192">In this step, you configure your VPN device.</span></span> <span data-ttu-id="f21b6-193">當設定 VPN 裝置，您會需要 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="f21b6-193">When configuring your VPN device, you need hello following:</span></span>

- <span data-ttu-id="f21b6-194">共用金鑰。</span><span class="sxs-lookup"><span data-stu-id="f21b6-194">A shared key.</span></span> <span data-ttu-id="f21b6-195">這是共用相同 hello 建立您的站對站 VPN 連線時所指定的索引鍵。</span><span class="sxs-lookup"><span data-stu-id="f21b6-195">This is hello same shared key that you specify when creating your Site-to-Site VPN connection.</span></span> <span data-ttu-id="f21b6-196">在我們的範例中，我們會使用基本的共用金鑰。</span><span class="sxs-lookup"><span data-stu-id="f21b6-196">In our examples, we use a basic shared key.</span></span> <span data-ttu-id="f21b6-197">我們建議您產生更複雜金鑰 toouse。</span><span class="sxs-lookup"><span data-stu-id="f21b6-197">We recommend that you generate a more complex key toouse.</span></span>
- <span data-ttu-id="f21b6-198">hello 的虛擬網路閘道的公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="f21b6-198">hello Public IP address of your virtual network gateway.</span></span> <span data-ttu-id="f21b6-199">您可以使用 hello Azure 入口網站、 PowerShell 或 CLI 檢視 hello 公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="f21b6-199">You can view hello public IP address by using hello Azure portal, PowerShell, or CLI.</span></span> <span data-ttu-id="f21b6-200">toofind hello 公用 IP 位址的虛擬網路閘道使用 PowerShell，下列範例使用 hello:</span><span class="sxs-lookup"><span data-stu-id="f21b6-200">toofind hello Public IP address of your virtual network gateway using PowerShell, use hello following example:</span></span>

  ```powershell
  Get-AzureRmPublicIpAddress -Name GW1PublicIP -ResourceGroupName TestRG1
  ```

[!INCLUDE [Configure VPN device](../../includes/vpn-gateway-configure-vpn-device-rm-include.md)]


## <span data-ttu-id="f21b6-201"><a name="CreateConnection"></a>8.建立 hello VPN 連線</span><span class="sxs-lookup"><span data-stu-id="f21b6-201"><a name="CreateConnection"></a>8. Create hello VPN connection</span></span>

<span data-ttu-id="f21b6-202">接下來，建立您的虛擬網路閘道與 VPN 裝置之間的 hello 站對站 VPN 連線。</span><span class="sxs-lookup"><span data-stu-id="f21b6-202">Next, create hello Site-to-Site VPN connection between your virtual network gateway and your VPN device.</span></span> <span data-ttu-id="f21b6-203">是以您自己的確定 tooreplace hello 值。</span><span class="sxs-lookup"><span data-stu-id="f21b6-203">Be sure tooreplace hello values with your own.</span></span> <span data-ttu-id="f21b6-204">hello 共用的金鑰必須符合您要用於 VPN 裝置組態的 hello 值。</span><span class="sxs-lookup"><span data-stu-id="f21b6-204">hello shared key must match hello value you used for your VPN device configuration.</span></span> <span data-ttu-id="f21b6-205">請注意該 hello '-ConnectionType' 站台對站台是*IPsec*。</span><span class="sxs-lookup"><span data-stu-id="f21b6-205">Notice that hello '-ConnectionType' for Site-to-Site is *IPsec*.</span></span>

1. <span data-ttu-id="f21b6-206">設定 hello 變數。</span><span class="sxs-lookup"><span data-stu-id="f21b6-206">Set hello variables.</span></span>
  ```powershell
  $gateway1 = Get-AzureRmVirtualNetworkGateway -Name VNet1GW -ResourceGroupName TestRG1
  $local = Get-AzureRmLocalNetworkGateway -Name Site2 -ResourceGroupName TestRG1
  ```

2. <span data-ttu-id="f21b6-207">建立 hello 連線。</span><span class="sxs-lookup"><span data-stu-id="f21b6-207">Create hello connection.</span></span>
  ```powershell
  New-AzureRmVirtualNetworkGatewayConnection -Name VNet1toSite2 -ResourceGroupName TestRG1 `
  -Location 'East US' -VirtualNetworkGateway1 $gateway1 -LocalNetworkGateway2 $local `
  -ConnectionType IPsec -RoutingWeight 10 -SharedKey 'abc123'
  ```

<span data-ttu-id="f21b6-208">過一會兒，hello 會建立連線。</span><span class="sxs-lookup"><span data-stu-id="f21b6-208">After a short while, hello connection will be established.</span></span>

## <span data-ttu-id="f21b6-209"><a name="toverify"></a>9.確認 hello VPN 連線</span><span class="sxs-lookup"><span data-stu-id="f21b6-209"><a name="toverify"></a>9. Verify hello VPN connection</span></span>

<span data-ttu-id="f21b6-210">有幾個不同的方式 tooverify VPN 連線。</span><span class="sxs-lookup"><span data-stu-id="f21b6-210">There are a few different ways tooverify your VPN connection.</span></span>

[!INCLUDE [Verify connection](../../includes/vpn-gateway-verify-connection-ps-rm-include.md)]

## <span data-ttu-id="f21b6-211"><a name="connectVM"></a>tooconnect tooa 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="f21b6-211"><a name="connectVM"></a>tooconnect tooa virtual machine</span></span>

[!INCLUDE [Connect tooa VM](../../includes/vpn-gateway-connect-vm-s2s-include.md)]


## <span data-ttu-id="f21b6-212"><a name="modify"></a>修改區域網路閘道的 IP 位址首碼</span><span class="sxs-lookup"><span data-stu-id="f21b6-212"><a name="modify"></a>Modify IP address prefixes for a local network gateway</span></span>

<span data-ttu-id="f21b6-213">如果您想要路由傳送 tooyour 在內部部署位置的 hello IP 位址首碼的變更，您可以修改 hello 區域網路閘道。</span><span class="sxs-lookup"><span data-stu-id="f21b6-213">If hello IP address prefixes that you want routed tooyour on-premises location change, you can modify hello local network gateway.</span></span> <span data-ttu-id="f21b6-214">所提供的指示有兩組。</span><span class="sxs-lookup"><span data-stu-id="f21b6-214">Two sets of instructions are provided.</span></span> <span data-ttu-id="f21b6-215">您選擇的 hello 指示取決於是否已建立您的閘道連線。</span><span class="sxs-lookup"><span data-stu-id="f21b6-215">hello instructions you choose depend on whether you have already created your gateway connection.</span></span>

[!INCLUDE [Modify prefixes](../../includes/vpn-gateway-modify-ip-prefix-rm-include.md)]

## <span data-ttu-id="f21b6-216"><a name="modifygwipaddress"></a>修改 hello 區域網路閘道的閘道 IP 位址</span><span class="sxs-lookup"><span data-stu-id="f21b6-216"><a name="modifygwipaddress"></a>Modify hello gateway IP address for a local network gateway</span></span>

[!INCLUDE [Modify gateway IP address](../../includes/vpn-gateway-modify-lng-gateway-ip-rm-include.md)]

## <a name="next-steps"></a><span data-ttu-id="f21b6-217">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f21b6-217">Next steps</span></span>

*  <span data-ttu-id="f21b6-218">一旦完成您的連線，您可以將虛擬機器 tooyour 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="f21b6-218">Once your connection is complete, you can add virtual machines tooyour virtual networks.</span></span> <span data-ttu-id="f21b6-219">如需詳細資訊，請參閱[虛擬機器](https://docs.microsoft.com/azure/#pivot=services&panel=Compute)。</span><span class="sxs-lookup"><span data-stu-id="f21b6-219">For more information, see [Virtual Machines](https://docs.microsoft.com/azure/#pivot=services&panel=Compute).</span></span>
* <span data-ttu-id="f21b6-220">BGP 的相關資訊，請參閱 hello [BGP 概觀](vpn-gateway-bgp-overview.md)和[如何 tooconfigure BGP](vpn-gateway-bgp-resource-manager-ps.md)。</span><span class="sxs-lookup"><span data-stu-id="f21b6-220">For information about BGP, see hello [BGP Overview](vpn-gateway-bgp-overview.md) and [How tooconfigure BGP](vpn-gateway-bgp-resource-manager-ps.md).</span></span>
