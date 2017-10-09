---
title: "在 OMS 記錄分析 aaaWebhook 警示動作範例 |Microsoft 文件"
description: "其中一個 hello 動作，您可以在記錄分析警示會回應 tooa 執行 * webhook *，可讓您 tooinvoke 外部處理序，透過單一 HTTP 要求。 本文透過一個範例練習在 Log Analytics 中利用 Slack 建立 webhook 動作。"
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 13c39f0f-fd3c-472d-8324-ddf7538be45e
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/27/2017
ms.author: bwren
ms.openlocfilehash: e60bdc4922347073d572c2e4719461b13e8e7d1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-alert-webhook-action-in-oms-log-analytics-toosend-message-tooslack"></a>在 OMS 記錄分析 toosend 訊息 tooSlack 中建立警示的 webhook 動作
其中一個 hello 動作，您可以在回應 tooa 執行[記錄分析警示](log-analytics-alerts.md)是*webhook*，可讓您 tooinvoke 外部處理序，透過單一 HTTP 要求。  您可以在 [Log Analytics 中的警示](log-analytics-alerts.md)

在本文中，我們將透過一個範例，練習在 Log Analytics 中利用 Slack (訊息服務) 建立 webhook 動作。

> [!NOTE]
> 您必須擁有 Slack 帳戶 toocomplete 此範例。  您可以在 [slack.com](http://slack.com)註冊免費帳戶。
> 
> 

## <a name="step-1---enable-webhooks-in-slack"></a>步驟 1 - 在 Slack 中啟用 webhook
1. 登入在 tooSlack [slack.com](http://slack.com)。
2. 選取通道在 hello**通道**hello 左窗格中的區段。  這是 hello 通道 hello 訊息將傳送至。  您可以選取其中一個 hello 預設頻道例如**一般**或**隨機**。  在實際執行案例中，您很有可能會建立特殊通道，例如 **criticalservicealerts**。 <br>
   
   ![Slack channels](media/log-analytics-alerts-webhooks/oms-webhooks01.png)
3. 按一下**新增的應用程式或自訂整合**tooopen hello 應用程式目錄。
4. 型別*webhook* hello [搜尋] 方塊，然後選取成**傳入 Webhook**。 <br>
   
   ![Slack channels](media/log-analytics-alerts-webhooks/oms-webhooks02.png)
5. 按一下**安裝**下一個 tooyour 小組名稱。
6. 按一下 [加入組態] 。
7. 您正要 toouse 如這個範例中，然後再按一下，選取 hello hello 通道**新增連入的 Webhook 整合**。  
8. 複製 hello **Webhook URL**。  您將會貼入這 hello 警示設定。 <br>
   
    ![Slack channels](media/log-analytics-alerts-webhooks/oms-webhooks05.png)

## <a name="step-2---create-alert-rule-in-log-analytics"></a>步驟 2 - 在 Log Analytics 中建立警示規則
1. [建立警示規則](log-analytics-alerts.md)以 hello 下列設定。
   * 查詢： ```    Type=Event EventLevelName=error ```
   * 檢查此警示的間隔︰5 分鐘
   * 結果的 hello 數目是： 大於 10
   * 在此時間範圍內︰60 分鐘
   * 選取**是**如**Webhook**和**否**的 hello 其他動作。
2. 貼上的 hello Slack URL 到 hello **Webhook URL**欄位。
3. 選取 hello 選項太**包括自訂 JSON 承載**。
4. Slack 需要有 JSON 格式化並加上參數 *text* 的承載。  這是它會顯示，它會建立 hello 訊息中的 hello 文字。  您可以使用一或多個 hello 警示參數使用 hello  *#* 符號例如如 hello 下列範例所示。
   
    ```
    {
    "text":"#alertrulename fired with #searchresultcount records which exceeds hello over threshold of #thresholdvalue ."
    }
    ```
   
    ![example JSON payload](media/log-analytics-alerts-webhooks/oms-webhooks07.png)
5. 按一下**儲存**toosave hello 警示規則。
6. 等候建立警示 toobe 有足夠的時間，然後檢查的訊息，將會類似 toohello 下列 Slack。
   
   ![example webhook in Slack](media/log-analytics-alerts-webhooks/oms-webhooks08.png)

### <a name="advanced-webhook-payload-for-slack"></a>Slack 的進階 webhook 承載
您可以使用 Slack 來廣泛自訂傳入訊息。 如需詳細資訊，請參閱[傳入 Webhook](https://api.slack.com/incoming-webhooks) hello Slack 網站上。 以下是更複雜的裝載 toocreate 豐富的訊息格式：

    {
        "attachments": [
            {
                "title":"OMS Alerts Custom Payload",
                "fields": [
                    {
                        "title": "Alert Rule Name",
                        "value": "#alertrulename"},
                    {
                        "title": "Link tooSearchResults",
                        "value": "<#linktosearchresults|OMS Search Results>"},
                    {
                        "title": "Search Interval",
                        "value": "#searchinterval"},
                    {
                        "title": "Threshold Operator",
                        "value": "#thresholdoperator"},
                    {
                        "title": "Threshold Value",
                        "value": "#thresholdvalue"}
                ],
                "color": "#F35A00"
            }
        ]
    }


這會在 Slack 類似 toohello 下列來產生一則訊息。

![example message in Slack](media/log-analytics-alerts-webhooks/oms-webhooks09.png)

## <a name="summary"></a>摘要
就地此警示規則，您必須傳送訊息 tooSlack 每次符合 hello 準則。  

這是動作的只有一個執行，您可以建立回應 tooan 警示中的範例。  Mail tooyourself 或其他收件者，您可以建立在 Azure 自動化中或電子郵件動作 toosend runbook 呼叫另一個外部服務，runbook 動作 toostart webhook 動作。   

## <a name="next-steps"></a>後續步驟
* 深入了解 [Log Analytics 中的其他警示動作](log-analytics-alerts-actions.md)，包括其他動作。


