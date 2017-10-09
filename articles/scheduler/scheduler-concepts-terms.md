---
title: "aaaScheduler 概念、 詞彙，以及實體 |Microsoft 文件"
description: "Azure 排程器概念、詞彙及實體階層，包括工作和工作集合。  顯示排程工作的完整範例。"
services: scheduler
documentationcenter: .NET
author: derek1ee
manager: kevinlam1
editor: 
ms.assetid: 3ef16fab-d18a-48ba-8e56-3f3e0a1bcb92
ms.service: scheduler
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: get-started-article
ms.date: 08/18/2016
ms.author: deli
ms.openlocfilehash: 73e7de7bfd2937e401aeab05e0e10fa292cf37b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="scheduler-concepts-terminology--entity-hierarchy"></a><span data-ttu-id="d9bb7-104">排程器概念、術語及實體階層</span><span class="sxs-lookup"><span data-stu-id="d9bb7-104">Scheduler concepts, terminology, + entity hierarchy</span></span>
## <a name="scheduler-entity-hierarchy"></a><span data-ttu-id="d9bb7-105">排程器實體階層</span><span class="sxs-lookup"><span data-stu-id="d9bb7-105">Scheduler entity hierarchy</span></span>
<span data-ttu-id="d9bb7-106">hello 下表描述公開或使用排程器 API hello hello 主要資源：</span><span class="sxs-lookup"><span data-stu-id="d9bb7-106">hello following table describes hello main resources exposed or used by hello Scheduler API:</span></span>

| <span data-ttu-id="d9bb7-107">資源</span><span class="sxs-lookup"><span data-stu-id="d9bb7-107">Resource</span></span> | <span data-ttu-id="d9bb7-108">說明</span><span class="sxs-lookup"><span data-stu-id="d9bb7-108">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d9bb7-109">**工作集合**</span><span class="sxs-lookup"><span data-stu-id="d9bb7-109">**Job collection**</span></span> |<span data-ttu-id="d9bb7-110">工作集合包含的工作群組，並維護設定、 配額及流速 hello 集合內的工作所共用的。</span><span class="sxs-lookup"><span data-stu-id="d9bb7-110">A job collection contains a group of jobs and maintains settings, quotas, and throttles that are shared by jobs within hello collection.</span></span> <span data-ttu-id="d9bb7-111">作業集合是由訂用帳戶擁有者和群組工作一起根據使用方式或應用程式界限所建立的。</span><span class="sxs-lookup"><span data-stu-id="d9bb7-111">A job collection is created by a subscription owner and groups jobs together based on usage or application boundaries.</span></span> <span data-ttu-id="d9bb7-112">它是受條件約束的 tooone 區域。</span><span class="sxs-lookup"><span data-stu-id="d9bb7-112">It’s constrained tooone region.</span></span> <span data-ttu-id="d9bb7-113">它也可讓 hello 強制執行配額 tooconstrain hello 使用量的所有工作在該集合中。</span><span class="sxs-lookup"><span data-stu-id="d9bb7-113">It also allows hello enforcement of quotas tooconstrain hello usage of all jobs in that collection.</span></span> <span data-ttu-id="d9bb7-114">hello 配額包含 MaxJobs 和 MaxRecurrence。</span><span class="sxs-lookup"><span data-stu-id="d9bb7-114">hello quotas include MaxJobs and MaxRecurrence.</span></span> |
| <span data-ttu-id="d9bb7-115">**作業**</span><span class="sxs-lookup"><span data-stu-id="d9bb7-115">**Job**</span></span> |<span data-ttu-id="d9bb7-116">工作定義單一週期動作，以及簡單或複雜的執行策略。</span><span class="sxs-lookup"><span data-stu-id="d9bb7-116">A job defines a single recurrent action, with simple or complex strategies for execution.</span></span> <span data-ttu-id="d9bb7-117">動作可能包括 HTTP、儲存體佇列、服務匯流排佇列或服務匯流排主題要求。</span><span class="sxs-lookup"><span data-stu-id="d9bb7-117">Actions may include HTTP, storage queue, service bus queue, or service bus topic requests.</span></span> |
| <span data-ttu-id="d9bb7-118">**工作歷程記錄**</span><span class="sxs-lookup"><span data-stu-id="d9bb7-118">**Job history**</span></span> |<span data-ttu-id="d9bb7-119">工作歷程記錄代表工作的執行詳細資料。</span><span class="sxs-lookup"><span data-stu-id="d9bb7-119">A job history represents details for an execution of a job.</span></span> <span data-ttu-id="d9bb7-120">它包含成功與失敗，以及任何回應詳細資料。</span><span class="sxs-lookup"><span data-stu-id="d9bb7-120">It contains success vs. failure, as well as any response details.</span></span> |

