---
title: "設定 Azure 站對站連線的強制通道：傳統 | Microsoft Docs"
description: "如何 tooredirect 或 'force' 所有網際網路繫結流量後 tooyour 內部位置。"
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 5c0177f1-540c-4474-9b80-f541fa44240b
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/01/2017
ms.author: cherylmc
ms.openlocfilehash: 35b3a9ea370f9f962572629a69cc9aed16a87837
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-forced-tunneling-using-hello-classic-deployment-model"></a><span data-ttu-id="4e0a5-103">設定強制通道使用 hello 傳統部署模型</span><span class="sxs-lookup"><span data-stu-id="4e0a5-103">Configure forced tunneling using hello classic deployment model</span></span>

<span data-ttu-id="4e0a5-104">強制通道可讓您重新導向或 「 強制 」 所有網際網路繫結流量後 tooyour 在內部部署位置透過站對站 VPN 通道來檢查和稽核。</span><span class="sxs-lookup"><span data-stu-id="4e0a5-104">Forced tunneling lets you redirect or "force" all Internet-bound traffic back tooyour on-premises location via a Site-to-Site VPN tunnel for inspection and auditing.</span></span> <span data-ttu-id="4e0a5-105">這是多數企業 IT 原則的重要安全性需求。</span><span class="sxs-lookup"><span data-stu-id="4e0a5-105">This is a critical security requirement for most enterprise IT policies.</span></span> <span data-ttu-id="4e0a5-106">如果沒有強制通道，您在 Azure 中的 Vm 所傳來的網際網路繫結流量將一律周遊出 toohello 網際網路，而 hello 選項 tooallow 不直接的 Azure 網路基礎結構從您 tooinspect 或稽核 hello 流量。</span><span class="sxs-lookup"><span data-stu-id="4e0a5-106">Without forced tunneling, Internet-bound traffic from your VMs in Azure will always traverse from Azure network infrastructure directly out toohello Internet, without hello option tooallow you tooinspect or audit hello traffic.</span></span> <span data-ttu-id="4e0a5-107">Tooinformation 洩漏或其他類型的安全性漏洞，可能會導致未經授權的網際網路存取。</span><span class="sxs-lookup"><span data-stu-id="4e0a5-107">Unauthorized Internet access can potentially lead tooinformation disclosure or other types of security breaches.</span></span>

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

<span data-ttu-id="4e0a5-108">這篇文章會引導您設定強制通道使用 hello 傳統部署模型所建立的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="4e0a5-108">This article walks you through configuring forced tunneling for virtual networks created using hello classic deployment model.</span></span> <span data-ttu-id="4e0a5-109">使用 PowerShell，不能透過 hello 入口網站可以設定強制通道。</span><span class="sxs-lookup"><span data-stu-id="4e0a5-109">Forced tunneling can be configured by using PowerShell, not through hello portal.</span></span> <span data-ttu-id="4e0a5-110">如果您想 tooconfigure 強制通道的 hello Resource Manager 部署模型時，請從下列下拉式清單中的 hello 中選取傳統的發行項：</span><span class="sxs-lookup"><span data-stu-id="4e0a5-110">If you want tooconfigure forced tunneling for hello Resource Manager deployment model, select classic article from hello following dropdown list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="4e0a5-111">PowerShell - 傳統</span><span class="sxs-lookup"><span data-stu-id="4e0a5-111">PowerShell - Classic</span></span>](vpn-gateway-about-forced-tunneling.md)
> * [<span data-ttu-id="4e0a5-112">PowerShell - 資源管理員</span><span class="sxs-lookup"><span data-stu-id="4e0a5-112">PowerShell - Resource Manager</span></span>](vpn-gateway-forced-tunneling-rm.md)
> 
> 

## <a name="requirements-and-considerations"></a><span data-ttu-id="4e0a5-113">需求和考量</span><span class="sxs-lookup"><span data-stu-id="4e0a5-113">Requirements and considerations</span></span>
<span data-ttu-id="4e0a5-114">Azure 中的強制通道會透過虛擬網路使用者定義路由 (UDR) 進行設定。</span><span class="sxs-lookup"><span data-stu-id="4e0a5-114">Forced tunneling in Azure is configured via virtual network user-defined routes (UDR).</span></span> <span data-ttu-id="4e0a5-115">重新導向流量 tooan 內部部署站台以預設路由 toohello Azure VPN 閘道。</span><span class="sxs-lookup"><span data-stu-id="4e0a5-115">Redirecting traffic tooan on-premises site is expressed as a Default Route toohello Azure VPN gateway.</span></span> <span data-ttu-id="4e0a5-116">hello 下節列出 hello 目前限制的 hello 路由表和路由的 Azure 虛擬網路：</span><span class="sxs-lookup"><span data-stu-id="4e0a5-116">hello following section lists hello current limitation of hello routing table and routes for an Azure Virtual Network:</span></span>

