---
title: "aaaGetting 已開始使用 Azure 儲存體和 Visual Studio 已連接服務 （WebJob 專案）"
description: "Tooget 啟動用戶端連接使用 Visual Studio tooa 儲存體帳戶已連接服務後，使用 Azure 資料表儲存體 Azure Webjob 專案在 Visual Studio 中的方式"
services: storage
documentationcenter: 
author: TomArcher
manager: douge
editor: 
ms.assetid: 061a6c46-0592-4e5d-aced-ab7498481cde
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: tarcher
ms.openlocfilehash: 448dee3369207062ee85c6636c84bcb4e26a2085
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-storage-azure-webjob-projects"></a><span data-ttu-id="82d03-103">開始使用 Azure 儲存體 (Azure WebJob 專案)</span><span class="sxs-lookup"><span data-stu-id="82d03-103">Getting Started with Azure Storage (Azure WebJob Projects)</span></span>
[!INCLUDE [storage-try-azure-tools-tables](../../includes/storage-try-azure-tools-tables.md)]

## <a name="overview"></a><span data-ttu-id="82d03-104">概觀</span><span class="sxs-lookup"><span data-stu-id="82d03-104">Overview</span></span>
<span data-ttu-id="82d03-105">本文章提供 C# 程式碼範例，示範顯示如何 toouse hello Azure WebJobs SDK 版本 1.x 以 hello Azure 資料表儲存體服務。</span><span class="sxs-lookup"><span data-stu-id="82d03-105">This article provides C# code samples that show show how toouse hello Azure WebJobs SDK version 1.x with hello Azure table storage service.</span></span> <span data-ttu-id="82d03-106">hello 程式碼範例使用 hello [WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk.md)版本 1.x。</span><span class="sxs-lookup"><span data-stu-id="82d03-106">hello code samples use hello [WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk.md) version 1.x.</span></span>

