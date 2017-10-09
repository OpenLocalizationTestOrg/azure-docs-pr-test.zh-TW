---
title: "使用.NET aaaPublish Azure 媒體服務內容 |Microsoft 文件"
description: "深入了解如何 toocreate 是使用的 toobuild 串流 URL 定位器。 程式碼範例會以 C# 所撰寫，並使用 hello Media Services SDK for.NET。"
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
ms.openlocfilehash: c941cd93c252a96e66546cce2793bb426afac059
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="publish-azure-media-services-content-using-net"></a><span data-ttu-id="e31e6-104">使用 .NET 發佈 Azure 媒體服務內容</span><span class="sxs-lookup"><span data-stu-id="e31e6-104">Publish Azure Media Services content using .NET</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e31e6-105">REST</span><span class="sxs-lookup"><span data-stu-id="e31e6-105">REST</span></span>](media-services-rest-deliver-streaming-content.md)
> * [<span data-ttu-id="e31e6-106">.NET</span><span class="sxs-lookup"><span data-stu-id="e31e6-106">.NET</span></span>](media-services-deliver-streaming-content.md)
> * [<span data-ttu-id="e31e6-107">入口網站</span><span class="sxs-lookup"><span data-stu-id="e31e6-107">Portal</span></span>](media-services-portal-publish.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="e31e6-108">Overview</span><span class="sxs-lookup"><span data-stu-id="e31e6-108">Overview</span></span>
<span data-ttu-id="e31e6-109">您可以建立隨選串流定位器及建置串流 URL，串流處理調適性位元速率 MP4 集。</span><span class="sxs-lookup"><span data-stu-id="e31e6-109">You can stream an adaptive bitrate MP4 set by creating an OnDemand streaming locator and building a streaming URL.</span></span> <span data-ttu-id="e31e6-110">hello[編碼資產](media-services-encode-asset.md)主題說明如何設定 tooencode 成彈性位元速率 MP4。</span><span class="sxs-lookup"><span data-stu-id="e31e6-110">hello [encoding an asset](media-services-encode-asset.md) topic shows how tooencode into an adaptive bitrate MP4 set.</span></span> 

> [!NOTE]
> <span data-ttu-id="e31e6-111">如果您的內容已加密，請在建立定位器之前設定資產傳遞原則 (如 [這個](media-services-dotnet-configure-asset-delivery-policy.md) 主題中所述)。</span><span class="sxs-lookup"><span data-stu-id="e31e6-111">If your content is encrypted, configure asset delivery policy (as described in [this](media-services-dotnet-configure-asset-delivery-policy.md) topic) before creating a locator.</span></span> 
> 
> 

<span data-ttu-id="e31e6-112">您也可以使用串流定位器 toobuild Url 可以漸進式下載該點 tooMP4 檔案 OnDemand。</span><span class="sxs-lookup"><span data-stu-id="e31e6-112">You can also use an OnDemand streaming locator toobuild URLs that point tooMP4 files that can be progressively downloaded.</span></span>  

<span data-ttu-id="e31e6-113">本主題說明如何 toocreate OnDemand 定位器 toopublish 資料流處理，您的資產和組建平滑，MPEG DASH 和 HLS 資料流 Url。</span><span class="sxs-lookup"><span data-stu-id="e31e6-113">This topic shows how toocreate an OnDemand streaming locator toopublish your asset and build a Smooth, MPEG DASH, and HLS streaming URLs.</span></span> <span data-ttu-id="e31e6-114">它也會示範熱 toobuild 漸進式下載 Url。</span><span class="sxs-lookup"><span data-stu-id="e31e6-114">It also shows hot toobuild progressive download URLs.</span></span> 

## <a name="create-an-ondemand-streaming-locator"></a><span data-ttu-id="e31e6-115">建立隨選串流定位器</span><span class="sxs-lookup"><span data-stu-id="e31e6-115">Create an OnDemand streaming locator</span></span>
<span data-ttu-id="e31e6-116">toocreate hello OnDemand 串流定位器，並取得 Url，您需要下列項目 toodo hello:</span><span class="sxs-lookup"><span data-stu-id="e31e6-116">toocreate hello OnDemand streaming locator and get URLs, you need toodo hello following things:</span></span>

1. <span data-ttu-id="e31e6-117">如果 hello 內容會經過加密，定義存取原則。</span><span class="sxs-lookup"><span data-stu-id="e31e6-117">If hello content is encrypted, define an access policy.</span></span>
2. <span data-ttu-id="e31e6-118">建立隨選串流定位器。</span><span class="sxs-lookup"><span data-stu-id="e31e6-118">Create an OnDemand streaming locator.</span></span>
3. <span data-ttu-id="e31e6-119">如果您計劃 toostream，取得資料流 hello 資產中的資訊清單檔案 (.ism) 的 hello。</span><span class="sxs-lookup"><span data-stu-id="e31e6-119">If you plan toostream, get hello streaming manifest file (.ism) in hello asset.</span></span> 
   
   <span data-ttu-id="e31e6-120">如果您計劃 tooprogressively 下載，會收到 hello hello 資產中的 MP4 檔案的名稱。</span><span class="sxs-lookup"><span data-stu-id="e31e6-120">If you plan tooprogressively download, get hello names of MP4 files in hello asset.</span></span>  
4. <span data-ttu-id="e31e6-121">建置 Url toohello 資訊清單檔或 MP4 檔案。</span><span class="sxs-lookup"><span data-stu-id="e31e6-121">Build URLs toohello manifest file or MP4 files.</span></span> 


>[!NOTE]
><span data-ttu-id="e31e6-122">對於不同的 AMS 原則 (例如 Locator 原則或 ContentKeyAuthorizationPolicy) 有 1,000,000 個原則的限制。</span><span class="sxs-lookup"><span data-stu-id="e31e6-122">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="e31e6-123">使用 hello 相同原則識別碼，如果您一律使用 hello 相同天 / 存取權限。</span><span class="sxs-lookup"><span data-stu-id="e31e6-123">Use hello same policy ID if you are always using hello same days / access permissions.</span></span> <span data-ttu-id="e31e6-124">例如，原則的定位器供 tooremain 就地很長的時間 （非上載原則）。</span><span class="sxs-lookup"><span data-stu-id="e31e6-124">For example, policies for locators that are intended tooremain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="e31e6-125">如需詳細資訊，請參閱 [這個](media-services-dotnet-manage-entities.md#limit-access-policies) 主題。</span><span class="sxs-lookup"><span data-stu-id="e31e6-125">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

### <a name="use-media-services-net-sdk"></a><span data-ttu-id="e31e6-126">使用 Media Services .NET SDK</span><span class="sxs-lookup"><span data-stu-id="e31e6-126">Use Media Services .NET SDK</span></span>
<span data-ttu-id="e31e6-127">建置串流 URL</span><span class="sxs-lookup"><span data-stu-id="e31e6-127">Build Streaming URLs</span></span> 

    private static void BuildStreamingURLs(IAsset asset)
    {

        // Create a 30-day readonly access policy. 
          // You cannot create a streaming locator using an AccessPolicy that includes write or delete permissions.
        IAccessPolicy policy = _context.AccessPolicies.Create("Streaming policy",
            TimeSpan.FromDays(30),
            AccessPermissions.Read);

        // Create a locator toohello streaming content on an origin. 
        ILocator originLocator = _context.Locators.CreateLocator(LocatorType.OnDemandOrigin, asset,
            policy,
            DateTime.UtcNow.AddMinutes(-5));

        // Display some useful values based on hello locator.
        Console.WriteLine("Streaming asset base path on origin: ");
        Console.WriteLine(originLocator.Path);
        Console.WriteLine();

        // Get a reference toohello streaming manifest file from hello  
        // collection of files in hello asset. 
        var manifestFile = asset.AssetFiles.Where(f => f.Name.ToLower().
                                    EndsWith(".ism")).
                                    FirstOrDefault();

        // Create a full URL toohello manifest file. Use this for playback
        // in streaming media clients. 
        string urlForClientStreaming = originLocator.Path + manifestFile.Name + "/manifest";
        Console.WriteLine("URL toomanifest for client streaming using Smooth Streaming protocol: ");
        Console.WriteLine(urlForClientStreaming);
        Console.WriteLine("URL toomanifest for client streaming using HLS protocol: ");
        Console.WriteLine(urlForClientStreaming + "(format=m3u8-aapl)");
        Console.WriteLine("URL toomanifest for client streaming using MPEG DASH protocol: ");
        Console.WriteLine(urlForClientStreaming + "(format=mpd-time-csf)"); 
        Console.WriteLine();
    }

<span data-ttu-id="e31e6-128">hello 輸出：</span><span class="sxs-lookup"><span data-stu-id="e31e6-128">hello outputs:</span></span>

    URL toomanifest for client streaming using Smooth Streaming protocol:
    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny.ism/manifest
    URL toomanifest for client streaming using HLS protocol:
    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny.ism/manifest(format=m3u8-aapl)
    URL toomanifest for client streaming using MPEG DASH protocol:
    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny.ism/manifest(format=mpd-time-csf)


> [!NOTE]
> <span data-ttu-id="e31e6-129">您也可以透過 SSL 連線串流您的內容。</span><span class="sxs-lookup"><span data-stu-id="e31e6-129">You can also stream your content over an SSL connection.</span></span> <span data-ttu-id="e31e6-130">這個方法 toodo，請確定您串流 Url 開頭 HTTPS。</span><span class="sxs-lookup"><span data-stu-id="e31e6-130">toodo this approach, make sure your streaming URLs start with HTTPS.</span></span> <span data-ttu-id="e31e6-131">目前 AMS 不支援使用 SSL 搭配自訂網域。</span><span class="sxs-lookup"><span data-stu-id="e31e6-131">Currently, AMS doesn’t support SSL with custom domains.</span></span>
> 
> 

<span data-ttu-id="e31e6-132">建置漸進式下載 URL</span><span class="sxs-lookup"><span data-stu-id="e31e6-132">Build progressive download URLs</span></span> 

    private static void BuildProgressiveDownloadURLs(IAsset asset)
    {
        // Create a 30-day readonly access policy. 
        IAccessPolicy policy = _context.AccessPolicies.Create("Streaming policy",
            TimeSpan.FromDays(30),
            AccessPermissions.Read);

        // Create an OnDemandOrigin locator toohello asset. 
        ILocator originLocator = _context.Locators.CreateLocator(LocatorType.OnDemandOrigin, asset,
            policy,
            DateTime.UtcNow.AddMinutes(-5));

        // Display some useful values based on hello locator.
        Console.WriteLine("Streaming asset base path on origin: ");
        Console.WriteLine(originLocator.Path);
        Console.WriteLine();

        // Get MP4 files.
        IEnumerable<IAssetFile> mp4AssetFiles = asset
            .AssetFiles
            .ToList()
            .Where(af => af.Name.EndsWith(".mp4", StringComparison.OrdinalIgnoreCase));

        // Create a full URL toohello MP4 files. Use this tooprogressively download files.
        foreach (var pd in mp4AssetFiles)
            Console.WriteLine(originLocator.Path + pd.Name);
    }

<span data-ttu-id="e31e6-133">hello 輸出：</span><span class="sxs-lookup"><span data-stu-id="e31e6-133">hello outputs:</span></span>

    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny_H264_650kbps_AAC_und_ch2_96kbps.mp4
    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny_H264_400kbps_AAC_und_ch2_96kbps.mp4
    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny_H264_3400kbps_AAC_und_ch2_96kbps.mp4
    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny_H264_2250kbps_AAC_und_ch2_96kbps.mp4

    . . . 

### <a name="use-media-services-net-sdk-extensions"></a><span data-ttu-id="e31e6-134">使用 Media Services .NET SDK 延伸模組</span><span class="sxs-lookup"><span data-stu-id="e31e6-134">Use Media Services .NET SDK Extensions</span></span>
<span data-ttu-id="e31e6-135">hello 下列程式碼呼叫.NET SDK 延伸模組方法建立定位器，並產生彈性資料流的 hello Smooth Streaming、 HLS 及 MPEG-DASH Url。</span><span class="sxs-lookup"><span data-stu-id="e31e6-135">hello following code calls .NET SDK extensions methods that create a locator and generate hello Smooth Streaming, HLS, and MPEG-DASH URLs for adaptive streaming.</span></span>

    // Create a loctor.
    _context.Locators.Create(
        LocatorType.OnDemandOrigin,
        inputAsset,
        AccessPermissions.Read,
        TimeSpan.FromDays(30));

    // Get hello streaming URLs.
    Uri smoothStreamingUri = inputAsset.GetSmoothStreamingUri();
    Uri hlsUri = inputAsset.GetHlsUri();
    Uri mpegDashUri = inputAsset.GetMpegDashUri();

    Console.WriteLine(smoothStreamingUri);
    Console.WriteLine(hlsUri);
    Console.WriteLine(mpegDashUri);


## <a name="media-services-learning-paths"></a><span data-ttu-id="e31e6-136">媒體服務學習路徑</span><span class="sxs-lookup"><span data-stu-id="e31e6-136">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="e31e6-137">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="e31e6-137">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a><span data-ttu-id="e31e6-138">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e31e6-138">Next steps</span></span>
* [<span data-ttu-id="e31e6-139">下載資產</span><span class="sxs-lookup"><span data-stu-id="e31e6-139">Download assets</span></span>](media-services-deliver-asset-download.md)
* [<span data-ttu-id="e31e6-140">設定資產傳遞原則</span><span class="sxs-lookup"><span data-stu-id="e31e6-140">Configure asset delivery policy</span></span>](media-services-dotnet-configure-asset-delivery-policy.md)

