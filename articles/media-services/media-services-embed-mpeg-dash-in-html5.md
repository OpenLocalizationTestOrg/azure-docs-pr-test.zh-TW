---
title: "aaaEmbedding MPEG-DASH 自動調整串流影片中具有 DASH.js 的 HTML5 應用程式 |Microsoft 文件"
description: "本主題示範如何 tooembed MPEG-DASH 自動調整串流影片具有 DASH.js 的 HTML5 應用程式中。"
author: Juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: 5aa0e7b6-f5c3-4cc1-aa33-ed16ea4780c2
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/26/2016
ms.author: juliako
ms.openlocfilehash: a73713d20f95262654532b94576ae9669d829354
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="embedding-a-mpeg-dash-adaptive-streaming-video-in-an-html5-application-with-dashjs"></a><span data-ttu-id="8385b-103">透過 DASH.js 將 MPEG-DASH 彈性資料流視訊嵌入到 HTML5 應用程式</span><span class="sxs-lookup"><span data-stu-id="8385b-103">Embedding a MPEG-DASH Adaptive Streaming Video in an HTML5 Application with DASH.js</span></span>
## <a name="overview"></a><span data-ttu-id="8385b-104">概觀</span><span class="sxs-lookup"><span data-stu-id="8385b-104">Overview</span></span>
<span data-ttu-id="8385b-105">MPEG DASH 是 ISO 標準 hello 彈性的視訊內容，提供重要的優點的人員想 toodeliver 高品質且可調整視訊串流處理輸出資料流。</span><span class="sxs-lookup"><span data-stu-id="8385b-105">MPEG-DASH is an ISO standard for hello adaptive streaming of video content, which offers significant benefits for those who wish toodeliver high-quality, adaptive video streaming output.</span></span> <span data-ttu-id="8385b-106">MPEG DASH，與 hello 視訊資料流將會自動卸除 tooa 低定義 hello 網路變得壅塞時。</span><span class="sxs-lookup"><span data-stu-id="8385b-106">With MPEG-DASH, hello video stream will automatically drop tooa lower definition when hello network becomes congested.</span></span> <span data-ttu-id="8385b-107">這會減少 hello hello 播放程式會下載 hello 接下來幾秒 tooplay （也稱為緩衝處理） 時看到 「 暫停 」 的視訊 hello 檢視器的可能性。</span><span class="sxs-lookup"><span data-stu-id="8385b-107">This reduces hello likelihood of hello viewer seeing a "paused" video while hello player downloads hello next few seconds tooplay (aka buffering).</span></span> <span data-ttu-id="8385b-108">當網路壅塞會降低，hello 影片播放器接著會傳回 tooa 高品質資料流。</span><span class="sxs-lookup"><span data-stu-id="8385b-108">As network congestion reduces, hello video player will in turn return tooa higher quality stream.</span></span> <span data-ttu-id="8385b-109">需要此功能 tooadapt hello 頻寬也會導致更快速的開始時間讓視訊。</span><span class="sxs-lookup"><span data-stu-id="8385b-109">This ability tooadapt hello bandwidth required also results in a faster start time for video.</span></span> <span data-ttu-id="8385b-110">表示 hello 幾秒可以播放 fast-下載較低品質區段中，一旦已緩衝處理足夠的內容，然後逐步 tooa 愈高，品質設定。</span><span class="sxs-lookup"><span data-stu-id="8385b-110">That means that hello first few seconds can be played in a fast-to-download lower quality segment and then step up tooa higher quality once sufficient content has been buffered.</span></span>

<span data-ttu-id="8385b-111">Dash.js 是以 JavaScript 撰寫的開放原始碼 MPEG-DASH 視訊播放程式。</span><span class="sxs-lookup"><span data-stu-id="8385b-111">Dash.js is an open source MPEG-DASH video player written in JavaScript.</span></span> <span data-ttu-id="8385b-112">其目的是 tooprovide 強固且能跨平台的播放程式可以在需要視訊播放的應用程式中自由地重複使用。</span><span class="sxs-lookup"><span data-stu-id="8385b-112">Its goal is tooprovide a robust, cross-platform player that can be freely reused in applications that require video playback.</span></span> <span data-ttu-id="8385b-113">它提供 MPEG-DASH 播放支援 hello W3C 媒體來源延伸模組 (MSE)，現今也就是 Chrome、 Microsoft Edge 和 IE11 （其他瀏覽器已指出其意圖 toosupport MSE） 的任何瀏覽器中。</span><span class="sxs-lookup"><span data-stu-id="8385b-113">It provides MPEG-DASH playback in any browser that supports hello W3C Media Source Extensions (MSE), today that is Chrome, Microsoft Edge and IE11 (other browsers have indicated their intent toosupport MSE).</span></span> <span data-ttu-id="8385b-114">Js DASH.js 的詳細資訊，請參閱 hello GitHub dash.js 儲存機制。</span><span class="sxs-lookup"><span data-stu-id="8385b-114">For more information about DASH.js, js see hello GitHub dash.js repository.</span></span>

