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
# <a name="manage-packet-captures-with-azure-network-watcher-using-azure-cli-20"></a><span data-ttu-id="65014-103">使用 Azure CLI 2.0，利用 Azure 網路監看員管理封包擷取</span><span class="sxs-lookup"><span data-stu-id="65014-103">Manage packet captures with Azure Network Watcher using Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="65014-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="65014-104">Azure portal</span></span>](network-watcher-packet-capture-manage-portal.md)
> - [<span data-ttu-id="65014-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="65014-105">PowerShell</span></span>](network-watcher-packet-capture-manage-powershell.md)
> - [<span data-ttu-id="65014-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="65014-106">CLI 1.0</span></span>](network-watcher-packet-capture-manage-cli-nodejs.md)
> - [<span data-ttu-id="65014-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="65014-107">CLI 2.0</span></span>](network-watcher-packet-capture-manage-cli.md)
> - [<span data-ttu-id="65014-108">Azure REST API</span><span class="sxs-lookup"><span data-stu-id="65014-108">Azure REST API</span></span>](network-watcher-packet-capture-manage-rest.md)

<span data-ttu-id="65014-109">網路監看員封包擷取可讓您 toocreate 擷取工作階段 tootrack 流量 tooand 從虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="65014-109">Network Watcher packet capture allows you toocreate capture sessions tootrack traffic tooand from a virtual machine.</span></span> <span data-ttu-id="65014-110">篩選器可供 hello 擷取工作階段 tooensure 擷取您想要只 hello 流量。</span><span class="sxs-lookup"><span data-stu-id="65014-110">Filters are provided for hello capture session tooensure you capture only hello traffic you want.</span></span> <span data-ttu-id="65014-111">封包擷取可在主動和被動協助 toodiagnose 網路異常狀況。</span><span class="sxs-lookup"><span data-stu-id="65014-111">Packet capture helps toodiagnose network anomalies both reactively and proactively.</span></span> <span data-ttu-id="65014-112">其他用途包括收集網路統計資料，取得有關網路入侵，toodebug 用戶端與伺服器通訊，以及執行更多。</span><span class="sxs-lookup"><span data-stu-id="65014-112">Other uses include gathering network statistics, gaining information on network intrusions, toodebug client-server communications and much more.</span></span> <span data-ttu-id="65014-113">透過無法 tooremotely 觸發程序封包擷取，這項功能可以減輕工作 hello 負擔的手動和 hello 想要在電腦上，以節省寶貴的時間執行封包擷取。</span><span class="sxs-lookup"><span data-stu-id="65014-113">By being able tooremotely trigger packet captures, this capability eases hello burden of running a packet capture manually and on hello desired machine, which saves valuable time.</span></span>

<span data-ttu-id="65014-114">本文使用我們的下一個層代 CLI hello 資源管理部署模型，Azure CLI 2.0 中，這是適用於 Windows、 Mac 和 Linux。</span><span class="sxs-lookup"><span data-stu-id="65014-114">This article uses our next generation CLI for hello resource management deployment model, Azure CLI 2.0, which is available for Windows, Mac and Linux.</span></span>

<span data-ttu-id="65014-115">tooperform hello 步驟在本文中，您需要[hello Azure 命令列介面安裝的 Mac、 Linux 及 Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2)。</span><span class="sxs-lookup"><span data-stu-id="65014-115">tooperform hello steps in this article, you need too[install hello Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span></span>

<span data-ttu-id="65014-116">這篇文章帶領您完成 hello 封包擷取目前可用的不同的管理工作。</span><span class="sxs-lookup"><span data-stu-id="65014-116">This article takes you through hello different management tasks that are currently available for packet capture.</span></span>

- [<span data-ttu-id="65014-117">**啟動封包擷取**</span><span class="sxs-lookup"><span data-stu-id="65014-117">**Start a packet capture**</span></span>](#start-a-packet-capture)
- [<span data-ttu-id="65014-118">**停止封包擷取**</span><span class="sxs-lookup"><span data-stu-id="65014-118">**Stop a packet capture**</span></span>](#stop-a-packet-capture)
- [<span data-ttu-id="65014-119">**刪除封包擷取**</span><span class="sxs-lookup"><span data-stu-id="65014-119">**Delete a packet capture**</span></span>](#delete-a-packet-capture)
- [<span data-ttu-id="65014-120">**下載封包擷取**</span><span class="sxs-lookup"><span data-stu-id="65014-120">**Download a packet capture**</span></span>](#download-a-packet-capture)

## <a name="before-you-begin"></a><span data-ttu-id="65014-121">開始之前</span><span class="sxs-lookup"><span data-stu-id="65014-121">Before you begin</span></span>

<span data-ttu-id="65014-122">本文假設您擁有 hello 下列資源：</span><span class="sxs-lookup"><span data-stu-id="65014-122">This article assumes you have hello following resources:</span></span>

- <span data-ttu-id="65014-123">執行個體要在 hello 區域網路監看員的 toocreate 封包擷取</span><span class="sxs-lookup"><span data-stu-id="65014-123">An instance of Network Watcher in hello region you want toocreate a packet capture</span></span>
- <span data-ttu-id="65014-124">虛擬機器與 hello 封包擷取啟用擴充功能。</span><span class="sxs-lookup"><span data-stu-id="65014-124">A virtual machine with hello packet capture extension enabled.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="65014-125">封包擷取需要的代理程式 toobe hello 虛擬機器上執行。</span><span class="sxs-lookup"><span data-stu-id="65014-125">Packet capture requires an agent toobe running on hello virtual machine.</span></span> <span data-ttu-id="65014-126">hello 代理程式會安裝為擴充功能。</span><span class="sxs-lookup"><span data-stu-id="65014-126">hello Agent is installed as an extension.</span></span> <span data-ttu-id="65014-127">如需 VM 擴充功能的指示，請瀏覽[虛擬機器擴充功能和功能](../virtual-machines/windows/extensions-features.md)。</span><span class="sxs-lookup"><span data-stu-id="65014-127">For instructions on VM extensions, visit [Virtual Machine extensions and features](../virtual-machines/windows/extensions-features.md).</span></span>

## <a name="install-vm-extension"></a><span data-ttu-id="65014-128">安裝 VM 擴充功能</span><span class="sxs-lookup"><span data-stu-id="65014-128">Install VM extension</span></span>

### <a name="step-1"></a><span data-ttu-id="65014-129">步驟 1</span><span class="sxs-lookup"><span data-stu-id="65014-129">Step 1</span></span>

<span data-ttu-id="65014-130">執行 hello `az vm extension set` cmdlet tooinstall hello 封包擷取代理程式 hello 客體虛擬機器上的。</span><span class="sxs-lookup"><span data-stu-id="65014-130">Run hello `az vm extension set` cmdlet tooinstall hello packet capture agent on hello guest virtual machine.</span></span>

<span data-ttu-id="65014-131">若為 Windows 虛擬機器：</span><span class="sxs-lookup"><span data-stu-id="65014-131">For Windows virtual machines:</span></span>

```azurecli
az vm extension set --resource-group resourceGroupName --vm-name virtualMachineName --publisher Microsoft.Azure.NetworkWatcher --name NetworkWatcherAgentWindows --version 1.4
```

<span data-ttu-id="65014-132">若為 Linux 虛擬機器：</span><span class="sxs-lookup"><span data-stu-id="65014-132">For Linux virtual machines:</span></span>

```azurecli
az vm extension set --resource-group resourceGroupName --vm-name virtualMachineName --publisher Microsoft.Azure.NetworkWatcher --name NetworkWatcherAgentLinux--version 1.4
````

### <a name="step-2"></a><span data-ttu-id="65014-133">步驟 2</span><span class="sxs-lookup"><span data-stu-id="65014-133">Step 2</span></span>

<span data-ttu-id="65014-134">tooensure hello 代理程式的安裝，執行 hello `vm extension get` cmdlet 並將它傳遞 hello 資源群組和虛擬機器名稱。</span><span class="sxs-lookup"><span data-stu-id="65014-134">tooensure that hello agent is installed, run hello `vm extension get` cmdlet and pass it hello resource group and virtual machine name.</span></span> <span data-ttu-id="65014-135">檢查 hello 產生清單 tooensure hello 代理程式已安裝。</span><span class="sxs-lookup"><span data-stu-id="65014-135">Check hello resulting list tooensure hello agent is installed.</span></span>

```azurecli
az vm extension show -resource-group resourceGroupName --vm-name virtualMachineName --name NetworkWatcherAgentWindows
```

<span data-ttu-id="65014-136">下列範例中的 hello 是執行 hello 回應的範例`az vm extension show`</span><span class="sxs-lookup"><span data-stu-id="65014-136">hello following sample is an example of hello response from running `az vm extension show`</span></span>

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

## <a name="start-a-packet-capture"></a><span data-ttu-id="65014-137">啟動封包擷取</span><span class="sxs-lookup"><span data-stu-id="65014-137">Start a packet capture</span></span>

<span data-ttu-id="65014-138">Hello 前面的步驟完成後，hello 虛擬機器上安裝 hello 封包擷取代理程式。</span><span class="sxs-lookup"><span data-stu-id="65014-138">Once hello preceding steps are complete, hello packet capture agent is installed on hello virtual machine.</span></span>

### <a name="step-1"></a><span data-ttu-id="65014-139">步驟 1</span><span class="sxs-lookup"><span data-stu-id="65014-139">Step 1</span></span>

<span data-ttu-id="65014-140">hello 下一個步驟是 tooretrieve hello 網路監看員執行個體。</span><span class="sxs-lookup"><span data-stu-id="65014-140">hello next step is tooretrieve hello Network Watcher instance.</span></span> <span data-ttu-id="65014-141">T 名稱 hello 網路監看員會傳遞 toohello`az network watcher show`步驟 4 中的 cmdlet。</span><span class="sxs-lookup"><span data-stu-id="65014-141">TThe name of hello Network Watcher is passed toohello `az network watcher show` cmdlet in step 4.</span></span>

```azurecli
az network watcher show -resource-group resourceGroup -name networkWatcherName
```

### <a name="step-2"></a><span data-ttu-id="65014-142">步驟 2</span><span class="sxs-lookup"><span data-stu-id="65014-142">Step 2</span></span>

<span data-ttu-id="65014-143">擷取儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="65014-143">Retrieve a storage account.</span></span> <span data-ttu-id="65014-144">這個儲存體帳戶是使用的 toostore hello 封包擷取檔案。</span><span class="sxs-lookup"><span data-stu-id="65014-144">This storage account is used toostore hello packet capture file.</span></span>

```azurecli
azure storage account list
```

### <a name="step-3"></a><span data-ttu-id="65014-145">步驟 3</span><span class="sxs-lookup"><span data-stu-id="65014-145">Step 3</span></span>

<span data-ttu-id="65014-146">篩選可使用的 toolimit hello 資料儲存的 hello 封包擷取。</span><span class="sxs-lookup"><span data-stu-id="65014-146">Filters can be used toolimit hello data that is stored by hello packet capture.</span></span> <span data-ttu-id="65014-147">hello 下列範例設定封包擷取與多個篩選器。</span><span class="sxs-lookup"><span data-stu-id="65014-147">hello following example sets up a packet capture with several  filters.</span></span>  <span data-ttu-id="65014-148">hello 前三個篩選器收集傳出的 TCP 流量只會從本機 IP 10.0.0.3 toodestination 連接埠 20、 80 和 443。</span><span class="sxs-lookup"><span data-stu-id="65014-148">hello first three filters collect outgoing TCP traffic only from local IP 10.0.0.3 toodestination ports 20, 80 and 443.</span></span>  <span data-ttu-id="65014-149">hello 最後一個篩選條件會收集只有 UDP 流量。</span><span class="sxs-lookup"><span data-stu-id="65014-149">hello last filter collects only UDP traffic.</span></span>

```azurecli
az network watcher packet-capture create --resource-group {resoureceurceGroupName} --vm {vmName} --name packetCaptureName --storage-account gwteststorage123abc --filters "[{\"protocol\":\"TCP\", \"remoteIPAddress\":\"1.1.1.1-255.255.255\",\"localIPAddress\":\"10.0.0.3\", \"remotePort\":\"20\"},{\"protocol\":\"TCP\", \"remoteIPAddress\":\"1.1.1.1-255.255.255\",\"localIPAddress\":\"10.0.0.3\", \"remotePort\":\"80\"},{\"protocol\":\"TCP\", \"remoteIPAddress\":\"1.1.1.1-255.255.255\",\"localIPAddress\":\"10.0.0.3\", \"remotePort\":\"443\"},{\"protocol\":\"UDP\"}]"
```

<span data-ttu-id="65014-150">hello 下列範例是執行 hello hello 預期輸出`az network watcher packet-capture create`cmdlet。</span><span class="sxs-lookup"><span data-stu-id="65014-150">hello following example is hello expected output from running hello `az network watcher packet-capture create` cmdlet.</span></span>

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

## <a name="get-a-packet-capture"></a><span data-ttu-id="65014-151">取得封包擷取</span><span class="sxs-lookup"><span data-stu-id="65014-151">Get a packet capture</span></span>

<span data-ttu-id="65014-152">執行 hello `az network watcher packet-capture show` cmdlet，擷取目前正在執行，或已完成的封包擷取 hello 狀態。</span><span class="sxs-lookup"><span data-stu-id="65014-152">Running hello `az network watcher packet-capture show` cmdlet, retrieves hello status of a currently running, or completed packet capture.</span></span>

```azurecli
az network watcher packet-capture show --name packetCaptureName --location westcentralus
```

<span data-ttu-id="65014-153">hello 下列範例是 hello 輸出 hello `az network watcher packet-capture show` cmdlet。</span><span class="sxs-lookup"><span data-stu-id="65014-153">hello following example is hello output from hello `az network watcher packet-capture show` cmdlet.</span></span> <span data-ttu-id="65014-154">hello 下列範例是 hello 擷取完成後。</span><span class="sxs-lookup"><span data-stu-id="65014-154">hello following example is after hello capture is complete.</span></span> <span data-ttu-id="65014-155">將停止 hello PacketCaptureStatus 值 StopReason TimeExceeded。</span><span class="sxs-lookup"><span data-stu-id="65014-155">hello PacketCaptureStatus value is Stopped, with a StopReason of TimeExceeded.</span></span> <span data-ttu-id="65014-156">這個值會顯示 hello 封包擷取已順利完成，並執行它的時間。</span><span class="sxs-lookup"><span data-stu-id="65014-156">This value shows that hello packet capture was successful and ran its time.</span></span>

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

## <a name="stop-a-packet-capture"></a><span data-ttu-id="65014-157">停止封包擷取</span><span class="sxs-lookup"><span data-stu-id="65014-157">Stop a packet capture</span></span>

<span data-ttu-id="65014-158">藉由執行 hello `az network watcher packet-capture stop` cmdlet 時，如果擷取工作階段正在進行中它已停止。</span><span class="sxs-lookup"><span data-stu-id="65014-158">By running hello `az network watcher packet-capture stop` cmdlet, if a capture session is in progress it is stopped.</span></span>

```azurecli
az network watcher packet-capture stop --name packetCaptureName --location westcentralus
```

> [!NOTE]
> <span data-ttu-id="65014-159">hello cmdlet 會傳回任何回應時執行的目前執行的擷取工作階段或現有的工作階段已經停止。</span><span class="sxs-lookup"><span data-stu-id="65014-159">hello cmdlet returns no response when ran on a currently running capture session or an existing session that has already stopped.</span></span>

## <a name="delete-a-packet-capture"></a><span data-ttu-id="65014-160">刪除封包擷取</span><span class="sxs-lookup"><span data-stu-id="65014-160">Delete a packet capture</span></span>

```azurecli
az network watcher packet-capture delete --name packetCaptureName --location westcentralus
```

> [!NOTE]
> <span data-ttu-id="65014-161">刪除封包擷取並不會刪除 hello 儲存體帳戶中的 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="65014-161">Deleting a packet capture does not delete hello file in hello storage account.</span></span>

## <a name="download-a-packet-capture"></a><span data-ttu-id="65014-162">下載封包擷取</span><span class="sxs-lookup"><span data-stu-id="65014-162">Download a packet capture</span></span>

<span data-ttu-id="65014-163">您的封包擷取工作階段完成後，請 hello 擷取檔案可上傳的 tooblob 儲存體或 tooa 本機檔案 hello VM 上。</span><span class="sxs-lookup"><span data-stu-id="65014-163">Once your packet capture session has completed, hello capture file can be uploaded tooblob storage or tooa local file on hello VM.</span></span> <span data-ttu-id="65014-164">hello 封包擷取 hello 儲存位置被定義在 hello 工作階段的建立。</span><span class="sxs-lookup"><span data-stu-id="65014-164">hello storage location of hello packet capture is defined at creation of hello session.</span></span> <span data-ttu-id="65014-165">方便的工具 tooaccess 這些擷取的檔案儲存的 tooa 儲存體帳戶是 Microsoft Azure 儲存體總管 中，這可以在這裡下載： http://storageexplorer.com/</span><span class="sxs-lookup"><span data-stu-id="65014-165">A convenient tool tooaccess these capture files saved tooa storage account is Microsoft Azure Storage Explorer, which can be downloaded here:  http://storageexplorer.com/</span></span>

<span data-ttu-id="65014-166">如果指定的儲存體帳戶，則封包擷取檔案會儲存在下列位置的 hello tooa 儲存體帳戶：</span><span class="sxs-lookup"><span data-stu-id="65014-166">If a storage account is specified, packet capture files are saved tooa storage account at hello following location:</span></span>

```
https://{storageAccountName}.blob.core.windows.net/network-watcher-logs/subscriptions/{subscriptionId}/resourcegroups/{storageAccountResourceGroup}/providers/microsoft.compute/virtualmachines/{VMName}/{year}/{month}/{day}/packetCapture_{creationTime}.cap
```

## <a name="next-steps"></a><span data-ttu-id="65014-167">後續步驟</span><span class="sxs-lookup"><span data-stu-id="65014-167">Next steps</span></span>

<span data-ttu-id="65014-168">了解如何 tooautomate 封包擷取虛擬機器警示藉由檢視[建立警示觸發的封包擷取](network-watcher-alert-triggered-packet-capture.md)</span><span class="sxs-lookup"><span data-stu-id="65014-168">Learn how tooautomate packet captures with Virtual machine alerts by viewing [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>

<span data-ttu-id="65014-169">造訪[檢查 IP 流量驗證](network-watcher-check-ip-flow-verify-portal.md)來得知 VM 是否允許特定流量流入或流出</span><span class="sxs-lookup"><span data-stu-id="65014-169">Find if certain traffic is allowed in or out of your VM by visiting [Check IP flow verify](network-watcher-check-ip-flow-verify-portal.md)</span></span>

<!-- Image references -->
