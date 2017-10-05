---
title: "將內容傳遞給客戶 | Microsoft Docs"
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
ms.openlocfilehash: 46dccd5a50b6dc7c7a93700b8fae554587385031
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="deliver-content-to-customers"></a><span data-ttu-id="35584-103">將內容傳遞給客戶</span><span class="sxs-lookup"><span data-stu-id="35584-103">Deliver content to customers</span></span>
<span data-ttu-id="35584-104">當您將串流或點播視訊內容傳遞給客戶時，您的目標是在不同的網路條件下將高品質的視訊傳遞到各種裝置。</span><span class="sxs-lookup"><span data-stu-id="35584-104">When you're delivering your streaming or video-on-demand content to customers, your goal is to deliver high-quality video to various devices under different network conditions.</span></span>

<span data-ttu-id="35584-105">若要達成此目標，您可以：</span><span class="sxs-lookup"><span data-stu-id="35584-105">To achieve this goal, you can:</span></span>

* <span data-ttu-id="35584-106">將您的串流編碼成多位元速率 (調適性位元速率) 視訊串流。</span><span class="sxs-lookup"><span data-stu-id="35584-106">Encode your stream to a multi-bitrate (adaptive bitrate) video stream.</span></span> <span data-ttu-id="35584-107">這會負責處理品質和網路狀況。</span><span class="sxs-lookup"><span data-stu-id="35584-107">This will take care of quality and network conditions.</span></span>
* <span data-ttu-id="35584-108">使用 Microsoft Azure 媒體服務 [動態封裝](media-services-dynamic-packaging-overview.md) 將串流動態地重新封裝至不同的通訊協定。</span><span class="sxs-lookup"><span data-stu-id="35584-108">Use Microsoft Azure Media Services [dynamic packaging](media-services-dynamic-packaging-overview.md) to dynamically re-package your stream into different protocols.</span></span> <span data-ttu-id="35584-109">這會負責處理不同裝置上的串流處理。</span><span class="sxs-lookup"><span data-stu-id="35584-109">This will take care of streaming on different devices.</span></span> <span data-ttu-id="35584-110">媒體服務支援傳遞下列自適性串流技術：HTTP 即時串流 (HLS)、Smooth Streaming 和 MPEG-DASH。</span><span class="sxs-lookup"><span data-stu-id="35584-110">Media Services supports delivery of the following adaptive bitrate streaming technologies: HTTP Live Streaming (HLS), Smooth Streaming, and MPEG-DASH.</span></span>

>[!NOTE]
><span data-ttu-id="35584-111">建立 AMS 帳戶時，**預設**串流端點會新增至 [已停止] 狀態的帳戶。</span><span class="sxs-lookup"><span data-stu-id="35584-111">When your AMS account is created a **default** streaming endpoint is added to your account in the **Stopped** state.</span></span> <span data-ttu-id="35584-112">若要開始串流內容並利用動態封裝和動態加密功能，您想要串流內容的串流端點必須處於 [執行中] 狀態。</span><span class="sxs-lookup"><span data-stu-id="35584-112">To start streaming your content and take advantage of dynamic packaging and dynamic encryption, the streaming endpoint from which you want to stream content has to be in the **Running** state.</span></span> 

<span data-ttu-id="35584-113">本文提供內容傳遞概念的重要概觀。</span><span class="sxs-lookup"><span data-stu-id="35584-113">This article gives an overview of important content delivery concepts.</span></span>

