---
title: "什麼是 Azure WebJobs SDK"
description: "Azure WebJobs SDK 簡介。 說明 SDK 是什麼、適用哪些典型案例，以及程式碼範例。"
services: app-service\web, storage
documentationcenter: .net
author: ggailey777
manager: erikre
editor: jimbe
ms.assetid: 8281267b-572b-4b14-a328-6704493ea682
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2016
ms.author: glenga
ms.openlocfilehash: 8eb05b7cbfb4505f2e94c5b8e6d367ec63a2f033
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="what-is-the-azure-webjobs-sdk"></a><span data-ttu-id="a923f-104">什麼是 Azure WebJobs SDK</span><span class="sxs-lookup"><span data-stu-id="a923f-104">What is the Azure WebJobs SDK</span></span>
## <span data-ttu-id="a923f-105"><a id="overview"></a>概觀</span><span class="sxs-lookup"><span data-stu-id="a923f-105"><a id="overview"></a>Overview</span></span>
<span data-ttu-id="a923f-106">本文說明 WebJobs SDK 是什麼、檢閱部分適用的典型案例，以及提供在程式碼中的使用方式概觀。</span><span class="sxs-lookup"><span data-stu-id="a923f-106">This article explains what the WebJobs SDK is, reviews some common scenarios it is useful for, and gives an overview of how you use it in your code.</span></span>

[!INCLUDE [app-service-web-webjobs-corenote](../../includes/app-service-web-webjobs-corenote.md)]

<span data-ttu-id="a923f-107">[WebJobs](websites-webjobs-resources.md) 是一項 Azure App Service 功能，可讓您在與 Web 應用程式、API 應用程式或行動應用程式相同的內容中執行程式或指令碼。</span><span class="sxs-lookup"><span data-stu-id="a923f-107">[WebJobs](websites-webjobs-resources.md) is a feature of Azure App Service that enables you to run a program or script in the same context as a web app, API app, or mobile app.</span></span> <span data-ttu-id="a923f-108">[WebJobs SDK](websites-webjobs-resources.md) 的目的是為了簡化您為 WebJob 可執行的一般工作 (例如影像處理、佇列處理、RSS 彙總、檔案維護及傳送電子郵件) 撰寫的程式碼。</span><span class="sxs-lookup"><span data-stu-id="a923f-108">The purpose of the [WebJobs SDK](websites-webjobs-resources.md) is to simplify the code you write for common tasks that a WebJob can perform, such as image processing, queue processing, RSS aggregation, file maintenance, and sending emails.</span></span> <span data-ttu-id="a923f-109">WebJobs SDK 具有內建功能，用於處理 Azure 儲存體和服務匯流排、工作排程和處理錯誤，以及許多其他常見案例。</span><span class="sxs-lookup"><span data-stu-id="a923f-109">The WebJobs SDK has built-in features for working with Azure Storage and Service Bus, for scheduling tasks and handling errors, and for many other common scenarios.</span></span> <span data-ttu-id="a923f-110">此外，它已被設計成可延伸。</span><span class="sxs-lookup"><span data-stu-id="a923f-110">In addition, it's designed to be extensible.</span></span> <span data-ttu-id="a923f-111">[WebJobs SDK 是開放原始碼](https://github.com/Azure/azure-webjobs-sdk/)，並且有[擴充功能的開放原始碼儲存機制](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Binding-Extensions-Overview)。</span><span class="sxs-lookup"><span data-stu-id="a923f-111">The [WebJobs SDK is open source](https://github.com/Azure/azure-webjobs-sdk/), and there's an [open source repository for extensions](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Binding-Extensions-Overview).</span></span>

<span data-ttu-id="a923f-112">WebJobs SDK 包含下列元件：</span><span class="sxs-lookup"><span data-stu-id="a923f-112">The WebJobs SDK includes the following components:</span></span>

