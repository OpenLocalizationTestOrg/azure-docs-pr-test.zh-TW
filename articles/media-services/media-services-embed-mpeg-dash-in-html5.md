---
title: "透過 DASH.js 將 MPEG-DASH 彈性資料流視訊嵌入到 HTML5 應用程式 | Microsoft Docs"
description: "本主題示範如何使用 DASH.js 在 HTML5 應用程式中嵌入 MPEG-DASH 彈性資料流視訊。"
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
ms.openlocfilehash: 27ce6325773ba1f9fd9cd9ab9e07ea9f5e2488ac
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="embedding-a-mpeg-dash-adaptive-streaming-video-in-an-html5-application-with-dashjs"></a><span data-ttu-id="8a76f-103">透過 DASH.js 將 MPEG-DASH 彈性資料流視訊嵌入到 HTML5 應用程式</span><span class="sxs-lookup"><span data-stu-id="8a76f-103">Embedding a MPEG-DASH Adaptive Streaming Video in an HTML5 Application with DASH.js</span></span>
## <a name="overview"></a><span data-ttu-id="8a76f-104">Overview</span><span class="sxs-lookup"><span data-stu-id="8a76f-104">Overview</span></span>
<span data-ttu-id="8a76f-105">MPEG-DASH 符合 ISO 的視訊內容彈性資料流標準，能為想要傳遞高品質彈性視訊資料流輸出的人帶來相當大的幫助。</span><span class="sxs-lookup"><span data-stu-id="8a76f-105">MPEG-DASH is an ISO standard for the adaptive streaming of video content, which offers significant benefits for those who wish to deliver high-quality, adaptive video streaming output.</span></span> <span data-ttu-id="8a76f-106">透過 MPEG-DASH，視訊資料流在網路擁塞時會自動降至低畫質的內容。</span><span class="sxs-lookup"><span data-stu-id="8a76f-106">With MPEG-DASH, the video stream will automatically drop to a lower definition when the network becomes congested.</span></span> <span data-ttu-id="8a76f-107">這會減少檢視者在播放程式下載接下來數秒的播放內容 (亦即緩衝) 時，看到視訊「暫停」的可能性。</span><span class="sxs-lookup"><span data-stu-id="8a76f-107">This reduces the likelihood of the viewer seeing a "paused" video while the player downloads the next few seconds to play (aka buffering).</span></span> <span data-ttu-id="8a76f-108">當網路不再擁塞，視訊播放程式會改為高品質的資料流。</span><span class="sxs-lookup"><span data-stu-id="8a76f-108">As network congestion reduces, the video player will in turn return to a higher quality stream.</span></span> <span data-ttu-id="8a76f-109">這種調整所需頻寬的能力也會讓視訊的開始時間變快。</span><span class="sxs-lookup"><span data-stu-id="8a76f-109">This ability to adapt the bandwidth required also results in a faster start time for video.</span></span> <span data-ttu-id="8a76f-110">這表示會在快速下載但低品質區段中播放頭幾秒的內容，一旦已緩衝足夠的內容，就會升級為高品質內容。</span><span class="sxs-lookup"><span data-stu-id="8a76f-110">That means that the first few seconds can be played in a fast-to-download lower quality segment and then step up to a higher quality once sufficient content has been buffered.</span></span>

<span data-ttu-id="8a76f-111">Dash.js 是以 JavaScript 撰寫的開放原始碼 MPEG-DASH 視訊播放程式。</span><span class="sxs-lookup"><span data-stu-id="8a76f-111">Dash.js is an open source MPEG-DASH video player written in JavaScript.</span></span> <span data-ttu-id="8a76f-112">其目標是要在需要播放視訊的應用程式中，提供一個健全、跨平台、並可自由重複使用的播放程式。</span><span class="sxs-lookup"><span data-stu-id="8a76f-112">Its goal is to provide a robust, cross-platform player that can be freely reused in applications that require video playback.</span></span> <span data-ttu-id="8a76f-113">它可在任何支援 W3C Media Source Extensions (MSE) 的瀏覽器 (亦即今日的 Chrome、Microsoft Edge 與 IE11 ) 中播放 MPEG-DASH (其他瀏覽器已表示其支援 MSE 的用途)。</span><span class="sxs-lookup"><span data-stu-id="8a76f-113">It provides MPEG-DASH playback in any browser that supports the W3C Media Source Extensions (MSE), today that is Chrome, Microsoft Edge and IE11 (other browsers have indicated their intent to support MSE).</span></span> <span data-ttu-id="8a76f-114">如需 DASH.js 的詳細資訊，請參閱 GitHub dash.js 存放庫。</span><span class="sxs-lookup"><span data-stu-id="8a76f-114">For more information about DASH.js, js see the GitHub dash.js repository.</span></span>

