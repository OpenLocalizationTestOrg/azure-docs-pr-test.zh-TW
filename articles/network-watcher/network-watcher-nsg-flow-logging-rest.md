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
# <a name="configuring-network-security-group-flow-logs-using-rest-api"></a><span data-ttu-id="7f936-103">使用 REST API 設定網路安全性群組流量記錄</span><span class="sxs-lookup"><span data-stu-id="7f936-103">Configuring Network Security Group flow logs using REST API</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="7f936-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="7f936-104">Azure portal</span></span>](network-watcher-nsg-flow-logging-portal.md)
> - [<span data-ttu-id="7f936-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="7f936-105">PowerShell</span></span>](network-watcher-nsg-flow-logging-powershell.md)
> - [<span data-ttu-id="7f936-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="7f936-106">CLI 1.0</span></span>](network-watcher-nsg-flow-logging-cli-nodejs.md)
> - [<span data-ttu-id="7f936-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="7f936-107">CLI 2.0</span></span>](network-watcher-nsg-flow-logging-cli.md)
> - [<span data-ttu-id="7f936-108">REST API</span><span class="sxs-lookup"><span data-stu-id="7f936-108">REST API</span></span>](network-watcher-nsg-flow-logging-rest.md)

<span data-ttu-id="7f936-109">網路安全性小組流程記錄檔是 tooview ingress 和 egress IP 流量，透過網路安全性群組相關的資訊可讓您的網路監看員的功能。</span><span class="sxs-lookup"><span data-stu-id="7f936-109">Network Security Group flow logs are a feature of Network Watcher that allows you tooview information about ingress and egress IP traffic through a Network Security Group.</span></span> <span data-ttu-id="7f936-110">這些流程記錄檔會寫入以 json 格式，並顯示輸出和輸入每個規則為基礎的流量，hello NIC hello 流程適用於，5 個 tuple hello 流程 （來源/目的地 IP，來源/目的地連接埠通訊協定） 的資訊，並允許流量，如果 hello 或被拒絕。</span><span class="sxs-lookup"><span data-stu-id="7f936-110">These flow logs are written in json format and show outbound and inbound flows on a per rule basis, hello NIC hello flow applies to, 5-tuple information about hello flow (Source/Destination IP, Source/Destination Port, Protocol), and if hello traffic was allowed or denied.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="7f936-111">開始之前</span><span class="sxs-lookup"><span data-stu-id="7f936-111">Before you begin</span></span>

<span data-ttu-id="7f936-112">ARMclient 是使用 PowerShell 的使用的 toocall hello REST API。</span><span class="sxs-lookup"><span data-stu-id="7f936-112">ARMclient is used toocall hello REST API using PowerShell.</span></span> <span data-ttu-id="7f936-113">您可以在 chocolatey 的 [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient) 上找到 ARMClient</span><span class="sxs-lookup"><span data-stu-id="7f936-113">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient)</span></span>

<span data-ttu-id="7f936-114">此案例假設您已依照中的 hello 步驟[建立網路監看員](network-watcher-create.md)toocreate 網路監看員。</span><span class="sxs-lookup"><span data-stu-id="7f936-114">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span>

> [!Important]
> <span data-ttu-id="7f936-115">網路監看員 REST api 呼叫 hello hello 要求 URI 是 hello 包含 hello 網路監看員，您執行的 hello 診斷動作不 hello 資源的資源群組中的資源群組名稱。</span><span class="sxs-lookup"><span data-stu-id="7f936-115">For Network Watcher REST API calls hello resource group name in hello request URI is hello resource group that contains hello Network Watcher, not hello resources you are performing hello diagnostic actions on.</span></span>

## <a name="scenario"></a><span data-ttu-id="7f936-116">案例</span><span class="sxs-lookup"><span data-stu-id="7f936-116">Scenario</span></span>

<span data-ttu-id="7f936-117">涵蓋在本文中的 hello 案例顯示如何 tooenable、 停用及查詢的流程使用 hello REST API 的記錄檔。</span><span class="sxs-lookup"><span data-stu-id="7f936-117">hello scenario covered in this article shows you how tooenable, disable, and query flow logs using hello REST API.</span></span> <span data-ttu-id="7f936-118">請瀏覽更多關於網路安全性群組流程 loggings，toolearn[網路安全性小組流程記錄概觀](network-watcher-nsg-flow-logging-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="7f936-118">toolearn more about Network Security Group flow loggings, visit [Network Security Group flow logging - Overview](network-watcher-nsg-flow-logging-overview.md).</span></span>

<span data-ttu-id="7f936-119">在此案例中，您將會：</span><span class="sxs-lookup"><span data-stu-id="7f936-119">In this scenario, you will:</span></span>

* <span data-ttu-id="7f936-120">啟用流程記錄</span><span class="sxs-lookup"><span data-stu-id="7f936-120">Enable flow logs</span></span>
* <span data-ttu-id="7f936-121">停用流程記錄</span><span class="sxs-lookup"><span data-stu-id="7f936-121">Disable flow logs</span></span>
* <span data-ttu-id="7f936-122">查詢流量記錄狀態</span><span class="sxs-lookup"><span data-stu-id="7f936-122">Query flow logs status</span></span>

## <a name="log-in-with-armclient"></a><span data-ttu-id="7f936-123">使用 ARMClient 登入</span><span class="sxs-lookup"><span data-stu-id="7f936-123">Log in with ARMClient</span></span>

<span data-ttu-id="7f936-124">登入 tooarmclient 與您的 Azure 認證。</span><span class="sxs-lookup"><span data-stu-id="7f936-124">Log in tooarmclient with your Azure credentials.</span></span>

```PowerShell
armclient login
```

## <a name="register-insights-provider"></a><span data-ttu-id="7f936-125">註冊 Insights 提供者</span><span class="sxs-lookup"><span data-stu-id="7f936-125">Register Insights provider</span></span>

<span data-ttu-id="7f936-126">為了讓流量記錄 toowork 成功，hello **Microsoft.Insights**必須註冊提供者。</span><span class="sxs-lookup"><span data-stu-id="7f936-126">In order for flow logging toowork successfully, hello **Microsoft.Insights** provider must be registered.</span></span> <span data-ttu-id="7f936-127">如果您不確定是否 hello **Microsoft.Insights**提供者是已註冊，請執行的 hello 下列指令碼。</span><span class="sxs-lookup"><span data-stu-id="7f936-127">If you are not sure if hello **Microsoft.Insights** provider is registered, run hello following script.</span></span>

```powershell
$subscriptionId = "00000000-0000-0000-0000-000000000000"
armclient post "https://management.azure.com//subscriptions/${subscriptionId}/providers/Microsoft.Insights/register?api-version=2016-09-01"
```

## <a name="enable-network-security-group-flow-logs"></a><span data-ttu-id="7f936-128">啟用網路安全性群組流量記錄</span><span class="sxs-lookup"><span data-stu-id="7f936-128">Enable Network Security Group flow logs</span></span>

<span data-ttu-id="7f936-129">hello 命令 tooenable 流程記錄檔以 hello 下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="7f936-129">hello command tooenable flow logs is shown in hello following example:</span></span>

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

<span data-ttu-id="7f936-130">hello 從傳回的回應 hello 上述範例是，如下所示：</span><span class="sxs-lookup"><span data-stu-id="7f936-130">hello response returned from hello preceding example is as follows:</span></span>

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

## <a name="disable-network-security-group-flow-logs"></a><span data-ttu-id="7f936-131">停用網路安全性群組流量記錄</span><span class="sxs-lookup"><span data-stu-id="7f936-131">Disable Network Security Group flow logs</span></span>

<span data-ttu-id="7f936-132">下列範例 toodisable 流量使用 hello 記錄。</span><span class="sxs-lookup"><span data-stu-id="7f936-132">Use hello following example toodisable flow logs.</span></span> <span data-ttu-id="7f936-133">hello 呼叫是相同 hello 與啟用流程記錄檔中，除了**false** hello 啟用屬性設定。</span><span class="sxs-lookup"><span data-stu-id="7f936-133">hello call is hello same as enabling flow logs, except **false** is set for hello enabled property.</span></span>

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

<span data-ttu-id="7f936-134">hello 從傳回的回應 hello 上述範例是，如下所示：</span><span class="sxs-lookup"><span data-stu-id="7f936-134">hello response returned from hello preceding example is as follows:</span></span>

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

## <a name="query-flow-logs"></a><span data-ttu-id="7f936-135">查詢流量記錄</span><span class="sxs-lookup"><span data-stu-id="7f936-135">Query flow logs</span></span>

<span data-ttu-id="7f936-136">下列查詢 hello 流程的狀態 REST 呼叫的 hello 登入網路安全性群組。</span><span class="sxs-lookup"><span data-stu-id="7f936-136">hello following REST call queries hello status of flow logs on a Network Security Group.</span></span>

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

<span data-ttu-id="7f936-137">hello 以下是傳回的 hello 回應的範例：</span><span class="sxs-lookup"><span data-stu-id="7f936-137">hello following is an example of hello response returned:</span></span>

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

## <a name="download-a-flow-log"></a><span data-ttu-id="7f936-138">下載流量記錄</span><span class="sxs-lookup"><span data-stu-id="7f936-138">Download a flow log</span></span>

<span data-ttu-id="7f936-139">hello 流程記錄檔的儲存位置是在建立時定義。</span><span class="sxs-lookup"><span data-stu-id="7f936-139">hello storage location of a flow log is defined at creation.</span></span> <span data-ttu-id="7f936-140">這些非固定格式儲存的記錄檔 tooa 儲存體帳戶是 Microsoft Azure 儲存體總管 中，這可以在這裡下載方便的工具 tooaccess: http://storageexplorer.com/</span><span class="sxs-lookup"><span data-stu-id="7f936-140">A convenient tool tooaccess these flow logs saved tooa storage account is Microsoft Azure Storage Explorer, which can be downloaded here:  http://storageexplorer.com/</span></span>

<span data-ttu-id="7f936-141">如果指定的儲存體帳戶，則封包擷取檔案會儲存在下列位置的 hello tooa 儲存體帳戶：</span><span class="sxs-lookup"><span data-stu-id="7f936-141">If a storage account is specified, packet capture files are saved tooa storage account at hello following location:</span></span>

```
https://{storageAccountName}.blob.core.windows.net/insights-logs-networksecuritygroupflowevent/resourceId%3D/subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/microsoft.network/networksecuritygroups/{nsgName}/{year}/{month}/{day}/PT1H.json
```

## <a name="next-steps"></a><span data-ttu-id="7f936-142">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7f936-142">Next steps</span></span>

<span data-ttu-id="7f936-143">了解如何太[視覺化與 PowerBI NSG 流程記錄](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span><span class="sxs-lookup"><span data-stu-id="7f936-143">Learn how too[Visualize your NSG flow logs with PowerBI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span></span>

<span data-ttu-id="7f936-144">了解如何太[視覺化 NSG 流程記錄與開放原始碼工具](network-watcher-visualize-nsg-flow-logs-open-source-tools.md)</span><span class="sxs-lookup"><span data-stu-id="7f936-144">Learn how too[Visualize your NSG flow logs with open source tools](network-watcher-visualize-nsg-flow-logs-open-source-tools.md)</span></span>
