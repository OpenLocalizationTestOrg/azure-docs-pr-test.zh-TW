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
# <a name="azure-functions-c-script-developer-reference"></a><span data-ttu-id="babcd-104">Azure Functions C# 指令碼開發人員參考</span><span class="sxs-lookup"><span data-stu-id="babcd-104">Azure Functions C# script developer reference</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="babcd-105">C# 指令碼</span><span class="sxs-lookup"><span data-stu-id="babcd-105">C# script</span></span>](functions-reference-csharp.md)
> * [<span data-ttu-id="babcd-106">F# 指令碼</span><span class="sxs-lookup"><span data-stu-id="babcd-106">F# script</span></span>](functions-reference-fsharp.md)
> * [<span data-ttu-id="babcd-107">Node.js</span><span class="sxs-lookup"><span data-stu-id="babcd-107">Node.js</span></span>](functions-reference-node.md)
>
>

<span data-ttu-id="babcd-108">Azure Functions 的 C# 指令碼體驗是以 Azure WebJobs SDK 為基礎。</span><span class="sxs-lookup"><span data-stu-id="babcd-108">The C# script experience for Azure Functions is based on the Azure WebJobs SDK.</span></span> <span data-ttu-id="babcd-109">資料會透過方法引數流入您的 C# 函式。</span><span class="sxs-lookup"><span data-stu-id="babcd-109">Data flows into your C# function via method arguments.</span></span> <span data-ttu-id="babcd-110">引數名稱會指定於 `function.json`中，而且有預先定義的名稱可用來存取函式記錄器和取消權杖等項目。</span><span class="sxs-lookup"><span data-stu-id="babcd-110">Argument names are specified in `function.json`, and there are predefined names for accessing things like the function logger and cancellation tokens.</span></span>

<span data-ttu-id="babcd-111">本文假設您已經讀過 [Azure Functions 開發人員參考](functions-reference.md)。</span><span class="sxs-lookup"><span data-stu-id="babcd-111">This article assumes that you've already read the [Azure Functions developer reference](functions-reference.md).</span></span>

<span data-ttu-id="babcd-112">如需使用 C# 類別庫的詳細資訊，請參閱[使用 .NET 類別庫搭配 Azure Functions](functions-dotnet-class-library.md)。</span><span class="sxs-lookup"><span data-stu-id="babcd-112">For information on using C# class libraries, see [Using .NET class libraries with Azure Functions](functions-dotnet-class-library.md).</span></span>

## <a name="how-csx-works"></a><span data-ttu-id="babcd-113">.csx 的運作方式</span><span class="sxs-lookup"><span data-stu-id="babcd-113">How .csx works</span></span>
<span data-ttu-id="babcd-114">`.csx` 格式允許撰寫較少「重複使用」文字，只專注於撰寫 C# 函式。</span><span class="sxs-lookup"><span data-stu-id="babcd-114">The `.csx` format allows you to write less "boilerplate" and focus on writing just a C# function.</span></span> <span data-ttu-id="babcd-115">像往常一樣，在檔案開頭包含任何組件參考和命名空間。</span><span class="sxs-lookup"><span data-stu-id="babcd-115">Include any assembly references and namespaces at the beginning of the file as usual.</span></span> <span data-ttu-id="babcd-116">只需定義 `Run` 方法，而不用在命名空間和類別中包裝所有項目。</span><span class="sxs-lookup"><span data-stu-id="babcd-116">Instead of wrapping everything in a namespace and class, just define a `Run` method.</span></span> <span data-ttu-id="babcd-117">如果您需要包含任何類別，例如若要定義純舊 CLR 物件 (POCO) 物件，您可以包含相同檔案內的類別。</span><span class="sxs-lookup"><span data-stu-id="babcd-117">If you need to include any classes, for instance to define Plain Old CLR Object (POCO) objects, you can include a class inside the same file.</span></span>   

## <a name="binding-to-arguments"></a><span data-ttu-id="babcd-118">繫結至引數</span><span class="sxs-lookup"><span data-stu-id="babcd-118">Binding to arguments</span></span>
<span data-ttu-id="babcd-119">各種繫結會透過 *function.json* 組態中的 `name` 屬性繫結至 C# 函式。</span><span class="sxs-lookup"><span data-stu-id="babcd-119">The various bindings are bound to a C# function via the `name` property in the *function.json* configuration.</span></span> <span data-ttu-id="babcd-120">每個繫結都有自己支援的類型；例如，Blob 觸發程序可以支援字串、POCO 或 CloudBlockBlob。</span><span class="sxs-lookup"><span data-stu-id="babcd-120">Each binding has its own supported types; for instance, a blob trigger can support a string, a POCO, or a CloudBlockBlob.</span></span> <span data-ttu-id="babcd-121">支援的類型會記錄在每個繫結的參考中。</span><span class="sxs-lookup"><span data-stu-id="babcd-121">The supported types are documented in the reference for each binding.</span></span> <span data-ttu-id="babcd-122">POCO 物件的每個屬性必須定義 getter 和 setter。</span><span class="sxs-lookup"><span data-stu-id="babcd-122">A POCO object must have a getter and setter defined for each property.</span></span>

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

## <a name="using-method-return-value-for-output-binding"></a><span data-ttu-id="babcd-123">使用輸出繫結的方法傳回值</span><span class="sxs-lookup"><span data-stu-id="babcd-123">Using method return value for output binding</span></span>

<span data-ttu-id="babcd-124">您可以使用 function.json 中的名稱 `$return`，使用輸出繫結的方法傳回值：</span><span class="sxs-lookup"><span data-stu-id="babcd-124">You can use a method return value for an output binding, by using the name `$return` in *function.json*:</span></span>

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

## <a name="writing-multiple-output-values"></a><span data-ttu-id="babcd-125">撰寫多個輸出值</span><span class="sxs-lookup"><span data-stu-id="babcd-125">Writing multiple output values</span></span>

<span data-ttu-id="babcd-126">若要多個值寫入至輸出繫結，請使用 [`ICollector`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/ICollector.cs) 或 [`IAsyncCollector`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IAsyncCollector.cs) 類型。</span><span class="sxs-lookup"><span data-stu-id="babcd-126">To write multiple values to an output binding, use the [`ICollector`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/ICollector.cs) or [`IAsyncCollector`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IAsyncCollector.cs) types.</span></span> <span data-ttu-id="babcd-127">這些類型是在方法完成時，寫入至輸出繫結的唯寫集合。</span><span class="sxs-lookup"><span data-stu-id="babcd-127">These types are write-only collections that are written to the output binding when the method completes.</span></span>

<span data-ttu-id="babcd-128">這個範例會使用 `ICollector` 寫入多個佇列訊息：</span><span class="sxs-lookup"><span data-stu-id="babcd-128">This example writes multiple queue messages using `ICollector`:</span></span>

```csharp
public static void Run(ICollector<string> myQueueItem, TraceWriter log)
{
    myQueueItem.Add("Hello");
    myQueueItem.Add("World!");
}
```

## <a name="logging"></a><span data-ttu-id="babcd-129">記錄</span><span class="sxs-lookup"><span data-stu-id="babcd-129">Logging</span></span>
<span data-ttu-id="babcd-130">若要使用 C# 將輸出記錄至串流記錄，請包含 `TraceWriter` 類型的引數。</span><span class="sxs-lookup"><span data-stu-id="babcd-130">To log output to your streaming logs in C#, include an argument of type `TraceWriter`.</span></span> <span data-ttu-id="babcd-131">建議您將它命名為 `log`。</span><span class="sxs-lookup"><span data-stu-id="babcd-131">We recommend that you name it `log`.</span></span> <span data-ttu-id="babcd-132">避免在 Azure Functions 中使用 `Console.Write`。</span><span class="sxs-lookup"><span data-stu-id="babcd-132">Avoid using `Console.Write` in Azure Functions.</span></span> 

<span data-ttu-id="babcd-133">`TraceWriter` 已定義於 [Azure WebJobs SDK](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.Host/TraceWriter.cs)。</span><span class="sxs-lookup"><span data-stu-id="babcd-133">`TraceWriter` is defined in the [Azure WebJobs SDK](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.Host/TraceWriter.cs).</span></span> <span data-ttu-id="babcd-134">可以在 [host\.json] 中設定 `TraceWriter` 的記錄層級。</span><span class="sxs-lookup"><span data-stu-id="babcd-134">The log level for `TraceWriter` can be configured in [host\.json].</span></span>

```csharp
public static void Run(string myBlob, TraceWriter log)
{
    log.Info($"C# Blob trigger function processed: {myBlob}");
}
```

## <a name="async"></a><span data-ttu-id="babcd-135">非同步處理</span><span class="sxs-lookup"><span data-stu-id="babcd-135">Async</span></span>
<span data-ttu-id="babcd-136">若要讓函式變成非同步，請使用 `async` 關鍵字並傳回 `Task` 物件。</span><span class="sxs-lookup"><span data-stu-id="babcd-136">To make a function asynchronous, use the `async` keyword and return a `Task` object.</span></span>

```csharp
public async static Task ProcessQueueMessageAsync(
        string blobName,
        Stream blobInput,
        Stream blobOutput)
{
    await blobInput.CopyToAsync(blobOutput, 4096, token);
}
```

## <a name="cancellation-token"></a><span data-ttu-id="babcd-137">取消權杖</span><span class="sxs-lookup"><span data-stu-id="babcd-137">Cancellation Token</span></span>
<span data-ttu-id="babcd-138">某些作業需要正常關機。</span><span class="sxs-lookup"><span data-stu-id="babcd-138">Some operations require graceful shutdown.</span></span> <span data-ttu-id="babcd-139">雖然撰寫能夠處理當機情況的程式碼一律是最理想的做法，但是如果您想要處理順利關機要求，您可以定義 [`CancellationToken`](https://msdn.microsoft.com/library/system.threading.cancellationtoken.aspx) 類型的引數。</span><span class="sxs-lookup"><span data-stu-id="babcd-139">While it's always best to write code that can handle crashing,  in cases where you want to handle graceful shutdown requests, you define a [`CancellationToken`](https://msdn.microsoft.com/library/system.threading.cancellationtoken.aspx) typed argument.</span></span>  <span data-ttu-id="babcd-140">提供 `CancellationToken` ，表示已觸發主機關機。</span><span class="sxs-lookup"><span data-stu-id="babcd-140">A `CancellationToken` is provided to signal that a host shutdown is triggered.</span></span>

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

## <a name="importing-namespaces"></a><span data-ttu-id="babcd-141">匯入命名空間</span><span class="sxs-lookup"><span data-stu-id="babcd-141">Importing namespaces</span></span>
<span data-ttu-id="babcd-142">如果您需要匯入命名空間，可以如往常一樣利用 `using` 子句。</span><span class="sxs-lookup"><span data-stu-id="babcd-142">If you need to import namespaces, you can do so as usual, with the `using` clause.</span></span>

```csharp
using System.Net;
using System.Threading.Tasks;

public static Task<HttpResponseMessage> Run(HttpRequestMessage req, TraceWriter log)
```

<span data-ttu-id="babcd-143">下列命名空間會自動匯入，所以是選擇性的︰</span><span class="sxs-lookup"><span data-stu-id="babcd-143">The following namespaces are automatically imported and are therefore optional:</span></span>

* `System`
* `System.Collections.Generic`
* `System.IO`
* `System.Linq`
* `System.Net.Http`
* `System.Threading.Tasks`
* `Microsoft.Azure.WebJobs`
* `Microsoft.Azure.WebJobs.Host`

## <a name="referencing-external-assemblies"></a><span data-ttu-id="babcd-144">參考外部組件</span><span class="sxs-lookup"><span data-stu-id="babcd-144">Referencing External Assemblies</span></span>
<span data-ttu-id="babcd-145">若為架構組件，請使用 `#r "AssemblyName"` 指示詞加入參考。</span><span class="sxs-lookup"><span data-stu-id="babcd-145">For framework assemblies, add references by using the `#r "AssemblyName"` directive.</span></span>

```csharp
#r "System.Web.Http"

using System.Net;
using System.Net.Http;
using System.Threading.Tasks;

public static Task<HttpResponseMessage> Run(HttpRequestMessage req, TraceWriter log)
```

<span data-ttu-id="babcd-146">Azure Functions 裝載環境會自動加入下列組件︰</span><span class="sxs-lookup"><span data-stu-id="babcd-146">The following assemblies are automatically added by the Azure Functions hosting environment:</span></span>

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

<span data-ttu-id="babcd-147">simple-name 可能會參考下列組件 (例如，`#r "AssemblyName"`)：</span><span class="sxs-lookup"><span data-stu-id="babcd-147">The following assemblies may be referenced by simple-name (for example, `#r "AssemblyName"`):</span></span>

* `Newtonsoft.Json`
* `Microsoft.WindowsAzure.Storage`
* `Microsoft.ServiceBus`
* `Microsoft.AspNet.WebHooks.Receivers`
* `Microsoft.AspNet.WebHooks.Common`
* `Microsoft.Azure.NotificationHubs`

## <a name="referencing-custom-assemblies"></a><span data-ttu-id="babcd-148">參考自訂組件</span><span class="sxs-lookup"><span data-stu-id="babcd-148">Referencing custom assemblies</span></span>

<span data-ttu-id="babcd-149">若要參考自訂組件，您可以使用「共用」組件或「私人」組件：</span><span class="sxs-lookup"><span data-stu-id="babcd-149">To reference a custom assembly, you can use either a *shared* assembly or a *private* assembly:</span></span>
- <span data-ttu-id="babcd-150">共用組件會共用於函式應用程式內的所有函式。</span><span class="sxs-lookup"><span data-stu-id="babcd-150">Shared assemblies are shared across all functions within a function app.</span></span> <span data-ttu-id="babcd-151">若要參考自訂組件上，請將組件上傳至應用程式函式，例如在函式應用程式根目錄的 `bin` 資料夾中。</span><span class="sxs-lookup"><span data-stu-id="babcd-151">To reference a custom assembly, upload the assembly to your function app, such as in a `bin` folder in the function app root.</span></span> 
- <span data-ttu-id="babcd-152">私人組件屬於所指定函式的內容，而且支援不同版本的側載。</span><span class="sxs-lookup"><span data-stu-id="babcd-152">Private assemblies are part of a given function's context, and support side-loading of different versions.</span></span> <span data-ttu-id="babcd-153">應該在函式目錄的 `bin` 資料夾中上傳私人組件。</span><span class="sxs-lookup"><span data-stu-id="babcd-153">Private assemblies should be uploaded in a `bin` folder in the function directory.</span></span> <span data-ttu-id="babcd-154">使用檔案名稱 (例如 `#r "MyAssembly.dll"`) 進行參照。</span><span class="sxs-lookup"><span data-stu-id="babcd-154">Reference using the file name, such as  `#r "MyAssembly.dll"`.</span></span> 

<span data-ttu-id="babcd-155">如需如何將檔案上傳至函數資料夾的資訊，請參閱以下的＜封裝管理＞小節。</span><span class="sxs-lookup"><span data-stu-id="babcd-155">For information on how to upload files to your function folder, see the following section on package management.</span></span>

### <a name="watched-directories"></a><span data-ttu-id="babcd-156">監看的目錄</span><span class="sxs-lookup"><span data-stu-id="babcd-156">Watched directories</span></span>

<span data-ttu-id="babcd-157">系統會自動監看包含函式指令碼檔案之目錄中的組件變更。</span><span class="sxs-lookup"><span data-stu-id="babcd-157">The directory that contains the function script file is automatically watched for changes to assemblies.</span></span> <span data-ttu-id="babcd-158">若要監看其他目錄中的組件變更，將它們新增至 [host\.json] 中的 `watchDirectories` 清單。</span><span class="sxs-lookup"><span data-stu-id="babcd-158">To watch for assembly changes in other directories, add them to the `watchDirectories` list in [host\.json].</span></span>

## <a name="using-nuget-packages"></a><span data-ttu-id="babcd-159">使用 NuGet 套件</span><span class="sxs-lookup"><span data-stu-id="babcd-159">Using NuGet packages</span></span>
<span data-ttu-id="babcd-160">若要在 C# 函式中使用 NuGet 套件，請將 project.json  檔案上傳至函式應用程式檔案系統中的函式資料夾。</span><span class="sxs-lookup"><span data-stu-id="babcd-160">To use NuGet packages in a C# function, upload a *project.json* file to the function's folder in the function app's file system.</span></span> <span data-ttu-id="babcd-161">以下是範例 project.json  檔案，該檔案會加入對 Microsoft.ProjectOxford.Face 1.1.0 版的參考：</span><span class="sxs-lookup"><span data-stu-id="babcd-161">Here is an example *project.json* file that adds a reference to Microsoft.ProjectOxford.Face version 1.1.0:</span></span>

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

<span data-ttu-id="babcd-162">只支援 .NET Framework 4.6，因此請確認您的 *project.json* 檔案指定 `net46`，如以下所示。</span><span class="sxs-lookup"><span data-stu-id="babcd-162">Only the .NET Framework 4.6 is supported, so make sure that your *project.json* file specifies `net46` as shown here.</span></span>

<span data-ttu-id="babcd-163">當您上傳 project.json  檔案時，執行階段會取得封裝並自動加入對封裝組件的參考。</span><span class="sxs-lookup"><span data-stu-id="babcd-163">When you upload a *project.json* file, the runtime gets the packages and automatically adds references to the package assemblies.</span></span> <span data-ttu-id="babcd-164">您不需要加入 `#r "AssemblyName"` 指示詞。</span><span class="sxs-lookup"><span data-stu-id="babcd-164">You don't need to add `#r "AssemblyName"` directives.</span></span> <span data-ttu-id="babcd-165">若要使用 NuGet 套件中定義的類型，請將所需的 `using` 陳述式新增到 *run.csx* 檔案</span><span class="sxs-lookup"><span data-stu-id="babcd-165">To use the types defined in the NuGet packages, add the required `using` statements to your *run.csx* file</span></span> 

<span data-ttu-id="babcd-166">在 Functions 執行階段中，NuGet 還原會透過比較 `project.json` 和 `project.lock.json` 來運作。</span><span class="sxs-lookup"><span data-stu-id="babcd-166">In the Functions runtime, NuGet restore works by comparing `project.json` and `project.lock.json`.</span></span> <span data-ttu-id="babcd-167">如果檔案的日期和時間戳記**不**相符，會執行 NuGet 還原，且 NuGet 會下載更新的套件。</span><span class="sxs-lookup"><span data-stu-id="babcd-167">If the date and time stamps of the files **do not** match, a NuGet restore runs and NuGet downloads updated packages.</span></span> <span data-ttu-id="babcd-168">不過，如果檔案的日期和時間戳記**相符**，NuGet 不會執行還原。</span><span class="sxs-lookup"><span data-stu-id="babcd-168">However, if the date and time stamps of the files **do** match, NuGet does not perform a restore.</span></span> <span data-ttu-id="babcd-169">因此，不應該部署 `project.lock.json`，因為它會導致 NuGet 略過還原。</span><span class="sxs-lookup"><span data-stu-id="babcd-169">Therefore, `project.lock.json` should not be deployed as it causes NuGet to skip package restore.</span></span> <span data-ttu-id="babcd-170">若要避免部署鎖定檔案，請將 `project.lock.json` 加入至 `.gitignore` 檔案。</span><span class="sxs-lookup"><span data-stu-id="babcd-170">To avoid deploying the lock file, add the `project.lock.json` to the `.gitignore` file.</span></span>

<span data-ttu-id="babcd-171">若要使用自訂 NuGet 摘要，請在函式應用程式根目錄的 *Nuget.Config* 檔案中指定摘要。</span><span class="sxs-lookup"><span data-stu-id="babcd-171">To use a custom NuGet feed, specify the feed in a *Nuget.Config* file in the Function App root.</span></span> <span data-ttu-id="babcd-172">如需詳細資訊，請參閱[設定 NuGet 行為](/nuget/consume-packages/configuring-nuget-behavior)。</span><span class="sxs-lookup"><span data-stu-id="babcd-172">For more information, see [Configuring NuGet behavior](/nuget/consume-packages/configuring-nuget-behavior).</span></span>

### <a name="using-a-projectjson-file"></a><span data-ttu-id="babcd-173">使用 project.json 檔案</span><span class="sxs-lookup"><span data-stu-id="babcd-173">Using a project.json file</span></span>
1. <span data-ttu-id="babcd-174">在 Azure 入口網站中開啟函式。</span><span class="sxs-lookup"><span data-stu-id="babcd-174">Open the function in the Azure portal.</span></span> <span data-ttu-id="babcd-175">[記錄] 索引標籤會顯示套件安裝輸出。</span><span class="sxs-lookup"><span data-stu-id="babcd-175">The logs tab displays the package installation output.</span></span>
2. <span data-ttu-id="babcd-176">若要上傳 project.json 檔案，請使用 Azure Functions 開發人員參考主題的[如何更新函式應用程式檔案](functions-reference.md#fileupdate)所述的其中一個方法。</span><span class="sxs-lookup"><span data-stu-id="babcd-176">To upload a project.json file, use one of the methods described in the [How to update function app files](functions-reference.md#fileupdate) in the Azure Functions developer reference topic.</span></span>
3. <span data-ttu-id="babcd-177">上傳 project.json  檔案之後，您會在函式的串流記錄檔中看到如下列範例所示的輸出：</span><span class="sxs-lookup"><span data-stu-id="babcd-177">After the *project.json* file is uploaded, you see output like the following example in your function's streaming log:</span></span>

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

## <a name="environment-variables"></a><span data-ttu-id="babcd-178">環境變數</span><span class="sxs-lookup"><span data-stu-id="babcd-178">Environment variables</span></span>
<span data-ttu-id="babcd-179">若要取得環境變數或應用程式設定值，請使用 `System.Environment.GetEnvironmentVariable`，如下列程式碼範例所示：</span><span class="sxs-lookup"><span data-stu-id="babcd-179">To get an environment variable or an app setting value, use `System.Environment.GetEnvironmentVariable`, as shown in the following code example:</span></span>

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

## <a name="reusing-csx-code"></a><span data-ttu-id="babcd-180">重複使用 .csx 程式碼</span><span class="sxs-lookup"><span data-stu-id="babcd-180">Reusing .csx code</span></span>
<span data-ttu-id="babcd-181">您可以在您的 *run.csx* 檔案中使用其他 *.csx* 檔案中定義的類別和方法。</span><span class="sxs-lookup"><span data-stu-id="babcd-181">You can use classes and methods defined in other *.csx* files in your *run.csx* file.</span></span> <span data-ttu-id="babcd-182">若要這樣做，請在您的 *run.csx* 檔案中使用 `#load` 指示詞。</span><span class="sxs-lookup"><span data-stu-id="babcd-182">To do that, use `#load` directives in your *run.csx* file.</span></span> <span data-ttu-id="babcd-183">在下列範例中，名為 `MyLogger` 的記錄常式已在 *myLogger.csx* 中共用，並使用 `#load` 指示詞載入至 *run.csx*︰</span><span class="sxs-lookup"><span data-stu-id="babcd-183">In the following example, a logging routine named `MyLogger` is shared in *myLogger.csx* and loaded into *run.csx* using the `#load` directive:</span></span>

<span data-ttu-id="babcd-184">範例 run.csx ：</span><span class="sxs-lookup"><span data-stu-id="babcd-184">Example *run.csx*:</span></span>

```csharp
#load "mylogger.csx"

public static void Run(TimerInfo myTimer, TraceWriter log)
{
    log.Verbose($"Log by run.csx: {DateTime.Now}");
    MyLogger(log, $"Log by MyLogger: {DateTime.Now}");
}
```

<span data-ttu-id="babcd-185">範例 mylogger.csx ：</span><span class="sxs-lookup"><span data-stu-id="babcd-185">Example *mylogger.csx*:</span></span>

```csharp
public static void MyLogger(TraceWriter log, string logtext)
{
    log.Verbose(logtext);
}
```

<span data-ttu-id="babcd-186">當您想要在使用一個 POCO 物件的函式之間使引數成為強式類型，使用共用的 *.csx* 是常見的模式。</span><span class="sxs-lookup"><span data-stu-id="babcd-186">Using a shared *.csx* is a common pattern when you want to strongly type your arguments between functions using a POCO object.</span></span> <span data-ttu-id="babcd-187">在下列簡化的範例中，HTTP 觸發程序和佇列觸發程序共用一個名為 `Order` 的 POCO 物件，來使排序資料成為強式類型︰</span><span class="sxs-lookup"><span data-stu-id="babcd-187">In the following simplified example, an HTTP trigger and queue trigger share a POCO object named `Order` to strongly type the order data:</span></span>

<span data-ttu-id="babcd-188">HTTP 觸發程序的範例 *run.csx*︰</span><span class="sxs-lookup"><span data-stu-id="babcd-188">Example *run.csx* for HTTP trigger:</span></span>

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

<span data-ttu-id="babcd-189">佇列觸發程序的範例 *run.csx*︰</span><span class="sxs-lookup"><span data-stu-id="babcd-189">Example *run.csx* for queue trigger:</span></span>

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

<span data-ttu-id="babcd-190">範例 *order.csx*：</span><span class="sxs-lookup"><span data-stu-id="babcd-190">Example *order.csx*:</span></span>

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

<span data-ttu-id="babcd-191">您可以使用包含 `#load` 指示詞的相對路徑：</span><span class="sxs-lookup"><span data-stu-id="babcd-191">You can use a relative path with the `#load` directive:</span></span>

* <span data-ttu-id="babcd-192">`#load "mylogger.csx"` 會載入位於函式資料夾中的檔案。</span><span class="sxs-lookup"><span data-stu-id="babcd-192">`#load "mylogger.csx"` loads a file located in the function folder.</span></span>
* <span data-ttu-id="babcd-193">`#load "loadedfiles\mylogger.csx"` 會載入位於函式資料夾的資料夾中的檔案。</span><span class="sxs-lookup"><span data-stu-id="babcd-193">`#load "loadedfiles\mylogger.csx"` loads a file located in a folder in the function folder.</span></span>
* <span data-ttu-id="babcd-194">`#load "..\shared\mylogger.csx"` 會載入位於與函式資料夾相同層級的資料夾中的檔案 (也就是在 [wwwroot] 的正下方)。</span><span class="sxs-lookup"><span data-stu-id="babcd-194">`#load "..\shared\mylogger.csx"` loads a file located in a folder at the same level as the function folder, that is, directly under *wwwroot*.</span></span>

<span data-ttu-id="babcd-195">`#load` 指示詞只適用於 *.csx* (C# 指令碼) 檔案，不適用於 *.cs* 檔案。</span><span class="sxs-lookup"><span data-stu-id="babcd-195">The `#load` directive works only with *.csx* (C# script) files, not with *.cs* files.</span></span>

<a name="imperative-bindings"></a> 

## <a name="binding-at-runtime-via-imperative-bindings"></a><span data-ttu-id="babcd-196">透過命令式繫結在執行階段繫結</span><span class="sxs-lookup"><span data-stu-id="babcd-196">Binding at runtime via imperative bindings</span></span>

<span data-ttu-id="babcd-197">在 C# 和其他 .NET 語言中，您可以使用相對於 *function.json* 中[*宣告式*](https://en.wikipedia.org/wiki/Declarative_programming)繫結的[命令式](https://en.wikipedia.org/wiki/Imperative_programming)繫結模式。</span><span class="sxs-lookup"><span data-stu-id="babcd-197">In C# and other .NET languages, you can use an [imperative](https://en.wikipedia.org/wiki/Imperative_programming) binding pattern, as opposed to the [*declarative*](https://en.wikipedia.org/wiki/Declarative_programming) bindings in *function.json*.</span></span> <span data-ttu-id="babcd-198">當繫結參數需要在執行階段而不是設計階段中計算時，命令式繫結非常有用。</span><span class="sxs-lookup"><span data-stu-id="babcd-198">Imperative binding is useful when binding parameters need to be computed at runtime rather than design time.</span></span> <span data-ttu-id="babcd-199">利用此模式，您可以快速在您的函式程式碼中繫結至支援的輸入和輸出繫結。</span><span class="sxs-lookup"><span data-stu-id="babcd-199">With this pattern, you can bind to supported input and output binding on-the-fly in your function code.</span></span>

<span data-ttu-id="babcd-200">定義命令式繫結，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="babcd-200">Define an imperative binding as follows:</span></span>

- <span data-ttu-id="babcd-201">**請勿**在 *function.json* 中為您所需的命令式繫結併入項目。</span><span class="sxs-lookup"><span data-stu-id="babcd-201">**Do not** include an entry in *function.json* for your desired imperative bindings.</span></span>
- <span data-ttu-id="babcd-202">傳入輸入參數 [`Binder binder`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.Host/Bindings/Runtime/Binder.cs) 或 [`IBinder binder`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IBinder.cs)。</span><span class="sxs-lookup"><span data-stu-id="babcd-202">Pass in an input parameter [`Binder binder`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.Host/Bindings/Runtime/Binder.cs) or [`IBinder binder`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IBinder.cs).</span></span>
- <span data-ttu-id="babcd-203">使用下列 C# 模式來執行資料繫結。</span><span class="sxs-lookup"><span data-stu-id="babcd-203">Use the following C# pattern to perform the data binding.</span></span>

```cs
using (var output = await binder.BindAsync<T>(new BindingTypeAttribute(...)))
{
    ...
}
```

<span data-ttu-id="babcd-204">其中 `BindingTypeAttribute` 是可定義繫結的.NET 屬性，而 `T` 是該繫結類型支援的輸入或輸出類型。</span><span class="sxs-lookup"><span data-stu-id="babcd-204">where `BindingTypeAttribute` is the .NET attribute that defines your binding and `T` is the input or output type that's supported by that binding type.</span></span> <span data-ttu-id="babcd-205">`T` 也不能是 `out` 參數類型 (例如 `out JObject`)。</span><span class="sxs-lookup"><span data-stu-id="babcd-205">`T` also cannot be an `out` parameter type (such as `out JObject`).</span></span> <span data-ttu-id="babcd-206">例如，Mobile Apps 資料表輸出繫結支援[六個輸出類型](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.MobileApps/MobileTableAttribute.cs#L17-L22)，但您只可以對 `T` 使用 [ICollector<T>](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/ICollector.cs) 或 [IAsyncCollector<T>](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IAsyncCollector.cs)。</span><span class="sxs-lookup"><span data-stu-id="babcd-206">For example, the Mobile Apps table output binding supports [six output types](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.MobileApps/MobileTableAttribute.cs#L17-L22), but you can only use [ICollector<T>](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/ICollector.cs) or [IAsyncCollector<T>](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IAsyncCollector.cs) for `T`.</span></span>

<span data-ttu-id="babcd-207">下列範例程式碼會使用在執行階段定義的 blob 路徑來建立[儲存體 blob 輸出繫結](functions-bindings-storage-blob.md#using-a-blob-output-binding)，然後將字串寫入 blob。</span><span class="sxs-lookup"><span data-stu-id="babcd-207">The following example code creates a [Storage blob output binding](functions-bindings-storage-blob.md#using-a-blob-output-binding) with blob path that's defined at run time, then writes a string to the blob.</span></span>

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

<span data-ttu-id="babcd-208">[BlobAttribute](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/BlobAttribute.cs) 會定義[儲存體 blob](functions-bindings-storage-blob.md) 輸入或輸出繫結，而 [TextWriter](https://msdn.microsoft.com/library/system.io.textwriter.aspx) 是支援的輸出繫結類型。</span><span class="sxs-lookup"><span data-stu-id="babcd-208">[BlobAttribute](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/BlobAttribute.cs) defines the [Storage blob](functions-bindings-storage-blob.md) input or output binding, and [TextWriter](https://msdn.microsoft.com/library/system.io.textwriter.aspx) is a supported output binding type.</span></span>
<span data-ttu-id="babcd-209">此程式碼會依原樣取得儲存體帳戶連接字串的預設應用程式設定 (也就是 `AzureWebJobsStorage`)。</span><span class="sxs-lookup"><span data-stu-id="babcd-209">As is, the code gets the default app setting for the Storage account connection string (which is `AzureWebJobsStorage`).</span></span> <span data-ttu-id="babcd-210">您可以指定要使用的自訂應用程式設定，方法是新增 [StorageAccountAttribute](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs) 並將屬性陣列傳遞至 `BindAsync<T>()`。</span><span class="sxs-lookup"><span data-stu-id="babcd-210">You can specify a custom app setting to use by adding the [StorageAccountAttribute](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs) and passing the attribute array into `BindAsync<T>()`.</span></span> <span data-ttu-id="babcd-211">例如，</span><span class="sxs-lookup"><span data-stu-id="babcd-211">For example,</span></span>

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

<span data-ttu-id="babcd-212">下表列出每個繫結類型的 .NET 屬性，以及定義它們的套件。</span><span class="sxs-lookup"><span data-stu-id="babcd-212">The following table lists the .NET attributes for each binding type and the packages in which they are defined.</span></span>

> [!div class="mx-codeBreakAll"]
| <span data-ttu-id="babcd-213">繫結</span><span class="sxs-lookup"><span data-stu-id="babcd-213">Binding</span></span> | <span data-ttu-id="babcd-214">屬性</span><span class="sxs-lookup"><span data-stu-id="babcd-214">Attribute</span></span> | <span data-ttu-id="babcd-215">新增參考</span><span class="sxs-lookup"><span data-stu-id="babcd-215">Add reference</span></span> |
|------|------|------|
| <span data-ttu-id="babcd-216">Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="babcd-216">Cosmos DB</span></span> | [`Microsoft.Azure.WebJobs.DocumentDBAttribute`](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.DocumentDB/DocumentDBAttribute.cs) | `#r "Microsoft.Azure.WebJobs.Extensions.DocumentDB"` |
| <span data-ttu-id="babcd-217">事件中樞</span><span class="sxs-lookup"><span data-stu-id="babcd-217">Event Hubs</span></span> | <span data-ttu-id="babcd-218">[`Microsoft.Azure.WebJobs.ServiceBus.EventHubAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/EventHubs/EventHubAttribute.cs), [`Microsoft.Azure.WebJobs.ServiceBusAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAccountAttribute.cs)</span><span class="sxs-lookup"><span data-stu-id="babcd-218">[`Microsoft.Azure.WebJobs.ServiceBus.EventHubAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/EventHubs/EventHubAttribute.cs), [`Microsoft.Azure.WebJobs.ServiceBusAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAccountAttribute.cs)</span></span> | `#r "Microsoft.Azure.Jobs.ServiceBus"` |
| <span data-ttu-id="babcd-219">行動應用程式</span><span class="sxs-lookup"><span data-stu-id="babcd-219">Mobile Apps</span></span> | [`Microsoft.Azure.WebJobs.MobileTableAttribute`](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.MobileApps/MobileTableAttribute.cs) | `#r "Microsoft.Azure.WebJobs.Extensions.MobileApps"` |
| <span data-ttu-id="babcd-220">通知中樞</span><span class="sxs-lookup"><span data-stu-id="babcd-220">Notification Hubs</span></span> | [`Microsoft.Azure.WebJobs.NotificationHubAttribute`](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.NotificationHubs/NotificationHubAttribute.cs) | `#r "Microsoft.Azure.WebJobs.Extensions.NotificationHubs"` |
| <span data-ttu-id="babcd-221">服務匯流排</span><span class="sxs-lookup"><span data-stu-id="babcd-221">Service Bus</span></span> | <span data-ttu-id="babcd-222">[`Microsoft.Azure.WebJobs.ServiceBusAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAttribute.cs), [`Microsoft.Azure.WebJobs.ServiceBusAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAccountAttribute.cs)</span><span class="sxs-lookup"><span data-stu-id="babcd-222">[`Microsoft.Azure.WebJobs.ServiceBusAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAttribute.cs), [`Microsoft.Azure.WebJobs.ServiceBusAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAccountAttribute.cs)</span></span> | `#r "Microsoft.Azure.WebJobs.ServiceBus"` |
| <span data-ttu-id="babcd-223">儲存體佇列</span><span class="sxs-lookup"><span data-stu-id="babcd-223">Storage queue</span></span> | <span data-ttu-id="babcd-224">[`Microsoft.Azure.WebJobs.QueueAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/QueueAttribute.cs), [`Microsoft.Azure.WebJobs.StorageAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs)</span><span class="sxs-lookup"><span data-stu-id="babcd-224">[`Microsoft.Azure.WebJobs.QueueAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/QueueAttribute.cs), [`Microsoft.Azure.WebJobs.StorageAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs)</span></span> | |
| <span data-ttu-id="babcd-225">儲存體 Blob</span><span class="sxs-lookup"><span data-stu-id="babcd-225">Storage blob</span></span> | <span data-ttu-id="babcd-226">[`Microsoft.Azure.WebJobs.BlobAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/BlobAttribute.cs), [`Microsoft.Azure.WebJobs.StorageAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs)</span><span class="sxs-lookup"><span data-stu-id="babcd-226">[`Microsoft.Azure.WebJobs.BlobAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/BlobAttribute.cs), [`Microsoft.Azure.WebJobs.StorageAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs)</span></span> | |
| <span data-ttu-id="babcd-227">儲存體資料表</span><span class="sxs-lookup"><span data-stu-id="babcd-227">Storage table</span></span> | <span data-ttu-id="babcd-228">[`Microsoft.Azure.WebJobs.TableAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/TableAttribute.cs), [`Microsoft.Azure.WebJobs.StorageAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs)</span><span class="sxs-lookup"><span data-stu-id="babcd-228">[`Microsoft.Azure.WebJobs.TableAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/TableAttribute.cs), [`Microsoft.Azure.WebJobs.StorageAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs)</span></span> | |
| <span data-ttu-id="babcd-229">Twilio</span><span class="sxs-lookup"><span data-stu-id="babcd-229">Twilio</span></span> | [`Microsoft.Azure.WebJobs.TwilioSmsAttribute`](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.Twilio/TwilioSMSAttribute.cs) | `#r "Microsoft.Azure.WebJobs.Extensions.Twilio"` |



## <a name="next-steps"></a><span data-ttu-id="babcd-230">後續步驟</span><span class="sxs-lookup"><span data-stu-id="babcd-230">Next steps</span></span>
<span data-ttu-id="babcd-231">如需詳細資訊，請參閱下列資源：</span><span class="sxs-lookup"><span data-stu-id="babcd-231">For more information, see the following resources:</span></span>

* [<span data-ttu-id="babcd-232">Azure Functions 的最佳做法</span><span class="sxs-lookup"><span data-stu-id="babcd-232">Best Practices for Azure Functions</span></span>](functions-best-practices.md)
* [<span data-ttu-id="babcd-233">Azure Functions 開發人員參考</span><span class="sxs-lookup"><span data-stu-id="babcd-233">Azure Functions developer reference</span></span>](functions-reference.md)
* [<span data-ttu-id="babcd-234">Azure Functions F# 開發人員參考</span><span class="sxs-lookup"><span data-stu-id="babcd-234">Azure Functions F# developer reference</span></span>](functions-reference-fsharp.md)
* [<span data-ttu-id="babcd-235">Azure Functions NodeJS 開發人員參考</span><span class="sxs-lookup"><span data-stu-id="babcd-235">Azure Functions NodeJS developer reference</span></span>](functions-reference-node.md)
* [<span data-ttu-id="babcd-236">Azure Functions 觸發程序和繫結</span><span class="sxs-lookup"><span data-stu-id="babcd-236">Azure Functions triggers and bindings</span></span>](functions-triggers-bindings.md)

[host\.json]: https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json
