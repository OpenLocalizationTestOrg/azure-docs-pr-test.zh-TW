---
title: "設計有效率的清單查詢 - Azure Batch | Microsoft Docs"
description: "藉由在要求集區、作業、工作和計算節點等 Batch 資源的資訊時篩選查詢，以提高效能。"
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
ms.assetid: 031fefeb-248e-4d5a-9bc2-f07e46ddd30d
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 08/02/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a80b207f591bd888d4749287527013c5e554fb6e
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="create-queries-to-list-batch-resources-efficiently"></a><span data-ttu-id="504b2-103">建立查詢以便有效率地列出 Batch 資源</span><span class="sxs-lookup"><span data-stu-id="504b2-103">Create queries to list Batch resources efficiently</span></span>

<span data-ttu-id="504b2-104">在此您將了解如何透過減少在使用 [Batch .NET][api_net] 程式庫查詢作業、工作和計算節點時所傳回的資料量，增加 Azure Batch 應用程式的效能。</span><span class="sxs-lookup"><span data-stu-id="504b2-104">Here you'll learn how to increase your Azure Batch application's performance by reducing the amount of data that is returned by the service when you query jobs, tasks, and compute nodes with the [Batch .NET][api_net] library.</span></span>

<span data-ttu-id="504b2-105">幾乎所有 Batch 應用程式都必須執行某種類型的監視或其他查詢 Batch 服務的作業，並且通常是定期執行。</span><span class="sxs-lookup"><span data-stu-id="504b2-105">Nearly all Batch applications need to perform some type of monitoring or other operation that queries the Batch service, often at regular intervals.</span></span> <span data-ttu-id="504b2-106">例如，若要判斷作業中是否有任何剩餘的已排入佇列的工作，您必須取得作業內每項工作的資料。</span><span class="sxs-lookup"><span data-stu-id="504b2-106">For example, to determine whether there are any queued tasks remaining in a job, you must get data on every task in the job.</span></span> <span data-ttu-id="504b2-107">若要判斷集區中節點的狀態，您必須取得集區中每個節點的資料。</span><span class="sxs-lookup"><span data-stu-id="504b2-107">To determine the status of nodes in your pool, you must get data on every node in the pool.</span></span> <span data-ttu-id="504b2-108">這篇文章說明如何以最有效率的方式執行這類查詢。</span><span class="sxs-lookup"><span data-stu-id="504b2-108">This article explains how to execute such queries in the most efficient way.</span></span>

> [!NOTE]
> <span data-ttu-id="504b2-109">Batch 服務會針對計算作業中工作的常見案例，提供特殊的 API 支援。</span><span class="sxs-lookup"><span data-stu-id="504b2-109">The Batch service provides special API support for the common scenario of counting tasks in a job.</span></span> <span data-ttu-id="504b2-110">您可以呼叫[取得工作計數][rest_get_task_counts]作業，而非使用清單查詢。</span><span class="sxs-lookup"><span data-stu-id="504b2-110">Instead of using a list query for these, you can call the [Get Task Counts][rest_get_task_counts] operation.</span></span> <span data-ttu-id="504b2-111">「取得工作計數」會指出多少工作擱置中、執行中或已完成，以及有多少工作成功或失敗。</span><span class="sxs-lookup"><span data-stu-id="504b2-111">Get Task Counts indicates how many tasks are pending, running or complete, and how many tasks have succeeded or failed.</span></span> <span data-ttu-id="504b2-112">「取得工作計數」比清單查詢更有效率。</span><span class="sxs-lookup"><span data-stu-id="504b2-112">Get Task Counts is more efficient than a list query.</span></span> <span data-ttu-id="504b2-113">如需詳細資訊，請參閱[依狀態計算作業的工作 (預覽)](batch-get-task-counts.md)。</span><span class="sxs-lookup"><span data-stu-id="504b2-113">For more information, see [Count tasks for a job by state (Preview)](batch-get-task-counts.md).</span></span> 
>
> <span data-ttu-id="504b2-114">「取得工作計數」作業不適用於早於 2017-06-01.5.1 的 Batch 服務版本。</span><span class="sxs-lookup"><span data-stu-id="504b2-114">The Get Task Counts operation is not available in Batch service versions earlier than 2017-06-01.5.1.</span></span> <span data-ttu-id="504b2-115">如果您使用舊版的服務，則改用清單查詢來計算作業中的工作。</span><span class="sxs-lookup"><span data-stu-id="504b2-115">If you are using an older version of the service, then use a list query to count tasks in a job instead.</span></span>
>
> 

## <a name="meet-the-detaillevel"></a><span data-ttu-id="504b2-116">認識 DetailLevel</span><span class="sxs-lookup"><span data-stu-id="504b2-116">Meet the DetailLevel</span></span>
<span data-ttu-id="504b2-117">在生產用 Batch 應用程式中，作業、工作和計算節點等實體的數量可能有數千個。</span><span class="sxs-lookup"><span data-stu-id="504b2-117">In a production Batch application, entities like jobs, tasks, and compute nodes can number in the thousands.</span></span> <span data-ttu-id="504b2-118">當您要求這些資源的資訊時，可能會有大量資料必須從 Batch 服務「傳送」到每個查詢上的應用程式。</span><span class="sxs-lookup"><span data-stu-id="504b2-118">When you request information on these resources, a potentially large amount of data must "cross the wire" from the Batch service to your application on each query.</span></span> <span data-ttu-id="504b2-119">透過限制項目數量及查詢所傳回的資訊類型，您可以加速查詢，因而提高應用程式的效能。</span><span class="sxs-lookup"><span data-stu-id="504b2-119">By limiting the number of items and type of information that is returned by a query, you can increase the speed of your queries, and therefore the performance of your application.</span></span>

<span data-ttu-id="504b2-120">此 [Batch .NET][api_net] API 程式碼片段會列出與作業相關聯的「每一項」工作，以及各工作的「所有」屬性：</span><span class="sxs-lookup"><span data-stu-id="504b2-120">This [Batch .NET][api_net] API code snippet lists *every* task that is associated with a job, along with *all* of the properties of each task:</span></span>

```csharp
// Get a collection of all of the tasks and all of their properties for job-001
IPagedEnumerable<CloudTask> allTasks =
    batchClient.JobOperations.ListTasks("job-001");
```

<span data-ttu-id="504b2-121">不過，您可以藉由對查詢套用「詳細資料層級」，以進行更有效率的清單查詢。</span><span class="sxs-lookup"><span data-stu-id="504b2-121">You can perform a much more efficient list query, however, by applying a "detail level" to your query.</span></span> <span data-ttu-id="504b2-122">在 [JobOperations.ListTasks][net_list_tasks] 方法中提供 [ODATADetailLevel][odata] 物件即可執行此動作。</span><span class="sxs-lookup"><span data-stu-id="504b2-122">You do this by supplying an [ODATADetailLevel][odata] object to the [JobOperations.ListTasks][net_list_tasks] method.</span></span> <span data-ttu-id="504b2-123">此程式碼片段只是傳回已完成之工作的識別碼、命令列和計算節點資訊屬性：</span><span class="sxs-lookup"><span data-stu-id="504b2-123">This snippet returns only the ID, command line, and compute node information properties of completed tasks:</span></span>

