---
title: "aaaScheduler 輸出驗證"
description: "排程器輸出驗證"
services: scheduler
documentationcenter: .NET
author: derek1ee
manager: kevinlam1
editor: 
ms.assetid: 6707f82b-7e32-401b-a960-02aae7bb59cc
ms.service: scheduler
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/15/2016
ms.author: deli
ms.openlocfilehash: ef713f4770b48d0a9176415e87c1042a823582e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="scheduler-outbound-authentication"></a><span data-ttu-id="22631-103">排程器輸出驗證</span><span class="sxs-lookup"><span data-stu-id="22631-103">Scheduler Outbound Authentication</span></span>
<span data-ttu-id="22631-104">排程器作業可能需要 toocall 出 tooservices 需要驗證。</span><span class="sxs-lookup"><span data-stu-id="22631-104">Scheduler jobs may need toocall out tooservices that require authentication.</span></span> <span data-ttu-id="22631-105">如此一來，被呼叫的服務可以判斷是否 hello 排程器工作可以存取它的資源。</span><span class="sxs-lookup"><span data-stu-id="22631-105">This way, a called service can determine if hello Scheduler job can access its resources.</span></span> <span data-ttu-id="22631-106">其中某些服務包括其他 Azure 服務、Salesforce.com、Facebook 和安全的自訂網站。</span><span class="sxs-lookup"><span data-stu-id="22631-106">Some of these services include other Azure services, Salesforce.com, Facebook, and secure custom websites.</span></span>

## <a name="adding-and-removing-authentication"></a><span data-ttu-id="22631-107">新增和移除驗證</span><span class="sxs-lookup"><span data-stu-id="22631-107">Adding and Removing Authentication</span></span>
<span data-ttu-id="22631-108">加入驗證 tooa 排程器工作很簡單 – 將 JSON 子項目`authentication`toohello`request`時建立或更新工作項目。</span><span class="sxs-lookup"><span data-stu-id="22631-108">Adding authentication tooa Scheduler job is simple – add a JSON child element `authentication` toohello `request` element when creating or updating a job.</span></span> <span data-ttu-id="22631-109">密碼的 hello 一部分在 PUT、 PATCH 或 POST 要求 – 傳送 toohello 排程器服務`authentication`物件 – 永遠不會在回應中傳回。</span><span class="sxs-lookup"><span data-stu-id="22631-109">Secrets passed toohello Scheduler service in a PUT, PATCH, or POST request – as part of hello `authentication` object – are never returned in responses.</span></span> <span data-ttu-id="22631-110">在回應中，密碼資訊設定 toonull，或可能具有代表 hello 驗證實體的公開金鑰語彙基元。</span><span class="sxs-lookup"><span data-stu-id="22631-110">In responses, secret information is set toonull or may have a public token that represents hello authenticated entity.</span></span>

<span data-ttu-id="22631-111">tooremove 驗證、 PUT 或 PATCH hello 作業明確地設定 hello `authentication` toonull 的物件。</span><span class="sxs-lookup"><span data-stu-id="22631-111">tooremove authentication, PUT or PATCH hello job explicitly, setting hello `authentication` object toonull.</span></span> <span data-ttu-id="22631-112">您將不會看到回應中傳回的任何驗證屬性。</span><span class="sxs-lookup"><span data-stu-id="22631-112">You will not see any authentication properties back in response.</span></span>

<span data-ttu-id="22631-113">目前，hello 僅支援驗證類型是 hello`ClientCertificate`模型 （適用於使用 hello SSL/TLS 用戶端憑證）、 hello`Basic`模型 （適用於基本驗證），然後 hello`ActiveDirectoryOAuth`模型 （適用於 Active Directory OAuth驗證）。</span><span class="sxs-lookup"><span data-stu-id="22631-113">Currently, hello only supported authentication types are hello `ClientCertificate` model (for using hello SSL/TLS client certificates), hello `Basic` model (for Basic authentication), and hello `ActiveDirectoryOAuth` model (for Active Directory OAuth authentication.)</span></span>

## <a name="request-body-for-clientcertificate-authentication"></a><span data-ttu-id="22631-114">ClientCertificate 驗證的要求本文</span><span class="sxs-lookup"><span data-stu-id="22631-114">Request Body for ClientCertificate Authentication</span></span>
<span data-ttu-id="22631-115">加入使用 hello 驗證時`ClientCertificate`模型中，指定下列額外的項目 hello 要求主體中的 hello。</span><span class="sxs-lookup"><span data-stu-id="22631-115">When adding authentication using hello `ClientCertificate` model, specify hello following additional elements in hello request body.</span></span>  

