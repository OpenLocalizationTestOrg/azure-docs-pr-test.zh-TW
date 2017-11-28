---
title: "使用 REST 設定 Azure 媒體服務遙測 | Microsoft Docs"
description: "本文示範如何透過 REST API 使用 Azure 媒體服務遙測。"
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: e1a314fb-cc05-4a82-a41b-d1c9888aab09
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: juliako
ms.openlocfilehash: 7d785c6eb9a9e16ae4853cded3c7c142080c7a09
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="configuring-azure-media-services-telemetry-with-rest"></a><span data-ttu-id="b9687-103">使用 REST 設定 Azure 媒體服務遙測</span><span class="sxs-lookup"><span data-stu-id="b9687-103">Configuring Azure Media Services telemetry with REST</span></span>

<span data-ttu-id="b9687-104">本主題說明您使用 REST API 設定 Azure 媒體服務 (AMS) 遙測時可能採取的一般步驟。</span><span class="sxs-lookup"><span data-stu-id="b9687-104">This topic describes general steps that you might take when configuring the Azure Media Services (AMS) telemetry using REST API.</span></span> 

>[!NOTE]
><span data-ttu-id="b9687-105">如需什麼是 AMS 遙測及如何取用的詳細說明，請參閱[概觀](media-services-telemetry-overview.md)主題。</span><span class="sxs-lookup"><span data-stu-id="b9687-105">For the detailed explanation of what is AMS telemetry and how to consume it, see the [overview](media-services-telemetry-overview.md) topic.</span></span>

<span data-ttu-id="b9687-106">本主題中所述的步驟如下︰</span><span class="sxs-lookup"><span data-stu-id="b9687-106">The steps described in this topic are:</span></span>

