---
title: "aaaWhat 為 hello Azure WebJobs SDK"
description: "簡介 toohello Azure WebJobs SDK。 說明哪些 hello SDK，一般的案例很有用，而且程式碼範例。"
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
ms.openlocfilehash: efac7a75c3b68a6a6601fb298f2ccac9bd71709d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-hello-azure-webjobs-sdk"></a><span data-ttu-id="ebe3b-104">Hello Azure WebJobs SDK 是什麼</span><span class="sxs-lookup"><span data-stu-id="ebe3b-104">What is hello Azure WebJobs SDK</span></span>
## <span data-ttu-id="ebe3b-105"><a id="overview"></a>概觀</span><span class="sxs-lookup"><span data-stu-id="ebe3b-105"><a id="overview"></a>Overview</span></span>
<span data-ttu-id="ebe3b-106">這篇文章會說明什麼 hello WebJobs SDK 是的會檢閱一些常見的案例很有用，並提供如何使用它在程式碼中的概觀。</span><span class="sxs-lookup"><span data-stu-id="ebe3b-106">This article explains what hello WebJobs SDK is, reviews some common scenarios it is useful for, and gives an overview of how you use it in your code.</span></span>

[!INCLUDE [app-service-web-webjobs-corenote](../../includes/app-service-web-webjobs-corenote.md)]

<span data-ttu-id="ebe3b-107">[WebJobs](websites-webjobs-resources.md)程式或指令碼在 hello 是 toorun 可讓您的 Azure 應用程式服務的功能為 web 應用程式、 應用程式開發介面應用程式或行動裝置應用程式相同的內容。</span><span class="sxs-lookup"><span data-stu-id="ebe3b-107">[WebJobs](websites-webjobs-resources.md) is a feature of Azure App Service that enables you toorun a program or script in hello same context as a web app, API app, or mobile app.</span></span> <span data-ttu-id="ebe3b-108">hello 目的 hello [WebJobs SDK](websites-webjobs-resources.md) toosimplify hello 程式碼，您可以執行的 WebJob，例如映像處理、 佇列的處理、 RSS 彙總、 檔案維護的一般工作為撰寫，且傳送電子郵件。</span><span class="sxs-lookup"><span data-stu-id="ebe3b-108">hello purpose of hello [WebJobs SDK](websites-webjobs-resources.md) is toosimplify hello code you write for common tasks that a WebJob can perform, such as image processing, queue processing, RSS aggregation, file maintenance, and sending emails.</span></span> <span data-ttu-id="ebe3b-109">hello WebJobs SDK 有內建的功能，使用 Azure 儲存體和 Service Bus、 工作排程和處理錯誤，以及許多其他常見的案例。</span><span class="sxs-lookup"><span data-stu-id="ebe3b-109">hello WebJobs SDK has built-in features for working with Azure Storage and Service Bus, for scheduling tasks and handling errors, and for many other common scenarios.</span></span> <span data-ttu-id="ebe3b-110">此外，其設計目的是 toobe 可延伸。</span><span class="sxs-lookup"><span data-stu-id="ebe3b-110">In addition, it's designed toobe extensible.</span></span> <span data-ttu-id="ebe3b-111">hello [WebJobs SDK 是開放原始碼](https://github.com/Azure/azure-webjobs-sdk/)，而且沒有[擴充功能的開放原始碼儲存機制](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Binding-Extensions-Overview)。</span><span class="sxs-lookup"><span data-stu-id="ebe3b-111">hello [WebJobs SDK is open source](https://github.com/Azure/azure-webjobs-sdk/), and there's an [open source repository for extensions](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Binding-Extensions-Overview).</span></span>

<span data-ttu-id="ebe3b-112">hello WebJobs SDK 包含下列元件的 hello:</span><span class="sxs-lookup"><span data-stu-id="ebe3b-112">hello WebJobs SDK includes hello following components:</span></span>

