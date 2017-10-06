---
title: "使用 Azure 媒體分析 aaaDetect 動作 |Microsoft 文件"
description: "hello Azure 媒體動作偵測器媒體處理器 (MP) 可讓您 tooefficiently 識別有興趣，否則冗長且較為簡單的視訊中的章節。"
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
ms.openlocfilehash: cb431375c92222053ed2239dd4e45767524dab68
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="detect-motions-with-azure-media-analytics"></a><span data-ttu-id="e99c6-103">使用 Azure 媒體分析偵測動作</span><span class="sxs-lookup"><span data-stu-id="e99c6-103">Detect Motions with Azure Media Analytics</span></span>
## <a name="overview"></a><span data-ttu-id="e99c6-104">概觀</span><span class="sxs-lookup"><span data-stu-id="e99c6-104">Overview</span></span>
<span data-ttu-id="e99c6-105">hello **Azure 媒體動作偵測器**媒體處理器 (MP) 可讓您 tooefficiently 識別有興趣，否則冗長且較為簡單的視訊中的章節。</span><span class="sxs-lookup"><span data-stu-id="e99c6-105">hello **Azure Media Motion Detector** media processor (MP) enables you tooefficiently identify sections of interest within an otherwise long and uneventful video.</span></span> <span data-ttu-id="e99c6-106">影片偵測可用靜態攝影機錄影畫面 tooidentify 部分的 hello 視訊動作發生的位置。</span><span class="sxs-lookup"><span data-stu-id="e99c6-106">Motion detection can be used on static camera footage tooidentify sections of hello video where motion occurs.</span></span> <span data-ttu-id="e99c6-107">它會產生包含時間戳記與 hello 週框 hello 事件發生的位置 （地區） 的中繼資料的 JSON 檔案。</span><span class="sxs-lookup"><span data-stu-id="e99c6-107">It generates a JSON file containing a metadata with timestamps and hello bounding region where hello event occurred.</span></span>

<span data-ttu-id="e99c6-108">針對安全性視訊摘要，此技術是無法 toocategorize 移動到相關的事件，例如陰影和光源處理變更的誤判。</span><span class="sxs-lookup"><span data-stu-id="e99c6-108">Targeted towards security video feeds, this technology is able toocategorize motion into relevant events and false positives such as shadows and lighting changes.</span></span> <span data-ttu-id="e99c6-109">可以讓您從相機摘要 toogenerate 安全性警示，沒有與無止盡不相關的事件，同時會無法 tooextract 分鐘的時間很長的監視視訊從感興趣的垃圾信件。</span><span class="sxs-lookup"><span data-stu-id="e99c6-109">This allows you toogenerate security alerts from camera feeds without being spammed with endless irrelevant events, while being able tooextract moments of interest from extremely long surveillance videos.</span></span>

<span data-ttu-id="e99c6-110">hello **Azure 媒體動作偵測器**MP 目前為預覽狀態。</span><span class="sxs-lookup"><span data-stu-id="e99c6-110">hello **Azure Media Motion Detector** MP is currently in Preview.</span></span>

<span data-ttu-id="e99c6-111">本主題詳細說明有關**Azure 媒體動作偵測器**，並示範如何 toouse 使用 Media Services SDK for.NET</span><span class="sxs-lookup"><span data-stu-id="e99c6-111">This topic gives details about  **Azure Media Motion Detector** and shows how toouse it with Media Services SDK for .NET</span></span>

## <a name="motion-detector-input-files"></a><span data-ttu-id="e99c6-112">動作偵測器輸入檔案</span><span class="sxs-lookup"><span data-stu-id="e99c6-112">Motion Detector input files</span></span>
<span data-ttu-id="e99c6-113">影片檔案。</span><span class="sxs-lookup"><span data-stu-id="e99c6-113">Video files.</span></span> <span data-ttu-id="e99c6-114">目前支援下列格式的 hello: MP4、 MOV、 和 WMV。</span><span class="sxs-lookup"><span data-stu-id="e99c6-114">Currently, hello following formats are supported: MP4, MOV, and WMV.</span></span>

## <a name="task-configuration-preset"></a><span data-ttu-id="e99c6-115">工作組態 (預設)</span><span class="sxs-lookup"><span data-stu-id="e99c6-115">Task configuration (preset)</span></span>
<span data-ttu-id="e99c6-116">以 **Azure 媒體動作偵測器**建立工作時，您必須指定設定預設值。</span><span class="sxs-lookup"><span data-stu-id="e99c6-116">When creating a task with **Azure Media Motion Detector**, you must specify a configuration preset.</span></span> 

