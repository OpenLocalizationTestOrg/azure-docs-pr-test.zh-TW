---
title: "Azure 活動記錄檔警示 webhook aaaCall |Microsoft 文件"
description: "路由活動記錄檔事件 tooother 服務的自訂動作。 例如傳送簡訊、記錄 Bug、或透過聊天/傳訊服務來通知團隊。"
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 64d333d1-7f37-4a00-9d16-dda6e69a113b
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: johnkem
ms.openlocfilehash: 9017ff3e5165857ec7084a8f07f4123552e55f73
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="call-a-webhook-on-azure-activity-log-alerts"></a><span data-ttu-id="60dea-104">針對 Azure 活動記錄警示呼叫 Webhook</span><span class="sxs-lookup"><span data-stu-id="60dea-104">Call a webhook on Azure Activity Log alerts</span></span>
<span data-ttu-id="60dea-105">Webhook 可讓您 tooroute Azure 警示通知 tooother 系統後置處理或自訂動作。</span><span class="sxs-lookup"><span data-stu-id="60dea-105">Webhooks allow you tooroute an Azure alert notification tooother systems for post-processing or custom actions.</span></span> <span data-ttu-id="60dea-106">您可以使用 webhook 警示 tooroute 它 tooservices 傳送 SMS，記錄錯誤、 通知聊天/傳訊服務，透過小組或執行任意數目的其他動作。</span><span class="sxs-lookup"><span data-stu-id="60dea-106">You can use a webhook on an alert tooroute it tooservices that send SMS, log bugs, notify a team via chat/messaging services, or do any number of other actions.</span></span> <span data-ttu-id="60dea-107">本文說明 tooset webhook toobe 呼叫 Azure 活動記錄檔警示引發時的方式。</span><span class="sxs-lookup"><span data-stu-id="60dea-107">This article describes how tooset a webhook toobe called when an Azure Activity Log alert fires.</span></span> <span data-ttu-id="60dea-108">它也會顯示 hello HTTP POST tooa webhook 看起來像哪些 hello 裝載。</span><span class="sxs-lookup"><span data-stu-id="60dea-108">It also shows what hello payload for hello HTTP POST tooa webhook looks like.</span></span> <span data-ttu-id="60dea-109">如需有關 hello 安裝程式並在 Azure 度量的警示，結構描述資訊[請改為參閱此頁面](insights-webhooks-alerts.md)。</span><span class="sxs-lookup"><span data-stu-id="60dea-109">For information on hello setup and schema for an Azure metric alert, [see this page instead](insights-webhooks-alerts.md).</span></span> <span data-ttu-id="60dea-110">您也可以設定活動記錄檔警示 toosend 電子郵件時啟動。</span><span class="sxs-lookup"><span data-stu-id="60dea-110">You can also set up an Activity Log alert toosend email when activated.</span></span>

> [!NOTE]
> <span data-ttu-id="60dea-111">這項功能目前為預覽狀態，並將在未來的 hello 在某個時間點移除。</span><span class="sxs-lookup"><span data-stu-id="60dea-111">This feature is currently in preview and will be removed at some point in hello future.</span></span>
>
>

