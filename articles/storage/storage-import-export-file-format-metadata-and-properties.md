---
title: "aaaAzure 匯入/匯出中繼資料和屬性檔案格式 |Microsoft 文件"
description: "深入了解如何 toospecify 中繼資料和屬性的一或多個 blob 的一部分匯入或匯出工作。"
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
ms.openlocfilehash: bb13c1f1a27baea77298cb224970cd521d02d8c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-importexport-service-metadata-and-properties-file-format"></a><span data-ttu-id="b66e5-103">Azure 匯入/匯出服務中繼資料和屬性檔案格式</span><span class="sxs-lookup"><span data-stu-id="b66e5-103">Azure Import/Export service metadata and properties file format</span></span>
<span data-ttu-id="b66e5-104">您可以針對匯入或匯出作業中的一或多個 blob 指定中繼資料和屬性。</span><span class="sxs-lookup"><span data-stu-id="b66e5-104">You can specify metadata and properties for one or more blobs as part of an import job or an export job.</span></span> <span data-ttu-id="b66e5-105">tooset 中繼資料或屬性建立為匯入工作一部分的 blob，您會提供包含匯入的 hello 資料 toobe hello 硬碟機上的中繼資料或屬性檔案。</span><span class="sxs-lookup"><span data-stu-id="b66e5-105">tooset metadata or properties for blobs being created as part of an import job, you provide a metadata or properties file on hello hard drive containing hello data toobe imported.</span></span> <span data-ttu-id="b66e5-106">匯出工作，中繼資料和屬性會傳回 tooyou hello 硬碟機上寫入所包含的 tooa 中繼資料或屬性檔案。</span><span class="sxs-lookup"><span data-stu-id="b66e5-106">For an export job, metadata and properties are written tooa metadata or properties file that is included on hello hard drive returned tooyou.</span></span>  
  
