---
title: "檢查與 Azure 網路監看員的連線 - Azure 入口網站 | Microsoft Docs"
description: "此頁面說明如何在 Azure 入口網站中使用網路監看員來檢查連線能力"
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
ms.date: 08/02/2017
ms.author: gwallace
ms.openlocfilehash: ca62bea581acb59d3c3c0b8a204cc9d42de2b27f
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="check-connectivity-with-azure-network-watcher-using-the-azure-portal"></a><span data-ttu-id="8f2c0-103">使用 Azure 入口網站檢查與 Azure 網路監看員的連線</span><span class="sxs-lookup"><span data-stu-id="8f2c0-103">Check connectivity with Azure Network Watcher using the Azure portal</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="8f2c0-104">入口網站</span><span class="sxs-lookup"><span data-stu-id="8f2c0-104">Portal</span></span>](network-watcher-connectivity-portal.md)
> - [<span data-ttu-id="8f2c0-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8f2c0-105">PowerShell</span></span>](network-watcher-connectivity-powershell.md)
> - [<span data-ttu-id="8f2c0-106">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="8f2c0-106">CLI 2.0</span></span>](network-watcher-connectivity-cli.md)
> - [<span data-ttu-id="8f2c0-107">Azure REST API</span><span class="sxs-lookup"><span data-stu-id="8f2c0-107">Azure REST API</span></span>](network-watcher-connectivity-rest.md)

<span data-ttu-id="8f2c0-108">了解如何使用連線，確認是否可以建立從虛擬機器到指定端點的直接 TCP 連線。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-108">Learn how to use connectivity to verify if a direct TCP connection from a virtual machine to a given endpoint can be established.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="8f2c0-109">開始之前</span><span class="sxs-lookup"><span data-stu-id="8f2c0-109">Before you begin</span></span>

<span data-ttu-id="8f2c0-110">本文假設您具有下列資源：</span><span class="sxs-lookup"><span data-stu-id="8f2c0-110">This article assumes you have the following resources:</span></span>

* <span data-ttu-id="8f2c0-111">您想要檢查連線之區域中的網路監看員執行個體。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-111">An instance of Network Watcher in the region you want to check connectivity.</span></span>

* <span data-ttu-id="8f2c0-112">要檢查與其連線的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-112">Virtual machines to check connectivity with.</span></span>

<span data-ttu-id="8f2c0-113">使用 ARMclient 透過 PowerShell 呼叫 REST API。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-113">ARMclient is used to call the REST API using PowerShell.</span></span> <span data-ttu-id="8f2c0-114">您可以在 chocolatey 的 [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient) 上找到 ARMClient。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-114">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient).</span></span>

<span data-ttu-id="8f2c0-115">此案例假設您已依照[建立網路監看員](network-watcher-create.md)中的步驟建立網路監看員。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-115">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span>

[!INCLUDE [network-watcher-preview](../../includes/network-watcher-public-preview-notice.md)]

> [!IMPORTANT]
> <span data-ttu-id="8f2c0-116">連線檢查需要虛擬機器延伸模組 `AzureNetworkWatcherExtension`。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-116">Connectivity check requires a virtual machine extension `AzureNetworkWatcherExtension`.</span></span> <span data-ttu-id="8f2c0-117">若要在 Windows VM 上安裝擴充功能，請瀏覽[適用於 Windows 的 Azure 網路監看員代理程式虛擬機器擴充功能](../virtual-machines/windows/extensions-nwa.md)，若要在 Linux VM 上安裝，則請瀏覽[適用於 Linux 的 Azure 網路監看員代理程式虛擬機器擴充功能](../virtual-machines/linux/extensions-nwa.md)。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-117">For installing the extension on a Windows VM visit [Azure Network Watcher Agent virtual machine extension for Windows](../virtual-machines/windows/extensions-nwa.md) and for Linux VM visit [Azure Network Watcher Agent virtual machine extension for Linux](../virtual-machines/linux/extensions-nwa.md).</span></span>

