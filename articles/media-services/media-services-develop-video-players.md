---
title: "開發視訊播放器應用程式"
description: "本主題會提供 Player Framework 和外掛程式的連結，可讓您開發自己的用戶端應用程式，以使用來自媒體服務的串流媒體。"
author: Juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: 55e419fc-4c39-4902-9c62-f41cfcd86c6c
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: juliako
ms.openlocfilehash: 0e88baed8188890e80d4c2e7ee9d510fdabf6e43
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="develop-video-player-applications"></a><span data-ttu-id="fbafb-103">開發視訊播放器應用程式</span><span class="sxs-lookup"><span data-stu-id="fbafb-103">Develop video player applications</span></span>
## <a name="overview"></a><span data-ttu-id="fbafb-104">Overview</span><span class="sxs-lookup"><span data-stu-id="fbafb-104">Overview</span></span>
<span data-ttu-id="fbafb-105">Azure 媒體服務提供一些工具，供您用來建立適用於大部分平台的豐富、動態用戶端播放器應用程式，此處所述的平台包括：iOS 裝置、Android 裝置、Windows、Windows Phone、Xbox 和機上盒。</span><span class="sxs-lookup"><span data-stu-id="fbafb-105">Azure Media Services provides the tools you need to create rich, dynamic client player applications for most platforms including: iOS Devices, Android Devices, Windows, Windows Phone, Xbox, and Set-top boxes.</span></span> <span data-ttu-id="fbafb-106">本主題也會提供 SDK 和 Player Framework 連結，可讓您開發自己的用戶端應用程式，使用來自 Azure 媒體服務的串流媒體。</span><span class="sxs-lookup"><span data-stu-id="fbafb-106">This topic also provides links to SDKs and Player Frameworks that you can use to develop your own client applications that can consume streaming media from Azure Media Services.</span></span>

>[!NOTE]
><span data-ttu-id="fbafb-107">建立 AMS 帳戶時，**預設**串流端點會新增至 [已停止] 狀態的帳戶。</span><span class="sxs-lookup"><span data-stu-id="fbafb-107">When your AMS account is created a **default** streaming endpoint is added to your account in the **Stopped** state.</span></span> <span data-ttu-id="fbafb-108">若要開始串流內容並利用動態封裝和動態加密功能，您想要串流內容的串流端點必須處於 [執行中] 狀態。</span><span class="sxs-lookup"><span data-stu-id="fbafb-108">To start streaming your content and take advantage of dynamic packaging and dynamic encryption, the streaming endpoint from which you want to stream content has to be in the **Running** state.</span></span> 
 
