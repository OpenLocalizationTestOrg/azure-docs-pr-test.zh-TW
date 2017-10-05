---
title: "使用 Azure 媒體分析修訂臉部 | Microsoft Docs"
description: "本主題示範如何使用 Azure 媒體分析修訂臉部。"
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
ms.openlocfilehash: 747f3ae1a7484515083c590942de3da22568cd39
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="redact-faces-with-azure-media-analytics"></a><span data-ttu-id="6a4e7-103">使用 Azure 媒體分析修訂臉部</span><span class="sxs-lookup"><span data-stu-id="6a4e7-103">Redact faces with Azure Media Analytics</span></span>
## <a name="overview"></a><span data-ttu-id="6a4e7-104">概觀</span><span class="sxs-lookup"><span data-stu-id="6a4e7-104">Overview</span></span>
<span data-ttu-id="6a4e7-105">**Azure 媒體修訂器** 是 [Azure 媒體分析](media-services-analytics-overview.md) 媒體處理器 (MP)，可在雲端提供可調整的臉部修訂。</span><span class="sxs-lookup"><span data-stu-id="6a4e7-105">**Azure Media Redactor** is an [Azure Media Analytics](media-services-analytics-overview.md) media processor (MP) that offers scalable face redaction in the cloud.</span></span> <span data-ttu-id="6a4e7-106">臉部修訂可讓您修改視訊，以模糊所選人物的臉部。</span><span class="sxs-lookup"><span data-stu-id="6a4e7-106">Face redaction enables you to modify your video in order to blur faces of selected individuals.</span></span> <span data-ttu-id="6a4e7-107">在公共安全和新聞媒體案例中，您可能會想要使用臉部修訂服務。</span><span class="sxs-lookup"><span data-stu-id="6a4e7-107">You may want to use the face redaction service in public safety and news media scenarios.</span></span> <span data-ttu-id="6a4e7-108">若要手動修訂包含多個臉部的幾分鐘影片，可能要花上數小時的時間，若使用此服務，則只需要幾個簡單的步驟就能完成臉部修訂程序。</span><span class="sxs-lookup"><span data-stu-id="6a4e7-108">A few minutes of footage that contains multiple faces can take hours to redact manually, but with this service the face redaction process will require just a few simple steps.</span></span> <span data-ttu-id="6a4e7-109">如需詳細資訊，請參閱[此](https://azure.microsoft.com/blog/azure-media-redactor/)部落格。</span><span class="sxs-lookup"><span data-stu-id="6a4e7-109">For  more information, see [this](https://azure.microsoft.com/blog/azure-media-redactor/) blog.</span></span>

<span data-ttu-id="6a4e7-110">本主題提供有關 **Azure 媒體修訂** 的詳細資料，並示範如何搭配適用於 .NET 的媒體服務 SDK 來使用它。</span><span class="sxs-lookup"><span data-stu-id="6a4e7-110">This topic gives details about **Azure Media Redactor** and shows how to use it with Media Services SDK for .NET.</span></span>

<span data-ttu-id="6a4e7-111">**Azure 媒體修訂器** MP 目前為預覽功能。</span><span class="sxs-lookup"><span data-stu-id="6a4e7-111">The **Azure Media Redactor** MP is currently in Preview.</span></span> <span data-ttu-id="6a4e7-112">在所有公開的 Azure 區域及美國政府和中國的數據中心皆有提供。</span><span class="sxs-lookup"><span data-stu-id="6a4e7-112">It is available in all public Azure regions as well as US Government and China data centers.</span></span> <span data-ttu-id="6a4e7-113">此預覽版本目前以免費方式提供。</span><span class="sxs-lookup"><span data-stu-id="6a4e7-113">This preview is currently free of charge.</span></span> 

## <a name="face-redaction-modes"></a><span data-ttu-id="6a4e7-114">臉部修訂模式</span><span class="sxs-lookup"><span data-stu-id="6a4e7-114">Face redaction modes</span></span>
<span data-ttu-id="6a4e7-115">臉部修訂的運作方式是，偵測視訊中每個畫面內出現的臉部，並及時向前及向後追蹤臉部物體，讓同一個人在其他角度也可以變得模糊。</span><span class="sxs-lookup"><span data-stu-id="6a4e7-115">Facial redaction works by detecting faces in every frame of video and tracking the face object both forwards and backwards in time, so that the same individual can be blurred from other angles as well.</span></span> <span data-ttu-id="6a4e7-116">自動化修訂程序非常複雜，而且不一定會 100% 產生所需的輸出，因此，媒體分析提供您幾種方式來修改最終輸出。</span><span class="sxs-lookup"><span data-stu-id="6a4e7-116">The automated redaction process is very complex and does not always produce 100% of desired output, for this reason Media Analytics provides you with a couple of ways to modify the final output.</span></span>

<span data-ttu-id="6a4e7-117">除了完全自動模式，還有一種兩段式的工作流程可讓您透過識別碼清單選取/取消選取找到的臉部。</span><span class="sxs-lookup"><span data-stu-id="6a4e7-117">In addition to a fully automatic mode, there is a two-pass workflow which allows the selection/de-selection of found faces via a list of IDs.</span></span> <span data-ttu-id="6a4e7-118">此外，為了進行任意的每一畫面調整，MP 使用 JSON 格式的中繼資料檔案。</span><span class="sxs-lookup"><span data-stu-id="6a4e7-118">Also, to make arbitrary per frame adjustments the MP uses a metadata file in JSON format.</span></span> <span data-ttu-id="6a4e7-119">此工作流程分割成**分析**和**修訂**模式。</span><span class="sxs-lookup"><span data-stu-id="6a4e7-119">This workflow is split into **Analyze** and **Redact** modes.</span></span> <span data-ttu-id="6a4e7-120">您可以將這兩種模式結合成單一階段，以在一個作業中執行這兩項工作，我們將這個模式稱為 **結合**。</span><span class="sxs-lookup"><span data-stu-id="6a4e7-120">You can combine the two modes in a single pass that runs both tasks in one job; this mode is called **Combined**.</span></span>

### <a name="combined-mode"></a><span data-ttu-id="6a4e7-121">結合模式</span><span class="sxs-lookup"><span data-stu-id="6a4e7-121">Combined mode</span></span>
<span data-ttu-id="6a4e7-122">這會自動產生修訂的 mp4，而不需要手動輸入。</span><span class="sxs-lookup"><span data-stu-id="6a4e7-122">This will produce a redacted mp4 automatically without any manual input.</span></span>

| <span data-ttu-id="6a4e7-123">階段</span><span class="sxs-lookup"><span data-stu-id="6a4e7-123">Stage</span></span> | <span data-ttu-id="6a4e7-124">檔案名稱</span><span class="sxs-lookup"><span data-stu-id="6a4e7-124">File Name</span></span> | <span data-ttu-id="6a4e7-125">注意事項</span><span class="sxs-lookup"><span data-stu-id="6a4e7-125">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6a4e7-126">輸入資產</span><span class="sxs-lookup"><span data-stu-id="6a4e7-126">Input asset</span></span> |<span data-ttu-id="6a4e7-127">foo.bar</span><span class="sxs-lookup"><span data-stu-id="6a4e7-127">foo.bar</span></span> |<span data-ttu-id="6a4e7-128">WMV、MOV 或 MP4 格式的視訊</span><span class="sxs-lookup"><span data-stu-id="6a4e7-128">Video in WMV, MOV, or MP4 format</span></span> |
| <span data-ttu-id="6a4e7-129">輸入組態</span><span class="sxs-lookup"><span data-stu-id="6a4e7-129">Input config</span></span> |<span data-ttu-id="6a4e7-130">作業組態預設值</span><span class="sxs-lookup"><span data-stu-id="6a4e7-130">Job configuration preset</span></span> |<span data-ttu-id="6a4e7-131">{'version':'1.0', 'options': {'mode':'combined'}}</span><span class="sxs-lookup"><span data-stu-id="6a4e7-131">{'version':'1.0', 'options': {'mode':'combined'}}</span></span> |
| <span data-ttu-id="6a4e7-132">輸出資產</span><span class="sxs-lookup"><span data-stu-id="6a4e7-132">Output asset</span></span> |<span data-ttu-id="6a4e7-133">foo_redacted.mp4</span><span class="sxs-lookup"><span data-stu-id="6a4e7-133">foo_redacted.mp4</span></span> |<span data-ttu-id="6a4e7-134">已套用模糊處理的視訊</span><span class="sxs-lookup"><span data-stu-id="6a4e7-134">Video with blurring applied</span></span> |

#### <a name="input-example"></a><span data-ttu-id="6a4e7-135">輸入範例︰</span><span class="sxs-lookup"><span data-stu-id="6a4e7-135">Input example:</span></span>
[<span data-ttu-id="6a4e7-136">請觀看這個影片</span><span class="sxs-lookup"><span data-stu-id="6a4e7-136">view this video</span></span>](http://ampdemo.azureedge.net/?url=http%3A%2F%2Freferencestream-samplestream.streaming.mediaservices.windows.net%2Fed99001d-72ee-4f91-9fc0-cd530d0adbbc%2FDancing.mp4)

#### <a name="output-example"></a><span data-ttu-id="6a4e7-137">輸出範例：</span><span class="sxs-lookup"><span data-stu-id="6a4e7-137">Output example:</span></span>
[<span data-ttu-id="6a4e7-138">請觀看這個影片</span><span class="sxs-lookup"><span data-stu-id="6a4e7-138">view this video</span></span>](http://ampdemo.azureedge.net/?url=http%3A%2F%2Freferencestream-samplestream.streaming.mediaservices.windows.net%2Fc6608001-e5da-429b-9ec8-d69d8f3bfc79%2Fdance_redacted.mp4)

### <a name="analyze-mode"></a><span data-ttu-id="6a4e7-139">分析模式</span><span class="sxs-lookup"><span data-stu-id="6a4e7-139">Analyze mode</span></span>
<span data-ttu-id="6a4e7-140">兩段式工作流程的 **分析** 階段會接受視訊輸入，並產生臉部位置的 JSON 檔案和每個偵測到之臉部的 jpg 影像。</span><span class="sxs-lookup"><span data-stu-id="6a4e7-140">The **analyze** pass of the two-pass workflow takes a video input and produces a JSON file of face locations, and jpg images of each detected face.</span></span>

| <span data-ttu-id="6a4e7-141">階段</span><span class="sxs-lookup"><span data-stu-id="6a4e7-141">Stage</span></span> | <span data-ttu-id="6a4e7-142">檔案名稱</span><span class="sxs-lookup"><span data-stu-id="6a4e7-142">File Name</span></span> | <span data-ttu-id="6a4e7-143">注意事項</span><span class="sxs-lookup"><span data-stu-id="6a4e7-143">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6a4e7-144">輸入資產</span><span class="sxs-lookup"><span data-stu-id="6a4e7-144">Input asset</span></span> |<span data-ttu-id="6a4e7-145">foo.bar</span><span class="sxs-lookup"><span data-stu-id="6a4e7-145">foo.bar</span></span> |<span data-ttu-id="6a4e7-146">WMV、MPV 或 MP4 格式的視訊</span><span class="sxs-lookup"><span data-stu-id="6a4e7-146">Video in WMV, MPV, or MP4 format</span></span> |
| <span data-ttu-id="6a4e7-147">輸入組態</span><span class="sxs-lookup"><span data-stu-id="6a4e7-147">Input config</span></span> |<span data-ttu-id="6a4e7-148">作業組態預設值</span><span class="sxs-lookup"><span data-stu-id="6a4e7-148">Job configuration preset</span></span> |<span data-ttu-id="6a4e7-149">{'version':'1.0', 'options': {'mode':'analyze'}}</span><span class="sxs-lookup"><span data-stu-id="6a4e7-149">{'version':'1.0', 'options': {'mode':'analyze'}}</span></span> |
| <span data-ttu-id="6a4e7-150">輸出資產</span><span class="sxs-lookup"><span data-stu-id="6a4e7-150">Output asset</span></span> |<span data-ttu-id="6a4e7-151">foo_annotations.json</span><span class="sxs-lookup"><span data-stu-id="6a4e7-151">foo_annotations.json</span></span> |<span data-ttu-id="6a4e7-152">JSON 格式的臉部位置註解資料。</span><span class="sxs-lookup"><span data-stu-id="6a4e7-152">Annotation data of face locations in JSON format.</span></span> <span data-ttu-id="6a4e7-153">使用者可編輯此資料以修改模糊處理的邊框。</span><span class="sxs-lookup"><span data-stu-id="6a4e7-153">This can be edited by the user to modify the blurring bounding boxes.</span></span> <span data-ttu-id="6a4e7-154">請參閱以下範例。</span><span class="sxs-lookup"><span data-stu-id="6a4e7-154">See sample below.</span></span> |
| <span data-ttu-id="6a4e7-155">輸出資產</span><span class="sxs-lookup"><span data-stu-id="6a4e7-155">Output asset</span></span> |<span data-ttu-id="6a4e7-156">foo_thumb%06d.jpg [foo_thumb000001.jpg, foo_thumb000002.jpg]</span><span class="sxs-lookup"><span data-stu-id="6a4e7-156">foo_thumb%06d.jpg [foo_thumb000001.jpg, foo_thumb000002.jpg]</span></span> |<span data-ttu-id="6a4e7-157">所偵測到之每個臉部的已裁剪 jpg，數字表示臉部的 labelId</span><span class="sxs-lookup"><span data-stu-id="6a4e7-157">A cropped jpg of each detected face, where the number indicates the labelId of the face</span></span> |

#### <a name="output-example"></a><span data-ttu-id="6a4e7-158">輸出範例：</span><span class="sxs-lookup"><span data-stu-id="6a4e7-158">Output example:</span></span>

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

### <a name="redact-mode"></a><span data-ttu-id="6a4e7-159">修訂模式</span><span class="sxs-lookup"><span data-stu-id="6a4e7-159">Redact mode</span></span>
<span data-ttu-id="6a4e7-160">工作流程的第二個階段會接受必須結合成單一資產的較大量輸入。</span><span class="sxs-lookup"><span data-stu-id="6a4e7-160">The second pass of the workflow takes a larger number of inputs that must be combined into a single asset.</span></span>

<span data-ttu-id="6a4e7-161">這包括要模糊處理的識別碼清單、原始視訊和註解 JSON。</span><span class="sxs-lookup"><span data-stu-id="6a4e7-161">This includes a list of IDs to blur, the original video, and the annotations JSON.</span></span> <span data-ttu-id="6a4e7-162">這個模式會使用註解在輸入視訊上套用模糊處理。</span><span class="sxs-lookup"><span data-stu-id="6a4e7-162">This mode uses the annotations to apply blurring on the input video.</span></span>

<span data-ttu-id="6a4e7-163">分析階段的輸出不包含原始視訊。</span><span class="sxs-lookup"><span data-stu-id="6a4e7-163">The output from the Analyze pass does not include the original video.</span></span> <span data-ttu-id="6a4e7-164">視訊必須上傳到修訂模式工作的輸入資產並選取做為主要檔案。</span><span class="sxs-lookup"><span data-stu-id="6a4e7-164">The video needs to be uploaded into the input asset for the Redact mode task and selected as the primary file.</span></span>

| <span data-ttu-id="6a4e7-165">階段</span><span class="sxs-lookup"><span data-stu-id="6a4e7-165">Stage</span></span> | <span data-ttu-id="6a4e7-166">檔案名稱</span><span class="sxs-lookup"><span data-stu-id="6a4e7-166">File Name</span></span> | <span data-ttu-id="6a4e7-167">注意事項</span><span class="sxs-lookup"><span data-stu-id="6a4e7-167">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6a4e7-168">輸入資產</span><span class="sxs-lookup"><span data-stu-id="6a4e7-168">Input asset</span></span> |<span data-ttu-id="6a4e7-169">foo.bar</span><span class="sxs-lookup"><span data-stu-id="6a4e7-169">foo.bar</span></span> |<span data-ttu-id="6a4e7-170">WMV、MPV 或 MP4 格式的視訊。</span><span class="sxs-lookup"><span data-stu-id="6a4e7-170">Video in WMV, MPV, or MP4 format.</span></span> <span data-ttu-id="6a4e7-171">和步驟 1 相同的視訊。</span><span class="sxs-lookup"><span data-stu-id="6a4e7-171">Same video as in step 1.</span></span> |
| <span data-ttu-id="6a4e7-172">輸入資產</span><span class="sxs-lookup"><span data-stu-id="6a4e7-172">Input asset</span></span> |<span data-ttu-id="6a4e7-173">foo_annotations.json</span><span class="sxs-lookup"><span data-stu-id="6a4e7-173">foo_annotations.json</span></span> |<span data-ttu-id="6a4e7-174">來自第一個階段的註解中繼資料檔案，並帶有選擇性的修改。</span><span class="sxs-lookup"><span data-stu-id="6a4e7-174">annotations metadata file from phase one, with optional modifications.</span></span> |
| <span data-ttu-id="6a4e7-175">輸入資產</span><span class="sxs-lookup"><span data-stu-id="6a4e7-175">Input asset</span></span> |<span data-ttu-id="6a4e7-176">foo_IDList.txt (選擇性)</span><span class="sxs-lookup"><span data-stu-id="6a4e7-176">foo_IDList.txt (Optional)</span></span> |<span data-ttu-id="6a4e7-177">要修訂之臉部 ID 的選擇性換行分隔清單。</span><span class="sxs-lookup"><span data-stu-id="6a4e7-177">Optional new line separated list of face IDs to redact.</span></span> <span data-ttu-id="6a4e7-178">如果保持空白，則會模糊所有臉部。</span><span class="sxs-lookup"><span data-stu-id="6a4e7-178">If left blank, this blurs all faces.</span></span> |
| <span data-ttu-id="6a4e7-179">輸入組態</span><span class="sxs-lookup"><span data-stu-id="6a4e7-179">Input config</span></span> |<span data-ttu-id="6a4e7-180">作業組態預設值</span><span class="sxs-lookup"><span data-stu-id="6a4e7-180">Job configuration preset</span></span> |<span data-ttu-id="6a4e7-181">{'version':'1.0', 'options': {'mode':'redact'}}</span><span class="sxs-lookup"><span data-stu-id="6a4e7-181">{'version':'1.0', 'options': {'mode':'redact'}}</span></span> |
| <span data-ttu-id="6a4e7-182">輸出資產</span><span class="sxs-lookup"><span data-stu-id="6a4e7-182">Output asset</span></span> |<span data-ttu-id="6a4e7-183">foo_redacted.mp4</span><span class="sxs-lookup"><span data-stu-id="6a4e7-183">foo_redacted.mp4</span></span> |<span data-ttu-id="6a4e7-184">已根據註解套用模糊處理的視訊</span><span class="sxs-lookup"><span data-stu-id="6a4e7-184">Video with blurring applied based on annotations</span></span> |

#### <a name="example-output"></a><span data-ttu-id="6a4e7-185">範例輸出</span><span class="sxs-lookup"><span data-stu-id="6a4e7-185">Example output</span></span>
<span data-ttu-id="6a4e7-186">這是選取了一個識別碼的 IDList 輸出。</span><span class="sxs-lookup"><span data-stu-id="6a4e7-186">This is the output from an IDList with one ID selected.</span></span>

[<span data-ttu-id="6a4e7-187">請觀看這個影片</span><span class="sxs-lookup"><span data-stu-id="6a4e7-187">view this video</span></span>](http://ampdemo.azureedge.net/?url=http%3A%2F%2Freferencestream-samplestream.streaming.mediaservices.windows.net%2Fad6e24a2-4f9c-46ee-9fa7-bf05e20d19ac%2Fdance_redacted1.mp4)

<span data-ttu-id="6a4e7-188">Example foo_IDList.txt</span><span class="sxs-lookup"><span data-stu-id="6a4e7-188">Example foo_IDList.txt</span></span>
 
     1
     2
     3

## <a name="blur-types"></a><span data-ttu-id="6a4e7-189">模糊類型</span><span class="sxs-lookup"><span data-stu-id="6a4e7-189">Blur types</span></span>

<span data-ttu-id="6a4e7-190">在 [結合] 或 [修訂] 模式中，您可以透過 JSON 輸入設定從 5 種不同的模糊模式中進行選擇：[低]、[中]、[高]、[偵錯] 和 [黑色]。</span><span class="sxs-lookup"><span data-stu-id="6a4e7-190">In the **Combined** or **Redact** mode, there are 5 different blur modes you can choose from via the JSON input configuration: **Low**, **Med**, **High**, **Debug**, and **Black**.</span></span> <span data-ttu-id="6a4e7-191">預設會使用 [中]。</span><span class="sxs-lookup"><span data-stu-id="6a4e7-191">By default **Med** is used.</span></span>

<span data-ttu-id="6a4e7-192">您可以在下面找到模糊類型的範例。</span><span class="sxs-lookup"><span data-stu-id="6a4e7-192">You can find samples of the blur types below.</span></span>

### <a name="example-json"></a><span data-ttu-id="6a4e7-193">範例 JSON：</span><span class="sxs-lookup"><span data-stu-id="6a4e7-193">Example JSON:</span></span>

    {'version':'1.0', 'options': {'Mode': 'Combined', 'BlurType': 'High'}}

#### <a name="low"></a><span data-ttu-id="6a4e7-194">低</span><span class="sxs-lookup"><span data-stu-id="6a4e7-194">Low</span></span>

![低](./media/media-services-face-redaction/blur1.png)
 
#### <a name="med"></a><span data-ttu-id="6a4e7-196">中</span><span class="sxs-lookup"><span data-stu-id="6a4e7-196">Med</span></span>

![中](./media/media-services-face-redaction/blur2.png)

#### <a name="high"></a><span data-ttu-id="6a4e7-198">高</span><span class="sxs-lookup"><span data-stu-id="6a4e7-198">High</span></span>

![高](./media/media-services-face-redaction/blur3.png)

#### <a name="debug"></a><span data-ttu-id="6a4e7-200">偵錯</span><span class="sxs-lookup"><span data-stu-id="6a4e7-200">Debug</span></span>

![偵錯](./media/media-services-face-redaction/blur4.png)

#### <a name="black"></a><span data-ttu-id="6a4e7-202">黑色</span><span class="sxs-lookup"><span data-stu-id="6a4e7-202">Black</span></span>

![黑色](./media/media-services-face-redaction/blur5.png)

## <a name="elements-of-the-output-json-file"></a><span data-ttu-id="6a4e7-204">輸出 JSON 檔案的元素</span><span class="sxs-lookup"><span data-stu-id="6a4e7-204">Elements of the output JSON file</span></span>

<span data-ttu-id="6a4e7-205">修訂 MP 能提供高精確度的臉部位置偵測和追蹤功能，可在單一視訊畫面中偵測到最多 64 個人類臉部。</span><span class="sxs-lookup"><span data-stu-id="6a4e7-205">The Redaction MP provides high precision face location detection and tracking that can detect up to 64 human faces in a video frame.</span></span> <span data-ttu-id="6a4e7-206">正面的臉部能提供最佳結果，而側面的臉部和較小的臉部 (小於或等於 24x24 像素) 則頗具挑戰性。</span><span class="sxs-lookup"><span data-stu-id="6a4e7-206">Frontal faces provide the best results, while side faces and small faces (less than or equal to 24x24 pixels) are challenging.</span></span>

[!INCLUDE [media-services-analytics-output-json](../../includes/media-services-analytics-output-json.md)]

## <a name="net-sample-code"></a><span data-ttu-id="6a4e7-207">.NET 範例程式碼</span><span class="sxs-lookup"><span data-stu-id="6a4e7-207">.NET sample code</span></span>

<span data-ttu-id="6a4e7-208">下列程式將示範如何：</span><span class="sxs-lookup"><span data-stu-id="6a4e7-208">The following program shows how to:</span></span>

1. <span data-ttu-id="6a4e7-209">建立資產並將媒體檔案上傳到資產。</span><span class="sxs-lookup"><span data-stu-id="6a4e7-209">Create an asset and upload a media file into the asset.</span></span>
2. <span data-ttu-id="6a4e7-210">根據包含下列 JSON 預設值的組態檔案，建立具有臉部修訂工作的作業。</span><span class="sxs-lookup"><span data-stu-id="6a4e7-210">Create a job with a face redaction task based on a configuration file that contains the following json preset.</span></span> 
   
        {'version':'1.0', 'options': {'mode':'combined'}}
3. <span data-ttu-id="6a4e7-211">下載輸出 JSON 檔案。</span><span class="sxs-lookup"><span data-stu-id="6a4e7-211">Download the output JSON files.</span></span> 

#### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="6a4e7-212">建立和設定 Visual Studio 專案</span><span class="sxs-lookup"><span data-stu-id="6a4e7-212">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="6a4e7-213">設定您的開發環境並在 app.config 檔案中填入連線資訊，如[使用 .NET 進行 Media Services 開發](media-services-dotnet-how-to-use.md)中所述。</span><span class="sxs-lookup"><span data-stu-id="6a4e7-213">Set up your development environment and populate the app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

#### <a name="example"></a><span data-ttu-id="6a4e7-214">範例</span><span class="sxs-lookup"><span data-stu-id="6a4e7-214">Example</span></span>

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

            // Run the FaceRedaction job.
            var asset = RunFaceRedactionJob(@"C:\supportFiles\FaceRedaction\SomeFootage.mp4",
                        @"C:\supportFiles\FaceRedaction\config.json");

            // Download the job output asset.
            DownloadAsset(asset, @"C:\supportFiles\FaceRedaction\Output");
        }

        static IAsset RunFaceRedactionJob(string inputMediaFilePath, string configurationFile)
        {
            // Create an asset and upload the input media file to storage.
            IAsset asset = CreateAssetAndUploadSingleFile(inputMediaFilePath,
            "My Face Redaction Input Asset",
            AssetCreationOptions.None);

            // Declare a new job.
            IJob job = _context.Jobs.Create("My Face Redaction Job");

            // Get a reference to Azure Media Redactor.
            string MediaProcessorName = "Azure Media Redactor";

            var processor = GetLatestMediaProcessorByName(MediaProcessorName);

            // Read configuration from the specified file.
            string configuration = File.ReadAllText(configurationFile);

            // Create a task with the encoding details, using a string preset.
            ITask task = job.Tasks.AddNew("My Face Redaction Task",
            processor,
            configuration,
            TaskOptions.None);

            // Specify the input asset.
            task.InputAssets.Add(asset);

            // Add an output asset to contain the results of the job.
            task.OutputAssets.AddNew("My Face Redaction Output Asset", AssetCreationOptions.None);

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

## <a name="next-steps"></a><span data-ttu-id="6a4e7-215">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6a4e7-215">Next steps</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="6a4e7-216">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="6a4e7-216">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a><span data-ttu-id="6a4e7-217">相關連結</span><span class="sxs-lookup"><span data-stu-id="6a4e7-217">Related links</span></span>
[<span data-ttu-id="6a4e7-218">Azure 媒體服務分析概觀</span><span class="sxs-lookup"><span data-stu-id="6a4e7-218">Azure Media Services Analytics Overview</span></span>](media-services-analytics-overview.md)

[<span data-ttu-id="6a4e7-219">Azure 媒體分析示範</span><span class="sxs-lookup"><span data-stu-id="6a4e7-219">Azure Media Analytics demos</span></span>](http://azuremedialabs.azurewebsites.net/demos/Analytics.html)

