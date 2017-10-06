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
# <a name="how-toouse-azure-table-storage-with-hello-webjobs-sdk"></a>如何 toouse Azure 資料表儲存體與 hello WebJobs SDK
## <a name="overview"></a>概觀
本指南提供的 C# 程式碼範例 tooread 」 和 「 寫入 Azure 儲存體資料表所使用的方式，顯示[WebJobs SDK](websites-dotnet-webjobs-sdk.md)版本 1.x。

hello 指南假設您知道[toocreate WebJob 專案在 Visual Studio 中使用連接字串該點 tooyour 儲存體帳戶的方式](websites-dotnet-webjobs-sdk-get-started.md)或太[多個儲存體帳戶](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs)。

有些 hello 程式碼片段會顯示 hello`Table`函式中使用的屬性[以手動方式呼叫](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#manual)，也就是不是使用其中一個 hello 觸發程序屬性。 

## <a id="ingress"></a>如何 tooadd 實體 tooa 資料表
tooadd 實體 tooa 資料表，使用 hello`Table`屬性附帶`ICollector<T>`或`IAsyncCollector<T>`參數其中`T`指定 hello 結構描述要 tooadd 的 hello 實體。 hello 屬性建構函式接受字串參數，指定 hello hello 資料表名稱。 

hello 下列程式碼範例會將`Person`實體 tooa 資料表名為*輸入*。

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

通常 hello 要使用的類型`ICollector`衍生自`TableEntity`或實作`ITableEntity`，但不一定要。 Hello 下列任一`Person`類別與 hello hello 前面所示的程式碼的工作`Ingress`方法。

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

如果您想 toowork 直接與 hello Azure 儲存體 API，您可以加入`CloudStorageAccount`參數 toohello 方法簽章。

## <a id="monitor"></a> 即時監視
資料輸入函式通常會處理大型資料磁碟區，因為 hello WebJobs SDK 儀表板會提供即時監視資料。 hello**引動過程記錄**一節說明您是否 hello 函式仍在執行。

![輸入函式執行中](./media/websites-dotnet-webjobs-sdk-storage-tables-how-to/ingressrunning.png)

hello**引動過程詳細資料**頁面會報告 hello 函式的進度 （寫入的實體數目） 時正在執行，而且可讓您有機會 tooabort 它。 

![輸入函式執行中](./media/websites-dotnet-webjobs-sdk-storage-tables-how-to/ingressprogress.png)

當 hello 函式完成時 hello**引動過程詳細資料**頁面會報告 hello 寫入的資料列數目。

![輸入函式已完成](./media/websites-dotnet-webjobs-sdk-storage-tables-how-to/ingresssuccess.png)

## <a id="multiple"></a>如何 tooread 資料表中的多個實體
tooread 資料表時，使用 hello`Table`屬性附帶`IQueryable<T>`參數在其中輸入`T`衍生自`TableEntity`或實作`ITableEntity`。

hello 下列程式碼範例會讀取並記錄的所有資料列從 hello`Ingress`資料表：

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

### <a id="readone"></a>如何從資料表的單一實體 tooread
沒有`Table`具有兩個額外的參數，可讓您指定 hello 資料分割索引鍵和資料列索引鍵，當您想 toobind tooa 單一資料表實體的屬性建構函式。

hello 下列程式碼範例讀取的資料表資料列的`Person`根據資料分割索引鍵和資料列索引鍵值接收佇列訊息中的實體：  

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


hello`Person`在此範例中的類別並沒有 tooimplement `ITableEntity`。

## <a id="storageapi"></a>如何 toouse hello.NET 儲存體 API 直接 toowork 與資料表
您也可以使用 hello`Table`屬性附帶`CloudTable`更靈活地使用資料表的物件。

hello 下列程式碼範例使用`CloudTable`物件 tooadd 單一實體 toohello*輸入*資料表。 

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

如需有關如何 toouse hello`CloudTable`物件，請參閱[如何 toouse 資料表儲存體從.NET](../cosmos-db/table-storage-how-to-use-dotnet.md)。 

## <a id="queues"></a>Hello 佇列如何 tooarticle 所涵蓋的相關的主題
如需如何 toohandle 資料表處理觸發佇列訊息，或 WebJobs SDK 案例不處理，請參閱特定 tootable[如何 toouse Azure 佇列儲存體與 hello WebJobs SDK](websites-dotnet-webjobs-sdk-storage-queues-how-to.md)。 

在該文件中涵蓋的主題包括下列 hello:

* Async 函數
* 多個執行個體
* 正常關機
* 使用 WebJobs SDK hello 函式主體中的屬性
* 程式碼中設定 hello SDK 連接字串
* 在程式碼中設定 WebJobs SDK 建構函式參數的值
* 手動觸發函式
* 寫入記錄檔

## <a id="nextsteps"></a> 後續步驟
本指南提供的程式碼範例會顯示如何使用 Azure 資料表的 toohandle 常見案例。 如需有關如何 toouse Azure WebJobs 和 hello WebJobs SDK，請參閱[Azure WebJobs 建議資源](http://go.microsoft.com/fwlink/?linkid=390226)。