* <span data-ttu-id="4e0a5-117">每個虛擬網路的子網路皆有內建的系統路由表。</span><span class="sxs-lookup"><span data-stu-id="4e0a5-117">Each virtual network subnet has a built-in, system routing table.</span></span> <span data-ttu-id="4e0a5-118">hello 系統路由表具有下列三個路由群組的 hello:</span><span class="sxs-lookup"><span data-stu-id="4e0a5-118">hello system routing table has hello following three groups of routes:</span></span>

  * <span data-ttu-id="4e0a5-119">**區域的 VNet 路由：**直接 toohello Vm 中的目的地 hello 相同虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="4e0a5-119">**Local VNet routes:** Directly toohello destination VMs in hello same virtual network.</span></span>
  * <span data-ttu-id="4e0a5-120">**在內部部署路由：** toohello Azure VPN 閘道。</span><span class="sxs-lookup"><span data-stu-id="4e0a5-120">**On-premises routes:** toohello Azure VPN gateway.</span></span>
  * <span data-ttu-id="4e0a5-121">**預設路由：**直接 toohello 網際網路。</span><span class="sxs-lookup"><span data-stu-id="4e0a5-121">**Default route:** Directly toohello Internet.</span></span> <span data-ttu-id="4e0a5-122">目的地的封包 toohello 私人 IP 位址未涵蓋的 hello 前兩個路由皆會予以捨棄。</span><span class="sxs-lookup"><span data-stu-id="4e0a5-122">Packets destined toohello private IP addresses not covered by hello previous two routes will be dropped.</span></span>