<span data-ttu-id="82d03-107">hello Azure 資料表儲存體服務可讓您 toostore 大量結構化資料。</span><span class="sxs-lookup"><span data-stu-id="82d03-107">hello Azure Table storage service enables you toostore large amounts of structured data.</span></span> <span data-ttu-id="82d03-108">hello 服務是可接受來自內部和外部 hello Azure 雲端的已驗證的呼叫的 NoSQL 資料存放區。</span><span class="sxs-lookup"><span data-stu-id="82d03-108">hello service is a NoSQL datastore that accepts authenticated calls from inside and outside hello Azure cloud.</span></span> <span data-ttu-id="82d03-109">Azure 資料表很適合儲存結構化、非關聯式資料。</span><span class="sxs-lookup"><span data-stu-id="82d03-109">Azure tables are ideal for storing structured, non-relational data.</span></span>  <span data-ttu-id="82d03-110">如需詳細資訊，請參閱 [以 .NET 開始使用 Azure 資料表儲存體](storage-dotnet-how-to-use-tables.md#create-a-table) 。</span><span class="sxs-lookup"><span data-stu-id="82d03-110">See [Get started with Azure Table storage using .NET](storage-dotnet-how-to-use-tables.md#create-a-table) for more information.</span></span>

<span data-ttu-id="82d03-111">有些 hello 程式碼片段會顯示 hello**資料表**用於呼叫的函式以手動方式，亦即，不是使用其中一個 hello 觸發程序屬性的屬性。</span><span class="sxs-lookup"><span data-stu-id="82d03-111">Some of hello code snippets show hello **Table** attribute used in functions that are called manually, that is, not by using one of hello trigger attributes.</span></span>

## <a name="how-tooadd-entities-tooa-table"></a><span data-ttu-id="82d03-112">如何 tooadd 實體 tooa 資料表</span><span class="sxs-lookup"><span data-stu-id="82d03-112">How tooadd entities tooa table</span></span>
<span data-ttu-id="82d03-113">tooadd 實體 tooa 資料表，使用 hello**資料表**屬性附帶**ICollector<T>** 或**IAsyncCollector<T>** 參數其中**T**指定 hello 結構描述要 tooadd 的 hello 實體。</span><span class="sxs-lookup"><span data-stu-id="82d03-113">tooadd entities tooa table, use hello **Table** attribute with an **ICollector<T>** or **IAsyncCollector<T>** parameter where **T** specifies hello schema of hello entities you want tooadd.</span></span> <span data-ttu-id="82d03-114">hello 屬性建構函式接受字串參數，指定 hello hello 資料表名稱。</span><span class="sxs-lookup"><span data-stu-id="82d03-114">hello attribute constructor takes a string parameter that specifies hello name of hello table.</span></span>

<span data-ttu-id="82d03-115">hello 下列程式碼範例會將**人員**實體 tooa 資料表名為*輸入*。</span><span class="sxs-lookup"><span data-stu-id="82d03-115">hello following code sample adds **Person** entities tooa table named *Ingress*.</span></span>

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

<span data-ttu-id="82d03-116">通常 hello 要使用的類型**ICollector**衍生自**TableEntity**或實作**ITableEntity**，但不一定要。</span><span class="sxs-lookup"><span data-stu-id="82d03-116">Typically hello type you use with **ICollector** derives from **TableEntity** or implements **ITableEntity**, but it doesn't have to.</span></span> <span data-ttu-id="82d03-117">Hello 下列任一**人員**類別與 hello hello 前面所示的程式碼的工作**輸入**方法。</span><span class="sxs-lookup"><span data-stu-id="82d03-117">Either of hello following **Person** classes work with hello code shown in hello preceding **Ingress** method.</span></span>

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

<span data-ttu-id="82d03-118">如果您想 toowork 直接與 hello Azure 儲存體 API，您可以加入**CloudStorageAccount**參數 toohello 方法簽章。</span><span class="sxs-lookup"><span data-stu-id="82d03-118">If you want toowork directly with hello Azure storage API, you can add a **CloudStorageAccount** parameter toohello method signature.</span></span>

## <a name="real-time-monitoring"></a><span data-ttu-id="82d03-119">即時監視</span><span class="sxs-lookup"><span data-stu-id="82d03-119">Real-time monitoring</span></span>
<span data-ttu-id="82d03-120">資料輸入函式通常會處理大型資料磁碟區，因為 hello WebJobs SDK 儀表板會提供即時監視資料。</span><span class="sxs-lookup"><span data-stu-id="82d03-120">Because data ingress functions often process large volumes of data, hello WebJobs SDK dashboard provides real-time monitoring data.</span></span> <span data-ttu-id="82d03-121">hello**引動過程記錄**一節說明您是否 hello 函式仍在執行。</span><span class="sxs-lookup"><span data-stu-id="82d03-121">hello **Invocation Log** section tells you if hello function is still running.</span></span>

![輸入函式執行中](./media/vs-storage-webjobs-getting-started-tables/ingressrunning.png)

<span data-ttu-id="82d03-123">hello**引動過程詳細資料**頁面會報告 hello 函式的進度 （寫入的實體數目） 時正在執行，而且可讓您有機會 tooabort 它。</span><span class="sxs-lookup"><span data-stu-id="82d03-123">hello **Invocation Details** page reports hello function's progress (number of entities written) while it's running and gives you an opportunity tooabort it.</span></span>

![輸入函式執行中](./media/vs-storage-webjobs-getting-started-tables/ingressprogress.png)

<span data-ttu-id="82d03-125">當 hello 函式完成時 hello**引動過程詳細資料**頁面會報告 hello 寫入的資料列數目。</span><span class="sxs-lookup"><span data-stu-id="82d03-125">When hello function finishes, hello **Invocation Details** page reports hello number of rows written.</span></span>

![輸入函式已完成](./media/vs-storage-webjobs-getting-started-tables/ingresssuccess.png)

## <a name="how-tooread-multiple-entities-from-a-table"></a><span data-ttu-id="82d03-127">如何 tooread 資料表中的多個實體</span><span class="sxs-lookup"><span data-stu-id="82d03-127">How tooread multiple entities from a table</span></span>
<span data-ttu-id="82d03-128">tooread 資料表時，使用 hello**資料表**屬性附帶**IQueryable<T>** 參數在其中輸入**T**衍生自**TableEntity**或實作**ITableEntity**。</span><span class="sxs-lookup"><span data-stu-id="82d03-128">tooread a table, use hello **Table** attribute with an **IQueryable<T>** parameter where type **T** derives from **TableEntity** or implements **ITableEntity**.</span></span>

<span data-ttu-id="82d03-129">hello 下列程式碼範例會讀取並記錄的所有資料列從 hello**輸入**資料表：</span><span class="sxs-lookup"><span data-stu-id="82d03-129">hello following code sample reads and logs all rows from hello **Ingress** table:</span></span>

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

### <a name="how-tooread-a-single-entity-from-a-table"></a><span data-ttu-id="82d03-130">如何從資料表的單一實體 tooread</span><span class="sxs-lookup"><span data-stu-id="82d03-130">How tooread a single entity from a table</span></span>
<span data-ttu-id="82d03-131">沒有**資料表**具有兩個額外的參數，可讓您指定 hello 資料分割索引鍵和資料列索引鍵，當您想 toobind tooa 單一資料表實體的屬性建構函式。</span><span class="sxs-lookup"><span data-stu-id="82d03-131">There is a **Table** attribute constructor with two additional parameters that let you specify hello partition key and row key when you want toobind tooa single table entity.</span></span>

<span data-ttu-id="82d03-132">hello 下列程式碼範例讀取的資料表資料列的**人員**根據資料分割索引鍵和資料列索引鍵值接收佇列訊息中的實體：</span><span class="sxs-lookup"><span data-stu-id="82d03-132">hello following code sample reads a table row for a **Person** entity based on partition key and row key values received in a queue message:</span></span>  

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


<span data-ttu-id="82d03-133">hello**人員**在此範例中的類別並沒有 tooimplement **ITableEntity**。</span><span class="sxs-lookup"><span data-stu-id="82d03-133">hello **Person** class in this example does not have tooimplement **ITableEntity**.</span></span>

## <a name="how-toouse-hello-net-storage-api-directly-toowork-with-a-table"></a><span data-ttu-id="82d03-134">如何 toouse hello.NET 儲存體 API 直接 toowork 與資料表</span><span class="sxs-lookup"><span data-stu-id="82d03-134">How toouse hello .NET Storage API directly toowork with a table</span></span>
<span data-ttu-id="82d03-135">您也可以使用 hello**資料表**屬性附帶**CloudTable**更靈活地使用資料表的物件。</span><span class="sxs-lookup"><span data-stu-id="82d03-135">You can also use hello **Table** attribute with a **CloudTable** object for more flexibility in working with a table.</span></span>

<span data-ttu-id="82d03-136">hello 下列程式碼範例使用**CloudTable**物件 tooadd 單一實體 toohello*輸入*資料表。</span><span class="sxs-lookup"><span data-stu-id="82d03-136">hello following code sample uses a **CloudTable** object tooadd a single entity toohello *Ingress* table.</span></span>

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

<span data-ttu-id="82d03-137">如需有關如何 toouse hello **CloudTable**物件，請參閱[開始使用適用於.NET 的 Azure 資料表儲存體使用](storage-dotnet-how-to-use-tables.md)。</span><span class="sxs-lookup"><span data-stu-id="82d03-137">For more information about how toouse hello **CloudTable** object, see [Get started with Azure Table storage using .NET](storage-dotnet-how-to-use-tables.md).</span></span>

## <a name="related-topics-covered-by-hello-queues-how-tooarticle"></a><span data-ttu-id="82d03-138">Hello 佇列如何 tooarticle 所涵蓋的相關的主題</span><span class="sxs-lookup"><span data-stu-id="82d03-138">Related topics covered by hello queues how-tooarticle</span></span>
<span data-ttu-id="82d03-139">如需如何 toohandle 資料表處理觸發佇列訊息，或 WebJobs SDK 案例不處理，請參閱特定 tootable[開始使用 Azure 佇列儲存體和 Visual Studio 已連接服務 （WebJob 專案）](vs-storage-webjobs-getting-started-queues.md).</span><span class="sxs-lookup"><span data-stu-id="82d03-139">For information about how toohandle table processing triggered by a queue message, or for WebJobs SDK scenarios not specific tootable processing, see [Getting started with Azure Queue storage and Visual Studio connected services (WebJob Projects)](vs-storage-webjobs-getting-started-queues.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="82d03-140">後續步驟</span><span class="sxs-lookup"><span data-stu-id="82d03-140">Next steps</span></span>
<span data-ttu-id="82d03-141">本文提供的程式碼範例會顯示如何使用 Azure 資料表的 toohandle 常見案例。</span><span class="sxs-lookup"><span data-stu-id="82d03-141">This article has provided code samples that show how toohandle common scenarios for working with Azure tables.</span></span> <span data-ttu-id="82d03-142">如需有關如何 toouse Azure WebJobs 和 hello WebJobs SDK，請參閱[Azure WebJobs 文件資源](http://go.microsoft.com/fwlink/?linkid=390226)。</span><span class="sxs-lookup"><span data-stu-id="82d03-142">For more information about how toouse Azure WebJobs and hello WebJobs SDK, see [Azure WebJobs documentation resources](http://go.microsoft.com/fwlink/?linkid=390226).</span></span>

