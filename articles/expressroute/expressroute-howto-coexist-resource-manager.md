---
title: "設定可以並存的 ExpressRoute 和站對站 VPN 連線：Resource Manager：Azure | Microsoft Docs"
description: "本文會引導您針對 Resource Manager 部署模型設定可以並存的 ExpressRoute 和站對站 VPN 連線。"
documentationcenter: na
services: expressroute
author: charwen
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: c7717b14-3da3-4a6d-b78e-a5020766bc2c
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/19/2017
ms.author: charwen,cherylmc
ms.openlocfilehash: efda9f89d95617c8c4e75af91b20631dc468d4db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-expressroute-and-site-to-site-coexisting-connections"></a>設定 ExpressRoute 和站對站並存連線
> [!div class="op_single_selector"]
> * [PowerShell - Resource Manager](expressroute-howto-coexist-resource-manager.md)
> * [PowerShell - 傳統](expressroute-howto-coexist-classic.md)
> 
> 

設定站對站 VPN 和 ExpressRoute 並存連線有諸多好處。 您可以設定站對站 VPN，安全的容錯移轉路徑做為 ExressRoute，或使用站對站 Vpn tooconnect toosites 不透過 ExpressRoute 連接。 我們將討論 hello 步驟 tooconfigure 本文章中的這兩種案例。 本文適用於 toohello Resource Manager 部署模型，並使用 PowerShell。 此設定不適用於 hello Azure 入口網站。

> [!IMPORTANT]
> ExpressRoute 電路必須預先設定，才能執行下列的 hello 指示。 請確定您已依照 hello 指南太[建立 ExpressRoute 電路](expressroute-howto-circuit-arm.md)和[設定路由](expressroute-howto-routing-arm.md)在繼續之前。
> 
> 

## <a name="limits-and-limitations"></a>限制
* **不支援傳輸路由。** 您無法在透過站對站 VPN 連線的區域網路與透過 ExpressRoute 連線的區域網路之間，進行路由傳送 (透過 Azure)。
* **不支援基本 SKU 閘道。** 您必須使用非基本 SKU 閘道可取得這兩個 hello [ExpressRoute 閘道](expressroute-about-virtual-network-gateways.md)和 hello [VPN 閘道](../vpn-gateway/vpn-gateway-about-vpngateways.md)。
* **僅支援路由式 VPN 閘道。** 您必須使用路由式 [VPN 閘道](../vpn-gateway/vpn-gateway-about-vpngateways.md)。
* **應該為 VPN 閘道設定靜態路由。** 如果您的區域網路連線的 tooboth ExpressRoute 而且網站間 VPN，您必須在您區域網路 tooroute hello 站對站 VPN 連線 toohello 中設定的靜態路由公用網際網路。
* **您必須先設定 ExpressRoute 閘道，並連結 tooa 循環。** 您必須先建立 hello ExpressRoute 閘道，並將它連結 tooa 循環，然後再新增 hello 站對站 VPN 閘道。

## <a name="configuration-designs"></a>組態設計
### <a name="configure-a-site-to-site-vpn-as-a-failover-path-for-expressroute"></a>設定站對站 VPN 作為 ExpressRoute 的容錯移轉路徑
您可以設定站對站 VPN 連線作為 ExpressRoute 的備用連線。 這適用於僅 toovirtual 網路連結的 toohello Azure 私人互連路徑。 對於可透過 Azure 公用和 Microsoft 對等存取的服務，沒有 VPN 架構的容錯移轉解決方案。 hello ExpressRoute 電路一律為 hello 主要連結。 資料流過 hello 站對站 VPN 路徑只有 hello ExpressRoute 電路失敗時。

> [!NOTE]
> 雖然 ExpressRoute 循環時，最好透過站對站 VPN 這兩個路由是 hello 相同，則 Azure 會使用 hello 最長前置詞比對 toochoose hello 路由朝向 hello 封包的目的地。
> 
> 

![並存](media/expressroute-howto-coexist-resource-manager/scenario1.jpg)

### <a name="configure-a-site-to-site-vpn-tooconnect-toosites-not-connected-through-expressroute"></a>設定站對站 VPN tooconnect toosites 未透過 ExpressRoute 連線
您可以設定您的網路，其中某些站台直接 tooAzure 透過站對站 VPN 連接，而透過 ExpressRoute 連接某些站台。 

![並存](media/expressroute-howto-coexist-resource-manager/scenario2.jpg)

> [!NOTE]
> 您無法將虛擬網路設定為轉送路由器。
> 
> 