* <span data-ttu-id="a923f-113">**NuGet 封裝**。</span><span class="sxs-lookup"><span data-stu-id="a923f-113">**NuGet packages**.</span></span> <span data-ttu-id="a923f-114">您新增至 Visual Studio 主控台應用程式專案的 NuGet 封裝，會利用 WebJobs SDK 屬性修飾您的方法，提供一個供您程式碼使用的架構。</span><span class="sxs-lookup"><span data-stu-id="a923f-114">NuGet packages that you add to a Visual Studio Console Application project provide a framework that your code uses by decorating your methods with WebJobs SDK attributes.</span></span>
* <span data-ttu-id="a923f-115">**儀表板**。</span><span class="sxs-lookup"><span data-stu-id="a923f-115">**Dashboard**.</span></span> <span data-ttu-id="a923f-116">Azure App Service 中包含部分的 WebJobs SDK，該部份項目可針對使用 NuGet 封裝的程式提供豐富的監控和診斷功能。</span><span class="sxs-lookup"><span data-stu-id="a923f-116">Part of the WebJobs SDK is included in Azure App Service and provides rich monitoring and diagnostics for programs that use the NuGet packages.</span></span> <span data-ttu-id="a923f-117">您無需撰寫程式碼就可以使用這些監視和診斷功能。</span><span class="sxs-lookup"><span data-stu-id="a923f-117">You don't have to write code to use these monitoring and diagnostics features.</span></span>

## <span data-ttu-id="a923f-118"><a id="scenarios"></a>案例</span><span class="sxs-lookup"><span data-stu-id="a923f-118"><a id="scenarios"></a>Scenarios</span></span>
<span data-ttu-id="a923f-119">下列是 Azure WebJobs SDK 可協助您輕鬆處理的部分典型案例：</span><span class="sxs-lookup"><span data-stu-id="a923f-119">Here are some typical scenarios you can handle more easily with the Azure WebJobs SDK:</span></span>

