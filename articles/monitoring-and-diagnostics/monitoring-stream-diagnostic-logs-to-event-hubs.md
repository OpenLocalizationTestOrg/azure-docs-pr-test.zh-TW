---
title: "將 Azure 診斷記錄串流至事件中樞命名空間 | Microsoft Docs"
description: "了解如何將 Azure 診斷記錄串流至事件中樞命名空間。"
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 42bc4845-c564-4568-b72d-0614591ebd80
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: johnkem
ms.openlocfilehash: 01ba8ddfcf90e1368ac147296fd180f99420d96f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="stream-azure-diagnostic-logs-to-an-event-hubs-namespace"></a><span data-ttu-id="12c5b-103">將 Azure 診斷記錄串流至事件中樞命名空間</span><span class="sxs-lookup"><span data-stu-id="12c5b-103">Stream Azure Diagnostic Logs to an Event Hubs Namespace</span></span>
<span data-ttu-id="12c5b-104">您可以使用入口網站中內建的「匯出至事件中樞」選項，或透過 Azure PowerShell Cmdlet 或 Azure CLI 來啟用診斷設定中服務匯流排規則識別碼的方式，以近乎即時的速度將 **[Azure 診斷記錄](monitoring-overview-of-diagnostic-logs.md)**串流至任何應用程式。</span><span class="sxs-lookup"><span data-stu-id="12c5b-104">**[Azure diagnostic logs](monitoring-overview-of-diagnostic-logs.md)** can be streamed in near real time to any application using the built-in “Export to Event Hubs” option in the Portal, or by enabling the Service Bus Rule ID in a diagnostic setting via the Azure PowerShell Cmdlets or Azure CLI.</span></span>

## <a name="what-you-can-do-with-diagnostics-logs-and-event-hubs"></a><span data-ttu-id="12c5b-105">您可以使用診斷記錄和事件中樞執行的項目</span><span class="sxs-lookup"><span data-stu-id="12c5b-105">What you can do with diagnostics logs and Event Hubs</span></span>
<span data-ttu-id="12c5b-106">這裡有一些您可以使用診斷日誌串流功能的方法：</span><span class="sxs-lookup"><span data-stu-id="12c5b-106">Here are just a few ways you might use the streaming capability for Diagnostic Logs:</span></span>

* <span data-ttu-id="12c5b-107">**串流至第三方記錄與遙測系統** – 經過一段時間，事件中樞串流會成為將活動記錄輸送到第三方 SIEM 與記錄分析解決方案的機制。</span><span class="sxs-lookup"><span data-stu-id="12c5b-107">**Stream logs to 3rd party logging and telemetry systems** – Over time, Event Hubs streaming will become the mechanism to pipe your diagnostic logs in to third-party SIEMs and log analytics solutions.</span></span>
* <span data-ttu-id="12c5b-108">**將「最忙碌路徑」串流至 PowerBI 以檢視服務健全狀況** – 您可以使用事件中樞、串流分析和 PowerBI，輕鬆快速地將診斷資料轉換為 Azure 服務上的深入解析。</span><span class="sxs-lookup"><span data-stu-id="12c5b-108">**View service health by streaming “hot path” data to PowerBI** – Using Event Hubs, Stream Analytics, and PowerBI, you can easily transform your diagnostics data in to near real-time insights on your Azure services.</span></span> <span data-ttu-id="12c5b-109">[此文件文章提供絕佳概觀，說明如何設定事件中樞、使用串流分析處理資料，以及使用 PowerBI 作為輸出](../stream-analytics/stream-analytics-power-bi-dashboard.md)。</span><span class="sxs-lookup"><span data-stu-id="12c5b-109">[This documentation article gives a great overview of how to set up Event Hubs, process data with Stream Analytics, and use PowerBI as an output](../stream-analytics/stream-analytics-power-bi-dashboard.md).</span></span> <span data-ttu-id="12c5b-110">以下是設定診斷記錄的一些祕訣︰</span><span class="sxs-lookup"><span data-stu-id="12c5b-110">Here are a few tips for getting set up with diagnostic logs:</span></span>
  
  * <span data-ttu-id="12c5b-111">當您勾選入口網站中的選項，或透過 PowerShell 進行啟用時，就會自動建立診斷記錄類別的事件中樞，因此您需要選取命名空間中名稱開頭為 **insights-** 的事件中樞。</span><span class="sxs-lookup"><span data-stu-id="12c5b-111">An event hub for a category of diagnostic logs is created automatically when you check the option in the portal or enable it through PowerShell, so you want to select the event hub in the namespace with the name that starts with **insights-**.</span></span>
  * <span data-ttu-id="12c5b-112">下列 SQL 程式碼是您可以使用的範例串流分析查詢，能將所有記錄資料剖析至 PowerBI 表格：</span><span class="sxs-lookup"><span data-stu-id="12c5b-112">The following SQL code is a sample Stream Analytics query that you can use to parse all the log data in to a PowerBI table:</span></span>

    ```sql
    SELECT
    records.ArrayValue.[Properties you want to track]
    INTO
    [OutputSourceName – the PowerBI source]
    FROM
    [InputSourceName] AS e
    CROSS APPLY GetArrayElements(e.records) AS records
    ```

