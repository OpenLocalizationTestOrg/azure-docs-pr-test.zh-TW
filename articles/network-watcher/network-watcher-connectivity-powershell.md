---
title: "檢查與 Azure 網路監看員的連線 - PowerShell | Microsoft Docs"
description: "此頁面說明如何使用 PowerShell 測試與網路監看員的連線。"
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
ms.openlocfilehash: a8f936cd23838759dc30b04688d3c6544e4895cc
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="check-connectivity-with-azure-network-watcher-using-powershell"></a><span data-ttu-id="ee3dc-103">使用 PowerShell 檢查與 Azure 網路監看員的連線</span><span class="sxs-lookup"><span data-stu-id="ee3dc-103">Check connectivity with Azure Network Watcher using PowerShell</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="ee3dc-104">入口網站</span><span class="sxs-lookup"><span data-stu-id="ee3dc-104">Portal</span></span>](network-watcher-connectivity-portal.md)
> - [<span data-ttu-id="ee3dc-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ee3dc-105">PowerShell</span></span>](network-watcher-connectivity-powershell.md)
> - [<span data-ttu-id="ee3dc-106">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="ee3dc-106">CLI 2.0</span></span>](network-watcher-connectivity-cli.md)
> - [<span data-ttu-id="ee3dc-107">Azure REST API</span><span class="sxs-lookup"><span data-stu-id="ee3dc-107">Azure REST API</span></span>](network-watcher-connectivity-rest.md)

<span data-ttu-id="ee3dc-108">了解如何使用連線，確認是否可以建立從虛擬機器到指定端點的直接 TCP 連線。</span><span class="sxs-lookup"><span data-stu-id="ee3dc-108">Learn how to use connectivity to verify if a direct TCP connection from a virtual machine to a given endpoint can be established.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="ee3dc-109">開始之前</span><span class="sxs-lookup"><span data-stu-id="ee3dc-109">Before you begin</span></span>

<span data-ttu-id="ee3dc-110">本文假設您具有下列資源：</span><span class="sxs-lookup"><span data-stu-id="ee3dc-110">This article assumes you have the following resources:</span></span>

* <span data-ttu-id="ee3dc-111">您想要檢查連線之區域中的網路監看員執行個體。</span><span class="sxs-lookup"><span data-stu-id="ee3dc-111">An instance of Network Watcher in the region you want to check connectivity.</span></span>

* <span data-ttu-id="ee3dc-112">要檢查與其連線的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="ee3dc-112">Virtual machines to check connectivity with.</span></span>

[!INCLUDE [network-watcher-preview](../../includes/network-watcher-public-preview-notice.md)]

> [!IMPORTANT]
> <span data-ttu-id="ee3dc-113">連線檢查需要虛擬機器延伸模組 `AzureNetworkWatcherExtension`。</span><span class="sxs-lookup"><span data-stu-id="ee3dc-113">Connectivity check requires a virtual machine extension `AzureNetworkWatcherExtension`.</span></span> <span data-ttu-id="ee3dc-114">若要在 Windows VM 上安裝擴充功能，請瀏覽[適用於 Windows 的 Azure 網路監看員代理程式虛擬機器擴充功能](../virtual-machines/windows/extensions-nwa.md)，若要在 Linux VM 上安裝，則請瀏覽[適用於 Linux 的 Azure 網路監看員代理程式虛擬機器擴充功能](../virtual-machines/linux/extensions-nwa.md)。</span><span class="sxs-lookup"><span data-stu-id="ee3dc-114">For installing the extension on a Windows VM visit [Azure Network Watcher Agent virtual machine extension for Windows](../virtual-machines/windows/extensions-nwa.md) and for Linux VM visit [Azure Network Watcher Agent virtual machine extension for Linux](../virtual-machines/linux/extensions-nwa.md).</span></span>

## <a name="register-the-preview-capability"></a><span data-ttu-id="ee3dc-115">註冊預覽功能</span><span class="sxs-lookup"><span data-stu-id="ee3dc-115">Register the preview capability</span></span>