* <span data-ttu-id="a923f-120">影像處理或其他需要大量 CPU 的工作。</span><span class="sxs-lookup"><span data-stu-id="a923f-120">Image processing or other CPU-intensive work.</span></span> <span data-ttu-id="a923f-121">網站的一項常見功能是上傳影像或影片的能力。</span><span class="sxs-lookup"><span data-stu-id="a923f-121">A common feature of websites is the ability to upload images or videos.</span></span> <span data-ttu-id="a923f-122">在許多時候，您想要在內容上傳後處理該內容，但又不想在您執行此作業時讓使用者等候。</span><span class="sxs-lookup"><span data-stu-id="a923f-122">Often you want to manipulate the content after it's uploaded, but you don't want to make the user wait while you do that.</span></span>
* <span data-ttu-id="a923f-123">佇列處理。</span><span class="sxs-lookup"><span data-stu-id="a923f-123">Queue processing.</span></span> <span data-ttu-id="a923f-124">Web 前端與後端服務的一個常見通訊方式是使用佇列。</span><span class="sxs-lookup"><span data-stu-id="a923f-124">A common way for a web frontend to communicate with a backend service is to use queues.</span></span> <span data-ttu-id="a923f-125">當網站需要完成工作時，它會將訊息推播至佇列。</span><span class="sxs-lookup"><span data-stu-id="a923f-125">When the website needs to get work done, it pushes a message onto a queue.</span></span> <span data-ttu-id="a923f-126">後端服務會從佇列提取訊息，並完成工作。</span><span class="sxs-lookup"><span data-stu-id="a923f-126">A backend service pulls messages from the queue and does the work.</span></span> <span data-ttu-id="a923f-127">您可以在影像處理中使用佇列：例如，在使用者上傳多個檔案之後，將檔案名稱放置於佇列訊息中，由後端挑選佇列訊息進行處理。</span><span class="sxs-lookup"><span data-stu-id="a923f-127">You could use queues for image processing: for example, after the user uploads a number of files, put the file names in a queue message to be picked up by the backend for processing.</span></span> <span data-ttu-id="a923f-128">或者您可以使用佇列來提升網站回應能力。</span><span class="sxs-lookup"><span data-stu-id="a923f-128">Or you could use queues to improve site responsiveness.</span></span> <span data-ttu-id="a923f-129">例如，與其將目錄直接寫入 SQL Database，請寫入佇列並告知使用者已完成，然後由後端服務處理高延遲的關聯式資料庫工作。</span><span class="sxs-lookup"><span data-stu-id="a923f-129">For example, instead of writing directly to a SQL database, write to a queue, tell the user you're done, and let the backend service handle high-latency relational database work.</span></span> <span data-ttu-id="a923f-130">如需使用影像處理的佇列處理範例，請參閱 [WebJobs SDK 入門教學課程](websites-dotnet-webjobs-sdk-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="a923f-130">For an example of queue processing with image process, see the [WebJobs SDK Get Started tutorial](websites-dotnet-webjobs-sdk-get-started.md).</span></span>
* <span data-ttu-id="a923f-131">RSS 彙總。</span><span class="sxs-lookup"><span data-stu-id="a923f-131">RSS aggregation.</span></span> <span data-ttu-id="a923f-132">如果您有維持 RSS 摘要清單的網站，您可以在背景處理序中提取摘要的所有文章。</span><span class="sxs-lookup"><span data-stu-id="a923f-132">If you have a site that maintains a list of RSS feeds, you could pull in all of the articles from the feeds in a background process.</span></span>
* <span data-ttu-id="a923f-133">檔案維護，例如彙總或清除記錄檔案。</span><span class="sxs-lookup"><span data-stu-id="a923f-133">File maintenance, such as aggregating or cleaning up log files.</span></span>  <span data-ttu-id="a923f-134">您可能擁有由數個網站在不同的時間範圍內所建立的記錄檔案，您想要結合這些檔案以便執行分析工作。</span><span class="sxs-lookup"><span data-stu-id="a923f-134">You might have log files being created by several sites or for separate time spans which you want to combine in order to run analysis jobs on them.</span></span> <span data-ttu-id="a923f-135">或者您想要排程每週執行的工作，來將舊的記錄檔案清除。</span><span class="sxs-lookup"><span data-stu-id="a923f-135">Or you might want to schedule a task to run weekly to clean up old log files.</span></span>
* <span data-ttu-id="a923f-136">輸入 Azure 資料表。</span><span class="sxs-lookup"><span data-stu-id="a923f-136">Ingress into Azure Tables.</span></span> <span data-ttu-id="a923f-137">您可能會有想要剖析的儲存檔案和 Blob，並想要將資料儲存在資料表中。</span><span class="sxs-lookup"><span data-stu-id="a923f-137">You might have files stored and blobs and want to parse them and store the data in tables.</span></span> <span data-ttu-id="a923f-138">輸入函數可能會寫入許多行 (在某些情況下可能有上百萬行)，而 WebJobs SDK 讓您可以輕易地實作此功能。</span><span class="sxs-lookup"><span data-stu-id="a923f-138">The ingress function could be writing lots of rows (millions in some cases), and the WebJobs SDK makes it possible to implement this functionality easily.</span></span> <span data-ttu-id="a923f-139">SDK 還提供進度指標的即時監控，例如資料表中的寫入行數。</span><span class="sxs-lookup"><span data-stu-id="a923f-139">The SDK also provides real-time monitoring of progress indicators such as the number of rows written in the table.</span></span>
* <span data-ttu-id="a923f-140">其他您想要在背景執行序中執行的長時間執行工作，例如 [傳送電子郵件](https://github.com/victorhurdugaci/AzureWebJobsSamples/tree/master/SendEmailOnFailure)。</span><span class="sxs-lookup"><span data-stu-id="a923f-140">Other long-running tasks that you want to run in a background thread, such as [sending emails](https://github.com/victorhurdugaci/AzureWebJobsSamples/tree/master/SendEmailOnFailure).</span></span> 
* <span data-ttu-id="a923f-141">任何您想要依排程執行的工作，例如每晚執行備份作業。</span><span class="sxs-lookup"><span data-stu-id="a923f-141">Any tasks that you want to run on a schedule, such as performing a back-up operation every night.</span></span>

<span data-ttu-id="a923f-142">在這些許多情況中，您可能會想要擴充 Web 應用程式以便在多個 VM 上執行，這會同時執行多個 WebJobs。</span><span class="sxs-lookup"><span data-stu-id="a923f-142">In many of these scenarios you may want to scale a web app to run on multiple VMs, which would run multiple WebJobs simultaneously.</span></span> <span data-ttu-id="a923f-143">在某些情況下，這可能會導致相同資料多次進行處理，但當您使用內建佇列、blob 和 WebJobs SDK 的服務匯流排觸發程序時，這不會造成問題。</span><span class="sxs-lookup"><span data-stu-id="a923f-143">In some scenarios this could result in the same data getting processed multiple times, but this is not a problem when you use the built-in queue, blob, and Service Bus triggers of the WebJobs SDK.</span></span> <span data-ttu-id="a923f-144">SDK 可確保您的函式針對每個訊息或 blob 僅會處理一次。</span><span class="sxs-lookup"><span data-stu-id="a923f-144">The SDK ensures that your functions will be processed only once for each message or blob.</span></span>

<span data-ttu-id="a923f-145">WebJobs SDK 也可讓您輕鬆地處理常見的錯誤處理案例。</span><span class="sxs-lookup"><span data-stu-id="a923f-145">The WebJobs SDK also makes it easy to handle common error handling scenarios.</span></span> <span data-ttu-id="a923f-146">您可以設定警示以在函式失敗時傳送通知，還可以設定逾時，讓函式未在指定的時間限制內完成時自動取消。</span><span class="sxs-lookup"><span data-stu-id="a923f-146">You can set up alerts to send notifications when a function fails, and you can set timeouts so that a function is automatically canceled if it doesn't complete within a specified time limit.</span></span>

## <span data-ttu-id="a923f-147"><a id="code"></a> 程式碼範例</span><span class="sxs-lookup"><span data-stu-id="a923f-147"><a id="code"></a> Code samples</span></span>
<span data-ttu-id="a923f-148">使用 Azure 儲存體的處理傳統工作程式碼十分簡單。</span><span class="sxs-lookup"><span data-stu-id="a923f-148">The code for handling typical tasks that work with Azure Storage is simple.</span></span> <span data-ttu-id="a923f-149">在您「主控台應用程式」的 `Main` 方法中，您會建立一個 `JobHost` 物件來協調對您所撰寫之方法的呼叫。</span><span class="sxs-lookup"><span data-stu-id="a923f-149">In your Console Application's `Main` method you create a `JobHost` object that coordinates the calls to methods you write.</span></span> <span data-ttu-id="a923f-150">WebJobs SDK 架構會根據您在方法中使用的 WebJobs SDK 屬性，知道何時要呼叫方法及要使用哪些參數值。</span><span class="sxs-lookup"><span data-stu-id="a923f-150">The WebJobs SDK framework knows when to call your methods and what parameter values to use based on the WebJobs SDK attributes you use in them.</span></span> <span data-ttu-id="a923f-151">SDK 提供可指定造成呼叫函式之條件的「觸發程序」，以及可指定如何將資訊傳入方法參數及從方法參數傳出的「繫結器」。</span><span class="sxs-lookup"><span data-stu-id="a923f-151">The SDK provides *triggers* that specify what conditions cause the function to be called, and *binders* that specify how to get information into and out of method parameters.</span></span>

<span data-ttu-id="a923f-152">例如， [QueueTrigger](websites-dotnet-webjobs-sdk-storage-queues-how-to.md) 屬性會導致在佇列上收到訊息時呼叫函式，並且如果位元組陣列或自訂類型的訊息格式為 JSON，就會將該訊息自動還原序列化。</span><span class="sxs-lookup"><span data-stu-id="a923f-152">For example, the [QueueTrigger](websites-dotnet-webjobs-sdk-storage-queues-how-to.md) attribute causes a function to be called when a message is received on a queue, and if the message format is JSON for a byte array or a custom type, the message is automatically deserialized.</span></span> <span data-ttu-id="a923f-153">每當 Azure 儲存體帳戶中有新的 Blob 建立時， [BlobTrigger](websites-dotnet-webjobs-sdk-storage-blobs-how-to.md) 屬性就會觸發程序。</span><span class="sxs-lookup"><span data-stu-id="a923f-153">The [BlobTrigger](websites-dotnet-webjobs-sdk-storage-blobs-how-to.md) attribute triggers a process whenever a new blob is created in an Azure Storage account.</span></span>

<span data-ttu-id="a923f-154">下列是個簡單程式，可用來輪詢佇列並為收到的每則佇列訊息建立 Blob：</span><span class="sxs-lookup"><span data-stu-id="a923f-154">Here is a simple program that polls a queue and creates a blob for each queue message received:</span></span>

        public static void Main()
        {
            JobHost host = new JobHost();
            host.RunAndBlock();
        }

        public static void ProcessQueueMessage([QueueTrigger("webjobsqueue")] string inputText, 
            [Blob("containername/blobname")]TextWriter writer)
        {
            writer.WriteLine(inputText);
        }

<span data-ttu-id="a923f-155">`JobHost` 物件是一組背景功能的容器。</span><span class="sxs-lookup"><span data-stu-id="a923f-155">The `JobHost` object is a container for a set of background functions.</span></span> <span data-ttu-id="a923f-156">`JobHost` 物件可監視功能、注意可觸發功能的事件，以及發生觸發事件時執行功能。</span><span class="sxs-lookup"><span data-stu-id="a923f-156">The `JobHost` object monitors the functions, watches for events that trigger them, and executes the functions when trigger events occur.</span></span> <span data-ttu-id="a923f-157">您可以呼叫 `JobHost` 方法，指出您要在目前執行緒或背景執行緒上執行容器程序。</span><span class="sxs-lookup"><span data-stu-id="a923f-157">You call a `JobHost` method to indicate whether you want the container process to run on the current thread or a background thread.</span></span> <span data-ttu-id="a923f-158">在此範例中， `RunAndBlock` 方法會在目前執行緒上持續執行程序。</span><span class="sxs-lookup"><span data-stu-id="a923f-158">In the example, the `RunAndBlock` method runs the process continuously on the current thread.</span></span>

<span data-ttu-id="a923f-159">由於此範例中的 `ProcessQueueMessage` 方法具有 `QueueTrigger` 屬性，接收新的佇列訊息時便會觸發該功能。</span><span class="sxs-lookup"><span data-stu-id="a923f-159">Because the `ProcessQueueMessage` method in this example has a `QueueTrigger` attribute, the trigger for that function is the reception of a new queue message.</span></span> <span data-ttu-id="a923f-160">`JobHost` 物件會注意指定佇列 (在此範例中是 "webjobsqueue") 上的新佇列訊息，找到新佇列訊息時，此物件便會呼叫 `ProcessQueueMessage`。</span><span class="sxs-lookup"><span data-stu-id="a923f-160">The `JobHost` object watches for new queue messages on the specified queue ("webjobsqueue" in this sample) and when one is found, it calls `ProcessQueueMessage`.</span></span> 

<span data-ttu-id="a923f-161">`QueueTrigger` 屬性會將 `inputText` 參數繫結至佇列訊息的值。</span><span class="sxs-lookup"><span data-stu-id="a923f-161">The `QueueTrigger` attribute binds the `inputText` parameter to the value of the queue message.</span></span> <span data-ttu-id="a923f-162">而 `Blob` 屬性則會將 `TextWriter` 物件繫結至名為 "containername" 容器中名為 "blobname" 的 Blob。</span><span class="sxs-lookup"><span data-stu-id="a923f-162">And the `Blob` attribute binds a `TextWriter` object to a blob named "blobname" in a container named "containername".</span></span>  

        public static void ProcessQueueMessage([QueueTrigger("webjobsqueue")]] string inputText, 
            [Blob("containername/blobname")]TextWriter writer)

