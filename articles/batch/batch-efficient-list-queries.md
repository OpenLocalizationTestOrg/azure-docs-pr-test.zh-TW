---
title: "aaaDesign 有效率清單查詢 Azure 批次 |Microsoft 文件"
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
ms.openlocfilehash: b7e554119ec9d0e9e8007ccfb1ca80fe142a5e27
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-queries-toolist-batch-resources-efficiently"></a><span data-ttu-id="2d906-103">有效率地建立查詢 toolist 批次資源</span><span class="sxs-lookup"><span data-stu-id="2d906-103">Create queries toolist Batch resources efficiently</span></span>

<span data-ttu-id="2d906-104">這裡您將學習如何 tooincrease Azure Batch 應用程式的效能，藉由減少查詢作業時，會將 hello 服務所傳回之資料的 hello 數量工作、 以及計算節點以 hello[批次.NET] [ api_net]程式庫。</span><span class="sxs-lookup"><span data-stu-id="2d906-104">Here you'll learn how tooincrease your Azure Batch application's performance by reducing hello amount of data that is returned by hello service when you query jobs, tasks, and compute nodes with hello [Batch .NET][api_net] library.</span></span>

<span data-ttu-id="2d906-105">幾乎所有的批次應用程式需要 tooperform 某種類型的查詢通常定期 hello 批次服務的監視或其他作業。</span><span class="sxs-lookup"><span data-stu-id="2d906-105">Nearly all Batch applications need tooperform some type of monitoring or other operation that queries hello Batch service, often at regular intervals.</span></span> <span data-ttu-id="2d906-106">例如，toodetermine 是否有任何其餘作業中的佇列的工作，您必須取得資料 hello 工作中每個工作。</span><span class="sxs-lookup"><span data-stu-id="2d906-106">For example, toodetermine whether there are any queued tasks remaining in a job, you must get data on every task in hello job.</span></span> <span data-ttu-id="2d906-107">toodetermine hello 狀態的集區中的節點，您必須在 hello 集區中的每個節點上取得資料。</span><span class="sxs-lookup"><span data-stu-id="2d906-107">toodetermine hello status of nodes in your pool, you must get data on every node in hello pool.</span></span> <span data-ttu-id="2d906-108">這篇文章說明如何 tooexecute 這類查詢在 hello 最有效率的方式。</span><span class="sxs-lookup"><span data-stu-id="2d906-108">This article explains how tooexecute such queries in hello most efficient way.</span></span>

> [!NOTE]
> <span data-ttu-id="2d906-109">hello 批次服務會提供特殊的應用程式開發介面支援 hello 常見的案例的計數中的工作的工作。</span><span class="sxs-lookup"><span data-stu-id="2d906-109">hello Batch service provides special API support for hello common scenario of counting tasks in a job.</span></span> <span data-ttu-id="2d906-110">而不使用這些清單查詢，您可以呼叫 hello[取得工作計數][ rest_get_task_counts]作業。</span><span class="sxs-lookup"><span data-stu-id="2d906-110">Instead of using a list query for these, you can call hello [Get Task Counts][rest_get_task_counts] operation.</span></span> <span data-ttu-id="2d906-111">「取得工作計數」會指出多少工作擱置中、執行中或已完成，以及有多少工作成功或失敗。</span><span class="sxs-lookup"><span data-stu-id="2d906-111">Get Task Counts indicates how many tasks are pending, running or complete, and how many tasks have succeeded or failed.</span></span> <span data-ttu-id="2d906-112">「取得工作計數」比清單查詢更有效率。</span><span class="sxs-lookup"><span data-stu-id="2d906-112">Get Task Counts is more efficient than a list query.</span></span> <span data-ttu-id="2d906-113">如需詳細資訊，請參閱[依狀態計算作業的工作 (預覽)](batch-get-task-counts.md)。</span><span class="sxs-lookup"><span data-stu-id="2d906-113">For more information, see [Count tasks for a job by state (Preview)](batch-get-task-counts.md).</span></span> 
>
> <span data-ttu-id="2d906-114">hello 取得工作計數作業不適用於批次服務版本早於 2017年-06-01.5.1。</span><span class="sxs-lookup"><span data-stu-id="2d906-114">hello Get Task Counts operation is not available in Batch service versions earlier than 2017-06-01.5.1.</span></span> <span data-ttu-id="2d906-115">如果您使用較舊版本的 hello 服務，然後改用清單查詢 toocount 工作中的工作。</span><span class="sxs-lookup"><span data-stu-id="2d906-115">If you are using an older version of hello service, then use a list query toocount tasks in a job instead.</span></span>
>
> 

## <a name="meet-hello-detaillevel"></a><span data-ttu-id="2d906-116">符合 hello DetailLevel</span><span class="sxs-lookup"><span data-stu-id="2d906-116">Meet hello DetailLevel</span></span>
<span data-ttu-id="2d906-117">在實際執行批次應用程式，像是工作、 工作和計算節點的實體可以在 hello 千分位數字。</span><span class="sxs-lookup"><span data-stu-id="2d906-117">In a production Batch application, entities like jobs, tasks, and compute nodes can number in hello thousands.</span></span> <span data-ttu-id="2d906-118">當您要求這些資源的詳細資訊時，可能會大量的資料必須 「 通用 hello wire"hello 批次服務 tooyour 應用程式上每個查詢。</span><span class="sxs-lookup"><span data-stu-id="2d906-118">When you request information on these resources, a potentially large amount of data must "cross hello wire" from hello Batch service tooyour application on each query.</span></span> <span data-ttu-id="2d906-119">藉由限制 hello 項目數目和類型的查詢所傳回的資訊，您可以增加 hello，將查詢的速度，並因此 hello 應用程式的效能。</span><span class="sxs-lookup"><span data-stu-id="2d906-119">By limiting hello number of items and type of information that is returned by a query, you can increase hello speed of your queries, and therefore hello performance of your application.</span></span>

<span data-ttu-id="2d906-120">這[批次.NET] [ api_net]應用程式開發介面程式碼片段清單*每*與作業，連同相關聯的工作*所有*的每個 hello 屬性工作：</span><span class="sxs-lookup"><span data-stu-id="2d906-120">This [Batch .NET][api_net] API code snippet lists *every* task that is associated with a job, along with *all* of hello properties of each task:</span></span>

```csharp
// Get a collection of all of hello tasks and all of their properties for job-001
IPagedEnumerable<CloudTask> allTasks =
    batchClient.JobOperations.ListTasks("job-001");
```

