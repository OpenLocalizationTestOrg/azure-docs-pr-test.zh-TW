---
title: "aaaHow toouse Azure 資料表儲存體與 hello WebJobs SDK"
description: "了解如何 toouse Azure 資料表儲存體與 hello WebJobs SDK。 建立資料表、 加入實體 tootables 及讀取現有的資料表。"
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
ms.openlocfilehash: 8e28c69df4a934646add9e50c6de28e76dca1636
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-table-storage-with-hello-webjobs-sdk"></a><span data-ttu-id="0e98f-104">如何 toouse Azure 資料表儲存體與 hello WebJobs SDK</span><span class="sxs-lookup"><span data-stu-id="0e98f-104">How toouse Azure table storage with hello WebJobs SDK</span></span>
## <a name="overview"></a><span data-ttu-id="0e98f-105">概觀</span><span class="sxs-lookup"><span data-stu-id="0e98f-105">Overview</span></span>
<span data-ttu-id="0e98f-106">本指南提供的 C# 程式碼範例 tooread 」 和 「 寫入 Azure 儲存體資料表所使用的方式，顯示[WebJobs SDK](websites-dotnet-webjobs-sdk.md)版本 1.x。</span><span class="sxs-lookup"><span data-stu-id="0e98f-106">This guide provides C# code samples that show how tooread and write Azure storage tables by using [WebJobs SDK](websites-dotnet-webjobs-sdk.md) version 1.x.</span></span>

<span data-ttu-id="0e98f-107">hello 指南假設您知道[toocreate WebJob 專案在 Visual Studio 中使用連接字串該點 tooyour 儲存體帳戶的方式](websites-dotnet-webjobs-sdk-get-started.md)或太[多個儲存體帳戶](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs)。</span><span class="sxs-lookup"><span data-stu-id="0e98f-107">hello guide assumes you know [how toocreate a WebJob project in Visual Studio with connection strings that point tooyour storage account](websites-dotnet-webjobs-sdk-get-started.md) or too[multiple storage accounts](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).</span></span>