<span data-ttu-id="a923f-163">此功能會接著使用這些參數來將佇列訊息的值寫入 Blob：</span><span class="sxs-lookup"><span data-stu-id="a923f-163">The function then uses these parameters to write the value of the queue message to the blob:</span></span>

        writer.WriteLine(inputText);

<span data-ttu-id="a923f-164">WebJobs SDK 的觸發程序和繫結器功能可大幅簡化您所必須撰寫的程式碼。</span><span class="sxs-lookup"><span data-stu-id="a923f-164">The trigger and binder features of the WebJobs SDK greatly simplify the code you have to write.</span></span> <span data-ttu-id="a923f-165">WebJobs SDK 架構會為您完成處理佇列、Blob 或檔案或是起始已排定的工作所需的低階程式碼。</span><span class="sxs-lookup"><span data-stu-id="a923f-165">The low-level code required to process queues, blobs, or files, or to initiate scheduled tasks, is done for you by the WebJobs SDK framework.</span></span> <span data-ttu-id="a923f-166">例如，此架構會建立尚未存在的佇列、開啟佇列、讀取佇列訊息、在處理完成後刪除佇列訊息、建立尚未存在的 Blob 容器、寫入 Blob 等。</span><span class="sxs-lookup"><span data-stu-id="a923f-166">For example, the framework creates queues that don't exist yet, opens the queue, reads queue messages, deletes queue messages when processing is completed, creates blob containers that don't exist yet, writes to blobs, and so on.</span></span>

