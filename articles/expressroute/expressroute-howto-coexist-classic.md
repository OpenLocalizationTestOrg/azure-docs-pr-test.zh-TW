---
title: "設定可以並存的 ExpressRoute 和站對站 VPN 連線：傳統：Azure | Microsoft Docs"
description: "這篇文章會引導您設定 ExpressRoute 和 hello 傳統部署模型可同時存在站對站 VPN 連線。"
documentationcenter: na
services: expressroute
author: charwen
manager: carmonm
editor: 
tags: azure-service-management
ms.assetid: dcf1a5af-a289-466a-b812-0bfedbd2bda0
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/21/2017
ms.author: charwen
ms.openlocfilehash: abb30fff55e8ec243f2920c5b2f70c43717755fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-expressroute-and-site-to-site-coexisting-connections-classic"></a>設定 ExpressRoute 和站對站並存連線 (傳統)
> [!div class="op_single_selector"]
> * [PowerShell - 資源管理員](expressroute-howto-coexist-resource-manager.md)
> * [PowerShell - 傳統](expressroute-howto-coexist-classic.md)
> 
> 

Hello 能力 tooconfigure 站對站 VPN 和 ExpressRoute 會有幾項優點。 您可以設定站對站 VPN，安全的容錯移轉路徑做為 ExressRoute，或使用站對站 Vpn tooconnect toosites 不透過 ExpressRoute 連接。 我們將討論 hello 步驟 tooconfigure 本文章中的這兩種案例。 本文適用於 toohello 傳統部署模型。 此設定不在 hello 入口網站。

[!INCLUDE [expressroute-classic-end-include](../../includes/expressroute-classic-end-include.md)]

**關於 Azure 部署模型**

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

> [!IMPORTANT]
> ExpressRoute 電路必須預先設定，才能執行下列的 hello 指示。 請確定您已依照 hello 指南太[建立 ExpressRoute 電路](expressroute-howto-circuit-classic.md)和[設定路由](expressroute-howto-routing-classic.md)依照下列步驟 hello 之前。
> 
> 

## <a name="limits-and-limitations"></a>限制
* **不支援傳輸路由。** 您無法在透過站對站 VPN 連線的區域網路與透過 ExpressRoute 連線的區域網路之間，進行路由傳送 (透過 Azure)。
* **不支援點對站連線。** 您無法啟用點對站 VPN 連線 toohello 連接的 tooExpressRoute 相同 VNet。 點對站 VPN 和 ExpressRoute 不能共存在 hello 相同 VNet。
* **無法在 hello 站對站 VPN 閘道上啟用強制通道。** 您可以只 「 強制 」 所有網際網路繫結流量後 tooyour 在內部部署網路透過 ExpressRoute。
* **不支援基本 SKU 閘道。** 您必須使用非基本 SKU 閘道可取得這兩個 hello [ExpressRoute 閘道](expressroute-about-virtual-network-gateways.md)和 hello [VPN 閘道](../vpn-gateway/vpn-gateway-about-vpngateways.md)。
* **僅支援路由式 VPN 閘道。** 您必須使用路由式 [VPN 閘道](../vpn-gateway/vpn-gateway-about-vpngateways.md)。
* **應該為 VPN 閘道設定靜態路由。** 如果您的區域網路連線的 tooboth ExpressRoute 而且網站間 VPN，您必須在您區域網路 tooroute hello 站對站 VPN 連線 toohello 中設定的靜態路由公用網際網路。
* **必須先設定 ExpressRoute 閘道。** 新增 hello 站對站 VPN 閘道之前，您必須先建立 hello ExpressRoute 閘道。

## <a name="configuration-designs"></a>組態設計
### <a name="configure-a-site-to-site-vpn-as-a-failover-path-for-expressroute"></a>設定站對站 VPN 作為 ExpressRoute 的容錯移轉路徑
您可以設定站對站 VPN 連線作為 ExpressRoute 的備用連線。 這適用於僅 toovirtual 網路連結的 toohello Azure 私人互連路徑。 對於可透過 Azure 公用和 Microsoft 對等存取的服務，沒有 VPN 架構的容錯移轉解決方案。 hello ExpressRoute 電路一律為 hello 主要連結。 只有 hello ExpressRoute 電路失敗時，資料會流透過 hello 站對站 VPN 的路徑。 

