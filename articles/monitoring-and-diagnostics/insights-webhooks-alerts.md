---
title: "針對 Azure 度量警示設定 Webhook | Microsoft Docs"
description: "重設 Azure 警示的路徑到其他非 Azure 系統。"
author: johnkemnetz
manager: carmonm
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 8b3ae540-1d19-4f3d-a635-376042f8a5bb
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/03/2017
ms.author: johnkem
ms.openlocfilehash: 1a885166e5c71f13da222bfc22b0fc579096c52f
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="configure-a-webhook-on-an-azure-metric-alert"></a><span data-ttu-id="f3c18-103">針對 Azure 度量警示設定 Webhook</span><span class="sxs-lookup"><span data-stu-id="f3c18-103">Configure a webhook on an Azure metric alert</span></span>
<span data-ttu-id="f3c18-104">Webhook 可讓您將 Azure 警示通知路由到其他系統以進行後處理或自訂動作。</span><span class="sxs-lookup"><span data-stu-id="f3c18-104">Webhooks allow you to route an Azure alert notification to other systems for post-processing or custom actions.</span></span> <span data-ttu-id="f3c18-105">您可以針對警示使用 Webhook，以將警示路由到會傳送簡訊、記錄錯誤、透過聊天/傳訊服務通知小組，或進行任意數量之其他動作的服務。</span><span class="sxs-lookup"><span data-stu-id="f3c18-105">You can use a webhook on an alert to route it to services that send SMS, log bugs, notify a team via chat/messaging services, or do any number of other actions.</span></span> <span data-ttu-id="f3c18-106">本文說明如何針對 Azure 度量警示設定 Webhook，並說明 HTTP POST 對 Webhook 之承載的樣貌。</span><span class="sxs-lookup"><span data-stu-id="f3c18-106">This article describes how to set a webhook on an Azure metric alert and what the payload for the HTTP POST to a webhook looks like.</span></span> <span data-ttu-id="f3c18-107">如需有關 Azure 活動記錄警示 (事件警示) 之設定和結構描述的資訊， [請改為參閱本頁](insights-auditlog-to-webhook-email.md)。</span><span class="sxs-lookup"><span data-stu-id="f3c18-107">For information on the setup and schema for an Azure Activity Log alert (alert on events), [see this page instead](insights-auditlog-to-webhook-email.md).</span></span>

<span data-ttu-id="f3c18-108">Azure 警示會將警示內容以 JSON 格式 (定義如下的結構描述) HTTP POST 到您在建立警示時提供的 Webhook URI。</span><span class="sxs-lookup"><span data-stu-id="f3c18-108">Azure alerts HTTP POST the alert contents in JSON format, schema defined below, to a webhook URI that you provide when creating the alert.</span></span> <span data-ttu-id="f3c18-109">此 URI 必須是有效的 HTTP 或 HTTPS 端點。</span><span class="sxs-lookup"><span data-stu-id="f3c18-109">This URI must be a valid HTTP or HTTPS endpoint.</span></span> <span data-ttu-id="f3c18-110">當警示啟動時，Azure 會針對每個要求張貼一個項目。</span><span class="sxs-lookup"><span data-stu-id="f3c18-110">Azure posts one entry per request when an alert is activated.</span></span>

