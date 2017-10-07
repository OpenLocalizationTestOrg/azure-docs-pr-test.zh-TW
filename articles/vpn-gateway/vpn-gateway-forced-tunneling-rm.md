---
title: "設定 Azure 站對站連線的強制通道：Resource Manager | Microsoft Docs"
description: "如何 tooredirect 或 'force' 所有網際網路繫結流量後 tooyour 內部位置。"
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: cbe58db8-b598-4c9f-ac88-62c865eb8721
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: cherylmc
ms.openlocfilehash: 6bc52c04ab0749a674c9863be5e4f9a9f7c98df4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-forced-tunneling-using-hello-azure-resource-manager-deployment-model"></a>設定強制通道使用 hello Azure Resource Manager 部署模型

強制通道可讓您重新導向或 「 強制 」 所有網際網路繫結流量後 tooyour 在內部部署位置透過站對站 VPN 通道來檢查和稽核。 這是多數企業 IT 原則的重要安全性需求。 如果沒有強制通道，您在 Azure 中的 Vm 所傳來的網際網路繫結流量一律會周遊出 toohello 網際網路，而 hello 選項 tooallow 不直接的 Azure 網路基礎結構從您 tooinspect 或稽核 hello 流量。 Tooinformation 洩漏或其他類型的安全性漏洞，可能會導致未經授權的網際網路存取。

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)] 

這篇文章會引導您設定強制通道使用 hello Resource Manager 部署模型所建立的虛擬網路。 使用 PowerShell，不能透過 hello 入口網站可以設定強制通道。 如果您想 tooconfigure 強制通道 hello 傳統部署模型時，請從下列下拉式清單中的 hello 中選取傳統的發行項：

> [!div class="op_single_selector"]
> * [PowerShell - 傳統](vpn-gateway-about-forced-tunneling.md)
> * [PowerShell - 資源管理員](vpn-gateway-forced-tunneling-rm.md)
> 
> 

## <a name="about-forced-tunneling"></a>有關強制通道

hello 下列圖表說明如何強制通道的運作。 

![強制通道](./media/vpn-gateway-forced-tunneling-rm/forced-tunnel.png)

Hello 上述範例中，在 hello 的前端子網路則不會強制通道。 hello hello Frontend 子網路中的工作負載可以繼續 tooaccept，並直接從網際網路 hello 回應 toocustomer 要求。 hello mid-tier 和 Backend 子網路會強制通道。 這些兩個子網路 toohello 網際網路任何傳出連線會透過其中一個 S2S VPN 通道連接的 hello 強制或重新導向回 tooan 在內部部署站台。

這可讓您 toorestrict 和檢查您的虛擬機器從網際網路存取，或雲端服務在 Azure 中，同時繼續 tooenable 您所需的多層式服務架構。 如果您的虛擬網路中有沒有網際網路對向工作負載，您也可以套用強制通道 toohello 整個虛擬網路。

## <a name="requirements-and-considerations"></a>需求和考量

Azure 中的強制通道處理會透過虛擬網路使用者定義的路由進行設定。 重新導向流量 tooan 內部部署站台以預設路由 toohello Azure VPN 閘道。 如需有關使用者定義路由和虛擬網路的詳細資訊，請參閱[使用者定義路由和 IP 轉送](../virtual-network/virtual-networks-udr-overview.md)。

* 每個虛擬網路的子網路皆有內建的系統路由表。 hello 系統路由表具有下列三個路由群組的 hello:
  
  * **區域的 VNet 路由：**直接 toohello Vm 中的目的地 hello 相同虛擬網路。
  * **在內部部署路由：** toohello Azure VPN 閘道。
  * **預設路由：**直接 toohello 網際網路。 目的地的封包 toohello 私人 IP 位址未涵蓋的 hello 前兩個路由會卸除。
