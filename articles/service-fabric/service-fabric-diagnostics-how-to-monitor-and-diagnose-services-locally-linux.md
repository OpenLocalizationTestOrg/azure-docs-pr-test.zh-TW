---
title: "Azure 中 Linux microservices aaaDebug |Microsoft 文件"
description: "深入了解如何 toomonitor 及診斷您使用本機開發電腦上的 Microsoft Azure Service Fabric 撰寫的服務。"
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
ms.openlocfilehash: bee47bbabcf6b84ff2da14079e026529e36a198b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-diagnose-services-in-a-local-machine-development-setup"></a><span data-ttu-id="cad2d-103">監視和診斷本機開發設定中的服務</span><span class="sxs-lookup"><span data-stu-id="cad2d-103">Monitor and diagnose services in a local machine development setup</span></span>


> [!div class="op_single_selector"]
> * [<span data-ttu-id="cad2d-104">Windows</span><span class="sxs-lookup"><span data-stu-id="cad2d-104">Windows</span></span>](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)
> * [<span data-ttu-id="cad2d-105">Linux</span><span class="sxs-lookup"><span data-stu-id="cad2d-105">Linux</span></span>](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally-linux.md)
>
>

<span data-ttu-id="cad2d-106">監視、 偵測、 診斷及疑難排解允許服務 toocontinue 盡量減少 toohello 使用者體驗。</span><span class="sxs-lookup"><span data-stu-id="cad2d-106">Monitoring, detecting, diagnosing, and troubleshooting allow for services toocontinue with minimal disruption toohello user experience.</span></span> <span data-ttu-id="cad2d-107">在實際部署的生產環境中，監視和診斷非常重要。</span><span class="sxs-lookup"><span data-stu-id="cad2d-107">Monitoring and diagnostics are critical in an actual deployed production environment.</span></span> <span data-ttu-id="cad2d-108">在服務的開發採用類似的模型，可確保該 hello 診斷管線運作方式，當您移動 tooa 實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="cad2d-108">Adopting a similar model during development of services ensures that hello diagnostic pipeline works when you move tooa production environment.</span></span> <span data-ttu-id="cad2d-109">Service Fabric 輕鬆可以順暢地適用於所有單一電腦的本機開發的設定和實際生產環境叢集安裝的服務開發人員 tooimplement 診斷。</span><span class="sxs-lookup"><span data-stu-id="cad2d-109">Service Fabric makes it easy for service developers tooimplement diagnostics that can seamlessly work across both single-machine local development setups and real-world production cluster setups.</span></span>


## <a name="debugging-service-fabric-java-applications"></a><span data-ttu-id="cad2d-110">針對 Service Fabric Java 應用程式進行偵錯</span><span class="sxs-lookup"><span data-stu-id="cad2d-110">Debugging Service Fabric Java applications</span></span>