## <a name="register-the-preview-capability"></a><span data-ttu-id="8f2c0-118">註冊預覽功能</span><span class="sxs-lookup"><span data-stu-id="8f2c0-118">Register the preview capability</span></span>

<span data-ttu-id="8f2c0-119">連線檢查目前為公開預覽版本，若要使用這項功能，必須先註冊它。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-119">Connectivity check is currently in public preview, to use this feature it needs to be registered.</span></span> <span data-ttu-id="8f2c0-120">若要這麼做，請執行下列 PowerShell 範例：</span><span class="sxs-lookup"><span data-stu-id="8f2c0-120">To do this, run the following PowerShell sample:</span></span>

```powershell
Register-AzureRmProviderFeature -FeatureName AllowNetworkWatcherConnectivityCheck  -ProviderNamespace Microsoft.Network
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.Network
```

<span data-ttu-id="8f2c0-121">若要確認註冊是否成功，請執行下列 Powershell 範例︰</span><span class="sxs-lookup"><span data-stu-id="8f2c0-121">To verify the registration was successful, run the following Powershell sample:</span></span>

```powershell
Get-AzureRmProviderFeature -FeatureName AllowNetworkWatcherConnectivityCheck  -ProviderNamespace  Microsoft.Network
```

<span data-ttu-id="8f2c0-122">如果已正確註冊該功能，輸出應該會與以下相符︰</span><span class="sxs-lookup"><span data-stu-id="8f2c0-122">If the feature was properly registered, the output should match the following:</span></span>

```
FeatureName                             ProviderName      RegistrationState
-----------                             ------------      -----------------
AllowNetworkWatcherConnectivityCheck    Microsoft.Network Registered
```

## <a name="log-in-with-armclient"></a><span data-ttu-id="8f2c0-123">使用 ARMClient 登入</span><span class="sxs-lookup"><span data-stu-id="8f2c0-123">Log in with ARMClient</span></span>

<span data-ttu-id="8f2c0-124">使用 Azure 認證登入 Armclient。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-124">Log in to armclient with your Azure credentials.</span></span>

```PowerShell
armclient login
```

## <a name="retrieve-a-virtual-machine"></a><span data-ttu-id="8f2c0-125">擷取虛擬機器</span><span class="sxs-lookup"><span data-stu-id="8f2c0-125">Retrieve a virtual machine</span></span>

<span data-ttu-id="8f2c0-126">執行下列指令碼，以傳回虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-126">Run the following script to return a virtual machine.</span></span> <span data-ttu-id="8f2c0-127">執行連線時需要這項資訊。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-127">This information is needed for running connectivity.</span></span> 

<span data-ttu-id="8f2c0-128">下列程式碼需要下列變數的值︰</span><span class="sxs-lookup"><span data-stu-id="8f2c0-128">The following code needs values for the following variables:</span></span>

- <span data-ttu-id="8f2c0-129">**subscriptionId** - 要使用的訂用帳戶識別碼。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-129">**subscriptionId** - The subscription ID to use.</span></span>
- <span data-ttu-id="8f2c0-130">**resourceGroupName** - 包含虛擬機器的資源群組名稱。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-130">**resourceGroupName** - The name of a resource group that contains virtual machines.</span></span>

```powershell
$subscriptionId = '<subscription id>'
$resourceGroupName = '<resource group name>'

armclient get https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Compute/virtualMachines?api-version=2015-05-01-preview
```

<span data-ttu-id="8f2c0-131">從下列的輸出，會在下列範例中使用虛擬機器的識別碼︰</span><span class="sxs-lookup"><span data-stu-id="8f2c0-131">From the following output, the ID of the virtual machine is used in the following example:</span></span>

```json
...
,
      "type": "Microsoft.Compute/virtualMachines",
      "location": "westcentralus",
      "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoExampleRG/providers/Microsoft.Compute
/virtualMachines/ContosoVM",
      "name": "ContosoVM"
    }
  ]
}
```

