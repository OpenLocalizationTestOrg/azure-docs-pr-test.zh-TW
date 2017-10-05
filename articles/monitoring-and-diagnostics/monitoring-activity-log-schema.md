---
title: "Azure 活動記錄事件結構描述 | Microsoft Docs"
description: "了解發出至活動記錄之資料的事件結構描述"
author: johnkemnetz
manager: robb
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: johnkem
ms.openlocfilehash: a4ceb822e0ec3e1c1dc31ece1db761834e795f6c
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="azure-activity-log-event-schema"></a><span data-ttu-id="09bb1-103">Azure 活動記錄事件結構描述</span><span class="sxs-lookup"><span data-stu-id="09bb1-103">Azure Activity Log event schema</span></span>
<span data-ttu-id="09bb1-104">透過「Azure 活動記錄」，您可深入了解 Azure 中發生的任何訂用帳戶層級事件。</span><span class="sxs-lookup"><span data-stu-id="09bb1-104">The **Azure Activity Log** is a log that provides insight into any subscription-level events that have occurred in Azure.</span></span> <span data-ttu-id="09bb1-105">本文說明每個資料類別的事件結構描述。</span><span class="sxs-lookup"><span data-stu-id="09bb1-105">This article describes the event schema per category of data.</span></span>

## <a name="administrative"></a><span data-ttu-id="09bb1-106">管理</span><span class="sxs-lookup"><span data-stu-id="09bb1-106">Administrative</span></span>
<span data-ttu-id="09bb1-107">透過 Resource Manager 執行的所有建立、更新、刪除和動作作業皆記錄在此類別中。</span><span class="sxs-lookup"><span data-stu-id="09bb1-107">This category contains the record of all create, update, delete, and action operations performed through Resource Manager.</span></span> <span data-ttu-id="09bb1-108">您可能會在此類別中看到的事件類型範例包括「建立虛擬機器」和「刪除網路安全性群組」。使用者或應用程式使用 Resource Manager 所執行的每個動作，都會成為特定資源類型上的作業模型。</span><span class="sxs-lookup"><span data-stu-id="09bb1-108">Examples of the types of events you would see in this category include "create virtual machine" and "delete network security group" Every action taken by a user or application using Resource Manager is modeled as an operation on a particular resource type.</span></span> <span data-ttu-id="09bb1-109">如果作業類型為「寫入」、「刪除」或「動作」，則該作業的啟動及成功或失敗記錄皆會記錄在「系統管理」類別。</span><span class="sxs-lookup"><span data-stu-id="09bb1-109">If the operation type is Write, Delete, or Action, the records of both the start and success or fail of that operation are recorded in the Administrative category.</span></span> <span data-ttu-id="09bb1-110">「系統管理」類別也包含訂用帳戶中角色型存取控制的所有變更。</span><span class="sxs-lookup"><span data-stu-id="09bb1-110">The Administrative category also includes any changes to role-based access control in a subscription.</span></span>

### <a name="sample-event"></a><span data-ttu-id="09bb1-111">範例事件</span><span class="sxs-lookup"><span data-stu-id="09bb1-111">Sample event</span></span>
```json
{
  "authorization": {
    "action": "microsoft.support/supporttickets/write",
    "role": "Subscription Admin",
    "scope": "/subscriptions/s1/resourceGroups/MSSupportGroup/providers/microsoft.support/supporttickets/115012112305841"
  },
  "caller": "admin@contoso.com",
  "channels": "Operation",
  "claims": {
    "aud": "https://management.core.windows.net/",
    "iss": "https://sts.windows.net/72f988bf-86f1-41af-91ab-2d7cd011db47/",
    "iat": "1421876371",
    "nbf": "1421876371",
    "exp": "1421880271",
    "ver": "1.0",
    "http://schemas.microsoft.com/identity/claims/tenantid": "1e8d8218-c5e7-4578-9acc-9abbd5d23315 ",
    "http://schemas.microsoft.com/claims/authnmethodsreferences": "pwd",
    "http://schemas.microsoft.com/identity/claims/objectidentifier": "2468adf0-8211-44e3-95xq-85137af64708",
    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn": "admin@contoso.com",
    "puid": "20030000801A118C",
    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier": "9vckmEGF7zDKk1YzIY8k0t1_EAPaXoeHyPRn6f413zM",
    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname": "John",
    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname": "Smith",
    "name": "John Smith",
    "groups": "cacfe77c-e058-4712-83qw-f9b08849fd60,7f71d11d-4c41-4b23-99d2-d32ce7aa621c,31522864-0578-4ea0-9gdc-e66cc564d18c",
    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name": " admin@contoso.com",
    "appid": "c44b4083-3bq0-49c1-b47d-974e53cbdf3c",
    "appidacr": "2",
    "http://schemas.microsoft.com/identity/claims/scope": "user_impersonation",
    "http://schemas.microsoft.com/claims/authnclassreference": "1"
  },
  "correlationId": "1e121103-0ba6-4300-ac9d-952bb5d0c80f",
  "description": "",
  "eventDataId": "44ade6b4-3813-45e6-ae27-7420a95fa2f8",
  "eventName": {
    "value": "EndRequest",
    "localizedValue": "End request"
  },
  "httpRequest": {
    "clientRequestId": "27003b25-91d3-418f-8eb1-29e537dcb249",
    "clientIpAddress": "192.168.35.115",
    "method": "PUT"
  },
  "id": "/subscriptions/s1/resourceGroups/MSSupportGroup/providers/microsoft.support/supporttickets/115012112305841/events/44ade6b4-3813-45e6-ae27-7420a95fa2f8/ticks/635574752669792776",
  "level": "Informational",
  "resourceGroupName": "MSSupportGroup",
  "resourceProviderName": {
    "value": "microsoft.support",
    "localizedValue": "microsoft.support"
  },
  "resourceUri": "/subscriptions/s1/resourceGroups/MSSupportGroup/providers/microsoft.support/supporttickets/115012112305841",
  "operationId": "1e121103-0ba6-4300-ac9d-952bb5d0c80f",
  "operationName": {
    "value": "microsoft.support/supporttickets/write",
    "localizedValue": "microsoft.support/supporttickets/write"
  },
  "properties": {
    "statusCode": "Created"
  },
  "status": {
    "value": "Succeeded",
    "localizedValue": "Succeeded"
  },
  "subStatus": {
    "value": "Created",
    "localizedValue": "Created (HTTP Status Code: 201)"
  },
  "eventTimestamp": "2015-01-21T22:14:26.9792776Z",
  "submissionTimestamp": "2015-01-21T22:14:39.9936304Z",
  "subscriptionId": "s1"
}
```

