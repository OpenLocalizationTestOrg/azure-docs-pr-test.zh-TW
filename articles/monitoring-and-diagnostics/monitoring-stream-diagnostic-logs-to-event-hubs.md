---
title: "aaaStream Azure 診斷記錄檔 tooan 事件中樞命名空間 |Microsoft 文件"
description: "了解 toostream Azure 診斷記錄 tooan 事件中樞命名空間的方式。"
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
ms.openlocfilehash: 00092ea8f3fe4fa1476e3a697bf1e8645dd21e6e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="stream-azure-diagnostic-logs-tooan-event-hubs-namespace"></a>資料流 Azure 診斷記錄檔 tooan 事件中樞命名空間
**[Azure 診斷的記錄檔](monitoring-overview-of-diagnostic-logs.md)**可以接近即時 tooany 應用程式使用 hello 內建 「 匯出 tooEvent 中心 」 中的選項 hello 入口網站中，資料流中，或藉由啟用 hello 的診斷設定透過 hello Azure PowerShell 中的服務匯流排規則識別碼Cmdlet 或 Azure CLI。

## <a name="what-you-can-do-with-diagnostics-logs-and-event-hubs"></a>您可以使用診斷記錄和事件中樞執行的項目
以下是幾個方法，您可能會使用 hello 串流功能的診斷記錄檔：

* **資料流記錄 too3rd 合作對象記錄與遙測系統**– 一段時間，事件中心資料流將成為 hello 機制 toopipe toothird 合作對象 Siem 中的診斷記錄且記錄分析解決方案。
* **服務健全狀況檢視透過串流處理將 [最忙碌路徑] 資料 tooPowerBI** – 使用事件中心、 Stream Analytics 中，與 power Bi，您可以輕鬆地將 toonear 即時 insights 中的診斷資料轉換在您的 Azure 服務。 [文件本文件提供的絕佳概觀 tooset 向上事件中心使用 Stream Analytics 中，處理資料，以及做為輸出使用 PowerBI](../stream-analytics/stream-analytics-power-bi-dashboard.md)。 以下是設定診斷記錄的一些祕訣︰
  
  * 當您核取 hello 入口網站中的 hello 選項或啟用透過 PowerShell，因此您想 hello 命名空間與 hello 名稱開頭為 tooselect hello 事件中樞時自動建立事件中心的診斷記錄檔分類**insights**.
  * 下列 SQL 程式碼的 hello 是範例資料流分析查詢，您可以使用 tooparse hello 記錄的所有資料 tooa PowerBI 資料表中：

    ```sql
    SELECT
    records.ArrayValue.[Properties you want tootrack]
    INTO
    [OutputSourceName – hello PowerBI source]
    FROM
    [InputSourceName] AS e
    CROSS APPLY GetArrayElements(e.records) AS records
    ```

