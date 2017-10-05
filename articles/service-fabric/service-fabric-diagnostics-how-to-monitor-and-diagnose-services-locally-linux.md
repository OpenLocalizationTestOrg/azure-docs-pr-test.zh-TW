---
title: "在 Linux 中針對 Azure 微服務進行偵錯 | Microsoft Docs"
description: "了解如何監視和診斷在本機開發電腦上使用 Microsoft Azure Service Fabric 所撰寫的服務。"
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: 4eebe937-ab42-4429-93db-f35c26424321
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: 4bc73f581f4855ebc724df19dd56fab8bf103854
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="monitor-and-diagnose-services-in-a-local-machine-development-setup"></a><span data-ttu-id="48939-103">監視和診斷本機開發設定中的服務</span><span class="sxs-lookup"><span data-stu-id="48939-103">Monitor and diagnose services in a local machine development setup</span></span>


> [!div class="op_single_selector"]
> * [<span data-ttu-id="48939-104">Windows</span><span class="sxs-lookup"><span data-stu-id="48939-104">Windows</span></span>](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)
> * [<span data-ttu-id="48939-105">Linux</span><span class="sxs-lookup"><span data-stu-id="48939-105">Linux</span></span>](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally-linux.md)
>
>

<span data-ttu-id="48939-106">監視、偵測、診斷和疑難排解可讓服務繼續順利執行，盡可能減少服務中斷的使用者經驗。</span><span class="sxs-lookup"><span data-stu-id="48939-106">Monitoring, detecting, diagnosing, and troubleshooting allow for services to continue with minimal disruption to the user experience.</span></span> <span data-ttu-id="48939-107">在實際部署的生產環境中，監視和診斷非常重要。</span><span class="sxs-lookup"><span data-stu-id="48939-107">Monitoring and diagnostics are critical in an actual deployed production environment.</span></span> <span data-ttu-id="48939-108">若在開發服務期間採用類似的模型，當您移到生產環境時，將可確保診斷管線能夠運作。</span><span class="sxs-lookup"><span data-stu-id="48939-108">Adopting a similar model during development of services ensures that the diagnostic pipeline works when you move to a production environment.</span></span> <span data-ttu-id="48939-109">Service Fabric 可讓服務開發人員輕鬆實作診斷，可以在單一電腦本機開發設定和實際生產叢集設定上順暢地工作。</span><span class="sxs-lookup"><span data-stu-id="48939-109">Service Fabric makes it easy for service developers to implement diagnostics that can seamlessly work across both single-machine local development setups and real-world production cluster setups.</span></span>


## <a name="debugging-service-fabric-java-applications"></a><span data-ttu-id="48939-110">針對 Service Fabric Java 應用程式進行偵錯</span><span class="sxs-lookup"><span data-stu-id="48939-110">Debugging Service Fabric Java applications</span></span>

