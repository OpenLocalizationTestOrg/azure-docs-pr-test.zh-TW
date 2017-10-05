---
title: "Azure 媒體服務常見問題集 | Microsoft Docs"
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
ms.openlocfilehash: 48f3924d44a084d61c1d38002cd5098094001acb
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="frequently-asked-questions"></a><span data-ttu-id="3ff09-103">常見問題集</span><span class="sxs-lookup"><span data-stu-id="3ff09-103">Frequently asked questions</span></span>

<span data-ttu-id="3ff09-104">本文解說「Azure 媒體服務」(AMS) 使用者社群所提出的常見問題集。</span><span class="sxs-lookup"><span data-stu-id="3ff09-104">This article addresses frequently asked questions raised by the Azure Media Services (AMS) user community.</span></span>

## <a name="general-ams-faqs"></a><span data-ttu-id="3ff09-105">一般 AMS 常見問題集</span><span class="sxs-lookup"><span data-stu-id="3ff09-105">General AMS FAQs</span></span>
<span data-ttu-id="3ff09-106">問：如何調整索引？</span><span class="sxs-lookup"><span data-stu-id="3ff09-106">Q: How do you scale indexing?</span></span>

<span data-ttu-id="3ff09-107">答：編碼與編製索引工作的保留單位都相同。</span><span class="sxs-lookup"><span data-stu-id="3ff09-107">A: The reserved units are the same for Encoding and Indexing tasks.</span></span> <span data-ttu-id="3ff09-108">請依照 [如何調整編碼保留單位](media-services-scale-media-processing-overview.md)的指示進行。</span><span class="sxs-lookup"><span data-stu-id="3ff09-108">Follow instructions on [How to Scale Encoding Reserved Units](media-services-scale-media-processing-overview.md).</span></span> <span data-ttu-id="3ff09-109">**請注意** ，Indexer 效能不受保留單元類型影響。</span><span class="sxs-lookup"><span data-stu-id="3ff09-109">**Note** that Indexer performance is not affected by Reserved Unit Type.</span></span>

<span data-ttu-id="3ff09-110">問：我已上傳、編碼以及發佈視訊。</span><span class="sxs-lookup"><span data-stu-id="3ff09-110">Q: I uploaded, encoded, and published a video.</span></span> <span data-ttu-id="3ff09-111">當我試著串流處理視頻時，為什麼不會播放視頻？</span><span class="sxs-lookup"><span data-stu-id="3ff09-111">What would be the reason the video does not play when I try to stream it?</span></span>

<span data-ttu-id="3ff09-112">答：其中一個最常見的原因就是您嘗試從中進行播放的串流端點不是處於 [執行中] 狀態。</span><span class="sxs-lookup"><span data-stu-id="3ff09-112">A: One of the most common reasons is you do not have the streaming endpoint from which you are trying to playback in the **Running** state.</span></span>  

<span data-ttu-id="3ff09-113">問：我可以編輯即時資料流？</span><span class="sxs-lookup"><span data-stu-id="3ff09-113">Q: Can I do compositing on a live stream?</span></span>

<span data-ttu-id="3ff09-114">答：Azure 媒體服務目前尚未開放即時資料流的編輯功能，所以請您事先在電腦上編輯。</span><span class="sxs-lookup"><span data-stu-id="3ff09-114">A: Compositing on live streams is currently not offered in Azure Media Services, so you would need to pre-compose on your computer.</span></span>

<span data-ttu-id="3ff09-115">問：Azure CDN 可以搭配即時資料流使用？</span><span class="sxs-lookup"><span data-stu-id="3ff09-115">Q: Can I use Azure CDN with Live Streaming?</span></span>

