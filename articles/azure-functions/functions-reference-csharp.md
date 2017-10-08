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
# <a name="azure-functions-c-script-developer-reference"></a><span data-ttu-id="8013a-104">Azure Functions C# 指令碼開發人員參考</span><span class="sxs-lookup"><span data-stu-id="8013a-104">Azure Functions C# script developer reference</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="8013a-105">C# 指令碼</span><span class="sxs-lookup"><span data-stu-id="8013a-105">C# script</span></span>](functions-reference-csharp.md)
> * [<span data-ttu-id="8013a-106">F# 指令碼</span><span class="sxs-lookup"><span data-stu-id="8013a-106">F# script</span></span>](functions-reference-fsharp.md)
> * [<span data-ttu-id="8013a-107">Node.js</span><span class="sxs-lookup"><span data-stu-id="8013a-107">Node.js</span></span>](functions-reference-node.md)
>
>

<span data-ttu-id="8013a-108">hello Azure WebJobs SDK 是以基礎 hello Azure 函式的 C# 指令碼體驗。</span><span class="sxs-lookup"><span data-stu-id="8013a-108">hello C# script experience for Azure Functions is based on hello Azure WebJobs SDK.</span></span> <span data-ttu-id="8013a-109">資料會透過方法引數流入您的 C# 函式。</span><span class="sxs-lookup"><span data-stu-id="8013a-109">Data flows into your C# function via method arguments.</span></span> <span data-ttu-id="8013a-110">中指定的引數名稱`function.json`，而且沒有預先定義的存取像是 hello 函式記錄器和取消語彙基元名稱。</span><span class="sxs-lookup"><span data-stu-id="8013a-110">Argument names are specified in `function.json`, and there are predefined names for accessing things like hello function logger and cancellation tokens.</span></span>

<span data-ttu-id="8013a-111">本文章假設，您已閱讀 hello [Azure 函式的開發人員參考](functions-reference.md)。</span><span class="sxs-lookup"><span data-stu-id="8013a-111">This article assumes that you've already read hello [Azure Functions developer reference](functions-reference.md).</span></span>

<span data-ttu-id="8013a-112">如需使用 C# 類別庫的詳細資訊，請參閱[使用 .NET 類別庫搭配 Azure Functions](functions-dotnet-class-library.md)。</span><span class="sxs-lookup"><span data-stu-id="8013a-112">For information on using C# class libraries, see [Using .NET class libraries with Azure Functions](functions-dotnet-class-library.md).</span></span>

## <a name="how-csx-works"></a><span data-ttu-id="8013a-113">.csx 的運作方式</span><span class="sxs-lookup"><span data-stu-id="8013a-113">How .csx works</span></span>
<span data-ttu-id="8013a-114">hello`.csx`格式可讓您 toowrite 小於 「 重複使用 」，並專注於撰寫只是 C# 函式。</span><span class="sxs-lookup"><span data-stu-id="8013a-114">hello `.csx` format allows you toowrite less "boilerplate" and focus on writing just a C# function.</span></span> <span data-ttu-id="8013a-115">像往常一樣包含任何組件參考和在 hello 檔案 hello 開頭的命名空間。</span><span class="sxs-lookup"><span data-stu-id="8013a-115">Include any assembly references and namespaces at hello beginning of hello file as usual.</span></span> <span data-ttu-id="8013a-116">只需定義 `Run` 方法，而不用在命名空間和類別中包裝所有項目。</span><span class="sxs-lookup"><span data-stu-id="8013a-116">Instead of wrapping everything in a namespace and class, just define a `Run` method.</span></span> <span data-ttu-id="8013a-117">如果您需要 tooinclude 任何類別，用於執行個體 toodefine 純舊 CLR 物件 (POCO) 物件，您可以包含內部的類別 hello 相同的檔案。</span><span class="sxs-lookup"><span data-stu-id="8013a-117">If you need tooinclude any classes, for instance toodefine Plain Old CLR Object (POCO) objects, you can include a class inside hello same file.</span></span>   

## <a name="binding-tooarguments"></a><span data-ttu-id="8013a-118">繫結 tooarguments</span><span class="sxs-lookup"><span data-stu-id="8013a-118">Binding tooarguments</span></span>
<span data-ttu-id="8013a-119">hello 各種繫結是繫結的 tooa C# 函式，透過 hello`name`屬性在 hello *function.json*組態。</span><span class="sxs-lookup"><span data-stu-id="8013a-119">hello various bindings are bound tooa C# function via hello `name` property in hello *function.json* configuration.</span></span> <span data-ttu-id="8013a-120">每個繫結都有自己支援的類型；例如，Blob 觸發程序可以支援字串、POCO 或 CloudBlockBlob。</span><span class="sxs-lookup"><span data-stu-id="8013a-120">Each binding has its own supported types; for instance, a blob trigger can support a string, a POCO, or a CloudBlockBlob.</span></span> <span data-ttu-id="8013a-121">hello 支援類型會記錄在每個繫結的 hello 參考。</span><span class="sxs-lookup"><span data-stu-id="8013a-121">hello supported types are documented in hello reference for each binding.</span></span> <span data-ttu-id="8013a-122">POCO 物件的每個屬性必須定義 getter 和 setter。</span><span class="sxs-lookup"><span data-stu-id="8013a-122">A POCO object must have a getter and setter defined for each property.</span></span>

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

## <a name="using-method-return-value-for-output-binding"></a><span data-ttu-id="8013a-123">使用輸出繫結的方法傳回值</span><span class="sxs-lookup"><span data-stu-id="8013a-123">Using method return value for output binding</span></span>

<span data-ttu-id="8013a-124">您可以使用方法的傳回值的輸出繫結使用 hello 名稱`$return`中*function.json*:</span><span class="sxs-lookup"><span data-stu-id="8013a-124">You can use a method return value for an output binding, by using hello name `$return` in *function.json*:</span></span>

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

## <a name="writing-multiple-output-values"></a><span data-ttu-id="8013a-125">撰寫多個輸出值</span><span class="sxs-lookup"><span data-stu-id="8013a-125">Writing multiple output values</span></span>

<span data-ttu-id="8013a-126">toowrite 多個值 tooan 輸出繫結，請使用 hello [ `ICollector` ](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/ICollector.cs)或[ `IAsyncCollector` ](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IAsyncCollector.cs)型別。</span><span class="sxs-lookup"><span data-stu-id="8013a-126">toowrite multiple values tooan output binding, use hello [`ICollector`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/ICollector.cs) or [`IAsyncCollector`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IAsyncCollector.cs) types.</span></span> <span data-ttu-id="8013a-127">這些類型是唯寫的集合寫入的 toohello 輸出繫結 hello 方法完成時。</span><span class="sxs-lookup"><span data-stu-id="8013a-127">These types are write-only collections that are written toohello output binding when hello method completes.</span></span>

<span data-ttu-id="8013a-128">這個範例會使用 `ICollector` 寫入多個佇列訊息：</span><span class="sxs-lookup"><span data-stu-id="8013a-128">This example writes multiple queue messages using `ICollector`:</span></span>

```csharp
public static void Run(ICollector<string> myQueueItem, TraceWriter log)
{
    myQueueItem.Add("Hello");
    myQueueItem.Add("World!");
}
```

## <a name="logging"></a><span data-ttu-id="8013a-129">記錄</span><span class="sxs-lookup"><span data-stu-id="8013a-129">Logging</span></span>
<span data-ttu-id="8013a-130">toolog 輸出 tooyour C# 中的資料流記錄，包含一個引數的型別`TraceWriter`。</span><span class="sxs-lookup"><span data-stu-id="8013a-130">toolog output tooyour streaming logs in C#, include an argument of type `TraceWriter`.</span></span> <span data-ttu-id="8013a-131">建議您將它命名為 `log`。</span><span class="sxs-lookup"><span data-stu-id="8013a-131">We recommend that you name it `log`.</span></span> <span data-ttu-id="8013a-132">避免在 Azure Functions 中使用 `Console.Write`。</span><span class="sxs-lookup"><span data-stu-id="8013a-132">Avoid using `Console.Write` in Azure Functions.</span></span> 

<span data-ttu-id="8013a-133">`TraceWriter`定義在 hello [Azure WebJobs SDK](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.Host/TraceWriter.cs)。</span><span class="sxs-lookup"><span data-stu-id="8013a-133">`TraceWriter` is defined in hello [Azure WebJobs SDK](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.Host/TraceWriter.cs).</span></span> <span data-ttu-id="8013a-134">hello 記錄層級`TraceWriter`可在設定[主機\.json]。</span><span class="sxs-lookup"><span data-stu-id="8013a-134">hello log level for `TraceWriter` can be configured in [host\.json].</span></span>

```csharp
public static void Run(string myBlob, TraceWriter log)
{
    log.Info($"C# Blob trigger function processed: {myBlob}");
}
```

## <a name="async"></a><span data-ttu-id="8013a-135">非同步處理</span><span class="sxs-lookup"><span data-stu-id="8013a-135">Async</span></span>
<span data-ttu-id="8013a-136">toomake 非同步函式使用 hello`async`關鍵字，並傳回`Task`物件。</span><span class="sxs-lookup"><span data-stu-id="8013a-136">toomake a function asynchronous, use hello `async` keyword and return a `Task` object.</span></span>

```csharp
public async static Task ProcessQueueMessageAsync(
        string blobName,
        Stream blobInput,
        Stream blobOutput)
{
    await blobInput.CopyToAsync(blobOutput, 4096, token);
}
```

## <a name="cancellation-token"></a><span data-ttu-id="8013a-137">取消權杖</span><span class="sxs-lookup"><span data-stu-id="8013a-137">Cancellation Token</span></span>
<span data-ttu-id="8013a-138">某些作業需要正常關機。</span><span class="sxs-lookup"><span data-stu-id="8013a-138">Some operations require graceful shutdown.</span></span> <span data-ttu-id="8013a-139">它一律是損毀，萬一您想要 toohandle 正常關機的要求，可以處理的最佳 toowrite 代碼定義[ `CancellationToken` ](https://msdn.microsoft.com/library/system.threading.cancellationtoken.aspx)型別引數。</span><span class="sxs-lookup"><span data-stu-id="8013a-139">While it's always best toowrite code that can handle crashing,  in cases where you want toohandle graceful shutdown requests, you define a [`CancellationToken`](https://msdn.microsoft.com/library/system.threading.cancellationtoken.aspx) typed argument.</span></span>  <span data-ttu-id="8013a-140">A`CancellationToken`提供 toosignal 主機關機時觸發。</span><span class="sxs-lookup"><span data-stu-id="8013a-140">A `CancellationToken` is provided toosignal that a host shutdown is triggered.</span></span>

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

## <a name="importing-namespaces"></a><span data-ttu-id="8013a-141">匯入命名空間</span><span class="sxs-lookup"><span data-stu-id="8013a-141">Importing namespaces</span></span>
<span data-ttu-id="8013a-142">如果您需要 tooimport 命名空間，您可以像往常一樣，以 hello`using`子句。</span><span class="sxs-lookup"><span data-stu-id="8013a-142">If you need tooimport namespaces, you can do so as usual, with hello `using` clause.</span></span>

```csharp
using System.Net;
using System.Threading.Tasks;

public static Task<HttpResponseMessage> Run(HttpRequestMessage req, TraceWriter log)
```

<span data-ttu-id="8013a-143">hello 下列命名空間會自動匯入，因此選擇性：</span><span class="sxs-lookup"><span data-stu-id="8013a-143">hello following namespaces are automatically imported and are therefore optional:</span></span>

* `System`
* `System.Collections.Generic`
* `System.IO`
* `System.Linq`
* `System.Net.Http`
* `System.Threading.Tasks`
* `Microsoft.Azure.WebJobs`
* `Microsoft.Azure.WebJobs.Host`

## <a name="referencing-external-assemblies"></a><span data-ttu-id="8013a-144">參考外部組件</span><span class="sxs-lookup"><span data-stu-id="8013a-144">Referencing External Assemblies</span></span>
<span data-ttu-id="8013a-145">針對 framework 組件，請將參考加入使用 hello`#r "AssemblyName"`指示詞。</span><span class="sxs-lookup"><span data-stu-id="8013a-145">For framework assemblies, add references by using hello `#r "AssemblyName"` directive.</span></span>

```csharp
#r "System.Web.Http"

using System.Net;
using System.Net.Http;
using System.Threading.Tasks;

public static Task<HttpResponseMessage> Run(HttpRequestMessage req, TraceWriter log)
```

<span data-ttu-id="8013a-146">hello 下列組件會自動加入裝載環境的 hello Azure 函式：</span><span class="sxs-lookup"><span data-stu-id="8013a-146">hello following assemblies are automatically added by hello Azure Functions hosting environment:</span></span>

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

<span data-ttu-id="8013a-147">hello 參考下列組件可能是由簡單名稱 (例如， `#r "AssemblyName"`):</span><span class="sxs-lookup"><span data-stu-id="8013a-147">hello following assemblies may be referenced by simple-name (for example, `#r "AssemblyName"`):</span></span>

* `Newtonsoft.Json`
* `Microsoft.WindowsAzure.Storage`
* `Microsoft.ServiceBus`
* `Microsoft.AspNet.WebHooks.Receivers`
* `Microsoft.AspNet.WebHooks.Common`
* `Microsoft.Azure.NotificationHubs`

## <a name="referencing-custom-assemblies"></a><span data-ttu-id="8013a-148">參考自訂組件</span><span class="sxs-lookup"><span data-stu-id="8013a-148">Referencing custom assemblies</span></span>

<span data-ttu-id="8013a-149">tooreference 自訂組件，您可以使用*共用*組件或*私人*組件：</span><span class="sxs-lookup"><span data-stu-id="8013a-149">tooreference a custom assembly, you can use either a *shared* assembly or a *private* assembly:</span></span>
- <span data-ttu-id="8013a-150">共用組件會共用於函式應用程式內的所有函式。</span><span class="sxs-lookup"><span data-stu-id="8013a-150">Shared assemblies are shared across all functions within a function app.</span></span> <span data-ttu-id="8013a-151">tooreference 自訂組件上, 傳 hello 組件 tooyour 函式應用程式，例如`bin`hello 函式應用程式根目錄中的資料夾。</span><span class="sxs-lookup"><span data-stu-id="8013a-151">tooreference a custom assembly, upload hello assembly tooyour function app, such as in a `bin` folder in hello function app root.</span></span> 
- <span data-ttu-id="8013a-152">私人組件屬於所指定函式的內容，而且支援不同版本的側載。</span><span class="sxs-lookup"><span data-stu-id="8013a-152">Private assemblies are part of a given function's context, and support side-loading of different versions.</span></span> <span data-ttu-id="8013a-153">應該在私用組件上傳`bin`hello 函式的目錄資料夾中。</span><span class="sxs-lookup"><span data-stu-id="8013a-153">Private assemblies should be uploaded in a `bin` folder in hello function directory.</span></span> <span data-ttu-id="8013a-154">參考使用 hello 檔案名稱，例如`#r "MyAssembly.dll"`。</span><span class="sxs-lookup"><span data-stu-id="8013a-154">Reference using hello file name, such as  `#r "MyAssembly.dll"`.</span></span> 

<span data-ttu-id="8013a-155">上如何 tooupload 檔案 tooyour 函數資料夾的資訊，請參閱 hello 下列封裝管理上的一節。</span><span class="sxs-lookup"><span data-stu-id="8013a-155">For information on how tooupload files tooyour function folder, see hello following section on package management.</span></span>

### <a name="watched-directories"></a><span data-ttu-id="8013a-156">監看的目錄</span><span class="sxs-lookup"><span data-stu-id="8013a-156">Watched directories</span></span>

<span data-ttu-id="8013a-157">變更 tooassemblies 自動監看 hello 目錄，包含 hello 函式的指令碼檔案。</span><span class="sxs-lookup"><span data-stu-id="8013a-157">hello directory that contains hello function script file is automatically watched for changes tooassemblies.</span></span> <span data-ttu-id="8013a-158">toowatch 組件中的變更其他目錄，將它們加入 toohello`watchDirectories`清單中[主機\.json]。</span><span class="sxs-lookup"><span data-stu-id="8013a-158">toowatch for assembly changes in other directories, add them toohello `watchDirectories` list in [host\.json].</span></span>

## <a name="using-nuget-packages"></a><span data-ttu-id="8013a-159">使用 NuGet 套件</span><span class="sxs-lookup"><span data-stu-id="8013a-159">Using NuGet packages</span></span>
<span data-ttu-id="8013a-160">在 C# 函式，toouse NuGet 封裝上傳*project.json* hello 函式應用程式的檔案系統中檔案 toohello 函式的資料夾。</span><span class="sxs-lookup"><span data-stu-id="8013a-160">toouse NuGet packages in a C# function, upload a *project.json* file toohello function's folder in hello function app's file system.</span></span> <span data-ttu-id="8013a-161">以下是範例*project.json*會新增參考 tooMicrosoft.ProjectOxford.Face 版本 1.1.0 的檔案：</span><span class="sxs-lookup"><span data-stu-id="8013a-161">Here is an example *project.json* file that adds a reference tooMicrosoft.ProjectOxford.Face version 1.1.0:</span></span>

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

<span data-ttu-id="8013a-162">只有 hello.NET Framework 4.6 支援，因此請確定您*project.json*檔案會指定`net46`如下所示。</span><span class="sxs-lookup"><span data-stu-id="8013a-162">Only hello .NET Framework 4.6 is supported, so make sure that your *project.json* file specifies `net46` as shown here.</span></span>

<span data-ttu-id="8013a-163">當您上傳*project.json*檔案中，hello 執行階段取得 hello 封裝，並會自動將參考 toohello 封裝組件。</span><span class="sxs-lookup"><span data-stu-id="8013a-163">When you upload a *project.json* file, hello runtime gets hello packages and automatically adds references toohello package assemblies.</span></span> <span data-ttu-id="8013a-164">您不需要 tooadd`#r "AssemblyName"`指示詞。</span><span class="sxs-lookup"><span data-stu-id="8013a-164">You don't need tooadd `#r "AssemblyName"` directives.</span></span> <span data-ttu-id="8013a-165">hello 的 NuGet 封裝中定義的 toouse hello 型別新增所需的 hello`using`陳述式 tooyour *run.csx*檔案</span><span class="sxs-lookup"><span data-stu-id="8013a-165">toouse hello types defined in hello NuGet packages, add hello required `using` statements tooyour *run.csx* file</span></span> 

<span data-ttu-id="8013a-166">在 hello 函式的執行階段，NuGet 還原的運作方式是比較`project.json`和`project.lock.json`。</span><span class="sxs-lookup"><span data-stu-id="8013a-166">In hello Functions runtime, NuGet restore works by comparing `project.json` and `project.lock.json`.</span></span> <span data-ttu-id="8013a-167">如果 hello hello 檔案的日期和時間戳記**不**相符項目，NuGet 還原執行並 NuGet 下載已更新的封裝。</span><span class="sxs-lookup"><span data-stu-id="8013a-167">If hello date and time stamps of hello files **do not** match, a NuGet restore runs and NuGet downloads updated packages.</span></span> <span data-ttu-id="8013a-168">不過，如果 hello hello 檔案的日期和時間戳記**不要**NuGet 相符項目，不會執行還原。</span><span class="sxs-lookup"><span data-stu-id="8013a-168">However, if hello date and time stamps of hello files **do** match, NuGet does not perform a restore.</span></span> <span data-ttu-id="8013a-169">因此，`project.lock.json`不應部署因為它會導致 NuGet tooskip 封裝還原。</span><span class="sxs-lookup"><span data-stu-id="8013a-169">Therefore, `project.lock.json` should not be deployed as it causes NuGet tooskip package restore.</span></span> <span data-ttu-id="8013a-170">部署 hello 鎖定 tooavoid file、 add hello `project.lock.json` toohello`.gitignore`檔案。</span><span class="sxs-lookup"><span data-stu-id="8013a-170">tooavoid deploying hello lock file, add hello `project.lock.json` toohello `.gitignore` file.</span></span>

<span data-ttu-id="8013a-171">toouse 自訂 NuGet 摘要中，指定摘要中的 hello *Nuget.Config* hello 函式應用程式根目錄中的檔案。</span><span class="sxs-lookup"><span data-stu-id="8013a-171">toouse a custom NuGet feed, specify hello feed in a *Nuget.Config* file in hello Function App root.</span></span> <span data-ttu-id="8013a-172">如需詳細資訊，請參閱[設定 NuGet 行為](/nuget/consume-packages/configuring-nuget-behavior)。</span><span class="sxs-lookup"><span data-stu-id="8013a-172">For more information, see [Configuring NuGet behavior](/nuget/consume-packages/configuring-nuget-behavior).</span></span>

### <a name="using-a-projectjson-file"></a><span data-ttu-id="8013a-173">使用 project.json 檔案</span><span class="sxs-lookup"><span data-stu-id="8013a-173">Using a project.json file</span></span>
1. <span data-ttu-id="8013a-174">開啟 hello Azure 入口網站中的 hello 函式。</span><span class="sxs-lookup"><span data-stu-id="8013a-174">Open hello function in hello Azure portal.</span></span> <span data-ttu-id="8013a-175">hello 記錄 索引標籤會顯示 hello 封裝安裝輸出。</span><span class="sxs-lookup"><span data-stu-id="8013a-175">hello logs tab displays hello package installation output.</span></span>
2. <span data-ttu-id="8013a-176">tooupload project.json 檔案中，使用其中一種 hello 中所述的 hello 方法[tooupdate 運作應用程式檔案的方式](functions-reference.md#fileupdate)hello Azure 函式開發人員參考主題。</span><span class="sxs-lookup"><span data-stu-id="8013a-176">tooupload a project.json file, use one of hello methods described in hello [How tooupdate function app files](functions-reference.md#fileupdate) in hello Azure Functions developer reference topic.</span></span>
3. <span data-ttu-id="8013a-177">之後 hello *project.json*上傳檔案時，您會看到類似下列範例函式中的 hello 輸出的資料流記錄：</span><span class="sxs-lookup"><span data-stu-id="8013a-177">After hello *project.json* file is uploaded, you see output like hello following example in your function's streaming log:</span></span>

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

## <a name="environment-variables"></a><span data-ttu-id="8013a-178">環境變數</span><span class="sxs-lookup"><span data-stu-id="8013a-178">Environment variables</span></span>
<span data-ttu-id="8013a-179">tooget 環境變數或應用程式設定值，使用`System.Environment.GetEnvironmentVariable`hello 下列程式碼範例所示：</span><span class="sxs-lookup"><span data-stu-id="8013a-179">tooget an environment variable or an app setting value, use `System.Environment.GetEnvironmentVariable`, as shown in hello following code example:</span></span>

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

## <a name="reusing-csx-code"></a><span data-ttu-id="8013a-180">重複使用 .csx 程式碼</span><span class="sxs-lookup"><span data-stu-id="8013a-180">Reusing .csx code</span></span>
<span data-ttu-id="8013a-181">您可以在您的 *run.csx* 檔案中使用其他 *.csx* 檔案中定義的類別和方法。</span><span class="sxs-lookup"><span data-stu-id="8013a-181">You can use classes and methods defined in other *.csx* files in your *run.csx* file.</span></span> <span data-ttu-id="8013a-182">可使用 toodo`#load`指示詞中的您*run.csx*檔案。</span><span class="sxs-lookup"><span data-stu-id="8013a-182">toodo that, use `#load` directives in your *run.csx* file.</span></span> <span data-ttu-id="8013a-183">在下列範例的 hello，記錄常式命名為`MyLogger`中共用*myLogger.csx*並載入*run.csx*使用 hello`#load`指示詞：</span><span class="sxs-lookup"><span data-stu-id="8013a-183">In hello following example, a logging routine named `MyLogger` is shared in *myLogger.csx* and loaded into *run.csx* using hello `#load` directive:</span></span>

<span data-ttu-id="8013a-184">範例 run.csx ：</span><span class="sxs-lookup"><span data-stu-id="8013a-184">Example *run.csx*:</span></span>

```csharp
#load "mylogger.csx"

public static void Run(TimerInfo myTimer, TraceWriter log)
{
    log.Verbose($"Log by run.csx: {DateTime.Now}");
    MyLogger(log, $"Log by MyLogger: {DateTime.Now}");
}
```

<span data-ttu-id="8013a-185">範例 mylogger.csx ：</span><span class="sxs-lookup"><span data-stu-id="8013a-185">Example *mylogger.csx*:</span></span>

```csharp
public static void MyLogger(TraceWriter log, string logtext)
{
    log.Verbose(logtext);
}
```

<span data-ttu-id="8013a-186">使用共用*.csx*是常見的模式，當您想 toostrongly 時輸入您使用 POCO 物件的函式之間的引數。</span><span class="sxs-lookup"><span data-stu-id="8013a-186">Using a shared *.csx* is a common pattern when you want toostrongly type your arguments between functions using a POCO object.</span></span> <span data-ttu-id="8013a-187">Hello 下列簡化的範例，在 HTTP 觸發程序和佇列觸發程序共用名為 POCO 物件`Order`toostrongly 類型 hello 訂單資料：</span><span class="sxs-lookup"><span data-stu-id="8013a-187">In hello following simplified example, an HTTP trigger and queue trigger share a POCO object named `Order` toostrongly type hello order data:</span></span>

<span data-ttu-id="8013a-188">HTTP 觸發程序的範例 *run.csx*︰</span><span class="sxs-lookup"><span data-stu-id="8013a-188">Example *run.csx* for HTTP trigger:</span></span>

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

<span data-ttu-id="8013a-189">佇列觸發程序的範例 *run.csx*︰</span><span class="sxs-lookup"><span data-stu-id="8013a-189">Example *run.csx* for queue trigger:</span></span>

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

<span data-ttu-id="8013a-190">範例 *order.csx*：</span><span class="sxs-lookup"><span data-stu-id="8013a-190">Example *order.csx*:</span></span>

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

<span data-ttu-id="8013a-191">您可以使用相對路徑，以 hello`#load`指示詞：</span><span class="sxs-lookup"><span data-stu-id="8013a-191">You can use a relative path with hello `#load` directive:</span></span>

* <span data-ttu-id="8013a-192">`#load "mylogger.csx"`載入檔案，位於 hello 函式資料夾。</span><span class="sxs-lookup"><span data-stu-id="8013a-192">`#load "mylogger.csx"` loads a file located in hello function folder.</span></span>
* <span data-ttu-id="8013a-193">`#load "loadedfiles\mylogger.csx"`載入檔案，位於 hello 函式資料夾中的資料夾。</span><span class="sxs-lookup"><span data-stu-id="8013a-193">`#load "loadedfiles\mylogger.csx"` loads a file located in a folder in hello function folder.</span></span>
* <span data-ttu-id="8013a-194">`#load "..\shared\mylogger.csx"`載入位於的 hello 相同層級為 hello 函式的資料夾，也就是在資料夾中的檔案直接在*wwwroot*。</span><span class="sxs-lookup"><span data-stu-id="8013a-194">`#load "..\shared\mylogger.csx"` loads a file located in a folder at hello same level as hello function folder, that is, directly under *wwwroot*.</span></span>

<span data-ttu-id="8013a-195">hello`#load`指示詞只適用於*.csx* （C# 指令碼） 檔案，不能搭配*.cs*檔案。</span><span class="sxs-lookup"><span data-stu-id="8013a-195">hello `#load` directive works only with *.csx* (C# script) files, not with *.cs* files.</span></span>

<a name="imperative-bindings"></a> 

## <a name="binding-at-runtime-via-imperative-bindings"></a><span data-ttu-id="8013a-196">透過命令式繫結在執行階段繫結</span><span class="sxs-lookup"><span data-stu-id="8013a-196">Binding at runtime via imperative bindings</span></span>

<span data-ttu-id="8013a-197">在 C# 和其他.NET 語言，您可以使用[命令式](https://en.wikipedia.org/wiki/Imperative_programming)繫結模式，但不要 toohello [*宣告式*](https://en.wikipedia.org/wiki/Declarative_programming)中的繫結*function.json*.</span><span class="sxs-lookup"><span data-stu-id="8013a-197">In C# and other .NET languages, you can use an [imperative](https://en.wikipedia.org/wiki/Imperative_programming) binding pattern, as opposed toohello [*declarative*](https://en.wikipedia.org/wiki/Declarative_programming) bindings in *function.json*.</span></span> <span data-ttu-id="8013a-198">命令式的繫結時，必須在執行階段，而不是設計階段計算 toobe 繫結參數。</span><span class="sxs-lookup"><span data-stu-id="8013a-198">Imperative binding is useful when binding parameters need toobe computed at runtime rather than design time.</span></span> <span data-ttu-id="8013a-199">此模式中，您可以繫結 toosupported 輸入，並輸出函式程式碼中的繫結上作業。</span><span class="sxs-lookup"><span data-stu-id="8013a-199">With this pattern, you can bind toosupported input and output binding on-the-fly in your function code.</span></span>

<span data-ttu-id="8013a-200">定義命令式繫結，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="8013a-200">Define an imperative binding as follows:</span></span>

- <span data-ttu-id="8013a-201">**請勿**在 *function.json* 中為您所需的命令式繫結併入項目。</span><span class="sxs-lookup"><span data-stu-id="8013a-201">**Do not** include an entry in *function.json* for your desired imperative bindings.</span></span>
- <span data-ttu-id="8013a-202">傳入輸入參數 [`Binder binder`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.Host/Bindings/Runtime/Binder.cs) 或 [`IBinder binder`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IBinder.cs)。</span><span class="sxs-lookup"><span data-stu-id="8013a-202">Pass in an input parameter [`Binder binder`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.Host/Bindings/Runtime/Binder.cs) or [`IBinder binder`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IBinder.cs).</span></span>
- <span data-ttu-id="8013a-203">使用下列 C# 模式 tooperform hello 資料繫結的 hello。</span><span class="sxs-lookup"><span data-stu-id="8013a-203">Use hello following C# pattern tooperform hello data binding.</span></span>

```cs
using (var output = await binder.BindAsync<T>(new BindingTypeAttribute(...)))
{
    ...
}
```

<span data-ttu-id="8013a-204">其中`BindingTypeAttribute`hello.NET 屬性可定義您的繫結和`T`是 hello 該繫結類型所支援的輸入或輸出類型。</span><span class="sxs-lookup"><span data-stu-id="8013a-204">where `BindingTypeAttribute` is hello .NET attribute that defines your binding and `T` is hello input or output type that's supported by that binding type.</span></span> <span data-ttu-id="8013a-205">`T` 也不能是 `out` 參數類型 (例如 `out JObject`)。</span><span class="sxs-lookup"><span data-stu-id="8013a-205">`T` also cannot be an `out` parameter type (such as `out JObject`).</span></span> <span data-ttu-id="8013a-206">例如，Mobile Apps 資料表輸出繫結支援[六個輸出類型](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.MobileApps/MobileTableAttribute.cs#L17-L22)，但您只可以對 `T` 使用 [ICollector<T>](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/ICollector.cs) 或 [IAsyncCollector<T>](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IAsyncCollector.cs)。</span><span class="sxs-lookup"><span data-stu-id="8013a-206">For example, the Mobile Apps table output binding supports [six output types](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.MobileApps/MobileTableAttribute.cs#L17-L22), but you can only use [ICollector<T>](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/ICollector.cs) or [IAsyncCollector<T>](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IAsyncCollector.cs) for `T`.</span></span>

<span data-ttu-id="8013a-207">下列範例程式碼的 hello 建立[儲存體 blob 輸出繫結](functions-bindings-storage-blob.md#using-a-blob-output-binding)與 blob 路徑，定義在執行階段，然後字串 toohello 將 blob 寫入。</span><span class="sxs-lookup"><span data-stu-id="8013a-207">hello following example code creates a [Storage blob output binding](functions-bindings-storage-blob.md#using-a-blob-output-binding) with blob path that's defined at run time, then writes a string toohello blob.</span></span>

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

<span data-ttu-id="8013a-208">[BlobAttribute](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/BlobAttribute.cs)定義 hello[儲存體 blob](functions-bindings-storage-blob.md)輸入或輸出繫結，以及[TextWriter](https://msdn.microsoft.com/library/system.io.textwriter.aspx)是支援的輸出繫結型別。</span><span class="sxs-lookup"><span data-stu-id="8013a-208">[BlobAttribute](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/BlobAttribute.cs) defines hello [Storage blob](functions-bindings-storage-blob.md) input or output binding, and [TextWriter](https://msdn.microsoft.com/library/system.io.textwriter.aspx) is a supported output binding type.</span></span>
<span data-ttu-id="8013a-209">Hello 程式碼，取得儲存體帳戶連接字串 hello hello 預設應用程式設定 (也就是`AzureWebJobsStorage`)。</span><span class="sxs-lookup"><span data-stu-id="8013a-209">As is, hello code gets hello default app setting for hello Storage account connection string (which is `AzureWebJobsStorage`).</span></span> <span data-ttu-id="8013a-210">您可以加入，以指定自訂應用程式設定 toouse [StorageAccountAttribute](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs)並傳遞到 hello 屬性陣列`BindAsync<T>()`。</span><span class="sxs-lookup"><span data-stu-id="8013a-210">You can specify a custom app setting toouse by adding the [StorageAccountAttribute](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs) and passing hello attribute array into `BindAsync<T>()`.</span></span> <span data-ttu-id="8013a-211">例如，</span><span class="sxs-lookup"><span data-stu-id="8013a-211">For example,</span></span>

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

<span data-ttu-id="8013a-212">hello 下表列出針對其定義每個繫結型別和 hello 封裝 hello.NET 屬性。</span><span class="sxs-lookup"><span data-stu-id="8013a-212">hello following table lists hello .NET attributes for each binding type and hello packages in which they are defined.</span></span>

> [!div class="mx-codeBreakAll"]
| <span data-ttu-id="8013a-213">繫結</span><span class="sxs-lookup"><span data-stu-id="8013a-213">Binding</span></span> | <span data-ttu-id="8013a-214">屬性</span><span class="sxs-lookup"><span data-stu-id="8013a-214">Attribute</span></span> | <span data-ttu-id="8013a-215">新增參考</span><span class="sxs-lookup"><span data-stu-id="8013a-215">Add reference</span></span> |
|------|------|------|
| <span data-ttu-id="8013a-216">Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="8013a-216">Cosmos DB</span></span> | [`Microsoft.Azure.WebJobs.DocumentDBAttribute`](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.DocumentDB/DocumentDBAttribute.cs) | `#r "Microsoft.Azure.WebJobs.Extensions.DocumentDB"` |
| <span data-ttu-id="8013a-217">事件中樞</span><span class="sxs-lookup"><span data-stu-id="8013a-217">Event Hubs</span></span> | <span data-ttu-id="8013a-218">[`Microsoft.Azure.WebJobs.ServiceBus.EventHubAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/EventHubs/EventHubAttribute.cs), [`Microsoft.Azure.WebJobs.ServiceBusAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAccountAttribute.cs)</span><span class="sxs-lookup"><span data-stu-id="8013a-218">[`Microsoft.Azure.WebJobs.ServiceBus.EventHubAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/EventHubs/EventHubAttribute.cs), [`Microsoft.Azure.WebJobs.ServiceBusAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAccountAttribute.cs)</span></span> | `#r "Microsoft.Azure.Jobs.ServiceBus"` |
| <span data-ttu-id="8013a-219">行動應用程式</span><span class="sxs-lookup"><span data-stu-id="8013a-219">Mobile Apps</span></span> | [`Microsoft.Azure.WebJobs.MobileTableAttribute`](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.MobileApps/MobileTableAttribute.cs) | `#r "Microsoft.Azure.WebJobs.Extensions.MobileApps"` |
| <span data-ttu-id="8013a-220">通知中樞</span><span class="sxs-lookup"><span data-stu-id="8013a-220">Notification Hubs</span></span> | [`Microsoft.Azure.WebJobs.NotificationHubAttribute`](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.NotificationHubs/NotificationHubAttribute.cs) | `#r "Microsoft.Azure.WebJobs.Extensions.NotificationHubs"` |
| <span data-ttu-id="8013a-221">服務匯流排</span><span class="sxs-lookup"><span data-stu-id="8013a-221">Service Bus</span></span> | <span data-ttu-id="8013a-222">[`Microsoft.Azure.WebJobs.ServiceBusAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAttribute.cs), [`Microsoft.Azure.WebJobs.ServiceBusAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAccountAttribute.cs)</span><span class="sxs-lookup"><span data-stu-id="8013a-222">[`Microsoft.Azure.WebJobs.ServiceBusAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAttribute.cs), [`Microsoft.Azure.WebJobs.ServiceBusAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAccountAttribute.cs)</span></span> | `#r "Microsoft.Azure.WebJobs.ServiceBus"` |
| <span data-ttu-id="8013a-223">儲存體佇列</span><span class="sxs-lookup"><span data-stu-id="8013a-223">Storage queue</span></span> | <span data-ttu-id="8013a-224">[`Microsoft.Azure.WebJobs.QueueAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/QueueAttribute.cs), [`Microsoft.Azure.WebJobs.StorageAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs)</span><span class="sxs-lookup"><span data-stu-id="8013a-224">[`Microsoft.Azure.WebJobs.QueueAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/QueueAttribute.cs), [`Microsoft.Azure.WebJobs.StorageAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs)</span></span> | |
| <span data-ttu-id="8013a-225">儲存體 Blob</span><span class="sxs-lookup"><span data-stu-id="8013a-225">Storage blob</span></span> | <span data-ttu-id="8013a-226">[`Microsoft.Azure.WebJobs.BlobAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/BlobAttribute.cs), [`Microsoft.Azure.WebJobs.StorageAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs)</span><span class="sxs-lookup"><span data-stu-id="8013a-226">[`Microsoft.Azure.WebJobs.BlobAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/BlobAttribute.cs), [`Microsoft.Azure.WebJobs.StorageAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs)</span></span> | |
| <span data-ttu-id="8013a-227">儲存體資料表</span><span class="sxs-lookup"><span data-stu-id="8013a-227">Storage table</span></span> | <span data-ttu-id="8013a-228">[`Microsoft.Azure.WebJobs.TableAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/TableAttribute.cs), [`Microsoft.Azure.WebJobs.StorageAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs)</span><span class="sxs-lookup"><span data-stu-id="8013a-228">[`Microsoft.Azure.WebJobs.TableAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/TableAttribute.cs), [`Microsoft.Azure.WebJobs.StorageAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs)</span></span> | |
| <span data-ttu-id="8013a-229">Twilio</span><span class="sxs-lookup"><span data-stu-id="8013a-229">Twilio</span></span> | [`Microsoft.Azure.WebJobs.TwilioSmsAttribute`](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.Twilio/TwilioSMSAttribute.cs) | `#r "Microsoft.Azure.WebJobs.Extensions.Twilio"` |



## <a name="next-steps"></a><span data-ttu-id="8013a-230">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8013a-230">Next steps</span></span>
<span data-ttu-id="8013a-231">如需詳細資訊，請參閱下列資源的 hello:</span><span class="sxs-lookup"><span data-stu-id="8013a-231">For more information, see hello following resources:</span></span>

* [<span data-ttu-id="8013a-232">Azure Functions 的最佳作法</span><span class="sxs-lookup"><span data-stu-id="8013a-232">Best Practices for Azure Functions</span></span>](functions-best-practices.md)
* [<span data-ttu-id="8013a-233">Azure Functions 開發人員參考</span><span class="sxs-lookup"><span data-stu-id="8013a-233">Azure Functions developer reference</span></span>](functions-reference.md)
* [<span data-ttu-id="8013a-234">Azure Functions F# 開發人員參考</span><span class="sxs-lookup"><span data-stu-id="8013a-234">Azure Functions F# developer reference</span></span>](functions-reference-fsharp.md)
* [<span data-ttu-id="8013a-235">Azure Functions NodeJS 開發人員參考</span><span class="sxs-lookup"><span data-stu-id="8013a-235">Azure Functions NodeJS developer reference</span></span>](functions-reference-node.md)
* [<span data-ttu-id="8013a-236">Azure Functions 觸發程序和繫結</span><span class="sxs-lookup"><span data-stu-id="8013a-236">Azure Functions triggers and bindings</span></span>](functions-triggers-bindings.md)

[host\.json]: https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json