## <a name="creating-a-browser-based-streaming-video-player"></a><span data-ttu-id="8a76f-115">建立以瀏覽器為基礎的資料流視訊播放程式</span><span class="sxs-lookup"><span data-stu-id="8a76f-115">Creating a browser-based streaming video player</span></span>
<span data-ttu-id="8a76f-116">若要建立簡單的網頁來顯示附有播放、暫停、倒轉等應有控制項的視訊播放器，您必須：</span><span class="sxs-lookup"><span data-stu-id="8a76f-116">To create a simple web page that displays a video player with the expected controls such a play, pause, rewind etc., you will need to:</span></span>

1. <span data-ttu-id="8a76f-117">建立 HTML 網頁</span><span class="sxs-lookup"><span data-stu-id="8a76f-117">Create an HTML page</span></span>
2. <span data-ttu-id="8a76f-118">新增視訊標記</span><span class="sxs-lookup"><span data-stu-id="8a76f-118">Add the video tag</span></span>
3. <span data-ttu-id="8a76f-119">新增 dash.js 播放程式</span><span class="sxs-lookup"><span data-stu-id="8a76f-119">Add the dash.js player</span></span>
4. <span data-ttu-id="8a76f-120">初始化播放程式</span><span class="sxs-lookup"><span data-stu-id="8a76f-120">Initialize the player</span></span>
5. <span data-ttu-id="8a76f-121">新增部分 CSS 樣式</span><span class="sxs-lookup"><span data-stu-id="8a76f-121">Add some CSS style</span></span>
6. <span data-ttu-id="8a76f-122">在實作 MSE 的瀏覽器中檢視結果</span><span class="sxs-lookup"><span data-stu-id="8a76f-122">View the results in a browser that implements MSE</span></span>

<span data-ttu-id="8a76f-123">只需數行的 JavaScript 程式碼，就能完成播放程式的初始化。</span><span class="sxs-lookup"><span data-stu-id="8a76f-123">Initializing the player can be completed in just a handful of lines of JavaScript code.</span></span> <span data-ttu-id="8a76f-124">使用 dash.js 其實很簡單，只要在以瀏覽器為基礎的應用程式中嵌入 MPEG-DASH 視訊即可。</span><span class="sxs-lookup"><span data-stu-id="8a76f-124">Using dash.js, it really is that simple to embed MPEG-DASH video in your browser based applications.</span></span>

## <a name="creating-the-html-page"></a><span data-ttu-id="8a76f-125">建立 HTML 網頁</span><span class="sxs-lookup"><span data-stu-id="8a76f-125">Creating the HTML Page</span></span>
<span data-ttu-id="8a76f-126">第一個步驟是建立一個包含**視訊**元素的標準 HTML 頁面，然後將此檔案儲存為 basicPlayer.html，如下列範例說明：</span><span class="sxs-lookup"><span data-stu-id="8a76f-126">The first step is to create a standard HTML page containing the **video** element, save this file as basicPlayer.html, as the following example illustrates:</span></span>

    <!DOCTYPE html>
    <html>
      <head><title>Adaptive Streaming in HTML5</title></head>
      <body>
        <h1>Adaptive Streaming with HTML5</h1>
        <video id="videoplayer" controls></video>
      </body>
    </html>

