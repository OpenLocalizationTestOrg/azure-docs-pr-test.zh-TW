---
title: "使用 Azure 網路監看員管理網路安全性群組流量記錄 - REST API | Microsoft Docs"
description: "此頁面說明如何使用 REST API 在 Azure 網路監看員中管理網路安全性群組流量記錄"
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
ms.openlocfilehash: c89a2ab4c39978771c940a819493b4e2283d5f9f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="configuring-network-security-group-flow-logs-using-rest-api"></a><span data-ttu-id="2cfca-103">使用 REST API 設定網路安全性群組流量記錄</span><span class="sxs-lookup"><span data-stu-id="2cfca-103">Configuring Network Security Group flow logs using REST API</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="2cfca-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="2cfca-104">Azure portal</span></span>](network-watcher-nsg-flow-logging-portal.md)
> - [<span data-ttu-id="2cfca-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="2cfca-105">PowerShell</span></span>](network-watcher-nsg-flow-logging-powershell.md)
> - [<span data-ttu-id="2cfca-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="2cfca-106">CLI 1.0</span></span>](network-watcher-nsg-flow-logging-cli-nodejs.md)
> - [<span data-ttu-id="2cfca-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="2cfca-107">CLI 2.0</span></span>](network-watcher-nsg-flow-logging-cli.md)
> - [<span data-ttu-id="2cfca-108">REST API</span><span class="sxs-lookup"><span data-stu-id="2cfca-108">REST API</span></span>](network-watcher-nsg-flow-logging-rest.md)

<span data-ttu-id="2cfca-109">網路安全性群組流量記錄是網路監看員的一項功能，可讓您檢視透過網路安全性群組傳輸之輸入和輸出 IP 流量的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="2cfca-109">Network Security Group flow logs are a feature of Network Watcher that allows you to view information about ingress and egress IP traffic through a Network Security Group.</span></span> <span data-ttu-id="2cfca-110">這些流量記錄是以 json 格式撰寫，會顯示每一規則的輸出和輸入流量、流量套用至的 NIC、有關流量的 5 個 Tuple 資訊 (來源/目的地 IP、來源/目的地連接埠、通訊協定)，以及流量是被允許或拒絕。</span><span class="sxs-lookup"><span data-stu-id="2cfca-110">These flow logs are written in json format and show outbound and inbound flows on a per rule basis, the NIC the flow applies to, 5-tuple information about the flow (Source/Destination IP, Source/Destination Port, Protocol), and if the traffic was allowed or denied.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="2cfca-111">開始之前</span><span class="sxs-lookup"><span data-stu-id="2cfca-111">Before you begin</span></span>

<span data-ttu-id="2cfca-112">使用 ARMclient 透過 PowerShell 呼叫 REST API。</span><span class="sxs-lookup"><span data-stu-id="2cfca-112">ARMclient is used to call the REST API using PowerShell.</span></span> <span data-ttu-id="2cfca-113">您可以在 chocolatey 的 [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient) 上找到 ARMClient</span><span class="sxs-lookup"><span data-stu-id="2cfca-113">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient)</span></span>

<span data-ttu-id="2cfca-114">此案例假設您已依照[建立網路監看員](network-watcher-create.md)中的步驟建立網路監看員。</span><span class="sxs-lookup"><span data-stu-id="2cfca-114">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span>

> [!Important]
> <span data-ttu-id="2cfca-115">針對網路監看員 REST API 呼叫，要求 URI 中的資源群組名稱是包含網路監看員的資源群組，而非您要執行診斷動作的資源。</span><span class="sxs-lookup"><span data-stu-id="2cfca-115">For Network Watcher REST API calls the resource group name in the request URI is the resource group that contains the Network Watcher, not the resources you are performing the diagnostic actions on.</span></span>

## <a name="scenario"></a><span data-ttu-id="2cfca-116">案例</span><span class="sxs-lookup"><span data-stu-id="2cfca-116">Scenario</span></span>

<span data-ttu-id="2cfca-117">本文章涵蓋的案例會示範如何使用 REST API 啟用、停用以及查詢流程記錄。</span><span class="sxs-lookup"><span data-stu-id="2cfca-117">The scenario covered in this article shows you how to enable, disable, and query flow logs using the REST API.</span></span> <span data-ttu-id="2cfca-118">若要深入了解網路安全性群組流程記錄，請造訪[網路安全性群組流程記錄 - 概觀](network-watcher-nsg-flow-logging-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="2cfca-118">To learn more about Network Security Group flow loggings, visit [Network Security Group flow logging - Overview](network-watcher-nsg-flow-logging-overview.md).</span></span>

<span data-ttu-id="2cfca-119">在此案例中，您將會：</span><span class="sxs-lookup"><span data-stu-id="2cfca-119">In this scenario, you will:</span></span>

* <span data-ttu-id="2cfca-120">啟用流程記錄</span><span class="sxs-lookup"><span data-stu-id="2cfca-120">Enable flow logs</span></span>
* <span data-ttu-id="2cfca-121">停用流程記錄</span><span class="sxs-lookup"><span data-stu-id="2cfca-121">Disable flow logs</span></span>
* <span data-ttu-id="2cfca-122">查詢流量記錄狀態</span><span class="sxs-lookup"><span data-stu-id="2cfca-122">Query flow logs status</span></span>

## <a name="log-in-with-armclient"></a><span data-ttu-id="2cfca-123">使用 ARMClient 登入</span><span class="sxs-lookup"><span data-stu-id="2cfca-123">Log in with ARMClient</span></span>

<span data-ttu-id="2cfca-124">使用 Azure 認證登入 Armclient。</span><span class="sxs-lookup"><span data-stu-id="2cfca-124">Log in to armclient with your Azure credentials.</span></span>

```PowerShell
armclient login
```

## <a name="register-insights-provider"></a><span data-ttu-id="2cfca-125">註冊 Insights 提供者</span><span class="sxs-lookup"><span data-stu-id="2cfca-125">Register Insights provider</span></span>

<span data-ttu-id="2cfca-126">若要讓流量記錄成功運作，必須註冊 **Microsoft.Insights** 提供者。</span><span class="sxs-lookup"><span data-stu-id="2cfca-126">In order for flow logging to work successfully, the **Microsoft.Insights** provider must be registered.</span></span> <span data-ttu-id="2cfca-127">如果您不確定是否已註冊 **Microsoft.Insights** 提供者，請執行下列程式碼。</span><span class="sxs-lookup"><span data-stu-id="2cfca-127">If you are not sure if the **Microsoft.Insights** provider is registered, run the following script.</span></span>

```powershell
$subscriptionId = "00000000-0000-0000-0000-000000000000"
armclient post "https://management.azure.com//subscriptions/${subscriptionId}/providers/Microsoft.Insights/register?api-version=2016-09-01"
```

## <a name="enable-network-security-group-flow-logs"></a><span data-ttu-id="2cfca-128">啟用網路安全性群組流量記錄</span><span class="sxs-lookup"><span data-stu-id="2cfca-128">Enable Network Security Group flow logs</span></span>

<span data-ttu-id="2cfca-129">用來啟用流量記錄的命令如下列範例所示︰</span><span class="sxs-lookup"><span data-stu-id="2cfca-129">The command to enable flow logs is shown in the following example:</span></span>

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

<span data-ttu-id="2cfca-130">前述範例中所傳回的回應如下所示︰</span><span class="sxs-lookup"><span data-stu-id="2cfca-130">The response returned from the preceding example is as follows:</span></span>

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

## <a name="disable-network-security-group-flow-logs"></a><span data-ttu-id="2cfca-131">停用網路安全性群組流量記錄</span><span class="sxs-lookup"><span data-stu-id="2cfca-131">Disable Network Security Group flow logs</span></span>

<span data-ttu-id="2cfca-132">使用下列範例來停用流量記錄。</span><span class="sxs-lookup"><span data-stu-id="2cfca-132">Use the following example to disable flow logs.</span></span> <span data-ttu-id="2cfca-133">呼叫等同於啟用流程記錄，除了針對已啟用屬性設定的 **false**。</span><span class="sxs-lookup"><span data-stu-id="2cfca-133">The call is the same as enabling flow logs, except **false** is set for the enabled property.</span></span>

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

<span data-ttu-id="2cfca-134">前述範例中所傳回的回應如下所示︰</span><span class="sxs-lookup"><span data-stu-id="2cfca-134">The response returned from the preceding example is as follows:</span></span>

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

## <a name="query-flow-logs"></a><span data-ttu-id="2cfca-135">查詢流量記錄</span><span class="sxs-lookup"><span data-stu-id="2cfca-135">Query flow logs</span></span>

<span data-ttu-id="2cfca-136">下列 REST 呼叫會查詢網路安全性群組上的流程記錄狀態。</span><span class="sxs-lookup"><span data-stu-id="2cfca-136">The following REST call queries the status of flow logs on a Network Security Group.</span></span>

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

<span data-ttu-id="2cfca-137">以下是所回傳之回應的範例：</span><span class="sxs-lookup"><span data-stu-id="2cfca-137">The following is an example of the response returned:</span></span>

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

## <a name="download-a-flow-log"></a><span data-ttu-id="2cfca-138">下載流量記錄</span><span class="sxs-lookup"><span data-stu-id="2cfca-138">Download a flow log</span></span>

<span data-ttu-id="2cfca-139">流量記錄的儲存位置會在建立時定義。</span><span class="sxs-lookup"><span data-stu-id="2cfca-139">The storage location of a flow log is defined at creation.</span></span> <span data-ttu-id="2cfca-140">若要存取這些儲存至儲存體帳戶的流量記錄，Microsoft Azure 儲存體總管是很便利的工具，您可以在這裡下載︰http://storageexplorer.com/</span><span class="sxs-lookup"><span data-stu-id="2cfca-140">A convenient tool to access these flow logs saved to a storage account is Microsoft Azure Storage Explorer, which can be downloaded here:  http://storageexplorer.com/</span></span>

<span data-ttu-id="2cfca-141">如果指定了儲存體帳戶，封包擷取檔案便會儲存到儲存體帳戶的下列位置︰</span><span class="sxs-lookup"><span data-stu-id="2cfca-141">If a storage account is specified, packet capture files are saved to a storage account at the following location:</span></span>

```
https://{storageAccountName}.blob.core.windows.net/insights-logs-networksecuritygroupflowevent/resourceId%3D/subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/microsoft.network/networksecuritygroups/{nsgName}/{year}/{month}/{day}/PT1H.json
```

## <a name="next-steps"></a><span data-ttu-id="2cfca-142">後續步驟</span><span class="sxs-lookup"><span data-stu-id="2cfca-142">Next steps</span></span>

<span data-ttu-id="2cfca-143">了解如何[使用 PowerBI 視覺化 NSG 流量記錄](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span><span class="sxs-lookup"><span data-stu-id="2cfca-143">Learn how to [Visualize your NSG flow logs with PowerBI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span></span>

<span data-ttu-id="2cfca-144">了解如何[使用開放原始碼工具視覺化 NSG 流量記錄](network-watcher-visualize-nsg-flow-logs-open-source-tools.md)</span><span class="sxs-lookup"><span data-stu-id="2cfca-144">Learn how to [Visualize your NSG flow logs with open source tools](network-watcher-visualize-nsg-flow-logs-open-source-tools.md)</span></span>
