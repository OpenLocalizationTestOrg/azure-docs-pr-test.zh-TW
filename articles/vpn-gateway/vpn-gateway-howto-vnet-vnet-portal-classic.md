---
title: "建立 VNet 之間的連線：傳統：Azure 入口網站 | Microsoft Docs"
description: "如何 tooconnect Azure 虛擬網路一起使用 PowerShell 和 hello Azure 傳統入口網站。"
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/02/2017
ms.author: cherylmc
ms.openlocfilehash: f29c3c091d049ff96cf59f4c28ab86a100bcb5fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-vnet-to-vnet-connection-classic"></a>設定 VNet 對 VNet 連線 (傳統)

[!INCLUDE [deployment models](../../includes/vpn-gateway-classic-deployment-model-include.md)]

本文章將示範如何 toocreate 虛擬網路之間的 VPN 閘道連線。 hello 虛擬網路可在 hello 相同或不同區域，並從 hello 相同或不同的訂用帳戶。 本文章中的 hello 步驟適用於 toohello 傳統部署模型和 hello Azure 入口網站。 您也可以建立此組態使用不同的部署工具或部署模型，從下列清單中的 hello 選取不同的選項：

> [!div class="op_single_selector"]
> * [Azure 入口網站](vpn-gateway-howto-vnet-vnet-resource-manager-portal.md)
> * [PowerShell](vpn-gateway-vnet-vnet-rm-ps.md)
> * [Azure CLI](vpn-gateway-howto-vnet-vnet-cli.md)
> * [Azure 入口網站 (傳統)](vpn-gateway-howto-vnet-vnet-portal-classic.md)
> * [連線不同的部署模型 - Azure 入口網站](vpn-gateway-connect-different-deployment-models-portal.md)
> * [連線不同的部署模型 - PowerShell](vpn-gateway-connect-different-deployment-models-powershell.md)
>
>

![VNet tooVNet 連線能力圖表](./media/vpn-gateway-howto-vnet-vnet-portal-classic/v2vclassic.png)

## <a name="about-vnet-to-vnet-connections"></a>關於 VNet 對 VNet 連線

在 hello 傳統部署模型中使用的 VPN 閘道連接虛擬網路 tooanother 虛擬網路 (VNet 對 VNet) 是類似 tooconnecting 虛擬網路 tooan 在內部部署站台位置。 這兩種連線類型使用的 VPN 閘道 tooprovide 採用 IPsec/IKE 的安全通道。

hello 您連接的 Vnet 可位於不同的訂用帳戶和不同的區域。 您可以結合 VNet tooVNet 通訊與多網站組態。 這可讓您建立結合了跨單位連線與內部虛擬網路連線的網路拓撲。

![VNet tooVNet 連線](./media/vpn-gateway-howto-vnet-vnet-portal-classic/aboutconnections.png)

### <a name="why"></a>為什麼要連線虛擬網路？

您可以遵循原因 hello tooconnect 虛擬網路：

* **跨區域的異地備援和異地目前狀態**

  * 您可以使用安全連線設定自己的異地複寫或同步處理，而不用查看網際網路對向端點。
  * 有了 Azure Load Balancer 和 Microsoft 或第三方叢集技術，您便可以利用跨多個 Azure 區域的異地備援，設定具有高可用性的工作負載。 重要的一個例子是 tooset 設定 SQL Always On 與分配到多個 Azure 區域的可用性群組。
* **具有嚴密隔離界限的區域性多層式應用程式**

  * 在 hello 相同區域中，您可以設定多層應用程式與多個 Vnet 連接以及嚴密隔離和安全層級間通訊。
* **Azure 中的跨訂用帳戶、組織間通訊**

  * 如果您有多個 Azure 訂用帳戶，您可以將虛擬網路之間不同訂用帳戶的工作負載安全地連接在一起。
  * 針對企業或服務提供者，您可以在 Azure 中使用安全 VPN 技術啟用跨組織通訊。

