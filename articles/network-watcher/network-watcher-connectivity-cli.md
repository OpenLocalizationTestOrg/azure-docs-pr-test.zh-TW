---
title: "與 Azure 網路監看員-Azure CLI 2.0 aaaCheck 連線 |Microsoft 文件"
description: "此頁面說明如何 toouse 連線檢查與使用 Azure CLI 2.0 網路監看員"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/11/2017
ms.author: gwallace
ms.openlocfilehash: e94e0fad03fd36ebf4e1fdf9e3cfee934b289deb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="check-connectivity-with-azure-network-watcher-using-azure-cli-20"></a><span data-ttu-id="a9f95-103">使用 Azure CLI 2.0 檢查與 Azure 網路監看員的連線</span><span class="sxs-lookup"><span data-stu-id="a9f95-103">Check connectivity with Azure Network Watcher using Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="a9f95-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a9f95-104">PowerShell</span></span>](network-watcher-connectivity-powershell.md)
> - [<span data-ttu-id="a9f95-105">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="a9f95-105">CLI 2.0</span></span>](network-watcher-connectivity-cli.md)
> - [<span data-ttu-id="a9f95-106">Azure REST API</span><span class="sxs-lookup"><span data-stu-id="a9f95-106">Azure REST API</span></span>](network-watcher-connectivity-rest.md)

<span data-ttu-id="a9f95-107">了解可以如何建立 toouse 連線 tooverify 如果從虛擬機器 tooa 指定端點的直接 TCP 連接。</span><span class="sxs-lookup"><span data-stu-id="a9f95-107">Learn how toouse connectivity tooverify if a direct TCP connection from a virtual machine tooa given endpoint can be established.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="a9f95-108">開始之前</span><span class="sxs-lookup"><span data-stu-id="a9f95-108">Before you begin</span></span>

<span data-ttu-id="a9f95-109">本文假設您擁有 hello 下列資源：</span><span class="sxs-lookup"><span data-stu-id="a9f95-109">This article assumes you have hello following resources:</span></span>

* <span data-ttu-id="a9f95-110">執行個體要 toocheck 連線的網路監看員 hello 區域中。</span><span class="sxs-lookup"><span data-stu-id="a9f95-110">An instance of Network Watcher in hello region you want toocheck connectivity.</span></span>

* <span data-ttu-id="a9f95-111">虛擬機器與 toocheck 連線。</span><span class="sxs-lookup"><span data-stu-id="a9f95-111">Virtual machines toocheck connectivity with.</span></span>

[!INCLUDE [network-watcher-preview](../../includes/network-watcher-public-preview-notice.md)]

> [!IMPORTANT]
> <span data-ttu-id="a9f95-112">連線檢查需要虛擬機器延伸模組 `AzureNetworkWatcherExtension`。</span><span class="sxs-lookup"><span data-stu-id="a9f95-112">Connectivity check requires a virtual machine extension `AzureNetworkWatcherExtension`.</span></span> <span data-ttu-id="a9f95-113">Hello 擴充功能安裝在 Windows VM 上瀏覽[Azure 網路監看員的代理程式適用於 Windows 的虛擬機器擴充功能](../virtual-machines/windows/extensions-nwa.md)和如 Linux VM，請造訪[Azure 網路監看員的代理程式虛擬機器擴充功能，適用於 Linux](../virtual-machines/linux/extensions-nwa.md).</span><span class="sxs-lookup"><span data-stu-id="a9f95-113">For installing hello extension on a Windows VM visit [Azure Network Watcher Agent virtual machine extension for Windows](../virtual-machines/windows/extensions-nwa.md) and for Linux VM visit [Azure Network Watcher Agent virtual machine extension for Linux](../virtual-machines/linux/extensions-nwa.md).</span></span>

## <a name="register-hello-preview-capability"></a><span data-ttu-id="a9f95-114">註冊 hello 預覽功能</span><span class="sxs-lookup"><span data-stu-id="a9f95-114">Register hello preview capability</span></span> 

<span data-ttu-id="a9f95-115">連線能力檢查目前處於公開預覽，toouse 需要 toobe 註冊這項功能。</span><span class="sxs-lookup"><span data-stu-id="a9f95-115">Connectivity check is currently in public preview, toouse this feature it needs toobe registered.</span></span> <span data-ttu-id="a9f95-116">toodo 遵循 CLI 範例，執行的 hello</span><span class="sxs-lookup"><span data-stu-id="a9f95-116">toodo this, run hello following CLI sample</span></span>

```azurecli 
az feature register --namespace Microsoft.Network --name AllowNetworkWatcherConnectivityCheck

az provider register --namespace Microsoft.Network 
``` 