### <a name="parameters"></a><span data-ttu-id="e99c6-117">參數</span><span class="sxs-lookup"><span data-stu-id="e99c6-117">Parameters</span></span>
<span data-ttu-id="e99c6-118">您可以使用下列參數的 hello:</span><span class="sxs-lookup"><span data-stu-id="e99c6-118">You can use hello following parameters:</span></span>

| <span data-ttu-id="e99c6-119">名稱</span><span class="sxs-lookup"><span data-stu-id="e99c6-119">Name</span></span> | <span data-ttu-id="e99c6-120">選項</span><span class="sxs-lookup"><span data-stu-id="e99c6-120">Options</span></span> | <span data-ttu-id="e99c6-121">說明</span><span class="sxs-lookup"><span data-stu-id="e99c6-121">Description</span></span> | <span data-ttu-id="e99c6-122">預設值</span><span class="sxs-lookup"><span data-stu-id="e99c6-122">Default</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="e99c6-123">sensitivityLevel</span><span class="sxs-lookup"><span data-stu-id="e99c6-123">sensitivityLevel</span></span> |<span data-ttu-id="e99c6-124">字串：'low'、'medium'、'high'</span><span class="sxs-lookup"><span data-stu-id="e99c6-124">String:'low', 'medium', 'high'</span></span> |<span data-ttu-id="e99c6-125">在哪些動作會報告設定 hello 敏感度層級。</span><span class="sxs-lookup"><span data-stu-id="e99c6-125">Sets hello sensitivity level at which motions is reported.</span></span> <span data-ttu-id="e99c6-126">調整這個 tooadjust 數量誤判。</span><span class="sxs-lookup"><span data-stu-id="e99c6-126">Adjust this tooadjust amount of false positives.</span></span> |<span data-ttu-id="e99c6-127">'medium'</span><span class="sxs-lookup"><span data-stu-id="e99c6-127">'medium'</span></span> |
| <span data-ttu-id="e99c6-128">frameSamplingValue</span><span class="sxs-lookup"><span data-stu-id="e99c6-128">frameSamplingValue</span></span> |<span data-ttu-id="e99c6-129">正整數</span><span class="sxs-lookup"><span data-stu-id="e99c6-129">Positive integer</span></span> |<span data-ttu-id="e99c6-130">在哪些演算法回合設定 hello 頻率。</span><span class="sxs-lookup"><span data-stu-id="e99c6-130">Sets hello frequency at which algorithm runs.</span></span> <span data-ttu-id="e99c6-131">1 等於每個畫面，2 表示每 2 個畫面，依此類推。</span><span class="sxs-lookup"><span data-stu-id="e99c6-131">1 equals every frame, 2 means every 2nd frame, and so on.</span></span> |<span data-ttu-id="e99c6-132">1</span><span class="sxs-lookup"><span data-stu-id="e99c6-132">1</span></span> |
| <span data-ttu-id="e99c6-133">detectLightChange</span><span class="sxs-lookup"><span data-stu-id="e99c6-133">detectLightChange</span></span> |<span data-ttu-id="e99c6-134">布林值：'true'、'false'</span><span class="sxs-lookup"><span data-stu-id="e99c6-134">Boolean:'true', 'false'</span></span> |<span data-ttu-id="e99c6-135">設定是否 hello 結果中會報告淺的變更</span><span class="sxs-lookup"><span data-stu-id="e99c6-135">Sets whether light changes are reported in hello results</span></span> |<span data-ttu-id="e99c6-136">'False'</span><span class="sxs-lookup"><span data-stu-id="e99c6-136">'False'</span></span> |
| <span data-ttu-id="e99c6-137">mergeTimeThreshold</span><span class="sxs-lookup"><span data-stu-id="e99c6-137">mergeTimeThreshold</span></span> |<span data-ttu-id="e99c6-138">Xs-time: Hh:mm:ss</span><span class="sxs-lookup"><span data-stu-id="e99c6-138">Xs-time: Hh:mm:ss</span></span><br/><span data-ttu-id="e99c6-139">範例：00:00:03</span><span class="sxs-lookup"><span data-stu-id="e99c6-139">Example: 00:00:03</span></span> |<span data-ttu-id="e99c6-140">指定 hello 影片事件結合並回報為 1 2 個事件之間的時間間隔。</span><span class="sxs-lookup"><span data-stu-id="e99c6-140">Specifies hello time window between motion events where 2 events will be combined and reported as 1.</span></span> |<span data-ttu-id="e99c6-141">00:00:00</span><span class="sxs-lookup"><span data-stu-id="e99c6-141">00:00:00</span></span> |
| <span data-ttu-id="e99c6-142">detectionZones</span><span class="sxs-lookup"><span data-stu-id="e99c6-142">detectionZones</span></span> |<span data-ttu-id="e99c6-143">偵測區域的陣列︰</span><span class="sxs-lookup"><span data-stu-id="e99c6-143">An array of detection zones:</span></span><br/><span data-ttu-id="e99c6-144">- 偵測區域是 3 個或更多個點的陣列</span><span class="sxs-lookup"><span data-stu-id="e99c6-144">- Detection Zone is an array of 3 or more points</span></span><br/><span data-ttu-id="e99c6-145">點是 x 和 y 座標，從 0 too1。</span><span class="sxs-lookup"><span data-stu-id="e99c6-145">- Point is a x and y coordinate from 0 too1.</span></span> |<span data-ttu-id="e99c6-146">描述使用多邊形偵測區域 toobe hello 清單。</span><span class="sxs-lookup"><span data-stu-id="e99c6-146">Describes hello list of polygonal detection zones toobe used.</span></span><br/><span data-ttu-id="e99c6-147">會使用 hello 區域報告結果，做為識別碼，以第一個是 'id' hello: 0</span><span class="sxs-lookup"><span data-stu-id="e99c6-147">Results will be reported with hello zones as an ID, with hello first one being 'id':0</span></span> |<span data-ttu-id="e99c6-148">其中涵蓋了 hello 整個框架的單一區域。</span><span class="sxs-lookup"><span data-stu-id="e99c6-148">Single zone which covers hello entire frame.</span></span> |