### <a name="property-descriptions"></a><span data-ttu-id="09bb1-112">屬性描述</span><span class="sxs-lookup"><span data-stu-id="09bb1-112">Property descriptions</span></span>
| <span data-ttu-id="09bb1-113">元素名稱</span><span class="sxs-lookup"><span data-stu-id="09bb1-113">Element Name</span></span> | <span data-ttu-id="09bb1-114">說明</span><span class="sxs-lookup"><span data-stu-id="09bb1-114">Description</span></span> |
| --- | --- |
| <span data-ttu-id="09bb1-115">授權</span><span class="sxs-lookup"><span data-stu-id="09bb1-115">authorization</span></span> |<span data-ttu-id="09bb1-116">事件的 RBAC 屬性的 blob。</span><span class="sxs-lookup"><span data-stu-id="09bb1-116">Blob of RBAC properties of the event.</span></span> <span data-ttu-id="09bb1-117">通常包括 action、role 和 scope 屬性。</span><span class="sxs-lookup"><span data-stu-id="09bb1-117">Usually includes the “action”, “role” and “scope” properties.</span></span> |
| <span data-ttu-id="09bb1-118">呼叫者</span><span class="sxs-lookup"><span data-stu-id="09bb1-118">caller</span></span> |<span data-ttu-id="09bb1-119">已執行作業的使用者的電子郵件地址，根據可用性的 UPN 宣告或 SPN 宣告。</span><span class="sxs-lookup"><span data-stu-id="09bb1-119">Email address of the user who has performed the operation, UPN claim, or SPN claim based on availability.</span></span> |
| <span data-ttu-id="09bb1-120">通道</span><span class="sxs-lookup"><span data-stu-id="09bb1-120">channels</span></span> |<span data-ttu-id="09bb1-121">為下列其中一個值：Admin、Operation</span><span class="sxs-lookup"><span data-stu-id="09bb1-121">One of the following values: “Admin”, “Operation”</span></span> |
| <span data-ttu-id="09bb1-122">claims</span><span class="sxs-lookup"><span data-stu-id="09bb1-122">claims</span></span> |<span data-ttu-id="09bb1-123">Active Directory 用來驗證使用者或應用程式以在 Resource Manager 中執行此作業的 JWT 權杖。</span><span class="sxs-lookup"><span data-stu-id="09bb1-123">The JWT token used by Active Directory to authenticate the user or application to perform this operation in resource manager.</span></span> |
| <span data-ttu-id="09bb1-124">correlationId</span><span class="sxs-lookup"><span data-stu-id="09bb1-124">correlationId</span></span> |<span data-ttu-id="09bb1-125">通常是字串格式的 GUID。</span><span class="sxs-lookup"><span data-stu-id="09bb1-125">Usually a GUID in the string format.</span></span> <span data-ttu-id="09bb1-126">具有相同 correlationId、屬於同一 uber 動作的事件。</span><span class="sxs-lookup"><span data-stu-id="09bb1-126">Events that share a correlationId belong to the same uber action.</span></span> |
| <span data-ttu-id="09bb1-127">說明</span><span class="sxs-lookup"><span data-stu-id="09bb1-127">description</span></span> |<span data-ttu-id="09bb1-128">事件的靜態文字描述。</span><span class="sxs-lookup"><span data-stu-id="09bb1-128">Static text description of an event.</span></span> |
| <span data-ttu-id="09bb1-129">eventDataId</span><span class="sxs-lookup"><span data-stu-id="09bb1-129">eventDataId</span></span> |<span data-ttu-id="09bb1-130">事件的唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="09bb1-130">Unique identifier of an event.</span></span> |
| <span data-ttu-id="09bb1-131">httpRequest</span><span class="sxs-lookup"><span data-stu-id="09bb1-131">httpRequest</span></span> |<span data-ttu-id="09bb1-132">描述 HTTP 要求的 blob。</span><span class="sxs-lookup"><span data-stu-id="09bb1-132">Blob describing the Http Request.</span></span> <span data-ttu-id="09bb1-133">通常包括 “clientRequestId”、“clientIpAddress”和 “method” (HTTP 方法。</span><span class="sxs-lookup"><span data-stu-id="09bb1-133">Usually includes the “clientRequestId”, “clientIpAddress” and “method” (HTTP method.</span></span> <span data-ttu-id="09bb1-134">例如，PUT)。</span><span class="sxs-lookup"><span data-stu-id="09bb1-134">For example, PUT).</span></span> |
| <span data-ttu-id="09bb1-135">層級</span><span class="sxs-lookup"><span data-stu-id="09bb1-135">level</span></span> |<span data-ttu-id="09bb1-136">事件的層級。</span><span class="sxs-lookup"><span data-stu-id="09bb1-136">Level of the event.</span></span> <span data-ttu-id="09bb1-137">下列其中一個值：重大、錯誤、警告、資訊和詳細資訊</span><span class="sxs-lookup"><span data-stu-id="09bb1-137">One of the following values: “Critical”, “Error”, “Warning”, “Informational” and “Verbose”</span></span> |
| <span data-ttu-id="09bb1-138">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="09bb1-138">resourceGroupName</span></span> |<span data-ttu-id="09bb1-139">受影響資源的資源群組的名稱。</span><span class="sxs-lookup"><span data-stu-id="09bb1-139">Name of the resource group for the impacted resource.</span></span> |
| <span data-ttu-id="09bb1-140">resourceProviderName</span><span class="sxs-lookup"><span data-stu-id="09bb1-140">resourceProviderName</span></span> |<span data-ttu-id="09bb1-141">受影響資源的資源提供者的名稱。</span><span class="sxs-lookup"><span data-stu-id="09bb1-141">Name of the resource provider for the impacted resource</span></span> |
| <span data-ttu-id="09bb1-142">resourceId</span><span class="sxs-lookup"><span data-stu-id="09bb1-142">resourceId</span></span> |<span data-ttu-id="09bb1-143">受影響資源的資源識別碼。</span><span class="sxs-lookup"><span data-stu-id="09bb1-143">Resource id of the impacted resource.</span></span> |
| <span data-ttu-id="09bb1-144">operationId</span><span class="sxs-lookup"><span data-stu-id="09bb1-144">operationId</span></span> |<span data-ttu-id="09bb1-145">對應至單一作業的事件共用的 GUID。</span><span class="sxs-lookup"><span data-stu-id="09bb1-145">A GUID shared among the events that correspond to a single operation.</span></span> |
| <span data-ttu-id="09bb1-146">operationName</span><span class="sxs-lookup"><span data-stu-id="09bb1-146">operationName</span></span> |<span data-ttu-id="09bb1-147">作業名稱。</span><span class="sxs-lookup"><span data-stu-id="09bb1-147">Name of the operation.</span></span> |
| <span data-ttu-id="09bb1-148">properties</span><span class="sxs-lookup"><span data-stu-id="09bb1-148">properties</span></span> |<span data-ttu-id="09bb1-149">描述事件詳細資料的一組 `<Key, Value>` 配對 (也就是字典)。</span><span class="sxs-lookup"><span data-stu-id="09bb1-149">Set of `<Key, Value>` pairs (that is, a Dictionary) describing the details of the event.</span></span> |
| <span data-ttu-id="09bb1-150">status</span><span class="sxs-lookup"><span data-stu-id="09bb1-150">status</span></span> |<span data-ttu-id="09bb1-151">字串，描述作業的狀態。</span><span class="sxs-lookup"><span data-stu-id="09bb1-151">String describing the status of the operation.</span></span> <span data-ttu-id="09bb1-152">常見的值包括︰Started、In Progress、Succeeded、Failed、Active、Resolved。</span><span class="sxs-lookup"><span data-stu-id="09bb1-152">Some common values are: Started, In Progress, Succeeded, Failed, Active, Resolved.</span></span> |
| <span data-ttu-id="09bb1-153">子狀態</span><span class="sxs-lookup"><span data-stu-id="09bb1-153">subStatus</span></span> |<span data-ttu-id="09bb1-154">通常包含對應 REST 呼叫的 HTTP 狀態碼，但也可以包含其他描述子狀態的字串，常見的值包括：確定 (HTTP 狀態碼︰200)，已建立 (HTTP 狀態碼︰201)、接受 (HTTP 狀態碼︰202)、沒有內容 (HTTP 狀態碼︰204)、不正確的要求 (HTTP 狀態碼︰400)、找不到 (HTTP 狀態碼︰404)，衝突 (HTTP 狀態碼︰409)、內部伺服器錯誤 (HTTP 狀態碼︰500)、服務無法使用 (HTTP 狀態碼︰503)、閘道逾時 (HTTP 狀態碼︰504)。</span><span class="sxs-lookup"><span data-stu-id="09bb1-154">Usually the HTTP status code of the corresponding REST call, but can also include other strings describing a substatus, such as these common values: OK (HTTP Status Code: 200), Created (HTTP Status Code: 201), Accepted (HTTP Status Code: 202), No Content (HTTP Status Code: 204), Bad Request (HTTP Status Code: 400), Not Found (HTTP Status Code: 404), Conflict (HTTP Status Code: 409), Internal Server Error (HTTP Status Code: 500), Service Unavailable (HTTP Status Code: 503), Gateway Timeout (HTTP Status Code: 504).</span></span> |
| <span data-ttu-id="09bb1-155">eventTimestamp</span><span class="sxs-lookup"><span data-stu-id="09bb1-155">eventTimestamp</span></span> |<span data-ttu-id="09bb1-156">處理與事件對應之要求的Azure 服務產生事件時的時間戳記。</span><span class="sxs-lookup"><span data-stu-id="09bb1-156">Timestamp when the event was generated by the Azure service processing the request corresponding the event.</span></span> |
| <span data-ttu-id="09bb1-157">submissionTimestamp</span><span class="sxs-lookup"><span data-stu-id="09bb1-157">submissionTimestamp</span></span> |<span data-ttu-id="09bb1-158">當事件變成可供查詢時的時間戳記。</span><span class="sxs-lookup"><span data-stu-id="09bb1-158">Timestamp when the event became available for querying.</span></span> |
| <span data-ttu-id="09bb1-159">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="09bb1-159">subscriptionId</span></span> |<span data-ttu-id="09bb1-160">Azure 訂用帳戶識別碼。</span><span class="sxs-lookup"><span data-stu-id="09bb1-160">Azure Subscription Id.</span></span> |

## <a name="service-health"></a><span data-ttu-id="09bb1-161">服務健康情況</span><span class="sxs-lookup"><span data-stu-id="09bb1-161">Service health</span></span>
<span data-ttu-id="09bb1-162">所有在 Azure 中發生的服務健康情況事件皆記錄在此類別中。</span><span class="sxs-lookup"><span data-stu-id="09bb1-162">This category contains the record of any service health incidents that have occurred in Azure.</span></span> <span data-ttu-id="09bb1-163">您可能會在此類別中看到的事件類型範例為「美國東部的 SQL Azure 發生停機事件」。</span><span class="sxs-lookup"><span data-stu-id="09bb1-163">An example of the type of event you would see in this category is "SQL Azure in East US is experiencing downtime."</span></span> <span data-ttu-id="09bb1-164">服務健康情況事件有五個種類：「需要採取動作」、「協助復原」、「事件」、「維護」、「資訊」或「安全性」，這些事件只會在訂用帳戶中有可能會受該事件影響的資源時顯示。</span><span class="sxs-lookup"><span data-stu-id="09bb1-164">Service health events come in five varieties: Action Required, Assisted Recovery, Incident, Maintenance, Information, or Security, and only appear if you have a resource in the subscription that would be impacted by the event.</span></span>

