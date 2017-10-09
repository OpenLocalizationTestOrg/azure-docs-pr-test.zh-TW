---
title: "與 Azure 網路監看員-Azure 入口網站的 aaaCheck 連線 |Microsoft 文件"
description: "此頁面可讓您說明如何與網路監看員中 toocheck 連線 hello Azure 入口網站"
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
ms.openlocfilehash: 8560011906fcce46d31556fc52cbfa671e8e653a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="check-connectivity-with-azure-network-watcher-using-hello-azure-portal"></a><span data-ttu-id="61a23-103">請檢查與 Azure 網路監看員使用 hello Azure 入口網站的連線</span><span class="sxs-lookup"><span data-stu-id="61a23-103">Check connectivity with Azure Network Watcher using hello Azure portal</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="61a23-104">入口網站</span><span class="sxs-lookup"><span data-stu-id="61a23-104">Portal</span></span>](network-watcher-connectivity-portal.md)
> - [<span data-ttu-id="61a23-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="61a23-105">PowerShell</span></span>](network-watcher-connectivity-powershell.md)
> - [<span data-ttu-id="61a23-106">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="61a23-106">CLI 2.0</span></span>](network-watcher-connectivity-cli.md)
> - [<span data-ttu-id="61a23-107">Azure REST API</span><span class="sxs-lookup"><span data-stu-id="61a23-107">Azure REST API</span></span>](network-watcher-connectivity-rest.md)

<span data-ttu-id="61a23-108">了解可以如何建立 toouse 連線 tooverify 如果從虛擬機器 tooa 指定端點的直接 TCP 連接。</span><span class="sxs-lookup"><span data-stu-id="61a23-108">Learn how toouse connectivity tooverify if a direct TCP connection from a virtual machine tooa given endpoint can be established.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="61a23-109">開始之前</span><span class="sxs-lookup"><span data-stu-id="61a23-109">Before you begin</span></span>

<span data-ttu-id="61a23-110">本文假設您擁有 hello 下列資源：</span><span class="sxs-lookup"><span data-stu-id="61a23-110">This article assumes you have hello following resources:</span></span>

* <span data-ttu-id="61a23-111">執行個體要 toocheck 連線的網路監看員 hello 區域中。</span><span class="sxs-lookup"><span data-stu-id="61a23-111">An instance of Network Watcher in hello region you want toocheck connectivity.</span></span>

* <span data-ttu-id="61a23-112">虛擬機器與 toocheck 連線。</span><span class="sxs-lookup"><span data-stu-id="61a23-112">Virtual machines toocheck connectivity with.</span></span>

<span data-ttu-id="61a23-113">ARMclient 是使用 PowerShell 的使用的 toocall hello REST API。</span><span class="sxs-lookup"><span data-stu-id="61a23-113">ARMclient is used toocall hello REST API using PowerShell.</span></span> <span data-ttu-id="61a23-114">您可以在 chocolatey 的 [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient) 上找到 ARMClient。</span><span class="sxs-lookup"><span data-stu-id="61a23-114">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient).</span></span>

<span data-ttu-id="61a23-115">此案例假設您已依照中的 hello 步驟[建立網路監看員](network-watcher-create.md)toocreate 網路監看員。</span><span class="sxs-lookup"><span data-stu-id="61a23-115">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span>

[!INCLUDE [network-watcher-preview](../../includes/network-watcher-public-preview-notice.md)]

> [!IMPORTANT]
> <span data-ttu-id="61a23-116">連線檢查需要虛擬機器延伸模組 `AzureNetworkWatcherExtension`。</span><span class="sxs-lookup"><span data-stu-id="61a23-116">Connectivity check requires a virtual machine extension `AzureNetworkWatcherExtension`.</span></span> <span data-ttu-id="61a23-117">Hello 擴充功能安裝在 Windows VM 上瀏覽[Azure 網路監看員的代理程式適用於 Windows 的虛擬機器擴充功能](../virtual-machines/windows/extensions-nwa.md)和如 Linux VM，請造訪[Azure 網路監看員的代理程式虛擬機器擴充功能，適用於 Linux](../virtual-machines/linux/extensions-nwa.md).</span><span class="sxs-lookup"><span data-stu-id="61a23-117">For installing hello extension on a Windows VM visit [Azure Network Watcher Agent virtual machine extension for Windows](../virtual-machines/windows/extensions-nwa.md) and for Linux VM visit [Azure Network Watcher Agent virtual machine extension for Linux](../virtual-machines/linux/extensions-nwa.md).</span></span>

## <a name="register-hello-preview-capability"></a><span data-ttu-id="61a23-118">註冊 hello 預覽功能</span><span class="sxs-lookup"><span data-stu-id="61a23-118">Register hello preview capability</span></span>

