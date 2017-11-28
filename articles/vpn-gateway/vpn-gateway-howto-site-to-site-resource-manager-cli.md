---
title: "連接您在內部部署網路 tooan Azure 虛擬網路： 站對站 VPN: CLI |Microsoft 文件"
description: "IPsec 連線從您內部網路 tooan Azure 虛擬網路上的步驟 toocreate hello 公用網際網路。 這些步驟可協助您使用 CLI 建立跨單位的站對站 VPN 閘道連線。"
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/09/2017
ms.author: cherylmc
ms.openlocfilehash: c652cf2caf3928cdeb19d7dc329f6db101e5ed90
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-with-a-site-to-site-vpn-connection-using-cli"></a><span data-ttu-id="51666-104">使用 CLI 建立具有站對站 VPN 連線的虛擬網路</span><span class="sxs-lookup"><span data-stu-id="51666-104">Create a virtual network with a Site-to-Site VPN connection using CLI</span></span>

<span data-ttu-id="51666-105">本文章將示範如何 toouse 會 hello Azure CLI toocreate 站對站 VPN 閘道連線從您的內部部署網路 toohello VNet。</span><span class="sxs-lookup"><span data-stu-id="51666-105">This article shows you how toouse hello Azure CLI toocreate a Site-to-Site VPN gateway connection from your on-premises network toohello VNet.</span></span> <span data-ttu-id="51666-106">本文章中的 hello 步驟適用於 toohello Resource Manager 部署模型。</span><span class="sxs-lookup"><span data-stu-id="51666-106">hello steps in this article apply toohello Resource Manager deployment model.</span></span> <span data-ttu-id="51666-107">您也可以建立此組態使用不同的部署工具或部署模型，從下列清單中的 hello 選取不同的選項：</span><span class="sxs-lookup"><span data-stu-id="51666-107">You can also create this configuration using a different deployment tool or deployment model by selecting a different option from hello following list:</span></span><br>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="51666-108">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="51666-108">Azure portal</span></span>](vpn-gateway-howto-site-to-site-resource-manager-portal.md)
> * [<span data-ttu-id="51666-109">PowerShell</span><span class="sxs-lookup"><span data-stu-id="51666-109">PowerShell</span></span>](vpn-gateway-create-site-to-site-rm-powershell.md)
> * [<span data-ttu-id="51666-110">CLI</span><span class="sxs-lookup"><span data-stu-id="51666-110">CLI</span></span>](vpn-gateway-howto-site-to-site-resource-manager-cli.md)
> * [<span data-ttu-id="51666-111">Azure 入口網站 (傳統)</span><span class="sxs-lookup"><span data-stu-id="51666-111">Azure portal (classic)</span></span>](vpn-gateway-howto-site-to-site-classic-portal.md)
> 
>


![站對站 VPN 閘道跨單位連線圖表](./media/vpn-gateway-howto-site-to-site-resource-manager-cli/site-to-site-diagram.png)

<span data-ttu-id="51666-113">站對站 VPN 閘道連線是使用的 tooconnect 您內部網路 tooan Azure 虛擬網路透過 VPN IPsec/IKE （IKEv1 或 IKEv2） 通道。</span><span class="sxs-lookup"><span data-stu-id="51666-113">A Site-to-Site VPN gateway connection is used tooconnect your on-premises network tooan Azure virtual network over an IPsec/IKE (IKEv1 or IKEv2) VPN tunnel.</span></span> <span data-ttu-id="51666-114">這種類型的連線需要 VPN 裝置位於內部部署具有對外開放的公用 IP 位址指派 tooit。</span><span class="sxs-lookup"><span data-stu-id="51666-114">This type of connection requires a VPN device located on-premises that has an externally facing public IP address assigned tooit.</span></span> <span data-ttu-id="51666-115">如需 VPN 閘道的詳細資訊，請參閱[關於 VPN 閘道](vpn-gateway-about-vpngateways.md)。</span><span class="sxs-lookup"><span data-stu-id="51666-115">For more information about VPN gateways, see [About VPN gateway](vpn-gateway-about-vpngateways.md).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="51666-116">開始之前</span><span class="sxs-lookup"><span data-stu-id="51666-116">Before you begin</span></span>