### <a name="sample-event"></a><span data-ttu-id="09bb1-165">範例事件</span><span class="sxs-lookup"><span data-stu-id="09bb1-165">Sample event</span></span>
```json
{
  "channels": "Admin",
  "correlationId": "c550176b-8f52-4380-bdc5-36c1b59d3a44",
  "description": "Active: Network Infrastructure - UK South",
  "eventDataId": "c5bc4514-6642-2be3-453e-c6a67841b073",
  "eventName": {
      "value": null
  },
  "category": {
      "value": "ServiceHealth",
      "localizedValue": "Service Health"
  },
  "eventTimestamp": "2017-07-20T23:30:14.8022297Z",
  "id": "/subscriptions/mySubscriptionID/events/c5bc4514-6642-2be3-453e-c6a67841b073/ticks/636361902148022297",
  "level": "Warning",
  "operationName": {
      "value": "Microsoft.ServiceHealth/incident/action",
      "localizedValue": "Microsoft.ServiceHealth/incident/action"
  },
  "resourceProviderName": {
      "value": null
  },
  "resourceType": {
      "value": null,
      "localizedValue": ""
  },
  "resourceId": "/subscriptions/mySubscriptionID",
  "status": {
      "value": "Active",
      "localizedValue": "Active"
  },
  "subStatus": {
      "value": null
  },
  "submissionTimestamp": "2017-07-20T23:30:34.7431946Z",
  "subscriptionId": "mySubscriptionID",
  "properties": {
    "title": "Network Infrastructure - UK South",
    "service": "Service Fabric",
    "region": "UK South",
    "communication": "Starting at approximately 21:41 UTC on 20 Jul 2017, a subset of customers in UK South may experience degraded performance, connectivity drops or timeouts when accessing their Azure resources hosted in this region. Engineers are investigating underlying Network Infrastructure issues in this region. Impacted services may include, but are not limited to App Services, Automation, Service Bus, Log Analytics, Key Vault, SQL Database, Service Fabric, Event Hubs, Stream Analytics, Azure Data Movement, API Management, and Azure Search. Multiple engineering teams are engaged in multiple workflows to mitigate the impact. The next update will be provided in 60 minutes, or as events warrant.",
    "incidentType": "Incident",
    "trackingId": "NA0F-BJG",
    "impactStartTime": "2017-07-20T21:41:00.0000000Z",
    "impactedServices": "[{\"ImpactedRegions\":[{\"RegionName\":\"UK South\"}],\"ServiceName\":\"Service Fabric\"}]",
    "defaultLanguageTitle": "Network Infrastructure - UK South",
    "defaultLanguageContent": "Starting at approximately 21:41 UTC on 20 Jul 2017, a subset of customers in UK South may experience degraded performance, connectivity drops or timeouts when accessing their Azure resources hosted in this region. Engineers are investigating underlying Network Infrastructure issues in this region. Impacted services may include, but are not limited to App Services, Automation, Service Bus, Log Analytics, Key Vault, SQL Database, Service Fabric, Event Hubs, Stream Analytics, Azure Data Movement, API Management, and Azure Search. Multiple engineering teams are engaged in multiple workflows to mitigate the impact. The next update will be provided in 60 minutes, or as events warrant.",
    "stage": "Active",
    "communicationId": "636361902146035247",
    "version": "0.1.1"
  }
}
```

