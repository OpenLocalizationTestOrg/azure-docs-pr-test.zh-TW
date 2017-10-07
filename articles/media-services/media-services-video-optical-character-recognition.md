---
title: "Azure 媒體分析 ocr aaaDigitize 文字 |Microsoft 文件"
description: "Azure 媒體分析 OCR （光學字元辨識） 可讓您 tooconvert 文字內容中的視訊檔案為可編輯，搜尋數位文字。  這可讓您 tooautomate hello 擷取有意義的中繼資料從您的媒體 hello 視訊訊號。"
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 307c196e-3a50-4f4b-b982-51585448ffc6
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/31/2017
ms.author: juliako
ms.openlocfilehash: 0476c3ba3942b2c5182a34a429909adbf5c75ac9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-media-analytics-tooconvert-text-content-in-video-files-into-digital-text"></a><span data-ttu-id="966e9-104">視訊檔案中，使用 Azure 媒體分析 tooconvert 文字內容，到數位的文字</span><span class="sxs-lookup"><span data-stu-id="966e9-104">Use Azure Media Analytics tooconvert text content in video files into digital text</span></span>
## <a name="overview"></a><span data-ttu-id="966e9-105">概觀</span><span class="sxs-lookup"><span data-stu-id="966e9-105">Overview</span></span>
<span data-ttu-id="966e9-106">如果您需要從視訊檔案的內容 tooextract 文字，並產生可編輯的可搜尋數位文字，您應該使用 Azure 媒體分析 OCR （光學字元辨識）。</span><span class="sxs-lookup"><span data-stu-id="966e9-106">If you need tooextract text content from your video files and generate an editable, searchable digital text, you should use Azure Media Analytics OCR (optical character recognition).</span></span> <span data-ttu-id="966e9-107">此 Azure 媒體處理器會偵測視訊檔案的文字內容並產生文字檔案，以供您使用。</span><span class="sxs-lookup"><span data-stu-id="966e9-107">This Azure Media Processor detects text content in your video files and generates text files for your use.</span></span> <span data-ttu-id="966e9-108">OCR 可讓您 tooautomate hello 的有意義的中繼資料中擷取媒體的 hello 視訊訊號。</span><span class="sxs-lookup"><span data-stu-id="966e9-108">OCR enables you tooautomate hello extraction of meaningful metadata from hello video signal of your media.</span></span>

<span data-ttu-id="966e9-109">搭配使用搜尋引擎，您可以輕鬆地索引時您的媒體依文字、 與增強 hello 發現您的內容。</span><span class="sxs-lookup"><span data-stu-id="966e9-109">When used in conjunction with a search engine, you can easily index your media by text, and enhance hello discoverability of your content.</span></span> <span data-ttu-id="966e9-110">這在具有大量文字的視訊 (例如視訊錄製或投影片簡報的螢幕擷取) 中非常實用。</span><span class="sxs-lookup"><span data-stu-id="966e9-110">This is extremely useful in highly textual video, like a video recording or screen-capture of a slideshow presentation.</span></span> <span data-ttu-id="966e9-111">hello Azure OCR 媒體處理器最適合用於數位文字。</span><span class="sxs-lookup"><span data-stu-id="966e9-111">hello Azure OCR Media Processor is optimized for digital text.</span></span>

<span data-ttu-id="966e9-112">hello **Azure 媒體 OCR**媒體處理器目前為預覽狀態。</span><span class="sxs-lookup"><span data-stu-id="966e9-112">hello **Azure Media OCR** media processor is currently in Preview.</span></span>