<span data-ttu-id="60dea-112">您可以設定活動記錄檔警示使用 hello [Azure PowerShell Cmdlet](insights-powershell-samples.md#create-metric-alerts)，[跨平台 CLI](insights-cli-samples.md#work-with-alerts)，或[Azure 監視 REST API](https://msdn.microsoft.com/library/azure/dn933805.aspx)。</span><span class="sxs-lookup"><span data-stu-id="60dea-112">You can set up an Activity Log alert using hello [Azure PowerShell Cmdlets](insights-powershell-samples.md#create-metric-alerts), [Cross-Platform CLI](insights-cli-samples.md#work-with-alerts), or [Azure Monitor REST API](https://msdn.microsoft.com/library/azure/dn933805.aspx).</span></span> <span data-ttu-id="60dea-113">目前，您無法設定一個使用 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="60dea-113">Currently, you cannot set one up using hello Azure portal.</span></span>

## <a name="authenticating-hello-webhook"></a><span data-ttu-id="60dea-114">驗證 hello webhook</span><span class="sxs-lookup"><span data-stu-id="60dea-114">Authenticating hello webhook</span></span>
<span data-ttu-id="60dea-115">hello webhook 可以使用其中一種方法進行驗證：</span><span class="sxs-lookup"><span data-stu-id="60dea-115">hello webhook can authenticate using either of these methods:</span></span>

1. <span data-ttu-id="60dea-116">**權杖為基礎的授權**-hello 的 webhook URI 便可以 token 的識別碼，例如，`https://mysamplealert/webcallback?tokenid=sometokenid&someparameter=somevalue`</span><span class="sxs-lookup"><span data-stu-id="60dea-116">**Token-based authorization** - hello webhook URI is saved with a token ID, for example, `https://mysamplealert/webcallback?tokenid=sometokenid&someparameter=somevalue`</span></span>
2. <span data-ttu-id="60dea-117">**基本授權**-hello 的 webhook URI，例如儲存使用者名稱及密碼，`https://userid:password@mysamplealert/webcallback?someparamater=somevalue&foo=bar`</span><span class="sxs-lookup"><span data-stu-id="60dea-117">**Basic authorization** - hello webhook URI is saved with a username and password, for example, `https://userid:password@mysamplealert/webcallback?someparamater=somevalue&foo=bar`</span></span>

## <a name="payload-schema"></a><span data-ttu-id="60dea-118">承載結構描述</span><span class="sxs-lookup"><span data-stu-id="60dea-118">Payload schema</span></span>
<span data-ttu-id="60dea-119">hello POST 作業包含下列 JSON 裝載和結構描述的所有活動記錄檔為基礎的警示 hello。</span><span class="sxs-lookup"><span data-stu-id="60dea-119">hello POST operation contains hello following JSON payload and schema for all Activity Log-based alerts.</span></span> <span data-ttu-id="60dea-120">此結構描述是類似 toohello 使用其中一種標準為基礎的警示。</span><span class="sxs-lookup"><span data-stu-id="60dea-120">This schema is similar toohello one used by metric-based alerts.</span></span>

```
{
        "status": "Activated",
        "context": {
                "resourceProviderName": "Microsoft.Web",
                "event": {
                        "$type": "Microsoft.WindowsAzure.Management.Monitoring.Automation.Notifications.GenericNotifications.Datacontracts.InstanceEventContext, Microsoft.WindowsAzure.Management.Mon.Automation",
                        "authorization": {
                                "action": "Microsoft.Web/sites/start/action",
                                "scope": "/subscriptions/s1/resourcegroups/rg1/providers/Microsoft.Web/sites/leoalerttest"
                        },
                        "eventDataId": "327caaca-08d7-41b1-86d8-27d0a7adb92d",
                        "category": "Administrative",
                        "caller": "myname@mycompany.com",
                        "httpRequest": {
                                "clientRequestId": "f58cead8-c9ed-43af-8710-55e64def208d",
                                "clientIpAddress": "104.43.166.155",
                                "method": "POST"
                        },
                        "status": "Succeeded",
                        "subStatus": "OK",
                        "level": "Informational",
                        "correlationId": "4a40beaa-6a63-4d92-85c4-923a25abb590",
                        "eventDescription": "",
                        "operationName": "Microsoft.Web/sites/start/action",
                        "operationId": "4a40beaa-6a63-4d92-85c4-923a25abb590",
                        "properties": {
                                "$type": "Microsoft.WindowsAzure.Management.Common.Storage.CasePreservedDictionary, Microsoft.WindowsAzure.Management.Common.Storage",
                                "statusCode": "OK",
                                "serviceRequestId": "f7716681-496a-4f5c-8d14-d564bcf54714"
                        }
                },
                "timestamp": "Friday, March 11, 2016 9:13:23 PM",
                "id": "/subscriptions/s1/resourceGroups/rg1/providers/microsoft.insights/alertrules/alertonevent2",
                "name": "alertonevent2",
                "description": "test alert on event start",
                "conditionType": "Event",
                "subscriptionId": "s1",
                "resourceId": "/subscriptions/s1/resourcegroups/rg1/providers/Microsoft.Web/sites/leoalerttest",
                "resourceGroupName": "rg1"
        },
        "properties": {
                "key1": "value1",
                "key2": "value2"
        }
}
```

| <span data-ttu-id="60dea-121">元素名稱</span><span class="sxs-lookup"><span data-stu-id="60dea-121">Element Name</span></span> | <span data-ttu-id="60dea-122">說明</span><span class="sxs-lookup"><span data-stu-id="60dea-122">Description</span></span> |
| --- | --- |
| <span data-ttu-id="60dea-123">status</span><span class="sxs-lookup"><span data-stu-id="60dea-123">status</span></span> |<span data-ttu-id="60dea-124">用於度量警示。</span><span class="sxs-lookup"><span data-stu-id="60dea-124">Used for metric alerts.</span></span> <span data-ttu-id="60dea-125">一定會設定太 「 啟動 」 的活動記錄檔的警示。</span><span class="sxs-lookup"><span data-stu-id="60dea-125">Always set too"activated" for Activity Log alerts.</span></span> |
| <span data-ttu-id="60dea-126">context</span><span class="sxs-lookup"><span data-stu-id="60dea-126">context</span></span> |<span data-ttu-id="60dea-127">Hello 事件的內容。</span><span class="sxs-lookup"><span data-stu-id="60dea-127">Context of hello event.</span></span> |
| <span data-ttu-id="60dea-128">resourceProviderName</span><span class="sxs-lookup"><span data-stu-id="60dea-128">resourceProviderName</span></span> |<span data-ttu-id="60dea-129">hello 資源提供者的 hello 影響資源。</span><span class="sxs-lookup"><span data-stu-id="60dea-129">hello resource provider of hello impacted resource.</span></span> |
| <span data-ttu-id="60dea-130">conditionType</span><span class="sxs-lookup"><span data-stu-id="60dea-130">conditionType</span></span> |<span data-ttu-id="60dea-131">一律為「事件」。</span><span class="sxs-lookup"><span data-stu-id="60dea-131">Always "Event."</span></span> |
| <span data-ttu-id="60dea-132">名稱</span><span class="sxs-lookup"><span data-stu-id="60dea-132">name</span></span> |<span data-ttu-id="60dea-133">Hello 警示規則的名稱。</span><span class="sxs-lookup"><span data-stu-id="60dea-133">Name of hello alert rule.</span></span> |
| <span data-ttu-id="60dea-134">id</span><span class="sxs-lookup"><span data-stu-id="60dea-134">id</span></span> |<span data-ttu-id="60dea-135">Hello 警示的資源識別碼。</span><span class="sxs-lookup"><span data-stu-id="60dea-135">Resource ID of hello alert.</span></span> |
| <span data-ttu-id="60dea-136">說明</span><span class="sxs-lookup"><span data-stu-id="60dea-136">description</span></span> |<span data-ttu-id="60dea-137">Hello 警示建立期間所設定警示描述。</span><span class="sxs-lookup"><span data-stu-id="60dea-137">Alert description as set during creation of hello alert.</span></span> |
| <span data-ttu-id="60dea-138">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="60dea-138">subscriptionId</span></span> |<span data-ttu-id="60dea-139">Azure 訂用帳戶識別碼。</span><span class="sxs-lookup"><span data-stu-id="60dea-139">Azure Subscription ID.</span></span> |
| <span data-ttu-id="60dea-140">timestamp</span><span class="sxs-lookup"><span data-stu-id="60dea-140">timestamp</span></span> |<span data-ttu-id="60dea-141">Hello 處理 hello 要求的 Azure 服務所產生的 hello 事件的時間。</span><span class="sxs-lookup"><span data-stu-id="60dea-141">Time at which hello event was generated by hello Azure service that processed hello request.</span></span> |
| <span data-ttu-id="60dea-142">resourceId</span><span class="sxs-lookup"><span data-stu-id="60dea-142">resourceId</span></span> |<span data-ttu-id="60dea-143">資源識別碼 hello 影響資源。</span><span class="sxs-lookup"><span data-stu-id="60dea-143">Resource ID of hello impacted resource.</span></span> |
| <span data-ttu-id="60dea-144">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="60dea-144">resourceGroupName</span></span> |<span data-ttu-id="60dea-145">Hello hello 資源群組名稱會影響資源</span><span class="sxs-lookup"><span data-stu-id="60dea-145">Name of hello resource group for hello impacted resource</span></span> |
| <span data-ttu-id="60dea-146">屬性</span><span class="sxs-lookup"><span data-stu-id="60dea-146">properties</span></span> |<span data-ttu-id="60dea-147">一組`<Key, Value>`組 (也就是`Dictionary<String, String>`)，包括有關 hello 事件的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="60dea-147">Set of `<Key, Value>` pairs (i.e. `Dictionary<String, String>`) that includes details about hello event.</span></span> |
| <span data-ttu-id="60dea-148">事件</span><span class="sxs-lookup"><span data-stu-id="60dea-148">event</span></span> |<span data-ttu-id="60dea-149">包含有關 hello 事件的中繼資料元素。</span><span class="sxs-lookup"><span data-stu-id="60dea-149">Element containing metadata about hello event.</span></span> |
| <span data-ttu-id="60dea-150">授權</span><span class="sxs-lookup"><span data-stu-id="60dea-150">authorization</span></span> |<span data-ttu-id="60dea-151">hello hello 事件的 RBAC 屬性。</span><span class="sxs-lookup"><span data-stu-id="60dea-151">hello RBAC properties of hello event.</span></span> <span data-ttu-id="60dea-152">這些通常包括 hello 「 動作 」、 「 角色 」 和 hello 」 範圍中 」。</span><span class="sxs-lookup"><span data-stu-id="60dea-152">These usually include hello “action”, “role” and hello “scope.”</span></span> |
| <span data-ttu-id="60dea-153">category</span><span class="sxs-lookup"><span data-stu-id="60dea-153">category</span></span> |<span data-ttu-id="60dea-154">Hello 事件類別目錄。</span><span class="sxs-lookup"><span data-stu-id="60dea-154">Category of hello event.</span></span> <span data-ttu-id="60dea-155">支援值包括︰管理、警示、安全性、ServiceHealth、建議。</span><span class="sxs-lookup"><span data-stu-id="60dea-155">Supported values include: Administrative, Alert, Security, ServiceHealth, Recommendation.</span></span> |
| <span data-ttu-id="60dea-156">呼叫者</span><span class="sxs-lookup"><span data-stu-id="60dea-156">caller</span></span> |<span data-ttu-id="60dea-157">執行 hello 作業、 UPN 宣告或 SPN 宣告根據可用性的 hello 使用者的電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="60dea-157">Email address of hello user who performed hello operation, UPN claim, or SPN claim based on availability.</span></span> <span data-ttu-id="60dea-158">特定系統呼叫可為 Null。</span><span class="sxs-lookup"><span data-stu-id="60dea-158">Can be null for certain system calls.</span></span> |
| <span data-ttu-id="60dea-159">correlationId</span><span class="sxs-lookup"><span data-stu-id="60dea-159">correlationId</span></span> |<span data-ttu-id="60dea-160">通常是字串格式的 GUID。</span><span class="sxs-lookup"><span data-stu-id="60dea-160">Usually a GUID in string format.</span></span> <span data-ttu-id="60dea-161">具有相互關聯識別碼的事件屬於 toohello 相同較大的動作，通常會共用的相互關聯識別碼。</span><span class="sxs-lookup"><span data-stu-id="60dea-161">Events with correlationId belong toohello same larger action and usually share a correlationId.</span></span> |
| <span data-ttu-id="60dea-162">eventDescription</span><span class="sxs-lookup"><span data-stu-id="60dea-162">eventDescription</span></span> |<span data-ttu-id="60dea-163">Hello 事件的靜態文字描述。</span><span class="sxs-lookup"><span data-stu-id="60dea-163">Static text description of hello event.</span></span> |
| <span data-ttu-id="60dea-164">eventDataId</span><span class="sxs-lookup"><span data-stu-id="60dea-164">eventDataId</span></span> |<span data-ttu-id="60dea-165">Hello 事件的唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="60dea-165">Unique identifier for hello event.</span></span> |
| <span data-ttu-id="60dea-166">eventSource</span><span class="sxs-lookup"><span data-stu-id="60dea-166">eventSource</span></span> |<span data-ttu-id="60dea-167">名稱 hello Azure 服務或基礎結構產生的 hello 事件。</span><span class="sxs-lookup"><span data-stu-id="60dea-167">Name of hello Azure service or infrastructure that generated hello event.</span></span> |
| <span data-ttu-id="60dea-168">httpRequest</span><span class="sxs-lookup"><span data-stu-id="60dea-168">httpRequest</span></span> |<span data-ttu-id="60dea-169">通常包括 hello"clientRequestId"、"clientIpAddress"和"method"(例如 PUT HTTP 方法)。</span><span class="sxs-lookup"><span data-stu-id="60dea-169">Usually includes hello “clientRequestId”, “clientIpAddress” and “method” (HTTP method e.g. PUT).</span></span> |
| <span data-ttu-id="60dea-170">層級</span><span class="sxs-lookup"><span data-stu-id="60dea-170">level</span></span> |<span data-ttu-id="60dea-171">Hello 下列值之一:"Critical"、"Error"、"Warning"、"Informational"和"Verbose"。</span><span class="sxs-lookup"><span data-stu-id="60dea-171">One of hello following values: “Critical”, “Error”, “Warning”, “Informational” and “Verbose.”</span></span> |
| <span data-ttu-id="60dea-172">operationId</span><span class="sxs-lookup"><span data-stu-id="60dea-172">operationId</span></span> |<span data-ttu-id="60dea-173">通常是在對應 toosingle 作業 hello 事件之間共用的 GUID。</span><span class="sxs-lookup"><span data-stu-id="60dea-173">Usually a GUID shared among hello events corresponding toosingle operation.</span></span> |
| <span data-ttu-id="60dea-174">operationName</span><span class="sxs-lookup"><span data-stu-id="60dea-174">operationName</span></span> |<span data-ttu-id="60dea-175">Hello 作業的名稱。</span><span class="sxs-lookup"><span data-stu-id="60dea-175">Name of hello operation.</span></span> |
| <span data-ttu-id="60dea-176">屬性</span><span class="sxs-lookup"><span data-stu-id="60dea-176">properties</span></span> |<span data-ttu-id="60dea-177">Hello 事件的屬性。</span><span class="sxs-lookup"><span data-stu-id="60dea-177">Properties of hello event.</span></span> |
| <span data-ttu-id="60dea-178">status</span><span class="sxs-lookup"><span data-stu-id="60dea-178">status</span></span> |<span data-ttu-id="60dea-179">字串。</span><span class="sxs-lookup"><span data-stu-id="60dea-179">String.</span></span> <span data-ttu-id="60dea-180">Hello 作業的狀態。</span><span class="sxs-lookup"><span data-stu-id="60dea-180">Status of hello operation.</span></span> <span data-ttu-id="60dea-181">常見的值包括︰「已啟動」、「進行中」、「成功」、「失敗」、「使用中」、「已解決」。</span><span class="sxs-lookup"><span data-stu-id="60dea-181">Common values include: "Started", "In Progress", "Succeeded", "Failed", "Active", "Resolved".</span></span> |
| <span data-ttu-id="60dea-182">子狀態</span><span class="sxs-lookup"><span data-stu-id="60dea-182">subStatus</span></span> |<span data-ttu-id="60dea-183">通常包含對應 REST 呼叫 hello hello HTTP 狀態碼。</span><span class="sxs-lookup"><span data-stu-id="60dea-183">Usually includes hello HTTP status code of hello corresponding REST call.</span></span> <span data-ttu-id="60dea-184">它也可以包含其他描述子狀態的字串。</span><span class="sxs-lookup"><span data-stu-id="60dea-184">It might also include other strings describing a substatus.</span></span> <span data-ttu-id="60dea-185">常見子狀態的值包括：確定 (HTTP 狀態碼︰200)，已建立 (HTTP 狀態碼︰201)、接受 (HTTP 狀態碼︰202)、沒有內容 (HTTP 狀態碼︰204)、不正確的要求 (HTTP 狀態碼︰400)、找不到 (HTTP 狀態碼︰404)，衝突 (HTTP 狀態碼︰409)、內部伺服器錯誤 (HTTP 狀態碼︰500)、服務無法使用 (HTTP 狀態碼︰503)、閘道逾時 (HTTP 狀態碼︰504)</span><span class="sxs-lookup"><span data-stu-id="60dea-185">Common substatus values include: OK (HTTP Status Code: 200), Created (HTTP Status Code: 201), Accepted (HTTP Status Code: 202), No Content (HTTP Status Code: 204), Bad Request (HTTP Status Code: 400), Not Found (HTTP Status Code: 404), Conflict (HTTP Status Code: 409), Internal Server Error (HTTP Status Code: 500), Service Unavailable (HTTP Status Code: 503), Gateway Timeout (HTTP Status Code: 504)</span></span> |

## <a name="next-steps"></a><span data-ttu-id="60dea-186">後續步驟</span><span class="sxs-lookup"><span data-stu-id="60dea-186">Next steps</span></span>
* [<span data-ttu-id="60dea-187">深入了解 hello 活動記錄檔</span><span class="sxs-lookup"><span data-stu-id="60dea-187">Learn more about hello Activity Log</span></span>](monitoring-overview-activity-logs.md)
* [<span data-ttu-id="60dea-188">對 Azure 警示執行 Azure 自動化指令碼 (Runbook)</span><span class="sxs-lookup"><span data-stu-id="60dea-188">Execute Azure Automation scripts (Runbooks) on Azure alerts</span></span>](http://go.microsoft.com/fwlink/?LinkId=627081)
* <span data-ttu-id="60dea-189">[使用邏輯應用程式在從 Azure 警示 toosend Twilio 透過 SMS](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-text-message-with-logic-app)。</span><span class="sxs-lookup"><span data-stu-id="60dea-189">[Use Logic App toosend an SMS via Twilio from an Azure alert](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-text-message-with-logic-app).</span></span> <span data-ttu-id="60dea-190">這個範例適用於度量的警示，但可能已修改的 toowork 活動記錄警示。</span><span class="sxs-lookup"><span data-stu-id="60dea-190">This example is for metric alerts, but could be modified toowork with an Activity Log alert.</span></span>
* <span data-ttu-id="60dea-191">[使用邏輯應用程式 toosend Slack 訊息從 Azure 警示](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-slack-with-logic-app)。</span><span class="sxs-lookup"><span data-stu-id="60dea-191">[Use Logic App toosend a Slack message from an Azure alert](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-slack-with-logic-app).</span></span> <span data-ttu-id="60dea-192">這個範例適用於度量的警示，但可能已修改的 toowork 活動記錄警示。</span><span class="sxs-lookup"><span data-stu-id="60dea-192">This example is for metric alerts, but could be modified toowork with an Activity Log alert.</span></span>
* <span data-ttu-id="60dea-193">[使用邏輯應用程式 toosend 從 Azure 警示訊息 tooan Azure 佇列](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-queue-with-logic-app)。</span><span class="sxs-lookup"><span data-stu-id="60dea-193">[Use Logic App toosend a message tooan Azure Queue from an Azure alert](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-queue-with-logic-app).</span></span> <span data-ttu-id="60dea-194">這個範例適用於度量的警示，但可能已修改的 toowork 活動記錄警示。</span><span class="sxs-lookup"><span data-stu-id="60dea-194">This example is for metric alerts, but could be modified toowork with an Activity Log alert.</span></span>
