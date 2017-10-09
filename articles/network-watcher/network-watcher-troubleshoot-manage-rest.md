---
title: "aaaTroubleshoot 虛擬網路閘道連線使用的 Azure 網路監看員的 REST 和 |Microsoft 文件"
description: "此頁面說明 tootroubleshoot 虛擬網路閘道使用 Azure 網路監看員連接如何 REST"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: e4d5f195-b839-4394-94ef-a04192766e55
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/19/2017
ms.author: gwallace
ms.openlocfilehash: cc89b46643fdbfefe53727b45d6b7d06914b58a6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-virtual-network-gateway-and-connections-using-azure-network-watcher"></a><span data-ttu-id="f108b-103">使用 Azure 網路監看員來針對虛擬網路閘道和連線進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="f108b-103">Troubleshoot Virtual Network gateway and Connections using Azure Network Watcher</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="f108b-104">入口網站</span><span class="sxs-lookup"><span data-stu-id="f108b-104">Portal</span></span>](network-watcher-troubleshoot-manage-portal.md)
> - [<span data-ttu-id="f108b-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f108b-105">PowerShell</span></span>](network-watcher-troubleshoot-manage-powershell.md)
> - [<span data-ttu-id="f108b-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="f108b-106">CLI 1.0</span></span>](network-watcher-troubleshoot-manage-cli-nodejs.md)
> - [<span data-ttu-id="f108b-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="f108b-107">CLI 2.0</span></span>](network-watcher-troubleshoot-manage-cli.md)
> - [<span data-ttu-id="f108b-108">REST API</span><span class="sxs-lookup"><span data-stu-id="f108b-108">REST API</span></span>](network-watcher-troubleshoot-manage-rest.md)

<span data-ttu-id="f108b-109">網路監看員會提供許多功能與 toounderstanding 您在 Azure 中的網路資源。</span><span class="sxs-lookup"><span data-stu-id="f108b-109">Network Watcher provides many capabilities as it relates toounderstanding your network resources in Azure.</span></span> <span data-ttu-id="f108b-110">這些功能的其中之一便是資源疑難排解。</span><span class="sxs-lookup"><span data-stu-id="f108b-110">One of these capabilities is resource troubleshooting.</span></span> <span data-ttu-id="f108b-111">疑難排解資源可以透過 hello 入口網站、 PowerShell、 CLI 或 REST API 呼叫。</span><span class="sxs-lookup"><span data-stu-id="f108b-111">Resource troubleshooting can be called through hello portal, PowerShell, CLI, or REST API.</span></span> <span data-ttu-id="f108b-112">呼叫時，網路監看員會檢查 hello 的虛擬網路閘道或連線的健全狀況，並傳回其發現。</span><span class="sxs-lookup"><span data-stu-id="f108b-112">When called, Network Watcher inspects hello health of a Virtual Network Gateway or a Connection and returns its findings.</span></span>

<span data-ttu-id="f108b-113">這篇文章會帶領您完成疑難排解資源的目前可用的 hello 不同的管理工作。</span><span class="sxs-lookup"><span data-stu-id="f108b-113">This article takes you through hello different management tasks that are currently available for resource troubleshooting.</span></span>

- [<span data-ttu-id="f108b-114">針對虛擬網路閘道進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="f108b-114">**Troubleshoot a Virtual Network gateway**</span></span>](#troubleshoot-a-virtual-network-gateway)
- [<span data-ttu-id="f108b-115">針對連線進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="f108b-115">**Troubleshoot a Connection**</span></span>](#troubleshoot-connections)

## <a name="before-you-begin"></a><span data-ttu-id="f108b-116">開始之前</span><span class="sxs-lookup"><span data-stu-id="f108b-116">Before you begin</span></span>

<span data-ttu-id="f108b-117">ARMclient 是使用 PowerShell 的使用的 toocall hello REST API。</span><span class="sxs-lookup"><span data-stu-id="f108b-117">ARMclient is used toocall hello REST API using PowerShell.</span></span> <span data-ttu-id="f108b-118">您可以在 chocolatey 的 [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient) 上找到 ARMClient</span><span class="sxs-lookup"><span data-stu-id="f108b-118">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient)</span></span>

<span data-ttu-id="f108b-119">此案例假設您已依照中的 hello 步驟[建立網路監看員](network-watcher-create.md)toocreate 網路監看員。</span><span class="sxs-lookup"><span data-stu-id="f108b-119">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span>

<span data-ttu-id="f108b-120">如需支援的閘道類型清單，請瀏覽[支援的閘道類型](network-watcher-troubleshoot-overview.md#supported-gateway-types)。</span><span class="sxs-lookup"><span data-stu-id="f108b-120">For a list of supported gateway types visit, [Supported Gateway types](network-watcher-troubleshoot-overview.md#supported-gateway-types).</span></span>

## <a name="overview"></a><span data-ttu-id="f108b-121">概觀</span><span class="sxs-lookup"><span data-stu-id="f108b-121">Overview</span></span>

<span data-ttu-id="f108b-122">網路監看員疑難排解提供 hello 功能的虛擬網路閘道與連線發生問題進行疑難排解。</span><span class="sxs-lookup"><span data-stu-id="f108b-122">Network Watcher troubleshooting provides hello ability troubleshoot issues that arise with Virtual Network gateways and Connections.</span></span> <span data-ttu-id="f108b-123">Toohello 資源提出的要求時疑難排解記錄檔要查詢及檢查。</span><span class="sxs-lookup"><span data-stu-id="f108b-123">When a request is made toohello resource troubleshooting, logs are querying and inspected.</span></span> <span data-ttu-id="f108b-124">檢查完成時，會傳回 hello 結果。</span><span class="sxs-lookup"><span data-stu-id="f108b-124">When inspection is complete, hello results are returned.</span></span> <span data-ttu-id="f108b-125">hello 疑難排解應用程式開發介面要求是長時間執行的要求，這可能需要多個分鐘 tooreturn 結果。</span><span class="sxs-lookup"><span data-stu-id="f108b-125">hello troubleshoot API requests are long running requests, which could take multiple minutes tooreturn a result.</span></span> <span data-ttu-id="f108b-126">記錄會儲存在儲存體帳戶的容器中。</span><span class="sxs-lookup"><span data-stu-id="f108b-126">Logs are stored in a container on a storage account.</span></span>

## <a name="log-in-with-armclient"></a><span data-ttu-id="f108b-127">使用 ARMClient 登入</span><span class="sxs-lookup"><span data-stu-id="f108b-127">Log in with ARMClient</span></span>

```PowerShell
armclient login
```

## <a name="troubleshoot-a-virtual-network-gateway"></a><span data-ttu-id="f108b-128">針對虛擬網路閘道進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="f108b-128">Troubleshoot a Virtual Network gateway</span></span>


### <a name="post-hello-troubleshoot-request"></a><span data-ttu-id="f108b-129">POST hello 疑難排解要求</span><span class="sxs-lookup"><span data-stu-id="f108b-129">POST hello troubleshoot request</span></span>

<span data-ttu-id="f108b-130">下列範例查詢 hello 狀態的虛擬網路閘道的 hello。</span><span class="sxs-lookup"><span data-stu-id="f108b-130">hello following example queries hello status of a Virtual Network gateway.</span></span>

```powershell

$subscriptionId = "00000000-0000-0000-0000-000000000000"
$resourceGroupName = "ContosoRG"
$NWresourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$vnetGatewayName = "ContosoVNETGateway"
$storageAccountName = "contososa"
$containerName = "gwlogs"
$requestBody = @"
{
'TargetResourceId': '/subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/Microsoft.Network/virtualNetworkGateways/${vnetGatewayName}',
'Properties': {
'StorageId': '/subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/Microsoft.Storage/storageAccounts/${storageAccountName}',
'StoragePath': 'https://${storageAccountName}.blob.core.windows.net/${containerName}'
}
}
"@

}
armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${NWresourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/troubleshoot?api-version=2016-03-30 "
```

<span data-ttu-id="f108b-131">由於這項作業是長時間執行，hello URI 查詢 hello 作業，且下列回應 hello 中所示，將會傳回 hello 回應標頭中的 hello URI hello 結果：</span><span class="sxs-lookup"><span data-stu-id="f108b-131">Since this operation is long running, hello URI for querying hello operation and hello URI for hello result is returned in hello response header as shown in hello following response:</span></span>

<span data-ttu-id="f108b-132">**重要的值**</span><span class="sxs-lookup"><span data-stu-id="f108b-132">**Important Values**</span></span>

* <span data-ttu-id="f108b-133">**Azure AsyncOperation** -這個屬性包含 hello URI tooquery hello 非同步疑難排解作業</span><span class="sxs-lookup"><span data-stu-id="f108b-133">**Azure-AsyncOperation** - This property contains hello URI tooquery hello Async troubleshoot operation</span></span>
* <span data-ttu-id="f108b-134">**位置**-這個屬性包含 hello hello 結果的所在當 hello 作業已完成的 URI</span><span class="sxs-lookup"><span data-stu-id="f108b-134">**Location** - This property contains hello URI where hello results are when hello operation is complete</span></span>

```
HTTP/1.1 202 Accepted
Pragma: no-cache
Retry-After: 10
x-ms-request-id: 8a1167b7-6768-4ac1-85dc-703c9c9b9247
Azure-AsyncOperation: https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operations/8a1167b7-6768-4ac1-85dc-703c9c9b9247?api-version=2016-03-30
Strict-Transport-Security: max-age=31536000; includeSubDomains
Cache-Control: no-cache
Location: https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operationResults/8a1167b7-6768-4ac1-85dc-703c9c9b9247?api-version=2016-03-30
Server: Microsoft-HTTPAPI/2.0; Microsoft-HTTPAPI/2.0
x-ms-ratelimit-remaining-subscription-writes: 1199
x-ms-correlation-request-id: 4364d88a-bd08-422c-a716-dbb0cdc99f7b
x-ms-routing-request-id: NORTHCENTRALUS:20170112T183202Z:4364d88a-bd08-422c-a716-dbb0cdc99f7b
Date: Thu, 12 Jan 2017 18:32:01 GMT

null
```

### <a name="query-hello-async-operation-for-completion"></a><span data-ttu-id="f108b-135">查詢 hello 非同步作業完成</span><span class="sxs-lookup"><span data-stu-id="f108b-135">Query hello async operation for completion</span></span>

<span data-ttu-id="f108b-136">使用 hello 作業 URI tooquery hello 作業進度的 hello hello 下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="f108b-136">Use hello operations URI tooquery for hello progress of hello operation as seen in hello following example:</span></span>

```powershell
armclient get "https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operations/8a1167b7-6768-4ac1-85dc-703c9c9b9247?api-version=2016-03-30"
```

<span data-ttu-id="f108b-137">Hello 作業正在進行中，雖然 hello 回應顯示**InProgress** hello 下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="f108b-137">While hello operation is in progress, hello response shows **InProgress** as seen in hello following example:</span></span>

```json
{
  "status": "InProgress"
}
```

<span data-ttu-id="f108b-138">當 hello 作業已完成的 hello 狀態變更太**Succeeded**。</span><span class="sxs-lookup"><span data-stu-id="f108b-138">When hello operation is complete hello status changes too**Succeeded**.</span></span>

```json
{
  "status": "Succeeded"
}
```

### <a name="retrieve-hello-results"></a><span data-ttu-id="f108b-139">擷取 hello 結果</span><span class="sxs-lookup"><span data-stu-id="f108b-139">Retrieve hello results</span></span>

<span data-ttu-id="f108b-140">一旦傳回 hello 狀態是**Succeeded**，取得上呼叫方法 hello operationResult URI tooretrieve hello 結果。</span><span class="sxs-lookup"><span data-stu-id="f108b-140">Once hello status returned is **Succeeded**, call a GET Method on hello operationResult URI tooretrieve hello results.</span></span>

```powershell
armclient get "https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operationResults/8a1167b7-6768-4ac1-85dc-703c9c9b9247?api-version=2016-03-30"
```

<span data-ttu-id="f108b-141">hello 下列回應是一般的降低回應查詢的閘道進行疑難排解的 hello 結果時，傳回的範例。</span><span class="sxs-lookup"><span data-stu-id="f108b-141">hello following responses are examples of a typical degraded response returned when querying hello results of troubleshooting a gateway.</span></span> <span data-ttu-id="f108b-142">請參閱[了解 hello 結果](#understanding-the-results)tooget 釐清哪些 hello 回應平均值中的 hello 屬性。</span><span class="sxs-lookup"><span data-stu-id="f108b-142">See [Understanding hello results](#understanding-the-results) tooget clarification on what hello properties in hello response mean.</span></span>

```json
{
  "startTime": "2017-01-12T10:31:41.562646-08:00",
  "endTime": "2017-01-12T18:31:48.677Z",
  "code": "Degraded",
  "results": [
    {
      "id": "PlatformInActive",
      "summary": "We are sorry, your VPN gateway is in standby mode",
      "detail": "During this time hello gateway will not initiate or accept VPN connections with on premises VPN devices or other Azure VPN Gateways. This is a transient state while hello Azure platform is being updated.",
      "recommendedActions": [
        {
          "actionText": "If hello condition persists, please try resetting your Azure VPN gateway",
          "actionUri": "https://azure.microsoft.com/en-us/documentation/articles/vpn-gateway-resetgw-classic/",
          "actionUriText": "resetting hello VPN Gateway"
        },
        {
          "actionText": "If your VPN gateway isn't up and running by hello expected resolution time, contact support",
          "actionUri": "http://azure.microsoft.com/support",
          "actionUriText": "contact support"
        }
      ]
    },
    {
      "id": "NoFault",
      "summary": "This VPN gateway is running normally",
      "detail": "There aren't any known Azure platform problems affecting this VPN Connection",
      "recommendedActions": [
        {
          "actionText": "If you are still experience problems with hello VPN gateway, please try resetting hello VPN gateway.",
          "actionUri": "https://azure.microsoft.com/en-us/documentation/articles/vpn-gateway-resetgw-classic/",
          "actionUriText": "resetting VPN gateway"
        },
        {
          "actionText": "If you are experiencing problems you believe are caused by Azure, contact support",
          "actionUri": "http://azure.microsoft.com/support",
          "actionUriText": "contact support"
        }
      ]
    }
  ]
}
```


## <a name="troubleshoot-connections"></a><span data-ttu-id="f108b-143">針對連線進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="f108b-143">Troubleshoot Connections</span></span>

<span data-ttu-id="f108b-144">下列範例查詢 hello 的連接狀態而 hello。</span><span class="sxs-lookup"><span data-stu-id="f108b-144">hello following example queries hello status of a Connection.</span></span>

```powershell

$subscriptionId = "00000000-0000-0000-0000-000000000000"
$resourceGroupName = "ContosoRG"
$NWresourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$connectionName = "VNET2toVNET1Connection"
$storageAccountName = "contososa"
$containerName = "gwlogs"
$requestBody = @{
"TargetResourceId": "/subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/Microsoft.Network/connections/${connectionName}",
"Properties": {
"StorageId": "/subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/Microsoft.Storage/storageAccounts/${storageAccountName}",
"StoragePath": "https://${storageAccountName}.blob.core.windows.net/${containerName}"
}

}
armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${NWresourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/troubleshoot?api-version=2016-03-30 "
```

> [!NOTE]
> <span data-ttu-id="f108b-145">hello 疑難排解作業無法在連線和其相對應的閘道中以平行方式執行。</span><span class="sxs-lookup"><span data-stu-id="f108b-145">hello troubleshoot operation cannot be run in parallel on a Connection and its corresponding gateways.</span></span> <span data-ttu-id="f108b-146">hello 作業必須完成先前 toorunning 它 hello 先前的資源上。</span><span class="sxs-lookup"><span data-stu-id="f108b-146">hello operation must complete prior toorunning it on hello previous resource.</span></span>

<span data-ttu-id="f108b-147">由於這是長時間執行的交易，在 hello 回應標頭，hello URI 的查詢 hello 作業和 hello 結果 hello URI 會傳回下列回應 hello 中所示：</span><span class="sxs-lookup"><span data-stu-id="f108b-147">Since this is a long running transaction, in hello response header, hello URI for querying hello operation and hello URI for hello result is returned as shown in hello following response:</span></span>

<span data-ttu-id="f108b-148">**重要的值**</span><span class="sxs-lookup"><span data-stu-id="f108b-148">**Important Values**</span></span>

* <span data-ttu-id="f108b-149">**Azure AsyncOperation** -這個屬性包含 hello URI tooquery hello 非同步疑難排解作業</span><span class="sxs-lookup"><span data-stu-id="f108b-149">**Azure-AsyncOperation** - This property contains hello URI tooquery hello Async troubleshoot operation</span></span>
* <span data-ttu-id="f108b-150">**位置**-這個屬性包含 hello hello 結果的所在當 hello 作業已完成的 URI</span><span class="sxs-lookup"><span data-stu-id="f108b-150">**Location** - This property contains hello URI where hello results are when hello operation is complete</span></span>

```
HTTP/1.1 202 Accepted
Pragma: no-cache
Retry-After: 10
x-ms-request-id: 8a1167b7-6768-4ac1-85dc-703c9c9b9247
Azure-AsyncOperation: https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operations/8a1167b7-6768-4ac1-85dc-703c9c9b9247?api-version=2016-03-30
Strict-Transport-Security: max-age=31536000; includeSubDomains
Cache-Control: no-cache
Location: https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operationResults/8a1167b7-6768-4ac1-85dc-703c9c9b9247?api-version=2016-03-30
Server: Microsoft-HTTPAPI/2.0; Microsoft-HTTPAPI/2.0
x-ms-ratelimit-remaining-subscription-writes: 1199
x-ms-correlation-request-id: 4364d88a-bd08-422c-a716-dbb0cdc99f7b
x-ms-routing-request-id: NORTHCENTRALUS:20170112T183202Z:4364d88a-bd08-422c-a716-dbb0cdc99f7b
Date: Thu, 12 Jan 2017 18:32:01 GMT

null
```

### <a name="query-hello-async-operation-for-completion"></a><span data-ttu-id="f108b-151">查詢 hello 非同步作業完成</span><span class="sxs-lookup"><span data-stu-id="f108b-151">Query hello async operation for completion</span></span>

<span data-ttu-id="f108b-152">使用 hello 作業 URI tooquery hello 作業進度的 hello hello 下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="f108b-152">Use hello operations URI tooquery for hello progress of hello operation as seen in hello following example:</span></span>

```powershell
armclient get "https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operations/843b1c31-4717-4fdd-b7a6-4c786ca9c501?api-version=2016-03-30"
```

<span data-ttu-id="f108b-153">Hello 作業正在進行中，雖然 hello 回應顯示**InProgress** hello 下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="f108b-153">While hello operation is in progress, hello response shows **InProgress** as seen in hello following example:</span></span>

```json
{
  "status": "InProgress"
}
```

<span data-ttu-id="f108b-154">Hello 狀態 hello 作業完成時，變更太**Succeeded**。</span><span class="sxs-lookup"><span data-stu-id="f108b-154">When hello operation is complete, hello status changes too**Succeeded**.</span></span>

```json
{
  "status": "Succeeded"
}
```

<span data-ttu-id="f108b-155">hello 下列回應是回應的一般查詢的疑難排解連線的 hello 結果時，傳回的範例。</span><span class="sxs-lookup"><span data-stu-id="f108b-155">hello following responses are examples of a typical response returned when querying hello results of troubleshooting a Connection.</span></span>

### <a name="retrieve-hello-results"></a><span data-ttu-id="f108b-156">擷取 hello 結果</span><span class="sxs-lookup"><span data-stu-id="f108b-156">Retrieve hello results</span></span>

<span data-ttu-id="f108b-157">一旦傳回 hello 狀態是**Succeeded**，取得上呼叫方法 hello operationResult URI tooretrieve hello 結果。</span><span class="sxs-lookup"><span data-stu-id="f108b-157">Once hello status returned is **Succeeded**, call a GET Method on hello operationResult URI tooretrieve hello results.</span></span>

```powershell
armclient get "https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operationResults/843b1c31-4717-4fdd-b7a6-4c786ca9c501?api-version=2016-03-30"
```

<span data-ttu-id="f108b-158">hello 下列回應是回應的一般查詢的疑難排解連線的 hello 結果時，傳回的範例。</span><span class="sxs-lookup"><span data-stu-id="f108b-158">hello following responses are examples of a typical response returned when querying hello results of troubleshooting a Connection.</span></span>

```json
{
  "startTime": "2017-01-12T14:09:19.1215346-08:00",
  "endTime": "2017-01-12T22:09:23.747Z",
  "code": "UnHealthy",
  "results": [
    {
      "id": "PlatformInActive",
      "summary": "We are sorry, your VPN gateway is in standby mode",
      "detail": "During this time hello gateway will not initiate or accept VPN connections with on premises VPN devices or other Azure VPN Gateways. This 
is a transient state while hello Azure platform is being updated.",
      "recommendedActions": [
        {
          "actionText": "If hello condition persists, please try resetting your Azure VPN gateway",
          "actionUri": "https://azure.microsoft.com/en-us/documentation/articles/vpn-gateway-resetgw-classic/",
          "actionUriText": "resetting hello VPN gateway"
        },
        {
          "actionText": "If your VPN Connection isn't up and running by hello expected resolution time, contact support",
          "actionUri": "http://azure.microsoft.com/support",
          "actionUriText": "contact support"
        }
      ]
    },
    {
      "id": "NoFault",
      "summary": "This VPN Connection is running normally",
      "detail": "There aren't any known Azure platform problems affecting this VPN Connection",
      "recommendedActions": [
        {
          "actionText": "If you are still experience problems with hello VPN gateway, please try resetting hello VPN gateway.",
          "actionUri": "https://azure.microsoft.com/en-us/documentation/articles/vpn-gateway-resetgw-classic/",
          "actionUriText": "resetting VPN gateway"
        },
        {
          "actionText": "If you are experiencing problems you believe are caused by Azure, contact support",
          "actionUri": "http://azure.microsoft.com/support",
          "actionUriText": "contact support"
        }
      ]
    }
  ]
}
```

## <a name="understanding-hello-results"></a><span data-ttu-id="f108b-159">了解 hello 結果</span><span class="sxs-lookup"><span data-stu-id="f108b-159">Understanding hello results</span></span>

<span data-ttu-id="f108b-160">動作的 hello 文字上 tooresolve hello 問題的方式，提供一般指引。</span><span class="sxs-lookup"><span data-stu-id="f108b-160">hello action text provides general guidance on how tooresolve hello issue.</span></span> <span data-ttu-id="f108b-161">Hello 問題，可以採取的動作，如果是其他指南提供的連結。</span><span class="sxs-lookup"><span data-stu-id="f108b-161">If an action can be taken for hello issue, a link is provided with additional guidance.</span></span> <span data-ttu-id="f108b-162">Hello 案例中的任何其他指引，hello 回應提供 hello url tooopen 支援案例。</span><span class="sxs-lookup"><span data-stu-id="f108b-162">In hello case where there is no additional guidance, hello response provides hello url tooopen a support case.</span></span>  <span data-ttu-id="f108b-163">如需回應 hello 和時要包含的 hello 屬性的詳細資訊，請瀏覽[網路監看員疑難排解概觀](network-watcher-troubleshoot-overview.md)</span><span class="sxs-lookup"><span data-stu-id="f108b-163">For more information about hello properties of hello response and what is included, visit [Network Watcher Troubleshoot overview](network-watcher-troubleshoot-overview.md)</span></span>

<span data-ttu-id="f108b-164">如需從 azure 儲存體帳戶下載檔案的指示，請參閱太[開始使用適用於.NET 的 Azure Blob 儲存體使用](../storage/blobs/storage-dotnet-how-to-use-blobs.md)。</span><span class="sxs-lookup"><span data-stu-id="f108b-164">For instructions on downloading files from azure storage accounts, refer too[Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="f108b-165">另一項可用工具為儲存體總管。</span><span class="sxs-lookup"><span data-stu-id="f108b-165">Another tool that can be used is Storage Explorer.</span></span> <span data-ttu-id="f108b-166">儲存體總管的詳細資訊可以在這裡找到在 hello 下列連結：[存放裝置總管](http://storageexplorer.com/)</span><span class="sxs-lookup"><span data-stu-id="f108b-166">More information about Storage Explorer can be found here at hello following link: [Storage Explorer](http://storageexplorer.com/)</span></span>

## <a name="next-steps"></a><span data-ttu-id="f108b-167">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f108b-167">Next steps</span></span>

<span data-ttu-id="f108b-168">如果設定已變更為該停止 VPN 連線能力，請參閱[管理網路安全性群組](../virtual-network/virtual-network-manage-nsg-arm-portal.md)tootrack 向 hello 網路安全性群組和安全性規則，可能會有問題。</span><span class="sxs-lookup"><span data-stu-id="f108b-168">If settings have been changed that stop VPN connectivity, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack down hello network security group and security rules that may be in question.</span></span>
