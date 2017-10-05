---
title: "進階媒體編碼器 Premium 工作流程教學課程"
description: "本文件包含的逐步解說可示範如何使用媒體編碼器 Premium 工作流程執行進階的工作，以及如何使用工作流程設計工具建立複雜的工作流程。"
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
ms.openlocfilehash: 565497bd5a35e3c4d69d29512307cf3ca2364bdd
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="advanced-media-encoder-premium-workflow-tutorials"></a><span data-ttu-id="ee1eb-103">進階媒體編碼器 Premium 工作流程教學課程</span><span class="sxs-lookup"><span data-stu-id="ee1eb-103">Advanced Media Encoder Premium Workflow tutorials</span></span>
## <a name="overview"></a><span data-ttu-id="ee1eb-104">Overview</span><span class="sxs-lookup"><span data-stu-id="ee1eb-104">Overview</span></span>
<span data-ttu-id="ee1eb-105">本文件包含的逐步解說可示範如何使用**工作流程設計工具**自訂工作流程。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-105">This document contains walkthroughs that show how to customize workflows with  **Workflow Designer**.</span></span> <span data-ttu-id="ee1eb-106">您可以在[這裡](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows/PremiumEncoderWorkflowSamples)尋找實際的工作流程檔案。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-106">You can find the actual workflow files [here](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows/PremiumEncoderWorkflowSamples).</span></span>  

## <a name="toc"></a><span data-ttu-id="ee1eb-107">目錄</span><span class="sxs-lookup"><span data-stu-id="ee1eb-107">TOC</span></span>
<span data-ttu-id="ee1eb-108">本文涵蓋下列主題：</span><span class="sxs-lookup"><span data-stu-id="ee1eb-108">The following topics are covered:</span></span>

* [<span data-ttu-id="ee1eb-109">將 MXF 編碼為單一位元速率 MP4</span><span class="sxs-lookup"><span data-stu-id="ee1eb-109">Encoding MXF into a single bitrate MP4</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4)
  * [<span data-ttu-id="ee1eb-110">開始新的工作流程</span><span class="sxs-lookup"><span data-stu-id="ee1eb-110">Starting a new workflow</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_start_new)
  * [<span data-ttu-id="ee1eb-111">使用媒體檔案輸入</span><span class="sxs-lookup"><span data-stu-id="ee1eb-111">Using the Media File Input</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_file_input)
  * [<span data-ttu-id="ee1eb-112">檢查媒體串流</span><span class="sxs-lookup"><span data-stu-id="ee1eb-112">Inspecting media streams</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_streams)
  * [<span data-ttu-id="ee1eb-113">為產生的 MP4 檔案加入視訊編碼器</span><span class="sxs-lookup"><span data-stu-id="ee1eb-113">Adding a video encoder for .MP4 file generation</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_file_generation)
  * [<span data-ttu-id="ee1eb-114">對音訊串流編碼</span><span class="sxs-lookup"><span data-stu-id="ee1eb-114">Encoding the audio stream</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_audio)
  * [<span data-ttu-id="ee1eb-115">將音訊和視訊串流多工處理為 MP4 容器</span><span class="sxs-lookup"><span data-stu-id="ee1eb-115">Multiplexing Audio and Video streams into an MP4 container</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_audio_and_fideo)
  * [<span data-ttu-id="ee1eb-116">寫入 MP4 檔案</span><span class="sxs-lookup"><span data-stu-id="ee1eb-116">Writing the MP4 file</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_writing_mp4)
  * [<span data-ttu-id="ee1eb-117">從輸出檔案建立媒體服務資產</span><span class="sxs-lookup"><span data-stu-id="ee1eb-117">Creating a Media Services Asset from the output file</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_asset_from_output)
  * [<span data-ttu-id="ee1eb-118">在本機測試完成的工作流程</span><span class="sxs-lookup"><span data-stu-id="ee1eb-118">Test the finished workflow locally</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_test)
* [<span data-ttu-id="ee1eb-119">將 MXF 編碼為多位元速率 MP4 - 動態封裝已啟用</span><span class="sxs-lookup"><span data-stu-id="ee1eb-119">Encoding MXF into multibitrate MP4s - dynamic packaging enabled</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging)
  * [<span data-ttu-id="ee1eb-120">加入一或多個其他的 MP4 輸出</span><span class="sxs-lookup"><span data-stu-id="ee1eb-120">Adding one or more additional MP4 outputs</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging_more_outputs)
  * [<span data-ttu-id="ee1eb-121">設定檔案輸出名稱</span><span class="sxs-lookup"><span data-stu-id="ee1eb-121">Configuring the file output names</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging_conf_output_names)
  * [<span data-ttu-id="ee1eb-122">加入個別的曲目</span><span class="sxs-lookup"><span data-stu-id="ee1eb-122">Adding a separate Audio Track</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging_audio_tracks)
  * [<span data-ttu-id="ee1eb-123">加入 .ISM SMIL 檔案</span><span class="sxs-lookup"><span data-stu-id="ee1eb-123">Adding the .ISM SMIL File</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging_ism_file)
