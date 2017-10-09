---
title: "連接虛擬網路 toomultiple 的站台，使用 VPN 閘道和 PowerShell： 傳統 |Microsoft 文件"
description: "本文將引導您完成連接多個本機內部部署站台 tooa 虛擬網路 VPN 閘道用於 hello 傳統部署模型。"
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: 
tags: azure-service-management
ms.assetid: b043df6e-f1e8-4a4d-8467-c06079e2c093
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/20/2017
ms.author: yushwang
ms.openlocfilehash: 5404b1c55ed3453b4dbc94dfd93e47c0812025f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-site-to-site-connection-tooa-vnet-with-an-existing-vpn-gateway-connection-classic"></a>新增站對站連線 tooa VNet 與現有的 VPN 閘道連線 （傳統）

[!INCLUDE [deployment models](../../includes/vpn-gateway-classic-deployment-model-include.md)]

> [!div class="op_single_selector"]
> * [Azure 入口網站](vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md)
> * [PowerShell (傳統)](vpn-gateway-multi-site.md)
>
>

這篇文章會引導您使用 PowerShell tooadd 站台對站 (S2S) 連線 tooa VPN 閘道具有現有連線。 這種類型通常是連接的參照的 tooas"多站台 」 設定。 hello 本文章中的步驟適用於使用 hello 傳統部署模型 （也稱為服務管理） 建立 toovirtual 網路。 這些步驟不會套用 tooExpressRoute /-網站共存連接組態。

### <a name="deployment-models-and-methods"></a>部署模型和方法

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

當此組態有新文章和額外工具可以使用時，我們就會更新此資料表。 發行項可用時，我們直接連結 tooit 這個資料表中。

[!INCLUDE [vpn-gateway-table-multi-site](../../includes/vpn-gateway-table-multisite-include.md)]

## <a name="about-connecting"></a>關於連線

您可以連接多個內部部署站台 tooa 單一虛擬網路。 這對建立混合式雲端解決方案特別具有吸引力。 建立多網站連線 tooyour Azure 虛擬網路閘道是類似 toocreating 其他站台對站連線。 事實上，您可以使用現有的 Azure VPN 閘道，只要是動態的 hello 閘道 （路由式）。

如果您已經有靜態閘道連接的 tooyour 虛擬網路，您可以變更 hello 閘道類型 toodynamic 無須 toorebuild hello 虛擬網路中的順序 tooaccommodate 多站台。 在變更之前 hello 路由類型，請確定您在內部部署 VPN 閘道支援路由式 VPN 組態。

![多重網站圖表](./media/vpn-gateway-multi-site/multisite.png "多重網站")

## <a name="points-tooconsider"></a>點 tooconsider

**您必須能夠 toouse hello 入口 toomake 變更 toothis 虛擬網路。** 您需要 toomake 變更 toohello 網路組態檔而不是使用 hello 入口網站。 如果您在 hello 入口網站中進行變更，他們將會覆寫您對此虛擬網路的多網站參考設定。

您應該可以放心使用 hello 時間 hello 網路組態檔完成 hello 多網站程序。 不過，如果您有多人使用您的網路設定，您必須先 toomake 確定每個人都知悉這項限制。 這並不表示您無法完全使用 hello 入口網站。 您可以使用它的一切，除了進行組態變更 toothis 特定虛擬網路。

## <a name="before-you-begin"></a>開始之前

開始設定之前，請確認您擁有 hello 下列：

* 每個內部部署位置都有相容的 VPN 硬體。 請檢查[關於 VPN 裝置的虛擬網路連線](vpn-gateway-about-vpn-devices.md)tooverify 如果您想 toouse hello 裝置已知 toobe 相容。
* 每個 VPN 裝置都有對外的公用 IPv4 IP 位址。 hello IP 位址不得位於 NAT 後方。 這是必要條件。
* 您將需要 tooinstall hello 最新版本的 hello Azure PowerShell cmdlet。 請確定您安裝 hello 服務管理 (SM) 版本中加入 toohello 資源管理員版本。 請參閱[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)如需詳細資訊。
* 熟悉如何設定 VPN 硬體的人員。 您將了解 toohave 強式如何 tooconfigure 您的 VPN 裝置或沒有人使用。
* hello （如果您尚未建立一個） toouse 想在虛擬網路 IP 位址範圍。
* hello IP 位址範圍的每個您將要連接到的 hello 區域網路網站。 您將需要 toomake 確定 hello IP 位址範圍的每個您想 tooconnect toodo 不重疊的 hello 區域網路網站。 否則，hello 入口網站或 hello REST API 將會拒絕上傳的 hello 組態。<br>例如，如果您有兩個區域網路網站都包含 hello IP 位址範圍 10.2.3.0/24，您必須具有目的地位址 10.2.3.3 的套件，Azure 可能不知道要 toosend hello 封裝 toobecause hello 位址範圍是哪一個站的台重疊。 tooprevent 路由問題，Azure 不允許您 tooupload 具有重疊範圍的組態檔。

