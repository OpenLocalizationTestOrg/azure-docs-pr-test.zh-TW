---
title: "了解活動記錄警示中使用的 Webhook 結構描述 | Microsoft Docs"
description: "深入了解活動記錄警示啟動時，張貼至 Webhook URL 的 JSON 結構描述。"
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: johnkem
ms.openlocfilehash: 75c71bcd16573d4f4dd3377c623aa9b414aa3906
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="webhooks-for-azure-activity-log-alerts"></a><span data-ttu-id="1dc22-103">Azure 活動記錄警示的 Webhook</span><span class="sxs-lookup"><span data-stu-id="1dc22-103">Webhooks for Azure activity log alerts</span></span>
<span data-ttu-id="1dc22-104">在定義動作群組的過程中，您可以設定 Webhook 端點以接收活動記錄警示通知。</span><span class="sxs-lookup"><span data-stu-id="1dc22-104">As part of the definition of an action group, you can configure webhook endpoints to receive activity log alert notifications.</span></span> <span data-ttu-id="1dc22-105">您可以使用 Webhook 將這些通知路由到其他系統，以進行後置處理或自訂動作。</span><span class="sxs-lookup"><span data-stu-id="1dc22-105">With webhooks, you can route these notifications to other systems for post-processing or custom actions.</span></span> <span data-ttu-id="1dc22-106">本文會說明 HTTP POST 至 Webhook 的承載資料樣貌。</span><span class="sxs-lookup"><span data-stu-id="1dc22-106">This article shows what the payload for the HTTP POST to a webhook looks like.</span></span>

<span data-ttu-id="1dc22-107">如需有關活動記錄警示的詳細資訊，請參閱如何[建立 Azure 活動記錄警示](monitoring-activity-log-alerts.md)。</span><span class="sxs-lookup"><span data-stu-id="1dc22-107">For more information on activity log alerts, see how to [create Azure activity log alerts](monitoring-activity-log-alerts.md).</span></span>

<span data-ttu-id="1dc22-108">如需有關動作群組的資訊，請參閱如何[建立動作群組](monitoring-action-groups.md)。</span><span class="sxs-lookup"><span data-stu-id="1dc22-108">For information on action groups, see how to [create action groups](monitoring-action-groups.md).</span></span>

## <a name="authenticate-the-webhook"></a><span data-ttu-id="1dc22-109">驗證 Webhook</span><span class="sxs-lookup"><span data-stu-id="1dc22-109">Authenticate the webhook</span></span>
<span data-ttu-id="1dc22-110">Webhook 可以選擇使用以權杖作為基礎的授權來進行驗證。</span><span class="sxs-lookup"><span data-stu-id="1dc22-110">The webhook can optionally use token-based authorization for authentication.</span></span> <span data-ttu-id="1dc22-111">Webhook URI 是以權杖識別碼儲存，例如，`https://mysamplealert/webcallback?tokenid=sometokenid&someparameter=somevalue`。</span><span class="sxs-lookup"><span data-stu-id="1dc22-111">The webhook URI is saved with a token ID, for example, `https://mysamplealert/webcallback?tokenid=sometokenid&someparameter=somevalue`.</span></span>

## <a name="payload-schema"></a><span data-ttu-id="1dc22-112">承載結構描述</span><span class="sxs-lookup"><span data-stu-id="1dc22-112">Payload schema</span></span>
<span data-ttu-id="1dc22-113">POST 作業中所包含的 JSON 承載，會根據承載的 data.context.activityLog.eventSource 欄位而有所不同。</span><span class="sxs-lookup"><span data-stu-id="1dc22-113">The JSON payload contained in the POST operation differs based on the payload's data.context.activityLog.eventSource field.</span></span>

