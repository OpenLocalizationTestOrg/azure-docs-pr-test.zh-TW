---
title: "擷取 Azure 網路監看員-PowerShell aaaManage 封包 |Microsoft 文件"
description: "此頁面說明如何 toomanage hello 封包擷取網路監看員使用 PowerShell 的功能"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 04d82085-c9ea-4ea1-b050-a3dd4960f3aa
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 77a522a1b05e020a73ba7140c1410615eb8761da
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-packet-captures-with-azure-network-watcher-using-powershell"></a>使用 PowerShell 以 Azure 網路監看員管理封包擷取

> [!div class="op_single_selector"]
> - [Azure 入口網站](network-watcher-packet-capture-manage-portal.md)
> - [PowerShell](network-watcher-packet-capture-manage-powershell.md)
> - [CLI 1.0](network-watcher-packet-capture-manage-cli-nodejs.md)
> - [CLI 2.0](network-watcher-packet-capture-manage-cli.md)
> - [Azure REST API](network-watcher-packet-capture-manage-rest.md)

網路監看員封包擷取可讓您 toocreate 擷取工作階段 tootrack 流量 tooand 從虛擬機器。 篩選器可供 hello 擷取工作階段 tooensure 擷取您想要只 hello 流量。 封包擷取可在主動和被動協助 toodiagnose 網路異常狀況。 其他用途包括收集網路統計資料，取得有關網路入侵，toodebug 用戶端與伺服器通訊，以及執行更多。 透過無法 tooremotely 觸發程序封包擷取，這項功能可以減輕工作 hello 負擔的手動和 hello 想要在電腦上，以節省寶貴的時間執行封包擷取。

這篇文章帶領您完成 hello 封包擷取目前可用的不同的管理工作。

