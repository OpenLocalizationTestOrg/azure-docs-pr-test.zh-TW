---
title: "擷取 Azure 網路監看員-Azure CLI 2.0 aaaManage 封包 |Microsoft 文件"
description: "此頁面可讓您說明如何 toomanage hello 封包擷取功能，使用 Azure CLI 2.0 網路監看員"
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
ms.openlocfilehash: d19cb7d0ca3b7a9bc0546859e07ef6d4df4f42d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-packet-captures-with-azure-network-watcher-using-azure-cli-20"></a>使用 Azure CLI 2.0，利用 Azure 網路監看員管理封包擷取

> [!div class="op_single_selector"]
> - [Azure 入口網站](network-watcher-packet-capture-manage-portal.md)
> - [PowerShell](network-watcher-packet-capture-manage-powershell.md)
> - [CLI 1.0](network-watcher-packet-capture-manage-cli-nodejs.md)
> - [CLI 2.0](network-watcher-packet-capture-manage-cli.md)
> - [Azure REST API](network-watcher-packet-capture-manage-rest.md)

網路監看員封包擷取可讓您 toocreate 擷取工作階段 tootrack 流量 tooand 從虛擬機器。 篩選器可供 hello 擷取工作階段 tooensure 擷取您想要只 hello 流量。 封包擷取可在主動和被動協助 toodiagnose 網路異常狀況。 其他用途包括收集網路統計資料，取得有關網路入侵，toodebug 用戶端與伺服器通訊，以及執行更多。 透過無法 tooremotely 觸發程序封包擷取，這項功能可以減輕工作 hello 負擔的手動和 hello 想要在電腦上，以節省寶貴的時間執行封包擷取。

本文使用我們的下一個層代 CLI hello 資源管理部署模型，Azure CLI 2.0 中，這是適用於 Windows、 Mac 和 Linux。

tooperform hello 步驟在本文中，您需要[hello Azure 命令列介面安裝的 Mac、 Linux 及 Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2)。

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

執行 hello `az vm extension set` cmdlet tooinstall hello 封包擷取代理程式 hello 客體虛擬機器上的。

若為 Windows 虛擬機器：

```azurecli
az vm extension set --resource-group resourceGroupName --vm-name virtualMachineName --publisher Microsoft.Azure.NetworkWatcher --name NetworkWatcherAgentWindows --version 1.4
```

若為 Linux 虛擬機器：

