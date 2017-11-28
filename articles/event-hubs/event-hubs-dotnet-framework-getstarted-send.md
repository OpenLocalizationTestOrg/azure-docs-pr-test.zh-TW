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
# <a name="send-events-tooazure-event-hubs-using-hello-net-framework"></a><span data-ttu-id="41b1d-103">傳送事件使用.NET Framework hello tooAzure 事件中心</span><span class="sxs-lookup"><span data-stu-id="41b1d-103">Send events tooAzure Event Hubs using hello .NET Framework</span></span>

## <a name="introduction"></a><span data-ttu-id="41b1d-104">簡介</span><span class="sxs-lookup"><span data-stu-id="41b1d-104">Introduction</span></span>

<span data-ttu-id="41b1d-105">「事件中樞」是一種服務，可處理來自連接裝置和應用程式的大量事件資料 (遙測)。</span><span class="sxs-lookup"><span data-stu-id="41b1d-105">Event Hubs is a service that processes large amounts of event data (telemetry) from connected devices and applications.</span></span> <span data-ttu-id="41b1d-106">資料收集到事件中心之後，您可以使用存放裝置叢集的 hello 資料儲存或轉換使用即時分析提供者。</span><span class="sxs-lookup"><span data-stu-id="41b1d-106">After you collect data into Event Hubs, you can store hello data using a storage cluster or transform it using a real-time analytics provider.</span></span> <span data-ttu-id="41b1d-107">此大規模事件收集和處理功能是索引鍵的現代應用程式架構，包括 hello 物聯網 (IoT) 元件。</span><span class="sxs-lookup"><span data-stu-id="41b1d-107">This large-scale event collection and processing capability is a key component of modern application architectures including hello Internet of Things (IoT).</span></span>

