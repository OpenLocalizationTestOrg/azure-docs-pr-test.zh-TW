---
title: "使用 Azure 媒體分析 OCR 將文字數位化 | Microsoft Docs"
description: "Azure 媒體分析 OCR (光學字元辨識) 可讓您將視訊檔中的文字內容轉換成可編輯、可搜尋的數位文字。  這可讓您從媒體的視訊訊號自動擷取有意義的中繼資料。"
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
ms.openlocfilehash: 43f5b3a9bbec243e668c79702045094fcfedbdda
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="use-azure-media-analytics-to-convert-text-content-in-video-files-into-digital-text"></a><span data-ttu-id="0c1de-104">使用 Azure 媒體分析以將視訊檔案中的文字內容轉換為數位文字</span><span class="sxs-lookup"><span data-stu-id="0c1de-104">Use Azure Media Analytics to convert text content in video files into digital text</span></span>
## <a name="overview"></a><span data-ttu-id="0c1de-105">概觀</span><span class="sxs-lookup"><span data-stu-id="0c1de-105">Overview</span></span>
<span data-ttu-id="0c1de-106">如果您需要擷取視訊檔案的文字內容，並產生可編輯、可搜尋的數位文字，您應該使用 Azure 媒體分析 OCR (光學字元辨識)。</span><span class="sxs-lookup"><span data-stu-id="0c1de-106">If you need to extract text content from your video files and generate an editable, searchable digital text, you should use Azure Media Analytics OCR (optical character recognition).</span></span> <span data-ttu-id="0c1de-107">此 Azure 媒體處理器會偵測視訊檔案的文字內容並產生文字檔案，以供您使用。</span><span class="sxs-lookup"><span data-stu-id="0c1de-107">This Azure Media Processor detects text content in your video files and generates text files for your use.</span></span> <span data-ttu-id="0c1de-108">OCR 可讓您從媒體的視訊訊號自動擷取有意義的中繼資料。</span><span class="sxs-lookup"><span data-stu-id="0c1de-108">OCR enables you to automate the extraction of meaningful metadata from the video signal of your media.</span></span>

<span data-ttu-id="0c1de-109">搭配搜尋引擎使用時，您可以輕易地依文字編製媒體的索引，並增強探索內容的能力。</span><span class="sxs-lookup"><span data-stu-id="0c1de-109">When used in conjunction with a search engine, you can easily index your media by text, and enhance the discoverability of your content.</span></span> <span data-ttu-id="0c1de-110">這在具有大量文字的視訊 (例如視訊錄製或投影片簡報的螢幕擷取) 中非常實用。</span><span class="sxs-lookup"><span data-stu-id="0c1de-110">This is extremely useful in highly textual video, like a video recording or screen-capture of a slideshow presentation.</span></span> <span data-ttu-id="0c1de-111">Azure OCR 媒體處理器已針對數位文字進行最佳化。</span><span class="sxs-lookup"><span data-stu-id="0c1de-111">The Azure OCR Media Processor is optimized for digital text.</span></span>

<span data-ttu-id="0c1de-112">**Azure 媒體 OCR** 媒體處理器目前為預覽版。</span><span class="sxs-lookup"><span data-stu-id="0c1de-112">The **Azure Media OCR** media processor is currently in Preview.</span></span>

