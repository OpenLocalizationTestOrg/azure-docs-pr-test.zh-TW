---
title: "  透過 Azure 入口網站發佈內容 | Microsoft Docs"
description: "本教學課程將逐步引導您完成透過 Azure 入口網站發佈內容的步驟。"
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
ms.openlocfilehash: 68a2fbdda0996cf4ba5ea3b09816bf845af756f4
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="publish-content-with-the-azure-portal"></a><span data-ttu-id="8050d-103">透過 Azure 入口網站發佈內容</span><span class="sxs-lookup"><span data-stu-id="8050d-103">Publish content with the Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="8050d-104">入口網站</span><span class="sxs-lookup"><span data-stu-id="8050d-104">Portal</span></span>](media-services-portal-publish.md)
> * [<span data-ttu-id="8050d-105">.NET</span><span class="sxs-lookup"><span data-stu-id="8050d-105">.NET</span></span>](media-services-deliver-streaming-content.md)
> * [<span data-ttu-id="8050d-106">REST</span><span class="sxs-lookup"><span data-stu-id="8050d-106">REST</span></span>](media-services-rest-deliver-streaming-content.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="8050d-107">Overview</span><span class="sxs-lookup"><span data-stu-id="8050d-107">Overview</span></span>
> [!NOTE]
> <span data-ttu-id="8050d-108">若要完成此教學課程，您需要 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="8050d-108">To complete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="8050d-109">如需詳細資料，請參閱 [Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="8050d-109">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
> 
> 

<span data-ttu-id="8050d-110">如要想提供 URL 給使用者，讓使用者可以利用這個 URL 來傳送或下載內容，請您先建立定位器來發佈您的資產。</span><span class="sxs-lookup"><span data-stu-id="8050d-110">To provide your user with a  URL that can be used to stream or download your content, you first need to "publish" your asset by creating a locator.</span></span> <span data-ttu-id="8050d-111">定位器提供對於資產中包含之檔案的存取。</span><span class="sxs-lookup"><span data-stu-id="8050d-111">Locators provide access to files contained in the asset.</span></span> <span data-ttu-id="8050d-112">媒體服務支援兩種類型的定位器：</span><span class="sxs-lookup"><span data-stu-id="8050d-112">Media Services supports two types of locators:</span></span> 

* <span data-ttu-id="8050d-113">串流 (OnDemandOrigin) 定位器，用來自適性串流 (例如，串流處理 MPEG DASH、HLS 或 Smooth Streaming)。</span><span class="sxs-lookup"><span data-stu-id="8050d-113">Streaming (OnDemandOrigin) locators, used for adaptive streaming (for example, to stream MPEG DASH, HLS, or Smooth Streaming).</span></span> <span data-ttu-id="8050d-114">若要建立串流定位器，您的資產必須包含 .ism 檔案。</span><span class="sxs-lookup"><span data-stu-id="8050d-114">To create a streaming locator your asset must contain an .ism file.</span></span> 
* <span data-ttu-id="8050d-115">漸進式 (SAS) 定位器，用於透過漸進式下載傳遞視訊。</span><span class="sxs-lookup"><span data-stu-id="8050d-115">Progressive (SAS) locators, used for delivery of video via progressive download.</span></span>

<span data-ttu-id="8050d-116">資料流 URL 的格式如下，還可以用它來播放 Smooth Streaming 資產。</span><span class="sxs-lookup"><span data-stu-id="8050d-116">A streaming URL has the following format and you can use it to play Smooth Streaming assets.</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest

<span data-ttu-id="8050d-117">若要建立 HLS 資料流 URL，請在 URL 加上 (format=m3u8-aapl)。</span><span class="sxs-lookup"><span data-stu-id="8050d-117">To build an HLS streaming URL, append (format=m3u8-aapl) to the URL.</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=m3u8-aapl)

<span data-ttu-id="8050d-118">若要建置 MPEG DASH 串流 URL，請將 (格式=mpd-time-csf) 附加至 URL。</span><span class="sxs-lookup"><span data-stu-id="8050d-118">To build an  MPEG DASH streaming URL, append (format=mpd-time-csf) to the URL.</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=mpd-time-csf)

<span data-ttu-id="8050d-119">SAS URL 具有下列格式。</span><span class="sxs-lookup"><span data-stu-id="8050d-119">A SAS URL has the following format.</span></span>

    {blob container name}/{asset name}/{file name}/{SAS signature}

