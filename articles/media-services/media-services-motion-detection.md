---
title: "使用 Azure 媒體分析偵測動作 | Microsoft Docs"
description: "「Azure 媒體動作偵測器」媒體處理器 (MP) 能讓您在冗長且平淡的影片中，有效識別出感興趣的區段。"
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: d144f813-1a55-442f-a895-5c4cb6d0aeae
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/31/2017
ms.author: milanga;juliako;
ms.openlocfilehash: 115ad9dfd88062f23d5d17eed8897ce5d2ca8484
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="detect-motions-with-azure-media-analytics"></a><span data-ttu-id="d4925-103">使用 Azure 媒體分析偵測動作</span><span class="sxs-lookup"><span data-stu-id="d4925-103">Detect Motions with Azure Media Analytics</span></span>
## <a name="overview"></a><span data-ttu-id="d4925-104">概觀</span><span class="sxs-lookup"><span data-stu-id="d4925-104">Overview</span></span>
<span data-ttu-id="d4925-105">**Azure 媒體動作偵測器** 媒體處理器 (MP) 能讓您在冗長且平淡的影片中，有效識別出感興趣的區段。</span><span class="sxs-lookup"><span data-stu-id="d4925-105">The **Azure Media Motion Detector** media processor (MP) enables you to efficiently identify sections of interest within an otherwise long and uneventful video.</span></span> <span data-ttu-id="d4925-106">動作偵測可以用來在靜態攝影機資料上識別影片中有動作發生的區段。</span><span class="sxs-lookup"><span data-stu-id="d4925-106">Motion detection can be used on static camera footage to identify sections of the video where motion occurs.</span></span> <span data-ttu-id="d4925-107">它會產生 JSON 檔案，其中包含具有時間戳記的中繼資料，以及發生事件的週框區域。</span><span class="sxs-lookup"><span data-stu-id="d4925-107">It generates a JSON file containing a metadata with timestamps and the bounding region where the event occurred.</span></span>

<span data-ttu-id="d4925-108">如果將此技術用於監視器的影片輸出，它將能把動作分類為相關事件及誤判情況 (例如陰影或光源變更)。</span><span class="sxs-lookup"><span data-stu-id="d4925-108">Targeted towards security video feeds, this technology is able to categorize motion into relevant events and false positives such as shadows and lighting changes.</span></span> <span data-ttu-id="d4925-109">這能讓您在不用檢視無止境的不相關事件之下，便能從攝影機輸出產生安全性警示，並從時間相當長的監視影片中擷取感興趣的片段。</span><span class="sxs-lookup"><span data-stu-id="d4925-109">This allows you to generate security alerts from camera feeds without being spammed with endless irrelevant events, while being able to extract moments of interest from extremely long surveillance videos.</span></span>

<span data-ttu-id="d4925-110">**Azure 媒體動作偵測器** MP 目前為預覽功能。</span><span class="sxs-lookup"><span data-stu-id="d4925-110">The **Azure Media Motion Detector** MP is currently in Preview.</span></span>

<span data-ttu-id="d4925-111">本主題提供有關 **Azure 媒體動作偵測器**的詳細資料，並示範如何搭配適用於 .NET 的媒體服務 SDK 來使用它。</span><span class="sxs-lookup"><span data-stu-id="d4925-111">This topic gives details about  **Azure Media Motion Detector** and shows how to use it with Media Services SDK for .NET</span></span>

## <a name="motion-detector-input-files"></a><span data-ttu-id="d4925-112">動作偵測器輸入檔案</span><span class="sxs-lookup"><span data-stu-id="d4925-112">Motion Detector input files</span></span>
<span data-ttu-id="d4925-113">影片檔案。</span><span class="sxs-lookup"><span data-stu-id="d4925-113">Video files.</span></span> <span data-ttu-id="d4925-114">目前支援下列格式：MP4、MOV 及 WMV。</span><span class="sxs-lookup"><span data-stu-id="d4925-114">Currently, the following formats are supported: MP4, MOV, and WMV.</span></span>