* [<span data-ttu-id="ee1eb-124">將 MXF 編碼為多位元速率 MP4 - 增強的藍圖</span><span class="sxs-lookup"><span data-stu-id="ee1eb-124">Encoding MXF into multibitrate MP4 - enhanced blueprint</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to__multibitrate_MP4)
  * [<span data-ttu-id="ee1eb-125">要增強的工作流程概觀</span><span class="sxs-lookup"><span data-stu-id="ee1eb-125">Workflow overview to enhance</span></span>](#workflow-overview-to-enhance)
  * [<span data-ttu-id="ee1eb-126">檔案命名慣例</span><span class="sxs-lookup"><span data-stu-id="ee1eb-126">File Naming Conventions</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to__multibitrate_MP4_file_naming)
  * [<span data-ttu-id="ee1eb-127">發佈元件屬性至工作流程根目錄</span><span class="sxs-lookup"><span data-stu-id="ee1eb-127">Publishing component properties onto the workflow root</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to__multibitrate_MP4_publishing)
  * [<span data-ttu-id="ee1eb-128">讓產生的輸出檔案名稱依賴發佈的屬性值</span><span class="sxs-lookup"><span data-stu-id="ee1eb-128">Have generated output file names rely on published property values</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to__multibitrate_MP4_output_files)
* [<span data-ttu-id="ee1eb-129">加入縮圖至多位元速率 MP4 輸出</span><span class="sxs-lookup"><span data-stu-id="ee1eb-129">Adding thumbnails to multibitrate MP4 output</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4)
  * [<span data-ttu-id="ee1eb-130">要加入縮圖的目標工作流程概觀</span><span class="sxs-lookup"><span data-stu-id="ee1eb-130">Workflow overview to add thumbnails to</span></span>](#workflow-overview-to-add-thumbnails-to)
  * [<span data-ttu-id="ee1eb-131">加入 JPG 編碼</span><span class="sxs-lookup"><span data-stu-id="ee1eb-131">Adding JPG Encoding</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4__with_jpg)
  * [<span data-ttu-id="ee1eb-132">處理色彩空間轉換</span><span class="sxs-lookup"><span data-stu-id="ee1eb-132">Dealing with Color Space conversion</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4_color_space)
  * [<span data-ttu-id="ee1eb-133">寫入縮圖</span><span class="sxs-lookup"><span data-stu-id="ee1eb-133">Writing the thumbnails</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4_writing_thumbnails)
  * [<span data-ttu-id="ee1eb-134">偵測工作流程中的錯誤</span><span class="sxs-lookup"><span data-stu-id="ee1eb-134">Detecting errors in a workflow</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4_errors)
  * [<span data-ttu-id="ee1eb-135">工作流程完成</span><span class="sxs-lookup"><span data-stu-id="ee1eb-135">Finished Workflow</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4_finish)
* [<span data-ttu-id="ee1eb-136">多位元速率 MP4 輸出以時間為基礎的修剪</span><span class="sxs-lookup"><span data-stu-id="ee1eb-136">Time-based trimming of multibitrate MP4 output</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#time_based_trim)
  * [<span data-ttu-id="ee1eb-137">要開始加入修剪的目標工作流程概觀</span><span class="sxs-lookup"><span data-stu-id="ee1eb-137">Workflow overview to start adding trimming to</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#time_based_trim_start)
  * [<span data-ttu-id="ee1eb-138">使用串流修剪器</span><span class="sxs-lookup"><span data-stu-id="ee1eb-138">Using the Stream Trimmer</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#time_based_trim_use_stream_trimmer)
  * [<span data-ttu-id="ee1eb-139">工作流程完成</span><span class="sxs-lookup"><span data-stu-id="ee1eb-139">Finished Workflow</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#time_based_trim_finish)
* [<span data-ttu-id="ee1eb-140">推出指令碼元件</span><span class="sxs-lookup"><span data-stu-id="ee1eb-140">Introducing the Scripted Component</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#scripting)
  * [<span data-ttu-id="ee1eb-141">工作流程內的指令碼：Hello World</span><span class="sxs-lookup"><span data-stu-id="ee1eb-141">Scripting within a workflow: hello world</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#scripting_hello_world)
* [<span data-ttu-id="ee1eb-142">多位元速率 MP4 輸出以畫面格為基礎的修剪</span><span class="sxs-lookup"><span data-stu-id="ee1eb-142">Frame-based trimming of multibitrate MP4 output</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim)
  * [<span data-ttu-id="ee1eb-143">要開始加入修剪的目標藍圖概觀</span><span class="sxs-lookup"><span data-stu-id="ee1eb-143">Blueprint overview to start adding trimming to</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim_start)
  * [<span data-ttu-id="ee1eb-144">使用剪輯清單 XML</span><span class="sxs-lookup"><span data-stu-id="ee1eb-144">Using the Clip List XML</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim_clip_list)
  * [<span data-ttu-id="ee1eb-145">透過指令碼元件修改剪輯清單</span><span class="sxs-lookup"><span data-stu-id="ee1eb-145">Modifying the clip list from a Scripted Component</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim_modify_clip_list)
  * [<span data-ttu-id="ee1eb-146">加入 ClippingEnabled 便利屬性</span><span class="sxs-lookup"><span data-stu-id="ee1eb-146">Adding a ClippingEnabled convenience property</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim_clippingenabled_prop)

## <span data-ttu-id="ee1eb-147"><a id="MXF_to_MP4"></a>將 MXF 編碼為單一位元速率 MP4</span><span class="sxs-lookup"><span data-stu-id="ee1eb-147"><a id="MXF_to_MP4"></a>Encoding MXF into a single bitrate MP4</span></span>
<span data-ttu-id="ee1eb-148">在本逐步解說中，我們將使用來自 .MXF 輸入檔案 AAC-HE 編碼的音訊來建立單一位元速率 .MP4 檔案。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-148">In this walkthrough we'll create a single bitrate .MP4 file with AAC-HE encoded audio from an .MXF input file.</span></span>

### <span data-ttu-id="ee1eb-149"><a id="MXF_to_MP4_start_new"></a>開始新的工作流程</span><span class="sxs-lookup"><span data-stu-id="ee1eb-149"><a id="MXF_to_MP4_start_new"></a>Starting a new workflow</span></span>
<span data-ttu-id="ee1eb-150">開啟「工作流程設計工具」，然後選取 [檔案] - [新增工作區] - [轉碼藍圖]</span><span class="sxs-lookup"><span data-stu-id="ee1eb-150">Open Workflow Designer and select "File"-"New Workspace"-"Transcode Blueprint"</span></span>

<span data-ttu-id="ee1eb-151">新的工作流程將顯示 3 個元素：</span><span class="sxs-lookup"><span data-stu-id="ee1eb-151">The new workflow will show 3 elements:</span></span>

* <span data-ttu-id="ee1eb-152">主要來源檔案</span><span class="sxs-lookup"><span data-stu-id="ee1eb-152">Primary Source File</span></span>
* <span data-ttu-id="ee1eb-153">剪輯清單 XML</span><span class="sxs-lookup"><span data-stu-id="ee1eb-153">Clip List XML</span></span>
* <span data-ttu-id="ee1eb-154">輸出檔案/資產</span><span class="sxs-lookup"><span data-stu-id="ee1eb-154">Output File/Asset</span></span>  

![新編碼工作流程](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-transcode-blueprint.png)

<span data-ttu-id="ee1eb-156">*新編碼工作流程*</span><span class="sxs-lookup"><span data-stu-id="ee1eb-156">*New Encoding Workflow*</span></span>

### <span data-ttu-id="ee1eb-157"><a id="MXF_to_MP4_with_file_input"></a>使用媒體檔案輸入</span><span class="sxs-lookup"><span data-stu-id="ee1eb-157"><a id="MXF_to_MP4_with_file_input"></a>Using the Media File Input</span></span>
<span data-ttu-id="ee1eb-158">為了接受我們的輸入媒體檔案，您會從加入媒體檔案輸入元件開始。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-158">In order to accept our input media file, one starts with adding a Media File Input component.</span></span> <span data-ttu-id="ee1eb-159">若要將元件加入至工作流程，請在 [儲存機制] 搜尋方塊中尋找它，然後將所需的項目拖曳至設計工具窗格。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-159">To add a component to the workflow, look for it in the Repository search box and drag the desired entry onto the designer pane.</span></span> <span data-ttu-id="ee1eb-160">請對「媒體檔案輸入」執行這項操作，並將 [主要來源檔案] 元件從 [媒體檔案輸入] 連接至 [檔案名稱] 輸入接點。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-160">Do this for the Media File Input and connect the Primary Source File component to the Filename input pin from the Media File Input.</span></span>

![連接的媒體檔案輸入](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-file-input.png)

<span data-ttu-id="ee1eb-162">*連接的媒體檔案輸入*</span><span class="sxs-lookup"><span data-stu-id="ee1eb-162">*Connected Media File Input*</span></span>

<span data-ttu-id="ee1eb-163">在可以執行更多動作之前，我們必須先向工作流程設計工具指出我們要用來設計工作流程的範例檔案。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-163">Before we can do much else, we'll first need to indicate to the workflow designer what sample file we'd like to use to design our workflow with.</span></span> <span data-ttu-id="ee1eb-164">若要這樣做，請按一下設計工具窗格背景，並在右手邊屬性窗格中尋找 [主要來源檔案] 屬性。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-164">To do so, click the designer pane background and look for the Primary Source File property on the right-hand property pane.</span></span> <span data-ttu-id="ee1eb-165">按一下資料夾圖示，然後選取所需的檔案來測試工作流程。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-165">Click the folder icon and select the desired file to test the workflow with.</span></span> <span data-ttu-id="ee1eb-166">完成此動作之後，媒體檔案輸入元件會檢查檔案，並填入其輸出接點，以反映它檢查的檔案。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-166">As soon as this is done, the Media File Input component will inspect the file and populate its output pins to reflect the file it inspected.</span></span>

![填入媒體檔案輸入](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-populated-media-file-input.png)

<span data-ttu-id="ee1eb-168">*填入媒體檔案輸入*</span><span class="sxs-lookup"><span data-stu-id="ee1eb-168">*Populated Media File Input*</span></span>

<span data-ttu-id="ee1eb-169">雖然這會指定我們想要使用的輸入，它還未告知編碼的輸出應該通往的位置。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-169">While this specifies with what input we'd like to work with, it doesn't tell yet where the encoded output should go to.</span></span> <span data-ttu-id="ee1eb-170">類似於設定主要來源檔案的方式，現在設定輸出資料夾變數的屬性，就在其下方。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-170">Similar to how the Primary Source File was configured, now configure the Output Folder Variable property, just below it.</span></span>

![設定輸入和輸出屬性](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-configured-io-properties.png)

<span data-ttu-id="ee1eb-172">*設定輸入和輸出屬性*</span><span class="sxs-lookup"><span data-stu-id="ee1eb-172">*Configured Input and Output properties*</span></span>

### <span data-ttu-id="ee1eb-173"><a id="MXF_to_MP4_streams"></a>檢查媒體串流</span><span class="sxs-lookup"><span data-stu-id="ee1eb-173"><a id="MXF_to_MP4_streams"></a>Inspecting media streams</span></span>
<span data-ttu-id="ee1eb-174">通常您會想要知道經過工作流程之後串流的外觀。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-174">Often it's desired to know how the stream looks like that flows through the workflow.</span></span> <span data-ttu-id="ee1eb-175">若要在工作流程中的任何一點檢查串流，只要按一下任何元件上的輸出或輸入接點。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-175">To inspect a stream at any point in the workflow, just click an output or input pin on any of the components.</span></span> <span data-ttu-id="ee1eb-176">在此情況下，請嘗試從我們的 [媒體檔案輸入] 按一下 [未壓縮的視訊] 輸出接點。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-176">In this case, try clicking on the Uncompressed Video output pin from our Media File Input.</span></span> <span data-ttu-id="ee1eb-177">對話方塊會開啟，讓您檢查輸出視訊。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-177">A dialog will open up that allows to inspect the outbound video.</span></span>

![檢查未壓縮的視訊輸出接點](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-inspecting-uncompressed-video-output.png)

<span data-ttu-id="ee1eb-179">*檢查未壓縮的視訊輸出接點*</span><span class="sxs-lookup"><span data-stu-id="ee1eb-179">*Inspecting the Uncompressed Video output pin*</span></span>

<span data-ttu-id="ee1eb-180">在我們的案例中，它會告訴我們，比方說我們要對一段接近 2 分鐘的視訊，以 4:2:2 取樣每秒 24 個畫面格處理 1920x1080 輸入。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-180">In our case, it tells us for example that we're dealing with a 1920x1080 input at 24 frames per second in 4:2:2 sampling for a video of almost 2 minutes.</span></span>

### <span data-ttu-id="ee1eb-181"><a id="MXF_to_MP4_file_generation"></a>為產生的 MP4 檔案加入視訊編碼器</span><span class="sxs-lookup"><span data-stu-id="ee1eb-181"><a id="MXF_to_MP4_file_generation"></a>Adding a video encoder for .MP4 file generation</span></span>
<span data-ttu-id="ee1eb-182">請注意，現在，[未壓縮的視訊] 和多個 [未壓縮的音訊] 輸出接點可供用於我們的媒體檔案輸入。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-182">Note that now, an Uncompressed Video and multiple Uncompressed Audio output pins are available for use on our Media File Input.</span></span> <span data-ttu-id="ee1eb-183">為了對輸入視訊編碼，我們需要編碼元件 - 在此情況下用於產生 .MP4 檔案。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-183">In order to encode the inbound video, we need an encoding component - in this case for generating .MP4 files.</span></span>

<span data-ttu-id="ee1eb-184">若要將視訊串流編碼成 H.264，請將 AVC 視訊編碼器元件加入至設計工具介面。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-184">To encode the video stream to H.264, add the AVC Video Encoder component to the designer surface.</span></span> <span data-ttu-id="ee1eb-185">此元件會將未壓縮的視訊串流做為輸入，並在其輸出接點上提供 AVC 壓縮視訊串流。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-185">This component takes an uncompress video stream as input and delivers an AVC compressed video stream on its output pin.</span></span>

![未連接的 AVC 編碼器](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-unconnected-avc-encoder.png)

<span data-ttu-id="ee1eb-187">*未連接的 AVC 編碼器*</span><span class="sxs-lookup"><span data-stu-id="ee1eb-187">*Unconnected AVC Encoder*</span></span>

<span data-ttu-id="ee1eb-188">其屬性會決定編碼確切發生的方式。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-188">Its properties determine how the encoding exactly happens.</span></span> <span data-ttu-id="ee1eb-189">讓我們看看一些更重要的設定：</span><span class="sxs-lookup"><span data-stu-id="ee1eb-189">Let's have a look at some of the more important settings:</span></span>

* <span data-ttu-id="ee1eb-190">輸出寬度和輸出高度：這些屬性決定編碼視訊的解析度。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-190">Output width and Output height: these determine the resolution of the encoded video.</span></span> <span data-ttu-id="ee1eb-191">在本例中，我們使用 640x360</span><span class="sxs-lookup"><span data-stu-id="ee1eb-191">In our case let's go with 640x360</span></span>
* <span data-ttu-id="ee1eb-192">畫面格速率：設定為通過時，它只會採用來源畫面格速率，不過可加以覆寫。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-192">Frame Rate: when set to passthrough it will just adopt the source frame rate, it's possible to override this though.</span></span> <span data-ttu-id="ee1eb-193">請注意，這類的畫面格速率轉換並非動作補償。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-193">Note that such framerate conversion is not motion-compensated.</span></span>
* <span data-ttu-id="ee1eb-194">設定檔和層級：這些屬性會決定 AVC 設定檔和層級。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-194">Profile and Level: these determine the AVC profile and level.</span></span> <span data-ttu-id="ee1eb-195">若要便利地取得不同層級和設定檔的詳細資訊，請按一下 [AVC 視訊編碼器] 元件的問號圖示，說明頁面便會顯示有關每個層級的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-195">To conveniently get more information about the different levels and profiles, click the question mark icon on the AVC Video Encoder component and the help page will show more detail about each of the levels.</span></span> <span data-ttu-id="ee1eb-196">在我們的範例中，讓我們對 [主要設定檔] 使用層級 3.2 (預設值)。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-196">For our sample, let's go with Main Profile at level 3.2 (the default).</span></span>
* <span data-ttu-id="ee1eb-197">速率控制模式和位元速率 (kbps)：我們的案例中，我們選擇使用 1200 kbps 常數位元速率 (CBR) 輸出</span><span class="sxs-lookup"><span data-stu-id="ee1eb-197">Rate Control Mode and Bitrate (kbps): in our scenario we opt for a constant bitrate (CBR) output at 1200 kbps</span></span>
* <span data-ttu-id="ee1eb-198">視訊格式：這是關於會寫入至 H.264 串流的 VUI (視訊可用性資訊) (解碼器可能會用來加強顯示，但對正確解碼並非必要的輔助資訊)：</span><span class="sxs-lookup"><span data-stu-id="ee1eb-198">Video Format: this is about the VUI (Video Usability Information) that gets written into the H.264 stream (side information that might be used by a decoder to enhance the display but not essential to correctly decode):</span></span>
* <span data-ttu-id="ee1eb-199">NTSC (一般用於美國或日本，使用 30 fps)</span><span class="sxs-lookup"><span data-stu-id="ee1eb-199">NTSC (typical for US or Japan, using 30 fps)</span></span>
* <span data-ttu-id="ee1eb-200">PAL (一般用於歐洲地區，使用 25 fps)</span><span class="sxs-lookup"><span data-stu-id="ee1eb-200">PAL (typical for Europe, using 25 fps)</span></span>
* <span data-ttu-id="ee1eb-201">GOP 大小模式：針對我們的目的，我們將設定固定的 GOP 大小，主要間隔為 2 秒，並且關閉 GOP。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-201">GOP Size Mode: we'll configure Fixed GOP Size for our purposes with a Key Interval of 2 seconds with Closed GOPs.</span></span> <span data-ttu-id="ee1eb-202">這可確保與 Azure 媒體服務提供的動態封裝的相容性。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-202">This ensures compatibility with the dynamic packaging Azure Media Services provides.</span></span>

<span data-ttu-id="ee1eb-203">若要摘要我們 AVC 編碼器，請將 [未壓縮的視訊] 輸出接點從 [媒體檔案輸入] 元件連接到 [AVC 編碼器] 的 [未壓縮的視訊] 輸入接點。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-203">To feed our AVC encoder, connect the Uncompressed Video output pin from the Media File Input component to the Uncompressed Video input pin from the AVC encoder.</span></span>

![連接的 AVC 編碼器](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-connected-avc-encoder.png)

<span data-ttu-id="ee1eb-205">*連接的 AVC 主要編碼器*</span><span class="sxs-lookup"><span data-stu-id="ee1eb-205">*Connected AVC Main encoder*</span></span>

### <span data-ttu-id="ee1eb-206"><a id="MXF_to_MP4_audio"></a>對音訊串流編碼</span><span class="sxs-lookup"><span data-stu-id="ee1eb-206"><a id="MXF_to_MP4_audio"></a>Encoding the audio stream</span></span>
<span data-ttu-id="ee1eb-207">此時，我們已將視訊編碼，但仍需要壓縮原始未壓縮的音訊串流。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-207">At this point, we have encoded video but the original uncompressed audio stream still needs to be compressed.</span></span> <span data-ttu-id="ee1eb-208">對此，我們會使用 AAC 編碼器 (Dolby) 元件的 AAC 編碼。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-208">For this we'll go with AAC encoding by the AAC Encoder (Dolby) component.</span></span> <span data-ttu-id="ee1eb-209">將它加入至工作流程。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-209">Add it to the workflow.</span></span>

![未連接的 AVC 編碼器](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-unconnected-aac-encoder.png)

<span data-ttu-id="ee1eb-211">*未連接的 AAC 編碼器*</span><span class="sxs-lookup"><span data-stu-id="ee1eb-211">*Unconnected AAC encoder*</span></span>

<span data-ttu-id="ee1eb-212">現在有不相容性：AAC 編碼器只有單一未壓縮音訊輸入接點，而媒體檔案輸入可能會有兩個不同的未壓縮音訊串流可用：一個用於左音訊聲道，一個用於右聲道。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-212">Now there's an incompatibility: there's only a single uncompressed audio input pin from the AAC Encoder while more than likely the Media File Input will have two different uncompressed audio stream available: one for the left audio channel and one for the right.</span></span> <span data-ttu-id="ee1eb-213">(如果您正在處理環繞音效，則是 6 聲道。)因此，不可能直接將音訊從 [媒體檔案輸入] 來源連接至 AAC 音訊編碼器。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-213">(If you're dealing with surround sound, that's 6 channels.) So it's not possible to directly connect the audio from the Media File Input source into the AAC audio encoder.</span></span> <span data-ttu-id="ee1eb-214">AAC 元件預期稱為「交錯」的音訊串流：具有左右聲道並彼此交錯的單一串流。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-214">The AAC component expects a so-called "interleaved" audio stream: a single stream that has both the left and the right channels interleaved with each other.</span></span> <span data-ttu-id="ee1eb-215">一旦我們從來源媒體檔案知道哪一個音訊資料軌在來源中的哪個位置，我們可以使用正確指派的左右喇叭位置來產生這類的交錯音訊串流。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-215">Once we know from our source media file which audio tracks are on what position in the source, we can generate such interleaved audio stream with the correctly assigned speaker positions for left and right.</span></span>

<span data-ttu-id="ee1eb-216">首先，使用者會想要從需要的來源音訊聲道產生交錯的串流。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-216">First one will want to generated an interleaved stream from the required source audio channels.</span></span> <span data-ttu-id="ee1eb-217">音訊串流交錯器元件會為我們處理。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-217">The Audio Stream Interleaver component will handle this for us.</span></span> <span data-ttu-id="ee1eb-218">將它加入至工作流程，並從 [媒體檔案輸入] 將音訊輸出連接到它。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-218">Add it to the workflow and connect the audio outputs from the Media File Input into it.</span></span>

![連接音訊串流交錯器](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-connected-audio-stream-interleaver.png)

<span data-ttu-id="ee1eb-220">*連接音訊串流交錯器*</span><span class="sxs-lookup"><span data-stu-id="ee1eb-220">*Connected Audio Stream Interleaver*</span></span>

<span data-ttu-id="ee1eb-221">既然我們已經有交錯的音訊串流，我們仍未指派左或右喇叭的位置。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-221">Now that we have an interleaved audio stream, we still didn't specify where to assign the left or right speaker positions to.</span></span> <span data-ttu-id="ee1eb-222">為了指定位置，我們可以利用「喇叭位置指定器」。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-222">In order to specify this, we can leverage the Speaker Position Assigner.</span></span>

![加入喇叭位置指定器](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-adding-speaker-position-assigner.png)

<span data-ttu-id="ee1eb-224">*加入喇叭位置指定器*</span><span class="sxs-lookup"><span data-stu-id="ee1eb-224">*Adding a Speaker Position Assigner*</span></span>

<span data-ttu-id="ee1eb-225">設定 [喇叭位置指定器] 以搭配使用透過 [自訂] 編碼器預設過濾器和稱為 "2.0 (L,R)" 的聲道預設的立體聲輸入串流。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-225">Configure the Speaker Position Assigner for use with a stereo input stream through an Encoder Preset Filter of "Custom" and the Channel Preset called "2.0 (L,R)".</span></span> <span data-ttu-id="ee1eb-226">(這會將左喇叭位置指派為聲道 1，右喇叭位置指定為聲道 2。)</span><span class="sxs-lookup"><span data-stu-id="ee1eb-226">(This will assign the left speaker position to channel 1 and the right speaker position to channel 2.)</span></span>

<span data-ttu-id="ee1eb-227">將 [喇叭位置指定器] 的輸出連接到 [AAC 編碼器] 的輸入。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-227">Connect the output of the Speaker Position Assigner to the input of the AAC Encoder.</span></span> <span data-ttu-id="ee1eb-228">然後，告訴 AAC 編碼器使用 "2.0 (L,R)" 聲道預設，讓它知道要將立體聲音訊處理為輸入。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-228">Then, tell the AAC Encoder to work with a "2.0 (L,R)" Channel Preset, so it knows to deal with stereo audio as input.</span></span>

### <span data-ttu-id="ee1eb-229"><a id="MXF_to_MP4_audio_and_fideo"></a>將音訊和視訊串流多工處理為 MP4 容器</span><span class="sxs-lookup"><span data-stu-id="ee1eb-229"><a id="MXF_to_MP4_audio_and_fideo"></a>Multiplexing Audio and Video streams into an MP4 container</span></span>
<span data-ttu-id="ee1eb-230">假設我們有 AVC 編碼的視訊串流和 AAC 編碼的音訊串流，我們可以將兩者擷取為 .MP4 容器。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-230">Given our AVC encoded video stream and our AAC encoded audio stream, we can capture both into an .MP4 container.</span></span> <span data-ttu-id="ee1eb-231">將不同的串流混合為單一串流的程序稱為「多工處理」(multiplexing，或 "muxing")。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-231">The process of mixing different streams into a single one is called "multiplexing" (or "muxing").</span></span> <span data-ttu-id="ee1eb-232">在此情況下，我們正在將音訊及視訊串流交錯到單一一致的 .MP4 封裝。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-232">In this case we're interleaving the audio and the video streams in a single coherent .MP4 package.</span></span> <span data-ttu-id="ee1eb-233">為 .MP4 容器協調此動作的元件稱為 ISO MPEG-4 多工器。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-233">The component that coordinates this for an .MP4 container is called the ISO MPEG-4 Multiplexer.</span></span> <span data-ttu-id="ee1eb-234">將其中一個加入至設計工具介面，並將 AVC 視訊編碼器和 AAC 編碼器連接到其輸入。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-234">Add one to the designer surface and connect both the AVC Video Encoder and the AAC Encoder to its inputs.</span></span>

![連接的 MPEG4 多工器](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-connected-mpeg4-multiplexer.png)

<span data-ttu-id="ee1eb-236">*連接的 MPEG4 多工器*</span><span class="sxs-lookup"><span data-stu-id="ee1eb-236">*Connected MPEG4 Multiplexer*</span></span>

### <span data-ttu-id="ee1eb-237"><a id="MXF_to_MP4_writing_mp4"></a>寫入 MP4 檔案</span><span class="sxs-lookup"><span data-stu-id="ee1eb-237"><a id="MXF_to_MP4_writing_mp4"></a>Writing the MP4 file</span></span>
<span data-ttu-id="ee1eb-238">寫入輸出檔時，會使用「檔案輸出」元件。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-238">When writing an output file, the File Output component is used.</span></span> <span data-ttu-id="ee1eb-239">我們可以將它連接到 ISO MPEG-4 多工器的輸出，讓其輸出寫入至磁碟。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-239">We can connect this to the output of the ISO MPEG-4 Multiplexer so that its output gets written to disk.</span></span> <span data-ttu-id="ee1eb-240">若要這樣做，請將容器 (MPEG-4) 輸出接點連接到 [檔案輸出] 的 [寫入] 輸入接點。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-240">To do this, connect the Container (MPEG-4) output pin to the Write input pin of the File Output.</span></span>

![連接的檔案輸出](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-connected-file-output.png)

<span data-ttu-id="ee1eb-242">*連接的檔案輸出*</span><span class="sxs-lookup"><span data-stu-id="ee1eb-242">*Connected File Output*</span></span>

<span data-ttu-id="ee1eb-243">將使用的檔案名稱取決於檔案屬性。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-243">The filename that will be used is determined by the File property.</span></span> <span data-ttu-id="ee1eb-244">雖然可以將該屬性硬式編碼為特定值，使用者最可能想要改為透過運算式設定它。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-244">While that property can be hardcoded to a given value, most likely one will want to set it through an expression instead.</span></span>

<span data-ttu-id="ee1eb-245">若要讓工作流程透過運算式自動判斷輸出 [檔案名稱] 屬性，請按一下 [檔案名稱] 旁邊的按鈕 (資料夾圖示旁)。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-245">To have the workflow automatically determine the output File name property from an expression, click the buton next to the File name (next to the folder icon).</span></span> <span data-ttu-id="ee1eb-246">從下拉式功能表選取 [運算式]。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-246">From the drop down menu then select "Expression".</span></span> <span data-ttu-id="ee1eb-247">這會顯示運算式編輯器。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-247">This will bring up the expression editor.</span></span> <span data-ttu-id="ee1eb-248">先清除編輯器的內容。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-248">Clear the contents of the editor first.</span></span>

![空白的運算式編輯器](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-empty-expression-editor.png)

<span data-ttu-id="ee1eb-250">*空白的運算式編輯器*</span><span class="sxs-lookup"><span data-stu-id="ee1eb-250">*Empty Expression Editor*</span></span>

<span data-ttu-id="ee1eb-251">運算式編輯器允許以一或多個變數的混合輸入任何常值。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-251">The expression editor allows to enter any literal value, mixed with one or more variables.</span></span> <span data-ttu-id="ee1eb-252">以貨幣符號開頭的變數。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-252">Variables start with a dollar sign.</span></span> <span data-ttu-id="ee1eb-253">當您按下 $ 鍵，編輯器會顯示下拉式清單方塊，其中含有可用變數的選擇。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-253">As you hit the $ key, the editor will show a dropdown box with a choice of available variables.</span></span> <span data-ttu-id="ee1eb-254">在此案例中，我們將使用輸出目錄變數與基礎輸入檔案名稱變數的組合：</span><span class="sxs-lookup"><span data-stu-id="ee1eb-254">In our case we'll use a combination of the output directory variable and the base input file name variable:</span></span>

    ${ROOT_outputWriteDirectory}\\${ROOT_sourceFileBaseName}.MP4

![填入運算式編輯器](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-expression-editor.png)

<span data-ttu-id="ee1eb-256">*填入運算式編輯器*</span><span class="sxs-lookup"><span data-stu-id="ee1eb-256">*Filled out Expression Editor*</span></span>

> [!NOTE]
> <span data-ttu-id="ee1eb-257">若要在 Azure 中查看編碼作業的輸出檔，您必須在運算式編輯器提供值。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-257">In order to see see an output file of your encoding job in Azure, you must provide a value in the expression editor.</span></span>
>
>

<span data-ttu-id="ee1eb-258">當您按 [確定] 確認運算式時，[屬性] 視窗將會預覽在此時間點的檔案屬性所解析的值。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-258">When you confirm the expression by hitting ok, the property window will preview to what value the File property resolves at this point in time.</span></span>

![檔案運算式解析輸出目錄](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-file-expression-resolves-output-dir.png)

<span data-ttu-id="ee1eb-260">*檔案運算式解析輸出目錄*</span><span class="sxs-lookup"><span data-stu-id="ee1eb-260">*File Expression resolves output dir*</span></span>

### <span data-ttu-id="ee1eb-261"><a id="MXF_to_MP4_asset_from_output"></a>從輸出檔案建立媒體服務資產</span><span class="sxs-lookup"><span data-stu-id="ee1eb-261"><a id="MXF_to_MP4_asset_from_output"></a>Creating a Media Services Asset from the output file</span></span>
<span data-ttu-id="ee1eb-262">雖然我們已編寫 MP4 輸出檔，我們仍需要指出此檔案屬於媒體服務會因為執行此工作流程產生的輸出資產。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-262">While we have written an MP4 output file, we still need to indicate that this file belongs to the output asset which media services will generate as a result of executing this workflow.</span></span> <span data-ttu-id="ee1eb-263">在此端，會使用工作流程畫布上的 [輸出檔案/資產] 節點。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-263">To this end, the Output File/Asset node on the workflow canvas is used.</span></span> <span data-ttu-id="ee1eb-264">所有連入到此節點的檔案就會成為產生的 Azure 媒體服務資產的一部分。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-264">All incoming files into this node will make part of the resulting Azure Media Services asset.</span></span>

<span data-ttu-id="ee1eb-265">將 [檔案輸出] 元件連接到 [輸出檔案/資產] 元件以完成工作流程。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-265">Connect the File Output component to the Output File/Asset component to finish the workflow.</span></span>

![工作流程完成](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-finished-workflow.png)

<span data-ttu-id="ee1eb-267">*工作流程完成*</span><span class="sxs-lookup"><span data-stu-id="ee1eb-267">*Finished Workflow*</span></span>

### <span data-ttu-id="ee1eb-268"><a id="MXF_to_MP4_test"></a>在本機測試完成的工作流程</span><span class="sxs-lookup"><span data-stu-id="ee1eb-268"><a id="MXF_to_MP4_test"></a>Test the finished workflow locally</span></span>
<span data-ttu-id="ee1eb-269">若要在本機測試工作流程，請按頂端工具列中的 [播放] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-269">To test the workflow locally, hit the play button in the toolbar at the top.</span></span> <span data-ttu-id="ee1eb-270">當工作流程完成執行時，請檢查設定的輸出資料夾中產生的輸出。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-270">When the workflow finished executing, inspect the output generated in the configured output folder.</span></span> <span data-ttu-id="ee1eb-271">您會看到從 MXF 輸入來源檔案進行編碼完成的 MP4 輸出檔。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-271">You'll see the finished MP4 output file that was encoded from the MXF input source file.</span></span>

## <span data-ttu-id="ee1eb-272"><a id="MXF_to_MP4_with_dyn_packaging"></a>將 MXF 編碼為 MP4 - 多位元速率動態封裝已啟用</span><span class="sxs-lookup"><span data-stu-id="ee1eb-272"><a id="MXF_to_MP4_with_dyn_packaging"></a>Encoding MXF into MP4 - multibitrate dynamic packaging enabled</span></span>
<span data-ttu-id="ee1eb-273">在本逐步解說中，我們將使用來單一 .MXF 輸入檔案 AAC 編碼的音訊來建立一組多位元速率 MP4 檔案。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-273">In this walkthrough we'll create a set of multiple bitrate MP4 files with AAC encoded audio from a single .MXF input file.</span></span>

<span data-ttu-id="ee1eb-274">想要將多位元速率資產輸出用於結合 Azure 媒體服務提供的動態封裝功能時，將需要對每個不同的位元速率與解析度產生多個結合 GOP 的 MP4 檔案。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-274">When a multi-bitrate asset output is desired for use in combination with the Dynamic Packaging features offered by Azure Media Services, multiple GOP-aligned MP4 files of each a different bitrate and resolution will need to be generated.</span></span> <span data-ttu-id="ee1eb-275">若要這樣做， [將 MXF 編碼為單一位元速率 MP4](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4) 逐步解說提供不錯的起點。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-275">To do so, the [Encoding MXF into a single bitrate MP4](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4) walkthrough provides us with a good starting point.</span></span>

![開始工作流程](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-starting-workflow.png)

<span data-ttu-id="ee1eb-277">*開始工作流程*</span><span class="sxs-lookup"><span data-stu-id="ee1eb-277">*Starting Workflow*</span></span>

### <span data-ttu-id="ee1eb-278"><a id="MXF_to_MP4_with_dyn_packaging_more_outputs"></a>加入一或多個其他的 MP4 輸出</span><span class="sxs-lookup"><span data-stu-id="ee1eb-278"><a id="MXF_to_MP4_with_dyn_packaging_more_outputs"></a>Adding one or more additional MP4 outputs</span></span>
<span data-ttu-id="ee1eb-279">我們產生的 Azure 媒體服務資產中的每個 MP4 檔案，將支援不同的位元速率與解析度。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-279">Every MP4 file in our resulting Azure Media Services asset will support a different bitrate and resolution.</span></span> <span data-ttu-id="ee1eb-280">讓我們加入一或多個 MP4 輸出檔案至工作流程。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-280">Let's add one or more MP4 output files to the workflow.</span></span>

<span data-ttu-id="ee1eb-281">若要確定我們使用相同的設定來建立視訊編碼器，最方便的方式是複製現有的 AVC 視訊編碼器，並設定其他解析度及位元速率的組合 (讓我們加入 960x540，每秒 25 個畫面格，2.5 Mbps 的組合)。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-281">To make sure we have all our video encoders created with the same settings, it's most convenient to duplicate the already existing AVC Video Encoder and configure another combination of resolution and bitrate (let's add one of 960 x 540 at 25 frames per second at 2,5 Mbps).</span></span> <span data-ttu-id="ee1eb-282">若要複製現有的編碼器，請在設計工具介面複製貼上。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-282">To duplicate the existing encoder, copy paste it on the designer surface.</span></span>

<span data-ttu-id="ee1eb-283">將 [媒體檔案輸入] 的 [未壓縮的視訊] 輸出接點連接到我們的新 AVC 元件。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-283">Connect the Uncompressed Video output pin of the Media File Input into our new AVC component.</span></span>

![連接第二個 AVC 編碼器](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-second-avc-encoder-connected.png)

<span data-ttu-id="ee1eb-285">*連接第二個 AVC 編碼器*</span><span class="sxs-lookup"><span data-stu-id="ee1eb-285">*Second AVC encoder connected*</span></span>

<span data-ttu-id="ee1eb-286">現在對我們的新 AVC 編碼器採用組態，以 2.5 Mbps 輸出 960x540。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-286">Now adapt the configuration for our new AVC encoder to output 960x540 at 2,5 Mbps.</span></span> <span data-ttu-id="ee1eb-287">(對此使用其屬性 [輸出寬度]、[輸出高度] 和 [位元速率 (kbps)]。)</span><span class="sxs-lookup"><span data-stu-id="ee1eb-287">(Use its properties "Output width", "Output height", and "Bitrate (kbps)" for this.)</span></span>

<span data-ttu-id="ee1eb-288">假設我們想要使用產生的資產搭配 Azure 媒體服務的動態封裝，串流處理端點必須能夠從這些 MP4 檔案產生 HLS/分散的 MP4/DASH 片段，這些片段會以要在不同的位元速率之間切換來獲得單一順暢的連續視訊和音訊體驗的用戶端的方式彼此完全對應。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-288">Given we want to use the resulting asset together with Azure Media Services' dynamic packaging, the streaming endpoint needs to be capable of generating from these MP4 files HLS/Fragmented MP4/DASH fragments that are exactly aligned to each other in a way that clients that are switching between different bitrates get a single smooth continuous video and audio experience.</span></span> <span data-ttu-id="ee1eb-289">為了達到這個目的，我們需要確保兩個 MP4 檔案的 AVC 編碼器與 GOP (「一組圖片」) 大小的屬性設定為 2 秒，您可以透過以下方式完成：</span><span class="sxs-lookup"><span data-stu-id="ee1eb-289">To make that happen, we need to ensure that, in the properties of both AVC encoders the GOP ("group of pictures") size for both MP4 files is set to 2 seconds, which can be done by:</span></span>

* <span data-ttu-id="ee1eb-290">將 GOP 大小模式設定為固定 GOP 大小，以及</span><span class="sxs-lookup"><span data-stu-id="ee1eb-290">setting the GOP Size Mode to Fixed GOP size and</span></span>
* <span data-ttu-id="ee1eb-291">主要畫面格間隔設為兩秒。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-291">the Key Frame Interval to two seconds.</span></span>
* <span data-ttu-id="ee1eb-292">同時將 [GOP IDR 控制] 設為 [關閉 GOP] 以確保所有 GOP 獨立而沒有相依性</span><span class="sxs-lookup"><span data-stu-id="ee1eb-292">also set the GOP IDR Control to Closed GOP to ensure all GOP's are standing on their own without dependencies</span></span>

<span data-ttu-id="ee1eb-293">為了讓您方便了解我們的工作流程，請將第一個 AVC 編碼器重新命名為「AVC 視訊編碼器 640x360 1200 kbps」，將第二個 AVC 編碼器重新命名為「AVC 視訊編碼器 960x540 2500 kbps」。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-293">To make our workflow convenient to understand, rename the first AVC encoder to "AVC Video Encoder 640x360 1200kbps" and the second AVC encoder "AVC Video Encoder 960x540 2500 kbps".</span></span>

<span data-ttu-id="ee1eb-294">現在加入第二個「ISO MPEG-4 多工器」和第二個 [檔案輸出]。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-294">Now add a second ISO MPEG-4 Multiplexer and a second File Output.</span></span> <span data-ttu-id="ee1eb-295">將多工器連接至新的 AVC 編碼器，並確定其輸出導向到 [檔案輸出]。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-295">Connect the multiplexer to the new AVC encoder and make sure its output is directed into the File Output.</span></span> <span data-ttu-id="ee1eb-296">然後將 AAC 音訊編碼器輸出連接至新的多工器輸入。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-296">Then also connect the AAC audio encoder output to the new multiplexer's input.</span></span> <span data-ttu-id="ee1eb-297">接著就可以將 [檔案輸出] 連接至 [輸出檔案/資產] 節點，以將它加入將建立的 [媒體服務資產]。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-297">The File Output in turn can then be connected to the Output File/Asset node to add it to the Media Services Asset that will be created.</span></span>

![連接第二個 Muxer 和檔案輸出](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-second-muxer-file-output-connected.png)

<span data-ttu-id="ee1eb-299">*連接第二個 Muxer 和檔案輸出*</span><span class="sxs-lookup"><span data-stu-id="ee1eb-299">*Second Muxer and File Output connected*</span></span>

<span data-ttu-id="ee1eb-300">為了與 Azure 媒體服務動態封裝的相容性，請將多工器的 [區塊模式] 設定為 GOP 計數或持續時間，並將每個區塊的 GOP 設為 1。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-300">For compatibility with Azure Media Services dynamic packaging, configure the multiplexer's Chunk Mode to GOP count or duration and set the GOPs per chunk to 1.</span></span> <span data-ttu-id="ee1eb-301">(這應該是預設值。)</span><span class="sxs-lookup"><span data-stu-id="ee1eb-301">(This should be the default.)</span></span>

![Muxer 區塊模式](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-muxer-chunk-modes.png)

<span data-ttu-id="ee1eb-303">*Muxer 區塊模式*</span><span class="sxs-lookup"><span data-stu-id="ee1eb-303">*Muxer Chunk Modes*</span></span>

<span data-ttu-id="ee1eb-304">注意：您可以對要加入至資產輸出的任何其他位元速率和解析度組合重複此程序。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-304">Note: you may want to repeat this process for any other bitrate and resolution combinations you want to have added to the asset output.</span></span>

### <span data-ttu-id="ee1eb-305"><a id="MXF_to_MP4_with_dyn_packaging_conf_output_names"></a>設定檔案輸出名稱</span><span class="sxs-lookup"><span data-stu-id="ee1eb-305"><a id="MXF_to_MP4_with_dyn_packaging_conf_output_names"></a>Configuring the file output names</span></span>
<span data-ttu-id="ee1eb-306">我們已將一個以上的單一檔案加入至輸出資產。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-306">We have more than one single file added to the output asset.</span></span> <span data-ttu-id="ee1eb-307">這使得您需要確定每個輸出檔案的檔案名稱會彼此不同，並甚至可能套用檔案命名慣例，使得您能夠從檔案名稱清楚知道要處理的是什麼。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-307">This provides a need to make sure the filenames for each of the output files are different from each other and maybe even apply a file-naming convention so it becomes clear from the file name what you're dealing with.</span></span>

<span data-ttu-id="ee1eb-308">檔案輸出命名可以透過設計工具中的運算式來控制。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-308">File output naming can be controlled through expressions in the designer.</span></span> <span data-ttu-id="ee1eb-309">開啟其中一個 [檔案輸出] 元件的屬性窗格，然後開啟 [檔案屬性] 的運算式編輯器。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-309">Open the property pane for one of the File Output components and open the expression editor for the File property.</span></span> <span data-ttu-id="ee1eb-310">我們的第一個輸出檔是透過下列運算式設定 (請參閱從 [MXF 到單一位元速率 MP4 輸出](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4)的教學課程)：</span><span class="sxs-lookup"><span data-stu-id="ee1eb-310">Our first output file was configured through the following expression (see the tutorial for going from [MXF to a single bitrate MP4 output](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4)):</span></span>

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}.MP4

<span data-ttu-id="ee1eb-311">這表示我們的檔案名稱由兩個變數決定：要寫入的輸出目錄和來源檔案基礎名稱。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-311">This means that our filename is determined by two variables: the output directory to write in and the source file base name.</span></span> <span data-ttu-id="ee1eb-312">前者會在工作流程根目錄上公開為屬性，後者則是由連入的檔案決定。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-312">The former is exposed as a property on the workflow root and the latter is determined by the incoming file.</span></span> <span data-ttu-id="ee1eb-313">請注意，輸出目錄是您用於本機測試的目錄；當 Azure 媒體服務中以雲端為基礎的媒體處理器執行工作流程時，這個屬性會由工作流程引擎覆寫。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-313">Note that the output directory is what you use for local testing; this property will be overridden by the workflow engine when the workflow is executed by the cloud-based media processor in Azure Media Services.</span></span>
<span data-ttu-id="ee1eb-314">若要提供這兩個輸出檔案一致的輸出命名，請將第一個檔案命名運算式變更為：</span><span class="sxs-lookup"><span data-stu-id="ee1eb-314">To give both our output files a consistent output naming, change the first file naming expression to:</span></span>

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_640x360_1.MP4

<span data-ttu-id="ee1eb-315">並將第二個變更為：</span><span class="sxs-lookup"><span data-stu-id="ee1eb-315">and the second to:</span></span>

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_960x540_2.MP4

<span data-ttu-id="ee1eb-316">執行中繼的測試回合，以確定正確產生這兩個 MP4 輸出檔案。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-316">Execute an intermediate test run to make sure both MP4 output files are properly generated.</span></span>

### <span data-ttu-id="ee1eb-317"><a id="MXF_to_MP4_with_dyn_packaging_audio_tracks"></a>加入個別的曲目</span><span class="sxs-lookup"><span data-stu-id="ee1eb-317"><a id="MXF_to_MP4_with_dyn_packaging_audio_tracks"></a>Adding a separate Audio Track</span></span>
<span data-ttu-id="ee1eb-318">如我們稍後所見，產生要隨著我們的 MP4 輸出檔案傳送的 .ism 檔案時，我們也將需要僅限音訊的 MP4 檔案做為調適性串流的曲目。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-318">As we'll see later when we generate an .ism file to go with our MP4 output files, we will also require a audio-only MP4 file as the audio track for our adaptive streaming.</span></span> <span data-ttu-id="ee1eb-319">若要建立此檔案，請將額外的 Muxer 加入至工作流程 (ISO-MPEG-4 多工器)，並 AAC 編碼器的輸出接點與其曲目 1 輸入接點連接。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-319">To create this file, add an additional muxer to the workflow (ISO-MPEG-4 Multiplexer) and connect the AAC encoder's output pin with its input pin for Track 1.</span></span>

![加入音訊 Muxer](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-audio-muxer-added.png)

<span data-ttu-id="ee1eb-321">*加入音訊 Muxer*</span><span class="sxs-lookup"><span data-stu-id="ee1eb-321">*Audio Muxer Added*</span></span>

<span data-ttu-id="ee1eb-322">建立第三個 [檔案輸出] 元件，以從 Muxer 輸出輸出串流，並將檔案命名運算式設定為：</span><span class="sxs-lookup"><span data-stu-id="ee1eb-322">Create a third File Output component to output the outbound stream from the muxer and configure the file naming expression as:</span></span>

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_128kbps_audio.MP4

![音訊 Muxer 建立輸出檔案](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-audio-muxer-creating-file-output.png)

<span data-ttu-id="ee1eb-324">*音訊 Muxer 建立輸出檔案*</span><span class="sxs-lookup"><span data-stu-id="ee1eb-324">*Audio Muxer creating File Output*</span></span>

### <span data-ttu-id="ee1eb-325"><a id="MXF_to_MP4_with_dyn_packaging_ism_file"></a>加入 .ISM SMIL 檔案</span><span class="sxs-lookup"><span data-stu-id="ee1eb-325"><a id="MXF_to_MP4_with_dyn_packaging_ism_file"></a>Adding the .ISM SMIL File</span></span>
<span data-ttu-id="ee1eb-326">為了讓動態封裝能在我們媒體服務資產中結合這兩個 MP4 檔案 (僅限音訊的 MP4) 運作，我們也需要資訊清單檔案 (也稱為 "SMIL" 檔案：同步多媒體整合語言)。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-326">For the dynamic packaging to work in combination with both MP4 files (and the audio-only MP4) in our Media Services asset, we also need a manifest file (also called a "SMIL" file: Synchronized Multimedia Integration Language).</span></span> <span data-ttu-id="ee1eb-327">這個檔案可向 Azure 媒體服務指出哪些 MP4 檔案可供動態封裝，以及要考量進行音訊串流的檔案。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-327">This file indicates to Azure Media Services what MP4 files are available for dynamic packaging and which of those to consider for the audio streaming.</span></span> <span data-ttu-id="ee1eb-328">具有單一的音訊串流之一組 MP4 的一般資訊清單檔看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="ee1eb-328">A typical manifest file for a set of MP4's with a single audio stream looks like this:</span></span>

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

<span data-ttu-id="ee1eb-329">.ism 檔案中包含 switch 陳述式、每個個別 MP4 視訊檔案的參考，此外還有只包含音訊的 MP4 的一個 (或多個) 音訊檔案的參考。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-329">The .ism file contains within a switch statement, a reference to each of the individual MP4 video files and in addition to those also one (or more) audio file references to an MP4 that only contains the audio.</span></span>

<span data-ttu-id="ee1eb-330">為我們的一組 MP4 產生資訊清單檔案，可透過名為「AMS 資訊清單寫入器」的元件完成。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-330">Generating the manifest file for our set of MP4's can be done through a component called the "AMS Manifest Writer".</span></span> <span data-ttu-id="ee1eb-331">若要使用它，請將它拖曳到介面上並將 [寫入完成] 輸出接點從三個 [檔案輸出] 元件連接到 [AMS 資訊清單寫入器] 輸入。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-331">To use it, drag it onto the surface and connect the "Write Complete" output pins from the three File Output components to the AMS Manifest Writer input.</span></span> <span data-ttu-id="ee1eb-332">然後務必將 [AMS 資訊清單寫入器] 的輸出連接到 [輸出檔案/資產]。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-332">Then make sure to connect the output of the AMS Manifest Writer to the Output File/Asset.</span></span>

<span data-ttu-id="ee1eb-333">如同對我們的其他檔案輸出元件，使用運算式來設定 .ism 檔案輸出名稱：</span><span class="sxs-lookup"><span data-stu-id="ee1eb-333">As with our other file output components, configure the .ism file output name with an expression:</span></span>

    ${ROOT_outputWriteDirectory}\\${ROOT_sourceFileBaseName}_manifest.ism

<span data-ttu-id="ee1eb-334">我們完成的工作流程看起來如下：</span><span class="sxs-lookup"><span data-stu-id="ee1eb-334">Our finished workflow looks like the below:</span></span>

![MXF 到多位元速率 MP4 的工作流程完成](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-finished-mxf-to-multibitrate-mp4-workflow.png)

<span data-ttu-id="ee1eb-336">*MXF 到多位元速率 MP4 的工作流程完成*</span><span class="sxs-lookup"><span data-stu-id="ee1eb-336">*Finished MXF to multibitrate MP4 workflow*</span></span>

## <span data-ttu-id="ee1eb-337"><a id="MXF_to__multibitrate_MP4"></a>將 MXF 編碼為多位元速率 MP4 - 增強的藍圖</span><span class="sxs-lookup"><span data-stu-id="ee1eb-337"><a id="MXF_to__multibitrate_MP4"></a>Encoding MXF into multibitrate MP4 - enhanced blueprint</span></span>
<span data-ttu-id="ee1eb-338">在 [前一個工作流程逐步解說](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging) 中，我們已了解單一 MXF 輸入資產如何可以轉換成輸出資產，其具有多位元速率 MP4 檔案、僅限音訊的 MP4 檔案和用於與 Azure 媒體服務動態封裝結合使用的資訊清單檔。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-338">In the [previous workflow walkthrough](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging) we've seen how a single MXF input asset can be converted into an output asset with multi-bitrate MP4 files, an audio-only MP4 file and a manifest file for use in conjunction with Azure Media Services dynamic packaging.</span></span>

<span data-ttu-id="ee1eb-339">此逐步解說將示範如何加強一些層面，並使它更便利。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-339">This walkthrough will show how some of the aspects can be enhanced and made more convenient.</span></span>

### <span data-ttu-id="ee1eb-340"><a id="MXF_to_multibitrate_MP4_overview"></a>要增強的工作流程概觀</span><span class="sxs-lookup"><span data-stu-id="ee1eb-340"><a id="MXF_to_multibitrate_MP4_overview"></a>Workflow overview to enhance</span></span>
![要增強的多位元速率 MP4 工作流程](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-multibitrate-mp4-workflow-to-enhance.png)

<span data-ttu-id="ee1eb-342">*要增強的多位元速率 MP4 工作流程*</span><span class="sxs-lookup"><span data-stu-id="ee1eb-342">*Multibitrate MP4 workflow to enhance*</span></span>

### <span data-ttu-id="ee1eb-343"><a id="MXF_to__multibitrate_MP4_file_naming"></a>檔案命名慣例</span><span class="sxs-lookup"><span data-stu-id="ee1eb-343"><a id="MXF_to__multibitrate_MP4_file_naming"></a>File Naming Conventions</span></span>
<span data-ttu-id="ee1eb-344">在先前的工作流程中，我們已將簡單的運算式指定做為產生輸出檔案名稱的基礎。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-344">In the previous workflow we specified a simple expression as the basis for generating output file names.</span></span> <span data-ttu-id="ee1eb-345">不過，我們有一些重複項目：所有的個別輸出檔案元件都指定了這類運算式。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-345">We have some duplication though: all of the the individual output file components specified such expression.</span></span>

<span data-ttu-id="ee1eb-346">例如，我們的第一個視訊檔案的檔案輸出元件是使用此運算式設定：</span><span class="sxs-lookup"><span data-stu-id="ee1eb-346">For example, our file output component for the first video file is configured with this expression:</span></span>

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_640x360_1.MP4

<span data-ttu-id="ee1eb-347">等候第二個視訊輸出時，我們有如下的運算式：</span><span class="sxs-lookup"><span data-stu-id="ee1eb-347">While for the second output video, we have an expression like:</span></span>

    ${ROOT_outputWriteDirectory}\\${ROOT_sourceFileBaseName}_960x540_2.MP4

<span data-ttu-id="ee1eb-348">如果我們可以移除某些重複項目，並改為使得項目更可以設定，是不是比較清楚、較不容易出錯、更方便？</span><span class="sxs-lookup"><span data-stu-id="ee1eb-348">Wouldn't it be cleaner, less error prone and more convenient if we could remove some of this duplication and make things more configurable instead?</span></span> <span data-ttu-id="ee1eb-349">幸好我們可以：設計工具的運算式功能結合能夠在我們的工作流程根目錄上建立自訂屬性，會讓我們多一層的便利性。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-349">Luckily we can: the designer's expression capabilities in combination with the ability to create custom properties on our workflow root will give us an added layer of convenience.</span></span>

<span data-ttu-id="ee1eb-350">假設我們將從個別 MP4 檔案的位元速率推動檔案名稱的組態。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-350">Let's assume we'll drive filename configuration from the bitrates of the individual MP4 files.</span></span> <span data-ttu-id="ee1eb-351">我們將力求在一個集中位置 (在我們圖形的根目錄) 設定的這些位元速率，將從該位置存取它們，以設定及推動檔案名稱產生。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-351">These bitrates we'll aim to configure in one central place (on the root of our graph), from where they'll be accessed to configure and drive file name generation.</span></span> <span data-ttu-id="ee1eb-352">為了這樣做，我們會從將來自兩個 AVC 編碼器的位元速率屬性發佈到我們的工作流程根目錄開始，使其成為可從根目錄及從 AVC 編碼器存取。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-352">To do this, we start by publishing the bitrate property from both AVC encoders to the root of our workflow, so that it becomes accessible from both the root as well as from the AVC encoders.</span></span> <span data-ttu-id="ee1eb-353">(即使顯示在兩個不同的位置，只有單一的基礎值。)</span><span class="sxs-lookup"><span data-stu-id="ee1eb-353">(Even if displayed in two different spots, there's only one underlying value.)</span></span>

### <span data-ttu-id="ee1eb-354"><a id="MXF_to__multibitrate_MP4_publishing"></a>發佈元件屬性至工作流程根目錄</span><span class="sxs-lookup"><span data-stu-id="ee1eb-354"><a id="MXF_to__multibitrate_MP4_publishing"></a>Publishing component properties onto the workflow root</span></span>
<span data-ttu-id="ee1eb-355">開啟第一個 AVC 編碼器，移至 [位元速率 (kbps)] 屬性，並從下拉式清單中選擇 [發佈]。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-355">Open the first AVC encoder, go to the Bitrate (kbps) property and from the dropdown choose Publish.</span></span>

![發佈位元速率屬性](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-publishing-bitrate-property.png)

<span data-ttu-id="ee1eb-357">*發佈位元速率屬性*</span><span class="sxs-lookup"><span data-stu-id="ee1eb-357">*Publishing the bitrate property*</span></span>

<span data-ttu-id="ee1eb-358">設定 [發佈] 對話方塊，以發佈至我們的工作流程圖形的根目錄，使用發佈的名稱 "video1bitrate" 以及可讀取的顯示名稱「視訊 1 位元速率」。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-358">Configure the publish dialog to publish to the root of our workflow graph, with a published name of "video1bitrate" and a readable display name of "Video 1 Bitrate".</span></span> <span data-ttu-id="ee1eb-359">設定名為「串流處理位元速率」的自訂群組名稱，並按 [發佈]。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-359">Configure a custom group name called "Streaming Bitrates" and hit Publish.</span></span>

![發佈位元速率屬性](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-publishing-dialog-for-bitrate-property.png)

<span data-ttu-id="ee1eb-361">*位元速率屬性的發佈對話方塊*</span><span class="sxs-lookup"><span data-stu-id="ee1eb-361">*Publishing dialog for bitrate property*</span></span>

<span data-ttu-id="ee1eb-362">對第二個 AVC 編碼器的位元速率屬性重複相同的動作，並在相同的自訂群組「串流處理位元速率」中將它命名為 "video2bitrate"，以及顯示名稱「視訊 2 位元速率」。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-362">Repeat the same for the bitrate property of the second AVC encoder and name it "video2bitrate" with a display name of "Video 2 Bitrate", in the same custom group "Streaming Bitrates".</span></span>

<span data-ttu-id="ee1eb-363">如果我們現在檢查工作流程根目錄屬性，就會看到我們的自訂群組顯示這兩個發佈的屬性。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-363">If we now inspect the workflow root properties, we'll see our custom group with the two published properties show up.</span></span> <span data-ttu-id="ee1eb-364">兩個都會反映其各自的 AVC 編碼器位元速率的值。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-364">Both are reflecting the value of their respective AVC encoder bitrate.</span></span>

![工作流程根目錄上發佈的位元速率屬性](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-published-bitrate-props-on-workflow-root.png)

<span data-ttu-id="ee1eb-366">每當我們想要從程式碼或透過運算式存取這些屬性時，我們可以這麼做：</span><span class="sxs-lookup"><span data-stu-id="ee1eb-366">Whenever we want to access these properties from code or from an expression, we can do so like this:</span></span>

* <span data-ttu-id="ee1eb-367">從根目錄下之元件中的內嵌程式碼：node.getPropertyAsString('../video1bitrate',null)</span><span class="sxs-lookup"><span data-stu-id="ee1eb-367">from inline code from a component right below the root: node.getPropertyAsString('../video1bitrate',null)</span></span>
* <span data-ttu-id="ee1eb-368">在運算式內：${ROOT_video1bitrate}</span><span class="sxs-lookup"><span data-stu-id="ee1eb-368">within an expression: ${ROOT_video1bitrate}</span></span>

<span data-ttu-id="ee1eb-369">讓我們透過也在其上發佈我們的曲目位元速率來完成「串流處理位元速率」群組。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-369">Let's complete the "Streaming Bitrates" group by publishing our audio track bitrate on it as well.</span></span> <span data-ttu-id="ee1eb-370">在 AAC 編碼器的屬性內，搜尋「位元速率」設定，並從它旁邊的下拉式清單中選取 [發佈]。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-370">Within the properties of the AAC Encoder, search for the Bitrate setting and select Publish from the dropdown next to it.</span></span> <span data-ttu-id="ee1eb-371">發佈到在我們的自訂群組「串流處理位元速率」內具有名稱 "audio1bitrate" 和顯示名稱「音訊 1 位元速率」的圖形根目錄中。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-371">Publish to the root of the graph with name "audio1bitrate" and display name "Audio 1 Bitrate" within our custom group "Streaming Bitrates".</span></span>

![音訊位元速率的發佈對話方塊](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-publishing-dialog-for-audio-bitrate.png)

<span data-ttu-id="ee1eb-373">*音訊位元速率的發佈對話方塊*</span><span class="sxs-lookup"><span data-stu-id="ee1eb-373">*Publishing dialog for audio bitrate*</span></span>

![在根目錄產生視訊和音訊屬性](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-resulting-video-and-audio-props-on-root.png)

<span data-ttu-id="ee1eb-375">*在根目錄產生視訊和音訊屬性*</span><span class="sxs-lookup"><span data-stu-id="ee1eb-375">*Resulting video and audio props on root*</span></span>

<span data-ttu-id="ee1eb-376">請注意，對這三個值的任何變更也會重新設定並變更所連結 (和發佈來源位置) 的個別元件的值。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-376">Note that changing any of those three values also re-configures and changes the values on the respective components they are linked with (and where published from).</span></span>

### <span data-ttu-id="ee1eb-377"><a id="MXF_to__multibitrate_MP4_output_files"></a>讓產生的輸出檔案名稱依賴發佈的屬性值</span><span class="sxs-lookup"><span data-stu-id="ee1eb-377"><a id="MXF_to__multibitrate_MP4_output_files"></a>Have generated output file names rely on published property values</span></span>
<span data-ttu-id="ee1eb-378">不要對我們產生的檔案名稱進行硬式編碼，我們現在可以在每個「檔案輸出」元件上變更檔案名稱，以仰賴我們剛在圖形根目錄上發佈的運算式屬性。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-378">Instead of hardcoding our generated file names, we can now change our filename expression on each of the File Output components to rely on the bitrate properties we just published on the graph root.</span></span> <span data-ttu-id="ee1eb-379">從我們的第一個檔案輸出開始，尋找檔案屬性，然後編輯運算式，如下：</span><span class="sxs-lookup"><span data-stu-id="ee1eb-379">Starting with our first file output, find the File property and edit the expression like this:</span></span>

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_${ROOT_video1bitrate}kbps.MP4

<span data-ttu-id="ee1eb-380">可以透過在運算式視窗中時按鍵盤上的貨幣符號來存取及輸入此運算式中的不同參數。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-380">The different parameters in this expression can be accessed and entered by hitting the dollar sign on the keyboard while in the expression window.</span></span> <span data-ttu-id="ee1eb-381">其中一個可用的參數是我們稍早發佈的 video1bitrate 屬性。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-381">One of the available parameters is our video1bitrate property which we published earlier.</span></span>

![存取運算式內的參數](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-accessing-parameters-within-an-expression.png)

<span data-ttu-id="ee1eb-383">*存取運算式內的參數*</span><span class="sxs-lookup"><span data-stu-id="ee1eb-383">*Accessing parameters within an expression*</span></span>

<span data-ttu-id="ee1eb-384">對第二個視訊的檔案輸出執行相同的動作：</span><span class="sxs-lookup"><span data-stu-id="ee1eb-384">Do the same for the file output for our second video:</span></span>

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_${ROOT_video2bitrate}kbps.MP4

<span data-ttu-id="ee1eb-385">以及對僅音訊檔案輸出：</span><span class="sxs-lookup"><span data-stu-id="ee1eb-385">and for the audio-only file output:</span></span>

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_${ROOT_audio1bitrate}bps_audio.MP4

<span data-ttu-id="ee1eb-386">如果我們現在變更任何視訊或音訊檔案的位元速率，將重新設定個別的編碼器，而將會對所有項目自動使用以位元速率為基礎的檔案名稱慣例。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-386">If we now change the bitrate for any of the video or audio files, the respective encoder will be reconfigured and the bitrate-based file name convention will be honored all automatic.</span></span>

## <span data-ttu-id="ee1eb-387"><a id="thumbnails_to__multibitrate_MP4"></a>加入縮圖至多位元速率 MP4 輸出</span><span class="sxs-lookup"><span data-stu-id="ee1eb-387"><a id="thumbnails_to__multibitrate_MP4"></a>Adding thumbnails to multibitrate MP4 output</span></span>
<span data-ttu-id="ee1eb-388">從 [透過 MXF 輸入產生多位元速率 MP4 輸出](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging)的工作流程開始，我們現在將尋求將縮圖加入到輸出。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-388">Starting from a workflow that generates [a multibitrate MP4 output from an MXF input](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging), we will now be looking into adding thumbnails to the output.</span></span>

### <span data-ttu-id="ee1eb-389"><a id="thumbnails_to__multibitrate_MP4_overview"></a>要加入縮圖的目標工作流程概觀</span><span class="sxs-lookup"><span data-stu-id="ee1eb-389"><a id="thumbnails_to__multibitrate_MP4_overview"></a>Workflow overview to add thumbnails to</span></span>
![要從中開始的多位元速率 MP4 工作流程](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-multibitrate-mp4-workflow-to-start-from.png)

<span data-ttu-id="ee1eb-391">*要從中開始的多位元速率 MP4 工作流程*</span><span class="sxs-lookup"><span data-stu-id="ee1eb-391">*Multibitrate MP4 workflow to start from*</span></span>

### <span data-ttu-id="ee1eb-392"><a id="thumbnails_to__multibitrate_MP4__with_jpg"></a>加入 JPG 編碼</span><span class="sxs-lookup"><span data-stu-id="ee1eb-392"><a id="thumbnails_to__multibitrate_MP4__with_jpg"></a>Adding JPG Encoding</span></span>
<span data-ttu-id="ee1eb-393">我們的縮圖產生核心會是可以輸出 JPG 檔案的 JPG 編碼器元件。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-393">The heart of our thumbnail generation will be the JPG Encoder component, able to output JPG files.</span></span>

![JPG 編碼器](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-jpg-encoder.png)

<span data-ttu-id="ee1eb-395">*JPG 編碼器*</span><span class="sxs-lookup"><span data-stu-id="ee1eb-395">*JPG Encoder*</span></span>

<span data-ttu-id="ee1eb-396">不過我們無法直接將未壓縮的視訊串流從媒體檔案輸入連接到 JPG 編碼器。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-396">We cannot however directly connect our Uncompressed Video stream from the Media File Input into the JPG encoder.</span></span> <span data-ttu-id="ee1eb-397">相反地，它預期會收到個別的畫面格。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-397">Instead, it expects to be handed individual frames.</span></span> <span data-ttu-id="ee1eb-398">我們可以透過「視訊畫面格閘道」元件執行此動作。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-398">This, we can do through the Video Frame Gate component.</span></span>

![將畫面格閘道連接到 JPG 編碼器](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-connect-frame-gate-to-jpg-encoder.png)

<span data-ttu-id="ee1eb-400">*將畫面格閘道連接到 JPG 編碼器*</span><span class="sxs-lookup"><span data-stu-id="ee1eb-400">*Connecting a frame gate to the JPG encoder*</span></span>

<span data-ttu-id="ee1eb-401">畫面格閘道會每隔許多秒或畫面格執行一次，可讓視訊畫面格傳遞。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-401">The frame gate once every so many seconds or frames allows a video frame to pass.</span></span> <span data-ttu-id="ee1eb-402">它發生的間隔和時間位移可在屬性中設定。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-402">The interval and the time offset with which this happens is configurable in the properties.</span></span>

![視訊畫面格閘道屬性](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-video-frame-gate-properties.png)

<span data-ttu-id="ee1eb-404">*視訊畫面格閘道屬性*</span><span class="sxs-lookup"><span data-stu-id="ee1eb-404">*Video Frame Gate properties*</span></span>

<span data-ttu-id="ee1eb-405">讓我們透過將模式設為時間 (秒) 及間隔設為 60，每隔一分鐘建立縮圖。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-405">Let's create a thumbnail every minute by setting the mode to Time (seconds) and the Interval to 60.</span></span>

### <span data-ttu-id="ee1eb-406"><a id="thumbnails_to__multibitrate_MP4_color_space"></a>處理色彩空間轉換</span><span class="sxs-lookup"><span data-stu-id="ee1eb-406"><a id="thumbnails_to__multibitrate_MP4_color_space"></a>Dealing with Color Space conversion</span></span>
<span data-ttu-id="ee1eb-407">雖然邏輯上可看到畫面格閘道和媒體檔案輸入的未壓縮的視訊接點現在已可連接，如果我們想執行此動作，則會收到警告。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-407">While it would seem logical both Uncompressed Video pins of the frame gate and the Media File Input can now be connected, we would get a warning if we would do so.</span></span>

![輸入色彩空間錯誤](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-input-color-space-error.png)

<span data-ttu-id="ee1eb-409">*輸入色彩空間錯誤*</span><span class="sxs-lookup"><span data-stu-id="ee1eb-409">*Input color space error*</span></span>

<span data-ttu-id="ee1eb-410">這是因為在我們原始原始未壓縮的視訊串流 (來自我們的 MXF) 中，色彩資訊的表示方式與 JPG 編碼器所預期的不同。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-410">This is because the way in which colour information is represented in our original raw uncompressed video stream, coming from our MXF, is different from what the JPG Encoder is expecting.</span></span> <span data-ttu-id="ee1eb-411">更具體來說，預期會流入稱為 "RGB" 或「灰階」的「色彩空間」。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-411">More specifically, a so-called "color space" of "RGB" or "Grayscale" is expected to flow in.</span></span> <span data-ttu-id="ee1eb-412">這表示，視訊畫面格閘道的輸入視訊串流，將需要先套用有關其色彩空間的轉換。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-412">This means that the Video Frame Gate's inbound video stream will need to have a conversion applied regarding its color space first.</span></span>

<span data-ttu-id="ee1eb-413">拖曳到工作流程上的 [色彩空間轉換器 - Intel]，並將它連接到我們的畫面格閘道。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-413">Drag onto the workflow the Color Space Converter - Intel and connect it to our frame gate.</span></span>

![連接色彩空間轉換器](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-connect-color-space-convertor.png)

<span data-ttu-id="ee1eb-415">*連接色彩空間轉換器*</span><span class="sxs-lookup"><span data-stu-id="ee1eb-415">*Connecting a Color Space Convertor*</span></span>

<span data-ttu-id="ee1eb-416">在屬性視窗中，從 [預設] 清單選擇 BGR 24 項目。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-416">In the properties window, pick the BGR 24 entry from the Preset list.</span></span>

### <span data-ttu-id="ee1eb-417"><a id="thumbnails_to__multibitrate_MP4_writing_thumbnails"></a>寫入縮圖</span><span class="sxs-lookup"><span data-stu-id="ee1eb-417"><a id="thumbnails_to__multibitrate_MP4_writing_thumbnails"></a>Writing the thumbnails</span></span>
<span data-ttu-id="ee1eb-418">不同於我們的 MP4 視訊，JPG 編碼器元件會將輸出多個檔案。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-418">Different from our MP4 video's, the JPG Encoder component will output more than one file.</span></span> <span data-ttu-id="ee1eb-419">為了解決這個問題，可以使用「場景搜尋 JPG 檔案寫入器」元件：它會採用傳入的 JPG 縮圖並寫出，每個檔案名稱結尾加上不同的數字。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-419">In order to deal with this, a Scene Search JPG File Writer component can be used: it will take the incoming JPG thumbnails and write them out, each filename being suffixed by a different number.</span></span> <span data-ttu-id="ee1eb-420">(數字通常指出縮圖取自串流中的秒數/單位數。)</span><span class="sxs-lookup"><span data-stu-id="ee1eb-420">(The number typically indicating the number of seconds/units in the stream which the thumbnail was drawn from.)</span></span>

![推出場景搜尋 JPG 檔案寫入器](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-scene-search-jpg-file-writer.png)

<span data-ttu-id="ee1eb-422">*推出場景搜尋 JPG 檔案寫入器*</span><span class="sxs-lookup"><span data-stu-id="ee1eb-422">*Introducing the Scene Search JPG File Writer*</span></span>

<span data-ttu-id="ee1eb-423">使用以下運算式設定輸出資料夾路徑屬性：${ROOT_outputWriteDirectory}</span><span class="sxs-lookup"><span data-stu-id="ee1eb-423">Configure the Output Folder Path property with the expression: ${ROOT_outputWriteDirectory}</span></span>

<span data-ttu-id="ee1eb-424">和使用下列設定檔案名稱前置詞屬性：</span><span class="sxs-lookup"><span data-stu-id="ee1eb-424">and the Filename Prefix property with:</span></span>

    ${ROOT_sourceFileBaseName}_thumb_

<span data-ttu-id="ee1eb-425">前置詞會決定縮圖檔案命名的方式。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-425">The prefix will determine how the thumbnail files are being named.</span></span> <span data-ttu-id="ee1eb-426">它們的前端將會加上數字，指出串流中縮圖的位置。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-426">They will be suffixed with a number indicating the thumb's position in the stream.</span></span>

![場景搜尋 JPG 檔案寫入器屬性](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-scene-search-jpg-file-writer-properties.png)

<span data-ttu-id="ee1eb-428">*場景搜尋 JPG 檔案寫入器屬性*</span><span class="sxs-lookup"><span data-stu-id="ee1eb-428">*Scene Search JPG File Writer properties*</span></span>

<span data-ttu-id="ee1eb-429">將 [場景搜尋 JPG 檔案寫入器] 連接至 [輸出檔案/資產] 節點。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-429">Connect the Scene Search JPG File Writer to the Output File/Asset node.</span></span>

### <span data-ttu-id="ee1eb-430"><a id="thumbnails_to__multibitrate_MP4_errors"></a>偵測工作流程中的錯誤</span><span class="sxs-lookup"><span data-stu-id="ee1eb-430"><a id="thumbnails_to__multibitrate_MP4_errors"></a>Detecting errors in a workflow</span></span>
<span data-ttu-id="ee1eb-431">將色彩空間轉換器的輸入連接到原始未壓縮的視訊輸出。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-431">Connect the input of the color space converter to the raw uncompressed video output.</span></span> <span data-ttu-id="ee1eb-432">現在，對工作流程執行本機測試回合。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-432">Now perform a local test run for the workflow.</span></span> <span data-ttu-id="ee1eb-433">工作流程很可能會突然停止執行，並在發生錯誤之元件上以紅色外框指出：</span><span class="sxs-lookup"><span data-stu-id="ee1eb-433">There's a good chance the workflow will suddenly stop executing and indicate with a red outline on the component that encountered an error:</span></span>

![色彩空間轉換器錯誤](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-color-space-converter-error.png)

<span data-ttu-id="ee1eb-435">*色彩空間轉換器錯誤*</span><span class="sxs-lookup"><span data-stu-id="ee1eb-435">*Color Space Converter error*</span></span>

<span data-ttu-id="ee1eb-436">按一下色彩空間轉換器元件右上角的小型紅色 "E" 圖示，以查看編碼嘗試失敗的原因。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-436">Click the little red "E" icon in the top right corner of the Color Space Converter component to see what's the reason the encoding attempt failed.</span></span>

![色彩空間轉換器錯誤對話方塊](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-color-space-converter-error-dialog.png)

<span data-ttu-id="ee1eb-438">*色彩空間轉換器錯誤對話方塊*</span><span class="sxs-lookup"><span data-stu-id="ee1eb-438">*Color Space Converter error dialog*</span></span>

<span data-ttu-id="ee1eb-439">結果，如您所見，對於我們要求 YUV 到 RGB 的轉換，色彩空間轉換器的傳入色彩空間標準必須為 rec601。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-439">It turns out, as you can see, that the incoming color space standard for the color space converter has to be rec601 for our requested conversion of YUV to RGB.</span></span> <span data-ttu-id="ee1eb-440">顯然我們的串流並未指出它是 rec601。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-440">Apparently our stream doesn't indicate it's rec601.</span></span> <span data-ttu-id="ee1eb-441">(Rec 601 是以數位視訊格式編碼交錯式類比視訊訊號的標準。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-441">(Rec 601 is a standard for encoding interlaced analog video signals in digital video form.</span></span> <span data-ttu-id="ee1eb-442">它會指定涵蓋 720 亮度取樣和每一行 360 色度取樣的作用中區域。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-442">It specifies an active region covering 720 luminance samples and 360 chrominance samples per line.</span></span> <span data-ttu-id="ee1eb-443">色彩編碼系統稱為 YCbCr 4:2:2。)</span><span class="sxs-lookup"><span data-stu-id="ee1eb-443">The color encoding system is known as YCbCr 4:2:2.)</span></span>

<span data-ttu-id="ee1eb-444">為了修正此問題，我們會在串流的中繼資料上指出我們要處理 rec601 內容。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-444">To fix this, we'll indicate on the metadata of our stream that we're dealing with rec601 content.</span></span> <span data-ttu-id="ee1eb-445">若要這樣做，我們將使用「視訊資料類型更新器」元件，我們會將它放在原始來源和色彩空間轉換元件之間。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-445">To do so we'll use a Video Data Type Updater component, which we'll put in between our raw source and the color space conversion component.</span></span> <span data-ttu-id="ee1eb-446">此資料類型的更新器可讓您手動更新特定視訊資料類型屬性。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-446">This data type updater allows for the manual update of certain video data type properties.</span></span> <span data-ttu-id="ee1eb-447">將它設定，以指出 "Rec 601" 的色彩空間標準。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-447">Configure it to indicate a Color Space Standard of "Rec 601".</span></span> <span data-ttu-id="ee1eb-448">在尚未定義色彩空間的情況下，這將導致視訊資料類型更新器以 "Rec 601" 色彩空間標記串流。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-448">This will cause the Video Data Type Updater to tag the stream with the "Rec 601" color space if there was no color space defined yet.</span></span> <span data-ttu-id="ee1eb-449">(它不會覆寫任何現有的中繼資料，除非已勾選 [覆寫] 核取方塊。)</span><span class="sxs-lookup"><span data-stu-id="ee1eb-449">(It will not override any existing metadata, unless the Override checkbox was checked.)</span></span>

![更新資料類型更新程式上的色彩空間標準](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-update-color-space-standard-on-data-type.png)

<span data-ttu-id="ee1eb-451">*更新資料類型更新程式上的色彩空間標準*</span><span class="sxs-lookup"><span data-stu-id="ee1eb-451">*Updating Color Space Standard on the Data Type Updater*</span></span>

### <span data-ttu-id="ee1eb-452"><a id="thumbnails_to__multibitrate_MP4_finish"></a>工作流程完成</span><span class="sxs-lookup"><span data-stu-id="ee1eb-452"><a id="thumbnails_to__multibitrate_MP4_finish"></a>Finished Workflow</span></span>
<span data-ttu-id="ee1eb-453">現在，我們完成了工作流程，接著執行另一個測試回合來查看它傳遞。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-453">Now that our our workflow is finished, do another test run to see it pass.</span></span>

![具有縮圖的多個 mp4 輸出完成的工作流程](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-finished-workflow-for-multi-mp4-thumbnails.png)

<span data-ttu-id="ee1eb-455">*具有縮圖的多個 mp4 輸出完成的工作流程*</span><span class="sxs-lookup"><span data-stu-id="ee1eb-455">*Finished workflow for multi-mp4 output with thumbnails*</span></span>

## <span data-ttu-id="ee1eb-456"><a id="time_based_trim"></a>多位元速率 MP4 輸出以時間為基礎的修剪</span><span class="sxs-lookup"><span data-stu-id="ee1eb-456"><a id="time_based_trim"></a>Time-based trimming of multibitrate MP4 output</span></span>
<span data-ttu-id="ee1eb-457">從 [透過 MXF 輸入產生多位元速率 MP4 輸出](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging)的工作流程開始，我們現在將尋求以時間戳記為基礎修剪來源視訊。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-457">Starting from a workflow that generates [a multibitrate MP4 output from an MXF input](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging), we will now be looking into trimming the source video based on time-stamps.</span></span>

### <span data-ttu-id="ee1eb-458"><a id="time_based_trim_start"></a>要開始加入修剪的目標工作流程概觀</span><span class="sxs-lookup"><span data-stu-id="ee1eb-458"><a id="time_based_trim_start"></a>Workflow overview to start adding trimming to</span></span>
![要加入修剪的目標開始工作流程](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-starting-workflow-to-add-trimming.png)

<span data-ttu-id="ee1eb-460">*要加入修剪的目標開始工作流程*</span><span class="sxs-lookup"><span data-stu-id="ee1eb-460">*Starting workflow to add trimming to*</span></span>

### <span data-ttu-id="ee1eb-461"><a id="time_based_trim_use_stream_trimmer"></a>使用串流修剪器</span><span class="sxs-lookup"><span data-stu-id="ee1eb-461"><a id="time_based_trim_use_stream_trimmer"></a>Using the Stream Trimmer</span></span>
<span data-ttu-id="ee1eb-462">串流修剪器元件允許根據計時資訊 (秒、分等等) 修剪輸入串流的開頭和結尾。修剪器不支援以畫面格為基礎的修剪。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-462">The Stream Trimmer component allows to trim the beginning and ending of an input stream base on timing information (seconds, minutes, ...). The trimmer does not support frame-based trimming.</span></span>

![串流修剪器](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-stream-trimmer.png)

<span data-ttu-id="ee1eb-464">*串流修剪器*</span><span class="sxs-lookup"><span data-stu-id="ee1eb-464">*Stream Trimmer*</span></span>

<span data-ttu-id="ee1eb-465">不要直接將 AVC 編碼器和喇叭位置指定器連結至媒體檔案輸入，我們會將它們放在串流修剪器之間。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-465">Instead of linking the AVC encoders and speaker position assigner to the Media File Input directly, we'll put in between those the stream trimmer.</span></span> <span data-ttu-id="ee1eb-466">(一個用於視訊訊號，一個用於交錯的音訊訊號。)</span><span class="sxs-lookup"><span data-stu-id="ee1eb-466">(One for the video signal and one for the interleaved audio signal.)</span></span>

![在內部放入串流修剪器](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-put-stream-trimmer-in-between.png)

<span data-ttu-id="ee1eb-468">*在內部放入串流修剪器*</span><span class="sxs-lookup"><span data-stu-id="ee1eb-468">*Put Stream Trimmer in between*</span></span>

<span data-ttu-id="ee1eb-469">讓我們設定修剪器，使得我們只會處理 15 秒的視訊和音訊及 60 秒視訊。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-469">Let's configure the trimmer so that we will only process video and audio between 15 seconds and 60 seconds in the video.</span></span>

<span data-ttu-id="ee1eb-470">移至視訊串流修剪器的屬性，並設定開始時間 (15 秒)] 和 [結束時間 (60 秒) 屬性。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-470">Go to the properties of the Video Stream Trimmer and configure both Start Time (15s) and End Time (60s) properties.</span></span> <span data-ttu-id="ee1eb-471">若要確定我們的音訊和視訊修剪器一律會同時設定為相同的開始與結束值，我們會將它們發佈至工作流程根目錄。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-471">To make sure both our audio and video trimmer are always configured to the same start and end values, we will publish those to the root of the workflow.</span></span>

![串流修剪器的發佈開始時間屬性](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-publish-start-time-from-stream-trimmer.png)

<span data-ttu-id="ee1eb-473">*串流修剪器的發佈開始時間屬性*</span><span class="sxs-lookup"><span data-stu-id="ee1eb-473">*Publish start time property from Stream Trimmer*</span></span>

![發佈屬性對話方塊的開始時間](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-publish-dialog-for-start-time.png)

<span data-ttu-id="ee1eb-475">*發佈屬性對話方塊的開始時間*</span><span class="sxs-lookup"><span data-stu-id="ee1eb-475">*Publish property dialog for start time*</span></span>

![發佈屬性對話方塊的結束時間](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-publish-dialog-for-end-time.png)

<span data-ttu-id="ee1eb-477">*發佈屬性對話方塊的結束時間*</span><span class="sxs-lookup"><span data-stu-id="ee1eb-477">*Publish property dialog for end time*</span></span>

<span data-ttu-id="ee1eb-478">如果我們現在檢查我們的工作流程根目錄，這兩個屬性將會整齊地顯示，且可從該處設定。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-478">If we now inspect the root of our workflow, both properties will be neatly displayed and configurable from there.</span></span>

![在根目錄可取得發佈的屬性](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-published-properties-available-on-root.png)

<span data-ttu-id="ee1eb-480">*在根目錄可取得發佈的屬性*</span><span class="sxs-lookup"><span data-stu-id="ee1eb-480">*Published properties available on root*</span></span>

<span data-ttu-id="ee1eb-481">現在從音訊修剪器開啟修剪屬性，並使用參考工作流程根目錄上所發佈屬性的運算式來設定開始和結束時間。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-481">Now open the trimming properties from the audio trimmer and configure both start and end times with an expression that refers to the published properties on the root of our workflow.</span></span>

<span data-ttu-id="ee1eb-482">針對音訊修剪開始時間：</span><span class="sxs-lookup"><span data-stu-id="ee1eb-482">For the audio trimming start time:</span></span>

    ${ROOT_TrimmingStartTime}

<span data-ttu-id="ee1eb-483">和其結束時間：</span><span class="sxs-lookup"><span data-stu-id="ee1eb-483">and for its end time:</span></span>

    ${ROOT_TrimmingEndTime}

### <span data-ttu-id="ee1eb-484"><a id="time_based_trim_finish"></a>工作流程完成</span><span class="sxs-lookup"><span data-stu-id="ee1eb-484"><a id="time_based_trim_finish"></a>Finished Workflow</span></span>
![工作流程完成](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-finished-workflow-time-base-trimming.png)

<span data-ttu-id="ee1eb-486">*工作流程完成*</span><span class="sxs-lookup"><span data-stu-id="ee1eb-486">*Finished Workflow*</span></span>

## <span data-ttu-id="ee1eb-487"><a id="scripting"></a>推出指令碼元件</span><span class="sxs-lookup"><span data-stu-id="ee1eb-487"><a id="scripting"></a>Introducing the Scripted Component</span></span>
<span data-ttu-id="ee1eb-488">指令碼元件可以在我們的工作流程執行階段期間執行任意指令碼。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-488">Scripted Components can execute arbitrary scripts during the execution phases of our workflow.</span></span> <span data-ttu-id="ee1eb-489">有四個可以執行的不同的指令碼，每個都具有特定特性，以及在工作流程生命週期中的位置：</span><span class="sxs-lookup"><span data-stu-id="ee1eb-489">There are four different scripts that can be executed, each with specific characteristics and their own place in the workflow life-cycle:</span></span>

* <span data-ttu-id="ee1eb-490">**commandScript**</span><span class="sxs-lookup"><span data-stu-id="ee1eb-490">**commandScript**</span></span>
* <span data-ttu-id="ee1eb-491">**realizeScript**</span><span class="sxs-lookup"><span data-stu-id="ee1eb-491">**realizeScript**</span></span>
* <span data-ttu-id="ee1eb-492">**processInputScript**</span><span class="sxs-lookup"><span data-stu-id="ee1eb-492">**processInputScript**</span></span>
* <span data-ttu-id="ee1eb-493">**lifeCycleScript**</span><span class="sxs-lookup"><span data-stu-id="ee1eb-493">**lifeCycleScript**</span></span>

<span data-ttu-id="ee1eb-494">指令碼元件的文件會更詳細說明上述各項。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-494">The documentation of the Scripted Component goes in more detail for each of the above.</span></span> <span data-ttu-id="ee1eb-495">在 [下一節](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim)， **realizeScript** 指令碼元件用來在工作流程啟動時快速建構剪輯清單 XML。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-495">In [the following section](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim), the **realizeScript** scripting component is used to construct a cliplist xml on the fly when the workflow starts.</span></span> <span data-ttu-id="ee1eb-496">在元件安裝期間會呼叫此指令碼，這種情況在其生命週期中只會發生一次。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-496">This script is called during the component setup, which happens only once in it's lifecycle.</span></span>

### <span data-ttu-id="ee1eb-497"><a id="scripting_hello_world"></a>工作流程內的指令碼：Hello World</span><span class="sxs-lookup"><span data-stu-id="ee1eb-497"><a id="scripting_hello_world"></a>Scripting within a workflow: hello world</span></span>
<span data-ttu-id="ee1eb-498">將指令碼元件拖曳至設計工具介面上，並重新命名 (例如，"SetClipListXML")。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-498">Drag a Scripted Component onto the designer surface and rename it (for example, "SetClipListXML").</span></span>

![加入指令碼元件](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-add-scripted-comp.png)

<span data-ttu-id="ee1eb-500">*加入指令碼元件*</span><span class="sxs-lookup"><span data-stu-id="ee1eb-500">*Adding a Scripted Component*</span></span>

<span data-ttu-id="ee1eb-501">檢查指令碼元件的屬性時，會顯示四種不同的指令碼類型，而每個可設定到不同的指令碼。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-501">When you inspect the properties of the Scripted Component, the four different script types will be shown, each configurable to a different script.</span></span>

![指令碼元件屬性](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-scripted-comp-properties.png)

<span data-ttu-id="ee1eb-503">*指令碼元件屬性*</span><span class="sxs-lookup"><span data-stu-id="ee1eb-503">*Scripted Component properties*</span></span>

<span data-ttu-id="ee1eb-504">清除 processInputScript，並為 realizeScript 開啟編輯器。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-504">Clear the processInputScript and open the editor for the realizeScript.</span></span> <span data-ttu-id="ee1eb-505">現在我們已設定好並準備要開始指令碼。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-505">Now we're set up and ready to start scripting.</span></span>

<span data-ttu-id="ee1eb-506">指令碼是以 Groovy 編寫，它是 Java 平台適用的動態編譯指令碼語言，其維持與 Java 的相容性。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-506">Scripts are written in Groovy, a dynamically compiled scripting language for the Java platform that retains compatibility with Java.</span></span> <span data-ttu-id="ee1eb-507">事實上，大部分的 Java 程式碼是有效的 Groovy 程式碼。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-507">Actually, most Java code is valid Groovy code.</span></span>

<span data-ttu-id="ee1eb-508">讓我們在 realizeScript 的內容中編寫一個簡單的 Hello World Groovy 指令碼。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-508">Let's write a simple hello world groovy script in the context of our realizeScript.</span></span> <span data-ttu-id="ee1eb-509">在編輯器中輸入下列命令：</span><span class="sxs-lookup"><span data-stu-id="ee1eb-509">Enter the following in the editor:</span></span>

    node.log("hello world");

<span data-ttu-id="ee1eb-510">現在執行本機測試回合。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-510">Now execute a local test run.</span></span> <span data-ttu-id="ee1eb-511">在這項執行之後，(透過 [指令碼元件] 上的 [系統] 索引標籤) 檢查 [記錄] 屬性。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-511">After this run, inspect (through the System tab on the Scripted Component) the Logs property.</span></span>

![Hello World 記錄輸出](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-log-output.png)

<span data-ttu-id="ee1eb-513">*Hello World 記錄輸出*</span><span class="sxs-lookup"><span data-stu-id="ee1eb-513">*Hello world log output*</span></span>

<span data-ttu-id="ee1eb-514">我們呼叫記錄方法所在的節點物件，是指我們目前的「節點」或是我們正在編寫指令碼的元件。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-514">The node object we call the log method on, refers to our current "node" or the component we're scripting within.</span></span> <span data-ttu-id="ee1eb-515">每個元件因此具備可透過系統索引標籤輸出記錄資料的能力。在此情況下，我們會輸出字串常值 "Hello World"。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-515">Every component as such has the ability to output logging data, available through the system tab. In this case, we output the string literal "hello world".</span></span> <span data-ttu-id="ee1eb-516">在此處需要了解的是這可以證明是非常重要的偵錯工具，讓您深入了解指令碼實際上做些什麼。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-516">Important to understand here is that this can prove to be an invaluable debugging tool, providing you with insight on what the script is actually doing.</span></span>

<span data-ttu-id="ee1eb-517">從我們的指令碼環境內，我們也可以存取其他元件的屬性。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-517">From within our scripting environment, we also have access to properties on other components.</span></span> <span data-ttu-id="ee1eb-518">試試看：</span><span class="sxs-lookup"><span data-stu-id="ee1eb-518">Try this:</span></span>

    //inspect current node:
    def nodepath = node.getNodePath();
    node.log("this node path: " + nodepath);

    //walking up to other nodes:
    def parentnode = node.getParentNode();
    def parentnodepath = parentnode.getNodePath();
    node.log("parent node path: " + parentnodepath);

    //read properties from a node:
    def sourceFileExt = parentnode.getPropertyAsString( "sourceFileExtension", null );
    def sourceFileName = parentnode.getPropertyAsString("sourceFileBaseName", null);
    node.log("source file name with extension " + sourceFileExt + " is: " + sourceFileName);

<span data-ttu-id="ee1eb-519">我們的記錄視窗的顯示如下：</span><span class="sxs-lookup"><span data-stu-id="ee1eb-519">Our log window will show us the following:</span></span>

![用於存取節點路徑的記錄輸出](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-log-output2.png)

<span data-ttu-id="ee1eb-521">*用於存取節點路徑的記錄輸出*</span><span class="sxs-lookup"><span data-stu-id="ee1eb-521">*Log output for accessing node paths*</span></span>

## <span data-ttu-id="ee1eb-522"><a id="frame_based_trim"></a>多位元速率 MP4 輸出以畫面格為基礎的修剪</span><span class="sxs-lookup"><span data-stu-id="ee1eb-522"><a id="frame_based_trim"></a>Frame-based trimming of multibitrate MP4 output</span></span>
<span data-ttu-id="ee1eb-523">從 [透過 MXF 輸入產生多位元速率 MP4 輸出](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging)的工作流程開始，我們現在將尋求以畫面格計數為基礎修剪來源視訊。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-523">Starting from a workflow that generates [a multibitrate MP4 output from an MXF input](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging), we will now be looking into trimming the source video based on frame counts.</span></span>

### <span data-ttu-id="ee1eb-524"><a id="frame_based_trim_start"></a>要開始加入修剪的目標藍圖概觀</span><span class="sxs-lookup"><span data-stu-id="ee1eb-524"><a id="frame_based_trim_start"></a>Blueprint overview to start adding trimming to</span></span>
![要開始加入修剪的目標工作流程](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-workflow-start-adding-trimming-to.png)

<span data-ttu-id="ee1eb-526">*要開始加入修剪的目標工作流程*</span><span class="sxs-lookup"><span data-stu-id="ee1eb-526">*Workflow to start adding trimming to*</span></span>

### <span data-ttu-id="ee1eb-527"><a id="frame_based_trim_clip_list"></a>使用剪輯清單 XML</span><span class="sxs-lookup"><span data-stu-id="ee1eb-527"><a id="frame_based_trim_clip_list"></a>Using the Clip List XML</span></span>
<span data-ttu-id="ee1eb-528">在所有先前的工作流程教學課程中，我們使用「媒體檔案輸入」元件做為我們的視訊輸入來源。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-528">In all previous workflow tutorials, we used the Media File Input component as our video input source.</span></span> <span data-ttu-id="ee1eb-529">不過，在此特定案例中，我們將改為使用剪輯清單來源元件。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-529">For this specific scenario though, we'll be using the Clip List Source component instead.</span></span> <span data-ttu-id="ee1eb-530">請注意，這應該不是最好的工作方式；只在有實際原因這麼做時才使用剪輯清單來源 (如同在以下情況下，我們會使用剪輯清單修剪功能)。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-530">Note that this should not be the preferred way of working; only use the Clip List Source when there's a real reason to do so (like in the below case, where we're making use of the clip list trimming capabilities).</span></span>

<span data-ttu-id="ee1eb-531">若要從我們的「媒體檔案輸入」切換到「剪輯清單來源」，請將 [剪輯清單來源] 元件拖曳至設計介面，並將 [剪輯清單 XML] 接點連接至工作流程設計工具的 [剪輯清單 XML] 節點。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-531">To switch from our Media File Input to the Clip List Source, drag the Clip List Source component onto the design surface and connect the Clip List XML pin to the Clip List XML node of the workflow designer.</span></span> <span data-ttu-id="ee1eb-532">這應該會根據我們的輸入視訊，以輸出接點填入剪輯清單來源。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-532">This should populate the Clip List Source with output pins, according to our input video.</span></span> <span data-ttu-id="ee1eb-533">現在，從剪輯清單來源將「未壓縮的視訊」和「未壓縮的音訊」接點連接至相應的「AVC 編碼器」和「音訊串流交錯器」。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-533">Now connect the Uncompressed Video and Uncompressed Audio pins from the the Clip List Source to the respective AVC Encoders and Audio Stream Interleaver.</span></span> <span data-ttu-id="ee1eb-534">現在移除媒體檔案輸入。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-534">Now remove the Media File Input.</span></span>

![以剪輯清單來源取代媒體檔案輸入](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-replaced-media-file-with-clip-source.png)

<span data-ttu-id="ee1eb-536">*以剪輯清單來源取代媒體檔案輸入*</span><span class="sxs-lookup"><span data-stu-id="ee1eb-536">*Replaced the Media File Input with the Clip List Source*</span></span>

<span data-ttu-id="ee1eb-537">剪輯清單來源元件會將它視為輸入「剪輯清單 XML」。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-537">The Clip List Source component takes as its input a "Clip List XML".</span></span> <span data-ttu-id="ee1eb-538">選取要在本機測試的來源檔案，會為您自動填入此剪輯清單 XML。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-538">When selecting the source file to test with locally, this clip list xml is auto-populated for you.</span></span>

![自動填入剪輯清單 XML 屬性](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-auto-populated-clip-list-xml-property.png)

<span data-ttu-id="ee1eb-540">*自動填入剪輯清單 XML 屬性*</span><span class="sxs-lookup"><span data-stu-id="ee1eb-540">*Auto-populated Clip List XML property*</span></span>

<span data-ttu-id="ee1eb-541">更仔細一點觀察 XML，這是其外觀：</span><span class="sxs-lookup"><span data-stu-id="ee1eb-541">Looking a bit closer to the xml, this is how it looks like:</span></span>

![編輯剪輯清單對話方塊](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-edit-clip-list-dialog.png)

<span data-ttu-id="ee1eb-543">*編輯剪輯清單對話方塊*</span><span class="sxs-lookup"><span data-stu-id="ee1eb-543">*Edit clip list dialog*</span></span>

<span data-ttu-id="ee1eb-544">不過這不會反映剪輯清單 XML 的功能。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-544">This however does not reflect the capabilities of the clip list xml.</span></span> <span data-ttu-id="ee1eb-545">我們擁有的其中一個選項是在視訊和音訊來源下加入「修剪」元素，像這樣：</span><span class="sxs-lookup"><span data-stu-id="ee1eb-545">One option we have is to add a "Trim" element under both the video and audio source, like this:</span></span>

![加入修剪元素至剪輯清單](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-adding-trim-element-to-clip-list.png)

<span data-ttu-id="ee1eb-547">*加入修剪元素至剪輯清單*</span><span class="sxs-lookup"><span data-stu-id="ee1eb-547">*Adding a trim element to the clip list*</span></span>

<span data-ttu-id="ee1eb-548">如果您修改類似以上的剪輯清單 XML，並執行本機測試回合，您會看到視訊已正確在視訊中修剪為 10 到 20 秒。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-548">If you modify the clip list xml like this above and perform a local test run, you'll see the video correctly been trimmed between 10 and 20 seconds in the video.</span></span>

<span data-ttu-id="ee1eb-549">不過，相對於當您執行本機執行時發生的情況，在 Azure 媒體服務中執行的工作流程中，這個完全相同的剪輯清單 XML 將不會有相同的效果。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-549">Contrary to what happens when you do a local run though, this very same cliplist xml would not have the same effect when applied in a workflow that runs in Azure Media Services.</span></span> <span data-ttu-id="ee1eb-550">Azure Premium 編碼器啟動時，每次都會根據提供給編碼作業的輸入檔產生剪輯清單 XML。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-550">When Azure Premium Encoder starts, the cliplist xml is generated every time again, based on the input file the encoding job was given.</span></span> <span data-ttu-id="ee1eb-551">這表示，我們在 XML 上執行的任何變更不幸地會被覆寫。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-551">This means that any changes we do on the xml would unfortunately be overridden.</span></span>

<span data-ttu-id="ee1eb-552">若要克服剪輯清單 XML 在編碼作業開始時被抹除，我們可以在工作流程開始之後快速重新產生它。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-552">To counter the cliplist xml being wiped when an encoding job is started, we can re-generate it on the fly just after the start of our workflow.</span></span> <span data-ttu-id="ee1eb-553">透過稱為「指令碼元件」的項目即可以採取這種自訂動作。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-553">Such custom actions can be taken through what is called a "Scripted Component".</span></span> <span data-ttu-id="ee1eb-554">如需詳細資訊，請參閱 [推出指令碼元件](media-services-media-encoder-premium-workflow-tutorials.md#scripting)。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-554">For more information, see [Introducing the Scripted Component](media-services-media-encoder-premium-workflow-tutorials.md#scripting).</span></span>

<span data-ttu-id="ee1eb-555">將指令碼元件拖曳至設計工具介面上，並重新命名為 "SetClipListXML"。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-555">Drag a Scripted Component onto the designer surface and rename it to "SetClipListXML".</span></span>

![加入指令碼元件](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-add-scripted-comp.png)

<span data-ttu-id="ee1eb-557">*加入指令碼元件*</span><span class="sxs-lookup"><span data-stu-id="ee1eb-557">*Adding a Scripted Component*</span></span>

<span data-ttu-id="ee1eb-558">檢查指令碼元件的屬性時，會顯示四種不同的指令碼類型，而每個可設定到不同的指令碼。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-558">When you inspect the properties of the Scripted Component, the four different script types will be shown, each configurable to a different script.</span></span>

![指令碼元件屬性](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-scripted-comp-properties.png)

<span data-ttu-id="ee1eb-560">*指令碼元件屬性*</span><span class="sxs-lookup"><span data-stu-id="ee1eb-560">*Scripted Component properties*</span></span>

### <span data-ttu-id="ee1eb-561"><a id="frame_based_trim_modify_clip_list"></a>透過指令碼元件修改剪輯清單</span><span class="sxs-lookup"><span data-stu-id="ee1eb-561"><a id="frame_based_trim_modify_clip_list"></a>Modifying the clip list from a Scripted Component</span></span>
<span data-ttu-id="ee1eb-562">在我們可以重新寫入工作流程啟動時產生的剪輯清單 XML 之前，我們將需要存取剪輯清單 XML 屬性和內容。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-562">Before we can re-write the cliplist xml that is generated during workflow startup, we'll need to have access to the cliplist xml property and contents.</span></span> <span data-ttu-id="ee1eb-563">我們可以像這樣執行：</span><span class="sxs-lookup"><span data-stu-id="ee1eb-563">We can do so like this:</span></span>

    // get cliplist xml:
    def clipListXML = node.getProperty("../clipListXml");
    node.log("clip list xml coming in: " + clipListXML);

![記錄傳入剪輯清單](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-incoming-clip-list-logged.png)

<span data-ttu-id="ee1eb-565">*記錄傳入剪輯清單*</span><span class="sxs-lookup"><span data-stu-id="ee1eb-565">*Incoming clip list being logged*</span></span>

<span data-ttu-id="ee1eb-566">首先，我們需要決定我們想要修剪視訊的哪一個點到哪一個點。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-566">First we need a way to determine from which point till which point we want to trim the video.</span></span> <span data-ttu-id="ee1eb-567">為了讓它方便工作流程較不具技術性的使用者，請將兩個屬性發佈至圖形的根目錄。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-567">To make this convenient to the less-technical user of the workflow, publish two properties to the root of the graph.</span></span> <span data-ttu-id="ee1eb-568">若要這樣做，請以滑鼠右鍵按一下設計工具介面並選取 [加入屬性]：</span><span class="sxs-lookup"><span data-stu-id="ee1eb-568">To do this, right click the designer surface and select "Add Property":</span></span>

* <span data-ttu-id="ee1eb-569">第一個屬性："ClippingTimeStart"，類型："TIMECODE"</span><span class="sxs-lookup"><span data-stu-id="ee1eb-569">First property: "ClippingTimeStart" of type: "TIMECODE"</span></span>
* <span data-ttu-id="ee1eb-570">第二個屬性："ClippingTimeEnd"，類型："TIMECODE"</span><span class="sxs-lookup"><span data-stu-id="ee1eb-570">Second property: "ClippingTimeEnd" of type: "TIMECODE"</span></span>

![加入屬性對話方塊的剪輯開始時間](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-clip-start-time.png)

<span data-ttu-id="ee1eb-572">*加入屬性對話方塊的剪輯開始時間*</span><span class="sxs-lookup"><span data-stu-id="ee1eb-572">*Add Property dialog for clipping start time*</span></span>

![工作流程根目錄上發佈的剪輯時間屬性](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-clip-time-props.png)

<span data-ttu-id="ee1eb-574">*工作流程根目錄上發佈的剪輯時間屬性*</span><span class="sxs-lookup"><span data-stu-id="ee1eb-574">*Published clipping time props on workflow root*</span></span>

<span data-ttu-id="ee1eb-575">將這兩個屬性設定為適當的值：</span><span class="sxs-lookup"><span data-stu-id="ee1eb-575">Configure both properties to a suitable value:</span></span>

![設定剪輯開始和結束屬性](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-configure-clip-start-end-prop.png)

<span data-ttu-id="ee1eb-577">*設定剪輯開始和結束屬性*</span><span class="sxs-lookup"><span data-stu-id="ee1eb-577">*Configure the clipping start and end properties*</span></span>

<span data-ttu-id="ee1eb-578">現在，從我們的指令碼內，我們就可以存取這兩個屬性，像這樣：</span><span class="sxs-lookup"><span data-stu-id="ee1eb-578">Now, from within our script, we can access both properties, like this:</span></span>

    // get start and end of clipping:
    def clipstart = node.getProperty("../ClippingTimeStart").toString();
    def clipend = node.getProperty("../ClippingTimeEnd").toString();

    node.log("clipping start: " + clipstart);
    node.log("clipping end: " + clipend);

![顯示剪輯的開始與結束的記錄視窗](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-show-start-end-clip.png)

<span data-ttu-id="ee1eb-580">*顯示剪輯的開始與結束的記錄視窗*</span><span class="sxs-lookup"><span data-stu-id="ee1eb-580">*Log window showing start and end of clipping*</span></span>

<span data-ttu-id="ee1eb-581">讓我們使用簡單的規則運算式，將時間碼字串剖析為更方便使用的格式：</span><span class="sxs-lookup"><span data-stu-id="ee1eb-581">Let's parse the timecode strings into a more convenient to use form, using a simple regular expression:</span></span>

    //parse the start timing:
    def startregresult = (~/(\d\d:\d\d:\d\d:\d\d)\/(\d\d)/).matcher(clipstart);
    startregresult.matches();
    def starttimecode = startregresult.group(1);
    node.log("timecode start is: " + starttimecode);
    def startframerate = startregresult.group(2);
    node.log("framerate start is: " + startframerate);

    //parse the end timing:
    def endregresult = (~/(\d\d:\d\d:\d\d:\d\d)\/(\d\d)/).matcher(clipend);
    endregresult.matches();
    def endtimecode = endregresult.group(1);
    node.log("timecode end is: " + endtimecode);
    def endframerate = endregresult.group(2);
    node.log("framerate end is: " + endframerate);

![具有剖析的時間碼輸出的記錄檔視窗](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-output-parsed-timecode.png)

<span data-ttu-id="ee1eb-583">*具有剖析的時間碼輸出的記錄檔視窗*</span><span class="sxs-lookup"><span data-stu-id="ee1eb-583">*Log window with output of parsed timecode*</span></span>

<span data-ttu-id="ee1eb-584">在手邊備有這項資訊，我們現在可以修改剪輯清單 XML 以反映影片所需的畫面格精確剪輯的開始和結束時間。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-584">With this information at hand, we can now modify the cliplist xml to reflect the start and end times for the desired frame-accurate clipping of the movie.</span></span>

![要加入修剪元素的指令碼](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-add-trim-elements.png)

<span data-ttu-id="ee1eb-586">*要加入修剪元素的指令碼*</span><span class="sxs-lookup"><span data-stu-id="ee1eb-586">*Script code to add trim elements*</span></span>

<span data-ttu-id="ee1eb-587">這是透過一般的字串處理作業完成。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-587">This was done through normal string manipulation operations.</span></span> <span data-ttu-id="ee1eb-588">產生的經修改剪輯清單 XML 會透過 "setProperty" 方法寫回工作流程根目錄上的 clipListXML 屬性。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-588">The resulting modified clip list xml is written back to the clipListXML property on the workflow root through the "setProperty" method.</span></span> <span data-ttu-id="ee1eb-589">在另一個測試回合之後記錄視窗會向我們顯示下列：</span><span class="sxs-lookup"><span data-stu-id="ee1eb-589">The log window after another test run would show us the following:</span></span>

![記錄產生的剪輯清單](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-log-result-clip-list.png)

<span data-ttu-id="ee1eb-591">*記錄產生的剪輯清單*</span><span class="sxs-lookup"><span data-stu-id="ee1eb-591">*Logging the resulting clip list*</span></span>

<span data-ttu-id="ee1eb-592">執行測試回合以查看視訊和音訊串流剪輯的情況。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-592">Do a test-run to see how the video and audio streams have been clipped.</span></span> <span data-ttu-id="ee1eb-593">不過，由於您將對修剪點的使用不同值進行多個測試回合，您會發現，這些將不會被納入考量！</span><span class="sxs-lookup"><span data-stu-id="ee1eb-593">As you'll do more than one test-run with different values for the trimming points, you'll notice that those will not be taken into account however!</span></span> <span data-ttu-id="ee1eb-594">這是因為設計工具不同於 Azure 執行階段，不會在每次執行時覆寫剪輯清單 XML。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-594">The reason for this is that the designer, unlike the Azure runtime, does NOT override the cliplist xml every run.</span></span> <span data-ttu-id="ee1eb-595">這就表示，只有在您第一次設定輸入和輸出點時，會導致 XML 轉換，所有其他時候，我們的成立條件子句 (if(clipListXML.indexOf("<trim>") == -1)) 會在一個元素已經存在時避免工作流程加入另一個修剪元素。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-595">This means that only the very first time you have set the in and out points, will cause the xml to transform, all the other times, our guard clause (if(clipListXML.indexOf("<trim>") == -1)) will prevent the workflow from adding another trim element when there's already one present.</span></span>

<span data-ttu-id="ee1eb-596">為了讓工作流程方便在本機測試，我們最好加入一些管理程式碼，其會檢查是否已經存在修剪元素。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-596">To make our workflow convenient to test locally, we best add some house-keeping code that inspects if a trim element was already present.</span></span> <span data-ttu-id="ee1eb-597">如果是的話，我們可以在繼續之前，將 XML 修改為新的值來將它移除。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-597">If so, we can remove it before continuing by modifying the xml with the new values.</span></span> <span data-ttu-id="ee1eb-598">不要使用純文字字串操作，透過實際的 XML 物件模型剖析執行此動作可能更安全。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-598">Rather than using plain string manipulations, it's probably safer to do this through real xml object model parsing.</span></span>

<span data-ttu-id="ee1eb-599">在我們可以加入這類程式碼之前，我們還需要先在指令碼的開頭加入我們一些匯入陳述式：</span><span class="sxs-lookup"><span data-stu-id="ee1eb-599">Before we can add such code though, we'll need to add a number of import statements at the start of our script first:</span></span>

    import javax.xml.parsers.*;
    import org.xml.sax.*;
    import org.w3c.dom.*;
    import javax.xml.*;
    import javax.xml.xpath.*;
    import javax.xml.transform.*;
    import javax.xml.transform.stream.*;
    import javax.xml.transform.dom.*;

<span data-ttu-id="ee1eb-600">在此之後，我們可以加入必要的清除程式碼：</span><span class="sxs-lookup"><span data-stu-id="ee1eb-600">After this, we can add the required cleaning code:</span></span>

    //for local testing: delete any pre-existing trim elements from the clip list xml by parsing the xml into a DOM:
    DocumentBuilderFactory factory=DocumentBuilderFactory.newInstance();
    DocumentBuilder builder=factory.newDocumentBuilder();
    InputSource is=new InputSource(new StringReader(clipListXML));
    Document dom=builder.parse(is);

    //find the trim element inside videoSource and audioSource and remove it if it exists already:
    XPath xpath = XPathFactory.newInstance().newXPath();
    String findAllTrimElements = "//trim";
    NodeList trimelems = xpath.evaluate(findAllTrimElements,dom,XPathConstants.NODESET);

    //copy trim nodes into a "to-be-deleted" collection
    Set<Element> elementsToDelete = new HashSet<Element>();
    for (int i = 0; i < trimelems.getLength(); i++) {
        Element e = (Element)trimelems.item(i);
        elementsToDelete.add(e);
    }

    node.log("about to delete any existing trim nodes");
     //delete the trim nodes:
    elementsToDelete.each{
        e -> e.getParentNode().removeChild(e);
    };
    node.log("deleted any existing trim nodes");

    //serialize the modified clip list xml dom into a string:
    def transformer = TransformerFactory.newInstance().newTransformer();
    StreamResult result = new StreamResult(new StringWriter());
    DOMSource source = new DOMSource(dom);
    transformer.transform(source, result);
    clipListXML = result.getWriter().toString();

<span data-ttu-id="ee1eb-601">這個程式碼會放在我們加入修剪元素至剪輯清單 XML 的點的正上方。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-601">This code goes just above the point at which we add the trim elements to the cliplist xml.</span></span>

<span data-ttu-id="ee1eb-602">此時，只要我們需要，可以在讓變更隨著時間套用時執行及修改工作流程。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-602">At this point, we can run and modify our workflow as much as we want while having the changes applied ever time.</span></span>    

### <span data-ttu-id="ee1eb-603"><a id="frame_based_trim_clippingenabled_prop"></a>加入 ClippingEnabled 便利屬性</span><span class="sxs-lookup"><span data-stu-id="ee1eb-603"><a id="frame_based_trim_clippingenabled_prop"></a>Adding a ClippingEnabled convenience property</span></span>
<span data-ttu-id="ee1eb-604">因為您可能不要一律進行修剪，讓我們透過加入方便的布林值旗標 (可指出是否要啟用修剪/剪輯) 來完成工作流程。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-604">As you might not always want trimming to happen, let's finish off our workflow by adding a convenient boolean flag that indicates whether or not we want to enable trimming / clipping.</span></span>

<span data-ttu-id="ee1eb-605">就像之前，發佈新的屬性到我們稱為 "ClippingEnabled" (類型 "BOOLEAN") 的工作流程根目錄。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-605">Just as before, publish a new property to the root of our workflow called "ClippingEnabled" of type "BOOLEAN".</span></span>

![發佈啟用剪輯屬性](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-enable-clip.png)

<span data-ttu-id="ee1eb-607">*發佈啟用剪輯屬性*</span><span class="sxs-lookup"><span data-stu-id="ee1eb-607">*Published a property for enabling clipping*</span></span>

<span data-ttu-id="ee1eb-608">使用以下簡單的成立條件子句，我們可以檢查是否需要修剪，並決定是否因此需要修改剪輯清單。</span><span class="sxs-lookup"><span data-stu-id="ee1eb-608">With the below simple guard clause, we can check if trimming is required and decide if our clip list as such needs to be modified or not.</span></span>

    //check if clipping is required:
    def clippingrequired = node.getProperty("../ClippingEnabled");
    node.log("clipping required: " + clippingrequired.toString());
    if(clippingrequired == null || clippingrequired == false)
    {
        node.setProperty("../clipListXml",clipListXML);
        node.log("no clipping required");
        return;
    }


### <span data-ttu-id="ee1eb-609"><a id="code"></a>完整程式碼</span><span class="sxs-lookup"><span data-stu-id="ee1eb-609"><a id="code"></a>Complete code</span></span>
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

    //parse the start timing:
    def startregresult = (~/(\d\d:\d\d:\d\d:\d\d)\/(\d\d)/).matcher(clipstart);
    startregresult.matches();
    def starttimecode = startregresult.group(1);
    node.log("timecode start is: " + starttimecode);
    def startframerate = startregresult.group(2);
    node.log("framerate start is: " + startframerate);

    //parse the end timing:
    def endregresult = (~/(\d\d:\d\d:\d\d:\d\d)\/(\d\d)/).matcher(clipend);
    endregresult.matches();
    def endtimecode = endregresult.group(1);
    node.log("timecode end is: " + endtimecode);
    def endframerate = endregresult.group(2);

    node.log("framerate end is: " + endframerate);

    //for local testing: delete any pre-existing trim elements
    //from the clip list xml by parsing the xml into a DOM:

    DocumentBuilderFactory factory=DocumentBuilderFactory.newInstance();
    DocumentBuilder builder=factory.newDocumentBuilder();
    InputSource is=new InputSource(new StringReader(clipListXML));
    Document dom=builder.parse(is);

    //find the trim element inside videoSource and audioSource and remove it if it exists already:
    XPath xpath = XPathFactory.newInstance().newXPath();
    String findAllTrimElements = "//trim";
    NodeList trimelems = xpath.evaluate(findAllTrimElements, dom, XPathConstants.NODESET);

    //copy trim nodes into a "to-be-deleted" collection
    Set<Element> elementsToDelete = new HashSet<Element>();
    for (int i = 0; i < trimelems.getLength(); i++) {
        Element e = (Element)trimelems.item(i);
        elementsToDelete.add(e);
    }

    node.log("about to delete any existing trim nodes");
    //delete the trim nodes:
    elementsToDelete.each{ e ->
        e.getParentNode().removeChild(e);
    };
    node.log("deleted any existing trim nodes");

    //serialize the modified clip list xml dom into a string:
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

    //add trim elements to cliplist xml
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


## <a name="also-see"></a><span data-ttu-id="ee1eb-610">另請參閱</span><span class="sxs-lookup"><span data-stu-id="ee1eb-610">Also see</span></span>
[<span data-ttu-id="ee1eb-611">介紹 Azure 媒體服務中的 Premium 編碼</span><span class="sxs-lookup"><span data-stu-id="ee1eb-611">Introducing Premium Encoding in Azure Media Services</span></span>](http://azure.microsoft.com/blog/2015/03/05/introducing-premium-encoding-in-azure-media-services)

[<span data-ttu-id="ee1eb-612">如何使用 Azure 媒體服務中的 Premium 編碼</span><span class="sxs-lookup"><span data-stu-id="ee1eb-612">How to Use Premium Encoding in Azure Media Services</span></span>](http://azure.microsoft.com/blog/2015/03/06/how-to-use-premium-encoding-in-azure-media-services)

[<span data-ttu-id="ee1eb-613">透過 Azure 媒體服務編碼的隨選內容</span><span class="sxs-lookup"><span data-stu-id="ee1eb-613">Encoding On-Demand Content with Azure Media Service</span></span>](media-services-encode-asset.md#media-encoder-premium-workflow)

[<span data-ttu-id="ee1eb-614">Media Encoder Premium Workflow 格式和轉碼器</span><span class="sxs-lookup"><span data-stu-id="ee1eb-614">Media Encoder Premium Workflow Formats and Codecs</span></span>](media-services-premium-workflow-encoder-formats.md)

[<span data-ttu-id="ee1eb-615">範例工作流程檔案</span><span class="sxs-lookup"><span data-stu-id="ee1eb-615">Sample workflow files</span></span>](http://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows)

[<span data-ttu-id="ee1eb-616">Azure 媒體服務總管工具</span><span class="sxs-lookup"><span data-stu-id="ee1eb-616">Azure Media Services Explorer tool</span></span>](http://aka.ms/amse)

## <a name="media-services-learning-paths"></a><span data-ttu-id="ee1eb-617">媒體服務學習路徑</span><span class="sxs-lookup"><span data-stu-id="ee1eb-617">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="ee1eb-618">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="ee1eb-618">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
