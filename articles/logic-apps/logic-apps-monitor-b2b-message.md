---
title: "aaaMonitor B2B 交易並設定記錄-Azure 邏輯應用程式 |Microsoft 文件"
description: "監視 AS2、X12 和 EDIFACT 訊息，並啟動整合帳戶的診斷記錄"
author: padmavc
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: bb7d9432-b697-44db-aa88-bd16ddfad23f
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 07/21/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: a6745ebf41aab331020bfec072f5806711d125bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-set-up-diagnostics-logging-for-b2b-communication-in-integration-accounts"></a>監視和設定整合帳戶中 B2B 通訊的診斷記錄

在您透過整合帳戶設定兩個執行中商務程序或應用程式之間的 B2B 通訊之後，這些實體也可以彼此交換訊息。 tooconfirm 此通訊如預期般運作，您可以設定 AS2，X12、 監視和 EDIFACT 訊息，以及透過 hello 整合帳戶的診斷記錄[Azure Log Analytics](../log-analytics/log-analytics-overview.md)服務。 [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md) 中的這個服務會監視您的雲端和內部部署環境，協助您維護其可用性和效能，同時收集執行階段詳細資料和事件，進行更豐富的偵錯。 您也可以[搭配使用診斷資料與其他服務](#extend-diagnostic-data)，例如 Azure 儲存體和 Azure 事件中樞。

## <a name="requirements"></a>需求

* 已設定診斷記錄的邏輯應用程式。 深入了解[如何該邏輯應用程式的記錄 tooset](../logic-apps/logic-apps-monitor-your-logic-apps.md#azure-diagnostics)。

  > [!NOTE]
  > 您雖然符合此需求之後，您應該有 hello 中的工作區[Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md)。 您應該使用 hello 同一個 OMS 工作區，當您設定為整合帳戶記錄。 如果您沒有 OMS 工作區，了解[如何 toocreate OMS 工作區](../log-analytics/log-analytics-get-started.md)。

* 已連結 tooyour 邏輯應用程式整合帳戶。 深入了解[toocreate 整合與連結 tooyour 邏輯應用程式的帳戶](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md)。

## <a name="turn-on-diagnostics-logging-for-your-integration-account"></a>開啟整合帳戶的診斷記錄

您可以開啟記錄直接從整合帳戶或[hello Azure 監視服務透過](#azure-monitor-service)。 Azure 監視器提供基礎結構層級資料的基本監視。 深入了解 [Azure 監視器](../monitoring-and-diagnostics/monitoring-overview-azure-monitor.md)。

### <a name="turn-on-diagnostics-logging-directly-from-your-integration-account"></a>直接從整合帳戶開啟診斷記錄

1. 在 hello [Azure 入口網站](https://portal.azure.com)、 尋找並選取 integration 帳戶。 在 [監視] 下，選擇 [診斷記錄]，如下所示：

   ![尋找並選取整合帳戶，然後選擇 [診斷記錄]。](media/logic-apps-monitor-b2b-message/integration-account-diagnostics.png)

2. 選取整合帳戶之後，會自動選取下列值的 hello。 如果這些值正確，請選擇 [開啟診斷]。 否則，請選取您想要的 hello 值：

   1. 在下**訂用帳戶**，選取 hello 您整合帳戶所使用的 Azure 訂用帳戶。
   2. 在下**資源群組**，選取您整合帳戶所使用的 hello 資源群組。
   3. 在 [資源類型] 下，選取 [整合帳戶]。 
   4. 在 [資源] 下，選取整合帳戶。 
   5. 選擇 [開啟診斷]。

   ![針對整合帳戶設定診斷](media/logic-apps-monitor-b2b-message/turn-on-diagnostics-integration-account.png)

3. 在 [診斷設定] 的 [狀態] 下，選擇 [開啟]。

   ![開啟 Azure 診斷](media/logic-apps-monitor-b2b-message/turn-on-diagnostics-integration-account-2.png)

4. 現在選取 hello OMS 工作區和資料 toouse 記錄，如下所示：

   1. 選取**傳送 tooLog 分析**。 
   2. 在 [Log Analytics] 下，選擇 [設定]。 
   3. 在下**OMS 工作區**，選取 hello OMS 工作區 toouse 進行記錄。
   4. 在下**記錄**，選取 hello **IntegrationAccountTrackingEvents**類別目錄。
   5. 選擇 [儲存]。

   ![設定記錄分析，讓您可以傳送診斷資料 tooa 記錄檔](media/logic-apps-monitor-b2b-message/send-diagnostics-data-log-analytics-workspace.png)

5. 現在[在 OMS 中設定 B2B 訊息的追蹤](../logic-apps/logic-apps-track-b2b-messages-omsportal.md)。

<a name="azure-monitor-service"></a>

### <a name="turn-on-diagnostics-logging-through-azure-monitor"></a>透過 Azure 監視器開啟診斷記錄

1. 在 hello [Azure 入口網站](https://portal.azure.com)，在 hello Azure 的主功能表，選擇**監視器**，**診斷記錄檔**。 然後選取整合帳戶，如下所示：

   ![依序選擇 [監視器] 和 [診斷記錄]，然後選取整合帳戶](media/logic-apps-monitor-b2b-message/monitor-service-diagnostics-logs.png)

2. 選取整合帳戶之後，會自動選取下列值的 hello。 如果這些值正確，請選擇 [開啟診斷]。 否則，請選取您想要的 hello 值：

   1. 在下**訂用帳戶**，選取 hello 您整合帳戶所使用的 Azure 訂用帳戶。
   2. 在下**資源群組**，選取您整合帳戶所使用的 hello 資源群組。
   3. 在 [資源類型] 下，選取 [整合帳戶]。
   4. 在 [資源] 下，選取整合帳戶。
   5. 選擇 [開啟診斷]。

   ![針對整合帳戶設定診斷](media/logic-apps-monitor-b2b-message/turn-on-diagnostics-integration-account.png)

3. 在 [診斷設定] 下，選擇 [開啟]。

   ![開啟 Azure 診斷](media/logic-apps-monitor-b2b-message/turn-on-diagnostics-integration-account-2.png)

4. 現在選取 hello OMS 工作區和事件類別目錄的記錄，如下所示：

   1. 選取**傳送 tooLog 分析**。 
   2. 在 [Log Analytics] 下，選擇 [設定]。 
   3. 在下**OMS 工作區**，選取 hello OMS 工作區 toouse 進行記錄。
   4. 在下**記錄**，選取 hello **IntegrationAccountTrackingEvents**類別目錄。
   5. 完成之後，請選擇 [儲存]。

   ![設定記錄分析，讓您可以傳送診斷資料 tooa 記錄檔](media/logic-apps-monitor-b2b-message/send-diagnostics-data-log-analytics-workspace.png)

5. 現在[在 OMS 中設定 B2B 訊息的追蹤](../logic-apps/logic-apps-track-b2b-messages-omsportal.md)。

## <a name="extend-how-and-where-you-use-diagnostic-data-with-other-services"></a>延伸搭配使用診斷資料與其他服務的方式和位置

使用 Azure Log Analytics，即可延伸如何搭配使用邏輯應用程式的診斷資料與其他 Azure services，例如： 

* [在 Azure 儲存體中封存 Azure 診斷記錄](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md)
* [資料流 Azure 診斷記錄檔 tooAzure 事件中心](../monitoring-and-diagnostics/monitoring-stream-diagnostic-logs-to-event-hubs.md) 

您可以接著使用其他服務的遙測和分析來取得即時監視，例如 [Azure Stream Analytics](../stream-analytics/stream-analytics-introduction.md) 和 [Power BI](../log-analytics/log-analytics-powerbi.md)。 例如：

* [從事件中心 tooStream 分析的資料流資料](../stream-analytics/stream-analytics-define-inputs.md)
* [使用串流分析分析串流資料並在 Power BI 中建立即時分析儀表板](../stream-analytics/stream-analytics-power-bi-dashboard.md)

根據您想要設定的 hello 選項，請確定您第一次[建立 Azure 儲存體帳戶](../storage/common/storage-create-storage-account.md)或[建立 Azure 事件中樞](../event-hubs/event-hubs-create.md)。 然後選取您想要 toosend 診斷資料的 hello 選項：

![傳送資料 tooAzure 儲存體帳戶或事件中心](./media/logic-apps-monitor-b2b-message/storage-account-event-hubs.png)

> [!NOTE]
> Toouse 您選擇儲存體帳戶時，才會套用保留期限。

## <a name="supported-tracking-schemas"></a>支援的追蹤結構描述

Azure 支援這些追蹤結構描述類型，這些全都已修正除了 hello 自訂類型的結構描述。

* [AS2 追蹤結構描述](../logic-apps/logic-apps-track-integration-account-as2-tracking-schemas.md)
* [X12 追蹤結構描述](../logic-apps/logic-apps-track-integration-account-x12-tracking-schema.md)
* [自訂追蹤結構描述](../logic-apps/logic-apps-track-integration-account-custom-tracking-schema.md)

## <a name="next-steps"></a>後續步驟

* [在 OMS 中追蹤 B2B 訊息](../logic-apps/logic-apps-track-b2b-messages-omsportal.md "在 OMS 中追蹤 B2B 訊息")
* [深入了解 hello Enterprise Integration Pack](../logic-apps/logic-apps-enterprise-integration-overview.md "深入了解 Enterprise Integration Pack")

