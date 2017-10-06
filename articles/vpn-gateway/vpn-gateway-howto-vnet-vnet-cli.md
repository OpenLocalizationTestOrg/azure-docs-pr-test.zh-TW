---
title: "連接虛擬網路 tooanother VNet: Azure CLI |Microsoft 文件"
description: "本文將逐步引導您使用 Azure Resource Manager 和 Azure CLI，將虛擬網路連線在一起。"
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 0683c664-9c03-40a4-b198-a6529bf1ce8b
ms.service: vpn-gateway
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/02/2017
ms.author: cherylmc
ms.openlocfilehash: 70113914bcae03c80f9ad133ff081d1cf37fc309
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-vnet-to-vnet-vpn-gateway-connection-using-azure-cli"></a>使用 Azure CLI 設定 VNet 對 VNet 的 VPN 閘道連線

本文章將示範如何 toocreate 虛擬網路之間的 VPN 閘道連線。 hello 虛擬網路可在 hello 相同或不同區域，並從 hello 相同或不同的訂用帳戶。 當連接的 Vnet，從不同的訂用帳戶，hello 訂用帳戶不需要與相關聯的 toobe hello 相同的 Active Directory 租用戶。 

這篇文章中的 hello 步驟套用 toohello Resource Manager 部署模型，並使用 Azure CLI。 您也可以建立此組態使用不同的部署工具或部署模型，從下列清單中的 hello 選取不同的選項：

> [!div class="op_single_selector"]
> * [Azure 入口網站](vpn-gateway-howto-vnet-vnet-resource-manager-portal.md)
> * [PowerShell](vpn-gateway-vnet-vnet-rm-ps.md)
> * [Azure CLI](vpn-gateway-howto-vnet-vnet-cli.md)
> * [Azure 入口網站 (傳統)](vpn-gateway-howto-vnet-vnet-portal-classic.md)
> * [連線不同的部署模型 - Azure 入口網站](vpn-gateway-connect-different-deployment-models-portal.md)
> * [連線不同的部署模型 - PowerShell](vpn-gateway-connect-different-deployment-models-powershell.md)
>
>

連接虛擬網路 tooanother 虛擬網路 (VNet 對 VNet) 是類似 tooconnecting VNet tooan 在內部部署站台位置。 這兩種連線類型使用的 VPN 閘道 tooprovide 採用 IPsec/IKE 的安全通道。 如果您的 Vnet hello 中相同的區域，您可能會想 tooconsider 它們使用對等互連的 VNet 連接。 VNet 對等互連不會使用 VPN 閘道。 如需詳細資訊，請參閱 [VNet 對等互連](../virtual-network/virtual-network-peering-overview.md)。

您可以將 VNet 對 VNet 通訊與多站台組態結合。 這可讓您建立結合內部虛擬網路連線使用跨單位連線的網路拓樸 hello 下列圖表所示：

![關於連線](./media/vpn-gateway-howto-vnet-vnet-cli/aboutconnections.png)

### <a name="why"></a>為什麼要連線虛擬網路？

您可以遵循原因 hello tooconnect 虛擬網路：

* **跨區域的異地備援和異地目前狀態**

  * 您可以使用安全連線設定自己的異地複寫或同步處理，而不用查看網際網路對向端點。
  * 您可以使用 Azure 流量管理員和負載平衡器，利用異地備援跨多個 Azure 區域設定高度可用的工作負載。 重要的一個例子是 tooset 設定 SQL Always On 與分配到多個 Azure 區域的可用性群組。
* **具有隔離或管理界限的區域性多層式應用程式**

  * 在 hello 相同區域中，您可以設定多層應用程式與多個虛擬網路連接在一起，因為 tooisolation 或系統管理需求。

