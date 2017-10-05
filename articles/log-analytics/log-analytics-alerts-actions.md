---
title: "OMS Log Analytics 中的警示回應 | Microsoft Docs"
description: "Log Analytics 中的警示會識別您的 OMS 儲存機制中的重要資訊，並可主動通知您相關問題或叫用動作以嘗試更正問題。  本文描述如何建立警示規則及詳細說明可以採取的各種動作。"
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
ms.openlocfilehash: b8731e1fe48b7d809b113eb5273e3962542b8f34
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="add-actions-to-alert-rules-in-log-analytics"></a><span data-ttu-id="dc257-104">將動作新增至 Log Analytics 中的警示規則</span><span class="sxs-lookup"><span data-stu-id="dc257-104">Add actions to alert rules in Log Analytics</span></span>
<span data-ttu-id="dc257-105">[在 Log Analytics 中建立警示](log-analytics-alerts.md)後，您可以選擇[設定警示規則](log-analytics-alerts.md)以執行一或多個動作。</span><span class="sxs-lookup"><span data-stu-id="dc257-105">When an [alert is created in Log Analytics](log-analytics-alerts.md), you have the option of [configuring the alert rule](log-analytics-alerts.md) to perform one or more actions.</span></span>  <span data-ttu-id="dc257-106">本文說明各種可用的動作以及設定每種動作的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="dc257-106">This article describes the different actions that are available and details on configuring each kind.</span></span>

