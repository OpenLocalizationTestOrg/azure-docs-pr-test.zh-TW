---
title: "活動記錄檔警示中使用的 aaaUnderstand hello webhook 結構描述 |Microsoft 文件"
description: "深入了解 hello hello 活動記錄檔警示啟動時張貼 tooa webhook URL 的 JSON 結構描述。"
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
ms.openlocfilehash: 75562e0589222d3e392ea73eacfd7414a422d115
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="webhooks-for-azure-activity-log-alerts"></a><span data-ttu-id="1d72b-103">Azure 活動記錄警示的 Webhook</span><span class="sxs-lookup"><span data-stu-id="1d72b-103">Webhooks for Azure activity log alerts</span></span>
<span data-ttu-id="1d72b-104">Hello 定義的動作群組的一部分，您可以設定 webhook 端點 tooreceive 活動記錄檔警示通知。</span><span class="sxs-lookup"><span data-stu-id="1d72b-104">As part of hello definition of an action group, you can configure webhook endpoints tooreceive activity log alert notifications.</span></span> <span data-ttu-id="1d72b-105">使用 webhook，您可以路由傳送這些通知 tooother 系統以進行後置處理或自訂動作。</span><span class="sxs-lookup"><span data-stu-id="1d72b-105">With webhooks, you can route these notifications tooother systems for post-processing or custom actions.</span></span> <span data-ttu-id="1d72b-106">本文說明哪些 hello 的內容看起來像 hello HTTP POST tooa webhook。</span><span class="sxs-lookup"><span data-stu-id="1d72b-106">This article shows what hello payload for hello HTTP POST tooa webhook looks like.</span></span>

<span data-ttu-id="1d72b-107">如需有關活動記錄檔警示的詳細資訊，請參閱如何太[建立 Azure 活動記錄檔警示](monitoring-activity-log-alerts.md)。</span><span class="sxs-lookup"><span data-stu-id="1d72b-107">For more information on activity log alerts, see how too[create Azure activity log alerts](monitoring-activity-log-alerts.md).</span></span>

<span data-ttu-id="1d72b-108">動作群組的相關資訊，請參閱如何太[建立動作群組](monitoring-action-groups.md)。</span><span class="sxs-lookup"><span data-stu-id="1d72b-108">For information on action groups, see how too[create action groups](monitoring-action-groups.md).</span></span>

## <a name="authenticate-hello-webhook"></a><span data-ttu-id="1d72b-109">驗證 hello webhook</span><span class="sxs-lookup"><span data-stu-id="1d72b-109">Authenticate hello webhook</span></span>
<span data-ttu-id="1d72b-110">hello webhook 進行驗證，可以選擇使用權杖為基礎的授權。</span><span class="sxs-lookup"><span data-stu-id="1d72b-110">hello webhook can optionally use token-based authorization for authentication.</span></span> <span data-ttu-id="1d72b-111">hello 的 webhook URI 便可以 token 的識別碼，例如`https://mysamplealert/webcallback?tokenid=sometokenid&someparameter=somevalue`。</span><span class="sxs-lookup"><span data-stu-id="1d72b-111">hello webhook URI is saved with a token ID, for example, `https://mysamplealert/webcallback?tokenid=sometokenid&someparameter=somevalue`.</span></span>

## <a name="payload-schema"></a><span data-ttu-id="1d72b-112">承載結構描述</span><span class="sxs-lookup"><span data-stu-id="1d72b-112">Payload schema</span></span>
<span data-ttu-id="1d72b-113">hello POST 作業中所包含的 hello JSON 承載不同根據 hello 裝載 data.context.activityLog.eventSource 欄位上。</span><span class="sxs-lookup"><span data-stu-id="1d72b-113">hello JSON payload contained in hello POST operation differs based on hello payload's data.context.activityLog.eventSource field.</span></span>

###<a name="common"></a><span data-ttu-id="1d72b-114">一般</span><span class="sxs-lookup"><span data-stu-id="1d72b-114">Common</span></span>
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
###<a name="administrative"></a><span data-ttu-id="1d72b-115">管理</span><span class="sxs-lookup"><span data-stu-id="1d72b-115">Administrative</span></span>
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
###<a name="servicehealth"></a><span data-ttu-id="1d72b-116">服務健康狀況</span><span class="sxs-lookup"><span data-stu-id="1d72b-116">ServiceHealth</span></span>
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

