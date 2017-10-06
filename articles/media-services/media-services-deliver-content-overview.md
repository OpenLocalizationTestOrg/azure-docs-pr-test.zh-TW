---
title: "aaaDelivering 內容 toocustomers |Microsoft 文件"
description: "本主題簡介當您利用 Azure 媒體服務傳遞內容時會涉及各個方面。"
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 89ede54a-6a9c-4814-9858-dcfbb5f4fed5
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: juliako
ms.openlocfilehash: 0570bd62d9d42633df0132f9449b357e2abb4086
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deliver-content-toocustomers"></a><span data-ttu-id="3a5d1-103">傳遞內容 toocustomers</span><span class="sxs-lookup"><span data-stu-id="3a5d1-103">Deliver content toocustomers</span></span>
<span data-ttu-id="3a5d1-104">當提供資料流或 video-on-demand 內容 toocustomers 時，您的目標是在不同的網路狀況下 toodeliver 高品質的視訊 toovarious 裝置。</span><span class="sxs-lookup"><span data-stu-id="3a5d1-104">When you're delivering your streaming or video-on-demand content toocustomers, your goal is toodeliver high-quality video toovarious devices under different network conditions.</span></span>

<span data-ttu-id="3a5d1-105">tooachieve 達成此目標，您可以：</span><span class="sxs-lookup"><span data-stu-id="3a5d1-105">tooachieve this goal, you can:</span></span>

* <span data-ttu-id="3a5d1-106">編碼的資料流 tooa 多位元速率 （彈性位元速率） 視訊資料流。</span><span class="sxs-lookup"><span data-stu-id="3a5d1-106">Encode your stream tooa multi-bitrate (adaptive bitrate) video stream.</span></span> <span data-ttu-id="3a5d1-107">這會負責處理品質和網路狀況。</span><span class="sxs-lookup"><span data-stu-id="3a5d1-107">This will take care of quality and network conditions.</span></span>
* <span data-ttu-id="3a5d1-108">使用 Microsoft Azure Media Services[動態封裝](media-services-dynamic-packaging-overview.md)toodynamically 重新封裝您的資料流成不同的通訊協定。</span><span class="sxs-lookup"><span data-stu-id="3a5d1-108">Use Microsoft Azure Media Services [dynamic packaging](media-services-dynamic-packaging-overview.md) toodynamically re-package your stream into different protocols.</span></span> <span data-ttu-id="3a5d1-109">這會負責處理不同裝置上的串流處理。</span><span class="sxs-lookup"><span data-stu-id="3a5d1-109">This will take care of streaming on different devices.</span></span> <span data-ttu-id="3a5d1-110">Media Services 支援的下列彈性位元速率串流技術的 hello 傳遞： HTTP Live Streaming (HLS)、 Smooth Streaming 和 MPEG DASH。</span><span class="sxs-lookup"><span data-stu-id="3a5d1-110">Media Services supports delivery of hello following adaptive bitrate streaming technologies: HTTP Live Streaming (HLS), Smooth Streaming, and MPEG-DASH.</span></span>

>[!NOTE]
><span data-ttu-id="3a5d1-111">AMS 帳戶建立時**預設**串流端點就會加入 tooyour 帳戶 hello**已停止**狀態。</span><span class="sxs-lookup"><span data-stu-id="3a5d1-111">When your AMS account is created a **default** streaming endpoint is added tooyour account in hello **Stopped** state.</span></span> <span data-ttu-id="3a5d1-112">串流處理您的內容，並採取利用動態封裝和動態加密，toostart hello 串流端點，您想要從中 toostream 內容已經在 hello toobe**執行**狀態。</span><span class="sxs-lookup"><span data-stu-id="3a5d1-112">toostart streaming your content and take advantage of dynamic packaging and dynamic encryption, hello streaming endpoint from which you want toostream content has toobe in hello **Running** state.</span></span> 

<span data-ttu-id="3a5d1-113">本文提供內容傳遞概念的重要概觀。</span><span class="sxs-lookup"><span data-stu-id="3a5d1-113">This article gives an overview of important content delivery concepts.</span></span>

