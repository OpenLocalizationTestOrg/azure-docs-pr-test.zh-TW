---
title: "Operations Management Suite Azure 邏輯應用程式中的 aaaTrack B2B 訊息 |Microsoft 文件"
description: "使用 Azure Log Analytics 追蹤 Operations Management Suite (OMS) 中整合帳戶和邏輯應用程式的 B2B 通訊"
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
ms.date: 07/21/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: f385a72008b19408bb45d61c440df0505b688175
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="track-b2b-communication-in-hello-microsoft-operations-management-suite-oms"></a>在 hello Microsoft Operations Management Suite (OMS) 中的追蹤 B2B 通訊

在您透過整合帳戶設定兩個執行中商務程序或應用程式之間的 B2B 通訊之後，這些實體也可以彼此交換訊息。 toocheck 是否正確處理這些訊息，您可以追蹤 X12，AS2 和 EDIFACT 訊息與[Azure Log Analytics](../log-analytics/log-analytics-overview.md)在 hello [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md)。 例如，您可以使用這些網頁追蹤功能來追蹤訊息：

* 訊息計數和狀態
* 通知狀態
* 訊息與通知的相互關聯
* 失敗的詳細錯誤描述
* 搜尋功能

## <a name="requirements"></a>需求

* 已設定診斷記錄的邏輯應用程式。 深入了解[如何 toocreate 邏輯應用程式](logic-apps-create-a-logic-app.md)和[如何該邏輯應用程式的記錄 tooset](../logic-apps/logic-apps-monitor-your-logic-apps.md#azure-diagnostics)。

* 已設定監視和記錄的整合帳戶。 深入了解[如何 toocreate 整合帳戶](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md)和[如何監視和記錄該帳戶的總 tooset](../logic-apps/logic-apps-monitor-b2b-message.md)。

* 如果您還沒有這麼做，[發行分析的診斷資料 tooLog](../logic-apps/logic-apps-track-b2b-messages-omsportal.md)在 OMS 中。

> [!NOTE]
> 您雖然符合 hello 先前的需求之後，您應該有 hello 中的工作區[Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md)。 您應該使用 hello 追蹤您在 OMS 中的 B2B 通訊的同一個 OMS 工作區。 
>  
> 如果您沒有 OMS 工作區，了解[如何 toocreate OMS 工作區](../log-analytics/log-analytics-get-started.md)。

## <a name="add-hello-logic-apps-b2b-solution-toohello-operations-management-suite-oms"></a>新增 hello 邏輯應用程式 B2B 解決方案 toohello Operations Management Suite (OMS)

toohave OMS 追蹤 B2B 訊息的應用程式邏輯，您必須新增 hello**邏輯應用程式 B2B**方案 toohello OMS 入口網站。 深入了解[加入解決方案 tooOMS](../log-analytics/log-analytics-get-started.md)。

1. 在 hello [Azure 入口網站](https://portal.azure.com)，選擇**更服務**。 搜尋 "log analytics"，然後選擇 [Log Analytics]，如下所示：

   ![尋找 Log Analytics](media/logic-apps-track-b2b-messages-omsportal/browseloganalytics.png)

2. 在 [Log Analytics] 下，尋找並選取 OMS 工作區。 

   ![選取 OMS 工作區](media/logic-apps-track-b2b-messages-omsportal/selectla.png)

3. 在 [管理] 下，選擇 [OMS 入口網站]。

   ![選擇 OMS 入口網站](media/logic-apps-track-b2b-messages-omsportal/omsportalpage.png)

4. Hello OMS 首頁上開啟之後，請選擇**解決方案資源庫**。    

   ![選取方案庫](media/logic-apps-track-b2b-messages-omsportal/omshomepage1.png)

5. 在 [所有解決方案] 下，尋找並選擇 [Logic Apps B2B]。     

   ![選擇 Logic Apps B2B](media/logic-apps-track-b2b-messages-omsportal/omshomepage2.png)

6. 在 [Logic Apps B2B] 下，選擇 [新增]。

   ![選擇 [新增]](media/logic-apps-track-b2b-messages-omsportal/omshomepage3.png)

   在 hello OMS 首頁上，hello 磚**邏輯應用程式 B2B 訊息**隨即顯示。 
   當處理 B2B 訊息時，此磚會更新 hello 訊息計數。

   ![OMS 首頁、[Logic Apps B2B 訊息] 磚](media/logic-apps-track-b2b-messages-omsportal/omshomepage4.png)

<a name="message-status-details"></a>

## <a name="track-message-status-and-details-in-hello-operations-management-suite"></a>追蹤訊息狀態和 hello Operations Management Suite 中的詳細資料

1. 處理 B2B 訊息之後，您可以檢視 hello 狀態和適用於這些訊息的詳細資料。 在 hello OMS 首頁上，選擇 hello**邏輯應用程式 B2B 訊息**磚。

   ![更新的訊息計數](media/logic-apps-track-b2b-messages-omsportal/omshomepage6.png)

   > [!NOTE]
   > 根據預設，hello**邏輯應用程式 B2B 訊息**磚會顯示一天為基礎的資料。 toochange hello 資料範圍 tooa 不同的間隔中，選擇 hello 頁面頂端的 hello OMS hello 範圍控制項：
   > 
   > ![變更資料範圍](media/logic-apps-track-b2b-messages-omsportal/change-interval.png)
   >

2. 在 hello 訊息狀態儀表板出現之後，您可以檢視特定訊息類型，顯示資料是根據一天的其他詳細資料。 選擇 hello 磚**AS2**， **X12**，或**EDIFACT**。

   ![檢視訊息狀態](media/logic-apps-track-b2b-messages-omsportal/omshomepage5.png)

   會針對您所選擇的磚顯示訊息清單。 
   toolearn 進一步了解 hello 屬性對於每個訊息類型，請參閱這些訊息屬性的描述：

   * [AS2 訊息屬性](#as2-message-properties)
   * [X12 訊息屬性](#x12-message-properties)
   * [EDIFACT 訊息屬性](#EDIFACT-message-properties)

   例如，AS2 訊息清單可能如下：

   ![檢視 AS2 訊息](media/logic-apps-track-b2b-messages-omsportal/as2messagelist.png)

3. 特定訊息，tooview 或匯出的 hello 輸入和輸出選取這些訊息，然後選擇**下載**。 則會提示您，儲存 hello.zip 檔案 tooyour 本機電腦，並解壓縮該檔案。 

   hello 解壓縮的資料夾會包含每個選取之訊息的資料夾。 
   如果您設定通知，hello 訊息資料夾也會包含認可詳細資料的檔案。 
   每個訊息資料夾都會至少有這些檔案： 
   
   * 人類看得懂的檔案，以 hello 輸入及輸出內容承載詳細資料
   * 編碼的檔案具有 hello 輸入和輸出

   對於每個訊息類型，您可以找到 hello 資料夾和檔案名稱格式：

   * [AS2 資料夾和檔案名稱格式](#as2-folder-file-names)
   * [X12 資料夾和檔案名稱格式](#x12-folder-file-names)
   * [EDIFACT 資料夾和檔案名稱格式](#edifact-folder-file-names)

   ![下載訊息檔案](media/logic-apps-track-b2b-messages-omsportal/download-messages.png)

4. tooview hello 相同的所有動作識別碼，在上執行 hello**記錄搜尋**頁面上，從 hello 訊息清單中選擇一則訊息。

   您可以依資料行排序這些動作，或搜尋特定結果。

   ![動作以 hello 相同回合 ID](media/logic-apps-track-b2b-messages-omsportal/logsearch.png)

   * toosearch 預先建立的查詢結果選擇**我的最愛**。

   * 深入了解[toobuild 藉由加入篩選查詢的方式](logic-apps-track-b2b-messages-omsportal-query-filter-control-number.md)。 
   深入了解或者[toofind 資料與記錄檔中記錄分析搜尋的方式](../log-analytics/log-analytics-log-searches.md)。

   * toochange hello 搜尋方塊中，更新 hello 與 hello 資料行和值，您想查詢 toouse 做為篩選的查詢。

<a name="message-list-property-descriptions"></a>

## <a name="property-descriptions-and-name-formats-for-as2-x12-and-edifact-messages"></a>AS2、X12 和 EDIFACT 訊息的屬性描述和名稱格式

對於每個訊息類型，以下是 hello 屬性說明與下載的訊息檔案的名稱格式。

<a name="as2-message-properties"></a>

### <a name="as2-message-property-descriptions"></a>AS2 訊息屬性描述

以下是每個 AS2 訊息的 hello 屬性描述。

| 屬性 | 說明 |
| --- | --- |
| 傳送者 | 中所指定的 hello 來賓夥伴**接收設定**，或在其中指定 hello 主控合作夥伴**傳送設定**AS2 協議 |
| 接收者 | 中所指定的 hello 主機夥伴**接收設定**，或在其中指定 hello 來賓夥伴**傳送設定**AS2 協議 |
| 邏輯應用程式 | hello AS2 動作會設定其中的 hello 邏輯應用程式 |
| 狀態 | hello AS2 訊息狀態 <br>成功 = 已接收或傳送有效的 AS2 訊息。 未設定 MDN。 <br>成功 = 已接收或傳送有效的 AS2 訊息。 已設定並接收 MDN，或傳送 MDN。 <br>失敗 = 已接收無效的 AS2 訊息。 未設定 MDN。 <br>暫止 = 已接收或傳送有效的 AS2 訊息。 已設定 MDN，並預期要有 MDN。 |
| Ack | hello 訊息的 MDN 狀態 <br>接受 = 已接收或傳送正值的 MDN。 <br>Pending = 等待 tooreceive 或傳送 MDN。 <br>拒絕 = 已接收或傳送負值的 MDN。 <br>不需要 = MDN 不會設定在 hello 協議。 |
| 方向 | hello AS2 訊息的方向 |
| 相互關連識別碼 | 相互關聯的所有 hello 觸發程序和動作邏輯應用程式中的 hello 識別碼 |
| 訊息識別碼 | hello AS2 訊息識別碼，從 hello AS2 訊息標頭 |
| Timestamp | hello hello AS2 動作處理 hello 訊息時的時間 |
|          |             |

<a name="as2-folder-file-names"></a>

### <a name="as2-name-formats-for-downloaded-message-files"></a>所下載訊息檔案的 AS2 名稱格式

以下是針對每個下載的 AS2 訊息的資料夾和檔案的 hello 名稱格式。

| 資料夾或檔案 | 名稱格式 |
| :------------- | :---------- |
| 訊息資料夾 | [寄件者]\_[接收者]\_AS2\_[相互關聯識別碼]\_[訊息識別碼]\_[時間戳記] |
| 輸入、輸出和通知檔案 (若已設定) | **輸入承載**：[寄件者]\_[接收者]\_AS2\_[相互關聯識別碼]\_input_payload.txt </p>**輸出承載**：[寄件者]\_[接收者]\_AS2\_[相互關聯識別碼]\_output\_payload.txt </p></p>**輸入**：[寄件者]\_[接收者]\_AS2\_[相互關聯識別碼]\_inputs.txt </p></p>**輸出**：[寄件者]\_[接收者]\_AS2\_[相互關聯識別碼]\_outputs.txt |
|          |             |

<a name="x12-message-properties"></a>

### <a name="x12-message-property-descriptions"></a>X12 訊息屬性描述

以下是每個 X12 的 hello 屬性描述訊息。

| 屬性 | 說明 |
| --- | --- |
| 傳送者 | 中所指定的 hello 來賓夥伴**接收設定**，或在其中指定 hello 主控合作夥伴**傳送設定**x12 協議 |
| 接收者 | 中指定的 hello 主控合作夥伴**接收設定**，或在指定的 hello 來賓夥伴**傳送設定**x12 協議 |
| 邏輯應用程式 | hello X12 動作會設定其中的 hello 邏輯應用程式 |
| 狀態 | hello X12 訊息狀態 <br>成功 = 已接收或傳送有效的 X12 訊息。 未設定任何功能通知。 <br>成功 = 已接收或傳送有效的 X12 訊息。 已設定和接收功能通知，或傳送功能通知。 <br>失敗 = 已接收或傳送有效的 X12 訊息。 <br>暫止 = 已接收或傳送有效的 X12 訊息。 已設定功能通知，並預期要有功能通知。 |
| Ack | 功能認可 (997) 狀態 <br>接受 = 已接收或傳送正值的功能通知。 <br>拒絕 = 已接收或傳送負值的功能通知。 <br>暫止 = 預期要有功能通知但未收到。 <br>暫止的 = 產生功能通知，但無法傳送 toopartner。 <br>不需要 = 未設定功能通知。 |
| 方向 | hello X12 訊息方向 |
| 相互關連識別碼 | 相互關聯的所有 hello 觸發程序和動作邏輯應用程式中的 hello 識別碼 |
| 訊息類型 | hello EDI X 12 訊息類型 |
| ICN | hello X12 訊息的 hello 交換控制編號 |
| TSCN | hello X12 訊息的交易集控制編號 hello |
| Timestamp | hello hello X12 動作處理 hello 訊息時的時間 |
|          |             |

<a name="x12-folder-file-names"></a>

### <a name="x12-name-formats-for-downloaded-message-files"></a>所下載訊息檔案的 X12 名稱格式

以下是 hello 名稱格式，針對每個下載 X12 訊息的資料夾和檔案。

| 資料夾或檔案 | 名稱格式 |
| :------------- | :---------- |
| 訊息資料夾 | [寄件者]\_[接收者]\_X12\_[交換控制編號]\_[通用控制編號]\_[交易集控制編號]\_[時間戳記] |
| 輸入、輸出和通知檔案 (若已設定) | **輸入承載**：[寄件者]\_[接收者]\_X12\_[交換控制編號]\_input_payload.txt </p>**輸出承載**：[寄件者]\_[接收者]\_X12\_[交換控制編號]\_output\_payload.txt </p></p>**輸入**：[寄件者]\_[接收者]\_X12\_[交換控制編號]\_inputs.txt </p></p>**輸出**：[寄件者]\_[接收者]\_X12\_[交換控制編號]\_outputs.txt |
|          |             |

<a name="EDIFACT-message-properties"></a>

### <a name="edifact-message-property-descriptions"></a>EDIFACT 訊息屬性描述

以下是每個 EDIFACT 訊息的 hello 屬性描述。

| 屬性 | 說明 |
| --- | --- |
| 傳送者 | 中所指定的 hello 來賓夥伴**接收設定**，或在其中指定 hello 主控合作夥伴**傳送設定**EDIFACT 協議 |
| 接收者 | 中所指定的 hello 主機夥伴**接收設定**，或在其中指定 hello 來賓夥伴**傳送設定**EDIFACT 協議 |
| 邏輯應用程式 | hello EDIFACT 動作會設定其中的 hello 邏輯應用程式 |
| 狀態 | hello EDIFACT 訊息狀態 <br>成功 = 已接收或傳送有效的 EDIFACT 訊息。 未設定任何功能通知。 <br>成功 = 已接收或傳送有效的 EDIFACT 訊息。 已設定和接收功能通知，或傳送功能通知。 <br>失敗 = 已接收或傳送有效的 EDIFACT 訊息。 <br>暫止 = 已接收或傳送有效的 EDIFACT 訊息。 已設定功能通知，並預期要有功能通知。 |
| Ack | 功能認可 (997) 狀態 <br>接受 = 已接收或傳送正值的功能通知。 <br>拒絕 = 已接收或傳送負值的功能通知。 <br>暫止 = 預期要有功能通知但未收到。 <br>暫止的 = 產生功能通知，但無法傳送 toopartner。 <br>不需要 = 未設定功能通知。 |
| 方向 | hello EDIFACT 訊息方向 |
| 相互關連識別碼 | 相互關聯的所有 hello 觸發程序和動作邏輯應用程式中的 hello 識別碼 |
| 訊息類型 | hello EDIFACT 訊息類型 |
| ICN | hello EDIFACT 訊息的 hello 交換控制編號 |
| TSCN | hello EDIFACT 訊息的交易集控制編號 hello |
| Timestamp | hello hello EDIFACT 動作處理 hello 訊息時的時間 |
|          |               |

<a name="edifact-folder-file-names"></a>

### <a name="edifact-name-formats-for-downloaded-message-files"></a>所下載訊息檔案的 EDIFACT 名稱格式

以下是針對每個下載的 EDIFACT 訊息的資料夾和檔案的 hello 名稱格式。

| 資料夾或檔案 | 名稱格式 |
| :------------- | :---------- |
| 訊息資料夾 | [寄件者]\_[接收者]\_EDIFACT\_[交換控制編號]\_[通用控制編號]\_[交易集控制編號]\_[時間戳記] |
| 輸入、輸出和通知檔案 (若已設定) | **輸入承載**：[寄件者]\_[接收者]\_EDIFACT\_[交換控制編號]\_input_payload.txt </p>**輸出承載**：[寄件者]\_[接收者]\_EDIFACT\_[交換控制編號]\_output\_payload.txt </p></p>**輸入**：[寄件者]\_[接收者]\_EDIFACT\_[交換控制編號]\_inputs.txt </p></p>**輸出**：[寄件者]\_[接收者]\_EDIFACT\_[交換控制編號]\_outputs.txt |
|          |             |

## <a name="next-steps"></a>後續步驟

* [在 Operations Management Suite 中查詢 B2B 訊息](../logic-apps/logic-apps-track-b2b-messages-omsportal-query-filter-control-number.md)
* [AS2 追蹤結構描述](../logic-apps/logic-apps-track-integration-account-as2-tracking-schemas.md)
* [X12 追蹤結構描述](../logic-apps/logic-apps-track-integration-account-x12-tracking-schema.md)
* [自訂追蹤結構描述](../logic-apps/logic-apps-track-integration-account-custom-tracking-schema.md)