<span data-ttu-id="61a23-119">連線能力檢查目前處於公開預覽，toouse 需要 toobe 註冊這項功能。</span><span class="sxs-lookup"><span data-stu-id="61a23-119">Connectivity check is currently in public preview, toouse this feature it needs toobe registered.</span></span> <span data-ttu-id="61a23-120">toodo，執行下列 PowerShell 範例的 hello:</span><span class="sxs-lookup"><span data-stu-id="61a23-120">toodo this, run hello following PowerShell sample:</span></span>

```powershell
Register-AzureRmProviderFeature -FeatureName AllowNetworkWatcherConnectivityCheck  -ProviderNamespace Microsoft.Network
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.Network
```

<span data-ttu-id="61a23-121">tooverify hello 登錄成功，執行下列 Powershell 範例 hello:</span><span class="sxs-lookup"><span data-stu-id="61a23-121">tooverify hello registration was successful, run hello following Powershell sample:</span></span>

```powershell
Get-AzureRmProviderFeature -FeatureName AllowNetworkWatcherConnectivityCheck  -ProviderNamespace  Microsoft.Network
```

<span data-ttu-id="61a23-122">如果 hello 功能已正確註冊，hello 輸出應符合下列 hello:</span><span class="sxs-lookup"><span data-stu-id="61a23-122">If hello feature was properly registered, hello output should match hello following:</span></span>

```
FeatureName                             ProviderName      RegistrationState
-----------                             ------------      -----------------
AllowNetworkWatcherConnectivityCheck    Microsoft.Network Registered
```

## <a name="log-in-with-armclient"></a><span data-ttu-id="61a23-123">使用 ARMClient 登入</span><span class="sxs-lookup"><span data-stu-id="61a23-123">Log in with ARMClient</span></span>

<span data-ttu-id="61a23-124">登入 tooarmclient 與您的 Azure 認證。</span><span class="sxs-lookup"><span data-stu-id="61a23-124">Log in tooarmclient with your Azure credentials.</span></span>

```PowerShell
armclient login
```

## <a name="retrieve-a-virtual-machine"></a><span data-ttu-id="61a23-125">擷取虛擬機器</span><span class="sxs-lookup"><span data-stu-id="61a23-125">Retrieve a virtual machine</span></span>

<span data-ttu-id="61a23-126">執行下列指令碼 tooreturn hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="61a23-126">Run hello following script tooreturn a virtual machine.</span></span> <span data-ttu-id="61a23-127">執行連線時需要這項資訊。</span><span class="sxs-lookup"><span data-stu-id="61a23-127">This information is needed for running connectivity.</span></span> 

<span data-ttu-id="61a23-128">下列程式碼的 hello hello 下列變數需要值：</span><span class="sxs-lookup"><span data-stu-id="61a23-128">hello following code needs values for hello following variables:</span></span>

- <span data-ttu-id="61a23-129">**subscriptionId** -hello 訂用帳戶 ID toouse。</span><span class="sxs-lookup"><span data-stu-id="61a23-129">**subscriptionId** - hello subscription ID toouse.</span></span>
- <span data-ttu-id="61a23-130">**resourceGroupName** -hello 包含虛擬機器的資源群組的名稱。</span><span class="sxs-lookup"><span data-stu-id="61a23-130">**resourceGroupName** - hello name of a resource group that contains virtual machines.</span></span>

```powershell
$subscriptionId = '<subscription id>'
$resourceGroupName = '<resource group name>'

armclient get https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Compute/virtualMachines?api-version=2015-05-01-preview
```

<span data-ttu-id="61a23-131">從 hello 下列輸出，hello hello 虛擬機器識別碼 hello 下列範例中使用：</span><span class="sxs-lookup"><span data-stu-id="61a23-131">From hello following output, hello ID of hello virtual machine is used in hello following example:</span></span>

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

## <a name="check-connectivity-tooa-virtual-machine"></a><span data-ttu-id="61a23-132">請檢查連線 tooa 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="61a23-132">Check connectivity tooa virtual machine</span></span>

<span data-ttu-id="61a23-133">這個範例會檢查透過連接埠 80 連線 tooa 目的地虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="61a23-133">This example checks connectivity tooa destination virtual machine over port 80.</span></span>

### <a name="example"></a><span data-ttu-id="61a23-134">範例</span><span class="sxs-lookup"><span data-stu-id="61a23-134">Example</span></span>

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

<span data-ttu-id="61a23-135">由於這項作業是長時間執行，hello hello 結果的 URI 會傳回 hello 回應標頭中下列回應 hello 中所示：</span><span class="sxs-lookup"><span data-stu-id="61a23-135">Since this operation is long running, hello URI for hello result is returned in hello response header as shown in hello following response:</span></span>

<span data-ttu-id="61a23-136">**重要的值**</span><span class="sxs-lookup"><span data-stu-id="61a23-136">**Important Values**</span></span>