## <a name="scheduler-entity-management"></a><span data-ttu-id="d9bb7-121">排程器實體管理</span><span class="sxs-lookup"><span data-stu-id="d9bb7-121">Scheduler entity management</span></span>
<span data-ttu-id="d9bb7-122">在高層級，hello 排程器和 hello 服務管理 API 會公開下列 hello 資源執行作業的 hello:</span><span class="sxs-lookup"><span data-stu-id="d9bb7-122">At a high level, hello scheduler and hello service management API expose hello following operations on hello resources:</span></span>

| <span data-ttu-id="d9bb7-123">功能</span><span class="sxs-lookup"><span data-stu-id="d9bb7-123">Capability</span></span> | <span data-ttu-id="d9bb7-124">描述和 URI 位址</span><span class="sxs-lookup"><span data-stu-id="d9bb7-124">Description and URI address</span></span> |
| --- | --- |
| <span data-ttu-id="d9bb7-125">**工作集合管理**</span><span class="sxs-lookup"><span data-stu-id="d9bb7-125">**Job collection management**</span></span> |<span data-ttu-id="d9bb7-126">GET、 PUT 和 DELETE 支援建立和修改工作集合和內含的 hello 工作。</span><span class="sxs-lookup"><span data-stu-id="d9bb7-126">GET, PUT, and DELETE support for creating and modifying job collections and hello jobs contained therein.</span></span> <span data-ttu-id="d9bb7-127">工作集合是工作的容器，並將對應 tooquotas 和共用的設定。</span><span class="sxs-lookup"><span data-stu-id="d9bb7-127">A job collection is a container for jobs and maps tooquotas and shared settings.</span></span> <span data-ttu-id="d9bb7-128">稍後所述的配額範例為最大工作數目和最小週期間隔。</span><span class="sxs-lookup"><span data-stu-id="d9bb7-128">Examples of quotas, described later, are maximum number of jobs and smallest recurrence interval.</span></span> <p><span data-ttu-id="d9bb7-129">PUT 和 DELETE：`https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Scheduler/jobCollections/{jobCollectionName}`</span><span class="sxs-lookup"><span data-stu-id="d9bb7-129">PUT and DELETE: `https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Scheduler/jobCollections/{jobCollectionName}`</span></span></p><p><span data-ttu-id="d9bb7-130">GET：`https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Scheduler/jobCollections/{jobCollectionName}`</span><span class="sxs-lookup"><span data-stu-id="d9bb7-130">GET: `https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Scheduler/jobCollections/{jobCollectionName}`</span></span></p> |
| <span data-ttu-id="d9bb7-131">**工作管理**</span><span class="sxs-lookup"><span data-stu-id="d9bb7-131">**Job management**</span></span> |<span data-ttu-id="d9bb7-132">GET、PUT、POST、PATCH 和 DELETE 支援建立和修改雲端服務。</span><span class="sxs-lookup"><span data-stu-id="d9bb7-132">GET, PUT, POST, PATCH, and DELETE support for creating and modifying jobs.</span></span> <span data-ttu-id="d9bb7-133">所有工作必須都屬於 tooa 工作集合已存在，因此沒有隱含建立。</span><span class="sxs-lookup"><span data-stu-id="d9bb7-133">All jobs must belong tooa job collection that already exists, so there is no implicit creation.</span></span> <p>`https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Scheduler/jobCollections/{jobCollectionName}/jobs/{jobName}`</p> |
| <span data-ttu-id="d9bb7-134">**工作歷程記錄管理**</span><span class="sxs-lookup"><span data-stu-id="d9bb7-134">**Job history management**</span></span> |<span data-ttu-id="d9bb7-135">GET 支援擷取 60 天的工作執行歷程記錄，例如工作經歷時間和工作執行結果。</span><span class="sxs-lookup"><span data-stu-id="d9bb7-135">GET support for fetching 60 days of job execution history, such as job elapsed time and job execution results.</span></span> <span data-ttu-id="d9bb7-136">加入根據狀況和狀態篩選的查詢字串參數支援。</span><span class="sxs-lookup"><span data-stu-id="d9bb7-136">Adds query string parameter support for filtering based on state and status.</span></span> <P>`https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Scheduler/jobCollections/{jobCollectionName}/jobs/{jobName}/history`</p> |