### <a name="json-example"></a><span data-ttu-id="e99c6-149">JSON 範例</span><span class="sxs-lookup"><span data-stu-id="e99c6-149">JSON example</span></span>
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


## <a name="motion-detector-output-files"></a><span data-ttu-id="e99c6-150">動作偵測器輸出檔案</span><span class="sxs-lookup"><span data-stu-id="e99c6-150">Motion Detector output files</span></span>
<span data-ttu-id="e99c6-151">影片偵測作業會傳回 JSON 檔案中會描述 hello 影片警示和其類別，在 hello 視訊 hello 輸出資產。</span><span class="sxs-lookup"><span data-stu-id="e99c6-151">A motion detection job will return a JSON file in hello output asset which describes hello motion alerts, and their categories, within hello video.</span></span> <span data-ttu-id="e99c6-152">hello 檔案會包含有關 hello 時間和持續時間的移動 hello 視訊中偵測到的資訊。</span><span class="sxs-lookup"><span data-stu-id="e99c6-152">hello file will contain information about hello time and duration of motion detected in hello video.</span></span>

<span data-ttu-id="e99c6-153">hello 影片偵測器 API 提供指標，當物件在影片中有固定的背景影像 （例如監視視訊）。</span><span class="sxs-lookup"><span data-stu-id="e99c6-153">hello Motion Detector API provides indicators once there are objects in motion in a fixed background video (e.g. a surveillance video).</span></span> <span data-ttu-id="e99c6-154">hello 動作偵測器是定型的 tooreduce false 警示，例如光源和陰影變更。</span><span class="sxs-lookup"><span data-stu-id="e99c6-154">hello Motion Detector is trained tooreduce false alarms, such as lighting and shadow changes.</span></span> <span data-ttu-id="e99c6-155">目前限制的 hello 演算法包括晚上願景影片、 半透明效果的物件和小型物件。</span><span class="sxs-lookup"><span data-stu-id="e99c6-155">Current limitations of hello algorithms include night vision videos, semi-transparent objects, and small objects.</span></span>