<span data-ttu-id="3a5d1-114">toocheck 已知問題，請參閱[已知問題](media-services-deliver-content-overview.md#known-issues)。</span><span class="sxs-lookup"><span data-stu-id="3a5d1-114">toocheck known issues, see [Known issues](media-services-deliver-content-overview.md#known-issues).</span></span>

## <a name="dynamic-packaging"></a><span data-ttu-id="3a5d1-115">動態封裝</span><span class="sxs-lookup"><span data-stu-id="3a5d1-115">Dynamic packaging</span></span>
<span data-ttu-id="3a5d1-116">Hello 動態封裝與該媒體服務提供，您可以提供您彈性位元速率 MP4 或 Smooth Streaming 編碼內容，在資料流中支援的媒體服務 （MPEG DASH、 HLS、 Smooth Streaming） 格式而不需要 toore 套件的這些資料流的格式。</span><span class="sxs-lookup"><span data-stu-id="3a5d1-116">With hello dynamic packaging that Media Services provides, you can deliver your adaptive bitrate MP4 or Smooth Streaming encoded content in streaming formats supported by Media Services (MPEG-DASH, HLS, Smooth Streaming,) without having toore-package into these streaming formats.</span></span> <span data-ttu-id="3a5d1-117">我們建議您利用動態封裝傳遞內容。</span><span class="sxs-lookup"><span data-stu-id="3a5d1-117">We recommend delivering your content with dynamic packaging.</span></span>

<span data-ttu-id="3a5d1-118">tootake 利用動態封裝，您需要 tooencode （來源） 夾層檔為一組彈性位元速率 MP4 檔案或彈性位元速率 Smooth Streaming 檔案。</span><span class="sxs-lookup"><span data-stu-id="3a5d1-118">tootake advantage of dynamic packaging, you need tooencode your mezzanine (source) file into a set of adaptive-bitrate MP4 files or adaptive bitrate Smooth Streaming files.</span></span>

<span data-ttu-id="3a5d1-119">使用動態封裝，您可以儲存並支付一種儲存格式中的 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="3a5d1-119">With dynamic packaging, you store and pay for hello files in single storage format.</span></span> <span data-ttu-id="3a5d1-120">媒體服務會建立及傳遞 hello 適當的回應，根據您的要求。</span><span class="sxs-lookup"><span data-stu-id="3a5d1-120">Media Services will build and serve hello appropriate response based on your requests.</span></span>

<span data-ttu-id="3a5d1-121">動態封裝適用於標準和高階串流端點。</span><span class="sxs-lookup"><span data-stu-id="3a5d1-121">Dynamic packaging is available for standard and premium streaming endpoints.</span></span> 

<span data-ttu-id="3a5d1-122">如需詳細資訊，請參閱 [動態封裝](media-services-dynamic-packaging-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="3a5d1-122">For more information, see [Dynamic packaging](media-services-dynamic-packaging-overview.md).</span></span>

## <a name="filters-and-dynamic-manifests"></a><span data-ttu-id="3a5d1-123">篩選器與動態資訊清單</span><span class="sxs-lookup"><span data-stu-id="3a5d1-123">Filters and dynamic manifests</span></span>
<span data-ttu-id="3a5d1-124">您可以使用媒體服務為資產定義篩選器。</span><span class="sxs-lookup"><span data-stu-id="3a5d1-124">You can define filters for your assets with Media Services.</span></span> <span data-ttu-id="3a5d1-125">這些篩選都是伺服器端規則可幫助您執行一些作業，例如播放視訊的特定區段，或指定的音訊和視訊客戶的裝置可以處理 （而不是與 hello 資產相關聯的所有 hello 轉譯的轉譯子集的客戶).</span><span class="sxs-lookup"><span data-stu-id="3a5d1-125">These filters are server-side rules that help your customers do things like play a specific section of a video or specify a subset of audio and video renditions that your customer's device can handle (instead of all hello renditions that are associated with hello asset).</span></span> <span data-ttu-id="3a5d1-126">此篩選透過來達成*動態資訊清單*會在您的客戶要求 toostream 視訊以其中一個或多個指定的篩選條件時建立。</span><span class="sxs-lookup"><span data-stu-id="3a5d1-126">This filtering is achieved through *dynamic manifests* that are created when your customer requests toostream a video based on one or more specified filters.</span></span>

<span data-ttu-id="3a5d1-127">如需詳細資訊，請參閱 [篩選器與動態資訊清單](media-services-dynamic-manifest-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="3a5d1-127">For more information, see [Filters and dynamic manifests](media-services-dynamic-manifest-overview.md).</span></span>

## <a name="locators"></a><span data-ttu-id="3a5d1-128">定位器</span><span class="sxs-lookup"><span data-stu-id="3a5d1-128">Locators</span></span>
<span data-ttu-id="3a5d1-129">tooprovide 您的使用者可以使用的 toostream 或下載您的內容的 url，您必須先 toopublish 資產建立定位器。</span><span class="sxs-lookup"><span data-stu-id="3a5d1-129">tooprovide your user with a URL that can be used toostream or download your content, you first need toopublish your asset by creating a locator.</span></span> <span data-ttu-id="3a5d1-130">定位器提供項目點 tooaccess hello 資產中包含的檔案。</span><span class="sxs-lookup"><span data-stu-id="3a5d1-130">A locator provides an entry point tooaccess hello files contained in an asset.</span></span> <span data-ttu-id="3a5d1-131">媒體服務支援兩種類型的定位器：</span><span class="sxs-lookup"><span data-stu-id="3a5d1-131">Media Services supports two types of locators:</span></span>

* <span data-ttu-id="3a5d1-132">OnDemandOrigin 定位器。</span><span class="sxs-lookup"><span data-stu-id="3a5d1-132">OnDemandOrigin locators.</span></span> <span data-ttu-id="3a5d1-133">這些是使用的 toostream 媒體 （例如，MPEG DASH、 HLS 或 Smooth Streaming），或漸進式下載檔案。</span><span class="sxs-lookup"><span data-stu-id="3a5d1-133">These are used toostream media (for example, MPEG-DASH, HLS, or Smooth Streaming) or progressively download files.</span></span>
* <span data-ttu-id="3a5d1-134">共用存取簽章 (SAS) URL 定位器。</span><span class="sxs-lookup"><span data-stu-id="3a5d1-134">Shared access signature (SAS) URL locators.</span></span> <span data-ttu-id="3a5d1-135">這些是使用的 toodownload 媒體檔案 tooyour 本機電腦。</span><span class="sxs-lookup"><span data-stu-id="3a5d1-135">These are used toodownload media files tooyour local computer.</span></span>

<span data-ttu-id="3a5d1-136">*存取原則*是使用的 toodefine hello 權限 （例如讀取、 寫入和清單） 和用戶端具有存取特定資產的持續時間。</span><span class="sxs-lookup"><span data-stu-id="3a5d1-136">An *access policy* is used toodefine hello permissions (such as read, write, and list) and duration for which a client has access for a particular asset.</span></span> <span data-ttu-id="3a5d1-137">請注意 hello 清單權限 (AccessPermissions.List) 不應該用在建立 OrDemandOrigin 定位器。</span><span class="sxs-lookup"><span data-stu-id="3a5d1-137">Note that hello list permission (AccessPermissions.List) should not be used in creating an OrDemandOrigin locator.</span></span>

<span data-ttu-id="3a5d1-138">定位器有到期日。</span><span class="sxs-lookup"><span data-stu-id="3a5d1-138">Locators have expiration dates.</span></span> <span data-ttu-id="3a5d1-139">hello Azure 入口網站設定到期日 100 年 hello 未來的定位器。</span><span class="sxs-lookup"><span data-stu-id="3a5d1-139">hello Azure portal sets an expiration date 100 years in hello future for locators.</span></span>

> [!NOTE]
> <span data-ttu-id="3a5d1-140">如果您使用 hello Azure 入口網站 toocreate 定位器 2015 年 3 月之前，這些定位器設定 tooexpire 兩年之後。</span><span class="sxs-lookup"><span data-stu-id="3a5d1-140">If you used hello Azure portal toocreate locators before March 2015, those locators were set tooexpire after two years.</span></span>
> 
> 

<span data-ttu-id="3a5d1-141">定位器時，使用上的到期日 tooupdate [REST](https://docs.microsoft.com/rest/api/media/operations/locator#update_a_locator)或[.NET](http://go.microsoft.com/fwlink/?LinkID=533259)應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="3a5d1-141">tooupdate an expiration date on a locator, use [REST](https://docs.microsoft.com/rest/api/media/operations/locator#update_a_locator) or [.NET](http://go.microsoft.com/fwlink/?LinkID=533259) APIs.</span></span> <span data-ttu-id="3a5d1-142">請注意，當您更新的 SAS 定位器的 hello 到期日，hello URL 就會變更。</span><span class="sxs-lookup"><span data-stu-id="3a5d1-142">Note that when you update hello expiration date of a SAS locator, hello URL changes.</span></span>

<span data-ttu-id="3a5d1-143">定位器並非設計 toomanage 每位使用者存取控制。</span><span class="sxs-lookup"><span data-stu-id="3a5d1-143">Locators are not designed toomanage per-user access control.</span></span> <span data-ttu-id="3a5d1-144">您可以使用數位版權管理 (DRM) 解決方案提供不同的存取權限 tooindividual 的使用者。</span><span class="sxs-lookup"><span data-stu-id="3a5d1-144">You can give different access rights tooindividual users by using Digital Rights Management (DRM) solutions.</span></span> <span data-ttu-id="3a5d1-145">如需詳細資訊，請參閱 [保護媒體](http://msdn.microsoft.com/library/azure/dn282272.aspx)。</span><span class="sxs-lookup"><span data-stu-id="3a5d1-145">For more information, see [Securing Media](http://msdn.microsoft.com/library/azure/dn282272.aspx).</span></span>

<span data-ttu-id="3a5d1-146">當您建立定位器時，可能會有 30 秒的延遲，因為 Azure 儲存體中 toorequired 儲存體和傳播程序。</span><span class="sxs-lookup"><span data-stu-id="3a5d1-146">When you create a locator, there may be a 30-second delay due toorequired storage and propagation processes in Azure Storage.</span></span>

## <a name="adaptive-streaming"></a><span data-ttu-id="3a5d1-147">調適性串流處理</span><span class="sxs-lookup"><span data-stu-id="3a5d1-147">Adaptive streaming</span></span>
<span data-ttu-id="3a5d1-148">彈性位元速率技術 toodetermine 網路條件允許影片播放器應用程式，並選取從幾種位元。</span><span class="sxs-lookup"><span data-stu-id="3a5d1-148">Adaptive bitrate technologies allow video player applications toodetermine network conditions and select from several bitrates.</span></span> <span data-ttu-id="3a5d1-149">當降低網路通訊時，請 hello 用戶端可以選取較低的位元速率，因此具有較低的視訊品質，可以繼續播放。</span><span class="sxs-lookup"><span data-stu-id="3a5d1-149">When network communication degrades, hello client can select a lower bitrate so playback can continue with lower video quality.</span></span> <span data-ttu-id="3a5d1-150">當網路狀況的改善，hello 用戶端可以切換 tooa 高位元速率以提高視訊品質。</span><span class="sxs-lookup"><span data-stu-id="3a5d1-150">As network conditions improve, hello client can switch tooa higher bitrate with improved video quality.</span></span> <span data-ttu-id="3a5d1-151">Azure Media Services 支援下列彈性位元速率技術 hello: HTTP Live Streaming (HLS)、 Smooth Streaming 和 MPEG DASH。</span><span class="sxs-lookup"><span data-stu-id="3a5d1-151">Azure Media Services supports hello following adaptive bitrate technologies: HTTP Live Streaming (HLS), Smooth Streaming, and MPEG-DASH.</span></span>

<span data-ttu-id="3a5d1-152">具有串流 Url 的 tooprovide 使用者，您首先必須建立 OnDemandOrigin 定位器。</span><span class="sxs-lookup"><span data-stu-id="3a5d1-152">tooprovide users with streaming URLs, you first must create an OnDemandOrigin locator.</span></span> <span data-ttu-id="3a5d1-153">建立 hello hello 包含 hello 內容的基底路徑 toohello 資產的定位器可讓您 toostream。</span><span class="sxs-lookup"><span data-stu-id="3a5d1-153">Creating hello locator gives you hello base path toohello asset that contains hello content you want toostream.</span></span> <span data-ttu-id="3a5d1-154">不過，此內容，您需要進一步此路徑 toomodify toobe 無法 toostream。</span><span class="sxs-lookup"><span data-stu-id="3a5d1-154">However, toobe able toostream this content, you need toomodify this path further.</span></span> <span data-ttu-id="3a5d1-155">完整的 URL toohello 串流資訊清單檔案，您必須串連 hello 定位器路徑 tooconstruct 值和 hello 資訊清單 (filename.ism) 檔名。</span><span class="sxs-lookup"><span data-stu-id="3a5d1-155">tooconstruct a full URL toohello streaming manifest file, you must concatenate hello locator’s path value and hello manifest (filename.ism) file name.</span></span> <span data-ttu-id="3a5d1-156">然後附加**/資訊清單**和適當的格式 （如有需要） toohello 定位器路徑。</span><span class="sxs-lookup"><span data-stu-id="3a5d1-156">Then append **/Manifest** and an appropriate format (if needed) toohello locator path.</span></span>

> [!NOTE]
> <span data-ttu-id="3a5d1-157">您也可以透過 SSL 連線串流您的內容。</span><span class="sxs-lookup"><span data-stu-id="3a5d1-157">You can also stream your content over an SSL connection.</span></span> <span data-ttu-id="3a5d1-158">toodo，請確定您串流 Url 開頭 HTTPS。</span><span class="sxs-lookup"><span data-stu-id="3a5d1-158">toodo this, make sure your streaming URLs start with HTTPS.</span></span> <span data-ttu-id="3a5d1-159">請注意，目前 AMS 不支援使用 SSL 搭配自訂網域。</span><span class="sxs-lookup"><span data-stu-id="3a5d1-159">Note that, currently, AMS doesn’t support SSL with custom domains.</span></span>  
> 


<span data-ttu-id="3a5d1-160">如果 hello 串流的端點，您可以從中傳遞內容建立在 2014 年 9 月 10 日之後，您只可以串流 over SSL。</span><span class="sxs-lookup"><span data-stu-id="3a5d1-160">You can only stream over SSL if hello streaming endpoint from which you deliver your content was created after September 10th, 2014.</span></span> <span data-ttu-id="3a5d1-161">如果您的串流 Url 根據串流端點的 2014 年 9 月 10 日之後建立的 hello hello URL 包含"streaming.mediaservices.windows.net。 」</span><span class="sxs-lookup"><span data-stu-id="3a5d1-161">If your streaming URLs are based on hello streaming endpoints created after September 10th, 2014, hello URL contains “streaming.mediaservices.windows.net.”</span></span> <span data-ttu-id="3a5d1-162">包含"origin.mediaservices.windows.net 」 （hello 舊格式） 的串流 Url 不支援 SSL。</span><span class="sxs-lookup"><span data-stu-id="3a5d1-162">Streaming URLs that contain “origin.mediaservices.windows.net” (hello old format) do not support SSL.</span></span> <span data-ttu-id="3a5d1-163">如果您的 URL 的 hello 舊格式，而且要透過 SSL toobe 無法 toostream，建立新的串流端點。</span><span class="sxs-lookup"><span data-stu-id="3a5d1-163">If your URL is in hello old format and you want toobe able toostream over SSL, create a new streaming endpoint.</span></span> <span data-ttu-id="3a5d1-164">使用基礎 hello 新端點 toostream 將內容串流透過 SSL 的 Url。</span><span class="sxs-lookup"><span data-stu-id="3a5d1-164">Use URLs based on hello new streaming endpoint toostream your content over SSL.</span></span>

## <a name="streaming-url-formats"></a><span data-ttu-id="3a5d1-165">Streaming URL 格式</span><span class="sxs-lookup"><span data-stu-id="3a5d1-165">Streaming URL formats</span></span>
### <a name="mpeg-dash-format"></a><span data-ttu-id="3a5d1-166">MPEG-DASH 格式</span><span class="sxs-lookup"><span data-stu-id="3a5d1-166">MPEG-DASH format</span></span>
<span data-ttu-id="3a5d1-167">{串流端點名稱-媒體服務帳戶名稱}.streaming.mediaservices.windows.net/{定位器識別碼}/{檔案名稱}.ism/Manifest(format=mpd-time-csf)</span><span class="sxs-lookup"><span data-stu-id="3a5d1-167">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=mpd-time-csf)</span></span>

<span data-ttu-id="3a5d1-168">http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=mpd-time-csf)</span><span class="sxs-lookup"><span data-stu-id="3a5d1-168">http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=mpd-time-csf)</span></span>

### <a name="apple-http-live-streaming-hls-v4-format"></a><span data-ttu-id="3a5d1-169">Apple HTTP Live Streaming (HLS) V4 格式</span><span class="sxs-lookup"><span data-stu-id="3a5d1-169">Apple HTTP Live Streaming (HLS) V4 format</span></span>
<span data-ttu-id="3a5d1-170">{串流端點名稱-媒體服務帳戶名稱}.streaming.mediaservices.windows.net/{定位器識別碼}/{檔案名稱}.ism/Manifest(format=m3u8-aapl)</span><span class="sxs-lookup"><span data-stu-id="3a5d1-170">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=m3u8-aapl)</span></span>