## <a name="job-types"></a><span data-ttu-id="d9bb7-137">工作類型</span><span class="sxs-lookup"><span data-stu-id="d9bb7-137">Job types</span></span>
<span data-ttu-id="d9bb7-138">工作有多種類型︰HTTP 工作 (包括支援 SSL 的 HTTPS 工作)、儲存體佇列工作、服務匯流排佇列工作和服務匯流排主題工作。</span><span class="sxs-lookup"><span data-stu-id="d9bb7-138">There are multiple types of jobs: HTTP jobs (including HTTPS jobs that support SSL), storage queue jobs, service bus queue jobs, and service bus topic jobs.</span></span> <span data-ttu-id="d9bb7-139">如果您有現有的工作負載或服務的端點，則 HTTP 工作是理想的工作。</span><span class="sxs-lookup"><span data-stu-id="d9bb7-139">HTTP jobs are ideal if you have an endpoint of an existing workload or service.</span></span> <span data-ttu-id="d9bb7-140">您可以使用儲存體佇列工作 toopost 訊息 toostorage 佇列，讓這些工作都適合用來儲存體佇列的工作負載。</span><span class="sxs-lookup"><span data-stu-id="d9bb7-140">You can use storage queue jobs toopost messages toostorage queues, so those jobs are ideal for workloads that use storage queues.</span></span> <span data-ttu-id="d9bb7-141">同樣地，服務匯流排工作很適合用於使用服務匯流排佇列和主題的工作負載。</span><span class="sxs-lookup"><span data-stu-id="d9bb7-141">Similarly, service bus jobs are ideal for workloads that use service bus queues and topics.</span></span>

## <a name="hello-job-entity-in-detail"></a><span data-ttu-id="d9bb7-142">在詳細資料中的 hello 「 工作 」 實體</span><span class="sxs-lookup"><span data-stu-id="d9bb7-142">hello "job" entity in detail</span></span>
<span data-ttu-id="d9bb7-143">在基本層級中，排程工作有幾個部分：</span><span class="sxs-lookup"><span data-stu-id="d9bb7-143">At a basic level, a scheduled job has several parts:</span></span>

* <span data-ttu-id="d9bb7-144">hello 動作 tooperform hello 工作計時器啟動時</span><span class="sxs-lookup"><span data-stu-id="d9bb7-144">hello action tooperform when hello job timer fires</span></span>  
* <span data-ttu-id="d9bb7-145">（選擇性） hello 時間 toorun hello 工作</span><span class="sxs-lookup"><span data-stu-id="d9bb7-145">(Optional) hello time toorun hello job</span></span>  
* <span data-ttu-id="d9bb7-146">（選擇性）時間和頻率 toorepeat hello 工作</span><span class="sxs-lookup"><span data-stu-id="d9bb7-146">(Optional) When and how often toorepeat hello job</span></span>  
* <span data-ttu-id="d9bb7-147">（選擇性）動作 toofire hello 主要動作失敗時</span><span class="sxs-lookup"><span data-stu-id="d9bb7-147">(Optional) An action toofire if hello primary action fails</span></span>  

<span data-ttu-id="d9bb7-148">就內部而言，排程的工作也會包含系統提供的資料，例如 hello 下次排程執行時間。</span><span class="sxs-lookup"><span data-stu-id="d9bb7-148">Internally, a scheduled job also contains system-provided data such as hello next scheduled execution time.</span></span>

