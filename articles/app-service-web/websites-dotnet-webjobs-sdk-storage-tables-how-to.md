---
title: "如何透過 WebJobs SDK 使用 Azure 資料表儲存體"
description: "了解如何透過 WebJobs SDK 使用 Azure 資料表儲存體。 建立資料表、將實體新增至資料表以及讀取現有資料表。"
services: app-service\web, storage
documentationcenter: .net
author: ggailey777
manager: erikre
editor: jimbe
ms.assetid: 451432cc-c780-4310-85d3-84f44fe48afe
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 06/01/2016
ms.author: glenga
ms.openlocfilehash: 13cfc788c14d714df7022ce003d34691cf73d121
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-azure-table-storage-with-the-webjobs-sdk"></a><span data-ttu-id="273e7-104">如何透過 WebJobs SDK 使用 Azure 資料表儲存體</span><span class="sxs-lookup"><span data-stu-id="273e7-104">How to use Azure table storage with the WebJobs SDK</span></span>
## <a name="overview"></a><span data-ttu-id="273e7-105">概觀</span><span class="sxs-lookup"><span data-stu-id="273e7-105">Overview</span></span>
<span data-ttu-id="273e7-106">本指南提供 C# 程式碼範例，示範如何使用 [WebJobs SDK](websites-dotnet-webjobs-sdk.md) 1.x 版讀取和寫入 Azure 儲存體資料表。</span><span class="sxs-lookup"><span data-stu-id="273e7-106">This guide provides C# code samples that show how to read and write Azure storage tables by using [WebJobs SDK](websites-dotnet-webjobs-sdk.md) version 1.x.</span></span>

<span data-ttu-id="273e7-107">本指南假設您知道[如何使用指向您儲存體帳戶的連接字串，在 Visual Studio 中建立 WebJob 專案](websites-dotnet-webjobs-sdk-get-started.md)，或是使用指向[多個儲存體帳戶](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs)的連接字串來建立該專案。</span><span class="sxs-lookup"><span data-stu-id="273e7-107">The guide assumes you know [how to create a WebJob project in Visual Studio with connection strings that point to your storage account](websites-dotnet-webjobs-sdk-get-started.md) or to [multiple storage accounts](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).</span></span>