### <a name="property-descriptions"></a><span data-ttu-id="09bb1-166">屬性描述</span><span class="sxs-lookup"><span data-stu-id="09bb1-166">Property descriptions</span></span>
<span data-ttu-id="09bb1-167">元素名稱</span><span class="sxs-lookup"><span data-stu-id="09bb1-167">Element Name</span></span> | <span data-ttu-id="09bb1-168">說明</span><span class="sxs-lookup"><span data-stu-id="09bb1-168">Description</span></span>
-------- | -----------
<span data-ttu-id="09bb1-169">通道</span><span class="sxs-lookup"><span data-stu-id="09bb1-169">channels</span></span> | <span data-ttu-id="09bb1-170">為下列其中一個值：Admin、Operation</span><span class="sxs-lookup"><span data-stu-id="09bb1-170">Is one of the following values: “Admin”, “Operation”</span></span>
<span data-ttu-id="09bb1-171">correlationId</span><span class="sxs-lookup"><span data-stu-id="09bb1-171">correlationId</span></span> | <span data-ttu-id="09bb1-172">通常是字串格式的 GUID。</span><span class="sxs-lookup"><span data-stu-id="09bb1-172">Is usually a GUID in the string format.</span></span> <span data-ttu-id="09bb1-173">屬於相同 uber 動作的事件通常會共用同一個 correlationId。</span><span class="sxs-lookup"><span data-stu-id="09bb1-173">Events with that belong to the same uber action usually share the same correlationId.</span></span>
<span data-ttu-id="09bb1-174">說明</span><span class="sxs-lookup"><span data-stu-id="09bb1-174">description</span></span> | <span data-ttu-id="09bb1-175">事件的描述。</span><span class="sxs-lookup"><span data-stu-id="09bb1-175">Description of the event.</span></span>
<span data-ttu-id="09bb1-176">eventDataId</span><span class="sxs-lookup"><span data-stu-id="09bb1-176">eventDataId</span></span> | <span data-ttu-id="09bb1-177">事件的唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="09bb1-177">The unique identifier of an event.</span></span>
<span data-ttu-id="09bb1-178">eventName</span><span class="sxs-lookup"><span data-stu-id="09bb1-178">eventName</span></span> | <span data-ttu-id="09bb1-179">事件的標題。</span><span class="sxs-lookup"><span data-stu-id="09bb1-179">The title of the event.</span></span>
<span data-ttu-id="09bb1-180">層級</span><span class="sxs-lookup"><span data-stu-id="09bb1-180">level</span></span> | <span data-ttu-id="09bb1-181">事件的層級。</span><span class="sxs-lookup"><span data-stu-id="09bb1-181">Level of the event.</span></span> <span data-ttu-id="09bb1-182">下列其中一個值：重大、錯誤、警告、資訊和詳細資訊</span><span class="sxs-lookup"><span data-stu-id="09bb1-182">One of the following values: “Critical”, “Error”, “Warning”, “Informational” and “Verbose”</span></span>
<span data-ttu-id="09bb1-183">resourceProviderName</span><span class="sxs-lookup"><span data-stu-id="09bb1-183">resourceProviderName</span></span> | <span data-ttu-id="09bb1-184">受影響資源的資源提供者名稱。</span><span class="sxs-lookup"><span data-stu-id="09bb1-184">Name of the resource provider for the impacted resource.</span></span> <span data-ttu-id="09bb1-185">如果未知，此參數會是 null。</span><span class="sxs-lookup"><span data-stu-id="09bb1-185">If not known, this will be null.</span></span>
<span data-ttu-id="09bb1-186">resourceType</span><span class="sxs-lookup"><span data-stu-id="09bb1-186">resourceType</span></span>| <span data-ttu-id="09bb1-187">受影響資源的資源類型。</span><span class="sxs-lookup"><span data-stu-id="09bb1-187">The type of resource of the impacted resource.</span></span> <span data-ttu-id="09bb1-188">如果未知，此參數會是 null。</span><span class="sxs-lookup"><span data-stu-id="09bb1-188">If not known, this will be null.</span></span>
<span data-ttu-id="09bb1-189">子狀態</span><span class="sxs-lookup"><span data-stu-id="09bb1-189">subStatus</span></span> | <span data-ttu-id="09bb1-190">針對服務健康情況事件通常為 null。</span><span class="sxs-lookup"><span data-stu-id="09bb1-190">Usually null for Service Health events.</span></span>
<span data-ttu-id="09bb1-191">eventTimestamp</span><span class="sxs-lookup"><span data-stu-id="09bb1-191">eventTimestamp</span></span> | <span data-ttu-id="09bb1-192">記錄事件產生並提交至活動記錄時的時間戳記。</span><span class="sxs-lookup"><span data-stu-id="09bb1-192">Timestamp when the log event was generated and submitted to the Activity Log.</span></span>
<span data-ttu-id="09bb1-193">submissionTimestamp</span><span class="sxs-lookup"><span data-stu-id="09bb1-193">submissionTimestamp</span></span> |   <span data-ttu-id="09bb1-194">事件在活動記錄中可供查詢時的時間戳記。</span><span class="sxs-lookup"><span data-stu-id="09bb1-194">Timestamp when the event became available in the Activity Log.</span></span>
<span data-ttu-id="09bb1-195">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="09bb1-195">subscriptionId</span></span> | <span data-ttu-id="09bb1-196">記錄此事件的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="09bb1-196">The Azure subscription in which this event was logged.</span></span>
<span data-ttu-id="09bb1-197">status</span><span class="sxs-lookup"><span data-stu-id="09bb1-197">status</span></span> | <span data-ttu-id="09bb1-198">字串，描述作業的狀態。</span><span class="sxs-lookup"><span data-stu-id="09bb1-198">String describing the status of the operation.</span></span> <span data-ttu-id="09bb1-199">某些常見的值為：Active、Resolved。</span><span class="sxs-lookup"><span data-stu-id="09bb1-199">Some common values are: Active, Resolved.</span></span>
<span data-ttu-id="09bb1-200">operationName</span><span class="sxs-lookup"><span data-stu-id="09bb1-200">operationName</span></span> | <span data-ttu-id="09bb1-201">作業名稱。</span><span class="sxs-lookup"><span data-stu-id="09bb1-201">Name of the operation.</span></span> <span data-ttu-id="09bb1-202">通常是 Microsoft.ServiceHealth/incident/action。</span><span class="sxs-lookup"><span data-stu-id="09bb1-202">Usually Microsoft.ServiceHealth/incident/action.</span></span>
<span data-ttu-id="09bb1-203">category</span><span class="sxs-lookup"><span data-stu-id="09bb1-203">category</span></span> | <span data-ttu-id="09bb1-204">"ServiceHealth"</span><span class="sxs-lookup"><span data-stu-id="09bb1-204">"ServiceHealth"</span></span>
<span data-ttu-id="09bb1-205">resourceId</span><span class="sxs-lookup"><span data-stu-id="09bb1-205">resourceId</span></span> | <span data-ttu-id="09bb1-206">受影響資源的資源識別碼 (如果知道)。</span><span class="sxs-lookup"><span data-stu-id="09bb1-206">Resource id of the impacted resource, if known.</span></span> <span data-ttu-id="09bb1-207">否則會提供訂用帳戶識別碼。</span><span class="sxs-lookup"><span data-stu-id="09bb1-207">Subscription ID is provided otherwise.</span></span>
<span data-ttu-id="09bb1-208">Properties.title</span><span class="sxs-lookup"><span data-stu-id="09bb1-208">Properties.title</span></span> | <span data-ttu-id="09bb1-209">此通訊的當地語系化標題。</span><span class="sxs-lookup"><span data-stu-id="09bb1-209">The localized title for this communication.</span></span> <span data-ttu-id="09bb1-210">預設語言為英文。</span><span class="sxs-lookup"><span data-stu-id="09bb1-210">English is the default language.</span></span>
<span data-ttu-id="09bb1-211">Properties.communication</span><span class="sxs-lookup"><span data-stu-id="09bb1-211">Properties.communication</span></span> | <span data-ttu-id="09bb1-212">與 HTML 標記通訊的詳細資料 (已當地語系化)。</span><span class="sxs-lookup"><span data-stu-id="09bb1-212">The localized details of the communication with HTML markup.</span></span> <span data-ttu-id="09bb1-213">預設語言為英文。</span><span class="sxs-lookup"><span data-stu-id="09bb1-213">English is the default.</span></span>
<span data-ttu-id="09bb1-214">Properties.incidentType</span><span class="sxs-lookup"><span data-stu-id="09bb1-214">Properties.incidentType</span></span> | <span data-ttu-id="09bb1-215">可能的值：AssistedRecovery、ActionRequired、Information、Incident、Maintenance、Security</span><span class="sxs-lookup"><span data-stu-id="09bb1-215">Possible values: AssistedRecovery, ActionRequired, Information, Incident, Maintenance, Security</span></span>
<span data-ttu-id="09bb1-216">Properties.trackingId</span><span class="sxs-lookup"><span data-stu-id="09bb1-216">Properties.trackingId</span></span> | <span data-ttu-id="09bb1-217">識別與此事件 (event) 相關聯的附帶事件 (Incident)。</span><span class="sxs-lookup"><span data-stu-id="09bb1-217">Identifies the incident this event is associated with.</span></span> <span data-ttu-id="09bb1-218">可用此屬性讓與附帶事件 (Incident) 有關的事件 (event) 相關聯。</span><span class="sxs-lookup"><span data-stu-id="09bb1-218">Use this to correlate the events related to an incident.</span></span>
<span data-ttu-id="09bb1-219">Properties.impactedServices</span><span class="sxs-lookup"><span data-stu-id="09bb1-219">Properties.impactedServices</span></span> | <span data-ttu-id="09bb1-220">逸出的 JSON blob，描述受到附帶事件 (Incident) 影響的服務和區域。</span><span class="sxs-lookup"><span data-stu-id="09bb1-220">An escaped JSON blob which describes the services and regions that are impacted by the incident.</span></span> <span data-ttu-id="09bb1-221">Services 清單 (每一份都有 ServiceName) 和 ImpactedRegions 清單 (每一份都有 RegionName)。</span><span class="sxs-lookup"><span data-stu-id="09bb1-221">A list of Services, each of which has a ServiceName and a list of ImpactedRegions, each of which has a RegionName.</span></span>
<span data-ttu-id="09bb1-222">Properties.defaultLanguageTitle</span><span class="sxs-lookup"><span data-stu-id="09bb1-222">Properties.defaultLanguageTitle</span></span> | <span data-ttu-id="09bb1-223">英文的通訊</span><span class="sxs-lookup"><span data-stu-id="09bb1-223">The communication in English</span></span>
<span data-ttu-id="09bb1-224">Properties.defaultLanguageContent</span><span class="sxs-lookup"><span data-stu-id="09bb1-224">Properties.defaultLanguageContent</span></span> | <span data-ttu-id="09bb1-225">英文的通訊，如 html 標記或純文字</span><span class="sxs-lookup"><span data-stu-id="09bb1-225">The communication in English as either html markup or plain text</span></span>
<span data-ttu-id="09bb1-226">Properties.stage</span><span class="sxs-lookup"><span data-stu-id="09bb1-226">Properties.stage</span></span> | <span data-ttu-id="09bb1-227">AssistedRecovery、ActionRequired、Information、Incident、Security 的可能值：Active、Resolved。</span><span class="sxs-lookup"><span data-stu-id="09bb1-227">Possible values for AssistedRecovery, ActionRequired, Information, Incident, Security: are Active, Resolved.</span></span> <span data-ttu-id="09bb1-228">Maintenance 的可能值︰Active、Planned、InProgress、Canceled、Rescheduled、Resolved、Complete</span><span class="sxs-lookup"><span data-stu-id="09bb1-228">For Maintenance they are: Active, Planned, InProgress, Canceled, Rescheduled, Resolved, Complete</span></span>
<span data-ttu-id="09bb1-229">Properties.communicationId</span><span class="sxs-lookup"><span data-stu-id="09bb1-229">Properties.communicationId</span></span> | <span data-ttu-id="09bb1-230">與此事件相關聯的通訊。</span><span class="sxs-lookup"><span data-stu-id="09bb1-230">The communication this event is associated.</span></span>

## <a name="alert"></a><span data-ttu-id="09bb1-231">警示</span><span class="sxs-lookup"><span data-stu-id="09bb1-231">Alert</span></span>
<span data-ttu-id="09bb1-232">此類別包含所有 Azure 警示的啟用記錄。</span><span class="sxs-lookup"><span data-stu-id="09bb1-232">This category contains the record of all activations of Azure alerts.</span></span> <span data-ttu-id="09bb1-233">您可能會在此類別中看到的事件類型範例為「myVM 上的 CPU 百分比在過去 5 分鐘內已超過 80」。</span><span class="sxs-lookup"><span data-stu-id="09bb1-233">An example of the type of event you would see in this category is "CPU % on myVM has been over 80 for the past 5 minutes."</span></span> <span data-ttu-id="09bb1-234">各種 Azure 系統都有警示概念，您可以定義某種類型的規則，並在條件符合該規則時接收通知。</span><span class="sxs-lookup"><span data-stu-id="09bb1-234">A variety of Azure systems have an alerting concept -- you can define a rule of some sort and receive a notification when conditions match that rule.</span></span> <span data-ttu-id="09bb1-235">每次支援的 Azure 警示類型「啟動」時，或產生通知的條件符合時，該啟用記錄會也會推送至此類別的活動記錄。</span><span class="sxs-lookup"><span data-stu-id="09bb1-235">Each time a supported Azure alert type 'activates,' or the conditions are met to generate a notification, a record of the activation is also pushed to this category of the Activity Log.</span></span>