<span data-ttu-id="966e9-113">本主題詳細說明有關**Azure 媒體 OCR** ，並示範如何 toouse 使用 Media Services SDK for.NET。</span><span class="sxs-lookup"><span data-stu-id="966e9-113">This topic gives details about  **Azure Media OCR** and shows how toouse it with Media Services SDK for .NET.</span></span> <span data-ttu-id="966e9-114">如需詳細資訊和範例，請參閱 [這篇部落格](https://azure.microsoft.com/blog/announcing-video-ocr-public-preview-new-config/)。</span><span class="sxs-lookup"><span data-stu-id="966e9-114">For additional information and examples, see [this blog](https://azure.microsoft.com/blog/announcing-video-ocr-public-preview-new-config/).</span></span>

## <a name="ocr-input-files"></a><span data-ttu-id="966e9-115">OCR 輸入檔案</span><span class="sxs-lookup"><span data-stu-id="966e9-115">OCR input files</span></span>
<span data-ttu-id="966e9-116">影片檔案。</span><span class="sxs-lookup"><span data-stu-id="966e9-116">Video files.</span></span> <span data-ttu-id="966e9-117">目前支援下列格式的 hello: MP4、 MOV、 和 WMV。</span><span class="sxs-lookup"><span data-stu-id="966e9-117">Currently, hello following formats are supported: MP4, MOV, and WMV.</span></span>

## <a name="task-configuration"></a><span data-ttu-id="966e9-118">工作組態</span><span class="sxs-lookup"><span data-stu-id="966e9-118">Task configuration</span></span>
<span data-ttu-id="966e9-119">工作組態 (預設)。</span><span class="sxs-lookup"><span data-stu-id="966e9-119">Task configuration (preset).</span></span> <span data-ttu-id="966e9-120">使用 **Azure 媒體 OCR** 建立工作時，您必須使用 JSON 或 XML 來指定組態預設。</span><span class="sxs-lookup"><span data-stu-id="966e9-120">When creating a task with **Azure Media OCR**, you must specify a configuration preset using JSON  or XML.</span></span> 

>[!NOTE]
><span data-ttu-id="966e9-121">hello OCR 引擎才會與最小 40 像素 toomaximum 32000 像素的影像區域，做為有效的輸入，在這兩個高度/寬度。</span><span class="sxs-lookup"><span data-stu-id="966e9-121">hello OCR engine only takes an image region with minimum 40 pixels toomaximum 32000 pixels as a valid input in both height/width.</span></span>
>

### <a name="attribute-descriptions"></a><span data-ttu-id="966e9-122">屬性描述</span><span class="sxs-lookup"><span data-stu-id="966e9-122">Attribute descriptions</span></span>
| <span data-ttu-id="966e9-123">屬性名稱</span><span class="sxs-lookup"><span data-stu-id="966e9-123">Attribute name</span></span> | <span data-ttu-id="966e9-124">說明</span><span class="sxs-lookup"><span data-stu-id="966e9-124">Description</span></span> |
| --- | --- |
|<span data-ttu-id="966e9-125">AdvancedOutput</span><span class="sxs-lookup"><span data-stu-id="966e9-125">AdvancedOutput</span></span>| <span data-ttu-id="966e9-126">如果您設定 AdvancedOutput tootrue，hello JSON 輸出會包含位置資料的每個單字 （在加法 toophrases 和區域）。</span><span class="sxs-lookup"><span data-stu-id="966e9-126">If you set AdvancedOutput tootrue, hello JSON output will contain positional data for every single word (in addition toophrases and regions).</span></span> <span data-ttu-id="966e9-127">如果您不想 toosee 這些詳細資料，設定 hello 旗標 toofalse。</span><span class="sxs-lookup"><span data-stu-id="966e9-127">If you do not want toosee these details, set hello flag toofalse.</span></span> <span data-ttu-id="966e9-128">hello 預設值為 false。</span><span class="sxs-lookup"><span data-stu-id="966e9-128">hello default value is false.</span></span> <span data-ttu-id="966e9-129">如需詳細資訊，請參閱 [此部落格](https://azure.microsoft.com/blog/azure-media-ocr-simplified-output/)。</span><span class="sxs-lookup"><span data-stu-id="966e9-129">For more information, see [this blog](https://azure.microsoft.com/blog/azure-media-ocr-simplified-output/).</span></span>|
| <span data-ttu-id="966e9-130">語言</span><span class="sxs-lookup"><span data-stu-id="966e9-130">Language</span></span> |<span data-ttu-id="966e9-131">（選擇性） 描述文字的哪些 toolook hello 語言。</span><span class="sxs-lookup"><span data-stu-id="966e9-131">(optional) describes hello language of text for which toolook.</span></span> <span data-ttu-id="966e9-132">Hello 下列其中一種： 自動偵測 （預設值）、 阿拉伯文、 ChineseSimplified、 ChineseTraditional、 捷克文丹麥文、 荷蘭文、 英文、 芬蘭文、 法文、 德文、 希臘文、 匈牙利文、 義大利文、 日文、 韓文、 挪威文、 波蘭文、 葡萄牙文、 羅馬尼亞文、 俄文SerbianCyrillic、 SerbianLatin、 斯洛伐克文、 西班牙文、 瑞典文、 土耳其文。</span><span class="sxs-lookup"><span data-stu-id="966e9-132">One of hello following: AutoDetect (default), Arabic, ChineseSimplified, ChineseTraditional, Czech Danish, Dutch, English, Finnish, French, German,  Greek, Hungarian, Italian, Japanese, Korean, Norwegian, Polish, Portuguese, Romanian, Russian, SerbianCyrillic, SerbianLatin, Slovak, Spanish, Swedish, Turkish.</span></span> |
| <span data-ttu-id="966e9-133">TextOrientation</span><span class="sxs-lookup"><span data-stu-id="966e9-133">TextOrientation</span></span> |<span data-ttu-id="966e9-134">（選擇性） 描述 hello 哪些 toolook 文字方向。</span><span class="sxs-lookup"><span data-stu-id="966e9-134">(optional) describes hello orientation of text for which toolook.</span></span>  <span data-ttu-id="966e9-135">「 左 」 表示 hello 的所有字母上方所指朝向 hello 左邊。</span><span class="sxs-lookup"><span data-stu-id="966e9-135">"Left" means that hello top of all letters are pointed towards hello left.</span></span>  <span data-ttu-id="966e9-136">預設文字 (像是可在書本中找到的文字) 的方向為 "Up"。</span><span class="sxs-lookup"><span data-stu-id="966e9-136">Default text (like that which can be found in a book) can be called "Up" oriented.</span></span>  <span data-ttu-id="966e9-137">Hello 下列其中一種： 自動偵測 （預設值），最多、 右邊、 向下、 左。</span><span class="sxs-lookup"><span data-stu-id="966e9-137">One of hello following: AutoDetect (default), Up, Right, Down, Left.</span></span> |
| <span data-ttu-id="966e9-138">TimeInterval</span><span class="sxs-lookup"><span data-stu-id="966e9-138">TimeInterval</span></span> |<span data-ttu-id="966e9-139">（選擇性） 描述 hello 取樣率。</span><span class="sxs-lookup"><span data-stu-id="966e9-139">(optional) describes hello sampling rate.</span></span>  <span data-ttu-id="966e9-140">預設值為每 1/2 秒。</span><span class="sxs-lookup"><span data-stu-id="966e9-140">Default is every 1/2 second.</span></span><br/><span data-ttu-id="966e9-141">JSON 格式 – HH:mm:ss.SSS (預設值 00:00:00.500)</span><span class="sxs-lookup"><span data-stu-id="966e9-141">JSON format – HH:mm:ss.SSS (default 00:00:00.500)</span></span><br/><span data-ttu-id="966e9-142">XML 格式 – W3C XSD 持續時間基本型別 (預設值 PT0.5)</span><span class="sxs-lookup"><span data-stu-id="966e9-142">XML format – W3C XSD duration primitive (default PT0.5)</span></span> |
| <span data-ttu-id="966e9-143">DetectRegions</span><span class="sxs-lookup"><span data-stu-id="966e9-143">DetectRegions</span></span> |<span data-ttu-id="966e9-144">（選擇性）指定區域內 hello 視訊畫面格 toodetect 文字 DetectRegion 物件的陣列。</span><span class="sxs-lookup"><span data-stu-id="966e9-144">(optional) An array of DetectRegion objects specifying regions within hello video frame in which toodetect text.</span></span><br/><span data-ttu-id="966e9-145">DetectRegion 物件是由下列四個整數值的 hello:</span><span class="sxs-lookup"><span data-stu-id="966e9-145">A DetectRegion object is made of hello following four integer values:</span></span><br/><span data-ttu-id="966e9-146">左 – 從 hello 左邊界的像素為單位</span><span class="sxs-lookup"><span data-stu-id="966e9-146">Left – pixels from hello left-margin</span></span><br/><span data-ttu-id="966e9-147">Top – 從 hello 的上邊界的像素為單位</span><span class="sxs-lookup"><span data-stu-id="966e9-147">Top – pixels from hello top-margin</span></span><br/><span data-ttu-id="966e9-148">寬度-像素為單位的 hello 區域的寬度</span><span class="sxs-lookup"><span data-stu-id="966e9-148">Width – width of hello region in pixels</span></span><br/><span data-ttu-id="966e9-149">高度-像素為單位的 hello 區域的高度</span><span class="sxs-lookup"><span data-stu-id="966e9-149">Height – height of hello region in pixels</span></span> |

#### <a name="json-preset-example"></a><span data-ttu-id="966e9-150">JSON 預設範例</span><span class="sxs-lookup"><span data-stu-id="966e9-150">JSON preset example</span></span>

    {
        "Version":1.0, 
        "Options": 
        {
            "AdvancedOutput":"true",
            "Language":"English", 
            "TimeInterval":"00:00:01.5",
            "TextOrientation":"Up",
            "DetectRegions": [
                    {
                       "Left": 10,
                       "Top": 10,
                       "Width": 100,
                       "Height": 50
                    }
             ]
        }
    }


#### <a name="xml-preset-example"></a><span data-ttu-id="966e9-151">XML 預設範例</span><span class="sxs-lookup"><span data-stu-id="966e9-151">XML preset example</span></span>
    <?xml version=""1.0"" encoding=""utf-16""?>
    <VideoOcrPreset xmlns:xsi=""http://www.w3.org/2001/XMLSchema-instance"" xmlns:xsd=""http://www.w3.org/2001/XMLSchema"" Version=""1.0"" xmlns=""http://www.windowsazure.com/media/encoding/Preset/2014/03"">
      <Options>
         <AdvancedOutput>true</AdvancedOutput>
         <Language>English</Language>
         <TimeInterval>PT1.5S</TimeInterval>
         <DetectRegions>
             <DetectRegion>
                   <Left>10</Left>
                   <Top>10</Top>
                   <Width>100</Width>
                   <Height>50</Height>
            </DetectRegion>
       </DetectRegions>
       <TextOrientation>Up</TextOrientation>
      </Options>
    </VideoOcrPreset>

## <a name="ocr-output-files"></a><span data-ttu-id="966e9-152">OCR 輸出檔案</span><span class="sxs-lookup"><span data-stu-id="966e9-152">OCR output files</span></span>
<span data-ttu-id="966e9-153">hello OCR 媒體處理器的 hello 輸出是 JSON 檔案。</span><span class="sxs-lookup"><span data-stu-id="966e9-153">hello output of hello OCR media processor is a JSON file.</span></span>

### <a name="elements-of-hello-output-json-file"></a><span data-ttu-id="966e9-154">Hello 輸出 JSON 檔案的項目</span><span class="sxs-lookup"><span data-stu-id="966e9-154">Elements of hello output JSON file</span></span>
<span data-ttu-id="966e9-155">hello 視訊 OCR 輸出提供在視訊中找到的 hello 字元時間分割資料。</span><span class="sxs-lookup"><span data-stu-id="966e9-155">hello Video OCR output provides time-segmented data on hello characters found in your video.</span></span>  <span data-ttu-id="966e9-156">您可以使用的語言或 toohone 中方向等屬性完全 hello 字，您有興趣分析。</span><span class="sxs-lookup"><span data-stu-id="966e9-156">You can use attributes such as language or orientation toohone-in on exactly hello words that you are interested in analyzing.</span></span> 

<span data-ttu-id="966e9-157">hello 輸出內容包含下列屬性的 hello:</span><span class="sxs-lookup"><span data-stu-id="966e9-157">hello output contains hello following attributes:</span></span>

| <span data-ttu-id="966e9-158">元素</span><span class="sxs-lookup"><span data-stu-id="966e9-158">Element</span></span> | <span data-ttu-id="966e9-159">說明</span><span class="sxs-lookup"><span data-stu-id="966e9-159">Description</span></span> |
| --- | --- |
| <span data-ttu-id="966e9-160">時幅</span><span class="sxs-lookup"><span data-stu-id="966e9-160">Timescale</span></span> |<span data-ttu-id="966e9-161">hello 視訊的每秒 「 滴答 」</span><span class="sxs-lookup"><span data-stu-id="966e9-161">"ticks" per second of hello video</span></span> |
| <span data-ttu-id="966e9-162">Offset</span><span class="sxs-lookup"><span data-stu-id="966e9-162">Offset</span></span> |<span data-ttu-id="966e9-163">時間戳記的時間位移。</span><span class="sxs-lookup"><span data-stu-id="966e9-163">time offset for timestamps.</span></span> <span data-ttu-id="966e9-164">在版本 1.0 的影片 API 中，這永遠會是 0。</span><span class="sxs-lookup"><span data-stu-id="966e9-164">In version 1.0 of Video APIs, this will always be 0.</span></span> |
| <span data-ttu-id="966e9-165">畫面播放速率</span><span class="sxs-lookup"><span data-stu-id="966e9-165">Framerate</span></span> |<span data-ttu-id="966e9-166">每秒的 hello 視訊畫面格</span><span class="sxs-lookup"><span data-stu-id="966e9-166">Frames per second of hello video</span></span> |
| <span data-ttu-id="966e9-167">width</span><span class="sxs-lookup"><span data-stu-id="966e9-167">width</span></span> |<span data-ttu-id="966e9-168">hello 視訊像素為單位的寬度</span><span class="sxs-lookup"><span data-stu-id="966e9-168">width of hello video in pixels</span></span> |
| <span data-ttu-id="966e9-169">height</span><span class="sxs-lookup"><span data-stu-id="966e9-169">height</span></span> |<span data-ttu-id="966e9-170">hello 視訊像素為單位的高度</span><span class="sxs-lookup"><span data-stu-id="966e9-170">height of hello video in pixels</span></span> |
| <span data-ttu-id="966e9-171">片段</span><span class="sxs-lookup"><span data-stu-id="966e9-171">Fragments</span></span> |<span data-ttu-id="966e9-172">以時間為基礎的中繼資料被截斷成哪一個 hello 視訊的區塊的陣列</span><span class="sxs-lookup"><span data-stu-id="966e9-172">array of time-based chunks of video into which hello metadata is chunked</span></span> |
| <span data-ttu-id="966e9-173">start</span><span class="sxs-lookup"><span data-stu-id="966e9-173">start</span></span> |<span data-ttu-id="966e9-174">片段的開始時間 (以「刻度」為單位)</span><span class="sxs-lookup"><span data-stu-id="966e9-174">start time of a fragment in "ticks"</span></span> |
| <span data-ttu-id="966e9-175">duration</span><span class="sxs-lookup"><span data-stu-id="966e9-175">duration</span></span> |<span data-ttu-id="966e9-176">片段的長度 (以「刻度」為單位)</span><span class="sxs-lookup"><span data-stu-id="966e9-176">length of a fragment in "ticks"</span></span> |
| <span data-ttu-id="966e9-177">interval</span><span class="sxs-lookup"><span data-stu-id="966e9-177">interval</span></span> |<span data-ttu-id="966e9-178">每個事件內 hello 給定片段的間隔</span><span class="sxs-lookup"><span data-stu-id="966e9-178">interval of each event within hello given fragment</span></span> |
| <span data-ttu-id="966e9-179">活動</span><span class="sxs-lookup"><span data-stu-id="966e9-179">events</span></span> |<span data-ttu-id="966e9-180">包含區域的陣列</span><span class="sxs-lookup"><span data-stu-id="966e9-180">array containing regions</span></span> |
| <span data-ttu-id="966e9-181">region</span><span class="sxs-lookup"><span data-stu-id="966e9-181">region</span></span> |<span data-ttu-id="966e9-182">物件，代表偵測到的單字或片語</span><span class="sxs-lookup"><span data-stu-id="966e9-182">object representing detected words or phrases</span></span> |
| <span data-ttu-id="966e9-183">語言</span><span class="sxs-lookup"><span data-stu-id="966e9-183">language</span></span> |<span data-ttu-id="966e9-184">區域內偵測到的 hello 文字的語言</span><span class="sxs-lookup"><span data-stu-id="966e9-184">language of hello text detected within a region</span></span> |
| <span data-ttu-id="966e9-185">orientation</span><span class="sxs-lookup"><span data-stu-id="966e9-185">orientation</span></span> |<span data-ttu-id="966e9-186">區域內偵測到的 hello 文字方向</span><span class="sxs-lookup"><span data-stu-id="966e9-186">orientation of hello text detected within a region</span></span> |
| <span data-ttu-id="966e9-187">lines</span><span class="sxs-lookup"><span data-stu-id="966e9-187">lines</span></span> |<span data-ttu-id="966e9-188">區域內偵測到的文字行陣列</span><span class="sxs-lookup"><span data-stu-id="966e9-188">array of lines of text detected within a region</span></span> |
| <span data-ttu-id="966e9-189">文字</span><span class="sxs-lookup"><span data-stu-id="966e9-189">text</span></span> |<span data-ttu-id="966e9-190">實際的 hello 文字</span><span class="sxs-lookup"><span data-stu-id="966e9-190">hello actual text</span></span> |

### <a name="json-output-example"></a><span data-ttu-id="966e9-191">JSON 輸出範例</span><span class="sxs-lookup"><span data-stu-id="966e9-191">JSON output example</span></span>
<span data-ttu-id="966e9-192">hello 下列輸出範例包含 hello 一般視訊資訊和數個視訊片段。</span><span class="sxs-lookup"><span data-stu-id="966e9-192">hello following output example contains hello general video information and several video fragments.</span></span> <span data-ttu-id="966e9-193">在每個視訊片段中，它會包含每個偵測到的 OCR 管理組件以 hello 語言和其文字方向的區域。</span><span class="sxs-lookup"><span data-stu-id="966e9-193">In every video fragment, it contains every region which is detected by OCR MP with hello language and its text orientation.</span></span> <span data-ttu-id="966e9-194">hello 區域也包含 hello 一行文字、 與 hello 行的位置，這行中的每個 word 資訊 （word 內容、 位置和信心） 這個區域中的每個字行。</span><span class="sxs-lookup"><span data-stu-id="966e9-194">hello region also contains every word line in this region with hello line’s text, hello line’s position, and every word information (word content, position and confidence) in this line.</span></span> <span data-ttu-id="966e9-195">hello 以下是範例，並使某些註解內嵌。</span><span class="sxs-lookup"><span data-stu-id="966e9-195">hello following is an example, and I put some comments inline.</span></span>

    {
        "version": 1, 
        "timescale": 90000, 
        "offset": 0, 
        "framerate": 30, 
        "width": 640, 
        "height": 480,  // general video information
        "fragments": [
            {
                "start": 0, 
                "duration": 180000, 
                "interval": 90000,  // hello time information about this fragment
                "events": [
                    [
                       { 
                            "region": { // hello detected region array in this fragment 
                                "language": "English",  // region language
                                "orientation": "Up",  // text orientation
                                "lines": [  // line information array in this region, including hello text and hello position
                                    {
                                        "text": "One Two", 
                                        "left": 10, 
                                        "top": 10, 
                                        "right": 210, 
                                        "bottom": 110, 
                                        "word": [  // word information array in this line
                                            {
                                                "text": "One", 
                                                "left": 10, 
                                                "top": 10, 
                                                "right": 110, 
                                                "bottom": 110, 
                                                "confidence": 900
                                            }, 
                                            {
                                                "text": "Two", 
                                                "left": 110, 
                                                "top": 10, 
                                                "right": 210, 
                                                "bottom": 110, 
                                                "confidence": 910
                                            }
                                        ]
                                    }
                                ]
                            }
                        }
                    ]
                ]
            }
        ]
    }

## <a name="net-sample-code"></a><span data-ttu-id="966e9-196">.NET 範例程式碼</span><span class="sxs-lookup"><span data-stu-id="966e9-196">.NET sample code</span></span>

<span data-ttu-id="966e9-197">hello 以下程式顯示如何：</span><span class="sxs-lookup"><span data-stu-id="966e9-197">hello following program shows how to:</span></span>

1. <span data-ttu-id="966e9-198">建立資產，並將媒體檔案上傳到 hello 資產。</span><span class="sxs-lookup"><span data-stu-id="966e9-198">Create an asset and upload a media file into hello asset.</span></span>
2. <span data-ttu-id="966e9-199">使用 OCR 設定/預設檔案建立作業。</span><span class="sxs-lookup"><span data-stu-id="966e9-199">Create a job with an OCR configuration/preset file.</span></span>
3. <span data-ttu-id="966e9-200">下載 hello 輸出 JSON 檔案。</span><span class="sxs-lookup"><span data-stu-id="966e9-200">Download hello output JSON files.</span></span> 
   
#### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="966e9-201">建立和設定 Visual Studio 專案</span><span class="sxs-lookup"><span data-stu-id="966e9-201">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="966e9-202">設定您的開發環境，並填入 hello 與連接資訊的 app.config 檔案中所述[與.NET 的 Media Services 開發](media-services-dotnet-how-to-use.md)。</span><span class="sxs-lookup"><span data-stu-id="966e9-202">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

#### <a name="example"></a><span data-ttu-id="966e9-203">範例</span><span class="sxs-lookup"><span data-stu-id="966e9-203">Example</span></span>

    using System;
    using System.Configuration;
    using System.IO;
    using System.Linq;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using System.Threading;
    using System.Threading.Tasks;

    namespace OCR
    {
        class Program
        {
            // Read values from hello App.config file.
            private static readonly string _AADTenantDomain =
                ConfigurationManager.AppSettings["AADTenantDomain"];
            private static readonly string _RESTAPIEndpoint =
                ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];

            // Field for service context.
            private static CloudMediaContext _context = null;

            static void Main(string[] args)
            {
                var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
                var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

                _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);

                // Run hello OCR job.
                var asset = RunOCRJob(@"C:\supportFiles\OCR\presentation.mp4",
                                            @"C:\supportFiles\OCR\config.json");

                // Download hello job output asset.
                DownloadAsset(asset, @"C:\supportFiles\OCR\Output");
            }

            static IAsset RunOCRJob(string inputMediaFilePath, string configurationFile)
            {
                // Create an asset and upload hello input media file toostorage.
                IAsset asset = CreateAssetAndUploadSingleFile(inputMediaFilePath,
                    "My OCR Input Asset",
                    AssetCreationOptions.None);

                // Declare a new job.
                IJob job = _context.Jobs.Create("My OCR Job");

                // Get a reference tooAzure Media OCR.
                string MediaProcessorName = "Azure Media OCR";

                var processor = GetLatestMediaProcessorByName(MediaProcessorName);

                // Read configuration from hello specified file.
                string configuration = File.ReadAllText(configurationFile);

                // Create a task with hello encoding details, using a string preset.
                ITask task = job.Tasks.AddNew("My OCR Task",
                    processor,
                    configuration,
                    TaskOptions.None);

                // Specify hello input asset.
                task.InputAssets.Add(asset);

                // Add an output asset toocontain hello results of hello job.
                task.OutputAssets.AddNew("My OCR Output Asset", AssetCreationOptions.None);

                // Use hello following event handler toocheck job progress.  
                job.StateChanged += new EventHandler<JobStateChangedEventArgs>(StateChanged);

                // Launch hello job.
                job.Submit();

                // Check job execution and wait for job toofinish.
                Task progressJobTask = job.GetExecutionProgressTask(CancellationToken.None);

                progressJobTask.Wait();

                // If job state is Error, hello event handling
                // method for job progress should log errors.  Here we check
                // for error state and exit if needed.
                if (job.State == JobState.Error)
                {
                    ErrorDetail error = job.Tasks.First().ErrorDetails.First();
                    Console.WriteLine(string.Format("Error: {0}. {1}",
                                                    error.Code,
                                                    error.Message));
                    return null;
                }

                return job.OutputMediaAssets[0];
            }

            static IAsset CreateAssetAndUploadSingleFile(string filePath, string assetName, AssetCreationOptions options)
            {
                IAsset asset = _context.Assets.Create(assetName, options);

                var assetFile = asset.AssetFiles.Create(Path.GetFileName(filePath));
                assetFile.Upload(filePath);

                return asset;
            }

            static void DownloadAsset(IAsset asset, string outputDirectory)
            {
                foreach (IAssetFile file in asset.AssetFiles)
                {
                    file.Download(Path.Combine(outputDirectory, file.Name));
                }
            }

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

            static private void StateChanged(object sender, JobStateChangedEventArgs e)
            {
                Console.WriteLine("Job state changed event:");
                Console.WriteLine("  Previous state: " + e.PreviousState);
                Console.WriteLine("  Current state: " + e.CurrentState);

                switch (e.CurrentState)
                {
                    case JobState.Finished:
                        Console.WriteLine();
                        Console.WriteLine("Job is finished.");
                        Console.WriteLine();
                        break;
                    case JobState.Canceling:
                    case JobState.Queued:
                    case JobState.Scheduled:
                    case JobState.Processing:
                        Console.WriteLine("Please wait...\n");
                        break;
                    case JobState.Canceled:
                    case JobState.Error:
                        // Cast sender as a job.
                        IJob job = (IJob)sender;
                        // Display or log error details as needed.
                        // LogJobStop(job.Id);
                        break;
                    default:
                        break;
                }
            }

        }
    }

## <a name="media-services-learning-paths"></a><span data-ttu-id="966e9-204">媒體服務學習路徑</span><span class="sxs-lookup"><span data-stu-id="966e9-204">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="966e9-205">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="966e9-205">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a><span data-ttu-id="966e9-206">相關連結</span><span class="sxs-lookup"><span data-stu-id="966e9-206">Related links</span></span>
[<span data-ttu-id="966e9-207">Azure 媒體服務分析概觀</span><span class="sxs-lookup"><span data-stu-id="966e9-207">Azure Media Services Analytics Overview</span></span>](media-services-analytics-overview.md)

