---
title: "aaaDetect 表面和使用 Azure 媒體分析情緒 |Microsoft 文件"
description: "本主題示範如何 toodetect 正面會面對和情緒使用 Azure 媒體分析。"
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 5ca4692c-23f1-451d-9d82-cbc8bf0fd707
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/18/2017
ms.author: milanga;juliako;
ms.openlocfilehash: f58d81d82dde08a694cdb4d92c6bab6a40a9c157
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="detect-face-and-emotion-with-azure-media-analytics"></a><span data-ttu-id="e2c1e-103">使用 Azure 媒體分析偵測臉部和情緒</span><span class="sxs-lookup"><span data-stu-id="e2c1e-103">Detect Face and Emotion with Azure Media Analytics</span></span>
## <a name="overview"></a><span data-ttu-id="e2c1e-104">概觀</span><span class="sxs-lookup"><span data-stu-id="e2c1e-104">Overview</span></span>
<span data-ttu-id="e2c1e-105">hello **Azure 媒體正面偵測器**媒體處理器 (MP) 可讓您 toocount、 軌跡的移動，即使量測計的對象參與以及透過臉部表情的反應。</span><span class="sxs-lookup"><span data-stu-id="e2c1e-105">hello **Azure Media Face Detector** media processor (MP) enables you toocount, track movements, and even gauge audience participation and reaction via facial expressions.</span></span> <span data-ttu-id="e2c1e-106">此服務包含兩個功能：</span><span class="sxs-lookup"><span data-stu-id="e2c1e-106">This service contains two features:</span></span> 

* <span data-ttu-id="e2c1e-107">**臉部偵測**</span><span class="sxs-lookup"><span data-stu-id="e2c1e-107">**Face detection**</span></span>
  
    <span data-ttu-id="e2c1e-108">臉部偵測能夠找出並追蹤影片中的臉部。</span><span class="sxs-lookup"><span data-stu-id="e2c1e-108">Face detection finds and tracks human faces within a video.</span></span> <span data-ttu-id="e2c1e-109">多個字型可以偵測到且後續追蹤與 hello 時間和位置傳回中繼資料中的 JSON 檔案中，移動。</span><span class="sxs-lookup"><span data-stu-id="e2c1e-109">Multiple faces can be detected and subsequently be tracked as they move around, with hello time and location metadata returned in a JSON file.</span></span> <span data-ttu-id="e2c1e-110">在追蹤時，它就會嘗試 toogive 一致的識別碼 toohello 相同面臨 hello 人員四處移動在畫面上，即使它們受到阻擋或簡短保留 hello 框架時。</span><span class="sxs-lookup"><span data-stu-id="e2c1e-110">During tracking, it will attempt toogive a consistent ID toohello same face while hello person is moving around on screen, even if they are obstructed or briefly leave hello frame.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="e2c1e-111">此服務並不會執行臉部辨識。</span><span class="sxs-lookup"><span data-stu-id="e2c1e-111">This service does not perform facial recognition.</span></span> <span data-ttu-id="e2c1e-112">個人離開 hello 框架，或會變成受到阻擋的時間太長時，會指定新的識別碼，就會傳回。</span><span class="sxs-lookup"><span data-stu-id="e2c1e-112">An individual who leaves hello frame or becomes obstructed for too long will be given a new ID when they return.</span></span>
  > 
  > 
* <span data-ttu-id="e2c1e-113">**情緒偵測**</span><span class="sxs-lookup"><span data-stu-id="e2c1e-113">**Emotion detection**</span></span>
  
    <span data-ttu-id="e2c1e-114">情緒偵測作業屬於選擇性元件的 hello 分析多個情感屬性傳回 hello 字體偵測到，包括快樂、 sadness、 擔心、 anger，以及更多的臉偵測媒體處理器。</span><span class="sxs-lookup"><span data-stu-id="e2c1e-114">Emotion Detection is an optional component of hello Face Detection Media Processor that returns analysis on multiple emotional attributes from hello faces detected, including happiness, sadness, fear, anger, and more.</span></span> 