### <a name="sample-event"></a><span data-ttu-id="09bb1-236">範例事件</span><span class="sxs-lookup"><span data-stu-id="09bb1-236">Sample event</span></span>

```json
{
  "caller": "Microsoft.Insights/alertRules",
  "channels": "Admin, Operation",
  "claims": {
    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/spn": "Microsoft.Insights/alertRules"
  },
  "correlationId": "/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/microsoft.insights/alertrules/myalert/incidents/L3N1YnNjcmlwdGlvbnMvZGY2MDJjOWMtN2FhMC00MDdkLWE2ZmItZWIyMGM4YmQxMTkyL3Jlc291cmNlR3JvdXBzL0NzbUV2ZW50RE9HRk9PRC1XZXN0VVMvcHJvdmlkZXJzL21pY3Jvc29mdC5pbnNpZ2h0cy9hbGVydHJ1bGVzL215YWxlcnQwNjM2MzYyMjU4NTM1MjIxOTIw",
  "description": "'Disk read LessThan 100000 ([Count]) in the last 5 minutes' has been resolved for CloudService: myResourceGroup/Production/Event.BackgroundJobsWorker.razzle (myResourceGroup)",
  "eventDataId": "149d4baf-53dc-4cf4-9e29-17de37405cd9",
  "eventName": {
    "value": "Alert",
    "localizedValue": "Alert"
  },
  "category": {
    "value": "Alert",
    "localizedValue": "Alert"
  },
  "id": "/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/Microsoft.ClassicCompute/domainNames/myResourceGroup/slots/Production/roles/Event.BackgroundJobsWorker.razzle/events/149d4baf-53dc-4cf4-9e29-17de37405cd9/ticks/636362258535221920",
  "level": "Informational",
  "resourceGroupName": "myResourceGroup",
  "resourceProviderName": {
    "value": "Microsoft.ClassicCompute",
    "localizedValue": "Microsoft.ClassicCompute"
  },
  "resourceId": "/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/Microsoft.ClassicCompute/domainNames/myResourceGroup/slots/Production/roles/Event.BackgroundJobsWorker.razzle",
  "resourceType": {
    "value": "Microsoft.ClassicCompute/domainNames/slots/roles",
    "localizedValue": "Microsoft.ClassicCompute/domainNames/slots/roles"
  },
  "operationId": "/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/microsoft.insights/alertrules/myalert/incidents/L3N1YnNjcmlwdGlvbnMvZGY2MDJjOWMtN2FhMC00MDdkLWE2ZmItZWIyMGM4YmQxMTkyL3Jlc291cmNlR3JvdXBzL0NzbUV2ZW50RE9HRk9PRC1XZXN0VVMvcHJvdmlkZXJzL21pY3Jvc29mdC5pbnNpZ2h0cy9hbGVydHJ1bGVzL215YWxlcnQwNjM2MzYyMjU4NTM1MjIxOTIw",
  "operationName": {
    "value": "Microsoft.Insights/AlertRules/Resolved/Action",
    "localizedValue": "Microsoft.Insights/AlertRules/Resolved/Action"
  },
  "properties": {
    "RuleUri": "/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/microsoft.insights/alertrules/myalert",
    "RuleName": "myalert",
    "RuleDescription": "",
    "Threshold": "100000",
    "WindowSizeInMinutes": "5",
    "Aggregation": "Average",
    "Operator": "LessThan",
    "MetricName": "Disk read",
    "MetricUnit": "Count"
  },
  "status": {
    "value": "Resolved",
    "localizedValue": "Resolved"
  },
  "subStatus": {
    "value": null
  },
  "eventTimestamp": "2017-07-21T09:24:13.522192Z",
  "submissionTimestamp": "2017-07-21T09:24:15.6578651Z",
  "subscriptionId": "mySubscriptionID"
}
```

### <a name="property-descriptions"></a><span data-ttu-id="09bb1-237">屬性描述</span><span class="sxs-lookup"><span data-stu-id="09bb1-237">Property descriptions</span></span>
| <span data-ttu-id="09bb1-238">元素名稱</span><span class="sxs-lookup"><span data-stu-id="09bb1-238">Element Name</span></span> | <span data-ttu-id="09bb1-239">說明</span><span class="sxs-lookup"><span data-stu-id="09bb1-239">Description</span></span> |
| --- | --- |
| <span data-ttu-id="09bb1-240">呼叫者</span><span class="sxs-lookup"><span data-stu-id="09bb1-240">caller</span></span> | <span data-ttu-id="09bb1-241">一律是 Microsoft.Insights/alertRules</span><span class="sxs-lookup"><span data-stu-id="09bb1-241">Always Microsoft.Insights/alertRules</span></span> |
| <span data-ttu-id="09bb1-242">通道</span><span class="sxs-lookup"><span data-stu-id="09bb1-242">channels</span></span> | <span data-ttu-id="09bb1-243">一律是 “Admin, Operation”</span><span class="sxs-lookup"><span data-stu-id="09bb1-243">Always “Admin, Operation”</span></span> |
| <span data-ttu-id="09bb1-244">claims</span><span class="sxs-lookup"><span data-stu-id="09bb1-244">claims</span></span> | <span data-ttu-id="09bb1-245">具有警示引擎的 SPN (服務主體名稱) 或資源類型的 JSON Blob。</span><span class="sxs-lookup"><span data-stu-id="09bb1-245">JSON blob with the SPN (service principal name), or resource type, of the alert engine.</span></span> |
| <span data-ttu-id="09bb1-246">correlationId</span><span class="sxs-lookup"><span data-stu-id="09bb1-246">correlationId</span></span> | <span data-ttu-id="09bb1-247">字串格式的 GUID。</span><span class="sxs-lookup"><span data-stu-id="09bb1-247">A GUID in the string format.</span></span> |
| <span data-ttu-id="09bb1-248">說明</span><span class="sxs-lookup"><span data-stu-id="09bb1-248">description</span></span> |<span data-ttu-id="09bb1-249">警示事件的靜態文字描述。</span><span class="sxs-lookup"><span data-stu-id="09bb1-249">Static text description of the alert event.</span></span> |
| <span data-ttu-id="09bb1-250">eventDataId</span><span class="sxs-lookup"><span data-stu-id="09bb1-250">eventDataId</span></span> |<span data-ttu-id="09bb1-251">警示事件的唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="09bb1-251">Unique identifier of the alert event.</span></span> |
| <span data-ttu-id="09bb1-252">層級</span><span class="sxs-lookup"><span data-stu-id="09bb1-252">level</span></span> |<span data-ttu-id="09bb1-253">事件的層級。</span><span class="sxs-lookup"><span data-stu-id="09bb1-253">Level of the event.</span></span> <span data-ttu-id="09bb1-254">下列其中一個值：重大、錯誤、警告、資訊和詳細資訊</span><span class="sxs-lookup"><span data-stu-id="09bb1-254">One of the following values: “Critical”, “Error”, “Warning”, “Informational” and “Verbose”</span></span> |
| <span data-ttu-id="09bb1-255">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="09bb1-255">resourceGroupName</span></span> |<span data-ttu-id="09bb1-256">如果為計量警示，這是受影響資源的資源群組名稱。</span><span class="sxs-lookup"><span data-stu-id="09bb1-256">Name of the resource group for the impacted resource if it is a metric alert.</span></span> <span data-ttu-id="09bb1-257">針對其他警示類型，這是包含警示本身的資源群組名稱。</span><span class="sxs-lookup"><span data-stu-id="09bb1-257">For other alert types, this is the name of the resource group that contains the alert itself.</span></span> |
| <span data-ttu-id="09bb1-258">resourceProviderName</span><span class="sxs-lookup"><span data-stu-id="09bb1-258">resourceProviderName</span></span> |<span data-ttu-id="09bb1-259">如果為計量警示，這是受影響資源的資源提供者名稱。</span><span class="sxs-lookup"><span data-stu-id="09bb1-259">Name of the resource provider for the impacted resource if it is a metric alert.</span></span> <span data-ttu-id="09bb1-260">針對其他警示類型，這是警示本身的資源提供者名稱。</span><span class="sxs-lookup"><span data-stu-id="09bb1-260">For other alert types, this is the name of the resource provider for the alert itself.</span></span> |
| <span data-ttu-id="09bb1-261">resourceId</span><span class="sxs-lookup"><span data-stu-id="09bb1-261">resourceId</span></span> | <span data-ttu-id="09bb1-262">如果為計量警示，這是受影響資源的資源識別碼名稱。</span><span class="sxs-lookup"><span data-stu-id="09bb1-262">Name of the resource ID for the impacted resource if it is a metric alert.</span></span> <span data-ttu-id="09bb1-263">針對其他警示類型，這是警示資源本身的資源識別碼。</span><span class="sxs-lookup"><span data-stu-id="09bb1-263">For other alert types, this is the resource ID of the alert resource itself.</span></span> |
| <span data-ttu-id="09bb1-264">operationId</span><span class="sxs-lookup"><span data-stu-id="09bb1-264">operationId</span></span> |<span data-ttu-id="09bb1-265">對應至單一作業的事件共用的 GUID。</span><span class="sxs-lookup"><span data-stu-id="09bb1-265">A GUID shared among the events that correspond to a single operation.</span></span> |
| <span data-ttu-id="09bb1-266">operationName</span><span class="sxs-lookup"><span data-stu-id="09bb1-266">operationName</span></span> |<span data-ttu-id="09bb1-267">作業名稱。</span><span class="sxs-lookup"><span data-stu-id="09bb1-267">Name of the operation.</span></span> |
| <span data-ttu-id="09bb1-268">properties</span><span class="sxs-lookup"><span data-stu-id="09bb1-268">properties</span></span> |<span data-ttu-id="09bb1-269">描述事件詳細資料的一組 `<Key, Value>` 配對 (也就是字典)。</span><span class="sxs-lookup"><span data-stu-id="09bb1-269">Set of `<Key, Value>` pairs (that is, a Dictionary) describing the details of the event.</span></span> |
| <span data-ttu-id="09bb1-270">status</span><span class="sxs-lookup"><span data-stu-id="09bb1-270">status</span></span> |<span data-ttu-id="09bb1-271">字串，描述作業的狀態。</span><span class="sxs-lookup"><span data-stu-id="09bb1-271">String describing the status of the operation.</span></span> <span data-ttu-id="09bb1-272">常見的值包括︰Started、In Progress、Succeeded、Failed、Active、Resolved。</span><span class="sxs-lookup"><span data-stu-id="09bb1-272">Some common values are: Started, In Progress, Succeeded, Failed, Active, Resolved.</span></span> |
| <span data-ttu-id="09bb1-273">子狀態</span><span class="sxs-lookup"><span data-stu-id="09bb1-273">subStatus</span></span> | <span data-ttu-id="09bb1-274">針對警示通常為 null。</span><span class="sxs-lookup"><span data-stu-id="09bb1-274">Usually null for alerts.</span></span> |
| <span data-ttu-id="09bb1-275">eventTimestamp</span><span class="sxs-lookup"><span data-stu-id="09bb1-275">eventTimestamp</span></span> |<span data-ttu-id="09bb1-276">處理與事件對應之要求的Azure 服務產生事件時的時間戳記。</span><span class="sxs-lookup"><span data-stu-id="09bb1-276">Timestamp when the event was generated by the Azure service processing the request corresponding the event.</span></span> |
| <span data-ttu-id="09bb1-277">submissionTimestamp</span><span class="sxs-lookup"><span data-stu-id="09bb1-277">submissionTimestamp</span></span> |<span data-ttu-id="09bb1-278">當事件變成可供查詢時的時間戳記。</span><span class="sxs-lookup"><span data-stu-id="09bb1-278">Timestamp when the event became available for querying.</span></span> |
| <span data-ttu-id="09bb1-279">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="09bb1-279">subscriptionId</span></span> |<span data-ttu-id="09bb1-280">Azure 訂用帳戶識別碼。</span><span class="sxs-lookup"><span data-stu-id="09bb1-280">Azure Subscription Id.</span></span> |