<span data-ttu-id="3a5d1-171">http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=m3u8-aapl)</span><span class="sxs-lookup"><span data-stu-id="3a5d1-171">http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=m3u8-aapl)</span></span>

### <a name="apple-http-live-streaming-hls-v3-format"></a><span data-ttu-id="3a5d1-172">Apple HTTP Live Streaming (HLS) V3 格式</span><span class="sxs-lookup"><span data-stu-id="3a5d1-172">Apple HTTP Live Streaming (HLS) V3 format</span></span>
<span data-ttu-id="3a5d1-173">{串流端點名稱-媒體服務帳戶名稱}.streaming.mediaservices.windows.net/{定位器識別碼}/{檔案名稱}.ism/Manifest(format=m3u8-aapl-v3)</span><span class="sxs-lookup"><span data-stu-id="3a5d1-173">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=m3u8-aapl-v3)</span></span>

<span data-ttu-id="3a5d1-174">http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=m3u8-aapl-v3)</span><span class="sxs-lookup"><span data-stu-id="3a5d1-174">http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=m3u8-aapl-v3)</span></span>

### <a name="apple-http-live-streaming-hls-format-with-audio-only-filter"></a><span data-ttu-id="3a5d1-175">Apple HTTP Live Streaming (HLS) 格式搭配僅限音訊的篩選條件</span><span class="sxs-lookup"><span data-stu-id="3a5d1-175">Apple HTTP Live Streaming (HLS) format with audio-only filter</span></span>
<span data-ttu-id="3a5d1-176">根據預設，僅限音訊播放軌併入的 hello HLS 資訊清單。</span><span class="sxs-lookup"><span data-stu-id="3a5d1-176">By default, audio-only tracks are included in hello HLS manifest.</span></span> <span data-ttu-id="3a5d1-177">這對於行動電話通訊網路的 Apple Store 認證是必要條件。</span><span class="sxs-lookup"><span data-stu-id="3a5d1-177">This is required for Apple Store certification for cellular networks.</span></span> <span data-ttu-id="3a5d1-178">在此情況下，如果用戶端沒有足夠的頻寬或連線透過 2g 連線，播放會切換 tooaudio 專用。</span><span class="sxs-lookup"><span data-stu-id="3a5d1-178">In this case, if a client doesn’t have sufficient bandwidth or is connected over a 2G connection, playback switches tooaudio-only.</span></span> <span data-ttu-id="3a5d1-179">這有助於 tookeep 內容資料流不進行緩衝處理，但沒有影像。</span><span class="sxs-lookup"><span data-stu-id="3a5d1-179">This helps tookeep content streaming without buffering, but there is no video.</span></span> <span data-ttu-id="3a5d1-180">在某些情況中，播放程式緩衝處理可能比只有音訊更好。</span><span class="sxs-lookup"><span data-stu-id="3a5d1-180">In some scenarios, player buffering might be preferred over audio-only.</span></span> <span data-ttu-id="3a5d1-181">如果您想 tooremove hello 純音訊播放軌時，將**碴錼 = false** toohello URL。</span><span class="sxs-lookup"><span data-stu-id="3a5d1-181">If you want tooremove hello audio-only track, add **audio-only=false** toohello URL.</span></span>

