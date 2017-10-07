---
title: "如何 Azure ExpressRoute 電路的路由 tooconfigure: CLI |Microsoft 文件"
description: "這篇文章可協助您建立與 hello 私人、 公用及 Microsoft 對等 ExpressRoute 循環的佈建。 本文也會顯示 toocheck hello 狀態、 更新或刪除您的電路的互連的方式。"
documentationcenter: na
services: expressroute
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: anzaman,cherylmc
ms.openlocfilehash: 33130af050045527cdb316e77821c6d101b6a82a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-routing-for-an-expressroute-circuit-using-cli"></a>使用 CLI 來建立和修改 ExpressRoute 路線的路由

這篇文章可協助您建立及管理在 hello 資源管理員部署模型中使用 CLI 的 ExpressRoute 電路的路由組態。 您也可以檢查 hello 狀態、 更新或刪除，並取消佈建 ExpressRoute 循環的對等互連。 如果您想 toouse 不同方法 toowork 與您的循環，請從下列清單中的 hello 選取一個發行項：

> [!div class="op_single_selector"]
> * [Azure 入口網站](expressroute-howto-routing-portal-resource-manager.md)
> * [PowerShell](expressroute-howto-routing-arm.md)
> * [Azure CLI](howto-routing-cli.md)
> * [視訊 - 私用對等互連](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-private-peering-for-your-expressroute-circuit)
> * [視訊 - 公用對等互連](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-public-peering-for-your-expressroute-circuit)
> * [視訊 - Microsoft 對等互連](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-microsoft-peering-for-your-expressroute-circuit)
> * [PowerShell (傳統)](expressroute-howto-routing-classic.md)
> 

## <a name="configuration-prerequisites"></a>組態必要條件

* 在開始之前，安裝 hello 最新版本 （2.0 或更新版本） 的 hello CLI 命令。 如需安裝 hello CLI 命令的資訊，請參閱[安裝 Azure CLI 2.0](/cli/azure/install-azure-cli)。
* 請確定您已經檢閱 hello[必要條件](expressroute-prerequisites.md)，[路由需求](expressroute-routing.md)，和[工作流程](expressroute-workflows.md)頁面開始設定之前。
* 您必須擁有作用中的 ExpressRoute 線路。 請依照下列指示 hello 太[建立 ExpressRoute 電路](howto-circuit-cli.md)和有 hello 電路啟用您的連線提供者，才能繼續。 hello ExpressRoute 電路必須位於您 toobe 無法 toorun hello 命令，在本文中的佈建並啟用狀態。

這些說明僅適用於 toocircuits 建立與服務供應項目層級 2 連線服務的提供者。 如果您使用的服務提供者提供受管理的第 3 層服務 (通常是 IPVPN，如 MPLS)，連線提供者會為您設定和管理路由。

您可以為 ExpressRoute 線路設定一個、兩個或全部三個對等 (Azure 私用、Azure 公用和 Microsoft)。 您可以依自己選擇的任何順序設定對等。 不過，您必須確定您完成每個對等互連一次一個的 hello 設定。

## <a name="azure-private-peering"></a>Azure 私用對等

本節可協助您建立、 取得、 更新和刪除 hello Azure ExpressRoute 循環的私用對等設定。

### <a name="toocreate-azure-private-peering"></a>toocreate Azure 私人互連

1. 安裝 Azure CLI hello 最新版本。 您必須使用 hello hello Azure 命令列介面 (CLI) 最新版本。 * 檢閱 hello[必要條件](expressroute-prerequisites.md)和[工作流程](expressroute-workflows.md)開始設定之前。

  ```azurecli
  az login
  ```

  選取您想要 toocreate ExpressRoute 電路的 hello 訂用帳戶

  ```azurecli
  az account set --subscription "<subscription ID>"
  ```