<span data-ttu-id="3ff09-116">答：媒體服務支援 Azure CDN 整合 (如需詳細資訊，請參閱 [如何在媒體服務帳戶中管理串流端點](media-services-portal-manage-streaming-endpoints.md))。</span><span class="sxs-lookup"><span data-stu-id="3ff09-116">A: Media Services supports integration with Azure CDN (for more information, see [How to Manage Streaming Endpoints in a Media Services Account](media-services-portal-manage-streaming-endpoints.md)).</span></span>  <span data-ttu-id="3ff09-117">即時資料流可以搭配 CDN 使用。</span><span class="sxs-lookup"><span data-stu-id="3ff09-117">You can use Live streaming with CDN.</span></span> <span data-ttu-id="3ff09-118">Azure 媒體服務提供 Smooth Streaming、HLS 和 MPEG-DASH 輸出。</span><span class="sxs-lookup"><span data-stu-id="3ff09-118">Azure Media Services provides Smooth Streaming, HLS and MPEG-DASH outputs.</span></span> <span data-ttu-id="3ff09-119">所有這些格式都使用 HTTP 來傳送資料以及獲得 HTTP 快取的優點。</span><span class="sxs-lookup"><span data-stu-id="3ff09-119">All these formats use HTTP for transferring data and get benefits of HTTP caching.</span></span> <span data-ttu-id="3ff09-120">在即時資料流實際視訊/音訊資料是分割成片段，而且這個獨立片段會快取到 CDN。</span><span class="sxs-lookup"><span data-stu-id="3ff09-120">In live streaming actual video/audio data is divided to fragments and this individual fragments get cached in CDN.</span></span> <span data-ttu-id="3ff09-121">唯一要重新整理的資料是資訊清單資料。</span><span class="sxs-lookup"><span data-stu-id="3ff09-121">Only data needs to be refreshed is the manifest data.</span></span> <span data-ttu-id="3ff09-122">CDN 會定期重新整理資訊清單資料。</span><span class="sxs-lookup"><span data-stu-id="3ff09-122">CDN periodically refreshes manifest data.</span></span>

<span data-ttu-id="3ff09-123">問：Azure 媒體服務支援儲存影像？</span><span class="sxs-lookup"><span data-stu-id="3ff09-123">Q: Does Azure Media services support storing images?</span></span>

