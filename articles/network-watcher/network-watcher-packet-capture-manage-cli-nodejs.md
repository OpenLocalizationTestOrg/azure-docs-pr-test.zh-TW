---
title: "擷取 Azure 網路監看員-Azure CLI 1.0 aaaManage 封包 |Microsoft 文件"
description: "此頁面可讓您說明如何 toomanage hello 封包擷取功能，使用 Azure CLI 1.0 網路監看員"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: cb0c1d10-f7f2-4c34-b08c-f73452430be8
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: c4b710a8d82ccaaf65876a8c2ef845aa97b5f831
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-packet-captures-with-azure-network-watcher-using-azure-cli-10"></a>使用 Azure CLI 1.0，利用 Azure 網路監看員管理封包擷取

> [!div class="op_single_selector"]
> - [Azure 入口網站](network-watcher-packet-capture-manage-portal.md)
> - [PowerShell](network-watcher-packet-capture-manage-powershell.md)
> - [CLI 1.0](network-watcher-packet-capture-manage-cli-nodejs.md)
> - [CLI 2.0](network-watcher-packet-capture-manage-cli.md)
> - [Azure REST API](network-watcher-packet-capture-manage-rest.md)

網路監看員封包擷取可讓您 toocreate 擷取工作階段 tootrack 流量 tooand 從虛擬機器。 篩選器可供 hello 擷取工作階段 tooensure 擷取您想要只 hello 流量。 封包擷取可在主動和被動協助 toodiagnose 網路異常狀況。 其他用途包括收集網路統計資料，取得有關網路入侵，toodebug 用戶端與伺服器通訊，以及執行更多。 透過無法 tooremotely 觸發程序封包擷取，這項功能可以減輕工作 hello 負擔的手動和 hello 想要在電腦上，以節省寶貴的時間執行封包擷取。

本文使用跨平台 Azure CLI 1.0，這適用於 Windows、Mac 和 Linux。

這篇文章帶領您完成 hello 封包擷取目前可用的不同的管理工作。