## <a name="task-configuration-preset"></a><span data-ttu-id="d4925-115">工作組態 (預設)</span><span class="sxs-lookup"><span data-stu-id="d4925-115">Task configuration (preset)</span></span>
<span data-ttu-id="d4925-116">以 **Azure 媒體動作偵測器**建立工作時，您必須指定設定預設值。</span><span class="sxs-lookup"><span data-stu-id="d4925-116">When creating a task with **Azure Media Motion Detector**, you must specify a configuration preset.</span></span> 

### <a name="parameters"></a><span data-ttu-id="d4925-117">參數</span><span class="sxs-lookup"><span data-stu-id="d4925-117">Parameters</span></span>
<span data-ttu-id="d4925-118">您可以使用以下參數：</span><span class="sxs-lookup"><span data-stu-id="d4925-118">You can use the following parameters:</span></span>

| <span data-ttu-id="d4925-119">名稱</span><span class="sxs-lookup"><span data-stu-id="d4925-119">Name</span></span> | <span data-ttu-id="d4925-120">選項</span><span class="sxs-lookup"><span data-stu-id="d4925-120">Options</span></span> | <span data-ttu-id="d4925-121">說明</span><span class="sxs-lookup"><span data-stu-id="d4925-121">Description</span></span> | <span data-ttu-id="d4925-122">預設值</span><span class="sxs-lookup"><span data-stu-id="d4925-122">Default</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="d4925-123">sensitivityLevel</span><span class="sxs-lookup"><span data-stu-id="d4925-123">sensitivityLevel</span></span> |<span data-ttu-id="d4925-124">字串：'low'、'medium'、'high'</span><span class="sxs-lookup"><span data-stu-id="d4925-124">String:'low', 'medium', 'high'</span></span> |<span data-ttu-id="d4925-125">設定要報告哪些動作的敏感度等級。</span><span class="sxs-lookup"><span data-stu-id="d4925-125">Sets the sensitivity level at which motions is reported.</span></span> <span data-ttu-id="d4925-126">調整該項目可調整誤判的數量。</span><span class="sxs-lookup"><span data-stu-id="d4925-126">Adjust this to adjust amount of false positives.</span></span> |<span data-ttu-id="d4925-127">'medium'</span><span class="sxs-lookup"><span data-stu-id="d4925-127">'medium'</span></span> |
| <span data-ttu-id="d4925-128">frameSamplingValue</span><span class="sxs-lookup"><span data-stu-id="d4925-128">frameSamplingValue</span></span> |<span data-ttu-id="d4925-129">正整數</span><span class="sxs-lookup"><span data-stu-id="d4925-129">Positive integer</span></span> |<span data-ttu-id="d4925-130">設定演算法的執行頻率。</span><span class="sxs-lookup"><span data-stu-id="d4925-130">Sets the frequency at which algorithm runs.</span></span> <span data-ttu-id="d4925-131">1 等於每個畫面，2 表示每 2 個畫面，依此類推。</span><span class="sxs-lookup"><span data-stu-id="d4925-131">1 equals every frame, 2 means every 2nd frame, and so on.</span></span> |<span data-ttu-id="d4925-132">1</span><span class="sxs-lookup"><span data-stu-id="d4925-132">1</span></span> |
| <span data-ttu-id="d4925-133">detectLightChange</span><span class="sxs-lookup"><span data-stu-id="d4925-133">detectLightChange</span></span> |<span data-ttu-id="d4925-134">布林值：'true'、'false'</span><span class="sxs-lookup"><span data-stu-id="d4925-134">Boolean:'true', 'false'</span></span> |<span data-ttu-id="d4925-135">設定是否要在結果中報告光源變化</span><span class="sxs-lookup"><span data-stu-id="d4925-135">Sets whether light changes are reported in the results</span></span> |<span data-ttu-id="d4925-136">'False'</span><span class="sxs-lookup"><span data-stu-id="d4925-136">'False'</span></span> |
| <span data-ttu-id="d4925-137">mergeTimeThreshold</span><span class="sxs-lookup"><span data-stu-id="d4925-137">mergeTimeThreshold</span></span> |<span data-ttu-id="d4925-138">Xs-time: Hh:mm:ss</span><span class="sxs-lookup"><span data-stu-id="d4925-138">Xs-time: Hh:mm:ss</span></span><br/><span data-ttu-id="d4925-139">範例：00:00:03</span><span class="sxs-lookup"><span data-stu-id="d4925-139">Example: 00:00:03</span></span> |<span data-ttu-id="d4925-140">指定要將 2 個事件合併及回報為 1 個事件的動作事件時間間隔。</span><span class="sxs-lookup"><span data-stu-id="d4925-140">Specifies the time window between motion events where 2 events will be combined and reported as 1.</span></span> |<span data-ttu-id="d4925-141">00:00:00</span><span class="sxs-lookup"><span data-stu-id="d4925-141">00:00:00</span></span> |
| <span data-ttu-id="d4925-142">detectionZones</span><span class="sxs-lookup"><span data-stu-id="d4925-142">detectionZones</span></span> |<span data-ttu-id="d4925-143">偵測區域的陣列︰</span><span class="sxs-lookup"><span data-stu-id="d4925-143">An array of detection zones:</span></span><br/><span data-ttu-id="d4925-144">- 偵測區域是 3 個或更多個點的陣列</span><span class="sxs-lookup"><span data-stu-id="d4925-144">- Detection Zone is an array of 3 or more points</span></span><br/><span data-ttu-id="d4925-145">- 點是介於 0 到 1 之間的 x 和 y 座標。</span><span class="sxs-lookup"><span data-stu-id="d4925-145">- Point is a x and y coordinate from 0 to 1.</span></span> |<span data-ttu-id="d4925-146">描述要使用的多邊形偵測區域清單。</span><span class="sxs-lookup"><span data-stu-id="d4925-146">Describes the list of polygonal detection zones to be used.</span></span><br/><span data-ttu-id="d4925-147">結果會使用區域為識別碼報告，第一個為 'id':0</span><span class="sxs-lookup"><span data-stu-id="d4925-147">Results will be reported with the zones as an ID, with the first one being 'id':0</span></span> |<span data-ttu-id="d4925-148">涵蓋整個畫面的單一區域。</span><span class="sxs-lookup"><span data-stu-id="d4925-148">Single zone which covers the entire frame.</span></span> |