* <span data-ttu-id="12c5b-113">**建置自訂遙測及記錄平台** – 如果您已有自建遙測平台或正好在考慮建置一個，事件中樞所具備的高度可調整的發佈訂閱特質可讓您靈活擷取診斷記錄檔。</span><span class="sxs-lookup"><span data-stu-id="12c5b-113">**Build a custom telemetry and logging platform** – If you already have a custom-built telemetry platform or are just thinking about building one, the highly scalable publish-subscribe nature of Event Hubs allows you to flexibly ingest diagnostic logs.</span></span> <span data-ttu-id="12c5b-114">[請參閱此處的 Dan Rosanova 指南，以在全球級別的遙測平台中使用事件中樞](https://azure.microsoft.com/documentation/videos/build-2015-designing-and-sizing-a-global-scale-telemetry-platform-on-azure-event-Hubs/)。</span><span class="sxs-lookup"><span data-stu-id="12c5b-114">[See Dan Rosanova’s guide to using Event Hubs in a global scale telemetry platform here](https://azure.microsoft.com/documentation/videos/build-2015-designing-and-sizing-a-global-scale-telemetry-platform-on-azure-event-Hubs/).</span></span>

## <a name="enable-streaming-of-diagnostic-logs"></a><span data-ttu-id="12c5b-115">啟用診斷記錄的串流</span><span class="sxs-lookup"><span data-stu-id="12c5b-115">Enable streaming of diagnostic logs</span></span>
<span data-ttu-id="12c5b-116">您可以透過入口網站或使用 [Azure 監視器 REST API](https://docs.microsoft.com/rest/api/monitor/servicediagnosticsettings)，啟用以程式控制方式對診斷記錄進行串流的功能。</span><span class="sxs-lookup"><span data-stu-id="12c5b-116">You can enable streaming of diagnostic logs programmatically, via the portal, or using the [Azure Monitor REST APIs](https://docs.microsoft.com/rest/api/monitor/servicediagnosticsettings).</span></span> <span data-ttu-id="12c5b-117">無論如何，您所建立的診斷設定可讓您指定事件中樞命名空間，以及記錄類別和您需要傳送至命名空間的計量。</span><span class="sxs-lookup"><span data-stu-id="12c5b-117">Either way, you create a diagnostic setting in which you specify an Event Hubs namespace and the log categories and metrics you want to send in to the namespace.</span></span> <span data-ttu-id="12c5b-118">針對您所啟用的每個記錄類別，會在命名空間中建立事件中樞。</span><span class="sxs-lookup"><span data-stu-id="12c5b-118">An event hub is created in the namespace for each log category you enable.</span></span> <span data-ttu-id="12c5b-119">診斷**記錄類別**是一種資源可以收集的記錄類型。</span><span class="sxs-lookup"><span data-stu-id="12c5b-119">A diagnostic **log category** is a type of log that a resource may collect.</span></span>

> [!WARNING]
> <span data-ttu-id="12c5b-120">啟用和串流來自計算資源 (例如，VM 或 Service Fabric) 的診斷記錄 [需要一組不同的步驟](../event-hubs/event-hubs-streaming-azure-diags-data.md)。</span><span class="sxs-lookup"><span data-stu-id="12c5b-120">Enabling and streaming diagnostic logs from Compute resources (for example, VMs or Service Fabric) [requires a different set of steps](../event-hubs/event-hubs-streaming-azure-diags-data.md).</span></span>
> 
> 

<span data-ttu-id="12c5b-121">服務匯流排或事件中樞命名空間不一定要和資源發出記錄檔屬於相同的訂用帳戶，只要進行設定的使用者有這兩個訂用帳戶的適當 RBAC 存取權。</span><span class="sxs-lookup"><span data-stu-id="12c5b-121">The Service Bus or Event Hubs namespace does not have to be in the same subscription as the resource emitting logs as long as the user who configures the setting has appropriate RBAC access to both subscriptions.</span></span>

## <a name="stream-diagnostic-logs-using-the-portal"></a><span data-ttu-id="12c5b-122">使用入口網站串流診斷記錄</span><span class="sxs-lookup"><span data-stu-id="12c5b-122">Stream diagnostic logs using the portal</span></span>
1. <span data-ttu-id="12c5b-123">在入口網站中，瀏覽至 Azure 監視器，然後按一下 [診斷設定]</span><span class="sxs-lookup"><span data-stu-id="12c5b-123">In the portal, navigate to Azure Monitor and click on **Diagnostic Settings**</span></span>

    ![Azure 監視器的監視區段](media/monitoring-stream-diagnostic-logs-to-event-hubs/diagnostic-settings-blade.png)

2. <span data-ttu-id="12c5b-125">選擇性地依資源群組或資源類型篩選清單，然後按一下您要設定診斷設定的資源。</span><span class="sxs-lookup"><span data-stu-id="12c5b-125">Optionally filter the list by resource group or resource type, then click on the resource for which you would like to set a diagnostic setting.</span></span>

3. <span data-ttu-id="12c5b-126">如果您選取的資源上沒有任何設定，系統會提示您建立設定。</span><span class="sxs-lookup"><span data-stu-id="12c5b-126">If no settings exist on the resource you have selected, you are prompted to create a setting.</span></span> <span data-ttu-id="12c5b-127">按一下「開啟診斷」。</span><span class="sxs-lookup"><span data-stu-id="12c5b-127">Click "Turn on diagnostics."</span></span>

   ![新增診斷設定 - 無現有的設定](media/monitoring-stream-diagnostic-logs-to-event-hubs/diagnostic-settings-none.png)

   <span data-ttu-id="12c5b-129">如果資源上已有設定，您將會看此資源上已設定的設定清單。</span><span class="sxs-lookup"><span data-stu-id="12c5b-129">If there are existing settings on the resource, you will see a list of settings already configured on this resource.</span></span> <span data-ttu-id="12c5b-130">按一下「新增診斷設定」。</span><span class="sxs-lookup"><span data-stu-id="12c5b-130">Click "Add diagnostic setting."</span></span>

   ![新增診斷設定 - 現有的設定](media/monitoring-stream-diagnostic-logs-to-event-hubs/diagnostic-settings-multiple.png)

3. <span data-ttu-id="12c5b-132">為設定提供名稱並核取 [串流至事件中樞] 方塊，然後選取 [事件中樞命名空間]。</span><span class="sxs-lookup"><span data-stu-id="12c5b-132">Give your setting a name and check the box for **Stream to an event hub**, then select an Event Hubs namespace.</span></span>
   
   ![新增診斷設定 - 現有的設定](media/monitoring-stream-diagnostic-logs-to-event-hubs/diagnostic-settings-configure.png)
    
   <span data-ttu-id="12c5b-134">選取的命名空間將會是事件中樞的建立所在 (如果這是您第一次的串流診斷記錄) 或串流處理的目的地 (如果已存在將該記錄檔分類串流至此命名空間的資源)，而原則會定義串流機制擁有的權限。</span><span class="sxs-lookup"><span data-stu-id="12c5b-134">The namespace selected will be where the event hub is created (if this is your first time streaming diagnostic logs) or streamed to (if there are already resources that are streaming that log category to this namespace), and the policy defines the permissions that the streaming mechanism has.</span></span> <span data-ttu-id="12c5b-135">目前，將事件串流到中樞需要管理、傳送和接聽的權限。</span><span class="sxs-lookup"><span data-stu-id="12c5b-135">Today, streaming to an event hub requires Manage, Send, and Listen permissions.</span></span> <span data-ttu-id="12c5b-136">您可以在入口網站的 [設定] 索引標籤下，為您的命名空間建立或修改事件中樞命名空間共用存取原則。</span><span class="sxs-lookup"><span data-stu-id="12c5b-136">You can create or modify Event Hubs namespace shared access policies in the portal under the Configure tab for your namespace.</span></span> <span data-ttu-id="12c5b-137">若要更新其中一個診斷設定，用戶端必須擁有事件中樞授權規則的 ListKey 權限。</span><span class="sxs-lookup"><span data-stu-id="12c5b-137">To update one of these diagnostic settings, the client must have the ListKey permission on the Event Hubs authorization rule.</span></span>

4. <span data-ttu-id="12c5b-138">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="12c5b-138">Click **Save**.</span></span>

<span data-ttu-id="12c5b-139">過了幾分鐘之後，新的設定就會出現在此資源的設定清單中，而且每次產生新的事件資料，都會將診斷記錄串流至該儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="12c5b-139">After a few moments, the new setting appears in your list of settings for this resource, and diagnostic logs are streamed to that storage account as soon as new event data is generated.</span></span>

### <a name="via-powershell-cmdlets"></a><span data-ttu-id="12c5b-140">透過 PowerShell Cmdlet</span><span class="sxs-lookup"><span data-stu-id="12c5b-140">Via PowerShell Cmdlets</span></span>
<span data-ttu-id="12c5b-141">若要透過 [Azure PowerShell Cmdlet](insights-powershell-samples.md) 啟用串流功能，您可以使用 `Set-AzureRmDiagnosticSetting` Cmdlet 搭配下列參數︰</span><span class="sxs-lookup"><span data-stu-id="12c5b-141">To enable streaming via the [Azure PowerShell Cmdlets](insights-powershell-samples.md), you can use the `Set-AzureRmDiagnosticSetting` cmdlet with these parameters:</span></span>

```powershell
Set-AzureRmDiagnosticSetting -ResourceId [your resource ID] -ServiceBusRuleId [your Service Bus rule ID] -Enabled $true
```

<span data-ttu-id="12c5b-142">服務匯流排規則識別碼是此格式的字串︰`{Service Bus resource ID}/authorizationrules/{key name}`，例如，`/subscriptions/{subscription ID}/resourceGroups/Default-ServiceBus-WestUS/providers/Microsoft.ServiceBus/namespaces/{Service Bus namespace}/authorizationrules/RootManageSharedAccessKey`。</span><span class="sxs-lookup"><span data-stu-id="12c5b-142">The Service Bus Rule ID is a string with this format: `{Service Bus resource ID}/authorizationrules/{key name}`, for example, `/subscriptions/{subscription ID}/resourceGroups/Default-ServiceBus-WestUS/providers/Microsoft.ServiceBus/namespaces/{Service Bus namespace}/authorizationrules/RootManageSharedAccessKey`.</span></span>

### <a name="via-azure-cli"></a><span data-ttu-id="12c5b-143">透過 Azure CLI</span><span class="sxs-lookup"><span data-stu-id="12c5b-143">Via Azure CLI</span></span>
<span data-ttu-id="12c5b-144">若要透過 [Azure CLI](insights-cli-samples.md) 啟用串流功能，您可以使用如下的 `insights diagnostic set` 命令︰</span><span class="sxs-lookup"><span data-stu-id="12c5b-144">To enable streaming via the [Azure CLI](insights-cli-samples.md), you can use the `insights diagnostic set` command like this:</span></span>

```azurecli
azure insights diagnostic set --resourceId <resourceID> --serviceBusRuleId <serviceBusRuleID> --enabled true
```

<span data-ttu-id="12c5b-145">如 PowerShell Cmdlet 所述，對服務匯流排規則識別碼使用相同的格式。</span><span class="sxs-lookup"><span data-stu-id="12c5b-145">Use the same format for Service Bus Rule ID as explained for the PowerShell Cmdlet.</span></span>

## <a name="how-do-i-consume-the-log-data-from-event-hubs"></a><span data-ttu-id="12c5b-146">我要如何透過事件中樞取用記錄檔資料？</span><span class="sxs-lookup"><span data-stu-id="12c5b-146">How do I consume the log data from Event Hubs?</span></span>
<span data-ttu-id="12c5b-147">此處是來自事件中樞的範例輸出資料：</span><span class="sxs-lookup"><span data-stu-id="12c5b-147">Here is sample output data from Event Hubs:</span></span>

```json
{
    "records": [
        {
            "time": "2016-07-15T18:00:22.6235064Z",
            "workflowId": "/SUBSCRIPTIONS/DF602C9C-7AA0-407D-A6FB-EB20C8BD1192/RESOURCEGROUPS/JOHNKEMTEST/PROVIDERS/MICROSOFT.LOGIC/WORKFLOWS/JOHNKEMTESTLA",
            "resourceId": "/SUBSCRIPTIONS/DF602C9C-7AA0-407D-A6FB-EB20C8BD1192/RESOURCEGROUPS/JOHNKEMTEST/PROVIDERS/MICROSOFT.LOGIC/WORKFLOWS/JOHNKEMTESTLA/RUNS/08587330013509921957/ACTIONS/SEND_EMAIL",
            "category": "WorkflowRuntime",
            "level": "Error",
            "operationName": "Microsoft.Logic/workflows/workflowActionCompleted",
            "properties": {
                "$schema": "2016-04-01-preview",
                "startTime": "2016-07-15T17:58:55.048482Z",
                "endTime": "2016-07-15T18:00:22.4109204Z",
                "status": "Failed",
                "code": "BadGateway",
                "resource": {
                    "subscriptionId": "df602c9c-7aa0-407d-a6fb-eb20c8bd1192",
                    "resourceGroupName": "JohnKemTest",
                    "workflowId": "243aac67fe904cf195d4a28297803785",
                    "workflowName": "JohnKemTestLA",
                    "runId": "08587330013509921957",
                    "location": "westus",
                    "actionName": "Send_email"
                },
                "correlation": {
                    "actionTrackingId": "29a9862f-969b-4c70-90c4-dfbdc814e413",
                    "clientTrackingId": "08587330013509921958"
                }
            }
        },
        {
            "time": "2016-07-15T18:01:15.7532989Z",
            "workflowId": "/SUBSCRIPTIONS/DF602C9C-7AA0-407D-A6FB-EB20C8BD1192/RESOURCEGROUPS/JOHNKEMTEST/PROVIDERS/MICROSOFT.LOGIC/WORKFLOWS/JOHNKEMTESTLA",
            "resourceId": "/SUBSCRIPTIONS/DF602C9C-7AA0-407D-A6FB-EB20C8BD1192/RESOURCEGROUPS/JOHNKEMTEST/PROVIDERS/MICROSOFT.LOGIC/WORKFLOWS/JOHNKEMTESTLA/RUNS/08587330012106702630/ACTIONS/SEND_EMAIL",
            "category": "WorkflowRuntime",
            "level": "Information",
            "operationName": "Microsoft.Logic/workflows/workflowActionStarted",
            "properties": {
                "$schema": "2016-04-01-preview",
                "startTime": "2016-07-15T18:01:15.5828115Z",
                "status": "Running",
                "resource": {
                    "subscriptionId": "df602c9c-7aa0-407d-a6fb-eb20c8bd1192",
                    "resourceGroupName": "JohnKemTest",
                    "workflowId": "243aac67fe904cf195d4a28297803785",
                    "workflowName": "JohnKemTestLA",
                    "runId": "08587330012106702630",
                    "location": "westus",
                    "actionName": "Send_email"
                },
                "correlation": {
                    "actionTrackingId": "042fb72c-7bd4-439e-89eb-3cf4409d429e",
                    "clientTrackingId": "08587330012106702632"
                }
            }
        }
    ]
}
```

| <span data-ttu-id="12c5b-148">元素名稱</span><span class="sxs-lookup"><span data-stu-id="12c5b-148">Element Name</span></span> | <span data-ttu-id="12c5b-149">說明</span><span class="sxs-lookup"><span data-stu-id="12c5b-149">Description</span></span> |
| --- | --- |
| <span data-ttu-id="12c5b-150">記錄數</span><span class="sxs-lookup"><span data-stu-id="12c5b-150">records</span></span> |<span data-ttu-id="12c5b-151">此承載中的所有記錄事件的陣列。</span><span class="sxs-lookup"><span data-stu-id="12c5b-151">An array of all log events in this payload.</span></span> |
| <span data-ttu-id="12c5b-152">分析</span><span class="sxs-lookup"><span data-stu-id="12c5b-152">time</span></span> |<span data-ttu-id="12c5b-153">事件發生的時間。</span><span class="sxs-lookup"><span data-stu-id="12c5b-153">Time at which the event occurred.</span></span> |
| <span data-ttu-id="12c5b-154">category</span><span class="sxs-lookup"><span data-stu-id="12c5b-154">category</span></span> |<span data-ttu-id="12c5b-155">此事件的記錄檔分類。</span><span class="sxs-lookup"><span data-stu-id="12c5b-155">Log category for this event.</span></span> |
| <span data-ttu-id="12c5b-156">resourceId</span><span class="sxs-lookup"><span data-stu-id="12c5b-156">resourceId</span></span> |<span data-ttu-id="12c5b-157">產生此事件之資源的資源識別碼。</span><span class="sxs-lookup"><span data-stu-id="12c5b-157">Resource ID of the resource that generated this event.</span></span> |
| <span data-ttu-id="12c5b-158">operationName</span><span class="sxs-lookup"><span data-stu-id="12c5b-158">operationName</span></span> |<span data-ttu-id="12c5b-159">作業名稱。</span><span class="sxs-lookup"><span data-stu-id="12c5b-159">Name of the operation.</span></span> |
| <span data-ttu-id="12c5b-160">層級</span><span class="sxs-lookup"><span data-stu-id="12c5b-160">level</span></span> |<span data-ttu-id="12c5b-161">選用。</span><span class="sxs-lookup"><span data-stu-id="12c5b-161">Optional.</span></span> <span data-ttu-id="12c5b-162">表示記錄事件層級。</span><span class="sxs-lookup"><span data-stu-id="12c5b-162">Indicates the log event level.</span></span> |
| <span data-ttu-id="12c5b-163">properties</span><span class="sxs-lookup"><span data-stu-id="12c5b-163">properties</span></span> |<span data-ttu-id="12c5b-164">事件的屬性。</span><span class="sxs-lookup"><span data-stu-id="12c5b-164">Properties of the event.</span></span> |

<span data-ttu-id="12c5b-165">您可以在[這裡](monitoring-overview-of-diagnostic-logs.md)檢視支援串流至事件中樞的所有資源提供者清單。</span><span class="sxs-lookup"><span data-stu-id="12c5b-165">You can view a list of all resource providers that support streaming to Event Hubs [here](monitoring-overview-of-diagnostic-logs.md).</span></span>

## <a name="stream-data-from-compute-resources"></a><span data-ttu-id="12c5b-166">從計算資源中串流資料</span><span class="sxs-lookup"><span data-stu-id="12c5b-166">Stream data from Compute resources</span></span>
<span data-ttu-id="12c5b-167">您也可以使用 Windows Azure 診斷代理程式，從計算資源中串流診斷記錄。</span><span class="sxs-lookup"><span data-stu-id="12c5b-167">You can also stream diagnostic logs from Compute resources using the Windows Azure Diagnostics agent.</span></span> <span data-ttu-id="12c5b-168">[請參閱本文章](../event-hubs/event-hubs-streaming-azure-diags-data.md)了解如何設定。</span><span class="sxs-lookup"><span data-stu-id="12c5b-168">[See this article](../event-hubs/event-hubs-streaming-azure-diags-data.md) for how to set that up.</span></span>

## <a name="next-steps"></a><span data-ttu-id="12c5b-169">後續步驟</span><span class="sxs-lookup"><span data-stu-id="12c5b-169">Next steps</span></span>
* [<span data-ttu-id="12c5b-170">深入了解 Azure 診斷記錄檔</span><span class="sxs-lookup"><span data-stu-id="12c5b-170">Read more about Azure Diagnostic Logs</span></span>](monitoring-overview-of-diagnostic-logs.md)
* [<span data-ttu-id="12c5b-171">開始使用事件中心</span><span class="sxs-lookup"><span data-stu-id="12c5b-171">Get started with Event Hubs</span></span>](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)

