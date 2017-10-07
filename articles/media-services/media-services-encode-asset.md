---
title: "aaaOverview 與 Azure 上比較要求的媒體編碼器 |Microsoft 文件"
description: "本主題概要說明並比較 Azure 隨選媒體編碼器。"
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: e6bfc068-fa46-4d68-b1ce-9092c8f3a3c9
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/10/2017
ms.author: juliako
ms.openlocfilehash: 24a3e0a16162b1bebfcde290b6baf2dd8dbfff17
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="overview-and-comparison-of-azure-on-demand-media-encoders"></a>Azure 隨選媒體編碼器的概觀和比較
## <a name="encoding-overview"></a>編碼概觀
Azure Media Services 提供多個 hello 編碼媒體 hello 雲端中的選項。

開始使用 Media Services，很重要的 toounderstand hello 差異轉碼器與檔案格式。
轉碼器是實作 hello 壓縮/解壓縮演算法，而檔案格式是保留 hello 壓縮視訊的容器的 hello 軟體。

Media Services 提供動態封裝可讓您 toodeliver MP4 或 Smooth Streaming 您彈性位元速率編碼格式 （MPEG DASH、 HLS、 Smooth Streaming） 的 Media Services 支援的資料流處理中的內容，而不必 toore 封裝至您串流格式。

>[!NOTE]
>AMS 帳戶建立時**預設**串流端點就會加入 tooyour 帳戶 hello**已停止**狀態。 串流處理您的內容，並採取利用動態封裝和動態加密，toostart hello 串流端點，您想要從中 toostream 內容已經在 hello toobe**執行**狀態。 tootake 利用[動態封裝](media-services-dynamic-packaging-overview.md)，您需要 toodo hello 下列：
>
>此外，編碼為一組彈性位元速率 MP4 檔案或彈性位元速率 Smooth Streaming 檔案 （hello 編碼步驟示範稍後在本教學課程） 的原始程式檔。

Media Services 支援 hello 下列上這篇文章所述的需求編碼器：

* [Media Encoder Standard](media-services-encode-asset.md#media-encoder-standard)
* [媒體編碼器高階工作流程](media-services-encode-asset.md#media-encoder-premium-workflow)

本文簡短介紹的隨選媒體編碼器，並提供連結 tooarticles，提供更詳細的資訊。 hello 主題也提供 hello 編碼器的比較。

>[!NOTE]
>依預設，每個媒體服務帳戶一次可以有一個進行中的編碼工作。 您可以保留編碼單元可讓您 toohave 同時執行，一個用於每個您所購買的編碼保留單元的多個編碼工作。 如需相關資訊，請參閱 [調整編碼單位](media-services-scale-media-processing-overview.md)。

## <a name="media-encoder-standard"></a>Media Encoder Standard
### <a name="how-toouse"></a>如何 toouse
[如何與媒體編碼器標準 tooencode](media-services-dotnet-encode-with-media-encoder-standard.md)

### <a name="formats"></a>格式
[格式和轉碼器](media-services-media-encoder-standard-formats.md)

### <a name="presets"></a>預設值
媒體編碼器標準設定時，使用其中一個所述的 hello 編碼器預設[這裡](http://go.microsoft.com/fwlink/?linkid=618336&clcid=0x409)。

### <a name="input-and-output-metadata"></a>輸入和輸出中繼資料
hello 編碼器輸入中繼資料描述[這裡](media-services-input-metadata-schema.md)。

hello 編碼器輸出中繼資料描述[這裡](media-services-output-metadata-schema.md)。

### <a name="generate-thumbnails"></a>產生縮圖
如需資訊，請參閱[如何使用媒體編碼器標準 toogenerate 縮圖](media-services-advanced-encoding-with-mes.md#thumbnails)。

### <a name="trim-videos-clipping"></a>修剪視訊 (裁剪)
資訊，請參閱[如何使用媒體編碼器標準 tootrim 視訊](media-services-advanced-encoding-with-mes.md#trim_video)。

### <a name="create-overlays"></a>建立疊加層
資訊，請參閱[如何使用媒體編碼器標準 toocreate 覆疊](media-services-advanced-encoding-with-mes.md#overlay)。

### <a name="see-also"></a>另請參閱
[hello 媒體服務部落格](https://azure.microsoft.com/blog/2015/07/16/announcing-the-general-availability-of-media-encoder-standard/)

## <a name="media-encoder-premium-workflow"></a>媒體編碼器高階工作流程
### <a name="overview"></a>Overview
[介紹 Azure 媒體服務中的 Premium 編碼](https://azure.microsoft.com/blog/2015/03/05/introducing-premium-encoding-in-azure-media-services/)

### <a name="how-toouse"></a>如何 toouse
Media Encoder Premium Workflow 使用複雜的工作流程設定。 無法建立工作流程檔案，並使用 hello 更新[工作流程設計工具](media-services-workflow-designer.md)工具。

[如何在 Azure Media Services 編碼 Premium tooUse](https://azure.microsoft.com/blog/2015/03/06/how-to-use-premium-encoding-in-azure-media-services/)

### <a name="known-issues"></a>已知問題
如果您輸入的視訊不包含字幕，hello 輸出資產仍然會包含空白的 TTML 檔案。


## <a name="media-services-learning-paths"></a>媒體服務學習路徑
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>提供意見反應
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-articles"></a>相關文章
* [透過自訂 Media Encoder Standard 預設值來執行進階編碼工作](media-services-custom-mes-presets-with-dotnet.md)
* [配額和限制](media-services-quotas-and-limitations.md)

<!--Reference links in article-->
[1]: http://azure.microsoft.com/pricing/details/media-services/