### <span data-ttu-id="e99c6-156"><a id="output_elements"></a>Hello 輸出 JSON 檔案的項目</span><span class="sxs-lookup"><span data-stu-id="e99c6-156"><a id="output_elements"></a>Elements of hello output JSON file</span></span>
> [!NOTE]
> <span data-ttu-id="e99c6-157">在 hello 最新版本中，hello 輸出 JSON 格式已變更，可能會對某些客戶代表是重大變更。</span><span class="sxs-lookup"><span data-stu-id="e99c6-157">In hello latest release, hello Output JSON format has changed and may represent a breaking change for some customers.</span></span>
> 
> 

<span data-ttu-id="e99c6-158">hello 下表說明 hello 輸出 JSON 檔案的項目。</span><span class="sxs-lookup"><span data-stu-id="e99c6-158">hello following table describes elements of hello output JSON file.</span></span>

| <span data-ttu-id="e99c6-159">元素</span><span class="sxs-lookup"><span data-stu-id="e99c6-159">Element</span></span> | <span data-ttu-id="e99c6-160">說明</span><span class="sxs-lookup"><span data-stu-id="e99c6-160">Description</span></span> |
| --- | --- |
| <span data-ttu-id="e99c6-161">版本</span><span class="sxs-lookup"><span data-stu-id="e99c6-161">Version</span></span> |<span data-ttu-id="e99c6-162">這是指 toohello 版的 hello 視訊應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="e99c6-162">This refers toohello version of hello Video API.</span></span> <span data-ttu-id="e99c6-163">hello 目前版本為 2。</span><span class="sxs-lookup"><span data-stu-id="e99c6-163">hello current version is 2.</span></span> |
| <span data-ttu-id="e99c6-164">時幅</span><span class="sxs-lookup"><span data-stu-id="e99c6-164">Timescale</span></span> |<span data-ttu-id="e99c6-165">「 滴答 」 每秒的 hello 視訊。</span><span class="sxs-lookup"><span data-stu-id="e99c6-165">"Ticks" per second of hello video.</span></span> |
| <span data-ttu-id="e99c6-166">Offset</span><span class="sxs-lookup"><span data-stu-id="e99c6-166">Offset</span></span> |<span data-ttu-id="e99c6-167">hello 「 滴答 」 中的時間戳記的時間位移。</span><span class="sxs-lookup"><span data-stu-id="e99c6-167">hello time offset for timestamps in "ticks".</span></span> <span data-ttu-id="e99c6-168">在版本 1.0 的影片 API 中，這永遠會是 0。</span><span class="sxs-lookup"><span data-stu-id="e99c6-168">In version 1.0 of Video APIs, this will always be 0.</span></span> <span data-ttu-id="e99c6-169">在我們於未來將支援的案例中，此值可能會變更。</span><span class="sxs-lookup"><span data-stu-id="e99c6-169">In future scenarios we support, this value may change.</span></span> |
| <span data-ttu-id="e99c6-170">畫面播放速率</span><span class="sxs-lookup"><span data-stu-id="e99c6-170">Framerate</span></span> |<span data-ttu-id="e99c6-171">每秒的 hello 視訊畫面。</span><span class="sxs-lookup"><span data-stu-id="e99c6-171">Frames per second of hello video.</span></span> |
| <span data-ttu-id="e99c6-172">寬度，高度</span><span class="sxs-lookup"><span data-stu-id="e99c6-172">Width, Height</span></span> |<span data-ttu-id="e99c6-173">是指 toohello 寬度和高度 hello 視訊像素為單位。</span><span class="sxs-lookup"><span data-stu-id="e99c6-173">Refers toohello width and height of hello video in pixels.</span></span> |
| <span data-ttu-id="e99c6-174">Start</span><span class="sxs-lookup"><span data-stu-id="e99c6-174">Start</span></span> |<span data-ttu-id="e99c6-175">hello 開始 「 滴答 」 中的時間戳記。</span><span class="sxs-lookup"><span data-stu-id="e99c6-175">hello start timestamp in "ticks".</span></span> |
| <span data-ttu-id="e99c6-176">Duration</span><span class="sxs-lookup"><span data-stu-id="e99c6-176">Duration</span></span> |<span data-ttu-id="e99c6-177">hello 事件，請在 「 滴答 」 hello 長度。</span><span class="sxs-lookup"><span data-stu-id="e99c6-177">hello length of hello event, in "ticks".</span></span> |
| <span data-ttu-id="e99c6-178">間隔</span><span class="sxs-lookup"><span data-stu-id="e99c6-178">Interval</span></span> |<span data-ttu-id="e99c6-179">hello 間隔 hello 事件，請在 「 滴答 」 中的每個項目。</span><span class="sxs-lookup"><span data-stu-id="e99c6-179">hello interval of each entry in hello event, in "ticks".</span></span> |
| <span data-ttu-id="e99c6-180">事件</span><span class="sxs-lookup"><span data-stu-id="e99c6-180">Events</span></span> |<span data-ttu-id="e99c6-181">每個事件片段包含該持續時間內偵測到的 hello 影片。</span><span class="sxs-lookup"><span data-stu-id="e99c6-181">Each event fragment contains hello motion detected within that time duration.</span></span> |
| <span data-ttu-id="e99c6-182">類型</span><span class="sxs-lookup"><span data-stu-id="e99c6-182">Type</span></span> |<span data-ttu-id="e99c6-183">在 hello 目前版本中，這一律是 '2' 的泛型影片。</span><span class="sxs-lookup"><span data-stu-id="e99c6-183">In hello current version, this is always ‘2’ for generic motion.</span></span> <span data-ttu-id="e99c6-184">此標籤會提供在未來版本中視訊 Api hello 彈性 toocategorize 影片。</span><span class="sxs-lookup"><span data-stu-id="e99c6-184">This label gives Video APIs hello flexibility toocategorize motion in future versions.</span></span> |
| <span data-ttu-id="e99c6-185">RegionID</span><span class="sxs-lookup"><span data-stu-id="e99c6-185">RegionID</span></span> |<span data-ttu-id="e99c6-186">如前文所述，這在此版本中將永遠會是 0。</span><span class="sxs-lookup"><span data-stu-id="e99c6-186">As explained above, this will always be 0 in this version.</span></span> <span data-ttu-id="e99c6-187">此標籤可讓視訊 API hello 彈性 toofind 動作的未來版本中的各個區域。</span><span class="sxs-lookup"><span data-stu-id="e99c6-187">This label gives Video API hello flexibility toofind motion in various regions in future versions.</span></span> |
| <span data-ttu-id="e99c6-188">區域</span><span class="sxs-lookup"><span data-stu-id="e99c6-188">Regions</span></span> |<span data-ttu-id="e99c6-189">是指 toohello 區域在視訊中的關心影片。</span><span class="sxs-lookup"><span data-stu-id="e99c6-189">Refers toohello area in your video where you care about motion.</span></span> <br/><br/><span data-ttu-id="e99c6-190">-「 識別碼 」 代表 hello 區 – 在此版本中都只有一個，識別碼為 0。</span><span class="sxs-lookup"><span data-stu-id="e99c6-190">-"id" represents hello region area – in this version there is only one, ID 0.</span></span> <br/><span data-ttu-id="e99c6-191">-「 類型 」 代表 hello 圖形的 hello 關心影片的區域。</span><span class="sxs-lookup"><span data-stu-id="e99c6-191">-"type" represents hello shape of hello region you care about for motion.</span></span> <span data-ttu-id="e99c6-192">目前支援「矩形」和「多邊形」。</span><span class="sxs-lookup"><span data-stu-id="e99c6-192">Currently, "rectangle" and "polygon" are supported.</span></span><br/> <span data-ttu-id="e99c6-193">如果您指定 「 矩形 」，hello 區具有維度的 x、 Y、 寬度和高度。</span><span class="sxs-lookup"><span data-stu-id="e99c6-193">If you specified "rectangle", hello region has dimensions in X, Y, Width, and Height.</span></span> <span data-ttu-id="e99c6-194">hello X 和 Y 座標代表 hello 左上 XY 座標的正規化的小數位數為 0.0 too1.0 中的 hello 區域。</span><span class="sxs-lookup"><span data-stu-id="e99c6-194">hello X and Y coordinates represent hello upper left hand XY coordinates of hello region in a normalized scale of 0.0 too1.0.</span></span> <span data-ttu-id="e99c6-195">hello 寬度和高度代表 hello 正規化的小數位數為 0.0 too1.0 中的 hello 區域大小。</span><span class="sxs-lookup"><span data-stu-id="e99c6-195">hello width and height represent hello size of hello region in a normalized scale of 0.0 too1.0.</span></span> <span data-ttu-id="e99c6-196">在 hello 目前版本中，X、 Y、 寬度和高度都一律固定為 0，0，1，1。</span><span class="sxs-lookup"><span data-stu-id="e99c6-196">In hello current version, X, Y, Width, and Height are always fixed at 0, 0 and 1, 1.</span></span> <br/><span data-ttu-id="e99c6-197">如果您指定 「 多邊形 」，hello 地區會有維度以點為單位。</span><span class="sxs-lookup"><span data-stu-id="e99c6-197">If you specified "polygon", hello region has dimensions in points.</span></span> <br/> |
| <span data-ttu-id="e99c6-198">片段</span><span class="sxs-lookup"><span data-stu-id="e99c6-198">Fragments</span></span> |<span data-ttu-id="e99c6-199">到不同的區段，稱為片段 hello 中繼資料區塊上處理。</span><span class="sxs-lookup"><span data-stu-id="e99c6-199">hello metadata is chunked up into different segments called fragments.</span></span> <span data-ttu-id="e99c6-200">每個片段皆包含開始、持續時間、間隔數字及事件。</span><span class="sxs-lookup"><span data-stu-id="e99c6-200">Each fragment contains a start, duration, interval number, and event(s).</span></span> <span data-ttu-id="e99c6-201">沒有事件的片段，代表在該片段的開始時間和持續時間之間沒有偵測到任何動作。</span><span class="sxs-lookup"><span data-stu-id="e99c6-201">A fragment with no events means that no motion was detected during that start time and duration.</span></span> |
| <span data-ttu-id="e99c6-202">括號 []</span><span class="sxs-lookup"><span data-stu-id="e99c6-202">Brackets []</span></span> |<span data-ttu-id="e99c6-203">每個括號表示 hello 事件中的一個時間間隔。</span><span class="sxs-lookup"><span data-stu-id="e99c6-203">Each bracket represents one interval in hello event.</span></span> <span data-ttu-id="e99c6-204">如果間隔顯示空白括號，便代表沒有偵測到動作。</span><span class="sxs-lookup"><span data-stu-id="e99c6-204">Empty brackets for that interval means that no motion was detected.</span></span> |
| <span data-ttu-id="e99c6-205">位置</span><span class="sxs-lookup"><span data-stu-id="e99c6-205">locations</span></span> |<span data-ttu-id="e99c6-206">這個新的項目，[事件] 底下列出 hello hello 動作發生所在的位置。</span><span class="sxs-lookup"><span data-stu-id="e99c6-206">This new entry under events lists hello location where hello motion occurred.</span></span> <span data-ttu-id="e99c6-207">這是比 hello 偵測區域更明確。</span><span class="sxs-lookup"><span data-stu-id="e99c6-207">This is more specific than hello detection zones.</span></span> |

