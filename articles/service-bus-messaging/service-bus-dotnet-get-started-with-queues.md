---
title: "開始使用 Azure Service Bus 佇列的 aaaGet |Microsoft 文件"
description: "撰寫使用服務匯流排傳訊佇列的 C# 主控台應用程式。"
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 68a34c00-5600-43f6-bbcc-fea599d500da
ms.service: service-bus-messaging
ms.devlang: tbd
ms.topic: hero-article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 06/26/2017
ms.author: sethm
ms.openlocfilehash: eaa362ab0eabd2427977398c1deab5dc00105ae9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-service-bus-queues"></a>開始使用服務匯流排佇列
[!INCLUDE [service-bus-selector-queues](../../includes/service-bus-selector-queues.md)]

## <a name="what-will-be-accomplished"></a>將會完成的工作
本教學課程涵蓋 hello 下列步驟：

1. 建立服務匯流排命名空間，使用 hello Azure 入口網站。
2. 建立服務匯流排佇列，使用 hello Azure 入口網站。
3. 訊息寫入主控台應用程式 toosend。
4. 撰寫主控台應用程式 tooreceive hello hello 上一個步驟中傳送的訊息。

## <a name="prerequisites"></a>必要條件
1. [Visual Studio 2015 或更新版本](http://www.visualstudio.com)。 在此教學課程中的 hello 範例會使用 Visual Studio 2017。
2. Azure 訂用帳戶。

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="1-create-a-namespace-using-hello-azure-portal"></a>1.建立命名空間使用 hello Azure 入口網站
如果您已經建立 Service Bus 訊息的命名空間，跳 toohello[建立佇列，使用 Azure 入口網站 hello](#2-create-a-queue-using-the-azure-portal) > 一節。

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="2-create-a-queue-using-hello-azure-portal"></a>2.建立佇列，使用 hello Azure 入口網站
如果您已經建立 Service Bus 佇列，跳 toohello[傳送訊息 toohello 佇列](#3-send-messages-to-the-queue)> 一節。

[!INCLUDE [service-bus-create-queue-portal](../../includes/service-bus-create-queue-portal.md)]

## <a name="3-send-messages-toohello-queue"></a>3.傳送訊息 toohello 佇列
toosend 訊息 toohello 佇列中，我們會撰寫 C# 主控台應用程式使用 Visual Studio。

### <a name="create-a-console-application"></a>建立主控台應用程式

啟動 Visual Studio，並建立新的**主控台應用程式 (.NET Framework)** 專案。

### <a name="add-hello-service-bus-nuget-package"></a>加入 hello 服務匯流排 NuGet 封裝
1. Hello 新建立的專案上按一下滑鼠右鍵，然後選取**管理 NuGet 封裝**。
2. 按一下 hello**瀏覽**索引標籤上，搜尋**Microsoft Azure 服務匯流排**，然後選取 hello **WindowsAzure.ServiceBus**項目。 按一下**安裝**toocomplete hello 安裝，然後關閉此對話方塊。
   
    ![選取 NuGet 封裝][nuget-pkg]

### <a name="write-some-code-toosend-a-message-toohello-queue"></a>撰寫一些程式碼 toosend 訊息 toohello 佇列
1. 新增下列 hello `using` hello Program.cs 檔案的陳述式 toohello 頂端。
   
    ```csharp
    using Microsoft.ServiceBus.Messaging;
    ```
2. 新增下列程式碼 toohello hello`Main`方法。 設定 hello`connectionString`變數 toohello 連接字串時建立 hello 命名空間中，取得及設定`queueName`toohello 建立 hello 佇列時所使用的佇列名稱。
   
    ```csharp
    var connectionString = "<your connection string>";
    var queueName = "<your queue name>";
   
    var client = QueueClient.CreateFromConnectionString(connectionString, queueName);
    var message = new BrokeredMessage("This is a test message!");

    Console.WriteLine(String.Format("Message id: {0}", message.MessageId));

    client.Send(message);

    Console.WriteLine("Message successfully sent! Press ENTER tooexit program");
    Console.ReadLine();
    ```
   
    Program.cs 檔案看起來應該會像下面這樣。
   
    ```csharp
    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Text;
    using System.Threading.Tasks;
    using Microsoft.ServiceBus.Messaging;

    namespace qsend
    {
        class Program
        {
            static void Main(string[] args)
            {
                var connectionString = "Endpoint=sb://<your namespace>.servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=<your key>";
                var queueName = "<your queue name>";

                var client = QueueClient.CreateFromConnectionString(connectionString, queueName);
                var message = new BrokeredMessage("This is a test message!");

                Console.WriteLine(String.Format("Message id: {0}", message.MessageId));

                client.Send(message);

                Console.WriteLine("Message successfully sent! Press ENTER tooexit program");
                Console.ReadLine();
            }
        }
    }
    ```
3. 執行 hello 程式並檢查 hello Azure 入口網站： 按一下您的佇列 hello 命名空間中的 hello 名稱**概觀**刀鋒視窗。 hello 佇列**Essentials**刀鋒視窗會顯示。 請注意該 hello**作用中的訊息計數**值現在應該是 1。 每的次您執行 hello 寄件者應用程式而不擷取 hello 訊息，這個值會增加 1。 也請注意 hello hello 佇列的目前的大小遞增每個時間 hello 應用程式會加入訊息 toohello 佇列。
   
      ![訊息大小][queue-message]

## <a name="4-receive-messages-from-hello-queue"></a>4.從 hello 佇列接收訊息

1. 只傳送 tooreceive hello 訊息建立新的主控台應用程式，並加入參考 toohello 服務匯流排 NuGet 封裝，類似 toohello 先前寄件者應用程式。
2. 新增下列 hello `using` hello Program.cs 檔案的陳述式 toohello 頂端。
   
    ```csharp
    using Microsoft.ServiceBus.Messaging;
    ```
3. 新增下列程式碼 toohello hello`Main`方法。 設定 hello`connectionString`變數 toohello 連接字串時建立 hello 命名空間、 取得和設定`queueName`toohello 建立 hello 佇列時所使用的佇列名稱。
   
    ```csharp
    var connectionString = "<your connection string>";
    var queueName = "<your queue name>";
   
    var client = QueueClient.CreateFromConnectionString(connectionString, queueName);
   
    client.OnMessage(message =>
    {
      Console.WriteLine(String.Format("Message body: {0}", message.GetBody<String>()));
      Console.WriteLine(String.Format("Message id: {0}", message.MessageId));
    });
   
    Console.WriteLine("Press ENTER tooexit program");
    Console.ReadLine();
    ```
   
    Program.cs 檔案看起來應該會像下面這樣：
   
    ```csharp
    using System;
    using Microsoft.ServiceBus.Messaging;
   
    namespace GettingStartedWithQueues
    {
      class Program
      {
        static void Main(string[] args)
        {
          var connectionString = "Endpoint=sb://<your namespace>.servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=<your key>";;
          var queueName = "<your queue name>";
   
          var client = QueueClient.CreateFromConnectionString(connectionString, queueName);
   
          client.OnMessage(message =>
          {
            Console.WriteLine(String.Format("Message body: {0}", message.GetBody<String>()));
            Console.WriteLine(String.Format("Message id: {0}", message.MessageId));
          });

          Console.WriteLine("Press ENTER tooexit program");   
          Console.ReadLine();
        }
      }
    }
    ```
4. 執行 hello 程式並再次檢查 hello 入口網站。 請注意該 hello**作用中的訊息計數**和**目前**值現在是 0。
   
    ![佇列長度][queue-message-receive]

恭喜！ 您現已建立佇列、傳送訊息和接收訊息。

## <a name="next-steps"></a>後續步驟

請查看我們[範例 GitHub 儲存機制](https://github.com/Azure/azure-service-bus/tree/master/samples)，示範一些更進階的功能的服務匯流排傳訊的 hello。

<!--Image references-->

[nuget-pkg]: ./media/service-bus-dotnet-get-started-with-queues/nuget-package.png
[queue-message]: ./media/service-bus-dotnet-get-started-with-queues/queue-message.png
[queue-message-receive]: ./media/service-bus-dotnet-get-started-with-queues/queue-message-receive.png
[github-samples]: https://github.com/Azure-Samples/azure-servicebus-messaging-samples
