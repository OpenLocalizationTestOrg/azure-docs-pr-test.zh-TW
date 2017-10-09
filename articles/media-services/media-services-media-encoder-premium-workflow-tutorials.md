---
title: "aaaAvanced 媒體編碼器高階工作流程的教學課程"
description: "本文件包含說明如何 tooperform 進階使用媒體編碼器高階工作流程工作的逐步解說也以及 toocreate 複雜工作流程與工作流程設計工具。"
services: media-services
documentationcenter: 
author: xstof
manager: cfowler
editor: 
ms.assetid: 1ba52865-b4a8-4ca0-ac96-920d55b9d15b
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: christoc;xpouyat;juliako
ms.openlocfilehash: 641bd1be3bd795b5e138fa7ffdf299ff6710904e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-media-encoder-premium-workflow-tutorials"></a><span data-ttu-id="c6748-103">進階媒體編碼器 Premium 工作流程教學課程</span><span class="sxs-lookup"><span data-stu-id="c6748-103">Advanced Media Encoder Premium Workflow tutorials</span></span>
## <a name="overview"></a><span data-ttu-id="c6748-104">概觀</span><span class="sxs-lookup"><span data-stu-id="c6748-104">Overview</span></span>
<span data-ttu-id="c6748-105">本文件說明的逐步解說如何 toocustomize 的工作流程**工作流程設計工具**。</span><span class="sxs-lookup"><span data-stu-id="c6748-105">This document contains walkthroughs that show how toocustomize workflows with  **Workflow Designer**.</span></span> <span data-ttu-id="c6748-106">您可以尋找 hello 實際工作流程檔案[這裡](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows/PremiumEncoderWorkflowSamples)。</span><span class="sxs-lookup"><span data-stu-id="c6748-106">You can find hello actual workflow files [here](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows/PremiumEncoderWorkflowSamples).</span></span>  

## <a name="toc"></a><span data-ttu-id="c6748-107">目錄</span><span class="sxs-lookup"><span data-stu-id="c6748-107">TOC</span></span>
<span data-ttu-id="c6748-108">涵蓋下列主題中的 hello:</span><span class="sxs-lookup"><span data-stu-id="c6748-108">hello following topics are covered:</span></span>

* [<span data-ttu-id="c6748-109">將 MXF 編碼為單一位元速率 MP4</span><span class="sxs-lookup"><span data-stu-id="c6748-109">Encoding MXF into a single bitrate MP4</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4)
  * [<span data-ttu-id="c6748-110">開始新的工作流程</span><span class="sxs-lookup"><span data-stu-id="c6748-110">Starting a new workflow</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_start_new)
  * [<span data-ttu-id="c6748-111">使用媒體檔案輸入 hello</span><span class="sxs-lookup"><span data-stu-id="c6748-111">Using hello Media File Input</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_file_input)
  * [<span data-ttu-id="c6748-112">檢查媒體串流</span><span class="sxs-lookup"><span data-stu-id="c6748-112">Inspecting media streams</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_streams)
  * [<span data-ttu-id="c6748-113">為產生的 MP4 檔案加入視訊編碼器</span><span class="sxs-lookup"><span data-stu-id="c6748-113">Adding a video encoder for .MP4 file generation</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_file_generation)
  * [<span data-ttu-id="c6748-114">編碼的 hello 音訊資料流</span><span class="sxs-lookup"><span data-stu-id="c6748-114">Encoding hello audio stream</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_audio)
  * [<span data-ttu-id="c6748-115">將音訊和視訊串流多工處理為 MP4 容器</span><span class="sxs-lookup"><span data-stu-id="c6748-115">Multiplexing Audio and Video streams into an MP4 container</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_audio_and_fideo)
  * [<span data-ttu-id="c6748-116">寫入 hello MP4 檔案</span><span class="sxs-lookup"><span data-stu-id="c6748-116">Writing hello MP4 file</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_writing_mp4)
  * [<span data-ttu-id="c6748-117">從 hello 輸出檔案建立 Media Services 資產</span><span class="sxs-lookup"><span data-stu-id="c6748-117">Creating a Media Services Asset from hello output file</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_asset_from_output)
  * [<span data-ttu-id="c6748-118">測試 hello 完成在本機工作流程</span><span class="sxs-lookup"><span data-stu-id="c6748-118">Test hello finished workflow locally</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_test)
* [<span data-ttu-id="c6748-119">將 MXF 編碼為多位元速率 MP4 - 動態封裝已啟用</span><span class="sxs-lookup"><span data-stu-id="c6748-119">Encoding MXF into multibitrate MP4s - dynamic packaging enabled</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging)
  * [<span data-ttu-id="c6748-120">加入一或多個其他的 MP4 輸出</span><span class="sxs-lookup"><span data-stu-id="c6748-120">Adding one or more additional MP4 outputs</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging_more_outputs)
  * [<span data-ttu-id="c6748-121">設定 hello 檔案輸出名稱</span><span class="sxs-lookup"><span data-stu-id="c6748-121">Configuring hello file output names</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging_conf_output_names)
  * [<span data-ttu-id="c6748-122">加入個別的曲目</span><span class="sxs-lookup"><span data-stu-id="c6748-122">Adding a separate Audio Track</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging_audio_tracks)
  * [<span data-ttu-id="c6748-123">加入 hello。ISM SMIL 檔案</span><span class="sxs-lookup"><span data-stu-id="c6748-123">Adding hello .ISM SMIL File</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging_ism_file)