<span data-ttu-id="a9f95-117">tooverify hello 登錄成功，執行下列 CLI 命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="a9f95-117">tooverify hello registration was successful, run hello following CLI command:</span></span>

```azurecli
az feature show --namespace Microsoft.Network --name AllowNetworkWatcherConnectivityCheck 
```

<span data-ttu-id="a9f95-118">如果 hello 功能已正確註冊，hello 輸出應符合下列 hello:</span><span class="sxs-lookup"><span data-stu-id="a9f95-118">If hello feature was properly registered, hello output should match hello following:</span></span> 

```json
{
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Features/providers/Microsoft.Network/features/AllowNetworkWatcherConnectivityCheck",
  "name": "Microsoft.Network/AllowNetworkWatcherConnectivityCheck",
  "properties": {
    "state": "Registered"
  },
  "type": "Microsoft.Features/providers/features"
}
``` 

## <a name="check-connectivity-tooa-virtual-machine"></a><span data-ttu-id="a9f95-119">請檢查連線 tooa 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="a9f95-119">Check connectivity tooa virtual machine</span></span>

<span data-ttu-id="a9f95-120">這個範例會檢查透過連接埠 80 連線 tooa 目的地虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="a9f95-120">This example checks connectivity tooa destination virtual machine over port 80.</span></span>

### <a name="example"></a><span data-ttu-id="a9f95-121">範例</span><span class="sxs-lookup"><span data-stu-id="a9f95-121">Example</span></span>

```azurecli
az network watcher test-connectivity --resource-group ContosoRG --source-resource MultiTierApp0 --dest-resource Database0 --dest-port 80
```

### <a name="response"></a><span data-ttu-id="a9f95-122">Response</span><span class="sxs-lookup"><span data-stu-id="a9f95-122">Response</span></span>

<span data-ttu-id="a9f95-123">下列回應 hello 取自 hello 前一個範例。</span><span class="sxs-lookup"><span data-stu-id="a9f95-123">hello following response is from hello previous example.</span></span>  <span data-ttu-id="a9f95-124">此回應 hello`ConnectionStatus`是**連線**。</span><span class="sxs-lookup"><span data-stu-id="a9f95-124">In this response, hello `ConnectionStatus` is **Unreachable**.</span></span> <span data-ttu-id="a9f95-125">您可以看到所有 hello 探查傳送失敗。</span><span class="sxs-lookup"><span data-stu-id="a9f95-125">You can see that all hello probes sent failed.</span></span> <span data-ttu-id="a9f95-126">hello 連線無法在 hello 虛擬應用裝置使用者設定的到期 tooa`NetworkSecurityRule`名為**UserRule_Port80**，通訊埠 80 上設定 tooblock 連入流量。</span><span class="sxs-lookup"><span data-stu-id="a9f95-126">hello connectivity failed at hello virtual appliance due tooa user-configured `NetworkSecurityRule` named **UserRule_Port80**, configured tooblock incoming traffic on port 80.</span></span> <span data-ttu-id="a9f95-127">這項資訊可以使用的 tooresearch 連線問題。</span><span class="sxs-lookup"><span data-stu-id="a9f95-127">This information can be used tooresearch connection issues.</span></span>

```json
{
  "avgLatencyInMs": null,
  "connectionStatus": "Unreachable",
  "hops": [
    {
      "address": "10.1.1.4",
      "id": "bb01d336-d881-4808-9fbc-72f091974d68",
      "issues": [],
      "nextHopIds": [
        "f8b074e9-9980-496b-a35e-619f9bcbf648"
      ],
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/ap
pNic0/ipConfigurations/ipconfig1",
      "type": "Source"
    },
    {
      "address": "10.1.2.4",
      "id": "f8b074e9-9980-496b-a35e-619f9bcbf648",
      "issues": [],
      "nextHopIds": [
        "8a5857f3-6ab8-4b11-b9bf-a046d66b8696"
      ],
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/fw
Nic/ipConfigurations/ipconfig1",
      "type": "VirtualAppliance"
    },
    {
      "address": "10.1.3.4",
      "id": "8a5857f3-6ab8-4b11-b9bf-a046d66b8696",
      "issues": [
        {
          "context": [
            {
              "key": "RuleName",
              "value": "UserRule_Port80"
            }
          ],
          "origin": "Outbound",
          "severity": "Error",
          "type": "NetworkSecurityRule"
        }
      ],
      "nextHopIds": [
        "6ce2f7a2-ceb4-4145-80e8-5d9f661655d6"
      ],
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/au
Nic/ipConfigurations/ipconfig1",
      "type": "VirtualAppliance"
    },
    {
      "address": "10.1.4.4",
      "id": "6ce2f7a2-ceb4-4145-80e8-5d9f661655d6",
      "issues": [],
      "nextHopIds": [],
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/db
Nic0/ipConfigurations/ipconfig1",
      "type": "VnetLocal"
    }
  ],
  "maxLatencyInMs": null,
  "minLatencyInMs": null,
  "probesFailed": 100,
  "probesSent": 100
}
```

