---
title: "與 Azure 網路監看員-PowerShell aaaCheck 連線 |Microsoft 文件"
description: "此頁面說明如何使用 PowerShell 的網路監看員 tootest 連線"
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
ms.openlocfilehash: 4bcb90a72f178445c38b7bd7fc5054c5d0c200bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="check-connectivity-with-azure-network-watcher-using-powershell"></a><span data-ttu-id="a65ac-103">使用 PowerShell 檢查與 Azure 網路監看員的連線</span><span class="sxs-lookup"><span data-stu-id="a65ac-103">Check connectivity with Azure Network Watcher using PowerShell</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="a65ac-104">入口網站</span><span class="sxs-lookup"><span data-stu-id="a65ac-104">Portal</span></span>](network-watcher-connectivity-portal.md)
> - [<span data-ttu-id="a65ac-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a65ac-105">PowerShell</span></span>](network-watcher-connectivity-powershell.md)
> - [<span data-ttu-id="a65ac-106">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="a65ac-106">CLI 2.0</span></span>](network-watcher-connectivity-cli.md)
> - [<span data-ttu-id="a65ac-107">Azure REST API</span><span class="sxs-lookup"><span data-stu-id="a65ac-107">Azure REST API</span></span>](network-watcher-connectivity-rest.md)

<span data-ttu-id="a65ac-108">了解可以如何建立 toouse 連線 tooverify 如果從虛擬機器 tooa 指定端點的直接 TCP 連接。</span><span class="sxs-lookup"><span data-stu-id="a65ac-108">Learn how toouse connectivity tooverify if a direct TCP connection from a virtual machine tooa given endpoint can be established.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="a65ac-109">開始之前</span><span class="sxs-lookup"><span data-stu-id="a65ac-109">Before you begin</span></span>

<span data-ttu-id="a65ac-110">本文假設您擁有 hello 下列資源：</span><span class="sxs-lookup"><span data-stu-id="a65ac-110">This article assumes you have hello following resources:</span></span>

* <span data-ttu-id="a65ac-111">執行個體要 toocheck 連線的網路監看員 hello 區域中。</span><span class="sxs-lookup"><span data-stu-id="a65ac-111">An instance of Network Watcher in hello region you want toocheck connectivity.</span></span>

* <span data-ttu-id="a65ac-112">虛擬機器與 toocheck 連線。</span><span class="sxs-lookup"><span data-stu-id="a65ac-112">Virtual machines toocheck connectivity with.</span></span>

[!INCLUDE [network-watcher-preview](../../includes/network-watcher-public-preview-notice.md)]

> [!IMPORTANT]
> <span data-ttu-id="a65ac-113">連線檢查需要虛擬機器延伸模組 `AzureNetworkWatcherExtension`。</span><span class="sxs-lookup"><span data-stu-id="a65ac-113">Connectivity check requires a virtual machine extension `AzureNetworkWatcherExtension`.</span></span> <span data-ttu-id="a65ac-114">Hello 擴充功能安裝在 Windows VM 上瀏覽[Azure 網路監看員的代理程式適用於 Windows 的虛擬機器擴充功能](../virtual-machines/windows/extensions-nwa.md)和如 Linux VM，請造訪[Azure 網路監看員的代理程式虛擬機器擴充功能，適用於 Linux](../virtual-machines/linux/extensions-nwa.md).</span><span class="sxs-lookup"><span data-stu-id="a65ac-114">For installing hello extension on a Windows VM visit [Azure Network Watcher Agent virtual machine extension for Windows](../virtual-machines/windows/extensions-nwa.md) and for Linux VM visit [Azure Network Watcher Agent virtual machine extension for Linux](../virtual-machines/linux/extensions-nwa.md).</span></span>

## <a name="register-hello-preview-capability"></a><span data-ttu-id="a65ac-115">註冊 hello 預覽功能</span><span class="sxs-lookup"><span data-stu-id="a65ac-115">Register hello preview capability</span></span>

<span data-ttu-id="a65ac-116">連線目前處於公開預覽，toouse 需要 toobe 註冊這項功能。</span><span class="sxs-lookup"><span data-stu-id="a65ac-116">Connectivity is currently in public preview, toouse this feature it needs toobe registered.</span></span> <span data-ttu-id="a65ac-117">toodo，執行下列 PowerShell 範例的 hello:</span><span class="sxs-lookup"><span data-stu-id="a65ac-117">toodo this, run hello following PowerShell sample:</span></span>

```powershell
Register-AzureRmProviderFeature -FeatureName AllowNetworkWatcherConnectivityCheck  -ProviderNamespace Microsoft.Network
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.Network
```

<span data-ttu-id="a65ac-118">tooverify hello 登錄成功，執行下列 Powershell 範例 hello:</span><span class="sxs-lookup"><span data-stu-id="a65ac-118">tooverify hello registration was successful, run hello following Powershell sample:</span></span>