* [<span data-ttu-id="c6748-124">將 MXF 編碼為多位元速率 MP4 - 增強的藍圖</span><span class="sxs-lookup"><span data-stu-id="c6748-124">Encoding MXF into multibitrate MP4 - enhanced blueprint</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to__multibitrate_MP4)
  * [<span data-ttu-id="c6748-125">工作流程概觀 tooenhance</span><span class="sxs-lookup"><span data-stu-id="c6748-125">Workflow overview tooenhance</span></span>](#workflow-overview-to-enhance)
  * [<span data-ttu-id="c6748-126">檔案命名慣例</span><span class="sxs-lookup"><span data-stu-id="c6748-126">File Naming Conventions</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to__multibitrate_MP4_file_naming)
  * [<span data-ttu-id="c6748-127">發行到 hello 工作流程的根元件內容</span><span class="sxs-lookup"><span data-stu-id="c6748-127">Publishing component properties onto hello workflow root</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to__multibitrate_MP4_publishing)
  * [<span data-ttu-id="c6748-128">讓產生的輸出檔案名稱依賴發佈的屬性值</span><span class="sxs-lookup"><span data-stu-id="c6748-128">Have generated output file names rely on published property values</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to__multibitrate_MP4_output_files)
* [<span data-ttu-id="c6748-129">加入縮圖 toomultibitrate MP4 輸出</span><span class="sxs-lookup"><span data-stu-id="c6748-129">Adding thumbnails toomultibitrate MP4 output</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4)
  * [<span data-ttu-id="c6748-130">工作流程概觀 tooadd 的縮圖</span><span class="sxs-lookup"><span data-stu-id="c6748-130">Workflow overview tooadd thumbnails to</span></span>](#workflow-overview-to-add-thumbnails-to)
  * [<span data-ttu-id="c6748-131">加入 JPG 編碼</span><span class="sxs-lookup"><span data-stu-id="c6748-131">Adding JPG Encoding</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4__with_jpg)
  * [<span data-ttu-id="c6748-132">處理色彩空間轉換</span><span class="sxs-lookup"><span data-stu-id="c6748-132">Dealing with Color Space conversion</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4_color_space)
  * [<span data-ttu-id="c6748-133">寫入 hello 縮圖</span><span class="sxs-lookup"><span data-stu-id="c6748-133">Writing hello thumbnails</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4_writing_thumbnails)
  * [<span data-ttu-id="c6748-134">偵測工作流程中的錯誤</span><span class="sxs-lookup"><span data-stu-id="c6748-134">Detecting errors in a workflow</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4_errors)
  * [<span data-ttu-id="c6748-135">工作流程完成</span><span class="sxs-lookup"><span data-stu-id="c6748-135">Finished Workflow</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4_finish)
* [<span data-ttu-id="c6748-136">多位元速率 MP4 輸出以時間為基礎的修剪</span><span class="sxs-lookup"><span data-stu-id="c6748-136">Time-based trimming of multibitrate MP4 output</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#time_based_trim)
  * [<span data-ttu-id="c6748-137">加入要修剪的工作流程概觀 toostart</span><span class="sxs-lookup"><span data-stu-id="c6748-137">Workflow overview toostart adding trimming to</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#time_based_trim_start)
  * [<span data-ttu-id="c6748-138">使用資料流修剪器 hello</span><span class="sxs-lookup"><span data-stu-id="c6748-138">Using hello Stream Trimmer</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#time_based_trim_use_stream_trimmer)
  * [<span data-ttu-id="c6748-139">工作流程完成</span><span class="sxs-lookup"><span data-stu-id="c6748-139">Finished Workflow</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#time_based_trim_finish)
* [<span data-ttu-id="c6748-140">簡介 hello 編寫指令碼元件</span><span class="sxs-lookup"><span data-stu-id="c6748-140">Introducing hello Scripted Component</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#scripting)
  * [<span data-ttu-id="c6748-141">工作流程內的指令碼：Hello World</span><span class="sxs-lookup"><span data-stu-id="c6748-141">Scripting within a workflow: hello world</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#scripting_hello_world)
* [<span data-ttu-id="c6748-142">多位元速率 MP4 輸出以畫面格為基礎的修剪</span><span class="sxs-lookup"><span data-stu-id="c6748-142">Frame-based trimming of multibitrate MP4 output</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim)
  * [<span data-ttu-id="c6748-143">加入要修剪的概觀 toostart 藍圖</span><span class="sxs-lookup"><span data-stu-id="c6748-143">Blueprint overview toostart adding trimming to</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim_start)
  * [<span data-ttu-id="c6748-144">使用 hello 剪輯清單 XML</span><span class="sxs-lookup"><span data-stu-id="c6748-144">Using hello Clip List XML</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim_clip_list)
  * [<span data-ttu-id="c6748-145">修改編寫指令碼元件中的 hello 剪輯清單</span><span class="sxs-lookup"><span data-stu-id="c6748-145">Modifying hello clip list from a Scripted Component</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim_modify_clip_list)
  * [<span data-ttu-id="c6748-146">加入 ClippingEnabled 便利屬性</span><span class="sxs-lookup"><span data-stu-id="c6748-146">Adding a ClippingEnabled convenience property</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim_clippingenabled_prop)

## <span data-ttu-id="c6748-147"><a id="MXF_to_MP4"></a>將 MXF 編碼為單一位元速率 MP4</span><span class="sxs-lookup"><span data-stu-id="c6748-147"><a id="MXF_to_MP4"></a>Encoding MXF into a single bitrate MP4</span></span>
<span data-ttu-id="c6748-148">在本逐步解說中，我們將使用來自 .MXF 輸入檔案 AAC-HE 編碼的音訊來建立單一位元速率 .MP4 檔案。</span><span class="sxs-lookup"><span data-stu-id="c6748-148">In this walkthrough we'll create a single bitrate .MP4 file with AAC-HE encoded audio from an .MXF input file.</span></span>

### <span data-ttu-id="c6748-149"><a id="MXF_to_MP4_start_new"></a>開始新的工作流程</span><span class="sxs-lookup"><span data-stu-id="c6748-149"><a id="MXF_to_MP4_start_new"></a>Starting a new workflow</span></span>
<span data-ttu-id="c6748-150">開啟「工作流程設計工具」，然後選取 [檔案] - [新增工作區] - [轉碼藍圖]</span><span class="sxs-lookup"><span data-stu-id="c6748-150">Open Workflow Designer and select "File"-"New Workspace"-"Transcode Blueprint"</span></span>

<span data-ttu-id="c6748-151">hello 新的工作流程將會顯示 3 個元素：</span><span class="sxs-lookup"><span data-stu-id="c6748-151">hello new workflow will show 3 elements:</span></span>

* <span data-ttu-id="c6748-152">主要來源檔案</span><span class="sxs-lookup"><span data-stu-id="c6748-152">Primary Source File</span></span>
* <span data-ttu-id="c6748-153">剪輯清單 XML</span><span class="sxs-lookup"><span data-stu-id="c6748-153">Clip List XML</span></span>
* <span data-ttu-id="c6748-154">輸出檔案/資產</span><span class="sxs-lookup"><span data-stu-id="c6748-154">Output File/Asset</span></span>  

![新編碼工作流程](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-transcode-blueprint.png)

<span data-ttu-id="c6748-156">*新編碼工作流程*</span><span class="sxs-lookup"><span data-stu-id="c6748-156">*New Encoding Workflow*</span></span>

### <span data-ttu-id="c6748-157"><a id="MXF_to_MP4_with_file_input"></a>使用媒體檔案輸入 hello</span><span class="sxs-lookup"><span data-stu-id="c6748-157"><a id="MXF_to_MP4_with_file_input"></a>Using hello Media File Input</span></span>
<span data-ttu-id="c6748-158">順序 tooaccept 在我們的輸入的媒體檔案，啟動新增媒體檔案輸入的元件。</span><span class="sxs-lookup"><span data-stu-id="c6748-158">In order tooaccept our input media file, one starts with adding a Media File Input component.</span></span> <span data-ttu-id="c6748-159">tooadd 元件 toohello 的工作流程，hello 儲存機制搜尋 方塊中尋找它，並將 hello 預期項目拖曳至 hello 設計工具窗格。</span><span class="sxs-lookup"><span data-stu-id="c6748-159">tooadd a component toohello workflow, look for it in hello Repository search box and drag hello desired entry onto hello designer pane.</span></span> <span data-ttu-id="c6748-160">Hello 輸入媒體檔案進行此作業並 hello 輸入媒體檔案從連接 hello 主要原始程式檔元件 toohello Filename 輸入的 pin。</span><span class="sxs-lookup"><span data-stu-id="c6748-160">Do this for hello Media File Input and connect hello Primary Source File component toohello Filename input pin from hello Media File Input.</span></span>

![連接的媒體檔案輸入](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-file-input.png)

<span data-ttu-id="c6748-162">*連接的媒體檔案輸入*</span><span class="sxs-lookup"><span data-stu-id="c6748-162">*Connected Media File Input*</span></span>

<span data-ttu-id="c6748-163">我們可以執行許多其他之前，我們必須先 tooindicate toohello 工作流程設計工具範例的檔案，我們都希望 toouse toodesign 我們的工作流程。</span><span class="sxs-lookup"><span data-stu-id="c6748-163">Before we can do much else, we'll first need tooindicate toohello workflow designer what sample file we'd like toouse toodesign our workflow with.</span></span> <span data-ttu-id="c6748-164">因此 toodo 按一下 hello 設計工具窗格的背景，然後尋找在 hello 右側的屬性窗格中的 hello 主要原始程式檔屬性。</span><span class="sxs-lookup"><span data-stu-id="c6748-164">toodo so, click hello designer pane background and look for hello Primary Source File property on hello right-hand property pane.</span></span> <span data-ttu-id="c6748-165">按一下 hello 資料夾圖示，然後選取所需的 hello 檔案 tootest hello 的工作流程。</span><span class="sxs-lookup"><span data-stu-id="c6748-165">Click hello folder icon and select hello desired file tootest hello workflow with.</span></span> <span data-ttu-id="c6748-166">進行此設定，如 hello 媒體檔案輸入元件會檢查 hello 檔案，並填入它檢查其輸出 pin tooreflect hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="c6748-166">As soon as this is done, hello Media File Input component will inspect hello file and populate its output pins tooreflect hello file it inspected.</span></span>

![填入媒體檔案輸入](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-populated-media-file-input.png)

<span data-ttu-id="c6748-168">*填入媒體檔案輸入*</span><span class="sxs-lookup"><span data-stu-id="c6748-168">*Populated Media File Input*</span></span>

<span data-ttu-id="c6748-169">這會指定使用哪些輸入，我們都希望 toowork 與，而不知道尚未 hello 編碼的輸出應該移至。</span><span class="sxs-lookup"><span data-stu-id="c6748-169">While this specifies with what input we'd like toowork with, it doesn't tell yet where hello encoded output should go to.</span></span> <span data-ttu-id="c6748-170">已設定為主要原始程式檔，類似 toohow hello 現在設定 hello 正下方的輸出資料夾變數屬性。</span><span class="sxs-lookup"><span data-stu-id="c6748-170">Similar toohow hello Primary Source File was configured, now configure hello Output Folder Variable property, just below it.</span></span>

![設定輸入和輸出屬性](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-configured-io-properties.png)

<span data-ttu-id="c6748-172">*設定輸入和輸出屬性*</span><span class="sxs-lookup"><span data-stu-id="c6748-172">*Configured Input and Output properties*</span></span>

### <span data-ttu-id="c6748-173"><a id="MXF_to_MP4_streams"></a>檢查媒體串流</span><span class="sxs-lookup"><span data-stu-id="c6748-173"><a id="MXF_to_MP4_streams"></a>Inspecting media streams</span></span>
<span data-ttu-id="c6748-174">通常它是所需的 hello 資料流的外觀類似的 tooknow 流經 hello 工作流程。</span><span class="sxs-lookup"><span data-stu-id="c6748-174">Often it's desired tooknow how hello stream looks like that flows through hello workflow.</span></span> <span data-ttu-id="c6748-175">輸出或輸入的 pin，任何 hello 元件上，只要按一下 tooinspect hello 工作流程，在任何時間點的資料流。</span><span class="sxs-lookup"><span data-stu-id="c6748-175">tooinspect a stream at any point in hello workflow, just click an output or input pin on any of hello components.</span></span> <span data-ttu-id="c6748-176">在此情況下，請按一下從我們的媒體檔案輸入 hello 未壓縮視訊輸出的 pin。</span><span class="sxs-lookup"><span data-stu-id="c6748-176">In this case, try clicking on hello Uncompressed Video output pin from our Media File Input.</span></span> <span data-ttu-id="c6748-177">對話方塊會開啟，可讓 tooinspect hello 輸出視訊。</span><span class="sxs-lookup"><span data-stu-id="c6748-177">A dialog will open up that allows tooinspect hello outbound video.</span></span>

![檢查 hello 未壓縮視訊輸出連接](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-inspecting-uncompressed-video-output.png)

<span data-ttu-id="c6748-179">*檢查 hello 未壓縮視訊輸出連接*</span><span class="sxs-lookup"><span data-stu-id="c6748-179">*Inspecting hello Uncompressed Video output pin*</span></span>

<span data-ttu-id="c6748-180">在我們的案例中，它會告訴我們，比方說我們要對一段接近 2 分鐘的視訊，以 4:2:2 取樣每秒 24 個畫面格處理 1920x1080 輸入。</span><span class="sxs-lookup"><span data-stu-id="c6748-180">In our case, it tells us for example that we're dealing with a 1920x1080 input at 24 frames per second in 4:2:2 sampling for a video of almost 2 minutes.</span></span>

### <span data-ttu-id="c6748-181"><a id="MXF_to_MP4_file_generation"></a>為產生的 MP4 檔案加入視訊編碼器</span><span class="sxs-lookup"><span data-stu-id="c6748-181"><a id="MXF_to_MP4_file_generation"></a>Adding a video encoder for .MP4 file generation</span></span>
<span data-ttu-id="c6748-182">請注意，現在，[未壓縮的視訊] 和多個 [未壓縮的音訊] 輸出接點可供用於我們的媒體檔案輸入。</span><span class="sxs-lookup"><span data-stu-id="c6748-182">Note that now, an Uncompressed Video and multiple Uncompressed Audio output pins are available for use on our Media File Input.</span></span> <span data-ttu-id="c6748-183">在訂單 tooencode hello 輸入的視訊，我們需要的編碼元件-在此情況下產生。MP4 檔案。</span><span class="sxs-lookup"><span data-stu-id="c6748-183">In order tooencode hello inbound video, we need an encoding component - in this case for generating .MP4 files.</span></span>

<span data-ttu-id="c6748-184">tooencode hello tooH.264 視訊資料流，並將 hello AVC 視訊編碼程式元件 toohello 設計工具介面。</span><span class="sxs-lookup"><span data-stu-id="c6748-184">tooencode hello video stream tooH.264, add hello AVC Video Encoder component toohello designer surface.</span></span> <span data-ttu-id="c6748-185">此元件會將未壓縮的視訊串流做為輸入，並在其輸出接點上提供 AVC 壓縮視訊串流。</span><span class="sxs-lookup"><span data-stu-id="c6748-185">This component takes an uncompress video stream as input and delivers an AVC compressed video stream on its output pin.</span></span>

![未連接的 AVC 編碼器](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-unconnected-avc-encoder.png)

<span data-ttu-id="c6748-187">*未連接的 AVC 編碼器*</span><span class="sxs-lookup"><span data-stu-id="c6748-187">*Unconnected AVC Encoder*</span></span>

<span data-ttu-id="c6748-188">其屬性會決定如何 hello 編碼完全執行。</span><span class="sxs-lookup"><span data-stu-id="c6748-188">Its properties determine how hello encoding exactly happens.</span></span> <span data-ttu-id="c6748-189">讓我們先看一些 hello 更重要的設定：</span><span class="sxs-lookup"><span data-stu-id="c6748-189">Let's have a look at some of hello more important settings:</span></span>

* <span data-ttu-id="c6748-190">輸出寬度和高度輸出： 這些屬性會決定 hello 的 hello 編碼視訊的解析度。</span><span class="sxs-lookup"><span data-stu-id="c6748-190">Output width and Output height: these determine hello resolution of hello encoded video.</span></span> <span data-ttu-id="c6748-191">在本例中，我們使用 640x360</span><span class="sxs-lookup"><span data-stu-id="c6748-191">In our case let's go with 640x360</span></span>
* <span data-ttu-id="c6748-192">畫面播放速率： 只要組 toopassthrough 採用 hello 來源畫面播放速率，時，可能 toooverride 這雖然。</span><span class="sxs-lookup"><span data-stu-id="c6748-192">Frame Rate: when set toopassthrough it will just adopt hello source frame rate, it's possible toooverride this though.</span></span> <span data-ttu-id="c6748-193">請注意，這類的畫面格速率轉換並非動作補償。</span><span class="sxs-lookup"><span data-stu-id="c6748-193">Note that such framerate conversion is not motion-compensated.</span></span>
* <span data-ttu-id="c6748-194">設定檔和層級： 這些決定 hello AVC 設定檔與層級。</span><span class="sxs-lookup"><span data-stu-id="c6748-194">Profile and Level: these determine hello AVC profile and level.</span></span> <span data-ttu-id="c6748-195">tooconveniently 取得詳細資訊需 hello 不同層級和設定檔，按一下 hello AVC 視訊編碼器元件上的 hello 問號圖示，然後 hello 說明頁面會顯示有關每 hello 層的其他詳細資料。</span><span class="sxs-lookup"><span data-stu-id="c6748-195">tooconveniently get more information about hello different levels and profiles, click hello question mark icon on hello AVC Video Encoder component and hello help page will show more detail about each of hello levels.</span></span> <span data-ttu-id="c6748-196">我們的範例，我們來使用層級 3.2 （hello 預設值） 的主要設定檔。</span><span class="sxs-lookup"><span data-stu-id="c6748-196">For our sample, let's go with Main Profile at level 3.2 (hello default).</span></span>
* <span data-ttu-id="c6748-197">速率控制模式和位元速率 (kbps)：我們的案例中，我們選擇使用 1200 kbps 常數位元速率 (CBR) 輸出</span><span class="sxs-lookup"><span data-stu-id="c6748-197">Rate Control Mode and Bitrate (kbps): in our scenario we opt for a constant bitrate (CBR) output at 1200 kbps</span></span>
* <span data-ttu-id="c6748-198">視訊格式: 這是有關 hello VUI （視訊可用性資訊），取得寫入 hello H.264 資料流 （可能由解碼器 tooenhance hello 顯示但 toocorrectly 不必要的側邊資訊解碼）：</span><span class="sxs-lookup"><span data-stu-id="c6748-198">Video Format: this is about hello VUI (Video Usability Information) that gets written into hello H.264 stream (side information that might be used by a decoder tooenhance hello display but not essential toocorrectly decode):</span></span>
* <span data-ttu-id="c6748-199">NTSC (一般用於美國或日本，使用 30 fps)</span><span class="sxs-lookup"><span data-stu-id="c6748-199">NTSC (typical for US or Japan, using 30 fps)</span></span>
* <span data-ttu-id="c6748-200">PAL (一般用於歐洲地區，使用 25 fps)</span><span class="sxs-lookup"><span data-stu-id="c6748-200">PAL (typical for Europe, using 25 fps)</span></span>
* <span data-ttu-id="c6748-201">GOP 大小模式：針對我們的目的，我們將設定固定的 GOP 大小，主要間隔為 2 秒，並且關閉 GOP。</span><span class="sxs-lookup"><span data-stu-id="c6748-201">GOP Size Mode: we'll configure Fixed GOP Size for our purposes with a Key Interval of 2 seconds with Closed GOPs.</span></span> <span data-ttu-id="c6748-202">這可確保與 hello 動態封裝 Azure Media Services 提供的相容性。</span><span class="sxs-lookup"><span data-stu-id="c6748-202">This ensures compatibility with hello dynamic packaging Azure Media Services provides.</span></span>

<span data-ttu-id="c6748-203">toofeed AVC encoder 中，從 hello 媒體檔案輸入元件 toohello 未壓縮視訊輸入 pin hello AVC 編碼器連接 hello 未壓縮視訊輸出連接。</span><span class="sxs-lookup"><span data-stu-id="c6748-203">toofeed our AVC encoder, connect hello Uncompressed Video output pin from hello Media File Input component toohello Uncompressed Video input pin from hello AVC encoder.</span></span>

![連接的 AVC 編碼器](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-connected-avc-encoder.png)

<span data-ttu-id="c6748-205">*連接的 AVC 主要編碼器*</span><span class="sxs-lookup"><span data-stu-id="c6748-205">*Connected AVC Main encoder*</span></span>

### <span data-ttu-id="c6748-206"><a id="MXF_to_MP4_audio"></a>編碼的 hello 音訊資料流</span><span class="sxs-lookup"><span data-stu-id="c6748-206"><a id="MXF_to_MP4_audio"></a>Encoding hello audio stream</span></span>
<span data-ttu-id="c6748-207">此時，我們已編碼視訊，但 hello 原始未壓縮音訊資料流仍然需要 toobe 壓縮。</span><span class="sxs-lookup"><span data-stu-id="c6748-207">At this point, we have encoded video but hello original uncompressed audio stream still needs toobe compressed.</span></span> <span data-ttu-id="c6748-208">此我們會討論使用 aac 以編碼 hello AAC 編碼器 (Dolby) 元件。</span><span class="sxs-lookup"><span data-stu-id="c6748-208">For this we'll go with AAC encoding by hello AAC Encoder (Dolby) component.</span></span> <span data-ttu-id="c6748-209">將它加入 toohello 工作流程。</span><span class="sxs-lookup"><span data-stu-id="c6748-209">Add it toohello workflow.</span></span>

![未連接的 AVC 編碼器](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-unconnected-aac-encoder.png)

<span data-ttu-id="c6748-211">*未連接的 AAC 編碼器*</span><span class="sxs-lookup"><span data-stu-id="c6748-211">*Unconnected AAC encoder*</span></span>

<span data-ttu-id="c6748-212">現在有不相容的問題： 沒有只有單一未壓縮音訊輸入的 pin hello AAC 編碼器從多個可能的 hello 輸入媒體檔案會有兩個不同未壓縮的音訊資料流可用時： 一個用於保留音訊頻道，另一個用於 hello hello權限。</span><span class="sxs-lookup"><span data-stu-id="c6748-212">Now there's an incompatibility: there's only a single uncompressed audio input pin from hello AAC Encoder while more than likely hello Media File Input will have two different uncompressed audio stream available: one for hello left audio channel and one for hello right.</span></span> <span data-ttu-id="c6748-213">(如果您正在處理環繞音效，則是 6 聲道。)如此就不可能 toodirectly hello 音訊 hello 媒體檔案輸入來源連接到 hello AAC 音訊編碼器。</span><span class="sxs-lookup"><span data-stu-id="c6748-213">(If you're dealing with surround sound, that's 6 channels.) So it's not possible toodirectly connect hello audio from hello Media File Input source into hello AAC audio encoder.</span></span> <span data-ttu-id="c6748-214">hello AAC 元件必須要有所謂的 「 交錯"音訊資料流： 同時具有單一資料流 hello 與彼此交錯的左邊和 hello 右邊的通道。</span><span class="sxs-lookup"><span data-stu-id="c6748-214">hello AAC component expects a so-called "interleaved" audio stream: a single stream that has both hello left and hello right channels interleaved with each other.</span></span> <span data-ttu-id="c6748-215">我們已了解我們的來源媒體檔案從音訊音軌 hello 來源中的哪個位置，在我們可以正確地產生這類交錯的音訊資料流以 hello 指派 left 和 right 喇叭的位置。</span><span class="sxs-lookup"><span data-stu-id="c6748-215">Once we know from our source media file which audio tracks are on what position in hello source, we can generate such interleaved audio stream with hello correctly assigned speaker positions for left and right.</span></span>

<span data-ttu-id="c6748-216">第一次一個也會想 toogenerated 從所需的 hello 來源音訊頻道的交錯式資料流。</span><span class="sxs-lookup"><span data-stu-id="c6748-216">First one will want toogenerated an interleaved stream from hello required source audio channels.</span></span> <span data-ttu-id="c6748-217">hello 音訊資料流 Interleaver 元件會處理這項工作給我們。</span><span class="sxs-lookup"><span data-stu-id="c6748-217">hello Audio Stream Interleaver component will handle this for us.</span></span> <span data-ttu-id="c6748-218">將它加入 toohello 工作流程並 hello 音訊輸出從連線到其中的媒體檔案輸入 hello。</span><span class="sxs-lookup"><span data-stu-id="c6748-218">Add it toohello workflow and connect hello audio outputs from hello Media File Input into it.</span></span>

![連接音訊串流交錯器](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-connected-audio-stream-interleaver.png)

<span data-ttu-id="c6748-220">*連接音訊串流交錯器*</span><span class="sxs-lookup"><span data-stu-id="c6748-220">*Connected Audio Stream Interleaver*</span></span>

<span data-ttu-id="c6748-221">現在，我們已經交錯的音訊資料流時，我們仍未指定 tooassign hello 左或向右喇叭来放置的位置。</span><span class="sxs-lookup"><span data-stu-id="c6748-221">Now that we have an interleaved audio stream, we still didn't specify where tooassign hello left or right speaker positions to.</span></span> <span data-ttu-id="c6748-222">在此順序 toospecify，我們可以利用 hello 喇叭位置 Assigner。</span><span class="sxs-lookup"><span data-stu-id="c6748-222">In order toospecify this, we can leverage hello Speaker Position Assigner.</span></span>

![加入喇叭位置指定器](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-adding-speaker-position-assigner.png)

<span data-ttu-id="c6748-224">*加入喇叭位置指定器*</span><span class="sxs-lookup"><span data-stu-id="c6748-224">*Adding a Speaker Position Assigner*</span></span>

<span data-ttu-id="c6748-225">設定用於 hello 喇叭位置 Assigner 立體聲的輸入資料流編碼器預設篩選條件的 「 自訂 」 並 hello 通道預先設定稱為 「 2.0 （L、 R）"。</span><span class="sxs-lookup"><span data-stu-id="c6748-225">Configure hello Speaker Position Assigner for use with a stereo input stream through an Encoder Preset Filter of "Custom" and hello Channel Preset called "2.0 (L,R)".</span></span> <span data-ttu-id="c6748-226">（這會指派 hello 左的喇叭位置 toochannel 1 和 hello 右喇叭位置 toochannel 2）。</span><span class="sxs-lookup"><span data-stu-id="c6748-226">(This will assign hello left speaker position toochannel 1 and hello right speaker position toochannel 2.)</span></span>

<span data-ttu-id="c6748-227">Hello hello 喇叭位置 Assigner toohello 輸入 hello AAC 編碼器的輸出連接。</span><span class="sxs-lookup"><span data-stu-id="c6748-227">Connect hello output of hello Speaker Position Assigner toohello input of hello AAC Encoder.</span></span> <span data-ttu-id="c6748-228">然後，告訴 hello AAC 編碼器 toowork"2.0 （L、 R）"預設通道，讓它知道 toodeal 與立體聲音訊做為輸入。</span><span class="sxs-lookup"><span data-stu-id="c6748-228">Then, tell hello AAC Encoder toowork with a "2.0 (L,R)" Channel Preset, so it knows toodeal with stereo audio as input.</span></span>

### <span data-ttu-id="c6748-229"><a id="MXF_to_MP4_audio_and_fideo"></a>將音訊和視訊串流多工處理為 MP4 容器</span><span class="sxs-lookup"><span data-stu-id="c6748-229"><a id="MXF_to_MP4_audio_and_fideo"></a>Multiplexing Audio and Video streams into an MP4 container</span></span>
<span data-ttu-id="c6748-230">假設我們有 AVC 編碼的視訊串流和 AAC 編碼的音訊串流，我們可以將兩者擷取為 .MP4 容器。</span><span class="sxs-lookup"><span data-stu-id="c6748-230">Given our AVC encoded video stream and our AAC encoded audio stream, we can capture both into an .MP4 container.</span></span> <span data-ttu-id="c6748-231">hello 的成單一混用不同的資料流的程序稱為 「 多工 」 （或 「 muxing"）。</span><span class="sxs-lookup"><span data-stu-id="c6748-231">hello process of mixing different streams into a single one is called "multiplexing" (or "muxing").</span></span> <span data-ttu-id="c6748-232">在此情況下，我們正在交錯 hello 音訊與視訊 hello 一致的單一資料流。MP4 封裝。</span><span class="sxs-lookup"><span data-stu-id="c6748-232">In this case we're interleaving hello audio and hello video streams in a single coherent .MP4 package.</span></span> <span data-ttu-id="c6748-233">此作業對於協調的 hello 元件。MP4 容器稱為 hello ISO mpeg-4 多工器。</span><span class="sxs-lookup"><span data-stu-id="c6748-233">hello component that coordinates this for an .MP4 container is called hello ISO MPEG-4 Multiplexer.</span></span> <span data-ttu-id="c6748-234">加入一個 toohello 設計工具介面，並連接 hello AVC 視訊編碼器和 hello AAC 編碼器 tooits 輸入。</span><span class="sxs-lookup"><span data-stu-id="c6748-234">Add one toohello designer surface and connect both hello AVC Video Encoder and hello AAC Encoder tooits inputs.</span></span>

![連接的 MPEG4 多工器](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-connected-mpeg4-multiplexer.png)

<span data-ttu-id="c6748-236">*連接的 MPEG4 多工器*</span><span class="sxs-lookup"><span data-stu-id="c6748-236">*Connected MPEG4 Multiplexer*</span></span>

### <span data-ttu-id="c6748-237"><a id="MXF_to_MP4_writing_mp4"></a>寫入 hello MP4 檔案</span><span class="sxs-lookup"><span data-stu-id="c6748-237"><a id="MXF_to_MP4_writing_mp4"></a>Writing hello MP4 file</span></span>
<span data-ttu-id="c6748-238">寫入輸出檔時，使用 hello 檔案輸出的元件。</span><span class="sxs-lookup"><span data-stu-id="c6748-238">When writing an output file, hello File Output component is used.</span></span> <span data-ttu-id="c6748-239">使其輸出寫入 toodisk，我們就可以連接 ISO mpeg-4 多工器 hello toohello 的輸出。</span><span class="sxs-lookup"><span data-stu-id="c6748-239">We can connect this toohello output of hello ISO MPEG-4 Multiplexer so that its output gets written toodisk.</span></span> <span data-ttu-id="c6748-240">toodo，連接到 hello 容器 (MPEG-4) 輸出 pin toohello 寫入輸入的 pin 的 hello 輸出檔。</span><span class="sxs-lookup"><span data-stu-id="c6748-240">toodo this, connect hello Container (MPEG-4) output pin toohello Write input pin of hello File Output.</span></span>

![連接的檔案輸出](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-connected-file-output.png)

<span data-ttu-id="c6748-242">*連接的檔案輸出*</span><span class="sxs-lookup"><span data-stu-id="c6748-242">*Connected File Output*</span></span>

<span data-ttu-id="c6748-243">將使用的 hello filename 取決於 hello 檔案屬性。</span><span class="sxs-lookup"><span data-stu-id="c6748-243">hello filename that will be used is determined by hello File property.</span></span> <span data-ttu-id="c6748-244">雖然該屬性可能是硬式編碼 tooa 給定值，一個最有可能會想 tooset 它透過運算式改為。</span><span class="sxs-lookup"><span data-stu-id="c6748-244">While that property can be hardcoded tooa given value, most likely one will want tooset it through an expression instead.</span></span>

<span data-ttu-id="c6748-245">toohave hello 工作流程自動判斷 hello 輸出檔案名稱屬性的運算式，請按一下 hello 按鈕下一個 toohello 檔案名稱 （下一步 toohello 資料夾圖示）。</span><span class="sxs-lookup"><span data-stu-id="c6748-245">toohave hello workflow automatically determine hello output File name property from an expression, click hello buton next toohello File name (next toohello folder icon).</span></span> <span data-ttu-id="c6748-246">從 hello 下拉式功能表，然後選取 「 運算式 」。</span><span class="sxs-lookup"><span data-stu-id="c6748-246">From hello drop down menu then select "Expression".</span></span> <span data-ttu-id="c6748-247">這會顯示 hello 運算式編輯器。</span><span class="sxs-lookup"><span data-stu-id="c6748-247">This will bring up hello expression editor.</span></span> <span data-ttu-id="c6748-248">第一次清除 hello 編輯器 hello 內容。</span><span class="sxs-lookup"><span data-stu-id="c6748-248">Clear hello contents of hello editor first.</span></span>

![空白的運算式編輯器](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-empty-expression-editor.png)

<span data-ttu-id="c6748-250">*空白的運算式編輯器*</span><span class="sxs-lookup"><span data-stu-id="c6748-250">*Empty Expression Editor*</span></span>

<span data-ttu-id="c6748-251">hello 運算式編輯器可讓 tooenter 與一個或多個變數混合任何常值。</span><span class="sxs-lookup"><span data-stu-id="c6748-251">hello expression editor allows tooenter any literal value, mixed with one or more variables.</span></span> <span data-ttu-id="c6748-252">以貨幣符號開頭的變數。</span><span class="sxs-lookup"><span data-stu-id="c6748-252">Variables start with a dollar sign.</span></span> <span data-ttu-id="c6748-253">當您叫用 hello $ 索引鍵，hello 編輯器會顯示下拉式清單方塊選擇可用的變數。</span><span class="sxs-lookup"><span data-stu-id="c6748-253">As you hit hello $ key, hello editor will show a dropdown box with a choice of available variables.</span></span> <span data-ttu-id="c6748-254">在我們的案例中，我們將使用 hello 輸出目錄變數和 hello 基底的輸入的檔案名稱的變數的組合：</span><span class="sxs-lookup"><span data-stu-id="c6748-254">In our case we'll use a combination of hello output directory variable and hello base input file name variable:</span></span>

    ${ROOT_outputWriteDirectory}\\${ROOT_sourceFileBaseName}.MP4

![填入運算式編輯器](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-expression-editor.png)

<span data-ttu-id="c6748-256">*填入運算式編輯器*</span><span class="sxs-lookup"><span data-stu-id="c6748-256">*Filled out Expression Editor*</span></span>

> [!NOTE]
> <span data-ttu-id="c6748-257">順序 toosee 看到您在 Azure 中的編碼工作的輸出檔，您必須提供 hello 運算式編輯器中的值。</span><span class="sxs-lookup"><span data-stu-id="c6748-257">In order toosee see an output file of your encoding job in Azure, you must provide a value in hello expression editor.</span></span>
>
>

<span data-ttu-id="c6748-258">當您按下 [確定] 確認 hello 運算式時，hello 屬性視窗就會在此時間點預覽 toowhat 值 hello 檔案屬性解析。</span><span class="sxs-lookup"><span data-stu-id="c6748-258">When you confirm hello expression by hitting ok, hello property window will preview toowhat value hello File property resolves at this point in time.</span></span>

![檔案運算式解析輸出目錄](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-file-expression-resolves-output-dir.png)

<span data-ttu-id="c6748-260">*檔案運算式解析輸出目錄*</span><span class="sxs-lookup"><span data-stu-id="c6748-260">*File Expression resolves output dir*</span></span>

### <span data-ttu-id="c6748-261"><a id="MXF_to_MP4_asset_from_output"></a>從 hello 輸出檔案建立 Media Services 資產</span><span class="sxs-lookup"><span data-stu-id="c6748-261"><a id="MXF_to_MP4_asset_from_output"></a>Creating a Media Services Asset from hello output file</span></span>
<span data-ttu-id="c6748-262">雖然我們已經寫 MP4 輸出檔案，我們仍需要 tooindicate 這個檔案所屬 toohello 輸出的資產的媒體服務會產生的結果執行此工作流程。</span><span class="sxs-lookup"><span data-stu-id="c6748-262">While we have written an MP4 output file, we still need tooindicate that this file belongs toohello output asset which media services will generate as a result of executing this workflow.</span></span> <span data-ttu-id="c6748-263">會使用 toothis 結束時，將輸出檔案資產節點 hello hello 工作流程畫布上。</span><span class="sxs-lookup"><span data-stu-id="c6748-263">toothis end, hello Output File/Asset node on hello workflow canvas is used.</span></span> <span data-ttu-id="c6748-264">所有連入的檔案到此節點就會產生部分 hello 產生 Azure Media Services 資產。</span><span class="sxs-lookup"><span data-stu-id="c6748-264">All incoming files into this node will make part of hello resulting Azure Media Services asset.</span></span>

<span data-ttu-id="c6748-265">連接 hello 檔案輸出元件 toohello 輸出檔案資產元件 toofinish hello 工作流程。</span><span class="sxs-lookup"><span data-stu-id="c6748-265">Connect hello File Output component toohello Output File/Asset component toofinish hello workflow.</span></span>

![工作流程完成](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-finished-workflow.png)

<span data-ttu-id="c6748-267">*工作流程完成*</span><span class="sxs-lookup"><span data-stu-id="c6748-267">*Finished Workflow*</span></span>

### <span data-ttu-id="c6748-268"><a id="MXF_to_MP4_test"></a>測試 hello 完成在本機工作流程</span><span class="sxs-lookup"><span data-stu-id="c6748-268"><a id="MXF_to_MP4_test"></a>Test hello finished workflow locally</span></span>
<span data-ttu-id="c6748-269">在本機，tootest hello 工作流程叫用 hello hello 頂端的工具列中的 [hello] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="c6748-269">tootest hello workflow locally, hit hello play button in hello toolbar at hello top.</span></span> <span data-ttu-id="c6748-270">Hello 工作流程執行完成時，檢查 hello hello 設定輸出資料夾中產生的輸出。</span><span class="sxs-lookup"><span data-stu-id="c6748-270">When hello workflow finished executing, inspect hello output generated in hello configured output folder.</span></span> <span data-ttu-id="c6748-271">您會看見 hello 完成從 hello MXF 輸入原始程式檔已編碼的 MP4 輸出檔。</span><span class="sxs-lookup"><span data-stu-id="c6748-271">You'll see hello finished MP4 output file that was encoded from hello MXF input source file.</span></span>

## <span data-ttu-id="c6748-272"><a id="MXF_to_MP4_with_dyn_packaging"></a>將 MXF 編碼為 MP4 - 多位元速率動態封裝已啟用</span><span class="sxs-lookup"><span data-stu-id="c6748-272"><a id="MXF_to_MP4_with_dyn_packaging"></a>Encoding MXF into MP4 - multibitrate dynamic packaging enabled</span></span>
<span data-ttu-id="c6748-273">在本逐步解說中，我們將使用來單一 .MXF 輸入檔案 AAC 編碼的音訊來建立一組多位元速率 MP4 檔案。</span><span class="sxs-lookup"><span data-stu-id="c6748-273">In this walkthrough we'll create a set of multiple bitrate MP4 files with AAC encoded audio from a single .MXF input file.</span></span>

<span data-ttu-id="c6748-274">當多位元速率資產輸出是所需的組合用於與 Azure Media Services 的每個不同的位元速率與解析度需要 toobe 產生多個 gop 之 MP4 檔案所提供的 hello 動態封裝功能。</span><span class="sxs-lookup"><span data-stu-id="c6748-274">When a multi-bitrate asset output is desired for use in combination with hello Dynamic Packaging features offered by Azure Media Services, multiple GOP-aligned MP4 files of each a different bitrate and resolution will need toobe generated.</span></span> <span data-ttu-id="c6748-275">因此，hello toodo[編碼成單一位元速率 MP4 的 MXF](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4)逐步解說提供很好的起點。</span><span class="sxs-lookup"><span data-stu-id="c6748-275">toodo so, hello [Encoding MXF into a single bitrate MP4](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4) walkthrough provides us with a good starting point.</span></span>

![開始工作流程](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-starting-workflow.png)

<span data-ttu-id="c6748-277">*開始工作流程*</span><span class="sxs-lookup"><span data-stu-id="c6748-277">*Starting Workflow*</span></span>

### <span data-ttu-id="c6748-278"><a id="MXF_to_MP4_with_dyn_packaging_more_outputs"></a>加入一或多個其他的 MP4 輸出</span><span class="sxs-lookup"><span data-stu-id="c6748-278"><a id="MXF_to_MP4_with_dyn_packaging_more_outputs"></a>Adding one or more additional MP4 outputs</span></span>
<span data-ttu-id="c6748-279">我們產生的 Azure 媒體服務資產中的每個 MP4 檔案，將支援不同的位元速率與解析度。</span><span class="sxs-lookup"><span data-stu-id="c6748-279">Every MP4 file in our resulting Azure Media Services asset will support a different bitrate and resolution.</span></span> <span data-ttu-id="c6748-280">讓我們加入一個或多個 MP4 輸出檔案 toohello 工作流程。</span><span class="sxs-lookup"><span data-stu-id="c6748-280">Let's add one or more MP4 output files toohello workflow.</span></span>

<span data-ttu-id="c6748-281">我們有 toomake 確定所有我們視訊編碼器以建立 hello 相同的設定，它的最方便 tooduplicate hello 現有 AVC 視訊編碼程式，並設定另一個組合的解析度及位元速率 （讓我們加入一個 960 x 540 在第二個位於每 25 的畫面格2,5 Mbps)。</span><span class="sxs-lookup"><span data-stu-id="c6748-281">toomake sure we have all our video encoders created with hello same settings, it's most convenient tooduplicate hello already existing AVC Video Encoder and configure another combination of resolution and bitrate (let's add one of 960 x 540 at 25 frames per second at 2,5 Mbps).</span></span> <span data-ttu-id="c6748-282">tooduplicate hello 現有的編碼器，複製貼上它 hello 設計工具介面上。</span><span class="sxs-lookup"><span data-stu-id="c6748-282">tooduplicate hello existing encoder, copy paste it on hello designer surface.</span></span>

<span data-ttu-id="c6748-283">連接到我們新的 AVC 元件的媒體檔案輸入 hello 的 hello 未壓縮視訊輸出連接。</span><span class="sxs-lookup"><span data-stu-id="c6748-283">Connect hello Uncompressed Video output pin of hello Media File Input into our new AVC component.</span></span>

![連接第二個 AVC 編碼器](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-second-avc-encoder-connected.png)

<span data-ttu-id="c6748-285">*連接第二個 AVC 編碼器*</span><span class="sxs-lookup"><span data-stu-id="c6748-285">*Second AVC encoder connected*</span></span>

<span data-ttu-id="c6748-286">現在採用我們新 AVC 編碼器 toooutput 960 x 540 以 2,5 Mbps 的 hello 組態。</span><span class="sxs-lookup"><span data-stu-id="c6748-286">Now adapt hello configuration for our new AVC encoder toooutput 960x540 at 2,5 Mbps.</span></span> <span data-ttu-id="c6748-287">(對此使用其屬性 [輸出寬度]、[輸出高度] 和 [位元速率 (kbps)]。)</span><span class="sxs-lookup"><span data-stu-id="c6748-287">(Use its properties "Output width", "Output height", and "Bitrate (kbps)" for this.)</span></span>

<span data-ttu-id="c6748-288">指定我們想要搭配 Azure Media Services 的動態封裝 toouse hello 產生資產，hello 串流端點必須能夠從這些 MP4 檔案 HLS/分散 MP4/DASH 片段完全對齊的 tooeach 其他的方式產生 toobe要切換不同的位元之間的用戶端會收到單一 smooth 連續視訊和音訊體驗。</span><span class="sxs-lookup"><span data-stu-id="c6748-288">Given we want toouse hello resulting asset together with Azure Media Services' dynamic packaging, hello streaming endpoint needs toobe capable of generating from these MP4 files HLS/Fragmented MP4/DASH fragments that are exactly aligned tooeach other in a way that clients that are switching between different bitrates get a single smooth continuous video and audio experience.</span></span> <span data-ttu-id="c6748-289">發生，我們需要在這兩個 AVC 編碼器的 hello 屬性 hello GOP （「 群組的圖片 」） 的這兩個 MP4 檔案大小設定 tooensure toomake too2 秒，都可以做到：</span><span class="sxs-lookup"><span data-stu-id="c6748-289">toomake that happen, we need tooensure that, in hello properties of both AVC encoders hello GOP ("group of pictures") size for both MP4 files is set too2 seconds, which can be done by:</span></span>

* <span data-ttu-id="c6748-290">設定 hello GOP 調整大小模式 tooFixed GOP 大小和</span><span class="sxs-lookup"><span data-stu-id="c6748-290">setting hello GOP Size Mode tooFixed GOP size and</span></span>
* <span data-ttu-id="c6748-291">hello 金鑰畫面格間隔 tootwo 秒數。</span><span class="sxs-lookup"><span data-stu-id="c6748-291">hello Key Frame Interval tootwo seconds.</span></span>
* <span data-ttu-id="c6748-292">也沒有自己的相依性設定 hello GOP IDR 控制項 tooClosed GOP tooensure 長久以來的所有的 GOP</span><span class="sxs-lookup"><span data-stu-id="c6748-292">also set hello GOP IDR Control tooClosed GOP tooensure all GOP's are standing on their own without dependencies</span></span>

<span data-ttu-id="c6748-293">toomake 我們的工作流程方便 toounderstand，重新命名 hello 第一個 AVC 編碼器太"AVC 視訊編碼器 640x360 1200 kbps"hello 第二個 AVC 編碼器和"AVC 視訊編碼器 960 x 540 2500 kbps"。</span><span class="sxs-lookup"><span data-stu-id="c6748-293">toomake our workflow convenient toounderstand, rename hello first AVC encoder too"AVC Video Encoder 640x360 1200kbps" and hello second AVC encoder "AVC Video Encoder 960x540 2500 kbps".</span></span>

<span data-ttu-id="c6748-294">現在加入第二個「ISO MPEG-4 多工器」和第二個 [檔案輸出]。</span><span class="sxs-lookup"><span data-stu-id="c6748-294">Now add a second ISO MPEG-4 Multiplexer and a second File Output.</span></span> <span data-ttu-id="c6748-295">連接 hello 多工器 toohello 新 AVC 的編碼器，並確定其輸出導向至 hello 輸出檔。</span><span class="sxs-lookup"><span data-stu-id="c6748-295">Connect hello multiplexer toohello new AVC encoder and make sure its output is directed into hello File Output.</span></span> <span data-ttu-id="c6748-296">也連接 hello AAC 音訊編碼器輸出 toohello 新多工器的輸入。</span><span class="sxs-lookup"><span data-stu-id="c6748-296">Then also connect hello AAC audio encoder output toohello new multiplexer's input.</span></span> <span data-ttu-id="c6748-297">hello 檔案輸出又接著可以連接的 toohello 輸出檔案資產節點 tooadd 它 toohello 將建立的 Media Services 資產。</span><span class="sxs-lookup"><span data-stu-id="c6748-297">hello File Output in turn can then be connected toohello Output File/Asset node tooadd it toohello Media Services Asset that will be created.</span></span>

![連接第二個 Muxer 和檔案輸出](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-second-muxer-file-output-connected.png)

<span data-ttu-id="c6748-299">*連接第二個 Muxer 和檔案輸出*</span><span class="sxs-lookup"><span data-stu-id="c6748-299">*Second Muxer and File Output connected*</span></span>

<span data-ttu-id="c6748-300">使用 Azure Media Services 動態封裝的相容性，設定 hello 多工器的區塊模式 tooGOP 計數或持續時間，設定每個區塊 too1 hello Gop。</span><span class="sxs-lookup"><span data-stu-id="c6748-300">For compatibility with Azure Media Services dynamic packaging, configure hello multiplexer's Chunk Mode tooGOP count or duration and set hello GOPs per chunk too1.</span></span> <span data-ttu-id="c6748-301">（這應該是 hello 預設值）。</span><span class="sxs-lookup"><span data-stu-id="c6748-301">(This should be hello default.)</span></span>

![Muxer 區塊模式](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-muxer-chunk-modes.png)

<span data-ttu-id="c6748-303">*Muxer 區塊模式*</span><span class="sxs-lookup"><span data-stu-id="c6748-303">*Muxer Chunk Modes*</span></span>

<span data-ttu-id="c6748-304">注意： 您可能想 toorepeat 此程序的位元速率與解析度組合想 toohave 加入 toohello 資產輸出。</span><span class="sxs-lookup"><span data-stu-id="c6748-304">Note: you may want toorepeat this process for any other bitrate and resolution combinations you want toohave added toohello asset output.</span></span>

### <span data-ttu-id="c6748-305"><a id="MXF_to_MP4_with_dyn_packaging_conf_output_names"></a>設定 hello 檔案輸出名稱</span><span class="sxs-lookup"><span data-stu-id="c6748-305"><a id="MXF_to_MP4_with_dyn_packaging_conf_output_names"></a>Configuring hello file output names</span></span>
<span data-ttu-id="c6748-306">我們有一個以上的單一檔案加入的 toohello 輸出資產。</span><span class="sxs-lookup"><span data-stu-id="c6748-306">We have more than one single file added toohello output asset.</span></span> <span data-ttu-id="c6748-307">這會提供檔名的 hello 每個輸出檔案與彼此不同，並讓它成為 hello 檔案名稱中的 清除您要處理的可能即使套用的檔案命名慣例需要的 toomake 確定 hello。</span><span class="sxs-lookup"><span data-stu-id="c6748-307">This provides a need toomake sure hello filenames for each of hello output files are different from each other and maybe even apply a file-naming convention so it becomes clear from hello file name what you're dealing with.</span></span>

<span data-ttu-id="c6748-308">檔案輸出命名可以控制透過 hello 設計工具中的運算式。</span><span class="sxs-lookup"><span data-stu-id="c6748-308">File output naming can be controlled through expressions in hello designer.</span></span> <span data-ttu-id="c6748-309">開啟其中一個 hello 檔案輸出元件 hello 屬性 窗格，然後開啟 hello hello 檔案屬性的運算式編輯器。</span><span class="sxs-lookup"><span data-stu-id="c6748-309">Open hello property pane for one of hello File Output components and open hello expression editor for hello File property.</span></span> <span data-ttu-id="c6748-310">我們第一個輸出檔案是否已透過下列運算式 hello (請參閱 hello 教學課程，可從移[MXF tooa 單一位元速率 MP4 輸出](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4)):</span><span class="sxs-lookup"><span data-stu-id="c6748-310">Our first output file was configured through hello following expression (see hello tutorial for going from [MXF tooa single bitrate MP4 output](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4)):</span></span>

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}.MP4

<span data-ttu-id="c6748-311">這表示我們的檔案名稱由兩個變數： hello 輸出目錄 toowrite 在和 hello 原始程式檔的基底名稱。</span><span class="sxs-lookup"><span data-stu-id="c6748-311">This means that our filename is determined by two variables: hello output directory toowrite in and hello source file base name.</span></span> <span data-ttu-id="c6748-312">hello 前者會公開為 hello 工作流程根目錄上的屬性和 hello 後者由 hello 連入的檔案。</span><span class="sxs-lookup"><span data-stu-id="c6748-312">hello former is exposed as a property on hello workflow root and hello latter is determined by hello incoming file.</span></span> <span data-ttu-id="c6748-313">請注意該 hello 輸出目錄是您用於本機測試;這個屬性將會覆寫 hello 工作流程引擎 hello 工作流程由 Azure Media Services 中的 hello 以雲端為基礎的媒體處理器執行時。</span><span class="sxs-lookup"><span data-stu-id="c6748-313">Note that hello output directory is what you use for local testing; this property will be overridden by hello workflow engine when hello workflow is executed by hello cloud-based media processor in Azure Media Services.</span></span>
<span data-ttu-id="c6748-314">toogive 這兩個輸出檔案一致輸出命名，變更 hello 第一次檔案命名運算式：</span><span class="sxs-lookup"><span data-stu-id="c6748-314">toogive both our output files a consistent output naming, change hello first file naming expression to:</span></span>

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_640x360_1.MP4

<span data-ttu-id="c6748-315">並以第二個 hello:</span><span class="sxs-lookup"><span data-stu-id="c6748-315">and hello second to:</span></span>

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_960x540_2.MP4

<span data-ttu-id="c6748-316">執行中繼的測試回合 toomake 確定這兩個 MP4 輸出會正確產生檔案。</span><span class="sxs-lookup"><span data-stu-id="c6748-316">Execute an intermediate test run toomake sure both MP4 output files are properly generated.</span></span>

### <span data-ttu-id="c6748-317"><a id="MXF_to_MP4_with_dyn_packaging_audio_tracks"></a>加入個別的曲目</span><span class="sxs-lookup"><span data-stu-id="c6748-317"><a id="MXF_to_MP4_with_dyn_packaging_audio_tracks"></a>Adding a separate Audio Track</span></span>
<span data-ttu-id="c6748-318">當我們與我們的 MP4 輸出檔案產生的.ism 檔案 toogo，我們將稍後看到，我們也需要純音訊 MP4 檔案 hello 音訊播放軌為我們的彈性資料流。</span><span class="sxs-lookup"><span data-stu-id="c6748-318">As we'll see later when we generate an .ism file toogo with our MP4 output files, we will also require a audio-only MP4 file as hello audio track for our adaptive streaming.</span></span> <span data-ttu-id="c6748-319">toocreate 這個檔案，加入其他 muxer toohello 流程 （ISO-mpeg-4 多工器），連接 hello AAC 編碼器的輸出連接其輸入的 pin 與追蹤 1。</span><span class="sxs-lookup"><span data-stu-id="c6748-319">toocreate this file, add an additional muxer toohello workflow (ISO-MPEG-4 Multiplexer) and connect hello AAC encoder's output pin with its input pin for Track 1.</span></span>

![加入音訊 Muxer](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-audio-muxer-added.png)

<span data-ttu-id="c6748-321">*加入音訊 Muxer*</span><span class="sxs-lookup"><span data-stu-id="c6748-321">*Audio Muxer Added*</span></span>

<span data-ttu-id="c6748-322">Hello muxer 從建立第三個檔案輸出元件 toooutput hello 輸出資料流，並設定 hello 做為檔案命名運算式：</span><span class="sxs-lookup"><span data-stu-id="c6748-322">Create a third File Output component toooutput hello outbound stream from hello muxer and configure hello file naming expression as:</span></span>

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_128kbps_audio.MP4

![音訊 Muxer 建立輸出檔案](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-audio-muxer-creating-file-output.png)

<span data-ttu-id="c6748-324">*音訊 Muxer 建立輸出檔案*</span><span class="sxs-lookup"><span data-stu-id="c6748-324">*Audio Muxer creating File Output*</span></span>

### <span data-ttu-id="c6748-325"><a id="MXF_to_MP4_with_dyn_packaging_ism_file"></a>加入 hello。ISM SMIL 檔案</span><span class="sxs-lookup"><span data-stu-id="c6748-325"><a id="MXF_to_MP4_with_dyn_packaging_ism_file"></a>Adding hello .ISM SMIL File</span></span>
<span data-ttu-id="c6748-326">若是 hello 動態封裝 toowork 結合這兩個 MP4 檔案 （和 hello 純音訊 MP4） 在 Media Services 資產，我們也需要資訊清單檔案 (也稱為 「 SMIL"檔： 同步處理多媒體 Integration 語言)。</span><span class="sxs-lookup"><span data-stu-id="c6748-326">For hello dynamic packaging toowork in combination with both MP4 files (and hello audio-only MP4) in our Media Services asset, we also need a manifest file (also called a "SMIL" file: Synchronized Multimedia Integration Language).</span></span> <span data-ttu-id="c6748-327">這個檔案會指出 tooAzure Media Services 哪些 MP4 檔案可供動態封裝和其中一個這些 tooconsider hello 音訊串流。</span><span class="sxs-lookup"><span data-stu-id="c6748-327">This file indicates tooAzure Media Services what MP4 files are available for dynamic packaging and which of those tooconsider for hello audio streaming.</span></span> <span data-ttu-id="c6748-328">具有單一的音訊串流之一組 MP4 的一般資訊清單檔看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="c6748-328">A typical manifest file for a set of MP4's with a single audio stream looks like this:</span></span>

    <?xml version="1.0" encoding="utf-8" standalone="yes"?>
    <smil xmlns="http://www.w3.org/2001/SMIL20/Language">
      <head>
        <meta name="formats" content="mp4" />
      </head>
      <body>
        <switch>
          <video src="H264_1900kbps_AAC_und_ch2_96kbps.mp4" />
          <video src="H264_1300kbps_AAC_und_ch2_96kbps.mp4" />
          <video src="H264_900kbps_AAC_und_ch2_96kbps.mp4" />
          <audio src="AAC_ch2_96kbps.mp4" title="AAC_und_ch2_96kbps" />
        </switch>
      </body>
    </smil>

<span data-ttu-id="c6748-329">hello.ism 檔案包含在 switch 陳述式，hello 個別 MP4 視訊檔案的參考 tooeach 和另外 toothose 另一個 （或以上） 音訊檔案參考 tooan 只包含 hello 音訊 MP4。</span><span class="sxs-lookup"><span data-stu-id="c6748-329">hello .ism file contains within a switch statement, a reference tooeach of hello individual MP4 video files and in addition toothose also one (or more) audio file references tooan MP4 that only contains hello audio.</span></span>

<span data-ttu-id="c6748-330">產生 hello 我們組 MP4 的資訊清單檔案可以透過稱為 hello"AMS 資訊清單的寫入器 」 元件。</span><span class="sxs-lookup"><span data-stu-id="c6748-330">Generating hello manifest file for our set of MP4's can be done through a component called hello "AMS Manifest Writer".</span></span> <span data-ttu-id="c6748-331">toouse，拖曳至 hello 介面並從三個檔案輸出元件 toohello hello AMS 資訊清單寫入器輸入連接 hello 「 寫入完成 」 的輸出連接。</span><span class="sxs-lookup"><span data-stu-id="c6748-331">toouse it, drag it onto hello surface and connect hello "Write Complete" output pins from hello three File Output components toohello AMS Manifest Writer input.</span></span> <span data-ttu-id="c6748-332">請確定 tooconnect hello 輸出 hello AMS 資訊清單的寫入器 toohello 輸出檔案資產。</span><span class="sxs-lookup"><span data-stu-id="c6748-332">Then make sure tooconnect hello output of hello AMS Manifest Writer toohello Output File/Asset.</span></span>

<span data-ttu-id="c6748-333">如同我們檔案輸出元件，設定 hello.ism 檔案輸出名稱的運算式：</span><span class="sxs-lookup"><span data-stu-id="c6748-333">As with our other file output components, configure hello .ism file output name with an expression:</span></span>

    ${ROOT_outputWriteDirectory}\\${ROOT_sourceFileBaseName}_manifest.ism

<span data-ttu-id="c6748-334">我們已完成的工作流程看起來像下列的 hello:</span><span class="sxs-lookup"><span data-stu-id="c6748-334">Our finished workflow looks like hello below:</span></span>

![完成的 MXF toomultibitrate MP4 工作流程](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-finished-mxf-to-multibitrate-mp4-workflow.png)

<span data-ttu-id="c6748-336">*完成的 MXF toomultibitrate MP4 工作流程*</span><span class="sxs-lookup"><span data-stu-id="c6748-336">*Finished MXF toomultibitrate MP4 workflow*</span></span>

## <span data-ttu-id="c6748-337"><a id="MXF_to__multibitrate_MP4"></a>將 MXF 編碼為多位元速率 MP4 - 增強的藍圖</span><span class="sxs-lookup"><span data-stu-id="c6748-337"><a id="MXF_to__multibitrate_MP4"></a>Encoding MXF into multibitrate MP4 - enhanced blueprint</span></span>
<span data-ttu-id="c6748-338">在 hello[前一個工作流程的逐步解說](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging)我們已看到如何單一 MXF 輸入的資產可以轉換成輸出資產多位元速率 MP4 檔案、 僅限音訊 MP4 檔案與 Azure 媒體搭配使用的資訊清單檔案服務動態封裝。</span><span class="sxs-lookup"><span data-stu-id="c6748-338">In hello [previous workflow walkthrough](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging) we've seen how a single MXF input asset can be converted into an output asset with multi-bitrate MP4 files, an audio-only MP4 file and a manifest file for use in conjunction with Azure Media Services dynamic packaging.</span></span>

<span data-ttu-id="c6748-339">這個逐步解說將示範如何某些 hello 方面可以來增強和進行更方便。</span><span class="sxs-lookup"><span data-stu-id="c6748-339">This walkthrough will show how some of hello aspects can be enhanced and made more convenient.</span></span>

### <span data-ttu-id="c6748-340"><a id="MXF_to_multibitrate_MP4_overview"></a>工作流程概觀 tooenhance</span><span class="sxs-lookup"><span data-stu-id="c6748-340"><a id="MXF_to_multibitrate_MP4_overview"></a>Workflow overview tooenhance</span></span>
![多位元速率 MP4 工作流程 tooenhance](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-multibitrate-mp4-workflow-to-enhance.png)

<span data-ttu-id="c6748-342">*多位元速率 MP4 工作流程 tooenhance*</span><span class="sxs-lookup"><span data-stu-id="c6748-342">*Multibitrate MP4 workflow tooenhance*</span></span>

### <span data-ttu-id="c6748-343"><a id="MXF_to__multibitrate_MP4_file_naming"></a>檔案命名慣例</span><span class="sxs-lookup"><span data-stu-id="c6748-343"><a id="MXF_to__multibitrate_MP4_file_naming"></a>File Naming Conventions</span></span>
<span data-ttu-id="c6748-344">我們已 hello 前一個工作流程中指定的簡單運算式做為產生輸出檔名的 hello 基礎。</span><span class="sxs-lookup"><span data-stu-id="c6748-344">In hello previous workflow we specified a simple expression as hello basis for generating output file names.</span></span> <span data-ttu-id="c6748-345">雖然我們有一些重複： hello hello 個別輸出檔案元件的所有指定的這類運算式。</span><span class="sxs-lookup"><span data-stu-id="c6748-345">We have some duplication though: all of hello hello individual output file components specified such expression.</span></span>

<span data-ttu-id="c6748-346">例如，我們 hello 的第一個視訊檔的檔案輸出元件必須設定此運算式：</span><span class="sxs-lookup"><span data-stu-id="c6748-346">For example, our file output component for hello first video file is configured with this expression:</span></span>

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_640x360_1.MP4

<span data-ttu-id="c6748-347">針對 hello 第二個輸出視訊，我們有如下的運算式：</span><span class="sxs-lookup"><span data-stu-id="c6748-347">While for hello second output video, we have an expression like:</span></span>

    ${ROOT_outputWriteDirectory}\\${ROOT_sourceFileBaseName}_960x540_2.MP4

<span data-ttu-id="c6748-348">如果我們可以移除某些重複項目，並改為使得項目更可以設定，是不是比較清楚、較不容易出錯、更方便？</span><span class="sxs-lookup"><span data-stu-id="c6748-348">Wouldn't it be cleaner, less error prone and more convenient if we could remove some of this duplication and make things more configurable instead?</span></span> <span data-ttu-id="c6748-349">幸好我們可以： hello 設計工具的運算式功能結合在我們的工作流程根目錄上的 hello 能力 toocreate 自訂屬性會提供多一層的便利性。</span><span class="sxs-lookup"><span data-stu-id="c6748-349">Luckily we can: hello designer's expression capabilities in combination with hello ability toocreate custom properties on our workflow root will give us an added layer of convenience.</span></span>

<span data-ttu-id="c6748-350">例如，假設我們將從 hello 種位元 hello 個別 MP4 檔案的磁碟機組態檔名。</span><span class="sxs-lookup"><span data-stu-id="c6748-350">Let's assume we'll drive filename configuration from hello bitrates of hello individual MP4 files.</span></span> <span data-ttu-id="c6748-351">我們將會是用在一個中央 tooconfigure 這些位元置於 （hello 根我們圖形的），從他們必須在存取的 tooconfigure 和磁碟機的檔案名稱產生。</span><span class="sxs-lookup"><span data-stu-id="c6748-351">These bitrates we'll aim tooconfigure in one central place (on hello root of our graph), from where they'll be accessed tooconfigure and drive file name generation.</span></span> <span data-ttu-id="c6748-352">toodo，我們一開始所發行的工作流程中，這兩個 AVC 編碼器 toohello 根 hello 位元速率屬性，使其成為可從兩個 hello 根以及從 hello AVC 編碼器存取。</span><span class="sxs-lookup"><span data-stu-id="c6748-352">toodo this, we start by publishing hello bitrate property from both AVC encoders toohello root of our workflow, so that it becomes accessible from both hello root as well as from hello AVC encoders.</span></span> <span data-ttu-id="c6748-353">(即使顯示在兩個不同的位置，只有單一的基礎值。)</span><span class="sxs-lookup"><span data-stu-id="c6748-353">(Even if displayed in two different spots, there's only one underlying value.)</span></span>

### <span data-ttu-id="c6748-354"><a id="MXF_to__multibitrate_MP4_publishing"></a>發行到 hello 工作流程的根元件內容</span><span class="sxs-lookup"><span data-stu-id="c6748-354"><a id="MXF_to__multibitrate_MP4_publishing"></a>Publishing component properties onto hello workflow root</span></span>
<span data-ttu-id="c6748-355">開啟第一個 AVC 編碼器 hello，請 toohello 位元速率 (kbps) 屬性，從 hello 下拉式清單中選擇 發行。</span><span class="sxs-lookup"><span data-stu-id="c6748-355">Open hello first AVC encoder, go toohello Bitrate (kbps) property and from hello dropdown choose Publish.</span></span>

![發行 hello 位元速率屬性](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-publishing-bitrate-property.png)

<span data-ttu-id="c6748-357">*發行 hello 位元速率屬性*</span><span class="sxs-lookup"><span data-stu-id="c6748-357">*Publishing hello bitrate property*</span></span>

<span data-ttu-id="c6748-358">設定 hello 發行對話方塊 toopublish toohello 根目錄中，我們的工作流程歷程圖中，以"video1bitrate 「 發佈的名稱 」 和 「 可讀取的顯示名稱 「 視訊 1 位元速率 」。</span><span class="sxs-lookup"><span data-stu-id="c6748-358">Configure hello publish dialog toopublish toohello root of our workflow graph, with a published name of "video1bitrate" and a readable display name of "Video 1 Bitrate".</span></span> <span data-ttu-id="c6748-359">設定名為「串流處理位元速率」的自訂群組名稱，並按 [發佈]。</span><span class="sxs-lookup"><span data-stu-id="c6748-359">Configure a custom group name called "Streaming Bitrates" and hit Publish.</span></span>

![發行 hello 位元速率屬性](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-publishing-dialog-for-bitrate-property.png)

<span data-ttu-id="c6748-361">*位元速率屬性的發佈對話方塊*</span><span class="sxs-lookup"><span data-stu-id="c6748-361">*Publishing dialog for bitrate property*</span></span>

<span data-ttu-id="c6748-362">重複的 hello、 相同的 hello hello 位元速率屬性 AVC 編碼器的第二個並將其命名"video2bitrate 」 顯示名稱 「 視訊 2 位元速率"hello 進行相同的自訂群組 」 串流處理位元"。</span><span class="sxs-lookup"><span data-stu-id="c6748-362">Repeat hello same for hello bitrate property of hello second AVC encoder and name it "video2bitrate" with a display name of "Video 2 Bitrate", in hello same custom group "Streaming Bitrates".</span></span>

<span data-ttu-id="c6748-363">現在，我們會檢查 hello 工作流程的根內容，我們將會看到兩個已發行的屬性顯示的 hello 我們自訂群組。</span><span class="sxs-lookup"><span data-stu-id="c6748-363">If we now inspect hello workflow root properties, we'll see our custom group with hello two published properties show up.</span></span> <span data-ttu-id="c6748-364">同時會反映其各自 AVC 編碼器位元速率 hello 值。</span><span class="sxs-lookup"><span data-stu-id="c6748-364">Both are reflecting hello value of their respective AVC encoder bitrate.</span></span>

![工作流程根目錄上發佈的位元速率屬性](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-published-bitrate-props-on-workflow-root.png)

<span data-ttu-id="c6748-366">每當我們想要 tooaccess 從程式碼或運算式，這些屬性，我們可以這樣做就像這樣：</span><span class="sxs-lookup"><span data-stu-id="c6748-366">Whenever we want tooaccess these properties from code or from an expression, we can do so like this:</span></span>

* <span data-ttu-id="c6748-367">從內嵌程式碼，從正下方 hello 根元件： node.getPropertyAsString('../ video1bitrate'，便是 null)</span><span class="sxs-lookup"><span data-stu-id="c6748-367">from inline code from a component right below hello root: node.getPropertyAsString('../video1bitrate',null)</span></span>
* <span data-ttu-id="c6748-368">在運算式內：${ROOT_video1bitrate}</span><span class="sxs-lookup"><span data-stu-id="c6748-368">within an expression: ${ROOT_video1bitrate}</span></span>

<span data-ttu-id="c6748-369">讓我們藉由發行我們音訊播放軌位元速率上的也完成 hello 」 串流處理位元 」 群組。</span><span class="sxs-lookup"><span data-stu-id="c6748-369">Let's complete hello "Streaming Bitrates" group by publishing our audio track bitrate on it as well.</span></span> <span data-ttu-id="c6748-370">在 hello 屬性中的 hello AAC 編碼器，搜尋 hello 位元速率設定並選取發行從 hello 下拉式清單中下一個 tooit。</span><span class="sxs-lookup"><span data-stu-id="c6748-370">Within hello properties of hello AAC Encoder, search for hello Bitrate setting and select Publish from hello dropdown next tooit.</span></span> <span data-ttu-id="c6748-371">發行具有名稱"audio1bitrate"hello 圖形的 toohello 根和顯示名稱"音訊 1 位元速率 「 我們的自訂群組 」 串流處理位元 」 內。</span><span class="sxs-lookup"><span data-stu-id="c6748-371">Publish toohello root of hello graph with name "audio1bitrate" and display name "Audio 1 Bitrate" within our custom group "Streaming Bitrates".</span></span>

![音訊位元速率的發佈對話方塊](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-publishing-dialog-for-audio-bitrate.png)

<span data-ttu-id="c6748-373">*音訊位元速率的發佈對話方塊*</span><span class="sxs-lookup"><span data-stu-id="c6748-373">*Publishing dialog for audio bitrate*</span></span>

![在根目錄產生視訊和音訊屬性](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-resulting-video-and-audio-props-on-root.png)

<span data-ttu-id="c6748-375">*在根目錄產生視訊和音訊屬性*</span><span class="sxs-lookup"><span data-stu-id="c6748-375">*Resulting video and audio props on root*</span></span>

<span data-ttu-id="c6748-376">請注意，變更任何這些三個值也會重新設定，變更 hello hello 個別的元件，它們會與連結上的值 （以及從發行）。</span><span class="sxs-lookup"><span data-stu-id="c6748-376">Note that changing any of those three values also re-configures and changes hello values on hello respective components they are linked with (and where published from).</span></span>

### <span data-ttu-id="c6748-377"><a id="MXF_to__multibitrate_MP4_output_files"></a>讓產生的輸出檔案名稱依賴發佈的屬性值</span><span class="sxs-lookup"><span data-stu-id="c6748-377"><a id="MXF_to__multibitrate_MP4_output_files"></a>Have generated output file names rely on published property values</span></span>
<span data-ttu-id="c6748-378">而不是硬式編碼我們產生的檔案名稱，我們現在可以變更每個 hello 檔案輸出元件 toorely hello 位元速率屬性我們 hello 圖形根上發行我們檔案名稱的運算式。</span><span class="sxs-lookup"><span data-stu-id="c6748-378">Instead of hardcoding our generated file names, we can now change our filename expression on each of hello File Output components toorely on hello bitrate properties we just published on hello graph root.</span></span> <span data-ttu-id="c6748-379">開始使用我們第一個輸出檔，尋找 hello 檔案屬性，然後編輯 hello 運算式如下：</span><span class="sxs-lookup"><span data-stu-id="c6748-379">Starting with our first file output, find hello File property and edit hello expression like this:</span></span>

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_${ROOT_video1bitrate}kbps.MP4

<span data-ttu-id="c6748-380">此運算式中的 hello 不同參數可以存取和輸入驉 hello hello 運算式視窗中的 hello 鍵盤上的貨幣符號。</span><span class="sxs-lookup"><span data-stu-id="c6748-380">hello different parameters in this expression can be accessed and entered by hitting hello dollar sign on hello keyboard while in hello expression window.</span></span> <span data-ttu-id="c6748-381">我們稍早已發佈我們 video1bitrate 屬性其中一個 hello 可用的參數。</span><span class="sxs-lookup"><span data-stu-id="c6748-381">One of hello available parameters is our video1bitrate property which we published earlier.</span></span>

![存取運算式內的參數](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-accessing-parameters-within-an-expression.png)

<span data-ttu-id="c6748-383">*存取運算式內的參數*</span><span class="sxs-lookup"><span data-stu-id="c6748-383">*Accessing parameters within an expression*</span></span>

<span data-ttu-id="c6748-384">請勿 hello 我們的第二個視訊的 hello 檔案輸出相同的：</span><span class="sxs-lookup"><span data-stu-id="c6748-384">Do hello same for hello file output for our second video:</span></span>

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_${ROOT_video2bitrate}kbps.MP4

<span data-ttu-id="c6748-385">和 hello 純音訊檔案輸出：</span><span class="sxs-lookup"><span data-stu-id="c6748-385">and for hello audio-only file output:</span></span>

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_${ROOT_audio1bitrate}bps_audio.MP4

<span data-ttu-id="c6748-386">如果我們現在會變更任何 hello 視訊或音訊檔案的位元速率 hello，hello 個別編碼器將重新設定，而且 hello 位元速率為基礎的檔案名稱慣例將適用於所有自動。</span><span class="sxs-lookup"><span data-stu-id="c6748-386">If we now change hello bitrate for any of hello video or audio files, hello respective encoder will be reconfigured and hello bitrate-based file name convention will be honored all automatic.</span></span>

## <span data-ttu-id="c6748-387"><a id="thumbnails_to__multibitrate_MP4"></a>加入縮圖 toomultibitrate MP4 輸出</span><span class="sxs-lookup"><span data-stu-id="c6748-387"><a id="thumbnails_to__multibitrate_MP4"></a>Adding thumbnails toomultibitrate MP4 output</span></span>
<span data-ttu-id="c6748-388">從產生的工作流程開始[輸入 MXF 的多位元速率 MP4 輸出](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging)，我們現在將會尋找到新增縮圖 toohello 輸出。</span><span class="sxs-lookup"><span data-stu-id="c6748-388">Starting from a workflow that generates [a multibitrate MP4 output from an MXF input](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging), we will now be looking into adding thumbnails toohello output.</span></span>

### <span data-ttu-id="c6748-389"><a id="thumbnails_to__multibitrate_MP4_overview"></a>工作流程概觀 tooadd 的縮圖</span><span class="sxs-lookup"><span data-stu-id="c6748-389"><a id="thumbnails_to__multibitrate_MP4_overview"></a>Workflow overview tooadd thumbnails to</span></span>
![從多位元速率 MP4 工作流程 toostart](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-multibitrate-mp4-workflow-to-start-from.png)

<span data-ttu-id="c6748-391">*從多位元速率 MP4 工作流程 toostart*</span><span class="sxs-lookup"><span data-stu-id="c6748-391">*Multibitrate MP4 workflow toostart from*</span></span>

### <span data-ttu-id="c6748-392"><a id="thumbnails_to__multibitrate_MP4__with_jpg"></a>加入 JPG 編碼</span><span class="sxs-lookup"><span data-stu-id="c6748-392"><a id="thumbnails_to__multibitrate_MP4__with_jpg"></a>Adding JPG Encoding</span></span>
<span data-ttu-id="c6748-393">我們的縮圖產生 hello 核心會 hello JPG 編碼器元件可以 toooutput JPG 檔案。</span><span class="sxs-lookup"><span data-stu-id="c6748-393">hello heart of our thumbnail generation will be hello JPG Encoder component, able toooutput JPG files.</span></span>

![JPG 編碼器](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-jpg-encoder.png)

<span data-ttu-id="c6748-395">*JPG 編碼器*</span><span class="sxs-lookup"><span data-stu-id="c6748-395">*JPG Encoder*</span></span>

<span data-ttu-id="c6748-396">我們無法不過從直接連接我們的未壓縮視訊資料流到 hello JPG 編碼器的媒體檔案輸入 hello。</span><span class="sxs-lookup"><span data-stu-id="c6748-396">We cannot however directly connect our Uncompressed Video stream from hello Media File Input into hello JPG encoder.</span></span> <span data-ttu-id="c6748-397">相反地，它會預期 toobe 傳個別畫面格。</span><span class="sxs-lookup"><span data-stu-id="c6748-397">Instead, it expects toobe handed individual frames.</span></span> <span data-ttu-id="c6748-398">這樣，我們可以透過 hello 視訊畫面格閘道元件進行。</span><span class="sxs-lookup"><span data-stu-id="c6748-398">This, we can do through hello Video Frame Gate component.</span></span>

![連接框架閘道 toohello JPG 編碼器](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-connect-frame-gate-to-jpg-encoder.png)

<span data-ttu-id="c6748-400">*連接框架閘道 toohello JPG 編碼器*</span><span class="sxs-lookup"><span data-stu-id="c6748-400">*Connecting a frame gate toohello JPG encoder*</span></span>

<span data-ttu-id="c6748-401">hello 框架閘道之後每個這麼多的秒數或框架可讓視訊畫面格 toopass。</span><span class="sxs-lookup"><span data-stu-id="c6748-401">hello frame gate once every so many seconds or frames allows a video frame toopass.</span></span> <span data-ttu-id="c6748-402">hello 間隔和 hello 時間位移與其中發生這種情況是 hello 屬性中設定的。</span><span class="sxs-lookup"><span data-stu-id="c6748-402">hello interval and hello time offset with which this happens is configurable in hello properties.</span></span>

![視訊畫面格閘道屬性](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-video-frame-gate-properties.png)

<span data-ttu-id="c6748-404">*視訊畫面格閘道屬性*</span><span class="sxs-lookup"><span data-stu-id="c6748-404">*Video Frame Gate properties*</span></span>

<span data-ttu-id="c6748-405">讓我們藉由設定 hello 模式 tooTime （秒） 每隔一分鐘建立縮圖和 hello 間隔 too60。</span><span class="sxs-lookup"><span data-stu-id="c6748-405">Let's create a thumbnail every minute by setting hello mode tooTime (seconds) and hello Interval too60.</span></span>

### <span data-ttu-id="c6748-406"><a id="thumbnails_to__multibitrate_MP4_color_space"></a>處理色彩空間轉換</span><span class="sxs-lookup"><span data-stu-id="c6748-406"><a id="thumbnails_to__multibitrate_MP4_color_space"></a>Dealing with Color Space conversion</span></span>
<span data-ttu-id="c6748-407">雖然相提並論，似乎邏輯這兩種未壓縮視訊的 hello 框架閘道與媒體檔案輸入 hello 的 pin 現在已連線，如果我們會這樣做，我們會收到警告。</span><span class="sxs-lookup"><span data-stu-id="c6748-407">While it would seem logical both Uncompressed Video pins of hello frame gate and hello Media File Input can now be connected, we would get a warning if we would do so.</span></span>

![輸入色彩空間錯誤](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-input-color-space-error.png)

<span data-ttu-id="c6748-409">*輸入色彩空間錯誤*</span><span class="sxs-lookup"><span data-stu-id="c6748-409">*Input color space error*</span></span>

<span data-ttu-id="c6748-410">這是因為 hello 的色彩中資訊的表示的方式我們原始原始未壓縮視訊資料流中，來自我們 MXF，哪些 hello JPG 編碼器所預期不同。</span><span class="sxs-lookup"><span data-stu-id="c6748-410">This is because hello way in which colour information is represented in our original raw uncompressed video stream, coming from our MXF, is different from what hello JPG Encoder is expecting.</span></span> <span data-ttu-id="c6748-411">更具體來說，所謂"色彩空間 」 的 「 RGB"或"灰階 」 是預期 tooflow 中的。</span><span class="sxs-lookup"><span data-stu-id="c6748-411">More specifically, a so-called "color space" of "RGB" or "Grayscale" is expected tooflow in.</span></span> <span data-ttu-id="c6748-412">這表示該 hello 視訊畫面格閘道的輸入視訊串流需要 toohave 先套用有關其色彩空間轉換。</span><span class="sxs-lookup"><span data-stu-id="c6748-412">This means that hello Video Frame Gate's inbound video stream will need toohave a conversion applied regarding its color space first.</span></span>

<span data-ttu-id="c6748-413">拖曳到 hello 工作流程 hello 色彩空間轉換程式 Intel，並將它連接 tooour 框架閘道。</span><span class="sxs-lookup"><span data-stu-id="c6748-413">Drag onto hello workflow hello Color Space Converter - Intel and connect it tooour frame gate.</span></span>

![連接色彩空間轉換器](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-connect-color-space-convertor.png)

<span data-ttu-id="c6748-415">*連接色彩空間轉換器*</span><span class="sxs-lookup"><span data-stu-id="c6748-415">*Connecting a Color Space Convertor*</span></span>

<span data-ttu-id="c6748-416">在 hello 屬性 視窗中，選擇 hello BGR 24 hello 預設清單項目。</span><span class="sxs-lookup"><span data-stu-id="c6748-416">In hello properties window, pick hello BGR 24 entry from hello Preset list.</span></span>

### <span data-ttu-id="c6748-417"><a id="thumbnails_to__multibitrate_MP4_writing_thumbnails"></a>寫入 hello 縮圖</span><span class="sxs-lookup"><span data-stu-id="c6748-417"><a id="thumbnails_to__multibitrate_MP4_writing_thumbnails"></a>Writing hello thumbnails</span></span>
<span data-ttu-id="c6748-418">不同於我們的 MP4 視訊，hello JPG 編碼器元件會輸出多個檔案。</span><span class="sxs-lookup"><span data-stu-id="c6748-418">Different from our MP4 video's, hello JPG Encoder component will output more than one file.</span></span> <span data-ttu-id="c6748-419">在與這個順序 toodeal，場景搜尋 JPG 檔案寫入器元件都可以使用： 它會採用 hello 傳入 JPG 縮圖，並將它們，寫入正在不同的數字並後置有每個檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="c6748-419">In order toodeal with this, a Scene Search JPG File Writer component can be used: it will take hello incoming JPG thumbnails and write them out, each filename being suffixed by a different number.</span></span> <span data-ttu-id="c6748-420">（從已繪製 hello 數字，通常表示的秒數/單位 hello 縮圖 hello 資料流中的 hello 數字）。</span><span class="sxs-lookup"><span data-stu-id="c6748-420">(hello number typically indicating hello number of seconds/units in hello stream which hello thumbnail was drawn from.)</span></span>

![介紹 hello 場景搜尋 JPG 檔案寫入器](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-scene-search-jpg-file-writer.png)

<span data-ttu-id="c6748-422">*介紹 hello 場景搜尋 JPG 檔案寫入器*</span><span class="sxs-lookup"><span data-stu-id="c6748-422">*Introducing hello Scene Search JPG File Writer*</span></span>

<span data-ttu-id="c6748-423">使用 hello 運算式設定 hello 輸出資料夾的路徑屬性: ${ROOT_outputWriteDirectory}</span><span class="sxs-lookup"><span data-stu-id="c6748-423">Configure hello Output Folder Path property with hello expression: ${ROOT_outputWriteDirectory}</span></span>

<span data-ttu-id="c6748-424">和 hello 與檔案名稱前置詞屬性：</span><span class="sxs-lookup"><span data-stu-id="c6748-424">and hello Filename Prefix property with:</span></span>

    ${ROOT_sourceFileBaseName}_thumb_

<span data-ttu-id="c6748-425">hello 前置詞會決定要如何命名 hello 縮圖的檔案。</span><span class="sxs-lookup"><span data-stu-id="c6748-425">hello prefix will determine how hello thumbnail files are being named.</span></span> <span data-ttu-id="c6748-426">它們會加 hello 資料流中的一個數字表示 hello 捲動方塊的位置。</span><span class="sxs-lookup"><span data-stu-id="c6748-426">They will be suffixed with a number indicating hello thumb's position in hello stream.</span></span>

![場景搜尋 JPG 檔案寫入器屬性](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-scene-search-jpg-file-writer-properties.png)

<span data-ttu-id="c6748-428">*場景搜尋 JPG 檔案寫入器屬性*</span><span class="sxs-lookup"><span data-stu-id="c6748-428">*Scene Search JPG File Writer properties*</span></span>

<span data-ttu-id="c6748-429">Hello 場景搜尋 JPG 檔案寫入器 toohello 輸出檔案資產節點連接。</span><span class="sxs-lookup"><span data-stu-id="c6748-429">Connect hello Scene Search JPG File Writer toohello Output File/Asset node.</span></span>

### <span data-ttu-id="c6748-430"><a id="thumbnails_to__multibitrate_MP4_errors"></a>偵測工作流程中的錯誤</span><span class="sxs-lookup"><span data-stu-id="c6748-430"><a id="thumbnails_to__multibitrate_MP4_errors"></a>Detecting errors in a workflow</span></span>
<span data-ttu-id="c6748-431">連接 hello 色彩空間轉換 toohello 原始未壓縮視訊輸出的 hello 的輸入。</span><span class="sxs-lookup"><span data-stu-id="c6748-431">Connect hello input of hello color space converter toohello raw uncompressed video output.</span></span> <span data-ttu-id="c6748-432">現在，執行本機測試回合 hello 工作流程。</span><span class="sxs-lookup"><span data-stu-id="c6748-432">Now perform a local test run for hello workflow.</span></span> <span data-ttu-id="c6748-433">沒有機會 hello 工作流程會突然停止執行，而且發生錯誤的 hello 元件上的紅色外框表示：</span><span class="sxs-lookup"><span data-stu-id="c6748-433">There's a good chance hello workflow will suddenly stop executing and indicate with a red outline on hello component that encountered an error:</span></span>

![色彩空間轉換器錯誤](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-color-space-converter-error.png)

<span data-ttu-id="c6748-435">*色彩空間轉換器錯誤*</span><span class="sxs-lookup"><span data-stu-id="c6748-435">*Color Space Converter error*</span></span>

<span data-ttu-id="c6748-436">按一下 hello hello 編碼嘗試失敗的原因是什麼 hello 右上角的 hello 色彩空間轉換元件 toosee"E"hello 稍有紅色圖示。</span><span class="sxs-lookup"><span data-stu-id="c6748-436">Click hello little red "E" icon in hello top right corner of hello Color Space Converter component toosee what's hello reason hello encoding attempt failed.</span></span>

![色彩空間轉換器錯誤對話方塊](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-color-space-converter-error-dialog.png)

<span data-ttu-id="c6748-438">*色彩空間轉換器錯誤對話方塊*</span><span class="sxs-lookup"><span data-stu-id="c6748-438">*Color Space Converter error dialog*</span></span>

<span data-ttu-id="c6748-439">事實上，您可以看到，hello 傳入色彩空間標準 hello 色彩空間轉換具有 toobe rec601 YUV tooRGB 我們要求轉換。</span><span class="sxs-lookup"><span data-stu-id="c6748-439">It turns out, as you can see, that hello incoming color space standard for hello color space converter has toobe rec601 for our requested conversion of YUV tooRGB.</span></span> <span data-ttu-id="c6748-440">顯然我們的串流並未指出它是 rec601。</span><span class="sxs-lookup"><span data-stu-id="c6748-440">Apparently our stream doesn't indicate it's rec601.</span></span> <span data-ttu-id="c6748-441">(Rec 601 是以數位視訊格式編碼交錯式類比視訊訊號的標準。</span><span class="sxs-lookup"><span data-stu-id="c6748-441">(Rec 601 is a standard for encoding interlaced analog video signals in digital video form.</span></span> <span data-ttu-id="c6748-442">它會指定涵蓋 720 亮度取樣和每一行 360 色度取樣的作用中區域。</span><span class="sxs-lookup"><span data-stu-id="c6748-442">It specifies an active region covering 720 luminance samples and 360 chrominance samples per line.</span></span> <span data-ttu-id="c6748-443">hello 色彩編碼系統稱為 YCbCr 4:2:2。)</span><span class="sxs-lookup"><span data-stu-id="c6748-443">hello color encoding system is known as YCbCr 4:2:2.)</span></span>

<span data-ttu-id="c6748-444">toofix，我們將會指出我們我們處理 rec601 內容的資料流的 hello 中繼資料。</span><span class="sxs-lookup"><span data-stu-id="c6748-444">toofix this, we'll indicate on hello metadata of our stream that we're dealing with rec601 content.</span></span> <span data-ttu-id="c6748-445">讓我們將使用視訊資料型別 Updater 元件，請說我們原始來源與 hello 色彩空間轉換元件之間 toodo。</span><span class="sxs-lookup"><span data-stu-id="c6748-445">toodo so we'll use a Video Data Type Updater component, which we'll put in between our raw source and hello color space conversion component.</span></span> <span data-ttu-id="c6748-446">此資料型別 updater 允許 hello 手動更新特定視訊資料的類型屬性。</span><span class="sxs-lookup"><span data-stu-id="c6748-446">This data type updater allows for hello manual update of certain video data type properties.</span></span> <span data-ttu-id="c6748-447">設定 tooindicate 色彩空間標準的 「 Rec 601"。</span><span class="sxs-lookup"><span data-stu-id="c6748-447">Configure it tooindicate a Color Space Standard of "Rec 601".</span></span> <span data-ttu-id="c6748-448">如果尚未定義任何色彩空間，這會導致 hello 視訊資料型別 Updater tootag hello 資料流與 hello"Rec 601"色彩空間。</span><span class="sxs-lookup"><span data-stu-id="c6748-448">This will cause hello Video Data Type Updater tootag hello stream with hello "Rec 601" color space if there was no color space defined yet.</span></span> <span data-ttu-id="c6748-449">（它不會覆寫任何現有的中繼資料，除非 hello 覆寫核取方塊已核取。）</span><span class="sxs-lookup"><span data-stu-id="c6748-449">(It will not override any existing metadata, unless hello Override checkbox was checked.)</span></span>

![更新資料型別 Updater hello 色彩空間標準](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-update-color-space-standard-on-data-type.png)

<span data-ttu-id="c6748-451">*更新資料型別 Updater hello 色彩空間標準*</span><span class="sxs-lookup"><span data-stu-id="c6748-451">*Updating Color Space Standard on hello Data Type Updater*</span></span>

### <span data-ttu-id="c6748-452"><a id="thumbnails_to__multibitrate_MP4_finish"></a>工作流程完成</span><span class="sxs-lookup"><span data-stu-id="c6748-452"><a id="thumbnails_to__multibitrate_MP4_finish"></a>Finished Workflow</span></span>
<span data-ttu-id="c6748-453">既然我們我們的工作流程已結束，請執行通過的測試回合的 toosee 另一個。</span><span class="sxs-lookup"><span data-stu-id="c6748-453">Now that our our workflow is finished, do another test run toosee it pass.</span></span>

![具有縮圖的多個 mp4 輸出完成的工作流程](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-finished-workflow-for-multi-mp4-thumbnails.png)

<span data-ttu-id="c6748-455">*具有縮圖的多個 mp4 輸出完成的工作流程*</span><span class="sxs-lookup"><span data-stu-id="c6748-455">*Finished workflow for multi-mp4 output with thumbnails*</span></span>

## <span data-ttu-id="c6748-456"><a id="time_based_trim"></a>多位元速率 MP4 輸出以時間為基礎的修剪</span><span class="sxs-lookup"><span data-stu-id="c6748-456"><a id="time_based_trim"></a>Time-based trimming of multibitrate MP4 output</span></span>
<span data-ttu-id="c6748-457">從產生的工作流程開始[輸入 MXF 的多位元速率 MP4 輸出](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging)，我們現在將會尋找到修剪 hello 來源視訊根據時間戳記。</span><span class="sxs-lookup"><span data-stu-id="c6748-457">Starting from a workflow that generates [a multibitrate MP4 output from an MXF input](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging), we will now be looking into trimming hello source video based on time-stamps.</span></span>

### <span data-ttu-id="c6748-458"><a id="time_based_trim_start"></a>加入要修剪的工作流程概觀 toostart</span><span class="sxs-lookup"><span data-stu-id="c6748-458"><a id="time_based_trim_start"></a>Workflow overview toostart adding trimming to</span></span>
![若要開始的工作流程 tooadd 修剪](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-starting-workflow-to-add-trimming.png)

<span data-ttu-id="c6748-460">*若要開始的工作流程 tooadd 修剪*</span><span class="sxs-lookup"><span data-stu-id="c6748-460">*Starting workflow tooadd trimming to*</span></span>

### <span data-ttu-id="c6748-461"><a id="time_based_trim_use_stream_trimmer"></a>使用資料流修剪器 hello</span><span class="sxs-lookup"><span data-stu-id="c6748-461"><a id="time_based_trim_use_stream_trimmer"></a>Using hello Stream Trimmer</span></span>
<span data-ttu-id="c6748-462">hello 資料流修剪器元件可讓 tootrim hello 開頭和結尾的輸入資料流的基礎計時資訊 （秒數、 分鐘的時間，...）。hello 修剪器不支援以框架為基礎的調整。</span><span class="sxs-lookup"><span data-stu-id="c6748-462">hello Stream Trimmer component allows tootrim hello beginning and ending of an input stream base on timing information (seconds, minutes, ...). hello trimmer does not support frame-based trimming.</span></span>

![串流修剪器](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-stream-trimmer.png)

<span data-ttu-id="c6748-464">*串流修剪器*</span><span class="sxs-lookup"><span data-stu-id="c6748-464">*Stream Trimmer*</span></span>

<span data-ttu-id="c6748-465">而不是直接連結 hello AVC 編碼器和喇叭位置 assigner toohello 媒體檔案輸入，我們會將這些 hello 資料流修剪器之間。</span><span class="sxs-lookup"><span data-stu-id="c6748-465">Instead of linking hello AVC encoders and speaker position assigner toohello Media File Input directly, we'll put in between those hello stream trimmer.</span></span> <span data-ttu-id="c6748-466">（一個 hello 視訊訊號，一個用於 hello 交錯音訊訊號）。</span><span class="sxs-lookup"><span data-stu-id="c6748-466">(One for hello video signal and one for hello interleaved audio signal.)</span></span>

![在內部放入串流修剪器](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-put-stream-trimmer-in-between.png)

<span data-ttu-id="c6748-468">*在內部放入串流修剪器*</span><span class="sxs-lookup"><span data-stu-id="c6748-468">*Put Stream Trimmer in between*</span></span>

<span data-ttu-id="c6748-469">讓我們設定 hello 修剪器，讓我們只會處理視訊和音訊 15 秒到 hello 視訊在 60 秒之間。</span><span class="sxs-lookup"><span data-stu-id="c6748-469">Let's configure hello trimmer so that we will only process video and audio between 15 seconds and 60 seconds in hello video.</span></span>

<span data-ttu-id="c6748-470">請 toohello hello 視訊資料流修剪器屬性，並設定開始時間 (15) 和結束時間 （60 秒） 的內容。</span><span class="sxs-lookup"><span data-stu-id="c6748-470">Go toohello properties of hello Video Stream Trimmer and configure both Start Time (15s) and End Time (60s) properties.</span></span> <span data-ttu-id="c6748-471">確定同時我們音訊和視訊修剪器一定是相同的開始和結束值設定的 toohello toomake，我們將發佈這些 toohello hello 工作流程的根。</span><span class="sxs-lookup"><span data-stu-id="c6748-471">toomake sure both our audio and video trimmer are always configured toohello same start and end values, we will publish those toohello root of hello workflow.</span></span>

![串流修剪器的發佈開始時間屬性](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-publish-start-time-from-stream-trimmer.png)

<span data-ttu-id="c6748-473">*串流修剪器的發佈開始時間屬性*</span><span class="sxs-lookup"><span data-stu-id="c6748-473">*Publish start time property from Stream Trimmer*</span></span>

![發佈屬性對話方塊的開始時間](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-publish-dialog-for-start-time.png)

<span data-ttu-id="c6748-475">*發佈屬性對話方塊的開始時間*</span><span class="sxs-lookup"><span data-stu-id="c6748-475">*Publish property dialog for start time*</span></span>

![發佈屬性對話方塊的結束時間](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-publish-dialog-for-end-time.png)

<span data-ttu-id="c6748-477">*發佈屬性對話方塊的結束時間*</span><span class="sxs-lookup"><span data-stu-id="c6748-477">*Publish property dialog for end time*</span></span>

<span data-ttu-id="c6748-478">如果我們現在會檢查 hello 根工作流程，這兩個屬性將會清楚顯示，且可設定從該處。</span><span class="sxs-lookup"><span data-stu-id="c6748-478">If we now inspect hello root of our workflow, both properties will be neatly displayed and configurable from there.</span></span>

![在根目錄可取得發佈的屬性](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-published-properties-available-on-root.png)

<span data-ttu-id="c6748-480">*在根目錄可取得發佈的屬性*</span><span class="sxs-lookup"><span data-stu-id="c6748-480">*Published properties available on root*</span></span>

<span data-ttu-id="c6748-481">現在從 hello 音訊修剪器開啟 hello 修剪屬性，並設定開始和結束時間的運算式可參考 toohello 發行的工作流程的 hello 根目錄上的屬性。</span><span class="sxs-lookup"><span data-stu-id="c6748-481">Now open hello trimming properties from hello audio trimmer and configure both start and end times with an expression that refers toohello published properties on hello root of our workflow.</span></span>

<span data-ttu-id="c6748-482">Hello 音訊修剪開始時間：</span><span class="sxs-lookup"><span data-stu-id="c6748-482">For hello audio trimming start time:</span></span>

    ${ROOT_TrimmingStartTime}

<span data-ttu-id="c6748-483">和其結束時間：</span><span class="sxs-lookup"><span data-stu-id="c6748-483">and for its end time:</span></span>

    ${ROOT_TrimmingEndTime}

### <span data-ttu-id="c6748-484"><a id="time_based_trim_finish"></a>工作流程完成</span><span class="sxs-lookup"><span data-stu-id="c6748-484"><a id="time_based_trim_finish"></a>Finished Workflow</span></span>
![工作流程完成](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-finished-workflow-time-base-trimming.png)

<span data-ttu-id="c6748-486">*工作流程完成*</span><span class="sxs-lookup"><span data-stu-id="c6748-486">*Finished Workflow*</span></span>

## <span data-ttu-id="c6748-487"><a id="scripting"></a>簡介 hello 編寫指令碼元件</span><span class="sxs-lookup"><span data-stu-id="c6748-487"><a id="scripting"></a>Introducing hello Scripted Component</span></span>
<span data-ttu-id="c6748-488">執行指令碼的元件可以 hello 的工作流程的執行階段期間執行任意指令碼。</span><span class="sxs-lookup"><span data-stu-id="c6748-488">Scripted Components can execute arbitrary scripts during hello execution phases of our workflow.</span></span> <span data-ttu-id="c6748-489">有四個不同的指令碼可以執行的每個都有特定的特性和自己 hello 工作流程生命週期中的位置：</span><span class="sxs-lookup"><span data-stu-id="c6748-489">There are four different scripts that can be executed, each with specific characteristics and their own place in hello workflow life-cycle:</span></span>

* <span data-ttu-id="c6748-490">**commandScript**</span><span class="sxs-lookup"><span data-stu-id="c6748-490">**commandScript**</span></span>
* <span data-ttu-id="c6748-491">**realizeScript**</span><span class="sxs-lookup"><span data-stu-id="c6748-491">**realizeScript**</span></span>
* <span data-ttu-id="c6748-492">**processInputScript**</span><span class="sxs-lookup"><span data-stu-id="c6748-492">**processInputScript**</span></span>
* <span data-ttu-id="c6748-493">**lifeCycleScript**</span><span class="sxs-lookup"><span data-stu-id="c6748-493">**lifeCycleScript**</span></span>

<span data-ttu-id="c6748-494">hello 文件的 hello 編寫指令碼元件會更詳細的 hello 上述每個。</span><span class="sxs-lookup"><span data-stu-id="c6748-494">hello documentation of hello Scripted Component goes in more detail for each of hello above.</span></span> <span data-ttu-id="c6748-495">在[hello 下列區段](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim)，hello **realizeScript** hello 工作流程啟動時，指令碼元件會使用的 tooconstruct hello 立即 cliplist xml。</span><span class="sxs-lookup"><span data-stu-id="c6748-495">In [hello following section](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim), hello **realizeScript** scripting component is used tooconstruct a cliplist xml on hello fly when hello workflow starts.</span></span> <span data-ttu-id="c6748-496">此指令碼會呼叫 hello 元件在安裝期間，發生一次在其生命週期中。</span><span class="sxs-lookup"><span data-stu-id="c6748-496">This script is called during hello component setup, which happens only once in it's lifecycle.</span></span>

### <span data-ttu-id="c6748-497"><a id="scripting_hello_world"></a>工作流程內的指令碼：Hello World</span><span class="sxs-lookup"><span data-stu-id="c6748-497"><a id="scripting_hello_world"></a>Scripting within a workflow: hello world</span></span>
<span data-ttu-id="c6748-498">Hello 設計工具介面上拖曳編寫指令碼元件，並重新命名它 (例如，"SetClipListXML")。</span><span class="sxs-lookup"><span data-stu-id="c6748-498">Drag a Scripted Component onto hello designer surface and rename it (for example, "SetClipListXML").</span></span>

![加入指令碼元件](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-add-scripted-comp.png)

<span data-ttu-id="c6748-500">*加入指令碼元件*</span><span class="sxs-lookup"><span data-stu-id="c6748-500">*Adding a Scripted Component*</span></span>

<span data-ttu-id="c6748-501">當您檢查 hello 屬性 hello 編寫指令碼元件，將會顯示四種不同的指令碼類型的 hello、 每個可設定 tooa 不同的指令碼。</span><span class="sxs-lookup"><span data-stu-id="c6748-501">When you inspect hello properties of hello Scripted Component, hello four different script types will be shown, each configurable tooa different script.</span></span>

![指令碼元件屬性](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-scripted-comp-properties.png)

<span data-ttu-id="c6748-503">*指令碼元件屬性*</span><span class="sxs-lookup"><span data-stu-id="c6748-503">*Scripted Component properties*</span></span>

<span data-ttu-id="c6748-504">清除 hello processInputScript 和 hello realizeScript 的 hello 編輯器開啟。</span><span class="sxs-lookup"><span data-stu-id="c6748-504">Clear hello processInputScript and open hello editor for hello realizeScript.</span></span> <span data-ttu-id="c6748-505">現在我們設定好，並準備 toostart 指令碼。</span><span class="sxs-lookup"><span data-stu-id="c6748-505">Now we're set up and ready toostart scripting.</span></span>

<span data-ttu-id="c6748-506">指令碼是以 Groovy，會保留與 Java 的相容性的 hello Java 平台動態編譯的指令碼語言撰寫。</span><span class="sxs-lookup"><span data-stu-id="c6748-506">Scripts are written in Groovy, a dynamically compiled scripting language for hello Java platform that retains compatibility with Java.</span></span> <span data-ttu-id="c6748-507">事實上，大部分的 Java 程式碼是有效的 Groovy 程式碼。</span><span class="sxs-lookup"><span data-stu-id="c6748-507">Actually, most Java code is valid Groovy code.</span></span>

<span data-ttu-id="c6748-508">讓我們我們 realizeScript hello 內容中撰寫簡單的 hello world groovy 指令碼。</span><span class="sxs-lookup"><span data-stu-id="c6748-508">Let's write a simple hello world groovy script in hello context of our realizeScript.</span></span> <span data-ttu-id="c6748-509">Hello 編輯器中輸入 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="c6748-509">Enter hello following in hello editor:</span></span>

    node.log("hello world");

<span data-ttu-id="c6748-510">現在執行本機測試回合。</span><span class="sxs-lookup"><span data-stu-id="c6748-510">Now execute a local test run.</span></span> <span data-ttu-id="c6748-511">之後此回合中，檢查 (透過 hello 系統索引標籤上 hello 編寫指令碼元件) hello 記錄屬性。</span><span class="sxs-lookup"><span data-stu-id="c6748-511">After this run, inspect (through hello System tab on hello Scripted Component) hello Logs property.</span></span>

![Hello World 記錄輸出](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-log-output.png)

<span data-ttu-id="c6748-513">*Hello World 記錄輸出*</span><span class="sxs-lookup"><span data-stu-id="c6748-513">*Hello world log output*</span></span>

<span data-ttu-id="c6748-514">hello 節點物件我們呼叫 hello 記錄方法，是指 tooour 目前 「 節點 」 或我們正在編寫指令碼中的 hello 元件。</span><span class="sxs-lookup"><span data-stu-id="c6748-514">hello node object we call hello log method on, refers tooour current "node" or hello component we're scripting within.</span></span> <span data-ttu-id="c6748-515">每個元件在這種情況有 hello 能力 toooutput 記錄資料，可透過 hello 系統索引標籤。在此情況下，我們會輸出 hello 字串常值"hello world"。</span><span class="sxs-lookup"><span data-stu-id="c6748-515">Every component as such has hello ability toooutput logging data, available through hello system tab. In this case, we output hello string literal "hello world".</span></span> <span data-ttu-id="c6748-516">這裡的重要 toounderstand 是，這可以證明 toobe 非常寶貴的偵錯工具，讓您深入了解哪些 hello 指令碼實際執行的動作。</span><span class="sxs-lookup"><span data-stu-id="c6748-516">Important toounderstand here is that this can prove toobe an invaluable debugging tool, providing you with insight on what hello script is actually doing.</span></span>

<span data-ttu-id="c6748-517">從在指令碼環境中，我們也對存取 tooproperties 其他元件。</span><span class="sxs-lookup"><span data-stu-id="c6748-517">From within our scripting environment, we also have access tooproperties on other components.</span></span> <span data-ttu-id="c6748-518">試試看：</span><span class="sxs-lookup"><span data-stu-id="c6748-518">Try this:</span></span>

    //inspect current node:
    def nodepath = node.getNodePath();
    node.log("this node path: " + nodepath);

    //walking up tooother nodes:
    def parentnode = node.getParentNode();
    def parentnodepath = parentnode.getNodePath();
    node.log("parent node path: " + parentnodepath);

    //read properties from a node:
    def sourceFileExt = parentnode.getPropertyAsString( "sourceFileExtension", null );
    def sourceFileName = parentnode.getPropertyAsString("sourceFileBaseName", null);
    node.log("source file name with extension " + sourceFileExt + " is: " + sourceFileName);

<span data-ttu-id="c6748-519">我們的記錄視窗會顯示下列 hello:</span><span class="sxs-lookup"><span data-stu-id="c6748-519">Our log window will show us hello following:</span></span>

![用於存取節點路徑的記錄輸出](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-log-output2.png)

<span data-ttu-id="c6748-521">*用於存取節點路徑的記錄輸出*</span><span class="sxs-lookup"><span data-stu-id="c6748-521">*Log output for accessing node paths*</span></span>

## <span data-ttu-id="c6748-522"><a id="frame_based_trim"></a>多位元速率 MP4 輸出以畫面格為基礎的修剪</span><span class="sxs-lookup"><span data-stu-id="c6748-522"><a id="frame_based_trim"></a>Frame-based trimming of multibitrate MP4 output</span></span>
<span data-ttu-id="c6748-523">從產生的工作流程開始[輸入 MXF 的多位元速率 MP4 輸出](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging)，我們現在將會尋找到修剪 hello 來源視訊根據框架計數。</span><span class="sxs-lookup"><span data-stu-id="c6748-523">Starting from a workflow that generates [a multibitrate MP4 output from an MXF input](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging), we will now be looking into trimming hello source video based on frame counts.</span></span>

### <span data-ttu-id="c6748-524"><a id="frame_based_trim_start"></a>加入要修剪的概觀 toostart 藍圖</span><span class="sxs-lookup"><span data-stu-id="c6748-524"><a id="frame_based_trim_start"></a>Blueprint overview toostart adding trimming to</span></span>
![加入要修剪的工作流程 toostart](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-workflow-start-adding-trimming-to.png)

<span data-ttu-id="c6748-526">*加入要修剪的工作流程 toostart*</span><span class="sxs-lookup"><span data-stu-id="c6748-526">*Workflow toostart adding trimming to*</span></span>

### <span data-ttu-id="c6748-527"><a id="frame_based_trim_clip_list"></a>使用 hello 剪輯清單 XML</span><span class="sxs-lookup"><span data-stu-id="c6748-527"><a id="frame_based_trim_clip_list"></a>Using hello Clip List XML</span></span>
<span data-ttu-id="c6748-528">在所有先前的工作流程教學課程，我們可以使用 hello 媒體檔案輸入元件做為我們視訊的輸入來源。</span><span class="sxs-lookup"><span data-stu-id="c6748-528">In all previous workflow tutorials, we used hello Media File Input component as our video input source.</span></span> <span data-ttu-id="c6748-529">針對這個特定案例，我們將使用 hello 剪輯清單來源元件改為。</span><span class="sxs-lookup"><span data-stu-id="c6748-529">For this specific scenario though, we'll be using hello Clip List Source component instead.</span></span> <span data-ttu-id="c6748-530">請注意，這不能 hello 慣用的方法來;只使用 hello 剪輯清單來源沒有真正原因 toodo 的因此時 (如同在下列情況下，我們做了其中的 hello hello 剪輯清單調整功能的使用)。</span><span class="sxs-lookup"><span data-stu-id="c6748-530">Note that this should not be hello preferred way of working; only use hello Clip List Source when there's a real reason toodo so (like in hello below case, where we're making use of hello clip list trimming capabilities).</span></span>

<span data-ttu-id="c6748-531">我們的媒體檔案輸入 toohello 剪輯來源清單，從 tooswitch hello 設計介面上拖曳 hello 剪輯清單來源元件，並連接 hello 剪輯清單 pin toohello 剪輯清單 XML 的 XML 節點 hello 工作流程設計工具。</span><span class="sxs-lookup"><span data-stu-id="c6748-531">tooswitch from our Media File Input toohello Clip List Source, drag hello Clip List Source component onto hello design surface and connect hello Clip List XML pin toohello Clip List XML node of hello workflow designer.</span></span> <span data-ttu-id="c6748-532">這應填入 hello 來源剪輯清單與輸出連接，根據 tooour 輸入的視訊。</span><span class="sxs-lookup"><span data-stu-id="c6748-532">This should populate hello Clip List Source with output pins, according tooour input video.</span></span> <span data-ttu-id="c6748-533">現在從 hello hello 剪輯清單來源 toohello 連線 hello 未壓縮視訊和未壓縮的音訊連接個別 AVC 編碼器和音訊資料流 Interleaver。</span><span class="sxs-lookup"><span data-stu-id="c6748-533">Now connect hello Uncompressed Video and Uncompressed Audio pins from hello hello Clip List Source toohello respective AVC Encoders and Audio Stream Interleaver.</span></span> <span data-ttu-id="c6748-534">現在要移除 hello 媒體檔案輸入。</span><span class="sxs-lookup"><span data-stu-id="c6748-534">Now remove hello Media File Input.</span></span>

![Hello 媒體檔案輸入取代 hello 剪輯來源清單](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-replaced-media-file-with-clip-source.png)

<span data-ttu-id="c6748-536">*Hello 媒體檔案輸入取代 hello 剪輯來源清單*</span><span class="sxs-lookup"><span data-stu-id="c6748-536">*Replaced hello Media File Input with hello Clip List Source*</span></span>

<span data-ttu-id="c6748-537">hello 剪輯清單來源元件會做為輸入 「 剪輯清單 XML"。</span><span class="sxs-lookup"><span data-stu-id="c6748-537">hello Clip List Source component takes as its input a "Clip List XML".</span></span> <span data-ttu-id="c6748-538">選取時 hello 來源檔案 tootest 與在本機，此剪輯清單 xml 是為您自動填入。</span><span class="sxs-lookup"><span data-stu-id="c6748-538">When selecting hello source file tootest with locally, this clip list xml is auto-populated for you.</span></span>

![自動填入剪輯清單 XML 屬性](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-auto-populated-clip-list-xml-property.png)

<span data-ttu-id="c6748-540">*自動填入剪輯清單 XML 屬性*</span><span class="sxs-lookup"><span data-stu-id="c6748-540">*Auto-populated Clip List XML property*</span></span>

<span data-ttu-id="c6748-541">尋找位元仔細 toohello xml，這是它的外觀類似：</span><span class="sxs-lookup"><span data-stu-id="c6748-541">Looking a bit closer toohello xml, this is how it looks like:</span></span>

![編輯剪輯清單對話方塊](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-edit-clip-list-dialog.png)

<span data-ttu-id="c6748-543">*編輯剪輯清單對話方塊*</span><span class="sxs-lookup"><span data-stu-id="c6748-543">*Edit clip list dialog*</span></span>

<span data-ttu-id="c6748-544">這但是不會反映 hello hello 剪輯清單 xml 功能。</span><span class="sxs-lookup"><span data-stu-id="c6748-544">This however does not reflect hello capabilities of hello clip list xml.</span></span> <span data-ttu-id="c6748-545">我們的其中一個選項是 tooadd 下 hello 視訊和音訊的來源，就像這樣的 「 修剪 」 項目：</span><span class="sxs-lookup"><span data-stu-id="c6748-545">One option we have is tooadd a "Trim" element under both hello video and audio source, like this:</span></span>

![新增修剪元素 toohello 剪輯清單](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-adding-trim-element-to-clip-list.png)

<span data-ttu-id="c6748-547">*新增修剪元素 toohello 剪輯清單*</span><span class="sxs-lookup"><span data-stu-id="c6748-547">*Adding a trim element toohello clip list*</span></span>

<span data-ttu-id="c6748-548">如果您修改 hello 剪輯清單 xml，像這樣上方，並執行本機測試回合，您會看到 hello 視訊正確已修剪介於 10 到 20 秒 hello 視訊中。</span><span class="sxs-lookup"><span data-stu-id="c6748-548">If you modify hello clip list xml like this above and perform a local test run, you'll see hello video correctly been trimmed between 10 and 20 seconds in hello video.</span></span>

<span data-ttu-id="c6748-549">當您執行本機執行，但此相同 cliplist xml 不會有相同效果時套用的 Azure 媒體服務中執行的工作流程中的 hello，就會發生反對 toowhat。</span><span class="sxs-lookup"><span data-stu-id="c6748-549">Contrary toowhat happens when you do a local run though, this very same cliplist xml would not have hello same effect when applied in a workflow that runs in Azure Media Services.</span></span> <span data-ttu-id="c6748-550">每次同樣地，根據 hello 輸入的檔 hello 編碼產生 Azure Premium 編碼程式啟動時，hello cliplist xml 時指定作業。</span><span class="sxs-lookup"><span data-stu-id="c6748-550">When Azure Premium Encoder starts, hello cliplist xml is generated every time again, based on hello input file hello encoding job was given.</span></span> <span data-ttu-id="c6748-551">這表示，我們會在 hello xml 執行的任何變更將不幸的是會被覆寫。</span><span class="sxs-lookup"><span data-stu-id="c6748-551">This means that any changes we do on hello xml would unfortunately be overridden.</span></span>

<span data-ttu-id="c6748-552">toocounter hello cliplist xml 抹除的編碼工作啟動時，我們可以重新產生它 hello 立即後方 hello 開始的工作流程。</span><span class="sxs-lookup"><span data-stu-id="c6748-552">toocounter hello cliplist xml being wiped when an encoding job is started, we can re-generate it on hello fly just after hello start of our workflow.</span></span> <span data-ttu-id="c6748-553">透過稱為「指令碼元件」的項目即可以採取這種自訂動作。</span><span class="sxs-lookup"><span data-stu-id="c6748-553">Such custom actions can be taken through what is called a "Scripted Component".</span></span> <span data-ttu-id="c6748-554">如需詳細資訊，請參閱[簡介 hello 編寫指令碼元件](media-services-media-encoder-premium-workflow-tutorials.md#scripting)。</span><span class="sxs-lookup"><span data-stu-id="c6748-554">For more information, see [Introducing hello Scripted Component](media-services-media-encoder-premium-workflow-tutorials.md#scripting).</span></span>

<span data-ttu-id="c6748-555">Hello 設計工具介面上拖曳編寫指令碼元件，並將它重新命名過"SetClipListXML"。</span><span class="sxs-lookup"><span data-stu-id="c6748-555">Drag a Scripted Component onto hello designer surface and rename it too"SetClipListXML".</span></span>

![加入指令碼元件](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-add-scripted-comp.png)

<span data-ttu-id="c6748-557">*加入指令碼元件*</span><span class="sxs-lookup"><span data-stu-id="c6748-557">*Adding a Scripted Component*</span></span>

<span data-ttu-id="c6748-558">當您檢查 hello 屬性 hello 編寫指令碼元件，將會顯示四種不同的指令碼類型的 hello、 每個可設定 tooa 不同的指令碼。</span><span class="sxs-lookup"><span data-stu-id="c6748-558">When you inspect hello properties of hello Scripted Component, hello four different script types will be shown, each configurable tooa different script.</span></span>

![指令碼元件屬性](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-scripted-comp-properties.png)

<span data-ttu-id="c6748-560">*指令碼元件屬性*</span><span class="sxs-lookup"><span data-stu-id="c6748-560">*Scripted Component properties*</span></span>

### <span data-ttu-id="c6748-561"><a id="frame_based_trim_modify_clip_list"></a>修改編寫指令碼元件中的 hello 剪輯清單</span><span class="sxs-lookup"><span data-stu-id="c6748-561"><a id="frame_based_trim_modify_clip_list"></a>Modifying hello clip list from a Scripted Component</span></span>
<span data-ttu-id="c6748-562">我們可以重新撰寫 hello cliplist 產生 xml，在工作流程啟動之前，我們需要 toohave 存取 toohello cliplist xml 屬性和內容。</span><span class="sxs-lookup"><span data-stu-id="c6748-562">Before we can re-write hello cliplist xml that is generated during workflow startup, we'll need toohave access toohello cliplist xml property and contents.</span></span> <span data-ttu-id="c6748-563">我們可以像這樣執行：</span><span class="sxs-lookup"><span data-stu-id="c6748-563">We can do so like this:</span></span>

    // get cliplist xml:
    def clipListXML = node.getProperty("../clipListXml");
    node.log("clip list xml coming in: " + clipListXML);

![記錄傳入剪輯清單](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-incoming-clip-list-logged.png)

<span data-ttu-id="c6748-565">*記錄傳入剪輯清單*</span><span class="sxs-lookup"><span data-stu-id="c6748-565">*Incoming clip list being logged*</span></span>

<span data-ttu-id="c6748-566">首先我們需要方式 toodetermine 點到哪一個點為止，我們想 tootrim hello 視訊。</span><span class="sxs-lookup"><span data-stu-id="c6748-566">First we need a way toodetermine from which point till which point we want tootrim hello video.</span></span> <span data-ttu-id="c6748-567">toomake hello 工作流程，這個方便 toohello 小於技術使用者發行 hello 圖形的兩個屬性 toohello 根。</span><span class="sxs-lookup"><span data-stu-id="c6748-567">toomake this convenient toohello less-technical user of hello workflow, publish two properties toohello root of hello graph.</span></span> <span data-ttu-id="c6748-568">toodo，hello 設計工具介面上按一下滑鼠右鍵，然後選取 「 新增屬性 」:</span><span class="sxs-lookup"><span data-stu-id="c6748-568">toodo this, right click hello designer surface and select "Add Property":</span></span>

* <span data-ttu-id="c6748-569">第一個屬性："ClippingTimeStart"，類型："TIMECODE"</span><span class="sxs-lookup"><span data-stu-id="c6748-569">First property: "ClippingTimeStart" of type: "TIMECODE"</span></span>
* <span data-ttu-id="c6748-570">第二個屬性："ClippingTimeEnd"，類型："TIMECODE"</span><span class="sxs-lookup"><span data-stu-id="c6748-570">Second property: "ClippingTimeEnd" of type: "TIMECODE"</span></span>

![加入屬性對話方塊的剪輯開始時間](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-clip-start-time.png)

<span data-ttu-id="c6748-572">*加入屬性對話方塊的剪輯開始時間*</span><span class="sxs-lookup"><span data-stu-id="c6748-572">*Add Property dialog for clipping start time*</span></span>

![工作流程根目錄上發佈的剪輯時間屬性](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-clip-time-props.png)

<span data-ttu-id="c6748-574">*工作流程根目錄上發佈的剪輯時間屬性*</span><span class="sxs-lookup"><span data-stu-id="c6748-574">*Published clipping time props on workflow root*</span></span>

<span data-ttu-id="c6748-575">設定這兩個屬性 tooa 適當的值：</span><span class="sxs-lookup"><span data-stu-id="c6748-575">Configure both properties tooa suitable value:</span></span>

![設定開始和結束的內容和結束時間裁剪 hello](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-configure-clip-start-end-prop.png)

<span data-ttu-id="c6748-577">*設定開始和結束的內容和結束時間裁剪 hello*</span><span class="sxs-lookup"><span data-stu-id="c6748-577">*Configure hello clipping start and end properties*</span></span>

<span data-ttu-id="c6748-578">現在，從我們的指令碼內，我們就可以存取這兩個屬性，像這樣：</span><span class="sxs-lookup"><span data-stu-id="c6748-578">Now, from within our script, we can access both properties, like this:</span></span>

    // get start and end of clipping:
    def clipstart = node.getProperty("../ClippingTimeStart").toString();
    def clipend = node.getProperty("../ClippingTimeEnd").toString();

    node.log("clipping start: " + clipstart);
    node.log("clipping end: " + clipend);

![顯示剪輯的開始與結束的記錄視窗](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-show-start-end-clip.png)

<span data-ttu-id="c6748-580">*顯示剪輯的開始與結束的記錄視窗*</span><span class="sxs-lookup"><span data-stu-id="c6748-580">*Log window showing start and end of clipping*</span></span>

<span data-ttu-id="c6748-581">讓我們更方便 toouse 表單，使用簡單的規則運算式剖析 hello 播放字串：</span><span class="sxs-lookup"><span data-stu-id="c6748-581">Let's parse hello timecode strings into a more convenient toouse form, using a simple regular expression:</span></span>

    //parse hello start timing:
    def startregresult = (~/(\d\d:\d\d:\d\d:\d\d)\/(\d\d)/).matcher(clipstart);
    startregresult.matches();
    def starttimecode = startregresult.group(1);
    node.log("timecode start is: " + starttimecode);
    def startframerate = startregresult.group(2);
    node.log("framerate start is: " + startframerate);

    //parse hello end timing:
    def endregresult = (~/(\d\d:\d\d:\d\d:\d\d)\/(\d\d)/).matcher(clipend);
    endregresult.matches();
    def endtimecode = endregresult.group(1);
    node.log("timecode end is: " + endtimecode);
    def endframerate = endregresult.group(2);
    node.log("framerate end is: " + endframerate);

![具有剖析的時間碼輸出的記錄檔視窗](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-output-parsed-timecode.png)

<span data-ttu-id="c6748-583">*具有剖析的時間碼輸出的記錄檔視窗*</span><span class="sxs-lookup"><span data-stu-id="c6748-583">*Log window with output of parsed timecode*</span></span>

<span data-ttu-id="c6748-584">於此資訊，我們現在可以修改 hello cliplist xml tooreflect hello 開始與 hello 的結束時間所需的 hello 影片框架精確裁剪。</span><span class="sxs-lookup"><span data-stu-id="c6748-584">With this information at hand, we can now modify hello cliplist xml tooreflect hello start and end times for hello desired frame-accurate clipping of hello movie.</span></span>

![指令碼程式碼 tooadd 修剪項目](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-add-trim-elements.png)

<span data-ttu-id="c6748-586">*指令碼程式碼 tooadd 修剪項目*</span><span class="sxs-lookup"><span data-stu-id="c6748-586">*Script code tooadd trim elements*</span></span>

<span data-ttu-id="c6748-587">這是透過一般的字串處理作業完成。</span><span class="sxs-lookup"><span data-stu-id="c6748-587">This was done through normal string manipulation operations.</span></span> <span data-ttu-id="c6748-588">hello 產生的已修改的剪輯清單 xml 重新寫入 toohello clipListXML 屬性 hello 工作流程根目錄上透過 hello"setProperty 」 方法。</span><span class="sxs-lookup"><span data-stu-id="c6748-588">hello resulting modified clip list xml is written back toohello clipListXML property on hello workflow root through hello "setProperty" method.</span></span> <span data-ttu-id="c6748-589">另一個測試回合之後，hello 記錄視窗會顯示我們 hello 遵循：</span><span class="sxs-lookup"><span data-stu-id="c6748-589">hello log window after another test run would show us hello following:</span></span>

![記錄產生剪輯清單 hello](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-log-result-clip-list.png)

<span data-ttu-id="c6748-591">*記錄產生剪輯清單 hello*</span><span class="sxs-lookup"><span data-stu-id="c6748-591">*Logging hello resulting clip list*</span></span>

<span data-ttu-id="c6748-592">執行測試回合 toosee hello 視訊和音訊資料流已裁剪的方式。</span><span class="sxs-lookup"><span data-stu-id="c6748-592">Do a test-run toosee how hello video and audio streams have been clipped.</span></span> <span data-ttu-id="c6748-593">當您將會執行包含不同的 hello 修剪點值的多個測試回合，您會注意到，這些將不會考量不過 ！</span><span class="sxs-lookup"><span data-stu-id="c6748-593">As you'll do more than one test-run with different values for hello trimming points, you'll notice that those will not be taken into account however!</span></span> <span data-ttu-id="c6748-594">hello 這個錯誤的原因是該 hello 設計工具，不同於 hello Azure 執行階段時，每次執行時不會不覆寫 hello cliplist xml。</span><span class="sxs-lookup"><span data-stu-id="c6748-594">hello reason for this is that hello designer, unlike hello Azure runtime, does NOT override hello cliplist xml every run.</span></span> <span data-ttu-id="c6748-595">這表示，只有 hello 第一次設定 hello 進出點，會導致 hello xml tootransform、 所有 hello 其他時間，我們防護子句 (如果 (clipListXML.indexOf (「<trim>") = =-1)) 會避免 hello 工作流程新增另一個修剪當已經有一個出現項目。</span><span class="sxs-lookup"><span data-stu-id="c6748-595">This means that only hello very first time you have set hello in and out points, will cause hello xml tootransform, all hello other times, our guard clause (if(clipListXML.indexOf("<trim>") == -1)) will prevent hello workflow from adding another trim element when there's already one present.</span></span>

<span data-ttu-id="c6748-596">toomake 我們的工作流程方便 tootest 在本機，我們最佳加入如果修剪的項目已經存在，會檢查某些馬上保留程式碼。</span><span class="sxs-lookup"><span data-stu-id="c6748-596">toomake our workflow convenient tootest locally, we best add some house-keeping code that inspects if a trim element was already present.</span></span> <span data-ttu-id="c6748-597">如果是這樣，我們可以移除它，然後再繼續修改 hello 與 hello 新值的 xml。</span><span class="sxs-lookup"><span data-stu-id="c6748-597">If so, we can remove it before continuing by modifying hello xml with hello new values.</span></span> <span data-ttu-id="c6748-598">而不是使用純文字字串操作，很可能是更安全的 toodo 透過實際的 xml 物件模型剖析。</span><span class="sxs-lookup"><span data-stu-id="c6748-598">Rather than using plain string manipulations, it's probably safer toodo this through real xml object model parsing.</span></span>

<span data-ttu-id="c6748-599">我們可以透過新增這類程式碼之前，我們需要的 tooadd 數目在 hello 匯入陳述式先啟動指令碼：</span><span class="sxs-lookup"><span data-stu-id="c6748-599">Before we can add such code though, we'll need tooadd a number of import statements at hello start of our script first:</span></span>

    import javax.xml.parsers.*;
    import org.xml.sax.*;
    import org.w3c.dom.*;
    import javax.xml.*;
    import javax.xml.xpath.*;
    import javax.xml.transform.*;
    import javax.xml.transform.stream.*;
    import javax.xml.transform.dom.*;

<span data-ttu-id="c6748-600">在此之後，我們可以加入清除程式碼所需的 hello:</span><span class="sxs-lookup"><span data-stu-id="c6748-600">After this, we can add hello required cleaning code:</span></span>

    //for local testing: delete any pre-existing trim elements from hello clip list xml by parsing hello xml into a DOM:
    DocumentBuilderFactory factory=DocumentBuilderFactory.newInstance();
    DocumentBuilder builder=factory.newDocumentBuilder();
    InputSource is=new InputSource(new StringReader(clipListXML));
    Document dom=builder.parse(is);

    //find hello trim element inside videoSource and audioSource and remove it if it exists already:
    XPath xpath = XPathFactory.newInstance().newXPath();
    String findAllTrimElements = "//trim";
    NodeList trimelems = xpath.evaluate(findAllTrimElements,dom,XPathConstants.NODESET);

    //copy trim nodes into a "to-be-deleted" collection
    Set<Element> elementsToDelete = new HashSet<Element>();
    for (int i = 0; i < trimelems.getLength(); i++) {
        Element e = (Element)trimelems.item(i);
        elementsToDelete.add(e);
    }

    node.log("about toodelete any existing trim nodes");
     //delete hello trim nodes:
    elementsToDelete.each{
        e -> e.getParentNode().removeChild(e);
    };
    node.log("deleted any existing trim nodes");

    //serialize hello modified clip list xml dom into a string:
    def transformer = TransformerFactory.newInstance().newTransformer();
    StreamResult result = new StreamResult(new StringWriter());
    DOMSource source = new DOMSource(dom);
    transformer.transform(source, result);
    clipListXML = result.getWriter().toString();

<span data-ttu-id="c6748-601">這個程式碼會正上方的中，我們加入 hello 修剪元素 toohello cliplist xml hello 點。</span><span class="sxs-lookup"><span data-stu-id="c6748-601">This code goes just above hello point at which we add hello trim elements toohello cliplist xml.</span></span>

<span data-ttu-id="c6748-602">此時，我們可以執行和修改工作流程時一樣我們想要在具有 hello 變更曾經套用時的時間。</span><span class="sxs-lookup"><span data-stu-id="c6748-602">At this point, we can run and modify our workflow as much as we want while having hello changes applied ever time.</span></span>    

### <span data-ttu-id="c6748-603"><a id="frame_based_trim_clippingenabled_prop"></a>加入 ClippingEnabled 便利屬性</span><span class="sxs-lookup"><span data-stu-id="c6748-603"><a id="frame_based_trim_clippingenabled_prop"></a>Adding a ClippingEnabled convenience property</span></span>
<span data-ttu-id="c6748-604">可能不一定要修剪 toohappen，讓我們先加入方便的布林值旗標，指出完成關閉工作流程是否我們想要 tooenable 修剪 / 結束時間裁剪。</span><span class="sxs-lookup"><span data-stu-id="c6748-604">As you might not always want trimming toohappen, let's finish off our workflow by adding a convenient boolean flag that indicates whether or not we want tooenable trimming / clipping.</span></span>

<span data-ttu-id="c6748-605">就像之前，發行我們稱為 「 ClippingEnabled 」 的工作流程的新屬性 toohello 根型別"BOOLEAN"。</span><span class="sxs-lookup"><span data-stu-id="c6748-605">Just as before, publish a new property toohello root of our workflow called "ClippingEnabled" of type "BOOLEAN".</span></span>

![發佈啟用剪輯屬性](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-enable-clip.png)

<span data-ttu-id="c6748-607">*發佈啟用剪輯屬性*</span><span class="sxs-lookup"><span data-stu-id="c6748-607">*Published a property for enabling clipping*</span></span>

<span data-ttu-id="c6748-608">以下列簡單的防護子句 hello，我們可以檢查是否需要調整，並決定是否我們剪輯清單在這種情況需要 toobe 修改。</span><span class="sxs-lookup"><span data-stu-id="c6748-608">With hello below simple guard clause, we can check if trimming is required and decide if our clip list as such needs toobe modified or not.</span></span>

    //check if clipping is required:
    def clippingrequired = node.getProperty("../ClippingEnabled");
    node.log("clipping required: " + clippingrequired.toString());
    if(clippingrequired == null || clippingrequired == false)
    {
        node.setProperty("../clipListXml",clipListXML);
        node.log("no clipping required");
        return;
    }


### <span data-ttu-id="c6748-609"><a id="code"></a>完整程式碼</span><span class="sxs-lookup"><span data-stu-id="c6748-609"><a id="code"></a>Complete code</span></span>
    import javax.xml.parsers.*;
    import org.xml.sax.*;
    import org.w3c.dom.*;
    import javax.xml.*;
    import javax.xml.xpath.*;
    import javax.xml.transform.*;
    import javax.xml.transform.stream.*;
    import javax.xml.transform.dom.*;

    // get cliplist xml:
    def clipListXML = node.getProperty("../clipListXml");
    node.log("clip list xml coming in: \n" + clipListXML);
    // get start and end of clipping:
    def clipstart = node.getProperty("../ClippingTimeStart").toString();
    def clipend = node.getProperty("../ClippingTimeEnd").toString();

    //parse hello start timing:
    def startregresult = (~/(\d\d:\d\d:\d\d:\d\d)\/(\d\d)/).matcher(clipstart);
    startregresult.matches();
    def starttimecode = startregresult.group(1);
    node.log("timecode start is: " + starttimecode);
    def startframerate = startregresult.group(2);
    node.log("framerate start is: " + startframerate);

    //parse hello end timing:
    def endregresult = (~/(\d\d:\d\d:\d\d:\d\d)\/(\d\d)/).matcher(clipend);
    endregresult.matches();
    def endtimecode = endregresult.group(1);
    node.log("timecode end is: " + endtimecode);
    def endframerate = endregresult.group(2);

    node.log("framerate end is: " + endframerate);

    //for local testing: delete any pre-existing trim elements
    //from hello clip list xml by parsing hello xml into a DOM:

    DocumentBuilderFactory factory=DocumentBuilderFactory.newInstance();
    DocumentBuilder builder=factory.newDocumentBuilder();
    InputSource is=new InputSource(new StringReader(clipListXML));
    Document dom=builder.parse(is);

    //find hello trim element inside videoSource and audioSource and remove it if it exists already:
    XPath xpath = XPathFactory.newInstance().newXPath();
    String findAllTrimElements = "//trim";
    NodeList trimelems = xpath.evaluate(findAllTrimElements, dom, XPathConstants.NODESET);

    //copy trim nodes into a "to-be-deleted" collection
    Set<Element> elementsToDelete = new HashSet<Element>();
    for (int i = 0; i < trimelems.getLength(); i++) {
        Element e = (Element)trimelems.item(i);
        elementsToDelete.add(e);
    }

    node.log("about toodelete any existing trim nodes");
    //delete hello trim nodes:
    elementsToDelete.each{ e ->
        e.getParentNode().removeChild(e);
    };
    node.log("deleted any existing trim nodes");

    //serialize hello modified clip list xml dom into a string:
    def transformer = TransformerFactory.newInstance().newTransformer();
    StreamResult result = new StreamResult(new StringWriter());
    DOMSource source = new DOMSource(dom);
    transformer.transform(source, result);
    clipListXML = result.getWriter().toString();

    //check if clipping is required:
    def clippingrequired = node.getProperty("../ClippingEnabled");
    node.log("clipping required: " + clippingrequired.toString());
    if(clippingrequired == null || clippingrequired == false)
    {
        node.setProperty("../clipListXml",clipListXML);
        node.log("no clipping required");
        return;
    }

    //add trim elements toocliplist xml
    if ( clipListXML.indexOf("<trim>") == -1 )
    {
        //trim video
        clipListXML = clipListXML.replace("<videoSource>","<videoSource>\n <trim>\n <inPoint fps=\""+
            startframerate +"\">" + starttimecode +
            "</inPoint>\n" + "<outPoint fps=\"" + endframerate +"\"> " + endtimecode +
            " </outPoint>\n </trim> \n");
        //trim audio
        clipListXML = clipListXML.replace("<audioSource>","<audioSource>\n <trim>\n <inPoint fps=\""+
            startframerate +"\">" + starttimecode +
            "</inPoint>\n" + "<outPoint fps=\""+ endframerate +"\">" +
            endtimecode + "</outPoint>\n </trim>\n");
        node.log( "clip list going out: \n" +clipListXML );
        node.setProperty("../clipListXml",clipListXML);
    }


## <a name="also-see"></a><span data-ttu-id="c6748-610">另請參閱</span><span class="sxs-lookup"><span data-stu-id="c6748-610">Also see</span></span>
[<span data-ttu-id="c6748-611">介紹 Azure 媒體服務中的 Premium 編碼</span><span class="sxs-lookup"><span data-stu-id="c6748-611">Introducing Premium Encoding in Azure Media Services</span></span>](http://azure.microsoft.com/blog/2015/03/05/introducing-premium-encoding-in-azure-media-services)

[<span data-ttu-id="c6748-612">如何在 Azure Media Services 編碼 Premium tooUse</span><span class="sxs-lookup"><span data-stu-id="c6748-612">How tooUse Premium Encoding in Azure Media Services</span></span>](http://azure.microsoft.com/blog/2015/03/06/how-to-use-premium-encoding-in-azure-media-services)

[<span data-ttu-id="c6748-613">透過 Azure 媒體服務編碼的隨選內容</span><span class="sxs-lookup"><span data-stu-id="c6748-613">Encoding On-Demand Content with Azure Media Service</span></span>](media-services-encode-asset.md#media-encoder-premium-workflow)

[<span data-ttu-id="c6748-614">Media Encoder Premium Workflow 格式和轉碼器</span><span class="sxs-lookup"><span data-stu-id="c6748-614">Media Encoder Premium Workflow Formats and Codecs</span></span>](media-services-premium-workflow-encoder-formats.md)

[<span data-ttu-id="c6748-615">範例工作流程檔案</span><span class="sxs-lookup"><span data-stu-id="c6748-615">Sample workflow files</span></span>](http://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows)

[<span data-ttu-id="c6748-616">Azure 媒體服務總管工具</span><span class="sxs-lookup"><span data-stu-id="c6748-616">Azure Media Services Explorer tool</span></span>](http://aka.ms/amse)

## <a name="media-services-learning-paths"></a><span data-ttu-id="c6748-617">媒體服務學習路徑</span><span class="sxs-lookup"><span data-stu-id="c6748-617">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="c6748-618">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="c6748-618">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
