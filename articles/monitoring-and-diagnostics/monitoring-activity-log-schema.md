---
title: "aaaAzure 活動記錄檔事件結構描述 |Microsoft 文件"
description: "了解 hello 事件結構描述的資料發出到 hello 活動記錄檔"
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
ms.openlocfilehash: dfece949a20a4d9b4e8a4d488c1c34842d87d586
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-activity-log-event-schema"></a><span data-ttu-id="02f7c-103">Azure 活動記錄事件結構描述</span><span class="sxs-lookup"><span data-stu-id="02f7c-103">Azure Activity Log event schema</span></span>
<span data-ttu-id="02f7c-104">hello **Azure 活動記錄檔**是提供深入了解 Azure 中所發生的任何訂用帳戶層級事件的記錄。</span><span class="sxs-lookup"><span data-stu-id="02f7c-104">hello **Azure Activity Log** is a log that provides insight into any subscription-level events that have occurred in Azure.</span></span> <span data-ttu-id="02f7c-105">本文說明 hello 事件結構描述，每個分類的資料。</span><span class="sxs-lookup"><span data-stu-id="02f7c-105">This article describes hello event schema per category of data.</span></span>

## <a name="administrative"></a><span data-ttu-id="02f7c-106">管理</span><span class="sxs-lookup"><span data-stu-id="02f7c-106">Administrative</span></span>
<span data-ttu-id="02f7c-107">這個類別所包含的所有 hello 記錄建立、 更新、 刪除和動作的作業執行透過資源管理員。</span><span class="sxs-lookup"><span data-stu-id="02f7c-107">This category contains hello record of all create, update, delete, and action operations performed through Resource Manager.</span></span> <span data-ttu-id="02f7c-108">Hello 類型的事件，您會看到此類別中包含的範例 「 建立虛擬機器 」 和 「 刪除網路安全性群組 」 每個使用者所採取的動作，或使用資源管理員的應用程式會模型化為特定資源類型上的作業。</span><span class="sxs-lookup"><span data-stu-id="02f7c-108">Examples of hello types of events you would see in this category include "create virtual machine" and "delete network security group" Every action taken by a user or application using Resource Manager is modeled as an operation on a particular resource type.</span></span> <span data-ttu-id="02f7c-109">如果 hello 作業類型是寫入刪除或動作，hello 記錄 hello 開始和成功或失敗的作業都會記錄在 hello 系統管理類別。</span><span class="sxs-lookup"><span data-stu-id="02f7c-109">If hello operation type is Write, Delete, or Action, hello records of both hello start and success or fail of that operation are recorded in hello Administrative category.</span></span> <span data-ttu-id="02f7c-110">hello 系統管理類別也會包含在訂閱中的任何變更 toorole 型存取控制。</span><span class="sxs-lookup"><span data-stu-id="02f7c-110">hello Administrative category also includes any changes toorole-based access control in a subscription.</span></span>

### <a name="sample-event"></a><span data-ttu-id="02f7c-111">範例事件</span><span class="sxs-lookup"><span data-stu-id="02f7c-111">Sample event</span></span>
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

