---
title: "開始使用 Azure 儲存體和 Visual Studio 已連接服務 (WebJob 專案)"
description: "在使用 Visual Studio 已連接服務連接到儲存體帳戶之後，如何於 Visual Studio Azure WebJobs 專案中開始使用 Azure 資料表儲存體"
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
ms.openlocfilehash: 79fba102377cdc6b681f6798699767961040a7e2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="getting-started-with-azure-storage-azure-webjob-projects"></a><span data-ttu-id="23a91-103">開始使用 Azure 儲存體 (Azure WebJob 專案)</span><span class="sxs-lookup"><span data-stu-id="23a91-103">Getting Started with Azure Storage (Azure WebJob Projects)</span></span>
[!INCLUDE [storage-try-azure-tools-tables](../../includes/storage-try-azure-tools-tables.md)]

## <a name="overview"></a><span data-ttu-id="23a91-104">概觀</span><span class="sxs-lookup"><span data-stu-id="23a91-104">Overview</span></span>
<span data-ttu-id="23a91-105">本文提供了 C# 程式碼範例，示範如何透過 Azure 資料表儲存體服務使用 Azure WebJobs SDK 1.x 版。</span><span class="sxs-lookup"><span data-stu-id="23a91-105">This article provides C# code samples that show show how to use the Azure WebJobs SDK version 1.x with the Azure table storage service.</span></span> <span data-ttu-id="23a91-106">此程式碼範例會使用 [WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk.md) 1.x 版。</span><span class="sxs-lookup"><span data-stu-id="23a91-106">The code samples use the [WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk.md) version 1.x.</span></span>