## <a name="adding-the-dashjs-player"></a><span data-ttu-id="8a76f-127">新增 DASH.js 播放程式</span><span class="sxs-lookup"><span data-stu-id="8a76f-127">Adding the DASH.js Player</span></span>
<span data-ttu-id="8a76f-128">若要將 dash.js 參考實作新增至該應用程式，您必須從 1.0 版的 dash.js 專案捕捉 dash.all.js 檔案。</span><span class="sxs-lookup"><span data-stu-id="8a76f-128">To add the dash.js reference implementation to the application, you’ll need to grab the dash.all.js file from the 1.0 release of dash.js project.</span></span> <span data-ttu-id="8a76f-129">這應該儲存在您應用程式的 JavaScript 資料夾中。</span><span class="sxs-lookup"><span data-stu-id="8a76f-129">This should be saved in the JavaScript folder of your application.</span></span> <span data-ttu-id="8a76f-130">此檔案可讓您很方便地將所有必要的 dash.js 程式碼提取到一個檔案中。</span><span class="sxs-lookup"><span data-stu-id="8a76f-130">This file is a convenience file that pulls together all the necessary dash.js code into a single file.</span></span> <span data-ttu-id="8a76f-131">如果您瀏覽過 dash.js 存放庫，就能發現各個檔案、測試程式碼等等，但如果您只是要使用 dash.js，那麼 dash.all.js 就是您所需的檔案。</span><span class="sxs-lookup"><span data-stu-id="8a76f-131">If you have a look around the dash.js repository, you will find the individual files, test code and much more, but if all you want to do is use dash.js, then the dash.all.js file is what you need.</span></span>

<span data-ttu-id="8a76f-132">若要在應用程式中新增 dash.js 播放程式，請將指令碼標記新增到 basicPlayer.html 的標頭區段：</span><span class="sxs-lookup"><span data-stu-id="8a76f-132">To add the dash.js player to your applications, add a script tag to the head section of basicPlayer.html:</span></span>

    <!-- DASH-AVC/265 reference implementation -->
    < script src="js/dash.all.js"></script>


<span data-ttu-id="8a76f-133">接下來，建立一個會在頁面載入時初始化播放程式的函式。</span><span class="sxs-lookup"><span data-stu-id="8a76f-133">Next, create a function to initialize the player when the page loads.</span></span> <span data-ttu-id="8a76f-134">在要載入 dash.all.js 的那一行之後新增下列指令碼：</span><span class="sxs-lookup"><span data-stu-id="8a76f-134">Add the following script after the line in which you load dash.all.js:</span></span>

    <script>
    // setup the video element and attach it to the Dash player
    function setupVideo() {
      var url = "http://wams.edgesuite.net/media/MPTExpressionData02/BigBuckBunny_1080p24_IYUV_2ch.ism/manifest(format=mpd-time-csf)";
      var context = new Dash.di.DashContext();
      var player = new MediaPlayer(context);
                      player.startup();
                      player.attachView(document.querySelector("#videoplayer"));
                      player.attachSource(url);
    }
    </script>

<span data-ttu-id="8a76f-135">此函式會先建立 DashContext。</span><span class="sxs-lookup"><span data-stu-id="8a76f-135">This function first creates a DashContext.</span></span> <span data-ttu-id="8a76f-136">這用來為特定的執行階段環境設定應用程式。</span><span class="sxs-lookup"><span data-stu-id="8a76f-136">This is used to configure the application for a specific runtime environment.</span></span> <span data-ttu-id="8a76f-137">從技術觀點來看，其會定義當建構應用程式時，相依性插入架構應使用的類別。</span><span class="sxs-lookup"><span data-stu-id="8a76f-137">From a technical point of view, it defines the classes that the dependency injection framework should use when constructing the application.</span></span> <span data-ttu-id="8a76f-138">在大部分情況下，您會使用 Dash.di.DashContext。</span><span class="sxs-lookup"><span data-stu-id="8a76f-138">In most cases, you will use Dash.di.DashContext.</span></span>

<span data-ttu-id="8a76f-139">接著，執行個體化 dash.js 架構的主要類別，亦即 MediaPlayer。</span><span class="sxs-lookup"><span data-stu-id="8a76f-139">Next, instantiate the primary class of the dash.js framework, MediaPlayer.</span></span> <span data-ttu-id="8a76f-140">這個類別包含所需的核心方法，例如播放和暫停，並會管理與視訊元素間的關聯性，及管理可描述待播放視訊的 Media Presentation Description (MPD) 檔案解譯。</span><span class="sxs-lookup"><span data-stu-id="8a76f-140">This class contains the core methods needed such as play and pause, manages the relationship with the video element and also manages the interpretation of the Media Presentation Description (MPD) file which describes the video to be played.</span></span>