<span data-ttu-id="a923f-167">下列程式碼範例以一個 WebJob 示範各種不同的觸發程序：`QueueTrigger`、`FileTrigger`、`WebHookTrigger` 及 `ErrorTrigger`。</span><span class="sxs-lookup"><span data-stu-id="a923f-167">The following code example shows a variety of triggers in one WebJob: `QueueTrigger`, `FileTrigger`, `WebHookTrigger`, and `ErrorTrigger`.</span></span> 

```
    public class Functions
    {
        public static void ProcessQueueMessage([QueueTrigger("queue")] string message,
        TextWriter log)
        {
            log.WriteLine(message);
        }

        public static void ProcessFileAndUploadToBlob(
            [FileTrigger(@"import\{name}", "*.*", autoDelete: true)] Stream file,
            [Blob(@"processed/{name}", FileAccess.Write)] Stream output,
            string name,
            TextWriter log)
        {
            output = file;
            file.Close();
            log.WriteLine(string.Format("Processed input file '{0}'!", name));
        }

        [Singleton]
        public static void ProcessWebHookA([WebHookTrigger] string body, TextWriter log)
        {
            log.WriteLine(string.Format("WebHookA invoked! Body: {0}", body));
        }

        public static void ProcessGitHubWebHook([WebHookTrigger] string body, TextWriter log)
        {
            dynamic issueEvent = JObject.Parse(body);
            log.WriteLine(string.Format("GitHub WebHook invoked! ('{0}', '{1}')",
                issueEvent.issue.title, issueEvent.action));
        }

        public static void ErrorMonitor(
        [ErrorTrigger("00:01:00", 1)] TraceFilter filter, TextWriter log,
        [SendGrid(
            To = "admin@emailaddress.com",
            Subject = "Error!")]
         SendGridMessage message)
        {
            // log last 5 detailed errors to the Dashboard
            log.WriteLine(filter.GetDetailedMessage(5));
            message.Text = filter.GetDetailedMessage(1);
        }
    }
```