<span data-ttu-id="e2c1e-115">hello **Azure 媒體正面偵測器**MP 目前為預覽狀態。</span><span class="sxs-lookup"><span data-stu-id="e2c1e-115">hello **Azure Media Face Detector** MP is currently in Preview.</span></span>

<span data-ttu-id="e2c1e-116">本主題詳細說明有關**Azure 媒體正面偵測器**，並示範如何 toouse 使用 Media Services SDK for.NET。</span><span class="sxs-lookup"><span data-stu-id="e2c1e-116">This topic gives details about  **Azure Media Face Detector** and shows how toouse it with Media Services SDK for .NET.</span></span>

## <a name="face-detector-input-files"></a><span data-ttu-id="e2c1e-117">臉部偵測器輸入檔案</span><span class="sxs-lookup"><span data-stu-id="e2c1e-117">Face Detector input files</span></span>
<span data-ttu-id="e2c1e-118">影片檔案。</span><span class="sxs-lookup"><span data-stu-id="e2c1e-118">Video files.</span></span> <span data-ttu-id="e2c1e-119">目前支援下列格式的 hello: MP4、 MOV、 和 WMV。</span><span class="sxs-lookup"><span data-stu-id="e2c1e-119">Currently, hello following formats are supported: MP4, MOV, and WMV.</span></span>

## <a name="face-detector-output-files"></a><span data-ttu-id="e2c1e-120">臉部偵測器輸出檔案</span><span class="sxs-lookup"><span data-stu-id="e2c1e-120">Face Detector output files</span></span>
<span data-ttu-id="e2c1e-121">hello 朝偵測和追蹤 API 可提供高精確度朝位置偵測和追蹤可以偵測向上 too64 人力字體視訊中。</span><span class="sxs-lookup"><span data-stu-id="e2c1e-121">hello face detection and tracking API provides high precision face location detection and tracking that can detect up too64 human faces in a video.</span></span> <span data-ttu-id="e2c1e-122">人臉正面提供 hello 獲得最佳結果，同時端字體和小型的字體 (小於或等於 too24x24 像素為單位) 可能不準確。</span><span class="sxs-lookup"><span data-stu-id="e2c1e-122">Frontal faces provide hello best results, while side faces and small faces (less than or equal too24x24 pixels) might not be as accurate.</span></span>

<span data-ttu-id="e2c1e-123">hello 偵測和追蹤字體傳回座標為 （左側、 頂端、 寬度和高度） 指出 hello 的表面，以像素的 hello 映像中的位置，以及一個朝識別碼數字，指出 hello 的個別的追蹤。</span><span class="sxs-lookup"><span data-stu-id="e2c1e-123">hello detected and tracked faces are returned with coordinates (left, top, width, and height) indicating hello location of faces in hello image in pixels, as well as a face ID number indicating hello tracking of that individual.</span></span> <span data-ttu-id="e2c1e-124">字體識別碼時情況下的很容易出錯 tooreset hello 人臉正面遺失或重疊在 hello 框架內，導致指派多個識別碼的某些個人。</span><span class="sxs-lookup"><span data-stu-id="e2c1e-124">Face ID numbers are prone tooreset under circumstances when hello frontal face is lost or overlapped in hello frame, resulting in some individuals getting assigned multiple IDs.</span></span>

## <span data-ttu-id="e2c1e-125"><a id="output_elements"></a>Hello 輸出 JSON 檔案的項目</span><span class="sxs-lookup"><span data-stu-id="e2c1e-125"><a id="output_elements"></a>Elements of hello output JSON file</span></span>

[!INCLUDE [media-services-analytics-output-json](../../includes/media-services-analytics-output-json.md)]

<span data-ttu-id="e2c1e-126">正面偵測器會使用的片段 （hello 中繼資料可以會中斷以時間為基礎的區塊，而您可以下載只配備），以及分割技術 （其中 hello 事件會分解以防它們得太大）。</span><span class="sxs-lookup"><span data-stu-id="e2c1e-126">Face Detector uses techniques of fragmentation (where hello metadata can be broken up in time-based chunks and you can download only what you need), and segmentation (where hello events are broken up in case they get too large).</span></span> <span data-ttu-id="e2c1e-127">一些簡單的計算，可協助您將 hello 資料轉換。</span><span class="sxs-lookup"><span data-stu-id="e2c1e-127">Some simple calculations can help you transform hello data.</span></span> <span data-ttu-id="e2c1e-128">例如，如果事件是從 6300 (刻度) 開始，並擁有 2997 (刻度/每秒) 的時幅，以及 29.97 (畫面/每秒) 的畫面播放速率，則：</span><span class="sxs-lookup"><span data-stu-id="e2c1e-128">For example, if an event started at 6300 (ticks), with a timescale of 2997 (ticks/sec) and framerate of 29.97 (frames/sec), then:</span></span>