<span data-ttu-id="2d906-121">您可以藉由套用 「 詳細資訊層級 」 tooyour 查詢，不過，執行更有效率的清單查詢。</span><span class="sxs-lookup"><span data-stu-id="2d906-121">You can perform a much more efficient list query, however, by applying a "detail level" tooyour query.</span></span> <span data-ttu-id="2d906-122">您可以提供[ODATADetailLevel] [ odata]物件 toohello [JobOperations.ListTasks] [ net_list_tasks]方法。</span><span class="sxs-lookup"><span data-stu-id="2d906-122">You do this by supplying an [ODATADetailLevel][odata] object toohello [JobOperations.ListTasks][net_list_tasks] method.</span></span> <span data-ttu-id="2d906-123">這個程式碼片段會傳回識別碼 hello、 命令列和計算節點資訊屬性的已完成的工作：</span><span class="sxs-lookup"><span data-stu-id="2d906-123">This snippet returns only hello ID, command line, and compute node information properties of completed tasks:</span></span>

```csharp
// Configure an ODATADetailLevel specifying a subset of tasks and
// their properties tooreturn
ODATADetailLevel detailLevel = new ODATADetailLevel();
detailLevel.FilterClause = "state eq 'completed'";
detailLevel.SelectClause = "id,commandLine,nodeInfo";

// Supply hello ODATADetailLevel toohello ListTasks method
IPagedEnumerable<CloudTask> completedTasks =
    batchClient.JobOperations.ListTasks("job-001", detailLevel);
```

