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
# <a name="inserting-ads-on-hello-client-side"></a><span data-ttu-id="a3ca0-103">插入廣告 hello 用戶端</span><span class="sxs-lookup"><span data-stu-id="a3ca0-103">Inserting ads on hello client side</span></span>
<span data-ttu-id="a3ca0-104">本主題包含有關如何 tooinsert 各類型廣告 hello 用戶端。</span><span class="sxs-lookup"><span data-stu-id="a3ca0-104">This topic contains information on how tooinsert various types of ads on hello client side.</span></span>

<span data-ttu-id="a3ca0-105">如需了解即時串流視訊的隱藏式字幕和廣告支援，請參閱 [隱藏式字幕支援和廣告插入標準](media-services-live-streaming-with-onprem-encoders.md#cc_and_ads)。</span><span class="sxs-lookup"><span data-stu-id="a3ca0-105">For information about closed captioning and ad support in Live streaming videos, see [Supported Closed Captioning and Ad Insertion Standards](media-services-live-streaming-with-onprem-encoders.md#cc_and_ads).</span></span>

> [!NOTE]
> <span data-ttu-id="a3ca0-106">Azure 媒體播放器目前不支援廣告。</span><span class="sxs-lookup"><span data-stu-id="a3ca0-106">Azure Media Player does not currently support Ads.</span></span>
> 
> 

## <span data-ttu-id="a3ca0-107"><a id="insert_ads_into_media"></a>將廣告插入您的媒體</span><span class="sxs-lookup"><span data-stu-id="a3ca0-107"><a id="insert_ads_into_media"></a>Inserting Ads into your Media</span></span>
<span data-ttu-id="a3ca0-108">Azure Media Services 提供廣告插入 hello Windows 媒體平台的支援： 播放器架構。</span><span class="sxs-lookup"><span data-stu-id="a3ca0-108">Azure Media Services provides support for ad insertion through hello Windows Media Platform: Player Frameworks.</span></span> <span data-ttu-id="a3ca0-109">具備廣告支援的播放器架構都適用於 Windows 8、Silverlight、Windows Phone 8 和 iOS 裝置。</span><span class="sxs-lookup"><span data-stu-id="a3ca0-109">Player frameworks with ad support are available for Windows 8, Silverlight, Windows Phone 8, and iOS devices.</span></span> <span data-ttu-id="a3ca0-110">每個播放器架構包含範例程式碼，為您示範如何 tooimplement 播放器應用程式。有三種不同的媒體： 清單插入的廣告。</span><span class="sxs-lookup"><span data-stu-id="a3ca0-110">Each player framework contains sample code that shows you how tooimplement a player application.There are three different kinds of ads you can insert into your media:list.</span></span>

* <span data-ttu-id="a3ca0-111">**線性**– 完整框架廣告暫停 hello 主要影片。</span><span class="sxs-lookup"><span data-stu-id="a3ca0-111">**Linear** – full frame ads that pause hello main video.</span></span>
* <span data-ttu-id="a3ca0-112">**非線性**– hello 主要影片播放時顯示的重疊廣告，通常標誌或其他靜態影像用來放置 hello 播放程式內。</span><span class="sxs-lookup"><span data-stu-id="a3ca0-112">**Nonlinear** – overlay ads that are displayed as hello main video is playing, usually a logo or other static image placed within hello player.</span></span>
* <span data-ttu-id="a3ca0-113">**附屬**– 之外 hello 播放程式會顯示的廣告。</span><span class="sxs-lookup"><span data-stu-id="a3ca0-113">**Companion** – ads that are displayed outside of hello player.</span></span>

<span data-ttu-id="a3ca0-114">廣告可以放在任何時間點 hello 主要影片的時間線。</span><span class="sxs-lookup"><span data-stu-id="a3ca0-114">Ads can be placed at any point in hello main video’s time line.</span></span> <span data-ttu-id="a3ca0-115">您必須告知 hello player tooplay 當 hello ad，以及哪些廣告 tooplay。</span><span class="sxs-lookup"><span data-stu-id="a3ca0-115">You must tell hello player when tooplay hello ad and which ads tooplay.</span></span> <span data-ttu-id="a3ca0-116">使用一組標準的 XML 格式檔案即可搞定：Video Ad Service Template (VAST)、Digital Video Multiple Ad Playlist (VMAP)、Media Abstract Sequencing Template (MAST) 以及 Digital Video Player Ad Interface Definition (VPAID)。</span><span class="sxs-lookup"><span data-stu-id="a3ca0-116">This is done using a set of standard XML-based files: Video Ad Service Template (VAST), Digital Video Multiple Ad Playlist (VMAP), Media Abstract Sequencing Template (MAST), and Digital Video Player Ad Interface Definition (VPAID).</span></span> <span data-ttu-id="a3ca0-117">VAST 檔案會指定哪些廣告 toodisplay。</span><span class="sxs-lookup"><span data-stu-id="a3ca0-117">VAST files specify what ads toodisplay.</span></span> <span data-ttu-id="a3ca0-118">VMAP 檔案會指定何時 tooplay 各種廣告及包含 VAST XML。</span><span class="sxs-lookup"><span data-stu-id="a3ca0-118">VMAP files specify when tooplay various ads and contain VAST XML.</span></span> <span data-ttu-id="a3ca0-119">MAST 檔案是另一個方式 toosequence 廣告也可包含 VAST XML。</span><span class="sxs-lookup"><span data-stu-id="a3ca0-119">MAST files are another way toosequence ads which also can contain VAST XML.</span></span> <span data-ttu-id="a3ca0-120">VPAID 檔案會定義 hello 影片播放器與 hello 廣告或廣告伺服器之間的介面。</span><span class="sxs-lookup"><span data-stu-id="a3ca0-120">VPAID files define an interface between hello video player and hello ad or ad server.</span></span>

<span data-ttu-id="a3ca0-121">每個播放器架構的運作方式不同，而且分別涵蓋於各自的主題。</span><span class="sxs-lookup"><span data-stu-id="a3ca0-121">Each player framework works differently and each will be covered in its own topic.</span></span> <span data-ttu-id="a3ca0-122">本主題將說明 hello 所使用的基本機制 tooinsert 廣告。影片播放器應用程式會從廣告伺服器要求廣告。</span><span class="sxs-lookup"><span data-stu-id="a3ca0-122">This topic will describe hello basic mechanisms used tooinsert ads.Video player applications request ads from an ad server.</span></span> <span data-ttu-id="a3ca0-123">hello ad 伺服器可以回應在數種方式：</span><span class="sxs-lookup"><span data-stu-id="a3ca0-123">hello ad server can respond in a number of ways:</span></span>

* <span data-ttu-id="a3ca0-124">傳回 VAST 檔案</span><span class="sxs-lookup"><span data-stu-id="a3ca0-124">Return a VAST file</span></span>
* <span data-ttu-id="a3ca0-125">傳回 VMAP 檔案 (有內嵌 VAST)</span><span class="sxs-lookup"><span data-stu-id="a3ca0-125">Return a VMAP file (with embedded VAST)</span></span>
* <span data-ttu-id="a3ca0-126">傳回 MAST 檔案 (有內嵌 VAST)</span><span class="sxs-lookup"><span data-stu-id="a3ca0-126">Return a MAST file (with embedded VAST)</span></span>
* <span data-ttu-id="a3ca0-127">傳回 VAST 檔案 (有 VPAID 廣告)</span><span class="sxs-lookup"><span data-stu-id="a3ca0-127">Return a VAST file with VPAID ads</span></span>

### <a name="using-a-video-ad-service-template-vast-file"></a><span data-ttu-id="a3ca0-128">使用 Video Ad Service Template (VAST) 檔案</span><span class="sxs-lookup"><span data-stu-id="a3ca0-128">Using a Video Ad Service Template (VAST) File</span></span>
<span data-ttu-id="a3ca0-129">VAST 檔案會指定哪些廣告或廣告 toodisplay。</span><span class="sxs-lookup"><span data-stu-id="a3ca0-129">A VAST file specifies what ad or ads toodisplay.</span></span> <span data-ttu-id="a3ca0-130">hello 下列 XML 是線性廣告的 VAST 檔案範例：</span><span class="sxs-lookup"><span data-stu-id="a3ca0-130">hello following XML is an example of a VAST file for a linear ad:</span></span>

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

<span data-ttu-id="a3ca0-131">hello 線性廣告描述 hello <**線性**> 項目。</span><span class="sxs-lookup"><span data-stu-id="a3ca0-131">hello linear ad is described by hello <**Linear**> element.</span></span> <span data-ttu-id="a3ca0-132">它會指定 hello ad hello 持續時間、 追蹤事件、 點選連結、 點選追蹤和一些**MediaFile**項目。</span><span class="sxs-lookup"><span data-stu-id="a3ca0-132">It specifies hello duration of hello ad, tracking events, click through, click tracking, and a number of **MediaFile** elements.</span></span> <span data-ttu-id="a3ca0-133">指定追蹤事件在 hello <**TrackingEvents**> 項目，並允許廣告伺服器 tootrack 檢視 hello ad 時所發生的各種事件。</span><span class="sxs-lookup"><span data-stu-id="a3ca0-133">Tracking events are specified within hello <**TrackingEvents**> element and allow an ad server tootrack various events that occur while viewing hello ad.</span></span> <span data-ttu-id="a3ca0-134">在此情況下 hello 開始、 中點，完成，然後展開會在追蹤事件。</span><span class="sxs-lookup"><span data-stu-id="a3ca0-134">In this case hello start, midpoint, complete, and expand events are tracked.</span></span> <span data-ttu-id="a3ca0-135">顯示 hello ad 時，就會發生 hello 開始事件。</span><span class="sxs-lookup"><span data-stu-id="a3ca0-135">hello start event occurs when hello ad is displayed.</span></span> <span data-ttu-id="a3ca0-136">hello 中間點事件發生時至少已經檢視 50%的 hello 廣告時間軸。</span><span class="sxs-lookup"><span data-stu-id="a3ca0-136">hello midpoint event occurs when at least 50% of hello ad’s timeline has been viewed.</span></span> <span data-ttu-id="a3ca0-137">hello 廣告執行 toohello 結束時，就會發生 hello 完成事件。</span><span class="sxs-lookup"><span data-stu-id="a3ca0-137">hello complete event occurs when hello ad has run toohello end.</span></span> <span data-ttu-id="a3ca0-138">hello 展開事件發生於 hello 使用者展開視訊播放程式 toofull 囉 」 畫面。</span><span class="sxs-lookup"><span data-stu-id="a3ca0-138">hello Expand event occurs when hello user expands hello video player toofull screen.</span></span> <span data-ttu-id="a3ca0-139">點選連結所指定的 <**點選連結**> 內的項目 <**VideoClicks**> 項目，並指定 URI tooa 資源 toodisplay hello 使用者按一下 hello ad 上時。</span><span class="sxs-lookup"><span data-stu-id="a3ca0-139">Clickthroughs are specified with a <**ClickThrough**> element within a <**VideoClicks**> element and specifies a URI tooa resource toodisplay when hello user clicks on hello ad.</span></span> <span data-ttu-id="a3ca0-140">點選追蹤中指定 <**點選追蹤**> 項目，也在 hello <**VideoClicks**> 項目，並指定追蹤資源 hello player toorequest hello 使用者按一下時在 hello ad.hello <**MediaFile**> 項目會指定廣告以特定編碼方式的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="a3ca0-140">ClickTracking is specified in a <**ClickTracking**> element, also within hello <**VideoClicks**> element and specifies a tracking resource for hello player toorequest when hello user clicks on hello ad.hello <**MediaFile**> elements specify information about a specific encoding of an ad.</span></span> <span data-ttu-id="a3ca0-141">當有多個 <**MediaFile**> 項目，hello 視訊播放程式可以選擇 hello 最佳編碼方式 hello 平台。</span><span class="sxs-lookup"><span data-stu-id="a3ca0-141">When there is more than one <**MediaFile**> element, hello video player can choose hello best encoding for hello platform.</span></span> 

<span data-ttu-id="a3ca0-142">線性廣告可以依照指定的順序顯示。</span><span class="sxs-lookup"><span data-stu-id="a3ca0-142">Linear ads can be displayed in a specified order.</span></span> <span data-ttu-id="a3ca0-143">toodo，請加入更多<Ad>元素 toohello VAST 檔案，並指定 hello 順序使用 hello 順序屬性。</span><span class="sxs-lookup"><span data-stu-id="a3ca0-143">toodo this, add additional <Ad> elements toohello VAST file and specify hello order using hello sequence attribute.</span></span> <span data-ttu-id="a3ca0-144">hello 下列範例將說明這點：</span><span class="sxs-lookup"><span data-stu-id="a3ca0-144">hello following example illustrates this:</span></span>

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

<span data-ttu-id="a3ca0-145">非線性廣告也是在 <Creative> 元素中指定。</span><span class="sxs-lookup"><span data-stu-id="a3ca0-145">Nonlinear ads are specified in a <Creative> element as well.</span></span> <span data-ttu-id="a3ca0-146">下列範例所示的 hello<Creative>元素，可描述非線性廣告。</span><span class="sxs-lookup"><span data-stu-id="a3ca0-146">hello following example shows a <Creative> element that describes a nonlinear ad.</span></span>

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


<span data-ttu-id="a3ca0-147">hello <**NonLinearAds**> 項目可以包含一或多個 <**非線性**> 項目，其中每一個都可以描述非線性廣告。</span><span class="sxs-lookup"><span data-stu-id="a3ca0-147">hello <**NonLinearAds**> element can contain one or more <**NonLinear**> elements, each of which can describe a nonlinear ad.</span></span> <span data-ttu-id="a3ca0-148">hello <**非線性**> 項目會指定 hello hello 非線性廣告的資源。</span><span class="sxs-lookup"><span data-stu-id="a3ca0-148">hello <**NonLinear**> element specifies hello resource for hello nonlinear ad.</span></span> <span data-ttu-id="a3ca0-149">hello 資源可以是 <**StaticResouce**>、 <**IFrameResource**>，或 <**HTMLResouce**>。</span><span class="sxs-lookup"><span data-stu-id="a3ca0-149">hello resource can be a <**StaticResouce**>, an <**IFrameResource**>, or an <**HTMLResouce**>.</span></span><span data-ttu-id="a3ca0-150"> <**StaticResource**> 描述非 HTML 資源，並定義指定 hello 資源的顯示方式的 creativeType 屬性：</span><span class="sxs-lookup"><span data-stu-id="a3ca0-150"> <**StaticResource**> describes a non-HTML resource and defines a creativeType attribute that specifies how hello resource is displayed:</span></span>

<span data-ttu-id="a3ca0-151">Image/gif、 image/jpeg、 image/png – hello 資源會顯示在 HTML <**img**> 標記。</span><span class="sxs-lookup"><span data-stu-id="a3ca0-151">Image/gif, image/jpeg, image/png – hello resource is displayed in an HTML <**img**> tag.</span></span>

<span data-ttu-id="a3ca0-152">應用程式/x-javascript – hello 資源會顯示在 HTML <**指令碼**> 標記。</span><span class="sxs-lookup"><span data-stu-id="a3ca0-152">Application/x-javascript – hello resource is displayed in an HTML <**script**> tag.</span></span>

<span data-ttu-id="a3ca0-153">應用程式/x shockwave-快閃記憶體 – hello 資源會顯示在 Flash player。</span><span class="sxs-lookup"><span data-stu-id="a3ca0-153">Application/x-shockwave-flash – hello resource is displayed in a Flash player.</span></span>

<span data-ttu-id="a3ca0-154">**IFrameResource** 說明可在 IFrame 中顯示的 HTML 資源。</span><span class="sxs-lookup"><span data-stu-id="a3ca0-154">**IFrameResource** describes an HTML resource that can be displayed in an IFrame.</span></span> <span data-ttu-id="a3ca0-155">**HTMLResource** 說明可插入網頁的 HTML 程式碼片段。</span><span class="sxs-lookup"><span data-stu-id="a3ca0-155">**HTMLResource** describes a piece of HTML code that can be inserted into a web page.</span></span> <span data-ttu-id="a3ca0-156">**TrackingEvents**指定追蹤事件和 hello URI toorequest hello 事件發生時。</span><span class="sxs-lookup"><span data-stu-id="a3ca0-156">**TrackingEvents** specify tracking events and hello URI toorequest when hello event occurs.</span></span> <span data-ttu-id="a3ca0-157">在此範例 hello 會追蹤 acceptInvitation 和 collapse 事件。</span><span class="sxs-lookup"><span data-stu-id="a3ca0-157">In this sample hello acceptInvitation and collapse events are tracked.</span></span> <span data-ttu-id="a3ca0-158">如需有關 hello **NonLinearAds**元素和其子系，請參閱 IAB.NET/VAST。</span><span class="sxs-lookup"><span data-stu-id="a3ca0-158">For more information on hello **NonLinearAds** element and its children, see IAB.NET/VAST.</span></span> <span data-ttu-id="a3ca0-159">請注意該 hello **TrackingEvents**項目是位於 hello **NonLinearAds**項目，而不是 hello**非線性**項目。</span><span class="sxs-lookup"><span data-stu-id="a3ca0-159">Note that hello **TrackingEvents** element is located within hello **NonLinearAds** element rather than hello **NonLinear** element.</span></span>

<span data-ttu-id="a3ca0-160">隨播廣告會在 <CompanionAds> 元素內定義。</span><span class="sxs-lookup"><span data-stu-id="a3ca0-160">Companion ads are defined within a <CompanionAds> element.</span></span> <span data-ttu-id="a3ca0-161">hello<CompanionAds>項目可以包含一或多個<Companion>項目。</span><span class="sxs-lookup"><span data-stu-id="a3ca0-161">hello <CompanionAds> element can contain one or more <Companion> elements.</span></span> <span data-ttu-id="a3ca0-162">每個<Companion>項目描述隨播廣告，而且只能包含<StaticResource>， <IFrameResource>，或<HTMLResource>其指定在 hello 方式如所示的非線性廣告相同。</span><span class="sxs-lookup"><span data-stu-id="a3ca0-162">Each <Companion> element describes a companion ad and can contain a <StaticResource>, <IFrameResource>, or <HTMLResource> which are specified in hello same way as in a nonlinear ad.</span></span> <span data-ttu-id="a3ca0-163">VAST 檔案可以包含多個隨播廣告，而且 hello 播放器應用程式可以選擇最適合 ad toodisplay hello。</span><span class="sxs-lookup"><span data-stu-id="a3ca0-163">A VAST file can contain multiple companion ads and hello player application can choose hello most appropriate ad toodisplay.</span></span> <span data-ttu-id="a3ca0-164">如需 VAST 的詳細資訊，請參閱 [VAST 3.0](http://www.iab.net/media/file/VASTv3.0.pdf)。</span><span class="sxs-lookup"><span data-stu-id="a3ca0-164">For more information about VAST, see [VAST 3.0](http://www.iab.net/media/file/VASTv3.0.pdf).</span></span>

### <a name="using-a-digital-video-multiple-ad-playlist-vmap-file"></a><span data-ttu-id="a3ca0-165">使用 Digital Video Multiple Ad Playlist (VMAP) 檔案</span><span class="sxs-lookup"><span data-stu-id="a3ca0-165">Using a Digital Video Multiple Ad Playlist (VMAP) File</span></span>
<span data-ttu-id="a3ca0-166">VMAP 檔案可讓您 toospecify 時插播廣告、 每個中斷的時間、 內中斷，可以顯示多少廣告和廣告類型可能會中斷期間顯示。</span><span class="sxs-lookup"><span data-stu-id="a3ca0-166">A VMAP file allows you toospecify when ad breaks occur, how long each break is, how many ads can be displayed within a break, and what types of ads may be displayed during a break.</span></span> <span data-ttu-id="a3ca0-167">依照 VMAP 檔案範例會定義單一廣告插播的 hello:</span><span class="sxs-lookup"><span data-stu-id="a3ca0-167">hello following in an example VMAP file that defines a single ad break:</span></span>

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

<span data-ttu-id="a3ca0-168">VMAP 檔案開頭為 <VMAP> 元素，包含一或多個 <AdBreak> 元素，每個元素都會定義廣告插播。</span><span class="sxs-lookup"><span data-stu-id="a3ca0-168">A VMAP file begins with a <VMAP> element that contains one or more <AdBreak> elements, each defining an ad break.</span></span> <span data-ttu-id="a3ca0-169">每個廣告插播都會指定插播類型、插播 ID 和時間位移。</span><span class="sxs-lookup"><span data-stu-id="a3ca0-169">Each ad break specifies a break type, break ID, and time offset.</span></span> <span data-ttu-id="a3ca0-170">hello breakType 屬性指定 hello hello 插播期間可以播放的廣告類型： 線性、 非線性或顯示。</span><span class="sxs-lookup"><span data-stu-id="a3ca0-170">hello breakType attribute specifies hello type of ad that can be played during hello break: linear, nonlinear, or display.</span></span> <span data-ttu-id="a3ca0-171">顯示廣告對應 tooVAST 隨播廣告。</span><span class="sxs-lookup"><span data-stu-id="a3ca0-171">Display ads map tooVAST companion ads.</span></span> <span data-ttu-id="a3ca0-172">在逗號 (無空格) 分隔的清單中可以指定一個以上的廣告類型。</span><span class="sxs-lookup"><span data-stu-id="a3ca0-172">More than one ad type can be specified in a comma (no spaces) separated list.</span></span> <span data-ttu-id="a3ca0-173">hello breakID 是廣告 hello 的選擇性識別碼。</span><span class="sxs-lookup"><span data-stu-id="a3ca0-173">hello breakID is an optional identifier for hello ad.</span></span> <span data-ttu-id="a3ca0-174">hello timeOffset 會指定何時應該顯示 hello ad。</span><span class="sxs-lookup"><span data-stu-id="a3ca0-174">hello timeOffset specifies when hello ad should be displayed.</span></span> <span data-ttu-id="a3ca0-175">您可以在 hello 下列方式的其中一個指定：</span><span class="sxs-lookup"><span data-stu-id="a3ca0-175">It can be specified in one of hello following ways:</span></span>

1. <span data-ttu-id="a3ca0-176">時間 – hh: mm: 或 hh:mm:ss.mmm 的格式，其中.mmm 為毫秒。</span><span class="sxs-lookup"><span data-stu-id="a3ca0-176">Time – in hh:mm:ss or hh:mm:ss.mmm format where .mmm is milliseconds.</span></span> <span data-ttu-id="a3ca0-177">hello 這個屬性的值會指定從 hello 影片時間軸 toohello hello 廣告插播開頭 hello 開頭的 hello 時間。</span><span class="sxs-lookup"><span data-stu-id="a3ca0-177">hello value of this attribute specifies hello time from hello beginning of hello video timeline toohello beginning of hello ad break.</span></span>
2. <span data-ttu-id="a3ca0-178">百分比 – 以 n %格式，其中 n 是 hello 影片時間軸 tooplay hello 百分比之前播放 hello ad</span><span class="sxs-lookup"><span data-stu-id="a3ca0-178">Percentage – in n% format where n is hello percentage of hello video timeline tooplay before playing hello ad</span></span>
3. <span data-ttu-id="a3ca0-179">開始/結束 – 指定廣告應該在之前或之後顯示 hello 視訊顯示</span><span class="sxs-lookup"><span data-stu-id="a3ca0-179">Start/End – specifies that an ad should be displayed before or after hello video has been displayed</span></span>
4. <span data-ttu-id="a3ca0-180">位置 – 指定 hello 的廣告插播的順序，未知，例如即時串流的 hello 廣告插播的 hello 逾時。</span><span class="sxs-lookup"><span data-stu-id="a3ca0-180">Position – specifies hello order of ad breaks when hello timing of hello ad breaks is unknown, such as in live streaming.</span></span> <span data-ttu-id="a3ca0-181">指定的每個廣告插播的 hello 順序 hello #n 格式，其中 n 是 1 或更大的整數。</span><span class="sxs-lookup"><span data-stu-id="a3ca0-181">hello order of each ad break is specified in hello #n format where n is an integer 1 or greater.</span></span> <span data-ttu-id="a3ca0-182">1 表示應該播放廣告 hello 在 hello 第一個機會，2 表示 hello 應該播放廣告在 hello 第二個機會，依此類推。</span><span class="sxs-lookup"><span data-stu-id="a3ca0-182">1 signifies hello ad should be played at hello first opportunity, 2 signifies hello ad should be played at hello second opportunity and so on.</span></span>

<span data-ttu-id="a3ca0-183">在 hello <**AdBreak**> 有項目可以是其中一個 <**AdSource**> 項目。</span><span class="sxs-lookup"><span data-stu-id="a3ca0-183">Within hello <**AdBreak**> element there can be one <**AdSource**> element.</span></span> <span data-ttu-id="a3ca0-184">hello <**AdSource**> 項目包含下列屬性的 hello:</span><span class="sxs-lookup"><span data-stu-id="a3ca0-184">hello <**AdSource**> element contains hello following attributes:</span></span>

1. <span data-ttu-id="a3ca0-185">Id – 指定 hello 廣告來源的識別碼</span><span class="sxs-lookup"><span data-stu-id="a3ca0-185">Id – specifies an identifier for hello ad source</span></span>
2. <span data-ttu-id="a3ca0-186">allowMultipleAds – 指定在 hello 廣告插播期間是否可以顯示多個廣告的布林值</span><span class="sxs-lookup"><span data-stu-id="a3ca0-186">allowMultipleAds – a Boolean value that specifies whether multiple ads can be displayed during hello ad break</span></span>
3. <span data-ttu-id="a3ca0-187">followRedirects – 選擇性的布林值，指定是否 hello 影片播放器應該接受廣告回應內重新導向</span><span class="sxs-lookup"><span data-stu-id="a3ca0-187">followRedirects – an optional Boolean value that specifies if hello video player should honor redirects within an ad response</span></span>

<span data-ttu-id="a3ca0-188">hello <**AdSource**> 項目會提供 hello 播放程式內嵌廣告回應或參考 tooan 廣告回應。</span><span class="sxs-lookup"><span data-stu-id="a3ca0-188">hello <**AdSource**> element provides hello player an inline ad response or a reference tooan ad response.</span></span> <span data-ttu-id="a3ca0-189">它可以包含下列項目 hello 的其中一個：</span><span class="sxs-lookup"><span data-stu-id="a3ca0-189">It can contain one of hello following elements:</span></span>

* <span data-ttu-id="a3ca0-190"><VASTAdData>表示 VAST 廣告回應內嵌在 hello VMAP 檔案</span><span class="sxs-lookup"><span data-stu-id="a3ca0-190"><VASTAdData> indicates a VAST ad response is embedded within hello VMAP file</span></span>
* <span data-ttu-id="a3ca0-191"><AdTagURI> 從另一個系統參考廣告回應的 URI</span><span class="sxs-lookup"><span data-stu-id="a3ca0-191"><AdTagURI> a URI that references an ad response from another system</span></span>
* <span data-ttu-id="a3ca0-192"><CustomAdData> -表示非 VAST 回應的任意字串</span><span class="sxs-lookup"><span data-stu-id="a3ca0-192"><CustomAdData> -an arbitrary string that respresents a non-VAST response</span></span>

<span data-ttu-id="a3ca0-193">在這個範例中，內嵌廣告回應是以 <VASTAdData> 元素指定，該元素包含 VAST 廣告回應。</span><span class="sxs-lookup"><span data-stu-id="a3ca0-193">In this example an in-line ad response is specified with a <VASTAdData> element that contains a VAST ad response.</span></span> <span data-ttu-id="a3ca0-194">如需有關 hello 其他項目，請參閱[VMAP](http://www.iab.net/guidelines/508676/digitalvideo/vsuite/vmap)。</span><span class="sxs-lookup"><span data-stu-id="a3ca0-194">For more information about hello other elements, see [VMAP](http://www.iab.net/guidelines/508676/digitalvideo/vsuite/vmap).</span></span>

<span data-ttu-id="a3ca0-195">hello <**AdBreak**> 項目也可以包含一個 <**TrackingEvents**> 項目。</span><span class="sxs-lookup"><span data-stu-id="a3ca0-195">hello <**AdBreak**> element can also contain one <**TrackingEvents**> element.</span></span> <span data-ttu-id="a3ca0-196">hello <**TrackingEvents**> 元素可讓您 tootrack hello 開頭或結尾廣告插播或 hello 廣告插播期間是否發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="a3ca0-196">hello <**TrackingEvents**> element allows you tootrack hello start or end of an ad break or whether an error occurred during hello ad break.</span></span> <span data-ttu-id="a3ca0-197">hello <**TrackingEvents**> 元素包含一或多個 <**追蹤**> 項目，其中每個指定的追蹤事件和追蹤 URI。</span><span class="sxs-lookup"><span data-stu-id="a3ca0-197">hello <**TrackingEvents**> element contains one or more <**Tracking**> elements, each of which specifies a tracking event and a tracking URI.</span></span> <span data-ttu-id="a3ca0-198">hello 可能的追蹤事件如下：</span><span class="sxs-lookup"><span data-stu-id="a3ca0-198">hello possible tracking events are:</span></span>

1. <span data-ttu-id="a3ca0-199">breakStart – 追蹤廣告插播的 hello 開頭</span><span class="sxs-lookup"><span data-stu-id="a3ca0-199">breakStart – tracks hello beginning of an ad break</span></span>
2. <span data-ttu-id="a3ca0-200">breakEnd – 追蹤廣告插播的 hello 完成</span><span class="sxs-lookup"><span data-stu-id="a3ca0-200">breakEnd – track hello completion of an ad break</span></span>
3. <span data-ttu-id="a3ca0-201">error – 追蹤 hello 廣告插播期間發生錯誤</span><span class="sxs-lookup"><span data-stu-id="a3ca0-201">error – tracks an error that occurred during hello ad break</span></span>

<span data-ttu-id="a3ca0-202">hello 下列範例會示範指定追蹤事件的 VMAP 檔案</span><span class="sxs-lookup"><span data-stu-id="a3ca0-202">hello following example shows a VMAP file that specifies tracking events</span></span>

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

<span data-ttu-id="a3ca0-203">如需有關 hello <**TrackingEvents**> 元素和其子系，請參閱 http://iab.org/VMAP.pdf</span><span class="sxs-lookup"><span data-stu-id="a3ca0-203">For more information on hello <**TrackingEvents**> element and its children, see http://iab.org/VMAP.pdf</span></span>

### <a name="using-a-media-abstract-sequencing-template-mast-file"></a><span data-ttu-id="a3ca0-204">使用 Media Abstract Sequencing Template (MAST) 檔案</span><span class="sxs-lookup"><span data-stu-id="a3ca0-204">Using a Media Abstract Sequencing Template (MAST) File</span></span>
<span data-ttu-id="a3ca0-205">MAST 檔案可讓您定義何時顯示廣告的 toospecify 觸發程序。</span><span class="sxs-lookup"><span data-stu-id="a3ca0-205">A MAST file allows you toospecify triggers that define when an ad is displayed.</span></span> <span data-ttu-id="a3ca0-206">hello 以下是範例 MAST 檔案，其中包含觸發程序前廣告、 片中廣告和片尾廣告。</span><span class="sxs-lookup"><span data-stu-id="a3ca0-206">hello following is an example MAST file that contains triggers for a pre roll ad, a mid-roll ad, and a post-roll ad.</span></span>

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



<span data-ttu-id="a3ca0-207">MAST 檔案開頭為 **MAST** 元素，其中包含一個 **triggers** 元素。</span><span class="sxs-lookup"><span data-stu-id="a3ca0-207">A MAST file begins with a **MAST** element that contains one **triggers** element.</span></span> <span data-ttu-id="a3ca0-208">hello<triggers>元素包含一或多個**觸發程序**項目會定義何時應該播放廣告。</span><span class="sxs-lookup"><span data-stu-id="a3ca0-208">hello <triggers> element contains one or more **trigger** elements that define when an ad should be played.</span></span> 

<span data-ttu-id="a3ca0-209">hello**觸發程序**元素包含**startConditions**指定廣告應該在何時開始 tooplay 項目。</span><span class="sxs-lookup"><span data-stu-id="a3ca0-209">hello **trigger** element contains a **startConditions** element which specify when an ad should begin tooplay.</span></span> <span data-ttu-id="a3ca0-210">hello **startConditions**元素包含一或多個<condition>項目。</span><span class="sxs-lookup"><span data-stu-id="a3ca0-210">hello **startConditions** element contains one or more <condition> elements.</span></span> <span data-ttu-id="a3ca0-211">當每個<condition>評估的 tootrue 觸發程序，起始或撤銷根據 hello<condition>內含**startConditions**或**endConditions**項目分別。</span><span class="sxs-lookup"><span data-stu-id="a3ca0-211">When each <condition> evaluates tootrue a trigger is initiated or revoked depending upon whether hello <condition> is contained within a **startConditions** or **endConditions** element respectively.</span></span> <span data-ttu-id="a3ca0-212">當多個<condition>項目都存在，則會視為隱含 OR，評估 tootrue 任何條件會導致 hello 觸發程序 tooinitiate。</span><span class="sxs-lookup"><span data-stu-id="a3ca0-212">When multiple <condition> elements are present, they are treated as an implicit OR, any condition evaluating tootrue will cause hello trigger tooinitiate.</span></span> <span data-ttu-id="a3ca0-213"><condition> 元素可以為巢狀。</span><span class="sxs-lookup"><span data-stu-id="a3ca0-213"><condition> elements can be nested.</span></span> <span data-ttu-id="a3ca0-214">當子<condition>都有預設項目，則會視為隱含 AND，所有條件必須都評估為 hello 觸發程序 tooinitiate tootrue。</span><span class="sxs-lookup"><span data-stu-id="a3ca0-214">When child <condition> elements are preset, they are treated as an implicit AND, all conditions must evaluate tootrue for hello trigger tooinitiate.</span></span> <span data-ttu-id="a3ca0-215">hello<condition>元素包含下列屬性可定義 hello 條件 hello:</span><span class="sxs-lookup"><span data-stu-id="a3ca0-215">hello <condition> element contains hello following attributes that define hello condition:</span></span> 

1. <span data-ttu-id="a3ca0-216">**型別**– 指定條件、 事件或屬性的 hello 類型</span><span class="sxs-lookup"><span data-stu-id="a3ca0-216">**type** – specifies hello type of condition, event or property</span></span>
2. <span data-ttu-id="a3ca0-217">**名稱**– hello hello 屬性或事件 toobe 評估期間使用的名稱</span><span class="sxs-lookup"><span data-stu-id="a3ca0-217">**name** – hello name of hello property or event toobe used during evaluation</span></span>
3. <span data-ttu-id="a3ca0-218">**值**– hello 會針對評估屬性的值</span><span class="sxs-lookup"><span data-stu-id="a3ca0-218">**value** – hello value that a property will be evaluated against</span></span>
4. <span data-ttu-id="a3ca0-219">**運算子**– 評估期間 hello 作業 toouse: EQ （等於）、 NEQ （不等於）、 GTR (greater)、 GEQ （大於或等於）、 LT （小於）、 LEQ （小於或等於）、 MOD （模數）</span><span class="sxs-lookup"><span data-stu-id="a3ca0-219">**operator** – hello operation toouse during evaluation: EQ (equal), NEQ (not equal), GTR (greater), GEQ (greater or equal), LT (Less than), LEQ (less than or equal), MOD (modulo)</span></span>

<span data-ttu-id="a3ca0-220">**endConditions** 也會包含 <condition> 元素。</span><span class="sxs-lookup"><span data-stu-id="a3ca0-220">**endConditions** also contain <condition> elements.</span></span> <span data-ttu-id="a3ca0-221">當條件評估 tootrue hello 觸發程序是 reset.hello<trigger>項目也包含<sources>包含一或多個項目<source>項目。</span><span class="sxs-lookup"><span data-stu-id="a3ca0-221">When a condition evaluates tootrue hello trigger is reset.hello <trigger> element also contains a <sources> element that contains one or more <source> elements.</span></span> <span data-ttu-id="a3ca0-222">hello<source>元素會定義 hello URI toohello 廣告回應 hello 廣告回應的類型。</span><span class="sxs-lookup"><span data-stu-id="a3ca0-222">hello <source> elements define hello URI toohello ad response and hello type of ad response.</span></span> <span data-ttu-id="a3ca0-223">在這個範例 URI 會指定 tooa VAST 回應。</span><span class="sxs-lookup"><span data-stu-id="a3ca0-223">In this example a URI is given tooa VAST response.</span></span> 

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


### <a name="using-video-player-ad-interface-definition-vpaid"></a><span data-ttu-id="a3ca0-224">使用 Video Player-Ad Interface Definition (VPAID)</span><span class="sxs-lookup"><span data-stu-id="a3ca0-224">Using Video Player-Ad Interface Definition (VPAID)</span></span>
<span data-ttu-id="a3ca0-225">VPAID 是啟用可執行的廣告單元 toocommunicate 與視訊播放程式的 API。</span><span class="sxs-lookup"><span data-stu-id="a3ca0-225">VPAID is an API for enabling executable ad units toocommunicate with a video player.</span></span> <span data-ttu-id="a3ca0-226">如此可提供高度互動性與體驗。</span><span class="sxs-lookup"><span data-stu-id="a3ca0-226">This allows highly interactive ad experiences.</span></span> <span data-ttu-id="a3ca0-227">hello 廣告可以回應 hello 檢視器所採取的 tooactions 與 hello 使用者可以互動 hello ad。</span><span class="sxs-lookup"><span data-stu-id="a3ca0-227">hello user can interact with hello ad and hello ad can respond tooactions taken by hello viewer.</span></span> <span data-ttu-id="a3ca0-228">例如廣告可能會顯示按鈕，好讓 hello 使用者 tooview hello 廣告的加長版或更多的資訊。</span><span class="sxs-lookup"><span data-stu-id="a3ca0-228">For example an ad may display buttons that allow hello user tooview more information or a longer version of hello ad.</span></span> <span data-ttu-id="a3ca0-229">hello 視訊播放程式必須支援 VPAID API hello 和 hello 可執行的廣告必須實作 hello API。</span><span class="sxs-lookup"><span data-stu-id="a3ca0-229">hello video player must support hello VPAID API and hello executable ad must implement hello API.</span></span> <span data-ttu-id="a3ca0-230">當播放程式從廣告伺服器 hello 伺服器要求廣告回應可能會包含 VPAID 廣告的 VAST 回應。</span><span class="sxs-lookup"><span data-stu-id="a3ca0-230">When a player requests an ad from an ad server hello server may respond with a VAST response that contains a VPAID ad.</span></span>

<span data-ttu-id="a3ca0-231">必須在如 Adobe Flash™ 或可以在網頁瀏覽器中執行的 JavaScript 執行階段環境中執行的程式碼中建立可執行廣告。</span><span class="sxs-lookup"><span data-stu-id="a3ca0-231">An executable ad is created in code that must be executed in a runtime environment such as Adobe Flash™ or JavaScript that can be executed in a web browser.</span></span> <span data-ttu-id="a3ca0-232">Ad 伺服器會傳回包含 VPAID 廣告的 VAST 回應 hello hello hello 中 apiFramework 屬性的值<MediaFile>項目必須為"VPAID"。</span><span class="sxs-lookup"><span data-stu-id="a3ca0-232">When an ad server returns a VAST response containing a VPAID ad, hello value of hello apiFramework attribute in hello <MediaFile> element must be “VPAID”.</span></span> <span data-ttu-id="a3ca0-233">這個屬性會指定該 hello 包含 ad 是可執行的 VPAID 廣告。</span><span class="sxs-lookup"><span data-stu-id="a3ca0-233">This attribute specifies that hello contained ad is a VPAID executable ad.</span></span> <span data-ttu-id="a3ca0-234">hello type 屬性必須設定 hello toohello MIME 類型可執行檔，例如 「 應用程式/x shockwave-快閃記憶體"或"應用程式/x-javascript"。</span><span class="sxs-lookup"><span data-stu-id="a3ca0-234">hello type attribute must be set toohello MIME type of hello executable, such as “application/x-shockwave-flash” or “application/x-javascript”.</span></span> <span data-ttu-id="a3ca0-235">hello 下列 XML 程式碼片段示範 hello<MediaFile>包含可執行的 VPAID 廣告的 VAST 回應中的項目。</span><span class="sxs-lookup"><span data-stu-id="a3ca0-235">hello following XML snippet shows hello <MediaFile> element from a VAST response containing a VPAID executable ad.</span></span> 

    <MediaFiles>
       <MediaFile id="1" delivery="progressive" type=”application/x-shockwaveflash”
                  width=”640” height=”480” apiFramework=”VPAID”>
           <!-- CDATA wrapped URI tooexecutable ad -->
       </MediaFile>
    </MediaFiles>


<span data-ttu-id="a3ca0-236">可執行的廣告可以使用 hello 初始化<AdParameters>hello 內的項目<Linear>或<NonLinear>VAST 回應中的項目。</span><span class="sxs-lookup"><span data-stu-id="a3ca0-236">An executable ad can be initialized using hello <AdParameters> element within hello <Linear> or <NonLinear> elements in a VAST response.</span></span> <span data-ttu-id="a3ca0-237">如需有關 hello<AdParameters>項目，請參閱[VAST 3.0](http://www.iab.net/media/file/VASTv3.0.pdf)。</span><span class="sxs-lookup"><span data-stu-id="a3ca0-237">For more information on hello <AdParameters> element, see [VAST 3.0](http://www.iab.net/media/file/VASTv3.0.pdf).</span></span> <span data-ttu-id="a3ca0-238">如需 hello VPAID API 的詳細資訊，請參閱[VPAID 2.0](http://www.iab.net/media/file/VPAID_2.0_Final_04-10-2012.pdf)。</span><span class="sxs-lookup"><span data-stu-id="a3ca0-238">For more information about hello VPAID API, see [VPAID 2.0](http://www.iab.net/media/file/VPAID_2.0_Final_04-10-2012.pdf).</span></span>

## <a name="implementing-a-windows-or-windows-phone-8-player-with-ad-support"></a><span data-ttu-id="a3ca0-239">實作包含廣告支援的 Windows 或 Windows Phone 8 播放器</span><span class="sxs-lookup"><span data-stu-id="a3ca0-239">Implementing a Windows or Windows Phone 8 Player with Ad Support</span></span>
<span data-ttu-id="a3ca0-240">hello Microsoft 媒體平台： Player Framework for Windows 8 和 Windows Phone 8 包含範例應用程式可為您示範如何使用影片播放器應用程式的 tooimplement hello 架構的集合。</span><span class="sxs-lookup"><span data-stu-id="a3ca0-240">hello Microsoft Media Platform: Player Framework for Windows 8 and Windows Phone 8 contains a collection of sample applications that show you how tooimplement a video player application using hello framework.</span></span> <span data-ttu-id="a3ca0-241">您可以下載從 hello 播放器架構和 hello 範例[Player Framework for Windows 8 和 Windows Phone 8](https://playerframework.codeplex.com)。</span><span class="sxs-lookup"><span data-stu-id="a3ca0-241">You can download hello Player Framework and hello samples from [Player Framework for Windows 8 and Windows Phone 8](https://playerframework.codeplex.com).</span></span>

<span data-ttu-id="a3ca0-242">當您開啟 hello Microsoft.PlayerFramework.Xaml.Samples 方案時您會看到 hello 專案中資料夾的數目。</span><span class="sxs-lookup"><span data-stu-id="a3ca0-242">When you open hello Microsoft.PlayerFramework.Xaml.Samples solution you will see a number of folders within hello project.</span></span> <span data-ttu-id="a3ca0-243">hello Advertising 資料夾包含 hello 範例程式碼相關 toocreating 包含廣告支援的視訊播放程式。</span><span class="sxs-lookup"><span data-stu-id="a3ca0-243">hello Advertising folder contains hello sample code relevant toocreating a video player with ad support.</span></span> <span data-ttu-id="a3ca0-244">內部 hello Advertising 資料夾是 XAML/cs 檔案數目每哪一個節目如何以不同方式 tooinsert 廣告。</span><span class="sxs-lookup"><span data-stu-id="a3ca0-244">Inside hello Advertising folder is a number of XAML/cs files each of which show how tooinsert ads in a different way.</span></span> <span data-ttu-id="a3ca0-245">hello 下列清單描述每個：</span><span class="sxs-lookup"><span data-stu-id="a3ca0-245">hello following list describes each:</span></span>

* <span data-ttu-id="a3ca0-246">AdPodPage.xaml 顯示如何 toodisplay ad pod。</span><span class="sxs-lookup"><span data-stu-id="a3ca0-246">AdPodPage.xaml Shows how toodisplay an ad pod.</span></span>
* <span data-ttu-id="a3ca0-247">AdSchedulingPage.xaml 顯示如何 tooschedule 廣告。</span><span class="sxs-lookup"><span data-stu-id="a3ca0-247">AdSchedulingPage.xaml Shows how tooschedule ads.</span></span>
* <span data-ttu-id="a3ca0-248">FreeWheelPage.xaml 顯示 toouse hello FreeWheel 外掛程式 tooschedule 廣告的方式。</span><span class="sxs-lookup"><span data-stu-id="a3ca0-248">FreeWheelPage.xaml Shows how toouse hello FreeWheel plugin tooschedule ads.</span></span>
* <span data-ttu-id="a3ca0-249">MastPage.xaml 顯示如何使用 MAST 檔案 tooschedule 廣告。</span><span class="sxs-lookup"><span data-stu-id="a3ca0-249">MastPage.xaml Shows how tooschedule ads with a MAST file.</span></span>
* <span data-ttu-id="a3ca0-250">ProgrammaticAdPage.xaml 顯示如何 tooprogrammatically 在影片中排程廣告。</span><span class="sxs-lookup"><span data-stu-id="a3ca0-250">ProgrammaticAdPage.xaml Shows how tooprogrammatically schedule ads into a video.</span></span>
* <span data-ttu-id="a3ca0-251">ScheduleClipPage.xaml 顯示如何 tooschedule ad 不使用 VAST 檔案。</span><span class="sxs-lookup"><span data-stu-id="a3ca0-251">ScheduleClipPage.xaml Shows how tooschedule an ad without a VAST file.</span></span>
* <span data-ttu-id="a3ca0-252">VastLinearCompanionPage.xaml 顯示如何 tooinsert 線性和隨播廣告。</span><span class="sxs-lookup"><span data-stu-id="a3ca0-252">VastLinearCompanionPage.xaml Shows how tooinsert a linear and companion ad.</span></span>
* <span data-ttu-id="a3ca0-253">VastNonLinearPage.xaml 顯示如何 tooinsert 非線性廣告。</span><span class="sxs-lookup"><span data-stu-id="a3ca0-253">VastNonLinearPage.xaml Shows how tooinsert a non-linear ad.</span></span>
* <span data-ttu-id="a3ca0-254">VmapPage.xaml 顯示如何使用 VMAP 檔案 toospecify 廣告。</span><span class="sxs-lookup"><span data-stu-id="a3ca0-254">VmapPage.xaml Shows how toospecify ads with a VMAP file.</span></span>

<span data-ttu-id="a3ca0-255">每個範例會使用 hello 播放器架構所定義的 hello MediaPlayer 類別。</span><span class="sxs-lookup"><span data-stu-id="a3ca0-255">Each of these samples uses hello MediaPlayer class defined by hello player framework.</span></span> <span data-ttu-id="a3ca0-256">大部分的範例會使用加入各種廣告回應格式支援的外掛程式。</span><span class="sxs-lookup"><span data-stu-id="a3ca0-256">Most samples use plugins that add support for various ad response formats.</span></span> <span data-ttu-id="a3ca0-257">hello ProgrammaticAdPage 範例以程式設計方式互動的 MediaPlayer 例項。</span><span class="sxs-lookup"><span data-stu-id="a3ca0-257">hello ProgrammaticAdPage sample programmatically interacts with a MediaPlayer instance.</span></span>

### <a name="adpodpage-sample"></a><span data-ttu-id="a3ca0-258">AdPodPage 範例</span><span class="sxs-lookup"><span data-stu-id="a3ca0-258">AdPodPage Sample</span></span>
<span data-ttu-id="a3ca0-259">這個範例會使用 hello AdSchedulerPlugin toodefine 時 toodisplay 廣告。</span><span class="sxs-lookup"><span data-stu-id="a3ca0-259">This sample uses hello AdSchedulerPlugin toodefine when toodisplay an ad.</span></span> <span data-ttu-id="a3ca0-260">在此範例中，片中廣告是排程的 toobe 5 秒鐘之後播放。</span><span class="sxs-lookup"><span data-stu-id="a3ca0-260">In this example a mid-roll advertisement is scheduled toobe played after 5 seconds.</span></span> <span data-ttu-id="a3ca0-261">從廣告伺服器傳回的 VAST 檔案中指定 hello ad pod （廣告 toodisplay 順序群組）。</span><span class="sxs-lookup"><span data-stu-id="a3ca0-261">hello ad pod (a group of ads toodisplay in order) is specified in a VAST file returned from an ad server.</span></span> <span data-ttu-id="a3ca0-262">hello URI toohello VAST 檔案會指定在 hello<RemoteAdSource>項目。</span><span class="sxs-lookup"><span data-stu-id="a3ca0-262">hello URI toohello VAST file is specified in hello <RemoteAdSource> element.</span></span>

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

<span data-ttu-id="a3ca0-263">如需 hello AdSchedulerPlugin 的詳細資訊，請參閱[hello Windows 8 和 Windows Phone 8 播放器架構中進行通告](http://playerframework.codeplex.com/wikipage?title=Advertising&referringTitle=Windows%208%20Player%20Documentation)</span><span class="sxs-lookup"><span data-stu-id="a3ca0-263">For more information about hello AdSchedulerPlugin, see [Advertising in hello Player Framework on Windows 8 and Windows Phone 8](http://playerframework.codeplex.com/wikipage?title=Advertising&referringTitle=Windows%208%20Player%20Documentation)</span></span>

### <a name="adschedulingpage"></a><span data-ttu-id="a3ca0-264">AdSchedulingPage</span><span class="sxs-lookup"><span data-stu-id="a3ca0-264">AdSchedulingPage</span></span>
<span data-ttu-id="a3ca0-265">此範例也會使用 hello AdSchedulerPlugin。</span><span class="sxs-lookup"><span data-stu-id="a3ca0-265">This sample also uses hello AdSchedulerPlugin.</span></span> <span data-ttu-id="a3ca0-266">它會排程三個廣告，片頭廣告、片中廣告和片尾廣告。</span><span class="sxs-lookup"><span data-stu-id="a3ca0-266">It schedules three ads, a pre-roll ad, a mid-roll ad, and a post-roll ad.</span></span> <span data-ttu-id="a3ca0-267">每個 ad 指定的 hello URI toohello VAST<RemoteAdSource>項目。</span><span class="sxs-lookup"><span data-stu-id="a3ca0-267">hello URI toohello VAST for each ad is specified in a <RemoteAdSource> element.</span></span>

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


### <a name="freewheelpage"></a><span data-ttu-id="a3ca0-268">FreeWheelPage</span><span class="sxs-lookup"><span data-stu-id="a3ca0-268">FreeWheelPage</span></span>
<span data-ttu-id="a3ca0-269">這個範例會使用 hello FreeWheelPlugin 指定指定的 URI 指定廣告內容以及廣告排程資訊該點 tooa SmartXML 檔案的來源屬性。</span><span class="sxs-lookup"><span data-stu-id="a3ca0-269">This sample uses hello FreeWheelPlugin which specifies a Source attribute that specifies a URI that points tooa SmartXML file that specifies ad content as well as ad scheduling information.</span></span>

    <mmppf:MediaPlayer x:Name="player" Source="http://smf.blob.core.windows.net/samples/videos/bigbuck.mp4">
                <mmppf:MediaPlayer.Plugins>
                    <ads:FreeWheelPlugin Source="http://smf.blob.core.windows.net/samples/win8/ads/freewheel.xml"/>
                    <ads:AdHandlerPlugin/>
                </mmppf:MediaPlayer.Plugins>
            </mmppf:MediaPlayer>

### <a name="mastpage"></a><span data-ttu-id="a3ca0-270">MastPage</span><span class="sxs-lookup"><span data-stu-id="a3ca0-270">MastPage</span></span>
<span data-ttu-id="a3ca0-271">這個範例會使用 hello MastSchedulerPlugin，可讓您 toouse MAST 檔案。</span><span class="sxs-lookup"><span data-stu-id="a3ca0-271">This sample uses hello MastSchedulerPlugin that allows you toouse a MAST file.</span></span> <span data-ttu-id="a3ca0-272">hello Source 屬性會指定 hello hello MAST 檔案位置。</span><span class="sxs-lookup"><span data-stu-id="a3ca0-272">hello Source attribute specifies hello location of hello MAST file.</span></span>

    <mmppf:MediaPlayer x:Name="player" Source="http://smf.blob.core.windows.net/samples/videos/bigbuck.mp4">
                <mmppf:MediaPlayer.Plugins>
                    <ads:MastSchedulerPlugin Source="http://smf.blob.core.windows.net/samples/win8/ads/mast.xml" />
                    <ads:AdHandlerPlugin/>
                </mmppf:MediaPlayer.Plugins>
            </mmppf:MediaPlayer>

### <a name="programmaticadpage"></a><span data-ttu-id="a3ca0-273">ProgrammaticAdPage</span><span class="sxs-lookup"><span data-stu-id="a3ca0-273">ProgrammaticAdPage</span></span>
<span data-ttu-id="a3ca0-274">此範例以程式設計的方式會與 hello MediaPlayer 互動。</span><span class="sxs-lookup"><span data-stu-id="a3ca0-274">This sample programmatically interacts with hello MediaPlayer.</span></span> <span data-ttu-id="a3ca0-275">hello ProgrammaticAdPage.xaml 檔案會具現化 hello MediaPlayer:</span><span class="sxs-lookup"><span data-stu-id="a3ca0-275">hello ProgrammaticAdPage.xaml file instantiates hello MediaPlayer:</span></span>

    <mmppf:MediaPlayer x:Name="player" Source="http://smf.blob.core.windows.net/samples/videos/bigbuck.mp4"/>

<span data-ttu-id="a3ca0-276">hello ProgrammaticAdPage.xaml.cs 檔案會建立 AdHandlerPlugin、 廣告應該顯示，並將其載入 RemoteAdSource 指定 URI tooa VAST 檔案，並再播放 hello MarkerReached 事件的處理常式時，加入 TimelineMarker toospecifyhello ad。</span><span class="sxs-lookup"><span data-stu-id="a3ca0-276">hello ProgrammaticAdPage.xaml.cs file creates an AdHandlerPlugin, adds a TimelineMarker toospecify when an ad should be displayed, and then adds a handler for hello MarkerReached event which loads a RemoteAdSource specifying a URI tooa VAST file, and then plays hello ad.</span></span>

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

### <a name="scheduleclippage"></a><span data-ttu-id="a3ca0-277">ScheduleClipPage</span><span class="sxs-lookup"><span data-stu-id="a3ca0-277">ScheduleClipPage</span></span>
<span data-ttu-id="a3ca0-278">這個範例會指定包含 hello 廣告的.wmv 檔案來使用 hello AdSchedulerPlugin tooschedule 片中廣告。</span><span class="sxs-lookup"><span data-stu-id="a3ca0-278">This sample uses hello AdSchedulerPlugin tooschedule a mid-roll ad by specifying a .wmv file that contains hello ad.</span></span>

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

### <a name="vastlinearcompanionpage"></a><span data-ttu-id="a3ca0-279">VastLinearCompanionPage</span><span class="sxs-lookup"><span data-stu-id="a3ca0-279">VastLinearCompanionPage</span></span>
<span data-ttu-id="a3ca0-280">此範例說明如何 toouse 會 hello AdSchedulerPlugin tooschedule 片中的線性廣告與隨播廣告。</span><span class="sxs-lookup"><span data-stu-id="a3ca0-280">This sample illustrates how toouse hello AdSchedulerPlugin tooschedule a mid-roll linear ad with an companion ad.</span></span> <span data-ttu-id="a3ca0-281">hello<RemoteAdSource>項目會指定 hello hello VAST 檔案位置。</span><span class="sxs-lookup"><span data-stu-id="a3ca0-281">hello <RemoteAdSource> element specifies hello location of hello VAST file.</span></span>

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

### <a name="vastlinearnonlinearpage"></a><span data-ttu-id="a3ca0-282">VastLinearNonLinearPage</span><span class="sxs-lookup"><span data-stu-id="a3ca0-282">VastLinearNonLinearPage</span></span>
<span data-ttu-id="a3ca0-283">這個範例會使用 hello AdSchedulerPlugin tooschedule 線性與非線性廣告。</span><span class="sxs-lookup"><span data-stu-id="a3ca0-283">This sample uses hello AdSchedulerPlugin tooschedule a linear and a non-linear ad.</span></span> <span data-ttu-id="a3ca0-284">hello VAST 檔案位置指定 hello<RemoteAdSource>項目。</span><span class="sxs-lookup"><span data-stu-id="a3ca0-284">hello VAST file location is specified with hello <RemoteAdSource> element.</span></span>

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

### <a name="vmappage"></a><span data-ttu-id="a3ca0-285">VMAPPage</span><span class="sxs-lookup"><span data-stu-id="a3ca0-285">VMAPPage</span></span>
<span data-ttu-id="a3ca0-286">此範例使用使用 VMAP 檔案 hello VmapSchedulerPlugin tooschedule 廣告。</span><span class="sxs-lookup"><span data-stu-id="a3ca0-286">This samples uses hello VmapSchedulerPlugin tooschedule ads using a VMAP file.</span></span> <span data-ttu-id="a3ca0-287">hello hello Source 屬性中指定 hello URI toohello VMAP 檔案<VmapSchedulerPlugin>項目。</span><span class="sxs-lookup"><span data-stu-id="a3ca0-287">hello URI toohello VMAP file is specified in hello Source attribute of hello <VmapSchedulerPlugin> element.</span></span>

    <mmppf:MediaPlayer x:Name="player" Source="http://smf.blob.core.windows.net/samples/videos/bigbuck.mp4">
                <mmppf:MediaPlayer.Plugins>
                    <ads:VmapSchedulerPlugin Source="http://smf.blob.core.windows.net/samples/win8/ads/vmap.xml"/>
                    <ads:AdHandlerPlugin/>
                </mmppf:MediaPlayer.Plugins>
            </mmppf:MediaPlayer>

## <a name="implementing-an-ios-video-player-with-ad-support"></a><span data-ttu-id="a3ca0-288">實作具有廣告支援的 iOS 視訊播放器</span><span class="sxs-lookup"><span data-stu-id="a3ca0-288">Implementing an iOS Video Player with Ad Support</span></span>
<span data-ttu-id="a3ca0-289">hello Microsoft 媒體平台： 適用於 iOS 的播放器架構包含範例應用程式可為您示範如何使用影片播放器應用程式的 tooimplement hello 架構的集合。</span><span class="sxs-lookup"><span data-stu-id="a3ca0-289">hello Microsoft Media Platform: Player Framework for iOS contains a collection of sample applications that show you how tooimplement a video player application using hello framework.</span></span> <span data-ttu-id="a3ca0-290">您可以下載從 hello 播放器架構和 hello 範例[Azure Media Player Framework](https://github.com/Azure/azure-media-player-framework)。</span><span class="sxs-lookup"><span data-stu-id="a3ca0-290">You can download hello Player Framework and hello samples from [Azure Media Player Framework](https://github.com/Azure/azure-media-player-framework).</span></span> <span data-ttu-id="a3ca0-291">hello github 頁面有 Wiki，包含上 hello 播放器架構和簡介 toohello 播放器範例的其他資訊的連結 tooa: [Azure 媒體播放器 Wiki](https://github.com/Azure/azure-media-player-framework/wiki/How-to-use-Azure-media-player-framework)。</span><span class="sxs-lookup"><span data-stu-id="a3ca0-291">hello github page has a link tooa Wiki that contains additional information on hello player framework and an introduction toohello player sample: [Azure Media Player Wiki](https://github.com/Azure/azure-media-player-framework/wiki/How-to-use-Azure-media-player-framework).</span></span>

### <a name="scheduling-ads-with-vmap"></a><span data-ttu-id="a3ca0-292">使用 VMAP 排程廣告</span><span class="sxs-lookup"><span data-stu-id="a3ca0-292">Scheduling Ads with VMAP</span></span>
<span data-ttu-id="a3ca0-293">hello 下列範例會示範如何使用 VMAP 檔案 tooschedule 廣告。</span><span class="sxs-lookup"><span data-stu-id="a3ca0-293">hello following example shows how tooschedule ads using a VMAP file.</span></span>

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

### <a name="scheduling-ads-with-vast"></a><span data-ttu-id="a3ca0-294">使用 VAST 排程廣告</span><span class="sxs-lookup"><span data-stu-id="a3ca0-294">Scheduling Ads with VAST</span></span>
<span data-ttu-id="a3ca0-295">hello 以下範例將示範如何 tooschedule 晚期繫結的 VAST 廣告。</span><span class="sxs-lookup"><span data-stu-id="a3ca0-295">hello following sample shows how tooschedule a late binding VAST ad.</span></span>

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

   <span data-ttu-id="a3ca0-296">hello 以下範例將示範如何 tooschedule 早期繫結的 VAST 廣告。</span><span class="sxs-lookup"><span data-stu-id="a3ca0-296">hello following sample shows how tooschedule an early binding VAST ad.</span></span>
<span data-ttu-id="a3ca0-297">早期繫結 VAST 廣告 //Download hello VAST 檔案範例： 4 排程 (！ [framework.adResolver downloadManifest： 資訊清單和 withURL: [NSURL URLWithString: @"http://portalvhdsq3m25bf47d15c.blob.core.windows.net/vast/PlayerTestVAST.xml"]]) {[自我 logFrameworkError];} else {adLinearTime.startTime = 7。adLinearTime.duration = 0;</span><span class="sxs-lookup"><span data-stu-id="a3ca0-297">//Example:4 Schedule an early binding VAST ad //Download hello VAST file if (![framework.adResolver downloadManifest:&manifest withURL:[NSURL URLWithString:@"http://portalvhdsq3m25bf47d15c.blob.core.windows.net/vast/PlayerTestVAST.xml"]]) { [self logFrameworkError]; } else { adLinearTime.startTime = 7; adLinearTime.duration = 0;</span></span>

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

<span data-ttu-id="a3ca0-298">hello 以下範例將示範如何 tooinsert ad 使用粗略剪下編輯 (R)</span><span class="sxs-lookup"><span data-stu-id="a3ca0-298">hello following sample shows how tooinsert an ad using Rough Cut Editing (RCE)</span></span>

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

<span data-ttu-id="a3ca0-299">hello 下列範例顯示如何 tooschedule ad pod。</span><span class="sxs-lookup"><span data-stu-id="a3ca0-299">hello following example shows how tooschedule an ad pod.</span></span>

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

<span data-ttu-id="a3ca0-300">下列範例會示範如何 hello tooschedule 非重複性片中廣告。</span><span class="sxs-lookup"><span data-stu-id="a3ca0-300">hello following example shows how tooschedule a non-sticky mid-roll ad.</span></span> <span data-ttu-id="a3ca0-301">不論任何搜尋 hello 檢視器會執行之後，非重複性廣告只會播放。</span><span class="sxs-lookup"><span data-stu-id="a3ca0-301">A non-sticky ad is only played once regardless of any seeking hello viewer performs.</span></span>

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

<span data-ttu-id="a3ca0-302">下列範例會示範如何 hello tooschedule 重複性片中廣告。</span><span class="sxs-lookup"><span data-stu-id="a3ca0-302">hello following example shows how tooschedule a sticky mid-roll ad.</span></span> <span data-ttu-id="a3ca0-303">重複性廣告會顯示 hello 指定 hello 影片時間軸上的點已達到每個時間。</span><span class="sxs-lookup"><span data-stu-id="a3ca0-303">A sticky ad will be displayed each time hello specified point on hello video timeline is reached.</span></span>

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


<span data-ttu-id="a3ca0-304">hello 以下範例將示範如何 tooschedule 片尾廣告。</span><span class="sxs-lookup"><span data-stu-id="a3ca0-304">hello following sample shows how tooschedule a post-roll ad.</span></span>

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

<span data-ttu-id="a3ca0-305">hello 以下範例將示範如何 tooschedule 前廣告。</span><span class="sxs-lookup"><span data-stu-id="a3ca0-305">hello following sample shows how tooschedule a pre-roll ad.</span></span>

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

<span data-ttu-id="a3ca0-306">hello 下列範例顯示如何 tooschedule 中間彙重疊廣告。</span><span class="sxs-lookup"><span data-stu-id="a3ca0-306">hello following sample shows how tooschedule a mid-roll overlay ad.</span></span>

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



## <a name="media-services-learning-paths"></a><span data-ttu-id="a3ca0-307">媒體服務學習路徑</span><span class="sxs-lookup"><span data-stu-id="a3ca0-307">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="a3ca0-308">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="a3ca0-308">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="a3ca0-309">另請參閱</span><span class="sxs-lookup"><span data-stu-id="a3ca0-309">See Also</span></span>
[<span data-ttu-id="a3ca0-310">開發視訊播放程式應用程式</span><span class="sxs-lookup"><span data-stu-id="a3ca0-310">Develop video player applications</span></span>](media-services-develop-video-players.md)

