---
title: "OMS Log Analytics 中的 Webhook 警示範例 | Microsoft Docs"
description: "您可以執行以回應 Log Analytics 警示的動作之一是 *webhook*，它可讓您透過單一 HTTP 要求來叫用外部處理序。 本文透過一個範例練習在 Log Analytics 中利用 Slack 建立 webhook 動作。"
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
ms.openlocfilehash: 55b66132f7ec5c26c0a7cac1ec0a5c403dbd1082
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-alert-webhook-action-in-oms-log-analytics-to-send-message-to-slack"></a><span data-ttu-id="1e19a-104">在 OMS Log Analytics 中建立警示 webhook 動作以傳送訊息給 Slack</span><span class="sxs-lookup"><span data-stu-id="1e19a-104">Create an alert webhook action in OMS Log Analytics to send message to Slack</span></span>
<span data-ttu-id="1e19a-105">您可以執行以回應 [Log Analytics 警示](log-analytics-alerts.md) 的動作之一是 *webhook*，它可讓您透過單一 HTTP 要求來叫用外部處理序。</span><span class="sxs-lookup"><span data-stu-id="1e19a-105">One of the actions you can run in response to a [Log Analytics alert](log-analytics-alerts.md) is a *webhook*, which allows you to invoke an external process through a single HTTP request.</span></span>  <span data-ttu-id="1e19a-106">您可以在 [Log Analytics 中的警示](log-analytics-alerts.md)</span><span class="sxs-lookup"><span data-stu-id="1e19a-106">You can read about details of alerts and webhooks in [Alerts in Log Analytics](log-analytics-alerts.md)</span></span>

<span data-ttu-id="1e19a-107">在本文中，我們將透過一個範例，練習在 Log Analytics 中利用 Slack (訊息服務) 建立 webhook 動作。</span><span class="sxs-lookup"><span data-stu-id="1e19a-107">In this article, we’ll walk through an example of creating a webhook action in a Log Analytics alert using Slack which is a messaging service.</span></span>

