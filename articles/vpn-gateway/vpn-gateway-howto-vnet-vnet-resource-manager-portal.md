---
title: "連接 Azure 虛擬網路 tooanother VNet： 入口網站 |Microsoft 文件"
description: "建立 Vnet 使用資源管理員之間的 VPN 閘道連線，並 hello Azure 入口網站。"
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: a7015cfc-764b-46a1-bfac-043d30a275df
ms.service: vpn-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/02/2017
ms.author: cherylmc
ms.openlocfilehash: a529f90d976bee0f50403947d06e9da8a6c05349
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-vnet-to-vnet-vpn-gateway-connection-using-hello-azure-portal"></a>設定 VNet 對 VNet VPN 閘道連線使用 hello Azure 入口網站

本文章將示範如何 toocreate 虛擬網路之間的 VPN 閘道連線。 hello 虛擬網路可在 hello 相同或不同區域，並從 hello 相同或不同的訂用帳戶。 當連接的 Vnet，從不同的訂用帳戶，hello 訂用帳戶不需要與相關聯的 toobe hello 相同的 Active Directory 租用戶。 

這篇文章中的 hello 步驟套用 toohello Resource Manager 部署模型，並使用 hello Azure 入口網站。 您也可以建立此組態使用不同的部署工具或部署模型，從下列清單中的 hello 選取不同的選項：

> [!div class="op_single_selector"]
> * [Azure 入口網站](vpn-gateway-howto-vnet-vnet-resource-manager-portal.md)
> * [PowerShell](vpn-gateway-vnet-vnet-rm-ps.md)
> * [Azure CLI](vpn-gateway-howto-vnet-vnet-cli.md)
> * [Azure 入口網站 (傳統)](vpn-gateway-howto-vnet-vnet-portal-classic.md)
> * [連線不同的部署模型 - Azure 入口網站](vpn-gateway-connect-different-deployment-models-portal.md)
> * [連線不同的部署模型 - PowerShell](vpn-gateway-connect-different-deployment-models-powershell.md)
>
>

![v2v 圖表](./media/vpn-gateway-howto-vnet-vnet-resource-manager-portal/v2vrmps.png)

連接虛擬網路 tooanother 虛擬網路 (VNet 對 VNet) 是類似 tooconnecting VNet tooan 在內部部署站台位置。 這兩種連線類型使用的 VPN 閘道 tooprovide 採用 IPsec/IKE 的安全通道。 如果您的 Vnet hello 中相同的區域，您可能會想 tooconsider 它們使用對等互連的 VNet 連接。 VNet 對等互連不會使用 VPN 閘道。 如需詳細資訊，請參閱 [VNet 對等互連](../virtual-network/virtual-network-peering-overview.md)。

您可以將 VNet 對 VNet 通訊與多站台組態結合。 這可讓您建立結合內部虛擬網路連線使用跨單位連線的網路拓樸 hello 下列圖表所示：

![關於連接](./media/vpn-gateway-howto-vnet-vnet-resource-manager-portal/aboutconnections.png "關於連接")

### <a name="why-connect-virtual-networks"></a>為什麼要連接虛擬網路？

您可以遵循原因 hello tooconnect 虛擬網路：

* **跨區域的異地備援和異地目前狀態**
  
  * 您可以使用安全連線設定自己的異地複寫或同步處理，而不用查看網際網路對向端點。
  * 您可以使用 Azure 流量管理員和負載平衡器，利用異地備援跨多個 Azure 區域設定高度可用的工作負載。 重要的一個例子是 tooset 設定 SQL Always On 與分配到多個 Azure 區域的可用性群組。
* **具有隔離或管理界限的區域性多層式應用程式**
  
  * 在 hello 相同區域中，您可以設定多層應用程式與多個虛擬網路連接在一起，因為 tooisolation 或系統管理需求。