<span data-ttu-id="23a91-107">Azure 資料表儲存體服務可讓您儲存大量的結構化資料。</span><span class="sxs-lookup"><span data-stu-id="23a91-107">The Azure Table storage service enables you to store large amounts of structured data.</span></span> <span data-ttu-id="23a91-108">此服務是一個 NoSQL 資料存放區，接受來自 Azure 雲端內外經過驗證的呼叫。</span><span class="sxs-lookup"><span data-stu-id="23a91-108">The service is a NoSQL datastore that accepts authenticated calls from inside and outside the Azure cloud.</span></span> <span data-ttu-id="23a91-109">Azure 資料表很適合儲存結構化、非關聯式資料。</span><span class="sxs-lookup"><span data-stu-id="23a91-109">Azure tables are ideal for storing structured, non-relational data.</span></span>  <span data-ttu-id="23a91-110">如需詳細資訊，請參閱 [以 .NET 開始使用 Azure 資料表儲存體](storage-dotnet-how-to-use-tables.md#create-a-table) 。</span><span class="sxs-lookup"><span data-stu-id="23a91-110">See [Get started with Azure Table storage using .NET](storage-dotnet-how-to-use-tables.md#create-a-table) for more information.</span></span>

<span data-ttu-id="23a91-111">有一些程式碼片段顯示用於以手動方式呼叫函式的 **Table** 屬性，亦即不是使用其中一個觸發程序屬性。</span><span class="sxs-lookup"><span data-stu-id="23a91-111">Some of the code snippets show the **Table** attribute used in functions that are called manually, that is, not by using one of the trigger attributes.</span></span>

## <a name="how-to-add-entities-to-a-table"></a><span data-ttu-id="23a91-112">如何將實體新增至資料表</span><span class="sxs-lookup"><span data-stu-id="23a91-112">How to add entities to a table</span></span>
<span data-ttu-id="23a91-113">若要將實體新增至資料表，請將 **Table** 屬性搭配 **ICollector<T>** 或 **IAsyncCollector<T>** 參數使用，其中 **T** 會指定您想要加入之實體的結構描述。</span><span class="sxs-lookup"><span data-stu-id="23a91-113">To add entities to a table, use the **Table** attribute with an **ICollector<T>** or **IAsyncCollector<T>** parameter where **T** specifies the schema of the entities you want to add.</span></span> <span data-ttu-id="23a91-114">屬性建構函式採用字串參數，來指定資料表的名稱。</span><span class="sxs-lookup"><span data-stu-id="23a91-114">The attribute constructor takes a string parameter that specifies the name of the table.</span></span>

<span data-ttu-id="23a91-115">以下程式碼範例會將 **Person** 實體加入名為 *Ingress*的資料表。</span><span class="sxs-lookup"><span data-stu-id="23a91-115">The following code sample adds **Person** entities to a table named *Ingress*.</span></span>

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

<span data-ttu-id="23a91-116">通常您搭配 **ICollector** 使用的類型是衍生自 **TableEntity** 或實作 **ITableEntity** 而得，但其實並不需要這麼做。</span><span class="sxs-lookup"><span data-stu-id="23a91-116">Typically the type you use with **ICollector** derives from **TableEntity** or implements **ITableEntity**, but it doesn't have to.</span></span> <span data-ttu-id="23a91-117">下列任一 **Person** 類別都能搭配前面 **Ingress** 方法中所示的程式碼使用。</span><span class="sxs-lookup"><span data-stu-id="23a91-117">Either of the following **Person** classes work with the code shown in the preceding **Ingress** method.</span></span>

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

<span data-ttu-id="23a91-118">如果您想要直接使用 Azure 儲存體 API，可將 **CloudStorageAccount** 參數新增至方法簽章。</span><span class="sxs-lookup"><span data-stu-id="23a91-118">If you want to work directly with the Azure storage API, you can add a **CloudStorageAccount** parameter to the method signature.</span></span>

## <a name="real-time-monitoring"></a><span data-ttu-id="23a91-119">即時監視</span><span class="sxs-lookup"><span data-stu-id="23a91-119">Real-time monitoring</span></span>
<span data-ttu-id="23a91-120">因為資料外送流量函式經常處理大量資料，所以 WebJobs SDK 儀表板提供即時監視資料。</span><span class="sxs-lookup"><span data-stu-id="23a91-120">Because data ingress functions often process large volumes of data, the WebJobs SDK dashboard provides real-time monitoring data.</span></span> <span data-ttu-id="23a91-121">[引動過程記錄]  區段可告訴您是否仍有執行中的函式。</span><span class="sxs-lookup"><span data-stu-id="23a91-121">The **Invocation Log** section tells you if the function is still running.</span></span>

![輸入函式執行中](./media/vs-storage-webjobs-getting-started-tables/ingressrunning.png)

<span data-ttu-id="23a91-123">[引動過程詳細資料]  頁面會報告執行中函式的進度 (寫入的實體數目)，並讓您有機會將它中止。</span><span class="sxs-lookup"><span data-stu-id="23a91-123">The **Invocation Details** page reports the function's progress (number of entities written) while it's running and gives you an opportunity to abort it.</span></span>

![輸入函式執行中](./media/vs-storage-webjobs-getting-started-tables/ingressprogress.png)

<span data-ttu-id="23a91-125">當函式完成時，[引動過程詳細資料]  頁面會報告寫入的資料列數目。</span><span class="sxs-lookup"><span data-stu-id="23a91-125">When the function finishes, the **Invocation Details** page reports the number of rows written.</span></span>

![輸入函式已完成](./media/vs-storage-webjobs-getting-started-tables/ingresssuccess.png)

## <a name="how-to-read-multiple-entities-from-a-table"></a><span data-ttu-id="23a91-127">如何讀取資料表中的多個實體</span><span class="sxs-lookup"><span data-stu-id="23a91-127">How to read multiple entities from a table</span></span>
<span data-ttu-id="23a91-128">若要讀取資料表，請使用 **Table** 屬性與 **IQueryable<T>** 參數，其中類型 **T** 是衍生自 **TableEntity** 或實作 **ITableEntity** 而得。</span><span class="sxs-lookup"><span data-stu-id="23a91-128">To read a table, use the **Table** attribute with an **IQueryable<T>** parameter where type **T** derives from **TableEntity** or implements **ITableEntity**.</span></span>

<span data-ttu-id="23a91-129">下列程式碼範例會讀取並記錄 **Ingress** 資料表中的所有資料列：</span><span class="sxs-lookup"><span data-stu-id="23a91-129">The following code sample reads and logs all rows from the **Ingress** table:</span></span>

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

### <a name="how-to-read-a-single-entity-from-a-table"></a><span data-ttu-id="23a91-130">如何讀取資料表中的單一實體</span><span class="sxs-lookup"><span data-stu-id="23a91-130">How to read a single entity from a table</span></span>
<span data-ttu-id="23a91-131">**Table** 屬性建構函式搭配兩個額外參數，可在想要繫結到單一資料表實體時，讓您指定資料分割索引鍵與資料列索引鍵。</span><span class="sxs-lookup"><span data-stu-id="23a91-131">There is a **Table** attribute constructor with two additional parameters that let you specify the partition key and row key when you want to bind to a single table entity.</span></span>

<span data-ttu-id="23a91-132">下列程式碼範例會根據在佇列訊息中收到的資料分割索引鍵與資料列索引鍵值，來讀取 **Person** 實體的資料表列：</span><span class="sxs-lookup"><span data-stu-id="23a91-132">The following code sample reads a table row for a **Person** entity based on partition key and row key values received in a queue message:</span></span>  

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


<span data-ttu-id="23a91-133">本範例中的 **Person** 類別不必實作 **ITableEntity**。</span><span class="sxs-lookup"><span data-stu-id="23a91-133">The **Person** class in this example does not have to implement **ITableEntity**.</span></span>

## <a name="how-to-use-the-net-storage-api-directly-to-work-with-a-table"></a><span data-ttu-id="23a91-134">如何直接利用 .NET 儲存體 API 來使用資料表</span><span class="sxs-lookup"><span data-stu-id="23a91-134">How to use the .NET Storage API directly to work with a table</span></span>
<span data-ttu-id="23a91-135">您也可以使用 **Table** 屬性搭配 **CloudTable** 物件，以更有彈性的方式使用資料表。</span><span class="sxs-lookup"><span data-stu-id="23a91-135">You can also use the **Table** attribute with a **CloudTable** object for more flexibility in working with a table.</span></span>

<span data-ttu-id="23a91-136">下列程式碼範例使用 **CloudTable** 物件將單一實體新增至 *Ingress* 資料表。</span><span class="sxs-lookup"><span data-stu-id="23a91-136">The following code sample uses a **CloudTable** object to add a single entity to the *Ingress* table.</span></span>

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

<span data-ttu-id="23a91-137">如需如何使用 **CloudTable** 物件的詳細資訊，請參閱 [以 .NET 開始使用 Azure 資料表儲存體](storage-dotnet-how-to-use-tables.md)。</span><span class="sxs-lookup"><span data-stu-id="23a91-137">For more information about how to use the **CloudTable** object, see [Get started with Azure Table storage using .NET](storage-dotnet-how-to-use-tables.md).</span></span>

## <a name="related-topics-covered-by-the-queues-how-to-article"></a><span data-ttu-id="23a91-138">佇列操作說明文章所涵蓋的相關主題</span><span class="sxs-lookup"><span data-stu-id="23a91-138">Related topics covered by the queues how-to article</span></span>
<span data-ttu-id="23a91-139">如需如何處理佇列訊息所觸發的資料表處理相關資訊，或是非資料表處理特有的 WebJobs SDK 案例，請參閱 [開始使用 Azure 佇列儲存體和 Visual Studio 已連接服務 (WebJob 專案)](vs-storage-webjobs-getting-started-queues.md)。</span><span class="sxs-lookup"><span data-stu-id="23a91-139">For information about how to handle table processing triggered by a queue message, or for WebJobs SDK scenarios not specific to table processing, see [Getting started with Azure Queue storage and Visual Studio connected services (WebJob Projects)](vs-storage-webjobs-getting-started-queues.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="23a91-140">後續步驟</span><span class="sxs-lookup"><span data-stu-id="23a91-140">Next steps</span></span>
<span data-ttu-id="23a91-141">本文提供的程式碼範例示範如何處理使用 Azure 資料表的常見案例。</span><span class="sxs-lookup"><span data-stu-id="23a91-141">This article has provided code samples that show how to handle common scenarios for working with Azure tables.</span></span> <span data-ttu-id="23a91-142">如需如何使用 Azure WebJobs 和 WebJobs SDK 的詳細資訊，請參閱 [Azure WebJobs 文件資源](http://go.microsoft.com/fwlink/?linkid=390226)。</span><span class="sxs-lookup"><span data-stu-id="23a91-142">For more information about how to use Azure WebJobs and the WebJobs SDK, see [Azure WebJobs documentation resources](http://go.microsoft.com/fwlink/?linkid=390226).</span></span>