<span data-ttu-id="51666-117">請確認您已符合下列準則，開始設定之前的 hello:</span><span class="sxs-lookup"><span data-stu-id="51666-117">Verify that you have met hello following criteria before beginning configuration:</span></span>

* <span data-ttu-id="51666-118">請確定您擁有相容的 VPN 裝置和人能夠 tooconfigure 它。</span><span class="sxs-lookup"><span data-stu-id="51666-118">Make sure you have a compatible VPN device and someone who is able tooconfigure it.</span></span> <span data-ttu-id="51666-119">如需相容 VPN 裝置和裝置組態的詳細資訊，請參閱[關於 VPN 裝置](vpn-gateway-about-vpn-devices.md)。</span><span class="sxs-lookup"><span data-stu-id="51666-119">For more information about compatible VPN devices and device configuration, see [About VPN Devices](vpn-gateway-about-vpn-devices.md).</span></span>
* <span data-ttu-id="51666-120">確認您的 VPN 裝置有對外開放的公用 IPv4 位址。</span><span class="sxs-lookup"><span data-stu-id="51666-120">Verify that you have an externally facing public IPv4 address for your VPN device.</span></span> <span data-ttu-id="51666-121">此 IP 位址不能位於 NAT 後方。</span><span class="sxs-lookup"><span data-stu-id="51666-121">This IP address cannot be located behind a NAT.</span></span>
* <span data-ttu-id="51666-122">如果您不熟悉 hello IP 位址範圍位於內部網路組態，您需要 toocoordinate 的人可以為您提供這些詳細資料。</span><span class="sxs-lookup"><span data-stu-id="51666-122">If you are unfamiliar with hello IP address ranges located in your on-premises network configuration, you need toocoordinate with someone who can provide those details for you.</span></span> <span data-ttu-id="51666-123">當您建立此設定時，您必須指定 hello IP 位址範圍前置詞，則 Azure 會路由傳送 tooyour 在內部部署位置。</span><span class="sxs-lookup"><span data-stu-id="51666-123">When you create this configuration, you must specify hello IP address range prefixes that Azure will route tooyour on-premises location.</span></span> <span data-ttu-id="51666-124">無 hello 的內部部署網路的子網路可以透過圈具有您想要 tooconnect hello 虛擬網路子網路。</span><span class="sxs-lookup"><span data-stu-id="51666-124">None of hello subnets of your on-premises network can over lap with hello virtual network subnets that you want tooconnect to.</span></span>
* <span data-ttu-id="51666-125">請確認您已安裝最新版本 （2.0 或更新版本） 的 hello CLI 命令。</span><span class="sxs-lookup"><span data-stu-id="51666-125">Verify that you have installed latest version of hello CLI commands (2.0 or later).</span></span> <span data-ttu-id="51666-126">如需安裝 hello CLI 命令的資訊，請參閱[安裝 Azure CLI 2.0](/cli/azure/install-azure-cli)和[開始使用 Azure CLI 2.0](/cli/azure/get-started-with-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="51666-126">For information about installing hello CLI commands, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli) and [Get Started with Azure CLI 2.0](/cli/azure/get-started-with-azure-cli).</span></span>

### <span data-ttu-id="51666-127"><a name="example"></a>範例值</span><span class="sxs-lookup"><span data-stu-id="51666-127"><a name="example"></a>Example values</span></span>

<span data-ttu-id="51666-128">您可以使用下列值 toocreate 測試環境的 hello 或 toothese 值，請參閱 toobetter 了解這篇文章中的 hello 範例：</span><span class="sxs-lookup"><span data-stu-id="51666-128">You can use hello following values toocreate a test environment, or refer toothese values toobetter understand hello examples in this article:</span></span>

```
#Example values

VnetName                = TestVNet1 
ResourceGroup           = TestRG1 
Location                = eastus 
AddressSpace            = 10.11.0.0/16 
SubnetName              = Subnet1 
Subnet                  = 10.11.0.0/24 
GatewaySubnet           = 10.11.255.0/27 
LocalNetworkGatewayName = Site2 
LNG Public IP           = <VPN device IP address>
LocalAddrPrefix1        = 10.0.0.0/24
LocalAddrPrefix2        = 20.0.0.0/24   
GatewayName             = VNet1GW 
PublicIP                = VNet1GWIP 
VPNType                 = RouteBased 
GatewayType             = Vpn 
ConnectionName          = VNet1toSite2
```

