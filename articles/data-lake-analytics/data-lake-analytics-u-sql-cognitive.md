---
title: "使用 Azure Data Lake Analytics 中的 U-SQL 辨識功能| Microsoft Docs"
description: "了解如何使用 U-SQL 中辨識功能的智慧"
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
ms.openlocfilehash: f77329f9838d6e824afa7234de90f62257a004de
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-get-started-with-the-cognitive-capabilities-of-u-sql"></a><span data-ttu-id="8b939-103">教學課程︰開始使用 U-SQL 的辨識功能</span><span class="sxs-lookup"><span data-stu-id="8b939-103">Tutorial: Get started with the Cognitive capabilities of U-SQL</span></span>

<span data-ttu-id="8b939-104">U-SQL 的辨識功能讓開發人員可以在其公司的巨量資料程式中使用 put 智慧。</span><span class="sxs-lookup"><span data-stu-id="8b939-104">Cognitive capabilities for U-SQL enable developers to use put intelligence in their big data programs.</span></span> <span data-ttu-id="8b939-105">整個程序簡述如下︰</span><span class="sxs-lookup"><span data-stu-id="8b939-105">The overall process in simple:</span></span>

* <span data-ttu-id="8b939-106">使用 REFERENCE ASSEMBLY 陳述式啟用 U-SQL 指令碼的辨識功能</span><span class="sxs-lookup"><span data-stu-id="8b939-106">Use the REFERENCE ASSEMBLY statement to enable the cognitive features for the U-SQL Script</span></span>
* <span data-ttu-id="8b939-107">呼叫 PROCESS 作業來使用辨識功能</span><span class="sxs-lookup"><span data-stu-id="8b939-107">Call the PROCESS operation to use the Cognitive capabilities</span></span> 

## <a name="imaging-scenarios"></a><span data-ttu-id="8b939-108">影像案例</span><span class="sxs-lookup"><span data-stu-id="8b939-108">Imaging scenarios</span></span>

### <a name="example-image-tagging"></a><span data-ttu-id="8b939-109">範例：影像標記</span><span class="sxs-lookup"><span data-stu-id="8b939-109">Example: Image tagging</span></span>

<span data-ttu-id="8b939-110">下列範例顯示以端對端使用影像功能來偵測影像中的物件。</span><span class="sxs-lookup"><span data-stu-id="8b939-110">The following example shows an end-to-end use of the imaging capabilities to detect objects in images.</span></span>

    REFERENCE ASSEMBLY ImageCommon;
    REFERENCE ASSEMBLY FaceSdk;
    REFERENCE ASSEMBLY ImageEmotion;
    REFERENCE ASSEMBLY ImageTagging;
    REFERENCE ASSEMBLY ImageOcr;

    @imgs =
        EXTRACT FileName string, ImgData byte[]
        FROM @"/images/{FileName:*}.jpg"
        USING new Cognition.Vision.ImageExtractor();

    // Extract the number of objects on each image and tag them 
    @objects =
        PROCESS @imgs 
        PRODUCE FileName,
                NumObjects int,
                Tags string
        READONLY FileName
        USING new Cognition.Vision.ImageTagger();


### <a name="extract-emotions-from-human-faces"></a><span data-ttu-id="8b939-111">從人臉擷取表情</span><span class="sxs-lookup"><span data-stu-id="8b939-111">Extract emotions from human faces</span></span> 

    @emotions =
        PROCESS @imgs
        PRODUCE FileName string,
                NumFaces int,
                Emotion string
        READONLY FileName
        USING new Cognition.Vision.EmotionAnalyzer();

### <a name="estimate-age-and-gender-for-human-faces"></a><span data-ttu-id="8b939-112">估計人臉的年齡和性別</span><span class="sxs-lookup"><span data-stu-id="8b939-112">Estimate age and gender for human faces</span></span>

    @faces = 
            PROCESS @imgs
            PRODUCE FileName,
                    NumFaces int,
                    FaceAge string,
                    FaceGender string
            READONLY FileName
            USING new Cognition.Vision.FaceDetector();

### <a name="detect-text-in-images-ocr"></a><span data-ttu-id="8b939-113">讀取影像中的文字 (OCR)</span><span class="sxs-lookup"><span data-stu-id="8b939-113">Detect text in Images (OCR)</span></span>

    @ocrs =
            PROCESS @imgs
            PRODUCE FileName,
                    Text string
            READONLY FileName
            USING new Cognition.Vision.OcrExtractor();

## <a name="text-scenarios"></a><span data-ttu-id="8b939-114">文字案例</span><span class="sxs-lookup"><span data-stu-id="8b939-114">Text scenarios</span></span>

### <a name="input-data"></a><span data-ttu-id="8b939-115">輸入資料</span><span class="sxs-lookup"><span data-stu-id="8b939-115">Input data</span></span>

<span data-ttu-id="8b939-116">假設我們的輸入是托爾斯泰的「戰爭與和平」(War and Peace)。</span><span class="sxs-lookup"><span data-stu-id="8b939-116">Assume that we have an input that consists of “War and Peace” by Leo Tolstoy.</span></span>

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

### <a name="extract-key-phrases-for-each-paragraph"></a><span data-ttu-id="8b939-117">擷取每個段落的關鍵片語</span><span class="sxs-lookup"><span data-stu-id="8b939-117">Extract key phrases for each paragraph</span></span>

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

    // Tokenize the key phrases.
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
    
### <a name="perform-sentiment-analysis-on-each-paragraph"></a><span data-ttu-id="8b939-118">對每個段落執行情感分析</span><span class="sxs-lookup"><span data-stu-id="8b939-118">Perform sentiment analysis on each paragraph</span></span>

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