<span data-ttu-id="41b1d-108">本教學課程示範如何 toouse hello [Azure 入口網站](https://portal.azure.com)toocreate 事件中心。</span><span class="sxs-lookup"><span data-stu-id="41b1d-108">This tutorial shows how toouse hello [Azure portal](https://portal.azure.com) toocreate an event hub.</span></span> <span data-ttu-id="41b1d-109">它也會示範如何使用主控台應用程式以使用 C# 撰寫的 toosend 事件 tooan 事件中心 hello.NET Framework。</span><span class="sxs-lookup"><span data-stu-id="41b1d-109">It also shows how toosend events tooan event hub using a console application written in C# using hello .NET Framework.</span></span> <span data-ttu-id="41b1d-110">使用.NET Framework hello tooreceive 事件，請參閱 「 hello[接收使用 hello.NET Framework 事件](event-hubs-dotnet-framework-getstarted-receive-eph.md)文章，或按一下 hello 適當接收的語言 hello 左側資料表的內容中。</span><span class="sxs-lookup"><span data-stu-id="41b1d-110">tooreceive events using hello .NET Framework, see hello [Receive events using hello .NET Framework](event-hubs-dotnet-framework-getstarted-receive-eph.md) article, or click hello appropriate receiving language in hello left-hand table of contents.</span></span>

<span data-ttu-id="41b1d-111">toocomplete 本教學課程中，您需要下列必要條件 hello:</span><span class="sxs-lookup"><span data-stu-id="41b1d-111">toocomplete this tutorial, you need hello following prerequisites:</span></span>

* <span data-ttu-id="41b1d-112">[Microsoft Visual Studio 2015 或更高版本](http://visualstudio.com)。</span><span class="sxs-lookup"><span data-stu-id="41b1d-112">[Microsoft Visual Studio 2015 or higher](http://visualstudio.com).</span></span> <span data-ttu-id="41b1d-113">在此教學課程中的 hello 螢幕擷取畫面會使用 Visual Studio 2017。</span><span class="sxs-lookup"><span data-stu-id="41b1d-113">hello screen shots in this tutorial use Visual Studio 2017.</span></span>
* <span data-ttu-id="41b1d-114">使用中的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="41b1d-114">An active Azure account.</span></span> <span data-ttu-id="41b1d-115">如果您沒有帳戶，只需要幾分鐘的時間就可以建立免費帳戶。</span><span class="sxs-lookup"><span data-stu-id="41b1d-115">If you don't have one, you can create a free account in just a couple of minutes.</span></span> <span data-ttu-id="41b1d-116">如需詳細資訊，請參閱 [Azure 免費試用](https://azure.microsoft.com/free/)。</span><span class="sxs-lookup"><span data-stu-id="41b1d-116">For details, see [Azure Free Trial](https://azure.microsoft.com/free/).</span></span>

## <a name="create-an-event-hubs-namespace-and-an-event-hub"></a><span data-ttu-id="41b1d-117">建立事件中樞命名空間和事件中樞</span><span class="sxs-lookup"><span data-stu-id="41b1d-117">Create an Event Hubs namespace and an event hub</span></span>

<span data-ttu-id="41b1d-118">hello 第一個步驟是 toouse hello [Azure 入口網站](https://portal.azure.com)toocreate 的命名空間的輸入事件中心，並取得 hello 應用程式需要 toocommunicate 與 hello 事件中心的管理認證。</span><span class="sxs-lookup"><span data-stu-id="41b1d-118">hello first step is toouse hello [Azure portal](https://portal.azure.com) toocreate a namespace of type Event Hubs, and obtain hello management credentials your application needs toocommunicate with hello event hub.</span></span> <span data-ttu-id="41b1d-119">toocreate 命名空間和事件中心，請依照下列中的 hello 程序[本文](event-hubs-create.md)，然後繼續進行下列步驟，在此教學課程中的 hello。</span><span class="sxs-lookup"><span data-stu-id="41b1d-119">toocreate a namespace and event hub, follow hello procedure in [this article](event-hubs-create.md), then proceed with hello following steps in this tutorial.</span></span>

## <a name="create-a-sender-console-application"></a><span data-ttu-id="41b1d-120">建立傳送者主控台應用程式</span><span class="sxs-lookup"><span data-stu-id="41b1d-120">Create a sender console application</span></span>

<span data-ttu-id="41b1d-121">在本節中，您會將寫入 Windows 主控台應用程式傳送事件 tooyour 事件中心。</span><span class="sxs-lookup"><span data-stu-id="41b1d-121">In this section, you'll write a Windows console app that sends events tooyour event hub.</span></span>

1. <span data-ttu-id="41b1d-122">在 Visual Studio 中，建立新的 Visual C# 桌面應用程式專案，使用 hello**主控台應用程式**專案範本。</span><span class="sxs-lookup"><span data-stu-id="41b1d-122">In Visual Studio, create a new Visual C# Desktop App project using hello **Console Application** project template.</span></span> <span data-ttu-id="41b1d-123">名稱 hello 專案**寄件者**。</span><span class="sxs-lookup"><span data-stu-id="41b1d-123">Name hello project **Sender**.</span></span>
   
    ![](./media/event-hubs-dotnet-framework-getstarted-send/create-sender-csharp1.png)
2. <span data-ttu-id="41b1d-124">在 [方案總管] 中，以滑鼠右鍵按一下 hello**寄件者**專案，然後再按一下**管理方案的 NuGet 套件**。</span><span class="sxs-lookup"><span data-stu-id="41b1d-124">In Solution Explorer, right-click hello **Sender** project, and then click **Manage NuGet Packages for Solution**.</span></span> 
3. <span data-ttu-id="41b1d-125">按一下 hello**瀏覽**索引標籤，然後搜尋`Microsoft Azure Service Bus`。</span><span class="sxs-lookup"><span data-stu-id="41b1d-125">Click hello **Browse** tab, then search for `Microsoft Azure Service Bus`.</span></span> <span data-ttu-id="41b1d-126">按一下**安裝**，並接受使用規定 hello。</span><span class="sxs-lookup"><span data-stu-id="41b1d-126">Click **Install**, and accept hello terms of use.</span></span> 
   
    ![](./media/event-hubs-dotnet-framework-getstarted-send/create-sender-csharp2.png)
   
    <span data-ttu-id="41b1d-127">Visual Studio 會下載、 安裝，並將參考 toohello [Azure 服務匯流排程式庫 NuGet 封裝](https://www.nuget.org/packages/WindowsAzure.ServiceBus)。</span><span class="sxs-lookup"><span data-stu-id="41b1d-127">Visual Studio downloads, installs, and adds a reference toohello [Azure Service Bus library NuGet package](https://www.nuget.org/packages/WindowsAzure.ServiceBus).</span></span>
4. <span data-ttu-id="41b1d-128">新增下列 hello`using`在 hello hello 最上方的陳述式**Program.cs**檔案：</span><span class="sxs-lookup"><span data-stu-id="41b1d-128">Add hello following `using` statements at hello top of hello **Program.cs** file:</span></span>
   
  ```csharp
  using System.Threading;
  using Microsoft.ServiceBus.Messaging;
  ```
5. <span data-ttu-id="41b1d-129">新增下列欄位 toohello hello**程式**類別，以取代 hello 名稱為您建立 hello 前一節中的 hello 事件中心與您先前儲存的 hello 命名空間層級的連接字串 hello 預留位置值。</span><span class="sxs-lookup"><span data-stu-id="41b1d-129">Add hello following fields toohello **Program** class, substituting hello placeholder values with hello name of hello event hub you created in hello previous section, and hello namespace-level connection string you saved previously.</span></span>
   
  ```csharp
  static string eventHubName = "{Event Hub name}";
  static string connectionString = "{send connection string}";
  ```
6. <span data-ttu-id="41b1d-130">新增下列方法 toohello hello**程式**類別：</span><span class="sxs-lookup"><span data-stu-id="41b1d-130">Add hello following method toohello **Program** class:</span></span>
   
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
   
  <span data-ttu-id="41b1d-131">此方法會持續傳送事件 tooyour 事件中心有 200 毫秒的延遲。</span><span class="sxs-lookup"><span data-stu-id="41b1d-131">This method continuously sends events tooyour event hub with a 200-ms delay.</span></span>
7. <span data-ttu-id="41b1d-132">最後，加入下列行 toohello hello **Main**方法：</span><span class="sxs-lookup"><span data-stu-id="41b1d-132">Finally, add hello following lines toohello **Main** method:</span></span>
   
  ```csharp
  Console.WriteLine("Press Ctrl-C toostop hello sender process");
  Console.WriteLine("Press Enter toostart now");
  Console.ReadLine();
  SendingRandomMessages();
  ```
8. <span data-ttu-id="41b1d-133">執行 hello 程式，並確定沒有任何錯誤。</span><span class="sxs-lookup"><span data-stu-id="41b1d-133">Run hello program, and ensure that there are no errors.</span></span>
  
<span data-ttu-id="41b1d-134">恭喜！</span><span class="sxs-lookup"><span data-stu-id="41b1d-134">Congratulations!</span></span> <span data-ttu-id="41b1d-135">現在您已送出訊息 tooan 事件中心。</span><span class="sxs-lookup"><span data-stu-id="41b1d-135">You have now sent messages tooan event hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="41b1d-136">後續步驟</span><span class="sxs-lookup"><span data-stu-id="41b1d-136">Next steps</span></span>
<span data-ttu-id="41b1d-137">既然您已建立之工作應用程式會建立事件中心，並將資料傳送，您可以繼續 toohello 下列案例：</span><span class="sxs-lookup"><span data-stu-id="41b1d-137">Now that you've built a working application that creates an event hub and sends data, you can move on toohello following scenarios:</span></span>

* [<span data-ttu-id="41b1d-138">接收事件使用 hello 事件處理器主機</span><span class="sxs-lookup"><span data-stu-id="41b1d-138">Receive events using hello Event Processor Host</span></span>](event-hubs-dotnet-framework-getstarted-receive-eph.md)
* [<span data-ttu-id="41b1d-139">事件處理器主機參考</span><span class="sxs-lookup"><span data-stu-id="41b1d-139">Event Processor Host reference</span></span>](/dotnet/api/microsoft.servicebus.messaging.eventprocessorhost)
* [<span data-ttu-id="41b1d-140">事件中樞概觀</span><span class="sxs-lookup"><span data-stu-id="41b1d-140">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)

<!-- Images. -->
[19]: ./media/event-hubs-csharp-ephcs-getstarted/create-eh-proj1.png
[20]: ./media/event-hubs-csharp-ephcs-getstarted/create-eh-proj2.png
[21]: ./media/event-hubs-csharp-ephcs-getstarted/run-csharp-ephcs1.png
[22]: ./media/event-hubs-csharp-ephcs-getstarted/run-csharp-ephcs2.png

