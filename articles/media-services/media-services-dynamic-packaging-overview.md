---
title: "aaaAzure Media Services 動態封裝概觀 |Microsoft 文件"
description: "hello 主題提供和動態封裝的概觀。"
author: Juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: 0d9e4f54-5daa-45c1-bfaa-cf09ca89b812
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: juliako
ms.openlocfilehash: 970e24eba800e098774172c87f56629430b227a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="dynamic-packaging"></a>動態封裝
## <a name="overview"></a>概觀
Microsoft Azure Media Services 可以使用的 toodeliver 許多媒體來源檔案格式、 媒體串流格式和內容保護格式 tooa 各種不同的用戶端技術 (比方說，iOS、 XBOX、 Silverlight、 Windows 8)。 這些用戶端各自使用不同的通訊協定，例如 iOS 需要 HTTP 即時串流 (HLS) V4 格式，而 Silverlight 與 Xbox 需要 Smooth Streaming。 如果您有一組彈性位元速率 （多位元速率） MP4 (ISO Base Media 14496-12) 檔案或一組彈性位元速率 Smooth Streaming 檔案的 MPEG DASH、 HLS 或 Smooth Streaming 的 tooserve tooclients，您應該利用媒體服務動態封裝。

您只需要動態封裝是 toocreate 包含一組彈性位元速率 MP4 檔案或彈性位元速率 Smooth Streaming 檔案的資產。 然後，hello hello 資訊清單中指定的格式為基礎或片段要求中 hello 隨選串流伺服器可確保您已選擇 hello 通訊協定接收 hello 資料流。 如此一來，您只需要 toostore 及支付一種儲存格式和 Media Services 服務中的 hello 檔案將會建立及傳遞 hello 適當的回應，根據用戶端的要求。

hello 下列圖表顯示 hello 傳統編碼和靜態封裝工作流程。

![靜態編碼](./media/media-services-dynamic-packaging-overview/media-services-static-packaging.png)

hello 下列圖表顯示 hello 動態封裝工作流程。

![動態編碼](./media/media-services-dynamic-packaging-overview/media-services-dynamic-packaging.png)


## <a name="common-scenario"></a>常見的案例
1. 上傳輸入檔案 (稱為夾層檔)。 例如，H.264、 MP4 或 WMV (如 hello 的支援格式清單，請參閱[格式支援的媒體編碼器標準 hello](media-services-media-encoder-standard-formats.md)。
2. 編碼夾層檔 tooH.264 MP4 彈性位元速率集。
3. 發行包含 hello 自動調整位元速率 MP4 集藉由建立 hello 上隨選 Locator hello 資產。
4. 建置串流 Url tooaccess hello 和串流處理內容。

## <a name="preparing-assets-for-dynamic-streaming"></a>準備動態串流的資產
tooprepare 資產用於動態串流處理您有兩個選項：

1. [上傳主檔案](media-services-dotnet-upload-files.md)。
2. [使用 hello 媒體編碼器標準編碼器 tooproduce H.264 MP4 彈性位元速率集](media-services-dotnet-encode-with-media-encoder-standard.md)。
3. [串流處理內容](media-services-deliver-content-overview.md)。

## <a id="unsupported_formats"></a>動態封裝不支援的格式
hello 下列來源檔案格式不受動態封裝。

* Dolby digital mp4 檔案。
* Dolby digital smooth 檔案。

## <a name="media-services-learning-paths"></a>媒體服務學習路徑
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>提供意見反應
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