### <a name="property-descriptions"></a><span data-ttu-id="02f7c-112">屬性描述</span><span class="sxs-lookup"><span data-stu-id="02f7c-112">Property descriptions</span></span>
| <span data-ttu-id="02f7c-113">元素名稱</span><span class="sxs-lookup"><span data-stu-id="02f7c-113">Element Name</span></span> | <span data-ttu-id="02f7c-114">說明</span><span class="sxs-lookup"><span data-stu-id="02f7c-114">Description</span></span> |
| --- | --- |
| <span data-ttu-id="02f7c-115">授權</span><span class="sxs-lookup"><span data-stu-id="02f7c-115">authorization</span></span> |<span data-ttu-id="02f7c-116">Blob hello 事件的 RBAC 屬性。</span><span class="sxs-lookup"><span data-stu-id="02f7c-116">Blob of RBAC properties of hello event.</span></span> <span data-ttu-id="02f7c-117">通常包含 hello 「 動作 」、 「 角色 」 和 「 範圍 」 屬性。</span><span class="sxs-lookup"><span data-stu-id="02f7c-117">Usually includes hello “action”, “role” and “scope” properties.</span></span> |
| <span data-ttu-id="02f7c-118">呼叫者</span><span class="sxs-lookup"><span data-stu-id="02f7c-118">caller</span></span> |<span data-ttu-id="02f7c-119">已執行 hello 作業、 UPN 宣告或 SPN 宣告根據可用性的 hello 使用者的電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="02f7c-119">Email address of hello user who has performed hello operation, UPN claim, or SPN claim based on availability.</span></span> |
| <span data-ttu-id="02f7c-120">通道</span><span class="sxs-lookup"><span data-stu-id="02f7c-120">channels</span></span> |<span data-ttu-id="02f7c-121">Hello 下列值之一: 「 系統管理 」、 「 作業 」</span><span class="sxs-lookup"><span data-stu-id="02f7c-121">One of hello following values: “Admin”, “Operation”</span></span> |
| <span data-ttu-id="02f7c-122">claims</span><span class="sxs-lookup"><span data-stu-id="02f7c-122">claims</span></span> |<span data-ttu-id="02f7c-123">hello JWT token 是由 Active Directory tooauthenticate hello 使用者或應用程式 tooperform 資源管理員中的這項作業。</span><span class="sxs-lookup"><span data-stu-id="02f7c-123">hello JWT token used by Active Directory tooauthenticate hello user or application tooperform this operation in resource manager.</span></span> |
| <span data-ttu-id="02f7c-124">correlationId</span><span class="sxs-lookup"><span data-stu-id="02f7c-124">correlationId</span></span> |<span data-ttu-id="02f7c-125">通常是 hello 字串格式 GUID。</span><span class="sxs-lookup"><span data-stu-id="02f7c-125">Usually a GUID in hello string format.</span></span> <span data-ttu-id="02f7c-126">共用的相互關聯識別碼的事件屬於 toohello 相同超級動作。</span><span class="sxs-lookup"><span data-stu-id="02f7c-126">Events that share a correlationId belong toohello same uber action.</span></span> |
| <span data-ttu-id="02f7c-127">說明</span><span class="sxs-lookup"><span data-stu-id="02f7c-127">description</span></span> |<span data-ttu-id="02f7c-128">事件的靜態文字描述。</span><span class="sxs-lookup"><span data-stu-id="02f7c-128">Static text description of an event.</span></span> |
| <span data-ttu-id="02f7c-129">eventDataId</span><span class="sxs-lookup"><span data-stu-id="02f7c-129">eventDataId</span></span> |<span data-ttu-id="02f7c-130">事件的唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="02f7c-130">Unique identifier of an event.</span></span> |
| <span data-ttu-id="02f7c-131">httpRequest</span><span class="sxs-lookup"><span data-stu-id="02f7c-131">httpRequest</span></span> |<span data-ttu-id="02f7c-132">Blob 描述 hello Http 要求。</span><span class="sxs-lookup"><span data-stu-id="02f7c-132">Blob describing hello Http Request.</span></span> <span data-ttu-id="02f7c-133">通常包括 hello"clientRequestId"、"clientIpAddress"和"method"（HTTP 方法。</span><span class="sxs-lookup"><span data-stu-id="02f7c-133">Usually includes hello “clientRequestId”, “clientIpAddress” and “method” (HTTP method.</span></span> <span data-ttu-id="02f7c-134">例如，PUT)。</span><span class="sxs-lookup"><span data-stu-id="02f7c-134">For example, PUT).</span></span> |
| <span data-ttu-id="02f7c-135">層級</span><span class="sxs-lookup"><span data-stu-id="02f7c-135">level</span></span> |<span data-ttu-id="02f7c-136">Hello 事件層級。</span><span class="sxs-lookup"><span data-stu-id="02f7c-136">Level of hello event.</span></span> <span data-ttu-id="02f7c-137">Hello 下列值之一: 「 重大 」、 「 錯誤 」、 「 警告 」、 「 資訊 」 及 「 詳細資訊 」</span><span class="sxs-lookup"><span data-stu-id="02f7c-137">One of hello following values: “Critical”, “Error”, “Warning”, “Informational” and “Verbose”</span></span> |
| <span data-ttu-id="02f7c-138">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="02f7c-138">resourceGroupName</span></span> |<span data-ttu-id="02f7c-139">Hello hello 資源群組名稱會影響資源。</span><span class="sxs-lookup"><span data-stu-id="02f7c-139">Name of hello resource group for hello impacted resource.</span></span> |
| <span data-ttu-id="02f7c-140">resourceProviderName</span><span class="sxs-lookup"><span data-stu-id="02f7c-140">resourceProviderName</span></span> |<span data-ttu-id="02f7c-141">Hello hello 資源提供者的名稱會影響資源</span><span class="sxs-lookup"><span data-stu-id="02f7c-141">Name of hello resource provider for hello impacted resource</span></span> |
| <span data-ttu-id="02f7c-142">resourceId</span><span class="sxs-lookup"><span data-stu-id="02f7c-142">resourceId</span></span> |<span data-ttu-id="02f7c-143">資源識別碼 hello 影響資源。</span><span class="sxs-lookup"><span data-stu-id="02f7c-143">Resource id of hello impacted resource.</span></span> |
| <span data-ttu-id="02f7c-144">operationId</span><span class="sxs-lookup"><span data-stu-id="02f7c-144">operationId</span></span> |<span data-ttu-id="02f7c-145">GUID 對應 tooa 單一作業的 hello 事件之間共用。</span><span class="sxs-lookup"><span data-stu-id="02f7c-145">A GUID shared among hello events that correspond tooa single operation.</span></span> |
| <span data-ttu-id="02f7c-146">operationName</span><span class="sxs-lookup"><span data-stu-id="02f7c-146">operationName</span></span> |<span data-ttu-id="02f7c-147">Hello 作業的名稱。</span><span class="sxs-lookup"><span data-stu-id="02f7c-147">Name of hello operation.</span></span> |
| <span data-ttu-id="02f7c-148">屬性</span><span class="sxs-lookup"><span data-stu-id="02f7c-148">properties</span></span> |<span data-ttu-id="02f7c-149">一組`<Key, Value>`組 （也就是字典） 描述 hello hello 事件詳細資料。</span><span class="sxs-lookup"><span data-stu-id="02f7c-149">Set of `<Key, Value>` pairs (that is, a Dictionary) describing hello details of hello event.</span></span> |
| <span data-ttu-id="02f7c-150">status</span><span class="sxs-lookup"><span data-stu-id="02f7c-150">status</span></span> |<span data-ttu-id="02f7c-151">描述 hello hello 作業狀態的字串。</span><span class="sxs-lookup"><span data-stu-id="02f7c-151">String describing hello status of hello operation.</span></span> <span data-ttu-id="02f7c-152">常見的值包括︰Started、In Progress、Succeeded、Failed、Active、Resolved。</span><span class="sxs-lookup"><span data-stu-id="02f7c-152">Some common values are: Started, In Progress, Succeeded, Failed, Active, Resolved.</span></span> |
| <span data-ttu-id="02f7c-153">子狀態</span><span class="sxs-lookup"><span data-stu-id="02f7c-153">subStatus</span></span> |<span data-ttu-id="02f7c-154">通常 hello hello 對應 REST 呼叫的 HTTP 狀態碼，但也可能包含其他描述子狀態，例如這些常見的值的字串: [確定] (HTTP 狀態碼： 200)，建立 (HTTP 狀態碼： 201)、 接受 (HTTP 狀態碼： 202)，無內容 (HTTP狀態碼： 204)，不正確的要求 (HTTP 狀態碼： 400)、 找不到 (HTTP 狀態碼： 404)，衝突 (HTTP 狀態碼： 409)，內部伺服器錯誤 (HTTP 狀態碼： 500)，則 Service 無法使用 (HTTP 狀態碼： 503)，閘道逾時 (HTTP 狀態碼： 504)。</span><span class="sxs-lookup"><span data-stu-id="02f7c-154">Usually hello HTTP status code of hello corresponding REST call, but can also include other strings describing a substatus, such as these common values: OK (HTTP Status Code: 200), Created (HTTP Status Code: 201), Accepted (HTTP Status Code: 202), No Content (HTTP Status Code: 204), Bad Request (HTTP Status Code: 400), Not Found (HTTP Status Code: 404), Conflict (HTTP Status Code: 409), Internal Server Error (HTTP Status Code: 500), Service Unavailable (HTTP Status Code: 503), Gateway Timeout (HTTP Status Code: 504).</span></span> |
| <span data-ttu-id="02f7c-155">eventTimestamp</span><span class="sxs-lookup"><span data-stu-id="02f7c-155">eventTimestamp</span></span> |<span data-ttu-id="02f7c-156">Hello Azure 服務處理 hello 產生 hello 事件時的時間戳記要求相對應的 hello 事件。</span><span class="sxs-lookup"><span data-stu-id="02f7c-156">Timestamp when hello event was generated by hello Azure service processing hello request corresponding hello event.</span></span> |
| <span data-ttu-id="02f7c-157">submissionTimestamp</span><span class="sxs-lookup"><span data-stu-id="02f7c-157">submissionTimestamp</span></span> |<span data-ttu-id="02f7c-158">時間戳記 hello 事件變成可供查詢。</span><span class="sxs-lookup"><span data-stu-id="02f7c-158">Timestamp when hello event became available for querying.</span></span> |
| <span data-ttu-id="02f7c-159">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="02f7c-159">subscriptionId</span></span> |<span data-ttu-id="02f7c-160">Azure 訂用帳戶識別碼。</span><span class="sxs-lookup"><span data-stu-id="02f7c-160">Azure Subscription Id.</span></span> |

## <a name="service-health"></a><span data-ttu-id="02f7c-161">服務健康情況</span><span class="sxs-lookup"><span data-stu-id="02f7c-161">Service health</span></span>
<span data-ttu-id="02f7c-162">這個類別所包含任何服務健全狀況事件發生在 Azure 中的 hello 的記錄。</span><span class="sxs-lookup"><span data-stu-id="02f7c-162">This category contains hello record of any service health incidents that have occurred in Azure.</span></span> <span data-ttu-id="02f7c-163">舉例來說，hello 您將會看到此類別中類型是事件的"SQL Azure，在美國東部發生停機。 」</span><span class="sxs-lookup"><span data-stu-id="02f7c-163">An example of hello type of event you would see in this category is "SQL Azure in East US is experiencing downtime."</span></span> <span data-ttu-id="02f7c-164">服務健全狀況事件有五種： 所需的動作、 協助復原、 事件、 維護、 資訊或安全性，和，才會出現您擁有 hello 訂用帳戶會受到 hello 事件中的資源。</span><span class="sxs-lookup"><span data-stu-id="02f7c-164">Service health events come in five varieties: Action Required, Assisted Recovery, Incident, Maintenance, Information, or Security, and only appear if you have a resource in hello subscription that would be impacted by hello event.</span></span>

