---
title: "在 OMS 記錄分析 aaaResponses tooalerts |Microsoft 文件"
description: "警示記錄分析中的識別您的 OMS 儲存機制中的重要資訊和可以主動通知您的問題或叫用動作 tooattempt toocorrect 它們。  本文說明如何 toocreate 警示的規則和詳細資料 hello 不同動作才會。"
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 6cfd2a46-b6a2-4f79-a67b-08ce488f9a91
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/28/2017
ms.author: bwren
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d24bb726a96e7143985f111c0599dc4e7898b4f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="add-actions-tooalert-rules-in-log-analytics"></a>在 記錄分析中加入動作 tooalert 規則
當[警示會在記錄分析](log-analytics-alerts.md)，您可以在 hello 選擇[設定 hello 警示規則](log-analytics-alerts.md)tooperform 一或多個動作。  本文說明 hello 可用的不同動作及詳細資料，設定每個類型。

| 動作 | 說明 |
|:--|:--|
| [電子郵件](#email-actions) | 傳送電子郵件與 hello 的 hello 警示 tooone 或多個收件者的詳細資料。 |
| [Webhook](#webhook-actions) | 透過單一 HTTP POST 要求叫用外部處理序。 |
| [Runbook](#runbook-actions) | 在 Azure 自動化中啟動 Runbook。 |


## <a name="email-actions"></a>電子郵件動作
電子郵件動作會傳送 hello 的 hello 警示 tooone 或多個收件者的詳細資料的電子郵件。  您可以指定 hello 的 hello 郵件的主旨，但它的內容記錄分析所建構的標準格式。  中的 hello 記錄搜尋所傳回的 tooten 記錄的加法 toodetails 包含例如 hello 名稱的 hello 警示的摘要資訊。  它也包含連結 tooa 記錄搜尋記錄分析會從該查詢傳回 hello 整組記錄中。   hello 寄件者的 hello 郵件是*Microsoft Operations Management Suite Team &lt; noreply@oms.microsoft.com &gt;* 。 

電子郵件動作需要 hello 下表中的 hello 屬性。

| 屬性 | 說明 |
|:--- |:--- |
| 主旨 |Hello 電子郵件的主旨。  您無法修改 hello 郵件 hello 主體。 |
| 收件者 |所有電子郵件收件者的地址。  如果您指定一個以上的地址，然後個別 hello 位址以分號 （;）。 |


## <a name="webhook-actions"></a>Webhook 動作

Webhook 動作可讓您 tooinvoke 外部處理序，透過單一的 HTTP POST 要求。  呼叫 hello 服務應支援 webhook，並判斷將如何使用任何裝載接收。  您也可以呼叫 REST API，只要 hello 要求的格式 API 了解該 hello 特別不支援 webhook。  使用 webhook 回應 tooan 警示中的範例會傳送訊息[Slack](http://slack.com)或建立事件[PagerDuty](http://pagerduty.com/)。  與 Slack 的 webhook toocall 建立警示規則的完整逐步解說將會位於[記錄分析警示中的 Webhook](log-analytics-alerts-webhooks.md)。

Webhook 動作需要 hello 下表中的 hello 屬性。

| 屬性 | 說明 |
|:--- |:--- |
| Webhook URL |hello hello webhook URL。 |
| 自訂 JSON 承載 |自訂承載 toosend 與 hello webhook。  如需詳細資料，請參閱下文。 |


Webhook 包含 URL，並且在 hello 資料的 JSON 中格式化的承載傳送 toohello 外部服務。  根據預設，hello 裝載會將包含下表中的 hello hello 值。  您可以選擇 tooreplace 自訂您自己的其中一個使用此內容。  在此情況下您可以使用 hello 資料表中的 hello 變數每 hello 參數 tooinclude 其值在您的自訂承載。

| 參數 | 變數 | 說明 |
|:--- |:--- |:--- |
| AlertRuleName |#alertrulename |Hello 警示規則的名稱。 |
| AlertThresholdOperator |#thresholdoperator |Hello 警示規則的臨界值運算子。  大於或等於。 |
| AlertThresholdValue |#thresholdvalue |Hello 警示規則的臨界值。 |
| LinkToSearchResults |#linktosearchresults |連結 tooLog 分析記錄搜尋，傳回從建立 hello 警示的 hello 查詢 hello 記錄。 |
| ResultCount |#searchresultcount |Hello 搜尋結果中的記錄數目。 |
| SearchIntervalEndtimeUtc |#searchintervalendtimeutc |以 UTC 格式 hello 查詢的結束時間。 |
| SearchIntervalInSeconds |#searchinterval |Hello 警示規則的時間間隔。 |
| SearchIntervalStartTimeUtc |#searchintervalstarttimeutc |啟動 hello 查詢時間以 UTC 格式。 |
| SearchQuery |#searchquery |Hello 警示規則所用的記錄搜尋查詢。 |
| SearchResults |請參閱下方 |JSON 格式中的 hello 查詢所傳回的記錄。  有限的 toohello 5000 第一次記錄。 |
| WorkspaceID |#workspaceid |OMS 工作區的識別碼。 |

例如，您可以指定下列自訂承載包含單一參數來呼叫 hello*文字*。  此 webhook 呼叫 hello 服務會需要此參數。

    {
        "text":"#alertrulename fired with #searchresultcount over threshold of #thresholdvalue."
    }

這個範例裝載會解析 toosomething 像 hello 遵循時傳送 toohello webhook。

    {
        "text":"My Alert Rule fired with 18 records over threshold of 10 ."
    }

tooinclude 搜尋結果中自訂內容，新增以下為最上層屬性 hello json 承載中的 hello。  

    "IncludeSearchResults":true

例如，toocreate 包含只 hello 警示的名稱和 hello 搜尋結果的自訂內容，您可以使用下列的 hello。 

    {
       "alertname":"#alertrulename",
       "IncludeSearchResults":true
    }


您可以逐步完成使用 webhook toostart 外部服務在建立警示規則的完整範例[OMS 記錄分析 toosend 訊息 tooSlack 中建立警示的 webhook 動作](log-analytics-alerts-webhooks.md)。

## <a name="runbook-actions"></a>Runbook 動作
Runbook 動作可在 Azure 自動化中啟動 Runbook。  若要 toouse 這種類型的動作，您必須具有 hello[自動化解決方案](log-analytics-add-solutions.md)OMS 工作區中安裝並設定。  您可以選取從您設定在 hello 自動化解決方案中的 hello 自動化帳戶中的 hello runbook。

Runbook 動作需要 hello 下表中的 hello 屬性。

| 屬性 | 說明 |
|:--- |:---|
| Runbook | 建立警示時，想要 toostart 的 Runbook。 |
| 執行位置 | 指定**Azure** toorun hello runbook hello 雲端中的。  指定**Hybrid worker** toorun hello runbook 上的代理程式[Hybrid Runbook Worker](../automation/automation-hybrid-runbook-worker.md )安裝。  |

Hello runbook 使用的 Runbook 動作啟動[webhook](../automation/automation-webhooks.md)。  當您建立 hello 警示規則時，就會自動以 hello 名稱建立新的 webhook hello runbook **OMS 警示補救**後面跟著 GUID。  

您無法直接填入 hello runbook 的任何參數，但是 hello [$WebhookData 參數](../automation/automation-webhooks.md)將包含 hello hello 警示，包括 hello hello 建立它的記錄搜尋結果的詳細資料。  hello runbook 將需要 toodefine **$WebhookData**做為其參數 tooaccess hello hello 警示的內容。  hello 警示資料可在呼叫的單一屬性的 json 格式**SearchResults**在 hello **RequestBody**屬性**$WebhookData**。  這會有與 hello 下表中的 hello 屬性。

| 節點 | 說明 |
|:--- |:--- |
| id |路徑和 hello 搜尋的 GUID。 |
| __metadata |Hello 警示包括 hello 數目的記錄和狀態的 hello 搜尋結果的相關資訊。 |
| value |Hello 搜尋結果中的每一筆記錄的個別項目。  hello 屬性和 hello 記錄的值，會比對 hello 項目的 hello 詳細資料。 |

比方說，hello 下列 runbook 會擷取 hello hello 記錄搜尋所傳回的記錄，並指派不同的屬性，根據每一筆記錄的 hello 類型。  請注意該 hello runbook 啟動轉換**RequestBody**從 json，因此它可以當作 PowerShell 中的物件。

    param ( 
        [object]$WebhookData
    )

    $RequestBody = ConvertFrom-JSON -InputObject $WebhookData.RequestBody
    $Records     = $RequestBody.SearchResults.value

    foreach ($Record in $Records)
    {
        $Computer = $Record.Computer

        if ($Record.Type -eq 'Event')
        {
            $EventNo    = $Record.EventID
            $EventLevel = $Record.EventLevelName
            $EventData  = $Record.EventData
        }

        if ($Record.Type -eq 'Perf')
        {
            $Object    = $Record.ObjectName
            $Counter   = $Record.CounterName
            $Instance  = $Record.InstanceName
            $Value     = $Record.CounterValue
        }
    }


## <a name="next-steps"></a>後續步驟
- 完成 [設定 Webook](log-analytics-alerts-webhooks.md) 和警示規則的逐步解說。  
- 深入了解如何 toowrite [Azure 自動化中的 runbook](https://azure.microsoft.com/documentation/services/automation) tooremediate 警示所識別的問題。