## <a name="check-connectivity-to-a-virtual-machine"></a><span data-ttu-id="8f2c0-132">檢查與虛擬機器的連線</span><span class="sxs-lookup"><span data-stu-id="8f2c0-132">Check connectivity to a virtual machine</span></span>

<span data-ttu-id="8f2c0-133">這個範例會檢查透過連接埠 80 的目的地虛擬機器連線。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-133">This example checks connectivity to a destination virtual machine over port 80.</span></span>

### <a name="example"></a><span data-ttu-id="8f2c0-134">範例</span><span class="sxs-lookup"><span data-stu-id="8f2c0-134">Example</span></span>

```powershell
$subscriptionId = "00000000-0000-0000-0000-000000000000"
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$sourceResourceId = "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Compute/virtualMachines/MultiTierApp0"
$destinationAddress = "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Compute/virtualMachines/Database0"
$destinationPort = "0"
$requestBody = @"
{
  'source': {
    'resourceId': '${sourceResourceId}',
    'port': 0
  },
  'destination': {
    'resourceId': '${destinationAddress}',
    'port': ${destinationPort}
  }
}
"@

$response = armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/connectivityCheck?api-version=2017-03-01" $requestBody
```

<span data-ttu-id="8f2c0-135">因為這項作業的執行時間很長，所以回應標頭中會傳回結果 URI，如下列回應所示：</span><span class="sxs-lookup"><span data-stu-id="8f2c0-135">Since this operation is long running, the URI for the result is returned in the response header as shown in the following response:</span></span>

<span data-ttu-id="8f2c0-136">**重要的值**</span><span class="sxs-lookup"><span data-stu-id="8f2c0-136">**Important Values**</span></span>

* <span data-ttu-id="8f2c0-137">**Location** - 此屬性包含作業完成時結果所在的 URI</span><span class="sxs-lookup"><span data-stu-id="8f2c0-137">**Location** - This property contains the URI where the results are when the operation is complete</span></span>

```
HTTP/1.1 202 Accepted
Pragma: no-cache
Retry-After: 10
x-ms-request-id: f09b55fe-1d3a-4df7-817f-bceb8d2a94c8
Strict-Transport-Security: max-age=31536000; includeSubDomains
Cache-Control: no-cache
Location: https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operationResults/f09b55fe-1d3a-4df7-817f-bceb8d2a94c8?api-version=2017-03-01
Server: Microsoft-HTTPAPI/2.0; Microsoft-HTTPAPI/2.0
x-ms-ratelimit-remaining-subscription-writes: 1199
x-ms-correlation-request-id: 367a91aa-7142-436a-867d-d3a36f80bc54
x-ms-routing-request-id: WESTUS2:20170602T202117Z:367a91aa-7142-436a-867d-d3a36f80bc54
Date: Fri, 02 Jun 2017 20:21:16 GMT

null
```

### <a name="response"></a><span data-ttu-id="8f2c0-138">Response</span><span class="sxs-lookup"><span data-stu-id="8f2c0-138">Response</span></span>

<span data-ttu-id="8f2c0-139">下列回應是來自上一個範例。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-139">The following response is from the previous example.</span></span>  <span data-ttu-id="8f2c0-140">在此回應中，`ConnectionStatus` 為 [無法連線]。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-140">In this response, the `ConnectionStatus` is **Unreachable**.</span></span> <span data-ttu-id="8f2c0-141">您可以看到傳送的所有探查都失敗。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-141">You can see that all the probes sent failed.</span></span> <span data-ttu-id="8f2c0-142">因為名為 **UserRule_Port80** 的使用者設定 `NetworkSecurityRule` 設定成封鎖連接埠 80 的連入流量，所以虛擬設備的連線失敗。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-142">The connectivity failed at the virtual appliance due to a user-configured `NetworkSecurityRule` named **UserRule_Port80**, configured to block incoming traffic on port 80.</span></span> <span data-ttu-id="8f2c0-143">這項資訊可以用來研究連線問題。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-143">This information can be used to research connection issues.</span></span>