## <span data-ttu-id="a923f-168"><a id="schedule"></a> 排程</span><span class="sxs-lookup"><span data-stu-id="a923f-168"><a id="schedule"></a> Scheduling</span></span>
<span data-ttu-id="a923f-169">`TimerTrigger` 屬性可讓您依排程觸發函式執行。</span><span class="sxs-lookup"><span data-stu-id="a923f-169">The `TimerTrigger` attribute gives you the ability to trigger functions to run on a schedule.</span></span> <span data-ttu-id="a923f-170">您可以透過 Azure 來進行 WebJob 的整體排程，或是使用 WebJobs SDK `TimerTrigger`來排定 WebJob 的個別函式。</span><span class="sxs-lookup"><span data-stu-id="a923f-170">You can schedule a WebJob as a whole through Azure or schedule individual functions of a WebJob using the WebJobs SDK `TimerTrigger`.</span></span> <span data-ttu-id="a923f-171">以下是程式碼範例。</span><span class="sxs-lookup"><span data-stu-id="a923f-171">Here's a code sample.</span></span>

```
public class Functions
{
    public static void ProcessTimer([TimerTrigger("*/15 * * * * *", RunOnStartup = true)]
    TimerInfo info, [Queue("queue")] out string message)
    {
        message = info.FormatNextOccurrences(1);
    }
}
```