<span data-ttu-id="e99c6-208">hello 以下是 JSON 輸出範例</span><span class="sxs-lookup"><span data-stu-id="e99c6-208">hello following is a JSON output example</span></span>

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
## <a name="limitations"></a><span data-ttu-id="e99c6-209">限制</span><span class="sxs-lookup"><span data-stu-id="e99c6-209">Limitations</span></span>
* <span data-ttu-id="e99c6-210">支援的 hello 輸入視訊格式包括 MP4、 MOV、 和 WMV。</span><span class="sxs-lookup"><span data-stu-id="e99c6-210">hello supported input video formats include MP4, MOV, and WMV.</span></span>
* <span data-ttu-id="e99c6-211">動作偵測已針對固定背景的影片最佳化。</span><span class="sxs-lookup"><span data-stu-id="e99c6-211">Motion Detection is optimized for stationary background videos.</span></span> <span data-ttu-id="e99c6-212">hello 演算法著重於減少錯誤的警示，例如光源變更和陰影。</span><span class="sxs-lookup"><span data-stu-id="e99c6-212">hello algorithm focuses on reducing false alarms, such as lighting changes, and shadows.</span></span>
* <span data-ttu-id="e99c6-213">某些影片可能無法偵測 tootechnical 挑戰; 到期例如晚上願景影片、 半透明效果的物件和小型物件。</span><span class="sxs-lookup"><span data-stu-id="e99c6-213">Some motion may not be detected due tootechnical challenges; e.g. night vision videos, semi-transparent objects, and small objects.</span></span>