```json
{
  "hops": [
    {
      "type": "Source",
      "id": "0cb75c91-7ebf-4df8-8424-15594d6fb51c",
      "address": "10.1.1.4",
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/appNic0/ipConfigurations/ipconfig1",
      "nextHopIds": [
        "06dee00a-9c4a-4fb1-b2ea-fa0a539ca684"
      ],
      "issues": []
    },
    {
      "type": "VirtualAppliance",
      "id": "06dee00a-9c4a-4fb1-b2ea-fa0a539ca684",
      "address": "10.1.2.4",
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/fwNic/ipConfigurations/ipconfig1",
      "nextHopIds": [
        "75e0cfa5-f9d2-48d8-b705-2c7016f81570"
      ],
      "issues": []
    },
    {
      "type": "VirtualAppliance",
      "id": "75e0cfa5-f9d2-48d8-b705-2c7016f81570",
      "address": "10.1.3.4",
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/auNic/ipConfigurations/ipconfig1",
      "nextHopIds": [
        "86caf6aa-33b0-48a1-b4da-f3c9ce785072"
      ],
      "issues": [
        {
          "origin": "Outbound",
          "severity": "Error",
          "type": "NetworkSecurityRule",
          "context": [
            {
              "key": "RuleName",
              "value": "UserRule_Port80"
            }
          ]
        }
      ]
    },
    {
      "type": "VnetLocal",
      "id": "86caf6aa-33b0-48a1-b4da-f3c9ce785072",
      "address": "10.1.4.4",
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/dbNic0/ipConfigurations/ipconfig1",
      "nextHopIds": [],
      "issues": []
    }
  ],
  "connectionStatus": "Unreachable",
  "probesSent": 100,
  "probesFailed": 100
}
```

## <a name="validate-routing-issues"></a><span data-ttu-id="8f2c0-144">驗證路由問題</span><span class="sxs-lookup"><span data-stu-id="8f2c0-144">Validate routing issues</span></span>

<span data-ttu-id="8f2c0-145">此範例會檢查虛擬機器與遠端端點之間的連線。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-145">The example checks connectivity between a virtual machine and a remote endpoint.</span></span>

### <a name="example"></a><span data-ttu-id="8f2c0-146">範例</span><span class="sxs-lookup"><span data-stu-id="8f2c0-146">Example</span></span>

```powershell
$subscriptionId = "00000000-0000-0000-0000-000000000000"
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$sourceResourceId = "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Compute/virtualMachines/MultiTierApp0"
$destinationAddress = "13.107.21.200"
$destinationPort = "80"
$requestBody = @"
{
  'source': {
    'resourceId': '${sourceResourceId}',
    'port': 0
  },
  'destination': {
    'address': '${destinationAddress}',
    'port': ${destinationPort}
  }
}
"@

$response = armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/connectivityCheck?api-version=2017-03-01" $requestBody
```

<span data-ttu-id="8f2c0-147">因為這項作業的執行時間很長，所以回應標頭中會傳回結果 URI，如下列回應所示：</span><span class="sxs-lookup"><span data-stu-id="8f2c0-147">Since this operation is long running, the URI for the result is returned in the response header as shown in the following response:</span></span>

<span data-ttu-id="8f2c0-148">**重要的值**</span><span class="sxs-lookup"><span data-stu-id="8f2c0-148">**Important Values**</span></span>

* <span data-ttu-id="8f2c0-149">**Location** - 此屬性包含作業完成時結果所在的 URI</span><span class="sxs-lookup"><span data-stu-id="8f2c0-149">**Location** - This property contains the URI where the results are when the operation is complete</span></span>

