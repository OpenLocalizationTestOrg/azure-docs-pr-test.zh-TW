---
title: "Azure 媒體服務動態封裝概觀 | Microsoft Docs"
description: "本主題提供動態封裝的概觀。"
author: Juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: 0d9e4f54-5daa-45c1-bfaa-cf09ca89b812
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: juliako
ms.openlocfilehash: 2d212599302fced3f60085ab30cdeaefc1ee2e6a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="dynamic-packaging"></a><span data-ttu-id="c5f0d-103">動態封裝</span><span class="sxs-lookup"><span data-stu-id="c5f0d-103">Dynamic packaging</span></span>
## <a name="overview"></a><span data-ttu-id="c5f0d-104">Overview</span><span class="sxs-lookup"><span data-stu-id="c5f0d-104">Overview</span></span>
<span data-ttu-id="c5f0d-105">Microsoft Azure Media Services 可用來針對數種用戶端技術 (例如 iOS、XBOX、Silverlight、Windows 8) 提供許多媒體來源檔案格式、媒體串流格式和內容保護格式。</span><span class="sxs-lookup"><span data-stu-id="c5f0d-105">Microsoft Azure Media Services can be used to deliver many media source file formats, media streaming formats, and content protection formats to a variety of client technologies (for example, iOS, XBOX, Silverlight, Windows 8).</span></span> <span data-ttu-id="c5f0d-106">這些用戶端各自使用不同的通訊協定，例如 iOS 需要 HTTP 即時串流 (HLS) V4 格式，而 Silverlight 與 Xbox 需要 Smooth Streaming。</span><span class="sxs-lookup"><span data-stu-id="c5f0d-106">These clients understand different protocols, for example iOS requires an HTTP Live Streaming (HLS) V4 format and Silverlight and Xbox require Smooth Streaming.</span></span> <span data-ttu-id="c5f0d-107">如果您有一組自動調整位元速率 (多位元速率) MP4 (ISO Base Media 14496-12) 檔案或一組自動調整位元速率 Smooth Streaming 檔案，想要傳遞給了解 MPEG DASH、HLS 或 Smooth Streaming 的用戶端，應該利用媒體服務動態封裝。</span><span class="sxs-lookup"><span data-stu-id="c5f0d-107">If you have a set of adaptive bitrate (multi-bitrate) MP4 (ISO Base Media 14496-12) files or a set of adaptive bitrate Smooth Streaming files that you want to serve to clients that understand MPEG DASH, HLS or Smooth Streaming, you should take advantage of Media Services dynamic packaging.</span></span>

<span data-ttu-id="c5f0d-108">使用動態封裝，您只需要建立包含一組自動調整位元速率 MP4 檔案或自動調整位元速率 Smooth Streaming 檔案的資產。</span><span class="sxs-lookup"><span data-stu-id="c5f0d-108">With dynamic packaging all you need is to create an asset that contains a set of adaptive bitrate MP4 files or adaptive bitrate Smooth Streaming files.</span></span> <span data-ttu-id="c5f0d-109">然後隨選串流伺服器會根據資訊清單或片段要求中的指定格式，確保您以自己選擇的通訊協定接收串流。</span><span class="sxs-lookup"><span data-stu-id="c5f0d-109">Then, based on the specified format in the manifest or fragment request, the On-Demand Streaming server will ensure that you receive the stream in the protocol you have chosen.</span></span> <span data-ttu-id="c5f0d-110">因此，您只需要儲存及支付一種儲存格式之檔案的費用，媒體服務會根據用戶端的要求建置及提供適當的回應。</span><span class="sxs-lookup"><span data-stu-id="c5f0d-110">As a result, you only need to store and pay for the files in single storage format and Media Services service will build and serve the appropriate response based on requests from a client.</span></span>

<span data-ttu-id="c5f0d-111">下圖顯示傳統編碼和靜態封裝工作流程。</span><span class="sxs-lookup"><span data-stu-id="c5f0d-111">The following diagram shows the traditional encoding and static packaging workflow.</span></span>

![靜態編碼](./media/media-services-dynamic-packaging-overview/media-services-static-packaging.png)

<span data-ttu-id="c5f0d-113">下圖顯示動態封裝工作流程。</span><span class="sxs-lookup"><span data-stu-id="c5f0d-113">The following diagram shows the dynamic packaging workflow.</span></span>