<span data-ttu-id="3a5d1-182">http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=m3u8-aapl-v3,audio-only=false)</span><span class="sxs-lookup"><span data-stu-id="3a5d1-182">http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=m3u8-aapl-v3,audio-only=false)</span></span>

<span data-ttu-id="3a5d1-183">如需詳細資訊，請參閱 [Dynamic Manifest Composition support and HLS output additional features (動態資訊清單組合支援和 HLS 輸出額外功能)](https://azure.microsoft.com/blog/azure-media-services-release-dynamic-manifest-composition-remove-hls-audio-only-track-and-hls-i-frame-track-support/)。</span><span class="sxs-lookup"><span data-stu-id="3a5d1-183">For more information, see [Dynamic Manifest Composition support and HLS output additional features](https://azure.microsoft.com/blog/azure-media-services-release-dynamic-manifest-composition-remove-hls-audio-only-track-and-hls-i-frame-track-support/).</span></span>

### <a name="smooth-streaming-format"></a><span data-ttu-id="3a5d1-184">Smooth Streaming 格式</span><span class="sxs-lookup"><span data-stu-id="3a5d1-184">Smooth Streaming format</span></span>
<span data-ttu-id="3a5d1-185">{串流端點名稱-媒體服務帳戶名稱}.streaming.mediaservices.windows.net/{定位器識別碼}/{檔案名稱}.ism/Manifest</span><span class="sxs-lookup"><span data-stu-id="3a5d1-185">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest</span></span>

<span data-ttu-id="3a5d1-186">範例：</span><span class="sxs-lookup"><span data-stu-id="3a5d1-186">Example:</span></span>

<span data-ttu-id="3a5d1-187">http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest</span><span class="sxs-lookup"><span data-stu-id="3a5d1-187">http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest</span></span>

### <span data-ttu-id="3a5d1-188"><a id="fmp4_v20"></a>Smooth Streaming 2.0 資訊清單 (舊版資訊清單)</span><span class="sxs-lookup"><span data-stu-id="3a5d1-188"><a id="fmp4_v20"></a>Smooth Streaming 2.0 manifest (legacy manifest)</span></span>
<span data-ttu-id="3a5d1-189">根據預設，Smooth Streaming 資訊清單的格式包含 hello 重複標記 (r tag)。</span><span class="sxs-lookup"><span data-stu-id="3a5d1-189">By default, Smooth Streaming manifest format contains hello repeat tag (r-tag).</span></span> <span data-ttu-id="3a5d1-190">不過，有些播放程式不支援 hello r 標記。</span><span class="sxs-lookup"><span data-stu-id="3a5d1-190">However, some players do not support hello r-tag.</span></span> <span data-ttu-id="3a5d1-191">這些播放程式的用戶端可以使用停用 hello r 標記的格式：</span><span class="sxs-lookup"><span data-stu-id="3a5d1-191">Clients with these players can use a format that disables hello r-tag:</span></span>

<span data-ttu-id="3a5d1-192">{串流端點名稱-媒體服務帳戶名稱}.streaming.mediaservices.windows.net/{定位器識別碼}/{檔案名稱}.ism/Manifest(format=fmp4-v20)</span><span class="sxs-lookup"><span data-stu-id="3a5d1-192">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=fmp4-v20)</span></span>

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=fmp4-v20)

