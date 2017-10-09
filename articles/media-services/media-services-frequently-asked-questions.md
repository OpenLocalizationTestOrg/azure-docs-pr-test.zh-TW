---
title: "aaaAzure Media Services 常見問題集 |Microsoft 文件"
description: "常見問題集 (FAQ)"
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 5374f7f4-c189-43ef-8b7f-f2f4141e2748
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: juliako
ms.openlocfilehash: 6d48a5c1291f3c2559d8445921d571718d0a0a6d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-questions"></a>常見問題集

本文中的 hello Azure 媒體服務 (AMS) 中使用者社群所引發的常見問題。

## <a name="general-ams-faqs"></a>一般 AMS 常見問題集
問：如何調整索引？

答： hello 保留單位的編碼方式和索引工作會 hello 相同。 依指示[如何 tooScale 編碼保留單元](media-services-scale-media-processing-overview.md)。 **請注意** ，Indexer 效能不受保留單元類型影響。

問：我已上傳、編碼以及發佈視訊。 什麼是 hello 原因 hello 視訊不是扮演當我嘗試 toostream 它嗎？

答： 其中一個最常見的原因是您不需要串流的端點，嘗試在 hello tooplayback hello hello**執行**狀態。  

問：我可以編輯即時資料流？

答： 複合即時資料流上目前不提供在 Azure Media Services 中，因此您必須 toopre-撰寫您的電腦上。

問：Azure CDN 可以搭配即時資料流使用？

答： Media Services 支援與 Azure CDN 整合 (如需詳細資訊，請參閱[如何在 Media Services 帳戶中的 tooManage 資料流端點](media-services-portal-manage-streaming-endpoints.md))。  即時資料流可以搭配 CDN 使用。 Azure 媒體服務提供 Smooth Streaming、HLS 和 MPEG-DASH 輸出。 所有這些格式都使用 HTTP 來傳送資料以及獲得 HTTP 快取的優點。 在即時資料流的實際視訊/音訊資料是分割的 toofragments 和這個個別的片段會被在 CDN 中快取。 只有資料需求 toobe 重新整理是 hello 資訊清單的資料。 CDN 會定期重新整理資訊清單資料。

問：Azure 媒體服務支援儲存影像？

答： 如果您只想 toostore JPEG 或 PNG 影像，您應該將 Azure Blob 儲存體中。 沒有任何在 Media Services 帳戶除非您想的 tookeep 它們與您的視訊或音訊資產相關聯的權益 tooputting。 或如果您為 hello 視訊編碼程式中的覆疊可能需要 toouse hello 映像。媒體編碼器標準支援在視訊頂端的覆疊影像，而這就是什麼它會列出 JPEG 和 PNG 支援輸入格式。 如需詳細資訊，請參閱 [建立重疊](media-services-advanced-encoding-with-mes.md#overlay)。

問： 如何從一個 Media Services 帳戶 tooanother 複製資產。

答： toocopy 資產，從一個 Media Services 帳戶 tooanother 使用.NET 中，使用[IAsset.Copy](https://github.com/Azure/azure-sdk-for-media-services-extensions/blob/dev/MediaServices.Client.Extensions/IAssetExtensions.cs#L354) hello 中可用的擴充方法[Azure Media Services.NET SDK Extensions](https://github.com/Azure/azure-sdk-for-media-services-extensions/)儲存機制。 如需詳細資訊，請參閱 [這個](https://social.msdn.microsoft.com/Forums/azure/28912d5d-6733-41c1-b27d-5d5dff2695ca/migrate-media-services-across-subscription?forum=MediaServices) 論壇執行緒。

問： 哪些是 hello 支援字元時使用 AMS 命名的檔案嗎？

答： Media Services 使用 hello hello IAssetFile.Name 屬性值，當建置 Url 的 hello 串流處理內容 (例如，http://{AMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/streamingParameters。)基於這個理由，不允許 percent-encoding。 hello hello 值**名稱**屬性不能有 hello 下列任何一項[百分比編碼的保留字元](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters): ！ *' （);: @& = + $，/？ %# []"。 此外，只能有一個 ‘.’ hello 檔案名稱副檔名。

問： 如何將 tooconnect 使用嗎？

答： 如需如何 tooconnect toohello AMS API，請參閱[存取 hello Azure 媒體服務 API 與 Azure AD 驗證](media-services-use-aad-auth-to-access-ams-api.md)。 已成功連接之後 toohttps://media.windows.net，您會收到指定另一個媒體服務 URI 的 301 重新導向。 您必須進行的後續呼叫 toohello 新的 URI。 

問： 如何在編碼程序的 hello 旋轉視訊。

答： hello[媒體編碼器標準](media-services-dotnet-encode-with-media-encoder-standard.md)支援 90/180/270 的旋轉角度。 hello 預設行為是 「 自動 」，它會嘗試 toodetect hello 旋轉檔案中繼資料 hello 傳入 MP4/MOV 和補償它。 Hello 如下**來源**hello json 預設定義的項目 tooone[這裡](media-services-mes-presets-overview.md):

    "Version": 1.0,
    "Sources": [
    {
      "Streams": [],
      "Filters": {
        "Rotation": "90"
      }
    }
    ],
    "Codecs": [

    ...


## <a name="media-services-learning-paths"></a>媒體服務學習路徑
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>提供意見反應
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
