---
title: "aaaUse Azure 佇列儲存體 toomonitor Media Services 工作通知使用.NET |Microsoft 文件"
description: "了解如何 toouse Azure 佇列儲存體 toomonitor Media Services 工作通知。 hello 程式碼範例以 C# 撰寫，並使用 hello Media Services SDK for.NET。"
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: f535d0b5-f86c-465f-81c6-177f4f490987
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/14/2017
ms.author: juliako
ms.openlocfilehash: e4068621ada00d763133dc0d01cfc666b53f8b1b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-queue-storage-toomonitor-media-services-job-notifications-with-net"></a><span data-ttu-id="805dc-104">搭配.NET 使用 Azure 佇列儲存體 toomonitor Media Services 工作通知</span><span class="sxs-lookup"><span data-stu-id="805dc-104">Use Azure Queue storage toomonitor Media Services job notifications with .NET</span></span>
<span data-ttu-id="805dc-105">當您執行編碼工作時，通常會需要方式 tootrack 工作進度。</span><span class="sxs-lookup"><span data-stu-id="805dc-105">When you run encoding jobs, you often require a way tootrack job progress.</span></span> <span data-ttu-id="805dc-106">您可以設定 Media Services toodeliver 通知太[Azure 佇列儲存體](../storage/storage-dotnet-how-to-use-queues.md)。</span><span class="sxs-lookup"><span data-stu-id="805dc-106">You can configure Media Services toodeliver notifications too[Azure Queue storage](../storage/storage-dotnet-how-to-use-queues.md).</span></span> <span data-ttu-id="805dc-107">您可以取得通知 hello 佇列儲存體監控工作進度。</span><span class="sxs-lookup"><span data-stu-id="805dc-107">You can monitor job progress by getting notifications from hello Queue storage.</span></span> 

<span data-ttu-id="805dc-108">訊息傳遞 tooQueue 存放裝置可以存取從任何地方 hello world。</span><span class="sxs-lookup"><span data-stu-id="805dc-108">Messages delivered tooQueue storage can be accessed from anywhere in hello world.</span></span> <span data-ttu-id="805dc-109">hello 佇列儲存體傳訊架構是可靠且具有高擴充性。</span><span class="sxs-lookup"><span data-stu-id="805dc-109">hello Queue storage messaging architecture is reliable and highly scalable.</span></span> <span data-ttu-id="805dc-110">建議利用其他方法，針對訊息輪詢佇列儲存體。</span><span class="sxs-lookup"><span data-stu-id="805dc-110">Polling Queue storage for messages is recommended over using other methods.</span></span>

<span data-ttu-id="805dc-111">編碼工作後一些額外的工作完成的接聽 tooMedia 服務通知的常見案例就是如果您正在開發的內容管理系統需要 tooperform （例如，在工作流程或 toopublish tootrigger hello 下一個步驟內容）。</span><span class="sxs-lookup"><span data-stu-id="805dc-111">One common scenario for listening tooMedia Services notifications is if you are developing a content management system that needs tooperform some additional task after an encoding job completes (for example, tootrigger hello next step in a workflow, or toopublish content).</span></span>

<span data-ttu-id="805dc-112">本主題說明如何 tooget 通知訊息從佇列儲存體。</span><span class="sxs-lookup"><span data-stu-id="805dc-112">This topic shows how tooget notification messages from Queue storage.</span></span>  

## <a name="considerations"></a><span data-ttu-id="805dc-113">考量</span><span class="sxs-lookup"><span data-stu-id="805dc-113">Considerations</span></span>
<span data-ttu-id="805dc-114">開發使用佇列儲存體的媒體服務應用程式時，請考慮下列 hello:</span><span class="sxs-lookup"><span data-stu-id="805dc-114">Consider hello following when developing Media Services applications that use Queue storage:</span></span>