## <a name="progressive-download"></a><span data-ttu-id="3a5d1-193">漸進式下載</span><span class="sxs-lookup"><span data-stu-id="3a5d1-193">Progressive download</span></span>
<span data-ttu-id="3a5d1-194">漸進式下載，您可以開始播放媒體之前已下載 hello 整個檔案。</span><span class="sxs-lookup"><span data-stu-id="3a5d1-194">With progressive download, you can start playing media before hello entire file has been downloaded.</span></span> <span data-ttu-id="3a5d1-195">您無法漸進式下載 .ism* (ismv、isma、ismt 或 ismc) 檔案。</span><span class="sxs-lookup"><span data-stu-id="3a5d1-195">You cannot progressively download .ism* (ismv, isma, ismt, or ismc) files.</span></span>

<span data-ttu-id="3a5d1-196">tooprogressively 下載內容時，使用 hello OnDemandOrigin 定位器類型。</span><span class="sxs-lookup"><span data-stu-id="3a5d1-196">tooprogressively download content, use hello OnDemandOrigin type of locator.</span></span> <span data-ttu-id="3a5d1-197">hello 下列範例顯示 hello hello OnDemandOrigin 定位器類型為基礎的 URL:</span><span class="sxs-lookup"><span data-stu-id="3a5d1-197">hello following example shows hello URL that is based on hello OnDemandOrigin type of locator:</span></span>

    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny_H264_650kbps_AAC_und_ch2_96kbps.mp4