<span data-ttu-id="a923f-172">如需詳細範例程式碼，請參閱 GitHub.com 上 azure-webjobs-sdk-extensions 存放庫中的 [TimerSamples.cs](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/ExtensionsSample/Samples/TimerSamples.cs) 。</span><span class="sxs-lookup"><span data-stu-id="a923f-172">For more sample code, see [TimerSamples.cs](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/ExtensionsSample/Samples/TimerSamples.cs) in the azure-webjobs-sdk-extensions repository on GitHub.com.</span></span>

## <a name="extensibility"></a><span data-ttu-id="a923f-173">擴充性</span><span class="sxs-lookup"><span data-stu-id="a923f-173">Extensibility</span></span>
<span data-ttu-id="a923f-174">您並不受限於使用內建功能 -- WebJobs SDK 可讓您撰寫自訂的觸發程序和繫結器。</span><span class="sxs-lookup"><span data-stu-id="a923f-174">You're not limited to built-in functionality -- the WebJobs SDK allows you to write custom triggers and binders.</span></span>  <span data-ttu-id="a923f-175">例如，您可以撰寫用於快取事件和定期排程的觸發程序。</span><span class="sxs-lookup"><span data-stu-id="a923f-175">For example, you can write triggers for cache events and periodic schedules.</span></span> <span data-ttu-id="a923f-176">[開放原始碼存放庫](https://github.com/Azure/azure-webjobs-sdk-extensions)包含[關於 WebJobs SDK 擴充性的詳細指南](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Binding-Extensions-Overview)和範例程式碼，可幫助您開始撰寫自己的觸發程序和繫結器。</span><span class="sxs-lookup"><span data-stu-id="a923f-176">An [open source repository](https://github.com/Azure/azure-webjobs-sdk-extensions) contains a [detailed guide on WebJobs SDK extensibility](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Binding-Extensions-Overview) and sample code to help get you started writing your own triggers and binders.</span></span>

## <span data-ttu-id="a923f-177"><a id="workerrole"></a>在 WebJobs 外部使用 WebJobs SDK</span><span class="sxs-lookup"><span data-stu-id="a923f-177"><a id="workerrole"></a>Using the WebJobs SDK outside of WebJobs</span></span>
<span data-ttu-id="a923f-178">使用 WebJobs SDK 的程式是指可在任意位置執行的標準主控台應用程式 -- 它不一定要以 WebJob 的形式執行。</span><span class="sxs-lookup"><span data-stu-id="a923f-178">A program that uses the the WebJobs SDK is a standard Console Application and can run anywhere -- it doesn't have to run as a WebJob.</span></span> <span data-ttu-id="a923f-179">您可以在開發電腦上本機測試程式，並在實際執行環境中，以雲端服務背景工作角色或 Windows 服務的身分執行此程式 (如果您慣用其中一個環境)。</span><span class="sxs-lookup"><span data-stu-id="a923f-179">You can test the program locally on your development computer, and in production you can run it in a Cloud Service worker role or a Windows service if you prefer one of those environments.</span></span> 