### <a name="sample-event"></a><span data-ttu-id="02f7c-165">範例事件</span><span class="sxs-lookup"><span data-stu-id="02f7c-165">Sample event</span></span>
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
    "communication": "Starting at approximately 21:41 UTC on 20 Jul 2017, a subset of customers in UK South may experience degraded performance, connectivity drops or timeouts when accessing their Azure resources hosted in this region. Engineers are investigating underlying Network Infrastructure issues in this region. Impacted services may include, but are not limited tooApp Services, Automation, Service Bus, Log Analytics, Key Vault, SQL Database, Service Fabric, Event Hubs, Stream Analytics, Azure Data Movement, API Management, and Azure Search. Multiple engineering teams are engaged in multiple workflows toomitigate hello impact. hello next update will be provided in 60 minutes, or as events warrant.",
    "incidentType": "Incident",
    "trackingId": "NA0F-BJG",
    "impactStartTime": "2017-07-20T21:41:00.0000000Z",
    "impactedServices": "[{\"ImpactedRegions\":[{\"RegionName\":\"UK South\"}],\"ServiceName\":\"Service Fabric\"}]",
    "defaultLanguageTitle": "Network Infrastructure - UK South",
    "defaultLanguageContent": "Starting at approximately 21:41 UTC on 20 Jul 2017, a subset of customers in UK South may experience degraded performance, connectivity drops or timeouts when accessing their Azure resources hosted in this region. Engineers are investigating underlying Network Infrastructure issues in this region. Impacted services may include, but are not limited tooApp Services, Automation, Service Bus, Log Analytics, Key Vault, SQL Database, Service Fabric, Event Hubs, Stream Analytics, Azure Data Movement, API Management, and Azure Search. Multiple engineering teams are engaged in multiple workflows toomitigate hello impact. hello next update will be provided in 60 minutes, or as events warrant.",
    "stage": "Active",
    "communicationId": "636361902146035247",
    "version": "0.1.1"
  }
}
```

### <a name="property-descriptions"></a><span data-ttu-id="02f7c-166">屬性描述</span><span class="sxs-lookup"><span data-stu-id="02f7c-166">Property descriptions</span></span>
<span data-ttu-id="02f7c-167">元素名稱</span><span class="sxs-lookup"><span data-stu-id="02f7c-167">Element Name</span></span> | <span data-ttu-id="02f7c-168">說明</span><span class="sxs-lookup"><span data-stu-id="02f7c-168">Description</span></span>
-------- | -----------
<span data-ttu-id="02f7c-169">通道</span><span class="sxs-lookup"><span data-stu-id="02f7c-169">channels</span></span> | <span data-ttu-id="02f7c-170">是 hello 下列值之一: 「 系統管理 」、 「 作業 」</span><span class="sxs-lookup"><span data-stu-id="02f7c-170">Is one of hello following values: “Admin”, “Operation”</span></span>
<span data-ttu-id="02f7c-171">correlationId</span><span class="sxs-lookup"><span data-stu-id="02f7c-171">correlationId</span></span> | <span data-ttu-id="02f7c-172">通常是 hello 字串格式的 GUID。</span><span class="sxs-lookup"><span data-stu-id="02f7c-172">Is usually a GUID in hello string format.</span></span> <span data-ttu-id="02f7c-173">事件與屬於相同超級動作通常會共用的 toohello hello 相同的相互關聯識別碼。</span><span class="sxs-lookup"><span data-stu-id="02f7c-173">Events with that belong toohello same uber action usually share hello same correlationId.</span></span>
<span data-ttu-id="02f7c-174">說明</span><span class="sxs-lookup"><span data-stu-id="02f7c-174">description</span></span> | <span data-ttu-id="02f7c-175">Hello 事件的描述。</span><span class="sxs-lookup"><span data-stu-id="02f7c-175">Description of hello event.</span></span>
<span data-ttu-id="02f7c-176">eventDataId</span><span class="sxs-lookup"><span data-stu-id="02f7c-176">eventDataId</span></span> | <span data-ttu-id="02f7c-177">hello 事件的唯一識別項。</span><span class="sxs-lookup"><span data-stu-id="02f7c-177">hello unique identifier of an event.</span></span>
<span data-ttu-id="02f7c-178">eventName</span><span class="sxs-lookup"><span data-stu-id="02f7c-178">eventName</span></span> | <span data-ttu-id="02f7c-179">hello hello 事件標題。</span><span class="sxs-lookup"><span data-stu-id="02f7c-179">hello title of hello event.</span></span>
<span data-ttu-id="02f7c-180">層級</span><span class="sxs-lookup"><span data-stu-id="02f7c-180">level</span></span> | <span data-ttu-id="02f7c-181">Hello 事件層級。</span><span class="sxs-lookup"><span data-stu-id="02f7c-181">Level of hello event.</span></span> <span data-ttu-id="02f7c-182">Hello 下列值之一: 「 重大 」、 「 錯誤 」、 「 警告 」、 「 資訊 」 及 「 詳細資訊 」</span><span class="sxs-lookup"><span data-stu-id="02f7c-182">One of hello following values: “Critical”, “Error”, “Warning”, “Informational” and “Verbose”</span></span>
<span data-ttu-id="02f7c-183">resourceProviderName</span><span class="sxs-lookup"><span data-stu-id="02f7c-183">resourceProviderName</span></span> | <span data-ttu-id="02f7c-184">Hello hello 資源提供者的名稱會影響資源。</span><span class="sxs-lookup"><span data-stu-id="02f7c-184">Name of hello resource provider for hello impacted resource.</span></span> <span data-ttu-id="02f7c-185">如果未知，此參數會是 null。</span><span class="sxs-lookup"><span data-stu-id="02f7c-185">If not known, this will be null.</span></span>
<span data-ttu-id="02f7c-186">resourceType</span><span class="sxs-lookup"><span data-stu-id="02f7c-186">resourceType</span></span>| <span data-ttu-id="02f7c-187">資源的 hello hello 類型會影響資源。</span><span class="sxs-lookup"><span data-stu-id="02f7c-187">hello type of resource of hello impacted resource.</span></span> <span data-ttu-id="02f7c-188">如果未知，此參數會是 null。</span><span class="sxs-lookup"><span data-stu-id="02f7c-188">If not known, this will be null.</span></span>
<span data-ttu-id="02f7c-189">子狀態</span><span class="sxs-lookup"><span data-stu-id="02f7c-189">subStatus</span></span> | <span data-ttu-id="02f7c-190">針對服務健康情況事件通常為 null。</span><span class="sxs-lookup"><span data-stu-id="02f7c-190">Usually null for Service Health events.</span></span>
<span data-ttu-id="02f7c-191">eventTimestamp</span><span class="sxs-lookup"><span data-stu-id="02f7c-191">eventTimestamp</span></span> | <span data-ttu-id="02f7c-192">時間戳記 hello 記錄事件產生並提交 toohello 活動記錄檔。</span><span class="sxs-lookup"><span data-stu-id="02f7c-192">Timestamp when hello log event was generated and submitted toohello Activity Log.</span></span>
<span data-ttu-id="02f7c-193">submissionTimestamp</span><span class="sxs-lookup"><span data-stu-id="02f7c-193">submissionTimestamp</span></span> |   <span data-ttu-id="02f7c-194">時間戳記 hello 事件變成可在 hello 活動記錄檔中。</span><span class="sxs-lookup"><span data-stu-id="02f7c-194">Timestamp when hello event became available in hello Activity Log.</span></span>
<span data-ttu-id="02f7c-195">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="02f7c-195">subscriptionId</span></span> | <span data-ttu-id="02f7c-196">hello 記錄這個事件的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="02f7c-196">hello Azure subscription in which this event was logged.</span></span>
<span data-ttu-id="02f7c-197">status</span><span class="sxs-lookup"><span data-stu-id="02f7c-197">status</span></span> | <span data-ttu-id="02f7c-198">描述 hello hello 作業狀態的字串。</span><span class="sxs-lookup"><span data-stu-id="02f7c-198">String describing hello status of hello operation.</span></span> <span data-ttu-id="02f7c-199">某些常見的值為：Active、Resolved。</span><span class="sxs-lookup"><span data-stu-id="02f7c-199">Some common values are: Active, Resolved.</span></span>
<span data-ttu-id="02f7c-200">operationName</span><span class="sxs-lookup"><span data-stu-id="02f7c-200">operationName</span></span> | <span data-ttu-id="02f7c-201">Hello 作業的名稱。</span><span class="sxs-lookup"><span data-stu-id="02f7c-201">Name of hello operation.</span></span> <span data-ttu-id="02f7c-202">通常是 Microsoft.ServiceHealth/incident/action。</span><span class="sxs-lookup"><span data-stu-id="02f7c-202">Usually Microsoft.ServiceHealth/incident/action.</span></span>
<span data-ttu-id="02f7c-203">category</span><span class="sxs-lookup"><span data-stu-id="02f7c-203">category</span></span> | <span data-ttu-id="02f7c-204">"ServiceHealth"</span><span class="sxs-lookup"><span data-stu-id="02f7c-204">"ServiceHealth"</span></span>
<span data-ttu-id="02f7c-205">resourceId</span><span class="sxs-lookup"><span data-stu-id="02f7c-205">resourceId</span></span> | <span data-ttu-id="02f7c-206">如果已知資源識別碼 hello 會影響資源。</span><span class="sxs-lookup"><span data-stu-id="02f7c-206">Resource id of hello impacted resource, if known.</span></span> <span data-ttu-id="02f7c-207">否則會提供訂用帳戶識別碼。</span><span class="sxs-lookup"><span data-stu-id="02f7c-207">Subscription ID is provided otherwise.</span></span>
<span data-ttu-id="02f7c-208">Properties.title</span><span class="sxs-lookup"><span data-stu-id="02f7c-208">Properties.title</span></span> | <span data-ttu-id="02f7c-209">此通訊的 hello 當地語系化標題。</span><span class="sxs-lookup"><span data-stu-id="02f7c-209">hello localized title for this communication.</span></span> <span data-ttu-id="02f7c-210">英文是 hello 預設語言。</span><span class="sxs-lookup"><span data-stu-id="02f7c-210">English is hello default language.</span></span>
<span data-ttu-id="02f7c-211">Properties.communication</span><span class="sxs-lookup"><span data-stu-id="02f7c-211">Properties.communication</span></span> | <span data-ttu-id="02f7c-212">hello 當地語系化 hello 通訊以 HTML 標記的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="02f7c-212">hello localized details of hello communication with HTML markup.</span></span> <span data-ttu-id="02f7c-213">英文是 hello 預設值。</span><span class="sxs-lookup"><span data-stu-id="02f7c-213">English is hello default.</span></span>
<span data-ttu-id="02f7c-214">Properties.incidentType</span><span class="sxs-lookup"><span data-stu-id="02f7c-214">Properties.incidentType</span></span> | <span data-ttu-id="02f7c-215">可能的值：AssistedRecovery、ActionRequired、Information、Incident、Maintenance、Security</span><span class="sxs-lookup"><span data-stu-id="02f7c-215">Possible values: AssistedRecovery, ActionRequired, Information, Incident, Maintenance, Security</span></span>
<span data-ttu-id="02f7c-216">Properties.trackingId</span><span class="sxs-lookup"><span data-stu-id="02f7c-216">Properties.trackingId</span></span> | <span data-ttu-id="02f7c-217">識別此事件相關聯的 hello 事件。</span><span class="sxs-lookup"><span data-stu-id="02f7c-217">Identifies hello incident this event is associated with.</span></span> <span data-ttu-id="02f7c-218">使用此 toocorrelate hello 事件相關的 tooan 事件。</span><span class="sxs-lookup"><span data-stu-id="02f7c-218">Use this toocorrelate hello events related tooan incident.</span></span>
<span data-ttu-id="02f7c-219">Properties.impactedServices</span><span class="sxs-lookup"><span data-stu-id="02f7c-219">Properties.impactedServices</span></span> | <span data-ttu-id="02f7c-220">逸出的 JSON blob hello 服務和區域 hello 事件受影響的描述。</span><span class="sxs-lookup"><span data-stu-id="02f7c-220">An escaped JSON blob which describes hello services and regions that are impacted by hello incident.</span></span> <span data-ttu-id="02f7c-221">Services 清單 (每一份都有 ServiceName) 和 ImpactedRegions 清單 (每一份都有 RegionName)。</span><span class="sxs-lookup"><span data-stu-id="02f7c-221">A list of Services, each of which has a ServiceName and a list of ImpactedRegions, each of which has a RegionName.</span></span>
<span data-ttu-id="02f7c-222">Properties.defaultLanguageTitle</span><span class="sxs-lookup"><span data-stu-id="02f7c-222">Properties.defaultLanguageTitle</span></span> | <span data-ttu-id="02f7c-223">英文版的 hello 通訊</span><span class="sxs-lookup"><span data-stu-id="02f7c-223">hello communication in English</span></span>
<span data-ttu-id="02f7c-224">Properties.defaultLanguageContent</span><span class="sxs-lookup"><span data-stu-id="02f7c-224">Properties.defaultLanguageContent</span></span> | <span data-ttu-id="02f7c-225">做為 html 標記或純文字的英文版的 hello 通訊</span><span class="sxs-lookup"><span data-stu-id="02f7c-225">hello communication in English as either html markup or plain text</span></span>
<span data-ttu-id="02f7c-226">Properties.stage</span><span class="sxs-lookup"><span data-stu-id="02f7c-226">Properties.stage</span></span> | <span data-ttu-id="02f7c-227">AssistedRecovery、ActionRequired、Information、Incident、Security 的可能值：Active、Resolved。</span><span class="sxs-lookup"><span data-stu-id="02f7c-227">Possible values for AssistedRecovery, ActionRequired, Information, Incident, Security: are Active, Resolved.</span></span> <span data-ttu-id="02f7c-228">Maintenance 的可能值︰Active、Planned、InProgress、Canceled、Rescheduled、Resolved、Complete</span><span class="sxs-lookup"><span data-stu-id="02f7c-228">For Maintenance they are: Active, Planned, InProgress, Canceled, Rescheduled, Resolved, Complete</span></span>
<span data-ttu-id="02f7c-229">Properties.communicationId</span><span class="sxs-lookup"><span data-stu-id="02f7c-229">Properties.communicationId</span></span> | <span data-ttu-id="02f7c-230">hello 通訊此事件是相關聯。</span><span class="sxs-lookup"><span data-stu-id="02f7c-230">hello communication this event is associated.</span></span>

## <a name="alert"></a><span data-ttu-id="02f7c-231">警示</span><span class="sxs-lookup"><span data-stu-id="02f7c-231">Alert</span></span>
<span data-ttu-id="02f7c-232">這個類別所包含所有啟用的 Azure 警示 hello 的記錄。</span><span class="sxs-lookup"><span data-stu-id="02f7c-232">This category contains hello record of all activations of Azure alerts.</span></span> <span data-ttu-id="02f7c-233">Hello 您將會看到此類別中類型的範例是事件的"myVM 上的 CPU 百分比已超過 80 hello 過去 5 分鐘。 」</span><span class="sxs-lookup"><span data-stu-id="02f7c-233">An example of hello type of event you would see in this category is "CPU % on myVM has been over 80 for hello past 5 minutes."</span></span> <span data-ttu-id="02f7c-234">各種 Azure 系統都有警示概念，您可以定義某種類型的規則，並在條件符合該規則時接收通知。</span><span class="sxs-lookup"><span data-stu-id="02f7c-234">A variety of Azure systems have an alerting concept -- you can define a rule of some sort and receive a notification when conditions match that rule.</span></span> <span data-ttu-id="02f7c-235">每次支援 Azure 的警示類型 '啟動，' 或 hello 條件都符合的 toogenerate 通知，hello 啟用的記錄也會推入 toothis 類別目錄的 hello 活動記錄檔。</span><span class="sxs-lookup"><span data-stu-id="02f7c-235">Each time a supported Azure alert type 'activates,' or hello conditions are met toogenerate a notification, a record of hello activation is also pushed toothis category of hello Activity Log.</span></span>

### <a name="sample-event"></a><span data-ttu-id="02f7c-236">範例事件</span><span class="sxs-lookup"><span data-stu-id="02f7c-236">Sample event</span></span>

```json
{
  "caller": "Microsoft.Insights/alertRules",
  "channels": "Admin, Operation",
  "claims": {
    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/spn": "Microsoft.Insights/alertRules"
  },
  "correlationId": "/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/microsoft.insights/alertrules/myalert/incidents/L3N1YnNjcmlwdGlvbnMvZGY2MDJjOWMtN2FhMC00MDdkLWE2ZmItZWIyMGM4YmQxMTkyL3Jlc291cmNlR3JvdXBzL0NzbUV2ZW50RE9HRk9PRC1XZXN0VVMvcHJvdmlkZXJzL21pY3Jvc29mdC5pbnNpZ2h0cy9hbGVydHJ1bGVzL215YWxlcnQwNjM2MzYyMjU4NTM1MjIxOTIw",
  "description": "'Disk read LessThan 100000 ([Count]) in hello last 5 minutes' has been resolved for CloudService: myResourceGroup/Production/Event.BackgroundJobsWorker.razzle (myResourceGroup)",
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

### <a name="property-descriptions"></a><span data-ttu-id="02f7c-237">屬性描述</span><span class="sxs-lookup"><span data-stu-id="02f7c-237">Property descriptions</span></span>
| <span data-ttu-id="02f7c-238">元素名稱</span><span class="sxs-lookup"><span data-stu-id="02f7c-238">Element Name</span></span> | <span data-ttu-id="02f7c-239">說明</span><span class="sxs-lookup"><span data-stu-id="02f7c-239">Description</span></span> |
| --- | --- |
| <span data-ttu-id="02f7c-240">呼叫者</span><span class="sxs-lookup"><span data-stu-id="02f7c-240">caller</span></span> | <span data-ttu-id="02f7c-241">一律是 Microsoft.Insights/alertRules</span><span class="sxs-lookup"><span data-stu-id="02f7c-241">Always Microsoft.Insights/alertRules</span></span> |
| <span data-ttu-id="02f7c-242">通道</span><span class="sxs-lookup"><span data-stu-id="02f7c-242">channels</span></span> | <span data-ttu-id="02f7c-243">一律是 “Admin, Operation”</span><span class="sxs-lookup"><span data-stu-id="02f7c-243">Always “Admin, Operation”</span></span> |
| <span data-ttu-id="02f7c-244">claims</span><span class="sxs-lookup"><span data-stu-id="02f7c-244">claims</span></span> | <span data-ttu-id="02f7c-245">JSON 的 hello 警示引擎 hello SPN （服務主體的名稱） 或資源類型的 blob。</span><span class="sxs-lookup"><span data-stu-id="02f7c-245">JSON blob with hello SPN (service principal name), or resource type, of hello alert engine.</span></span> |
| <span data-ttu-id="02f7c-246">correlationId</span><span class="sxs-lookup"><span data-stu-id="02f7c-246">correlationId</span></span> | <span data-ttu-id="02f7c-247">Hello 字串格式的 GUID。</span><span class="sxs-lookup"><span data-stu-id="02f7c-247">A GUID in hello string format.</span></span> |
| <span data-ttu-id="02f7c-248">說明</span><span class="sxs-lookup"><span data-stu-id="02f7c-248">description</span></span> |<span data-ttu-id="02f7c-249">Hello 警示事件的靜態文字描述。</span><span class="sxs-lookup"><span data-stu-id="02f7c-249">Static text description of hello alert event.</span></span> |
| <span data-ttu-id="02f7c-250">eventDataId</span><span class="sxs-lookup"><span data-stu-id="02f7c-250">eventDataId</span></span> |<span data-ttu-id="02f7c-251">Hello 警示事件的唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="02f7c-251">Unique identifier of hello alert event.</span></span> |
| <span data-ttu-id="02f7c-252">層級</span><span class="sxs-lookup"><span data-stu-id="02f7c-252">level</span></span> |<span data-ttu-id="02f7c-253">Hello 事件層級。</span><span class="sxs-lookup"><span data-stu-id="02f7c-253">Level of hello event.</span></span> <span data-ttu-id="02f7c-254">Hello 下列值之一: 「 重大 」、 「 錯誤 」、 「 警告 」、 「 資訊 」 及 「 詳細資訊 」</span><span class="sxs-lookup"><span data-stu-id="02f7c-254">One of hello following values: “Critical”, “Error”, “Warning”, “Informational” and “Verbose”</span></span> |
| <span data-ttu-id="02f7c-255">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="02f7c-255">resourceGroupName</span></span> |<span data-ttu-id="02f7c-256">Hello hello 資源群組名稱會影響資源是否度量的警示。</span><span class="sxs-lookup"><span data-stu-id="02f7c-256">Name of hello resource group for hello impacted resource if it is a metric alert.</span></span> <span data-ttu-id="02f7c-257">對於其他警示類型，這是 hello hello 包含本身 hello 警示的資源群組名稱。</span><span class="sxs-lookup"><span data-stu-id="02f7c-257">For other alert types, this is hello name of hello resource group that contains hello alert itself.</span></span> |
| <span data-ttu-id="02f7c-258">resourceProviderName</span><span class="sxs-lookup"><span data-stu-id="02f7c-258">resourceProviderName</span></span> |<span data-ttu-id="02f7c-259">Hello hello 資源提供者的名稱會影響資源是否度量的警示。</span><span class="sxs-lookup"><span data-stu-id="02f7c-259">Name of hello resource provider for hello impacted resource if it is a metric alert.</span></span> <span data-ttu-id="02f7c-260">對於其他警示類型，這是 hello hello 資源提供者名稱本身 hello 警示。</span><span class="sxs-lookup"><span data-stu-id="02f7c-260">For other alert types, this is hello name of hello resource provider for hello alert itself.</span></span> |
| <span data-ttu-id="02f7c-261">resourceId</span><span class="sxs-lookup"><span data-stu-id="02f7c-261">resourceId</span></span> | <span data-ttu-id="02f7c-262">Hello hello 資源 ID 的名稱會影響資源是否度量的警示。</span><span class="sxs-lookup"><span data-stu-id="02f7c-262">Name of hello resource ID for hello impacted resource if it is a metric alert.</span></span> <span data-ttu-id="02f7c-263">對於其他警示類型，這是 hello hello 警示資源本身的資源識別碼。</span><span class="sxs-lookup"><span data-stu-id="02f7c-263">For other alert types, this is hello resource ID of hello alert resource itself.</span></span> |
| <span data-ttu-id="02f7c-264">operationId</span><span class="sxs-lookup"><span data-stu-id="02f7c-264">operationId</span></span> |<span data-ttu-id="02f7c-265">GUID 對應 tooa 單一作業的 hello 事件之間共用。</span><span class="sxs-lookup"><span data-stu-id="02f7c-265">A GUID shared among hello events that correspond tooa single operation.</span></span> |
| <span data-ttu-id="02f7c-266">operationName</span><span class="sxs-lookup"><span data-stu-id="02f7c-266">operationName</span></span> |<span data-ttu-id="02f7c-267">Hello 作業的名稱。</span><span class="sxs-lookup"><span data-stu-id="02f7c-267">Name of hello operation.</span></span> |
| <span data-ttu-id="02f7c-268">屬性</span><span class="sxs-lookup"><span data-stu-id="02f7c-268">properties</span></span> |<span data-ttu-id="02f7c-269">一組`<Key, Value>`組 （也就是字典） 描述 hello hello 事件詳細資料。</span><span class="sxs-lookup"><span data-stu-id="02f7c-269">Set of `<Key, Value>` pairs (that is, a Dictionary) describing hello details of hello event.</span></span> |
| <span data-ttu-id="02f7c-270">status</span><span class="sxs-lookup"><span data-stu-id="02f7c-270">status</span></span> |<span data-ttu-id="02f7c-271">描述 hello hello 作業狀態的字串。</span><span class="sxs-lookup"><span data-stu-id="02f7c-271">String describing hello status of hello operation.</span></span> <span data-ttu-id="02f7c-272">常見的值包括︰Started、In Progress、Succeeded、Failed、Active、Resolved。</span><span class="sxs-lookup"><span data-stu-id="02f7c-272">Some common values are: Started, In Progress, Succeeded, Failed, Active, Resolved.</span></span> |
| <span data-ttu-id="02f7c-273">子狀態</span><span class="sxs-lookup"><span data-stu-id="02f7c-273">subStatus</span></span> | <span data-ttu-id="02f7c-274">針對警示通常為 null。</span><span class="sxs-lookup"><span data-stu-id="02f7c-274">Usually null for alerts.</span></span> |
| <span data-ttu-id="02f7c-275">eventTimestamp</span><span class="sxs-lookup"><span data-stu-id="02f7c-275">eventTimestamp</span></span> |<span data-ttu-id="02f7c-276">Hello Azure 服務處理 hello 產生 hello 事件時的時間戳記要求相對應的 hello 事件。</span><span class="sxs-lookup"><span data-stu-id="02f7c-276">Timestamp when hello event was generated by hello Azure service processing hello request corresponding hello event.</span></span> |
| <span data-ttu-id="02f7c-277">submissionTimestamp</span><span class="sxs-lookup"><span data-stu-id="02f7c-277">submissionTimestamp</span></span> |<span data-ttu-id="02f7c-278">時間戳記 hello 事件變成可供查詢。</span><span class="sxs-lookup"><span data-stu-id="02f7c-278">Timestamp when hello event became available for querying.</span></span> |
| <span data-ttu-id="02f7c-279">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="02f7c-279">subscriptionId</span></span> |<span data-ttu-id="02f7c-280">Azure 訂用帳戶識別碼。</span><span class="sxs-lookup"><span data-stu-id="02f7c-280">Azure Subscription Id.</span></span> |

### <a name="properties-field-per-alert-type"></a><span data-ttu-id="02f7c-281">每個警示類型的屬性欄位</span><span class="sxs-lookup"><span data-stu-id="02f7c-281">Properties field per alert type</span></span>
<span data-ttu-id="02f7c-282">hello 屬性] 欄位會包含根據 hello 事件來源的 hello 警示有不同的值。</span><span class="sxs-lookup"><span data-stu-id="02f7c-282">hello properties field will contain different values depending on hello source of hello alert event.</span></span> <span data-ttu-id="02f7c-283">兩個常見的警示事件提供者為活動記錄警示和計量警示。</span><span class="sxs-lookup"><span data-stu-id="02f7c-283">Two common alert event providers are Activity Log alerts and metric alerts.</span></span>