* <span data-ttu-id="61a23-137">**位置**-這個屬性包含 hello hello 結果的所在當 hello 作業已完成的 URI</span><span class="sxs-lookup"><span data-stu-id="61a23-137">**Location** - This property contains hello URI where hello results are when hello operation is complete</span></span>

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

### <a name="response"></a><span data-ttu-id="61a23-138">Response</span><span class="sxs-lookup"><span data-stu-id="61a23-138">Response</span></span>

<span data-ttu-id="61a23-139">下列回應 hello 取自 hello 前一個範例。</span><span class="sxs-lookup"><span data-stu-id="61a23-139">hello following response is from hello previous example.</span></span>  <span data-ttu-id="61a23-140">此回應 hello`ConnectionStatus`是**連線**。</span><span class="sxs-lookup"><span data-stu-id="61a23-140">In this response, hello `ConnectionStatus` is **Unreachable**.</span></span> <span data-ttu-id="61a23-141">您可以看到所有 hello 探查傳送失敗。</span><span class="sxs-lookup"><span data-stu-id="61a23-141">You can see that all hello probes sent failed.</span></span> <span data-ttu-id="61a23-142">hello 連線無法在 hello 虛擬應用裝置使用者設定的到期 tooa`NetworkSecurityRule`名為**UserRule_Port80**，通訊埠 80 上設定 tooblock 連入流量。</span><span class="sxs-lookup"><span data-stu-id="61a23-142">hello connectivity failed at hello virtual appliance due tooa user-configured `NetworkSecurityRule` named **UserRule_Port80**, configured tooblock incoming traffic on port 80.</span></span> <span data-ttu-id="61a23-143">這項資訊可以使用的 tooresearch 連線問題。</span><span class="sxs-lookup"><span data-stu-id="61a23-143">This information can be used tooresearch connection issues.</span></span>

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

## <a name="validate-routing-issues"></a><span data-ttu-id="61a23-144">驗證路由問題</span><span class="sxs-lookup"><span data-stu-id="61a23-144">Validate routing issues</span></span>

<span data-ttu-id="61a23-145">hello 範例會檢查虛擬機器與遠端端點之間的連線。</span><span class="sxs-lookup"><span data-stu-id="61a23-145">hello example checks connectivity between a virtual machine and a remote endpoint.</span></span>

### <a name="example"></a><span data-ttu-id="61a23-146">範例</span><span class="sxs-lookup"><span data-stu-id="61a23-146">Example</span></span>

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

<span data-ttu-id="61a23-147">由於這項作業是長時間執行，hello hello 結果的 URI 會傳回 hello 回應標頭中下列回應 hello 中所示：</span><span class="sxs-lookup"><span data-stu-id="61a23-147">Since this operation is long running, hello URI for hello result is returned in hello response header as shown in hello following response:</span></span>

<span data-ttu-id="61a23-148">**重要的值**</span><span class="sxs-lookup"><span data-stu-id="61a23-148">**Important Values**</span></span>

* <span data-ttu-id="61a23-149">**位置**-這個屬性包含 hello hello 結果的所在當 hello 作業已完成的 URI</span><span class="sxs-lookup"><span data-stu-id="61a23-149">**Location** - This property contains hello URI where hello results are when hello operation is complete</span></span>

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

### <a name="response"></a><span data-ttu-id="61a23-150">Response</span><span class="sxs-lookup"><span data-stu-id="61a23-150">Response</span></span>

<span data-ttu-id="61a23-151">在下列範例的 hello，hello`connectionStatus`會顯示為**連線**。</span><span class="sxs-lookup"><span data-stu-id="61a23-151">In hello following example, hello `connectionStatus` is shown as **Unreachable**.</span></span> <span data-ttu-id="61a23-152">在 hello`hops`詳細資料，您可以看到下`issues`hello 流量遭到封鎖到期 tooa `UserDefinedRoute`。</span><span class="sxs-lookup"><span data-stu-id="61a23-152">In hello `hops` details, you can see under `issues` that hello traffic was blocked due tooa `UserDefinedRoute`.</span></span>

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

## <a name="check-website-latency"></a><span data-ttu-id="61a23-153">檢查網站延遲</span><span class="sxs-lookup"><span data-stu-id="61a23-153">Check website latency</span></span>

<span data-ttu-id="61a23-154">hello 下列範例會檢查 hello 連線 tooa 網站。</span><span class="sxs-lookup"><span data-stu-id="61a23-154">hello following example checks hello connectivity tooa website.</span></span>

### <a name="example"></a><span data-ttu-id="61a23-155">範例</span><span class="sxs-lookup"><span data-stu-id="61a23-155">Example</span></span>

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

