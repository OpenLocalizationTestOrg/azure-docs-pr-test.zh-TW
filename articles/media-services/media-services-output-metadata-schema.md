---
title: "aaaAzure Media Services 輸出中繼資料結構描述 |Microsoft 文件"
description: "hello 主題提供 Azure Media Services 輸出中繼資料架構的概觀。"
author: Juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: 1ed84c88-eea5-4a24-9c4f-f2428157d08a
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: juliako
ms.openlocfilehash: 7f07d6accbe0b171d0408b15d5e1e6b5afd6c367
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="output-metadata"></a><span data-ttu-id="d5cbb-103">輸出中繼資料</span><span class="sxs-lookup"><span data-stu-id="d5cbb-103">Output Metadata</span></span>
## <a name="overview"></a><span data-ttu-id="d5cbb-104">概觀</span><span class="sxs-lookup"><span data-stu-id="d5cbb-104">Overview</span></span>
<span data-ttu-id="d5cbb-105">輸入的資產或多個相關聯的編碼工作，是您想 tooperform 部分編碼工作。</span><span class="sxs-lookup"><span data-stu-id="d5cbb-105">An encoding job is associated with an input asset (or assets) on which you want tooperform some encoding tasks.</span></span> <span data-ttu-id="d5cbb-106">例如，將 MP4 檔案 tooH.264 MP4 彈性位元速率編碼設定。建立縮圖。建立覆疊。</span><span class="sxs-lookup"><span data-stu-id="d5cbb-106">For example, encode an MP4 file tooH.264 MP4 adaptive bitrate sets; create a thumbnail; create overlays.</span></span> <span data-ttu-id="d5cbb-107">完成工作時，就會產生輸出資產。</span><span class="sxs-lookup"><span data-stu-id="d5cbb-107">Upon completion of a task, an output asset is produced.</span></span>  <span data-ttu-id="d5cbb-108">hello 輸出資產包含視訊、 音訊、 縮圖，等 hello 輸出資產也包含 hello 輸出資產的相關中繼資料檔案。</span><span class="sxs-lookup"><span data-stu-id="d5cbb-108">hello output asset contains video, audio, thumbnails, etc. hello output asset also contains a file with metadata about hello output asset.</span></span> <span data-ttu-id="d5cbb-109">hello hello 中繼資料 XML 檔案名稱具有下列格式的 hello: &lt;s&gt;l (例如，BigBuckBunny_manifest.xml)。</span><span class="sxs-lookup"><span data-stu-id="d5cbb-109">hello name of hello metadata XML file has hello following format: &lt;source_file_name&gt;_manifest.xml (for example, BigBuckBunny_manifest.xml).</span></span>  

<span data-ttu-id="d5cbb-110">如果您想 tooexamine hello 中繼資料檔案時，您可以建立**SAS**定位器和下載 hello 檔案 tooyour 本機電腦。</span><span class="sxs-lookup"><span data-stu-id="d5cbb-110">If you want tooexamine hello metadata file, you can create a **SAS** locator and download hello file tooyour local computer.</span></span>  

<span data-ttu-id="d5cbb-111">本主題討論 hello 項目和 hello XML 結構描述的類型上的 hello 輸出中繼資料 (&lt;s&gt;l) 為基礎。</span><span class="sxs-lookup"><span data-stu-id="d5cbb-111">This topic discusses hello elements and types of hello XML schema on which hello output metada (&lt;source_file_name&gt;_manifest.xml) is based.</span></span> <span data-ttu-id="d5cbb-112">如需 hello 檔案，其中包含有關 hello 輸入資產的中繼資料資訊，請參閱[輸入中繼資料](media-services-input-metadata-schema.md)。</span><span class="sxs-lookup"><span data-stu-id="d5cbb-112">For information about hello file that contains metadata about hello input asset, see [Input Metadata](media-services-input-metadata-schema.md).</span></span>  

> [!NOTE]
> <span data-ttu-id="d5cbb-113">您可以尋找 hello 完整的結構描述程式碼以及在 hello 本主題結尾的 XML 範例。</span><span class="sxs-lookup"><span data-stu-id="d5cbb-113">You can find hello complete schema code and XML example at hello end of this topic.</span></span>  
>
>

## <span data-ttu-id="d5cbb-114"><a name="AssetFiles "></a> AssetFiles 根元素</span><span class="sxs-lookup"><span data-stu-id="d5cbb-114"><a name="AssetFiles "></a> AssetFiles root element</span></span>
<span data-ttu-id="d5cbb-115">Hello 編碼工作的 AssetFile 項目的集合。</span><span class="sxs-lookup"><span data-stu-id="d5cbb-115">Collection of AssetFile entries for hello encoding job.</span></span>  

### <a name="child-elements"></a><span data-ttu-id="d5cbb-116">子元素</span><span class="sxs-lookup"><span data-stu-id="d5cbb-116">Child elements</span></span>
| <span data-ttu-id="d5cbb-117">名稱</span><span class="sxs-lookup"><span data-stu-id="d5cbb-117">Name</span></span> | <span data-ttu-id="d5cbb-118">說明</span><span class="sxs-lookup"><span data-stu-id="d5cbb-118">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d5cbb-119">**AssetFile**</span><span class="sxs-lookup"><span data-stu-id="d5cbb-119">**AssetFile**</span></span><br/><br/> <span data-ttu-id="d5cbb-120">minOccurs="0" maxOccurs="1"</span><span class="sxs-lookup"><span data-stu-id="d5cbb-120">minOccurs="0" maxOccurs="1"</span></span> |<span data-ttu-id="d5cbb-121">[AssetFile 元素](media-services-output-metadata-schema.md)一部分 hello AssetFiles 集合。</span><span class="sxs-lookup"><span data-stu-id="d5cbb-121">An [AssetFile element](media-services-output-metadata-schema.md) that is part of hello AssetFiles collection.</span></span> |