- [**啟動封包擷取**](#start-a-packet-capture)
- [**停止封包擷取**](#stop-a-packet-capture)
- [**刪除封包擷取**](#delete-a-packet-capture)
- [**下載封包擷取**](#download-a-packet-capture)

## <a name="before-you-begin"></a>開始之前

本文假設您擁有 hello 下列資源：

- 執行個體要在 hello 區域網路監看員的 toocreate 封包擷取
- 虛擬機器與 hello 封包擷取啟用擴充功能。

> [!IMPORTANT]
> 封包擷取需要的代理程式 toobe hello 虛擬機器上執行。 hello 代理程式會安裝為擴充功能。 如需 VM 擴充功能的指示，請瀏覽[虛擬機器擴充功能和功能](../virtual-machines/windows/extensions-features.md)。

## <a name="install-vm-extension"></a>安裝 VM 擴充功能

### <a name="step-1"></a>步驟 1

執行 hello `azure vm extension set` cmdlet tooinstall hello 封包擷取代理程式 hello 客體虛擬機器上的。

若為 Windows 虛擬機器：

```azurecli
azure vm extension set -g resourceGroupName -m virtualMachineName -p Microsoft.Azure.NetworkWatcher -r AzureNetworkWatcherExtension -n NetworkWatcherAgentWindows -o 1.4
```

若為 Linux 虛擬機器：

```azurecli
azure vm extension set -g resourceGroupName -m virtualMachineName -p Microsoft.Azure.NetworkWatcher -r AzureNetworkWatcherExtension -n NetworkWatcherAgentLinux -o 1.4
````

### <a name="step-2"></a>步驟 2

tooensure hello 代理程式的安裝，執行 hello `vm extension get` cmdlet 並將它傳遞 hello 資源群組和虛擬機器名稱。 檢查 hello 產生清單 tooensure hello 代理程式已安裝。

```azurecli
azure vm extension get -g resourceGroupName -m virtualMachineName
```

下列範例中的 hello 是執行 hello 回應的範例`azure vm extension get`

```
info:    Executing command vm extension get
+ Looking up hello VM "virtualMachineName"
data:    Publisher                       Name                        Version  State
data:    ------------------------------  -----------------------     -------  ---------
data:    Microsoft.Azure.NetworkWatcher  NetworkWatcherAgentWindows  1.4      Succeeded
info:    vm extension get command OK
```

## <a name="start-a-packet-capture"></a>啟動封包擷取

Hello 前面的步驟完成後，hello 虛擬機器上安裝 hello 封包擷取代理程式。

### <a name="step-1"></a>步驟 1

hello 下一個步驟是 tooretrieve hello 網路監看員執行個體。 這個變數會傳遞 toohello`network watcher show`步驟 4 中的 cmdlet。

```azurecli
azure network watcher show -g resourceGroup -n networkWatcherName
```

### <a name="step-2"></a>步驟 2

擷取儲存體帳戶。 這個儲存體帳戶是使用的 toostore hello 封包擷取檔案。

```azurecli
azure storage account list
```

### <a name="step-3"></a>步驟 3

篩選可使用的 toolimit hello 資料儲存的 hello 封包擷取。 hello 下列範例設定封包擷取與多個篩選器。  hello 前三個篩選器收集傳出的 TCP 流量只會從本機 IP 10.0.0.3 toodestination 連接埠 20、 80 和 443。  hello 最後一個篩選條件會收集只有 UDP 流量。

```azurecli
azure network watcher packet-capture create -g resourceGroupName -w networkWatcherName -n packetCaptureName -t targetResourceId -o storageAccountResourceId -f "[{\"protocol\":\"TCP\", \"remoteIPAddress\":\"1.1.1.1-255.255.255\",\"localIPAddress\":\"10.0.0.3\", \"remotePort\":\"20\"},{\"protocol\":\"TCP\", \"remoteIPAddress\":\"1.1.1.1-255.255.255\",\"localIPAddress\":\"10.0.0.3\", \"remotePort\":\"80\"},{\"protocol\":\"TCP\", \"remoteIPAddress\":\"1.1.1.1-255.255.255\",\"localIPAddress\":\"10.0.0.3\", \"remotePort\":\"443\"},{\"protocol\":\"UDP\"}]"
```

一個封包擷取可以定義多個篩選器。 如果您使用複雜的篩選條件結構，它是較佳的 toouse 篩選 json 檔案 tooavoid 語法錯誤。 比方說，使用 hello 旗標 」-r"(而不是"-f")，並傳遞 hello 包含下列篩選器的 hello 的 json 檔案的位置：

```json
[
    {
        "protocol":"TCP",
        "remoteIPAddress":"1.1.1.1-255.255.255",
        "localIPAddress":"10.0.0.3",
        "remotePort":"20"
    },
    {
        "protocol":"TCP",
        "remoteIPAddress":"1.1.1.1-255.255.255",
        "localIPAddress":"10.0.0.3",
        "remotePort":"80"
    },
    {
        "protocol":"TCP",
        "remoteIPAddress":"1.1.1.1-255.255.255",
        "localIPAddress":"10.0.0.3",
        "remotePort":"443"
    },
    {
        "protocol":"UDP"
    }
]
```


hello 下列範例是執行 hello hello 預期輸出`network watcher packet-capture create`cmdlet。

```
data:    Name                            : packetCaptureName
data:    Etag                            : W/"d59bb2d2-dc95-43da-b740-e0ef8fcacecb"
data:    Target                          : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/resourceGroupName/providers/Microsoft.Compute/virtualMachines/testVM
data:    Bytes tooCapture Per Packet     : 0
data:    Total Bytes Per Session         : 1073741824
data:    Time Limit In Seconds           : 18000
data:    Storage Location:
data:      Storage Id                    : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/resourceGroupName/providers/Microsoft.Storage/storageAccounts/testStorage
data:      Storage Path                  : https://testStorage.blob.core.windows.net/network-watcher-logs/subscriptions/00000000-0000-0000-0000-000000000000/resourcegroups/testRG/providers/microsoft.compute/virtualmachines/testVM/2017/02/17/packetcapture_01_21_18_145.cap
data:    Filters                         : []
data:    Provisioning State              : Succeeded
info:    network watcher packet-capture create command OK
```

## <a name="get-a-packet-capture"></a>取得封包擷取

執行 hello `network watcher packet-capture show` cmdlet，擷取目前正在執行，或已完成的封包擷取 hello 狀態。

```azurecli
azure network watcher packet-capture show -g resourceGroupName -w networkWatcherName -n packetCaptureName
```

hello 下列範例是 hello 輸出 hello `network watcher packet-capture show` cmdlet。 hello 下列範例是 hello 擷取完成後。 將停止 hello PacketCaptureStatus 值 StopReason TimeExceeded。 這個值會顯示 hello 封包擷取已順利完成，並執行它的時間。

```
data:    Name                            : packetCaptureName
data:    Etag                            : W/"d59bb2d2-dc95-43da-b740-e0ef8fcacecb"
data:    Target                          : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/resourceGroupName/providers/Microsoft.Compute/virtualMachines/testVM
data:    Bytes tooCapture Per Packet     : 0
data:    Total Bytes Per Session         : 1073741824
data:    Time Limit In Seconds           : 18000
data:    Storage Location:
data:      Storage Id                    : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/resourceGroupName/providers/Microsoft.Storage/storageAccounts/testStorage
data:      Storage Path                  : https://testStorage.blob.core.windows.net/network-watcher-logs/subscriptions/00000000-0000-0000-0000-000000000000/resourcegroups/testRG/providers/microsoft.compute/virtualmachines/testVM/2017/02/17/packetcapture_01_21_18_145.cap
data:    Filters                         : []
data:    Provisioning State              : Succeeded
info:    network watcher packet-capture show command OK
```

## <a name="stop-a-packet-capture"></a>停止封包擷取

藉由執行 hello `network watcher packet-capture stop` cmdlet 時，如果擷取工作階段正在進行中它已停止。

```azurecli
azure network watcher packet-capture stop -g resourceGroupName -w networkWatcherName -n packetCaptureName
```

> [!NOTE]
> hello cmdlet 會傳回任何回應時執行的目前執行的擷取工作階段或現有的工作階段已經停止。

## <a name="delete-a-packet-capture"></a>刪除封包擷取

```azurecli
azure network watcher packet-capture delete -g resourceGroupName -w networkWatcherName -n packetCaptureName
```

> [!NOTE]
> 刪除封包擷取並不會刪除 hello 儲存體帳戶中的 hello 檔案。

## <a name="download-a-packet-capture"></a>下載封包擷取

您的封包擷取工作階段完成後，請 hello 擷取檔案可上傳的 tooblob 儲存體或 tooa 本機檔案 hello VM 上。 hello 封包擷取 hello 儲存位置被定義在 hello 工作階段的建立。 方便的工具 tooaccess 這些擷取的檔案儲存的 tooa 儲存體帳戶是 Microsoft Azure 儲存體總管 中，這可以在這裡下載： http://storageexplorer.com/

如果指定的儲存體帳戶，則封包擷取檔案會儲存在下列位置的 hello tooa 儲存體帳戶：

```
https://{storageAccountName}.blob.core.windows.net/network-watcher-logs/subscriptions/{subscriptionId}/resourcegroups/{storageAccountResourceGroup}/providers/microsoft.compute/virtualmachines/{VMName}/{year}/{month}/{day}/packetCapture_{creationTime}.cap
```

## <a name="next-steps"></a>後續步驟

了解如何 tooautomate 封包擷取虛擬機器警示藉由檢視[建立警示觸發的封包擷取](network-watcher-alert-triggered-packet-capture.md)

造訪[檢查 IP 流量驗證](network-watcher-check-ip-flow-verify-portal.md)來得知 VM 是否允許特定流量流入或流出

<!-- Image references -->
