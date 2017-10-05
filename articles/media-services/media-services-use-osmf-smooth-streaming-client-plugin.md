---
title: "Open Source Media Framework 的 Smooth Streaming 外掛程式"
description: "了解如何使用 Adobe Open Source Media Framework 的 Azure 媒體服務 Smooth Streaming 外掛程式。"
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
ms.openlocfilehash: 9c764f176ae75085320882de3fb26d8e7d52daaf
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-the-microsoft-smooth-streaming-plugin-for-the-adobe-open-source-media-framework"></a><span data-ttu-id="d3258-103">如何使用 Adobe Open Source Media Framework 的 Microsoft Smooth Streaming 外掛程式</span><span class="sxs-lookup"><span data-stu-id="d3258-103">How to Use the Microsoft Smooth Streaming Plugin for the Adobe Open Source Media Framework</span></span>
## <a name="overview"></a><span data-ttu-id="d3258-104">Overview</span><span class="sxs-lookup"><span data-stu-id="d3258-104">Overview</span></span>
<span data-ttu-id="d3258-105">Open Source Media Framework 2.0 的 Microsoft Smooth Streaming 外掛程式 (SS for OSMF) 可擴充 OSMF 的預設功能，並可為新的和現有的 OSMF 播放程式新增 Microsoft Smooth Streaming 內容播放功能。</span><span class="sxs-lookup"><span data-stu-id="d3258-105">The Microsoft Smooth Streaming plugin for Open Source Media Framework 2.0 (SS for OSMF) extends the default capabilities of OSMF and adds Microsoft Smooth Streaming content playback to new and existing OSMF players.</span></span> <span data-ttu-id="d3258-106">此外掛程式也可為 Strobe Media Playback (SMP) 新增 Smooth Streaming 播放功能。</span><span class="sxs-lookup"><span data-stu-id="d3258-106">The plugin also adds Smooth Streaming playback capabilities to Strobe Media Playback (SMP).</span></span>

<span data-ttu-id="d3258-107">SS for OSMF 包含兩個外掛程式版本：</span><span class="sxs-lookup"><span data-stu-id="d3258-107">SS for OSMF includes two versions of plugin:</span></span>

* <span data-ttu-id="d3258-108">OSMF 的靜態 Smooth Streaming 外掛程式 (.swc)</span><span class="sxs-lookup"><span data-stu-id="d3258-108">Static Smooth Streaming plugin for OSMF (.swc)</span></span>
* <span data-ttu-id="d3258-109">OSMF 的動態 Smooth Streaming 外掛程式 (.swf)</span><span class="sxs-lookup"><span data-stu-id="d3258-109">Dynamic Smooth Streaming plugin for OSMF (.swf)</span></span>