* <span data-ttu-id="e2c1e-129">開始/時幅 = 2.1 秒</span><span class="sxs-lookup"><span data-stu-id="e2c1e-129">Start/Timescale = 2.1 seconds</span></span>
* <span data-ttu-id="e2c1e-130">秒數 x 畫面播放速率 = 63 格畫面</span><span class="sxs-lookup"><span data-stu-id="e2c1e-130">Seconds x Framerate = 63 frames</span></span>

## <a name="face-detection-input-and-output-example"></a><span data-ttu-id="e2c1e-131">臉部偵測輸入和輸出範例</span><span class="sxs-lookup"><span data-stu-id="e2c1e-131">Face detection input and output example</span></span>
### <a name="input-video"></a><span data-ttu-id="e2c1e-132">輸入影片</span><span class="sxs-lookup"><span data-stu-id="e2c1e-132">Input video</span></span>
[<span data-ttu-id="e2c1e-133">輸入影片</span><span class="sxs-lookup"><span data-stu-id="e2c1e-133">Input Video</span></span>](http://ampdemo.azureedge.net/azuremediaplayer.html?url=https%3A%2F%2Freferencestream-samplestream.streaming.mediaservices.windows.net%2Fc8834d9f-0b49-4b38-bcaf-ece2746f1972%2FMicrosoft%20Convergence%202015%20%20Keynote%20Highlights.ism%2Fmanifest&amp;autoplay=false)

### <a name="task-configuration-preset"></a><span data-ttu-id="e2c1e-134">工作設定 (預設)</span><span class="sxs-lookup"><span data-stu-id="e2c1e-134">Task configuration (preset)</span></span>
<span data-ttu-id="e2c1e-135">以 **Azure 媒體臉部偵測器**建立工作時，您必須指定設定預設值。</span><span class="sxs-lookup"><span data-stu-id="e2c1e-135">When creating a task with **Azure Media Face Detector**, you must specify a configuration preset.</span></span> <span data-ttu-id="e2c1e-136">下列組態的預設 hello 只適用於臉偵測。</span><span class="sxs-lookup"><span data-stu-id="e2c1e-136">hello following configuration preset is just for face detection.</span></span>

    {
      "version":"1.0",
      "options":{
          "TrackingMode": "Fast"
      }
    }

#### <a name="attribute-descriptions"></a><span data-ttu-id="e2c1e-137">屬性描述</span><span class="sxs-lookup"><span data-stu-id="e2c1e-137">Attribute descriptions</span></span>
| <span data-ttu-id="e2c1e-138">屬性名稱</span><span class="sxs-lookup"><span data-stu-id="e2c1e-138">Attribute name</span></span> | <span data-ttu-id="e2c1e-139">說明</span><span class="sxs-lookup"><span data-stu-id="e2c1e-139">Description</span></span> |
| --- | --- |
| <span data-ttu-id="e2c1e-140">Mode</span><span class="sxs-lookup"><span data-stu-id="e2c1e-140">Mode</span></span> |<span data-ttu-id="e2c1e-141">Fast：較快的處理速度，但較不精確 (預設)。</span><span class="sxs-lookup"><span data-stu-id="e2c1e-141">Fast - fast processing speed, but less accurate (default).</span></span>|

### <a name="json-output"></a><span data-ttu-id="e2c1e-142">JSON 輸出</span><span class="sxs-lookup"><span data-stu-id="e2c1e-142">JSON output</span></span>
<span data-ttu-id="e2c1e-143">下列範例的 JSON 輸出的 hello 已遭截斷。</span><span class="sxs-lookup"><span data-stu-id="e2c1e-143">hello following example of JSON output was truncated.</span></span>

    {
    "version": 1,
    "timescale": 30000,
    "offset": 0,
    "framerate": 29.97,
    "width": 1280,
    "height": 720,
    "fragments": [
        {
        "start": 0,
        "duration": 60060
        },
        {
        "start": 60060,
        "duration": 60060,
        "interval": 1001,
        "events": [
            [
            {
                "id": 0,
                "x": 0.519531,
                "y": 0.180556,
                "width": 0.0867188,
                "height": 0.154167
            }
            ],
            [
            {
                "id": 0,
                "x": 0.517969,
                "y": 0.181944,
                "width": 0.0867188,
                "height": 0.154167
            }
            ],
            [
            {
                "id": 0,
                "x": 0.517187,
                "y": 0.183333,
                "width": 0.0851562,
                "height": 0.151389
            }
            ],

        . . . 

## <a name="emotion-detection-input-and-output-example"></a><span data-ttu-id="e2c1e-144">情緒偵測輸入和輸出範例</span><span class="sxs-lookup"><span data-stu-id="e2c1e-144">Emotion detection input and output example</span></span>
### <a name="input-video"></a><span data-ttu-id="e2c1e-145">輸入影片</span><span class="sxs-lookup"><span data-stu-id="e2c1e-145">Input video</span></span>
[<span data-ttu-id="e2c1e-146">輸入影片</span><span class="sxs-lookup"><span data-stu-id="e2c1e-146">Input Video</span></span>](http://ampdemo.azureedge.net/azuremediaplayer.html?url=https%3A%2F%2Freferencestream-samplestream.streaming.mediaservices.windows.net%2Fc8834d9f-0b49-4b38-bcaf-ece2746f1972%2FMicrosoft%20Convergence%202015%20%20Keynote%20Highlights.ism%2Fmanifest&amp;autoplay=false)

### <a name="task-configuration-preset"></a><span data-ttu-id="e2c1e-147">工作設定 (預設)</span><span class="sxs-lookup"><span data-stu-id="e2c1e-147">Task configuration (preset)</span></span>
<span data-ttu-id="e2c1e-148">以 **Azure 媒體臉部偵測器**建立工作時，您必須指定設定預設值。</span><span class="sxs-lookup"><span data-stu-id="e2c1e-148">When creating a task with **Azure Media Face Detector**, you must specify a configuration preset.</span></span> <span data-ttu-id="e2c1e-149">下列組態的預設 hello 指定的 toocreate JSON 根據 hello 情緒偵測。</span><span class="sxs-lookup"><span data-stu-id="e2c1e-149">hello following configuration preset specifies toocreate JSON based on hello emotion detection.</span></span>

    {
      "version": "1.0",
      "options": {
        "aggregateEmotionWindowMs": "987",
        "mode": "aggregateEmotion",
        "aggregateEmotionIntervalMs": "342"
      }
    }


#### <a name="attribute-descriptions"></a><span data-ttu-id="e2c1e-150">屬性描述</span><span class="sxs-lookup"><span data-stu-id="e2c1e-150">Attribute descriptions</span></span>
| <span data-ttu-id="e2c1e-151">屬性名稱</span><span class="sxs-lookup"><span data-stu-id="e2c1e-151">Attribute name</span></span> | <span data-ttu-id="e2c1e-152">說明</span><span class="sxs-lookup"><span data-stu-id="e2c1e-152">Description</span></span> |
| --- | --- |
| <span data-ttu-id="e2c1e-153">模式</span><span class="sxs-lookup"><span data-stu-id="e2c1e-153">Mode</span></span> |<span data-ttu-id="e2c1e-154">Faces：僅臉部偵測。</span><span class="sxs-lookup"><span data-stu-id="e2c1e-154">Faces: Only face detection.</span></span><br/><span data-ttu-id="e2c1e-155">PerFaceEmotion：將每個臉部偵測的情緒單獨傳回。</span><span class="sxs-lookup"><span data-stu-id="e2c1e-155">PerFaceEmotion: Return emotion independently for each face detection.</span></span><br/><span data-ttu-id="e2c1e-156">AggregateEmotion：傳回該畫面中所有臉部的平均情緒值。</span><span class="sxs-lookup"><span data-stu-id="e2c1e-156">AggregateEmotion: Return average emotion values for all faces in frame.</span></span> |
| <span data-ttu-id="e2c1e-157">AggregateEmotionWindowMs</span><span class="sxs-lookup"><span data-stu-id="e2c1e-157">AggregateEmotionWindowMs</span></span> |<span data-ttu-id="e2c1e-158">在已選取 AggregateEmotion 模式時使用。</span><span class="sxs-lookup"><span data-stu-id="e2c1e-158">Use if AggregateEmotion mode selected.</span></span> <span data-ttu-id="e2c1e-159">指定每個彙總的結果視訊使用 tooproduce hello 長度，以毫秒為單位。</span><span class="sxs-lookup"><span data-stu-id="e2c1e-159">Specifies hello length of video used tooproduce each aggregate result, in milliseconds.</span></span> |
| <span data-ttu-id="e2c1e-160">AggregateEmotionIntervalMs</span><span class="sxs-lookup"><span data-stu-id="e2c1e-160">AggregateEmotionIntervalMs</span></span> |<span data-ttu-id="e2c1e-161">在已選取 AggregateEmotion 模式時使用。</span><span class="sxs-lookup"><span data-stu-id="e2c1e-161">Use if AggregateEmotion mode selected.</span></span> <span data-ttu-id="e2c1e-162">指定哪些頻率 tooproduce 彙總結果。</span><span class="sxs-lookup"><span data-stu-id="e2c1e-162">Specifies with what frequency tooproduce aggregate results.</span></span> |

#### <a name="aggregate-defaults"></a><span data-ttu-id="e2c1e-163">彙總預設值</span><span class="sxs-lookup"><span data-stu-id="e2c1e-163">Aggregate defaults</span></span>
<span data-ttu-id="e2c1e-164">以下被建議的 hello 彙總視窗和間隔設定的值。</span><span class="sxs-lookup"><span data-stu-id="e2c1e-164">Below are recommended values for hello aggregate window and interval settings.</span></span> <span data-ttu-id="e2c1e-165">AggregateEmotionWindowMs 應該超過 AggregateEmotionIntervalMs。</span><span class="sxs-lookup"><span data-stu-id="e2c1e-165">AggregateEmotionWindowMs should be longer than AggregateEmotionIntervalMs.</span></span>

|| <span data-ttu-id="e2c1e-166">預設</span><span class="sxs-lookup"><span data-stu-id="e2c1e-166">Defaults(s)</span></span> | <span data-ttu-id="e2c1e-167">最小</span><span class="sxs-lookup"><span data-stu-id="e2c1e-167">Min(s)</span></span> | <span data-ttu-id="e2c1e-168">最大</span><span class="sxs-lookup"><span data-stu-id="e2c1e-168">Max(s)</span></span> |
|--- | --- | --- | --- |
| <span data-ttu-id="e2c1e-169">AggregateEmotionWindowMs</span><span class="sxs-lookup"><span data-stu-id="e2c1e-169">AggregateEmotionWindowMs</span></span> |<span data-ttu-id="e2c1e-170">0.5</span><span class="sxs-lookup"><span data-stu-id="e2c1e-170">0.5</span></span> |<span data-ttu-id="e2c1e-171">2</span><span class="sxs-lookup"><span data-stu-id="e2c1e-171">2</span></span> |<span data-ttu-id="e2c1e-172">0.25</span><span class="sxs-lookup"><span data-stu-id="e2c1e-172">0.25</span></span>|
| <span data-ttu-id="e2c1e-173">AggregateEmotionIntervalMs</span><span class="sxs-lookup"><span data-stu-id="e2c1e-173">AggregateEmotionIntervalMs</span></span> |<span data-ttu-id="e2c1e-174">0.5</span><span class="sxs-lookup"><span data-stu-id="e2c1e-174">0.5</span></span> |<span data-ttu-id="e2c1e-175">1</span><span class="sxs-lookup"><span data-stu-id="e2c1e-175">1</span></span> |<span data-ttu-id="e2c1e-176">0.25</span><span class="sxs-lookup"><span data-stu-id="e2c1e-176">0.25</span></span>|

### <a name="json-output"></a><span data-ttu-id="e2c1e-177">JSON 輸出</span><span class="sxs-lookup"><span data-stu-id="e2c1e-177">JSON output</span></span>
<span data-ttu-id="e2c1e-178">彙總情緒的 JSON 輸出 (已截斷)：</span><span class="sxs-lookup"><span data-stu-id="e2c1e-178">JSON output for aggregate emotion (truncated):</span></span>

    {
     "version": 1,
     "timescale": 30000,
     "offset": 0,
     "framerate": 29.97,
     "width": 1280,
     "height": 720,
     "fragments": [
       {
         "start": 0,
         "duration": 60060,
         "interval": 15015,
         "events": [
           [
             {
               "windowFaceDistribution": {
                 "neutral": 0,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               },
               "windowMeanScores": {
                 "neutral": 0,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               }
             }
           ],
           [
             {
               "windowFaceDistribution": {
                 "neutral": 0,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               },
               "windowMeanScores": {
                 "neutral": 0,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               }
             }
           ],
           [
             {
               "windowFaceDistribution": {
                 "neutral": 0,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               },
               "windowMeanScores": {
                 "neutral": 0,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               }
             }
           ],
           [
             {
               "windowFaceDistribution": {
                 "neutral": 0,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               },
               "windowMeanScores": {
                 "neutral": 0,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               }
             }
           ]
         ]
       },
       {
         "start": 60060,
         "duration": 60060,
         "interval": 15015,
         "events": [
           [
             {
               "windowFaceDistribution": {
                 "neutral": 1,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               },
               "windowMeanScores": {
                 "neutral": 0.688541,
                 "happiness": 0.0586323,
                 "surprise": 0.227184,
                 "sadness": 0.00945675,
                 "anger": 0.00592107,
                 "disgust": 0.00154993,
                 "fear": 0.00450447,
                 "contempt": 0.0042109
               }
             }
           ],
           [
             {
               "windowFaceDistribution": {
                 "neutral": 1,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,

## <a name="limitations"></a><span data-ttu-id="e2c1e-179">限制</span><span class="sxs-lookup"><span data-stu-id="e2c1e-179">Limitations</span></span>
* <span data-ttu-id="e2c1e-180">支援的 hello 輸入視訊格式包括 MP4、 MOV、 和 WMV。</span><span class="sxs-lookup"><span data-stu-id="e2c1e-180">hello supported input video formats include MP4, MOV, and WMV.</span></span>
* <span data-ttu-id="e2c1e-181">hello 偵測臉大小範圍為 24 x 24 too2048x2048 像素。</span><span class="sxs-lookup"><span data-stu-id="e2c1e-181">hello detectable face size range is 24x24 too2048x2048 pixels.</span></span> <span data-ttu-id="e2c1e-182">將不會偵測 hello 字體超出此範圍。</span><span class="sxs-lookup"><span data-stu-id="e2c1e-182">hello faces out of this range will not be detected.</span></span>
* <span data-ttu-id="e2c1e-183">每個視訊，hello 字體傳回的數目上限為 64。</span><span class="sxs-lookup"><span data-stu-id="e2c1e-183">For each video, hello maximum number of faces returned is 64.</span></span>
* <span data-ttu-id="e2c1e-184">因為 tootechnical 挑戰; 可能無法偵測某些字體例如非常大的正面角度 （h e a d-碰到） 和大型阻擋。</span><span class="sxs-lookup"><span data-stu-id="e2c1e-184">Some faces may not be detected due tootechnical challenges; e.g. very large face angles (head-pose), and large occlusion.</span></span> <span data-ttu-id="e2c1e-185">人臉和正面附近的字體有 hello 最佳的結果。</span><span class="sxs-lookup"><span data-stu-id="e2c1e-185">Frontal and near-frontal faces have hello best results.</span></span>

## <a name="net-sample-code"></a><span data-ttu-id="e2c1e-186">.NET 範例程式碼</span><span class="sxs-lookup"><span data-stu-id="e2c1e-186">.NET sample code</span></span>

<span data-ttu-id="e2c1e-187">hello 以下程式顯示如何：</span><span class="sxs-lookup"><span data-stu-id="e2c1e-187">hello following program shows how to:</span></span>

1. <span data-ttu-id="e2c1e-188">建立資產，並將媒體檔案上傳到 hello 資產。</span><span class="sxs-lookup"><span data-stu-id="e2c1e-188">Create an asset and upload a media file into hello asset.</span></span>
2. <span data-ttu-id="e2c1e-189">建立具有工作臉偵測工作，根據包含 hello 下列 json 的預設組態檔。</span><span class="sxs-lookup"><span data-stu-id="e2c1e-189">Create a job with a face detection task based on a configuration file that contains hello following json preset.</span></span> 
   
        {
            "version": "1.0"
        }
3. <span data-ttu-id="e2c1e-190">下載 hello 輸出 JSON 檔案。</span><span class="sxs-lookup"><span data-stu-id="e2c1e-190">Download hello output JSON files.</span></span> 

#### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="e2c1e-191">建立和設定 Visual Studio 專案</span><span class="sxs-lookup"><span data-stu-id="e2c1e-191">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="e2c1e-192">設定您的開發環境，並填入 hello 與連接資訊的 app.config 檔案中所述[與.NET 的 Media Services 開發](media-services-dotnet-how-to-use.md)。</span><span class="sxs-lookup"><span data-stu-id="e2c1e-192">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

#### <a name="example"></a><span data-ttu-id="e2c1e-193">範例</span><span class="sxs-lookup"><span data-stu-id="e2c1e-193">Example</span></span>

    using System;
    using System.Configuration;
    using System.IO;
    using System.Linq;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using System.Threading;
    using System.Threading.Tasks;

    namespace FaceDetection
    {
        class Program
        {
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

                // Run hello FaceDetection job.
                var asset = RunFaceDetectionJob(@"C:\supportFiles\FaceDetection\BigBuckBunny.mp4",
                                            @"C:\supportFiles\FaceDetection\config.json");

                // Download hello job output asset.
                DownloadAsset(asset, @"C:\supportFiles\FaceDetection\Output");
            }

            static IAsset RunFaceDetectionJob(string inputMediaFilePath, string configurationFile)
            {
                // Create an asset and upload hello input media file toostorage.
                IAsset asset = CreateAssetAndUploadSingleFile(inputMediaFilePath,
                    "My Face Detection Input Asset",
                    AssetCreationOptions.None);

                // Declare a new job.
                IJob job = _context.Jobs.Create("My Face Detection Job");

                // Get a reference tooAzure Media Face Detector.
                string MediaProcessorName = "Azure Media Face Detector";

                var processor = GetLatestMediaProcessorByName(MediaProcessorName);

                // Read configuration from hello specified file.
                string configuration = File.ReadAllText(configurationFile);

                // Create a task with hello encoding details, using a string preset.
                ITask task = job.Tasks.AddNew("My Face Detection Task",
                    processor,
                    configuration,
                    TaskOptions.None);

                // Specify hello input asset.
                task.InputAssets.Add(asset);

                // Add an output asset toocontain hello results of hello job.
                task.OutputAssets.AddNew("My Face Detectoion Output Asset", AssetCreationOptions.None);

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

## <a name="media-services-learning-paths"></a><span data-ttu-id="e2c1e-194">媒體服務學習路徑</span><span class="sxs-lookup"><span data-stu-id="e2c1e-194">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="e2c1e-195">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="e2c1e-195">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a><span data-ttu-id="e2c1e-196">相關連結</span><span class="sxs-lookup"><span data-stu-id="e2c1e-196">Related links</span></span>
[<span data-ttu-id="e2c1e-197">Azure 媒體服務分析概觀</span><span class="sxs-lookup"><span data-stu-id="e2c1e-197">Azure Media Services Analytics Overview</span></span>](media-services-analytics-overview.md)

[<span data-ttu-id="e2c1e-198">Azure 媒體分析示範</span><span class="sxs-lookup"><span data-stu-id="e2c1e-198">Azure Media Analytics demos</span></span>](http://amslabs.azurewebsites.net/demos/Analytics.html)

