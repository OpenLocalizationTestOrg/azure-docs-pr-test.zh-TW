---
title: "媒體服務平台上的媒體分析 | Microsoft Docs"
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
ms.openlocfilehash: c0bbe6f80370515fa783b12757434897fe2221b6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="media-analytics-on-the-media-services-platform"></a><span data-ttu-id="c8efb-103">媒體服務平台上的媒體分析</span><span class="sxs-lookup"><span data-stu-id="c8efb-103">Media Analytics on the Media Services platform</span></span>
## <a name="overview"></a><span data-ttu-id="c8efb-104">概觀</span><span class="sxs-lookup"><span data-stu-id="c8efb-104">Overview</span></span>
<span data-ttu-id="c8efb-105">越來越多組織採用影片做為慣用的媒體，用來訓練員工、連絡客戶與記錄商務功能。</span><span class="sxs-lookup"><span data-stu-id="c8efb-105">More organizations are using video as the preferred medium to train their employees, engage their customers, and document business functions.</span></span> <span data-ttu-id="c8efb-106">雖然雲端運算可供儲存、串流及存取大型媒體檔案，</span><span class="sxs-lookup"><span data-stu-id="c8efb-106">Cloud computing provides a way to store, stream, and access these large media files.</span></span> <span data-ttu-id="c8efb-107">但隨著公司影片庫內容的成長，需要同樣有效的方法深入分析內容。</span><span class="sxs-lookup"><span data-stu-id="c8efb-107">But as a company's library of video content grows, it needs an equally effective means of extracting insights from the content.</span></span> 

<span data-ttu-id="c8efb-108">為了滿足不斷成長的需求，Azure 媒體服務提供 Azure 媒體分析。</span><span class="sxs-lookup"><span data-stu-id="c8efb-108">To address this growing need, Azure Media Services offers Azure Media Analytics.</span></span> <span data-ttu-id="c8efb-109">媒體分析是一組語音與視覺元件，可讓組織或企業從其影片檔輕鬆地產生能採取行動的見解。</span><span class="sxs-lookup"><span data-stu-id="c8efb-109">Media Analytics is a collection of speech and vision components that makes it easier for organizations and enterprises to derive actionable insights from their video files.</span></span> <span data-ttu-id="c8efb-110">媒體分析服務是使用核心媒體服務平台元件建置而成，因此可隨時進行一天的大規模媒體處理。</span><span class="sxs-lookup"><span data-stu-id="c8efb-110">Built by using the core Media Services platform components, Media Analytics can handle media processing at scale on day one.</span></span>

<span data-ttu-id="c8efb-111">有了媒體分析，開發人員可以快速地將進階影片功能帶入應用程式。</span><span class="sxs-lookup"><span data-stu-id="c8efb-111">With Media Analytics, developers can quickly bring advanced video functionality into applications.</span></span> <span data-ttu-id="c8efb-112">其提供的企業環境具備大型組織所需的完整規模、相容性、安全性和遍及全球的觸角。</span><span class="sxs-lookup"><span data-stu-id="c8efb-112">It provides enterprise environments with the full scale, compliance, security, and global reach required by large organizations.</span></span>

<span data-ttu-id="c8efb-113">下圖顯示媒體分析和媒體服務平台的其他主要部分。</span><span class="sxs-lookup"><span data-stu-id="c8efb-113">The following diagram shows Media Analytics and other major parts of the Media Services platform.</span></span> 

![VoD 工作流程](./media/media-services-analytics-overview/media-services-analytics-overview01.png)

<span data-ttu-id="c8efb-115">媒體分析的媒體處理器會產生 MP4 檔案或 JSON 檔案。</span><span class="sxs-lookup"><span data-stu-id="c8efb-115">Media Analytics media processors produce MP4 files or JSON files.</span></span> <span data-ttu-id="c8efb-116">如果媒體處理器產生 MP4 檔案，您可以漸進式下載檔案。</span><span class="sxs-lookup"><span data-stu-id="c8efb-116">If a media processor produces an MP4 file, you can progressively download the file.</span></span> <span data-ttu-id="c8efb-117">如果媒體處理器產生 JSON 檔案，您可以從 Azure Blob 儲存體下載檔案。</span><span class="sxs-lookup"><span data-stu-id="c8efb-117">If a media processor produces a JSON file, you can download the file from Azure Blob storage.</span></span> 

## <a name="media-analytics-services"></a><span data-ttu-id="c8efb-118">媒體分析服務</span><span class="sxs-lookup"><span data-stu-id="c8efb-118">Media Analytics services</span></span>