## <a name="creating-a-browser-based-streaming-video-player"></a><span data-ttu-id="8385b-115">建立以瀏覽器為基礎的資料流視訊播放程式</span><span class="sxs-lookup"><span data-stu-id="8385b-115">Creating a browser-based streaming video player</span></span>
<span data-ttu-id="8385b-116">toocreate 簡單的 web 網頁會顯示以 hello 預期影片播放器控制這類播放、 暫停、 倒帶等，您將需要：</span><span class="sxs-lookup"><span data-stu-id="8385b-116">toocreate a simple web page that displays a video player with hello expected controls such a play, pause, rewind etc., you will need to:</span></span>

1. <span data-ttu-id="8385b-117">建立 HTML 網頁</span><span class="sxs-lookup"><span data-stu-id="8385b-117">Create an HTML page</span></span>
2. <span data-ttu-id="8385b-118">新增 hello 視訊標記</span><span class="sxs-lookup"><span data-stu-id="8385b-118">Add hello video tag</span></span>
3. <span data-ttu-id="8385b-119">新增 hello dash.js 播放程式</span><span class="sxs-lookup"><span data-stu-id="8385b-119">Add hello dash.js player</span></span>
4. <span data-ttu-id="8385b-120">初始化 hello 播放程式</span><span class="sxs-lookup"><span data-stu-id="8385b-120">Initialize hello player</span></span>
5. <span data-ttu-id="8385b-121">新增部分 CSS 樣式</span><span class="sxs-lookup"><span data-stu-id="8385b-121">Add some CSS style</span></span>
6. <span data-ttu-id="8385b-122">實作 MSE 的瀏覽器中檢視 hello 結果</span><span class="sxs-lookup"><span data-stu-id="8385b-122">View hello results in a browser that implements MSE</span></span>

<span data-ttu-id="8385b-123">正在初始化 hello 播放程式可以完成在只要少數的 JavaScript 程式碼行。</span><span class="sxs-lookup"><span data-stu-id="8385b-123">Initializing hello player can be completed in just a handful of lines of JavaScript code.</span></span> <span data-ttu-id="8385b-124">它使用 dash.js，確實是在瀏覽器型應用程式中的簡單 tooembed MPEG-DASH 視訊。</span><span class="sxs-lookup"><span data-stu-id="8385b-124">Using dash.js, it really is that simple tooembed MPEG-DASH video in your browser based applications.</span></span>

## <a name="creating-hello-html-page"></a><span data-ttu-id="8385b-125">建立 hello HTML 網頁</span><span class="sxs-lookup"><span data-stu-id="8385b-125">Creating hello HTML Page</span></span>
<span data-ttu-id="8385b-126">hello 第一個步驟是包含 hello toocreate 標準 HTML 頁面**視訊**項目，這個檔案儲存為 basicPlayer.html，為 hello 下列範例將說明：</span><span class="sxs-lookup"><span data-stu-id="8385b-126">hello first step is toocreate a standard HTML page containing hello **video** element, save this file as basicPlayer.html, as hello following example illustrates:</span></span>

    <!DOCTYPE html>
    <html>
      <head><title>Adaptive Streaming in HTML5</title></head>
      <body>
        <h1>Adaptive Streaming with HTML5</h1>
        <video id="videoplayer" controls></video>
      </body>
    </html>

