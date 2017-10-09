---
title: "使用媒體處理器 aaaHow tooCreate hello Azure Media Services SDK for.NET |Microsoft 文件"
description: "了解 toocreate 媒體處理器元件 tooencode 」，將格式轉換、 加密或解密媒體內容，Azure 媒體服務的方式。 程式碼範例會以 C# 所撰寫，並使用 hello Media Services SDK for.NET。"
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: dbf9496f-c6f0-42a7-aa36-70f89dcb8ea2
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: juliako
ms.openlocfilehash: f133565cc1321d366013f17302adc8bc7585b251
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-to-get-a-media-processor-instance"></a>如何：取得媒體處理器執行個體
> [!div class="op_single_selector"]
> * [.NET](media-services-get-media-processor.md)
> * [REST](media-services-rest-get-media-processor.md)
> 
> 

## <a name="overview"></a>Overview
在媒體服務中，媒體處理器是可處理特定處理工作的元件，例如編碼、格式轉換、加密或解密媒體內容。 通常當您建立工作 tooencode 建立媒體處理器、 加密，或將媒體內容的 hello 格式轉換。

## <a name="azure-media-processors"></a>Azure 媒體處理器 

hello 下列主題提供媒體處理器的清單：

* [編碼媒體處理器](scenarios-and-availability.md#encoding-media-processors)
* [分析媒體處理器](scenarios-and-availability.md#analytics-media-processors)

## <a name="get-media-processor"></a>取得媒體處理器

hello 遵循方法顯示如何 tooget 媒體處理器執行個體。 hello 程式碼範例假設名為的模組層級變數 hello 使用**（_c)** tooreference hello 伺服器內容 hello > 一節中所述[如何： 連接服務以程式設計方式 tooMedia](media-services-use-aad-auth-to-access-ams-api.md)。

    private static IMediaProcessor GetLatestMediaProcessorByName(string mediaProcessorName)
    {
        var processor = _context.MediaProcessors.Where(p => p.Name == mediaProcessorName).
        ToList().OrderBy(p => new Version(p.Version)).LastOrDefault();

        if (processor == null)
        throw new ArgumentException(string.Format("Unknown media processor", mediaProcessorName));

        return processor;
    }


## <a name="media-services-learning-paths"></a>媒體服務學習路徑
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>提供意見反應
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a>後續步驟
您現在知道如何 tooget 媒體處理器執行個體中，移 toohello[如何 tooEncode 資產](media-services-dotnet-encode-with-media-encoder-standard.md)這會顯示如何 toouse 會 hello 媒體編碼器標準 tooencode 資產的主題。

