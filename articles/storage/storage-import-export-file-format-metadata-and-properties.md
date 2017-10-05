---
title: "Azure 匯入/匯出中繼資料和屬性檔案格式 | Microsoft Docs"
description: "了解如何針對匯入或匯出作業中的一或多個 blob 指定中繼資料和屬性。"
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 840364c6-d9a8-4b43-a9f3-f7441c625069
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: 3f728ad94cdcbd32092b677f11a737ae91376720
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="azure-importexport-service-metadata-and-properties-file-format"></a><span data-ttu-id="64d00-103">Azure 匯入/匯出服務中繼資料和屬性檔案格式</span><span class="sxs-lookup"><span data-stu-id="64d00-103">Azure Import/Export service metadata and properties file format</span></span>
<span data-ttu-id="64d00-104">您可以針對匯入或匯出作業中的一或多個 blob 指定中繼資料和屬性。</span><span class="sxs-lookup"><span data-stu-id="64d00-104">You can specify metadata and properties for one or more blobs as part of an import job or an export job.</span></span> <span data-ttu-id="64d00-105">若要針對建立為匯入作業一部分的 blob 設定中繼資料或屬性，您可在包含要匯入資料的硬碟上提供中繼資料或屬性檔案。</span><span class="sxs-lookup"><span data-stu-id="64d00-105">To set metadata or properties for blobs being created as part of an import job, you provide a metadata or properties file on the hard drive containing the data to be imported.</span></span> <span data-ttu-id="64d00-106">若為匯出作業，中繼資料和屬性會寫入至中繼資料或屬性檔案 (包含在傳回給您的硬碟上)。</span><span class="sxs-lookup"><span data-stu-id="64d00-106">For an export job, metadata and properties are written to a metadata or properties file that is included on the hard drive returned to you.</span></span>  
  
## <a name="metadata-file-format"></a><span data-ttu-id="64d00-107">中繼資料檔案格式</span><span class="sxs-lookup"><span data-stu-id="64d00-107">Metadata file format</span></span>  
<span data-ttu-id="64d00-108">中繼資料檔案的格式如下所示：</span><span class="sxs-lookup"><span data-stu-id="64d00-108">The format of a metadata file is as follows:</span></span>  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<Metadata>  
[<metadata-name-1>metadata-value-1</metadata-name-1>]  
[<metadata-name-2>metadata-value-2</metadata-name-2>]  
. . .  
</Metadata>  
```
  
|<span data-ttu-id="64d00-109">XML 元素</span><span class="sxs-lookup"><span data-stu-id="64d00-109">XML Element</span></span>|<span data-ttu-id="64d00-110">類型</span><span class="sxs-lookup"><span data-stu-id="64d00-110">Type</span></span>|<span data-ttu-id="64d00-111">說明</span><span class="sxs-lookup"><span data-stu-id="64d00-111">Description</span></span>|  
|-----------------|----------|-----------------|  
|`Metadata`|<span data-ttu-id="64d00-112">根元素</span><span class="sxs-lookup"><span data-stu-id="64d00-112">Root element</span></span>|<span data-ttu-id="64d00-113">中繼資料檔案的根項目。</span><span class="sxs-lookup"><span data-stu-id="64d00-113">The root element of the metadata file.</span></span>|  
|`metadata-name`|<span data-ttu-id="64d00-114">String</span><span class="sxs-lookup"><span data-stu-id="64d00-114">String</span></span>|<span data-ttu-id="64d00-115">選用。</span><span class="sxs-lookup"><span data-stu-id="64d00-115">Optional.</span></span> <span data-ttu-id="64d00-116">XML 元素可指定 blob 的中繼資料名稱，而其值可指定中繼資料設定的值。</span><span class="sxs-lookup"><span data-stu-id="64d00-116">The XML element specifies the name of the metadata for the blob, and its value specifies the value of the metadata setting.</span></span>|  
  
## <a name="properties-file-format"></a><span data-ttu-id="64d00-117">屬性檔案格式</span><span class="sxs-lookup"><span data-stu-id="64d00-117">Properties file format</span></span>  
<span data-ttu-id="64d00-118">屬性檔案的格式如下所示：</span><span class="sxs-lookup"><span data-stu-id="64d00-118">The format of a properties file is as follows:</span></span>  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<Properties>  
[<Last-Modified>date-time-value</Last-Modified>]  
[<Etag>etag</Etag>]  
[<Content-Length>size-in-bytes<Content-Length>]  
[<Content-Type>content-type</Content-Type>]  
[<Content-MD5>content-md5</Content-MD5>]  
[<Content-Encoding>content-encoding</Content-Encoding>]  
[<Content-Language>content-language</Content-Language>]  
[<Cache-Control>cache-control</Cache-Control>]  
</Properties>  
```
  