## <a name="validate-routing-issues"></a><span data-ttu-id="a9f95-128">驗證路由問題</span><span class="sxs-lookup"><span data-stu-id="a9f95-128">Validate routing issues</span></span>

<span data-ttu-id="a9f95-129">hello 範例會檢查虛擬機器與遠端端點之間的連線。</span><span class="sxs-lookup"><span data-stu-id="a9f95-129">hello example checks connectivity between a virtual machine and a remote endpoint.</span></span>

### <a name="example"></a><span data-ttu-id="a9f95-130">範例</span><span class="sxs-lookup"><span data-stu-id="a9f95-130">Example</span></span>

```azurecli
az network watcher test-connectivity --resource-group ContosoRG --source-resource MultiTierApp0 --dest-address 13.107.21.200 --dest-port 80
```

### <a name="response"></a><span data-ttu-id="a9f95-131">Response</span><span class="sxs-lookup"><span data-stu-id="a9f95-131">Response</span></span>

<span data-ttu-id="a9f95-132">在下列範例的 hello，hello`connectionStatus`會顯示為**連線**。</span><span class="sxs-lookup"><span data-stu-id="a9f95-132">In hello following example, hello `connectionStatus` is shown as **Unreachable**.</span></span> <span data-ttu-id="a9f95-133">在 hello`hops`詳細資料，您可以看到下`issues`hello 流量遭到封鎖到期 tooa `UserDefinedRoute`。</span><span class="sxs-lookup"><span data-stu-id="a9f95-133">In hello `hops` details, you can see under `issues` that hello traffic was blocked due tooa `UserDefinedRoute`.</span></span>

```json
{
  "avgLatencyInMs": null,
  "connectionStatus": "Unreachable",
  "hops": [
    {
      "address": "10.1.1.4",
      "id": "f2cb1868-2049-4839-b8ed-57a480d06f95",
      "issues": [
        {
          "context": [
            {
              "key": "RouteType",
              "value": "User"
            }
          ],
          "origin": "Outbound",
          "severity": "Error",
          "type": "UserDefinedRoute"
        }
      ],
      "nextHopIds": [
        "da4022db-0ab0-48c4-a507-dd4c03561ca5"
      ],
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/ap
pNic0/ipConfigurations/ipconfig1",
      "type": "Source"
    },
    {
      "address": "13.107.21.200",
      "id": "da4022db-0ab0-48c4-a507-dd4c03561ca5",
      "issues": [],
      "nextHopIds": [],
      "resourceId": "Unknown",
      "type": "Destination"
    }
  ],
  "maxLatencyInMs": null,
  "minLatencyInMs": null,
  "probesFailed": 100,
  "probesSent": 100
}
```

## <a name="check-website-latency"></a><span data-ttu-id="a9f95-134">檢查網站延遲</span><span class="sxs-lookup"><span data-stu-id="a9f95-134">Check website latency</span></span>

<span data-ttu-id="a9f95-135">hello 下列範例會檢查 hello 連線 tooa 網站。</span><span class="sxs-lookup"><span data-stu-id="a9f95-135">hello following example checks hello connectivity tooa website.</span></span>

### <a name="example"></a><span data-ttu-id="a9f95-136">範例</span><span class="sxs-lookup"><span data-stu-id="a9f95-136">Example</span></span>

```azurecli
az network watcher test-connectivity --resource-group ContosoRG --source-resource MultiTierApp0 --dest-address http://bing.com --dest-port 80
```

### <a name="response"></a><span data-ttu-id="a9f95-137">Response</span><span class="sxs-lookup"><span data-stu-id="a9f95-137">Response</span></span>

<span data-ttu-id="a9f95-138">在下列回應 hello，您可以看到 hello`connectionStatus`顯示為**Reachable**。</span><span class="sxs-lookup"><span data-stu-id="a9f95-138">In hello following response, you can see hello `connectionStatus` shows as **Reachable**.</span></span> <span data-ttu-id="a9f95-139">連線成功時，會提供延遲值。</span><span class="sxs-lookup"><span data-stu-id="a9f95-139">When a connection is successful, latency values are provided.</span></span>