| <span data-ttu-id="22631-116">元素</span><span class="sxs-lookup"><span data-stu-id="22631-116">Element</span></span> | <span data-ttu-id="22631-117">說明</span><span class="sxs-lookup"><span data-stu-id="22631-117">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="22631-118">*authentication (父元素)*</span><span class="sxs-lookup"><span data-stu-id="22631-118">*authentication (parent element)*</span></span> |<span data-ttu-id="22631-119">使用 SSL 用戶端憑證的驗證物件。</span><span class="sxs-lookup"><span data-stu-id="22631-119">Authentication object for using an SSL client certificate.</span></span> |
| <span data-ttu-id="22631-120">*type*</span><span class="sxs-lookup"><span data-stu-id="22631-120">*type*</span></span> |<span data-ttu-id="22631-121">必要。</span><span class="sxs-lookup"><span data-stu-id="22631-121">Required.</span></span> <span data-ttu-id="22631-122">驗證類型。SSL 用戶端憑證，hello 值必須是`ClientCertificate`。</span><span class="sxs-lookup"><span data-stu-id="22631-122">Type of authentication.For SSL client certificates, hello value must be `ClientCertificate`.</span></span> |
| <span data-ttu-id="22631-123">*pfx*</span><span class="sxs-lookup"><span data-stu-id="22631-123">*pfx*</span></span> |<span data-ttu-id="22631-124">必要。</span><span class="sxs-lookup"><span data-stu-id="22631-124">Required.</span></span> <span data-ttu-id="22631-125">Hello PFX 檔案的 Base64 編碼內容。</span><span class="sxs-lookup"><span data-stu-id="22631-125">Base64-encoded contents of hello PFX file.</span></span> |
| <span data-ttu-id="22631-126">*password*</span><span class="sxs-lookup"><span data-stu-id="22631-126">*password*</span></span> |<span data-ttu-id="22631-127">必要。</span><span class="sxs-lookup"><span data-stu-id="22631-127">Required.</span></span> <span data-ttu-id="22631-128">密碼 tooaccess hello PFX 檔案。</span><span class="sxs-lookup"><span data-stu-id="22631-128">Password tooaccess hello PFX file.</span></span> |

## <a name="response-body-for-clientcertificate-authentication"></a><span data-ttu-id="22631-129">ClientCertificate 驗證的回應本文</span><span class="sxs-lookup"><span data-stu-id="22631-129">Response Body for ClientCertificate Authentication</span></span>
<span data-ttu-id="22631-130">當使用驗證資訊會傳送要求時，hello 回應會包含 hello 遵循驗證相關的項目。</span><span class="sxs-lookup"><span data-stu-id="22631-130">When a request is sent with authentication info, hello response contains hello following authentication-related elements.</span></span>

| <span data-ttu-id="22631-131">元素</span><span class="sxs-lookup"><span data-stu-id="22631-131">Element</span></span> | <span data-ttu-id="22631-132">說明</span><span class="sxs-lookup"><span data-stu-id="22631-132">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="22631-133">*authentication (父元素)*</span><span class="sxs-lookup"><span data-stu-id="22631-133">*authentication (parent element)*</span></span> |<span data-ttu-id="22631-134">使用 SSL 用戶端憑證的驗證物件。</span><span class="sxs-lookup"><span data-stu-id="22631-134">Authentication object for using an SSL client certificate.</span></span> |
| <span data-ttu-id="22631-135">*type*</span><span class="sxs-lookup"><span data-stu-id="22631-135">*type*</span></span> |<span data-ttu-id="22631-136">驗證類型。</span><span class="sxs-lookup"><span data-stu-id="22631-136">Type of authentication.</span></span> <span data-ttu-id="22631-137">SSL 用戶端憑證，hello 值是`ClientCertificate`。</span><span class="sxs-lookup"><span data-stu-id="22631-137">For SSL client certificates, hello value is `ClientCertificate`.</span></span> |
| <span data-ttu-id="22631-138">*certificateThumbprint*</span><span class="sxs-lookup"><span data-stu-id="22631-138">*certificateThumbprint*</span></span> |<span data-ttu-id="22631-139">hello hello 憑證指紋。</span><span class="sxs-lookup"><span data-stu-id="22631-139">hello thumbprint of hello certificate.</span></span> |
| <span data-ttu-id="22631-140">*certificateSubjectName*</span><span class="sxs-lookup"><span data-stu-id="22631-140">*certificateSubjectName*</span></span> |<span data-ttu-id="22631-141">hello 主體辨別的名稱 hello 憑證。</span><span class="sxs-lookup"><span data-stu-id="22631-141">hello subject distinguished name of hello certificate.</span></span> |
| <span data-ttu-id="22631-142">*certificateExpiration*</span><span class="sxs-lookup"><span data-stu-id="22631-142">*certificateExpiration*</span></span> |<span data-ttu-id="22631-143">hello hello 憑證的到期日。</span><span class="sxs-lookup"><span data-stu-id="22631-143">hello expiration date of hello certificate.</span></span> |