```
HTTP/1.1 202 Accepted
Pragma: no-cache
Retry-After: 10
x-ms-request-id: 15eeeb69-fcef-41db-bc4a-e2adcf2658e0
Strict-Transport-Security: max-age=31536000; includeSubDomains
Cache-Control: no-cache
Location: https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operationResults/15eeeb69-fcef-41db-bc4a-e2adcf2658e0?api-version=2017-03-01
Server: Microsoft-HTTPAPI/2.0; Microsoft-HTTPAPI/2.0
x-ms-ratelimit-remaining-subscription-writes: 1199
x-ms-correlation-request-id: 4370b798-cd8b-4d3e-ba28-22232bc81dc5
x-ms-routing-request-id: WESTUS:20170602T202606Z:4370b798-cd8b-4d3e-ba28-22232bc81dc5
Date: Fri, 02 Jun 2017 20:26:05 GMT

null
```

### <a name="response"></a><span data-ttu-id="8f2c0-150">Response</span><span class="sxs-lookup"><span data-stu-id="8f2c0-150">Response</span></span>

<span data-ttu-id="8f2c0-151">在下列範例中，`connectionStatus` 會顯示為 [無法連線]。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-151">In the following example, the `connectionStatus` is shown as **Unreachable**.</span></span> <span data-ttu-id="8f2c0-152">在 `hops` 詳細資料中，您可以在 `issues` 下看到已因 `UserDefinedRoute` 而封鎖流量。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-152">In the `hops` details, you can see under `issues` that the traffic was blocked due to a `UserDefinedRoute`.</span></span>

```json
{
  "hops": [
    {
      "type": "Source",
      "id": "5528055a-b393-4751-97bc-353d8c0aaeff",
      "address": "10.1.1.4",
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/appNic0/ipConfigurations/ipconfig1",
      "nextHopIds": [
        "66eefa79-5bfe-48b2-b6ca-eec8247457a3"
      ],
      "issues": [
        {
          "origin": "Outbound",
          "severity": "Error",
          "type": "UserDefinedRoute",
          "context": [
            {
              "key": "RouteType",
              "value": "User"
            }
          ]
        }
      ]
    },
    {
      "type": "Destination",
      "id": "66eefa79-5bfe-48b2-b6ca-eec8247457a3",
      "address": "13.107.21.200",
      "resourceId": "Unknown",
      "nextHopIds": [],
      "issues": []
    }
  ],
  "connectionStatus": "Unreachable",
  "probesSent": 100,
  "probesFailed": 100
}
```

## <a name="check-website-latency"></a><span data-ttu-id="8f2c0-153">檢查網站延遲</span><span class="sxs-lookup"><span data-stu-id="8f2c0-153">Check website latency</span></span>

<span data-ttu-id="8f2c0-154">下列範例會檢查網站連線。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-154">The following example checks the connectivity to a website.</span></span>

### <a name="example"></a><span data-ttu-id="8f2c0-155">範例</span><span class="sxs-lookup"><span data-stu-id="8f2c0-155">Example</span></span>

```powershell
$subscriptionId = "00000000-0000-0000-0000-000000000000"
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$sourceResourceId = "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Compute/virtualMachines/MultiTierApp0"
$destinationAddress = "http://bing.com"
$destinationPort = "0"
$requestBody = @"
{
  'source': {
    'resourceId': '${sourceResourceId}',
    'port': 0
  },
  'destination': {
    'address': '${destinationAddress}',
    'port': ${destinationPort}
  }
}
"@

$response = armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/connectivityCheck?api-version=2017-03-01" $requestBody
```

<span data-ttu-id="8f2c0-156">因為這項作業的執行時間很長，所以回應標頭中會傳回結果 URI，如下列回應所示：</span><span class="sxs-lookup"><span data-stu-id="8f2c0-156">Since this operation is long running, the URI for the result is returned in the response header as shown in the following response:</span></span>

<span data-ttu-id="8f2c0-157">**重要的值**</span><span class="sxs-lookup"><span data-stu-id="8f2c0-157">**Important Values**</span></span>