```azurecli
az vm extension set --resource-group resourceGroupName --vm-name virtualMachineName --publisher Microsoft.Azure.NetworkWatcher --name NetworkWatcherAgentLinux--version 1.4
````

### <a name="step-2"></a>步驟 2

tooensure hello 代理程式的安裝，執行 hello `vm extension get` cmdlet 並將它傳遞 hello 資源群組和虛擬機器名稱。 檢查 hello 產生清單 tooensure hello 代理程式已安裝。

```azurecli
az vm extension show -resource-group resourceGroupName --vm-name virtualMachineName --name NetworkWatcherAgentWindows
```

下列範例中的 hello 是執行 hello 回應的範例`az vm extension show`

```json
{
  "autoUpgradeMinorVersion": true,
  "forceUpdateTag": null,
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Compute/virtualMachines/{vmName}/extensions/NetworkWatcherAgentWindows",
  "instanceView": null,
  "location": "westcentralus",
  "name": "NetworkWatcherAgentWindows",
  "protectedSettings": null,
  "provisioningState": "Succeeded",
  "publisher": "Microsoft.Azure.NetworkWatcher",
  "resourceGroup": "{resourceGroupName}",
  "settings": null,
  "tags": null,
  "type": "Microsoft.Compute/virtualMachines/extensions",
  "typeHandlerVersion": "1.4",
  "virtualMachineExtensionType": "NetworkWatcherAgentWindows"
}
```

## <a name="start-a-packet-capture"></a>啟動封包擷取

Hello 前面的步驟完成後，hello 虛擬機器上安裝 hello 封包擷取代理程式。

### <a name="step-1"></a>步驟 1

hello 下一個步驟是 tooretrieve hello 網路監看員執行個體。 T 名稱 hello 網路監看員會傳遞 toohello`az network watcher show`步驟 4 中的 cmdlet。

```azurecli
az network watcher show -resource-group resourceGroup -name networkWatcherName
```

### <a name="step-2"></a>步驟 2

擷取儲存體帳戶。 這個儲存體帳戶是使用的 toostore hello 封包擷取檔案。

```azurecli
azure storage account list
```

### <a name="step-3"></a>步驟 3

篩選可使用的 toolimit hello 資料儲存的 hello 封包擷取。 hello 下列範例設定封包擷取與多個篩選器。  hello 前三個篩選器收集傳出的 TCP 流量只會從本機 IP 10.0.0.3 toodestination 連接埠 20、 80 和 443。  hello 最後一個篩選條件會收集只有 UDP 流量。

```azurecli
az network watcher packet-capture create --resource-group {resoureceurceGroupName} --vm {vmName} --name packetCaptureName --storage-account gwteststorage123abc --filters "[{\"protocol\":\"TCP\", \"remoteIPAddress\":\"1.1.1.1-255.255.255\",\"localIPAddress\":\"10.0.0.3\", \"remotePort\":\"20\"},{\"protocol\":\"TCP\", \"remoteIPAddress\":\"1.1.1.1-255.255.255\",\"localIPAddress\":\"10.0.0.3\", \"remotePort\":\"80\"},{\"protocol\":\"TCP\", \"remoteIPAddress\":\"1.1.1.1-255.255.255\",\"localIPAddress\":\"10.0.0.3\", \"remotePort\":\"443\"},{\"protocol\":\"UDP\"}]"
```

hello 下列範例是執行 hello hello 預期輸出`az network watcher packet-capture create`cmdlet。

```json
{
  "bytesToCapturePerPacket": 0,
  "etag": "W/\"b8cf3528-2e14-45cb-a7f3-5712ffb687ac\"",
  "filters": [
    {
      "localIpAddress": "10.0.0.3",
      "localPort": "",
      "protocol": "TCP",
      "remoteIpAddress": "1.1.1.1-255.255.255",
      "remotePort": "20"
    },
    {
      "localIpAddress": "10.0.0.3",
      "localPort": "",
      "protocol": "TCP",
      "remoteIpAddress": "1.1.1.1-255.255.255",
      "remotePort": "80"
    },
    {
      "localIpAddress": "10.0.0.3",
      "localPort": "",
      "protocol": "TCP",
      "remoteIpAddress": "1.1.1.1-255.255.255",
      "remotePort": "443"
    },
    {
      "localIpAddress": "",
      "localPort": "",
      "protocol": "UDP",
      "remoteIpAddress": "",
      "remotePort": ""
    }
  ],
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/NetworkWatcherRG/providers/Microsoft.Network/networkWatchers/NetworkWatcher_westcentralus/pa
cketCaptures/packetCaptureName",
  "name": "packetCaptureName",
  "provisioningState": "Succeeded",
  "resourceGroup": "NetworkWatcherRG",
  "storageLocation": {
    "filePath": null,
    "storageId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/gwteststorage123abc",
    "storagePath": "https://gwteststorage123abc.blob.core.windows.net/network-watcher-logs/subscriptions/00000000-0000-0000-0000-000000000000/resourcegroups/{resourceGroupName}/p
roviders/microsoft.compute/virtualmachines/{vmName}/2017/05/25/packetcapture_16_22_34_630.cap"
  },
  "target": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Compute/virtualMachines/{vmName}",
  "timeLimitInSeconds": 18000,
  "totalBytesPerSession": 1073741824
}
```

## <a name="get-a-packet-capture"></a>取得封包擷取

執行 hello `az network watcher packet-capture show` cmdlet，擷取目前正在執行，或已完成的封包擷取 hello 狀態。

```azurecli
az network watcher packet-capture show --name packetCaptureName --location westcentralus
```

hello 下列範例是 hello 輸出 hello `az network watcher packet-capture show` cmdlet。 hello 下列範例是 hello 擷取完成後。 將停止 hello PacketCaptureStatus 值 StopReason TimeExceeded。 這個值會顯示 hello 封包擷取已順利完成，並執行它的時間。

```
{
  "bytesToCapturePerPacket": 0,
  "etag": "W/\"b8cf3528-2e14-45cb-a7f3-5712ffb687ac\"",
  "filters": [
    {
      "localIpAddress": "10.0.0.3",
      "localPort": "",
      "protocol": "TCP",
      "remoteIpAddress": "1.1.1.1-255.255.255",
      "remotePort": "20"
    },
    {
      "localIpAddress": "10.0.0.3",
      "localPort": "",
      "protocol": "TCP",
      "remoteIpAddress": "1.1.1.1-255.255.255",
      "remotePort": "80"
    },
    {
      "localIpAddress": "10.0.0.3",
      "localPort": "",
      "protocol": "TCP",
      "remoteIpAddress": "1.1.1.1-255.255.255",
      "remotePort": "443"
    },
    {
      "localIpAddress": "",
      "localPort": "",
      "protocol": "UDP",
      "remoteIpAddress": "",
      "remotePort": ""
    }
  ],
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/NetworkWatcherRG/providers/Microsoft.Network/networkWatchers/NetworkWatcher_westcentralus/packetCaptures/packetCaptureName",
  "name": "packetCaptureName",
  "provisioningState": "Succeeded",
  "resourceGroup": "NetworkWatcherRG",
  "storageLocation": {
    "filePath": null,
    "storageId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/gwteststorage123abc",
    "storagePath": "https://gwteststorage123abc.blob.core.windows.net/network-watcher-logs/subscriptions/00000000-0000-0000-0000-000000000000/resourcegroups/{resourceGroupName}/providers/microsoft.compute/virtualmachines/{vmName}/2017/05/25/packetcapt
ure_16_22_34_630.cap"
  },
  "target": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Compute/virtualMachines/{vmName}",
  "timeLimitInSeconds": 18000,
  "totalBytesPerSession": 1073741824
}
```

## <a name="stop-a-packet-capture"></a>停止封包擷取

藉由執行 hello `az network watcher packet-capture stop` cmdlet 時，如果擷取工作階段正在進行中它已停止。

```azurecli
az network watcher packet-capture stop --name packetCaptureName --location westcentralus
```

> [!NOTE]
> hello cmdlet 會傳回任何回應時執行的目前執行的擷取工作階段或現有的工作階段已經停止。

## <a name="delete-a-packet-capture"></a>刪除封包擷取

```azurecli
az network watcher packet-capture delete --name packetCaptureName --location westcentralus
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
