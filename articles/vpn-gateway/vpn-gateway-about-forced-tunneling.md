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
# <a name="configure-forced-tunneling-using-hello-classic-deployment-model"></a>設定強制通道使用 hello 傳統部署模型

強制通道可讓您重新導向或 「 強制 」 所有網際網路繫結流量後 tooyour 在內部部署位置透過站對站 VPN 通道來檢查和稽核。 這是多數企業 IT 原則的重要安全性需求。 如果沒有強制通道，您在 Azure 中的 Vm 所傳來的網際網路繫結流量將一律周遊出 toohello 網際網路，而 hello 選項 tooallow 不直接的 Azure 網路基礎結構從您 tooinspect 或稽核 hello 流量。 Tooinformation 洩漏或其他類型的安全性漏洞，可能會導致未經授權的網際網路存取。

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

這篇文章會引導您設定強制通道使用 hello 傳統部署模型所建立的虛擬網路。 使用 PowerShell，不能透過 hello 入口網站可以設定強制通道。 如果您想 tooconfigure 強制通道的 hello Resource Manager 部署模型時，請從下列下拉式清單中的 hello 中選取傳統的發行項：

> [!div class="op_single_selector"]
> * [PowerShell - 傳統](vpn-gateway-about-forced-tunneling.md)
> * [PowerShell - 資源管理員](vpn-gateway-forced-tunneling-rm.md)
> 
> 

## <a name="requirements-and-considerations"></a>需求和考量
Azure 中的強制通道會透過虛擬網路使用者定義路由 (UDR) 進行設定。 重新導向流量 tooan 內部部署站台以預設路由 toohello Azure VPN 閘道。 hello 下節列出 hello 目前限制的 hello 路由表和路由的 Azure 虛擬網路：

* 每個虛擬網路的子網路皆有內建的系統路由表。 hello 系統路由表具有下列三個路由群組的 hello:

  * **區域的 VNet 路由：**直接 toohello Vm 中的目的地 hello 相同虛擬網路。
  * **在內部部署路由：** toohello Azure VPN 閘道。
  * **預設路由：**直接 toohello 網際網路。 目的地的封包 toohello 私人 IP 位址未涵蓋的 hello 前兩個路由皆會予以捨棄。