> [!NOTE]
> 雖然 ExpressRoute 循環時，最好透過站對站 VPN 這兩個路由是 hello 相同，則 Azure 會使用 hello 最長前置詞比對 toochoose hello 路由朝向 hello 封包的目的地。
> 
> 

![並存](media/expressroute-howto-coexist-classic/scenario1.jpg)

### <a name="configure-a-site-to-site-vpn-tooconnect-toosites-not-connected-through-expressroute"></a>設定站對站 VPN tooconnect toosites 未透過 ExpressRoute 連線
您可以設定您的網路，其中某些站台直接 tooAzure 透過站對站 VPN 連接，而透過 ExpressRoute 連接某些站台。 

![並存](media/expressroute-howto-coexist-classic/scenario2.jpg)

> [!NOTE]
> 您無法將虛擬網路設定為轉送路由器。
> 
> 

## <a name="selecting-hello-steps-toouse"></a>選取 hello 步驟 toouse
有兩組不同的程序 toochoose 從順序 tooconfigure 連接中，可以共存。 您選取的 hello 組態程序將取決於您是否有現有的虛擬網路，您會想 tooconnect，或是 toocreate 新的虛擬網路。

* 我不具有 VNet，而且需要 toocreate 其中一個。
  
    如果您還沒有虛擬網路，此程序將逐步引導您建立新的虛擬網路使用 hello 傳統部署模型，並建立新的 ExpressRoute 以及站台對站台 VPN 連線。 tooconfigure，遵循 hello 發行項 > 一節中的 hello 步驟[toocreate 新的虛擬網路和共存連線](#new)。
* 我已經有一個傳統部署模型 VNet。
  
    您可能已經有虛擬網路，而且使用現有的站對站 VPN 連線或 ExpressRoute 連線。 hello 文章區段[tooconfigure coexsiting 連線已存在的 vnet](#add)將逐步引導您透過刪除 hello 閘道，然後建立新的 ExpressRoute 和站對站 VPN 連線。 請注意，在建立新的連線時 hello，hello 必須完成步驟非常特定的順序。 請勿使用其他發行項 toocreate hello 指示進行，您的閘道和連線。
  
    在此程序，建立可同時存在的連接會需要您 toodelete 您的閘道，然後設定新的閘道。 這表示您必須跨單位連線的停機時間時就刪除並重新建立您的閘道與連線，但您不需要 toomigrate 任何 Vm 或服務 tooa 新的虛擬網路。 Vm 和服務仍會無法 toocommunicate 出透過 hello 負載平衡器時所設定的 toodo 因此，設定您的閘道。

## <a name="new"></a>toocreate 新的虛擬網路和共存的連線
此程序會引導您建立 VNet，並建立將並存的站對站和 ExpressRoute 連線。

1. 您將需要 tooinstall hello 最新版本的 hello Azure PowerShell cmdlet。 請參閱[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)如需安裝 hello PowerShell cmdlet 的詳細資訊。 請注意 hello cmdlet，您將使用此組態可能會與您可能的熟悉稍有不同。 確定 toouse hello cmdlet 這些指示中指定。 
2. 建立虛擬網路的結構描述。 如需 hello 組態結構描述的詳細資訊，請參閱[Azure 虛擬網路組態結構描述](https://msdn.microsoft.com/library/azure/jj157100.aspx)。
   
    當您建立您的結構描述時，請確定您使用下列值的 hello:
   
   * hello hello 虛擬網路的閘道子網路必須 /27 或短的前置詞 （例如 /26 或 /25）。
   * hello 閘道連線類型是 「 專用。 」
     
             <VirtualNetworkSite name="MyAzureVNET" Location="Central US">
               <AddressSpace>
                 <AddressPrefix>10.17.159.192/26</AddressPrefix>
               </AddressSpace>
               <Subnets>
                 <Subnet name="Subnet-1">
                   <AddressPrefix>10.17.159.192/27</AddressPrefix>
                 </Subnet>
                 <Subnet name="GatewaySubnet">
                   <AddressPrefix>10.17.159.224/27</AddressPrefix>
                 </Subnet>
               </Subnets>
               <Gateway>
                 <ConnectionsToLocalNetwork>
                   <LocalNetworkSiteRef name="MyLocalNetwork">
                     <Connection type="Dedicated" />
                   </LocalNetworkSiteRef>
                 </ConnectionsToLocalNetwork>
               </Gateway>
             </VirtualNetworkSite>
3. 建立及設定您的 xml 結構描述檔案之後, hello 檔案上傳。 這樣會建立您的虛擬網路。
   
    使用下列 cmdlet tooupload hello 檔案，取代您自己 hello 值。
   
        Set-AzureVNetConfig -ConfigurationPath 'C:\NetworkConfig.xml'
4. <a name="gw"></a>建立 ExpressRoute 閘道。 是確定 toospecify hello 做為 GatewaySKU*標準*， *HighPerformance*，或*UltraPerformance* hello 做為 gatewaytype 的授權和*DynamicRouting*.
   
    使用下列範例中，取代為您自己的 hello 值 hello。
   
        New-AzureVNetGateway -VNetName MyAzureVNET -GatewayType DynamicRouting -GatewaySKU HighPerformance
5. 連結 hello ExpressRoute 閘道 toohello ExpressRoute 電路。 在完成這個步驟之後，會建立 hello 與內部網路與 Azure 中的，透過 ExpressRoute，之間的連線。
   
        New-AzureDedicatedCircuitLink -ServiceKey <service-key> -VNetName MyAzureVNET
6. <a name="vpngw"></a>接下來，建立站對站 VPN 閘道。 hello GatewaySKU 必須*標準*， *HighPerformance*，或*UltraPerformance*而且 hello gatewaytype 的授權必須*DynamicRouting*。
   
        New-AzureVirtualNetworkGateway -VNetName MyAzureVNET -GatewayName S2SVPN -GatewayType DynamicRouting -GatewaySKU  HighPerformance
   
    tooretrieve hello 虛擬網路閘道設定，包括 hello 閘道識別碼和 hello 公用 IP，使用 hello `Get-AzureVirtualNetworkGateway` cmdlet。
   
        Get-AzureVirtualNetworkGateway
   
        GatewayId            : 348ae011-ffa9-4add-b530-7cb30010565e
        GatewayName          : S2SVPN
        LastEventData        :
        GatewayType          : DynamicRouting
        LastEventTimeStamp   : 5/29/2015 4:41:41 PM
        LastEventMessage     : Successfully created a gateway for hello following virtual network: GNSDesMoines
        LastEventID          : 23002
        State                : Provisioned
        VIPAddress           : 104.43.x.y
        DefaultSite          :
        GatewaySKU           : HighPerformance
        Location             :
        VnetId               : 979aabcf-e47f-4136-ab9b-b4780c1e1bd5
        SubnetId             :
        EnableBgp            : False
        OperationDescription : Get-AzureVirtualNetworkGateway
        OperationId          : 42773656-85e1-a6b6-8705-35473f1e6f6a
        OperationStatus      : Succeeded
7. 建立本機的站台 VPN 閘道實體。 此命令不會設定內部部署 VPN 閘道。 相反地，它可讓您 tooprovide hello 本機閘道設定，例如 hello 公用 IP 和 hello 在內部部署位址空間，如此 hello Azure VPN 閘道可以連線 tooit。
   
   > [!IMPORTANT]
   > hello netcfg 中未定義本機 hello hello 站對站 VPN 站台。 相反地，您必須使用這個指令程式 toospecify hello 本機站台參數。 您無法使用入口網站或 hello netcfg 檔案，其定義。
   > 
   > 
   
    使用下列範例中，取代您自己 hello 值 hello。
   
        New-AzureLocalNetworkGateway -GatewayName MyLocalNetwork -IpAddress <MyLocalGatewayIp> -AddressSpace <MyLocalNetworkAddress>
   
   > [!NOTE]
   > 如果您的區域網路有多個路由，您可以將它們全部放在陣列中傳遞。  $MyLocalNetworkAddress = @("10.1.2.0/24","10.1.3.0/24","10.2.1.0/24")  
   > 
   > 

    tooretrieve hello 虛擬網路閘道設定，包括 hello 閘道識別碼和 hello 公用 IP，使用 hello `Get-AzureVirtualNetworkGateway` cmdlet。 請參閱下列範例中的 hello。

        Get-AzureLocalNetworkGateway

        GatewayId            : 532cb428-8c8c-4596-9a4f-7ae3a9fcd01b
        GatewayName          : MyLocalNetwork
        IpAddress            : 23.39.x.y
        AddressSpace         : {10.1.2.0/24}
        OperationDescription : Get-AzureLocalNetworkGateway
        OperationId          : ddc4bfae-502c-adc7-bd7d-1efbc00b3fe5
        OperationStatus      : Succeeded


1. 設定本機 VPN 裝置 tooconnect toohello 新閘道。 使用您在步驟 6 中設定 VPN 裝置時擷取的 hello 資訊。 如需關於 VPN 裝置組態的詳細資訊，請參閱 [VPN 裝置組態](../vpn-gateway/vpn-gateway-about-vpn-devices.md)。
2. 連結 hello Azure toohello 本機閘道上的站對站 VPN 閘道。
   
    在此範例中，connectedEntityId 是 hello 本機閘道識別碼，您可以執行尋找`Get-AzureLocalNetworkGateway`。 您可以使用 hello 找到 virtualNetworkGatewayId `Get-AzureVirtualNetworkGateway` cmdlet。 這個步驟之後，hello 您區域網路與 Azure 之間 hello 站對站 VPN 連線透過連接。

        New-AzureVirtualNetworkGatewayConnection -connectedEntityId <local-network-gateway-id> -gatewayConnectionName Azure2Local -gatewayConnectionType IPsec -sharedKey abc123 -virtualNetworkGatewayId <azure-s2s-vpn-gateway-id>

## <a name="add"></a>現有的 VNet 的 tooconfigure coexsiting 連線
如果您有現有的虛擬網路，請檢查 hello 閘道子網路大小。 如果 hello 閘道子網路是/28 或 29，您必須先刪除 hello 虛擬網路閘道並增加 hello 閘道子網路大小。 hello 本節中的步驟將示範如何 toodo 的。

Hello 閘道子網路是否 /27 或更大而且透過 ExpressRoute 連接 hello 虛擬網路，您可以略過下列步驟 hello 而太[[步驟 6-建立站對站 VPN 閘道]](#vpngw) hello 前一節中。

> [!NOTE]
> 當您刪除 hello 現有閘道時，您本機內部部署將會遺失 hello 連接 tooyour 虛擬網路，當您使用此設定。
> 
> 

1. 您將需要 tooinstall hello 最新版本的 hello Azure 資源管理員 PowerShell cmdlet。 請參閱[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)如需安裝 hello PowerShell cmdlet 的詳細資訊。 請注意 hello cmdlet，您將使用此組態可能會與您可能的熟悉稍有不同。 確定 toouse hello cmdlet 這些指示中指定。 
2. 刪除 hello 現有 ExpressRoute 或站對站 VPN 閘道。 使用下列 cmdlet，取代您自己 hello 值 hello。
   
        Remove-AzureVNetGateway –VnetName MyAzureVNET
3. 匯出 hello 虛擬網路的結構描述。 使用下列 PowerShell cmdlet，取代您自己 hello 值 hello。
   
        Get-AzureVNetConfig –ExportToFile “C:\NetworkConfig.xml”
4. 編輯 hello 網路組態檔結構描述，以便 hello 閘道子網路是 /27 或短的前置詞 （例如 /26 或 /25）。 請參閱下列範例中的 hello。 
   
   > [!NOTE]
   > 如果您沒有足夠的 IP 位址保留在您虛擬網路 tooincrease hello 閘道子網路大小，您需要 tooadd 多個 IP 位址空間。 如需 hello 組態結構描述的詳細資訊，請參閱[Azure 虛擬網路組態結構描述](https://msdn.microsoft.com/library/azure/jj157100.aspx)。
   > 
   > 
   
          <Subnet name="GatewaySubnet">
            <AddressPrefix>10.17.159.224/27</AddressPrefix>
          </Subnet>
5. 如果您先前的閘道站對站 VPN，您也必須變更 hello 連線類型太**專用**。
   
                 <Gateway>
                  <ConnectionsToLocalNetwork>
                    <LocalNetworkSiteRef name="MyLocalNetwork">
                      <Connection type="Dedicated" />
                    </LocalNetworkSiteRef>
                  </ConnectionsToLocalNetwork>
                </Gateway>
6. 此時，您必須使用沒有閘道器的 VNet。 toocreate 新的閘道完成您的連線，您可以繼續使用[步驟 4-建立 ExpressRoute 閘道](#gw)、 在 hello 前面的步驟中找到。

## <a name="next-steps"></a>後續步驟
如需 ExpressRoute 的詳細資訊，請參閱 hello [ExpressRoute 常見問題集](expressroute-faqs.md)