<span data-ttu-id="a923f-180">不過，對於 Azure App Service Web 應用程式，儀表板只能做為延伸模組來使用。</span><span class="sxs-lookup"><span data-stu-id="a923f-180">However, the dashboard is only available as an extension for an Azure App Service web app.</span></span> <span data-ttu-id="a923f-181">如果您想要在 WebJob 外部執行但仍然使用儀表板，則您可以設定 Web 應用程式使用 WebJobs SDK 儀表板連接字串所參考的相同儲存體帳戶，接著該 Web 應用程式的 WebJobs 儀表板便會顯示有關這個異地執行程式中的執行函數資料。</span><span class="sxs-lookup"><span data-stu-id="a923f-181">If you want to run outside of a WebJob and still use the Dashboard, you can configure a web app to use the same storage account that your WebJobs SDK Dashboard connection string refers to, and that web app's WebJobs Dashboard will then show data about function execution from your program that is running somewhere else.</span></span> <span data-ttu-id="a923f-182">您可以使用 URL https://*{webappname}*.scm.azurewebsites.net/azurejobs/#/functions 進入儀表板。</span><span class="sxs-lookup"><span data-stu-id="a923f-182">You can get to the Dashboard by using the URL https://*{webappname}*.scm.azurewebsites.net/azurejobs/#/functions.</span></span> <span data-ttu-id="a923f-183">如需詳細資訊，請參閱 [使用 WebJobs SDK 來取得本機開發的儀表板](http://blogs.msdn.com/b/jmstall/archive/2014/01/27/getting-a-dashboard-for-local-development-with-the-webjobs-sdk.aspx)(英文)，但請注意，此部落格文章顯示舊的連接字串名稱。</span><span class="sxs-lookup"><span data-stu-id="a923f-183">For more information, see [Getting a dashboard for local development with the WebJobs SDK](http://blogs.msdn.com/b/jmstall/archive/2014/01/27/getting-a-dashboard-for-local-development-with-the-webjobs-sdk.aspx), but note that the blog post shows an old connection string name.</span></span> 

## <span data-ttu-id="a923f-184"><a id="nostorage"></a>儀表板功能</span><span class="sxs-lookup"><span data-stu-id="a923f-184"><a id="nostorage"></a>Dashboard features</span></span>
<span data-ttu-id="a923f-185">即使您不使用 WebJobs SDK 觸發程序或繫結器，WebJobs SDK 仍可提供數個好處：</span><span class="sxs-lookup"><span data-stu-id="a923f-185">The WebJobs SDK provides several advantages even if you don't use WebJobs SDK triggers or binders:</span></span>

* <span data-ttu-id="a923f-186">您可以從儀表板叫用函數。</span><span class="sxs-lookup"><span data-stu-id="a923f-186">You can invoke functions from the Dashboard.</span></span>
* <span data-ttu-id="a923f-187">您可以從儀表板轉送函數。</span><span class="sxs-lookup"><span data-stu-id="a923f-187">You can replay functions from the Dashboard.</span></span>
* <span data-ttu-id="a923f-188">您可以在儀表板中檢視記錄檔，連結到特定的 WebJob (使用 Console.Out、Console.Error、Trace 等編寫的應用程式記錄檔) 或連結到產生它們的特定函式引動過程 (使用 SDK 傳遞至函數做為參數的 `TextWriter` 物件編寫的記錄檔)。</span><span class="sxs-lookup"><span data-stu-id="a923f-188">You can view logs in the Dashboard, linked to the particular WebJob (application logs, written by using Console.Out, Console.Error, Trace, etc.) or linked to the particular function invocation that generated them (logs written by using a `TextWriter` object that the SDK passes to the function as a parameter).</span></span> 

<span data-ttu-id="a923f-189">如需詳細資訊，請參閱[如何手動叫用函數](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#manual)和[如何寫入記錄](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#logs)</span><span class="sxs-lookup"><span data-stu-id="a923f-189">For more information, see [How to manually invoke a function](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#manual) and [How to write logs](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#logs)</span></span> 

## <span data-ttu-id="a923f-190"><a id="nextsteps"></a>接續步驟</span><span class="sxs-lookup"><span data-stu-id="a923f-190"><a id="nextsteps"></a>Next steps</span></span>
<span data-ttu-id="a923f-191">如需 WebJobs SDK 的詳細資訊，請參閱 [Azure WebJobs 建議使用的資源](http://go.microsoft.com/fwlink/?linkid=390226)。</span><span class="sxs-lookup"><span data-stu-id="a923f-191">For more information about the WebJobs SDK, see [Azure WebJobs Recommended Resources](http://go.microsoft.com/fwlink/?linkid=390226).</span></span>

<span data-ttu-id="a923f-192">如需有關 WebJobs SDK 最新增強功能的資訊，請參閱 [版本資訊](https://github.com/Azure/azure-webjobs-sdk/wiki/Release-Notes)。</span><span class="sxs-lookup"><span data-stu-id="a923f-192">For information about the latest enhancements to the WebJobs SDK, see the [Release Notes](https://github.com/Azure/azure-webjobs-sdk/wiki/Release-Notes).</span></span>