### <a name="properties-field-per-alert-type"></a><span data-ttu-id="09bb1-281">每個警示類型的屬性欄位</span><span class="sxs-lookup"><span data-stu-id="09bb1-281">Properties field per alert type</span></span>
<span data-ttu-id="09bb1-282">屬性欄位將依據警示事件來源包含不同的值。</span><span class="sxs-lookup"><span data-stu-id="09bb1-282">The properties field will contain different values depending on the source of the alert event.</span></span> <span data-ttu-id="09bb1-283">兩個常見的警示事件提供者為活動記錄警示和計量警示。</span><span class="sxs-lookup"><span data-stu-id="09bb1-283">Two common alert event providers are Activity Log alerts and metric alerts.</span></span>

#### <a name="properties-for-activity-log-alerts"></a><span data-ttu-id="09bb1-284">活動記錄警示的屬性</span><span class="sxs-lookup"><span data-stu-id="09bb1-284">Properties for Activity Log alerts</span></span>
| <span data-ttu-id="09bb1-285">元素名稱</span><span class="sxs-lookup"><span data-stu-id="09bb1-285">Element Name</span></span> | <span data-ttu-id="09bb1-286">說明</span><span class="sxs-lookup"><span data-stu-id="09bb1-286">Description</span></span> |
| --- | --- |
| <span data-ttu-id="09bb1-287">properties.subscriptionId</span><span class="sxs-lookup"><span data-stu-id="09bb1-287">properties.subscriptionId</span></span> | <span data-ttu-id="09bb1-288">導致啟用此活動記錄警示規則之活動記錄事件的訂用帳戶識別碼。</span><span class="sxs-lookup"><span data-stu-id="09bb1-288">The subscription ID from the activity log event which caused this activity log alert rule to be activated.</span></span> |
| <span data-ttu-id="09bb1-289">properties.eventDataId</span><span class="sxs-lookup"><span data-stu-id="09bb1-289">properties.eventDataId</span></span> | <span data-ttu-id="09bb1-290">導致啟用此活動記錄警示規則之活動記錄事件的事件資料識別碼。</span><span class="sxs-lookup"><span data-stu-id="09bb1-290">The event data ID from the activity log event which caused this activity log alert rule to be activated.</span></span> |
| <span data-ttu-id="09bb1-291">properties.resourceGroup</span><span class="sxs-lookup"><span data-stu-id="09bb1-291">properties.resourceGroup</span></span> | <span data-ttu-id="09bb1-292">導致啟用此活動記錄警示規則之活動記錄事件的資源群組。</span><span class="sxs-lookup"><span data-stu-id="09bb1-292">The resource group from the activity log event which caused this activity log alert rule to be activated.</span></span> |
| <span data-ttu-id="09bb1-293">properties.resourceId</span><span class="sxs-lookup"><span data-stu-id="09bb1-293">properties.resourceId</span></span> | <span data-ttu-id="09bb1-294">導致啟用此活動記錄警示規則之活動記錄事件的資源識別碼。</span><span class="sxs-lookup"><span data-stu-id="09bb1-294">The resource ID from the activity log event which caused this activity log alert rule to be activated.</span></span> |
| <span data-ttu-id="09bb1-295">properties.eventTimestamp</span><span class="sxs-lookup"><span data-stu-id="09bb1-295">properties.eventTimestamp</span></span> | <span data-ttu-id="09bb1-296">導致啟用此活動記錄警示規則之活動記錄事件的事件時間戳記。</span><span class="sxs-lookup"><span data-stu-id="09bb1-296">The event timestamp of the activity log event which caused this activity log alert rule to be activated.</span></span> |
| <span data-ttu-id="09bb1-297">properties.operationName</span><span class="sxs-lookup"><span data-stu-id="09bb1-297">properties.operationName</span></span> | <span data-ttu-id="09bb1-298">導致啟用此活動記錄警示規則之活動記錄事件的作業名稱。</span><span class="sxs-lookup"><span data-stu-id="09bb1-298">The operation name from the activity log event which caused this activity log alert rule to be activated.</span></span> |
| <span data-ttu-id="09bb1-299">properties.status</span><span class="sxs-lookup"><span data-stu-id="09bb1-299">properties.status</span></span> | <span data-ttu-id="09bb1-300">導致啟用此活動記錄警示規則之活動記錄事件的狀態。</span><span class="sxs-lookup"><span data-stu-id="09bb1-300">The status from the activity log event which caused this activity log alert rule to be activated.</span></span>|