### <a name="json-example"></a><span data-ttu-id="d4925-149">JSON 範例</span><span class="sxs-lookup"><span data-stu-id="d4925-149">JSON example</span></span>
    {
      "version": "1.0",
      "options": {
        "sensitivityLevel": "medium",
        "frameSamplingValue": 1,
        "detectLightChange": "False",
        "mergeTimeThreshold":
        "00:00:02",
        "detectionZones": [
          [
            {"x": 0, "y": 0},
            {"x": 0.5, "y": 0},
            {"x": 0, "y": 1}
           ],
          [
            {"x": 0.3, "y": 0.3},
            {"x": 0.55, "y": 0.3},
            {"x": 0.8, "y": 0.3},
            {"x": 0.8, "y": 0.55},
            {"x": 0.8, "y": 0.8},
            {"x": 0.55, "y": 0.8},
            {"x": 0.3, "y": 0.8},
            {"x": 0.3, "y": 0.55}
          ]
        ]
      }
    }


## <a name="motion-detector-output-files"></a><span data-ttu-id="d4925-150">動作偵測器輸出檔案</span><span class="sxs-lookup"><span data-stu-id="d4925-150">Motion Detector output files</span></span>
<span data-ttu-id="d4925-151">動作偵測工作會在輸出資產中傳回 JSON 檔案，該檔案會在影片中描述動作警示及類別。</span><span class="sxs-lookup"><span data-stu-id="d4925-151">A motion detection job will return a JSON file in the output asset which describes the motion alerts, and their categories, within the video.</span></span> <span data-ttu-id="d4925-152">檔案將包含在影片中所偵測到動作之時間和持續時間的資訊。</span><span class="sxs-lookup"><span data-stu-id="d4925-152">The file will contain information about the time and duration of motion detected in the video.</span></span>

