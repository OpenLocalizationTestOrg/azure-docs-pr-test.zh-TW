---
title: "aaaAzure Media Services 常見問題集 |Microsoft 文件"
description: "常見問題集 (FAQ)"
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 5374f7f4-c189-43ef-8b7f-f2f4141e2748
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: juliako
ms.openlocfilehash: 6d48a5c1291f3c2559d8445921d571718d0a0a6d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-questions"></a><span data-ttu-id="e0d96-103">常見問題集</span><span class="sxs-lookup"><span data-stu-id="e0d96-103">Frequently asked questions</span></span>

<span data-ttu-id="e0d96-104">本文中的 hello Azure 媒體服務 (AMS) 中使用者社群所引發的常見問題。</span><span class="sxs-lookup"><span data-stu-id="e0d96-104">This article addresses frequently asked questions raised by hello Azure Media Services (AMS) user community.</span></span>

## <a name="general-ams-faqs"></a><span data-ttu-id="e0d96-105">一般 AMS 常見問題集</span><span class="sxs-lookup"><span data-stu-id="e0d96-105">General AMS FAQs</span></span>
<span data-ttu-id="e0d96-106">問：如何調整索引？</span><span class="sxs-lookup"><span data-stu-id="e0d96-106">Q: How do you scale indexing?</span></span>