## <span data-ttu-id="51666-129"><a name="Login"></a>1.連接 tooyour 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="51666-129"><a name="Login"></a>1. Connect tooyour subscription</span></span>

[!INCLUDE [CLI login](../../includes/vpn-gateway-cli-login-include.md)]

## <span data-ttu-id="51666-130"><a name="rg"></a>2.建立資源群組</span><span class="sxs-lookup"><span data-stu-id="51666-130"><a name="rg"></a>2. Create a resource group</span></span>

<span data-ttu-id="51666-131">hello 下列範例會建立名為 'TestRG1' hello 'eastus' 位置中的資源群組。</span><span class="sxs-lookup"><span data-stu-id="51666-131">hello following example creates a resource group named 'TestRG1' in hello 'eastus' location.</span></span> <span data-ttu-id="51666-132">如果您已經有資源群組，您想 toocreate VNet hello 區中，您可以改為使用一個。</span><span class="sxs-lookup"><span data-stu-id="51666-132">If you already have a resource group in hello region that you want toocreate your VNet, you can use that one instead.</span></span>

```azurecli
az group create --name TestRG1 --location eastus
```

## <span data-ttu-id="51666-133"><a name="VNet"></a>3.建立虛擬網路</span><span class="sxs-lookup"><span data-stu-id="51666-133"><a name="VNet"></a>3. Create a virtual network</span></span>