<span data-ttu-id="35584-114">若要查閱已知問題，請參閱 [已知問題](media-services-deliver-content-overview.md#known-issues)。</span><span class="sxs-lookup"><span data-stu-id="35584-114">To check known issues, see [Known issues](media-services-deliver-content-overview.md#known-issues).</span></span>

## <a name="dynamic-packaging"></a><span data-ttu-id="35584-115">動態封裝</span><span class="sxs-lookup"><span data-stu-id="35584-115">Dynamic packaging</span></span>
<span data-ttu-id="35584-116">媒體服務提供的動態封裝，可讓您以媒體服務支援的串流格式 (MPEG-DASH、HLS、Smooth Streaming) 提供調適性位元速率 MP4 或 Smooth Streaming 編碼內容，而不必重新封裝成這些串流格式。</span><span class="sxs-lookup"><span data-stu-id="35584-116">With the dynamic packaging that Media Services provides, you can deliver your adaptive bitrate MP4 or Smooth Streaming encoded content in streaming formats supported by Media Services (MPEG-DASH, HLS, Smooth Streaming,) without having to re-package into these streaming formats.</span></span> <span data-ttu-id="35584-117">我們建議您利用動態封裝傳遞內容。</span><span class="sxs-lookup"><span data-stu-id="35584-117">We recommend delivering your content with dynamic packaging.</span></span>

<span data-ttu-id="35584-118">若要利用動態封裝功能，您必須將您的夾層 (來源) 檔案編碼成一組調適性位元速率 MP4 檔案或調適性位元速率 Smooth Streaming 檔案。</span><span class="sxs-lookup"><span data-stu-id="35584-118">To take advantage of dynamic packaging, you need to encode your mezzanine (source) file into a set of adaptive-bitrate MP4 files or adaptive bitrate Smooth Streaming files.</span></span>

<span data-ttu-id="35584-119">使用動態封裝，您可以儲存及播放單一儲存格式的檔案。</span><span class="sxs-lookup"><span data-stu-id="35584-119">With dynamic packaging, you store and pay for the files in single storage format.</span></span> <span data-ttu-id="35584-120">媒體服務會根據您的要求建置及傳遞適當的回應。</span><span class="sxs-lookup"><span data-stu-id="35584-120">Media Services will build and serve the appropriate response based on your requests.</span></span>

<span data-ttu-id="35584-121">動態封裝適用於標準和高階串流端點。</span><span class="sxs-lookup"><span data-stu-id="35584-121">Dynamic packaging is available for standard and premium streaming endpoints.</span></span> 

<span data-ttu-id="35584-122">如需詳細資訊，請參閱 [動態封裝](media-services-dynamic-packaging-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="35584-122">For more information, see [Dynamic packaging](media-services-dynamic-packaging-overview.md).</span></span>

## <a name="filters-and-dynamic-manifests"></a><span data-ttu-id="35584-123">篩選器與動態資訊清單</span><span class="sxs-lookup"><span data-stu-id="35584-123">Filters and dynamic manifests</span></span>
<span data-ttu-id="35584-124">您可以使用媒體服務為資產定義篩選器。</span><span class="sxs-lookup"><span data-stu-id="35584-124">You can define filters for your assets with Media Services.</span></span> <span data-ttu-id="35584-125">這些篩選器是伺服器端規則，可協助您的客戶執行如下的動作：播放一段特定視訊，或指定您客戶裝置可以處理的一部分音訊和視訊轉譯 (而非與該資產相關的所有轉譯)。</span><span class="sxs-lookup"><span data-stu-id="35584-125">These filters are server-side rules that help your customers do things like play a specific section of a video or specify a subset of audio and video renditions that your customer's device can handle (instead of all the renditions that are associated with the asset).</span></span> <span data-ttu-id="35584-126">透過當您的客戶要求根據一或多個指定的篩選器來串流視訊時所建立的 *動態資訊清單* ，可達成此篩選。</span><span class="sxs-lookup"><span data-stu-id="35584-126">This filtering is achieved through *dynamic manifests* that are created when your customer requests to stream a video based on one or more specified filters.</span></span>

<span data-ttu-id="35584-127">如需詳細資訊，請參閱 [篩選器與動態資訊清單](media-services-dynamic-manifest-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="35584-127">For more information, see [Filters and dynamic manifests](media-services-dynamic-manifest-overview.md).</span></span>

## <a name="locators"></a><span data-ttu-id="35584-128">定位器</span><span class="sxs-lookup"><span data-stu-id="35584-128">Locators</span></span>
<span data-ttu-id="35584-129">若要提供 URL 給使用者，讓使用者可以利用這個 URL 來串流或下載內容，您必須先建立定位器來發佈您的資產。</span><span class="sxs-lookup"><span data-stu-id="35584-129">To provide your user with a URL that can be used to stream or download your content, you first need to publish your asset by creating a locator.</span></span> <span data-ttu-id="35584-130">定位器提供一個登入點，讓使用者可以存取資產包含的檔案。</span><span class="sxs-lookup"><span data-stu-id="35584-130">A locator provides an entry point to access the files contained in an asset.</span></span> <span data-ttu-id="35584-131">媒體服務支援兩種類型的定位器：</span><span class="sxs-lookup"><span data-stu-id="35584-131">Media Services supports two types of locators:</span></span>

* <span data-ttu-id="35584-132">OnDemandOrigin 定位器。</span><span class="sxs-lookup"><span data-stu-id="35584-132">OnDemandOrigin locators.</span></span> <span data-ttu-id="35584-133">這些定位器可用來串流媒體 (例如，MPEG-DASH、HLS 或 Smooth Streaming) 或漸進式下載檔案。</span><span class="sxs-lookup"><span data-stu-id="35584-133">These are used to stream media (for example, MPEG-DASH, HLS, or Smooth Streaming) or progressively download files.</span></span>
* <span data-ttu-id="35584-134">共用存取簽章 (SAS) URL 定位器。</span><span class="sxs-lookup"><span data-stu-id="35584-134">Shared access signature (SAS) URL locators.</span></span> <span data-ttu-id="35584-135">這些定位器可用來將媒體檔案下載到本機電腦。</span><span class="sxs-lookup"><span data-stu-id="35584-135">These are used to download media files to your local computer.</span></span>

<span data-ttu-id="35584-136">「存取原則」  可用來定義權限 (例如讀取、寫入和列出)，以及用戶端可存取特定資產多久的時間。</span><span class="sxs-lookup"><span data-stu-id="35584-136">An *access policy* is used to define the permissions (such as read, write, and list) and duration for which a client has access for a particular asset.</span></span> <span data-ttu-id="35584-137">請注意，建立 OrDemandOrigin 定位器時，不應使用列出權限 (AccessPermissions.List)。</span><span class="sxs-lookup"><span data-stu-id="35584-137">Note that the list permission (AccessPermissions.List) should not be used in creating an OrDemandOrigin locator.</span></span>

<span data-ttu-id="35584-138">定位器有到期日。</span><span class="sxs-lookup"><span data-stu-id="35584-138">Locators have expiration dates.</span></span> <span data-ttu-id="35584-139">Azure 入口網站會為定位器設定 100 年後的到期日。</span><span class="sxs-lookup"><span data-stu-id="35584-139">The Azure portal sets an expiration date 100 years in the future for locators.</span></span>

> [!NOTE]
> <span data-ttu-id="35584-140">如果您在 2015 年 3 月之前使用 Azure 入口網站建立定位器，這些定位器已設定為兩年之後到期。</span><span class="sxs-lookup"><span data-stu-id="35584-140">If you used the Azure portal to create locators before March 2015, those locators were set to expire after two years.</span></span>
> 
> 

<span data-ttu-id="35584-141">若要更新定位器的到期日，請使用 [REST](https://docs.microsoft.com/rest/api/media/operations/locator#update_a_locator) 或 [.NET](http://go.microsoft.com/fwlink/?LinkID=533259) API。</span><span class="sxs-lookup"><span data-stu-id="35584-141">To update an expiration date on a locator, use [REST](https://docs.microsoft.com/rest/api/media/operations/locator#update_a_locator) or [.NET](http://go.microsoft.com/fwlink/?LinkID=533259) APIs.</span></span> <span data-ttu-id="35584-142">請注意，當您更新 SAS 定位器的到期日，URL 也會隨之變更。</span><span class="sxs-lookup"><span data-stu-id="35584-142">Note that when you update the expiration date of a SAS locator, the URL changes.</span></span>

<span data-ttu-id="35584-143">定位器並不是用來控制每個使用者的權限。</span><span class="sxs-lookup"><span data-stu-id="35584-143">Locators are not designed to manage per-user access control.</span></span> <span data-ttu-id="35584-144">您可以使用數位版權管理 (DRM) 方案，給予個別使用者不同的存取權限。</span><span class="sxs-lookup"><span data-stu-id="35584-144">You can give different access rights to individual users by using Digital Rights Management (DRM) solutions.</span></span> <span data-ttu-id="35584-145">如需詳細資訊，請參閱 [保護媒體](http://msdn.microsoft.com/library/azure/dn282272.aspx)。</span><span class="sxs-lookup"><span data-stu-id="35584-145">For more information, see [Securing Media](http://msdn.microsoft.com/library/azure/dn282272.aspx).</span></span>

<span data-ttu-id="35584-146">建立定位器時，由於 Azure 儲存體需要執行一些儲存體和傳播程序，因此有時候會延遲 30 秒的時間。</span><span class="sxs-lookup"><span data-stu-id="35584-146">When you create a locator, there may be a 30-second delay due to required storage and propagation processes in Azure Storage.</span></span>

## <a name="adaptive-streaming"></a><span data-ttu-id="35584-147">調適性串流處理</span><span class="sxs-lookup"><span data-stu-id="35584-147">Adaptive streaming</span></span>
<span data-ttu-id="35584-148">調適性位元速率技術可讓視訊播放器應用程式判斷網路狀況，並由數種位元速率中進行選擇。</span><span class="sxs-lookup"><span data-stu-id="35584-148">Adaptive bitrate technologies allow video player applications to determine network conditions and select from several bitrates.</span></span> <span data-ttu-id="35584-149">當網路通訊降級時，用戶端可以選取較低的位元速率，讓播放能夠以較低的視訊品質繼續。</span><span class="sxs-lookup"><span data-stu-id="35584-149">When network communication degrades, the client can select a lower bitrate so playback can continue with lower video quality.</span></span> <span data-ttu-id="35584-150">當網路狀況改善時，用戶端可以切換至較高的位元速率，以提高視訊品質。</span><span class="sxs-lookup"><span data-stu-id="35584-150">As network conditions improve, the client can switch to a higher bitrate with improved video quality.</span></span> <span data-ttu-id="35584-151">Azure 媒體服務支援下列調適性位元速率技術：HTTP 即時串流 (HLS)、Smooth Streaming 和 MPEG-DASH。</span><span class="sxs-lookup"><span data-stu-id="35584-151">Azure Media Services supports the following adaptive bitrate technologies: HTTP Live Streaming (HLS), Smooth Streaming, and MPEG-DASH.</span></span>

<span data-ttu-id="35584-152">若要提供漸進式下載 URL 給使用者，您必須先建立 OnDemandOrigin 定位器。</span><span class="sxs-lookup"><span data-stu-id="35584-152">To provide users with streaming URLs, you first must create an OnDemandOrigin locator.</span></span> <span data-ttu-id="35584-153">建立定位器可針對包含您要串流之內容的資產，提供其基底路徑。</span><span class="sxs-lookup"><span data-stu-id="35584-153">Creating the locator gives you the base path to the asset that contains the content you want to stream.</span></span> <span data-ttu-id="35584-154">不過，若要能夠串流此內容，您還需要進一步修改此路徑。</span><span class="sxs-lookup"><span data-stu-id="35584-154">However, to be able to stream this content, you need to modify this path further.</span></span> <span data-ttu-id="35584-155">若要建構串流資訊清單檔案的完整 URL，您必須串連定位器的路徑值和資訊清單 (filename.ism) 的檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="35584-155">To construct a full URL to the streaming manifest file, you must concatenate the locator’s path value and the manifest (filename.ism) file name.</span></span> <span data-ttu-id="35584-156">接著，在定位器路徑後面附加 **/Manifest** 和適當的格式 (如果需要)。</span><span class="sxs-lookup"><span data-stu-id="35584-156">Then append **/Manifest** and an appropriate format (if needed) to the locator path.</span></span>

> [!NOTE]
> <span data-ttu-id="35584-157">您也可以透過 SSL 連線串流您的內容。</span><span class="sxs-lookup"><span data-stu-id="35584-157">You can also stream your content over an SSL connection.</span></span> <span data-ttu-id="35584-158">若要這樣做，請確定您的串流 URL 以 HTTPS 開頭。</span><span class="sxs-lookup"><span data-stu-id="35584-158">To do this, make sure your streaming URLs start with HTTPS.</span></span> <span data-ttu-id="35584-159">請注意，目前 AMS 不支援使用 SSL 搭配自訂網域。</span><span class="sxs-lookup"><span data-stu-id="35584-159">Note that, currently, AMS doesn’t support SSL with custom domains.</span></span>  
> 


<span data-ttu-id="35584-160">只有當您傳遞內容的來源串流端點是在 2014 年 9 月 10 日之後建立時，才能透過 SSL 串流。</span><span class="sxs-lookup"><span data-stu-id="35584-160">You can only stream over SSL if the streaming endpoint from which you deliver your content was created after September 10th, 2014.</span></span> <span data-ttu-id="35584-161">如果您的串流 URL 是根據 2014 年 9 月 10 日之後建立的串流端點，則 URL 會包含 "streaming.mediaservices.windows.net"。</span><span class="sxs-lookup"><span data-stu-id="35584-161">If your streaming URLs are based on the streaming endpoints created after September 10th, 2014, the URL contains “streaming.mediaservices.windows.net.”</span></span> <span data-ttu-id="35584-162">包含 "origin.mediaservices.windows.net" (舊格式) 的串流 URL 不支援 SSL。</span><span class="sxs-lookup"><span data-stu-id="35584-162">Streaming URLs that contain “origin.mediaservices.windows.net” (the old format) do not support SSL.</span></span> <span data-ttu-id="35584-163">如果您的 URL 是舊格式，而且您希望能夠透過 SSL 串流，請建立新的串流端點。</span><span class="sxs-lookup"><span data-stu-id="35584-163">If your URL is in the old format and you want to be able to stream over SSL, create a new streaming endpoint.</span></span> <span data-ttu-id="35584-164">使用根據新的串流端點的 URL，透過 SSL 串流內容。</span><span class="sxs-lookup"><span data-stu-id="35584-164">Use URLs based on the new streaming endpoint to stream your content over SSL.</span></span>

## <a name="streaming-url-formats"></a><span data-ttu-id="35584-165">Streaming URL 格式</span><span class="sxs-lookup"><span data-stu-id="35584-165">Streaming URL formats</span></span>
### <a name="mpeg-dash-format"></a><span data-ttu-id="35584-166">MPEG-DASH 格式</span><span class="sxs-lookup"><span data-stu-id="35584-166">MPEG-DASH format</span></span>
<span data-ttu-id="35584-167">{串流端點名稱-媒體服務帳戶名稱}.streaming.mediaservices.windows.net/{定位器識別碼}/{檔案名稱}.ism/Manifest(format=mpd-time-csf)</span><span class="sxs-lookup"><span data-stu-id="35584-167">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=mpd-time-csf)</span></span>

<span data-ttu-id="35584-168">http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=mpd-time-csf)</span><span class="sxs-lookup"><span data-stu-id="35584-168">http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=mpd-time-csf)</span></span>

### <a name="apple-http-live-streaming-hls-v4-format"></a><span data-ttu-id="35584-169">Apple HTTP Live Streaming (HLS) V4 格式</span><span class="sxs-lookup"><span data-stu-id="35584-169">Apple HTTP Live Streaming (HLS) V4 format</span></span>
<span data-ttu-id="35584-170">{串流端點名稱-媒體服務帳戶名稱}.streaming.mediaservices.windows.net/{定位器識別碼}/{檔案名稱}.ism/Manifest(format=m3u8-aapl)</span><span class="sxs-lookup"><span data-stu-id="35584-170">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=m3u8-aapl)</span></span>

<span data-ttu-id="35584-171">http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=m3u8-aapl)</span><span class="sxs-lookup"><span data-stu-id="35584-171">http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=m3u8-aapl)</span></span>

