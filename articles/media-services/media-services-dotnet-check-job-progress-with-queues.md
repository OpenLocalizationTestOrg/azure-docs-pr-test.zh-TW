---
title: "使用 Azure 佇列儲存體監視 .NET 的媒體服務工作通知 | Microsoft Docs"
description: "了解如何使用 Azure 佇列儲存體監視媒體服務工作通知。 程式碼範例是以 C# 撰寫，並使用 Media Services SDK for .NET。"
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
ms.openlocfilehash: 5ee89d0ae4c3c56d164aff4e321ee99f015ba4fb
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="use-azure-queue-storage-to-monitor-media-services-job-notifications-with-net"></a><span data-ttu-id="0342f-104">使用 Azure 佇列儲存體監視 .NET 的媒體服務工作通知</span><span class="sxs-lookup"><span data-stu-id="0342f-104">Use Azure Queue storage to monitor Media Services job notifications with .NET</span></span>
<span data-ttu-id="0342f-105">執行編碼作業時，您通常需要設法追蹤作業進度。</span><span class="sxs-lookup"><span data-stu-id="0342f-105">When you run encoding jobs, you often require a way to track job progress.</span></span> <span data-ttu-id="0342f-106">您可以設定媒體服務，將通知傳遞給 [Azure 佇列儲存體](../storage/storage-dotnet-how-to-use-queues.md)。</span><span class="sxs-lookup"><span data-stu-id="0342f-106">You can configure Media Services to deliver notifications to [Azure Queue storage](../storage/storage-dotnet-how-to-use-queues.md).</span></span> <span data-ttu-id="0342f-107">從佇列儲存體取得通知，即可監視作業進度。</span><span class="sxs-lookup"><span data-stu-id="0342f-107">You can monitor job progress by getting notifications from the Queue storage.</span></span> 

<span data-ttu-id="0342f-108">使用者可以從世界各個角落存取之前已傳送至佇列儲存體的訊息。</span><span class="sxs-lookup"><span data-stu-id="0342f-108">Messages delivered to Queue storage can be accessed from anywhere in the world.</span></span> <span data-ttu-id="0342f-109">佇列儲存體訊息架構十分可靠，而且具有高擴充性。</span><span class="sxs-lookup"><span data-stu-id="0342f-109">The Queue storage messaging architecture is reliable and highly scalable.</span></span> <span data-ttu-id="0342f-110">建議利用其他方法，針對訊息輪詢佇列儲存體。</span><span class="sxs-lookup"><span data-stu-id="0342f-110">Polling Queue storage for messages is recommended over using other methods.</span></span>

<span data-ttu-id="0342f-111">舉一個常見的接聽媒體服務通知案例：假設您正在設計一套內容管理系，而且在編碼作業完成之後，這套系統需要執行其他一些工作 (例如，觸發工作流程的下一個步驟或者發佈內容)。</span><span class="sxs-lookup"><span data-stu-id="0342f-111">One common scenario for listening to Media Services notifications is if you are developing a content management system that needs to perform some additional task after an encoding job completes (for example, to trigger the next step in a workflow, or to publish content).</span></span>

<span data-ttu-id="0342f-112">本主題示範如何從佇列儲存體取得通知訊息。</span><span class="sxs-lookup"><span data-stu-id="0342f-112">This topic shows how to get notification messages from Queue storage.</span></span>  

## <a name="considerations"></a><span data-ttu-id="0342f-113">考量</span><span class="sxs-lookup"><span data-stu-id="0342f-113">Considerations</span></span>
<span data-ttu-id="0342f-114">若您開發的媒體服務應用程式會使用佇列儲存體，請考慮下列幾點：</span><span class="sxs-lookup"><span data-stu-id="0342f-114">Consider the following when developing Media Services applications that use Queue storage:</span></span>