```powershell
Get-AzureRmProviderFeature -FeatureName AllowNetworkWatcherConnectivityCheck  -ProviderNamespace  Microsoft.Network
```

<span data-ttu-id="a65ac-119">如果 hello 功能已正確註冊，hello 輸出應符合下列 hello:</span><span class="sxs-lookup"><span data-stu-id="a65ac-119">If hello feature was properly registered, hello output should match hello following:</span></span>

```
FeatureName         ProviderName      RegistrationState
-----------         ------------      -----------------
AllowNetworkWatcherConnectivityCheck  Microsoft.Network Registered
```

## <a name="check-connectivity-tooa-virtual-machine"></a><span data-ttu-id="a65ac-120">請檢查連線 tooa 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="a65ac-120">Check connectivity tooa virtual machine</span></span>

<span data-ttu-id="a65ac-121">這個範例會檢查透過連接埠 80 連線 tooa 目的地虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="a65ac-121">This example checks connectivity tooa destination virtual machine over port 80.</span></span>

### <a name="example"></a><span data-ttu-id="a65ac-122">範例</span><span class="sxs-lookup"><span data-stu-id="a65ac-122">Example</span></span>

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

### <a name="response"></a><span data-ttu-id="a65ac-123">Response</span><span class="sxs-lookup"><span data-stu-id="a65ac-123">Response</span></span>

<span data-ttu-id="a65ac-124">下列回應 hello 取自 hello 前一個範例。</span><span class="sxs-lookup"><span data-stu-id="a65ac-124">hello following response is from hello previous example.</span></span>  <span data-ttu-id="a65ac-125">此回應 hello`ConnectionStatus`是**連線**。</span><span class="sxs-lookup"><span data-stu-id="a65ac-125">In this response, hello `ConnectionStatus` is **Unreachable**.</span></span> <span data-ttu-id="a65ac-126">您可以看到所有 hello 探查傳送失敗。</span><span class="sxs-lookup"><span data-stu-id="a65ac-126">You can see that all hello probes sent failed.</span></span> <span data-ttu-id="a65ac-127">hello 連線無法在 hello 虛擬應用裝置使用者設定的到期 tooa`NetworkSecurityRule`名為**UserRule_Port80**，通訊埠 80 上設定 tooblock 連入流量。</span><span class="sxs-lookup"><span data-stu-id="a65ac-127">hello connectivity failed at hello virtual appliance due tooa user-configured `NetworkSecurityRule` named **UserRule_Port80**, configured tooblock incoming traffic on port 80.</span></span> <span data-ttu-id="a65ac-128">這項資訊可以使用的 tooresearch 連線問題。</span><span class="sxs-lookup"><span data-stu-id="a65ac-128">This information can be used tooresearch connection issues.</span></span>

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

## <a name="validate-routing-issues"></a><span data-ttu-id="a65ac-129">驗證路由問題</span><span class="sxs-lookup"><span data-stu-id="a65ac-129">Validate routing issues</span></span>

<span data-ttu-id="a65ac-130">hello 範例會檢查虛擬機器與遠端端點之間的連線。</span><span class="sxs-lookup"><span data-stu-id="a65ac-130">hello example checks connectivity between a virtual machine and a remote endpoint.</span></span>

### <a name="example"></a><span data-ttu-id="a65ac-131">範例</span><span class="sxs-lookup"><span data-stu-id="a65ac-131">Example</span></span>

```powershell
$rgName = "ContosoRG"
$sourceVMName = "MultiTierApp0"

$RG = Get-AzureRMResourceGroup -Name $rgName

$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq $RG.Location } 
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName

$VM1 = Get-AzureRMVM -ResourceGroupName $rgName | Where-Object -Property Name -EQ $sourceVMName

Test-AzureRmNetworkWatcherConnectivity -NetworkWatcher $networkWatcher -SourceId $VM1.Id -DestinationAddress 13.107.21.200 -DestinationPort 80
```

### <a name="response"></a><span data-ttu-id="a65ac-132">Response</span><span class="sxs-lookup"><span data-stu-id="a65ac-132">Response</span></span>

<span data-ttu-id="a65ac-133">在下列範例的 hello，hello`ConnectionStatus`會顯示為**連線**。</span><span class="sxs-lookup"><span data-stu-id="a65ac-133">In hello following example, hello `ConnectionStatus` is shown as **Unreachable**.</span></span> <span data-ttu-id="a65ac-134">在 hello`Hops`詳細資料，您可以看到下`Issues`hello 流量遭到封鎖到期 tooa `UserDefinedRoute`。</span><span class="sxs-lookup"><span data-stu-id="a65ac-134">In hello `Hops` details, you can see under `Issues` that hello traffic was blocked due tooa `UserDefinedRoute`.</span></span> 

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

## <a name="check-website-latency"></a><span data-ttu-id="a65ac-135">檢查網站延遲</span><span class="sxs-lookup"><span data-stu-id="a65ac-135">Check website latency</span></span>