如需 VNet 對 VNet 連線的詳細資訊，請參閱 hello [VNet 對 VNet 常見問題集](#faq)hello 本文結尾處。

### <a name="which-set-of-steps-should-i-use"></a>我應該使用哪個步驟集？

在本文中，您會看到兩組不同的步驟。 一組步驟[Vnet 中的 hello 相同訂用帳戶](#samesub)，而另一個用於[位於不同的訂用帳戶中的 Vnet](#difsub)。

## <a name="samesub"></a>連線 Vnet 中 hello 相同訂用帳戶

![v2v 圖表](./media/vpn-gateway-howto-vnet-vnet-cli/v2vrmps.png)

### <a name="before-you-begin"></a>開始之前

在開始之前，安裝 hello 最新版本 （2.0 或更新版本） 的 hello CLI 命令。 如需安裝 hello CLI 命令的資訊，請參閱[安裝 Azure CLI 2.0](/cli/azure/install-azure-cli)。

### <a name="Plan"></a>規劃 IP 位址範圍

在 hello 下列步驟，我們會建立兩個虛擬網路，以及其個別的閘道子網路和設定。 我們再建立 hello 之間的 VPN 連線兩個 Vnet。 它是您的網路設定的重要 tooplan hello IP 位址範圍。 請記住，您必須先確定您的 VNet 範圍或區域網路範圍沒有以任何方式重疊。 在這些範例中，我們不會包含 DNS 伺服器。 如果您想要了解虛擬網路的名稱解析，請參閱[名稱解析](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md)。

我們使用下列值 hello 範例中的 hello:

**TestVNet1 的值︰**

* VNet 名稱︰TestVNet1
* 資源群組︰TestRG1
* 位置：美國東部
* TestVNet1：10.11.0.0/16 和 10.12.0.0/16
* FrontEnd：10.11.0.0/24
* BackEnd：10.12.0.0/24
* GatewaySubnet：10.12.255.0/27
* GatewayName：VNet1GW
* 公用 IP: VNet1GWIP
* VPNType：RouteBased
* Connection(1to4)：VNet1toVNet4
* Connection(1to5)：VNet1toVNet5
* ConnectionType：VNet2VNet

**TestVNet4 的值︰**

* VNet 名稱︰TestVNet4
* TestVNet2：10.41.0.0/16 和 10.42.0.0/16
* FrontEnd：10.41.0.0/24
* BackEnd：10.42.0.0/24
* GatewaySubnet：10.42.255.0/27
* 資源群組：TestRG4
* 位置：美國西部
* GatewayName：VNet4GW
* 公用 IP：VNet4GWIP
* VPNType：RouteBased
* 連線︰VNet4toVNet1
* ConnectionType：VNet2VNet


### <a name="Connect"></a>步驟 1-連接 tooyour 訂用帳戶

[!INCLUDE [CLI login](../../includes/vpn-gateway-cli-login-numbers-include.md)]

### <a name="TestVNet1"></a>步驟 2 - 建立及設定 TestVNet1

1. 建立資源群組。

  ```azurecli
  az group create -n TestRG1  -l eastus
  ```
2. 建立 TestVNet1 TestVNet1 和 hello 子網路。 此範例會建立名為 TestVNet1 的虛擬網路和名為 FrontEnd 的子網路。

  ```azurecli
  az network vnet create -n TestVNet1 -g TestRG1 --address-prefix 10.11.0.0/16 -l eastus --subnet-name FrontEnd --subnet-prefix 10.11.0.0/24
  ```
3. 建立 hello 後端子網路的其他位址空間。 請注意，在此步驟中，我們指定我們稍早建立這兩個 hello 位址空間 hello 我們想要 tooadd 其他位址空間。 這是因為 hello [az 網路 vnet 更新](https://docs.microsoft.com/cli/azure/network/vnet#update)命令會覆寫 hello 先前的設定。 請確定 toospecify hello 位址首碼的所有使用這個命令時。

  ```azurecli
  az network vnet update -n TestVNet1 --address-prefixes 10.11.0.0/16 10.12.0.0/16 -g TestRG1
  ```
4. 建立 hello 後端子網路。
  
  ```azurecli
  az network vnet subnet create --vnet-name TestVNet1 -n BackEnd -g TestRG1 --address-prefix 10.12.0.0/24 
  ```
5. 建立 hello 閘道子網路。 請注意該 hello 閘道子網路名稱為 'GatewaySubnet'。 此名稱是必要的。 在此範例中，使用 /27 hello 閘道子網路。 雖然可能 toocreate 閘道子網路為/29，我們建議您建立較大的子網路選取至少是/28 或 /27 包含多個位址。 這可讓足夠位址 tooaccommodate 可能其他組態，您可能想在 hello 未來。

  ```azurecli 
  az network vnet subnet create --vnet-name TestVNet1 -n GatewaySubnet -g TestRG1 --address-prefix 10.12.255.0/27
  ```
6. 要求的公用 IP 位址 toobe 配置的 toohello 閘道您將建立您的 VNet。 請注意該 hello AllocationMethod 是動態。 您無法指定您想 toouse hello IP 位址。 它是動態配置的 tooyour 閘道。

  ```azurecli
  az network public-ip create -n VNet1GWIP -g TestRG1 --allocation-method Dynamic
  ```
7. 建立 TestVNet1 hello 虛擬網路閘道。 VNet 對 VNet 組態需要 RouteBased VpnType。 如果您執行此命令使用 hello '-沒有-wait' 參數，您沒有看到任何意見反應或輸出。 hello '-沒有-wait' 參數可讓 hello 閘道 toocreate hello 背景。 它並不表示該 hello VPN 閘道完成立即建立。 建立閘道可以通常要花費 45 分鐘或更多，根據 hello 閘道使用的 SKU。

  ```azurecli
  az network vnet-gateway create -n VNet1GW -l eastus --public-ip-address VNet1GWIP -g TestRG1 --vnet TestVNet1 --gateway-type Vpn --sku VpnGw1 --vpn-type RouteBased --no-wait
  ```

### <a name="TestVNet4"></a>步驟 3 - 建立及設定 TestVNet4

1. 建立資源群組。

  ```azurecli
  az group create -n TestRG4  -l westus
  ```
2. 建立 TestVNet4。

  ```azurecli
  az network vnet create -n TestVNet4 -g TestRG4 --address-prefix 10.41.0.0/16 -l westus --subnet-name FrontEnd --subnet-prefix 10.41.0.0/24
  ```

3. 為 TestVNet4 建立其他子網路。

  ```azurecli
  az network vnet update -n TestVNet4 --address-prefixes 10.41.0.0/16 10.42.0.0/16 -g TestRG4 
  az network vnet subnet create --vnet-name TestVNet4 -n BackEnd -g TestRG4 --address-prefix 10.42.0.0/24 
  ```
4. 建立 hello 閘道子網路。

  ```azurecli
   az network vnet subnet create --vnet-name TestVNet4 -n GatewaySubnet -g TestRG4 --address-prefix 10.42.255.0/27
  ```
5. 要求公用 IP 位址。

  ```azurecli
  az network public-ip create -n VNet4GWIP -g TestRG4 --allocation-method Dynamic
  ```
6. 建立 hello TestVNet4 虛擬網路閘道。

  ```azurecli
  az network vnet-gateway create -n VNet4GW -l westus --public-ip-address VNet4GWIP -g TestRG4 --vnet TestVNet4 --gateway-type Vpn --sku VpnGw1 --vpn-type RouteBased --no-wait
  ```

### <a name="createconnect"></a>步驟 4-建立 hello 連線

您現在有兩個具有 VPN 閘道的 VNet。 hello 下一個步驟是 hello 虛擬網路閘道之間的 toocreate VPN 閘道連線。 如果您使用上述的 hello 範例，VNet 閘道位於不同的資源群組中。 在不同的資源群組中閘道時，您需要 tooidentify，並建立連接時指定每個閘道的 hello 資源 Id。 如果您的 Vnet 中 hello 相同資源群組中，您可以使用 hello[第二個集合的指示](#samerg)因為您不需要 toospecify hello 資源 Id。

### <a name="diffrg"></a>tooconnect 位於不同的資源群組中的 Vnet

1. 取得 hello 的 VNet1GW 資源識別碼 hello 輸出 hello 下列命令：

  ```azurecli
  az network vnet-gateway show -n VNet1GW -g TestRG1
  ```

  Hello 輸出中尋找 hello"識別碼:"行。 hello 並用引號括住的 hello 值為 hello 下一節中所需的 toocreate hello 連線。 使您可以輕鬆地將其貼在建立您的連線時，請複製這些值 tooa 文字編輯器，例如 [記事本]。

  範例輸出︰

  ```
  "activeActive": false, 
  "bgpSettings": { 
    "asn": 65515, 
    "bgpPeeringAddress": "10.12.255.30", 
    "peerWeight": 0 
   }, 
  "enableBgp": false, 
  "etag": "W/\"ecb42bc5-c176-44e1-802f-b0ce2962ac04\"", 
  "gatewayDefaultSite": null, 
  "gatewayType": "Vpn", 
  "id": "/subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW", 
  "ipConfigurations":
  ```

  Hello 值之後，複製**「 識別碼 」:** hello 括在引號內。

  ```
  "id": "/subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW"
 ```

2. 收到 hello 的 VNet4GW 資源識別碼和複製 hello 值 tooa 文字編輯器。

  ```azurecli
  az network vnet-gateway show -n VNet4GW -g TestRG4
  ```

3. 建立 hello TestVNet1 tooTestVNet4 連線。 在此步驟中，您會從 TestVNet1 tooTestVNet4 建立 hello 連線。 沒有 hello 範例中所參考的共用的金鑰。 您可以使用您自己的值為 hello 共用金鑰。 hello 很重要的是該 hello 共用的金鑰必須符合這兩個連接。 建立連線需要時 toocomplete 短。

  ```azurecli
  az network vpn-connection create -n VNet1ToVNet4 -g TestRG1 --vnet-gateway1 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW -l eastus --shared-key "aabbcc" --vnet-gateway2 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG4/providers/Microsoft.Network/virtualNetworkGateways/VNet4GW 
  ```
4. 建立 hello TestVNet4 tooTestVNet1 連線。 除了您要建立 hello 連線從 TestVNet4 tooTestVNet1 類似 toohello 一個以上版本，則此步驟。 請確定 hello 共用金鑰相符。 花幾分鐘的時間 tooestablish hello 連線。

  ```azurecli
  az network vpn-connection create -n VNet4ToVNet1 -g TestRG4 --vnet-gateway1 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG4/providers/Microsoft.Network/virtualNetworkGateways/VNet4GW -l westus --shared-key "aabbcc" --vnet-gateway2 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1G
  ```
5. 確認您的連線。 請參閱[驗證您的連線](#verify)。

### <a name="samerg"></a>tooconnect Vnet 中的 hello 相同資源群組

1. 建立 hello TestVNet1 tooTestVNet4 連線。 在此步驟中，您會從 TestVNet1 tooTestVNet4 建立 hello 連線。 請注意 hello 資源群組是 hello hello 範例中相同。 您也會看見 hello 範例中所參考的共用的金鑰。 您可以使用您自己的值為 hello 共用金鑰，不過，hello 共用的金鑰必須符合這兩個連接。 建立連線需要時 toocomplete 短。

  ```azurecli
  az network vpn-connection create -n VNet1ToVNet4 -g TestRG1 --vnet-gateway1 VNet1GW -l eastus --shared-key "eeffgg" --vnet-gateway2 VNet4GW
  ```
2. 建立 hello TestVNet4 tooTestVNet1 連線。 除了您要建立 hello 連線從 TestVNet4 tooTestVNet1 類似 toohello 一個以上版本，則此步驟。 請確定 hello 共用金鑰相符。 花幾分鐘的時間 tooestablish hello 連線。

  ```azurecli
  az network vpn-connection create -n VNet4ToVNet1 -g TestRG1 --vnet-gateway1 VNet4GW -l eastus --shared-key "eeffgg" --vnet-gateway2 VNet1GW
  ```
3. 確認您的連線。 請參閱[驗證您的連線](#verify)。

## <a name="difsub"></a>與位於不同訂用帳戶的 VNet 連線

![v2v 圖表](./media/vpn-gateway-howto-vnet-vnet-cli/v2vdiffsub.png)

在此案例中，我們會連接 TestVNet1 和 TestVNet5。 hello Vnet 可位於不同的訂用帳戶。 hello 訂用帳戶不需要與 hello 相關聯的 toobe 相同的 Active Directory 租用戶。 此設定的 hello 步驟順序 tooconnect TestVNet1 tooTestVNet5 中加入額外的 VNet 對 VNet 連線。

### <a name="TestVNet1diff"></a>步驟 5 - 建立及設定 TestVNet1

從 hello 前幾節中的 hello 步驟繼續執行這些指示。 您必須先完成[步驟 1](#Connect)和[步驟 2](#TestVNet1) toocreate 並設定 TestVNet1 hello TestVNet1 VPN 閘道。 此組態中，您不需要的 toocreate TestVNet4 hello 前一節，雖然如果您建立它，它不會衝突進行這些步驟。 完成步驟 1 和步驟 2 後，繼續進行下面的步驟 6。

### <a name="verifyranges"></a>步驟 6-確認 hello IP 位址範圍

在建立其他連接時，很重要 tooverify hello 的 hello 新的虛擬網路的 IP 位址空間未與任何其他 VNet 範圍或區域網路閘道的範圍重疊。 針對此練習，您可以使用下列值 hello TestVNet5 hello:

**TestVNet5 的值︰**

* VNet 名稱︰TestVNet5
* 資源群組：TestRG5
* 位置：日本東部
* TestVNet5：10.51.0.0/16 和 10.52.0.0/16
* FrontEnd：10.51.0.0/24
* BackEnd：10.52.0.0/24
* GatewaySubnet：10.52.255.0.0/27
* GatewayName：VNet5GW
* 公用 IP：VNet5GWIP
* VPNType：RouteBased
* 連線︰VNet5toVNet1
* ConnectionType：VNet2VNet

### <a name="TestVNet5"></a>步驟 7 - 建立及設定 TestVNet5

Hello 新訂用帳戶，訂用帳戶 5 hello 內容中，必須完成此步驟。 此組件可能會由擁有 hello 訂用帳戶的另一個組織中的 hello 系統管理員執行。 訂用帳戶使用之間 tooswitch 'az 帳戶清單--所有' toolist hello 訂用帳戶可用 tooyour 帳戶，然後使用 'az 帳戶集--訂用帳戶<subscriptionID>' 想 toouse tooswitch toohello 訂用帳戶。

1. 請確定您已連線的 tooSubscription 5，則建立的資源群組。

  ```azurecli
  az group create -n TestRG5  -l japaneast
  ```
2. 建立 TestVNet5。

  ```azurecli
  az network vnet create -n TestVNet5 -g TestRG5 --address-prefix 10.51.0.0/16 -l japaneast --subnet-name FrontEnd --subnet-prefix 10.51.0.0/24
  ```

3. 新增子網路。

  ```azurecli
  az network vnet update -n TestVNet5 --address-prefixes 10.51.0.0/16 10.52.0.0/16 -g TestRG5
  az network vnet subnet create --vnet-name TestVNet5 -n BackEnd -g TestRG5 --address-prefix 10.52.0.0/24
  ```

4. 加入 hello 閘道子網路。

  ```azurecli
  az network vnet subnet create --vnet-name TestVNet5 -n GatewaySubnet -g TestRG5 --address-prefix 10.52.255.0/27
  ```

5. 要求公用 IP 位址。

  ```azurecli
  az network public-ip create -n VNet5GWIP -g TestRG5 --allocation-method Dynamic
  ```
6. 建立 hello TestVNet5 閘道

  ```azurecli
  az network vnet-gateway create -n VNet5GW -l japaneast --public-ip-address VNet5GWIP -g TestRG5 --vnet TestVNet5 --gateway-type Vpn --sku VpnGw1 --vpn-type RouteBased --no-wait
  ```

### <a name="connections5"></a>步驟 8-建立 hello 連線

我們會分割成兩個標示的 CLI 工作階段的這個步驟**[訂用帳戶 1]**，和**[訂用帳戶 5]**因為 hello 閘道 hello 不同訂用帳戶中。 訂用帳戶使用之間 tooswitch 'az 帳戶清單--所有' toolist hello 訂用帳戶可用 tooyour 帳戶，然後使用 'az 帳戶集--訂用帳戶<subscriptionID>' 想 toouse tooswitch toohello 訂用帳戶。

1. **[訂用帳戶 1]**登入，並連接 tooSubscription 1。 Hello 執行的下列命令 tooget hello 名稱和識別碼 hello hello 輸出的閘道：

  ```azurecli
  az network vnet-gateway show -n VNet1GW -g TestRG1
  ```

  複製 hello 輸出 」 識別碼:"。 傳送 hello 識別碼和 hello hello VNet 閘道 (VNet1GW) toohello 管理員的訂用帳戶 5 透過電子郵件或其他方法的名稱。

  範例輸出︰

  ```
  "id": "/subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW"
  ```

2. **[訂用帳戶 5]**登入，並連接 tooSubscription 5。 Hello 執行的下列命令 tooget hello 名稱和識別碼 hello hello 輸出的閘道：

  ```azurecli
  az network vnet-gateway show -n VNet5GW -g TestRG5
  ```

  複製 hello 輸出 」 識別碼:"。 傳送 hello 識別碼和 hello hello VNet 閘道 (VNet5GW) toohello 管理員的訂用帳戶 1 透過電子郵件或其他方法的名稱。

3. **[訂用帳戶 1]**在此步驟中，您建立從 TestVNet1 tooTestVNet5 hello 連線。 您可以使用您自己的值為 hello 共用金鑰，不過，hello 共用的金鑰必須符合這兩個連接。 建立連接，可能會同時 toocomplete 短。 請確定您連接 tooSubscription 1。

  ```azurecli
  az network vpn-connection create -n VNet1ToVNet5 -g TestRG1 --vnet-gateway1 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW -l eastus --shared-key "eeffgg" --vnet-gateway2 /subscriptions/e7e33b39-fe28-4822-b65c-a4db8bbff7cb/resourceGroups/TestRG5/providers/Microsoft.Network/virtualNetworkGateways/VNet5GW
  ```

4. **[訂用帳戶 5]**這個步驟是上述其中一個類似 toohello，除了您要建立 hello 連線從 TestVNet5 tooTestVNet1。 請確定該 hello 共用金鑰相符，而且您連線 tooSubscription 5。

  ```azurecli
  az network vpn-connection create -n VNet5ToVNet1 -g TestRG5 --vnet-gateway1 /subscriptions/e7e33b39-fe28-4822-b65c-a4db8bbff7cb/resourceGroups/TestRG5/providers/Microsoft.Network/virtualNetworkGateways/VNet5GW -l japaneast --shared-key "eeffgg" --vnet-gateway2 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW
  ```

## <a name="verify"></a>確認 hello 的連接
[!INCLUDE [vpn-gateway-no-nsg-include](../../includes/vpn-gateway-no-nsg-include.md)]

[!INCLUDE [verify connections v2v cli](../../includes/vpn-gateway-verify-connection-cli-rm-include.md)]

## <a name="faq"></a>VNet 對 VNet 常見問題集
[!INCLUDE [vpn-gateway-vnet-vnet-faq](../../includes/vpn-gateway-vnet-vnet-faq-include.md)]

## <a name="next-steps"></a>後續步驟

* 一旦完成您的連線，您可以將虛擬機器 tooyour 虛擬網路。 如需詳細資訊，請參閱 hello[虛擬機器文件](https://docs.microsoft.com/azure/#pivot=services&panel=Compute)。
* BGP 的相關資訊，請參閱 hello [BGP 概觀](vpn-gateway-bgp-overview.md)和[如何 tooconfigure BGP](vpn-gateway-bgp-resource-manager-ps.md)。
