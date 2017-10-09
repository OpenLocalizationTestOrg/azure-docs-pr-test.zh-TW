---
title: "aaaAzure Media Services 動態封裝概觀 |Microsoft 文件"
description: "hello 主題提供和動態封裝的概觀。"
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
ms.openlocfilehash: 970e24eba800e098774172c87f56629430b227a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="dynamic-packaging"></a><span data-ttu-id="425a4-103">動態封裝</span><span class="sxs-lookup"><span data-stu-id="425a4-103">Dynamic packaging</span></span>
## <a name="overview"></a><span data-ttu-id="425a4-104">概觀</span><span class="sxs-lookup"><span data-stu-id="425a4-104">Overview</span></span>
<span data-ttu-id="425a4-105">Microsoft Azure Media Services 可以使用的 toodeliver 許多媒體來源檔案格式、 媒體串流格式和內容保護格式 tooa 各種不同的用戶端技術 (比方說，iOS、 XBOX、 Silverlight、 Windows 8)。</span><span class="sxs-lookup"><span data-stu-id="425a4-105">Microsoft Azure Media Services can be used toodeliver many media source file formats, media streaming formats, and content protection formats tooa variety of client technologies (for example, iOS, XBOX, Silverlight, Windows 8).</span></span> <span data-ttu-id="425a4-106">這些用戶端各自使用不同的通訊協定，例如 iOS 需要 HTTP 即時串流 (HLS) V4 格式，而 Silverlight 與 Xbox 需要 Smooth Streaming。</span><span class="sxs-lookup"><span data-stu-id="425a4-106">These clients understand different protocols, for example iOS requires an HTTP Live Streaming (HLS) V4 format and Silverlight and Xbox require Smooth Streaming.</span></span> <span data-ttu-id="425a4-107">如果您有一組彈性位元速率 （多位元速率） MP4 (ISO Base Media 14496-12) 檔案或一組彈性位元速率 Smooth Streaming 檔案的 MPEG DASH、 HLS 或 Smooth Streaming 的 tooserve tooclients，您應該利用媒體服務動態封裝。</span><span class="sxs-lookup"><span data-stu-id="425a4-107">If you have a set of adaptive bitrate (multi-bitrate) MP4 (ISO Base Media 14496-12) files or a set of adaptive bitrate Smooth Streaming files that you want tooserve tooclients that understand MPEG DASH, HLS or Smooth Streaming, you should take advantage of Media Services dynamic packaging.</span></span>

<span data-ttu-id="425a4-108">您只需要動態封裝是 toocreate 包含一組彈性位元速率 MP4 檔案或彈性位元速率 Smooth Streaming 檔案的資產。</span><span class="sxs-lookup"><span data-stu-id="425a4-108">With dynamic packaging all you need is toocreate an asset that contains a set of adaptive bitrate MP4 files or adaptive bitrate Smooth Streaming files.</span></span> <span data-ttu-id="425a4-109">然後，hello hello 資訊清單中指定的格式為基礎或片段要求中 hello 隨選串流伺服器可確保您已選擇 hello 通訊協定接收 hello 資料流。</span><span class="sxs-lookup"><span data-stu-id="425a4-109">Then, based on hello specified format in hello manifest or fragment request, hello On-Demand Streaming server will ensure that you receive hello stream in hello protocol you have chosen.</span></span> <span data-ttu-id="425a4-110">如此一來，您只需要 toostore 及支付一種儲存格式和 Media Services 服務中的 hello 檔案將會建立及傳遞 hello 適當的回應，根據用戶端的要求。</span><span class="sxs-lookup"><span data-stu-id="425a4-110">As a result, you only need toostore and pay for hello files in single storage format and Media Services service will build and serve hello appropriate response based on requests from a client.</span></span>

<span data-ttu-id="425a4-111">hello 下列圖表顯示 hello 傳統編碼和靜態封裝工作流程。</span><span class="sxs-lookup"><span data-stu-id="425a4-111">hello following diagram shows hello traditional encoding and static packaging workflow.</span></span>

![靜態編碼](./media/media-services-dynamic-packaging-overview/media-services-static-packaging.png)

<span data-ttu-id="425a4-113">hello 下列圖表顯示 hello 動態封裝工作流程。</span><span class="sxs-lookup"><span data-stu-id="425a4-113">hello following diagram shows hello dynamic packaging workflow.</span></span>

