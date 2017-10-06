---
title: "建立與修改 Azure ExpressRoute 線路：CLI | Microsoft Docs"
description: "本文說明如何 toocreate，佈建、 驗證、 更新、 刪除和取消佈建使用 CLI 的 ExpressRoute 電路。"
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
ms.date: 07/25/2017
ms.author: anzaman;cherylmc
ms.openlocfilehash: 396e325658a59afadb209bb525cbb59ac775ae6b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-an-expressroute-circuit-using-cli"></a>使用 CLI 建立和修改 ExpressRoute 線路


本文說明如何使用 Azure ExpressRoute 電路 toocreate hello 命令列介面 (CLI)。 本文也會顯示 toocheck hello 狀態如何更新或刪除和取消佈建電路。 如果您想 toouse ExpressRoute 電路以不同的方法 toowork，您可以從下列清單中的 hello 選取 hello 發行項：

> [!div class="op_single_selector"]
> * [Azure 入口網站](expressroute-howto-circuit-portal-resource-manager.md)
> * [PowerShell](expressroute-howto-circuit-arm.md)
> * [Azure CLI](howto-circuit-cli.md)
> * [影片 - Azure 入口網站](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-an-expressroute-circuit)
> * [PowerShell (傳統)](expressroute-howto-circuit-classic.md)
> 

## <a name="before-you-begin"></a>開始之前

* 在開始之前，安裝 hello 最新版本 （2.0 或更新版本） 的 hello CLI 命令。 如需安裝 hello CLI 命令的資訊，請參閱[安裝 Azure CLI 2.0](/cli/azure/install-azure-cli)和[開始使用 Azure CLI 2.0](/cli/azure/get-started-with-azure-cli)。
* 檢閱 hello[必要條件](expressroute-prerequisites.md)和[工作流程](expressroute-workflows.md)開始設定之前。

## <a name="create-and-provision-an-expressroute-circuit"></a>建立和佈建 ExpressRoute 線路

### <a name="1-sign-in-tooyour-azure-account-and-select-your-subscription"></a>1.登入 tooyour Azure 帳戶並選取您的訂用帳戶

toobegin 您的設定，登入 tooyour Azure 帳戶。 使用下列範例 toohelp 您連接的 hello:

```azurecli
az login
```

請檢查 hello hello 帳戶的訂用帳戶。

```azurecli
az account list
```

選取您想要的 toocreate ExpressRoute 電路的 hello 訂用帳戶。

```azurecli
az account set --subscription "<subscription ID>"
```

### <a name="2-get-hello-list-of-supported-providers-locations-and-bandwidths"></a>2.取得支援的提供者、 位置及頻寬 hello 清單

建立 ExpressRoute 電路之前，您需要支援的連線提供者、 位置及頻寬選項的 hello 清單。 hello CLI 命令 'az 網路快速路由清單-服務-提供者' 會傳回此資訊，您將在稍後步驟中使用：

```azurecli
az network express-route list-service-providers
```

hello 回應是類似 toohello 下列範例：

```azurecli
[
  {
    "bandwidthsOffered": [
      {
        "offerName": "50Mbps",
        "valueInMbps": 50
      },
      {
        "offerName": "100Mbps",
        "valueInMbps": 100
      },
      {
        "offerName": "200Mbps",
        "valueInMbps": 200
      },
      {
        "offerName": "500Mbps",
        "valueInMbps": 500
      },
      {
        "offerName": "1Gbps",
        "valueInMbps": 1000
      },
      {
        "offerName": "2Gbps",
        "valueInMbps": 2000
      },
      {
        "offerName": "5Gbps",
        "valueInMbps": 5000
      },
      {
        "offerName": "10Gbps",
        "valueInMbps": 10000
      }
    ],
    "id": "/subscriptions//resourceGroups//providers/Microsoft.Network/expressRouteServiceProviders/",
    "location": null,
    "name": "AARNet",
    "peeringLocations": [
      "Melbourne",
      "Sydney"
    ],
    "provisioningState": "Succeeded",
    "resourceGroup": "",
    "tags": null,
    "type": "Microsoft.Network/expressRouteServiceProviders"
  },
```