* <span data-ttu-id="ebe3b-113">**NuGet 封裝**。</span><span class="sxs-lookup"><span data-stu-id="ebe3b-113">**NuGet packages**.</span></span> <span data-ttu-id="ebe3b-114">您加入 tooa Visual Studio 主控台應用程式專案的 NuGet 套件提供一種架構，而將 WebJobs SDK 屬性與方法的程式碼使用。</span><span class="sxs-lookup"><span data-stu-id="ebe3b-114">NuGet packages that you add tooa Visual Studio Console Application project provide a framework that your code uses by decorating your methods with WebJobs SDK attributes.</span></span>
* <span data-ttu-id="ebe3b-115">**儀表板**。</span><span class="sxs-lookup"><span data-stu-id="ebe3b-115">**Dashboard**.</span></span> <span data-ttu-id="ebe3b-116">Hello WebJobs SDK 的一部分包含在 Azure 應用程式服務，並提供豐富的監視和診斷使用 hello NuGet 封裝的程式。</span><span class="sxs-lookup"><span data-stu-id="ebe3b-116">Part of hello WebJobs SDK is included in Azure App Service and provides rich monitoring and diagnostics for programs that use hello NuGet packages.</span></span> <span data-ttu-id="ebe3b-117">您不需要 toowrite 程式碼 toouse 這些監視和診斷功能。</span><span class="sxs-lookup"><span data-stu-id="ebe3b-117">You don't have toowrite code toouse these monitoring and diagnostics features.</span></span>

## <span data-ttu-id="ebe3b-118"><a id="scenarios"></a>案例</span><span class="sxs-lookup"><span data-stu-id="ebe3b-118"><a id="scenarios"></a>Scenarios</span></span>
<span data-ttu-id="ebe3b-119">以下是一些典型的案例，您可以更輕鬆地處理以 hello Azure WebJobs SDK:</span><span class="sxs-lookup"><span data-stu-id="ebe3b-119">Here are some typical scenarios you can handle more easily with hello Azure WebJobs SDK:</span></span>