|<span data-ttu-id="64d00-119">XML 元素</span><span class="sxs-lookup"><span data-stu-id="64d00-119">XML Element</span></span>|<span data-ttu-id="64d00-120">類型</span><span class="sxs-lookup"><span data-stu-id="64d00-120">Type</span></span>|<span data-ttu-id="64d00-121">說明</span><span class="sxs-lookup"><span data-stu-id="64d00-121">Description</span></span>|  
|-----------------|----------|-----------------|  
|`Properties`|<span data-ttu-id="64d00-122">根元素</span><span class="sxs-lookup"><span data-stu-id="64d00-122">Root element</span></span>|<span data-ttu-id="64d00-123">屬性檔案的根元素。</span><span class="sxs-lookup"><span data-stu-id="64d00-123">The root element of the properties file.</span></span>|  
|`Last-Modified`|<span data-ttu-id="64d00-124">String</span><span class="sxs-lookup"><span data-stu-id="64d00-124">String</span></span>|<span data-ttu-id="64d00-125">選用。</span><span class="sxs-lookup"><span data-stu-id="64d00-125">Optional.</span></span> <span data-ttu-id="64d00-126">Blob 上次修改時間。</span><span class="sxs-lookup"><span data-stu-id="64d00-126">The last-modified time for the blob.</span></span> <span data-ttu-id="64d00-127">僅限匯出作業。</span><span class="sxs-lookup"><span data-stu-id="64d00-127">For export jobs only.</span></span>|  
|`Etag`|<span data-ttu-id="64d00-128">String</span><span class="sxs-lookup"><span data-stu-id="64d00-128">String</span></span>|<span data-ttu-id="64d00-129">選用。</span><span class="sxs-lookup"><span data-stu-id="64d00-129">Optional.</span></span> <span data-ttu-id="64d00-130">Blob 的 ETag 值。</span><span class="sxs-lookup"><span data-stu-id="64d00-130">The blob's ETag value.</span></span> <span data-ttu-id="64d00-131">僅限匯出作業。</span><span class="sxs-lookup"><span data-stu-id="64d00-131">For export jobs only.</span></span>|  
|`Content-Length`|<span data-ttu-id="64d00-132">String</span><span class="sxs-lookup"><span data-stu-id="64d00-132">String</span></span>|<span data-ttu-id="64d00-133">選用。</span><span class="sxs-lookup"><span data-stu-id="64d00-133">Optional.</span></span> <span data-ttu-id="64d00-134">Blob 大小 (以位元組為單位)。</span><span class="sxs-lookup"><span data-stu-id="64d00-134">The size of the blob in bytes.</span></span> <span data-ttu-id="64d00-135">僅限匯出作業。</span><span class="sxs-lookup"><span data-stu-id="64d00-135">For export jobs only.</span></span>|  
|`Content-Type`|<span data-ttu-id="64d00-136">String</span><span class="sxs-lookup"><span data-stu-id="64d00-136">String</span></span>|<span data-ttu-id="64d00-137">選用。</span><span class="sxs-lookup"><span data-stu-id="64d00-137">Optional.</span></span> <span data-ttu-id="64d00-138">Blob 的內容類型。</span><span class="sxs-lookup"><span data-stu-id="64d00-138">The content type of the blob.</span></span>|  
|`Content-MD5`|<span data-ttu-id="64d00-139">String</span><span class="sxs-lookup"><span data-stu-id="64d00-139">String</span></span>|<span data-ttu-id="64d00-140">選用。</span><span class="sxs-lookup"><span data-stu-id="64d00-140">Optional.</span></span> <span data-ttu-id="64d00-141">Blob 的 MD5 雜湊。</span><span class="sxs-lookup"><span data-stu-id="64d00-141">The blob's MD5 hash.</span></span>|  
|`Content-Encoding`|<span data-ttu-id="64d00-142">String</span><span class="sxs-lookup"><span data-stu-id="64d00-142">String</span></span>|<span data-ttu-id="64d00-143">選用。</span><span class="sxs-lookup"><span data-stu-id="64d00-143">Optional.</span></span> <span data-ttu-id="64d00-144">Blob 的內容編碼。</span><span class="sxs-lookup"><span data-stu-id="64d00-144">The blob's content encoding.</span></span>|  
|`Content-Language`|<span data-ttu-id="64d00-145">String</span><span class="sxs-lookup"><span data-stu-id="64d00-145">String</span></span>|<span data-ttu-id="64d00-146">選用。</span><span class="sxs-lookup"><span data-stu-id="64d00-146">Optional.</span></span> <span data-ttu-id="64d00-147">Blob 的內容語言。</span><span class="sxs-lookup"><span data-stu-id="64d00-147">The blob's content language.</span></span>|  
|`Cache-Control`|<span data-ttu-id="64d00-148">String</span><span class="sxs-lookup"><span data-stu-id="64d00-148">String</span></span>|<span data-ttu-id="64d00-149">選用。</span><span class="sxs-lookup"><span data-stu-id="64d00-149">Optional.</span></span> <span data-ttu-id="64d00-150">Blob 的快取控制字串。</span><span class="sxs-lookup"><span data-stu-id="64d00-150">The cache control string for the blob.</span></span>|  

## <a name="next-steps"></a><span data-ttu-id="64d00-151">後續步驟</span><span class="sxs-lookup"><span data-stu-id="64d00-151">Next steps</span></span>

<span data-ttu-id="64d00-152">如需有關設定 blob 中繼資料和屬性的詳細規則，請參閱[設定 Blob 屬性](/rest/api/storageservices/set-blob-properties)、[設定 Blob 中繼資料](/rest/api/storageservices/set-blob-metadata)和[設定及擷取 Blob 資源的屬性和中繼資料](/rest/api/storageservices/setting-and-retrieving-properties-and-metadata-for-blob-resources)。</span><span class="sxs-lookup"><span data-stu-id="64d00-152">See [Set blob properties](/rest/api/storageservices/set-blob-properties), [Set Blob Metadata](/rest/api/storageservices/set-blob-metadata), and [Setting and retrieving properties and metadata for blob resources](/rest/api/storageservices/setting-and-retrieving-properties-and-metadata-for-blob-resources) for detailed rules about setting blob metadata and properties.</span></span>
