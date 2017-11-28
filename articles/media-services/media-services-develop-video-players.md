---
title: "aaaDevelop 影片播放器應用程式"
description: "hello 主題提供的連結 tooPlayer 架構和外掛程式，您可以使用 toodevelop 自己的用戶端應用程式可以取用從媒體服務串流媒體。"
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
ms.openlocfilehash: a66daa4f006a1f05271cc9ed6a02ea7ee460321d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="develop-video-player-applications"></a><span data-ttu-id="25cab-103">開發視訊播放器應用程式</span><span class="sxs-lookup"><span data-stu-id="25cab-103">Develop video player applications</span></span>
## <a name="overview"></a><span data-ttu-id="25cab-104">概觀</span><span class="sxs-lookup"><span data-stu-id="25cab-104">Overview</span></span>
<span data-ttu-id="25cab-105">Azure Media Services 提供 hello 工具，您需要 toocreate 豐富、 動態的用戶端播放器應用程式，用於大部分平台，包括： iOS 裝置、 Android 裝置、 Windows、 Windows Phone、 Xbox 和機上方塊。</span><span class="sxs-lookup"><span data-stu-id="25cab-105">Azure Media Services provides hello tools you need toocreate rich, dynamic client player applications for most platforms including: iOS Devices, Android Devices, Windows, Windows Phone, Xbox, and Set-top boxes.</span></span> <span data-ttu-id="25cab-106">本主題也會提供連結 tooSDKs 和播放器架構，您可以使用 toodevelop 自己的用戶端應用程式可以取用從 Azure 媒體服務串流媒體。</span><span class="sxs-lookup"><span data-stu-id="25cab-106">This topic also provides links tooSDKs and Player Frameworks that you can use toodevelop your own client applications that can consume streaming media from Azure Media Services.</span></span>

>[!NOTE]
><span data-ttu-id="25cab-107">AMS 帳戶建立時**預設**串流端點就會加入 tooyour 帳戶 hello**已停止**狀態。</span><span class="sxs-lookup"><span data-stu-id="25cab-107">When your AMS account is created a **default** streaming endpoint is added tooyour account in hello **Stopped** state.</span></span> <span data-ttu-id="25cab-108">串流處理您的內容，並採取利用動態封裝和動態加密，toostart hello 串流端點，您想要從中 toostream 內容已經在 hello toobe**執行**狀態。</span><span class="sxs-lookup"><span data-stu-id="25cab-108">toostart streaming your content and take advantage of dynamic packaging and dynamic encryption, hello streaming endpoint from which you want toostream content has toobe in hello **Running** state.</span></span> 
 