<span data-ttu-id="d9bb7-149">下列程式碼的 hello 提供排程工作的完整範例。</span><span class="sxs-lookup"><span data-stu-id="d9bb7-149">hello following code provides a comprehensive example of a scheduled job.</span></span> <span data-ttu-id="d9bb7-150">後續章節將提供詳細資料。</span><span class="sxs-lookup"><span data-stu-id="d9bb7-150">Details are provided in subsequent sections.</span></span>

    {
        "startTime": "2012-08-04T00:00Z",               // optional
        "action":
        {
            "type": "http",
            "retryPolicy": { "retryType":"none" },
            "request":
            {
                "uri": "http://contoso.com/foo",        // required
                "method": "PUT",                        // required
                "body": "Posting from a timer",         // optional
                "headers":                              // optional

                {
                    "Content-Type": "application/json"
                },
            },
           "errorAction":
           {
               "type": "http",
               "request":
               {
                   "uri": "http://contoso.com/notifyError",
                   "method": "POST",
               },
           },
        },
        "recurrence":                                   // optional
        {
            "frequency": "week",                        // can be "year" "month" "day" "week" "minute"
            "interval": 1,                              // optional, how often toofire (default too1)
            "schedule":                                 // optional (advanced scheduling specifics)
            {
                "weekDays": ["monday", "wednesday", "friday"],
                "hours": [10, 22]
            },
            "count": 10,                                 // optional (default toorecur infinitely)
            "endTime": "2012-11-04",                     // optional (default toorecur infinitely)
        },
        "state": "disabled",                           // enabled or disabled
        "status":                                       // controlled by Scheduler service
        {
            "lastExecutionTime": "2007-03-01T13:00:00Z",
            "nextExecutionTime": "2007-03-01T14:00:00Z ",
            "executionCount": 3,
                                                "failureCount": 0,
                                                "faultedCount": 0
        },
    }

<span data-ttu-id="d9bb7-151">Hello 範例排程工作上面所示，工作定義會有幾個部分：</span><span class="sxs-lookup"><span data-stu-id="d9bb7-151">As seen in hello sample scheduled job above, a job definition has several parts:</span></span>

* <span data-ttu-id="d9bb7-152">開始時間 ("startTime")</span><span class="sxs-lookup"><span data-stu-id="d9bb7-152">Start time (“startTime”)</span></span>  
* <span data-ttu-id="d9bb7-153">動作 ("action")，其中包含錯誤動作 ("errorAction")</span><span class="sxs-lookup"><span data-stu-id="d9bb7-153">Action (“action”), which includes error action (“errorAction”)</span></span>
* <span data-ttu-id="d9bb7-154">週期 ("recurrence")</span><span class="sxs-lookup"><span data-stu-id="d9bb7-154">Recurrence (“recurrence”)</span></span>  
* <span data-ttu-id="d9bb7-155">狀況 (“state”)</span><span class="sxs-lookup"><span data-stu-id="d9bb7-155">State (“state”)</span></span>  
* <span data-ttu-id="d9bb7-156">狀態 (“status”)</span><span class="sxs-lookup"><span data-stu-id="d9bb7-156">Status (“status”)</span></span>  
* <span data-ttu-id="d9bb7-157">重試原則 ("retryPolicy")</span><span class="sxs-lookup"><span data-stu-id="d9bb7-157">Retry policy (“retryPolicy”)</span></span>  

<span data-ttu-id="d9bb7-158">讓我們詳細檢查每一種方式：</span><span class="sxs-lookup"><span data-stu-id="d9bb7-158">Let’s examine each of these in detail:</span></span>