```csharp
// Configure an ODATADetailLevel specifying a subset of tasks and
// their properties to return
ODATADetailLevel detailLevel = new ODATADetailLevel();
detailLevel.FilterClause = "state eq 'completed'";
detailLevel.SelectClause = "id,commandLine,nodeInfo";

// Supply the ODATADetailLevel to the ListTasks method
IPagedEnumerable<CloudTask> completedTasks =
    batchClient.JobOperations.ListTasks("job-001", detailLevel);
```

<span data-ttu-id="504b2-124">在此範例案例中，如果作業中有數千個工作，則第二次查詢傳回結果的速度，通常會比第一次快很多。</span><span class="sxs-lookup"><span data-stu-id="504b2-124">In this example scenario, if there are thousands of tasks in the job, the results from the second query will typically be returned much quicker than the first.</span></span> <span data-ttu-id="504b2-125">使用 Batch .NET API 列出項目時，使用 ODATADetailLevel 的詳細資訊如 [下](#efficient-querying-in-batch-net)所示。</span><span class="sxs-lookup"><span data-stu-id="504b2-125">More information about using ODATADetailLevel when you list items with the Batch .NET API is included [below](#efficient-querying-in-batch-net).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="504b2-126">我們強烈建議「一律」在 .NET API 清單呼叫中提供 ODATADetailLevel 物件，以確保應用程式發揮最高效率和效能。</span><span class="sxs-lookup"><span data-stu-id="504b2-126">We highly recommend that you *always* supply an ODATADetailLevel object to your .NET API list calls to ensure maximum efficiency and performance of your application.</span></span> <span data-ttu-id="504b2-127">透過指定詳細層級，您可以幫助縮短 Batch 服務回應時間、提高網路使用率，以及讓用戶端應用程式的記憶體使用量降到最低。</span><span class="sxs-lookup"><span data-stu-id="504b2-127">By specifying a detail level, you can help to lower Batch service response times, improve network utilization, and minimize memory usage by client applications.</span></span>
> 
> 

## <a name="filter-select-and-expand"></a><span data-ttu-id="504b2-128">篩選、選取及展開</span><span class="sxs-lookup"><span data-stu-id="504b2-128">Filter, select, and expand</span></span>
<span data-ttu-id="504b2-129">[Batch .NET][api_net] 和 [Batch REST][api_rest] API 可讓您減少清單中傳回的項目數和每個項目傳回的資訊量。</span><span class="sxs-lookup"><span data-stu-id="504b2-129">The [Batch .NET][api_net] and [Batch REST][api_rest] APIs provide the ability to reduce both the number of items that are returned in a list, as well as the amount of information that is returned for each.</span></span> <span data-ttu-id="504b2-130">您可以藉由在執行清單查詢時指定**篩選**、**選取**和**展開字串**來執行此動作。</span><span class="sxs-lookup"><span data-stu-id="504b2-130">You do so by specifying **filter**, **select**, and **expand strings** when performing list queries.</span></span>

### <a name="filter"></a><span data-ttu-id="504b2-131">Filter</span><span class="sxs-lookup"><span data-stu-id="504b2-131">Filter</span></span>
<span data-ttu-id="504b2-132">篩選字串是可減少傳回的項目數的運算式。</span><span class="sxs-lookup"><span data-stu-id="504b2-132">The filter string is an expression that reduces the number of items that are returned.</span></span> <span data-ttu-id="504b2-133">例如，只列出工作正在執行的作業，或只列出可執行作業的計算節點。</span><span class="sxs-lookup"><span data-stu-id="504b2-133">For example, list only the running tasks for a job, or list only compute nodes that are ready to run tasks.</span></span>

* <span data-ttu-id="504b2-134">篩選字串包含一個或多個運算式，而運算式由屬性名稱、運算子和值構成。</span><span class="sxs-lookup"><span data-stu-id="504b2-134">The filter string consists of one or more expressions, with an expression that consists of a property name, operator, and value.</span></span> <span data-ttu-id="504b2-135">可指定的屬性及每個屬性支援的運算子，取決於您查詢的每個實體類型。</span><span class="sxs-lookup"><span data-stu-id="504b2-135">The properties that can be specified are specific to each entity type that you query, as are the operators that are supported for each property.</span></span>
* <span data-ttu-id="504b2-136">多個運算式可以透過邏輯運算子 `and` 和 `or` 結合。</span><span class="sxs-lookup"><span data-stu-id="504b2-136">Multiple expressions can be combined by using the logical operators `and` and `or`.</span></span>
* <span data-ttu-id="504b2-137">此範例篩選字串只會列出執行中「轉譯」工作： `(state eq 'running') and startswith(id, 'renderTask')`。</span><span class="sxs-lookup"><span data-stu-id="504b2-137">This example filter string lists only the running "render" tasks: `(state eq 'running') and startswith(id, 'renderTask')`.</span></span>

### <a name="select"></a><span data-ttu-id="504b2-138">選取</span><span class="sxs-lookup"><span data-stu-id="504b2-138">Select</span></span>
<span data-ttu-id="504b2-139">選取字串限制每個項目傳回的屬性值。</span><span class="sxs-lookup"><span data-stu-id="504b2-139">The select string limits the property values that are returned for each item.</span></span> <span data-ttu-id="504b2-140">指定屬性名稱的清單，而且查詢結果中只有針對項目傳回的那些屬性值。</span><span class="sxs-lookup"><span data-stu-id="504b2-140">You specify a list of property names, and only those property values are returned for the items in the query results.</span></span>

* <span data-ttu-id="504b2-141">選取字串由屬性名稱的逗號分隔清單組成。</span><span class="sxs-lookup"><span data-stu-id="504b2-141">The select string consists of a comma-separated list of property names.</span></span> <span data-ttu-id="504b2-142">您可以針對查詢的實體類型指定任何屬性。</span><span class="sxs-lookup"><span data-stu-id="504b2-142">You can specify any of the properties for the entity type you are querying.</span></span>
* <span data-ttu-id="504b2-143">此範例選取字串會指定應該針對每個工作只傳回三個屬性： `id, state, stateTransitionTime`。</span><span class="sxs-lookup"><span data-stu-id="504b2-143">This example select string specifies that only three property values should be returned for each task: `id, state, stateTransitionTime`.</span></span>

### <a name="expand"></a><span data-ttu-id="504b2-144">展開</span><span class="sxs-lookup"><span data-stu-id="504b2-144">Expand</span></span>
<span data-ttu-id="504b2-145">展開字串減少取得某些資訊所需的 API 呼叫次數。</span><span class="sxs-lookup"><span data-stu-id="504b2-145">The expand string reduces the number of API calls that are required to obtain certain information.</span></span> <span data-ttu-id="504b2-146">當您使用展開字串時，可以透過單一 API 呼叫取得每個項目的相關詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="504b2-146">When you use an expand string, more information about each item can be obtained with a single API call.</span></span> <span data-ttu-id="504b2-147">不是首先取得實體的清單，然後在清單中要求每個項目的資訊，而是您可以使用展開字串在單一 API 呼叫中取得相同資訊。</span><span class="sxs-lookup"><span data-stu-id="504b2-147">Rather than first obtaining the list of entities, then requesting information for each item in the list, you use an expand string to obtain the same information in a single API call.</span></span> <span data-ttu-id="504b2-148">較少的 API 呼叫表示較佳的效能。</span><span class="sxs-lookup"><span data-stu-id="504b2-148">Less API calls means better performance.</span></span>

* <span data-ttu-id="504b2-149">與選取字串相似，展開字串可以控制清單查詢結果中是否包含特定資料。</span><span class="sxs-lookup"><span data-stu-id="504b2-149">Similar to the select string, the expand string controls whether certain data is included in list query results.</span></span>
* <span data-ttu-id="504b2-150">只有在用於列出作業、作業排程、作業和集區時，才支援展開字串。</span><span class="sxs-lookup"><span data-stu-id="504b2-150">The expand string is only supported when it is used in listing jobs, job schedules, tasks, and pools.</span></span> <span data-ttu-id="504b2-151">目前，它僅支援統計資訊。</span><span class="sxs-lookup"><span data-stu-id="504b2-151">Currently, it only supports statistics information.</span></span>
* <span data-ttu-id="504b2-152">當需要所有屬性但未指定選取字串時， *必須* 使用展開字串來取得統計資料資訊。</span><span class="sxs-lookup"><span data-stu-id="504b2-152">When all properties are required and no select string is specified, the expand string *must* be used to get statistics information.</span></span> <span data-ttu-id="504b2-153">如果使用選取字串來取得屬性子集，則可以在選取字串中指定 `stats` ，不需要指定展開字串。</span><span class="sxs-lookup"><span data-stu-id="504b2-153">If a select string is used to obtain a subset of properties, then `stats` can be specified in the select string, and the expand string does not need to be specified.</span></span>
* <span data-ttu-id="504b2-154">此範例展開字串指定應該在清單中傳回每個項目的統計資料資訊： `stats`。</span><span class="sxs-lookup"><span data-stu-id="504b2-154">This example expand string specifies that statistics information should be returned for each item in the list: `stats`.</span></span>

> [!NOTE]
> <span data-ttu-id="504b2-155">建構任何這三種查詢字串類型時 (篩選、選取和展開)，您必須確定屬性名稱和大小寫符合其對應的 Batch REST API 元素。</span><span class="sxs-lookup"><span data-stu-id="504b2-155">When constructing any of the three query string types (filter, select, and expand), you must ensure that the property names and case match that of their REST API element counterparts.</span></span> <span data-ttu-id="504b2-156">例如，使用 .NET [CloudTask](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask) 類別時，即使 .NET 屬性是 [CloudTask.State](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.state)，也必須指定 **state** 而不是 **State**。</span><span class="sxs-lookup"><span data-stu-id="504b2-156">For example, when working with the .NET [CloudTask](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask) class, you must specify **state** instead of **State**, even though the .NET property is [CloudTask.State](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.state).</span></span> <span data-ttu-id="504b2-157">關於 .NET 和 REST API 之間的屬性對應，請參閱下表。</span><span class="sxs-lookup"><span data-stu-id="504b2-157">See the tables below for property mappings between the .NET and REST APIs.</span></span>
> 
> 

### <a name="rules-for-filter-select-and-expand-strings"></a><span data-ttu-id="504b2-158">篩選、選取和展開字串的規則</span><span class="sxs-lookup"><span data-stu-id="504b2-158">Rules for filter, select, and expand strings</span></span>
* <span data-ttu-id="504b2-159">篩選、選取和展開字串中的屬性名稱，應該和 [Batch REST][api_rest] API 中的屬性名稱一致，就算是使用 [Batch .NET][api_net] 或其他 Batch SDK 的其中一個也是如此。</span><span class="sxs-lookup"><span data-stu-id="504b2-159">Properties names in filter, select, and expand strings should appear as they do in the [Batch REST][api_rest] API--even when you use [Batch .NET][api_net] or one of the other Batch SDKs.</span></span>
* <span data-ttu-id="504b2-160">所有屬性名稱都會區分大小寫，但屬性值不會區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="504b2-160">All property names are case-sensitive, but property values are case insensitive.</span></span>
* <span data-ttu-id="504b2-161">日期/時間字串有兩種格式，開頭必須加上 `DateTime`。</span><span class="sxs-lookup"><span data-stu-id="504b2-161">Date/time strings can be one of two formats, and must be preceded with `DateTime`.</span></span>
  
  * <span data-ttu-id="504b2-162">W3C-DTF 格式範例：`creationTime gt DateTime'2011-05-08T08:49:37Z'`</span><span class="sxs-lookup"><span data-stu-id="504b2-162">W3C-DTF format example: `creationTime gt DateTime'2011-05-08T08:49:37Z'`</span></span>
  * <span data-ttu-id="504b2-163">RFC 1123 格式範例：`creationTime gt DateTime'Sun, 08 May 2011 08:49:37 GMT'`</span><span class="sxs-lookup"><span data-stu-id="504b2-163">RFC 1123 format example: `creationTime gt DateTime'Sun, 08 May 2011 08:49:37 GMT'`</span></span>
* <span data-ttu-id="504b2-164">布林值字串為 `true` 或 `false`。</span><span class="sxs-lookup"><span data-stu-id="504b2-164">Boolean strings are either `true` or `false`.</span></span>
* <span data-ttu-id="504b2-165">如果指定無效的屬性或運算子，將會導致 `400 (Bad Request)` 錯誤。</span><span class="sxs-lookup"><span data-stu-id="504b2-165">If an invalid property or operator is specified, a `400 (Bad Request)` error will result.</span></span>

## <a name="efficient-querying-in-batch-net"></a><span data-ttu-id="504b2-166">在 Batch .NET 中有效率地查詢</span><span class="sxs-lookup"><span data-stu-id="504b2-166">Efficient querying in Batch .NET</span></span>
<span data-ttu-id="504b2-167">在 [Batch .NET][api_net] API 內，[ODATADetailLevel][odata] 類別用來提供篩選、選取和展開字串給清單作業。</span><span class="sxs-lookup"><span data-stu-id="504b2-167">Within the [Batch .NET][api_net] API, the [ODATADetailLevel][odata] class is used for supplying filter, select, and expand strings to list operations.</span></span> <span data-ttu-id="504b2-168">ODataDetailLevel 物件有三個公用字串屬性，可以在建構函式中指定或是直接在物件上設定。</span><span class="sxs-lookup"><span data-stu-id="504b2-168">The ODataDetailLevel class has three public string properties that can be specified in the constructor, or set directly on the object.</span></span> <span data-ttu-id="504b2-169">然後您可以將 ODataDetailLevel 物件當做參數傳給各種清單作業，例如 [ListPools][net_list_pools]、[ListJobs][net_list_jobs] 和 [ListTasks][net_list_tasks]。</span><span class="sxs-lookup"><span data-stu-id="504b2-169">You then pass the ODataDetailLevel object as a parameter to the various list operations such as [ListPools][net_list_pools], [ListJobs][net_list_jobs], and [ListTasks][net_list_tasks].</span></span>

* <span data-ttu-id="504b2-170">[ODATADetailLevel][odata].[FilterClause][odata_filter]：限制傳回的項目數。</span><span class="sxs-lookup"><span data-stu-id="504b2-170">[ODATADetailLevel][odata].[FilterClause][odata_filter]: Limit the number of items that are returned.</span></span>
* <span data-ttu-id="504b2-171">[ODATADetailLevel][odata].[SelectClause][odata_select]：指定隨著每個項目一起傳回的屬性值。</span><span class="sxs-lookup"><span data-stu-id="504b2-171">[ODATADetailLevel][odata].[SelectClause][odata_select]: Specify which property values are returned with each item.</span></span>
* <span data-ttu-id="504b2-172">[ODATADetailLevel][odata].[ExpandClause][odata_expand]：在單一 API 呼叫中擷取所有項目的資料，而不是針對每個項目個別呼叫。</span><span class="sxs-lookup"><span data-stu-id="504b2-172">[ODATADetailLevel][odata].[ExpandClause][odata_expand]: Retrieve data for all items in a single API call instead of separate calls for each item.</span></span>

<span data-ttu-id="504b2-173">下列程式碼片段使用 Batch .NET API，有效率地向 Batch 服務查詢一組特定集區的統計資料。</span><span class="sxs-lookup"><span data-stu-id="504b2-173">The following code snippet uses the Batch .NET API to efficiently query the Batch service for the statistics of a specific set of pools.</span></span> <span data-ttu-id="504b2-174">在此案例中，Batch 使用者具有測試與生產的集區。</span><span class="sxs-lookup"><span data-stu-id="504b2-174">In this scenario, the Batch user has both test and production pools.</span></span> <span data-ttu-id="504b2-175">這些測試集區識別碼前面會加上 "test"，而生產集區識別碼則會加上 "prod"。</span><span class="sxs-lookup"><span data-stu-id="504b2-175">The test pool IDs are prefixed with "test", and the production pool IDs are prefixed with "prod".</span></span> <span data-ttu-id="504b2-176">在程式碼片段中，「myBatchClient」  是適當初始化的 [BatchClient](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.batchclient) 類別的執行個體。</span><span class="sxs-lookup"><span data-stu-id="504b2-176">In the snippet, *myBatchClient* is a properly initialized instance of the [BatchClient](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.batchclient) class.</span></span>

```csharp
// First we need an ODATADetailLevel instance on which to set the filter, select,
// and expand clause strings
ODATADetailLevel detailLevel = new ODATADetailLevel();

// We want to pull only the "test" pools, so we limit the number of items returned
// by using a FilterClause and specifying that the pool IDs must start with "test"
detailLevel.FilterClause = "startswith(id, 'test')";

// To further limit the data that crosses the wire, configure the SelectClause to
// limit the properties that are returned on each CloudPool object to only
// CloudPool.Id and CloudPool.Statistics
detailLevel.SelectClause = "id, stats";

// Specify the ExpandClause so that the .NET API pulls the statistics for the
// CloudPools in a single underlying REST API call. Note that we use the pool's
// REST API element name "stats" here as opposed to "Statistics" as it appears in
// the .NET API (CloudPool.Statistics)
detailLevel.ExpandClause = "stats";

// Now get our collection of pools, minimizing the amount of data that is returned
// by specifying the detail level that we configured above
List<CloudPool> testPools =
    await myBatchClient.PoolOperations.ListPools(detailLevel).ToListAsync();
```

> [!TIP]
> <span data-ttu-id="504b2-177">使用「選取」和「展開」子句設定的 [ODATADetailLevel][odata] 執行個體，也可以傳給適當的 Get 方法，例如 [PoolOperations.GetPool](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.getpool.aspx)，以限制傳回的資料量。</span><span class="sxs-lookup"><span data-stu-id="504b2-177">An instance of [ODATADetailLevel][odata] that is configured with Select and Expand clauses can also be passed to appropriate Get methods, such as [PoolOperations.GetPool](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.getpool.aspx), to limit the amount of data that is returned.</span></span>
> 
> 

## <a name="batch-rest-to-net-api-mappings"></a><span data-ttu-id="504b2-178">Batch REST 與 .NET API 的對應</span><span class="sxs-lookup"><span data-stu-id="504b2-178">Batch REST to .NET API mappings</span></span>
<span data-ttu-id="504b2-179">篩選、選取和展開字串中的屬性名稱在名稱和大小寫方面， *必須* 反映其 REST API 對應項目。</span><span class="sxs-lookup"><span data-stu-id="504b2-179">Property names in filter, select, and expand strings *must* reflect their REST API counterparts, both in name and case.</span></span> <span data-ttu-id="504b2-180">下表提供 .NET 和 REST API 對應項目之間的對應。</span><span class="sxs-lookup"><span data-stu-id="504b2-180">The tables below provide mappings between the .NET and REST API counterparts.</span></span>

### <a name="mappings-for-filter-strings"></a><span data-ttu-id="504b2-181">篩選字串的對應</span><span class="sxs-lookup"><span data-stu-id="504b2-181">Mappings for filter strings</span></span>
* <span data-ttu-id="504b2-182">**.NET 清單方法**：此欄的每個 .NET API 方法都接受 [ODATADetailLevel][odata] 物件作為參數。</span><span class="sxs-lookup"><span data-stu-id="504b2-182">**.NET list methods**: Each of the .NET API methods in this column accepts an [ODATADetailLevel][odata] object as a parameter.</span></span>
* <span data-ttu-id="504b2-183">**REST 清單要求**：此資料行的每個 REST API 頁面都連結至一個資料表，其中指定「篩選」字串中允許的屬性和作業。</span><span class="sxs-lookup"><span data-stu-id="504b2-183">**REST list requests**: Each REST API page linked to in this column contains a table that specifies the properties and operations that are allowed in *filter* strings.</span></span> <span data-ttu-id="504b2-184">建構 [ODATADetailLevel.FilterClause][odata_filter] 字串時會使用這些屬性名稱和作業。</span><span class="sxs-lookup"><span data-stu-id="504b2-184">You will use these property names and operations when you construct an [ODATADetailLevel.FilterClause][odata_filter] string.</span></span>

| <span data-ttu-id="504b2-185">.NET 清單方法</span><span class="sxs-lookup"><span data-stu-id="504b2-185">.NET list methods</span></span> | <span data-ttu-id="504b2-186">REST 清單要求</span><span class="sxs-lookup"><span data-stu-id="504b2-186">REST list requests</span></span> |
| --- | --- |
| <span data-ttu-id="504b2-187">[CertificateOperations.ListCertificates][net_list_certs]</span><span class="sxs-lookup"><span data-stu-id="504b2-187">[CertificateOperations.ListCertificates][net_list_certs]</span></span> |<span data-ttu-id="504b2-188">[列出帳戶中的憑證][rest_list_certs]</span><span class="sxs-lookup"><span data-stu-id="504b2-188">[List the certificates in an account][rest_list_certs]</span></span> |
| <span data-ttu-id="504b2-189">[CloudTask.ListNodeFiles][net_list_task_files]</span><span class="sxs-lookup"><span data-stu-id="504b2-189">[CloudTask.ListNodeFiles][net_list_task_files]</span></span> |<span data-ttu-id="504b2-190">[列出與作業相關聯的檔案][rest_list_task_files]</span><span class="sxs-lookup"><span data-stu-id="504b2-190">[List the files associated with a task][rest_list_task_files]</span></span> |
| <span data-ttu-id="504b2-191">[JobOperations.ListJobPreparationAndReleaseTaskStatus][net_list_jobprep_status]</span><span class="sxs-lookup"><span data-stu-id="504b2-191">[JobOperations.ListJobPreparationAndReleaseTaskStatus][net_list_jobprep_status]</span></span> |<span data-ttu-id="504b2-192">[列出作業準備和工作解除作業的狀態][rest_list_jobprep_status]</span><span class="sxs-lookup"><span data-stu-id="504b2-192">[List the status of the job preparation and job release tasks for a job][rest_list_jobprep_status]</span></span> |
| <span data-ttu-id="504b2-193">[JobOperations.ListJobs][net_list_jobs]</span><span class="sxs-lookup"><span data-stu-id="504b2-193">[JobOperations.ListJobs][net_list_jobs]</span></span> |<span data-ttu-id="504b2-194">[列出帳戶中的作業][rest_list_jobs]</span><span class="sxs-lookup"><span data-stu-id="504b2-194">[List the jobs in an account][rest_list_jobs]</span></span> |
| <span data-ttu-id="504b2-195">[JobOperations.ListNodeFiles][net_list_nodefiles]</span><span class="sxs-lookup"><span data-stu-id="504b2-195">[JobOperations.ListNodeFiles][net_list_nodefiles]</span></span> |<span data-ttu-id="504b2-196">[列出節點上的檔案][rest_list_nodefiles]</span><span class="sxs-lookup"><span data-stu-id="504b2-196">[List the files on a node][rest_list_nodefiles]</span></span> |
| <span data-ttu-id="504b2-197">[JobOperations.ListTasks][net_list_tasks]</span><span class="sxs-lookup"><span data-stu-id="504b2-197">[JobOperations.ListTasks][net_list_tasks]</span></span> |<span data-ttu-id="504b2-198">[列出與工作相關聯的作業][rest_list_tasks]</span><span class="sxs-lookup"><span data-stu-id="504b2-198">[List the tasks associated with a job][rest_list_tasks]</span></span> |
| <span data-ttu-id="504b2-199">[JobScheduleOperations.ListJobSchedules][net_list_job_schedules]</span><span class="sxs-lookup"><span data-stu-id="504b2-199">[JobScheduleOperations.ListJobSchedules][net_list_job_schedules]</span></span> |<span data-ttu-id="504b2-200">[列出帳戶中的作業排程][rest_list_job_schedules]</span><span class="sxs-lookup"><span data-stu-id="504b2-200">[List the job schedules in an account][rest_list_job_schedules]</span></span> |
| <span data-ttu-id="504b2-201">[JobScheduleOperations.ListJobs][net_list_schedule_jobs]</span><span class="sxs-lookup"><span data-stu-id="504b2-201">[JobScheduleOperations.ListJobs][net_list_schedule_jobs]</span></span> |<span data-ttu-id="504b2-202">[列出與作業排程相關聯的作業][rest_list_schedule_jobs]</span><span class="sxs-lookup"><span data-stu-id="504b2-202">[List the jobs associated with a job schedule][rest_list_schedule_jobs]</span></span> |
| <span data-ttu-id="504b2-203">[PoolOperations.ListComputeNodes][net_list_compute_nodes]</span><span class="sxs-lookup"><span data-stu-id="504b2-203">[PoolOperations.ListComputeNodes][net_list_compute_nodes]</span></span> |<span data-ttu-id="504b2-204">[列出集區中的運算節點][rest_list_compute_nodes]</span><span class="sxs-lookup"><span data-stu-id="504b2-204">[List the compute nodes in a pool][rest_list_compute_nodes]</span></span> |
| <span data-ttu-id="504b2-205">[PoolOperations.ListPools][net_list_pools]</span><span class="sxs-lookup"><span data-stu-id="504b2-205">[PoolOperations.ListPools][net_list_pools]</span></span> |<span data-ttu-id="504b2-206">[列出帳戶中的集區][rest_list_pools]</span><span class="sxs-lookup"><span data-stu-id="504b2-206">[List the pools in an account][rest_list_pools]</span></span> |

### <a name="mappings-for-select-strings"></a><span data-ttu-id="504b2-207">選取字串的對應</span><span class="sxs-lookup"><span data-stu-id="504b2-207">Mappings for select strings</span></span>
* <span data-ttu-id="504b2-208">**Batch .NET types**：Batch .NET API 類型。</span><span class="sxs-lookup"><span data-stu-id="504b2-208">**Batch .NET types**: Batch .NET API types.</span></span>
* <span data-ttu-id="504b2-209">**REST API entities**：此資料行中的每個頁面包含一個或多個資料表，其中列出類型的 REST API 屬性名稱。</span><span class="sxs-lookup"><span data-stu-id="504b2-209">**REST API entities**: Each page in this column contains one or more tables that list the REST API property names for the type.</span></span> <span data-ttu-id="504b2-210">建構「選取」  字串時會使用這些屬性名稱。</span><span class="sxs-lookup"><span data-stu-id="504b2-210">These property names are used when you construct *select* strings.</span></span> <span data-ttu-id="504b2-211">建構 [ODATADetailLevel.SelectClause][odata_select] 字串時會使用這些相同的屬性名稱。</span><span class="sxs-lookup"><span data-stu-id="504b2-211">You will use these same property names when you construct an [ODATADetailLevel.SelectClause][odata_select] string.</span></span>

| <span data-ttu-id="504b2-212">Batch .NET types</span><span class="sxs-lookup"><span data-stu-id="504b2-212">Batch .NET types</span></span> | <span data-ttu-id="504b2-213">REST API entities</span><span class="sxs-lookup"><span data-stu-id="504b2-213">REST API entities</span></span> |
| --- | --- |
| <span data-ttu-id="504b2-214">[憑證][net_cert]</span><span class="sxs-lookup"><span data-stu-id="504b2-214">[Certificate][net_cert]</span></span> |<span data-ttu-id="504b2-215">[取得憑證的相關資訊][rest_get_cert]</span><span class="sxs-lookup"><span data-stu-id="504b2-215">[Get information about a certificate][rest_get_cert]</span></span> |
| <span data-ttu-id="504b2-216">[CloudJob][net_job]</span><span class="sxs-lookup"><span data-stu-id="504b2-216">[CloudJob][net_job]</span></span> |<span data-ttu-id="504b2-217">[取得作業的相關資訊][rest_get_job]</span><span class="sxs-lookup"><span data-stu-id="504b2-217">[Get information about a job][rest_get_job]</span></span> |
| <span data-ttu-id="504b2-218">[CloudJobSchedule][net_schedule]</span><span class="sxs-lookup"><span data-stu-id="504b2-218">[CloudJobSchedule][net_schedule]</span></span> |<span data-ttu-id="504b2-219">[取得作業排程的相關資訊][rest_get_schedule]</span><span class="sxs-lookup"><span data-stu-id="504b2-219">[Get information about a job schedule][rest_get_schedule]</span></span> |
| <span data-ttu-id="504b2-220">[ComputeNode][net_node]</span><span class="sxs-lookup"><span data-stu-id="504b2-220">[ComputeNode][net_node]</span></span> |<span data-ttu-id="504b2-221">[取得節點的相關資訊][rest_get_node]</span><span class="sxs-lookup"><span data-stu-id="504b2-221">[Get information about a node][rest_get_node]</span></span> |
| <span data-ttu-id="504b2-222">[CloudPool][net_pool]</span><span class="sxs-lookup"><span data-stu-id="504b2-222">[CloudPool][net_pool]</span></span> |<span data-ttu-id="504b2-223">[取得集區的相關資訊][rest_get_pool]</span><span class="sxs-lookup"><span data-stu-id="504b2-223">[Get information about a pool][rest_get_pool]</span></span> |
| <span data-ttu-id="504b2-224">[CloudTask][net_task]</span><span class="sxs-lookup"><span data-stu-id="504b2-224">[CloudTask][net_task]</span></span> |<span data-ttu-id="504b2-225">[取得作業的相關資訊][rest_get_task]</span><span class="sxs-lookup"><span data-stu-id="504b2-225">[Get information about a task][rest_get_task]</span></span> |

## <a name="example-construct-a-filter-string"></a><span data-ttu-id="504b2-226">範例：建構篩選字串</span><span class="sxs-lookup"><span data-stu-id="504b2-226">Example: construct a filter string</span></span>
<span data-ttu-id="504b2-227">建構 [ODATADetailLevel.FilterClause][odata_filter] 的篩選字串時，請參閱「篩選字串的對應」下方的資料表，找出與您想要執行的清單作業相對應的 REST API 文件頁面。</span><span class="sxs-lookup"><span data-stu-id="504b2-227">When you construct a filter string for [ODATADetailLevel.FilterClause][odata_filter], consult the table above under "Mappings for filter strings" to find the REST API documentation page that corresponds to the list operation that you wish to perform.</span></span> <span data-ttu-id="504b2-228">在該頁面的第一個含有多資料列的資料表中，您可以找到可篩選的屬性及其支援的運算子。</span><span class="sxs-lookup"><span data-stu-id="504b2-228">You will find the filterable properties and their supported operators in the first multirow table on that page.</span></span> <span data-ttu-id="504b2-229">假設您想要擷取結束碼不為零的所有作業，[與作業相關聯的清單作業][rest_list_tasks]中的這一列指定適用的屬性字串和允許的運算子：</span><span class="sxs-lookup"><span data-stu-id="504b2-229">If you wish to retrieve all tasks whose exit code was nonzero, for example, this row on [List the tasks associated with a job][rest_list_tasks] specifies the applicable property string and allowable operators:</span></span>

| <span data-ttu-id="504b2-230">屬性</span><span class="sxs-lookup"><span data-stu-id="504b2-230">Property</span></span> | <span data-ttu-id="504b2-231">允許的作業</span><span class="sxs-lookup"><span data-stu-id="504b2-231">Operations allowed</span></span> | <span data-ttu-id="504b2-232">類型</span><span class="sxs-lookup"><span data-stu-id="504b2-232">Type</span></span> |
|:--- |:--- |:--- |
| `executionInfo/exitCode` |`eq, ge, gt, le , lt` |`Int` |

<span data-ttu-id="504b2-233">因此，為了列出具有非零結束碼的所有作業，篩選字串如下：</span><span class="sxs-lookup"><span data-stu-id="504b2-233">Thus, the filter string for listing all tasks with a nonzero exit code would be:</span></span>

`(executionInfo/exitCode lt 0) or (executionInfo/exitCode gt 0)`

## <a name="example-construct-a-select-string"></a><span data-ttu-id="504b2-234">範例：建構選取字串</span><span class="sxs-lookup"><span data-stu-id="504b2-234">Example: construct a select string</span></span>
<span data-ttu-id="504b2-235">如果要建構 [ODATADetailLevel.SelectClause][odata_select]，請參閱「選取字串的對應」下方的資料表，瀏覽至與您要列出的實體類型相對應的 REST API 頁面。</span><span class="sxs-lookup"><span data-stu-id="504b2-235">To construct [ODATADetailLevel.SelectClause][odata_select], consult the table above under "Mappings for select strings" and navigate to the REST API page that corresponds to the type of entity that you are listing.</span></span> <span data-ttu-id="504b2-236">在該頁面的第一個含有多資料列的資料表中，您可以找到可選取的屬性及其支援的運算子。</span><span class="sxs-lookup"><span data-stu-id="504b2-236">You will find the selectable properties and their supported operators in the first multirow table on that page.</span></span> <span data-ttu-id="504b2-237">假設您只想要擷取清單中每個作業的識別碼和命令列，您可以在[取得作業的相關資訊][rest_get_task]中的適當資料表找到這幾列：</span><span class="sxs-lookup"><span data-stu-id="504b2-237">If you wish to retrieve only the ID and command line for each task in a list, for example, you will find these rows in the applicable table on [Get information about a task][rest_get_task]:</span></span>

| <span data-ttu-id="504b2-238">屬性</span><span class="sxs-lookup"><span data-stu-id="504b2-238">Property</span></span> | <span data-ttu-id="504b2-239">類型</span><span class="sxs-lookup"><span data-stu-id="504b2-239">Type</span></span> | <span data-ttu-id="504b2-240">注意事項</span><span class="sxs-lookup"><span data-stu-id="504b2-240">Notes</span></span> |
|:--- |:--- |:--- |
| `id` |`String` |`The ID of the task.` |
| `commandLine` |`String` |`The command line of the task.` |

<span data-ttu-id="504b2-241">為了讓每個列出的作業只包含識別碼和命令列，選取字串如下列：</span><span class="sxs-lookup"><span data-stu-id="504b2-241">The select string for including only the ID and command line with each listed task would then be:</span></span>

`id, commandLine`

## <a name="code-samples"></a><span data-ttu-id="504b2-242">程式碼範例</span><span class="sxs-lookup"><span data-stu-id="504b2-242">Code samples</span></span>
### <a name="efficient-list-queries-code-sample"></a><span data-ttu-id="504b2-243">有效率的清單查詢程式碼範例</span><span class="sxs-lookup"><span data-stu-id="504b2-243">Efficient list queries code sample</span></span>
<span data-ttu-id="504b2-244">請查閱 GitHub 上的 [EfficientListQueries][efficient_query_sample] 範例專案，以了解有效率的清單查詢可如何提升應用程式的效能。</span><span class="sxs-lookup"><span data-stu-id="504b2-244">Check out the [EfficientListQueries][efficient_query_sample] sample project on GitHub to see how efficient list querying can affect performance in an application.</span></span> <span data-ttu-id="504b2-245">這個 C# 主控台應用程式會建立並將大量工作加入至作業。</span><span class="sxs-lookup"><span data-stu-id="504b2-245">This C# console application creates and adds a large number of tasks to a job.</span></span> <span data-ttu-id="504b2-246">然後，它會對 [JobOperations.ListTasks][net_list_tasks] 方法進行多個呼叫，並且傳遞設定了不同屬性值的 [ODATADetailLevel][odata] 物件，來變更要傳回的資料量。</span><span class="sxs-lookup"><span data-stu-id="504b2-246">Then, it makes multiple calls to the [JobOperations.ListTasks][net_list_tasks] method and passes [ODATADetailLevel][odata] objects that are configured with different property values to vary the amount of data to be returned.</span></span> <span data-ttu-id="504b2-247">它會產生類似下列的輸出：</span><span class="sxs-lookup"><span data-stu-id="504b2-247">It produces output similar to the following:</span></span>

```
Adding 5000 tasks to job jobEffQuery...
5000 tasks added in 00:00:47.3467587, hit ENTER to query tasks...

4943 tasks retrieved in 00:00:04.3408081 (ExpandClause:  | FilterClause: state eq 'active' | SelectClause: id,state)
0 tasks retrieved in 00:00:00.2662920 (ExpandClause:  | FilterClause: state eq 'running' | SelectClause: id,state)
59 tasks retrieved in 00:00:00.3337760 (ExpandClause:  | FilterClause: state eq 'completed' | SelectClause: id,state)
5000 tasks retrieved in 00:00:04.1429881 (ExpandClause:  | FilterClause:  | SelectClause: id,state)
5000 tasks retrieved in 00:00:15.1016127 (ExpandClause:  | FilterClause:  | SelectClause: id,state,environmentSettings)
5000 tasks retrieved in 00:00:17.0548145 (ExpandClause: stats | FilterClause:  | SelectClause: )

Sample complete, hit ENTER to continue...
```

<span data-ttu-id="504b2-248">如同經過的時間所顯示的，您可以透過限制屬性和傳回的項目數目來大幅降低查詢回應時間。</span><span class="sxs-lookup"><span data-stu-id="504b2-248">As shown in the elapsed times, you can greatly lower query response times by limiting the properties and the number of items that are returned.</span></span> <span data-ttu-id="504b2-249">您可以在 GitHub 上的 [azure-batch-samples][github_samples] 儲存機制，找到本範例專案和其他範例專案。</span><span class="sxs-lookup"><span data-stu-id="504b2-249">You can find this and other sample projects in the [azure-batch-samples][github_samples] repository on GitHub.</span></span>

### <a name="batchmetrics-library-and-code-sample"></a><span data-ttu-id="504b2-250">BatchMetrics 程式庫和程式碼範例</span><span class="sxs-lookup"><span data-stu-id="504b2-250">BatchMetrics library and code sample</span></span>
<span data-ttu-id="504b2-251">除了上述的 EfficientListQueries 程式碼範例，您還可以在 [azure-batch-samples][github_samples] GitHub 儲存機制中找到 [BatchMetrics][batch_metrics] 專案。</span><span class="sxs-lookup"><span data-stu-id="504b2-251">In addition to the EfficientListQueries code sample above, you can find the [BatchMetrics][batch_metrics] project in the [azure-batch-samples][github_samples] GitHub repository.</span></span> <span data-ttu-id="504b2-252">BatchMetrics 範例專案會示範如何使用 Batch API 有效率地監視 Azure Batch 作業進度。</span><span class="sxs-lookup"><span data-stu-id="504b2-252">The BatchMetrics sample project demonstrates how to efficiently monitor Azure Batch job progress using the Batch API.</span></span>

<span data-ttu-id="504b2-253">[BatchMetrics][batch_metrics] 範例包含可併入自己專案的 .NET 類別庫專案，以及用來運作和示範如何使用程式庫的簡單命令列程式。</span><span class="sxs-lookup"><span data-stu-id="504b2-253">The [BatchMetrics][batch_metrics] sample includes a .NET class library project which you can incorporate into your own projects, and a simple command-line program to exercise and demonstrate the use of the library.</span></span>

<span data-ttu-id="504b2-254">專案內的範例應用程式會示範下列作業：</span><span class="sxs-lookup"><span data-stu-id="504b2-254">The sample application within the project demonstrates the following operations:</span></span>

1. <span data-ttu-id="504b2-255">選取特定屬性以便只下載您需要的屬性</span><span class="sxs-lookup"><span data-stu-id="504b2-255">Selecting specific attributes in order to download only the properties you need</span></span>
2. <span data-ttu-id="504b2-256">篩選狀態轉換時間以便只下載上次查詢之後的變更</span><span class="sxs-lookup"><span data-stu-id="504b2-256">Filtering on state transition times in order to download only changes since the last query</span></span>

<span data-ttu-id="504b2-257">例如，下列方法會出現在 BatchMetrics 程式庫。</span><span class="sxs-lookup"><span data-stu-id="504b2-257">For example, the following method appears in the BatchMetrics library.</span></span> <span data-ttu-id="504b2-258">它會傳回 ODATADetailLevel，指出只應該取得所查詢實體的 `id` 和 `state` 屬性。</span><span class="sxs-lookup"><span data-stu-id="504b2-258">It returns an ODATADetailLevel that specifies that only the `id` and `state` properties should be obtained for the entities that are queried.</span></span> <span data-ttu-id="504b2-259">它也會指出只應傳回自指定的 `DateTime` 參數之後其狀態已變更的實體。</span><span class="sxs-lookup"><span data-stu-id="504b2-259">It also specifies that only entities whose state has changed since the specified `DateTime` parameter should be returned.</span></span>

```csharp
internal static ODATADetailLevel OnlyChangedAfter(DateTime time)
{
    return new ODATADetailLevel(
        selectClause: "id, state",
        filterClause: string.Format("stateTransitionTime gt DateTime'{0:o}'", time)
    );
}
```

## <a name="next-steps"></a><span data-ttu-id="504b2-260">後續步驟</span><span class="sxs-lookup"><span data-stu-id="504b2-260">Next steps</span></span>
### <a name="parallel-node-tasks"></a><span data-ttu-id="504b2-261">平行節點工作</span><span class="sxs-lookup"><span data-stu-id="504b2-261">Parallel node tasks</span></span>
<span data-ttu-id="504b2-262">[使用並行節點工作最大化 Azure Batch 計算資源使用量](batch-parallel-node-tasks.md) 是另一篇與 Batch 應用程式效能有關的文章。</span><span class="sxs-lookup"><span data-stu-id="504b2-262">[Maximize Azure Batch compute resource usage with concurrent node tasks](batch-parallel-node-tasks.md) is another article related to Batch application performance.</span></span> <span data-ttu-id="504b2-263">某些類型的工作負載可以受益於在規模較大但數量較少的計算節點上執行平行工作。</span><span class="sxs-lookup"><span data-stu-id="504b2-263">Some types of workloads can benefit from executing parallel tasks on larger--but fewer--compute nodes.</span></span> <span data-ttu-id="504b2-264">如需這類案例的詳細資訊，請查看 [範例案例](batch-parallel-node-tasks.md#example-scenario) 。</span><span class="sxs-lookup"><span data-stu-id="504b2-264">Check out the [example scenario](batch-parallel-node-tasks.md#example-scenario) in the article for details on such a scenario.</span></span>

### <a name="batch-forum"></a><span data-ttu-id="504b2-265">Batch 論壇</span><span class="sxs-lookup"><span data-stu-id="504b2-265">Batch Forum</span></span>
<span data-ttu-id="504b2-266">MSDN 上的 [Azure Batch 論壇][forum]是一個很棒的地方，可以討論 Batch 和詢問有關此服務的問題。</span><span class="sxs-lookup"><span data-stu-id="504b2-266">The [Azure Batch Forum][forum] on MSDN is a great place to discuss Batch and ask questions about the service.</span></span> <span data-ttu-id="504b2-267">請前去查看很有幫助的「便利貼」文章，在建立 Batch 解決方案時，出現問題就張貼。</span><span class="sxs-lookup"><span data-stu-id="504b2-267">Head on over for helpful "sticky" posts, and post your questions as they arise while you build your Batch solutions.</span></span>

[api_net]: http://msdn.microsoft.com/library/azure/mt348682.aspx
[api_net_listjobs]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.listjobs.aspx
[api_rest]: http://msdn.microsoft.com/library/azure/dn820158.aspx
[batch_metrics]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/BatchMetrics
[efficient_query_sample]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/ArticleProjects/EfficientListQueries
[forum]: https://social.msdn.microsoft.com/forums/azure/en-US/home?forum=azurebatch
[github_samples]: https://github.com/Azure/azure-batch-samples
[odata]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.odatadetaillevel.aspx
[odata_ctor]: https://msdn.microsoft.com/library/azure/dn866178.aspx
[odata_expand]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.odatadetaillevel.expandclause.aspx
[odata_filter]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.odatadetaillevel.filterclause.aspx
[odata_select]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.odatadetaillevel.selectclause.aspx

[net_list_certs]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.certificateoperations.listcertificates.aspx
[net_list_compute_nodes]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.listcomputenodes.aspx
[net_list_job_schedules]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.jobscheduleoperations.listjobschedules.aspx
[net_list_jobprep_status]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.listjobpreparationandreleasetaskstatus.aspx
[net_list_jobs]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.listjobs.aspx
[net_list_nodefiles]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.listnodefiles.aspx
[net_list_pools]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.listpools.aspx
[net_list_schedule_jobs]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.jobscheduleoperations.listjobs.aspx
[net_list_task_files]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.listnodefiles.aspx
[net_list_tasks]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.listtasks.aspx

[rest_list_certs]: https://msdn.microsoft.com/library/azure/dn820154.aspx
[rest_list_compute_nodes]: https://msdn.microsoft.com/library/azure/dn820159.aspx
[rest_list_job_schedules]: https://msdn.microsoft.com/library/azure/mt282174.aspx
[rest_list_jobprep_status]: https://msdn.microsoft.com/library/azure/mt282170.aspx
[rest_list_jobs]: https://msdn.microsoft.com/library/azure/dn820117.aspx
[rest_list_nodefiles]: https://msdn.microsoft.com/library/azure/dn820151.aspx
[rest_list_pools]: https://msdn.microsoft.com/library/azure/dn820101.aspx
[rest_list_schedule_jobs]: https://msdn.microsoft.com/library/azure/mt282169.aspx
[rest_list_task_files]: https://msdn.microsoft.com/library/azure/dn820142.aspx
[rest_list_tasks]: https://msdn.microsoft.com/library/azure/dn820187.aspx

[rest_get_cert]: https://msdn.microsoft.com/library/azure/dn820176.aspx
[rest_get_job]: https://msdn.microsoft.com/library/azure/dn820106.aspx
[rest_get_node]: https://msdn.microsoft.com/library/azure/dn820168.aspx
[rest_get_pool]: https://msdn.microsoft.com/library/azure/dn820165.aspx
[rest_get_schedule]: https://msdn.microsoft.com/library/azure/mt282171.aspx
[rest_get_task]: https://msdn.microsoft.com/library/azure/dn820133.aspx

[net_cert]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.certificate.aspx
[net_job]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.aspx
[net_node]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.computenode.aspx
[net_pool]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.aspx
[net_schedule]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjobschedule.aspx
[net_task]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.aspx

[rest_get_task_counts]: https://docs.microsoft.com/rest/api/batchservice/get-the-task-counts-for-a-job