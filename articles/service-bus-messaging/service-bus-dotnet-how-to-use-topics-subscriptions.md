---
title: "aaaGet 開始使用 Azure 服務匯流排主題和訂用帳戶 |Microsoft 文件"
description: "撰寫使用服務匯流排傳訊主題和訂用帳戶的 C# 主控台應用程式。"
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: service-bus-messaging
ms.devlang: tbd
ms.topic: hero-article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 06/30/2017
ms.author: sethm
ms.openlocfilehash: 619d602599d97ecff2ded0681a383b19f1a8b7ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-service-bus-topics"></a>開始使用服務匯流排主題

[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

## <a name="what-will-be-accomplished"></a>將會完成的工作

本教學課程涵蓋 hello 下列步驟：

1. 建立服務匯流排命名空間，使用 hello Azure 入口網站。
2. 建立服務匯流排主題，使用 hello Azure 入口網站。
3. 建立服務匯流排訂用帳戶 toothat 主題，使用 hello Azure 入口網站。
4. 撰寫主控台應用程式 toosend 訊息 toohello 主題。
5. 撰寫從 hello 訂用帳戶的主控台應用程式 tooreceive 該訊息。

## <a name="prerequisites"></a>必要條件

1. [Visual Studio 2015 或更新版本](http://www.visualstudio.com)。 在此教學課程中的 hello 範例會使用 Visual Studio 2017。
2. Azure 訂用帳戶。

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="1-create-a-namespace-using-hello-azure-portal"></a>1.建立命名空間使用 hello Azure 入口網站

如果您已經建立 Service Bus 訊息的命名空間，跳 toohello[建立使用 hello Azure 入口網站主題](#2-create-a-topic-using-the-azure-portal)> 一節。

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="2-create-a-topic-using-hello-azure-portal"></a>2.建立使用 hello Azure 入口網站主題

1. 登入 toohello [Azure 入口網站][azure-portal]。
2. 在 hello hello 入口網站的左側瀏覽窗格中按一下**Service Bus** (如果您沒有看到**Service Bus**，按一下 **更多服務**)。
3. 按一下您想在其中要 toocreate hello 主題 hello 命名空間。 hello 命名空間概觀刀鋒視窗會出現：
   
    ![建立主題][createtopic1]
4. 在 hello**服務匯流排命名空間**刀鋒視窗中，按一下 **主題**，然後按一下 **新增主題**。
   
    ![選取主題][createtopic2]
5. 輸入 hello 主題的名稱，然後取消選取 hello**啟用資料分割**選項。 將 hello 保留其預設值與其他選項。
   
    ![選取新增][createtopic3]
6. 在 hello hello 刀鋒視窗底部，按一下 **建立**。

## <a name="3-create-a-subscription-toohello-topic"></a>3.建立訂用帳戶 toohello 主題

1. 在 hello 入口網站的資源 窗格中，按一下您在步驟 1 所建立的 hello 命名空間然後按一下您在步驟 2 中建立的 hello 主題的名稱。
2. Hello 頂端 hello 概觀窗格中，按一下 hello 加上登入接著太**訂用帳戶**tooadd 訂用帳戶 toothis 主題。

    ![建立訂用帳戶][createtopic4]

3. 輸入 hello 訂用帳戶的名稱。 將 hello 保留其預設值與其他選項。

## <a name="4-send-messages-toohello-topic"></a>4.傳送訊息 toohello 主題

toosend 訊息 toohello 主題中，我們會撰寫 C# 主控台應用程式使用 Visual Studio。

### <a name="create-a-console-application"></a>建立主控台應用程式

啟動 Visual Studio，並建立新的**主控台應用程式 (.NET Framework)** 專案。

### <a name="add-hello-service-bus-nuget-package"></a>加入 hello 服務匯流排 NuGet 封裝

1. Hello 新建立的專案上按一下滑鼠右鍵，然後選取**管理 NuGet 封裝**。
2. 按一下 hello**瀏覽**索引標籤上，搜尋**Microsoft Azure 服務匯流排**，然後選取 hello **WindowsAzure.ServiceBus**項目。 按一下**安裝**toocomplete hello 安裝，然後關閉此對話方塊。
   
    ![選取 NuGet 封裝][nuget-pkg]

### <a name="write-some-code-toosend-a-message-toohello-topic"></a>撰寫一些程式碼 toosend 訊息 toohello 主題

1. 新增下列 hello `using` hello Program.cs 檔案的陳述式 toohello 頂端。
   
    ```csharp
    using Microsoft.ServiceBus.Messaging;
    ```
2. 新增下列程式碼 toohello hello`Main`方法。 設定 hello`connectionString`變數 toohello 連接字串時建立 hello 命名空間中，取得及設定`topicName`toohello 建立 hello 主題時，您所使用的名稱。
   
    ```csharp
    var connectionString = "<your connection string>";
    var topicName = "<your topic name>";
   
    var client = TopicClient.CreateFromConnectionString(connectionString, topicName);
    var message = new BrokeredMessage("This is a test message!");

    Console.WriteLine(String.Format("Message body: {0}", message.GetBody<String>()));
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

    namespace tsend
    {
        class Program
        {
            static void Main(string[] args)
            {
                var connectionString = "Endpoint=sb://<your namespace>.servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=<your key>";
                var topicName = "<your topic name>";

                var client = TopicClient.CreateFromConnectionString(connectionString, topicName);
                var message = new BrokeredMessage("This is a test message!");

                Console.WriteLine(String.Format("Message body: {0}", message.GetBody<String>()));
                Console.WriteLine(String.Format("Message id: {0}", message.MessageId));

                client.Send(message);

                Console.WriteLine("Message successfully sent! Press ENTER tooexit program");
                Console.ReadLine();
            }
        }
    }
    ```
3. 執行 hello 程式並檢查 hello Azure 入口網站： 按一下主題 hello 命名空間中的 hello 名稱**概觀**刀鋒視窗。 hello 主題**Essentials**刀鋒視窗會顯示。 在 hello 訂閱 hello hello 刀鋒視窗的底部列，請注意該 hello**訊息計數**每個訂用帳戶現在應該為 1 的值。 每次執行 hello 寄件者應用程式，而不擷取 hello 訊息 （如 hello 下一節中所述），這個值會增加 1。 也請注意該 hello 的目前大小的 hello 主題遞增 hello**目前**上 hello 值**Essentials**刀鋒視窗每次 hello 應用程式加入訊息的 toohello 主題/訂用帳戶。
   
      ![訊息大小][topic-message]

## <a name="5-receive-messages-from-hello-subscription"></a>5.從 hello 訂閱接收訊息

1. tooreceive hello 訊息或只傳送的訊息建立新的主控台應用程式，並加入參考 toohello 服務匯流排 NuGet 封裝，類似 toohello 先前寄件者應用程式。
2. 新增下列 hello `using` hello Program.cs 檔案的陳述式 toohello 頂端。
   
    ```csharp
    using Microsoft.ServiceBus.Messaging;
    ```
3. 新增下列程式碼 toohello hello`Main`方法。 設定 hello`connectionString`變數 toohello 連接字串時建立 hello 命名空間中，取得並設定您`topicName`toohello 建立 hello 主題時，您所使用的名稱。
   
    ```csharp
    var connectionString = "<your connection string>";
    var topicName = "<your topic name>";
   
    var client = SubscriptionClient.CreateFromConnectionString(connectionString, topicName, "<your subscription name>");
   
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
   
    namespace GettingStartedWithTopics
    {
      class Program
      {
        static void Main(string[] args)
        {
          var connectionString = "Endpoint=sb://<your namespace>.servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=<your key>";;
          var topicName = "<your topic name>";
   
          var client = SubscriptionClient.CreateFromConnectionString(connectionString, topicName, "<your subscription name>");
   
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
4. 執行 hello 程式並再次檢查 hello 入口網站。 請注意該 hello**訊息計數**和**目前**值現在是 0。
   
    ![主題長度][topic-message-receive]

恭喜！ 您現在已建立主題和訂用帳戶，傳送一則訊息並接收該訊息。

## <a name="next-steps"></a>後續步驟

請查看我們[範例 GitHub 儲存機制](https://github.com/Azure/azure-service-bus/tree/master/samples)，示範一些更進階的功能的服務匯流排傳訊的 hello。

<!--Image references-->

[nuget-pkg]: ./media/service-bus-dotnet-how-to-use-topics-subscriptions/nuget-package.png
[topic-message]: ./media/service-bus-dotnet-how-to-use-topics-subscriptions/topic-message.png
[topic-message-receive]: ./media/service-bus-dotnet-how-to-use-topics-subscriptions/topic-message-receive.png
[createtopic1]: ./media/service-bus-dotnet-how-to-use-topics-subscriptions/create-topic1.png
[createtopic2]: ./media/service-bus-dotnet-how-to-use-topics-subscriptions/create-topic2.png
[createtopic3]: ./media/service-bus-dotnet-how-to-use-topics-subscriptions/create-topic3.png
[createtopic4]: ./media/service-bus-dotnet-how-to-use-topics-subscriptions/create-topic4.png
[github-samples]: https://github.com/Azure-Samples/azure-servicebus-messaging-samples
[azure-portal]: https://portal.azure.com