## <a name="sample-rest-request-for-clientcertificate-authentication"></a><span data-ttu-id="22631-144">ClientCertificate 驗證的範例 REST 要求</span><span class="sxs-lookup"><span data-stu-id="22631-144">Sample REST Request for ClientCertificate Authentication</span></span>
```
PUT https://management.azure.com/subscriptions/1fe0abdf-581e-4dfe-9ec7-e5cb8e7b205e/resourceGroups/CS-SoutheastAsia-scheduler/providers/Microsoft.Scheduler/jobcollections/southeastasiajc/jobs/httpjob?api-version=2016-01-01 HTTP/1.1
User-Agent: Fiddler
Host: management.azure.com
Authorization: Bearer sometoken
Content-Type: application/json; charset=utf-8

{
  "properties": {
    "startTime": "2015-05-14T14:10:00Z",
    "action": {
      "request": {
        "uri": "https://mywebserviceendpoint.com",
        "method": "GET",
        "headers": {
          "x-ms-version": "2013-03-01"
        },
        "authentication": {
          "type": "clientcertificate",
          "password": "password",
          "pfx": "pfx key"
        }
      },
      "type": "http"
    },
    "recurrence": {
      "frequency": "minute",
      "endTime": "2016-04-10T08:00:00Z",
      "interval": 1
    },
    "state": "enabled",
  }
}
```

## <a name="sample-rest-response-for-clientcertificate-authentication"></a><span data-ttu-id="22631-145">ClientCertificate 驗證的範例 REST 回應</span><span class="sxs-lookup"><span data-stu-id="22631-145">Sample REST Response for ClientCertificate Authentication</span></span>
```
HTTP/1.1 200 OK
Cache-Control: no-cache
Pragma: no-cache
Content-Length: 858
Content-Type: application/json; charset=utf-8
Expires: -1
x-ms-request-id: 56c7b40e-721a-437e-88e6-f68562a73aa8
Server: Microsoft-IIS/8.5
X-AspNet-Version: 4.0.30319
X-Powered-By: ASP.NET
x-ms-ratelimit-remaining-subscription-resource-requests: 599
x-ms-correlation-request-id: 1075219e-e879-4030-bc81-094e54fbabce
x-ms-routing-request-id: WESTUS:20160316T190424Z:1075219e-e879-4030-bc81-094e54fbabce
Strict-Transport-Security: max-age=31536000; includeSubDomains
Date: Wed, 16 Mar 2016 19:04:23 GMT

{
  "id": "/subscriptions/1fe0abdf-581e-4dfe-9ec7-e5cb8e7b205e/resourceGroups/CS-SoutheastAsia-scheduler/providers/Microsoft.Scheduler/jobCollections/southeastasiajc/jobs/httpjob",
  "type": "Microsoft.Scheduler/jobCollections/jobs",
  "name": "southeastasiajc/httpjob",
  "properties": {
    "startTime": "2015-05-14T14:10:00Z",
    "action": {
      "request": {
        "uri": "https://mywebserviceendpoint.com",
        "method": "GET",
        "headers": {
          "x-ms-version": "2013-03-01"
        },
        "authentication": {
          "certificateThumbprint": "88105CG9DF9ADE75B835711D899296CB217D7055",
          "certificateExpiration": "2021-01-01T07:00:00Z",
          "certificateSubjectName": "CN=Scheduler Mgmt",
          "type": "ClientCertificate"
        }
      },
      "type": "http"
    },
    "recurrence": {
      "frequency": "minute",
      "endTime": "2016-04-10T08:00:00Z",
      "interval": 1
    },
    "state": "enabled",
    "status": {
      "nextExecutionTime": "2016-03-16T19:05:00Z",
      "executionCount": 0,
      "failureCount": 0,
      "faultedCount": 0
    }
  }
}
```