## <a name="net-sample-code"></a><span data-ttu-id="e99c6-214">.NET 範例程式碼</span><span class="sxs-lookup"><span data-stu-id="e99c6-214">.NET sample code</span></span>

<span data-ttu-id="e99c6-215">hello 以下程式顯示如何：</span><span class="sxs-lookup"><span data-stu-id="e99c6-215">hello following program shows how to:</span></span>

1. <span data-ttu-id="e99c6-216">建立資產，並將媒體檔案上傳到 hello 資產。</span><span class="sxs-lookup"><span data-stu-id="e99c6-216">Create an asset and upload a media file into hello asset.</span></span>
2. <span data-ttu-id="e99c6-217">建立具有工作影片的影片偵測工作，根據包含 hello 下列 json 的預設組態檔。</span><span class="sxs-lookup"><span data-stu-id="e99c6-217">Create a job with a video motion detection task based on a configuration file that contains hello following json preset.</span></span> 
   
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
3. <span data-ttu-id="e99c6-218">下載 hello 輸出 JSON 檔案。</span><span class="sxs-lookup"><span data-stu-id="e99c6-218">Download hello output JSON files.</span></span> 

#### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="e99c6-219">建立和設定 Visual Studio 專案</span><span class="sxs-lookup"><span data-stu-id="e99c6-219">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="e99c6-220">設定您的開發環境，並填入 hello 與連接資訊的 app.config 檔案中所述[與.NET 的 Media Services 開發](media-services-dotnet-how-to-use.md)。</span><span class="sxs-lookup"><span data-stu-id="e99c6-220">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