<span data-ttu-id="e0d96-107">答： hello 保留單位的編碼方式和索引工作會 hello 相同。</span><span class="sxs-lookup"><span data-stu-id="e0d96-107">A: hello reserved units are hello same for Encoding and Indexing tasks.</span></span> <span data-ttu-id="e0d96-108">依指示[如何 tooScale 編碼保留單元](media-services-scale-media-processing-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="e0d96-108">Follow instructions on [How tooScale Encoding Reserved Units](media-services-scale-media-processing-overview.md).</span></span> <span data-ttu-id="e0d96-109">**請注意** ，Indexer 效能不受保留單元類型影響。</span><span class="sxs-lookup"><span data-stu-id="e0d96-109">**Note** that Indexer performance is not affected by Reserved Unit Type.</span></span>

<span data-ttu-id="e0d96-110">問：我已上傳、編碼以及發佈視訊。</span><span class="sxs-lookup"><span data-stu-id="e0d96-110">Q: I uploaded, encoded, and published a video.</span></span> <span data-ttu-id="e0d96-111">什麼是 hello 原因 hello 視訊不是扮演當我嘗試 toostream 它嗎？</span><span class="sxs-lookup"><span data-stu-id="e0d96-111">What would be hello reason hello video does not play when I try toostream it?</span></span>

<span data-ttu-id="e0d96-112">答： 其中一個最常見的原因是您不需要串流的端點，嘗試在 hello tooplayback hello hello**執行**狀態。</span><span class="sxs-lookup"><span data-stu-id="e0d96-112">A: One of hello most common reasons is you do not have hello streaming endpoint from which you are trying tooplayback in hello **Running** state.</span></span>  

<span data-ttu-id="e0d96-113">問：我可以編輯即時資料流？</span><span class="sxs-lookup"><span data-stu-id="e0d96-113">Q: Can I do compositing on a live stream?</span></span>

<span data-ttu-id="e0d96-114">答： 複合即時資料流上目前不提供在 Azure Media Services 中，因此您必須 toopre-撰寫您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="e0d96-114">A: Compositing on live streams is currently not offered in Azure Media Services, so you would need toopre-compose on your computer.</span></span>

<span data-ttu-id="e0d96-115">問：Azure CDN 可以搭配即時資料流使用？</span><span class="sxs-lookup"><span data-stu-id="e0d96-115">Q: Can I use Azure CDN with Live Streaming?</span></span>

<span data-ttu-id="e0d96-116">答： Media Services 支援與 Azure CDN 整合 (如需詳細資訊，請參閱[如何在 Media Services 帳戶中的 tooManage 資料流端點](media-services-portal-manage-streaming-endpoints.md))。</span><span class="sxs-lookup"><span data-stu-id="e0d96-116">A: Media Services supports integration with Azure CDN (for more information, see [How tooManage Streaming Endpoints in a Media Services Account](media-services-portal-manage-streaming-endpoints.md)).</span></span>  <span data-ttu-id="e0d96-117">即時資料流可以搭配 CDN 使用。</span><span class="sxs-lookup"><span data-stu-id="e0d96-117">You can use Live streaming with CDN.</span></span> <span data-ttu-id="e0d96-118">Azure 媒體服務提供 Smooth Streaming、HLS 和 MPEG-DASH 輸出。</span><span class="sxs-lookup"><span data-stu-id="e0d96-118">Azure Media Services provides Smooth Streaming, HLS and MPEG-DASH outputs.</span></span> <span data-ttu-id="e0d96-119">所有這些格式都使用 HTTP 來傳送資料以及獲得 HTTP 快取的優點。</span><span class="sxs-lookup"><span data-stu-id="e0d96-119">All these formats use HTTP for transferring data and get benefits of HTTP caching.</span></span> <span data-ttu-id="e0d96-120">在即時資料流的實際視訊/音訊資料是分割的 toofragments 和這個個別的片段會被在 CDN 中快取。</span><span class="sxs-lookup"><span data-stu-id="e0d96-120">In live streaming actual video/audio data is divided toofragments and this individual fragments get cached in CDN.</span></span> <span data-ttu-id="e0d96-121">只有資料需求 toobe 重新整理是 hello 資訊清單的資料。</span><span class="sxs-lookup"><span data-stu-id="e0d96-121">Only data needs toobe refreshed is hello manifest data.</span></span> <span data-ttu-id="e0d96-122">CDN 會定期重新整理資訊清單資料。</span><span class="sxs-lookup"><span data-stu-id="e0d96-122">CDN periodically refreshes manifest data.</span></span>

<span data-ttu-id="e0d96-123">問：Azure 媒體服務支援儲存影像？</span><span class="sxs-lookup"><span data-stu-id="e0d96-123">Q: Does Azure Media services support storing images?</span></span>

<span data-ttu-id="e0d96-124">答： 如果您只想 toostore JPEG 或 PNG 影像，您應該將 Azure Blob 儲存體中。</span><span class="sxs-lookup"><span data-stu-id="e0d96-124">A: If you are just looking toostore JPEG or PNG images, you should keep those in Azure Blob Storage.</span></span> <span data-ttu-id="e0d96-125">沒有任何在 Media Services 帳戶除非您想的 tookeep 它們與您的視訊或音訊資產相關聯的權益 tooputting。</span><span class="sxs-lookup"><span data-stu-id="e0d96-125">There is no benefit tooputting them in your Media Services account unless you want tookeep them associated with your Video or Audio Assets.</span></span> <span data-ttu-id="e0d96-126">或如果您為 hello 視訊編碼程式中的覆疊可能需要 toouse hello 映像。媒體編碼器標準支援在視訊頂端的覆疊影像，而這就是什麼它會列出 JPEG 和 PNG 支援輸入格式。</span><span class="sxs-lookup"><span data-stu-id="e0d96-126">Or if you might have a need toouse hello images as overlays in hello video encoder.Media Encoder Standard supports overlaying images on top of videos, and that is what it lists JPEG and PNG as supported input formats.</span></span> <span data-ttu-id="e0d96-127">如需詳細資訊，請參閱 [建立重疊](media-services-advanced-encoding-with-mes.md#overlay)。</span><span class="sxs-lookup"><span data-stu-id="e0d96-127">For more information, see [Creating Overlays](media-services-advanced-encoding-with-mes.md#overlay).</span></span>

<span data-ttu-id="e0d96-128">問： 如何從一個 Media Services 帳戶 tooanother 複製資產。</span><span class="sxs-lookup"><span data-stu-id="e0d96-128">Q: How can I copy assets from one Media Services account tooanother.</span></span>

<span data-ttu-id="e0d96-129">答： toocopy 資產，從一個 Media Services 帳戶 tooanother 使用.NET 中，使用[IAsset.Copy](https://github.com/Azure/azure-sdk-for-media-services-extensions/blob/dev/MediaServices.Client.Extensions/IAssetExtensions.cs#L354) hello 中可用的擴充方法[Azure Media Services.NET SDK Extensions](https://github.com/Azure/azure-sdk-for-media-services-extensions/)儲存機制。</span><span class="sxs-lookup"><span data-stu-id="e0d96-129">A: toocopy assets from one Media Services account tooanother using .NET, use [IAsset.Copy](https://github.com/Azure/azure-sdk-for-media-services-extensions/blob/dev/MediaServices.Client.Extensions/IAssetExtensions.cs#L354) extension method available in hello [Azure Media Services .NET SDK Extensions](https://github.com/Azure/azure-sdk-for-media-services-extensions/) repository.</span></span> <span data-ttu-id="e0d96-130">如需詳細資訊，請參閱 [這個](https://social.msdn.microsoft.com/Forums/azure/28912d5d-6733-41c1-b27d-5d5dff2695ca/migrate-media-services-across-subscription?forum=MediaServices) 論壇執行緒。</span><span class="sxs-lookup"><span data-stu-id="e0d96-130">For more information, see [this](https://social.msdn.microsoft.com/Forums/azure/28912d5d-6733-41c1-b27d-5d5dff2695ca/migrate-media-services-across-subscription?forum=MediaServices) forum thread.</span></span>

<span data-ttu-id="e0d96-131">問： 哪些是 hello 支援字元時使用 AMS 命名的檔案嗎？</span><span class="sxs-lookup"><span data-stu-id="e0d96-131">Q: What are hello supported characters for naming files when working with AMS?</span></span>

<span data-ttu-id="e0d96-132">答： Media Services 使用 hello hello IAssetFile.Name 屬性值，當建置 Url 的 hello 串流處理內容 (例如，http://{AMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/streamingParameters。)基於這個理由，不允許 percent-encoding。</span><span class="sxs-lookup"><span data-stu-id="e0d96-132">A: Media Services uses hello value of hello IAssetFile.Name property when building URLs for hello streaming content (for example, http://{AMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/streamingParameters.) For this reason, percent-encoding is not allowed.</span></span> <span data-ttu-id="e0d96-133">hello hello 值**名稱**屬性不能有 hello 下列任何一項[百分比編碼的保留字元](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters): ！ *' （);: @& = + $，/？ %# []"。</span><span class="sxs-lookup"><span data-stu-id="e0d96-133">hello value of hello **Name** property cannot have any of hello following [percent-encoding-reserved characters](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters): !*'();:@&=+$,/?%#[]".</span></span> <span data-ttu-id="e0d96-134">此外，只能有一個 ‘.’</span><span class="sxs-lookup"><span data-stu-id="e0d96-134">Also, there can only be one ‘.’</span></span> <span data-ttu-id="e0d96-135">hello 檔案名稱副檔名。</span><span class="sxs-lookup"><span data-stu-id="e0d96-135">for hello file name extension.</span></span>

<span data-ttu-id="e0d96-136">問： 如何將 tooconnect 使用嗎？</span><span class="sxs-lookup"><span data-stu-id="e0d96-136">Q: How tooconnect using REST?</span></span>

<span data-ttu-id="e0d96-137">答： 如需如何 tooconnect toohello AMS API，請參閱[存取 hello Azure 媒體服務 API 與 Azure AD 驗證](media-services-use-aad-auth-to-access-ams-api.md)。</span><span class="sxs-lookup"><span data-stu-id="e0d96-137">A: For information on how tooconnect toohello AMS API, see [Access hello Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> <span data-ttu-id="e0d96-138">已成功連接之後 toohttps://media.windows.net，您會收到指定另一個媒體服務 URI 的 301 重新導向。</span><span class="sxs-lookup"><span data-stu-id="e0d96-138">After successfully connecting toohttps://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="e0d96-139">您必須進行的後續呼叫 toohello 新的 URI。</span><span class="sxs-lookup"><span data-stu-id="e0d96-139">You must make subsequent calls toohello new URI.</span></span> 

<span data-ttu-id="e0d96-140">問： 如何在編碼程序的 hello 旋轉視訊。</span><span class="sxs-lookup"><span data-stu-id="e0d96-140">Q: How can I rotate a video during hello encoding process.</span></span>

<span data-ttu-id="e0d96-141">答： hello[媒體編碼器標準](media-services-dotnet-encode-with-media-encoder-standard.md)支援 90/180/270 的旋轉角度。</span><span class="sxs-lookup"><span data-stu-id="e0d96-141">A: hello [Media Encoder Standard](media-services-dotnet-encode-with-media-encoder-standard.md) supports rotation by angles of 90/180/270.</span></span> <span data-ttu-id="e0d96-142">hello 預設行為是 「 自動 」，它會嘗試 toodetect hello 旋轉檔案中繼資料 hello 傳入 MP4/MOV 和補償它。</span><span class="sxs-lookup"><span data-stu-id="e0d96-142">hello default behavior is "Auto", where it tries toodetect hello rotation metadata in hello incoming MP4/MOV file and compensate for it.</span></span> <span data-ttu-id="e0d96-143">Hello 如下**來源**hello json 預設定義的項目 tooone[這裡](media-services-mes-presets-overview.md):</span><span class="sxs-lookup"><span data-stu-id="e0d96-143">Include hello following **Sources** element tooone of hello json presets defined [here](media-services-mes-presets-overview.md):</span></span>

    "Version": 1.0,
    "Sources": [
    {
      "Streams": [],
      "Filters": {
        "Rotation": "90"
      }
    }
    ],
    "Codecs": [

    ...


## <a name="media-services-learning-paths"></a><span data-ttu-id="e0d96-144">媒體服務學習路徑</span><span class="sxs-lookup"><span data-stu-id="e0d96-144">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="e0d96-145">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="e0d96-145">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