2. 建立 ExpressRoute 線路。 請遵循 hello 指示 toocreate [ExpressRoute 電路](howto-circuit-cli.md)，並讓它佈建的 hello 連線服務提供者。

  如果您連線服務提供者提供受管理的第 3 層服務，您可以要求您連線提供者 tooenable 私用對等互連，為您的 Azure。 在此情況下，您不需要 toofollow hello 下一節中所列的指示。 不過，如果您連線服務提供者不會管理路由，在建立您的循環之後繼續您 hello 後續步驟的組態。
3. 請檢查 hello ExpressRoute 電路 toomake 確定佈建，而且也已啟用。 下列範例使用 hello:

  ```azurecli
  az network express-route show --resource-group ExpressRouteResourceGroup --name MyCircuit
  ```

  hello 回應是類似 toohello 下列範例：

  ```azurecli
  "allowClassicOperations": false,
  "authorizations": [],
  "circuitProvisioningState": "Enabled",
  "etag": "W/\"1262c492-ffef-4a63-95a8-a6002736b8c4\"",
  "gatewayManagerEtag": null,
  "id": "/subscriptions/81ab786c-56eb-4a4d-bb5f-f60329772466/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit",
  "location": "westus",
  "name": "MyCircuit",
  "peerings": [],
  "provisioningState": "Succeeded",
  "resourceGroup": "ExpressRouteResourceGroup",
  "serviceKey": "1d05cf70-1db5-419f-ad86-1ca62c3c125b",
  "serviceProviderNotes": null,
  "serviceProviderProperties": {
  "bandwidthInMbps": 200,
  "peeringLocation": "Silicon Valley",
  "serviceProviderName": "Equinix"
  },
  "serviceProviderProvisioningState": "Provisioned",
  "sku": {
    "family": "UnlimitedData",
    "name": "Standard_MeteredData",
    "tier": "Standard"
  },
  "tags": null,
  "type": "Microsoft.Network/expressRouteCircuits]
  ```

4. 設定 Azure 私用對等互連 hello 循環。 請確定您具備下列項目，再繼續進行下一個步驟的 hello hello:

  * / 30 子網路 hello 主要連結。 hello 子網路不能保留的虛擬網路的任何位址空間的一部分。
  * / 30 hello 次要連結的子網路。 hello 子網路不能保留的虛擬網路的任何位址空間的一部分。
  * 有效的 VLAN ID tooestablish 此對等。 請確認沒有其他對等互連中 hello 循環使用 hello 相同 VLAN id。
  * 對等的 AS 編號。 您可以使用 2 位元組和 4 位元組 AS 編號。 您可以將私用 AS 編號用於此對等。 請確定您不是使用 65515。
  * **選用-**如果您選擇其中一個 toouse 的 MD5 雜湊。

  使用下列範例 tooconfigure Azure 私用對等互連，為您的電路的 hello:

  ```azurecli
  az network express-route peering create --circuit-name MyCircuit --peer-asn 100 --primary-peer-subnet 10.0.0.0/30 -g ExpressRouteResourceGroup --secondary-peer-subnet 10.0.0.4/30 --vlan-id 200 --peering-type AzurePrivatePeering
  ```

  如果您選擇 toouse MD5 雜湊時，使用下列範例中的 hello:

  ```azurecli
  az network express-route peering create --circuit-name MyCircuit --peer-asn 100 --primary-peer-subnet 10.0.0.0/30 -g ExpressRouteResourceGroup --secondary-peer-subnet 10.0.0.4/30 --vlan-id 200 --peering-type AzurePrivatePeering --SharedKey "A1B2C3D4"
  ```

  > [!IMPORTANT]
  > 請確定您將 AS 編號指定為對等 ASN，而不是客戶 ASN。
  > 
  > 

### <a name="tooview-azure-private-peering-details"></a>tooview Azure 私用對等互連的詳細資料

您可以使用下列範例中的 hello，以取得設定的詳細資訊：

```azurecli
az network express-route peering show -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePrivatePeering
```

hello 輸出是 toohello 類似下列範例程式碼：