###<a name="common"></a><span data-ttu-id="1dc22-114">一般</span><span class="sxs-lookup"><span data-stu-id="1dc22-114">Common</span></span>
```json
{
    "schemaId": "Microsoft.Insights/activityLogs",
    "data": {
        "status": "Activated",
        "context": {
            "activityLog": {
                "channels": "Operation",
                "correlationId": "6ac88262-43be-4adf-a11c-bd2179852898",
                "eventSource": "Administrative",
                "eventTimestamp": "2017-03-29T15:43:08.0019532+00:00",
                "eventDataId": "8195a56a-85de-4663-943e-1a2bf401ad94",
                "level": "Informational",
                "operationName": "Microsoft.Insights/actionGroups/write",
                "operationId": "6ac88262-43be-4adf-a11c-bd2179852898",
                "status": "Started",
                "subStatus": "",
                "subscriptionId": "52c65f65-0518-4d37-9719-7dbbfc68c57a",
                "submissionTimestamp": "2017-03-29T15:43:20.3863637+00:00",
                ...
            }
        },
        "properties": {}
    }
}
```
###<a name="administrative"></a><span data-ttu-id="1dc22-115">管理</span><span class="sxs-lookup"><span data-stu-id="1dc22-115">Administrative</span></span>
```json
{
    "schemaId": "Microsoft.Insights/activityLogs",
    "data": {
        "status": "Activated",
        "context": {
            "activityLog": {
                "authorization": {
                    "action": "Microsoft.Insights/actionGroups/write",
                    "scope": "/subscriptions/52c65f65-0518-4d37-9719-7dbbfc68c57b/resourceGroups/CONTOSO-TEST/providers/Microsoft.Insights/actionGroups/IncidentActions"
                },
                "claims": "{...}",
                "caller": "me@contoso.com",
                "description": "",
                "httpRequest": "{...}",
                "resourceId": "/subscriptions/52c65f65-0518-4d37-9719-7dbbfc68c57b/resourceGroups/CONTOSO-TEST/providers/Microsoft.Insights/actionGroups/IncidentActions",
                "resourceGroupName": "CONTOSO-TEST",
                "resourceProviderName": "Microsoft.Insights",
                "resourceType": "Microsoft.Insights/actionGroups"
            }
        },
        "properties": {}
    }
}

```
###<a name="servicehealth"></a><span data-ttu-id="1dc22-116">服務健康狀況</span><span class="sxs-lookup"><span data-stu-id="1dc22-116">ServiceHealth</span></span>
```json
{
    "schemaId": "unknown",
    "data": {
        "status": "Activated",
        "context": {
            "activityLog": {
                "properties": {
                    "title": "...",
                    "service": "...",
                    "region": "...",
                    "communication": "...",
                    "incidentType": "Incident",
                    "trackingId": "...",
                    "groupId": "...",
                    "impactStartTime": "3/29/2017 3:43:21 PM",
                    "impactMitigationTime": "3/29/2017 3:43:21 PM",
                    "eventCreationTime": "3/29/2017 3:43:21 PM",
                    "impactedServices": "[{...}]",
                    "defaultLanguageTitle": "...",
                    "defaultLanguageContent": "...",
                    "stage": "Active",
                    "communicationId": "...",
                    "version": "0.1"
                }
            }
        },
        "properties": {}
    }
}
```

<span data-ttu-id="1dc22-117">如需服務健康狀態通知活動記錄警示的特定結構描述詳細資料，請參閱[服務健康狀態通知](monitoring-service-notifications.md)。</span><span class="sxs-lookup"><span data-stu-id="1dc22-117">For specific schema details on service health notification activity log alerts, see [Service health notifications](monitoring-service-notifications.md).</span></span>

<span data-ttu-id="1dc22-118">如需了解所有其他活動記錄警示的特定結構詳細資料，請參閱 [Azure 活動記錄的概觀](monitoring-overview-activity-logs.md)。</span><span class="sxs-lookup"><span data-stu-id="1dc22-118">For specific schema details on all other activity log alerts, see [Overview of the Azure activity log](monitoring-overview-activity-logs.md).</span></span>