#### <a name="properties-for-activity-log-alerts"></a><span data-ttu-id="02f7c-284">活動記錄警示的屬性</span><span class="sxs-lookup"><span data-stu-id="02f7c-284">Properties for Activity Log alerts</span></span>
| <span data-ttu-id="02f7c-285">元素名稱</span><span class="sxs-lookup"><span data-stu-id="02f7c-285">Element Name</span></span> | <span data-ttu-id="02f7c-286">說明</span><span class="sxs-lookup"><span data-stu-id="02f7c-286">Description</span></span> |
| --- | --- |
| <span data-ttu-id="02f7c-287">properties.subscriptionId</span><span class="sxs-lookup"><span data-stu-id="02f7c-287">properties.subscriptionId</span></span> | <span data-ttu-id="02f7c-288">從 hello 活動記錄檔事件導致啟動此活動記錄檔的警示規則 toobe hello 訂用帳戶 ID。</span><span class="sxs-lookup"><span data-stu-id="02f7c-288">hello subscription ID from hello activity log event which caused this activity log alert rule toobe activated.</span></span> |
| <span data-ttu-id="02f7c-289">properties.eventDataId</span><span class="sxs-lookup"><span data-stu-id="02f7c-289">properties.eventDataId</span></span> | <span data-ttu-id="02f7c-290">從 hello 活動記錄檔事件導致啟動此活動記錄檔的警示規則 toobe 事件資料識別碼 hello。</span><span class="sxs-lookup"><span data-stu-id="02f7c-290">hello event data ID from hello activity log event which caused this activity log alert rule toobe activated.</span></span> |
| <span data-ttu-id="02f7c-291">properties.resourceGroup</span><span class="sxs-lookup"><span data-stu-id="02f7c-291">properties.resourceGroup</span></span> | <span data-ttu-id="02f7c-292">從 hello 活動記錄檔事件導致啟動此活動記錄檔的警示規則 toobe hello 資源群組。</span><span class="sxs-lookup"><span data-stu-id="02f7c-292">hello resource group from hello activity log event which caused this activity log alert rule toobe activated.</span></span> |
| <span data-ttu-id="02f7c-293">properties.resourceId</span><span class="sxs-lookup"><span data-stu-id="02f7c-293">properties.resourceId</span></span> | <span data-ttu-id="02f7c-294">從 hello 活動記錄檔事件導致啟動此活動記錄檔的警示規則 toobe hello 資源識別碼。</span><span class="sxs-lookup"><span data-stu-id="02f7c-294">hello resource ID from hello activity log event which caused this activity log alert rule toobe activated.</span></span> |
| <span data-ttu-id="02f7c-295">properties.eventTimestamp</span><span class="sxs-lookup"><span data-stu-id="02f7c-295">properties.eventTimestamp</span></span> | <span data-ttu-id="02f7c-296">hello 導致啟動此活動記錄檔的警示規則 toobe hello 活動記錄檔事件的事件時間戳記。</span><span class="sxs-lookup"><span data-stu-id="02f7c-296">hello event timestamp of hello activity log event which caused this activity log alert rule toobe activated.</span></span> |
| <span data-ttu-id="02f7c-297">properties.operationName</span><span class="sxs-lookup"><span data-stu-id="02f7c-297">properties.operationName</span></span> | <span data-ttu-id="02f7c-298">從 hello 活動記錄檔事件導致啟動此活動記錄檔的警示規則 toobe hello 作業名稱。</span><span class="sxs-lookup"><span data-stu-id="02f7c-298">hello operation name from hello activity log event which caused this activity log alert rule toobe activated.</span></span> |
| <span data-ttu-id="02f7c-299">properties.status</span><span class="sxs-lookup"><span data-stu-id="02f7c-299">properties.status</span></span> | <span data-ttu-id="02f7c-300">從 hello 活動記錄檔事件導致啟動此活動記錄檔的警示規則 toobe hello 狀態。</span><span class="sxs-lookup"><span data-stu-id="02f7c-300">hello status from hello activity log event which caused this activity log alert rule toobe activated.</span></span>|

