---
title: "aaaSmooth Streaming 外掛程式，hello 開放來源媒體的架構。"
description: "了解如何 toouse hello Azure Media Services Smooth Streaming hello Adobe 開放的來源媒體架構的外掛程式。"
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 6068151f-b6b0-4507-9346-f03416d3d572
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/26/2016
ms.author: juliako
ms.openlocfilehash: 3cf8e4679279344cf79c3f0e5b28f63adf88179d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-microsoft-smooth-streaming-plugin-for-hello-adobe-open-source-media-framework"></a>如何 tooUse hello Microsoft Smooth Streaming 外掛程式 hello Adobe 開放的來源媒體架構
## <a name="overview"></a>概觀
hello Microsoft Smooth Streaming 外掛程式的開啟來源 Media Framework 2.0 (SS 的 OSMF) 擴充 OSMF hello 預設功能，並加入 Microsoft Smooth Streaming 內容的播放 toonew 和現有的 OSMF 播放程式。 hello 外掛程式也會將 Smooth Streaming 播放功能 tooStrobe Media Playback (SMP)。

SS for OSMF 包含兩個外掛程式版本：

* OSMF 的靜態 Smooth Streaming 外掛程式 (.swc)
* OSMF 的動態 Smooth Streaming 外掛程式 (.swf)