<span data-ttu-id="3a5d1-198">您必須解密想 toostream 漸進式下載的 hello origin 服務的任何儲存體加密資產。</span><span class="sxs-lookup"><span data-stu-id="3a5d1-198">You must decrypt any storage-encrypted assets that you want toostream from hello origin service for progressive download.</span></span>

## <a name="download"></a><span data-ttu-id="3a5d1-199">下載</span><span class="sxs-lookup"><span data-stu-id="3a5d1-199">Download</span></span>
<span data-ttu-id="3a5d1-200">toodownload 內容 tooa 用戶端裝置，您必須建立 SAS 定位器。</span><span class="sxs-lookup"><span data-stu-id="3a5d1-200">toodownload your content tooa client device, you must create a SAS Locator.</span></span> <span data-ttu-id="3a5d1-201">hello SAS 定位器可讓您存取您的檔案所在位置的 toohello Azure 儲存體容器。</span><span class="sxs-lookup"><span data-stu-id="3a5d1-201">hello SAS locator gives you access toohello Azure Storage container where your file is located.</span></span> <span data-ttu-id="3a5d1-202">toobuild hello 下載 URL，您有 hello 主機與 SAS 簽章之間的 tooembed hello 檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="3a5d1-202">toobuild hello download URL, you have tooembed hello file name between hello host and SAS signature.</span></span>