<span data-ttu-id="a65ac-136">hello 下列範例會檢查 hello 連線 tooa 網站。</span><span class="sxs-lookup"><span data-stu-id="a65ac-136">hello following example checks hello connectivity tooa website.</span></span>

### <a name="example"></a><span data-ttu-id="a65ac-137">範例</span><span class="sxs-lookup"><span data-stu-id="a65ac-137">Example</span></span>

```powershell
$rgName = "ContosoRG"
$sourceVMName = "MultiTierApp0"

$RG = Get-AzureRMResourceGroup -Name $rgName

$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq $RG.Location } 
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName

$VM1 = Get-AzureRMVM -ResourceGroupName $rgName | Where-Object -Property Name -EQ $sourceVMName

Test-AzureRmNetworkWatcherConnectivity -NetworkWatcher $networkWatcher -SourceId $VM1.Id -DestinationAddress http://bing.com/
```

### <a name="response"></a><span data-ttu-id="a65ac-138">Response</span><span class="sxs-lookup"><span data-stu-id="a65ac-138">Response</span></span>

<span data-ttu-id="a65ac-139">在下列回應 hello，您可以看到 hello`ConnectionStatus`顯示為**Reachable**。</span><span class="sxs-lookup"><span data-stu-id="a65ac-139">In hello following response, you can see hello `ConnectionStatus` shows as **Reachable**.</span></span> <span data-ttu-id="a65ac-140">連線成功時，會提供延遲值。</span><span class="sxs-lookup"><span data-stu-id="a65ac-140">When a connection is successful, latency values are provided.</span></span>

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

## <a name="check-connectivity-tooa-storage-endpoint"></a><span data-ttu-id="a65ac-141">請檢查連線 tooa 儲存體端點</span><span class="sxs-lookup"><span data-stu-id="a65ac-141">Check connectivity tooa storage endpoint</span></span>

<span data-ttu-id="a65ac-142">下列範例中的 hello 測試 hello 連線能力，從虛擬機器 tooa 部落格儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="a65ac-142">hello following example tests hello connectivity from a virtual machine tooa blog storage account.</span></span>

### <a name="example"></a><span data-ttu-id="a65ac-143">範例</span><span class="sxs-lookup"><span data-stu-id="a65ac-143">Example</span></span>

```powershell
$rgName = "ContosoRG"
$sourceVMName = "MultiTierApp0"

$RG = Get-AzureRMResourceGroup -Name $rgName

$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq $RG.Location }
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName

$VM1 = Get-AzureRMVM -ResourceGroupName $rgName | Where-Object -Property Name -EQ $sourceVMName

Test-AzureRmNetworkWatcherConnectivity -NetworkWatcher $networkWatcher -SourceId $VM1.Id -DestinationAddress https://contosostorageexample.blob.core.windows.net/ 
```

### <a name="response"></a><span data-ttu-id="a65ac-144">Response</span><span class="sxs-lookup"><span data-stu-id="a65ac-144">Response</span></span>

<span data-ttu-id="a65ac-145">hello 下列 json 是 hello 執行 hello 前一個 cmdlet 的範例回應。</span><span class="sxs-lookup"><span data-stu-id="a65ac-145">hello following json is hello example response from running hello previous cmdlet.</span></span> <span data-ttu-id="a65ac-146">因為取得 hello 目的地，hello`ConnectionStatus`屬性會顯示為**Reachable**。</span><span class="sxs-lookup"><span data-stu-id="a65ac-146">As hello destination is reachable, hello `ConnectionStatus` property shows as **Reachable**.</span></span>  <span data-ttu-id="a65ac-147">為您提供有關 hello 數目躍點需要的 tooreach hello 儲存體 blob 和延遲的 hello 詳細資料。</span><span class="sxs-lookup"><span data-stu-id="a65ac-147">You are provided hello details regarding hello number of hops required tooreach hello storage blob and latency.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="a65ac-148">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a65ac-148">Next steps</span></span>

<span data-ttu-id="a65ac-149">造訪[檢查 IP 流量驗證](network-watcher-check-ip-flow-verify-portal.md)來得知 VM 是否允許特定流量流入或流出</span><span class="sxs-lookup"><span data-stu-id="a65ac-149">Find if certain traffic is allowed in or out of your VM by visiting [Check IP flow verify](network-watcher-check-ip-flow-verify-portal.md)</span></span>

<span data-ttu-id="a65ac-150">如果正在封鎖流量，不應該看到[管理網路安全性群組](../virtual-network/virtual-network-manage-nsg-arm-portal.md)tootrack hello 網路安全性群組和安全性規則所定義的關閉。</span><span class="sxs-lookup"><span data-stu-id="a65ac-150">If traffic is being blocked and it should not be, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack down hello network security group and security rules that are defined.</span></span>

<!-- Image references -->














