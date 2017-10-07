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
# <a name="manage-packet-captures-with-azure-network-watcher-using-powershell"></a><span data-ttu-id="17f00-103">使用 PowerShell 以 Azure 網路監看員管理封包擷取</span><span class="sxs-lookup"><span data-stu-id="17f00-103">Manage packet captures with Azure Network Watcher using PowerShell</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="17f00-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="17f00-104">Azure portal</span></span>](network-watcher-packet-capture-manage-portal.md)
> - [<span data-ttu-id="17f00-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="17f00-105">PowerShell</span></span>](network-watcher-packet-capture-manage-powershell.md)
> - [<span data-ttu-id="17f00-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="17f00-106">CLI 1.0</span></span>](network-watcher-packet-capture-manage-cli-nodejs.md)
> - [<span data-ttu-id="17f00-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="17f00-107">CLI 2.0</span></span>](network-watcher-packet-capture-manage-cli.md)
> - [<span data-ttu-id="17f00-108">Azure REST API</span><span class="sxs-lookup"><span data-stu-id="17f00-108">Azure REST API</span></span>](network-watcher-packet-capture-manage-rest.md)

<span data-ttu-id="17f00-109">網路監看員封包擷取可讓您 toocreate 擷取工作階段 tootrack 流量 tooand 從虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="17f00-109">Network Watcher packet capture allows you toocreate capture sessions tootrack traffic tooand from a virtual machine.</span></span> <span data-ttu-id="17f00-110">篩選器可供 hello 擷取工作階段 tooensure 擷取您想要只 hello 流量。</span><span class="sxs-lookup"><span data-stu-id="17f00-110">Filters are provided for hello capture session tooensure you capture only hello traffic you want.</span></span> <span data-ttu-id="17f00-111">封包擷取可在主動和被動協助 toodiagnose 網路異常狀況。</span><span class="sxs-lookup"><span data-stu-id="17f00-111">Packet capture helps toodiagnose network anomalies both reactively and proactively.</span></span> <span data-ttu-id="17f00-112">其他用途包括收集網路統計資料，取得有關網路入侵，toodebug 用戶端與伺服器通訊，以及執行更多。</span><span class="sxs-lookup"><span data-stu-id="17f00-112">Other uses include gathering network statistics, gaining information on network intrusions, toodebug client-server communications and much more.</span></span> <span data-ttu-id="17f00-113">透過無法 tooremotely 觸發程序封包擷取，這項功能可以減輕工作 hello 負擔的手動和 hello 想要在電腦上，以節省寶貴的時間執行封包擷取。</span><span class="sxs-lookup"><span data-stu-id="17f00-113">By being able tooremotely trigger packet captures, this capability eases hello burden of running a packet capture manually and on hello desired machine, which saves valuable time.</span></span>

<span data-ttu-id="17f00-114">這篇文章帶領您完成 hello 封包擷取目前可用的不同的管理工作。</span><span class="sxs-lookup"><span data-stu-id="17f00-114">This article takes you through hello different management tasks that are currently available for packet capture.</span></span>

- [<span data-ttu-id="17f00-115">**啟動封包擷取**</span><span class="sxs-lookup"><span data-stu-id="17f00-115">**Start a packet capture**</span></span>](#start-a-packet-capture)
- [<span data-ttu-id="17f00-116">**停止封包擷取**</span><span class="sxs-lookup"><span data-stu-id="17f00-116">**Stop a packet capture**</span></span>](#stop-a-packet-capture)
- [<span data-ttu-id="17f00-117">**刪除封包擷取**</span><span class="sxs-lookup"><span data-stu-id="17f00-117">**Delete a packet capture**</span></span>](#delete-a-packet-capture)
- [<span data-ttu-id="17f00-118">**下載封包擷取**</span><span class="sxs-lookup"><span data-stu-id="17f00-118">**Download a packet capture**</span></span>](#download-a-packet-capture)

## <a name="before-you-begin"></a><span data-ttu-id="17f00-119">開始之前</span><span class="sxs-lookup"><span data-stu-id="17f00-119">Before you begin</span></span>

<span data-ttu-id="17f00-120">本文假設您擁有 hello 下列資源：</span><span class="sxs-lookup"><span data-stu-id="17f00-120">This article assumes you have hello following resources:</span></span>

* <span data-ttu-id="17f00-121">執行個體要在 hello 區域網路監看員的 toocreate 封包擷取</span><span class="sxs-lookup"><span data-stu-id="17f00-121">An instance of Network Watcher in hello region you want toocreate a packet capture</span></span>

* <span data-ttu-id="17f00-122">虛擬機器與 hello 封包擷取啟用擴充功能。</span><span class="sxs-lookup"><span data-stu-id="17f00-122">A virtual machine with hello packet capture extension enabled.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="17f00-123">封包擷取需要虛擬機器擴充功能 `AzureNetworkWatcherExtension`。</span><span class="sxs-lookup"><span data-stu-id="17f00-123">Packet capture requires a virtual machine extension `AzureNetworkWatcherExtension`.</span></span> <span data-ttu-id="17f00-124">Hello 擴充功能安裝在 Windows VM 上瀏覽[Azure 網路監看員的代理程式適用於 Windows 的虛擬機器擴充功能](../virtual-machines/windows/extensions-nwa.md)和如 Linux VM，請造訪[Azure 網路監看員的代理程式虛擬機器擴充功能，適用於 Linux](../virtual-machines/linux/extensions-nwa.md).</span><span class="sxs-lookup"><span data-stu-id="17f00-124">For installing hello extension on a Windows VM visit [Azure Network Watcher Agent virtual machine extension for Windows](../virtual-machines/windows/extensions-nwa.md) and for Linux VM visit [Azure Network Watcher Agent virtual machine extension for Linux](../virtual-machines/linux/extensions-nwa.md).</span></span>

## <a name="install-vm-extension"></a><span data-ttu-id="17f00-125">安裝 VM 擴充功能</span><span class="sxs-lookup"><span data-stu-id="17f00-125">Install VM extension</span></span>

### <a name="step-1"></a><span data-ttu-id="17f00-126">步驟 1</span><span class="sxs-lookup"><span data-stu-id="17f00-126">Step 1</span></span>

```powershell
$VM = Get-AzureRmVM -ResourceGroupName testrg -Name VM1
```

### <a name="step-2"></a><span data-ttu-id="17f00-127">步驟 2</span><span class="sxs-lookup"><span data-stu-id="17f00-127">Step 2</span></span>

<span data-ttu-id="17f00-128">hello 擷取 hello 延伸模組資訊的下列範例所需 toorun hello `Set-AzureRmVMExtension` cmdlet。</span><span class="sxs-lookup"><span data-stu-id="17f00-128">hello following example retrieves hello extension information needed toorun hello `Set-AzureRmVMExtension` cmdlet.</span></span> <span data-ttu-id="17f00-129">此 cmdlet 會 hello 客體虛擬機器上安裝 hello 封包擷取代理程式。</span><span class="sxs-lookup"><span data-stu-id="17f00-129">This cmdlet installs hello packet capture agent on hello guest virtual machine.</span></span>

> [!NOTE]
> <span data-ttu-id="17f00-130">hello`Set-AzureRmVMExtension`指令程式可能需要幾分鐘的時間 toocomplete。</span><span class="sxs-lookup"><span data-stu-id="17f00-130">hello `Set-AzureRmVMExtension` cmdlet may take several minutes toocomplete.</span></span>

<span data-ttu-id="17f00-131">若為 Windows 虛擬機器：</span><span class="sxs-lookup"><span data-stu-id="17f00-131">For Windows virtual machines:</span></span>

```powershell
$AzureNetworkWatcherExtension = Get-AzureRmVMExtensionImage -Location WestCentralUS -PublisherName Microsoft.Azure.NetworkWatcher -Type NetworkWatcherAgentWindows -Version 1.4.13.0
$ExtensionName = "AzureNetworkWatcherExtension"
Set-AzureRmVMExtension -ResourceGroupName $VM.ResourceGroupName  -Location $VM.Location -VMName $VM.Name -Name $ExtensionName -Publisher $AzureNetworkWatcherExtension.PublisherName -ExtensionType $AzureNetworkWatcherExtension.Type -TypeHandlerVersion $AzureNetworkWatcherExtension.Version.Substring(0,3)
```

<span data-ttu-id="17f00-132">若為 Linux 虛擬機器：</span><span class="sxs-lookup"><span data-stu-id="17f00-132">For Linux virtual machines:</span></span>

```powershell
$AzureNetworkWatcherExtension = Get-AzureRmVMExtensionImage -Location WestCentralUS -PublisherName Microsoft.Azure.NetworkWatcher -Type NetworkWatcherAgentLinux -Version 1.4.13.0
$ExtensionName = "AzureNetworkWatcherExtension"
Set-AzureRmVMExtension -ResourceGroupName $VM.ResourceGroupName  -Location $VM.Location -VMName $VM.Name -Name $ExtensionName -Publisher $AzureNetworkWatcherExtension.PublisherName -ExtensionType $AzureNetworkWatcherExtension.Type -TypeHandlerVersion $AzureNetworkWatcherExtension.Version.Substring(0,3)
````

<span data-ttu-id="17f00-133">hello 下列範例是成功的回應之後執行 hello `Set-AzureRmVMExtension` cmdlet。</span><span class="sxs-lookup"><span data-stu-id="17f00-133">hello following example is a successful response after running hello `Set-AzureRmVMExtension` cmdlet.</span></span>

```
RequestId IsSuccessStatusCode StatusCode ReasonPhrase
--------- ------------------- ---------- ------------
                         True         OK OK   
```

### <a name="step-3"></a><span data-ttu-id="17f00-134">步驟 3</span><span class="sxs-lookup"><span data-stu-id="17f00-134">Step 3</span></span>

<span data-ttu-id="17f00-135">tooensure hello 代理程式的安裝，執行 hello `Get-AzureRmVMExtension` cmdlet 並將它傳遞 hello 虛擬機器名稱與 hello 延伸模組名稱。</span><span class="sxs-lookup"><span data-stu-id="17f00-135">tooensure that hello agent is installed, run hello `Get-AzureRmVMExtension` cmdlet and pass it hello virtual machine name and hello extension name.</span></span>

```powershell
Get-AzureRmVMExtension -ResourceGroupName $VM.ResourceGroupName  -VMName $VM.Name -Name $ExtensionName
```

<span data-ttu-id="17f00-136">下列範例中的 hello 是執行 hello 回應的範例`Get-AzureRmVMExtension`</span><span class="sxs-lookup"><span data-stu-id="17f00-136">hello following sample is an example of hello response from running `Get-AzureRmVMExtension`</span></span>

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

## <a name="start-a-packet-capture"></a><span data-ttu-id="17f00-137">啟動封包擷取</span><span class="sxs-lookup"><span data-stu-id="17f00-137">Start a packet capture</span></span>

<span data-ttu-id="17f00-138">Hello 前面的步驟完成後，hello 虛擬機器上安裝 hello 封包擷取代理程式。</span><span class="sxs-lookup"><span data-stu-id="17f00-138">Once hello preceding steps are complete, hello packet capture agent is installed on hello virtual machine.</span></span>

### <a name="step-1"></a><span data-ttu-id="17f00-139">步驟 1</span><span class="sxs-lookup"><span data-stu-id="17f00-139">Step 1</span></span>

<span data-ttu-id="17f00-140">hello 下一個步驟是 tooretrieve hello 網路監看員執行個體。</span><span class="sxs-lookup"><span data-stu-id="17f00-140">hello next step is tooretrieve hello Network Watcher instance.</span></span> <span data-ttu-id="17f00-141">這個變數會傳遞 toohello`New-AzureRmNetworkWatcherPacketCapture`步驟 4 中的 cmdlet。</span><span class="sxs-lookup"><span data-stu-id="17f00-141">This variable is passed toohello `New-AzureRmNetworkWatcherPacketCapture` cmdlet in step 4.</span></span>

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" }
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName  
```

### <a name="step-2"></a><span data-ttu-id="17f00-142">步驟 2</span><span class="sxs-lookup"><span data-stu-id="17f00-142">Step 2</span></span>

<span data-ttu-id="17f00-143">擷取儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="17f00-143">Retrieve a storage account.</span></span> <span data-ttu-id="17f00-144">這個儲存體帳戶是使用的 toostore hello 封包擷取檔案。</span><span class="sxs-lookup"><span data-stu-id="17f00-144">This storage account is used toostore hello packet capture file.</span></span>

```powershell
$storageAccount = Get-AzureRmStorageAccount -ResourceGroupName testrg -Name testrgsa123
```

### <a name="step-3"></a><span data-ttu-id="17f00-145">步驟 3</span><span class="sxs-lookup"><span data-stu-id="17f00-145">Step 3</span></span>

<span data-ttu-id="17f00-146">篩選可使用的 toolimit hello 資料儲存的 hello 封包擷取。</span><span class="sxs-lookup"><span data-stu-id="17f00-146">Filters can be used toolimit hello data that is stored by hello packet capture.</span></span> <span data-ttu-id="17f00-147">hello 下列範例設定兩個篩選條件。</span><span class="sxs-lookup"><span data-stu-id="17f00-147">hello following example sets up two filters.</span></span>  <span data-ttu-id="17f00-148">一個篩選條件會收集傳出 TCP 流量只會從本機 IP 10.0.0.3 toodestination 連接埠 20、 80 和 443。</span><span class="sxs-lookup"><span data-stu-id="17f00-148">One filter collects outgoing TCP traffic only from local IP 10.0.0.3 toodestination ports 20, 80 and 443.</span></span>  <span data-ttu-id="17f00-149">hello 第二個篩選會收集只有 UDP 流量。</span><span class="sxs-lookup"><span data-stu-id="17f00-149">hello second filter collects only UDP traffic.</span></span>

```powershell
$filter1 = New-AzureRmPacketCaptureFilterConfig -Protocol TCP -RemoteIPAddress "1.1.1.1-255.255.255" -LocalIPAddress "10.0.0.3" -LocalPort "1-65535" -RemotePort "20;80;443"
$filter2 = New-AzureRmPacketCaptureFilterConfig -Protocol UDP
```

> [!NOTE]
> <span data-ttu-id="17f00-150">一個封包擷取可以定義多個篩選器。</span><span class="sxs-lookup"><span data-stu-id="17f00-150">Multiple filters can be defined for a packet capture.</span></span>

### <a name="step-4"></a><span data-ttu-id="17f00-151">步驟 4</span><span class="sxs-lookup"><span data-stu-id="17f00-151">Step 4</span></span>

<span data-ttu-id="17f00-152">執行 hello `New-AzureRmNetworkWatcherPacketCapture` cmdlet toostart hello 封包擷取程序，傳遞所需的 hello hello 先前步驟中所擷取的值。</span><span class="sxs-lookup"><span data-stu-id="17f00-152">Run hello `New-AzureRmNetworkWatcherPacketCapture` cmdlet toostart hello packet capture process, passing hello required values retrieved in hello preceding steps.</span></span>
```powershell

New-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -TargetVirtualMachineId $vm.Id -PacketCaptureName "PacketCaptureTest" -StorageAccountId $storageAccount.id -TimeLimitInSeconds 60 -Filters $filter1, $filter2
```

<span data-ttu-id="17f00-153">hello 下列範例是執行 hello hello 預期輸出`New-AzureRmNetworkWatcherPacketCapture`cmdlet。</span><span class="sxs-lookup"><span data-stu-id="17f00-153">hello following example is hello expected output from running hello `New-AzureRmNetworkWatcherPacketCapture` cmdlet.</span></span>

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

## <a name="get-a-packet-capture"></a><span data-ttu-id="17f00-154">取得封包擷取</span><span class="sxs-lookup"><span data-stu-id="17f00-154">Get a packet capture</span></span>

<span data-ttu-id="17f00-155">執行 hello `Get-AzureRmNetworkWatcherPacketCapture` cmdlet，擷取目前正在執行，或已完成的封包擷取 hello 狀態。</span><span class="sxs-lookup"><span data-stu-id="17f00-155">Running hello `Get-AzureRmNetworkWatcherPacketCapture` cmdlet, retrieves hello status of a currently running, or completed packet capture.</span></span>

```powershell
Get-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -PacketCaptureName "PacketCaptureTest"
```

<span data-ttu-id="17f00-156">hello 下列範例是 hello 輸出 hello `Get-AzureRmNetworkWatcherPacketCapture` cmdlet。</span><span class="sxs-lookup"><span data-stu-id="17f00-156">hello following example is hello output from hello `Get-AzureRmNetworkWatcherPacketCapture` cmdlet.</span></span> <span data-ttu-id="17f00-157">hello 下列範例是 hello 擷取完成後。</span><span class="sxs-lookup"><span data-stu-id="17f00-157">hello following example is after hello capture is complete.</span></span> <span data-ttu-id="17f00-158">將停止 hello PacketCaptureStatus 值 StopReason TimeExceeded。</span><span class="sxs-lookup"><span data-stu-id="17f00-158">hello PacketCaptureStatus value is Stopped, with a StopReason of TimeExceeded.</span></span> <span data-ttu-id="17f00-159">這個值會顯示 hello 封包擷取已順利完成，並執行它的時間。</span><span class="sxs-lookup"><span data-stu-id="17f00-159">This value shows that hello packet capture was successful and ran its time.</span></span>
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

## <a name="stop-a-packet-capture"></a><span data-ttu-id="17f00-160">停止封包擷取</span><span class="sxs-lookup"><span data-stu-id="17f00-160">Stop a packet capture</span></span>

<span data-ttu-id="17f00-161">藉由執行 hello `Stop-AzureRmNetworkWatcherPacketCapture` cmdlet 時，如果擷取工作階段正在進行中它已停止。</span><span class="sxs-lookup"><span data-stu-id="17f00-161">By running hello `Stop-AzureRmNetworkWatcherPacketCapture` cmdlet, if a capture session is in progress it is stopped.</span></span>

```powershell
Stop-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -PacketCaptureName "PacketCaptureTest"
```

> [!NOTE]
> <span data-ttu-id="17f00-162">hello cmdlet 會傳回任何回應時執行的目前執行的擷取工作階段或現有的工作階段已經停止。</span><span class="sxs-lookup"><span data-stu-id="17f00-162">hello cmdlet returns no response when ran on a currently running capture session or an existing session that has already stopped.</span></span>

## <a name="delete-a-packet-capture"></a><span data-ttu-id="17f00-163">刪除封包擷取</span><span class="sxs-lookup"><span data-stu-id="17f00-163">Delete a packet capture</span></span>

```powershell
Remove-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -PacketCaptureName "PacketCaptureTest"
```

> [!NOTE]
> <span data-ttu-id="17f00-164">刪除封包擷取並不會刪除 hello 儲存體帳戶中的 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="17f00-164">Deleting a packet capture does not delete hello file in hello storage account.</span></span>

## <a name="download-a-packet-capture"></a><span data-ttu-id="17f00-165">下載封包擷取</span><span class="sxs-lookup"><span data-stu-id="17f00-165">Download a packet capture</span></span>

<span data-ttu-id="17f00-166">您的封包擷取工作階段完成後，請 hello 擷取檔案可上傳的 tooblob 儲存體或 tooa 本機檔案 hello VM 上。</span><span class="sxs-lookup"><span data-stu-id="17f00-166">Once your packet capture session has completed, hello capture file can be uploaded tooblob storage or tooa local file on hello VM.</span></span> <span data-ttu-id="17f00-167">hello 封包擷取 hello 儲存位置被定義在 hello 工作階段的建立。</span><span class="sxs-lookup"><span data-stu-id="17f00-167">hello storage location of hello packet capture is defined at creation of hello session.</span></span> <span data-ttu-id="17f00-168">方便的工具 tooaccess 這些擷取的檔案儲存的 tooa 儲存體帳戶是 Microsoft Azure 儲存體總管 中，這可以在這裡下載： http://storageexplorer.com/</span><span class="sxs-lookup"><span data-stu-id="17f00-168">A convenient tool tooaccess these capture files saved tooa storage account is Microsoft Azure Storage Explorer, which can be downloaded here:  http://storageexplorer.com/</span></span>

<span data-ttu-id="17f00-169">如果指定的儲存體帳戶，則封包擷取檔案會儲存在下列位置的 hello tooa 儲存體帳戶：</span><span class="sxs-lookup"><span data-stu-id="17f00-169">If a storage account is specified, packet capture files are saved tooa storage account at hello following location:</span></span>

```
https://{storageAccountName}.blob.core.windows.net/network-watcher-logs/subscriptions/{subscriptionId}/resourcegroups/{storageAccountResourceGroup}/providers/microsoft.compute/virtualmachines/{VMName}/{year}/{month}/{day}/packetCapture_{creationTime}.cap
```

## <a name="next-steps"></a><span data-ttu-id="17f00-170">後續步驟</span><span class="sxs-lookup"><span data-stu-id="17f00-170">Next steps</span></span>

<span data-ttu-id="17f00-171">了解如何 tooautomate 封包擷取虛擬機器警示藉由檢視[建立警示觸發的封包擷取](network-watcher-alert-triggered-packet-capture.md)</span><span class="sxs-lookup"><span data-stu-id="17f00-171">Learn how tooautomate packet captures with Virtual machine alerts by viewing [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>

<span data-ttu-id="17f00-172">造訪[檢查 IP 流量驗證](network-watcher-check-ip-flow-verify-portal.md)來得知 VM 是否允許特定流量流入或流出</span><span class="sxs-lookup"><span data-stu-id="17f00-172">Find if certain traffic is allowed in orr out of your VM by visiting [Check IP flow verify](network-watcher-check-ip-flow-verify-portal.md)</span></span>

<!-- Image references -->