<span data-ttu-id="ee3dc-116">連線目前為公開預覽版本，若要使用這項功能，必須先註冊它。</span><span class="sxs-lookup"><span data-stu-id="ee3dc-116">Connectivity is currently in public preview, to use this feature it needs to be registered.</span></span> <span data-ttu-id="ee3dc-117">若要這麼做，請執行下列 PowerShell 範例：</span><span class="sxs-lookup"><span data-stu-id="ee3dc-117">To do this, run the following PowerShell sample:</span></span>

```powershell
Register-AzureRmProviderFeature -FeatureName AllowNetworkWatcherConnectivityCheck  -ProviderNamespace Microsoft.Network
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.Network
```

<span data-ttu-id="ee3dc-118">若要確認註冊是否成功，請執行下列 Powershell 範例︰</span><span class="sxs-lookup"><span data-stu-id="ee3dc-118">To verify the registration was successful, run the following Powershell sample:</span></span>

```powershell
Get-AzureRmProviderFeature -FeatureName AllowNetworkWatcherConnectivityCheck  -ProviderNamespace  Microsoft.Network
```

<span data-ttu-id="ee3dc-119">如果已正確註冊該功能，輸出應該會與以下相符︰</span><span class="sxs-lookup"><span data-stu-id="ee3dc-119">If the feature was properly registered, the output should match the following:</span></span>

```
FeatureName         ProviderName      RegistrationState
-----------         ------------      -----------------
AllowNetworkWatcherConnectivityCheck  Microsoft.Network Registered
```

## <a name="check-connectivity-to-a-virtual-machine"></a><span data-ttu-id="ee3dc-120">檢查與虛擬機器的連線</span><span class="sxs-lookup"><span data-stu-id="ee3dc-120">Check connectivity to a virtual machine</span></span>

<span data-ttu-id="ee3dc-121">這個範例會檢查透過連接埠 80 的目的地虛擬機器連線。</span><span class="sxs-lookup"><span data-stu-id="ee3dc-121">This example checks connectivity to a destination virtual machine over port 80.</span></span>

### <a name="example"></a><span data-ttu-id="ee3dc-122">範例</span><span class="sxs-lookup"><span data-stu-id="ee3dc-122">Example</span></span>

```powershell
$rgName = "ContosoRG"
$sourceVMName = "MultiTierApp0"
$destVMName = "Database0"

$RG = Get-AzureRMResourceGroup -Name $rgName

$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq $RG.Location } 
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName

$VM1 = Get-AzureRMVM -ResourceGroupName $rgName | Where-Object -Property Name -EQ $sourceVMName
$VM2 = Get-AzureRMVM -ResourceGroupName $rgName | Where-Object -Property Name -EQ $destVMName

Test-AzureRmNetworkWatcherConnectivity -NetworkWatcher $networkWatcher -SourceId $VM1.Id -DestinationId $VM2.Id -DestinationPort 80
```

### <a name="response"></a><span data-ttu-id="ee3dc-123">Response</span><span class="sxs-lookup"><span data-stu-id="ee3dc-123">Response</span></span>

<span data-ttu-id="ee3dc-124">下列回應是來自上一個範例。</span><span class="sxs-lookup"><span data-stu-id="ee3dc-124">The following response is from the previous example.</span></span>  <span data-ttu-id="ee3dc-125">在此回應中，`ConnectionStatus` 為 [無法連線]。</span><span class="sxs-lookup"><span data-stu-id="ee3dc-125">In this response, the `ConnectionStatus` is **Unreachable**.</span></span> <span data-ttu-id="ee3dc-126">您可以看到傳送的所有探查都失敗。</span><span class="sxs-lookup"><span data-stu-id="ee3dc-126">You can see that all the probes sent failed.</span></span> <span data-ttu-id="ee3dc-127">因為名為 **UserRule_Port80** 的使用者設定 `NetworkSecurityRule` 設定成封鎖連接埠 80 的連入流量，所以虛擬設備的連線失敗。</span><span class="sxs-lookup"><span data-stu-id="ee3dc-127">The connectivity failed at the virtual appliance due to a user-configured `NetworkSecurityRule` named **UserRule_Port80**, configured to block incoming traffic on port 80.</span></span> <span data-ttu-id="ee3dc-128">這項資訊可以用來研究連線問題。</span><span class="sxs-lookup"><span data-stu-id="ee3dc-128">This information can be used to research connection issues.</span></span>