### <a name="apple-http-live-streaming-hls-v3-format"></a><span data-ttu-id="35584-172">Apple HTTP Live Streaming (HLS) V3 格式</span><span class="sxs-lookup"><span data-stu-id="35584-172">Apple HTTP Live Streaming (HLS) V3 format</span></span>
<span data-ttu-id="35584-173">{串流端點名稱-媒體服務帳戶名稱}.streaming.mediaservices.windows.net/{定位器識別碼}/{檔案名稱}.ism/Manifest(format=m3u8-aapl-v3)</span><span class="sxs-lookup"><span data-stu-id="35584-173">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=m3u8-aapl-v3)</span></span>

<span data-ttu-id="35584-174">http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=m3u8-aapl-v3)</span><span class="sxs-lookup"><span data-stu-id="35584-174">http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=m3u8-aapl-v3)</span></span>

### <a name="apple-http-live-streaming-hls-format-with-audio-only-filter"></a><span data-ttu-id="35584-175">Apple HTTP Live Streaming (HLS) 格式搭配僅限音訊的篩選條件</span><span class="sxs-lookup"><span data-stu-id="35584-175">Apple HTTP Live Streaming (HLS) format with audio-only filter</span></span>
<span data-ttu-id="35584-176">根據預設，只有音訊的播放軌是包含在 HLS 資訊清單中。</span><span class="sxs-lookup"><span data-stu-id="35584-176">By default, audio-only tracks are included in the HLS manifest.</span></span> <span data-ttu-id="35584-177">這對於行動電話通訊網路的 Apple Store 認證是必要條件。</span><span class="sxs-lookup"><span data-stu-id="35584-177">This is required for Apple Store certification for cellular networks.</span></span> <span data-ttu-id="35584-178">在此情況下，如果用戶端沒有足夠的頻寬，或透過 2G 網路連線，播放就會切換成只有音訊。</span><span class="sxs-lookup"><span data-stu-id="35584-178">In this case, if a client doesn’t have sufficient bandwidth or is connected over a 2G connection, playback switches to audio-only.</span></span> <span data-ttu-id="35584-179">這可協助保護內容串流，而不需要緩衝處理，但是沒有視訊。</span><span class="sxs-lookup"><span data-stu-id="35584-179">This helps to keep content streaming without buffering, but there is no video.</span></span> <span data-ttu-id="35584-180">在某些情況中，播放程式緩衝處理可能比只有音訊更好。</span><span class="sxs-lookup"><span data-stu-id="35584-180">In some scenarios, player buffering might be preferred over audio-only.</span></span> <span data-ttu-id="35584-181">如果您想要移除只有音訊的播放軌，可以將 **audio-only=false** 加入 URL。</span><span class="sxs-lookup"><span data-stu-id="35584-181">If you want to remove the audio-only track, add **audio-only=false** to the URL.</span></span>