## <a name="request-body-for-basic-authentication"></a><span data-ttu-id="22631-146">基本驗證的要求本文</span><span class="sxs-lookup"><span data-stu-id="22631-146">Request Body for Basic Authentication</span></span>
<span data-ttu-id="22631-147">加入使用 hello 驗證時`Basic`模型中，指定下列額外的項目 hello 要求主體中的 hello。</span><span class="sxs-lookup"><span data-stu-id="22631-147">When adding authentication using hello `Basic` model, specify hello following additional elements in hello request body.</span></span>

| <span data-ttu-id="22631-148">元素</span><span class="sxs-lookup"><span data-stu-id="22631-148">Element</span></span> | <span data-ttu-id="22631-149">說明</span><span class="sxs-lookup"><span data-stu-id="22631-149">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="22631-150">*authentication (父元素)*</span><span class="sxs-lookup"><span data-stu-id="22631-150">*authentication (parent element)*</span></span> |<span data-ttu-id="22631-151">使用基本驗證的驗證物件。</span><span class="sxs-lookup"><span data-stu-id="22631-151">Authentication object for using Basic authentication.</span></span> |
| <span data-ttu-id="22631-152">*type*</span><span class="sxs-lookup"><span data-stu-id="22631-152">*type*</span></span> |<span data-ttu-id="22631-153">必要。</span><span class="sxs-lookup"><span data-stu-id="22631-153">Required.</span></span> <span data-ttu-id="22631-154">驗證類型。</span><span class="sxs-lookup"><span data-stu-id="22631-154">Type of authentication.</span></span> <span data-ttu-id="22631-155">Hello 值必須是基本驗證， `Basic`。</span><span class="sxs-lookup"><span data-stu-id="22631-155">For Basic authentication, hello value must be `Basic`.</span></span> |
| <span data-ttu-id="22631-156">*username*</span><span class="sxs-lookup"><span data-stu-id="22631-156">*username*</span></span> |<span data-ttu-id="22631-157">必要。</span><span class="sxs-lookup"><span data-stu-id="22631-157">Required.</span></span> <span data-ttu-id="22631-158">使用者名稱 tooauthenticate。</span><span class="sxs-lookup"><span data-stu-id="22631-158">Username tooauthenticate.</span></span> |
| <span data-ttu-id="22631-159">*password*</span><span class="sxs-lookup"><span data-stu-id="22631-159">*password*</span></span> |<span data-ttu-id="22631-160">必要。</span><span class="sxs-lookup"><span data-stu-id="22631-160">Required.</span></span> <span data-ttu-id="22631-161">密碼 tooauthenticate。</span><span class="sxs-lookup"><span data-stu-id="22631-161">Password tooauthenticate.</span></span> |

## <a name="response-body-for-basic-authentication"></a><span data-ttu-id="22631-162">基本驗證的回應本文</span><span class="sxs-lookup"><span data-stu-id="22631-162">Response Body for Basic Authentication</span></span>
<span data-ttu-id="22631-163">當使用驗證資訊會傳送要求時，hello 回應會包含 hello 遵循驗證相關的項目。</span><span class="sxs-lookup"><span data-stu-id="22631-163">When a request is sent with authentication info, hello response contains hello following authentication-related elements.</span></span>

| <span data-ttu-id="22631-164">元素</span><span class="sxs-lookup"><span data-stu-id="22631-164">Element</span></span> | <span data-ttu-id="22631-165">說明</span><span class="sxs-lookup"><span data-stu-id="22631-165">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="22631-166">*authentication (父元素)*</span><span class="sxs-lookup"><span data-stu-id="22631-166">*authentication (parent element)*</span></span> |<span data-ttu-id="22631-167">使用基本驗證的驗證物件。</span><span class="sxs-lookup"><span data-stu-id="22631-167">Authentication object for using Basic authentication.</span></span> |
| <span data-ttu-id="22631-168">*type*</span><span class="sxs-lookup"><span data-stu-id="22631-168">*type*</span></span> |<span data-ttu-id="22631-169">驗證類型。</span><span class="sxs-lookup"><span data-stu-id="22631-169">Type of authentication.</span></span> <span data-ttu-id="22631-170">基本驗證 hello 值是`Basic`。</span><span class="sxs-lookup"><span data-stu-id="22631-170">For Basic authentication, hello value is `Basic`.</span></span> |
| <span data-ttu-id="22631-171">*username*</span><span class="sxs-lookup"><span data-stu-id="22631-171">*username*</span></span> |<span data-ttu-id="22631-172">hello 驗證使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="22631-172">hello authenticated username.</span></span> |