#### <a name="properties-for-metric-alerts"></a><span data-ttu-id="02f7c-301">計量警示屬性</span><span class="sxs-lookup"><span data-stu-id="02f7c-301">Properties for metric alerts</span></span>
| <span data-ttu-id="02f7c-302">元素名稱</span><span class="sxs-lookup"><span data-stu-id="02f7c-302">Element Name</span></span> | <span data-ttu-id="02f7c-303">說明</span><span class="sxs-lookup"><span data-stu-id="02f7c-303">Description</span></span> |
| --- | --- |
| <span data-ttu-id="02f7c-304">properties.RuleUri</span><span class="sxs-lookup"><span data-stu-id="02f7c-304">properties.RuleUri</span></span> | <span data-ttu-id="02f7c-305">Hello 度量的警示規則本身的資源識別碼。</span><span class="sxs-lookup"><span data-stu-id="02f7c-305">Resource ID of hello metric alert rule itself.</span></span> |
| <span data-ttu-id="02f7c-306">properties.RuleName</span><span class="sxs-lookup"><span data-stu-id="02f7c-306">properties.RuleName</span></span> | <span data-ttu-id="02f7c-307">hello hello 度量的警示規則名稱。</span><span class="sxs-lookup"><span data-stu-id="02f7c-307">hello name of hello metric alert rule.</span></span> |
| <span data-ttu-id="02f7c-308">properties.RuleDescription</span><span class="sxs-lookup"><span data-stu-id="02f7c-308">properties.RuleDescription</span></span> | <span data-ttu-id="02f7c-309">hello hello 度量警示的規則 （如 hello 警示規則中所定義） 的描述。</span><span class="sxs-lookup"><span data-stu-id="02f7c-309">hello description of hello metric alert rule (as defined in hello alert rule).</span></span> |
| <span data-ttu-id="02f7c-310">properties.Threshold</span><span class="sxs-lookup"><span data-stu-id="02f7c-310">properties.Threshold</span></span> | <span data-ttu-id="02f7c-311">hello hello 評估 hello 度量的警示規則中使用的臨界值。</span><span class="sxs-lookup"><span data-stu-id="02f7c-311">hello threshold value used in hello evaluation of hello metric alert rule.</span></span> |
| <span data-ttu-id="02f7c-312">properties.WindowSizeInMinutes</span><span class="sxs-lookup"><span data-stu-id="02f7c-312">properties.WindowSizeInMinutes</span></span> | <span data-ttu-id="02f7c-313">使用 hello 評估 hello 度量的警示規則中的 hello 視窗大小。</span><span class="sxs-lookup"><span data-stu-id="02f7c-313">hello window size used in hello evaluation of hello metric alert rule.</span></span> |
| <span data-ttu-id="02f7c-314">properties.Aggregation</span><span class="sxs-lookup"><span data-stu-id="02f7c-314">properties.Aggregation</span></span> | <span data-ttu-id="02f7c-315">hello hello 度量的警示規則中所定義的彙總類型。</span><span class="sxs-lookup"><span data-stu-id="02f7c-315">hello aggregation type defined in hello metric alert rule.</span></span> |
| <span data-ttu-id="02f7c-316">properties.Operator</span><span class="sxs-lookup"><span data-stu-id="02f7c-316">properties.Operator</span></span> | <span data-ttu-id="02f7c-317">hello hello 評估 hello 度量的警示規則中使用條件式的運算子。</span><span class="sxs-lookup"><span data-stu-id="02f7c-317">hello conditional operator used in hello evaluation of hello metric alert rule.</span></span> |
| <span data-ttu-id="02f7c-318">properties.MetricName</span><span class="sxs-lookup"><span data-stu-id="02f7c-318">properties.MetricName</span></span> | <span data-ttu-id="02f7c-319">使用 hello 評估 hello 度量的警示規則中的 hello 度量 hello 度量名稱。</span><span class="sxs-lookup"><span data-stu-id="02f7c-319">hello metric name of hello metric used in hello evaluation of hello metric alert rule.</span></span> |
| <span data-ttu-id="02f7c-320">properties.MetricUnit</span><span class="sxs-lookup"><span data-stu-id="02f7c-320">properties.MetricUnit</span></span> | <span data-ttu-id="02f7c-321">使用 hello 評估 hello 度量的警示規則中的 hello 度量 hello 度量單位。</span><span class="sxs-lookup"><span data-stu-id="02f7c-321">hello metric unit for hello metric used in hello evaluation of hello metric alert rule.</span></span> |