<span data-ttu-id="d3258-110">本文假設讀者具備使用 OSMF 和 OSMF 外掛程式的一般知識。如需 OSMF 的詳細資訊，請參閱 [OSMF 官方網站](http://osmf.org/)上的文件。</span><span class="sxs-lookup"><span data-stu-id="d3258-110">This document assumes that the reader has a general working knowledge of OSMF and OSMF plug-ins. For more information about OSMF, please see the documentation on the [official OSMF site](http://osmf.org/).</span></span>

### <a name="smooth-streaming-plugin-for-osmf-20"></a><span data-ttu-id="d3258-111">OSMF 2.0 的 Smooth Streaming 外掛程式</span><span class="sxs-lookup"><span data-stu-id="d3258-111">Smooth Streaming plugin for OSMF 2.0</span></span>
<span data-ttu-id="d3258-112">此外掛程式支援以下列功能載入及播放隨選的 Smooth Streaming 內容：</span><span class="sxs-lookup"><span data-stu-id="d3258-112">The plugin supports loading and playback of on-demand Smooth Streaming content with the following features:</span></span>

* <span data-ttu-id="d3258-113">隨選 Smooth Streaming 播放 (播放、暫停、搜尋、停止)</span><span class="sxs-lookup"><span data-stu-id="d3258-113">On-demand Smooth Streaming playback (Play, Pause, Seek, Stop)</span></span>
* <span data-ttu-id="d3258-114">即時 Smooth Streaming 播放 (播放)</span><span class="sxs-lookup"><span data-stu-id="d3258-114">Live Smooth Streaming playback (Play)</span></span>
* <span data-ttu-id="d3258-115">即時 DVR 功能 (暫停、搜尋、DVR 播放、移至即時)</span><span class="sxs-lookup"><span data-stu-id="d3258-115">Live DVR functions (Pause, Seek, DVR Playback, Go-to-Live)</span></span>
* <span data-ttu-id="d3258-116">視訊轉碼器的支援 - H.264</span><span class="sxs-lookup"><span data-stu-id="d3258-116">Support for video codecs - H.264</span></span>
* <span data-ttu-id="d3258-117">音訊轉碼器的支援 - AAC</span><span class="sxs-lookup"><span data-stu-id="d3258-117">Support for Audio codecs - AAC</span></span>
* <span data-ttu-id="d3258-118">透過 OSMF 內建 API 的多重音訊語言切換</span><span class="sxs-lookup"><span data-stu-id="d3258-118">Multiple audio language switching with OSMF built-in APIs</span></span>
* <span data-ttu-id="d3258-119">透過 OSMF 內建 API 的最高播放品質選取</span><span class="sxs-lookup"><span data-stu-id="d3258-119">Max playback quality selection with OSMF built-in APIs</span></span>
* <span data-ttu-id="d3258-120">透過 OSMF 字幕外掛程式的 Sidecar 隱藏式輔助字幕</span><span class="sxs-lookup"><span data-stu-id="d3258-120">Sidecar closed captions with OSMF captions plugin</span></span>
* <span data-ttu-id="d3258-121">Adobe&reg; Flash&reg; Player 11.4 或更高版本。</span><span class="sxs-lookup"><span data-stu-id="d3258-121">Adobe&reg; Flash&reg; Player 11.4 or higher.</span></span>
* <span data-ttu-id="d3258-122">此版本僅支援 OSMF 2.0。</span><span class="sxs-lookup"><span data-stu-id="d3258-122">This version only supports OSMF 2.0.</span></span>

## <a name="supported-features-and-known-issues"></a><span data-ttu-id="d3258-123">支援的功能和已知問題</span><span class="sxs-lookup"><span data-stu-id="d3258-123">Supported features and known issues</span></span>
<span data-ttu-id="d3258-124">如需支援功能、不支援功能和已知問題的完整清單，請參閱 [這份文件](http://download.microsoft.com/download/3/1/B/31B63D97-574E-4A8D-BF8D-170744181724/Smooth_Streaming_Plugin_for_OSMF.pdf)。</span><span class="sxs-lookup"><span data-stu-id="d3258-124">For a full list of supported features, unsupported features and known issues, refer to [this document](http://download.microsoft.com/download/3/1/B/31B63D97-574E-4A8D-BF8D-170744181724/Smooth_Streaming_Plugin_for_OSMF.pdf).</span></span>

## <a name="loading-the-plugin"></a><span data-ttu-id="d3258-125">載入外掛程式</span><span class="sxs-lookup"><span data-stu-id="d3258-125">Loading the Plugin</span></span>
<span data-ttu-id="d3258-126">OSMF 外掛程式可以靜態方式 (在編譯時) 或動態方式 (在執行階段) 載入。</span><span class="sxs-lookup"><span data-stu-id="d3258-126">OSMF plugins can be loaded statically (at compile time) or dynamically (at run-time).</span></span> <span data-ttu-id="d3258-127">OSMF 的 Smooth Streaming 外掛程式下載，會同時包含動態和靜態版本。</span><span class="sxs-lookup"><span data-stu-id="d3258-127">The Smooth Streaming plugin for OSMF download includes both dynamic and static versions.</span></span>

* <span data-ttu-id="d3258-128">靜態載入：若要以靜態方式載入，必須要有靜態程式庫 (SWC) 檔案。</span><span class="sxs-lookup"><span data-stu-id="d3258-128">Static loading: To load statically, a static library (SWC) file is required.</span></span> <span data-ttu-id="d3258-129">靜態外掛程式會在編譯時新增為專案的參考，並合併到最終的輸出檔內。</span><span class="sxs-lookup"><span data-stu-id="d3258-129">Static plugins are added as a reference to the projects and merge inside the final output file at the compile time.</span></span>
* <span data-ttu-id="d3258-130">動態載入：若要以動態方式載入，必須要有預先編譯的 (SWF) 檔案。</span><span class="sxs-lookup"><span data-stu-id="d3258-130">Dynamic loading: To load dynamically, a precompiled (SWF) file is required.</span></span> <span data-ttu-id="d3258-131">動態外掛程式會在執行階段載入，而不會包含在專案輸出中。</span><span class="sxs-lookup"><span data-stu-id="d3258-131">Dynamic plugins are loaded in the runtime and not included in the project output.</span></span> <span data-ttu-id="d3258-132">(編譯的輸出) 動態外掛程式可使用 HTTP 和 FILE 通訊協定來載入。</span><span class="sxs-lookup"><span data-stu-id="d3258-132">(Compiled output) Dynamic plugins can be loaded using HTTP and FILE protocols.</span></span>

<span data-ttu-id="d3258-133">如需靜態和動態載入的詳細資訊，請參閱官方 [OSMF 外掛程式頁面](http://osmf.org/dev/osmf/OtherPDFs/osmf_plugin_dev_guide.pdf)。</span><span class="sxs-lookup"><span data-stu-id="d3258-133">For more information on static and dynamic loading, see the official [OSMF plugin page](http://osmf.org/dev/osmf/OtherPDFs/osmf_plugin_dev_guide.pdf).</span></span>

### <a name="ss-for-osmf-static-loading"></a><span data-ttu-id="d3258-134">SS for OSMF 靜態載入</span><span class="sxs-lookup"><span data-stu-id="d3258-134">SS for OSMF Static Loading</span></span>
<span data-ttu-id="d3258-135">下方的程式碼片段將說明如何以靜態方式載入 OSMF 的 SS 外掛程式，並使用 OSMF MediaFactory 類別播放基本視訊。</span><span class="sxs-lookup"><span data-stu-id="d3258-135">The code snippet below shows how to load the SS plugin for OSMF statically and play a basic video using OSMF MediaFactory class.</span></span> <span data-ttu-id="d3258-136">在加入 SS for OSMF 程式碼之前，請確定專案參考包含 "MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swc" 靜態外掛程式。</span><span class="sxs-lookup"><span data-stu-id="d3258-136">Before including the SS for OSMF code, please ensure that the project reference includes the "MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swc" static plugin.</span></span>

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

            // Create the container (sprite) for managing display and layout
            _mediaPlayerSprite = new MediaPlayerSprite();    
            _mediaPlayerSprite.addEventListener(MediaErrorEvent.MEDIA_ERROR, onPlayerFailed);
            _mediaPlayerSprite.addEventListener(MediaPlayerStateChangeEvent.MEDIA_PLAYER_STATE_CHANGE, onPlayerStateChange);
            _mediaPlayerSprite.scaleMode = ScaleMode.NONE;
            _mediaPlayerSprite.width = stage.stageWidth;
            _mediaPlayerSprite.height = stage.stageHeight;
            //Adds the container to the stage
            addChild(_mediaPlayerSprite);

            // Create a mediafactory instance
            _mediaFactory = new DefaultMediaFactory();

            // Add the listeners for PLUGIN_LOADING
            _mediaFactory.addEventListener(MediaFactoryEvent.PLUGIN_LOAD,onPluginLoaded);
            _mediaFactory.addEventListener(MediaFactoryEvent.PLUGIN_LOAD_ERROR, onPluginLoadFailed );

            // Load the plugin class 
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
            // The plugin is loaded successfully.
            // Your web server needs to host a valid crossdomain.xml file to allow plugin to download Smooth Streaming files.
        loadMediaSource("http://devplatem.vo.msecnd.net/Sintel/Sintel_H264.ism/manifest")

        }

        private function onPluginLoadFailed( event:MediaFactoryEvent ):void
        {
            // The plugin is failed to load ...
        }


        private function onPlayerStateChange(event:MediaPlayerStateChangeEvent) : void
        {
            var state:String;

            state =  event.state;

            switch (state)
            {
                case MediaPlayerState.LOADING: 

                    // A new source is started to load.

                    break;

                case  MediaPlayerState.READY :   
                    // Add code to deal with Player Ready when it is hit the first load after a source is loaded. 

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
            // Take an URL of SmoothStreamingSource's manifest and add it to the page.

            var resource:URLResource= new URLResource( sourceURL );

            var element:MediaElement = _mediaFactory.createMediaElement( resource );
            _mediaPlayerSprite.scaleMode = ScaleMode.LETTERBOX;
            _mediaPlayerSprite.width = stage.stageWidth;
            _mediaPlayerSprite.height = stage.stageHeight;

            // Add the media element
            _mediaPlayerSprite.media = element;
        }     

    }
}
```


### <a name="ss-for-osmf-dynamic-loading"></a><span data-ttu-id="d3258-137">SS for OSMF 動態載入</span><span class="sxs-lookup"><span data-stu-id="d3258-137">SS for OSMF Dynamic Loading</span></span>
<span data-ttu-id="d3258-138">下方的程式碼片段將說明如何以動態方式載入 OSMF 的 SS 外掛程式，並使用 OSMF MediaFactory 類別播放基本視訊。</span><span class="sxs-lookup"><span data-stu-id="d3258-138">The code snippet below shows how to load the SS plugin for OSMF dynamically and play a basic video using the OSMF MediaFactory class.</span></span> <span data-ttu-id="d3258-139">在加入 SS for OSMF 程式碼之前，請將 "MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swf" 動態外掛程式複製到專案資料夾 (如果您要使用 FILE 通訊協定進行載入)，或是在 Web 伺服器下複製 (以進行 HTTP 載入)。</span><span class="sxs-lookup"><span data-stu-id="d3258-139">Before including the SS for OSMF code, copy the "MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swf" dynamic plugin to the project folder if you want to load using FILE protocol, or copy under a web server for HTTP load.</span></span> <span data-ttu-id="d3258-140">您不需要在專案參考中加入 "MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swc"。</span><span class="sxs-lookup"><span data-stu-id="d3258-140">There is no need to include "MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swc" in the project references.</span></span>

<span data-ttu-id="d3258-141">package {</span><span class="sxs-lookup"><span data-stu-id="d3258-141">package {</span></span>

    import flash.display.*;
    import org.osmf.media.*;
    import org.osmf.containers.MediaContainer;
    import org.osmf.events.MediaErrorEvent;
    import org.osmf.events.MediaFactoryEvent;
    import org.osmf.events.MediaPlayerStateChangeEvent;
    import org.osmf.layout.*;
    import flash.events.Event;
    import flash.system.Capabilities;


    //Sets the size of the SWF

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

            // Create the container (sprite) for managing display and layout
            _mediaPlayerSprite = new MediaPlayerSprite();    
            _mediaPlayerSprite.addEventListener(MediaErrorEvent.MEDIA_ERROR, onPlayerFailed);
            _mediaPlayerSprite.addEventListener(MediaPlayerStateChangeEvent.MEDIA_PLAYER_STATE_CHANGE, onPlayerStateChange);

            //Adds the container to the stage
            addChild(_mediaPlayerSprite);

            // Create a mediafactory instance
            _mediaFactory = new DefaultMediaFactory();

            // Add the listeners for PLUGIN_LOADING
            _mediaFactory.addEventListener(MediaFactoryEvent.PLUGIN_LOAD,onPluginLoaded);
            _mediaFactory.addEventListener(MediaFactoryEvent.PLUGIN_LOAD_ERROR, onPluginLoadFailed );

            // Load the plugin class 
            loadAdaptiveStreamingPlugin( );  

        }

        private function loadAdaptiveStreamingPlugin( ):void
        {
            var pluginResource:MediaResourceBase;
            var adaptiveStreamingPluginUrl:String;

            // Your dynamic plugin web server needs to host a valid crossdomain.xml file to allow loading plugins.

            adaptiveStreamingPluginUrl = "http://yourdomain/MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swf";
            pluginResource = new URLResource(adaptiveStreamingPluginUrl);
            _mediaFactory.loadPlugin( pluginResource ); 

        }

        private function onPluginLoaded( event:MediaFactoryEvent ):void
        {
            // The plugin is loaded successfully.

            // Your web server needs to host a valid crossdomain.xml file to allow plugin to download Smooth Streaming files.

    loadMediaSource("http://devplatem.vo.msecnd.net/Sintel/Sintel_H264.ism/manifest")
        }

        private function onPluginLoadFailed( event:MediaFactoryEvent ):void
        {
            // The plugin is failed to load ...
        }


        private function onPlayerStateChange(event:MediaPlayerStateChangeEvent) : void
        {
            var state:String;

            state =  event.state;

            switch (state)
            {
                case MediaPlayerState.LOADING: 

                    // A new source is started to load.

                    break;

                case  MediaPlayerState.READY :   
                    // Add code to deal with Player Ready when it is hit the first load after a source is loaded. 

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
            // Take an URL of SmoothStreamingSource's manifest and add it to the page.

            var resource:URLResource= new URLResource( sourceURL );

            var element:MediaElement = _mediaFactory.createMediaElement( resource );
            _mediaPlayerSprite.scaleMode = ScaleMode.LETTERBOX;
            _mediaPlayerSprite.width = stage.stageWidth;
            _mediaPlayerSprite.height = stage.stageHeight;
            // Add the media element
            _mediaPlayerSprite.media = element;
        }     

    }
<span data-ttu-id="d3258-142">}</span><span class="sxs-lookup"><span data-stu-id="d3258-142">}</span></span>

## <a name="strobe-media--playback-with-the-ss-odmf-dynamic-plugin"></a><span data-ttu-id="d3258-143">Strobe Media Playback 與 SS ODMF 動態外掛程式</span><span class="sxs-lookup"><span data-stu-id="d3258-143">Strobe Media  Playback with the SS ODMF Dynamic Plugin</span></span>
<span data-ttu-id="d3258-144">Smooth Streaming for OSMF 動態外掛程式與 [Strobe Media Playback (SMP)](http://osmf.org/strobe_mediaplayback.html)是相容的。</span><span class="sxs-lookup"><span data-stu-id="d3258-144">The Smooth Streaming for OSMF dynamic plugin is compatible with [Strobe Media Playback (SMP)](http://osmf.org/strobe_mediaplayback.html).</span></span> <span data-ttu-id="d3258-145">您可以使用 SS for OSMF 外掛程式，將 Smooth Streaming 內容播放新增至 SMP。</span><span class="sxs-lookup"><span data-stu-id="d3258-145">You can use the SS for OSMF plugin to add Smooth Streaming content playback to SMP.</span></span> <span data-ttu-id="d3258-146">若要這麼做，請使用下列步驟，在 Web 伺服器下複製 "MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swf"，以進行 HTTP 載入：</span><span class="sxs-lookup"><span data-stu-id="d3258-146">To do this, copy "MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swf" under a web server for HTTP load using the following steps:</span></span>

1. <span data-ttu-id="d3258-147">瀏覽 [Strobe Media Playback 設定頁面](http://osmf.org/dev/2.0gm/setup.html)。</span><span class="sxs-lookup"><span data-stu-id="d3258-147">Browse the [Strobe Media Playback setup page](http://osmf.org/dev/2.0gm/setup.html).</span></span> 
2. <span data-ttu-id="d3258-148">將 src 設為 Smooth Streaming 來源 (例如 http://devplatem.vo.msecnd.net/Sintel/Sintel_H264.ism/manifest)</span><span class="sxs-lookup"><span data-stu-id="d3258-148">Set the src to a Smooth Streaming source, (e.g. http://devplatem.vo.msecnd.net/Sintel/Sintel_H264.ism/manifest)</span></span> 
3. <span data-ttu-id="d3258-149">進行所需的組態變更，然後按一下 [Preview and Update]。</span><span class="sxs-lookup"><span data-stu-id="d3258-149">Make the desired configuration changes and click Preview and Update.</span></span>
   
   <span data-ttu-id="d3258-150">**注意** 您的內容 Web 伺服器需要有效的 crossdomain.xml。</span><span class="sxs-lookup"><span data-stu-id="d3258-150">**Note** Your content web server needs a valid crossdomain.xml.</span></span> 
4. <span data-ttu-id="d3258-151">使用您慣用的文字編輯器，將程式碼複製並貼至簡單的 HTML 頁面，如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="d3258-151">Copy and paste the code to a simple HTML page using your favorite text editor, such as in the following example:</span></span>

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



1. <span data-ttu-id="d3258-152">將 Smooth Streaming OSMF 外掛程式新增至內嵌程式碼，並加以儲存。</span><span class="sxs-lookup"><span data-stu-id="d3258-152">Add Smooth Streaming OSMF plugin to the embed code and save.</span></span>
   
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
2. <span data-ttu-id="d3258-153">儲存您的 HTML 頁面，並發佈至 Web 伺服器。</span><span class="sxs-lookup"><span data-stu-id="d3258-153">Save your HTML page and publish to a web server.</span></span> <span data-ttu-id="d3258-154">使用您慣用且具有 Flash&reg; Player 功能的網際網路瀏覽器 (Internet Explorer、Chrome、Firefox 等)，瀏覽至已發佈的網頁。</span><span class="sxs-lookup"><span data-stu-id="d3258-154">Browse to the published web page using your favorite Flash&reg; Player enabled Internet browser (Internet Explorer, Chrome, Firefox, so on).</span></span>
3. <span data-ttu-id="d3258-155">在 Adobe&reg; Flash&reg; Player 內欣賞 Smooth Streaming 內容。</span><span class="sxs-lookup"><span data-stu-id="d3258-155">Enjoy Smooth Streaming content inside Adobe&reg; Flash&reg; Player.</span></span>

<span data-ttu-id="d3258-156">如需一般 OSMF 開發的詳細資訊，請參閱官方 [OSMF 開發頁面](http://osmf.org/resources.html)。</span><span class="sxs-lookup"><span data-stu-id="d3258-156">For more information on general OSMF development, please see the official [OSMF development page](http://osmf.org/resources.html).</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="d3258-157">媒體服務學習路徑</span><span class="sxs-lookup"><span data-stu-id="d3258-157">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="d3258-158">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="d3258-158">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="d3258-159">另請參閱</span><span class="sxs-lookup"><span data-stu-id="d3258-159">See Also</span></span>
[<span data-ttu-id="d3258-160">OSMF 的 Microsoft 彈性資料流外掛程式更新 (英文)</span><span class="sxs-lookup"><span data-stu-id="d3258-160">Microsoft Adaptive Streaming Plugin for OSMF Update</span></span>](https://azure.microsoft.com/blog/2014/10/27/microsoft-adaptive-streaming-plugin-for-osmf-update/) 