## <a name="sample-rest-request-for-basic-authentication"></a><span data-ttu-id="22631-173">基本驗證的範例 REST 要求</span><span class="sxs-lookup"><span data-stu-id="22631-173">Sample REST Request for Basic Authentication</span></span>
```
PUT https://management.azure.com/subscriptions/1d908808-e491-4fe5-b97e-29886e18efd4/resourceGroups/CS-SoutheastAsia-scheduler/providers/Microsoft.Scheduler/jobcollections/southeastasiajc/jobs/httpjob?api-version=2016-01-01 HTTP/1.1
User-Agent: Fiddler
Host: management.azure.com
Authorization: Bearer sometoken
Content-Length: 562
Content-Type: application/json; charset=utf-8

{
  "properties": {
    "startTime": "2015-05-14T14:10:00Z",
    "action": {
      "request": {
        "uri": "https://mywebserviceendpoint.com",
        "method": "GET",
        "headers": {
          "x-ms-version": "2013-03-01"
        },
        "authentication": {
          "type": "basic",
          "username": "user",
          "password": "password"
        }
      },
      "type": "http"
    },
    "recurrence": {
      "frequency": "minute",
      "endTime": "2016-04-10T08:00:00Z",
      "interval": 1
    },
    "state": "enabled",
  }
}
```

## <a name="sample-rest-response-for-basic-authentication"></a><span data-ttu-id="22631-174">基本驗證的範例 REST 回應</span><span class="sxs-lookup"><span data-stu-id="22631-174">Sample REST Response for Basic Authentication</span></span>
```
HTTP/1.1 200 OK
Cache-Control: no-cache
Pragma: no-cache
Content-Length: 701
Content-Type: application/json; charset=utf-8
Expires: -1
x-ms-request-id: a2dcb9cd-1aea-4887-8893-d81273a8cf04
Server: Microsoft-IIS/8.5
X-AspNet-Version: 4.0.30319
X-Powered-By: ASP.NET
x-ms-ratelimit-remaining-subscription-resource-requests: 599
x-ms-correlation-request-id: 7816f222-6ea7-468d-b919-e6ddebbd7e95
x-ms-routing-request-id: WESTUS:20160316T190506Z:7816f222-6ea7-468d-b919-e6ddebbd7e95
Strict-Transport-Security: max-age=31536000; includeSubDomains
Date: Wed, 16 Mar 2016 19:05:06 GMT

{  
   "id":"/subscriptions/1d908808-e491-4fe5-b97e-29886e18efd4/resourceGroups/CS-SoutheastAsia-scheduler/providers/Microsoft.Scheduler/jobCollections/southeastasiajc/jobs/httpjob",
   "type":"Microsoft.Scheduler/jobCollections/jobs",
   "name":"southeastasiajc/httpjob",
   "properties":{  
      "startTime":"2015-05-14T14:10:00Z",
      "action":{  
         "request":{  
            "uri":"https://mywebserviceendpoint.com",
            "method":"GET",
            "headers":{  
               "x-ms-version":"2013-03-01"
            },
            "authentication":{  
               "username":"user1",
               "type":"Basic"
            }
         },
         "type":"http"
      },
      "recurrence":{  
         "frequency":"minute",
         "endTime":"2016-04-10T08:00:00Z",
         "interval":1
      },
      "state":"enabled",
      "status":{  
         "nextExecutionTime":"2016-03-16T19:06:00Z",
         "executionCount":0,
         "failureCount":0,
         "faultedCount":0
      }
   }
}
```

## <a name="request-body-for-activedirectoryoauth-authentication"></a><span data-ttu-id="22631-175">ActiveDirectoryOAuth 驗證的要求本文</span><span class="sxs-lookup"><span data-stu-id="22631-175">Request Body for ActiveDirectoryOAuth Authentication</span></span>
<span data-ttu-id="22631-176">加入使用 hello 驗證時`ActiveDirectoryOAuth`模型中，指定下列額外的項目 hello 要求主體中的 hello。</span><span class="sxs-lookup"><span data-stu-id="22631-176">When adding authentication using hello `ActiveDirectoryOAuth` model, specify hello following additional elements in hello request body.</span></span>