如果您連線服務提供者會列出，請檢查 hello 回應 toosee。 請記下的下列資訊，建立電路時，您需要的 hello:

* 名稱
* PeeringLocations
* BandwidthsOffered

您現在準備好 toocreate ExpressRoute 電路。

### <a name="3-create-an-expressroute-circuit"></a>3.建立 ExpressRoute 線路

> [!IMPORTANT]
> ExpressRoute 電路計費 hello 發出服務金鑰的時間。 準備好 tooprovision hello 電路 hello 連線服務提供者時，請執行此作業。
> 
> 

若您還沒有資源群組，您必須在建立 ExpressRoute 線路之前建立一個。 您可以建立資源群組執行下列命令的 hello:

```azurecli
az group create -n ExpressRouteResourceGroup -l "West US"
```

hello 下列範例示範透過在美國矽谷 Equinix toocreate 200 Mbps ExpressRoute 電路的方式。 如果您使用不同的提供者和不同的設定，請在您提出要求時替換成該資訊。 

請確定您指定正確 SKU 層 hello 和 SKU 系列：

* SKU 層會判斷 ExpressRoute 標準或 ExpressRoute 高階附加元件是否啟用。 您可以指定 'Standard' tooget hello 標準 SKU 或 「 高階 」 hello premium 附加元件。
* SKU 系列決定 hello 計費的型別。 您可以指定 [Metereddata] 以採用計量付費數據傳輸方案，選取 [Unlimiteddata] 以採用無限行動數據方案。 您可以變更從 'Metereddata 'too'Unlimiteddata'，但您無法變更 hello 類型從 'Unlimiteddata' too'Metereddata' hello 計費的型別。


ExpressRoute 電路計費 hello 發出服務金鑰的時間。 下列範例中的 hello 是新的服務金鑰的要求：

```azurecli
az network express-route create --bandwidth 200 -n MyCircuit --peering-location "Silicon Valley" -g ExpressRouteResourceGroup --provider "Equinix" -l "West US" --sku-family MeteredData --sku-tier Standard
```

hello 回應包含 hello 服務金鑰。

### <a name="4-list-all-expressroute-circuits"></a>4.列出所有 ExpressRoute 循環

一份您所建立的所有 hello ExpressRoute 電路 tooget 執行 hello 'az 網路快速路由清單' 命令。 您隨時可以使用此命令來擷取此資訊。 toolist 的所有電路，都請呼叫不含任何參數的 hello。

```azurecli
az network express-route list
```

您的服務金鑰已列在 hello *ServiceKey* hello 回應的欄位。

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
"serviceProviderProvisioningState": "NotProvisioned",
"sku": {
  "family": "UnlimitedData",
  "name": "Standard_MeteredData",
  "tier": "Standard"
},
"tags": null,
"type": "Microsoft.Network/expressRouteCircuits]
```

您可以使用 hello 執行 hello 命令來取得詳細的描述了所有 hello 參數 '-h' 參數。

```azurecli
az network express-route list -h
```

### <a name="5-send-hello-service-key-tooyour-connectivity-provider-for-provisioning"></a>5.佈建傳送嗨服務金鑰 tooyour 連線服務提供者

'ServiceProviderProvisioningState' 提供 hello 的佈建 hello 服務提供者端的目前狀態相關資訊。 hello 狀態提供 hello Microsoft 戶端 hello 狀態。 如需詳細資訊，請參閱 hello[工作流程發行項](expressroute-workflows.md#expressroute-circuit-provisioning-states)。

當您建立新的 ExpressRoute 電路時，hello 循環就會處於下列狀態的 hello:

```azurecli
"serviceProviderProvisioningState": "NotProvisioned"
"circuitProvisioningState": "Enabled"
```

hello 電路變更 toohello hello 連線服務提供者會在您啟用的 hello 程序中時，下列狀態：

```azurecli
"serviceProviderProvisioningState": "Provisioning"
"circuitProvisioningState": "Enabled"
```

您 toobe 無法 toouse ExpressRoute 電路，它必須處於下列狀態的 hello:

```azurecli
"serviceProviderProvisioningState": "Provisioned"
"circuitProvisioningState": "Enabled
```

### <a name="6-periodically-check-hello-status-and-hello-state-of-hello-circuit-key"></a>6.定期檢查 hello 狀態和 hello 循環索引鍵 hello 狀態

檢查 hello 狀態和 hello 循環索引鍵 hello 狀態，可讓您了解您的提供者已啟用您的循環時間。 設定 hello 循環之後，'ServiceProviderProvisioningState' 會顯示為 已佈建' hello 下列範例所示：

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
"serviceProviderProvisioningState": "NotProvisioned",
"sku": {
  "family": "UnlimitedData",
  "name": "Standard_MeteredData",
  "tier": "Standard"
},
"tags": null,
"type": "Microsoft.Network/expressRouteCircuits]
```

