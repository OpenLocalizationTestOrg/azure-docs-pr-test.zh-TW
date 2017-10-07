---
title: "aaaInserting 廣告 hello 用戶端 |Microsoft 文件"
description: "本主題說明如何在 tooinsert 廣告 hello 用戶端。"
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 65c9c747-128e-497e-afe0-3f92d2bf7972
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/26/2016
ms.author: juliako
ms.openlocfilehash: e6eab4aa92918ad734db8ac3a4e7818d02ed7fe4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="inserting-ads-on-hello-client-side"></a>插入廣告 hello 用戶端
本主題包含有關如何 tooinsert 各類型廣告 hello 用戶端。

如需了解即時串流視訊的隱藏式字幕和廣告支援，請參閱 [隱藏式字幕支援和廣告插入標準](media-services-live-streaming-with-onprem-encoders.md#cc_and_ads)。

> [!NOTE]
> Azure 媒體播放器目前不支援廣告。
> 
> 

## <a id="insert_ads_into_media"></a>將廣告插入您的媒體
Azure Media Services 提供廣告插入 hello Windows 媒體平台的支援： 播放器架構。 具備廣告支援的播放器架構都適用於 Windows 8、Silverlight、Windows Phone 8 和 iOS 裝置。 每個播放器架構包含範例程式碼，為您示範如何 tooimplement 播放器應用程式。有三種不同的媒體： 清單插入的廣告。

* **線性**– 完整框架廣告暫停 hello 主要影片。
* **非線性**– hello 主要影片播放時顯示的重疊廣告，通常標誌或其他靜態影像用來放置 hello 播放程式內。
* **附屬**– 之外 hello 播放程式會顯示的廣告。

廣告可以放在任何時間點 hello 主要影片的時間線。 您必須告知 hello player tooplay 當 hello ad，以及哪些廣告 tooplay。 使用一組標準的 XML 格式檔案即可搞定：Video Ad Service Template (VAST)、Digital Video Multiple Ad Playlist (VMAP)、Media Abstract Sequencing Template (MAST) 以及 Digital Video Player Ad Interface Definition (VPAID)。 VAST 檔案會指定哪些廣告 toodisplay。 VMAP 檔案會指定何時 tooplay 各種廣告及包含 VAST XML。 MAST 檔案是另一個方式 toosequence 廣告也可包含 VAST XML。 VPAID 檔案會定義 hello 影片播放器與 hello 廣告或廣告伺服器之間的介面。

每個播放器架構的運作方式不同，而且分別涵蓋於各自的主題。 本主題將說明 hello 所使用的基本機制 tooinsert 廣告。影片播放器應用程式會從廣告伺服器要求廣告。 hello ad 伺服器可以回應在數種方式：

* 傳回 VAST 檔案
* 傳回 VMAP 檔案 (有內嵌 VAST)
* 傳回 MAST 檔案 (有內嵌 VAST)
* 傳回 VAST 檔案 (有 VPAID 廣告)

### <a name="using-a-video-ad-service-template-vast-file"></a>使用 Video Ad Service Template (VAST) 檔案
VAST 檔案會指定哪些廣告或廣告 toodisplay。 hello 下列 XML 是線性廣告的 VAST 檔案範例：

    <VAST version="2.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="oxml.xsd">
      <Ad id="115571748">
        <InLine>
          <AdSystem version="2.0 alpha">Atlas</AdSystem>
          <AdTitle>Unknown</AdTitle>
          <Description>Unknown</Description>
          <Survey></Survey>
          <Error></Error>
          <Impression id="Atlas"><![CDATA[http://www.myserver.com/tracking-resource]]></Impression>
          <Creatives>
            <Creative id="video" sequence="0" AdID="">
              <Linear>
                <Duration>00:00:32</Duration>
                <TrackingEvents>
                  <Tracking event="start"><![CDATA[http://www.myserver.com/start-tracking-resource]]></Tracking>
                  <Tracking event="midpoint"><![CDATA[http://www.myserver.com/midpoint-tracking-resource]]></Tracking>
                  <Tracking event="complete"><![CDATA http://www.myserver.com/complete-tracking-resource]]></Tracking>
                  <Tracking event="expand"><![CDATA[http://www.myserver.com/expand-tracking-resource]]></Tracking>
                </TrackingEvents>
                <VideoClicks>
                  <ClickThrough id="Atlas Redirect"><![CDATA[http://www.myserver.com/click-resource]]></ClickThrough>
                  <ClickTracking id="Spare"></ClickTracking>
                </VideoClicks>
                <MediaFiles>
                  <MediaFile apiFramework="Windows Media" id="windows_progressive_200" maintainAspectRatio="true" scaleable="true"  delivery="progressive" bitrate="200" width="400" height="300" type="video/x-ms-wmv">
                    <![CDATA[http://www.myserver.com/media/myad_200_4x3.wmv]]>
                  </MediaFile>
                  <MediaFile apiFramework="Windows Media" id="windows_progressive_300" maintainAspectRatio="true" scaleable="true"  delivery="progressive" bitrate="300" width="400" height="300" type="video/x-ms-wmv">
                    <![CDATA[http://www.myserver.com/media/myad_300_4x3.wmv]]>
                  </MediaFile>
                </MediaFiles>
              </Linear>
            </Creative>
          </Creatives>
          <Extensions>
            <Extension type="Atlas">
            </Extension>
          </Extensions>
        </InLine>
      </Ad>
    </VAST>

hello 線性廣告描述 hello <**線性**> 項目。 它會指定 hello ad hello 持續時間、 追蹤事件、 點選連結、 點選追蹤和一些**MediaFile**項目。 指定追蹤事件在 hello <**TrackingEvents**> 項目，並允許廣告伺服器 tootrack 檢視 hello ad 時所發生的各種事件。 在此情況下 hello 開始、 中點，完成，然後展開會在追蹤事件。 顯示 hello ad 時，就會發生 hello 開始事件。 hello 中間點事件發生時至少已經檢視 50%的 hello 廣告時間軸。 hello 廣告執行 toohello 結束時，就會發生 hello 完成事件。 hello 展開事件發生於 hello 使用者展開視訊播放程式 toofull 囉 」 畫面。 點選連結所指定的 <**點選連結**> 內的項目 <**VideoClicks**> 項目，並指定 URI tooa 資源 toodisplay hello 使用者按一下 hello ad 上時。 點選追蹤中指定 <**點選追蹤**> 項目，也在 hello <**VideoClicks**> 項目，並指定追蹤資源 hello player toorequest hello 使用者按一下時在 hello ad.hello <**MediaFile**> 項目會指定廣告以特定編碼方式的相關資訊。 當有多個 <**MediaFile**> 項目，hello 視訊播放程式可以選擇 hello 最佳編碼方式 hello 平台。 

線性廣告可以依照指定的順序顯示。 toodo，請加入更多<Ad>元素 toohello VAST 檔案，並指定 hello 順序使用 hello 順序屬性。 hello 下列範例將說明這點：

    <VAST version="2.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="oxml.xsd">
      <Ad id="1" sequence="0">
        <InLine>
          <AdSystem version="2.0 alpha">Atlas</AdSystem>
          <AdTitle>Unknown</AdTitle>
          <Description>Unknown</Description>
          <Survey></Survey>
          <Error></Error>
          <Impression id="Atlas"><![CDATA[http://myserver.com/Impression/Ad1trackingResouce]]></Impression>
          <Creatives>
            <Creative id="video" sequence="0" AdID="">
              <Linear>
                <Duration>00:00:32</Duration>
                <MediaFiles>
                  <!-- ... -->
                </MediaFiles>
              </Linear>
            </Creative>
          </Creatives>
        </InLine>
      </Ad>
      <Ad id="2" sequence="1">
        <InLine>
          <AdSystem version="2.0 alpha">Atlas</AdSystem>
          <AdTitle>Unknown</AdTitle>
          <Description>Unknown</Description>
          <Survey></Survey>
          <Error></Error>
          <Impression id="Atlas"><![CDATA[http://myserver.com/Impression/Ad2trackingResouce]]></Impression>
          <Creatives>
            <Creative id="video" sequence="0" AdID="">
              <Linear>
                <Duration>00:00:30</Duration>
                <MediaFiles>
                  <!-- ... -->
                </MediaFiles>
              </Linear>
            </Creative>
          </Creatives>
        </InLine>
      </Ad>
    </VAST>

非線性廣告也是在 <Creative> 元素中指定。 下列範例所示的 hello<Creative>元素，可描述非線性廣告。

    <Creative id="video" sequence="1" AdID="">
      <NonLinearAds>
        <NonLinear width="216" height="121" minSuggestedDuration="00:00:15">
          <StaticResource creativeType="image/png"><![CDATA[http://myserver/images/image.png]]></StaticResource>
          <StaticResource creativeType="image/jpg"><![CDATA[http://myserver/images/image.jpg]]></StaticResource>
        </NonLinear>
        <TrackingEvents>
             <Tracking event="acceptInvitation"><![CDATA[http://myserver/tracking/trackingID]></Tracking>
             <Tracking event="collapse"><![CDATA[http://myserver/tracking/trackingID2]]></Tracking>
         </TrackingEvents>
       </NonLinearAds>
    </Creative>


hello <**NonLinearAds**> 項目可以包含一或多個 <**非線性**> 項目，其中每一個都可以描述非線性廣告。 hello <**非線性**> 項目會指定 hello hello 非線性廣告的資源。 hello 資源可以是 <**StaticResouce**>、 <**IFrameResource**>，或 <**HTMLResouce**>。 <**StaticResource**> 描述非 HTML 資源，並定義指定 hello 資源的顯示方式的 creativeType 屬性：

Image/gif、 image/jpeg、 image/png – hello 資源會顯示在 HTML <**img**> 標記。

應用程式/x-javascript – hello 資源會顯示在 HTML <**指令碼**> 標記。

應用程式/x shockwave-快閃記憶體 – hello 資源會顯示在 Flash player。

**IFrameResource** 說明可在 IFrame 中顯示的 HTML 資源。 **HTMLResource** 說明可插入網頁的 HTML 程式碼片段。 **TrackingEvents**指定追蹤事件和 hello URI toorequest hello 事件發生時。 在此範例 hello 會追蹤 acceptInvitation 和 collapse 事件。 如需有關 hello **NonLinearAds**元素和其子系，請參閱 IAB.NET/VAST。 請注意該 hello **TrackingEvents**項目是位於 hello **NonLinearAds**項目，而不是 hello**非線性**項目。

隨播廣告會在 <CompanionAds> 元素內定義。 hello<CompanionAds>項目可以包含一或多個<Companion>項目。 每個<Companion>項目描述隨播廣告，而且只能包含<StaticResource>， <IFrameResource>，或<HTMLResource>其指定在 hello 方式如所示的非線性廣告相同。 VAST 檔案可以包含多個隨播廣告，而且 hello 播放器應用程式可以選擇最適合 ad toodisplay hello。 如需 VAST 的詳細資訊，請參閱 [VAST 3.0](http://www.iab.net/media/file/VASTv3.0.pdf)。

### <a name="using-a-digital-video-multiple-ad-playlist-vmap-file"></a>使用 Digital Video Multiple Ad Playlist (VMAP) 檔案
VMAP 檔案可讓您 toospecify 時插播廣告、 每個中斷的時間、 內中斷，可以顯示多少廣告和廣告類型可能會中斷期間顯示。 依照 VMAP 檔案範例會定義單一廣告插播的 hello:

    <vmap:VMAP xmlns:vmap="http://www.iab.net/vmap-1.0" version="1.0">
      <vmap:AdBreak breakType="linear" breakId="mypre" timeOffset="start">
        <vmap:AdSource allowMultipleAds="true" followRedirects="true" id="1">
          <vmap:VASTData>
            <VAST version="2.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="oxml.xsd">
              <Ad id="115571748">
                <InLine>
                  <AdSystem version="2.0 alpha">Atlas</AdSystem>
                  <AdTitle>Unknown</AdTitle>
                  <Description>Unknown</Description>
                  <Survey></Survey>
                  <Error></Error>
                  <Impression id="Atlas"><![CDATA[http://view.atdmt.com/000/sview/115571748/direct;ai.201582527;vt.2/01/634364885739970673]]></Impression>
                  <Creatives>
                    <Creative id="video" sequence="0" AdID="">
                      <Linear>
                        <Duration>00:00:32</Duration>
                        <MediaFiles>
                          <MediaFile apiFramework="Windows Media" id="windows_progressive_200" maintainAspectRatio="true" scaleable="true"  delivery="progressive" bitrate="200" width="400" height="300" type="video/x-ms-wmv">
                            <![CDATA[http://smf.blob.core.windows.net/samples/ads/media/XBOX_HD_DEMO_700_1_000_200_4x3.wmv]]>
                          </MediaFile>
                          <MediaFile apiFramework="Windows Media" id="windows_progressive_300" maintainAspectRatio="true" scaleable="true"  delivery="progressive" bitrate="300" width="400" height="300" type="video/x-ms-wmv">
                            <![CDATA[http://smf.blob.core.windows.net/samples/ads/media/XBOX_HD_DEMO_700_2_000_300_4x3.wmv]]>
                          </MediaFile>
                          <MediaFile apiFramework="Windows Media" id="windows_progressive_500" maintainAspectRatio="true" scaleable="true"  delivery="progressive" bitrate="500" width="400" height="300" type="video/x-ms-wmv">
                            <![CDATA[http://smf.blob.core.windows.net/samples/ads/media/XBOX_HD_DEMO_700_1_000_500_4x3.wmv]]>
                          </MediaFile>
                          <MediaFile apiFramework="Windows Media" id="windows_progressive_700" maintainAspectRatio="true" scaleable="true" delivery="progressive" bitrate="700" width="400" height="300" type="video/x-ms-wmv">
                            <![CDATA[http://smf.blob.core.windows.net/samples/ads/media/XBOX_HD_DEMO_700_2_000_700_4x3.wmv]]>
                          </MediaFile>
                        </MediaFiles>
                      </Linear>
                    </Creative>
                  </Creatives>
                </InLine>
              </Ad>
            </VAST>
          </vmap:VASTData>
        </vmap:AdSource>
        <vmap:TrackingEvents>
          <vmap:Tracking event="breakStart">
            http://MyServer.com/breakstart.gif
          </vmap:Tracking>
        </vmap:TrackingEvents>
      </vmap:AdBreak>
    </vmap:VMAP>

VMAP 檔案開頭為 <VMAP> 元素，包含一或多個 <AdBreak> 元素，每個元素都會定義廣告插播。 每個廣告插播都會指定插播類型、插播 ID 和時間位移。 hello breakType 屬性指定 hello hello 插播期間可以播放的廣告類型： 線性、 非線性或顯示。 顯示廣告對應 tooVAST 隨播廣告。 在逗號 (無空格) 分隔的清單中可以指定一個以上的廣告類型。 hello breakID 是廣告 hello 的選擇性識別碼。 hello timeOffset 會指定何時應該顯示 hello ad。 您可以在 hello 下列方式的其中一個指定：

1. 時間 – hh: mm: 或 hh:mm:ss.mmm 的格式，其中.mmm 為毫秒。 hello 這個屬性的值會指定從 hello 影片時間軸 toohello hello 廣告插播開頭 hello 開頭的 hello 時間。
2. 百分比 – 以 n %格式，其中 n 是 hello 影片時間軸 tooplay hello 百分比之前播放 hello ad
3. 開始/結束 – 指定廣告應該在之前或之後顯示 hello 視訊顯示
4. 位置 – 指定 hello 的廣告插播的順序，未知，例如即時串流的 hello 廣告插播的 hello 逾時。 指定的每個廣告插播的 hello 順序 hello #n 格式，其中 n 是 1 或更大的整數。 1 表示應該播放廣告 hello 在 hello 第一個機會，2 表示 hello 應該播放廣告在 hello 第二個機會，依此類推。

在 hello <**AdBreak**> 有項目可以是其中一個 <**AdSource**> 項目。 hello <**AdSource**> 項目包含下列屬性的 hello:

1. Id – 指定 hello 廣告來源的識別碼
2. allowMultipleAds – 指定在 hello 廣告插播期間是否可以顯示多個廣告的布林值
3. followRedirects – 選擇性的布林值，指定是否 hello 影片播放器應該接受廣告回應內重新導向

hello <**AdSource**> 項目會提供 hello 播放程式內嵌廣告回應或參考 tooan 廣告回應。 它可以包含下列項目 hello 的其中一個：

* <VASTAdData>表示 VAST 廣告回應內嵌在 hello VMAP 檔案
* <AdTagURI> 從另一個系統參考廣告回應的 URI
* <CustomAdData> -表示非 VAST 回應的任意字串

在這個範例中，內嵌廣告回應是以 <VASTAdData> 元素指定，該元素包含 VAST 廣告回應。 如需有關 hello 其他項目，請參閱[VMAP](http://www.iab.net/guidelines/508676/digitalvideo/vsuite/vmap)。

hello <**AdBreak**> 項目也可以包含一個 <**TrackingEvents**> 項目。 hello <**TrackingEvents**> 元素可讓您 tootrack hello 開頭或結尾廣告插播或 hello 廣告插播期間是否發生錯誤。 hello <**TrackingEvents**> 元素包含一或多個 <**追蹤**> 項目，其中每個指定的追蹤事件和追蹤 URI。 hello 可能的追蹤事件如下：

1. breakStart – 追蹤廣告插播的 hello 開頭
2. breakEnd – 追蹤廣告插播的 hello 完成
3. error – 追蹤 hello 廣告插播期間發生錯誤

hello 下列範例會示範指定追蹤事件的 VMAP 檔案

    <vmap:VMAP xmlns:vmap="http://www.iab.net/vmap-1.0" version="1.0">
      <vmap:AdBreak breakType="linear" breakId="mypre" timeOffset="start">
        <vmap:AdSource allowMultipleAds="true" followRedirects="true" id="1">
          <vmap:VASTData>
            <!--Inline VAST -->
          </vmap:VASTData>
        </vmap:AdSource>
        <vmap:TrackingEvents>
          <vmap:Tracking event="breakStart">
            http://MyServer.com/breakstart.gif
          </vmap:Tracking>
          <vmap:Tracking event="breakend">
            http://MyServer.com/breakend.gif
          </vmap:Tracking>
          <vmap:Tracking event="error">
            http://MyServer.com/error.gif
          </vmap:Tracking>
        </vmap:TrackingEvents>
      </vmap:AdBreak>
    </vmap:VMAP>

如需有關 hello <**TrackingEvents**> 元素和其子系，請參閱 http://iab.org/VMAP.pdf

### <a name="using-a-media-abstract-sequencing-template-mast-file"></a>使用 Media Abstract Sequencing Template (MAST) 檔案
MAST 檔案可讓您定義何時顯示廣告的 toospecify 觸發程序。 hello 以下是範例 MAST 檔案，其中包含觸發程序前廣告、 片中廣告和片尾廣告。

    <MAST xsi:schemaLocation="http://openvideoplayer.sf.net/mast http://openvideoplayer.sf.net/mast/mast.xsd" xmlns="http://openvideoplayer.sf.net/mast" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
      <triggers>
        <trigger id="preroll" description="preroll every item"  >
          <startConditions>
            <condition type="event" name="OnItemStart" />
          </startConditions>
          <sources>
            <source uri="http://smf.blob.core.windows.net/samples/win8/ads/vast_linear.xml" format="vast">
              <sources />
            </source>
          </sources>
        </trigger>

        <trigger id="midroll" description="midroll at 15 sec."  >
          <startConditions>
            <condition type="property" name="Position" value="00:00:15.0" operator="GEQ" />
          </startConditions>
          <endConditions>
            <condition type="event" name="OnItemEnd"/>
            <!--This 'resets' hello trigger for hello next clip-->
          </endConditions>
          <sources>
            <source uri="http://smf.blob.core.windows.net/samples/win8/ads/vast_linear.xml" format="vast">
              <sources />
            </source>
          </sources>
        </trigger>

        <trigger id="postroll" description="postroll"  >
          <startConditions>
            <condition type="event" name="OnItemEnd"/>
          </startConditions>
          <sources>
            <source uri="http://smf.blob.core.windows.net/samples/win8/ads/vast_linear.xml" format="vast">
              <sources />
            </source>
          </sources>
        </trigger>
      </triggers>
    </MAST>



MAST 檔案開頭為 **MAST** 元素，其中包含一個 **triggers** 元素。 hello<triggers>元素包含一或多個**觸發程序**項目會定義何時應該播放廣告。 

hello**觸發程序**元素包含**startConditions**指定廣告應該在何時開始 tooplay 項目。 hello **startConditions**元素包含一或多個<condition>項目。 當每個<condition>評估的 tootrue 觸發程序，起始或撤銷根據 hello<condition>內含**startConditions**或**endConditions**項目分別。 當多個<condition>項目都存在，則會視為隱含 OR，評估 tootrue 任何條件會導致 hello 觸發程序 tooinitiate。 <condition> 元素可以為巢狀。 當子<condition>都有預設項目，則會視為隱含 AND，所有條件必須都評估為 hello 觸發程序 tooinitiate tootrue。 hello<condition>元素包含下列屬性可定義 hello 條件 hello: 

1. **型別**– 指定條件、 事件或屬性的 hello 類型
2. **名稱**– hello hello 屬性或事件 toobe 評估期間使用的名稱
3. **值**– hello 會針對評估屬性的值
4. **運算子**– 評估期間 hello 作業 toouse: EQ （等於）、 NEQ （不等於）、 GTR (greater)、 GEQ （大於或等於）、 LT （小於）、 LEQ （小於或等於）、 MOD （模數）

**endConditions** 也會包含 <condition> 元素。 當條件評估 tootrue hello 觸發程序是 reset.hello<trigger>項目也包含<sources>包含一或多個項目<source>項目。 hello<source>元素會定義 hello URI toohello 廣告回應 hello 廣告回應的類型。 在這個範例 URI 會指定 tooa VAST 回應。 

    <trigger id="postroll" description="postroll"  >
      <startConditions>
        <condition/>
      </startConditions>
      <sources>
        <source uri="http://smf.blob.core.windows.net/samples/win8/ads/vast_linear.xml" format="vast">
          <sources />
        </source>
      </sources>
    </trigger>


### <a name="using-video-player-ad-interface-definition-vpaid"></a>使用 Video Player-Ad Interface Definition (VPAID)
VPAID 是啟用可執行的廣告單元 toocommunicate 與視訊播放程式的 API。 如此可提供高度互動性與體驗。 hello 廣告可以回應 hello 檢視器所採取的 tooactions 與 hello 使用者可以互動 hello ad。 例如廣告可能會顯示按鈕，好讓 hello 使用者 tooview hello 廣告的加長版或更多的資訊。 hello 視訊播放程式必須支援 VPAID API hello 和 hello 可執行的廣告必須實作 hello API。 當播放程式從廣告伺服器 hello 伺服器要求廣告回應可能會包含 VPAID 廣告的 VAST 回應。

必須在如 Adobe Flash™ 或可以在網頁瀏覽器中執行的 JavaScript 執行階段環境中執行的程式碼中建立可執行廣告。 Ad 伺服器會傳回包含 VPAID 廣告的 VAST 回應 hello hello hello 中 apiFramework 屬性的值<MediaFile>項目必須為"VPAID"。 這個屬性會指定該 hello 包含 ad 是可執行的 VPAID 廣告。 hello type 屬性必須設定 hello toohello MIME 類型可執行檔，例如 「 應用程式/x shockwave-快閃記憶體"或"應用程式/x-javascript"。 hello 下列 XML 程式碼片段示範 hello<MediaFile>包含可執行的 VPAID 廣告的 VAST 回應中的項目。 

    <MediaFiles>
       <MediaFile id="1" delivery="progressive" type=”application/x-shockwaveflash”
                  width=”640” height=”480” apiFramework=”VPAID”>
           <!-- CDATA wrapped URI tooexecutable ad -->
       </MediaFile>
    </MediaFiles>


可執行的廣告可以使用 hello 初始化<AdParameters>hello 內的項目<Linear>或<NonLinear>VAST 回應中的項目。 如需有關 hello<AdParameters>項目，請參閱[VAST 3.0](http://www.iab.net/media/file/VASTv3.0.pdf)。 如需 hello VPAID API 的詳細資訊，請參閱[VPAID 2.0](http://www.iab.net/media/file/VPAID_2.0_Final_04-10-2012.pdf)。

## <a name="implementing-a-windows-or-windows-phone-8-player-with-ad-support"></a>實作包含廣告支援的 Windows 或 Windows Phone 8 播放器
hello Microsoft 媒體平台： Player Framework for Windows 8 和 Windows Phone 8 包含範例應用程式可為您示範如何使用影片播放器應用程式的 tooimplement hello 架構的集合。 您可以下載從 hello 播放器架構和 hello 範例[Player Framework for Windows 8 和 Windows Phone 8](https://playerframework.codeplex.com)。

當您開啟 hello Microsoft.PlayerFramework.Xaml.Samples 方案時您會看到 hello 專案中資料夾的數目。 hello Advertising 資料夾包含 hello 範例程式碼相關 toocreating 包含廣告支援的視訊播放程式。 內部 hello Advertising 資料夾是 XAML/cs 檔案數目每哪一個節目如何以不同方式 tooinsert 廣告。 hello 下列清單描述每個：

* AdPodPage.xaml 顯示如何 toodisplay ad pod。
* AdSchedulingPage.xaml 顯示如何 tooschedule 廣告。
* FreeWheelPage.xaml 顯示 toouse hello FreeWheel 外掛程式 tooschedule 廣告的方式。
* MastPage.xaml 顯示如何使用 MAST 檔案 tooschedule 廣告。
* ProgrammaticAdPage.xaml 顯示如何 tooprogrammatically 在影片中排程廣告。
* ScheduleClipPage.xaml 顯示如何 tooschedule ad 不使用 VAST 檔案。
* VastLinearCompanionPage.xaml 顯示如何 tooinsert 線性和隨播廣告。
* VastNonLinearPage.xaml 顯示如何 tooinsert 非線性廣告。
* VmapPage.xaml 顯示如何使用 VMAP 檔案 toospecify 廣告。

每個範例會使用 hello 播放器架構所定義的 hello MediaPlayer 類別。 大部分的範例會使用加入各種廣告回應格式支援的外掛程式。 hello ProgrammaticAdPage 範例以程式設計方式互動的 MediaPlayer 例項。

### <a name="adpodpage-sample"></a>AdPodPage 範例
這個範例會使用 hello AdSchedulerPlugin toodefine 時 toodisplay 廣告。 在此範例中，片中廣告是排程的 toobe 5 秒鐘之後播放。 從廣告伺服器傳回的 VAST 檔案中指定 hello ad pod （廣告 toodisplay 順序群組）。 hello URI toohello VAST 檔案會指定在 hello<RemoteAdSource>項目。

    <mmppf:MediaPlayer x:Name="player" Source="http://smf.blob.core.windows.net/samples/videos/bigbuck.mp4">

        <mmppf:MediaPlayer.Plugins>
            <ads:AdSchedulerPlugin>
                <ads:AdSchedulerPlugin.Advertisements>

                    <ads:MidrollAdvertisement Time="00:00:05">
                        <ads:MidrollAdvertisement.Source>
                            <ads:RemoteAdSource Uri="http://smf.blob.core.windows.net/samples/win8/ads/vast_adpod.xml" Type="vast"/>
                        </ads:MidrollAdvertisement.Source>
                    </ads:MidrollAdvertisement>

                </ads:AdSchedulerPlugin.Advertisements>
            </ads:AdSchedulerPlugin>
            <ads:AdHandlerPlugin/>
        </mmppf:MediaPlayer.Plugins>
    </mmppf:MediaPlayer>

如需 hello AdSchedulerPlugin 的詳細資訊，請參閱[hello Windows 8 和 Windows Phone 8 播放器架構中進行通告](http://playerframework.codeplex.com/wikipage?title=Advertising&referringTitle=Windows%208%20Player%20Documentation)

### <a name="adschedulingpage"></a>AdSchedulingPage
此範例也會使用 hello AdSchedulerPlugin。 它會排程三個廣告，片頭廣告、片中廣告和片尾廣告。 每個 ad 指定的 hello URI toohello VAST<RemoteAdSource>項目。

    <mmppf:MediaPlayer x:Name="player" Source="http://smf.blob.core.windows.net/samples/videos/bigbuck.mp4">
                <mmppf:MediaPlayer.Plugins>
                    <ads:AdSchedulerPlugin>
                        <ads:AdSchedulerPlugin.Advertisements>

                            <ads:PrerollAdvertisement>
                                <ads:PrerollAdvertisement.Source>
                                    <ads:RemoteAdSource Uri="http://smf.blob.core.windows.net/samples/win8/ads/vast_linear.xml" Type="vast"/>
                                </ads:PrerollAdvertisement.Source>
                            </ads:PrerollAdvertisement>

                            <ads:MidrollAdvertisement Time="00:00:15">
                                <ads:MidrollAdvertisement.Source>
                                    <ads:RemoteAdSource Uri="http://smf.blob.core.windows.net/samples/win8/ads/vast_linear.xml" Type="vast"/>
                                </ads:MidrollAdvertisement.Source>
                            </ads:MidrollAdvertisement>

                            <ads:PostrollAdvertisement>
                                <ads:PostrollAdvertisement.Source>
                                    <ads:RemoteAdSource Uri="http://smf.blob.core.windows.net/samples/win8/ads/vast_linear.xml" Type="vast"/>
                                </ads:PostrollAdvertisement.Source>
                            </ads:PostrollAdvertisement>

                        </ads:AdSchedulerPlugin.Advertisements>
                    </ads:AdSchedulerPlugin>
                    <ads:AdHandlerPlugin/>
                </mmppf:MediaPlayer.Plugins>
            </mmppf:MediaPlayer>


### <a name="freewheelpage"></a>FreeWheelPage
這個範例會使用 hello FreeWheelPlugin 指定指定的 URI 指定廣告內容以及廣告排程資訊該點 tooa SmartXML 檔案的來源屬性。

    <mmppf:MediaPlayer x:Name="player" Source="http://smf.blob.core.windows.net/samples/videos/bigbuck.mp4">
                <mmppf:MediaPlayer.Plugins>
                    <ads:FreeWheelPlugin Source="http://smf.blob.core.windows.net/samples/win8/ads/freewheel.xml"/>
                    <ads:AdHandlerPlugin/>
                </mmppf:MediaPlayer.Plugins>
            </mmppf:MediaPlayer>

### <a name="mastpage"></a>MastPage
這個範例會使用 hello MastSchedulerPlugin，可讓您 toouse MAST 檔案。 hello Source 屬性會指定 hello hello MAST 檔案位置。

    <mmppf:MediaPlayer x:Name="player" Source="http://smf.blob.core.windows.net/samples/videos/bigbuck.mp4">
                <mmppf:MediaPlayer.Plugins>
                    <ads:MastSchedulerPlugin Source="http://smf.blob.core.windows.net/samples/win8/ads/mast.xml" />
                    <ads:AdHandlerPlugin/>
                </mmppf:MediaPlayer.Plugins>
            </mmppf:MediaPlayer>

### <a name="programmaticadpage"></a>ProgrammaticAdPage
此範例以程式設計的方式會與 hello MediaPlayer 互動。 hello ProgrammaticAdPage.xaml 檔案會具現化 hello MediaPlayer:

    <mmppf:MediaPlayer x:Name="player" Source="http://smf.blob.core.windows.net/samples/videos/bigbuck.mp4"/>

hello ProgrammaticAdPage.xaml.cs 檔案會建立 AdHandlerPlugin、 廣告應該顯示，並將其載入 RemoteAdSource 指定 URI tooa VAST 檔案，並再播放 hello MarkerReached 事件的處理常式時，加入 TimelineMarker toospecifyhello ad。

    public sealed partial class ProgrammaticAdPage : Microsoft.PlayerFramework.Samples.Common.LayoutAwarePage
        {
            AdHandlerPlugin adHandler;

            public ProgrammaticAdPage()
            {
                this.InitializeComponent();
                adHandler = new AdHandlerPlugin();
                player.Plugins.Add(new AdHandlerPlugin());
                player.Markers.Add(new TimelineMarker() { Time = TimeSpan.FromSeconds(5), Type = "myAd" });
                player.MarkerReached += pf_MarkerReached;
            }

            async void pf_MarkerReached(object sender, TimelineMarkerRoutedEventArgs e)
            {
                if (e.Marker.Type == "myAd")
                {
                    var adSource = new RemoteAdSource() { Type = VastAdPayloadHandler.AdType, Uri = new Uri("http://smf.blob.core.windows.net/samples/win8/ads/vast_linear.xml") };
                    //var adSource = new AdSource() { Type = DocumentAdPayloadHandler.AdType, Payload = SampleAdDocument };
                    var progress = new Progress<AdStatus>();
                    try
                    {
                        await player.PlayAd(adSource, progress, CancellationToken.None);
                    }
                    catch { /* ignore */ }
                }
            }

### <a name="scheduleclippage"></a>ScheduleClipPage
這個範例會指定包含 hello 廣告的.wmv 檔案來使用 hello AdSchedulerPlugin tooschedule 片中廣告。

    <mmppf:MediaPlayer x:Name="player" Source="http://smf.cloudapp.net/html5/media/bigbuck.mp4">
                <mmppf:MediaPlayer.Plugins>
                    <ads:AdSchedulerPlugin>
                        <ads:AdSchedulerPlugin.Advertisements>

                            <ads:MidrollAdvertisement Time="00:00:05">
                                <ads:MidrollAdvertisement.Source>
                                    <ads:AdSource Type="clip">
                                        <ads:AdSource.Payload>
                                            <ads:ClipAdPayload MediaSource="http://smf.blob.core.windows.net/samples/ads/media/XBOX_HD_DEMO_700_2_000_700_4x3.wmv" MimeType="video/x-ms-wmv" />
                                        </ads:AdSource.Payload>
                                    </ads:AdSource>
                                </ads:MidrollAdvertisement.Source>
                            </ads:MidrollAdvertisement>

                        </ads:AdSchedulerPlugin.Advertisements>
                    </ads:AdSchedulerPlugin>
                    <ads:AdHandlerPlugin/>
                </mmppf:MediaPlayer.Plugins>
            </mmppf:MediaPlayer>

### <a name="vastlinearcompanionpage"></a>VastLinearCompanionPage
此範例說明如何 toouse 會 hello AdSchedulerPlugin tooschedule 片中的線性廣告與隨播廣告。 hello<RemoteAdSource>項目會指定 hello hello VAST 檔案位置。

    <mmppf:MediaPlayer Grid.Row="1"  x:Name="player" Source="http://smf.blob.core.windows.net/samples/videos/bigbuck.mp4">
                <mmppf:MediaPlayer.Plugins>
                    <ads:AdSchedulerPlugin>
                        <ads:AdSchedulerPlugin.Advertisements>

                            <ads:MidrollAdvertisement Time="00:00:05">
                                <ads:MidrollAdvertisement.Source>
                                    <ads:RemoteAdSource Uri="http://smf.blob.core.windows.net/samples/win8/ads/vast_linear_companions.xml" Type="vast"/>
                                </ads:MidrollAdvertisement.Source>
                            </ads:MidrollAdvertisement>

                        </ads:AdSchedulerPlugin.Advertisements>
                    </ads:AdSchedulerPlugin>
                    <ads:AdHandlerPlugin/>
                </mmppf:MediaPlayer.Plugins>
            </mmppf:MediaPlayer>

### <a name="vastlinearnonlinearpage"></a>VastLinearNonLinearPage
這個範例會使用 hello AdSchedulerPlugin tooschedule 線性與非線性廣告。 hello VAST 檔案位置指定 hello<RemoteAdSource>項目。

    <mmppf:MediaPlayer x:Name="player" Source="http://smf.blob.core.windows.net/samples/videos/bigbuck.mp4">
                <mmppf:MediaPlayer.Plugins>
                    <ads:AdSchedulerPlugin>
                        <ads:AdSchedulerPlugin.Advertisements>

                            <ads:MidrollAdvertisement Time="00:00:05">
                                <ads:MidrollAdvertisement.Source>
                                    <ads:RemoteAdSource Uri="http://smf.blob.core.windows.net/samples/win8/ads/vast_linear_nonlinear.xml" Type="vast"/>
                                </ads:MidrollAdvertisement.Source>
                            </ads:MidrollAdvertisement>

                        </ads:AdSchedulerPlugin.Advertisements>
                    </ads:AdSchedulerPlugin>
                    <ads:AdHandlerPlugin/>
                </mmppf:MediaPlayer.Plugins>
            </mmppf:MediaPlayer>

### <a name="vmappage"></a>VMAPPage
此範例使用使用 VMAP 檔案 hello VmapSchedulerPlugin tooschedule 廣告。 hello hello Source 屬性中指定 hello URI toohello VMAP 檔案<VmapSchedulerPlugin>項目。

    <mmppf:MediaPlayer x:Name="player" Source="http://smf.blob.core.windows.net/samples/videos/bigbuck.mp4">
                <mmppf:MediaPlayer.Plugins>
                    <ads:VmapSchedulerPlugin Source="http://smf.blob.core.windows.net/samples/win8/ads/vmap.xml"/>
                    <ads:AdHandlerPlugin/>
                </mmppf:MediaPlayer.Plugins>
            </mmppf:MediaPlayer>

## <a name="implementing-an-ios-video-player-with-ad-support"></a>實作具有廣告支援的 iOS 視訊播放器
hello Microsoft 媒體平台： 適用於 iOS 的播放器架構包含範例應用程式可為您示範如何使用影片播放器應用程式的 tooimplement hello 架構的集合。 您可以下載從 hello 播放器架構和 hello 範例[Azure Media Player Framework](https://github.com/Azure/azure-media-player-framework)。 hello github 頁面有 Wiki，包含上 hello 播放器架構和簡介 toohello 播放器範例的其他資訊的連結 tooa: [Azure 媒體播放器 Wiki](https://github.com/Azure/azure-media-player-framework/wiki/How-to-use-Azure-media-player-framework)。

### <a name="scheduling-ads-with-vmap"></a>使用 VMAP 排程廣告
hello 下列範例會示範如何使用 VMAP 檔案 tooschedule 廣告。

    // How tooschedule an Ad using VMAP.
    //First download hello VMAP manifest

    if (![framework.adResolver downloadManifest:&manifest withURL:[NSURL URLWithString:@"http://portalvhdsq3m25bf47d15c.blob.core.windows.net/vast/PlayerTestVMAP.xml"]])
            {
                [self logFrameworkError];
            }
            else
            {
                // Schedule a list of ads using hello downloaded VMAP manifest
                if (![framework scheduleVMAPWithManifest:manifest])
                {
                    [self logFrameworkError];
                }          
            }

### <a name="scheduling-ads-with-vast"></a>使用 VAST 排程廣告
hello 以下範例將示範如何 tooschedule 晚期繫結的 VAST 廣告。

    //Example:3 How tooschedule a late binding VAST ad.
    // set hello start time for hello ad
    adLinearTime.startTime = 13;
    adLinearTime.duration = 0;
    // Specify hello URI of hello VAST file
    NSString *vastAd1=@"http://portalvhdsq3m25bf47d15c.blob.core.windows.net/vast/PlayerTestVAST.xml";
    // Create an AdInfo object
     AdInfo *vastAdInfo1 = [[[AdInfo alloc] init] autorelease];
    // set URL tooVAST file
    vastAdInfo1.clipURL = [NSURL URLWithString:vastAd1];
    // set running time of ad
    vastAdInfo1.mediaTime = [[[MediaTime alloc] init] autorelease];
    vastAdInfo1.mediaTime.clipBeginMediaTime = 0;
    vastAdInfo1.mediaTime.clipEndMediaTime = 10;
    vastAdInfo1.policy = @"policy for late binding VAST";
    // specify ad type
    vastAdInfo1.type = AdType_Midroll;
    vastAdInfo1.appendTo=-1;
    adIndex = 0;
    // schedule ad
    if (![framework scheduleClip:vastAdInfo1 atTime:adLinearTime forType:PlaylistEntryType_VAST andGetClipId:&adIndex])
    {
        [self logFrameworkError];
    }

   hello 以下範例將示範如何 tooschedule 早期繫結的 VAST 廣告。
早期繫結 VAST 廣告 //Download hello VAST 檔案範例： 4 排程 (！ [framework.adResolver downloadManifest： 資訊清單和 withURL: [NSURL URLWithString: @"http://portalvhdsq3m25bf47d15c.blob.core.windows.net/vast/PlayerTestVAST.xml"]]) {[自我 logFrameworkError];} else {adLinearTime.startTime = 7。adLinearTime.duration = 0;

        // Create AdInfo instance
        AdInfo *vastAdInfo2 = [[[AdInfo alloc] init] autorelease];
        vastAdInfo2.mediaTime = [[[MediaTime alloc] init] autorelease];
        vastAdInfo2.policy = @"policy for early binding VAST";
        // specify ad type
        vastAdInfo2.type = AdType_Midroll;
        vastAdInfo2.appendTo=-1;
        // schedule ad
        if (![framework scheduleVASTClip:vastAdInfo2 withManifest:manifest atTime:adLinearTime andGetClipId:&adIndex])
        {
            [self logFrameworkError];
        }
    }

hello 以下範例將示範如何 tooinsert ad 使用粗略剪下編輯 (R)

    //Example:1 How toouse RCE.
    // specify manifest for ad content
    NSString *secondContent=@"http://wamsblureg001orig-hs.cloudapp.net/6651424c-a9d1-419b-895c-6993f0f48a26/The%20making%20of%20Microsoft%20Surface-m3u8-aapl.ism/Manifest(format=m3u8-aapl)";

    // specify ad length
    mediaTime.currentPlaybackPosition = 0;
    mediaTime.clipBeginMediaTime = 0;
    mediaTime.clipEndMediaTime = 80;
    // append ad content
    if (![framework appendContentClip:[NSURL URLWithString:secondContent] withMediaTime:mediaTime andGetClipId:&clipId])
    {
        [self logFrameworkError];
    }

hello 下列範例顯示如何 tooschedule ad pod。

    //Example:5 Schedule an ad Pod.
    // Set start time for ad
    adLinearTime.startTime = 23;
    adLinearTime.duration = 0;

    // Specify URL toocontent
    NSString *adpodSt1=@"https://portalvhdsq3m25bf47d15c.blob.core.windows.net/asset-e47b43fd-05dc-4587-ac87-5916439ad07f/Windows%208_%20Cliffjumpers.mp4?st=2012-11-28T16%3A31%3A57Z&se=2014-11-28T16%3A31%3A57Z&sr=c&si=2a6dbb1e-f906-4187-a3d3-7e517192cbd0&sig=qrXYZBekqlbbYKqwovxzaVZNLv9cgyINgMazSCbdrfU%3D";
    // Create an AdInfo instance
    AdInfo *adpodInfo1 = [[[AdInfo alloc] init] autorelease];
    // set URI tooad content
    adpodInfo1.clipURL = [NSURL URLWithString:adpodSt1];
    // Set ad running time
    adpodInfo1.mediaTime = [[[MediaTime alloc] init] autorelease];
    adpodInfo1.mediaTime.clipBeginMediaTime = 0;
    adpodInfo1.mediaTime.clipEndMediaTime = 17;
    adpodInfo1.policy = @"policy for ad pod 1";
    // Set ad type
    adpodInfo1.type = AdType_Midroll;
    adpodInfo1.appendTo=-1;
    adIndex = 0;
    // Schedule ad
    if (![framework scheduleClip:adpodInfo1 atTime:adLinearTime forType:PlaylistEntryType_Media andGetClipId:&adIndex])
    {
        [self logFrameworkError];
    }

下列範例會示範如何 hello tooschedule 非重複性片中廣告。 不論任何搜尋 hello 檢視器會執行之後，非重複性廣告只會播放。

    //Example:6 Schedule a single non sticky mid roll Ad
    // specify URL toocontent
    NSString *oneTimeAd=@"http://wamsblureg001orig-hs.cloudapp.net/5389c0c5-340f-48d7-90bc-0aab664e5f02/Windows%208_%20You%20and%20Me%20Together-m3u8-aapl.ism/Manifest(format=m3u8-aapl)";

    // create an AdInfo instance
    AdInfo *oneTimeInfo = [[[AdInfo alloc] init] autorelease];
    // set URL of ad
    oneTimeInfo.clipURL = [NSURL URLWithString:oneTimeAd];
    oneTimeInfo.mediaTime = [[[MediaTime alloc] init] autorelease];
    oneTimeInfo.mediaTime.clipBeginMediaTime = 0;
    oneTimeInfo.mediaTime.clipEndMediaTime = -1;
    oneTimeInfo.policy = @"policy for one-time ad";
    // set ad start time
    adLinearTime.startTime = 43;
    adLinearTime.duration = 0;
    // set ad type
    oneTimeInfo.type = AdType_Midroll;
    // non sticky ad
    oneTimeInfo.deleteAfterPlayed = YES;
    // schedule ad
    if (![framework scheduleClip:oneTimeInfo atTime:adLinearTime forType:PlaylistEntryType_Media andGetClipId:&adIndex])
    {
        [self logFrameworkError];
    }

下列範例會示範如何 hello tooschedule 重複性片中廣告。 重複性廣告會顯示 hello 指定 hello 影片時間軸上的點已達到每個時間。

    //Example:7 Schedule a single sticky mid roll Ad
    NSString *stickyAd=@"http://wamsblureg001orig-hs.cloudapp.net/2e4e7d1f-b72a-4994-a406-810c796fc4fc/The%20Surface%20Movement-m3u8-aapl.ism/Manifest(format=m3u8-aapl)";
    // create AdInfo instance
    AdInfo *stickyAdInfo = [[[AdInfo alloc] init] autorelease];
    // set URI tooad
    stickyAdInfo.clipURL = [NSURL URLWithString:stickyAd];
    stickyAdInfo.mediaTime = [[[MediaTime alloc] init] autorelease];
    stickyAdInfo.mediaTime.clipBeginMediaTime = 0;
    stickyAdInfo.mediaTime.clipEndMediaTime = 15;
    stickyAdInfo.policy = @"policy for sticky mid-roll ad";
    // set ad start time
    adLinearTime.startTime = 64;
    adLinearTime.duration = 0;
    // set ad type
    stickyAdInfo.type = AdType_Midroll;
    stickyAdInfo.deleteAfterPlayed = NO;
    // schedule ad
    if (![framework scheduleClip:stickyAdInfo atTime:adLinearTime forType:PlaylistEntryType_Media andGetClipId:&adIndex])
    {
        [self logFrameworkError];
    }


hello 以下範例將示範如何 tooschedule 片尾廣告。

    //Example:8 Schedule Post Roll Ad
    NSString *postAdURLString=@"http://wamsblureg001orig-hs.cloudapp.net/aa152d7f-3c54-487b-ba07-a58e0e33280b/wp-m3u8-aapl.ism/Manifest(format=m3u8-aapl)";
    // create AdInfo instance
    AdInfo *postAdInfo = [[[AdInfo alloc] init] autorelease];
    postAdInfo.clipURL = [NSURL URLWithString:postAdURLString];
    postAdInfo.mediaTime = [[[MediaTime alloc] init] autorelease];
    postAdInfo.mediaTime.clipBeginMediaTime = 0;
    // set ad length
    postAdInfo.mediaTime.clipEndMediaTime = 45;
    postAdInfo.policy = @"policy for post-roll ad";
    // set ad type
    postAdInfo.type = AdType_Postroll;
    adLinearTime.duration = 0;
    if (![framework scheduleClip:postAdInfo atTime:adLinearTime forType:PlaylistEntryType_Media andGetClipId:&adIndex])
    {
        [self logFrameworkError];
    }

hello 以下範例將示範如何 tooschedule 前廣告。

    //Example:9 Schedule Pre Roll Ad
    NSString *adURLString = @"http://wamsblureg001orig-hs.cloudapp.net/2e4e7d1f-b72a-4994-a406-810c796fc4fc/The%20Surface%20Movement-m3u8-aapl.ism/Manifest(format=m3u8-aapl)";
    AdInfo *adInfo = [[[AdInfo alloc] init] autorelease];
    adInfo.clipURL = [NSURL URLWithString:adURLString];
    adInfo.mediaTime = [[[MediaTime alloc] init] autorelease];
    adInfo.mediaTime.currentPlaybackPosition = 0;
    adInfo.mediaTime.clipBeginMediaTime = 40; //You could play a portion of an Ad. Yeh!
    adInfo.mediaTime.clipEndMediaTime = 59;
    adInfo.policy = @"policy for pre-roll ad";
    adInfo.appendTo = -1;
    adInfo.type = AdType_Preroll;
    adLinearTime.duration = 0;
    // schedule ad
    if (![framework scheduleClip:adInfo atTime:adLinearTime forType:PlaylistEntryType_Media andGetClipId:&adIndex])
    {
        [self logFrameworkError];
    }

hello 下列範例顯示如何 tooschedule 中間彙重疊廣告。

    // Example10: Schedule a Mid Roll overlay Ad
    NSString *adURLString = @"https://portalvhdsq3m25bf47d15c.blob.core.windows.net/asset-e47b43fd-05dc-4587-ac87-5916439ad07f/Windows%208_%20Cliffjumpers.mp4?st=2012-11-28T16%3A31%3A57Z&se=2014-11-28T16%3A31%3A57Z&sr=c&si=2a6dbb1e-f906-4187-a3d3-7e517192cbd0&sig=qrXYZBekqlbbYKqwovxzaVZNLv9cgyINgMazSCbdrfU%3D";
    //Create AdInfo instance
    AdInfo *adInfo = [[[AdInfo alloc] init] autorelease];
    adInfo.clipURL = [NSURL URLWithString:adURLString];
    adInfo.mediaTime = [[[MediaTime alloc] init] autorelease];
    adInfo.mediaTime.currentPlaybackPosition = 0;
    adInfo.mediaTime.clipBeginMediaTime = 0;
    // specify ad length
    adInfo.mediaTime.clipEndMediaTime = 20;
    adInfo.policy = @"policy for mid-roll overlay ad";
    adInfo.appendTo = -1;
    // specify ad type
    adInfo.type = AdType_Midroll;
    // specify ad start time & duration
    adLinearTime.startTime = 300;
    adLinearTime.duration = 20;
    // schedule ad            if (![framework scheduleClip:adInfo atTime:adLinearTime forType:PlaylistEntryType_Media andGetClipId:&adIndex])
    {
        [self logFrameworkError];
    }



## <a name="media-services-learning-paths"></a>媒體服務學習路徑
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>提供意見反應
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a>另請參閱
[開發視訊播放程式應用程式](media-services-develop-video-players.md)