| <span data-ttu-id="22631-177">元素</span><span class="sxs-lookup"><span data-stu-id="22631-177">Element</span></span> | <span data-ttu-id="22631-178">說明</span><span class="sxs-lookup"><span data-stu-id="22631-178">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="22631-179">*authentication (父元素)*</span><span class="sxs-lookup"><span data-stu-id="22631-179">*authentication (parent element)*</span></span> |<span data-ttu-id="22631-180">使用 ActiveDirectoryOAuth 驗證的驗證物件。</span><span class="sxs-lookup"><span data-stu-id="22631-180">Authentication object for using ActiveDirectoryOAuth authentication.</span></span> |
| <span data-ttu-id="22631-181">*type*</span><span class="sxs-lookup"><span data-stu-id="22631-181">*type*</span></span> |<span data-ttu-id="22631-182">必要。</span><span class="sxs-lookup"><span data-stu-id="22631-182">Required.</span></span> <span data-ttu-id="22631-183">驗證類型。</span><span class="sxs-lookup"><span data-stu-id="22631-183">Type of authentication.</span></span> <span data-ttu-id="22631-184">ActiveDirectoryOAuth 驗證的 hello 值必須是`ActiveDirectoryOAuth`。</span><span class="sxs-lookup"><span data-stu-id="22631-184">For ActiveDirectoryOAuth authentication, hello value must be `ActiveDirectoryOAuth`.</span></span> |
| <span data-ttu-id="22631-185">*tenant*</span><span class="sxs-lookup"><span data-stu-id="22631-185">*tenant*</span></span> |<span data-ttu-id="22631-186">必要。</span><span class="sxs-lookup"><span data-stu-id="22631-186">Required.</span></span> <span data-ttu-id="22631-187">hello hello Azure AD 租用戶的租用戶識別碼。</span><span class="sxs-lookup"><span data-stu-id="22631-187">hello tenant identifier for hello Azure AD tenant.</span></span> |
| <span data-ttu-id="22631-188">*audience*</span><span class="sxs-lookup"><span data-stu-id="22631-188">*audience*</span></span> |<span data-ttu-id="22631-189">必要。</span><span class="sxs-lookup"><span data-stu-id="22631-189">Required.</span></span> <span data-ttu-id="22631-190">這會設定 toohttps://management.core.windows.net/。</span><span class="sxs-lookup"><span data-stu-id="22631-190">This is set toohttps://management.core.windows.net/.</span></span> |
| <span data-ttu-id="22631-191">*clientId*</span><span class="sxs-lookup"><span data-stu-id="22631-191">*clientId*</span></span> |<span data-ttu-id="22631-192">必要。</span><span class="sxs-lookup"><span data-stu-id="22631-192">Required.</span></span> <span data-ttu-id="22631-193">Hello Azure AD 應用程式提供 hello 用戶端識別碼。</span><span class="sxs-lookup"><span data-stu-id="22631-193">Provide hello client identifier for hello Azure AD application.</span></span> |
| <span data-ttu-id="22631-194">*secret*</span><span class="sxs-lookup"><span data-stu-id="22631-194">*secret*</span></span> |<span data-ttu-id="22631-195">必要。</span><span class="sxs-lookup"><span data-stu-id="22631-195">Required.</span></span> <span data-ttu-id="22631-196">正在要求 hello 語彙基元的 hello 用戶端的密碼。</span><span class="sxs-lookup"><span data-stu-id="22631-196">Secret of hello client that is requesting hello token.</span></span> |

### <a name="determining-your-tenant-identifier"></a><span data-ttu-id="22631-197">判斷您的租用戶識別碼</span><span class="sxs-lookup"><span data-stu-id="22631-197">Determining your Tenant Identifier</span></span>
<span data-ttu-id="22631-198">您可以執行，以尋找 hello hello Azure AD 租用戶的租用戶識別碼`Get-AzureAccount`Azure PowerShell 中。</span><span class="sxs-lookup"><span data-stu-id="22631-198">You can find hello tenant identifier for hello Azure AD tenant by running `Get-AzureAccount` in Azure PowerShell.</span></span>

## <a name="response-body-for-activedirectoryoauth-authentication"></a><span data-ttu-id="22631-199">ActiveDirectoryOAuth 驗證的回應本文</span><span class="sxs-lookup"><span data-stu-id="22631-199">Response Body for ActiveDirectoryOAuth Authentication</span></span>
<span data-ttu-id="22631-200">當使用驗證資訊會傳送要求時，hello 回應會包含 hello 遵循驗證相關的項目。</span><span class="sxs-lookup"><span data-stu-id="22631-200">When a request is sent with authentication info, hello response contains hello following authentication-related elements.</span></span>