<span data-ttu-id="cad2d-111">對於 Java 應用程式，有 [多個記錄架構](http://en.wikipedia.org/wiki/Java_logging_framework) 可用。</span><span class="sxs-lookup"><span data-stu-id="cad2d-111">For Java applications, [multiple logging frameworks](http://en.wikipedia.org/wiki/Java_logging_framework) are available.</span></span> <span data-ttu-id="cad2d-112">因為`java.util.logging`是 hello 預設選項以 hello JRE，它也會用於 hello[程式碼範例在 github 中的](http://github.com/Azure-Samples/service-fabric-java-getting-started)。</span><span class="sxs-lookup"><span data-stu-id="cad2d-112">Since `java.util.logging` is hello default option with hello JRE, it is also used for hello [code examples in github](http://github.com/Azure-Samples/service-fabric-java-getting-started).</span></span>  <span data-ttu-id="cad2d-113">hello 下列討論內容說明如何 tooconfigure hello`java.util.logging`架構。</span><span class="sxs-lookup"><span data-stu-id="cad2d-113">hello following discussion explains how tooconfigure hello `java.util.logging` framework.</span></span>

<span data-ttu-id="cad2d-114">使用您的應用程式可以將重新導向 java.util.logging 記錄 toomemory、 輸出資料流、 主控台檔案或通訊端。</span><span class="sxs-lookup"><span data-stu-id="cad2d-114">Using java.util.logging you can redirect your application logs toomemory, output streams, console files, or sockets.</span></span> <span data-ttu-id="cad2d-115">每個選項都有 hello 架構中已經提供的預設處理常式。</span><span class="sxs-lookup"><span data-stu-id="cad2d-115">For each of these options, there are default handlers already provided in hello framework.</span></span> <span data-ttu-id="cad2d-116">您可以建立`app.properties`檔案 tooconfigure hello 檔案處理常式為您所有的應用程式 tooredirect 記錄 tooa 本機檔案。</span><span class="sxs-lookup"><span data-stu-id="cad2d-116">You can create a `app.properties` file tooconfigure hello file handler for your application tooredirect all logs tooa local file.</span></span>

<span data-ttu-id="cad2d-117">下列程式碼片段的 hello 包含範例組態：</span><span class="sxs-lookup"><span data-stu-id="cad2d-117">hello following code snippet contains an example configuration:</span></span>

```java
handlers = java.util.logging.FileHandler

java.util.logging.FileHandler.level = ALL
java.util.logging.FileHandler.formatter = java.util.logging.SimpleFormatter
java.util.logging.FileHandler.limit = 1024000
java.util.logging.FileHandler.count = 10
java.util.logging.FileHandler.pattern = /tmp/servicefabric/logs/mysfapp%u.%g.log             
```

<span data-ttu-id="cad2d-118">hello 資料夾指向的 tooby hello`app.properties`檔案必須存在。</span><span class="sxs-lookup"><span data-stu-id="cad2d-118">hello folder pointed tooby hello `app.properties` file must exist.</span></span> <span data-ttu-id="cad2d-119">之後 hello`app.properties`建立檔案，您需要 tooalso 修改項目點指令碼`entrypoint.sh`在 hello`<applicationfolder>/<servicePkg>/Code/`資料夾 tooset hello 屬性`java.util.logging.config.file`太`app.propertes`檔案。</span><span class="sxs-lookup"><span data-stu-id="cad2d-119">After hello `app.properties` file is created, you need tooalso modify your entry point script, `entrypoint.sh` in hello `<applicationfolder>/<servicePkg>/Code/` folder tooset hello property `java.util.logging.config.file` too`app.propertes` file.</span></span> <span data-ttu-id="cad2d-120">hello 項目應該看起來像下列程式碼片段的 hello:</span><span class="sxs-lookup"><span data-stu-id="cad2d-120">hello entry should look like hello following snippet:</span></span>

```sh
java -Djava.library.path=$LD_LIBRARY_PATH -Djava.util.logging.config.file=<path tooapp.properties> -jar <service name>.jar
```


<span data-ttu-id="cad2d-121">此設定會導致在 `/tmp/servicefabric/logs/`中以輪替方式收集記錄檔。</span><span class="sxs-lookup"><span data-stu-id="cad2d-121">This configuration results in logs being collected in a rotating fashion at `/tmp/servicefabric/logs/`.</span></span> <span data-ttu-id="cad2d-122">hello 記錄檔在此情況下名為 mysfapp%u.%g.log 其中：</span><span class="sxs-lookup"><span data-stu-id="cad2d-122">hello log file in this case is named mysfapp%u.%g.log where:</span></span>
* <span data-ttu-id="cad2d-123">**%u**是唯一的數字 tooresolve 同時 Java 處理序之間的衝突。</span><span class="sxs-lookup"><span data-stu-id="cad2d-123">**%u** is a unique number tooresolve conflicts between simultaneous Java processes.</span></span>
* <span data-ttu-id="cad2d-124">**%g**是 hello 產生數字 toodistinguish 之間輪替記錄檔。</span><span class="sxs-lookup"><span data-stu-id="cad2d-124">**%g** is hello generation number toodistinguish between rotating logs.</span></span>

<span data-ttu-id="cad2d-125">根據預設沒有處理常式已明確設定，如果 hello 主控台登錄處理常式。</span><span class="sxs-lookup"><span data-stu-id="cad2d-125">By default if no handler is explicitly configured, hello console handler is registered.</span></span> <span data-ttu-id="cad2d-126">其中一個可以檢視下 /var/log/syslog syslog hello 記錄檔。</span><span class="sxs-lookup"><span data-stu-id="cad2d-126">One can view hello logs in syslog under /var/log/syslog.</span></span>

<span data-ttu-id="cad2d-127">如需詳細資訊，請參閱 hello[程式碼範例在 github 中的](http://github.com/Azure-Samples/service-fabric-java-getting-started)。</span><span class="sxs-lookup"><span data-stu-id="cad2d-127">For more information, see hello [code examples in github](http://github.com/Azure-Samples/service-fabric-java-getting-started).</span></span>  


## <a name="debugging-service-fabric-c-applications"></a><span data-ttu-id="cad2d-128">針對 Service Fabric C# 應用程式進行偵錯</span><span class="sxs-lookup"><span data-stu-id="cad2d-128">Debugging Service Fabric C# applications</span></span>


<span data-ttu-id="cad2d-129">有多個架構適用於追蹤 Linux 上的 CoreCLR 應用程式。</span><span class="sxs-lookup"><span data-stu-id="cad2d-129">Multiple frameworks are available for tracing CoreCLR applications on Linux.</span></span> <span data-ttu-id="cad2d-130">如需詳細資訊，請參閱 [GitHub：logging](http:/github.com/aspnet/logging)。</span><span class="sxs-lookup"><span data-stu-id="cad2d-130">For more information, see [GitHub: logging](http:/github.com/aspnet/logging).</span></span>  <span data-ttu-id="cad2d-131">EventSource 熟悉 tooC # 開發人員，因為 ' 本文使用 EventSource CoreCLR Linux 上的樣本中的追蹤。</span><span class="sxs-lookup"><span data-stu-id="cad2d-131">Since EventSource is familiar tooC# developers,\`this article uses EventSource for tracing in CoreCLR samples on Linux.</span></span>

<span data-ttu-id="cad2d-132">hello 第一個步驟是 tooinclude System.Diagnostics.Tracing，因此您可以撰寫您的記錄檔 toomemory、 輸出資料流或主控台檔案。</span><span class="sxs-lookup"><span data-stu-id="cad2d-132">hello first step is tooinclude System.Diagnostics.Tracing so that you can write your logs toomemory, output streams, or console files.</span></span>  <span data-ttu-id="cad2d-133">如需使用 EventSource 的記錄，加入下列專案 tooyour project.json hello:</span><span class="sxs-lookup"><span data-stu-id="cad2d-133">For logging using EventSource, add hello following project tooyour project.json:</span></span>

```
    "System.Diagnostics.StackTrace": "4.0.1"
```

<span data-ttu-id="cad2d-134">您可以使用自訂的 EventListener toolisten hello 服務事件，並再適當地重新導向 tootrace 檔案。</span><span class="sxs-lookup"><span data-stu-id="cad2d-134">You can use a custom EventListener toolisten for hello service event and then appropriately redirect them tootrace files.</span></span> <span data-ttu-id="cad2d-135">hello 下列程式碼片段顯示使用 EventSource 和自訂 EventListener 記錄的範例實作：</span><span class="sxs-lookup"><span data-stu-id="cad2d-135">hello following code snippet shows a sample implementation of logging using EventSource and a custom EventListener:</span></span>


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

        // TBD: Need tooadd method for sample event.

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


<span data-ttu-id="cad2d-136">hello 先前程式碼片段會輸出中的 hello 記錄 tooa 檔案`/tmp/MyServiceLog.txt`。</span><span class="sxs-lookup"><span data-stu-id="cad2d-136">hello preceding snippet outputs hello logs tooa file in `/tmp/MyServiceLog.txt`.</span></span> <span data-ttu-id="cad2d-137">此檔案名稱必須 toobe 適當地更新。</span><span class="sxs-lookup"><span data-stu-id="cad2d-137">This file name needs toobe appropriately updated.</span></span> <span data-ttu-id="cad2d-138">如果您想 tooredirect hello 記錄 tooconsole，使用下列程式碼片段，您自訂在 EventListener 類別中的 hello:</span><span class="sxs-lookup"><span data-stu-id="cad2d-138">In case you want tooredirect hello logs tooconsole, use hello following snippet in your customized EventListener class:</span></span>

```csharp
public static TextWriter Out = Console.Out;
```

<span data-ttu-id="cad2d-139">hello 範例[C# 範例](https://github.com/Azure-Samples/service-fabric-dotnet-core-getting-started)使用 EventSource 和自訂的 EventListener toolog 事件 tooa 檔案。</span><span class="sxs-lookup"><span data-stu-id="cad2d-139">hello samples at [C# Samples](https://github.com/Azure-Samples/service-fabric-dotnet-core-getting-started) use EventSource and a custom EventListener toolog events tooa file.</span></span>



## <a name="next-steps"></a><span data-ttu-id="cad2d-140">後續步驟</span><span class="sxs-lookup"><span data-stu-id="cad2d-140">Next steps</span></span>
<span data-ttu-id="cad2d-141">hello 相同的追蹤程式碼加入 tooyour 應用程式也會搭配 Azure 的叢集上的應用程式的 hello 診斷。</span><span class="sxs-lookup"><span data-stu-id="cad2d-141">hello same tracing code added tooyour application also works with hello diagnostics of your application on an Azure cluster.</span></span> <span data-ttu-id="cad2d-142">簽出這些文章會討論 hello 的 hello 工具的不同選項，並且描述如何 tooset 註冊它們。</span><span class="sxs-lookup"><span data-stu-id="cad2d-142">Check out these articles that discuss hello different options for hello tools and describe how tooset them up.</span></span>
* [<span data-ttu-id="cad2d-143">Toocollect 使用 Azure 診斷的記錄檔</span><span class="sxs-lookup"><span data-stu-id="cad2d-143">How toocollect logs with Azure Diagnostics</span></span>](service-fabric-diagnostics-how-to-setup-lad.md)
