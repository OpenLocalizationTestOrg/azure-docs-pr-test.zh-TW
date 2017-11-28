---
title: "使用 Azure 網路監看員管理封包擷取 - Azure CLI 1.0 | Microsoft Docs"
description: "此頁面說明如何使用 Azure CLI 1.0 管理網路監看員的封包擷取功能"
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
ms.openlocfilehash: 91588910334859c1ea77186674d5bfb31b311b36
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="manage-packet-captures-with-azure-network-watcher-using-azure-cli-10"></a><span data-ttu-id="3eb26-103">使用 Azure CLI 1.0，利用 Azure 網路監看員管理封包擷取</span><span class="sxs-lookup"><span data-stu-id="3eb26-103">Manage packet captures with Azure Network Watcher using Azure CLI 1.0</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="3eb26-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="3eb26-104">Azure portal</span></span>](network-watcher-packet-capture-manage-portal.md)
> - [<span data-ttu-id="3eb26-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="3eb26-105">PowerShell</span></span>](network-watcher-packet-capture-manage-powershell.md)
> - [<span data-ttu-id="3eb26-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="3eb26-106">CLI 1.0</span></span>](network-watcher-packet-capture-manage-cli-nodejs.md)
> - [<span data-ttu-id="3eb26-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="3eb26-107">CLI 2.0</span></span>](network-watcher-packet-capture-manage-cli.md)
> - [<span data-ttu-id="3eb26-108">Azure REST API</span><span class="sxs-lookup"><span data-stu-id="3eb26-108">Azure REST API</span></span>](network-watcher-packet-capture-manage-rest.md)

<span data-ttu-id="3eb26-109">網路監看員封包擷取可讓您建立擷取工作階段來追蹤虛擬機器的流入和流出流量。</span><span class="sxs-lookup"><span data-stu-id="3eb26-109">Network Watcher packet capture allows you to create capture sessions to track traffic to and from a virtual machine.</span></span> <span data-ttu-id="3eb26-110">系統會為擷取工作階段提供篩選器，以確保您只會擷取到您想要的流量。</span><span class="sxs-lookup"><span data-stu-id="3eb26-110">Filters are provided for the capture session to ensure you capture only the traffic you want.</span></span> <span data-ttu-id="3eb26-111">封包擷取有助於被動和主動地診斷網路異常。</span><span class="sxs-lookup"><span data-stu-id="3eb26-111">Packet capture helps to diagnose network anomalies both reactively and proactively.</span></span> <span data-ttu-id="3eb26-112">其他用途包括收集網路統計資料、取得有關網路入侵的資訊，以及偵錯用戶端與伺服器間的通訊等等。</span><span class="sxs-lookup"><span data-stu-id="3eb26-112">Other uses include gathering network statistics, gaining information on network intrusions, to debug client-server communications and much more.</span></span> <span data-ttu-id="3eb26-113">藉由能夠從遠端觸發封包擷取，這項功能可以減輕在所需機器上手動執行封包擷取的工作負擔，進而省下寶貴的時間。</span><span class="sxs-lookup"><span data-stu-id="3eb26-113">By being able to remotely trigger packet captures, this capability eases the burden of running a packet capture manually and on the desired machine, which saves valuable time.</span></span>

<span data-ttu-id="3eb26-114">本文使用跨平台 Azure CLI 1.0，這適用於 Windows、Mac 和 Linux。</span><span class="sxs-lookup"><span data-stu-id="3eb26-114">This article uses cross-platform Azure CLI 1.0, which is available for Windows, Mac and Linux.</span></span>

<span data-ttu-id="3eb26-115">本文會帶領您逐步完成封包擷取目前可用的不同管理工作。</span><span class="sxs-lookup"><span data-stu-id="3eb26-115">This article takes you through the different management tasks that are currently available for packet capture.</span></span>

- [<span data-ttu-id="3eb26-116">**啟動封包擷取**</span><span class="sxs-lookup"><span data-stu-id="3eb26-116">**Start a packet capture**</span></span>](#start-a-packet-capture)
- [<span data-ttu-id="3eb26-117">**停止封包擷取**</span><span class="sxs-lookup"><span data-stu-id="3eb26-117">**Stop a packet capture**</span></span>](#stop-a-packet-capture)
- [<span data-ttu-id="3eb26-118">**刪除封包擷取**</span><span class="sxs-lookup"><span data-stu-id="3eb26-118">**Delete a packet capture**</span></span>](#delete-a-packet-capture)
- [<span data-ttu-id="3eb26-119">**下載封包擷取**</span><span class="sxs-lookup"><span data-stu-id="3eb26-119">**Download a packet capture**</span></span>](#download-a-packet-capture)

## <a name="before-you-begin"></a><span data-ttu-id="3eb26-120">開始之前</span><span class="sxs-lookup"><span data-stu-id="3eb26-120">Before you begin</span></span>

<span data-ttu-id="3eb26-121">本文假設您具有下列資源：</span><span class="sxs-lookup"><span data-stu-id="3eb26-121">This article assumes you have the following resources:</span></span>

- <span data-ttu-id="3eb26-122">您想要用來建立封包擷取之區域中的網路監看員執行個體</span><span class="sxs-lookup"><span data-stu-id="3eb26-122">An instance of Network Watcher in the region you want to create a packet capture</span></span>
- <span data-ttu-id="3eb26-123">已啟用封包擷取擴充功能的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="3eb26-123">A virtual machine with the packet capture extension enabled.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3eb26-124">封包擷取需要在虛擬機器上執行代理程式。</span><span class="sxs-lookup"><span data-stu-id="3eb26-124">Packet capture requires an agent to be running on the virtual machine.</span></span> <span data-ttu-id="3eb26-125">代理程式會安裝為擴充功能。</span><span class="sxs-lookup"><span data-stu-id="3eb26-125">The Agent is installed as an extension.</span></span> <span data-ttu-id="3eb26-126">如需 VM 擴充功能的指示，請瀏覽[虛擬機器擴充功能和功能](../virtual-machines/windows/extensions-features.md)。</span><span class="sxs-lookup"><span data-stu-id="3eb26-126">For instructions on VM extensions, visit [Virtual Machine extensions and features](../virtual-machines/windows/extensions-features.md).</span></span>

## <a name="install-vm-extension"></a><span data-ttu-id="3eb26-127">安裝 VM 擴充功能</span><span class="sxs-lookup"><span data-stu-id="3eb26-127">Install VM extension</span></span>

### <a name="step-1"></a><span data-ttu-id="3eb26-128">步驟 1</span><span class="sxs-lookup"><span data-stu-id="3eb26-128">Step 1</span></span>

<span data-ttu-id="3eb26-129">執行 `azure vm extension set` Cmdlet 在客體虛擬機器上安裝封包擷取代理程式。</span><span class="sxs-lookup"><span data-stu-id="3eb26-129">Run the `azure vm extension set` cmdlet to install the packet capture agent on the guest virtual machine.</span></span>

<span data-ttu-id="3eb26-130">若為 Windows 虛擬機器：</span><span class="sxs-lookup"><span data-stu-id="3eb26-130">For Windows virtual machines:</span></span>

```azurecli
azure vm extension set -g resourceGroupName -m virtualMachineName -p Microsoft.Azure.NetworkWatcher -r AzureNetworkWatcherExtension -n NetworkWatcherAgentWindows -o 1.4
```

<span data-ttu-id="3eb26-131">若為 Linux 虛擬機器：</span><span class="sxs-lookup"><span data-stu-id="3eb26-131">For Linux virtual machines:</span></span>

```azurecli
azure vm extension set -g resourceGroupName -m virtualMachineName -p Microsoft.Azure.NetworkWatcher -r AzureNetworkWatcherExtension -n NetworkWatcherAgentLinux -o 1.4
````

### <a name="step-2"></a><span data-ttu-id="3eb26-132">步驟 2</span><span class="sxs-lookup"><span data-stu-id="3eb26-132">Step 2</span></span>

<span data-ttu-id="3eb26-133">為了確定是否已安裝代理程式，請執行 `vm extension get` Cmdlet，並將資源群組和虛擬機器名稱傳遞給它。</span><span class="sxs-lookup"><span data-stu-id="3eb26-133">To ensure that the agent is installed, run the `vm extension get` cmdlet and pass it the resource group and virtual machine name.</span></span> <span data-ttu-id="3eb26-134">檢查結果清單以確定代理程式已安裝。</span><span class="sxs-lookup"><span data-stu-id="3eb26-134">Check the resulting list to ensure the agent is installed.</span></span>

```azurecli
azure vm extension get -g resourceGroupName -m virtualMachineName
```

<span data-ttu-id="3eb26-135">下列範例是執行 `azure vm extension get` 所得回應的範例</span><span class="sxs-lookup"><span data-stu-id="3eb26-135">The following sample is an example of the response from running `azure vm extension get`</span></span>

```
info:    Executing command vm extension get
+ Looking up the VM "virtualMachineName"
data:    Publisher                       Name                        Version  State
data:    ------------------------------  -----------------------     -------  ---------
data:    Microsoft.Azure.NetworkWatcher  NetworkWatcherAgentWindows  1.4      Succeeded
info:    vm extension get command OK
```

## <a name="start-a-packet-capture"></a><span data-ttu-id="3eb26-136">啟動封包擷取</span><span class="sxs-lookup"><span data-stu-id="3eb26-136">Start a packet capture</span></span>

<span data-ttu-id="3eb26-137">完成上述步驟之後，虛擬機器上便已安裝封包擷取代理程式。</span><span class="sxs-lookup"><span data-stu-id="3eb26-137">Once the preceding steps are complete, the packet capture agent is installed on the virtual machine.</span></span>

### <a name="step-1"></a><span data-ttu-id="3eb26-138">步驟 1</span><span class="sxs-lookup"><span data-stu-id="3eb26-138">Step 1</span></span>

<span data-ttu-id="3eb26-139">下一步是擷取網路監看員執行個體。</span><span class="sxs-lookup"><span data-stu-id="3eb26-139">The next step is to retrieve the Network Watcher instance.</span></span> <span data-ttu-id="3eb26-140">此變數會在步驟 4 傳遞至 `network watcher show` Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="3eb26-140">This variable is passed to the `network watcher show` cmdlet in step 4.</span></span>

```azurecli
azure network watcher show -g resourceGroup -n networkWatcherName
```

### <a name="step-2"></a><span data-ttu-id="3eb26-141">步驟 2</span><span class="sxs-lookup"><span data-stu-id="3eb26-141">Step 2</span></span>

<span data-ttu-id="3eb26-142">擷取儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="3eb26-142">Retrieve a storage account.</span></span> <span data-ttu-id="3eb26-143">此儲存體帳戶會用來儲存封包擷取檔案。</span><span class="sxs-lookup"><span data-stu-id="3eb26-143">This storage account is used to store the packet capture file.</span></span>

```azurecli
azure storage account list
```

### <a name="step-3"></a><span data-ttu-id="3eb26-144">步驟 3</span><span class="sxs-lookup"><span data-stu-id="3eb26-144">Step 3</span></span>

<span data-ttu-id="3eb26-145">可使用篩選器來限制封包擷取所儲存的資料。</span><span class="sxs-lookup"><span data-stu-id="3eb26-145">Filters can be used to limit the data that is stored by the packet capture.</span></span> <span data-ttu-id="3eb26-146">下列範例會設定具有多個篩選器的封包擷取。</span><span class="sxs-lookup"><span data-stu-id="3eb26-146">The following example sets up a packet capture with several  filters.</span></span>  <span data-ttu-id="3eb26-147">前三個篩選器只會收集從本機 IP 10.0.0.3 流往目的地連接埠 20、80 和 443 的連出 TCP 流量。</span><span class="sxs-lookup"><span data-stu-id="3eb26-147">The first three filters collect outgoing TCP traffic only from local IP 10.0.0.3 to destination ports 20, 80 and 443.</span></span>  <span data-ttu-id="3eb26-148">最後一個篩選器只會收集 UDP 流量。</span><span class="sxs-lookup"><span data-stu-id="3eb26-148">The last filter collects only UDP traffic.</span></span>

```azurecli
azure network watcher packet-capture create -g resourceGroupName -w networkWatcherName -n packetCaptureName -t targetResourceId -o storageAccountResourceId -f "[{\"protocol\":\"TCP\", \"remoteIPAddress\":\"1.1.1.1-255.255.255\",\"localIPAddress\":\"10.0.0.3\", \"remotePort\":\"20\"},{\"protocol\":\"TCP\", \"remoteIPAddress\":\"1.1.1.1-255.255.255\",\"localIPAddress\":\"10.0.0.3\", \"remotePort\":\"80\"},{\"protocol\":\"TCP\", \"remoteIPAddress\":\"1.1.1.1-255.255.255\",\"localIPAddress\":\"10.0.0.3\", \"remotePort\":\"443\"},{\"protocol\":\"UDP\"}]"
```

<span data-ttu-id="3eb26-149">一個封包擷取可以定義多個篩選器。</span><span class="sxs-lookup"><span data-stu-id="3eb26-149">Multiple filters can be defined for a packet capture.</span></span> <span data-ttu-id="3eb26-150">如果您使用複雜的篩選器結構，則最好使用 json 檔案形式的篩選器來避免發生語法錯誤。</span><span class="sxs-lookup"><span data-stu-id="3eb26-150">If you are using a complex filter structure, it is better to use filters as a json file to avoid syntax errors.</span></span> <span data-ttu-id="3eb26-151">比方說，使用旗標 "-r" (而不是 "-f") 並傳遞包含下列篩選器之 json 檔案的位置︰</span><span class="sxs-lookup"><span data-stu-id="3eb26-151">For example, use the flag "-r" (instead of "-f") and pass the location of a json file containing the following filters:</span></span>

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


<span data-ttu-id="3eb26-152">下列範例是執行 `network watcher packet-capture create` Cmdlet 後預期會得到的輸出。</span><span class="sxs-lookup"><span data-stu-id="3eb26-152">The following example is the expected output from running the `network watcher packet-capture create` cmdlet.</span></span>

```
data:    Name                            : packetCaptureName
data:    Etag                            : W/"d59bb2d2-dc95-43da-b740-e0ef8fcacecb"
data:    Target                          : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/resourceGroupName/providers/Microsoft.Compute/virtualMachines/testVM
data:    Bytes To Capture Per Packet     : 0
data:    Total Bytes Per Session         : 1073741824
data:    Time Limit In Seconds           : 18000
data:    Storage Location:
data:      Storage Id                    : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/resourceGroupName/providers/Microsoft.Storage/storageAccounts/testStorage
data:      Storage Path                  : https://testStorage.blob.core.windows.net/network-watcher-logs/subscriptions/00000000-0000-0000-0000-000000000000/resourcegroups/testRG/providers/microsoft.compute/virtualmachines/testVM/2017/02/17/packetcapture_01_21_18_145.cap
data:    Filters                         : []
data:    Provisioning State              : Succeeded
info:    network watcher packet-capture create command OK
```

## <a name="get-a-packet-capture"></a><span data-ttu-id="3eb26-153">取得封包擷取</span><span class="sxs-lookup"><span data-stu-id="3eb26-153">Get a packet capture</span></span>

<span data-ttu-id="3eb26-154">執行 `network watcher packet-capture show` Cmdlet 以擷取目前正在執行或已完成之封包擷取的狀態。</span><span class="sxs-lookup"><span data-stu-id="3eb26-154">Running the `network watcher packet-capture show` cmdlet, retrieves the status of a currently running, or completed packet capture.</span></span>

```azurecli
azure network watcher packet-capture show -g resourceGroupName -w networkWatcherName -n packetCaptureName
```

<span data-ttu-id="3eb26-155">下列範例是 `network watcher packet-capture show` Cmdlet 的輸出。</span><span class="sxs-lookup"><span data-stu-id="3eb26-155">The following example is the output from the `network watcher packet-capture show` cmdlet.</span></span> <span data-ttu-id="3eb26-156">下列範例是在擷取完成後。</span><span class="sxs-lookup"><span data-stu-id="3eb26-156">The following example is after the capture is complete.</span></span> <span data-ttu-id="3eb26-157">PacketCaptureStatus 值為 Stopped，而 StopReason 為 TimeExceeded。</span><span class="sxs-lookup"><span data-stu-id="3eb26-157">The PacketCaptureStatus value is Stopped, with a StopReason of TimeExceeded.</span></span> <span data-ttu-id="3eb26-158">這個值說明封包擷取已順利完成，並執行了它的時間。</span><span class="sxs-lookup"><span data-stu-id="3eb26-158">This value shows that the packet capture was successful and ran its time.</span></span>

```
data:    Name                            : packetCaptureName
data:    Etag                            : W/"d59bb2d2-dc95-43da-b740-e0ef8fcacecb"
data:    Target                          : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/resourceGroupName/providers/Microsoft.Compute/virtualMachines/testVM
data:    Bytes To Capture Per Packet     : 0
data:    Total Bytes Per Session         : 1073741824
data:    Time Limit In Seconds           : 18000
data:    Storage Location:
data:      Storage Id                    : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/resourceGroupName/providers/Microsoft.Storage/storageAccounts/testStorage
data:      Storage Path                  : https://testStorage.blob.core.windows.net/network-watcher-logs/subscriptions/00000000-0000-0000-0000-000000000000/resourcegroups/testRG/providers/microsoft.compute/virtualmachines/testVM/2017/02/17/packetcapture_01_21_18_145.cap
data:    Filters                         : []
data:    Provisioning State              : Succeeded
info:    network watcher packet-capture show command OK
```

## <a name="stop-a-packet-capture"></a><span data-ttu-id="3eb26-159">停止封包擷取</span><span class="sxs-lookup"><span data-stu-id="3eb26-159">Stop a packet capture</span></span>

<span data-ttu-id="3eb26-160">藉由執行 `network watcher packet-capture stop` Cmdlet，如果擷取工作階段正在進行中，則會加以停止。</span><span class="sxs-lookup"><span data-stu-id="3eb26-160">By running the `network watcher packet-capture stop` cmdlet, if a capture session is in progress it is stopped.</span></span>

```azurecli
azure network watcher packet-capture stop -g resourceGroupName -w networkWatcherName -n packetCaptureName
```

> [!NOTE]
> <span data-ttu-id="3eb26-161">此 Cmdlet 若執行於目前正在執行的擷取工作階段或已停止的現有工作階段，則不會傳回任何回應。</span><span class="sxs-lookup"><span data-stu-id="3eb26-161">The cmdlet returns no response when ran on a currently running capture session or an existing session that has already stopped.</span></span>

## <a name="delete-a-packet-capture"></a><span data-ttu-id="3eb26-162">刪除封包擷取</span><span class="sxs-lookup"><span data-stu-id="3eb26-162">Delete a packet capture</span></span>

```azurecli
azure network watcher packet-capture delete -g resourceGroupName -w networkWatcherName -n packetCaptureName
```

> [!NOTE]
> <span data-ttu-id="3eb26-163">刪除封包擷取不會刪除儲存體帳戶中的檔案。</span><span class="sxs-lookup"><span data-stu-id="3eb26-163">Deleting a packet capture does not delete the file in the storage account.</span></span>

## <a name="download-a-packet-capture"></a><span data-ttu-id="3eb26-164">下載封包擷取</span><span class="sxs-lookup"><span data-stu-id="3eb26-164">Download a packet capture</span></span>

<span data-ttu-id="3eb26-165">封包擷取工作階段完成後，即可將擷取檔案上傳到 Blob 儲存體或 VM 上的本機檔案。</span><span class="sxs-lookup"><span data-stu-id="3eb26-165">Once your packet capture session has completed, the capture file can be uploaded to blob storage or to a local file on the VM.</span></span> <span data-ttu-id="3eb26-166">封包擷取的儲存位置會在建立工作階段時定義。</span><span class="sxs-lookup"><span data-stu-id="3eb26-166">The storage location of the packet capture is defined at creation of the session.</span></span> <span data-ttu-id="3eb26-167">若要存取這些儲存至儲存體帳戶的擷取檔案，Microsoft Azure 儲存體總管是很便利的工具，您可以在這裡下載︰http://storageexplorer.com/</span><span class="sxs-lookup"><span data-stu-id="3eb26-167">A convenient tool to access these capture files saved to a storage account is Microsoft Azure Storage Explorer, which can be downloaded here:  http://storageexplorer.com/</span></span>

<span data-ttu-id="3eb26-168">如果指定了儲存體帳戶，封包擷取檔案便會儲存到儲存體帳戶的下列位置︰</span><span class="sxs-lookup"><span data-stu-id="3eb26-168">If a storage account is specified, packet capture files are saved to a storage account at the following location:</span></span>

```
https://{storageAccountName}.blob.core.windows.net/network-watcher-logs/subscriptions/{subscriptionId}/resourcegroups/{storageAccountResourceGroup}/providers/microsoft.compute/virtualmachines/{VMName}/{year}/{month}/{day}/packetCapture_{creationTime}.cap
```

## <a name="next-steps"></a><span data-ttu-id="3eb26-169">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3eb26-169">Next steps</span></span>

<span data-ttu-id="3eb26-170">檢視[建立由警示觸發的封包擷取](network-watcher-alert-triggered-packet-capture.md)來了解如何透過虛擬機器警示自動化封包擷取</span><span class="sxs-lookup"><span data-stu-id="3eb26-170">Learn how to automate packet captures with Virtual machine alerts by viewing [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>

<span data-ttu-id="3eb26-171">造訪[檢查 IP 流量驗證](network-watcher-check-ip-flow-verify-portal.md)來得知 VM 是否允許特定流量流入或流出</span><span class="sxs-lookup"><span data-stu-id="3eb26-171">Find if certain traffic is allowed in or out of your VM by visiting [Check IP flow verify](network-watcher-check-ip-flow-verify-portal.md)</span></span>

<!-- Image references -->
