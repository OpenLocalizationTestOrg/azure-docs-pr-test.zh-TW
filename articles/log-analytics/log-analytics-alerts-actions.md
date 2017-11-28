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
# <a name="add-actions-tooalert-rules-in-log-analytics"></a><span data-ttu-id="3b504-104">在 記錄分析中加入動作 tooalert 規則</span><span class="sxs-lookup"><span data-stu-id="3b504-104">Add actions tooalert rules in Log Analytics</span></span>
<span data-ttu-id="3b504-105">當[警示會在記錄分析](log-analytics-alerts.md)，您可以在 hello 選擇[設定 hello 警示規則](log-analytics-alerts.md)tooperform 一或多個動作。</span><span class="sxs-lookup"><span data-stu-id="3b504-105">When an [alert is created in Log Analytics](log-analytics-alerts.md), you have hello option of [configuring hello alert rule](log-analytics-alerts.md) tooperform one or more actions.</span></span>  <span data-ttu-id="3b504-106">本文說明 hello 可用的不同動作及詳細資料，設定每個類型。</span><span class="sxs-lookup"><span data-stu-id="3b504-106">This article describes hello different actions that are available and details on configuring each kind.</span></span>

| <span data-ttu-id="3b504-107">動作</span><span class="sxs-lookup"><span data-stu-id="3b504-107">Action</span></span> | <span data-ttu-id="3b504-108">說明</span><span class="sxs-lookup"><span data-stu-id="3b504-108">Description</span></span> |
|:--|:--|
| [<span data-ttu-id="3b504-109">電子郵件</span><span class="sxs-lookup"><span data-stu-id="3b504-109">Email</span></span>](#email-actions) | <span data-ttu-id="3b504-110">傳送電子郵件與 hello 的 hello 警示 tooone 或多個收件者的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="3b504-110">Send an e-mail with hello details of hello alert tooone or more recipients.</span></span> |
| [<span data-ttu-id="3b504-111">Webhook</span><span class="sxs-lookup"><span data-stu-id="3b504-111">Webhook</span></span>](#webhook-actions) | <span data-ttu-id="3b504-112">透過單一 HTTP POST 要求叫用外部處理序。</span><span class="sxs-lookup"><span data-stu-id="3b504-112">Invoke an external process through a single HTTP POST request.</span></span> |
| [<span data-ttu-id="3b504-113">Runbook</span><span class="sxs-lookup"><span data-stu-id="3b504-113">Runbook</span></span>](#runbook-actions) | <span data-ttu-id="3b504-114">在 Azure 自動化中啟動 Runbook。</span><span class="sxs-lookup"><span data-stu-id="3b504-114">Start a runbook in Azure Automation.</span></span> |


## <a name="email-actions"></a><span data-ttu-id="3b504-115">電子郵件動作</span><span class="sxs-lookup"><span data-stu-id="3b504-115">Email actions</span></span>
<span data-ttu-id="3b504-116">電子郵件動作會傳送 hello 的 hello 警示 tooone 或多個收件者的詳細資料的電子郵件。</span><span class="sxs-lookup"><span data-stu-id="3b504-116">Email actions send an e-mail with hello details of hello alert tooone or more recipients.</span></span>  <span data-ttu-id="3b504-117">您可以指定 hello 的 hello 郵件的主旨，但它的內容記錄分析所建構的標準格式。</span><span class="sxs-lookup"><span data-stu-id="3b504-117">You can specify hello subject of hello mail, but it's content is a standard format constructed by Log Analytics.</span></span>  <span data-ttu-id="3b504-118">中的 hello 記錄搜尋所傳回的 tooten 記錄的加法 toodetails 包含例如 hello 名稱的 hello 警示的摘要資訊。</span><span class="sxs-lookup"><span data-stu-id="3b504-118">It includes summary information such as hello name of hello alert in addition toodetails of up tooten records returned by hello log search.</span></span>  <span data-ttu-id="3b504-119">它也包含連結 tooa 記錄搜尋記錄分析會從該查詢傳回 hello 整組記錄中。</span><span class="sxs-lookup"><span data-stu-id="3b504-119">It also includes a link tooa log search in Log Analytics that will return hello entire set of records from that query.</span></span>   <span data-ttu-id="3b504-120">hello 寄件者的 hello 郵件是*Microsoft Operations Management Suite Team &lt; noreply@oms.microsoft.com &gt;* 。</span><span class="sxs-lookup"><span data-stu-id="3b504-120">hello sender of hello mail is *Microsoft Operations Management Suite Team &lt;noreply@oms.microsoft.com&gt;*.</span></span> 

<span data-ttu-id="3b504-121">電子郵件動作需要 hello 下表中的 hello 屬性。</span><span class="sxs-lookup"><span data-stu-id="3b504-121">Email actions require hello properties in hello following table.</span></span>

| <span data-ttu-id="3b504-122">屬性</span><span class="sxs-lookup"><span data-stu-id="3b504-122">Property</span></span> | <span data-ttu-id="3b504-123">說明</span><span class="sxs-lookup"><span data-stu-id="3b504-123">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="3b504-124">主旨</span><span class="sxs-lookup"><span data-stu-id="3b504-124">Subject</span></span> |<span data-ttu-id="3b504-125">Hello 電子郵件的主旨。</span><span class="sxs-lookup"><span data-stu-id="3b504-125">Subject in hello email.</span></span>  <span data-ttu-id="3b504-126">您無法修改 hello 郵件 hello 主體。</span><span class="sxs-lookup"><span data-stu-id="3b504-126">You cannot modify hello body of hello mail.</span></span> |
| <span data-ttu-id="3b504-127">收件者</span><span class="sxs-lookup"><span data-stu-id="3b504-127">Recipients</span></span> |<span data-ttu-id="3b504-128">所有電子郵件收件者的地址。</span><span class="sxs-lookup"><span data-stu-id="3b504-128">Addresses of all e-mail recipients.</span></span>  <span data-ttu-id="3b504-129">如果您指定一個以上的地址，然後個別 hello 位址以分號 （;）。</span><span class="sxs-lookup"><span data-stu-id="3b504-129">If you specify more than one address, then separate hello addresses with a semicolon (;).</span></span> |


## <a name="webhook-actions"></a><span data-ttu-id="3b504-130">Webhook 動作</span><span class="sxs-lookup"><span data-stu-id="3b504-130">Webhook actions</span></span>

<span data-ttu-id="3b504-131">Webhook 動作可讓您 tooinvoke 外部處理序，透過單一的 HTTP POST 要求。</span><span class="sxs-lookup"><span data-stu-id="3b504-131">Webhook actions allow you tooinvoke an external process through a single HTTP POST request.</span></span>  <span data-ttu-id="3b504-132">呼叫 hello 服務應支援 webhook，並判斷將如何使用任何裝載接收。</span><span class="sxs-lookup"><span data-stu-id="3b504-132">hello service being called should support webhooks and determine how it will use any payload it receives.</span></span>  <span data-ttu-id="3b504-133">您也可以呼叫 REST API，只要 hello 要求的格式 API 了解該 hello 特別不支援 webhook。</span><span class="sxs-lookup"><span data-stu-id="3b504-133">You could also call a REST API that doesn't specifically support webhooks as long as hello request is in a format that hello API understands.</span></span>  <span data-ttu-id="3b504-134">使用 webhook 回應 tooan 警示中的範例會傳送訊息[Slack](http://slack.com)或建立事件[PagerDuty](http://pagerduty.com/)。</span><span class="sxs-lookup"><span data-stu-id="3b504-134">Examples of using a webhook in response tooan alert are sending a message in [Slack](http://slack.com) or creating an incident in [PagerDuty](http://pagerduty.com/).</span></span>  <span data-ttu-id="3b504-135">與 Slack 的 webhook toocall 建立警示規則的完整逐步解說將會位於[記錄分析警示中的 Webhook](log-analytics-alerts-webhooks.md)。</span><span class="sxs-lookup"><span data-stu-id="3b504-135">A complete walkthrough of creating an alert rule with a webhook toocall Slack is available at [Webhooks in Log Analytics alerts](log-analytics-alerts-webhooks.md).</span></span>

<span data-ttu-id="3b504-136">Webhook 動作需要 hello 下表中的 hello 屬性。</span><span class="sxs-lookup"><span data-stu-id="3b504-136">Webhook actions require hello properties in hello following table.</span></span>

| <span data-ttu-id="3b504-137">屬性</span><span class="sxs-lookup"><span data-stu-id="3b504-137">Property</span></span> | <span data-ttu-id="3b504-138">說明</span><span class="sxs-lookup"><span data-stu-id="3b504-138">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="3b504-139">Webhook URL</span><span class="sxs-lookup"><span data-stu-id="3b504-139">Webhook URL</span></span> |<span data-ttu-id="3b504-140">hello hello webhook URL。</span><span class="sxs-lookup"><span data-stu-id="3b504-140">hello URL of hello webhook.</span></span> |
| <span data-ttu-id="3b504-141">自訂 JSON 承載</span><span class="sxs-lookup"><span data-stu-id="3b504-141">Custom JSON payload</span></span> |<span data-ttu-id="3b504-142">自訂承載 toosend 與 hello webhook。</span><span class="sxs-lookup"><span data-stu-id="3b504-142">Custom payload toosend with hello webhook.</span></span>  <span data-ttu-id="3b504-143">如需詳細資料，請參閱下文。</span><span class="sxs-lookup"><span data-stu-id="3b504-143">See below for details.</span></span> |


<span data-ttu-id="3b504-144">Webhook 包含 URL，並且在 hello 資料的 JSON 中格式化的承載傳送 toohello 外部服務。</span><span class="sxs-lookup"><span data-stu-id="3b504-144">Webhooks include a URL and a payload formatted in JSON that is hello data sent toohello external service.</span></span>  <span data-ttu-id="3b504-145">根據預設，hello 裝載會將包含下表中的 hello hello 值。</span><span class="sxs-lookup"><span data-stu-id="3b504-145">By default, hello payload will include hello values in hello following table.</span></span>  <span data-ttu-id="3b504-146">您可以選擇 tooreplace 自訂您自己的其中一個使用此內容。</span><span class="sxs-lookup"><span data-stu-id="3b504-146">You can choose tooreplace this payload with a custom one of your own.</span></span>  <span data-ttu-id="3b504-147">在此情況下您可以使用 hello 資料表中的 hello 變數每 hello 參數 tooinclude 其值在您的自訂承載。</span><span class="sxs-lookup"><span data-stu-id="3b504-147">In that case you can use hello variables in hello table for each of hello parameters tooinclude their value in your custom payload.</span></span>

| <span data-ttu-id="3b504-148">參數</span><span class="sxs-lookup"><span data-stu-id="3b504-148">Parameter</span></span> | <span data-ttu-id="3b504-149">變數</span><span class="sxs-lookup"><span data-stu-id="3b504-149">Variable</span></span> | <span data-ttu-id="3b504-150">說明</span><span class="sxs-lookup"><span data-stu-id="3b504-150">Description</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="3b504-151">AlertRuleName</span><span class="sxs-lookup"><span data-stu-id="3b504-151">AlertRuleName</span></span> |<span data-ttu-id="3b504-152">#alertrulename</span><span class="sxs-lookup"><span data-stu-id="3b504-152">#alertrulename</span></span> |<span data-ttu-id="3b504-153">Hello 警示規則的名稱。</span><span class="sxs-lookup"><span data-stu-id="3b504-153">Name of hello alert rule.</span></span> |
| <span data-ttu-id="3b504-154">AlertThresholdOperator</span><span class="sxs-lookup"><span data-stu-id="3b504-154">AlertThresholdOperator</span></span> |<span data-ttu-id="3b504-155">#thresholdoperator</span><span class="sxs-lookup"><span data-stu-id="3b504-155">#thresholdoperator</span></span> |<span data-ttu-id="3b504-156">Hello 警示規則的臨界值運算子。</span><span class="sxs-lookup"><span data-stu-id="3b504-156">Threshold operator for hello alert rule.</span></span>  <span data-ttu-id="3b504-157">大於或等於。</span><span class="sxs-lookup"><span data-stu-id="3b504-157">*Greater than* or *Less than*.</span></span> |
| <span data-ttu-id="3b504-158">AlertThresholdValue</span><span class="sxs-lookup"><span data-stu-id="3b504-158">AlertThresholdValue</span></span> |<span data-ttu-id="3b504-159">#thresholdvalue</span><span class="sxs-lookup"><span data-stu-id="3b504-159">#thresholdvalue</span></span> |<span data-ttu-id="3b504-160">Hello 警示規則的臨界值。</span><span class="sxs-lookup"><span data-stu-id="3b504-160">Threshold value for hello alert rule.</span></span> |
| <span data-ttu-id="3b504-161">LinkToSearchResults</span><span class="sxs-lookup"><span data-stu-id="3b504-161">LinkToSearchResults</span></span> |<span data-ttu-id="3b504-162">#linktosearchresults</span><span class="sxs-lookup"><span data-stu-id="3b504-162">#linktosearchresults</span></span> |<span data-ttu-id="3b504-163">連結 tooLog 分析記錄搜尋，傳回從建立 hello 警示的 hello 查詢 hello 記錄。</span><span class="sxs-lookup"><span data-stu-id="3b504-163">Link tooLog Analytics log search that returns hello records from hello query that created hello alert.</span></span> |
| <span data-ttu-id="3b504-164">ResultCount</span><span class="sxs-lookup"><span data-stu-id="3b504-164">ResultCount</span></span> |<span data-ttu-id="3b504-165">#searchresultcount</span><span class="sxs-lookup"><span data-stu-id="3b504-165">#searchresultcount</span></span> |<span data-ttu-id="3b504-166">Hello 搜尋結果中的記錄數目。</span><span class="sxs-lookup"><span data-stu-id="3b504-166">Number of records in hello search results.</span></span> |
| <span data-ttu-id="3b504-167">SearchIntervalEndtimeUtc</span><span class="sxs-lookup"><span data-stu-id="3b504-167">SearchIntervalEndtimeUtc</span></span> |<span data-ttu-id="3b504-168">#searchintervalendtimeutc</span><span class="sxs-lookup"><span data-stu-id="3b504-168">#searchintervalendtimeutc</span></span> |<span data-ttu-id="3b504-169">以 UTC 格式 hello 查詢的結束時間。</span><span class="sxs-lookup"><span data-stu-id="3b504-169">End time for hello query in UTC format.</span></span> |
| <span data-ttu-id="3b504-170">SearchIntervalInSeconds</span><span class="sxs-lookup"><span data-stu-id="3b504-170">SearchIntervalInSeconds</span></span> |<span data-ttu-id="3b504-171">#searchinterval</span><span class="sxs-lookup"><span data-stu-id="3b504-171">#searchinterval</span></span> |<span data-ttu-id="3b504-172">Hello 警示規則的時間間隔。</span><span class="sxs-lookup"><span data-stu-id="3b504-172">Time window for hello alert rule.</span></span> |
| <span data-ttu-id="3b504-173">SearchIntervalStartTimeUtc</span><span class="sxs-lookup"><span data-stu-id="3b504-173">SearchIntervalStartTimeUtc</span></span> |<span data-ttu-id="3b504-174">#searchintervalstarttimeutc</span><span class="sxs-lookup"><span data-stu-id="3b504-174">#searchintervalstarttimeutc</span></span> |<span data-ttu-id="3b504-175">啟動 hello 查詢時間以 UTC 格式。</span><span class="sxs-lookup"><span data-stu-id="3b504-175">Start time for hello query in UTC format.</span></span> |
| <span data-ttu-id="3b504-176">SearchQuery</span><span class="sxs-lookup"><span data-stu-id="3b504-176">SearchQuery</span></span> |<span data-ttu-id="3b504-177">#searchquery</span><span class="sxs-lookup"><span data-stu-id="3b504-177">#searchquery</span></span> |<span data-ttu-id="3b504-178">Hello 警示規則所用的記錄搜尋查詢。</span><span class="sxs-lookup"><span data-stu-id="3b504-178">Log search query used by hello alert rule.</span></span> |
| <span data-ttu-id="3b504-179">SearchResults</span><span class="sxs-lookup"><span data-stu-id="3b504-179">SearchResults</span></span> |<span data-ttu-id="3b504-180">請參閱下方</span><span class="sxs-lookup"><span data-stu-id="3b504-180">See below</span></span> |<span data-ttu-id="3b504-181">JSON 格式中的 hello 查詢所傳回的記錄。</span><span class="sxs-lookup"><span data-stu-id="3b504-181">Records returned by hello query in JSON format.</span></span>  <span data-ttu-id="3b504-182">有限的 toohello 5000 第一次記錄。</span><span class="sxs-lookup"><span data-stu-id="3b504-182">Limited toohello first 5,000 records.</span></span> |
| <span data-ttu-id="3b504-183">WorkspaceID</span><span class="sxs-lookup"><span data-stu-id="3b504-183">WorkspaceID</span></span> |<span data-ttu-id="3b504-184">#workspaceid</span><span class="sxs-lookup"><span data-stu-id="3b504-184">#workspaceid</span></span> |<span data-ttu-id="3b504-185">OMS 工作區的識別碼。</span><span class="sxs-lookup"><span data-stu-id="3b504-185">ID of your OMS workspace.</span></span> |

<span data-ttu-id="3b504-186">例如，您可以指定下列自訂承載包含單一參數來呼叫 hello*文字*。</span><span class="sxs-lookup"><span data-stu-id="3b504-186">For example, you might specify hello following custom payload that includes a single parameter called *text*.</span></span>  <span data-ttu-id="3b504-187">此 webhook 呼叫 hello 服務會需要此參數。</span><span class="sxs-lookup"><span data-stu-id="3b504-187">hello service that this webhook calls would be expecting this parameter.</span></span>

    {
        "text":"#alertrulename fired with #searchresultcount over threshold of #thresholdvalue."
    }

<span data-ttu-id="3b504-188">這個範例裝載會解析 toosomething 像 hello 遵循時傳送 toohello webhook。</span><span class="sxs-lookup"><span data-stu-id="3b504-188">This example payload would resolve toosomething like hello following when sent toohello webhook.</span></span>

    {
        "text":"My Alert Rule fired with 18 records over threshold of 10 ."
    }

<span data-ttu-id="3b504-189">tooinclude 搜尋結果中自訂內容，新增以下為最上層屬性 hello json 承載中的 hello。</span><span class="sxs-lookup"><span data-stu-id="3b504-189">tooinclude search results in a custom payload, add hello following line as a top level property in hello json payload.</span></span>  

    "IncludeSearchResults":true

<span data-ttu-id="3b504-190">例如，toocreate 包含只 hello 警示的名稱和 hello 搜尋結果的自訂內容，您可以使用下列的 hello。</span><span class="sxs-lookup"><span data-stu-id="3b504-190">For example, toocreate a custom payload that includes just hello alert name and hello search results, you could use hello following.</span></span> 

    {
       "alertname":"#alertrulename",
       "IncludeSearchResults":true
    }


<span data-ttu-id="3b504-191">您可以逐步完成使用 webhook toostart 外部服務在建立警示規則的完整範例[OMS 記錄分析 toosend 訊息 tooSlack 中建立警示的 webhook 動作](log-analytics-alerts-webhooks.md)。</span><span class="sxs-lookup"><span data-stu-id="3b504-191">You can walk through a complete example of creating an alert rule with a webhook toostart an external service at [Create an alert webhook action in OMS Log Analytics toosend message tooSlack](log-analytics-alerts-webhooks.md).</span></span>

## <a name="runbook-actions"></a><span data-ttu-id="3b504-192">Runbook 動作</span><span class="sxs-lookup"><span data-stu-id="3b504-192">Runbook actions</span></span>
<span data-ttu-id="3b504-193">Runbook 動作可在 Azure 自動化中啟動 Runbook。</span><span class="sxs-lookup"><span data-stu-id="3b504-193">Runbook actions start a runbook in Azure Automation.</span></span>  <span data-ttu-id="3b504-194">若要 toouse 這種類型的動作，您必須具有 hello[自動化解決方案](log-analytics-add-solutions.md)OMS 工作區中安裝並設定。</span><span class="sxs-lookup"><span data-stu-id="3b504-194">In order toouse this type of action, you must have hello [Automation solution](log-analytics-add-solutions.md) installed and configured in your OMS workspace.</span></span>  <span data-ttu-id="3b504-195">您可以選取從您設定在 hello 自動化解決方案中的 hello 自動化帳戶中的 hello runbook。</span><span class="sxs-lookup"><span data-stu-id="3b504-195">You can select from hello runbooks in hello automation account that you configured in hello Automation solution.</span></span>

<span data-ttu-id="3b504-196">Runbook 動作需要 hello 下表中的 hello 屬性。</span><span class="sxs-lookup"><span data-stu-id="3b504-196">Runbook actions require hello properties in hello following table.</span></span>

| <span data-ttu-id="3b504-197">屬性</span><span class="sxs-lookup"><span data-stu-id="3b504-197">Property</span></span> | <span data-ttu-id="3b504-198">說明</span><span class="sxs-lookup"><span data-stu-id="3b504-198">Description</span></span> |
|:--- |:---|
| <span data-ttu-id="3b504-199">Runbook</span><span class="sxs-lookup"><span data-stu-id="3b504-199">Runbook</span></span> | <span data-ttu-id="3b504-200">建立警示時，想要 toostart 的 Runbook。</span><span class="sxs-lookup"><span data-stu-id="3b504-200">Runbook that you want toostart when an alert is created.</span></span> |
| <span data-ttu-id="3b504-201">執行位置</span><span class="sxs-lookup"><span data-stu-id="3b504-201">Run on</span></span> | <span data-ttu-id="3b504-202">指定**Azure** toorun hello runbook hello 雲端中的。</span><span class="sxs-lookup"><span data-stu-id="3b504-202">Specify **Azure** toorun hello runbook in hello cloud.</span></span>  <span data-ttu-id="3b504-203">指定**Hybrid worker** toorun hello runbook 上的代理程式[Hybrid Runbook Worker](../automation/automation-hybrid-runbook-worker.md )安裝。</span><span class="sxs-lookup"><span data-stu-id="3b504-203">Specify **Hybrid worker** toorun hello runbook on an agent with [Hybrid Runbook Worker](../automation/automation-hybrid-runbook-worker.md ) installed.</span></span>  |

<span data-ttu-id="3b504-204">Hello runbook 使用的 Runbook 動作啟動[webhook](../automation/automation-webhooks.md)。</span><span class="sxs-lookup"><span data-stu-id="3b504-204">Runbook actions start hello runbook using a [webhook](../automation/automation-webhooks.md).</span></span>  <span data-ttu-id="3b504-205">當您建立 hello 警示規則時，就會自動以 hello 名稱建立新的 webhook hello runbook **OMS 警示補救**後面跟著 GUID。</span><span class="sxs-lookup"><span data-stu-id="3b504-205">When you create hello alert rule, it will automatically create a new webhook for hello runbook with hello name **OMS Alert Remediation** followed by a GUID.</span></span>  

<span data-ttu-id="3b504-206">您無法直接填入 hello runbook 的任何參數，但是 hello [$WebhookData 參數](../automation/automation-webhooks.md)將包含 hello hello 警示，包括 hello hello 建立它的記錄搜尋結果的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="3b504-206">You cannot directly populate any parameters of hello runbook, but hello [$WebhookData parameter](../automation/automation-webhooks.md) will include hello details of hello alert, including hello results of hello log search that created it.</span></span>  <span data-ttu-id="3b504-207">hello runbook 將需要 toodefine **$WebhookData**做為其參數 tooaccess hello hello 警示的內容。</span><span class="sxs-lookup"><span data-stu-id="3b504-207">hello runbook will need toodefine **$WebhookData** as a parameter for it tooaccess hello properties of hello alert.</span></span>  <span data-ttu-id="3b504-208">hello 警示資料可在呼叫的單一屬性的 json 格式**SearchResults**在 hello **RequestBody**屬性**$WebhookData**。</span><span class="sxs-lookup"><span data-stu-id="3b504-208">hello alert data is available in json format in a single property called **SearchResults** in hello **RequestBody** property of **$WebhookData**.</span></span>  <span data-ttu-id="3b504-209">這會有與 hello 下表中的 hello 屬性。</span><span class="sxs-lookup"><span data-stu-id="3b504-209">This will have with hello properties in hello following table.</span></span>

| <span data-ttu-id="3b504-210">節點</span><span class="sxs-lookup"><span data-stu-id="3b504-210">Node</span></span> | <span data-ttu-id="3b504-211">說明</span><span class="sxs-lookup"><span data-stu-id="3b504-211">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="3b504-212">id</span><span class="sxs-lookup"><span data-stu-id="3b504-212">id</span></span> |<span data-ttu-id="3b504-213">路徑和 hello 搜尋的 GUID。</span><span class="sxs-lookup"><span data-stu-id="3b504-213">Path and GUID of hello search.</span></span> |
| <span data-ttu-id="3b504-214">__metadata</span><span class="sxs-lookup"><span data-stu-id="3b504-214">__metadata</span></span> |<span data-ttu-id="3b504-215">Hello 警示包括 hello 數目的記錄和狀態的 hello 搜尋結果的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="3b504-215">Information about hello alert including hello number of records and status of hello search results.</span></span> |
| <span data-ttu-id="3b504-216">value</span><span class="sxs-lookup"><span data-stu-id="3b504-216">value</span></span> |<span data-ttu-id="3b504-217">Hello 搜尋結果中的每一筆記錄的個別項目。</span><span class="sxs-lookup"><span data-stu-id="3b504-217">Separate entry for each record in hello search results.</span></span>  <span data-ttu-id="3b504-218">hello 屬性和 hello 記錄的值，會比對 hello 項目的 hello 詳細資料。</span><span class="sxs-lookup"><span data-stu-id="3b504-218">hello details of hello entry will match hello properties and values of hello record.</span></span> |

<span data-ttu-id="3b504-219">比方說，hello 下列 runbook 會擷取 hello hello 記錄搜尋所傳回的記錄，並指派不同的屬性，根據每一筆記錄的 hello 類型。</span><span class="sxs-lookup"><span data-stu-id="3b504-219">For example, hello following runbook would extract hello records returned by hello log search  and assign different properties based on hello type of each record.</span></span>  <span data-ttu-id="3b504-220">請注意該 hello runbook 啟動轉換**RequestBody**從 json，因此它可以當作 PowerShell 中的物件。</span><span class="sxs-lookup"><span data-stu-id="3b504-220">Note that hello runbook starts by converting **RequestBody** from json so that it can be worked with as an object in PowerShell.</span></span>

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


## <a name="next-steps"></a><span data-ttu-id="3b504-221">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3b504-221">Next steps</span></span>
- <span data-ttu-id="3b504-222">完成 [設定 Webook](log-analytics-alerts-webhooks.md) 和警示規則的逐步解說。</span><span class="sxs-lookup"><span data-stu-id="3b504-222">Complete a walkthrough for [configuring a webook](log-analytics-alerts-webhooks.md) with an alert rule.</span></span>  
- <span data-ttu-id="3b504-223">深入了解如何 toowrite [Azure 自動化中的 runbook](https://azure.microsoft.com/documentation/services/automation) tooremediate 警示所識別的問題。</span><span class="sxs-lookup"><span data-stu-id="3b504-223">Learn how toowrite [runbooks in Azure Automation](https://azure.microsoft.com/documentation/services/automation) tooremediate problems identified by alerts.</span></span>