## <span data-ttu-id="d5cbb-122"><a name="AssetFile "></a> AssetFile 元素</span><span class="sxs-lookup"><span data-stu-id="d5cbb-122"><a name="AssetFile "></a> AssetFile element</span></span>
<span data-ttu-id="d5cbb-123">您可以找到 XML 範例 [XML 範例](media-services-output-metadata-schema.md#xml)。</span><span class="sxs-lookup"><span data-stu-id="d5cbb-123">You can find an XML example [XML example](media-services-output-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="d5cbb-124">屬性</span><span class="sxs-lookup"><span data-stu-id="d5cbb-124">Attributes</span></span>
| <span data-ttu-id="d5cbb-125">名稱</span><span class="sxs-lookup"><span data-stu-id="d5cbb-125">Name</span></span> | <span data-ttu-id="d5cbb-126">類型</span><span class="sxs-lookup"><span data-stu-id="d5cbb-126">Type</span></span> | <span data-ttu-id="d5cbb-127">說明</span><span class="sxs-lookup"><span data-stu-id="d5cbb-127">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d5cbb-128">**名稱**</span><span class="sxs-lookup"><span data-stu-id="d5cbb-128">**Name**</span></span><br/><br/> <span data-ttu-id="d5cbb-129">必要</span><span class="sxs-lookup"><span data-stu-id="d5cbb-129">Required</span></span> |<span data-ttu-id="d5cbb-130">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="d5cbb-130">**xs:string**</span></span> |<span data-ttu-id="d5cbb-131">hello 媒體資產檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="d5cbb-131">hello media asset file name.</span></span> |
| <span data-ttu-id="d5cbb-132">**大小**</span><span class="sxs-lookup"><span data-stu-id="d5cbb-132">**Size**</span></span><br/><br/> <span data-ttu-id="d5cbb-133">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="d5cbb-133">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="d5cbb-134">必要</span><span class="sxs-lookup"><span data-stu-id="d5cbb-134">Required</span></span> |<span data-ttu-id="d5cbb-135">**xs:long**</span><span class="sxs-lookup"><span data-stu-id="d5cbb-135">**xs:long**</span></span> |<span data-ttu-id="d5cbb-136">Hello 資產檔案，以位元組為單位的大小。</span><span class="sxs-lookup"><span data-stu-id="d5cbb-136">Size of hello asset file in bytes.</span></span> |
| <span data-ttu-id="d5cbb-137">**Duration**</span><span class="sxs-lookup"><span data-stu-id="d5cbb-137">**Duration**</span></span><br/><br/> <span data-ttu-id="d5cbb-138">必要</span><span class="sxs-lookup"><span data-stu-id="d5cbb-138">Required</span></span> |<span data-ttu-id="d5cbb-139">**xs:duration**</span><span class="sxs-lookup"><span data-stu-id="d5cbb-139">**xs:duration**</span></span> |<span data-ttu-id="d5cbb-140">內容播放持續時間。</span><span class="sxs-lookup"><span data-stu-id="d5cbb-140">Content play back duration.</span></span> |

### <a name="child-elements"></a><span data-ttu-id="d5cbb-141">子元素</span><span class="sxs-lookup"><span data-stu-id="d5cbb-141">Child elements</span></span>
| <span data-ttu-id="d5cbb-142">名稱</span><span class="sxs-lookup"><span data-stu-id="d5cbb-142">Name</span></span> | <span data-ttu-id="d5cbb-143">說明</span><span class="sxs-lookup"><span data-stu-id="d5cbb-143">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d5cbb-144">**來源**</span><span class="sxs-lookup"><span data-stu-id="d5cbb-144">**Sources**</span></span> |<span data-ttu-id="d5cbb-145">處理輸入/來源媒體檔案，集合中排序 tooproduce 此 AssetFile。</span><span class="sxs-lookup"><span data-stu-id="d5cbb-145">Collection of input/source media files, that was processed in order tooproduce this AssetFile.</span></span> <span data-ttu-id="d5cbb-146">如需詳細資訊，請參閱[來源元素](media-services-output-metadata-schema.md)。</span><span class="sxs-lookup"><span data-stu-id="d5cbb-146">For more information, see [Source element](media-services-output-metadata-schema.md).</span></span> |
| <span data-ttu-id="d5cbb-147">**VideoTracks**</span><span class="sxs-lookup"><span data-stu-id="d5cbb-147">**VideoTracks**</span></span><br/><br/> <span data-ttu-id="d5cbb-148">minOccurs="0" maxOccurs="1"</span><span class="sxs-lookup"><span data-stu-id="d5cbb-148">minOccurs="0" maxOccurs="1"</span></span> |<span data-ttu-id="d5cbb-149">每個實體資產檔案可以內含零個或多個交錯形成適當容器格式的視訊播放軌。</span><span class="sxs-lookup"><span data-stu-id="d5cbb-149">Each physical AssetFile can contain in it zero or more video tracks interleaved into an appropriate container format.</span></span> <span data-ttu-id="d5cbb-150">這是所有這些視訊播放軌的 hello 集合。</span><span class="sxs-lookup"><span data-stu-id="d5cbb-150">This is hello collection of all those video tracks.</span></span> <span data-ttu-id="d5cbb-151">如需詳細資訊，請參閱 [VideoTracks 元素](media-services-output-metadata-schema.md)。</span><span class="sxs-lookup"><span data-stu-id="d5cbb-151">For more information, see [VideoTracks element](media-services-output-metadata-schema.md).</span></span> |
| <span data-ttu-id="d5cbb-152">**AudioTracks**</span><span class="sxs-lookup"><span data-stu-id="d5cbb-152">**AudioTracks**</span></span><br/><br/> <span data-ttu-id="d5cbb-153">minOccurs="0" maxOccurs="1"</span><span class="sxs-lookup"><span data-stu-id="d5cbb-153">minOccurs="0" maxOccurs="1"</span></span> |<span data-ttu-id="d5cbb-154">每個實體資產檔案可以內含零個或多個交錯形成適當容器格式的音訊播放軌。</span><span class="sxs-lookup"><span data-stu-id="d5cbb-154">Each physical AssetFile can contain in it zero or more audio tracks interleaved into an appropriate container format.</span></span> <span data-ttu-id="d5cbb-155">這是所有這些音軌 hello 集合。</span><span class="sxs-lookup"><span data-stu-id="d5cbb-155">This is hello collection of all those audio tracks.</span></span> <span data-ttu-id="d5cbb-156">如需詳細資訊，請參閱 [AudioTracks 元素](media-services-output-metadata-schema.md)。</span><span class="sxs-lookup"><span data-stu-id="d5cbb-156">For more information, see [AudioTracks element](media-services-output-metadata-schema.md).</span></span> |

## <span data-ttu-id="d5cbb-157"><a name="Sources "></a> 來源元素</span><span class="sxs-lookup"><span data-stu-id="d5cbb-157"><a name="Sources "></a> Sources element</span></span>
<span data-ttu-id="d5cbb-158">處理輸入/來源媒體檔案，集合中排序 tooproduce 此 AssetFile。</span><span class="sxs-lookup"><span data-stu-id="d5cbb-158">Collection of input/source media files, that was processed in order tooproduce this AssetFile.</span></span>  

<span data-ttu-id="d5cbb-159">您可以找到 XML 範例 [XML 範例](media-services-output-metadata-schema.md#xml)。</span><span class="sxs-lookup"><span data-stu-id="d5cbb-159">You can find an XML example [XML example](media-services-output-metadata-schema.md#xml).</span></span>  

### <a name="child-elements"></a><span data-ttu-id="d5cbb-160">子元素</span><span class="sxs-lookup"><span data-stu-id="d5cbb-160">Child elements</span></span>
| <span data-ttu-id="d5cbb-161">名稱</span><span class="sxs-lookup"><span data-stu-id="d5cbb-161">Name</span></span> | <span data-ttu-id="d5cbb-162">說明</span><span class="sxs-lookup"><span data-stu-id="d5cbb-162">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d5cbb-163">**來源**</span><span class="sxs-lookup"><span data-stu-id="d5cbb-163">**Source**</span></span><br/><br/> <span data-ttu-id="d5cbb-164">minOccurs="1" maxOccurs="unbounded"</span><span class="sxs-lookup"><span data-stu-id="d5cbb-164">minOccurs="1" maxOccurs="unbounded"</span></span> |<span data-ttu-id="d5cbb-165">產生此資產時所使用的輸入/來源檔案。</span><span class="sxs-lookup"><span data-stu-id="d5cbb-165">An input/source file used when generating this asset.</span></span> <span data-ttu-id="d5cbb-166">如需詳細資訊，請參閱[來源元素](media-services-output-metadata-schema.md)。</span><span class="sxs-lookup"><span data-stu-id="d5cbb-166">For more information see [Source element](media-services-output-metadata-schema.md).</span></span> |

## <span data-ttu-id="d5cbb-167"><a name="Source "></a> 來源元素</span><span class="sxs-lookup"><span data-stu-id="d5cbb-167"><a name="Source "></a> Source element</span></span>
<span data-ttu-id="d5cbb-168">產生此資產時所使用的輸入/來源檔案。</span><span class="sxs-lookup"><span data-stu-id="d5cbb-168">An input/source file used when generating this asset.</span></span>  

<span data-ttu-id="d5cbb-169">您可以找到 XML 範例 [XML 範例](media-services-output-metadata-schema.md#xml)。</span><span class="sxs-lookup"><span data-stu-id="d5cbb-169">You can find an XML example [XML example](media-services-output-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="d5cbb-170">屬性</span><span class="sxs-lookup"><span data-stu-id="d5cbb-170">Attributes</span></span>
| <span data-ttu-id="d5cbb-171">名稱</span><span class="sxs-lookup"><span data-stu-id="d5cbb-171">Name</span></span> | <span data-ttu-id="d5cbb-172">類型</span><span class="sxs-lookup"><span data-stu-id="d5cbb-172">Type</span></span> | <span data-ttu-id="d5cbb-173">說明</span><span class="sxs-lookup"><span data-stu-id="d5cbb-173">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d5cbb-174">**名稱**</span><span class="sxs-lookup"><span data-stu-id="d5cbb-174">**Name**</span></span><br/><br/> <span data-ttu-id="d5cbb-175">必要</span><span class="sxs-lookup"><span data-stu-id="d5cbb-175">Required</span></span> |<span data-ttu-id="d5cbb-176">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="d5cbb-176">**xs:string**</span></span> |<span data-ttu-id="d5cbb-177">輸入的來源檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="d5cbb-177">Input source file name.</span></span> |

## <span data-ttu-id="d5cbb-178"><a name="VideoTracks "></a> VideoTracks 元素</span><span class="sxs-lookup"><span data-stu-id="d5cbb-178"><a name="VideoTracks "></a> VideoTracks element</span></span>
<span data-ttu-id="d5cbb-179">每個實體資產檔案可以內含零個或多個交錯形成適當容器格式的視訊播放軌。</span><span class="sxs-lookup"><span data-stu-id="d5cbb-179">Each physical AssetFile can contain in it zero or more video tracks interleaved into an appropriate container format.</span></span> <span data-ttu-id="d5cbb-180">這是所有這些視訊播放軌的 hello 集合。</span><span class="sxs-lookup"><span data-stu-id="d5cbb-180">This is hello collection of all those video tracks.</span></span>  

<span data-ttu-id="d5cbb-181">您可以找到 XML 範例 [XML 範例](media-services-output-metadata-schema.md#xml)。</span><span class="sxs-lookup"><span data-stu-id="d5cbb-181">You can find an XML example [XML example](media-services-output-metadata-schema.md#xml).</span></span>  

### <a name="child-elements"></a><span data-ttu-id="d5cbb-182">子元素</span><span class="sxs-lookup"><span data-stu-id="d5cbb-182">Child elements</span></span>
| <span data-ttu-id="d5cbb-183">名稱</span><span class="sxs-lookup"><span data-stu-id="d5cbb-183">Name</span></span> | <span data-ttu-id="d5cbb-184">說明</span><span class="sxs-lookup"><span data-stu-id="d5cbb-184">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d5cbb-185">**VideoTrack**</span><span class="sxs-lookup"><span data-stu-id="d5cbb-185">**VideoTrack**</span></span><br/><br/> <span data-ttu-id="d5cbb-186">minOccurs="1" maxOccurs="unbounded"</span><span class="sxs-lookup"><span data-stu-id="d5cbb-186">minOccurs="1" maxOccurs="unbounded"</span></span> |<span data-ttu-id="d5cbb-187">Hello 父系 AssetFile 中的特定視訊音軌。</span><span class="sxs-lookup"><span data-stu-id="d5cbb-187">A specific video track in hello parent AssetFile.</span></span> <span data-ttu-id="d5cbb-188">如需詳細資訊，請參閱 [VideoTrack 元素](media-services-output-metadata-schema.md#VideoTrack)。</span><span class="sxs-lookup"><span data-stu-id="d5cbb-188">For more information, see [VideoTrack element](media-services-output-metadata-schema.md#VideoTrack).</span></span> |

## <span data-ttu-id="d5cbb-189"><a name="VideoTrack"></a> VideoTrack 元素</span><span class="sxs-lookup"><span data-stu-id="d5cbb-189"><a name="VideoTrack"></a> VideoTrack element</span></span>
<span data-ttu-id="d5cbb-190">Hello 父系 AssetFile 中的特定視訊音軌。</span><span class="sxs-lookup"><span data-stu-id="d5cbb-190">A specific video track in hello parent AssetFile.</span></span>  

<span data-ttu-id="d5cbb-191">您可以找到 XML 範例 [XML 範例](media-services-output-metadata-schema.md#xml)。</span><span class="sxs-lookup"><span data-stu-id="d5cbb-191">You can find an XML example [XML example](media-services-output-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="d5cbb-192">屬性</span><span class="sxs-lookup"><span data-stu-id="d5cbb-192">Attributes</span></span>
| <span data-ttu-id="d5cbb-193">名稱</span><span class="sxs-lookup"><span data-stu-id="d5cbb-193">Name</span></span> | <span data-ttu-id="d5cbb-194">類型</span><span class="sxs-lookup"><span data-stu-id="d5cbb-194">Type</span></span> | <span data-ttu-id="d5cbb-195">說明</span><span class="sxs-lookup"><span data-stu-id="d5cbb-195">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d5cbb-196">**Id**</span><span class="sxs-lookup"><span data-stu-id="d5cbb-196">**Id**</span></span><br/><br/> <span data-ttu-id="d5cbb-197">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="d5cbb-197">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="d5cbb-198">必要</span><span class="sxs-lookup"><span data-stu-id="d5cbb-198">Required</span></span> |<span data-ttu-id="d5cbb-199">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="d5cbb-199">**xs:int**</span></span> |<span data-ttu-id="d5cbb-200">此視訊播放軌之以零為起始的索引。**注意：**不一定 hello TrackID MP4 檔案中使用。</span><span class="sxs-lookup"><span data-stu-id="d5cbb-200">Zero-based index of this video track. **Note:**  This is not necessarily hello TrackID as used in an MP4 file.</span></span> |
| <span data-ttu-id="d5cbb-201">**FourCC**</span><span class="sxs-lookup"><span data-stu-id="d5cbb-201">**FourCC**</span></span><br/><br/> <span data-ttu-id="d5cbb-202">必要</span><span class="sxs-lookup"><span data-stu-id="d5cbb-202">Required</span></span> |<span data-ttu-id="d5cbb-203">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="d5cbb-203">**xs:string**</span></span> |<span data-ttu-id="d5cbb-204">視訊轉碼器 FourCC 代碼。</span><span class="sxs-lookup"><span data-stu-id="d5cbb-204">Video codec FourCC code.</span></span> |
| <span data-ttu-id="d5cbb-205">**設定檔**</span><span class="sxs-lookup"><span data-stu-id="d5cbb-205">**Profile**</span></span> |<span data-ttu-id="d5cbb-206">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="d5cbb-206">**xs:string**</span></span> |<span data-ttu-id="d5cbb-207">H264 設定檔 （只適用 tooH264 轉碼器）。</span><span class="sxs-lookup"><span data-stu-id="d5cbb-207">H264 profile (only applicable tooH264 codec).</span></span> |
| <span data-ttu-id="d5cbb-208">**Level**</span><span class="sxs-lookup"><span data-stu-id="d5cbb-208">**Level**</span></span> |<span data-ttu-id="d5cbb-209">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="d5cbb-209">**xs:string**</span></span> |<span data-ttu-id="d5cbb-210">H264 層級 （僅適用 tooH264 轉碼器）。</span><span class="sxs-lookup"><span data-stu-id="d5cbb-210">H264 level (only applicable tooH264 codec).</span></span> |
| <span data-ttu-id="d5cbb-211">**Width**</span><span class="sxs-lookup"><span data-stu-id="d5cbb-211">**Width**</span></span><br/><br/> <span data-ttu-id="d5cbb-212">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="d5cbb-212">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="d5cbb-213">必要</span><span class="sxs-lookup"><span data-stu-id="d5cbb-213">Required</span></span> |<span data-ttu-id="d5cbb-214">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="d5cbb-214">**xs:int**</span></span> |<span data-ttu-id="d5cbb-215">編碼的視訊寬度 (以像素為單位)。</span><span class="sxs-lookup"><span data-stu-id="d5cbb-215">Encoded video width in pixels.</span></span> |
| <span data-ttu-id="d5cbb-216">**Height**</span><span class="sxs-lookup"><span data-stu-id="d5cbb-216">**Height**</span></span><br/><br/> <span data-ttu-id="d5cbb-217">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="d5cbb-217">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="d5cbb-218">必要</span><span class="sxs-lookup"><span data-stu-id="d5cbb-218">Required</span></span> |<span data-ttu-id="d5cbb-219">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="d5cbb-219">**xs:int**</span></span> |<span data-ttu-id="d5cbb-220">編碼的視訊高度 (以像素為單位)。</span><span class="sxs-lookup"><span data-stu-id="d5cbb-220">Encoded video height in pixels.</span></span> |
| <span data-ttu-id="d5cbb-221">**DisplayAspectRatioNumerator**</span><span class="sxs-lookup"><span data-stu-id="d5cbb-221">**DisplayAspectRatioNumerator**</span></span><br/><br/> <span data-ttu-id="d5cbb-222">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="d5cbb-222">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="d5cbb-223">必要</span><span class="sxs-lookup"><span data-stu-id="d5cbb-223">Required</span></span> |<span data-ttu-id="d5cbb-224">**xs:double**</span><span class="sxs-lookup"><span data-stu-id="d5cbb-224">**xs:double**</span></span> |<span data-ttu-id="d5cbb-225">視訊顯示長寬比的分子。</span><span class="sxs-lookup"><span data-stu-id="d5cbb-225">Video display aspect ratio numerator.</span></span> |
| <span data-ttu-id="d5cbb-226">**DisplayAspectRatioDenominator**</span><span class="sxs-lookup"><span data-stu-id="d5cbb-226">**DisplayAspectRatioDenominator**</span></span><br/><br/> <span data-ttu-id="d5cbb-227">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="d5cbb-227">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="d5cbb-228">必要</span><span class="sxs-lookup"><span data-stu-id="d5cbb-228">Required</span></span> |<span data-ttu-id="d5cbb-229">**xs:double**</span><span class="sxs-lookup"><span data-stu-id="d5cbb-229">**xs:double**</span></span> |<span data-ttu-id="d5cbb-230">視訊顯示長寬比的分母。</span><span class="sxs-lookup"><span data-stu-id="d5cbb-230">Video display aspect ratio denominator.</span></span> |
| <span data-ttu-id="d5cbb-231">**Framerate**</span><span class="sxs-lookup"><span data-stu-id="d5cbb-231">**Framerate**</span></span><br/><br/> <span data-ttu-id="d5cbb-232">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="d5cbb-232">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="d5cbb-233">必要</span><span class="sxs-lookup"><span data-stu-id="d5cbb-233">Required</span></span> |<span data-ttu-id="d5cbb-234">**xs:decimal**</span><span class="sxs-lookup"><span data-stu-id="d5cbb-234">**xs:decimal**</span></span> |<span data-ttu-id="d5cbb-235">測量的視訊畫面格速率 (採用 .3f 格式)。</span><span class="sxs-lookup"><span data-stu-id="d5cbb-235">Measured video frame rate in .3f format.</span></span> |
| <span data-ttu-id="d5cbb-236">**TargetFramerate**</span><span class="sxs-lookup"><span data-stu-id="d5cbb-236">**TargetFramerate**</span></span><br/><br/> <span data-ttu-id="d5cbb-237">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="d5cbb-237">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="d5cbb-238">必要</span><span class="sxs-lookup"><span data-stu-id="d5cbb-238">Required</span></span> |<span data-ttu-id="d5cbb-239">**xs:decimal**</span><span class="sxs-lookup"><span data-stu-id="d5cbb-239">**xs:decimal**</span></span> |<span data-ttu-id="d5cbb-240">預設的目標視訊畫面格速率 (採用 .3f 格式)。</span><span class="sxs-lookup"><span data-stu-id="d5cbb-240">Preset target video frame rate in .3f format.</span></span> |
| <span data-ttu-id="d5cbb-241">**Bitrate**</span><span class="sxs-lookup"><span data-stu-id="d5cbb-241">**Bitrate**</span></span><br/><br/> <span data-ttu-id="d5cbb-242">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="d5cbb-242">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="d5cbb-243">必要</span><span class="sxs-lookup"><span data-stu-id="d5cbb-243">Required</span></span> |<span data-ttu-id="d5cbb-244">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="d5cbb-244">**xs:int**</span></span> |<span data-ttu-id="d5cbb-245">視訊平均位元速率，以 kb / 秒，為從 hello AssetFile 計算而得。</span><span class="sxs-lookup"><span data-stu-id="d5cbb-245">Average video bit rate in kilobits per second, as calculated from hello AssetFile.</span></span> <span data-ttu-id="d5cbb-246">計算僅 hello 基本資料流裝載，而且不包含 hello 封裝負荷。</span><span class="sxs-lookup"><span data-stu-id="d5cbb-246">Counts only hello elementary stream payload, and does not include hello packaging overhead.</span></span> |
| <span data-ttu-id="d5cbb-247">**TargetBitrate**</span><span class="sxs-lookup"><span data-stu-id="d5cbb-247">**TargetBitrate**</span></span><br/><br/> <span data-ttu-id="d5cbb-248">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="d5cbb-248">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="d5cbb-249">必要</span><span class="sxs-lookup"><span data-stu-id="d5cbb-249">Required</span></span> |<span data-ttu-id="d5cbb-250">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="d5cbb-250">**xs:int**</span></span> |<span data-ttu-id="d5cbb-251">目標平均位元速率此視訊播放軌上、 透過 hello 編碼預設，以 kb / 秒的要求。</span><span class="sxs-lookup"><span data-stu-id="d5cbb-251">Target average bitrate for this video track, as requested via hello encoding preset, in kilobits per second.</span></span> |
| <span data-ttu-id="d5cbb-252">**MaxGOPBitrate**</span><span class="sxs-lookup"><span data-stu-id="d5cbb-252">**MaxGOPBitrate**</span></span><br/><br/> <span data-ttu-id="d5cbb-253">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="d5cbb-253">minInclusive ="0"</span></span> |<span data-ttu-id="d5cbb-254">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="d5cbb-254">**xs:int**</span></span> |<span data-ttu-id="d5cbb-255">此視訊播放軌的最大 GOP 平均位元速率 (千位元 / 秒)。</span><span class="sxs-lookup"><span data-stu-id="d5cbb-255">Max GOP average bitrate for this video track, in kilobits per second.</span></span> |

## <span data-ttu-id="d5cbb-256"><a name="AudioTracks "></a> AudioTracks 元素</span><span class="sxs-lookup"><span data-stu-id="d5cbb-256"><a name="AudioTracks "></a> AudioTracks element</span></span>
<span data-ttu-id="d5cbb-257">每個實體資產檔案可以內含零個或多個交錯形成適當容器格式的音訊播放軌。</span><span class="sxs-lookup"><span data-stu-id="d5cbb-257">Each physical AssetFile can contain in it zero or more audio tracks interleaved into an appropriate container format.</span></span> <span data-ttu-id="d5cbb-258">這是所有這些音軌 hello 集合。</span><span class="sxs-lookup"><span data-stu-id="d5cbb-258">This is hello collection of all those audio tracks.</span></span>  

<span data-ttu-id="d5cbb-259">您可以找到 XML 範例 [XML 範例](media-services-output-metadata-schema.md#xml)。</span><span class="sxs-lookup"><span data-stu-id="d5cbb-259">You can find an XML example [XML example](media-services-output-metadata-schema.md#xml).</span></span>  

### <a name="child-elements"></a><span data-ttu-id="d5cbb-260">子元素</span><span class="sxs-lookup"><span data-stu-id="d5cbb-260">Child elements</span></span>
| <span data-ttu-id="d5cbb-261">名稱</span><span class="sxs-lookup"><span data-stu-id="d5cbb-261">Name</span></span> | <span data-ttu-id="d5cbb-262">說明</span><span class="sxs-lookup"><span data-stu-id="d5cbb-262">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d5cbb-263">**AudioTrack**</span><span class="sxs-lookup"><span data-stu-id="d5cbb-263">**AudioTrack**</span></span><br/><br/> <span data-ttu-id="d5cbb-264">minOccurs="1" maxOccurs="unbounded"</span><span class="sxs-lookup"><span data-stu-id="d5cbb-264">minOccurs="1" maxOccurs="unbounded"</span></span> |<span data-ttu-id="d5cbb-265">Hello 父系 AssetFile 中的特定音訊音軌。</span><span class="sxs-lookup"><span data-stu-id="d5cbb-265">A specific audio track in hello parent AssetFile.</span></span> <span data-ttu-id="d5cbb-266">如需詳細資訊，請參閱 [AudioTrack 元素](media-services-output-metadata-schema.md)。</span><span class="sxs-lookup"><span data-stu-id="d5cbb-266">For more information, see [AudioTrack element](media-services-output-metadata-schema.md).</span></span> |

## <span data-ttu-id="d5cbb-267"><a name="AudioTrack "></a> AudioTrack 元素</span><span class="sxs-lookup"><span data-stu-id="d5cbb-267"><a name="AudioTrack "></a> AudioTrack element</span></span>
<span data-ttu-id="d5cbb-268">Hello 父系 AssetFile 中的特定音訊音軌。</span><span class="sxs-lookup"><span data-stu-id="d5cbb-268">A specific audio track in hello parent AssetFile.</span></span>  

<span data-ttu-id="d5cbb-269">您可以找到 XML 範例 [XML 範例](media-services-output-metadata-schema.md#xml)。</span><span class="sxs-lookup"><span data-stu-id="d5cbb-269">You can find an XML example [XML example](media-services-output-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="d5cbb-270">屬性</span><span class="sxs-lookup"><span data-stu-id="d5cbb-270">Attributes</span></span>
| <span data-ttu-id="d5cbb-271">名稱</span><span class="sxs-lookup"><span data-stu-id="d5cbb-271">Name</span></span> | <span data-ttu-id="d5cbb-272">類型</span><span class="sxs-lookup"><span data-stu-id="d5cbb-272">Type</span></span> | <span data-ttu-id="d5cbb-273">說明</span><span class="sxs-lookup"><span data-stu-id="d5cbb-273">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d5cbb-274">**Id**</span><span class="sxs-lookup"><span data-stu-id="d5cbb-274">**Id**</span></span><br/><br/> <span data-ttu-id="d5cbb-275">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="d5cbb-275">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="d5cbb-276">必要</span><span class="sxs-lookup"><span data-stu-id="d5cbb-276">Required</span></span> |<span data-ttu-id="d5cbb-277">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="d5cbb-277">**xs:int**</span></span> |<span data-ttu-id="d5cbb-278">此音訊播放軌之以零為起始的索引。**注意：**不一定 hello TrackID MP4 檔案中使用。</span><span class="sxs-lookup"><span data-stu-id="d5cbb-278">Zero-based index of this audio track. **Note:**  This is not necessarily hello TrackID as used in an MP4 file.</span></span> |
| <span data-ttu-id="d5cbb-279">**Codec**</span><span class="sxs-lookup"><span data-stu-id="d5cbb-279">**Codec**</span></span> |<span data-ttu-id="d5cbb-280">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="d5cbb-280">**xs:string**</span></span> |<span data-ttu-id="d5cbb-281">音訊播放軌轉碼器字串。</span><span class="sxs-lookup"><span data-stu-id="d5cbb-281">Audio track codec string.</span></span> |
| <span data-ttu-id="d5cbb-282">**EncoderVersion**</span><span class="sxs-lookup"><span data-stu-id="d5cbb-282">**EncoderVersion**</span></span> |<span data-ttu-id="d5cbb-283">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="d5cbb-283">**xs:string**</span></span> |<span data-ttu-id="d5cbb-284">選用的編碼器版本字串，為 EAC3 所需。</span><span class="sxs-lookup"><span data-stu-id="d5cbb-284">Optional encoder version string, required for EAC3.</span></span> |
| <span data-ttu-id="d5cbb-285">**Channels**</span><span class="sxs-lookup"><span data-stu-id="d5cbb-285">**Channels**</span></span><br/><br/> <span data-ttu-id="d5cbb-286">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="d5cbb-286">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="d5cbb-287">必要</span><span class="sxs-lookup"><span data-stu-id="d5cbb-287">Required</span></span> |<span data-ttu-id="d5cbb-288">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="d5cbb-288">**xs:int**</span></span> |<span data-ttu-id="d5cbb-289">音訊聲道數目。</span><span class="sxs-lookup"><span data-stu-id="d5cbb-289">Number of audio channels.</span></span> |
| <span data-ttu-id="d5cbb-290">**SamplingRate**</span><span class="sxs-lookup"><span data-stu-id="d5cbb-290">**SamplingRate**</span></span><br/><br/> <span data-ttu-id="d5cbb-291">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="d5cbb-291">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="d5cbb-292">必要</span><span class="sxs-lookup"><span data-stu-id="d5cbb-292">Required</span></span> |<span data-ttu-id="d5cbb-293">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="d5cbb-293">**xs:int**</span></span> |<span data-ttu-id="d5cbb-294">音訊取樣率 (每秒或每 Hz 的樣本數)。</span><span class="sxs-lookup"><span data-stu-id="d5cbb-294">Audio sampling rate in samples/sec or Hz.</span></span> |
| <span data-ttu-id="d5cbb-295">**Bitrate**</span><span class="sxs-lookup"><span data-stu-id="d5cbb-295">**Bitrate**</span></span><br/><br/> <span data-ttu-id="d5cbb-296">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="d5cbb-296">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="d5cbb-297">必要</span><span class="sxs-lookup"><span data-stu-id="d5cbb-297">Required</span></span> |<span data-ttu-id="d5cbb-298">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="d5cbb-298">**xs:int**</span></span> |<span data-ttu-id="d5cbb-299">音訊平均位元速率，以每秒位元，以從 hello AssetFile 計算而得。</span><span class="sxs-lookup"><span data-stu-id="d5cbb-299">Average audio bit rate in bits per second, as calculated from hello AssetFile.</span></span> <span data-ttu-id="d5cbb-300">計算僅 hello 基本資料流裝載，而且不包含 hello 封裝負荷。</span><span class="sxs-lookup"><span data-stu-id="d5cbb-300">Counts only hello elementary stream payload, and does not include hello packaging overhead.</span></span> |
| <span data-ttu-id="d5cbb-301">**BitsPerSample**</span><span class="sxs-lookup"><span data-stu-id="d5cbb-301">**BitsPerSample**</span></span><br/><br/> <span data-ttu-id="d5cbb-302">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="d5cbb-302">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="d5cbb-303">必要</span><span class="sxs-lookup"><span data-stu-id="d5cbb-303">Required</span></span> |<span data-ttu-id="d5cbb-304">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="d5cbb-304">**xs:int**</span></span> |<span data-ttu-id="d5cbb-305">位元，每個範例的 hello wFormatTag 格式類型。</span><span class="sxs-lookup"><span data-stu-id="d5cbb-305">Bits per sample for hello wFormatTag format type.</span></span> |

### <a name="child-elements"></a><span data-ttu-id="d5cbb-306">子元素</span><span class="sxs-lookup"><span data-stu-id="d5cbb-306">Child elements</span></span>
| <span data-ttu-id="d5cbb-307">名稱</span><span class="sxs-lookup"><span data-stu-id="d5cbb-307">Name</span></span> | <span data-ttu-id="d5cbb-308">說明</span><span class="sxs-lookup"><span data-stu-id="d5cbb-308">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d5cbb-309">**LoudnessMeteringResultParameters**</span><span class="sxs-lookup"><span data-stu-id="d5cbb-309">**LoudnessMeteringResultParameters**</span></span><br/><br/> <span data-ttu-id="d5cbb-310">minOccurs="0" maxOccurs="1"</span><span class="sxs-lookup"><span data-stu-id="d5cbb-310">minOccurs="0" maxOccurs="1"</span></span> |<span data-ttu-id="d5cbb-311">音量計量結果參數。</span><span class="sxs-lookup"><span data-stu-id="d5cbb-311">Loudness metering result parameters.</span></span> <span data-ttu-id="d5cbb-312">如需詳細資訊，請參閱 [LoudnessMeteringResultParameters 元素](media-services-output-metadata-schema.md)。</span><span class="sxs-lookup"><span data-stu-id="d5cbb-312">For more information, see [LoudnessMeteringResultParameters element](media-services-output-metadata-schema.md).</span></span> |

## <span data-ttu-id="d5cbb-313"><a name="LoudnessMeteringResultParameters "></a> LoudnessMeteringResultParameters 元素</span><span class="sxs-lookup"><span data-stu-id="d5cbb-313"><a name="LoudnessMeteringResultParameters "></a> LoudnessMeteringResultParameters element</span></span>
<span data-ttu-id="d5cbb-314">音量計量結果參數。</span><span class="sxs-lookup"><span data-stu-id="d5cbb-314">Loudness metering result parameters.</span></span>  

<span data-ttu-id="d5cbb-315">您可以找到 XML 範例 [XML 範例](media-services-output-metadata-schema.md#xml)。</span><span class="sxs-lookup"><span data-stu-id="d5cbb-315">You can find an XML example [XML example](media-services-output-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="d5cbb-316">屬性</span><span class="sxs-lookup"><span data-stu-id="d5cbb-316">Attributes</span></span>
| <span data-ttu-id="d5cbb-317">名稱</span><span class="sxs-lookup"><span data-stu-id="d5cbb-317">Name</span></span> | <span data-ttu-id="d5cbb-318">類型</span><span class="sxs-lookup"><span data-stu-id="d5cbb-318">Type</span></span> | <span data-ttu-id="d5cbb-319">說明</span><span class="sxs-lookup"><span data-stu-id="d5cbb-319">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d5cbb-320">**DPLMVersionInformation**</span><span class="sxs-lookup"><span data-stu-id="d5cbb-320">**DPLMVersionInformation**</span></span> |<span data-ttu-id="d5cbb-321">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="d5cbb-321">**xs:string**</span></span> |<span data-ttu-id="d5cbb-322">**Dolby** 專業音量計量開發套件版本。</span><span class="sxs-lookup"><span data-stu-id="d5cbb-322">**Dolby** professional loudness metering development kit version.</span></span> |
| <span data-ttu-id="d5cbb-323">**DialogNormalization**</span><span class="sxs-lookup"><span data-stu-id="d5cbb-323">**DialogNormalization**</span></span><br/><br/> <span data-ttu-id="d5cbb-324">minInclusive="-31" maxInclusive="-1"</span><span class="sxs-lookup"><span data-stu-id="d5cbb-324">minInclusive="-31" maxInclusive="-1"</span></span><br/><br/> <span data-ttu-id="d5cbb-325">必要</span><span class="sxs-lookup"><span data-stu-id="d5cbb-325">Required</span></span> |<span data-ttu-id="d5cbb-326">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="d5cbb-326">**xs:int**</span></span> |<span data-ttu-id="d5cbb-327">透過 DPLM 產生的 DialogNormalization，若設定了 LoudnessMetering 則為必要</span><span class="sxs-lookup"><span data-stu-id="d5cbb-327">DialogNormalization generated through DPLM, required when LoudnessMetering is set</span></span> |
| <span data-ttu-id="d5cbb-328">**IntegratedLoudness**</span><span class="sxs-lookup"><span data-stu-id="d5cbb-328">**IntegratedLoudness**</span></span><br/><br/> <span data-ttu-id="d5cbb-329">minInclusive="-70" maxInclusive="10"</span><span class="sxs-lookup"><span data-stu-id="d5cbb-329">minInclusive="-70" maxInclusive="10"</span></span><br/><br/> <span data-ttu-id="d5cbb-330">必要</span><span class="sxs-lookup"><span data-stu-id="d5cbb-330">Required</span></span> |<span data-ttu-id="d5cbb-331">**xs:float**</span><span class="sxs-lookup"><span data-stu-id="d5cbb-331">**xs:float**</span></span> |<span data-ttu-id="d5cbb-332">整合的音量</span><span class="sxs-lookup"><span data-stu-id="d5cbb-332">Integrated loudness</span></span> |
| <span data-ttu-id="d5cbb-333">**IntegratedLoudnessUnit**</span><span class="sxs-lookup"><span data-stu-id="d5cbb-333">**IntegratedLoudnessUnit**</span></span><br/><br/> <span data-ttu-id="d5cbb-334">必要</span><span class="sxs-lookup"><span data-stu-id="d5cbb-334">Required</span></span> |<span data-ttu-id="d5cbb-335">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="d5cbb-335">**xs:string**</span></span> |<span data-ttu-id="d5cbb-336">整合的音量單位。</span><span class="sxs-lookup"><span data-stu-id="d5cbb-336">Integrated loudness unit.</span></span> |
| <span data-ttu-id="d5cbb-337">**IntegratedLoudnessGatingMethod**</span><span class="sxs-lookup"><span data-stu-id="d5cbb-337">**IntegratedLoudnessGatingMethod**</span></span><br/><br/> <span data-ttu-id="d5cbb-338">必要</span><span class="sxs-lookup"><span data-stu-id="d5cbb-338">Required</span></span> |<span data-ttu-id="d5cbb-339">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="d5cbb-339">**xs:string**</span></span> |<span data-ttu-id="d5cbb-340">閘控識別碼</span><span class="sxs-lookup"><span data-stu-id="d5cbb-340">Gating identifier</span></span> |
| <span data-ttu-id="d5cbb-341">**IntegratedLoudnessSpeechPercentage**</span><span class="sxs-lookup"><span data-stu-id="d5cbb-341">**IntegratedLoudnessSpeechPercentage**</span></span><br/><br/> <span data-ttu-id="d5cbb-342">minInclusive ="0" maxInclusive="100"</span><span class="sxs-lookup"><span data-stu-id="d5cbb-342">minInclusive ="0" maxInclusive="100"</span></span> |<span data-ttu-id="d5cbb-343">**xs:float**</span><span class="sxs-lookup"><span data-stu-id="d5cbb-343">**xs:float**</span></span> |<span data-ttu-id="d5cbb-344">透過 hello 程式，以百分比表示的語音內容。</span><span class="sxs-lookup"><span data-stu-id="d5cbb-344">Speech content over hello program, as a percentage.</span></span> |
| <span data-ttu-id="d5cbb-345">**SamplePeak**</span><span class="sxs-lookup"><span data-stu-id="d5cbb-345">**SamplePeak**</span></span><br/><br/> <span data-ttu-id="d5cbb-346">必要</span><span class="sxs-lookup"><span data-stu-id="d5cbb-346">Required</span></span> |<span data-ttu-id="d5cbb-347">**xs:float**</span><span class="sxs-lookup"><span data-stu-id="d5cbb-347">**xs:float**</span></span> |<span data-ttu-id="d5cbb-348">自重設或上次清除後，每個聲道的尖峰絕對樣本值。</span><span class="sxs-lookup"><span data-stu-id="d5cbb-348">Peak absolute sample value, since reset or since it was last cleared, per channel.</span></span>  <span data-ttu-id="d5cbb-349">單位是 dBFS。</span><span class="sxs-lookup"><span data-stu-id="d5cbb-349">Units are dBFS.</span></span> |
| <span data-ttu-id="d5cbb-350">**SamplePeakUnit**</span><span class="sxs-lookup"><span data-stu-id="d5cbb-350">**SamplePeakUnit**</span></span><br/><br/> <span data-ttu-id="d5cbb-351">fixed="dBFS"</span><span class="sxs-lookup"><span data-stu-id="d5cbb-351">fixed="dBFS"</span></span><br/><br/> <span data-ttu-id="d5cbb-352">必要</span><span class="sxs-lookup"><span data-stu-id="d5cbb-352">Required</span></span> |<span data-ttu-id="d5cbb-353">**xs:anySimpleType**</span><span class="sxs-lookup"><span data-stu-id="d5cbb-353">**xs:anySimpleType**</span></span> |<span data-ttu-id="d5cbb-354">樣本尖峰單位。</span><span class="sxs-lookup"><span data-stu-id="d5cbb-354">Sample peak unit.</span></span> |
| <span data-ttu-id="d5cbb-355">**TruePeak**</span><span class="sxs-lookup"><span data-stu-id="d5cbb-355">**TruePeak**</span></span><br/><br/> <span data-ttu-id="d5cbb-356">必要</span><span class="sxs-lookup"><span data-stu-id="d5cbb-356">Required</span></span> |<span data-ttu-id="d5cbb-357">**xs:float**</span><span class="sxs-lookup"><span data-stu-id="d5cbb-357">**xs:float**</span></span> |<span data-ttu-id="d5cbb-358">根據 ITU-R BS.1770-2，自重設或上次清除後，每個聲道的最大實際尖峰值。</span><span class="sxs-lookup"><span data-stu-id="d5cbb-358">Maximum true peak value, as per ITU-R BS.1770-2, since reset or since it was last cleared, per channel.</span></span> <span data-ttu-id="d5cbb-359">單位是 dBTP。</span><span class="sxs-lookup"><span data-stu-id="d5cbb-359">Units are dBTP.</span></span> |
| <span data-ttu-id="d5cbb-360">**TruePeakUnit**</span><span class="sxs-lookup"><span data-stu-id="d5cbb-360">**TruePeakUnit**</span></span><br/><br/> <span data-ttu-id="d5cbb-361">fixed="dBTP"</span><span class="sxs-lookup"><span data-stu-id="d5cbb-361">fixed="dBTP"</span></span><br/><br/> <span data-ttu-id="d5cbb-362">必要</span><span class="sxs-lookup"><span data-stu-id="d5cbb-362">Required</span></span> |<span data-ttu-id="d5cbb-363">**xs:anySimpleType**</span><span class="sxs-lookup"><span data-stu-id="d5cbb-363">**xs:anySimpleType**</span></span> |<span data-ttu-id="d5cbb-364">實際尖峰單位。</span><span class="sxs-lookup"><span data-stu-id="d5cbb-364">True peak unit.</span></span> |

## <a name="schema-code"></a><span data-ttu-id="d5cbb-365">結構描述程式碼</span><span class="sxs-lookup"><span data-stu-id="d5cbb-365">Schema Code</span></span>
    <?xml version="1.0" encoding="utf-8"?>  
    <xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:msdata="urn:schemas-microsoft-com:xml-msdata" version="1.2"  
               xmlns="http://schemas.microsoft.com/windowsazure/mediaservices/2013/05/mediaencoder/metadata"  
               targetNamespace="http://schemas.microsoft.com/windowsazure/mediaservices/2013/05/mediaencoder/metadata"  
               elementFormDefault="qualified">  
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
                  <xs:element name="Sources">  
                    <xs:annotation>  
                      <xs:documentation>Collection of input/source media files, that was processed in order tooproduce this AssetFile</xs:documentation>  
                    </xs:annotation>  
                    <xs:complexType>  
                      <xs:sequence>  
                        <xs:element name="Source" minOccurs="1" maxOccurs="unbounded">  
                          <xs:annotation>  
                            <xs:documentation>An input/source file used when generating this asset</xs:documentation>  
                          </xs:annotation>  
                          <xs:complexType>  
                            <xs:attribute name="Name" type="xs:string" use="required">  
                              <xs:annotation>  
                                <xs:documentation>input source file name</xs:documentation>  
                              </xs:annotation>  
                            </xs:attribute>  
                          </xs:complexType>  
                        </xs:element>  
                      </xs:sequence>  
                    </xs:complexType>  
                  </xs:element>  
                  <xs:element name="VideoTracks" minOccurs="0">  
                    <xs:annotation>  
                      <xs:documentation>Each physical AssetFile can contain in it zero or more video tracks interleaved into an appropriate container format. This is hello collection of all those video tracks</xs:documentation>  
                    </xs:annotation>  
                    <xs:complexType>  
                      <xs:sequence>  
                        <xs:element name="VideoTrack" maxOccurs="unbounded">  
                          <xs:annotation>  
                            <xs:documentation>A specific video track in hello parent AssetFile</xs:documentation>  
                          </xs:annotation>  
                          <xs:complexType>  
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
                            <xs:attribute name="FourCC" type="xs:string" use="required">  
                              <xs:annotation>  
                                <xs:documentation>video codec FourCC code</xs:documentation>  
                              </xs:annotation>  
                            </xs:attribute>  
                            <xs:attribute name="Profile" type="xs:string">  
                              <xs:annotation>  
                                <xs:documentation>H264 profile (only appliable for H264 codec)</xs:documentation>  
                              </xs:annotation>  
                            </xs:attribute>  
                            <xs:attribute name="Level" type="xs:string">  
                              <xs:annotation>  
                                <xs:documentation>H264 level (only appliable for H264 codec)</xs:documentation>  
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
                            <xs:attribute name="Framerate" use="required">  
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
                            <xs:attribute name="TargetFramerate" use="required">  
                              <xs:annotation>  
                                <xs:documentation>preset target video frame rate in .3f format</xs:documentation>  
                              </xs:annotation>  
                              <xs:simpleType>  
                                <xs:restriction base="xs:decimal">  
                                  <xs:minInclusive value="0"/>  
                                  <xs:fractionDigits value="3"/>  
                                </xs:restriction>  
                              </xs:simpleType>  
                            </xs:attribute>  
                            <xs:attribute name="Bitrate" use="required">  
                              <xs:annotation>  
                                <xs:documentation>average video bit rate in kilobits per second, as calculated from hello AssetFile. Counts only hello elementary stream payload, and does not include hello packaging overhead</xs:documentation>  
                              </xs:annotation>  
                              <xs:simpleType>  
                                <xs:restriction base="xs:int">  
                                  <xs:minInclusive value="0"/>  
                                </xs:restriction>  
                              </xs:simpleType>  
                            </xs:attribute>  
                            <xs:attribute name="TargetBitrate" use="required">  
                              <xs:annotation>  
                                <xs:documentation>target average bitrate for this video track, as requested via hello encoding preset, in kilobits per second</xs:documentation>  
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
                          </xs:complexType>  
                        </xs:element>  
                      </xs:sequence>  
                    </xs:complexType>  
                  </xs:element>  
                  <xs:element name="AudioTracks" minOccurs="0">  
                    <xs:annotation>  
                      <xs:documentation>each physical AssetFile can contain in it zero or more audio tracks interleaved into an appropriate container format. This is hello collection of all those audio tracks</xs:documentation>  
                    </xs:annotation>  
                    <xs:complexType>  
                      <xs:sequence>  
                        <xs:element name="AudioTrack" maxOccurs="unbounded">  
                          <xs:annotation>  
                            <xs:documentation>a specific audio track in hello parent AssetFile</xs:documentation>  
                          </xs:annotation>  
                          <xs:complexType>  
                            <xs:sequence>  
                              <xs:element name="LoudnessMeteringResultParameters" minOccurs="0" maxOccurs="1">  
                                <xs:annotation>  
                                  <xs:documentation>Loudness Metering Result Parameters</xs:documentation>  
                                </xs:annotation>  
                                <xs:complexType>  
                                  <xs:attribute name="DPLMVersionInformation" type="xs:string">  
                                    <xs:annotation>  
                                      <xs:documentation>Dolby Professional Loudness Metering Development Kit Version</xs:documentation>  
                                    </xs:annotation>  
                                  </xs:attribute>  
                                  <xs:attribute name="DialogNormalization" use="required">  
                                    <xs:annotation>  
                                      <xs:documentation> DialogNormalization generated through DPLM, required when LoudnessMetering is set</xs:documentation>  
                                    </xs:annotation>  
                                    <xs:simpleType>  
                                      <xs:restriction base="xs:int">  
                                        <xs:minInclusive value="-31"/>  
                                        <xs:maxInclusive value="-1"/>  
                                      </xs:restriction>  
                                    </xs:simpleType>  
                                  </xs:attribute>  
                                  <xs:attribute name="IntegratedLoudness" use="required">  
                                    <xs:annotation>  
                                      <xs:documentation>Integrated loudness</xs:documentation>  
                                    </xs:annotation>  
                                    <xs:simpleType>  
                                      <xs:restriction base="xs:float">  
                                        <xs:minInclusive value="-70"/>  
                                        <xs:maxInclusive value="10"/>  
                                      </xs:restriction>  
                                    </xs:simpleType>  
                                  </xs:attribute>  
                                  <xs:attribute name="IntegratedLoudnessUnit" use="required" type="xs:string">  
                                  </xs:attribute>  
                                  <xs:attribute name="IntegratedLoudnessGatingMethod" use="required" type="xs:string">  
                                    <xs:annotation>  
                                      <xs:documentation>Gating identifier</xs:documentation>  
                                    </xs:annotation>  
                                  </xs:attribute>  
                                  <xs:attribute name="IntegratedLoudnessSpeechPercentage">  
                                    <xs:annotation>  
                                      <xs:documentation>Speech content over hello program, as a percentage.</xs:documentation>  
                                    </xs:annotation>  
                                    <xs:simpleType>  
                                      <xs:restriction base="xs:float">  
                                        <xs:minInclusive value="0"/>  
                                        <xs:maxInclusive value="100"/>  
                                      </xs:restriction>  
                                    </xs:simpleType>  
                                  </xs:attribute>  
                                  <xs:attribute name="SamplePeak" use="required" type="xs:float">  
                                    <xs:annotation>  
                                      <xs:documentation>Peak absolute sample value, since reset or since it was last cleared, per channel.  Units are dBFS.</xs:documentation>  
                                    </xs:annotation>  
                                  </xs:attribute>  
                                  <xs:attribute name="SamplePeakUnit" use="required" fixed="dBFS">  
                                  </xs:attribute>  
                                  <xs:attribute name="TruePeak" use="required" type="xs:float">  
                                    <xs:annotation>  
                                      <xs:documentation>Maximum True Peak value, as per ITU-R BS.1770-2, since reset or since it was last cleared, per channel.  Units are dBTP.</xs:documentation>  
                                    </xs:annotation>  
                                  </xs:attribute>  
                                  <xs:attribute name="TruePeakUnit" use="required" fixed="dBTP">  
                                  </xs:attribute>  
                                </xs:complexType>  
                              </xs:element>  
                            </xs:sequence>  
                            <xs:attribute name="Id" use="required">  
                              <xs:annotation>  
                                <xs:documentation>zero-based index of this audio track. Note: this is not necessarily hello TrackID as used in an MP4 file</xs:documentation>  
                              </xs:annotation>  
                              <xs:simpleType>  
                                <xs:restriction base="xs:int">  
                                  <xs:minInclusive value="0"/>  
                                </xs:restriction>  
                              </xs:simpleType>  
                            </xs:attribute>  
                            <xs:attribute name="Codec" type="xs:string">  
                              <xs:annotation>  
                                <xs:documentation>audio track codec string</xs:documentation>  
                              </xs:annotation>  
                            </xs:attribute>  
                            <xs:attribute name="EncoderVersion" type="xs:string">  
                              <xs:annotation>  
                                <xs:documentation>optional encoder version string, required for EAC3</xs:documentation>  
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
                            <xs:attribute name="Bitrate" use="required">  
                              <xs:annotation>  
                                <xs:documentation>average audio bit rate in bits per second, as calculated from hello AssetFile. Counts only hello elementary stream payload, and does not include hello packaging overhead</xs:documentation>  
                              </xs:annotation>  
                              <xs:simpleType>  
                                <xs:restriction base="xs:int">  
                                  <xs:minInclusive value="0"/>  
                                </xs:restriction>  
                              </xs:simpleType>  
                            </xs:attribute>  
                            <xs:attribute name="BitsPerSample" use="required">  
                              <xs:annotation>  
                                <xs:documentation>Bits per sample for hello wFormatTag format type</xs:documentation>  
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
                <xs:attribute name="Duration" use="required">  
                  <xs:annotation>  
                    <xs:documentation>content play back duration</xs:documentation>  
                  </xs:annotation>  
                  <xs:simpleType>  
                    <xs:restriction base="xs:duration"/>  
                  </xs:simpleType>  
                </xs:attribute>  
              </xs:complexType>  
            </xs:element>  
          </xs:sequence>  
        </xs:complexType>  
      </xs:element>  
    </xs:schema>  



## <span data-ttu-id="d5cbb-366"><a name="xml"></a> XML 範例</span><span class="sxs-lookup"><span data-stu-id="d5cbb-366"><a name="xml"></a> XML example</span></span>
 <span data-ttu-id="d5cbb-367">hello 以下是 hello 輸出中繼資料檔案的範例。</span><span class="sxs-lookup"><span data-stu-id="d5cbb-367">hello following is an example of hello Output metadata file.</span></span>  

    <AssetFiles xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
                xmlns="http://schemas.microsoft.com/windowsazure/mediaservices/2013/05/mediaencoder/metadata">  
      <AssetFile Name="BigBuckBunny_H264_3400kbps_AAC_und_ch2_96kbps.mp4" Size="4646283" Duration="PT8.4288444S">  
        <Sources>  
          <Source Name="BigBuckBunny.mp4"/>  
        </Sources>  
        <VideoTracks>  
          <VideoTrack Id="0" FourCC="AVC1" Profile="Main" Level="3.2" Width="1280" Height="720" DisplayAspectRatioNumerator="16" DisplayAspectRatioDenominator="9" Framerate="23.974" TargetFramerate="23.974" Bitrate="4250" TargetBitrate="3400" MaxGOPBitrate="5514"/>  
        </VideoTracks>  
        <AudioTracks>  
          <AudioTrack Id="0" Codec="AacLc" Channels="2" SamplingRate="44100" Bitrate="93" BitsPerSample="16"/>  
        </AudioTracks>  
      </AssetFile>  
      <AssetFile Name="BigBuckBunny_H264_2250kbps_AAC_und_ch2_96kbps.mp4" Size="3166728" Duration="PT8.4288444S">  
        <Sources>  
          <Source Name="BigBuckBunny.mp4"/>  
        </Sources>  
        <VideoTracks>  
          <VideoTrack Id="0" FourCC="AVC1" Profile="Main" Level="3.1" Width="960" Height="540" DisplayAspectRatioNumerator="16" DisplayAspectRatioDenominator="9" Framerate="23.974" TargetFramerate="23.974" Bitrate="2846" TargetBitrate="2250" MaxGOPBitrate="3630"/>  
        </VideoTracks>  
        <AudioTracks>  
          <AudioTrack Id="0" Codec="AacLc" Channels="2" SamplingRate="44100" Bitrate="93" BitsPerSample="16"/>  
        </AudioTracks>  
      </AssetFile>  
      <AssetFile Name="BigBuckBunny_H264_1500kbps_AAC_und_ch2_96kbps.mp4" Size="2205095" Duration="PT8.4288444S">  
        <Sources>  
          <Source Name="BigBuckBunny.mp4"/>  
        </Sources>  
        <VideoTracks>  
          <VideoTrack Id="0" FourCC="AVC1" Profile="Main" Level="3.1" Width="960" Height="540" DisplayAspectRatioNumerator="16" DisplayAspectRatioDenominator="9" Framerate="23.974" TargetFramerate="23.974" Bitrate="1932" TargetBitrate="1500" MaxGOPBitrate="2513"/>  
        </VideoTracks>  
        <AudioTracks>  
          <AudioTrack Id="0" Codec="AacLc" Channels="2" SamplingRate="44100" Bitrate="93" BitsPerSample="16"/>  
        </AudioTracks>  
      </AssetFile>  
      <AssetFile Name="BigBuckBunny_H264_1000kbps_AAC_und_ch2_96kbps.mp4" Size="1508567" Duration="PT8.4288444S">  
        <Sources>  
          <Source Name="BigBuckBunny.mp4"/>  
        </Sources>  
        <VideoTracks>  
          <VideoTrack Id="0" FourCC="AVC1" Profile="Main" Level="3.0" Width="640" Height="360" DisplayAspectRatioNumerator="16" DisplayAspectRatioDenominator="9" Framerate="23.974" TargetFramerate="23.974" Bitrate="1271" TargetBitrate="1000" MaxGOPBitrate="1527"/>  
        </VideoTracks>  
        <AudioTracks>  
          <AudioTrack Id="0" Codec="AacLc" Channels="2" SamplingRate="44100" Bitrate="93" BitsPerSample="16"/>  
        </AudioTracks>  
      </AssetFile>  
      <AssetFile Name="BigBuckBunny_H264_650kbps_AAC_und_ch2_96kbps.mp4" Size="1057155" Duration="PT8.4288444S">  
        <Sources>  
          <Source Name="BigBuckBunny.mp4"/>  
        </Sources>  
        <VideoTracks>  
          <VideoTrack Id="0" FourCC="AVC1" Profile="Main" Level="3.0" Width="640" Height="360" DisplayAspectRatioNumerator="16" DisplayAspectRatioDenominator="9" Framerate="23.974" TargetFramerate="23.974" Bitrate="843" TargetBitrate="650" MaxGOPBitrate="1086"/>  
        </VideoTracks>  
        <AudioTracks>  
          <AudioTrack Id="0" Codec="AacLc" Channels="2" SamplingRate="44100" Bitrate="93" BitsPerSample="16"/>  
        </AudioTracks>  
      </AssetFile>  
      <AssetFile Name="BigBuckBunny_H264_400kbps_AAC_und_ch2_96kbps.mp4" Size="699262" Duration="PT8.4288444S">  
        <Sources>  
          <Source Name="BigBuckBunny.mp4"/>  
        </Sources>  
        <VideoTracks>  
          <VideoTrack Id="0" FourCC="AVC1" Profile="Main" Level="1.3" Width="320" Height="180" DisplayAspectRatioNumerator="16" DisplayAspectRatioDenominator="9" Framerate="23.974" TargetFramerate="23.974" Bitrate="503" TargetBitrate="400" MaxGOPBitrate="661"/>  
        </VideoTracks>  
        <AudioTracks>  
          <AudioTrack Id="0" Codec="AacLc" Channels="2" SamplingRate="44100" Bitrate="93" BitsPerSample="16"/>  
        </AudioTracks>  
      </AssetFile>  
      <AssetFile Name="BigBuckBunny_AAC_und_ch2_96kbps.mp4" Size="166780" Duration="PT8.4288444S">  
        <Sources>  
          <Source Name="BigBuckBunny.mp4"/>  
        </Sources>  
        <AudioTracks>  
          <AudioTrack Id="0" Codec="AacLc" Channels="2" SamplingRate="44100" Bitrate="93" BitsPerSample="16"/>  
        </AudioTracks>  
      </AssetFile>  
      <AssetFile Name="BigBuckBunny_AAC_und_ch2_56kbps.mp4" Size="124576" Duration="PT8.4288444S">  
        <Sources>  
          <Source Name="BigBuckBunny.mp4"/>  
        </Sources>  
        <AudioTracks>  
          <AudioTrack Id="0" Codec="AacLc" Channels="2" SamplingRate="44100" Bitrate="53" BitsPerSample="16"/>  
        </AudioTracks>  
      </AssetFile>  
    </AssetFiles>  

## <a name="next-steps"></a><span data-ttu-id="d5cbb-368">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d5cbb-368">Next steps</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="d5cbb-369">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="d5cbb-369">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