<span data-ttu-id="3a5d1-203">hello 下列範例會顯示 hello URL 為基礎的 hello SAS 定位器：</span><span class="sxs-lookup"><span data-stu-id="3a5d1-203">hello following example shows hello URL that is based on hello SAS locator:</span></span>

    https://test001.blob.core.windows.net/asset-ca7a4c3f-9eb5-4fd8-a898-459cb17761bd/BigBuckBunny.mp4?sv=2012-02-12&se=2014-05-03T01%3A23%3A50Z&sr=c&si=7c093e7c-7dab-45b4-beb4-2bfdff764bb5&sig=msEHP90c6JHXEOtTyIWqD7xio91GtVg0UIzjdpFscHk%3D

<span data-ttu-id="3a5d1-204">hello 下列考量適用於：</span><span class="sxs-lookup"><span data-stu-id="3a5d1-204">hello following considerations apply:</span></span>

* <span data-ttu-id="3a5d1-205">您必須解密想 toostream 漸進式下載的 hello origin 服務的任何儲存體加密資產。</span><span class="sxs-lookup"><span data-stu-id="3a5d1-205">You must decrypt any storage-encrypted assets that you want toostream from hello origin service for progressive download.</span></span>
* <span data-ttu-id="3a5d1-206">未在 12 小時內完成的下載，最後一定會失敗。</span><span class="sxs-lookup"><span data-stu-id="3a5d1-206">A download that has not finished within 12 hours will fail.</span></span>

## <a name="streaming-endpoints"></a><span data-ttu-id="3a5d1-207">串流端點</span><span class="sxs-lookup"><span data-stu-id="3a5d1-207">Streaming endpoints</span></span>