<span data-ttu-id="2d906-124">在此範例案例，還有上千款 hello 作業中的工作如果 hello hello 第二個查詢結果通常會是速度快得多超過 hello 傳回第一次。</span><span class="sxs-lookup"><span data-stu-id="2d906-124">In this example scenario, if there are thousands of tasks in hello job, hello results from hello second query will typically be returned much quicker than hello first.</span></span> <span data-ttu-id="2d906-125">當您列出 hello 批次.NET API 的項目時，使用 ODATADetailLevel 詳細資訊就會包含[下方](#efficient-querying-in-batch-net)。</span><span class="sxs-lookup"><span data-stu-id="2d906-125">More information about using ODATADetailLevel when you list items with hello Batch .NET API is included [below](#efficient-querying-in-batch-net).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2d906-126">我們強烈建議您使用您*一律*提供 ODATADetailLevel 物件 tooyour.NET API 清單呼叫 tooensure 最大效率和應用程式的效能。</span><span class="sxs-lookup"><span data-stu-id="2d906-126">We highly recommend that you *always* supply an ODATADetailLevel object tooyour .NET API list calls tooensure maximum efficiency and performance of your application.</span></span> <span data-ttu-id="2d906-127">藉由指定詳細層級，您可以協助 toolower 批次服務的回應時間、 提高網路使用率和記憶體使用量降至最低用戶端應用程式。</span><span class="sxs-lookup"><span data-stu-id="2d906-127">By specifying a detail level, you can help toolower Batch service response times, improve network utilization, and minimize memory usage by client applications.</span></span>
> 
> 

## <a name="filter-select-and-expand"></a><span data-ttu-id="2d906-128">篩選、選取及展開</span><span class="sxs-lookup"><span data-stu-id="2d906-128">Filter, select, and expand</span></span>
<span data-ttu-id="2d906-129">hello[批次.NET] [ api_net]和[批次 REST] [ api_rest] Api 提供 hello 能力 tooreduce 項目在清單中，會傳回這兩個 hello 數目以及 hello 與每個傳回的資訊數量。</span><span class="sxs-lookup"><span data-stu-id="2d906-129">hello [Batch .NET][api_net] and [Batch REST][api_rest] APIs provide hello ability tooreduce both hello number of items that are returned in a list, as well as hello amount of information that is returned for each.</span></span> <span data-ttu-id="2d906-130">您可以藉由在執行清單查詢時指定**篩選**、**選取**和**展開字串**來執行此動作。</span><span class="sxs-lookup"><span data-stu-id="2d906-130">You do so by specifying **filter**, **select**, and **expand strings** when performing list queries.</span></span>

### <a name="filter"></a><span data-ttu-id="2d906-131">Filter</span><span class="sxs-lookup"><span data-stu-id="2d906-131">Filter</span></span>
<span data-ttu-id="2d906-132">hello 篩選字串是運算式，可降低 hello 傳回項目數目。</span><span class="sxs-lookup"><span data-stu-id="2d906-132">hello filter string is an expression that reduces hello number of items that are returned.</span></span> <span data-ttu-id="2d906-133">例如，清單只 hello 執行作業或清單只有計算節點是準備 toorun 工作的工作。</span><span class="sxs-lookup"><span data-stu-id="2d906-133">For example, list only hello running tasks for a job, or list only compute nodes that are ready toorun tasks.</span></span>

* <span data-ttu-id="2d906-134">hello 篩選字串包含一個或多個運算式，包含屬性名稱、 運算子和值的運算式。</span><span class="sxs-lookup"><span data-stu-id="2d906-134">hello filter string consists of one or more expressions, with an expression that consists of a property name, operator, and value.</span></span> <span data-ttu-id="2d906-135">hello 屬性可指定是在查詢時，特定 tooeach 實體型別是 hello 運算子所支援的每一個屬性。</span><span class="sxs-lookup"><span data-stu-id="2d906-135">hello properties that can be specified are specific tooeach entity type that you query, as are hello operators that are supported for each property.</span></span>
* <span data-ttu-id="2d906-136">使用 hello 邏輯運算子也可以結合多個運算式`and`和`or`。</span><span class="sxs-lookup"><span data-stu-id="2d906-136">Multiple expressions can be combined by using hello logical operators `and` and `or`.</span></span>
* <span data-ttu-id="2d906-137">此範例中篩選字串清單，僅執行 hello 的 「 轉譯 」 工作： `(state eq 'running') and startswith(id, 'renderTask')`。</span><span class="sxs-lookup"><span data-stu-id="2d906-137">This example filter string lists only hello running "render" tasks: `(state eq 'running') and startswith(id, 'renderTask')`.</span></span>

### <a name="select"></a><span data-ttu-id="2d906-138">選取</span><span class="sxs-lookup"><span data-stu-id="2d906-138">Select</span></span>
<span data-ttu-id="2d906-139">hello 選取字串限制所傳回的每個項目 hello 屬性值。</span><span class="sxs-lookup"><span data-stu-id="2d906-139">hello select string limits hello property values that are returned for each item.</span></span> <span data-ttu-id="2d906-140">您指定的屬性名稱清單，而且只有這些屬性的值會傳回 hello hello 查詢結果中的項目。</span><span class="sxs-lookup"><span data-stu-id="2d906-140">You specify a list of property names, and only those property values are returned for hello items in hello query results.</span></span>

* <span data-ttu-id="2d906-141">hello 選取字串包含屬性名稱的逗號分隔清單。</span><span class="sxs-lookup"><span data-stu-id="2d906-141">hello select string consists of a comma-separated list of property names.</span></span> <span data-ttu-id="2d906-142">您可以指定任何 hello hello 您要查詢的實體類型的屬性。</span><span class="sxs-lookup"><span data-stu-id="2d906-142">You can specify any of hello properties for hello entity type you are querying.</span></span>
* <span data-ttu-id="2d906-143">此範例選取字串會指定應該針對每個工作只傳回三個屬性： `id, state, stateTransitionTime`。</span><span class="sxs-lookup"><span data-stu-id="2d906-143">This example select string specifies that only three property values should be returned for each task: `id, state, stateTransitionTime`.</span></span>

### <a name="expand"></a><span data-ttu-id="2d906-144">展開</span><span class="sxs-lookup"><span data-stu-id="2d906-144">Expand</span></span>
<span data-ttu-id="2d906-145">hello 展開字串可減少需要的 tooobtain API 呼叫的 hello 數目特定資訊。</span><span class="sxs-lookup"><span data-stu-id="2d906-145">hello expand string reduces hello number of API calls that are required tooobtain certain information.</span></span> <span data-ttu-id="2d906-146">當您使用展開字串時，可以透過單一 API 呼叫取得每個項目的相關詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="2d906-146">When you use an expand string, more information about each item can be obtained with a single API call.</span></span> <span data-ttu-id="2d906-147">而不是第一次取得 hello 清單中的實體，則要求資訊 hello 清單中的每個項目，您可以使用擴充字串 tooobtain hello 單一 API 呼叫中的相同資訊。</span><span class="sxs-lookup"><span data-stu-id="2d906-147">Rather than first obtaining hello list of entities, then requesting information for each item in hello list, you use an expand string tooobtain hello same information in a single API call.</span></span> <span data-ttu-id="2d906-148">較少的 API 呼叫表示較佳的效能。</span><span class="sxs-lookup"><span data-stu-id="2d906-148">Less API calls means better performance.</span></span>

* <span data-ttu-id="2d906-149">類似 toohello 選取字串 hello 展開字串控制項是否包含特定資料查詢結果清單中。</span><span class="sxs-lookup"><span data-stu-id="2d906-149">Similar toohello select string, hello expand string controls whether certain data is included in list query results.</span></span>
* <span data-ttu-id="2d906-150">hello 展開字串僅適用於列出工作、 工作排程、 工作和集區時。</span><span class="sxs-lookup"><span data-stu-id="2d906-150">hello expand string is only supported when it is used in listing jobs, job schedules, tasks, and pools.</span></span> <span data-ttu-id="2d906-151">目前，它僅支援統計資訊。</span><span class="sxs-lookup"><span data-stu-id="2d906-151">Currently, it only supports statistics information.</span></span>
* <span data-ttu-id="2d906-152">Hello 時需要的所有屬性，指定任何選取的字串，會展開字串*必須*使用的 tooget 統計資料資訊。</span><span class="sxs-lookup"><span data-stu-id="2d906-152">When all properties are required and no select string is specified, hello expand string *must* be used tooget statistics information.</span></span> <span data-ttu-id="2d906-153">如果選取的字串是使用的 tooobtain 屬性的子集，則`stats`可以在 hello 選取字串中，指定與 hello 展開字串不需要指定 toobe。</span><span class="sxs-lookup"><span data-stu-id="2d906-153">If a select string is used tooobtain a subset of properties, then `stats` can be specified in hello select string, and hello expand string does not need toobe specified.</span></span>
* <span data-ttu-id="2d906-154">這個範例會展開字串指定應傳回每個項目的 hello 清單中的統計資料資訊： `stats`。</span><span class="sxs-lookup"><span data-stu-id="2d906-154">This example expand string specifies that statistics information should be returned for each item in hello list: `stats`.</span></span>

> [!NOTE]
> <span data-ttu-id="2d906-155">當建構 hello 的任何三個查詢字串型別 （篩選、 選取及展開），您必須確定 hello 屬性名稱和大小寫符合的 REST API 項目與其。</span><span class="sxs-lookup"><span data-stu-id="2d906-155">When constructing any of hello three query string types (filter, select, and expand), you must ensure that hello property names and case match that of their REST API element counterparts.</span></span> <span data-ttu-id="2d906-156">例如，當使用 hello.NET [CloudTask](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask)類別，您必須指定**狀態**而不是**狀態**，即使 hello.NET 屬性是[CloudTask.State](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.state)。</span><span class="sxs-lookup"><span data-stu-id="2d906-156">For example, when working with hello .NET [CloudTask](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask) class, you must specify **state** instead of **State**, even though hello .NET property is [CloudTask.State](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.state).</span></span> <span data-ttu-id="2d906-157">請參閱下方的 hello 資料表 hello.NET 和 REST Api 之間的屬性對應。</span><span class="sxs-lookup"><span data-stu-id="2d906-157">See hello tables below for property mappings between hello .NET and REST APIs.</span></span>
> 
> 

### <a name="rules-for-filter-select-and-expand-strings"></a><span data-ttu-id="2d906-158">篩選、選取和展開字串的規則</span><span class="sxs-lookup"><span data-stu-id="2d906-158">Rules for filter, select, and expand strings</span></span>
* <span data-ttu-id="2d906-159">屬性名稱，在篩選中，選取和展開字串應該會出現在 hello[批次 REST] [ api_rest] API-只有當您使用時，即使[批次.NET] [ api_net]或其中一個 hello 其他批次 Sdk。</span><span class="sxs-lookup"><span data-stu-id="2d906-159">Properties names in filter, select, and expand strings should appear as they do in hello [Batch REST][api_rest] API--even when you use [Batch .NET][api_net] or one of hello other Batch SDKs.</span></span>
* <span data-ttu-id="2d906-160">所有屬性名稱都會區分大小寫，但屬性值不會區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="2d906-160">All property names are case-sensitive, but property values are case insensitive.</span></span>
* <span data-ttu-id="2d906-161">日期/時間字串有兩種格式，開頭必須加上 `DateTime`。</span><span class="sxs-lookup"><span data-stu-id="2d906-161">Date/time strings can be one of two formats, and must be preceded with `DateTime`.</span></span>
  
  * <span data-ttu-id="2d906-162">W3C-DTF 格式範例：`creationTime gt DateTime'2011-05-08T08:49:37Z'`</span><span class="sxs-lookup"><span data-stu-id="2d906-162">W3C-DTF format example: `creationTime gt DateTime'2011-05-08T08:49:37Z'`</span></span>
  * <span data-ttu-id="2d906-163">RFC 1123 格式範例：`creationTime gt DateTime'Sun, 08 May 2011 08:49:37 GMT'`</span><span class="sxs-lookup"><span data-stu-id="2d906-163">RFC 1123 format example: `creationTime gt DateTime'Sun, 08 May 2011 08:49:37 GMT'`</span></span>
* <span data-ttu-id="2d906-164">布林值字串為 `true` 或 `false`。</span><span class="sxs-lookup"><span data-stu-id="2d906-164">Boolean strings are either `true` or `false`.</span></span>
* <span data-ttu-id="2d906-165">如果指定無效的屬性或運算子，將會導致 `400 (Bad Request)` 錯誤。</span><span class="sxs-lookup"><span data-stu-id="2d906-165">If an invalid property or operator is specified, a `400 (Bad Request)` error will result.</span></span>

## <a name="efficient-querying-in-batch-net"></a><span data-ttu-id="2d906-166">在 Batch .NET 中有效率地查詢</span><span class="sxs-lookup"><span data-stu-id="2d906-166">Efficient querying in Batch .NET</span></span>
<span data-ttu-id="2d906-167">在 hello[批次.NET] [ api_net] API、 hello [ODATADetailLevel] [ odata]類別用來提供篩選、 選取和展開的字串toolist 作業。</span><span class="sxs-lookup"><span data-stu-id="2d906-167">Within hello [Batch .NET][api_net] API, hello [ODATADetailLevel][odata] class is used for supplying filter, select, and expand strings toolist operations.</span></span> <span data-ttu-id="2d906-168">hello ODataDetailLevel 類別有三個公用的字串屬性，可以指定在 hello 建構函式，或直接 hello 物件上設定。</span><span class="sxs-lookup"><span data-stu-id="2d906-168">hello ODataDetailLevel class has three public string properties that can be specified in hello constructor, or set directly on hello object.</span></span> <span data-ttu-id="2d906-169">您接著將 hello ODataDetailLevel 物件當做參數 toohello 各種清單作業，例如[ListPools][net_list_pools]， [ListJobs][net_list_jobs]，和[ListTasks][net_list_tasks]。</span><span class="sxs-lookup"><span data-stu-id="2d906-169">You then pass hello ODataDetailLevel object as a parameter toohello various list operations such as [ListPools][net_list_pools], [ListJobs][net_list_jobs], and [ListTasks][net_list_tasks].</span></span>

* <span data-ttu-id="2d906-170">[ODATADetailLevel][odata]。[FilterClause][odata_filter]: hello 傳回項目數目限制。</span><span class="sxs-lookup"><span data-stu-id="2d906-170">[ODATADetailLevel][odata].[FilterClause][odata_filter]: Limit hello number of items that are returned.</span></span>
* <span data-ttu-id="2d906-171">[ODATADetailLevel][odata].[SelectClause][odata_select]：指定隨著每個項目一起傳回的屬性值。</span><span class="sxs-lookup"><span data-stu-id="2d906-171">[ODATADetailLevel][odata].[SelectClause][odata_select]: Specify which property values are returned with each item.</span></span>
* <span data-ttu-id="2d906-172">[ODATADetailLevel][odata].[ExpandClause][odata_expand]：在單一 API 呼叫中擷取所有項目的資料，而不是針對每個項目個別呼叫。</span><span class="sxs-lookup"><span data-stu-id="2d906-172">[ODATADetailLevel][odata].[ExpandClause][odata_expand]: Retrieve data for all items in a single API call instead of separate calls for each item.</span></span>

<span data-ttu-id="2d906-173">hello 下列程式碼片段會使用 hello 批次.NET API tooefficiently hello 批次的查詢服務的一組特定的集區的 hello 統計資料。</span><span class="sxs-lookup"><span data-stu-id="2d906-173">hello following code snippet uses hello Batch .NET API tooefficiently query hello Batch service for hello statistics of a specific set of pools.</span></span> <span data-ttu-id="2d906-174">在此案例中，hello 批次使用者已測試與實際的集區。</span><span class="sxs-lookup"><span data-stu-id="2d906-174">In this scenario, hello Batch user has both test and production pools.</span></span> <span data-ttu-id="2d906-175">hello 測試集區識別碼前面會加上 「 測試 」，並 hello 生產集區識別碼前面會加上"prod"。</span><span class="sxs-lookup"><span data-stu-id="2d906-175">hello test pool IDs are prefixed with "test", and hello production pool IDs are prefixed with "prod".</span></span> <span data-ttu-id="2d906-176">在 hello 片段*myBatchClient* hello 的正確初始化執行個體[BatchClient](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.batchclient)類別。</span><span class="sxs-lookup"><span data-stu-id="2d906-176">In hello snippet, *myBatchClient* is a properly initialized instance of hello [BatchClient](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.batchclient) class.</span></span>

```csharp
// First we need an ODATADetailLevel instance on which tooset hello filter, select,
// and expand clause strings
ODATADetailLevel detailLevel = new ODATADetailLevel();

// We want toopull only hello "test" pools, so we limit hello number of items returned
// by using a FilterClause and specifying that hello pool IDs must start with "test"
detailLevel.FilterClause = "startswith(id, 'test')";

// toofurther limit hello data that crosses hello wire, configure hello SelectClause to
// limit hello properties that are returned on each CloudPool object tooonly
// CloudPool.Id and CloudPool.Statistics
detailLevel.SelectClause = "id, stats";

// Specify hello ExpandClause so that hello .NET API pulls hello statistics for the
// CloudPools in a single underlying REST API call. Note that we use hello pool's
// REST API element name "stats" here as opposed too"Statistics" as it appears in
// hello .NET API (CloudPool.Statistics)
detailLevel.ExpandClause = "stats";

// Now get our collection of pools, minimizing hello amount of data that is returned
// by specifying hello detail level that we configured above
List<CloudPool> testPools =
    await myBatchClient.PoolOperations.ListPools(detailLevel).ToListAsync();
```

> [!TIP]
> <span data-ttu-id="2d906-177">執行個體[ODATADetailLevel] [ odata] ，設定選取和展開子句也可以傳遞 tooappropriate Get 方法，例如[PoolOperations.GetPool](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.getpool.aspx)會傳回的資料 toolimit hello 數量。</span><span class="sxs-lookup"><span data-stu-id="2d906-177">An instance of [ODATADetailLevel][odata] that is configured with Select and Expand clauses can also be passed tooappropriate Get methods, such as [PoolOperations.GetPool](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.getpool.aspx), toolimit hello amount of data that is returned.</span></span>
> 
> 

## <a name="batch-rest-toonet-api-mappings"></a><span data-ttu-id="2d906-178">批次 REST too.NET API 對應</span><span class="sxs-lookup"><span data-stu-id="2d906-178">Batch REST too.NET API mappings</span></span>
<span data-ttu-id="2d906-179">篩選、選取和展開字串中的屬性名稱在名稱和大小寫方面， *必須* 反映其 REST API 對應項目。</span><span class="sxs-lookup"><span data-stu-id="2d906-179">Property names in filter, select, and expand strings *must* reflect their REST API counterparts, both in name and case.</span></span> <span data-ttu-id="2d906-180">下列的 hello 表格提供 hello.NET 和 REST API 的對應項目之間的對應。</span><span class="sxs-lookup"><span data-stu-id="2d906-180">hello tables below provide mappings between hello .NET and REST API counterparts.</span></span>

### <a name="mappings-for-filter-strings"></a><span data-ttu-id="2d906-181">篩選字串的對應</span><span class="sxs-lookup"><span data-stu-id="2d906-181">Mappings for filter strings</span></span>
* <span data-ttu-id="2d906-182">**清單的.NET 方法**: hello.NET API 方法，這個資料行中的每個接受[ODATADetailLevel] [ odata]物件做為參數。</span><span class="sxs-lookup"><span data-stu-id="2d906-182">**.NET list methods**: Each of hello .NET API methods in this column accepts an [ODATADetailLevel][odata] object as a parameter.</span></span>
* <span data-ttu-id="2d906-183">**其餘列出要求**： 每個 REST API 頁面連結的 tooin 此資料行包含資料表中，指定 hello 屬性和作業中允許的*篩選*字串。</span><span class="sxs-lookup"><span data-stu-id="2d906-183">**REST list requests**: Each REST API page linked tooin this column contains a table that specifies hello properties and operations that are allowed in *filter* strings.</span></span> <span data-ttu-id="2d906-184">建構 [ODATADetailLevel.FilterClause][odata_filter] 字串時會使用這些屬性名稱和作業。</span><span class="sxs-lookup"><span data-stu-id="2d906-184">You will use these property names and operations when you construct an [ODATADetailLevel.FilterClause][odata_filter] string.</span></span>

| <span data-ttu-id="2d906-185">.NET 清單方法</span><span class="sxs-lookup"><span data-stu-id="2d906-185">.NET list methods</span></span> | <span data-ttu-id="2d906-186">REST 清單要求</span><span class="sxs-lookup"><span data-stu-id="2d906-186">REST list requests</span></span> |
| --- | --- |
| <span data-ttu-id="2d906-187">[CertificateOperations.ListCertificates][net_list_certs]</span><span class="sxs-lookup"><span data-stu-id="2d906-187">[CertificateOperations.ListCertificates][net_list_certs]</span></span> |<span data-ttu-id="2d906-188">[列出帳戶中的 hello 憑證][rest_list_certs]</span><span class="sxs-lookup"><span data-stu-id="2d906-188">[List hello certificates in an account][rest_list_certs]</span></span> |
| <span data-ttu-id="2d906-189">[CloudTask.ListNodeFiles][net_list_task_files]</span><span class="sxs-lookup"><span data-stu-id="2d906-189">[CloudTask.ListNodeFiles][net_list_task_files]</span></span> |<span data-ttu-id="2d906-190">[列出與工作相關聯的 hello 檔案][rest_list_task_files]</span><span class="sxs-lookup"><span data-stu-id="2d906-190">[List hello files associated with a task][rest_list_task_files]</span></span> |
| <span data-ttu-id="2d906-191">[JobOperations.ListJobPreparationAndReleaseTaskStatus][net_list_jobprep_status]</span><span class="sxs-lookup"><span data-stu-id="2d906-191">[JobOperations.ListJobPreparationAndReleaseTaskStatus][net_list_jobprep_status]</span></span> |<span data-ttu-id="2d906-192">[列示 hello 的 hello 作業準備及作業版本作業 」 工作的狀態][rest_list_jobprep_status]</span><span class="sxs-lookup"><span data-stu-id="2d906-192">[List hello status of hello job preparation and job release tasks for a job][rest_list_jobprep_status]</span></span> |
| <span data-ttu-id="2d906-193">[JobOperations.ListJobs][net_list_jobs]</span><span class="sxs-lookup"><span data-stu-id="2d906-193">[JobOperations.ListJobs][net_list_jobs]</span></span> |<span data-ttu-id="2d906-194">[列出帳戶中的 hello 工作][rest_list_jobs]</span><span class="sxs-lookup"><span data-stu-id="2d906-194">[List hello jobs in an account][rest_list_jobs]</span></span> |
| <span data-ttu-id="2d906-195">[JobOperations.ListNodeFiles][net_list_nodefiles]</span><span class="sxs-lookup"><span data-stu-id="2d906-195">[JobOperations.ListNodeFiles][net_list_nodefiles]</span></span> |<span data-ttu-id="2d906-196">[在節點上的清單 hello 檔案][rest_list_nodefiles]</span><span class="sxs-lookup"><span data-stu-id="2d906-196">[List hello files on a node][rest_list_nodefiles]</span></span> |
| <span data-ttu-id="2d906-197">[JobOperations.ListTasks][net_list_tasks]</span><span class="sxs-lookup"><span data-stu-id="2d906-197">[JobOperations.ListTasks][net_list_tasks]</span></span> |<span data-ttu-id="2d906-198">[列出 hello 工作與工作相關聯][rest_list_tasks]</span><span class="sxs-lookup"><span data-stu-id="2d906-198">[List hello tasks associated with a job][rest_list_tasks]</span></span> |
| <span data-ttu-id="2d906-199">[JobScheduleOperations.ListJobSchedules][net_list_job_schedules]</span><span class="sxs-lookup"><span data-stu-id="2d906-199">[JobScheduleOperations.ListJobSchedules][net_list_job_schedules]</span></span> |<span data-ttu-id="2d906-200">[列出帳戶中的 hello 作業排程][rest_list_job_schedules]</span><span class="sxs-lookup"><span data-stu-id="2d906-200">[List hello job schedules in an account][rest_list_job_schedules]</span></span> |
| <span data-ttu-id="2d906-201">[JobScheduleOperations.ListJobs][net_list_schedule_jobs]</span><span class="sxs-lookup"><span data-stu-id="2d906-201">[JobScheduleOperations.ListJobs][net_list_schedule_jobs]</span></span> |<span data-ttu-id="2d906-202">[列出 hello 工作相關聯的工作排程][rest_list_schedule_jobs]</span><span class="sxs-lookup"><span data-stu-id="2d906-202">[List hello jobs associated with a job schedule][rest_list_schedule_jobs]</span></span> |
| <span data-ttu-id="2d906-203">[PoolOperations.ListComputeNodes][net_list_compute_nodes]</span><span class="sxs-lookup"><span data-stu-id="2d906-203">[PoolOperations.ListComputeNodes][net_list_compute_nodes]</span></span> |<span data-ttu-id="2d906-204">[清單 hello 計算集區中的節點][rest_list_compute_nodes]</span><span class="sxs-lookup"><span data-stu-id="2d906-204">[List hello compute nodes in a pool][rest_list_compute_nodes]</span></span> |
| <span data-ttu-id="2d906-205">[PoolOperations.ListPools][net_list_pools]</span><span class="sxs-lookup"><span data-stu-id="2d906-205">[PoolOperations.ListPools][net_list_pools]</span></span> |<span data-ttu-id="2d906-206">[在帳戶中的清單 hello 集區][rest_list_pools]</span><span class="sxs-lookup"><span data-stu-id="2d906-206">[List hello pools in an account][rest_list_pools]</span></span> |

### <a name="mappings-for-select-strings"></a><span data-ttu-id="2d906-207">選取字串的對應</span><span class="sxs-lookup"><span data-stu-id="2d906-207">Mappings for select strings</span></span>
* <span data-ttu-id="2d906-208">**Batch .NET types**：Batch .NET API 類型。</span><span class="sxs-lookup"><span data-stu-id="2d906-208">**Batch .NET types**: Batch .NET API types.</span></span>
* <span data-ttu-id="2d906-209">**REST API 實體**： 此資料行中的每個頁面包含一或多個資料表，列出 hello 類型 hello REST API 屬性的名稱。</span><span class="sxs-lookup"><span data-stu-id="2d906-209">**REST API entities**: Each page in this column contains one or more tables that list hello REST API property names for hello type.</span></span> <span data-ttu-id="2d906-210">建構「選取」  字串時會使用這些屬性名稱。</span><span class="sxs-lookup"><span data-stu-id="2d906-210">These property names are used when you construct *select* strings.</span></span> <span data-ttu-id="2d906-211">建構 [ODATADetailLevel.SelectClause][odata_select] 字串時會使用這些相同的屬性名稱。</span><span class="sxs-lookup"><span data-stu-id="2d906-211">You will use these same property names when you construct an [ODATADetailLevel.SelectClause][odata_select] string.</span></span>

| <span data-ttu-id="2d906-212">Batch .NET types</span><span class="sxs-lookup"><span data-stu-id="2d906-212">Batch .NET types</span></span> | <span data-ttu-id="2d906-213">REST API entities</span><span class="sxs-lookup"><span data-stu-id="2d906-213">REST API entities</span></span> |
| --- | --- |
| <span data-ttu-id="2d906-214">[憑證][net_cert]</span><span class="sxs-lookup"><span data-stu-id="2d906-214">[Certificate][net_cert]</span></span> |<span data-ttu-id="2d906-215">[取得憑證的相關資訊][rest_get_cert]</span><span class="sxs-lookup"><span data-stu-id="2d906-215">[Get information about a certificate][rest_get_cert]</span></span> |
| <span data-ttu-id="2d906-216">[CloudJob][net_job]</span><span class="sxs-lookup"><span data-stu-id="2d906-216">[CloudJob][net_job]</span></span> |<span data-ttu-id="2d906-217">[取得作業的相關資訊][rest_get_job]</span><span class="sxs-lookup"><span data-stu-id="2d906-217">[Get information about a job][rest_get_job]</span></span> |
| <span data-ttu-id="2d906-218">[CloudJobSchedule][net_schedule]</span><span class="sxs-lookup"><span data-stu-id="2d906-218">[CloudJobSchedule][net_schedule]</span></span> |<span data-ttu-id="2d906-219">[取得作業排程的相關資訊][rest_get_schedule]</span><span class="sxs-lookup"><span data-stu-id="2d906-219">[Get information about a job schedule][rest_get_schedule]</span></span> |
| <span data-ttu-id="2d906-220">[ComputeNode][net_node]</span><span class="sxs-lookup"><span data-stu-id="2d906-220">[ComputeNode][net_node]</span></span> |<span data-ttu-id="2d906-221">[取得節點的相關資訊][rest_get_node]</span><span class="sxs-lookup"><span data-stu-id="2d906-221">[Get information about a node][rest_get_node]</span></span> |
| <span data-ttu-id="2d906-222">[CloudPool][net_pool]</span><span class="sxs-lookup"><span data-stu-id="2d906-222">[CloudPool][net_pool]</span></span> |<span data-ttu-id="2d906-223">[取得集區的相關資訊][rest_get_pool]</span><span class="sxs-lookup"><span data-stu-id="2d906-223">[Get information about a pool][rest_get_pool]</span></span> |
| <span data-ttu-id="2d906-224">[CloudTask][net_task]</span><span class="sxs-lookup"><span data-stu-id="2d906-224">[CloudTask][net_task]</span></span> |<span data-ttu-id="2d906-225">[取得作業的相關資訊][rest_get_task]</span><span class="sxs-lookup"><span data-stu-id="2d906-225">[Get information about a task][rest_get_task]</span></span> |

## <a name="example-construct-a-filter-string"></a><span data-ttu-id="2d906-226">範例：建構篩選字串</span><span class="sxs-lookup"><span data-stu-id="2d906-226">Example: construct a filter string</span></span>
<span data-ttu-id="2d906-227">當您建構篩選字串[ODATADetailLevel.FilterClause][odata_filter]，請參閱底下 「 篩選字串對應 」 toofind hello REST API 文件頁面對應上方 hello 資料表您想 tooperform toohello 清單作業。</span><span class="sxs-lookup"><span data-stu-id="2d906-227">When you construct a filter string for [ODATADetailLevel.FilterClause][odata_filter], consult hello table above under "Mappings for filter strings" toofind hello REST API documentation page that corresponds toohello list operation that you wish tooperform.</span></span> <span data-ttu-id="2d906-228">在 hello 第一個多重資料列的資料表在該頁面上，您會發現 hello 可篩選的屬性和其支援的運算子。</span><span class="sxs-lookup"><span data-stu-id="2d906-228">You will find hello filterable properties and their supported operators in hello first multirow table on that page.</span></span> <span data-ttu-id="2d906-229">如果您想 tooretrieve 其結束碼為非零的所有工作，例如，此資料列上[清單與工作相關聯的 hello 工作][ rest_list_tasks]指定 hello 適用的屬性字串和允許的運算子：</span><span class="sxs-lookup"><span data-stu-id="2d906-229">If you wish tooretrieve all tasks whose exit code was nonzero, for example, this row on [List hello tasks associated with a job][rest_list_tasks] specifies hello applicable property string and allowable operators:</span></span>

| <span data-ttu-id="2d906-230">屬性</span><span class="sxs-lookup"><span data-stu-id="2d906-230">Property</span></span> | <span data-ttu-id="2d906-231">允許的作業</span><span class="sxs-lookup"><span data-stu-id="2d906-231">Operations allowed</span></span> | <span data-ttu-id="2d906-232">類型</span><span class="sxs-lookup"><span data-stu-id="2d906-232">Type</span></span> |
|:--- |:--- |:--- |
| `executionInfo/exitCode` |`eq, ge, gt, le , lt` |`Int` |

<span data-ttu-id="2d906-233">因此，會是 hello 篩選條件字串，以列出所有工作，則為非零結束代碼：</span><span class="sxs-lookup"><span data-stu-id="2d906-233">Thus, hello filter string for listing all tasks with a nonzero exit code would be:</span></span>

`(executionInfo/exitCode lt 0) or (executionInfo/exitCode gt 0)`

## <a name="example-construct-a-select-string"></a><span data-ttu-id="2d906-234">範例：建構選取字串</span><span class="sxs-lookup"><span data-stu-id="2d906-234">Example: construct a select string</span></span>
<span data-ttu-id="2d906-235">tooconstruct [ODATADetailLevel.SelectClause][odata_select]，請參閱底下 「 選取的字串對應 」 上方 hello 資料表，並瀏覽 toohello 對應 toohello 型別之實體的 REST API 頁面，您列出。</span><span class="sxs-lookup"><span data-stu-id="2d906-235">tooconstruct [ODATADetailLevel.SelectClause][odata_select], consult hello table above under "Mappings for select strings" and navigate toohello REST API page that corresponds toohello type of entity that you are listing.</span></span> <span data-ttu-id="2d906-236">在 hello 第一個多重資料列的資料表在該頁面上，您會發現 hello 可選取的屬性和其支援的運算子。</span><span class="sxs-lookup"><span data-stu-id="2d906-236">You will find hello selectable properties and their supported operators in hello first multirow table on that page.</span></span> <span data-ttu-id="2d906-237">如果您想 tooretrieve 只有 hello 識別碼以及每項工作的命令列在清單中，比方說，您會發現這些資料列中 hello 適用的資料表上[取得工作的相關資訊][rest_get_task]:</span><span class="sxs-lookup"><span data-stu-id="2d906-237">If you wish tooretrieve only hello ID and command line for each task in a list, for example, you will find these rows in hello applicable table on [Get information about a task][rest_get_task]:</span></span>

| <span data-ttu-id="2d906-238">屬性</span><span class="sxs-lookup"><span data-stu-id="2d906-238">Property</span></span> | <span data-ttu-id="2d906-239">類型</span><span class="sxs-lookup"><span data-stu-id="2d906-239">Type</span></span> | <span data-ttu-id="2d906-240">注意事項</span><span class="sxs-lookup"><span data-stu-id="2d906-240">Notes</span></span> |
|:--- |:--- |:--- |
| `id` |`String` |`hello ID of hello task.` |
| `commandLine` |`String` |`hello command line of hello task.` |

<span data-ttu-id="2d906-241">hello 選取字串，包括唯一識別碼 hello 和命令列與每個列出的工作將會是：</span><span class="sxs-lookup"><span data-stu-id="2d906-241">hello select string for including only hello ID and command line with each listed task would then be:</span></span>

`id, commandLine`

## <a name="code-samples"></a><span data-ttu-id="2d906-242">程式碼範例</span><span class="sxs-lookup"><span data-stu-id="2d906-242">Code samples</span></span>
### <a name="efficient-list-queries-code-sample"></a><span data-ttu-id="2d906-243">有效率的清單查詢程式碼範例</span><span class="sxs-lookup"><span data-stu-id="2d906-243">Efficient list queries code sample</span></span>
<span data-ttu-id="2d906-244">簽出 hello [EfficientListQueries] [ efficient_query_sample] GitHub toosee 效率的範例專案清單查詢可能會影響應用程式中的效能。</span><span class="sxs-lookup"><span data-stu-id="2d906-244">Check out hello [EfficientListQueries][efficient_query_sample] sample project on GitHub toosee how efficient list querying can affect performance in an application.</span></span> <span data-ttu-id="2d906-245">此 C# 主控台應用程式建立，並將大量的工作 tooa 作業。</span><span class="sxs-lookup"><span data-stu-id="2d906-245">This C# console application creates and adds a large number of tasks tooa job.</span></span> <span data-ttu-id="2d906-246">然後，它可讓多個呼叫 toohello [JobOperations.ListTasks] [ net_list_tasks]方法，並傳遞[ODATADetailLevel] [ odata]的物件設定為使用不同的屬性值 toovary hello 數量資料 toobe 傳回。</span><span class="sxs-lookup"><span data-stu-id="2d906-246">Then, it makes multiple calls toohello [JobOperations.ListTasks][net_list_tasks] method and passes [ODATADetailLevel][odata] objects that are configured with different property values toovary hello amount of data toobe returned.</span></span> <span data-ttu-id="2d906-247">它會產生類似 toohello 下列輸出：</span><span class="sxs-lookup"><span data-stu-id="2d906-247">It produces output similar toohello following:</span></span>

```
Adding 5000 tasks toojob jobEffQuery...
5000 tasks added in 00:00:47.3467587, hit ENTER tooquery tasks...

4943 tasks retrieved in 00:00:04.3408081 (ExpandClause:  | FilterClause: state eq 'active' | SelectClause: id,state)
0 tasks retrieved in 00:00:00.2662920 (ExpandClause:  | FilterClause: state eq 'running' | SelectClause: id,state)
59 tasks retrieved in 00:00:00.3337760 (ExpandClause:  | FilterClause: state eq 'completed' | SelectClause: id,state)
5000 tasks retrieved in 00:00:04.1429881 (ExpandClause:  | FilterClause:  | SelectClause: id,state)
5000 tasks retrieved in 00:00:15.1016127 (ExpandClause:  | FilterClause:  | SelectClause: id,state,environmentSettings)
5000 tasks retrieved in 00:00:17.0548145 (ExpandClause: stats | FilterClause:  | SelectClause: )

Sample complete, hit ENTER toocontinue...
```

<span data-ttu-id="2d906-248">Hello 經過時間所示，您可以大幅降低查詢回應時間，藉由限制 hello 屬性和項目所傳回的 hello 數目。</span><span class="sxs-lookup"><span data-stu-id="2d906-248">As shown in hello elapsed times, you can greatly lower query response times by limiting hello properties and hello number of items that are returned.</span></span> <span data-ttu-id="2d906-249">您可以在 hello 中找到這個和其他範例專案[azure 批次範例][ github_samples] GitHub 上的儲存機制。</span><span class="sxs-lookup"><span data-stu-id="2d906-249">You can find this and other sample projects in hello [azure-batch-samples][github_samples] repository on GitHub.</span></span>

### <a name="batchmetrics-library-and-code-sample"></a><span data-ttu-id="2d906-250">BatchMetrics 程式庫和程式碼範例</span><span class="sxs-lookup"><span data-stu-id="2d906-250">BatchMetrics library and code sample</span></span>
<span data-ttu-id="2d906-251">此外 toohello EfficientListQueries 程式碼上述範例，您可以找到 hello [BatchMetrics] [ batch_metrics] hello 中的專案[azure 批次範例][ github_samples]GitHub 儲存機制。</span><span class="sxs-lookup"><span data-stu-id="2d906-251">In addition toohello EfficientListQueries code sample above, you can find hello [BatchMetrics][batch_metrics] project in hello [azure-batch-samples][github_samples] GitHub repository.</span></span> <span data-ttu-id="2d906-252">hello BatchMetrics 範例專案會示範如何 tooefficiently 監視使用 hello 批次 API 的 Azure 批次工作進度。</span><span class="sxs-lookup"><span data-stu-id="2d906-252">hello BatchMetrics sample project demonstrates how tooefficiently monitor Azure Batch job progress using hello Batch API.</span></span>

<span data-ttu-id="2d906-253">hello [BatchMetrics] [ batch_metrics]範例包含.NET 類別庫專案的可合併到您自己的專案和簡單的命令列程式 tooexercise 和示範 hello 使用 hello程式庫。</span><span class="sxs-lookup"><span data-stu-id="2d906-253">hello [BatchMetrics][batch_metrics] sample includes a .NET class library project which you can incorporate into your own projects, and a simple command-line program tooexercise and demonstrate hello use of hello library.</span></span>

<span data-ttu-id="2d906-254">hello 專案中的 hello 範例應用程式會示範下列作業的 hello:</span><span class="sxs-lookup"><span data-stu-id="2d906-254">hello sample application within hello project demonstrates hello following operations:</span></span>

1. <span data-ttu-id="2d906-255">您選取特定的屬性順序 toodownload 只有 hello 屬性中需要</span><span class="sxs-lookup"><span data-stu-id="2d906-255">Selecting specific attributes in order toodownload only hello properties you need</span></span>
2. <span data-ttu-id="2d906-256">篩選順序 toodownload 狀態轉換時間僅會變更 hello 上次查詢後</span><span class="sxs-lookup"><span data-stu-id="2d906-256">Filtering on state transition times in order toodownload only changes since hello last query</span></span>

<span data-ttu-id="2d906-257">例如，下列方法的 hello 會出現在 hello BatchMetrics 程式庫。</span><span class="sxs-lookup"><span data-stu-id="2d906-257">For example, hello following method appears in hello BatchMetrics library.</span></span> <span data-ttu-id="2d906-258">它會傳回指定的唯一 hello ODATADetailLevel`id`和`state`應該查詢的 hello 實體取得內容。</span><span class="sxs-lookup"><span data-stu-id="2d906-258">It returns an ODATADetailLevel that specifies that only hello `id` and `state` properties should be obtained for hello entities that are queried.</span></span> <span data-ttu-id="2d906-259">它也會指定唯一的實體，其狀態已變更自指定的 hello`DateTime`應傳回參數。</span><span class="sxs-lookup"><span data-stu-id="2d906-259">It also specifies that only entities whose state has changed since hello specified `DateTime` parameter should be returned.</span></span>

```csharp
internal static ODATADetailLevel OnlyChangedAfter(DateTime time)
{
    return new ODATADetailLevel(
        selectClause: "id, state",
        filterClause: string.Format("stateTransitionTime gt DateTime'{0:o}'", time)
    );
}
```

## <a name="next-steps"></a><span data-ttu-id="2d906-260">後續步驟</span><span class="sxs-lookup"><span data-stu-id="2d906-260">Next steps</span></span>
### <a name="parallel-node-tasks"></a><span data-ttu-id="2d906-261">平行節點工作</span><span class="sxs-lookup"><span data-stu-id="2d906-261">Parallel node tasks</span></span>
<span data-ttu-id="2d906-262">[Azure Batch 計算資源使用率與並行節點工作最大化](batch-parallel-node-tasks.md)是另一個發行項相關 tooBatch 應用程式效能。</span><span class="sxs-lookup"><span data-stu-id="2d906-262">[Maximize Azure Batch compute resource usage with concurrent node tasks](batch-parallel-node-tasks.md) is another article related tooBatch application performance.</span></span> <span data-ttu-id="2d906-263">某些類型的工作負載可以受益於在規模較大但數量較少的計算節點上執行平行工作。</span><span class="sxs-lookup"><span data-stu-id="2d906-263">Some types of workloads can benefit from executing parallel tasks on larger--but fewer--compute nodes.</span></span> <span data-ttu-id="2d906-264">簽出 hello[範例案例](batch-parallel-node-tasks.md#example-scenario)如需詳細資訊，在這類案例中的 hello 文件中。</span><span class="sxs-lookup"><span data-stu-id="2d906-264">Check out hello [example scenario](batch-parallel-node-tasks.md#example-scenario) in hello article for details on such a scenario.</span></span>

### <a name="batch-forum"></a><span data-ttu-id="2d906-265">Batch 論壇</span><span class="sxs-lookup"><span data-stu-id="2d906-265">Batch Forum</span></span>
<span data-ttu-id="2d906-266">hello [Azure Batch 論壇][ forum] MSDN 上會很大的放置 toodiscuss 批次，並詢問 hello 服務有關的問題。</span><span class="sxs-lookup"><span data-stu-id="2d906-266">hello [Azure Batch Forum][forum] on MSDN is a great place toodiscuss Batch and ask questions about hello service.</span></span> <span data-ttu-id="2d906-267">請前去查看很有幫助的「便利貼」文章，在建立 Batch 解決方案時，出現問題就張貼。</span><span class="sxs-lookup"><span data-stu-id="2d906-267">Head on over for helpful "sticky" posts, and post your questions as they arise while you build your Batch solutions.</span></span>

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