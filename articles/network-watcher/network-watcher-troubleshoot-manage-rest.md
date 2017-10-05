---
title: "使用 Azure 網路監看員來針對虛擬網路閘道和連線進行疑難排解 - REST | Microsoft Docs"
description: "此頁面說明如何搭配使用 Azure 網路監看員和 REST，以針對虛擬網路閘道和連線進行疑難排解"
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
ms.openlocfilehash: bc61be74d85a309c158716460b918baaf4fa94dc
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="troubleshoot-virtual-network-gateway-and-connections-using-azure-network-watcher"></a><span data-ttu-id="026b8-103">使用 Azure 網路監看員來針對虛擬網路閘道和連線進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="026b8-103">Troubleshoot Virtual Network gateway and Connections using Azure Network Watcher</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="026b8-104">入口網站</span><span class="sxs-lookup"><span data-stu-id="026b8-104">Portal</span></span>](network-watcher-troubleshoot-manage-portal.md)
> - [<span data-ttu-id="026b8-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="026b8-105">PowerShell</span></span>](network-watcher-troubleshoot-manage-powershell.md)
> - [<span data-ttu-id="026b8-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="026b8-106">CLI 1.0</span></span>](network-watcher-troubleshoot-manage-cli-nodejs.md)
> - [<span data-ttu-id="026b8-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="026b8-107">CLI 2.0</span></span>](network-watcher-troubleshoot-manage-cli.md)
> - [<span data-ttu-id="026b8-108">REST API</span><span class="sxs-lookup"><span data-stu-id="026b8-108">REST API</span></span>](network-watcher-troubleshoot-manage-rest.md)

<span data-ttu-id="026b8-109">網路監看員提供了許多功能，因為它的作用就是為了讓您了解您在 Azure 中的網路資源。</span><span class="sxs-lookup"><span data-stu-id="026b8-109">Network Watcher provides many capabilities as it relates to understanding your network resources in Azure.</span></span> <span data-ttu-id="026b8-110">這些功能的其中之一便是資源疑難排解。</span><span class="sxs-lookup"><span data-stu-id="026b8-110">One of these capabilities is resource troubleshooting.</span></span> <span data-ttu-id="026b8-111">您可以透過入口網站、PowerShell、CLI 或 REST API 呼叫資源疑難排解。</span><span class="sxs-lookup"><span data-stu-id="026b8-111">Resource troubleshooting can be called through the portal, PowerShell, CLI, or REST API.</span></span> <span data-ttu-id="026b8-112">一經呼叫，網路監看員就會檢查虛擬網路閘道或連線的健全狀況，並傳回其調查結果。</span><span class="sxs-lookup"><span data-stu-id="026b8-112">When called, Network Watcher inspects the health of a Virtual Network Gateway or a Connection and returns its findings.</span></span>

<span data-ttu-id="026b8-113">本文會帶領您逐步完成資源疑難排解目前可用的不同管理工作。</span><span class="sxs-lookup"><span data-stu-id="026b8-113">This article takes you through the different management tasks that are currently available for resource troubleshooting.</span></span>

- [<span data-ttu-id="026b8-114">針對虛擬網路閘道進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="026b8-114">**Troubleshoot a Virtual Network gateway**</span></span>](#troubleshoot-a-virtual-network-gateway)
- [<span data-ttu-id="026b8-115">針對連線進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="026b8-115">**Troubleshoot a Connection**</span></span>](#troubleshoot-connections)

## <a name="before-you-begin"></a><span data-ttu-id="026b8-116">開始之前</span><span class="sxs-lookup"><span data-stu-id="026b8-116">Before you begin</span></span>

<span data-ttu-id="026b8-117">使用 ARMclient 透過 PowerShell 呼叫 REST API。</span><span class="sxs-lookup"><span data-stu-id="026b8-117">ARMclient is used to call the REST API using PowerShell.</span></span> <span data-ttu-id="026b8-118">您可以在 chocolatey 的 [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient) 上找到 ARMClient</span><span class="sxs-lookup"><span data-stu-id="026b8-118">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient)</span></span>

<span data-ttu-id="026b8-119">此案例假設您已依照[建立網路監看員](network-watcher-create.md)中的步驟建立網路監看員。</span><span class="sxs-lookup"><span data-stu-id="026b8-119">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span>

<span data-ttu-id="026b8-120">如需支援的閘道類型清單，請瀏覽[支援的閘道類型](network-watcher-troubleshoot-overview.md#supported-gateway-types)。</span><span class="sxs-lookup"><span data-stu-id="026b8-120">For a list of supported gateway types visit, [Supported Gateway types](network-watcher-troubleshoot-overview.md#supported-gateway-types).</span></span>

## <a name="overview"></a><span data-ttu-id="026b8-121">概觀</span><span class="sxs-lookup"><span data-stu-id="026b8-121">Overview</span></span>

<span data-ttu-id="026b8-122">網路監看員疑難排解可讓您針對虛擬網路閘道和連線所發生的問題進行疑難排解。</span><span class="sxs-lookup"><span data-stu-id="026b8-122">Network Watcher troubleshooting provides the ability troubleshoot issues that arise with Virtual Network gateways and Connections.</span></span> <span data-ttu-id="026b8-123">要求進行資源疑難排解時會查詢並檢查記錄。</span><span class="sxs-lookup"><span data-stu-id="026b8-123">When a request is made to the resource troubleshooting, logs are querying and inspected.</span></span> <span data-ttu-id="026b8-124">檢查完成時，就會傳回結果。</span><span class="sxs-lookup"><span data-stu-id="026b8-124">When inspection is complete, the results are returned.</span></span> <span data-ttu-id="026b8-125">疑難排解 API 要求是執行時間很長的要求，可能需要幾分鐘的時間才會傳回結果。</span><span class="sxs-lookup"><span data-stu-id="026b8-125">The troubleshoot API requests are long running requests, which could take multiple minutes to return a result.</span></span> <span data-ttu-id="026b8-126">記錄會儲存在儲存體帳戶的容器中。</span><span class="sxs-lookup"><span data-stu-id="026b8-126">Logs are stored in a container on a storage account.</span></span>

## <a name="log-in-with-armclient"></a><span data-ttu-id="026b8-127">使用 ARMClient 登入</span><span class="sxs-lookup"><span data-stu-id="026b8-127">Log in with ARMClient</span></span>

```PowerShell
armclient login
```

## <a name="troubleshoot-a-virtual-network-gateway"></a><span data-ttu-id="026b8-128">針對虛擬網路閘道進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="026b8-128">Troubleshoot a Virtual Network gateway</span></span>


### <a name="post-the-troubleshoot-request"></a><span data-ttu-id="026b8-129">POST 疑難排解要求</span><span class="sxs-lookup"><span data-stu-id="026b8-129">POST the troubleshoot request</span></span>

<span data-ttu-id="026b8-130">下列範例會查詢虛擬網路閘道的狀態。</span><span class="sxs-lookup"><span data-stu-id="026b8-130">The following example queries the status of a Virtual Network gateway.</span></span>

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

<span data-ttu-id="026b8-131">由於這項作業的執行時間很長，回應標頭中會傳回用於查詢作業的 URI 和結果的 URI，如下列回應所示：</span><span class="sxs-lookup"><span data-stu-id="026b8-131">Since this operation is long running, the URI for querying the operation and the URI for the result is returned in the response header as shown in the following response:</span></span>

<span data-ttu-id="026b8-132">**重要的值**</span><span class="sxs-lookup"><span data-stu-id="026b8-132">**Important Values**</span></span>

* <span data-ttu-id="026b8-133">**Azure AsyncOperation** - 此屬性包含用來查詢非同步疑難排解作業的 URI</span><span class="sxs-lookup"><span data-stu-id="026b8-133">**Azure-AsyncOperation** - This property contains the URI to query the Async troubleshoot operation</span></span>
* <span data-ttu-id="026b8-134">**Location** - 此屬性包含作業完成時結果所在的 URI</span><span class="sxs-lookup"><span data-stu-id="026b8-134">**Location** - This property contains the URI where the results are when the operation is complete</span></span>

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

### <a name="query-the-async-operation-for-completion"></a><span data-ttu-id="026b8-135">查詢非同步作業是否完成</span><span class="sxs-lookup"><span data-stu-id="026b8-135">Query the async operation for completion</span></span>

<span data-ttu-id="026b8-136">使用作業 URI 來查詢作業的進度，如下列範例所示︰</span><span class="sxs-lookup"><span data-stu-id="026b8-136">Use the operations URI to query for the progress of the operation as seen in the following example:</span></span>

```powershell
armclient get "https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operations/8a1167b7-6768-4ac1-85dc-703c9c9b9247?api-version=2016-03-30"
```

<span data-ttu-id="026b8-137">當作業正在進行時，回應會顯示 **InProgress**，如下列範例所示︰</span><span class="sxs-lookup"><span data-stu-id="026b8-137">While the operation is in progress, the response shows **InProgress** as seen in the following example:</span></span>

```json
{
  "status": "InProgress"
}
```

<span data-ttu-id="026b8-138">作業完成時，狀態會變更為 **Succeeded**。</span><span class="sxs-lookup"><span data-stu-id="026b8-138">When the operation is complete the status changes to **Succeeded**.</span></span>

```json
{
  "status": "Succeeded"
}
```

### <a name="retrieve-the-results"></a><span data-ttu-id="026b8-139">擷取結果</span><span class="sxs-lookup"><span data-stu-id="026b8-139">Retrieve the results</span></span>

<span data-ttu-id="026b8-140">一旦傳回的狀態是 **Succeeded**，請在 operationResult URI 上呼叫 GET 方法來擷取結果。</span><span class="sxs-lookup"><span data-stu-id="026b8-140">Once the status returned is **Succeeded**, call a GET Method on the operationResult URI to retrieve the results.</span></span>

```powershell
armclient get "https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operationResults/8a1167b7-6768-4ac1-85dc-703c9c9b9247?api-version=2016-03-30"
```

<span data-ttu-id="026b8-141">下列回應是查詢閘道疑難排解的結果時，通常會傳回的降級回應的範例。</span><span class="sxs-lookup"><span data-stu-id="026b8-141">The following responses are examples of a typical degraded response returned when querying the results of troubleshooting a gateway.</span></span> <span data-ttu-id="026b8-142">請參閱[了解結果](#understanding-the-results)，以釐清回應中的屬性代表什麼意思。</span><span class="sxs-lookup"><span data-stu-id="026b8-142">See [Understanding the results](#understanding-the-results) to get clarification on what the properties in the response mean.</span></span>

```json
{
  "startTime": "2017-01-12T10:31:41.562646-08:00",
  "endTime": "2017-01-12T18:31:48.677Z",
  "code": "Degraded",
  "results": [
    {
      "id": "PlatformInActive",
      "summary": "We are sorry, your VPN gateway is in standby mode",
      "detail": "During this time the gateway will not initiate or accept VPN connections with on premises VPN devices or other Azure VPN Gateways. This is a transient state while the Azure platform is being updated.",
      "recommendedActions": [
        {
          "actionText": "If the condition persists, please try resetting your Azure VPN gateway",
          "actionUri": "https://azure.microsoft.com/en-us/documentation/articles/vpn-gateway-resetgw-classic/",
          "actionUriText": "resetting the VPN Gateway"
        },
        {
          "actionText": "If your VPN gateway isn't up and running by the expected resolution time, contact support",
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
          "actionText": "If you are still experience problems with the VPN gateway, please try resetting the VPN gateway.",
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


## <a name="troubleshoot-connections"></a><span data-ttu-id="026b8-143">針對連線進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="026b8-143">Troubleshoot Connections</span></span>

<span data-ttu-id="026b8-144">下列範例會查詢連線的狀態。</span><span class="sxs-lookup"><span data-stu-id="026b8-144">The following example queries the status of a Connection.</span></span>

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
> <span data-ttu-id="026b8-145">無法同時針對連線和其相對應的閘道執行疑難排解作業。</span><span class="sxs-lookup"><span data-stu-id="026b8-145">The troubleshoot operation cannot be run in parallel on a Connection and its corresponding gateways.</span></span> <span data-ttu-id="026b8-146">作業必須完成，才能在先前的資源上執行。</span><span class="sxs-lookup"><span data-stu-id="026b8-146">The operation must complete prior to running it on the previous resource.</span></span>

<span data-ttu-id="026b8-147">由於這是長時間執行的交易，回應標頭中會傳回用於查詢作業的 URI 和結果的 URI，如下列回應所示：</span><span class="sxs-lookup"><span data-stu-id="026b8-147">Since this is a long running transaction, in the response header, the URI for querying the operation and the URI for the result is returned as shown in the following response:</span></span>

<span data-ttu-id="026b8-148">**重要的值**</span><span class="sxs-lookup"><span data-stu-id="026b8-148">**Important Values**</span></span>

* <span data-ttu-id="026b8-149">**Azure AsyncOperation** - 此屬性包含用來查詢非同步疑難排解作業的 URI</span><span class="sxs-lookup"><span data-stu-id="026b8-149">**Azure-AsyncOperation** - This property contains the URI to query the Async troubleshoot operation</span></span>
* <span data-ttu-id="026b8-150">**Location** - 此屬性包含作業完成時結果所在的 URI</span><span class="sxs-lookup"><span data-stu-id="026b8-150">**Location** - This property contains the URI where the results are when the operation is complete</span></span>

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

### <a name="query-the-async-operation-for-completion"></a><span data-ttu-id="026b8-151">查詢非同步作業是否完成</span><span class="sxs-lookup"><span data-stu-id="026b8-151">Query the async operation for completion</span></span>

<span data-ttu-id="026b8-152">使用作業 URI 來查詢作業的進度，如下列範例所示︰</span><span class="sxs-lookup"><span data-stu-id="026b8-152">Use the operations URI to query for the progress of the operation as seen in the following example:</span></span>

```powershell
armclient get "https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operations/843b1c31-4717-4fdd-b7a6-4c786ca9c501?api-version=2016-03-30"
```

<span data-ttu-id="026b8-153">當作業正在進行時，回應會顯示 **InProgress**，如下列範例所示︰</span><span class="sxs-lookup"><span data-stu-id="026b8-153">While the operation is in progress, the response shows **InProgress** as seen in the following example:</span></span>

```json
{
  "status": "InProgress"
}
```

<span data-ttu-id="026b8-154">作業完成時，狀態會變更為 **Succeeded**。</span><span class="sxs-lookup"><span data-stu-id="026b8-154">When the operation is complete, the status changes to **Succeeded**.</span></span>

```json
{
  "status": "Succeeded"
}
```

<span data-ttu-id="026b8-155">下列回應是查詢連線疑難排解的結果時，通常會傳回的回應範例。</span><span class="sxs-lookup"><span data-stu-id="026b8-155">The following responses are examples of a typical response returned when querying the results of troubleshooting a Connection.</span></span>

### <a name="retrieve-the-results"></a><span data-ttu-id="026b8-156">擷取結果</span><span class="sxs-lookup"><span data-stu-id="026b8-156">Retrieve the results</span></span>

<span data-ttu-id="026b8-157">一旦傳回的狀態是 **Succeeded**，請在 operationResult URI 上呼叫 GET 方法來擷取結果。</span><span class="sxs-lookup"><span data-stu-id="026b8-157">Once the status returned is **Succeeded**, call a GET Method on the operationResult URI to retrieve the results.</span></span>

```powershell
armclient get "https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operationResults/843b1c31-4717-4fdd-b7a6-4c786ca9c501?api-version=2016-03-30"
```

<span data-ttu-id="026b8-158">下列回應是查詢連線疑難排解的結果時，通常會傳回的回應範例。</span><span class="sxs-lookup"><span data-stu-id="026b8-158">The following responses are examples of a typical response returned when querying the results of troubleshooting a Connection.</span></span>

```json
{
  "startTime": "2017-01-12T14:09:19.1215346-08:00",
  "endTime": "2017-01-12T22:09:23.747Z",
  "code": "UnHealthy",
  "results": [
    {
      "id": "PlatformInActive",
      "summary": "We are sorry, your VPN gateway is in standby mode",
      "detail": "During this time the gateway will not initiate or accept VPN connections with on premises VPN devices or other Azure VPN Gateways. This 
is a transient state while the Azure platform is being updated.",
      "recommendedActions": [
        {
          "actionText": "If the condition persists, please try resetting your Azure VPN gateway",
          "actionUri": "https://azure.microsoft.com/en-us/documentation/articles/vpn-gateway-resetgw-classic/",
          "actionUriText": "resetting the VPN gateway"
        },
        {
          "actionText": "If your VPN Connection isn't up and running by the expected resolution time, contact support",
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
          "actionText": "If you are still experience problems with the VPN gateway, please try resetting the VPN gateway.",
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

## <a name="understanding-the-results"></a><span data-ttu-id="026b8-159">了解結果</span><span class="sxs-lookup"><span data-stu-id="026b8-159">Understanding the results</span></span>

<span data-ttu-id="026b8-160">動作文字會提供有關如何解決問題的一般指引。</span><span class="sxs-lookup"><span data-stu-id="026b8-160">The action text provides general guidance on how to resolve the issue.</span></span> <span data-ttu-id="026b8-161">如果問題有可行動作，則會提供附有其他指引的連結。</span><span class="sxs-lookup"><span data-stu-id="026b8-161">If an action can be taken for the issue, a link is provided with additional guidance.</span></span> <span data-ttu-id="026b8-162">如果沒有其他指引，回應中會提供 URL 以供您開啟支援案例。</span><span class="sxs-lookup"><span data-stu-id="026b8-162">In the case where there is no additional guidance, the response provides the url to open a support case.</span></span>  <span data-ttu-id="026b8-163">如需回應屬性和所含內容的詳細資訊，請瀏覽[網路監看員疑難排解概觀](network-watcher-troubleshoot-overview.md)</span><span class="sxs-lookup"><span data-stu-id="026b8-163">For more information about the properties of the response and what is included, visit [Network Watcher Troubleshoot overview](network-watcher-troubleshoot-overview.md)</span></span>

<span data-ttu-id="026b8-164">如需從 Azure 儲存體帳戶下載檔案的指示，請參閱[以 .NET 開始使用 Azure Blob 儲存體](../storage/blobs/storage-dotnet-how-to-use-blobs.md)。</span><span class="sxs-lookup"><span data-stu-id="026b8-164">For instructions on downloading files from azure storage accounts, refer to [Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="026b8-165">另一項可用工具為儲存體總管。</span><span class="sxs-lookup"><span data-stu-id="026b8-165">Another tool that can be used is Storage Explorer.</span></span> <span data-ttu-id="026b8-166">有關儲存體總管的詳細資訊可以在下列連結找到︰[儲存體總管](http://storageexplorer.com/)</span><span class="sxs-lookup"><span data-stu-id="026b8-166">More information about Storage Explorer can be found here at the following link: [Storage Explorer](http://storageexplorer.com/)</span></span>

## <a name="next-steps"></a><span data-ttu-id="026b8-167">後續步驟</span><span class="sxs-lookup"><span data-stu-id="026b8-167">Next steps</span></span>

<span data-ttu-id="026b8-168">如果設定已變更而停止了 VPN 連線，請參閱[管理網路安全性群組](../virtual-network/virtual-network-manage-nsg-arm-portal.md)以追蹤可能有問題的網路安全性群組和安全性規則。</span><span class="sxs-lookup"><span data-stu-id="026b8-168">If settings have been changed that stop VPN connectivity, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) to track down the network security group and security rules that may be in question.</span></span>