<span data-ttu-id="d4925-153">動作偵測器 API 會在物件於固定背景的影片 (例如監視影片) 中移動時提供指示器。</span><span class="sxs-lookup"><span data-stu-id="d4925-153">The Motion Detector API provides indicators once there are objects in motion in a fixed background video (e.g. a surveillance video).</span></span> <span data-ttu-id="d4925-154">動作偵測器已針對降低誤判 (例如光源和陰影變化) 進行調整。</span><span class="sxs-lookup"><span data-stu-id="d4925-154">The Motion Detector is trained to reduce false alarms, such as lighting and shadow changes.</span></span> <span data-ttu-id="d4925-155">目前演算法的限制包括夜視影片、半透明物件及小型物件。</span><span class="sxs-lookup"><span data-stu-id="d4925-155">Current limitations of the algorithms include night vision videos, semi-transparent objects, and small objects.</span></span>

### <span data-ttu-id="d4925-156"><a id="output_elements"></a>輸出 JSON 檔案的元素</span><span class="sxs-lookup"><span data-stu-id="d4925-156"><a id="output_elements"></a>Elements of the output JSON file</span></span>
> [!NOTE]
> <span data-ttu-id="d4925-157">在最新版本中，輸出 JSON 格式已變更，而且對某些客戶來說可能代表著重大變更。</span><span class="sxs-lookup"><span data-stu-id="d4925-157">In the latest release, the Output JSON format has changed and may represent a breaking change for some customers.</span></span>
> 
> 

<span data-ttu-id="d4925-158">下表說明輸出 JSON 的元素。</span><span class="sxs-lookup"><span data-stu-id="d4925-158">The following table describes elements of the output JSON file.</span></span>