| <span data-ttu-id="22631-201">元素</span><span class="sxs-lookup"><span data-stu-id="22631-201">Element</span></span> | <span data-ttu-id="22631-202">說明</span><span class="sxs-lookup"><span data-stu-id="22631-202">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="22631-203">*authentication (父元素)*</span><span class="sxs-lookup"><span data-stu-id="22631-203">*authentication (parent element)*</span></span> |<span data-ttu-id="22631-204">使用 ActiveDirectoryOAuth 驗證的驗證物件。</span><span class="sxs-lookup"><span data-stu-id="22631-204">Authentication object for using ActiveDirectoryOAuth authentication.</span></span> |
| <span data-ttu-id="22631-205">*type*</span><span class="sxs-lookup"><span data-stu-id="22631-205">*type*</span></span> |<span data-ttu-id="22631-206">驗證類型。</span><span class="sxs-lookup"><span data-stu-id="22631-206">Type of authentication.</span></span> <span data-ttu-id="22631-207">ActiveDirectoryOAuth 驗證的 hello 值是`ActiveDirectoryOAuth`。</span><span class="sxs-lookup"><span data-stu-id="22631-207">For ActiveDirectoryOAuth authentication, hello value is `ActiveDirectoryOAuth`.</span></span> |
| <span data-ttu-id="22631-208">*tenant*</span><span class="sxs-lookup"><span data-stu-id="22631-208">*tenant*</span></span> |<span data-ttu-id="22631-209">hello hello Azure AD 租用戶的租用戶識別碼。</span><span class="sxs-lookup"><span data-stu-id="22631-209">hello tenant identifier for hello Azure AD tenant.</span></span> |
| <span data-ttu-id="22631-210">*audience*</span><span class="sxs-lookup"><span data-stu-id="22631-210">*audience*</span></span> |<span data-ttu-id="22631-211">這會設定 toohttps://management.core.windows.net/。</span><span class="sxs-lookup"><span data-stu-id="22631-211">This is set toohttps://management.core.windows.net/.</span></span> |
| <span data-ttu-id="22631-212">*clientId*</span><span class="sxs-lookup"><span data-stu-id="22631-212">*clientId*</span></span> |<span data-ttu-id="22631-213">hello hello Azure AD 應用程式的用戶端識別項。</span><span class="sxs-lookup"><span data-stu-id="22631-213">hello client identifier for hello Azure AD application.</span></span> |

## <a name="sample-rest-request-for-activedirectoryoauth-authentication"></a><span data-ttu-id="22631-214">ActiveDirectoryOAuth 驗證的範例 REST 要求</span><span class="sxs-lookup"><span data-stu-id="22631-214">Sample REST Request for ActiveDirectoryOAuth Authentication</span></span>
```
PUT https://management.azure.com/subscriptions/1d908808-e491-4fe5-b97e-29886e18efd4/resourceGroups/CS-SoutheastAsia-scheduler/providers/Microsoft.Scheduler/jobcollections/southeastasiajc/jobs/httpjob?api-version=2016-01-01 HTTP/1.1
User-Agent: Fiddler
Host: management.azure.com
Authorization: Bearer sometoken
Content-Length: 757
Content-Type: application/json; charset=utf-8

{
  "properties": {
    "startTime": "2015-05-14T14:10:00Z",
    "action": {
      "request": {
        "uri": "https://mywebserviceendpoint.com",
        "method": "GET",
        "headers": {
          "x-ms-version": "2013-03-01"
        },
        "authentication": {
          "tenant":"microsoft.onmicrosoft.com",
          "audience":"https://management.core.windows.net/",
          "clientId":"dc23e764-9be6-4a33-9b9a-c46e36f0c137",
          "secret": "G6u071r8Gjw4V4KSibnb+VK4+tX399hkHaj7LOyHuj5=",
          "type":"ActiveDirectoryOAuth"
        }
      },
      "type": "http"
    },
    "recurrence": {
      "frequency": "minute",
      "endTime": "2016-04-10T08:00:00Z",
      "interval": 1
    },
    "state": "enabled",
  }
}
```