![動態編碼](./media/media-services-dynamic-packaging-overview/media-services-dynamic-packaging.png)


## <a name="common-scenario"></a><span data-ttu-id="c5f0d-115">常見的案例</span><span class="sxs-lookup"><span data-stu-id="c5f0d-115">Common scenario</span></span>
1. <span data-ttu-id="c5f0d-116">上傳輸入檔案 (稱為夾層檔)。</span><span class="sxs-lookup"><span data-stu-id="c5f0d-116">Upload an input file (called a mezzanine file).</span></span> <span data-ttu-id="c5f0d-117">例如，H.264、MP4 或 WMV (如需支援格式清單，請參閱 [媒體編碼器標準所支援的格式](media-services-media-encoder-standard-formats.md))。</span><span class="sxs-lookup"><span data-stu-id="c5f0d-117">For example, H.264, MP4, or WMV (for the list of supported formats see [Formats Supported by the Media Encoder Standard](media-services-media-encoder-standard-formats.md).</span></span>
2. <span data-ttu-id="c5f0d-118">將夾層檔編碼為 H.264 MP4 自動調整位元速率集。</span><span class="sxs-lookup"><span data-stu-id="c5f0d-118">Encode your mezzanine file to H.264 MP4 adaptive bitrate sets.</span></span>
3. <span data-ttu-id="c5f0d-119">藉由建立隨選定位器，發行包含自動調整位元速率 MP4 集的資產。</span><span class="sxs-lookup"><span data-stu-id="c5f0d-119">Publish the asset that contains the adaptive bitrate MP4 set by creating the On-Demand Locator.</span></span>
4. <span data-ttu-id="c5f0d-120">建置串流 URL 來存取和串流您的內容。</span><span class="sxs-lookup"><span data-stu-id="c5f0d-120">Build the streaming URLs to access and stream your content.</span></span>

## <a name="preparing-assets-for-dynamic-streaming"></a><span data-ttu-id="c5f0d-121">準備動態串流的資產</span><span class="sxs-lookup"><span data-stu-id="c5f0d-121">Preparing assets for dynamic streaming</span></span>
<span data-ttu-id="c5f0d-122">若要準備動態串流的資產，您有兩個選項：</span><span class="sxs-lookup"><span data-stu-id="c5f0d-122">To prepare your asset for dynamic streaming you have two options:</span></span>

1. <span data-ttu-id="c5f0d-123">[上傳主檔案](media-services-dotnet-upload-files.md)。</span><span class="sxs-lookup"><span data-stu-id="c5f0d-123">[Upload a master file](media-services-dotnet-upload-files.md).</span></span>
2. <span data-ttu-id="c5f0d-124">[使用媒體編碼器標準編碼器產生 H.264 MP4 自動調整位元速率集](media-services-dotnet-encode-with-media-encoder-standard.md)。</span><span class="sxs-lookup"><span data-stu-id="c5f0d-124">[Use the Media Encoder Standard encoder to produce H.264 MP4 adaptive bitrate sets](media-services-dotnet-encode-with-media-encoder-standard.md).</span></span>
3. <span data-ttu-id="c5f0d-125">[串流處理內容](media-services-deliver-content-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="c5f0d-125">[Stream your content](media-services-deliver-content-overview.md).</span></span>

## <span data-ttu-id="c5f0d-126"><a id="unsupported_formats"></a>動態封裝不支援的格式</span><span class="sxs-lookup"><span data-stu-id="c5f0d-126"><a id="unsupported_formats"></a>Formats that are not supported by dynamic packaging</span></span>
<span data-ttu-id="c5f0d-127">動態封裝不支援下列來源檔案格式。</span><span class="sxs-lookup"><span data-stu-id="c5f0d-127">The following source file formats are not supported by dynamic packaging.</span></span>

* <span data-ttu-id="c5f0d-128">Dolby digital mp4 檔案。</span><span class="sxs-lookup"><span data-stu-id="c5f0d-128">Dolby digital mp4 files.</span></span>
* <span data-ttu-id="c5f0d-129">Dolby digital smooth 檔案。</span><span class="sxs-lookup"><span data-stu-id="c5f0d-129">Dolby digital smooth files.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="c5f0d-130">媒體服務學習路徑</span><span class="sxs-lookup"><span data-stu-id="c5f0d-130">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="c5f0d-131">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="c5f0d-131">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

