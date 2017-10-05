---
title: "Azure Functions F# 開發人員參考 | Microsoft Docs"
description: "了解如何使用 F# 開發 Azure Functions。"
services: functions
documentationcenter: fsharp
author: sylvanc
manager: jbronsk
editor: 
tags: 
keywords: "azure 函式、 函式、 事件處理 webhook、 動態的計算、 無伺服器的架構，F #"
ms.assetid: e60226e5-2630-41d7-9e5b-9f9e5acc8e50
ms.service: functions
ms.devlang: fsharp
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 09/09/2016
ms.author: syclebsc
ms.openlocfilehash: 1691d378263f6b4ce5072f5c621d8db02f774b5f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="azure-functions-f-developer-reference"></a><span data-ttu-id="c7fd0-104">Azure Functions F# 開發人員參考</span><span class="sxs-lookup"><span data-stu-id="c7fd0-104">Azure Functions F# Developer Reference</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c7fd0-105">C# 指令碼</span><span class="sxs-lookup"><span data-stu-id="c7fd0-105">C# script</span></span>](functions-reference-csharp.md)
> * [<span data-ttu-id="c7fd0-106">F# 指令碼</span><span class="sxs-lookup"><span data-stu-id="c7fd0-106">F# script</span></span>](functions-reference-fsharp.md)
> * [<span data-ttu-id="c7fd0-107">Node.js</span><span class="sxs-lookup"><span data-stu-id="c7fd0-107">Node.js</span></span>](functions-reference-node.md)
> 
> 

<span data-ttu-id="c7fd0-108">Azure Functions 的 F# 是可在雲端輕鬆執行程式碼片段或「函式」的解決方案。</span><span class="sxs-lookup"><span data-stu-id="c7fd0-108">F# for Azure Functions is a solution for easily running small pieces of code, or "functions," in the cloud.</span></span> <span data-ttu-id="c7fd0-109">資料會透過函式引數流入您的 F# 函式。</span><span class="sxs-lookup"><span data-stu-id="c7fd0-109">Data flows into your F# function via function arguments.</span></span> <span data-ttu-id="c7fd0-110">引數名稱會指定於 `function.json`中，而且有預先定義的名稱可用來存取函式記錄器和取消權杖等項目。</span><span class="sxs-lookup"><span data-stu-id="c7fd0-110">Argument names are specified in `function.json`, and there are predefined names for accessing things like the function logger and cancellation tokens.</span></span>

<span data-ttu-id="c7fd0-111">本文假設您已經讀過 [Azure Functions 開發人員參考](functions-reference.md)。</span><span class="sxs-lookup"><span data-stu-id="c7fd0-111">This article assumes that you've already read the [Azure Functions developer reference](functions-reference.md).</span></span>

## <a name="how-fsx-works"></a><span data-ttu-id="c7fd0-112">.fsx 的運作方式</span><span class="sxs-lookup"><span data-stu-id="c7fd0-112">How .fsx works</span></span>
<span data-ttu-id="c7fd0-113">`.fsx` 檔案是 F# 指令碼。</span><span class="sxs-lookup"><span data-stu-id="c7fd0-113">An `.fsx` file is an F# script.</span></span> <span data-ttu-id="c7fd0-114">您可以將它視為包含在單一檔案內的 F# 專案。</span><span class="sxs-lookup"><span data-stu-id="c7fd0-114">It can be thought of as an F# project that's contained in a single file.</span></span> <span data-ttu-id="c7fd0-115">檔案包含程式的程式碼 (在此案例中為您的 Azure 函式) 和用於管理相依性的指示詞。</span><span class="sxs-lookup"><span data-stu-id="c7fd0-115">The file contains both the code for your program (in this case, your Azure Function) and directives for managing dependencies.</span></span>

<span data-ttu-id="c7fd0-116">當您使用 Azure 函式的 `.fsx` 時，其中會自動包含常用的必要組件，讓您得以專注於函式本身而非「重複使用」的程式碼。</span><span class="sxs-lookup"><span data-stu-id="c7fd0-116">When you use an `.fsx` for an Azure Function, commonly required assemblies are automatically included for you, allowing you to focus on the function rather than "boilerplate" code.</span></span>

## <a name="binding-to-arguments"></a><span data-ttu-id="c7fd0-117">繫結至引數</span><span class="sxs-lookup"><span data-stu-id="c7fd0-117">Binding to arguments</span></span>
<span data-ttu-id="c7fd0-118">如 [Azure Functions 觸發程序和繫結開發人員參考](functions-triggers-bindings.md)所述，每個繫結都支援某幾組引數。</span><span class="sxs-lookup"><span data-stu-id="c7fd0-118">Each binding supports some set of arguments, as detailed in the [Azure Functions triggers and bindings developer reference](functions-triggers-bindings.md).</span></span> <span data-ttu-id="c7fd0-119">例如，Blob 觸發程序支援的其中一個引數繫結是可使用 F# 記錄來表示的 POCO。</span><span class="sxs-lookup"><span data-stu-id="c7fd0-119">For example, one of the argument bindings a blob trigger supports is a POCO, which can be expressed using an F# record.</span></span> <span data-ttu-id="c7fd0-120">例如：</span><span class="sxs-lookup"><span data-stu-id="c7fd0-120">For example:</span></span>

```fsharp
type Item = { Id: string }

let Run(blob: string, output: byref<Item>) =
    let item = { Id = "Some ID" }
    output <- item
```

<span data-ttu-id="c7fd0-121">F# Azure 函式會採用一個或多個引數。</span><span class="sxs-lookup"><span data-stu-id="c7fd0-121">Your F# Azure Function will take one or more arguments.</span></span> <span data-ttu-id="c7fd0-122">在談論 Azure Functions 引數時，我們指的是*輸入*引數和*輸出*引數。</span><span class="sxs-lookup"><span data-stu-id="c7fd0-122">When we talk about Azure Functions arguments, we refer to *input* arguments and *output* arguments.</span></span> <span data-ttu-id="c7fd0-123">輸入引數的用途正如其名︰輸入到 F# Azure 函式。</span><span class="sxs-lookup"><span data-stu-id="c7fd0-123">An input argument is exactly what it sounds like: input to your F# Azure Function.</span></span> <span data-ttu-id="c7fd0-124">*輸出*引數是可變動的資料或 `byref<>` 引數，可用來將資料從函式*往外*送回。</span><span class="sxs-lookup"><span data-stu-id="c7fd0-124">An *output* argument is mutable data or a `byref<>` argument that serves as a way to pass data back *out* of your function.</span></span>

<span data-ttu-id="c7fd0-125">在上述範例中，`blob` 是輸入引數，而 `output` 是輸出引數。</span><span class="sxs-lookup"><span data-stu-id="c7fd0-125">In the example above, `blob` is an input argument, and `output` is an output argument.</span></span> <span data-ttu-id="c7fd0-126">請注意，我們使用 `byref<>` 做為 `output` (不必加上 `[<Out>]` 註解)。</span><span class="sxs-lookup"><span data-stu-id="c7fd0-126">Notice that we used `byref<>` for `output` (there's no need to add the `[<Out>]` annotation).</span></span> <span data-ttu-id="c7fd0-127">使用 `byref<>` 類型可讓您的函式變更引數所指稱的記錄或物件。</span><span class="sxs-lookup"><span data-stu-id="c7fd0-127">Using a `byref<>` type allows your function to change which record or object the argument refers to.</span></span>

<span data-ttu-id="c7fd0-128">使用 F# 記錄做為輸入類型時，記錄定義必須標上 `[<CLIMutable>]` ，以便讓 Azure Functions 架構先適當地設定欄位，再將記錄傳遞給您的函式。</span><span class="sxs-lookup"><span data-stu-id="c7fd0-128">When an F# record is used as an input type, the record definition must be marked with `[<CLIMutable>]` in order to allow the Azure Functions framework to set the fields appropriately before passing the record to your function.</span></span> <span data-ttu-id="c7fd0-129">實際上， `[<CLIMutable>]` 會產生記錄屬性的 setter。</span><span class="sxs-lookup"><span data-stu-id="c7fd0-129">Under the hood, `[<CLIMutable>]` generates setters for the record properties.</span></span> <span data-ttu-id="c7fd0-130">例如：</span><span class="sxs-lookup"><span data-stu-id="c7fd0-130">For example:</span></span>

```fsharp
[<CLIMutable>]
type TestObject =
    { SenderName : string
      Greeting : string }

let Run(req: TestObject, log: TraceWriter) =
    { req with Greeting = sprintf "Hello, %s" req.SenderName }
```

<span data-ttu-id="c7fd0-131">F# 類別也可用於輸入和輸出引數。</span><span class="sxs-lookup"><span data-stu-id="c7fd0-131">An F# class can also be used for both in and out arguments.</span></span> <span data-ttu-id="c7fd0-132">針對類別，屬性通常需要 getter 和 setter。</span><span class="sxs-lookup"><span data-stu-id="c7fd0-132">For a class, properties will usually need getters and setters.</span></span> <span data-ttu-id="c7fd0-133">例如：</span><span class="sxs-lookup"><span data-stu-id="c7fd0-133">For example:</span></span>

```fsharp
type Item() =
    member val Id = "" with get,set
    member val Text = "" with get,set

let Run(input: string, item: byref<Item>) =
    let result = Item(Id = input, Text = "Hello from F#!")
    item <- result
```

## <a name="logging"></a><span data-ttu-id="c7fd0-134">記錄</span><span class="sxs-lookup"><span data-stu-id="c7fd0-134">Logging</span></span>
<span data-ttu-id="c7fd0-135">若要將輸出記錄至 F# 的[串流記錄](../app-service-web/web-sites-streaming-logs-and-console.md)，您的函式應該採用 `TraceWriter` 類型的引數。</span><span class="sxs-lookup"><span data-stu-id="c7fd0-135">To log output to your [streaming logs](../app-service-web/web-sites-streaming-logs-and-console.md) in F#, your function should take an argument of type `TraceWriter`.</span></span> <span data-ttu-id="c7fd0-136">為求一致，我們建議將此引數命名為 `log`。</span><span class="sxs-lookup"><span data-stu-id="c7fd0-136">For consistency, we recommend this argument is named `log`.</span></span> <span data-ttu-id="c7fd0-137">例如：</span><span class="sxs-lookup"><span data-stu-id="c7fd0-137">For example:</span></span>

```fsharp
let Run(blob: string, output: byref<string>, log: TraceWriter) =
    log.Verbose(sprintf "F# Azure Function processed a blob: %s" blob)
    output <- input
```

## <a name="async"></a><span data-ttu-id="c7fd0-138">非同步處理</span><span class="sxs-lookup"><span data-stu-id="c7fd0-138">Async</span></span>
<span data-ttu-id="c7fd0-139">可以使用 `async` 工作流程，但結果需要傳回 `Task`。</span><span class="sxs-lookup"><span data-stu-id="c7fd0-139">The `async` workflow can be used, but the result needs to return a `Task`.</span></span> <span data-ttu-id="c7fd0-140">這可以透過 `Async.StartAsTask`來完成，例如︰</span><span class="sxs-lookup"><span data-stu-id="c7fd0-140">This can be done with `Async.StartAsTask`, for example:</span></span>

```fsharp
let Run(req: HttpRequestMessage) =
    async {
        return new HttpResponseMessage(HttpStatusCode.OK)
    } |> Async.StartAsTask
```

## <a name="cancellation-token"></a><span data-ttu-id="c7fd0-141">取消權杖</span><span class="sxs-lookup"><span data-stu-id="c7fd0-141">Cancellation Token</span></span>
<span data-ttu-id="c7fd0-142">如果您的函式需要正常地處理關閉，您可以為其指定 [`CancellationToken`](https://msdn.microsoft.com/library/system.threading.cancellationtoken.aspx) 引數。</span><span class="sxs-lookup"><span data-stu-id="c7fd0-142">If your function needs to handle shutdown gracefully, you can give it a [`CancellationToken`](https://msdn.microsoft.com/library/system.threading.cancellationtoken.aspx) argument.</span></span> <span data-ttu-id="c7fd0-143">這可與 `async`結合，例如︰</span><span class="sxs-lookup"><span data-stu-id="c7fd0-143">This can be combined with `async`, for example:</span></span>

```fsharp
let Run(req: HttpRequestMessage, token: CancellationToken)
    let f = async {
        do! Async.Sleep(10)
        return new HttpResponseMessage(HttpStatusCode.OK)
    }
    Async.StartAsTask(f, token)
```

## <a name="importing-namespaces"></a><span data-ttu-id="c7fd0-144">匯入命名空間</span><span class="sxs-lookup"><span data-stu-id="c7fd0-144">Importing namespaces</span></span>
<span data-ttu-id="c7fd0-145">命名空間可透過一般方式開啟︰</span><span class="sxs-lookup"><span data-stu-id="c7fd0-145">Namespaces can be opened in the usual way:</span></span>

```fsharp
open System.Net
open System.Threading.Tasks

let Run(req: HttpRequestMessage, log: TraceWriter) =
    ...
```

<span data-ttu-id="c7fd0-146">下列命名空間會自動開啟︰</span><span class="sxs-lookup"><span data-stu-id="c7fd0-146">The following namespaces are automatically opened:</span></span>

* `System`
* `System.Collections.Generic`
* `System.IO`
* `System.Linq`
* `System.Net.Http`
* `System.Threading.Tasks`
* `Microsoft.Azure.WebJobs`
* <span data-ttu-id="c7fd0-147">`Microsoft.Azure.WebJobs.Host`。</span><span class="sxs-lookup"><span data-stu-id="c7fd0-147">`Microsoft.Azure.WebJobs.Host`.</span></span>

## <a name="referencing-external-assemblies"></a><span data-ttu-id="c7fd0-148">參考外部組件</span><span class="sxs-lookup"><span data-stu-id="c7fd0-148">Referencing External Assemblies</span></span>
<span data-ttu-id="c7fd0-149">同樣地，在新增架構組件參考時也可以加上 `#r "AssemblyName"` 指示詞。</span><span class="sxs-lookup"><span data-stu-id="c7fd0-149">Similarly, framework assembly references be added with the `#r "AssemblyName"` directive.</span></span>

```fsharp
#r "System.Web.Http"

open System.Net
open System.Net.Http
open System.Threading.Tasks

let Run(req: HttpRequestMessage, log: TraceWriter) =
    ...
```

<span data-ttu-id="c7fd0-150">Azure Functions 裝載環境會自動加入下列組件︰</span><span class="sxs-lookup"><span data-stu-id="c7fd0-150">The following assemblies are automatically added by the Azure Functions hosting environment:</span></span>

* <span data-ttu-id="c7fd0-151">`mscorlib`,</span><span class="sxs-lookup"><span data-stu-id="c7fd0-151">`mscorlib`,</span></span>
* `System`
* `System.Core`
* `System.Xml`
* `System.Net.Http`
* `Microsoft.Azure.WebJobs`
* `Microsoft.Azure.WebJobs.Host`
* `Microsoft.Azure.WebJobs.Extensions`
* `System.Web.Http`
* <span data-ttu-id="c7fd0-152">`System.Net.Http.Formatting`。</span><span class="sxs-lookup"><span data-stu-id="c7fd0-152">`System.Net.Http.Formatting`.</span></span>

<span data-ttu-id="c7fd0-153">此外，下列組件為特殊案例，可以使用簡單名稱來參考 (例如 `#r "AssemblyName"`)：</span><span class="sxs-lookup"><span data-stu-id="c7fd0-153">In addition, the following assemblies are special cased and may be referenced by simplename (e.g. `#r "AssemblyName"`):</span></span>

* `Newtonsoft.Json`
* `Microsoft.WindowsAzure.Storage`
* `Microsoft.ServiceBus`
* `Microsoft.AspNet.WebHooks.Receivers`
* <span data-ttu-id="c7fd0-154">`Microsoft.AspNEt.WebHooks.Common`。</span><span class="sxs-lookup"><span data-stu-id="c7fd0-154">`Microsoft.AspNEt.WebHooks.Common`.</span></span>

<span data-ttu-id="c7fd0-155">如果您需要參考私用組件，您可以將組件檔案上傳至您函式的相對 `bin` 資料夾，然後使用檔案名稱來參考它 (例如 `#r "MyAssembly.dll"`)。</span><span class="sxs-lookup"><span data-stu-id="c7fd0-155">If you need to reference a private assembly, you can upload the assembly file into a `bin` folder relative to your function and reference it by using the file name (e.g.  `#r "MyAssembly.dll"`).</span></span> <span data-ttu-id="c7fd0-156">如需如何將檔案上傳至函數資料夾的資訊，請參閱以下的＜封裝管理＞小節。</span><span class="sxs-lookup"><span data-stu-id="c7fd0-156">For information on how to upload files to your function folder, see the following section on package management.</span></span>

## <a name="editor-prelude"></a><span data-ttu-id="c7fd0-157">編輯器序言</span><span class="sxs-lookup"><span data-stu-id="c7fd0-157">Editor Prelude</span></span>
<span data-ttu-id="c7fd0-158">支援 F# 編譯器服務的編輯器不會知道 Azure Functions 自動包含的命名空間和組件。</span><span class="sxs-lookup"><span data-stu-id="c7fd0-158">An editor that supports F# Compiler Services will not be aware of the namespaces and assemblies that Azure Functions automatically includes.</span></span> <span data-ttu-id="c7fd0-159">因此，最好在其中包含序言以協助編輯器找到您使用的組件，並明確開啟命名空間。</span><span class="sxs-lookup"><span data-stu-id="c7fd0-159">As such, it can be useful to include a prelude that helps the editor find the assemblies you are using, and to explicitly open namespaces.</span></span> <span data-ttu-id="c7fd0-160">例如：</span><span class="sxs-lookup"><span data-stu-id="c7fd0-160">For example:</span></span>

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

<span data-ttu-id="c7fd0-161">當 Azure Functions 執行程式碼時，它會在定義了 `COMPILED` 的情況下處理來源，所以編輯器序言會遭到忽略。</span><span class="sxs-lookup"><span data-stu-id="c7fd0-161">When Azure Functions executes your code, it processes the source with `COMPILED` defined, so the editor prelude will be ignored.</span></span>

<a name="package"></a>

## <a name="package-management"></a><span data-ttu-id="c7fd0-162">封裝管理</span><span class="sxs-lookup"><span data-stu-id="c7fd0-162">Package management</span></span>
<span data-ttu-id="c7fd0-163">若要在 F# 函式中使用 NuGet 封裝，請將 `project.json` 檔案新增至函式應用程式檔案系統中的函式資料夾。</span><span class="sxs-lookup"><span data-stu-id="c7fd0-163">To use NuGet packages in an F# function, add a `project.json` file to the the function's folder in the function app's file system.</span></span> <span data-ttu-id="c7fd0-164">以下的 `project.json` 範例檔案會對 `Microsoft.ProjectOxford.Face` 1.1.0 版新增 NuGet 封裝參考︰</span><span class="sxs-lookup"><span data-stu-id="c7fd0-164">Here is an example `project.json` file that adds a NuGet package reference to `Microsoft.ProjectOxford.Face` version 1.1.0:</span></span>

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

<span data-ttu-id="c7fd0-165">只有 .NET Framework 4.6 會受到支援，因此請確認您的 `project.json` 檔案會如這裡所示指定 `net46`。</span><span class="sxs-lookup"><span data-stu-id="c7fd0-165">Only the .NET Framework 4.6 is supported, so make sure that your `project.json` file specifies `net46` as shown here.</span></span>

<span data-ttu-id="c7fd0-166">當您上傳 `project.json` 檔案時，執行階段會取得封裝並自動加入對封裝組件的參考。</span><span class="sxs-lookup"><span data-stu-id="c7fd0-166">When you upload a `project.json` file, the runtime gets the packages and automatically adds references to the package assemblies.</span></span> <span data-ttu-id="c7fd0-167">您不需要加入 `#r "AssemblyName"` 指示詞。</span><span class="sxs-lookup"><span data-stu-id="c7fd0-167">You don't need to add `#r "AssemblyName"` directives.</span></span> <span data-ttu-id="c7fd0-168">只需將必要的 `open` 陳述式加入您的 `.fsx` 檔案。</span><span class="sxs-lookup"><span data-stu-id="c7fd0-168">Just add the required `open` statements to your `.fsx` file.</span></span>

<span data-ttu-id="c7fd0-169">您可能會想在編輯器序言中自動放入參考組件，來改善您的編輯器與 F# 編譯器服務的互動。</span><span class="sxs-lookup"><span data-stu-id="c7fd0-169">You may wish to put automatically references assemblies in your editor prelude, to improve your editor's interaction with F# Compile Services.</span></span>

### <a name="how-to-add-a-projectjson-file-to-your-azure-function"></a><span data-ttu-id="c7fd0-170">如何將 `project.json` 檔案新增至 Azure 函式</span><span class="sxs-lookup"><span data-stu-id="c7fd0-170">How to add a `project.json` file to your Azure Function</span></span>
1. <span data-ttu-id="c7fd0-171">首先，在 Azure 入口網站中開啟您的函式，以確定函式應用程式正在執行中。</span><span class="sxs-lookup"><span data-stu-id="c7fd0-171">Begin by making sure your function app is running, which you can do by opening your function in the Azure portal.</span></span> <span data-ttu-id="c7fd0-172">這也可供存取將要顯示封裝安裝輸出的串流記錄檔。</span><span class="sxs-lookup"><span data-stu-id="c7fd0-172">This also gives access to the streaming logs where package installation output will be displayed.</span></span>
2. <span data-ttu-id="c7fd0-173">若要上傳 `project.json` 檔案，請使用 [如何更新函式應用程式檔案](functions-reference.md#fileupdate)中所述的其中一個方法。</span><span class="sxs-lookup"><span data-stu-id="c7fd0-173">To upload a `project.json` file, use one of the methods described in [how to update function app files](functions-reference.md#fileupdate).</span></span> <span data-ttu-id="c7fd0-174">如果您使用 [Azure Functions 的持續部署](functions-continuous-deployment.md)，您可以將 `project.json` 檔案新增預備分支，以便在試驗過後再將它新增至部署分支。</span><span class="sxs-lookup"><span data-stu-id="c7fd0-174">If you are using [Continuous Deployment for Azure Functions](functions-continuous-deployment.md), you can add a `project.json` file to your staging branch in order to experiment with it before adding it to your deployment branch.</span></span>
3. <span data-ttu-id="c7fd0-175">加入 `project.json` 檔案之後，您會在函式的串流記錄中看到類似下列範例的輸出：</span><span class="sxs-lookup"><span data-stu-id="c7fd0-175">After the `project.json` file is added, you will see output similar to the following example in your function's streaming log:</span></span>

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

## <a name="environment-variables"></a><span data-ttu-id="c7fd0-176">環境變數</span><span class="sxs-lookup"><span data-stu-id="c7fd0-176">Environment variables</span></span>
<span data-ttu-id="c7fd0-177">若要取得環境變數或應用程式設定值，請使用 `System.Environment.GetEnvironmentVariable`，例如：</span><span class="sxs-lookup"><span data-stu-id="c7fd0-177">To get an environment variable or an app setting value, use `System.Environment.GetEnvironmentVariable`, for example:</span></span>

```fsharp
open System.Environment

let Run(timer: TimerInfo, log: TraceWriter) =
    log.Info("Storage = " + GetEnvironmentVariable("AzureWebJobsStorage"))
    log.Info("Site = " + GetEnvironmentVariable("WEBSITE_SITE_NAME"))
```

## <a name="reusing-fsx-code"></a><span data-ttu-id="c7fd0-178">重複使用 .fsx 程式碼</span><span class="sxs-lookup"><span data-stu-id="c7fd0-178">Reusing .fsx code</span></span>
<span data-ttu-id="c7fd0-179">您可以使用 `#load` 指示詞以使用其他 `.fsx` 檔案中的程式碼。</span><span class="sxs-lookup"><span data-stu-id="c7fd0-179">You can use code from other `.fsx` files by using a `#load` directive.</span></span> <span data-ttu-id="c7fd0-180">例如：</span><span class="sxs-lookup"><span data-stu-id="c7fd0-180">For example:</span></span>

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

<span data-ttu-id="c7fd0-181">提供給 `#load` 指示詞的路徑會相對於 `.fsx` 檔案的位置。</span><span class="sxs-lookup"><span data-stu-id="c7fd0-181">Paths provides to the `#load` directive are relative to the location of your `.fsx` file.</span></span>

* <span data-ttu-id="c7fd0-182">`#load "logger.fsx"` 會載入位於函式資料夾中的檔案。</span><span class="sxs-lookup"><span data-stu-id="c7fd0-182">`#load "logger.fsx"` loads a file located in the function folder.</span></span>
* <span data-ttu-id="c7fd0-183">`#load "package\logger.fsx"` 會載入位於函式資料夾的 `package`資料夾中的檔案。</span><span class="sxs-lookup"><span data-stu-id="c7fd0-183">`#load "package\logger.fsx"` loads a file located in the `package` folder in the function folder.</span></span>
* <span data-ttu-id="c7fd0-184">`#load "..\shared\mylogger.fsx"` 會載入位於與函式資料夾相同層級的 `shared`資料夾中的檔案 (也就是在 `wwwroot` 的正下方)。</span><span class="sxs-lookup"><span data-stu-id="c7fd0-184">`#load "..\shared\mylogger.fsx"` loads a file located in the `shared` folder at the same level as the function folder, that is, directly under `wwwroot`.</span></span>

<span data-ttu-id="c7fd0-185">`#load` 指示詞只能搭配 `.fsx` (F# 指令碼) 檔案運作，而不能與 `.fs` 檔案搭配。</span><span class="sxs-lookup"><span data-stu-id="c7fd0-185">The `#load` directive only works with `.fsx` (F# script) files, and not with `.fs` files.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c7fd0-186">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c7fd0-186">Next steps</span></span>
<span data-ttu-id="c7fd0-187">如需詳細資訊，請參閱下列資源：</span><span class="sxs-lookup"><span data-stu-id="c7fd0-187">For more information, see the following resources:</span></span>

* [<span data-ttu-id="c7fd0-188">F# 指南</span><span class="sxs-lookup"><span data-stu-id="c7fd0-188">F# Guide</span></span>](/dotnet/articles/fsharp/index)
* [<span data-ttu-id="c7fd0-189">Azure Functions 的最佳作法</span><span class="sxs-lookup"><span data-stu-id="c7fd0-189">Best Practices for Azure Functions</span></span>](functions-best-practices.md)
* [<span data-ttu-id="c7fd0-190">Azure Functions 開發人員參考</span><span class="sxs-lookup"><span data-stu-id="c7fd0-190">Azure Functions developer reference</span></span>](functions-reference.md)
* [<span data-ttu-id="c7fd0-191">Azure Functions C# 開發人員參考</span><span class="sxs-lookup"><span data-stu-id="c7fd0-191">Azure Functions C# developer reference</span></span>](functions-reference-csharp.md)
* [<span data-ttu-id="c7fd0-192">Azure Functions NodeJS 開發人員參考</span><span class="sxs-lookup"><span data-stu-id="c7fd0-192">Azure Functions NodeJS developer reference</span></span>](functions-reference-node.md)
* [<span data-ttu-id="c7fd0-193">Azure Functions 觸發程序和繫結</span><span class="sxs-lookup"><span data-stu-id="c7fd0-193">Azure Functions triggers and bindings</span></span>](functions-triggers-bindings.md)
* [<span data-ttu-id="c7fd0-194">Azure Functions 測試</span><span class="sxs-lookup"><span data-stu-id="c7fd0-194">Azure Functions testing</span></span>](functions-test-a-function.md)
* [<span data-ttu-id="c7fd0-195">Azure Functions 調整</span><span class="sxs-lookup"><span data-stu-id="c7fd0-195">Azure Functions scaling</span></span>](functions-scale.md)