## <a name="azure-media-player"></a><span data-ttu-id="fbafb-109">Azure Media Player</span><span class="sxs-lookup"><span data-stu-id="fbafb-109">Azure Media Player</span></span>
<span data-ttu-id="fbafb-110">[Azure 媒體播放器](http://aka.ms/ampinfo) 是一款網頁視訊播放器，可以在各種瀏覽器和裝置上播放 Microsoft Azure 媒體服務的媒體內容。</span><span class="sxs-lookup"><span data-stu-id="fbafb-110">[Azure Media Player](http://aka.ms/ampinfo) is a web video player built to play back media content from Microsoft Azure Media Services on a wide variety of browsers and devices.</span></span> <span data-ttu-id="fbafb-111">Azure Media Player 採用業界標準，例如 HTML5、媒體來源延伸模組 (MSE) 和加密媒體擴充功能 (EME)，提供豐富的調適性串流體驗。</span><span class="sxs-lookup"><span data-stu-id="fbafb-111">Azure Media Player utilizes industry standards, such as HTML5, Media Source Extensions (MSE), and Encrypted Media Extensions (EME) to provide an enriched adaptive streaming experience.</span></span> <span data-ttu-id="fbafb-112">無法在裝置或瀏覽器使用這些標準時，Azure Media Player 則會使用 Flash 和 Silverlight 做為後援技術。</span><span class="sxs-lookup"><span data-stu-id="fbafb-112">When these standards are not available on a device or in a browser, Azure Media Player uses Flash and Silverlight as fallback technology.</span></span> <span data-ttu-id="fbafb-113">不論使用何種播放技術，開發人員都會有統一的 JavaScript 介面來存取應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="fbafb-113">Regardless of the playback technology used, developers will have a unified JavaScript interface to access APIs.</span></span> <span data-ttu-id="fbafb-114">這樣我們就可以在各種裝置和瀏覽器上順利播放 Azure 媒體服務提供的內容。</span><span class="sxs-lookup"><span data-stu-id="fbafb-114">This allows for content served by Azure Media Services to be played across a wide-range of devices and browsers without any extra effort.</span></span>

<span data-ttu-id="fbafb-115">我們可以利用 Microsoft Azure 媒體服務播放 DASH、Smooth Streaming 和 HLS 資料流等格式的內容。</span><span class="sxs-lookup"><span data-stu-id="fbafb-115">Microsoft Azure Media Services allows for content to be served up with DASH, Smooth Streaming, and HLS streaming formats to play back content.</span></span> <span data-ttu-id="fbafb-116">Azure Media Player 會考量這些不同的格式，並根據平台/瀏覽器功能自動播放最合適的連結。</span><span class="sxs-lookup"><span data-stu-id="fbafb-116">Azure Media Player takes into account these various formats and automatically plays the best link based on the platform/browser capabilities.</span></span> <span data-ttu-id="fbafb-117">Microsoft Azure 媒體服務也允許利用 PlayReady 加密或 AES 128 位元信封加密，進行資產的動態加密。</span><span class="sxs-lookup"><span data-stu-id="fbafb-117">Microsoft Azure Media Services also allows for dynamic encryption of assets with PlayReady encryption or AES-128 bit envelope encryption.</span></span> <span data-ttu-id="fbafb-118">只要設定正確，Azure Media Player 允許解密 PlayReady 和 AES 128 位元加密的內容。</span><span class="sxs-lookup"><span data-stu-id="fbafb-118">Azure Media Player allows for decryption of PlayReady and AES-128 bit encrypted content when appropriately configured.</span></span> 

<span data-ttu-id="fbafb-119">其他資訊：</span><span class="sxs-lookup"><span data-stu-id="fbafb-119">For more information:</span></span>

* [<span data-ttu-id="fbafb-120">Azure Media Player</span><span class="sxs-lookup"><span data-stu-id="fbafb-120">Azure Media Player</span></span>](http://aka.ms/ampinfo)
* [<span data-ttu-id="fbafb-121">Azure Media Player 文件</span><span class="sxs-lookup"><span data-stu-id="fbafb-121">Azure Media Player Documentation</span></span>](http://aka.ms/ampdocs) 
* [<span data-ttu-id="fbafb-122">Azure Media Player 開始使用部落格</span><span class="sxs-lookup"><span data-stu-id="fbafb-122">Azure Media Player Getting Started Blog</span></span>](https://azure.microsoft.com/blog/2015/04/15/announcing-azure-media-player/)
* [<span data-ttu-id="fbafb-123">註冊以持續收到 Azure Media Player 的最新消息</span><span class="sxs-lookup"><span data-stu-id="fbafb-123">Sign up to stay up to date with the latest from Azure Media Player</span></span>](http://aka.ms/ampsignup)
* [<span data-ttu-id="fbafb-124">新增功能要求、概念和意見反應</span><span class="sxs-lookup"><span data-stu-id="fbafb-124">Add new feature requests, ideas, feedback</span></span>](http://aka.ms/ampuservoice) 

## <a name="other-tools-for-creating-player-applications"></a><span data-ttu-id="fbafb-125">其他可用來建立播放器應用程式的工具</span><span class="sxs-lookup"><span data-stu-id="fbafb-125">Other Tools for Creating Player Applications</span></span>
<span data-ttu-id="fbafb-126">您也可以使用任何下列 SDK：</span><span class="sxs-lookup"><span data-stu-id="fbafb-126">You can also use any of the following SDKs:</span></span>

* [<span data-ttu-id="fbafb-127">Smooth Streaming Client SDK</span><span class="sxs-lookup"><span data-stu-id="fbafb-127">Smooth Streaming Client SDK</span></span>](http://www.iis.net/downloads/microsoft/smooth-streaming) 
* [<span data-ttu-id="fbafb-128">Smooth Streaming Windows 市集應用程式</span><span class="sxs-lookup"><span data-stu-id="fbafb-128">Smooth Streaming Windows Store App</span></span>](media-services-build-smooth-streaming-apps.md)
* [<span data-ttu-id="fbafb-129">Microsoft 媒體平台：Player Framework</span><span class="sxs-lookup"><span data-stu-id="fbafb-129">Microsoft Media Platform: Player Framework</span></span>](http://playerframework.codeplex.com/) 
* [<span data-ttu-id="fbafb-130">HTML5 Player Framework 文件</span><span class="sxs-lookup"><span data-stu-id="fbafb-130">HTML5 Player Framework Documentation</span></span>](http://playerframework.codeplex.com/wikipage?title=HTML5%20Player&referringTitle=Documentation) 
* [<span data-ttu-id="fbafb-131">Microsoft Smooth Streaming Plugin for OSMF</span><span class="sxs-lookup"><span data-stu-id="fbafb-131">Microsoft Smooth Streaming Plugin for OSMF</span></span>](https://www.microsoft.com/download/details.aspx?id=36057) 
* [<span data-ttu-id="fbafb-132">Licensing Microsoft® Smooth Streaming Client Porting Kit</span><span class="sxs-lookup"><span data-stu-id="fbafb-132">Licensing Microsoft® Smooth Streaming Client Porting Kit</span></span>](http://aka.ms/sspk) 
* [<span data-ttu-id="fbafb-133">XBOX Video Application Development</span><span class="sxs-lookup"><span data-stu-id="fbafb-133">XBOX Video Application Development</span></span>](http://xbox.create.msdn.com/) 

## <a name="advertising"></a><span data-ttu-id="fbafb-134">廣告</span><span class="sxs-lookup"><span data-stu-id="fbafb-134">Advertising</span></span>
<span data-ttu-id="fbafb-135">Azure 媒體服務允許透過 Windows Media 平台插入廣告：Player Framework。</span><span class="sxs-lookup"><span data-stu-id="fbafb-135">Azure Media Services provides support for ad insertion through the Windows Media Platform: Player Frameworks.</span></span> <span data-ttu-id="fbafb-136">具備廣告支援的播放器架構都適用於 Windows 8、Silverlight、Windows Phone 8 和 iOS 裝置。</span><span class="sxs-lookup"><span data-stu-id="fbafb-136">Player frameworks with ad support are available for Windows 8, Silverlight, Windows Phone 8, and iOS devices.</span></span> <span data-ttu-id="fbafb-137">每一個播放器架構都有範例程式碼，教您如何實作播放器應用程式。</span><span class="sxs-lookup"><span data-stu-id="fbafb-137">Each player framework contains sample code that shows you how to implement a player application.</span></span> <span data-ttu-id="fbafb-138">目前有三種不同的廣告可以插入媒體中：</span><span class="sxs-lookup"><span data-stu-id="fbafb-138">There are three different kinds of ads you can insert into your media:</span></span>

<span data-ttu-id="fbafb-139">線性 – 可暫停主要影片的完整框架廣告</span><span class="sxs-lookup"><span data-stu-id="fbafb-139">Linear – full frame ads that pause the main video</span></span>

<span data-ttu-id="fbafb-140">非線性 – 播放被當做主要影片而顯示的疊加廣告，通常是播放器中的標誌或其他靜態影像</span><span class="sxs-lookup"><span data-stu-id="fbafb-140">Nonlinear – overlay ads that are displayed as the main video is playing, usually a logo or other static image placed within the player</span></span>

<span data-ttu-id="fbafb-141">隨播 – 顯示在播放器之外的廣告</span><span class="sxs-lookup"><span data-stu-id="fbafb-141">Companion – ads that are displayed outside of the player</span></span>

<span data-ttu-id="fbafb-142">廣告可以放在主要影片時間軸的任何時間點。</span><span class="sxs-lookup"><span data-stu-id="fbafb-142">Ads can be placed at any point in the main video’s time line.</span></span> <span data-ttu-id="fbafb-143">您必須告訴播放器何時播放廣告以及要播放哪些廣告。</span><span class="sxs-lookup"><span data-stu-id="fbafb-143">You must tell the player when to play the ad and which ads to play.</span></span> <span data-ttu-id="fbafb-144">使用一組標準的 XML 格式檔案即可搞定：Video Ad Service Template (VAST)、Digital Video Multiple Ad Playlist (VMAP)、Media Abstract Sequencing Template (MAST) 以及 Digital Video Player Ad Interface Definition (VPAID)。</span><span class="sxs-lookup"><span data-stu-id="fbafb-144">This is done using a set of standard XML-based files: Video Ad Service Template (VAST), Digital Video Multiple Ad Playlist (VMAP), Media Abstract Sequencing Template (MAST), and Digital Video Player Ad Interface Definition (VPAID).</span></span> <span data-ttu-id="fbafb-145">VAST 檔案會指定要顯示的廣告。</span><span class="sxs-lookup"><span data-stu-id="fbafb-145">VAST files specify what ads to display.</span></span> <span data-ttu-id="fbafb-146">VMAP 檔案會指定何時播放各種廣告而且包含 VAST XML。</span><span class="sxs-lookup"><span data-stu-id="fbafb-146">VMAP files specify when to play various ads and contain VAST XML.</span></span> <span data-ttu-id="fbafb-147">MAST 檔案是另一種廣告排序的方法，而且也包含 VAST XML。</span><span class="sxs-lookup"><span data-stu-id="fbafb-147">MAST files are another way to sequence ads which also can contain VAST XML.</span></span> <span data-ttu-id="fbafb-148">VPAID 檔案會定義影片播放器廣告和廣告或廣告伺服器之間的介面。</span><span class="sxs-lookup"><span data-stu-id="fbafb-148">VPAID files define an interface between the video player and the ad or ad server.</span></span> <span data-ttu-id="fbafb-149">如需詳細資訊，請參閱 [插入廣告](https://msdn.microsoft.com/library/dn387398.aspx)。</span><span class="sxs-lookup"><span data-stu-id="fbafb-149">For more information, see [Inserting Ads](https://msdn.microsoft.com/library/dn387398.aspx).</span></span>

<span data-ttu-id="fbafb-150">如需了解即時資料流視訊的隱藏式字幕和廣告支援，請參閱 [支援的隱藏式輔助字幕和廣告插入標準](https://msdn.microsoft.com/library/c49e0b4d-357e-4cca-95e5-2288924d1ff3#caption_ad)。</span><span class="sxs-lookup"><span data-stu-id="fbafb-150">For information about closed captioning and ads support in Live streaming videos, see [Supported Closed Captioning and Ad Insertion Standards](https://msdn.microsoft.com/library/c49e0b4d-357e-4cca-95e5-2288924d1ff3#caption_ad).</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="fbafb-151">媒體服務學習路徑</span><span class="sxs-lookup"><span data-stu-id="fbafb-151">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="fbafb-152">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="fbafb-152">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="fbafb-153">另請參閱</span><span class="sxs-lookup"><span data-stu-id="fbafb-153">See Also</span></span>
[<span data-ttu-id="fbafb-154">透過 DASH.js 將 MPEG-DASH 彈性資料流視訊嵌入到 HTML5 應用程式</span><span class="sxs-lookup"><span data-stu-id="fbafb-154">Embedding a MPEG-DASH Adaptive Streaming Video in an HTML5 Application with DASH.js</span></span>](media-services-embed-mpeg-dash-in-html5.md)

[<span data-ttu-id="fbafb-155">GitHub dash.js 存放庫</span><span class="sxs-lookup"><span data-stu-id="fbafb-155">GitHub dash.js repository</span></span>](https://github.com/Dash-Industry-Forum/dash.js)

