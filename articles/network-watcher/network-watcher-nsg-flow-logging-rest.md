---
title: "使用 Azure 網路監看員的 REST API 記錄 aaaManage 網路安全性小組流程 |Microsoft 文件"
description: "此頁面說明 toomanage 網路安全性小組流程中使用 REST API 的 Azure 網路監看員的記錄檔"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 2ab25379-0fd3-4bfe-9d82-425dfc7ad6bb
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: be81e35f4d01c67efef99773e9b4e2ae4b8e209e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-network-security-group-flow-logs-using-rest-api"></a>使用 REST API 設定網路安全性群組流量記錄

> [!div class="op_single_selector"]
> - [Azure 入口網站](network-watcher-nsg-flow-logging-portal.md)
> - [PowerShell](network-watcher-nsg-flow-logging-powershell.md)
> - [CLI 1.0](network-watcher-nsg-flow-logging-cli-nodejs.md)
> - [CLI 2.0](network-watcher-nsg-flow-logging-cli.md)
> - [REST API](network-watcher-nsg-flow-logging-rest.md)

網路安全性小組流程記錄檔是 tooview ingress 和 egress IP 流量，透過網路安全性群組相關的資訊可讓您的網路監看員的功能。 這些流程記錄檔會寫入以 json 格式，並顯示輸出和輸入每個規則為基礎的流量，hello NIC hello 流程適用於，5 個 tuple hello 流程 （來源/目的地 IP，來源/目的地連接埠通訊協定） 的資訊，並允許流量，如果 hello 或被拒絕。

## <a name="before-you-begin"></a>開始之前

ARMclient 是使用 PowerShell 的使用的 toocall hello REST API。 您可以在 chocolatey 的 [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient) 上找到 ARMClient

此案例假設您已依照中的 hello 步驟[建立網路監看員](network-watcher-create.md)toocreate 網路監看員。

> [!Important]
> 網路監看員 REST api 呼叫 hello hello 要求 URI 是 hello 包含 hello 網路監看員，您執行的 hello 診斷動作不 hello 資源的資源群組中的資源群組名稱。

## <a name="scenario"></a>案例

涵蓋在本文中的 hello 案例顯示如何 tooenable、 停用及查詢的流程使用 hello REST API 的記錄檔。 請瀏覽更多關於網路安全性群組流程 loggings，toolearn[網路安全性小組流程記錄概觀](network-watcher-nsg-flow-logging-overview.md)。

在此案例中，您將會：

* 啟用流程記錄
* 停用流程記錄
* 查詢流量記錄狀態

## <a name="log-in-with-armclient"></a>使用 ARMClient 登入

登入 tooarmclient 與您的 Azure 認證。

```PowerShell
armclient login
```

## <a name="register-insights-provider"></a>註冊 Insights 提供者

為了讓流量記錄 toowork 成功，hello **Microsoft.Insights**必須註冊提供者。 如果您不確定是否 hello **Microsoft.Insights**提供者是已註冊，請執行的 hello 下列指令碼。

```powershell
$subscriptionId = "00000000-0000-0000-0000-000000000000"
armclient post "https://management.azure.com//subscriptions/${subscriptionId}/providers/Microsoft.Insights/register?api-version=2016-09-01"
```

## <a name="enable-network-security-group-flow-logs"></a>啟用網路安全性群組流量記錄

hello 命令 tooenable 流程記錄檔以 hello 下列範例所示：

```powershell
$subscriptionId = "00000000-0000-0000-0000-000000000000"
$targetUri = "" # example /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName/providers/Microsoft.Network/networkSecurityGroups/{nsgName}"
$storageId = "/subscriptions/00000000-0000-0000-0000-000000000000/{resourceGroupName/providers/Microsoft.Storage/storageAccounts/{saName}"
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$requestBody = @"
{
    'targetResourceId': '${targetUri}',
    'properties': {
    'storageId': '${storageId}',
    'enabled': 'true',
    'retentionPolicy' : {
            days: 5,
            enabled: true
        }
    }
}
"@

armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/configureFlowLog?api-version=2016-12-01" $requestBody
```

hello 從傳回的回應 hello 上述範例是，如下所示：

```json
{
  "targetResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkSecurityGroups/{nsgName}",
  "properties": {
    "storageId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{saName}",
    "enabled": true,
    "retentionPolicy": {
      "days": 5,
      "enabled": true
    }
  }
}
```

## <a name="disable-network-security-group-flow-logs"></a>停用網路安全性群組流量記錄

下列範例 toodisable 流量使用 hello 記錄。 hello 呼叫是相同 hello 與啟用流程記錄檔中，除了**false** hello 啟用屬性設定。

```powershell
$subscriptionId = "00000000-0000-0000-0000-000000000000"
$targetUri = "" # example /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName/providers/Microsoft.Network/networkSecurityGroups/{nsgName}"
$storageId = "/subscriptions/00000000-0000-0000-0000-000000000000/{resourceGroupName/providers/Microsoft.Storage/storageAccounts/{saName}"
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$requestBody = @"
{
    'targetResourceId': '${targetUri}',
    'properties': {
    'storageId': '${storageId}',
    'enabled': 'false',
    'retentionPolicy' : {
            days: 5,
            enabled: true
        }
    }
}
"@

armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/configureFlowLog?api-version=2016-12-01" $requestBody
```

hello 從傳回的回應 hello 上述範例是，如下所示：

```json
{
  "targetResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkSecurityGroups/{nsgName}",
  "properties": {
    "storageId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{saName}",
    "enabled": false,
    "retentionPolicy": {
      "days": 5,
      "enabled": true
    }
  }
}
```

## <a name="query-flow-logs"></a>查詢流量記錄

下列查詢 hello 流程的狀態 REST 呼叫的 hello 登入網路安全性群組。

```powershell
$subscriptionId = "00000000-0000-0000-0000-000000000000"
$targetUri = "" # example /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName/providers/Microsoft.Network/networkSecurityGroups/{nsgName}"
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$requestBody = @"
{
    'targetResourceId': '${targetUri}',
}
"@

armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/queryFlowLogStatus?api-version=2016-12-01" $requestBody
```

hello 以下是傳回的 hello 回應的範例：

```json
{
  "targetResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkSecurityGroups/{nsgName}",
  "properties": {
    "storageId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{saName}",
    "enabled": true,
   "retentionPolicy": {
      "days": 5,
      "enabled": true
    }
  }
}
```

## <a name="download-a-flow-log"></a>下載流量記錄

hello 流程記錄檔的儲存位置是在建立時定義。 這些非固定格式儲存的記錄檔 tooa 儲存體帳戶是 Microsoft Azure 儲存體總管 中，這可以在這裡下載方便的工具 tooaccess: http://storageexplorer.com/

如果指定的儲存體帳戶，則封包擷取檔案會儲存在下列位置的 hello tooa 儲存體帳戶：

```
https://{storageAccountName}.blob.core.windows.net/insights-logs-networksecuritygroupflowevent/resourceId%3D/subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/microsoft.network/networksecuritygroups/{nsgName}/{year}/{month}/{day}/PT1H.json
```

## <a name="next-steps"></a>後續步驟

了解如何太[視覺化與 PowerBI NSG 流程記錄](network-watcher-visualize-nsg-flow-logs-power-bi.md)

了解如何太[視覺化 NSG 流程記錄與開放原始碼工具](network-watcher-visualize-nsg-flow-logs-open-source-tools.md)