| <span data-ttu-id="d4925-159">元素</span><span class="sxs-lookup"><span data-stu-id="d4925-159">Element</span></span> | <span data-ttu-id="d4925-160">說明</span><span class="sxs-lookup"><span data-stu-id="d4925-160">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d4925-161">版本</span><span class="sxs-lookup"><span data-stu-id="d4925-161">Version</span></span> |<span data-ttu-id="d4925-162">這是指影片 API 的版本。</span><span class="sxs-lookup"><span data-stu-id="d4925-162">This refers to the version of the Video API.</span></span> <span data-ttu-id="d4925-163">目前版本為 2。</span><span class="sxs-lookup"><span data-stu-id="d4925-163">The current version is 2.</span></span> |
| <span data-ttu-id="d4925-164">時幅</span><span class="sxs-lookup"><span data-stu-id="d4925-164">Timescale</span></span> |<span data-ttu-id="d4925-165">影片每秒的「刻度」數目。</span><span class="sxs-lookup"><span data-stu-id="d4925-165">"Ticks" per second of the video.</span></span> |
| <span data-ttu-id="d4925-166">Offset</span><span class="sxs-lookup"><span data-stu-id="d4925-166">Offset</span></span> |<span data-ttu-id="d4925-167">時間戳記的時間位移 (以「刻度」為單位)。</span><span class="sxs-lookup"><span data-stu-id="d4925-167">The time offset for timestamps in "ticks".</span></span> <span data-ttu-id="d4925-168">在版本 1.0 的影片 API 中，這永遠會是 0。</span><span class="sxs-lookup"><span data-stu-id="d4925-168">In version 1.0 of Video APIs, this will always be 0.</span></span> <span data-ttu-id="d4925-169">在我們於未來將支援的案例中，此值可能會變更。</span><span class="sxs-lookup"><span data-stu-id="d4925-169">In future scenarios we support, this value may change.</span></span> |
| <span data-ttu-id="d4925-170">畫面播放速率</span><span class="sxs-lookup"><span data-stu-id="d4925-170">Framerate</span></span> |<span data-ttu-id="d4925-171">影片的每秒畫面格數。</span><span class="sxs-lookup"><span data-stu-id="d4925-171">Frames per second of the video.</span></span> |
| <span data-ttu-id="d4925-172">寬度，高度</span><span class="sxs-lookup"><span data-stu-id="d4925-172">Width, Height</span></span> |<span data-ttu-id="d4925-173">指的是影片的寬度和高度 (以像素為單位)。</span><span class="sxs-lookup"><span data-stu-id="d4925-173">Refers to the width and height of the video in pixels.</span></span> |
| <span data-ttu-id="d4925-174">啟動</span><span class="sxs-lookup"><span data-stu-id="d4925-174">Start</span></span> |<span data-ttu-id="d4925-175">開始的時間戳記 (以「刻度」為單位)。</span><span class="sxs-lookup"><span data-stu-id="d4925-175">The start timestamp in "ticks".</span></span> |
| <span data-ttu-id="d4925-176">持續時間</span><span class="sxs-lookup"><span data-stu-id="d4925-176">Duration</span></span> |<span data-ttu-id="d4925-177">事件的長度 (以「刻度」為單位)。</span><span class="sxs-lookup"><span data-stu-id="d4925-177">The length of the event, in "ticks".</span></span> |
| <span data-ttu-id="d4925-178">間隔</span><span class="sxs-lookup"><span data-stu-id="d4925-178">Interval</span></span> |<span data-ttu-id="d4925-179">事件中每個項目的間隔 (以「刻度」為單位)。</span><span class="sxs-lookup"><span data-stu-id="d4925-179">The interval of each entry in the event, in "ticks".</span></span> |
| <span data-ttu-id="d4925-180">事件</span><span class="sxs-lookup"><span data-stu-id="d4925-180">Events</span></span> |<span data-ttu-id="d4925-181">每個事件片段皆包含在該持續期間內所偵測到的動作。</span><span class="sxs-lookup"><span data-stu-id="d4925-181">Each event fragment contains the motion detected within that time duration.</span></span> |
| <span data-ttu-id="d4925-182">類型</span><span class="sxs-lookup"><span data-stu-id="d4925-182">Type</span></span> |<span data-ttu-id="d4925-183">在目前的版本中，針對一般動作，這永遠會是「2」。</span><span class="sxs-lookup"><span data-stu-id="d4925-183">In the current version, this is always ‘2’ for generic motion.</span></span> <span data-ttu-id="d4925-184">此標籤可讓影片 API 在未來的版本中能夠彈性地為動作進行分類。</span><span class="sxs-lookup"><span data-stu-id="d4925-184">This label gives Video APIs the flexibility to categorize motion in future versions.</span></span> |
| <span data-ttu-id="d4925-185">RegionID</span><span class="sxs-lookup"><span data-stu-id="d4925-185">RegionID</span></span> |<span data-ttu-id="d4925-186">如前文所述，這在此版本中將永遠會是 0。</span><span class="sxs-lookup"><span data-stu-id="d4925-186">As explained above, this will always be 0 in this version.</span></span> <span data-ttu-id="d4925-187">此標籤可讓影片 API 在未來的版本中能夠彈性地在各個區域中尋找動作。</span><span class="sxs-lookup"><span data-stu-id="d4925-187">This label gives Video API the flexibility to find motion in various regions in future versions.</span></span> |
| <span data-ttu-id="d4925-188">區域</span><span class="sxs-lookup"><span data-stu-id="d4925-188">Regions</span></span> |<span data-ttu-id="d4925-189">指的是影片中您會關心其中所發生之動作的區塊。</span><span class="sxs-lookup"><span data-stu-id="d4925-189">Refers to the area in your video where you care about motion.</span></span> <br/><br/><span data-ttu-id="d4925-190">-「識別碼」表示區域區塊 – 在此版本中只有一個，識別碼為 0。</span><span class="sxs-lookup"><span data-stu-id="d4925-190">-"id" represents the region area – in this version there is only one, ID 0.</span></span> <br/><span data-ttu-id="d4925-191">-「類型」代表您關心動作的區域形狀。</span><span class="sxs-lookup"><span data-stu-id="d4925-191">-"type" represents the shape of the region you care about for motion.</span></span> <span data-ttu-id="d4925-192">目前支援「矩形」和「多邊形」。</span><span class="sxs-lookup"><span data-stu-id="d4925-192">Currently, "rectangle" and "polygon" are supported.</span></span><br/> <span data-ttu-id="d4925-193">如果您指定「矩形」，區域的維度將以 X、Y、寬度及高度表示。</span><span class="sxs-lookup"><span data-stu-id="d4925-193">If you specified "rectangle", the region has dimensions in X, Y, Width, and Height.</span></span> <span data-ttu-id="d4925-194">X 和 Y 座標代表以標準化縮放 (0.0 到 1.0) 顯示之區域左上角的 XY 座標。</span><span class="sxs-lookup"><span data-stu-id="d4925-194">The X and Y coordinates represent the upper left hand XY coordinates of the region in a normalized scale of 0.0 to 1.0.</span></span> <span data-ttu-id="d4925-195">寬度和高度代表以標準化縮放 (0.0 到 1.0) 顯示之區域的大小。</span><span class="sxs-lookup"><span data-stu-id="d4925-195">The width and height represent the size of the region in a normalized scale of 0.0 to 1.0.</span></span> <span data-ttu-id="d4925-196">在目前版本中，X、Y、寬度和高度一律固定為 0, 0 和 1, 1。</span><span class="sxs-lookup"><span data-stu-id="d4925-196">In the current version, X, Y, Width, and Height are always fixed at 0, 0 and 1, 1.</span></span> <br/><span data-ttu-id="d4925-197">如果您指定「多邊形」，區域的維度將以點表示。</span><span class="sxs-lookup"><span data-stu-id="d4925-197">If you specified "polygon", the region has dimensions in points.</span></span> <br/> |
| <span data-ttu-id="d4925-198">片段</span><span class="sxs-lookup"><span data-stu-id="d4925-198">Fragments</span></span> |<span data-ttu-id="d4925-199">中繼資料會被分成稱為「片段」的不同區段。</span><span class="sxs-lookup"><span data-stu-id="d4925-199">The metadata is chunked up into different segments called fragments.</span></span> <span data-ttu-id="d4925-200">每個片段皆包含開始、持續時間、間隔數字及事件。</span><span class="sxs-lookup"><span data-stu-id="d4925-200">Each fragment contains a start, duration, interval number, and event(s).</span></span> <span data-ttu-id="d4925-201">沒有事件的片段，代表在該片段的開始時間和持續時間之間沒有偵測到任何動作。</span><span class="sxs-lookup"><span data-stu-id="d4925-201">A fragment with no events means that no motion was detected during that start time and duration.</span></span> |
| <span data-ttu-id="d4925-202">括號 []</span><span class="sxs-lookup"><span data-stu-id="d4925-202">Brackets []</span></span> |<span data-ttu-id="d4925-203">每個括號皆代表事件中的單一間隔。</span><span class="sxs-lookup"><span data-stu-id="d4925-203">Each bracket represents one interval in the event.</span></span> <span data-ttu-id="d4925-204">如果間隔顯示空白括號，便代表沒有偵測到動作。</span><span class="sxs-lookup"><span data-stu-id="d4925-204">Empty brackets for that interval means that no motion was detected.</span></span> |
| <span data-ttu-id="d4925-205">位置</span><span class="sxs-lookup"><span data-stu-id="d4925-205">locations</span></span> |<span data-ttu-id="d4925-206">這是位在事件下的新項目，它能列出動作的發生位置。</span><span class="sxs-lookup"><span data-stu-id="d4925-206">This new entry under events lists the location where the motion occurred.</span></span> <span data-ttu-id="d4925-207">它比偵測區域更明確。</span><span class="sxs-lookup"><span data-stu-id="d4925-207">This is more specific than the detection zones.</span></span> |

