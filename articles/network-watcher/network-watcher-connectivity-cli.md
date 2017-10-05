---
title: "檢查與 Azure 網路監看員的連線 - Azure CLI 2.0 | Microsoft Docs"
description: "此頁面說明如何使用 Azure CLI 2.0 檢查與網路監看員的連線"
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
ms.openlocfilehash: c1deaa40bfda0bf3858ad56d3d6a90df34351278
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="check-connectivity-with-azure-network-watcher-using-azure-cli-20"></a><span data-ttu-id="ec944-103">使用 Azure CLI 2.0 檢查與 Azure 網路監看員的連線</span><span class="sxs-lookup"><span data-stu-id="ec944-103">Check connectivity with Azure Network Watcher using Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="ec944-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ec944-104">PowerShell</span></span>](network-watcher-connectivity-powershell.md)
> - [<span data-ttu-id="ec944-105">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="ec944-105">CLI 2.0</span></span>](network-watcher-connectivity-cli.md)
> - [<span data-ttu-id="ec944-106">Azure REST API</span><span class="sxs-lookup"><span data-stu-id="ec944-106">Azure REST API</span></span>](network-watcher-connectivity-rest.md)

<span data-ttu-id="ec944-107">了解如何使用連線，確認是否可以建立從虛擬機器到指定端點的直接 TCP 連線。</span><span class="sxs-lookup"><span data-stu-id="ec944-107">Learn how to use connectivity to verify if a direct TCP connection from a virtual machine to a given endpoint can be established.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="ec944-108">開始之前</span><span class="sxs-lookup"><span data-stu-id="ec944-108">Before you begin</span></span>

<span data-ttu-id="ec944-109">本文假設您具有下列資源：</span><span class="sxs-lookup"><span data-stu-id="ec944-109">This article assumes you have the following resources:</span></span>

* <span data-ttu-id="ec944-110">您想要檢查連線之區域中的網路監看員執行個體。</span><span class="sxs-lookup"><span data-stu-id="ec944-110">An instance of Network Watcher in the region you want to check connectivity.</span></span>

* <span data-ttu-id="ec944-111">要檢查與其連線的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="ec944-111">Virtual machines to check connectivity with.</span></span>

[!INCLUDE [network-watcher-preview](../../includes/network-watcher-public-preview-notice.md)]

> [!IMPORTANT]
> <span data-ttu-id="ec944-112">連線檢查需要虛擬機器延伸模組 `AzureNetworkWatcherExtension`。</span><span class="sxs-lookup"><span data-stu-id="ec944-112">Connectivity check requires a virtual machine extension `AzureNetworkWatcherExtension`.</span></span> <span data-ttu-id="ec944-113">若要在 Windows VM 上安裝擴充功能，請瀏覽[適用於 Windows 的 Azure 網路監看員代理程式虛擬機器擴充功能](../virtual-machines/windows/extensions-nwa.md)，若要在 Linux VM 上安裝，則請瀏覽[適用於 Linux 的 Azure 網路監看員代理程式虛擬機器擴充功能](../virtual-machines/linux/extensions-nwa.md)。</span><span class="sxs-lookup"><span data-stu-id="ec944-113">For installing the extension on a Windows VM visit [Azure Network Watcher Agent virtual machine extension for Windows](../virtual-machines/windows/extensions-nwa.md) and for Linux VM visit [Azure Network Watcher Agent virtual machine extension for Linux](../virtual-machines/linux/extensions-nwa.md).</span></span>

## <a name="register-the-preview-capability"></a><span data-ttu-id="ec944-114">註冊預覽功能</span><span class="sxs-lookup"><span data-stu-id="ec944-114">Register the preview capability</span></span> 

<span data-ttu-id="ec944-115">連線檢查目前為公開預覽版本，若要使用這項功能，必須先註冊它。</span><span class="sxs-lookup"><span data-stu-id="ec944-115">Connectivity check is currently in public preview, to use this feature it needs to be registered.</span></span> <span data-ttu-id="ec944-116">若要這樣做，請執行下列 CLI 範例</span><span class="sxs-lookup"><span data-stu-id="ec944-116">To do this, run the following CLI sample</span></span>

```azurecli 
az feature register --namespace Microsoft.Network --name AllowNetworkWatcherConnectivityCheck

az provider register --namespace Microsoft.Network 
``` 