<span data-ttu-id="3ff09-124">答：如果您只想要儲存 JPEG 或 PNG 影像，請儲存至 Azure Blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="3ff09-124">A: If you are just looking to store JPEG or PNG images, you should keep those in Azure Blob Storage.</span></span> <span data-ttu-id="3ff09-125">除非您想維持影像與視訊或音訊資產之間的關聯，否則將影像保存在媒體服務帳戶中，實際上一點用處也沒有。</span><span class="sxs-lookup"><span data-stu-id="3ff09-125">There is no benefit to putting them in your Media Services account unless you want to keep them associated with your Video or Audio Assets.</span></span> <span data-ttu-id="3ff09-126">或者，當您需要在視訊編碼器中將影像作為重疊時才有必要。媒體編碼器標準支援在視訊上層重疊影像，因此會將 JPEG 和 PNG 列為支援的輸入格式。</span><span class="sxs-lookup"><span data-stu-id="3ff09-126">Or if you might have a need to use the images as overlays in the video encoder.Media Encoder Standard supports overlaying images on top of videos, and that is what it lists JPEG and PNG as supported input formats.</span></span> <span data-ttu-id="3ff09-127">如需詳細資訊，請參閱 [建立重疊](media-services-advanced-encoding-with-mes.md#overlay)。</span><span class="sxs-lookup"><span data-stu-id="3ff09-127">For more information, see [Creating Overlays](media-services-advanced-encoding-with-mes.md#overlay).</span></span>

<span data-ttu-id="3ff09-128">問：我如何將資產從一個媒體服務帳戶複製到另一個帳戶。</span><span class="sxs-lookup"><span data-stu-id="3ff09-128">Q: How can I copy assets from one Media Services account to another.</span></span>

<span data-ttu-id="3ff09-129">答：若要使用 .NET 將資產從某個媒體服務帳戶複製到另一個帳戶，請使用 [Azure Media Services .NET SDK Extensions](https://github.com/Azure/azure-sdk-for-media-services-extensions/) (Azure 媒體服務 .NET SDK 擴充功能) 儲存機制中可用的 [IAsset.Copy](https://github.com/Azure/azure-sdk-for-media-services-extensions/blob/dev/MediaServices.Client.Extensions/IAssetExtensions.cs#L354) 擴充功能方法。</span><span class="sxs-lookup"><span data-stu-id="3ff09-129">A: To copy assets from one Media Services account to another using .NET, use [IAsset.Copy](https://github.com/Azure/azure-sdk-for-media-services-extensions/blob/dev/MediaServices.Client.Extensions/IAssetExtensions.cs#L354) extension method available in the [Azure Media Services .NET SDK Extensions](https://github.com/Azure/azure-sdk-for-media-services-extensions/) repository.</span></span> <span data-ttu-id="3ff09-130">如需詳細資訊，請參閱 [這個](https://social.msdn.microsoft.com/Forums/azure/28912d5d-6733-41c1-b27d-5d5dff2695ca/migrate-media-services-across-subscription?forum=MediaServices) 論壇執行緒。</span><span class="sxs-lookup"><span data-stu-id="3ff09-130">For more information, see [this](https://social.msdn.microsoft.com/Forums/azure/28912d5d-6733-41c1-b27d-5d5dff2695ca/migrate-media-services-across-subscription?forum=MediaServices) forum thread.</span></span>

<span data-ttu-id="3ff09-131">問：使用 AMS 時，有哪些支援的字元可用來命名檔案？</span><span class="sxs-lookup"><span data-stu-id="3ff09-131">Q: What are the supported characters for naming files when working with AMS?</span></span>

<span data-ttu-id="3ff09-132">答：建置串流內容的 URL (例如，http://{AMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/streamingParameters) 時，媒體服務會使用 IAssetFile.Name 屬性的值。基於這個理由，不允許 percent-encoding。</span><span class="sxs-lookup"><span data-stu-id="3ff09-132">A: Media Services uses the value of the IAssetFile.Name property when building URLs for the streaming content (for example, http://{AMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/streamingParameters.) For this reason, percent-encoding is not allowed.</span></span> <span data-ttu-id="3ff09-133">**Name** 屬性的值不能有下列任何[百分比編碼保留字元](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters)：!*'();:@&=+$,/?%#[]"。</span><span class="sxs-lookup"><span data-stu-id="3ff09-133">The value of the **Name** property cannot have any of the following [percent-encoding-reserved characters](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters): !*'();:@&=+$,/?%#[]".</span></span> <span data-ttu-id="3ff09-134">此外，只能有一個 ‘.’</span><span class="sxs-lookup"><span data-stu-id="3ff09-134">Also, there can only be one ‘.’</span></span> <span data-ttu-id="3ff09-135">在檔案名稱的副檔名。</span><span class="sxs-lookup"><span data-stu-id="3ff09-135">for the file name extension.</span></span>

<span data-ttu-id="3ff09-136">問：如何使用 REST 連線？</span><span class="sxs-lookup"><span data-stu-id="3ff09-136">Q: How to connect using REST?</span></span>

<span data-ttu-id="3ff09-137">答：如需連線至 AMS API 的詳細資訊，請參閱[使用 Azure AD 驗證存取 Azure 媒體服務 API](media-services-use-aad-auth-to-access-ams-api.md)。</span><span class="sxs-lookup"><span data-stu-id="3ff09-137">A: For information on how to connect to the AMS API, see [Access the Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> <span data-ttu-id="3ff09-138">順利連線到 https://media.windows.net 之後，您會收到 301 重新導向，指定另一個媒體服務 URI。</span><span class="sxs-lookup"><span data-stu-id="3ff09-138">After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="3ff09-139">後續的呼叫必須送到新的 URI。</span><span class="sxs-lookup"><span data-stu-id="3ff09-139">You must make subsequent calls to the new URI.</span></span> 

<span data-ttu-id="3ff09-140">問：如何在編碼過程中旋轉影片？</span><span class="sxs-lookup"><span data-stu-id="3ff09-140">Q: How can I rotate a video during the encoding process.</span></span>

<span data-ttu-id="3ff09-141">答：[Media Encoder Standard](media-services-dotnet-encode-with-media-encoder-standard.md) 支援 90/180/270 度的旋轉角度。</span><span class="sxs-lookup"><span data-stu-id="3ff09-141">A: The [Media Encoder Standard](media-services-dotnet-encode-with-media-encoder-standard.md) supports rotation by angles of 90/180/270.</span></span> <span data-ttu-id="3ff09-142">預設行為是「自動」，此時它會嘗試偵測內送之 MP4/MOV 檔案的旋轉中繼資料並加以補償。</span><span class="sxs-lookup"><span data-stu-id="3ff09-142">The default behavior is "Auto", where it tries to detect the rotation metadata in the incoming MP4/MOV file and compensate for it.</span></span> <span data-ttu-id="3ff09-143">包括以下 **Sources** 元素至[這裡](media-services-mes-presets-overview.md)所定義的其中一個 json 預設項目：</span><span class="sxs-lookup"><span data-stu-id="3ff09-143">Include the following **Sources** element to one of the json presets defined [here](media-services-mes-presets-overview.md):</span></span>

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


## <a name="media-services-learning-paths"></a><span data-ttu-id="3ff09-144">媒體服務學習路徑</span><span class="sxs-lookup"><span data-stu-id="3ff09-144">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="3ff09-145">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="3ff09-145">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