```azurecli
{
  "azureAsn": 12076,
  "etag": "W/\"2e97be83-a684-4f29-bf3c-96191e270666\"",
  "gatewayManagerEtag": "18",
  "id": "/subscriptions/9a0c2943-e0c2-4608-876c-e0ddffd1211b/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit/peerings/AzurePrivatePeering",
  "ipv6PeeringConfig": null,
  "lastModifiedBy": "Customer",
  "microsoftPeeringConfig": null,
  "name": "AzurePrivatePeering",
  "peerAsn": 7671,
  "peeringType": "AzurePrivatePeering",
  "primaryAzurePort": "",
  "primaryPeerAddressPrefix": "",
  "provisioningState": "Succeeded",
  "resourceGroup": "ExpressRouteResourceGroup",
  "routeFilter": null,
  "secondaryAzurePort": "",
  "secondaryPeerAddressPrefix": "",
  "sharedKey": null,
  "state": "Enabled",
  "stats": null,
  "vlanId": 100
}
```

### <a name="tooupdate-azure-private-peering-configuration"></a>tooupdate Azure 私用對等組態

您可以更新使用下列範例中的 hello hello 設定的任何部分。 在此範例中，從 100 too500 正在更新 hello hello 循環的 VLAN ID。

```azurecli
az network express-route peering update --vlan-id 500 -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePrivatePeering
```

### <a name="toodelete-azure-private-peering"></a>toodelete Azure 私人互連

您可以執行下列範例中的 hello 來移除您對等的設定：

> [!WARNING]
> 您必須確定所有虛擬網路，然後再執行此範例會從 hello ExpressRoute 電路取消連結。 
> 
> 

```azurecli
az network express-route peering delete -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePrivatePeering
```

## <a name="azure-public-peering"></a>Azure 公用對等

本節可協助您建立、 取得、 更新和刪除 hello Azure ExpressRoute 循環的公用對等設定。

### <a name="toocreate-azure-public-peering"></a>toocreate Azure 公用對等互連

1. 安裝 Azure CLI hello 最新版本。 您必須使用 hello hello Azure 命令列介面 (CLI) 最新版本。 * 檢閱 hello[必要條件](expressroute-prerequisites.md)和[工作流程](expressroute-workflows.md)開始設定之前。

  ```azurecli
  az login
  ```

  選取您想要的 toocreate ExpressRoute 電路的 hello 訂用帳戶。

  ```azurecli
  az account set --subscription "<subscription ID>"
  ```
2. 建立 ExpressRoute 線路。  請遵循 hello 指示 toocreate [ExpressRoute 電路](howto-circuit-cli.md)，並讓它佈建的 hello 連線服務提供者。

  如果您的連線提供者是提供受管理的第 3 層服務，您可以要求連線提供者為您啟用 Azure 私用對等互連。 在此情況下，您不需要 toofollow hello 下一節中所列的指示。 不過，如果您連線服務提供者不會管理路由，在建立您的循環之後繼續您 hello 後續步驟的組態。
3. 請檢查已佈建並也啟用 hello ExpressRoute 電路 tooensure。 下列範例使用 hello:

  ```azurecli
  az network express-route list
  ```

  hello 回應是類似 toohello 下列範例：

  ```azurecli
  "allowClassicOperations": false,
  "authorizations": [],
  "circuitProvisioningState": "Enabled",
  "etag": "W/\"1262c492-ffef-4a63-95a8-a6002736b8c4\"",
  "gatewayManagerEtag": null,
  "id": "/subscriptions/81ab786c-56eb-4a4d-bb5f-f60329772466/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit",
  "location": "westus",
  "name": "MyCircuit",
  "peerings": [],
  "provisioningState": "Succeeded",
  "resourceGroup": "ExpressRouteResourceGroup",
  "serviceKey": "1d05cf70-1db5-419f-ad86-1ca62c3c125b",
  "serviceProviderNotes": null,
  "serviceProviderProperties": {
    "bandwidthInMbps": 200,
    "peeringLocation": "Silicon Valley",
    "serviceProviderName": "Equinix"
  },
  "serviceProviderProvisioningState": "Provisioned",
  "sku": {
    "family": "UnlimitedData",
    "name": "Standard_MeteredData",
    "tier": "Standard"
  },
  "tags": null,
  "type": "Microsoft.Network/expressRouteCircuits]
  ```

