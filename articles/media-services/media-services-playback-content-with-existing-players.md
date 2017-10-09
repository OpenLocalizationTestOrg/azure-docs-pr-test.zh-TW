---
title: "現有的播放程式 tooplayback 內容-Azure aaaUse |Microsoft 文件"
description: "本主題列出現有的播放程式，您可以使用 tooplayback 您的內容。"
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 7e9fcf89-0fb6-4fa4-96cb-666320684d69
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: juliako
ms.openlocfilehash: 54817345a19a9d3b18f1e7b352c3342043a569b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="playing-your-content-with-existing-players"></a>使用現有播放器來播放您的內容
Azure 媒體服務支援許多熱門的串流格式，例如 Smooth Streaming、HTTP 即時資料流和 MPEG-Dash。 本主題會指引您 tooexisting 播放程式，您可以使用 tootest 您的資料流。

### <a name="hello-azure-portal-media-services-content-player"></a>hello Azure 入口網站媒體服務內容播放程式
hello **Azure**入口網站提供內容的播放程式，您可以使用 tootest 視訊。

Hello 按一下所需的視訊 (請確定它是[發行](media-services-portal-publish.md)) 按一下 hello**播放**在 hello hello 入口網站底部的按鈕。

適用一些考量事項：

* hello**媒體服務內容播放程式**播放從 hello 預設串流端點。 如果您想 tooplay 從非預設串流端點，請使用其他播放器。 例如， [Azure 媒體播放器](http://amsplayer.azurewebsites.net/azuremediaplayer.html)。

![AMSPlayer][AMSPlayer]

### <a name="azure-media-player"></a>Azure 媒體播放器
使用[Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html) tooplayback 內容 （清除或受保護） 中任何 hello 下列格式：

* Smooth Streaming
* MPEG DASH
* HLS
* Progressive MP4

### <a name="flash-player"></a>Flash Player
#### <a name="aes-encrypted-with-token"></a>AES 加密與權杖
[http://aestoken.azurewebsites.net](http://aestoken.azurewebsites.net)

### <a name="silverlight-players"></a>Silverlight 播放程式
#### <a name="monitoring"></a>監視
[http://smf.cloudapp.net/healthmonitor](http://smf.cloudapp.net/healthmonitor)

#### <a name="playready-with-token"></a>PlayReady 與權杖
[http://sltoken.azurewebsites.net](http://sltoken.azurewebsites.net)

### <a name="dash-players"></a>DASH 播放程式
[http://dashplayer.azurewebsites.net](http://dashplayer.azurewebsites.net)

[http://dashif.org](http://dashif.org)

### <a name="other"></a>其他
tootest HLS Url，您也可以使用：

* **Safari** 或
* **3ivx HLS 播放器** 。

## <a name="developing-video-players"></a>開發視訊播放器
如需有關如何 toodevelop 您自己的播放程式，請參閱資訊[開發視訊播放程式](media-services-develop-video-players.md)

## <a name="media-services-learning-paths"></a>媒體服務學習路徑
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>提供意見反應
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

[AMSPlayer]: ./media/media-services-playback-content-with-existing-players/media-services-portal-player.png