## <a name="selecting-hello-steps-toouse"></a>選取 hello 步驟 toouse
有兩組不同的程序 toochoose 從。 您選取的 hello 組態程序取決於您擁有現有的虛擬網路，您會想 tooconnect，或是 toocreate 新的虛擬網路。

* 我不具有 VNet，而且需要 toocreate 其中一個。
  
    如果您還沒有虛擬網路，這個程序將引導您使用 Resource Manager 部署模型來建立新的虛擬網路，並建立新的 ExpressRoute 和站對站 VPN 連線。 tooconfigure 虛擬網路，請依照下列中的 hello 步驟[toocreate 新的虛擬網路和共存連線](#new)。
* 我已經有一個 Resource Manager 部署模型 VNet。
  
    您可能已經有虛擬網路，而且使用現有的站對站 VPN 連線或 ExpressRoute 連線。 hello [tooconfigure 共存連線已存在的 vnet](#add) > 一節將引導您刪除 hello 閘道，然後建立新的 ExpressRoute 以及站台對站台 VPN 連線。 在建立新的連線時 hello，hello 步驟都必須以特定順序完成。 請勿使用其他發行項 toocreate hello 指示進行，您的閘道和連線。
  
    在此程序，建立可同時存在的連線需要您 toodelete 閘道，而然後設定新的閘道。 您必須跨單位連線的停機時間時就刪除並重新建立您的閘道與連線，但您不需要 toomigrate 任何 Vm 或服務 tooa 新的虛擬網路。 Vm 和服務仍會無法 toocommunicate 出透過 hello 負載平衡器時所設定的 toodo 因此，設定您的閘道。

## <a name="new"></a>toocreate 新的虛擬網路和共存的連線
此程序會引導您建立會並存的 VNet、站對站和 ExpressRoute 連線。

1. 安裝 Azure PowerShell cmdlet hello hello 最新版本。 如需安裝 hello cmdlet 的資訊，請參閱[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)。 hello cmdlet 可讓您針對此組態可能會與您可能的熟悉稍有不同。 確定 toouse hello cmdlet 這些指示中指定。
2. 登入 tooyour 帳戶，並設定 hello 環境。

  ```powershell
  login-AzureRmAccount
  Select-AzureRmSubscription -SubscriptionName 'yoursubscription'
  $location = "Central US"
  $resgrp = New-AzureRmResourceGroup -Name "ErVpnCoex" -Location $location
  $VNetASN = 65010
  ```
3. 建立包含閘道子網路的虛擬網路。 如需 hello 虛擬網路組態的詳細資訊，請參閱[Azure 虛擬網路組態](../virtual-network/virtual-networks-create-vnet-arm-ps.md)。
   
   > [!IMPORTANT]
   > hello 閘道子網路必須 /27 或短的前置詞 （例如 /26 或 /25）。
   > 
   > 
   
    建立新的 VNet。

  ```powershell
  $vnet = New-AzureRmVirtualNetwork -Name "CoexVnet" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -AddressPrefix "10.200.0.0/16"
  ```
   
    新增子網路。

  ```powershell
  Add-AzureRmVirtualNetworkSubnetConfig -Name "App" -VirtualNetwork $vnet -AddressPrefix "10.200.1.0/24"
  Add-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet -AddressPrefix "10.200.255.0/24"
  ```
   
    儲存 hello VNet 組態。

  ```powershell
  $vnet = Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
  ```
4. <a name="gw"></a>建立 ExpressRoute 閘道。 如需 hello ExpressRoute 閘道設定的詳細資訊，請參閱[ExpressRoute 閘道組態](expressroute-howto-add-gateway-resource-manager.md)。 hello GatewaySKU 必須*標準*， *HighPerformance*，或*UltraPerformance*。

  ```powershell
  $gwSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
  $gwIP = New-AzureRmPublicIpAddress -Name "ERGatewayIP" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -AllocationMethod Dynamic
  $gwConfig = New-AzureRmVirtualNetworkGatewayIpConfig -Name "ERGatewayIpConfig" -SubnetId $gwSubnet.Id -PublicIpAddressId $gwIP.Id
  $gw = New-AzureRmVirtualNetworkGateway -Name "ERGateway" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -IpConfigurations $gwConfig -GatewayType "ExpressRoute" -GatewaySku Standard
  ```
5. 連結 hello ExpressRoute 閘道 toohello ExpressRoute 電路。 在完成這個步驟之後，會建立 hello 與內部網路與 Azure 中的，透過 ExpressRoute，之間的連線。 如需 hello 連結作業的詳細資訊，請參閱[連結 Vnet tooExpressRoute](expressroute-howto-linkvnet-arm.md)。

  ```powershell
  $ckt = Get-AzureRmExpressRouteCircuit -Name "YourCircuit" -ResourceGroupName "YourCircuitResourceGroup"
  New-AzureRmVirtualNetworkGatewayConnection -Name "ERConnection" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -VirtualNetworkGateway1 $gw -PeerId $ckt.Id -ConnectionType ExpressRoute
  ```
6. <a name="vpngw"></a>接下來，建立站對站 VPN 閘道。 如需 hello VPN 閘道設定的詳細資訊，請參閱[站對站連線設定 VNet](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md)。 hello GatewaySKU 必須*標準*， *HighPerformance*，或*UltraPerformance*。 hello VpnType 必須*RouteBased*。

  ```powershell
  $gwSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
  $gwIP = New-AzureRmPublicIpAddress -Name "VPNGatewayIP" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -AllocationMethod Dynamic
  $gwConfig = New-AzureRmVirtualNetworkGatewayIpConfig -Name "VPNGatewayIpConfig" -SubnetId $gwSubnet.Id -PublicIpAddressId $gwIP.Id
  New-AzureRmVirtualNetworkGateway -Name "VPNGateway" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -IpConfigurations $gwConfig -GatewayType "Vpn" -VpnType "RouteBased" -GatewaySku "Standard"
  ```
   
    Azure VPN 閘道支援 BGP 路由通訊協定。 您可以在 hello 下列命令中加入 hello-Asn 交換器，該虛擬網路指定 ASN （AS 號碼）。 未指定該參數會預設 tooAS 號碼 65515。

  ```powershell
  $azureVpn = New-AzureRmVirtualNetworkGateway -Name "VPNGateway" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -IpConfigurations $gwConfig -GatewayType "Vpn" -VpnType "RouteBased" -GatewaySku "Standard" -Asn $VNetASN
  ```
   
    您可以找到 hello BGP 對等 IP 和 hello Azure hello $azureVpn.BgpSettings.BgpPeeringAddress 和 $azureVpn.BgpSettings.Asn 中的 VPN 閘道使用的數字。 如需詳細資訊，請參閱針對 Azure VPN 閘道[設定 BGP](../vpn-gateway/vpn-gateway-bgp-resource-manager-ps.md)。
7. 建立本機的站台 VPN 閘道實體。 此命令不會設定內部部署 VPN 閘道。 相反地，它可讓您 tooprovide hello 本機閘道設定，例如 hello 公用 IP 和 hello 在內部部署位址空間，如此 hello Azure VPN 閘道可以連線 tooit。
   
    如果本機 VPN 裝置僅支援靜態路由，您可以在 hello 下列方式設定 hello 靜態路由：

  ```powershell
  $MyLocalNetworkAddress = @("10.100.0.0/16","10.101.0.0/16","10.102.0.0/16")
  $localVpn = New-AzureRmLocalNetworkGateway -Name "LocalVPNGateway" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -GatewayIpAddress *<Public IP>* -AddressPrefix $MyLocalNetworkAddress
  ```
   
    如果本機 VPN 裝置支援 hello BGP，並想 tooenable 動態路由，您需要 tooknow hello BGP 對等互連 IP 與 hello 因為數字，您的本機 VPN 裝置使用。

  ```powershell
  $localVPNPublicIP = "<Public IP>"
  $localBGPPeeringIP = "<Private IP for hello BGP session>"
  $localBGPASN = "<ASN>"
  $localAddressPrefix = $localBGPPeeringIP + "/32"
  $localVpn = New-AzureRmLocalNetworkGateway -Name "LocalVPNGateway" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -GatewayIpAddress $localVPNPublicIP -AddressPrefix $localAddressPrefix -BgpPeeringAddress $localBGPPeeringIP -Asn $localBGPASN
  ```
8. 設定本機 VPN 裝置 tooconnect toohello 新 Azure VPN 閘道。 如需關於 VPN 裝置組態的詳細資訊，請參閱 [VPN 裝置組態](../vpn-gateway/vpn-gateway-about-vpn-devices.md)。
9. 連結 hello Azure toohello 本機閘道上的站對站 VPN 閘道。

  ```powershell
  $azureVpn = Get-AzureRmVirtualNetworkGateway -Name "VPNGateway" -ResourceGroupName $resgrp.ResourceGroupName
  New-AzureRmVirtualNetworkGatewayConnection -Name "VPNConnection" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -VirtualNetworkGateway1 $azureVpn -LocalNetworkGateway2 $localVpn -ConnectionType IPsec -SharedKey <yourkey>
  ```

## <a name="add"></a>tooconfigure 共存連線已存在的 vnet
如果您有現有的虛擬網路，請檢查 hello 閘道子網路大小。 如果 hello 閘道子網路是/28 或 29，您必須先刪除 hello 虛擬網路閘道並增加 hello 閘道子網路大小。 hello 本節中的步驟示範 toodo 的。

Hello 閘道子網路是否 /27 或更大而且透過 ExpressRoute 連接 hello 虛擬網路，您可以略過下列步驟 hello 而太[[步驟 6-建立站對站 VPN 閘道]](#vpngw) hello 前一節中。 

> [!NOTE]
> 當您刪除 hello 現有閘道時，您本機內部部署將會遺失 hello 連接 tooyour 虛擬網路，當您使用此設定。 
> 
> 

1. 您將需要 tooinstall hello 最新版本的 hello Azure PowerShell cmdlet。 如需有關如何安裝 cmdlet 的詳細資訊，請參閱[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)。 hello cmdlet 可讓您針對此組態可能會與您可能的熟悉稍有不同。 確定 toouse hello cmdlet 這些指示中指定。 
2. 刪除 hello 現有 ExpressRoute 或站對站 VPN 閘道。

  ```powershell 
  Remove-AzureRmVirtualNetworkGateway -Name <yourgatewayname> -ResourceGroupName <yourresourcegroup>
  ```
3. 刪除閘道子網路。

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -Name <yourvnetname> -ResourceGroupName <yourresourcegroup> Remove-AzureRmVirtualNetworkSubnetConfig -Name GatewaySubnet -VirtualNetwork $vnet
  ```
4. 新增 /27 或更大的閘道子網路。
   
   > [!NOTE]
   > 如果您沒有足夠的 IP 位址保留在您虛擬網路 tooincrease hello 閘道子網路大小，您需要 tooadd 多個 IP 位址空間。
   > 
   > 

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -Name <yourvnetname> -ResourceGroupName <yourresourcegroup>
  Add-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet -AddressPrefix "10.200.255.0/24"
  ```
   
    儲存 hello VNet 組態。

  ```powershell
  $vnet = Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
  ```
5. 此時，您會使用沒有閘道器的 VNet。 toocreate 新的閘道完成您的連線，您可以繼續使用[步驟 4-建立 ExpressRoute 閘道](#gw)、 在 hello 前面的步驟中找到。

## <a name="tooadd-point-to-site-configuration-toohello-vpn-gateway"></a>tooadd 點對站組態 toohello VPN 閘道
您可以依照下列 tooadd 點對站組態 tooyour 共存安裝程式中的 VPN 閘道的 hello 步驟。

1. 新增 VPN 用戶端位址集區。

  ```powershell
  $azureVpn = Get-AzureRmVirtualNetworkGateway -Name "VPNGateway" -ResourceGroupName $resgrp.ResourceGroupName
  Set-AzureRmVirtualNetworkGatewayVpnClientConfig -VirtualNetworkGateway $azureVpn -VpnClientAddressPool "10.251.251.0/24"
  ```
2. 上傳 hello VPN 根憑證 tooAzure VPN 閘道。 在此範例中，它會假設該 hello 根憑證會儲存在 hello 本機電腦執行下列 PowerShell 指令程式的 hello。

  ```powershell
  $p2sCertFullName = "RootErVpnCoexP2S.cer" 
  $p2sCertMatchName = "RootErVpnCoexP2S" 
  $p2sCertToUpload=get-childitem Cert:\CurrentUser\My | Where-Object {$_.Subject -match $p2sCertMatchName} 
  if ($p2sCertToUpload.count -eq 1){write-host "cert found"} else {write-host "cert not found" exit} 
  $p2sCertData = [System.Convert]::ToBase64String($p2sCertToUpload.RawData) Add-AzureRmVpnClientRootCertificate -VpnClientRootCertificateName $p2sCertFullName -VirtualNetworkGatewayname $azureVpn.Name -ResourceGroupName $resgrp.ResourceGroupName -PublicCertData $p2sCertData
  ```

如需點對站 VPN 的詳細資訊，請參閱 [設定點對站連線](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md)。

## <a name="next-steps"></a>後續步驟
如需 ExpressRoute 的詳細資訊，請參閱 hello [ExpressRoute 常見問題集](expressroute-faqs.md)。