| <span data-ttu-id="1dc22-119">元素名稱</span><span class="sxs-lookup"><span data-stu-id="1dc22-119">Element name</span></span> | <span data-ttu-id="1dc22-120">說明</span><span class="sxs-lookup"><span data-stu-id="1dc22-120">Description</span></span> |
| --- | --- |
| <span data-ttu-id="1dc22-121">status</span><span class="sxs-lookup"><span data-stu-id="1dc22-121">status</span></span> |<span data-ttu-id="1dc22-122">用於度量警示。</span><span class="sxs-lookup"><span data-stu-id="1dc22-122">Used for metric alerts.</span></span> <span data-ttu-id="1dc22-123">針對活動記錄警示，一律設為「啟動」。</span><span class="sxs-lookup"><span data-stu-id="1dc22-123">Always set to "activated" for activity log alerts.</span></span> |
| <span data-ttu-id="1dc22-124">context</span><span class="sxs-lookup"><span data-stu-id="1dc22-124">context</span></span> |<span data-ttu-id="1dc22-125">事件的內容。</span><span class="sxs-lookup"><span data-stu-id="1dc22-125">Context of the event.</span></span> |
| <span data-ttu-id="1dc22-126">resourceProviderName</span><span class="sxs-lookup"><span data-stu-id="1dc22-126">resourceProviderName</span></span> |<span data-ttu-id="1dc22-127">受影響資源的資源提供者。</span><span class="sxs-lookup"><span data-stu-id="1dc22-127">The resource provider of the impacted resource.</span></span> |
| <span data-ttu-id="1dc22-128">conditionType</span><span class="sxs-lookup"><span data-stu-id="1dc22-128">conditionType</span></span> |<span data-ttu-id="1dc22-129">一律為「事件」。</span><span class="sxs-lookup"><span data-stu-id="1dc22-129">Always "Event."</span></span> |
| <span data-ttu-id="1dc22-130">名稱</span><span class="sxs-lookup"><span data-stu-id="1dc22-130">name</span></span> |<span data-ttu-id="1dc22-131">警示規則的名稱。</span><span class="sxs-lookup"><span data-stu-id="1dc22-131">Name of the alert rule.</span></span> |
| <span data-ttu-id="1dc22-132">id</span><span class="sxs-lookup"><span data-stu-id="1dc22-132">id</span></span> |<span data-ttu-id="1dc22-133">警示的資源識別碼。</span><span class="sxs-lookup"><span data-stu-id="1dc22-133">Resource ID of the alert.</span></span> |
| <span data-ttu-id="1dc22-134">說明</span><span class="sxs-lookup"><span data-stu-id="1dc22-134">description</span></span> |<span data-ttu-id="1dc22-135">建立警示時，會設定警示描述。</span><span class="sxs-lookup"><span data-stu-id="1dc22-135">Alert description set when the alert is created.</span></span> |
| <span data-ttu-id="1dc22-136">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="1dc22-136">subscriptionId</span></span> |<span data-ttu-id="1dc22-137">Azure 訂用帳戶識別碼。</span><span class="sxs-lookup"><span data-stu-id="1dc22-137">Azure subscription ID.</span></span> |
| <span data-ttu-id="1dc22-138">timestamp</span><span class="sxs-lookup"><span data-stu-id="1dc22-138">timestamp</span></span> |<span data-ttu-id="1dc22-139">處理要求的 Azure 服務產生事件的時間。</span><span class="sxs-lookup"><span data-stu-id="1dc22-139">Time at which the event was generated by the Azure service that processed the request.</span></span> |
| <span data-ttu-id="1dc22-140">resourceId</span><span class="sxs-lookup"><span data-stu-id="1dc22-140">resourceId</span></span> |<span data-ttu-id="1dc22-141">受影響資源的資源識別碼。</span><span class="sxs-lookup"><span data-stu-id="1dc22-141">Resource ID of the impacted resource.</span></span> |
| <span data-ttu-id="1dc22-142">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="1dc22-142">resourceGroupName</span></span> |<span data-ttu-id="1dc22-143">受影響資源的資源群組的名稱。</span><span class="sxs-lookup"><span data-stu-id="1dc22-143">Name of the resource group for the impacted resource.</span></span> |
| <span data-ttu-id="1dc22-144">屬性</span><span class="sxs-lookup"><span data-stu-id="1dc22-144">properties</span></span> |<span data-ttu-id="1dc22-145">一組包含事件相關詳細資料的`<Key, Value>`配對 (也就是 `Dictionary<String, String>`)。</span><span class="sxs-lookup"><span data-stu-id="1dc22-145">Set of `<Key, Value>` pairs (that is, `Dictionary<String, String>`) that includes details about the event.</span></span> |
| <span data-ttu-id="1dc22-146">事件</span><span class="sxs-lookup"><span data-stu-id="1dc22-146">event</span></span> |<span data-ttu-id="1dc22-147">包含事件相關中繼資料的元素。</span><span class="sxs-lookup"><span data-stu-id="1dc22-147">Element that contains metadata about the event.</span></span> |
| <span data-ttu-id="1dc22-148">授權</span><span class="sxs-lookup"><span data-stu-id="1dc22-148">authorization</span></span> |<span data-ttu-id="1dc22-149">事件的角色型存取控制屬性。</span><span class="sxs-lookup"><span data-stu-id="1dc22-149">The Role-Based Access Control properties of the event.</span></span> <span data-ttu-id="1dc22-150">這些屬性通常包括動作、角色和範圍。</span><span class="sxs-lookup"><span data-stu-id="1dc22-150">These properties usually include the action, the role, and the scope.</span></span> |
| <span data-ttu-id="1dc22-151">category</span><span class="sxs-lookup"><span data-stu-id="1dc22-151">category</span></span> |<span data-ttu-id="1dc22-152">事件的類別。</span><span class="sxs-lookup"><span data-stu-id="1dc22-152">Category of the event.</span></span> <span data-ttu-id="1dc22-153">支援值包括「管理」、「警示」、「安全性」、「ServiceHealth」和「建議」。</span><span class="sxs-lookup"><span data-stu-id="1dc22-153">Supported values include Administrative, Alert, Security, ServiceHealth, and Recommendation.</span></span> |
| <span data-ttu-id="1dc22-154">呼叫者</span><span class="sxs-lookup"><span data-stu-id="1dc22-154">caller</span></span> |<span data-ttu-id="1dc22-155">已執行作業的使用者的電子郵件地址，根據可用性的 UPN 宣告或 SPN 宣告。</span><span class="sxs-lookup"><span data-stu-id="1dc22-155">Email address of the user who performed the operation, UPN claim, or SPN claim based on availability.</span></span> <span data-ttu-id="1dc22-156">特定系統呼叫可為 Null。</span><span class="sxs-lookup"><span data-stu-id="1dc22-156">Can be null for certain system calls.</span></span> |
| <span data-ttu-id="1dc22-157">correlationId</span><span class="sxs-lookup"><span data-stu-id="1dc22-157">correlationId</span></span> |<span data-ttu-id="1dc22-158">通常是字串格式的 GUID。</span><span class="sxs-lookup"><span data-stu-id="1dc22-158">Usually a GUID in string format.</span></span> <span data-ttu-id="1dc22-159">具有屬於同一個較大動作的 correlationId 的事件，且通常會共用 correlationId。</span><span class="sxs-lookup"><span data-stu-id="1dc22-159">Events with correlationId belong to the same larger action and usually share a correlationId.</span></span> |
| <span data-ttu-id="1dc22-160">eventDescription</span><span class="sxs-lookup"><span data-stu-id="1dc22-160">eventDescription</span></span> |<span data-ttu-id="1dc22-161">事件的靜態文字描述。</span><span class="sxs-lookup"><span data-stu-id="1dc22-161">Static text description of the event.</span></span> |
| <span data-ttu-id="1dc22-162">eventDataId</span><span class="sxs-lookup"><span data-stu-id="1dc22-162">eventDataId</span></span> |<span data-ttu-id="1dc22-163">事件的唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="1dc22-163">Unique identifier for the event.</span></span> |
| <span data-ttu-id="1dc22-164">eventSource</span><span class="sxs-lookup"><span data-stu-id="1dc22-164">eventSource</span></span> |<span data-ttu-id="1dc22-165">產生事件的 Azure 服務或基礎結構的名稱。</span><span class="sxs-lookup"><span data-stu-id="1dc22-165">Name of the Azure service or infrastructure that generated the event.</span></span> |
| <span data-ttu-id="1dc22-166">httpRequest</span><span class="sxs-lookup"><span data-stu-id="1dc22-166">httpRequest</span></span> |<span data-ttu-id="1dc22-167">要求通常包括 “clientRequestId”、“clientIpAddress” 和 HTTP “method” (例如 PUT)。</span><span class="sxs-lookup"><span data-stu-id="1dc22-167">The request usually includes the clientRequestId, clientIpAddress, and HTTP method (for example, PUT).</span></span> |
| <span data-ttu-id="1dc22-168">層級</span><span class="sxs-lookup"><span data-stu-id="1dc22-168">level</span></span> |<span data-ttu-id="1dc22-169">下列其中一個值：「重大」、「錯誤」、「警告」、「資訊」和「詳細資訊」。</span><span class="sxs-lookup"><span data-stu-id="1dc22-169">One of the following values: Critical, Error, Warning, Informational, and Verbose.</span></span> |
| <span data-ttu-id="1dc22-170">operationId</span><span class="sxs-lookup"><span data-stu-id="1dc22-170">operationId</span></span> |<span data-ttu-id="1dc22-171">通常是對應至單一作業的事件之間共用的 GUID。</span><span class="sxs-lookup"><span data-stu-id="1dc22-171">Usually a GUID shared among the events corresponding to single operation.</span></span> |
| <span data-ttu-id="1dc22-172">operationName</span><span class="sxs-lookup"><span data-stu-id="1dc22-172">operationName</span></span> |<span data-ttu-id="1dc22-173">作業名稱。</span><span class="sxs-lookup"><span data-stu-id="1dc22-173">Name of the operation.</span></span> |
| <span data-ttu-id="1dc22-174">屬性</span><span class="sxs-lookup"><span data-stu-id="1dc22-174">properties</span></span> |<span data-ttu-id="1dc22-175">事件的屬性。</span><span class="sxs-lookup"><span data-stu-id="1dc22-175">Properties of the event.</span></span> |
| <span data-ttu-id="1dc22-176">status</span><span class="sxs-lookup"><span data-stu-id="1dc22-176">status</span></span> |<span data-ttu-id="1dc22-177">字串。</span><span class="sxs-lookup"><span data-stu-id="1dc22-177">String.</span></span> <span data-ttu-id="1dc22-178">作業的狀態。</span><span class="sxs-lookup"><span data-stu-id="1dc22-178">Status of the operation.</span></span> <span data-ttu-id="1dc22-179">常見的值包括︰「已啟動」、「進行中」、「成功」、「失敗」、「使用中」和「已解決」。</span><span class="sxs-lookup"><span data-stu-id="1dc22-179">Common values include Started, In Progress, Succeeded, Failed, Active, and Resolved.</span></span> |
| <span data-ttu-id="1dc22-180">子狀態</span><span class="sxs-lookup"><span data-stu-id="1dc22-180">subStatus</span></span> |<span data-ttu-id="1dc22-181">通常包含對應 REST 呼叫的 HTTP 狀態碼。</span><span class="sxs-lookup"><span data-stu-id="1dc22-181">Usually includes the HTTP status code of the corresponding REST call.</span></span> <span data-ttu-id="1dc22-182">它也可以包含其他描述子狀態的字串。</span><span class="sxs-lookup"><span data-stu-id="1dc22-182">It might also include other strings that describe a substatus.</span></span> <span data-ttu-id="1dc22-183">常見子狀態的值包括：確定 (HTTP 狀態碼︰200)，已建立 (HTTP 狀態碼︰201)、接受 (HTTP 狀態碼︰202)、沒有內容 (HTTP 狀態碼︰204)、不正確的要求 (HTTP 狀態碼︰400)、找不到 (HTTP 狀態碼︰404)，衝突 (HTTP 狀態碼︰409)、內部伺服器錯誤 (HTTP 狀態碼︰500)、服務無法使用 (HTTP 狀態碼︰503) 和閘道逾時 (HTTP 狀態碼︰504)。</span><span class="sxs-lookup"><span data-stu-id="1dc22-183">Common substatus values include OK (HTTP Status Code: 200), Created (HTTP Status Code: 201), Accepted (HTTP Status Code: 202), No Content (HTTP Status Code: 204), Bad Request (HTTP Status Code: 400), Not Found (HTTP Status Code: 404), Conflict (HTTP Status Code: 409), Internal Server Error (HTTP Status Code: 500), Service Unavailable (HTTP Status Code: 503), and Gateway Timeout (HTTP Status Code: 504).</span></span> |