- [**啟動封包擷取**](#start-a-packet-capture)
- [**停止封包擷取**](#stop-a-packet-capture)
- [**刪除封包擷取**](#delete-a-packet-capture)
- [**下載封包擷取**](#download-a-packet-capture)

## <a name="before-you-begin"></a>開始之前

本文假設您擁有 hello 下列資源：

* 執行個體要在 hello 區域網路監看員的 toocreate 封包擷取

* 虛擬機器與 hello 封包擷取啟用擴充功能。

> [!IMPORTANT]
> 封包擷取需要虛擬機器擴充功能 `AzureNetworkWatcherExtension`。 Hello 擴充功能安裝在 Windows VM 上瀏覽[Azure 網路監看員的代理程式適用於 Windows 的虛擬機器擴充功能](../virtual-machines/windows/extensions-nwa.md)和如 Linux VM，請造訪[Azure 網路監看員的代理程式虛擬機器擴充功能，適用於 Linux](../virtual-machines/linux/extensions-nwa.md).

## <a name="install-vm-extension"></a>安裝 VM 擴充功能

### <a name="step-1"></a>步驟 1

```powershell
$VM = Get-AzureRmVM -ResourceGroupName testrg -Name VM1
```

### <a name="step-2"></a>步驟 2

hello 擷取 hello 延伸模組資訊的下列範例所需 toorun hello `Set-AzureRmVMExtension` cmdlet。 此 cmdlet 會 hello 客體虛擬機器上安裝 hello 封包擷取代理程式。

> [!NOTE]
> hello`Set-AzureRmVMExtension`指令程式可能需要幾分鐘的時間 toocomplete。

若為 Windows 虛擬機器：

```powershell
$AzureNetworkWatcherExtension = Get-AzureRmVMExtensionImage -Location WestCentralUS -PublisherName Microsoft.Azure.NetworkWatcher -Type NetworkWatcherAgentWindows -Version 1.4.13.0
$ExtensionName = "AzureNetworkWatcherExtension"
Set-AzureRmVMExtension -ResourceGroupName $VM.ResourceGroupName  -Location $VM.Location -VMName $VM.Name -Name $ExtensionName -Publisher $AzureNetworkWatcherExtension.PublisherName -ExtensionType $AzureNetworkWatcherExtension.Type -TypeHandlerVersion $AzureNetworkWatcherExtension.Version.Substring(0,3)
```

若為 Linux 虛擬機器：

```powershell
$AzureNetworkWatcherExtension = Get-AzureRmVMExtensionImage -Location WestCentralUS -PublisherName Microsoft.Azure.NetworkWatcher -Type NetworkWatcherAgentLinux -Version 1.4.13.0
$ExtensionName = "AzureNetworkWatcherExtension"
Set-AzureRmVMExtension -ResourceGroupName $VM.ResourceGroupName  -Location $VM.Location -VMName $VM.Name -Name $ExtensionName -Publisher $AzureNetworkWatcherExtension.PublisherName -ExtensionType $AzureNetworkWatcherExtension.Type -TypeHandlerVersion $AzureNetworkWatcherExtension.Version.Substring(0,3)
````

hello 下列範例是成功的回應之後執行 hello `Set-AzureRmVMExtension` cmdlet。

```
RequestId IsSuccessStatusCode StatusCode ReasonPhrase
--------- ------------------- ---------- ------------
                         True         OK OK   
```

### <a name="step-3"></a>步驟 3

tooensure hello 代理程式的安裝，執行 hello `Get-AzureRmVMExtension` cmdlet 並將它傳遞 hello 虛擬機器名稱與 hello 延伸模組名稱。

```powershell
Get-AzureRmVMExtension -ResourceGroupName $VM.ResourceGroupName  -VMName $VM.Name -Name $ExtensionName
```

下列範例中的 hello 是執行 hello 回應的範例`Get-AzureRmVMExtension`

```
ResourceGroupName       : testrg
VMName                  : testvm1
Name                    : AzureNetworkWatcherExtension
Location                : westcentralus
Etag                    : null
Publisher               : Microsoft.Azure.NetworkWatcher
ExtensionType           : NetworkWatcherAgentWindows
TypeHandlerVersion      : 1.4
Id                      : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Compute/virtualMachines/testvm1/
                          extensions/AzureNetworkWatcherExtension
PublicSettings          : 
ProtectedSettings       : 
ProvisioningState       : Succeeded
Statuses                : 
SubStatuses             : 
AutoUpgradeMinorVersion : True
ForceUpdateTag          : 
```

## <a name="start-a-packet-capture"></a>啟動封包擷取

Hello 前面的步驟完成後，hello 虛擬機器上安裝 hello 封包擷取代理程式。

### <a name="step-1"></a>步驟 1

hello 下一個步驟是 tooretrieve hello 網路監看員執行個體。 這個變數會傳遞 toohello`New-AzureRmNetworkWatcherPacketCapture`步驟 4 中的 cmdlet。

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" }
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName  
```

### <a name="step-2"></a>步驟 2

擷取儲存體帳戶。 這個儲存體帳戶是使用的 toostore hello 封包擷取檔案。

```powershell
$storageAccount = Get-AzureRmStorageAccount -ResourceGroupName testrg -Name testrgsa123
```

### <a name="step-3"></a>步驟 3

篩選可使用的 toolimit hello 資料儲存的 hello 封包擷取。 hello 下列範例設定兩個篩選條件。  一個篩選條件會收集傳出 TCP 流量只會從本機 IP 10.0.0.3 toodestination 連接埠 20、 80 和 443。  hello 第二個篩選會收集只有 UDP 流量。

```powershell
$filter1 = New-AzureRmPacketCaptureFilterConfig -Protocol TCP -RemoteIPAddress "1.1.1.1-255.255.255" -LocalIPAddress "10.0.0.3" -LocalPort "1-65535" -RemotePort "20;80;443"
$filter2 = New-AzureRmPacketCaptureFilterConfig -Protocol UDP
```

> [!NOTE]
> 一個封包擷取可以定義多個篩選器。

### <a name="step-4"></a>步驟 4

執行 hello `New-AzureRmNetworkWatcherPacketCapture` cmdlet toostart hello 封包擷取程序，傳遞所需的 hello hello 先前步驟中所擷取的值。
```powershell

New-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -TargetVirtualMachineId $vm.Id -PacketCaptureName "PacketCaptureTest" -StorageAccountId $storageAccount.id -TimeLimitInSeconds 60 -Filters $filter1, $filter2
```

hello 下列範例是執行 hello hello 預期輸出`New-AzureRmNetworkWatcherPacketCapture`cmdlet。

```
Name                    : PacketCaptureTest
Id                      : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/NetworkWatcherRG/providers/Microsoft.Network/networkWatcher
                          s/NetworkWatcher_westcentralus/packetCaptures/PacketCaptureTest
Etag                    : W/"3bf27278-8251-4651-9546-c7f369855e4e"
ProvisioningState       : Succeeded
Target                  : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Compute/virtualMachines/testvm1
BytesToCapturePerPacket : 0
TotalBytesPerSession    : 1073741824
TimeLimitInSeconds      : 60
StorageLocation         : {
                            "StorageId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Storage/storageA
                          ccounts/examplestorage",
                            "StoragePath": "https://examplestorage.blob.core.windows.net/network-watcher-logs/subscriptions/00000000-0000-0000-0000-00000
                          0000000/resourcegroups/testrg/providers/microsoft.compute/virtualmachines/testvm1/2017/02/01/packetcapture_22_42_48_238.cap"
                          }
Filters                 : [
                            {
                              "Protocol": "TCP",
                              "RemoteIPAddress": "1.1.1.1-255.255.255",
                              "LocalIPAddress": "10.0.0.3",
                              "LocalPort": "1-65535",
                              "RemotePort": "20;80;443"
                            },
                            {
                              "Protocol": "UDP",
                              "RemoteIPAddress": "",
                              "LocalIPAddress": "",
                              "LocalPort": "",
                              "RemotePort": ""
                            }
                          ]


```

## <a name="get-a-packet-capture"></a>取得封包擷取

執行 hello `Get-AzureRmNetworkWatcherPacketCapture` cmdlet，擷取目前正在執行，或已完成的封包擷取 hello 狀態。

```powershell
Get-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -PacketCaptureName "PacketCaptureTest"
```

hello 下列範例是 hello 輸出 hello `Get-AzureRmNetworkWatcherPacketCapture` cmdlet。 hello 下列範例是 hello 擷取完成後。 將停止 hello PacketCaptureStatus 值 StopReason TimeExceeded。 這個值會顯示 hello 封包擷取已順利完成，並執行它的時間。
```
Name                    : PacketCaptureTest
Id                      : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/NetworkWatcherRG/providers/Microsoft.Network/networkWatcher
                          s/NetworkWatcher_westcentralus/packetCaptures/PacketCaptureTest
Etag                    : W/"4b9a81ed-dc63-472e-869e-96d7166ccb9b"
ProvisioningState       : Succeeded
Target                  : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Compute/virtualMachines/testvm1
BytesToCapturePerPacket : 0
TotalBytesPerSession    : 1073741824
TimeLimitInSeconds      : 60
StorageLocation         : {
                            "StorageId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Storage/storageA
                          ccounts/examplestorage",
                            "StoragePath": "https://examplestorage.blob.core.windows.net/network-watcher-logs/subscriptions/00000000-0000-0000-0000-00000
                          0000000/resourcegroups/testrg/providers/microsoft.compute/virtualmachines/testvm1/2017/02/01/packetcapture_22_42_48_238.cap"
                          }
Filters                 : [
                            {
                              "Protocol": "TCP",
                              "RemoteIPAddress": "1.1.1.1-255.255.255",
                              "LocalIPAddress": "10.0.0.3",
                              "LocalPort": "1-65535",
                              "RemotePort": "20;80;443"
                            },
                            {
                              "Protocol": "UDP",
                              "RemoteIPAddress": "",
                              "LocalIPAddress": "",
                              "LocalPort": "",
                              "RemotePort": ""
                            }
                          ]
CaptureStartTime        : 2/1/2017 10:43:01 PM
PacketCaptureStatus     : Stopped
StopReason              : TimeExceeded
PacketCaptureError      : []
```

## <a name="stop-a-packet-capture"></a>停止封包擷取

藉由執行 hello `Stop-AzureRmNetworkWatcherPacketCapture` cmdlet 時，如果擷取工作階段正在進行中它已停止。

```powershell
Stop-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -PacketCaptureName "PacketCaptureTest"
```

> [!NOTE]
> hello cmdlet 會傳回任何回應時執行的目前執行的擷取工作階段或現有的工作階段已經停止。

## <a name="delete-a-packet-capture"></a>刪除封包擷取

```powershell
Remove-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -PacketCaptureName "PacketCaptureTest"
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














