---
title: "aaaCheck 狀態設定記錄，並取得警示-Azure 邏輯應用程式 |Microsoft 文件"
description: "監視邏輯應用程式的狀態和效能、記錄診斷資料，並設定警示"
author: jeffhollan
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: 5c1b1e15-3b6c-49dc-98a6-bdbe7cb75339
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 07/21/2017
ms.author: LADocs; jehollan
ms.openlocfilehash: 81f186e11a669b710f4c06089597eb5a76f7a44e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-status-set-up-diagnostics-logging-and-turn-on-alerts-for-azure-logic-apps"></a>監視狀態、設定診斷記錄，以及開啟 Azure Logic Apps 的警示

在您[建立和執行邏輯應用程式](../logic-apps/logic-apps-create-a-logic-app.md)之後，即可檢查其執行歷程記錄、觸發程式歷程記錄、狀態和效能。 針對即時事件監視和更豐富的偵錯，設定邏輯應用程式的[診斷記錄](#azure-diagnostics)。 因此，您可以[尋找並檢視事件](#find-events)，例如觸發程序事件、執行事件和動作事件。 您也可以[搭配使用此診斷資料與其他服務](#extend-diagnostic-data)，例如 Azure 儲存體和 Azure 事件中樞。 

tooget 通知失敗或其他可能的問題，設定[警示](#add-azure-alerts)。 例如，您可以建立警示來偵測「一小時有五個以上的執行失敗時」。 您也可以使用 [Azure 診斷事件設定和內容](#diagnostic-event-properties)，透過程式設計方式設定監視、追蹤和記錄。

## <a name="view-runs-and-trigger-history-for-your-logic-app"></a>檢視邏輯應用程式的執行和觸發程序歷程記錄

1. toofind hello 中的應用程式邏輯[Azure 入口網站](https://portal.azure.com)，在 hello Azure 的主功能表，選擇**更多服務**。 Hello 搜尋方塊中，尋找 「 邏輯應用程式 」，然後選擇**Logic apps**。

   ![尋找邏輯應用程式](./media/logic-apps-monitor-your-logic-apps/find-your-logic-app.png)

   hello Azure 入口網站會顯示所有 hello 邏輯應用程式與您 Azure 訂用帳戶相關聯。 

2. 選取邏輯應用程式，然後選擇 [概觀]。

   hello Azure 入口網站會顯示 hello 執行歷程記錄，以及觸發程序邏輯應用程式記錄。 例如：

   ![邏輯應用程式執行歷程記錄和觸發程序歷程記錄](media/logic-apps-monitor-your-logic-apps/overview.png)

   * **執行歷程記錄**顯示所有 hello 執行邏輯應用程式。 
   * **觸發程序記錄**顯示所有 hello 觸發程序活動邏輯應用程式。

   如需狀態描述，請參閱[針對邏輯應用程式進行疑難排解](../logic-apps/logic-apps-diagnosing-failures.md)。

   > [!TIP]
   > 如果找不到預期 hello 工具列的 hello 資料選擇**重新整理**。

3. tooview hello 底下步驟特定執行中，從**執行歷程記錄**，選取執行。 

   hello 監視器檢視顯示每個步驟中執行。 例如：

   ![特定執行的動作](media/logic-apps-monitor-your-logic-apps/monitor-view-updated.png)

4. tooget 詳細 hello 執行，請選擇**執行詳細資料**。 這項資訊摘要說明 hello 步驟、 狀態、 輸入，並執行 hello 的輸出。 

   ![選擇 [執行詳細資料]](media/logic-apps-monitor-your-logic-apps/run-details.png)

   例如，您可以取得 hello 回合的**相互關聯識別碼**，您可能需要當您使用 hello [Logic apps REST API](https://docs.microsoft.com/rest/api/logic)。

5. tooget 詳細特定的步驟中，選擇該步驟。 您現在可以檢閱詳細資料，例如輸入、輸出以及該步驟所發生的任何錯誤。 例如：

   ![步驟詳細資料](media/logic-apps-monitor-your-logic-apps/monitor-view-details.png)
   
   > [!NOTE]
   > Hello Logic Apps 服務內加密的所有執行階段詳細資料與事件。 只有當使用者要求 tooview 該資料解密。 您也可以控制與存取 toothese 事件[所有存取控制 (RBAC)](../active-directory/role-based-access-control-what-is.md)。

6. tooget 事件的詳細特定觸發程序，請返回 toohello**概觀**窗格。 在下**觸發記錄**，選取 hello 觸發程序事件。 您現在可以檢閱輸入和輸出這類詳細資料，例如：

   ![觸發程序事件輸出詳細資料](media/logic-apps-monitor-your-logic-apps/trigger-details.png)

<a name="azure-diagnostics"></a>

## <a name="turn-on-diagnostics-logging-for-your-logic-app"></a>開啟邏輯應用程式的診斷記錄

如需使用執行階段詳細資料和事件進行更豐富的偵錯，您可以使用 [Azure Log Analytics](../log-analytics/log-analytics-overview.md) 設定診斷記錄。 記錄分析是中的服務[Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md)中監視您的雲端和內部部署環境 toohelp 您維護其可用性和效能。 

開始之前，您會需要 toohave OMS 工作區。 深入了解[如何 toocreate OMS 工作區](../log-analytics/log-analytics-get-started.md)。

1. 在 hello [Azure 入口網站](https://portal.azure.com)、 尋找並選取邏輯應用程式。 

2. 在 [hello 邏輯應用程式] 刀鋒視窗功能表上底下**監視**，選擇**診斷** > **診斷設定**。

   ![移 tooMonitoring，診斷，診斷設定](media/logic-apps-monitor-your-logic-apps/logic-app-diagnostics.png)

3. 在 [診斷設定] 下，選擇 [開啟]。

   ![開啟診斷記錄](media/logic-apps-monitor-your-logic-apps/turn-on-diagnostics-logic-app.png)

4. 現在選取 hello OMS 工作區和事件類別目錄的記錄，如下所示：

   1. 選取**傳送 tooLog 分析**。 
   2. 在 [Log Analytics] 下，選擇 [設定]。 
   3. 在下**OMS 工作區**，選取 hello OMS 工作區 toouse 進行記錄。
   4. 在下**記錄**，選取 hello **WorkflowRuntime**類別目錄。
   5. 選擇 hello 度量的間隔。
   6. 完成之後，請選擇 [儲存]。

   ![選取用於記錄的 OMS 工作區和資料](media/logic-apps-monitor-your-logic-apps/send-diagnostics-data-log-analytics-workspace.png)

現在，您可以尋找事件，以及觸發程序事件、執行事件和動作事件的其他資料。

<a name="find-events"></a>

## <a name="find-events-and-data-for-your-logic-app"></a>尋找邏輯應用程式的事件和資料

應用程式中的邏輯，例如觸發程序事件，執行事件，以及動作事件，請遵循下列步驟 toofind 並檢視事件。

1. 在 hello [Azure 入口網站](https://portal.azure.com)，選擇**更服務**。 搜尋 "log analytics"，然後選擇 [Log Analytics]，如下所示：

   ![選擇 [Log Analytics]](media/logic-apps-monitor-your-logic-apps/browseloganalytics.png)

2. 在 [Log Analytics] 下，尋找並選取 OMS 工作區。 

   ![選取 OMS 工作區](media/logic-apps-monitor-your-logic-apps/selectla.png)

3. 在 [管理] 下，選擇 [OMS 入口網站]。

   ![選擇 [OMS 入口網站]](media/logic-apps-monitor-your-logic-apps/omsportalpage.png)

4. 在 OMS 首頁上，選擇 [記錄搜尋]。

   ![在 OMS 首頁上，選擇 [記錄搜尋]](media/logic-apps-monitor-your-logic-apps/logsearch.png)

   -或-

   ![Hello OMS 功能表上，選擇 [記錄搜尋]](media/logic-apps-monitor-your-logic-apps/logsearch-2.png)

5. 在 hello 搜尋方塊中，指定您想 toofind，欄位按**Enter**。 當您開始鍵入時，OMS 會顯示您可以使用的可能相符項目和作業。 

   例如，toofind hello 前 10 個事件發生時，輸入，並選取這個搜尋查詢：**類別 = WorkflowRuntime | 前 10 個**

   ![輸入搜尋字串](media/logic-apps-monitor-your-logic-apps/oms-start-query.png)

   深入了解[如何 toofind 記錄分析資料](../log-analytics/log-analytics-log-searches.md)。

6. 在 [hello 結果] 頁面上，hello 左工具列，選擇 hello 時間範圍內的 tooview。
toorefine 所新增的篩選器，查詢選擇**+ 加**。

   ![選擇查詢結果的時間範圍](media/logic-apps-monitor-your-logic-apps/query-results.png)

7. 下**加入篩選**，因此您可以找到您想要的 hello 篩選輸入 hello 篩選器名稱。 選取 hello 篩選，然後選擇  **+ 加**。

   這個範例會使用 hello word 「 狀態 」 toofind 失敗事件**AzureDiagnostics**。
   這裡 hello 篩選**status_s**已選取。

   ![選取篩選](media/logic-apps-monitor-your-logic-apps/log-search-add-filter.png)

8. 在 hello 左列中，選取 hello 篩選值，您想 toouse，並選擇**套用**。

   ![選取篩選值，然後選擇 [套用]](media/logic-apps-monitor-your-logic-apps/log-search-apply-filter.png)

9. 現在會傳回 toohello 您要建置的查詢。 使用您所選取的篩選和值來更新您的查詢。 現在也會篩選您的先前結果。

   ![傳回篩選的結果與 tooyour 查詢](media/logic-apps-monitor-your-logic-apps/log-search-query-filtered-results.png)

10. toosave 您查詢供未來使用，請選擇 **儲存**。 深入了解[如何 toosave 查詢](../logic-apps/logic-apps-track-b2b-messages-omsportal-query-filter-control-number.md#save-oms-query)。

<a name="extend-diagnostic-data"></a>

## <a name="extend-how-and-where-you-use-diagnostic-data-with-other-services"></a>延伸搭配使用診斷資料與其他服務的方式和位置

使用 Azure Log Analytics，即可延伸如何搭配使用邏輯應用程式的診斷資料與其他 Azure services，例如： 

* [在 Azure 儲存體中封存 Azure 診斷記錄](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md)
* [資料流 Azure 診斷記錄檔 tooAzure 事件中心](../monitoring-and-diagnostics/monitoring-stream-diagnostic-logs-to-event-hubs.md) 

您可以接著使用其他服務的遙測和分析來取得即時監視，例如 [Azure Stream Analytics](../stream-analytics/stream-analytics-introduction.md) 和 [Power BI](../log-analytics/log-analytics-powerbi.md)。 例如：

* [從事件中心 tooStream 分析的資料流資料](../stream-analytics/stream-analytics-define-inputs.md)
* [使用串流分析分析串流資料並在 Power BI 中建立即時分析儀表板](../stream-analytics/stream-analytics-power-bi-dashboard.md)

根據您想要設定的 hello 選項，請確定您第一次[建立 Azure 儲存體帳戶](../storage/common/storage-create-storage-account.md)或[建立 Azure 事件中樞](../event-hubs/event-hubs-create.md)。 然後選取您想要 toosend 診斷資料的 hello 選項：

![傳送資料 tooAzure 儲存體帳戶或事件中心](./media/logic-apps-monitor-your-logic-apps/storage-account-event-hubs.png)

> [!NOTE]
> Toouse 您選擇儲存體帳戶時，才會套用保留期限。

<a name="add-azure-alerts"></a>

## <a name="set-up-alerts-for-your-logic-app"></a>設定邏輯應用程式的警示

toomonitor 特定的衡量標準或邏輯應用程式中，已超過臨界值設定[在 Azure 中的警示](../monitoring-and-diagnostics/monitoring-overview-alerts.md)。 了解 [Azure 中的計量](../monitoring-and-diagnostics/monitoring-overview-metrics.md)。 

tooset 向上沒有警示[Azure Log Analytics](../log-analytics/log-analytics-overview.md)，請遵循下列步驟。 如需更進階的警示準則和動作，也請[設定 Log Analytics](#azure-diagnostics)。

1. 在 [hello 邏輯應用程式] 刀鋒視窗功能表上底下**監視**，選擇**診斷** > **警示規則** > **新增警示**如下所示：

   ![新增邏輯應用程式的警示](media/logic-apps-monitor-your-logic-apps/set-up-alerts.png)

2. 在 hello**加入警示規則**刀鋒視窗中，建立您的警示所示：

   1. 在 [資源] 下，選取尚未選取的邏輯應用程式。 
   2. 提供警示的名稱和描述。
   3. 選取**度量**或想要 tootrack 事件。
   4. 選取**條件**，指定**閾值**hello 度量，以及選取 hello**期間**監視此度量。
   5. 選取是否 toosend 郵件 hello 警示。 
   6. 指定用於傳送嗨警示的其他電子郵件地址。 
   您也可以指定您想要 toosend hello 警示的 webhook URL。

   例如，一小時有五個以上的執行失敗時，此規則會傳送警示：

   ![建立計量警示規則](media/logic-apps-monitor-your-logic-apps/create-alert-rule.png)

> [!TIP]
> toorun 邏輯應用程式警示，您可以包含 hello[要求觸發程序](../connectors/connectors-native-reqres.md)在工作流程，可讓您執行工作，如這些範例：
> 
> * [Post tooSlack](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-slack-with-logic-app)
> * [傳送文字](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-text-message-with-logic-app)
> * [新增訊息 tooa 佇列](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-queue-with-logic-app)

<a name="diagnostic-event-properties"></a>

## <a name="azure-diagnostics-event-settings-and-details"></a>Azure 診斷事件設定和詳細資料

每個診斷事件的應用程式邏輯和事件，例如 hello 狀態詳細資料，開始時間、 結束時間等等。 tooprogrammatically 設定監視、 追蹤和記錄，您可以使用這些詳細資料以 hello [Azure 邏輯應用程式的 REST API](https://docs.microsoft.com/rest/api/logic)和 hello [Azure 診斷的 REST API](../monitoring-and-diagnostics/monitoring-supported-metrics.md#microsoftlogicworkflows)。

比方說，hello`ActionCompleted`事件有 hello`clientTrackingId`和`trackedProperties`屬性，您可以使用追蹤和監視：

``` json
{
    "time": "2016-07-09T17:09:54.4773148Z",
    "workflowId": "/SUBSCRIPTIONS/<subscription-ID>/RESOURCEGROUPS/MYRESOURCEGROUP/PROVIDERS/MICROSOFT.LOGIC/WORKFLOWS/MYLOGICAPP",
    "resourceId": "/SUBSCRIPTIONS/<subscription-ID>/RESOURCEGROUPS/MYRESOURCEGROUP/PROVIDERS/MICROSOFT.LOGIC/WORKFLOWS/MYLOGICAPP/RUNS/08587361146922712057/ACTIONS/HTTP",
    "category": "WorkflowRuntime",
    "level": "Information",
    "operationName": "Microsoft.Logic/workflows/workflowActionCompleted",
    "properties": {
        "$schema": "2016-06-01",
        "startTime": "2016-07-09T17:09:53.4336305Z",
        "endTime": "2016-07-09T17:09:53.5430281Z",
        "status": "Succeeded",
        "code": "OK",
        "resource": {
            "subscriptionId": "<subscription-ID>",
            "resourceGroupName": "MyResourceGroup",
            "workflowId": "cff00d5458f944d5a766f2f9ad142553",
            "workflowName": "MyLogicApp",
            "runId": "08587361146922712057",
            "location": "westus",
            "actionName": "Http"
        },
        "correlation": {
            "actionTrackingId": "e1931543-906d-4d1d-baed-dee72ddf1047",
            "clientTrackingId": "<my-custom-tracking-ID>"
        },
        "trackedProperties": {
            "myTrackedProperty": "<value>"
        }
    }
}
```

* `clientTrackingId`： 如果未提供 Azure 自動產生這個識別碼，並將事件相互關聯之間執行邏輯應用程式，包括任何巢狀工作流程，會從呼叫 hello 邏輯應用程式。 您可以手動指定此識別碼，從觸發程序藉由傳遞`x-ms-client-tracking-id`hello 觸發程序要求在您自訂 ID 值的標頭。 您可以使用要求觸發程序、HTTP 觸發程序或 Webhook 觸發程序。

* `trackedProperties`: tootrack 輸入或輸出中診斷資料，您可以加入追蹤的屬性 tooactions 邏輯應用程式的 JSON 定義中。 追蹤的屬性可以追蹤僅以單一動作的輸入和輸出，但您可以使用 hello`correlation`事件 toocorrelate 跨中執行的動作的屬性。

  tootrack 一或多個屬性，新增 hello`trackedProperties`區段和 hello 想 toohello 動作定義的屬性。 例如，假設您要 tootrack 資料，例如 「 訂單識別碼 」 您遙測中：

  ``` json
  "myAction": {
    "type": "http",
    "inputs": {
        "uri": "http://uri",
        "headers": {
            "Content-Type": "application/json"
        },
        "body": "@triggerBody()"
    },
    "trackedProperties": {
        "myActionHTTPStatusCode": "@action()['outputs']['statusCode']",
        "myActionHTTPValue": "@action()['outputs']['body']['<content>']",
        "transactionId": "@action()['inputs']['body']['<content>']"
    }
  }
  ```

## <a name="next-steps"></a>後續步驟

* [建立範本以進行邏輯應用程式部署和發行管理](../logic-apps/logic-apps-create-deploy-template.md)
* [B2B 案例搭配企業整合套件](../logic-apps/logic-apps-enterprise-integration-overview.md)
* [監視 B2B 訊息](../logic-apps/logic-apps-monitor-b2b-message.md)