## <a name="autoscale"></a><span data-ttu-id="02f7c-322">Autoscale</span><span class="sxs-lookup"><span data-stu-id="02f7c-322">Autoscale</span></span>
<span data-ttu-id="02f7c-323">這個類別包含 hello 作業的記錄任何事件相關的 toohello hello 自動調整引擎根據您定義您的訂用帳戶中的任何自動調整規模設定。</span><span class="sxs-lookup"><span data-stu-id="02f7c-323">This category contains hello record of any events related toohello operation of hello autoscale engine based on any autoscale settings you have defined in your subscription.</span></span> <span data-ttu-id="02f7c-324">Hello 您將會看到此類別中類型的範例是事件的 「 自動調整規模小數位數設定動作失敗。 」</span><span class="sxs-lookup"><span data-stu-id="02f7c-324">An example of hello type of event you would see in this category is "Autoscale scale up action failed."</span></span> <span data-ttu-id="02f7c-325">使用自動調整規模，您可以自動向外擴充或調整在 hello 中支援的資源類型的執行個體的數目會根據使用自動調整規模設定的日期和/或負載 （標準） 的資料的時間。</span><span class="sxs-lookup"><span data-stu-id="02f7c-325">Using autoscale, you can automatically scale out or scale in hello number of instances in a supported resource type based on time of day and/or load (metric) data using an autoscale setting.</span></span> <span data-ttu-id="02f7c-326">Hello 條件符合時 tooscale 向上或向下 hello 開始，並成功或失敗的事件會記錄在此類別。</span><span class="sxs-lookup"><span data-stu-id="02f7c-326">When hello conditions are met tooscale up or down, hello start and succeeded or failed events will be recorded in this category.</span></span>