## <a name="metadata-file-format"></a><span data-ttu-id="b66e5-107">中繼資料檔案格式</span><span class="sxs-lookup"><span data-stu-id="b66e5-107">Metadata file format</span></span>  
<span data-ttu-id="b66e5-108">hello 的中繼資料檔案的格式如下所示：</span><span class="sxs-lookup"><span data-stu-id="b66e5-108">hello format of a metadata file is as follows:</span></span>  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<Metadata>  
[<metadata-name-1>metadata-value-1</metadata-name-1>]  
[<metadata-name-2>metadata-value-2</metadata-name-2>]  
. . .  
</Metadata>  
```
  
|<span data-ttu-id="b66e5-109">XML 元素</span><span class="sxs-lookup"><span data-stu-id="b66e5-109">XML Element</span></span>|<span data-ttu-id="b66e5-110">類型</span><span class="sxs-lookup"><span data-stu-id="b66e5-110">Type</span></span>|<span data-ttu-id="b66e5-111">說明</span><span class="sxs-lookup"><span data-stu-id="b66e5-111">Description</span></span>|  
|-----------------|----------|-----------------|  
|`Metadata`|<span data-ttu-id="b66e5-112">根元素</span><span class="sxs-lookup"><span data-stu-id="b66e5-112">Root element</span></span>|<span data-ttu-id="b66e5-113">hello hello 中繼資料檔案的根項目。</span><span class="sxs-lookup"><span data-stu-id="b66e5-113">hello root element of hello metadata file.</span></span>|  
|`metadata-name`|<span data-ttu-id="b66e5-114">String</span><span class="sxs-lookup"><span data-stu-id="b66e5-114">String</span></span>|<span data-ttu-id="b66e5-115">選用。</span><span class="sxs-lookup"><span data-stu-id="b66e5-115">Optional.</span></span> <span data-ttu-id="b66e5-116">hello XML 項目指定 hello 名稱 hello blob hello 中繼資料，其值會指定 hello hello 中繼資料設定值。</span><span class="sxs-lookup"><span data-stu-id="b66e5-116">hello XML element specifies hello name of hello metadata for hello blob, and its value specifies hello value of hello metadata setting.</span></span>|  
  
## <a name="properties-file-format"></a><span data-ttu-id="b66e5-117">屬性檔案格式</span><span class="sxs-lookup"><span data-stu-id="b66e5-117">Properties file format</span></span>  
<span data-ttu-id="b66e5-118">hello 屬性檔的格式如下所示：</span><span class="sxs-lookup"><span data-stu-id="b66e5-118">hello format of a properties file is as follows:</span></span>  
  
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
  
|<span data-ttu-id="b66e5-119">XML 元素</span><span class="sxs-lookup"><span data-stu-id="b66e5-119">XML Element</span></span>|<span data-ttu-id="b66e5-120">類型</span><span class="sxs-lookup"><span data-stu-id="b66e5-120">Type</span></span>|<span data-ttu-id="b66e5-121">說明</span><span class="sxs-lookup"><span data-stu-id="b66e5-121">Description</span></span>|  
|-----------------|----------|-----------------|  
|`Properties`|<span data-ttu-id="b66e5-122">根元素</span><span class="sxs-lookup"><span data-stu-id="b66e5-122">Root element</span></span>|<span data-ttu-id="b66e5-123">hello hello 屬性檔的根項目。</span><span class="sxs-lookup"><span data-stu-id="b66e5-123">hello root element of hello properties file.</span></span>|  
|`Last-Modified`|<span data-ttu-id="b66e5-124">String</span><span class="sxs-lookup"><span data-stu-id="b66e5-124">String</span></span>|<span data-ttu-id="b66e5-125">選用。</span><span class="sxs-lookup"><span data-stu-id="b66e5-125">Optional.</span></span> <span data-ttu-id="b66e5-126">hello 上次修改時間 hello blob。</span><span class="sxs-lookup"><span data-stu-id="b66e5-126">hello last-modified time for hello blob.</span></span> <span data-ttu-id="b66e5-127">僅限匯出作業。</span><span class="sxs-lookup"><span data-stu-id="b66e5-127">For export jobs only.</span></span>|  
|`Etag`|<span data-ttu-id="b66e5-128">String</span><span class="sxs-lookup"><span data-stu-id="b66e5-128">String</span></span>|<span data-ttu-id="b66e5-129">選用。</span><span class="sxs-lookup"><span data-stu-id="b66e5-129">Optional.</span></span> <span data-ttu-id="b66e5-130">hello blob 的 ETag 值。</span><span class="sxs-lookup"><span data-stu-id="b66e5-130">hello blob's ETag value.</span></span> <span data-ttu-id="b66e5-131">僅限匯出作業。</span><span class="sxs-lookup"><span data-stu-id="b66e5-131">For export jobs only.</span></span>|  
|`Content-Length`|<span data-ttu-id="b66e5-132">String</span><span class="sxs-lookup"><span data-stu-id="b66e5-132">String</span></span>|<span data-ttu-id="b66e5-133">選用。</span><span class="sxs-lookup"><span data-stu-id="b66e5-133">Optional.</span></span> <span data-ttu-id="b66e5-134">hello 的 hello blob 以位元組為單位的大小。</span><span class="sxs-lookup"><span data-stu-id="b66e5-134">hello size of hello blob in bytes.</span></span> <span data-ttu-id="b66e5-135">僅限匯出作業。</span><span class="sxs-lookup"><span data-stu-id="b66e5-135">For export jobs only.</span></span>|  
|`Content-Type`|<span data-ttu-id="b66e5-136">String</span><span class="sxs-lookup"><span data-stu-id="b66e5-136">String</span></span>|<span data-ttu-id="b66e5-137">選用。</span><span class="sxs-lookup"><span data-stu-id="b66e5-137">Optional.</span></span> <span data-ttu-id="b66e5-138">hello hello blob 的內容型別。</span><span class="sxs-lookup"><span data-stu-id="b66e5-138">hello content type of hello blob.</span></span>|  
|`Content-MD5`|<span data-ttu-id="b66e5-139">String</span><span class="sxs-lookup"><span data-stu-id="b66e5-139">String</span></span>|<span data-ttu-id="b66e5-140">選用。</span><span class="sxs-lookup"><span data-stu-id="b66e5-140">Optional.</span></span> <span data-ttu-id="b66e5-141">hello blob 的 MD5 雜湊。</span><span class="sxs-lookup"><span data-stu-id="b66e5-141">hello blob's MD5 hash.</span></span>|  
|`Content-Encoding`|<span data-ttu-id="b66e5-142">String</span><span class="sxs-lookup"><span data-stu-id="b66e5-142">String</span></span>|<span data-ttu-id="b66e5-143">選用。</span><span class="sxs-lookup"><span data-stu-id="b66e5-143">Optional.</span></span> <span data-ttu-id="b66e5-144">hello blob 的內容編碼方式。</span><span class="sxs-lookup"><span data-stu-id="b66e5-144">hello blob's content encoding.</span></span>|  
|`Content-Language`|<span data-ttu-id="b66e5-145">String</span><span class="sxs-lookup"><span data-stu-id="b66e5-145">String</span></span>|<span data-ttu-id="b66e5-146">選用。</span><span class="sxs-lookup"><span data-stu-id="b66e5-146">Optional.</span></span> <span data-ttu-id="b66e5-147">hello blob 的內容語言。</span><span class="sxs-lookup"><span data-stu-id="b66e5-147">hello blob's content language.</span></span>|  
|`Cache-Control`|<span data-ttu-id="b66e5-148">String</span><span class="sxs-lookup"><span data-stu-id="b66e5-148">String</span></span>|<span data-ttu-id="b66e5-149">選用。</span><span class="sxs-lookup"><span data-stu-id="b66e5-149">Optional.</span></span> <span data-ttu-id="b66e5-150">hello blob 的快取控制字串 hello。</span><span class="sxs-lookup"><span data-stu-id="b66e5-150">hello cache control string for hello blob.</span></span>|  

## <a name="next-steps"></a><span data-ttu-id="b66e5-151">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b66e5-151">Next steps</span></span>

<span data-ttu-id="b66e5-152">如需有關設定 blob 中繼資料和屬性的詳細規則，請參閱[設定 Blob 屬性](/rest/api/storageservices/set-blob-properties)、[設定 Blob 中繼資料](/rest/api/storageservices/set-blob-metadata)和[設定及擷取 Blob 資源的屬性和中繼資料](/rest/api/storageservices/setting-and-retrieving-properties-and-metadata-for-blob-resources)。</span><span class="sxs-lookup"><span data-stu-id="b66e5-152">See [Set blob properties](/rest/api/storageservices/set-blob-properties), [Set Blob Metadata](/rest/api/storageservices/set-blob-metadata), and [Setting and retrieving properties and metadata for blob resources](/rest/api/storageservices/setting-and-retrieving-properties-and-metadata-for-blob-resources) for detailed rules about setting blob metadata and properties.</span></span>
