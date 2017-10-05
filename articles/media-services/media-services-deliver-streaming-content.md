---
title: "使用 .NET 發佈 Azure 媒體服務內容 | Microsoft Docs"
description: "了解如何建立定位器，用來建置串流 URL。 程式碼範例以 C# 撰寫，並使用 Media Services SDK for .NET。"
author: juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: c53b1f83-4cb1-4b09-840f-9c145b7d6f8d
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: juliako
ms.openlocfilehash: 2bcb012eef84faa7c1e13ed22e88e45e4300ed54
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="publish-azure-media-services-content-using-net"></a><span data-ttu-id="30787-104">使用 .NET 發佈 Azure 媒體服務內容</span><span class="sxs-lookup"><span data-stu-id="30787-104">Publish Azure Media Services content using .NET</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="30787-105">REST</span><span class="sxs-lookup"><span data-stu-id="30787-105">REST</span></span>](media-services-rest-deliver-streaming-content.md)
> * [<span data-ttu-id="30787-106">.NET</span><span class="sxs-lookup"><span data-stu-id="30787-106">.NET</span></span>](media-services-deliver-streaming-content.md)
> * [<span data-ttu-id="30787-107">入口網站</span><span class="sxs-lookup"><span data-stu-id="30787-107">Portal</span></span>](media-services-portal-publish.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="30787-108">Overview</span><span class="sxs-lookup"><span data-stu-id="30787-108">Overview</span></span>
<span data-ttu-id="30787-109">您可以建立隨選串流定位器及建置串流 URL，串流處理調適性位元速率 MP4 集。</span><span class="sxs-lookup"><span data-stu-id="30787-109">You can stream an adaptive bitrate MP4 set by creating an OnDemand streaming locator and building a streaming URL.</span></span> <span data-ttu-id="30787-110">[為資產編碼](media-services-encode-asset.md) 主題說明如何編碼為調適性位元速率 MP4 集。</span><span class="sxs-lookup"><span data-stu-id="30787-110">The [encoding an asset](media-services-encode-asset.md) topic shows how to encode into an adaptive bitrate MP4 set.</span></span> 

> [!NOTE]
> <span data-ttu-id="30787-111">如果您的內容已加密，請在建立定位器之前設定資產傳遞原則 (如 [這個](media-services-dotnet-configure-asset-delivery-policy.md) 主題中所述)。</span><span class="sxs-lookup"><span data-stu-id="30787-111">If your content is encrypted, configure asset delivery policy (as described in [this](media-services-dotnet-configure-asset-delivery-policy.md) topic) before creating a locator.</span></span> 
> 
> 

<span data-ttu-id="30787-112">您也可以使用隨選串流定位器來建置指向可漸進式下載之 MP4 檔案的 URL。</span><span class="sxs-lookup"><span data-stu-id="30787-112">You can also use an OnDemand streaming locator to build URLs that point to MP4 files that can be progressively downloaded.</span></span>  

<span data-ttu-id="30787-113">本主題說明如何建立隨選串流定位器，以發佈資產及建置 Smooth、MPEG DASH 和 HLS 串流 URL。</span><span class="sxs-lookup"><span data-stu-id="30787-113">This topic shows how to create an OnDemand streaming locator to publish your asset and build a Smooth, MPEG DASH, and HLS streaming URLs.</span></span> <span data-ttu-id="30787-114">它也會示範如何建置漸進式下載 URL。</span><span class="sxs-lookup"><span data-stu-id="30787-114">It also shows hot to build progressive download URLs.</span></span> 

## <a name="create-an-ondemand-streaming-locator"></a><span data-ttu-id="30787-115">建立隨選串流定位器</span><span class="sxs-lookup"><span data-stu-id="30787-115">Create an OnDemand streaming locator</span></span>
<span data-ttu-id="30787-116">若要建立隨選串流定位器並取得 URL，您需要執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="30787-116">To create the OnDemand streaming locator and get URLs, you need to do the following things:</span></span>

1. <span data-ttu-id="30787-117">如果內容已加密，請定義存取原則。</span><span class="sxs-lookup"><span data-stu-id="30787-117">If the content is encrypted, define an access policy.</span></span>
2. <span data-ttu-id="30787-118">建立隨選串流定位器。</span><span class="sxs-lookup"><span data-stu-id="30787-118">Create an OnDemand streaming locator.</span></span>
3. <span data-ttu-id="30787-119">如果您想要串流處理，請取得資產內的串流資訊清單檔案 (.ism)。</span><span class="sxs-lookup"><span data-stu-id="30787-119">If you plan to stream, get the streaming manifest file (.ism) in the asset.</span></span> 
   
   <span data-ttu-id="30787-120">如果您想要漸進式地下載，請取得資產中的 MP4 檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="30787-120">If you plan to progressively download, get the names of MP4 files in the asset.</span></span>  
4. <span data-ttu-id="30787-121">建置資訊清單檔或 MP4 檔案的 URL。</span><span class="sxs-lookup"><span data-stu-id="30787-121">Build URLs to the manifest file or MP4 files.</span></span> 


>[!NOTE]
><span data-ttu-id="30787-122">對於不同的 AMS 原則 (例如 Locator 原則或 ContentKeyAuthorizationPolicy) 有 1,000,000 個原則的限制。</span><span class="sxs-lookup"><span data-stu-id="30787-122">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="30787-123">如果您一律使用相同的天數 / 存取權限，則應該使用相同的原則識別碼。</span><span class="sxs-lookup"><span data-stu-id="30787-123">Use the same policy ID if you are always using the same days / access permissions.</span></span> <span data-ttu-id="30787-124">例如，為預定要長時間維持就地 (非上傳原則) 的定位器原則。</span><span class="sxs-lookup"><span data-stu-id="30787-124">For example, policies for locators that are intended to remain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="30787-125">如需詳細資訊，請參閱 [這個](media-services-dotnet-manage-entities.md#limit-access-policies) 主題。</span><span class="sxs-lookup"><span data-stu-id="30787-125">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

### <a name="use-media-services-net-sdk"></a><span data-ttu-id="30787-126">使用 Media Services .NET SDK</span><span class="sxs-lookup"><span data-stu-id="30787-126">Use Media Services .NET SDK</span></span>
<span data-ttu-id="30787-127">建置串流 URL</span><span class="sxs-lookup"><span data-stu-id="30787-127">Build Streaming URLs</span></span> 

    private static void BuildStreamingURLs(IAsset asset)
    {

        // Create a 30-day readonly access policy. 
          // You cannot create a streaming locator using an AccessPolicy that includes write or delete permissions.
        IAccessPolicy policy = _context.AccessPolicies.Create("Streaming policy",
            TimeSpan.FromDays(30),
            AccessPermissions.Read);

        // Create a locator to the streaming content on an origin. 
        ILocator originLocator = _context.Locators.CreateLocator(LocatorType.OnDemandOrigin, asset,
            policy,
            DateTime.UtcNow.AddMinutes(-5));

        // Display some useful values based on the locator.
        Console.WriteLine("Streaming asset base path on origin: ");
        Console.WriteLine(originLocator.Path);
        Console.WriteLine();

        // Get a reference to the streaming manifest file from the  
        // collection of files in the asset. 
        var manifestFile = asset.AssetFiles.Where(f => f.Name.ToLower().
                                    EndsWith(".ism")).
                                    FirstOrDefault();

        // Create a full URL to the manifest file. Use this for playback
        // in streaming media clients. 
        string urlForClientStreaming = originLocator.Path + manifestFile.Name + "/manifest";
        Console.WriteLine("URL to manifest for client streaming using Smooth Streaming protocol: ");
        Console.WriteLine(urlForClientStreaming);
        Console.WriteLine("URL to manifest for client streaming using HLS protocol: ");
        Console.WriteLine(urlForClientStreaming + "(format=m3u8-aapl)");
        Console.WriteLine("URL to manifest for client streaming using MPEG DASH protocol: ");
        Console.WriteLine(urlForClientStreaming + "(format=mpd-time-csf)"); 
        Console.WriteLine();
    }

<span data-ttu-id="30787-128">輸出：</span><span class="sxs-lookup"><span data-stu-id="30787-128">The outputs:</span></span>

    URL to manifest for client streaming using Smooth Streaming protocol:
    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny.ism/manifest
    URL to manifest for client streaming using HLS protocol:
    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny.ism/manifest(format=m3u8-aapl)
    URL to manifest for client streaming using MPEG DASH protocol:
    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny.ism/manifest(format=mpd-time-csf)


> [!NOTE]
> <span data-ttu-id="30787-129">您也可以透過 SSL 連線串流您的內容。</span><span class="sxs-lookup"><span data-stu-id="30787-129">You can also stream your content over an SSL connection.</span></span> <span data-ttu-id="30787-130">若要執行這個方法，請確定您的串流 URL 是以 HTTPS 開頭。</span><span class="sxs-lookup"><span data-stu-id="30787-130">To do this approach, make sure your streaming URLs start with HTTPS.</span></span> <span data-ttu-id="30787-131">目前 AMS 不支援使用 SSL 搭配自訂網域。</span><span class="sxs-lookup"><span data-stu-id="30787-131">Currently, AMS doesn’t support SSL with custom domains.</span></span>
> 
> 

<span data-ttu-id="30787-132">建置漸進式下載 URL</span><span class="sxs-lookup"><span data-stu-id="30787-132">Build progressive download URLs</span></span> 

    private static void BuildProgressiveDownloadURLs(IAsset asset)
    {
        // Create a 30-day readonly access policy. 
        IAccessPolicy policy = _context.AccessPolicies.Create("Streaming policy",
            TimeSpan.FromDays(30),
            AccessPermissions.Read);

        // Create an OnDemandOrigin locator to the asset. 
        ILocator originLocator = _context.Locators.CreateLocator(LocatorType.OnDemandOrigin, asset,
            policy,
            DateTime.UtcNow.AddMinutes(-5));

        // Display some useful values based on the locator.
        Console.WriteLine("Streaming asset base path on origin: ");
        Console.WriteLine(originLocator.Path);
        Console.WriteLine();

        // Get MP4 files.
        IEnumerable<IAssetFile> mp4AssetFiles = asset
            .AssetFiles
            .ToList()
            .Where(af => af.Name.EndsWith(".mp4", StringComparison.OrdinalIgnoreCase));

        // Create a full URL to the MP4 files. Use this to progressively download files.
        foreach (var pd in mp4AssetFiles)
            Console.WriteLine(originLocator.Path + pd.Name);
    }

<span data-ttu-id="30787-133">輸出：</span><span class="sxs-lookup"><span data-stu-id="30787-133">The outputs:</span></span>

    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny_H264_650kbps_AAC_und_ch2_96kbps.mp4
    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny_H264_400kbps_AAC_und_ch2_96kbps.mp4
    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny_H264_3400kbps_AAC_und_ch2_96kbps.mp4
    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny_H264_2250kbps_AAC_und_ch2_96kbps.mp4

    . . . 

### <a name="use-media-services-net-sdk-extensions"></a><span data-ttu-id="30787-134">使用 Media Services .NET SDK 延伸模組</span><span class="sxs-lookup"><span data-stu-id="30787-134">Use Media Services .NET SDK Extensions</span></span>
<span data-ttu-id="30787-135">下列程式碼會呼叫 .NET SDK 擴充功能方法，以針對調適性串流建立定位器並產生 Smooth Streaming、HLS 和 MPEG-DASH URL。</span><span class="sxs-lookup"><span data-stu-id="30787-135">The following code calls .NET SDK extensions methods that create a locator and generate the Smooth Streaming, HLS, and MPEG-DASH URLs for adaptive streaming.</span></span>

    // Create a loctor.
    _context.Locators.Create(
        LocatorType.OnDemandOrigin,
        inputAsset,
        AccessPermissions.Read,
        TimeSpan.FromDays(30));

    // Get the streaming URLs.
    Uri smoothStreamingUri = inputAsset.GetSmoothStreamingUri();
    Uri hlsUri = inputAsset.GetHlsUri();
    Uri mpegDashUri = inputAsset.GetMpegDashUri();

    Console.WriteLine(smoothStreamingUri);
    Console.WriteLine(hlsUri);
    Console.WriteLine(mpegDashUri);


## <a name="media-services-learning-paths"></a><span data-ttu-id="30787-136">媒體服務學習路徑</span><span class="sxs-lookup"><span data-stu-id="30787-136">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="30787-137">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="30787-137">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a><span data-ttu-id="30787-138">後續步驟</span><span class="sxs-lookup"><span data-stu-id="30787-138">Next steps</span></span>
* [<span data-ttu-id="30787-139">下載資產</span><span class="sxs-lookup"><span data-stu-id="30787-139">Download assets</span></span>](media-services-deliver-asset-download.md)
* [<span data-ttu-id="30787-140">設定資產傳遞原則</span><span class="sxs-lookup"><span data-stu-id="30787-140">Configure asset delivery policy</span></span>](media-services-dotnet-configure-asset-delivery-policy.md)