<span data-ttu-id="35584-182">http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=m3u8-aapl-v3,audio-only=false)</span><span class="sxs-lookup"><span data-stu-id="35584-182">http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=m3u8-aapl-v3,audio-only=false)</span></span>

<span data-ttu-id="35584-183">如需詳細資訊，請參閱 [Dynamic Manifest Composition support and HLS output additional features (動態資訊清單組合支援和 HLS 輸出額外功能)](https://azure.microsoft.com/blog/azure-media-services-release-dynamic-manifest-composition-remove-hls-audio-only-track-and-hls-i-frame-track-support/)。</span><span class="sxs-lookup"><span data-stu-id="35584-183">For more information, see [Dynamic Manifest Composition support and HLS output additional features](https://azure.microsoft.com/blog/azure-media-services-release-dynamic-manifest-composition-remove-hls-audio-only-track-and-hls-i-frame-track-support/).</span></span>

### <a name="smooth-streaming-format"></a><span data-ttu-id="35584-184">Smooth Streaming 格式</span><span class="sxs-lookup"><span data-stu-id="35584-184">Smooth Streaming format</span></span>
<span data-ttu-id="35584-185">{串流端點名稱-媒體服務帳戶名稱}.streaming.mediaservices.windows.net/{定位器識別碼}/{檔案名稱}.ism/Manifest</span><span class="sxs-lookup"><span data-stu-id="35584-185">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest</span></span>

<span data-ttu-id="35584-186">範例：</span><span class="sxs-lookup"><span data-stu-id="35584-186">Example:</span></span>

<span data-ttu-id="35584-187">http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest</span><span class="sxs-lookup"><span data-stu-id="35584-187">http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest</span></span>

### <span data-ttu-id="35584-188"><a id="fmp4_v20"></a>Smooth Streaming 2.0 資訊清單 (舊版資訊清單)</span><span class="sxs-lookup"><span data-stu-id="35584-188"><a id="fmp4_v20"></a>Smooth Streaming 2.0 manifest (legacy manifest)</span></span>
<span data-ttu-id="35584-189">根據預設，Smooth Streaming 資訊清單格式包含重複的標記 (r-tag)。</span><span class="sxs-lookup"><span data-stu-id="35584-189">By default, Smooth Streaming manifest format contains the repeat tag (r-tag).</span></span> <span data-ttu-id="35584-190">不過，有些播放程式不支援 r-tag。</span><span class="sxs-lookup"><span data-stu-id="35584-190">However, some players do not support the r-tag.</span></span> <span data-ttu-id="35584-191">使用這些播放程式的用戶端可以使用停用 r-tag 的格式︰</span><span class="sxs-lookup"><span data-stu-id="35584-191">Clients with these players can use a format that disables the r-tag:</span></span>

<span data-ttu-id="35584-192">{串流端點名稱-媒體服務帳戶名稱}.streaming.mediaservices.windows.net/{定位器識別碼}/{檔案名稱}.ism/Manifest(format=fmp4-v20)</span><span class="sxs-lookup"><span data-stu-id="35584-192">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=fmp4-v20)</span></span>

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=fmp4-v20)