### <a name="indexer"></a><span data-ttu-id="c8efb-119">索引器</span><span class="sxs-lookup"><span data-stu-id="c8efb-119">Indexer</span></span>
<span data-ttu-id="c8efb-120">Azure 媒體索引器可讓您的內容可供搜尋，並且產生隱藏式輔助字幕。</span><span class="sxs-lookup"><span data-stu-id="c8efb-120">With Azure Media Indexer, you can make content searchable and generate closed-captioning tracks.</span></span> <span data-ttu-id="c8efb-121">相較於舊版，Azure 媒體索引器 2 (預覽版) 速度更快，支援更多的語言。</span><span class="sxs-lookup"><span data-stu-id="c8efb-121">Compared to the previous version, Azure Media Indexer 2 Preview has faster indexing and broader language support.</span></span> <span data-ttu-id="c8efb-122">支援的語言包括英文、西班牙文、法文、德文、義大利文、中文、葡萄牙文和阿拉伯文。</span><span class="sxs-lookup"><span data-stu-id="c8efb-122">Supported languages include English, Spanish, French, German, Italian, Chinese, Portuguese, and Arabic.</span></span> <span data-ttu-id="c8efb-123">如需詳細資訊和範例，請參閱[利用 Azure 媒體索引器 2 處理影片](media-services-process-content-with-indexer2.md)。</span><span class="sxs-lookup"><span data-stu-id="c8efb-123">For detailed information and examples, see [Process videos with Azure Media Indexer 2](media-services-process-content-with-indexer2.md).</span></span>
### <a name="hyperlapse"></a><span data-ttu-id="c8efb-124">Hyperlapse</span><span class="sxs-lookup"><span data-stu-id="c8efb-124">Hyperlapse</span></span>
<span data-ttu-id="c8efb-125">Microsoft Hyperlapse 將影像防震與縮時攝影功能結合在一起，能從完整的內容中建立快速、消費性的影片。</span><span class="sxs-lookup"><span data-stu-id="c8efb-125">Microsoft Hyperlapse combines video stabilization and time-lapse capability to create quick, consumable videos from your long-form content.</span></span> <span data-ttu-id="c8efb-126">除了縮時攝影外，您也可以使用 Hyperlapse，從透過行動電話及攝影機拍攝的晃動影片中產生不晃動的影片。</span><span class="sxs-lookup"><span data-stu-id="c8efb-126">Besides creating time-lapse video, you can use Hyperlapse to create stable videos from shaky videos captured via cell phones and camcorders.</span></span> <span data-ttu-id="c8efb-127">如需詳細資訊和範例，請參閱 [Hyperlapse 媒體檔案與 Azure 媒體超縮時攝影](media-services-hyperlapse-content.md)。</span><span class="sxs-lookup"><span data-stu-id="c8efb-127">For detailed information and examples, see [Hyperlapse media files with Azure Media Hyperlapse](media-services-hyperlapse-content.md).</span></span>
### <a name="motion-detector"></a><span data-ttu-id="c8efb-128">動作偵測</span><span class="sxs-lookup"><span data-stu-id="c8efb-128">Motion Detector</span></span>
<span data-ttu-id="c8efb-129">您可以使用動作偵測在影片中偵測背景靜止的動作。</span><span class="sxs-lookup"><span data-stu-id="c8efb-129">You can use Motion Detector to detect motion in a video with stationary backgrounds.</span></span> <span data-ttu-id="c8efb-130">如此一來，便能夠檢查監視攝影機所偵測到的動作事件中是否有誤判。</span><span class="sxs-lookup"><span data-stu-id="c8efb-130">This makes it possible to check for false positives on motion events detected by surveillance cameras.</span></span> <span data-ttu-id="c8efb-131">如需詳細資訊和範例，請參閱 [Azure 媒體分析的動作偵測](media-services-motion-detection.md)。</span><span class="sxs-lookup"><span data-stu-id="c8efb-131">For detailed information and examples, see [Motion detection for Azure Media Analytics](media-services-motion-detection.md).</span></span>
### <a name="face-detector"></a><span data-ttu-id="c8efb-132">臉部偵測</span><span class="sxs-lookup"><span data-stu-id="c8efb-132">Face Detector</span></span>
<span data-ttu-id="c8efb-133">透過使用臉部偵測，您便能偵測人臉及其表情，包括快樂、悲傷及驚喜。</span><span class="sxs-lookup"><span data-stu-id="c8efb-133">By using Face Detector, you can detect people’s faces and their emotions, including happiness, sadness, and surprise.</span></span> <span data-ttu-id="c8efb-134">這項服務有數個實用的產業應用程式 (將於稍後說明)，包括彙總並分析事件參與人員的反應。</span><span class="sxs-lookup"><span data-stu-id="c8efb-134">This has several useful industry applications, described later, including aggregating and analyzing reactions of people attending an event.</span></span> <span data-ttu-id="c8efb-135">如需詳細資訊和範例，請參閱 [Azure 媒體分析的臉部和情緒偵測](media-services-face-and-emotion-detection.md)。</span><span class="sxs-lookup"><span data-stu-id="c8efb-135">For detailed information and examples, see [Face and emotion detection for Azure Media Analytics](media-services-face-and-emotion-detection.md).</span></span>
### <a name="video-summarization"></a><span data-ttu-id="c8efb-136">影片摘要</span><span class="sxs-lookup"><span data-stu-id="c8efb-136">Video summarization</span></span>
<span data-ttu-id="c8efb-137">視訊摘要可自動選取來源視訊的有趣片段，協助您建立較長視訊的摘要。</span><span class="sxs-lookup"><span data-stu-id="c8efb-137">Video summarization can help you create summaries of long videos by automatically selecting interesting snippets from the source video.</span></span> <span data-ttu-id="c8efb-138">針對片長較長的影片，如果您想要提供精彩內容的快速概觀，此功能非常有用。</span><span class="sxs-lookup"><span data-stu-id="c8efb-138">This ability is useful when you want to provide a quick overview of what to expect in a long video.</span></span> <span data-ttu-id="c8efb-139">如需詳細資訊和範例，請參閱[使用 Azure 媒體影片縮圖建立影片摘要](media-services-video-summarization.md)。</span><span class="sxs-lookup"><span data-stu-id="c8efb-139">For detailed information and examples, see [Use Azure Media Video Thumbnails to create video summarization](media-services-video-summarization.md).</span></span>
### <a name="optical-character-recognition"></a><span data-ttu-id="c8efb-140">光學字元辨識</span><span class="sxs-lookup"><span data-stu-id="c8efb-140">Optical character recognition</span></span>
<span data-ttu-id="c8efb-141">Azure 媒體 OCR (光學字元辨識) 可讓您將影片檔中的文字內容轉換成可編輯、可搜尋的數位文字。</span><span class="sxs-lookup"><span data-stu-id="c8efb-141">With Azure Media OCR (optical character recognition), you can convert text content in video files into editable, searchable digital text.</span></span> <span data-ttu-id="c8efb-142">接著您便可從媒體的影片訊號中自動擷取出有意義的中繼資料。</span><span class="sxs-lookup"><span data-stu-id="c8efb-142">You can then automate the extraction of meaningful metadata from the video signal of your media.</span></span>
### <a name="scalable-face-redaction"></a><span data-ttu-id="c8efb-143">可調整式臉部修訂</span><span class="sxs-lookup"><span data-stu-id="c8efb-143">Scalable face redaction</span></span>
<span data-ttu-id="c8efb-144">Azure 媒體修訂器是媒體分析媒體處理器，可在雲端提供可調整式臉部修訂。</span><span class="sxs-lookup"><span data-stu-id="c8efb-144">Azure Media Redactor is a Media Analytics media processor that offers scalable face redaction in the cloud.</span></span> <span data-ttu-id="c8efb-145">您可以使用臉部修訂功能修改影片，將所選人物的臉部變得模糊。</span><span class="sxs-lookup"><span data-stu-id="c8efb-145">By using face redaction, you can modify your video to blur faces of selected individuals.</span></span> <span data-ttu-id="c8efb-146">您可能會想要在新聞媒體中或涉及公共安全時，使用臉部修訂服務。</span><span class="sxs-lookup"><span data-stu-id="c8efb-146">You might want to use the face redaction service in news media or when public safety is involved.</span></span> <span data-ttu-id="c8efb-147">當要手動修訂多個臉部時，即使片長只有數分鐘，也會花上數小時修訂，但若使用此服務，則只需要幾個簡單的步驟就能完成臉部修訂。</span><span class="sxs-lookup"><span data-stu-id="c8efb-147">A few minutes of footage that contains multiple faces can take hours to redact manually, but with this service, face redaction takes just a few simple steps.</span></span> <span data-ttu-id="c8efb-148">如需詳細資訊，請參閱[使用 Azure 媒體分析修訂臉部](media-services-face-redaction.md)一文。</span><span class="sxs-lookup"><span data-stu-id="c8efb-148">For more information, see the [Redact faces with Azure Media Analytics](media-services-face-redaction.md) article.</span></span>