4. 設定 Azure 公用對等互連 hello 循環。 請確定您擁有 hello 繼續接下來，下列資訊。

  * / 30 子網路 hello 主要連結。 這必須是有效的公用 IPv4 首碼。
  * / 30 hello 次要連結的子網路。 這必須是有效的公用 IPv4 首碼。
  * 有效的 VLAN ID tooestablish 此對等。 請確認沒有其他對等互連中 hello 循環使用 hello 相同 VLAN id。
  * 對等的 AS 編號。 您可以使用 2 位元組和 4 位元組 AS 編號。
  * **選用-**如果您選擇其中一個 toouse 的 MD5 雜湊。

  執行下列範例 tooconfigure Azure 公用對等互連，為您的電路的 hello:

  ```azurecli
  az network express-route peering create --circuit-name MyCircuit --peer-asn 100 --primary-peer-subnet 12.0.0.0/30 -g ExpressRouteResourceGroup --secondary-peer-subnet 12.0.0.4/30 --vlan-id 200 --peering-type AzurePublicPeering
  ```

  如果您選擇 toouse MD5 雜湊時，使用下列範例中的 hello:

  ```azurecli
  az network express-route peering create --circuit-name MyCircuit --peer-asn 100 --primary-peer-subnet 12.0.0.0/30 -g ExpressRouteResourceGroup --secondary-peer-subnet 12.0.0.4/30 --vlan-id 200 --peering-type AzurePublicPeering --SharedKey "A1B2C3D4"
  ```

  > [!IMPORTANT]
  > 請確定您將 AS 編號指定為對等 ASN，而不是客戶 ASN。

### <a name="tooview-azure-public-peering-details"></a>tooview Azure 公用對等互連的詳細資料

就可以使用下列範例中的 hello 設定詳細資料：

```azurecli
az network express-route peering show -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePublicPeering
```

hello 輸出是 toohello 類似下列範例程式碼：

```azurecli
{
  "azureAsn": 12076,
  "etag": "W/\"2e97be83-a684-4f29-bf3c-96191e270666\"",
  "gatewayManagerEtag": "18",
  "id": "/subscriptions/9a0c2943-e0c2-4608-876c-e0ddffd1211b/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit/peerings/AzurePublicPeering",
  "lastModifiedBy": "Customer",
  "microsoftPeeringConfig": null,
  "name": "AzurePublicPeering",
  "peerAsn": 7671,
  "peeringType": "AzurePublicPeering",
  "primaryAzurePort": "",
  "primaryPeerAddressPrefix": "",
  "provisioningState": "Succeeded",
  "resourceGroup": "ExpressRouteResourceGroup",
  "routeFilter": null,
  "secondaryAzurePort": "",
  "secondaryPeerAddressPrefix": "",
  "sharedKey": null,
  "state": "Enabled",
  "stats": null,
  "vlanId": 100
}
```

### <a name="tooupdate-azure-public-peering-configuration"></a>tooupdate Azure 公用對等組態

您可以更新使用下列範例中的 hello hello 設定的任何部分。 在此範例中，從 200 too600 正在更新 hello hello 循環的 VLAN ID。

```azurecli
az network express-route peering update --vlan-id 600 -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePublicPeering
```

### <a name="toodelete-azure-public-peering"></a>toodelete Azure 公用對等互連

您可以執行下列範例中的 hello 來移除您對等的設定：

```azurecli
az network express-route peering delete -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePublicPeering
```

## <a name="microsoft-peering"></a>Microsoft 對等互連

