---
title: "aaaFind 下一個躍點與 Azure 網路監看員下一個躍點-PowerShell |Microsoft 文件"
description: "本文將說明如何尋找哪些 hello 下個躍點類型會與 ip 位址使用下個躍點使用 PowerShell。"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 6a656c55-17bd-40f1-905d-90659087639c
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: fdb0b4a02d95fc45c103fe952fc1afa095414c18
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="find-out-what-hello-next-hop-type-is-using-hello-next-hop-capability-in-azure-network-watcher-using-powershell"></a>找出 hello 下一個躍點類型會使用 Azure 網路監看員使用 PowerShell 中的 hello 下一個躍點功能

> [!div class="op_single_selector"]
> - [Azure 入口網站](network-watcher-check-next-hop-portal.md)
> - [PowerShell](network-watcher-check-next-hop-powershell.md)
> - [CLI 1.0](network-watcher-check-next-hop-cli-nodejs.md)
> - [CLI 2.0](network-watcher-check-next-hop-cli.md)
> - [Azure REST API](network-watcher-check-next-hop-rest.md)

下一個躍點是網路監看員提供 hello 功能的一項功能取得下一個躍點類型 hello 和根據指定的虛擬機器的 IP 位址。 這項功能可用於判斷如果離開虛擬機器的流量會周遊閘道、 網際網路或虛擬網路 tooget tooits 目的地。

## <a name="before-you-begin"></a>開始之前

在此案例中，您將使用 hello Azure 入口網站 toofind hello 下一個躍點類型和 IP 位址。

此案例假設您已依照中的 hello 步驟[建立網路監看員](network-watcher-create.md)toocreate 網路監看員。 hello 案例也會假設具有有效的虛擬機器的資源群組存在 toobe 使用。

## <a name="scenario"></a>案例

在此文章所涵蓋的 hello 案例使用下一個躍點，會找出 hello 下一個躍點類型和資源的 IP 位址的網路監看員的一項功能。 toolearn 深入了解下個躍點，請瀏覽[下一個躍點概觀](network-watcher-next-hop-overview.md)。

## <a name="retrieve-network-watcher"></a>擷取網路監看員

hello 第一個步驟是 tooretrieve hello 網路監看員執行個體。 hello`$networkWatcher`變數傳遞 toohello 下一個躍點驗證 cmdlet。

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" } 
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName 
```

## <a name="get-a-virtual-machine"></a>取得虛擬機器

下一個躍點傳回 hello 下一個躍點和 hello hello 下一個躍點 IP 位址，從虛擬機器。 Hello cmdlet 需要虛擬機器的識別碼。 如果您已經知道 hello 虛擬機器 toouse hello 識別碼，您可以略過此步驟。

```powershell
$VM = Get-AzurermVM -ResourceGroupName "testrg" -Name "testvm1"
```

> [!NOTE]
> 下一個躍點需要 hello VM 資源配置 toorun。

## <a name="get-hello-network-interfaces"></a>取得 hello 網路介面

需要 hello 的 hello 虛擬機器上的 NIC 的 IP 位址，在此範例中我們擷取 hello Nic 的虛擬機器上。 如果您已經知道 hello IP 位址，您會想 tootest hello 虛擬機器上，您可以略過此步驟。

```powershell
$Nics = Get-AzureRmNetworkInterface | Where {$_.Id -eq $vm.NetworkProfile.NetworkInterfaces.Id.ForEach({$_})}
```

## <a name="get-next-hop"></a>取得下一個躍點

現在，我們會呼叫 hello `Get-AzureRmNetworkWatcherNextHop` cmdlet。 我們傳遞 hello cmdlet hello 網路監看員，虛擬機器識別碼時，來源 IP 位址和目的地 IP 位址。 在此範例中，hello 目的地 IP 位址會是 tooa VM，另一個虛擬網路中。 Hello 兩個虛擬網路之間沒有虛擬網路閘道。

```powershell
Get-AzureRmNetworkWatcherNextHop -NetworkWatcher $networkWatcher -TargetVirtualMachineId $VM.Id -SourceIPAddress $nics[0].IpConfigurations[0].PrivateIpAddress  -DestinationIPAddress 10.0.2.4 
```

## <a name="review-results"></a>檢閱結果

完成時，會提供 hello 結果。 它是的資源 hello 類型以及傳回 hello 下一個躍點 IP 位址。 在此案例中，它是 hello 虛擬網路閘道的 hello 公用 IP 位址。

```
NextHopIpAddress NextHopType           RouteTableId 
---------------- -----------           ------------ 
13.78.238.92     VirtualNetworkGateway Gateway Route
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

