<span data-ttu-id="51666-134">如果您還沒有虛擬網路，建立一個使用 hello [az 網路 vnet 建立](/cli/azure/network/vnet#create)命令。</span><span class="sxs-lookup"><span data-stu-id="51666-134">If you don't already have a virtual network, create one using hello [az network vnet create](/cli/azure/network/vnet#create) command.</span></span> <span data-ttu-id="51666-135">當建立虛擬網路，請確定 hello 您指定的位址空間不將任何您已在內部部署網路的 hello 位址空間重疊。</span><span class="sxs-lookup"><span data-stu-id="51666-135">When creating a virtual network, make sure that hello address spaces you specify don't overlap any of hello address spaces that you have on your on-premises network.</span></span>

<span data-ttu-id="51666-136">hello 下列範例會建立名為 'TestVNet1' 和 'Subnet1' 子網路，虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="51666-136">hello following example creates a virtual network named 'TestVNet1' and a subnet, 'Subnet1'.</span></span>

```azurecli
az network vnet create --name TestVNet1 --resource-group TestRG1 --address-prefix 10.11.0.0/16 --location eastus --subnet-name Subnet1 --subnet-prefix 10.11.0.0/24
```

## <span data-ttu-id="51666-137">4.<a name="gwsub"></a>建立 hello 閘道子網路</span><span class="sxs-lookup"><span data-stu-id="51666-137">4. <a name="gwsub"></a>Create hello gateway subnet</span></span>

[!INCLUDE [vpn-gateway-no-nsg](../../includes/vpn-gateway-no-nsg-include.md)]

<span data-ttu-id="51666-138">對於此組態，您也需要有閘道子網路。</span><span class="sxs-lookup"><span data-stu-id="51666-138">For this configuration, you also need a gateway subnet.</span></span> <span data-ttu-id="51666-139">hello 虛擬網路閘道會使用包含 hello hello VPN 閘道服務所使用的 IP 位址的閘道子網路。</span><span class="sxs-lookup"><span data-stu-id="51666-139">hello virtual network gateway uses a gateway subnet that contains hello IP addresses that are used by hello VPN gateway services.</span></span> <span data-ttu-id="51666-140">當您建立閘道子網路時，請將它命名為「GatewaySubnet」。</span><span class="sxs-lookup"><span data-stu-id="51666-140">When you create a gateway subnet, it must be named 'GatewaySubnet'.</span></span> <span data-ttu-id="51666-141">如果您將其命名為其他名字，您會建立子網路，但 Azure 不會將它視為閘道器子網路。</span><span class="sxs-lookup"><span data-stu-id="51666-141">If you name it something else, you create a subnet, but Azure won't treat it as a gateway subnet.</span></span>

<span data-ttu-id="51666-142">您指定的 hello 閘道子網路的 hello 大小取決於 hello VPN 閘道設定您想 toocreate。</span><span class="sxs-lookup"><span data-stu-id="51666-142">hello size of hello gateway subnet that you specify depends on hello VPN gateway configuration that you want toocreate.</span></span> <span data-ttu-id="51666-143">雖然可能 toocreate 閘道子網路為/29，我們建議您建立較大的子網路，其中包含多個位址，藉由選取 /27 或/28。</span><span class="sxs-lookup"><span data-stu-id="51666-143">While it is possible toocreate a gateway subnet as small as /29, we recommend that you create a larger subnet that includes more addresses by selecting /27 or /28.</span></span> <span data-ttu-id="51666-144">使用較大的閘道子網路允許足夠的 IP 位址 tooaccommodate 可能未來設定。</span><span class="sxs-lookup"><span data-stu-id="51666-144">Using a larger gateway subnet allows for enough IP addresses tooaccommodate possible future configurations.</span></span>

<span data-ttu-id="51666-145">使用 hello [az vnet 子網路建立](/cli/azure/network/vnet/subnet#create)命令 toocreate hello 閘道子網路。</span><span class="sxs-lookup"><span data-stu-id="51666-145">Use hello [az network vnet subnet create](/cli/azure/network/vnet/subnet#create) command toocreate hello gateway subnet.</span></span>

```azurecli
az network vnet subnet create --address-prefix 10.11.255.0/27 --name GatewaySubnet --resource-group TestRG1 --vnet-name TestVNet1
```

## <span data-ttu-id="51666-146"><a name="localnet"></a>5.建立 hello 區域網路閘道</span><span class="sxs-lookup"><span data-stu-id="51666-146"><a name="localnet"></a>5. Create hello local network gateway</span></span>

<span data-ttu-id="51666-147">hello 區域網路閘道通常是指 tooyour 在內部部署位置。</span><span class="sxs-lookup"><span data-stu-id="51666-147">hello local network gateway typically refers tooyour on-premises location.</span></span> <span data-ttu-id="51666-148">您提供 hello 站台的名稱之 Azure 可以參考 tooit，然後指定 hello IP 位址的 hello 在內部部署 VPN 裝置 toowhich 中，您將建立連接。</span><span class="sxs-lookup"><span data-stu-id="51666-148">You give hello site a name by which Azure can refer tooit, then specify hello IP address of hello on-premises VPN device toowhich you will create a connection.</span></span> <span data-ttu-id="51666-149">您也指定 hello 而必須路由傳送透過 hello VPN 閘道 toohello VPN 裝置 IP 位址首碼。</span><span class="sxs-lookup"><span data-stu-id="51666-149">You also specify hello IP address prefixes that will be routed through hello VPN gateway toohello VPN device.</span></span> <span data-ttu-id="51666-150">您指定的 hello 位址前置詞是在內部部署網路上的 hello 前置詞。</span><span class="sxs-lookup"><span data-stu-id="51666-150">hello address prefixes you specify are hello prefixes located on your on-premises network.</span></span> <span data-ttu-id="51666-151">如果您在內部部署網路變更時，您可以輕鬆地更新 hello 前置詞。</span><span class="sxs-lookup"><span data-stu-id="51666-151">If your on-premises network changes, you can easily update hello prefixes.</span></span>

<span data-ttu-id="51666-152">使用下列值的 hello:</span><span class="sxs-lookup"><span data-stu-id="51666-152">Use hello following values:</span></span>

* <span data-ttu-id="51666-153">hello *-閘道 ip 位址*是 hello 在內部部署 VPN 裝置 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="51666-153">hello *--gateway-ip-address* is hello IP address of your on-premises VPN device.</span></span> <span data-ttu-id="51666-154">VPN 裝置不能位於 NAT 後方。</span><span class="sxs-lookup"><span data-stu-id="51666-154">Your VPN device cannot be located behind a NAT.</span></span>
* <span data-ttu-id="51666-155">hello *-本機位址首碼*是內部位址空間。</span><span class="sxs-lookup"><span data-stu-id="51666-155">hello *--local-address-prefixes* are your on-premises address spaces.</span></span>

<span data-ttu-id="51666-156">使用 hello [az 網路本機閘道建立](/cli/azure/network/local-gateway#create)命令 tooadd 區域網路閘道與多個位址前置詞：</span><span class="sxs-lookup"><span data-stu-id="51666-156">Use hello [az network local-gateway create](/cli/azure/network/local-gateway#create) command tooadd a local network gateway with multiple address prefixes:</span></span>

```azurecli
az network local-gateway create --gateway-ip-address 23.99.221.164 --name Site2 --resource-group TestRG1 --local-address-prefixes 10.0.0.0/24 20.0.0.0/24
```

## <span data-ttu-id="51666-157"><a name="PublicIP"></a>6.要求公用 IP 位址</span><span class="sxs-lookup"><span data-stu-id="51666-157"><a name="PublicIP"></a>6. Request a Public IP address</span></span>

<span data-ttu-id="51666-158">VPN 閘道必須具有公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="51666-158">A VPN gateway must have a Public IP address.</span></span> <span data-ttu-id="51666-159">您第一次要求 hello IP 位址資源，並建立您的虛擬網路閘道時參考 tooit。</span><span class="sxs-lookup"><span data-stu-id="51666-159">You first request hello IP address resource, and then refer tooit when creating your virtual network gateway.</span></span> <span data-ttu-id="51666-160">hello IP 位址建立 hello VPN 閘道時，會動態指定 toohello 資源。</span><span class="sxs-lookup"><span data-stu-id="51666-160">hello IP address is dynamically assigned toohello resource when hello VPN gateway is created.</span></span> <span data-ttu-id="51666-161">VPN 閘道目前僅支援*動態*公用 IP 位址配置。</span><span class="sxs-lookup"><span data-stu-id="51666-161">VPN Gateway currently only supports *Dynamic* Public IP address allocation.</span></span> <span data-ttu-id="51666-162">您無法要求靜態公用 IP 位址指派。</span><span class="sxs-lookup"><span data-stu-id="51666-162">You cannot request a Static Public IP address assignment.</span></span> <span data-ttu-id="51666-163">不過，這不表示 hello IP 位址變更之後已被指派 tooyour VPN 閘道。</span><span class="sxs-lookup"><span data-stu-id="51666-163">However, this does not mean that hello IP address changes after it has been assigned tooyour VPN gateway.</span></span> <span data-ttu-id="51666-164">hello 公用 IP 位址變更為當 hello 閘道 hello 才會刪除並重新建立。</span><span class="sxs-lookup"><span data-stu-id="51666-164">hello only time hello Public IP address changes is when hello gateway is deleted and re-created.</span></span> <span data-ttu-id="51666-165">它不會因為重新調整、重設或 VPN 閘道的其他內部維護/升級而變更。</span><span class="sxs-lookup"><span data-stu-id="51666-165">It doesn't change across resizing, resetting, or other internal maintenance/upgrades of your VPN gateway.</span></span>

<span data-ttu-id="51666-166">使用 hello [az 網路公用 ip 建立](/cli/azure/network/public-ip#create)命令 toorequest 的動態公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="51666-166">Use hello [az network public-ip create](/cli/azure/network/public-ip#create) command toorequest a Dynamic Public IP address.</span></span>

```azurecli
az network public-ip create --name VNet1GWIP --resource-group TestRG1 --allocation-method Dynamic
```

## <span data-ttu-id="51666-167"><a name="CreateGateway"></a>7.建立 hello VPN 閘道</span><span class="sxs-lookup"><span data-stu-id="51666-167"><a name="CreateGateway"></a>7. Create hello VPN gateway</span></span>

<span data-ttu-id="51666-168">建立 hello 虛擬網路 VPN 閘道。</span><span class="sxs-lookup"><span data-stu-id="51666-168">Create hello virtual network VPN gateway.</span></span> <span data-ttu-id="51666-169">建立 VPN 閘道可能佔用 too45 分鐘或更多 toocomplete。</span><span class="sxs-lookup"><span data-stu-id="51666-169">Creating a VPN gateway can take up too45 minutes or more toocomplete.</span></span>

<span data-ttu-id="51666-170">使用下列值的 hello:</span><span class="sxs-lookup"><span data-stu-id="51666-170">Use hello following values:</span></span>

* <span data-ttu-id="51666-171">hello *-閘道類型*網站-站台組態是*Vpn*。</span><span class="sxs-lookup"><span data-stu-id="51666-171">hello *--gateway-type* for a Site-to-Site configuration is *Vpn*.</span></span> <span data-ttu-id="51666-172">hello 閘道類型一律為您實作的特定 toohello 組態。</span><span class="sxs-lookup"><span data-stu-id="51666-172">hello gateway type is always specific toohello configuration that you are implementing.</span></span> <span data-ttu-id="51666-173">如需詳細資訊，請參閱[閘道類型](vpn-gateway-about-vpn-gateway-settings.md#gwtype)。</span><span class="sxs-lookup"><span data-stu-id="51666-173">For more information, see [Gateway types](vpn-gateway-about-vpn-gateway-settings.md#gwtype).</span></span>
* <span data-ttu-id="51666-174">hello *-vpn 類型*可以*RouteBased* （又稱為 tooas 某些文件中的動態閘道），或*PolicyBased* （又稱為 tooas 部分中是靜態閘道文件）。</span><span class="sxs-lookup"><span data-stu-id="51666-174">hello *--vpn-type* can be *RouteBased* (referred tooas a Dynamic Gateway in some documentation), or *PolicyBased* (referred tooas a Static Gateway in some documentation).</span></span> <span data-ttu-id="51666-175">您所連接的 hello 裝置的特定 toorequirements hello 設定。</span><span class="sxs-lookup"><span data-stu-id="51666-175">hello setting is specific toorequirements of hello device that you are connecting to.</span></span> <span data-ttu-id="51666-176">如需 VPN 閘道類型的詳細資訊，請參閱[關於 VPN 閘道組態設定](vpn-gateway-about-vpn-gateway-settings.md#vpntype)。</span><span class="sxs-lookup"><span data-stu-id="51666-176">For more information about VPN gateway types, see [About VPN Gateway configuration settings](vpn-gateway-about-vpn-gateway-settings.md#vpntype).</span></span>
* <span data-ttu-id="51666-177">選取您想 toouse 的閘道 SKU hello。</span><span class="sxs-lookup"><span data-stu-id="51666-177">Select hello Gateway SKU that you want toouse.</span></span> <span data-ttu-id="51666-178">某些 SKU 有組態限制。</span><span class="sxs-lookup"><span data-stu-id="51666-178">There are configuration limitations for certain SKUs.</span></span> <span data-ttu-id="51666-179">如需詳細資訊，請參閱[閘道 SKU](vpn-gateway-about-vpn-gateway-settings.md#gwsku)。</span><span class="sxs-lookup"><span data-stu-id="51666-179">For more information, see [Gateway SKUs](vpn-gateway-about-vpn-gateway-settings.md#gwsku).</span></span>

<span data-ttu-id="51666-180">建立 hello VPN 閘道使用 hello [az 網路 vnet 閘道建立](/cli/azure/network/vnet-gateway#create)命令。</span><span class="sxs-lookup"><span data-stu-id="51666-180">Create hello VPN gateway using hello [az network vnet-gateway create](/cli/azure/network/vnet-gateway#create) command.</span></span> <span data-ttu-id="51666-181">如果您執行此命令使用 hello '-沒有-wait' 參數，您沒有看到任何意見反應或輸出。</span><span class="sxs-lookup"><span data-stu-id="51666-181">If you run this command using hello '--no-wait' parameter, you don't see any feedback or output.</span></span> <span data-ttu-id="51666-182">此參數允許 hello 閘道 toocreate hello 背景。</span><span class="sxs-lookup"><span data-stu-id="51666-182">This parameter allows hello gateway toocreate in hello background.</span></span> <span data-ttu-id="51666-183">它會採用約 45 分鐘內 toocreate 閘道。</span><span class="sxs-lookup"><span data-stu-id="51666-183">It takes around 45 minutes toocreate a gateway.</span></span>

```azurecli
az network vnet-gateway create --name VNet1GW --public-ip-address VNet1GWIP --resource-group TestRG1 --vnet TestVNet1 --gateway-type Vpn --vpn-type RouteBased --sku VpnGw1 --no-wait 
```

## <span data-ttu-id="51666-184"><a name="VPNDevice"></a>8.設定 VPN 裝置</span><span class="sxs-lookup"><span data-stu-id="51666-184"><a name="VPNDevice"></a>8. Configure your VPN device</span></span>

<span data-ttu-id="51666-185">站台對站連線 tooan 在內部部署網路需要 VPN 裝置。</span><span class="sxs-lookup"><span data-stu-id="51666-185">Site-to-Site connections tooan on-premises network require a VPN device.</span></span> <span data-ttu-id="51666-186">在此步驟中，設定 VPN 裝置。</span><span class="sxs-lookup"><span data-stu-id="51666-186">In this step, you configure your VPN device.</span></span> <span data-ttu-id="51666-187">當設定 VPN 裝置，您會需要 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="51666-187">When configuring your VPN device, you need hello following:</span></span>

- <span data-ttu-id="51666-188">共用金鑰。</span><span class="sxs-lookup"><span data-stu-id="51666-188">A shared key.</span></span> <span data-ttu-id="51666-189">這是共用相同 hello 建立您的站對站 VPN 連線時所指定的索引鍵。</span><span class="sxs-lookup"><span data-stu-id="51666-189">This is hello same shared key that you specify when creating your Site-to-Site VPN connection.</span></span> <span data-ttu-id="51666-190">在我們的範例中，我們會使用基本的共用金鑰。</span><span class="sxs-lookup"><span data-stu-id="51666-190">In our examples, we use a basic shared key.</span></span> <span data-ttu-id="51666-191">我們建議您產生更複雜金鑰 toouse。</span><span class="sxs-lookup"><span data-stu-id="51666-191">We recommend that you generate a more complex key toouse.</span></span>
- <span data-ttu-id="51666-192">hello 的虛擬網路閘道的公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="51666-192">hello Public IP address of your virtual network gateway.</span></span> <span data-ttu-id="51666-193">您可以使用 hello Azure 入口網站、 PowerShell 或 CLI 檢視 hello 公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="51666-193">You can view hello public IP address by using hello Azure portal, PowerShell, or CLI.</span></span> <span data-ttu-id="51666-194">toofind hello 公用 IP 位址的虛擬網路閘道，使用 hello [az 網路公用 ip 清單](/cli/azure/network/public-ip#list)命令。</span><span class="sxs-lookup"><span data-stu-id="51666-194">toofind hello public IP address of your virtual network gateway, use hello [az network public-ip list](/cli/azure/network/public-ip#list) command.</span></span> <span data-ttu-id="51666-195">以方便閱讀，hello 輸出會是格式化的 toodisplay hello 清單的資料表中的公用 Ip。</span><span class="sxs-lookup"><span data-stu-id="51666-195">For easy reading, hello output is formatted toodisplay hello list of public IPs in table format.</span></span>

  ```azurecli
  az network public-ip list --resource-group TestRG1 --output table
  ```


[!INCLUDE [Configure VPN device](../../includes/vpn-gateway-configure-vpn-device-rm-include.md)]


## <span data-ttu-id="51666-196"><a name="CreateConnection"></a>9.建立 hello VPN 連線</span><span class="sxs-lookup"><span data-stu-id="51666-196"><a name="CreateConnection"></a>9. Create hello VPN connection</span></span>

<span data-ttu-id="51666-197">建立虛擬網路閘道與內部部署 VPN 裝置之間的 hello 站對站 VPN 連線。</span><span class="sxs-lookup"><span data-stu-id="51666-197">Create hello Site-to-Site VPN connection between your virtual network gateway and your on-premises VPN device.</span></span> <span data-ttu-id="51666-198">請特別注意 toohello 共用金鑰值，它必須符合設定的 hello 共用您的 VPN 裝置的金鑰值。</span><span class="sxs-lookup"><span data-stu-id="51666-198">Pay particular attention toohello shared key value, which must match hello configured shared key value for your VPN device.</span></span>

<span data-ttu-id="51666-199">建立 hello 連線使用 hello [az 網路 vpn 連線建立](/cli/azure/network/vpn-connection#create)命令。</span><span class="sxs-lookup"><span data-stu-id="51666-199">Create hello connection using hello [az network vpn-connection create](/cli/azure/network/vpn-connection#create) command.</span></span>

```azurecli
az network vpn-connection create --name VNet1toSite2 -resource-group TestRG1 --vnet-gateway1 VNet1GW -l eastus --shared-key abc123 --local-gateway2 Site2
```

<span data-ttu-id="51666-200">過一會兒，hello 會建立連線。</span><span class="sxs-lookup"><span data-stu-id="51666-200">After a short while, hello connection will be established.</span></span>

## <span data-ttu-id="51666-201"><a name="toverify"></a>10.確認 hello VPN 連線</span><span class="sxs-lookup"><span data-stu-id="51666-201"><a name="toverify"></a>10. Verify hello VPN connection</span></span>

[!INCLUDE [verify connection](../../includes/vpn-gateway-verify-connection-cli-rm-include.md)]

<span data-ttu-id="51666-202">如果您想 toouse 另一個方法 tooverify 您的連線，請參閱[驗證的 VPN 閘道連線](vpn-gateway-verify-connection-resource-manager.md)。</span><span class="sxs-lookup"><span data-stu-id="51666-202">If you want toouse another method tooverify your connection, see [Verify a VPN Gateway connection](vpn-gateway-verify-connection-resource-manager.md).</span></span>

## <span data-ttu-id="51666-203"><a name="connectVM"></a>tooconnect tooa 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="51666-203"><a name="connectVM"></a>tooconnect tooa virtual machine</span></span>

[!INCLUDE [Connect tooa VM](../../includes/vpn-gateway-connect-vm-s2s-include.md)]

## <span data-ttu-id="51666-204"><a name="tasks"></a>常見工作</span><span class="sxs-lookup"><span data-stu-id="51666-204"><a name="tasks"></a>Common tasks</span></span>

<span data-ttu-id="51666-205">本節包含使用站對站組態時很實用的常見命令。</span><span class="sxs-lookup"><span data-stu-id="51666-205">This section contains common commands that are helpful when working with site-to-site configurations.</span></span> <span data-ttu-id="51666-206">Hello 的 CLI 網路命令的完整清單，請參閱[Azure CLI-網路](/cli/azure/network)。</span><span class="sxs-lookup"><span data-stu-id="51666-206">For hello full list of CLI networking commands, see [Azure CLI - Networking](/cli/azure/network).</span></span>

[!INCLUDE [local network gateway common tasks](../../includes/vpn-gateway-common-tasks-cli-include.md)]

## <a name="next-steps"></a><span data-ttu-id="51666-207">後續步驟</span><span class="sxs-lookup"><span data-stu-id="51666-207">Next steps</span></span>

* <span data-ttu-id="51666-208">一旦完成您的連線，您可以將虛擬機器 tooyour 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="51666-208">Once your connection is complete, you can add virtual machines tooyour virtual networks.</span></span> <span data-ttu-id="51666-209">如需詳細資訊，請參閱[虛擬機器](https://docs.microsoft.com/azure/#pivot=services&panel=Compute)。</span><span class="sxs-lookup"><span data-stu-id="51666-209">For more information, see [Virtual Machines](https://docs.microsoft.com/azure/#pivot=services&panel=Compute).</span></span>
* <span data-ttu-id="51666-210">BGP 的相關資訊，請參閱 hello [BGP 概觀](vpn-gateway-bgp-overview.md)和[如何 tooconfigure BGP](vpn-gateway-bgp-resource-manager-ps.md)。</span><span class="sxs-lookup"><span data-stu-id="51666-210">For information about BGP, see hello [BGP Overview](vpn-gateway-bgp-overview.md) and [How tooconfigure BGP](vpn-gateway-bgp-resource-manager-ps.md).</span></span>
* <span data-ttu-id="51666-211">如需強制通道的相關資訊，請參閱[關於強制通道](vpn-gateway-forced-tunneling-rm.md)。</span><span class="sxs-lookup"><span data-stu-id="51666-211">For information about Forced Tunneling, see [About Forced Tunneling](vpn-gateway-forced-tunneling-rm.md).</span></span>
* <span data-ttu-id="51666-212">如需高可用性主動-主動連線的相關資訊，請參閱[高可用性跨單位和 VNet 對 VNet 連線能力](vpn-gateway-highlyavailable.md)。</span><span class="sxs-lookup"><span data-stu-id="51666-212">For information about Highly Available Active-Active connections, see [Highly Available cross-premises and VNet-to-VNet connectivity](vpn-gateway-highlyavailable.md).</span></span>
* <span data-ttu-id="51666-213">如需 Azure CLI 網路命令的清單，請參閱 [Azure CLI](https://docs.microsoft.com/cli/azure/network)。</span><span class="sxs-lookup"><span data-stu-id="51666-213">For a list of networking Azure CLI commands, see [Azure CLI](https://docs.microsoft.com/cli/azure/network).</span></span>