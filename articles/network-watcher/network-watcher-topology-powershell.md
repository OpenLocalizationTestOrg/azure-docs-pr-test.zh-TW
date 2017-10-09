---
title: "aaaView Azure 網路監看員拓樸-PowerShell |Microsoft 文件"
description: "本文將說明如何 toouse PowerShell tooquery 網路拓撲。"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: bd0e882d-8011-45e8-a7ce-de231a69fb85
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 2bc0ecf5baa81a68be53f55c74f362a7bc97116f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="view-network-watcher-topology-with-powershell"></a>使用 PowerShell 檢視網路監看員拓撲

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

在此案例中，您可以使用 hello `Get-AzureRmNetworkWatcherTopology` cmdlet tooretrieve hello 拓撲資訊。 另外還有發行項上如何太[擷取使用 REST API 的網路拓樸](network-watcher-topology-rest.md)。

此案例假設您已依照中的 hello 步驟[建立網路監看員](network-watcher-create.md)toocreate 網路監看員。

## <a name="scenario"></a>案例

hello 案例涵蓋在本文中擷取指定的資源群組的 hello 拓撲回應。

## <a name="retrieve-network-watcher"></a>擷取網路監看員

hello 第一個步驟是 tooretrieve hello 網路監看員執行個體。 hello`$networkWatcher`變數傳遞 toohello `Get-AzureRmNetworkWatcherTopology` cmdlet。

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" }
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName
```

## <a name="retrieve-topology"></a>擷取拓撲

hello`Get-AzureRmNetworkWatcherTopology`指令程式會擷取指定的資源群組的 hello 拓撲。

```powershell
Get-AzureRmNetworkWatcherTopology -NetworkWatcher $networkWatcher -TargetResourceGroupName testrg
```

## <a name="results"></a>結果

hello 傳回的結果具有的屬性名稱 「 資源 」，其中包含 hello hello json 回應主體`Get-AzureRmNetworkWatcherTopology`cmdlet。  hello 回應包含 hello 網路安全性群組與它們關聯 （也就是包含、 相關聯） 中的 hello 資源。

```json
Id              : 00000000-0000-0000-0000-000000000000
CreatedDateTime : 2/1/2017 7:52:21 PM
LastModified    : 2/1/2017 7:46:18 PM
Resources       : [
                    {
                      "Name": "testrg-vnet",
                      "Id":
                  "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/testrg-vnet",
                      "Location": "westcentralus",
                      "Associations": [
                        {
                          "AssociationType": "Contains",
                          "Name": "default",
                          "ResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNe
                  tworks/testrg-vnet/subnets/default"
                        }
                      ]
                    },
                    {
                      "Name": "default",
                      "Id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/testr
                  g-vnet/subnets/default",
                      "Location": "westcentralus",
                      "Associations": []
                    },
                    {
                      "Name": "testrg-vnet2",
                      "Id": 
                  "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/testrg-vnet2",
                      "Location": "westcentralus",
                      "Associations": [
                        {
                          "AssociationType": "Contains",
                          "Name": "default",
                          "ResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNe
                  tworks/testrg-vnet2/subnets/default"
                        },
                        {
                          "AssociationType": "Contains",
                          "Name": "GatewaySubnet",
                          "ResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNe
                  tworks/testrg-vnet2/subnets/GatewaySubnet"
                        },
                        {
                          "AssociationType": "Contains",
                          "Name": "gateway2",
                          "ResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNe
                  tworkGateways/gateway2"
                        }
                      ]
                    },
                    ...
                  ]
```

## <a name="next-steps"></a>後續步驟

了解 toovisualize NSG 流程記錄的方式有了 Power BI 瀏覽[視覺化 NSG 流動 Power BI 的記錄檔](network-watcher-visualize-nsg-flow-logs-power-bi.md)