* <span data-ttu-id="ebe3b-120">影像處理或其他需要大量 CPU 的工作。</span><span class="sxs-lookup"><span data-stu-id="ebe3b-120">Image processing or other CPU-intensive work.</span></span> <span data-ttu-id="ebe3b-121">網站的共通的功能是 hello 能力 tooupload 影像或視訊。</span><span class="sxs-lookup"><span data-stu-id="ebe3b-121">A common feature of websites is hello ability tooupload images or videos.</span></span> <span data-ttu-id="ebe3b-122">通常您之後想要 toomanipulate hello 內容上傳，但當您這麼做時，您不想 toomake hello 使用者等候。</span><span class="sxs-lookup"><span data-stu-id="ebe3b-122">Often you want toomanipulate hello content after it's uploaded, but you don't want toomake hello user wait while you do that.</span></span>
* <span data-ttu-id="ebe3b-123">佇列處理。</span><span class="sxs-lookup"><span data-stu-id="ebe3b-123">Queue processing.</span></span> <span data-ttu-id="ebe3b-124">與後端服務的 web 前端 toocommunicate 的常用方式是 toouse 佇列。</span><span class="sxs-lookup"><span data-stu-id="ebe3b-124">A common way for a web frontend toocommunicate with a backend service is toouse queues.</span></span> <span data-ttu-id="ebe3b-125">當 hello 網站需要 tooget 工作完成時，它會推送到佇列的訊息。</span><span class="sxs-lookup"><span data-stu-id="ebe3b-125">When hello website needs tooget work done, it pushes a message onto a queue.</span></span> <span data-ttu-id="ebe3b-126">後端服務會從 hello 佇列提取訊息，並沒有 hello 工作。</span><span class="sxs-lookup"><span data-stu-id="ebe3b-126">A backend service pulls messages from hello queue and does hello work.</span></span> <span data-ttu-id="ebe3b-127">您可以使用映像處理佇列： 例如，hello 使用者上傳的檔案數目之後，將 hello 檔案名稱以收取 hello 後端處理的佇列訊息 toobe。</span><span class="sxs-lookup"><span data-stu-id="ebe3b-127">You could use queues for image processing: for example, after hello user uploads a number of files, put hello file names in a queue message toobe picked up by hello backend for processing.</span></span> <span data-ttu-id="ebe3b-128">或者，您可以使用佇列 tooimprove 網站回應速度。</span><span class="sxs-lookup"><span data-stu-id="ebe3b-128">Or you could use queues tooimprove site responsiveness.</span></span> <span data-ttu-id="ebe3b-129">例如，而不是直接寫入 tooa SQL database，撰寫 tooa 佇列，告訴您完成時，並讓 hello 後端服務控制代碼高延遲關聯式資料庫工作的 hello 使用者。</span><span class="sxs-lookup"><span data-stu-id="ebe3b-129">For example, instead of writing directly tooa SQL database, write tooa queue, tell hello user you're done, and let hello backend service handle high-latency relational database work.</span></span> <span data-ttu-id="ebe3b-130">如需佇列處理的映像程序的範例，請參閱 hello [WebJobs SDK 快速入門教學課程](websites-dotnet-webjobs-sdk-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="ebe3b-130">For an example of queue processing with image process, see hello [WebJobs SDK Get Started tutorial](websites-dotnet-webjobs-sdk-get-started.md).</span></span>
* <span data-ttu-id="ebe3b-131">RSS 彙總。</span><span class="sxs-lookup"><span data-stu-id="ebe3b-131">RSS aggregation.</span></span> <span data-ttu-id="ebe3b-132">如果您有站台維護的 RSS 摘要清單，您無法提取所有 hello 發行項的背景處理序中的 hello 摘要。</span><span class="sxs-lookup"><span data-stu-id="ebe3b-132">If you have a site that maintains a list of RSS feeds, you could pull in all of hello articles from hello feeds in a background process.</span></span>
* <span data-ttu-id="ebe3b-133">檔案維護，例如彙總或清除記錄檔案。</span><span class="sxs-lookup"><span data-stu-id="ebe3b-133">File maintenance, such as aggregating or cleaning up log files.</span></span>  <span data-ttu-id="ebe3b-134">您可能必須建立數個站台或不同的記錄檔時間範圍以您想 toocombine 中排序 toorun 分析作業在其上。</span><span class="sxs-lookup"><span data-stu-id="ebe3b-134">You might have log files being created by several sites or for separate time spans which you want toocombine in order toorun analysis jobs on them.</span></span> <span data-ttu-id="ebe3b-135">或者，您可能想 tooschedule 舊的記錄檔的工作 toorun 每週 tooclean。</span><span class="sxs-lookup"><span data-stu-id="ebe3b-135">Or you might want tooschedule a task toorun weekly tooclean up old log files.</span></span>
* <span data-ttu-id="ebe3b-136">輸入 Azure 資料表。</span><span class="sxs-lookup"><span data-stu-id="ebe3b-136">Ingress into Azure Tables.</span></span> <span data-ttu-id="ebe3b-137">您可能已儲存的檔案和 blob，並想 tooparse 它們 hello 資料並儲存在資料表。</span><span class="sxs-lookup"><span data-stu-id="ebe3b-137">You might have files stored and blobs and want tooparse them and store hello data in tables.</span></span> <span data-ttu-id="ebe3b-138">hello 輸入函式可能會寫入大量資料列 （在某些情況下包含數百萬），並 hello WebJobs SDK，讓可能 tooimplement 這項功能容易。</span><span class="sxs-lookup"><span data-stu-id="ebe3b-138">hello ingress function could be writing lots of rows (millions in some cases), and hello WebJobs SDK makes it possible tooimplement this functionality easily.</span></span> <span data-ttu-id="ebe3b-139">hello SDK 也提供即時監視進度指標，例如 hello 寫入 hello 資料表中的資料列數目。</span><span class="sxs-lookup"><span data-stu-id="ebe3b-139">hello SDK also provides real-time monitoring of progress indicators such as hello number of rows written in hello table.</span></span>
* <span data-ttu-id="ebe3b-140">其他長時間執行工作，例如要在背景執行緒、 toorun[傳送電子郵件](https://github.com/victorhurdugaci/AzureWebJobsSamples/tree/master/SendEmailOnFailure)。</span><span class="sxs-lookup"><span data-stu-id="ebe3b-140">Other long-running tasks that you want toorun in a background thread, such as [sending emails](https://github.com/victorhurdugaci/AzureWebJobsSamples/tree/master/SendEmailOnFailure).</span></span> 
* <span data-ttu-id="ebe3b-141">您想依排程，例如執行備份作業每晚 toorun 任何工作。</span><span class="sxs-lookup"><span data-stu-id="ebe3b-141">Any tasks that you want toorun on a schedule, such as performing a back-up operation every night.</span></span>

<span data-ttu-id="ebe3b-142">在許多案例中，您可能想 tooscale web 應用程式 toorun 上多個 Vm，就會同時執行多個 WebJobs。</span><span class="sxs-lookup"><span data-stu-id="ebe3b-142">In many of these scenarios you may want tooscale a web app toorun on multiple VMs, which would run multiple WebJobs simultaneously.</span></span> <span data-ttu-id="ebe3b-143">在某些情況下，這可能導致 hello 相同資料進行處理多次，但這不是 hello 的問題使用內建 hello 的佇列、 blob 和 Service Bus WebJobs SDK 的觸發程序時。</span><span class="sxs-lookup"><span data-stu-id="ebe3b-143">In some scenarios this could result in hello same data getting processed multiple times, but this is not a problem when you use hello built-in queue, blob, and Service Bus triggers of hello WebJobs SDK.</span></span> <span data-ttu-id="ebe3b-144">hello SDK 可確保您的函式將會一次處理的每個訊息或 blob。</span><span class="sxs-lookup"><span data-stu-id="ebe3b-144">hello SDK ensures that your functions will be processed only once for each message or blob.</span></span>

<span data-ttu-id="ebe3b-145">hello WebJobs SDK 也可讓您輕鬆 toohandle 常見的錯誤處理案例。</span><span class="sxs-lookup"><span data-stu-id="ebe3b-145">hello WebJobs SDK also makes it easy toohandle common error handling scenarios.</span></span> <span data-ttu-id="ebe3b-146">您可以設定警示通知 toosend 當函式失敗，並使函式會自動取消，如果它未在指定的時間限制內完成，您可以設定逾時。</span><span class="sxs-lookup"><span data-stu-id="ebe3b-146">You can set up alerts toosend notifications when a function fails, and you can set timeouts so that a function is automatically canceled if it doesn't complete within a specified time limit.</span></span>

## <span data-ttu-id="ebe3b-147"><a id="code"></a> 程式碼範例</span><span class="sxs-lookup"><span data-stu-id="ebe3b-147"><a id="code"></a> Code samples</span></span>
<span data-ttu-id="ebe3b-148">hello 處理可搭配 Azure 儲存體的一般工作的程式碼很簡單。</span><span class="sxs-lookup"><span data-stu-id="ebe3b-148">hello code for handling typical tasks that work with Azure Storage is simple.</span></span> <span data-ttu-id="ebe3b-149">在主控台應用程式的`Main`方法建立`JobHost`協調 hello 的物件呼叫的 toomethods 您撰寫。</span><span class="sxs-lookup"><span data-stu-id="ebe3b-149">In your Console Application's `Main` method you create a `JobHost` object that coordinates hello calls toomethods you write.</span></span> <span data-ttu-id="ebe3b-150">hello WebJobs SDK 架構知道當您的方法，及哪些參數值 toouse 根據 hello WebJobs SDK toocall 屬性中加以使用。</span><span class="sxs-lookup"><span data-stu-id="ebe3b-150">hello WebJobs SDK framework knows when toocall your methods and what parameter values toouse based on hello WebJobs SDK attributes you use in them.</span></span> <span data-ttu-id="ebe3b-151">hello SDK 提供*觸發程序*旗標會指定什麼條件會造成呼叫，hello 函式 toobe 和*繫結器*旗標會指定如何執行和跳離方法參數的 tooget 資訊。</span><span class="sxs-lookup"><span data-stu-id="ebe3b-151">hello SDK provides *triggers* that specify what conditions cause hello function toobe called, and *binders* that specify how tooget information into and out of method parameters.</span></span>

<span data-ttu-id="ebe3b-152">例如，hello [QueueTrigger](websites-dotnet-webjobs-sdk-storage-queues-how-to.md)屬性就會導致佇列接收訊息時，如果 hello 訊息格式的位元組陣列或自訂型別為 JSON，hello 訊息就會自動還原序列化時呼叫的函式 toobe。</span><span class="sxs-lookup"><span data-stu-id="ebe3b-152">For example, hello [QueueTrigger](websites-dotnet-webjobs-sdk-storage-queues-how-to.md) attribute causes a function toobe called when a message is received on a queue, and if hello message format is JSON for a byte array or a custom type, hello message is automatically deserialized.</span></span> <span data-ttu-id="ebe3b-153">hello [BlobTrigger](websites-dotnet-webjobs-sdk-storage-blobs-how-to.md)屬性觸發程序，每次在 Azure 儲存體帳戶中建立新的 blob。</span><span class="sxs-lookup"><span data-stu-id="ebe3b-153">hello [BlobTrigger](websites-dotnet-webjobs-sdk-storage-blobs-how-to.md) attribute triggers a process whenever a new blob is created in an Azure Storage account.</span></span>

<span data-ttu-id="ebe3b-154">下列是個簡單程式，可用來輪詢佇列並為收到的每則佇列訊息建立 Blob：</span><span class="sxs-lookup"><span data-stu-id="ebe3b-154">Here is a simple program that polls a queue and creates a blob for each queue message received:</span></span>

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

<span data-ttu-id="ebe3b-155">hello`JobHost`物件是一組背景函式的容器。</span><span class="sxs-lookup"><span data-stu-id="ebe3b-155">hello `JobHost` object is a container for a set of background functions.</span></span> <span data-ttu-id="ebe3b-156">hello`JobHost`物件監視 hello 函式、 監看觸發這些事件和觸發程序事件發生時執行 hello 函式。</span><span class="sxs-lookup"><span data-stu-id="ebe3b-156">hello `JobHost` object monitors hello functions, watches for events that trigger them, and executes hello functions when trigger events occur.</span></span> <span data-ttu-id="ebe3b-157">您呼叫`JobHost`方法 tooindicate 是否要在 hello 容器程序 toorun hello 目前的執行緒或背景執行緒。</span><span class="sxs-lookup"><span data-stu-id="ebe3b-157">You call a `JobHost` method tooindicate whether you want hello container process toorun on hello current thread or a background thread.</span></span> <span data-ttu-id="ebe3b-158">在 hello 範例 hello`RunAndBlock`方法 hello 程序會持續執行 hello 目前執行緒上。</span><span class="sxs-lookup"><span data-stu-id="ebe3b-158">In hello example, hello `RunAndBlock` method runs hello process continuously on hello current thread.</span></span>

<span data-ttu-id="ebe3b-159">因為 hello`ProcessQueueMessage`在此範例中的方法有`QueueTrigger`屬性，hello 觸發程序該函式是 hello 訊息接收的新佇列。</span><span class="sxs-lookup"><span data-stu-id="ebe3b-159">Because hello `ProcessQueueMessage` method in this example has a `QueueTrigger` attribute, hello trigger for that function is hello reception of a new queue message.</span></span> <span data-ttu-id="ebe3b-160">hello`JobHost`物件會監看 hello 指定佇列 (在此範例中為"webjobsqueue 」) 上的新佇列訊息，並找到一個物件，它會呼叫`ProcessQueueMessage`。</span><span class="sxs-lookup"><span data-stu-id="ebe3b-160">hello `JobHost` object watches for new queue messages on hello specified queue ("webjobsqueue" in this sample) and when one is found, it calls `ProcessQueueMessage`.</span></span> 

<span data-ttu-id="ebe3b-161">hello`QueueTrigger`屬性繫結 hello `inputText` hello 佇列訊息的參數 toohello 值。</span><span class="sxs-lookup"><span data-stu-id="ebe3b-161">hello `QueueTrigger` attribute binds hello `inputText` parameter toohello value of hello queue message.</span></span> <span data-ttu-id="ebe3b-162">和 hello`Blob`屬性繫結`TextWriter`物件 tooa blob 名為"blobname"中名為 「 容器名稱 」 的容器。</span><span class="sxs-lookup"><span data-stu-id="ebe3b-162">And hello `Blob` attribute binds a `TextWriter` object tooa blob named "blobname" in a container named "containername".</span></span>  

        public static void ProcessQueueMessage([QueueTrigger("webjobsqueue")]] string inputText, 
            [Blob("containername/blobname")]TextWriter writer)

<span data-ttu-id="ebe3b-163">hello 函式，然後使用 hello 佇列訊息 toohello blob 這些參數 toowrite hello 值：</span><span class="sxs-lookup"><span data-stu-id="ebe3b-163">hello function then uses these parameters toowrite hello value of hello queue message toohello blob:</span></span>

        writer.WriteLine(inputText);

<span data-ttu-id="ebe3b-164">hello hello WebJobs SDK 的觸發程序和繫結器功能大幅簡化您有 toowrite hello 程式碼。</span><span class="sxs-lookup"><span data-stu-id="ebe3b-164">hello trigger and binder features of hello WebJobs SDK greatly simplify hello code you have toowrite.</span></span> <span data-ttu-id="ebe3b-165">hello 低層級所需的程式碼 tooprocess 佇列、 blob 或檔案或 tooinitiate 排定工作，會為您完成以上 hello WebJobs SDK 架構。</span><span class="sxs-lookup"><span data-stu-id="ebe3b-165">hello low-level code required tooprocess queues, blobs, or files, or tooinitiate scheduled tasks, is done for you by hello WebJobs SDK framework.</span></span> <span data-ttu-id="ebe3b-166">例如，hello 架構建立並不存在的佇列、 開啟 hello 佇列、 讀取佇列訊息、 刪除佇列訊息，當處理完成時，會建立 blob 容器不存在於尚未，寫入 tooblobs，依此類推。</span><span class="sxs-lookup"><span data-stu-id="ebe3b-166">For example, hello framework creates queues that don't exist yet, opens hello queue, reads queue messages, deletes queue messages when processing is completed, creates blob containers that don't exist yet, writes tooblobs, and so on.</span></span>

<span data-ttu-id="ebe3b-167">hello 下列程式碼範例顯示各種不同的觸發程序中一個 WebJob: `QueueTrigger`， `FileTrigger`， `WebHookTrigger`，和`ErrorTrigger`。</span><span class="sxs-lookup"><span data-stu-id="ebe3b-167">hello following code example shows a variety of triggers in one WebJob: `QueueTrigger`, `FileTrigger`, `WebHookTrigger`, and `ErrorTrigger`.</span></span> 

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
            too= "admin@emailaddress.com",
            Subject = "Error!")]
         SendGridMessage message)
        {
            // log last 5 detailed errors toohello Dashboard
            log.WriteLine(filter.GetDetailedMessage(5));
            message.Text = filter.GetDetailedMessage(1);
        }
    }
