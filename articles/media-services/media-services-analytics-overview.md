---
title: "hello Media Services 平台上的分析 aaaMedia |Microsoft 文件"
description: "媒體分析公開預覽、企業規模的語音和電腦視覺服務集合、相容性、安全性和遍及全球的觸角概觀"
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: c56e3781-8510-4f7f-b5ff-a218c1bb6f4c
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 06/29/2017
ms.author: milanga;juliako;johndeu
ms.openlocfilehash: 7545f0532d7618164ebe65e2f4232c5f63453cfd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="media-analytics-on-hello-media-services-platform"></a><span data-ttu-id="e5237-103">Hello Media Services 平台上的媒體分析</span><span class="sxs-lookup"><span data-stu-id="e5237-103">Media Analytics on hello Media Services platform</span></span>
## <a name="overview"></a><span data-ttu-id="e5237-104">概觀</span><span class="sxs-lookup"><span data-stu-id="e5237-104">Overview</span></span>
<span data-ttu-id="e5237-105">多個組織會使用視訊做為 hello 慣用中型 tootrain 員工、 客戶，與文件商務功能中進行。</span><span class="sxs-lookup"><span data-stu-id="e5237-105">More organizations are using video as hello preferred medium tootrain their employees, engage their customers, and document business functions.</span></span> <span data-ttu-id="e5237-106">雲端運算提供方式 toostore，串流處理，以及存取這些大型的媒體檔案。</span><span class="sxs-lookup"><span data-stu-id="e5237-106">Cloud computing provides a way toostore, stream, and access these large media files.</span></span> <span data-ttu-id="e5237-107">但您公司的文件庫的視訊內容成長時，還需要從 hello 內容擷取 insights 同樣有效方法。</span><span class="sxs-lookup"><span data-stu-id="e5237-107">But as a company's library of video content grows, it needs an equally effective means of extracting insights from hello content.</span></span> 

<span data-ttu-id="e5237-108">tooaddress 這個持續成長的需要，Azure Media Services 提供 Azure 媒體分析。</span><span class="sxs-lookup"><span data-stu-id="e5237-108">tooaddress this growing need, Azure Media Services offers Azure Media Analytics.</span></span> <span data-ttu-id="e5237-109">媒體分析是語音和願景的元件，讓組織和企業 tooderive 可執行的洞察力更容易從視訊檔案的集合。</span><span class="sxs-lookup"><span data-stu-id="e5237-109">Media Analytics is a collection of speech and vision components that makes it easier for organizations and enterprises tooderive actionable insights from their video files.</span></span> <span data-ttu-id="e5237-110">建立使用 hello 核心 Media Services 平台元件，媒體分析可以處理媒體處理上一天的小數位數。</span><span class="sxs-lookup"><span data-stu-id="e5237-110">Built by using hello core Media Services platform components, Media Analytics can handle media processing at scale on day one.</span></span>

<span data-ttu-id="e5237-111">有了媒體分析，開發人員可以快速地將進階影片功能帶入應用程式。</span><span class="sxs-lookup"><span data-stu-id="e5237-111">With Media Analytics, developers can quickly bring advanced video functionality into applications.</span></span> <span data-ttu-id="e5237-112">Hello 完整標尺、 相容性、 安全性和大型組織所需的全球化提供的企業環境。</span><span class="sxs-lookup"><span data-stu-id="e5237-112">It provides enterprise environments with hello full scale, compliance, security, and global reach required by large organizations.</span></span>

<span data-ttu-id="e5237-113">hello 下列圖表顯示媒體分析和其他 hello Media Services 平台的主要部分。</span><span class="sxs-lookup"><span data-stu-id="e5237-113">hello following diagram shows Media Analytics and other major parts of hello Media Services platform.</span></span> 

![VoD 工作流程](./media/media-services-analytics-overview/media-services-analytics-overview01.png)

