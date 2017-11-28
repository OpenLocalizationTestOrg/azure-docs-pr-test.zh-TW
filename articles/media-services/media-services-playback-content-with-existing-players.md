---
title: "使用現有的撥放器來撥放內容 - Azure | Microsoft Docs"
description: "本主題列出現有的播放程式，您可以使用來播放您的內容。"
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 7e9fcf89-0fb6-4fa4-96cb-666320684d69
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: juliako
ms.openlocfilehash: 48f373b013b1192c353352b801876d706d91dd28
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="playing-your-content-with-existing-players"></a><span data-ttu-id="bf757-103">使用現有播放器來播放您的內容</span><span class="sxs-lookup"><span data-stu-id="bf757-103">Playing your content with existing players</span></span>
<span data-ttu-id="bf757-104">Azure 媒體服務支援許多熱門的串流格式，例如 Smooth Streaming、HTTP 即時資料流和 MPEG-Dash。</span><span class="sxs-lookup"><span data-stu-id="bf757-104">Azure Media Services supports many popular streaming formats, such as Smooth Streaming, HTTP Live Streaming, and MPEG-Dash.</span></span> <span data-ttu-id="bf757-105">本主題會指引您可用來測試串流的現有播放程式。</span><span class="sxs-lookup"><span data-stu-id="bf757-105">This topic points you to existing players that you can use to test your streams.</span></span>

### <a name="the-azure-portal-media-services-content-player"></a><span data-ttu-id="bf757-106">Azure 入口網站媒體服務內容播放程式</span><span class="sxs-lookup"><span data-stu-id="bf757-106">The Azure portal Media Services content player</span></span>
<span data-ttu-id="bf757-107">**Azure** 入口網站提供內容播放程式，您可用來測試您的視訊。</span><span class="sxs-lookup"><span data-stu-id="bf757-107">The **Azure** portal provides a content player that you can use to test your video.</span></span>

<span data-ttu-id="bf757-108">按一下想用的視訊 (請確定它 [已發行](media-services-portal-publish.md))，按一下入口網站底部的 [ **播放** ] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="bf757-108">Click on the desired video (make sure it was [published](media-services-portal-publish.md)) and click the **Play** button at the bottom of the portal.</span></span>

<span data-ttu-id="bf757-109">適用一些考量事項：</span><span class="sxs-lookup"><span data-stu-id="bf757-109">Some considerations apply:</span></span>