## <a name="next-steps"></a><span data-ttu-id="1dc22-184">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1dc22-184">Next steps</span></span>
* <span data-ttu-id="1dc22-185">[深入了解活動記錄](monitoring-overview-activity-logs.md)。</span><span class="sxs-lookup"><span data-stu-id="1dc22-185">[Learn more about the activity log](monitoring-overview-activity-logs.md).</span></span>
* <span data-ttu-id="1dc22-186">[對 Azure 警示執行 Azure 自動化指令碼 (Runbook)](http://go.microsoft.com/fwlink/?LinkId=627081)。</span><span class="sxs-lookup"><span data-stu-id="1dc22-186">[Execute Azure automation scripts (Runbooks) on Azure alerts](http://go.microsoft.com/fwlink/?LinkId=627081).</span></span>
* <span data-ttu-id="1dc22-187">[使用邏輯應用程式透過 Twilio 從 Azure 警示傳送 SMS](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-text-message-with-logic-app)。</span><span class="sxs-lookup"><span data-stu-id="1dc22-187">[Use a logic app to send an SMS via Twilio from an Azure alert](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-text-message-with-logic-app).</span></span> <span data-ttu-id="1dc22-188">此範例適用於計量警示，但經過修改後即可用於活動記錄警示。</span><span class="sxs-lookup"><span data-stu-id="1dc22-188">This example is for metric alerts, but it can be modified to work with an activity log alert.</span></span>
* <span data-ttu-id="1dc22-189">[使用邏輯應用程式從 Azure 警示傳送 Slack 訊息](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-slack-with-logic-app)。</span><span class="sxs-lookup"><span data-stu-id="1dc22-189">[Use a logic app to send a Slack message from an Azure alert](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-slack-with-logic-app).</span></span> <span data-ttu-id="1dc22-190">此範例適用於計量警示，但經過修改後即可用於活動記錄警示。</span><span class="sxs-lookup"><span data-stu-id="1dc22-190">This example is for metric alerts, but it can be modified to work with an activity log alert.</span></span>
* <span data-ttu-id="1dc22-191">[使用邏輯應用程式從 Azure 警示將訊息傳送到 Azure 佇列](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-queue-with-logic-app)。</span><span class="sxs-lookup"><span data-stu-id="1dc22-191">[Use a logic app to send a message to an Azure queue from an Azure alert](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-queue-with-logic-app).</span></span> <span data-ttu-id="1dc22-192">此範例適用於計量警示，但經過修改後即可用於活動記錄警示。</span><span class="sxs-lookup"><span data-stu-id="1dc22-192">This example is for metric alerts, but it can be modified to work with an activity log alert.</span></span>
