---
title: "Azure Media Services aaaMicrosoft 案例和跨資料中心的功能可用性 |Microsoft 文件"
description: "本主題概述跨資料中心的 Microsoft Azure 媒體服務功能和服務情節和可用性。"
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/10/2017
ms.author: juliako;anilmur
ms.openlocfilehash: 3dbab6998ed5da738baf8f1e2fb096dfba336e19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="scenarios-and-availability-of-media-services-features-across-datacenters"></a><span data-ttu-id="75683-103">跨資料中心的媒體服務功能情節和可用性</span><span class="sxs-lookup"><span data-stu-id="75683-103">Scenarios and availability of Media Services features across datacenters</span></span>

<span data-ttu-id="75683-104">Microsoft Azure 媒體服務 (AMS) 可讓您 toosecurely 上傳、 儲存、 編碼，和封裝視訊或音訊內容的隨選及即時串流傳遞 toovarious 用戶端 （例如，電視、 PC 和行動裝置）。</span><span class="sxs-lookup"><span data-stu-id="75683-104">Microsoft Azure Media Services (AMS) enables you toosecurely upload, store, encode, and package video or audio content for both on-demand and live streaming delivery toovarious clients (for example, TV, PC, and mobile devices).</span></span>

<span data-ttu-id="75683-105">AMS hello 世界各地的多個資料中心運作。</span><span class="sxs-lookup"><span data-stu-id="75683-105">AMS operates in multiple data centers around hello world.</span></span> <span data-ttu-id="75683-106">這些資料中心會分組在 toogeographic 區域，讓您彈性選擇 where toobuild 應用程式。</span><span class="sxs-lookup"><span data-stu-id="75683-106">These data centers are grouped in toogeographic regions, giving you flexibility in choosing where toobuild your applications.</span></span> <span data-ttu-id="75683-107">您可以檢閱 hello[地區的清單以及其位置](https://azure.microsoft.com/regions/)。</span><span class="sxs-lookup"><span data-stu-id="75683-107">You can review hello [list of regions and their locations](https://azure.microsoft.com/regions/).</span></span> 

<span data-ttu-id="75683-108">本主題說明[即時](#live_scenarios)傳遞內容或[隨選](#vod_scenarios)傳遞內容的常見情節。</span><span class="sxs-lookup"><span data-stu-id="75683-108">This topic shows common scenarios for delivering your content [live](#live_scenarios) or [on-demand](#vod_scenarios).</span></span> <span data-ttu-id="75683-109">hello 主題也會提供跨資料中心的媒體功能和服務的可用性相關的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="75683-109">hello topic also provides details about availability of media features and services across data centers.</span></span>

## <a name="overview"></a><span data-ttu-id="75683-110">概觀</span><span class="sxs-lookup"><span data-stu-id="75683-110">Overview</span></span>

### <a name="prerequisites"></a><span data-ttu-id="75683-111">必要條件</span><span class="sxs-lookup"><span data-stu-id="75683-111">Prerequisites</span></span>

<span data-ttu-id="75683-112">toostart 使用 Azure Media Services 中，您應該有下列 hello:</span><span class="sxs-lookup"><span data-stu-id="75683-112">toostart using Azure Media Services, you should have hello following:</span></span>

* <span data-ttu-id="75683-113">一個 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="75683-113">An Azure account.</span></span> <span data-ttu-id="75683-114">如果您沒有帳戶，只需要幾分鐘的時間就可以建立免費試用帳戶。</span><span class="sxs-lookup"><span data-stu-id="75683-114">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="75683-115">如需詳細資訊，請參閱 [Azure 免費試用](https://azure.microsoft.com)。</span><span class="sxs-lookup"><span data-stu-id="75683-115">For details, see [Azure Free Trial](https://azure.microsoft.com).</span></span>
* <span data-ttu-id="75683-116">Azure 媒體服務帳戶。</span><span class="sxs-lookup"><span data-stu-id="75683-116">An Azure Media Services account.</span></span> <span data-ttu-id="75683-117">如需詳細資訊，請參閱[建立帳戶](media-services-portal-create-account.md)。</span><span class="sxs-lookup"><span data-stu-id="75683-117">For more information, see [Create Account](media-services-portal-create-account.md).</span></span>
* <span data-ttu-id="75683-118">hello 串流的端點要從中 toostream 內容已經在 hello toobe**執行**狀態。</span><span class="sxs-lookup"><span data-stu-id="75683-118">hello streaming endpoint from which you want toostream content has toobe in hello **Running** state.</span></span>

    <span data-ttu-id="75683-119">建立 AMS 帳戶時，**預設**串流端點就會加入 tooyour 帳戶 hello**已停止**狀態。</span><span class="sxs-lookup"><span data-stu-id="75683-119">When your AMS account is created, a **default** streaming endpoint is added tooyour account in hello **Stopped** state.</span></span> <span data-ttu-id="75683-120">串流處理您的內容，並採取利用動態封裝和動態加密，串流端點的 hello toostart hello 中有 toobe**執行**狀態。</span><span class="sxs-lookup"><span data-stu-id="75683-120">toostart streaming your content and take advantage of dynamic packaging and dynamic encryption, hello streaming endpoint has toobe in hello **Running** state.</span></span>

### <a name="commonly-used-objects-when-developing-against-hello-ams-odata-model"></a><span data-ttu-id="75683-121">通常用於針對 hello AMS OData 模型開發的物件</span><span class="sxs-lookup"><span data-stu-id="75683-121">Commonly used objects when developing against hello AMS OData model</span></span>

<span data-ttu-id="75683-122">hello 下圖顯示一些最常用的 hello 物件對 hello 媒體服務 OData 模型進行開發時。</span><span class="sxs-lookup"><span data-stu-id="75683-122">hello following image shows some of hello most commonly used objects when developing against hello Media Services OData model.</span></span>

<span data-ttu-id="75683-123">按一下 hello 映像 tooview 它的完整大小。</span><span class="sxs-lookup"><span data-stu-id="75683-123">Click hello image tooview it full size.</span></span>  

<a href="./media/media-services-overview/media-services-overview-object-model.png" target="_blank"><img src="./media/media-services-overview/media-services-overview-object-model-small.png"></a> 

<span data-ttu-id="75683-124">您可以檢視整個模型的 hello[這裡](https://media.windows.net/API/$metadata?api-version=2.15)。</span><span class="sxs-lookup"><span data-stu-id="75683-124">You can view hello whole model [here](https://media.windows.net/API/$metadata?api-version=2.15).</span></span>  

## <a name="protect-content-in-storage-and-deliver-streaming-media-in-hello-clear-non-encrypted"></a><span data-ttu-id="75683-125">保護儲存體中的內容，並在 hello 傳遞串流處理媒體清除 （未加密）</span><span class="sxs-lookup"><span data-stu-id="75683-125">Protect content in storage and deliver streaming media in hello clear (non-encrypted)</span></span>

![VoD 工作流程](./media/scenarios-and-availability/scenarios-and-availability01.png)

1. <span data-ttu-id="75683-127">將高品質媒體檔上傳到資產。</span><span class="sxs-lookup"><span data-stu-id="75683-127">Upload a high-quality media file into an asset.</span></span>

    <span data-ttu-id="75683-128">建議 tooapply 儲存體加密選項 tooyour 資產中您的內容期間上傳和儲存體中的待用時的順序 tooprotect。</span><span class="sxs-lookup"><span data-stu-id="75683-128">It is recommended tooapply storage encryption option tooyour asset in order tooprotect your content during upload and while at rest in storage.</span></span>
2. <span data-ttu-id="75683-129">編碼 tooa 組彈性位元速率 MP4 檔案。</span><span class="sxs-lookup"><span data-stu-id="75683-129">Encode tooa set of adaptive bitrate MP4 files.</span></span>

    <span data-ttu-id="75683-130">建議 tooapply 儲存體加密選項 toohello 輸出資產順序 tooprotect 中的儲存的內容。</span><span class="sxs-lookup"><span data-stu-id="75683-130">It is recommended tooapply storage encryption option toohello output asset in order tooprotect your content at rest.</span></span>
3. <span data-ttu-id="75683-131">設定資產傳遞原則 (用於動態封裝)。</span><span class="sxs-lookup"><span data-stu-id="75683-131">Configure asset delivery policy (used by dynamic packaging).</span></span>

    <span data-ttu-id="75683-132">如果您的資產是已加密的儲存體， **必須** 設定資產傳遞原則。</span><span class="sxs-lookup"><span data-stu-id="75683-132">If your asset is storage encrypted, you **must** configure asset delivery policy.</span></span>
4. <span data-ttu-id="75683-133">發佈 hello 資產建立 OnDemand 定位器。</span><span class="sxs-lookup"><span data-stu-id="75683-133">Publish hello asset by creating an OnDemand locator.</span></span>
5. <span data-ttu-id="75683-134">串流發佈的內容。</span><span class="sxs-lookup"><span data-stu-id="75683-134">Stream published content.</span></span>

<span data-ttu-id="75683-135">如需在資料中心內的可用性資訊，請參閱 hello[可用性](#availability)> 一節。</span><span class="sxs-lookup"><span data-stu-id="75683-135">For information about availability in datacenters, see hello [Availability](#availability) section.</span></span>

## <a name="protect-content-in-storage-deliver-dynamically-encrypted-streaming-media"></a><span data-ttu-id="75683-136">保護儲存體中的內容、提供動態加密串流處理媒體</span><span class="sxs-lookup"><span data-stu-id="75683-136">Protect content in storage, deliver dynamically encrypted streaming media</span></span>

![利用 PlayReady 保護](./media/media-services-content-protection-overview/media-services-content-protection-with-multi-drm.png)

1. <span data-ttu-id="75683-138">將高品質媒體檔上傳到資產。</span><span class="sxs-lookup"><span data-stu-id="75683-138">Upload a high-quality media file into an asset.</span></span> <span data-ttu-id="75683-139">適用於儲存體加密選項 toohello 資產。</span><span class="sxs-lookup"><span data-stu-id="75683-139">Apply storage encryption option toohello asset.</span></span>
2. <span data-ttu-id="75683-140">編碼 tooa 組彈性位元速率 MP4 檔案。</span><span class="sxs-lookup"><span data-stu-id="75683-140">Encode tooa set of adaptive bitrate MP4 files.</span></span> <span data-ttu-id="75683-141">適用於儲存體加密選項 toohello 輸出資產。</span><span class="sxs-lookup"><span data-stu-id="75683-141">Apply storage encryption option toohello output asset.</span></span>
3. <span data-ttu-id="75683-142">建立您想要在播放期間動態加密 toobe hello 資產的加密內容金鑰。</span><span class="sxs-lookup"><span data-stu-id="75683-142">Create encryption content key for hello asset you want toobe dynamically encrypted during playback.</span></span>
4. <span data-ttu-id="75683-143">設定內容金鑰授權原則。</span><span class="sxs-lookup"><span data-stu-id="75683-143">Configure content key authorization policy.</span></span>
5. <span data-ttu-id="75683-144">設定資產傳遞原則 (供動態封裝和動態加密使用)。</span><span class="sxs-lookup"><span data-stu-id="75683-144">Configure asset delivery policy (used by dynamic packaging and dynamic encryption).</span></span>
6. <span data-ttu-id="75683-145">發佈 hello 資產建立 OnDemand 定位器。</span><span class="sxs-lookup"><span data-stu-id="75683-145">Publish hello asset by creating an OnDemand locator.</span></span>
7. <span data-ttu-id="75683-146">串流發佈的內容。</span><span class="sxs-lookup"><span data-stu-id="75683-146">Stream published content.</span></span>

<span data-ttu-id="75683-147">如需在資料中心內的可用性資訊，請參閱 hello[可用性](#availability)> 一節。</span><span class="sxs-lookup"><span data-stu-id="75683-147">For information about availability in datacenters, see hello [Availability](#availability) section.</span></span>

## <a name="use-media-analytics-tooderive-actionable-insights-from-your-videos"></a><span data-ttu-id="75683-148">使用媒體分析 tooderive 可付諸行動 insights 從您的視訊</span><span class="sxs-lookup"><span data-stu-id="75683-148">Use Media Analytics tooderive actionable insights from your videos</span></span>

<span data-ttu-id="75683-149">媒體分析是語音和願景的元件，可讓它更容易組織和企業 tooderive 可執行的洞察力的視訊檔案的集合。</span><span class="sxs-lookup"><span data-stu-id="75683-149">Media Analytics is a collection of speech and vision components that make it easier for organizations and enterprises tooderive actionable insights from their video files.</span></span> <span data-ttu-id="75683-150">如需詳細資訊，請參閱 [Azure 媒體服務分析概觀](media-services-analytics-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="75683-150">For more information, see [Azure Media Services Analytics Overview](media-services-analytics-overview.md).</span></span>

1. <span data-ttu-id="75683-151">將高品質媒體檔上傳到資產。</span><span class="sxs-lookup"><span data-stu-id="75683-151">Upload a high-quality media file into an asset.</span></span>
2. <span data-ttu-id="75683-152">處理您的視訊與 hello 媒體 Analytics services hello 中所述的其中一個[媒體分析概觀](media-services-analytics-overview.md)> 一節。</span><span class="sxs-lookup"><span data-stu-id="75683-152">Process your videos with one of hello Media Analytics services described in hello [Media Analytics overview](media-services-analytics-overview.md) section.</span></span>
3. <span data-ttu-id="75683-153">媒體分析的媒體處理器會產生 MP4 檔案或 JSON 檔案。</span><span class="sxs-lookup"><span data-stu-id="75683-153">Media Analytics media processors produce MP4 files or JSON files.</span></span> <span data-ttu-id="75683-154">如果媒體處理器所產生的 MP4 檔案，您可以漸進式下載 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="75683-154">If a media processor produced an MP4 file, you can progressively download hello file.</span></span> <span data-ttu-id="75683-155">如果媒體處理器所產生的 JSON 檔案，您可以從 hello Azure blob 儲存體下載 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="75683-155">If a media processor produced a JSON file, you can download hello file from hello Azure blob storage.</span></span>

<span data-ttu-id="75683-156">如需在資料中心內的可用性資訊，請參閱 hello[可用性](#availability)> 一節。</span><span class="sxs-lookup"><span data-stu-id="75683-156">For information about availability in datacenters, see hello [Availability](#availability) section.</span></span>

## <a name="deliver-progressive-download"></a><span data-ttu-id="75683-157">提供漸進式下載</span><span class="sxs-lookup"><span data-stu-id="75683-157">Deliver progressive download</span></span>

1. <span data-ttu-id="75683-158">將高品質媒體檔上傳到資產。</span><span class="sxs-lookup"><span data-stu-id="75683-158">Upload a high-quality media file into an asset.</span></span>
2. <span data-ttu-id="75683-159">Tooa 單一 MP4 檔案編碼。</span><span class="sxs-lookup"><span data-stu-id="75683-159">Encode tooa single MP4 file.</span></span>
3. <span data-ttu-id="75683-160">發行 hello 資產建立 OnDemand 或 SAS 定位器。</span><span class="sxs-lookup"><span data-stu-id="75683-160">Publish hello asset by creating an OnDemand or SAS locator.</span></span>

    <span data-ttu-id="75683-161">如果使用 SAS 定位器，hello 內容從 hello Azure blob 儲存體下載。</span><span class="sxs-lookup"><span data-stu-id="75683-161">If using SAS locator, hello content is downloaded from hello Azure blob storage.</span></span> <span data-ttu-id="75683-162">在此情況下，您不需要 toohave 串流端點處於啟動狀態。</span><span class="sxs-lookup"><span data-stu-id="75683-162">In this case, you do not need toohave streaming endpoints in started state.</span></span>
4. <span data-ttu-id="75683-163">漸進式下載內容。</span><span class="sxs-lookup"><span data-stu-id="75683-163">Progressively download content.</span></span>

## <span data-ttu-id="75683-164"><a id="live_scenarios"></a>傳遞即時串流事件</span><span class="sxs-lookup"><span data-stu-id="75683-164"><a id="live_scenarios"></a>Delivering live-streaming events</span></span> 

1. <span data-ttu-id="75683-165">使用各種即時串流通訊協定 (例如 RTMP 或 Smooth Streaming) 擷取即時內容。</span><span class="sxs-lookup"><span data-stu-id="75683-165">Ingest live content using various live streaming protocols (for example RTMP or Smooth Streaming).</span></span>
2. <span data-ttu-id="75683-166">(選擇性) 將您的串流編碼成調適性位元速率串流。</span><span class="sxs-lookup"><span data-stu-id="75683-166">(optionally) Encode your stream into adaptive bitrate stream.</span></span>
3. <span data-ttu-id="75683-167">預覽您的即時串流。</span><span class="sxs-lookup"><span data-stu-id="75683-167">Preview your live stream.</span></span>
4. <span data-ttu-id="75683-168">傳送嗨內容透過一般串流通訊協定 （例如，MPEG DASH、 Smooth、 HLS） 直接 tooyour 客戶或 tooa 內容傳遞網路 (CDN) 進行進一步的發佈。</span><span class="sxs-lookup"><span data-stu-id="75683-168">Deliver hello content through common streaming protocols (for example, MPEG DASH, Smooth, HLS) directly tooyour customers, or tooa Content Delivery Network (CDN) for further distribution.</span></span>

    <span data-ttu-id="75683-169">-或-</span><span class="sxs-lookup"><span data-stu-id="75683-169">-or-</span></span>

    <span data-ttu-id="75683-170">順序 toobe 中的記錄] 和 [存放區 hello 內嵌的內容資料流處理的更新版本 (Video-on-Demand)。</span><span class="sxs-lookup"><span data-stu-id="75683-170">Record and store hello ingested content in order toobe streamed later (Video-on-Demand).</span></span>

<span data-ttu-id="75683-171">在執行即時資料流時，您可以選擇 hello 下列其中一種會路由傳送：</span><span class="sxs-lookup"><span data-stu-id="75683-171">When doing live streaming, you can choose one of hello following routes:</span></span>

### <a name="working-with-channels-that-receive-multi-bitrate-live-stream-from-on-premises-encoders-pass-through"></a><span data-ttu-id="75683-172">使用可從內部部署編碼器接收多位元速率即時串流的通道 (即時通行)</span><span class="sxs-lookup"><span data-stu-id="75683-172">Working with channels that receive multi-bitrate live stream from on-premises encoders (pass-through)</span></span>

<span data-ttu-id="75683-173">hello 下列圖表顯示 hello 涉及 hello AMS 平台的主要組件以 hello**傳遞**工作流程。</span><span class="sxs-lookup"><span data-stu-id="75683-173">hello following diagram shows hello major parts of hello AMS platform that are involved in hello **pass-through** workflow.</span></span>

![即時工作流程](./media/scenarios-and-availability/media-services-live-streaming-current.png)

<span data-ttu-id="75683-175">如需詳細資訊，請參閱 [使用通道，從內部部署編碼器接收多位元速率即時串流](media-services-live-streaming-with-onprem-encoders.md)。</span><span class="sxs-lookup"><span data-stu-id="75683-175">For more information, see [Working with Channels that Receive Multi-bitrate Live Stream from On-premises Encoders](media-services-live-streaming-with-onprem-encoders.md).</span></span>

### <a name="working-with-channels-that-are-enabled-tooperform-live-encoding-with-azure-media-services"></a><span data-ttu-id="75683-176">使用通道啟用 tooperform 即時使用 Azure 媒體服務編碼</span><span class="sxs-lookup"><span data-stu-id="75683-176">Working with channels that are enabled tooperform live encoding with Azure Media Services</span></span>

<span data-ttu-id="75683-177">hello 下列圖表顯示 hello 主要一部分 hello AMS 平台的即時串流工作流程中所涉及其中通道是啟用 tooperform 即時使用媒體服務編碼。</span><span class="sxs-lookup"><span data-stu-id="75683-177">hello following diagram shows hello major parts of hello AMS platform that are involved in Live Streaming workflow where a Channel is enabled tooperform live encoding with Media Services.</span></span>

![即時工作流程](./media/scenarios-and-availability/media-services-live-streaming-new.png)

<span data-ttu-id="75683-179">如需詳細資訊，請參閱[使用通道，會啟用 tooPerform Live 使用 Azure 媒體服務編碼](media-services-manage-live-encoder-enabled-channels.md)。</span><span class="sxs-lookup"><span data-stu-id="75683-179">For more information, see [Working with Channels that are Enabled tooPerform Live Encoding with Azure Media Services](media-services-manage-live-encoder-enabled-channels.md).</span></span>

<span data-ttu-id="75683-180">如需在資料中心內的可用性資訊，請參閱 hello[可用性](#availability)> 一節。</span><span class="sxs-lookup"><span data-stu-id="75683-180">For information about availability in datacenters, see hello [Availability](#availability) section.</span></span>

## <a name="consuming-content"></a><span data-ttu-id="75683-181">使用內容</span><span class="sxs-lookup"><span data-stu-id="75683-181">Consuming content</span></span>

<span data-ttu-id="75683-182">Azure Media Services 提供 hello 工具，您需要 toocreate 豐富、 動態的用戶端播放器應用程式，用於大部分平台，包括： iOS 裝置、 Android 裝置、 Windows、 Windows Phone、 Xbox 和機上方塊。</span><span class="sxs-lookup"><span data-stu-id="75683-182">Azure Media Services provides hello tools you need toocreate rich, dynamic client player applications for most platforms including: iOS Devices, Android Devices, Windows, Windows Phone, Xbox, and Set-top boxes.</span></span> <span data-ttu-id="75683-183">下列主題中的 hello 提供連結 tooSDKs 和播放器架構，您可以使用 toodevelop 自己的用戶端應用程式可以取用從媒體服務串流媒體。</span><span class="sxs-lookup"><span data-stu-id="75683-183">hello following topic provides links tooSDKs and Player Frameworks that you can use toodevelop your own client applications that can consume streaming media from Media Services.</span></span> <span data-ttu-id="75683-184">如需詳細資訊，請參閱[開發視訊付款人應用程式](media-services-develop-video-players.md)。</span><span class="sxs-lookup"><span data-stu-id="75683-184">For more information, see [Developing video payer applications](media-services-develop-video-players.md)</span></span>

## <a name="enabling-azure-cdn"></a><span data-ttu-id="75683-185">啟用 Azure CDN</span><span class="sxs-lookup"><span data-stu-id="75683-185">Enabling Azure CDN</span></span>

<span data-ttu-id="75683-186">媒體服務支援與 Azure CDN 整合。</span><span class="sxs-lookup"><span data-stu-id="75683-186">Media Services supports integration with Azure CDN.</span></span> <span data-ttu-id="75683-187">如需詳細資訊 tooenable Azure CDN，請參閱[如何在 Media Services 帳戶中的 tooManage 資料流端點](media-services-portal-manage-streaming-endpoints.md)。</span><span class="sxs-lookup"><span data-stu-id="75683-187">For information on how tooenable Azure CDN, see [How tooManage Streaming Endpoints in a Media Services Account](media-services-portal-manage-streaming-endpoints.md).</span></span>

## <span data-ttu-id="75683-188"><a id="scaling"></a>調整媒體服務帳戶</span><span class="sxs-lookup"><span data-stu-id="75683-188"><a id="scaling"></a>Scaling a Media Services account</span></span>

<span data-ttu-id="75683-189">AMS 客戶可以使用其 AMS 帳戶來調整串流端點、媒體處理和儲存體。</span><span class="sxs-lookup"><span data-stu-id="75683-189">AMS customers can scale streaming endpoints, media processing, and storage in their AMS accounts.</span></span>

* <span data-ttu-id="75683-190">媒體服務客戶可以選擇一個**標準**串流端點或一個**進階**串流端點。</span><span class="sxs-lookup"><span data-stu-id="75683-190">Media Services customers can choose either a **Standard** streaming endpoint or a **Premium** streaming endpoint.</span></span> <span data-ttu-id="75683-191">大多數的串流工作負載都適合使用**標準**串流端點。</span><span class="sxs-lookup"><span data-stu-id="75683-191">A **Standard** streaming endpoint is suitable for most streaming workloads.</span></span> <span data-ttu-id="75683-192">它包含相同功能與 hello **Premium**自動串流端點與縮放比例的傳出頻寬。</span><span class="sxs-lookup"><span data-stu-id="75683-192">It includes hello same features as a **Premium** streaming endpoints and scales outbound bandwidth automatically.</span></span> 

    <span data-ttu-id="75683-193">**進階**串流端點適合進階工作負載，提供專用並能靈活調整的頻寬容量。</span><span class="sxs-lookup"><span data-stu-id="75683-193">**Premium** streaming endpoints are suitable for advanced workloads, providing dedicated and scalable bandwidth capacity.</span></span> <span data-ttu-id="75683-194">擁有**進階**串流端點的客戶預設會取得一個串流單位 (SU)。</span><span class="sxs-lookup"><span data-stu-id="75683-194">Customers that have a **Premium** streaming endpoint, by default get one streaming unit (SU).</span></span> <span data-ttu-id="75683-195">可以藉由新增 SUs 調整串流端點的 hello。</span><span class="sxs-lookup"><span data-stu-id="75683-195">hello streaming endpoint can be scaled by adding SUs.</span></span> <span data-ttu-id="75683-196">每個 SU 提供額外的頻寬容量 toohello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="75683-196">Each SU provides additional bandwidth capacity toohello application.</span></span> <span data-ttu-id="75683-197">如需有關調整**Premium**串流端點，請參閱 hello[調整串流端點](media-services-portal-scale-streaming-endpoints.md)主題。</span><span class="sxs-lookup"><span data-stu-id="75683-197">For more information about scaling **Premium** streaming endpoints, see hello [Scaling streaming endpoints](media-services-portal-scale-streaming-endpoints.md) topic.</span></span>

* <span data-ttu-id="75683-198">Media Services 帳戶會決定 hello 速度與媒體處理工作會處理保留單位類型相關聯。</span><span class="sxs-lookup"><span data-stu-id="75683-198">A Media Services account is associated with a Reserved Unit Type, which determines hello speed with which your media processing tasks are processed.</span></span> <span data-ttu-id="75683-199">您可以挑選之間 hello 下列保留單位類型： **S1**， **S2**，或**S3**。</span><span class="sxs-lookup"><span data-stu-id="75683-199">You can pick between hello following reserved unit types: **S1**, **S2**, or **S3**.</span></span> <span data-ttu-id="75683-200">例如，當您使用 hello 相同的編碼工作執行速度的 hello **S2**保留的單位類型比較 toohello **S1**型別。</span><span class="sxs-lookup"><span data-stu-id="75683-200">For example, hello same encoding job runs faster when you use hello **S2** reserved unit type compare toohello **S1** type.</span></span>

    <span data-ttu-id="75683-201">此外 toospecifying hello 保留單位類型，您可以指定 tooprovision 您帳戶的**保留單位**(RUs)。</span><span class="sxs-lookup"><span data-stu-id="75683-201">In addition toospecifying hello reserved unit type, you can specify tooprovision your account with **Reserved Units** (RUs).</span></span> <span data-ttu-id="75683-202">佈建之俄文的 hello 數目會決定 hello 可以指定帳戶中並行處理的媒體工作數目。</span><span class="sxs-lookup"><span data-stu-id="75683-202">hello number of provisioned RUs determines hello number of media tasks that can be processed concurrently in a given account.</span></span>

    >[!NOTE]
    ><span data-ttu-id="75683-203">RU 用於平行化所有媒體處理，包括使用 Azure 媒體索引器的索引作業。</span><span class="sxs-lookup"><span data-stu-id="75683-203">RUs work for parallelizing all media processing, including indexing jobs using Azure Media Indexer.</span></span> <span data-ttu-id="75683-204">不過，與編碼不同，索引工作的處理速度不會因為使用較快的保留單元而變快。</span><span class="sxs-lookup"><span data-stu-id="75683-204">However, unlike encoding, indexing jobs do not get processed faster with faster reserved units.</span></span>

    <span data-ttu-id="75683-205">如需詳細資訊，請參閱[調整媒體處理](media-services-portal-scale-media-processing.md)。</span><span class="sxs-lookup"><span data-stu-id="75683-205">For more information see, [Scale media processing](media-services-portal-scale-media-processing.md).</span></span>
* <span data-ttu-id="75683-206">您也可以藉由新增儲存體帳戶 tooit 調整 Media Services 帳戶。</span><span class="sxs-lookup"><span data-stu-id="75683-206">You can also scale your Media Services account by adding storage accounts tooit.</span></span> <span data-ttu-id="75683-207">每個儲存體帳戶為有限的 too500 TB。</span><span class="sxs-lookup"><span data-stu-id="75683-207">Each storage account is limited too500 TB.</span></span> <span data-ttu-id="75683-208">tooexpand hello 預設限制超過儲存體，您可以選擇 tooattach 多個儲存體帳戶 tooa 單一 Media Services 帳戶。</span><span class="sxs-lookup"><span data-stu-id="75683-208">tooexpand your storage beyond hello default limitations, you can choose tooattach multiple storage accounts tooa single Media Services account.</span></span> <span data-ttu-id="75683-209">如需詳細資訊，請參閱[管理儲存體帳戶](meda-services-managing-multiple-storage-accounts.md)。</span><span class="sxs-lookup"><span data-stu-id="75683-209">For more information, see [Manage storage accounts](meda-services-managing-multiple-storage-accounts.md).</span></span>

##<span data-ttu-id="75683-210"><a id="availability"></a> 跨資料中心的媒體服務功能可用性</span><span class="sxs-lookup"><span data-stu-id="75683-210"><a id="availability"></a> Availability of Media Services features across datacenters</span></span>

<span data-ttu-id="75683-211">本節詳述跨資料中心的媒體服務功能可用性。</span><span class="sxs-lookup"><span data-stu-id="75683-211">This section provides details about availability of Media Services features across datacenters.</span></span>

### <a name="ams-accounts"></a><span data-ttu-id="75683-212">AMS 帳戶</span><span class="sxs-lookup"><span data-stu-id="75683-212">AMS accounts</span></span>

#### <a name="availability"></a><span data-ttu-id="75683-213">Availability</span><span class="sxs-lookup"><span data-stu-id="75683-213">Availability</span></span>

<span data-ttu-id="75683-214">您可以建立 Media Services 帳戶，在下列區域的 hello： 北歐、 西歐、 美國西部、 美國東部、 東南亞、 東亞、 日本西部、 日本東部、 巴西南部、 印度西部、 印度南部和印度中部。</span><span class="sxs-lookup"><span data-stu-id="75683-214">You can create Media Services accounts in hello following regions: North Europe, West Europe, West US, East US, Southeast Asia, East Asia, Japan West, Japan East, Brazil South, India West, India South, and India Central.</span></span> 

### <a name="streaming-endpoints"></a><span data-ttu-id="75683-215">串流端點</span><span class="sxs-lookup"><span data-stu-id="75683-215">Streaming endpoints</span></span> 

<span data-ttu-id="75683-216">媒體服務客戶可以選擇一個**標準**串流端點或一個**進階**串流端點。</span><span class="sxs-lookup"><span data-stu-id="75683-216">Media Services customers can choose either a **Standard** streaming endpoint or a **Premium** streaming endpoint.</span></span> <span data-ttu-id="75683-217">如需詳細資訊，請參閱 hello[調整](#scaling)> 一節。</span><span class="sxs-lookup"><span data-stu-id="75683-217">For more information, see hello [scaling](#scaling) section.</span></span>

#### <a name="availability"></a><span data-ttu-id="75683-218">Availability</span><span class="sxs-lookup"><span data-stu-id="75683-218">Availability</span></span>

|<span data-ttu-id="75683-219">名稱</span><span class="sxs-lookup"><span data-stu-id="75683-219">Name</span></span>|<span data-ttu-id="75683-220">狀態</span><span class="sxs-lookup"><span data-stu-id="75683-220">Status</span></span>|<span data-ttu-id="75683-221">資料中心</span><span class="sxs-lookup"><span data-stu-id="75683-221">Datacenters</span></span>
|---|---|---|
|<span data-ttu-id="75683-222">標準</span><span class="sxs-lookup"><span data-stu-id="75683-222">Standard</span></span>|<span data-ttu-id="75683-223">GA</span><span class="sxs-lookup"><span data-stu-id="75683-223">GA</span></span>|<span data-ttu-id="75683-224">全部</span><span class="sxs-lookup"><span data-stu-id="75683-224">All</span></span>|
|<span data-ttu-id="75683-225">進階</span><span class="sxs-lookup"><span data-stu-id="75683-225">Premium</span></span>|<span data-ttu-id="75683-226">GA</span><span class="sxs-lookup"><span data-stu-id="75683-226">GA</span></span>|<span data-ttu-id="75683-227">全部</span><span class="sxs-lookup"><span data-stu-id="75683-227">All</span></span>|

### <a name="live-encoding"></a><span data-ttu-id="75683-228">即時編碼</span><span class="sxs-lookup"><span data-stu-id="75683-228">Live encoding</span></span>

#### <a name="availability"></a><span data-ttu-id="75683-229">Availability</span><span class="sxs-lookup"><span data-stu-id="75683-229">Availability</span></span>

<span data-ttu-id="75683-230">所有資料中心內都提供，但不含：德國、巴西南部、印度西部、印度南部和印度中部。</span><span class="sxs-lookup"><span data-stu-id="75683-230">Available in all datacenters except: Germany, Brazil South, India West, India South, and India Central.</span></span> 

### <a name="encoding-media-processors"></a><span data-ttu-id="75683-231">編碼媒體處理器</span><span class="sxs-lookup"><span data-stu-id="75683-231">Encoding media processors</span></span>

<span data-ttu-id="75683-232">AMS 提供兩個隨選編碼器：**媒體編碼器標準**和**媒體編碼器進階工作流程**。</span><span class="sxs-lookup"><span data-stu-id="75683-232">AMS offers two on-demand encoders **Media Encoder Standard** and **Media Encoder Premium Workflow**.</span></span> <span data-ttu-id="75683-233">如需詳細資訊，請參閱 [Azure 隨選媒體編碼器的概觀和比較](media-services-encode-asset.md)。</span><span class="sxs-lookup"><span data-stu-id="75683-233">For more information, see [Overview and comparison of Azure on-demand media encoders](media-services-encode-asset.md).</span></span> 

#### <a name="availability"></a><span data-ttu-id="75683-234">Availability</span><span class="sxs-lookup"><span data-stu-id="75683-234">Availability</span></span>

|<span data-ttu-id="75683-235">媒體處理器名稱</span><span class="sxs-lookup"><span data-stu-id="75683-235">Media processor name</span></span>|<span data-ttu-id="75683-236">狀態</span><span class="sxs-lookup"><span data-stu-id="75683-236">Status</span></span>|<span data-ttu-id="75683-237">資料中心</span><span class="sxs-lookup"><span data-stu-id="75683-237">Datacenters</span></span>
|---|---|---|
|<span data-ttu-id="75683-238">Media Encoder Standard</span><span class="sxs-lookup"><span data-stu-id="75683-238">Media Encoder Standard</span></span>|<span data-ttu-id="75683-239">GA</span><span class="sxs-lookup"><span data-stu-id="75683-239">GA</span></span>|<span data-ttu-id="75683-240">全部</span><span class="sxs-lookup"><span data-stu-id="75683-240">All</span></span>|
|<span data-ttu-id="75683-241">媒體編碼器高階工作流程</span><span class="sxs-lookup"><span data-stu-id="75683-241">Media Encoder Premium Workflow</span></span>|<span data-ttu-id="75683-242">GA</span><span class="sxs-lookup"><span data-stu-id="75683-242">GA</span></span>|<span data-ttu-id="75683-243">所有區域 (中國除外)</span><span class="sxs-lookup"><span data-stu-id="75683-243">All except China</span></span>|

### <a name="analytics-media-processors"></a><span data-ttu-id="75683-244">分析媒體處理器</span><span class="sxs-lookup"><span data-stu-id="75683-244">Analytics media processors</span></span>

<span data-ttu-id="75683-245">媒體分析是語音和願景的元件，讓組織和企業 tooderive 可執行的洞察力更容易從視訊檔案的集合。</span><span class="sxs-lookup"><span data-stu-id="75683-245">Media Analytics is a collection of speech and vision components that makes it easier for organizations and enterprises tooderive actionable insights from their video files.</span></span> <span data-ttu-id="75683-246">如需詳細資訊，請參閱 [Azure 媒體服務分析概觀](media-services-analytics-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="75683-246">For more information, see [Azure Media Services Analytics Overview](media-services-analytics-overview.md).</span></span>

#### <a name="availability"></a><span data-ttu-id="75683-247">Availability</span><span class="sxs-lookup"><span data-stu-id="75683-247">Availability</span></span>

|<span data-ttu-id="75683-248">媒體處理器名稱</span><span class="sxs-lookup"><span data-stu-id="75683-248">Media processor name</span></span>|<span data-ttu-id="75683-249">狀態</span><span class="sxs-lookup"><span data-stu-id="75683-249">Status</span></span>|<span data-ttu-id="75683-250">資料中心</span><span class="sxs-lookup"><span data-stu-id="75683-250">Datacenters</span></span>
|---|---|---|
|<span data-ttu-id="75683-251">Azure 媒體臉部偵測器</span><span class="sxs-lookup"><span data-stu-id="75683-251">Azure Media Face Detector</span></span>|<span data-ttu-id="75683-252">預覽</span><span class="sxs-lookup"><span data-stu-id="75683-252">Preview</span></span>|<span data-ttu-id="75683-253">全部</span><span class="sxs-lookup"><span data-stu-id="75683-253">All</span></span>|
|<span data-ttu-id="75683-254">Azure Media Hyperlapse</span><span class="sxs-lookup"><span data-stu-id="75683-254">Azure Media Hyperlapse</span></span>|<span data-ttu-id="75683-255">預覽</span><span class="sxs-lookup"><span data-stu-id="75683-255">Preview</span></span>|<span data-ttu-id="75683-256">全部</span><span class="sxs-lookup"><span data-stu-id="75683-256">All</span></span>|
|<span data-ttu-id="75683-257">Azure Media Indexer</span><span class="sxs-lookup"><span data-stu-id="75683-257">Azure Media Indexer</span></span>|<span data-ttu-id="75683-258">GA</span><span class="sxs-lookup"><span data-stu-id="75683-258">GA</span></span>|<span data-ttu-id="75683-259">全部</span><span class="sxs-lookup"><span data-stu-id="75683-259">All</span></span>|
|<span data-ttu-id="75683-260">Azure 媒體動作偵測器</span><span class="sxs-lookup"><span data-stu-id="75683-260">Azure Media Motion Detector</span></span>|<span data-ttu-id="75683-261">預覽</span><span class="sxs-lookup"><span data-stu-id="75683-261">Preview</span></span>|<span data-ttu-id="75683-262">全部</span><span class="sxs-lookup"><span data-stu-id="75683-262">All</span></span>|
|<span data-ttu-id="75683-263">Azure 媒體 OCR</span><span class="sxs-lookup"><span data-stu-id="75683-263">Azure Media OCR</span></span>|<span data-ttu-id="75683-264">預覽</span><span class="sxs-lookup"><span data-stu-id="75683-264">Preview</span></span>|<span data-ttu-id="75683-265">全部</span><span class="sxs-lookup"><span data-stu-id="75683-265">All</span></span>|
|<span data-ttu-id="75683-266">Azure 媒體Media Redactor</span><span class="sxs-lookup"><span data-stu-id="75683-266">Azure Media Redactor</span></span>|<span data-ttu-id="75683-267">預覽</span><span class="sxs-lookup"><span data-stu-id="75683-267">Preview</span></span>|<span data-ttu-id="75683-268">全部</span><span class="sxs-lookup"><span data-stu-id="75683-268">All</span></span>|
|<span data-ttu-id="75683-269">Azure Media Stabilizer</span><span class="sxs-lookup"><span data-stu-id="75683-269">Azure Media Stabilizer</span></span>|<span data-ttu-id="75683-270">預覽</span><span class="sxs-lookup"><span data-stu-id="75683-270">Preview</span></span>|<span data-ttu-id="75683-271">全部</span><span class="sxs-lookup"><span data-stu-id="75683-271">All</span></span>|
|<span data-ttu-id="75683-272">Azure 媒體視訊縮圖</span><span class="sxs-lookup"><span data-stu-id="75683-272">Azure Media Video Thumbnails</span></span>|<span data-ttu-id="75683-273">預覽</span><span class="sxs-lookup"><span data-stu-id="75683-273">Preview</span></span>|<span data-ttu-id="75683-274">全部</span><span class="sxs-lookup"><span data-stu-id="75683-274">All</span></span>|
|<span data-ttu-id="75683-275">Azure 媒體索引器 2</span><span class="sxs-lookup"><span data-stu-id="75683-275">Azure Media Indexer 2</span></span>|<span data-ttu-id="75683-276">預覽</span><span class="sxs-lookup"><span data-stu-id="75683-276">Preview</span></span>|<span data-ttu-id="75683-277">所有區域 (中國和美國聯邦政府區域除外)</span><span class="sxs-lookup"><span data-stu-id="75683-277">All except China and Federal Government region</span></span>|

### <a name="protection"></a><span data-ttu-id="75683-278">保護</span><span class="sxs-lookup"><span data-stu-id="75683-278">Protection</span></span>

<span data-ttu-id="75683-279">Microsoft Azure Media Services 可讓您 toosecure 離開您的電腦，透過儲存體、 處理和傳遞的 hello 時間從您的媒體。</span><span class="sxs-lookup"><span data-stu-id="75683-279">Microsoft Azure Media Services enables you toosecure your media from hello time it leaves your computer through storage, processing, and delivery.</span></span> <span data-ttu-id="75683-280">如需詳細資訊，請參閱[保護 AMS 內容](media-services-content-protection-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="75683-280">For more information, see [Protecting AMS content](media-services-content-protection-overview.md).</span></span>

#### <a name="availability"></a><span data-ttu-id="75683-281">Availability</span><span class="sxs-lookup"><span data-stu-id="75683-281">Availability</span></span>

|<span data-ttu-id="75683-282">加密</span><span class="sxs-lookup"><span data-stu-id="75683-282">Encryption</span></span>|<span data-ttu-id="75683-283">狀態</span><span class="sxs-lookup"><span data-stu-id="75683-283">Status</span></span>|<span data-ttu-id="75683-284">資料中心</span><span class="sxs-lookup"><span data-stu-id="75683-284">Datacenters</span></span>|
|---|---|---| 
|<span data-ttu-id="75683-285">儲存體</span><span class="sxs-lookup"><span data-stu-id="75683-285">Storage</span></span>|<span data-ttu-id="75683-286">GA</span><span class="sxs-lookup"><span data-stu-id="75683-286">GA</span></span>|<span data-ttu-id="75683-287">全部</span><span class="sxs-lookup"><span data-stu-id="75683-287">All</span></span>|
|<span data-ttu-id="75683-288">AES-128 金鑰</span><span class="sxs-lookup"><span data-stu-id="75683-288">AES-128 keys</span></span>|<span data-ttu-id="75683-289">GA</span><span class="sxs-lookup"><span data-stu-id="75683-289">GA</span></span>|<span data-ttu-id="75683-290">全部</span><span class="sxs-lookup"><span data-stu-id="75683-290">All</span></span>|
|<span data-ttu-id="75683-291">Fairplay</span><span class="sxs-lookup"><span data-stu-id="75683-291">Fairplay</span></span>|<span data-ttu-id="75683-292">GA</span><span class="sxs-lookup"><span data-stu-id="75683-292">GA</span></span>|<span data-ttu-id="75683-293">全部</span><span class="sxs-lookup"><span data-stu-id="75683-293">All</span></span>|
|<span data-ttu-id="75683-294">PlayReady</span><span class="sxs-lookup"><span data-stu-id="75683-294">PlayReady</span></span>|<span data-ttu-id="75683-295">GA</span><span class="sxs-lookup"><span data-stu-id="75683-295">GA</span></span>|<span data-ttu-id="75683-296">全部</span><span class="sxs-lookup"><span data-stu-id="75683-296">All</span></span>|
|<span data-ttu-id="75683-297">Widevine</span><span class="sxs-lookup"><span data-stu-id="75683-297">Widevine</span></span>|<span data-ttu-id="75683-298">GA</span><span class="sxs-lookup"><span data-stu-id="75683-298">GA</span></span>|<span data-ttu-id="75683-299">全部，但不含德國、美國聯邦政府和中國。</span><span class="sxs-lookup"><span data-stu-id="75683-299">All except Germany, Federal Government and China.</span></span>

### <a name="reserved-units-rus"></a><span data-ttu-id="75683-300">保留單元 (RU)</span><span class="sxs-lookup"><span data-stu-id="75683-300">Reserved units (RUs)</span></span>

<span data-ttu-id="75683-301">hello 佈建的保留單元數目決定 hello 可以指定帳戶中並行處理的媒體工作數目。</span><span class="sxs-lookup"><span data-stu-id="75683-301">hello number of provisioned reserved units determines hello number of media tasks that can be processed concurrently in a given account.</span></span> 

<span data-ttu-id="75683-302">如需詳細資訊，請參閱 hello[調整](#scaling)> 一節。</span><span class="sxs-lookup"><span data-stu-id="75683-302">For more information, see hello [scaling](#scaling) section.</span></span>

#### <a name="availability"></a><span data-ttu-id="75683-303">Availability</span><span class="sxs-lookup"><span data-stu-id="75683-303">Availability</span></span>

<span data-ttu-id="75683-304">所有資料中心內都提供。</span><span class="sxs-lookup"><span data-stu-id="75683-304">Available in all datacenters.</span></span>

### <a name="reserved-unit-ru-type"></a><span data-ttu-id="75683-305">保留單元 (RU) 類型</span><span class="sxs-lookup"><span data-stu-id="75683-305">Reserved unit (RU) type</span></span>

<span data-ttu-id="75683-306">Media Services 帳戶會保留的單位類型，用來決定 hello 速度處理您的媒體處理工作的相關聯。</span><span class="sxs-lookup"><span data-stu-id="75683-306">A Media Services account is associated with a Reserved unit type, which determines hello speed with which your media processing tasks are processed.</span></span> <span data-ttu-id="75683-307">您可以挑選之間 hello 下列保留單位類型： S1、 S2 或 S3。</span><span class="sxs-lookup"><span data-stu-id="75683-307">You can pick between hello following reserved unit types: S1, S2, or S3.</span></span>

<span data-ttu-id="75683-308">如需詳細資訊，請參閱 hello[調整](#scaling)> 一節。</span><span class="sxs-lookup"><span data-stu-id="75683-308">For more information, see hello [scaling](#scaling) section.</span></span>

#### <a name="availability"></a><span data-ttu-id="75683-309">Availability</span><span class="sxs-lookup"><span data-stu-id="75683-309">Availability</span></span>

|<span data-ttu-id="75683-310">RU 類型名稱</span><span class="sxs-lookup"><span data-stu-id="75683-310">RU type name</span></span>|<span data-ttu-id="75683-311">狀態</span><span class="sxs-lookup"><span data-stu-id="75683-311">Status</span></span>|<span data-ttu-id="75683-312">資料中心</span><span class="sxs-lookup"><span data-stu-id="75683-312">Datacenters</span></span>
|---|---|---|
|<span data-ttu-id="75683-313">S1</span><span class="sxs-lookup"><span data-stu-id="75683-313">S1</span></span>|<span data-ttu-id="75683-314">GA</span><span class="sxs-lookup"><span data-stu-id="75683-314">GA</span></span>|<span data-ttu-id="75683-315">全部</span><span class="sxs-lookup"><span data-stu-id="75683-315">All</span></span>|
|<span data-ttu-id="75683-316">S2</span><span class="sxs-lookup"><span data-stu-id="75683-316">S2</span></span>|<span data-ttu-id="75683-317">GA</span><span class="sxs-lookup"><span data-stu-id="75683-317">GA</span></span>|<span data-ttu-id="75683-318">全部，但不含巴西南部和印度西部</span><span class="sxs-lookup"><span data-stu-id="75683-318">All except Brazil South, and India West</span></span>|
|<span data-ttu-id="75683-319">S3</span><span class="sxs-lookup"><span data-stu-id="75683-319">S3</span></span>|<span data-ttu-id="75683-320">GA</span><span class="sxs-lookup"><span data-stu-id="75683-320">GA</span></span>|<span data-ttu-id="75683-321">全部，但不含印度西部</span><span class="sxs-lookup"><span data-stu-id="75683-321">All except India West</span></span>|

## <a name="next-steps"></a><span data-ttu-id="75683-322">後續步驟</span><span class="sxs-lookup"><span data-stu-id="75683-322">Next steps</span></span>

<span data-ttu-id="75683-323">檢閱媒體服務學習路徑。</span><span class="sxs-lookup"><span data-stu-id="75683-323">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="75683-324">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="75683-324">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