<span data-ttu-id="d4925-208">以下是 JSON 輸出範例</span><span class="sxs-lookup"><span data-stu-id="d4925-208">The following is a JSON output example</span></span>

    {
      "version": 2,
      "timescale": 23976,
      "offset": 0,
      "framerate": 24,
      "width": 1280,
      "height": 720,
      "regions": [
        {
          "id": 0,
          "type": "polygon",
          "points": [{'x': 0, 'y': 0},
            {'x': 0.5, 'y': 0},
            {'x': 0, 'y': 1}]
        }
      ],
      "fragments": [
        {
          "start": 0,
          "duration": 226765
        },
        {
          "start": 226765,
          "duration": 47952,
          "interval": 999,
          "events": [
            [
              {
                "type": 2,
                "typeName": "motion",
                "locations": [
                  {
                    "x": 0.004184,
                    "y": 0.007463,
                    "width": 0.991667,
                    "height": 0.985185
                  }
                ],
                "regionId": 0
              }
            ],

    …
## <a name="limitations"></a><span data-ttu-id="d4925-209">限制</span><span class="sxs-lookup"><span data-stu-id="d4925-209">Limitations</span></span>
* <span data-ttu-id="d4925-210">支援的輸入影片格式包括 MP4、MOV 及 WMV。</span><span class="sxs-lookup"><span data-stu-id="d4925-210">The supported input video formats include MP4, MOV, and WMV.</span></span>
* <span data-ttu-id="d4925-211">動作偵測已針對固定背景的影片最佳化。</span><span class="sxs-lookup"><span data-stu-id="d4925-211">Motion Detection is optimized for stationary background videos.</span></span> <span data-ttu-id="d4925-212">演算法會專注在降低誤判之上，例如光源變化和陰影。</span><span class="sxs-lookup"><span data-stu-id="d4925-212">The algorithm focuses on reducing false alarms, such as lighting changes, and shadows.</span></span>
* <span data-ttu-id="d4925-213">某些動作可能會因技術挑戰而無法偵測，例如夜視影片、半透明物件及小型物件。</span><span class="sxs-lookup"><span data-stu-id="d4925-213">Some motion may not be detected due to technical challenges; e.g. night vision videos, semi-transparent objects, and small objects.</span></span>

## <a name="net-sample-code"></a><span data-ttu-id="d4925-214">.NET 範例程式碼</span><span class="sxs-lookup"><span data-stu-id="d4925-214">.NET sample code</span></span>

<span data-ttu-id="d4925-215">下列程式將示範如何：</span><span class="sxs-lookup"><span data-stu-id="d4925-215">The following program shows how to:</span></span>

1. <span data-ttu-id="d4925-216">建立資產並將媒體檔案上傳到資產。</span><span class="sxs-lookup"><span data-stu-id="d4925-216">Create an asset and upload a media file into the asset.</span></span>
2. <span data-ttu-id="d4925-217">根據包含下列 JSON 預設值的設定檔案，建立執行影片動作偵測工作的作業。</span><span class="sxs-lookup"><span data-stu-id="d4925-217">Create a job with a video motion detection task based on a configuration file that contains the following json preset.</span></span> 
   
        {
          "Version": "1.0",
          "Options": {
            "SensitivityLevel": "medium",
            "FrameSamplingValue": 1,
            "DetectLightChange": "False",
            "MergeTimeThreshold":
            "00:00:02",
            "DetectionZones": [
              [
                {"x": 0, "y": 0},
                {"x": 0.5, "y": 0},
                {"x": 0, "y": 1}
               ],
              [
                {"x": 0.3, "y": 0.3},
                {"x": 0.55, "y": 0.3},
                {"x": 0.8, "y": 0.3},
                {"x": 0.8, "y": 0.55},
                {"x": 0.8, "y": 0.8},
                {"x": 0.55, "y": 0.8},
                {"x": 0.3, "y": 0.8},
                {"x": 0.3, "y": 0.55}
              ]
            ]
          }
        }
3. <span data-ttu-id="d4925-218">下載輸出 JSON 檔案。</span><span class="sxs-lookup"><span data-stu-id="d4925-218">Download the output JSON files.</span></span> 

#### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="d4925-219">建立和設定 Visual Studio 專案</span><span class="sxs-lookup"><span data-stu-id="d4925-219">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="d4925-220">設定您的開發環境並在 app.config 檔案中填入連線資訊，如[使用 .NET 進行 Media Services 開發](media-services-dotnet-how-to-use.md)中所述。</span><span class="sxs-lookup"><span data-stu-id="d4925-220">Set up your development environment and populate the app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

#### <a name="example"></a><span data-ttu-id="d4925-221">範例</span><span class="sxs-lookup"><span data-stu-id="d4925-221">Example</span></span>


    using System;
    using System.Configuration;
    using System.IO;
    using System.Linq;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using System.Threading;
    using System.Threading.Tasks;

    namespace VideoMotionDetection
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

                // Run the VideoMotionDetection job.
                var asset = RunVideoMotionDetectionJob(@"C:\supportFiles\VideoMotionDetection\BigBuckBunny.mp4",
                                            @"C:\supportFiles\VideoMotionDetection\config.json");

                // Download the job output asset.
                DownloadAsset(asset, @"C:\supportFiles\VideoMotionDetection\Output");
            }

            static IAsset RunVideoMotionDetectionJob(string inputMediaFilePath, string configurationFile)
            {
                // Create an asset and upload the input media file to storage.
                IAsset asset = CreateAssetAndUploadSingleFile(inputMediaFilePath,
                    "My Video Motion Detection Input Asset",
                    AssetCreationOptions.None);

                // Declare a new job.
                IJob job = _context.Jobs.Create("My Video Motion Detection Job");

                // Get a reference to Azure Media Motion Detector.
                string MediaProcessorName = "Azure Media Motion Detector";

                var processor = GetLatestMediaProcessorByName(MediaProcessorName);

                // Read configuration from the specified file.
                string configuration = File.ReadAllText(configurationFile);

                // Create a task with the encoding details, using a string preset.
                ITask task = job.Tasks.AddNew("My Video Motion Detection Task",
                    processor,
                    configuration,
                    TaskOptions.None);

                // Specify the input asset.
                task.InputAssets.Add(asset);

                // Add an output asset to contain the results of the job.
                task.OutputAssets.AddNew("My Video Motion Detectoion Output Asset", AssetCreationOptions.None);

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

## <a name="media-services-learning-paths"></a><span data-ttu-id="d4925-222">媒體服務學習路徑</span><span class="sxs-lookup"><span data-stu-id="d4925-222">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="d4925-223">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="d4925-223">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a><span data-ttu-id="d4925-224">相關連結</span><span class="sxs-lookup"><span data-stu-id="d4925-224">Related links</span></span>
[<span data-ttu-id="d4925-225">Azure 媒體服務動作偵測器部落格</span><span class="sxs-lookup"><span data-stu-id="d4925-225">Azure Media Services Motion Detector blog</span></span>](https://azure.microsoft.com/blog/motion-detector-update/)

[<span data-ttu-id="d4925-226">Azure 媒體服務分析概觀</span><span class="sxs-lookup"><span data-stu-id="d4925-226">Azure Media Services Analytics Overview</span></span>](media-services-analytics-overview.md)

[<span data-ttu-id="d4925-227">Azure 媒體分析示範</span><span class="sxs-lookup"><span data-stu-id="d4925-227">Azure Media Analytics demos</span></span>](http://azuremedialabs.azurewebsites.net/demos/Analytics.html)

