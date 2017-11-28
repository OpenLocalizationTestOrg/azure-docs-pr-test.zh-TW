---
title: "aaaGet 入門傳遞 VoD 使用 hello Azure 入口網站 |Microsoft 文件"
description: "本教學課程會引導您實作與使用 hello Azure 入口網站的 Azure 媒體服務 (AMS) 應用程式的基本 Video-on-Demand (VoD) 內容傳遞服務的 hello 步驟。"
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 6c98fcfa-39e6-43a5-83a5-d4954788f8a4
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/07/2017
ms.author: juliako
ms.openlocfilehash: 5c1c1b1f74ec1f1301120fe8e5a5ae183fe0338f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-delivering-content-on-demand-using-hello-azure-portal"></a><span data-ttu-id="1858c-103">快速入門將內容傳送隨選使用 hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="1858c-103">Get started with delivering content on demand using hello Azure portal</span></span>
[!INCLUDE [media-services-selector-get-started](../../includes/media-services-selector-get-started.md)]

<span data-ttu-id="1858c-104">本教學課程會引導您實作與使用 hello Azure 入口網站的 Azure 媒體服務 (AMS) 應用程式的基本 Video-on-Demand (VoD) 內容傳遞服務的 hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="1858c-104">This tutorial walks you through hello steps of implementing a basic Video-on-Demand (VoD) content delivery service with Azure Media Services (AMS) application using hello Azure portal.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1858c-105">必要條件</span><span class="sxs-lookup"><span data-stu-id="1858c-105">Prerequisites</span></span>
<span data-ttu-id="1858c-106">hello 下面是必要的 toocomplete hello 教學課程：</span><span class="sxs-lookup"><span data-stu-id="1858c-106">hello following are required toocomplete hello tutorial:</span></span>