* Hello 版本中的使用者定義的路由，您可建立路由表 tooadd 預設路由，並再將關聯 hello 路由表 tooyour VNet 子網路，tooenable 強制通道這些子網路上。
* 您在 hello 跨單位本機站台連線的 toohello 虛擬網路之間需要 tooset 「 預設網站 」。
* 強制通道必須與具有動態路由 VPN 閘道 (非靜態閘道) 的 VNet 相關聯。
* 未設定這項機制，透過 ExpressRoute 強制通道，但相反地，會啟用透過 ExpressRoute BGP hello 將預設路由通告對等互連工作階段。 請參閱 hello [ExpressRoute 文件](https://azure.microsoft.com/documentation/services/expressroute/)如需詳細資訊。

## <a name="configuration-overview"></a>組態概觀
下列範例的 hello，hello 前端子網路則不會強制通道。 hello hello Frontend 子網路中的工作負載可以繼續 tooaccept，並直接從網際網路 hello 回應 toocustomer 要求。 hello mid-tier 和 Backend 子網路會強制通道。 這些兩個子網路 toohello 網際網路任何傳出連線會透過其中一個 S2S VPN 通道連接的 hello 強制或重新導向回 tooan 在內部部署站台。

這可讓您 toorestrict 和檢查您的虛擬機器從網際網路存取，或雲端服務在 Azure 中，同時繼續 tooenable 您所需的多層式服務架構。 您也可以套用強制通道 toohello 整個虛擬網路是否有任何網際網路對向工作負載虛擬網路中。

![強制通道](./media/vpn-gateway-about-forced-tunneling/forced-tunnel.png)

## <a name="before-you-begin"></a>開始之前
請確認您有下列項目開始設定之前的 hello。

* Azure 訂用帳戶。 如果您還沒有 Azure 訂用帳戶，則可以啟用 [MSDN 訂戶權益](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/)或註冊[免費帳戶](https://azure.microsoft.com/pricing/free-trial/)。
* 已設定的虛擬網路。 
* hello 的 hello Azure PowerShell cmdlet 的最新版本。 請參閱[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)如需安裝 hello PowerShell cmdlet 的詳細資訊。

## <a name="configure-forced-tunneling"></a>設定強制通道
hello 遵循程序將協助您指定虛擬網路的強制通道。 hello 設定步驟對應 toohello VNet 網路組態檔。

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

在此範例中，虛擬網路 'Multitier-vnet' hello 有三個子網路: '前端'、 'Midtier，' 和 'Backend' 的子網路，具有四個跨單位連線: 'DefaultSiteHQ' 和三個分支。 

hello 步驟會將 hello 'DefaultSiteHQ' 設定為強制通道，hello 預設站台的連線，並設定 hello Midtier 和 Backend 子網路 toouse 強制通道。

1. 建立路由表。 使用下列 cmdlet toocreate hello 路由表。

  ```powershell
  New-AzureRouteTable –Name "MyRouteTable" –Label "Routing Table for Forced Tunneling" –Location "North Europe"
  ```
2. 新增預設路由 toohello 路由表。 

  hello 下列範例會將預設路由 toohello 路由表，在步驟 1 中建立。 請注意，hello 路由支援是 hello 目的地首碼"0.0.0.0/0"toohello"VPNGateway"下一個躍點。

  ```powershell
  Get-AzureRouteTable -Name "MyRouteTable" | Set-AzureRoute –RouteTable "MyRouteTable" –RouteName "DefaultRoute" –AddressPrefix "0.0.0.0/0" –NextHopType VPNGateway
  ```
3. 建立 hello 路由表 toohello 子網路的關聯。 

  建立路由表，並加入路由之後，請使用下列範例 tooadd hello 或 hello 路由表 tooa VNet 子網路建立關聯。 hello 範例新增 hello 路由表"MyRouteTable"toohello Midtier 和後端子網路的 VNet Multitier-vnet。

  ```powershell
  Set-AzureSubnetRouteTable -VirtualNetworkName "MultiTier-VNet" -SubnetName "Midtier" -RouteTableName "MyRouteTable"
  Set-AzureSubnetRouteTable -VirtualNetworkName "MultiTier-VNet" -SubnetName "Backend" -RouteTableName "MyRouteTable"
  ```
4. 為強制通道指派預設站台。 

  在前面步驟中的 hello，hello 範例 cmdlet 指令碼建立路由表的 hello 與 hello 路由表 tootwo hello VNet 子網路。 hello 其餘的步驟是 tooselect hello 多站台連線的 hello 與 hello 預設網站或通道的虛擬網路之間的本機站台。

  ```powershell
  $DefaultSite = @("DefaultSiteHQ")
  Set-AzureVNetGatewayDefaultSite –VNetName "MultiTier-VNet" –DefaultSite "DefaultSiteHQ"
  ```

## <a name="additional-powershell-cmdlets"></a>其他的 PowerShell Cmdlet
### <a name="toodelete-a-route-table"></a>toodelete 路由表

```powershell
Remove-AzureRouteTable -Name <routeTableName>
```
  
### <a name="toolist-a-route-table"></a>toolist 路由表

```powershell
Get-AzureRouteTable [-Name <routeTableName> [-DetailLevel <detailLevel>]]
```

### <a name="toodelete-a-route-from-a-route-table"></a>toodelete 從路由表的路由

```powershell
Remove-AzureRouteTable –Name <routeTableName>
```

### <a name="tooremove-a-route-from-a-subnet"></a>tooremove 從子網路的路由

```powershell
Remove-AzureSubnetRouteTable –VirtualNetworkName <virtualNetworkName> -SubnetName <subnetName>
```

### <a name="toolist-hello-route-table-associated-with-a-subnet"></a>與子網路相關聯的 toolist hello 路由表

```powershell
Get-AzureSubnetRouteTable -VirtualNetworkName <virtualNetworkName> -SubnetName <subnetName>
```

### <a name="tooremove-a-default-site-from-a-vnet-vpn-gateway"></a>tooremove 預設站台從 VNet VPN 閘道

```powershell
Remove-AzureVnetGatewayDefaultSite -VNetName <virtualNetworkName>
```