```
ConnectionStatus : Unreachable
AvgLatencyInMs   : 
MinLatencyInMs   : 
MaxLatencyInMs   : 
ProbesSent       : 100
ProbesFailed     : 100
Hops             : [
                     {
                       "Type": "Source",
                       "Id": "c5222ea0-3213-4f85-a642-cee63217c2f3",
                       "Address": "10.1.1.4",
                       "ResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGrou
                   ps/ContosoRG/providers/Microsoft.Network/networkInterfaces/appNic0/ipConfigurat
                   ions/ipconfig1",
                       "NextHopIds": [
                         "9283a9f0-cc5e-4239-8f5e-ae0f3c19fbaa"
                       ],
                       "Issues": []
                     },
                     {
                       "Type": "VirtualAppliance",
                       "Id": "9283a9f0-cc5e-4239-8f5e-ae0f3c19fbaa",
                       "Address": "10.1.2.4",
                       "ResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGrou
                   ps/ContosoRG/providers/Microsoft.Network/networkInterfaces/fwNic/ipConfiguratio
                   ns/ipconfig1",
                       "NextHopIds": [
                         "0f1500cd-c512-4d43-b431-7267e4e67017"
                       ],
                       "Issues": []
                     },
                     {
                       "Type": "VirtualAppliance",
                       "Id": "0f1500cd-c512-4d43-b431-7267e4e67017",
                       "Address": "10.1.3.4",
                       "ResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGrou
                   ps/ContosoRG/providers/Microsoft.Network/networkInterfaces/auNic/ipConfiguratio
                   ns/ipconfig1",
                       "NextHopIds": [
                         "a88940f8-5fbe-40da-8d99-1dee89240f64"
                       ],
                       "Issues": [
                         {
                           "Origin": "Outbound",
                           "Severity": "Error",
                           "Type": "NetworkSecurityRule",
                           "Context": [
                             {
                               "key": "RuleName",
                               "value": "UserRule_Port80"
                             }
                           ]
                         }
                       ]
                     },
                     {
                       "Type": "VnetLocal",
                       "Id": "a88940f8-5fbe-40da-8d99-1dee89240f64",
                       "Address": "10.1.4.4",
                       "ResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGrou
                   ps/ContosoRG/providers/Microsoft.Network/networkInterfaces/dbNic0/ipConfigurati
                   ons/ipconfig1",
                       "NextHopIds": [],
                       "Issues": []
                     }
                   ]
```

## <a name="validate-routing-issues"></a><span data-ttu-id="ee3dc-129">驗證路由問題</span><span class="sxs-lookup"><span data-stu-id="ee3dc-129">Validate routing issues</span></span>

<span data-ttu-id="ee3dc-130">此範例會檢查虛擬機器與遠端端點之間的連線。</span><span class="sxs-lookup"><span data-stu-id="ee3dc-130">The example checks connectivity between a virtual machine and a remote endpoint.</span></span>

### <a name="example"></a><span data-ttu-id="ee3dc-131">範例</span><span class="sxs-lookup"><span data-stu-id="ee3dc-131">Example</span></span>

```powershell
$rgName = "ContosoRG"
$sourceVMName = "MultiTierApp0"

$RG = Get-AzureRMResourceGroup -Name $rgName

$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq $RG.Location } 
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName

$VM1 = Get-AzureRMVM -ResourceGroupName $rgName | Where-Object -Property Name -EQ $sourceVMName

Test-AzureRmNetworkWatcherConnectivity -NetworkWatcher $networkWatcher -SourceId $VM1.Id -DestinationAddress 13.107.21.200 -DestinationPort 80
```

### <a name="response"></a><span data-ttu-id="ee3dc-132">Response</span><span class="sxs-lookup"><span data-stu-id="ee3dc-132">Response</span></span>