## <a name="common-scenarios"></a><span data-ttu-id="c8efb-149">常見案例</span><span class="sxs-lookup"><span data-stu-id="c8efb-149">Common scenarios</span></span>
<span data-ttu-id="c8efb-150">媒體分析可協助組織和企業從影片中得到新的見解，並更有效地管理大量的影片內容。</span><span class="sxs-lookup"><span data-stu-id="c8efb-150">Media Analytics can help organizations and enterprises glean new insights from video and more effectively manage large volumes of video content.</span></span> <span data-ttu-id="c8efb-151">以下是幾個案例︰</span><span class="sxs-lookup"><span data-stu-id="c8efb-151">Here are several scenarios:</span></span>

* <span data-ttu-id="c8efb-152">**客服中心**。</span><span class="sxs-lookup"><span data-stu-id="c8efb-152">**Call centers**.</span></span> <span data-ttu-id="c8efb-153">即使社交媒體出現，但客服中心仍能協助處理大量的客戶服務交易。</span><span class="sxs-lookup"><span data-stu-id="c8efb-153">Even with the advent of social media, customer call centers still facilitate a large percentage of customer-service transactions.</span></span> <span data-ttu-id="c8efb-154">客服中心的語音資料經編碼後可成為大量的客戶資訊，企業可分析這些資訊以提高客戶滿意度。</span><span class="sxs-lookup"><span data-stu-id="c8efb-154">Encoded in this audio data is a large amount of customer information that can be analyzed to achieve higher customer satisfaction.</span></span> <span data-ttu-id="c8efb-155">組織可使用媒體索引器擷取文字，及建置搜尋索引與儀表板。</span><span class="sxs-lookup"><span data-stu-id="c8efb-155">By using Media Indexer, organizations can extract text and build search indexes and dashboards.</span></span> <span data-ttu-id="c8efb-156">接著便可以從一般客訴、客訴來源及其他相關資料中獲取情報。</span><span class="sxs-lookup"><span data-stu-id="c8efb-156">Then they can extract intelligence around common complaints, sources of complaints, and other relevant data.</span></span>
* <span data-ttu-id="c8efb-157">**仲裁使用者產生的內容**。</span><span class="sxs-lookup"><span data-stu-id="c8efb-157">**User-generated content moderation**.</span></span> <span data-ttu-id="c8efb-158">從新聞媒體到警察局，許多組織都有對外公開的入口網站可接受使用者產生的媒體，例如影片和影像。</span><span class="sxs-lookup"><span data-stu-id="c8efb-158">From news media outlets to police departments, many organizations have public-facing portals that accept user-generated media such as videos and images.</span></span> <span data-ttu-id="c8efb-159">內容的數量可能會因為未預期事件而激增。</span><span class="sxs-lookup"><span data-stu-id="c8efb-159">The volume of content can spike due to unexpected events.</span></span> <span data-ttu-id="c8efb-160">在這些狀況下，很難有效地人工審查內容是否適當。</span><span class="sxs-lookup"><span data-stu-id="c8efb-160">In these scenarios, it is difficult to conduct effective manual reviews of content for appropriateness.</span></span> <span data-ttu-id="c8efb-161">客戶可以依賴內容仲裁服務將重點放在適當的內容。</span><span class="sxs-lookup"><span data-stu-id="c8efb-161">Customers can rely on the content-moderation service to focus on content that is appropriate.</span></span>
* <span data-ttu-id="c8efb-162">**監視錄影**.</span><span class="sxs-lookup"><span data-stu-id="c8efb-162">**Surveillance**.</span></span> <span data-ttu-id="c8efb-163">隨著 IP 攝影機的使用愈來愈普遍，監視影片的存量也隨之成長。</span><span class="sxs-lookup"><span data-stu-id="c8efb-163">With the growth in use of IP cameras comes a growing inventory of surveillance video.</span></span> <span data-ttu-id="c8efb-164">手動檢閱監視視訊既耗時又容易發生人為錯誤。</span><span class="sxs-lookup"><span data-stu-id="c8efb-164">Manually reviewing surveillance video is time intensive and prone to human error.</span></span> <span data-ttu-id="c8efb-165">媒體分析提供數種服務，例如動作偵測、臉部偵測和 Hyperlapse，讓審查、管理和建立衍生物件的程序變得更容易。</span><span class="sxs-lookup"><span data-stu-id="c8efb-165">Media Analytics provides services such as motion detection, face detection, and Hyperlapse to make the process of reviewing, managing, and creating derivatives easier.</span></span>