* <span data-ttu-id="8f2c0-158">**Location** - 此屬性包含作業完成時結果所在的 URI</span><span class="sxs-lookup"><span data-stu-id="8f2c0-158">**Location** - This property contains the URI where the results are when the operation is complete</span></span>

```
HTTP/1.1 202 Accepted
Pragma: no-cache
Retry-After: 10
x-ms-request-id: e49b12c7-c232-472c-b6d2-6c257ce80fa5
Strict-Transport-Security: max-age=31536000; includeSubDomains
Cache-Control: no-cache
Location: https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operationResults/e49b12c7-c232-472c-b6d2-6c257ce80fa5?api-version=2017-03-01
Server: Microsoft-HTTPAPI/2.0; Microsoft-HTTPAPI/2.0
x-ms-ratelimit-remaining-subscription-writes: 1199
x-ms-correlation-request-id: c3d9744f-5683-427d-bdd1-636b68ab01b6
x-ms-routing-request-id: WESTUS:20170602T203101Z:c3d9744f-5683-427d-bdd1-636b68ab01b6
Date: Fri, 02 Jun 2017 20:31:00 GMT

null
```

### <a name="response"></a><span data-ttu-id="8f2c0-159">Response</span><span class="sxs-lookup"><span data-stu-id="8f2c0-159">Response</span></span>

<span data-ttu-id="8f2c0-160">在下列回應中，您可以看到 `connectionStatus` 顯示為 [可以連線]。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-160">In the following response, you can see the `connectionStatus` shows as **Reachable**.</span></span> <span data-ttu-id="8f2c0-161">連線成功時，會提供延遲值。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-161">When a connection is successful, latency values are provided.</span></span>

```json
{
  "hops": [
    {
      "type": "Source",
      "id": "6adc0fe1-e384-4220-b1b1-f0d181220072",
      "address": "10.1.1.4",
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/appNic0/ipConfigurations/ipconfig1",
      "nextHopIds": [
        "b50b7076-9ff2-4782-b40e-0b89cf758f74"
      ],
      "issues": []
    },
    {
      "type": "Internet",
      "id": "b50b7076-9ff2-4782-b40e-0b89cf758f74",
      "address": "204.79.197.200",
      "resourceId": "Internet",
      "nextHopIds": [],
      "issues": []
    }
  ],
  "connectionStatus": "Reachable",
  "avgLatencyInMs": 1,
  "minLatencyInMs": 0,
  "maxLatencyInMs": 7,
  "probesSent": 100,
  "probesFailed": 0
}
```

## <a name="check-connectivity-to-a-storage-endpoint"></a><span data-ttu-id="8f2c0-162">檢查與儲存體端點的連線</span><span class="sxs-lookup"><span data-stu-id="8f2c0-162">Check connectivity to a storage endpoint</span></span>

<span data-ttu-id="8f2c0-163">下列範例會檢查從虛擬機器到部落格儲存體帳戶的連線。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-163">The following example checks the connectivity from a virtual machine to a blog storage account.</span></span>

### <a name="example"></a><span data-ttu-id="8f2c0-164">範例</span><span class="sxs-lookup"><span data-stu-id="8f2c0-164">Example</span></span>

```powershell
$subscriptionId = "00000000-0000-0000-0000-000000000000"
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$sourceResourceId = "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Compute/virtualMachines/MultiTierApp0"
$destinationAddress = "https://build2017nwdiag360.blob.core.windows.net/"
$destinationPort = "0"
$requestBody = @"
{
  'source': {
    'resourceId': '${sourceResourceId}',
    'port': 0
  },
  'destination': {
    'address': '${destinationAddress}',
    'port': ${destinationPort}
  }
}
"@

$response = armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/connectivityCheck?api-version=2017-03-01" $requestBody
```

<span data-ttu-id="8f2c0-165">因為這項作業的執行時間很長，所以回應標頭中會傳回結果 URI，如下列回應所示：</span><span class="sxs-lookup"><span data-stu-id="8f2c0-165">Since this operation is long running, the URI for the result is returned in the response header as shown in the following response:</span></span>

