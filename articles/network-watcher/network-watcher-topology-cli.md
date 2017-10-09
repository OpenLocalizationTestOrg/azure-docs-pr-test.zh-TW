---
title: "aaaView Azure 網路監看員拓樸-Azure CLI |Microsoft 文件"
description: "本文將說明如何 toouse Azure CLI tooquery 網路拓撲。"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 5cd279d7-3ab0-4813-aaa4-6a648bf74e7b
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: afa7e7dd844ecb2ab4c616ba99fa0a433f1e4ade
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="view-network-watcher-topology-with-azure-cli"></a>使用 Azure CLI 檢視網路監看員拓撲

> [!div class="op_single_selector"]
> - [PowerShell](network-watcher-topology-powershell.md)
> - [CLI 1.0](network-watcher-topology-cli-nodejs.md)
> - [CLI 2.0](network-watcher-topology-cli.md)
> - [REST API](network-watcher-topology-rest.md)

網路監看員 hello 拓撲功能提供的訂用帳戶中的 hello 網路資源的視覺表示法。 在 hello 入口網站，此視覺效果會自動顯示 tooyou。 hello 入口網站中的 hello 拓撲檢視背後的 hello 資訊可以透過 PowerShell 來擷取。
這項功能可讓您更多功能，如 hello 資料可供出 hello 視覺效果的其他工具 toobuild hello 拓撲資訊。

本文使用跨平台 Azure CLI 1.0，這適用於 Windows、Mac 和 Linux。 網路監看員目前使用 Azure CLI 1.0 提供 CLI 支援。

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

在此案例中，您可以使用 hello `network watcher topology` cmdlet tooretrieve hello 拓撲資訊。 另外還有發行項上如何太[擷取使用 REST API 的網路拓樸](network-watcher-topology-rest.md)。

此案例假設您已依照中的 hello 步驟[建立網路監看員](network-watcher-create.md)toocreate 網路監看員。

## <a name="scenario"></a>案例

hello 案例涵蓋在本文中擷取指定的資源群組的 hello 拓撲回應。

## <a name="retrieve-topology"></a>擷取拓撲

hello`network watcher topology`指令程式會擷取指定的資源群組的 hello 拓撲。 加入 hello 引數 」-json"tooview hello oput json 格式

```azurecli
azure network watcher topology -g resourceGroupName -n networkWatcherName -r topologyResourceGroupName --json
```

## <a name="results"></a>結果

hello 傳回的結果具有的屬性名稱 「 資源 」，其中包含 hello hello json 回應主體`network watcher topology`cmdlet。  hello 回應包含 hello 網路安全性群組與它們關聯 （也就是包含、 相關聯） 中的 hello 資源。

```json
{
  "id": "00000000-0000-0000-0000-000000000000",
  "createdDateTime": "2017-02-17T22:20:59.461Z",
  "lastModified": "2016-12-19T22:23:02.546Z",
  "resources": [
    {
      "name": "testrg-vnet",
      "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/testrg-vnet",
      "location": "westcentralus",
      "associations": [
        {
          "name": "default",
          "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/testrg-vnet/subnets/default",
          "associationType": "Contains"
        }
      ]
    },
    {
      "name": "default",
      "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/testrg-vnet/subnets/default",
      "location": "westcentralus",
      "associations": []
    },
    {
      "name": "testclient",
      "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Compute/virtualMachines/testclient",
      "location": "westcentralus",
      "associations": [
        {
          "name": "testNic",
          "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/networkInterfaces/testNic",
          "associationType": "Contains"
        }
      ]
    },
    ...    
  ]
}
```

## <a name="next-steps"></a>後續步驟

深入了解 hello 安全性規則所套用的 tooyour 網路資源，造訪[安全性的群組檢視概觀](network-watcher-security-group-view-overview.md)
