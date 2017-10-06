---
title: "aaa\"發行內容以 hello Azure 入口網站 |Microsoft 文件 」"
description: "本教學課程會引導您發行您的內容以 hello Azure 入口網站的 hello 步驟。"
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 92c364eb-5a5f-4f4e-8816-b162c031bb40
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: juliako
ms.openlocfilehash: a7a3867a6939b4b9da883176c6cc20c99d6c54e7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="publish-content-with-hello-azure-portal"></a><span data-ttu-id="9806f-103">發佈與 hello Azure 入口網站的內容</span><span class="sxs-lookup"><span data-stu-id="9806f-103">Publish content with hello Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="9806f-104">入口網站</span><span class="sxs-lookup"><span data-stu-id="9806f-104">Portal</span></span>](media-services-portal-publish.md)
> * [<span data-ttu-id="9806f-105">.NET</span><span class="sxs-lookup"><span data-stu-id="9806f-105">.NET</span></span>](media-services-deliver-streaming-content.md)
> * [<span data-ttu-id="9806f-106">REST</span><span class="sxs-lookup"><span data-stu-id="9806f-106">REST</span></span>](media-services-rest-deliver-streaming-content.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="9806f-107">概觀</span><span class="sxs-lookup"><span data-stu-id="9806f-107">Overview</span></span>
> [!NOTE]
> <span data-ttu-id="9806f-108">toocomplete 本教學課程中，您需要 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="9806f-108">toocomplete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="9806f-109">如需詳細資料，請參閱 [Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="9806f-109">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
> 
> 

<span data-ttu-id="9806f-110">tooprovide 您一個 url，也可以使用的 toostream 或下載您的內容的使用者，您首先需要太 「 發行 」 您的資產建立定位器。</span><span class="sxs-lookup"><span data-stu-id="9806f-110">tooprovide your user with a  URL that can be used toostream or download your content, you first need too"publish" your asset by creating a locator.</span></span> <span data-ttu-id="9806f-111">定位器提供存取 toofiles hello 資產中所包含。</span><span class="sxs-lookup"><span data-stu-id="9806f-111">Locators provide access toofiles contained in hello asset.</span></span> <span data-ttu-id="9806f-112">媒體服務支援兩種類型的定位器：</span><span class="sxs-lookup"><span data-stu-id="9806f-112">Media Services supports two types of locators:</span></span> 

* <span data-ttu-id="9806f-113">資料流 (OnDemandOrigin) 定位器，用於彈性資料流 （例如，toostream MPEG DASH、 HLS 或 Smooth Streaming）。</span><span class="sxs-lookup"><span data-stu-id="9806f-113">Streaming (OnDemandOrigin) locators, used for adaptive streaming (for example, toostream MPEG DASH, HLS, or Smooth Streaming).</span></span> <span data-ttu-id="9806f-114">toocreate 串流定位器資產必須包含.ism 檔案。</span><span class="sxs-lookup"><span data-stu-id="9806f-114">toocreate a streaming locator your asset must contain an .ism file.</span></span> 
* <span data-ttu-id="9806f-115">漸進式 (SAS) 定位器，用於透過漸進式下載傳遞視訊。</span><span class="sxs-lookup"><span data-stu-id="9806f-115">Progressive (SAS) locators, used for delivery of video via progressive download.</span></span>

<span data-ttu-id="9806f-116">串流 URL 具有下列格式的 hello，您可以使用它 tooplay Smooth Streaming 資產。</span><span class="sxs-lookup"><span data-stu-id="9806f-116">A streaming URL has hello following format and you can use it tooplay Smooth Streaming assets.</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest

<span data-ttu-id="9806f-117">附加 toobuild 的 HLS 資料流 URL (格式 = m3u8 aapl) toohello URL。</span><span class="sxs-lookup"><span data-stu-id="9806f-117">toobuild an HLS streaming URL, append (format=m3u8-aapl) toohello URL.</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=m3u8-aapl)

<span data-ttu-id="9806f-118">附加 toobuild 的 MPEG DASH 串流 URL (格式 = mpd-時間-csf) toohello URL。</span><span class="sxs-lookup"><span data-stu-id="9806f-118">toobuild an  MPEG DASH streaming URL, append (format=mpd-time-csf) toohello URL.</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=mpd-time-csf)

<span data-ttu-id="9806f-119">SAS URL 具有下列格式的 hello。</span><span class="sxs-lookup"><span data-stu-id="9806f-119">A SAS URL has hello following format.</span></span>

    {blob container name}/{asset name}/{file name}/{SAS signature}