<span data-ttu-id="e5237-115">媒體分析的媒體處理器會產生 MP4 檔案或 JSON 檔案。</span><span class="sxs-lookup"><span data-stu-id="e5237-115">Media Analytics media processors produce MP4 files or JSON files.</span></span> <span data-ttu-id="e5237-116">媒體處理器就會產生的 MP4 檔案，您可以漸進式下載 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="e5237-116">If a media processor produces an MP4 file, you can progressively download hello file.</span></span> <span data-ttu-id="e5237-117">媒體處理器就會產生 JSON 檔案，您可以從 Azure Blob 儲存體下載 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="e5237-117">If a media processor produces a JSON file, you can download hello file from Azure Blob storage.</span></span> 

## <a name="media-analytics-services"></a><span data-ttu-id="e5237-118">媒體分析服務</span><span class="sxs-lookup"><span data-stu-id="e5237-118">Media Analytics services</span></span>

### <a name="indexer"></a><span data-ttu-id="e5237-119">索引器</span><span class="sxs-lookup"><span data-stu-id="e5237-119">Indexer</span></span>
<span data-ttu-id="e5237-120">Azure 媒體索引器可讓您的內容可供搜尋，並且產生隱藏式輔助字幕。</span><span class="sxs-lookup"><span data-stu-id="e5237-120">With Azure Media Indexer, you can make content searchable and generate closed-captioning tracks.</span></span> <span data-ttu-id="e5237-121">比較的 toohello 舊版本中，Azure Media Indexer 2 預覽具有更快索引和更廣泛的語言支援。</span><span class="sxs-lookup"><span data-stu-id="e5237-121">Compared toohello previous version, Azure Media Indexer 2 Preview has faster indexing and broader language support.</span></span> <span data-ttu-id="e5237-122">支援的語言包括英文、西班牙文、法文、德文、義大利文、中文、葡萄牙文和阿拉伯文。</span><span class="sxs-lookup"><span data-stu-id="e5237-122">Supported languages include English, Spanish, French, German, Italian, Chinese, Portuguese, and Arabic.</span></span> <span data-ttu-id="e5237-123">如需詳細資訊和範例，請參閱[利用 Azure 媒體索引器 2 處理影片](media-services-process-content-with-indexer2.md)。</span><span class="sxs-lookup"><span data-stu-id="e5237-123">For detailed information and examples, see [Process videos with Azure Media Indexer 2](media-services-process-content-with-indexer2.md).</span></span>
### <a name="hyperlapse"></a><span data-ttu-id="e5237-124">Hyperlapse</span><span class="sxs-lookup"><span data-stu-id="e5237-124">Hyperlapse</span></span>
<span data-ttu-id="e5237-125">Microsoft Hyperlapse 結合視訊穩定和螢光功能 toocreate 快速，您可以使用視訊從您的完整格式內容。</span><span class="sxs-lookup"><span data-stu-id="e5237-125">Microsoft Hyperlapse combines video stabilization and time-lapse capability toocreate quick, consumable videos from your long-form content.</span></span> <span data-ttu-id="e5237-126">除了建立螢光視訊，您可以使用 Hyperlapse toocreate 穩定影片 shaky 擷取透過行動電話和攝影機的視訊。</span><span class="sxs-lookup"><span data-stu-id="e5237-126">Besides creating time-lapse video, you can use Hyperlapse toocreate stable videos from shaky videos captured via cell phones and camcorders.</span></span> <span data-ttu-id="e5237-127">如需詳細資訊和範例，請參閱 [Hyperlapse 媒體檔案與 Azure 媒體超縮時攝影](media-services-hyperlapse-content.md)。</span><span class="sxs-lookup"><span data-stu-id="e5237-127">For detailed information and examples, see [Hyperlapse media files with Azure Media Hyperlapse](media-services-hyperlapse-content.md).</span></span>
### <a name="motion-detector"></a><span data-ttu-id="e5237-128">動作偵測</span><span class="sxs-lookup"><span data-stu-id="e5237-128">Motion Detector</span></span>
<span data-ttu-id="e5237-129">您可以使用動作偵測器 toodetect 影片中，具有固定的背景的視訊。</span><span class="sxs-lookup"><span data-stu-id="e5237-129">You can use Motion Detector toodetect motion in a video with stationary backgrounds.</span></span> <span data-ttu-id="e5237-130">這使得可能的誤判 toocheck 影片監視攝影機所偵測到的事件。</span><span class="sxs-lookup"><span data-stu-id="e5237-130">This makes it possible toocheck for false positives on motion events detected by surveillance cameras.</span></span> <span data-ttu-id="e5237-131">如需詳細資訊和範例，請參閱 [Azure 媒體分析的動作偵測](media-services-motion-detection.md)。</span><span class="sxs-lookup"><span data-stu-id="e5237-131">For detailed information and examples, see [Motion detection for Azure Media Analytics](media-services-motion-detection.md).</span></span>
### <a name="face-detector"></a><span data-ttu-id="e5237-132">臉部偵測</span><span class="sxs-lookup"><span data-stu-id="e5237-132">Face Detector</span></span>
<span data-ttu-id="e5237-133">透過使用臉部偵測，您便能偵測人臉及其表情，包括快樂、悲傷及驚喜。</span><span class="sxs-lookup"><span data-stu-id="e5237-133">By using Face Detector, you can detect people’s faces and their emotions, including happiness, sadness, and surprise.</span></span> <span data-ttu-id="e5237-134">這項服務有數個實用的產業應用程式 (將於稍後說明)，包括彙總並分析事件參與人員的反應。</span><span class="sxs-lookup"><span data-stu-id="e5237-134">This has several useful industry applications, described later, including aggregating and analyzing reactions of people attending an event.</span></span> <span data-ttu-id="e5237-135">如需詳細資訊和範例，請參閱 [Azure 媒體分析的臉部和情緒偵測](media-services-face-and-emotion-detection.md)。</span><span class="sxs-lookup"><span data-stu-id="e5237-135">For detailed information and examples, see [Face and emotion detection for Azure Media Analytics](media-services-face-and-emotion-detection.md).</span></span>
### <a name="video-summarization"></a><span data-ttu-id="e5237-136">影片摘要</span><span class="sxs-lookup"><span data-stu-id="e5237-136">Video summarization</span></span>
<span data-ttu-id="e5237-137">視訊摘要可以協助您建立的較長的視訊摘要會自動從 hello 來源視訊中選取感興趣的程式碼片段。</span><span class="sxs-lookup"><span data-stu-id="e5237-137">Video summarization can help you create summaries of long videos by automatically selecting interesting snippets from hello source video.</span></span> <span data-ttu-id="e5237-138">這項功能時，您想要 tooprovide 哪些 tooexpect 長的視訊中的快速概觀。</span><span class="sxs-lookup"><span data-stu-id="e5237-138">This ability is useful when you want tooprovide a quick overview of what tooexpect in a long video.</span></span> <span data-ttu-id="e5237-139">如需詳細的資訊和範例，請參閱[toocreate 視訊摘要時，使用 Azure Media 視訊縮圖](media-services-video-summarization.md)。</span><span class="sxs-lookup"><span data-stu-id="e5237-139">For detailed information and examples, see [Use Azure Media Video Thumbnails toocreate video summarization](media-services-video-summarization.md).</span></span>
### <a name="optical-character-recognition"></a><span data-ttu-id="e5237-140">光學字元辨識</span><span class="sxs-lookup"><span data-stu-id="e5237-140">Optical character recognition</span></span>
<span data-ttu-id="e5237-141">Azure 媒體 OCR (光學字元辨識) 可讓您將影片檔中的文字內容轉換成可編輯、可搜尋的數位文字。</span><span class="sxs-lookup"><span data-stu-id="e5237-141">With Azure Media OCR (optical character recognition), you can convert text content in video files into editable, searchable digital text.</span></span> <span data-ttu-id="e5237-142">然後，您可以自動從您的媒體 hello 視訊訊號的 hello 擷取有意義的中繼資料。</span><span class="sxs-lookup"><span data-stu-id="e5237-142">You can then automate hello extraction of meaningful metadata from hello video signal of your media.</span></span>
### <a name="scalable-face-redaction"></a><span data-ttu-id="e5237-143">可調整式臉部修訂</span><span class="sxs-lookup"><span data-stu-id="e5237-143">Scalable face redaction</span></span>
<span data-ttu-id="e5237-144">Azure 媒體 Redactor 是提供可擴充的字體 redaction hello 雲端中的媒體分析媒體處理器。</span><span class="sxs-lookup"><span data-stu-id="e5237-144">Azure Media Redactor is a Media Analytics media processor that offers scalable face redaction in hello cloud.</span></span> <span data-ttu-id="e5237-145">藉由使用朝 redaction，您可以修改您的視訊 tooblur 字體的所選的個人。</span><span class="sxs-lookup"><span data-stu-id="e5237-145">By using face redaction, you can modify your video tooblur faces of selected individuals.</span></span> <span data-ttu-id="e5237-146">您可能想 toouse hello 朝 redaction 新聞媒體或服務時牽涉到公共安全。</span><span class="sxs-lookup"><span data-stu-id="e5237-146">You might want toouse hello face redaction service in news media or when public safety is involved.</span></span> <span data-ttu-id="e5237-147">幾分鐘的影片，其中包含多個字型都會小時 tooredact 以手動方式，但使用這項服務，朝 redaction 需幾個簡單的步驟。</span><span class="sxs-lookup"><span data-stu-id="e5237-147">A few minutes of footage that contains multiple faces can take hours tooredact manually, but with this service, face redaction takes just a few simple steps.</span></span> <span data-ttu-id="e5237-148">如需詳細資訊，請參閱 hello [Redact 使用 Azure 媒體分析字體](media-services-face-redaction.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="e5237-148">For more information, see hello [Redact faces with Azure Media Analytics](media-services-face-redaction.md) article.</span></span>

## <a name="common-scenarios"></a><span data-ttu-id="e5237-149">常見案例</span><span class="sxs-lookup"><span data-stu-id="e5237-149">Common scenarios</span></span>
<span data-ttu-id="e5237-150">媒體分析可協助組織和企業從影片中得到新的見解，並更有效地管理大量的影片內容。</span><span class="sxs-lookup"><span data-stu-id="e5237-150">Media Analytics can help organizations and enterprises glean new insights from video and more effectively manage large volumes of video content.</span></span> <span data-ttu-id="e5237-151">以下是幾個案例︰</span><span class="sxs-lookup"><span data-stu-id="e5237-151">Here are several scenarios:</span></span>

* <span data-ttu-id="e5237-152">**客服中心**。</span><span class="sxs-lookup"><span data-stu-id="e5237-152">**Call centers**.</span></span> <span data-ttu-id="e5237-153">社交媒體的 hello 問世，即使是使用客戶撥接中心仍可加速大量百分比的客戶服務的交易。</span><span class="sxs-lookup"><span data-stu-id="e5237-153">Even with hello advent of social media, customer call centers still facilitate a large percentage of customer-service transactions.</span></span> <span data-ttu-id="e5237-154">此音訊資料中的編碼是大量的客戶資訊可分析 tooachieve 較高的客戶滿意度。</span><span class="sxs-lookup"><span data-stu-id="e5237-154">Encoded in this audio data is a large amount of customer information that can be analyzed tooachieve higher customer satisfaction.</span></span> <span data-ttu-id="e5237-155">組織可使用媒體索引器擷取文字，及建置搜尋索引與儀表板。</span><span class="sxs-lookup"><span data-stu-id="e5237-155">By using Media Indexer, organizations can extract text and build search indexes and dashboards.</span></span> <span data-ttu-id="e5237-156">接著便可以從一般客訴、客訴來源及其他相關資料中獲取情報。</span><span class="sxs-lookup"><span data-stu-id="e5237-156">Then they can extract intelligence around common complaints, sources of complaints, and other relevant data.</span></span>
* <span data-ttu-id="e5237-157">**仲裁使用者產生的內容**。</span><span class="sxs-lookup"><span data-stu-id="e5237-157">**User-generated content moderation**.</span></span> <span data-ttu-id="e5237-158">從新聞媒體插座 toopolice 部門，許多組織必須面對大眾入口網站可接受使用者產生的媒體，例如視訊和影像。</span><span class="sxs-lookup"><span data-stu-id="e5237-158">From news media outlets toopolice departments, many organizations have public-facing portals that accept user-generated media such as videos and images.</span></span> <span data-ttu-id="e5237-159">hello 的內容的磁碟區可以因為 toounexpected 事件暴增。</span><span class="sxs-lookup"><span data-stu-id="e5237-159">hello volume of content can spike due toounexpected events.</span></span> <span data-ttu-id="e5237-160">在這些情況下，很難 tooconduct 有效手動的檢閱內容的適當性。</span><span class="sxs-lookup"><span data-stu-id="e5237-160">In these scenarios, it is difficult tooconduct effective manual reviews of content for appropriateness.</span></span> <span data-ttu-id="e5237-161">客戶可以依賴 hello 內容合適性服務 toofocus 適當的內容。</span><span class="sxs-lookup"><span data-stu-id="e5237-161">Customers can rely on hello content-moderation service toofocus on content that is appropriate.</span></span>
* <span data-ttu-id="e5237-162">**監視錄影**.</span><span class="sxs-lookup"><span data-stu-id="e5237-162">**Surveillance**.</span></span> <span data-ttu-id="e5237-163">Hello 與使用中的 IP 相機的成長是監視視訊的成長詳細目錄。</span><span class="sxs-lookup"><span data-stu-id="e5237-163">With hello growth in use of IP cameras comes a growing inventory of surveillance video.</span></span> <span data-ttu-id="e5237-164">手動檢視監視視訊是時間密集而且容易產生 toohuman 錯誤。</span><span class="sxs-lookup"><span data-stu-id="e5237-164">Manually reviewing surveillance video is time intensive and prone toohuman error.</span></span> <span data-ttu-id="e5237-165">媒體分析提供服務，例如影片偵測、 臉偵測和 Hyperlapse toomake hello 程序的檢視、 管理和建立衍生更容易。</span><span class="sxs-lookup"><span data-stu-id="e5237-165">Media Analytics provides services such as motion detection, face detection, and Hyperlapse toomake hello process of reviewing, managing, and creating derivatives easier.</span></span>

## <a name="media-analytics-media-processors"></a><span data-ttu-id="e5237-166">媒體分析媒體處理器</span><span class="sxs-lookup"><span data-stu-id="e5237-166">Media Analytics media processors</span></span>
<span data-ttu-id="e5237-167">本章節列出 hello 媒體分析媒體處理器，並且示範如何 toouse.NET 或 REST tooget 媒體處理器 (MP) 物件。</span><span class="sxs-lookup"><span data-stu-id="e5237-167">This section lists hello Media Analytics media processors and shows how toouse .NET or REST tooget a media processor (MP) object.</span></span>

### <a name="mp-names"></a><span data-ttu-id="e5237-168">MP 名稱</span><span class="sxs-lookup"><span data-stu-id="e5237-168">MP names</span></span>
* <span data-ttu-id="e5237-169">Azure 媒體索引器 2 預覽</span><span class="sxs-lookup"><span data-stu-id="e5237-169">Azure Media Indexer 2 Preview</span></span>
* <span data-ttu-id="e5237-170">Azure Media Indexer</span><span class="sxs-lookup"><span data-stu-id="e5237-170">Azure Media Indexer</span></span>
* <span data-ttu-id="e5237-171">Azure Media Hyperlapse</span><span class="sxs-lookup"><span data-stu-id="e5237-171">Azure Media Hyperlapse</span></span>
* <span data-ttu-id="e5237-172">Azure 媒體臉部偵測器</span><span class="sxs-lookup"><span data-stu-id="e5237-172">Azure Media Face Detector</span></span>
* <span data-ttu-id="e5237-173">Azure 媒體動作偵測器</span><span class="sxs-lookup"><span data-stu-id="e5237-173">Azure Media Motion Detector</span></span>
* <span data-ttu-id="e5237-174">Azure 媒體視訊縮圖</span><span class="sxs-lookup"><span data-stu-id="e5237-174">Azure Media Video Thumbnails</span></span>
* <span data-ttu-id="e5237-175">Azure 媒體 OCR</span><span class="sxs-lookup"><span data-stu-id="e5237-175">Azure Media OCR</span></span>

### <a name="net"></a><span data-ttu-id="e5237-176">.NET</span><span class="sxs-lookup"><span data-stu-id="e5237-176">.NET</span></span>
<span data-ttu-id="e5237-177">hello 遵循的 hello 函式會採用一個指定的管理組件名稱，並傳回的管理組件物件。</span><span class="sxs-lookup"><span data-stu-id="e5237-177">hello following function takes one of hello specified MP names and returns an MP object.</span></span>

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


### <a name="rest"></a><span data-ttu-id="e5237-178">REST</span><span class="sxs-lookup"><span data-stu-id="e5237-178">REST</span></span>
<span data-ttu-id="e5237-179">要求：</span><span class="sxs-lookup"><span data-stu-id="e5237-179">Request:</span></span>

    GET https://media.windows.net/api/MediaProcessors()?$filter=Name%20eq%20'Azure%20Media%20OCR' HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer <token>
    x-ms-version: 2.12
    Host: media.windows.net

<span data-ttu-id="e5237-180">回應：</span><span class="sxs-lookup"><span data-stu-id="e5237-180">Response:</span></span>

    . . .

    {  
       "odata.metadata":"https://media.windows.net/api/$metadata#MediaProcessors",
       "value":[  
          {  
             "Id":"nb:mpid:UUID:074c3899-d9fb-448f-9ae1-4ebcbe633056",
             "Description":"Azure Media OCR",
             "Name":"Azure Media OCR",
             "Sku":"",
             "Vendor":"Microsoft",
             "Version":"1.1"
          }
       ]
    }

## <a name="demos"></a><span data-ttu-id="e5237-181">示範</span><span class="sxs-lookup"><span data-stu-id="e5237-181">Demos</span></span>
<span data-ttu-id="e5237-182">請參閱 [Azure 媒體分析示範](http://azuremedialabs.azurewebsites.net/demos/Analytics.html)。</span><span class="sxs-lookup"><span data-stu-id="e5237-182">See [Azure Media Analytics demos](http://azuremedialabs.azurewebsites.net/demos/Analytics.html).</span></span>

## <a name="next-steps"></a><span data-ttu-id="e5237-183">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e5237-183">Next steps</span></span>
<span data-ttu-id="e5237-184">檢閱媒體服務學習路徑。</span><span class="sxs-lookup"><span data-stu-id="e5237-184">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="e5237-185">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="e5237-185">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-articles"></a><span data-ttu-id="e5237-186">相關文章</span><span class="sxs-lookup"><span data-stu-id="e5237-186">Related articles</span></span>
<span data-ttu-id="e5237-187">請參閱[媒體服務分析公告](https://azure.microsoft.com/blog/introducing-azure-media-analytics/)。</span><span class="sxs-lookup"><span data-stu-id="e5237-187">See [Media Services Analytics announcement](https://azure.microsoft.com/blog/introducing-azure-media-analytics/).</span></span>

<!-- Images -->

[overview]: ./media/media-services-video-on-demand-workflow/media-services-video-on-demand.png
