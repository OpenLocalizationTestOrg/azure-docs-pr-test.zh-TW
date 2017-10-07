---
title: "aaaDevelop 影片播放器應用程式"
description: "hello 主題提供的連結 tooPlayer 架構和外掛程式，您可以使用 toodevelop 自己的用戶端應用程式可以取用從媒體服務串流媒體。"
author: Juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: 55e419fc-4c39-4902-9c62-f41cfcd86c6c
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: juliako
ms.openlocfilehash: a66daa4f006a1f05271cc9ed6a02ea7ee460321d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="develop-video-player-applications"></a>開發視訊播放器應用程式
## <a name="overview"></a>概觀
Azure Media Services 提供 hello 工具，您需要 toocreate 豐富、 動態的用戶端播放器應用程式，用於大部分平台，包括： iOS 裝置、 Android 裝置、 Windows、 Windows Phone、 Xbox 和機上方塊。 本主題也會提供連結 tooSDKs 和播放器架構，您可以使用 toodevelop 自己的用戶端應用程式可以取用從 Azure 媒體服務串流媒體。

>[!NOTE]
>AMS 帳戶建立時**預設**串流端點就會加入 tooyour 帳戶 hello**已停止**狀態。 串流處理您的內容，並採取利用動態封裝和動態加密，toostart hello 串流端點，您想要從中 toostream 內容已經在 hello toobe**執行**狀態。 
 
## <a name="azure-media-player"></a>Azure 媒體播放器
[Azure Media Player](http://aka.ms/ampinfo) web 影片播放器 tooplay 後媒體內容從 Microsoft Azure Media Services 上建立各種不同的瀏覽器及裝置。 Azure Media Player 會使用業界標準，例如 HTML5、 媒體來源延伸模組 (MSE) 和加密媒體擴充功能 (EME) tooprovide 豐富的彈性串流處理體驗。 無法在裝置或瀏覽器使用這些標準時，Azure Media Player 則會使用 Flash 和 Silverlight 做為後援技術。 無論用 hello 播放技術，開發人員會有統一的 JavaScript 介面 tooaccess 應用程式開發介面。 這可讓內容由 Azure Media Services toobe 播放跨各種裝置和瀏覽器，而不需要任何額外的工作。

Microsoft Azure Media Services 可讓內容 toobe 提供 Smooth Streaming、 DASH 和 HLS 資料流格式 tooplay 備份內容。 Azure Media Player 會考量這些不同的格式，並自動播放 hello 根據 hello 平台/瀏覽器功能的最佳連結。 Microsoft Azure 媒體服務也允許利用 PlayReady 加密或 AES 128 位元信封加密，進行資產的動態加密。 只要設定正確，Azure Media Player 允許解密 PlayReady 和 AES 128 位元加密的內容。 

其他資訊：

* [Azure Media Player](http://aka.ms/ampinfo)
* [Azure Media Player 文件](http://aka.ms/ampdocs) 
* [Azure Media Player 開始使用部落格](https://azure.microsoft.com/blog/2015/04/15/announcing-azure-media-player/)
* [登入，以最新的 Azure Media Player 的 hello toodate 向上 toostay](http://aka.ms/ampsignup)
* [新增功能要求、概念和意見反應](http://aka.ms/ampuservoice) 

## <a name="other-tools-for-creating-player-applications"></a>其他可用來建立播放器應用程式的工具
您也可以使用任何下列 Sdk hello:

* [Smooth Streaming Client SDK](http://www.iis.net/downloads/microsoft/smooth-streaming) 
* [Smooth Streaming Windows 市集應用程式](media-services-build-smooth-streaming-apps.md)
* [Microsoft 媒體平台：Player Framework](http://playerframework.codeplex.com/) 
* [HTML5 Player Framework 文件](http://playerframework.codeplex.com/wikipage?title=HTML5%20Player&referringTitle=Documentation) 
* [Microsoft Smooth Streaming Plugin for OSMF](https://www.microsoft.com/download/details.aspx?id=36057) 
* [Licensing Microsoft® Smooth Streaming Client Porting Kit](http://aka.ms/sspk) 
* [XBOX Video Application Development](http://xbox.create.msdn.com/) 

## <a name="advertising"></a>廣告
Azure Media Services 提供廣告插入 hello Windows 媒體平台的支援： 播放器架構。 具備廣告支援的播放器架構都適用於 Windows 8、Silverlight、Windows Phone 8 和 iOS 裝置。 每個播放器架構包含範例程式碼，為您示範如何 tooimplement 播放器應用程式。 目前有三種不同的廣告可以插入媒體中：

線性 – 暫停主要影片的 hello 的完整框架廣告

非線性 – hello 主要影片播放時顯示的重疊廣告，通常標誌或其他靜態影像放置於 hello 播放程式內。

隨播 – 顯示 hello 播放程式之外的廣告

廣告可以放在任何時間點 hello 主要影片的時間線。 您必須告知 hello player tooplay 當 hello ad，以及哪些廣告 tooplay。 使用一組標準的 XML 格式檔案即可搞定：Video Ad Service Template (VAST)、Digital Video Multiple Ad Playlist (VMAP)、Media Abstract Sequencing Template (MAST) 以及 Digital Video Player Ad Interface Definition (VPAID)。 VAST 檔案會指定哪些廣告 toodisplay。 VMAP 檔案會指定何時 tooplay 各種廣告及包含 VAST XML。 MAST 檔案是另一個方式 toosequence 廣告也可包含 VAST XML。 VPAID 檔案會定義 hello 影片播放器與 hello 廣告或廣告伺服器之間的介面。 如需詳細資訊，請參閱 [插入廣告](https://msdn.microsoft.com/library/dn387398.aspx)。

如需了解即時資料流視訊的隱藏式字幕和廣告支援，請參閱 [支援的隱藏式輔助字幕和廣告插入標準](https://msdn.microsoft.com/library/c49e0b4d-357e-4cca-95e5-2288924d1ff3#caption_ad)。

## <a name="media-services-learning-paths"></a>媒體服務學習路徑
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>提供意見反應
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a>另請參閱
[透過 DASH.js 將 MPEG-DASH 彈性資料流視訊嵌入到 HTML5 應用程式](media-services-embed-mpeg-dash-in-html5.md)

[GitHub dash.js 存放庫](https://github.com/Dash-Industry-Forum/dash.js)

