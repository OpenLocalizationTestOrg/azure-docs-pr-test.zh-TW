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
# <a name="create-an-alert-webhook-action-in-oms-log-analytics-toosend-message-tooslack"></a><span data-ttu-id="6e79a-104">在 OMS 記錄分析 toosend 訊息 tooSlack 中建立警示的 webhook 動作</span><span class="sxs-lookup"><span data-stu-id="6e79a-104">Create an alert webhook action in OMS Log Analytics toosend message tooSlack</span></span>
<span data-ttu-id="6e79a-105">其中一個 hello 動作，您可以在回應 tooa 執行[記錄分析警示](log-analytics-alerts.md)是*webhook*，可讓您 tooinvoke 外部處理序，透過單一 HTTP 要求。</span><span class="sxs-lookup"><span data-stu-id="6e79a-105">One of hello actions you can run in response tooa [Log Analytics alert](log-analytics-alerts.md) is a *webhook*, which allows you tooinvoke an external process through a single HTTP request.</span></span>  <span data-ttu-id="6e79a-106">您可以在 [Log Analytics 中的警示](log-analytics-alerts.md)</span><span class="sxs-lookup"><span data-stu-id="6e79a-106">You can read about details of alerts and webhooks in [Alerts in Log Analytics](log-analytics-alerts.md)</span></span>

<span data-ttu-id="6e79a-107">在本文中，我們將透過一個範例，練習在 Log Analytics 中利用 Slack (訊息服務) 建立 webhook 動作。</span><span class="sxs-lookup"><span data-stu-id="6e79a-107">In this article, we’ll walk through an example of creating a webhook action in a Log Analytics alert using Slack which is a messaging service.</span></span>

