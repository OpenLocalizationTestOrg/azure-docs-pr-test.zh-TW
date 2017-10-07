---
title: "aaaAnalyze 程式媒體，請使用 hello Azure 入口網站 |Microsoft 文件"
description: "本主題討論如何 tooprocess 媒體分析媒體處理器 (Mp) 使用媒體 hello Azure 入口網站。"
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
ms.openlocfilehash: d549c0315cd58c3771420379316b4f2ad3c2cea6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-your-media-using-hello-azure-portal"></a><span data-ttu-id="2bac7-103">分析您的媒體使用 hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="2bac7-103">Analyze your media using hello Azure portal</span></span>
> [!NOTE]
> <span data-ttu-id="2bac7-104">toocomplete 本教學課程中，您需要 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="2bac7-104">toocomplete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="2bac7-105">如需詳細資料，請參閱 [Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="2bac7-105">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
> 
> 

## <a name="overview"></a><span data-ttu-id="2bac7-106">概觀</span><span class="sxs-lookup"><span data-stu-id="2bac7-106">Overview</span></span>
<span data-ttu-id="2bac7-107">Azure Media Services 分析是語音和願景元件 （企業規模、 相容性、 安全性和全球化） 可讓它更容易組織和企業 tooderive 可執行的洞察力的視訊檔案的集合。</span><span class="sxs-lookup"><span data-stu-id="2bac7-107">Azure Media Services Analytics is a collection of speech and vision components (at enterprise scale, compliance, security and global reach) that make it easier for organizations and enterprises tooderive actionable insights from their video files.</span></span> <span data-ttu-id="2bac7-108">如需更為詳細的 Azure 媒體服務分析概觀，請參閱[此主題](media-services-analytics-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="2bac7-108">For more detailed overview of Azure Media Services Analytics see [this](media-services-analytics-overview.md) topic.</span></span> 

<span data-ttu-id="2bac7-109">本主題討論如何 tooprocess 媒體分析媒體處理器 (Mp) 使用媒體 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="2bac7-109">This topic discusses how tooprocess your media with Media Analytics media processors (MPs) using hello Azure portal.</span></span> <span data-ttu-id="2bac7-110">媒體分析 MP 會產生 MP4 檔案或 JSON 檔案。</span><span class="sxs-lookup"><span data-stu-id="2bac7-110">Media Analytics MPs produce MP4 files or JSON files.</span></span> <span data-ttu-id="2bac7-111">如果媒體處理器所產生的 MP4 檔案，您可以漸進式下載 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="2bac7-111">If a media processor produced an MP4 file, you can progressively download hello file.</span></span> <span data-ttu-id="2bac7-112">如果媒體處理器所產生的 JSON 檔案，您可以從 hello Azure blob 儲存體下載 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="2bac7-112">If a media processor produced a JSON file, you can download hello file from hello Azure blob storage.</span></span> 

## <a name="choose-an-asset-that-you-want-tooanalyze"></a><span data-ttu-id="2bac7-113">選擇 資產的 tooanalyze</span><span class="sxs-lookup"><span data-stu-id="2bac7-113">Choose an asset that you want tooanalyze</span></span>
1. <span data-ttu-id="2bac7-114">在 hello [Azure 入口網站](https://portal.azure.com/)，選取您的 Azure Media Services 帳戶。</span><span class="sxs-lookup"><span data-stu-id="2bac7-114">In hello [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="2bac7-115">在 hello**設定**視窗中，選取**資產**。</span><span class="sxs-lookup"><span data-stu-id="2bac7-115">In hello **Settings** window, select **Assets**.</span></span>  
   <span data-ttu-id="2bac7-116">.</span><span class="sxs-lookup"><span data-stu-id="2bac7-116">.</span></span>
    <span data-ttu-id="2bac7-117">![分析影片](./media/media-services-portal-analyze/media-services-portal-analyze001.png)</span><span class="sxs-lookup"><span data-stu-id="2bac7-117">![Analyze videos](./media/media-services-portal-analyze/media-services-portal-analyze001.png)</span></span>
3. <span data-ttu-id="2bac7-118">您想要選取 hello 資產 tooanalyze 並按下 hello**分析** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="2bac7-118">Select hello asset that you would like tooanalyze and press hello **Analyze** button.</span></span>
   
    ![分析影片](./media/media-services-portal-analyze/media-services-portal-analyze002.png)
4. <span data-ttu-id="2bac7-120">在 hello**媒體分析程序媒體資產**視窗中，選取 hello 處理器。</span><span class="sxs-lookup"><span data-stu-id="2bac7-120">In hello **Process media asset with  Media Analytics** window, select hello processor.</span></span> 
   
    <span data-ttu-id="2bac7-121">hello 文章的 hello 其餘部分說明原因和方式 toouse 每個處理器。</span><span class="sxs-lookup"><span data-stu-id="2bac7-121">hello rest of hello article explains why and how toouse each processor.</span></span> 
5. <span data-ttu-id="2bac7-122">按**建立**toohello 啟動工作。</span><span class="sxs-lookup"><span data-stu-id="2bac7-122">Press **Create** toohello start a job.</span></span>

## <a name="azure-media-indexer"></a><span data-ttu-id="2bac7-123">Azure Media Indexer</span><span class="sxs-lookup"><span data-stu-id="2bac7-123">Azure Media Indexer</span></span>
<span data-ttu-id="2bac7-124">hello **Azure Media Indexer**媒體處理器可讓您 toomake 媒體檔案和內容可搜尋，以及產生已關閉隱藏式輔助字幕追蹤。</span><span class="sxs-lookup"><span data-stu-id="2bac7-124">hello **Azure Media Indexer** media processor enables you toomake media files and content searchable, as well as generate closed captioning tracks.</span></span> <span data-ttu-id="2bac7-125">本節會提供一些可為此 MP 指定之選項的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="2bac7-125">This sections gives some details about options that you can specify for this MP.</span></span>

![分析影片](./media/media-services-portal-analyze/media-services-portal-analyze003.png)

### <a name="language"></a><span data-ttu-id="2bac7-127">語言</span><span class="sxs-lookup"><span data-stu-id="2bac7-127">Language</span></span>
<span data-ttu-id="2bac7-128">hello 自然語言 toobe 辨識 hello 多媒體檔案中。</span><span class="sxs-lookup"><span data-stu-id="2bac7-128">hello natural language toobe recognized in hello multimedia file.</span></span> <span data-ttu-id="2bac7-129">例如，英文或西班牙文。</span><span class="sxs-lookup"><span data-stu-id="2bac7-129">For example, English or Spanish.</span></span> 

### <a name="captions"></a><span data-ttu-id="2bac7-130">標題</span><span class="sxs-lookup"><span data-stu-id="2bac7-130">Captions</span></span>
<span data-ttu-id="2bac7-131">您可以選擇要從內容產生的標題格式。</span><span class="sxs-lookup"><span data-stu-id="2bac7-131">You can choose a caption format that will be generated from your content.</span></span> <span data-ttu-id="2bac7-132">索引作業可以產生隱藏式的字幕檔案在 hello 下列格式：</span><span class="sxs-lookup"><span data-stu-id="2bac7-132">An indexing job can generate closed caption files in hello following formats:</span></span>  

* <span data-ttu-id="2bac7-133">**SAMI**</span><span class="sxs-lookup"><span data-stu-id="2bac7-133">**SAMI**</span></span>
* <span data-ttu-id="2bac7-134">**TTML**</span><span class="sxs-lookup"><span data-stu-id="2bac7-134">**TTML**</span></span>
* <span data-ttu-id="2bac7-135">**WebVTT**</span><span class="sxs-lookup"><span data-stu-id="2bac7-135">**WebVTT**</span></span>

<span data-ttu-id="2bac7-136">已關閉的字幕 (CC) 檔案，這些格式可以是使用的 toomake 音訊和視訊檔案存取 toopeople 聽覺時。</span><span class="sxs-lookup"><span data-stu-id="2bac7-136">Closed Caption (CC) files in these formats can be used toomake audio and video files accessible toopeople with hearing disability.</span></span>

### <a name="aib-file"></a><span data-ttu-id="2bac7-137">AIB 檔案</span><span class="sxs-lookup"><span data-stu-id="2bac7-137">AIB file</span></span>
<span data-ttu-id="2bac7-138">如果您將像是 toogenerate hello 音訊索引 Blob 檔案搭配使用 hello 自訂 SQL Server IFilter，請選取此選項。</span><span class="sxs-lookup"><span data-stu-id="2bac7-138">Select this option if you would like toogenerate hello Audio Index Blob file for use with hello custom SQL Server IFilter.</span></span> <span data-ttu-id="2bac7-139">如需詳細資訊，請參閱 [此部落格](https://azure.microsoft.com/blog/using-aib-files-with-azure-media-indexer-and-sql-server/) 。</span><span class="sxs-lookup"><span data-stu-id="2bac7-139">For more information, see [this](https://azure.microsoft.com/blog/using-aib-files-with-azure-media-indexer-and-sql-server/) blog.</span></span>

### <a name="keywords"></a><span data-ttu-id="2bac7-140">關鍵字</span><span class="sxs-lookup"><span data-stu-id="2bac7-140">Keywords</span></span>
<span data-ttu-id="2bac7-141">如果您想要 toogenerate 關鍵字 XML 檔案，請選取此選項。</span><span class="sxs-lookup"><span data-stu-id="2bac7-141">Select this option if you would like toogenerate a keywords XML file.</span></span> <span data-ttu-id="2bac7-142">這個檔案包含從 hello 語音內容，擷取使用頻率與偏移的資訊的關鍵字。</span><span class="sxs-lookup"><span data-stu-id="2bac7-142">This file contains keywords extracted from hello speech content, with frequency and offset information.</span></span>

### <a name="job-name"></a><span data-ttu-id="2bac7-143">作業名稱</span><span class="sxs-lookup"><span data-stu-id="2bac7-143">Job name</span></span>
<span data-ttu-id="2bac7-144">易記名稱，可讓您識別 hello 工作。</span><span class="sxs-lookup"><span data-stu-id="2bac7-144">A friendly name that lets you identify hello job.</span></span> <span data-ttu-id="2bac7-145">[這](media-services-portal-check-job-progress.md)文章說明如何監視 hello 作業的進度。</span><span class="sxs-lookup"><span data-stu-id="2bac7-145">[This](media-services-portal-check-job-progress.md) article describes how you can monitor hello progress of a job.</span></span> 

### <a name="output-file"></a><span data-ttu-id="2bac7-146">輸出檔案</span><span class="sxs-lookup"><span data-stu-id="2bac7-146">Output file</span></span>
<span data-ttu-id="2bac7-147">易記名稱，可讓您識別 hello 輸出的內容。</span><span class="sxs-lookup"><span data-stu-id="2bac7-147">A friendly name that lets you identify hello output content.</span></span> 

## <a name="azure-media-hyperlapse"></a><span data-ttu-id="2bac7-148">Azure Media Hyperlapse</span><span class="sxs-lookup"><span data-stu-id="2bac7-148">Azure Media Hyperlapse</span></span>
<span data-ttu-id="2bac7-149">Azure Media Hyperlapse 是能夠利用第一人稱視角或運動攝影的內容，來建立流暢縮時影片的 MP。</span><span class="sxs-lookup"><span data-stu-id="2bac7-149">Azure Media Hyperlapse is an MP that creates smooth time-lapsed videos from first-person or action-camera content.</span></span>  <span data-ttu-id="2bac7-150">如需詳細資訊，請參閱[此主題](media-services-hyperlapse-content.md)。</span><span class="sxs-lookup"><span data-stu-id="2bac7-150">For more information, see [this](media-services-hyperlapse-content.md) topic.</span></span> <span data-ttu-id="2bac7-151">本節會提供一些可為此 MP 指定之選項的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="2bac7-151">This sections gives some details about options that you can specify for this MP.</span></span>

![分析影片](./media/media-services-portal-analyze/media-services-portal-analyze004.png)

### <a name="speed"></a><span data-ttu-id="2bac7-153">速度</span><span class="sxs-lookup"><span data-stu-id="2bac7-153">Speed</span></span>
<span data-ttu-id="2bac7-154">指定哪些 toospeed 向上 hello 輸入視訊 hello 速度。</span><span class="sxs-lookup"><span data-stu-id="2bac7-154">Specify hello speed with which toospeed up hello input video.</span></span> <span data-ttu-id="2bac7-155">hello 輸出是 hello 輸入視訊穩定和時間屆滿轉譯。</span><span class="sxs-lookup"><span data-stu-id="2bac7-155">hello output is a stabilized and time-lapsed rendition of hello input video.</span></span>

### <a name="job-name"></a><span data-ttu-id="2bac7-156">作業名稱</span><span class="sxs-lookup"><span data-stu-id="2bac7-156">Job name</span></span>
<span data-ttu-id="2bac7-157">易記名稱，可讓您識別 hello 工作。</span><span class="sxs-lookup"><span data-stu-id="2bac7-157">A friendly name that lets you identify hello job.</span></span> <span data-ttu-id="2bac7-158">[這](media-services-portal-check-job-progress.md)文章說明如何監視 hello 作業的進度。</span><span class="sxs-lookup"><span data-stu-id="2bac7-158">[This](media-services-portal-check-job-progress.md) article describes how you can monitor hello progress of a job.</span></span> 

### <a name="output-file"></a><span data-ttu-id="2bac7-159">輸出檔案</span><span class="sxs-lookup"><span data-stu-id="2bac7-159">Output file</span></span>
<span data-ttu-id="2bac7-160">易記名稱，可讓您識別 hello 輸出的內容。</span><span class="sxs-lookup"><span data-stu-id="2bac7-160">A friendly name that lets you identify hello output content.</span></span> 

## <a name="azure-media-face-detector"></a><span data-ttu-id="2bac7-161">Azure 媒體臉部偵測器</span><span class="sxs-lookup"><span data-stu-id="2bac7-161">Azure Media Face Detector</span></span>
<span data-ttu-id="2bac7-162">hello **Azure 媒體正面偵測器**媒體處理器 (MP) 可讓您 toocount、 軌跡的移動，即使量測計的對象參與以及透過臉部表情的反應。</span><span class="sxs-lookup"><span data-stu-id="2bac7-162">hello **Azure Media Face Detector** media processor (MP) enables you toocount, track movements, and even gauge audience participation and reaction via facial expressions.</span></span> <span data-ttu-id="2bac7-163">此服務包含兩個功能：</span><span class="sxs-lookup"><span data-stu-id="2bac7-163">This service contains two features:</span></span> 

* <span data-ttu-id="2bac7-164">**臉部偵測**</span><span class="sxs-lookup"><span data-stu-id="2bac7-164">**Face detection**</span></span>
  
    <span data-ttu-id="2bac7-165">臉部偵測能夠找出並追蹤影片中的臉部。</span><span class="sxs-lookup"><span data-stu-id="2bac7-165">Face detection finds and tracks human faces within a video.</span></span> <span data-ttu-id="2bac7-166">多個字型可以偵測到且後續追蹤與 hello 時間和位置傳回中繼資料中的 JSON 檔案中，移動。</span><span class="sxs-lookup"><span data-stu-id="2bac7-166">Multiple faces can be detected and subsequently be tracked as they move around, with hello time and location metadata returned in a JSON file.</span></span> <span data-ttu-id="2bac7-167">在追蹤時，它就會嘗試 toogive 一致的識別碼 toohello 相同面臨 hello 人員四處移動在畫面上，即使它們受到阻擋或簡短保留 hello 框架時。</span><span class="sxs-lookup"><span data-stu-id="2bac7-167">During tracking, it will attempt toogive a consistent ID toohello same face while hello person is moving around on screen, even if they are obstructed or briefly leave hello frame.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="2bac7-168">此服務並不會執行臉部辨識。</span><span class="sxs-lookup"><span data-stu-id="2bac7-168">This services does not perform facial recognition.</span></span> <span data-ttu-id="2bac7-169">個人離開 hello 框架，或會變成受到阻擋的時間太長時，會指定新的識別碼，就會傳回。</span><span class="sxs-lookup"><span data-stu-id="2bac7-169">An individual who leaves hello frame or becomes obstructed for too long will be given a new ID when they return.</span></span>
  > 
  > 
* <span data-ttu-id="2bac7-170">**情緒偵測**</span><span class="sxs-lookup"><span data-stu-id="2bac7-170">**Emotion detection**</span></span>
  
    <span data-ttu-id="2bac7-171">情緒偵測作業屬於選擇性元件的 hello 分析多個情感屬性傳回 hello 字體偵測到，包括快樂、 sadness、 擔心、 anger，以及更多的臉偵測媒體處理器。</span><span class="sxs-lookup"><span data-stu-id="2bac7-171">Emotion Detection is an optional component of hello Face Detection Media Processor that returns analysis on multiple emotional attributes from hello faces detected, including happiness, sadness, fear, anger, and more.</span></span> 

![分析影片](./media/media-services-portal-analyze/media-services-portal-analyze005.png)

### <a name="detection-mode"></a><span data-ttu-id="2bac7-173">偵測模式</span><span class="sxs-lookup"><span data-stu-id="2bac7-173">Detection mode</span></span>
<span data-ttu-id="2bac7-174">Hello 處理器，可以使用其中一個 hello 下列模式：</span><span class="sxs-lookup"><span data-stu-id="2bac7-174">One of hello following modes can be used by hello processor:</span></span>

* <span data-ttu-id="2bac7-175">臉部偵測</span><span class="sxs-lookup"><span data-stu-id="2bac7-175">face detection</span></span>
* <span data-ttu-id="2bac7-176">每一人臉情緒偵測</span><span class="sxs-lookup"><span data-stu-id="2bac7-176">per face emotion detection</span></span>
* <span data-ttu-id="2bac7-177">彙總情緒偵測</span><span class="sxs-lookup"><span data-stu-id="2bac7-177">aggregate emotion detection</span></span>

### <a name="job-name"></a><span data-ttu-id="2bac7-178">作業名稱</span><span class="sxs-lookup"><span data-stu-id="2bac7-178">Job name</span></span>
<span data-ttu-id="2bac7-179">易記名稱，可讓您識別 hello 工作。</span><span class="sxs-lookup"><span data-stu-id="2bac7-179">A friendly name that lets you identify hello job.</span></span> <span data-ttu-id="2bac7-180">[這](media-services-portal-check-job-progress.md)文章說明如何監視 hello 作業的進度。</span><span class="sxs-lookup"><span data-stu-id="2bac7-180">[This](media-services-portal-check-job-progress.md) article describes how you can monitor hello progress of a job.</span></span> 

### <a name="output-file"></a><span data-ttu-id="2bac7-181">輸出檔案</span><span class="sxs-lookup"><span data-stu-id="2bac7-181">Output file</span></span>
<span data-ttu-id="2bac7-182">易記名稱，可讓您識別 hello 輸出的內容。</span><span class="sxs-lookup"><span data-stu-id="2bac7-182">A friendly name that lets you identify hello output content.</span></span> 

## <a name="azure-media-motion-detector"></a><span data-ttu-id="2bac7-183">Azure 媒體動作偵測器</span><span class="sxs-lookup"><span data-stu-id="2bac7-183">Azure Media Motion Detector</span></span>
<span data-ttu-id="2bac7-184">hello **Azure 媒體動作偵測器**媒體處理器 (MP) 可讓您 tooefficiently 識別有興趣，否則冗長且較為簡單的視訊中的章節。</span><span class="sxs-lookup"><span data-stu-id="2bac7-184">hello **Azure Media Motion Detector** media processor (MP) enables you tooefficiently identify sections of interest within an otherwise long and uneventful video.</span></span> <span data-ttu-id="2bac7-185">影片偵測可用靜態攝影機錄影畫面 tooidentify 部分的 hello 視訊動作發生的位置。</span><span class="sxs-lookup"><span data-stu-id="2bac7-185">Motion detection can be used on static camera footage tooidentify sections of hello video where motion occurs.</span></span> <span data-ttu-id="2bac7-186">它會產生包含時間戳記與 hello 週框 hello 事件發生的位置 （地區） 的中繼資料的 JSON 檔案。</span><span class="sxs-lookup"><span data-stu-id="2bac7-186">It generates a JSON file containing a metadata with timestamps and hello bounding region where hello event occurred.</span></span>

<span data-ttu-id="2bac7-187">針對安全性視訊摘要，此技術是無法 toocategorize 移動到相關的事件，例如陰影和光源處理變更的誤判。</span><span class="sxs-lookup"><span data-stu-id="2bac7-187">Targeted towards security video feeds, this technology is able toocategorize motion into relevant events and false positives such as shadows and lighting changes.</span></span> <span data-ttu-id="2bac7-188">可以讓您從相機摘要 toogenerate 安全性警示，沒有與無止盡不相關的事件，同時會無法 tooextract 分鐘的時間很長的監視視訊從感興趣的垃圾信件。</span><span class="sxs-lookup"><span data-stu-id="2bac7-188">This allows you toogenerate security alerts from camera feeds without being spammed with endless irrelevant events, while being able tooextract moments of interest from extremely long surveillance videos.</span></span>

![分析影片](./media/media-services-portal-analyze/media-services-portal-analyze006.png)

## <a name="azure-media-video-thumbnails"></a><span data-ttu-id="2bac7-190">Azure 媒體視訊縮圖</span><span class="sxs-lookup"><span data-stu-id="2bac7-190">Azure Media Video Thumbnails</span></span>
<span data-ttu-id="2bac7-191">此處理器可協助您建立自動從 hello 來源視訊中選取感興趣的程式碼片段的較長的視訊摘要。</span><span class="sxs-lookup"><span data-stu-id="2bac7-191">This processor can help you create summaries of long videos by automatically selecting interesting snippets from hello source video.</span></span> <span data-ttu-id="2bac7-192">當您想 tooprovide 哪些 tooexpect 長的視訊中的快速概觀，這非常有用。</span><span class="sxs-lookup"><span data-stu-id="2bac7-192">This is useful when you want tooprovide a quick overview of what tooexpect in a long video.</span></span> <span data-ttu-id="2bac7-193">如需詳細的資訊和範例，請參閱[使用 Azure Media 視訊縮圖 tooCreate 視訊摘要](media-services-video-summarization.md)</span><span class="sxs-lookup"><span data-stu-id="2bac7-193">For detailed information and examples, see [Use Azure Media Video Thumbnails tooCreate a Video Summarization](media-services-video-summarization.md)</span></span>

![分析影片](./media/media-services-portal-analyze/media-services-portal-analyze008.png)

### <a name="job-name"></a><span data-ttu-id="2bac7-195">作業名稱</span><span class="sxs-lookup"><span data-stu-id="2bac7-195">Job name</span></span>
<span data-ttu-id="2bac7-196">易記名稱，可讓您識別 hello 工作。</span><span class="sxs-lookup"><span data-stu-id="2bac7-196">A friendly name that lets you identify hello job.</span></span> <span data-ttu-id="2bac7-197">[這](media-services-portal-check-job-progress.md)文章說明如何監視 hello 作業的進度。</span><span class="sxs-lookup"><span data-stu-id="2bac7-197">[This](media-services-portal-check-job-progress.md) article describes how you can monitor hello progress of a job.</span></span> 

### <a name="output-file"></a><span data-ttu-id="2bac7-198">輸出檔案</span><span class="sxs-lookup"><span data-stu-id="2bac7-198">Output file</span></span>
<span data-ttu-id="2bac7-199">易記名稱，可讓您識別 hello 輸出的內容。</span><span class="sxs-lookup"><span data-stu-id="2bac7-199">A friendly name that lets you identify hello output content.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="2bac7-200">後續步驟</span><span class="sxs-lookup"><span data-stu-id="2bac7-200">Next steps</span></span>
<span data-ttu-id="2bac7-201">檢視媒體服務學習路徑。</span><span class="sxs-lookup"><span data-stu-id="2bac7-201">View Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="2bac7-202">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="2bac7-202">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