## <a name="azure-media-player"></a><span data-ttu-id="25cab-109">Azure 媒體播放器</span><span class="sxs-lookup"><span data-stu-id="25cab-109">Azure Media Player</span></span>
<span data-ttu-id="25cab-110">[Azure Media Player](http://aka.ms/ampinfo) web 影片播放器 tooplay 後媒體內容從 Microsoft Azure Media Services 上建立各種不同的瀏覽器及裝置。</span><span class="sxs-lookup"><span data-stu-id="25cab-110">[Azure Media Player](http://aka.ms/ampinfo) is a web video player built tooplay back media content from Microsoft Azure Media Services on a wide variety of browsers and devices.</span></span> <span data-ttu-id="25cab-111">Azure Media Player 會使用業界標準，例如 HTML5、 媒體來源延伸模組 (MSE) 和加密媒體擴充功能 (EME) tooprovide 豐富的彈性串流處理體驗。</span><span class="sxs-lookup"><span data-stu-id="25cab-111">Azure Media Player utilizes industry standards, such as HTML5, Media Source Extensions (MSE), and Encrypted Media Extensions (EME) tooprovide an enriched adaptive streaming experience.</span></span> <span data-ttu-id="25cab-112">無法在裝置或瀏覽器使用這些標準時，Azure Media Player 則會使用 Flash 和 Silverlight 做為後援技術。</span><span class="sxs-lookup"><span data-stu-id="25cab-112">When these standards are not available on a device or in a browser, Azure Media Player uses Flash and Silverlight as fallback technology.</span></span> <span data-ttu-id="25cab-113">無論用 hello 播放技術，開發人員會有統一的 JavaScript 介面 tooaccess 應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="25cab-113">Regardless of hello playback technology used, developers will have a unified JavaScript interface tooaccess APIs.</span></span> <span data-ttu-id="25cab-114">這可讓內容由 Azure Media Services toobe 播放跨各種裝置和瀏覽器，而不需要任何額外的工作。</span><span class="sxs-lookup"><span data-stu-id="25cab-114">This allows for content served by Azure Media Services toobe played across a wide-range of devices and browsers without any extra effort.</span></span>

<span data-ttu-id="25cab-115">Microsoft Azure Media Services 可讓內容 toobe 提供 Smooth Streaming、 DASH 和 HLS 資料流格式 tooplay 備份內容。</span><span class="sxs-lookup"><span data-stu-id="25cab-115">Microsoft Azure Media Services allows for content toobe served up with DASH, Smooth Streaming, and HLS streaming formats tooplay back content.</span></span> <span data-ttu-id="25cab-116">Azure Media Player 會考量這些不同的格式，並自動播放 hello 根據 hello 平台/瀏覽器功能的最佳連結。</span><span class="sxs-lookup"><span data-stu-id="25cab-116">Azure Media Player takes into account these various formats and automatically plays hello best link based on hello platform/browser capabilities.</span></span> <span data-ttu-id="25cab-117">Microsoft Azure 媒體服務也允許利用 PlayReady 加密或 AES 128 位元信封加密，進行資產的動態加密。</span><span class="sxs-lookup"><span data-stu-id="25cab-117">Microsoft Azure Media Services also allows for dynamic encryption of assets with PlayReady encryption or AES-128 bit envelope encryption.</span></span> <span data-ttu-id="25cab-118">只要設定正確，Azure Media Player 允許解密 PlayReady 和 AES 128 位元加密的內容。</span><span class="sxs-lookup"><span data-stu-id="25cab-118">Azure Media Player allows for decryption of PlayReady and AES-128 bit encrypted content when appropriately configured.</span></span> 

<span data-ttu-id="25cab-119">其他資訊：</span><span class="sxs-lookup"><span data-stu-id="25cab-119">For more information:</span></span>

* [<span data-ttu-id="25cab-120">Azure Media Player</span><span class="sxs-lookup"><span data-stu-id="25cab-120">Azure Media Player</span></span>](http://aka.ms/ampinfo)
* [<span data-ttu-id="25cab-121">Azure Media Player 文件</span><span class="sxs-lookup"><span data-stu-id="25cab-121">Azure Media Player Documentation</span></span>](http://aka.ms/ampdocs) 
* [<span data-ttu-id="25cab-122">Azure Media Player 開始使用部落格</span><span class="sxs-lookup"><span data-stu-id="25cab-122">Azure Media Player Getting Started Blog</span></span>](https://azure.microsoft.com/blog/2015/04/15/announcing-azure-media-player/)
* [<span data-ttu-id="25cab-123">登入，以最新的 Azure Media Player 的 hello toodate 向上 toostay</span><span class="sxs-lookup"><span data-stu-id="25cab-123">Sign up toostay up toodate with hello latest from Azure Media Player</span></span>](http://aka.ms/ampsignup)
* [<span data-ttu-id="25cab-124">新增功能要求、概念和意見反應</span><span class="sxs-lookup"><span data-stu-id="25cab-124">Add new feature requests, ideas, feedback</span></span>](http://aka.ms/ampuservoice) 

## <a name="other-tools-for-creating-player-applications"></a><span data-ttu-id="25cab-125">其他可用來建立播放器應用程式的工具</span><span class="sxs-lookup"><span data-stu-id="25cab-125">Other Tools for Creating Player Applications</span></span>
<span data-ttu-id="25cab-126">您也可以使用任何下列 Sdk hello:</span><span class="sxs-lookup"><span data-stu-id="25cab-126">You can also use any of hello following SDKs:</span></span>

* [<span data-ttu-id="25cab-127">Smooth Streaming Client SDK</span><span class="sxs-lookup"><span data-stu-id="25cab-127">Smooth Streaming Client SDK</span></span>](http://www.iis.net/downloads/microsoft/smooth-streaming) 
* [<span data-ttu-id="25cab-128">Smooth Streaming Windows 市集應用程式</span><span class="sxs-lookup"><span data-stu-id="25cab-128">Smooth Streaming Windows Store App</span></span>](media-services-build-smooth-streaming-apps.md)
* [<span data-ttu-id="25cab-129">Microsoft 媒體平台：Player Framework</span><span class="sxs-lookup"><span data-stu-id="25cab-129">Microsoft Media Platform: Player Framework</span></span>](http://playerframework.codeplex.com/) 
* [<span data-ttu-id="25cab-130">HTML5 Player Framework 文件</span><span class="sxs-lookup"><span data-stu-id="25cab-130">HTML5 Player Framework Documentation</span></span>](http://playerframework.codeplex.com/wikipage?title=HTML5%20Player&referringTitle=Documentation) 
* [<span data-ttu-id="25cab-131">Microsoft Smooth Streaming Plugin for OSMF</span><span class="sxs-lookup"><span data-stu-id="25cab-131">Microsoft Smooth Streaming Plugin for OSMF</span></span>](https://www.microsoft.com/download/details.aspx?id=36057) 
* [<span data-ttu-id="25cab-132">Licensing Microsoft® Smooth Streaming Client Porting Kit</span><span class="sxs-lookup"><span data-stu-id="25cab-132">Licensing Microsoft® Smooth Streaming Client Porting Kit</span></span>](http://aka.ms/sspk) 
* [<span data-ttu-id="25cab-133">XBOX Video Application Development</span><span class="sxs-lookup"><span data-stu-id="25cab-133">XBOX Video Application Development</span></span>](http://xbox.create.msdn.com/) 

## <a name="advertising"></a><span data-ttu-id="25cab-134">廣告</span><span class="sxs-lookup"><span data-stu-id="25cab-134">Advertising</span></span>
<span data-ttu-id="25cab-135">Azure Media Services 提供廣告插入 hello Windows 媒體平台的支援： 播放器架構。</span><span class="sxs-lookup"><span data-stu-id="25cab-135">Azure Media Services provides support for ad insertion through hello Windows Media Platform: Player Frameworks.</span></span> <span data-ttu-id="25cab-136">具備廣告支援的播放器架構都適用於 Windows 8、Silverlight、Windows Phone 8 和 iOS 裝置。</span><span class="sxs-lookup"><span data-stu-id="25cab-136">Player frameworks with ad support are available for Windows 8, Silverlight, Windows Phone 8, and iOS devices.</span></span> <span data-ttu-id="25cab-137">每個播放器架構包含範例程式碼，為您示範如何 tooimplement 播放器應用程式。</span><span class="sxs-lookup"><span data-stu-id="25cab-137">Each player framework contains sample code that shows you how tooimplement a player application.</span></span> <span data-ttu-id="25cab-138">目前有三種不同的廣告可以插入媒體中：</span><span class="sxs-lookup"><span data-stu-id="25cab-138">There are three different kinds of ads you can insert into your media:</span></span>

<span data-ttu-id="25cab-139">線性 – 暫停主要影片的 hello 的完整框架廣告</span><span class="sxs-lookup"><span data-stu-id="25cab-139">Linear – full frame ads that pause hello main video</span></span>

<span data-ttu-id="25cab-140">非線性 – hello 主要影片播放時顯示的重疊廣告，通常標誌或其他靜態影像放置於 hello 播放程式內。</span><span class="sxs-lookup"><span data-stu-id="25cab-140">Nonlinear – overlay ads that are displayed as hello main video is playing, usually a logo or other static image placed within hello player</span></span>

<span data-ttu-id="25cab-141">隨播 – 顯示 hello 播放程式之外的廣告</span><span class="sxs-lookup"><span data-stu-id="25cab-141">Companion – ads that are displayed outside of hello player</span></span>

<span data-ttu-id="25cab-142">廣告可以放在任何時間點 hello 主要影片的時間線。</span><span class="sxs-lookup"><span data-stu-id="25cab-142">Ads can be placed at any point in hello main video’s time line.</span></span> <span data-ttu-id="25cab-143">您必須告知 hello player tooplay 當 hello ad，以及哪些廣告 tooplay。</span><span class="sxs-lookup"><span data-stu-id="25cab-143">You must tell hello player when tooplay hello ad and which ads tooplay.</span></span> <span data-ttu-id="25cab-144">使用一組標準的 XML 格式檔案即可搞定：Video Ad Service Template (VAST)、Digital Video Multiple Ad Playlist (VMAP)、Media Abstract Sequencing Template (MAST) 以及 Digital Video Player Ad Interface Definition (VPAID)。</span><span class="sxs-lookup"><span data-stu-id="25cab-144">This is done using a set of standard XML-based files: Video Ad Service Template (VAST), Digital Video Multiple Ad Playlist (VMAP), Media Abstract Sequencing Template (MAST), and Digital Video Player Ad Interface Definition (VPAID).</span></span> <span data-ttu-id="25cab-145">VAST 檔案會指定哪些廣告 toodisplay。</span><span class="sxs-lookup"><span data-stu-id="25cab-145">VAST files specify what ads toodisplay.</span></span> <span data-ttu-id="25cab-146">VMAP 檔案會指定何時 tooplay 各種廣告及包含 VAST XML。</span><span class="sxs-lookup"><span data-stu-id="25cab-146">VMAP files specify when tooplay various ads and contain VAST XML.</span></span> <span data-ttu-id="25cab-147">MAST 檔案是另一個方式 toosequence 廣告也可包含 VAST XML。</span><span class="sxs-lookup"><span data-stu-id="25cab-147">MAST files are another way toosequence ads which also can contain VAST XML.</span></span> <span data-ttu-id="25cab-148">VPAID 檔案會定義 hello 影片播放器與 hello 廣告或廣告伺服器之間的介面。</span><span class="sxs-lookup"><span data-stu-id="25cab-148">VPAID files define an interface between hello video player and hello ad or ad server.</span></span> <span data-ttu-id="25cab-149">如需詳細資訊，請參閱 [插入廣告](https://msdn.microsoft.com/library/dn387398.aspx)。</span><span class="sxs-lookup"><span data-stu-id="25cab-149">For more information, see [Inserting Ads](https://msdn.microsoft.com/library/dn387398.aspx).</span></span>

<span data-ttu-id="25cab-150">如需了解即時資料流視訊的隱藏式字幕和廣告支援，請參閱 [支援的隱藏式輔助字幕和廣告插入標準](https://msdn.microsoft.com/library/c49e0b4d-357e-4cca-95e5-2288924d1ff3#caption_ad)。</span><span class="sxs-lookup"><span data-stu-id="25cab-150">For information about closed captioning and ads support in Live streaming videos, see [Supported Closed Captioning and Ad Insertion Standards](https://msdn.microsoft.com/library/c49e0b4d-357e-4cca-95e5-2288924d1ff3#caption_ad).</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="25cab-151">媒體服務學習路徑</span><span class="sxs-lookup"><span data-stu-id="25cab-151">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="25cab-152">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="25cab-152">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="25cab-153">另請參閱</span><span class="sxs-lookup"><span data-stu-id="25cab-153">See Also</span></span>
[<span data-ttu-id="25cab-154">透過 DASH.js 將 MPEG-DASH 彈性資料流視訊嵌入到 HTML5 應用程式</span><span class="sxs-lookup"><span data-stu-id="25cab-154">Embedding a MPEG-DASH Adaptive Streaming Video in an HTML5 Application with DASH.js</span></span>](media-services-embed-mpeg-dash-in-html5.md)

[<span data-ttu-id="25cab-155">GitHub dash.js 存放庫</span><span class="sxs-lookup"><span data-stu-id="25cab-155">GitHub dash.js repository</span></span>](https://github.com/Dash-Industry-Forum/dash.js)