<span data-ttu-id="ec944-117">若要確認註冊是否成功，請執行下列 CLI 命令︰</span><span class="sxs-lookup"><span data-stu-id="ec944-117">To verify the registration was successful, run the following CLI command:</span></span>

```azurecli
az feature show --namespace Microsoft.Network --name AllowNetworkWatcherConnectivityCheck 
```

<span data-ttu-id="ec944-118">如果已正確註冊該功能，輸出應該會與以下相符︰</span><span class="sxs-lookup"><span data-stu-id="ec944-118">If the feature was properly registered, the output should match the following:</span></span> 

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

## <a name="check-connectivity-to-a-virtual-machine"></a><span data-ttu-id="ec944-119">檢查與虛擬機器的連線</span><span class="sxs-lookup"><span data-stu-id="ec944-119">Check connectivity to a virtual machine</span></span>

<span data-ttu-id="ec944-120">這個範例會檢查透過連接埠 80 的目的地虛擬機器連線。</span><span class="sxs-lookup"><span data-stu-id="ec944-120">This example checks connectivity to a destination virtual machine over port 80.</span></span>

### <a name="example"></a><span data-ttu-id="ec944-121">範例</span><span class="sxs-lookup"><span data-stu-id="ec944-121">Example</span></span>

```azurecli
az network watcher test-connectivity --resource-group ContosoRG --source-resource MultiTierApp0 --dest-resource Database0 --dest-port 80
```

### <a name="response"></a><span data-ttu-id="ec944-122">Response</span><span class="sxs-lookup"><span data-stu-id="ec944-122">Response</span></span>

<span data-ttu-id="ec944-123">下列回應是來自上一個範例。</span><span class="sxs-lookup"><span data-stu-id="ec944-123">The following response is from the previous example.</span></span>  <span data-ttu-id="ec944-124">在此回應中，`ConnectionStatus` 為 [無法連線]。</span><span class="sxs-lookup"><span data-stu-id="ec944-124">In this response, the `ConnectionStatus` is **Unreachable**.</span></span> <span data-ttu-id="ec944-125">您可以看到傳送的所有探查都失敗。</span><span class="sxs-lookup"><span data-stu-id="ec944-125">You can see that all the probes sent failed.</span></span> <span data-ttu-id="ec944-126">因為名為 **UserRule_Port80** 的使用者設定 `NetworkSecurityRule` 設定成封鎖連接埠 80 的連入流量，所以虛擬設備的連線失敗。</span><span class="sxs-lookup"><span data-stu-id="ec944-126">The connectivity failed at the virtual appliance due to a user-configured `NetworkSecurityRule` named **UserRule_Port80**, configured to block incoming traffic on port 80.</span></span> <span data-ttu-id="ec944-127">這項資訊可以用來研究連線問題。</span><span class="sxs-lookup"><span data-stu-id="ec944-127">This information can be used to research connection issues.</span></span>

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

## <a name="validate-routing-issues"></a><span data-ttu-id="ec944-128">驗證路由問題</span><span class="sxs-lookup"><span data-stu-id="ec944-128">Validate routing issues</span></span>

<span data-ttu-id="ec944-129">此範例會檢查虛擬機器與遠端端點之間的連線。</span><span class="sxs-lookup"><span data-stu-id="ec944-129">The example checks connectivity between a virtual machine and a remote endpoint.</span></span>

### <a name="example"></a><span data-ttu-id="ec944-130">範例</span><span class="sxs-lookup"><span data-stu-id="ec944-130">Example</span></span>

```azurecli
az network watcher test-connectivity --resource-group ContosoRG --source-resource MultiTierApp0 --dest-address 13.107.21.200 --dest-port 80
```

### <a name="response"></a><span data-ttu-id="ec944-131">Response</span><span class="sxs-lookup"><span data-stu-id="ec944-131">Response</span></span>

<span data-ttu-id="ec944-132">在下列範例中，`connectionStatus` 會顯示為 [無法連線]。</span><span class="sxs-lookup"><span data-stu-id="ec944-132">In the following example, the `connectionStatus` is shown as **Unreachable**.</span></span> <span data-ttu-id="ec944-133">在 `hops` 詳細資料中，您可以在 `issues` 下看到已因 `UserDefinedRoute` 而封鎖流量。</span><span class="sxs-lookup"><span data-stu-id="ec944-133">In the `hops` details, you can see under `issues` that the traffic was blocked due to a `UserDefinedRoute`.</span></span>

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