<span data-ttu-id="273e7-108">有一些程式碼片段顯示 `Table` 屬性用於以 [手動方式呼叫](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#manual)的函式中，也就是說使用的並非觸發屬性。</span><span class="sxs-lookup"><span data-stu-id="273e7-108">Some of the code snippets show the `Table` attribute used in functions that are [called manually](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#manual), that is, not by using one of the trigger attributes.</span></span> 

## <span data-ttu-id="273e7-109"><a id="ingress"></a> 如何將實體新增至資料表</span><span class="sxs-lookup"><span data-stu-id="273e7-109"><a id="ingress"></a> How to add entities to a table</span></span>
<span data-ttu-id="273e7-110">若要將實體新增至資料表，請將 `Table` 屬性搭配 `ICollector<T>` 或 `IAsyncCollector<T>` 參數使用，其中 `T` 會指定您想要加入之實體的結構描述。</span><span class="sxs-lookup"><span data-stu-id="273e7-110">To add entities to a table, use the `Table` attribute with an `ICollector<T>` or `IAsyncCollector<T>` parameter where `T` specifies the schema of the entities you want to add.</span></span> <span data-ttu-id="273e7-111">屬性建構函式採用字串參數，來指定資料表的名稱。</span><span class="sxs-lookup"><span data-stu-id="273e7-111">The attribute constructor takes a string parameter that specifies the name of the table.</span></span> 

<span data-ttu-id="273e7-112">以下程式碼範例會將 `Person` 實體加入名為 *Ingress*的資料表。</span><span class="sxs-lookup"><span data-stu-id="273e7-112">The following code sample adds `Person` entities to a table named *Ingress*.</span></span>

        [NoAutomaticTrigger]
        public static void IngressDemo(
            [Table("Ingress")] ICollector<Person> tableBinding)
        {
            for (int i = 0; i < 100000; i++)
            {
                tableBinding.Add(
                    new Person() { 
                        PartitionKey = "Test", 
                        RowKey = i.ToString(), 
                        Name = "Name" }
                    );
            }
        }

<span data-ttu-id="273e7-113">您和 `ICollector` 一起使用的型別通常衍生自 `TableEntity` 或實作 `ITableEntity`，但並非必要。</span><span class="sxs-lookup"><span data-stu-id="273e7-113">Typically the type you use with `ICollector` derives from `TableEntity` or implements `ITableEntity`, but it doesn't have to.</span></span> <span data-ttu-id="273e7-114">下列任一個 `Person` 類別都能搭配前面 `Ingress` 方法中所示的程式碼使用。</span><span class="sxs-lookup"><span data-stu-id="273e7-114">Either of the following `Person` classes work with the code shown in the preceding `Ingress` method.</span></span>

        public class Person : TableEntity
        {
            public string Name { get; set; }
        }

        public class Person
        {
            public string PartitionKey { get; set; }
            public string RowKey { get; set; }
            public string Name { get; set; }
        }

<span data-ttu-id="273e7-115">如果您想要直接使用 Azure 儲存體 API，您可以將 `CloudStorageAccount` 參數新增至方法簽章。</span><span class="sxs-lookup"><span data-stu-id="273e7-115">If you want to work directly with the Azure storage API, you can add a `CloudStorageAccount` parameter to the method signature.</span></span>

## <span data-ttu-id="273e7-116"><a id="monitor"></a> 即時監視</span><span class="sxs-lookup"><span data-stu-id="273e7-116"><a id="monitor"></a> Real-time monitoring</span></span>
<span data-ttu-id="273e7-117">因為資料外送流量函式經常處理大量資料，所以 WebJobs SDK 儀表板提供即時監視資料。</span><span class="sxs-lookup"><span data-stu-id="273e7-117">Because data ingress functions often process large volumes of data, the WebJobs SDK dashboard provides real-time monitoring data.</span></span> <span data-ttu-id="273e7-118">[引動過程記錄]  區段可告訴您是否仍有執行中的函式。</span><span class="sxs-lookup"><span data-stu-id="273e7-118">The **Invocation Log** section tells you if the function is still running.</span></span>

![輸入函式執行中](./media/websites-dotnet-webjobs-sdk-storage-tables-how-to/ingressrunning.png)

<span data-ttu-id="273e7-120">[引動過程詳細資料]  頁面會報告執行中函式的進度 (寫入的實體數目)，並讓您有機會將它中止。</span><span class="sxs-lookup"><span data-stu-id="273e7-120">The **Invocation Details** page reports the function's progress (number of entities written) while it's running and gives you an opportunity to abort it.</span></span> 

![輸入函式執行中](./media/websites-dotnet-webjobs-sdk-storage-tables-how-to/ingressprogress.png)

<span data-ttu-id="273e7-122">當函式完成時，[引動過程詳細資料]  頁面會報告寫入的資料列數目。</span><span class="sxs-lookup"><span data-stu-id="273e7-122">When the function finishes, the **Invocation Details** page reports the number of rows written.</span></span>

![輸入函式已完成](./media/websites-dotnet-webjobs-sdk-storage-tables-how-to/ingresssuccess.png)

## <span data-ttu-id="273e7-124"><a id="multiple"></a> 如何讀取資料表中的多個實體</span><span class="sxs-lookup"><span data-stu-id="273e7-124"><a id="multiple"></a> How to read multiple entities from a table</span></span>
<span data-ttu-id="273e7-125">若要讀取資料表，請使用 `Table` 屬性搭配 `T` 型別衍生自 `TableEntity` 的 `IQueryable<T>` 參數或實作 `ITableEntity`。</span><span class="sxs-lookup"><span data-stu-id="273e7-125">To read a table, use the `Table` attribute with an `IQueryable<T>` parameter where type `T` derives from `TableEntity` or implements `ITableEntity`.</span></span>

<span data-ttu-id="273e7-126">下列程式碼範例會讀取並記錄 `Ingress` 資料表中的所有資料列：</span><span class="sxs-lookup"><span data-stu-id="273e7-126">The following code sample reads and logs all rows from the `Ingress` table:</span></span>

        public static void ReadTable(
            [Table("Ingress")] IQueryable<Person> tableBinding,
            TextWriter logger)
        {
            var query = from p in tableBinding select p;
            foreach (Person person in query)
            {
                logger.WriteLine("PK:{0}, RK:{1}, Name:{2}", 
                    person.PartitionKey, person.RowKey, person.Name);
            }
        }

### <span data-ttu-id="273e7-127"><a id="readone"></a> 如何讀取資料表中的單一實體</span><span class="sxs-lookup"><span data-stu-id="273e7-127"><a id="readone"></a> How to read a single entity from a table</span></span>
<span data-ttu-id="273e7-128">`Table` 屬性建構函式搭配兩個額外參數，可在想要繫結到單一資料表實體時，讓您指定資料分割索引鍵與資料列索引鍵。</span><span class="sxs-lookup"><span data-stu-id="273e7-128">There is a `Table` attribute constructor with two additional parameters that let you specify the partition key and row key when you want to bind to a single table entity.</span></span>

<span data-ttu-id="273e7-129">下列程式碼範例會根據在佇列訊息中收到的資料分割索引鍵與資料列索引鍵值，來讀取 `Person` 實體的資料表列：</span><span class="sxs-lookup"><span data-stu-id="273e7-129">The following code sample reads a table row for a `Person` entity based on partition key and row key values received in a queue message:</span></span>  

        public static void ReadTableEntity(
            [QueueTrigger("inputqueue")] Person personInQueue,
            [Table("persontable","{PartitionKey}", "{RowKey}")] Person personInTable,
            TextWriter logger)
        {
            if (personInTable == null)
            {
                logger.WriteLine("Person not found: PK:{0}, RK:{1}",
                        personInQueue.PartitionKey, personInQueue.RowKey);
            }
            else
            {
                logger.WriteLine("Person found: PK:{0}, RK:{1}, Name:{2}",
                        personInTable.PartitionKey, personInTable.RowKey, personInTable.Name);
            }
        }


<span data-ttu-id="273e7-130">本範例中的 `Person` 類別不必實作 `ITableEntity`。</span><span class="sxs-lookup"><span data-stu-id="273e7-130">The `Person` class in this example does not have to implement `ITableEntity`.</span></span>

## <span data-ttu-id="273e7-131"><a id="storageapi"></a> 如何直接利用 .NET 儲存體 API 來使用資料表</span><span class="sxs-lookup"><span data-stu-id="273e7-131"><a id="storageapi"></a> How to use the .NET Storage API directly to work with a table</span></span>
<span data-ttu-id="273e7-132">您也可以使用 `Table` 屬性搭配 `CloudTable` 物件，以更有彈性的方式使用資料表。</span><span class="sxs-lookup"><span data-stu-id="273e7-132">You can also use the `Table` attribute with a `CloudTable` object for more flexibility in working with a table.</span></span>

<span data-ttu-id="273e7-133">下列程式碼範例使用 `CloudTable` 物件將單一實體新增至 *Ingress* 資料表。</span><span class="sxs-lookup"><span data-stu-id="273e7-133">The following code sample uses a `CloudTable` object to add a single entity to the *Ingress* table.</span></span> 

        public static void UseStorageAPI(
            [Table("Ingress")] CloudTable tableBinding,
            TextWriter logger)
        {
            var person = new Person()
                {
                    PartitionKey = "Test",
                    RowKey = "100",
                    Name = "Name"
                };
            TableOperation insertOperation = TableOperation.Insert(person);
            tableBinding.Execute(insertOperation);
        }

<span data-ttu-id="273e7-134">如需如何使用 `CloudTable` 物件的詳細資訊，請參閱 [如何從 .NET 使用資料表儲存體](../cosmos-db/table-storage-how-to-use-dotnet.md)。</span><span class="sxs-lookup"><span data-stu-id="273e7-134">For more information about how to use the `CloudTable` object, see [How to use Table Storage from .NET](../cosmos-db/table-storage-how-to-use-dotnet.md).</span></span> 

## <span data-ttu-id="273e7-135"><a id="queues"></a>佇列操作說明文章所涵蓋的相關主題</span><span class="sxs-lookup"><span data-stu-id="273e7-135"><a id="queues"></a>Related topics covered by the queues how-to article</span></span>
<span data-ttu-id="273e7-136">如需如何處理佇列訊息所觸發的資料表處理的相關資訊，或是非資料表處理特有的 WebJobs SDK 案例，請參閱 [如何透過 WebJobs SDK 使用 Azure 佇列儲存體](websites-dotnet-webjobs-sdk-storage-queues-how-to.md)。</span><span class="sxs-lookup"><span data-stu-id="273e7-136">For information about how to handle table processing triggered by a queue message, or for WebJobs SDK scenarios not specific to table processing, see [How to use Azure queue storage with the WebJobs SDK](websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span></span> 

<span data-ttu-id="273e7-137">該文章涵蓋下列主題：</span><span class="sxs-lookup"><span data-stu-id="273e7-137">Topics covered in that article include the following:</span></span>

* <span data-ttu-id="273e7-138">Async 函數</span><span class="sxs-lookup"><span data-stu-id="273e7-138">Async functions</span></span>
* <span data-ttu-id="273e7-139">多個執行個體</span><span class="sxs-lookup"><span data-stu-id="273e7-139">Multiple instances</span></span>
* <span data-ttu-id="273e7-140">正常關機</span><span class="sxs-lookup"><span data-stu-id="273e7-140">Graceful shutdown</span></span>
* <span data-ttu-id="273e7-141">在函式主體中使用 WebJobs SDK 屬性</span><span class="sxs-lookup"><span data-stu-id="273e7-141">Use WebJobs SDK attributes in the body of a function</span></span>
* <span data-ttu-id="273e7-142">在程式碼中設定 SDK 連接字串</span><span class="sxs-lookup"><span data-stu-id="273e7-142">Set the SDK connection strings in code</span></span>
* <span data-ttu-id="273e7-143">在程式碼中設定 WebJobs SDK 建構函式參數的值</span><span class="sxs-lookup"><span data-stu-id="273e7-143">Set values for WebJobs SDK constructor parameters in code</span></span>
* <span data-ttu-id="273e7-144">手動觸發函式</span><span class="sxs-lookup"><span data-stu-id="273e7-144">Trigger a function manually</span></span>
* <span data-ttu-id="273e7-145">寫入記錄檔</span><span class="sxs-lookup"><span data-stu-id="273e7-145">Write logs</span></span>

## <span data-ttu-id="273e7-146"><a id="nextsteps"></a> 後續步驟</span><span class="sxs-lookup"><span data-stu-id="273e7-146"><a id="nextsteps"></a> Next steps</span></span>
<span data-ttu-id="273e7-147">本指南提供的程式碼範例示範如何處理使用 Azure 資料表的常見案例。</span><span class="sxs-lookup"><span data-stu-id="273e7-147">This guide has provided code samples that show how to handle common scenarios for working with Azure tables.</span></span> <span data-ttu-id="273e7-148">如需 Azure WebJobs 和 WebJobs SDK 的詳細資訊，請參閱 [Azure WebJobs 建議使用的資源](http://go.microsoft.com/fwlink/?linkid=390226)。</span><span class="sxs-lookup"><span data-stu-id="273e7-148">For more information about how to use Azure WebJobs and the WebJobs SDK, see [Azure WebJobs Recommended Resources](http://go.microsoft.com/fwlink/?linkid=390226).</span></span>

