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
# <a name="getting-started-with-azure-storage-azure-webjob-projects"></a>開始使用 Azure 儲存體 (Azure WebJob 專案)
[!INCLUDE [storage-try-azure-tools-tables](../../includes/storage-try-azure-tools-tables.md)]

## <a name="overview"></a>概觀
本文章提供 C# 程式碼範例，示範顯示如何 toouse hello Azure WebJobs SDK 版本 1.x 以 hello Azure 資料表儲存體服務。 hello 程式碼範例使用 hello [WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk.md)版本 1.x。

hello Azure 資料表儲存體服務可讓您 toostore 大量結構化資料。 hello 服務是可接受來自內部和外部 hello Azure 雲端的已驗證的呼叫的 NoSQL 資料存放區。 Azure 資料表很適合儲存結構化、非關聯式資料。  如需詳細資訊，請參閱 [以 .NET 開始使用 Azure 資料表儲存體](storage-dotnet-how-to-use-tables.md#create-a-table) 。

有些 hello 程式碼片段會顯示 hello**資料表**用於呼叫的函式以手動方式，亦即，不是使用其中一個 hello 觸發程序屬性的屬性。

## <a name="how-tooadd-entities-tooa-table"></a>如何 tooadd 實體 tooa 資料表
tooadd 實體 tooa 資料表，使用 hello**資料表**屬性附帶**ICollector<T>** 或**IAsyncCollector<T>** 參數其中**T**指定 hello 結構描述要 tooadd 的 hello 實體。 hello 屬性建構函式接受字串參數，指定 hello hello 資料表名稱。

hello 下列程式碼範例會將**人員**實體 tooa 資料表名為*輸入*。

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

通常 hello 要使用的類型**ICollector**衍生自**TableEntity**或實作**ITableEntity**，但不一定要。 Hello 下列任一**人員**類別與 hello hello 前面所示的程式碼的工作**輸入**方法。

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

如果您想 toowork 直接與 hello Azure 儲存體 API，您可以加入**CloudStorageAccount**參數 toohello 方法簽章。

## <a name="real-time-monitoring"></a>即時監視
資料輸入函式通常會處理大型資料磁碟區，因為 hello WebJobs SDK 儀表板會提供即時監視資料。 hello**引動過程記錄**一節說明您是否 hello 函式仍在執行。

![輸入函式執行中](./media/vs-storage-webjobs-getting-started-tables/ingressrunning.png)

hello**引動過程詳細資料**頁面會報告 hello 函式的進度 （寫入的實體數目） 時正在執行，而且可讓您有機會 tooabort 它。

![輸入函式執行中](./media/vs-storage-webjobs-getting-started-tables/ingressprogress.png)

當 hello 函式完成時 hello**引動過程詳細資料**頁面會報告 hello 寫入的資料列數目。

![輸入函式已完成](./media/vs-storage-webjobs-getting-started-tables/ingresssuccess.png)

## <a name="how-tooread-multiple-entities-from-a-table"></a>如何 tooread 資料表中的多個實體
tooread 資料表時，使用 hello**資料表**屬性附帶**IQueryable<T>** 參數在其中輸入**T**衍生自**TableEntity**或實作**ITableEntity**。

hello 下列程式碼範例會讀取並記錄的所有資料列從 hello**輸入**資料表：

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

### <a name="how-tooread-a-single-entity-from-a-table"></a>如何從資料表的單一實體 tooread
沒有**資料表**具有兩個額外的參數，可讓您指定 hello 資料分割索引鍵和資料列索引鍵，當您想 toobind tooa 單一資料表實體的屬性建構函式。

hello 下列程式碼範例讀取的資料表資料列的**人員**根據資料分割索引鍵和資料列索引鍵值接收佇列訊息中的實體：  

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


hello**人員**在此範例中的類別並沒有 tooimplement **ITableEntity**。

## <a name="how-toouse-hello-net-storage-api-directly-toowork-with-a-table"></a>如何 toouse hello.NET 儲存體 API 直接 toowork 與資料表
您也可以使用 hello**資料表**屬性附帶**CloudTable**更靈活地使用資料表的物件。

hello 下列程式碼範例使用**CloudTable**物件 tooadd 單一實體 toohello*輸入*資料表。

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

如需有關如何 toouse hello **CloudTable**物件，請參閱[開始使用適用於.NET 的 Azure 資料表儲存體使用](storage-dotnet-how-to-use-tables.md)。

## <a name="related-topics-covered-by-hello-queues-how-tooarticle"></a>Hello 佇列如何 tooarticle 所涵蓋的相關的主題
如需如何 toohandle 資料表處理觸發佇列訊息，或 WebJobs SDK 案例不處理，請參閱特定 tootable[開始使用 Azure 佇列儲存體和 Visual Studio 已連接服務 （WebJob 專案）](vs-storage-webjobs-getting-started-queues.md).

## <a name="next-steps"></a>後續步驟
本文提供的程式碼範例會顯示如何使用 Azure 資料表的 toohandle 常見案例。 如需有關如何 toouse Azure WebJobs 和 hello WebJobs SDK，請參閱[Azure WebJobs 文件資源](http://go.microsoft.com/fwlink/?linkid=390226)。