![動態編碼](./media/media-services-dynamic-packaging-overview/media-services-dynamic-packaging.png)


## <a name="common-scenario"></a><span data-ttu-id="425a4-115">常見的案例</span><span class="sxs-lookup"><span data-stu-id="425a4-115">Common scenario</span></span>
1. <span data-ttu-id="425a4-116">上傳輸入檔案 (稱為夾層檔)。</span><span class="sxs-lookup"><span data-stu-id="425a4-116">Upload an input file (called a mezzanine file).</span></span> <span data-ttu-id="425a4-117">例如，H.264、 MP4 或 WMV (如 hello 的支援格式清單，請參閱[格式支援的媒體編碼器標準 hello](media-services-media-encoder-standard-formats.md)。</span><span class="sxs-lookup"><span data-stu-id="425a4-117">For example, H.264, MP4, or WMV (for hello list of supported formats see [Formats Supported by hello Media Encoder Standard](media-services-media-encoder-standard-formats.md).</span></span>
2. <span data-ttu-id="425a4-118">編碼夾層檔 tooH.264 MP4 彈性位元速率集。</span><span class="sxs-lookup"><span data-stu-id="425a4-118">Encode your mezzanine file tooH.264 MP4 adaptive bitrate sets.</span></span>
3. <span data-ttu-id="425a4-119">發行包含 hello 自動調整位元速率 MP4 集藉由建立 hello 上隨選 Locator hello 資產。</span><span class="sxs-lookup"><span data-stu-id="425a4-119">Publish hello asset that contains hello adaptive bitrate MP4 set by creating hello On-Demand Locator.</span></span>
4. <span data-ttu-id="425a4-120">建置串流 Url tooaccess hello 和串流處理內容。</span><span class="sxs-lookup"><span data-stu-id="425a4-120">Build hello streaming URLs tooaccess and stream your content.</span></span>

## <a name="preparing-assets-for-dynamic-streaming"></a><span data-ttu-id="425a4-121">準備動態串流的資產</span><span class="sxs-lookup"><span data-stu-id="425a4-121">Preparing assets for dynamic streaming</span></span>
<span data-ttu-id="425a4-122">tooprepare 資產用於動態串流處理您有兩個選項：</span><span class="sxs-lookup"><span data-stu-id="425a4-122">tooprepare your asset for dynamic streaming you have two options:</span></span>

1. <span data-ttu-id="425a4-123">[上傳主檔案](media-services-dotnet-upload-files.md)。</span><span class="sxs-lookup"><span data-stu-id="425a4-123">[Upload a master file](media-services-dotnet-upload-files.md).</span></span>
2. <span data-ttu-id="425a4-124">[使用 hello 媒體編碼器標準編碼器 tooproduce H.264 MP4 彈性位元速率集](media-services-dotnet-encode-with-media-encoder-standard.md)。</span><span class="sxs-lookup"><span data-stu-id="425a4-124">[Use hello Media Encoder Standard encoder tooproduce H.264 MP4 adaptive bitrate sets](media-services-dotnet-encode-with-media-encoder-standard.md).</span></span>
3. <span data-ttu-id="425a4-125">[串流處理內容](media-services-deliver-content-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="425a4-125">[Stream your content](media-services-deliver-content-overview.md).</span></span>

## <span data-ttu-id="425a4-126"><a id="unsupported_formats"></a>動態封裝不支援的格式</span><span class="sxs-lookup"><span data-stu-id="425a4-126"><a id="unsupported_formats"></a>Formats that are not supported by dynamic packaging</span></span>
<span data-ttu-id="425a4-127">hello 下列來源檔案格式不受動態封裝。</span><span class="sxs-lookup"><span data-stu-id="425a4-127">hello following source file formats are not supported by dynamic packaging.</span></span>

* <span data-ttu-id="425a4-128">Dolby digital mp4 檔案。</span><span class="sxs-lookup"><span data-stu-id="425a4-128">Dolby digital mp4 files.</span></span>
* <span data-ttu-id="425a4-129">Dolby digital smooth 檔案。</span><span class="sxs-lookup"><span data-stu-id="425a4-129">Dolby digital smooth files.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="425a4-130">媒體服務學習路徑</span><span class="sxs-lookup"><span data-stu-id="425a4-130">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="425a4-131">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="425a4-131">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