<span data-ttu-id="0c1de-113">本主題提供有關 **Azure 媒體 OCR** 的詳細資料，並示範如何搭配適用於 .NET 的媒體服務 SDK 來使用它。</span><span class="sxs-lookup"><span data-stu-id="0c1de-113">This topic gives details about  **Azure Media OCR** and shows how to use it with Media Services SDK for .NET.</span></span> <span data-ttu-id="0c1de-114">如需詳細資訊和範例，請參閱 [這篇部落格](https://azure.microsoft.com/blog/announcing-video-ocr-public-preview-new-config/)。</span><span class="sxs-lookup"><span data-stu-id="0c1de-114">For additional information and examples, see [this blog](https://azure.microsoft.com/blog/announcing-video-ocr-public-preview-new-config/).</span></span>

## <a name="ocr-input-files"></a><span data-ttu-id="0c1de-115">OCR 輸入檔案</span><span class="sxs-lookup"><span data-stu-id="0c1de-115">OCR input files</span></span>
<span data-ttu-id="0c1de-116">影片檔案。</span><span class="sxs-lookup"><span data-stu-id="0c1de-116">Video files.</span></span> <span data-ttu-id="0c1de-117">目前支援下列格式：MP4、MOV 及 WMV。</span><span class="sxs-lookup"><span data-stu-id="0c1de-117">Currently, the following formats are supported: MP4, MOV, and WMV.</span></span>

## <a name="task-configuration"></a><span data-ttu-id="0c1de-118">工作組態</span><span class="sxs-lookup"><span data-stu-id="0c1de-118">Task configuration</span></span>
<span data-ttu-id="0c1de-119">工作組態 (預設)。</span><span class="sxs-lookup"><span data-stu-id="0c1de-119">Task configuration (preset).</span></span> <span data-ttu-id="0c1de-120">使用 **Azure 媒體 OCR** 建立工作時，您必須使用 JSON 或 XML 來指定組態預設。</span><span class="sxs-lookup"><span data-stu-id="0c1de-120">When creating a task with **Azure Media OCR**, you must specify a configuration preset using JSON  or XML.</span></span> 

>[!NOTE]
><span data-ttu-id="0c1de-121">OCR 引擎只會接受高度/寬度兩者在最小 40 像素到最大 32000 像素的影像區域為有效的輸入。</span><span class="sxs-lookup"><span data-stu-id="0c1de-121">The OCR engine only takes an image region with minimum 40 pixels to maximum 32000 pixels as a valid input in both height/width.</span></span>
>

### <a name="attribute-descriptions"></a><span data-ttu-id="0c1de-122">屬性描述</span><span class="sxs-lookup"><span data-stu-id="0c1de-122">Attribute descriptions</span></span>
| <span data-ttu-id="0c1de-123">屬性名稱</span><span class="sxs-lookup"><span data-stu-id="0c1de-123">Attribute name</span></span> | <span data-ttu-id="0c1de-124">說明</span><span class="sxs-lookup"><span data-stu-id="0c1de-124">Description</span></span> |
| --- | --- |
|<span data-ttu-id="0c1de-125">AdvancedOutput</span><span class="sxs-lookup"><span data-stu-id="0c1de-125">AdvancedOutput</span></span>| <span data-ttu-id="0c1de-126">如果您將 AdvancedOutput 設為 true，JSON 輸出就會包含每一個文字的位置資料 (除了片語和區域)。</span><span class="sxs-lookup"><span data-stu-id="0c1de-126">If you set AdvancedOutput to true, the JSON output will contain positional data for every single word (in addition to phrases and regions).</span></span> <span data-ttu-id="0c1de-127">如果您不想要查看這些詳細資料，請將旗標設定為 false。</span><span class="sxs-lookup"><span data-stu-id="0c1de-127">If you do not want to see these details, set the flag to false.</span></span> <span data-ttu-id="0c1de-128">預設值為 False。</span><span class="sxs-lookup"><span data-stu-id="0c1de-128">The default value is false.</span></span> <span data-ttu-id="0c1de-129">如需詳細資訊，請參閱 [此部落格](https://azure.microsoft.com/blog/azure-media-ocr-simplified-output/)。</span><span class="sxs-lookup"><span data-stu-id="0c1de-129">For more information, see [this blog](https://azure.microsoft.com/blog/azure-media-ocr-simplified-output/).</span></span>|
| <span data-ttu-id="0c1de-130">語言</span><span class="sxs-lookup"><span data-stu-id="0c1de-130">Language</span></span> |<span data-ttu-id="0c1de-131">(選擇性) 說明要尋找的文字語言。</span><span class="sxs-lookup"><span data-stu-id="0c1de-131">(optional) describes the language of text for which to look.</span></span> <span data-ttu-id="0c1de-132">下列其中一種︰AutoDetect (預設值)、Arabic、ChineseSimplified、ChineseTraditional、Czech Danish、Dutch、English、Finnish、French、German、Greek、Hungarian、Italian、Japanese、Korean、Norwegian、Polish、Portuguese、Romanian、Russian、SerbianCyrillic、SerbianLatin、Slovak、Spanish、Swedish、Turkish。</span><span class="sxs-lookup"><span data-stu-id="0c1de-132">One of the following: AutoDetect (default), Arabic, ChineseSimplified, ChineseTraditional, Czech Danish, Dutch, English, Finnish, French, German,  Greek, Hungarian, Italian, Japanese, Korean, Norwegian, Polish, Portuguese, Romanian, Russian, SerbianCyrillic, SerbianLatin, Slovak, Spanish, Swedish, Turkish.</span></span> |
| <span data-ttu-id="0c1de-133">TextOrientation</span><span class="sxs-lookup"><span data-stu-id="0c1de-133">TextOrientation</span></span> |<span data-ttu-id="0c1de-134">(選擇性) 說明要尋找的文字方向。</span><span class="sxs-lookup"><span data-stu-id="0c1de-134">(optional) describes the orientation of text for which to look.</span></span>  <span data-ttu-id="0c1de-135">"Left" 表示所有字母頂端都會指向左邊。</span><span class="sxs-lookup"><span data-stu-id="0c1de-135">"Left" means that the top of all letters are pointed towards the left.</span></span>  <span data-ttu-id="0c1de-136">預設文字 (像是可在書本中找到的文字) 的方向為 "Up"。</span><span class="sxs-lookup"><span data-stu-id="0c1de-136">Default text (like that which can be found in a book) can be called "Up" oriented.</span></span>  <span data-ttu-id="0c1de-137">下列其中一種︰AutoDetect (預設值)、Up、Right、Down、Left。</span><span class="sxs-lookup"><span data-stu-id="0c1de-137">One of the following: AutoDetect (default), Up, Right, Down, Left.</span></span> |
| <span data-ttu-id="0c1de-138">TimeInterval</span><span class="sxs-lookup"><span data-stu-id="0c1de-138">TimeInterval</span></span> |<span data-ttu-id="0c1de-139">(選擇性) 說明取樣率。</span><span class="sxs-lookup"><span data-stu-id="0c1de-139">(optional) describes the sampling rate.</span></span>  <span data-ttu-id="0c1de-140">預設值為每 1/2 秒。</span><span class="sxs-lookup"><span data-stu-id="0c1de-140">Default is every 1/2 second.</span></span><br/><span data-ttu-id="0c1de-141">JSON 格式 – HH:mm:ss.SSS (預設值 00:00:00.500)</span><span class="sxs-lookup"><span data-stu-id="0c1de-141">JSON format – HH:mm:ss.SSS (default 00:00:00.500)</span></span><br/><span data-ttu-id="0c1de-142">XML 格式 – W3C XSD 持續時間基本型別 (預設值 PT0.5)</span><span class="sxs-lookup"><span data-stu-id="0c1de-142">XML format – W3C XSD duration primitive (default PT0.5)</span></span> |
| <span data-ttu-id="0c1de-143">DetectRegions</span><span class="sxs-lookup"><span data-stu-id="0c1de-143">DetectRegions</span></span> |<span data-ttu-id="0c1de-144">(選擇性) DetectRegion 物件的陣列，指定在其中偵測文字的視訊畫面格內的區域。</span><span class="sxs-lookup"><span data-stu-id="0c1de-144">(optional) An array of DetectRegion objects specifying regions within the video frame in which to detect text.</span></span><br/><span data-ttu-id="0c1de-145">DetectRegion 物件是由下列四個整數值組成︰</span><span class="sxs-lookup"><span data-stu-id="0c1de-145">A DetectRegion object is made of the following four integer values:</span></span><br/><span data-ttu-id="0c1de-146">左 – 像素的左邊界</span><span class="sxs-lookup"><span data-stu-id="0c1de-146">Left – pixels from the left-margin</span></span><br/><span data-ttu-id="0c1de-147">上 – 像素的上邊界</span><span class="sxs-lookup"><span data-stu-id="0c1de-147">Top – pixels from the top-margin</span></span><br/><span data-ttu-id="0c1de-148">寬度 – 以像素為單位的區域寬度</span><span class="sxs-lookup"><span data-stu-id="0c1de-148">Width – width of the region in pixels</span></span><br/><span data-ttu-id="0c1de-149">高度 – 以像素為單位的區域高度</span><span class="sxs-lookup"><span data-stu-id="0c1de-149">Height – height of the region in pixels</span></span> |

#### <a name="json-preset-example"></a><span data-ttu-id="0c1de-150">JSON 預設範例</span><span class="sxs-lookup"><span data-stu-id="0c1de-150">JSON preset example</span></span>

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


#### <a name="xml-preset-example"></a><span data-ttu-id="0c1de-151">XML 預設範例</span><span class="sxs-lookup"><span data-stu-id="0c1de-151">XML preset example</span></span>
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

## <a name="ocr-output-files"></a><span data-ttu-id="0c1de-152">OCR 輸出檔案</span><span class="sxs-lookup"><span data-stu-id="0c1de-152">OCR output files</span></span>
<span data-ttu-id="0c1de-153">OCR 媒體處理器的輸出是 JSON 檔案。</span><span class="sxs-lookup"><span data-stu-id="0c1de-153">The output of the OCR media processor is a JSON file.</span></span>

### <a name="elements-of-the-output-json-file"></a><span data-ttu-id="0c1de-154">輸出 JSON 檔案的元素</span><span class="sxs-lookup"><span data-stu-id="0c1de-154">Elements of the output JSON file</span></span>
<span data-ttu-id="0c1de-155">視訊 OCR 輸出會在可於視訊上找到的字元中提供時間分段資料。</span><span class="sxs-lookup"><span data-stu-id="0c1de-155">The Video OCR output provides time-segmented data on the characters found in your video.</span></span>  <span data-ttu-id="0c1de-156">您可以使用屬性 (例如語言或方向)，確實琢磨您有興趣進行分析的文字。</span><span class="sxs-lookup"><span data-stu-id="0c1de-156">You can use attributes such as language or orientation to hone-in on exactly the words that you are interested in analyzing.</span></span> 

<span data-ttu-id="0c1de-157">輸出包含下列屬性：</span><span class="sxs-lookup"><span data-stu-id="0c1de-157">The output contains the following attributes:</span></span>

| <span data-ttu-id="0c1de-158">元素</span><span class="sxs-lookup"><span data-stu-id="0c1de-158">Element</span></span> | <span data-ttu-id="0c1de-159">說明</span><span class="sxs-lookup"><span data-stu-id="0c1de-159">Description</span></span> |
| --- | --- |
| <span data-ttu-id="0c1de-160">時幅</span><span class="sxs-lookup"><span data-stu-id="0c1de-160">Timescale</span></span> |<span data-ttu-id="0c1de-161">影片每秒的「刻度」數目</span><span class="sxs-lookup"><span data-stu-id="0c1de-161">"ticks" per second of the video</span></span> |
| <span data-ttu-id="0c1de-162">Offset</span><span class="sxs-lookup"><span data-stu-id="0c1de-162">Offset</span></span> |<span data-ttu-id="0c1de-163">時間戳記的時間位移。</span><span class="sxs-lookup"><span data-stu-id="0c1de-163">time offset for timestamps.</span></span> <span data-ttu-id="0c1de-164">在版本 1.0 的影片 API 中，這永遠會是 0。</span><span class="sxs-lookup"><span data-stu-id="0c1de-164">In version 1.0 of Video APIs, this will always be 0.</span></span> |
| <span data-ttu-id="0c1de-165">畫面播放速率</span><span class="sxs-lookup"><span data-stu-id="0c1de-165">Framerate</span></span> |<span data-ttu-id="0c1de-166">影片的每秒畫面格數</span><span class="sxs-lookup"><span data-stu-id="0c1de-166">Frames per second of the video</span></span> |
| <span data-ttu-id="0c1de-167">width</span><span class="sxs-lookup"><span data-stu-id="0c1de-167">width</span></span> |<span data-ttu-id="0c1de-168">視訊寬度 (以像素為單位)</span><span class="sxs-lookup"><span data-stu-id="0c1de-168">width of the video in pixels</span></span> |
| <span data-ttu-id="0c1de-169">height</span><span class="sxs-lookup"><span data-stu-id="0c1de-169">height</span></span> |<span data-ttu-id="0c1de-170">視訊高度 (以像素為單位)</span><span class="sxs-lookup"><span data-stu-id="0c1de-170">height of the video in pixels</span></span> |
| <span data-ttu-id="0c1de-171">片段</span><span class="sxs-lookup"><span data-stu-id="0c1de-171">Fragments</span></span> |<span data-ttu-id="0c1de-172">在視訊中，將中繼資料切割為以時間為基礎的區塊陣列</span><span class="sxs-lookup"><span data-stu-id="0c1de-172">array of time-based chunks of video into which the metadata is chunked</span></span> |
| <span data-ttu-id="0c1de-173">start</span><span class="sxs-lookup"><span data-stu-id="0c1de-173">start</span></span> |<span data-ttu-id="0c1de-174">片段的開始時間 (以「刻度」為單位)</span><span class="sxs-lookup"><span data-stu-id="0c1de-174">start time of a fragment in "ticks"</span></span> |
| <span data-ttu-id="0c1de-175">duration</span><span class="sxs-lookup"><span data-stu-id="0c1de-175">duration</span></span> |<span data-ttu-id="0c1de-176">片段的長度 (以「刻度」為單位)</span><span class="sxs-lookup"><span data-stu-id="0c1de-176">length of a fragment in "ticks"</span></span> |
| <span data-ttu-id="0c1de-177">interval</span><span class="sxs-lookup"><span data-stu-id="0c1de-177">interval</span></span> |<span data-ttu-id="0c1de-178">指定片段內每個事件的間隔</span><span class="sxs-lookup"><span data-stu-id="0c1de-178">interval of each event within the given fragment</span></span> |
| <span data-ttu-id="0c1de-179">events</span><span class="sxs-lookup"><span data-stu-id="0c1de-179">events</span></span> |<span data-ttu-id="0c1de-180">包含區域的陣列</span><span class="sxs-lookup"><span data-stu-id="0c1de-180">array containing regions</span></span> |
| <span data-ttu-id="0c1de-181">region</span><span class="sxs-lookup"><span data-stu-id="0c1de-181">region</span></span> |<span data-ttu-id="0c1de-182">物件，代表偵測到的單字或片語</span><span class="sxs-lookup"><span data-stu-id="0c1de-182">object representing detected words or phrases</span></span> |
| <span data-ttu-id="0c1de-183">語言</span><span class="sxs-lookup"><span data-stu-id="0c1de-183">language</span></span> |<span data-ttu-id="0c1de-184">區域內偵測到的文字語言</span><span class="sxs-lookup"><span data-stu-id="0c1de-184">language of the text detected within a region</span></span> |
| <span data-ttu-id="0c1de-185">orientation</span><span class="sxs-lookup"><span data-stu-id="0c1de-185">orientation</span></span> |<span data-ttu-id="0c1de-186">區域內偵測到的文字方向</span><span class="sxs-lookup"><span data-stu-id="0c1de-186">orientation of the text detected within a region</span></span> |
| <span data-ttu-id="0c1de-187">lines</span><span class="sxs-lookup"><span data-stu-id="0c1de-187">lines</span></span> |<span data-ttu-id="0c1de-188">區域內偵測到的文字行陣列</span><span class="sxs-lookup"><span data-stu-id="0c1de-188">array of lines of text detected within a region</span></span> |
| <span data-ttu-id="0c1de-189">文字</span><span class="sxs-lookup"><span data-stu-id="0c1de-189">text</span></span> |<span data-ttu-id="0c1de-190">實際的文字</span><span class="sxs-lookup"><span data-stu-id="0c1de-190">the actual text</span></span> |

### <a name="json-output-example"></a><span data-ttu-id="0c1de-191">JSON 輸出範例</span><span class="sxs-lookup"><span data-stu-id="0c1de-191">JSON output example</span></span>
<span data-ttu-id="0c1de-192">下列輸出範例包含一般視訊資訊和數個視訊片段。</span><span class="sxs-lookup"><span data-stu-id="0c1de-192">The following output example contains the general video information and several video fragments.</span></span> <span data-ttu-id="0c1de-193">每個視訊片段都包含 OCR MP 使用語言及其文字方向偵測到的每個區域。</span><span class="sxs-lookup"><span data-stu-id="0c1de-193">In every video fragment, it contains every region which is detected by OCR MP with the language and its text orientation.</span></span> <span data-ttu-id="0c1de-194">區域也包含這個區域中的每個文字行，以及該行的文字、該行的位置和該行中每個單字的資訊 (單字內容、位置和信賴度)。</span><span class="sxs-lookup"><span data-stu-id="0c1de-194">The region also contains every word line in this region with the line’s text, the line’s position, and every word information (word content, position and confidence) in this line.</span></span> <span data-ttu-id="0c1de-195">以下是範例，而我在其中放入了一些註解。</span><span class="sxs-lookup"><span data-stu-id="0c1de-195">The following is an example, and I put some comments inline.</span></span>

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
                "interval": 90000,  // the time information about this fragment
                "events": [
                    [
                       { 
                            "region": { // the detected region array in this fragment 
                                "language": "English",  // region language
                                "orientation": "Up",  // text orientation
                                "lines": [  // line information array in this region, including the text and the position
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

## <a name="net-sample-code"></a><span data-ttu-id="0c1de-196">.NET 範例程式碼</span><span class="sxs-lookup"><span data-stu-id="0c1de-196">.NET sample code</span></span>

<span data-ttu-id="0c1de-197">下列程式將示範如何：</span><span class="sxs-lookup"><span data-stu-id="0c1de-197">The following program shows how to:</span></span>

1. <span data-ttu-id="0c1de-198">建立資產並將媒體檔案上傳到資產。</span><span class="sxs-lookup"><span data-stu-id="0c1de-198">Create an asset and upload a media file into the asset.</span></span>
2. <span data-ttu-id="0c1de-199">使用 OCR 設定/預設檔案建立作業。</span><span class="sxs-lookup"><span data-stu-id="0c1de-199">Create a job with an OCR configuration/preset file.</span></span>
3. <span data-ttu-id="0c1de-200">下載輸出 JSON 檔案。</span><span class="sxs-lookup"><span data-stu-id="0c1de-200">Download the output JSON files.</span></span> 
   
#### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="0c1de-201">建立和設定 Visual Studio 專案</span><span class="sxs-lookup"><span data-stu-id="0c1de-201">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="0c1de-202">設定您的開發環境並在 app.config 檔案中填入連線資訊，如[使用 .NET 進行 Media Services 開發](media-services-dotnet-how-to-use.md)中所述。</span><span class="sxs-lookup"><span data-stu-id="0c1de-202">Set up your development environment and populate the app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

#### <a name="example"></a><span data-ttu-id="0c1de-203">範例</span><span class="sxs-lookup"><span data-stu-id="0c1de-203">Example</span></span>

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
            // Read values from the App.config file.
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

                // Run the OCR job.
                var asset = RunOCRJob(@"C:\supportFiles\OCR\presentation.mp4",
                                            @"C:\supportFiles\OCR\config.json");

                // Download the job output asset.
                DownloadAsset(asset, @"C:\supportFiles\OCR\Output");
            }

            static IAsset RunOCRJob(string inputMediaFilePath, string configurationFile)
            {
                // Create an asset and upload the input media file to storage.
                IAsset asset = CreateAssetAndUploadSingleFile(inputMediaFilePath,
                    "My OCR Input Asset",
                    AssetCreationOptions.None);

                // Declare a new job.
                IJob job = _context.Jobs.Create("My OCR Job");

                // Get a reference to Azure Media OCR.
                string MediaProcessorName = "Azure Media OCR";

                var processor = GetLatestMediaProcessorByName(MediaProcessorName);

                // Read configuration from the specified file.
                string configuration = File.ReadAllText(configurationFile);

                // Create a task with the encoding details, using a string preset.
                ITask task = job.Tasks.AddNew("My OCR Task",
                    processor,
                    configuration,
                    TaskOptions.None);

                // Specify the input asset.
                task.InputAssets.Add(asset);

                // Add an output asset to contain the results of the job.
                task.OutputAssets.AddNew("My OCR Output Asset", AssetCreationOptions.None);

                // Use the following event handler to check job progress.  
                job.StateChanged += new EventHandler<JobStateChangedEventArgs>(StateChanged);

                // Launch the job.
                job.Submit();

                // Check job execution and wait for job to finish.
                Task progressJobTask = job.GetExecutionProgressTask(CancellationToken.None);

                progressJobTask.Wait();

                // If job state is Error, the event handling
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

## <a name="media-services-learning-paths"></a><span data-ttu-id="0c1de-204">媒體服務學習路徑</span><span class="sxs-lookup"><span data-stu-id="0c1de-204">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="0c1de-205">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="0c1de-205">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a><span data-ttu-id="0c1de-206">相關連結</span><span class="sxs-lookup"><span data-stu-id="0c1de-206">Related links</span></span>
[<span data-ttu-id="0c1de-207">Azure 媒體服務分析概觀</span><span class="sxs-lookup"><span data-stu-id="0c1de-207">Azure Media Services Analytics Overview</span></span>](media-services-analytics-overview.md)