### <a name="7-create-your-routing-configuration"></a>7.建立路由組態

如需逐步指示，請參閱 hello [ExpressRoute 電路的路由組態](howto-routing-cli.md)文章 toocreate 和修改循環的對等互連。

> [!IMPORTANT]
> 這些說明僅適用於 toocircuits 與提供層級 2 連線服務的服務提供者所建立。 如果您使用的服務提供者是提供受管理的第 3 層服務 (通常是 IP VPN，如 MPLS)，您的連線提供者會為您設定和管理路由。
> 
> 

### <a name="8-link-a-virtual-network-tooan-expressroute-circuit"></a>8.連結虛擬網路 tooan ExpressRoute 電路

接下來，將虛擬網路 tooyour ExpressRoute 電路的連結。 使用 hello[連結虛擬網路 tooExpressRoute 電路](howto-linkvnet-cli.md)發行項。

## <a name="modify"></a>修改 ExpressRoute 線路

您可以修改 ExpressRoute 線路的某些屬性，而不會影響連線。 您可以進行下列變更，不需停機的 hello:

* 您可以啟用或停用 ExpressRoute 線路的 ExpressRoute 進階附加元件。
* 前提是有容量可用 hello 連接埠上，您可以增加 hello 頻寬的 ExpressRoute 電路。 不過，不支援降級 hello 電路頻寬。 
* 您可以將計量資料 tooUnlimited 資料變更 hello 計量計劃。 不過，變更 hello 計量不受限制的資料 tooMetered 不支援資料從計劃。
* 您可以啟用和停用 [允許傳統作業]。

如需有關限制和限制的詳細資訊，請參閱 hello [ExpressRoute 常見問題集](expressroute-faqs.md)。

### <a name="tooenable-hello-expressroute-premium-add-on"></a>tooenable hello ExpressRoute 高階的附加元件

您可以使用下列命令的 hello，為您現有的電路啟用 hello ExpressRoute premium add-on:

```azurecli
az network express-route update -n MyCircuit -g ExpressRouteResourceGroup --sku-tier Premium
```

現在，hello expressroute 電路都已啟用 hello ExpressRoute premium 附加元件功能。 我們開始 hello 命令已順利執行完成後，只要您計費 hello premium 附加元件的功能。

### <a name="toodisable-hello-expressroute-premium-add-on"></a>toodisable hello ExpressRoute 高階的附加元件

> [!IMPORTANT]
> 如果您使用大於 hello 標準循環所允許的資源，這項作業可能會失敗。
> 
> 

停用之前 hello ExpressRoute premium add-on，了解 hello 下列準則：

