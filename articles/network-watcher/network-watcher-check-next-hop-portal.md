---
title: "aaaFind 下一個躍點與 Azure 網路監看員下一個躍點-Azure 入口網站 |Microsoft 文件"
description: "本文將說明如何尋找哪些 hello 下個躍點類型，且使用下一個躍點使用的 ip 位址 hello Azure 入口網站"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 7b459dcf-4077-424e-a774-f7bfa34c5975
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: b64a2a5275c15aa8bdb10601de4ae1504a9ab551
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="find-out-what-hello-next-hop-type-is-using-hello-next-hop-capability-in-azure-network-watcher-using-hello-portal"></a>找出 hello 下一個躍點類型會使用 Azure 網路監看員使用 hello 入口網站中的 hello 下一個躍點功能

> [!div class="op_single_selector"]
> - [Azure 入口網站](network-watcher-check-next-hop-portal.md)
> - [PowerShell](network-watcher-check-next-hop-powershell.md)
> - [CLI 1.0](network-watcher-check-next-hop-cli-nodejs.md)
> - [CLI 2.0](network-watcher-check-next-hop-cli.md)
> - [Azure REST API](network-watcher-check-next-hop-rest.md)

下一個躍點是網路監看員提供 hello 功能的一項功能取得下一個躍點類型 hello 和根據指定的虛擬機器的 IP 位址。 這項功能可用於判斷如果離開虛擬機器的流量會周遊閘道、 網際網路或虛擬網路 tooget tooits 目的地。

## <a name="before-you-begin"></a>開始之前

此案例假設您已依照中的 hello 步驟[建立網路監看員](network-watcher-create.md)toocreate 網路監看員。 hello 案例也會假設具有有效的虛擬機器的資源群組存在 toobe 使用。

## <a name="scenario"></a>案例

涵蓋在本文中的 hello 案例會使用下一個躍點 toofind 出 hello 下一個躍點類型和 IP 位址資源。 toolearn 深入了解下個躍點，請瀏覽[下一個躍點概觀](network-watcher-next-hop-overview.md)。

在此案例中，您將會：

* 從虛擬機器擷取 hello 下一個躍點。

## <a name="get-next-hop"></a>取得下一個躍點

### <a name="step-1"></a>步驟 1

瀏覽 tooyour 網路監看員資源 hello Azure 入口網站中。

### <a name="step-2"></a>步驟 2

按一下**下個躍點**hello 瀏覽窗格中，選取 hello 虛擬機器網路介面，填寫 hello 來源和目的地 IP，然後按一下 hello**下個躍點**] 按鈕。

> [!NOTE]
> 下一個躍點需要 hello VM 資源配置 toorun。

![取得下一個躍點概觀][1]

### <a name="step-3"></a>步驟 3

Hello 工作完成之後，會提供 hello 結果。 hello IP 位址和裝置 hello 下一個躍點的類型時，就會顯示。 hello 下表顯示可用的傳回的值 hello hello 入口網站中。

**下一個躍點類型**

* Internet
* VirtualAppliance
* VirtualNetworkGateway
* VnetLocal
* HyperNetGateway
* VnetPeering
* None

如果自訂的路由使用的 tooroute 這個流量，hello 使用者定義的路由 (UDR) 也會顯示 hello 結果。

![取得下一個躍點結果][2]

## <a name="next-steps"></a>後續步驟

深入了解如何 tooreview 您的網路安全性群組設定，以程式設計方式造訪[NSG 稽核與網路監看員](network-watcher-nsg-auditing-powershell.md)

[1]: ./media/network-watcher-check-next-hop-portal/figure1.png
[2]: ./media/network-watcher-check-next-hop-portal/figure2.png