本節可協助您建立、 取得、 更新和刪除 ExpressRoute 循環的 hello Microsoft 對等設定。

> [!IMPORTANT]
> Microsoft 對等互連的 ExpressRoute 電路已設定先前 tooAugust 1，2017年必須透過 hello Microsoft 對等互連，公告的所有服務首碼，即使未定義路由篩選器。 Microsoft 對等互連的當天或之後 2017 年 8 月 1，已設定的 ExpressRoute 電路並不會有任何前置詞通告的路由篩選器連接直到 toohello 循環。 如需詳細資訊，請參閱[設定 Microsoft 對等互連的路由篩選](how-to-routefilter-powershell.md)。
> 
> 

### <a name="toocreate-microsoft-peering"></a>toocreate Microsoft 對等互連

1. 安裝 Azure CLI hello 最新版本。 使用 hello 最新版本的 hello Azure 命令列介面 (CLI)。 * 檢閱 hello[必要條件](expressroute-prerequisites.md)和[工作流程](expressroute-workflows.md)開始設定之前。

  ```azurecli
  az login
  ```

  選取您想要的 toocreate ExpressRoute 電路的 hello 訂用帳戶。

  ```azurecli
  az account set --subscription "<subscription ID>"
  ```
2. 建立 ExpressRoute 線路。 請遵循 hello 指示 toocreate [ExpressRoute 電路](howto-circuit-cli.md)，並讓它佈建的 hello 連線服務提供者。

  如果您連線服務提供者提供受管理的第 3 層服務，您可以要求您連線提供者 tooenable 私用對等互連，為您的 Azure。 在此情況下，您不需要 toofollow hello 下一節中所列的指示。 不過，如果您連線服務提供者不會管理路由，在建立您的循環之後繼續您 hello 後續步驟的組態。

3. 請檢查 hello ExpressRoute 電路 toomake 確定佈建，而且也已啟用。 下列範例使用 hello:

  ```azurecli
  az network express-route list
  ```

  hello 回應是類似 toohello 下列範例：

  ```azurecli
  "allowClassicOperations": false,
  "authorizations": [],
  "circuitProvisioningState": "Enabled",
  "etag": "W/\"1262c492-ffef-4a63-95a8-a6002736b8c4\"",
  "gatewayManagerEtag": null,
  "id": "/subscriptions/81ab786c-56eb-4a4d-bb5f-f60329772466/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit",
  "location": "westus",
  "name": "MyCircuit",
  "peerings": [],
  "provisioningState": "Succeeded",
  "resourceGroup": "ExpressRouteResourceGroup",
  "serviceKey": "1d05cf70-1db5-419f-ad86-1ca62c3c125b",
  "serviceProviderNotes": null,
  "serviceProviderProperties": {
    "bandwidthInMbps": 200,
    "peeringLocation": "Silicon Valley",
    "serviceProviderName": "Equinix"
  },
  "serviceProviderProvisioningState": "Provisioned",
  "sku": {
    "family": "UnlimitedData",
    "name": "Standard_MeteredData",
    "tier": "Standard"
  },
  "tags": null,
  "type": "Microsoft.Network/expressRouteCircuits]
  ```

