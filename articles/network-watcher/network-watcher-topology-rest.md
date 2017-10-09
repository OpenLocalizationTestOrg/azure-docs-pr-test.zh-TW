---
title: "aaaView Azure 網路監看員拓樸-REST API |Microsoft 文件"
description: "本文將說明如何 toouse 會 REST API tooquery 網路拓撲。"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: de9af643-aea1-4c4c-89c5-21f1bf334c06
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 39292025bcd561f007c9e31271b1389be48ea79f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="view-network-watcher-topology-with-rest-api"></a>使用 REST API 檢視網路監看員拓撲

> [!div class="op_single_selector"]
> - [PowerShell](network-watcher-topology-powershell.md)
> - [CLI 1.0](network-watcher-topology-cli-nodejs.md)
> - [CLI 2.0](network-watcher-topology-cli.md)
> - [REST API](network-watcher-topology-rest.md)

網路監看員 hello 拓撲功能提供的訂用帳戶中的 hello 網路資源的視覺表示法。 在 hello 入口網站，此視覺效果會自動顯示 tooyou。 hello 入口網站中的 hello 拓撲檢視背後的 hello 資訊可以透過 PowerShell 來擷取。
這項功能可讓您更多功能，如 hello 資料可供出 hello 視覺效果的其他工具 toobuild hello 拓撲資訊。

hello 互連的方式是在兩個關聯性模型化。

- **內含項目** - 範例︰VNet 包含子網路包含 NIC
- **相關聯** - 範例︰NIC 與 VM 相關聯

hello 下列清單會查詢 hello 拓撲 REST API 時所傳回的屬性。

* **名稱**-hello hello 資源的名稱
* **識別碼**-hello hello 資源的 uri。
* **位置**-hello hello 資源所在的位置。
* **關聯**-一份關聯 toohello 參考物件。
    * **名稱**-hello hello 名稱所參考的資源。
    * **resourceId** -hello resourceId 為 hello 參考 hello 關聯中的 hello 資源 uri。
    * **associationType** -這個值會參考 hello hello 子物件 hello 父系之間的關聯性。 有效值為 [包含] 或 [相關聯]。

## <a name="before-you-begin"></a>開始之前

在此案例中，您可以擷取 hello 拓撲資訊。 ARMclient 是使用 PowerShell 的使用的 toocall hello REST API。 您可以在 chocolatey 的 [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient) 上找到 ARMClient

此案例假設您已依照中的 hello 步驟[建立網路監看員](network-watcher-create.md)toocreate 網路監看員。

## <a name="scenario"></a>案例

hello 案例涵蓋在本文中擷取指定的資源群組的 hello 拓撲回應。

## <a name="log-in-with-armclient"></a>使用 ARMClient 登入

登入 tooarmclient 與您的 Azure 認證。

```PowerShell
armclient login
```

## <a name="retrieve-topology"></a>擷取拓撲

hello hello REST API 中的下列範例要求 hello 拓撲。  hello 範例是參數化的 tooallow 為建立範例的彈性。  以它們周圍的 \< \> 取代所有值。

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "<resource group name>" # Resource group name toorun topology on
$NWresourceGroupName = "<resource group name>" # Network Watcher resource group name
$networkWatcherName = "<network watcher name>"
$requestBody = @"
{
    'targetResourceGroupName': '${resourceGroupName}'
}
"@

armclient POST "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${NWresourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/topology?api-version=2016-07-01" $requestBody
```

下列回應 hello 是縮短回應時，會傳回的範例擷取的資源群組拓撲：

```json
{
  "id": "ecd6c860-9cf5-411a-bdba-512f8df7799f",
  "createdDateTime": "2017-01-18T04:13:07.1974591Z",
  "lastModified": "2017-01-17T22:11:52.3527348Z",
  "resources": [
    {
      "name": "virtualNetwork1",
      "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/virtualNetworks/{virtualNetworkName}",
      "location": "westcentralus",
      "associations": [
        {
          "name": "{subnetName}",
          "resourceId": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/virtualNetworks/(virtualNetworkName)/subnets
/{subnetName}",
          "associationType": "Contains"
        }
      ]
    },
    {
      "name": "webtestnsg-wjplxls65qcto",
      "resourceId": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkSecurityGroups/{nsgName}
s65qcto",
      "associationType": "Associated"
    },
    ...
  ]
}
```

## <a name="next-steps"></a>後續步驟

了解 toovisualize NSG 流程記錄的方式有了 Power BI 瀏覽[視覺化 NSG 流動 Power BI 的記錄檔](network-watcher-visualize-nsg-flow-logs-power-bi.md)