* <span data-ttu-id="0342f-115">佇列儲存體不保證會按照先進先出 (FIFO) 的順序進行。</span><span class="sxs-lookup"><span data-stu-id="0342f-115">Queue storage does not provide a guarantee of first-in-first-out (FIFO) ordered delivery.</span></span> <span data-ttu-id="0342f-116">如需詳細資訊，請參閱 [Azure 佇列和 Azure 服務匯流排佇列的比較和對比](https://msdn.microsoft.com/library/azure/hh767287.aspx)。</span><span class="sxs-lookup"><span data-stu-id="0342f-116">For more information, see [Azure Queues and Azure Service Bus Queues Compared and Contrasted](https://msdn.microsoft.com/library/azure/hh767287.aspx).</span></span>
* <span data-ttu-id="0342f-117">佇列儲存體不是推送服務。</span><span class="sxs-lookup"><span data-stu-id="0342f-117">Queue storage is not a push service.</span></span> <span data-ttu-id="0342f-118">您必須輪詢佇列。</span><span class="sxs-lookup"><span data-stu-id="0342f-118">You have to poll the queue.</span></span>
* <span data-ttu-id="0342f-119">您可以有任意數目的佇列。</span><span class="sxs-lookup"><span data-stu-id="0342f-119">You can have any number of queues.</span></span> <span data-ttu-id="0342f-120">如需詳細資訊，請參閱 [佇列服務 REST API](https://docs.microsoft.com/rest/api/storageservices/Queue-Service-REST-API)。</span><span class="sxs-lookup"><span data-stu-id="0342f-120">For more information, see [Queue Service REST API](https://docs.microsoft.com/rest/api/storageservices/Queue-Service-REST-API).</span></span>
* <span data-ttu-id="0342f-121">佇列儲存體具有一些要注意的限制和細節。</span><span class="sxs-lookup"><span data-stu-id="0342f-121">Queue storage has some limitations and specifics to be aware of.</span></span> <span data-ttu-id="0342f-122">如需這些限制與細節的說明，請參閱 [Azure 佇列和 Azure 服務匯流排佇列的異同比較](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-azure-and-service-bus-queues-compared-contrasted)。</span><span class="sxs-lookup"><span data-stu-id="0342f-122">These are described in [Azure Queues and Azure Service Bus Queues Compared and Contrasted](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-azure-and-service-bus-queues-compared-contrasted).</span></span>

## <a name="net-code-example"></a><span data-ttu-id="0342f-123">.NET 程式碼範例</span><span class="sxs-lookup"><span data-stu-id="0342f-123">.NET code example</span></span>

<span data-ttu-id="0342f-124">本節的程式碼會執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="0342f-124">The code example in this section does the following:</span></span>

1. <span data-ttu-id="0342f-125">定義一個會對應至通知訊息格式的 **EncodingJobMessage** 類別。</span><span class="sxs-lookup"><span data-stu-id="0342f-125">Defines the **EncodingJobMessage** class that maps to the notification message format.</span></span> <span data-ttu-id="0342f-126">程式碼會將那些從佇列接收到的訊息還原序列化，然後變成 **EncodingJobMessage** 類型的物件。</span><span class="sxs-lookup"><span data-stu-id="0342f-126">The code deserializes messages received from the queue into objects of the **EncodingJobMessage** type.</span></span>
2. <span data-ttu-id="0342f-127">從 app.config 檔案載入媒體服務和儲存體帳戶資訊。</span><span class="sxs-lookup"><span data-stu-id="0342f-127">Loads the Media Services and Storage account information from the app.config file.</span></span> <span data-ttu-id="0342f-128">這個程式碼範例會使用此資訊來建立 **CloudMediaContext** 和 **CloudQueue** 物件。</span><span class="sxs-lookup"><span data-stu-id="0342f-128">The code example uses this information to create the **CloudMediaContext** and **CloudQueue** objects.</span></span>
3. <span data-ttu-id="0342f-129">建立一個會接收編碼工作相關通知訊息的佇列。</span><span class="sxs-lookup"><span data-stu-id="0342f-129">Creates the queue that receives notification messages about the encoding job.</span></span>
4. <span data-ttu-id="0342f-130">建立一個會對應到佇列的通知端點。</span><span class="sxs-lookup"><span data-stu-id="0342f-130">Creates the notification end point that is mapped to the queue.</span></span>
5. <span data-ttu-id="0342f-131">將通知端點附加至工作，然後提交編碼工作。</span><span class="sxs-lookup"><span data-stu-id="0342f-131">Attaches the notification end point to the job and submits the encoding job.</span></span> <span data-ttu-id="0342f-132">您可以將多個通知端點附加至工作。</span><span class="sxs-lookup"><span data-stu-id="0342f-132">You can have multiple notification end points attached to a job.</span></span>
6. <span data-ttu-id="0342f-133">將 **NotificationJobState.FinalStatesOnly** 傳遞到 **AddNew** 方法</span><span class="sxs-lookup"><span data-stu-id="0342f-133">Passes **NotificationJobState.FinalStatesOnly** to the **AddNew** method.</span></span> <span data-ttu-id="0342f-134">(在此範例中，我們只對工作的最終狀態感興趣)。</span><span class="sxs-lookup"><span data-stu-id="0342f-134">(In this example, we are only interested in final states of the job processing.)</span></span>

        job.JobNotificationSubscriptions.AddNew(NotificationJobState.FinalStatesOnly, _notificationEndPoint);
7. <span data-ttu-id="0342f-135">如果您傳遞 **NotificationJobState.All**，即會取得下列所有狀態變更通知：已排入佇列、已排程、處理中，以及已完成。</span><span class="sxs-lookup"><span data-stu-id="0342f-135">If you pass **NotificationJobState.All**, you get all of the following state change notifications: queued, scheduled, processing, and finished.</span></span> <span data-ttu-id="0342f-136">不過，如先前所述，佇列儲存體不保證會按照順序傳遞。</span><span class="sxs-lookup"><span data-stu-id="0342f-136">However, as noted earlier, Queue storage does not guarantee ordered delivery.</span></span> <span data-ttu-id="0342f-137">若要排序訊息，請使用 **Timestamp** 屬性 (定義於以下範例的 **EncodingJobMessage** 類型上)。</span><span class="sxs-lookup"><span data-stu-id="0342f-137">To order messages, use the **Timestamp** property (defined on the **EncodingJobMessage** type in the example below).</span></span> <span data-ttu-id="0342f-138">可能會有重複的訊息。</span><span class="sxs-lookup"><span data-stu-id="0342f-138">Duplicate messages are possible.</span></span> <span data-ttu-id="0342f-139">若要檢查重複項，請使用 **ETag 屬性** (定義於 **EncodingJobMessage** 類型上)。</span><span class="sxs-lookup"><span data-stu-id="0342f-139">To check for duplicates, use the **ETag property** (defined on the **EncodingJobMessage** type).</span></span> <span data-ttu-id="0342f-140">可能也會略過某些狀態變更通知。</span><span class="sxs-lookup"><span data-stu-id="0342f-140">It is also possible that some state change notifications get skipped.</span></span>
8. <span data-ttu-id="0342f-141">每隔 10 秒檢查佇列一次，等候作業進入已完成狀態。</span><span class="sxs-lookup"><span data-stu-id="0342f-141">Waits for the job to get to the finished state by checking the queue every 10 seconds.</span></span> <span data-ttu-id="0342f-142">處理好訊息之後，請予以刪除。</span><span class="sxs-lookup"><span data-stu-id="0342f-142">Deletes messages after they have been processed.</span></span>
9. <span data-ttu-id="0342f-143">刪除佇列和通知端點。</span><span class="sxs-lookup"><span data-stu-id="0342f-143">Deletes the queue and the notification end point.</span></span>

> [!NOTE]
> <span data-ttu-id="0342f-144">要想監視工作的狀態，建議您接聽通知訊息，如下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="0342f-144">The recommended way to monitor a job’s state is by listening to notification messages, as shown in the following example.</span></span>
>
> <span data-ttu-id="0342f-145">或者，使用 **IJob.State** 屬性檢查工作狀態。</span><span class="sxs-lookup"><span data-stu-id="0342f-145">Alternatively, you could check on a job’s state by using the **IJob.State** property.</span></span>  <span data-ttu-id="0342f-146">在 **IJob** 的狀態設定成 [已完成] 之前，您可能會收到一則有關作業已完成的通知訊息。</span><span class="sxs-lookup"><span data-stu-id="0342f-146">A notification message about a job’s completion may arrive before the state on **IJob** is set to **Finished**.</span></span> <span data-ttu-id="0342f-147">**IJob.State** 屬性會延遲片刻再反映正確的狀態。</span><span class="sxs-lookup"><span data-stu-id="0342f-147">The **IJob.State**  property reflects the accurate state with a slight delay.</span></span>
>
>

### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="0342f-148">建立和設定 Visual Studio 專案</span><span class="sxs-lookup"><span data-stu-id="0342f-148">Create and configure a Visual Studio project</span></span>

1. <span data-ttu-id="0342f-149">設定您的開發環境並在 app.config 檔案中填入連線資訊，如[使用 .NET 進行 Media Services 開發](media-services-dotnet-how-to-use.md)所述。</span><span class="sxs-lookup"><span data-stu-id="0342f-149">Set up your development environment and populate the app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 
2. <span data-ttu-id="0342f-150">建立新的資料夾 (資料夾可在本機磁碟機上任意處)，並複製您想要編碼和串流處理或漸進式下載的 .mp4 檔案。</span><span class="sxs-lookup"><span data-stu-id="0342f-150">Create a new folder (folder can be anywhere on your local drive) and copy an .mp4 file that you want to encode and stream or progressively download.</span></span> <span data-ttu-id="0342f-151">在此範例中，使用 "C:\Media" 路徑。</span><span class="sxs-lookup"><span data-stu-id="0342f-151">In this example, the "C:\Media" path is used.</span></span>

### <a name="code"></a><span data-ttu-id="0342f-152">代碼</span><span class="sxs-lookup"><span data-stu-id="0342f-152">Code</span></span>

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

        // Type of the event. Valid values are
        // JobStateChange and NotificationEndpointRegistration.
        public String EventType { get; set; }

        // ETag is used to help the customer detect if
        // the message is a duplicate of another message previously sent.
        public String ETag { get; set; }

        // Time of occurrence of the event.
        public String TimeStamp { get; set; }

        // Collection of values specific to the event.

        // For the JobStateChange event the values are:
        //     JobId - Id of the Job that triggered the notification.
        //     NewState- The new state of the Job. Valid values are:
        //          Scheduled, Processing, Canceling, Cancelled, Error, Finished
        //     OldState- The old state of the Job. Valid values are:
        //          Scheduled, Processing, Canceling, Cancelled, Error, Finished

        // For the NotificationEndpointRegistration event the values are:
        //     NotificationEndpointId- Id of the NotificationEndpoint
        //          that triggered the notification.
        //     State- The state of the Endpoint.
        //          Valid values are: Registered and Unregistered.

        public IDictionary<string, object> Properties { get; set; }
    }

    class Program
    {

        // Read values from the App.config file.
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

            // Create the context.
            var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
            var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

            _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);

            // Create the queue that will be receiving the notification messages.
            _queue = CreateQueue(_StorageConnectionString, endPointAddress);

            // Create the notification point that is mapped to the queue.
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

            // Create the queue client
            CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

            // Retrieve a reference to a queue
            CloudQueue queue = queueClient.GetQueueReference(endPointAddress);

            // Create the queue if it doesn't already exist
            queue.CreateIfNotExists();

            return queue;
        }


        public static IJob SubmitEncodingJobWithNotificationEndPoint(string inputMediaFilePath)
        {
            // Declare a new job.
            IJob job = _context.Jobs.Create("My MP4 to Smooth Streaming encoding job");

            //Create an encrypted asset and upload the mp4.
            IAsset asset = CreateAssetAndUploadSingleFile(AssetCreationOptions.StorageEncrypted,
                inputMediaFilePath);

            // Get a media processor reference, and pass to it the name of the
            // processor to use for the specific task.
            IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Standard");

            // Create a task with the conversion details, using a configuration file.
            ITask task = job.Tasks.AddNew("My encoding Task",
                processor,
                "Adaptive Streaming",
                Microsoft.WindowsAzure.MediaServices.Client.TaskOptions.None);

            // Specify the input asset to be encoded.
            task.InputAssets.Add(asset);

            // Add an output asset to contain the results of the job.
            task.OutputAssets.AddNew("Output asset",
                AssetCreationOptions.None);

            // Add a notification point to the job. You can add multiple notification points.  
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
                // Specify how often you want to get messages from the queue.
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

                        // Display the message information.
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
                    // Delete the message after we've read it.
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
<span data-ttu-id="0342f-153">上述範例會產生下列輸出。</span><span class="sxs-lookup"><span data-stu-id="0342f-153">The preceding example produced the following output.</span></span> <span data-ttu-id="0342f-154">您的值會不一樣。</span><span class="sxs-lookup"><span data-stu-id="0342f-154">Your values will vary.</span></span>

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
        JobName: My MP4 to Smooth Streaming encoding job
        NewState: Finished
        OldState: Processing
        AccountName: westeuropewamsaccount
    job with Id: nb:jid:UUID:526291de-f166-be47-b62a-11ffe6d4be54 reached expected
    State: Finished


## <a name="next-step"></a><span data-ttu-id="0342f-155">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0342f-155">Next step</span></span>
<span data-ttu-id="0342f-156">檢閱媒體服務學習路徑。</span><span class="sxs-lookup"><span data-stu-id="0342f-156">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="0342f-157">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="0342f-157">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
