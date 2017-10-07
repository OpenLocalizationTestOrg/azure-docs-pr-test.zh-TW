---
title: "與 Azure 網路監看員下個躍點-REST 下個躍點 aaaFind |Microsoft 文件"
description: "本文將說明如何尋找哪些 hello 下個躍點類型，且使用下一個躍點使用的 ip 位址 hello Azure REST API"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 2216c059-45ba-4214-8304-e56769b779a6
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: a2b61b355aae8ae513ebd44837184fbc6cfd668c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="find-out-what-hello-next-hop-type-is-using-hello-next-hop-capability-in-aure-network-watcher-using-azure-rest-api"></a>找出 hello 下一個躍點類型會使用 Aure 網路監看員使用 Azure REST API 中的 hello 下一個躍點功能

> [!div class="op_single_selector"]
> - [Azure 入口網站](network-watcher-check-next-hop-portal.md)
> - [PowerShell](network-watcher-check-next-hop-powershell.md)
> - [CLI 1.0](network-watcher-check-next-hop-cli-nodejs.md)
> - [CLI 2.0](network-watcher-check-next-hop-cli.md)
> - [Azure REST API](network-watcher-check-next-hop-rest.md)

下一個躍點是網路監看員提供 hello 功能的一項功能取得下一個躍點類型 hello 和根據指定的虛擬機器的 IP 位址。 這項功能可用於判斷如果離開虛擬機器的流量會周遊閘道、 網際網路或虛擬網路 tooget tooits 目的地。

## <a name="before-you-begin"></a>開始之前

ARMclient 是使用 PowerShell 的使用的 toocall hello REST API。 您可以在 chocolatey 的 [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient) 上找到 ARMClient

此案例假設您已依照中的 hello 步驟[建立網路監看員](network-watcher-create.md)toocreate 網路監看員。

## <a name="scenario"></a>案例

在此文章所涵蓋的 hello 案例使用下一個躍點，會找出 hello 下一個躍點類型和資源的 IP 位址的網路監看員的一項功能。 toolearn 深入了解下個躍點，請瀏覽[下一個躍點概觀](network-watcher-next-hop-overview.md)。

在此案例中，您將會：

* 擷取虛擬機器的 hello 下一個躍點。

## <a name="log-in-with-armclient"></a>使用 ARMClient 登入

登入 tooarmclient 與您的 Azure 認證。

```PowerShell
armclient login
```

## <a name="retrieve-a-virtual-machine"></a>擷取虛擬機器

執行下列指令碼 tooreturn hello 虛擬機器。 執行下一個躍點需要這項資訊。

下列程式碼的 hello hello 下列變數需要值：

- **subscriptionId** -hello 訂用帳戶 Id toouse。
- **resourceGroupName** -hello 包含虛擬機器的資源群組的名稱。

```powershell
$subscriptionId = '<subscription id>'
$resourceGroupName = '<resource group name>'

armclient get https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Compute/virtualMachines?api-version=2015-05-01-preview
```

從 hello 下列輸出，hello hello 虛擬機器識別碼 hello 下列範例中使用：

```json
...
,
      "type": "Microsoft.Compute/virtualMachines",
      "location": "westcentralus",
      "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoExampleRG/providers/Microsoft.Compute
/virtualMachines/ContosoVM",
      "name": "ContosoVM"
    }
  ]
}
```

## <a name="get-next-hop"></a>取得下一個躍點

一旦建立 hello 授權標頭，就可以擷取 hello 從虛擬機器的下一個躍點。 hello 下列的值必須取代的 hello 程式碼範例 toowork。

> [!Important]
> 網路監看員 REST api 呼叫 hello hello 要求 URI 是 hello 包含 hello 網路監看員，您執行的 hello 診斷動作不 hello 資源的資源群組中的資源群組名稱。

```powershell
$sourceIP = "10.0.0.4"
$destinationIP = "8.8.8.8"
$resourceGroupName = <resource group name>
$requestBody = @"
{
    'targetResourceId': '${targetUri}',
    'sourceIpAddress': '${sourceIP}',
    'destinationIpAddress': '${destinationIP}',
    'targetNicResourceId' : '${targetNic}'
}
"@

armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/nextHop?api-version=2016-12-01" $requestBody
```

> [!NOTE]
> 下一個躍點需要 hello VM 資源配置 toorun。

## <a name="results"></a>結果

hello 下列程式碼片段是收到 hello 輸出的範例。 hello 結果包含下列值的 hello:

* **nextHopType** -這個值可以是下列值的 hello 的其中一個： 網際網路、 VirtualAppliance、 VirtualNetworkGateway、 VnetLocal、 HyperNetGateway，或 None。
* **nextHopIpAddress** -hello hello 下一個躍點 IP 位址。
* **routeTableId** -hello 值為 hello 與 hello 路由相關聯的路由表的 uri，或如果不是使用者定義路由是定義的 hello 值*系統路由*傳回。

hello 以下是 json 格式的 hello 結果。

```json
{
  "nextHopType": "Internet",
  "routeTableId": "System Route"
}
```

## <a name="next-steps"></a>後續步驟

後無法 toofind 出 hello 虛擬機器的下一個躍點後，您可以檢視您的網路資源的 hello 安全性造訪[安全性檢視概觀](network-watcher-security-group-view-overview.md)