## <a name="starttime"></a><span data-ttu-id="d9bb7-159">startTime</span><span class="sxs-lookup"><span data-stu-id="d9bb7-159">startTime</span></span>
<span data-ttu-id="d9bb7-160">hello"startTime"是 hello 開始時間和時區時差中的 hello 網路上允許 hello 呼叫端 toospecify [ISO 8601 格式](http://en.wikipedia.org/wiki/ISO_8601)。</span><span class="sxs-lookup"><span data-stu-id="d9bb7-160">hello "startTime” is hello start time and allows hello caller toospecify a time zone offset on hello wire in [ISO-8601 format](http://en.wikipedia.org/wiki/ISO_8601).</span></span>

## <a name="action-and-erroraction"></a><span data-ttu-id="d9bb7-161">action 和 errorAction</span><span class="sxs-lookup"><span data-stu-id="d9bb7-161">action and errorAction</span></span>
<span data-ttu-id="d9bb7-162">hello 「 動作 」 是每次叫用的 hello 動作，並描述服務叫用類型。</span><span class="sxs-lookup"><span data-stu-id="d9bb7-162">hello “action” is hello action invoked on each occurrence and describes a type of service invocation.</span></span> <span data-ttu-id="d9bb7-163">hello 動作是 hello 提供排程上可執行的內容。</span><span class="sxs-lookup"><span data-stu-id="d9bb7-163">hello action is what will be executed on hello provided schedule.</span></span> <span data-ttu-id="d9bb7-164">排程器支援 HTTP、儲存體佇列、服務匯流排主題和服務匯流排佇列動作。</span><span class="sxs-lookup"><span data-stu-id="d9bb7-164">Scheduler supports HTTP, storage queue, service bus topic, and service bus queue actions.</span></span>

<span data-ttu-id="d9bb7-165">在上面的 hello 範例中的 hello 動作是 HTTP 動作。</span><span class="sxs-lookup"><span data-stu-id="d9bb7-165">hello action in hello example above is an HTTP action.</span></span> <span data-ttu-id="d9bb7-166">以下是儲存體佇列動作的範例：</span><span class="sxs-lookup"><span data-stu-id="d9bb7-166">Below is an example of a storage queue action:</span></span>

    {
            "type": "storageQueue",
            "queueMessage":
            {
                "storageAccount": "myStorageAccount",  // required
                "queueName": "myqueue",                // required
                "sasToken": "TOKEN",                   // required
                "message":                             // required
                    "My message body",
            },
    }

<span data-ttu-id="d9bb7-167">以下是服務匯流排主題動作的範例。</span><span class="sxs-lookup"><span data-stu-id="d9bb7-167">Below is an example of a service bus topic action.</span></span>

  <span data-ttu-id="d9bb7-168">"action": { "type": "serviceBusTopic", "serviceBusTopicMessage": { "topicPath": "t1",</span><span class="sxs-lookup"><span data-stu-id="d9bb7-168">"action": { "type": "serviceBusTopic", "serviceBusTopicMessage": { "topicPath": "t1",</span></span>  
      <span data-ttu-id="d9bb7-169">"namespace": "mySBNamespace", "transportType": "netMessaging", // Can be either netMessaging or AMQP "authentication": { "sasKeyName": "QPolicy", "type": "sharedAccessKey" }, "message": "Some message", "brokeredMessageProperties": {}, "customMessageProperties": { "appname": "FromScheduler" } }, }</span><span class="sxs-lookup"><span data-stu-id="d9bb7-169">"namespace": "mySBNamespace", "transportType": "netMessaging", // Can be either netMessaging or AMQP "authentication": { "sasKeyName": "QPolicy", "type": "sharedAccessKey" }, "message": "Some message", "brokeredMessageProperties": {}, "customMessageProperties": { "appname": "FromScheduler" } }, }</span></span>

<span data-ttu-id="d9bb7-170">以下是服務匯流排佇列動作的範例：</span><span class="sxs-lookup"><span data-stu-id="d9bb7-170">Below is an example of a service bus queue action:</span></span>

  <span data-ttu-id="d9bb7-171">"action": { "serviceBusQueueMessage": { "queueName": "q1",</span><span class="sxs-lookup"><span data-stu-id="d9bb7-171">"action": { "serviceBusQueueMessage": { "queueName": "q1",</span></span>  
      <span data-ttu-id="d9bb7-172">"namespace": "mySBNamespace", "transportType": "netMessaging", // Can be either netMessaging or AMQP "authentication": {</span><span class="sxs-lookup"><span data-stu-id="d9bb7-172">"namespace": "mySBNamespace", "transportType": "netMessaging", // Can be either netMessaging or AMQP "authentication": {</span></span>  
        <span data-ttu-id="d9bb7-173">"sasKeyName": "QPolicy", "type": "sharedAccessKey" }, "message": "Some message",</span><span class="sxs-lookup"><span data-stu-id="d9bb7-173">"sasKeyName": "QPolicy", "type": "sharedAccessKey" }, "message": "Some message",</span></span>  
      <span data-ttu-id="d9bb7-174">"brokeredMessageProperties": {}, "customMessageProperties": { "appname": "FromScheduler" } }, "type": "serviceBusQueue" }</span><span class="sxs-lookup"><span data-stu-id="d9bb7-174">"brokeredMessageProperties": {}, "customMessageProperties": { "appname": "FromScheduler" } }, "type": "serviceBusQueue" }</span></span>

<span data-ttu-id="d9bb7-175">hello"errorAction"是 hello 錯誤處理常式，hello hello 主要動作失敗時叫用的動作。</span><span class="sxs-lookup"><span data-stu-id="d9bb7-175">hello “errorAction” is hello error handler, hello action invoked when hello primary action fails.</span></span> <span data-ttu-id="d9bb7-176">您可以使用此變數 toocall 錯誤處理端點，或傳送使用者通知。</span><span class="sxs-lookup"><span data-stu-id="d9bb7-176">You can use this variable toocall an error-handling endpoint or send a user notification.</span></span> <span data-ttu-id="d9bb7-177">這適用於該 hello 達到 hello 案例中的次要端點主要無法使用 （例如，在 hello 案例中損毀 hello 端點的站台時） 或可以用來通知錯誤處理端點。</span><span class="sxs-lookup"><span data-stu-id="d9bb7-177">This can be used for reaching a secondary endpoint in hello case that hello primary is not available (e.g., in hello case of a disaster at hello endpoint’s site) or can be used for notifying an error handling endpoint.</span></span> <span data-ttu-id="d9bb7-178">如同主要動作 hello，hello 錯誤動作可以是根據其他動作的簡單或複合邏輯。</span><span class="sxs-lookup"><span data-stu-id="d9bb7-178">Just like hello primary action, hello error action can be simple or composite logic based on other actions.</span></span> <span data-ttu-id="d9bb7-179">如何 toocreate SAS 權杖，參照太 toolearn[建立和使用共用存取簽章](https://msdn.microsoft.com/library/azure/jj721951.aspx)。</span><span class="sxs-lookup"><span data-stu-id="d9bb7-179">toolearn how toocreate a SAS token, refer too[Create and Use a Shared Access Signature](https://msdn.microsoft.com/library/azure/jj721951.aspx).</span></span>

## <a name="recurrence"></a><span data-ttu-id="d9bb7-180">週期</span><span class="sxs-lookup"><span data-stu-id="d9bb7-180">recurrence</span></span>
<span data-ttu-id="d9bb7-181">週期具有數個部分：</span><span class="sxs-lookup"><span data-stu-id="d9bb7-181">Recurrence has several parts:</span></span>

* <span data-ttu-id="d9bb7-182">頻率：分鐘、小時、天、週、月、年的其中一個</span><span class="sxs-lookup"><span data-stu-id="d9bb7-182">Frequency: One of minute, hour, day, week, month, year</span></span>  
* <span data-ttu-id="d9bb7-183">間隔： Hello 給 hello 循環頻率間隔</span><span class="sxs-lookup"><span data-stu-id="d9bb7-183">Interval: Interval at hello given frequency for hello recurrence</span></span>  
* <span data-ttu-id="d9bb7-184">指定的排程： 指定分鐘、 小時、 工作日、 月和間 hello 循環</span><span class="sxs-lookup"><span data-stu-id="d9bb7-184">Prescribed schedule: Specify minutes, hours, weekdays, months, and monthdays of hello recurrence</span></span>  
* <span data-ttu-id="d9bb7-185">計數：週期的計數</span><span class="sxs-lookup"><span data-stu-id="d9bb7-185">Count: Count of occurrences</span></span>  
* <span data-ttu-id="d9bb7-186">結束時間： hello 指定結束時間之後，會執行任何工作</span><span class="sxs-lookup"><span data-stu-id="d9bb7-186">End time: No jobs will execute after hello specified end time</span></span>  

<span data-ttu-id="d9bb7-187">如果工作已在其 JSON 定義中指定週期物件，則工作會重複執行。</span><span class="sxs-lookup"><span data-stu-id="d9bb7-187">A job is recurring if it has a recurring object specified in its JSON definition.</span></span> <span data-ttu-id="d9bb7-188">如果指定 count 和 endTime，被採用先發生的 hello 完成規則。</span><span class="sxs-lookup"><span data-stu-id="d9bb7-188">If both count and endTime are specified, hello completion rule that occurs first is honored.</span></span>

## <a name="state"></a><span data-ttu-id="d9bb7-189">state</span><span class="sxs-lookup"><span data-stu-id="d9bb7-189">state</span></span>
<span data-ttu-id="d9bb7-190">hello hello 工作狀態是四個值之一： 啟用、 停用、 已完成，或是發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="d9bb7-190">hello state of hello job is one of four values: enabled, disabled, completed, or faulted.</span></span> <span data-ttu-id="d9bb7-191">您可以放入或修補程式的工作，為 tooupdate 它們 toohello 啟用或停用狀態。</span><span class="sxs-lookup"><span data-stu-id="d9bb7-191">You can PUT or PATCH jobs so as tooupdate them toohello enabled or disabled state.</span></span> <span data-ttu-id="d9bb7-192">如果作業已完成或發生錯誤，也就是最後的狀態，無法更新 （但仍可刪除 hello 作業）。</span><span class="sxs-lookup"><span data-stu-id="d9bb7-192">If a job has been completed or faulted, that is a final state that cannot be updated (though hello job can still be DELETED).</span></span> <span data-ttu-id="d9bb7-193">Hello 狀態屬性的範例如下所示：</span><span class="sxs-lookup"><span data-stu-id="d9bb7-193">An example of hello state property is as follows:</span></span>

        "state": "disabled", // enabled, disabled, completed, or faulted
<span data-ttu-id="d9bb7-194">已完成和發生錯誤的工作會在 60 天後刪除。</span><span class="sxs-lookup"><span data-stu-id="d9bb7-194">Completed and faulted jobs are deleted after 60 days.</span></span>

## <a name="status"></a><span data-ttu-id="d9bb7-195">status</span><span class="sxs-lookup"><span data-stu-id="d9bb7-195">status</span></span>
<span data-ttu-id="d9bb7-196">排程器工作啟動之後，將會傳回 hello hello 工作目前狀態的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="d9bb7-196">Once a Scheduler job has started, information will be returned about hello current status of hello job.</span></span> <span data-ttu-id="d9bb7-197">此物件不是由 hello 使用者可設定 — hello 系統設定。</span><span class="sxs-lookup"><span data-stu-id="d9bb7-197">This object is not settable by hello user—it’s set by hello system.</span></span> <span data-ttu-id="d9bb7-198">不過，它包含在 hello 工作物件 （而非個別連結的資源），使其中一個可以輕鬆地取得 hello 工作的狀態。</span><span class="sxs-lookup"><span data-stu-id="d9bb7-198">However, it is included in hello job object (rather than a separate linked resource) so that one can obtain hello status of a job easily.</span></span>

<span data-ttu-id="d9bb7-199">工作狀態包含 hello hello 先前執行時 （如果有的話），hello hello 下一個排程的執行 （適用於進行中作業） 的時間與 hello 作業 hello 執行計數。</span><span class="sxs-lookup"><span data-stu-id="d9bb7-199">Job status includes hello time of hello previous execution (if any), hello time of hello next scheduled execution (for in-progress jobs), and hello execution count of hello job.</span></span>

## <a name="retrypolicy"></a><span data-ttu-id="d9bb7-200">RetryPolicy</span><span class="sxs-lookup"><span data-stu-id="d9bb7-200">retryPolicy</span></span>
<span data-ttu-id="d9bb7-201">如果排程器工作失敗，則可能 toospecify 是否及如何 hello 動作重試一次重試原則 toodetermine。</span><span class="sxs-lookup"><span data-stu-id="d9bb7-201">If a Scheduler job fails, it is possible toospecify a retry policy toodetermine whether and how hello action is retried.</span></span> <span data-ttu-id="d9bb7-202">這由 hello **retryType**物件 — 設定得**無**如果沒有重試原則，如上所示。</span><span class="sxs-lookup"><span data-stu-id="d9bb7-202">This is determined by hello **retryType** object—it is set too**none** if there is no retry policy, as shown above.</span></span> <span data-ttu-id="d9bb7-203">設定得**固定**如果重試原則。</span><span class="sxs-lookup"><span data-stu-id="d9bb7-203">Set it too**fixed** if there is a retry policy.</span></span>

<span data-ttu-id="d9bb7-204">tooset 重試原則，可指定其他兩個設定： 重試間隔 (**retryInterval**) 和 hello 重試次數 (**retryCount**)。</span><span class="sxs-lookup"><span data-stu-id="d9bb7-204">tooset a retry policy, two additional settings may be specified: a retry interval (**retryInterval**) and hello number of retries (**retryCount**).</span></span>

<span data-ttu-id="d9bb7-205">指定以 hello 的 hello 重試間隔**retryInterval**物件，為 hello 重試間隔。</span><span class="sxs-lookup"><span data-stu-id="d9bb7-205">hello retry interval, specified with hello **retryInterval** object, is hello interval between retries.</span></span> <span data-ttu-id="d9bb7-206">其預設值為 30 秒、最小可設定值為 15 秒，而最大值為 18 個月。</span><span class="sxs-lookup"><span data-stu-id="d9bb7-206">Its default value is 30 seconds, its minimum configurable value is 15 seconds, and its maximum value is 18 months.</span></span> <span data-ttu-id="d9bb7-207">免費作業集合中作業的最小可設定值為 1 小時。</span><span class="sxs-lookup"><span data-stu-id="d9bb7-207">Jobs in Free job collections have a minimum configurable value of 1 hour.</span></span>  <span data-ttu-id="d9bb7-208">它被定義在 hello ISO 8601 格式。</span><span class="sxs-lookup"><span data-stu-id="d9bb7-208">It is defined in hello ISO 8601 format.</span></span> <span data-ttu-id="d9bb7-209">同樣地，指定 hello hello 重試次數值，以 hello **retryCount**物件; 它是嘗試重試的 hello 次數。</span><span class="sxs-lookup"><span data-stu-id="d9bb7-209">Similarly, hello value of hello number of retries is specified with hello **retryCount** object; it is hello number of times a retry is attempted.</span></span> <span data-ttu-id="d9bb7-210">其預設值為 4，且其最大值 20\。</span><span class="sxs-lookup"><span data-stu-id="d9bb7-210">Its default value is 4, and its maximum value is 20\.</span></span> <span data-ttu-id="d9bb7-211">同時**retryInterval**和**retryCount**是選擇性的。</span><span class="sxs-lookup"><span data-stu-id="d9bb7-211">Both **retryInterval** and **retryCount** are optional.</span></span> <span data-ttu-id="d9bb7-212">如果會指定其預設值**retryType**設定得**固定**和明確指定任何值。</span><span class="sxs-lookup"><span data-stu-id="d9bb7-212">They are given their default values if **retryType** is set too**fixed** and no values are specified explicitly.</span></span>

## <a name="see-also"></a><span data-ttu-id="d9bb7-213">另請參閱</span><span class="sxs-lookup"><span data-stu-id="d9bb7-213">See also</span></span>
 [<span data-ttu-id="d9bb7-214">排程器是什麼？</span><span class="sxs-lookup"><span data-stu-id="d9bb7-214">What is Scheduler?</span></span>](scheduler-intro.md)

 [<span data-ttu-id="d9bb7-215">開始在 hello Azure 入口網站中使用排程器</span><span class="sxs-lookup"><span data-stu-id="d9bb7-215">Get started using Scheduler in hello Azure portal</span></span>](scheduler-get-started-portal.md)

 [<span data-ttu-id="d9bb7-216">Azure 排程器的計劃和計費</span><span class="sxs-lookup"><span data-stu-id="d9bb7-216">Plans and billing in Azure Scheduler</span></span>](scheduler-plans-billing.md)

 [<span data-ttu-id="d9bb7-217">排程 toobuild 複雜的方式與進階循環使用 Azure 排程器</span><span class="sxs-lookup"><span data-stu-id="d9bb7-217">How toobuild complex schedules and advanced recurrence with Azure Scheduler</span></span>](scheduler-advanced-complexity.md)

 [<span data-ttu-id="d9bb7-218">Azure 排程器 REST API 參考</span><span class="sxs-lookup"><span data-stu-id="d9bb7-218">Azure Scheduler REST API reference</span></span>](https://msdn.microsoft.com/library/mt629143)

 [<span data-ttu-id="d9bb7-219">Azure 排程器 PowerShell Cmdlet 參考</span><span class="sxs-lookup"><span data-stu-id="d9bb7-219">Azure Scheduler PowerShell cmdlets reference</span></span>](scheduler-powershell-reference.md)

 [<span data-ttu-id="d9bb7-220">Azure 排程器高可用性和可靠性</span><span class="sxs-lookup"><span data-stu-id="d9bb7-220">Azure Scheduler high-availability and reliability</span></span>](scheduler-high-availability-reliability.md)

 [<span data-ttu-id="d9bb7-221">Azure 排程器限制、預設值和錯誤碼</span><span class="sxs-lookup"><span data-stu-id="d9bb7-221">Azure Scheduler limits, defaults, and error codes</span></span>](scheduler-limits-defaults-errors.md)

 [<span data-ttu-id="d9bb7-222">Azure 排程器輸出驗證</span><span class="sxs-lookup"><span data-stu-id="d9bb7-222">Azure Scheduler outbound authentication</span></span>](scheduler-outbound-authentication.md)