* <span data-ttu-id="4e0a5-123">Hello 版本中的使用者定義的路由，您可建立路由表 tooadd 預設路由，並再將關聯 hello 路由表 tooyour VNet 子網路，tooenable 強制通道這些子網路上。</span><span class="sxs-lookup"><span data-stu-id="4e0a5-123">With hello release of user-defined routes, you can create a routing table tooadd a default route, and then associate hello routing table tooyour VNet subnet(s) tooenable forced tunneling on those subnets.</span></span>
* <span data-ttu-id="4e0a5-124">您在 hello 跨單位本機站台連線的 toohello 虛擬網路之間需要 tooset 「 預設網站 」。</span><span class="sxs-lookup"><span data-stu-id="4e0a5-124">You need tooset a "default site" among hello cross-premises local sites connected toohello virtual network.</span></span>
* <span data-ttu-id="4e0a5-125">強制通道必須與具有動態路由 VPN 閘道 (非靜態閘道) 的 VNet 相關聯。</span><span class="sxs-lookup"><span data-stu-id="4e0a5-125">Forced tunneling must be associated with a VNet that has a dynamic routing VPN gateway (not a static gateway).</span></span>
* <span data-ttu-id="4e0a5-126">未設定這項機制，透過 ExpressRoute 強制通道，但相反地，會啟用透過 ExpressRoute BGP hello 將預設路由通告對等互連工作階段。</span><span class="sxs-lookup"><span data-stu-id="4e0a5-126">ExpressRoute forced tunneling is not configured via this mechanism, but instead, is enabled by advertising a default route via hello ExpressRoute BGP peering sessions.</span></span> <span data-ttu-id="4e0a5-127">請參閱 hello [ExpressRoute 文件](https://azure.microsoft.com/documentation/services/expressroute/)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="4e0a5-127">Please see hello [ExpressRoute Documentation](https://azure.microsoft.com/documentation/services/expressroute/) for more information.</span></span>

## <a name="configuration-overview"></a><span data-ttu-id="4e0a5-128">組態概觀</span><span class="sxs-lookup"><span data-stu-id="4e0a5-128">Configuration overview</span></span>
<span data-ttu-id="4e0a5-129">下列範例的 hello，hello 前端子網路則不會強制通道。</span><span class="sxs-lookup"><span data-stu-id="4e0a5-129">In hello following example, hello Frontend subnet is not forced tunneled.</span></span> <span data-ttu-id="4e0a5-130">hello hello Frontend 子網路中的工作負載可以繼續 tooaccept，並直接從網際網路 hello 回應 toocustomer 要求。</span><span class="sxs-lookup"><span data-stu-id="4e0a5-130">hello workloads in hello Frontend subnet can continue tooaccept and respond toocustomer requests from hello Internet directly.</span></span> <span data-ttu-id="4e0a5-131">hello mid-tier 和 Backend 子網路會強制通道。</span><span class="sxs-lookup"><span data-stu-id="4e0a5-131">hello Mid-tier and Backend subnets are forced tunneled.</span></span> <span data-ttu-id="4e0a5-132">這些兩個子網路 toohello 網際網路任何傳出連線會透過其中一個 S2S VPN 通道連接的 hello 強制或重新導向回 tooan 在內部部署站台。</span><span class="sxs-lookup"><span data-stu-id="4e0a5-132">Any outbound connections from these two subnets toohello Internet will be forced or redirected back tooan on-premises site via one of hello S2S VPN tunnels.</span></span>

<span data-ttu-id="4e0a5-133">這可讓您 toorestrict 和檢查您的虛擬機器從網際網路存取，或雲端服務在 Azure 中，同時繼續 tooenable 您所需的多層式服務架構。</span><span class="sxs-lookup"><span data-stu-id="4e0a5-133">This allows you toorestrict and inspect Internet access from your virtual machines or cloud services in Azure, while continuing tooenable your multi-tier service architecture required.</span></span> <span data-ttu-id="4e0a5-134">您也可以套用強制通道 toohello 整個虛擬網路是否有任何網際網路對向工作負載虛擬網路中。</span><span class="sxs-lookup"><span data-stu-id="4e0a5-134">You also can apply forced tunneling toohello entire virtual networks if there are no Internet-facing workloads in your virtual networks.</span></span>

![強制通道](./media/vpn-gateway-about-forced-tunneling/forced-tunnel.png)

## <a name="before-you-begin"></a><span data-ttu-id="4e0a5-136">開始之前</span><span class="sxs-lookup"><span data-stu-id="4e0a5-136">Before you begin</span></span>
<span data-ttu-id="4e0a5-137">請確認您有下列項目開始設定之前的 hello。</span><span class="sxs-lookup"><span data-stu-id="4e0a5-137">Verify that you have hello following items before beginning configuration.</span></span>

* <span data-ttu-id="4e0a5-138">Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="4e0a5-138">An Azure subscription.</span></span> <span data-ttu-id="4e0a5-139">如果您還沒有 Azure 訂用帳戶，則可以啟用 [MSDN 訂戶權益](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/)或註冊[免費帳戶](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="4e0a5-139">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free account](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="4e0a5-140">已設定的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="4e0a5-140">A configured virtual network.</span></span> 
* <span data-ttu-id="4e0a5-141">hello 的 hello Azure PowerShell cmdlet 的最新版本。</span><span class="sxs-lookup"><span data-stu-id="4e0a5-141">hello latest version of hello Azure PowerShell cmdlets.</span></span> <span data-ttu-id="4e0a5-142">請參閱[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)如需安裝 hello PowerShell cmdlet 的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="4e0a5-142">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for more information about installing hello PowerShell cmdlets.</span></span>

## <a name="configure-forced-tunneling"></a><span data-ttu-id="4e0a5-143">設定強制通道</span><span class="sxs-lookup"><span data-stu-id="4e0a5-143">Configure forced tunneling</span></span>
<span data-ttu-id="4e0a5-144">hello 遵循程序將協助您指定虛擬網路的強制通道。</span><span class="sxs-lookup"><span data-stu-id="4e0a5-144">hello following procedure will help you specify forced tunneling for a virtual network.</span></span> <span data-ttu-id="4e0a5-145">hello 設定步驟對應 toohello VNet 網路組態檔。</span><span class="sxs-lookup"><span data-stu-id="4e0a5-145">hello configuration steps correspond toohello VNet network configuration file.</span></span>

```
<VirtualNetworkSite name="MultiTier-VNet" Location="North Europe">
     <AddressSpace>
      <AddressPrefix>10.1.0.0/16</AddressPrefix>
        </AddressSpace>
        <Subnets>
          <Subnet name="Frontend">
            <AddressPrefix>10.1.0.0/24</AddressPrefix>
          </Subnet>
          <Subnet name="Midtier">
            <AddressPrefix>10.1.1.0/24</AddressPrefix>
          </Subnet>
          <Subnet name="Backend">
            <AddressPrefix>10.1.2.0/23</AddressPrefix>
          </Subnet>
          <Subnet name="GatewaySubnet">
            <AddressPrefix>10.1.200.0/28</AddressPrefix>
          </Subnet>
        </Subnets>
        <Gateway>
          <ConnectionsToLocalNetwork>
            <LocalNetworkSiteRef name="DefaultSiteHQ">
              <Connection type="IPsec" />
            </LocalNetworkSiteRef>
            <LocalNetworkSiteRef name="Branch1">
              <Connection type="IPsec" />
            </LocalNetworkSiteRef>
            <LocalNetworkSiteRef name="Branch2">
              <Connection type="IPsec" />
            </LocalNetworkSiteRef>
            <LocalNetworkSiteRef name="Branch3">
              <Connection type="IPsec" />
            </LocalNetworkSiteRef>
        </Gateway>
      </VirtualNetworkSite>
    </VirtualNetworkSite>
```

<span data-ttu-id="4e0a5-146">在此範例中，虛擬網路 'Multitier-vnet' hello 有三個子網路: '前端'、 'Midtier，' 和 'Backend' 的子網路，具有四個跨單位連線: 'DefaultSiteHQ' 和三個分支。</span><span class="sxs-lookup"><span data-stu-id="4e0a5-146">In this example, hello virtual network 'MultiTier-VNet' has three subnets: 'Frontend', 'Midtier', and 'Backend' subnets, with four cross premises connections: 'DefaultSiteHQ', and three Branches.</span></span> 

<span data-ttu-id="4e0a5-147">hello 步驟會將 hello 'DefaultSiteHQ' 設定為強制通道，hello 預設站台的連線，並設定 hello Midtier 和 Backend 子網路 toouse 強制通道。</span><span class="sxs-lookup"><span data-stu-id="4e0a5-147">hello steps will set hello 'DefaultSiteHQ' as hello default site connection for forced tunneling, and configure hello Midtier and Backend subnets toouse forced tunneling.</span></span>

1. <span data-ttu-id="4e0a5-148">建立路由表。</span><span class="sxs-lookup"><span data-stu-id="4e0a5-148">Create a routing table.</span></span> <span data-ttu-id="4e0a5-149">使用下列 cmdlet toocreate hello 路由表。</span><span class="sxs-lookup"><span data-stu-id="4e0a5-149">Use hello following cmdlet toocreate your route table.</span></span>

  ```powershell
  New-AzureRouteTable –Name "MyRouteTable" –Label "Routing Table for Forced Tunneling" –Location "North Europe"
  ```
2. <span data-ttu-id="4e0a5-150">新增預設路由 toohello 路由表。</span><span class="sxs-lookup"><span data-stu-id="4e0a5-150">Add a default route toohello routing table.</span></span> 

  <span data-ttu-id="4e0a5-151">hello 下列範例會將預設路由 toohello 路由表，在步驟 1 中建立。</span><span class="sxs-lookup"><span data-stu-id="4e0a5-151">hello following example adds a default route toohello routing table created in Step 1.</span></span> <span data-ttu-id="4e0a5-152">請注意，hello 路由支援是 hello 目的地首碼"0.0.0.0/0"toohello"VPNGateway"下一個躍點。</span><span class="sxs-lookup"><span data-stu-id="4e0a5-152">Note that hello only route supported is hello destination prefix of "0.0.0.0/0" toohello "VPNGateway" NextHop.</span></span>

  ```powershell
  Get-AzureRouteTable -Name "MyRouteTable" | Set-AzureRoute –RouteTable "MyRouteTable" –RouteName "DefaultRoute" –AddressPrefix "0.0.0.0/0" –NextHopType VPNGateway
  ```
3. <span data-ttu-id="4e0a5-153">建立 hello 路由表 toohello 子網路的關聯。</span><span class="sxs-lookup"><span data-stu-id="4e0a5-153">Associate hello routing table toohello subnets.</span></span> 

  <span data-ttu-id="4e0a5-154">建立路由表，並加入路由之後，請使用下列範例 tooadd hello 或 hello 路由表 tooa VNet 子網路建立關聯。</span><span class="sxs-lookup"><span data-stu-id="4e0a5-154">After a routing table is created and a route added, use hello following example tooadd or associate hello route table tooa VNet subnet.</span></span> <span data-ttu-id="4e0a5-155">hello 範例新增 hello 路由表"MyRouteTable"toohello Midtier 和後端子網路的 VNet Multitier-vnet。</span><span class="sxs-lookup"><span data-stu-id="4e0a5-155">hello example adds hello route table "MyRouteTable" toohello Midtier and Backend subnets of VNet MultiTier-VNet.</span></span>

  ```powershell
  Set-AzureSubnetRouteTable -VirtualNetworkName "MultiTier-VNet" -SubnetName "Midtier" -RouteTableName "MyRouteTable"
  Set-AzureSubnetRouteTable -VirtualNetworkName "MultiTier-VNet" -SubnetName "Backend" -RouteTableName "MyRouteTable"
  ```
4. <span data-ttu-id="4e0a5-156">為強制通道指派預設站台。</span><span class="sxs-lookup"><span data-stu-id="4e0a5-156">Assign a default site for forced tunneling.</span></span> 

  <span data-ttu-id="4e0a5-157">在前面步驟中的 hello，hello 範例 cmdlet 指令碼建立路由表的 hello 與 hello 路由表 tootwo hello VNet 子網路。</span><span class="sxs-lookup"><span data-stu-id="4e0a5-157">In hello preceding step, hello sample cmdlet scripts created hello routing table and associated hello route table tootwo of hello VNet subnets.</span></span> <span data-ttu-id="4e0a5-158">hello 其餘的步驟是 tooselect hello 多站台連線的 hello 與 hello 預設網站或通道的虛擬網路之間的本機站台。</span><span class="sxs-lookup"><span data-stu-id="4e0a5-158">hello remaining step is tooselect a local site among hello multi-site connections of hello virtual network as hello default site or tunnel.</span></span>

  ```powershell
  $DefaultSite = @("DefaultSiteHQ")
  Set-AzureVNetGatewayDefaultSite –VNetName "MultiTier-VNet" –DefaultSite "DefaultSiteHQ"
  ```

## <a name="additional-powershell-cmdlets"></a><span data-ttu-id="4e0a5-159">其他的 PowerShell Cmdlet</span><span class="sxs-lookup"><span data-stu-id="4e0a5-159">Additional PowerShell cmdlets</span></span>
### <a name="toodelete-a-route-table"></a><span data-ttu-id="4e0a5-160">toodelete 路由表</span><span class="sxs-lookup"><span data-stu-id="4e0a5-160">toodelete a route table</span></span>

```powershell
Remove-AzureRouteTable -Name <routeTableName>
```
  
### <a name="toolist-a-route-table"></a><span data-ttu-id="4e0a5-161">toolist 路由表</span><span class="sxs-lookup"><span data-stu-id="4e0a5-161">toolist a route table</span></span>

```powershell
Get-AzureRouteTable [-Name <routeTableName> [-DetailLevel <detailLevel>]]
```

### <a name="toodelete-a-route-from-a-route-table"></a><span data-ttu-id="4e0a5-162">toodelete 從路由表的路由</span><span class="sxs-lookup"><span data-stu-id="4e0a5-162">toodelete a route from a route table</span></span>

```powershell
Remove-AzureRouteTable –Name <routeTableName>
```

### <a name="tooremove-a-route-from-a-subnet"></a><span data-ttu-id="4e0a5-163">tooremove 從子網路的路由</span><span class="sxs-lookup"><span data-stu-id="4e0a5-163">tooremove a route from a subnet</span></span>

```powershell
Remove-AzureSubnetRouteTable –VirtualNetworkName <virtualNetworkName> -SubnetName <subnetName>
```

### <a name="toolist-hello-route-table-associated-with-a-subnet"></a><span data-ttu-id="4e0a5-164">與子網路相關聯的 toolist hello 路由表</span><span class="sxs-lookup"><span data-stu-id="4e0a5-164">toolist hello route table associated with a subnet</span></span>

```powershell
Get-AzureSubnetRouteTable -VirtualNetworkName <virtualNetworkName> -SubnetName <subnetName>
```

### <a name="tooremove-a-default-site-from-a-vnet-vpn-gateway"></a><span data-ttu-id="4e0a5-165">tooremove 預設站台從 VNet VPN 閘道</span><span class="sxs-lookup"><span data-stu-id="4e0a5-165">tooremove a default site from a VNet VPN gateway</span></span>

```powershell
Remove-AzureVnetGatewayDefaultSite -VNetName <virtualNetworkName>
```