---
title: "aaaCreate Azure 網路監看員執行個體 |Microsoft 文件"
description: "本頁面提供的 hello 步驟 toocreate 網路監看員的執行個體使用 hello 入口網站和 Azure REST API"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: b1314119-0b87-4f4d-b44c-2c4d0547fb76
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 90d4f90c9709a80e4b27863e79e5b6e16de145c7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-network-watcher-instance"></a>建立 Azure 網路監看員執行個體

網路監看員是地區和服務，可讓您 toomonitor 診斷層級網路案例中，，然後從 Azure 的情況。 案例層級的監視可讓您在結束 tooend 網路層級檢視 toodiagnose 問題。 網路診斷和使用網路監看員的視覺化工具，可協助您了解、 診斷，以及取得 Azure insights tooyour 網路。

> [!NOTE]
> 因為網路監看員時，目前只支援 CLI 1.0，hello 指示 toocreate 的新網路監看員執行個體提供 CLI 1.0。

## <a name="create-a-network-watcher-in-hello-portal"></a>在 hello 入口網站中建立網路監看員

瀏覽過**更服務** > **網路** > **網路監看員**。 您可以選取所有您想 tooenable 網路監看員的 hello 訂閱的。 此動作會在每個可用區域建立網路監看員。

![建立網路監看員][1]

當您啟用網路監看員使用 hello 入口網站時，hello hello 網路監看員執行個體名稱將會自動設定 tooNetworkWatcher_region_name region_name 其中對應 toohello hello 執行個體已啟用的 Azure 區域。  例如，在美國中西部區域啟用的網路監看員，名稱將會是 NetworkWatcher_westcentralus

此外，會自動加入 hello 網路監看員執行個體，稱為 NetworkWatcherRG 的資源群組。  如果該資源群組不存在，系統將會建立它。

如果您想將網路監看員執行個體和 hello toocustomize hello 名稱就放到的資源群組，您可以使用 Powershell、 REST API hello 或 ARMClient 如下所述的方法。  在每個選項中，hello 資源群組必須先放置到其中的 hello 網路監看員。  

## <a name="create-a-network-watcher-with-powershell"></a>使用 PowerShell 建立網路監看員

toocreate 網路監看員，執行下列範例中的 hello 的執行個體：

```powershell
New-AzureRmNetworkWatcher -Name "NetworkWatcher_westcentralus" -ResourceGroupName "NetworkWatcherRG" -Location "West Central US"
```

## <a name="create-a-network-watcher-with-hello-rest-api"></a>以 hello REST API 建立網路監看員

ARMclient 是使用 PowerShell 的使用的 toocall hello REST API。 您可以在 chocolatey 的 [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient) 上找到 ARMClient

### <a name="log-in-with-armclient"></a>使用 ARMClient 登入

```powerShell
armclient login
```

### <a name="create-hello-network-watcher"></a>建立 hello 網路監看員

```powershell
$subscriptionId = '<subscription id>'
$networkWatcherName = '<name of network watcher>'
$resourceGroupName = '<resource group name>'
$apiversion = "2016-09-01"
$requestBody = @"
{
'location': 'West Central US'
}
"@

armclient put "https://management.azure.com/subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}?api-version=${api-version}" $requestBody
```

## <a name="next-steps"></a>後續步驟

現在，您有網路監看員的執行個體，深入了解可用的 hello 功能：

* [拓撲](network-watcher-topology-overview.md)
* [封包擷取](network-watcher-packet-capture-overview.md)
* [IP 流量驗證](network-watcher-ip-flow-verify-overview.md)
* [下一個躍點](network-watcher-next-hop-overview.md)
* [安全性群組檢視](network-watcher-security-group-view-overview.md)
* [NSG 流量記錄](network-watcher-nsg-flow-logging-overview.md)
* [虛擬網路閘道疑難排解](network-watcher-troubleshoot-overview.md)

一旦建立網路監看員執行個體之後，可以設定下列 hello 文章封裝擷取：[建立警示觸發的封包擷取](network-watcher-alert-triggered-packet-capture.md)

[1]: ./media/network-watcher-create/figure1.png











