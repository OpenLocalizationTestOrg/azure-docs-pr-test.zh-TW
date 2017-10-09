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
# <a name="azure-functions-f-developer-reference"></a><span data-ttu-id="251d0-104">Azure Functions F# 開發人員參考</span><span class="sxs-lookup"><span data-stu-id="251d0-104">Azure Functions F# Developer Reference</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="251d0-105">C# 指令碼</span><span class="sxs-lookup"><span data-stu-id="251d0-105">C# script</span></span>](functions-reference-csharp.md)
> * [<span data-ttu-id="251d0-106">F# 指令碼</span><span class="sxs-lookup"><span data-stu-id="251d0-106">F# script</span></span>](functions-reference-fsharp.md)
> * [<span data-ttu-id="251d0-107">Node.js</span><span class="sxs-lookup"><span data-stu-id="251d0-107">Node.js</span></span>](functions-reference-node.md)
> 
> 

<span data-ttu-id="251d0-108">F # Azure 函式是輕鬆 hello 雲端中執行少量的程式碼或 「 函數 」 的解決方案。</span><span class="sxs-lookup"><span data-stu-id="251d0-108">F# for Azure Functions is a solution for easily running small pieces of code, or "functions," in hello cloud.</span></span> <span data-ttu-id="251d0-109">資料會透過函式引數流入您的 F# 函式。</span><span class="sxs-lookup"><span data-stu-id="251d0-109">Data flows into your F# function via function arguments.</span></span> <span data-ttu-id="251d0-110">中指定的引數名稱`function.json`，而且沒有預先定義的存取像是 hello 函式記錄器和取消語彙基元名稱。</span><span class="sxs-lookup"><span data-stu-id="251d0-110">Argument names are specified in `function.json`, and there are predefined names for accessing things like hello function logger and cancellation tokens.</span></span>

<span data-ttu-id="251d0-111">本文章假設，您已閱讀 hello [Azure 函式的開發人員參考](functions-reference.md)。</span><span class="sxs-lookup"><span data-stu-id="251d0-111">This article assumes that you've already read hello [Azure Functions developer reference](functions-reference.md).</span></span>

## <a name="how-fsx-works"></a><span data-ttu-id="251d0-112">.fsx 的運作方式</span><span class="sxs-lookup"><span data-stu-id="251d0-112">How .fsx works</span></span>
<span data-ttu-id="251d0-113">`.fsx` 檔案是 F# 指令碼。</span><span class="sxs-lookup"><span data-stu-id="251d0-113">An `.fsx` file is an F# script.</span></span> <span data-ttu-id="251d0-114">您可以將它視為包含在單一檔案內的 F# 專案。</span><span class="sxs-lookup"><span data-stu-id="251d0-114">It can be thought of as an F# project that's contained in a single file.</span></span> <span data-ttu-id="251d0-115">hello 檔案包含 hello 程式碼，為您的程式 （在此情況下，您的 Azure 函式） 和指示詞，以管理相依性。</span><span class="sxs-lookup"><span data-stu-id="251d0-115">hello file contains both hello code for your program (in this case, your Azure Function) and directives for managing dependencies.</span></span>

<span data-ttu-id="251d0-116">當您使用`.fsx`Azure 函式，通常需要組件會自動包含您允許您 toofocus hello 函式，而不是 「 重複使用 」 程式碼。</span><span class="sxs-lookup"><span data-stu-id="251d0-116">When you use an `.fsx` for an Azure Function, commonly required assemblies are automatically included for you, allowing you toofocus on hello function rather than "boilerplate" code.</span></span>

## <a name="binding-tooarguments"></a><span data-ttu-id="251d0-117">繫結 tooarguments</span><span class="sxs-lookup"><span data-stu-id="251d0-117">Binding tooarguments</span></span>
<span data-ttu-id="251d0-118">每個繫結支援的引數，部分設定為中所述的 hello [Azure 函式的觸發程序和繫結開發人員的參考](functions-triggers-bindings.md)。</span><span class="sxs-lookup"><span data-stu-id="251d0-118">Each binding supports some set of arguments, as detailed in hello [Azure Functions triggers and bindings developer reference](functions-triggers-bindings.md).</span></span> <span data-ttu-id="251d0-119">例如，其中一個 hello blob 的觸發程序支援的引數繫結是 POCO，可以使用 F # 記錄來表示。</span><span class="sxs-lookup"><span data-stu-id="251d0-119">For example, one of hello argument bindings a blob trigger supports is a POCO, which can be expressed using an F# record.</span></span> <span data-ttu-id="251d0-120">例如：</span><span class="sxs-lookup"><span data-stu-id="251d0-120">For example:</span></span>

```fsharp
type Item = { Id: string }

let Run(blob: string, output: byref<Item>) =
    let item = { Id = "Some ID" }
    output <- item
```

<span data-ttu-id="251d0-121">F# Azure 函式會採用一個或多個引數。</span><span class="sxs-lookup"><span data-stu-id="251d0-121">Your F# Azure Function will take one or more arguments.</span></span> <span data-ttu-id="251d0-122">當我們談論 Azure 函式引數時，我們太*輸入*引數和*輸出*引數。</span><span class="sxs-lookup"><span data-stu-id="251d0-122">When we talk about Azure Functions arguments, we refer too*input* arguments and *output* arguments.</span></span> <span data-ttu-id="251d0-123">輸入的引數是完全聽起來： 輸入 tooyour F # Azure 函式。</span><span class="sxs-lookup"><span data-stu-id="251d0-123">An input argument is exactly what it sounds like: input tooyour F# Azure Function.</span></span> <span data-ttu-id="251d0-124">*輸出*引數是可變動的資料或`byref<>`引數做為方法 toopass 資料回*出*函式。</span><span class="sxs-lookup"><span data-stu-id="251d0-124">An *output* argument is mutable data or a `byref<>` argument that serves as a way toopass data back *out* of your function.</span></span>

<span data-ttu-id="251d0-125">在 hello 上述範例中，`blob`是輸入引數，和`output`是輸出引數。</span><span class="sxs-lookup"><span data-stu-id="251d0-125">In hello example above, `blob` is an input argument, and `output` is an output argument.</span></span> <span data-ttu-id="251d0-126">請注意，我們使用`byref<>`如`output`(沒有任何需要 tooadd hello`[<Out>]`註解)。</span><span class="sxs-lookup"><span data-stu-id="251d0-126">Notice that we used `byref<>` for `output` (there's no need tooadd hello `[<Out>]` annotation).</span></span> <span data-ttu-id="251d0-127">使用`byref<>`類型可讓您的記錄或物件 hello 引數會參考的函式 toochange。</span><span class="sxs-lookup"><span data-stu-id="251d0-127">Using a `byref<>` type allows your function toochange which record or object hello argument refers to.</span></span>

<span data-ttu-id="251d0-128">使用 F # 記錄時，做為輸入的類型，hello 記錄定義都必須標記為`[<CLIMutable>]`中排序 tooallow hello Azure 函式架構 tooset hello 欄位之前適當地傳遞 hello 記錄 tooyour 函式。</span><span class="sxs-lookup"><span data-stu-id="251d0-128">When an F# record is used as an input type, hello record definition must be marked with `[<CLIMutable>]` in order tooallow hello Azure Functions framework tooset hello fields appropriately before passing hello record tooyour function.</span></span> <span data-ttu-id="251d0-129">Hello 幕後`[<CLIMutable>]`產生 hello 記錄屬性 setter。</span><span class="sxs-lookup"><span data-stu-id="251d0-129">Under hello hood, `[<CLIMutable>]` generates setters for hello record properties.</span></span> <span data-ttu-id="251d0-130">例如：</span><span class="sxs-lookup"><span data-stu-id="251d0-130">For example:</span></span>

```fsharp
[<CLIMutable>]
type TestObject =
    { SenderName : string
      Greeting : string }

let Run(req: TestObject, log: TraceWriter) =
    { req with Greeting = sprintf "Hello, %s" req.SenderName }
```

<span data-ttu-id="251d0-131">F# 類別也可用於輸入和輸出引數。</span><span class="sxs-lookup"><span data-stu-id="251d0-131">An F# class can also be used for both in and out arguments.</span></span> <span data-ttu-id="251d0-132">針對類別，屬性通常需要 getter 和 setter。</span><span class="sxs-lookup"><span data-stu-id="251d0-132">For a class, properties will usually need getters and setters.</span></span> <span data-ttu-id="251d0-133">例如：</span><span class="sxs-lookup"><span data-stu-id="251d0-133">For example:</span></span>

```fsharp
type Item() =
    member val Id = "" with get,set
    member val Text = "" with get,set

let Run(input: string, item: byref<Item>) =
    let result = Item(Id = input, Text = "Hello from F#!")
    item <- result
```

## <a name="logging"></a><span data-ttu-id="251d0-134">記錄</span><span class="sxs-lookup"><span data-stu-id="251d0-134">Logging</span></span>
<span data-ttu-id="251d0-135">toolog 輸出 tooyour[資料流記錄](../app-service-web/web-sites-streaming-logs-and-console.md)在 F # 中，您的函式應該採取的型別引數`TraceWriter`。</span><span class="sxs-lookup"><span data-stu-id="251d0-135">toolog output tooyour [streaming logs](../app-service-web/web-sites-streaming-logs-and-console.md) in F#, your function should take an argument of type `TraceWriter`.</span></span> <span data-ttu-id="251d0-136">為求一致，我們建議將此引數命名為 `log`。</span><span class="sxs-lookup"><span data-stu-id="251d0-136">For consistency, we recommend this argument is named `log`.</span></span> <span data-ttu-id="251d0-137">例如：</span><span class="sxs-lookup"><span data-stu-id="251d0-137">For example:</span></span>

```fsharp
let Run(blob: string, output: byref<string>, log: TraceWriter) =
    log.Verbose(sprintf "F# Azure Function processed a blob: %s" blob)
    output <- input
```

## <a name="async"></a><span data-ttu-id="251d0-138">非同步處理</span><span class="sxs-lookup"><span data-stu-id="251d0-138">Async</span></span>
<span data-ttu-id="251d0-139">hello`async`可以使用工作流程，但其 hello 結果必須 tooreturn `Task`。</span><span class="sxs-lookup"><span data-stu-id="251d0-139">hello `async` workflow can be used, but hello result needs tooreturn a `Task`.</span></span> <span data-ttu-id="251d0-140">這可以透過 `Async.StartAsTask`來完成，例如︰</span><span class="sxs-lookup"><span data-stu-id="251d0-140">This can be done with `Async.StartAsTask`, for example:</span></span>

```fsharp
let Run(req: HttpRequestMessage) =
    async {
        return new HttpResponseMessage(HttpStatusCode.OK)
    } |> Async.StartAsTask
```

## <a name="cancellation-token"></a><span data-ttu-id="251d0-141">取消權杖</span><span class="sxs-lookup"><span data-stu-id="251d0-141">Cancellation Token</span></span>
<span data-ttu-id="251d0-142">如果您的函式會依正常程序需要 toohandle 關機，您可以提供給它[ `CancellationToken` ](https://msdn.microsoft.com/library/system.threading.cancellationtoken.aspx)引數。</span><span class="sxs-lookup"><span data-stu-id="251d0-142">If your function needs toohandle shutdown gracefully, you can give it a [`CancellationToken`](https://msdn.microsoft.com/library/system.threading.cancellationtoken.aspx) argument.</span></span> <span data-ttu-id="251d0-143">這可與 `async`結合，例如︰</span><span class="sxs-lookup"><span data-stu-id="251d0-143">This can be combined with `async`, for example:</span></span>

```fsharp
let Run(req: HttpRequestMessage, token: CancellationToken)
    let f = async {
        do! Async.Sleep(10)
        return new HttpResponseMessage(HttpStatusCode.OK)
    }
    Async.StartAsTask(f, token)
```

## <a name="importing-namespaces"></a><span data-ttu-id="251d0-144">匯入命名空間</span><span class="sxs-lookup"><span data-stu-id="251d0-144">Importing namespaces</span></span>
<span data-ttu-id="251d0-145">命名空間，請開啟 hello 一般方式：</span><span class="sxs-lookup"><span data-stu-id="251d0-145">Namespaces can be opened in hello usual way:</span></span>

```fsharp
open System.Net
open System.Threading.Tasks

let Run(req: HttpRequestMessage, log: TraceWriter) =
    ...
```

<span data-ttu-id="251d0-146">會自動開啟 hello 下列命名空間：</span><span class="sxs-lookup"><span data-stu-id="251d0-146">hello following namespaces are automatically opened:</span></span>

* `System`
* `System.Collections.Generic`
* `System.IO`
* `System.Linq`
* `System.Net.Http`
* `System.Threading.Tasks`
* `Microsoft.Azure.WebJobs`
* <span data-ttu-id="251d0-147">`Microsoft.Azure.WebJobs.Host`。</span><span class="sxs-lookup"><span data-stu-id="251d0-147">`Microsoft.Azure.WebJobs.Host`.</span></span>

## <a name="referencing-external-assemblies"></a><span data-ttu-id="251d0-148">參考外部組件</span><span class="sxs-lookup"><span data-stu-id="251d0-148">Referencing External Assemblies</span></span>
<span data-ttu-id="251d0-149">同樣地，framework 組件以 hello 新增參考`#r "AssemblyName"`指示詞。</span><span class="sxs-lookup"><span data-stu-id="251d0-149">Similarly, framework assembly references be added with hello `#r "AssemblyName"` directive.</span></span>

```fsharp
#r "System.Web.Http"

open System.Net
open System.Net.Http
open System.Threading.Tasks

let Run(req: HttpRequestMessage, log: TraceWriter) =
    ...
```

<span data-ttu-id="251d0-150">hello 下列組件會自動加入裝載環境的 hello Azure 函式：</span><span class="sxs-lookup"><span data-stu-id="251d0-150">hello following assemblies are automatically added by hello Azure Functions hosting environment:</span></span>

* <span data-ttu-id="251d0-151">`mscorlib`,</span><span class="sxs-lookup"><span data-stu-id="251d0-151">`mscorlib`,</span></span>
* `System`
* `System.Core`
* `System.Xml`
* `System.Net.Http`
* `Microsoft.Azure.WebJobs`
* `Microsoft.Azure.WebJobs.Host`
* `Microsoft.Azure.WebJobs.Extensions`
* `System.Web.Http`
* <span data-ttu-id="251d0-152">`System.Net.Http.Formatting`。</span><span class="sxs-lookup"><span data-stu-id="251d0-152">`System.Net.Http.Formatting`.</span></span>

<span data-ttu-id="251d0-153">此外，下列組件的 hello 是特殊大小寫慣例，而且可能會由 simplename 參考 (例如`#r "AssemblyName"`):</span><span class="sxs-lookup"><span data-stu-id="251d0-153">In addition, hello following assemblies are special cased and may be referenced by simplename (e.g. `#r "AssemblyName"`):</span></span>

* `Newtonsoft.Json`
* `Microsoft.WindowsAzure.Storage`
* `Microsoft.ServiceBus`
* `Microsoft.AspNet.WebHooks.Receivers`
* <span data-ttu-id="251d0-154">`Microsoft.AspNEt.WebHooks.Common`。</span><span class="sxs-lookup"><span data-stu-id="251d0-154">`Microsoft.AspNEt.WebHooks.Common`.</span></span>

<span data-ttu-id="251d0-155">如果您需要 tooreference 私用組件，您可以上傳組件檔 hello`bin`資料夾相對 tooyour 函式，並使用它 （例如 hello 檔案名稱的參考 `#r "MyAssembly.dll"`).</span><span class="sxs-lookup"><span data-stu-id="251d0-155">If you need tooreference a private assembly, you can upload hello assembly file into a `bin` folder relative tooyour function and reference it by using hello file name (e.g.  `#r "MyAssembly.dll"`).</span></span> <span data-ttu-id="251d0-156">上如何 tooupload 檔案 tooyour 函數資料夾的資訊，請參閱 hello 下列封裝管理上的一節。</span><span class="sxs-lookup"><span data-stu-id="251d0-156">For information on how tooupload files tooyour function folder, see hello following section on package management.</span></span>

## <a name="editor-prelude"></a><span data-ttu-id="251d0-157">編輯器序言</span><span class="sxs-lookup"><span data-stu-id="251d0-157">Editor Prelude</span></span>
<span data-ttu-id="251d0-158">支援 F # 編譯器服務的編輯器不會留意 hello 命名空間和 Azure 函式會自動包含的組件。</span><span class="sxs-lookup"><span data-stu-id="251d0-158">An editor that supports F# Compiler Services will not be aware of hello namespaces and assemblies that Azure Functions automatically includes.</span></span> <span data-ttu-id="251d0-159">在這種情況，可能很有用 tooinclude 可協助您使用的 hello 組件的 hello 編輯器 prelude 並 tooexplicitly 開啟命名空間。</span><span class="sxs-lookup"><span data-stu-id="251d0-159">As such, it can be useful tooinclude a prelude that helps hello editor find hello assemblies you are using, and tooexplicitly open namespaces.</span></span> <span data-ttu-id="251d0-160">例如：</span><span class="sxs-lookup"><span data-stu-id="251d0-160">For example:</span></span>

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

<span data-ttu-id="251d0-161">當 Azure 函式會執行您的程式碼時，它會處理與 hello 來源`COMPILED`定義，所以將忽略 hello 編輯器 prelude。</span><span class="sxs-lookup"><span data-stu-id="251d0-161">When Azure Functions executes your code, it processes hello source with `COMPILED` defined, so hello editor prelude will be ignored.</span></span>

<a name="package"></a>

## <a name="package-management"></a><span data-ttu-id="251d0-162">封裝管理</span><span class="sxs-lookup"><span data-stu-id="251d0-162">Package management</span></span>
<span data-ttu-id="251d0-163">在 F # 函式，toouse NuGet 封裝加入`project.json`hello 函式應用程式的檔案系統中檔案 toohello hello 函式的資料夾。</span><span class="sxs-lookup"><span data-stu-id="251d0-163">toouse NuGet packages in an F# function, add a `project.json` file toohello hello function's folder in hello function app's file system.</span></span> <span data-ttu-id="251d0-164">以下是範例`project.json`太新增 NuGet 封裝參考的檔案`Microsoft.ProjectOxford.Face`1.1.0 版：</span><span class="sxs-lookup"><span data-stu-id="251d0-164">Here is an example `project.json` file that adds a NuGet package reference too`Microsoft.ProjectOxford.Face` version 1.1.0:</span></span>

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

<span data-ttu-id="251d0-165">只有 hello.NET Framework 4.6 支援，因此請確定您`project.json`檔案會指定`net46`如下所示。</span><span class="sxs-lookup"><span data-stu-id="251d0-165">Only hello .NET Framework 4.6 is supported, so make sure that your `project.json` file specifies `net46` as shown here.</span></span>

<span data-ttu-id="251d0-166">當您上傳`project.json`檔案中，hello 執行階段取得 hello 封裝，並會自動將參考 toohello 封裝組件。</span><span class="sxs-lookup"><span data-stu-id="251d0-166">When you upload a `project.json` file, hello runtime gets hello packages and automatically adds references toohello package assemblies.</span></span> <span data-ttu-id="251d0-167">您不需要 tooadd`#r "AssemblyName"`指示詞。</span><span class="sxs-lookup"><span data-stu-id="251d0-167">You don't need tooadd `#r "AssemblyName"` directives.</span></span> <span data-ttu-id="251d0-168">只要加入所需的 hello`open`陳述式 tooyour`.fsx`檔案。</span><span class="sxs-lookup"><span data-stu-id="251d0-168">Just add hello required `open` statements tooyour `.fsx` file.</span></span>

<span data-ttu-id="251d0-169">您可能希望 tooput 會自動參考組件，在您的編輯器 prelude，tooimprove 編輯器的 F # 編譯服務互動。</span><span class="sxs-lookup"><span data-stu-id="251d0-169">You may wish tooput automatically references assemblies in your editor prelude, tooimprove your editor's interaction with F# Compile Services.</span></span>

### <a name="how-tooadd-a-projectjson-file-tooyour-azure-function"></a><span data-ttu-id="251d0-170">如何 tooadd`project.json`檔案 tooyour Azure 函式</span><span class="sxs-lookup"><span data-stu-id="251d0-170">How tooadd a `project.json` file tooyour Azure Function</span></span>
1. <span data-ttu-id="251d0-171">藉由確定您的函式應用程式開始執行，您可以這麼做在 hello Azure 入口網站中開啟您的函式。</span><span class="sxs-lookup"><span data-stu-id="251d0-171">Begin by making sure your function app is running, which you can do by opening your function in hello Azure portal.</span></span> <span data-ttu-id="251d0-172">這也會提供存取 toohello 串流記錄將會顯示封裝安裝輸出。</span><span class="sxs-lookup"><span data-stu-id="251d0-172">This also gives access toohello streaming logs where package installation output will be displayed.</span></span>
2. <span data-ttu-id="251d0-173">tooupload`project.json`檔案，請使用其中一種 hello 方法中所述[tooupdate 運作應用程式檔案的方式](functions-reference.md#fileupdate)。</span><span class="sxs-lookup"><span data-stu-id="251d0-173">tooupload a `project.json` file, use one of hello methods described in [how tooupdate function app files](functions-reference.md#fileupdate).</span></span> <span data-ttu-id="251d0-174">如果您使用[Azure 函式的連續部署](functions-continuous-deployment.md)，您可以加入`project.json`檔案 tooyour 暫置中與它的順序 tooexperiment，再將其新增 tooyour 部署分支的分支。</span><span class="sxs-lookup"><span data-stu-id="251d0-174">If you are using [Continuous Deployment for Azure Functions](functions-continuous-deployment.md), you can add a `project.json` file tooyour staging branch in order tooexperiment with it before adding it tooyour deployment branch.</span></span>
3. <span data-ttu-id="251d0-175">之後 hello`project.json`加入檔案之後，您會看到下列函式中的範例的輸出類似 toohello 的資料流記錄：</span><span class="sxs-lookup"><span data-stu-id="251d0-175">After hello `project.json` file is added, you will see output similar toohello following example in your function's streaming log:</span></span>

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

## <a name="environment-variables"></a><span data-ttu-id="251d0-176">環境變數</span><span class="sxs-lookup"><span data-stu-id="251d0-176">Environment variables</span></span>
<span data-ttu-id="251d0-177">tooget 環境變數或應用程式設定值，使用`System.Environment.GetEnvironmentVariable`，例如：</span><span class="sxs-lookup"><span data-stu-id="251d0-177">tooget an environment variable or an app setting value, use `System.Environment.GetEnvironmentVariable`, for example:</span></span>

```fsharp
open System.Environment

let Run(timer: TimerInfo, log: TraceWriter) =
    log.Info("Storage = " + GetEnvironmentVariable("AzureWebJobsStorage"))
    log.Info("Site = " + GetEnvironmentVariable("WEBSITE_SITE_NAME"))
```

## <a name="reusing-fsx-code"></a><span data-ttu-id="251d0-178">重複使用 .fsx 程式碼</span><span class="sxs-lookup"><span data-stu-id="251d0-178">Reusing .fsx code</span></span>
<span data-ttu-id="251d0-179">您可以使用 `#load` 指示詞以使用其他 `.fsx` 檔案中的程式碼。</span><span class="sxs-lookup"><span data-stu-id="251d0-179">You can use code from other `.fsx` files by using a `#load` directive.</span></span> <span data-ttu-id="251d0-180">例如：</span><span class="sxs-lookup"><span data-stu-id="251d0-180">For example:</span></span>

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

<span data-ttu-id="251d0-181">路徑提供 toohello`#load`指示詞會相對 toohello 位置您`.fsx`檔案。</span><span class="sxs-lookup"><span data-stu-id="251d0-181">Paths provides toohello `#load` directive are relative toohello location of your `.fsx` file.</span></span>

* <span data-ttu-id="251d0-182">`#load "logger.fsx"`載入檔案，位於 hello 函式資料夾。</span><span class="sxs-lookup"><span data-stu-id="251d0-182">`#load "logger.fsx"` loads a file located in hello function folder.</span></span>
* <span data-ttu-id="251d0-183">`#load "package\logger.fsx"`載入檔案，位於 hello`package`資料夾中的 hello 函式的資料夾。</span><span class="sxs-lookup"><span data-stu-id="251d0-183">`#load "package\logger.fsx"` loads a file located in hello `package` folder in hello function folder.</span></span>
* <span data-ttu-id="251d0-184">`#load "..\shared\mylogger.fsx"`載入檔案，位於 hello `shared` hello 相同層級為 hello 函式的資料夾，也就是位於資料夾之下`wwwroot`。</span><span class="sxs-lookup"><span data-stu-id="251d0-184">`#load "..\shared\mylogger.fsx"` loads a file located in hello `shared` folder at hello same level as hello function folder, that is, directly under `wwwroot`.</span></span>

<span data-ttu-id="251d0-185">hello`#load`指示詞只能搭配`.fsx`（F # 指令碼） 檔案，而不是使用`.fs`檔案。</span><span class="sxs-lookup"><span data-stu-id="251d0-185">hello `#load` directive only works with `.fsx` (F# script) files, and not with `.fs` files.</span></span>

## <a name="next-steps"></a><span data-ttu-id="251d0-186">後續步驟</span><span class="sxs-lookup"><span data-stu-id="251d0-186">Next steps</span></span>
<span data-ttu-id="251d0-187">如需詳細資訊，請參閱下列資源的 hello:</span><span class="sxs-lookup"><span data-stu-id="251d0-187">For more information, see hello following resources:</span></span>

* [<span data-ttu-id="251d0-188">F# 指南</span><span class="sxs-lookup"><span data-stu-id="251d0-188">F# Guide</span></span>](/dotnet/articles/fsharp/index)
* [<span data-ttu-id="251d0-189">Azure Functions 的最佳作法</span><span class="sxs-lookup"><span data-stu-id="251d0-189">Best Practices for Azure Functions</span></span>](functions-best-practices.md)
* [<span data-ttu-id="251d0-190">Azure Functions 開發人員參考</span><span class="sxs-lookup"><span data-stu-id="251d0-190">Azure Functions developer reference</span></span>](functions-reference.md)
* [<span data-ttu-id="251d0-191">Azure Functions C# 開發人員參考</span><span class="sxs-lookup"><span data-stu-id="251d0-191">Azure Functions C# developer reference</span></span>](functions-reference-csharp.md)
* [<span data-ttu-id="251d0-192">Azure Functions NodeJS 開發人員參考</span><span class="sxs-lookup"><span data-stu-id="251d0-192">Azure Functions NodeJS developer reference</span></span>](functions-reference-node.md)
* [<span data-ttu-id="251d0-193">Azure Functions 觸發程序和繫結</span><span class="sxs-lookup"><span data-stu-id="251d0-193">Azure Functions triggers and bindings</span></span>](functions-triggers-bindings.md)
* [<span data-ttu-id="251d0-194">Azure Functions 測試</span><span class="sxs-lookup"><span data-stu-id="251d0-194">Azure Functions testing</span></span>](functions-test-a-function.md)
* [<span data-ttu-id="251d0-195">Azure Functions 調整</span><span class="sxs-lookup"><span data-stu-id="251d0-195">Azure Functions scaling</span></span>](functions-scale.md)