* <span data-ttu-id="805dc-115">佇列儲存體不保證會按照先進先出 (FIFO) 的順序進行。</span><span class="sxs-lookup"><span data-stu-id="805dc-115">Queue storage does not provide a guarantee of first-in-first-out (FIFO) ordered delivery.</span></span> <span data-ttu-id="805dc-116">如需詳細資訊，請參閱 [Azure 佇列和 Azure 服務匯流排佇列的比較和對比](https://msdn.microsoft.com/library/azure/hh767287.aspx)。</span><span class="sxs-lookup"><span data-stu-id="805dc-116">For more information, see [Azure Queues and Azure Service Bus Queues Compared and Contrasted](https://msdn.microsoft.com/library/azure/hh767287.aspx).</span></span>
* <span data-ttu-id="805dc-117">佇列儲存體不是推送服務。</span><span class="sxs-lookup"><span data-stu-id="805dc-117">Queue storage is not a push service.</span></span> <span data-ttu-id="805dc-118">您有 toopoll hello 佇列。</span><span class="sxs-lookup"><span data-stu-id="805dc-118">You have toopoll hello queue.</span></span>
* <span data-ttu-id="805dc-119">您可以有任意數目的佇列。</span><span class="sxs-lookup"><span data-stu-id="805dc-119">You can have any number of queues.</span></span> <span data-ttu-id="805dc-120">如需詳細資訊，請參閱 [佇列服務 REST API](https://docs.microsoft.com/rest/api/storageservices/Queue-Service-REST-API)。</span><span class="sxs-lookup"><span data-stu-id="805dc-120">For more information, see [Queue Service REST API](https://docs.microsoft.com/rest/api/storageservices/Queue-Service-REST-API).</span></span>
* <span data-ttu-id="805dc-121">佇列儲存體方面有一些限制和特性 toobe 留意。</span><span class="sxs-lookup"><span data-stu-id="805dc-121">Queue storage has some limitations and specifics toobe aware of.</span></span> <span data-ttu-id="805dc-122">如需這些限制與細節的說明，請參閱 [Azure 佇列和 Azure 服務匯流排佇列的異同比較](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-azure-and-service-bus-queues-compared-contrasted)。</span><span class="sxs-lookup"><span data-stu-id="805dc-122">These are described in [Azure Queues and Azure Service Bus Queues Compared and Contrasted](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-azure-and-service-bus-queues-compared-contrasted).</span></span>

## <a name="net-code-example"></a><span data-ttu-id="805dc-123">.NET 程式碼範例</span><span class="sxs-lookup"><span data-stu-id="805dc-123">.NET code example</span></span>

<span data-ttu-id="805dc-124">本節中的 hello 程式碼範例並未 hello 遵循：</span><span class="sxs-lookup"><span data-stu-id="805dc-124">hello code example in this section does hello following:</span></span>

1. <span data-ttu-id="805dc-125">定義 hello **EncodingJobMessage**對應 toohello 通知訊息格式的類別。</span><span class="sxs-lookup"><span data-stu-id="805dc-125">Defines hello **EncodingJobMessage** class that maps toohello notification message format.</span></span> <span data-ttu-id="805dc-126">hello 程式碼將訊息從 hello 佇列會接收到的 hello 物件還原序列化**EncodingJobMessage**型別。</span><span class="sxs-lookup"><span data-stu-id="805dc-126">hello code deserializes messages received from hello queue into objects of hello **EncodingJobMessage** type.</span></span>
2. <span data-ttu-id="805dc-127">載入 hello Media Services 並從 hello app.config 檔案的儲存體帳戶資訊。</span><span class="sxs-lookup"><span data-stu-id="805dc-127">Loads hello Media Services and Storage account information from hello app.config file.</span></span> <span data-ttu-id="805dc-128">hello 程式碼範例會使用此資訊 toocreate hello **CloudMediaContext**和**CloudQueue**物件。</span><span class="sxs-lookup"><span data-stu-id="805dc-128">hello code example uses this information toocreate hello **CloudMediaContext** and **CloudQueue** objects.</span></span>
3. <span data-ttu-id="805dc-129">建立 hello 收到 hello 編碼作業有關的通知訊息的佇列。</span><span class="sxs-lookup"><span data-stu-id="805dc-129">Creates hello queue that receives notification messages about hello encoding job.</span></span>
4. <span data-ttu-id="805dc-130">建立結束點所對應 toohello 佇列 hello 通知。</span><span class="sxs-lookup"><span data-stu-id="805dc-130">Creates hello notification end point that is mapped toohello queue.</span></span>
5. <span data-ttu-id="805dc-131">附加 hello 通知端點 toohello 作業，並送出 hello 編碼工作。</span><span class="sxs-lookup"><span data-stu-id="805dc-131">Attaches hello notification end point toohello job and submits hello encoding job.</span></span> <span data-ttu-id="805dc-132">您可以有多個通知附加的結束點 tooa 作業。</span><span class="sxs-lookup"><span data-stu-id="805dc-132">You can have multiple notification end points attached tooa job.</span></span>
6. <span data-ttu-id="805dc-133">傳遞**NotificationJobState.FinalStatesOnly** toohello **AddNew**方法。</span><span class="sxs-lookup"><span data-stu-id="805dc-133">Passes **NotificationJobState.FinalStatesOnly** toohello **AddNew** method.</span></span> <span data-ttu-id="805dc-134">（在此範例中，我們是只有興趣 hello 作業處理的最後狀態）。</span><span class="sxs-lookup"><span data-stu-id="805dc-134">(In this example, we are only interested in final states of hello job processing.)</span></span>

        job.JobNotificationSubscriptions.AddNew(NotificationJobState.FinalStatesOnly, _notificationEndPoint);
7. <span data-ttu-id="805dc-135">如果您要傳入**NotificationJobState.All**，您可以獲得所有下列狀態變更通知的 hello： 排入佇列、 排程、 處理和已完成。</span><span class="sxs-lookup"><span data-stu-id="805dc-135">If you pass **NotificationJobState.All**, you get all of hello following state change notifications: queued, scheduled, processing, and finished.</span></span> <span data-ttu-id="805dc-136">不過，如先前所述，佇列儲存體不保證會按照順序傳遞。</span><span class="sxs-lookup"><span data-stu-id="805dc-136">However, as noted earlier, Queue storage does not guarantee ordered delivery.</span></span> <span data-ttu-id="805dc-137">tooorder 訊息使用 hello**時間戳記**屬性 (定義於 hello **EncodingJobMessage** hello 下面範例中的型別)。</span><span class="sxs-lookup"><span data-stu-id="805dc-137">tooorder messages, use hello **Timestamp** property (defined on hello **EncodingJobMessage** type in hello example below).</span></span> <span data-ttu-id="805dc-138">可能會有重複的訊息。</span><span class="sxs-lookup"><span data-stu-id="805dc-138">Duplicate messages are possible.</span></span> <span data-ttu-id="805dc-139">重複項目，使用 hello toocheck **ETag 屬性**(定義於 hello **EncodingJobMessage**類型)。</span><span class="sxs-lookup"><span data-stu-id="805dc-139">toocheck for duplicates, use hello **ETag property** (defined on hello **EncodingJobMessage** type).</span></span> <span data-ttu-id="805dc-140">可能也會略過某些狀態變更通知。</span><span class="sxs-lookup"><span data-stu-id="805dc-140">It is also possible that some state change notifications get skipped.</span></span>
8. <span data-ttu-id="805dc-141">等候 hello 作業 tooget toohello 的完成狀態檢查 hello 佇列每隔 10 秒。</span><span class="sxs-lookup"><span data-stu-id="805dc-141">Waits for hello job tooget toohello finished state by checking hello queue every 10 seconds.</span></span> <span data-ttu-id="805dc-142">處理好訊息之後，請予以刪除。</span><span class="sxs-lookup"><span data-stu-id="805dc-142">Deletes messages after they have been processed.</span></span>
9. <span data-ttu-id="805dc-143">刪除佇列 hello 和 hello 通知結束點。</span><span class="sxs-lookup"><span data-stu-id="805dc-143">Deletes hello queue and hello notification end point.</span></span>

> [!NOTE]
> <span data-ttu-id="805dc-144">hello 建議作業的狀態是所接聽的 toonotification 訊息的方式 toomonitor hello 下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="805dc-144">hello recommended way toomonitor a job’s state is by listening toonotification messages, as shown in hello following example.</span></span>
>
> <span data-ttu-id="805dc-145">或者，您無法檢查工作狀態使用 hello **IJob.State**屬性。</span><span class="sxs-lookup"><span data-stu-id="805dc-145">Alternatively, you could check on a job’s state by using hello **IJob.State** property.</span></span>  <span data-ttu-id="805dc-146">相關工作的完成通知訊息可能會到達 hello 狀態之前**IJob**設定得**已經完成**。</span><span class="sxs-lookup"><span data-stu-id="805dc-146">A notification message about a job’s completion may arrive before hello state on **IJob** is set too**Finished**.</span></span> <span data-ttu-id="805dc-147">hello **IJob.State**屬性會反映 hello 精確狀態與稍微延遲。</span><span class="sxs-lookup"><span data-stu-id="805dc-147">hello **IJob.State**  property reflects hello accurate state with a slight delay.</span></span>
>
>

### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="805dc-148">建立和設定 Visual Studio 專案</span><span class="sxs-lookup"><span data-stu-id="805dc-148">Create and configure a Visual Studio project</span></span>

1. <span data-ttu-id="805dc-149">設定您的開發環境，並填入 hello 與連接資訊的 app.config 檔案中所述[與.NET 的 Media Services 開發](media-services-dotnet-how-to-use.md)。</span><span class="sxs-lookup"><span data-stu-id="805dc-149">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 
2. <span data-ttu-id="805dc-150">建立新的資料夾 （資料夾可以是任何位置在本機磁碟機上），並將您想要 tooencode 和資料流或漸進式下載.mp4 檔案複製。</span><span class="sxs-lookup"><span data-stu-id="805dc-150">Create a new folder (folder can be anywhere on your local drive) and copy an .mp4 file that you want tooencode and stream or progressively download.</span></span> <span data-ttu-id="805dc-151">在此範例中，會使用 hello"C:\Media 」 路徑。</span><span class="sxs-lookup"><span data-stu-id="805dc-151">In this example, hello "C:\Media" path is used.</span></span>

### <a name="code"></a><span data-ttu-id="805dc-152">代碼</span><span class="sxs-lookup"><span data-stu-id="805dc-152">Code</span></span>

```
using System;
using System.Linq;
using System.Configuration;
using System.IO;
using System.Threading;
using System.Collections.Generic;
using Microsoft.WindowsAzure.MediaServices.Client;
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Queue;
using System.Runtime.Serialization.Json;

namespace JobNotification
{
    public class EncodingJobMessage
    {
        // MessageVersion is used for version control.
        public String MessageVersion { get; set; }

        // Type of hello event. Valid values are
        // JobStateChange and NotificationEndpointRegistration.
        public String EventType { get; set; }

        // ETag is used toohelp hello customer detect if
        // hello message is a duplicate of another message previously sent.
        public String ETag { get; set; }

        // Time of occurrence of hello event.
        public String TimeStamp { get; set; }

        // Collection of values specific toohello event.

        // For hello JobStateChange event hello values are:
        //     JobId - Id of hello Job that triggered hello notification.
        //     NewState- hello new state of hello Job. Valid values are:
        //          Scheduled, Processing, Canceling, Cancelled, Error, Finished
        //     OldState- hello old state of hello Job. Valid values are:
        //          Scheduled, Processing, Canceling, Cancelled, Error, Finished

        // For hello NotificationEndpointRegistration event hello values are:
        //     NotificationEndpointId- Id of hello NotificationEndpoint
        //          that triggered hello notification.
        //     State- hello state of hello Endpoint.
        //          Valid values are: Registered and Unregistered.

        public IDictionary<string, object> Properties { get; set; }
    }

    class Program
    {

        // Read values from hello App.config file.
        private static readonly string _AADTenantDomain =
            ConfigurationManager.AppSettings["AADTenantDomain"];
        private static readonly string _RESTAPIEndpoint =
            ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];
        private static readonly string _StorageConnectionString = 
            ConfigurationManager.AppSettings["StorageConnectionString"];

        private static CloudMediaContext _context = null;
        private static CloudQueue _queue = null;
        private static INotificationEndPoint _notificationEndPoint = null;

        private static readonly string _singleInputMp4Path =
            Path.GetFullPath(@"C:\Media\BigBuckBunny.mp4");

        static void Main(string[] args)
        {
            string endPointAddress = Guid.NewGuid().ToString();

            // Create hello context.
            var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
            var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

            _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);

            // Create hello queue that will be receiving hello notification messages.
            _queue = CreateQueue(_StorageConnectionString, endPointAddress);

            // Create hello notification point that is mapped toohello queue.
            _notificationEndPoint =
                    _context.NotificationEndPoints.Create(
                    Guid.NewGuid().ToString(), NotificationEndPointType.AzureQueue, endPointAddress);


            if (_notificationEndPoint != null)
            {
                IJob job = SubmitEncodingJobWithNotificationEndPoint(_singleInputMp4Path);
                WaitForJobToReachedFinishedState(job.Id);
            }

            // Clean up.
            _queue.Delete();
            _notificationEndPoint.Delete();
        }


        static public CloudQueue CreateQueue(string storageAccountConnectionString, string endPointAddress)
        {
            CloudStorageAccount storageAccount = CloudStorageAccount.Parse(storageAccountConnectionString);

            // Create hello queue client
            CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

            // Retrieve a reference tooa queue
            CloudQueue queue = queueClient.GetQueueReference(endPointAddress);

            // Create hello queue if it doesn't already exist
            queue.CreateIfNotExists();

            return queue;
        }


        public static IJob SubmitEncodingJobWithNotificationEndPoint(string inputMediaFilePath)
        {
            // Declare a new job.
            IJob job = _context.Jobs.Create("My MP4 tooSmooth Streaming encoding job");

            //Create an encrypted asset and upload hello mp4.
            IAsset asset = CreateAssetAndUploadSingleFile(AssetCreationOptions.StorageEncrypted,
                inputMediaFilePath);

            // Get a media processor reference, and pass tooit hello name of the
            // processor toouse for hello specific task.
            IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Standard");

            // Create a task with hello conversion details, using a configuration file.
            ITask task = job.Tasks.AddNew("My encoding Task",
                processor,
                "Adaptive Streaming",
                Microsoft.WindowsAzure.MediaServices.Client.TaskOptions.None);

            // Specify hello input asset toobe encoded.
            task.InputAssets.Add(asset);

            // Add an output asset toocontain hello results of hello job.
            task.OutputAssets.AddNew("Output asset",
                AssetCreationOptions.None);

            // Add a notification point toohello job. You can add multiple notification points.  
            job.JobNotificationSubscriptions.AddNew(NotificationJobState.FinalStatesOnly,
                _notificationEndPoint);

            job.Submit();

            return job;
        }

        public static void WaitForJobToReachedFinishedState(string jobId)
        {
            int expectedState = (int)JobState.Finished;
            int timeOutInSeconds = 600;

            bool jobReachedExpectedState = false;
            DateTime startTime = DateTime.Now;
            int jobState = -1;

            while (!jobReachedExpectedState)
            {
                // Specify how often you want tooget messages from hello queue.
                Thread.Sleep(TimeSpan.FromSeconds(10));

                foreach (var message in _queue.GetMessages(10))
                {
                    using (Stream stream = new MemoryStream(message.AsBytes))
                    {
                        DataContractJsonSerializerSettings settings = new DataContractJsonSerializerSettings();
                        settings.UseSimpleDictionaryFormat = true;
                        DataContractJsonSerializer ser = new DataContractJsonSerializer(typeof(EncodingJobMessage), settings);
                        EncodingJobMessage encodingJobMsg = (EncodingJobMessage)ser.ReadObject(stream);

                        Console.WriteLine();

                        // Display hello message information.
                        Console.WriteLine("EventType: {0}", encodingJobMsg.EventType);
                        Console.WriteLine("MessageVersion: {0}", encodingJobMsg.MessageVersion);
                        Console.WriteLine("ETag: {0}", encodingJobMsg.ETag);
                        Console.WriteLine("TimeStamp: {0}", encodingJobMsg.TimeStamp);
                        foreach (var property in encodingJobMsg.Properties)
                        {
                            Console.WriteLine("    {0}: {1}", property.Key, property.Value);
                        }

                        // We are only interested in messages
                        // where EventType is "JobStateChange".
                        if (encodingJobMsg.EventType == "JobStateChange")
                        {
                            string JobId = (String)encodingJobMsg.Properties.Where(j => j.Key == "JobId").FirstOrDefault().Value;
                            if (JobId == jobId)
                            {
                                string oldJobStateStr = (String)encodingJobMsg.Properties.
                                                            Where(j => j.Key == "OldState").FirstOrDefault().Value;
                                string newJobStateStr = (String)encodingJobMsg.Properties.
                                                            Where(j => j.Key == "NewState").FirstOrDefault().Value;

                                JobState oldJobState = (JobState)Enum.Parse(typeof(JobState), oldJobStateStr);
                                JobState newJobState = (JobState)Enum.Parse(typeof(JobState), newJobStateStr);

                                if (newJobState == (JobState)expectedState)
                                {
                                    Console.WriteLine("job with Id: {0} reached expected state: {1}",
                                        jobId, newJobState);
                                    jobReachedExpectedState = true;
                                    break;
                                }
                            }
                        }
                    }
                    // Delete hello message after we've read it.
                    _queue.DeleteMessage(message);
                }

                // Wait until timeout
                TimeSpan timeDiff = DateTime.Now - startTime;
                bool timedOut = (timeDiff.TotalSeconds > timeOutInSeconds);
                if (timedOut)
                {
                    Console.WriteLine(@"Timeout for checking job notification messages,
                                        latest found state ='{0}', wait time = {1} secs",
                        jobState,
                        timeDiff.TotalSeconds);

                    throw new TimeoutException();
                }
            }
        }

        static private IAsset CreateAssetAndUploadSingleFile(AssetCreationOptions assetCreationOptions, string singleFilePath)
        {
            var asset = _context.Assets.Create("UploadSingleFile_" + DateTime.UtcNow.ToString(),
                assetCreationOptions);

            var fileName = Path.GetFileName(singleFilePath);

            var assetFile = asset.AssetFiles.Create(fileName);

            Console.WriteLine("Created assetFile {0}", assetFile.Name);
            Console.WriteLine("Upload {0}", assetFile.Name);

            assetFile.Upload(singleFilePath);
            Console.WriteLine("Done uploading of {0}", assetFile.Name);

            return asset;
        }

        static private IMediaProcessor GetLatestMediaProcessorByName(string mediaProcessorName)
        {
            var processor = _context.MediaProcessors.Where(p => p.Name == mediaProcessorName).
                ToList().OrderBy(p => new Version(p.Version)).LastOrDefault();

            if (processor == null)
                throw new ArgumentException(string.Format("Unknown media processor", mediaProcessorName));

            return processor;
        }
    }
}
```
<span data-ttu-id="805dc-153">hello 上述範例所產生 hello 遵循輸出。</span><span class="sxs-lookup"><span data-stu-id="805dc-153">hello preceding example produced hello following output.</span></span> <span data-ttu-id="805dc-154">您的值會不一樣。</span><span class="sxs-lookup"><span data-stu-id="805dc-154">Your values will vary.</span></span>

    Created assetFile BigBuckBunny.mp4
    Upload BigBuckBunny.mp4
    Done uploading of BigBuckBunny.mp4

    EventType: NotificationEndPointRegistration
    MessageVersion: 1.0
    ETag: e0238957a9b25bdf3351a88e57978d6a81a84527fad03bc23861dbe28ab293f6
    TimeStamp: 2013-05-14T20:22:37
        NotificationEndPointId: nb:nepid:UUID:d6af9412-2488-45b2-ba1f-6e0ade6dbc27
        State: Registered
        Name: dde957b2-006e-41f2-9869-a978870ac620
        Created: 2013-05-14T20:22:35

    EventType: JobStateChange
    MessageVersion: 1.0
    ETag: 4e381f37c2d844bde06ace650310284d6928b1e50101d82d1b56220cfcb6076c
    TimeStamp: 2013-05-14T20:24:40
        JobId: nb:jid:UUID:526291de-f166-be47-b62a-11ffe6d4be54
        JobName: My MP4 tooSmooth Streaming encoding job
        NewState: Finished
        OldState: Processing
        AccountName: westeuropewamsaccount
    job with Id: nb:jid:UUID:526291de-f166-be47-b62a-11ffe6d4be54 reached expected
    State: Finished


## <a name="next-step"></a><span data-ttu-id="805dc-155">後續步驟</span><span class="sxs-lookup"><span data-stu-id="805dc-155">Next step</span></span>
<span data-ttu-id="805dc-156">檢閱媒體服務學習路徑。</span><span class="sxs-lookup"><span data-stu-id="805dc-156">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="805dc-157">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="805dc-157">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
