---
title: "使用 .NET 類別庫搭配 Azure Functions | Microsoft Docs"
description: "了解如何撰寫 .NET 類別庫來與 Azure Functions 搭配使用"
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
ms.openlocfilehash: 0613bb96d3afb85ff7e684246b128e4eef518d23
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="using-net-class-libraries-with-azure-functions"></a><span data-ttu-id="e7ecf-104">使用 .NET 類別庫搭配 Azure Functions</span><span class="sxs-lookup"><span data-stu-id="e7ecf-104">Using .NET class libraries with Azure Functions</span></span>

<span data-ttu-id="e7ecf-105">除了指令碼檔之外，Azure Functions 還支援發佈類別庫作為一個或多個函式的實作。</span><span class="sxs-lookup"><span data-stu-id="e7ecf-105">In addition to script files, Azure Functions supports publishing a class library as the implementation for one or more functions.</span></span> <span data-ttu-id="e7ecf-106">建議您使用 [Azure Functions Visual Studio 2017 Tools](https://blogs.msdn.microsoft.com/webdev/2017/05/10/azure-function-tools-for-visual-studio-2017/)。</span><span class="sxs-lookup"><span data-stu-id="e7ecf-106">We recommend that you use the [Azure Functions Visual Studio 2017 Tools](https://blogs.msdn.microsoft.com/webdev/2017/05/10/azure-function-tools-for-visual-studio-2017/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e7ecf-107">必要條件</span><span class="sxs-lookup"><span data-stu-id="e7ecf-107">Prerequisites</span></span> 

<span data-ttu-id="e7ecf-108">本文有下列先決條件：</span><span class="sxs-lookup"><span data-stu-id="e7ecf-108">This article has the following prerequisites:</span></span>

- <span data-ttu-id="e7ecf-109">[Visual Studio 2017 15.3 預覽](https://www.visualstudio.com/vs/preview/)。</span><span class="sxs-lookup"><span data-stu-id="e7ecf-109">[Visual Studio 2017 15.3 Preview](https://www.visualstudio.com/vs/preview/).</span></span> <span data-ttu-id="e7ecf-110">安裝 **ASP.NET 和 Web 開發**及 **Azure 開發**工作負載。</span><span class="sxs-lookup"><span data-stu-id="e7ecf-110">Install the workloads **ASP.NET and web development** and **Azure development**.</span></span>
- [<span data-ttu-id="e7ecf-111">Azure Function Tools for Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="e7ecf-111">Azure Function Tools for Visual Studio 2017</span></span>](https://marketplace.visualstudio.com/items?itemName=AndrewBHall-MSFT.AzureFunctionToolsforVisualStudio2017)

## <a name="functions-class-library-project"></a><span data-ttu-id="e7ecf-112">Functions 類別庫專案</span><span class="sxs-lookup"><span data-stu-id="e7ecf-112">Functions class library project</span></span>

<span data-ttu-id="e7ecf-113">從 Visual Studio 中建立 Azure Functions 專案。</span><span class="sxs-lookup"><span data-stu-id="e7ecf-113">From Visual Studio, create a new Azure Functions project.</span></span> <span data-ttu-id="e7ecf-114">新的專案範本會建立 host.json 和 local.settings.json 檔案。</span><span class="sxs-lookup"><span data-stu-id="e7ecf-114">The new project template creates the files *host.json* and *local.settings.json*.</span></span> <span data-ttu-id="e7ecf-115">您可以[在 host.json 中自訂 Azure Functions 執行階段設定](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json)。</span><span class="sxs-lookup"><span data-stu-id="e7ecf-115">You can [customize Azure Functions runtime settings in host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json).</span></span> 

<span data-ttu-id="e7ecf-116">local.settings.json 檔案會儲存應用程式設定、連接字串和 Azure Functions Core Tools 的設定。</span><span class="sxs-lookup"><span data-stu-id="e7ecf-116">The file *local.settings.json* stores app settings, connection strings, and settings for Azure Functions Core Tools.</span></span> <span data-ttu-id="e7ecf-117">若要深入了解其結構，請參閱[在本機撰寫程式碼和測試 Azure Functions](functions-run-local.md#local-settings)。</span><span class="sxs-lookup"><span data-stu-id="e7ecf-117">To learn more about its structure, see [Code and test Azure functions locally](functions-run-local.md#local-settings).</span></span>

### <a name="functionname-attribute"></a><span data-ttu-id="e7ecf-118">FunctionName 屬性</span><span class="sxs-lookup"><span data-stu-id="e7ecf-118">FunctionName attribute</span></span>

<span data-ttu-id="e7ecf-119">屬性 [`FunctionNameAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/FunctionNameAttribute.cs) 會將方法標記為函式進入點。</span><span class="sxs-lookup"><span data-stu-id="e7ecf-119">The attribute [`FunctionNameAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/FunctionNameAttribute.cs) marks a method as a function entry point.</span></span> <span data-ttu-id="e7ecf-120">它必須剛好僅與一個觸發程序以及 0 個以上的輸入和輸出繫結搭配使用。</span><span class="sxs-lookup"><span data-stu-id="e7ecf-120">It must be used with exactly one trigger and 0 or more input and output bindings.</span></span>

### <a name="conversion-to-functionjson"></a><span data-ttu-id="e7ecf-121">轉換成 function.json</span><span class="sxs-lookup"><span data-stu-id="e7ecf-121">Conversion to function.json</span></span>

<span data-ttu-id="e7ecf-122">建置 Azure Functions 專案時，它會在目錄中產生一個檔案 `function.json`，比對由 `[FunctionName]` 所定義的函式名稱。</span><span class="sxs-lookup"><span data-stu-id="e7ecf-122">When an Azure Functions project is built, it produces a file `function.json` in the directory matching the function name defined by `[FunctionName]`.</span></span> <span data-ttu-id="e7ecf-123">它會指定觸發程序和繫結，並指向專案組件檔。</span><span class="sxs-lookup"><span data-stu-id="e7ecf-123">It specifies triggers and bindings and points to the project assembly file.</span></span>

<span data-ttu-id="e7ecf-124">此轉換是由 NuGet 套件 [Microsoft\.NET\.Sdk\.Functions](http://www.nuget.org/packages/Microsoft.NET.Sdk.Functions) 執行。</span><span class="sxs-lookup"><span data-stu-id="e7ecf-124">This conversion is performed by the NuGet package [Microsoft\.NET\.Sdk\.Functions](http://www.nuget.org/packages/Microsoft.NET.Sdk.Functions).</span></span> <span data-ttu-id="e7ecf-125">來源可在 GitHub 存放庫 [azure\-functions\-vs\-build\-sdk](https://github.com/Azure/azure-functions-vs-build-sdk) 提供使用。</span><span class="sxs-lookup"><span data-stu-id="e7ecf-125">The source is available in the GitHub repo [azure\-functions\-vs\-build\-sdk](https://github.com/Azure/azure-functions-vs-build-sdk).</span></span>

## <a name="triggers-and-bindings"></a><span data-ttu-id="e7ecf-126">觸發和繫結</span><span class="sxs-lookup"><span data-stu-id="e7ecf-126">Triggers and bindings</span></span>

<span data-ttu-id="e7ecf-127">下表列出的觸發程序和繫結可在 Azure Functions 類別庫專案中提供使用。</span><span class="sxs-lookup"><span data-stu-id="e7ecf-127">The following table lists the triggers and bindings that are available in an Azure Functions class library project.</span></span> <span data-ttu-id="e7ecf-128">所有屬性都在 `Microsoft.Azure.WebJobs` 命名空間中。</span><span class="sxs-lookup"><span data-stu-id="e7ecf-128">All attributes are in the namespace `Microsoft.Azure.WebJobs`.</span></span>

| <span data-ttu-id="e7ecf-129">繫結</span><span class="sxs-lookup"><span data-stu-id="e7ecf-129">Binding</span></span> | <span data-ttu-id="e7ecf-130">屬性</span><span class="sxs-lookup"><span data-stu-id="e7ecf-130">Attribute</span></span> | <span data-ttu-id="e7ecf-131">Nuget 套件</span><span class="sxs-lookup"><span data-stu-id="e7ecf-131">NuGet package</span></span> |
|------   | ------    | ------        |
| [<span data-ttu-id="e7ecf-132">Blob 儲存體觸發程序, 輸入, 輸出</span><span class="sxs-lookup"><span data-stu-id="e7ecf-132">Blob storage trigger, input, output</span></span>](#blob-storage) | <span data-ttu-id="e7ecf-133">[BlobAttribute], [StorageAccountAttribute]</span><span class="sxs-lookup"><span data-stu-id="e7ecf-133">[BlobAttribute], [StorageAccountAttribute]</span></span> | <span data-ttu-id="e7ecf-134">[Microsoft.Azure.WebJobs]</span><span class="sxs-lookup"><span data-stu-id="e7ecf-134">[Microsoft.Azure.WebJobs]</span></span> | <span data-ttu-id="e7ecf-135">[Blob 儲存體]</span><span class="sxs-lookup"><span data-stu-id="e7ecf-135">[Blob storage]</span></span> |
| [<span data-ttu-id="e7ecf-136">Cosmos DB 輸入和輸出繫結</span><span class="sxs-lookup"><span data-stu-id="e7ecf-136">Cosmos DB input and output binding</span></span>](#cosmos-db) | <span data-ttu-id="e7ecf-137">[DocumentDBAttribute]</span><span class="sxs-lookup"><span data-stu-id="e7ecf-137">[DocumentDBAttribute]</span></span> | <span data-ttu-id="e7ecf-138">[Microsoft.Azure.WebJobs.Extensions.DocumentDB]</span><span class="sxs-lookup"><span data-stu-id="e7ecf-138">[Microsoft.Azure.WebJobs.Extensions.DocumentDB]</span></span> | 
| [<span data-ttu-id="e7ecf-139">事件中心觸發程序和輸出</span><span class="sxs-lookup"><span data-stu-id="e7ecf-139">Event Hubs trigger and output</span></span>](#event-hub) | <span data-ttu-id="e7ecf-140">[EventHubTriggerAttribute], [EventHubAttribute]</span><span class="sxs-lookup"><span data-stu-id="e7ecf-140">[EventHubTriggerAttribute], [EventHubAttribute]</span></span> | <span data-ttu-id="e7ecf-141">[Microsoft.Azure.WebJobs.ServiceBus]</span><span class="sxs-lookup"><span data-stu-id="e7ecf-141">[Microsoft.Azure.WebJobs.ServiceBus]</span></span> |
| [<span data-ttu-id="e7ecf-142">外部檔案輸入和輸出</span><span class="sxs-lookup"><span data-stu-id="e7ecf-142">External file input and output</span></span>](#api-hub) | <span data-ttu-id="e7ecf-143">[ApiHubFileAttribute]</span><span class="sxs-lookup"><span data-stu-id="e7ecf-143">[ApiHubFileAttribute]</span></span> | <span data-ttu-id="e7ecf-144">[Microsoft.Azure.WebJobs.Extensions.ApiHub]</span><span class="sxs-lookup"><span data-stu-id="e7ecf-144">[Microsoft.Azure.WebJobs.Extensions.ApiHub]</span></span> |
| [<span data-ttu-id="e7ecf-145">HTTP 和 Webhook 觸發程序</span><span class="sxs-lookup"><span data-stu-id="e7ecf-145">HTTP and webhook trigger</span></span>](#http) | <span data-ttu-id="e7ecf-146">[HttpTriggerAttribute]</span><span class="sxs-lookup"><span data-stu-id="e7ecf-146">[HttpTriggerAttribute]</span></span> | <span data-ttu-id="e7ecf-147">[Microsoft.Azure.WebJobs.Extensions.Http]</span><span class="sxs-lookup"><span data-stu-id="e7ecf-147">[Microsoft.Azure.WebJobs.Extensions.Http]</span></span> |
| [<span data-ttu-id="e7ecf-148">Mobile Apps 輸入和輸出</span><span class="sxs-lookup"><span data-stu-id="e7ecf-148">Mobile Apps input and output</span></span>](#mobile-apps) | <span data-ttu-id="e7ecf-149">[MobileTableAttribute]</span><span class="sxs-lookup"><span data-stu-id="e7ecf-149">[MobileTableAttribute]</span></span> | <span data-ttu-id="e7ecf-150">[Microsoft.Azure.WebJobs.Extensions.MobileApps]</span><span class="sxs-lookup"><span data-stu-id="e7ecf-150">[Microsoft.Azure.WebJobs.Extensions.MobileApps]</span></span> | 
| [<span data-ttu-id="e7ecf-151">通知中樞輸出</span><span class="sxs-lookup"><span data-stu-id="e7ecf-151">Notification Hubs output</span></span>](#nh) | <span data-ttu-id="e7ecf-152">[NotificationHubAttribute]</span><span class="sxs-lookup"><span data-stu-id="e7ecf-152">[NotificationHubAttribute]</span></span> | <span data-ttu-id="e7ecf-153">[Microsoft.Azure.WebJobs.Extensions.NotificationHubs]</span><span class="sxs-lookup"><span data-stu-id="e7ecf-153">[Microsoft.Azure.WebJobs.Extensions.NotificationHubs]</span></span> | 
| [<span data-ttu-id="e7ecf-154">佇列儲存體觸發程序和輸出</span><span class="sxs-lookup"><span data-stu-id="e7ecf-154">Queue storage trigger and output</span></span>](#queue) | <span data-ttu-id="e7ecf-155">[QueueAttribute], [StorageAccountAttribute]</span><span class="sxs-lookup"><span data-stu-id="e7ecf-155">[QueueAttribute], [StorageAccountAttribute]</span></span> | <span data-ttu-id="e7ecf-156">[Microsoft.Azure.WebJobs]</span><span class="sxs-lookup"><span data-stu-id="e7ecf-156">[Microsoft.Azure.WebJobs]</span></span> | 
| [<span data-ttu-id="e7ecf-157">SendGrid 輸出</span><span class="sxs-lookup"><span data-stu-id="e7ecf-157">SendGrid output</span></span>](#sendgrid) | <span data-ttu-id="e7ecf-158">[SendGridAttribute]</span><span class="sxs-lookup"><span data-stu-id="e7ecf-158">[SendGridAttribute]</span></span> | <span data-ttu-id="e7ecf-159">[Microsoft.Azure.WebJobs.Extensions.SendGrid]</span><span class="sxs-lookup"><span data-stu-id="e7ecf-159">[Microsoft.Azure.WebJobs.Extensions.SendGrid]</span></span> | 
| [<span data-ttu-id="e7ecf-160">服務匯流排觸發程序和輸出</span><span class="sxs-lookup"><span data-stu-id="e7ecf-160">Service Bus trigger and output</span></span>](#service-bus) | <span data-ttu-id="e7ecf-161">[ServiceBusAttribute], [ServiceBusAccountAttribute]</span><span class="sxs-lookup"><span data-stu-id="e7ecf-161">[ServiceBusAttribute], [ServiceBusAccountAttribute]</span></span> | <span data-ttu-id="e7ecf-162">[Microsoft.Azure.WebJobs.ServiceBus]</span><span class="sxs-lookup"><span data-stu-id="e7ecf-162">[Microsoft.Azure.WebJobs.ServiceBus]</span></span>
| [<span data-ttu-id="e7ecf-163">資料表儲存體輸入和輸出</span><span class="sxs-lookup"><span data-stu-id="e7ecf-163">Table storage input and output</span></span>](#table) | <span data-ttu-id="e7ecf-164">[TableAttribute], [StorageAccountAttribute]</span><span class="sxs-lookup"><span data-stu-id="e7ecf-164">[TableAttribute], [StorageAccountAttribute]</span></span> | <span data-ttu-id="e7ecf-165">[Microsoft.Azure.WebJobs]</span><span class="sxs-lookup"><span data-stu-id="e7ecf-165">[Microsoft.Azure.WebJobs]</span></span> | 
| [<span data-ttu-id="e7ecf-166">計時器觸發程序</span><span class="sxs-lookup"><span data-stu-id="e7ecf-166">Timer trigger</span></span>](#timer) | <span data-ttu-id="e7ecf-167">[TimerTriggerAttribute]</span><span class="sxs-lookup"><span data-stu-id="e7ecf-167">[TimerTriggerAttribute]</span></span> | <span data-ttu-id="e7ecf-168">[Microsoft.Azure.WebJobs.Extensions]</span><span class="sxs-lookup"><span data-stu-id="e7ecf-168">[Microsoft.Azure.WebJobs.Extensions]</span></span> | 
| [<span data-ttu-id="e7ecf-169">Twilio 輸出</span><span class="sxs-lookup"><span data-stu-id="e7ecf-169">Twilio output</span></span>](#twilio) | <span data-ttu-id="e7ecf-170">[TwilioSmsAttribute]</span><span class="sxs-lookup"><span data-stu-id="e7ecf-170">[TwilioSmsAttribute]</span></span> | <span data-ttu-id="e7ecf-171">[Microsoft.Azure.WebJobs.Extensions.Twilio]</span><span class="sxs-lookup"><span data-stu-id="e7ecf-171">[Microsoft.Azure.WebJobs.Extensions.Twilio]</span></span> | 

<a name="blob-storage"></a>

### <a name="blob-storage-trigger-input-and-output-bindings"></a><span data-ttu-id="e7ecf-172">Blob 儲存體觸發程序、輸入和輸出繫結</span><span class="sxs-lookup"><span data-stu-id="e7ecf-172">Blob storage trigger, input, and output bindings</span></span>

<span data-ttu-id="e7ecf-173">Azure Functions 支援適用於 Azure Blob 儲存體的觸發程序、輸入和輸出繫結。</span><span class="sxs-lookup"><span data-stu-id="e7ecf-173">Azure Functions supports trigger, input, and output bindings for Azure Blob storage.</span></span> <span data-ttu-id="e7ecf-174">如需有關繫結運算式和中繼資料的詳細資訊，請參閱 [Azure Functions Blob 儲存體繫結](functions-bindings-storage-blob.md)。</span><span class="sxs-lookup"><span data-stu-id="e7ecf-174">For more information on binding expressions and metadata, see [Azure Functions Blob storage bindings](functions-bindings-storage-blob.md).</span></span>

<span data-ttu-id="e7ecf-175">Blob 觸發程序是使用 `[BlobTrigger]` 屬性定義。</span><span class="sxs-lookup"><span data-stu-id="e7ecf-175">A blob trigger is defined with the `[BlobTrigger]` attribute.</span></span> <span data-ttu-id="e7ecf-176">您可以使用 `[StorageAccount]` 屬性來定義整個函式或類別所使用的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="e7ecf-176">You can use the attribute `[StorageAccount]` to define the storage account that is used by an entire function or class.</span></span>

```csharp
[StorageAccount("AzureWebJobsStorage")]
[FunctionName("BlobTriggerCSharp")]        
public static void Run([BlobTrigger("samples-workitems/{name}")] Stream myBlob, string name, TraceWriter log)
{
    log.Info($"C# Blob trigger function Processed blob\n Name:{name} \n Size: {myBlob.Length} Bytes");
}
```

<span data-ttu-id="e7ecf-177">Blob 輸入和輸出是使用 `[Blob]` 屬性定義，以及表示讀取或寫入的 `FileAccess` 參數。</span><span class="sxs-lookup"><span data-stu-id="e7ecf-177">Blob input and output are defined using the `[Blob]` attribute, along with a `FileAccess` parameter indicating read or write.</span></span> <span data-ttu-id="e7ecf-178">下列範例是使用 blob 觸發程序和 blob 輸出繫結。</span><span class="sxs-lookup"><span data-stu-id="e7ecf-178">The following example uses a blob trigger and blob output binding.</span></span>

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

### <a name="cosmos-db-input-and-output-bindings"></a><span data-ttu-id="e7ecf-179">Cosmos DB 輸入和輸出繫結</span><span class="sxs-lookup"><span data-stu-id="e7ecf-179">Cosmos DB input and output bindings</span></span>

<span data-ttu-id="e7ecf-180">Azure Functions 支援 Cosmos DB 的輸入和輸出繫結。</span><span class="sxs-lookup"><span data-stu-id="e7ecf-180">Azure Functions supports input and output bindings for Cosmos DB.</span></span> <span data-ttu-id="e7ecf-181">若要深入了解 Cosmos DB 繫結的功能，請參閱 [Azure Functions Cosmos DB 繫結](functions-bindings-documentdb.md)。</span><span class="sxs-lookup"><span data-stu-id="e7ecf-181">To learn more about the features of the Cosmos DB binding, see [Azure Functions Cosmos DB bindings](functions-bindings-documentdb.md).</span></span>

<span data-ttu-id="e7ecf-182">若要繫結至 Cosmos DB 文件，請使用 NuGet 套件 [Microsoft.Azure.WebJobs.Extensions.DocumentDB] 中的 `[DocumentDB]` 屬性。</span><span class="sxs-lookup"><span data-stu-id="e7ecf-182">To bind to a Cosmos DB document, use the attribute `[DocumentDB]` in the NuGet package [Microsoft.Azure.WebJobs.Extensions.DocumentDB].</span></span> <span data-ttu-id="e7ecf-183">下列範例具有佇列觸發程序和 DocumentDB API 輸出繫結：</span><span class="sxs-lookup"><span data-stu-id="e7ecf-183">The following example has a queue trigger and a DocumentDB API output binding:</span></span>

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

### <a name="event-hubs-trigger-and-output"></a><span data-ttu-id="e7ecf-184">事件中心觸發程序和輸出</span><span class="sxs-lookup"><span data-stu-id="e7ecf-184">Event Hubs trigger and output</span></span>

<span data-ttu-id="e7ecf-185">Azure Functions 支援事件中樞的觸發程序和輸出繫結。</span><span class="sxs-lookup"><span data-stu-id="e7ecf-185">Azure Functions supports trigger and output bindings for Event Hubs.</span></span> <span data-ttu-id="e7ecf-186">如需詳細資訊，請參閱 [Azure Functions 事件中樞繫結](functions-bindings-event-hubs.md)。</span><span class="sxs-lookup"><span data-stu-id="e7ecf-186">For more information, see  [Azure Functions Event Hub bindings](functions-bindings-event-hubs.md).</span></span>

<span data-ttu-id="e7ecf-187">`[Microsoft.Azure.WebJobs.ServiceBus.EventHubTriggerAttribute]` 和 `[Microsoft.Azure.WebJobs.ServiceBus.EventHubAttribute]` 類型定義於 NuGet 套件 [Microsoft.Azure.WebJobs.ServiceBus] 中。</span><span class="sxs-lookup"><span data-stu-id="e7ecf-187">The types `[Microsoft.Azure.WebJobs.ServiceBus.EventHubTriggerAttribute]` and `[Microsoft.Azure.WebJobs.ServiceBus.EventHubAttribute]` are defined in the NuGet package [Microsoft.Azure.WebJobs.ServiceBus].</span></span> 

<span data-ttu-id="e7ecf-188">下列範例會使用事件中心觸發程序：</span><span class="sxs-lookup"><span data-stu-id="e7ecf-188">The following example uses an Event Hub trigger:</span></span>

```csharp
[FunctionName("EventHubTriggerCSharp")]
public static void Run([EventHubTrigger("samples-workitems", Connection = "EventHubConnection")] string myEventHubMessage, TraceWriter log)
{
    log.Info($"C# Event Hub trigger function processed a message: {myEventHubMessage}");
}
```

<span data-ttu-id="e7ecf-189">下列範例具有輸出事件中心，是使用方法傳回值作為輸出：</span><span class="sxs-lookup"><span data-stu-id="e7ecf-189">The following example has an Event Hub output, using the method return value as the output:</span></span>

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

### <a name="external-file-input-and-output"></a><span data-ttu-id="e7ecf-190">外部檔案輸入和輸出</span><span class="sxs-lookup"><span data-stu-id="e7ecf-190">External file input and output</span></span>

<span data-ttu-id="e7ecf-191">Azure Functions 支援適用於外部檔案 (例如 Google Drive、Dropbox 和 OneDrive) 的觸發程序、輸入和輸出繫結。</span><span class="sxs-lookup"><span data-stu-id="e7ecf-191">Azure Functions supports trigger, input, and output bindings for external files, such as Google Drive, Dropbox, and OneDrive.</span></span> <span data-ttu-id="e7ecf-192">若要深入了解，請參閱 [Azure Functions 外部檔案繫結](functions-bindings-external-file.md)。</span><span class="sxs-lookup"><span data-stu-id="e7ecf-192">To learn more, see [Azure Functions External File bindings](functions-bindings-external-file.md).</span></span> <span data-ttu-id="e7ecf-193">`[ExternalFileTrigger]` 和 `[ExternalFile]` 屬性定義於 NuGet 套件 [Microsoft.Azure.WebJobs.Extensions.ApiHub] 中。</span><span class="sxs-lookup"><span data-stu-id="e7ecf-193">The attributes `[ExternalFileTrigger]` and `[ExternalFile]` are defined in the NuGet package [Microsoft.Azure.WebJobs.Extensions.ApiHub].</span></span>

<span data-ttu-id="e7ecf-194">下列 C# 範例示範外部檔案輸入和輸出繫結。</span><span class="sxs-lookup"><span data-stu-id="e7ecf-194">The following C# example demonstrates an external file input and output binding.</span></span> <span data-ttu-id="e7ecf-195">程式碼會將輸入檔案複製到輸出檔案。</span><span class="sxs-lookup"><span data-stu-id="e7ecf-195">The code copies the input file to the output file.</span></span>

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

### <a name="http-and-webhooks"></a><span data-ttu-id="e7ecf-196">HTTP 和 Webhook</span><span class="sxs-lookup"><span data-stu-id="e7ecf-196">HTTP and webhooks</span></span>

<span data-ttu-id="e7ecf-197">使用 `HttpTrigger` 屬性來定義 HTTP 觸發程序或 webhook。</span><span class="sxs-lookup"><span data-stu-id="e7ecf-197">Use the `HttpTrigger` attribute to define an HTTP trigger or webhook.</span></span> <span data-ttu-id="e7ecf-198">此屬性定義於 NuGet 套件 [Microsoft.Azure.WebJobs.Extensions.Http] 中。</span><span class="sxs-lookup"><span data-stu-id="e7ecf-198">This attribute is defined in the NuGet package [Microsoft.Azure.WebJobs.Extensions.Http].</span></span> <span data-ttu-id="e7ecf-199">您可以自訂授權層級、webhook 類型、路由和方法。</span><span class="sxs-lookup"><span data-stu-id="e7ecf-199">You can customize the authorization level, webhook type, route, and methods.</span></span> <span data-ttu-id="e7ecf-200">下列範例會使用匿名驗證和 _genericJson_ webhook 類型來定義 HTTP 觸發程序。</span><span class="sxs-lookup"><span data-stu-id="e7ecf-200">The following example defines an HTTP trigger with anonymous authentication and _genericJson_ webhook type.</span></span>

```csharp
[FunctionName("HttpTriggerCSharp")]
public static HttpResponseMessage Run([HttpTrigger(AuthorizationLevel.Anonymous, WebHookType = "genericJson")] HttpRequestMessage req)
{
    return req.CreateResponse(HttpStatusCode.OK);
}
```

<a name="mobile-apps"></a>

### <a name="mobile-apps-input-and-output"></a><span data-ttu-id="e7ecf-201">Mobile Apps 輸入和輸出</span><span class="sxs-lookup"><span data-stu-id="e7ecf-201">Mobile Apps input and output</span></span>

<span data-ttu-id="e7ecf-202">Azure Functions 支援 Mobile Apps 的輸入和輸出繫結。</span><span class="sxs-lookup"><span data-stu-id="e7ecf-202">Azure Functions supports input and output bindings for Mobile Apps.</span></span> <span data-ttu-id="e7ecf-203">若要深入了解，請參閱 [Azure Functions Mobile Apps 繫結](functions-bindings-mobile-apps.md)。</span><span class="sxs-lookup"><span data-stu-id="e7ecf-203">To learn more, see [Azure Functions Mobile Apps bindings](functions-bindings-mobile-apps.md).</span></span> <span data-ttu-id="e7ecf-204">`[MobileTable]` 屬性定義於 NuGet 套件 [Microsoft.Azure.WebJobs.Extensions.MobileApps] 中。</span><span class="sxs-lookup"><span data-stu-id="e7ecf-204">The attribute `[MobileTable]` is defined in the NuGet package [Microsoft.Azure.WebJobs.Extensions.MobileApps].</span></span>

<span data-ttu-id="e7ecf-205">下列範例會示範 Mobile Apps 輸出繫結：</span><span class="sxs-lookup"><span data-stu-id="e7ecf-205">The following example demonstrates a Mobile Apps output binding:</span></span>

```csharp
[FunctionName("MobileAppsOutput")]        
[return: MobileTable(ApiKeySetting = "MyMobileAppKey", TableName = "MyTable", MobileAppUriSetting = "MyMobileAppUri")]
public static object Run([QueueTrigger("myqueue-items", Connection = "AzureWebJobsStorage")] string myQueueItem, TraceWriter log)
{
    return new { Text = $"I'm running in a C# function! {myQueueItem}" };
}
```

<a name="nh"></a>

### <a name="notification-hubs-output"></a><span data-ttu-id="e7ecf-206">通知中樞輸出</span><span class="sxs-lookup"><span data-stu-id="e7ecf-206">Notification Hubs output</span></span>

<span data-ttu-id="e7ecf-207">Azure Functions 會支援通知中樞的輸出繫結。</span><span class="sxs-lookup"><span data-stu-id="e7ecf-207">Azure Functions supports an output binding for Notification Hubs.</span></span> <span data-ttu-id="e7ecf-208">若要深入了解，請參閱 [Azure Functions 通知中樞輸出繫結](functions-bindings-notification-hubs.md)。</span><span class="sxs-lookup"><span data-stu-id="e7ecf-208">To learn more, see [Azure Functions Notification Hub output binding](functions-bindings-notification-hubs.md).</span></span> <span data-ttu-id="e7ecf-209">`[NotificationHub]` 屬性定義於 NuGet 套件 [Microsoft.Azure.WebJobs.Extensions.NotificationHubs] 中。</span><span class="sxs-lookup"><span data-stu-id="e7ecf-209">The attribute `[NotificationHub]` is defined in the NuGet package [Microsoft.Azure.WebJobs.Extensions.NotificationHubs].</span></span>

<a name="queue"></a>

### <a name="queue-storage-trigger-and-output"></a><span data-ttu-id="e7ecf-210">佇列儲存體觸發程序和輸出</span><span class="sxs-lookup"><span data-stu-id="e7ecf-210">Queue storage trigger and output</span></span>

<span data-ttu-id="e7ecf-211">Azure Functions 支援適用於 Azure 佇列的觸發程序和輸出繫結。</span><span class="sxs-lookup"><span data-stu-id="e7ecf-211">Azure Functions supports trigger and output bindings for Azure queues.</span></span> <span data-ttu-id="e7ecf-212">如需詳細資訊，請參閱 [Azure Functions 佇列儲存體繫結](functions-bindings-storage-queue.md)。</span><span class="sxs-lookup"><span data-stu-id="e7ecf-212">For more information, see [Azure Functions Queue Storage bindings](functions-bindings-storage-queue.md).</span></span>

<span data-ttu-id="e7ecf-213">下列範例示範如何使用 `[Queue]` 屬性，搭配佇列輸出繫結使用函式傳回型別。</span><span class="sxs-lookup"><span data-stu-id="e7ecf-213">The following example shows how to use the function return type with a queue output binding, using the `[Queue]` attribute.</span></span> <span data-ttu-id="e7ecf-214">若要定義佇列觸發程序，請使用 `[QueueTrigger]` 屬性。</span><span class="sxs-lookup"><span data-stu-id="e7ecf-214">To define a queue trigger, use the `[QueueTrigger]` attribute.</span></span>

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

### <a name="sendgrid-output"></a><span data-ttu-id="e7ecf-215">SendGrid 輸出</span><span class="sxs-lookup"><span data-stu-id="e7ecf-215">SendGrid output</span></span>

<span data-ttu-id="e7ecf-216">Azure Functions 支援用於以程式設計方式傳送電子郵件的 SendGrid 輸出繫結。</span><span class="sxs-lookup"><span data-stu-id="e7ecf-216">Azure Functions supports a SendGrid output binding for sending email programmatically.</span></span> <span data-ttu-id="e7ecf-217">若要深入了解，請參閱 [Azure Functions SendGrid 繫結](functions-bindings-sendgrid.md)。</span><span class="sxs-lookup"><span data-stu-id="e7ecf-217">To learn more, see [Azure Functions SendGrid bindings](functions-bindings-sendgrid.md).</span></span>

<span data-ttu-id="e7ecf-218">`[SendGrid]` 屬性定義於 NuGet 套件 [Microsoft.Azure.WebJobs.Extensions.SendGrid] 中。</span><span class="sxs-lookup"><span data-stu-id="e7ecf-218">The attribute `[SendGrid]` is defined in the NuGet package [Microsoft.Azure.WebJobs.Extensions.SendGrid].</span></span>

<span data-ttu-id="e7ecf-219">以下範例使用服務匯流排佇列觸發程序，以及使用 `SendGridMessage` 的 SendGrid 輸出繫結：</span><span class="sxs-lookup"><span data-stu-id="e7ecf-219">The following is an example of using a Service Bus queue trigger and a SendGrid output binding using `SendGridMessage`:</span></span>

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
    public string To { get; set; }
    public string From { get; set; }
    public string Subject { get; set; }
    public string Body { get; set; }
}
```

<a name="service-bus"></a>

### <a name="service-bus-trigger-and-output"></a><span data-ttu-id="e7ecf-220">服務匯流排觸發程序和輸出</span><span class="sxs-lookup"><span data-stu-id="e7ecf-220">Service Bus trigger and output</span></span>

<span data-ttu-id="e7ecf-221">Azure Functions 支援服務匯流排佇列和主題的觸發程序和輸出繫結。</span><span class="sxs-lookup"><span data-stu-id="e7ecf-221">Azure Functions supports trigger and output bindings for Service Bus queues and topics.</span></span> <span data-ttu-id="e7ecf-222">如需有關如何設定繫結的詳細資訊，請參閱 [Azure Functions 服務匯流排繫結](functions-bindings-service-bus.md)。</span><span class="sxs-lookup"><span data-stu-id="e7ecf-222">For more information on configuring bindings, see [Azure Functions Service Bus bindings](functions-bindings-service-bus.md).</span></span>

<span data-ttu-id="e7ecf-223">`[ServiceBusTrigger]` 和 `[ServiceBus]` 屬性定義於 NuGet 套件 [Microsoft.Azure.WebJobs.ServiceBus] 中。</span><span class="sxs-lookup"><span data-stu-id="e7ecf-223">The attributes `[ServiceBusTrigger]` and `[ServiceBus]` are defined in the NuGet package [Microsoft.Azure.WebJobs.ServiceBus].</span></span> 

<span data-ttu-id="e7ecf-224">以下是服務匯流排佇列觸發程序的範例：</span><span class="sxs-lookup"><span data-stu-id="e7ecf-224">The following is an example of a Service Bus queue trigger:</span></span>

```csharp
[FunctionName("ServiceBusQueueTriggerCSharp")]                    
public static void Run([ServiceBusTrigger("myqueue", AccessRights.Manage, Connection = "ServiceBusConnection")] string myQueueItem, TraceWriter log)
{
    log.Info($"C# ServiceBus queue trigger function processed message: {myQueueItem}");
}
```

<span data-ttu-id="e7ecf-225">以下是服務匯流排輸出繫結的範例，使用方法傳回型別作為輸出：</span><span class="sxs-lookup"><span data-stu-id="e7ecf-225">The following is an example of a Service Bus output binding, using the method return type as the output:</span></span>

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

### <a name="table-storage-input-and-output"></a><span data-ttu-id="e7ecf-226">資料表儲存體輸入和輸出</span><span class="sxs-lookup"><span data-stu-id="e7ecf-226">Table storage input and output</span></span>

<span data-ttu-id="e7ecf-227">Azure Functions 支援 Azure 資料表儲存體的輸入和輸出繫結。</span><span class="sxs-lookup"><span data-stu-id="e7ecf-227">Azure Functions supports input and output bindings for Azure Table storage.</span></span> <span data-ttu-id="e7ecf-228">若要深入了解，請參閱 [Azure Functions 資料表儲存體繫結](functions-bindings-storage-table.md)。</span><span class="sxs-lookup"><span data-stu-id="e7ecf-228">To learn more, see [Azure Functions Table storage bindings](functions-bindings-storage-table.md).</span></span>

<span data-ttu-id="e7ecf-229">下列範例是具有兩個函式的類別，示範資料表儲存體輸出和輸入繫結。</span><span class="sxs-lookup"><span data-stu-id="e7ecf-229">The following example is a class with two functions, demonstrating table storage output and input bindings.</span></span> 

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

    // use the metadata parameter "queueTrigger" to bind the queue payload
    [FunctionName("TableInput")]
    public static void TableInput([QueueTrigger("table-items")] string input, [Table("MyTable", "Http", "{queueTrigger}")] MyPoco poco, TraceWriter log)
    {
        log.Info($"C# function processed: {poco.Text}");
    }
}

```

<a name="timer"></a>

### <a name="timer-trigger"></a><span data-ttu-id="e7ecf-230">計時器觸發程序</span><span class="sxs-lookup"><span data-stu-id="e7ecf-230">Timer trigger</span></span>

<span data-ttu-id="e7ecf-231">Azure Functions 具有計時器觸發程序繫結，可讓您根據所定義的排程執行函式程式碼。</span><span class="sxs-lookup"><span data-stu-id="e7ecf-231">Azure Functions has a timer trigger binding that lets you run your function code based on a defined schedule.</span></span> <span data-ttu-id="e7ecf-232">若要深入了解繫結的功能，請參閱[使用 Azure Functions 排程程式碼執行](functions-bindings-timer.md)。</span><span class="sxs-lookup"><span data-stu-id="e7ecf-232">To learn more about the features of the binding, see [Schedule code execution with Azure Functions](functions-bindings-timer.md).</span></span>

<span data-ttu-id="e7ecf-233">在耗用量方案中，您可以使用 [CRON 運算式](http://en.wikipedia.org/wiki/Cron#CRON_expression)來定義排程。</span><span class="sxs-lookup"><span data-stu-id="e7ecf-233">On the Consumption plan, you can define schedules with a [CRON expression](http://en.wikipedia.org/wiki/Cron#CRON_expression).</span></span> <span data-ttu-id="e7ecf-234">如果您是使用 App Service 方案，也可以使用 TimeSpan 字串。</span><span class="sxs-lookup"><span data-stu-id="e7ecf-234">If you're using an App Service Plan, you can also use a TimeSpan string.</span></span> 

<span data-ttu-id="e7ecf-235">下列範例會定義每隔 5 分鐘執行的計時器觸發程序：</span><span class="sxs-lookup"><span data-stu-id="e7ecf-235">The following example defines a timer trigger that runs every 5 minutes:</span></span>

```csharp
[FunctionName("TimerTriggerCSharp")]
public static void Run([TimerTrigger("0 */5 * * * *")]TimerInfo myTimer, TraceWriter log)
{
    log.Info($"C# Timer trigger function executed at: {DateTime.Now}");
}
```

<a name="twilio"></a>

### <a name="twilio-output"></a><span data-ttu-id="e7ecf-236">Twilio 輸出</span><span class="sxs-lookup"><span data-stu-id="e7ecf-236">Twilio output</span></span>

<span data-ttu-id="e7ecf-237">Azure Functions 支援 Twilio 輸出繫結，讓函式能傳送 SMS 文字訊息。</span><span class="sxs-lookup"><span data-stu-id="e7ecf-237">Azure Functions supports Twilio output bindings to enable your functions to send SMS text messages.</span></span> <span data-ttu-id="e7ecf-238">若要深入了解，請參閱 [使用 Twilio 輸出繫結從 Azure Functions 傳送 SMS 文字訊息](functions-bindings-twilio.md)。</span><span class="sxs-lookup"><span data-stu-id="e7ecf-238">To learn more, see [Send SMS messages from Azure Functions using the Twilio output binding](functions-bindings-twilio.md).</span></span> 

<span data-ttu-id="e7ecf-239">`[TwilioSms]` 屬性定義於 NuGet 套件 [Microsoft.Azure.WebJobs.Extensions.Twilio] 中。</span><span class="sxs-lookup"><span data-stu-id="e7ecf-239">The attribute `[TwilioSms]` is defined in the package [Microsoft.Azure.WebJobs.Extensions.Twilio].</span></span>

<span data-ttu-id="e7ecf-240">下列 C# 範例是使用佇列觸發程序和 Twilio 輸出繫結：</span><span class="sxs-lookup"><span data-stu-id="e7ecf-240">The following C# example uses a queue trigger and a Twilio output binding:</span></span>

```csharp
[FunctionName("QueueTwilio")]
[return: TwilioSms(AccountSidSetting = "TwilioAccountSid", AuthTokenSetting = "TwilioAuthToken", From = "+1425XXXXXXX" )]
public static SMSMessage Run([QueueTrigger("myqueue-items", Connection = "AzureWebJobsStorage")] JObject order, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {order}");

    var message = new SMSMessage()
    {
        Body = $"Hello {order["name"]}, thanks for your order!",
        To = order["mobileNumber"].ToString()
    };

    return message;
}
```

## <a name="next-steps"></a><span data-ttu-id="e7ecf-241">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e7ecf-241">Next steps</span></span>

<span data-ttu-id="e7ecf-242">如需有關如何在 C# 指令碼中使用 Azure Functions 的詳細資訊，請參閱 [Azure Functions C\# 指令碼開發人員參考](functions-reference-csharp.md)。</span><span class="sxs-lookup"><span data-stu-id="e7ecf-242">For more information on using Azure Functions in C# scripting, see [Azure Functions C\# script developer reference](functions-reference-csharp.md).</span></span>

[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]


<!-- NuGet packages --> 
<span data-ttu-id="e7ecf-243">[Microsoft.Azure.WebJobs]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs/2.1.0-beta1</span><span class="sxs-lookup"><span data-stu-id="e7ecf-243">[Microsoft.Azure.WebJobs]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs/2.1.0-beta1</span></span>
<span data-ttu-id="e7ecf-244">[Microsoft.Azure.WebJobs.Extensions.DocumentDB]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.DocumentDB/1.1.0-beta1</span><span class="sxs-lookup"><span data-stu-id="e7ecf-244">[Microsoft.Azure.WebJobs.Extensions.DocumentDB]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.DocumentDB/1.1.0-beta1</span></span>
<span data-ttu-id="e7ecf-245">[Microsoft.Azure.WebJobs.ServiceBus]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.ServiceBus/2.1.0-beta1</span><span class="sxs-lookup"><span data-stu-id="e7ecf-245">[Microsoft.Azure.WebJobs.ServiceBus]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.ServiceBus/2.1.0-beta1</span></span>
<span data-ttu-id="e7ecf-246">[Microsoft.Azure.WebJobs.Extensions.MobileApps]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.MobileApps/1.1.0-beta1</span><span class="sxs-lookup"><span data-stu-id="e7ecf-246">[Microsoft.Azure.WebJobs.Extensions.MobileApps]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.MobileApps/1.1.0-beta1</span></span>
<span data-ttu-id="e7ecf-247">[Microsoft.Azure.WebJobs.Extensions.NotificationHubs]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.NotificationHubs/1.1.0-beta1</span><span class="sxs-lookup"><span data-stu-id="e7ecf-247">[Microsoft.Azure.WebJobs.Extensions.NotificationHubs]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.NotificationHubs/1.1.0-beta1</span></span>
<span data-ttu-id="e7ecf-248">[Microsoft.Azure.WebJobs.ServiceBus]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.ServiceBus/2.1.0-beta1</span><span class="sxs-lookup"><span data-stu-id="e7ecf-248">[Microsoft.Azure.WebJobs.ServiceBus]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.ServiceBus/2.1.0-beta1</span></span>
<span data-ttu-id="e7ecf-249">[Microsoft.Azure.WebJobs.Extensions.SendGrid]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.SendGrid/2.1.0-beta1</span><span class="sxs-lookup"><span data-stu-id="e7ecf-249">[Microsoft.Azure.WebJobs.Extensions.SendGrid]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.SendGrid/2.1.0-beta1</span></span>
<span data-ttu-id="e7ecf-250">[Microsoft.Azure.WebJobs.Extensions.Http]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.Http/1.0.0-beta1</span><span class="sxs-lookup"><span data-stu-id="e7ecf-250">[Microsoft.Azure.WebJobs.Extensions.Http]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.Http/1.0.0-beta1</span></span>
[Microsoft.Azure.WebJobs.Extensions.BotFramework]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.BotFramework/1.0.15-beta
<span data-ttu-id="e7ecf-251">[Microsoft.Azure.WebJobs.Extensions.ApiHub]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.ApiHub/1.0.0-beta4</span><span class="sxs-lookup"><span data-stu-id="e7ecf-251">[Microsoft.Azure.WebJobs.Extensions.ApiHub]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.ApiHub/1.0.0-beta4</span></span>
<span data-ttu-id="e7ecf-252">[Microsoft.Azure.WebJobs.Extensions.Twilio]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.Twilio/1.1.0-beta1</span><span class="sxs-lookup"><span data-stu-id="e7ecf-252">[Microsoft.Azure.WebJobs.Extensions.Twilio]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.Twilio/1.1.0-beta1</span></span>
<span data-ttu-id="e7ecf-253">[Microsoft.Azure.WebJobs.Extensions]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions/2.1.0-beta1</span><span class="sxs-lookup"><span data-stu-id="e7ecf-253">[Microsoft.Azure.WebJobs.Extensions]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions/2.1.0-beta1</span></span>


<!-- Links to source --> 
<span data-ttu-id="e7ecf-254">[DocumentDBAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.DocumentDB/DocumentDBAttribute.cs</span><span class="sxs-lookup"><span data-stu-id="e7ecf-254">[DocumentDBAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.DocumentDB/DocumentDBAttribute.cs</span></span>
<span data-ttu-id="e7ecf-255">[EventHubAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/EventHubs/EventHubAttribute.cs</span><span class="sxs-lookup"><span data-stu-id="e7ecf-255">[EventHubAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/EventHubs/EventHubAttribute.cs</span></span>
<span data-ttu-id="e7ecf-256">[EventHubTriggerAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/EventHubs/EventHubTriggerAttribute.cs</span><span class="sxs-lookup"><span data-stu-id="e7ecf-256">[EventHubTriggerAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/EventHubs/EventHubTriggerAttribute.cs</span></span>
<span data-ttu-id="e7ecf-257">[MobileTableAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.MobileApps/MobileTableAttribute.cs</span><span class="sxs-lookup"><span data-stu-id="e7ecf-257">[MobileTableAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.MobileApps/MobileTableAttribute.cs</span></span>
<span data-ttu-id="e7ecf-258">[NotificationHubAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.NotificationHubs/NotificationHubAttribute.cs </span><span class="sxs-lookup"><span data-stu-id="e7ecf-258">[NotificationHubAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.NotificationHubs/NotificationHubAttribute.cs </span></span>
<span data-ttu-id="e7ecf-259">[ServiceBusAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAttribute.cs</span><span class="sxs-lookup"><span data-stu-id="e7ecf-259">[ServiceBusAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAttribute.cs</span></span>
<span data-ttu-id="e7ecf-260">[ServiceBusAccountAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAccountAttribute.cs</span><span class="sxs-lookup"><span data-stu-id="e7ecf-260">[ServiceBusAccountAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAccountAttribute.cs</span></span>
<span data-ttu-id="e7ecf-261">[QueueAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/QueueAttribute.cs</span><span class="sxs-lookup"><span data-stu-id="e7ecf-261">[QueueAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/QueueAttribute.cs</span></span>
<span data-ttu-id="e7ecf-262">[StorageAccountAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs</span><span class="sxs-lookup"><span data-stu-id="e7ecf-262">[StorageAccountAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs</span></span>
<span data-ttu-id="e7ecf-263">[BlobAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/BlobAttribute.cs</span><span class="sxs-lookup"><span data-stu-id="e7ecf-263">[BlobAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/BlobAttribute.cs</span></span>
<span data-ttu-id="e7ecf-264">[TableAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/TableAttribute.cs</span><span class="sxs-lookup"><span data-stu-id="e7ecf-264">[TableAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/TableAttribute.cs</span></span>
<span data-ttu-id="e7ecf-265">[TwilioSmsAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.Twilio/TwilioSMSAttribute.cs</span><span class="sxs-lookup"><span data-stu-id="e7ecf-265">[TwilioSmsAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.Twilio/TwilioSMSAttribute.cs</span></span>
<span data-ttu-id="e7ecf-266">[SendGridAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.SendGrid/SendGridAttribute.cs</span><span class="sxs-lookup"><span data-stu-id="e7ecf-266">[SendGridAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.SendGrid/SendGridAttribute.cs</span></span>
<span data-ttu-id="e7ecf-267">[HttpTriggerAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/dev/src/WebJobs.Extensions.Http/HttpTriggerAttribute.cs</span><span class="sxs-lookup"><span data-stu-id="e7ecf-267">[HttpTriggerAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/dev/src/WebJobs.Extensions.Http/HttpTriggerAttribute.cs</span></span>
<span data-ttu-id="e7ecf-268">[ApiHubFileAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.ApiHub/ApiHubFileAttribute.cs</span><span class="sxs-lookup"><span data-stu-id="e7ecf-268">[ApiHubFileAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.ApiHub/ApiHubFileAttribute.cs</span></span>
<span data-ttu-id="e7ecf-269">[TimerTriggerAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions/Extensions/Timers/TimerTriggerAttribute.cs</span><span class="sxs-lookup"><span data-stu-id="e7ecf-269">[TimerTriggerAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions/Extensions/Timers/TimerTriggerAttribute.cs</span></span>
