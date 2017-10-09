---
title: "連接傳統虛擬網路 tooAzure 資源管理員 Vnet： 入口網站 |Microsoft 文件"
description: "深入了解如何 toocreate 傳統 Vnet 和 VPN 閘道與 hello 入口網站所使用的資源管理員 Vnet 之間的 VPN 連線"
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: 5a90498c-4520-4bd3-a833-ad85924ecaf9
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/21/2017
ms.author: cherylmc
ms.openlocfilehash: bef63b4e829335b2e1a9434a35ebfe33b4fd7373
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="connect-virtual-networks-from-different-deployment-models-using-hello-portal"></a>若要從不同的部署模型使用 hello 入口網站連接虛擬網路

本文章將示範如何 tooconnect 傳統 Vnet tooResource 管理員 Vnet tooallow hello 位於彼此的 hello 不同的部署模型 toocommunicate 中的資源。 這篇文章中的 hello 步驟主要使用 hello Azure 入口網站，但您也可以建立使用 hello PowerShell hello 文章從此清單中選取此設定。

> [!div class="op_single_selector"]
> * [入口網站](vpn-gateway-connect-different-deployment-models-portal.md)
> * [PowerShell](vpn-gateway-connect-different-deployment-models-powershell.md)
> 
> 

連接傳統的 VNet tooa 資源管理員 VNet 是類似 tooconnecting VNet tooan 在內部部署站台位置。 這兩種連線類型使用的 VPN 閘道 tooprovide 採用 IPsec/IKE 的安全通道。 您可以在不同訂用帳戶和不同區域中的 VNet 之間建立連線。 只要 hello 閘道設定使用動態或路由為基礎，您也可以連接到已連線 tooon 內部部署網路的 Vnet。 如需 VNet 對 VNet 連線的詳細資訊，請參閱 hello [VNet 對 VNet 常見問題集](#faq)hello 本文結尾處。 

如果您的 Vnet 中 hello 相同區域中，您可能會想 tooinstead 考慮它們使用對等互連的 VNet 連接。 VNet 對等互連不會使用 VPN 閘道。 如需詳細資訊，請參閱 [VNet 對等互連](../virtual-network/virtual-network-peering-overview.md)。 

### <a name="prerequisites"></a>必要條件

* 這些步驟假設已建立兩個 VNet。 如果您使用這份文件做為練習，而且不需要 Vnet，有連結 hello 步驟 toohelp 在您建立它們。
* 請確認個 Vnet 不會彼此重疊的 hello hello 位址範圍，或其他連線閘道可能連接到該 hello 與任何 hello 的重疊範圍。
* 安裝資源管理員和服務管理 （傳統） 的 hello 最新版的 PowerShell cmdlet。 在本文中，我們將使用 hello Azure 入口網站和 PowerShell。 PowerShell 是必要的 toocreate hello 連線從傳統 VNet toohello hello 資源管理員 VNet。 如需詳細資訊，請參閱[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)。 

### <a name="values"></a>設定範例

您可以使用這些值 toocreate 測試環境中，或參閱 toothem toobetter 了解這篇文章中的 hello 範例。

**傳統 VNet**

VNet 名稱 = ClassicVNet  <br>
位址空間 = 10.0.0.0/24 <br>
子網路 1 = 10.0.0.0/27 <br>
資源群組 = ClassicRG <br>
位置 = West US <br>
GatewaySubnet = 10.0.0.32/28 <br>
本機站台 = RMVNetLocal <br>

**Resource Manager VNet**

VNet 名稱 = RMVNet  <br>
位址空間 = 192.168.0.0/16 <br>
子網路 1 = 192.168.1.0/24 <br>
GatewaySubnet = 192.168.0.0/26 <br>
資源群組 = RG1 <br>
位置 = 美國東部 <br>
虛擬網路閘道名稱 = RMGateway <br>
閘道類型 = VPN <br>
VPN 類型 = 路由式 <br>
閘道公用 IP 位址名稱 = rmgwpip <br>
區域網路閘道 = ClassicVNetLocal <br>
連線名稱 = RMtoClassic

### <a name="connection-overview"></a>連線概觀

此組態中，您建立 VPN 閘道連線透過 hello 虛擬網路之間的 IPsec/IKE VPN 通道。 請確定沒有任何 VNet 範圍重疊彼此，或與任何 hello 所連接的區域網路。

hello 下表顯示 hello 範例 Vnet 和本機站台所定義之範例：

| 虛擬網路 | 位址空間 | 區域 | Toolocal 網路站台連線 |
|:--- |:--- |:--- |:--- |
| ClassicVNet |(10.0.0.0/24) |美國西部 | RMVNetLocal (192.168.0.0/16) |
| RMVNet | (192.168.0.0/16) |美國東部 |ClassicVNetLocal (10.0.0.0/24) |

## <a name="classicvnet"></a>1.設定 hello 傳統的 VNet 設定

在本節中，您會建立 hello 區域網路 （本機站台） 和傳統 VNet 的 hello 虛擬網路閘道。 如果您不需要傳統的 VNet，且正在執行這些步驟，做為練習，您可以使用來建立 VNet[本文](../virtual-network/virtual-networks-create-vnet-classic-pportal.md)和 hello[範例](#values)上述的設定值。

當使用 hello 入口 toocreate 傳統的虛擬網路時，您必須使用下列步驟，否則 hello 選項 toocreate 傳統的虛擬網路不會出現的 hello 來巡覽 toohello 虛擬網路 刀鋒視窗：

1. 按一下 hello '+' tooopen hello 'New' 刀鋒視窗。
2. Hello '搜尋 hello marketplace' 欄位中，輸入 [虛擬網路]。 如果相反地，選取 網路功能-> 虛擬網路，則不會收到 hello 選項 toocreate 傳統的 VNet。
3. 傳回清單中的 hello 從找出 虛擬網路，然後按一下 tooopen hello 虛擬網路 刀鋒視窗。 
4. Hello 虛擬網路] 刀鋒視窗中，選取 [傳統' toocreate 傳統的 VNet。 

如果您已經有 VPN 閘道的 VNet，請確認該 hello 閘道，而是動態。 如果是靜態，您必須先刪除 hello VPN 閘道，然後繼續進行。

已提供螢幕擷取畫面做為範例。 是確定 tooreplace hello 值，以您自己，或使用 hello[範例](#values)值。

### <a name="part-1---configure-hello-local-site"></a>第 1 部-設定 hello 本機站台

開啟 hello [Azure 入口網站](https://ms.portal.azure.com)並以您的 Azure 帳戶登入。

1. 瀏覽過**所有資源**並找出 hello **ClassicVNet** hello 清單中。
2. 在 hello**概觀**刀鋒視窗中的，在 hello **VPN 連線**區段中，按一下 hello**閘道**圖形 toocreate 閘道。

    ![設定 VPN 閘道](./media/vpn-gateway-connect-different-deployment-models-portal/gatewaygraphic.png "設定 VPN 閘道")
3. 在 hello**新的 VPN 連線**刀鋒視窗中，針對**連線類型**，選取**站對站**。
4. 針對 [本機站台]，按一下 [設定必要設定]。 這會開啟 hello**本機站台**刀鋒視窗。
5. 在 hello**本機站台**刀鋒視窗中，建立名稱 toorefer toohello 資源管理員的 VNet。 例如，'RMVNetLocal'。
6. 如果 hello 資源管理員 VNet 的 hello VPN 閘道已經有公用 IP 位址，則將 hello 值用於 hello **VPN 閘道 IP 位址**欄位。 如果您要執行這些步驟作為練習，或者您的 Resource Manager VNet 還沒有虛擬網路閘道，您可以自行設定預留位置 IP 位址。 請確定 hello 預留位置 IP 位址使用有效的格式。 更新版本中，您可以取代 hello 預留位置 IP 位址以 hello hello 資源管理員虛擬網路閘道的公用 IP 位址。
7. 如**用戶端的位址空間**，hello 值用於 hello hello 資源管理員 VNet 的虛擬網路 IP 位址空間。 這項設定是使用的 toospecify hello 位址空間 tooroute toohello 資源管理員虛擬網路。
8. 按一下**確定**toosave hello 值，並傳回 toohello**新的 VPN 連線**刀鋒視窗。

### <a name="part-2---create-hello-virtual-network-gateway"></a>第 2 部-建立 hello 虛擬網路閘道

1. 在 hello**新的 VPN 連線**刀鋒視窗中，選取 hello**立即建立閘道**核取方塊，按一下 **選擇性閘道組態**tooopen hello **閘道組態**刀鋒視窗。 

    ![開啟 [閘道組態] 刀鋒視窗](./media/vpn-gateway-connect-different-deployment-models-portal/optionalgatewayconfiguration.png "開啟 [閘道組態] 刀鋒視窗")
2. 按一下**子網路-設定必要的設定**tooopen hello**加入子網路**刀鋒視窗。 hello**名稱**已經設定使用所需的 hello 值**GatewaySubnet**。
3. hello**位址範圍**hello 閘道子網路的參考 toohello 範圍。 雖然您可以使用 /29 位址範圍 (3 個位址) 建立閘道子網路，但是我們建議您建立包含更多 IP 位址的閘道子網路。 這可以容納未來可能需要更多可用 IP 位址的組態。 可能的話，請使用 /27 或 /28。 如果您使用下列步驟做為練習，您可以參考 toohello[範例](#values)值。 按一下**確定**toocreate hello 閘道子網路。
4. 在 hello**閘道組態**刀鋒視窗中，**大小**參考 toohello 閘道 SKU。 選取您的 VPN 閘道的 hello 閘道 SKU。
5. 確認 hello**路由類型**是**動態**，然後按一下**確定**tooreturn toohello**新的 VPN 連線**刀鋒視窗。
6. 在 hello**新的 VPN 連線**刀鋒視窗中，按一下  **確定** toobegin 建立 VPN 閘道。 建立 VPN 閘道，可能會佔用 too45 分鐘 toocomplete。

### <a name="ip"></a>第 3-部分複製 hello 虛擬網路閘道的公用 IP 位址

建立 hello 虛擬網路閘道之後，您可以檢視 hello 閘道 IP 位址。 

1. 瀏覽 tooyour 傳統的 VNet，然後按一下**概觀**。
2. 按一下**VPN 連線**tooopen hello VPN 連線刀鋒視窗。 在 hello VPN 連線刀鋒視窗中，您可以檢視 hello 公用 IP 位址。 這是 hello 分派 tooyour 虛擬網路閘道的公用 IP 位址。 
3. 請記下或複製 hello IP 位址。 當您在稍後的步驟中處理 Resource Manager 區域網路閘道組態設定時，便會用到該 IP 位址。 您也可以檢視您的閘道連線的 hello 狀態。 請注意您所建立的 hello 區域網路網站會列為 '連接到'。 您已建立您的連線之後，hello 狀態會變更。
4. 複製 hello 閘道 IP 位址之後關閉 hello 刀鋒視窗。

## <a name="rmvnet"></a>2.設定 hello 資源管理員的 VNet 設定

本節中，您為資源管理員 VNet 建立 hello 虛擬網路閘道與 hello 區域網路閘道。 如果您沒有資源管理員 VNet，且正在執行下列步驟，做為練習，您可以使用來建立 VNet[本文](../virtual-network/virtual-networks-create-vnet-arm-pportal.md)和 hello[範例](#values)上述的設定值。

已提供螢幕擷取畫面做為範例。 是確定 tooreplace hello 值，以您自己，或使用 hello[範例](#values)值。

### <a name="part-1---create-a-gateway-subnet"></a>第 1 部份 - 建立閘道子網路

才可建立虛擬網路閘道，您必須先 toocreate hello 閘道子網路。 以 /28 或更高的 CIDR 計數建立閘道子網路。 (/27、/26 等)

[!INCLUDE [vpn-gateway-no-nsg-include](../../includes/vpn-gateway-no-nsg-include.md)]

[!INCLUDE [vpn-gateway-add-gwsubnet-rm-portal](../../includes/vpn-gateway-add-gwsubnet-rm-portal-include.md)]

### <a name="part-2---create-a-virtual-network-gateway"></a>第 2 部份 - 建立虛擬網路閘道

[!INCLUDE [vpn-gateway-add-gw-rm-portal](../../includes/vpn-gateway-add-gw-rm-portal-include.md)]

### <a name="createlng"></a>第 3 部份 - 建立區域網路閘道

hello 區域網路閘道指定 hello 位址範圍，與傳統 VNet 和其虛擬網路閘道相關聯的 hello 公用 IP 位址。

如果您執行下列步驟做為練習，請參閱 toothese 設定：

| 虛擬網路 | 位址空間 | 區域 | Toolocal 網路站台連線 |閘道公用 IP 位址|
|:--- |:--- |:--- |:--- |:--- |
| ClassicVNet |(10.0.0.0/24) |美國西部 | RMVNetLocal (192.168.0.0/16) |hello 分派 toohello ClassicVNet 閘道的公用 IP 位址|
| RMVNet | (192.168.0.0/16) |美國東部 |ClassicVNetLocal (10.0.0.0/24) |hello 分派 toohello RMVNet 閘道的公用 IP 位址。|

[!INCLUDE [vpn-gateway-add-lng-rm-portal](../../includes/vpn-gateway-add-lng-rm-portal-include.md)]

## <a name="modifylng"></a>3.修改 hello 傳統 VNet 本機站台設定

在本節中，您會取代 hello 本機站台設定值，指定以 hello 資源管理員 VPN 閘道 IP 位址時所使用的 hello 預留位置 IP 位址。 本節使用 hello 傳統 (SM) PowerShell cmdlet。

1. 在 hello Azure 入口網站，瀏覽 toohello 傳統虛擬網路。
2. 在您的虛擬網路的 hello 刀鋒視窗，按一下 **概觀**。
3. 在 hello **VPN 連線**區段中，按一下 hello hello 圖形中本機網站名稱。

    ![VPN-connections](./media/vpn-gateway-connect-different-deployment-models-portal/vpnconnections.png "VPN 連線")
4. 在 hello**站對站 VPN 連線**刀鋒視窗中，按一下 hello hello 站台名稱。

    ![Site-name](./media/vpn-gateway-connect-different-deployment-models-portal/sitetosite3.png "本機站台名稱")
5. 在 hello 連接刀鋒視窗中為您本機的網站，按一下 hello 本機站台 tooopen hello hello 名稱**本機站台**刀鋒視窗。

    ![Open-local-site](./media/vpn-gateway-connect-different-deployment-models-portal/openlocal.png "開啟本機站台")
6. 在 hello**本機站台**刀鋒視窗中，取代 hello **VPN 閘道 IP 位址**hello hello 資源管理員閘道 IP 位址。

    ![Gateway-ip-address](./media/vpn-gateway-connect-different-deployment-models-portal/gwipaddress.png "閘道 IP 位址")
7. 按一下**確定**tooupdate hello IP 位址。

## <a name="RMtoclassic"></a>4.建立資源管理員 tooclassic 連線

在這些步驟中，您可以設定 hello 資源管理員 VNet 中的 hello 連接 toohello 傳統的 VNet 使用 hello Azure 入口網站。

1. 在**所有資源**，找出 hello 區域網路閘道。 在本例中，為 hello 區域網路閘道**ClassicVNetLocal**。
2. 按一下**組態**並確認 hello IP 位址的值為 hello 的 hello VPN 閘道傳統的 VNet。 視需要更新，然後按一下 [儲存]。 關閉 hello 刀鋒視窗。
3. 在**所有資源**，按一下 hello 區域網路閘道。
4. 按一下**連線**tooopen hello 連線刀鋒視窗。
5. 在 hello**連線**刀鋒視窗中，按一下   **+**  tooadd 連接。
6. 在 hello**加入連接**刀鋒視窗中，名稱 hello 連線。 例如，'RMtoClassic'。
7. 已在此刀鋒視窗中選取 [站對站]。
8. 選取您想要與此站台 tooassociate hello 虛擬網路閘道。
9. 建立**共用金鑰**。 從傳統 VNet toohello hello 資源管理員 VNet 建立 hello 連接中也使用此金鑰。 您可以產生 hello 金鑰，或建立一個。 在我們的範例中，我們使用的是 'abc123'，但是您可以(且應該) 使用更為複雜的值。
10. 按一下**確定**toocreate hello 連線。

##<a name="classictoRM"></a>5.建立傳統 tooResource Manager 連線

在這些步驟中，您可以設定傳統 VNet toohello hello 資源管理員 VNet 中的 hello 連接。 這些步驟需要 PowerShell。 您無法在 hello 入口網站中建立此連線。 請確定您已下載並安裝 hello 傳統 (SM) 和資源管理員 (RM) PowerShell cmdlet。

### <a name="1-connect-tooyour-azure-account"></a>1.連接 tooyour Azure 帳戶

使用提高的權限開啟 hello PowerShell 主控台，並登入 tooyour Azure 帳戶。 hello 下列 cmdlet 會提示您輸入 hello 登入認證您的 Azure 帳戶。 登入之後，使其可用 tooAzure PowerShell，會下載您的帳戶設定。

```powershell
Login-AzureRmAccount
```
   
如果您有多個訂用帳戶，請取得 Azure 訂用帳戶的清單。

```powershell
Get-AzureRmSubscription
```

指定您想 toouse hello 訂用帳戶。 

```powershell
Select-AzureRmSubscription -SubscriptionName "Name of subscription"
```

加入您 Azure 帳戶 toouse hello 傳統 PowerShell cmdlet (SM)。 toodo 因此，您可以使用下列命令的 hello:

```powershell
Add-AzureAccount
```

### <a name="2-view-hello-network-configuration-file-values"></a>2.檢視 hello 網路組態檔值

當您建立 VNet hello Azure 入口網站中時，不在 hello Azure 入口網站中顯示 hello Azure 會使用的完整名稱。 比方說，VNet 出現 toobe hello Azure 入口網站中名為 'ClassicVNet' 可能 hello 網路組態檔中有多長的名稱。 hello 名稱可能看起來像這樣: ' 群組 ClassicRG ClassicVNet'。 在這些步驟中，您可以下載 hello 網路組態檔和檢視 hello 值。

您的電腦上建立目錄，然後匯出 hello 網路組態檔 toohello 目錄。 在此範例中，hello 網路組態檔會是匯出的 tooC:\AzureNet。

```powershell
Get-AzureVNetConfig -ExportToFile C:\AzureNet\NetworkConfig.xml
```

使用傳統 VNet 的文字編輯器和檢視 hello 名稱開啟 hello 檔案。 執行 PowerShell cmdlet 時，請使用 hello 網路組態檔中的 hello 名稱。

- VNet 名稱會列為 **VirtualNetworkSite name =**
- 網站名稱會列為 **LocalNetworkSite name=**

### <a name="3-create-hello-connection"></a>3.建立 hello 連線

設定 hello 共用的金鑰，並從傳統 VNet toohello hello 資源管理員 VNet 建立 hello 連接。 您無法設定 hello 使用 hello 入口網站的共用的金鑰。 請確定您執行這些步驟時使用精簡 hello PowerShell cmdlet hello 登入。 因此，使用 toodo **Add-azureaccount**。 否則，就能 tooset hello '-AzureVNetGatewayKey'。

- 在此範例中， **-VNetName** hello 名稱做為傳統 VNet 找到您的網路組態檔中的 hello。 
- hello **-LocalNetworkSiteName** hello 本機站台上，指定為 hello 名稱位於您的網路組態檔。
- hello **-SharedKey**是產生及指定的值。 針對此範例，我們使用的是 *abc123*，但是您可以使用更為複雜的值。 hello 重要件事就是您在此處指定的 hello 該值必須是相同的值，指定建立資源管理員 tooclassic 連接時的 hello。

```powershell
Set-AzureVNetGatewayKey -VNetName "Group ClassicRG ClassicVNet" `
-LocalNetworkSiteName "172B9E16_RMVNetLocal" -SharedKey abc123
```

##<a name="verify"></a>6.確認您的連線

您可以確認您使用的連線 hello Azure 入口網站或 PowerShell。 當驗證，您可能需要 toowait 一兩分鐘 hello 連接所建立。 當連接成功時，hello 連線狀態變更從 '連接到' too'Connected'。

### <a name="tooverify-hello-connection-from-your-classic-vnet-tooyour-resource-manager-vnet"></a>從傳統 VNet tooyour 資源管理員 VNet tooverify hello 連線

[!INCLUDE [vpn-gateway-verify-connection-azureportal-classic](../../includes/vpn-gateway-verify-connection-azureportal-classic-include.md)]

###<a name="tooverify-hello-connection-from-your-resource-manager-vnet-tooyour-classic-vnet"></a>從資源管理員 VNet tooyour tooverify hello 連接傳統的 VNet

[!INCLUDE [vpn-gateway-verify-connection-portal-rm](../../includes/vpn-gateway-verify-connection-portal-rm-include.md)]

## <a name="faq"></a>VNet 對 VNet 常見問題集

[!INCLUDE [vpn-gateway-vnet-vnet-faq](../../includes/vpn-gateway-vnet-vnet-faq-include.md)]
