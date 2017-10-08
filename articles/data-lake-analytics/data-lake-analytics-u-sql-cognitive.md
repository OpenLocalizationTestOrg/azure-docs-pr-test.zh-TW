---
title: "aaaUsing Azure Data Lake Analytics U-SQL 認知能力 |Microsoft 文件"
description: "了解如何 toouse hello 認知中的功能 U-SQL 智慧"
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: sukvg
editor: cgronlun
ms.assetid: 019c1d53-4e61-4cad-9b2c-7a60307cbe19
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/05/2016
ms.author: saveenr
ms.openlocfilehash: 2c9ac71f490e929070fa0e72b93c3ffdb1ab243b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-get-started-with-hello-cognitive-capabilities-of-u-sql"></a><span data-ttu-id="821a9-103">教學課程： 開始使用 U-SQL hello 認知功能</span><span class="sxs-lookup"><span data-stu-id="821a9-103">Tutorial: Get started with hello Cognitive capabilities of U-SQL</span></span>

<span data-ttu-id="821a9-104">U-SQL 認知功能可讓開發人員 toouse 智慧置於他們巨量資料的程式。</span><span class="sxs-lookup"><span data-stu-id="821a9-104">Cognitive capabilities for U-SQL enable developers toouse put intelligence in their big data programs.</span></span> <span data-ttu-id="821a9-105">hello 中簡單的整體程序：</span><span class="sxs-lookup"><span data-stu-id="821a9-105">hello overall process in simple:</span></span>

* <span data-ttu-id="821a9-106">Hello 參考組件陳述式 tooenable hello 認知功能用於 hello U-SQL 指令碼</span><span class="sxs-lookup"><span data-stu-id="821a9-106">Use hello REFERENCE ASSEMBLY statement tooenable hello cognitive features for hello U-SQL Script</span></span>
* <span data-ttu-id="821a9-107">呼叫 hello 處理作業 toouse hello 認知功能</span><span class="sxs-lookup"><span data-stu-id="821a9-107">Call hello PROCESS operation toouse hello Cognitive capabilities</span></span> 

## <a name="imaging-scenarios"></a><span data-ttu-id="821a9-108">影像案例</span><span class="sxs-lookup"><span data-stu-id="821a9-108">Imaging scenarios</span></span>

### <a name="example-image-tagging"></a><span data-ttu-id="821a9-109">範例：影像標記</span><span class="sxs-lookup"><span data-stu-id="821a9-109">Example: Image tagging</span></span>

<span data-ttu-id="821a9-110">下列範例中的 hello 顯示 hello 影像處理功能 toodetect 物件映像中的端對端使用。</span><span class="sxs-lookup"><span data-stu-id="821a9-110">hello following example shows an end-to-end use of hello imaging capabilities toodetect objects in images.</span></span>

    REFERENCE ASSEMBLY ImageCommon;
    REFERENCE ASSEMBLY FaceSdk;
    REFERENCE ASSEMBLY ImageEmotion;
    REFERENCE ASSEMBLY ImageTagging;
    REFERENCE ASSEMBLY ImageOcr;

    @imgs =
        EXTRACT FileName string, ImgData byte[]
        FROM @"/images/{FileName:*}.jpg"
        USING new Cognition.Vision.ImageExtractor();

    // Extract hello number of objects on each image and tag them 
    @objects =
        PROCESS @imgs 
        PRODUCE FileName,
                NumObjects int,
                Tags string
        READONLY FileName
        USING new Cognition.Vision.ImageTagger();


### <a name="extract-emotions-from-human-faces"></a><span data-ttu-id="821a9-111">從人臉擷取表情</span><span class="sxs-lookup"><span data-stu-id="821a9-111">Extract emotions from human faces</span></span> 

    @emotions =
        PROCESS @imgs
        PRODUCE FileName string,
                NumFaces int,
                Emotion string
        READONLY FileName
        USING new Cognition.Vision.EmotionAnalyzer();

### <a name="estimate-age-and-gender-for-human-faces"></a><span data-ttu-id="821a9-112">估計人臉的年齡和性別</span><span class="sxs-lookup"><span data-stu-id="821a9-112">Estimate age and gender for human faces</span></span>

    @faces = 
            PROCESS @imgs
            PRODUCE FileName,
                    NumFaces int,
                    FaceAge string,
                    FaceGender string
            READONLY FileName
            USING new Cognition.Vision.FaceDetector();

### <a name="detect-text-in-images-ocr"></a><span data-ttu-id="821a9-113">讀取影像中的文字 (OCR)</span><span class="sxs-lookup"><span data-stu-id="821a9-113">Detect text in Images (OCR)</span></span>

    @ocrs =
            PROCESS @imgs
            PRODUCE FileName,
                    Text string
            READONLY FileName
            USING new Cognition.Vision.OcrExtractor();

## <a name="text-scenarios"></a><span data-ttu-id="821a9-114">文字案例</span><span class="sxs-lookup"><span data-stu-id="821a9-114">Text scenarios</span></span>

### <a name="input-data"></a><span data-ttu-id="821a9-115">輸入資料</span><span class="sxs-lookup"><span data-stu-id="821a9-115">Input data</span></span>

<span data-ttu-id="821a9-116">假設我們的輸入是托爾斯泰的「戰爭與和平」(War and Peace)。</span><span class="sxs-lookup"><span data-stu-id="821a9-116">Assume that we have an input that consists of “War and Peace” by Leo Tolstoy.</span></span>

    REFERENCE ASSEMBLY [TextCommon];
    REFERENCE ASSEMBLY [TextSentiment];
    REFERENCE ASSEMBLY [TextKeyPhrase];

    @WarAndPeace =
        EXTRACT No int,
                Year string,
                Book string,
                Chapter string,
                Text string
        FROM @"/usqlext/samples/cognition/war_and_peace.csv"
        USING Extractors.Csv();

### <a name="extract-key-phrases-for-each-paragraph"></a><span data-ttu-id="821a9-117">擷取每個段落的關鍵片語</span><span class="sxs-lookup"><span data-stu-id="821a9-117">Extract key phrases for each paragraph</span></span>

    @keyphrase =
        PROCESS @WarAndPeace
        PRODUCE No,
                Year,
                Book,
                Chapter,
                Text,
                KeyPhrase string
        READONLY No,
                Year,
                Book,
                Chapter,
                Text
        USING new Cognition.Text.KeyPhraseExtractor();

    // Tokenize hello key phrases.
    @kpsplits =
        SELECT No,
            Year,
            Book,
            Chapter,
            Text,
            T.KeyPhrase
        FROM @keyphrase
            CROSS APPLY
                new Cognition.Text.Splitter("KeyPhrase") AS T(KeyPhrase);
    
### <a name="perform-sentiment-analysis-on-each-paragraph"></a><span data-ttu-id="821a9-118">對每個段落執行情感分析</span><span class="sxs-lookup"><span data-stu-id="821a9-118">Perform sentiment analysis on each paragraph</span></span>

    @sentiment =
        PROCESS @WarAndPeace
        PRODUCE No,
                Year,
                Book,
                Chapter,
                Text,
                Sentiment string,
                Conf double
        READONLY No,
                Year,
                Book,
                Chapter,
                Text
        USING new Cognition.Text.SentimentAnalyzer(true);