> [!NOTE]
> <span data-ttu-id="1e19a-108">您必須有 Slack 帳戶才能完成此範例。</span><span class="sxs-lookup"><span data-stu-id="1e19a-108">You must have a Slack account to complete this sample.</span></span>  <span data-ttu-id="1e19a-109">您可以在 [slack.com](http://slack.com)註冊免費帳戶。</span><span class="sxs-lookup"><span data-stu-id="1e19a-109">You can sign up for a free account at [slack.com](http://slack.com).</span></span>
> 
> 

## <a name="step-1---enable-webhooks-in-slack"></a><span data-ttu-id="1e19a-110">步驟 1 - 在 Slack 中啟用 webhook</span><span class="sxs-lookup"><span data-stu-id="1e19a-110">Step 1 - Enable webhooks in Slack</span></span>
1. <span data-ttu-id="1e19a-111">在 [slack.com](http://slack.com)上登入 Slack。</span><span class="sxs-lookup"><span data-stu-id="1e19a-111">Sign in to Slack at [slack.com](http://slack.com).</span></span>
2. <span data-ttu-id="1e19a-112">在左窗格的 [通道] 區段中選取通道。</span><span class="sxs-lookup"><span data-stu-id="1e19a-112">Select a channel in the **Channels** section in the left pane.</span></span>  <span data-ttu-id="1e19a-113">這是訊息將傳往的通道。</span><span class="sxs-lookup"><span data-stu-id="1e19a-113">This is the channel that the message will be sent to.</span></span>  <span data-ttu-id="1e19a-114">您可以選取其中一個預設通道，例如 **general** 或 **random**。</span><span class="sxs-lookup"><span data-stu-id="1e19a-114">You can select one of the default channels such as **general** or **random**.</span></span>  <span data-ttu-id="1e19a-115">在實際執行案例中，您很有可能會建立特殊通道，例如 **criticalservicealerts**。</span><span class="sxs-lookup"><span data-stu-id="1e19a-115">In a production scenario, you would most likely create a special channel such as **criticalservicealerts**.</span></span> <br>
   
   ![Slack channels](media/log-analytics-alerts-webhooks/oms-webhooks01.png)
3. <span data-ttu-id="1e19a-117">按一下 [加入應用程式或自訂整合]  開啟 [應用程式目錄]。</span><span class="sxs-lookup"><span data-stu-id="1e19a-117">Click **Add an app or custom integration** to open the App Directory.</span></span>
4. <span data-ttu-id="1e19a-118">在搜尋方塊中輸入 *webhook*，然後選取 [傳入 WebHook]。</span><span class="sxs-lookup"><span data-stu-id="1e19a-118">Type *webhooks* into the search box and then select **Incoming WebHooks**.</span></span> <br>
   
   ![Slack channels](media/log-analytics-alerts-webhooks/oms-webhooks02.png)
5. <span data-ttu-id="1e19a-120">按一下小組名稱旁邊的 [安裝]  。</span><span class="sxs-lookup"><span data-stu-id="1e19a-120">Click **Install** next to your team name.</span></span>
6. <span data-ttu-id="1e19a-121">按一下 [加入組態] 。</span><span class="sxs-lookup"><span data-stu-id="1e19a-121">Click **Add Configuration**.</span></span>
7. <span data-ttu-id="1e19a-122">選取您要用於此範例的通道，然後按一下 [加入連入 Webhook 整合] 。</span><span class="sxs-lookup"><span data-stu-id="1e19a-122">Select the the channel that you're going to use for this example, and then click **Add Incoming WebHooks integration**.</span></span>  
8. <span data-ttu-id="1e19a-123">複製 [Webhook URL] 。</span><span class="sxs-lookup"><span data-stu-id="1e19a-123">Copy the **Webhook URL**.</span></span>  <span data-ttu-id="1e19a-124">您將會此資訊貼入 [警示組態] 中。</span><span class="sxs-lookup"><span data-stu-id="1e19a-124">You'll be pasting this into the Alert configuration.</span></span> <br>
   
    ![Slack channels](media/log-analytics-alerts-webhooks/oms-webhooks05.png)

## <a name="step-2---create-alert-rule-in-log-analytics"></a><span data-ttu-id="1e19a-126">步驟 2 - 在 Log Analytics 中建立警示規則</span><span class="sxs-lookup"><span data-stu-id="1e19a-126">Step 2 - Create alert rule in Log Analytics</span></span>
1. <span data-ttu-id="1e19a-127">[建立警示規則](log-analytics-alerts.md) 。</span><span class="sxs-lookup"><span data-stu-id="1e19a-127">[Create an alert rule](log-analytics-alerts.md) with the following settings.</span></span>
   * <span data-ttu-id="1e19a-128">查詢： ```    Type=Event EventLevelName=error ```</span><span class="sxs-lookup"><span data-stu-id="1e19a-128">Query: ```    Type=Event EventLevelName=error ```</span></span>
   * <span data-ttu-id="1e19a-129">檢查此警示的間隔︰5 分鐘</span><span class="sxs-lookup"><span data-stu-id="1e19a-129">Check for this alert every: 5 minutes</span></span>
   * <span data-ttu-id="1e19a-130">結果數目：大於 10</span><span class="sxs-lookup"><span data-stu-id="1e19a-130">The number of results is: greater than 10</span></span>
   * <span data-ttu-id="1e19a-131">在此時間範圍內︰60 分鐘</span><span class="sxs-lookup"><span data-stu-id="1e19a-131">Over this time window: 60 minutes</span></span>
   * <span data-ttu-id="1e19a-132">對 [Webhook] 選取 [是]，對其他動作選取 [否]。</span><span class="sxs-lookup"><span data-stu-id="1e19a-132">Select **Yes** for **Webhook** and **No** for the other actions.</span></span>
2. <span data-ttu-id="1e19a-133">將 Slack URL 貼入 [Webhook URL]  欄位中。</span><span class="sxs-lookup"><span data-stu-id="1e19a-133">Paste the Slack URL into the **Webhook URL** field.</span></span>
3. <span data-ttu-id="1e19a-134">選取選項來 [加入自訂 JSON 承載] 。</span><span class="sxs-lookup"><span data-stu-id="1e19a-134">Select the option to **include a custom JSON payload**.</span></span>
4. <span data-ttu-id="1e19a-135">Slack 需要有 JSON 格式化並加上參數 *text* 的承載。</span><span class="sxs-lookup"><span data-stu-id="1e19a-135">Slack expects a payload formatted in JSON with a parameter named *text*.</span></span>  <span data-ttu-id="1e19a-136">這是在它建立的訊息中顯示的文字。</span><span class="sxs-lookup"><span data-stu-id="1e19a-136">This is the text that it will display in the message it creates.</span></span>  <span data-ttu-id="1e19a-137">您可以透過 *#* 符號使用一或多個警示參數，如下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="1e19a-137">You can use one or more of the alert parameters using the *#* symbol such as in the following example.</span></span>
   
    ```
    {
    "text":"#alertrulename fired with #searchresultcount records which exceeds the over threshold of #thresholdvalue ."
    }
    ```
   
    ![example JSON payload](media/log-analytics-alerts-webhooks/oms-webhooks07.png)
5. <span data-ttu-id="1e19a-139">按一下 [儲存]  以儲存警示規則。</span><span class="sxs-lookup"><span data-stu-id="1e19a-139">Click **Save** to save the alert rule.</span></span>
6. <span data-ttu-id="1e19a-140">等待足夠的時間來建立警示，然後檢查 Slack 是否出現類似如下的訊息。</span><span class="sxs-lookup"><span data-stu-id="1e19a-140">Wait sufficient time for an alert to be created and then check Slack for a message which will be similar to the following.</span></span>
   
   ![example webhook in Slack](media/log-analytics-alerts-webhooks/oms-webhooks08.png)

### <a name="advanced-webhook-payload-for-slack"></a><span data-ttu-id="1e19a-142">Slack 的進階 webhook 承載</span><span class="sxs-lookup"><span data-stu-id="1e19a-142">Advanced webhook payload for Slack</span></span>
<span data-ttu-id="1e19a-143">您可以使用 Slack 來廣泛自訂傳入訊息。</span><span class="sxs-lookup"><span data-stu-id="1e19a-143">You can extensively customize inbound messages with Slack.</span></span> <span data-ttu-id="1e19a-144">如需詳細資訊，請參閱 Slack 網站上的 [Incoming Webhook](https://api.slack.com/incoming-webhooks) 。</span><span class="sxs-lookup"><span data-stu-id="1e19a-144">For more information, see [Incoming Webhooks](https://api.slack.com/incoming-webhooks) on the Slack website.</span></span> <span data-ttu-id="1e19a-145">以下是更複雜的承載，可建立加上格式的豐富訊息︰</span><span class="sxs-lookup"><span data-stu-id="1e19a-145">Following is a more complex payload to create a rich message with formatting:</span></span>

    {
        "attachments": [
            {
                "title":"OMS Alerts Custom Payload",
                "fields": [
                    {
                        "title": "Alert Rule Name",
                        "value": "#alertrulename"},
                    {
                        "title": "Link To SearchResults",
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


<span data-ttu-id="1e19a-146">這會在 Slack 中產生類似如下的訊息。</span><span class="sxs-lookup"><span data-stu-id="1e19a-146">This would generate a message in Slack similar to the following.</span></span>

![example message in Slack](media/log-analytics-alerts-webhooks/oms-webhooks09.png)

## <a name="summary"></a><span data-ttu-id="1e19a-148">摘要</span><span class="sxs-lookup"><span data-stu-id="1e19a-148">Summary</span></span>
<span data-ttu-id="1e19a-149">有了此警示規則後，每次符合準則時，我們就將訊息傳送至 Slack。</span><span class="sxs-lookup"><span data-stu-id="1e19a-149">With this alert rule in place, you would have a message sent to Slack every time the criteria is met.</span></span>  

<span data-ttu-id="1e19a-150">這只是舉例說明您可以建立以回應警示的動作。</span><span class="sxs-lookup"><span data-stu-id="1e19a-150">This is only one example of an action that you can create in response to an alert.</span></span>  <span data-ttu-id="1e19a-151">您可以建立 webhook 動作以呼叫另一個外部服務、建立 Runbook 動作以啟動 Azure 自動化中的 Runbook，或建立電子郵件動作將郵件傳送給自己或其他收件者。</span><span class="sxs-lookup"><span data-stu-id="1e19a-151">You could create a webhook action that calls another external service, a runbook action to start a runbook in Azure Automation, or an email action to send a mail to yourself or other recipients.</span></span>   

## <a name="next-steps"></a><span data-ttu-id="1e19a-152">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1e19a-152">Next Steps</span></span>
* <span data-ttu-id="1e19a-153">深入了解 [Log Analytics 中的其他警示動作](log-analytics-alerts-actions.md)，包括其他動作。</span><span class="sxs-lookup"><span data-stu-id="1e19a-153">Learn about other [alert actions in Log Analytics](log-analytics-alerts-actions.md) including other actions.</span></span>