## <a name="check-website-latency"></a><span data-ttu-id="ec944-134">檢查網站延遲</span><span class="sxs-lookup"><span data-stu-id="ec944-134">Check website latency</span></span>

<span data-ttu-id="ec944-135">下列範例會檢查網站連線。</span><span class="sxs-lookup"><span data-stu-id="ec944-135">The following example checks the connectivity to a website.</span></span>

### <a name="example"></a><span data-ttu-id="ec944-136">範例</span><span class="sxs-lookup"><span data-stu-id="ec944-136">Example</span></span>

```azurecli
az network watcher test-connectivity --resource-group ContosoRG --source-resource MultiTierApp0 --dest-address http://bing.com --dest-port 80
```

### <a name="response"></a><span data-ttu-id="ec944-137">Response</span><span class="sxs-lookup"><span data-stu-id="ec944-137">Response</span></span>

<span data-ttu-id="ec944-138">在下列回應中，您可以看到 `connectionStatus` 顯示為 [可以連線]。</span><span class="sxs-lookup"><span data-stu-id="ec944-138">In the following response, you can see the `connectionStatus` shows as **Reachable**.</span></span> <span data-ttu-id="ec944-139">連線成功時，會提供延遲值。</span><span class="sxs-lookup"><span data-stu-id="ec944-139">When a connection is successful, latency values are provided.</span></span>

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

## <a name="check-connectivity-to-a-storage-endpoint"></a><span data-ttu-id="ec944-140">檢查與儲存體端點的連線</span><span class="sxs-lookup"><span data-stu-id="ec944-140">Check connectivity to a storage endpoint</span></span>

<span data-ttu-id="ec944-141">下列範例會檢查從虛擬機器到部落格儲存體帳戶的連線。</span><span class="sxs-lookup"><span data-stu-id="ec944-141">The following example checks the connectivity from a virtual machine to a blog storage account.</span></span>

### <a name="example"></a><span data-ttu-id="ec944-142">範例</span><span class="sxs-lookup"><span data-stu-id="ec944-142">Example</span></span>

```azurecli
az network watcher test-connectivity --resource-group ContosoRG --source-resource MultiTierApp0 --dest-address https://contosoexamplesa.blob.core.windows.net/
```

### <a name="response"></a><span data-ttu-id="ec944-143">Response</span><span class="sxs-lookup"><span data-stu-id="ec944-143">Response</span></span>

<span data-ttu-id="ec944-144">下列 JSON 是執行前一個 Cmdlet 的範例回應。</span><span class="sxs-lookup"><span data-stu-id="ec944-144">The following json is the example response from running the previous cmdlet.</span></span> <span data-ttu-id="ec944-145">因為檢查成功，所以 `connectionStatus` 屬性會顯示為 [可以連線]。</span><span class="sxs-lookup"><span data-stu-id="ec944-145">As the check is successful, the `connectionStatus` property shows as **Reachable**.</span></span>  <span data-ttu-id="ec944-146">系統會向您提供連線儲存體 Blob 和延遲所需躍點數目的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="ec944-146">You are provided the details regarding the number of hops required to reach the storage blob and latency.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="ec944-147">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ec944-147">Next steps</span></span>

<span data-ttu-id="ec944-148">檢視[建立由警示觸發的封包擷取](network-watcher-alert-triggered-packet-capture.md)來了解如何透過虛擬機器警示自動化封包擷取</span><span class="sxs-lookup"><span data-stu-id="ec944-148">Learn how to automate packet captures with Virtual machine alerts by viewing [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>

<span data-ttu-id="ec944-149">造訪[檢查 IP 流量驗證](network-watcher-check-ip-flow-verify-portal.md)來得知 VM 是否允許特定流量流入或流出</span><span class="sxs-lookup"><span data-stu-id="ec944-149">Find if certain traffic is allowed in or out of your VM by visiting [Check IP flow verify](network-watcher-check-ip-flow-verify-portal.md)</span></span>