> [!NOTE]
> <span data-ttu-id="6e79a-108">您必須擁有 Slack 帳戶 toocomplete 此範例。</span><span class="sxs-lookup"><span data-stu-id="6e79a-108">You must have a Slack account toocomplete this sample.</span></span>  <span data-ttu-id="6e79a-109">您可以在 [slack.com](http://slack.com)註冊免費帳戶。</span><span class="sxs-lookup"><span data-stu-id="6e79a-109">You can sign up for a free account at [slack.com](http://slack.com).</span></span>
> 
> 

## <a name="step-1---enable-webhooks-in-slack"></a><span data-ttu-id="6e79a-110">步驟 1 - 在 Slack 中啟用 webhook</span><span class="sxs-lookup"><span data-stu-id="6e79a-110">Step 1 - Enable webhooks in Slack</span></span>
1. <span data-ttu-id="6e79a-111">登入在 tooSlack [slack.com](http://slack.com)。</span><span class="sxs-lookup"><span data-stu-id="6e79a-111">Sign in tooSlack at [slack.com](http://slack.com).</span></span>
2. <span data-ttu-id="6e79a-112">選取通道在 hello**通道**hello 左窗格中的區段。</span><span class="sxs-lookup"><span data-stu-id="6e79a-112">Select a channel in hello **Channels** section in hello left pane.</span></span>  <span data-ttu-id="6e79a-113">這是 hello 通道 hello 訊息將傳送至。</span><span class="sxs-lookup"><span data-stu-id="6e79a-113">This is hello channel that hello message will be sent to.</span></span>  <span data-ttu-id="6e79a-114">您可以選取其中一個 hello 預設頻道例如**一般**或**隨機**。</span><span class="sxs-lookup"><span data-stu-id="6e79a-114">You can select one of hello default channels such as **general** or **random**.</span></span>  <span data-ttu-id="6e79a-115">在實際執行案例中，您很有可能會建立特殊通道，例如 **criticalservicealerts**。</span><span class="sxs-lookup"><span data-stu-id="6e79a-115">In a production scenario, you would most likely create a special channel such as **criticalservicealerts**.</span></span> <br>
   
   ![Slack channels](media/log-analytics-alerts-webhooks/oms-webhooks01.png)
3. <span data-ttu-id="6e79a-117">按一下**新增的應用程式或自訂整合**tooopen hello 應用程式目錄。</span><span class="sxs-lookup"><span data-stu-id="6e79a-117">Click **Add an app or custom integration** tooopen hello App Directory.</span></span>
4. <span data-ttu-id="6e79a-118">型別*webhook* hello [搜尋] 方塊，然後選取成**傳入 Webhook**。</span><span class="sxs-lookup"><span data-stu-id="6e79a-118">Type *webhooks* into hello search box and then select **Incoming WebHooks**.</span></span> <br>
   
   ![Slack channels](media/log-analytics-alerts-webhooks/oms-webhooks02.png)
5. <span data-ttu-id="6e79a-120">按一下**安裝**下一個 tooyour 小組名稱。</span><span class="sxs-lookup"><span data-stu-id="6e79a-120">Click **Install** next tooyour team name.</span></span>
6. <span data-ttu-id="6e79a-121">按一下 [加入組態] 。</span><span class="sxs-lookup"><span data-stu-id="6e79a-121">Click **Add Configuration**.</span></span>
7. <span data-ttu-id="6e79a-122">您正要 toouse 如這個範例中，然後再按一下，選取 hello hello 通道**新增連入的 Webhook 整合**。</span><span class="sxs-lookup"><span data-stu-id="6e79a-122">Select hello hello channel that you're going toouse for this example, and then click **Add Incoming WebHooks integration**.</span></span>  
8. <span data-ttu-id="6e79a-123">複製 hello **Webhook URL**。</span><span class="sxs-lookup"><span data-stu-id="6e79a-123">Copy hello **Webhook URL**.</span></span>  <span data-ttu-id="6e79a-124">您將會貼入這 hello 警示設定。</span><span class="sxs-lookup"><span data-stu-id="6e79a-124">You'll be pasting this into hello Alert configuration.</span></span> <br>
   
    ![Slack channels](media/log-analytics-alerts-webhooks/oms-webhooks05.png)

## <a name="step-2---create-alert-rule-in-log-analytics"></a><span data-ttu-id="6e79a-126">步驟 2 - 在 Log Analytics 中建立警示規則</span><span class="sxs-lookup"><span data-stu-id="6e79a-126">Step 2 - Create alert rule in Log Analytics</span></span>
1. <span data-ttu-id="6e79a-127">[建立警示規則](log-analytics-alerts.md)以 hello 下列設定。</span><span class="sxs-lookup"><span data-stu-id="6e79a-127">[Create an alert rule](log-analytics-alerts.md) with hello following settings.</span></span>
   * <span data-ttu-id="6e79a-128">查詢： ```    Type=Event EventLevelName=error ```</span><span class="sxs-lookup"><span data-stu-id="6e79a-128">Query: ```    Type=Event EventLevelName=error ```</span></span>
   * <span data-ttu-id="6e79a-129">檢查此警示的間隔︰5 分鐘</span><span class="sxs-lookup"><span data-stu-id="6e79a-129">Check for this alert every: 5 minutes</span></span>
   * <span data-ttu-id="6e79a-130">結果的 hello 數目是： 大於 10</span><span class="sxs-lookup"><span data-stu-id="6e79a-130">hello number of results is: greater than 10</span></span>
   * <span data-ttu-id="6e79a-131">在此時間範圍內︰60 分鐘</span><span class="sxs-lookup"><span data-stu-id="6e79a-131">Over this time window: 60 minutes</span></span>
   * <span data-ttu-id="6e79a-132">選取**是**如**Webhook**和**否**的 hello 其他動作。</span><span class="sxs-lookup"><span data-stu-id="6e79a-132">Select **Yes** for **Webhook** and **No** for hello other actions.</span></span>
2. <span data-ttu-id="6e79a-133">貼上的 hello Slack URL 到 hello **Webhook URL**欄位。</span><span class="sxs-lookup"><span data-stu-id="6e79a-133">Paste hello Slack URL into hello **Webhook URL** field.</span></span>
3. <span data-ttu-id="6e79a-134">選取 hello 選項太**包括自訂 JSON 承載**。</span><span class="sxs-lookup"><span data-stu-id="6e79a-134">Select hello option too**include a custom JSON payload**.</span></span>
4. <span data-ttu-id="6e79a-135">Slack 需要有 JSON 格式化並加上參數 *text* 的承載。</span><span class="sxs-lookup"><span data-stu-id="6e79a-135">Slack expects a payload formatted in JSON with a parameter named *text*.</span></span>  <span data-ttu-id="6e79a-136">這是它會顯示，它會建立 hello 訊息中的 hello 文字。</span><span class="sxs-lookup"><span data-stu-id="6e79a-136">This is hello text that it will display in hello message it creates.</span></span>  <span data-ttu-id="6e79a-137">您可以使用一或多個 hello 警示參數使用 hello  *#* 符號例如如 hello 下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="6e79a-137">You can use one or more of hello alert parameters using hello *#* symbol such as in hello following example.</span></span>
   
    ```
    {
    "text":"#alertrulename fired with #searchresultcount records which exceeds hello over threshold of #thresholdvalue ."
    }
    ```
   
    ![example JSON payload](media/log-analytics-alerts-webhooks/oms-webhooks07.png)
5. <span data-ttu-id="6e79a-139">按一下**儲存**toosave hello 警示規則。</span><span class="sxs-lookup"><span data-stu-id="6e79a-139">Click **Save** toosave hello alert rule.</span></span>
6. <span data-ttu-id="6e79a-140">等候建立警示 toobe 有足夠的時間，然後檢查的訊息，將會類似 toohello 下列 Slack。</span><span class="sxs-lookup"><span data-stu-id="6e79a-140">Wait sufficient time for an alert toobe created and then check Slack for a message which will be similar toohello following.</span></span>
   
   ![example webhook in Slack](media/log-analytics-alerts-webhooks/oms-webhooks08.png)

### <a name="advanced-webhook-payload-for-slack"></a><span data-ttu-id="6e79a-142">Slack 的進階 webhook 承載</span><span class="sxs-lookup"><span data-stu-id="6e79a-142">Advanced webhook payload for Slack</span></span>
<span data-ttu-id="6e79a-143">您可以使用 Slack 來廣泛自訂傳入訊息。</span><span class="sxs-lookup"><span data-stu-id="6e79a-143">You can extensively customize inbound messages with Slack.</span></span> <span data-ttu-id="6e79a-144">如需詳細資訊，請參閱[傳入 Webhook](https://api.slack.com/incoming-webhooks) hello Slack 網站上。</span><span class="sxs-lookup"><span data-stu-id="6e79a-144">For more information, see [Incoming Webhooks](https://api.slack.com/incoming-webhooks) on hello Slack website.</span></span> <span data-ttu-id="6e79a-145">以下是更複雜的裝載 toocreate 豐富的訊息格式：</span><span class="sxs-lookup"><span data-stu-id="6e79a-145">Following is a more complex payload toocreate a rich message with formatting:</span></span>

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


<span data-ttu-id="6e79a-146">這會在 Slack 類似 toohello 下列來產生一則訊息。</span><span class="sxs-lookup"><span data-stu-id="6e79a-146">This would generate a message in Slack similar toohello following.</span></span>

![example message in Slack](media/log-analytics-alerts-webhooks/oms-webhooks09.png)

## <a name="summary"></a><span data-ttu-id="6e79a-148">摘要</span><span class="sxs-lookup"><span data-stu-id="6e79a-148">Summary</span></span>
<span data-ttu-id="6e79a-149">就地此警示規則，您必須傳送訊息 tooSlack 每次符合 hello 準則。</span><span class="sxs-lookup"><span data-stu-id="6e79a-149">With this alert rule in place, you would have a message sent tooSlack every time hello criteria is met.</span></span>  

<span data-ttu-id="6e79a-150">這是動作的只有一個執行，您可以建立回應 tooan 警示中的範例。</span><span class="sxs-lookup"><span data-stu-id="6e79a-150">This is only one example of an action that you can create in response tooan alert.</span></span>  <span data-ttu-id="6e79a-151">Mail tooyourself 或其他收件者，您可以建立在 Azure 自動化中或電子郵件動作 toosend runbook 呼叫另一個外部服務，runbook 動作 toostart webhook 動作。</span><span class="sxs-lookup"><span data-stu-id="6e79a-151">You could create a webhook action that calls another external service, a runbook action toostart a runbook in Azure Automation, or an email action toosend a mail tooyourself or other recipients.</span></span>   

## <a name="next-steps"></a><span data-ttu-id="6e79a-152">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6e79a-152">Next Steps</span></span>
* <span data-ttu-id="6e79a-153">深入了解 [Log Analytics 中的其他警示動作](log-analytics-alerts-actions.md)，包括其他動作。</span><span class="sxs-lookup"><span data-stu-id="6e79a-153">Learn about other [alert actions in Log Analytics](log-analytics-alerts-actions.md) including other actions.</span></span>