## <a name="media-analytics-media-processors"></a><span data-ttu-id="c8efb-166">媒體分析媒體處理器</span><span class="sxs-lookup"><span data-stu-id="c8efb-166">Media Analytics media processors</span></span>
<span data-ttu-id="c8efb-167">本節列出所有媒體分析媒體處理器，並示範如何使用 .NET 或 REST 來取得媒體處理器 (MP) 物件。</span><span class="sxs-lookup"><span data-stu-id="c8efb-167">This section lists the Media Analytics media processors and shows how to use .NET or REST to get a media processor (MP) object.</span></span>

### <a name="mp-names"></a><span data-ttu-id="c8efb-168">MP 名稱</span><span class="sxs-lookup"><span data-stu-id="c8efb-168">MP names</span></span>
* <span data-ttu-id="c8efb-169">Azure 媒體索引器 2 預覽</span><span class="sxs-lookup"><span data-stu-id="c8efb-169">Azure Media Indexer 2 Preview</span></span>
* <span data-ttu-id="c8efb-170">Azure Media Indexer</span><span class="sxs-lookup"><span data-stu-id="c8efb-170">Azure Media Indexer</span></span>
* <span data-ttu-id="c8efb-171">Azure Media Hyperlapse</span><span class="sxs-lookup"><span data-stu-id="c8efb-171">Azure Media Hyperlapse</span></span>
* <span data-ttu-id="c8efb-172">Azure 媒體臉部偵測器</span><span class="sxs-lookup"><span data-stu-id="c8efb-172">Azure Media Face Detector</span></span>
* <span data-ttu-id="c8efb-173">Azure 媒體動作偵測器</span><span class="sxs-lookup"><span data-stu-id="c8efb-173">Azure Media Motion Detector</span></span>
* <span data-ttu-id="c8efb-174">Azure 媒體視訊縮圖</span><span class="sxs-lookup"><span data-stu-id="c8efb-174">Azure Media Video Thumbnails</span></span>
* <span data-ttu-id="c8efb-175">Azure 媒體 OCR</span><span class="sxs-lookup"><span data-stu-id="c8efb-175">Azure Media OCR</span></span>

