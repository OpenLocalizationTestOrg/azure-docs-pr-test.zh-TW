---
title: "從使用標準.NET 的 Azure 事件中樞 aaaReceive 事件 |Microsoft 文件"
description: "開始接收訊息以 hello EventProcessorHost.NET 標準"
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/27/2017
ms.author: sethm
ms.openlocfilehash: c3983f2668ac8f65522e44a1609dfd2eed31b7d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-receiving-messages-with-hello-event-processor-host-in-net-standard"></a>開始在標準.NET 中接收訊息以 hello 事件處理器主機

> [!NOTE]
> 您可在 [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleEphReceiver) 上取得此範例。

本教學課程示範如何 toowrite.NET Core 主控台應用程式從事件中心接收訊息，使用**EventProcessorHost**。 您可以執行 hello [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleEphReceiver)做為方案的事件中樞與儲存體帳戶值，取代 hello 字串。 您可以遵循 hello 步驟在本教學課程 toocreate 自己。

## <a name="prerequisites"></a>必要條件

* [Microsoft Visual Studio 2015 或 2017](http://www.visualstudio.com)。 也支援在此教學課程使用 Visual Studio 2017，hello 範例，但 Visual Studio 2015。
* [.NET Core Visual Studio 2015 或 2017 工具](http://www.microsoft.com/net/core)。
* Azure 訂用帳戶。
* Azure 事件中樞命名空間。
* 一個 Azure 儲存體帳戶。

## <a name="create-an-event-hubs-namespace-and-an-event-hub"></a>建立事件中樞命名空間和事件中樞  

hello 第一個步驟是 toouse hello [Azure 入口網站](https://portal.azure.com)toocreate hello 事件中心的命名空間類型，並取得 hello 應用程式需要 toocommunicate 與 hello 事件中心的管理認證。 toocreate 命名空間和事件中心，請依照下列中的 hello 程序[本文](event-hubs-create.md)，再繼續執行步驟的 hello。  

## <a name="create-an-azure-storage-account"></a>建立 Azure 儲存體帳戶  

1. 登入 toohello [Azure 入口網站](https://portal.azure.com)。  
2. 在 hello hello 入口網站的左側瀏覽窗格中按一下**新增**，按一下 **儲存體**，然後按一下**儲存體帳戶**。  
3. 完成 hello 欄位在 hello 儲存體帳戶 刀鋒視窗，然後再按一下**建立**。

    ![建立儲存體帳戶][1]

4. Vez que aparezca hello**部署成功**訊息中，按一下 hello hello 新的儲存體帳戶名稱。 在 hello **Essentials**刀鋒視窗中，按一下  **Blob**。 當 hello **Blob 服務**開啟刀鋒視窗中，按一下**+ 容器**hello 頂端。 指定的名稱，hello 容器，然後關閉 hello **Blob 服務**刀鋒視窗。  
5. 按一下**存取金鑰**hello 左刀鋒視窗，然後複製 hello 名稱中的 hello 儲存體容器、 hello 儲存體帳戶，以及 hello 值**key1**。 儲存這些值 tooNotepad 或一些其他的暫存位置。  

## <a name="create-a-console-application"></a>建立主控台應用程式

啟動 Visual Studio。 從 hello**檔案**功能表上，按一下 **新增**，然後按一下**專案**。 建立 .NET Core 主控台應用程式。

![新增專案][2]

## <a name="add-hello-event-hubs-nuget-package"></a>加入 hello 事件中心 NuGet 封裝

新增 hello [ `Microsoft.Azure.EventHubs` ](https://www.nuget.org/packages/Microsoft.Azure.EventHubs/)和[ `Microsoft.Azure.EventHubs.Processor` ](https://www.nuget.org/packages/Microsoft.Azure.EventHubs.Processor/) .NET 標準程式庫 NuGet 封裝 tooyour 專案依照下列步驟： 

1. Hello 新建立的專案上按一下滑鼠右鍵，然後選取**管理 NuGet 封裝**。
2. 按一下 hello**瀏覽** 索引標籤，然後搜尋 「 Microsoft.Azure.EventHubs 」 和選取 hello **Microsoft.Azure.EventHubs**封裝。 按一下**安裝**toocomplete hello 安裝，然後關閉此對話方塊。
3. 重複步驟 1 和 2，並安裝 hello **Microsoft.Azure.EventHubs.Processor**封裝。

## <a name="implement-hello-ieventprocessor-interface"></a>實作 hello IEventProcessor 介面

1. 在 方案總管 中，以滑鼠右鍵按一下 hello 專案中，按一下 **新增**，然後按一下**類別**。 Hello 新類別命名**SimpleEventProcessor**。

2. 開啟 hello SimpleEventProcessor.cs 檔案並加入下列 hello `using` hello 檔案的陳述式 toohello 頂端。

    ```csharp
    using Microsoft.Azure.EventHubs;
    using Microsoft.Azure.EventHubs.Processor;
    using System.Threading.Tasks;
    ```

3. 實作 hello`IEventProcessor`介面。 取代 hello hello 整個內容`SimpleEventProcessor`類別以下列程式碼的 hello:

    ```csharp
    public class SimpleEventProcessor : IEventProcessor
    {
        public Task CloseAsync(PartitionContext context, CloseReason reason)
        {
            Console.WriteLine($"Processor Shutting Down. Partition '{context.PartitionId}', Reason: '{reason}'.");
            return Task.CompletedTask;
        }

        public Task OpenAsync(PartitionContext context)
        {
            Console.WriteLine($"SimpleEventProcessor initialized. Partition: '{context.PartitionId}'");
            return Task.CompletedTask;
        }

        public Task ProcessErrorAsync(PartitionContext context, Exception error)
        {
            Console.WriteLine($"Error on Partition: {context.PartitionId}, Error: {error.Message}");
            return Task.CompletedTask;
        }

        public Task ProcessEventsAsync(PartitionContext context, IEnumerable<EventData> messages)
        {
            foreach (var eventData in messages)
            {
                var data = Encoding.UTF8.GetString(eventData.Body.Array, eventData.Body.Offset, eventData.Body.Count);
                Console.WriteLine($"Message received. Partition: '{context.PartitionId}', Data: '{data}'");
            }

            return context.CheckpointAsync();
        }
    }
    ```

## <a name="write-a-main-console-method-that-uses-hello-simpleeventprocessor-class-tooreceive-messages"></a>撰寫使用 hello SimpleEventProcessor 類別 tooreceive 訊息主控台方法

1. 新增下列 hello `using` hello Program.cs 檔案的陳述式 toohello 頂端。

    ```csharp
    using Microsoft.Azure.EventHubs;
    using Microsoft.Azure.EventHubs.Processor;
    using System.Threading.Tasks;
    ```

2. 新增常數 toohello `Program` hello 事件中樞連接字串、 事件中樞的名稱、 儲存體帳戶容器的名稱、 儲存體帳戶名稱，和儲存體帳戶金鑰的類別。 新增下列程式碼，其相對應值取代 hello 預留位置 hello。

    ```csharp
    private const string EhConnectionString = "{Event Hubs connection string}";
    private const string EhEntityPath = "{Event Hub path/name}";
    private const string StorageContainerName = "{Storage account container name}";
    private const string StorageAccountName = "{Storage account name}";
    private const string StorageAccountKey = "{Storage account key}";

    private static readonly string StorageConnectionString = string.Format("DefaultEndpointsProtocol=https;AccountName={0};AccountKey={1}", StorageAccountName, StorageAccountKey);
    ```   

3. 新增名為方法`MainAsync`toohello`Program`類別，如下所示：

    ```csharp
    private static async Task MainAsync(string[] args)
    {
        Console.WriteLine("Registering EventProcessor...");

        var eventProcessorHost = new EventProcessorHost(
            EhEntityPath,
            PartitionReceiver.DefaultConsumerGroupName,
            EhConnectionString,
            StorageConnectionString,
            StorageContainerName);

        // Registers hello Event Processor Host and starts receiving messages
        await eventProcessorHost.RegisterEventProcessorAsync<SimpleEventProcessor>();

        Console.WriteLine("Receiving. Press ENTER toostop worker.");
        Console.ReadLine();

        // Disposes of hello Event Processor Host
        await eventProcessorHost.UnregisterEventProcessorAsync();
    }
    ```

3. 新增下列一行程式碼 toohello hello`Main`方法：

    ```csharp
    MainAsync(args).GetAwaiter().GetResult();
    ```

    Program.cs 檔案看起來應該會像下面這樣：

    ```csharp
    namespace SampleEphReceiver
    {

        public class Program
        {
            private const string EhConnectionString = "{Event Hubs connection string}";
            private const string EhEntityPath = "{Event Hub path/name}";
            private const string StorageContainerName = "{Storage account container name}";
            private const string StorageAccountName = "{Storage account name}";
            private const string StorageAccountKey = "{Storage account key}";

            private static readonly string StorageConnectionString = string.Format("DefaultEndpointsProtocol=https;AccountName={0};AccountKey={1}", StorageAccountName, StorageAccountKey);

            public static void Main(string[] args)
            {
                MainAsync(args).GetAwaiter().GetResult();
            }

            private static async Task MainAsync(string[] args)
            {
                Console.WriteLine("Registering EventProcessor...");

                var eventProcessorHost = new EventProcessorHost(
                    EhEntityPath,
                    PartitionReceiver.DefaultConsumerGroupName,
                    EhConnectionString,
                    StorageConnectionString,
                    StorageContainerName);

                // Registers hello Event Processor Host and starts receiving messages
                await eventProcessorHost.RegisterEventProcessorAsync<SimpleEventProcessor>();

                Console.WriteLine("Receiving. Press ENTER toostop worker.");
                Console.ReadLine();

                // Disposes of hello Event Processor Host
                await eventProcessorHost.UnregisterEventProcessorAsync();
            }
        }
    }
    ```

4. 執行 hello 程式，並確定沒有任何錯誤。

恭喜！ 您現在已從事件中心接收訊息，使用 hello 事件處理器主機。

## <a name="next-steps"></a>後續步驟
您可以進一步了解事件中心瀏覽下列連結查看 hello:

* [事件中樞概觀](event-hubs-what-is-event-hubs.md)
* [建立事件中樞](event-hubs-create.md)
* [事件中樞常見問題集](event-hubs-faq.md)

[1]: ./media/event-hubs-dotnet-standard-getstarted-receive-eph/event-hubs-python1.png
[2]: ./media/event-hubs-dotnet-standard-getstarted-receive-eph/netcore.png
