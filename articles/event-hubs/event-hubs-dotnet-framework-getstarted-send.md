---
title: "aaaSend 事件 tooAzure 事件中心使用 hello.NET Framework |Microsoft 文件"
description: "開始使用.NET Framework hello tooEvent 中樞傳送事件"
services: event-hubs
documentationcenter: 
author: sethmanheim
manager: timlt
editor: 
ms.assetid: c4974bd3-2a79-48a1-aa3b-8ee2d6655b28
ms.service: event-hubs
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/12/2017
ms.author: sethm
ms.openlocfilehash: 05514546a6094096e4a3c800db058190076de80a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="send-events-tooazure-event-hubs-using-hello-net-framework"></a>傳送事件使用.NET Framework hello tooAzure 事件中心

## <a name="introduction"></a>簡介

「事件中樞」是一種服務，可處理來自連接裝置和應用程式的大量事件資料 (遙測)。 資料收集到事件中心之後，您可以使用存放裝置叢集的 hello 資料儲存或轉換使用即時分析提供者。 此大規模事件收集和處理功能是索引鍵的現代應用程式架構，包括 hello 物聯網 (IoT) 元件。

本教學課程示範如何 toouse hello [Azure 入口網站](https://portal.azure.com)toocreate 事件中心。 它也會示範如何使用主控台應用程式以使用 C# 撰寫的 toosend 事件 tooan 事件中心 hello.NET Framework。 使用.NET Framework hello tooreceive 事件，請參閱 「 hello[接收使用 hello.NET Framework 事件](event-hubs-dotnet-framework-getstarted-receive-eph.md)文章，或按一下 hello 適當接收的語言 hello 左側資料表的內容中。

toocomplete 本教學課程中，您需要下列必要條件 hello:

* [Microsoft Visual Studio 2015 或更高版本](http://visualstudio.com)。 在此教學課程中的 hello 螢幕擷取畫面會使用 Visual Studio 2017。
* 使用中的 Azure 帳戶。 如果您沒有帳戶，只需要幾分鐘的時間就可以建立免費帳戶。 如需詳細資訊，請參閱 [Azure 免費試用](https://azure.microsoft.com/free/)。

## <a name="create-an-event-hubs-namespace-and-an-event-hub"></a>建立事件中樞命名空間和事件中樞

hello 第一個步驟是 toouse hello [Azure 入口網站](https://portal.azure.com)toocreate 的命名空間的輸入事件中心，並取得 hello 應用程式需要 toocommunicate 與 hello 事件中心的管理認證。 toocreate 命名空間和事件中心，請依照下列中的 hello 程序[本文](event-hubs-create.md)，然後繼續進行下列步驟，在此教學課程中的 hello。

## <a name="create-a-sender-console-application"></a>建立傳送者主控台應用程式

在本節中，您會將寫入 Windows 主控台應用程式傳送事件 tooyour 事件中心。

1. 在 Visual Studio 中，建立新的 Visual C# 桌面應用程式專案，使用 hello**主控台應用程式**專案範本。 名稱 hello 專案**寄件者**。
   
    ![](./media/event-hubs-dotnet-framework-getstarted-send/create-sender-csharp1.png)
2. 在 [方案總管] 中，以滑鼠右鍵按一下 hello**寄件者**專案，然後再按一下**管理方案的 NuGet 套件**。 
3. 按一下 hello**瀏覽**索引標籤，然後搜尋`Microsoft Azure Service Bus`。 按一下**安裝**，並接受使用規定 hello。 
   
    ![](./media/event-hubs-dotnet-framework-getstarted-send/create-sender-csharp2.png)
   
    Visual Studio 會下載、 安裝，並將參考 toohello [Azure 服務匯流排程式庫 NuGet 封裝](https://www.nuget.org/packages/WindowsAzure.ServiceBus)。
4. 新增下列 hello`using`在 hello hello 最上方的陳述式**Program.cs**檔案：
   
  ```csharp
  using System.Threading;
  using Microsoft.ServiceBus.Messaging;
  ```
5. 新增下列欄位 toohello hello**程式**類別，以取代 hello 名稱為您建立 hello 前一節中的 hello 事件中心與您先前儲存的 hello 命名空間層級的連接字串 hello 預留位置值。
   
  ```csharp
  static string eventHubName = "{Event Hub name}";
  static string connectionString = "{send connection string}";
  ```
6. 新增下列方法 toohello hello**程式**類別：
   
  ```csharp
  static void SendingRandomMessages()
  {
      var eventHubClient = EventHubClient.CreateFromConnectionString(connectionString, eventHubName);
      while (true)
      {
          try
          {
              var message = Guid.NewGuid().ToString();
              Console.WriteLine("{0} > Sending message: {1}", DateTime.Now, message);
              eventHubClient.Send(new EventData(Encoding.UTF8.GetBytes(message)));
          }
          catch (Exception exception)
          {
              Console.ForegroundColor = ConsoleColor.Red;
              Console.WriteLine("{0} > Exception: {1}", DateTime.Now, exception.Message);
              Console.ResetColor();
          }
   
          Thread.Sleep(200);
      }
  }
  ```
   
  此方法會持續傳送事件 tooyour 事件中心有 200 毫秒的延遲。
7. 最後，加入下列行 toohello hello **Main**方法：
   
  ```csharp
  Console.WriteLine("Press Ctrl-C toostop hello sender process");
  Console.WriteLine("Press Enter toostart now");
  Console.ReadLine();
  SendingRandomMessages();
  ```
8. 執行 hello 程式，並確定沒有任何錯誤。
  
恭喜！ 現在您已送出訊息 tooan 事件中心。

## <a name="next-steps"></a>後續步驟
既然您已建立之工作應用程式會建立事件中心，並將資料傳送，您可以繼續 toohello 下列案例：

* [接收事件使用 hello 事件處理器主機](event-hubs-dotnet-framework-getstarted-receive-eph.md)
* [事件處理器主機參考](/dotnet/api/microsoft.servicebus.messaging.eventprocessorhost)
* [事件中樞概觀](event-hubs-what-is-event-hubs.md)

<!-- Images. -->
[19]: ./media/event-hubs-csharp-ephcs-getstarted/create-eh-proj1.png
[20]: ./media/event-hubs-csharp-ephcs-getstarted/create-eh-proj2.png
[21]: ./media/event-hubs-csharp-ephcs-getstarted/run-csharp-ephcs1.png
[22]: ./media/event-hubs-csharp-ephcs-getstarted/run-csharp-ephcs2.png