## <a name="adding-hello-dashjs-player"></a><span data-ttu-id="8385b-127">新增 hello DASH.js 播放程式</span><span class="sxs-lookup"><span data-stu-id="8385b-127">Adding hello DASH.js Player</span></span>
<span data-ttu-id="8385b-128">tooadd hello dash.js 參考實作 toohello 應用程式，您將需要從 dash.js 專案 hello 1.0 版本 toograb hello dash.all.js 檔案。</span><span class="sxs-lookup"><span data-stu-id="8385b-128">tooadd hello dash.js reference implementation toohello application, you’ll need toograb hello dash.all.js file from hello 1.0 release of dash.js project.</span></span> <span data-ttu-id="8385b-129">這應該會儲存在您的應用程式的 hello JavaScript 資料夾。</span><span class="sxs-lookup"><span data-stu-id="8385b-129">This should be saved in hello JavaScript folder of your application.</span></span> <span data-ttu-id="8385b-130">這個檔案是必須綜覽所有 hello 必要 dash.js 程式碼到單一檔案的便利性檔案。</span><span class="sxs-lookup"><span data-stu-id="8385b-130">This file is a convenience file that pulls together all hello necessary dash.js code into a single file.</span></span> <span data-ttu-id="8385b-131">如果您有一起來看看周圍 hello dash.js 儲存機制時，會尋找 hello 個別檔案，請測試程式碼和更多，但是，如果您想 toodo 使用 dash.js 則 hello dash.all.js 檔案就是您的需要。</span><span class="sxs-lookup"><span data-stu-id="8385b-131">If you have a look around hello dash.js repository, you will find hello individual files, test code and much more, but if all you want toodo is use dash.js, then hello dash.all.js file is what you need.</span></span>

<span data-ttu-id="8385b-132">tooadd hello dash.js player tooyour 應用程式，新增 basicPlayer.html 指令碼標記 toohello 標頭區段：</span><span class="sxs-lookup"><span data-stu-id="8385b-132">tooadd hello dash.js player tooyour applications, add a script tag toohello head section of basicPlayer.html:</span></span>

    <!-- DASH-AVC/265 reference implementation -->
    < script src="js/dash.all.js"></script>


<span data-ttu-id="8385b-133">Hello 網頁載入時，接下來，建立函式 tooinitialize hello 播放程式。</span><span class="sxs-lookup"><span data-stu-id="8385b-133">Next, create a function tooinitialize hello player when hello page loads.</span></span> <span data-ttu-id="8385b-134">加入下列指令碼之後您可以在其中載入 dash.all.js hello 列, hello:</span><span class="sxs-lookup"><span data-stu-id="8385b-134">Add hello following script after hello line in which you load dash.all.js:</span></span>

    <script>
    // setup hello video element and attach it toohello Dash player
    function setupVideo() {
      var url = "http://wams.edgesuite.net/media/MPTExpressionData02/BigBuckBunny_1080p24_IYUV_2ch.ism/manifest(format=mpd-time-csf)";
      var context = new Dash.di.DashContext();
      var player = new MediaPlayer(context);
                      player.startup();
                      player.attachView(document.querySelector("#videoplayer"));
                      player.attachSource(url);
    }
    </script>

<span data-ttu-id="8385b-135">此函式會先建立 DashContext。</span><span class="sxs-lookup"><span data-stu-id="8385b-135">This function first creates a DashContext.</span></span> <span data-ttu-id="8385b-136">這是針對特定執行階段環境使用的 tooconfigure hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="8385b-136">This is used tooconfigure hello application for a specific runtime environment.</span></span> <span data-ttu-id="8385b-137">從技術觀點來看，它會定義的 hello 建構 hello 應用程式時，應該使用 hello 相依性插入架構的類別。</span><span class="sxs-lookup"><span data-stu-id="8385b-137">From a technical point of view, it defines hello classes that hello dependency injection framework should use when constructing hello application.</span></span> <span data-ttu-id="8385b-138">在大部分情況下，您會使用 Dash.di.DashContext。</span><span class="sxs-lookup"><span data-stu-id="8385b-138">In most cases, you will use Dash.di.DashContext.</span></span>

<span data-ttu-id="8385b-139">接下來，具現化 hello dash.js framework MediaPlayer hello 主要的類別。</span><span class="sxs-lookup"><span data-stu-id="8385b-139">Next, instantiate hello primary class of hello dash.js framework, MediaPlayer.</span></span> <span data-ttu-id="8385b-140">這個類別包含 hello 核心方法需要這類播放和暫停、 管理 hello hello video 項目關聯性，並也會管理 hello 媒體呈現描述 (MPD) 檔描述 hello 播放的視訊 toobe hello 解譯。</span><span class="sxs-lookup"><span data-stu-id="8385b-140">This class contains hello core methods needed such as play and pause, manages hello relationship with hello video element and also manages hello interpretation of hello Media Presentation Description (MPD) file which describes hello video toobe played.</span></span>

