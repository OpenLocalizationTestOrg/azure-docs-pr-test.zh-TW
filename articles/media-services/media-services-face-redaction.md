---
title: "使用 Azure 媒體分析 aaaRedact 字體 |Microsoft 文件"
description: "本主題示範使用 Azure media analytics tooredact 面臨的方式。"
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 5b6d8b8c-5f4d-4fef-b3d6-dc22c6b5a0f5
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/31/2017
ms.author: juliako;
ms.openlocfilehash: 1f5688a8c6374151c526a9c702b904d8c3e46164
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="redact-faces-with-azure-media-analytics"></a><span data-ttu-id="037ff-103">使用 Azure 媒體分析修訂臉部</span><span class="sxs-lookup"><span data-stu-id="037ff-103">Redact faces with Azure Media Analytics</span></span>
## <a name="overview"></a><span data-ttu-id="037ff-104">概觀</span><span class="sxs-lookup"><span data-stu-id="037ff-104">Overview</span></span>
<span data-ttu-id="037ff-105">**Azure 媒體 Redactor**是[Azure 媒體分析](media-services-analytics-overview.md)提供可擴充的字體 redaction hello 雲端中的媒體處理器 (MP)。</span><span class="sxs-lookup"><span data-stu-id="037ff-105">**Azure Media Redactor** is an [Azure Media Analytics](media-services-analytics-overview.md) media processor (MP) that offers scalable face redaction in hello cloud.</span></span> <span data-ttu-id="037ff-106">字體 redaction 可讓您 toomodify 順序 tooblur 表面選取個人視訊。</span><span class="sxs-lookup"><span data-stu-id="037ff-106">Face redaction enables you toomodify your video in order tooblur faces of selected individuals.</span></span> <span data-ttu-id="037ff-107">您可以在公用的安全性和新聞媒體案例 toouse hello 朝 redaction 服務。</span><span class="sxs-lookup"><span data-stu-id="037ff-107">You may want toouse hello face redaction service in public safety and news media scenarios.</span></span> <span data-ttu-id="037ff-108">幾分鐘的影片，其中包含多個字型都會小時 tooredact 以手動方式，但具有此服務的 hello 圖示 redaction 程序將需要幾個簡單的步驟。</span><span class="sxs-lookup"><span data-stu-id="037ff-108">A few minutes of footage that contains multiple faces can take hours tooredact manually, but with this service hello face redaction process will require just a few simple steps.</span></span> <span data-ttu-id="037ff-109">如需詳細資訊，請參閱[此](https://azure.microsoft.com/blog/azure-media-redactor/)部落格。</span><span class="sxs-lookup"><span data-stu-id="037ff-109">For  more information, see [this](https://azure.microsoft.com/blog/azure-media-redactor/) blog.</span></span>

<span data-ttu-id="037ff-110">本主題詳細說明有關**Azure 媒體 Redactor** ，並示範如何 toouse 使用 Media Services SDK for.NET。</span><span class="sxs-lookup"><span data-stu-id="037ff-110">This topic gives details about **Azure Media Redactor** and shows how toouse it with Media Services SDK for .NET.</span></span>

<span data-ttu-id="037ff-111">hello **Azure 媒體 Redactor** MP 目前為預覽狀態。</span><span class="sxs-lookup"><span data-stu-id="037ff-111">hello **Azure Media Redactor** MP is currently in Preview.</span></span> <span data-ttu-id="037ff-112">在所有公開的 Azure 區域及美國政府和中國的數據中心皆有提供。</span><span class="sxs-lookup"><span data-stu-id="037ff-112">It is available in all public Azure regions as well as US Government and China data centers.</span></span> <span data-ttu-id="037ff-113">此預覽版本目前以免費方式提供。</span><span class="sxs-lookup"><span data-stu-id="037ff-113">This preview is currently free of charge.</span></span> 

## <a name="face-redaction-modes"></a><span data-ttu-id="037ff-114">臉部修訂模式</span><span class="sxs-lookup"><span data-stu-id="037ff-114">Face redaction modes</span></span>
<span data-ttu-id="037ff-115">臉部 redaction 運作方式是在每個畫面格的視訊中偵測到字體及追蹤 hello 朝物件，兩者向前及向後的時間，使 hello 相同的個人可以模糊從以及其他角度。</span><span class="sxs-lookup"><span data-stu-id="037ff-115">Facial redaction works by detecting faces in every frame of video and tracking hello face object both forwards and backwards in time, so that hello same individual can be blurred from other angles as well.</span></span> <span data-ttu-id="037ff-116">hello 自動化的 redaction 程序是很複雜的並不一定會產生 100%的所需的輸出，因此媒體分析提供讓您透過數種方式 toomodify hello 最終輸出。</span><span class="sxs-lookup"><span data-stu-id="037ff-116">hello automated redaction process is very complex and does not always produce 100% of desired output, for this reason Media Analytics provides you with a couple of ways toomodify hello final output.</span></span>

<span data-ttu-id="037ff-117">加法 tooa 完全自動模式中，在沒有兩段式工作流程可讓 hello 選取項目/還原-selection 的找到表面透過 Id 的清單。</span><span class="sxs-lookup"><span data-stu-id="037ff-117">In addition tooa fully automatic mode, there is a two-pass workflow which allows hello selection/de-selection of found faces via a list of IDs.</span></span> <span data-ttu-id="037ff-118">此外，toomake 任意每框架調整 hello 管理組件會使用 JSON 格式的中繼資料檔案。</span><span class="sxs-lookup"><span data-stu-id="037ff-118">Also, toomake arbitrary per frame adjustments hello MP uses a metadata file in JSON format.</span></span> <span data-ttu-id="037ff-119">此工作流程分割成**分析**和**修訂**模式。</span><span class="sxs-lookup"><span data-stu-id="037ff-119">This workflow is split into **Analyze** and **Redact** modes.</span></span> <span data-ttu-id="037ff-120">您可以結合在單一行程中一個作業，執行這兩項工作中的 hello 兩種模式這個模式稱為**組合**。</span><span class="sxs-lookup"><span data-stu-id="037ff-120">You can combine hello two modes in a single pass that runs both tasks in one job; this mode is called **Combined**.</span></span>

### <a name="combined-mode"></a><span data-ttu-id="037ff-121">結合模式</span><span class="sxs-lookup"><span data-stu-id="037ff-121">Combined mode</span></span>
<span data-ttu-id="037ff-122">這會自動產生修訂的 mp4，而不需要手動輸入。</span><span class="sxs-lookup"><span data-stu-id="037ff-122">This will produce a redacted mp4 automatically without any manual input.</span></span>

| <span data-ttu-id="037ff-123">階段</span><span class="sxs-lookup"><span data-stu-id="037ff-123">Stage</span></span> | <span data-ttu-id="037ff-124">檔案名稱</span><span class="sxs-lookup"><span data-stu-id="037ff-124">File Name</span></span> | <span data-ttu-id="037ff-125">注意事項</span><span class="sxs-lookup"><span data-stu-id="037ff-125">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="037ff-126">輸入資產</span><span class="sxs-lookup"><span data-stu-id="037ff-126">Input asset</span></span> |<span data-ttu-id="037ff-127">foo.bar</span><span class="sxs-lookup"><span data-stu-id="037ff-127">foo.bar</span></span> |<span data-ttu-id="037ff-128">WMV、MOV 或 MP4 格式的視訊</span><span class="sxs-lookup"><span data-stu-id="037ff-128">Video in WMV, MOV, or MP4 format</span></span> |
| <span data-ttu-id="037ff-129">輸入組態</span><span class="sxs-lookup"><span data-stu-id="037ff-129">Input config</span></span> |<span data-ttu-id="037ff-130">作業組態預設值</span><span class="sxs-lookup"><span data-stu-id="037ff-130">Job configuration preset</span></span> |<span data-ttu-id="037ff-131">{'version':'1.0', 'options': {'mode':'combined'}}</span><span class="sxs-lookup"><span data-stu-id="037ff-131">{'version':'1.0', 'options': {'mode':'combined'}}</span></span> |
| <span data-ttu-id="037ff-132">輸出資產</span><span class="sxs-lookup"><span data-stu-id="037ff-132">Output asset</span></span> |<span data-ttu-id="037ff-133">foo_redacted.mp4</span><span class="sxs-lookup"><span data-stu-id="037ff-133">foo_redacted.mp4</span></span> |<span data-ttu-id="037ff-134">已套用模糊處理的視訊</span><span class="sxs-lookup"><span data-stu-id="037ff-134">Video with blurring applied</span></span> |

#### <a name="input-example"></a><span data-ttu-id="037ff-135">輸入範例︰</span><span class="sxs-lookup"><span data-stu-id="037ff-135">Input example:</span></span>
[<span data-ttu-id="037ff-136">請觀看這個影片</span><span class="sxs-lookup"><span data-stu-id="037ff-136">view this video</span></span>](http://ampdemo.azureedge.net/?url=http%3A%2F%2Freferencestream-samplestream.streaming.mediaservices.windows.net%2Fed99001d-72ee-4f91-9fc0-cd530d0adbbc%2FDancing.mp4)

#### <a name="output-example"></a><span data-ttu-id="037ff-137">輸出範例：</span><span class="sxs-lookup"><span data-stu-id="037ff-137">Output example:</span></span>
[<span data-ttu-id="037ff-138">請觀看這個影片</span><span class="sxs-lookup"><span data-stu-id="037ff-138">view this video</span></span>](http://ampdemo.azureedge.net/?url=http%3A%2F%2Freferencestream-samplestream.streaming.mediaservices.windows.net%2Fc6608001-e5da-429b-9ec8-d69d8f3bfc79%2Fdance_redacted.mp4)

### <a name="analyze-mode"></a><span data-ttu-id="037ff-139">分析模式</span><span class="sxs-lookup"><span data-stu-id="037ff-139">Analyze mode</span></span>
<span data-ttu-id="037ff-140">hello**分析**hello 兩段式工作流程的階段接受視訊輸入，並且會產生正面的位置，請在 JSON 檔案和 jpg 影像，每個偵測到的字體。</span><span class="sxs-lookup"><span data-stu-id="037ff-140">hello **analyze** pass of hello two-pass workflow takes a video input and produces a JSON file of face locations, and jpg images of each detected face.</span></span>

| <span data-ttu-id="037ff-141">階段</span><span class="sxs-lookup"><span data-stu-id="037ff-141">Stage</span></span> | <span data-ttu-id="037ff-142">檔案名稱</span><span class="sxs-lookup"><span data-stu-id="037ff-142">File Name</span></span> | <span data-ttu-id="037ff-143">注意事項</span><span class="sxs-lookup"><span data-stu-id="037ff-143">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="037ff-144">輸入資產</span><span class="sxs-lookup"><span data-stu-id="037ff-144">Input asset</span></span> |<span data-ttu-id="037ff-145">foo.bar</span><span class="sxs-lookup"><span data-stu-id="037ff-145">foo.bar</span></span> |<span data-ttu-id="037ff-146">WMV、MPV 或 MP4 格式的視訊</span><span class="sxs-lookup"><span data-stu-id="037ff-146">Video in WMV, MPV, or MP4 format</span></span> |
| <span data-ttu-id="037ff-147">輸入組態</span><span class="sxs-lookup"><span data-stu-id="037ff-147">Input config</span></span> |<span data-ttu-id="037ff-148">作業組態預設值</span><span class="sxs-lookup"><span data-stu-id="037ff-148">Job configuration preset</span></span> |<span data-ttu-id="037ff-149">{'version':'1.0', 'options': {'mode':'analyze'}}</span><span class="sxs-lookup"><span data-stu-id="037ff-149">{'version':'1.0', 'options': {'mode':'analyze'}}</span></span> |
| <span data-ttu-id="037ff-150">輸出資產</span><span class="sxs-lookup"><span data-stu-id="037ff-150">Output asset</span></span> |<span data-ttu-id="037ff-151">foo_annotations.json</span><span class="sxs-lookup"><span data-stu-id="037ff-151">foo_annotations.json</span></span> |<span data-ttu-id="037ff-152">JSON 格式的臉部位置註解資料。</span><span class="sxs-lookup"><span data-stu-id="037ff-152">Annotation data of face locations in JSON format.</span></span> <span data-ttu-id="037ff-153">這可以編輯 hello 使用者 toomodify hello 模糊週框方塊。</span><span class="sxs-lookup"><span data-stu-id="037ff-153">This can be edited by hello user toomodify hello blurring bounding boxes.</span></span> <span data-ttu-id="037ff-154">請參閱以下範例。</span><span class="sxs-lookup"><span data-stu-id="037ff-154">See sample below.</span></span> |
| <span data-ttu-id="037ff-155">輸出資產</span><span class="sxs-lookup"><span data-stu-id="037ff-155">Output asset</span></span> |<span data-ttu-id="037ff-156">foo_thumb%06d.jpg [foo_thumb000001.jpg, foo_thumb000002.jpg]</span><span class="sxs-lookup"><span data-stu-id="037ff-156">foo_thumb%06d.jpg [foo_thumb000001.jpg, foo_thumb000002.jpg]</span></span> |<span data-ttu-id="037ff-157">每個裁剪的 jpg 偵測到的表面，其中 hello 數字表示 hello 面臨的 hello labelId</span><span class="sxs-lookup"><span data-stu-id="037ff-157">A cropped jpg of each detected face, where hello number indicates hello labelId of hello face</span></span> |

#### <a name="output-example"></a><span data-ttu-id="037ff-158">輸出範例：</span><span class="sxs-lookup"><span data-stu-id="037ff-158">Output example:</span></span>

    {
      "version": 1,
      "timescale": 24000,
      "offset": 0,
      "framerate": 23.976,
      "width": 1280,
      "height": 720,
      "fragments": [
        {
          "start": 0,
          "duration": 48048,
          "interval": 1001,
          "events": [
            [],
            [],
            [],
            [],
            [],
            [],
            [],
            [],
            [],
            [],
            [],
            [],
            [],
            [
              {
                "index": 13,
                "id": 1138,
                "x": 0.29537,
                "y": -0.18987,
                "width": 0.36239,
                "height": 0.80335
              },
              {
                "index": 13,
                "id": 2028,
                "x": 0.60427,
                "y": 0.16098,
                "width": 0.26958,
                "height": 0.57943
              }
            ],

    … truncated

### <a name="redact-mode"></a><span data-ttu-id="037ff-159">修訂模式</span><span class="sxs-lookup"><span data-stu-id="037ff-159">Redact mode</span></span>
<span data-ttu-id="037ff-160">hello hello 工作流程的第二個階段會較大的輸入必須結合成單一資產的數目。</span><span class="sxs-lookup"><span data-stu-id="037ff-160">hello second pass of hello workflow takes a larger number of inputs that must be combined into a single asset.</span></span>

<span data-ttu-id="037ff-161">這包括識別碼 tooblur、 hello 原始視訊，以及 hello 註解 JSON 的清單。</span><span class="sxs-lookup"><span data-stu-id="037ff-161">This includes a list of IDs tooblur, hello original video, and hello annotations JSON.</span></span> <span data-ttu-id="037ff-162">這個模式會使用 hello 註釋上 hello 輸入視訊模糊的 tooapply。</span><span class="sxs-lookup"><span data-stu-id="037ff-162">This mode uses hello annotations tooapply blurring on hello input video.</span></span>

<span data-ttu-id="037ff-163">hello hello 分析階段的輸出不包括 hello 原始視訊。</span><span class="sxs-lookup"><span data-stu-id="037ff-163">hello output from hello Analyze pass does not include hello original video.</span></span> <span data-ttu-id="037ff-164">hello 視訊需要 toobe 上傳到 hello hello Redact 模式工作的輸入資產，並選取為 hello 主要檔案。</span><span class="sxs-lookup"><span data-stu-id="037ff-164">hello video needs toobe uploaded into hello input asset for hello Redact mode task and selected as hello primary file.</span></span>

| <span data-ttu-id="037ff-165">階段</span><span class="sxs-lookup"><span data-stu-id="037ff-165">Stage</span></span> | <span data-ttu-id="037ff-166">檔案名稱</span><span class="sxs-lookup"><span data-stu-id="037ff-166">File Name</span></span> | <span data-ttu-id="037ff-167">注意事項</span><span class="sxs-lookup"><span data-stu-id="037ff-167">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="037ff-168">輸入資產</span><span class="sxs-lookup"><span data-stu-id="037ff-168">Input asset</span></span> |<span data-ttu-id="037ff-169">foo.bar</span><span class="sxs-lookup"><span data-stu-id="037ff-169">foo.bar</span></span> |<span data-ttu-id="037ff-170">WMV、MPV 或 MP4 格式的視訊。</span><span class="sxs-lookup"><span data-stu-id="037ff-170">Video in WMV, MPV, or MP4 format.</span></span> <span data-ttu-id="037ff-171">和步驟 1 相同的視訊。</span><span class="sxs-lookup"><span data-stu-id="037ff-171">Same video as in step 1.</span></span> |
| <span data-ttu-id="037ff-172">輸入資產</span><span class="sxs-lookup"><span data-stu-id="037ff-172">Input asset</span></span> |<span data-ttu-id="037ff-173">foo_annotations.json</span><span class="sxs-lookup"><span data-stu-id="037ff-173">foo_annotations.json</span></span> |<span data-ttu-id="037ff-174">來自第一個階段的註解中繼資料檔案，並帶有選擇性的修改。</span><span class="sxs-lookup"><span data-stu-id="037ff-174">annotations metadata file from phase one, with optional modifications.</span></span> |
| <span data-ttu-id="037ff-175">輸入資產</span><span class="sxs-lookup"><span data-stu-id="037ff-175">Input asset</span></span> |<span data-ttu-id="037ff-176">foo_IDList.txt (選擇性)</span><span class="sxs-lookup"><span data-stu-id="037ff-176">foo_IDList.txt (Optional)</span></span> |<span data-ttu-id="037ff-177">選擇性的新行分隔識別碼 tooredact 朝的清單。</span><span class="sxs-lookup"><span data-stu-id="037ff-177">Optional new line separated list of face IDs tooredact.</span></span> <span data-ttu-id="037ff-178">如果保持空白，則會模糊所有臉部。</span><span class="sxs-lookup"><span data-stu-id="037ff-178">If left blank, this blurs all faces.</span></span> |
| <span data-ttu-id="037ff-179">輸入組態</span><span class="sxs-lookup"><span data-stu-id="037ff-179">Input config</span></span> |<span data-ttu-id="037ff-180">作業組態預設值</span><span class="sxs-lookup"><span data-stu-id="037ff-180">Job configuration preset</span></span> |<span data-ttu-id="037ff-181">{'version':'1.0', 'options': {'mode':'redact'}}</span><span class="sxs-lookup"><span data-stu-id="037ff-181">{'version':'1.0', 'options': {'mode':'redact'}}</span></span> |
| <span data-ttu-id="037ff-182">輸出資產</span><span class="sxs-lookup"><span data-stu-id="037ff-182">Output asset</span></span> |<span data-ttu-id="037ff-183">foo_redacted.mp4</span><span class="sxs-lookup"><span data-stu-id="037ff-183">foo_redacted.mp4</span></span> |<span data-ttu-id="037ff-184">已根據註解套用模糊處理的視訊</span><span class="sxs-lookup"><span data-stu-id="037ff-184">Video with blurring applied based on annotations</span></span> |

#### <a name="example-output"></a><span data-ttu-id="037ff-185">範例輸出</span><span class="sxs-lookup"><span data-stu-id="037ff-185">Example output</span></span>
<span data-ttu-id="037ff-186">這是一個識別碼為選取 IDList hello 輸出。</span><span class="sxs-lookup"><span data-stu-id="037ff-186">This is hello output from an IDList with one ID selected.</span></span>

[<span data-ttu-id="037ff-187">請觀看這個影片</span><span class="sxs-lookup"><span data-stu-id="037ff-187">view this video</span></span>](http://ampdemo.azureedge.net/?url=http%3A%2F%2Freferencestream-samplestream.streaming.mediaservices.windows.net%2Fad6e24a2-4f9c-46ee-9fa7-bf05e20d19ac%2Fdance_redacted1.mp4)

<span data-ttu-id="037ff-188">Example foo_IDList.txt</span><span class="sxs-lookup"><span data-stu-id="037ff-188">Example foo_IDList.txt</span></span>
 
     1
     2
     3

## <a name="blur-types"></a><span data-ttu-id="037ff-189">模糊類型</span><span class="sxs-lookup"><span data-stu-id="037ff-189">Blur types</span></span>

<span data-ttu-id="037ff-190">在 hello**組合**或**Redact**模式中，有 5 不同模糊模式，您可以選擇透過 hello JSON 輸入組態：**低**， **Med**，**高**，**偵錯**，和**黑色**。</span><span class="sxs-lookup"><span data-stu-id="037ff-190">In hello **Combined** or **Redact** mode, there are 5 different blur modes you can choose from via hello JSON input configuration: **Low**, **Med**, **High**, **Debug**, and **Black**.</span></span> <span data-ttu-id="037ff-191">預設會使用 [中]。</span><span class="sxs-lookup"><span data-stu-id="037ff-191">By default **Med** is used.</span></span>

<span data-ttu-id="037ff-192">您可以尋找範例的 hello 模糊下列型別。</span><span class="sxs-lookup"><span data-stu-id="037ff-192">You can find samples of hello blur types below.</span></span>

### <a name="example-json"></a><span data-ttu-id="037ff-193">範例 JSON：</span><span class="sxs-lookup"><span data-stu-id="037ff-193">Example JSON:</span></span>

    {'version':'1.0', 'options': {'Mode': 'Combined', 'BlurType': 'High'}}

#### <a name="low"></a><span data-ttu-id="037ff-194">低</span><span class="sxs-lookup"><span data-stu-id="037ff-194">Low</span></span>

![低](./media/media-services-face-redaction/blur1.png)
 
#### <a name="med"></a><span data-ttu-id="037ff-196">中</span><span class="sxs-lookup"><span data-stu-id="037ff-196">Med</span></span>

![中](./media/media-services-face-redaction/blur2.png)

#### <a name="high"></a><span data-ttu-id="037ff-198">高</span><span class="sxs-lookup"><span data-stu-id="037ff-198">High</span></span>

![高](./media/media-services-face-redaction/blur3.png)

#### <a name="debug"></a><span data-ttu-id="037ff-200">偵錯</span><span class="sxs-lookup"><span data-stu-id="037ff-200">Debug</span></span>

![偵錯](./media/media-services-face-redaction/blur4.png)

#### <a name="black"></a><span data-ttu-id="037ff-202">黑色</span><span class="sxs-lookup"><span data-stu-id="037ff-202">Black</span></span>

![黑色](./media/media-services-face-redaction/blur5.png)

## <a name="elements-of-hello-output-json-file"></a><span data-ttu-id="037ff-204">Hello 輸出 JSON 檔案的項目</span><span class="sxs-lookup"><span data-stu-id="037ff-204">Elements of hello output JSON file</span></span>

<span data-ttu-id="037ff-205">hello Redaction 管理組件提供高精確度朝位置偵測和追蹤可以偵測出 too64 人力字體視訊畫面中。</span><span class="sxs-lookup"><span data-stu-id="037ff-205">hello Redaction MP provides high precision face location detection and tracking that can detect up too64 human faces in a video frame.</span></span> <span data-ttu-id="037ff-206">人臉正面提供 hello 獲得最佳結果，同時端字體和小型的字體 (小於或等於 too24x24 像素為單位) 一大挑戰。</span><span class="sxs-lookup"><span data-stu-id="037ff-206">Frontal faces provide hello best results, while side faces and small faces (less than or equal too24x24 pixels) are challenging.</span></span>

[!INCLUDE [media-services-analytics-output-json](../../includes/media-services-analytics-output-json.md)]

## <a name="net-sample-code"></a><span data-ttu-id="037ff-207">.NET 範例程式碼</span><span class="sxs-lookup"><span data-stu-id="037ff-207">.NET sample code</span></span>

<span data-ttu-id="037ff-208">hello 以下程式顯示如何：</span><span class="sxs-lookup"><span data-stu-id="037ff-208">hello following program shows how to:</span></span>

1. <span data-ttu-id="037ff-209">建立資產，並將媒體檔案上傳到 hello 資產。</span><span class="sxs-lookup"><span data-stu-id="037ff-209">Create an asset and upload a media file into hello asset.</span></span>
2. <span data-ttu-id="037ff-210">建立工作，以根據組態檔包含下列 json 的預設 hello 朝 redaction 工作。</span><span class="sxs-lookup"><span data-stu-id="037ff-210">Create a job with a face redaction task based on a configuration file that contains hello following json preset.</span></span> 
   
        {'version':'1.0', 'options': {'mode':'combined'}}
3. <span data-ttu-id="037ff-211">下載 hello 輸出 JSON 檔案。</span><span class="sxs-lookup"><span data-stu-id="037ff-211">Download hello output JSON files.</span></span> 

#### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="037ff-212">建立和設定 Visual Studio 專案</span><span class="sxs-lookup"><span data-stu-id="037ff-212">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="037ff-213">設定您的開發環境，並填入 hello 與連接資訊的 app.config 檔案中所述[與.NET 的 Media Services 開發](media-services-dotnet-how-to-use.md)。</span><span class="sxs-lookup"><span data-stu-id="037ff-213">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

#### <a name="example"></a><span data-ttu-id="037ff-214">範例</span><span class="sxs-lookup"><span data-stu-id="037ff-214">Example</span></span>

    using System;
    using System.Configuration;
    using System.IO;
    using System.Linq;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using System.Threading;
    using System.Threading.Tasks;

    namespace FaceRedaction
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

            // Run hello FaceRedaction job.
            var asset = RunFaceRedactionJob(@"C:\supportFiles\FaceRedaction\SomeFootage.mp4",
                        @"C:\supportFiles\FaceRedaction\config.json");

            // Download hello job output asset.
            DownloadAsset(asset, @"C:\supportFiles\FaceRedaction\Output");
        }

        static IAsset RunFaceRedactionJob(string inputMediaFilePath, string configurationFile)
        {
            // Create an asset and upload hello input media file toostorage.
            IAsset asset = CreateAssetAndUploadSingleFile(inputMediaFilePath,
            "My Face Redaction Input Asset",
            AssetCreationOptions.None);

            // Declare a new job.
            IJob job = _context.Jobs.Create("My Face Redaction Job");

            // Get a reference tooAzure Media Redactor.
            string MediaProcessorName = "Azure Media Redactor";

            var processor = GetLatestMediaProcessorByName(MediaProcessorName);

            // Read configuration from hello specified file.
            string configuration = File.ReadAllText(configurationFile);

            // Create a task with hello encoding details, using a string preset.
            ITask task = job.Tasks.AddNew("My Face Redaction Task",
            processor,
            configuration,
            TaskOptions.None);

            // Specify hello input asset.
            task.InputAssets.Add(asset);

            // Add an output asset toocontain hello results of hello job.
            task.OutputAssets.AddNew("My Face Redaction Output Asset", AssetCreationOptions.None);

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

## <a name="next-steps"></a><span data-ttu-id="037ff-215">後續步驟</span><span class="sxs-lookup"><span data-stu-id="037ff-215">Next steps</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="037ff-216">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="037ff-216">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a><span data-ttu-id="037ff-217">相關連結</span><span class="sxs-lookup"><span data-stu-id="037ff-217">Related links</span></span>
[<span data-ttu-id="037ff-218">Azure 媒體服務分析概觀</span><span class="sxs-lookup"><span data-stu-id="037ff-218">Azure Media Services Analytics Overview</span></span>](media-services-analytics-overview.md)

[<span data-ttu-id="037ff-219">Azure 媒體分析示範</span><span class="sxs-lookup"><span data-stu-id="037ff-219">Azure Media Analytics demos</span></span>](http://azuremedialabs.azurewebsites.net/demos/Analytics.html)