#### <a name="properties-for-metric-alerts"></a><span data-ttu-id="09bb1-301">計量警示屬性</span><span class="sxs-lookup"><span data-stu-id="09bb1-301">Properties for metric alerts</span></span>
| <span data-ttu-id="09bb1-302">元素名稱</span><span class="sxs-lookup"><span data-stu-id="09bb1-302">Element Name</span></span> | <span data-ttu-id="09bb1-303">說明</span><span class="sxs-lookup"><span data-stu-id="09bb1-303">Description</span></span> |
| --- | --- |
| <span data-ttu-id="09bb1-304">properties.RuleUri</span><span class="sxs-lookup"><span data-stu-id="09bb1-304">properties.RuleUri</span></span> | <span data-ttu-id="09bb1-305">計量警示規則本身的資源識別碼。</span><span class="sxs-lookup"><span data-stu-id="09bb1-305">Resource ID of the metric alert rule itself.</span></span> |
| <span data-ttu-id="09bb1-306">properties.RuleName</span><span class="sxs-lookup"><span data-stu-id="09bb1-306">properties.RuleName</span></span> | <span data-ttu-id="09bb1-307">計量警示規則的名稱。</span><span class="sxs-lookup"><span data-stu-id="09bb1-307">The name of the metric alert rule.</span></span> |
| <span data-ttu-id="09bb1-308">properties.RuleDescription</span><span class="sxs-lookup"><span data-stu-id="09bb1-308">properties.RuleDescription</span></span> | <span data-ttu-id="09bb1-309">計量警示規則的描述 (如警示規則中所定義)。</span><span class="sxs-lookup"><span data-stu-id="09bb1-309">The description of the metric alert rule (as defined in the alert rule).</span></span> |
| <span data-ttu-id="09bb1-310">properties.Threshold</span><span class="sxs-lookup"><span data-stu-id="09bb1-310">properties.Threshold</span></span> | <span data-ttu-id="09bb1-311">用於評估計量警示規則的臨界值。</span><span class="sxs-lookup"><span data-stu-id="09bb1-311">The threshold value used in the evaluation of the metric alert rule.</span></span> |
| <span data-ttu-id="09bb1-312">properties.WindowSizeInMinutes</span><span class="sxs-lookup"><span data-stu-id="09bb1-312">properties.WindowSizeInMinutes</span></span> | <span data-ttu-id="09bb1-313">用於評估計量警示規則的視窗大小。</span><span class="sxs-lookup"><span data-stu-id="09bb1-313">The window size used in the evaluation of the metric alert rule.</span></span> |
| <span data-ttu-id="09bb1-314">properties.Aggregation</span><span class="sxs-lookup"><span data-stu-id="09bb1-314">properties.Aggregation</span></span> | <span data-ttu-id="09bb1-315">定義於計量警示規則中的彙總類型。</span><span class="sxs-lookup"><span data-stu-id="09bb1-315">The aggregation type defined in the metric alert rule.</span></span> |
| <span data-ttu-id="09bb1-316">properties.Operator</span><span class="sxs-lookup"><span data-stu-id="09bb1-316">properties.Operator</span></span> | <span data-ttu-id="09bb1-317">用於評估計量警示規則的條件運算子。</span><span class="sxs-lookup"><span data-stu-id="09bb1-317">The conditional operator used in the evaluation of the metric alert rule.</span></span> |
| <span data-ttu-id="09bb1-318">properties.MetricName</span><span class="sxs-lookup"><span data-stu-id="09bb1-318">properties.MetricName</span></span> | <span data-ttu-id="09bb1-319">用於評估計量警示規則之計量的計量名稱。</span><span class="sxs-lookup"><span data-stu-id="09bb1-319">The metric name of the metric used in the evaluation of the metric alert rule.</span></span> |
| <span data-ttu-id="09bb1-320">properties.MetricUnit</span><span class="sxs-lookup"><span data-stu-id="09bb1-320">properties.MetricUnit</span></span> | <span data-ttu-id="09bb1-321">用於評估計量警示規則之計量的計量單位。</span><span class="sxs-lookup"><span data-stu-id="09bb1-321">The metric unit for the metric used in the evaluation of the metric alert rule.</span></span> |

## <a name="autoscale"></a><span data-ttu-id="09bb1-322">Autoscale</span><span class="sxs-lookup"><span data-stu-id="09bb1-322">Autoscale</span></span>
<span data-ttu-id="09bb1-323">所有與自動調整引擎 (以訂用帳戶中定義的自動調整設定為基礎) 作業相關的所有事件皆記錄在此類別。</span><span class="sxs-lookup"><span data-stu-id="09bb1-323">This category contains the record of any events related to the operation of the autoscale engine based on any autoscale settings you have defined in your subscription.</span></span> <span data-ttu-id="09bb1-324">您可能會在此類別中看到的事件類型範例為「自動調整相應增加動作失敗」。</span><span class="sxs-lookup"><span data-stu-id="09bb1-324">An example of the type of event you would see in this category is "Autoscale scale up action failed."</span></span> <span data-ttu-id="09bb1-325">自動調整可讓您使用自動調整設定，依據每日時間和/或負載 (計量) 資料，自動相應放大或縮小受支援資源類型中的執行個體數目。</span><span class="sxs-lookup"><span data-stu-id="09bb1-325">Using autoscale, you can automatically scale out or scale in the number of instances in a supported resource type based on time of day and/or load (metric) data using an autoscale setting.</span></span> <span data-ttu-id="09bb1-326">符合相應增加或相應減少的條件時，啟動及成功或失敗事件將會記錄在此類別中。</span><span class="sxs-lookup"><span data-stu-id="09bb1-326">When the conditions are met to scale up or down, the start and succeeded or failed events will be recorded in this category.</span></span>

### <a name="sample-event"></a><span data-ttu-id="09bb1-327">範例事件</span><span class="sxs-lookup"><span data-stu-id="09bb1-327">Sample event</span></span>
```json
{
  "caller": "Microsoft.Insights/autoscaleSettings",
  "channels": "Admin, Operation",
  "claims": {
    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/spn": "Microsoft.Insights/autoscaleSettings"
  },
  "correlationId": "fc6a7ff5-ff68-4bb7-81b4-3629212d03d0",
  "description": "The autoscale engine attempting to scale resource '/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/Microsoft.ClassicCompute/domainNames/myResourceGroup/slots/Production/roles/myResource' from 3 instances count to 2 instances count.",
  "eventDataId": "a5b92075-1de9-42f1-b52e-6f3e4945a7c7",
  "eventName": {
    "value": "AutoscaleAction",
    "localizedValue": "AutoscaleAction"
  },
  "category": {
    "value": "Autoscale",
    "localizedValue": "Autoscale"
  },
  "id": "/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/microsoft.insights/autoscalesettings/myResourceGroup-Production-myResource-myResourceGroup/events/a5b92075-1de9-42f1-b52e-6f3e4945a7c7/ticks/636361956518681572",
  "level": "Informational",
  "resourceGroupName": "myResourceGroup",
  "resourceProviderName": {
    "value": "microsoft.insights",
    "localizedValue": "microsoft.insights"
  },
  "resourceId": "/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/microsoft.insights/autoscalesettings/myResourceGroup-Production-myResource-myResourceGroup",
  "resourceType": {
    "value": "microsoft.insights/autoscalesettings",
    "localizedValue": "microsoft.insights/autoscalesettings"
  },
  "operationId": "fc6a7ff5-ff68-4bb7-81b4-3629212d03d0",
  "operationName": {
    "value": "Microsoft.Insights/AutoscaleSettings/Scaledown/Action",
    "localizedValue": "Microsoft.Insights/AutoscaleSettings/Scaledown/Action"
  },
  "properties": {
    "Description": "The autoscale engine attempting to scale resource '/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/Microsoft.ClassicCompute/domainNames/myResourceGroup/slots/Production/roles/myResource' from 3 instances count to 2 instances count.",
    "ResourceName": "/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/Microsoft.ClassicCompute/domainNames/myResourceGroup/slots/Production/roles/myResource",
    "OldInstancesCount": "3",
    "NewInstancesCount": "2",
    "LastScaleActionTime": "Fri, 21 Jul 2017 01:00:51 GMT"
  },
  "status": {
    "value": "Succeeded",
    "localizedValue": "Succeeded"
  },
  "subStatus": {
    "value": null
  },
  "eventTimestamp": "2017-07-21T01:00:51.8681572Z",
  "submissionTimestamp": "2017-07-21T01:00:52.3008754Z",
  "subscriptionId": "mySubscriptionID"
}

```