## <a name="sample-rest-response-for-activedirectoryoauth-authentication"></a><span data-ttu-id="22631-215">ActiveDirectoryOAuth 驗證的範例 REST 回應</span><span class="sxs-lookup"><span data-stu-id="22631-215">Sample REST Response for ActiveDirectoryOAuth Authentication</span></span>
```
HTTP/1.1 200 OK
Cache-Control: no-cache
Pragma: no-cache
Content-Length: 885
Content-Type: application/json; charset=utf-8
Expires: -1
x-ms-request-id: 86d8e9fd-ac0d-4bed-9420-9baba1af3251
Server: Microsoft-IIS/8.5
X-AspNet-Version: 4.0.30319
X-Powered-By: ASP.NET
x-ms-ratelimit-remaining-subscription-resource-requests: 599
x-ms-correlation-request-id: 5183bbf4-9fa1-44bb-98c6-6872e3f2e7ce
x-ms-routing-request-id: WESTUS:20160316T191003Z:5183bbf4-9fa1-44bb-98c6-6872e3f2e7ce
Strict-Transport-Security: max-age=31536000; includeSubDomains
Date: Wed, 16 Mar 2016 19:10:02 GMT

{  
   "id":"/subscriptions/1d908808-e491-4fe5-b97e-29886e18efd4/resourceGroups/CS-SoutheastAsia-scheduler/providers/Microsoft.Scheduler/jobCollections/southeastasiajc/jobs/httpjob",
   "type":"Microsoft.Scheduler/jobCollections/jobs",
   "name":"southeastasiajc/httpjob",
   "properties":{  
      "startTime":"2015-05-14T14:10:00Z",
      "action":{  
         "request":{  
            "uri":"https://mywebserviceendpoint.com",
            "method":"GET",
            "headers":{  
               "x-ms-version":"2013-03-01"
            },
            "authentication":{  
               "tenant":"microsoft.onmicrosoft.com",
               "audience":"https://management.core.windows.net/",
               "clientId":"dc23e764-9be6-4a33-9b9a-c46e36f0c137",
               "type":"ActiveDirectoryOAuth"
            }
         },
         "type":"http"
      },
      "recurrence":{  
         "frequency":"minute",
         "endTime":"2016-04-10T08:00:00Z",
         "interval":1
      },
      "state":"enabled",
      "status":{  
         "lastExecutionTime":"2016-03-16T19:10:00.3762123Z",
         "nextExecutionTime":"2016-03-16T19:11:00Z",
         "executionCount":5,
         "failureCount":5,
         "faultedCount":1
      }
   }
}
```

## <a name="see-also"></a><span data-ttu-id="22631-216">另請參閱</span><span class="sxs-lookup"><span data-stu-id="22631-216">See Also</span></span>
 [<span data-ttu-id="22631-217">排程器是什麼？</span><span class="sxs-lookup"><span data-stu-id="22631-217">What is Scheduler?</span></span>](scheduler-intro.md)

 [<span data-ttu-id="22631-218">Azure 排程器概念、術語及實體階層</span><span class="sxs-lookup"><span data-stu-id="22631-218">Azure Scheduler concepts, terminology, and entity hierarchy</span></span>](scheduler-concepts-terms.md)

 [<span data-ttu-id="22631-219">開始在 hello Azure 入口網站中使用排程器</span><span class="sxs-lookup"><span data-stu-id="22631-219">Get started using Scheduler in hello Azure portal</span></span>](scheduler-get-started-portal.md)

 [<span data-ttu-id="22631-220">Azure 排程器的計劃和計費</span><span class="sxs-lookup"><span data-stu-id="22631-220">Plans and billing in Azure Scheduler</span></span>](scheduler-plans-billing.md)

 [<span data-ttu-id="22631-221">Azure 排程器 REST API 參考</span><span class="sxs-lookup"><span data-stu-id="22631-221">Azure Scheduler REST API reference</span></span>](https://msdn.microsoft.com/library/mt629143)

 [<span data-ttu-id="22631-222">Azure 排程器 PowerShell Cmdlet 參考</span><span class="sxs-lookup"><span data-stu-id="22631-222">Azure Scheduler PowerShell cmdlets reference</span></span>](scheduler-powershell-reference.md)

 [<span data-ttu-id="22631-223">Azure 排程器高可用性和可靠性</span><span class="sxs-lookup"><span data-stu-id="22631-223">Azure Scheduler high-availability and reliability</span></span>](scheduler-high-availability-reliability.md)

 [<span data-ttu-id="22631-224">Azure 排程器限制、預設值和錯誤碼</span><span class="sxs-lookup"><span data-stu-id="22631-224">Azure Scheduler limits, defaults, and error codes</span></span>](scheduler-limits-defaults-errors.md)