## <a name="configuring-webhooks-via-the-portal"></a><span data-ttu-id="f3c18-111">透過入口網站設定 Webhook</span><span class="sxs-lookup"><span data-stu-id="f3c18-111">Configuring webhooks via the portal</span></span>
<span data-ttu-id="f3c18-112">您可以在 [入口網站](https://portal.azure.com/)的 [建立/更新警示] 畫面中新增或更新 Webhook URI。</span><span class="sxs-lookup"><span data-stu-id="f3c18-112">You can add or update the webhook URI in the Create/Update Alerts screen in the [portal](https://portal.azure.com/).</span></span>

![新增警示規則](./media/insights-webhooks-alerts/Alertwebhook.png)

<span data-ttu-id="f3c18-114">您也可以使用 [Azure PowerShell Cmdlet](insights-powershell-samples.md#create-metric-alerts)、[跨平台 CLI](insights-cli-samples.md#work-with-alerts) 或 [Azure 監視器 REST API](https://msdn.microsoft.com/library/azure/dn933805.aspx) 設定警示以張貼至 Webhook URI。</span><span class="sxs-lookup"><span data-stu-id="f3c18-114">You can also configure an alert to post to a webhook URI using the [Azure PowerShell Cmdlets](insights-powershell-samples.md#create-metric-alerts), [Cross-Platform CLI](insights-cli-samples.md#work-with-alerts), or [Azure Monitor REST API](https://msdn.microsoft.com/library/azure/dn933805.aspx).</span></span>

## <a name="authenticating-the-webhook"></a><span data-ttu-id="f3c18-115">驗證 Webhook</span><span class="sxs-lookup"><span data-stu-id="f3c18-115">Authenticating the webhook</span></span>
<span data-ttu-id="f3c18-116">Webhook 可以使用權杖型授權來驗證。</span><span class="sxs-lookup"><span data-stu-id="f3c18-116">The webhook can authenticate using token-based authorization.</span></span> <span data-ttu-id="f3c18-117">Webhook URI 是以權杖識別碼儲存，例如</span><span class="sxs-lookup"><span data-stu-id="f3c18-117">The webhook URI is saved with a token ID, eg.</span></span> `https://mysamplealert/webcallback?tokenid=sometokenid&someparameter=somevalue`

## <a name="payload-schema"></a><span data-ttu-id="f3c18-118">承載結構描述</span><span class="sxs-lookup"><span data-stu-id="f3c18-118">Payload schema</span></span>
<span data-ttu-id="f3c18-119">POST 作業對於所有以計量為基礎的警示會包含下列 JSON 承載和結構描述。</span><span class="sxs-lookup"><span data-stu-id="f3c18-119">The POST operation contains the following JSON payload and schema for all metric-based alerts.</span></span>

```JSON
{
"status": "Activated",
"context": {
            "timestamp": "2015-08-14T22:26:41.9975398Z",
            "id": "/subscriptions/s1/resourceGroups/useast/providers/microsoft.insights/alertrules/ruleName1",
            "name": "ruleName1",
            "description": "some description",
            "conditionType": "Metric",
            "condition": {
                        "metricName": "Requests",
                        "metricUnit": "Count",
                        "metricValue": "10",
                        "threshold": "10",
                        "windowSize": "15",
                        "timeAggregation": "Average",
                        "operator": "GreaterThanOrEqual"
                },
            "subscriptionId": "s1",
            "resourceGroupName": "useast",                                
            "resourceName": "mysite1",
            "resourceType": "microsoft.foo/sites",
            "resourceId": "/subscriptions/s1/resourceGroups/useast/providers/microsoft.foo/sites/mysite1",
            "resourceRegion": "centralus",
            "portalLink": "https://portal.azure.com/#resource/subscriptions/s1/resourceGroups/useast/providers/microsoft.foo/sites/mysite1"
},
"properties": {
              "key1": "value1",
              "key2": "value2"
              }
}
```


| <span data-ttu-id="f3c18-120">欄位</span><span class="sxs-lookup"><span data-stu-id="f3c18-120">Field</span></span> | <span data-ttu-id="f3c18-121">強制</span><span class="sxs-lookup"><span data-stu-id="f3c18-121">Mandatory</span></span> | <span data-ttu-id="f3c18-122">一組固定值</span><span class="sxs-lookup"><span data-stu-id="f3c18-122">Fixed Set of Values</span></span> | <span data-ttu-id="f3c18-123">注意事項</span><span class="sxs-lookup"><span data-stu-id="f3c18-123">Notes</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="f3c18-124">status</span><span class="sxs-lookup"><span data-stu-id="f3c18-124">status</span></span> |<span data-ttu-id="f3c18-125">Y</span><span class="sxs-lookup"><span data-stu-id="f3c18-125">Y</span></span> |<span data-ttu-id="f3c18-126">“Activated”、“Resolved”</span><span class="sxs-lookup"><span data-stu-id="f3c18-126">“Activated”, “Resolved”</span></span> |<span data-ttu-id="f3c18-127">以您設定的條件為基礎的警示狀態。</span><span class="sxs-lookup"><span data-stu-id="f3c18-127">Status for the alert based off of the conditions you have set.</span></span> |
| <span data-ttu-id="f3c18-128">context</span><span class="sxs-lookup"><span data-stu-id="f3c18-128">context</span></span> |<span data-ttu-id="f3c18-129">Y</span><span class="sxs-lookup"><span data-stu-id="f3c18-129">Y</span></span> | |<span data-ttu-id="f3c18-130">警示內容。</span><span class="sxs-lookup"><span data-stu-id="f3c18-130">The alert context.</span></span> |
| <span data-ttu-id="f3c18-131">timestamp</span><span class="sxs-lookup"><span data-stu-id="f3c18-131">timestamp</span></span> |<span data-ttu-id="f3c18-132">Y</span><span class="sxs-lookup"><span data-stu-id="f3c18-132">Y</span></span> | |<span data-ttu-id="f3c18-133">警示觸發的時間。</span><span class="sxs-lookup"><span data-stu-id="f3c18-133">The time at which the alert was triggered.</span></span> |
| <span data-ttu-id="f3c18-134">id</span><span class="sxs-lookup"><span data-stu-id="f3c18-134">id</span></span> |<span data-ttu-id="f3c18-135">Y</span><span class="sxs-lookup"><span data-stu-id="f3c18-135">Y</span></span> | |<span data-ttu-id="f3c18-136">每個警示規則都有唯一的識別碼。</span><span class="sxs-lookup"><span data-stu-id="f3c18-136">Every alert rule has a unique id.</span></span> |
| <span data-ttu-id="f3c18-137">名稱</span><span class="sxs-lookup"><span data-stu-id="f3c18-137">name</span></span> |<span data-ttu-id="f3c18-138">Y</span><span class="sxs-lookup"><span data-stu-id="f3c18-138">Y</span></span> | |<span data-ttu-id="f3c18-139">警示名稱。</span><span class="sxs-lookup"><span data-stu-id="f3c18-139">The alert name.</span></span> |
| <span data-ttu-id="f3c18-140">說明</span><span class="sxs-lookup"><span data-stu-id="f3c18-140">description</span></span> |<span data-ttu-id="f3c18-141">Y</span><span class="sxs-lookup"><span data-stu-id="f3c18-141">Y</span></span> | |<span data-ttu-id="f3c18-142">警示的描述。</span><span class="sxs-lookup"><span data-stu-id="f3c18-142">Description of the alert.</span></span> |
| <span data-ttu-id="f3c18-143">conditionType</span><span class="sxs-lookup"><span data-stu-id="f3c18-143">conditionType</span></span> |<span data-ttu-id="f3c18-144">Y</span><span class="sxs-lookup"><span data-stu-id="f3c18-144">Y</span></span> |<span data-ttu-id="f3c18-145">“Metric”、“Event”</span><span class="sxs-lookup"><span data-stu-id="f3c18-145">“Metric”, “Event”</span></span> |<span data-ttu-id="f3c18-146">支援兩種類型的警示。</span><span class="sxs-lookup"><span data-stu-id="f3c18-146">Two types of alerts are supported.</span></span> <span data-ttu-id="f3c18-147">一種根據度量條件，另一種根據活動記錄中的事件。</span><span class="sxs-lookup"><span data-stu-id="f3c18-147">One based on a metric condition and the other based on an event in the Activity Log.</span></span> <span data-ttu-id="f3c18-148">使用此值來檢查警示是根據度量或事件。</span><span class="sxs-lookup"><span data-stu-id="f3c18-148">Use this value to check if the alert is based on metric or event.</span></span> |
| <span data-ttu-id="f3c18-149">condition</span><span class="sxs-lookup"><span data-stu-id="f3c18-149">condition</span></span> |<span data-ttu-id="f3c18-150">Y</span><span class="sxs-lookup"><span data-stu-id="f3c18-150">Y</span></span> | |<span data-ttu-id="f3c18-151">根據 conditionType 所要檢查的特定欄位。</span><span class="sxs-lookup"><span data-stu-id="f3c18-151">The specific fields to check for based on the conditionType.</span></span> |
| <span data-ttu-id="f3c18-152">metricName</span><span class="sxs-lookup"><span data-stu-id="f3c18-152">metricName</span></span> |<span data-ttu-id="f3c18-153">用於計量警示</span><span class="sxs-lookup"><span data-stu-id="f3c18-153">for Metric alerts</span></span> | |<span data-ttu-id="f3c18-154">定義規則所監視的計量名稱。</span><span class="sxs-lookup"><span data-stu-id="f3c18-154">The name of the metric that defines what the rule monitors.</span></span> |
| <span data-ttu-id="f3c18-155">metricUnit</span><span class="sxs-lookup"><span data-stu-id="f3c18-155">metricUnit</span></span> |<span data-ttu-id="f3c18-156">用於計量警示</span><span class="sxs-lookup"><span data-stu-id="f3c18-156">for Metric alerts</span></span> |<span data-ttu-id="f3c18-157">"Bytes"、"BytesPerSecond"、"Count"、"CountPerSecond"、"Percent"、"Seconds"</span><span class="sxs-lookup"><span data-stu-id="f3c18-157">"Bytes", "BytesPerSecond", "Count", "CountPerSecond", "Percent", "Seconds"</span></span> |<span data-ttu-id="f3c18-158">計量允許的單位。</span><span class="sxs-lookup"><span data-stu-id="f3c18-158">The unit allowed in the metric.</span></span> <span data-ttu-id="f3c18-159">[允許的值在此列出](https://msdn.microsoft.com/library/microsoft.azure.insights.models.unit.aspx)。</span><span class="sxs-lookup"><span data-stu-id="f3c18-159">[Allowed values are listed here](https://msdn.microsoft.com/library/microsoft.azure.insights.models.unit.aspx).</span></span> |
| <span data-ttu-id="f3c18-160">metricValue</span><span class="sxs-lookup"><span data-stu-id="f3c18-160">metricValue</span></span> |<span data-ttu-id="f3c18-161">用於計量警示</span><span class="sxs-lookup"><span data-stu-id="f3c18-161">for Metric alerts</span></span> | |<span data-ttu-id="f3c18-162">造成警示的計量實際值。</span><span class="sxs-lookup"><span data-stu-id="f3c18-162">The actual value of the metric that caused the alert.</span></span> |
| <span data-ttu-id="f3c18-163">threshold</span><span class="sxs-lookup"><span data-stu-id="f3c18-163">threshold</span></span> |<span data-ttu-id="f3c18-164">用於計量警示</span><span class="sxs-lookup"><span data-stu-id="f3c18-164">for Metric alerts</span></span> | |<span data-ttu-id="f3c18-165">會啟動警示的臨界值。</span><span class="sxs-lookup"><span data-stu-id="f3c18-165">The threshold value at which the alert is activated.</span></span> |
| <span data-ttu-id="f3c18-166">windowSize</span><span class="sxs-lookup"><span data-stu-id="f3c18-166">windowSize</span></span> |<span data-ttu-id="f3c18-167">用於計量警示</span><span class="sxs-lookup"><span data-stu-id="f3c18-167">for Metric alerts</span></span> | |<span data-ttu-id="f3c18-168">根據 threshold 用來監視警示活動的時間長度。</span><span class="sxs-lookup"><span data-stu-id="f3c18-168">The period of time that is used to monitor alert activity based on the threshold.</span></span> <span data-ttu-id="f3c18-169">必須介於 5 分鐘到 1 天之間。</span><span class="sxs-lookup"><span data-stu-id="f3c18-169">Must be between 5 minutes and 1 day.</span></span> <span data-ttu-id="f3c18-170">ISO 8601 持續時間格式。</span><span class="sxs-lookup"><span data-stu-id="f3c18-170">ISO 8601 duration format.</span></span> |
| <span data-ttu-id="f3c18-171">timeAggregation</span><span class="sxs-lookup"><span data-stu-id="f3c18-171">timeAggregation</span></span> |<span data-ttu-id="f3c18-172">用於計量警示</span><span class="sxs-lookup"><span data-stu-id="f3c18-172">for Metric alerts</span></span> |<span data-ttu-id="f3c18-173">"Average"、"Last"、"Maximum"、"Minimum"、"None"、"Total"</span><span class="sxs-lookup"><span data-stu-id="f3c18-173">"Average", "Last", "Maximum", "Minimum", "None", "Total"</span></span> |<span data-ttu-id="f3c18-174">收集的資料應如何隨著時間結合。</span><span class="sxs-lookup"><span data-stu-id="f3c18-174">How the data that is collected should be combined over time.</span></span> <span data-ttu-id="f3c18-175">預設值為 Average。</span><span class="sxs-lookup"><span data-stu-id="f3c18-175">The default value is Average.</span></span> <span data-ttu-id="f3c18-176">[允許的值在此列出](https://msdn.microsoft.com/library/microsoft.azure.insights.models.aggregationtype.aspx)。</span><span class="sxs-lookup"><span data-stu-id="f3c18-176">[Allowed values are listed here](https://msdn.microsoft.com/library/microsoft.azure.insights.models.aggregationtype.aspx).</span></span> |
| <span data-ttu-id="f3c18-177">operator</span><span class="sxs-lookup"><span data-stu-id="f3c18-177">operator</span></span> |<span data-ttu-id="f3c18-178">用於計量警示</span><span class="sxs-lookup"><span data-stu-id="f3c18-178">for Metric alerts</span></span> | |<span data-ttu-id="f3c18-179">用來比較目前之度量資料與設定之臨界值的運算子。</span><span class="sxs-lookup"><span data-stu-id="f3c18-179">The operator used to compare the current metric data to the set threshold.</span></span> |
| <span data-ttu-id="f3c18-180">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="f3c18-180">subscriptionId</span></span> |<span data-ttu-id="f3c18-181">Y</span><span class="sxs-lookup"><span data-stu-id="f3c18-181">Y</span></span> | |<span data-ttu-id="f3c18-182">Azure 訂用帳戶識別碼。</span><span class="sxs-lookup"><span data-stu-id="f3c18-182">Azure subscription ID.</span></span> |
| <span data-ttu-id="f3c18-183">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="f3c18-183">resourceGroupName</span></span> |<span data-ttu-id="f3c18-184">Y</span><span class="sxs-lookup"><span data-stu-id="f3c18-184">Y</span></span> | |<span data-ttu-id="f3c18-185">受影響資源的資源群組的名稱。</span><span class="sxs-lookup"><span data-stu-id="f3c18-185">Name of the resource group for the impacted resource.</span></span> |
| <span data-ttu-id="f3c18-186">resourceName</span><span class="sxs-lookup"><span data-stu-id="f3c18-186">resourceName</span></span> |<span data-ttu-id="f3c18-187">Y</span><span class="sxs-lookup"><span data-stu-id="f3c18-187">Y</span></span> | |<span data-ttu-id="f3c18-188">受影響資源的資源名稱。</span><span class="sxs-lookup"><span data-stu-id="f3c18-188">Resource name of the impacted resource.</span></span> |
| <span data-ttu-id="f3c18-189">resourceType</span><span class="sxs-lookup"><span data-stu-id="f3c18-189">resourceType</span></span> |<span data-ttu-id="f3c18-190">Y</span><span class="sxs-lookup"><span data-stu-id="f3c18-190">Y</span></span> | |<span data-ttu-id="f3c18-191">受影響資源的資源類型。</span><span class="sxs-lookup"><span data-stu-id="f3c18-191">Resource type of the impacted resource.</span></span> |
| <span data-ttu-id="f3c18-192">resourceId</span><span class="sxs-lookup"><span data-stu-id="f3c18-192">resourceId</span></span> |<span data-ttu-id="f3c18-193">Y</span><span class="sxs-lookup"><span data-stu-id="f3c18-193">Y</span></span> | |<span data-ttu-id="f3c18-194">受影響資源的資源識別碼。</span><span class="sxs-lookup"><span data-stu-id="f3c18-194">Resource ID of the impacted resource.</span></span> |
| <span data-ttu-id="f3c18-195">resourceRegion</span><span class="sxs-lookup"><span data-stu-id="f3c18-195">resourceRegion</span></span> |<span data-ttu-id="f3c18-196">Y</span><span class="sxs-lookup"><span data-stu-id="f3c18-196">Y</span></span> | |<span data-ttu-id="f3c18-197">受影響資源的區域或位置。</span><span class="sxs-lookup"><span data-stu-id="f3c18-197">Region or location of the impacted resource.</span></span> |
| <span data-ttu-id="f3c18-198">portalLink</span><span class="sxs-lookup"><span data-stu-id="f3c18-198">portalLink</span></span> |<span data-ttu-id="f3c18-199">Y</span><span class="sxs-lookup"><span data-stu-id="f3c18-199">Y</span></span> | |<span data-ttu-id="f3c18-200">入口網站資源摘要頁面的直接連結。</span><span class="sxs-lookup"><span data-stu-id="f3c18-200">Direct link to the portal resource summary page.</span></span> |
| <span data-ttu-id="f3c18-201">屬性</span><span class="sxs-lookup"><span data-stu-id="f3c18-201">properties</span></span> |<span data-ttu-id="f3c18-202">N</span><span class="sxs-lookup"><span data-stu-id="f3c18-202">N</span></span> |<span data-ttu-id="f3c18-203">選用</span><span class="sxs-lookup"><span data-stu-id="f3c18-203">Optional</span></span> |<span data-ttu-id="f3c18-204">一組包含事件相關詳細資料的 `<Key, Value>` 配對 (也就是 `Dictionary<String, String>`)。</span><span class="sxs-lookup"><span data-stu-id="f3c18-204">Set of `<Key, Value>` pairs (i.e. `Dictionary<String, String>`) that includes details about the event.</span></span> <span data-ttu-id="f3c18-205">properties 欄位是選擇性的。</span><span class="sxs-lookup"><span data-stu-id="f3c18-205">The properties field is optional.</span></span> <span data-ttu-id="f3c18-206">在自訂 UI 或邏輯應用程式的工作流程中，使用者可以輸入可透過承載傳遞的索引鍵/值。</span><span class="sxs-lookup"><span data-stu-id="f3c18-206">In a custom UI or Logic app-based workflow, users can enter key/values that can be passed via the payload.</span></span> <span data-ttu-id="f3c18-207">另一種將自訂屬性傳回給 Webhook 的替代方式是透過 Webhook URI 本身 (做為查詢參數)</span><span class="sxs-lookup"><span data-stu-id="f3c18-207">The alternate way to pass custom properties back to the webhook is via the webhook uri itself (as query parameters)</span></span> |

> [!NOTE]
> <span data-ttu-id="f3c18-208">屬性欄位只能使用 [Azure 監視器 REST API](https://msdn.microsoft.com/library/azure/dn933805.aspx) 設定。</span><span class="sxs-lookup"><span data-stu-id="f3c18-208">The properties field can only be set using the [Azure Monitor REST API](https://msdn.microsoft.com/library/azure/dn933805.aspx).</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="f3c18-209">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f3c18-209">Next steps</span></span>
* <span data-ttu-id="f3c18-210">請觀賞 [使用 PagerDuty 整合 Azure 警示](http://go.microsoft.com/fwlink/?LinkId=627080)</span><span class="sxs-lookup"><span data-stu-id="f3c18-210">Learn more about Azure alerts and webhooks in the video [Integrate Azure Alerts with PagerDuty](http://go.microsoft.com/fwlink/?LinkId=627080)</span></span>
* [<span data-ttu-id="f3c18-211">對 Azure 警示執行 Azure 自動化指令碼 (Runbook)</span><span class="sxs-lookup"><span data-stu-id="f3c18-211">Execute Azure Automation scripts (Runbooks) on Azure alerts</span></span>](http://go.microsoft.com/fwlink/?LinkId=627081)
* [<span data-ttu-id="f3c18-212">使用邏輯應用程式透過 Twilio 從 Azure 警示傳送簡訊</span><span class="sxs-lookup"><span data-stu-id="f3c18-212">Use Logic App to send an SMS via Twilio from an Azure alert</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-text-message-with-logic-app)
* [<span data-ttu-id="f3c18-213">使用邏輯應用程式從 Azure 警示傳送 Slack 訊息</span><span class="sxs-lookup"><span data-stu-id="f3c18-213">Use Logic App to send a Slack message from an Azure alert</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-slack-with-logic-app)
* [<span data-ttu-id="f3c18-214">使用邏輯應用程式從 Azure 警示傳送訊息到 Azure 佇列</span><span class="sxs-lookup"><span data-stu-id="f3c18-214">Use Logic App to send a message to an Azure Queue from an Azure alert</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-queue-with-logic-app)