<span data-ttu-id="0e98f-108">有些 hello 程式碼片段會顯示 hello`Table`函式中使用的屬性[以手動方式呼叫](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#manual)，也就是不是使用其中一個 hello 觸發程序屬性。</span><span class="sxs-lookup"><span data-stu-id="0e98f-108">Some of hello code snippets show hello `Table` attribute used in functions that are [called manually](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#manual), that is, not by using one of hello trigger attributes.</span></span> 

## <span data-ttu-id="0e98f-109"><a id="ingress"></a>如何 tooadd 實體 tooa 資料表</span><span class="sxs-lookup"><span data-stu-id="0e98f-109"><a id="ingress"></a> How tooadd entities tooa table</span></span>
<span data-ttu-id="0e98f-110">tooadd 實體 tooa 資料表，使用 hello`Table`屬性附帶`ICollector<T>`或`IAsyncCollector<T>`參數其中`T`指定 hello 結構描述要 tooadd 的 hello 實體。</span><span class="sxs-lookup"><span data-stu-id="0e98f-110">tooadd entities tooa table, use hello `Table` attribute with an `ICollector<T>` or `IAsyncCollector<T>` parameter where `T` specifies hello schema of hello entities you want tooadd.</span></span> <span data-ttu-id="0e98f-111">hello 屬性建構函式接受字串參數，指定 hello hello 資料表名稱。</span><span class="sxs-lookup"><span data-stu-id="0e98f-111">hello attribute constructor takes a string parameter that specifies hello name of hello table.</span></span> 

<span data-ttu-id="0e98f-112">hello 下列程式碼範例會將`Person`實體 tooa 資料表名為*輸入*。</span><span class="sxs-lookup"><span data-stu-id="0e98f-112">hello following code sample adds `Person` entities tooa table named *Ingress*.</span></span>

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

<span data-ttu-id="0e98f-113">通常 hello 要使用的類型`ICollector`衍生自`TableEntity`或實作`ITableEntity`，但不一定要。</span><span class="sxs-lookup"><span data-stu-id="0e98f-113">Typically hello type you use with `ICollector` derives from `TableEntity` or implements `ITableEntity`, but it doesn't have to.</span></span> <span data-ttu-id="0e98f-114">Hello 下列任一`Person`類別與 hello hello 前面所示的程式碼的工作`Ingress`方法。</span><span class="sxs-lookup"><span data-stu-id="0e98f-114">Either of hello following `Person` classes work with hello code shown in hello preceding `Ingress` method.</span></span>

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

<span data-ttu-id="0e98f-115">如果您想 toowork 直接與 hello Azure 儲存體 API，您可以加入`CloudStorageAccount`參數 toohello 方法簽章。</span><span class="sxs-lookup"><span data-stu-id="0e98f-115">If you want toowork directly with hello Azure storage API, you can add a `CloudStorageAccount` parameter toohello method signature.</span></span>

## <span data-ttu-id="0e98f-116"><a id="monitor"></a> 即時監視</span><span class="sxs-lookup"><span data-stu-id="0e98f-116"><a id="monitor"></a> Real-time monitoring</span></span>
<span data-ttu-id="0e98f-117">資料輸入函式通常會處理大型資料磁碟區，因為 hello WebJobs SDK 儀表板會提供即時監視資料。</span><span class="sxs-lookup"><span data-stu-id="0e98f-117">Because data ingress functions often process large volumes of data, hello WebJobs SDK dashboard provides real-time monitoring data.</span></span> <span data-ttu-id="0e98f-118">hello**引動過程記錄**一節說明您是否 hello 函式仍在執行。</span><span class="sxs-lookup"><span data-stu-id="0e98f-118">hello **Invocation Log** section tells you if hello function is still running.</span></span>

![輸入函式執行中](./media/websites-dotnet-webjobs-sdk-storage-tables-how-to/ingressrunning.png)

<span data-ttu-id="0e98f-120">hello**引動過程詳細資料**頁面會報告 hello 函式的進度 （寫入的實體數目） 時正在執行，而且可讓您有機會 tooabort 它。</span><span class="sxs-lookup"><span data-stu-id="0e98f-120">hello **Invocation Details** page reports hello function's progress (number of entities written) while it's running and gives you an opportunity tooabort it.</span></span> 

![輸入函式執行中](./media/websites-dotnet-webjobs-sdk-storage-tables-how-to/ingressprogress.png)

<span data-ttu-id="0e98f-122">當 hello 函式完成時 hello**引動過程詳細資料**頁面會報告 hello 寫入的資料列數目。</span><span class="sxs-lookup"><span data-stu-id="0e98f-122">When hello function finishes, hello **Invocation Details** page reports hello number of rows written.</span></span>

![輸入函式已完成](./media/websites-dotnet-webjobs-sdk-storage-tables-how-to/ingresssuccess.png)

## <span data-ttu-id="0e98f-124"><a id="multiple"></a>如何 tooread 資料表中的多個實體</span><span class="sxs-lookup"><span data-stu-id="0e98f-124"><a id="multiple"></a> How tooread multiple entities from a table</span></span>
<span data-ttu-id="0e98f-125">tooread 資料表時，使用 hello`Table`屬性附帶`IQueryable<T>`參數在其中輸入`T`衍生自`TableEntity`或實作`ITableEntity`。</span><span class="sxs-lookup"><span data-stu-id="0e98f-125">tooread a table, use hello `Table` attribute with an `IQueryable<T>` parameter where type `T` derives from `TableEntity` or implements `ITableEntity`.</span></span>

<span data-ttu-id="0e98f-126">hello 下列程式碼範例會讀取並記錄的所有資料列從 hello`Ingress`資料表：</span><span class="sxs-lookup"><span data-stu-id="0e98f-126">hello following code sample reads and logs all rows from hello `Ingress` table:</span></span>

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

### <span data-ttu-id="0e98f-127"><a id="readone"></a>如何從資料表的單一實體 tooread</span><span class="sxs-lookup"><span data-stu-id="0e98f-127"><a id="readone"></a> How tooread a single entity from a table</span></span>
<span data-ttu-id="0e98f-128">沒有`Table`具有兩個額外的參數，可讓您指定 hello 資料分割索引鍵和資料列索引鍵，當您想 toobind tooa 單一資料表實體的屬性建構函式。</span><span class="sxs-lookup"><span data-stu-id="0e98f-128">There is a `Table` attribute constructor with two additional parameters that let you specify hello partition key and row key when you want toobind tooa single table entity.</span></span>

<span data-ttu-id="0e98f-129">hello 下列程式碼範例讀取的資料表資料列的`Person`根據資料分割索引鍵和資料列索引鍵值接收佇列訊息中的實體：</span><span class="sxs-lookup"><span data-stu-id="0e98f-129">hello following code sample reads a table row for a `Person` entity based on partition key and row key values received in a queue message:</span></span>  

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


<span data-ttu-id="0e98f-130">hello`Person`在此範例中的類別並沒有 tooimplement `ITableEntity`。</span><span class="sxs-lookup"><span data-stu-id="0e98f-130">hello `Person` class in this example does not have tooimplement `ITableEntity`.</span></span>

## <span data-ttu-id="0e98f-131"><a id="storageapi"></a>如何 toouse hello.NET 儲存體 API 直接 toowork 與資料表</span><span class="sxs-lookup"><span data-stu-id="0e98f-131"><a id="storageapi"></a> How toouse hello .NET Storage API directly toowork with a table</span></span>
<span data-ttu-id="0e98f-132">您也可以使用 hello`Table`屬性附帶`CloudTable`更靈活地使用資料表的物件。</span><span class="sxs-lookup"><span data-stu-id="0e98f-132">You can also use hello `Table` attribute with a `CloudTable` object for more flexibility in working with a table.</span></span>

<span data-ttu-id="0e98f-133">hello 下列程式碼範例使用`CloudTable`物件 tooadd 單一實體 toohello*輸入*資料表。</span><span class="sxs-lookup"><span data-stu-id="0e98f-133">hello following code sample uses a `CloudTable` object tooadd a single entity toohello *Ingress* table.</span></span> 

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

<span data-ttu-id="0e98f-134">如需有關如何 toouse hello`CloudTable`物件，請參閱[如何 toouse 資料表儲存體從.NET](../cosmos-db/table-storage-how-to-use-dotnet.md)。</span><span class="sxs-lookup"><span data-stu-id="0e98f-134">For more information about how toouse hello `CloudTable` object, see [How toouse Table Storage from .NET](../cosmos-db/table-storage-how-to-use-dotnet.md).</span></span> 

## <span data-ttu-id="0e98f-135"><a id="queues"></a>Hello 佇列如何 tooarticle 所涵蓋的相關的主題</span><span class="sxs-lookup"><span data-stu-id="0e98f-135"><a id="queues"></a>Related topics covered by hello queues how-tooarticle</span></span>
<span data-ttu-id="0e98f-136">如需如何 toohandle 資料表處理觸發佇列訊息，或 WebJobs SDK 案例不處理，請參閱特定 tootable[如何 toouse Azure 佇列儲存體與 hello WebJobs SDK](websites-dotnet-webjobs-sdk-storage-queues-how-to.md)。</span><span class="sxs-lookup"><span data-stu-id="0e98f-136">For information about how toohandle table processing triggered by a queue message, or for WebJobs SDK scenarios not specific tootable processing, see [How toouse Azure queue storage with hello WebJobs SDK](websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span></span> 

<span data-ttu-id="0e98f-137">在該文件中涵蓋的主題包括下列 hello:</span><span class="sxs-lookup"><span data-stu-id="0e98f-137">Topics covered in that article include hello following:</span></span>

* <span data-ttu-id="0e98f-138">Async 函數</span><span class="sxs-lookup"><span data-stu-id="0e98f-138">Async functions</span></span>
* <span data-ttu-id="0e98f-139">多個執行個體</span><span class="sxs-lookup"><span data-stu-id="0e98f-139">Multiple instances</span></span>
* <span data-ttu-id="0e98f-140">正常關機</span><span class="sxs-lookup"><span data-stu-id="0e98f-140">Graceful shutdown</span></span>
* <span data-ttu-id="0e98f-141">使用 WebJobs SDK hello 函式主體中的屬性</span><span class="sxs-lookup"><span data-stu-id="0e98f-141">Use WebJobs SDK attributes in hello body of a function</span></span>
* <span data-ttu-id="0e98f-142">程式碼中設定 hello SDK 連接字串</span><span class="sxs-lookup"><span data-stu-id="0e98f-142">Set hello SDK connection strings in code</span></span>
* <span data-ttu-id="0e98f-143">在程式碼中設定 WebJobs SDK 建構函式參數的值</span><span class="sxs-lookup"><span data-stu-id="0e98f-143">Set values for WebJobs SDK constructor parameters in code</span></span>
* <span data-ttu-id="0e98f-144">手動觸發函式</span><span class="sxs-lookup"><span data-stu-id="0e98f-144">Trigger a function manually</span></span>
* <span data-ttu-id="0e98f-145">寫入記錄檔</span><span class="sxs-lookup"><span data-stu-id="0e98f-145">Write logs</span></span>

## <span data-ttu-id="0e98f-146"><a id="nextsteps"></a> 後續步驟</span><span class="sxs-lookup"><span data-stu-id="0e98f-146"><a id="nextsteps"></a> Next steps</span></span>
<span data-ttu-id="0e98f-147">本指南提供的程式碼範例會顯示如何使用 Azure 資料表的 toohandle 常見案例。</span><span class="sxs-lookup"><span data-stu-id="0e98f-147">This guide has provided code samples that show how toohandle common scenarios for working with Azure tables.</span></span> <span data-ttu-id="0e98f-148">如需有關如何 toouse Azure WebJobs 和 hello WebJobs SDK，請參閱[Azure WebJobs 建議資源](http://go.microsoft.com/fwlink/?linkid=390226)。</span><span class="sxs-lookup"><span data-stu-id="0e98f-148">For more information about how toouse Azure WebJobs and hello WebJobs SDK, see [Azure WebJobs Recommended Resources](http://go.microsoft.com/fwlink/?linkid=390226).</span></span>

