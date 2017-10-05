---
title: "在用戶端插入廣告 | Microsoft Docs"
description: "本主題說明如何在用戶端上插入廣告。"
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
ms.openlocfilehash: 52ba731f88c630830560e3cf8406ba2e9613c8a5
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="inserting-ads-on-the-client-side"></a><span data-ttu-id="c4eb8-103">在用戶端插入廣告</span><span class="sxs-lookup"><span data-stu-id="c4eb8-103">Inserting ads on the client side</span></span>
<span data-ttu-id="c4eb8-104">本主題包含如何在用戶端上插入各種類型廣告的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="c4eb8-104">This topic contains information on how to insert various types of ads on the client side.</span></span>

<span data-ttu-id="c4eb8-105">如需了解即時串流視訊的隱藏式字幕和廣告支援，請參閱 [隱藏式字幕支援和廣告插入標準](media-services-live-streaming-with-onprem-encoders.md#cc_and_ads)。</span><span class="sxs-lookup"><span data-stu-id="c4eb8-105">For information about closed captioning and ad support in Live streaming videos, see [Supported Closed Captioning and Ad Insertion Standards](media-services-live-streaming-with-onprem-encoders.md#cc_and_ads).</span></span>

> [!NOTE]
> <span data-ttu-id="c4eb8-106">Azure 媒體播放器目前不支援廣告。</span><span class="sxs-lookup"><span data-stu-id="c4eb8-106">Azure Media Player does not currently support Ads.</span></span>
> 
> 

## <span data-ttu-id="c4eb8-107"><a id="insert_ads_into_media"></a>將廣告插入您的媒體</span><span class="sxs-lookup"><span data-stu-id="c4eb8-107"><a id="insert_ads_into_media"></a>Inserting Ads into your Media</span></span>
<span data-ttu-id="c4eb8-108">Azure 媒體服務允許透過 Windows Media 平台插入廣告：Player Framework。</span><span class="sxs-lookup"><span data-stu-id="c4eb8-108">Azure Media Services provides support for ad insertion through the Windows Media Platform: Player Frameworks.</span></span> <span data-ttu-id="c4eb8-109">具備廣告支援的播放器架構都適用於 Windows 8、Silverlight、Windows Phone 8 和 iOS 裝置。</span><span class="sxs-lookup"><span data-stu-id="c4eb8-109">Player frameworks with ad support are available for Windows 8, Silverlight, Windows Phone 8, and iOS devices.</span></span> <span data-ttu-id="c4eb8-110">每一個播放器架構都有範例程式碼，教您如何實作播放器應用程式。目前有三種不同的廣告可以插入 media:list 中：</span><span class="sxs-lookup"><span data-stu-id="c4eb8-110">Each player framework contains sample code that shows you how to implement a player application.There are three different kinds of ads you can insert into your media:list.</span></span>

* <span data-ttu-id="c4eb8-111">**線性** – 可暫停主要影片的完整框架廣告。</span><span class="sxs-lookup"><span data-stu-id="c4eb8-111">**Linear** – full frame ads that pause the main video.</span></span>
* <span data-ttu-id="c4eb8-112">**非線性** – 播放被當做主要影片而顯示的疊加廣告，通常是播放器中的標誌或其他靜態影像。</span><span class="sxs-lookup"><span data-stu-id="c4eb8-112">**Nonlinear** – overlay ads that are displayed as the main video is playing, usually a logo or other static image placed within the player.</span></span>
* <span data-ttu-id="c4eb8-113">**隨播** – 顯示在播放器之外的廣告。</span><span class="sxs-lookup"><span data-stu-id="c4eb8-113">**Companion** – ads that are displayed outside of the player.</span></span>

<span data-ttu-id="c4eb8-114">廣告可以放在主要影片時間軸的任何時間點。</span><span class="sxs-lookup"><span data-stu-id="c4eb8-114">Ads can be placed at any point in the main video’s time line.</span></span> <span data-ttu-id="c4eb8-115">您必須告訴播放器何時播放廣告以及要播放哪些廣告。</span><span class="sxs-lookup"><span data-stu-id="c4eb8-115">You must tell the player when to play the ad and which ads to play.</span></span> <span data-ttu-id="c4eb8-116">使用一組標準的 XML 格式檔案即可搞定：Video Ad Service Template (VAST)、Digital Video Multiple Ad Playlist (VMAP)、Media Abstract Sequencing Template (MAST) 以及 Digital Video Player Ad Interface Definition (VPAID)。</span><span class="sxs-lookup"><span data-stu-id="c4eb8-116">This is done using a set of standard XML-based files: Video Ad Service Template (VAST), Digital Video Multiple Ad Playlist (VMAP), Media Abstract Sequencing Template (MAST), and Digital Video Player Ad Interface Definition (VPAID).</span></span> <span data-ttu-id="c4eb8-117">VAST 檔案會指定要顯示的廣告。</span><span class="sxs-lookup"><span data-stu-id="c4eb8-117">VAST files specify what ads to display.</span></span> <span data-ttu-id="c4eb8-118">VMAP 檔案會指定何時播放各種廣告而且包含 VAST XML。</span><span class="sxs-lookup"><span data-stu-id="c4eb8-118">VMAP files specify when to play various ads and contain VAST XML.</span></span> <span data-ttu-id="c4eb8-119">MAST 檔案是另一種廣告排序的方法，而且也包含 VAST XML。</span><span class="sxs-lookup"><span data-stu-id="c4eb8-119">MAST files are another way to sequence ads which also can contain VAST XML.</span></span> <span data-ttu-id="c4eb8-120">VPAID 檔案會定義影片播放器廣告和廣告或廣告伺服器之間的介面。</span><span class="sxs-lookup"><span data-stu-id="c4eb8-120">VPAID files define an interface between the video player and the ad or ad server.</span></span>

<span data-ttu-id="c4eb8-121">每個播放器架構的運作方式不同，而且分別涵蓋於各自的主題。</span><span class="sxs-lookup"><span data-stu-id="c4eb8-121">Each player framework works differently and each will be covered in its own topic.</span></span> <span data-ttu-id="c4eb8-122">本主題將說明用來插入廣告的基本機制。視訊播放器應用程式會從廣告伺服器要求廣告。</span><span class="sxs-lookup"><span data-stu-id="c4eb8-122">This topic will describe the basic mechanisms used to insert ads.Video player applications request ads from an ad server.</span></span> <span data-ttu-id="c4eb8-123">廣告伺服器可以使用數種方法回應：</span><span class="sxs-lookup"><span data-stu-id="c4eb8-123">The ad server can respond in a number of ways:</span></span>

* <span data-ttu-id="c4eb8-124">傳回 VAST 檔案</span><span class="sxs-lookup"><span data-stu-id="c4eb8-124">Return a VAST file</span></span>
* <span data-ttu-id="c4eb8-125">傳回 VMAP 檔案 (有內嵌 VAST)</span><span class="sxs-lookup"><span data-stu-id="c4eb8-125">Return a VMAP file (with embedded VAST)</span></span>
* <span data-ttu-id="c4eb8-126">傳回 MAST 檔案 (有內嵌 VAST)</span><span class="sxs-lookup"><span data-stu-id="c4eb8-126">Return a MAST file (with embedded VAST)</span></span>
* <span data-ttu-id="c4eb8-127">傳回 VAST 檔案 (有 VPAID 廣告)</span><span class="sxs-lookup"><span data-stu-id="c4eb8-127">Return a VAST file with VPAID ads</span></span>

### <a name="using-a-video-ad-service-template-vast-file"></a><span data-ttu-id="c4eb8-128">使用 Video Ad Service Template (VAST) 檔案</span><span class="sxs-lookup"><span data-stu-id="c4eb8-128">Using a Video Ad Service Template (VAST) File</span></span>
<span data-ttu-id="c4eb8-129">VAST 檔案會指定要顯示的廣告。</span><span class="sxs-lookup"><span data-stu-id="c4eb8-129">A VAST file specifies what ad or ads to display.</span></span> <span data-ttu-id="c4eb8-130">下列 XML 是線性廣告的 VAST 檔案範例：</span><span class="sxs-lookup"><span data-stu-id="c4eb8-130">The following XML is an example of a VAST file for a linear ad:</span></span>

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

<span data-ttu-id="c4eb8-131">線性廣告是利用 <**Linear**> 元素來說明。</span><span class="sxs-lookup"><span data-stu-id="c4eb8-131">The linear ad is described by the <**Linear**> element.</span></span> <span data-ttu-id="c4eb8-132">它會指定廣告的持續時間、追蹤事件、點選連結、點選追蹤，以及許多 **MediaFile** 元素。</span><span class="sxs-lookup"><span data-stu-id="c4eb8-132">It specifies the duration of the ad, tracking events, click through, click tracking, and a number of **MediaFile** elements.</span></span> <span data-ttu-id="c4eb8-133">追蹤事件是在 <**TrackingEvents**> 元素中指定，並允許廣告伺服器追蹤在檢視廣告時所發生的各種事件。</span><span class="sxs-lookup"><span data-stu-id="c4eb8-133">Tracking events are specified within the <**TrackingEvents**> element and allow an ad server to track various events that occur while viewing the ad.</span></span> <span data-ttu-id="c4eb8-134">在此案例中會追蹤開始、中間點、完成及展開事件。</span><span class="sxs-lookup"><span data-stu-id="c4eb8-134">In this case the start, midpoint, complete, and expand events are tracked.</span></span> <span data-ttu-id="c4eb8-135">當顯示廣告時，就會發生開始事件。</span><span class="sxs-lookup"><span data-stu-id="c4eb8-135">The start event occurs when the ad is displayed.</span></span> <span data-ttu-id="c4eb8-136">當至少已經檢視 50% 的廣告時間軸時，就會發生中間點事件。</span><span class="sxs-lookup"><span data-stu-id="c4eb8-136">The midpoint event occurs when at least 50% of the ad’s timeline has been viewed.</span></span> <span data-ttu-id="c4eb8-137">當廣告播放到結尾時，就會發生完成事件。</span><span class="sxs-lookup"><span data-stu-id="c4eb8-137">The complete event occurs when the ad has run to the end.</span></span> <span data-ttu-id="c4eb8-138">當使用者將視訊播放器展開至全螢幕時，就會發生展開事件。</span><span class="sxs-lookup"><span data-stu-id="c4eb8-138">The Expand event occurs when the user expands the video player to full screen.</span></span> <span data-ttu-id="c4eb8-139">點選連結是以 <**VideoClicks**> 元素內的 <**ClickThrough**> 元素指定，並指定當使用者按一下廣告時要顯示資源的 URI。</span><span class="sxs-lookup"><span data-stu-id="c4eb8-139">Clickthroughs are specified with a <**ClickThrough**> element within a <**VideoClicks**> element and specifies a URI to a resource to display when the user clicks on the ad.</span></span> <span data-ttu-id="c4eb8-140">點選追蹤是在 <**ClickTracking**> 元素 (同樣位於 <**VideoClicks**> 元素內) 中指定，並指定在使用者按一下廣告時播放器要求的追蹤資源。<**MediaFile**> 元素會指定廣告特定編碼的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="c4eb8-140">ClickTracking is specified in a <**ClickTracking**> element, also within the <**VideoClicks**> element and specifies a tracking resource for the player to request when the user clicks on the ad.The <**MediaFile**> elements specify information about a specific encoding of an ad.</span></span> <span data-ttu-id="c4eb8-141">若有一個以上的 <**MediaFile**> 元素，視訊播放器就可以選擇最適合平台的編碼。</span><span class="sxs-lookup"><span data-stu-id="c4eb8-141">When there is more than one <**MediaFile**> element, the video player can choose the best encoding for the platform.</span></span> 

<span data-ttu-id="c4eb8-142">線性廣告可以依照指定的順序顯示。</span><span class="sxs-lookup"><span data-stu-id="c4eb8-142">Linear ads can be displayed in a specified order.</span></span> <span data-ttu-id="c4eb8-143">若要這樣做，請將其他 <Ad> 元素加入至 VAST 檔案，並使用順序屬性指定順序。</span><span class="sxs-lookup"><span data-stu-id="c4eb8-143">To do this, add additional <Ad> elements to the VAST file and specify the order using the sequence attribute.</span></span> <span data-ttu-id="c4eb8-144">下列範例會加以說明：</span><span class="sxs-lookup"><span data-stu-id="c4eb8-144">The following example illustrates this:</span></span>

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

<span data-ttu-id="c4eb8-145">非線性廣告也是在 <Creative> 元素中指定。</span><span class="sxs-lookup"><span data-stu-id="c4eb8-145">Nonlinear ads are specified in a <Creative> element as well.</span></span> <span data-ttu-id="c4eb8-146">下列範例顯示 <Creative> 元素，該元素會說明非線性廣告。</span><span class="sxs-lookup"><span data-stu-id="c4eb8-146">The following example shows a <Creative> element that describes a nonlinear ad.</span></span>

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


<span data-ttu-id="c4eb8-147"><**NonLinearAds**> 元素可以包含一或多個 <**NonLinear**> 元素，其中每一個元素都可說明一個非線性廣告。</span><span class="sxs-lookup"><span data-stu-id="c4eb8-147">The <**NonLinearAds**> element can contain one or more <**NonLinear**> elements, each of which can describe a nonlinear ad.</span></span> <span data-ttu-id="c4eb8-148"><**NonLinear**> 元素會指定非線性廣告的資源。</span><span class="sxs-lookup"><span data-stu-id="c4eb8-148">The <**NonLinear**> element specifies the resource for the nonlinear ad.</span></span> <span data-ttu-id="c4eb8-149">資源可以是 <**StaticResouce**>、<**IFrameResource**> 或 <**HTMLResouce**>。</span><span class="sxs-lookup"><span data-stu-id="c4eb8-149">The resource can be a <**StaticResouce**>, an <**IFrameResource**>, or an <**HTMLResouce**>.</span></span><span data-ttu-id="c4eb8-150"> <**StaticResource**> 說明非 HTML 資源，並且定義 creativeType 屬性，該屬性會指定資源的顯示方式：</span><span class="sxs-lookup"><span data-stu-id="c4eb8-150"> <**StaticResource**> describes a non-HTML resource and defines a creativeType attribute that specifies how the resource is displayed:</span></span>

<span data-ttu-id="c4eb8-151">image/gif、image/jpeg、image/png – 資源在 HTML <**img**> 標記中顯示。</span><span class="sxs-lookup"><span data-stu-id="c4eb8-151">Image/gif, image/jpeg, image/png – the resource is displayed in an HTML <**img**> tag.</span></span>

<span data-ttu-id="c4eb8-152">Application/x-javascript – 資源在 HTML <**script**> 標籤中顯示。</span><span class="sxs-lookup"><span data-stu-id="c4eb8-152">Application/x-javascript – the resource is displayed in an HTML <**script**> tag.</span></span>

<span data-ttu-id="c4eb8-153">Application/x-shockwave-flash – 資源在 Flash Player 中顯示。</span><span class="sxs-lookup"><span data-stu-id="c4eb8-153">Application/x-shockwave-flash – the resource is displayed in a Flash player.</span></span>

<span data-ttu-id="c4eb8-154">**IFrameResource** 說明可在 IFrame 中顯示的 HTML 資源。</span><span class="sxs-lookup"><span data-stu-id="c4eb8-154">**IFrameResource** describes an HTML resource that can be displayed in an IFrame.</span></span> <span data-ttu-id="c4eb8-155">**HTMLResource** 說明可插入網頁的 HTML 程式碼片段。</span><span class="sxs-lookup"><span data-stu-id="c4eb8-155">**HTMLResource** describes a piece of HTML code that can be inserted into a web page.</span></span> <span data-ttu-id="c4eb8-156">**TrackingEvents** 指定追蹤事件以及當發生事件時要求的 URI。</span><span class="sxs-lookup"><span data-stu-id="c4eb8-156">**TrackingEvents** specify tracking events and the URI to request when the event occurs.</span></span> <span data-ttu-id="c4eb8-157">在此範例中，會追蹤 acceptInvitation 和 collapse 事件。</span><span class="sxs-lookup"><span data-stu-id="c4eb8-157">In this sample the acceptInvitation and collapse events are tracked.</span></span> <span data-ttu-id="c4eb8-158">如需有關 **NonLinearAds** 元素和其子系的詳細資訊，請參閱 IAB.NET/VAST。</span><span class="sxs-lookup"><span data-stu-id="c4eb8-158">For more information on the **NonLinearAds** element and its children, see IAB.NET/VAST.</span></span> <span data-ttu-id="c4eb8-159">請注意，**TrackingEvents** 元素位於 **NonLinearAds** 元素內，而不是 **NonLinear** 元素中。</span><span class="sxs-lookup"><span data-stu-id="c4eb8-159">Note that the **TrackingEvents** element is located within the **NonLinearAds** element rather than the **NonLinear** element.</span></span>

<span data-ttu-id="c4eb8-160">隨播廣告會在 <CompanionAds> 元素內定義。</span><span class="sxs-lookup"><span data-stu-id="c4eb8-160">Companion ads are defined within a <CompanionAds> element.</span></span> <span data-ttu-id="c4eb8-161"><CompanionAds> 元素可以包含一或多個 <Companion> 元素。</span><span class="sxs-lookup"><span data-stu-id="c4eb8-161">The <CompanionAds> element can contain one or more <Companion> elements.</span></span> <span data-ttu-id="c4eb8-162">每個 <Companion> 元素都會說明隨播廣告，而且可以包含 <StaticResource>、<IFrameResource> 或 <HTMLResource>，其指定方式與非線性廣告相同。</span><span class="sxs-lookup"><span data-stu-id="c4eb8-162">Each <Companion> element describes a companion ad and can contain a <StaticResource>, <IFrameResource>, or <HTMLResource> which are specified in the same way as in a nonlinear ad.</span></span> <span data-ttu-id="c4eb8-163">VAST 檔案可以包含多個隨播廣告，而且播放器應用程式可以選擇要顯示的最適當廣告。</span><span class="sxs-lookup"><span data-stu-id="c4eb8-163">A VAST file can contain multiple companion ads and the player application can choose the most appropriate ad to display.</span></span> <span data-ttu-id="c4eb8-164">如需 VAST 的詳細資訊，請參閱 [VAST 3.0](http://www.iab.net/media/file/VASTv3.0.pdf)。</span><span class="sxs-lookup"><span data-stu-id="c4eb8-164">For more information about VAST, see [VAST 3.0](http://www.iab.net/media/file/VASTv3.0.pdf).</span></span>

### <a name="using-a-digital-video-multiple-ad-playlist-vmap-file"></a><span data-ttu-id="c4eb8-165">使用 Digital Video Multiple Ad Playlist (VMAP) 檔案</span><span class="sxs-lookup"><span data-stu-id="c4eb8-165">Using a Digital Video Multiple Ad Playlist (VMAP) File</span></span>
<span data-ttu-id="c4eb8-166">VMAP 檔案可讓您指定何時插播廣告、每個插播多久、插播中可以顯示多少廣告，以及插播期間可以顯示哪些類型的廣告。</span><span class="sxs-lookup"><span data-stu-id="c4eb8-166">A VMAP file allows you to specify when ad breaks occur, how long each break is, how many ads can be displayed within a break, and what types of ads may be displayed during a break.</span></span> <span data-ttu-id="c4eb8-167">範例 VMAP 檔案中的下列項目會定義單一廣告插播：</span><span class="sxs-lookup"><span data-stu-id="c4eb8-167">The following in an example VMAP file that defines a single ad break:</span></span>

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

<span data-ttu-id="c4eb8-168">VMAP 檔案開頭為 <VMAP> 元素，包含一或多個 <AdBreak> 元素，每個元素都會定義廣告插播。</span><span class="sxs-lookup"><span data-stu-id="c4eb8-168">A VMAP file begins with a <VMAP> element that contains one or more <AdBreak> elements, each defining an ad break.</span></span> <span data-ttu-id="c4eb8-169">每個廣告插播都會指定插播類型、插播 ID 和時間位移。</span><span class="sxs-lookup"><span data-stu-id="c4eb8-169">Each ad break specifies a break type, break ID, and time offset.</span></span> <span data-ttu-id="c4eb8-170">breakType 屬性會指定插播期間可以播放的廣告類型：線性、非線性或顯示。</span><span class="sxs-lookup"><span data-stu-id="c4eb8-170">The breakType attribute specifies the type of ad that can be played during the break: linear, nonlinear, or display.</span></span> <span data-ttu-id="c4eb8-171">顯示廣告會對應到 VAST 隨播廣告。</span><span class="sxs-lookup"><span data-stu-id="c4eb8-171">Display ads map to VAST companion ads.</span></span> <span data-ttu-id="c4eb8-172">在逗號 (無空格) 分隔的清單中可以指定一個以上的廣告類型。</span><span class="sxs-lookup"><span data-stu-id="c4eb8-172">More than one ad type can be specified in a comma (no spaces) separated list.</span></span> <span data-ttu-id="c4eb8-173">breakID 是廣告的選擇性識別碼。</span><span class="sxs-lookup"><span data-stu-id="c4eb8-173">The breakID is an optional identifier for the ad.</span></span> <span data-ttu-id="c4eb8-174">timeOffset 會指定何時應該顯示廣告。</span><span class="sxs-lookup"><span data-stu-id="c4eb8-174">The timeOffset specifies when the ad should be displayed.</span></span> <span data-ttu-id="c4eb8-175">可以利用下列方式之一來指定：</span><span class="sxs-lookup"><span data-stu-id="c4eb8-175">It can be specified in one of the following ways:</span></span>

1. <span data-ttu-id="c4eb8-176">時間 – hh: mm: 或 hh:mm:ss.mmm 的格式，其中.mmm 為毫秒。</span><span class="sxs-lookup"><span data-stu-id="c4eb8-176">Time – in hh:mm:ss or hh:mm:ss.mmm format where .mmm is milliseconds.</span></span> <span data-ttu-id="c4eb8-177">這個屬性的值會指定從視訊時間軸開始到廣告插播開始的時間。</span><span class="sxs-lookup"><span data-stu-id="c4eb8-177">The value of this attribute specifies the time from the beginning of the video timeline to the beginning of the ad break.</span></span>
2. <span data-ttu-id="c4eb8-178">百分比 – n% 格式，其中 n 是視訊時間軸在播放廣告之前播放的百分比</span><span class="sxs-lookup"><span data-stu-id="c4eb8-178">Percentage – in n% format where n is the percentage of the video timeline to play before playing the ad</span></span>
3. <span data-ttu-id="c4eb8-179">開始/結束 – 指定廣告應該在視訊顯示之前或之後顯示</span><span class="sxs-lookup"><span data-stu-id="c4eb8-179">Start/End – specifies that an ad should be displayed before or after the video has been displayed</span></span>
4. <span data-ttu-id="c4eb8-180">位置 – 指定當廣告插播的時機為未知時 (例如即時串流)，廣告插播的順序。</span><span class="sxs-lookup"><span data-stu-id="c4eb8-180">Position – specifies the order of ad breaks when the timing of the ad breaks is unknown, such as in live streaming.</span></span> <span data-ttu-id="c4eb8-181">每個廣告插播的順序是以 #n 格式指定，其中 n 是大於或等於 1 的整數。</span><span class="sxs-lookup"><span data-stu-id="c4eb8-181">The order of each ad break is specified in the #n format where n is an integer 1 or greater.</span></span> <span data-ttu-id="c4eb8-182">1 表示廣告應該在第一個機會時播放，2 表示廣告應該在第二個機會時播放，依此類推。</span><span class="sxs-lookup"><span data-stu-id="c4eb8-182">1 signifies the ad should be played at the first opportunity, 2 signifies the ad should be played at the second opportunity and so on.</span></span>

<span data-ttu-id="c4eb8-183">在 <**AdBreak**> 元素內可以有一個 <**AdSource**> 元素。</span><span class="sxs-lookup"><span data-stu-id="c4eb8-183">Within the <**AdBreak**> element there can be one <**AdSource**> element.</span></span> <span data-ttu-id="c4eb8-184"><**AdSource**> 元素包含下列屬性：</span><span class="sxs-lookup"><span data-stu-id="c4eb8-184">The <**AdSource**> element contains the following attributes:</span></span>

1. <span data-ttu-id="c4eb8-185">Id – 指定廣告來源的識別碼</span><span class="sxs-lookup"><span data-stu-id="c4eb8-185">Id – specifies an identifier for the ad source</span></span>
2. <span data-ttu-id="c4eb8-186">allowMultipleAds – 布林值，指定在廣告插播期間是否可以顯示多個廣告</span><span class="sxs-lookup"><span data-stu-id="c4eb8-186">allowMultipleAds – a Boolean value that specifies whether multiple ads can be displayed during the ad break</span></span>
3. <span data-ttu-id="c4eb8-187">followRedirects – 選用布林值，指定視訊播放器是否應該接受廣告回應內的重新導向</span><span class="sxs-lookup"><span data-stu-id="c4eb8-187">followRedirects – an optional Boolean value that specifies if the video player should honor redirects within an ad response</span></span>

<span data-ttu-id="c4eb8-188"><**AdSource**> 元素會提供播放器內嵌廣告回應或廣告回應的參考。</span><span class="sxs-lookup"><span data-stu-id="c4eb8-188">The <**AdSource**> element provides the player an inline ad response or a reference to an ad response.</span></span> <span data-ttu-id="c4eb8-189">可以包含下列其中一個元素：</span><span class="sxs-lookup"><span data-stu-id="c4eb8-189">It can contain one of the following elements:</span></span>

* <span data-ttu-id="c4eb8-190"><VASTAdData> 表示 VAST 廣告回應內嵌在 VMAP 檔案</span><span class="sxs-lookup"><span data-stu-id="c4eb8-190"><VASTAdData> indicates a VAST ad response is embedded within the VMAP file</span></span>
* <span data-ttu-id="c4eb8-191"><AdTagURI> 從另一個系統參考廣告回應的 URI</span><span class="sxs-lookup"><span data-stu-id="c4eb8-191"><AdTagURI> a URI that references an ad response from another system</span></span>
* <span data-ttu-id="c4eb8-192"><CustomAdData> -表示非 VAST 回應的任意字串</span><span class="sxs-lookup"><span data-stu-id="c4eb8-192"><CustomAdData> -an arbitrary string that respresents a non-VAST response</span></span>

<span data-ttu-id="c4eb8-193">在這個範例中，內嵌廣告回應是以 <VASTAdData> 元素指定，該元素包含 VAST 廣告回應。</span><span class="sxs-lookup"><span data-stu-id="c4eb8-193">In this example an in-line ad response is specified with a <VASTAdData> element that contains a VAST ad response.</span></span> <span data-ttu-id="c4eb8-194">如需其他元素的詳細資訊，請參閱 [VMAP](http://www.iab.net/guidelines/508676/digitalvideo/vsuite/vmap)。</span><span class="sxs-lookup"><span data-stu-id="c4eb8-194">For more information about the other elements, see [VMAP](http://www.iab.net/guidelines/508676/digitalvideo/vsuite/vmap).</span></span>

<span data-ttu-id="c4eb8-195"><**AdBreak**> 元素也可以包含一個 <**TrackingEvents**> 元素。</span><span class="sxs-lookup"><span data-stu-id="c4eb8-195">The <**AdBreak**> element can also contain one <**TrackingEvents**> element.</span></span> <span data-ttu-id="c4eb8-196"><**TrackingEvents**> 元素可讓您追蹤廣告插播的開頭或結束，或廣告插播期間是否發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="c4eb8-196">The <**TrackingEvents**> element allows you to track the start or end of an ad break or whether an error occurred during the ad break.</span></span> <span data-ttu-id="c4eb8-197"><**TrackingEvents**> 元素包含一或多個 <**Tracking**> 元素，每個元素會指定追蹤事件和追蹤 URI。</span><span class="sxs-lookup"><span data-stu-id="c4eb8-197">The <**TrackingEvents**> element contains one or more <**Tracking**> elements, each of which specifies a tracking event and a tracking URI.</span></span> <span data-ttu-id="c4eb8-198">可能的追蹤事件如下：</span><span class="sxs-lookup"><span data-stu-id="c4eb8-198">The possible tracking events are:</span></span>

1. <span data-ttu-id="c4eb8-199">breakStart – 追蹤廣告插播的開始</span><span class="sxs-lookup"><span data-stu-id="c4eb8-199">breakStart – tracks the beginning of an ad break</span></span>
2. <span data-ttu-id="c4eb8-200">breakEnd – 追蹤廣告插播的完成</span><span class="sxs-lookup"><span data-stu-id="c4eb8-200">breakEnd – track the completion of an ad break</span></span>
3. <span data-ttu-id="c4eb8-201">error – 追蹤廣告插播期間發生的錯誤</span><span class="sxs-lookup"><span data-stu-id="c4eb8-201">error – tracks an error that occurred during the ad break</span></span>

<span data-ttu-id="c4eb8-202">下列範例顯示會指定追蹤事件的 VMAP 檔案</span><span class="sxs-lookup"><span data-stu-id="c4eb8-202">The following example shows a VMAP file that specifies tracking events</span></span>

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

<span data-ttu-id="c4eb8-203">如需 <**TrackingEvents**> 元素及其子系的詳細資訊，請參閱 http://iab.org/VMAP.pdf</span><span class="sxs-lookup"><span data-stu-id="c4eb8-203">For more information on the <**TrackingEvents**> element and its children, see http://iab.org/VMAP.pdf</span></span>

### <a name="using-a-media-abstract-sequencing-template-mast-file"></a><span data-ttu-id="c4eb8-204">使用 Media Abstract Sequencing Template (MAST) 檔案</span><span class="sxs-lookup"><span data-stu-id="c4eb8-204">Using a Media Abstract Sequencing Template (MAST) File</span></span>
<span data-ttu-id="c4eb8-205">MAST 檔案可讓您指定觸發程序，定義何時顯示廣告。</span><span class="sxs-lookup"><span data-stu-id="c4eb8-205">A MAST file allows you to specify triggers that define when an ad is displayed.</span></span> <span data-ttu-id="c4eb8-206">以下是範例 MAST 檔案，其中包含片頭廣告、片中廣告和片尾廣告的觸發程序。</span><span class="sxs-lookup"><span data-stu-id="c4eb8-206">The following is an example MAST file that contains triggers for a pre roll ad, a mid-roll ad, and a post-roll ad.</span></span>

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
            <!--This 'resets' the trigger for the next clip-->
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



<span data-ttu-id="c4eb8-207">MAST 檔案開頭為 **MAST** 元素，其中包含一個 **triggers** 元素。</span><span class="sxs-lookup"><span data-stu-id="c4eb8-207">A MAST file begins with a **MAST** element that contains one **triggers** element.</span></span> <span data-ttu-id="c4eb8-208"><triggers> 元素包含一或多個 **trigger** 元素，定義何時應該播放廣告。</span><span class="sxs-lookup"><span data-stu-id="c4eb8-208">The <triggers> element contains one or more **trigger** elements that define when an ad should be played.</span></span> 

<span data-ttu-id="c4eb8-209">**trigger** 元素包含 **startConditions** 元素，定義何時應該開始播放廣告。</span><span class="sxs-lookup"><span data-stu-id="c4eb8-209">The **trigger** element contains a **startConditions** element which specify when an ad should begin to play.</span></span> <span data-ttu-id="c4eb8-210">**startConditions** 元素包含一或多個 <condition> 元素。</span><span class="sxs-lookup"><span data-stu-id="c4eb8-210">The **startConditions** element contains one or more <condition> elements.</span></span> <span data-ttu-id="c4eb8-211">當每個 <condition> 評估為 true 時，會起始或撤銷觸發程序，取決於 <condition> 是分別內含於 **startConditions** 或 **endConditions** 元素。</span><span class="sxs-lookup"><span data-stu-id="c4eb8-211">When each <condition> evaluates to true a trigger is initiated or revoked depending upon whether the <condition> is contained within a **startConditions** or **endConditions** element respectively.</span></span> <span data-ttu-id="c4eb8-212">當多個 <condition> 元素都存在時，則會視為隱含 OR，任何評估為 true 的條件都會導致起始觸發程序。</span><span class="sxs-lookup"><span data-stu-id="c4eb8-212">When multiple <condition> elements are present, they are treated as an implicit OR, any condition evaluating to true will cause the trigger to initiate.</span></span> <span data-ttu-id="c4eb8-213"><condition> 元素可以為巢狀。</span><span class="sxs-lookup"><span data-stu-id="c4eb8-213"><condition> elements can be nested.</span></span> <span data-ttu-id="c4eb8-214">當預設子系 <condition> 元素時，它們會被視為隱含 AND，所有條件必須評估為 true，才會起始觸發程序。</span><span class="sxs-lookup"><span data-stu-id="c4eb8-214">When child <condition> elements are preset, they are treated as an implicit AND, all conditions must evaluate to true for the trigger to initiate.</span></span> <span data-ttu-id="c4eb8-215"><condition> 元素包含會定義條件的下列屬性：</span><span class="sxs-lookup"><span data-stu-id="c4eb8-215">The <condition> element contains the following attributes that define the condition:</span></span> 

1. <span data-ttu-id="c4eb8-216">**type** – 指定條件、事件或屬性的類型</span><span class="sxs-lookup"><span data-stu-id="c4eb8-216">**type** – specifies the type of condition, event or property</span></span>
2. <span data-ttu-id="c4eb8-217">**name** – 要在評估期間使用之屬性或事件的名稱</span><span class="sxs-lookup"><span data-stu-id="c4eb8-217">**name** – the name of the property or event to be used during evaluation</span></span>
3. <span data-ttu-id="c4eb8-218">**value** – 屬性將會針對其進行評估的值</span><span class="sxs-lookup"><span data-stu-id="c4eb8-218">**value** – the value that a property will be evaluated against</span></span>
4. <span data-ttu-id="c4eb8-219">**operator** – 要在評估期間使用的運算：EQ (等於)、NEQ (不等於)、GTR (大於)、GEQ (大於或等於)、LT (小於)、LEQ (小於或等於)、MOD (模數)</span><span class="sxs-lookup"><span data-stu-id="c4eb8-219">**operator** – the operation to use during evaluation: EQ (equal), NEQ (not equal), GTR (greater), GEQ (greater or equal), LT (Less than), LEQ (less than or equal), MOD (modulo)</span></span>

<span data-ttu-id="c4eb8-220">**endConditions** 也會包含 <condition> 元素。</span><span class="sxs-lookup"><span data-stu-id="c4eb8-220">**endConditions** also contain <condition> elements.</span></span> <span data-ttu-id="c4eb8-221">當條件評估為 true 時，會重設觸發程序。<trigger> 元素也包含 <sources> 元素，該元素包含一或多個 <source> 元素。</span><span class="sxs-lookup"><span data-stu-id="c4eb8-221">When a condition evaluates to true the trigger is reset.The <trigger> element also contains a <sources> element that contains one or more <source> elements.</span></span> <span data-ttu-id="c4eb8-222"><source> 元素定義廣告回應的 URI 與廣告回應的類型。</span><span class="sxs-lookup"><span data-stu-id="c4eb8-222">The <source> elements define the URI to the ad response and the type of ad response.</span></span> <span data-ttu-id="c4eb8-223">在此範例中，會對 VAST 回應指定 URI。</span><span class="sxs-lookup"><span data-stu-id="c4eb8-223">In this example a URI is given to a VAST response.</span></span> 

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


### <a name="using-video-player-ad-interface-definition-vpaid"></a><span data-ttu-id="c4eb8-224">使用 Video Player-Ad Interface Definition (VPAID)</span><span class="sxs-lookup"><span data-stu-id="c4eb8-224">Using Video Player-Ad Interface Definition (VPAID)</span></span>
<span data-ttu-id="c4eb8-225">VPAID 是 API，用於啟用可執行廣告單元，以便與視訊播放器通訊。</span><span class="sxs-lookup"><span data-stu-id="c4eb8-225">VPAID is an API for enabling executable ad units to communicate with a video player.</span></span> <span data-ttu-id="c4eb8-226">如此可提供高度互動性與體驗。</span><span class="sxs-lookup"><span data-stu-id="c4eb8-226">This allows highly interactive ad experiences.</span></span> <span data-ttu-id="c4eb8-227">使用者可以與廣告互動，而且廣告可以回應檢視者採取的動作。</span><span class="sxs-lookup"><span data-stu-id="c4eb8-227">The user can interact with the ad and the ad can respond to actions taken by the viewer.</span></span> <span data-ttu-id="c4eb8-228">例如，廣告可能會顯示按鈕，讓使用者檢視更多詳細資訊或廣告的加長版。</span><span class="sxs-lookup"><span data-stu-id="c4eb8-228">For example an ad may display buttons that allow the user to view more information or a longer version of the ad.</span></span> <span data-ttu-id="c4eb8-229">視訊播放器必須支援 VPAID API，可執行廣告必須實作 API。</span><span class="sxs-lookup"><span data-stu-id="c4eb8-229">The video player must support the VPAID API and the executable ad must implement the API.</span></span> <span data-ttu-id="c4eb8-230">當播放器向廣告伺服器要求廣告時，該伺服器可能會以包含 VPAID 廣告的 VAST 回應進行回應。</span><span class="sxs-lookup"><span data-stu-id="c4eb8-230">When a player requests an ad from an ad server the server may respond with a VAST response that contains a VPAID ad.</span></span>

<span data-ttu-id="c4eb8-231">必須在如 Adobe Flash™ 或可以在網頁瀏覽器中執行的 JavaScript 執行階段環境中執行的程式碼中建立可執行廣告。</span><span class="sxs-lookup"><span data-stu-id="c4eb8-231">An executable ad is created in code that must be executed in a runtime environment such as Adobe Flash™ or JavaScript that can be executed in a web browser.</span></span> <span data-ttu-id="c4eb8-232">當廣告伺服器傳回包含 VPAID 廣告的 VAST 回應時，<MediaFile> 元素中屬性 apiFramework 的值必須是 "VPAID"。</span><span class="sxs-lookup"><span data-stu-id="c4eb8-232">When an ad server returns a VAST response containing a VPAID ad, the value of the apiFramework attribute in the <MediaFile> element must be “VPAID”.</span></span> <span data-ttu-id="c4eb8-233">這個屬性會指定包含的廣告是 VPAID 可執行廣告。</span><span class="sxs-lookup"><span data-stu-id="c4eb8-233">This attribute specifies that the contained ad is a VPAID executable ad.</span></span> <span data-ttu-id="c4eb8-234">類型屬性必須設定為可執行的 MIME 類型，例如 “application/x-shockwave-flash” 或 “application/x-javascript”。</span><span class="sxs-lookup"><span data-stu-id="c4eb8-234">The type attribute must be set to the MIME type of the executable, such as “application/x-shockwave-flash” or “application/x-javascript”.</span></span> <span data-ttu-id="c4eb8-235">下列 XML 程式碼片段顯示來自包含 VPAID 可執行廣告之 VAST 回應的 <MediaFile> 元素。</span><span class="sxs-lookup"><span data-stu-id="c4eb8-235">The following XML snippet shows the <MediaFile> element from a VAST response containing a VPAID executable ad.</span></span> 

    <MediaFiles>
       <MediaFile id="1" delivery="progressive" type=”application/x-shockwaveflash”
                  width=”640” height=”480” apiFramework=”VPAID”>
           <!-- CDATA wrapped URI to executable ad -->
       </MediaFile>
    </MediaFiles>


<span data-ttu-id="c4eb8-236">可以使用 VAST 回應中 <Linear> 或 <NonLinear> 元素內的 <AdParameters> 元素，初始化可執行廣告。</span><span class="sxs-lookup"><span data-stu-id="c4eb8-236">An executable ad can be initialized using the <AdParameters> element within the <Linear> or <NonLinear> elements in a VAST response.</span></span> <span data-ttu-id="c4eb8-237">如需 <AdParameters> 元素的詳細資訊，請參閱 [VAST 3.0](http://www.iab.net/media/file/VASTv3.0.pdf)。</span><span class="sxs-lookup"><span data-stu-id="c4eb8-237">For more information on the <AdParameters> element, see [VAST 3.0](http://www.iab.net/media/file/VASTv3.0.pdf).</span></span> <span data-ttu-id="c4eb8-238">如需 VPAID API 的詳細資訊，請參閱 [VPAID 2.0](http://www.iab.net/media/file/VPAID_2.0_Final_04-10-2012.pdf)。</span><span class="sxs-lookup"><span data-stu-id="c4eb8-238">For more information about the VPAID API, see [VPAID 2.0](http://www.iab.net/media/file/VPAID_2.0_Final_04-10-2012.pdf).</span></span>

## <a name="implementing-a-windows-or-windows-phone-8-player-with-ad-support"></a><span data-ttu-id="c4eb8-239">實作包含廣告支援的 Windows 或 Windows Phone 8 播放器</span><span class="sxs-lookup"><span data-stu-id="c4eb8-239">Implementing a Windows or Windows Phone 8 Player with Ad Support</span></span>
<span data-ttu-id="c4eb8-240">Microsoft 媒體平台：Player Framework for Windows 8 和 Windows Phone 8 包含範例應用程式集合，為您示範如何使用架構實作視訊播放器應用程式。</span><span class="sxs-lookup"><span data-stu-id="c4eb8-240">The Microsoft Media Platform: Player Framework for Windows 8 and Windows Phone 8 contains a collection of sample applications that show you how to implement a video player application using the framework.</span></span> <span data-ttu-id="c4eb8-241">您可以從 [適用於Windows 8 和 Windows Phone 8 的 Player Framework](https://playerframework.codeplex.com)下載 Player Framework 和範例。</span><span class="sxs-lookup"><span data-stu-id="c4eb8-241">You can download the Player Framework and the samples from [Player Framework for Windows 8 and Windows Phone 8](https://playerframework.codeplex.com).</span></span>

<span data-ttu-id="c4eb8-242">當您開啟 Microsoft.PlayerFramework.Xaml.Samples 方案時，您會在專案內看到許多資料夾。</span><span class="sxs-lookup"><span data-stu-id="c4eb8-242">When you open the Microsoft.PlayerFramework.Xaml.Samples solution you will see a number of folders within the project.</span></span> <span data-ttu-id="c4eb8-243">Advertising 資料夾包含與建立具有廣告支援的視訊播放器相關的範例程式碼。</span><span class="sxs-lookup"><span data-stu-id="c4eb8-243">The Advertising folder contains the sample code relevant to creating a video player with ad support.</span></span> <span data-ttu-id="c4eb8-244">在 Advertising 資料夾內有許多 XAML/cs 檔案，每個檔案都會顯示如何以不同方式插入廣告。</span><span class="sxs-lookup"><span data-stu-id="c4eb8-244">Inside the Advertising folder is a number of XAML/cs files each of which show how to insert ads in a different way.</span></span> <span data-ttu-id="c4eb8-245">下列清單分別說明：</span><span class="sxs-lookup"><span data-stu-id="c4eb8-245">The following list describes each:</span></span>

* <span data-ttu-id="c4eb8-246">AdPodPage.xaml 示範如何顯示廣告組合。</span><span class="sxs-lookup"><span data-stu-id="c4eb8-246">AdPodPage.xaml Shows how to display an ad pod.</span></span>
* <span data-ttu-id="c4eb8-247">AdSchedulingPage.xaml 示範如何排程廣告。</span><span class="sxs-lookup"><span data-stu-id="c4eb8-247">AdSchedulingPage.xaml Shows how to schedule ads.</span></span>
* <span data-ttu-id="c4eb8-248">FreeWheelPage.xaml 示範如何使用 FreeWheel 外掛程式排程廣告。</span><span class="sxs-lookup"><span data-stu-id="c4eb8-248">FreeWheelPage.xaml Shows how to use the FreeWheel plugin to schedule ads.</span></span>
* <span data-ttu-id="c4eb8-249">MastPage.xaml 示範如何使用 MAST 檔案排程廣告。</span><span class="sxs-lookup"><span data-stu-id="c4eb8-249">MastPage.xaml Shows how to schedule ads with a MAST file.</span></span>
* <span data-ttu-id="c4eb8-250">ProgrammaticAdPage.xaml 示範如何以程式設計方式在視訊中排程廣告。</span><span class="sxs-lookup"><span data-stu-id="c4eb8-250">ProgrammaticAdPage.xaml Shows how to programmatically schedule ads into a video.</span></span>
* <span data-ttu-id="c4eb8-251">ScheduleClipPage.xaml 示範如何在沒有 VAST 檔案的情況下排程廣告。</span><span class="sxs-lookup"><span data-stu-id="c4eb8-251">ScheduleClipPage.xaml Shows how to schedule an ad without a VAST file.</span></span>
* <span data-ttu-id="c4eb8-252">VastLinearCompanionPage.xaml 示範如何插入線性和隨播廣告。</span><span class="sxs-lookup"><span data-stu-id="c4eb8-252">VastLinearCompanionPage.xaml Shows how to insert a linear and companion ad.</span></span>
* <span data-ttu-id="c4eb8-253">VastNonLinearPage.xaml 示範如何插入非線性廣告。</span><span class="sxs-lookup"><span data-stu-id="c4eb8-253">VastNonLinearPage.xaml Shows how to insert a non-linear ad.</span></span>
* <span data-ttu-id="c4eb8-254">VmapPage.xaml 示範如何使用 VMAP 檔案指定廣告。</span><span class="sxs-lookup"><span data-stu-id="c4eb8-254">VmapPage.xaml Shows how to specify ads with a VMAP file.</span></span>

<span data-ttu-id="c4eb8-255">每個範例會使用 Player Framework 定義的 MediaPlayer 類別。</span><span class="sxs-lookup"><span data-stu-id="c4eb8-255">Each of these samples uses the MediaPlayer class defined by the player framework.</span></span> <span data-ttu-id="c4eb8-256">大部分的範例會使用加入各種廣告回應格式支援的外掛程式。</span><span class="sxs-lookup"><span data-stu-id="c4eb8-256">Most samples use plugins that add support for various ad response formats.</span></span> <span data-ttu-id="c4eb8-257">ProgrammaticAdPage 範例以程式設計方式與 MediaPlayer 執行個體互動。</span><span class="sxs-lookup"><span data-stu-id="c4eb8-257">The ProgrammaticAdPage sample programmatically interacts with a MediaPlayer instance.</span></span>

### <a name="adpodpage-sample"></a><span data-ttu-id="c4eb8-258">AdPodPage 範例</span><span class="sxs-lookup"><span data-stu-id="c4eb8-258">AdPodPage Sample</span></span>
<span data-ttu-id="c4eb8-259">此範例會使用 AdSchedulerPlugin 來定義何時顯示廣告。</span><span class="sxs-lookup"><span data-stu-id="c4eb8-259">This sample uses the AdSchedulerPlugin to define when to display an ad.</span></span> <span data-ttu-id="c4eb8-260">在此範例中，片中廣告排定在 5 秒鐘之後播放。</span><span class="sxs-lookup"><span data-stu-id="c4eb8-260">In this example a mid-roll advertisement is scheduled to be played after 5 seconds.</span></span> <span data-ttu-id="c4eb8-261">廣告組合 (依序顯示的廣告群組) 是在從廣告伺服器傳回的 VAST 檔案中指定。</span><span class="sxs-lookup"><span data-stu-id="c4eb8-261">The ad pod (a group of ads to display in order) is specified in a VAST file returned from an ad server.</span></span> <span data-ttu-id="c4eb8-262">VAST 檔案的 URI 是在 <RemoteAdSource> 元素中指定。</span><span class="sxs-lookup"><span data-stu-id="c4eb8-262">The URI to the VAST file is specified in the <RemoteAdSource> element.</span></span>

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

<span data-ttu-id="c4eb8-263">如需 AdSchedulerPlugin 的詳細資訊，請參閱 [Windows 8 和 Windows Phone 8 上 Player Framework 中的廣告](http://playerframework.codeplex.com/wikipage?title=Advertising&referringTitle=Windows%208%20Player%20Documentation)</span><span class="sxs-lookup"><span data-stu-id="c4eb8-263">For more information about the AdSchedulerPlugin, see [Advertising in the Player Framework on Windows 8 and Windows Phone 8](http://playerframework.codeplex.com/wikipage?title=Advertising&referringTitle=Windows%208%20Player%20Documentation)</span></span>

### <a name="adschedulingpage"></a><span data-ttu-id="c4eb8-264">AdSchedulingPage</span><span class="sxs-lookup"><span data-stu-id="c4eb8-264">AdSchedulingPage</span></span>
<span data-ttu-id="c4eb8-265">此範例也會使用 AdSchedulerPlugin。</span><span class="sxs-lookup"><span data-stu-id="c4eb8-265">This sample also uses the AdSchedulerPlugin.</span></span> <span data-ttu-id="c4eb8-266">它會排程三個廣告，片頭廣告、片中廣告和片尾廣告。</span><span class="sxs-lookup"><span data-stu-id="c4eb8-266">It schedules three ads, a pre-roll ad, a mid-roll ad, and a post-roll ad.</span></span> <span data-ttu-id="c4eb8-267">每個廣告的 VAST 的 URI 是在 <RemoteAdSource> 元素中指定。</span><span class="sxs-lookup"><span data-stu-id="c4eb8-267">The URI to the VAST for each ad is specified in a <RemoteAdSource> element.</span></span>

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


### <a name="freewheelpage"></a><span data-ttu-id="c4eb8-268">FreeWheelPage</span><span class="sxs-lookup"><span data-stu-id="c4eb8-268">FreeWheelPage</span></span>
<span data-ttu-id="c4eb8-269">此範例使用 FreeWheelPlugin，它會指定來源屬性，指定指向 SmartXML 檔案的 URI，該檔案會指定廣告內容以及廣告排程資訊。</span><span class="sxs-lookup"><span data-stu-id="c4eb8-269">This sample uses the FreeWheelPlugin which specifies a Source attribute that specifies a URI that points to a SmartXML file that specifies ad content as well as ad scheduling information.</span></span>

    <mmppf:MediaPlayer x:Name="player" Source="http://smf.blob.core.windows.net/samples/videos/bigbuck.mp4">
                <mmppf:MediaPlayer.Plugins>
                    <ads:FreeWheelPlugin Source="http://smf.blob.core.windows.net/samples/win8/ads/freewheel.xml"/>
                    <ads:AdHandlerPlugin/>
                </mmppf:MediaPlayer.Plugins>
            </mmppf:MediaPlayer>

### <a name="mastpage"></a><span data-ttu-id="c4eb8-270">MastPage</span><span class="sxs-lookup"><span data-stu-id="c4eb8-270">MastPage</span></span>
<span data-ttu-id="c4eb8-271">這個範例會使用可讓您使用 MAST 檔案的 MastSchedulerPlugin。</span><span class="sxs-lookup"><span data-stu-id="c4eb8-271">This sample uses the MastSchedulerPlugin that allows you to use a MAST file.</span></span> <span data-ttu-id="c4eb8-272">來源屬性會指定 MAST 檔案的位置。</span><span class="sxs-lookup"><span data-stu-id="c4eb8-272">The Source attribute specifies the location of the MAST file.</span></span>

    <mmppf:MediaPlayer x:Name="player" Source="http://smf.blob.core.windows.net/samples/videos/bigbuck.mp4">
                <mmppf:MediaPlayer.Plugins>
                    <ads:MastSchedulerPlugin Source="http://smf.blob.core.windows.net/samples/win8/ads/mast.xml" />
                    <ads:AdHandlerPlugin/>
                </mmppf:MediaPlayer.Plugins>
            </mmppf:MediaPlayer>

### <a name="programmaticadpage"></a><span data-ttu-id="c4eb8-273">ProgrammaticAdPage</span><span class="sxs-lookup"><span data-stu-id="c4eb8-273">ProgrammaticAdPage</span></span>
<span data-ttu-id="c4eb8-274">此範例以程式設計方式與 MediaPlayer 互動。</span><span class="sxs-lookup"><span data-stu-id="c4eb8-274">This sample programmatically interacts with the MediaPlayer.</span></span> <span data-ttu-id="c4eb8-275">ProgrammaticAdPage.xaml 檔案會具現化 MediaPlayer：</span><span class="sxs-lookup"><span data-stu-id="c4eb8-275">The ProgrammaticAdPage.xaml file instantiates the MediaPlayer:</span></span>

    <mmppf:MediaPlayer x:Name="player" Source="http://smf.blob.core.windows.net/samples/videos/bigbuck.mp4"/>

<span data-ttu-id="c4eb8-276">ProgrammaticAdPage.xaml.cs 檔案會建立 AdHandlerPlugin，加入 TimelineMarker 以指定廣告何時應該顯示，然後加入 MarkerReached 事件的處理常式，它會載入指定 VAST 檔案之 URI 的 RemoteAdSource，然後播放廣告 。</span><span class="sxs-lookup"><span data-stu-id="c4eb8-276">The ProgrammaticAdPage.xaml.cs file creates an AdHandlerPlugin, adds a TimelineMarker to specify when an ad should be displayed, and then adds a handler for the MarkerReached event which loads a RemoteAdSource specifying a URI to a VAST file, and then plays the ad.</span></span>

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

### <a name="scheduleclippage"></a><span data-ttu-id="c4eb8-277">ScheduleClipPage</span><span class="sxs-lookup"><span data-stu-id="c4eb8-277">ScheduleClipPage</span></span>
<span data-ttu-id="c4eb8-278">此範例會使用 AdSchedulerPlugin，藉由指定包含廣告的 .wmv 檔案來排程片中廣告。</span><span class="sxs-lookup"><span data-stu-id="c4eb8-278">This sample uses the AdSchedulerPlugin to schedule a mid-roll ad by specifying a .wmv file that contains the ad.</span></span>

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

### <a name="vastlinearcompanionpage"></a><span data-ttu-id="c4eb8-279">VastLinearCompanionPage</span><span class="sxs-lookup"><span data-stu-id="c4eb8-279">VastLinearCompanionPage</span></span>
<span data-ttu-id="c4eb8-280">這個範例說明如何使用 AdSchedulerPlugin 來排程具有隨播廣告的片中線性廣告。</span><span class="sxs-lookup"><span data-stu-id="c4eb8-280">This sample illustrates how to use the AdSchedulerPlugin to schedule a mid-roll linear ad with an companion ad.</span></span> <span data-ttu-id="c4eb8-281"><RemoteAdSource> 元素會指定 VAST 檔案的位置。</span><span class="sxs-lookup"><span data-stu-id="c4eb8-281">The <RemoteAdSource> element specifies the location of the VAST file.</span></span>

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

### <a name="vastlinearnonlinearpage"></a><span data-ttu-id="c4eb8-282">VastLinearNonLinearPage</span><span class="sxs-lookup"><span data-stu-id="c4eb8-282">VastLinearNonLinearPage</span></span>
<span data-ttu-id="c4eb8-283">此範例會使用 AdSchedulerPlugin 來排程線性和非線性廣告。</span><span class="sxs-lookup"><span data-stu-id="c4eb8-283">This sample uses the AdSchedulerPlugin to schedule a linear and a non-linear ad.</span></span> <span data-ttu-id="c4eb8-284">VAST 檔案位置是以 <RemoteAdSource> 元素指定。</span><span class="sxs-lookup"><span data-stu-id="c4eb8-284">The VAST file location is specified with the <RemoteAdSource> element.</span></span>

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

### <a name="vmappage"></a><span data-ttu-id="c4eb8-285">VMAPPage</span><span class="sxs-lookup"><span data-stu-id="c4eb8-285">VMAPPage</span></span>
<span data-ttu-id="c4eb8-286">此範例會使用 VmapSchedulerPlugin 排程使用 VMAP 檔案的廣告。</span><span class="sxs-lookup"><span data-stu-id="c4eb8-286">This samples uses the VmapSchedulerPlugin to schedule ads using a VMAP file.</span></span> <span data-ttu-id="c4eb8-287">VMAP 檔案的 URI 是在 <VmapSchedulerPlugin> 元素的 Source 屬性中指定。</span><span class="sxs-lookup"><span data-stu-id="c4eb8-287">The URI to the VMAP file is specified in the Source attribute of the <VmapSchedulerPlugin> element.</span></span>

    <mmppf:MediaPlayer x:Name="player" Source="http://smf.blob.core.windows.net/samples/videos/bigbuck.mp4">
                <mmppf:MediaPlayer.Plugins>
                    <ads:VmapSchedulerPlugin Source="http://smf.blob.core.windows.net/samples/win8/ads/vmap.xml"/>
                    <ads:AdHandlerPlugin/>
                </mmppf:MediaPlayer.Plugins>
            </mmppf:MediaPlayer>

## <a name="implementing-an-ios-video-player-with-ad-support"></a><span data-ttu-id="c4eb8-288">實作具有廣告支援的 iOS 視訊播放器</span><span class="sxs-lookup"><span data-stu-id="c4eb8-288">Implementing an iOS Video Player with Ad Support</span></span>
<span data-ttu-id="c4eb8-289">Microsoft 媒體平台：Player Framework for iOS 包含範例應用程式集合，為您示範如何使用架構實作視訊播放器應用程式。</span><span class="sxs-lookup"><span data-stu-id="c4eb8-289">The Microsoft Media Platform: Player Framework for iOS contains a collection of sample applications that show you how to implement a video player application using the framework.</span></span> <span data-ttu-id="c4eb8-290">您可以從 [Azure Media Player Framework](https://github.com/Azure/azure-media-player-framework)下載 Player Framework 和範例。</span><span class="sxs-lookup"><span data-stu-id="c4eb8-290">You can download the Player Framework and the samples from [Azure Media Player Framework](https://github.com/Azure/azure-media-player-framework).</span></span> <span data-ttu-id="c4eb8-291">此 github 頁面具有連接至 Wiki 的連結，該連結包含 Player Framework 的其他資訊和播放器範例的簡介： [Azure Media Player Wiki](https://github.com/Azure/azure-media-player-framework/wiki/How-to-use-Azure-media-player-framework)。</span><span class="sxs-lookup"><span data-stu-id="c4eb8-291">The github page has a link to a Wiki that contains additional information on the player framework and an introduction to the player sample: [Azure Media Player Wiki](https://github.com/Azure/azure-media-player-framework/wiki/How-to-use-Azure-media-player-framework).</span></span>

### <a name="scheduling-ads-with-vmap"></a><span data-ttu-id="c4eb8-292">使用 VMAP 排程廣告</span><span class="sxs-lookup"><span data-stu-id="c4eb8-292">Scheduling Ads with VMAP</span></span>
<span data-ttu-id="c4eb8-293">下列範例示範如何使用 VMAP 檔案排程廣告。</span><span class="sxs-lookup"><span data-stu-id="c4eb8-293">The following example shows how to schedule ads using a VMAP file.</span></span>

    // How to schedule an Ad using VMAP.
    //First download the VMAP manifest

    if (![framework.adResolver downloadManifest:&manifest withURL:[NSURL URLWithString:@"http://portalvhdsq3m25bf47d15c.blob.core.windows.net/vast/PlayerTestVMAP.xml"]])
            {
                [self logFrameworkError];
            }
            else
            {
                // Schedule a list of ads using the downloaded VMAP manifest
                if (![framework scheduleVMAPWithManifest:manifest])
                {
                    [self logFrameworkError];
                }          
            }

### <a name="scheduling-ads-with-vast"></a><span data-ttu-id="c4eb8-294">使用 VAST 排程廣告</span><span class="sxs-lookup"><span data-stu-id="c4eb8-294">Scheduling Ads with VAST</span></span>
<span data-ttu-id="c4eb8-295">下列範例示範如何排程晚期繫結 VAST 廣告。</span><span class="sxs-lookup"><span data-stu-id="c4eb8-295">The following sample shows how to schedule a late binding VAST ad.</span></span>

    //Example:3 How to schedule a late binding VAST ad.
    // set the start time for the ad
    adLinearTime.startTime = 13;
    adLinearTime.duration = 0;
    // Specify the URI of the VAST file
    NSString *vastAd1=@"http://portalvhdsq3m25bf47d15c.blob.core.windows.net/vast/PlayerTestVAST.xml";
    // Create an AdInfo object
     AdInfo *vastAdInfo1 = [[[AdInfo alloc] init] autorelease];
    // set URL to VAST file
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

   <span data-ttu-id="c4eb8-296">下列範例示範如何排程早期繫結 VAST 廣告。</span><span class="sxs-lookup"><span data-stu-id="c4eb8-296">The following sample shows how to schedule an early binding VAST ad.</span></span>
<span data-ttu-id="c4eb8-297">//Example:4 Schedule an early binding VAST ad //Download the VAST file if (![framework.adResolver downloadManifest:&manifest withURL:[NSURL URLWithString:@"http://portalvhdsq3m25bf47d15c.blob.core.windows.net/vast/PlayerTestVAST.xml"]]) { [self logFrameworkError]; } else { adLinearTime.startTime = 7; adLinearTime.duration = 0;</span><span class="sxs-lookup"><span data-stu-id="c4eb8-297">//Example:4 Schedule an early binding VAST ad //Download the VAST file if (![framework.adResolver downloadManifest:&manifest withURL:[NSURL URLWithString:@"http://portalvhdsq3m25bf47d15c.blob.core.windows.net/vast/PlayerTestVAST.xml"]]) { [self logFrameworkError]; } else { adLinearTime.startTime = 7; adLinearTime.duration = 0;</span></span>

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

<span data-ttu-id="c4eb8-298">下列範例示範如何使用粗略剪裁編輯 (RCE) 插入廣告</span><span class="sxs-lookup"><span data-stu-id="c4eb8-298">The following sample shows how to insert an ad using Rough Cut Editing (RCE)</span></span>

    //Example:1 How to use RCE.
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

<span data-ttu-id="c4eb8-299">下列範例示範如何排程廣告組合。</span><span class="sxs-lookup"><span data-stu-id="c4eb8-299">The following example shows how to schedule an ad pod.</span></span>

    //Example:5 Schedule an ad Pod.
    // Set start time for ad
    adLinearTime.startTime = 23;
    adLinearTime.duration = 0;

    // Specify URL to content
    NSString *adpodSt1=@"https://portalvhdsq3m25bf47d15c.blob.core.windows.net/asset-e47b43fd-05dc-4587-ac87-5916439ad07f/Windows%208_%20Cliffjumpers.mp4?st=2012-11-28T16%3A31%3A57Z&se=2014-11-28T16%3A31%3A57Z&sr=c&si=2a6dbb1e-f906-4187-a3d3-7e517192cbd0&sig=qrXYZBekqlbbYKqwovxzaVZNLv9cgyINgMazSCbdrfU%3D";
    // Create an AdInfo instance
    AdInfo *adpodInfo1 = [[[AdInfo alloc] init] autorelease];
    // set URI to ad content
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

<span data-ttu-id="c4eb8-300">下列範例示範如何排程非固定片中廣告。</span><span class="sxs-lookup"><span data-stu-id="c4eb8-300">The following example shows how to schedule a non-sticky mid-roll ad.</span></span> <span data-ttu-id="c4eb8-301">不論檢視者執行任何搜尋，非固定廣告只會播放一次。</span><span class="sxs-lookup"><span data-stu-id="c4eb8-301">A non-sticky ad is only played once regardless of any seeking the viewer performs.</span></span>

    //Example:6 Schedule a single non sticky mid roll Ad
    // specify URL to content
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

<span data-ttu-id="c4eb8-302">下列範例示範如何排程固定片中廣告。</span><span class="sxs-lookup"><span data-stu-id="c4eb8-302">The following example shows how to schedule a sticky mid-roll ad.</span></span> <span data-ttu-id="c4eb8-303">固定廣告會在每次到達視訊時間軸上的指定點時顯示。</span><span class="sxs-lookup"><span data-stu-id="c4eb8-303">A sticky ad will be displayed each time the specified point on the video timeline is reached.</span></span>

    //Example:7 Schedule a single sticky mid roll Ad
    NSString *stickyAd=@"http://wamsblureg001orig-hs.cloudapp.net/2e4e7d1f-b72a-4994-a406-810c796fc4fc/The%20Surface%20Movement-m3u8-aapl.ism/Manifest(format=m3u8-aapl)";
    // create AdInfo instance
    AdInfo *stickyAdInfo = [[[AdInfo alloc] init] autorelease];
    // set URI to ad
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


<span data-ttu-id="c4eb8-304">下列範例示範如何排程片尾廣告。</span><span class="sxs-lookup"><span data-stu-id="c4eb8-304">The following sample shows how to schedule a post-roll ad.</span></span>

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

<span data-ttu-id="c4eb8-305">下列範例示範如何排程片頭廣告。</span><span class="sxs-lookup"><span data-stu-id="c4eb8-305">The following sample shows how to schedule a pre-roll ad.</span></span>

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

<span data-ttu-id="c4eb8-306">下列範例示範如何排程片中重疊廣告。</span><span class="sxs-lookup"><span data-stu-id="c4eb8-306">The following sample shows how to schedule a mid-roll overlay ad.</span></span>

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



## <a name="media-services-learning-paths"></a><span data-ttu-id="c4eb8-307">媒體服務學習路徑</span><span class="sxs-lookup"><span data-stu-id="c4eb8-307">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="c4eb8-308">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="c4eb8-308">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="c4eb8-309">另請參閱</span><span class="sxs-lookup"><span data-stu-id="c4eb8-309">See Also</span></span>
[<span data-ttu-id="c4eb8-310">開發視訊播放程式應用程式</span><span class="sxs-lookup"><span data-stu-id="c4eb8-310">Develop video player applications</span></span>](media-services-develop-video-players.md)

