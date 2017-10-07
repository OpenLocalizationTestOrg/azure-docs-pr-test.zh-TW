---
title: "aaaAnalyze 程式媒體，請使用 hello Azure 入口網站 |Microsoft 文件"
description: "本主題討論如何 tooprocess 媒體分析媒體處理器 (Mp) 使用媒體 hello Azure 入口網站。"
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 18213fc1-74f5-4074-a32b-02846fe90601
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: juliako
ms.openlocfilehash: d549c0315cd58c3771420379316b4f2ad3c2cea6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-your-media-using-hello-azure-portal"></a>分析您的媒體使用 hello Azure 入口網站
> [!NOTE]
> toocomplete 本教學課程中，您需要 Azure 帳戶。 如需詳細資料，請參閱 [Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。 
> 
> 

## <a name="overview"></a>概觀
Azure Media Services 分析是語音和願景元件 （企業規模、 相容性、 安全性和全球化） 可讓它更容易組織和企業 tooderive 可執行的洞察力的視訊檔案的集合。 如需更為詳細的 Azure 媒體服務分析概觀，請參閱[此主題](media-services-analytics-overview.md)。 

本主題討論如何 tooprocess 媒體分析媒體處理器 (Mp) 使用媒體 hello Azure 入口網站。 媒體分析 MP 會產生 MP4 檔案或 JSON 檔案。 如果媒體處理器所產生的 MP4 檔案，您可以漸進式下載 hello 檔案。 如果媒體處理器所產生的 JSON 檔案，您可以從 hello Azure blob 儲存體下載 hello 檔案。 

## <a name="choose-an-asset-that-you-want-tooanalyze"></a>選擇 資產的 tooanalyze
1. 在 hello [Azure 入口網站](https://portal.azure.com/)，選取您的 Azure Media Services 帳戶。
2. 在 hello**設定**視窗中，選取**資產**。  
   .
    ![分析影片](./media/media-services-portal-analyze/media-services-portal-analyze001.png)
3. 您想要選取 hello 資產 tooanalyze 並按下 hello**分析** 按鈕。
   
    ![分析影片](./media/media-services-portal-analyze/media-services-portal-analyze002.png)
4. 在 hello**媒體分析程序媒體資產**視窗中，選取 hello 處理器。 
   
    hello 文章的 hello 其餘部分說明原因和方式 toouse 每個處理器。 
5. 按**建立**toohello 啟動工作。

## <a name="azure-media-indexer"></a>Azure Media Indexer
hello **Azure Media Indexer**媒體處理器可讓您 toomake 媒體檔案和內容可搜尋，以及產生已關閉隱藏式輔助字幕追蹤。 本節會提供一些可為此 MP 指定之選項的詳細資料。

![分析影片](./media/media-services-portal-analyze/media-services-portal-analyze003.png)

### <a name="language"></a>語言
hello 自然語言 toobe 辨識 hello 多媒體檔案中。 例如，英文或西班牙文。 

### <a name="captions"></a>標題
您可以選擇要從內容產生的標題格式。 索引作業可以產生隱藏式的字幕檔案在 hello 下列格式：  

* **SAMI**
* **TTML**
* **WebVTT**

已關閉的字幕 (CC) 檔案，這些格式可以是使用的 toomake 音訊和視訊檔案存取 toopeople 聽覺時。

### <a name="aib-file"></a>AIB 檔案
如果您將像是 toogenerate hello 音訊索引 Blob 檔案搭配使用 hello 自訂 SQL Server IFilter，請選取此選項。 如需詳細資訊，請參閱 [此部落格](https://azure.microsoft.com/blog/using-aib-files-with-azure-media-indexer-and-sql-server/) 。

### <a name="keywords"></a>關鍵字
如果您想要 toogenerate 關鍵字 XML 檔案，請選取此選項。 這個檔案包含從 hello 語音內容，擷取使用頻率與偏移的資訊的關鍵字。

### <a name="job-name"></a>作業名稱
易記名稱，可讓您識別 hello 工作。 [這](media-services-portal-check-job-progress.md)文章說明如何監視 hello 作業的進度。 

### <a name="output-file"></a>輸出檔案
易記名稱，可讓您識別 hello 輸出的內容。 

## <a name="azure-media-hyperlapse"></a>Azure Media Hyperlapse
Azure Media Hyperlapse 是能夠利用第一人稱視角或運動攝影的內容，來建立流暢縮時影片的 MP。  如需詳細資訊，請參閱[此主題](media-services-hyperlapse-content.md)。 本節會提供一些可為此 MP 指定之選項的詳細資料。

![分析影片](./media/media-services-portal-analyze/media-services-portal-analyze004.png)

### <a name="speed"></a>速度
指定哪些 toospeed 向上 hello 輸入視訊 hello 速度。 hello 輸出是 hello 輸入視訊穩定和時間屆滿轉譯。

### <a name="job-name"></a>作業名稱
易記名稱，可讓您識別 hello 工作。 [這](media-services-portal-check-job-progress.md)文章說明如何監視 hello 作業的進度。 

### <a name="output-file"></a>輸出檔案
易記名稱，可讓您識別 hello 輸出的內容。 

## <a name="azure-media-face-detector"></a>Azure 媒體臉部偵測器
hello **Azure 媒體正面偵測器**媒體處理器 (MP) 可讓您 toocount、 軌跡的移動，即使量測計的對象參與以及透過臉部表情的反應。 此服務包含兩個功能： 

* **臉部偵測**
  
    臉部偵測能夠找出並追蹤影片中的臉部。 多個字型可以偵測到且後續追蹤與 hello 時間和位置傳回中繼資料中的 JSON 檔案中，移動。 在追蹤時，它就會嘗試 toogive 一致的識別碼 toohello 相同面臨 hello 人員四處移動在畫面上，即使它們受到阻擋或簡短保留 hello 框架時。
  
  > [!NOTE]
  > 此服務並不會執行臉部辨識。 個人離開 hello 框架，或會變成受到阻擋的時間太長時，會指定新的識別碼，就會傳回。
  > 
  > 
* **情緒偵測**
  
    情緒偵測作業屬於選擇性元件的 hello 分析多個情感屬性傳回 hello 字體偵測到，包括快樂、 sadness、 擔心、 anger，以及更多的臉偵測媒體處理器。 

![分析影片](./media/media-services-portal-analyze/media-services-portal-analyze005.png)

### <a name="detection-mode"></a>偵測模式
Hello 處理器，可以使用其中一個 hello 下列模式：

* 臉部偵測
* 每一人臉情緒偵測
* 彙總情緒偵測

### <a name="job-name"></a>作業名稱
易記名稱，可讓您識別 hello 工作。 [這](media-services-portal-check-job-progress.md)文章說明如何監視 hello 作業的進度。 

### <a name="output-file"></a>輸出檔案
易記名稱，可讓您識別 hello 輸出的內容。 

## <a name="azure-media-motion-detector"></a>Azure 媒體動作偵測器
hello **Azure 媒體動作偵測器**媒體處理器 (MP) 可讓您 tooefficiently 識別有興趣，否則冗長且較為簡單的視訊中的章節。 影片偵測可用靜態攝影機錄影畫面 tooidentify 部分的 hello 視訊動作發生的位置。 它會產生包含時間戳記與 hello 週框 hello 事件發生的位置 （地區） 的中繼資料的 JSON 檔案。

針對安全性視訊摘要，此技術是無法 toocategorize 移動到相關的事件，例如陰影和光源處理變更的誤判。 可以讓您從相機摘要 toogenerate 安全性警示，沒有與無止盡不相關的事件，同時會無法 tooextract 分鐘的時間很長的監視視訊從感興趣的垃圾信件。

![分析影片](./media/media-services-portal-analyze/media-services-portal-analyze006.png)

## <a name="azure-media-video-thumbnails"></a>Azure 媒體視訊縮圖
此處理器可協助您建立自動從 hello 來源視訊中選取感興趣的程式碼片段的較長的視訊摘要。 當您想 tooprovide 哪些 tooexpect 長的視訊中的快速概觀，這非常有用。 如需詳細的資訊和範例，請參閱[使用 Azure Media 視訊縮圖 tooCreate 視訊摘要](media-services-video-summarization.md)

![分析影片](./media/media-services-portal-analyze/media-services-portal-analyze008.png)

### <a name="job-name"></a>作業名稱
易記名稱，可讓您識別 hello 工作。 [這](media-services-portal-check-job-progress.md)文章說明如何監視 hello 作業的進度。 

### <a name="output-file"></a>輸出檔案
易記名稱，可讓您識別 hello 輸出的內容。 

## <a name="next-steps"></a>後續步驟
檢視媒體服務學習路徑。

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>提供意見反應
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