<span data-ttu-id="8050d-120">如需詳細資訊，請參閱 [傳遞內容概觀](media-services-deliver-content-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="8050d-120">For more information, see [Delivering content overview](media-services-deliver-content-overview.md).</span></span>

> [!NOTE]
> <span data-ttu-id="8050d-121">如果您在 2015 年 3 月前使用入口網站來建立定位器，則建立的定位器 2 年後便告失效。</span><span class="sxs-lookup"><span data-stu-id="8050d-121">If you used the portal to create locators before March 2015, locators with a two year expiration date were created.</span></span>  
> 
> 

<span data-ttu-id="8050d-122">若要更新定位器的到期日，請使用 [REST](https://docs.microsoft.com/rest/api/media/operations/locator#update_a_locator) 或 [.NET](http://go.microsoft.com/fwlink/?LinkID=533259) API。</span><span class="sxs-lookup"><span data-stu-id="8050d-122">To update an expiration date on a locator, use [REST](https://docs.microsoft.com/rest/api/media/operations/locator#update_a_locator) or [.NET](http://go.microsoft.com/fwlink/?LinkID=533259) APIs.</span></span> <span data-ttu-id="8050d-123">請注意，當您更新 SAS 定位器的到期日，URL 也會隨之變更。</span><span class="sxs-lookup"><span data-stu-id="8050d-123">Note that when you update the expiration date of a SAS locator, the URL changes.</span></span>

### <a name="to-use-the-portal-to-publish-an-asset"></a><span data-ttu-id="8050d-124">使用入口網站發佈資產</span><span class="sxs-lookup"><span data-stu-id="8050d-124">To use the portal to publish an asset</span></span>
<span data-ttu-id="8050d-125">若要使用入口網站發佈資產，請執行下列作業：</span><span class="sxs-lookup"><span data-stu-id="8050d-125">To use the portal to publish an asset, do the following:</span></span>

1. <span data-ttu-id="8050d-126">在 [Azure 入口網站](https://portal.azure.com/)中，選取您的 Azure 媒體服務帳戶。</span><span class="sxs-lookup"><span data-stu-id="8050d-126">In the [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="8050d-127">選取 [釘選到儀表板]  > 。</span><span class="sxs-lookup"><span data-stu-id="8050d-127">Select **Settings** > **Assets**.</span></span>
3. <span data-ttu-id="8050d-128">選取您要發佈的資產。</span><span class="sxs-lookup"><span data-stu-id="8050d-128">Select the asset that you want to publish.</span></span>
4. <span data-ttu-id="8050d-129">按一下 [發佈]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="8050d-129">Click the **Publish** button.</span></span>
5. <span data-ttu-id="8050d-130">選取定位器類型。</span><span class="sxs-lookup"><span data-stu-id="8050d-130">Select the locator type.</span></span>
6. <span data-ttu-id="8050d-131">按 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="8050d-131">Press **Add**.</span></span>
   
    ![發佈](./media/media-services-portal-vod-get-started/media-services-publish1.png)

<span data-ttu-id="8050d-133">URL 便會加入 [已發佈的 URL] 清單中。</span><span class="sxs-lookup"><span data-stu-id="8050d-133">The URL will be added to the list of **Published URLs**.</span></span>

## <a name="play-content-from-the-portal"></a><span data-ttu-id="8050d-134">從入口網站播放內容</span><span class="sxs-lookup"><span data-stu-id="8050d-134">Play content from the portal</span></span>
<span data-ttu-id="8050d-135">Azure 入口網站提供內容播放程式，您可用來測試您的視訊。</span><span class="sxs-lookup"><span data-stu-id="8050d-135">The Azure portal provides a content player that you can use to test your video.</span></span>

<span data-ttu-id="8050d-136">按一下想要的視訊，然後按一下 [播放]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="8050d-136">Click the desired video and then click the **Play** button.</span></span>

![發佈](./media/media-services-portal-vod-get-started/media-services-play.png)

<span data-ttu-id="8050d-138">適用一些考量事項：</span><span class="sxs-lookup"><span data-stu-id="8050d-138">Some considerations apply:</span></span>

* <span data-ttu-id="8050d-139">確定已發佈視訊。</span><span class="sxs-lookup"><span data-stu-id="8050d-139">Make sure the video has been published.</span></span>
* <span data-ttu-id="8050d-140">此 **媒體播放器** 會從預設串流端點播放。</span><span class="sxs-lookup"><span data-stu-id="8050d-140">This **Media player** plays from the default streaming endpoint.</span></span> <span data-ttu-id="8050d-141">如果您想要從非預設串流端點播放，請按一下以複製 URL 並使用其他播放器。</span><span class="sxs-lookup"><span data-stu-id="8050d-141">If you want to play from a non-default streaming endpoint, click to copy the URL and use another player.</span></span> <span data-ttu-id="8050d-142">例如， [Azure 媒體服務播放器](http://amsplayer.azurewebsites.net/azuremediaplayer.html)。</span><span class="sxs-lookup"><span data-stu-id="8050d-142">For example, [Azure Media Services Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span></span>
* <span data-ttu-id="8050d-143">您正在進行串流的串流端點必須正在執行。</span><span class="sxs-lookup"><span data-stu-id="8050d-143">The streaming endpoint from which you are streaming must be running.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="8050d-144">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8050d-144">Next steps</span></span>
<span data-ttu-id="8050d-145">檢閱媒體服務學習路徑。</span><span class="sxs-lookup"><span data-stu-id="8050d-145">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="8050d-146">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="8050d-146">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

