---
title: "aaaAzure 函式 F # 開發人員參考資料 |Microsoft 文件"
description: "了解如何 toodevelop Azure 使用 F # 的函式。"
services: functions
documentationcenter: fsharp
author: sylvanc
manager: jbronsk
editor: 
tags: 
keywords: "azure functions, 函式, 事件處理, webhook, 動態計算, 無伺服器架構, F#"
ms.assetid: e60226e5-2630-41d7-9e5b-9f9e5acc8e50
ms.service: functions
ms.devlang: fsharp
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 09/09/2016
ms.author: syclebsc
ms.openlocfilehash: 1ac366ba6f73d191c582dcd9214b688ef719617a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-f-developer-reference"></a>Azure Functions F# 開發人員參考
> [!div class="op_single_selector"]
> * [C# 指令碼](functions-reference-csharp.md)
> * [F# 指令碼](functions-reference-fsharp.md)
> * [Node.js](functions-reference-node.md)
> 
> 

F # Azure 函式是輕鬆 hello 雲端中執行少量的程式碼或 「 函數 」 的解決方案。 資料會透過函式引數流入您的 F# 函式。 中指定的引數名稱`function.json`，而且沒有預先定義的存取像是 hello 函式記錄器和取消語彙基元名稱。

本文章假設，您已閱讀 hello [Azure 函式的開發人員參考](functions-reference.md)。

## <a name="how-fsx-works"></a>.fsx 的運作方式
`.fsx` 檔案是 F# 指令碼。 您可以將它視為包含在單一檔案內的 F# 專案。 hello 檔案包含 hello 程式碼，為您的程式 （在此情況下，您的 Azure 函式） 和指示詞，以管理相依性。

當您使用`.fsx`Azure 函式，通常需要組件會自動包含您允許您 toofocus hello 函式，而不是 「 重複使用 」 程式碼。

## <a name="binding-tooarguments"></a>繫結 tooarguments
每個繫結支援的引數，部分設定為中所述的 hello [Azure 函式的觸發程序和繫結開發人員的參考](functions-triggers-bindings.md)。 例如，其中一個 hello blob 的觸發程序支援的引數繫結是 POCO，可以使用 F # 記錄來表示。 例如：

```fsharp
type Item = { Id: string }

let Run(blob: string, output: byref<Item>) =
    let item = { Id = "Some ID" }
    output <- item
```

F# Azure 函式會採用一個或多個引數。 當我們談論 Azure 函式引數時，我們太*輸入*引數和*輸出*引數。 輸入的引數是完全聽起來： 輸入 tooyour F # Azure 函式。 *輸出*引數是可變動的資料或`byref<>`引數做為方法 toopass 資料回*出*函式。

在 hello 上述範例中，`blob`是輸入引數，和`output`是輸出引數。 請注意，我們使用`byref<>`如`output`(沒有任何需要 tooadd hello`[<Out>]`註解)。 使用`byref<>`類型可讓您的記錄或物件 hello 引數會參考的函式 toochange。

使用 F # 記錄時，做為輸入的類型，hello 記錄定義都必須標記為`[<CLIMutable>]`中排序 tooallow hello Azure 函式架構 tooset hello 欄位之前適當地傳遞 hello 記錄 tooyour 函式。 Hello 幕後`[<CLIMutable>]`產生 hello 記錄屬性 setter。 例如：

```fsharp
[<CLIMutable>]
type TestObject =
    { SenderName : string
      Greeting : string }

let Run(req: TestObject, log: TraceWriter) =
    { req with Greeting = sprintf "Hello, %s" req.SenderName }
```

F# 類別也可用於輸入和輸出引數。 針對類別，屬性通常需要 getter 和 setter。 例如：

```fsharp
type Item() =
    member val Id = "" with get,set
    member val Text = "" with get,set

let Run(input: string, item: byref<Item>) =
    let result = Item(Id = input, Text = "Hello from F#!")
    item <- result
```

## <a name="logging"></a>記錄
toolog 輸出 tooyour[資料流記錄](../app-service-web/web-sites-streaming-logs-and-console.md)在 F # 中，您的函式應該採取的型別引數`TraceWriter`。 為求一致，我們建議將此引數命名為 `log`。 例如：

```fsharp
let Run(blob: string, output: byref<string>, log: TraceWriter) =
    log.Verbose(sprintf "F# Azure Function processed a blob: %s" blob)
    output <- input
```

## <a name="async"></a>非同步處理
hello`async`可以使用工作流程，但其 hello 結果必須 tooreturn `Task`。 這可以透過 `Async.StartAsTask`來完成，例如︰

```fsharp
let Run(req: HttpRequestMessage) =
    async {
        return new HttpResponseMessage(HttpStatusCode.OK)
    } |> Async.StartAsTask
```

## <a name="cancellation-token"></a>取消權杖
如果您的函式會依正常程序需要 toohandle 關機，您可以提供給它[ `CancellationToken` ](https://msdn.microsoft.com/library/system.threading.cancellationtoken.aspx)引數。 這可與 `async`結合，例如︰

```fsharp
let Run(req: HttpRequestMessage, token: CancellationToken)
    let f = async {
        do! Async.Sleep(10)
        return new HttpResponseMessage(HttpStatusCode.OK)
    }
    Async.StartAsTask(f, token)
```

## <a name="importing-namespaces"></a>匯入命名空間
命名空間，請開啟 hello 一般方式：

```fsharp
open System.Net
open System.Threading.Tasks

let Run(req: HttpRequestMessage, log: TraceWriter) =
    ...
```

會自動開啟 hello 下列命名空間：

* `System`
* `System.Collections.Generic`
* `System.IO`
* `System.Linq`
* `System.Net.Http`
* `System.Threading.Tasks`
* `Microsoft.Azure.WebJobs`
* `Microsoft.Azure.WebJobs.Host`。

## <a name="referencing-external-assemblies"></a>參考外部組件
同樣地，framework 組件以 hello 新增參考`#r "AssemblyName"`指示詞。

```fsharp
#r "System.Web.Http"

open System.Net
open System.Net.Http
open System.Threading.Tasks

let Run(req: HttpRequestMessage, log: TraceWriter) =
    ...
```

hello 下列組件會自動加入裝載環境的 hello Azure 函式：

* `mscorlib`,
* `System`
* `System.Core`
* `System.Xml`
* `System.Net.Http`
* `Microsoft.Azure.WebJobs`
* `Microsoft.Azure.WebJobs.Host`
* `Microsoft.Azure.WebJobs.Extensions`
* `System.Web.Http`
* `System.Net.Http.Formatting`。

此外，下列組件的 hello 是特殊大小寫慣例，而且可能會由 simplename 參考 (例如`#r "AssemblyName"`):

* `Newtonsoft.Json`
* `Microsoft.WindowsAzure.Storage`
* `Microsoft.ServiceBus`
* `Microsoft.AspNet.WebHooks.Receivers`
* `Microsoft.AspNEt.WebHooks.Common`。

如果您需要 tooreference 私用組件，您可以上傳組件檔 hello`bin`資料夾相對 tooyour 函式，並使用它 （例如 hello 檔案名稱的參考 `#r "MyAssembly.dll"`). 上如何 tooupload 檔案 tooyour 函數資料夾的資訊，請參閱 hello 下列封裝管理上的一節。

## <a name="editor-prelude"></a>編輯器序言
支援 F # 編譯器服務的編輯器不會留意 hello 命名空間和 Azure 函式會自動包含的組件。 在這種情況，可能很有用 tooinclude 可協助您使用的 hello 組件的 hello 編輯器 prelude 並 tooexplicitly 開啟命名空間。 例如：

```fsharp
#if !COMPILED
#I "../../bin/Binaries/WebJobs.Script.Host"
#r "Microsoft.Azure.WebJobs.Host.dll"
#endif

open Sytem
open Microsoft.Azure.WebJobs.Host

let Run(blob: string, output: byref<string>, log: TraceWriter) =
    ...
```

當 Azure 函式會執行您的程式碼時，它會處理與 hello 來源`COMPILED`定義，所以將忽略 hello 編輯器 prelude。

<a name="package"></a>

## <a name="package-management"></a>封裝管理
在 F # 函式，toouse NuGet 封裝加入`project.json`hello 函式應用程式的檔案系統中檔案 toohello hello 函式的資料夾。 以下是範例`project.json`太新增 NuGet 封裝參考的檔案`Microsoft.ProjectOxford.Face`1.1.0 版：

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

只有 hello.NET Framework 4.6 支援，因此請確定您`project.json`檔案會指定`net46`如下所示。

當您上傳`project.json`檔案中，hello 執行階段取得 hello 封裝，並會自動將參考 toohello 封裝組件。 您不需要 tooadd`#r "AssemblyName"`指示詞。 只要加入所需的 hello`open`陳述式 tooyour`.fsx`檔案。

您可能希望 tooput 會自動參考組件，在您的編輯器 prelude，tooimprove 編輯器的 F # 編譯服務互動。

### <a name="how-tooadd-a-projectjson-file-tooyour-azure-function"></a>如何 tooadd`project.json`檔案 tooyour Azure 函式
1. 藉由確定您的函式應用程式開始執行，您可以這麼做在 hello Azure 入口網站中開啟您的函式。 這也會提供存取 toohello 串流記錄將會顯示封裝安裝輸出。
2. tooupload`project.json`檔案，請使用其中一種 hello 方法中所述[tooupdate 運作應用程式檔案的方式](functions-reference.md#fileupdate)。 如果您使用[Azure 函式的連續部署](functions-continuous-deployment.md)，您可以加入`project.json`檔案 tooyour 暫置中與它的順序 tooexperiment，再將其新增 tooyour 部署分支的分支。
3. 之後 hello`project.json`加入檔案之後，您會看到下列函式中的範例的輸出類似 toohello 的資料流記錄：

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
tooget 環境變數或應用程式設定值，使用`System.Environment.GetEnvironmentVariable`，例如：

```fsharp
open System.Environment

let Run(timer: TimerInfo, log: TraceWriter) =
    log.Info("Storage = " + GetEnvironmentVariable("AzureWebJobsStorage"))
    log.Info("Site = " + GetEnvironmentVariable("WEBSITE_SITE_NAME"))
```

## <a name="reusing-fsx-code"></a>重複使用 .fsx 程式碼
您可以使用 `#load` 指示詞以使用其他 `.fsx` 檔案中的程式碼。 例如：

`run.fsx`

```fsharp
#load "logger.fsx"

let Run(timer: TimerInfo, log: TraceWriter) =
    mylog log (sprintf "Timer: %s" DateTime.Now.ToString())
```

`logger.fsx`

```fsharp
let mylog(log: TraceWriter, text: string) =
    log.Verbose(text);
```

路徑提供 toohello`#load`指示詞會相對 toohello 位置您`.fsx`檔案。

* `#load "logger.fsx"`載入檔案，位於 hello 函式資料夾。
* `#load "package\logger.fsx"`載入檔案，位於 hello`package`資料夾中的 hello 函式的資料夾。
* `#load "..\shared\mylogger.fsx"`載入檔案，位於 hello `shared` hello 相同層級為 hello 函式的資料夾，也就是位於資料夾之下`wwwroot`。

hello`#load`指示詞只能搭配`.fsx`（F # 指令碼） 檔案，而不是使用`.fs`檔案。

## <a name="next-steps"></a>後續步驟
如需詳細資訊，請參閱下列資源的 hello:

* [F# 指南](/dotnet/articles/fsharp/index)
* [Azure Functions 的最佳作法](functions-best-practices.md)
* [Azure Functions 開發人員參考](functions-reference.md)
* [Azure Functions C# 開發人員參考](functions-reference-csharp.md)
* [Azure Functions NodeJS 開發人員參考](functions-reference-node.md)
* [Azure Functions 觸發程序和繫結](functions-triggers-bindings.md)
* [Azure Functions 測試](functions-test-a-function.md)
* [Azure Functions 調整](functions-scale.md)

