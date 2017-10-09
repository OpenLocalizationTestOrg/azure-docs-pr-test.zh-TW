---
title: "Operations Management Suite Azure 邏輯應用程式中的 B2B 訊息的 aaaQuery |Microsoft 文件"
description: "在 hello Operations Management Suite 中建立查詢 tootrack AS2，x12 和 EDIFACT 訊息"
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
ms.openlocfilehash: aee6644ff19add8f074ed5f1725db87b1d3b74b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="query-for-as2-x12-and-edifact-messages-in-hello-microsoft-operations-management-suite-oms"></a>As2，x12 和 EDIFACT 訊息 hello Microsoft Operations Management Suite (OMS) 中的查詢

x12，或您追蹤的 EDIFACT 訊息 toofind hello AS2 [Azure Log Analytics](../log-analytics/log-analytics-overview.md)在 hello [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md)，您可以建立篩選器動作，根據特定的查詢準則。 例如，您可以找到根據特定交換控制編號的訊息。

## <a name="requirements"></a>需求

* 已設定診斷記錄的邏輯應用程式。 深入了解[如何 toocreate 邏輯應用程式](../logic-apps/logic-apps-create-a-logic-app.md)和[如何該邏輯應用程式的記錄 tooset](../logic-apps/logic-apps-monitor-your-logic-apps.md#azure-diagnostics)。

* 已設定監視和記錄的整合帳戶。 深入了解[如何 toocreate 整合帳戶](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md)和[如何監視和記錄該帳戶的總 tooset](../logic-apps/logic-apps-monitor-b2b-message.md)。

* 如果您還沒有這麼做，[發行分析的診斷資料 tooLog](../logic-apps/logic-apps-track-b2b-messages-omsportal.md)和[設定郵件追蹤在 OMS 中](../logic-apps/logic-apps-track-b2b-messages-omsportal.md)。

> [!NOTE]
> 您雖然符合 hello 先前的需求之後，您應該有 hello 中的工作區[Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md)。 您應該使用 hello 追蹤您在 OMS 中的 B2B 通訊的同一個 OMS 工作區。 
>  
> 如果您沒有 OMS 工作區，了解[如何 toocreate OMS 工作區](../log-analytics/log-analytics-get-started.md)。

## <a name="create-message-queries-with-filters-in-hello-operations-management-suite-portal"></a>使用 hello Operations Management Suite 入口網站中的篩選器建立訊息查詢

此範例示範如何找到根據其交換控制編號的訊息。

> [!TIP] 
> 如果您知道您的 OMS 工作區名稱，請移至 tooyour 工作區的首頁 (`https://{your-workspace-name}.portal.mms.microsoft.com`)，然後啟動在步驟 4。 否則，請從步驟 1 開始。

1. 在 hello [Azure 入口網站](https://portal.azure.com)，選擇**更服務**。 搜尋 "log analytics"，然後選擇 [Log Analytics]，如下所示：

   ![尋找 Log Analytics](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/browseloganalytics.png)

2. 在 [Log Analytics] 下，尋找並選取 OMS 工作區。

   ![選取 OMS 工作區](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/selectla.png)

3. 在 [管理] 下，選擇 [OMS 入口網站]。

   ![選擇 OMS 入口網站](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/omsportalpage.png)

4. 在 OMS 首頁上，選擇 [記錄搜尋]。

   ![在 OMS 首頁上，選擇 [記錄搜尋]](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/logsearch.png)

   -或-

   ![Hello OMS 功能表上，選擇 [記錄搜尋]](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/logsearch-2.png)

5. 在 hello 搜尋方塊中，輸入您想 toofind，欄位按**Enter**。 當您開始鍵入時，OMS 會顯示您可以使用的可能相符項目和作業。 深入了解[如何 toofind 記錄分析資料](../log-analytics/log-analytics-log-searches.md)。

   此範例會搜尋具有 **Type=AzureDiagnostics** 的事件。

   ![開始鍵入查詢字串](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-start-query.png)

6. 在 hello 左列上，選擇 hello 時間範圍內的 tooview。 tooadd 篩選 tooyour 查詢中，選擇**+ 加**。

   ![新增篩選器 tooquery](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/query1.png)

7. 下**加入篩選**，因此您可以找到您想要的 hello 篩選輸入 hello 篩選器名稱。 選取 hello 篩選，然後選擇  **+ 加**。

   toofind hello 交換控制編號，此範例中搜尋 hello word"交換 」，並選取**event_record_messageProperties_interchangeControlNumber_s**為 hello 篩選條件。

   ![選取篩選](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-query-add-filter.png)

9. 在 hello 左列中，選取 hello 篩選值，您想 toouse，並選擇**套用**。

   這個範例會選取 hello 我們想要的 hello 訊息的交換控制編號。

   ![選取篩選值](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-query-select-filter-value.png)

10. 現在會傳回 toohello 您要建置的查詢。 已使用您所選取的篩選事件和值來更新您的查詢。 現在也會篩選您的先前結果。

    ![傳回篩選的結果與 tooyour 查詢](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-query-filtered-results.png)

<a name="save-oms-query"></a>

## <a name="save-your-query-for-future-use"></a>儲存查詢供日後使用

1. 從您的查詢上 hello**記錄搜尋**頁面上，選擇**儲存**。 提供查詢名稱，並選取分類，然後選擇 [儲存]。

   ![提供查詢名稱和分類](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-query-save.png)

2. tooview 查詢，並選擇**我的最愛**。

   ![選擇 [我的最愛]](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-query-favorites.png)

3. 在下**已儲存的搜尋**，選取您的查詢，好讓您可以檢視 hello 結果。 因此，您可以找到不同的結果，tooupdate hello 查詢編輯 hello 查詢。

   ![選取查詢](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-log-search-find-favorites.png)

## <a name="find-and-run-saved-queries-in-hello-operations-management-suite-portal"></a>尋找並執行已儲存的查詢在 hello Operations Management Suite 入口網站

1. 開啟 OMS 工作區首頁 (`https://{your-workspace-name}.portal.mms.microsoft.com`)，然後選擇 [記錄搜尋]。

   ![在 OMS 首頁上，選擇 [記錄搜尋]](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/logsearch.png)

   -或-

   ![Hello OMS 功能表上，選擇 [記錄搜尋]](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/logsearch-2.png)

2. 在 hello**記錄搜尋**首頁上，選擇 **我的最愛**。

   ![選擇 [我的最愛]](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-log-search-favorites.png)

3. 在下**已儲存的搜尋**，選取您的查詢，好讓您可以檢視 hello 結果。 因此，您可以找到不同的結果，tooupdate hello 查詢編輯 hello 查詢。

   ![選取查詢](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-log-search-find-favorites.png)

## <a name="next-steps"></a>後續步驟

* [AS2 追蹤結構描述](../logic-apps/logic-apps-track-integration-account-as2-tracking-schemas.md)
* [X12 追蹤結構描述](../logic-apps/logic-apps-track-integration-account-x12-tracking-schema.md)
* [自訂追蹤結構描述](../logic-apps/logic-apps-track-integration-account-custom-tracking-schema.md)