### <a name="sample-event"></a><span data-ttu-id="02f7c-327">範例事件</span><span class="sxs-lookup"><span data-stu-id="02f7c-327">Sample event</span></span>
```json
{
  "caller": "Microsoft.Insights/autoscaleSettings",
  "channels": "Admin, Operation",
  "claims": {
    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/spn": "Microsoft.Insights/autoscaleSettings"
  },
  "correlationId": "fc6a7ff5-ff68-4bb7-81b4-3629212d03d0",
  "description": "hello autoscale engine attempting tooscale resource '/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/Microsoft.ClassicCompute/domainNames/myResourceGroup/slots/Production/roles/myResource' from 3 instances count too2 instances count.",
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
    "Description": "hello autoscale engine attempting tooscale resource '/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/Microsoft.ClassicCompute/domainNames/myResourceGroup/slots/Production/roles/myResource' from 3 instances count too2 instances count.",
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

### <a name="property-descriptions"></a><span data-ttu-id="02f7c-328">屬性描述</span><span class="sxs-lookup"><span data-stu-id="02f7c-328">Property descriptions</span></span>
| <span data-ttu-id="02f7c-329">元素名稱</span><span class="sxs-lookup"><span data-stu-id="02f7c-329">Element Name</span></span> | <span data-ttu-id="02f7c-330">說明</span><span class="sxs-lookup"><span data-stu-id="02f7c-330">Description</span></span> |
| --- | --- |
| <span data-ttu-id="02f7c-331">呼叫者</span><span class="sxs-lookup"><span data-stu-id="02f7c-331">caller</span></span> | <span data-ttu-id="02f7c-332">一律是 Microsoft.Insights/autoscaleSettings</span><span class="sxs-lookup"><span data-stu-id="02f7c-332">Always Microsoft.Insights/autoscaleSettings</span></span> |
| <span data-ttu-id="02f7c-333">通道</span><span class="sxs-lookup"><span data-stu-id="02f7c-333">channels</span></span> | <span data-ttu-id="02f7c-334">一律是 “Admin, Operation”</span><span class="sxs-lookup"><span data-stu-id="02f7c-334">Always “Admin, Operation”</span></span> |
| <span data-ttu-id="02f7c-335">claims</span><span class="sxs-lookup"><span data-stu-id="02f7c-335">claims</span></span> | <span data-ttu-id="02f7c-336">JSON hello SPN （服務主體的名稱） 或資源的類型，hello 自動調整引擎的 blob。</span><span class="sxs-lookup"><span data-stu-id="02f7c-336">JSON blob with hello SPN (service principal name), or resource type, of hello autoscale engine.</span></span> |
| <span data-ttu-id="02f7c-337">correlationId</span><span class="sxs-lookup"><span data-stu-id="02f7c-337">correlationId</span></span> | <span data-ttu-id="02f7c-338">Hello 字串格式的 GUID。</span><span class="sxs-lookup"><span data-stu-id="02f7c-338">A GUID in hello string format.</span></span> |
| <span data-ttu-id="02f7c-339">說明</span><span class="sxs-lookup"><span data-stu-id="02f7c-339">description</span></span> |<span data-ttu-id="02f7c-340">Hello 自動調整事件的靜態文字描述。</span><span class="sxs-lookup"><span data-stu-id="02f7c-340">Static text description of hello autoscale event.</span></span> |
| <span data-ttu-id="02f7c-341">eventDataId</span><span class="sxs-lookup"><span data-stu-id="02f7c-341">eventDataId</span></span> |<span data-ttu-id="02f7c-342">Hello 自動調整事件的唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="02f7c-342">Unique identifier of hello autoscale event.</span></span> |
| <span data-ttu-id="02f7c-343">層級</span><span class="sxs-lookup"><span data-stu-id="02f7c-343">level</span></span> |<span data-ttu-id="02f7c-344">Hello 事件層級。</span><span class="sxs-lookup"><span data-stu-id="02f7c-344">Level of hello event.</span></span> <span data-ttu-id="02f7c-345">Hello 下列值之一: 「 重大 」、 「 錯誤 」、 「 警告 」、 「 資訊 」 及 「 詳細資訊 」</span><span class="sxs-lookup"><span data-stu-id="02f7c-345">One of hello following values: “Critical”, “Error”, “Warning”, “Informational” and “Verbose”</span></span> |
| <span data-ttu-id="02f7c-346">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="02f7c-346">resourceGroupName</span></span> |<span data-ttu-id="02f7c-347">Hello 自動調整規模設定 hello 資源群組名稱。</span><span class="sxs-lookup"><span data-stu-id="02f7c-347">Name of hello resource group for hello autoscale setting.</span></span> |
| <span data-ttu-id="02f7c-348">resourceProviderName</span><span class="sxs-lookup"><span data-stu-id="02f7c-348">resourceProviderName</span></span> |<span data-ttu-id="02f7c-349">Hello 自動調整規模設定 hello 資源提供者名稱。</span><span class="sxs-lookup"><span data-stu-id="02f7c-349">Name of hello resource provider for hello autoscale setting.</span></span> |
| <span data-ttu-id="02f7c-350">resourceId</span><span class="sxs-lookup"><span data-stu-id="02f7c-350">resourceId</span></span> |<span data-ttu-id="02f7c-351">資源識別碼 hello 自動調整規模設定。</span><span class="sxs-lookup"><span data-stu-id="02f7c-351">Resource id of hello autoscale setting.</span></span> |
| <span data-ttu-id="02f7c-352">operationId</span><span class="sxs-lookup"><span data-stu-id="02f7c-352">operationId</span></span> |<span data-ttu-id="02f7c-353">GUID 對應 tooa 單一作業的 hello 事件之間共用。</span><span class="sxs-lookup"><span data-stu-id="02f7c-353">A GUID shared among hello events that correspond tooa single operation.</span></span> |
| <span data-ttu-id="02f7c-354">operationName</span><span class="sxs-lookup"><span data-stu-id="02f7c-354">operationName</span></span> |<span data-ttu-id="02f7c-355">Hello 作業的名稱。</span><span class="sxs-lookup"><span data-stu-id="02f7c-355">Name of hello operation.</span></span> |
| <span data-ttu-id="02f7c-356">屬性</span><span class="sxs-lookup"><span data-stu-id="02f7c-356">properties</span></span> |<span data-ttu-id="02f7c-357">一組`<Key, Value>`組 （也就是字典） 描述 hello hello 事件詳細資料。</span><span class="sxs-lookup"><span data-stu-id="02f7c-357">Set of `<Key, Value>` pairs (that is, a Dictionary) describing hello details of hello event.</span></span> |
| <span data-ttu-id="02f7c-358">properties.Description</span><span class="sxs-lookup"><span data-stu-id="02f7c-358">properties.Description</span></span> | <span data-ttu-id="02f7c-359">詳細的描述哪些 hello 自動調整引擎正在進行的工作。</span><span class="sxs-lookup"><span data-stu-id="02f7c-359">Detailed description of what hello autoscale engine was doing.</span></span> |
| <span data-ttu-id="02f7c-360">properties.ResourceName</span><span class="sxs-lookup"><span data-stu-id="02f7c-360">properties.ResourceName</span></span> | <span data-ttu-id="02f7c-361">資源識別碼 hello 影響資源 (hello 的 hello 正在執行調整動作的資源)</span><span class="sxs-lookup"><span data-stu-id="02f7c-361">Resource ID of hello impacted resource (hello resource on which hello scale action was being performed)</span></span> |
| <span data-ttu-id="02f7c-362">properties.OldInstancesCount</span><span class="sxs-lookup"><span data-stu-id="02f7c-362">properties.OldInstancesCount</span></span> | <span data-ttu-id="02f7c-363">hello 自動調整規模動作之前的執行個體的 hello 數目所花費的效果。</span><span class="sxs-lookup"><span data-stu-id="02f7c-363">hello number of instances before hello autoscale action took effect.</span></span> |
| <span data-ttu-id="02f7c-364">properties.NewInstancesCount</span><span class="sxs-lookup"><span data-stu-id="02f7c-364">properties.NewInstancesCount</span></span> | <span data-ttu-id="02f7c-365">hello 自動調整規模動作之後的執行個體的 hello 數目所花費的效果。</span><span class="sxs-lookup"><span data-stu-id="02f7c-365">hello number of instances after hello autoscale action took effect.</span></span> |
| <span data-ttu-id="02f7c-366">properties.LastScaleActionTime</span><span class="sxs-lookup"><span data-stu-id="02f7c-366">properties.LastScaleActionTime</span></span> | <span data-ttu-id="02f7c-367">hello 的 hello 自動調整規模動作發生時的時間戳記。</span><span class="sxs-lookup"><span data-stu-id="02f7c-367">hello timestamp of when hello autoscale action occurred.</span></span> |
| <span data-ttu-id="02f7c-368">status</span><span class="sxs-lookup"><span data-stu-id="02f7c-368">status</span></span> |<span data-ttu-id="02f7c-369">描述 hello hello 作業狀態的字串。</span><span class="sxs-lookup"><span data-stu-id="02f7c-369">String describing hello status of hello operation.</span></span> <span data-ttu-id="02f7c-370">常見的值包括︰Started、In Progress、Succeeded、Failed、Active、Resolved。</span><span class="sxs-lookup"><span data-stu-id="02f7c-370">Some common values are: Started, In Progress, Succeeded, Failed, Active, Resolved.</span></span> |
| <span data-ttu-id="02f7c-371">子狀態</span><span class="sxs-lookup"><span data-stu-id="02f7c-371">subStatus</span></span> | <span data-ttu-id="02f7c-372">針對自動調整通常為 null。</span><span class="sxs-lookup"><span data-stu-id="02f7c-372">Usually null for autoscale.</span></span> |
| <span data-ttu-id="02f7c-373">eventTimestamp</span><span class="sxs-lookup"><span data-stu-id="02f7c-373">eventTimestamp</span></span> |<span data-ttu-id="02f7c-374">Hello Azure 服務處理 hello 產生 hello 事件時的時間戳記要求相對應的 hello 事件。</span><span class="sxs-lookup"><span data-stu-id="02f7c-374">Timestamp when hello event was generated by hello Azure service processing hello request corresponding hello event.</span></span> |
| <span data-ttu-id="02f7c-375">submissionTimestamp</span><span class="sxs-lookup"><span data-stu-id="02f7c-375">submissionTimestamp</span></span> |<span data-ttu-id="02f7c-376">時間戳記 hello 事件變成可供查詢。</span><span class="sxs-lookup"><span data-stu-id="02f7c-376">Timestamp when hello event became available for querying.</span></span> |
| <span data-ttu-id="02f7c-377">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="02f7c-377">subscriptionId</span></span> |<span data-ttu-id="02f7c-378">Azure 訂用帳戶識別碼。</span><span class="sxs-lookup"><span data-stu-id="02f7c-378">Azure Subscription Id.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="02f7c-379">後續步驟</span><span class="sxs-lookup"><span data-stu-id="02f7c-379">Next steps</span></span>
* [<span data-ttu-id="02f7c-380">深入了解 hello 活動記錄檔 （先前稱為稽核記錄檔）</span><span class="sxs-lookup"><span data-stu-id="02f7c-380">Learn more about hello Activity Log (formerly Audit Logs)</span></span>](monitoring-overview-activity-logs.md)
* [<span data-ttu-id="02f7c-381">資料流 hello Azure 活動記錄檔 tooEvent 集線器</span><span class="sxs-lookup"><span data-stu-id="02f7c-381">Stream hello Azure Activity Log tooEvent Hubs</span></span>](monitoring-stream-activity-logs-event-hubs.md)
