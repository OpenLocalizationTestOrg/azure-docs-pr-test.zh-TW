---
title: "aaaSend 事件 tooAzure 使用標準.NET 的事件中心 |Microsoft 文件"
description: "以.NET 標準 tooEvent 中樞傳送事件開始"
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
ms.openlocfilehash: caa9747a8a72aa8e7aea1348a116f6e4b406460e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-sending-messages-tooazure-event-hubs-in-net-standard"></a>開始傳送訊息的.NET 標準 tooAzure 事件中心

> [!NOTE]
> 您可在 [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleSender) 上取得此範例。

本教學課程會示範如何 toowrite.NET Core 主控台應用程式所傳送的一組訊息 tooan 事件中心。 您可以執行 hello [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleSender)做為方案層，就取代 hello`EhConnectionString`和`EhEntityPath`字串以您的事件中樞值。 您可以遵循 hello 步驟在本教學課程 toocreate 自己。

## <a name="prerequisites"></a>必要條件

* [Microsoft Visual Studio 2015 或 2017](http://www.visualstudio.com)。 也支援在此教學課程使用 Visual Studio 2017，hello 範例，但 Visual Studio 2015。
* [.NET Core Visual Studio 2015 或 2017 工具](http://www.microsoft.com/net/core)。
* Azure 訂用帳戶。
* 事件中樞命名空間。

toosend 訊息 tooan 事件中樞，我們將使用 Visual Studio toowrite C# 主控台應用程式。

## <a name="create-an-event-hubs-namespace-and-an-event-hub"></a>建立事件中樞命名空間和事件中樞

hello 第一個步驟是 toouse hello [Azure 入口網站](https://portal.azure.com)toocreate hello 事件中樞的類型、 命名空間，並取得 hello 應用程式需要 toocommunicate 與 hello 事件中心的管理認證。 toocreate 的命名空間和事件中心，請依照下列中的 hello 程序[本文](event-hubs-create.md)，再繼續執行步驟的 hello。

## <a name="create-a-console-application"></a>建立主控台應用程式

啟動 Visual Studio。 從 hello**檔案**功能表上，按一下 **新增**，然後按一下**專案**。 建立 .NET Core 主控台應用程式。

![新增專案][1]

## <a name="add-hello-event-hubs-nuget-package"></a>加入 hello 事件中心 NuGet 封裝

新增 hello [ `Microsoft.Azure.EventHubs` ](https://www.nuget.org/packages/Microsoft.Azure.EventHubs/) .NET 標準程式庫 NuGet 封裝 tooyour 專案依照下列步驟： 

1. Hello 新建立的專案上按一下滑鼠右鍵，然後選取**管理 NuGet 封裝**。
2. 按一下 hello**瀏覽** 索引標籤，然後搜尋 「 Microsoft.Azure.EventHubs 」 和選取 hello **Microsoft.Azure.EventHubs**封裝。 按一下**安裝**toocomplete hello 安裝，然後關閉此對話方塊。

## <a name="write-some-code-toosend-messages-toohello-event-hub"></a>撰寫一些程式碼 toosend 訊息 toohello 事件中樞

1. 新增下列 hello `using` hello Program.cs 檔案的陳述式 toohello 頂端。

    ```csharp
    using Microsoft.Azure.EventHubs;
    using System.Text;
    using System.Threading.Tasks;
    ```

2. 新增常數 toohello `Program` hello 事件中樞連接字串和實體路徑 （個別的事件中樞名稱） 的類別。 方括號中的 hello 預留位置取代為 hello 建立 hello 事件中心時取得的適當值。

    ```csharp
    private static EventHubClient eventHubClient;
    private const string EhConnectionString = "{Event Hubs connection string}";
    private const string EhEntityPath = "{Event Hub path/name}";
    ```

3. 新增名為方法`MainAsync`toohello`Program`類別，如下所示：

    ```csharp
    private static async Task MainAsync(string[] args)
    {
        // Creates an EventHubsConnectionStringBuilder object from hello connection string, and sets hello EntityPath.
        // Typically, hello connection string should have hello entity path in it, but for hello sake of this simple scenario
        // we are using hello connection string from hello namespace.
        var connectionStringBuilder = new EventHubsConnectionStringBuilder(EhConnectionString)
        {
            EntityPath = EhEntityPath
        };

        eventHubClient = EventHubClient.CreateFromConnectionString(connectionStringBuilder.ToString());

        await SendMessagesToEventHub(100);

        await eventHubClient.CloseAsync();

        Console.WriteLine("Press ENTER tooexit.");
        Console.ReadLine();
    }
    ```

4. 新增名為方法`SendMessagesToEventHub`toohello`Program`類別，如下所示：

    ```csharp
    // Creates an event hub client and sends 100 messages toohello event hub.
    private static async Task SendMessagesToEventHub(int numMessagesToSend)
    {
        for (var i = 0; i < numMessagesToSend; i++)
        {
            try
            {
                var message = $"Message {i}";
                Console.WriteLine($"Sending message: {message}");
                await eventHubClient.SendAsync(new EventData(Encoding.UTF8.GetBytes(message)));
            }
            catch (Exception exception)
            {
                Console.WriteLine($"{DateTime.Now} > Exception: {exception.Message}");
            }

            await Task.Delay(10);
        }

        Console.WriteLine($"{numMessagesToSend} messages sent.");
    }
    ```

5. 新增下列程式碼 toohello hello`Main`方法在 hello`Program`類別。

    ```csharp
    MainAsync(args).GetAwaiter().GetResult();
    ```

   Program.cs 看起來應該會像下面這樣。

    ```csharp
    namespace SampleSender
    {
        using System;
        using System.Text;
        using System.Threading.Tasks;
        using Microsoft.Azure.EventHubs;

        public class Program
        {
            private static EventHubClient eventHubClient;
            private const string EhConnectionString = "{Event Hubs connection string}";
            private const string EhEntityPath = "{Event Hub path/name}";

            public static void Main(string[] args)
            {
                MainAsync(args).GetAwaiter().GetResult();
            }

            private static async Task MainAsync(string[] args)
            {
                // Creates an EventHubsConnectionStringBuilder object from hello connection string, and sets hello EntityPath.
                // Typically, hello connection string should have hello entity path in it, but for hello sake of this simple scenario
                // we are using hello connection string from hello namespace.
                var connectionStringBuilder = new EventHubsConnectionStringBuilder(EhConnectionString)
                {
                    EntityPath = EhEntityPath
                };

                eventHubClient = EventHubClient.CreateFromConnectionString(connectionStringBuilder.ToString());

                await SendMessagesToEventHub(100);

                await eventHubClient.CloseAsync();

                Console.WriteLine("Press ENTER tooexit.");
                Console.ReadLine();
            }

            // Creates an event hub client and sends 100 messages toohello event hub.
            private static async Task SendMessagesToEventHub(int numMessagesToSend)
            {
                for (var i = 0; i < numMessagesToSend; i++)
                {
                    try
                    {
                        var message = $"Message {i}";
                        Console.WriteLine($"Sending message: {message}");
                        await eventHubClient.SendAsync(new EventData(Encoding.UTF8.GetBytes(message)));
                    }
                    catch (Exception exception)
                    {
                        Console.WriteLine($"{DateTime.Now} > Exception: {exception.Message}");
                    }

                    await Task.Delay(10);
                }

                Console.WriteLine($"{numMessagesToSend} messages sent.");
            }
        }
    }
    ```

6. 執行 hello 程式，並確定沒有任何錯誤。

恭喜！ 現在您已送出訊息 tooan 事件中心。

## <a name="next-steps"></a>後續步驟
您可以進一步了解事件中心瀏覽下列連結查看 hello:

* [從事件中樞接收事件](event-hubs-dotnet-standard-getstarted-receive-eph.md)
* [事件中樞概觀](event-hubs-what-is-event-hubs.md)
* [建立事件中樞](event-hubs-create.md)
* [事件中樞常見問題集](event-hubs-faq.md)

[1]: ./media/event-hubs-dotnet-standard-getstarted-send/netcore.png