* <span data-ttu-id="1858c-107">一個 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="1858c-107">An Azure account.</span></span> <span data-ttu-id="1858c-108">如需詳細資訊，請參閱 [Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="1858c-108">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
* <span data-ttu-id="1858c-109">媒體服務帳戶。</span><span class="sxs-lookup"><span data-stu-id="1858c-109">A Media Services account.</span></span> <span data-ttu-id="1858c-110">toocreate Media Services 帳戶，請參閱[如何 tooCreate Media Services 帳戶](media-services-portal-create-account.md)。</span><span class="sxs-lookup"><span data-stu-id="1858c-110">toocreate a Media Services account, see [How tooCreate a Media Services Account](media-services-portal-create-account.md).</span></span>

<span data-ttu-id="1858c-111">這個教學課程包括下列工作的 hello:</span><span class="sxs-lookup"><span data-stu-id="1858c-111">This tutorial includes hello following tasks:</span></span>

1. <span data-ttu-id="1858c-112">Azure 串流端點。</span><span class="sxs-lookup"><span data-stu-id="1858c-112">Start streaming endpoint.</span></span>
2. <span data-ttu-id="1858c-113">上傳視訊檔案。</span><span class="sxs-lookup"><span data-stu-id="1858c-113">Upload a video file.</span></span>
3. <span data-ttu-id="1858c-114">Hello 原始程式檔編碼為一組彈性位元速率 MP4 檔案。</span><span class="sxs-lookup"><span data-stu-id="1858c-114">Encode hello source file into a set of adaptive bitrate MP4 files.</span></span>
4. <span data-ttu-id="1858c-115">發佈 hello 資產和取得資料流和漸進式下載 Url。</span><span class="sxs-lookup"><span data-stu-id="1858c-115">Publish hello asset and get streaming and progressive download URLs.</span></span>  
5. <span data-ttu-id="1858c-116">播放您的內容。</span><span class="sxs-lookup"><span data-stu-id="1858c-116">Play your content.</span></span>

## <a name="start-streaming-endpoints"></a><span data-ttu-id="1858c-117">啟動串流端點</span><span class="sxs-lookup"><span data-stu-id="1858c-117">Start streaming endpoints</span></span> 

<span data-ttu-id="1858c-118">當使用 Azure Media Services hello 最常見的案例的其中一個會將視訊透過串流處理的彈性位元速率。</span><span class="sxs-lookup"><span data-stu-id="1858c-118">When working with Azure Media Services one of hello most common scenarios is delivering video via adaptive bitrate streaming.</span></span> <span data-ttu-id="1858c-119">Media Services 提供的動態封裝，可讓您 toodeliver 您彈性位元速率編碼的 MP4 內容串流處理媒體服務 (MPEG DASH、 HLS、 Smooth Streaming) 在 just-in-time，支援不需要您 toostore 預先封裝格式每種串流處理格式的版本。</span><span class="sxs-lookup"><span data-stu-id="1858c-119">Media Services provides dynamic packaging, which allows you toodeliver your adaptive bitrate MP4 encoded content in streaming formats supported by Media Services (MPEG DASH, HLS, Smooth Streaming) just-in-time, without you having toostore pre-packaged versions of each of these streaming formats.</span></span>

>[!NOTE]
><span data-ttu-id="1858c-120">AMS 帳戶建立時**預設**串流端點就會加入 tooyour 帳戶 hello**已停止**狀態。</span><span class="sxs-lookup"><span data-stu-id="1858c-120">When your AMS account is created a **default** streaming endpoint is added tooyour account in hello **Stopped** state.</span></span> <span data-ttu-id="1858c-121">串流處理您的內容，並採取利用動態封裝和動態加密，toostart hello 串流端點，您想要從中 toostream 內容已經在 hello toobe**執行**狀態。</span><span class="sxs-lookup"><span data-stu-id="1858c-121">toostart streaming your content and take advantage of dynamic packaging and dynamic encryption, hello streaming endpoint from which you want toostream content has toobe in hello **Running** state.</span></span> 

<span data-ttu-id="1858c-122">toostart hello 串流端點，請執行下列 hello:</span><span class="sxs-lookup"><span data-stu-id="1858c-122">toostart hello streaming endpoint, do hello following:</span></span>

1. <span data-ttu-id="1858c-123">在 [hello 登入[Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="1858c-123">Log in at hello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="1858c-124">在 [hello 設定視窗中，按一下 [串流端點。</span><span class="sxs-lookup"><span data-stu-id="1858c-124">In hello Settings window, click Streaming endpoints.</span></span> 
3. <span data-ttu-id="1858c-125">按一下 hello 預設串流端點。</span><span class="sxs-lookup"><span data-stu-id="1858c-125">Click hello default streaming endpoint.</span></span> 

    <span data-ttu-id="1858c-126">hello 預設串流端點詳細資料] 視窗隨即出現。</span><span class="sxs-lookup"><span data-stu-id="1858c-126">hello DEFAULT STREAMING ENDPOINT DETAILS window appears.</span></span>

4. <span data-ttu-id="1858c-127">按一下 hello 入門圖示。</span><span class="sxs-lookup"><span data-stu-id="1858c-127">Click hello Start icon.</span></span>
5. <span data-ttu-id="1858c-128">按一下 hello 儲存按鈕 toosave 您的變更。</span><span class="sxs-lookup"><span data-stu-id="1858c-128">Click hello Save button toosave your changes.</span></span>

## <a name="upload-files"></a><span data-ttu-id="1858c-129">上傳檔案</span><span class="sxs-lookup"><span data-stu-id="1858c-129">Upload files</span></span>
<span data-ttu-id="1858c-130">toostream 使用 Azure Media Services 的視訊，您需要 tooupload hello 來源視訊編碼多個位元，並發行 hello 結果。</span><span class="sxs-lookup"><span data-stu-id="1858c-130">toostream videos using Azure Media Services, you need tooupload hello source videos, encode them into multiple bitrates, and publish hello result.</span></span> <span data-ttu-id="1858c-131">本章節涵蓋 hello 第一個步驟。</span><span class="sxs-lookup"><span data-stu-id="1858c-131">hello first step is covered in this section.</span></span> 

1. <span data-ttu-id="1858c-132">在 [hello**設定**視窗中，按一下 [**資產**。</span><span class="sxs-lookup"><span data-stu-id="1858c-132">In hello **Setting** window, click **Assets**.</span></span>
   
    ![上傳檔案](./media/media-services-portal-vod-get-started/media-services-upload.png)
2. <span data-ttu-id="1858c-134">按一下 hello**上傳**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="1858c-134">Click hello **Upload** button.</span></span>
   
    <span data-ttu-id="1858c-135">hello**上載視訊資產**] 視窗隨即出現。</span><span class="sxs-lookup"><span data-stu-id="1858c-135">hello **Upload a video asset** window appears.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="1858c-136">檔案大小不受限。</span><span class="sxs-lookup"><span data-stu-id="1858c-136">There is no file size limitation.</span></span>
   > 
   > 
3. <span data-ttu-id="1858c-137">瀏覽您的電腦上的預期 toohello 視訊、 加以選取，並點擊 [確定]。</span><span class="sxs-lookup"><span data-stu-id="1858c-137">Browse toohello desired video on your computer, select it, and hit OK.</span></span>  
   
    <span data-ttu-id="1858c-138">hello 上載啟動，而且您可以看見 hello 進度 hello 檔名底下。</span><span class="sxs-lookup"><span data-stu-id="1858c-138">hello upload starts and you can see hello progress under hello file name.</span></span>  

<span data-ttu-id="1858c-139">Hello 上傳完成之後，您會看到 hello hello 中所列的新資產**資產**視窗。</span><span class="sxs-lookup"><span data-stu-id="1858c-139">Once hello upload completes, you see hello new asset listed in hello **Assets** window.</span></span> 

## <a name="encode-assets"></a><span data-ttu-id="1858c-140">為資產編碼</span><span class="sxs-lookup"><span data-stu-id="1858c-140">Encode assets</span></span>

<span data-ttu-id="1858c-141">當使用 Azure Media Services hello 最常見的案例之一傳遞彈性位元速率串流 tooyour 用戶端。</span><span class="sxs-lookup"><span data-stu-id="1858c-141">When working with Azure Media Services one of hello most common scenarios is delivering adaptive bitrate streaming tooyour clients.</span></span> <span data-ttu-id="1858c-142">Media Services 支援下列彈性位元速率串流技術的 hello: HTTP Live Streaming (HLS)，Smooth Streaming、 MPEG DASH。</span><span class="sxs-lookup"><span data-stu-id="1858c-142">Media Services supports hello following adaptive bitrate streaming technologies: HTTP Live Streaming (HLS), Smooth Streaming, MPEG DASH.</span></span> <span data-ttu-id="1858c-143">tooprepare 視訊彈性位元速率串流，您需要 tooencode 您的來源視訊多位元速率檔案。</span><span class="sxs-lookup"><span data-stu-id="1858c-143">tooprepare your videos for adaptive bitrate streaming, you need tooencode your source video into multi-bitrate files.</span></span> <span data-ttu-id="1858c-144">您應該使用 hello**媒體編碼器標準**編碼器 tooencode 視訊。</span><span class="sxs-lookup"><span data-stu-id="1858c-144">You should use hello **Media Encoder Standard** encoder tooencode your videos.</span></span>  

<span data-ttu-id="1858c-145">Media Services 也提供動態封裝，可讓您 toodeliver 中遵循的串流格式 hello 您多位元速率 mp4 集： MPEG DASH、 HLS、 Smooth Streaming，不需要您 toorepackage 到這些資料流的格式。</span><span class="sxs-lookup"><span data-stu-id="1858c-145">Media Services also provides dynamic packaging, which allows you toodeliver your multi-bitrate MP4s in hello following streaming formats: MPEG DASH, HLS, Smooth Streaming, without you having toorepackage into these streaming formats.</span></span> <span data-ttu-id="1858c-146">使用動態封裝，您只需要 toostore 及支付一種儲存格式，以及 Media Services 中的 hello 檔案建置，並提供服務 hello 適當的回應，根據用戶端的要求。</span><span class="sxs-lookup"><span data-stu-id="1858c-146">With dynamic packaging, you only need toostore and pay for hello files in single storage format and Media Services builds and serves hello appropriate response based on requests from a client.</span></span>

<span data-ttu-id="1858c-147">tootake 利用動態封裝，您需要 tooencode 原始程式檔成一組多位元速率 MP4 檔案 （hello 編碼步驟會示範稍後這一節）。</span><span class="sxs-lookup"><span data-stu-id="1858c-147">tootake advantage of dynamic packaging, you need tooencode your source file into a set of multi-bitrate MP4 files (hello encoding steps are demonstrated later in this section).</span></span>

### <a name="toouse-hello-portal-tooencode"></a><span data-ttu-id="1858c-148">toouse hello 入口 tooencode</span><span class="sxs-lookup"><span data-stu-id="1858c-148">toouse hello portal tooencode</span></span>
<span data-ttu-id="1858c-149">本章節描述 hello 步驟可讓您 tooencode 媒體編碼器標準內容。</span><span class="sxs-lookup"><span data-stu-id="1858c-149">This section describes hello steps you can take tooencode your content with Media Encoder Standard.</span></span>

1. <span data-ttu-id="1858c-150">在 [hello**設定**視窗中，選取**資產**。</span><span class="sxs-lookup"><span data-stu-id="1858c-150">In hello **Settings** window, select **Assets**.</span></span>  
2. <span data-ttu-id="1858c-151">在 [hello**資產**視窗中，您想要 tooencode 選取 hello 資產。</span><span class="sxs-lookup"><span data-stu-id="1858c-151">In hello **Assets** window, select hello asset that you would like tooencode.</span></span>
3. <span data-ttu-id="1858c-152">按 hello**編碼**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="1858c-152">Press hello **Encode** button.</span></span>
4. <span data-ttu-id="1858c-153">在 [hello**編碼資產**視窗中選取 hello 「 媒體編碼器標準 」 的處理器，並預先設定。</span><span class="sxs-lookup"><span data-stu-id="1858c-153">In hello **Encode an asset** window, select hello "Media Encoder Standard" processor and a preset.</span></span> <span data-ttu-id="1858c-154">如需預設值的相關資訊，請參閱[自動產生的位元速率排行榜](media-services-autogen-bitrate-ladder-with-mes.md)和 [MES 的工作預設值](media-services-mes-presets-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="1858c-154">For information about presets, see [auto-generate a bitrate ladder](media-services-autogen-bitrate-ladder-with-mes.md) and [Task Presets for MES](media-services-mes-presets-overview.md).</span></span> <span data-ttu-id="1858c-155">如果您打算使用的編碼預設 toocontrol，記住這： 請務必 tooselect hello 預先設定的最適合您輸入的視訊。</span><span class="sxs-lookup"><span data-stu-id="1858c-155">If you plan toocontrol which encoding preset is used, keep this in mind: it is important tooselect hello preset that is most appropriate for your input video.</span></span> <span data-ttu-id="1858c-156">比方說，如果您知道輸入的視訊具有 1920 x 1080 像素的解析度，然後您可以使用 hello"H264 多重位元速率 1080p 」 預設。</span><span class="sxs-lookup"><span data-stu-id="1858c-156">For example, if you know your input video has a resolution of 1920x1080 pixels, then you could use hello "H264 Multiple Bitrate 1080p" preset.</span></span> <span data-ttu-id="1858c-157">如果您有低解析度 (640x360) 視訊，則不應該使用 [H264 多重位元速率 1080p] 預設值。</span><span class="sxs-lookup"><span data-stu-id="1858c-157">If you have a low resolution (640x360) video, then you should not be using "H264 Multiple Bitrate 1080p" preset.</span></span>
   
   <span data-ttu-id="1858c-158">為了方便管理，您必須編輯 hello 名稱 hello 輸出資產，以及 hello hello 作業名稱的選項。</span><span class="sxs-lookup"><span data-stu-id="1858c-158">For easier management, you have an option of editing hello name of hello output asset, and hello name of hello job.</span></span>
   
   ![為資產編碼](./media/media-services-portal-vod-get-started/media-services-encode1.png)
5. <span data-ttu-id="1858c-160">按下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="1858c-160">Press **Create**.</span></span>

### <a name="monitor-encoding-job-progress"></a><span data-ttu-id="1858c-161">監視編碼作業進度</span><span class="sxs-lookup"><span data-stu-id="1858c-161">Monitor encoding job progress</span></span>
<span data-ttu-id="1858c-162">toomonitor hello 進度 hello 編碼作業中，按一下**設定**（hello 頁面頂端的 hello），然後選取 [**作業**。</span><span class="sxs-lookup"><span data-stu-id="1858c-162">toomonitor hello progress of hello encoding job, click **Settings** (at hello top of hello page) and then select **Jobs**.</span></span>

![工作](./media/media-services-portal-vod-get-started/media-services-jobs.png)

## <a name="publish-content"></a><span data-ttu-id="1858c-164">發佈內容</span><span class="sxs-lookup"><span data-stu-id="1858c-164">Publish content</span></span>
<span data-ttu-id="1858c-165">tooprovide 您一個 url，也可以使用的 toostream 或下載您的內容的使用者，您首先需要太 「 發行 」 您的資產建立定位器。</span><span class="sxs-lookup"><span data-stu-id="1858c-165">tooprovide your user with a  URL that can be used toostream or download your content, you first need too"publish" your asset by creating a locator.</span></span> <span data-ttu-id="1858c-166">定位器提供存取 toofiles hello 資產中所包含。</span><span class="sxs-lookup"><span data-stu-id="1858c-166">Locators provide access toofiles contained in hello asset.</span></span> <span data-ttu-id="1858c-167">媒體服務支援兩種類型的定位器：</span><span class="sxs-lookup"><span data-stu-id="1858c-167">Media Services supports two types of locators:</span></span> 

* <span data-ttu-id="1858c-168">資料流 (OnDemandOrigin) 定位器，用於彈性資料流 （例如，toostream MPEG DASH、 HLS 或 Smooth Streaming）。</span><span class="sxs-lookup"><span data-stu-id="1858c-168">Streaming (OnDemandOrigin) locators, used for adaptive streaming (for example, toostream MPEG DASH, HLS, or Smooth Streaming).</span></span> <span data-ttu-id="1858c-169">toocreate 串流定位器資產必須包含.ism 檔案。</span><span class="sxs-lookup"><span data-stu-id="1858c-169">toocreate a streaming locator your asset must contain an .ism file.</span></span> 
* <span data-ttu-id="1858c-170">漸進式 (SAS) 定位器，用於透過漸進式下載傳遞視訊。</span><span class="sxs-lookup"><span data-stu-id="1858c-170">Progressive (SAS) locators, used for delivery of video via progressive download.</span></span>

<span data-ttu-id="1858c-171">串流 URL 具有下列格式的 hello，您可以使用它 tooplay Smooth Streaming 資產。</span><span class="sxs-lookup"><span data-stu-id="1858c-171">A streaming URL has hello following format and you can use it tooplay Smooth Streaming assets.</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest

<span data-ttu-id="1858c-172">附加 toobuild 的 HLS 資料流 URL (格式 = m3u8 aapl) toohello URL。</span><span class="sxs-lookup"><span data-stu-id="1858c-172">toobuild an HLS streaming URL, append (format=m3u8-aapl) toohello URL.</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=m3u8-aapl)

<span data-ttu-id="1858c-173">附加 toobuild 的 MPEG DASH 串流 URL (格式 = mpd-時間-csf) toohello URL。</span><span class="sxs-lookup"><span data-stu-id="1858c-173">toobuild an  MPEG DASH streaming URL, append (format=mpd-time-csf) toohello URL.</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=mpd-time-csf)


<span data-ttu-id="1858c-174">SAS URL 具有下列格式的 hello。</span><span class="sxs-lookup"><span data-stu-id="1858c-174">A SAS URL has hello following format.</span></span>

    {blob container name}/{asset name}/{file name}/{SAS signature}

> [!NOTE]
> <span data-ttu-id="1858c-175">如果您使用 hello 入口 toocreate 定位器 2015 年 3 月之前，會建立定位器以兩年到期日。</span><span class="sxs-lookup"><span data-stu-id="1858c-175">If you used hello portal toocreate locators before March 2015, locators with a two-year expiration date were created.</span></span>  
> 
> 

<span data-ttu-id="1858c-176">定位器時，使用上的到期日 tooupdate [REST](https://docs.microsoft.com/rest/api/media/operations/locator#update_a_locator)或[.NET](http://go.microsoft.com/fwlink/?LinkID=533259)應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="1858c-176">tooupdate an expiration date on a locator, use [REST](https://docs.microsoft.com/rest/api/media/operations/locator#update_a_locator) or [.NET](http://go.microsoft.com/fwlink/?LinkID=533259) APIs.</span></span> <span data-ttu-id="1858c-177">當您更新的 SAS 定位器的 hello 到期日時，hello URL 將會變更。</span><span class="sxs-lookup"><span data-stu-id="1858c-177">When you update hello expiration date of a SAS locator, hello URL changes.</span></span>

### <a name="toouse-hello-portal-toopublish-an-asset"></a><span data-ttu-id="1858c-178">toouse hello 入口 toopublish 資產</span><span class="sxs-lookup"><span data-stu-id="1858c-178">toouse hello portal toopublish an asset</span></span>
<span data-ttu-id="1858c-179">toouse hello 入口 toopublish 資產，請勿 hello 遵循：</span><span class="sxs-lookup"><span data-stu-id="1858c-179">toouse hello portal toopublish an asset, do hello following:</span></span>

1. <span data-ttu-id="1858c-180">選取 **設定** > **資產**。</span><span class="sxs-lookup"><span data-stu-id="1858c-180">Select **Settings** > **Assets**.</span></span>
2. <span data-ttu-id="1858c-181">選取您想 toopublish hello 資產。</span><span class="sxs-lookup"><span data-stu-id="1858c-181">Select hello asset that you want toopublish.</span></span>
3. <span data-ttu-id="1858c-182">按一下 hello**發行**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="1858c-182">Click hello **Publish** button.</span></span>
4. <span data-ttu-id="1858c-183">選取 hello 定位器類型。</span><span class="sxs-lookup"><span data-stu-id="1858c-183">Select hello locator type.</span></span>
5. <span data-ttu-id="1858c-184">按 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="1858c-184">Press **Add**.</span></span>
   
    ![發佈](./media/media-services-portal-vod-get-started/media-services-publish1.png)

<span data-ttu-id="1858c-186">hello URL 加入 toohello 清單**發行 Url**。</span><span class="sxs-lookup"><span data-stu-id="1858c-186">hello URL is added toohello list of **Published URLs**.</span></span>

## <a name="play-content-from-hello-portal"></a><span data-ttu-id="1858c-187">播放內容從 hello 入口網站</span><span class="sxs-lookup"><span data-stu-id="1858c-187">Play content from hello portal</span></span>
<span data-ttu-id="1858c-188">hello Azure 入口網站提供內容的播放程式，您可以使用 tootest 視訊。</span><span class="sxs-lookup"><span data-stu-id="1858c-188">hello Azure portal provides a content player that you can use tootest your video.</span></span>

<span data-ttu-id="1858c-189">按一下想要的 hello 視訊，然後按一下 [hello**播放**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="1858c-189">Click hello desired video and then click hello **Play** button.</span></span>

![發佈](./media/media-services-portal-vod-get-started/media-services-play.png)

<span data-ttu-id="1858c-191">適用一些考量事項：</span><span class="sxs-lookup"><span data-stu-id="1858c-191">Some considerations apply:</span></span>

* <span data-ttu-id="1858c-192">資料流，toobegin 開始執行 hello**預設**串流端點。</span><span class="sxs-lookup"><span data-stu-id="1858c-192">toobegin streaming, start running hello **default** streaming endpoint.</span></span>
* <span data-ttu-id="1858c-193">請確定已發佈視訊 hello。</span><span class="sxs-lookup"><span data-stu-id="1858c-193">Make sure hello video has been published.</span></span>
* <span data-ttu-id="1858c-194">這**Media player**播放從 hello 預設串流端點。</span><span class="sxs-lookup"><span data-stu-id="1858c-194">This **Media player** plays from hello default streaming endpoint.</span></span> <span data-ttu-id="1858c-195">如果您想 tooplay 從非預設串流端點，按一下 [toocopy hello URL，並使用其他播放器。</span><span class="sxs-lookup"><span data-stu-id="1858c-195">If you want tooplay from a non-default streaming endpoint, click toocopy hello URL and use another player.</span></span> <span data-ttu-id="1858c-196">例如， [Azure 媒體服務播放器](http://amsplayer.azurewebsites.net/azuremediaplayer.html)。</span><span class="sxs-lookup"><span data-stu-id="1858c-196">For example, [Azure Media Services Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span></span>

## <a name="next-steps"></a><span data-ttu-id="1858c-197">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1858c-197">Next steps</span></span>
<span data-ttu-id="1858c-198">檢閱媒體服務學習路徑。</span><span class="sxs-lookup"><span data-stu-id="1858c-198">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="1858c-199">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="1858c-199">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

