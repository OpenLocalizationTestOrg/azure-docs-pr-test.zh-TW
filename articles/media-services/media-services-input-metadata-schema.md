---
title: "aaaAzure Media Services 輸入中繼資料結構描述 |Microsoft 文件"
description: "hello 主題提供 Azure Media Services 輸入中繼資料結構描述的概觀。"
author: Juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: d72848e2-4b65-4c84-94bc-e2a90a6e7f47
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: juliako
ms.openlocfilehash: 9b72c6ff317aa98451ea75548465dc6023b44a55
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="input-metadata"></a><span data-ttu-id="6d2f0-103">輸入中繼資料</span><span class="sxs-lookup"><span data-stu-id="6d2f0-103">Input Metadata</span></span>
<span data-ttu-id="6d2f0-104">輸入的資產或多個相關聯的編碼工作，是您想 tooperform 部分編碼工作。</span><span class="sxs-lookup"><span data-stu-id="6d2f0-104">An encoding job is associated with an input asset (or assets) on which you want tooperform some encoding tasks.</span></span>  <span data-ttu-id="6d2f0-105">完成工作時，就會產生輸出資產。</span><span class="sxs-lookup"><span data-stu-id="6d2f0-105">Upon completion of a task, an output asset is produced.</span></span>  <span data-ttu-id="6d2f0-106">hello 輸出資產包含視訊、 音訊、 縮圖、 資訊清單，等 hello 輸出資產也包含 hello 輸入資產的相關中繼資料檔案。</span><span class="sxs-lookup"><span data-stu-id="6d2f0-106">hello output asset contains video, audio, thumbnails, manifest, etc. hello output asset also contains a file with metadata about hello input asset.</span></span> <span data-ttu-id="6d2f0-107">hello hello 中繼資料 XML 檔案名稱具有下列格式的 hello: &lt;a&gt;_metadata.xml (例如，41114ad3-eb5e-4c 57-8 d 92-5354e2b7d4a4_metadata.xml)，其中&lt;a&gt;為 hello AssetIdhello 輸入資產的值。</span><span class="sxs-lookup"><span data-stu-id="6d2f0-107">hello name of hello metadata XML file has hello following format: &lt;asset_id&gt;_metadata.xml (for example, 41114ad3-eb5e-4c57-8d92-5354e2b7d4a4_metadata.xml), where &lt;asset_id&gt; is hello AssetId value of hello input asset.</span></span>  