<span data-ttu-id="1d72b-117">如需服務健康狀態通知活動記錄警示的特定結構描述詳細資料，請參閱[服務健康狀態通知](monitoring-service-notifications.md)。</span><span class="sxs-lookup"><span data-stu-id="1d72b-117">For specific schema details on service health notification activity log alerts, see [Service health notifications](monitoring-service-notifications.md).</span></span>

<span data-ttu-id="1d72b-118">所有其他活動記錄警示的特定結構描述資訊，請參閱[hello Azure 活動記錄檔的概觀](monitoring-overview-activity-logs.md)。</span><span class="sxs-lookup"><span data-stu-id="1d72b-118">For specific schema details on all other activity log alerts, see [Overview of hello Azure activity log](monitoring-overview-activity-logs.md).</span></span>

| <span data-ttu-id="1d72b-119">元素名稱</span><span class="sxs-lookup"><span data-stu-id="1d72b-119">Element name</span></span> | <span data-ttu-id="1d72b-120">說明</span><span class="sxs-lookup"><span data-stu-id="1d72b-120">Description</span></span> |
| --- | --- |
| <span data-ttu-id="1d72b-121">status</span><span class="sxs-lookup"><span data-stu-id="1d72b-121">status</span></span> |<span data-ttu-id="1d72b-122">用於度量警示。</span><span class="sxs-lookup"><span data-stu-id="1d72b-122">Used for metric alerts.</span></span> <span data-ttu-id="1d72b-123">一定會設定太 「 啟動 」 的活動記錄檔的警示。</span><span class="sxs-lookup"><span data-stu-id="1d72b-123">Always set too"activated" for activity log alerts.</span></span> |
| <span data-ttu-id="1d72b-124">context</span><span class="sxs-lookup"><span data-stu-id="1d72b-124">context</span></span> |<span data-ttu-id="1d72b-125">Hello 事件的內容。</span><span class="sxs-lookup"><span data-stu-id="1d72b-125">Context of hello event.</span></span> |
| <span data-ttu-id="1d72b-126">resourceProviderName</span><span class="sxs-lookup"><span data-stu-id="1d72b-126">resourceProviderName</span></span> |<span data-ttu-id="1d72b-127">hello 資源提供者的 hello 影響資源。</span><span class="sxs-lookup"><span data-stu-id="1d72b-127">hello resource provider of hello impacted resource.</span></span> |
| <span data-ttu-id="1d72b-128">conditionType</span><span class="sxs-lookup"><span data-stu-id="1d72b-128">conditionType</span></span> |<span data-ttu-id="1d72b-129">一律為「事件」。</span><span class="sxs-lookup"><span data-stu-id="1d72b-129">Always "Event."</span></span> |
| <span data-ttu-id="1d72b-130">名稱</span><span class="sxs-lookup"><span data-stu-id="1d72b-130">name</span></span> |<span data-ttu-id="1d72b-131">Hello 警示規則的名稱。</span><span class="sxs-lookup"><span data-stu-id="1d72b-131">Name of hello alert rule.</span></span> |
| <span data-ttu-id="1d72b-132">id</span><span class="sxs-lookup"><span data-stu-id="1d72b-132">id</span></span> |<span data-ttu-id="1d72b-133">Hello 警示的資源識別碼。</span><span class="sxs-lookup"><span data-stu-id="1d72b-133">Resource ID of hello alert.</span></span> |
| <span data-ttu-id="1d72b-134">說明</span><span class="sxs-lookup"><span data-stu-id="1d72b-134">description</span></span> |<span data-ttu-id="1d72b-135">建立 hello 警示時設定警示的描述。</span><span class="sxs-lookup"><span data-stu-id="1d72b-135">Alert description set when hello alert is created.</span></span> |
| <span data-ttu-id="1d72b-136">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="1d72b-136">subscriptionId</span></span> |<span data-ttu-id="1d72b-137">Azure 訂用帳戶識別碼。</span><span class="sxs-lookup"><span data-stu-id="1d72b-137">Azure subscription ID.</span></span> |
| <span data-ttu-id="1d72b-138">timestamp</span><span class="sxs-lookup"><span data-stu-id="1d72b-138">timestamp</span></span> |<span data-ttu-id="1d72b-139">Hello 處理 hello 要求的 Azure 服務所產生的 hello 事件的時間。</span><span class="sxs-lookup"><span data-stu-id="1d72b-139">Time at which hello event was generated by hello Azure service that processed hello request.</span></span> |
| <span data-ttu-id="1d72b-140">resourceId</span><span class="sxs-lookup"><span data-stu-id="1d72b-140">resourceId</span></span> |<span data-ttu-id="1d72b-141">資源識別碼 hello 影響資源。</span><span class="sxs-lookup"><span data-stu-id="1d72b-141">Resource ID of hello impacted resource.</span></span> |
| <span data-ttu-id="1d72b-142">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="1d72b-142">resourceGroupName</span></span> |<span data-ttu-id="1d72b-143">Hello hello 資源群組名稱會影響資源。</span><span class="sxs-lookup"><span data-stu-id="1d72b-143">Name of hello resource group for hello impacted resource.</span></span> |
| <span data-ttu-id="1d72b-144">屬性</span><span class="sxs-lookup"><span data-stu-id="1d72b-144">properties</span></span> |<span data-ttu-id="1d72b-145">一組`<Key, Value>`組 (也就是`Dictionary<String, String>`)，包括有關 hello 事件的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="1d72b-145">Set of `<Key, Value>` pairs (that is, `Dictionary<String, String>`) that includes details about hello event.</span></span> |
| <span data-ttu-id="1d72b-146">事件</span><span class="sxs-lookup"><span data-stu-id="1d72b-146">event</span></span> |<span data-ttu-id="1d72b-147">包含有關 hello 事件中繼資料的項目。</span><span class="sxs-lookup"><span data-stu-id="1d72b-147">Element that contains metadata about hello event.</span></span> |
| <span data-ttu-id="1d72b-148">授權</span><span class="sxs-lookup"><span data-stu-id="1d72b-148">authorization</span></span> |<span data-ttu-id="1d72b-149">hello hello 事件的角色型存取控制內容。</span><span class="sxs-lookup"><span data-stu-id="1d72b-149">hello Role-Based Access Control properties of hello event.</span></span> <span data-ttu-id="1d72b-150">這些屬性通常包含 hello 動作、 hello 角色和 hello 範圍。</span><span class="sxs-lookup"><span data-stu-id="1d72b-150">These properties usually include hello action, hello role, and hello scope.</span></span> |
| <span data-ttu-id="1d72b-151">category</span><span class="sxs-lookup"><span data-stu-id="1d72b-151">category</span></span> |<span data-ttu-id="1d72b-152">Hello 事件類別目錄。</span><span class="sxs-lookup"><span data-stu-id="1d72b-152">Category of hello event.</span></span> <span data-ttu-id="1d72b-153">支援值包括「管理」、「警示」、「安全性」、「ServiceHealth」和「建議」。</span><span class="sxs-lookup"><span data-stu-id="1d72b-153">Supported values include Administrative, Alert, Security, ServiceHealth, and Recommendation.</span></span> |
| <span data-ttu-id="1d72b-154">呼叫者</span><span class="sxs-lookup"><span data-stu-id="1d72b-154">caller</span></span> |<span data-ttu-id="1d72b-155">執行 hello 作業、 UPN 宣告或 SPN 宣告根據可用性的 hello 使用者的電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="1d72b-155">Email address of hello user who performed hello operation, UPN claim, or SPN claim based on availability.</span></span> <span data-ttu-id="1d72b-156">特定系統呼叫可為 Null。</span><span class="sxs-lookup"><span data-stu-id="1d72b-156">Can be null for certain system calls.</span></span> |
| <span data-ttu-id="1d72b-157">correlationId</span><span class="sxs-lookup"><span data-stu-id="1d72b-157">correlationId</span></span> |<span data-ttu-id="1d72b-158">通常是字串格式的 GUID。</span><span class="sxs-lookup"><span data-stu-id="1d72b-158">Usually a GUID in string format.</span></span> <span data-ttu-id="1d72b-159">具有相互關聯識別碼的事件屬於 toohello 相同較大的動作，通常會共用的相互關聯識別碼。</span><span class="sxs-lookup"><span data-stu-id="1d72b-159">Events with correlationId belong toohello same larger action and usually share a correlationId.</span></span> |
| <span data-ttu-id="1d72b-160">eventDescription</span><span class="sxs-lookup"><span data-stu-id="1d72b-160">eventDescription</span></span> |<span data-ttu-id="1d72b-161">Hello 事件的靜態文字描述。</span><span class="sxs-lookup"><span data-stu-id="1d72b-161">Static text description of hello event.</span></span> |
| <span data-ttu-id="1d72b-162">eventDataId</span><span class="sxs-lookup"><span data-stu-id="1d72b-162">eventDataId</span></span> |<span data-ttu-id="1d72b-163">Hello 事件的唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="1d72b-163">Unique identifier for hello event.</span></span> |
| <span data-ttu-id="1d72b-164">eventSource</span><span class="sxs-lookup"><span data-stu-id="1d72b-164">eventSource</span></span> |<span data-ttu-id="1d72b-165">名稱 hello Azure 服務或基礎結構產生的 hello 事件。</span><span class="sxs-lookup"><span data-stu-id="1d72b-165">Name of hello Azure service or infrastructure that generated hello event.</span></span> |
| <span data-ttu-id="1d72b-166">httpRequest</span><span class="sxs-lookup"><span data-stu-id="1d72b-166">httpRequest</span></span> |<span data-ttu-id="1d72b-167">hello 要求通常包括 hello clientRequestId、 clientIpAddress 和 HTTP 方法 (例如 PUT)。</span><span class="sxs-lookup"><span data-stu-id="1d72b-167">hello request usually includes hello clientRequestId, clientIpAddress, and HTTP method (for example, PUT).</span></span> |
| <span data-ttu-id="1d72b-168">層級</span><span class="sxs-lookup"><span data-stu-id="1d72b-168">level</span></span> |<span data-ttu-id="1d72b-169">Hello 下列值之一： 嚴重、 錯誤、 警告、 資訊和詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="1d72b-169">One of hello following values: Critical, Error, Warning, Informational, and Verbose.</span></span> |
| <span data-ttu-id="1d72b-170">operationId</span><span class="sxs-lookup"><span data-stu-id="1d72b-170">operationId</span></span> |<span data-ttu-id="1d72b-171">通常是在對應 toosingle 作業 hello 事件之間共用的 GUID。</span><span class="sxs-lookup"><span data-stu-id="1d72b-171">Usually a GUID shared among hello events corresponding toosingle operation.</span></span> |
| <span data-ttu-id="1d72b-172">operationName</span><span class="sxs-lookup"><span data-stu-id="1d72b-172">operationName</span></span> |<span data-ttu-id="1d72b-173">Hello 作業的名稱。</span><span class="sxs-lookup"><span data-stu-id="1d72b-173">Name of hello operation.</span></span> |
| <span data-ttu-id="1d72b-174">屬性</span><span class="sxs-lookup"><span data-stu-id="1d72b-174">properties</span></span> |<span data-ttu-id="1d72b-175">Hello 事件的屬性。</span><span class="sxs-lookup"><span data-stu-id="1d72b-175">Properties of hello event.</span></span> |
| <span data-ttu-id="1d72b-176">status</span><span class="sxs-lookup"><span data-stu-id="1d72b-176">status</span></span> |<span data-ttu-id="1d72b-177">字串。</span><span class="sxs-lookup"><span data-stu-id="1d72b-177">String.</span></span> <span data-ttu-id="1d72b-178">Hello 作業的狀態。</span><span class="sxs-lookup"><span data-stu-id="1d72b-178">Status of hello operation.</span></span> <span data-ttu-id="1d72b-179">常見的值包括︰「已啟動」、「進行中」、「成功」、「失敗」、「使用中」和「已解決」。</span><span class="sxs-lookup"><span data-stu-id="1d72b-179">Common values include Started, In Progress, Succeeded, Failed, Active, and Resolved.</span></span> |
| <span data-ttu-id="1d72b-180">子狀態</span><span class="sxs-lookup"><span data-stu-id="1d72b-180">subStatus</span></span> |<span data-ttu-id="1d72b-181">通常包含對應 REST 呼叫 hello hello HTTP 狀態碼。</span><span class="sxs-lookup"><span data-stu-id="1d72b-181">Usually includes hello HTTP status code of hello corresponding REST call.</span></span> <span data-ttu-id="1d72b-182">它也可以包含其他描述子狀態的字串。</span><span class="sxs-lookup"><span data-stu-id="1d72b-182">It might also include other strings that describe a substatus.</span></span> <span data-ttu-id="1d72b-183">常見子狀態的值包括：確定 (HTTP 狀態碼︰200)，已建立 (HTTP 狀態碼︰201)、接受 (HTTP 狀態碼︰202)、沒有內容 (HTTP 狀態碼︰204)、不正確的要求 (HTTP 狀態碼︰400)、找不到 (HTTP 狀態碼︰404)，衝突 (HTTP 狀態碼︰409)、內部伺服器錯誤 (HTTP 狀態碼︰500)、服務無法使用 (HTTP 狀態碼︰503) 和閘道逾時 (HTTP 狀態碼︰504)。</span><span class="sxs-lookup"><span data-stu-id="1d72b-183">Common substatus values include OK (HTTP Status Code: 200), Created (HTTP Status Code: 201), Accepted (HTTP Status Code: 202), No Content (HTTP Status Code: 204), Bad Request (HTTP Status Code: 400), Not Found (HTTP Status Code: 404), Conflict (HTTP Status Code: 409), Internal Server Error (HTTP Status Code: 500), Service Unavailable (HTTP Status Code: 503), and Gateway Timeout (HTTP Status Code: 504).</span></span> |

