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
# <a name="manage-packet-captures-with-azure-network-watcher-using-azure-cli-10"></a><span data-ttu-id="e2010-103">使用 Azure CLI 1.0，利用 Azure 網路監看員管理封包擷取</span><span class="sxs-lookup"><span data-stu-id="e2010-103">Manage packet captures with Azure Network Watcher using Azure CLI 1.0</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="e2010-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="e2010-104">Azure portal</span></span>](network-watcher-packet-capture-manage-portal.md)
> - [<span data-ttu-id="e2010-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e2010-105">PowerShell</span></span>](network-watcher-packet-capture-manage-powershell.md)
> - [<span data-ttu-id="e2010-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="e2010-106">CLI 1.0</span></span>](network-watcher-packet-capture-manage-cli-nodejs.md)
> - [<span data-ttu-id="e2010-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="e2010-107">CLI 2.0</span></span>](network-watcher-packet-capture-manage-cli.md)
> - [<span data-ttu-id="e2010-108">Azure REST API</span><span class="sxs-lookup"><span data-stu-id="e2010-108">Azure REST API</span></span>](network-watcher-packet-capture-manage-rest.md)

<span data-ttu-id="e2010-109">網路監看員封包擷取可讓您 toocreate 擷取工作階段 tootrack 流量 tooand 從虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="e2010-109">Network Watcher packet capture allows you toocreate capture sessions tootrack traffic tooand from a virtual machine.</span></span> <span data-ttu-id="e2010-110">篩選器可供 hello 擷取工作階段 tooensure 擷取您想要只 hello 流量。</span><span class="sxs-lookup"><span data-stu-id="e2010-110">Filters are provided for hello capture session tooensure you capture only hello traffic you want.</span></span> <span data-ttu-id="e2010-111">封包擷取可在主動和被動協助 toodiagnose 網路異常狀況。</span><span class="sxs-lookup"><span data-stu-id="e2010-111">Packet capture helps toodiagnose network anomalies both reactively and proactively.</span></span> <span data-ttu-id="e2010-112">其他用途包括收集網路統計資料，取得有關網路入侵，toodebug 用戶端與伺服器通訊，以及執行更多。</span><span class="sxs-lookup"><span data-stu-id="e2010-112">Other uses include gathering network statistics, gaining information on network intrusions, toodebug client-server communications and much more.</span></span> <span data-ttu-id="e2010-113">透過無法 tooremotely 觸發程序封包擷取，這項功能可以減輕工作 hello 負擔的手動和 hello 想要在電腦上，以節省寶貴的時間執行封包擷取。</span><span class="sxs-lookup"><span data-stu-id="e2010-113">By being able tooremotely trigger packet captures, this capability eases hello burden of running a packet capture manually and on hello desired machine, which saves valuable time.</span></span>

<span data-ttu-id="e2010-114">本文使用跨平台 Azure CLI 1.0，這適用於 Windows、Mac 和 Linux。</span><span class="sxs-lookup"><span data-stu-id="e2010-114">This article uses cross-platform Azure CLI 1.0, which is available for Windows, Mac and Linux.</span></span>

<span data-ttu-id="e2010-115">這篇文章帶領您完成 hello 封包擷取目前可用的不同的管理工作。</span><span class="sxs-lookup"><span data-stu-id="e2010-115">This article takes you through hello different management tasks that are currently available for packet capture.</span></span>

- [<span data-ttu-id="e2010-116">**啟動封包擷取**</span><span class="sxs-lookup"><span data-stu-id="e2010-116">**Start a packet capture**</span></span>](#start-a-packet-capture)
- [<span data-ttu-id="e2010-117">**停止封包擷取**</span><span class="sxs-lookup"><span data-stu-id="e2010-117">**Stop a packet capture**</span></span>](#stop-a-packet-capture)
- [<span data-ttu-id="e2010-118">**刪除封包擷取**</span><span class="sxs-lookup"><span data-stu-id="e2010-118">**Delete a packet capture**</span></span>](#delete-a-packet-capture)
- [<span data-ttu-id="e2010-119">**下載封包擷取**</span><span class="sxs-lookup"><span data-stu-id="e2010-119">**Download a packet capture**</span></span>](#download-a-packet-capture)

## <a name="before-you-begin"></a><span data-ttu-id="e2010-120">開始之前</span><span class="sxs-lookup"><span data-stu-id="e2010-120">Before you begin</span></span>

<span data-ttu-id="e2010-121">本文假設您擁有 hello 下列資源：</span><span class="sxs-lookup"><span data-stu-id="e2010-121">This article assumes you have hello following resources:</span></span>

- <span data-ttu-id="e2010-122">執行個體要在 hello 區域網路監看員的 toocreate 封包擷取</span><span class="sxs-lookup"><span data-stu-id="e2010-122">An instance of Network Watcher in hello region you want toocreate a packet capture</span></span>
- <span data-ttu-id="e2010-123">虛擬機器與 hello 封包擷取啟用擴充功能。</span><span class="sxs-lookup"><span data-stu-id="e2010-123">A virtual machine with hello packet capture extension enabled.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e2010-124">封包擷取需要的代理程式 toobe hello 虛擬機器上執行。</span><span class="sxs-lookup"><span data-stu-id="e2010-124">Packet capture requires an agent toobe running on hello virtual machine.</span></span> <span data-ttu-id="e2010-125">hello 代理程式會安裝為擴充功能。</span><span class="sxs-lookup"><span data-stu-id="e2010-125">hello Agent is installed as an extension.</span></span> <span data-ttu-id="e2010-126">如需 VM 擴充功能的指示，請瀏覽[虛擬機器擴充功能和功能](../virtual-machines/windows/extensions-features.md)。</span><span class="sxs-lookup"><span data-stu-id="e2010-126">For instructions on VM extensions, visit [Virtual Machine extensions and features](../virtual-machines/windows/extensions-features.md).</span></span>

## <a name="install-vm-extension"></a><span data-ttu-id="e2010-127">安裝 VM 擴充功能</span><span class="sxs-lookup"><span data-stu-id="e2010-127">Install VM extension</span></span>

### <a name="step-1"></a><span data-ttu-id="e2010-128">步驟 1</span><span class="sxs-lookup"><span data-stu-id="e2010-128">Step 1</span></span>

<span data-ttu-id="e2010-129">執行 hello `azure vm extension set` cmdlet tooinstall hello 封包擷取代理程式 hello 客體虛擬機器上的。</span><span class="sxs-lookup"><span data-stu-id="e2010-129">Run hello `azure vm extension set` cmdlet tooinstall hello packet capture agent on hello guest virtual machine.</span></span>

<span data-ttu-id="e2010-130">若為 Windows 虛擬機器：</span><span class="sxs-lookup"><span data-stu-id="e2010-130">For Windows virtual machines:</span></span>

```azurecli
azure vm extension set -g resourceGroupName -m virtualMachineName -p Microsoft.Azure.NetworkWatcher -r AzureNetworkWatcherExtension -n NetworkWatcherAgentWindows -o 1.4
```

<span data-ttu-id="e2010-131">若為 Linux 虛擬機器：</span><span class="sxs-lookup"><span data-stu-id="e2010-131">For Linux virtual machines:</span></span>

```azurecli
azure vm extension set -g resourceGroupName -m virtualMachineName -p Microsoft.Azure.NetworkWatcher -r AzureNetworkWatcherExtension -n NetworkWatcherAgentLinux -o 1.4
````

### <a name="step-2"></a><span data-ttu-id="e2010-132">步驟 2</span><span class="sxs-lookup"><span data-stu-id="e2010-132">Step 2</span></span>

<span data-ttu-id="e2010-133">tooensure hello 代理程式的安裝，執行 hello `vm extension get` cmdlet 並將它傳遞 hello 資源群組和虛擬機器名稱。</span><span class="sxs-lookup"><span data-stu-id="e2010-133">tooensure that hello agent is installed, run hello `vm extension get` cmdlet and pass it hello resource group and virtual machine name.</span></span> <span data-ttu-id="e2010-134">檢查 hello 產生清單 tooensure hello 代理程式已安裝。</span><span class="sxs-lookup"><span data-stu-id="e2010-134">Check hello resulting list tooensure hello agent is installed.</span></span>

```azurecli
azure vm extension get -g resourceGroupName -m virtualMachineName
```

<span data-ttu-id="e2010-135">下列範例中的 hello 是執行 hello 回應的範例`azure vm extension get`</span><span class="sxs-lookup"><span data-stu-id="e2010-135">hello following sample is an example of hello response from running `azure vm extension get`</span></span>

```
info:    Executing command vm extension get
+ Looking up hello VM "virtualMachineName"
data:    Publisher                       Name                        Version  State
data:    ------------------------------  -----------------------     -------  ---------
data:    Microsoft.Azure.NetworkWatcher  NetworkWatcherAgentWindows  1.4      Succeeded
info:    vm extension get command OK
```

## <a name="start-a-packet-capture"></a><span data-ttu-id="e2010-136">啟動封包擷取</span><span class="sxs-lookup"><span data-stu-id="e2010-136">Start a packet capture</span></span>

<span data-ttu-id="e2010-137">Hello 前面的步驟完成後，hello 虛擬機器上安裝 hello 封包擷取代理程式。</span><span class="sxs-lookup"><span data-stu-id="e2010-137">Once hello preceding steps are complete, hello packet capture agent is installed on hello virtual machine.</span></span>

### <a name="step-1"></a><span data-ttu-id="e2010-138">步驟 1</span><span class="sxs-lookup"><span data-stu-id="e2010-138">Step 1</span></span>

<span data-ttu-id="e2010-139">hello 下一個步驟是 tooretrieve hello 網路監看員執行個體。</span><span class="sxs-lookup"><span data-stu-id="e2010-139">hello next step is tooretrieve hello Network Watcher instance.</span></span> <span data-ttu-id="e2010-140">這個變數會傳遞 toohello`network watcher show`步驟 4 中的 cmdlet。</span><span class="sxs-lookup"><span data-stu-id="e2010-140">This variable is passed toohello `network watcher show` cmdlet in step 4.</span></span>

```azurecli
azure network watcher show -g resourceGroup -n networkWatcherName
```

### <a name="step-2"></a><span data-ttu-id="e2010-141">步驟 2</span><span class="sxs-lookup"><span data-stu-id="e2010-141">Step 2</span></span>

<span data-ttu-id="e2010-142">擷取儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="e2010-142">Retrieve a storage account.</span></span> <span data-ttu-id="e2010-143">這個儲存體帳戶是使用的 toostore hello 封包擷取檔案。</span><span class="sxs-lookup"><span data-stu-id="e2010-143">This storage account is used toostore hello packet capture file.</span></span>

```azurecli
azure storage account list
```

### <a name="step-3"></a><span data-ttu-id="e2010-144">步驟 3</span><span class="sxs-lookup"><span data-stu-id="e2010-144">Step 3</span></span>

<span data-ttu-id="e2010-145">篩選可使用的 toolimit hello 資料儲存的 hello 封包擷取。</span><span class="sxs-lookup"><span data-stu-id="e2010-145">Filters can be used toolimit hello data that is stored by hello packet capture.</span></span> <span data-ttu-id="e2010-146">hello 下列範例設定封包擷取與多個篩選器。</span><span class="sxs-lookup"><span data-stu-id="e2010-146">hello following example sets up a packet capture with several  filters.</span></span>  <span data-ttu-id="e2010-147">hello 前三個篩選器收集傳出的 TCP 流量只會從本機 IP 10.0.0.3 toodestination 連接埠 20、 80 和 443。</span><span class="sxs-lookup"><span data-stu-id="e2010-147">hello first three filters collect outgoing TCP traffic only from local IP 10.0.0.3 toodestination ports 20, 80 and 443.</span></span>  <span data-ttu-id="e2010-148">hello 最後一個篩選條件會收集只有 UDP 流量。</span><span class="sxs-lookup"><span data-stu-id="e2010-148">hello last filter collects only UDP traffic.</span></span>

```azurecli
azure network watcher packet-capture create -g resourceGroupName -w networkWatcherName -n packetCaptureName -t targetResourceId -o storageAccountResourceId -f "[{\"protocol\":\"TCP\", \"remoteIPAddress\":\"1.1.1.1-255.255.255\",\"localIPAddress\":\"10.0.0.3\", \"remotePort\":\"20\"},{\"protocol\":\"TCP\", \"remoteIPAddress\":\"1.1.1.1-255.255.255\",\"localIPAddress\":\"10.0.0.3\", \"remotePort\":\"80\"},{\"protocol\":\"TCP\", \"remoteIPAddress\":\"1.1.1.1-255.255.255\",\"localIPAddress\":\"10.0.0.3\", \"remotePort\":\"443\"},{\"protocol\":\"UDP\"}]"
```

<span data-ttu-id="e2010-149">一個封包擷取可以定義多個篩選器。</span><span class="sxs-lookup"><span data-stu-id="e2010-149">Multiple filters can be defined for a packet capture.</span></span> <span data-ttu-id="e2010-150">如果您使用複雜的篩選條件結構，它是較佳的 toouse 篩選 json 檔案 tooavoid 語法錯誤。</span><span class="sxs-lookup"><span data-stu-id="e2010-150">If you are using a complex filter structure, it is better toouse filters as a json file tooavoid syntax errors.</span></span> <span data-ttu-id="e2010-151">比方說，使用 hello 旗標 」-r"(而不是"-f")，並傳遞 hello 包含下列篩選器的 hello 的 json 檔案的位置：</span><span class="sxs-lookup"><span data-stu-id="e2010-151">For example, use hello flag "-r" (instead of "-f") and pass hello location of a json file containing hello following filters:</span></span>

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


<span data-ttu-id="e2010-152">hello 下列範例是執行 hello hello 預期輸出`network watcher packet-capture create`cmdlet。</span><span class="sxs-lookup"><span data-stu-id="e2010-152">hello following example is hello expected output from running hello `network watcher packet-capture create` cmdlet.</span></span>

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

## <a name="get-a-packet-capture"></a><span data-ttu-id="e2010-153">取得封包擷取</span><span class="sxs-lookup"><span data-stu-id="e2010-153">Get a packet capture</span></span>

<span data-ttu-id="e2010-154">執行 hello `network watcher packet-capture show` cmdlet，擷取目前正在執行，或已完成的封包擷取 hello 狀態。</span><span class="sxs-lookup"><span data-stu-id="e2010-154">Running hello `network watcher packet-capture show` cmdlet, retrieves hello status of a currently running, or completed packet capture.</span></span>

```azurecli
azure network watcher packet-capture show -g resourceGroupName -w networkWatcherName -n packetCaptureName
```

<span data-ttu-id="e2010-155">hello 下列範例是 hello 輸出 hello `network watcher packet-capture show` cmdlet。</span><span class="sxs-lookup"><span data-stu-id="e2010-155">hello following example is hello output from hello `network watcher packet-capture show` cmdlet.</span></span> <span data-ttu-id="e2010-156">hello 下列範例是 hello 擷取完成後。</span><span class="sxs-lookup"><span data-stu-id="e2010-156">hello following example is after hello capture is complete.</span></span> <span data-ttu-id="e2010-157">將停止 hello PacketCaptureStatus 值 StopReason TimeExceeded。</span><span class="sxs-lookup"><span data-stu-id="e2010-157">hello PacketCaptureStatus value is Stopped, with a StopReason of TimeExceeded.</span></span> <span data-ttu-id="e2010-158">這個值會顯示 hello 封包擷取已順利完成，並執行它的時間。</span><span class="sxs-lookup"><span data-stu-id="e2010-158">This value shows that hello packet capture was successful and ran its time.</span></span>

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

## <a name="stop-a-packet-capture"></a><span data-ttu-id="e2010-159">停止封包擷取</span><span class="sxs-lookup"><span data-stu-id="e2010-159">Stop a packet capture</span></span>

<span data-ttu-id="e2010-160">藉由執行 hello `network watcher packet-capture stop` cmdlet 時，如果擷取工作階段正在進行中它已停止。</span><span class="sxs-lookup"><span data-stu-id="e2010-160">By running hello `network watcher packet-capture stop` cmdlet, if a capture session is in progress it is stopped.</span></span>

```azurecli
azure network watcher packet-capture stop -g resourceGroupName -w networkWatcherName -n packetCaptureName
```

> [!NOTE]
> <span data-ttu-id="e2010-161">hello cmdlet 會傳回任何回應時執行的目前執行的擷取工作階段或現有的工作階段已經停止。</span><span class="sxs-lookup"><span data-stu-id="e2010-161">hello cmdlet returns no response when ran on a currently running capture session or an existing session that has already stopped.</span></span>

## <a name="delete-a-packet-capture"></a><span data-ttu-id="e2010-162">刪除封包擷取</span><span class="sxs-lookup"><span data-stu-id="e2010-162">Delete a packet capture</span></span>

```azurecli
azure network watcher packet-capture delete -g resourceGroupName -w networkWatcherName -n packetCaptureName
```

> [!NOTE]
> <span data-ttu-id="e2010-163">刪除封包擷取並不會刪除 hello 儲存體帳戶中的 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="e2010-163">Deleting a packet capture does not delete hello file in hello storage account.</span></span>

## <a name="download-a-packet-capture"></a><span data-ttu-id="e2010-164">下載封包擷取</span><span class="sxs-lookup"><span data-stu-id="e2010-164">Download a packet capture</span></span>

<span data-ttu-id="e2010-165">您的封包擷取工作階段完成後，請 hello 擷取檔案可上傳的 tooblob 儲存體或 tooa 本機檔案 hello VM 上。</span><span class="sxs-lookup"><span data-stu-id="e2010-165">Once your packet capture session has completed, hello capture file can be uploaded tooblob storage or tooa local file on hello VM.</span></span> <span data-ttu-id="e2010-166">hello 封包擷取 hello 儲存位置被定義在 hello 工作階段的建立。</span><span class="sxs-lookup"><span data-stu-id="e2010-166">hello storage location of hello packet capture is defined at creation of hello session.</span></span> <span data-ttu-id="e2010-167">方便的工具 tooaccess 這些擷取的檔案儲存的 tooa 儲存體帳戶是 Microsoft Azure 儲存體總管 中，這可以在這裡下載： http://storageexplorer.com/</span><span class="sxs-lookup"><span data-stu-id="e2010-167">A convenient tool tooaccess these capture files saved tooa storage account is Microsoft Azure Storage Explorer, which can be downloaded here:  http://storageexplorer.com/</span></span>

<span data-ttu-id="e2010-168">如果指定的儲存體帳戶，則封包擷取檔案會儲存在下列位置的 hello tooa 儲存體帳戶：</span><span class="sxs-lookup"><span data-stu-id="e2010-168">If a storage account is specified, packet capture files are saved tooa storage account at hello following location:</span></span>

```
https://{storageAccountName}.blob.core.windows.net/network-watcher-logs/subscriptions/{subscriptionId}/resourcegroups/{storageAccountResourceGroup}/providers/microsoft.compute/virtualmachines/{VMName}/{year}/{month}/{day}/packetCapture_{creationTime}.cap
```

## <a name="next-steps"></a><span data-ttu-id="e2010-169">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e2010-169">Next steps</span></span>

<span data-ttu-id="e2010-170">了解如何 tooautomate 封包擷取虛擬機器警示藉由檢視[建立警示觸發的封包擷取](network-watcher-alert-triggered-packet-capture.md)</span><span class="sxs-lookup"><span data-stu-id="e2010-170">Learn how tooautomate packet captures with Virtual machine alerts by viewing [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>

<span data-ttu-id="e2010-171">造訪[檢查 IP 流量驗證](network-watcher-check-ip-flow-verify-portal.md)來得知 VM 是否允許特定流量流入或流出</span><span class="sxs-lookup"><span data-stu-id="e2010-171">Find if certain traffic is allowed in or out of your VM by visiting [Check IP flow verify](network-watcher-check-ip-flow-verify-portal.md)</span></span>

<!-- Image references -->
