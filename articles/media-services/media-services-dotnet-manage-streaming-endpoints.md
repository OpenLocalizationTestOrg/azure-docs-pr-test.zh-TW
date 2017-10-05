---
title: "使用 .NET SDK 來管理串流端點。 | Microsoft Docs"
description: "本主題說明如何透過 Azure 入口網站管理串流端點。"
services: media-services
documentationcenter: 
author: Juliako
writer: juliako
manager: cfowler
editor: 
ms.assetid: 0da34a97-f36c-48d0-8ea2-ec12584a2215
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: juliako
ms.openlocfilehash: 2f4f464f8604b6f453d6b50b736c6a3a889a3408
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="manage-streaming-endpoints-with-net-sdk"></a><span data-ttu-id="3537f-104">使用 .NET SDK 來管理串流端點</span><span class="sxs-lookup"><span data-stu-id="3537f-104">Manage streaming endpoints with .NET SDK</span></span>

>[!NOTE]
><span data-ttu-id="3537f-105">請務必檢閱[概觀](media-services-streaming-endpoints-overview.md)主題。</span><span class="sxs-lookup"><span data-stu-id="3537f-105">Make sure to review the [overview](media-services-streaming-endpoints-overview.md) topic.</span></span> <span data-ttu-id="3537f-106">此外，也請檢閱 [StreamingEndpoint](https://docs.microsoft.com/rest/api/media/operations/streamingendpoint)。</span><span class="sxs-lookup"><span data-stu-id="3537f-106">Also, review [StreamingEndpoint](https://docs.microsoft.com/rest/api/media/operations/streamingendpoint).</span></span>

<span data-ttu-id="3537f-107">本主題中的程式碼示範如何使用「Azure 媒體服務 .NET SDK」來執行下列工作：</span><span class="sxs-lookup"><span data-stu-id="3537f-107">The code in this topic shows how to do the following tasks using the Azure Media Services .NET SDK:</span></span>

- <span data-ttu-id="3537f-108">檢查預設串流端點。</span><span class="sxs-lookup"><span data-stu-id="3537f-108">Examine the default streaming endpoint.</span></span>
- <span data-ttu-id="3537f-109">建立/新增新的串流端點。</span><span class="sxs-lookup"><span data-stu-id="3537f-109">Create/add new streaming endpoint.</span></span>

    <span data-ttu-id="3537f-110">如果您打算有不同的 CDN 或一個 CDN 和直接存取，您可能會想要有多個串流端點。</span><span class="sxs-lookup"><span data-stu-id="3537f-110">You might want to have multiple streaming endpoints if you plan to have different CDNs or a CDN and direct access.</span></span>

    > [!NOTE]
    > <span data-ttu-id="3537f-111">只有當串流端點處於執行中狀態時，才會向您收取費用。</span><span class="sxs-lookup"><span data-stu-id="3537f-111">You are only billed when your Streaming Endpoint is in running state.</span></span>
    
- <span data-ttu-id="3537f-112">更新串流端點。</span><span class="sxs-lookup"><span data-stu-id="3537f-112">Update the streaming endpoint.</span></span>
    
    <span data-ttu-id="3537f-113">請務必呼叫 Update() 函式。</span><span class="sxs-lookup"><span data-stu-id="3537f-113">Make sure to call the Update() function.</span></span>

- <span data-ttu-id="3537f-114">刪除串流端點。</span><span class="sxs-lookup"><span data-stu-id="3537f-114">Delete the streaming endpoint.</span></span>

    >[!NOTE]
    ><span data-ttu-id="3537f-115">預設串流端點不可刪除。</span><span class="sxs-lookup"><span data-stu-id="3537f-115">The default streaming endpoint cannot be deleted.</span></span>

<span data-ttu-id="3537f-116">如需調整串流端點的相關資訊，請參閱 [這個](media-services-portal-scale-streaming-endpoints.md) 主題。</span><span class="sxs-lookup"><span data-stu-id="3537f-116">For information about how to scale the streaming endpoint, see [this](media-services-portal-scale-streaming-endpoints.md) topic.</span></span>

## <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="3537f-117">建立和設定 Visual Studio 專案</span><span class="sxs-lookup"><span data-stu-id="3537f-117">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="3537f-118">設定您的開發環境並在 app.config 檔案中填入連線資訊，如[使用 .NET 進行 Media Services 開發](media-services-dotnet-how-to-use.md)中所述。</span><span class="sxs-lookup"><span data-stu-id="3537f-118">Set up your development environment and populate the app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

## <a name="add-code-that-manages-streaming-endpoints"></a><span data-ttu-id="3537f-119">新增可管理串流端點的程式碼</span><span class="sxs-lookup"><span data-stu-id="3537f-119">Add code that manages streaming endpoints</span></span>
    
<span data-ttu-id="3537f-120">以下列程式碼取代 Program.cs 中的程式碼：</span><span class="sxs-lookup"><span data-stu-id="3537f-120">Replace the code in the Program.cs with the following code:</span></span>

    using System;
    using System.Configuration;
    using System.Linq;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using Microsoft.WindowsAzure.MediaServices.Client.Live;

    namespace AMSStreamingEndpoint
    {
        class Program
        {
        // Read values from the App.config file.
        private static readonly string _AADTenantDomain =
        ConfigurationManager.AppSettings["AADTenantDomain"];
        private static readonly string _RESTAPIEndpoint =
        ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];

        private static CloudMediaContext _context = null;

        static void Main(string[] args)
        {
            var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
            var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

            _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);

            var defaultStreamingEndpoint = _context.StreamingEndpoints.Where(s => s.Name.Contains("default")).FirstOrDefault();
            ExamineStreamingEndpoint(defaultStreamingEndpoint);

            IStreamingEndpoint newStreamingEndpoint = AddStreamingEndpoint();
            UpdateStreamingEndpoint(newStreamingEndpoint);
            DeleteStreamingEndpoint(newStreamingEndpoint);
        }

        static public void ExamineStreamingEndpoint(IStreamingEndpoint streamingEndpoint)
        {
            Console.WriteLine(streamingEndpoint.Name);
            Console.WriteLine(streamingEndpoint.StreamingEndpointVersion);
            Console.WriteLine(streamingEndpoint.FreeTrialEndTime);
            Console.WriteLine(streamingEndpoint.ScaleUnits);
            Console.WriteLine(streamingEndpoint.CdnProvider);
            Console.WriteLine(streamingEndpoint.CdnProfile);
            Console.WriteLine(streamingEndpoint.CdnEnabled);
        }

        static public IStreamingEndpoint AddStreamingEndpoint()
        {
            var name = "StreamingEndpoint" + DateTime.UtcNow.ToString("hhmmss");
            var option = new StreamingEndpointCreationOptions(name, 1)
            {
            StreamingEndpointVersion = new Version("2.0"),
            CdnEnabled = true,
            CdnProfile = "CdnProfile",
            CdnProvider = CdnProviderType.PremiumVerizon
            };

            var streamingEndpoint = _context.StreamingEndpoints.Create(option);

            return streamingEndpoint;
        }

        static public void UpdateStreamingEndpoint(IStreamingEndpoint streamingEndpoint)
        {
            if (streamingEndpoint.StreamingEndpointVersion == "1.0")
            streamingEndpoint.StreamingEndpointVersion = "2.0";

            streamingEndpoint.CdnEnabled = false;
            streamingEndpoint.Update();
        }

        static public void DeleteStreamingEndpoint(IStreamingEndpoint streamingEndpoint)
        {
            streamingEndpoint.Delete();
        }
        }
    }


## <a name="next-steps"></a><span data-ttu-id="3537f-121">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3537f-121">Next steps</span></span>
<span data-ttu-id="3537f-122">檢閱媒體服務學習路徑。</span><span class="sxs-lookup"><span data-stu-id="3537f-122">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="3537f-123">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="3537f-123">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