## <a name="next-steps"></a><span data-ttu-id="1d72b-184">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1d72b-184">Next steps</span></span>
* <span data-ttu-id="1d72b-185">[深入了解 hello 活動記錄檔](monitoring-overview-activity-logs.md)。</span><span class="sxs-lookup"><span data-stu-id="1d72b-185">[Learn more about hello activity log](monitoring-overview-activity-logs.md).</span></span>
* <span data-ttu-id="1d72b-186">[對 Azure 警示執行 Azure 自動化指令碼 (Runbook)](http://go.microsoft.com/fwlink/?LinkId=627081)。</span><span class="sxs-lookup"><span data-stu-id="1d72b-186">[Execute Azure automation scripts (Runbooks) on Azure alerts](http://go.microsoft.com/fwlink/?LinkId=627081).</span></span>
* <span data-ttu-id="1d72b-187">[使用邏輯應用程式 toosend Twilio 透過 SMS 從 Azure 警示](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-text-message-with-logic-app)。</span><span class="sxs-lookup"><span data-stu-id="1d72b-187">[Use a logic app toosend an SMS via Twilio from an Azure alert](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-text-message-with-logic-app).</span></span> <span data-ttu-id="1d72b-188">這個範例適用於度量的警示，但可以修改的 toowork 與活動記錄警示。</span><span class="sxs-lookup"><span data-stu-id="1d72b-188">This example is for metric alerts, but it can be modified toowork with an activity log alert.</span></span>
* <span data-ttu-id="1d72b-189">[使用邏輯應用程式 toosend Slack 訊息從 Azure 警示](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-slack-with-logic-app)。</span><span class="sxs-lookup"><span data-stu-id="1d72b-189">[Use a logic app toosend a Slack message from an Azure alert](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-slack-with-logic-app).</span></span> <span data-ttu-id="1d72b-190">這個範例適用於度量的警示，但可以修改的 toowork 與活動記錄警示。</span><span class="sxs-lookup"><span data-stu-id="1d72b-190">This example is for metric alerts, but it can be modified toowork with an activity log alert.</span></span>
* <span data-ttu-id="1d72b-191">[使用從 Azure 警示佇列的訊息 tooan Azure 邏輯應用程式 toosend](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-queue-with-logic-app)。</span><span class="sxs-lookup"><span data-stu-id="1d72b-191">[Use a logic app toosend a message tooan Azure queue from an Azure alert](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-queue-with-logic-app).</span></span> <span data-ttu-id="1d72b-192">這個範例適用於度量的警示，但可以修改的 toowork 與活動記錄警示。</span><span class="sxs-lookup"><span data-stu-id="1d72b-192">This example is for metric alerts, but it can be modified toowork with an activity log alert.</span></span>