<span data-ttu-id="9806f-120">如需詳細資訊，請參閱 [傳遞內容概觀](media-services-deliver-content-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="9806f-120">For more information, see [Delivering content overview](media-services-deliver-content-overview.md).</span></span>

> [!NOTE]
> <span data-ttu-id="9806f-121">如果您使用 hello 入口 toocreate 定位器 2015 年 3 月之前，會建立定位器以兩年的到期日。</span><span class="sxs-lookup"><span data-stu-id="9806f-121">If you used hello portal toocreate locators before March 2015, locators with a two year expiration date were created.</span></span>  
> 
> 

<span data-ttu-id="9806f-122">定位器時，使用上的到期日 tooupdate [REST](https://docs.microsoft.com/rest/api/media/operations/locator#update_a_locator)或[.NET](http://go.microsoft.com/fwlink/?LinkID=533259)應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="9806f-122">tooupdate an expiration date on a locator, use [REST](https://docs.microsoft.com/rest/api/media/operations/locator#update_a_locator) or [.NET](http://go.microsoft.com/fwlink/?LinkID=533259) APIs.</span></span> <span data-ttu-id="9806f-123">請注意，當您更新的 SAS 定位器的 hello 到期日，hello URL 就會變更。</span><span class="sxs-lookup"><span data-stu-id="9806f-123">Note that when you update hello expiration date of a SAS locator, hello URL changes.</span></span>

### <a name="toouse-hello-portal-toopublish-an-asset"></a><span data-ttu-id="9806f-124">toouse hello 入口 toopublish 資產</span><span class="sxs-lookup"><span data-stu-id="9806f-124">toouse hello portal toopublish an asset</span></span>
<span data-ttu-id="9806f-125">toouse hello 入口 toopublish 資產，請勿 hello 遵循：</span><span class="sxs-lookup"><span data-stu-id="9806f-125">toouse hello portal toopublish an asset, do hello following:</span></span>

1. <span data-ttu-id="9806f-126">在 hello [Azure 入口網站](https://portal.azure.com/)，選取您的 Azure Media Services 帳戶。</span><span class="sxs-lookup"><span data-stu-id="9806f-126">In hello [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="9806f-127">選取 **設定** > **資產**。</span><span class="sxs-lookup"><span data-stu-id="9806f-127">Select **Settings** > **Assets**.</span></span>
3. <span data-ttu-id="9806f-128">選取您想 toopublish hello 資產。</span><span class="sxs-lookup"><span data-stu-id="9806f-128">Select hello asset that you want toopublish.</span></span>
4. <span data-ttu-id="9806f-129">按一下 hello**發行** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="9806f-129">Click hello **Publish** button.</span></span>
5. <span data-ttu-id="9806f-130">選取 hello 定位器類型。</span><span class="sxs-lookup"><span data-stu-id="9806f-130">Select hello locator type.</span></span>
6. <span data-ttu-id="9806f-131">按 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="9806f-131">Press **Add**.</span></span>
   
    ![發佈](./media/media-services-portal-vod-get-started/media-services-publish1.png)

<span data-ttu-id="9806f-133">hello URL 將會加入 toohello 清單**發行 Url**。</span><span class="sxs-lookup"><span data-stu-id="9806f-133">hello URL will be added toohello list of **Published URLs**.</span></span>

## <a name="play-content-from-hello-portal"></a><span data-ttu-id="9806f-134">播放內容從 hello 入口網站</span><span class="sxs-lookup"><span data-stu-id="9806f-134">Play content from hello portal</span></span>
<span data-ttu-id="9806f-135">hello Azure 入口網站提供內容的播放程式，您可以使用 tootest 視訊。</span><span class="sxs-lookup"><span data-stu-id="9806f-135">hello Azure portal provides a content player that you can use tootest your video.</span></span>

<span data-ttu-id="9806f-136">按一下想要的 hello 視訊，然後按一下hello**播放** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="9806f-136">Click hello desired video and then click hello **Play** button.</span></span>

![發佈](./media/media-services-portal-vod-get-started/media-services-play.png)

<span data-ttu-id="9806f-138">適用一些考量事項：</span><span class="sxs-lookup"><span data-stu-id="9806f-138">Some considerations apply:</span></span>

* <span data-ttu-id="9806f-139">請確定已發佈視訊 hello。</span><span class="sxs-lookup"><span data-stu-id="9806f-139">Make sure hello video has been published.</span></span>
* <span data-ttu-id="9806f-140">這**Media player**播放從 hello 預設串流端點。</span><span class="sxs-lookup"><span data-stu-id="9806f-140">This **Media player** plays from hello default streaming endpoint.</span></span> <span data-ttu-id="9806f-141">如果您想 tooplay 從非預設串流端點，按一下 toocopy hello URL，並使用其他播放器。</span><span class="sxs-lookup"><span data-stu-id="9806f-141">If you want tooplay from a non-default streaming endpoint, click toocopy hello URL and use another player.</span></span> <span data-ttu-id="9806f-142">例如， [Azure 媒體服務播放器](http://amsplayer.azurewebsites.net/azuremediaplayer.html)。</span><span class="sxs-lookup"><span data-stu-id="9806f-142">For example, [Azure Media Services Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span></span>
* <span data-ttu-id="9806f-143">必須執行 hello 串流的端點從中您串流處理。</span><span class="sxs-lookup"><span data-stu-id="9806f-143">hello streaming endpoint from which you are streaming must be running.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="9806f-144">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9806f-144">Next steps</span></span>
<span data-ttu-id="9806f-145">檢閱媒體服務學習路徑。</span><span class="sxs-lookup"><span data-stu-id="9806f-145">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="9806f-146">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="9806f-146">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