<span data-ttu-id="8385b-141">hello startup （） 函式的 hello MediaPlayer 類別稱為 tooensure 這 hello 位玩家已準備好 tooplay 視訊。</span><span class="sxs-lookup"><span data-stu-id="8385b-141">hello startup() function of hello MediaPlayer class is called tooensure that hello player is ready tooplay video.</span></span> <span data-ttu-id="8385b-142">其他項目在這個函式可確保，所有的 hello 必要的類別 （如 hello 內容所定義） 已載入。</span><span class="sxs-lookup"><span data-stu-id="8385b-142">Amongst other things this function ensures that all hello necessary classes (as defined by hello context) have been loaded.</span></span> <span data-ttu-id="8385b-143">Hello 播放程式準備就緒之後，您可以附加 hello video 項目 tooit 使用 hello attachView() 函式。</span><span class="sxs-lookup"><span data-stu-id="8385b-143">Once hello player is ready, you can attach hello video element tooit using hello attachView() function.</span></span> <span data-ttu-id="8385b-144">如此會啟用 hello MediaPlayer tooinject hello 視訊串流至 hello 項目，並也控制在必要時播放。</span><span class="sxs-lookup"><span data-stu-id="8385b-144">This enables hello MediaPlayer tooinject hello video stream into hello element and also control playback as necessary.</span></span>

<span data-ttu-id="8385b-145">傳遞的 hello MPD 檔案 toohello MediaPlayer hello URL，以便它所知道 hello 影片 end_time< 剛才建立的 tooplay.hello setupVideo() 函式需要 toobe hello 頁面完全載入後執行。</span><span class="sxs-lookup"><span data-stu-id="8385b-145">Pass hello URL of hello MPD file toohello MediaPlayer so that it knows about hello video it is expected tooplay.hello setupVideo() function just created will need toobe executed once hello page has fully loaded.</span></span> <span data-ttu-id="8385b-146">藉由使用 hello body 元素的 hello onload 事件執行這項操作。</span><span class="sxs-lookup"><span data-stu-id="8385b-146">Do this by using hello onload event of hello body element.</span></span> <span data-ttu-id="8385b-147">將 <body> 元素變更為：</span><span class="sxs-lookup"><span data-stu-id="8385b-147">Change your <body> element to:</span></span>

    <body onload="setupVideo()">

<span data-ttu-id="8385b-148">最後，設定 hello 視訊元素的 CSS hello 大小。</span><span class="sxs-lookup"><span data-stu-id="8385b-148">Finally, set hello size of hello video element using CSS.</span></span> <span data-ttu-id="8385b-149">在自動調整串流處理環境中，這是特別重要因為 hello 大小 hello 視訊播放播放會調整 toochanging 網路狀況可能會變更。</span><span class="sxs-lookup"><span data-stu-id="8385b-149">In an adaptive streaming environment, this is especially important because hello size of hello video being played may change as playback adapts toochanging network conditions.</span></span> <span data-ttu-id="8385b-150">在這個簡單的示範只強制 hello video 項目 toobe hello 可用的瀏覽器視窗的 80%藉由新增下列 CSS toohello 前端 hello 頁面區段的 hello:</span><span class="sxs-lookup"><span data-stu-id="8385b-150">In this simple demo simply force hello video element toobe 80% of hello available browser window by adding hello following CSS toohello head section of hello page:</span></span>

    <style>
    video {
      width: 80%;
      height: 80%;
    }
    </style>

## <a name="playing-a-video"></a><span data-ttu-id="8385b-151">播放視訊</span><span class="sxs-lookup"><span data-stu-id="8385b-151">Playing a Video</span></span>
<span data-ttu-id="8385b-152">tooplay 視訊，指向您的瀏覽器在 hello basicPlayback.html 檔案，然後按一下 顯示 hello 影片播放器上的播放。</span><span class="sxs-lookup"><span data-stu-id="8385b-152">tooplay a video, point your browser at hello basicPlayback.html file and click play on hello video player displayed.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="8385b-153">媒體服務學習路徑</span><span class="sxs-lookup"><span data-stu-id="8385b-153">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="8385b-154">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="8385b-154">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="8385b-155">另請參閱</span><span class="sxs-lookup"><span data-stu-id="8385b-155">See Also</span></span>
[<span data-ttu-id="8385b-156">開發視訊播放程式應用程式</span><span class="sxs-lookup"><span data-stu-id="8385b-156">Develop video player applications</span></span>](media-services-develop-video-players.md)

[<span data-ttu-id="8385b-157">GitHub dash.js 存放庫</span><span class="sxs-lookup"><span data-stu-id="8385b-157">GitHub dash.js repository</span></span>](https://github.com/Dash-Industry-Forum/dash.js) 

