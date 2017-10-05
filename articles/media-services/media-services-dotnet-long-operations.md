---
title: "輪詢長時間執行的作業 | Microsoft Docs"
description: "本主題說明如何輪詢長時間執行的作業。"
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 9a68c4b1-6159-42fe-9439-a3661a90ae03
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: juliako
ms.openlocfilehash: 7123a2d44d3b7c332afe30fb0fcea88ca29e313a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="delivering-live-streaming-with-azure-media-services"></a><span data-ttu-id="64544-103">利用 Azure 媒體服務提供即時資料流</span><span class="sxs-lookup"><span data-stu-id="64544-103">Delivering Live Streaming with Azure Media Services</span></span>

## <a name="overview"></a><span data-ttu-id="64544-104">Overview</span><span class="sxs-lookup"><span data-stu-id="64544-104">Overview</span></span>

<span data-ttu-id="64544-105">Microsoft Azure 媒體服務提供將要求傳送至媒體服務以啟動作業 (如建立、啟動、停止或刪除頻道) 的 API。</span><span class="sxs-lookup"><span data-stu-id="64544-105">Microsoft Azure Media Services offers APIs that send requests to Media Services to start operations (for example: create, start, stop, or delete a channel).</span></span> <span data-ttu-id="64544-106">這些作業屬於長時間執行的作業。</span><span class="sxs-lookup"><span data-stu-id="64544-106">These operations are long-running.</span></span>

