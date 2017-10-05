---
title: "Azure Functions C# 指令碼開發人員參考 | Microsoft Docs"
description: "了解如何使用 C# 開發 Azure Functions。"
services: functions
documentationcenter: na
author: lindydonna
manager: erikre
editor: 
tags: 
keywords: "azure functions, 函式, 事件處理, webhook, 動態計算, 無伺服器架構"
ms.assetid: f28cda01-15f3-4047-83f3-e89d5728301c
ms.service: functions
ms.devlang: dotnet
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 06/07/2017
ms.author: donnam
ms.openlocfilehash: 83a351ce0279ada8ce7fe0513497349471334a86
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="azure-functions-c-script-developer-reference"></a>Azure Functions C# 指令碼開發人員參考
> [!div class="op_single_selector"]
> * [C# 指令碼](functions-reference-csharp.md)
> * [F# 指令碼](functions-reference-fsharp.md)
> * [Node.js](functions-reference-node.md)
>
>

Azure Functions 的 C# 指令碼體驗是以 Azure WebJobs SDK 為基礎。 資料會透過方法引數流入您的 C# 函式。 引數名稱會指定於 `function.json`中，而且有預先定義的名稱可用來存取函式記錄器和取消權杖等項目。

本文假設您已經讀過 [Azure Functions 開發人員參考](functions-reference.md)。

如需使用 C# 類別庫的詳細資訊，請參閱[使用 .NET 類別庫搭配 Azure Functions](functions-dotnet-class-library.md)。

## <a name="how-csx-works"></a>.csx 的運作方式
`.csx` 格式允許撰寫較少「重複使用」文字，只專注於撰寫 C# 函式。 像往常一樣，在檔案開頭包含任何組件參考和命名空間。 只需定義 `Run` 方法，而不用在命名空間和類別中包裝所有項目。 如果您需要包含任何類別，例如若要定義純舊 CLR 物件 (POCO) 物件，您可以包含相同檔案內的類別。   

## <a name="binding-to-arguments"></a>繫結至引數
各種繫結會透過 *function.json* 組態中的 `name` 屬性繫結至 C# 函式。 每個繫結都有自己支援的類型；例如，Blob 觸發程序可以支援字串、POCO 或 CloudBlockBlob。 支援的類型會記錄在每個繫結的參考中。 POCO 物件的每個屬性必須定義 getter 和 setter。

```csharp
public static void Run(string myBlob, out MyClass myQueueItem)
{
    log.Verbose($"C# Blob trigger function processed: {myBlob}");
    myQueueItem = new MyClass() { Id = "myid" };
}

public class MyClass
{
    public string Id { get; set; }
}
```

[!INCLUDE [HTTP client best practices](../../includes/functions-http-client-best-practices.md)]

## <a name="using-method-return-value-for-output-binding"></a>使用輸出繫結的方法傳回值

您可以使用 function.json 中的名稱 `$return`，使用輸出繫結的方法傳回值：

```json
{
    "type": "queue",
    "direction": "out",
    "name": "$return",
    "queueName": "outqueue",
    "connection": "MyStorageConnectionString",
}
```

```csharp
public static string Run(string input, TraceWriter log)
{
    return input;
}
```

## <a name="writing-multiple-output-values"></a>撰寫多個輸出值

若要多個值寫入至輸出繫結，請使用 [`ICollector`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/ICollector.cs) 或 [`IAsyncCollector`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IAsyncCollector.cs) 類型。 這些類型是在方法完成時，寫入至輸出繫結的唯寫集合。

這個範例會使用 `ICollector` 寫入多個佇列訊息：

```csharp
public static void Run(ICollector<string> myQueueItem, TraceWriter log)
{
    myQueueItem.Add("Hello");
    myQueueItem.Add("World!");
}
```

## <a name="logging"></a>記錄
若要使用 C# 將輸出記錄至串流記錄，請包含 `TraceWriter` 類型的引數。 建議您將它命名為 `log`。 避免在 Azure Functions 中使用 `Console.Write`。 

`TraceWriter` 已定義於 [Azure WebJobs SDK](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.Host/TraceWriter.cs)。 可以在 [host\.json] 中設定 `TraceWriter` 的記錄層級。

```csharp
public static void Run(string myBlob, TraceWriter log)
{
    log.Info($"C# Blob trigger function processed: {myBlob}");
}
```

## <a name="async"></a>非同步處理
若要讓函式變成非同步，請使用 `async` 關鍵字並傳回 `Task` 物件。

```csharp
public async static Task ProcessQueueMessageAsync(
        string blobName,
        Stream blobInput,
        Stream blobOutput)
{
    await blobInput.CopyToAsync(blobOutput, 4096, token);
}
```

## <a name="cancellation-token"></a>取消權杖
某些作業需要正常關機。 雖然撰寫能夠處理當機情況的程式碼一律是最理想的做法，但是如果您想要處理順利關機要求，您可以定義 [`CancellationToken`](https://msdn.microsoft.com/library/system.threading.cancellationtoken.aspx) 類型的引數。  提供 `CancellationToken` ，表示已觸發主機關機。

```csharp
public async static Task ProcessQueueMessageAsyncCancellationToken(
        string blobName,
        Stream blobInput,
        Stream blobOutput,
        CancellationToken token)
    {
        await blobInput.CopyToAsync(blobOutput, 4096, token);
    }
```

## <a name="importing-namespaces"></a>匯入命名空間
如果您需要匯入命名空間，可以如往常一樣利用 `using` 子句。

```csharp
using System.Net;
using System.Threading.Tasks;

public static Task<HttpResponseMessage> Run(HttpRequestMessage req, TraceWriter log)
```

下列命名空間會自動匯入，所以是選擇性的︰

* `System`
* `System.Collections.Generic`
* `System.IO`
* `System.Linq`
* `System.Net.Http`
* `System.Threading.Tasks`
* `Microsoft.Azure.WebJobs`
* `Microsoft.Azure.WebJobs.Host`

## <a name="referencing-external-assemblies"></a>參考外部組件
若為架構組件，請使用 `#r "AssemblyName"` 指示詞加入參考。

```csharp
#r "System.Web.Http"

using System.Net;
using System.Net.Http;
using System.Threading.Tasks;

public static Task<HttpResponseMessage> Run(HttpRequestMessage req, TraceWriter log)
```

Azure Functions 裝載環境會自動加入下列組件︰

* `mscorlib`
* `System`
* `System.Core`
* `System.Xml`
* `System.Net.Http`
* `Microsoft.Azure.WebJobs`
* `Microsoft.Azure.WebJobs.Host`
* `Microsoft.Azure.WebJobs.Extensions`
* `System.Web.Http`
* `System.Net.Http.Formatting`

simple-name 可能會參考下列組件 (例如，`#r "AssemblyName"`)：

* `Newtonsoft.Json`
* `Microsoft.WindowsAzure.Storage`
* `Microsoft.ServiceBus`
* `Microsoft.AspNet.WebHooks.Receivers`
* `Microsoft.AspNet.WebHooks.Common`
* `Microsoft.Azure.NotificationHubs`

## <a name="referencing-custom-assemblies"></a>參考自訂組件

若要參考自訂組件，您可以使用「共用」組件或「私人」組件：
- 共用組件會共用於函式應用程式內的所有函式。 若要參考自訂組件上，請將組件上傳至應用程式函式，例如在函式應用程式根目錄的 `bin` 資料夾中。 
- 私人組件屬於所指定函式的內容，而且支援不同版本的側載。 應該在函式目錄的 `bin` 資料夾中上傳私人組件。 使用檔案名稱 (例如 `#r "MyAssembly.dll"`) 進行參照。 

如需如何將檔案上傳至函數資料夾的資訊，請參閱以下的＜封裝管理＞小節。

### <a name="watched-directories"></a>監看的目錄

系統會自動監看包含函式指令碼檔案之目錄中的組件變更。 若要監看其他目錄中的組件變更，將它們新增至 [host\.json] 中的 `watchDirectories` 清單。

## <a name="using-nuget-packages"></a>使用 NuGet 套件
若要在 C# 函式中使用 NuGet 套件，請將 project.json  檔案上傳至函式應用程式檔案系統中的函式資料夾。 以下是範例 project.json  檔案，該檔案會加入對 Microsoft.ProjectOxford.Face 1.1.0 版的參考：

```json
{
  "frameworks": {
    "net46":{
      "dependencies": {
        "Microsoft.ProjectOxford.Face": "1.1.0"
      }
    }
   }
}
```

只支援 .NET Framework 4.6，因此請確認您的 *project.json* 檔案指定 `net46`，如以下所示。

當您上傳 project.json  檔案時，執行階段會取得封裝並自動加入對封裝組件的參考。 您不需要加入 `#r "AssemblyName"` 指示詞。 若要使用 NuGet 套件中定義的類型，請將所需的 `using` 陳述式新增到 *run.csx* 檔案 

在 Functions 執行階段中，NuGet 還原會透過比較 `project.json` 和 `project.lock.json` 來運作。 如果檔案的日期和時間戳記**不**相符，會執行 NuGet 還原，且 NuGet 會下載更新的套件。 不過，如果檔案的日期和時間戳記**相符**，NuGet 不會執行還原。 因此，不應該部署 `project.lock.json`，因為它會導致 NuGet 略過還原。 若要避免部署鎖定檔案，請將 `project.lock.json` 加入至 `.gitignore` 檔案。

若要使用自訂 NuGet 摘要，請在函式應用程式根目錄的 *Nuget.Config* 檔案中指定摘要。 如需詳細資訊，請參閱[設定 NuGet 行為](/nuget/consume-packages/configuring-nuget-behavior)。

### <a name="using-a-projectjson-file"></a>使用 project.json 檔案
1. 在 Azure 入口網站中開啟函式。 [記錄] 索引標籤會顯示套件安裝輸出。
2. 若要上傳 project.json 檔案，請使用 Azure Functions 開發人員參考主題的[如何更新函式應用程式檔案](functions-reference.md#fileupdate)所述的其中一個方法。
3. 上傳 project.json  檔案之後，您會在函式的串流記錄檔中看到如下列範例所示的輸出：

```
2016-04-04T19:02:48.745 Restoring packages.
2016-04-04T19:02:48.745 Starting NuGet restore
2016-04-04T19:02:50.183 MSBuild auto-detection: using msbuild version '14.0' from 'D:\Program Files (x86)\MSBuild\14.0\bin'.
2016-04-04T19:02:50.261 Feeds used:
2016-04-04T19:02:50.261 C:\DWASFiles\Sites\facavalfunctest\LocalAppData\NuGet\Cache
2016-04-04T19:02:50.261 https://api.nuget.org/v3/index.json
2016-04-04T19:02:50.261
2016-04-04T19:02:50.511 Restoring packages for D:\home\site\wwwroot\HttpTriggerCSharp1\Project.json...
2016-04-04T19:02:52.800 Installing Newtonsoft.Json 6.0.8.
2016-04-04T19:02:52.800 Installing Microsoft.ProjectOxford.Face 1.1.0.
2016-04-04T19:02:57.095 All packages are compatible with .NETFramework,Version=v4.6.
2016-04-04T19:02:57.189
2016-04-04T19:02:57.189
2016-04-04T19:02:57.455 Packages restored.
```

## <a name="environment-variables"></a>環境變數
若要取得環境變數或應用程式設定值，請使用 `System.Environment.GetEnvironmentVariable`，如下列程式碼範例所示：

```csharp
public static void Run(TimerInfo myTimer, TraceWriter log)
{
    log.Info($"C# Timer trigger function executed at: {DateTime.Now}");
    log.Info(GetEnvironmentVariable("AzureWebJobsStorage"));
    log.Info(GetEnvironmentVariable("WEBSITE_SITE_NAME"));
}

public static string GetEnvironmentVariable(string name)
{
    return name + ": " +
        System.Environment.GetEnvironmentVariable(name, EnvironmentVariableTarget.Process);
}
```

## <a name="reusing-csx-code"></a>重複使用 .csx 程式碼
您可以在您的 *run.csx* 檔案中使用其他 *.csx* 檔案中定義的類別和方法。 若要這樣做，請在您的 *run.csx* 檔案中使用 `#load` 指示詞。 在下列範例中，名為 `MyLogger` 的記錄常式已在 *myLogger.csx* 中共用，並使用 `#load` 指示詞載入至 *run.csx*︰

範例 run.csx ：

```csharp
#load "mylogger.csx"

public static void Run(TimerInfo myTimer, TraceWriter log)
{
    log.Verbose($"Log by run.csx: {DateTime.Now}");
    MyLogger(log, $"Log by MyLogger: {DateTime.Now}");
}
```

範例 mylogger.csx ：

```csharp
public static void MyLogger(TraceWriter log, string logtext)
{
    log.Verbose(logtext);
}
```

當您想要在使用一個 POCO 物件的函式之間使引數成為強式類型，使用共用的 *.csx* 是常見的模式。 在下列簡化的範例中，HTTP 觸發程序和佇列觸發程序共用一個名為 `Order` 的 POCO 物件，來使排序資料成為強式類型︰

HTTP 觸發程序的範例 *run.csx*︰

```cs
#load "..\shared\order.csx"

using System.Net;

public static async Task<HttpResponseMessage> Run(Order req, IAsyncCollector<Order> outputQueueItem, TraceWriter log)
{
    log.Info("C# HTTP trigger function received an order.");
    log.Info(req.ToString());
    log.Info("Submitting to processing queue.");

    if (req.orderId == null)
    {
        return new HttpResponseMessage(HttpStatusCode.BadRequest);
    }
    else
    {
        await outputQueueItem.AddAsync(req);
        return new HttpResponseMessage(HttpStatusCode.OK);
    }
}
```

佇列觸發程序的範例 *run.csx*︰

```cs
#load "..\shared\order.csx"

using System;

public static void Run(Order myQueueItem, out Order outputQueueItem,TraceWriter log)
{
    log.Info($"C# Queue trigger function processed order...");
    log.Info(myQueueItem.ToString());

    outputQueueItem = myQueueItem;
}
```

範例 *order.csx*：

```cs
public class Order
{
    public string orderId {get; set; }
    public string custName {get; set;}
    public string custAddress {get; set;}
    public string custEmail {get; set;}
    public string cartId {get; set; }

    public override String ToString()
    {
        return "\n{\n\torderId : " + orderId +
                  "\n\tcustName : " + custName +             
                  "\n\tcustAddress : " + custAddress +             
                  "\n\tcustEmail : " + custEmail +             
                  "\n\tcartId : " + cartId + "\n}";             
    }
}
```

您可以使用包含 `#load` 指示詞的相對路徑：

* `#load "mylogger.csx"` 會載入位於函式資料夾中的檔案。
* `#load "loadedfiles\mylogger.csx"` 會載入位於函式資料夾的資料夾中的檔案。
* `#load "..\shared\mylogger.csx"` 會載入位於與函式資料夾相同層級的資料夾中的檔案 (也就是在 [wwwroot] 的正下方)。

`#load` 指示詞只適用於 *.csx* (C# 指令碼) 檔案，不適用於 *.cs* 檔案。

<a name="imperative-bindings"></a> 

## <a name="binding-at-runtime-via-imperative-bindings"></a>透過命令式繫結在執行階段繫結

在 C# 和其他 .NET 語言中，您可以使用相對於 *function.json* 中[*宣告式*](https://en.wikipedia.org/wiki/Declarative_programming)繫結的[命令式](https://en.wikipedia.org/wiki/Imperative_programming)繫結模式。 當繫結參數需要在執行階段而不是設計階段中計算時，命令式繫結非常有用。 利用此模式，您可以快速在您的函式程式碼中繫結至支援的輸入和輸出繫結。

定義命令式繫結，如下所示︰

- **請勿**在 *function.json* 中為您所需的命令式繫結併入項目。
- 傳入輸入參數 [`Binder binder`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.Host/Bindings/Runtime/Binder.cs) 或 [`IBinder binder`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IBinder.cs)。
- 使用下列 C# 模式來執行資料繫結。

```cs
using (var output = await binder.BindAsync<T>(new BindingTypeAttribute(...)))
{
    ...
}
```

其中 `BindingTypeAttribute` 是可定義繫結的.NET 屬性，而 `T` 是該繫結類型支援的輸入或輸出類型。 `T` 也不能是 `out` 參數類型 (例如 `out JObject`)。 例如，Mobile Apps 資料表輸出繫結支援[六個輸出類型](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.MobileApps/MobileTableAttribute.cs#L17-L22)，但您只可以對 `T` 使用 [ICollector<T>](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/ICollector.cs) 或 [IAsyncCollector<T>](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IAsyncCollector.cs)。

下列範例程式碼會使用在執行階段定義的 blob 路徑來建立[儲存體 blob 輸出繫結](functions-bindings-storage-blob.md#using-a-blob-output-binding)，然後將字串寫入 blob。

```cs
using Microsoft.Azure.WebJobs;
using Microsoft.Azure.WebJobs.Host.Bindings.Runtime;

public static async Task Run(string input, Binder binder)
{
    using (var writer = await binder.BindAsync<TextWriter>(new BlobAttribute("samples-output/path")))
    {
        writer.Write("Hello World!!");
    }
}
```

[BlobAttribute](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/BlobAttribute.cs) 會定義[儲存體 blob](functions-bindings-storage-blob.md) 輸入或輸出繫結，而 [TextWriter](https://msdn.microsoft.com/library/system.io.textwriter.aspx) 是支援的輸出繫結類型。
此程式碼會依原樣取得儲存體帳戶連接字串的預設應用程式設定 (也就是 `AzureWebJobsStorage`)。 您可以指定要使用的自訂應用程式設定，方法是新增 [StorageAccountAttribute](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs) 並將屬性陣列傳遞至 `BindAsync<T>()`。 例如，

```cs
using Microsoft.Azure.WebJobs;
using Microsoft.Azure.WebJobs.Host.Bindings.Runtime;

public static async Task Run(string input, Binder binder)
{
    var attributes = new Attribute[]
    {    
        new BlobAttribute("samples-output/path"),
        new StorageAccountAttribute("MyStorageAccount")
    };

    using (var writer = await binder.BindAsync<TextWriter>(attributes))
    {
        writer.Write("Hello World!");
    }
}
```

下表列出每個繫結類型的 .NET 屬性，以及定義它們的套件。

> [!div class="mx-codeBreakAll"]
| 繫結 | 屬性 | 新增參考 |
|------|------|------|
| Cosmos DB | [`Microsoft.Azure.WebJobs.DocumentDBAttribute`](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.DocumentDB/DocumentDBAttribute.cs) | `#r "Microsoft.Azure.WebJobs.Extensions.DocumentDB"` |
| 事件中樞 | [`Microsoft.Azure.WebJobs.ServiceBus.EventHubAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/EventHubs/EventHubAttribute.cs), [`Microsoft.Azure.WebJobs.ServiceBusAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAccountAttribute.cs) | `#r "Microsoft.Azure.Jobs.ServiceBus"` |
| 行動應用程式 | [`Microsoft.Azure.WebJobs.MobileTableAttribute`](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.MobileApps/MobileTableAttribute.cs) | `#r "Microsoft.Azure.WebJobs.Extensions.MobileApps"` |
| 通知中樞 | [`Microsoft.Azure.WebJobs.NotificationHubAttribute`](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.NotificationHubs/NotificationHubAttribute.cs) | `#r "Microsoft.Azure.WebJobs.Extensions.NotificationHubs"` |
| 服務匯流排 | [`Microsoft.Azure.WebJobs.ServiceBusAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAttribute.cs), [`Microsoft.Azure.WebJobs.ServiceBusAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAccountAttribute.cs) | `#r "Microsoft.Azure.WebJobs.ServiceBus"` |
| 儲存體佇列 | [`Microsoft.Azure.WebJobs.QueueAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/QueueAttribute.cs), [`Microsoft.Azure.WebJobs.StorageAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs) | |
| 儲存體 Blob | [`Microsoft.Azure.WebJobs.BlobAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/BlobAttribute.cs), [`Microsoft.Azure.WebJobs.StorageAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs) | |
| 儲存體資料表 | [`Microsoft.Azure.WebJobs.TableAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/TableAttribute.cs), [`Microsoft.Azure.WebJobs.StorageAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs) | |
| Twilio | [`Microsoft.Azure.WebJobs.TwilioSmsAttribute`](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.Twilio/TwilioSMSAttribute.cs) | `#r "Microsoft.Azure.WebJobs.Extensions.Twilio"` |



## <a name="next-steps"></a>後續步驟
如需詳細資訊，請參閱下列資源：

* [Azure Functions 的最佳做法](functions-best-practices.md)
* [Azure Functions 開發人員參考](functions-reference.md)
* [Azure Functions F# 開發人員參考](functions-reference-fsharp.md)
* [Azure Functions NodeJS 開發人員參考](functions-reference-node.md)
* [Azure Functions 觸發程序和繫結](functions-triggers-bindings.md)

[host\.json]: https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json