4. 設定 Microsoft 對等互連 hello 循環。 請確定您擁有 hello 下列資訊才能繼續。

  * / 30 子網路 hello 主要連結。 這必須是您所擁有且註冊在 RIR / IRR 中的有效公用 IPv4 首碼。
  * / 30 hello 次要連結的子網路。 這必須是您所擁有且註冊在 RIR / IRR 中的有效公用 IPv4 首碼。
  * 有效的 VLAN ID tooestablish 此對等。 請確認沒有其他對等互連中 hello 循環使用 hello 相同 VLAN id。
  * 對等的 AS 編號。 您可以使用 2 位元組和 4 位元組 AS 編號。
  * 通告前置詞： 您必須提供清單的所有前置詞您計劃 tooadvertise 透過 hello BGP 工作階段。 只接受公用 IP 位址首碼。 如果您計劃 toosend 一組前置詞，您可以傳送的逗號分隔清單。 這些前置詞必須是已註冊的 tooyou 在 RIR / IRR。
  * **選用-**客戶 ASN： 如果您不是數字的已註冊的 toohello 對等互連的廣告前置詞，您可以指定 hello 為其所註冊的數字 toowhich。
  * 路由登錄名稱： 您可以指定 hello RIR / IRR 哪些 hello 做為數字，但前置詞會註冊。
  * **選用-**如果您選擇其中一個 toouse 的 MD5 雜湊。

   下列範例 tooconfigure Microsoft 對等互連您循環執行的 hello:

  ```azurecli
  az network express-route peering create --circuit-name MyCircuit --peer-asn 100 --primary-peer-subnet 123.0.0.0/30 -g ExpressRouteResourceGroup --secondary-peer-subnet 123.0.0.4/30 --vlan-id 300 --peering-type MicrosoftPeering --advertised-public-prefixes 123.1.0.0/24
  ```

### <a name="tooget-microsoft-peering-details"></a>tooget Microsoft 對等詳細資料

您可以使用下列範例中的 hello，以取得設定的詳細資訊：

```azurecli
az network express-route peering show -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzureMicrosoftPeering
```

hello 輸出是 toohello 類似下列範例程式碼：

```azurecli
{
  "azureAsn": 12076,
  "etag": "W/\"2e97be83-a684-4f29-bf3c-96191e270666\"",
  "gatewayManagerEtag": "18",
  "id": "/subscriptions/9a0c2943-e0c2-4608-876c-e0ddffd1211b/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit/peerings/AzureMicrosoftPeering",
  "lastModifiedBy": "Customer",
  "microsoftPeeringConfig": {
    "advertisedPublicPrefixes": [
        ""
      ],
     "advertisedPublicPrefixesState": "",
     "customerASN": ,
     "routingRegistryName": ""
  }
  "name": "AzureMicrosoftPeering",
  "peerAsn": ,
  "peeringType": "AzureMicrosoftPeering",
  "primaryAzurePort": "",
  "primaryPeerAddressPrefix": "",
  "provisioningState": "Succeeded",
  "resourceGroup": "ExpressRouteResourceGroup",
  "routeFilter": null,
  "secondaryAzurePort": "",
  "secondaryPeerAddressPrefix": "",
  "sharedKey": null,
  "state": "Enabled",
  "stats": null,
  "vlanId": 100
}
```

### <a name="tooupdate-microsoft-peering-configuration"></a>tooupdate Microsoft 對等組態

您可以更新 hello 設定的任何部分。 hello 公告 hello 循環的前置詞正在更新從 123.1.0.0/24 too124.1.0.0/24 hello 下列範例中：

```azurecli
az network express-route peering update --circuit-name MyCircuit -g ExpressRouteResourceGroup --peering-type MicrosoftPeering --advertised-public-prefixes 124.1.0.0/24
```

### <a name="toodelete-microsoft-peering"></a>toodelete Microsoft 對等互連

您可以執行下列範例中的 hello 來移除您對等的設定：

```azurecli
az network express-route peering delete -g ExpressRouteResourceGroup --circuit-name MyCircuit --name MicrosoftPeering
```

## <a name="next-steps"></a>後續步驟

下一步，[連結 VNet tooan ExpressRoute 電路](howto-linkvnet-cli.md)。

* 如需 ExpressRoute 工作流程的詳細資訊，請參閱 [ExpressRoute 工作流程](expressroute-workflows.md)。
* 如需線路對等的詳細資訊，請參閱 [ExpressRoute 線路和路由網域](expressroute-circuit-peerings.md)。
* 如需使用虛擬網路的詳細資訊，請參閱 [虛擬網路概觀](../virtual-network/virtual-networks-overview.md)。