<span data-ttu-id="ee3dc-133">在下列範例中，`ConnectionStatus` 會顯示為 [無法連線]。</span><span class="sxs-lookup"><span data-stu-id="ee3dc-133">In the following example, the `ConnectionStatus` is shown as **Unreachable**.</span></span> <span data-ttu-id="ee3dc-134">在 `Hops` 詳細資料中，您可以在 `Issues` 下看到已因 `UserDefinedRoute` 而封鎖流量。</span><span class="sxs-lookup"><span data-stu-id="ee3dc-134">In the `Hops` details, you can see under `Issues` that the traffic was blocked due to a `UserDefinedRoute`.</span></span> 

```
ConnectionStatus : Unreachable
AvgLatencyInMs   : 
MinLatencyInMs   : 
MaxLatencyInMs   : 
ProbesSent       : 100
ProbesFailed     : 100
Hops             : [
                     {
                       "Type": "Source",
                       "Id": "b4f7bceb-07a3-44ca-8bae-adec6628225f",
                       "Address": "10.1.1.4",
                       "ResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/appNic0/ipConfigurations/ipconfig1",
                       "NextHopIds": [
                         "3fee8adf-692f-4523-b742-f6fdf6da6584"
                       ],
                       "Issues": [
                         {
                           "Origin": "Outbound",
                           "Severity": "Error",
                           "Type": "UserDefinedRoute",
                           "Context": [
                             {
                               "key": "RouteType",
                               "value": "User"
                             }
                           ]
                         }
                       ]
                     },
                     {
                       "Type": "Destination",
                       "Id": "3fee8adf-692f-4523-b742-f6fdf6da6584",
                       "Address": "13.107.21.200",
                       "ResourceId": "Unknown",
                       "NextHopIds": [],
                       "Issues": []
                     }
                   ]
```

## <a name="check-website-latency"></a><span data-ttu-id="ee3dc-135">檢查網站延遲</span><span class="sxs-lookup"><span data-stu-id="ee3dc-135">Check website latency</span></span>

<span data-ttu-id="ee3dc-136">下列範例會檢查網站連線。</span><span class="sxs-lookup"><span data-stu-id="ee3dc-136">The following example checks the connectivity to a website.</span></span>

### <a name="example"></a><span data-ttu-id="ee3dc-137">範例</span><span class="sxs-lookup"><span data-stu-id="ee3dc-137">Example</span></span>

```powershell
$rgName = "ContosoRG"
$sourceVMName = "MultiTierApp0"

$RG = Get-AzureRMResourceGroup -Name $rgName

$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq $RG.Location } 
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName

$VM1 = Get-AzureRMVM -ResourceGroupName $rgName | Where-Object -Property Name -EQ $sourceVMName

Test-AzureRmNetworkWatcherConnectivity -NetworkWatcher $networkWatcher -SourceId $VM1.Id -DestinationAddress http://bing.com/
```

### <a name="response"></a><span data-ttu-id="ee3dc-138">Response</span><span class="sxs-lookup"><span data-stu-id="ee3dc-138">Response</span></span>

<span data-ttu-id="ee3dc-139">在下列回應中，您可以看到 `ConnectionStatus` 顯示為 [可以連線]。</span><span class="sxs-lookup"><span data-stu-id="ee3dc-139">In the following response, you can see the `ConnectionStatus` shows as **Reachable**.</span></span> <span data-ttu-id="ee3dc-140">連線成功時，會提供延遲值。</span><span class="sxs-lookup"><span data-stu-id="ee3dc-140">When a connection is successful, latency values are provided.</span></span>

```
ConnectionStatus : Reachable
AvgLatencyInMs   : 1
MinLatencyInMs   : 0
MaxLatencyInMs   : 7
ProbesSent       : 100
ProbesFailed     : 0
Hops             : [
                     {
                       "Type": "Source",
                       "Id": "1f0e3415-27b0-4bf7-a59d-3e19fb854e3e",
                       "Address": "10.1.1.4",
                       "ResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/appNic0/ipConfigurations/ipconfig1",
                       "NextHopIds": [
                         "f99f2bd1-42e8-4bbf-85b6-5d21d00c84e0"
                       ],
                       "Issues": []
                     },
                     {
                       "Type": "Internet",
                       "Id": "f99f2bd1-42e8-4bbf-85b6-5d21d00c84e0",
                       "Address": "204.79.197.200",
                       "ResourceId": "Internet",
                       "NextHopIds": [],
                       "Issues": []
                     }
                   ]
```