## <a name="progressive-download"></a><span data-ttu-id="35584-193">漸進式下載</span><span class="sxs-lookup"><span data-stu-id="35584-193">Progressive download</span></span>
<span data-ttu-id="35584-194">使用漸進式下載可以在下載完整檔案前就開始播放媒體。</span><span class="sxs-lookup"><span data-stu-id="35584-194">With progressive download, you can start playing media before the entire file has been downloaded.</span></span> <span data-ttu-id="35584-195">您無法漸進式下載 .ism* (ismv、isma、ismt 或 ismc) 檔案。</span><span class="sxs-lookup"><span data-stu-id="35584-195">You cannot progressively download .ism* (ismv, isma, ismt, or ismc) files.</span></span>

<span data-ttu-id="35584-196">若要漸進式下載內容，請使用 OnDemandOrigin 類型的定位器。</span><span class="sxs-lookup"><span data-stu-id="35584-196">To progressively download content, use the OnDemandOrigin type of locator.</span></span> <span data-ttu-id="35584-197">下列範例顯示的 URL 採用的是 OnDemandOrigin 類型的定位器：</span><span class="sxs-lookup"><span data-stu-id="35584-197">The following example shows the URL that is based on the OnDemandOrigin type of locator:</span></span>

    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny_H264_650kbps_AAC_und_ch2_96kbps.mp4