### <a name="property-descriptions"></a><span data-ttu-id="09bb1-328">屬性描述</span><span class="sxs-lookup"><span data-stu-id="09bb1-328">Property descriptions</span></span>
| <span data-ttu-id="09bb1-329">元素名稱</span><span class="sxs-lookup"><span data-stu-id="09bb1-329">Element Name</span></span> | <span data-ttu-id="09bb1-330">說明</span><span class="sxs-lookup"><span data-stu-id="09bb1-330">Description</span></span> |
| --- | --- |
| <span data-ttu-id="09bb1-331">呼叫者</span><span class="sxs-lookup"><span data-stu-id="09bb1-331">caller</span></span> | <span data-ttu-id="09bb1-332">一律是 Microsoft.Insights/autoscaleSettings</span><span class="sxs-lookup"><span data-stu-id="09bb1-332">Always Microsoft.Insights/autoscaleSettings</span></span> |
| <span data-ttu-id="09bb1-333">通道</span><span class="sxs-lookup"><span data-stu-id="09bb1-333">channels</span></span> | <span data-ttu-id="09bb1-334">一律是 “Admin, Operation”</span><span class="sxs-lookup"><span data-stu-id="09bb1-334">Always “Admin, Operation”</span></span> |
| <span data-ttu-id="09bb1-335">claims</span><span class="sxs-lookup"><span data-stu-id="09bb1-335">claims</span></span> | <span data-ttu-id="09bb1-336">具有自動調整引擎的 SPN (服務主體名稱) 或資源類型的 JSON Blob。</span><span class="sxs-lookup"><span data-stu-id="09bb1-336">JSON blob with the SPN (service principal name), or resource type, of the autoscale engine.</span></span> |
| <span data-ttu-id="09bb1-337">correlationId</span><span class="sxs-lookup"><span data-stu-id="09bb1-337">correlationId</span></span> | <span data-ttu-id="09bb1-338">字串格式的 GUID。</span><span class="sxs-lookup"><span data-stu-id="09bb1-338">A GUID in the string format.</span></span> |
| <span data-ttu-id="09bb1-339">說明</span><span class="sxs-lookup"><span data-stu-id="09bb1-339">description</span></span> |<span data-ttu-id="09bb1-340">自動調整事件的靜態文字描述。</span><span class="sxs-lookup"><span data-stu-id="09bb1-340">Static text description of the autoscale event.</span></span> |
| <span data-ttu-id="09bb1-341">eventDataId</span><span class="sxs-lookup"><span data-stu-id="09bb1-341">eventDataId</span></span> |<span data-ttu-id="09bb1-342">自動調整事件的唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="09bb1-342">Unique identifier of the autoscale event.</span></span> |
| <span data-ttu-id="09bb1-343">層級</span><span class="sxs-lookup"><span data-stu-id="09bb1-343">level</span></span> |<span data-ttu-id="09bb1-344">事件的層級。</span><span class="sxs-lookup"><span data-stu-id="09bb1-344">Level of the event.</span></span> <span data-ttu-id="09bb1-345">下列其中一個值：重大、錯誤、警告、資訊和詳細資訊</span><span class="sxs-lookup"><span data-stu-id="09bb1-345">One of the following values: “Critical”, “Error”, “Warning”, “Informational” and “Verbose”</span></span> |
| <span data-ttu-id="09bb1-346">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="09bb1-346">resourceGroupName</span></span> |<span data-ttu-id="09bb1-347">自動調整設定的資源群組名稱。</span><span class="sxs-lookup"><span data-stu-id="09bb1-347">Name of the resource group for the autoscale setting.</span></span> |
| <span data-ttu-id="09bb1-348">resourceProviderName</span><span class="sxs-lookup"><span data-stu-id="09bb1-348">resourceProviderName</span></span> |<span data-ttu-id="09bb1-349">自動調整設定的資源提供者名稱。</span><span class="sxs-lookup"><span data-stu-id="09bb1-349">Name of the resource provider for the autoscale setting.</span></span> |
| <span data-ttu-id="09bb1-350">resourceId</span><span class="sxs-lookup"><span data-stu-id="09bb1-350">resourceId</span></span> |<span data-ttu-id="09bb1-351">自動調整設定的資源識別碼。</span><span class="sxs-lookup"><span data-stu-id="09bb1-351">Resource id of the autoscale setting.</span></span> |
| <span data-ttu-id="09bb1-352">operationId</span><span class="sxs-lookup"><span data-stu-id="09bb1-352">operationId</span></span> |<span data-ttu-id="09bb1-353">對應至單一作業的事件共用的 GUID。</span><span class="sxs-lookup"><span data-stu-id="09bb1-353">A GUID shared among the events that correspond to a single operation.</span></span> |
| <span data-ttu-id="09bb1-354">operationName</span><span class="sxs-lookup"><span data-stu-id="09bb1-354">operationName</span></span> |<span data-ttu-id="09bb1-355">作業名稱。</span><span class="sxs-lookup"><span data-stu-id="09bb1-355">Name of the operation.</span></span> |
| <span data-ttu-id="09bb1-356">properties</span><span class="sxs-lookup"><span data-stu-id="09bb1-356">properties</span></span> |<span data-ttu-id="09bb1-357">描述事件詳細資料的一組 `<Key, Value>` 配對 (也就是字典)。</span><span class="sxs-lookup"><span data-stu-id="09bb1-357">Set of `<Key, Value>` pairs (that is, a Dictionary) describing the details of the event.</span></span> |
| <span data-ttu-id="09bb1-358">properties.Description</span><span class="sxs-lookup"><span data-stu-id="09bb1-358">properties.Description</span></span> | <span data-ttu-id="09bb1-359">自動調整引擎所執行之作業的詳細描述。</span><span class="sxs-lookup"><span data-stu-id="09bb1-359">Detailed description of what the autoscale engine was doing.</span></span> |
| <span data-ttu-id="09bb1-360">properties.ResourceName</span><span class="sxs-lookup"><span data-stu-id="09bb1-360">properties.ResourceName</span></span> | <span data-ttu-id="09bb1-361">受影響資源 (執行調整動作的資源) 的資源識別碼</span><span class="sxs-lookup"><span data-stu-id="09bb1-361">Resource ID of the impacted resource (the resource on which the scale action was being performed)</span></span> |
| <span data-ttu-id="09bb1-362">properties.OldInstancesCount</span><span class="sxs-lookup"><span data-stu-id="09bb1-362">properties.OldInstancesCount</span></span> | <span data-ttu-id="09bb1-363">自動調整動作生效之前的執行個體數目。</span><span class="sxs-lookup"><span data-stu-id="09bb1-363">The number of instances before the autoscale action took effect.</span></span> |
| <span data-ttu-id="09bb1-364">properties.NewInstancesCount</span><span class="sxs-lookup"><span data-stu-id="09bb1-364">properties.NewInstancesCount</span></span> | <span data-ttu-id="09bb1-365">自動調整動作生效之後的執行個體數目。</span><span class="sxs-lookup"><span data-stu-id="09bb1-365">The number of instances after the autoscale action took effect.</span></span> |
| <span data-ttu-id="09bb1-366">properties.LastScaleActionTime</span><span class="sxs-lookup"><span data-stu-id="09bb1-366">properties.LastScaleActionTime</span></span> | <span data-ttu-id="09bb1-367">自動調整動作發生時的時間戳記。</span><span class="sxs-lookup"><span data-stu-id="09bb1-367">The timestamp of when the autoscale action occurred.</span></span> |
| <span data-ttu-id="09bb1-368">status</span><span class="sxs-lookup"><span data-stu-id="09bb1-368">status</span></span> |<span data-ttu-id="09bb1-369">字串，描述作業的狀態。</span><span class="sxs-lookup"><span data-stu-id="09bb1-369">String describing the status of the operation.</span></span> <span data-ttu-id="09bb1-370">常見的值包括︰Started、In Progress、Succeeded、Failed、Active、Resolved。</span><span class="sxs-lookup"><span data-stu-id="09bb1-370">Some common values are: Started, In Progress, Succeeded, Failed, Active, Resolved.</span></span> |
| <span data-ttu-id="09bb1-371">子狀態</span><span class="sxs-lookup"><span data-stu-id="09bb1-371">subStatus</span></span> | <span data-ttu-id="09bb1-372">針對自動調整通常為 null。</span><span class="sxs-lookup"><span data-stu-id="09bb1-372">Usually null for autoscale.</span></span> |
| <span data-ttu-id="09bb1-373">eventTimestamp</span><span class="sxs-lookup"><span data-stu-id="09bb1-373">eventTimestamp</span></span> |<span data-ttu-id="09bb1-374">處理與事件對應之要求的Azure 服務產生事件時的時間戳記。</span><span class="sxs-lookup"><span data-stu-id="09bb1-374">Timestamp when the event was generated by the Azure service processing the request corresponding the event.</span></span> |
| <span data-ttu-id="09bb1-375">submissionTimestamp</span><span class="sxs-lookup"><span data-stu-id="09bb1-375">submissionTimestamp</span></span> |<span data-ttu-id="09bb1-376">當事件變成可供查詢時的時間戳記。</span><span class="sxs-lookup"><span data-stu-id="09bb1-376">Timestamp when the event became available for querying.</span></span> |
| <span data-ttu-id="09bb1-377">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="09bb1-377">subscriptionId</span></span> |<span data-ttu-id="09bb1-378">Azure 訂用帳戶識別碼。</span><span class="sxs-lookup"><span data-stu-id="09bb1-378">Azure Subscription Id.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="09bb1-379">後續步驟</span><span class="sxs-lookup"><span data-stu-id="09bb1-379">Next steps</span></span>
* [<span data-ttu-id="09bb1-380">深入了解活動記錄檔 (之前的稽核記錄檔)</span><span class="sxs-lookup"><span data-stu-id="09bb1-380">Learn more about the Activity Log (formerly Audit Logs)</span></span>](monitoring-overview-activity-logs.md)
* [<span data-ttu-id="09bb1-381">將 Azure 活動記錄檔串流至事件中樞</span><span class="sxs-lookup"><span data-stu-id="09bb1-381">Stream the Azure Activity Log to Event Hubs</span></span>](monitoring-stream-activity-logs-event-hubs.md)
