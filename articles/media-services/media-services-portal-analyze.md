---
title: "使用 Azure 入口網站分析您的媒體 | Microsoft Docs"
description: "本主題討論如何使用 Azure 入口網站，以媒體分析媒體處理器 (MP) 處理您的媒體。"
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 18213fc1-74f5-4074-a32b-02846fe90601
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: juliako
ms.openlocfilehash: 22032aef0cc8b7b015503043028873e70c21ee85
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="analyze-your-media-using-the-azure-portal"></a><span data-ttu-id="2959e-103">使用 Azure 入口網站分析您的媒體</span><span class="sxs-lookup"><span data-stu-id="2959e-103">Analyze your media using the Azure portal</span></span>
> [!NOTE]
> <span data-ttu-id="2959e-104">若要完成此教學課程，您需要 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="2959e-104">To complete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="2959e-105">如需詳細資訊，請參閱 [Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="2959e-105">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
> 
> 

## <a name="overview"></a><span data-ttu-id="2959e-106">Overview</span><span class="sxs-lookup"><span data-stu-id="2959e-106">Overview</span></span>
<span data-ttu-id="2959e-107">Azure 媒體服務分析是語音和視覺元件的集合 (具企業規模、相容性、安全性和遍及全球的觸角)，讓組織和企業從其影片檔輕鬆製作出能採取行動的深入見解內容。</span><span class="sxs-lookup"><span data-stu-id="2959e-107">Azure Media Services Analytics is a collection of speech and vision components (at enterprise scale, compliance, security and global reach) that make it easier for organizations and enterprises to derive actionable insights from their video files.</span></span> <span data-ttu-id="2959e-108">如需更為詳細的 Azure 媒體服務分析概觀，請參閱[此主題](media-services-analytics-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="2959e-108">For more detailed overview of Azure Media Services Analytics see [this](media-services-analytics-overview.md) topic.</span></span> 

<span data-ttu-id="2959e-109">本主題討論如何使用 Azure 入口網站，以媒體分析媒體處理器 (MP) 處理您的媒體。</span><span class="sxs-lookup"><span data-stu-id="2959e-109">This topic discusses how to process your media with Media Analytics media processors (MPs) using the Azure portal.</span></span> <span data-ttu-id="2959e-110">媒體分析 MP 會產生 MP4 檔案或 JSON 檔案。</span><span class="sxs-lookup"><span data-stu-id="2959e-110">Media Analytics MPs produce MP4 files or JSON files.</span></span> <span data-ttu-id="2959e-111">如果媒體處理器產生了 MP4 檔案，您可以漸進式下載檔案。</span><span class="sxs-lookup"><span data-stu-id="2959e-111">If a media processor produced an MP4 file, you can progressively download the file.</span></span> <span data-ttu-id="2959e-112">如果媒體處理器產生了 JSON 檔案，您可以從 Azure Blob 儲存體下載檔案。</span><span class="sxs-lookup"><span data-stu-id="2959e-112">If a media processor produced a JSON file, you can download the file from the Azure blob storage.</span></span> 

## <a name="choose-an-asset-that-you-want-to-analyze"></a><span data-ttu-id="2959e-113">選擇您要分析的資產</span><span class="sxs-lookup"><span data-stu-id="2959e-113">Choose an asset that you want to analyze</span></span>
1. <span data-ttu-id="2959e-114">在 [Azure 入口網站](https://portal.azure.com/)中，選取您的 Azure 媒體服務帳戶。</span><span class="sxs-lookup"><span data-stu-id="2959e-114">In the [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="2959e-115">在 [設定] 視窗中，選取 [資產]。</span><span class="sxs-lookup"><span data-stu-id="2959e-115">In the **Settings** window, select **Assets**.</span></span>  
   <span data-ttu-id="2959e-116">。</span><span class="sxs-lookup"><span data-stu-id="2959e-116">.</span></span>
    <span data-ttu-id="2959e-117">![分析影片](./media/media-services-portal-analyze/media-services-portal-analyze001.png)</span><span class="sxs-lookup"><span data-stu-id="2959e-117">![Analyze videos](./media/media-services-portal-analyze/media-services-portal-analyze001.png)</span></span>
3. <span data-ttu-id="2959e-118">選取您要分析的資產，並按下 [分析] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="2959e-118">Select the asset that you would like to analyze and press the **Analyze** button.</span></span>
   
    ![分析影片](./media/media-services-portal-analyze/media-services-portal-analyze002.png)
4. <span data-ttu-id="2959e-120">在 [以媒體分析處理媒體資產] 視窗中，選取處理器。</span><span class="sxs-lookup"><span data-stu-id="2959e-120">In the **Process media asset with  Media Analytics** window, select the processor.</span></span> 
   
    <span data-ttu-id="2959e-121">本文其餘部分會說明各個處理器的使用原因和方式。</span><span class="sxs-lookup"><span data-stu-id="2959e-121">The rest of the article explains why and how to use each processor.</span></span> 
5. <span data-ttu-id="2959e-122">按下 [建立] 來啟動作業。</span><span class="sxs-lookup"><span data-stu-id="2959e-122">Press **Create** to the start a job.</span></span>

## <a name="azure-media-indexer"></a><span data-ttu-id="2959e-123">Azure Media Indexer</span><span class="sxs-lookup"><span data-stu-id="2959e-123">Azure Media Indexer</span></span>
<span data-ttu-id="2959e-124">**Azure 媒體索引器**媒體處理器可讓您將媒體檔案和內容設為可供搜尋，並產生隱藏式輔助字幕追蹤。</span><span class="sxs-lookup"><span data-stu-id="2959e-124">The **Azure Media Indexer** media processor enables you to make media files and content searchable, as well as generate closed captioning tracks.</span></span> <span data-ttu-id="2959e-125">本節會提供一些可為此 MP 指定之選項的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="2959e-125">This sections gives some details about options that you can specify for this MP.</span></span>

![分析影片](./media/media-services-portal-analyze/media-services-portal-analyze003.png)

### <a name="language"></a><span data-ttu-id="2959e-127">語言</span><span class="sxs-lookup"><span data-stu-id="2959e-127">Language</span></span>
<span data-ttu-id="2959e-128">要在多媒體檔案中辨識的自然語言。</span><span class="sxs-lookup"><span data-stu-id="2959e-128">The natural language to be recognized in the multimedia file.</span></span> <span data-ttu-id="2959e-129">例如，英文或西班牙文。</span><span class="sxs-lookup"><span data-stu-id="2959e-129">For example, English or Spanish.</span></span> 

### <a name="captions"></a><span data-ttu-id="2959e-130">標題</span><span class="sxs-lookup"><span data-stu-id="2959e-130">Captions</span></span>
<span data-ttu-id="2959e-131">您可以選擇要從內容產生的標題格式。</span><span class="sxs-lookup"><span data-stu-id="2959e-131">You can choose a caption format that will be generated from your content.</span></span> <span data-ttu-id="2959e-132">索引工作可以產生下列格式的隱藏式輔助字幕檔案：</span><span class="sxs-lookup"><span data-stu-id="2959e-132">An indexing job can generate closed caption files in the following formats:</span></span>  

* <span data-ttu-id="2959e-133">**SAMI**</span><span class="sxs-lookup"><span data-stu-id="2959e-133">**SAMI**</span></span>
* <span data-ttu-id="2959e-134">**TTML**</span><span class="sxs-lookup"><span data-stu-id="2959e-134">**TTML**</span></span>
* <span data-ttu-id="2959e-135">**WebVTT**</span><span class="sxs-lookup"><span data-stu-id="2959e-135">**WebVTT**</span></span>

<span data-ttu-id="2959e-136">這些格式的隱藏式輔助字幕 (CC) 檔案可以用來讓具有聽力障礙的人存取音訊和視訊檔案。</span><span class="sxs-lookup"><span data-stu-id="2959e-136">Closed Caption (CC) files in these formats can be used to make audio and video files accessible to people with hearing disability.</span></span>

### <a name="aib-file"></a><span data-ttu-id="2959e-137">AIB 檔案</span><span class="sxs-lookup"><span data-stu-id="2959e-137">AIB file</span></span>
<span data-ttu-id="2959e-138">如果您想要產生音訊索引 Blob 檔案以便與自訂 SQL Server IFilter 搭配使用，請選取此選項。</span><span class="sxs-lookup"><span data-stu-id="2959e-138">Select this option if you would like to generate the Audio Index Blob file for use with the custom SQL Server IFilter.</span></span> <span data-ttu-id="2959e-139">如需詳細資訊，請參閱 [此部落格](https://azure.microsoft.com/blog/using-aib-files-with-azure-media-indexer-and-sql-server/) 。</span><span class="sxs-lookup"><span data-stu-id="2959e-139">For more information, see [this](https://azure.microsoft.com/blog/using-aib-files-with-azure-media-indexer-and-sql-server/) blog.</span></span>

### <a name="keywords"></a><span data-ttu-id="2959e-140">關鍵字</span><span class="sxs-lookup"><span data-stu-id="2959e-140">Keywords</span></span>
<span data-ttu-id="2959e-141">如果您想要產生關鍵字 XML 檔案，請選取此選項。</span><span class="sxs-lookup"><span data-stu-id="2959e-141">Select this option if you would like to generate a keywords XML file.</span></span> <span data-ttu-id="2959e-142">此檔案包含從語音內容擷取的關鍵字，以及關鍵字的頻率和位移資訊。</span><span class="sxs-lookup"><span data-stu-id="2959e-142">This file contains keywords extracted from the speech content, with frequency and offset information.</span></span>

### <a name="job-name"></a><span data-ttu-id="2959e-143">作業名稱</span><span class="sxs-lookup"><span data-stu-id="2959e-143">Job name</span></span>
<span data-ttu-id="2959e-144">可讓您識別作業的易記名稱。</span><span class="sxs-lookup"><span data-stu-id="2959e-144">A friendly name that lets you identify the job.</span></span> <span data-ttu-id="2959e-145">[本文](media-services-portal-check-job-progress.md)說明如何監視作業進度。</span><span class="sxs-lookup"><span data-stu-id="2959e-145">[This](media-services-portal-check-job-progress.md) article describes how you can monitor the progress of a job.</span></span> 

### <a name="output-file"></a><span data-ttu-id="2959e-146">輸出檔案</span><span class="sxs-lookup"><span data-stu-id="2959e-146">Output file</span></span>
<span data-ttu-id="2959e-147">可讓您識別輸出內容的易記名稱。</span><span class="sxs-lookup"><span data-stu-id="2959e-147">A friendly name that lets you identify the output content.</span></span> 

## <a name="azure-media-hyperlapse"></a><span data-ttu-id="2959e-148">Azure Media Hyperlapse</span><span class="sxs-lookup"><span data-stu-id="2959e-148">Azure Media Hyperlapse</span></span>
<span data-ttu-id="2959e-149">Azure Media Hyperlapse 是能夠利用第一人稱視角或運動攝影的內容，來建立流暢縮時影片的 MP。</span><span class="sxs-lookup"><span data-stu-id="2959e-149">Azure Media Hyperlapse is an MP that creates smooth time-lapsed videos from first-person or action-camera content.</span></span>  <span data-ttu-id="2959e-150">如需詳細資訊，請參閱[此主題](media-services-hyperlapse-content.md)。</span><span class="sxs-lookup"><span data-stu-id="2959e-150">For more information, see [this](media-services-hyperlapse-content.md) topic.</span></span> <span data-ttu-id="2959e-151">本節會提供一些可為此 MP 指定之選項的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="2959e-151">This sections gives some details about options that you can specify for this MP.</span></span>

![分析影片](./media/media-services-portal-analyze/media-services-portal-analyze004.png)

### <a name="speed"></a><span data-ttu-id="2959e-153">速度</span><span class="sxs-lookup"><span data-stu-id="2959e-153">Speed</span></span>
<span data-ttu-id="2959e-154">指定用來讓輸入影片加速的速度。</span><span class="sxs-lookup"><span data-stu-id="2959e-154">Specify the speed with which to speed up the input video.</span></span> <span data-ttu-id="2959e-155">輸出是輸入影片經過穩定和縮時轉譯的成果。</span><span class="sxs-lookup"><span data-stu-id="2959e-155">The output is a stabilized and time-lapsed rendition of the input video.</span></span>

### <a name="job-name"></a><span data-ttu-id="2959e-156">作業名稱</span><span class="sxs-lookup"><span data-stu-id="2959e-156">Job name</span></span>
<span data-ttu-id="2959e-157">可讓您識別作業的易記名稱。</span><span class="sxs-lookup"><span data-stu-id="2959e-157">A friendly name that lets you identify the job.</span></span> <span data-ttu-id="2959e-158">[本文](media-services-portal-check-job-progress.md)說明如何監視作業進度。</span><span class="sxs-lookup"><span data-stu-id="2959e-158">[This](media-services-portal-check-job-progress.md) article describes how you can monitor the progress of a job.</span></span> 

### <a name="output-file"></a><span data-ttu-id="2959e-159">輸出檔案</span><span class="sxs-lookup"><span data-stu-id="2959e-159">Output file</span></span>
<span data-ttu-id="2959e-160">可讓您識別輸出內容的易記名稱。</span><span class="sxs-lookup"><span data-stu-id="2959e-160">A friendly name that lets you identify the output content.</span></span> 

## <a name="azure-media-face-detector"></a><span data-ttu-id="2959e-161">Azure 媒體臉部偵測器</span><span class="sxs-lookup"><span data-stu-id="2959e-161">Azure Media Face Detector</span></span>
<span data-ttu-id="2959e-162">**Azure 媒體臉部偵測器** 媒體處理器 (MP) 能讓您透過臉部表情針對對象的參與情形做出計算、追蹤移動，甚至進行量測。</span><span class="sxs-lookup"><span data-stu-id="2959e-162">The **Azure Media Face Detector** media processor (MP) enables you to count, track movements, and even gauge audience participation and reaction via facial expressions.</span></span> <span data-ttu-id="2959e-163">此服務包含兩個功能：</span><span class="sxs-lookup"><span data-stu-id="2959e-163">This service contains two features:</span></span> 

* <span data-ttu-id="2959e-164">**臉部偵測**</span><span class="sxs-lookup"><span data-stu-id="2959e-164">**Face detection**</span></span>
  
    <span data-ttu-id="2959e-165">臉部偵測能夠找出並追蹤影片中的臉部。</span><span class="sxs-lookup"><span data-stu-id="2959e-165">Face detection finds and tracks human faces within a video.</span></span> <span data-ttu-id="2959e-166">可以同時追蹤多個臉部，隨著對象移動持續進行追蹤，並將時間和位置的中繼資料以 JSON 檔案的格式回傳。</span><span class="sxs-lookup"><span data-stu-id="2959e-166">Multiple faces can be detected and subsequently be tracked as they move around, with the time and location metadata returned in a JSON file.</span></span> <span data-ttu-id="2959e-167">追蹤期間，服務會在人員於螢幕上四處移動時，嘗試為他們的臉部賦予相同的識別碼，就算他們被擋住或暫時離開畫面也一樣。</span><span class="sxs-lookup"><span data-stu-id="2959e-167">During tracking, it will attempt to give a consistent ID to the same face while the person is moving around on screen, even if they are obstructed or briefly leave the frame.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="2959e-168">此服務並不會執行臉部辨識。</span><span class="sxs-lookup"><span data-stu-id="2959e-168">This services does not perform facial recognition.</span></span> <span data-ttu-id="2959e-169">臉部離開畫面或被擋住太久的人員，將會在回來時被賦予新的識別碼。</span><span class="sxs-lookup"><span data-stu-id="2959e-169">An individual who leaves the frame or becomes obstructed for too long will be given a new ID when they return.</span></span>
  > 
  > 
* <span data-ttu-id="2959e-170">**情緒偵測**</span><span class="sxs-lookup"><span data-stu-id="2959e-170">**Emotion detection**</span></span>
  
    <span data-ttu-id="2959e-171">「情緒偵測」是臉部偵測媒體處理器的選擇性元件，它會根據已偵測的臉部，傳回多個情緒屬性的分析，包括快樂、悲傷、恐懼、憤怒等等。</span><span class="sxs-lookup"><span data-stu-id="2959e-171">Emotion Detection is an optional component of the Face Detection Media Processor that returns analysis on multiple emotional attributes from the faces detected, including happiness, sadness, fear, anger, and more.</span></span> 

![分析影片](./media/media-services-portal-analyze/media-services-portal-analyze005.png)

### <a name="detection-mode"></a><span data-ttu-id="2959e-173">偵測模式</span><span class="sxs-lookup"><span data-stu-id="2959e-173">Detection mode</span></span>
<span data-ttu-id="2959e-174">處理器可使用下列其中一個模式︰</span><span class="sxs-lookup"><span data-stu-id="2959e-174">One of the following modes can be used by the processor:</span></span>

* <span data-ttu-id="2959e-175">臉部偵測</span><span class="sxs-lookup"><span data-stu-id="2959e-175">face detection</span></span>
* <span data-ttu-id="2959e-176">每一人臉情緒偵測</span><span class="sxs-lookup"><span data-stu-id="2959e-176">per face emotion detection</span></span>
* <span data-ttu-id="2959e-177">彙總情緒偵測</span><span class="sxs-lookup"><span data-stu-id="2959e-177">aggregate emotion detection</span></span>

### <a name="job-name"></a><span data-ttu-id="2959e-178">作業名稱</span><span class="sxs-lookup"><span data-stu-id="2959e-178">Job name</span></span>
<span data-ttu-id="2959e-179">可讓您識別作業的易記名稱。</span><span class="sxs-lookup"><span data-stu-id="2959e-179">A friendly name that lets you identify the job.</span></span> <span data-ttu-id="2959e-180">[本文](media-services-portal-check-job-progress.md)說明如何監視作業進度。</span><span class="sxs-lookup"><span data-stu-id="2959e-180">[This](media-services-portal-check-job-progress.md) article describes how you can monitor the progress of a job.</span></span> 

### <a name="output-file"></a><span data-ttu-id="2959e-181">輸出檔案</span><span class="sxs-lookup"><span data-stu-id="2959e-181">Output file</span></span>
<span data-ttu-id="2959e-182">可讓您識別輸出內容的易記名稱。</span><span class="sxs-lookup"><span data-stu-id="2959e-182">A friendly name that lets you identify the output content.</span></span> 

## <a name="azure-media-motion-detector"></a><span data-ttu-id="2959e-183">Azure 媒體動作偵測器</span><span class="sxs-lookup"><span data-stu-id="2959e-183">Azure Media Motion Detector</span></span>
<span data-ttu-id="2959e-184">**Azure 媒體動作偵測器** 媒體處理器 (MP) 能讓您在冗長且平淡的影片中，有效識別出感興趣的區段。</span><span class="sxs-lookup"><span data-stu-id="2959e-184">The **Azure Media Motion Detector** media processor (MP) enables you to efficiently identify sections of interest within an otherwise long and uneventful video.</span></span> <span data-ttu-id="2959e-185">動作偵測可以用來在靜態攝影機資料上識別影片中有動作發生的區段。</span><span class="sxs-lookup"><span data-stu-id="2959e-185">Motion detection can be used on static camera footage to identify sections of the video where motion occurs.</span></span> <span data-ttu-id="2959e-186">它會產生 JSON 檔案，其中包含具有時間戳記的中繼資料，以及發生事件的週框區域。</span><span class="sxs-lookup"><span data-stu-id="2959e-186">It generates a JSON file containing a metadata with timestamps and the bounding region where the event occurred.</span></span>

<span data-ttu-id="2959e-187">如果將此技術用於監視器的影片輸出，它將能把動作分類為相關事件及誤判情況 (例如陰影或光源變更)。</span><span class="sxs-lookup"><span data-stu-id="2959e-187">Targeted towards security video feeds, this technology is able to categorize motion into relevant events and false positives such as shadows and lighting changes.</span></span> <span data-ttu-id="2959e-188">這能讓您在不用檢視無止境的不相關事件之下，便能從攝影機輸出產生安全性警示，並從時間相當長的監視影片中擷取感興趣的片段。</span><span class="sxs-lookup"><span data-stu-id="2959e-188">This allows you to generate security alerts from camera feeds without being spammed with endless irrelevant events, while being able to extract moments of interest from extremely long surveillance videos.</span></span>

![分析影片](./media/media-services-portal-analyze/media-services-portal-analyze006.png)

## <a name="azure-media-video-thumbnails"></a><span data-ttu-id="2959e-190">Azure 媒體視訊縮圖</span><span class="sxs-lookup"><span data-stu-id="2959e-190">Azure Media Video Thumbnails</span></span>
<span data-ttu-id="2959e-191">此處理器可自動選取來源視訊的有趣片段，協助您建立較長視訊的摘要。</span><span class="sxs-lookup"><span data-stu-id="2959e-191">This processor can help you create summaries of long videos by automatically selecting interesting snippets from the source video.</span></span> <span data-ttu-id="2959e-192">針對片長較長的視訊，如果您想要提供精彩內容的快速概觀，這非常有用。</span><span class="sxs-lookup"><span data-stu-id="2959e-192">This is useful when you want to provide a quick overview of what to expect in a long video.</span></span> <span data-ttu-id="2959e-193">如需詳細資訊和範例，請參閱 [使用 Azure 媒體視訊縮圖建立視訊摘要](media-services-video-summarization.md)</span><span class="sxs-lookup"><span data-stu-id="2959e-193">For detailed information and examples, see [Use Azure Media Video Thumbnails to Create a Video Summarization](media-services-video-summarization.md)</span></span>

![分析影片](./media/media-services-portal-analyze/media-services-portal-analyze008.png)

### <a name="job-name"></a><span data-ttu-id="2959e-195">作業名稱</span><span class="sxs-lookup"><span data-stu-id="2959e-195">Job name</span></span>
<span data-ttu-id="2959e-196">可讓您識別作業的易記名稱。</span><span class="sxs-lookup"><span data-stu-id="2959e-196">A friendly name that lets you identify the job.</span></span> <span data-ttu-id="2959e-197">[本文](media-services-portal-check-job-progress.md)說明如何監視作業進度。</span><span class="sxs-lookup"><span data-stu-id="2959e-197">[This](media-services-portal-check-job-progress.md) article describes how you can monitor the progress of a job.</span></span> 

### <a name="output-file"></a><span data-ttu-id="2959e-198">輸出檔案</span><span class="sxs-lookup"><span data-stu-id="2959e-198">Output file</span></span>
<span data-ttu-id="2959e-199">可讓您識別輸出內容的易記名稱。</span><span class="sxs-lookup"><span data-stu-id="2959e-199">A friendly name that lets you identify the output content.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="2959e-200">後續步驟</span><span class="sxs-lookup"><span data-stu-id="2959e-200">Next steps</span></span>
<span data-ttu-id="2959e-201">檢視媒體服務學習路徑。</span><span class="sxs-lookup"><span data-stu-id="2959e-201">View Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="2959e-202">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="2959e-202">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