如需 VNet 對 VNet 連線的詳細資訊，請參閱[VNet 對 VNet 考量](#faq)hello 本文結尾處。

### <a name="before-you-begin"></a>開始之前

開始這個練習中前, 下載並安裝 hello 的 hello Azure 服務管理 (SM) PowerShell cmdlet 的最新版本。 如需詳細資訊，請參閱[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)。 我們會將大部分的 hello 步驟 hello 入口網站，但您必須使用 PowerShell toocreate hello 連線 hello Vnet 之間。 您無法建立 hello 連線使用 hello Azure 入口網站。

## <a name="plan"></a>步驟 1 - 規劃 IP 位址範圍

它是您將使用 tooconfigure 您的虛擬網路的重要 toodecide hello 範圍。 此組態中，您必須確定沒有任何 VNet 範圍重疊彼此，或與任何 hello 所連接的區域網路。

hello 下表顯示的範例 toodefine Vnet。 使用 hello 範圍僅供參考。 記下您的虛擬網路的 hello 範圍。 稍後的步驟將會需要這項資訊。

**範例**

| 虛擬網路 | 位址空間 | 區域 | Toolocal 網路站台連線 |
|:--- |:--- |:--- |:--- |
| TestVNet1 |TestVNet1<br>(10.11.0.0/16)<br>(10.12.0.0/16) |美國東部 |VNet4Local<br>(10.41.0.0/16)<br>(10.42.0.0/16) |
| TestVNet4 |TestVNet4<br>(10.41.0.0/16)<br>(10.42.0.0/16) |美國西部 |VNet1Local<br>(10.11.0.0/16)<br>(10.12.0.0/16) |

## <a name="vnetvalues"></a>步驟 2-建立虛擬網路，hello

建立兩個虛擬網路中 hello [Azure 入口網站](https://portal.azure.com)。 Hello 步驟 toocreate 傳統虛擬網路，請參閱[建立傳統的虛擬網路](../virtual-network/virtual-networks-create-vnet-classic-pportal.md)。 

當使用 hello 入口 toocreate 傳統的虛擬網路時，您必須使用下列步驟，否則 hello 選項 toocreate 傳統的虛擬網路不會出現的 hello 來巡覽 toohello 虛擬網路 刀鋒視窗：

1. 按一下 hello '+' tooopen hello 'New' 刀鋒視窗。
2. Hello '搜尋 hello marketplace' 欄位中，輸入 [虛擬網路]。 如果相反地，選取 網路功能-> 虛擬網路，則不會收到 hello 選項 toocreate 傳統的 VNet。
3. 傳回清單中的 hello 從找出 虛擬網路，然後按一下 tooopen hello 虛擬網路 刀鋒視窗。 
4. Hello 虛擬網路] 刀鋒視窗中，選取 [傳統' toocreate 傳統的 VNet。 

如果您使用這份文件做為練習，您可以使用下列範例值 hello:

**TestVNet1 的值**

名稱︰TestVNet1<br>
位址空間︰10.11.0.0/16、10.12.0.0/16 (選擇性)<br>
子網路名稱：default<br>
子網路位址範圍：10.11.0.1/24<br>
資源群組：ClassicRG<br>
位置：美國東部<br>
GatewaySubnet：10.11.1.0/27

**TestVNet4 的值**

名稱︰TestVNet4<br>
位址空間︰10.41.0.0/16、10.42.0.0/16 (選擇性)<br>
子網路名稱：default<br>
子網路位址範圍：10.41.0.1/24<br>
資源群組：ClassicRG<br>
位置：美國西部<br>
GatewaySubnet：10.41.1.0/27

**在建立 Vnet 時，請記得 hello 下列設定：**

* **虛擬網路位址空間**– 在 hello 虛擬網路位址空間頁面上，指定您想 toouse，虛擬網路的 hello 位址範圍。 這些是 hello 動態 IP 位址將指派 toohello Vm，而您將部署 toothis 虛擬網路的其他角色執行個體。<br>您選取的空間不能與 hello 位址空間重疊任何 hello 位址 hello 此 VNet 將會連接到其他 Vnet 或內部部署位置。

* **位置** – 當您建立虛擬網路時，您會將該位置與 Azure 位置 (區域) 產生關聯。 例如，如果您想為您 Vm 部署實體上位於美國西部 tooyour 虛擬網路 toobe，選取該位置。 您無法變更您在建立之後，您的虛擬網路與相關聯的 hello 位置。

**建立 Vnet 之後, 您可以新增下列設定的 hello:**

* **位址空間**– 其他位址空間不需要此設定，但您可以建立 hello VNet 之後加入其他位址空間。

* **子網路**– 不需要針對此設定，其他子網路，但是您可能想 toohave 中與其他角色執行個體位於不同子網路的 Vm。

* **DNS 伺服器**– 輸入 hello DNS 伺服器名稱和 IP 位址。 此設定不會建立 DNS 伺服器。 它可讓您為此虛擬網路的名稱解析需 toouse toospecify hello DNS 伺服器。

在本節中，您可以設定 hello 連接類型，hello 本機站台，並建立 hello 閘道。

## <a name="localsite"></a>步驟 3-設定 hello 本機站台

Azure 會使用 hello 中指定的設定每個區域網路網站 toodetermine tooroute hello Vnet 之間的流量。 每個 VNet 必須指向 toohello 個別區域網路，您想讓 tooroute 流量。 您決定要 toouse toorefer tooeach 區域網路網站的 hello 名稱。 它是最佳 toouse 描述性項目。

比方說，TestVNet1 tooa 區域網路的站台連線，您建立名為 'VNet4Local'。 VNet4Local hello 設定包含 TestVNet4 hello 位址前置詞。

hello 本機站台的每個 VNet 是 hello 另一個 VNet。 下列範例值 hello 適用於我們的設定：

| 虛擬網路 | 位址空間 | 區域 | Toolocal 網路站台連線 |
|:--- |:--- |:--- |:--- |
| TestVNet1 |TestVNet1<br>(10.11.0.0/16)<br>(10.12.0.0/16) |美國東部 |VNet4Local<br>(10.41.0.0/16)<br>(10.42.0.0/16) |
| TestVNet4 |TestVNet4<br>(10.41.0.0/16)<br>(10.42.0.0/16) |美國西部 |VNet1Local<br>(10.11.0.0/16)<br>(10.12.0.0/16) |

1. 尋找 TestVNet1 hello Azure 入口網站中。 在 hello **VPN 連線**> 一節的 hello 刀鋒視窗中，按一下 **閘道**。

    ![沒有閘道](./media/vpn-gateway-howto-vnet-vnet-portal-classic/nogateway.png)
2. 在 hello**新的 VPN 連線**頁面上，選取**站對站**。
3. 按一下**本機站台**tooopen hello 本機站台頁面並 hello 的設定。
4. 在 hello**本機站台**頁面上，您的本機站台的名稱。 在本例中，我們命名 hello 本機站台 'VNet4Local'。
5. 針對 [VPN 閘道 IP 位址]，只要是有效的格式，您可以使用您想要的任何 IP 位址。 一般而言，您會使用 VPN 裝置 hello 實際外部 IP 位址。 但是，傳統的 VNet 對 VNet 組態，您可以使用 hello 公用 IP 位址指派給您的 VNet toohello 閘道。 假設您已尚未建立 hello 虛擬網路閘道，您可以指定任何有效的公用 IP 位址做為預留位置。<br>請勿將此欄位留白 - 這不是此組態的選擇性欄位。 在稍後步驟中，您會返回這些設定，並設定它們與 hello 對應虛擬網路閘道的 IP 位址，Azure 會產生它之後。
6. 如**用戶端的位址空間**，使用另一個 VNet hello hello 位址空間。 Tooyour 規劃範例，請參閱。 按一下**確定**toosave 您的設定和傳回後 toohello**新的 VPN 連線**刀鋒視窗。

    ![本機網站](./media/vpn-gateway-howto-vnet-vnet-portal-classic/localsite.png)

## <a name="gw"></a>步驟 4-建立 hello 虛擬網路閘道

每個虛擬網路都必須有虛擬網路閘道。 hello 虛擬網路閘道路由，並加密流量。

1. 在 hello**新的 VPN 連線**刀鋒視窗中，選取 hello 核取方塊**立即建立閘道**。
2. 按一下 [子網路、大小和路由類型]。 在 hello**閘道組態**刀鋒視窗中，按一下 **子網路**。
3. 與 hello 需要名稱為 'GatewaySubnet'，就會自動填入 hello 閘道子網路名稱。 hello**位址範圍**包含 hello 配置 toohello VPN 閘道服務的 IP 位址。 某些設定可讓閘道子網路/29，但它的最佳 toouse/28 或 /27 tooaccommodate 未來組態可能需要多個 IP 位址的 hello 閘道服務。 在我們的範例設定中，我們會使用 10.11.1.0/27。 調整 hello 位址空間，然後按一下 **確定**。
4. 設定 hello**閘道大小**。 此設定表示 toohello[閘道 SKU](vpn-gateway-about-vpn-gateway-settings.md#gwsku)。
5. 設定 hello**路由類型**。 hello 路由類型，此設定必須是**動態**。 除非您終止 hello 閘道，並建立新的連線，您無法稍後變更 hello 路由類型。
6. 按一下 [確定] 。
7. 在 hello**新的 VPN 連線**刀鋒視窗中，按一下**確定**toobegin 建立 hello 虛擬網路閘道。 建立閘道可以通常要花費 45 分鐘以上，視 hello 選取的閘道 SKU。

## <a name="vnet4settings"></a>步驟 5 - 進行 TestVNet4 設定

重覆步驟 hello[建立本機網站](#localsite)和[建立 hello 虛擬網路閘道](#gw)tooconfigure TestVNet4，替代 hello 值只有在必要時。 如果您進行練習，請使用 hello[範例值](#vnetvalues)。

## <a name="updatelocal"></a>步驟 6-更新 hello 本機站台

這兩個 vnet 建立虛擬網路閘道之後，您必須調整 hello 本機站台**VPN 閘道 IP 位址**值。

|VNet 名稱|已連線網站|閘道 IP 位址|
|:--- |:--- |:--- |
|TestVNet1|VNet4Local|TestVNet4 的 VPN 閘道 IP 位址|
|TestVNet4|VNet1Local|TestVNet1 的 VPN 閘道 IP 位址|

### <a name="part-1---get-hello-virtual-network-gateway-public-ip-address"></a>組件 1-取得 hello 虛擬網路閘道的公用 IP 位址

1. Hello Azure 入口網站中，找出您的虛擬網路。
2. 按一下 tooopen hello VNet**概觀**刀鋒視窗。 Hello 刀鋒視窗，在**VPN 連線**，您可以檢視您的虛擬網路閘道 hello IP 位址。

  ![公用 IP](./media/vpn-gateway-howto-vnet-vnet-portal-classic/publicIP.png)
3. 複製 hello IP 位址。 您可以將 hello 下一節。
4. 對 TestVNet4 重複執行這些步驟

### <a name="part-2---modify-hello-local-sites"></a>第 2 部分-修改 hello 本機站台

1. Hello Azure 入口網站中，找出您的虛擬網路。
2. 在 hello VNet**概觀**刀鋒視窗中，按一下 hello 本機站台。

  ![建立本機網站](./media/vpn-gateway-howto-vnet-vnet-portal-classic/local.png)
3. 在 hello**站對站 VPN 連線**刀鋒視窗中，按一下您想 toomodify hello 本機站台 hello 名稱。

  ![開啟本機網站](./media/vpn-gateway-howto-vnet-vnet-portal-classic/openlocal.png)
4. 按一下 hello**本機站台**想 toomodify。

  ![修改網站](./media/vpn-gateway-howto-vnet-vnet-portal-classic/connections.png)
5. 更新 hello **VPN 閘道 IP 位址**按一下**確定**toosave hello 設定。

  ![閘道 IP](./media/vpn-gateway-howto-vnet-vnet-portal-classic/gwupdate.png)
6. 關閉 hello 其他刀鋒視窗。
7. 對 TestVNet4 重複執行這些步驟。

## <a name="getvalues"></a>步驟 7: hello 網路組態檔中的擷取值

當您在 hello Azure 入口網站中建立傳統的 Vnet 時，您檢視的 hello 名稱不是您使用 PowerShell 的 hello 完整名稱。 例如，出現 toobe 名為 VNet **TestVNet1**在 hello 入口網站中，可能會有多長的名稱 hello 網路組態檔中。 hello 名稱可能看起來像這樣：**群組 ClassicRG TestVNet1**。 當您建立您的連線時，是您在 hello 網路組態檔中看到的重要 toouse hello 值。

在 hello 下列步驟，您將連接 tooyour Azure 帳戶然後下載並檢視 hello 網路組態檔 tooobtain hello 值所需的連線。

1. 下載並安裝 hello 的 hello Azure 服務管理 (SM) PowerShell cmdlet 的最新版本。 如需詳細資訊，請參閱[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)。

2. 使用提高的權限開啟 PowerShell 主控台和 tooyour 帳戶連接。 使用下列範例 toohelp 您連接的 hello:

  ```powershell
  Login-AzureRmAccount
  ```

  請檢查 hello hello 帳戶的訂用帳戶。

  ```powershell
  Get-AzureRmSubscription
  ```

  如果您有多個訂閱，選取您想 toouse hello 訂用帳戶。

  ```powershell
  Select-AzureRmSubscription -SubscriptionName "Replace_with_your_subscription_name"
  ```

  接下來，使用下列 cmdlet tooadd hello Azure 訂用帳戶 tooPowerShell hello 傳統部署模型。

  ```powershell
  Add-AzureAccount
  ```
3. 匯出並檢視 hello 網路組態檔。 您的電腦上建立目錄，然後匯出 hello 網路組態檔 toohello 目錄。 在此範例中，hello 網路組態檔匯出太**C:\AzureNet**。

  ```powershell
  Get-AzureVNetConfig -ExportToFile C:\AzureNet\NetworkConfig.xml
  ```
4. 開啟 hello 檔案，並為您的 Vnet 和站台的文字編輯器和檢視 hello 名稱。 這些會是建立您的連線時所使用的 hello 名稱。<br>VNet 名稱會列為 **VirtualNetworkSite name =**<br>網站名稱會列為 **LocalNetworkSiteRef name =**

## <a name="createconnections"></a>步驟 8-建立 hello VPN 閘道連線

當 hello 上述所有步驟都完成時，您可以將 hello IPsec/IKE 預先共用的金鑰，並建立 hello 連線。 這組步驟會使用 PowerShell。 無法在 hello Azure 入口網站中設定 hello 傳統部署模型的 VNet 對 VNet 連線。

在 hello 範例中，請注意，hello 共用的金鑰是完全 hello 相同。 一定要相符 hello 共用的金鑰。 為確定 tooreplace hello hello 確切名稱，您的 Vnet 與區域網路網站與這些範例中的值。

1. 建立 hello TestVNet1 tooTestVNet4 連線。

  ```powershell
  Set-AzureVNetGatewayKey -VNetName 'Group ClassicRG TestVNet1' `
  -LocalNetworkSiteName '17BE5E2C_VNet4Local' -SharedKey A1b2C3D4
  ```
2. 建立 hello TestVNet4 tooTestVNet1 連線。

  ```powershell
  Set-AzureVNetGatewayKey -VNetName 'Group ClassicRG TestVNet4' `
  -LocalNetworkSiteName 'F7F7BFC7_VNet1Local' -SharedKey A1b2C3D4
  ```
3. 等候 hello 連線 tooinitialize。 一旦 hello 閘道完成初始化，hello 狀態會是 '成功'。

  ```
  Error          :
  HttpStatusCode : OK
  Id             :
  Status         : Successful
  RequestId      :
  StatusCode     : OK
  ```

## <a name="faq"></a>傳統 VNet 的 VNet 對 VNet 考量
* hello 虛擬網路可位於 hello 相同或不同的訂用帳戶。
* hello 虛擬網路可位於 hello 相同或不同 Azure 區域 （位置）。
* 即使虛擬網路連接在一起，雲端服務或負載平衡端點也無法跨虛擬網路。
* 將多個虛擬網路連接在一起並不需要任何 VPN 裝置。
* VNet 對 VNet 支援連接 Azure 虛擬網路。 不支援連接的虛擬機器或雲端服務不會部署 tooa 虛擬網路。
* VNet 對 VNet 需要動態路由閘道。 不支援 Azure 靜態路由閘道。
* 虛擬網路連線能力可以與多站台 VPN 同時使用。 沒有最多 10 個 VPN 通道連線 tooeither 其他虛擬網路或在內部部署網站虛擬網路 VPN 閘道。
* hello hello 虛擬網路及內部部署區域網路網站不能重疊位址空間。 重疊的位址空間會導致 hello 建立虛擬網路或上傳的 netcfg 組態檔 toofail。
* 不支援成對虛擬網路之間的備援通道。
* 所有 VPN 通道 hello VNet，包括 P2S Vpn、 共用 hello hello VPN 閘道，可用的頻寬，以及 hello 相同 azure VPN 閘道執行時間 SLA。
* VNet 對 VNet 流量會透過 hello Azure 骨幹。

## <a name="next-steps"></a>後續步驟
確認您的連線。 [確認 VPN 閘道連線](vpn-gateway-verify-connection-resource-manager.md)。