- <span data-ttu-id="b9687-107">取得與媒體服務帳戶相關聯的儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="b9687-107">Getting the storage account associated with a Media Services account</span></span>
- <span data-ttu-id="b9687-108">取得通知端點</span><span class="sxs-lookup"><span data-stu-id="b9687-108">Getting the Notification Endpoints</span></span>
- <span data-ttu-id="b9687-109">建立用於監視的通知端點。</span><span class="sxs-lookup"><span data-stu-id="b9687-109">Creating a Notification Endpoint for Monitoring.</span></span> 

    <span data-ttu-id="b9687-110">若要建立通知端點，請將 EndPointType 設為 AzureTable (2)，並將 endPontAddress 設為儲存體資料表 (例如，https://telemetryvalidationstore.table.core.windows.net/)。</span><span class="sxs-lookup"><span data-stu-id="b9687-110">To create a Notification Endpoint, set the EndPointType to AzureTable (2) and endPontAddress set to the storage table (for example, https://telemetryvalidationstore.table.core.windows.net/).</span></span>
  
- <span data-ttu-id="b9687-111">取得監視組態</span><span class="sxs-lookup"><span data-stu-id="b9687-111">Get the monitoring configurations</span></span>

    <span data-ttu-id="b9687-112">針對要監視的服務建立監視組態設定。</span><span class="sxs-lookup"><span data-stu-id="b9687-112">Create a monitoring configuration settings for the services you want to monitor.</span></span> <span data-ttu-id="b9687-113">系統最多只允許一個監視組態設定。</span><span class="sxs-lookup"><span data-stu-id="b9687-113">No more than one monitoring configuration settings is allowed.</span></span> 

- <span data-ttu-id="b9687-114">新增監視組態</span><span class="sxs-lookup"><span data-stu-id="b9687-114">Add a monitoring configuration</span></span>


 
## <a name="get-the-storage-account-associated-with-a-media-services-account"></a><span data-ttu-id="b9687-115">取得與媒體服務帳戶相關聯的儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="b9687-115">Get the storage account associated with a Media Services account</span></span>

###<a name="request"></a><span data-ttu-id="b9687-116">要求</span><span class="sxs-lookup"><span data-stu-id="b9687-116">Request</span></span>

    GET https://wamsbnp1clus001rest-hs.cloudapp.net/api/StorageAccounts HTTP/1.1
    x-ms-version: 2.13
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    Accept: application/json; odata=verbose
    Authorization: (redacted)
    Host: wamsbnp1clus001rest-hs.cloudapp.net
    Response
    HTTP/1.1 200 OK
    Cache-Control: no-cache
    Content-Length: 370
    Content-Type: application/json;odata=verbose;charset=utf-8
    Server: Microsoft-IIS/8.5
    request-id: 8206e222-2a59-482c-a6a9-de6b8bda57fb
    x-ms-request-id: 8206e222-2a59-482c-a6a9-de6b8bda57fb
    X-Content-Type-Options: nosniff
    DataServiceVersion: 2.0;
    access-control-expose-headers: request-id, x-ms-request-id
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Wed, 02 Dec 2015 05:10:40 GMT
    
    {"d":{"results":[{"__metadata":{"id":"https://wamsbnp1clus001rest-hs.cloudapp.net/api/StorageAccounts('telemetryvalidationstore')","uri":"https://wamsbnp1clus001rest-hs.cloudapp.net/api/StorageAccounts('telemetryvalidationstore')","type":"Microsoft.Cloud.Media.Vod.Rest.Data.Models.StorageAccount"},"Name":"telemetryvalidationstore","IsDefault":true,"BytesUsed":null}]}}

## <a name="get-the-notification-endpoints"></a><span data-ttu-id="b9687-117">取得通知端點</span><span class="sxs-lookup"><span data-stu-id="b9687-117">Get the Notification Endpoints</span></span>

###<a name="request"></a><span data-ttu-id="b9687-118">要求</span><span class="sxs-lookup"><span data-stu-id="b9687-118">Request</span></span>

    GET https://wamsbnp1clus001rest-hs.cloudapp.net/api/NotificationEndPoints HTTP/1.1
    x-ms-version: 2.13
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    Accept: application/json; odata=verbose
    Authorization: (redacted)
    Host: wamsbnp1clus001rest-hs.cloudapp.net
    
###<a name="response"></a><span data-ttu-id="b9687-119">Response</span><span class="sxs-lookup"><span data-stu-id="b9687-119">Response</span></span>
    HTTP/1.1 200 OK
    Cache-Control: no-cache
    Content-Length: 20
    Content-Type: application/json;odata=verbose;charset=utf-8
    Server: Microsoft-IIS/8.5
    request-id: c68de2b3-0be1-4823-b622-6ca6f94a96b5
    x-ms-request-id: c68de2b3-0be1-4823-b622-6ca6f94a96b5
    X-Content-Type-Options: nosniff
    DataServiceVersion: 2.0;
    access-control-expose-headers: request-id, x-ms-request-id
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Wed, 02 Dec 2015 05:10:40 GMT
    
    {  
        "d":{  
            "results":[]
        }
    }
 
## <a name="create-a-notification-endpoint-for-monitoring"></a><span data-ttu-id="b9687-120">建立用於監視的通知端點</span><span class="sxs-lookup"><span data-stu-id="b9687-120">Create a Notification Endpoint for monitoring</span></span>

###<a name="request"></a><span data-ttu-id="b9687-121">要求</span><span class="sxs-lookup"><span data-stu-id="b9687-121">Request</span></span>

    POST https://wamsbnp1clus001rest-hs.cloudapp.net/api/NotificationEndPoints HTTP/1.1
    x-ms-version: 2.13
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    Accept: application/json; odata=verbose
    Authorization: (redacted)
    Content-Type: application/json; charset=utf-8
    Host: wamsbnp1clus001rest-hs.cloudapp.net
    Content-Length: 115
    
    {  
        "Name":"monitoring",
        "EndPointAddress":"https://telemetryvalidationstore.table.core.windows.net/",
        "EndPointType":2
    }

>[!NOTE]
><span data-ttu-id="b9687-122">別忘了將 "https://telemetryvalidationstore.table.core.windows.net" 值變更為您的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="b9687-122">Don't forget to change the "https://telemetryvalidationstore.table.core.windows.net" value to your storage account.</span></span>

###<a name="response"></a><span data-ttu-id="b9687-123">Response</span><span class="sxs-lookup"><span data-stu-id="b9687-123">Response</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 578
    Content-Type: application/json;odata=verbose;charset=utf-8
    Location: https://wamsbnp1clus001rest-hs.cloudapp.net/api/NotificationEndPoints('nb%3Anepid%3AUUID%3A76bb4faf-ea29-4815-840a-9a8e20102fc4')
    Server: Microsoft-IIS/8.5
    request-id: e8fa5a60-7d8b-4b00-a7ee-9b0f162fe0a9
    x-ms-request-id: e8fa5a60-7d8b-4b00-a7ee-9b0f162fe0a9
    X-Content-Type-Options: nosniff
    DataServiceVersion: 1.0;
    access-control-expose-headers: request-id, x-ms-request-id
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Wed, 02 Dec 2015 05:10:42 GMT
    
    {"d":{"__metadata":{"id":"https://wamsbnp1clus001rest-hs.cloudapp.net/api/NotificationEndPoints('nb%3Anepid%3AUUID%3A76bb4faf-ea29-4815-840a-9a8e20102fc4')","uri":"https://wamsbnp1clus001rest-hs.cloudapp.net/api/NotificationEndPoints('nb%3Anepid%3AUUID%3A76bb4faf-ea29-4815-840a-9a8e20102fc4')","type":"Microsoft.Cloud.Media.Vod.Rest.Data.Models.NotificationEndPoint"},"Id":"nb:nepid:UUID:76bb4faf-ea29-4815-840a-9a8e20102fc4","Name":"monitoring","Created":"\/Date(1449033042667)\/","EndPointAddress":"https://telemetryvalidationstore.table.core.windows.net/","EndPointType":2}}
 
## <a name="get-the-monitoring-configurations"></a><span data-ttu-id="b9687-124">取得監視組態</span><span class="sxs-lookup"><span data-stu-id="b9687-124">Get the monitoring configurations</span></span>

### <a name="request"></a><span data-ttu-id="b9687-125">要求</span><span class="sxs-lookup"><span data-stu-id="b9687-125">Request</span></span>

    GET https://wamsbnp1clus001rest-hs.cloudapp.net/api/MonitoringConfigurations HTTP/1.1
    x-ms-version: 2.13
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    Accept: application/json; odata=verbose
    Authorization: (redacted)
    Host: wamsbnp1clus001rest-hs.cloudapp.net

###<a name="response"></a><span data-ttu-id="b9687-126">Response</span><span class="sxs-lookup"><span data-stu-id="b9687-126">Response</span></span>
    
    HTTP/1.1 200 OK
    Cache-Control: no-cache
    Content-Length: 20
    Content-Type: application/json;odata=verbose;charset=utf-8
    Server: Microsoft-IIS/8.5
    request-id: 00a3ee37-bb19-4fca-b5c7-a92b629d4416
    x-ms-request-id: 00a3ee37-bb19-4fca-b5c7-a92b629d4416
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    access-control-expose-headers: request-id, x-ms-request-id
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Wed, 02 Dec 2015 05:10:42 GMT
    
    {"d":{"results":[]}}

## <a name="add-a-monitoring-configuration"></a><span data-ttu-id="b9687-127">新增監視組態</span><span class="sxs-lookup"><span data-stu-id="b9687-127">Add a monitoring configuration</span></span>

### <a name="request"></a><span data-ttu-id="b9687-128">要求</span><span class="sxs-lookup"><span data-stu-id="b9687-128">Request</span></span>

    POST https://wamsbnp1clus001rest-hs.cloudapp.net/api/MonitoringConfigurations HTTP/1.1
    x-ms-version: 2.13
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    Accept: application/json; odata=verbose
    Authorization: (redacted)
    Content-Type: application/json; charset=utf-8
    Host: wamsbnp1clus001rest-hs.cloudapp.net
    Content-Length: 133
    
    {  
       "NotificationEndPointId":"nb:nepid:UUID:76bb4faf-ea29-4815-840a-9a8e20102fc4",
       "Settings":[  
          {  
         "Component":"Channel",
         "Level":"Normal"
          }
       ]
    }

### <a name="response"></a><span data-ttu-id="b9687-129">Response</span><span class="sxs-lookup"><span data-stu-id="b9687-129">Response</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 825
    Content-Type: application/json;odata=verbose;charset=utf-8
    Location: https://wamsbnp1clus001rest-hs.cloudapp.net/api/MonitoringConfigurations('nb%3Amcid%3AUUID%3A1a8931ae-799f-45fd-8aeb-9641740295c2')
    Server: Microsoft-IIS/8.5
    request-id: daede9cb-8684-41b0-a921-a3af66430cbe
    x-ms-request-id: daede9cb-8684-41b0-a921-a3af66430cbe
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    access-control-expose-headers: request-id, x-ms-request-id
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Wed, 02 Dec 2015 05:10:43 GMT
    
    {"d":{"__metadata":{"id":"https://wamsbnp1clus001rest-hs.cloudapp.net/api/MonitoringConfigurations('nb%3Amcid%3AUUID%3A1a8931ae-799f-45fd-8aeb-9641740295c2')","uri":"https://wamsbnp1clus001rest-hs.cloudapp.net/api/MonitoringConfigurations('nb%3Amcid%3AUUID%3A1a8931ae-799f-45fd-8aeb-9641740295c2')","type":"Microsoft.Cloud.Media.Vod.Rest.Data.Models.MonitoringConfiguration"},"Id":"nb:mcid:UUID:1a8931ae-799f-45fd-8aeb-9641740295c2","NotificationEndPointId":"nb:nepid:UUID:76bb4faf-ea29-4815-840a-9a8e20102fc4","Created":"2015-12-02T05:10:43.7680396Z","LastModified":"2015-12-02T05:10:43.7680396Z","Settings":{"__metadata":{"type":"Collection(Microsoft.Cloud.Media.Vod.Rest.Data.Models.ComponentMonitoringSettings)"},"results":[{"Component":"Channel","Level":"Normal"},{"Component":"StreamingEndpoint","Level":"Disabled"}]}}}

## <a name="stop-telemetry"></a><span data-ttu-id="b9687-130">停止遙測</span><span class="sxs-lookup"><span data-stu-id="b9687-130">Stop telemetry</span></span>

###<a name="request"></a><span data-ttu-id="b9687-131">要求</span><span class="sxs-lookup"><span data-stu-id="b9687-131">Request</span></span>

    DELETE https://wamsbnp1clus001rest-hs.cloudapp.net/api/MonitoringConfigurations('nb%3Amcid%3AUUID%3A1a8931ae-799f-45fd-8aeb-9641740295c2')
    x-ms-version: 2.13
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    Accept: application/json; odata=verbose
    Authorization: (redacted)
    Content-Type: application/json; charset=utf-8
    Host: wamsbnp1clus001rest-hs.cloudapp.net

## <a name="consuming-telemetry-information"></a><span data-ttu-id="b9687-132">取用遙測資訊</span><span class="sxs-lookup"><span data-stu-id="b9687-132">Consuming telemetry information</span></span>

<span data-ttu-id="b9687-133">如需取用遙測資訊的相關資訊，請參閱[這個](media-services-telemetry-overview.md)主題。</span><span class="sxs-lookup"><span data-stu-id="b9687-133">For information about consuming telemetry information, see [this](media-services-telemetry-overview.md) topic.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b9687-134">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b9687-134">Next steps</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="b9687-135">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="b9687-135">Provide feedback</span></span>

[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
