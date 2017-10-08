---
title: "aaaAzure 函式 C# 指令碼開發人員參考資料 |Microsoft 文件"
description: "了解如何 toodevelop Azure 函式使用 C#。"
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
ms.openlocfilehash: 27a8f4eb77497a373ff4031539e2e930585e48e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-c-script-developer-reference"></a>Azure Functions C# 指令碼開發人員參考
> [!div class="op_single_selector"]
> * [C# 指令碼](functions-reference-csharp.md)
> * [F# 指令碼](functions-reference-fsharp.md)
> * [Node.js](functions-reference-node.md)
>
>

hello Azure WebJobs SDK 是以基礎 hello Azure 函式的 C# 指令碼體驗。 資料會透過方法引數流入您的 C# 函式。 中指定的引數名稱`function.json`，而且沒有預先定義的存取像是 hello 函式記錄器和取消語彙基元名稱。

本文章假設，您已閱讀 hello [Azure 函式的開發人員參考](functions-reference.md)。

如需使用 C# 類別庫的詳細資訊，請參閱[使用 .NET 類別庫搭配 Azure Functions](functions-dotnet-class-library.md)。

## <a name="how-csx-works"></a>.csx 的運作方式
hello`.csx`格式可讓您 toowrite 小於 「 重複使用 」，並專注於撰寫只是 C# 函式。 像往常一樣包含任何組件參考和在 hello 檔案 hello 開頭的命名空間。 只需定義 `Run` 方法，而不用在命名空間和類別中包裝所有項目。 如果您需要 tooinclude 任何類別，用於執行個體 toodefine 純舊 CLR 物件 (POCO) 物件，您可以包含內部的類別 hello 相同的檔案。   

## <a name="binding-tooarguments"></a>繫結 tooarguments
hello 各種繫結是繫結的 tooa C# 函式，透過 hello`name`屬性在 hello *function.json*組態。 每個繫結都有自己支援的類型；例如，Blob 觸發程序可以支援字串、POCO 或 CloudBlockBlob。 hello 支援類型會記錄在每個繫結的 hello 參考。 POCO 物件的每個屬性必須定義 getter 和 setter。

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

您可以使用方法的傳回值的輸出繫結使用 hello 名稱`$return`中*function.json*:

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

toowrite 多個值 tooan 輸出繫結，請使用 hello [ `ICollector` ](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/ICollector.cs)或[ `IAsyncCollector` ](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IAsyncCollector.cs)型別。 這些類型是唯寫的集合寫入的 toohello 輸出繫結 hello 方法完成時。

這個範例會使用 `ICollector` 寫入多個佇列訊息：

```csharp
public static void Run(ICollector<string> myQueueItem, TraceWriter log)
{
    myQueueItem.Add("Hello");
    myQueueItem.Add("World!");
}
```

## <a name="logging"></a>記錄
toolog 輸出 tooyour C# 中的資料流記錄，包含一個引數的型別`TraceWriter`。 建議您將它命名為 `log`。 避免在 Azure Functions 中使用 `Console.Write`。 

`TraceWriter`定義在 hello [Azure WebJobs SDK](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.Host/TraceWriter.cs)。 hello 記錄層級`TraceWriter`可在設定[主機\.json]。

```csharp
public static void Run(string myBlob, TraceWriter log)
{
    log.Info($"C# Blob trigger function processed: {myBlob}");
}
```

## <a name="async"></a>非同步處理
toomake 非同步函式使用 hello`async`關鍵字，並傳回`Task`物件。

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
某些作業需要正常關機。 它一律是損毀，萬一您想要 toohandle 正常關機的要求，可以處理的最佳 toowrite 代碼定義[ `CancellationToken` ](https://msdn.microsoft.com/library/system.threading.cancellationtoken.aspx)型別引數。  A`CancellationToken`提供 toosignal 主機關機時觸發。

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
如果您需要 tooimport 命名空間，您可以像往常一樣，以 hello`using`子句。

```csharp
using System.Net;
using System.Threading.Tasks;

public static Task<HttpResponseMessage> Run(HttpRequestMessage req, TraceWriter log)
```

hello 下列命名空間會自動匯入，因此選擇性：

* `System`
* `System.Collections.Generic`
* `System.IO`
* `System.Linq`
* `System.Net.Http`
* `System.Threading.Tasks`
* `Microsoft.Azure.WebJobs`
* `Microsoft.Azure.WebJobs.Host`

## <a name="referencing-external-assemblies"></a>參考外部組件
針對 framework 組件，請將參考加入使用 hello`#r "AssemblyName"`指示詞。

```csharp
#r "System.Web.Http"

using System.Net;
using System.Net.Http;
using System.Threading.Tasks;

public static Task<HttpResponseMessage> Run(HttpRequestMessage req, TraceWriter log)
```

hello 下列組件會自動加入裝載環境的 hello Azure 函式：

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

hello 參考下列組件可能是由簡單名稱 (例如， `#r "AssemblyName"`):

* `Newtonsoft.Json`
* `Microsoft.WindowsAzure.Storage`
* `Microsoft.ServiceBus`
* `Microsoft.AspNet.WebHooks.Receivers`
* `Microsoft.AspNet.WebHooks.Common`
* `Microsoft.Azure.NotificationHubs`

## <a name="referencing-custom-assemblies"></a>參考自訂組件

tooreference 自訂組件，您可以使用*共用*組件或*私人*組件：
- 共用組件會共用於函式應用程式內的所有函式。 tooreference 自訂組件上, 傳 hello 組件 tooyour 函式應用程式，例如`bin`hello 函式應用程式根目錄中的資料夾。 
- 私人組件屬於所指定函式的內容，而且支援不同版本的側載。 應該在私用組件上傳`bin`hello 函式的目錄資料夾中。 參考使用 hello 檔案名稱，例如`#r "MyAssembly.dll"`。 

上如何 tooupload 檔案 tooyour 函數資料夾的資訊，請參閱 hello 下列封裝管理上的一節。

### <a name="watched-directories"></a>監看的目錄

變更 tooassemblies 自動監看 hello 目錄，包含 hello 函式的指令碼檔案。 toowatch 組件中的變更其他目錄，將它們加入 toohello`watchDirectories`清單中[主機\.json]。

## <a name="using-nuget-packages"></a>使用 NuGet 套件
在 C# 函式，toouse NuGet 封裝上傳*project.json* hello 函式應用程式的檔案系統中檔案 toohello 函式的資料夾。 以下是範例*project.json*會新增參考 tooMicrosoft.ProjectOxford.Face 版本 1.1.0 的檔案：

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

只有 hello.NET Framework 4.6 支援，因此請確定您*project.json*檔案會指定`net46`如下所示。

當您上傳*project.json*檔案中，hello 執行階段取得 hello 封裝，並會自動將參考 toohello 封裝組件。 您不需要 tooadd`#r "AssemblyName"`指示詞。 hello 的 NuGet 封裝中定義的 toouse hello 型別新增所需的 hello`using`陳述式 tooyour *run.csx*檔案 

在 hello 函式的執行階段，NuGet 還原的運作方式是比較`project.json`和`project.lock.json`。 如果 hello hello 檔案的日期和時間戳記**不**相符項目，NuGet 還原執行並 NuGet 下載已更新的封裝。 不過，如果 hello hello 檔案的日期和時間戳記**不要**NuGet 相符項目，不會執行還原。 因此，`project.lock.json`不應部署因為它會導致 NuGet tooskip 封裝還原。 部署 hello 鎖定 tooavoid file、 add hello `project.lock.json` toohello`.gitignore`檔案。

toouse 自訂 NuGet 摘要中，指定摘要中的 hello *Nuget.Config* hello 函式應用程式根目錄中的檔案。 如需詳細資訊，請參閱[設定 NuGet 行為](/nuget/consume-packages/configuring-nuget-behavior)。

### <a name="using-a-projectjson-file"></a>使用 project.json 檔案
1. 開啟 hello Azure 入口網站中的 hello 函式。 hello 記錄 索引標籤會顯示 hello 封裝安裝輸出。
2. tooupload project.json 檔案中，使用其中一種 hello 中所述的 hello 方法[tooupdate 運作應用程式檔案的方式](functions-reference.md#fileupdate)hello Azure 函式開發人員參考主題。
3. 之後 hello *project.json*上傳檔案時，您會看到類似下列範例函式中的 hello 輸出的資料流記錄：

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
tooget 環境變數或應用程式設定值，使用`System.Environment.GetEnvironmentVariable`hello 下列程式碼範例所示：

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
您可以在您的 *run.csx* 檔案中使用其他 *.csx* 檔案中定義的類別和方法。 可使用 toodo`#load`指示詞中的您*run.csx*檔案。 在下列範例的 hello，記錄常式命名為`MyLogger`中共用*myLogger.csx*並載入*run.csx*使用 hello`#load`指示詞：

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

使用共用*.csx*是常見的模式，當您想 toostrongly 時輸入您使用 POCO 物件的函式之間的引數。 Hello 下列簡化的範例，在 HTTP 觸發程序和佇列觸發程序共用名為 POCO 物件`Order`toostrongly 類型 hello 訂單資料：

HTTP 觸發程序的範例 *run.csx*︰

```cs
#load "..\shared\order.csx"

using System.Net;

public static async Task<HttpResponseMessage> Run(Order req, IAsyncCollector<Order> outputQueueItem, TraceWriter log)
{
    log.Info("C# HTTP trigger function received an order.");
    log.Info(req.ToString());
    log.Info("Submitting tooprocessing queue.");

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

您可以使用相對路徑，以 hello`#load`指示詞：

* `#load "mylogger.csx"`載入檔案，位於 hello 函式資料夾。
* `#load "loadedfiles\mylogger.csx"`載入檔案，位於 hello 函式資料夾中的資料夾。
* `#load "..\shared\mylogger.csx"`載入位於的 hello 相同層級為 hello 函式的資料夾，也就是在資料夾中的檔案直接在*wwwroot*。

hello`#load`指示詞只適用於*.csx* （C# 指令碼） 檔案，不能搭配*.cs*檔案。

<a name="imperative-bindings"></a> 

## <a name="binding-at-runtime-via-imperative-bindings"></a>透過命令式繫結在執行階段繫結

在 C# 和其他.NET 語言，您可以使用[命令式](https://en.wikipedia.org/wiki/Imperative_programming)繫結模式，但不要 toohello [*宣告式*](https://en.wikipedia.org/wiki/Declarative_programming)中的繫結*function.json*. 命令式的繫結時，必須在執行階段，而不是設計階段計算 toobe 繫結參數。 此模式中，您可以繫結 toosupported 輸入，並輸出函式程式碼中的繫結上作業。

定義命令式繫結，如下所示︰

- **請勿**在 *function.json* 中為您所需的命令式繫結併入項目。
- 傳入輸入參數 [`Binder binder`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.Host/Bindings/Runtime/Binder.cs) 或 [`IBinder binder`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IBinder.cs)。
- 使用下列 C# 模式 tooperform hello 資料繫結的 hello。

```cs
using (var output = await binder.BindAsync<T>(new BindingTypeAttribute(...)))
{
    ...
}
```

其中`BindingTypeAttribute`hello.NET 屬性可定義您的繫結和`T`是 hello 該繫結類型所支援的輸入或輸出類型。 `T` 也不能是 `out` 參數類型 (例如 `out JObject`)。 例如，Mobile Apps 資料表輸出繫結支援[六個輸出類型](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.MobileApps/MobileTableAttribute.cs#L17-L22)，但您只可以對 `T` 使用 [ICollector<T>](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/ICollector.cs) 或 [IAsyncCollector<T>](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IAsyncCollector.cs)。

下列範例程式碼的 hello 建立[儲存體 blob 輸出繫結](functions-bindings-storage-blob.md#using-a-blob-output-binding)與 blob 路徑，定義在執行階段，然後字串 toohello 將 blob 寫入。

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

[BlobAttribute](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/BlobAttribute.cs)定義 hello[儲存體 blob](functions-bindings-storage-blob.md)輸入或輸出繫結，以及[TextWriter](https://msdn.microsoft.com/library/system.io.textwriter.aspx)是支援的輸出繫結型別。
Hello 程式碼，取得儲存體帳戶連接字串 hello hello 預設應用程式設定 (也就是`AzureWebJobsStorage`)。 您可以加入，以指定自訂應用程式設定 toouse [StorageAccountAttribute](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs)並傳遞到 hello 屬性陣列`BindAsync<T>()`。 例如，

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

hello 下表列出針對其定義每個繫結型別和 hello 封裝 hello.NET 屬性。

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
如需詳細資訊，請參閱下列資源的 hello:

* [Azure Functions 的最佳作法](functions-best-practices.md)
* [Azure Functions 開發人員參考](functions-reference.md)
* [Azure Functions F# 開發人員參考](functions-reference-fsharp.md)
* [Azure Functions NodeJS 開發人員參考](functions-reference-node.md)
* [Azure Functions 觸發程序和繫結](functions-triggers-bindings.md)

[host\.json]: https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json