<span data-ttu-id="8a76f-141">這會呼叫 MediaPlayer 類別的 startup () 函式，以確保播放程式準備好播放視訊。</span><span class="sxs-lookup"><span data-stu-id="8a76f-141">The startup() function of the MediaPlayer class is called to ensure that the player is ready to play video.</span></span> <span data-ttu-id="8a76f-142">此外，這個函式可確保已載入所有必要的類別 (如內容所定義)。</span><span class="sxs-lookup"><span data-stu-id="8a76f-142">Amongst other things this function ensures that all the necessary classes (as defined by the context) have been loaded.</span></span> <span data-ttu-id="8a76f-143">一旦播放程式準備就緒，您可以使用 attachview () 函式將視訊元素附加到播放程式。</span><span class="sxs-lookup"><span data-stu-id="8a76f-143">Once the player is ready, you can attach the video element to it using the attachView() function.</span></span> <span data-ttu-id="8a76f-144">這可讓 MediaPlayer 將視訊資料流插入元素中，並視需要控制播放。</span><span class="sxs-lookup"><span data-stu-id="8a76f-144">This enables the MediaPlayer to inject the video stream into the element and also control playback as necessary.</span></span>

<span data-ttu-id="8a76f-145">將 MPD 檔案的 URL 傳遞到 MediaPlayer，讓它知道預期要播放的視訊。一旦頁面整個載入後，就必須執行剛剛建立的 setupVideo() 函式。</span><span class="sxs-lookup"><span data-stu-id="8a76f-145">Pass the URL of the MPD file to the MediaPlayer so that it knows about the video it is expected to play.The setupVideo() function just created will need to be executed once the page has fully loaded.</span></span> <span data-ttu-id="8a76f-146">做法是使用內文元素的載入事件。</span><span class="sxs-lookup"><span data-stu-id="8a76f-146">Do this by using the onload event of the body element.</span></span> <span data-ttu-id="8a76f-147">將 <body> 元素變更為：</span><span class="sxs-lookup"><span data-stu-id="8a76f-147">Change your <body> element to:</span></span>

    <body onload="setupVideo()">

<span data-ttu-id="8a76f-148">最後，使用 CSS 設定視訊元素的大小。</span><span class="sxs-lookup"><span data-stu-id="8a76f-148">Finally, set the size of the video element using CSS.</span></span> <span data-ttu-id="8a76f-149">這在可調資料流環境中特別重要，因為當隨著多變的網路狀況調適播放時，正在播放的視訊大小可能會改變。</span><span class="sxs-lookup"><span data-stu-id="8a76f-149">In an adaptive streaming environment, this is especially important because the size of the video being played may change as playback adapts to changing network conditions.</span></span> <span data-ttu-id="8a76f-150">在此簡單的示範中，只會強制視訊元素變成可用瀏覽器視窗的 80%，做法是在頁面的標頭區段中新增下列 CSS：</span><span class="sxs-lookup"><span data-stu-id="8a76f-150">In this simple demo simply force the video element to be 80% of the available browser window by adding the following CSS to the head section of the page:</span></span>

    <style>
    video {
      width: 80%;
      height: 80%;
    }
    </style>

## <a name="playing-a-video"></a><span data-ttu-id="8a76f-151">播放視訊</span><span class="sxs-lookup"><span data-stu-id="8a76f-151">Playing a Video</span></span>
<span data-ttu-id="8a76f-152">若要播放視訊，請將瀏覽器指向 basicPlayback.html 檔案，然後按一下所顯示視訊播放程式上的 [播放]。</span><span class="sxs-lookup"><span data-stu-id="8a76f-152">To play a video, point your browser at the basicPlayback.html file and click play on the video player displayed.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="8a76f-153">媒體服務學習路徑</span><span class="sxs-lookup"><span data-stu-id="8a76f-153">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="8a76f-154">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="8a76f-154">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="8a76f-155">另請參閱</span><span class="sxs-lookup"><span data-stu-id="8a76f-155">See Also</span></span>
[<span data-ttu-id="8a76f-156">開發視訊播放程式應用程式</span><span class="sxs-lookup"><span data-stu-id="8a76f-156">Develop video player applications</span></span>](media-services-develop-video-players.md)

[<span data-ttu-id="8a76f-157">GitHub dash.js 存放庫</span><span class="sxs-lookup"><span data-stu-id="8a76f-157">GitHub dash.js repository</span></span>](https://github.com/Dash-Industry-Forum/dash.js) 

