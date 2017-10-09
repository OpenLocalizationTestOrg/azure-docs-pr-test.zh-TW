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
# <a name="troubleshoot-virtual-network-gateway-and-connections-using-azure-network-watcher"></a>使用 Azure 網路監看員來針對虛擬網路閘道和連線進行疑難排解

> [!div class="op_single_selector"]
> - [入口網站](network-watcher-troubleshoot-manage-portal.md)
> - [PowerShell](network-watcher-troubleshoot-manage-powershell.md)
> - [CLI 1.0](network-watcher-troubleshoot-manage-cli-nodejs.md)
> - [CLI 2.0](network-watcher-troubleshoot-manage-cli.md)
> - [REST API](network-watcher-troubleshoot-manage-rest.md)

網路監看員會提供許多功能與 toounderstanding 您在 Azure 中的網路資源。 這些功能的其中之一便是資源疑難排解。 疑難排解資源可以透過 hello 入口網站、 PowerShell、 CLI 或 REST API 呼叫。 呼叫時，網路監看員會檢查 hello 的虛擬網路閘道或連線的健全狀況，並傳回其發現。

這篇文章會帶領您完成疑難排解資源的目前可用的 hello 不同的管理工作。

- [針對虛擬網路閘道進行疑難排解](#troubleshoot-a-virtual-network-gateway)
- [針對連線進行疑難排解](#troubleshoot-connections)

## <a name="before-you-begin"></a>開始之前

ARMclient 是使用 PowerShell 的使用的 toocall hello REST API。 您可以在 chocolatey 的 [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient) 上找到 ARMClient

此案例假設您已依照中的 hello 步驟[建立網路監看員](network-watcher-create.md)toocreate 網路監看員。

如需支援的閘道類型清單，請瀏覽[支援的閘道類型](network-watcher-troubleshoot-overview.md#supported-gateway-types)。

## <a name="overview"></a>概觀

網路監看員疑難排解提供 hello 功能的虛擬網路閘道與連線發生問題進行疑難排解。 Toohello 資源提出的要求時疑難排解記錄檔要查詢及檢查。 檢查完成時，會傳回 hello 結果。 hello 疑難排解應用程式開發介面要求是長時間執行的要求，這可能需要多個分鐘 tooreturn 結果。 記錄會儲存在儲存體帳戶的容器中。

## <a name="log-in-with-armclient"></a>使用 ARMClient 登入

```PowerShell
armclient login
```

## <a name="troubleshoot-a-virtual-network-gateway"></a>針對虛擬網路閘道進行疑難排解


### <a name="post-hello-troubleshoot-request"></a>POST hello 疑難排解要求

下列範例查詢 hello 狀態的虛擬網路閘道的 hello。

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

由於這項作業是長時間執行，hello URI 查詢 hello 作業，且下列回應 hello 中所示，將會傳回 hello 回應標頭中的 hello URI hello 結果：

**重要的值**

* **Azure AsyncOperation** -這個屬性包含 hello URI tooquery hello 非同步疑難排解作業
* **位置**-這個屬性包含 hello hello 結果的所在當 hello 作業已完成的 URI

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

### <a name="query-hello-async-operation-for-completion"></a>查詢 hello 非同步作業完成

使用 hello 作業 URI tooquery hello 作業進度的 hello hello 下列範例所示：

```powershell
armclient get "https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operations/8a1167b7-6768-4ac1-85dc-703c9c9b9247?api-version=2016-03-30"
```

Hello 作業正在進行中，雖然 hello 回應顯示**InProgress** hello 下列範例所示：

```json
{
  "status": "InProgress"
}
```

當 hello 作業已完成的 hello 狀態變更太**Succeeded**。

```json
{
  "status": "Succeeded"
}
```

### <a name="retrieve-hello-results"></a>擷取 hello 結果

一旦傳回 hello 狀態是**Succeeded**，取得上呼叫方法 hello operationResult URI tooretrieve hello 結果。

```powershell
armclient get "https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operationResults/8a1167b7-6768-4ac1-85dc-703c9c9b9247?api-version=2016-03-30"
```

hello 下列回應是一般的降低回應查詢的閘道進行疑難排解的 hello 結果時，傳回的範例。 請參閱[了解 hello 結果](#understanding-the-results)tooget 釐清哪些 hello 回應平均值中的 hello 屬性。

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


## <a name="troubleshoot-connections"></a>針對連線進行疑難排解

下列範例查詢 hello 的連接狀態而 hello。

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
> hello 疑難排解作業無法在連線和其相對應的閘道中以平行方式執行。 hello 作業必須完成先前 toorunning 它 hello 先前的資源上。

由於這是長時間執行的交易，在 hello 回應標頭，hello URI 的查詢 hello 作業和 hello 結果 hello URI 會傳回下列回應 hello 中所示：

**重要的值**

* **Azure AsyncOperation** -這個屬性包含 hello URI tooquery hello 非同步疑難排解作業
* **位置**-這個屬性包含 hello hello 結果的所在當 hello 作業已完成的 URI

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

### <a name="query-hello-async-operation-for-completion"></a>查詢 hello 非同步作業完成

使用 hello 作業 URI tooquery hello 作業進度的 hello hello 下列範例所示：

```powershell
armclient get "https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operations/843b1c31-4717-4fdd-b7a6-4c786ca9c501?api-version=2016-03-30"
```

Hello 作業正在進行中，雖然 hello 回應顯示**InProgress** hello 下列範例所示：

```json
{
  "status": "InProgress"
}
```

Hello 狀態 hello 作業完成時，變更太**Succeeded**。

```json
{
  "status": "Succeeded"
}
```

hello 下列回應是回應的一般查詢的疑難排解連線的 hello 結果時，傳回的範例。

### <a name="retrieve-hello-results"></a>擷取 hello 結果

一旦傳回 hello 狀態是**Succeeded**，取得上呼叫方法 hello operationResult URI tooretrieve hello 結果。

```powershell
armclient get "https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operationResults/843b1c31-4717-4fdd-b7a6-4c786ca9c501?api-version=2016-03-30"
```

hello 下列回應是回應的一般查詢的疑難排解連線的 hello 結果時，傳回的範例。

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

## <a name="understanding-hello-results"></a>了解 hello 結果

動作的 hello 文字上 tooresolve hello 問題的方式，提供一般指引。 Hello 問題，可以採取的動作，如果是其他指南提供的連結。 Hello 案例中的任何其他指引，hello 回應提供 hello url tooopen 支援案例。  如需回應 hello 和時要包含的 hello 屬性的詳細資訊，請瀏覽[網路監看員疑難排解概觀](network-watcher-troubleshoot-overview.md)

如需從 azure 儲存體帳戶下載檔案的指示，請參閱太[開始使用適用於.NET 的 Azure Blob 儲存體使用](../storage/blobs/storage-dotnet-how-to-use-blobs.md)。 另一項可用工具為儲存體總管。 儲存體總管的詳細資訊可以在這裡找到在 hello 下列連結：[存放裝置總管](http://storageexplorer.com/)

## <a name="next-steps"></a>後續步驟

如果設定已變更為該停止 VPN 連線能力，請參閱[管理網路安全性群組](../virtual-network/virtual-network-manage-nsg-arm-portal.md)tootrack 向 hello 網路安全性群組和安全性規則，可能會有問題。