<span data-ttu-id="64544-107">Media Services .NET SDK 提供能傳送要求並等候作業完成的 API (API 會在內部依照某些間隔輪詢作業進度).</span><span class="sxs-lookup"><span data-stu-id="64544-107">The Media Services .NET SDK provides APIs that send the request and wait for the operation to complete (internally, the APIs are polling for operation progress at some intervals).</span></span> <span data-ttu-id="64544-108">例如，當您呼叫 channel.Start() 時，方法會在通道啟動後返回。</span><span class="sxs-lookup"><span data-stu-id="64544-108">For example, when you call channel.Start(), the method returns after the channel is started.</span></span> <span data-ttu-id="64544-109">您也可以使用非同步的 version: await channel.StartAsync() (如需以工作為基礎的非同步模式，請參閱 [TAP](https://msdn.microsoft.com/library/hh873175\(v=vs.110\).aspx))。</span><span class="sxs-lookup"><span data-stu-id="64544-109">You can also use the asynchronous version: await channel.StartAsync() (for information about Task-based Asynchronous Pattern, see [TAP](https://msdn.microsoft.com/library/hh873175\(v=vs.110\).aspx)).</span></span> <span data-ttu-id="64544-110">傳送作業要求並輪詢狀態，直到作業完成為止的 API 稱為「輪詢方法」。</span><span class="sxs-lookup"><span data-stu-id="64544-110">APIs that send an operation request and then poll for the status until the operation is complete are called “polling methods”.</span></span> <span data-ttu-id="64544-111">我們建議豐富型用戶端應用程式和/或可設定狀態的服務使用這些方法 (尤其是非同步版本)。</span><span class="sxs-lookup"><span data-stu-id="64544-111">These methods (especially the Async version) are recommended for rich client applications and/or stateful services.</span></span>

<span data-ttu-id="64544-112">我們有一些無法等候長時間執行之 http 要求，並想要的手動輪詢作業進度之應用程式的案例。</span><span class="sxs-lookup"><span data-stu-id="64544-112">There are scenarios where an application cannot wait for a long running http request and wants to poll for the operation progress manually.</span></span> <span data-ttu-id="64544-113">與無狀態 Web 服務互動之瀏覽器是典型的範例：當瀏覽器要求建立通道時，Web 服務會起始長時間執行的作業，並將作業識別碼傳回瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="64544-113">A typical example would be a browser interacting with a stateless web service: when the browser requests to create a channel, the web service initiates a long running operation and returns the operation ID to the browser.</span></span> <span data-ttu-id="64544-114">接著，瀏覽器會要求 Web 服務來根據識別碼取得作業狀態。</span><span class="sxs-lookup"><span data-stu-id="64544-114">The browser could then ask the web service to get the operation status based on the ID.</span></span> <span data-ttu-id="64544-115">Media Services .NET SDK 提供適用於此案例的 API。</span><span class="sxs-lookup"><span data-stu-id="64544-115">The Media Services .NET SDK provides APIs that are useful for this scenario.</span></span> <span data-ttu-id="64544-116">這些 API 稱為「非輪詢方法」。</span><span class="sxs-lookup"><span data-stu-id="64544-116">These APIs are called “non-polling methods”.</span></span>
<span data-ttu-id="64544-117">「非輪詢方法」的命名模式如下：SendOperationNameOperation (例如，SendCreateOperation)。</span><span class="sxs-lookup"><span data-stu-id="64544-117">The “non-polling methods” have the following naming pattern: Send*OperationName*Operation (for example, SendCreateOperation).</span></span> <span data-ttu-id="64544-118">SendOperationNameOperation 方法會傳回 **IOperation** 物件；傳回的物件含有可用來追蹤作業的資訊。</span><span class="sxs-lookup"><span data-stu-id="64544-118">Send*OperationName*Operation methods return the **IOperation** object; the returned object contains information that can be used to track the operation.</span></span> <span data-ttu-id="64544-119">Send*OperationName*OperationAsync 方法會傳回 **Task<IOperation>**。</span><span class="sxs-lookup"><span data-stu-id="64544-119">The Send*OperationName*OperationAsync methods return **Task<IOperation>**.</span></span>

<span data-ttu-id="64544-120">以下是目前支援非輪詢方法的類別：**通道**、**StreamingEndpoint** 及**程式**。</span><span class="sxs-lookup"><span data-stu-id="64544-120">Currently, the following classes support non-polling methods:  **Channel**, **StreamingEndpoint**, and **Program**.</span></span>

<span data-ttu-id="64544-121">若要輪詢作業狀態，請針對 **OperationBaseCollection** 類別使用 **GetOperation** 方法。</span><span class="sxs-lookup"><span data-stu-id="64544-121">To poll for the operation status, use the **GetOperation** method on the **OperationBaseCollection** class.</span></span> <span data-ttu-id="64544-122">請使用下列間隔來檢查作業狀態：對於**通道**和 **StreamingEndpoint** 作業，使用 30 秒；對於**程式**作業，使用 10 秒。</span><span class="sxs-lookup"><span data-stu-id="64544-122">Use the following intervals to check the operation status: for **Channel** and **StreamingEndpoint** operations, use 30 seconds; for **Program** operations, use 10 seconds.</span></span>

## <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="64544-123">建立和設定 Visual Studio 專案</span><span class="sxs-lookup"><span data-stu-id="64544-123">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="64544-124">設定您的開發環境並在 app.config 檔案中填入連線資訊，如[使用 .NET 進行 Media Services 開發](media-services-dotnet-how-to-use.md)中所述。</span><span class="sxs-lookup"><span data-stu-id="64544-124">Set up your development environment and populate the app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span>

## <a name="example"></a><span data-ttu-id="64544-125">範例</span><span class="sxs-lookup"><span data-stu-id="64544-125">Example</span></span>

<span data-ttu-id="64544-126">以下範例定義名為 **ChannelOperations**的類別。</span><span class="sxs-lookup"><span data-stu-id="64544-126">The following example defines a class called **ChannelOperations**.</span></span> <span data-ttu-id="64544-127">此類別定義可能是 Web 服務類別定義的起始點。</span><span class="sxs-lookup"><span data-stu-id="64544-127">This class definition could be a starting point for your web service class definition.</span></span> <span data-ttu-id="64544-128">為了簡單起見，以下範例使用非同步版本的方法。</span><span class="sxs-lookup"><span data-stu-id="64544-128">For simplicity, the following examples use the non-async versions of methods.</span></span>

<span data-ttu-id="64544-129">此範例也示範用戶端如何使用這個類別。</span><span class="sxs-lookup"><span data-stu-id="64544-129">The example also shows how the client might use this class.</span></span>

### <a name="channeloperations-class-definition"></a><span data-ttu-id="64544-130">ChannelOperations class definition</span><span class="sxs-lookup"><span data-stu-id="64544-130">ChannelOperations class definition</span></span>

    using Microsoft.WindowsAzure.MediaServices.Client;
    using System;
    using System.Collections.Generic;
    using System.Configuration;
    using System.Net;

    /// <summary> 
    /// The ChannelOperations class only implements 
    /// the Channel’s creation operation. 
    /// </summary> 
    public class ChannelOperations
    {
        // Read values from the App.config file.
        private static readonly string _AADTenantDomain =
            ConfigurationManager.AppSettings["AADTenantDomain"];
        private static readonly string _RESTAPIEndpoint =
            ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];

        // Field for service context.
        private static CloudMediaContext _context = null;

        public ChannelOperations()
        {
            var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
            var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

            _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);
        }

        /// <summary>  
        /// Initiates the creation of a new channel.  
        /// </summary>  
        /// <param name="channelName">Name to be given to the new channel</param>  
        /// <returns>  
        /// Operation Id for the long running operation being executed by Media Services. 
        /// Use this operation Id to poll for the channel creation status. 
        /// </returns> 
        public string StartChannelCreation(string channelName)
        {
            var operation = _context.Channels.SendCreateOperation(
                new ChannelCreationOptions
                {
                    Name = channelName,
                    Input = CreateChannelInput(),
                    Preview = CreateChannelPreview(),
                    Output = CreateChannelOutput()
                });

            return operation.Id;
        }

        /// <summary> 
        /// Checks if the operation has been completed. 
        /// If the operation succeeded, the created channel Id is returned in the out parameter.
        /// </summary> 
        /// <param name="operationId">The operation Id.</param> 
        /// <param name="channel">
        /// If the operation succeeded, 
        /// the created channel Id is returned in the out parameter.</param>
        /// <returns>Returns false if the operation is still in progress; otherwise, true.</returns> 
        public bool IsCompleted(string operationId, out string channelId)
        {
            IOperation operation = _context.Operations.GetOperation(operationId);
            bool completed = false;

            channelId = null;

            switch (operation.State)
            {
                case OperationState.Failed:
                    // Handle the failure. 
                    // For example, throw an exception. 
                    // Use the following information in the exception: operationId, operation.ErrorMessage.
                    break;
                case OperationState.Succeeded:
                    completed = true;
                    channelId = operation.TargetEntityId;
                    break;
                case OperationState.InProgress:
                    completed = false;
                    break;
            }
            return completed;
        }

        private static ChannelInput CreateChannelInput()
        {
            return new ChannelInput
            {
                StreamingProtocol = StreamingProtocol.RTMP,
                AccessControl = new ChannelAccessControl
                {
                    IPAllowList = new List<IPRange>
                        {
                            new IPRange
                            {
                                Name = "TestChannelInput001",
                                Address = IPAddress.Parse("0.0.0.0"),
                                SubnetPrefixLength = 0
                            }
                        }
                }
            };
        }

        private static ChannelPreview CreateChannelPreview()
        {
            return new ChannelPreview
            {
                AccessControl = new ChannelAccessControl
                {
                    IPAllowList = new List<IPRange>
                        {
                            new IPRange
                            {
                                Name = "TestChannelPreview001",
                                Address = IPAddress.Parse("0.0.0.0"),
                                SubnetPrefixLength = 0
                            }
                        }
                }
            };
        }

        private static ChannelOutput CreateChannelOutput()
        {
            return new ChannelOutput
            {
                Hls = new ChannelOutputHls { FragmentsPerSegment = 1 }
            };
        }
    }

### <a name="the-client-code"></a><span data-ttu-id="64544-131">The client code</span><span class="sxs-lookup"><span data-stu-id="64544-131">The client code</span></span>
    ChannelOperations channelOperations = new ChannelOperations();
    string opId = channelOperations.StartChannelCreation("MyChannel001");

    string channelId = null;
    bool isCompleted = false;

    while (isCompleted == false)
    {
        System.Threading.Thread.Sleep(TimeSpan.FromSeconds(30));
        isCompleted = channelOperations.IsCompleted(opId, out channelId);
    }

    // If we got here, we should have the newly created channel id.
    Console.WriteLine(channelId);



## <a name="media-services-learning-paths"></a><span data-ttu-id="64544-132">媒體服務學習路徑</span><span class="sxs-lookup"><span data-stu-id="64544-132">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="64544-133">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="64544-133">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

