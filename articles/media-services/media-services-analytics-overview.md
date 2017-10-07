---
title: "hello Media Services 平台上的分析 aaaMedia |Microsoft 文件"
description: "媒體分析公開預覽、企業規模的語音和電腦視覺服務集合、相容性、安全性和遍及全球的觸角概觀"
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: c56e3781-8510-4f7f-b5ff-a218c1bb6f4c
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 06/29/2017
ms.author: milanga;juliako;johndeu
ms.openlocfilehash: 7545f0532d7618164ebe65e2f4232c5f63453cfd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="media-analytics-on-hello-media-services-platform"></a>Hello Media Services 平台上的媒體分析
## <a name="overview"></a>概觀
多個組織會使用視訊做為 hello 慣用中型 tootrain 員工、 客戶，與文件商務功能中進行。 雲端運算提供方式 toostore，串流處理，以及存取這些大型的媒體檔案。 但您公司的文件庫的視訊內容成長時，還需要從 hello 內容擷取 insights 同樣有效方法。 

tooaddress 這個持續成長的需要，Azure Media Services 提供 Azure 媒體分析。 媒體分析是語音和願景的元件，讓組織和企業 tooderive 可執行的洞察力更容易從視訊檔案的集合。 建立使用 hello 核心 Media Services 平台元件，媒體分析可以處理媒體處理上一天的小數位數。

有了媒體分析，開發人員可以快速地將進階影片功能帶入應用程式。 Hello 完整標尺、 相容性、 安全性和大型組織所需的全球化提供的企業環境。

hello 下列圖表顯示媒體分析和其他 hello Media Services 平台的主要部分。 

![VoD 工作流程](./media/media-services-analytics-overview/media-services-analytics-overview01.png)

媒體分析的媒體處理器會產生 MP4 檔案或 JSON 檔案。 媒體處理器就會產生的 MP4 檔案，您可以漸進式下載 hello 檔案。 媒體處理器就會產生 JSON 檔案，您可以從 Azure Blob 儲存體下載 hello 檔案。 

## <a name="media-analytics-services"></a>媒體分析服務

### <a name="indexer"></a>索引器
Azure 媒體索引器可讓您的內容可供搜尋，並且產生隱藏式輔助字幕。 比較的 toohello 舊版本中，Azure Media Indexer 2 預覽具有更快索引和更廣泛的語言支援。 支援的語言包括英文、西班牙文、法文、德文、義大利文、中文、葡萄牙文和阿拉伯文。 如需詳細資訊和範例，請參閱[利用 Azure 媒體索引器 2 處理影片](media-services-process-content-with-indexer2.md)。
### <a name="hyperlapse"></a>Hyperlapse
Microsoft Hyperlapse 結合視訊穩定和螢光功能 toocreate 快速，您可以使用視訊從您的完整格式內容。 除了建立螢光視訊，您可以使用 Hyperlapse toocreate 穩定影片 shaky 擷取透過行動電話和攝影機的視訊。 如需詳細資訊和範例，請參閱 [Hyperlapse 媒體檔案與 Azure 媒體超縮時攝影](media-services-hyperlapse-content.md)。
### <a name="motion-detector"></a>動作偵測
您可以使用動作偵測器 toodetect 影片中，具有固定的背景的視訊。 這使得可能的誤判 toocheck 影片監視攝影機所偵測到的事件。 如需詳細資訊和範例，請參閱 [Azure 媒體分析的動作偵測](media-services-motion-detection.md)。
### <a name="face-detector"></a>臉部偵測
透過使用臉部偵測，您便能偵測人臉及其表情，包括快樂、悲傷及驚喜。 這項服務有數個實用的產業應用程式 (將於稍後說明)，包括彙總並分析事件參與人員的反應。 如需詳細資訊和範例，請參閱 [Azure 媒體分析的臉部和情緒偵測](media-services-face-and-emotion-detection.md)。
### <a name="video-summarization"></a>影片摘要
視訊摘要可以協助您建立的較長的視訊摘要會自動從 hello 來源視訊中選取感興趣的程式碼片段。 這項功能時，您想要 tooprovide 哪些 tooexpect 長的視訊中的快速概觀。 如需詳細的資訊和範例，請參閱[toocreate 視訊摘要時，使用 Azure Media 視訊縮圖](media-services-video-summarization.md)。
### <a name="optical-character-recognition"></a>光學字元辨識
Azure 媒體 OCR (光學字元辨識) 可讓您將影片檔中的文字內容轉換成可編輯、可搜尋的數位文字。 然後，您可以自動從您的媒體 hello 視訊訊號的 hello 擷取有意義的中繼資料。
### <a name="scalable-face-redaction"></a>可調整式臉部修訂
Azure 媒體 Redactor 是提供可擴充的字體 redaction hello 雲端中的媒體分析媒體處理器。 藉由使用朝 redaction，您可以修改您的視訊 tooblur 字體的所選的個人。 您可能想 toouse hello 朝 redaction 新聞媒體或服務時牽涉到公共安全。 幾分鐘的影片，其中包含多個字型都會小時 tooredact 以手動方式，但使用這項服務，朝 redaction 需幾個簡單的步驟。 如需詳細資訊，請參閱 hello [Redact 使用 Azure 媒體分析字體](media-services-face-redaction.md)發行項。