#### <a name="example"></a><span data-ttu-id="e99c6-221">範例</span><span class="sxs-lookup"><span data-stu-id="e99c6-221">Example</span></span>


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

                // Run hello VideoMotionDetection job.
                var asset = RunVideoMotionDetectionJob(@"C:\supportFiles\VideoMotionDetection\BigBuckBunny.mp4",
                                            @"C:\supportFiles\VideoMotionDetection\config.json");

                // Download hello job output asset.
                DownloadAsset(asset, @"C:\supportFiles\VideoMotionDetection\Output");
            }

            static IAsset RunVideoMotionDetectionJob(string inputMediaFilePath, string configurationFile)
            {
                // Create an asset and upload hello input media file toostorage.
                IAsset asset = CreateAssetAndUploadSingleFile(inputMediaFilePath,
                    "My Video Motion Detection Input Asset",
                    AssetCreationOptions.None);

                // Declare a new job.
                IJob job = _context.Jobs.Create("My Video Motion Detection Job");

                // Get a reference tooAzure Media Motion Detector.
                string MediaProcessorName = "Azure Media Motion Detector";

                var processor = GetLatestMediaProcessorByName(MediaProcessorName);

                // Read configuration from hello specified file.
                string configuration = File.ReadAllText(configurationFile);

                // Create a task with hello encoding details, using a string preset.
                ITask task = job.Tasks.AddNew("My Video Motion Detection Task",
                    processor,
                    configuration,
                    TaskOptions.None);

                // Specify hello input asset.
                task.InputAssets.Add(asset);

                // Add an output asset toocontain hello results of hello job.
                task.OutputAssets.AddNew("My Video Motion Detectoion Output Asset", AssetCreationOptions.None);

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

## <a name="media-services-learning-paths"></a><span data-ttu-id="e99c6-222">媒體服務學習路徑</span><span class="sxs-lookup"><span data-stu-id="e99c6-222">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="e99c6-223">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="e99c6-223">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a><span data-ttu-id="e99c6-224">相關連結</span><span class="sxs-lookup"><span data-stu-id="e99c6-224">Related links</span></span>
[<span data-ttu-id="e99c6-225">Azure 媒體服務動作偵測器部落格</span><span class="sxs-lookup"><span data-stu-id="e99c6-225">Azure Media Services Motion Detector blog</span></span>](https://azure.microsoft.com/blog/motion-detector-update/)

[<span data-ttu-id="e99c6-226">Azure 媒體服務分析概觀</span><span class="sxs-lookup"><span data-stu-id="e99c6-226">Azure Media Services Analytics Overview</span></span>](media-services-analytics-overview.md)

[<span data-ttu-id="e99c6-227">Azure 媒體分析示範</span><span class="sxs-lookup"><span data-stu-id="e99c6-227">Azure Media Analytics demos</span></span>](http://azuremedialabs.azurewebsites.net/demos/Analytics.html)