### <a name="net"></a><span data-ttu-id="c8efb-176">.NET</span><span class="sxs-lookup"><span data-stu-id="c8efb-176">.NET</span></span>
<span data-ttu-id="c8efb-177">下列函數會採用其中一個指定的 MP 名稱，並傳回 MP 物件。</span><span class="sxs-lookup"><span data-stu-id="c8efb-177">The following function takes one of the specified MP names and returns an MP object.</span></span>

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


### <a name="rest"></a><span data-ttu-id="c8efb-178">REST</span><span class="sxs-lookup"><span data-stu-id="c8efb-178">REST</span></span>
<span data-ttu-id="c8efb-179">要求：</span><span class="sxs-lookup"><span data-stu-id="c8efb-179">Request:</span></span>

    GET https://media.windows.net/api/MediaProcessors()?$filter=Name%20eq%20'Azure%20Media%20OCR' HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer <token>
    x-ms-version: 2.12
    Host: media.windows.net

<span data-ttu-id="c8efb-180">回應：</span><span class="sxs-lookup"><span data-stu-id="c8efb-180">Response:</span></span>

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

## <a name="demos"></a><span data-ttu-id="c8efb-181">示範</span><span class="sxs-lookup"><span data-stu-id="c8efb-181">Demos</span></span>
<span data-ttu-id="c8efb-182">請參閱 [Azure 媒體分析示範](http://azuremedialabs.azurewebsites.net/demos/Analytics.html)。</span><span class="sxs-lookup"><span data-stu-id="c8efb-182">See [Azure Media Analytics demos](http://azuremedialabs.azurewebsites.net/demos/Analytics.html).</span></span>

## <a name="next-steps"></a><span data-ttu-id="c8efb-183">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c8efb-183">Next steps</span></span>
<span data-ttu-id="c8efb-184">檢閱媒體服務學習路徑。</span><span class="sxs-lookup"><span data-stu-id="c8efb-184">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="c8efb-185">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="c8efb-185">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-articles"></a><span data-ttu-id="c8efb-186">相關文章</span><span class="sxs-lookup"><span data-stu-id="c8efb-186">Related articles</span></span>
<span data-ttu-id="c8efb-187">請參閱[媒體服務分析公告](https://azure.microsoft.com/blog/introducing-azure-media-analytics/)。</span><span class="sxs-lookup"><span data-stu-id="c8efb-187">See [Media Services Analytics announcement](https://azure.microsoft.com/blog/introducing-azure-media-analytics/).</span></span>

<!-- Images -->

[overview]: ./media/media-services-video-on-demand-workflow/media-services-video-on-demand.png