如需 VNet 對 VNet 連線的詳細資訊，請參閱 hello [VNet 對 VNet 常見問題集](#faq)hello 本文結尾處。 請注意，是否您的 Vnet 不同訂用帳戶中，您無法建立 hello 連接 hello 入口網站中。 您可以使用 [PowerShell](vpn-gateway-vnet-vnet-rm-ps.md) 或 [CLI](vpn-gateway-howto-vnet-vnet-cli.md)。

### <a name="values"></a>設定範例

當使用這些步驟，做為練習，您可以使用 hello 範例設定值。 為了舉例說明，我們對每個 VNet 使用多個位址空間。 不過，VNet 對 VNet 組態不需要多個位址空間。

**TestVNet1 的值︰**

* VNet 名稱︰TestVNet1
* 位址空間︰10.11.0.0/16
  * 子網路名稱：FrontEnd
  * 子網路位址範圍：10.11.0.0/24
* 資源群組︰TestRG1
* 位置：美國東部
* 位址空間︰10.12.0.0/16
  * 子網路名稱：BackEnd
  * 子網路位址範圍︰10.12.0.0/24
* 閘道子網路名稱： GatewaySubnet （如此便會自動填滿 hello 入口網站中）
  * 閘道子網路位址範圍︰10.11.255.0/27
* DNS 伺服器： 使用您的 DNS 伺服器 hello IP 位址
* 虛擬網路閘道名稱︰TestVNet1GW
* 閘道類型：VPN
* VPN 類型：路由式
* SKU： 選取您想要 toouse 的閘道 SKU hello
* 公用 IP 位址名稱︰TestVNet1GWIP
* 連接值︰
  * 名稱︰TestVNet1toTestVNet4
  * 共用的金鑰： 您可以自行建立 hello 共用的金鑰。 此範例中，我們將使用 abc123。 hello 重點是，當您建立 hello hello Vnet 之間的連線，必須符合 hello 值。

**TestVNet4 的值︰**

* VNet 名稱︰TestVNet4
* 位址空間︰10.41.0.0/16
  * 子網路名稱：FrontEnd
  * 子網路位址範圍︰10.41.0.0/24
* 資源群組︰TestRG1
* 位置：美國西部
* 位址空間︰10.42.0.0/16
  * 子網路名稱：BackEnd
  * 子網路位址範圍︰10.42.0.0/24
* GatewaySubnet 名稱： GatewaySubnet （如此便會自動填滿 hello 入口網站中）
  * 閘道子網路位址範圍︰10.41.255.0/27
* DNS 伺服器： 使用您的 DNS 伺服器 hello IP 位址
* 虛擬網路閘道名稱︰TestVNet4GW
* 閘道類型：VPN
* VPN 類型：路由式
* SKU： 選取您想要 toouse 的閘道 SKU hello
* 公用 IP 位址名稱︰TestVNet4GWIP
* 連接值︰
  * 名稱︰TestVNet4toTestVNet1
  * 共用的金鑰： 您可以自行建立 hello 共用的金鑰。 此範例中，我們將使用 abc123。 hello 重點是，當您建立 hello hello Vnet 之間的連線，必須符合 hello 值。

## <a name="CreatVNet"></a>1.建立及設定 TestVNet1
如果您沒有 VNet，請確認 hello 設定與您的 VPN 閘道設計相容。 請特別注意 tooany 的子網路，可能會與其他網路重疊。 如果有重疊的子網路，您的連線便無法正常運作。 如果您的 VNet 設定的 hello 正確的設定，就可以開始在 hello hello 步驟[指定 DNS 伺服器](#dns)> 一節。

### <a name="toocreate-a-virtual-network"></a>toocreate 虛擬網路
[!INCLUDE [vpn-gateway-basic-vnet-rm-portal](../../includes/vpn-gateway-basic-vnet-rm-portal-include.md)]

## <a name="subnets"></a>2.新增其他位址空間和建立子網路
建立 VNet 之後，您可以新增其他位址空間和建立子網路。

[!INCLUDE [vpn-gateway-additional-address-space](../../includes/vpn-gateway-additional-address-space-include.md)]

## <a name="gatewaysubnet"></a>3.建立閘道子網路
連接您的虛擬網路 tooa 閘道之前，您首先需要 toocreate hello 閘道子網路要為 hello 虛擬網路 toowhich tooconnect。 可能的話，它是最佳 toocreate 閘道子網路中順序 tooprovide 使用 CIDR 區塊/28 或 /27 足夠的 IP 位址 tooaccommodate 額外設定需求。

如果您要建立此設定做為練習，請參閱 toothese[範例設定](#values)時建立您的閘道子網路。

[!INCLUDE [vpn-gateway-no-nsg](../../includes/vpn-gateway-no-nsg-include.md)]

### <a name="toocreate-a-gateway-subnet"></a>toocreate 閘道子網路
[!INCLUDE [vpn-gateway-add-gwsubnet-rm-portal](../../includes/vpn-gateway-add-gwsubnet-rm-portal-include.md)]

## <a name="dns"></a>4.指定 DNS 伺服器 (選擇性)
VNet 對 VNet 連線不需要 DNS。 不過，如果您想要部署的 tooyour 虛擬網路的資源 toohave 名稱解析，您應該指定 DNS 伺服器。 此設定可讓您指定 hello toouse 需為此虛擬網路的名稱解析的 DNS 伺服器。 它不會建立 DNS 伺服器。

[!INCLUDE [vpn-gateway-add-dns-rm-portal](../../includes/vpn-gateway-add-dns-rm-portal-include.md)]

## <a name="VNetGateway"></a>5.建立虛擬網路閘道
在此步驟中，您可以建立 hello 虛擬網路閘道的 VNet。 建立閘道可以通常要花費 45 分鐘以上，視 hello 選取的閘道 SKU。 如果您要建立此設定做為練習，您可以參考 toohello[範例設定](#values)。

### <a name="toocreate-a-virtual-network-gateway"></a>toocreate 虛擬網路閘道
[!INCLUDE [vpn-gateway-add-gw-rm-portal](../../includes/vpn-gateway-add-gw-rm-portal-include.md)]

## <a name="CreateTestVNet4"></a>6.建立及設定 TestVNet4
當您設定 TestVNet1 之後時，請重複 hello 先前步驟中，取代這些 TestVNet4 hello 值建立 TestVNet4。 您無須 toowait TestVNet1 hello 虛擬網路閘道後才設定 TestVNet4 之前建立。 如果您使用您自己的值，請確定 hello 位址空間不與任何 hello 您想要 tooconnect 的 Vnet 重疊。

## <a name="TestVNet1Connection"></a>7.設定 hello TestVNet1 連線
當完成 TestVNet1 和 TestVNet4 hello 虛擬網路閘道時，您可以建立虛擬網路閘道連線。 在本節中，您將從 VNet1 tooVNet4 建立連接。 這些步驟只適用於 hello 的 Vnet 相同訂用帳戶。 如果您的 Vnet 不同訂用帳戶中，您必須使用 PowerShell toomake hello 連接。 請參閱 hello [PowerShell](vpn-gateway-vnet-vnet-rm-ps.md)發行項。

1. 在**所有資源**，瀏覽您的 VNet toohello 虛擬網路閘道。 例如，**TestVNet1GW**。 按一下**TestVNet1GW** tooopen hello 虛擬網路閘道刀鋒視窗。
   
    ![連接刀鋒視窗](./media/vpn-gateway-howto-vnet-vnet-resource-manager-portal/settings_connection.png "連接刀鋒視窗e")
2. 按一下**+ 加**tooopen hello**加入連接**刀鋒視窗。
3. 在 hello**加入連接**刀鋒視窗中，在 hello 名稱欄位中，輸入您的連線的名稱。 例如，**TestVNet1toTestVNet4**。
   
    ![連接名稱](./media/vpn-gateway-howto-vnet-vnet-resource-manager-portal/v1tov4.png "連接名稱")
4. 在 [連線類型] 中， 選取**VNet 對 VNet**從 hello 下拉式清單。
5. hello**第一個虛擬網路閘道**因為您正在建立此連線從 hello 指定的虛擬網路閘道，自動填入欄位值。
6. hello**第二個虛擬網路閘道**欄位是 hello 的 hello VNet 的虛擬網路閘道的 toocreate 的連接。 按一下**選擇另一個虛擬網路閘道**tooopen hello**選擇虛擬網路閘道**刀鋒視窗。
   
    ![新增連接](./media/vpn-gateway-howto-vnet-vnet-resource-manager-portal/add_connection.png "新增連接")
7. 列出此刀鋒視窗檢視 hello 虛擬網路閘道。 請注意，只會列出您的訂用帳戶中的虛擬網路閘道。 如果您希望您的訂用帳戶的 tooconnect tooa 虛擬網路閘道，請使用 hello [PowerShell 文章](vpn-gateway-vnet-vnet-rm-ps.md)。 
8. 按一下您想要 tooconnect hello 虛擬網路閘道。
9. 在 hello**共用金鑰**欄位中，輸入您的連線的共用的金鑰。 您可以產生此金鑰，或自行建立此金鑰。 在 站對站連接 hello 您使用的索引鍵會是完全 hello 相同的內部部署裝置和虛擬網路閘道連接。 hello 概念很類似，不同處在於連線 tooa VPN 裝置，而您要連接 tooanother 虛擬網路閘道。
   
    ![共用金鑰](./media/vpn-gateway-howto-vnet-vnet-resource-manager-portal/sharedkey.png "共用金鑰")
10. 按一下**確定**在 hello hello 刀鋒視窗 toosave 底部 您的變更。

## <a name="TestVNet4Connection"></a>8.設定 hello TestVNet4 連線
接下來，從 TestVNet4 tooTestVNet1 建立連接。 使用 hello 相同您使用從 TestVNet1 tooTestVNet4 toocreate hello 連接方法。 請確定您使用 hello 相同的共用金鑰。

## <a name="VerifyConnection"></a>9.確認您的連接
請確認 hello 連線。 每個虛擬網路閘道，請勿 hello 遵循：

1. 找出 hello 虛擬網路閘道的 hello 刀鋒視窗。 例如，**TestVNet4GW**。 
2. 在 hello 虛擬網路閘道刀鋒視窗中，按一下 **連線**hello 虛擬網路閘道的 tooview hello 連線刀鋒視窗。

檢視 hello 連線，並確認 hello 狀態。 Hello 連線建立之後，您會看到**Succeeded**和**Connected** hello 狀態值為。

![已成功](./media/vpn-gateway-howto-vnet-vnet-resource-manager-portal/connected.png "已成功")

您可以按兩下每個連接，個別 tooview hello 連線的相關資訊。

![程式集](./media/vpn-gateway-howto-vnet-vnet-resource-manager-portal/essentials.png "程式集")

## <a name="faq"></a>VNet 對 VNet 常見問題集
檢視 VNet 對 VNet 連線的其他資訊的 hello 常見問題集詳細資料。

[!INCLUDE [vpn-gateway-vnet-vnet-faq](../../includes/vpn-gateway-vnet-vnet-faq-include.md)]

## <a name="next-steps"></a>後續步驟
一旦完成您的連線，您可以將虛擬機器 tooyour 虛擬網路。 請參閱 hello[虛擬機器文件](https://docs.microsoft.com/azure/#pivot=services&panel=Compute)如需詳細資訊。