<span data-ttu-id="8f2c0-166">**重要的值**</span><span class="sxs-lookup"><span data-stu-id="8f2c0-166">**Important Values**</span></span>

* <span data-ttu-id="8f2c0-167">**Location** - 此屬性包含作業完成時結果所在的 URI</span><span class="sxs-lookup"><span data-stu-id="8f2c0-167">**Location** - This property contains the URI where the results are when the operation is complete</span></span>

```
HTTP/1.1 202 Accepted
Pragma: no-cache
Retry-After: 10
x-ms-request-id: c4ed3806-61ea-4a6b-abc1-9d6f2afc79c2
Strict-Transport-Security: max-age=31536000; includeSubDomains
Cache-Control: no-cache
Location: https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operationResults/c4ed3806-61ea-4a6b-abc1-9d6f2afc79c2?api-version=2017-03-01
Server: Microsoft-HTTPAPI/2.0; Microsoft-HTTPAPI/2.0
x-ms-ratelimit-remaining-subscription-writes: 1199
x-ms-correlation-request-id: 93bf5af0-fef5-4b7a-bb9e-9976ba5cdb95
x-ms-routing-request-id: WESTUS2:20170602T200504Z:93bf5af0-fef5-4b7a-bb9e-9976ba5cdb95
Date: Fri, 02 Jun 2017 20:05:03 GMT

null
```

### <a name="response"></a><span data-ttu-id="8f2c0-168">Response</span><span class="sxs-lookup"><span data-stu-id="8f2c0-168">Response</span></span>

<span data-ttu-id="8f2c0-169">下列範例是執行前一個 API 呼叫的回應。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-169">The following example is the response from running the previous API call.</span></span> <span data-ttu-id="8f2c0-170">因為檢查成功，所以 `connectionStatus` 屬性會顯示為 [可以連線]。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-170">As the check is successful, the `connectionStatus` property shows as **Reachable**.</span></span>  <span data-ttu-id="8f2c0-171">系統會向您提供連線儲存體 Blob 和延遲所需躍點數目的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-171">You are provided the details regarding the number of hops required to reach the storage blob and latency.</span></span>

```json
{
  "hops": [
    {
      "type": "Source",
      "id": "6adc0fe1-e384-4220-b1b1-f0d181220072",
      "address": "10.1.1.4",
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/appNic0/ipConfigurations/ipconfig1",
      "nextHopIds": [
        "b50b7076-9ff2-4782-b40e-0b89cf758f74"
      ],
      "issues": []
    },
    {
      "type": "Internet",
      "id": "b50b7076-9ff2-4782-b40e-0b89cf758f74",
      "address": "13.71.200.248",
      "resourceId": "Internet",
      "nextHopIds": [],
      "issues": []
    }
  ],
  "connectionStatus": "Reachable",
  "avgLatencyInMs": 1,
  "minLatencyInMs": 0,
  "maxLatencyInMs": 7,
  "probesSent": 100,
  "probesFailed": 0
}
```

## <a name="next-steps"></a><span data-ttu-id="8f2c0-172">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8f2c0-172">Next steps</span></span>

<span data-ttu-id="8f2c0-173">檢視[建立由警示觸發的封包擷取](network-watcher-alert-triggered-packet-capture.md)來了解如何透過虛擬機器警示自動化封包擷取</span><span class="sxs-lookup"><span data-stu-id="8f2c0-173">Learn how to automate packet captures with Virtual machine alerts by viewing [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>

<span data-ttu-id="8f2c0-174">造訪[檢查 IP 流量驗證](network-watcher-check-ip-flow-verify-portal.md)來得知 VM 是否允許特定流量流入或流出</span><span class="sxs-lookup"><span data-stu-id="8f2c0-174">Find if certain traffic is allowed in or out of your VM by visiting [Check IP flow verify](network-watcher-check-ip-flow-verify-portal.md)</span></span>

<!-- Image references -->














