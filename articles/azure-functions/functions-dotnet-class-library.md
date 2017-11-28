---
title: "aaaUsing.NET 類別庫來搭配 Azure 函式 |Microsoft 文件"
description: "了解如何 tooauthor.NET 類別庫使用的 Azure 函式"
services: functions
documentationcenter: na
author: lindydonna
manager: erikre
editor: 
tags: 
keywords: "azure functions, 函數, 事件處理, 動態運算, 無伺服器架構"
ms.assetid: 9f5db0c2-a88e-4fa8-9b59-37a7096fc828
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 06/09/2017
ms.author: donnam
ms.openlocfilehash: 4e0fd954b554006ba1d8ecc47403a9fb1c67c3b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="using-net-class-libraries-with-azure-functions"></a><span data-ttu-id="3464d-104">使用 .NET 類別庫搭配 Azure Functions</span><span class="sxs-lookup"><span data-stu-id="3464d-104">Using .NET class libraries with Azure Functions</span></span>

<span data-ttu-id="3464d-105">此外 tooscript 檔案，Azure 函式支援發行類別庫做為一或多個函式的 hello 實作。</span><span class="sxs-lookup"><span data-stu-id="3464d-105">In addition tooscript files, Azure Functions supports publishing a class library as hello implementation for one or more functions.</span></span> <span data-ttu-id="3464d-106">我們建議您改用 hello [Azure 函式 Visual Studio 2017 Tools](https://blogs.msdn.microsoft.com/webdev/2017/05/10/azure-function-tools-for-visual-studio-2017/)。</span><span class="sxs-lookup"><span data-stu-id="3464d-106">We recommend that you use hello [Azure Functions Visual Studio 2017 Tools](https://blogs.msdn.microsoft.com/webdev/2017/05/10/azure-function-tools-for-visual-studio-2017/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3464d-107">必要條件</span><span class="sxs-lookup"><span data-stu-id="3464d-107">Prerequisites</span></span> 

<span data-ttu-id="3464d-108">這篇文章有 hello 下列必要條件：</span><span class="sxs-lookup"><span data-stu-id="3464d-108">This article has hello following prerequisites:</span></span>

- <span data-ttu-id="3464d-109">[Visual Studio 2017 15.3 預覽](https://www.visualstudio.com/vs/preview/)。</span><span class="sxs-lookup"><span data-stu-id="3464d-109">[Visual Studio 2017 15.3 Preview](https://www.visualstudio.com/vs/preview/).</span></span> <span data-ttu-id="3464d-110">安裝 hello 工作負載**ASP.NET 及 web 開發**和**Azure 開發**。</span><span class="sxs-lookup"><span data-stu-id="3464d-110">Install hello workloads **ASP.NET and web development** and **Azure development**.</span></span>
- [<span data-ttu-id="3464d-111">Azure Function Tools for Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="3464d-111">Azure Function Tools for Visual Studio 2017</span></span>](https://marketplace.visualstudio.com/items?itemName=AndrewBHall-MSFT.AzureFunctionToolsforVisualStudio2017)

## <a name="functions-class-library-project"></a><span data-ttu-id="3464d-112">Functions 類別庫專案</span><span class="sxs-lookup"><span data-stu-id="3464d-112">Functions class library project</span></span>

<span data-ttu-id="3464d-113">從 Visual Studio 中建立 Azure Functions 專案。</span><span class="sxs-lookup"><span data-stu-id="3464d-113">From Visual Studio, create a new Azure Functions project.</span></span> <span data-ttu-id="3464d-114">hello 新的專案範本建立 hello 檔案*host.json*和*local.settings.json*。</span><span class="sxs-lookup"><span data-stu-id="3464d-114">hello new project template creates hello files *host.json* and *local.settings.json*.</span></span> <span data-ttu-id="3464d-115">您可以[在 host.json 中自訂 Azure Functions 執行階段設定](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json)。</span><span class="sxs-lookup"><span data-stu-id="3464d-115">You can [customize Azure Functions runtime settings in host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json).</span></span> 

<span data-ttu-id="3464d-116">hello 檔案*local.settings.json*儲存應用程式設定、 連接字串和 Azure 函式的核心工具的設定。</span><span class="sxs-lookup"><span data-stu-id="3464d-116">hello file *local.settings.json* stores app settings, connection strings, and settings for Azure Functions Core Tools.</span></span> <span data-ttu-id="3464d-117">toolearn 進一步了解它的結構，請參閱[程式碼和測試 Azure 函式在本機](functions-run-local.md#local-settings)。</span><span class="sxs-lookup"><span data-stu-id="3464d-117">toolearn more about its structure, see [Code and test Azure functions locally](functions-run-local.md#local-settings).</span></span>

### <a name="functionname-attribute"></a><span data-ttu-id="3464d-118">FunctionName 屬性</span><span class="sxs-lookup"><span data-stu-id="3464d-118">FunctionName attribute</span></span>

<span data-ttu-id="3464d-119">hello 屬性[ `FunctionNameAttribute` ](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/FunctionNameAttribute.cs)標記做為函式進入點方法。</span><span class="sxs-lookup"><span data-stu-id="3464d-119">hello attribute [`FunctionNameAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/FunctionNameAttribute.cs) marks a method as a function entry point.</span></span> <span data-ttu-id="3464d-120">它必須剛好僅與一個觸發程序以及 0 個以上的輸入和輸出繫結搭配使用。</span><span class="sxs-lookup"><span data-stu-id="3464d-120">It must be used with exactly one trigger and 0 or more input and output bindings.</span></span>

### <a name="conversion-toofunctionjson"></a><span data-ttu-id="3464d-121">轉換 toofunction.json</span><span class="sxs-lookup"><span data-stu-id="3464d-121">Conversion toofunction.json</span></span>

<span data-ttu-id="3464d-122">Azure 函式專案建置時，它會產生一個檔案`function.json`hello 目錄中符合 hello 函式名稱所定義`[FunctionName]`。</span><span class="sxs-lookup"><span data-stu-id="3464d-122">When an Azure Functions project is built, it produces a file `function.json` in hello directory matching hello function name defined by `[FunctionName]`.</span></span> <span data-ttu-id="3464d-123">它會指定觸發程序和繫結和點 toohello 專案的組件檔。</span><span class="sxs-lookup"><span data-stu-id="3464d-123">It specifies triggers and bindings and points toohello project assembly file.</span></span>

<span data-ttu-id="3464d-124">Hello NuGet 封裝會執行此轉換[Microsoft\.NET\.Sdk\.函式](http://www.nuget.org/packages/Microsoft.NET.Sdk.Functions)。</span><span class="sxs-lookup"><span data-stu-id="3464d-124">This conversion is performed by hello NuGet package [Microsoft\.NET\.Sdk\.Functions](http://www.nuget.org/packages/Microsoft.NET.Sdk.Functions).</span></span> <span data-ttu-id="3464d-125">hello 來源可供使用 hello GitHub 儲存機制內[azure\-函式\-vs\-建置\-sdk](https://github.com/Azure/azure-functions-vs-build-sdk)。</span><span class="sxs-lookup"><span data-stu-id="3464d-125">hello source is available in hello GitHub repo [azure\-functions\-vs\-build\-sdk](https://github.com/Azure/azure-functions-vs-build-sdk).</span></span>

## <a name="triggers-and-bindings"></a><span data-ttu-id="3464d-126">觸發和繫結</span><span class="sxs-lookup"><span data-stu-id="3464d-126">Triggers and bindings</span></span>

<span data-ttu-id="3464d-127">hello 下表列出 hello 觸發程序和 Azure 函式的類別庫專案中可用的繫結。</span><span class="sxs-lookup"><span data-stu-id="3464d-127">hello following table lists hello triggers and bindings that are available in an Azure Functions class library project.</span></span> <span data-ttu-id="3464d-128">Hello 命名空間中的所有屬性都是`Microsoft.Azure.WebJobs`。</span><span class="sxs-lookup"><span data-stu-id="3464d-128">All attributes are in hello namespace `Microsoft.Azure.WebJobs`.</span></span>

| <span data-ttu-id="3464d-129">繫結</span><span class="sxs-lookup"><span data-stu-id="3464d-129">Binding</span></span> | <span data-ttu-id="3464d-130">屬性</span><span class="sxs-lookup"><span data-stu-id="3464d-130">Attribute</span></span> | <span data-ttu-id="3464d-131">Nuget 套件</span><span class="sxs-lookup"><span data-stu-id="3464d-131">NuGet package</span></span> |
|------   | ------    | ------        |
| [<span data-ttu-id="3464d-132">Blob 儲存體觸發程序, 輸入, 輸出</span><span class="sxs-lookup"><span data-stu-id="3464d-132">Blob storage trigger, input, output</span></span>](#blob-storage) | <span data-ttu-id="3464d-133">[BlobAttribute], [StorageAccountAttribute]</span><span class="sxs-lookup"><span data-stu-id="3464d-133">[BlobAttribute], [StorageAccountAttribute]</span></span> | <span data-ttu-id="3464d-134">[Microsoft.Azure.WebJobs]</span><span class="sxs-lookup"><span data-stu-id="3464d-134">[Microsoft.Azure.WebJobs]</span></span> | <span data-ttu-id="3464d-135">[Blob 儲存體]</span><span class="sxs-lookup"><span data-stu-id="3464d-135">[Blob storage]</span></span> |
| [<span data-ttu-id="3464d-136">Cosmos DB 輸入和輸出繫結</span><span class="sxs-lookup"><span data-stu-id="3464d-136">Cosmos DB input and output binding</span></span>](#cosmos-db) | <span data-ttu-id="3464d-137">[DocumentDBAttribute]</span><span class="sxs-lookup"><span data-stu-id="3464d-137">[DocumentDBAttribute]</span></span> | <span data-ttu-id="3464d-138">[Microsoft.Azure.WebJobs.Extensions.DocumentDB]</span><span class="sxs-lookup"><span data-stu-id="3464d-138">[Microsoft.Azure.WebJobs.Extensions.DocumentDB]</span></span> | 
| [<span data-ttu-id="3464d-139">事件中心觸發程序和輸出</span><span class="sxs-lookup"><span data-stu-id="3464d-139">Event Hubs trigger and output</span></span>](#event-hub) | <span data-ttu-id="3464d-140">[EventHubTriggerAttribute], [EventHubAttribute]</span><span class="sxs-lookup"><span data-stu-id="3464d-140">[EventHubTriggerAttribute], [EventHubAttribute]</span></span> | <span data-ttu-id="3464d-141">[Microsoft.Azure.WebJobs.ServiceBus]</span><span class="sxs-lookup"><span data-stu-id="3464d-141">[Microsoft.Azure.WebJobs.ServiceBus]</span></span> |
| [<span data-ttu-id="3464d-142">外部檔案輸入和輸出</span><span class="sxs-lookup"><span data-stu-id="3464d-142">External file input and output</span></span>](#api-hub) | <span data-ttu-id="3464d-143">[ApiHubFileAttribute]</span><span class="sxs-lookup"><span data-stu-id="3464d-143">[ApiHubFileAttribute]</span></span> | <span data-ttu-id="3464d-144">[Microsoft.Azure.WebJobs.Extensions.ApiHub]</span><span class="sxs-lookup"><span data-stu-id="3464d-144">[Microsoft.Azure.WebJobs.Extensions.ApiHub]</span></span> |
| [<span data-ttu-id="3464d-145">HTTP 和 Webhook 觸發程序</span><span class="sxs-lookup"><span data-stu-id="3464d-145">HTTP and webhook trigger</span></span>](#http) | <span data-ttu-id="3464d-146">[HttpTriggerAttribute]</span><span class="sxs-lookup"><span data-stu-id="3464d-146">[HttpTriggerAttribute]</span></span> | <span data-ttu-id="3464d-147">[Microsoft.Azure.WebJobs.Extensions.Http]</span><span class="sxs-lookup"><span data-stu-id="3464d-147">[Microsoft.Azure.WebJobs.Extensions.Http]</span></span> |
| [<span data-ttu-id="3464d-148">Mobile Apps 輸入和輸出</span><span class="sxs-lookup"><span data-stu-id="3464d-148">Mobile Apps input and output</span></span>](#mobile-apps) | <span data-ttu-id="3464d-149">[MobileTableAttribute]</span><span class="sxs-lookup"><span data-stu-id="3464d-149">[MobileTableAttribute]</span></span> | <span data-ttu-id="3464d-150">[Microsoft.Azure.WebJobs.Extensions.MobileApps]</span><span class="sxs-lookup"><span data-stu-id="3464d-150">[Microsoft.Azure.WebJobs.Extensions.MobileApps]</span></span> | 
| [<span data-ttu-id="3464d-151">通知中樞輸出</span><span class="sxs-lookup"><span data-stu-id="3464d-151">Notification Hubs output</span></span>](#nh) | <span data-ttu-id="3464d-152">[NotificationHubAttribute]</span><span class="sxs-lookup"><span data-stu-id="3464d-152">[NotificationHubAttribute]</span></span> | <span data-ttu-id="3464d-153">[Microsoft.Azure.WebJobs.Extensions.NotificationHubs]</span><span class="sxs-lookup"><span data-stu-id="3464d-153">[Microsoft.Azure.WebJobs.Extensions.NotificationHubs]</span></span> | 
| [<span data-ttu-id="3464d-154">佇列儲存體觸發程序和輸出</span><span class="sxs-lookup"><span data-stu-id="3464d-154">Queue storage trigger and output</span></span>](#queue) | <span data-ttu-id="3464d-155">[QueueAttribute], [StorageAccountAttribute]</span><span class="sxs-lookup"><span data-stu-id="3464d-155">[QueueAttribute], [StorageAccountAttribute]</span></span> | <span data-ttu-id="3464d-156">[Microsoft.Azure.WebJobs]</span><span class="sxs-lookup"><span data-stu-id="3464d-156">[Microsoft.Azure.WebJobs]</span></span> | 
| [<span data-ttu-id="3464d-157">SendGrid 輸出</span><span class="sxs-lookup"><span data-stu-id="3464d-157">SendGrid output</span></span>](#sendgrid) | <span data-ttu-id="3464d-158">[SendGridAttribute]</span><span class="sxs-lookup"><span data-stu-id="3464d-158">[SendGridAttribute]</span></span> | <span data-ttu-id="3464d-159">[Microsoft.Azure.WebJobs.Extensions.SendGrid]</span><span class="sxs-lookup"><span data-stu-id="3464d-159">[Microsoft.Azure.WebJobs.Extensions.SendGrid]</span></span> | 
| [<span data-ttu-id="3464d-160">服務匯流排觸發程序和輸出</span><span class="sxs-lookup"><span data-stu-id="3464d-160">Service Bus trigger and output</span></span>](#service-bus) | <span data-ttu-id="3464d-161">[ServiceBusAttribute], [ServiceBusAccountAttribute]</span><span class="sxs-lookup"><span data-stu-id="3464d-161">[ServiceBusAttribute], [ServiceBusAccountAttribute]</span></span> | <span data-ttu-id="3464d-162">[Microsoft.Azure.WebJobs.ServiceBus]</span><span class="sxs-lookup"><span data-stu-id="3464d-162">[Microsoft.Azure.WebJobs.ServiceBus]</span></span>
| [<span data-ttu-id="3464d-163">資料表儲存體輸入和輸出</span><span class="sxs-lookup"><span data-stu-id="3464d-163">Table storage input and output</span></span>](#table) | <span data-ttu-id="3464d-164">[TableAttribute], [StorageAccountAttribute]</span><span class="sxs-lookup"><span data-stu-id="3464d-164">[TableAttribute], [StorageAccountAttribute]</span></span> | <span data-ttu-id="3464d-165">[Microsoft.Azure.WebJobs]</span><span class="sxs-lookup"><span data-stu-id="3464d-165">[Microsoft.Azure.WebJobs]</span></span> | 
| [<span data-ttu-id="3464d-166">計時器觸發程序</span><span class="sxs-lookup"><span data-stu-id="3464d-166">Timer trigger</span></span>](#timer) | <span data-ttu-id="3464d-167">[TimerTriggerAttribute]</span><span class="sxs-lookup"><span data-stu-id="3464d-167">[TimerTriggerAttribute]</span></span> | <span data-ttu-id="3464d-168">[Microsoft.Azure.WebJobs.Extensions]</span><span class="sxs-lookup"><span data-stu-id="3464d-168">[Microsoft.Azure.WebJobs.Extensions]</span></span> | 
| [<span data-ttu-id="3464d-169">Twilio 輸出</span><span class="sxs-lookup"><span data-stu-id="3464d-169">Twilio output</span></span>](#twilio) | <span data-ttu-id="3464d-170">[TwilioSmsAttribute]</span><span class="sxs-lookup"><span data-stu-id="3464d-170">[TwilioSmsAttribute]</span></span> | <span data-ttu-id="3464d-171">[Microsoft.Azure.WebJobs.Extensions.Twilio]</span><span class="sxs-lookup"><span data-stu-id="3464d-171">[Microsoft.Azure.WebJobs.Extensions.Twilio]</span></span> | 

<a name="blob-storage"></a>

### <a name="blob-storage-trigger-input-and-output-bindings"></a><span data-ttu-id="3464d-172">Blob 儲存體觸發程序、輸入和輸出繫結</span><span class="sxs-lookup"><span data-stu-id="3464d-172">Blob storage trigger, input, and output bindings</span></span>

<span data-ttu-id="3464d-173">Azure Functions 支援適用於 Azure Blob 儲存體的觸發程序、輸入和輸出繫結。</span><span class="sxs-lookup"><span data-stu-id="3464d-173">Azure Functions supports trigger, input, and output bindings for Azure Blob storage.</span></span> <span data-ttu-id="3464d-174">如需有關繫結運算式和中繼資料的詳細資訊，請參閱 [Azure Functions Blob 儲存體繫結](functions-bindings-storage-blob.md)。</span><span class="sxs-lookup"><span data-stu-id="3464d-174">For more information on binding expressions and metadata, see [Azure Functions Blob storage bindings](functions-bindings-storage-blob.md).</span></span>

<span data-ttu-id="3464d-175">Blob 的觸發程序定義以 hello`[BlobTrigger]`屬性。</span><span class="sxs-lookup"><span data-stu-id="3464d-175">A blob trigger is defined with hello `[BlobTrigger]` attribute.</span></span> <span data-ttu-id="3464d-176">您可以使用 hello 屬性`[StorageAccount]`toodefine hello 儲存體帳戶所使用的整個函式或類別。</span><span class="sxs-lookup"><span data-stu-id="3464d-176">You can use hello attribute `[StorageAccount]` toodefine hello storage account that is used by an entire function or class.</span></span>

```csharp
[StorageAccount("AzureWebJobsStorage")]
[FunctionName("BlobTriggerCSharp")]        
public static void Run([BlobTrigger("samples-workitems/{name}")] Stream myBlob, string name, TraceWriter log)
{
    log.Info($"C# Blob trigger function Processed blob\n Name:{name} \n Size: {myBlob.Length} Bytes");
}
```

<span data-ttu-id="3464d-177">Blob 輸入和輸出定義使用 hello`[Blob]`屬性，以及與`FileAccess`參數，表示讀取或寫入。</span><span class="sxs-lookup"><span data-stu-id="3464d-177">Blob input and output are defined using hello `[Blob]` attribute, along with a `FileAccess` parameter indicating read or write.</span></span> <span data-ttu-id="3464d-178">下列範例會使用 hello blob 觸發程序和 blob 輸出繫結。</span><span class="sxs-lookup"><span data-stu-id="3464d-178">hello following example uses a blob trigger and blob output binding.</span></span>

```csharp
[FunctionName("ResizeImage")]
[StorageAccount("AzureWebJobsStorage")]
public static void Run(
    [BlobTrigger("sample-images/{name}")] Stream image, 
    [Blob("sample-images-sm/{name}", FileAccess.Write)] Stream imageSmall, 
    [Blob("sample-images-md/{name}", FileAccess.Write)] Stream imageMedium)
{
    var imageBuilder = ImageResizer.ImageBuilder.Current;
    var size = imageDimensionsTable[ImageSize.Small];

    imageBuilder.Build(image, imageSmall,
        new ResizeSettings(size.Item1, size.Item2, FitMode.Max, null), false);

    image.Position = 0;
    size = imageDimensionsTable[ImageSize.Medium];

    imageBuilder.Build(image, imageMedium,
        new ResizeSettings(size.Item1, size.Item2, FitMode.Max, null), false);
}

public enum ImageSize { ExtraSmall, Small, Medium }

private static Dictionary<ImageSize, (int, int)> imageDimensionsTable = new Dictionary<ImageSize, (int, int)>() {
    { ImageSize.ExtraSmall, (320, 200) },
    { ImageSize.Small,      (640, 400) },
    { ImageSize.Medium,     (800, 600) }
};
```        

<a name="cosmos-db"></a>

### <a name="cosmos-db-input-and-output-bindings"></a><span data-ttu-id="3464d-179">Cosmos DB 輸入和輸出繫結</span><span class="sxs-lookup"><span data-stu-id="3464d-179">Cosmos DB input and output bindings</span></span>

<span data-ttu-id="3464d-180">Azure Functions 支援 Cosmos DB 的輸入和輸出繫結。</span><span class="sxs-lookup"><span data-stu-id="3464d-180">Azure Functions supports input and output bindings for Cosmos DB.</span></span> <span data-ttu-id="3464d-181">toolearn hello 功能 hello Cosmos DB，繫結的詳細資料請參閱[Azure 函式 Cosmos DB 繫結](functions-bindings-documentdb.md)。</span><span class="sxs-lookup"><span data-stu-id="3464d-181">toolearn more about hello features of hello Cosmos DB binding, see [Azure Functions Cosmos DB bindings](functions-bindings-documentdb.md).</span></span>

<span data-ttu-id="3464d-182">toobind tooa Cosmos DB 文件中，使用 hello 屬性`[DocumentDB]`hello NuGet 封裝中[Microsoft.Azure.WebJobs.Extensions.DocumentDB]。</span><span class="sxs-lookup"><span data-stu-id="3464d-182">toobind tooa Cosmos DB document, use hello attribute `[DocumentDB]` in hello NuGet package [Microsoft.Azure.WebJobs.Extensions.DocumentDB].</span></span> <span data-ttu-id="3464d-183">下列範例中的 hello 具有佇列觸發程序和輸出繫結 DocumentDB API:</span><span class="sxs-lookup"><span data-stu-id="3464d-183">hello following example has a queue trigger and a DocumentDB API output binding:</span></span>

```csharp
[FunctionName("QueueToDocDB")]        
public static void Run(
    [QueueTrigger("myqueue-items", Connection = "AzureWebJobsStorage")] string myQueueItem, 
    [DocumentDB("ToDoList", "Items", ConnectionStringSetting = "DocDBConnection")] out dynamic document)
{
    document = new { Text = myQueueItem, id = Guid.NewGuid() };
}

```

<a name="event-hub"></a>

### <a name="event-hubs-trigger-and-output"></a><span data-ttu-id="3464d-184">事件中心觸發程序和輸出</span><span class="sxs-lookup"><span data-stu-id="3464d-184">Event Hubs trigger and output</span></span>

<span data-ttu-id="3464d-185">Azure Functions 支援事件中樞的觸發程序和輸出繫結。</span><span class="sxs-lookup"><span data-stu-id="3464d-185">Azure Functions supports trigger and output bindings for Event Hubs.</span></span> <span data-ttu-id="3464d-186">如需詳細資訊，請參閱 [Azure Functions 事件中樞繫結](functions-bindings-event-hubs.md)。</span><span class="sxs-lookup"><span data-stu-id="3464d-186">For more information, see  [Azure Functions Event Hub bindings](functions-bindings-event-hubs.md).</span></span>

<span data-ttu-id="3464d-187">hello 類型`[Microsoft.Azure.WebJobs.ServiceBus.EventHubTriggerAttribute]`和`[Microsoft.Azure.WebJobs.ServiceBus.EventHubAttribute]`hello NuGet 封裝中定義[Microsoft.Azure.WebJobs.ServiceBus]。</span><span class="sxs-lookup"><span data-stu-id="3464d-187">hello types `[Microsoft.Azure.WebJobs.ServiceBus.EventHubTriggerAttribute]` and `[Microsoft.Azure.WebJobs.ServiceBus.EventHubAttribute]` are defined in hello NuGet package [Microsoft.Azure.WebJobs.ServiceBus].</span></span> 

<span data-ttu-id="3464d-188">hello 下列範例會使用事件中心觸發程序：</span><span class="sxs-lookup"><span data-stu-id="3464d-188">hello following example uses an Event Hub trigger:</span></span>

```csharp
[FunctionName("EventHubTriggerCSharp")]
public static void Run([EventHubTrigger("samples-workitems", Connection = "EventHubConnection")] string myEventHubMessage, TraceWriter log)
{
    log.Info($"C# Event Hub trigger function processed a message: {myEventHubMessage}");
}
```

<span data-ttu-id="3464d-189">hello 下列範例包含事件中心輸出時，使用 hello 方法的傳回值為 hello 輸出：</span><span class="sxs-lookup"><span data-stu-id="3464d-189">hello following example has an Event Hub output, using hello method return value as hello output:</span></span>

```csharp
[FunctionName("EventHubOutput")]
[return: EventHub("outputEventHubMessage", Connection = "EventHubConnection")]
public static string Run([TimerTrigger("0 */5 * * * *")] TimerInfo myTimer, TraceWriter log)
{
    log.Info($"C# Timer trigger function executed at: {DateTime.Now}");
    return $"{DateTime.Now}";
}
```

<a name="api-hub"></a>

### <a name="external-file-input-and-output"></a><span data-ttu-id="3464d-190">外部檔案輸入和輸出</span><span class="sxs-lookup"><span data-stu-id="3464d-190">External file input and output</span></span>

<span data-ttu-id="3464d-191">Azure Functions 支援適用於外部檔案 (例如 Google Drive、Dropbox 和 OneDrive) 的觸發程序、輸入和輸出繫結。</span><span class="sxs-lookup"><span data-stu-id="3464d-191">Azure Functions supports trigger, input, and output bindings for external files, such as Google Drive, Dropbox, and OneDrive.</span></span> <span data-ttu-id="3464d-192">詳細資訊，請參閱 toolearn [Azure 函式的外部檔案繫結](functions-bindings-external-file.md)。</span><span class="sxs-lookup"><span data-stu-id="3464d-192">toolearn more, see [Azure Functions External File bindings](functions-bindings-external-file.md).</span></span> <span data-ttu-id="3464d-193">hello 屬性`[ExternalFileTrigger]`和`[ExternalFile]`hello NuGet 封裝中定義[Microsoft.Azure.WebJobs.Extensions.ApiHub]。</span><span class="sxs-lookup"><span data-stu-id="3464d-193">hello attributes `[ExternalFileTrigger]` and `[ExternalFile]` are defined in hello NuGet package [Microsoft.Azure.WebJobs.Extensions.ApiHub].</span></span>

<span data-ttu-id="3464d-194">hello 下列 C# 範例示範外部檔案輸入和輸出繫結。</span><span class="sxs-lookup"><span data-stu-id="3464d-194">hello following C# example demonstrates an external file input and output binding.</span></span> <span data-ttu-id="3464d-195">hello 程式碼複製 hello 輸入的檔 toohello 輸出檔。</span><span class="sxs-lookup"><span data-stu-id="3464d-195">hello code copies hello input file toohello output file.</span></span>

```csharp
[StorageAccount("MyStorageConnection")]
[FunctionName("ExternalFile")]
[return: ApiHubFile("MyFileConnection", "samples-workitems/{queueTrigger}-Copy", FileAccess.Write)]
public static string Run([QueueTrigger("myqueue-items")] string myQueueItem, 
    [ApiHubFile("MyFileConnection", "samples-workitems/{queueTrigger}", FileAccess.Read)] string myInputFile, 
    TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");
    return myInputFile;
}
```

<a name="http"></a>

### <a name="http-and-webhooks"></a><span data-ttu-id="3464d-196">HTTP 和 Webhook</span><span class="sxs-lookup"><span data-stu-id="3464d-196">HTTP and webhooks</span></span>

<span data-ttu-id="3464d-197">使用 hello`HttpTrigger`屬性 toodefine HTTP 觸發程序或 webhook。</span><span class="sxs-lookup"><span data-stu-id="3464d-197">Use hello `HttpTrigger` attribute toodefine an HTTP trigger or webhook.</span></span> <span data-ttu-id="3464d-198">這個屬性定義在 hello NuGet 封裝[Microsoft.Azure.WebJobs.Extensions.Http]。</span><span class="sxs-lookup"><span data-stu-id="3464d-198">This attribute is defined in hello NuGet package [Microsoft.Azure.WebJobs.Extensions.Http].</span></span> <span data-ttu-id="3464d-199">您可以自訂 hello 授權層級、 webhook 類型、 route 和方法。</span><span class="sxs-lookup"><span data-stu-id="3464d-199">You can customize hello authorization level, webhook type, route, and methods.</span></span> <span data-ttu-id="3464d-200">hello 下列範例會定義匿名驗證的 HTTP 觸發程序和_genericJson_ webhook 型別。</span><span class="sxs-lookup"><span data-stu-id="3464d-200">hello following example defines an HTTP trigger with anonymous authentication and _genericJson_ webhook type.</span></span>

```csharp
[FunctionName("HttpTriggerCSharp")]
public static HttpResponseMessage Run([HttpTrigger(AuthorizationLevel.Anonymous, WebHookType = "genericJson")] HttpRequestMessage req)
{
    return req.CreateResponse(HttpStatusCode.OK);
}
```

<a name="mobile-apps"></a>

### <a name="mobile-apps-input-and-output"></a><span data-ttu-id="3464d-201">Mobile Apps 輸入和輸出</span><span class="sxs-lookup"><span data-stu-id="3464d-201">Mobile Apps input and output</span></span>

<span data-ttu-id="3464d-202">Azure Functions 支援 Mobile Apps 的輸入和輸出繫結。</span><span class="sxs-lookup"><span data-stu-id="3464d-202">Azure Functions supports input and output bindings for Mobile Apps.</span></span> <span data-ttu-id="3464d-203">詳細資訊，請參閱 toolearn [Azure 函式行動應用程式繫結](functions-bindings-mobile-apps.md)。</span><span class="sxs-lookup"><span data-stu-id="3464d-203">toolearn more, see [Azure Functions Mobile Apps bindings](functions-bindings-mobile-apps.md).</span></span> <span data-ttu-id="3464d-204">hello 屬性`[MobileTable]`hello NuGet 封裝中定義[Microsoft.Azure.WebJobs.Extensions.MobileApps]。</span><span class="sxs-lookup"><span data-stu-id="3464d-204">hello attribute `[MobileTable]` is defined in hello NuGet package [Microsoft.Azure.WebJobs.Extensions.MobileApps].</span></span>

<span data-ttu-id="3464d-205">hello 下列範例會示範行動應用程式輸出繫結：</span><span class="sxs-lookup"><span data-stu-id="3464d-205">hello following example demonstrates a Mobile Apps output binding:</span></span>

```csharp
[FunctionName("MobileAppsOutput")]        
[return: MobileTable(ApiKeySetting = "MyMobileAppKey", TableName = "MyTable", MobileAppUriSetting = "MyMobileAppUri")]
public static object Run([QueueTrigger("myqueue-items", Connection = "AzureWebJobsStorage")] string myQueueItem, TraceWriter log)
{
    return new { Text = $"I'm running in a C# function! {myQueueItem}" };
}
```

<a name="nh"></a>

### <a name="notification-hubs-output"></a><span data-ttu-id="3464d-206">通知中樞輸出</span><span class="sxs-lookup"><span data-stu-id="3464d-206">Notification Hubs output</span></span>

<span data-ttu-id="3464d-207">Azure Functions 會支援通知中樞的輸出繫結。</span><span class="sxs-lookup"><span data-stu-id="3464d-207">Azure Functions supports an output binding for Notification Hubs.</span></span> <span data-ttu-id="3464d-208">詳細資訊，請參閱 toolearn [Azure 函式的通知中樞輸出繫結](functions-bindings-notification-hubs.md)。</span><span class="sxs-lookup"><span data-stu-id="3464d-208">toolearn more, see [Azure Functions Notification Hub output binding](functions-bindings-notification-hubs.md).</span></span> <span data-ttu-id="3464d-209">hello 屬性`[NotificationHub]`hello NuGet 封裝中定義[Microsoft.Azure.WebJobs.Extensions.NotificationHubs]。</span><span class="sxs-lookup"><span data-stu-id="3464d-209">hello attribute `[NotificationHub]` is defined in hello NuGet package [Microsoft.Azure.WebJobs.Extensions.NotificationHubs].</span></span>

<a name="queue"></a>

### <a name="queue-storage-trigger-and-output"></a><span data-ttu-id="3464d-210">佇列儲存體觸發程序和輸出</span><span class="sxs-lookup"><span data-stu-id="3464d-210">Queue storage trigger and output</span></span>

<span data-ttu-id="3464d-211">Azure Functions 支援適用於 Azure 佇列的觸發程序和輸出繫結。</span><span class="sxs-lookup"><span data-stu-id="3464d-211">Azure Functions supports trigger and output bindings for Azure queues.</span></span> <span data-ttu-id="3464d-212">如需詳細資訊，請參閱 [Azure Functions 佇列儲存體繫結](functions-bindings-storage-queue.md)。</span><span class="sxs-lookup"><span data-stu-id="3464d-212">For more information, see [Azure Functions Queue Storage bindings](functions-bindings-storage-queue.md).</span></span>

<span data-ttu-id="3464d-213">hello 下列範例示範如何 toouse hello 函式傳回型別具有佇列輸出繫結、 使用 hello`[Queue]`屬性。</span><span class="sxs-lookup"><span data-stu-id="3464d-213">hello following example shows how toouse hello function return type with a queue output binding, using hello `[Queue]` attribute.</span></span> <span data-ttu-id="3464d-214">toodefine 佇列觸發程序，使用 hello`[QueueTrigger]`屬性。</span><span class="sxs-lookup"><span data-stu-id="3464d-214">toodefine a queue trigger, use hello `[QueueTrigger]` attribute.</span></span>

```csharp
[StorageAccount("AzureWebJobsStorage")]
public static class QueueFunctions
{
    // HTTP trigger with queue output binding
    [FunctionName("QueueOutput")]
    [return: Queue("myqueue-items")]
    public static string QueueOutput([HttpTrigger] dynamic input,  TraceWriter log)
    {
        log.Info($"C# function processed: {input.Text}");
        return input.Text;
    }

    // Queue trigger
    [FunctionName("QueueTrigger")]
    [StorageAccount("AzureWebJobsStorage")]
    public static void QueueTrigger([QueueTrigger("myqueue-items")] string myQueueItem, TraceWriter log)
    {
        log.Info($"C# function processed: {myQueueItem}");
    }
}

```

<a name="sendgrid"></a>

### <a name="sendgrid-output"></a><span data-ttu-id="3464d-215">SendGrid 輸出</span><span class="sxs-lookup"><span data-stu-id="3464d-215">SendGrid output</span></span>

<span data-ttu-id="3464d-216">Azure Functions 支援用於以程式設計方式傳送電子郵件的 SendGrid 輸出繫結。</span><span class="sxs-lookup"><span data-stu-id="3464d-216">Azure Functions supports a SendGrid output binding for sending email programmatically.</span></span> <span data-ttu-id="3464d-217">詳細資訊，請參閱 toolearn [Azure 函式 SendGrid 繫結](functions-bindings-sendgrid.md)。</span><span class="sxs-lookup"><span data-stu-id="3464d-217">toolearn more, see [Azure Functions SendGrid bindings](functions-bindings-sendgrid.md).</span></span>

<span data-ttu-id="3464d-218">hello 屬性`[SendGrid]`hello NuGet 封裝中定義[Microsoft.Azure.WebJobs.Extensions.SendGrid]。</span><span class="sxs-lookup"><span data-stu-id="3464d-218">hello attribute `[SendGrid]` is defined in hello NuGet package [Microsoft.Azure.WebJobs.Extensions.SendGrid].</span></span>

<span data-ttu-id="3464d-219">hello 以下是使用服務匯流排佇列觸發程序和 SendGrid 輸出繫結使用的範例`SendGridMessage`:</span><span class="sxs-lookup"><span data-stu-id="3464d-219">hello following is an example of using a Service Bus queue trigger and a SendGrid output binding using `SendGridMessage`:</span></span>

```csharp
[FunctionName("SendEmail")]
public static void Run(
    [ServiceBusTrigger("myqueue", AccessRights.Manage, Connection = "ServiceBusConnection")] OutgoingEmail email,
    [SendGrid] out SendGridMessage message)
{
    message = new SendGridMessage();
    message.AddTo(email.To);
    message.AddContent("text/html", email.Body);
    message.SetFrom(new EmailAddress(email.From));
    message.SetSubject(email.Subject);
}

public class OutgoingEmail
{
    public string too{ get; set; }
    public string From { get; set; }
    public string Subject { get; set; }
    public string Body { get; set; }
}
```

<a name="service-bus"></a>

### <a name="service-bus-trigger-and-output"></a><span data-ttu-id="3464d-220">服務匯流排觸發程序和輸出</span><span class="sxs-lookup"><span data-stu-id="3464d-220">Service Bus trigger and output</span></span>

<span data-ttu-id="3464d-221">Azure Functions 支援服務匯流排佇列和主題的觸發程序和輸出繫結。</span><span class="sxs-lookup"><span data-stu-id="3464d-221">Azure Functions supports trigger and output bindings for Service Bus queues and topics.</span></span> <span data-ttu-id="3464d-222">如需有關如何設定繫結的詳細資訊，請參閱 [Azure Functions 服務匯流排繫結](functions-bindings-service-bus.md)。</span><span class="sxs-lookup"><span data-stu-id="3464d-222">For more information on configuring bindings, see [Azure Functions Service Bus bindings](functions-bindings-service-bus.md).</span></span>

<span data-ttu-id="3464d-223">hello 屬性`[ServiceBusTrigger]`和`[ServiceBus]`hello NuGet 封裝中定義[Microsoft.Azure.WebJobs.ServiceBus]。</span><span class="sxs-lookup"><span data-stu-id="3464d-223">hello attributes `[ServiceBusTrigger]` and `[ServiceBus]` are defined in hello NuGet package [Microsoft.Azure.WebJobs.ServiceBus].</span></span> 

<span data-ttu-id="3464d-224">hello 下列是服務匯流排佇列觸發程序的範例：</span><span class="sxs-lookup"><span data-stu-id="3464d-224">hello following is an example of a Service Bus queue trigger:</span></span>

```csharp
[FunctionName("ServiceBusQueueTriggerCSharp")]                    
public static void Run([ServiceBusTrigger("myqueue", AccessRights.Manage, Connection = "ServiceBusConnection")] string myQueueItem, TraceWriter log)
{
    log.Info($"C# ServiceBus queue trigger function processed message: {myQueueItem}");
}
```

<span data-ttu-id="3464d-225">hello 下列是服務匯流排輸出繫結、 使用 hello 方法的傳回型別做為 hello 輸出的範例：</span><span class="sxs-lookup"><span data-stu-id="3464d-225">hello following is an example of a Service Bus output binding, using hello method return type as hello output:</span></span>

```csharp
[FunctionName("ServiceBusOutput")]
[return: ServiceBus("myqueue", Connection = "ServiceBusConnection")]
public static string ServiceBusOutput([HttpTrigger] dynamic input, TraceWriter log)
{
    log.Info($"C# function processed: {input.Text}");
    return input.Text;
}
```        

<a name="table"></a>

### <a name="table-storage-input-and-output"></a><span data-ttu-id="3464d-226">資料表儲存體輸入和輸出</span><span class="sxs-lookup"><span data-stu-id="3464d-226">Table storage input and output</span></span>

<span data-ttu-id="3464d-227">Azure Functions 支援 Azure 資料表儲存體的輸入和輸出繫結。</span><span class="sxs-lookup"><span data-stu-id="3464d-227">Azure Functions supports input and output bindings for Azure Table storage.</span></span> <span data-ttu-id="3464d-228">詳細資訊，請參閱 toolearn [Azure 函式的資料表儲存體繫結](functions-bindings-storage-table.md)。</span><span class="sxs-lookup"><span data-stu-id="3464d-228">toolearn more, see [Azure Functions Table storage bindings](functions-bindings-storage-table.md).</span></span>

<span data-ttu-id="3464d-229">hello 下列範例是具有兩個函式，示範資料表儲存體輸出和輸入的繫結的類別。</span><span class="sxs-lookup"><span data-stu-id="3464d-229">hello following example is a class with two functions, demonstrating table storage output and input bindings.</span></span> 

```csharp
[StorageAccount("AzureWebJobsStorage")]
public class TableStorage
{
    public class MyPoco
    {
        public string PartitionKey { get; set; }
        public string RowKey { get; set; }
        public string Text { get; set; }
    }

    [FunctionName("TableOutput")]
    [return: Table("MyTable")]
    public static MyPoco TableOutput([HttpTrigger] dynamic input, TraceWriter log)
    {
        log.Info($"C# http trigger function processed: {input.Text}");
        return new MyPoco { PartitionKey = "Http", RowKey = Guid.NewGuid().ToString(), Text = input.Text };
    }

    // use hello metadata parameter "queueTrigger" toobind hello queue payload
    [FunctionName("TableInput")]
    public static void TableInput([QueueTrigger("table-items")] string input, [Table("MyTable", "Http", "{queueTrigger}")] MyPoco poco, TraceWriter log)
    {
        log.Info($"C# function processed: {poco.Text}");
    }
}

```

<a name="timer"></a>

### <a name="timer-trigger"></a><span data-ttu-id="3464d-230">計時器觸發程序</span><span class="sxs-lookup"><span data-stu-id="3464d-230">Timer trigger</span></span>

<span data-ttu-id="3464d-231">Azure Functions 具有計時器觸發程序繫結，可讓您根據所定義的排程執行函式程式碼。</span><span class="sxs-lookup"><span data-stu-id="3464d-231">Azure Functions has a timer trigger binding that lets you run your function code based on a defined schedule.</span></span> <span data-ttu-id="3464d-232">toolearn hello 功能，hello 繫結的詳細資料請參閱[排程與 Azure 函式的程式碼執行](functions-bindings-timer.md)。</span><span class="sxs-lookup"><span data-stu-id="3464d-232">toolearn more about hello features of hello binding, see [Schedule code execution with Azure Functions](functions-bindings-timer.md).</span></span>

<span data-ttu-id="3464d-233">在 hello 耗用量計劃，您可以定義排程與[CRON 運算式](http://en.wikipedia.org/wiki/Cron#CRON_expression)。</span><span class="sxs-lookup"><span data-stu-id="3464d-233">On hello Consumption plan, you can define schedules with a [CRON expression](http://en.wikipedia.org/wiki/Cron#CRON_expression).</span></span> <span data-ttu-id="3464d-234">如果您是使用 App Service 方案，也可以使用 TimeSpan 字串。</span><span class="sxs-lookup"><span data-stu-id="3464d-234">If you're using an App Service Plan, you can also use a TimeSpan string.</span></span> 

<span data-ttu-id="3464d-235">下列範例中的 hello 定義執行每隔 5 分鐘的計時器觸發程序：</span><span class="sxs-lookup"><span data-stu-id="3464d-235">hello following example defines a timer trigger that runs every 5 minutes:</span></span>

```csharp
[FunctionName("TimerTriggerCSharp")]
public static void Run([TimerTrigger("0 */5 * * * *")]TimerInfo myTimer, TraceWriter log)
{
    log.Info($"C# Timer trigger function executed at: {DateTime.Now}");
}
```

<a name="twilio"></a>

### <a name="twilio-output"></a><span data-ttu-id="3464d-236">Twilio 輸出</span><span class="sxs-lookup"><span data-stu-id="3464d-236">Twilio output</span></span>

<span data-ttu-id="3464d-237">Azure 函式支援 Twilio 輸出繫結 tooenable 函式 toosend SMS 文字訊息。</span><span class="sxs-lookup"><span data-stu-id="3464d-237">Azure Functions supports Twilio output bindings tooenable your functions toosend SMS text messages.</span></span> <span data-ttu-id="3464d-238">詳細資訊，請參閱 toolearn[傳送 SMS 訊息使用 hello Twilio Azure 函式的輸出繫結](functions-bindings-twilio.md)。</span><span class="sxs-lookup"><span data-stu-id="3464d-238">toolearn more, see [Send SMS messages from Azure Functions using hello Twilio output binding](functions-bindings-twilio.md).</span></span> 

<span data-ttu-id="3464d-239">hello 屬性`[TwilioSms]`hello 封裝中定義[Microsoft.Azure.WebJobs.Extensions.Twilio]。</span><span class="sxs-lookup"><span data-stu-id="3464d-239">hello attribute `[TwilioSms]` is defined in hello package [Microsoft.Azure.WebJobs.Extensions.Twilio].</span></span>

<span data-ttu-id="3464d-240">hello 下列 C# 範例會使用佇列觸發程序和 Twilio 輸出繫結：</span><span class="sxs-lookup"><span data-stu-id="3464d-240">hello following C# example uses a queue trigger and a Twilio output binding:</span></span>

```csharp
[FunctionName("QueueTwilio")]
[return: TwilioSms(AccountSidSetting = "TwilioAccountSid", AuthTokenSetting = "TwilioAuthToken", From = "+1425XXXXXXX" )]
public static SMSMessage Run([QueueTrigger("myqueue-items", Connection = "AzureWebJobsStorage")] JObject order, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {order}");

    var message = new SMSMessage()
    {
        Body = $"Hello {order["name"]}, thanks for your order!",
        too= order["mobileNumber"].ToString()
    };

    return message;
}
```

## <a name="next-steps"></a><span data-ttu-id="3464d-241">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3464d-241">Next steps</span></span>

<span data-ttu-id="3464d-242">如需有關如何在 C# 指令碼中使用 Azure Functions 的詳細資訊，請參閱 [Azure Functions C\# 指令碼開發人員參考](functions-reference-csharp.md)。</span><span class="sxs-lookup"><span data-stu-id="3464d-242">For more information on using Azure Functions in C# scripting, see [Azure Functions C\# script developer reference](functions-reference-csharp.md).</span></span>

[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]


<!-- NuGet packages --> 
[Microsoft.Azure.WebJobs]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs/2.1.0-beta1
[Microsoft.Azure.WebJobs.Extensions.DocumentDB]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.DocumentDB/1.1.0-beta1
[Microsoft.Azure.WebJobs.ServiceBus]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.ServiceBus/2.1.0-beta1
[Microsoft.Azure.WebJobs.Extensions.MobileApps]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.MobileApps/1.1.0-beta1
[Microsoft.Azure.WebJobs.Extensions.NotificationHubs]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.NotificationHubs/1.1.0-beta1
[Microsoft.Azure.WebJobs.ServiceBus]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.ServiceBus/2.1.0-beta1
[Microsoft.Azure.WebJobs.Extensions.SendGrid]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.SendGrid/2.1.0-beta1
[Microsoft.Azure.WebJobs.Extensions.Http]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.Http/1.0.0-beta1
[Microsoft.Azure.WebJobs.Extensions.BotFramework]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.BotFramework/1.0.15-beta
[Microsoft.Azure.WebJobs.Extensions.ApiHub]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.ApiHub/1.0.0-beta4
[Microsoft.Azure.WebJobs.Extensions.Twilio]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.Twilio/1.1.0-beta1
[Microsoft.Azure.WebJobs.Extensions]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions/2.1.0-beta1


<!-- Links toosource --> 
[DocumentDBAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.DocumentDB/DocumentDBAttribute.cs
[EventHubAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/EventHubs/EventHubAttribute.cs
[EventHubTriggerAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/EventHubs/EventHubTriggerAttribute.cs
[MobileTableAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.MobileApps/MobileTableAttribute.cs
[NotificationHubAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.NotificationHubs/NotificationHubAttribute.cs 
[ServiceBusAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAttribute.cs
[ServiceBusAccountAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAccountAttribute.cs
[QueueAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/QueueAttribute.cs
[StorageAccountAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs
[BlobAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/BlobAttribute.cs
[TableAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/TableAttribute.cs
[TwilioSmsAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.Twilio/TwilioSMSAttribute.cs
[SendGridAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.SendGrid/SendGridAttribute.cs
[HttpTriggerAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/dev/src/WebJobs.Extensions.Http/HttpTriggerAttribute.cs
[ApiHubFileAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.ApiHub/ApiHubFileAttribute.cs
[TimerTriggerAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions/Extensions/Timers/TimerTriggerAttribute.cs