本文件假設 hello 讀取器具有一般的實用知識的 OSMF 和 OSMF 外掛程式。如需 OSMF 的詳細資訊，請參閱 hello 文件 hello[官方 OSMF 網站](http://osmf.org/)。

### <a name="smooth-streaming-plugin-for-osmf-20"></a>OSMF 2.0 的 Smooth Streaming 外掛程式
hello 外掛程式支援載入和點播 Smooth Streaming 內容的播放與 hello 下列功能：

* 隨選 Smooth Streaming 播放 (播放、暫停、搜尋、停止)
* 即時 Smooth Streaming 播放 (播放)
* 即時 DVR 功能 (暫停、搜尋、DVR 播放、移至即時)
* 視訊轉碼器的支援 - H.264
* 音訊轉碼器的支援 - AAC
* 透過 OSMF 內建 API 的多重音訊語言切換
* 透過 OSMF 內建 API 的最高播放品質選取
* 透過 OSMF 字幕外掛程式的 Sidecar 隱藏式輔助字幕
* Adobe&reg; Flash&reg; Player 11.4 或更高版本。
* 此版本僅支援 OSMF 2.0。

## <a name="supported-features-and-known-issues"></a>支援的功能和已知問題
如需支援的功能、 不支援的功能和已知的問題的完整清單，請參閱太[這份文件](http://download.microsoft.com/download/3/1/B/31B63D97-574E-4A8D-BF8D-170744181724/Smooth_Streaming_Plugin_for_OSMF.pdf)。

## <a name="loading-hello-plugin"></a>載入 hello 外掛程式
OSMF 外掛程式可以靜態方式 (在編譯時) 或動態方式 (在執行階段) 載入。 hello Smooth Streaming 外掛程式 OSMF 下載包含動態和靜態的版本。

* 靜態載入： tooload 靜態，靜態程式庫 (SWC) 檔是必要項。 靜態外掛程式會加入做為參考 toohello 專案和 hello 最終輸出內合併 hello 編譯時期的檔案。
* 動態載入： tooload 動態，先行編譯 (SWF) 檔是必要項。 動態外掛程式 hello 執行階段中載入，而且不包含在 hello 專案輸出。 (編譯的輸出) 動態外掛程式可使用 HTTP 和 FILE 通訊協定來載入。

如需靜態和動態載入的詳細資訊，請參閱 hello 官方[OSMF 外掛程式網頁](http://osmf.org/dev/osmf/OtherPDFs/osmf_plugin_dev_guide.pdf)。

### <a name="ss-for-osmf-static-loading"></a>SS for OSMF 靜態載入
hello 下列程式碼片段顯示如何 tooload 靜態 OSMF hello SS 外掛程式及播放使用 OSMF MediaFactory 類別的基本視訊。 前包括 hello SS OSMF 程式碼，請確定 hello 專案參考包含 hello"MSAdaptiveStreamingPlugin-v1.0.3 osmf2.0.swc 的 「 靜態外掛程式。

```
package 
{

    import com.microsoft.azure.media.AdaptiveStreamingPluginInfo;

    import flash.display.*;
    import org.osmf.media.*;
    import org.osmf.containers.MediaContainer;
    import org.osmf.events.MediaErrorEvent;
    import org.osmf.events.MediaFactoryEvent;
    import org.osmf.events.MediaPlayerStateChangeEvent;
    import org.osmf.layout.*;



    [SWF(width="1024", height="768", backgroundColor='#405050', frameRate="25")]
    public class TestPlayer extends Sprite
    {        
        public var _container:MediaContainer;
        public var _mediaFactory:DefaultMediaFactory;
        private var _mediaPlayerSprite:MediaPlayerSprite;


        public function TestPlayer( )
        {
            stage.quality = StageQuality.HIGH;

            initMediaPlayer();

        }

        private function initMediaPlayer():void
        {

            // Create hello container (sprite) for managing display and layout
            _mediaPlayerSprite = new MediaPlayerSprite();    
            _mediaPlayerSprite.addEventListener(MediaErrorEvent.MEDIA_ERROR, onPlayerFailed);
            _mediaPlayerSprite.addEventListener(MediaPlayerStateChangeEvent.MEDIA_PLAYER_STATE_CHANGE, onPlayerStateChange);
            _mediaPlayerSprite.scaleMode = ScaleMode.NONE;
            _mediaPlayerSprite.width = stage.stageWidth;
            _mediaPlayerSprite.height = stage.stageHeight;
            //Adds hello container toohello stage
            addChild(_mediaPlayerSprite);

            // Create a mediafactory instance
            _mediaFactory = new DefaultMediaFactory();

            // Add hello listeners for PLUGIN_LOADING
            _mediaFactory.addEventListener(MediaFactoryEvent.PLUGIN_LOAD,onPluginLoaded);
            _mediaFactory.addEventListener(MediaFactoryEvent.PLUGIN_LOAD_ERROR, onPluginLoadFailed );

            // Load hello plugin class 
            loadAdaptiveStreamingPlugin( );  

        }

        private function loadAdaptiveStreamingPlugin( ):void
        {
            var pluginResource:MediaResourceBase;

            pluginResource = new PluginInfoResource(new AdaptiveStreamingPluginInfo( )); 
            _mediaFactory.loadPlugin( pluginResource ); 
        }

        private function onPluginLoaded( event:MediaFactoryEvent ):void
        {
            // hello plugin is loaded successfully.
            // Your web server needs toohost a valid crossdomain.xml file tooallow plugin toodownload Smooth Streaming files.
        loadMediaSource("http://devplatem.vo.msecnd.net/Sintel/Sintel_H264.ism/manifest")

        }

        private function onPluginLoadFailed( event:MediaFactoryEvent ):void
        {
            // hello plugin is failed tooload ...
        }


        private function onPlayerStateChange(event:MediaPlayerStateChangeEvent) : void
        {
            var state:String;

            state =  event.state;

            switch (state)
            {
                case MediaPlayerState.LOADING: 

                    // A new source is started tooload.

                    break;

                case  MediaPlayerState.READY :   
                    // Add code toodeal with Player Ready when it is hit hello first load after a source is loaded. 

                    break;

                case MediaPlayerState.BUFFERING :

                    break;

                case  MediaPlayerState.PAUSED :
                    break;      
                // other states ...          
            }
        }

        private function onPlayerFailed(event:MediaErrorEvent) : void
        {
            // Media Player is failed .           
        }

        private function loadMediaSource(sourceURL : String):void 
        {
            // Take an URL of SmoothStreamingSource's manifest and add it toohello page.

            var resource:URLResource= new URLResource( sourceURL );

            var element:MediaElement = _mediaFactory.createMediaElement( resource );
            _mediaPlayerSprite.scaleMode = ScaleMode.LETTERBOX;
            _mediaPlayerSprite.width = stage.stageWidth;
            _mediaPlayerSprite.height = stage.stageHeight;

            // Add hello media element
            _mediaPlayerSprite.media = element;
        }     

    }
}
```


### <a name="ss-for-osmf-dynamic-loading"></a>SS for OSMF 動態載入
hello 下列程式碼片段顯示如何 tooload 動態 OSMF hello SS 外掛程式及播放使用 hello OSMF MediaFactory 類別的基本視訊。 前先包含 hello SS OSMF 程式碼，複製 hello"MSAdaptiveStreamingPlugin-v1.0.3 osmf2.0.swf 的 「 動態外掛程式 toohello 專案資料夾，如果您想要使用檔案的通訊協定，tooload 或複製 web 伺服器的 HTTP 負載底下。 沒有任何需要 tooinclude"MSAdaptiveStreamingPlugin-v1.0.3 osmf2.0.swc 的"hello 專案參考中。

package {

    import flash.display.*;
    import org.osmf.media.*;
    import org.osmf.containers.MediaContainer;
    import org.osmf.events.MediaErrorEvent;
    import org.osmf.events.MediaFactoryEvent;
    import org.osmf.events.MediaPlayerStateChangeEvent;
    import org.osmf.layout.*;
    import flash.events.Event;
    import flash.system.Capabilities;


    //Sets hello size of hello SWF

    [SWF(width="1024", height="768", backgroundColor='#405050', frameRate="25")]
    public class TestPlayer extends Sprite
    {        
        public var _container:MediaContainer;
        public var _mediaFactory:DefaultMediaFactory;
        private var _mediaPlayerSprite:MediaPlayerSprite;


        public function TestPlayer( )
        {
            stage.quality = StageQuality.HIGH;
            initMediaPlayer();
        }

        private function initMediaPlayer():void
        {

            // Create hello container (sprite) for managing display and layout
            _mediaPlayerSprite = new MediaPlayerSprite();    
            _mediaPlayerSprite.addEventListener(MediaErrorEvent.MEDIA_ERROR, onPlayerFailed);
            _mediaPlayerSprite.addEventListener(MediaPlayerStateChangeEvent.MEDIA_PLAYER_STATE_CHANGE, onPlayerStateChange);

            //Adds hello container toohello stage
            addChild(_mediaPlayerSprite);

            // Create a mediafactory instance
            _mediaFactory = new DefaultMediaFactory();

            // Add hello listeners for PLUGIN_LOADING
            _mediaFactory.addEventListener(MediaFactoryEvent.PLUGIN_LOAD,onPluginLoaded);
            _mediaFactory.addEventListener(MediaFactoryEvent.PLUGIN_LOAD_ERROR, onPluginLoadFailed );

            // Load hello plugin class 
            loadAdaptiveStreamingPlugin( );  

        }

        private function loadAdaptiveStreamingPlugin( ):void
        {
            var pluginResource:MediaResourceBase;
            var adaptiveStreamingPluginUrl:String;

            // Your dynamic plugin web server needs toohost a valid crossdomain.xml file tooallow loading plugins.

            adaptiveStreamingPluginUrl = "http://yourdomain/MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swf";
            pluginResource = new URLResource(adaptiveStreamingPluginUrl);
            _mediaFactory.loadPlugin( pluginResource ); 

        }

        private function onPluginLoaded( event:MediaFactoryEvent ):void
        {
            // hello plugin is loaded successfully.

            // Your web server needs toohost a valid crossdomain.xml file tooallow plugin toodownload Smooth Streaming files.

    loadMediaSource("http://devplatem.vo.msecnd.net/Sintel/Sintel_H264.ism/manifest")
        }

        private function onPluginLoadFailed( event:MediaFactoryEvent ):void
        {
            // hello plugin is failed tooload ...
        }


        private function onPlayerStateChange(event:MediaPlayerStateChangeEvent) : void
        {
            var state:String;

            state =  event.state;

            switch (state)
            {
                case MediaPlayerState.LOADING: 

                    // A new source is started tooload.

                    break;

                case  MediaPlayerState.READY :   
                    // Add code toodeal with Player Ready when it is hit hello first load after a source is loaded. 

                    break;

                case MediaPlayerState.BUFFERING :

                    break;

                case  MediaPlayerState.PAUSED :
                    break;      
                // other states ...          
            }
        }

        private function onPlayerFailed(event:MediaErrorEvent) : void
        {
            // Media Player is failed .           
        }

        private function loadMediaSource(sourceURL : String):void 
        {
            // Take an URL of SmoothStreamingSource's manifest and add it toohello page.

            var resource:URLResource= new URLResource( sourceURL );

            var element:MediaElement = _mediaFactory.createMediaElement( resource );
            _mediaPlayerSprite.scaleMode = ScaleMode.LETTERBOX;
            _mediaPlayerSprite.width = stage.stageWidth;
            _mediaPlayerSprite.height = stage.stageHeight;
            // Add hello media element
            _mediaPlayerSprite.media = element;
        }     

    }
}

## <a name="strobe-media--playback-with-hello-ss-odmf-dynamic-plugin"></a>Strobe Media Playback 以 hello SS ODMF 動態外掛程式
hello Smooth Streaming OSMF 動態外掛程式會與相容[Strobe Media Playback (SMP)](http://osmf.org/strobe_mediaplayback.html)。 您可以用於 OSMF 外掛程式 tooadd Smooth Streaming 內容的播放 tooSMP hello SS。 toodo，本版"MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swf 」 在 web 伺服器 HTTP 負載使用 hello 下列步驟：

1. 瀏覽 hello [Strobe Media Playback [安裝] 頁面](http://osmf.org/dev/2.0gm/setup.html)。 
2. 設定 hello src tooa Smooth Streaming 來源 (例如 http://devplatem.vo.msecnd.net/Sintel/Sintel_H264.ism/manifest) 
3. 進行所需的 hello 組態變更，然後按一下 [預覽和更新。
   
   **注意** 您的內容 Web 伺服器需要有效的 crossdomain.xml。 
4. 複製並貼入 hello 程式碼 tooa 簡單的 HTML 網頁 hello 下列範例中，使用慣用的文字編輯器，例如：

        <html>
        <body>
        <object width="920" height="640"> 
        <param name="movie" value="http://osmf.org/dev/2.0gm/StrobeMediaPlayback.swf"></param>
        <param name="flashvars" value="src=http://devplatem.vo.msecnd.net/Sintel/Sintel_H264.ism/manifest &autoPlay=true"></param>
        <param name="allowFullScreen" value="true"></param>
        <param name="allowscriptaccess" value="always"></param>
        <param name="wmode" value="direct"></param>
        <embed src="http://osmf.org/dev/2.0gm/StrobeMediaPlayback.swf" 
            type="application/x-shockwave-flash" 
            allowscriptaccess="always" 
            allowfullscreen="true" 
            wmode="direct" 
            width="920" 
            height="640" 
            flashvars=" src=http://devplatem.vo.msecnd.net/Sintel/Sintel_H264.ism/manifest&autoPlay=true">
        </embed>
        </object>
        </body>
        </html>



1. 將 Smooth Streaming OSMF 外掛程式 toohello 內嵌程式碼並儲存。
   
        <html>
        <object width="920" height="640"> 
        <param name="movie" value="http://osmf.org/dev/2.0gm/StrobeMediaPlayback.swf"></param>
        <param name="flashvars" value="src=http://devplatem.vo.msecnd.net/Sintel/Sintel_H264.ism/manifest&autoPlay=true&plugin_AdaptiveStreamingPlugin=http://yourdomain/MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swf&AdaptiveStreamingPlugin_retryLive=true&AdaptiveStreamingPlugin_retryInterval=10"></param>
        <param name="allowFullScreen" value="true"></param>
        <param name="allowscriptaccess" value="always"></param>
        <param name="wmode" value="direct"></param>
        <embed src="http://osmf.org/dev/2.0gm/StrobeMediaPlayback.swf" 
            type="application/x-shockwave-flash" 
            allowscriptaccess="always" 
            allowfullscreen="true" 
            wmode="direct" 
            width="920" 
            height="640" 
            flashvars="src=http://devplatem.vo.msecnd.net/Sintel/Sintel_H264.ism/manifest&autoPlay=true&plugin_AdaptiveStreamingPlugin=http://yourdomain/MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swf&AdaptiveStreamingPlugin_retryLive=true&AdaptiveStreamingPlugin_retryInterval=10">
        </embed>
        </object>
        </html>
2. 儲存您的 HTML 頁面，並發行 tooa 網頁伺服器。 瀏覽 toohello 發行網頁使用您最愛閃爍&reg;Player 啟用網際網路瀏覽器 (Internet Explorer、 Chrome、 Firefox，等等)。
3. 在 Adobe&reg; Flash&reg; Player 內欣賞 Smooth Streaming 內容。

如需有關一般 OSMF 開發的詳細資訊，請參閱 hello 官方[OSMF 開發頁面](http://osmf.org/resources.html)。

## <a name="media-services-learning-paths"></a>媒體服務學習路徑
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>提供意見反應
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a>另請參閱
[OSMF 的 Microsoft 彈性資料流外掛程式更新 (英文)](https://azure.microsoft.com/blog/2014/10/27/microsoft-adaptive-streaming-plugin-for-osmf-update/) 