<span data-ttu-id="35584-198">您必須解密任何您想要從原始服務串流的儲存體加密資產，這樣才能漸進式下載。</span><span class="sxs-lookup"><span data-stu-id="35584-198">You must decrypt any storage-encrypted assets that you want to stream from the origin service for progressive download.</span></span>

## <a name="download"></a><span data-ttu-id="35584-199">下載</span><span class="sxs-lookup"><span data-stu-id="35584-199">Download</span></span>
<span data-ttu-id="35584-200">若要將您的內容下載到用戶端裝置，您必須建立一個 SAS 定位器。</span><span class="sxs-lookup"><span data-stu-id="35584-200">To download your content to a client device, you must create a SAS Locator.</span></span> <span data-ttu-id="35584-201">您可以利用 SAS 定位器存取檔案所在的 Azure 儲存體容器。</span><span class="sxs-lookup"><span data-stu-id="35584-201">The SAS locator gives you access to the Azure Storage container where your file is located.</span></span> <span data-ttu-id="35584-202">若要建立下載 URL，您必須將檔案名稱內嵌在主機與 SAS 簽章之間。</span><span class="sxs-lookup"><span data-stu-id="35584-202">To build the download URL, you have to embed the file name between the host and SAS signature.</span></span>

<span data-ttu-id="35584-203">下列範例顯示的 URL 是採用 SAS 定位器：</span><span class="sxs-lookup"><span data-stu-id="35584-203">The following example shows the URL that is based on the SAS locator:</span></span>

    https://test001.blob.core.windows.net/asset-ca7a4c3f-9eb5-4fd8-a898-459cb17761bd/BigBuckBunny.mp4?sv=2012-02-12&se=2014-05-03T01%3A23%3A50Z&sr=c&si=7c093e7c-7dab-45b4-beb4-2bfdff764bb5&sig=msEHP90c6JHXEOtTyIWqD7xio91GtVg0UIzjdpFscHk%3D

