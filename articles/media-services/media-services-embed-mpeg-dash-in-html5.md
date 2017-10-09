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
# <a name="embedding-a-mpeg-dash-adaptive-streaming-video-in-an-html5-application-with-dashjs"></a>透過 DASH.js 將 MPEG-DASH 彈性資料流視訊嵌入到 HTML5 應用程式
## <a name="overview"></a>概觀
MPEG DASH 是 ISO 標準 hello 彈性的視訊內容，提供重要的優點的人員想 toodeliver 高品質且可調整視訊串流處理輸出資料流。 MPEG DASH，與 hello 視訊資料流將會自動卸除 tooa 低定義 hello 網路變得壅塞時。 這會減少 hello hello 播放程式會下載 hello 接下來幾秒 tooplay （也稱為緩衝處理） 時看到 「 暫停 」 的視訊 hello 檢視器的可能性。 當網路壅塞會降低，hello 影片播放器接著會傳回 tooa 高品質資料流。 需要此功能 tooadapt hello 頻寬也會導致更快速的開始時間讓視訊。 表示 hello 幾秒可以播放 fast-下載較低品質區段中，一旦已緩衝處理足夠的內容，然後逐步 tooa 愈高，品質設定。

Dash.js 是以 JavaScript 撰寫的開放原始碼 MPEG-DASH 視訊播放程式。 其目的是 tooprovide 強固且能跨平台的播放程式可以在需要視訊播放的應用程式中自由地重複使用。 它提供 MPEG-DASH 播放支援 hello W3C 媒體來源延伸模組 (MSE)，現今也就是 Chrome、 Microsoft Edge 和 IE11 （其他瀏覽器已指出其意圖 toosupport MSE） 的任何瀏覽器中。 Js DASH.js 的詳細資訊，請參閱 hello GitHub dash.js 儲存機制。

## <a name="creating-a-browser-based-streaming-video-player"></a>建立以瀏覽器為基礎的資料流視訊播放程式
toocreate 簡單的 web 網頁會顯示以 hello 預期影片播放器控制這類播放、 暫停、 倒帶等，您將需要：

1. 建立 HTML 網頁
2. 新增 hello 視訊標記
3. 新增 hello dash.js 播放程式
4. 初始化 hello 播放程式
5. 新增部分 CSS 樣式
6. 實作 MSE 的瀏覽器中檢視 hello 結果

正在初始化 hello 播放程式可以完成在只要少數的 JavaScript 程式碼行。 它使用 dash.js，確實是在瀏覽器型應用程式中的簡單 tooembed MPEG-DASH 視訊。

## <a name="creating-hello-html-page"></a>建立 hello HTML 網頁
hello 第一個步驟是包含 hello toocreate 標準 HTML 頁面**視訊**項目，這個檔案儲存為 basicPlayer.html，為 hello 下列範例將說明：

    <!DOCTYPE html>
    <html>
      <head><title>Adaptive Streaming in HTML5</title></head>
      <body>
        <h1>Adaptive Streaming with HTML5</h1>
        <video id="videoplayer" controls></video>
      </body>
    </html>

## <a name="adding-hello-dashjs-player"></a>新增 hello DASH.js 播放程式
tooadd hello dash.js 參考實作 toohello 應用程式，您將需要從 dash.js 專案 hello 1.0 版本 toograb hello dash.all.js 檔案。 這應該會儲存在您的應用程式的 hello JavaScript 資料夾。 這個檔案是必須綜覽所有 hello 必要 dash.js 程式碼到單一檔案的便利性檔案。 如果您有一起來看看周圍 hello dash.js 儲存機制時，會尋找 hello 個別檔案，請測試程式碼和更多，但是，如果您想 toodo 使用 dash.js 則 hello dash.all.js 檔案就是您的需要。

tooadd hello dash.js player tooyour 應用程式，新增 basicPlayer.html 指令碼標記 toohello 標頭區段：

    <!-- DASH-AVC/265 reference implementation -->
    < script src="js/dash.all.js"></script>


Hello 網頁載入時，接下來，建立函式 tooinitialize hello 播放程式。 加入下列指令碼之後您可以在其中載入 dash.all.js hello 列, hello:

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

此函式會先建立 DashContext。 這是針對特定執行階段環境使用的 tooconfigure hello 應用程式。 從技術觀點來看，它會定義的 hello 建構 hello 應用程式時，應該使用 hello 相依性插入架構的類別。 在大部分情況下，您會使用 Dash.di.DashContext。

接下來，具現化 hello dash.js framework MediaPlayer hello 主要的類別。 這個類別包含 hello 核心方法需要這類播放和暫停、 管理 hello hello video 項目關聯性，並也會管理 hello 媒體呈現描述 (MPD) 檔描述 hello 播放的視訊 toobe hello 解譯。

hello startup （） 函式的 hello MediaPlayer 類別稱為 tooensure 這 hello 位玩家已準備好 tooplay 視訊。 其他項目在這個函式可確保，所有的 hello 必要的類別 （如 hello 內容所定義） 已載入。 Hello 播放程式準備就緒之後，您可以附加 hello video 項目 tooit 使用 hello attachView() 函式。 如此會啟用 hello MediaPlayer tooinject hello 視訊串流至 hello 項目，並也控制在必要時播放。

傳遞的 hello MPD 檔案 toohello MediaPlayer hello URL，以便它所知道 hello 影片 end_time< 剛才建立的 tooplay.hello setupVideo() 函式需要 toobe hello 頁面完全載入後執行。 藉由使用 hello body 元素的 hello onload 事件執行這項操作。 將 <body> 元素變更為：

    <body onload="setupVideo()">

最後，設定 hello 視訊元素的 CSS hello 大小。 在自動調整串流處理環境中，這是特別重要因為 hello 大小 hello 視訊播放播放會調整 toochanging 網路狀況可能會變更。 在這個簡單的示範只強制 hello video 項目 toobe hello 可用的瀏覽器視窗的 80%藉由新增下列 CSS toohello 前端 hello 頁面區段的 hello:

    <style>
    video {
      width: 80%;
      height: 80%;
    }
    </style>

## <a name="playing-a-video"></a>播放視訊
tooplay 視訊，指向您的瀏覽器在 hello basicPlayback.html 檔案，然後按一下 顯示 hello 影片播放器上的播放。

## <a name="media-services-learning-paths"></a>媒體服務學習路徑
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>提供意見反應
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a>另請參閱
[開發視訊播放程式應用程式](media-services-develop-video-players.md)

[GitHub dash.js 存放庫](https://github.com/Dash-Industry-Forum/dash.js) 