<span data-ttu-id="48939-111">對於 Java 應用程式，有 [多個記錄架構](http://en.wikipedia.org/wiki/Java_logging_framework) 可用。</span><span class="sxs-lookup"><span data-stu-id="48939-111">For Java applications, [multiple logging frameworks](http://en.wikipedia.org/wiki/Java_logging_framework) are available.</span></span> <span data-ttu-id="48939-112">由於 `java.util.logging` 是 JRE 的預設選項，它也會用於 [github 中的程式碼範例](http://github.com/Azure-Samples/service-fabric-java-getting-started)。</span><span class="sxs-lookup"><span data-stu-id="48939-112">Since `java.util.logging` is the default option with the JRE, it is also used for the [code examples in github](http://github.com/Azure-Samples/service-fabric-java-getting-started).</span></span>  <span data-ttu-id="48939-113">下列討論說明如何設定 `java.util.logging` 架構。</span><span class="sxs-lookup"><span data-stu-id="48939-113">The following discussion explains how to configure the `java.util.logging` framework.</span></span>

<span data-ttu-id="48939-114">您可以使用 java.util.logging 將應用程式記錄檔重新導向至記憶體、輸出串流、主控台檔案或通訊端。</span><span class="sxs-lookup"><span data-stu-id="48939-114">Using java.util.logging you can redirect your application logs to memory, output streams, console files, or sockets.</span></span> <span data-ttu-id="48939-115">對於其中每個選項，架構中已經提供預設處理常式。</span><span class="sxs-lookup"><span data-stu-id="48939-115">For each of these options, there are default handlers already provided in the framework.</span></span> <span data-ttu-id="48939-116">您可以建立 `app.properties` 檔案來設定應用程式的檔案處理常式，將所有記錄檔重新導向至本機檔案。</span><span class="sxs-lookup"><span data-stu-id="48939-116">You can create a `app.properties` file to configure the file handler for your application to redirect all logs to a local file.</span></span>

<span data-ttu-id="48939-117">下列程式碼片段包含範例組態︰</span><span class="sxs-lookup"><span data-stu-id="48939-117">The following code snippet contains an example configuration:</span></span>

```java
handlers = java.util.logging.FileHandler

java.util.logging.FileHandler.level = ALL
java.util.logging.FileHandler.formatter = java.util.logging.SimpleFormatter
java.util.logging.FileHandler.limit = 1024000
java.util.logging.FileHandler.count = 10
java.util.logging.FileHandler.pattern = /tmp/servicefabric/logs/mysfapp%u.%g.log             
```

<span data-ttu-id="48939-118">`app.properties` 檔案所指向的資料夾必須存在。</span><span class="sxs-lookup"><span data-stu-id="48939-118">The folder pointed to by the `app.properties` file must exist.</span></span> <span data-ttu-id="48939-119">建立 `app.properties` 檔案之後，您還必須修改 `<applicationfolder>/<servicePkg>/Code/` 資料夾中的進入點指令碼 `entrypoint.sh`，以將屬性 `java.util.logging.config.file` 設定為 `app.propertes` 檔案。</span><span class="sxs-lookup"><span data-stu-id="48939-119">After the `app.properties` file is created, you need to also modify your entry point script, `entrypoint.sh` in the `<applicationfolder>/<servicePkg>/Code/` folder to set the property `java.util.logging.config.file` to `app.propertes` file.</span></span> <span data-ttu-id="48939-120">輸入如下列片段所示：</span><span class="sxs-lookup"><span data-stu-id="48939-120">The entry should look like the following snippet:</span></span>

```sh
java -Djava.library.path=$LD_LIBRARY_PATH -Djava.util.logging.config.file=<path to app.properties> -jar <service name>.jar
```


<span data-ttu-id="48939-121">此設定會導致在 `/tmp/servicefabric/logs/`中以輪替方式收集記錄檔。</span><span class="sxs-lookup"><span data-stu-id="48939-121">This configuration results in logs being collected in a rotating fashion at `/tmp/servicefabric/logs/`.</span></span> <span data-ttu-id="48939-122">在此情況下，記錄檔的名稱為 mysfapp%u.%g.log，其中︰</span><span class="sxs-lookup"><span data-stu-id="48939-122">The log file in this case is named mysfapp%u.%g.log where:</span></span>
* <span data-ttu-id="48939-123">**%u** 是解決同時 Java 處理序之間衝突的唯一號碼。</span><span class="sxs-lookup"><span data-stu-id="48939-123">**%u** is a unique number to resolve conflicts between simultaneous Java processes.</span></span>
* <span data-ttu-id="48939-124">**%g** 是區分輪替記錄的產生號碼。</span><span class="sxs-lookup"><span data-stu-id="48939-124">**%g** is the generation number to distinguish between rotating logs.</span></span>

<span data-ttu-id="48939-125">依預設，如果未明確設定任何處理常式，則會註冊主控台處理常式。</span><span class="sxs-lookup"><span data-stu-id="48939-125">By default if no handler is explicitly configured, the console handler is registered.</span></span> <span data-ttu-id="48939-126">使用者可以在 /var/log/syslog 下檢視 syslog 中的記錄檔。</span><span class="sxs-lookup"><span data-stu-id="48939-126">One can view the logs in syslog under /var/log/syslog.</span></span>

<span data-ttu-id="48939-127">如需詳細資訊，請參閱 [github 中的程式碼範例](http://github.com/Azure-Samples/service-fabric-java-getting-started)。</span><span class="sxs-lookup"><span data-stu-id="48939-127">For more information, see the [code examples in github](http://github.com/Azure-Samples/service-fabric-java-getting-started).</span></span>  


## <a name="debugging-service-fabric-c-applications"></a><span data-ttu-id="48939-128">針對 Service Fabric C# 應用程式進行偵錯</span><span class="sxs-lookup"><span data-stu-id="48939-128">Debugging Service Fabric C# applications</span></span>


<span data-ttu-id="48939-129">有多個架構適用於追蹤 Linux 上的 CoreCLR 應用程式。</span><span class="sxs-lookup"><span data-stu-id="48939-129">Multiple frameworks are available for tracing CoreCLR applications on Linux.</span></span> <span data-ttu-id="48939-130">如需詳細資訊，請參閱 [GitHub：logging](http:/github.com/aspnet/logging)。</span><span class="sxs-lookup"><span data-stu-id="48939-130">For more information, see [GitHub: logging](http:/github.com/aspnet/logging).</span></span>  <span data-ttu-id="48939-131">因為 C# 開發人員熟悉 EventSource，本文使用 EventSource 來追蹤 Linux 上的 CoreCLR 範例。</span><span class="sxs-lookup"><span data-stu-id="48939-131">Since EventSource is familiar to C# developers,\`this article uses EventSource for tracing in CoreCLR samples on Linux.</span></span>

<span data-ttu-id="48939-132">第一個步驟是加入 System.Diagnostics.Tracing，使您可以將您的記錄檔寫入記憶體中、輸出串流或主控台檔案。</span><span class="sxs-lookup"><span data-stu-id="48939-132">The first step is to include System.Diagnostics.Tracing so that you can write your logs to memory, output streams, or console files.</span></span>  <span data-ttu-id="48939-133">針對使用 EventSource 進行記錄，請將下列專案加入您的 project.json︰</span><span class="sxs-lookup"><span data-stu-id="48939-133">For logging using EventSource, add the following project to your project.json:</span></span>

```
    "System.Diagnostics.StackTrace": "4.0.1"
```

<span data-ttu-id="48939-134">您可以使用自訂 EventListener 接聽服務事件，然後適當地將其重新導向至追蹤檔案。</span><span class="sxs-lookup"><span data-stu-id="48939-134">You can use a custom EventListener to listen for the service event and then appropriately redirect them to trace files.</span></span> <span data-ttu-id="48939-135">下列程式碼片段顯示使用 EventSource 和自訂 EventListener 來進行記錄的範例實作︰</span><span class="sxs-lookup"><span data-stu-id="48939-135">The following code snippet shows a sample implementation of logging using EventSource and a custom EventListener:</span></span>


```csharp

 public class ServiceEventSource : EventSource
 {
        public static ServiceEventSource Current = new ServiceEventSource();

        [NonEvent]
        public void Message(string message, params object[] args)
        {
            if (this.IsEnabled())
            {
                var finalMessage = string.Format(message, args);
                this.Message(finalMessage);
            }
        }

        // TBD: Need to add method for sample event.

}

```


```csharp
   internal class ServiceEventListener : EventListener
   {

        protected override void OnEventSourceCreated(EventSource eventSource)
        {
            EnableEvents(eventSource, EventLevel.LogAlways, EventKeywords.All);
        }
        protected override void OnEventWritten(EventWrittenEventArgs eventData)
        {
            using (StreamWriter Out = new StreamWriter( new FileStream("/tmp/MyServiceLog.txt", FileMode.Append)))           
        { 
                 // report all event information               
         Out.Write(" {0} ",  Write(eventData.Task.ToString(), eventData.EventName, eventData.EventId.ToString(), eventData.Level,""));
                if (eventData.Message != null)              
            Out.WriteLine(eventData.Message, eventData.Payload.ToArray());              
            else             
        { 
                    string[] sargs = eventData.Payload != null ? eventData.Payload.Select(o => o.ToString()).ToArray() : null; 
                    Out.WriteLine("({0}).", sargs != null ? string.Join(", ", sargs) : "");             
        }
           }
        }
    }
```


<span data-ttu-id="48939-136">上述程式碼片段會將記錄輸出到 `/tmp/MyServiceLog.txt` 中的檔案。</span><span class="sxs-lookup"><span data-stu-id="48939-136">The preceding snippet outputs the logs to a file in `/tmp/MyServiceLog.txt`.</span></span> <span data-ttu-id="48939-137">此檔案名稱必須適當地更新。</span><span class="sxs-lookup"><span data-stu-id="48939-137">This file name needs to be appropriately updated.</span></span> <span data-ttu-id="48939-138">如果您想要將記錄重新導向至主控台，在您的自訂 EventListener 類別中使用下列程式碼片︰</span><span class="sxs-lookup"><span data-stu-id="48939-138">In case you want to redirect the logs to console, use the following snippet in your customized EventListener class:</span></span>

```csharp
public static TextWriter Out = Console.Out;
```

<span data-ttu-id="48939-139">[C# Samples](https://github.com/Azure-Samples/service-fabric-dotnet-core-getting-started) 中的範例使用 EventSource 和自訂 EventListener 事件將事件記錄到檔案中。</span><span class="sxs-lookup"><span data-stu-id="48939-139">The samples at [C# Samples](https://github.com/Azure-Samples/service-fabric-dotnet-core-getting-started) use EventSource and a custom EventListener to log events to a file.</span></span>



## <a name="next-steps"></a><span data-ttu-id="48939-140">後續步驟</span><span class="sxs-lookup"><span data-stu-id="48939-140">Next steps</span></span>
<span data-ttu-id="48939-141">新增至應用程式的相同追蹤程式碼，也可以用來配合診斷 Azure 叢集上的應用程式。</span><span class="sxs-lookup"><span data-stu-id="48939-141">The same tracing code added to your application also works with the diagnostics of your application on an Azure cluster.</span></span> <span data-ttu-id="48939-142">請參閱下列文章，其中討論各種適用於工具的選項，並說明如何設定它們。</span><span class="sxs-lookup"><span data-stu-id="48939-142">Check out these articles that discuss the different options for the tools and describe how to set them up.</span></span>
* [<span data-ttu-id="48939-143">如何利用 Azure 診斷收集記錄檔</span><span class="sxs-lookup"><span data-stu-id="48939-143">How to collect logs with Azure Diagnostics</span></span>](service-fabric-diagnostics-how-to-setup-lad.md)