| <span data-ttu-id="dc257-107">動作</span><span class="sxs-lookup"><span data-stu-id="dc257-107">Action</span></span> | <span data-ttu-id="dc257-108">說明</span><span class="sxs-lookup"><span data-stu-id="dc257-108">Description</span></span> |
|:--|:--|
| [<span data-ttu-id="dc257-109">電子郵件</span><span class="sxs-lookup"><span data-stu-id="dc257-109">Email</span></span>](#email-actions) | <span data-ttu-id="dc257-110">傳送內含警示詳細資料的電子郵件給一或多位收件者。</span><span class="sxs-lookup"><span data-stu-id="dc257-110">Send an e-mail with the details of the alert to one or more recipients.</span></span> |
| [<span data-ttu-id="dc257-111">Webhook</span><span class="sxs-lookup"><span data-stu-id="dc257-111">Webhook</span></span>](#webhook-actions) | <span data-ttu-id="dc257-112">透過單一 HTTP POST 要求叫用外部處理序。</span><span class="sxs-lookup"><span data-stu-id="dc257-112">Invoke an external process through a single HTTP POST request.</span></span> |
| [<span data-ttu-id="dc257-113">Runbook</span><span class="sxs-lookup"><span data-stu-id="dc257-113">Runbook</span></span>](#runbook-actions) | <span data-ttu-id="dc257-114">在 Azure 自動化中啟動 Runbook。</span><span class="sxs-lookup"><span data-stu-id="dc257-114">Start a runbook in Azure Automation.</span></span> |


## <a name="email-actions"></a><span data-ttu-id="dc257-115">電子郵件動作</span><span class="sxs-lookup"><span data-stu-id="dc257-115">Email actions</span></span>
<span data-ttu-id="dc257-116">電子郵件動作會傳送內含警示詳細資料的電子郵件給一或多位收件者。</span><span class="sxs-lookup"><span data-stu-id="dc257-116">Email actions send an e-mail with the details of the alert to one or more recipients.</span></span>  <span data-ttu-id="dc257-117">您可以指定郵件的主旨，但其內容是由 Log Analytics 所編製的標準格式。</span><span class="sxs-lookup"><span data-stu-id="dc257-117">You can specify the subject of the mail, but it's content is a standard format constructed by Log Analytics.</span></span>  <span data-ttu-id="dc257-118">除了記錄檔搜尋所傳回的最多 10 筆記錄的詳細資料以外，其中還包括摘要資訊 (如警示名稱)。</span><span class="sxs-lookup"><span data-stu-id="dc257-118">It includes summary information such as the name of the alert in addition to details of up to ten records returned by the log search.</span></span>  <span data-ttu-id="dc257-119">此外，也包括 Log Analytics 中將從該查詢傳回整個記錄集的記錄檔搜尋的連結。</span><span class="sxs-lookup"><span data-stu-id="dc257-119">It also includes a link to a log search in Log Analytics that will return the entire set of records from that query.</span></span>   <span data-ttu-id="dc257-120">此郵件的寄件者為 *Microsoft Operations Management Suite Team &lt;noreply@oms.microsoft.com&gt;*。</span><span class="sxs-lookup"><span data-stu-id="dc257-120">The sender of the mail is *Microsoft Operations Management Suite Team &lt;noreply@oms.microsoft.com&gt;*.</span></span> 

<span data-ttu-id="dc257-121">電子郵件動作需要下表中的屬性。</span><span class="sxs-lookup"><span data-stu-id="dc257-121">Email actions require the properties in the following table.</span></span>

| <span data-ttu-id="dc257-122">屬性</span><span class="sxs-lookup"><span data-stu-id="dc257-122">Property</span></span> | <span data-ttu-id="dc257-123">說明</span><span class="sxs-lookup"><span data-stu-id="dc257-123">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="dc257-124">主旨</span><span class="sxs-lookup"><span data-stu-id="dc257-124">Subject</span></span> |<span data-ttu-id="dc257-125">電子郵件的主旨。</span><span class="sxs-lookup"><span data-stu-id="dc257-125">Subject in the email.</span></span>  <span data-ttu-id="dc257-126">您無法修改郵件的內文。</span><span class="sxs-lookup"><span data-stu-id="dc257-126">You cannot modify the body of the mail.</span></span> |
| <span data-ttu-id="dc257-127">收件者</span><span class="sxs-lookup"><span data-stu-id="dc257-127">Recipients</span></span> |<span data-ttu-id="dc257-128">所有電子郵件收件者的地址。</span><span class="sxs-lookup"><span data-stu-id="dc257-128">Addresses of all e-mail recipients.</span></span>  <span data-ttu-id="dc257-129">如果您指定多個地址，則使用分號 (;) 分隔這些地址。</span><span class="sxs-lookup"><span data-stu-id="dc257-129">If you specify more than one address, then separate the addresses with a semicolon (;).</span></span> |


## <a name="webhook-actions"></a><span data-ttu-id="dc257-130">Webhook 動作</span><span class="sxs-lookup"><span data-stu-id="dc257-130">Webhook actions</span></span>

<span data-ttu-id="dc257-131">Webhook 動作可讓您透過單一 HTTP POST 要求叫用外部處理序。</span><span class="sxs-lookup"><span data-stu-id="dc257-131">Webhook actions allow you to invoke an external process through a single HTTP POST request.</span></span>  <span data-ttu-id="dc257-132">被呼叫的服務應支援 Webhook，並判斷將如何使用所接收的承載。</span><span class="sxs-lookup"><span data-stu-id="dc257-132">The service being called should support webhooks and determine how it will use any payload it receives.</span></span>  <span data-ttu-id="dc257-133">只要此要求是 API 所認得的格式，您也可以呼叫不會特別支援 Webhook 的 REST API。</span><span class="sxs-lookup"><span data-stu-id="dc257-133">You could also call a REST API that doesn't specifically support webhooks as long as the request is in a format that the API understands.</span></span>  <span data-ttu-id="dc257-134">使用 Webhook 來回應警示的範例會在 [Slack](http://slack.com) 中傳送訊息，或在 [PagerDuty](http://pagerduty.com/) 中建立事件。</span><span class="sxs-lookup"><span data-stu-id="dc257-134">Examples of using a webhook in response to an alert are sending a message in [Slack](http://slack.com) or creating an incident in [PagerDuty](http://pagerduty.com/).</span></span>  <span data-ttu-id="dc257-135">如需使用 Webhook 來呼叫 Slack 以建立警示規則的完整逐步解說，請參閱 [Log Analytics 警示中的 Webhook](log-analytics-alerts-webhooks.md)。</span><span class="sxs-lookup"><span data-stu-id="dc257-135">A complete walkthrough of creating an alert rule with a webhook to call Slack is available at [Webhooks in Log Analytics alerts](log-analytics-alerts-webhooks.md).</span></span>

<span data-ttu-id="dc257-136">Webhook 動作需要下表中的屬性。</span><span class="sxs-lookup"><span data-stu-id="dc257-136">Webhook actions require the properties in the following table.</span></span>

| <span data-ttu-id="dc257-137">屬性</span><span class="sxs-lookup"><span data-stu-id="dc257-137">Property</span></span> | <span data-ttu-id="dc257-138">說明</span><span class="sxs-lookup"><span data-stu-id="dc257-138">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="dc257-139">Webhook URL</span><span class="sxs-lookup"><span data-stu-id="dc257-139">Webhook URL</span></span> |<span data-ttu-id="dc257-140">Webhook 的 URL。</span><span class="sxs-lookup"><span data-stu-id="dc257-140">The URL of the webhook.</span></span> |
| <span data-ttu-id="dc257-141">自訂 JSON 承載</span><span class="sxs-lookup"><span data-stu-id="dc257-141">Custom JSON payload</span></span> |<span data-ttu-id="dc257-142">要隨著 webhook 傳送的自訂承載。</span><span class="sxs-lookup"><span data-stu-id="dc257-142">Custom payload to send with the webhook.</span></span>  <span data-ttu-id="dc257-143">如需詳細資料，請參閱下文。</span><span class="sxs-lookup"><span data-stu-id="dc257-143">See below for details.</span></span> |


<span data-ttu-id="dc257-144">Webhook 包括 URL 以及 JSON 格式的承載 (也就是傳送至外部服務的資料)。</span><span class="sxs-lookup"><span data-stu-id="dc257-144">Webhooks include a URL and a payload formatted in JSON that is the data sent to the external service.</span></span>  <span data-ttu-id="dc257-145">根據預設，承載會包含下表中的值。</span><span class="sxs-lookup"><span data-stu-id="dc257-145">By default, the payload will include the values in the following table.</span></span>  <span data-ttu-id="dc257-146">您可以選擇用自己的自訂承載來取代此承載。</span><span class="sxs-lookup"><span data-stu-id="dc257-146">You can choose to replace this payload with a custom one of your own.</span></span>  <span data-ttu-id="dc257-147">在此情況下，您可以使用下表中每個參數的變數，將其值包含在您的自訂承載中。</span><span class="sxs-lookup"><span data-stu-id="dc257-147">In that case you can use the variables in the table for each of the parameters to include their value in your custom payload.</span></span>

| <span data-ttu-id="dc257-148">參數</span><span class="sxs-lookup"><span data-stu-id="dc257-148">Parameter</span></span> | <span data-ttu-id="dc257-149">變數</span><span class="sxs-lookup"><span data-stu-id="dc257-149">Variable</span></span> | <span data-ttu-id="dc257-150">說明</span><span class="sxs-lookup"><span data-stu-id="dc257-150">Description</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="dc257-151">AlertRuleName</span><span class="sxs-lookup"><span data-stu-id="dc257-151">AlertRuleName</span></span> |<span data-ttu-id="dc257-152">#alertrulename</span><span class="sxs-lookup"><span data-stu-id="dc257-152">#alertrulename</span></span> |<span data-ttu-id="dc257-153">警示規則的名稱。</span><span class="sxs-lookup"><span data-stu-id="dc257-153">Name of the alert rule.</span></span> |
| <span data-ttu-id="dc257-154">AlertThresholdOperator</span><span class="sxs-lookup"><span data-stu-id="dc257-154">AlertThresholdOperator</span></span> |<span data-ttu-id="dc257-155">#thresholdoperator</span><span class="sxs-lookup"><span data-stu-id="dc257-155">#thresholdoperator</span></span> |<span data-ttu-id="dc257-156">警示規則的臨界值運算子。</span><span class="sxs-lookup"><span data-stu-id="dc257-156">Threshold operator for the alert rule.</span></span>  <span data-ttu-id="dc257-157">大於或等於。</span><span class="sxs-lookup"><span data-stu-id="dc257-157">*Greater than* or *Less than*.</span></span> |
| <span data-ttu-id="dc257-158">AlertThresholdValue</span><span class="sxs-lookup"><span data-stu-id="dc257-158">AlertThresholdValue</span></span> |<span data-ttu-id="dc257-159">#thresholdvalue</span><span class="sxs-lookup"><span data-stu-id="dc257-159">#thresholdvalue</span></span> |<span data-ttu-id="dc257-160">警示規則的臨界值。</span><span class="sxs-lookup"><span data-stu-id="dc257-160">Threshold value for the alert rule.</span></span> |
| <span data-ttu-id="dc257-161">LinkToSearchResults</span><span class="sxs-lookup"><span data-stu-id="dc257-161">LinkToSearchResults</span></span> |<span data-ttu-id="dc257-162">#linktosearchresults</span><span class="sxs-lookup"><span data-stu-id="dc257-162">#linktosearchresults</span></span> |<span data-ttu-id="dc257-163">連結至 Log Analytics 記錄檔搜尋，而該搜尋會從建立警示的查詢傳回記錄。</span><span class="sxs-lookup"><span data-stu-id="dc257-163">Link to Log Analytics log search that returns the records from the query that created the alert.</span></span> |
| <span data-ttu-id="dc257-164">ResultCount</span><span class="sxs-lookup"><span data-stu-id="dc257-164">ResultCount</span></span> |<span data-ttu-id="dc257-165">#searchresultcount</span><span class="sxs-lookup"><span data-stu-id="dc257-165">#searchresultcount</span></span> |<span data-ttu-id="dc257-166">搜尋結果中的記錄數目。</span><span class="sxs-lookup"><span data-stu-id="dc257-166">Number of records in the search results.</span></span> |
| <span data-ttu-id="dc257-167">SearchIntervalEndtimeUtc</span><span class="sxs-lookup"><span data-stu-id="dc257-167">SearchIntervalEndtimeUtc</span></span> |<span data-ttu-id="dc257-168">#searchintervalendtimeutc</span><span class="sxs-lookup"><span data-stu-id="dc257-168">#searchintervalendtimeutc</span></span> |<span data-ttu-id="dc257-169">查詢的結束時間 (UTC 格式)。</span><span class="sxs-lookup"><span data-stu-id="dc257-169">End time for the query in UTC format.</span></span> |
| <span data-ttu-id="dc257-170">SearchIntervalInSeconds</span><span class="sxs-lookup"><span data-stu-id="dc257-170">SearchIntervalInSeconds</span></span> |<span data-ttu-id="dc257-171">#searchinterval</span><span class="sxs-lookup"><span data-stu-id="dc257-171">#searchinterval</span></span> |<span data-ttu-id="dc257-172">警示規則的時間範圍。</span><span class="sxs-lookup"><span data-stu-id="dc257-172">Time window for the alert rule.</span></span> |
| <span data-ttu-id="dc257-173">SearchIntervalStartTimeUtc</span><span class="sxs-lookup"><span data-stu-id="dc257-173">SearchIntervalStartTimeUtc</span></span> |<span data-ttu-id="dc257-174">#searchintervalstarttimeutc</span><span class="sxs-lookup"><span data-stu-id="dc257-174">#searchintervalstarttimeutc</span></span> |<span data-ttu-id="dc257-175">查詢的開始時間 (UTC 格式)。</span><span class="sxs-lookup"><span data-stu-id="dc257-175">Start time for the query in UTC format.</span></span> |
| <span data-ttu-id="dc257-176">SearchQuery</span><span class="sxs-lookup"><span data-stu-id="dc257-176">SearchQuery</span></span> |<span data-ttu-id="dc257-177">#searchquery</span><span class="sxs-lookup"><span data-stu-id="dc257-177">#searchquery</span></span> |<span data-ttu-id="dc257-178">警示規則所使用的記錄檔搜尋查詢。</span><span class="sxs-lookup"><span data-stu-id="dc257-178">Log search query used by the alert rule.</span></span> |
| <span data-ttu-id="dc257-179">SearchResults</span><span class="sxs-lookup"><span data-stu-id="dc257-179">SearchResults</span></span> |<span data-ttu-id="dc257-180">請參閱下方</span><span class="sxs-lookup"><span data-stu-id="dc257-180">See below</span></span> |<span data-ttu-id="dc257-181">查詢所傳回的記錄 (JSON 格式)。</span><span class="sxs-lookup"><span data-stu-id="dc257-181">Records returned by the query in JSON format.</span></span>  <span data-ttu-id="dc257-182">受限於前 5,000 筆記錄。</span><span class="sxs-lookup"><span data-stu-id="dc257-182">Limited to the first 5,000 records.</span></span> |
| <span data-ttu-id="dc257-183">WorkspaceID</span><span class="sxs-lookup"><span data-stu-id="dc257-183">WorkspaceID</span></span> |<span data-ttu-id="dc257-184">#workspaceid</span><span class="sxs-lookup"><span data-stu-id="dc257-184">#workspaceid</span></span> |<span data-ttu-id="dc257-185">OMS 工作區的識別碼。</span><span class="sxs-lookup"><span data-stu-id="dc257-185">ID of your OMS workspace.</span></span> |

<span data-ttu-id="dc257-186">例如，您可以指定下列自訂承載，其中包含稱為 text 的單一參數。</span><span class="sxs-lookup"><span data-stu-id="dc257-186">For example, you might specify the following custom payload that includes a single parameter called *text*.</span></span>  <span data-ttu-id="dc257-187">此 Webhook 所呼叫的服務需要有這個參數。</span><span class="sxs-lookup"><span data-stu-id="dc257-187">The service that this webhook calls would be expecting this parameter.</span></span>

    {
        "text":"#alertrulename fired with #searchresultcount over threshold of #thresholdvalue."
    }

<span data-ttu-id="dc257-188">此範例承載會在傳送到 Webhook 時解析如下。</span><span class="sxs-lookup"><span data-stu-id="dc257-188">This example payload would resolve to something like the following when sent to the webhook.</span></span>

    {
        "text":"My Alert Rule fired with 18 records over threshold of 10 ."
    }

<span data-ttu-id="dc257-189">若要在自訂承載中包含搜尋結果，請將下面一行新增為 json 承載中的最上層屬性。</span><span class="sxs-lookup"><span data-stu-id="dc257-189">To include search results in a custom payload, add the following line as a top level property in the json payload.</span></span>  

    "IncludeSearchResults":true

<span data-ttu-id="dc257-190">例如，若要建立只包含警示名稱和搜尋結果的自訂承載，您可以使用下列程式碼。</span><span class="sxs-lookup"><span data-stu-id="dc257-190">For example, to create a custom payload that includes just the alert name and the search results, you could use the following.</span></span> 

    {
       "alertname":"#alertrulename",
       "IncludeSearchResults":true
    }


<span data-ttu-id="dc257-191">您可以[在 OMS Log Analytics 中建立警示 webhook 動作以傳送訊息給 Slack](log-analytics-alerts-webhooks.md)時使用 Webhook 來啟動外部服務，逐步執行建立警示規則的完整範例。</span><span class="sxs-lookup"><span data-stu-id="dc257-191">You can walk through a complete example of creating an alert rule with a webhook to start an external service at [Create an alert webhook action in OMS Log Analytics to send message to Slack](log-analytics-alerts-webhooks.md).</span></span>

## <a name="runbook-actions"></a><span data-ttu-id="dc257-192">Runbook 動作</span><span class="sxs-lookup"><span data-stu-id="dc257-192">Runbook actions</span></span>
<span data-ttu-id="dc257-193">Runbook 動作可在 Azure 自動化中啟動 Runbook。</span><span class="sxs-lookup"><span data-stu-id="dc257-193">Runbook actions start a runbook in Azure Automation.</span></span>  <span data-ttu-id="dc257-194">若要使用這類型的動作，您必須在 OMS 工作區中安裝並設定 [自動化解決方案](log-analytics-add-solutions.md) 。</span><span class="sxs-lookup"><span data-stu-id="dc257-194">In order to use this type of action, you must have the [Automation solution](log-analytics-add-solutions.md) installed and configured in your OMS workspace.</span></span>  <span data-ttu-id="dc257-195">您可以從自動化解決方案中設定的自動化帳戶中的 Runbook 進行選取。</span><span class="sxs-lookup"><span data-stu-id="dc257-195">You can select from the runbooks in the automation account that you configured in the Automation solution.</span></span>

<span data-ttu-id="dc257-196">Runbook 動作需要下表中的屬性。</span><span class="sxs-lookup"><span data-stu-id="dc257-196">Runbook actions require the properties in the following table.</span></span>

| <span data-ttu-id="dc257-197">屬性</span><span class="sxs-lookup"><span data-stu-id="dc257-197">Property</span></span> | <span data-ttu-id="dc257-198">說明</span><span class="sxs-lookup"><span data-stu-id="dc257-198">Description</span></span> |
|:--- |:---|
| <span data-ttu-id="dc257-199">Runbook</span><span class="sxs-lookup"><span data-stu-id="dc257-199">Runbook</span></span> | <span data-ttu-id="dc257-200">建立警示後，您想要啟動的 Runbook。</span><span class="sxs-lookup"><span data-stu-id="dc257-200">Runbook that you want to start when an alert is created.</span></span> |
| <span data-ttu-id="dc257-201">執行位置</span><span class="sxs-lookup"><span data-stu-id="dc257-201">Run on</span></span> | <span data-ttu-id="dc257-202">指定 [Azure] 以在雲端執行 Runbook。</span><span class="sxs-lookup"><span data-stu-id="dc257-202">Specify **Azure** to run the runbook in the cloud.</span></span>  <span data-ttu-id="dc257-203">指定 [Hybrid Worker]，以在已安裝 [Hybrid Runbook Worker](../automation/automation-hybrid-runbook-worker.md ) 的代理程式上執行 Runbook。</span><span class="sxs-lookup"><span data-stu-id="dc257-203">Specify **Hybrid worker** to run the runbook on an agent with [Hybrid Runbook Worker](../automation/automation-hybrid-runbook-worker.md ) installed.</span></span>  |

<span data-ttu-id="dc257-204">Runbook 動作會使用 [Webhook](../automation/automation-webhooks.md)來啟動 Runbook。</span><span class="sxs-lookup"><span data-stu-id="dc257-204">Runbook actions start the runbook using a [webhook](../automation/automation-webhooks.md).</span></span>  <span data-ttu-id="dc257-205">當您建立警示規則時，系統會自動為 Runbook 建立新的 Webhook，其名稱為 **OMS 警示補救** 後面接著 GUID。</span><span class="sxs-lookup"><span data-stu-id="dc257-205">When you create the alert rule, it will automatically create a new webhook for the runbook with the name **OMS Alert Remediation** followed by a GUID.</span></span>  

<span data-ttu-id="dc257-206">您無法直接填入 Runbook 的任何參數，但 [$WebhookData 參數](../automation/automation-webhooks.md) 會包含警示的詳細資料，包括記錄檔搜尋 (建立此警示) 的結果。</span><span class="sxs-lookup"><span data-stu-id="dc257-206">You cannot directly populate any parameters of the runbook, but the [$WebhookData parameter](../automation/automation-webhooks.md) will include the details of the alert, including the results of the log search that created it.</span></span>  <span data-ttu-id="dc257-207">Runbook 必須定義 **$WebhookData** 做為參數，才能存取警示的屬性。</span><span class="sxs-lookup"><span data-stu-id="dc257-207">The runbook will need to define **$WebhookData** as a parameter for it to access the properties of the alert.</span></span>  <span data-ttu-id="dc257-208">在 **$WebhookData** 的 **RequestBody** 屬性中，警示資料以 JSON 格式儲存在一個稱為 **SearchResults** 的屬性中。</span><span class="sxs-lookup"><span data-stu-id="dc257-208">The alert data is available in json format in a single property called **SearchResults** in the **RequestBody** property of **$WebhookData**.</span></span>  <span data-ttu-id="dc257-209">此資料具有下表中的屬性。</span><span class="sxs-lookup"><span data-stu-id="dc257-209">This will have with the properties in the following table.</span></span>

| <span data-ttu-id="dc257-210">節點</span><span class="sxs-lookup"><span data-stu-id="dc257-210">Node</span></span> | <span data-ttu-id="dc257-211">說明</span><span class="sxs-lookup"><span data-stu-id="dc257-211">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="dc257-212">id</span><span class="sxs-lookup"><span data-stu-id="dc257-212">id</span></span> |<span data-ttu-id="dc257-213">搜尋的路徑和 GUID。</span><span class="sxs-lookup"><span data-stu-id="dc257-213">Path and GUID of the search.</span></span> |
| <span data-ttu-id="dc257-214">__metadata</span><span class="sxs-lookup"><span data-stu-id="dc257-214">__metadata</span></span> |<span data-ttu-id="dc257-215">警示的相關資訊，包括搜尋結果的記錄數和狀態。</span><span class="sxs-lookup"><span data-stu-id="dc257-215">Information about the alert including the number of records and status of the search results.</span></span> |
| <span data-ttu-id="dc257-216">value</span><span class="sxs-lookup"><span data-stu-id="dc257-216">value</span></span> |<span data-ttu-id="dc257-217">搜尋結果中每一筆記錄的個別項目。</span><span class="sxs-lookup"><span data-stu-id="dc257-217">Separate entry for each record in the search results.</span></span>  <span data-ttu-id="dc257-218">項目的詳細資料會符合記錄的屬性和記錄。</span><span class="sxs-lookup"><span data-stu-id="dc257-218">The details of the entry will match the properties and values of the record.</span></span> |

<span data-ttu-id="dc257-219">例如，下列 Runbook 會擷取記錄搜尋所傳回的記錄，並根據每一筆記錄的類型來指派不同屬性。</span><span class="sxs-lookup"><span data-stu-id="dc257-219">For example, the following runbook would extract the records returned by the log search  and assign different properties based on the type of each record.</span></span>  <span data-ttu-id="dc257-220">請注意，Runbook 會開始從 JSON 轉換 **RequestBody**，讓它可以在 PowerShell 中當作物件來使用。</span><span class="sxs-lookup"><span data-stu-id="dc257-220">Note that the runbook starts by converting **RequestBody** from json so that it can be worked with as an object in PowerShell.</span></span>

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


## <a name="next-steps"></a><span data-ttu-id="dc257-221">後續步驟</span><span class="sxs-lookup"><span data-stu-id="dc257-221">Next steps</span></span>
- <span data-ttu-id="dc257-222">完成 [設定 Webook](log-analytics-alerts-webhooks.md) 和警示規則的逐步解說。</span><span class="sxs-lookup"><span data-stu-id="dc257-222">Complete a walkthrough for [configuring a webook](log-analytics-alerts-webhooks.md) with an alert rule.</span></span>  
- <span data-ttu-id="dc257-223">了解如何在 [Azure 自動化中撰寫 Runbook](https://azure.microsoft.com/documentation/services/automation) 以補救警示所識別的問題。</span><span class="sxs-lookup"><span data-stu-id="dc257-223">Learn how to write [runbooks in Azure Automation](https://azure.microsoft.com/documentation/services/automation) to remediate problems identified by alerts.</span></span>