```

## <span data-ttu-id="ebe3b-168"><a id="schedule"></a> 排程</span><span class="sxs-lookup"><span data-stu-id="ebe3b-168"><a id="schedule"></a> Scheduling</span></span>
<span data-ttu-id="ebe3b-169">hello`TimerTrigger`屬性可提供 hello 能力 tootrigger 函式 toorun 的排程。</span><span class="sxs-lookup"><span data-stu-id="ebe3b-169">hello `TimerTrigger` attribute gives you hello ability tootrigger functions toorun on a schedule.</span></span> <span data-ttu-id="ebe3b-170">因為整個透過 Azure 或排程個別函式的 WebJob 使用 hello WebJobs SDK，您可以排程 WebJob `TimerTrigger`。</span><span class="sxs-lookup"><span data-stu-id="ebe3b-170">You can schedule a WebJob as a whole through Azure or schedule individual functions of a WebJob using hello WebJobs SDK `TimerTrigger`.</span></span> <span data-ttu-id="ebe3b-171">以下是程式碼範例。</span><span class="sxs-lookup"><span data-stu-id="ebe3b-171">Here's a code sample.</span></span>

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

<span data-ttu-id="ebe3b-172">如需範例程式碼，請參閱[TimerSamples.cs](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/ExtensionsSample/Samples/TimerSamples.cs)上 GitHub.com hello azure webjobs sdk-副檔名儲存機制中。</span><span class="sxs-lookup"><span data-stu-id="ebe3b-172">For more sample code, see [TimerSamples.cs](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/ExtensionsSample/Samples/TimerSamples.cs) in hello azure-webjobs-sdk-extensions repository on GitHub.com.</span></span>

## <a name="extensibility"></a><span data-ttu-id="ebe3b-173">擴充性</span><span class="sxs-lookup"><span data-stu-id="ebe3b-173">Extensibility</span></span>
<span data-ttu-id="ebe3b-174">Toobuilt 中不受限於功能-hello WebJobs SDK 可讓您 toowrite 自訂觸發程序和繫結器。</span><span class="sxs-lookup"><span data-stu-id="ebe3b-174">You're not limited toobuilt-in functionality -- hello WebJobs SDK allows you toowrite custom triggers and binders.</span></span>  <span data-ttu-id="ebe3b-175">例如，您可以撰寫用於快取事件和定期排程的觸發程序。</span><span class="sxs-lookup"><span data-stu-id="ebe3b-175">For example, you can write triggers for cache events and periodic schedules.</span></span> <span data-ttu-id="ebe3b-176">[開放原始碼儲存機制](https://github.com/Azure/azure-webjobs-sdk-extensions)包含[上 WebJobs SDK 擴充性的詳細的指引](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Binding-Extensions-Overview)和範例程式碼 toohelp 協助您開始撰寫您自己的觸發程序和繫結器。</span><span class="sxs-lookup"><span data-stu-id="ebe3b-176">An [open source repository](https://github.com/Azure/azure-webjobs-sdk-extensions) contains a [detailed guide on WebJobs SDK extensibility](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Binding-Extensions-Overview) and sample code toohelp get you started writing your own triggers and binders.</span></span>

## <span data-ttu-id="ebe3b-177"><a id="workerrole"></a>使用 hello 之外 WebJobs WebJobs SDK</span><span class="sxs-lookup"><span data-stu-id="ebe3b-177"><a id="workerrole"></a>Using hello WebJobs SDK outside of WebJobs</span></span>
<span data-ttu-id="ebe3b-178">使用 WebJobs SDK 是標準的主控台應用程式，且可以執行任何位置-hello hello 的程式不一定 toorun webjob。</span><span class="sxs-lookup"><span data-stu-id="ebe3b-178">A program that uses hello hello WebJobs SDK is a standard Console Application and can run anywhere -- it doesn't have toorun as a WebJob.</span></span> <span data-ttu-id="ebe3b-179">在開發電腦，並在生產環境，您可以執行中雲端服務背景工作角色或 Windows 服務如果您偏好其中一個這些環境中，您可以在本機測試 hello 程式。</span><span class="sxs-lookup"><span data-stu-id="ebe3b-179">You can test hello program locally on your development computer, and in production you can run it in a Cloud Service worker role or a Windows service if you prefer one of those environments.</span></span> 

<span data-ttu-id="ebe3b-180">不過，hello 儀表板才會為 Azure App Service web 應用程式的延伸模組。</span><span class="sxs-lookup"><span data-stu-id="ebe3b-180">However, hello dashboard is only available as an extension for an Azure App Service web app.</span></span> <span data-ttu-id="ebe3b-181">如果您想 toorun WebJob 之外，且仍使用 hello 儀表板，您可以設定 web 應用程式 toouse hello 相同儲存體帳戶是指您 WebJobs SDK 儀表板的連接字串，以及該 web 應用程式的 WebJobs 儀表板會顯示有關函數的資料從您的程式執行的其他地方執行。</span><span class="sxs-lookup"><span data-stu-id="ebe3b-181">If you want toorun outside of a WebJob and still use hello Dashboard, you can configure a web app toouse hello same storage account that your WebJobs SDK Dashboard connection string refers to, and that web app's WebJobs Dashboard will then show data about function execution from your program that is running somewhere else.</span></span> <span data-ttu-id="ebe3b-182">您可以取得 toohello 儀表板使用 hello URL https://*{webappname}*.scm.azurewebsites.net/azurejobs/#/functions。</span><span class="sxs-lookup"><span data-stu-id="ebe3b-182">You can get toohello Dashboard by using hello URL https://*{webappname}*.scm.azurewebsites.net/azurejobs/#/functions.</span></span> <span data-ttu-id="ebe3b-183">如需詳細資訊，請參閱[儀表板取得以 hello WebJobs SDK 的本機開發](http://blogs.msdn.com/b/jmstall/archive/2014/01/27/getting-a-dashboard-for-local-development-with-the-webjobs-sdk.aspx)，但請注意 hello 部落格文章，顯示舊的連接字串名稱。</span><span class="sxs-lookup"><span data-stu-id="ebe3b-183">For more information, see [Getting a dashboard for local development with hello WebJobs SDK](http://blogs.msdn.com/b/jmstall/archive/2014/01/27/getting-a-dashboard-for-local-development-with-the-webjobs-sdk.aspx), but note that hello blog post shows an old connection string name.</span></span> 

## <span data-ttu-id="ebe3b-184"><a id="nostorage"></a>儀表板功能</span><span class="sxs-lookup"><span data-stu-id="ebe3b-184"><a id="nostorage"></a>Dashboard features</span></span>
<span data-ttu-id="ebe3b-185">即使您不使用 WebJobs SDK 觸發程序或繫結器 hello WebJobs SDK 會提供數個優點：</span><span class="sxs-lookup"><span data-stu-id="ebe3b-185">hello WebJobs SDK provides several advantages even if you don't use WebJobs SDK triggers or binders:</span></span>

* <span data-ttu-id="ebe3b-186">您可以叫用函式從 hello 儀表板。</span><span class="sxs-lookup"><span data-stu-id="ebe3b-186">You can invoke functions from hello Dashboard.</span></span>
* <span data-ttu-id="ebe3b-187">您可以重新執行函式從 hello 儀表板。</span><span class="sxs-lookup"><span data-stu-id="ebe3b-187">You can replay functions from hello Dashboard.</span></span>
* <span data-ttu-id="ebe3b-188">您可以檢視記錄檔中 hello 儀表板連結 toohello 特定 WebJob （應用程式記錄檔，寫入使用 Console.Out、 Console.Error、 追蹤等） 或連結 toohello 特定函式引動過程產生它們 (使用所撰寫的記錄檔`TextWriter`物件的 hello SDK 將 toohello 函式做為參數）。</span><span class="sxs-lookup"><span data-stu-id="ebe3b-188">You can view logs in hello Dashboard, linked toohello particular WebJob (application logs, written by using Console.Out, Console.Error, Trace, etc.) or linked toohello particular function invocation that generated them (logs written by using a `TextWriter` object that hello SDK passes toohello function as a parameter).</span></span> 

<span data-ttu-id="ebe3b-189">如需詳細資訊，請參閱[toomanually 如何叫用函式](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#manual)和[toowrite 的記錄檔](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#logs)</span><span class="sxs-lookup"><span data-stu-id="ebe3b-189">For more information, see [How toomanually invoke a function](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#manual) and [How toowrite logs](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#logs)</span></span> 

## <span data-ttu-id="ebe3b-190"><a id="nextsteps"></a>接續步驟</span><span class="sxs-lookup"><span data-stu-id="ebe3b-190"><a id="nextsteps"></a>Next steps</span></span>
<span data-ttu-id="ebe3b-191">如需 hello WebJobs SDK 的詳細資訊，請參閱[Azure WebJobs 建議資源](http://go.microsoft.com/fwlink/?linkid=390226)。</span><span class="sxs-lookup"><span data-stu-id="ebe3b-191">For more information about hello WebJobs SDK, see [Azure WebJobs Recommended Resources](http://go.microsoft.com/fwlink/?linkid=390226).</span></span>

<span data-ttu-id="ebe3b-192">如需最新增強功能 toohello hello WebJobs SDK 資訊，請參閱 hello[版本資訊](https://github.com/Azure/azure-webjobs-sdk/wiki/Release-Notes)。</span><span class="sxs-lookup"><span data-stu-id="ebe3b-192">For information about hello latest enhancements toohello WebJobs SDK, see hello [Release Notes](https://github.com/Azure/azure-webjobs-sdk/wiki/Release-Notes).</span></span>