## <a name="1-create-a-site-to-site-vpn"></a>1.建立站對站 VPN
如已有動態路由閘道的站對站 VPN，太棒了！ 您可以繼續在太[hello 虛擬網路組態設定匯出](#export)。 如果沒有，請不要 hello 遵循：

### <a name="if-you-already-have-a-site-to-site-virtual-network-but-it-has-a-static-policy-based-routing-gateway"></a>如果您已經有站對站虛擬網路，但其有靜態 (原則式) 路由閘道：
1. 變更您閘道類型 toodynamic 路由。 多網站 VPN 需要動態 (亦稱作路由式) 路由閘道。 toochange 您的閘道類型，您將需要 toofirst 刪除 hello 現有閘道，然後建立一個新。 如需指示，請參閱[toochange 如何 hello VPN 閘道的路由類型](vpn-gateway-configure-vpn-gateway-mp.md)。  
2. 設定新的閘道，並建立 VPN 通道。 如需指示，請參閱[hello Azure 傳統入口網站中設定 VPN 閘道](vpn-gateway-configure-vpn-gateway-mp.md)。 首先，變更您閘道類型 toodynamic 路由。

### <a name="if-you-dont-have-a-site-to-site-virtual-network"></a>如果您沒有站對站虛擬網路：
1. 建立站對站虛擬網路使用下列指示： [hello Azure 傳統入口網站中的站對站 VPN 連線建立虛擬網路](vpn-gateway-site-to-site-create.md)。  
2. 使用下列指示設定動態路由閘道： [設定 VPN 閘道](vpn-gateway-configure-vpn-gateway-mp.md)。 要確定 tooselect**動態路由**適用於您的閘道類型。

## <a name="export"></a>2.匯出 hello 網路組態檔
藉由執行下列命令的 hello 匯出您的 Azure 網路組態檔。 您可以變更 hello hello 檔 tooexport tooa 不同位置的必要的位置。

```powershell
Get-AzureVNetConfig -ExportToFile C:\AzureNet\NetworkConfig.xml
```

## <a name="3-open-hello-network-configuration-file"></a>3.開啟 hello 網路組態檔
Hello 最後一個步驟中，開啟您所下載的 hello 網路組態檔。 使用您喜歡的任何 xml 編輯器。 hello 檔案應該看起來類似 toohello 下列：

        <NetworkConfiguration xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/ServiceHosting/2011/07/NetworkConfiguration">
          <VirtualNetworkConfiguration>
            <LocalNetworkSites>
              <LocalNetworkSite name="Site1">
                <AddressSpace>
                  <AddressPrefix>10.0.0.0/16</AddressPrefix>
                  <AddressPrefix>10.1.0.0/16</AddressPrefix>
                </AddressSpace>
                <VPNGatewayAddress>131.2.3.4</VPNGatewayAddress>
              </LocalNetworkSite>
              <LocalNetworkSite name="Site2">
                <AddressSpace>
                  <AddressPrefix>10.2.0.0/16</AddressPrefix>
                  <AddressPrefix>10.3.0.0/16</AddressPrefix>
                </AddressSpace>
                <VPNGatewayAddress>131.4.5.6</VPNGatewayAddress>
              </LocalNetworkSite>
            </LocalNetworkSites>
            <VirtualNetworkSites>
              <VirtualNetworkSite name="VNet1" AffinityGroup="USWest">
                <AddressSpace>
                  <AddressPrefix>10.20.0.0/16</AddressPrefix>
                  <AddressPrefix>10.21.0.0/16</AddressPrefix>
                </AddressSpace>
                <Subnets>
                  <Subnet name="FE">
                    <AddressPrefix>10.20.0.0/24</AddressPrefix>
                  </Subnet>
                  <Subnet name="BE">
                    <AddressPrefix>10.20.1.0/24</AddressPrefix>
                  </Subnet>
                  <Subnet name="GatewaySubnet">
                    <AddressPrefix>10.20.2.0/29</AddressPrefix>
                  </Subnet>
                </Subnets>
                <Gateway>
                  <ConnectionsToLocalNetwork>
                    <LocalNetworkSiteRef name="Site1">
                      <Connection type="IPsec" />
                    </LocalNetworkSiteRef>
                  </ConnectionsToLocalNetwork>
                </Gateway>
              </VirtualNetworkSite>
            </VirtualNetworkSites>
          </VirtualNetworkConfiguration>
        </NetworkConfiguration>

## <a name="4-add-multiple-site-references"></a>4.新增多個網站參考
當您新增或移除網站參考資訊時，您要進行組態變更 toohello ConnectionsToLocalNetwork/LocalNetworkSiteRef。 Azure toocreate 加入新的本機網站參考會觸發新的通道。 Hello 下列範例中，在 hello 網路組態僅適用於單一站台連線。 一旦您完成變更後，請儲存 hello 檔案。

```
  <Gateway>
    <ConnectionsToLocalNetwork>
      <LocalNetworkSiteRef name="Site1"><Connection type="IPsec" /></LocalNetworkSiteRef>
    </ConnectionsToLocalNetwork>
  </Gateway>
```

tooadd 其他網站參考資料 （建立多網站組態），只要加入其他"LocalNetworkSiteRef"字行，如以下 hello 範例所示：

```
  <Gateway>
    <ConnectionsToLocalNetwork>
      <LocalNetworkSiteRef name="Site1"><Connection type="IPsec" /></LocalNetworkSiteRef>
      <LocalNetworkSiteRef name="Site2"><Connection type="IPsec" /></LocalNetworkSiteRef>
    </ConnectionsToLocalNetwork>
  </Gateway>
```

## <a name="5-import-hello-network-configuration-file"></a>5.匯入 hello 網路組態檔
匯入 hello 網路組態檔。 當您匯入具有 hello 變更這個檔案時，將會加入 hello 新通道。 hello 通道會使用您稍早建立的 hello 動態閘道。 您可以使用 hello 傳統入口網站或 PowerShell tooimport hello 檔案。

## <a name="6-download-keys"></a>6.下載金鑰
一旦新的通道新增之後，使用每個通道 hello PowerShell cmdlet ' Get AzureVNetGatewayKey' tooget hello IPsec/IKE 預先共用的金鑰。

例如：

```powershell
Get-AzureVNetGatewayKey –VNetName "VNet1" –LocalNetworkSiteName "Site1"
Get-AzureVNetGatewayKey –VNetName "VNet1" –LocalNetworkSiteName "Site2"
```

如果您想要的話，您也可以使用 hello*取得虛擬網路閘道共用金鑰*REST API tooget hello 預先共用的金鑰。

## <a name="7-verify-your-connections"></a>7.確認您的連線
檢查 hello 多網站通道狀態。 下載每個通道的 hello 金鑰之後, 您會想 tooverify 連線。 請使用 ' Get AzureVnetConnection' tooget 通道連接的虛擬網路清單，hello 下面範例所示。 VNet1 是 hello VNet hello 名稱。

```powershell
Get-AzureVnetConnection -VNetName VNET1
```

範例傳回：

```
    ConnectivityState         : Connected
    EgressBytesTransferred    : 661530
    IngressBytesTransferred   : 519207
    LastConnectionEstablished : 5/2/2014 2:51:40 PM
    LastEventID               : 23401
    LastEventMessage          : hello connectivity state for hello local network site 'Site1' changed from Not Connected tooConnected.
    LastEventTimeStamp        : 5/2/2014 2:51:40 PM
    LocalNetworkSiteName      : Site1
    OperationDescription      : Get-AzureVNetConnection
    OperationId               : 7f68a8e6-51e9-9db4-88c2-16b8067fed7f
    OperationStatus           : Succeeded

    ConnectivityState         : Connected
    EgressBytesTransferred    : 789398
    IngressBytesTransferred   : 143908
    LastConnectionEstablished : 5/2/2014 3:20:40 PM
    LastEventID               : 23401
    LastEventMessage          : hello connectivity state for hello local network site 'Site2' changed from Not Connected tooConnected.
    LastEventTimeStamp        : 5/2/2014 2:51:40 PM
    LocalNetworkSiteName      : Site2
    OperationDescription      : Get-AzureVNetConnection
    OperationId               : 7893b329-51e9-9db4-88c2-16b8067fed7f
    OperationStatus           : Succeeded
```

## <a name="next-steps"></a>後續步驟

toolearn 深入了解 VPN 閘道，請參閱[有關 VPN 閘道](vpn-gateway-about-vpngateways.md)。