```json
{
  "avgLatencyInMs": 2,
  "connectionStatus": "Reachable",
  "hops": [
    {
      "address": "10.1.1.4",
      "id": "639c2d19-e163-4dfd-8737-5018dd1168ae",
      "issues": [],
      "nextHopIds": [
        "fd43a6e7-c758-4f48-90aa-8db99105a4a3"
      ],
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/ap
pNic0/ipConfigurations/ipconfig1",
      "type": "Source"
    },
    {
      "address": "204.79.197.200",
      "id": "fd43a6e7-c758-4f48-90aa-8db99105a4a3",
      "issues": [],
      "nextHopIds": [],
      "resourceId": "Internet",
      "type": "Internet"
    }
  ],
  "maxLatencyInMs": 7,
  "minLatencyInMs": 0,
  "probesFailed": 0,
  "probesSent": 100
}
```

## <a name="check-connectivity-tooa-storage-endpoint"></a><span data-ttu-id="a9f95-140">請檢查連線 tooa 儲存體端點</span><span class="sxs-lookup"><span data-stu-id="a9f95-140">Check connectivity tooa storage endpoint</span></span>

<span data-ttu-id="a9f95-141">hello 下列範例會檢查 hello 連線從虛擬機器 tooa 部落格儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="a9f95-141">hello following example checks hello connectivity from a virtual machine tooa blog storage account.</span></span>

### <a name="example"></a><span data-ttu-id="a9f95-142">範例</span><span class="sxs-lookup"><span data-stu-id="a9f95-142">Example</span></span>

```azurecli
az network watcher test-connectivity --resource-group ContosoRG --source-resource MultiTierApp0 --dest-address https://contosoexamplesa.blob.core.windows.net/
```

### <a name="response"></a><span data-ttu-id="a9f95-143">Response</span><span class="sxs-lookup"><span data-stu-id="a9f95-143">Response</span></span>

<span data-ttu-id="a9f95-144">hello 下列 json 是 hello 執行 hello 前一個 cmdlet 的範例回應。</span><span class="sxs-lookup"><span data-stu-id="a9f95-144">hello following json is hello example response from running hello previous cmdlet.</span></span> <span data-ttu-id="a9f95-145">如同 hello 檢查成功，hello`connectionStatus`屬性會顯示為**Reachable**。</span><span class="sxs-lookup"><span data-stu-id="a9f95-145">As hello check is successful, hello `connectionStatus` property shows as **Reachable**.</span></span>  <span data-ttu-id="a9f95-146">為您提供有關 hello 數目躍點需要的 tooreach hello 儲存體 blob 和延遲的 hello 詳細資料。</span><span class="sxs-lookup"><span data-stu-id="a9f95-146">You are provided hello details regarding hello number of hops required tooreach hello storage blob and latency.</span></span>

```json
{
  "avgLatencyInMs": 1,
  "connectionStatus": "Reachable",
  "hops": [
    {
      "address": "10.1.1.4",
      "id": "5136acff-bf26-4c93-9966-4edb7dd40353",
      "issues": [],
      "nextHopIds": [
        "f8d958b7-3636-4d63-9441-602c1eb2fd56"
      ],
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/appNic0/ipConfigurations/ipconfig1",
      "type": "Source"
    },
    {
      "address": "1.2.3.4",
      "id": "f8d958b7-3636-4d63-9441-602c1eb2fd56",
      "issues": [],
      "nextHopIds": [],
      "resourceId": "Internet",
      "type": "Internet"
    }
  ],
  "maxLatencyInMs": 7,
  "minLatencyInMs": 0,
  "probesFailed": 0,
  "probesSent": 100
}
```

## <a name="next-steps"></a><span data-ttu-id="a9f95-147">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a9f95-147">Next steps</span></span>

<span data-ttu-id="a9f95-148">了解如何 tooautomate 封包擷取虛擬機器警示藉由檢視[建立警示觸發的封包擷取](network-watcher-alert-triggered-packet-capture.md)</span><span class="sxs-lookup"><span data-stu-id="a9f95-148">Learn how tooautomate packet captures with Virtual machine alerts by viewing [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>

<span data-ttu-id="a9f95-149">造訪[檢查 IP 流量驗證](network-watcher-check-ip-flow-verify-portal.md)來得知 VM 是否允許特定流量流入或流出</span><span class="sxs-lookup"><span data-stu-id="a9f95-149">Find if certain traffic is allowed in or out of your VM by visiting [Check IP flow verify](network-watcher-check-ip-flow-verify-portal.md)</span></span>