* 這個程序會使用使用者定義的路由 (UDR) toocreate 路由表 tooadd 預設路由，並將產生關聯路由表 tooyour VNet 子網路，tooenable 強制通道這些子網路上的 hello。
* 強制通道必須與具有路由型 VPN 閘道的 VNet 相關聯。 您在 hello 跨單位本機站台連線的 toohello 虛擬網路之間需要 tooset 「 預設網站 」。 此外，hello 內部部署 VPN 裝置必須使用 0.0.0.0/0 做為傳輸選取器設定。 
* 未設定這項機制，透過 ExpressRoute 強制通道，但相反地，會啟用透過 ExpressRoute BGP hello 將預設路由通告對等互連工作階段。 如需詳細資訊，請參閱 hello [ExpressRoute 文件](https://azure.microsoft.com/documentation/services/expressroute/)。

## <a name="configuration-overview"></a>組態概觀

下列程序的 hello 可協助您建立資源群組和 VNet。 然後您將建立 VPN 閘道，並設定強制通道。 在此程序中，虛擬網路 'Multitier-vnet' hello 有三個的子網路: '前端'、 'Midtier，' 和 'Backend'，與四個跨單位連線: 'DefaultSiteHQ' 和三個分支。

hello 程序步驟設定 hello 'DefaultSiteHQ' hello 預設站台連線的強制通道，以及設定 hello 'Midtier' 和 'Backend' 的子網路 toouse 強制通道。

## <a name="before-you-begin"></a>開始之前

安裝 hello hello Azure 資源管理員的 PowerShell 指令程式最新版本。 請參閱[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)如需安裝 hello PowerShell cmdlet 的詳細資訊。

### <a name="toolog-in"></a>toolog 中

[!INCLUDE [toolog in](../../includes/vpn-gateway-ps-login-include.md)]

## <a name="configure-forced-tunneling"></a>設定強制通道

1. 建立資源群組。

  ```powershell
  New-AzureRmResourceGroup -Name 'ForcedTunneling' -Location 'North Europe'
  ```
2. 建立虛擬網路並指定子網路。

  ```powershell 
  $s1 = New-AzureRmVirtualNetworkSubnetConfig -Name "Frontend" -AddressPrefix "10.1.0.0/24"
  $s2 = New-AzureRmVirtualNetworkSubnetConfig -Name "Midtier" -AddressPrefix "10.1.1.0/24"
  $s3 = New-AzureRmVirtualNetworkSubnetConfig -Name "Backend" -AddressPrefix "10.1.2.0/24"
  $s4 = New-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -AddressPrefix "10.1.200.0/28"
  $vnet = New-AzureRmVirtualNetwork -Name "MultiTier-VNet" -Location "North Europe" -ResourceGroupName "ForcedTunneling" -AddressPrefix "10.1.0.0/16" -Subnet $s1,$s2,$s3,$s4
  ```
3. 建立 hello 區域網路閘道。

  ```powershell
  $lng1 = New-AzureRmLocalNetworkGateway -Name "DefaultSiteHQ" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -GatewayIpAddress "111.111.111.111" -AddressPrefix "192.168.1.0/24"
  $lng2 = New-AzureRmLocalNetworkGateway -Name "Branch1" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -GatewayIpAddress "111.111.111.112" -AddressPrefix "192.168.2.0/24"
  $lng3 = New-AzureRmLocalNetworkGateway -Name "Branch2" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -GatewayIpAddress "111.111.111.113" -AddressPrefix "192.168.3.0/24"
  $lng4 = New-AzureRmLocalNetworkGateway -Name "Branch3" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -GatewayIpAddress "111.111.111.114" -AddressPrefix "192.168.4.0/24"
  ```
4. 建立 hello 路由表和路由規則。

  ```powershell
  New-AzureRmRouteTable –Name "MyRouteTable" -ResourceGroupName "ForcedTunneling" –Location "North Europe"
  $rt = Get-AzureRmRouteTable –Name "MyRouteTable" -ResourceGroupName "ForcedTunneling" 
  Add-AzureRmRouteConfig -Name "DefaultRoute" -AddressPrefix "0.0.0.0/0" -NextHopType VirtualNetworkGateway -RouteTable $rt
  Set-AzureRmRouteTable -RouteTable $rt
  ```
5. 讓 hello 路由表 toohello Midtier 和後端子網路產生關聯。

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -Name "MultiTier-Vnet" -ResourceGroupName "ForcedTunneling"
  Set-AzureRmVirtualNetworkSubnetConfig -Name "MidTier" -VirtualNetwork $vnet -AddressPrefix "10.1.1.0/24" -RouteTable $rt
  Set-AzureRmVirtualNetworkSubnetConfig -Name "Backend" -VirtualNetwork $vnet -AddressPrefix "10.1.2.0/24" -RouteTable $rt
  Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
  ```
6. 建立 hello 閘道與預設網站。 這個步驟需要一些時間 toocomplete，有時 45 分鐘以上，因為您建立和設定 hello 閘道。<br> hello **-GatewayDefaultSite**是 hello 指令程式參數，可讓 hello 強制路由組態 toowork，所以請小心 tooconfigure 設定正確。 此參數僅適用於 PowerShell 1.0 或更新版本。

  ```powershell
  $pip = New-AzureRmPublicIpAddress -Name "GatewayIP" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -AllocationMethod Dynamic
  $gwsubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
  $ipconfig = New-AzureRmVirtualNetworkGatewayIpConfig -Name "gwIpConfig" -SubnetId $gwsubnet.Id -PublicIpAddressId $pip.Id
  New-AzureRmVirtualNetworkGateway -Name "Gateway1" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -IpConfigurations $ipconfig -GatewayType Vpn -VpnType RouteBased -GatewaySku VpnGw1 -GatewayDefaultSite $lng1 -EnableBgp $false
  ```
7. 建立 hello 站對站 VPN 連線。

  ```powershell
  $gateway = Get-AzureRmVirtualNetworkGateway -Name "Gateway1" -ResourceGroupName "ForcedTunneling"
  $lng1 = Get-AzureRmLocalNetworkGateway -Name "DefaultSiteHQ" -ResourceGroupName "ForcedTunneling" 
  $lng2 = Get-AzureRmLocalNetworkGateway -Name "Branch1" -ResourceGroupName "ForcedTunneling" 
  $lng3 = Get-AzureRmLocalNetworkGateway -Name "Branch2" -ResourceGroupName "ForcedTunneling" 
  $lng4 = Get-AzureRmLocalNetworkGateway -Name "Branch3" -ResourceGroupName "ForcedTunneling" 
    
  New-AzureRmVirtualNetworkGatewayConnection -Name "Connection1" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -VirtualNetworkGateway1 $gateway -LocalNetworkGateway2 $lng1 -ConnectionType IPsec -SharedKey "preSharedKey"
  New-AzureRmVirtualNetworkGatewayConnection -Name "Connection2" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -VirtualNetworkGateway1 $gateway -LocalNetworkGateway2 $lng2 -ConnectionType IPsec -SharedKey "preSharedKey"
  New-AzureRmVirtualNetworkGatewayConnection -Name "Connection3" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -VirtualNetworkGateway1 $gateway -LocalNetworkGateway2 $lng3 -ConnectionType IPsec -SharedKey "preSharedKey"
  New-AzureRmVirtualNetworkGatewayConnection -Name "Connection4" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -VirtualNetworkGateway1 $gateway -LocalNetworkGateway2 $lng4 -ConnectionType IPsec -SharedKey "preSharedKey"
    
  Get-AzureRmVirtualNetworkGatewayConnection -Name "Connection1" -ResourceGroupName "ForcedTunneling"
  ```