* <span data-ttu-id="bf757-110">**媒體服務內容播放程式** 會從預設串流端點播放。</span><span class="sxs-lookup"><span data-stu-id="bf757-110">The **MEDIA SERVICES CONTENT PLAYER** plays from the default streaming endpoint.</span></span> <span data-ttu-id="bf757-111">如果您想要從非預設串流端點播放，請使用其他播放程式。</span><span class="sxs-lookup"><span data-stu-id="bf757-111">If you want to play from a non-default streaming endpoint, use another player.</span></span> <span data-ttu-id="bf757-112">例如， [Azure 媒體播放器](http://amsplayer.azurewebsites.net/azuremediaplayer.html)。</span><span class="sxs-lookup"><span data-stu-id="bf757-112">For example, [Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span></span>

![AMSPlayer][AMSPlayer]

### <a name="azure-media-player"></a><span data-ttu-id="bf757-114">Azure 媒體播放器</span><span class="sxs-lookup"><span data-stu-id="bf757-114">Azure Media Player</span></span>
<span data-ttu-id="bf757-115">使用 [Azure 媒體播放器](http://amsplayer.azurewebsites.net/azuremediaplayer.html) 播放以下任一格式的內容 (清除或受保護)：</span><span class="sxs-lookup"><span data-stu-id="bf757-115">Use [Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html) to playback your content (clear or protected) in any of the following formats:</span></span>

* <span data-ttu-id="bf757-116">Smooth Streaming</span><span class="sxs-lookup"><span data-stu-id="bf757-116">Smooth Streaming</span></span>
* <span data-ttu-id="bf757-117">MPEG DASH</span><span class="sxs-lookup"><span data-stu-id="bf757-117">MPEG DASH</span></span>
* <span data-ttu-id="bf757-118">HLS</span><span class="sxs-lookup"><span data-stu-id="bf757-118">HLS</span></span>
* <span data-ttu-id="bf757-119">Progressive MP4</span><span class="sxs-lookup"><span data-stu-id="bf757-119">Progressive MP4</span></span>

### <a name="flash-player"></a><span data-ttu-id="bf757-120">Flash Player</span><span class="sxs-lookup"><span data-stu-id="bf757-120">Flash Player</span></span>
#### <a name="aes-encrypted-with-token"></a><span data-ttu-id="bf757-121">AES 加密與權杖</span><span class="sxs-lookup"><span data-stu-id="bf757-121">AES-encrypted with Token</span></span>
[<span data-ttu-id="bf757-122">http://aestoken.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="bf757-122">http://aestoken.azurewebsites.net</span></span>](http://aestoken.azurewebsites.net)

### <a name="silverlight-players"></a><span data-ttu-id="bf757-123">Silverlight 播放程式</span><span class="sxs-lookup"><span data-stu-id="bf757-123">Silverlight Players</span></span>
#### <a name="monitoring"></a><span data-ttu-id="bf757-124">監視</span><span class="sxs-lookup"><span data-stu-id="bf757-124">Monitoring</span></span>
[<span data-ttu-id="bf757-125">http://smf.cloudapp.net/healthmonitor</span><span class="sxs-lookup"><span data-stu-id="bf757-125">http://smf.cloudapp.net/healthmonitor</span></span>](http://smf.cloudapp.net/healthmonitor)

#### <a name="playready-with-token"></a><span data-ttu-id="bf757-126">PlayReady 與權杖</span><span class="sxs-lookup"><span data-stu-id="bf757-126">PlayReady with Token</span></span>
[<span data-ttu-id="bf757-127">http://sltoken.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="bf757-127">http://sltoken.azurewebsites.net</span></span>](http://sltoken.azurewebsites.net)

### <a name="dash-players"></a><span data-ttu-id="bf757-128">DASH 播放程式</span><span class="sxs-lookup"><span data-stu-id="bf757-128">DASH Players</span></span>
[<span data-ttu-id="bf757-129">http://dashplayer.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="bf757-129">http://dashplayer.azurewebsites.net</span></span>](http://dashplayer.azurewebsites.net)

[<span data-ttu-id="bf757-130">http://dashif.org</span><span class="sxs-lookup"><span data-stu-id="bf757-130">http://dashif.org</span></span>](http://dashif.org)

### <a name="other"></a><span data-ttu-id="bf757-131">其他</span><span class="sxs-lookup"><span data-stu-id="bf757-131">Other</span></span>
<span data-ttu-id="bf757-132">若要測試 HLS URL，您也可以使用：</span><span class="sxs-lookup"><span data-stu-id="bf757-132">To test HLS URLs you can also use:</span></span>

* <span data-ttu-id="bf757-133">**Safari** 或</span><span class="sxs-lookup"><span data-stu-id="bf757-133">**Safari** on an iOS device or</span></span>
* <span data-ttu-id="bf757-134">**3ivx HLS 播放器** 。</span><span class="sxs-lookup"><span data-stu-id="bf757-134">**3ivx HLS Player** on Windows.</span></span>

## <a name="developing-video-players"></a><span data-ttu-id="bf757-135">開發視訊播放器</span><span class="sxs-lookup"><span data-stu-id="bf757-135">Developing video players</span></span>
<span data-ttu-id="bf757-136">如需瞭解如何自行開發播放程式，請參閱 [開發視訊播放器](media-services-develop-video-players.md)</span><span class="sxs-lookup"><span data-stu-id="bf757-136">For information about how to develop your own players, see [Developing video players](media-services-develop-video-players.md)</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="bf757-137">媒體服務學習路徑</span><span class="sxs-lookup"><span data-stu-id="bf757-137">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="bf757-138">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="bf757-138">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

[AMSPlayer]: ./media/media-services-playback-content-with-existing-players/media-services-portal-player.png