<span data-ttu-id="6d2f0-108">如果您想 tooexamine hello 中繼資料檔案時，您可以建立**SAS**定位器和下載 hello 檔案 tooyour 本機電腦。</span><span class="sxs-lookup"><span data-stu-id="6d2f0-108">If you want tooexamine hello metadata file, you can create a **SAS** locator and download hello file tooyour local computer.</span></span> <span data-ttu-id="6d2f0-109">您可以找到範例如何 toocreate SAS 定位器和下載檔案[使用 hello Media Services.NET SDK Extensions](media-services-dotnet-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="6d2f0-109">You can find an example on how toocreate a SAS locator and download a file  [Using hello Media Services .NET SDK Extensions](media-services-dotnet-get-started.md).</span></span>  

<span data-ttu-id="6d2f0-110">本主題討論 hello 項目和 hello XML 結構描述的類型上的 hello 輸入中繼資料 (&lt;a&gt;_metadata.xml) 為基礎。</span><span class="sxs-lookup"><span data-stu-id="6d2f0-110">This topic discusses hello elements and types of hello XML schema on which hello input metada (&lt;asset_id&gt;_metadata.xml) is based.</span></span>  <span data-ttu-id="6d2f0-111">如需 hello 檔案，其中包含有關 hello 輸出資產的中繼資料資訊，請參閱[輸出中繼資料](media-services-output-metadata-schema.md)。</span><span class="sxs-lookup"><span data-stu-id="6d2f0-111">For information about hello file that contains metadata about hello output asset, see [Output Metadata](media-services-output-metadata-schema.md).</span></span>  

> [!NOTE]
> <span data-ttu-id="6d2f0-112">您可以找到 hello[結構描述程式碼](media-services-input-metadata-schema.md#code) [XML 範例](media-services-input-metadata-schema.md#xml)hello 本主題結尾處。</span><span class="sxs-lookup"><span data-stu-id="6d2f0-112">You can find hello [Schema Code](media-services-input-metadata-schema.md#code) an [XML example](media-services-input-metadata-schema.md#xml) at hello end of this topic.</span></span>  
> 
> 

## <span data-ttu-id="6d2f0-113"><a name="AssetFiles"></a> Assetfile 元素 (根元素)</span><span class="sxs-lookup"><span data-stu-id="6d2f0-113"><a name="AssetFiles"></a> AssetFiles element (root element)</span></span>
<span data-ttu-id="6d2f0-114">包含集合[AssetFile 元素](media-services-input-metadata-schema.md#AssetFile)s hello 編碼工作。</span><span class="sxs-lookup"><span data-stu-id="6d2f0-114">Contains a collection of [AssetFile element](media-services-input-metadata-schema.md#AssetFile)s for hello encoding job.</span></span>  

<span data-ttu-id="6d2f0-115">請參閱本主題的 hello 結尾 XML 範例： [XML 範例](media-services-input-metadata-schema.md#xml)。</span><span class="sxs-lookup"><span data-stu-id="6d2f0-115">See an XML example at hello end of this topic: [XML example](media-services-input-metadata-schema.md#xml).</span></span>  

| <span data-ttu-id="6d2f0-116">名稱</span><span class="sxs-lookup"><span data-stu-id="6d2f0-116">Name</span></span> | <span data-ttu-id="6d2f0-117">說明</span><span class="sxs-lookup"><span data-stu-id="6d2f0-117">Description</span></span> |
| --- | --- |
| <span data-ttu-id="6d2f0-118">**AssetFile**</span><span class="sxs-lookup"><span data-stu-id="6d2f0-118">**AssetFile**</span></span><br /><br /> <span data-ttu-id="6d2f0-119">minOccurs="1" maxOccurs="unbounded"</span><span class="sxs-lookup"><span data-stu-id="6d2f0-119">minOccurs="1" maxOccurs="unbounded"</span></span> |<span data-ttu-id="6d2f0-120">單一子元素。</span><span class="sxs-lookup"><span data-stu-id="6d2f0-120">A single child element.</span></span> <span data-ttu-id="6d2f0-121">如需詳細資訊，請參閱 [AssetFile 元素](media-services-input-metadata-schema.md#AssetFile)。</span><span class="sxs-lookup"><span data-stu-id="6d2f0-121">For more information, see [AssetFile element](media-services-input-metadata-schema.md#AssetFile).</span></span> |

## <span data-ttu-id="6d2f0-122"><a name="AssetFile"></a> AssetFile 元素</span><span class="sxs-lookup"><span data-stu-id="6d2f0-122"><a name="AssetFile"></a> AssetFile element</span></span>
 <span data-ttu-id="6d2f0-123">包含可描述資產檔案的屬性和元素。</span><span class="sxs-lookup"><span data-stu-id="6d2f0-123">Contains attributes and elements that describe an asset file.</span></span>  

 <span data-ttu-id="6d2f0-124">請參閱本主題的 hello 結尾 XML 範例： [XML 範例](media-services-input-metadata-schema.md#xml)。</span><span class="sxs-lookup"><span data-stu-id="6d2f0-124">See an XML example at hello end of this topic: [XML example](media-services-input-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="6d2f0-125">屬性</span><span class="sxs-lookup"><span data-stu-id="6d2f0-125">Attributes</span></span>
| <span data-ttu-id="6d2f0-126">名稱</span><span class="sxs-lookup"><span data-stu-id="6d2f0-126">Name</span></span> | <span data-ttu-id="6d2f0-127">類型</span><span class="sxs-lookup"><span data-stu-id="6d2f0-127">Type</span></span> | <span data-ttu-id="6d2f0-128">說明</span><span class="sxs-lookup"><span data-stu-id="6d2f0-128">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6d2f0-129">**名稱**</span><span class="sxs-lookup"><span data-stu-id="6d2f0-129">**Name**</span></span><br /><br /> <span data-ttu-id="6d2f0-130">必要</span><span class="sxs-lookup"><span data-stu-id="6d2f0-130">Required</span></span> |<span data-ttu-id="6d2f0-131">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="6d2f0-131">**xs:string**</span></span> |<span data-ttu-id="6d2f0-132">資產檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="6d2f0-132">Asset file name.</span></span> |
| <span data-ttu-id="6d2f0-133">**大小**</span><span class="sxs-lookup"><span data-stu-id="6d2f0-133">**Size**</span></span><br /><br /> <span data-ttu-id="6d2f0-134">必要</span><span class="sxs-lookup"><span data-stu-id="6d2f0-134">Required</span></span> |<span data-ttu-id="6d2f0-135">**xs:long**</span><span class="sxs-lookup"><span data-stu-id="6d2f0-135">**xs:long**</span></span> |<span data-ttu-id="6d2f0-136">Hello 資產檔案，以位元組為單位的大小。</span><span class="sxs-lookup"><span data-stu-id="6d2f0-136">Size of hello asset file in bytes.</span></span> |
| <span data-ttu-id="6d2f0-137">**Duration**</span><span class="sxs-lookup"><span data-stu-id="6d2f0-137">**Duration**</span></span><br /><br /> <span data-ttu-id="6d2f0-138">必要</span><span class="sxs-lookup"><span data-stu-id="6d2f0-138">Required</span></span> |<span data-ttu-id="6d2f0-139">**xs:duration**</span><span class="sxs-lookup"><span data-stu-id="6d2f0-139">**xs:duration**</span></span> |<span data-ttu-id="6d2f0-140">內容播放持續時間。</span><span class="sxs-lookup"><span data-stu-id="6d2f0-140">Content play back duration.</span></span> <span data-ttu-id="6d2f0-141">範例：Duration="PT25M37.757S"。</span><span class="sxs-lookup"><span data-stu-id="6d2f0-141">Example: Duration="PT25M37.757S".</span></span> |
| <span data-ttu-id="6d2f0-142">**NumberOfStreams**</span><span class="sxs-lookup"><span data-stu-id="6d2f0-142">**NumberOfStreams**</span></span><br /><br /> <span data-ttu-id="6d2f0-143">必要</span><span class="sxs-lookup"><span data-stu-id="6d2f0-143">Required</span></span> |<span data-ttu-id="6d2f0-144">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="6d2f0-144">**xs:int**</span></span> |<span data-ttu-id="6d2f0-145">Hello 資產檔案中的資料流數目。</span><span class="sxs-lookup"><span data-stu-id="6d2f0-145">Number of streams in hello asset file.</span></span> |
| <span data-ttu-id="6d2f0-146">**FormatNames**</span><span class="sxs-lookup"><span data-stu-id="6d2f0-146">**FormatNames**</span></span><br /><br /> <span data-ttu-id="6d2f0-147">必要</span><span class="sxs-lookup"><span data-stu-id="6d2f0-147">Required</span></span> |<span data-ttu-id="6d2f0-148">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="6d2f0-148">**xs:string**</span></span> |<span data-ttu-id="6d2f0-149">Format names.</span><span class="sxs-lookup"><span data-stu-id="6d2f0-149">Format names.</span></span> |
| <span data-ttu-id="6d2f0-150">**FormatVerboseNames**</span><span class="sxs-lookup"><span data-stu-id="6d2f0-150">**FormatVerboseNames**</span></span><br /><br /> <span data-ttu-id="6d2f0-151">必要</span><span class="sxs-lookup"><span data-stu-id="6d2f0-151">Required</span></span> |<span data-ttu-id="6d2f0-152">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="6d2f0-152">**xs:string**</span></span> |<span data-ttu-id="6d2f0-153">格式詳細資訊名稱。</span><span class="sxs-lookup"><span data-stu-id="6d2f0-153">Format verbose names.</span></span> |
| <span data-ttu-id="6d2f0-154">**StartTime**</span><span class="sxs-lookup"><span data-stu-id="6d2f0-154">**StartTime**</span></span> |<span data-ttu-id="6d2f0-155">**xs:duration**</span><span class="sxs-lookup"><span data-stu-id="6d2f0-155">**xs:duration**</span></span> |<span data-ttu-id="6d2f0-156">內容開始時間。</span><span class="sxs-lookup"><span data-stu-id="6d2f0-156">Content start time.</span></span> <span data-ttu-id="6d2f0-157">範例︰StartTime="PT2.669S"。</span><span class="sxs-lookup"><span data-stu-id="6d2f0-157">Example: StartTime="PT2.669S".</span></span> |
| <span data-ttu-id="6d2f0-158">**OverallBitRate**</span><span class="sxs-lookup"><span data-stu-id="6d2f0-158">**OverallBitRate**</span></span> |<span data-ttu-id="6d2f0-159">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="6d2f0-159">**xs:int**</span></span> |<span data-ttu-id="6d2f0-160">Hello 資產檔案，以 kbps 為單位的平均位元速率。</span><span class="sxs-lookup"><span data-stu-id="6d2f0-160">Average bitrate of hello asset file in kbps.</span></span> |

> [!NOTE]
> <span data-ttu-id="6d2f0-161">hello 下列 4 子元素必須循序出現。</span><span class="sxs-lookup"><span data-stu-id="6d2f0-161">hello following 4 child elements must appear in a sequence.</span></span>  
> 
> 

### <a name="child-elements"></a><span data-ttu-id="6d2f0-162">子元素</span><span class="sxs-lookup"><span data-stu-id="6d2f0-162">Child elements</span></span>
| <span data-ttu-id="6d2f0-163">名稱</span><span class="sxs-lookup"><span data-stu-id="6d2f0-163">Name</span></span> | <span data-ttu-id="6d2f0-164">類型</span><span class="sxs-lookup"><span data-stu-id="6d2f0-164">Type</span></span> | <span data-ttu-id="6d2f0-165">說明</span><span class="sxs-lookup"><span data-stu-id="6d2f0-165">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6d2f0-166">**Programs**</span><span class="sxs-lookup"><span data-stu-id="6d2f0-166">**Programs**</span></span><br /><br /> <span data-ttu-id="6d2f0-167">minOccurs="0"</span><span class="sxs-lookup"><span data-stu-id="6d2f0-167">minOccurs="0"</span></span> | |<span data-ttu-id="6d2f0-168">所有的集合[程式項目](media-services-input-metadata-schema.md#Programs)hello 資產檔案格式為 MPEG-TS 時。</span><span class="sxs-lookup"><span data-stu-id="6d2f0-168">Collection of all [Programs element](media-services-input-metadata-schema.md#Programs) when hello asset file is in MPEG-TS format.</span></span> |
| <span data-ttu-id="6d2f0-169">**VideoTracks**</span><span class="sxs-lookup"><span data-stu-id="6d2f0-169">**VideoTracks**</span></span><br /><br /> <span data-ttu-id="6d2f0-170">minOccurs="0"</span><span class="sxs-lookup"><span data-stu-id="6d2f0-170">minOccurs="0"</span></span> | |<span data-ttu-id="6d2f0-171">每個實體資產檔案可以包含零個或多個交錯形成適當容器格式的視訊播放軌。</span><span class="sxs-lookup"><span data-stu-id="6d2f0-171">Each physical asset file can contain zero or more video tracks interleaved into an appropriate container format.</span></span> <span data-ttu-id="6d2f0-172">這個項目包含所有的集合[Videotrack 元素](media-services-input-metadata-schema.md#VideoTracks)hello 資產檔案的一部分。</span><span class="sxs-lookup"><span data-stu-id="6d2f0-172">This element contains a collection of all [VideoTracks element](media-services-input-metadata-schema.md#VideoTracks) that are part of hello asset file.</span></span> |
| <span data-ttu-id="6d2f0-173">**AudioTracks**</span><span class="sxs-lookup"><span data-stu-id="6d2f0-173">**AudioTracks**</span></span><br /><br /> <span data-ttu-id="6d2f0-174">minOccurs="0"</span><span class="sxs-lookup"><span data-stu-id="6d2f0-174">minOccurs="0"</span></span> | |<span data-ttu-id="6d2f0-175">每個實體資產檔案可以包含零個或多個交錯形成適當容器格式的音訊播放軌。</span><span class="sxs-lookup"><span data-stu-id="6d2f0-175">Each physical asset file can contain zero or more audio tracks interleaved into an appropriate container format.</span></span> <span data-ttu-id="6d2f0-176">這個項目包含所有的集合[Audiotrack 元素](media-services-input-metadata-schema.md#AudioTracks)hello 資產檔案的一部分。</span><span class="sxs-lookup"><span data-stu-id="6d2f0-176">This element contains a collection of all [AudioTracks element](media-services-input-metadata-schema.md#AudioTracks) that are part of hello asset file.</span></span> |
| <span data-ttu-id="6d2f0-177">**Metadata**</span><span class="sxs-lookup"><span data-stu-id="6d2f0-177">**Metadata**</span></span><br /><br /> <span data-ttu-id="6d2f0-178">minOccurs="0" maxOccurs="unbounded"</span><span class="sxs-lookup"><span data-stu-id="6d2f0-178">minOccurs="0" maxOccurs="unbounded"</span></span> |[<span data-ttu-id="6d2f0-179">MetadataType</span><span class="sxs-lookup"><span data-stu-id="6d2f0-179">MetadataType</span></span>](media-services-input-metadata-schema.md#MetadataType) |<span data-ttu-id="6d2f0-180">資產檔案的中繼資料 (以索引鍵\值字串表示)。</span><span class="sxs-lookup"><span data-stu-id="6d2f0-180">Asset file’s metadata represented as key\value strings.</span></span> <span data-ttu-id="6d2f0-181">例如：</span><span class="sxs-lookup"><span data-stu-id="6d2f0-181">For example:</span></span><br /><br /> <span data-ttu-id="6d2f0-182">**&lt;Metadata key="language" value="eng" /&gt;**</span><span class="sxs-lookup"><span data-stu-id="6d2f0-182">**&lt;Metadata key="language" value="eng" /&gt;**</span></span> |

## <span data-ttu-id="6d2f0-183"><a name="TrackType"></a> TrackType</span><span class="sxs-lookup"><span data-stu-id="6d2f0-183"><a name="TrackType"></a> TrackType</span></span>
<span data-ttu-id="6d2f0-184">請參閱本主題的 hello 結尾 XML 範例： [XML 範例](media-services-input-metadata-schema.md#xml)。</span><span class="sxs-lookup"><span data-stu-id="6d2f0-184">See an XML example at hello end of this topic: [XML example](media-services-input-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="6d2f0-185">屬性</span><span class="sxs-lookup"><span data-stu-id="6d2f0-185">Attributes</span></span>
| <span data-ttu-id="6d2f0-186">名稱</span><span class="sxs-lookup"><span data-stu-id="6d2f0-186">Name</span></span> | <span data-ttu-id="6d2f0-187">類型</span><span class="sxs-lookup"><span data-stu-id="6d2f0-187">Type</span></span> | <span data-ttu-id="6d2f0-188">說明</span><span class="sxs-lookup"><span data-stu-id="6d2f0-188">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6d2f0-189">**Id**</span><span class="sxs-lookup"><span data-stu-id="6d2f0-189">**Id**</span></span><br /><br /> <span data-ttu-id="6d2f0-190">必要</span><span class="sxs-lookup"><span data-stu-id="6d2f0-190">Required</span></span> |<span data-ttu-id="6d2f0-191">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="6d2f0-191">**xs:int**</span></span> |<span data-ttu-id="6d2f0-192">此音訊或視訊播放軌之以零為起始的索引。</span><span class="sxs-lookup"><span data-stu-id="6d2f0-192">Zero-based index of this audio or video track.</span></span><br /><br /> <span data-ttu-id="6d2f0-193">這不一定是該 hello TrackID MP4 檔案中使用。</span><span class="sxs-lookup"><span data-stu-id="6d2f0-193">This is not necessarily that hello TrackID as used in an MP4 file.</span></span> |
| <span data-ttu-id="6d2f0-194">**Codec**</span><span class="sxs-lookup"><span data-stu-id="6d2f0-194">**Codec**</span></span> |<span data-ttu-id="6d2f0-195">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="6d2f0-195">**xs:string**</span></span> |<span data-ttu-id="6d2f0-196">視訊播放軌轉碼器字串。</span><span class="sxs-lookup"><span data-stu-id="6d2f0-196">Video track codec string.</span></span> |
| <span data-ttu-id="6d2f0-197">**CodecLongName**</span><span class="sxs-lookup"><span data-stu-id="6d2f0-197">**CodecLongName**</span></span> |<span data-ttu-id="6d2f0-198">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="6d2f0-198">**xs:string**</span></span> |<span data-ttu-id="6d2f0-199">音訊或視訊播放軌轉碼器長名稱。</span><span class="sxs-lookup"><span data-stu-id="6d2f0-199">Audio or video track codec long name.</span></span> |
| <span data-ttu-id="6d2f0-200">**TimeBase**</span><span class="sxs-lookup"><span data-stu-id="6d2f0-200">**TimeBase**</span></span><br /><br /> <span data-ttu-id="6d2f0-201">必要</span><span class="sxs-lookup"><span data-stu-id="6d2f0-201">Required</span></span> |<span data-ttu-id="6d2f0-202">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="6d2f0-202">**xs:string**</span></span> |<span data-ttu-id="6d2f0-203">時間基準。</span><span class="sxs-lookup"><span data-stu-id="6d2f0-203">Time base.</span></span> <span data-ttu-id="6d2f0-204">範例：TimeBase="1/48000"</span><span class="sxs-lookup"><span data-stu-id="6d2f0-204">Example: TimeBase="1/48000"</span></span> |
| <span data-ttu-id="6d2f0-205">**NumberOfFrames**</span><span class="sxs-lookup"><span data-stu-id="6d2f0-205">**NumberOfFrames**</span></span> |<span data-ttu-id="6d2f0-206">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="6d2f0-206">**xs:int**</span></span> |<span data-ttu-id="6d2f0-207">畫面格數 (針對視訊播放軌呈現)。</span><span class="sxs-lookup"><span data-stu-id="6d2f0-207">Number of frames (present for video tracks).</span></span> |
| <span data-ttu-id="6d2f0-208">**StartTime**</span><span class="sxs-lookup"><span data-stu-id="6d2f0-208">**StartTime**</span></span> |<span data-ttu-id="6d2f0-209">**xs:duration**</span><span class="sxs-lookup"><span data-stu-id="6d2f0-209">**xs:duration**</span></span> |<span data-ttu-id="6d2f0-210">播放軌開始時間。</span><span class="sxs-lookup"><span data-stu-id="6d2f0-210">Track start time.</span></span> <span data-ttu-id="6d2f0-211">範例︰StartTime="PT2.669S"</span><span class="sxs-lookup"><span data-stu-id="6d2f0-211">Example: StartTime="PT2.669S"</span></span> |
| <span data-ttu-id="6d2f0-212">**Duration**</span><span class="sxs-lookup"><span data-stu-id="6d2f0-212">**Duration**</span></span> |<span data-ttu-id="6d2f0-213">**xs:duration**</span><span class="sxs-lookup"><span data-stu-id="6d2f0-213">**xs:duration**</span></span> |<span data-ttu-id="6d2f0-214">播放軌持續時間。</span><span class="sxs-lookup"><span data-stu-id="6d2f0-214">Track duration.</span></span> <span data-ttu-id="6d2f0-215">範例：Duration="PTSampleFormat M37.757S"。</span><span class="sxs-lookup"><span data-stu-id="6d2f0-215">Example: Duration="PTSampleFormat M37.757S".</span></span> |

> [!NOTE]
> <span data-ttu-id="6d2f0-216">hello 下列 2 的子元素必須循序出現。</span><span class="sxs-lookup"><span data-stu-id="6d2f0-216">hello following 2 child elements must appear in a sequence.</span></span>  
> 
> 

### <a name="child-elements"></a><span data-ttu-id="6d2f0-217">子元素</span><span class="sxs-lookup"><span data-stu-id="6d2f0-217">Child elements</span></span>
| <span data-ttu-id="6d2f0-218">名稱</span><span class="sxs-lookup"><span data-stu-id="6d2f0-218">Name</span></span> | <span data-ttu-id="6d2f0-219">類型</span><span class="sxs-lookup"><span data-stu-id="6d2f0-219">Type</span></span> | <span data-ttu-id="6d2f0-220">說明</span><span class="sxs-lookup"><span data-stu-id="6d2f0-220">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6d2f0-221">**Disposition**</span><span class="sxs-lookup"><span data-stu-id="6d2f0-221">**Disposition**</span></span><br /><br /> <span data-ttu-id="6d2f0-222">minOccurs="0" maxOccurs="1"</span><span class="sxs-lookup"><span data-stu-id="6d2f0-222">minOccurs="0" maxOccurs="1"</span></span> |[<span data-ttu-id="6d2f0-223">StreamDispositionType</span><span class="sxs-lookup"><span data-stu-id="6d2f0-223">StreamDispositionType</span></span>](media-services-input-metadata-schema.md#StreamDispositionType) |<span data-ttu-id="6d2f0-224">包含簡報資訊 (例如，特定音訊播放軌是否適用於視障者)。</span><span class="sxs-lookup"><span data-stu-id="6d2f0-224">Contains presentation information (for example, whether a particular audio track is for visually impaired viewers).</span></span> |
| <span data-ttu-id="6d2f0-225">**Metadata**</span><span class="sxs-lookup"><span data-stu-id="6d2f0-225">**Metadata**</span></span><br /><br /> <span data-ttu-id="6d2f0-226">minOccurs="0" maxOccurs="unbounded"</span><span class="sxs-lookup"><span data-stu-id="6d2f0-226">minOccurs="0" maxOccurs="unbounded"</span></span> |[<span data-ttu-id="6d2f0-227">MetadataType</span><span class="sxs-lookup"><span data-stu-id="6d2f0-227">MetadataType</span></span>](media-services-input-metadata-schema.md#MetadataType) |<span data-ttu-id="6d2f0-228">可以是使用的 toohold 的各種資訊的泛用的索引鍵/值字串。</span><span class="sxs-lookup"><span data-stu-id="6d2f0-228">Generic key/value strings that can be used toohold a variety of information.</span></span> <span data-ttu-id="6d2f0-229">例如，key=”language” 和 value=”eng”。</span><span class="sxs-lookup"><span data-stu-id="6d2f0-229">For example, key=”language”, and value=”eng”.</span></span> |

## <span data-ttu-id="6d2f0-230"><a name="AudioTrackType"></a> AudioTrackType (繼承自 TrackType)</span><span class="sxs-lookup"><span data-stu-id="6d2f0-230"><a name="AudioTrackType"></a> AudioTrackType (inherits from TrackType)</span></span>
 <span data-ttu-id="6d2f0-231">**AudioTrackType** 是全域複雜類型，其繼承自 [TrackType](media-services-input-metadata-schema.md#TrackType)。</span><span class="sxs-lookup"><span data-stu-id="6d2f0-231">**AudioTrackType** is a global complex type that inherits from [TrackType](media-services-input-metadata-schema.md#TrackType).</span></span>  

 <span data-ttu-id="6d2f0-232">hello 類型代表 hello 資產檔案中的特定音訊音軌。</span><span class="sxs-lookup"><span data-stu-id="6d2f0-232">hello type represents a specific audio track in hello asset file.</span></span>  

 <span data-ttu-id="6d2f0-233">請參閱本主題的 hello 結尾 XML 範例： [XML 範例](media-services-input-metadata-schema.md#xml)。</span><span class="sxs-lookup"><span data-stu-id="6d2f0-233">See an XML example at hello end of this topic: [XML example](media-services-input-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="6d2f0-234">屬性</span><span class="sxs-lookup"><span data-stu-id="6d2f0-234">Attributes</span></span>
| <span data-ttu-id="6d2f0-235">名稱</span><span class="sxs-lookup"><span data-stu-id="6d2f0-235">Name</span></span> | <span data-ttu-id="6d2f0-236">類型</span><span class="sxs-lookup"><span data-stu-id="6d2f0-236">Type</span></span> | <span data-ttu-id="6d2f0-237">說明</span><span class="sxs-lookup"><span data-stu-id="6d2f0-237">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6d2f0-238">**SampleFormat**</span><span class="sxs-lookup"><span data-stu-id="6d2f0-238">**SampleFormat**</span></span> |<span data-ttu-id="6d2f0-239">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="6d2f0-239">**xs:string**</span></span> |<span data-ttu-id="6d2f0-240">樣本格式。</span><span class="sxs-lookup"><span data-stu-id="6d2f0-240">Sample format.</span></span> |
| <span data-ttu-id="6d2f0-241">**ChannelLayout**</span><span class="sxs-lookup"><span data-stu-id="6d2f0-241">**ChannelLayout**</span></span> |<span data-ttu-id="6d2f0-242">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="6d2f0-242">**xs:string**</span></span> |<span data-ttu-id="6d2f0-243">聲道配置。</span><span class="sxs-lookup"><span data-stu-id="6d2f0-243">Channel layout.</span></span> |
| <span data-ttu-id="6d2f0-244">**Channels**</span><span class="sxs-lookup"><span data-stu-id="6d2f0-244">**Channels**</span></span><br /><br /> <span data-ttu-id="6d2f0-245">必要</span><span class="sxs-lookup"><span data-stu-id="6d2f0-245">Required</span></span> |<span data-ttu-id="6d2f0-246">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="6d2f0-246">**xs:int**</span></span> |<span data-ttu-id="6d2f0-247">音訊聲道數目 (0 個或多個)。</span><span class="sxs-lookup"><span data-stu-id="6d2f0-247">Number (0 or more) of audio channels.</span></span> |
| <span data-ttu-id="6d2f0-248">**SamplingRate**</span><span class="sxs-lookup"><span data-stu-id="6d2f0-248">**SamplingRate**</span></span><br /><br /> <span data-ttu-id="6d2f0-249">必要</span><span class="sxs-lookup"><span data-stu-id="6d2f0-249">Required</span></span> |<span data-ttu-id="6d2f0-250">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="6d2f0-250">**xs:int**</span></span> |<span data-ttu-id="6d2f0-251">音訊取樣率 (每秒或每 Hz 的樣本數)。</span><span class="sxs-lookup"><span data-stu-id="6d2f0-251">Audio sampling rate in samples/sec or Hz.</span></span> |
| <span data-ttu-id="6d2f0-252">**Bitrate**</span><span class="sxs-lookup"><span data-stu-id="6d2f0-252">**Bitrate**</span></span> |<span data-ttu-id="6d2f0-253">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="6d2f0-253">**xs:int**</span></span> |<span data-ttu-id="6d2f0-254">音訊平均位元速率，以每秒位元，以從 hello 資產檔案計算而得。</span><span class="sxs-lookup"><span data-stu-id="6d2f0-254">Average audio bit rate in bits per second, as calculated from hello asset file.</span></span> <span data-ttu-id="6d2f0-255">計算 hello 基本資料流裝載，以及這個計數不包含 hello 封裝負荷。</span><span class="sxs-lookup"><span data-stu-id="6d2f0-255">Only hello elementary stream payload is counted, and hello packaging overhead is not included in this count.</span></span> |
| <span data-ttu-id="6d2f0-256">**BitsPerSample**</span><span class="sxs-lookup"><span data-stu-id="6d2f0-256">**BitsPerSample**</span></span> |<span data-ttu-id="6d2f0-257">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="6d2f0-257">**xs:int**</span></span> |<span data-ttu-id="6d2f0-258">位元，每個範例的 hello wFormatTag 格式類型。</span><span class="sxs-lookup"><span data-stu-id="6d2f0-258">Bits per sample for hello wFormatTag format type.</span></span> |

## <span data-ttu-id="6d2f0-259"><a name="VideoTrackType"></a> VideoTrackType (繼承自 TrackType)</span><span class="sxs-lookup"><span data-stu-id="6d2f0-259"><a name="VideoTrackType"></a> VideoTrackType (inherits from TrackType)</span></span>
<span data-ttu-id="6d2f0-260">**VideoTrackType** 是全域複雜類型，其繼承自 [TrackType](media-services-input-metadata-schema.md#TrackType)。</span><span class="sxs-lookup"><span data-stu-id="6d2f0-260">**VideoTrackType** is a global complex type that inherits from [TrackType](media-services-input-metadata-schema.md#TrackType).</span></span>  

<span data-ttu-id="6d2f0-261">hello 類型代表 hello 資產檔案中的特定視訊音軌。</span><span class="sxs-lookup"><span data-stu-id="6d2f0-261">hello type represents a specific video track in hello asset file.</span></span>  

<span data-ttu-id="6d2f0-262">請參閱本主題的 hello 結尾 XML 範例： [XML 範例](media-services-input-metadata-schema.md#xml)。</span><span class="sxs-lookup"><span data-stu-id="6d2f0-262">See an XML example at hello end of this topic: [XML example](media-services-input-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="6d2f0-263">屬性</span><span class="sxs-lookup"><span data-stu-id="6d2f0-263">Attributes</span></span>
| <span data-ttu-id="6d2f0-264">名稱</span><span class="sxs-lookup"><span data-stu-id="6d2f0-264">Name</span></span> | <span data-ttu-id="6d2f0-265">類型</span><span class="sxs-lookup"><span data-stu-id="6d2f0-265">Type</span></span> | <span data-ttu-id="6d2f0-266">說明</span><span class="sxs-lookup"><span data-stu-id="6d2f0-266">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6d2f0-267">**FourCC**</span><span class="sxs-lookup"><span data-stu-id="6d2f0-267">**FourCC**</span></span><br /><br /> <span data-ttu-id="6d2f0-268">必要</span><span class="sxs-lookup"><span data-stu-id="6d2f0-268">Required</span></span> |<span data-ttu-id="6d2f0-269">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="6d2f0-269">**xs:string**</span></span> |<span data-ttu-id="6d2f0-270">視訊轉碼器 FourCC 代碼。</span><span class="sxs-lookup"><span data-stu-id="6d2f0-270">Video codec FourCC code.</span></span> |
| <span data-ttu-id="6d2f0-271">**設定檔**</span><span class="sxs-lookup"><span data-stu-id="6d2f0-271">**Profile**</span></span> |<span data-ttu-id="6d2f0-272">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="6d2f0-272">**xs:string**</span></span> |<span data-ttu-id="6d2f0-273">視訊播放軌的設定檔。</span><span class="sxs-lookup"><span data-stu-id="6d2f0-273">Video track's profile.</span></span> |
| <span data-ttu-id="6d2f0-274">**Level**</span><span class="sxs-lookup"><span data-stu-id="6d2f0-274">**Level**</span></span> |<span data-ttu-id="6d2f0-275">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="6d2f0-275">**xs:string**</span></span> |<span data-ttu-id="6d2f0-276">視訊播放軌的層級。</span><span class="sxs-lookup"><span data-stu-id="6d2f0-276">Video track's level.</span></span> |
| <span data-ttu-id="6d2f0-277">**PixelFormat**</span><span class="sxs-lookup"><span data-stu-id="6d2f0-277">**PixelFormat**</span></span> |<span data-ttu-id="6d2f0-278">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="6d2f0-278">**xs:string**</span></span> |<span data-ttu-id="6d2f0-279">視訊播放軌的像素格式。</span><span class="sxs-lookup"><span data-stu-id="6d2f0-279">Video track's pixel format.</span></span> |
| <span data-ttu-id="6d2f0-280">**Width**</span><span class="sxs-lookup"><span data-stu-id="6d2f0-280">**Width**</span></span><br /><br /> <span data-ttu-id="6d2f0-281">必要</span><span class="sxs-lookup"><span data-stu-id="6d2f0-281">Required</span></span> |<span data-ttu-id="6d2f0-282">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="6d2f0-282">**xs:int**</span></span> |<span data-ttu-id="6d2f0-283">編碼的視訊寬度 (以像素為單位)。</span><span class="sxs-lookup"><span data-stu-id="6d2f0-283">Encoded video width in pixels.</span></span> |
| <span data-ttu-id="6d2f0-284">**Height**</span><span class="sxs-lookup"><span data-stu-id="6d2f0-284">**Height**</span></span><br /><br /> <span data-ttu-id="6d2f0-285">必要</span><span class="sxs-lookup"><span data-stu-id="6d2f0-285">Required</span></span> |<span data-ttu-id="6d2f0-286">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="6d2f0-286">**xs:int**</span></span> |<span data-ttu-id="6d2f0-287">編碼的視訊高度 (以像素為單位)。</span><span class="sxs-lookup"><span data-stu-id="6d2f0-287">Encoded video height in pixels.</span></span> |
| <span data-ttu-id="6d2f0-288">**DisplayAspectRatioNumerator**</span><span class="sxs-lookup"><span data-stu-id="6d2f0-288">**DisplayAspectRatioNumerator**</span></span><br /><br /> <span data-ttu-id="6d2f0-289">必要</span><span class="sxs-lookup"><span data-stu-id="6d2f0-289">Required</span></span> |<span data-ttu-id="6d2f0-290">**xs:double**</span><span class="sxs-lookup"><span data-stu-id="6d2f0-290">**xs:double**</span></span> |<span data-ttu-id="6d2f0-291">視訊顯示長寬比的分子。</span><span class="sxs-lookup"><span data-stu-id="6d2f0-291">Video display aspect ratio numerator.</span></span> |
| <span data-ttu-id="6d2f0-292">**DisplayAspectRatioDenominator**</span><span class="sxs-lookup"><span data-stu-id="6d2f0-292">**DisplayAspectRatioDenominator**</span></span><br /><br /> <span data-ttu-id="6d2f0-293">必要</span><span class="sxs-lookup"><span data-stu-id="6d2f0-293">Required</span></span> |<span data-ttu-id="6d2f0-294">**xs:double**</span><span class="sxs-lookup"><span data-stu-id="6d2f0-294">**xs:double**</span></span> |<span data-ttu-id="6d2f0-295">視訊顯示長寬比的分母。</span><span class="sxs-lookup"><span data-stu-id="6d2f0-295">Video display aspect ratio denominator.</span></span> |
| <span data-ttu-id="6d2f0-296">**DisplayAspectRatioDenominator**</span><span class="sxs-lookup"><span data-stu-id="6d2f0-296">**DisplayAspectRatioDenominator**</span></span><br /><br /> <span data-ttu-id="6d2f0-297">必要</span><span class="sxs-lookup"><span data-stu-id="6d2f0-297">Required</span></span> |<span data-ttu-id="6d2f0-298">**xs:double**</span><span class="sxs-lookup"><span data-stu-id="6d2f0-298">**xs:double**</span></span> |<span data-ttu-id="6d2f0-299">視訊樣本長寬比的分子。</span><span class="sxs-lookup"><span data-stu-id="6d2f0-299">Video sample aspect ratio numerator.</span></span> |
| <span data-ttu-id="6d2f0-300">**SampleAspectRatioNumerator**</span><span class="sxs-lookup"><span data-stu-id="6d2f0-300">**SampleAspectRatioNumerator**</span></span> |<span data-ttu-id="6d2f0-301">**xs:double**</span><span class="sxs-lookup"><span data-stu-id="6d2f0-301">**xs:double**</span></span> |<span data-ttu-id="6d2f0-302">視訊樣本長寬比的分子。</span><span class="sxs-lookup"><span data-stu-id="6d2f0-302">Video sample aspect ratio numerator.</span></span> |
| <span data-ttu-id="6d2f0-303">**SampleAspectRatioNumerator**</span><span class="sxs-lookup"><span data-stu-id="6d2f0-303">**SampleAspectRatioNumerator**</span></span> |<span data-ttu-id="6d2f0-304">**xs:double**</span><span class="sxs-lookup"><span data-stu-id="6d2f0-304">**xs:double**</span></span> |<span data-ttu-id="6d2f0-305">視訊樣本長寬比的分母。</span><span class="sxs-lookup"><span data-stu-id="6d2f0-305">Video sample aspect ratio denominator.</span></span> |
| <span data-ttu-id="6d2f0-306">**FrameRate**</span><span class="sxs-lookup"><span data-stu-id="6d2f0-306">**FrameRate**</span></span><br /><br /> <span data-ttu-id="6d2f0-307">必要</span><span class="sxs-lookup"><span data-stu-id="6d2f0-307">Required</span></span> |<span data-ttu-id="6d2f0-308">**xs:decimal**</span><span class="sxs-lookup"><span data-stu-id="6d2f0-308">**xs:decimal**</span></span> |<span data-ttu-id="6d2f0-309">測量的視訊畫面格速率 (採用 .3f 格式)。</span><span class="sxs-lookup"><span data-stu-id="6d2f0-309">Measured video frame rate in .3f format.</span></span> |
| <span data-ttu-id="6d2f0-310">**Bitrate**</span><span class="sxs-lookup"><span data-stu-id="6d2f0-310">**Bitrate**</span></span> |<span data-ttu-id="6d2f0-311">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="6d2f0-311">**xs:int**</span></span> |<span data-ttu-id="6d2f0-312">視訊平均位元速率，以 kb / 秒，為從 hello 資產檔案計算而得。</span><span class="sxs-lookup"><span data-stu-id="6d2f0-312">Average video bit rate in kilobits per second, as calculated from hello asset file.</span></span> <span data-ttu-id="6d2f0-313">計算 hello 基本資料流裝載，並不包含 hello 封裝負荷。</span><span class="sxs-lookup"><span data-stu-id="6d2f0-313">Only hello elementary stream payload is counted, and hello packaging overhead is not included.</span></span> |
| <span data-ttu-id="6d2f0-314">**MaxGOPBitrate**</span><span class="sxs-lookup"><span data-stu-id="6d2f0-314">**MaxGOPBitrate**</span></span> |<span data-ttu-id="6d2f0-315">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="6d2f0-315">**xs:int**</span></span> |<span data-ttu-id="6d2f0-316">此視訊播放軌的最大 GOP 平均位元速率 (千位元 / 秒)。</span><span class="sxs-lookup"><span data-stu-id="6d2f0-316">Max GOP average bitrate for this video track, in kilobits per second.</span></span> |
| <span data-ttu-id="6d2f0-317">**HasBFrames**</span><span class="sxs-lookup"><span data-stu-id="6d2f0-317">**HasBFrames**</span></span> |<span data-ttu-id="6d2f0-318">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="6d2f0-318">**xs:int**</span></span> |<span data-ttu-id="6d2f0-319">B 畫面格的視訊播放軌數目。</span><span class="sxs-lookup"><span data-stu-id="6d2f0-319">Video track number of B frames.</span></span> |

## <span data-ttu-id="6d2f0-320"><a name="MetadataType"></a> MetadataType</span><span class="sxs-lookup"><span data-stu-id="6d2f0-320"><a name="MetadataType"></a> MetadataType</span></span>
<span data-ttu-id="6d2f0-321">**MetadataType** 是全域複雜類型，其以索引鍵/值字串的形式描述資產檔案的中繼資料。</span><span class="sxs-lookup"><span data-stu-id="6d2f0-321">**MetadataType** is a global complex type that describes metadata of an asset file as key/value strings.</span></span> <span data-ttu-id="6d2f0-322">例如，key=”language” 和 value=”eng”。</span><span class="sxs-lookup"><span data-stu-id="6d2f0-322">For example, key=”language”, and value=”eng”.</span></span>  

<span data-ttu-id="6d2f0-323">請參閱本主題的 hello 結尾 XML 範例： [XML 範例](media-services-input-metadata-schema.md#xml)。</span><span class="sxs-lookup"><span data-stu-id="6d2f0-323">See an XML example at hello end of this topic: [XML example](media-services-input-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="6d2f0-324">屬性</span><span class="sxs-lookup"><span data-stu-id="6d2f0-324">Attributes</span></span>
| <span data-ttu-id="6d2f0-325">名稱</span><span class="sxs-lookup"><span data-stu-id="6d2f0-325">Name</span></span> | <span data-ttu-id="6d2f0-326">類型</span><span class="sxs-lookup"><span data-stu-id="6d2f0-326">Type</span></span> | <span data-ttu-id="6d2f0-327">說明</span><span class="sxs-lookup"><span data-stu-id="6d2f0-327">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6d2f0-328">**key**</span><span class="sxs-lookup"><span data-stu-id="6d2f0-328">**key**</span></span><br /><br /> <span data-ttu-id="6d2f0-329">必要</span><span class="sxs-lookup"><span data-stu-id="6d2f0-329">Required</span></span> |<span data-ttu-id="6d2f0-330">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="6d2f0-330">**xs:string**</span></span> |<span data-ttu-id="6d2f0-331">hello 索引鍵/值組中的 hello 索引鍵。</span><span class="sxs-lookup"><span data-stu-id="6d2f0-331">hello key in hello key/value pair.</span></span> |
| <span data-ttu-id="6d2f0-332">**value**</span><span class="sxs-lookup"><span data-stu-id="6d2f0-332">**value**</span></span><br /><br /> <span data-ttu-id="6d2f0-333">必要</span><span class="sxs-lookup"><span data-stu-id="6d2f0-333">Required</span></span> |<span data-ttu-id="6d2f0-334">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="6d2f0-334">**xs:string**</span></span> |<span data-ttu-id="6d2f0-335">hello 索引鍵/值組中的 hello 值。</span><span class="sxs-lookup"><span data-stu-id="6d2f0-335">hello value in hello key/value pair.</span></span> |

## <span data-ttu-id="6d2f0-336"><a name="ProgramType"></a> ProgramType</span><span class="sxs-lookup"><span data-stu-id="6d2f0-336"><a name="ProgramType"></a> ProgramType</span></span>
<span data-ttu-id="6d2f0-337">**ProgramType** 是用來描述節目的全域複雜類型。</span><span class="sxs-lookup"><span data-stu-id="6d2f0-337">**ProgramType** is a global complex type that describes a program.</span></span>  

### <a name="attributes"></a><span data-ttu-id="6d2f0-338">屬性</span><span class="sxs-lookup"><span data-stu-id="6d2f0-338">Attributes</span></span>
| <span data-ttu-id="6d2f0-339">名稱</span><span class="sxs-lookup"><span data-stu-id="6d2f0-339">Name</span></span> | <span data-ttu-id="6d2f0-340">類型</span><span class="sxs-lookup"><span data-stu-id="6d2f0-340">Type</span></span> | <span data-ttu-id="6d2f0-341">說明</span><span class="sxs-lookup"><span data-stu-id="6d2f0-341">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6d2f0-342">**ProgramId**</span><span class="sxs-lookup"><span data-stu-id="6d2f0-342">**ProgramId**</span></span><br /><br /> <span data-ttu-id="6d2f0-343">必要</span><span class="sxs-lookup"><span data-stu-id="6d2f0-343">Required</span></span> |<span data-ttu-id="6d2f0-344">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="6d2f0-344">**xs:int**</span></span> |<span data-ttu-id="6d2f0-345">Program Id</span><span class="sxs-lookup"><span data-stu-id="6d2f0-345">Program Id</span></span> |
| <span data-ttu-id="6d2f0-346">**NumberOfPrograms**</span><span class="sxs-lookup"><span data-stu-id="6d2f0-346">**NumberOfPrograms**</span></span><br /><br /> <span data-ttu-id="6d2f0-347">必要</span><span class="sxs-lookup"><span data-stu-id="6d2f0-347">Required</span></span> |<span data-ttu-id="6d2f0-348">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="6d2f0-348">**xs:int**</span></span> |<span data-ttu-id="6d2f0-349">節目數量。</span><span class="sxs-lookup"><span data-stu-id="6d2f0-349">Number of programs.</span></span> |
| <span data-ttu-id="6d2f0-350">**PmtPid**</span><span class="sxs-lookup"><span data-stu-id="6d2f0-350">**PmtPid**</span></span><br /><br /> <span data-ttu-id="6d2f0-351">必要</span><span class="sxs-lookup"><span data-stu-id="6d2f0-351">Required</span></span> |<span data-ttu-id="6d2f0-352">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="6d2f0-352">**xs:int**</span></span> |<span data-ttu-id="6d2f0-353">節目對應表 (PMT) 包含節目相關資訊。</span><span class="sxs-lookup"><span data-stu-id="6d2f0-353">Program Map Tables (PMTs) contain information about programs.</span></span>  <span data-ttu-id="6d2f0-354">如需詳細資訊，請參閱 [PMt](http://en.wikipedia.org/wiki/MPEG_transport_stream#PMT)。</span><span class="sxs-lookup"><span data-stu-id="6d2f0-354">For more information, see [PMt](http://en.wikipedia.org/wiki/MPEG_transport_stream#PMT).</span></span> |
| <span data-ttu-id="6d2f0-355">**PcrPid**</span><span class="sxs-lookup"><span data-stu-id="6d2f0-355">**PcrPid**</span></span><br /><br /> <span data-ttu-id="6d2f0-356">必要</span><span class="sxs-lookup"><span data-stu-id="6d2f0-356">Required</span></span> |<span data-ttu-id="6d2f0-357">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="6d2f0-357">**xs:int**</span></span> |<span data-ttu-id="6d2f0-358">由解碼器使用。</span><span class="sxs-lookup"><span data-stu-id="6d2f0-358">Used by decoder.</span></span> <span data-ttu-id="6d2f0-359">如需詳細資訊，請參閱 [PCR](http://en.wikipedia.org/wiki/MPEG_transport_stream#PCR)</span><span class="sxs-lookup"><span data-stu-id="6d2f0-359">For more information, see [PCR](http://en.wikipedia.org/wiki/MPEG_transport_stream#PCR)</span></span> |
| <span data-ttu-id="6d2f0-360">**StartPTS**</span><span class="sxs-lookup"><span data-stu-id="6d2f0-360">**StartPTS**</span></span> |<span data-ttu-id="6d2f0-361">**xs: long**</span><span class="sxs-lookup"><span data-stu-id="6d2f0-361">**xs: long**</span></span> |<span data-ttu-id="6d2f0-362">啟動簡報時間戳記。</span><span class="sxs-lookup"><span data-stu-id="6d2f0-362">Starting presentation time stamp.</span></span> |
| <span data-ttu-id="6d2f0-363">**EndPTS**</span><span class="sxs-lookup"><span data-stu-id="6d2f0-363">**EndPTS**</span></span> |<span data-ttu-id="6d2f0-364">**xs: long**</span><span class="sxs-lookup"><span data-stu-id="6d2f0-364">**xs: long**</span></span> |<span data-ttu-id="6d2f0-365">結束簡報時間戳記。</span><span class="sxs-lookup"><span data-stu-id="6d2f0-365">Ending presentation time stamp.</span></span> |

## <span data-ttu-id="6d2f0-366"><a name="StreamDispositionType"></a> StreamDispositionType</span><span class="sxs-lookup"><span data-stu-id="6d2f0-366"><a name="StreamDispositionType"></a> StreamDispositionType</span></span>
<span data-ttu-id="6d2f0-367">**StreamDispositionType**是描述 hello 資料流的全域複雜類型。</span><span class="sxs-lookup"><span data-stu-id="6d2f0-367">**StreamDispositionType** is a global complex type that describes hello stream.</span></span>  

<span data-ttu-id="6d2f0-368">請參閱本主題的 hello 結尾 XML 範例： [XML 範例](media-services-input-metadata-schema.md#xml)。</span><span class="sxs-lookup"><span data-stu-id="6d2f0-368">See an XML example at hello end of this topic: [XML example](media-services-input-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="6d2f0-369">屬性</span><span class="sxs-lookup"><span data-stu-id="6d2f0-369">Attributes</span></span>
| <span data-ttu-id="6d2f0-370">名稱</span><span class="sxs-lookup"><span data-stu-id="6d2f0-370">Name</span></span> | <span data-ttu-id="6d2f0-371">類型</span><span class="sxs-lookup"><span data-stu-id="6d2f0-371">Type</span></span> | <span data-ttu-id="6d2f0-372">說明</span><span class="sxs-lookup"><span data-stu-id="6d2f0-372">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6d2f0-373">**預設值**</span><span class="sxs-lookup"><span data-stu-id="6d2f0-373">**Default**</span></span><br /><br /> <span data-ttu-id="6d2f0-374">必要</span><span class="sxs-lookup"><span data-stu-id="6d2f0-374">Required</span></span> |<span data-ttu-id="6d2f0-375">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="6d2f0-375">**xs:int**</span></span> |<span data-ttu-id="6d2f0-376">設定這是此屬性 too1 tooindicate hello 預設呈現方式。</span><span class="sxs-lookup"><span data-stu-id="6d2f0-376">Set this attribute too1 tooindicate this is hello default presentation.</span></span> |
| <span data-ttu-id="6d2f0-377">**Dub**</span><span class="sxs-lookup"><span data-stu-id="6d2f0-377">**Dub**</span></span><br /><br /> <span data-ttu-id="6d2f0-378">必要</span><span class="sxs-lookup"><span data-stu-id="6d2f0-378">Required</span></span> |<span data-ttu-id="6d2f0-379">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="6d2f0-379">**xs:int**</span></span> |<span data-ttu-id="6d2f0-380">設定此屬性 too1 tooindicate hello 名簡報。</span><span class="sxs-lookup"><span data-stu-id="6d2f0-380">Set this attribute too1 tooindicate this is hello dubbed presentation.</span></span> |
| <span data-ttu-id="6d2f0-381">**Original**</span><span class="sxs-lookup"><span data-stu-id="6d2f0-381">**Original**</span></span><br /><br /> <span data-ttu-id="6d2f0-382">必要</span><span class="sxs-lookup"><span data-stu-id="6d2f0-382">Required</span></span> |<span data-ttu-id="6d2f0-383">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="6d2f0-383">**xs:int**</span></span> |<span data-ttu-id="6d2f0-384">設定這是此屬性 too1 tooindicate hello 原始簡報。</span><span class="sxs-lookup"><span data-stu-id="6d2f0-384">Set this attribute too1 tooindicate this is hello original presentation.</span></span> |
| <span data-ttu-id="6d2f0-385">**Comment**</span><span class="sxs-lookup"><span data-stu-id="6d2f0-385">**Comment**</span></span><br /><br /> <span data-ttu-id="6d2f0-386">必要</span><span class="sxs-lookup"><span data-stu-id="6d2f0-386">Required</span></span> |<span data-ttu-id="6d2f0-387">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="6d2f0-387">**xs:int**</span></span> |<span data-ttu-id="6d2f0-388">設定此屬性 too1 tooindicate 此音軌包含評論。</span><span class="sxs-lookup"><span data-stu-id="6d2f0-388">Set this attribute too1 tooindicate this track contains commentary.</span></span> |
| <span data-ttu-id="6d2f0-389">**Lyrics**</span><span class="sxs-lookup"><span data-stu-id="6d2f0-389">**Lyrics**</span></span><br /><br /> <span data-ttu-id="6d2f0-390">必要</span><span class="sxs-lookup"><span data-stu-id="6d2f0-390">Required</span></span> |<span data-ttu-id="6d2f0-391">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="6d2f0-391">**xs:int**</span></span> |<span data-ttu-id="6d2f0-392">設定此屬性 too1 tooindicate 此音軌包含歌詞。</span><span class="sxs-lookup"><span data-stu-id="6d2f0-392">Set this attribute too1 tooindicate this track contains lyrics.</span></span> |
| <span data-ttu-id="6d2f0-393">**Karaoke**</span><span class="sxs-lookup"><span data-stu-id="6d2f0-393">**Karaoke**</span></span><br /><br /> <span data-ttu-id="6d2f0-394">必要</span><span class="sxs-lookup"><span data-stu-id="6d2f0-394">Required</span></span> |<span data-ttu-id="6d2f0-395">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="6d2f0-395">**xs:int**</span></span> |<span data-ttu-id="6d2f0-396">設定此屬性 too1 tooindicate 這代表 hello 伴唱帶音軌 （背景音樂、 無人聲）。</span><span class="sxs-lookup"><span data-stu-id="6d2f0-396">Set this attribute too1 tooindicate this represents hello karaoke track (background music, no vocals).</span></span> |
| <span data-ttu-id="6d2f0-397">**Forced**</span><span class="sxs-lookup"><span data-stu-id="6d2f0-397">**Forced**</span></span><br /><br /> <span data-ttu-id="6d2f0-398">必要</span><span class="sxs-lookup"><span data-stu-id="6d2f0-398">Required</span></span> |<span data-ttu-id="6d2f0-399">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="6d2f0-399">**xs:int**</span></span> |<span data-ttu-id="6d2f0-400">設定此屬性 too1 tooindicate，這是強制的 hello 簡報。</span><span class="sxs-lookup"><span data-stu-id="6d2f0-400">Set this attribute too1 tooindicate this is hello forced presentation.</span></span> |
| <span data-ttu-id="6d2f0-401">**HearingImpaired**</span><span class="sxs-lookup"><span data-stu-id="6d2f0-401">**HearingImpaired**</span></span><br /><br /> <span data-ttu-id="6d2f0-402">必要</span><span class="sxs-lookup"><span data-stu-id="6d2f0-402">Required</span></span> |<span data-ttu-id="6d2f0-403">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="6d2f0-403">**xs:int**</span></span> |<span data-ttu-id="6d2f0-404">設定此屬性 too1 tooindicate 此音軌適用於 hello 聽覺障礙者。</span><span class="sxs-lookup"><span data-stu-id="6d2f0-404">Set this attribute too1 tooindicate this track is for hello hearing impaired.</span></span> |
| <span data-ttu-id="6d2f0-405">**VisualImpaired**</span><span class="sxs-lookup"><span data-stu-id="6d2f0-405">**VisualImpaired**</span></span><br /><br /> <span data-ttu-id="6d2f0-406">必要</span><span class="sxs-lookup"><span data-stu-id="6d2f0-406">Required</span></span> |<span data-ttu-id="6d2f0-407">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="6d2f0-407">**xs:int**</span></span> |<span data-ttu-id="6d2f0-408">設定此屬性 too1 tooindicate 此音軌適用於視覺障礙者 hello。</span><span class="sxs-lookup"><span data-stu-id="6d2f0-408">Set this attribute too1 tooindicate this track is for hello visually impaired.</span></span> |
| <span data-ttu-id="6d2f0-409">**CleanEffects**</span><span class="sxs-lookup"><span data-stu-id="6d2f0-409">**CleanEffects**</span></span><br /><br /> <span data-ttu-id="6d2f0-410">必要</span><span class="sxs-lookup"><span data-stu-id="6d2f0-410">Required</span></span> |<span data-ttu-id="6d2f0-411">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="6d2f0-411">**xs:int**</span></span> |<span data-ttu-id="6d2f0-412">設定此屬性 too1 tooindicate 此音軌有全新效果。</span><span class="sxs-lookup"><span data-stu-id="6d2f0-412">Set this attribute too1 tooindicate this track has clean effects.</span></span> |
| <span data-ttu-id="6d2f0-413">**AttachedPic**</span><span class="sxs-lookup"><span data-stu-id="6d2f0-413">**AttachedPic**</span></span><br /><br /> <span data-ttu-id="6d2f0-414">必要</span><span class="sxs-lookup"><span data-stu-id="6d2f0-414">Required</span></span> |<span data-ttu-id="6d2f0-415">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="6d2f0-415">**xs:int**</span></span> |<span data-ttu-id="6d2f0-416">設定此屬性 too1 tooindicate 此音軌有圖片。</span><span class="sxs-lookup"><span data-stu-id="6d2f0-416">Set this attribute too1 tooindicate this track has pictures.</span></span> |

## <span data-ttu-id="6d2f0-417"><a name="Programs"></a> Programs 元素</span><span class="sxs-lookup"><span data-stu-id="6d2f0-417"><a name="Programs"></a> Programs element</span></span>
<span data-ttu-id="6d2f0-418">保有多個 **Program** 元素的包裝函式元素。</span><span class="sxs-lookup"><span data-stu-id="6d2f0-418">Wrapper element holding multiple **Program** elements.</span></span>  

### <a name="child-elements"></a><span data-ttu-id="6d2f0-419">子元素</span><span class="sxs-lookup"><span data-stu-id="6d2f0-419">Child elements</span></span>
| <span data-ttu-id="6d2f0-420">名稱</span><span class="sxs-lookup"><span data-stu-id="6d2f0-420">Name</span></span> | <span data-ttu-id="6d2f0-421">類型</span><span class="sxs-lookup"><span data-stu-id="6d2f0-421">Type</span></span> | <span data-ttu-id="6d2f0-422">說明</span><span class="sxs-lookup"><span data-stu-id="6d2f0-422">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6d2f0-423">**Program**</span><span class="sxs-lookup"><span data-stu-id="6d2f0-423">**Program**</span></span><br /><br /> <span data-ttu-id="6d2f0-424">minOccurs="0" maxOccurs="unbounded"</span><span class="sxs-lookup"><span data-stu-id="6d2f0-424">minOccurs="0" maxOccurs="unbounded"</span></span> |[<span data-ttu-id="6d2f0-425">ProgramType</span><span class="sxs-lookup"><span data-stu-id="6d2f0-425">ProgramType</span></span>](media-services-input-metadata-schema.md#ProgramType) |<span data-ttu-id="6d2f0-426">為 MPEG-TS 格式的資產檔案，包含 hello 資產檔案中程式的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="6d2f0-426">For asset files that are in MPEG-TS format, contains information about programs in hello asset file.</span></span> |

## <span data-ttu-id="6d2f0-427"><a name="VideoTracks"></a> VideoTracks 元素</span><span class="sxs-lookup"><span data-stu-id="6d2f0-427"><a name="VideoTracks"></a> VideoTracks element</span></span>
 <span data-ttu-id="6d2f0-428">保有多個 **VideoTrack** 元素的包裝函式元素。</span><span class="sxs-lookup"><span data-stu-id="6d2f0-428">Wrapper element holding multiple **VideoTrack** elements.</span></span>  

 <span data-ttu-id="6d2f0-429">請參閱本主題的 hello 結尾 XML 範例： [XML 範例](media-services-input-metadata-schema.md#xml)。</span><span class="sxs-lookup"><span data-stu-id="6d2f0-429">See an XML example at hello end of this topic: [XML example](media-services-input-metadata-schema.md#xml).</span></span>  

### <a name="child-elements"></a><span data-ttu-id="6d2f0-430">子元素</span><span class="sxs-lookup"><span data-stu-id="6d2f0-430">Child elements</span></span>
| <span data-ttu-id="6d2f0-431">名稱</span><span class="sxs-lookup"><span data-stu-id="6d2f0-431">Name</span></span> | <span data-ttu-id="6d2f0-432">類型</span><span class="sxs-lookup"><span data-stu-id="6d2f0-432">Type</span></span> | <span data-ttu-id="6d2f0-433">說明</span><span class="sxs-lookup"><span data-stu-id="6d2f0-433">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6d2f0-434">**VideoTrack**</span><span class="sxs-lookup"><span data-stu-id="6d2f0-434">**VideoTrack**</span></span><br /><br /> <span data-ttu-id="6d2f0-435">minOccurs="0" maxOccurs="unbounded"</span><span class="sxs-lookup"><span data-stu-id="6d2f0-435">minOccurs="0" maxOccurs="unbounded"</span></span> |[<span data-ttu-id="6d2f0-436">VideoTrackType (繼承自 TrackType)</span><span class="sxs-lookup"><span data-stu-id="6d2f0-436">VideoTrackType (inherits from TrackType)</span></span>](media-services-input-metadata-schema.md#VideoTrackType) |<span data-ttu-id="6d2f0-437">包含 hello 資產檔案中的視訊音軌的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="6d2f0-437">Contains information about video tracks in hello asset file.</span></span> |

## <span data-ttu-id="6d2f0-438"><a name="AudioTracks"></a> AudioTracks 元素</span><span class="sxs-lookup"><span data-stu-id="6d2f0-438"><a name="AudioTracks"></a> AudioTracks element</span></span>
 <span data-ttu-id="6d2f0-439">保有多個 **AudioTrack** 元素的包裝函式元素。</span><span class="sxs-lookup"><span data-stu-id="6d2f0-439">Wrapper element holding multiple **AudioTrack** elements.</span></span>  

 <span data-ttu-id="6d2f0-440">請參閱本主題的 hello 結尾 XML 範例： [XML 範例](media-services-input-metadata-schema.md#xml)。</span><span class="sxs-lookup"><span data-stu-id="6d2f0-440">See an XML example at hello end of this topic: [XML example](media-services-input-metadata-schema.md#xml).</span></span>  

### <a name="elements"></a><span data-ttu-id="6d2f0-441">元素</span><span class="sxs-lookup"><span data-stu-id="6d2f0-441">elements</span></span>
| <span data-ttu-id="6d2f0-442">名稱</span><span class="sxs-lookup"><span data-stu-id="6d2f0-442">Name</span></span> | <span data-ttu-id="6d2f0-443">類型</span><span class="sxs-lookup"><span data-stu-id="6d2f0-443">Type</span></span> | <span data-ttu-id="6d2f0-444">說明</span><span class="sxs-lookup"><span data-stu-id="6d2f0-444">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6d2f0-445">**AudioTrack**</span><span class="sxs-lookup"><span data-stu-id="6d2f0-445">**AudioTrack**</span></span><br /><br /> <span data-ttu-id="6d2f0-446">minOccurs="0" maxOccurs="unbounded"</span><span class="sxs-lookup"><span data-stu-id="6d2f0-446">minOccurs="0" maxOccurs="unbounded"</span></span> |[<span data-ttu-id="6d2f0-447">AudioTrackType (繼承自 TrackType)</span><span class="sxs-lookup"><span data-stu-id="6d2f0-447">AudioTrackType (inherits from TrackType)</span></span>](media-services-input-metadata-schema.md#AudioTrackType) |<span data-ttu-id="6d2f0-448">包含 hello 資產檔案中的音訊音軌的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="6d2f0-448">Contains information about audio tracks in hello asset file.</span></span> |

## <span data-ttu-id="6d2f0-449"><a name="code"></a> 結構描述程式碼</span><span class="sxs-lookup"><span data-stu-id="6d2f0-449"><a name="code"></a> Schema Code</span></span>
    <?xml version="1.0" encoding="utf-8"?>  
    <xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:msdata="urn:schemas-microsoft-com:xml-msdata" version="1.0"  
               xmlns="http://schemas.microsoft.com/windowsazure/mediaservices/2014/07/mediaencoder/inputmetadata"  
               targetNamespace="http://schemas.microsoft.com/windowsazure/mediaservices/2014/07/mediaencoder/inputmetadata"  
               elementFormDefault="qualified">  

      <xs:complexType name="MetadataType">  
        <xs:attribute name="key"   type="xs:string" use="required"/>  
        <xs:attribute name="value" type="xs:string" use="required"/>  
      </xs:complexType>  

      <xs:complexType name="ProgramType">  
        <xs:attribute name="ProgramId" type="xs:int" use="required">  
          <xs:annotation>  
            <xs:documentation>Program Id</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="NumberOfPrograms" type="xs:int" use="required">  
          <xs:annotation>  
            <xs:documentation>Number of programs</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="PmtPid" type="xs:int" use="required">  
          <xs:annotation>  
            <xs:documentation>pmt pid</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="PcrPid" type="xs:int" use="required">  
          <xs:annotation>  
            <xs:documentation>pcr pid</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="StartPTS" type="xs:long">  
          <xs:annotation>  
            <xs:documentation>start pts</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="EndPTS" type="xs:long">  
          <xs:annotation>  
            <xs:documentation>end pts</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
      </xs:complexType>  

      <xs:complexType name="StreamDispositionType">  
        <xs:attribute name="Default"          type="xs:int" use="required" />  
        <xs:attribute name="Dub"              type="xs:int" use="required" />  
        <xs:attribute name="Original"         type="xs:int" use="required" />  
        <xs:attribute name="Comment"          type="xs:int" use="required" />  
        <xs:attribute name="Lyrics"           type="xs:int" use="required" />  
        <xs:attribute name="Karaoke"          type="xs:int" use="required" />  
        <xs:attribute name="Forced"           type="xs:int" use="required" />  
        <xs:attribute name="HearingImpaired"  type="xs:int" use="required" />  
        <xs:attribute name="VisualImpaired"   type="xs:int" use="required" />  
        <xs:attribute name="CleanEffects"     type="xs:int" use="required" />  
        <xs:attribute name="AttachedPic"      type="xs:int" use="required" />  
      </xs:complexType>  

      <xs:complexType name="TrackType" abstract="true">  
        <xs:sequence>  
          <xs:element name="Disposition" type="StreamDispositionType" minOccurs="0" maxOccurs="1"/>  
          <xs:element name="Metadata" type="MetadataType" minOccurs="0" maxOccurs="unbounded"/>  
        </xs:sequence>  
        <xs:attribute name="Id" use="required">  
          <xs:annotation>  
            <xs:documentation>zero-based index of this video track. Note: this is not necessarily hello TrackID as used in an MP4 file</xs:documentation>  
          </xs:annotation>  
          <xs:simpleType>  
            <xs:restriction base="xs:int">  
              <xs:minInclusive value="0"/>  
            </xs:restriction>  
          </xs:simpleType>  
        </xs:attribute>  
        <xs:attribute name="Codec" type="xs:string">  
          <xs:annotation>  
            <xs:documentation>video track codec string</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="CodecLongName" type="xs:string">  
          <xs:annotation>  
            <xs:documentation>video track codec long name</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="TimeBase"  type="xs:string" use="required">  
          <xs:annotation>  
            <xs:documentation>Time base. Example: TimeBase="1/48000"</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="NumberOfFrames">  
          <xs:annotation>  
            <xs:documentation>number of frames</xs:documentation>  
          </xs:annotation>  
          <xs:simpleType>  
            <xs:restriction base="xs:int">  
              <xs:minInclusive value="0"/>  
            </xs:restriction>  
          </xs:simpleType>  
        </xs:attribute>  
        <xs:attribute name="StartTime" type="xs:duration">  
          <xs:annotation>  
            <xs:documentation>Track start time. Example: StartTime="PT2.669S"</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="Duration" type="xs:duration">  
          <xs:annotation>  
            <xs:documentation>Track duration. Example: Duration="PT25M37.757S"</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
      </xs:complexType>  

      <xs:complexType name="VideoTrackType">  
        <xs:annotation>  
          <xs:documentation>A specific video track in hello parent AssetFile</xs:documentation>  
        </xs:annotation>  
        <xs:complexContent>  
          <xs:extension base="TrackType">  
            <xs:attribute name="FourCC" type="xs:string" use="required">  
              <xs:annotation>  
                <xs:documentation>video codec FourCC code</xs:documentation>  
              </xs:annotation>  
            </xs:attribute>  
            <xs:attribute name="Profile" type="xs:string">  
              <xs:annotation>  
                <xs:documentation>profile</xs:documentation>  
              </xs:annotation>  
            </xs:attribute>  
            <xs:attribute name="Level" type="xs:string">  
              <xs:annotation>  
                <xs:documentation>level</xs:documentation>  
              </xs:annotation>  
            </xs:attribute>  
            <xs:attribute name="PixelFormat" type="xs:string">  
              <xs:annotation>  
                <xs:documentation>Video track's pixel format</xs:documentation>  
              </xs:annotation>  
            </xs:attribute>  
            <xs:attribute name="Width" use="required">  
              <xs:annotation>  
                <xs:documentation>encoded video width in pixels</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:int">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="Height" use="required">  
              <xs:annotation>  
                <xs:documentation>encoded video height in pixels</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:int">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="DisplayAspectRatioNumerator" use="required">  
              <xs:annotation>  
                <xs:documentation>video display aspect ratio numerator</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:double">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="DisplayAspectRatioDenominator" use="required">  
              <xs:annotation>  
                <xs:documentation>video display aspect ratio denominator</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:double">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="SampleAspectRatioNumerator">  
              <xs:annotation>  
                <xs:documentation>video sample aspect ratio numerator</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:double">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="SampleAspectRatioDenominator">  
              <xs:annotation>  
                <xs:documentation>video sample aspect ratio denominator</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:double">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="FrameRate" use="required">  
              <xs:annotation>  
                <xs:documentation>measured video frame rate in .3f format</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:decimal">  
                  <xs:minInclusive value="0"/>  
                  <xs:fractionDigits value="3"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="Bitrate">  
              <xs:annotation>  
                <xs:documentation>average video bit rate in kilobits per second, as calculated from hello AssetFile. Counts only hello elementary stream payload, and does not include hello packaging overhead</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:int">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="MaxGOPBitrate">  
              <xs:annotation>  
                <xs:documentation>Max GOP average bitrate for this video track, in kilobits per second</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:int">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="HasBFrames" type="xs:int">  
              <xs:annotation>  
                <xs:documentation>video track number of B frames</xs:documentation>  
              </xs:annotation>  
            </xs:attribute>  
          </xs:extension>  
        </xs:complexContent>  
      </xs:complexType>  

      <xs:complexType name="AudioTrackType">  
        <xs:annotation>  
          <xs:documentation>a specific audio track in hello parent AssetFile</xs:documentation>  
        </xs:annotation>  
        <xs:complexContent>  
          <xs:extension base="TrackType">  
            <xs:attribute name="SampleFormat"  type="xs:string">  
              <xs:annotation>  
                <xs:documentation>sample format</xs:documentation>  
              </xs:annotation>  
            </xs:attribute>  
            <xs:attribute name="ChannelLayout"  type="xs:string">  
              <xs:annotation>  
                <xs:documentation>channel layout</xs:documentation>  
              </xs:annotation>  
            </xs:attribute>  
            <xs:attribute name="Channels" use="required">  
              <xs:annotation>  
                <xs:documentation>number of audio channels</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:int">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="SamplingRate" use="required">  
              <xs:annotation>  
                <xs:documentation>audio sampling rate in samples/sec or Hz</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:int">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="Bitrate">  
              <xs:annotation>  
                <xs:documentation>average audio bit rate in bits per second, as calculated from hello AssetFile. Counts only hello elementary stream payload, and does not include hello packaging overhead</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:int">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="BitsPerSample">  
              <xs:annotation>  
                <xs:documentation>Bits per sample for hello wFormatTag format type</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:int">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
          </xs:extension>  
        </xs:complexContent>  
      </xs:complexType>  

      <xs:element name="AssetFiles">  
        <xs:annotation>  
          <xs:documentation>Collection of AssetFile entries for hello encoding job</xs:documentation>  
        </xs:annotation>  
        <xs:complexType>  
          <xs:sequence>  
            <xs:element name="AssetFile" minOccurs="1" maxOccurs="unbounded">  
              <xs:annotation>  
                <xs:documentation>asset file</xs:documentation>  
              </xs:annotation>  
              <xs:complexType>  
                <xs:sequence>  
                  <xs:element name="Programs" minOccurs="0">  
                    <xs:annotation>  
                      <xs:documentation>This is hello collection of all programs when file is MPEG-TS</xs:documentation>  
                    </xs:annotation>  
                    <xs:complexType>  
                      <xs:sequence>  
                        <xs:element name="Program" type="ProgramType" minOccurs="0" maxOccurs="unbounded" />  
                      </xs:sequence>  
                    </xs:complexType>  
                  </xs:element>  
                  <xs:element name="VideoTracks" minOccurs="0">  
                    <xs:annotation>  
                      <xs:documentation>Each physical AssetFile can contain in it zero or more video tracks interleaved into an appropriate container format. This is hello collection of all those video tracks</xs:documentation>  
                    </xs:annotation>  
                    <xs:complexType>  
                      <xs:sequence>  
                        <xs:element name="VideoTrack" type="VideoTrackType" minOccurs="0" maxOccurs="unbounded" />  
                      </xs:sequence>  
                    </xs:complexType>  
                  </xs:element>  
                  <xs:element name="AudioTracks" minOccurs="0">  
                    <xs:annotation>  
                      <xs:documentation>each physical AssetFile can contain in it zero or more audio tracks interleaved into an appropriate container format. This is hello collection of all those audio tracks</xs:documentation>  
                    </xs:annotation>  
                    <xs:complexType>  
                      <xs:sequence>  
                        <xs:element name="AudioTrack" type="AudioTrackType" minOccurs="0" maxOccurs="unbounded" />  
                      </xs:sequence>  
                    </xs:complexType>  
                  </xs:element>  
                  <xs:element name="Metadata" type="MetadataType" minOccurs="0" maxOccurs="unbounded" />  
                </xs:sequence>  
                <xs:attribute name="Name" type="xs:string" use="required">  
                  <xs:annotation>  
                    <xs:documentation>hello media asset file name</xs:documentation>  
                  </xs:annotation>  
                </xs:attribute>  
                <xs:attribute name="Size" use="required">  
                  <xs:annotation>  
                    <xs:documentation>size of file in bytes</xs:documentation>  
                  </xs:annotation>  
                  <xs:simpleType>  
                    <xs:restriction base="xs:long">  
                      <xs:minInclusive value="0"/>  
                    </xs:restriction>  
                  </xs:simpleType>  
                </xs:attribute>  
                <xs:attribute name="Duration" type="xs:duration" use="required">  
                  <xs:annotation>  
                    <xs:documentation>content play back duration. Example: Duration="PT25M37.757S"</xs:documentation>  
                  </xs:annotation>  
                </xs:attribute>  
                <xs:attribute name="NumberOfStreams" type="xs:int" use="required">  
                  <xs:annotation>  
                    <xs:documentation>number of streams in asset file</xs:documentation>  
                  </xs:annotation>  
                </xs:attribute>  
                <xs:attribute name="FormatNames" type="xs:string" use="required">  
                  <xs:annotation>  
                    <xs:documentation>format names</xs:documentation>  
                  </xs:annotation>  
                </xs:attribute>  
                <xs:attribute name="FormatVerboseName" type="xs:string" use="required">  
                  <xs:annotation>  
                    <xs:documentation>format verbose names</xs:documentation>  
                  </xs:annotation>  
                </xs:attribute>  
                <xs:attribute name="StartTime" type="xs:duration">  
                  <xs:annotation>  
                    <xs:documentation>content start time. Example: StartTime="PT2.669S"</xs:documentation>  
                  </xs:annotation>  
                </xs:attribute>  
                <xs:attribute name="OverallBitRate">  
                  <xs:annotation>  
                    <xs:documentation>average bitrate of hello asset file in kbps</xs:documentation>  
                  </xs:annotation>  
                  <xs:simpleType>  
                    <xs:restriction base="xs:int">  
                      <xs:minInclusive value="0"/>  
                    </xs:restriction>  
                  </xs:simpleType>  
                </xs:attribute>  
              </xs:complexType>  
            </xs:element>  
          </xs:sequence>  
        </xs:complexType>  
      </xs:element>  
    </xs:schema>  


## <span data-ttu-id="6d2f0-450"><a name="xml"></a> XML 範例</span><span class="sxs-lookup"><span data-stu-id="6d2f0-450"><a name="xml"></a> XML example</span></span>
<span data-ttu-id="6d2f0-451">hello 以下是 hello 輸入中繼資料檔案的範例。</span><span class="sxs-lookup"><span data-stu-id="6d2f0-451">hello following is an example of hello Input metadata file.</span></span>  

    <?xml version="1.0" encoding="utf-8"?>  
    <AssetFiles xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns="http://schemas.microsoft.com/windowsazure/mediaservices/2014/07/mediaencoder/inputmetadata">  
      <AssetFile Name="bear.mp4" Size="1973733" Duration="PT12.678S" NumberOfStreams="2" FormatNames="mov,mp4,m4a,3gp,3g2,mj2" FormatVerboseName="QuickTime / MOV" StartTime="PT0S" OverallBitRate="1245">  
        <VideoTracks>  
          <VideoTrack Id="1" Codec="h264" CodecLongName="H.264 / AVC / MPEG-4 AVC / MPEG-4 part 10" TimeBase="1/29970" NumberOfFrames="375" StartTime="PT0.034S" Duration="PT12.645S" FourCC="avc1" Profile="High" Level="4.1" PixelFormat="yuv420p" Width="512" Height="384" DisplayAspectRatioNumerator="4" DisplayAspectRatioDenominator="3" SampleAspectRatioNumerator="1" SampleAspectRatioDenominator="1" FrameRate="29.656" Bitrate="1043" HasBFrames="1">  
            <Disposition Default="1" Dub="0" Original="0" Comment="0" Lyrics="0" Karaoke="0" Forced="0" HearingImpaired="0" VisualImpaired="0" CleanEffects="0" AttachedPic="0" />  
            <Metadata key="creation_time" value="2010-03-10 16:11:56" />  
            <Metadata key="language" value="eng" />  
            <Metadata key="handler_name" value="Mainconcept MP4 Video Media Handler" />  
          </VideoTrack>  
        </VideoTracks>  
        <AudioTracks>  
          <AudioTrack Id="0" Codec="aac" CodecLongName="AAC (Advanced Audio Coding)" TimeBase="1/44100" NumberOfFrames="546" StartTime="PT0S" Duration="PT12.678S" SampleFormat="fltp" ChannelLayout="stereo" Channels="2" SamplingRate="44100" Bitrate="156" BitsPerSample="0">  
            <Disposition Default="1" Dub="0" Original="0" Comment="0" Lyrics="0" Karaoke="0" Forced="0" HearingImpaired="0" VisualImpaired="0" CleanEffects="0" AttachedPic="0" />  
            <Metadata key="creation_time" value="2010-03-10 16:11:56" />  
            <Metadata key="language" value="eng" />  
            <Metadata key="handler_name" value="Mainconcept MP4 Sound Media Handler" />  
          </AudioTrack>  
        </AudioTracks>  
        <Metadata key="major_brand" value="mp42" />  
        <Metadata key="minor_version" value="0" />  
        <Metadata key="compatible_brands" value="mp42mp41" />  
        <Metadata key="creation_time" value="2010-03-10 16:11:53" />  
        <Metadata key="comment" value="Courtesy of National Geographic.  Used by Permission." />  
      </AssetFile>  
    </AssetFiles>  

## <a name="next-steps"></a><span data-ttu-id="6d2f0-452">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6d2f0-452">Next steps</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="6d2f0-453">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="6d2f0-453">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