## <a name="check-connectivity-to-a-storage-endpoint"></a><span data-ttu-id="ee3dc-141">檢查與儲存體端點的連線</span><span class="sxs-lookup"><span data-stu-id="ee3dc-141">Check connectivity to a storage endpoint</span></span>

<span data-ttu-id="ee3dc-142">下列範例會測試從虛擬機器到部落格儲存體帳戶的連線。</span><span class="sxs-lookup"><span data-stu-id="ee3dc-142">The following example tests the connectivity from a virtual machine to a blog storage account.</span></span>

### <a name="example"></a><span data-ttu-id="ee3dc-143">範例</span><span class="sxs-lookup"><span data-stu-id="ee3dc-143">Example</span></span>

```powershell
$rgName = "ContosoRG"
$sourceVMName = "MultiTierApp0"

$RG = Get-AzureRMResourceGroup -Name $rgName

$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq $RG.Location }
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName

$VM1 = Get-AzureRMVM -ResourceGroupName $rgName | Where-Object -Property Name -EQ $sourceVMName

Test-AzureRmNetworkWatcherConnectivity -NetworkWatcher $networkWatcher -SourceId $VM1.Id -DestinationAddress https://contosostorageexample.blob.core.windows.net/ 
```

### <a name="response"></a><span data-ttu-id="ee3dc-144">Response</span><span class="sxs-lookup"><span data-stu-id="ee3dc-144">Response</span></span>

<span data-ttu-id="ee3dc-145">下列 JSON 是執行前一個 Cmdlet 的範例回應。</span><span class="sxs-lookup"><span data-stu-id="ee3dc-145">The following json is the example response from running the previous cmdlet.</span></span> <span data-ttu-id="ee3dc-146">因為可以連線目的地，所以 `ConnectionStatus` 屬性會顯示為 [可以連線]。</span><span class="sxs-lookup"><span data-stu-id="ee3dc-146">As the destination is reachable, the `ConnectionStatus` property shows as **Reachable**.</span></span>  <span data-ttu-id="ee3dc-147">系統會向您提供連線儲存體 Blob 和延遲所需躍點數目的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="ee3dc-147">You are provided the details regarding the number of hops required to reach the storage blob and latency.</span></span>

```
ConnectionStatus : Reachable
AvgLatencyInMs   : 1
MinLatencyInMs   : 0
MaxLatencyInMs   : 8
ProbesSent       : 100
ProbesFailed     : 0
Hops             : [
                     {
                       "Type": "Source",
                       "Id": "9e7f61d9-fb45-41db-83e2-c815a919b8ed",
                       "Address": "10.1.1.4",
                       "ResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/appNic0/ipConfigurations/ipconfig1",
                       "NextHopIds": [
                         "1e6d4b3c-7964-4afd-b959-aaa746ee0f15"
                       ],
                       "Issues": []
                     },
                     {
                       "Type": "Internet",
                       "Id": "1e6d4b3c-7964-4afd-b959-aaa746ee0f15",
                       "Address": "13.71.200.248",
                       "ResourceId": "Internet",
                       "NextHopIds": [],
                       "Issues": []
                     }
                   ]
```

## <a name="next-steps"></a><span data-ttu-id="ee3dc-148">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ee3dc-148">Next steps</span></span>

<span data-ttu-id="ee3dc-149">造訪[檢查 IP 流量驗證](network-watcher-check-ip-flow-verify-portal.md)來得知 VM 是否允許特定流量流入或流出</span><span class="sxs-lookup"><span data-stu-id="ee3dc-149">Find if certain traffic is allowed in or out of your VM by visiting [Check IP flow verify](network-watcher-check-ip-flow-verify-portal.md)</span></span>

<span data-ttu-id="ee3dc-150">如果流量遭到封鎖，但不應如此，請參閱[管理網路安全性群組](../virtual-network/virtual-network-manage-nsg-arm-portal.md)以追蹤網路安全性群組和所定義的安全性規則。</span><span class="sxs-lookup"><span data-stu-id="ee3dc-150">If traffic is being blocked and it should not be, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) to track down the network security group and security rules that are defined.</span></span>

<!-- Image references -->