<span data-ttu-id="35584-204">您必須考量下列事項：</span><span class="sxs-lookup"><span data-stu-id="35584-204">The following considerations apply:</span></span>

* <span data-ttu-id="35584-205">您必須解密任何您想要從原始服務串流的儲存體加密資產，這樣才能漸進式下載。</span><span class="sxs-lookup"><span data-stu-id="35584-205">You must decrypt any storage-encrypted assets that you want to stream from the origin service for progressive download.</span></span>
* <span data-ttu-id="35584-206">未在 12 小時內完成的下載，最後一定會失敗。</span><span class="sxs-lookup"><span data-stu-id="35584-206">A download that has not finished within 12 hours will fail.</span></span>

## <a name="streaming-endpoints"></a><span data-ttu-id="35584-207">串流端點</span><span class="sxs-lookup"><span data-stu-id="35584-207">Streaming endpoints</span></span>

<span data-ttu-id="35584-208">串流端點代表可以直接將內容傳遞給用戶端播放程式應用程式，或傳遞給內容傳遞網路 (CDN) 進行進一步發佈的串流服務。</span><span class="sxs-lookup"><span data-stu-id="35584-208">A streaming endpoint represents a streaming service that can deliver content directly to a client player application or to a content delivery network (CDN) for further distribution.</span></span> <span data-ttu-id="35584-209">來自串流端點服務的輸出串流可以是即時資料流，或媒體服務帳戶中的隨選視訊資產。</span><span class="sxs-lookup"><span data-stu-id="35584-209">The outbound stream from a streaming endpoint service can be a live stream or a video-on-demand asset in your Media Services account.</span></span> <span data-ttu-id="35584-210">串流端點有兩種類型：「標準」和「進階」。</span><span class="sxs-lookup"><span data-stu-id="35584-210">There are two types of streaming endpoints, **standard** and **premium**.</span></span> <span data-ttu-id="35584-211">如需詳細資訊，請參閱[串流端點概觀](media-services-streaming-endpoints-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="35584-211">For more information, see [Streaming endpoints overview](media-services-streaming-endpoints-overview.md).</span></span>

>[!NOTE]
><span data-ttu-id="35584-212">建立 AMS 帳戶時，**預設**串流端點會新增至 [已停止] 狀態的帳戶。</span><span class="sxs-lookup"><span data-stu-id="35584-212">When your AMS account is created a **default** streaming endpoint is added to your account in the **Stopped** state.</span></span> <span data-ttu-id="35584-213">若要開始串流內容並利用動態封裝和動態加密功能，您想要串流內容的串流端點必須處於 [執行中] 狀態。</span><span class="sxs-lookup"><span data-stu-id="35584-213">To start streaming your content and take advantage of dynamic packaging and dynamic encryption, the streaming endpoint from which you want to stream content has to be in the **Running** state.</span></span> 

## <a name="known-issues"></a><span data-ttu-id="35584-214">已知問題</span><span class="sxs-lookup"><span data-stu-id="35584-214">Known issues</span></span>
### <a name="changes-to-smooth-streaming-manifest-version"></a><span data-ttu-id="35584-215">Smooth Streaming 資訊清單版本變更</span><span class="sxs-lookup"><span data-stu-id="35584-215">Changes to Smooth Streaming manifest version</span></span>
<span data-ttu-id="35584-216">在 2016 年 7 月之前的服務版本 -- 使用動態封裝串流媒體編碼器標準、媒體編碼器高階工作流程或舊版 Azure 媒體編碼器所產生的資產時 -- 傳回的 Smooth Streaming 資訊清單會符合 2.0 版。</span><span class="sxs-lookup"><span data-stu-id="35584-216">Before the July 2016 service release--when assets produced by Media Encoder Standard, Media Encoder Premium Workflow, or the earlier Azure Media Encoder were streamed by using dynamic packaging--the Smooth Streaming manifest returned would conform to version 2.0.</span></span> <span data-ttu-id="35584-217">在 2.0 版中，片段持續期間不使用所謂的重複 ('r') 標籤。</span><span class="sxs-lookup"><span data-stu-id="35584-217">In version 2.0, the fragment durations do not use the so-called repeat (‘r’) tags.</span></span> <span data-ttu-id="35584-218">例如：</span><span class="sxs-lookup"><span data-stu-id="35584-218">For example:</span></span>

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

<span data-ttu-id="35584-219">在 2016 年 7 月之後的服務版本中，產生的 Smooth Streaming 資訊清單會符合 2.2 版，即片段持續時間使用重複標籤。</span><span class="sxs-lookup"><span data-stu-id="35584-219">In the July 2016 service release, the generated Smooth Streaming manifest conforms to version 2.2, with fragment durations using repeat tags.</span></span> <span data-ttu-id="35584-220">例如：</span><span class="sxs-lookup"><span data-stu-id="35584-220">For example:</span></span>

    <?xml version="1.0" encoding="UTF-8"?>
    <SmoothStreamingMedia MajorVersion="2" MinorVersion="2" Duration="8000" TimeScale="1000">
        <StreamIndex Chunks="4" Type="video" Url="QualityLevels({bitrate})/Fragments(video={start time})" QualityLevels="3" Subtype="" Name="video" TimeScale="1000">
            <QualityLevel Index="0" Bitrate="1000000" FourCC="AVC1" MaxWidth="640" MaxHeight="360" CodecPrivateData="00000001674D4029965201405FF2E02A100000030010000003032E0A000F42400040167F18E3050007A12000200B3F8C70ED0B16890000000168EB7352" />
            <c t="0" d="2000" r="4" />
        </StreamIndex>
    </SmoothStreamingMedia>

<span data-ttu-id="35584-221">某些舊版的 Smooth Streaming 用戶端可能不支援重複標籤，因此將無法載入資訊清單。</span><span class="sxs-lookup"><span data-stu-id="35584-221">Some of the legacy Smooth Streaming clients may not support the repeat tags and will fail to load the manifest.</span></span> <span data-ttu-id="35584-222">若要解決這個問題，您可以使用舊版資訊清單格式參數 **(format=fmp4-v20)** ，或將用戶端更新為支援重複標籤的最新版本。</span><span class="sxs-lookup"><span data-stu-id="35584-222">To mitigate this issue, you can use the legacy manifest format parameter **(format=fmp4-v20)** or update your client to the latest version, which supports repeat tags.</span></span> <span data-ttu-id="35584-223">如需詳細資訊，請參閱 [Smooth Streaming 2.0](media-services-deliver-content-overview.md#fmp4_v20)。</span><span class="sxs-lookup"><span data-stu-id="35584-223">For more information, see [Smooth Streaming 2.0](media-services-deliver-content-overview.md#fmp4_v20).</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="35584-224">媒體服務學習路徑</span><span class="sxs-lookup"><span data-stu-id="35584-224">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="35584-225">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="35584-225">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-topics"></a><span data-ttu-id="35584-226">相關主題</span><span class="sxs-lookup"><span data-stu-id="35584-226">Related topics</span></span>
[<span data-ttu-id="35584-227">啟動儲存體金鑰之後更新媒體服務定位器</span><span class="sxs-lookup"><span data-stu-id="35584-227">Update Media Services locators after rolling storage keys</span></span>](media-services-roll-storage-access-keys.md)