<span data-ttu-id="61a23-156">由於這項作業是長時間執行，hello hello 結果的 URI 會傳回 hello 回應標頭中下列回應 hello 中所示：</span><span class="sxs-lookup"><span data-stu-id="61a23-156">Since this operation is long running, hello URI for hello result is returned in hello response header as shown in hello following response:</span></span>

<span data-ttu-id="61a23-157">**重要的值**</span><span class="sxs-lookup"><span data-stu-id="61a23-157">**Important Values**</span></span>

* <span data-ttu-id="61a23-158">**位置**-這個屬性包含 hello hello 結果的所在當 hello 作業已完成的 URI</span><span class="sxs-lookup"><span data-stu-id="61a23-158">**Location** - This property contains hello URI where hello results are when hello operation is complete</span></span>

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

### <a name="response"></a><span data-ttu-id="61a23-159">Response</span><span class="sxs-lookup"><span data-stu-id="61a23-159">Response</span></span>

<span data-ttu-id="61a23-160">在下列回應 hello，您可以看到 hello`connectionStatus`顯示為**Reachable**。</span><span class="sxs-lookup"><span data-stu-id="61a23-160">In hello following response, you can see hello `connectionStatus` shows as **Reachable**.</span></span> <span data-ttu-id="61a23-161">連線成功時，會提供延遲值。</span><span class="sxs-lookup"><span data-stu-id="61a23-161">When a connection is successful, latency values are provided.</span></span>

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

## <a name="check-connectivity-tooa-storage-endpoint"></a><span data-ttu-id="61a23-162">請檢查連線 tooa 儲存體端點</span><span class="sxs-lookup"><span data-stu-id="61a23-162">Check connectivity tooa storage endpoint</span></span>

<span data-ttu-id="61a23-163">hello 下列範例會檢查 hello 連線從虛擬機器 tooa 部落格儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="61a23-163">hello following example checks hello connectivity from a virtual machine tooa blog storage account.</span></span>

### <a name="example"></a><span data-ttu-id="61a23-164">範例</span><span class="sxs-lookup"><span data-stu-id="61a23-164">Example</span></span>

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

<span data-ttu-id="61a23-165">由於這項作業是長時間執行，hello hello 結果的 URI 會傳回 hello 回應標頭中下列回應 hello 中所示：</span><span class="sxs-lookup"><span data-stu-id="61a23-165">Since this operation is long running, hello URI for hello result is returned in hello response header as shown in hello following response:</span></span>

<span data-ttu-id="61a23-166">**重要的值**</span><span class="sxs-lookup"><span data-stu-id="61a23-166">**Important Values**</span></span>

* <span data-ttu-id="61a23-167">**位置**-這個屬性包含 hello hello 結果的所在當 hello 作業已完成的 URI</span><span class="sxs-lookup"><span data-stu-id="61a23-167">**Location** - This property contains hello URI where hello results are when hello operation is complete</span></span>

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

### <a name="response"></a><span data-ttu-id="61a23-168">Response</span><span class="sxs-lookup"><span data-stu-id="61a23-168">Response</span></span>

<span data-ttu-id="61a23-169">hello 下列範例是 hello 回應 hello 先前的應用程式開發介面呼叫的執行。</span><span class="sxs-lookup"><span data-stu-id="61a23-169">hello following example is hello response from running hello previous API call.</span></span> <span data-ttu-id="61a23-170">如同 hello 檢查成功，hello`connectionStatus`屬性會顯示為**Reachable**。</span><span class="sxs-lookup"><span data-stu-id="61a23-170">As hello check is successful, hello `connectionStatus` property shows as **Reachable**.</span></span>  <span data-ttu-id="61a23-171">為您提供有關 hello 數目躍點需要的 tooreach hello 儲存體 blob 和延遲的 hello 詳細資料。</span><span class="sxs-lookup"><span data-stu-id="61a23-171">You are provided hello details regarding hello number of hops required tooreach hello storage blob and latency.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="61a23-172">後續步驟</span><span class="sxs-lookup"><span data-stu-id="61a23-172">Next steps</span></span>

<span data-ttu-id="61a23-173">了解如何 tooautomate 封包擷取虛擬機器警示藉由檢視[建立警示觸發的封包擷取](network-watcher-alert-triggered-packet-capture.md)</span><span class="sxs-lookup"><span data-stu-id="61a23-173">Learn how tooautomate packet captures with Virtual machine alerts by viewing [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>

<span data-ttu-id="61a23-174">造訪[檢查 IP 流量驗證](network-watcher-check-ip-flow-verify-portal.md)來得知 VM 是否允許特定流量流入或流出</span><span class="sxs-lookup"><span data-stu-id="61a23-174">Find if certain traffic is allowed in or out of your VM by visiting [Check IP flow verify](network-watcher-check-ip-flow-verify-portal.md)</span></span>

<!-- Image references -->














