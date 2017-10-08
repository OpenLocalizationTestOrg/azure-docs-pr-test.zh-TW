---
title: "aaaFind 與 Azure 網路監看員下一個躍點-Azure CLI 1.0 的下一個躍點 |Microsoft 文件"
description: "本文將說明如何尋找哪些 hello 下個躍點類型會與 ip 位址使用下個躍點使用 Azure CLI。"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 0700c274-3e0d-4dca-acfa-3ceac8990613
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 54124c051021413695d70ba93c370605abc6ebbe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="find-out-what-hello-next-hop-type-is-using-hello-next-hop-capability-in-azure-network-watcher-using-azure-cli-10"></a>找出 hello 下一個躍點類型會使用 Azure 網路監看員使用 Azure CLI 1.0 中的 hello 下一個躍點功能

> [!div class="op_single_selector"]
> - [Azure 入口網站](network-watcher-check-next-hop-portal.md)
> - [PowerShell](network-watcher-check-next-hop-powershell.md)
> - [CLI 1.0](network-watcher-check-next-hop-cli-nodejs.md)
> - [CLI 2.0](network-watcher-check-next-hop-cli.md)
> - [Azure REST API](network-watcher-check-next-hop-rest.md)

下一個躍點是網路監看員提供 hello 功能的一項功能取得下一個躍點類型 hello 和根據指定的虛擬機器的 IP 位址。 這項功能可用於判斷如果離開虛擬機器的流量會周遊閘道、 網際網路或虛擬網路 tooget tooits 目的地。

本文使用跨平台 Azure CLI 1.0，這適用於 Windows、Mac 和 Linux。

## <a name="before-you-begin"></a>開始之前

在此案例中，您將使用 hello Azure CLI toofind hello 下一個躍點類型和 IP 位址。

此案例假設您已依照中的 hello 步驟[建立網路監看員](network-watcher-create.md)toocreate 網路監看員。 hello 案例也會假設具有有效的虛擬機器的資源群組存在 toobe 使用。

## <a name="scenario"></a>案例

在此文章所涵蓋的 hello 案例使用下一個躍點，會找出 hello 下一個躍點類型和資源的 IP 位址的網路監看員的一項功能。 toolearn 深入了解下個躍點，請瀏覽[下一個躍點概觀](network-watcher-next-hop-overview.md)。


## <a name="get-next-hop"></a>取得下一個躍點

tooget hello 下一個躍點，我們會呼叫 hello `azure netowrk watcher next-hop` cmdlet。 我們會傳送 hello cmdlet hello 網路監看員資源群組、 hello NetworkWatcher、 虛擬機器識別碼、 來源 IP 位址和目的地 IP 位址。 在此範例中，hello 目的地 IP 位址會是 tooa VM，另一個虛擬網路中。 Hello 兩個虛擬網路之間沒有虛擬網路閘道。 

```azurecli
azure network watcher next-hop -g resourceGroupName -n networkWatcherName -t targetResourceId -a <source-ip> -d <destination-ip>
```

> [!NOTE]
如果 hello VM 有多個 Nic 和任何 hello Nic 上啟用 IP 轉送，然後 hello NIC 參數 (-我 nic 識別碼)，必須指定。 否則為選擇性。

## <a name="review-results"></a>檢閱結果

完成時，會提供 hello 結果。 它是的資源 hello 類型以及傳回 hello 下一個躍點 IP 位址。

```
data:    Next Hop Ip Address             : 10.0.1.2
info:    network watcher next-hop command OK
```

hello 下列清單顯示目前可用 NextHopType 值 hello:

**下一個躍點類型**

* Internet
* VirtualAppliance
* VirtualNetworkGateway
* VnetLocal
* HyperNetGateway
* VnetPeering
* None

## <a name="next-steps"></a>後續步驟

深入了解如何 tooreview 您的網路安全性群組設定，以程式設計方式造訪[NSG 稽核與網路監看員](network-watcher-nsg-auditing-powershell.md)