* **建置自訂的遙測及記錄平台**– 如果您已自訂的遙測平台，或都只考慮的建立一個具有高擴充性 hello 發行-訂閱性質的事件中心可讓您 tooflexibly 內嵌診斷記錄檔。 [請參閱 Dan Rosanova 指南 toousing 事件中心的全球遙測平台中](https://azure.microsoft.com/documentation/videos/build-2015-designing-and-sizing-a-global-scale-telemetry-platform-on-azure-event-Hubs/)。

## <a name="enable-streaming-of-diagnostic-logs"></a>啟用診斷記錄的串流
您可以啟用資料流的診斷記錄檔以程式設計的方式，透過 hello 入口網站，或使用 hello [Azure 監視 REST Api](https://docs.microsoft.com/rest/api/monitor/servicediagnosticsettings)。 無論如何，您建立的診斷設定指定的事件中樞命名空間和 hello 記錄檔分類想 toosend toohello 命名空間中的度量。 事件中心會建立每個您啟用的記錄檔類別目錄的 hello 命名空間中。 診斷**記錄類別**是一種資源可以收集的記錄類型。

> [!WARNING]
> 啟用和串流來自計算資源 (例如，VM 或 Service Fabric) 的診斷記錄 [需要一組不同的步驟](../event-hubs/event-hubs-streaming-azure-diags-data.md)。
> 
> 

服務匯流排 hello 或事件中樞命名空間中沒有 toobe hello 發出記錄檔，只要將設定 hello 設定 hello 使用者擁有適當的 RBAC 存取 tooboth 訂閱 hello 資源相同訂用帳戶。

## <a name="stream-diagnostic-logs-using-hello-portal"></a>資料流使用 hello 入口網站的診斷記錄檔
1. 在 hello 入口網站中，瀏覽 tooAzure 監視器並按一下**診斷設定**

    ![Azure 監視器的監視區段](media/monitoring-stream-diagnostic-logs-to-event-hubs/diagnostic-settings-blade.png)

2. 選擇性地篩選資源群組或資源類型的 hello 清單，然後按一下 hello 資源，您想要 tooset 診斷設定。

3. 如果您選取的 hello 資源上有沒有設定，您必須提示的 toocreate 設定。 按一下「開啟診斷」。

   ![新增診斷設定 - 無現有的設定](media/monitoring-stream-diagnostic-logs-to-event-hubs/diagnostic-settings-none.png)

   如果 hello 資源上的現有設定，您會看到已設定此資源上設定的清單。 按一下「新增診斷設定」。

   ![新增診斷設定 - 現有的設定](media/monitoring-stream-diagnostic-logs-to-event-hubs/diagnostic-settings-multiple.png)

3. 提供設定名稱，並核取方塊 hello**資料流 tooan 事件中心**，然後選取 事件中樞命名空間。
   
   ![新增診斷設定 - 現有的設定](media/monitoring-stream-diagnostic-logs-to-event-hubs/diagnostic-settings-configure.png)
    
   hello 選取命名空間將會建立 （如果這是您第一次資料流診斷記錄） 或資料流處理太 hello 事件中心位置 （如果已經有進行串流處理該記錄檔分類 toothis 命名空間的資源），並 hello 原則定義 hellohello 串流處理機制具有的權限。 現在，事件中心資料流 tooan 需要管理、 傳送和接聽的權限。 您可以建立或修改命名空間的 hello 設定 索引標籤下的 hello 入口網站中的事件中樞命名空間的共用存取原則。 其中一個診斷設定 tooupdate，hello 用戶端必須有 hello ListKey 權限 hello 事件中樞授權規則。

4. 按一下 [儲存] 。

在幾分鐘之後, hello 新設定會出現在此資源，設定的清單，並診斷記錄檔進行串流 toothat 儲存體帳戶，只要產生新的事件資料。

### <a name="via-powershell-cmdlets"></a>透過 PowerShell Cmdlet
hello 透過串流處理 tooenable [Azure PowerShell Cmdlet](insights-powershell-samples.md)，您可以使用 hello`Set-AzureRmDiagnosticSetting`指令程式搭配下列參數：

```powershell
Set-AzureRmDiagnosticSetting -ResourceId [your resource ID] -ServiceBusRuleId [your Service Bus rule ID] -Enabled $true
```

服務匯流排規則識別碼 hello 是這種格式的字串： `{Service Bus resource ID}/authorizationrules/{key name}`，例如`/subscriptions/{subscription ID}/resourceGroups/Default-ServiceBus-WestUS/providers/Microsoft.ServiceBus/namespaces/{Service Bus namespace}/authorizationrules/RootManageSharedAccessKey`。

### <a name="via-azure-cli"></a>透過 Azure CLI
透過 hello 串流 tooenable [Azure CLI](insights-cli-samples.md)，您可以使用 hello`insights diagnostic set`命令如下：

```azurecli
azure insights diagnostic set --resourceId <resourceID> --serviceBusRuleId <serviceBusRuleID> --enabled true
```

使用的 hello 相同格式的服務匯流排規則識別碼 hello PowerShell Cmdlet 的說明。

## <a name="how-do-i-consume-hello-log-data-from-event-hubs"></a>我要如何使用 hello 記錄資料，從事件中心？
此處是來自事件中樞的範例輸出資料：

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

| 元素名稱 | 說明 |
| --- | --- |
| 記錄數 |此承載中的所有記錄事件的陣列。 |
| 分析 |Hello 發生事件的時間。 |
| category |此事件的記錄檔分類。 |
| resourceId |產生這個事件的 hello 資源的資源識別碼。 |
| operationName |Hello 作業的名稱。 |
| 層級 |選用。 表示 hello 記錄事件層級。 |
| 屬性 |Hello 事件的屬性。 |

您可以檢視支援資料流 tooEvent 集線器的所有資源提供者的清單[這裡](monitoring-overview-of-diagnostic-logs.md)。

## <a name="stream-data-from-compute-resources"></a>從計算資源中串流資料
您也可以串流來自使用 hello Windows Azure 診斷代理程式的計算資源的診斷記錄檔。 [請參閱本文章](../event-hubs/event-hubs-streaming-azure-diags-data.md)如何 tooset 該總。

## <a name="next-steps"></a>後續步驟
* [深入了解 Azure 診斷記錄檔](monitoring-overview-of-diagnostic-logs.md)
* [開始使用事件中心](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)