* 您從 premium toostandard 降級之前，您必須確定您擁有少於 10 個虛擬網路連結的 toohello 循環。 如果數目大於 10，更新要求就會失敗，且我們會以進階費率計費。
* 您必須取消連結其他地理政治區域中的所有虛擬網路。 如果您未將所有虛擬網路取消連結，更新要求就會失敗，且我們會以進階費率計費。
* 就私用對等設定而言，路由表必須少於 4000 個路由。 如果您的路由表的大小大於 4000 路由，會卸除 hello BGP 工作階段。 hello 工作階段將不會重新啟用，直到 hello 公告的首碼數目，低於 4000。

您可以使用下列範例中的 hello，停用 hello ExpressRoute premium add-on hello 現有循環：

```azurecli
az network express-route update -n MyCircuit -g ExpressRouteResourceGroup --sku-tier Standard
```

### <a name="tooupdate-hello-expressroute-circuit-bandwidth"></a>tooupdate hello ExpressRoute 電路頻寬

您的提供者支援的 hello 頻寬選項，請檢查 hello [ExpressRoute 常見問題集](expressroute-faqs.md)。 您可以挑選任何比您現有的循環 hello 大小更大的大小。

> [!IMPORTANT]
> 如果 hello 現有連接埠上沒有足夠的容量，您可能必須 toorecreate hello ExpressRoute 電路。 如果沒有任何額外的容量可在該位置，您無法升級 hello 循環。
>
> 您無法減少 hello 頻寬的 ExpressRoute 電路不會中斷。 降級頻寬需要您 toodeprovision hello ExpressRoute 電路並再重新佈建新增的 ExpressRoute 電路。
>

決定您需要的 hello 大小之後，請使用下列命令 tooresize hello 您的循環：

```azurecli
az network express-route update -n MyCircuit -g ExpressRouteResourceGroup --bandwidth 1000
```

您的電路會調整大小，Microsoft hello 一邊。 接下來，您必須連絡其端 toomatch 您連接的提供者 tooupdate 設定這項變更。 此通知之後，我們會開始計費您更新的 hello 頻寬選項。

### <a name="toomove-hello-sku-from-metered-toounlimited"></a>從付費 toounlimited toomove hello SKU

您可以使用下列範例中的 hello 變更 hello 的 ExpressRoute 電路 SKU:

```azurecli
az network express-route update -n MyCircuit -g ExpressRouteResourceGroup --sku-family UnlimitedData
```

### <a name="toocontrol-access-toohello-classic-and-resource-manager-environments"></a>toocontrol 存取 toohello 傳統和資源管理員環境

檢閱中的 hello 指示[從 hello 傳統 toohello Resource Manager 部署模型的移動 ExpressRoute 電路](expressroute-howto-move-arm.md)。

## <a name="deprovisioning-and-deleting-an-expressroute-circuit"></a>取消佈建和刪除 ExpressRoute 線路

toodeprovision 和刪除 ExpressRoute 循環，請確定您瞭解下列準則的 hello:

* 您必須取消連結從 hello ExpressRoute 電路的所有虛擬網路。 如果此作業失敗，請檢查 toosee 如果任何虛擬網路連結 toohello 循環。
* 如果 hello ExpressRoute 電路服務提供者佈建狀態為**佈建**或**已佈建**，您必須使用您的服務提供者 toodeprovision hello 電路邊。 我們繼續 tooreserve 資源，並向您收取費用，直到完成取消佈建 hello 電路 hello 服務提供者，並通知我們。
* 如果 hello 服務提供者已解除佈建 hello 循環，您可以刪除 hello 循環。 當電路會解除佈建時，hello 服務提供者佈建狀態會設定太**未佈建**。 這會停止計費 hello 循環。

若要刪除 ExpressRoute 電路，您可以執行下列命令的 hello:

```azurecli
az network express-route delete  -n MyCircuit -g ExpressRouteResourceGroup
```

## <a name="next-steps"></a>後續步驟

建立您的循環之後，請確定您執行下列工作 hello:

* [建立和修改 ExpressRoute 線路的路由](howto-routing-cli.md)
* [連結您的虛擬網路 tooyour ExpressRoute 電路](howto-linkvnet-cli.md)