## <a name="common-scenarios"></a>常見案例
媒體分析可協助組織和企業從影片中得到新的見解，並更有效地管理大量的影片內容。 以下是幾個案例︰

* **客服中心**。 社交媒體的 hello 問世，即使是使用客戶撥接中心仍可加速大量百分比的客戶服務的交易。 此音訊資料中的編碼是大量的客戶資訊可分析 tooachieve 較高的客戶滿意度。 組織可使用媒體索引器擷取文字，及建置搜尋索引與儀表板。 接著便可以從一般客訴、客訴來源及其他相關資料中獲取情報。
* **仲裁使用者產生的內容**。 從新聞媒體插座 toopolice 部門，許多組織必須面對大眾入口網站可接受使用者產生的媒體，例如視訊和影像。 hello 的內容的磁碟區可以因為 toounexpected 事件暴增。 在這些情況下，很難 tooconduct 有效手動的檢閱內容的適當性。 客戶可以依賴 hello 內容合適性服務 toofocus 適當的內容。
* **監視錄影**. Hello 與使用中的 IP 相機的成長是監視視訊的成長詳細目錄。 手動檢視監視視訊是時間密集而且容易產生 toohuman 錯誤。 媒體分析提供服務，例如影片偵測、 臉偵測和 Hyperlapse toomake hello 程序的檢視、 管理和建立衍生更容易。

## <a name="media-analytics-media-processors"></a>媒體分析媒體處理器
本章節列出 hello 媒體分析媒體處理器，並且示範如何 toouse.NET 或 REST tooget 媒體處理器 (MP) 物件。

### <a name="mp-names"></a>MP 名稱
* Azure 媒體索引器 2 預覽
* Azure Media Indexer
* Azure Media Hyperlapse
* Azure 媒體臉部偵測器
* Azure 媒體動作偵測器
* Azure 媒體視訊縮圖
* Azure 媒體 OCR

### <a name="net"></a>.NET
hello 遵循的 hello 函式會採用一個指定的管理組件名稱，並傳回的管理組件物件。

    static IMediaProcessor GetLatestMediaProcessorByName(string mediaProcessorName)
    {
        var processor = _context.MediaProcessors
            .Where(p => p.Name == mediaProcessorName)
            .ToList()
            .OrderBy(p => new Version(p.Version))
            .LastOrDefault();

        if (processor == null)
            throw new ArgumentException(string.Format("Unknown media processor",
                                                       mediaProcessorName));

        return processor;
    }


### <a name="rest"></a>REST
要求：

    GET https://media.windows.net/api/MediaProcessors()?$filter=Name%20eq%20'Azure%20Media%20OCR' HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer <token>
    x-ms-version: 2.12
    Host: media.windows.net

回應：

    . . .

    {  
       "odata.metadata":"https://media.windows.net/api/$metadata#MediaProcessors",
       "value":[  
          {  
             "Id":"nb:mpid:UUID:074c3899-d9fb-448f-9ae1-4ebcbe633056",
             "Description":"Azure Media OCR",
             "Name":"Azure Media OCR",
             "Sku":"",
             "Vendor":"Microsoft",
             "Version":"1.1"
          }
       ]
    }

## <a name="demos"></a>示範
請參閱 [Azure 媒體分析示範](http://azuremedialabs.azurewebsites.net/demos/Analytics.html)。

## <a name="next-steps"></a>後續步驟
檢閱媒體服務學習路徑。

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>提供意見反應
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-articles"></a>相關文章
請參閱[媒體服務分析公告](https://azure.microsoft.com/blog/introducing-azure-media-analytics/)。

<!-- Images -->

[overview]: ./media/media-services-video-on-demand-workflow/media-services-video-on-demand.png
