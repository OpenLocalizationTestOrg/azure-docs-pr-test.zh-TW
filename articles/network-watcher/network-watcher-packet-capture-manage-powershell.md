---
title: "使用 Azure 網路監看員管理封包擷取 - PowerShell | Microsoft Docs"
description: "此頁面說明如何使用 PowerShell 管理網路監看員的封包擷取功能"
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
ms.openlocfilehash: abd3b3641da80ee835fac85b4bde68594449e451
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="manage-packet-captures-with-azure-network-watcher-using-powershell"></a><span data-ttu-id="fd29b-103">使用 PowerShell 以 Azure 網路監看員管理封包擷取</span><span class="sxs-lookup"><span data-stu-id="fd29b-103">Manage packet captures with Azure Network Watcher using PowerShell</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="fd29b-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="fd29b-104">Azure portal</span></span>](network-watcher-packet-capture-manage-portal.md)
> - [<span data-ttu-id="fd29b-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="fd29b-105">PowerShell</span></span>](network-watcher-packet-capture-manage-powershell.md)
> - [<span data-ttu-id="fd29b-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="fd29b-106">CLI 1.0</span></span>](network-watcher-packet-capture-manage-cli-nodejs.md)
> - [<span data-ttu-id="fd29b-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="fd29b-107">CLI 2.0</span></span>](network-watcher-packet-capture-manage-cli.md)
> - [<span data-ttu-id="fd29b-108">Azure REST API</span><span class="sxs-lookup"><span data-stu-id="fd29b-108">Azure REST API</span></span>](network-watcher-packet-capture-manage-rest.md)

<span data-ttu-id="fd29b-109">網路監看員封包擷取可讓您建立擷取工作階段來追蹤虛擬機器的流入和流出流量。</span><span class="sxs-lookup"><span data-stu-id="fd29b-109">Network Watcher packet capture allows you to create capture sessions to track traffic to and from a virtual machine.</span></span> <span data-ttu-id="fd29b-110">系統會為擷取工作階段提供篩選器，以確保您只會擷取到您想要的流量。</span><span class="sxs-lookup"><span data-stu-id="fd29b-110">Filters are provided for the capture session to ensure you capture only the traffic you want.</span></span> <span data-ttu-id="fd29b-111">封包擷取有助於被動和主動地診斷網路異常。</span><span class="sxs-lookup"><span data-stu-id="fd29b-111">Packet capture helps to diagnose network anomalies both reactively and proactively.</span></span> <span data-ttu-id="fd29b-112">其他用途包括收集網路統計資料、取得有關網路入侵的資訊，以及偵錯用戶端與伺服器間的通訊等等。</span><span class="sxs-lookup"><span data-stu-id="fd29b-112">Other uses include gathering network statistics, gaining information on network intrusions, to debug client-server communications and much more.</span></span> <span data-ttu-id="fd29b-113">藉由能夠從遠端觸發封包擷取，這項功能可以減輕在所需機器上手動執行封包擷取的工作負擔，進而省下寶貴的時間。</span><span class="sxs-lookup"><span data-stu-id="fd29b-113">By being able to remotely trigger packet captures, this capability eases the burden of running a packet capture manually and on the desired machine, which saves valuable time.</span></span>

<span data-ttu-id="fd29b-114">本文會帶領您逐步完成封包擷取目前可用的不同管理工作。</span><span class="sxs-lookup"><span data-stu-id="fd29b-114">This article takes you through the different management tasks that are currently available for packet capture.</span></span>

- [<span data-ttu-id="fd29b-115">**啟動封包擷取**</span><span class="sxs-lookup"><span data-stu-id="fd29b-115">**Start a packet capture**</span></span>](#start-a-packet-capture)
- [<span data-ttu-id="fd29b-116">**停止封包擷取**</span><span class="sxs-lookup"><span data-stu-id="fd29b-116">**Stop a packet capture**</span></span>](#stop-a-packet-capture)
- [<span data-ttu-id="fd29b-117">**刪除封包擷取**</span><span class="sxs-lookup"><span data-stu-id="fd29b-117">**Delete a packet capture**</span></span>](#delete-a-packet-capture)
- [<span data-ttu-id="fd29b-118">**下載封包擷取**</span><span class="sxs-lookup"><span data-stu-id="fd29b-118">**Download a packet capture**</span></span>](#download-a-packet-capture)

## <a name="before-you-begin"></a><span data-ttu-id="fd29b-119">開始之前</span><span class="sxs-lookup"><span data-stu-id="fd29b-119">Before you begin</span></span>

<span data-ttu-id="fd29b-120">本文假設您具有下列資源：</span><span class="sxs-lookup"><span data-stu-id="fd29b-120">This article assumes you have the following resources:</span></span>

* <span data-ttu-id="fd29b-121">您想要用來建立封包擷取之區域中的網路監看員執行個體</span><span class="sxs-lookup"><span data-stu-id="fd29b-121">An instance of Network Watcher in the region you want to create a packet capture</span></span>

* <span data-ttu-id="fd29b-122">已啟用封包擷取擴充功能的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="fd29b-122">A virtual machine with the packet capture extension enabled.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fd29b-123">封包擷取需要虛擬機器擴充功能 `AzureNetworkWatcherExtension`。</span><span class="sxs-lookup"><span data-stu-id="fd29b-123">Packet capture requires a virtual machine extension `AzureNetworkWatcherExtension`.</span></span> <span data-ttu-id="fd29b-124">若要在 Windows VM 上安裝擴充功能，請瀏覽[適用於 Windows 的 Azure 網路監看員代理程式虛擬機器擴充功能](../virtual-machines/windows/extensions-nwa.md)，若要在 Linux VM 上安裝，則請瀏覽[適用於 Linux 的 Azure 網路監看員代理程式虛擬機器擴充功能](../virtual-machines/linux/extensions-nwa.md)。</span><span class="sxs-lookup"><span data-stu-id="fd29b-124">For installing the extension on a Windows VM visit [Azure Network Watcher Agent virtual machine extension for Windows](../virtual-machines/windows/extensions-nwa.md) and for Linux VM visit [Azure Network Watcher Agent virtual machine extension for Linux](../virtual-machines/linux/extensions-nwa.md).</span></span>

## <a name="install-vm-extension"></a><span data-ttu-id="fd29b-125">安裝 VM 擴充功能</span><span class="sxs-lookup"><span data-stu-id="fd29b-125">Install VM extension</span></span>

### <a name="step-1"></a><span data-ttu-id="fd29b-126">步驟 1</span><span class="sxs-lookup"><span data-stu-id="fd29b-126">Step 1</span></span>

```powershell
$VM = Get-AzureRmVM -ResourceGroupName testrg -Name VM1
```

### <a name="step-2"></a><span data-ttu-id="fd29b-127">步驟 2</span><span class="sxs-lookup"><span data-stu-id="fd29b-127">Step 2</span></span>

<span data-ttu-id="fd29b-128">下列範例會擷取執行 `Set-AzureRmVMExtension` cmdlet 所需的延伸資訊。</span><span class="sxs-lookup"><span data-stu-id="fd29b-128">The following example retrieves the extension information needed to run the `Set-AzureRmVMExtension` cmdlet.</span></span> <span data-ttu-id="fd29b-129">此 Cmdlet 會在客體虛擬機器上安裝封包擷取代理程式。</span><span class="sxs-lookup"><span data-stu-id="fd29b-129">This cmdlet installs the packet capture agent on the guest virtual machine.</span></span>

> [!NOTE]
> <span data-ttu-id="fd29b-130">`Set-AzureRmVMExtension` cmdlet 可能需要幾分鐘的時間才能完成。</span><span class="sxs-lookup"><span data-stu-id="fd29b-130">The `Set-AzureRmVMExtension` cmdlet may take several minutes to complete.</span></span>

<span data-ttu-id="fd29b-131">若為 Windows 虛擬機器：</span><span class="sxs-lookup"><span data-stu-id="fd29b-131">For Windows virtual machines:</span></span>

```powershell
$AzureNetworkWatcherExtension = Get-AzureRmVMExtensionImage -Location WestCentralUS -PublisherName Microsoft.Azure.NetworkWatcher -Type NetworkWatcherAgentWindows -Version 1.4.13.0
$ExtensionName = "AzureNetworkWatcherExtension"
Set-AzureRmVMExtension -ResourceGroupName $VM.ResourceGroupName  -Location $VM.Location -VMName $VM.Name -Name $ExtensionName -Publisher $AzureNetworkWatcherExtension.PublisherName -ExtensionType $AzureNetworkWatcherExtension.Type -TypeHandlerVersion $AzureNetworkWatcherExtension.Version.Substring(0,3)
```

<span data-ttu-id="fd29b-132">若為 Linux 虛擬機器：</span><span class="sxs-lookup"><span data-stu-id="fd29b-132">For Linux virtual machines:</span></span>

```powershell
$AzureNetworkWatcherExtension = Get-AzureRmVMExtensionImage -Location WestCentralUS -PublisherName Microsoft.Azure.NetworkWatcher -Type NetworkWatcherAgentLinux -Version 1.4.13.0
$ExtensionName = "AzureNetworkWatcherExtension"
Set-AzureRmVMExtension -ResourceGroupName $VM.ResourceGroupName  -Location $VM.Location -VMName $VM.Name -Name $ExtensionName -Publisher $AzureNetworkWatcherExtension.PublisherName -ExtensionType $AzureNetworkWatcherExtension.Type -TypeHandlerVersion $AzureNetworkWatcherExtension.Version.Substring(0,3)
````

<span data-ttu-id="fd29b-133">執行 `Set-AzureRmVMExtension` cmdlet 之後，下列範例會是成功回應。</span><span class="sxs-lookup"><span data-stu-id="fd29b-133">The following example is a successful response after running the `Set-AzureRmVMExtension` cmdlet.</span></span>

```
RequestId IsSuccessStatusCode StatusCode ReasonPhrase
--------- ------------------- ---------- ------------
                         True         OK OK   
```

### <a name="step-3"></a><span data-ttu-id="fd29b-134">步驟 3</span><span class="sxs-lookup"><span data-stu-id="fd29b-134">Step 3</span></span>

<span data-ttu-id="fd29b-135">為了確定是否已安裝代理程式，請執行 `Get-AzureRmVMExtension` Cmdlet，並將虛擬機器名稱和副檔名傳遞給它。</span><span class="sxs-lookup"><span data-stu-id="fd29b-135">To ensure that the agent is installed, run the `Get-AzureRmVMExtension` cmdlet and pass it the virtual machine name and the extension name.</span></span>

```powershell
Get-AzureRmVMExtension -ResourceGroupName $VM.ResourceGroupName  -VMName $VM.Name -Name $ExtensionName
```

<span data-ttu-id="fd29b-136">下列範例是執行 `Get-AzureRmVMExtension` 所得回應的範例</span><span class="sxs-lookup"><span data-stu-id="fd29b-136">The following sample is an example of the response from running `Get-AzureRmVMExtension`</span></span>

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

## <a name="start-a-packet-capture"></a><span data-ttu-id="fd29b-137">啟動封包擷取</span><span class="sxs-lookup"><span data-stu-id="fd29b-137">Start a packet capture</span></span>

<span data-ttu-id="fd29b-138">完成上述步驟之後，虛擬機器上便已安裝封包擷取代理程式。</span><span class="sxs-lookup"><span data-stu-id="fd29b-138">Once the preceding steps are complete, the packet capture agent is installed on the virtual machine.</span></span>

### <a name="step-1"></a><span data-ttu-id="fd29b-139">步驟 1</span><span class="sxs-lookup"><span data-stu-id="fd29b-139">Step 1</span></span>

<span data-ttu-id="fd29b-140">下一步是擷取網路監看員執行個體。</span><span class="sxs-lookup"><span data-stu-id="fd29b-140">The next step is to retrieve the Network Watcher instance.</span></span> <span data-ttu-id="fd29b-141">此變數會在步驟 4 傳遞至 `New-AzureRmNetworkWatcherPacketCapture` Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="fd29b-141">This variable is passed to the `New-AzureRmNetworkWatcherPacketCapture` cmdlet in step 4.</span></span>

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" }
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName  
```

### <a name="step-2"></a><span data-ttu-id="fd29b-142">步驟 2</span><span class="sxs-lookup"><span data-stu-id="fd29b-142">Step 2</span></span>

<span data-ttu-id="fd29b-143">擷取儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="fd29b-143">Retrieve a storage account.</span></span> <span data-ttu-id="fd29b-144">此儲存體帳戶會用來儲存封包擷取檔案。</span><span class="sxs-lookup"><span data-stu-id="fd29b-144">This storage account is used to store the packet capture file.</span></span>

```powershell
$storageAccount = Get-AzureRmStorageAccount -ResourceGroupName testrg -Name testrgsa123
```

### <a name="step-3"></a><span data-ttu-id="fd29b-145">步驟 3</span><span class="sxs-lookup"><span data-stu-id="fd29b-145">Step 3</span></span>

<span data-ttu-id="fd29b-146">可使用篩選器來限制封包擷取所儲存的資料。</span><span class="sxs-lookup"><span data-stu-id="fd29b-146">Filters can be used to limit the data that is stored by the packet capture.</span></span> <span data-ttu-id="fd29b-147">下列範例會設定兩個篩選器。</span><span class="sxs-lookup"><span data-stu-id="fd29b-147">The following example sets up two filters.</span></span>  <span data-ttu-id="fd29b-148">一個篩選器只會收集從本機 IP 10.0.0.3 流往目的地連接埠 20、80 和 443 的連出 TCP 流量。</span><span class="sxs-lookup"><span data-stu-id="fd29b-148">One filter collects outgoing TCP traffic only from local IP 10.0.0.3 to destination ports 20, 80 and 443.</span></span>  <span data-ttu-id="fd29b-149">第二個篩選器只會收集 UDP 流量。</span><span class="sxs-lookup"><span data-stu-id="fd29b-149">The second filter collects only UDP traffic.</span></span>

```powershell
$filter1 = New-AzureRmPacketCaptureFilterConfig -Protocol TCP -RemoteIPAddress "1.1.1.1-255.255.255" -LocalIPAddress "10.0.0.3" -LocalPort "1-65535" -RemotePort "20;80;443"
$filter2 = New-AzureRmPacketCaptureFilterConfig -Protocol UDP
```

> [!NOTE]
> <span data-ttu-id="fd29b-150">一個封包擷取可以定義多個篩選器。</span><span class="sxs-lookup"><span data-stu-id="fd29b-150">Multiple filters can be defined for a packet capture.</span></span>

### <a name="step-4"></a><span data-ttu-id="fd29b-151">步驟 4</span><span class="sxs-lookup"><span data-stu-id="fd29b-151">Step 4</span></span>

<span data-ttu-id="fd29b-152">執行 `New-AzureRmNetworkWatcherPacketCapture` cmdlet 可啟動封包擷取程序，並傳遞先前步驟中擷取的必要值。</span><span class="sxs-lookup"><span data-stu-id="fd29b-152">Run the `New-AzureRmNetworkWatcherPacketCapture` cmdlet to start the packet capture process, passing the required values retrieved in the preceding steps.</span></span>
```powershell

New-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -TargetVirtualMachineId $vm.Id -PacketCaptureName "PacketCaptureTest" -StorageAccountId $storageAccount.id -TimeLimitInSeconds 60 -Filters $filter1, $filter2
```

<span data-ttu-id="fd29b-153">下列範例是執行 `New-AzureRmNetworkWatcherPacketCapture` Cmdlet 後預期會得到的輸出。</span><span class="sxs-lookup"><span data-stu-id="fd29b-153">The following example is the expected output from running the `New-AzureRmNetworkWatcherPacketCapture` cmdlet.</span></span>

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

## <a name="get-a-packet-capture"></a><span data-ttu-id="fd29b-154">取得封包擷取</span><span class="sxs-lookup"><span data-stu-id="fd29b-154">Get a packet capture</span></span>

<span data-ttu-id="fd29b-155">執行 `Get-AzureRmNetworkWatcherPacketCapture` Cmdlet 以擷取目前正在執行或已完成之封包擷取的狀態。</span><span class="sxs-lookup"><span data-stu-id="fd29b-155">Running the `Get-AzureRmNetworkWatcherPacketCapture` cmdlet, retrieves the status of a currently running, or completed packet capture.</span></span>

```powershell
Get-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -PacketCaptureName "PacketCaptureTest"
```

<span data-ttu-id="fd29b-156">下列範例是 `Get-AzureRmNetworkWatcherPacketCapture` Cmdlet 的輸出。</span><span class="sxs-lookup"><span data-stu-id="fd29b-156">The following example is the output from the `Get-AzureRmNetworkWatcherPacketCapture` cmdlet.</span></span> <span data-ttu-id="fd29b-157">下列範例是在擷取完成後。</span><span class="sxs-lookup"><span data-stu-id="fd29b-157">The following example is after the capture is complete.</span></span> <span data-ttu-id="fd29b-158">PacketCaptureStatus 值為 Stopped，而 StopReason 為 TimeExceeded。</span><span class="sxs-lookup"><span data-stu-id="fd29b-158">The PacketCaptureStatus value is Stopped, with a StopReason of TimeExceeded.</span></span> <span data-ttu-id="fd29b-159">這個值說明封包擷取已順利完成，並執行了它的時間。</span><span class="sxs-lookup"><span data-stu-id="fd29b-159">This value shows that the packet capture was successful and ran its time.</span></span>
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

## <a name="stop-a-packet-capture"></a><span data-ttu-id="fd29b-160">停止封包擷取</span><span class="sxs-lookup"><span data-stu-id="fd29b-160">Stop a packet capture</span></span>

<span data-ttu-id="fd29b-161">藉由執行 `Stop-AzureRmNetworkWatcherPacketCapture` Cmdlet，如果擷取工作階段正在進行中，則會加以停止。</span><span class="sxs-lookup"><span data-stu-id="fd29b-161">By running the `Stop-AzureRmNetworkWatcherPacketCapture` cmdlet, if a capture session is in progress it is stopped.</span></span>

```powershell
Stop-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -PacketCaptureName "PacketCaptureTest"
```

> [!NOTE]
> <span data-ttu-id="fd29b-162">此 Cmdlet 若執行於目前正在執行的擷取工作階段或已停止的現有工作階段，則不會傳回任何回應。</span><span class="sxs-lookup"><span data-stu-id="fd29b-162">The cmdlet returns no response when ran on a currently running capture session or an existing session that has already stopped.</span></span>

## <a name="delete-a-packet-capture"></a><span data-ttu-id="fd29b-163">刪除封包擷取</span><span class="sxs-lookup"><span data-stu-id="fd29b-163">Delete a packet capture</span></span>

```powershell
Remove-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -PacketCaptureName "PacketCaptureTest"
```

> [!NOTE]
> <span data-ttu-id="fd29b-164">刪除封包擷取不會刪除儲存體帳戶中的檔案。</span><span class="sxs-lookup"><span data-stu-id="fd29b-164">Deleting a packet capture does not delete the file in the storage account.</span></span>

## <a name="download-a-packet-capture"></a><span data-ttu-id="fd29b-165">下載封包擷取</span><span class="sxs-lookup"><span data-stu-id="fd29b-165">Download a packet capture</span></span>

<span data-ttu-id="fd29b-166">封包擷取工作階段完成後，即可將擷取檔案上傳到 Blob 儲存體或 VM 上的本機檔案。</span><span class="sxs-lookup"><span data-stu-id="fd29b-166">Once your packet capture session has completed, the capture file can be uploaded to blob storage or to a local file on the VM.</span></span> <span data-ttu-id="fd29b-167">封包擷取的儲存位置會在建立工作階段時定義。</span><span class="sxs-lookup"><span data-stu-id="fd29b-167">The storage location of the packet capture is defined at creation of the session.</span></span> <span data-ttu-id="fd29b-168">若要存取這些儲存至儲存體帳戶的擷取檔案，Microsoft Azure 儲存體總管是很便利的工具，您可以在這裡下載︰http://storageexplorer.com/</span><span class="sxs-lookup"><span data-stu-id="fd29b-168">A convenient tool to access these capture files saved to a storage account is Microsoft Azure Storage Explorer, which can be downloaded here:  http://storageexplorer.com/</span></span>

<span data-ttu-id="fd29b-169">如果指定了儲存體帳戶，封包擷取檔案便會儲存到儲存體帳戶的下列位置︰</span><span class="sxs-lookup"><span data-stu-id="fd29b-169">If a storage account is specified, packet capture files are saved to a storage account at the following location:</span></span>

```
https://{storageAccountName}.blob.core.windows.net/network-watcher-logs/subscriptions/{subscriptionId}/resourcegroups/{storageAccountResourceGroup}/providers/microsoft.compute/virtualmachines/{VMName}/{year}/{month}/{day}/packetCapture_{creationTime}.cap
```

## <a name="next-steps"></a><span data-ttu-id="fd29b-170">後續步驟</span><span class="sxs-lookup"><span data-stu-id="fd29b-170">Next steps</span></span>

<span data-ttu-id="fd29b-171">檢視[建立由警示觸發的封包擷取](network-watcher-alert-triggered-packet-capture.md)來了解如何透過虛擬機器警示自動化封包擷取</span><span class="sxs-lookup"><span data-stu-id="fd29b-171">Learn how to automate packet captures with Virtual machine alerts by viewing [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>

<span data-ttu-id="fd29b-172">造訪[檢查 IP 流量驗證](network-watcher-check-ip-flow-verify-portal.md)來得知 VM 是否允許特定流量流入或流出</span><span class="sxs-lookup"><span data-stu-id="fd29b-172">Find if certain traffic is allowed in orr out of your VM by visiting [Check IP flow verify](network-watcher-check-ip-flow-verify-portal.md)</span></span>

<!-- Image references -->