<span data-ttu-id="3a5d1-208">串流端點，代表可以將內容傳遞直接 tooa 用戶端播放器應用程式或 tooa 內容傳遞網路 (CDN) 的進一步發佈的串流服務。</span><span class="sxs-lookup"><span data-stu-id="3a5d1-208">A streaming endpoint represents a streaming service that can deliver content directly tooa client player application or tooa content delivery network (CDN) for further distribution.</span></span> <span data-ttu-id="3a5d1-209">從資料流的端點服務的 hello 輸出資料流可以是即時資料流或 video-on-demand 資產 Media Services 帳戶中。</span><span class="sxs-lookup"><span data-stu-id="3a5d1-209">hello outbound stream from a streaming endpoint service can be a live stream or a video-on-demand asset in your Media Services account.</span></span> <span data-ttu-id="3a5d1-210">串流端點有兩種類型：「標準」和「進階」。</span><span class="sxs-lookup"><span data-stu-id="3a5d1-210">There are two types of streaming endpoints, **standard** and **premium**.</span></span> <span data-ttu-id="3a5d1-211">如需詳細資訊，請參閱[串流端點概觀](media-services-streaming-endpoints-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="3a5d1-211">For more information, see [Streaming endpoints overview](media-services-streaming-endpoints-overview.md).</span></span>

>[!NOTE]
><span data-ttu-id="3a5d1-212">AMS 帳戶建立時**預設**串流端點就會加入 tooyour 帳戶 hello**已停止**狀態。</span><span class="sxs-lookup"><span data-stu-id="3a5d1-212">When your AMS account is created a **default** streaming endpoint is added tooyour account in hello **Stopped** state.</span></span> <span data-ttu-id="3a5d1-213">串流處理您的內容，並採取利用動態封裝和動態加密，toostart hello 串流端點，您想要從中 toostream 內容已經在 hello toobe**執行**狀態。</span><span class="sxs-lookup"><span data-stu-id="3a5d1-213">toostart streaming your content and take advantage of dynamic packaging and dynamic encryption, hello streaming endpoint from which you want toostream content has toobe in hello **Running** state.</span></span> 

## <a name="known-issues"></a><span data-ttu-id="3a5d1-214">已知問題</span><span class="sxs-lookup"><span data-stu-id="3a5d1-214">Known issues</span></span>
### <a name="changes-toosmooth-streaming-manifest-version"></a><span data-ttu-id="3a5d1-215">變更 tooSmooth Streaming 資訊清單版本</span><span class="sxs-lookup"><span data-stu-id="3a5d1-215">Changes tooSmooth Streaming manifest version</span></span>
<span data-ttu-id="3a5d1-216">在傳回 hello 2016 年 7 月版本更新服務-時所產生的媒體編碼器 Standard、 媒體編碼器高階工作流程或 hello 較早的 Azure 媒體編碼程式使用動態封裝-hello Smooth Streaming 資料流處理的資產資訊清單會符合tooversion 2.0。</span><span class="sxs-lookup"><span data-stu-id="3a5d1-216">Before hello July 2016 service release--when assets produced by Media Encoder Standard, Media Encoder Premium Workflow, or hello earlier Azure Media Encoder were streamed by using dynamic packaging--hello Smooth Streaming manifest returned would conform tooversion 2.0.</span></span> <span data-ttu-id="3a5d1-217">在 2.0 版中，hello 片段期間不要使用 hello 所謂重複 ('r') 標記。</span><span class="sxs-lookup"><span data-stu-id="3a5d1-217">In version 2.0, hello fragment durations do not use hello so-called repeat (‘r’) tags.</span></span> <span data-ttu-id="3a5d1-218">例如：</span><span class="sxs-lookup"><span data-stu-id="3a5d1-218">For example:</span></span>

<?xml version="1.0" encoding="UTF-8"?>
    <SmoothStreamingMedia MajorVersion="2" MinorVersion="0" Duration="8000" TimeScale="1000">
        <StreamIndex Chunks="4" Type="video" Url="QualityLevels({bitrate})/Fragments(video={start time})" QualityLevels="3" Subtype="" Name="video" TimeScale="1000">
            <QualityLevel Index="0" Bitrate="1000000" FourCC="AVC1" MaxWidth="640" MaxHeight="360" CodecPrivateData="00000001674D4029965201405FF2E02A100000030010000003032E0A000F42400040167F18E3050007A12000200B3F8C70ED0B16890000000168EB7352" />
            <c t="0" d="2000" n="0" />
            <c d="2000" />
            <c d="2000" />
            <c d="2000" />
        </StreamIndex>
    </SmoothStreamingMedia>

<span data-ttu-id="3a5d1-219">Hello 2016 年 7 月的服務版本中，在產生 hello Smooth Streaming 資訊清單會搭配使用重複的標記的片段持續時間符合 tooversion 2.2。</span><span class="sxs-lookup"><span data-stu-id="3a5d1-219">In hello July 2016 service release, hello generated Smooth Streaming manifest conforms tooversion 2.2, with fragment durations using repeat tags.</span></span> <span data-ttu-id="3a5d1-220">例如：</span><span class="sxs-lookup"><span data-stu-id="3a5d1-220">For example:</span></span>

    <?xml version="1.0" encoding="UTF-8"?>
    <SmoothStreamingMedia MajorVersion="2" MinorVersion="2" Duration="8000" TimeScale="1000">
        <StreamIndex Chunks="4" Type="video" Url="QualityLevels({bitrate})/Fragments(video={start time})" QualityLevels="3" Subtype="" Name="video" TimeScale="1000">
            <QualityLevel Index="0" Bitrate="1000000" FourCC="AVC1" MaxWidth="640" MaxHeight="360" CodecPrivateData="00000001674D4029965201405FF2E02A100000030010000003032E0A000F42400040167F18E3050007A12000200B3F8C70ED0B16890000000168EB7352" />
            <c t="0" d="2000" r="4" />
        </StreamIndex>
    </SmoothStreamingMedia>

<span data-ttu-id="3a5d1-221">某些 hello 舊版 Smooth Streaming 用戶端可能不支援 hello 重複標記，且將會失敗 tooload hello 資訊清單。</span><span class="sxs-lookup"><span data-stu-id="3a5d1-221">Some of hello legacy Smooth Streaming clients may not support hello repeat tags and will fail tooload hello manifest.</span></span> <span data-ttu-id="3a5d1-222">toomitigate 這個問題，您可以使用 hello 傳統資訊清單的格式參數**(格式 = fmp4 v20)**或更新您的用戶端 toohello 最新版本可支援重複的標記。</span><span class="sxs-lookup"><span data-stu-id="3a5d1-222">toomitigate this issue, you can use hello legacy manifest format parameter **(format=fmp4-v20)** or update your client toohello latest version, which supports repeat tags.</span></span> <span data-ttu-id="3a5d1-223">如需詳細資訊，請參閱 [Smooth Streaming 2.0](media-services-deliver-content-overview.md#fmp4_v20)。</span><span class="sxs-lookup"><span data-stu-id="3a5d1-223">For more information, see [Smooth Streaming 2.0](media-services-deliver-content-overview.md#fmp4_v20).</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="3a5d1-224">媒體服務學習路徑</span><span class="sxs-lookup"><span data-stu-id="3a5d1-224">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="3a5d1-225">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="3a5d1-225">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-topics"></a><span data-ttu-id="3a5d1-226">相關主題</span><span class="sxs-lookup"><span data-stu-id="3a5d1-226">Related topics</span></span>
[<span data-ttu-id="3a5d1-227">啟動儲存體金鑰之後更新媒體服務定位器</span><span class="sxs-lookup"><span data-stu-id="3a5d1-227">Update Media Services locators after rolling storage keys</span></span>](media-services-roll-storage-access-keys.md)

