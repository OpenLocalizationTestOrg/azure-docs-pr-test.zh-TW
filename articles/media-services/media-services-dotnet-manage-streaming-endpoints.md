---
title: "aaaManage 串流端點，其中包含.NET SDK。 | Microsoft Docs"
description: "本主題說明如何 toomanage 串流端點，其中包含 hello Azure 入口網站。"
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
ms.openlocfilehash: 30c092a8ebf4e2b2902392f4cf98f46d812ccdbc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-streaming-endpoints-with-net-sdk"></a><span data-ttu-id="744ac-104">使用 .NET SDK 來管理串流端點</span><span class="sxs-lookup"><span data-stu-id="744ac-104">Manage streaming endpoints with .NET SDK</span></span>

>[!NOTE]
><span data-ttu-id="744ac-105">請確定 tooreview hello[概觀](media-services-streaming-endpoints-overview.md)主題。</span><span class="sxs-lookup"><span data-stu-id="744ac-105">Make sure tooreview hello [overview](media-services-streaming-endpoints-overview.md) topic.</span></span> <span data-ttu-id="744ac-106">此外，也請檢閱 [StreamingEndpoint](https://docs.microsoft.com/rest/api/media/operations/streamingendpoint)。</span><span class="sxs-lookup"><span data-stu-id="744ac-106">Also, review [StreamingEndpoint](https://docs.microsoft.com/rest/api/media/operations/streamingendpoint).</span></span>

<span data-ttu-id="744ac-107">本主題中的 hello 程式碼會示範下列工作使用 toodo hello hello Azure Media Services.NET SDK 的方式：</span><span class="sxs-lookup"><span data-stu-id="744ac-107">hello code in this topic shows how toodo hello following tasks using hello Azure Media Services .NET SDK:</span></span>

- <span data-ttu-id="744ac-108">檢查 hello 預設串流端點。</span><span class="sxs-lookup"><span data-stu-id="744ac-108">Examine hello default streaming endpoint.</span></span>
- <span data-ttu-id="744ac-109">建立/新增新的串流端點。</span><span class="sxs-lookup"><span data-stu-id="744ac-109">Create/add new streaming endpoint.</span></span>

    <span data-ttu-id="744ac-110">您可能會想 toohave 多個串流端點如果您計劃 toohave 不同 Cdn 或 CDN 和直接存取。</span><span class="sxs-lookup"><span data-stu-id="744ac-110">You might want toohave multiple streaming endpoints if you plan toohave different CDNs or a CDN and direct access.</span></span>

    > [!NOTE]
    > <span data-ttu-id="744ac-111">只有當串流端點處於執行中狀態時，才會向您收取費用。</span><span class="sxs-lookup"><span data-stu-id="744ac-111">You are only billed when your Streaming Endpoint is in running state.</span></span>
    
- <span data-ttu-id="744ac-112">更新串流端點的 hello。</span><span class="sxs-lookup"><span data-stu-id="744ac-112">Update hello streaming endpoint.</span></span>
    
    <span data-ttu-id="744ac-113">請確定 toocall hello update （） 函式。</span><span class="sxs-lookup"><span data-stu-id="744ac-113">Make sure toocall hello Update() function.</span></span>

- <span data-ttu-id="744ac-114">刪除串流端點的 hello。</span><span class="sxs-lookup"><span data-stu-id="744ac-114">Delete hello streaming endpoint.</span></span>

    >[!NOTE]
    ><span data-ttu-id="744ac-115">無法刪除 hello 預設串流端點。</span><span class="sxs-lookup"><span data-stu-id="744ac-115">hello default streaming endpoint cannot be deleted.</span></span>

<span data-ttu-id="744ac-116">如需如何 tooscale hello 串流端點資訊，請參閱[這](media-services-portal-scale-streaming-endpoints.md)主題。</span><span class="sxs-lookup"><span data-stu-id="744ac-116">For information about how tooscale hello streaming endpoint, see [this](media-services-portal-scale-streaming-endpoints.md) topic.</span></span>

## <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="744ac-117">建立和設定 Visual Studio 專案</span><span class="sxs-lookup"><span data-stu-id="744ac-117">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="744ac-118">設定您的開發環境，並填入 hello 與連接資訊的 app.config 檔案中所述[與.NET 的 Media Services 開發](media-services-dotnet-how-to-use.md)。</span><span class="sxs-lookup"><span data-stu-id="744ac-118">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

## <a name="add-code-that-manages-streaming-endpoints"></a><span data-ttu-id="744ac-119">新增可管理串流端點的程式碼</span><span class="sxs-lookup"><span data-stu-id="744ac-119">Add code that manages streaming endpoints</span></span>
    
<span data-ttu-id="744ac-120">取代下列程式碼的 hello hello hello Program.cs 中的程式碼：</span><span class="sxs-lookup"><span data-stu-id="744ac-120">Replace hello code in hello Program.cs with hello following code:</span></span>

    using System;
    using System.Configuration;
    using System.Linq;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using Microsoft.WindowsAzure.MediaServices.Client.Live;

    namespace AMSStreamingEndpoint
    {
        class Program
        {
        // Read values from hello App.config file.
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


## <a name="next-steps"></a><span data-ttu-id="744ac-121">後續步驟</span><span class="sxs-lookup"><span data-stu-id="744ac-121">Next steps</span></span>
<span data-ttu-id="744ac-122">檢閱媒體服務學習路徑。</span><span class="sxs-lookup"><span data-stu-id="744ac-122">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="744ac-123">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="744ac-123">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

