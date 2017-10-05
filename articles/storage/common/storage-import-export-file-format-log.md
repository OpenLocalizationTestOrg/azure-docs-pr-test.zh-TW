---
title: "Azure 匯入/匯出記錄檔格式 | Microsoft Docs"
description: "了解執行匯入/匯出服務作業的步驟時所建立的記錄檔格式。"
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 38cc16bd-ad55-4625-9a85-e1726c35fd1b
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: 16234ccaf13ce1d85cfd207ed4734e683070faa6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="azure-importexport-service-log-file-format"></a><span data-ttu-id="aa9de-103">Azure 匯入/匯出服務記錄檔格式</span><span class="sxs-lookup"><span data-stu-id="aa9de-103">Azure Import/Export service log file format</span></span>
<span data-ttu-id="aa9de-104">當 Microsoft Azure 匯入/匯出服務於匯入工作或匯出工作期間在磁碟機上執行動作時，記錄檔會寫入至與該工作相關聯的儲存體帳戶中的區塊 Blob。</span><span class="sxs-lookup"><span data-stu-id="aa9de-104">When the Microsoft Azure Import/Export service performs an action on a drive as part of an import job or an export job, logs are written to block blobs in the storage account associated with that job.</span></span>  
  
<span data-ttu-id="aa9de-105">匯入/匯出服務可覆寫兩個記錄檔︰</span><span class="sxs-lookup"><span data-stu-id="aa9de-105">There are two logs that may be written by the Import/Export service:</span></span>  
  
-   <span data-ttu-id="aa9de-106">發生錯誤時，一定會產生錯誤記錄檔。</span><span class="sxs-lookup"><span data-stu-id="aa9de-106">The error log is always generated in the event of an error.</span></span>  
  
-   <span data-ttu-id="aa9de-107">詳細資訊記錄檔預設未啟用，但可透過在 [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) 或 [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) 作業上設定 `EnableVerboseLog` 屬性來啟用。</span><span class="sxs-lookup"><span data-stu-id="aa9de-107">The verbose log is not enabled by default, but may be enabled by setting the `EnableVerboseLog` property on a [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) or [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) operation.</span></span>  
  
## <a name="log-file-location"></a><span data-ttu-id="aa9de-108">記錄檔位置</span><span class="sxs-lookup"><span data-stu-id="aa9de-108">Log file location</span></span>  
<span data-ttu-id="aa9de-109">記錄檔會寫入至容器中的區塊 Blob 或 `ImportExportStatesPath` 設定指定的虛擬目錄 (您可以在 `Put Job` 作業上設定) 中。</span><span class="sxs-lookup"><span data-stu-id="aa9de-109">The logs are written to block blobs in the container or virtual directory specified by the `ImportExportStatesPath` setting, which you can set on a `Put Job` operation.</span></span> <span data-ttu-id="aa9de-110">寫入記錄檔的位置取決於為工作指定的驗證方式，以及為 `ImportExportStatesPath` 指定的值。</span><span class="sxs-lookup"><span data-stu-id="aa9de-110">The location to which the logs are written depends on how authentication is specified for the job, together with the value specified for `ImportExportStatesPath`.</span></span> <span data-ttu-id="aa9de-111">您可以透過儲存體帳戶金鑰或容器 SAS (共用存取簽章) 指定工作的驗證方式。</span><span class="sxs-lookup"><span data-stu-id="aa9de-111">Authentication for the job may be specified via a storage account key, or a container SAS (shared access signature).</span></span>  
  
<span data-ttu-id="aa9de-112">容器或虛擬目錄的名稱可以是 `waimportexport` 的預設名稱，或是您指定的其他容器或虛擬目錄名稱。</span><span class="sxs-lookup"><span data-stu-id="aa9de-112">The name of the container or virtual directory may either be the default name of `waimportexport`, or another container or virtual directory name that you specify.</span></span>  
  
<span data-ttu-id="aa9de-113">下表顯示可能的選項︰</span><span class="sxs-lookup"><span data-stu-id="aa9de-113">The table below shows the possible options:</span></span>  
  
|<span data-ttu-id="aa9de-114">驗證方法</span><span class="sxs-lookup"><span data-stu-id="aa9de-114">Authentication Method</span></span>|<span data-ttu-id="aa9de-115">`ImportExportStatesPath` 元素的值</span><span class="sxs-lookup"><span data-stu-id="aa9de-115">Value of `ImportExportStatesPath`Element</span></span>|<span data-ttu-id="aa9de-116">記錄檔 Blob 的位置</span><span class="sxs-lookup"><span data-stu-id="aa9de-116">Location of Log Blobs</span></span>|  
|---------------------------|----------------------------------------------|---------------------------|  
|<span data-ttu-id="aa9de-117">儲存體帳戶金鑰</span><span class="sxs-lookup"><span data-stu-id="aa9de-117">Storage account key</span></span>|<span data-ttu-id="aa9de-118">預設值</span><span class="sxs-lookup"><span data-stu-id="aa9de-118">Default value</span></span>|<span data-ttu-id="aa9de-119">名為 `waimportexport` 的容器，這是預設容器。</span><span class="sxs-lookup"><span data-stu-id="aa9de-119">A container named `waimportexport`, which is the default container.</span></span> <span data-ttu-id="aa9de-120">例如：</span><span class="sxs-lookup"><span data-stu-id="aa9de-120">For example:</span></span><br /><br /> `https://myaccount.blob.core.windows.net/waimportexport`|  
|<span data-ttu-id="aa9de-121">儲存體帳戶金鑰</span><span class="sxs-lookup"><span data-stu-id="aa9de-121">Storage account key</span></span>|<span data-ttu-id="aa9de-122">使用者指定值</span><span class="sxs-lookup"><span data-stu-id="aa9de-122">User-specified value</span></span>|<span data-ttu-id="aa9de-123">使用者命名的容器。</span><span class="sxs-lookup"><span data-stu-id="aa9de-123">A container named by the user.</span></span> <span data-ttu-id="aa9de-124">例如：</span><span class="sxs-lookup"><span data-stu-id="aa9de-124">For example:</span></span><br /><br /> `https://myaccount.blob.core.windows.net/mylogcontainer`|  
|<span data-ttu-id="aa9de-125">容器 SAS</span><span class="sxs-lookup"><span data-stu-id="aa9de-125">Container SAS</span></span>|<span data-ttu-id="aa9de-126">預設值</span><span class="sxs-lookup"><span data-stu-id="aa9de-126">Default value</span></span>|<span data-ttu-id="aa9de-127">名為 `waimportexport` 的虛擬目錄，這是預設名稱，位於 SAS 中指定的容器底下。</span><span class="sxs-lookup"><span data-stu-id="aa9de-127">A virtual directory named `waimportexport`, which is the default name, beneath the container specified in the SAS.</span></span><br /><br /> <span data-ttu-id="aa9de-128">例如，如果為工作指定的 SAS 是 `https://myaccount.blob.core.windows.net/mylogcontainer?sv=2012-02-12&se=2015-05-22T06%3A54%3A55Z&sr=c&sp=wl&sig=sigvalue`，記錄檔位置會是 `https://myaccount.blob.core.windows.net/mylogcontainer/waimportexport`</span><span class="sxs-lookup"><span data-stu-id="aa9de-128">For example, if the SAS specified for the job is  `https://myaccount.blob.core.windows.net/mylogcontainer?sv=2012-02-12&se=2015-05-22T06%3A54%3A55Z&sr=c&sp=wl&sig=sigvalue`, then the log location would be `https://myaccount.blob.core.windows.net/mylogcontainer/waimportexport`</span></span>|  
|<span data-ttu-id="aa9de-129">容器 SAS</span><span class="sxs-lookup"><span data-stu-id="aa9de-129">Container SAS</span></span>|<span data-ttu-id="aa9de-130">使用者指定值</span><span class="sxs-lookup"><span data-stu-id="aa9de-130">User-specified value</span></span>|<span data-ttu-id="aa9de-131">使用者命名的虛擬目錄，位於 SAS 中指定的容器底下。</span><span class="sxs-lookup"><span data-stu-id="aa9de-131">A virtual directory named by the user, beneath the container specified in the SAS.</span></span><br /><br /> <span data-ttu-id="aa9de-132">例如，如果為工作指定的 SAS 是 `https://myaccount.blob.core.windows.net/mylogcontainer?sv=2012-02-12&se=2015-05-22T06%3A54%3A55Z&sr=c&sp=wl&sig=sigvalue`，且指定的虛擬目錄名為 `mylogblobs`，記錄檔位置會是 `https://myaccount.blob.core.windows.net/mylogcontainer/waimportexport/mylogblobs`。</span><span class="sxs-lookup"><span data-stu-id="aa9de-132">For example, if the SAS specified for the job is  `https://myaccount.blob.core.windows.net/mylogcontainer?sv=2012-02-12&se=2015-05-22T06%3A54%3A55Z&sr=c&sp=wl&sig=sigvalue`, and the specified virtual directory is named `mylogblobs`, then the log location would be `https://myaccount.blob.core.windows.net/mylogcontainer/waimportexport/mylogblobs`.</span></span>|  
  
<span data-ttu-id="aa9de-133">您可以透過呼叫 [Get Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) 作業來擷取錯誤和詳細資訊記錄檔的 URL。</span><span class="sxs-lookup"><span data-stu-id="aa9de-133">You can retrieve the URL for the error and verbose logs by calling the [Get Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operation.</span></span> <span data-ttu-id="aa9de-134">磁碟機處理完成後會產生記錄檔。</span><span class="sxs-lookup"><span data-stu-id="aa9de-134">The logs are available after processing of the drive is complete.</span></span>  
  
## <a name="log-file-format"></a><span data-ttu-id="aa9de-135">記錄檔格式</span><span class="sxs-lookup"><span data-stu-id="aa9de-135">Log file format</span></span>  
<span data-ttu-id="aa9de-136">兩個記錄檔的格式同為 Blob，其中包含在硬碟和客戶的帳戶之間複製 Blob 時所發生事件的 XML 描述。</span><span class="sxs-lookup"><span data-stu-id="aa9de-136">The format for both logs is the same: a blob containing XML descriptions of the events that occurred while copying blobs between the hard drive and the customer's account.</span></span>  
  
<span data-ttu-id="aa9de-137">詳細資訊記錄檔包含與每個 Blob (匯入工作) 或檔案 (匯出工作) 的複製作業狀態相關的完整資訊，錯誤記錄檔則只包含匯入或匯出工作期間發生錯誤的 Blob 或檔案的資訊。</span><span class="sxs-lookup"><span data-stu-id="aa9de-137">The verbose log contains complete information about the status of the copy operation for every blob (for an import job) or file (for an export job), whereas the error log contains only the information for blobs or files that encountered errors during the import or export job.</span></span>  
  
<span data-ttu-id="aa9de-138">詳細資訊記錄檔格式顯示如下。</span><span class="sxs-lookup"><span data-stu-id="aa9de-138">The verbose log format is shown below.</span></span> <span data-ttu-id="aa9de-139">錯誤記錄檔的結構相同，但會篩選出成功的作業。</span><span class="sxs-lookup"><span data-stu-id="aa9de-139">The error log has the same structure, but filters out successful operations.</span></span>  

```xml
<DriveLog Version="2014-11-01">  
  <DriveId>drive-id</DriveId>  
  [<Blob Status="blob-status">  
   <BlobPath>blob-path</BlobPath>  
   <FilePath>file-path</FilePath>  
   [<Snapshot>snapshot</Snapshot>]  
   <Length>length</Length>  
   [<LastModified>last-modified</LastModified>]  
   [<ImportDisposition Status="import-disposition-status">import-disposition</ImportDisposition>]  
   [page-range-list-or-block-list]  
   [metadata-status]  
   [properties-status]  
  </Blob>]  
  [<Blob>  
    . . .  
  </Blob>]  
  <Status>drive-status</Status>  
</DriveLog>  
  
page-range-list-or-block-list ::= 
  page-range-list | block-list  
  
page-range-list ::=   
<PageRangeList>  
      [<PageRange Offset="page-range-offset" Length="page-range-length"   
       [Hash="md5-hash"] Status="page-range-status"/>]  
      [<PageRange Offset="page-range-offset" Length="page-range-length"   
       [Hash="md5-hash"] Status="page-range-status"/>]  
</PageRangeList>  
  
block-list ::=  
<BlockList>  
      [<Block Offset="block-offset" Length="block-length" [Id="block-id"]  
       [Hash="md5-hash"] Status="block-status"/>]  
      [<Block Offset="block-offset" Length="block-length" [Id="block-id"]   
       [Hash="md5-hash"] Status="block-status"/>]  
</BlockList>  
  
metadata-status ::=  
<Metadata Status="metadata-status">  
   [<GlobalPath Hash="md5-hash">global-metadata-file-path</GlobalPath>]  
   [<Path Hash="md5-hash">metadata-file-path</Path>]  
</Metadata>  
  
properties-status ::=  
<Properties Status="properties-status">  
   [<GlobalPath Hash="md5-hash">global-properties-file-path</GlobalPath>]  
   [<Path Hash="md5-hash">properties-file-path</Path>]  
</Properties>  
```

<span data-ttu-id="aa9de-140">下表說明記錄檔的元素：</span><span class="sxs-lookup"><span data-stu-id="aa9de-140">The following table describes the elements of the log file.</span></span>  
  
|<span data-ttu-id="aa9de-141">XML 元素</span><span class="sxs-lookup"><span data-stu-id="aa9de-141">XML Element</span></span>|<span data-ttu-id="aa9de-142">類型</span><span class="sxs-lookup"><span data-stu-id="aa9de-142">Type</span></span>|<span data-ttu-id="aa9de-143">說明</span><span class="sxs-lookup"><span data-stu-id="aa9de-143">Description</span></span>|  
|-----------------|----------|-----------------|  
|`DriveLog`|<span data-ttu-id="aa9de-144">XML 元素</span><span class="sxs-lookup"><span data-stu-id="aa9de-144">XML Element</span></span>|<span data-ttu-id="aa9de-145">代表磁碟機記錄檔。</span><span class="sxs-lookup"><span data-stu-id="aa9de-145">Represents a drive log.</span></span>|  
|`Version`|<span data-ttu-id="aa9de-146">屬性、字串</span><span class="sxs-lookup"><span data-stu-id="aa9de-146">Attribute, String</span></span>|<span data-ttu-id="aa9de-147">記錄檔格式的版本。</span><span class="sxs-lookup"><span data-stu-id="aa9de-147">The version of the log format.</span></span>|  
|`DriveId`|<span data-ttu-id="aa9de-148">String</span><span class="sxs-lookup"><span data-stu-id="aa9de-148">String</span></span>|<span data-ttu-id="aa9de-149">磁碟機的硬體序號。</span><span class="sxs-lookup"><span data-stu-id="aa9de-149">The drive's hardware serial number.</span></span>|  
|`Status`|<span data-ttu-id="aa9de-150">String</span><span class="sxs-lookup"><span data-stu-id="aa9de-150">String</span></span>|<span data-ttu-id="aa9de-151">磁碟機處理狀態。</span><span class="sxs-lookup"><span data-stu-id="aa9de-151">Status of the drive processing.</span></span> <span data-ttu-id="aa9de-152">如需詳細資訊，請參閱以下的 `Drive Status Codes` 表格。</span><span class="sxs-lookup"><span data-stu-id="aa9de-152">See the `Drive Status Codes` table below for more information.</span></span>|  
|`Blob`|<span data-ttu-id="aa9de-153">巢狀的 XML 元素</span><span class="sxs-lookup"><span data-stu-id="aa9de-153">Nested XML element</span></span>|<span data-ttu-id="aa9de-154">代表 Blob。</span><span class="sxs-lookup"><span data-stu-id="aa9de-154">Represents a blob.</span></span>|  
|`Blob/BlobPath`|<span data-ttu-id="aa9de-155">String</span><span class="sxs-lookup"><span data-stu-id="aa9de-155">String</span></span>|<span data-ttu-id="aa9de-156">Blob 的 URI。</span><span class="sxs-lookup"><span data-stu-id="aa9de-156">The URI of the blob.</span></span>|  
|`Blob/FilePath`|<span data-ttu-id="aa9de-157">String</span><span class="sxs-lookup"><span data-stu-id="aa9de-157">String</span></span>|<span data-ttu-id="aa9de-158">磁碟機上檔案的相對路徑。</span><span class="sxs-lookup"><span data-stu-id="aa9de-158">The relative path to the file on the drive.</span></span>|  
|`Blob/Snapshot`|<span data-ttu-id="aa9de-159">DateTime</span><span class="sxs-lookup"><span data-stu-id="aa9de-159">DateTime</span></span>|<span data-ttu-id="aa9de-160">Blob 快照集版本 (限匯出工作)。</span><span class="sxs-lookup"><span data-stu-id="aa9de-160">The snapshot version of the blob, for an export job only.</span></span>|  
|`Blob/Length`|<span data-ttu-id="aa9de-161">Integer</span><span class="sxs-lookup"><span data-stu-id="aa9de-161">Integer</span></span>|<span data-ttu-id="aa9de-162">Blob 總長度 (以位元組為單位)。</span><span class="sxs-lookup"><span data-stu-id="aa9de-162">The total length of the blob in bytes.</span></span>|  
|`Blob/LastModified`|<span data-ttu-id="aa9de-163">DateTime</span><span class="sxs-lookup"><span data-stu-id="aa9de-163">DateTime</span></span>|<span data-ttu-id="aa9de-164">上次修改 Blob 的日期/時間 (限匯出工作)。</span><span class="sxs-lookup"><span data-stu-id="aa9de-164">The date/time that the blob was last modified, for an export job only.</span></span>|  
|`Blob/ImportDisposition`|<span data-ttu-id="aa9de-165">String</span><span class="sxs-lookup"><span data-stu-id="aa9de-165">String</span></span>|<span data-ttu-id="aa9de-166">Blob 的匯入配置 (限匯入工作)。</span><span class="sxs-lookup"><span data-stu-id="aa9de-166">The import disposition of the blob, for an import job only.</span></span>|  
|`Blob/ImportDisposition/@Status`|<span data-ttu-id="aa9de-167">屬性、字串</span><span class="sxs-lookup"><span data-stu-id="aa9de-167">Attribute, String</span></span>|<span data-ttu-id="aa9de-168">匯入配置狀態。</span><span class="sxs-lookup"><span data-stu-id="aa9de-168">The status of the import disposition.</span></span>|  
|`PageRangeList`|<span data-ttu-id="aa9de-169">巢狀的 XML 元素</span><span class="sxs-lookup"><span data-stu-id="aa9de-169">Nested XML element</span></span>|<span data-ttu-id="aa9de-170">代表分頁 Blob 的頁面範圍清單。</span><span class="sxs-lookup"><span data-stu-id="aa9de-170">Represents a list of page ranges for a page blob.</span></span>|  
|`PageRange`|<span data-ttu-id="aa9de-171">XML 元素</span><span class="sxs-lookup"><span data-stu-id="aa9de-171">XML element</span></span>|<span data-ttu-id="aa9de-172">代表頁面範圍。</span><span class="sxs-lookup"><span data-stu-id="aa9de-172">Represents a page range.</span></span>|  
|`PageRange/@Offset`|<span data-ttu-id="aa9de-173">屬性、整數</span><span class="sxs-lookup"><span data-stu-id="aa9de-173">Attribute, Integer</span></span>|<span data-ttu-id="aa9de-174">Blob 中的頁面範圍起始位移。</span><span class="sxs-lookup"><span data-stu-id="aa9de-174">Starting offset of the page range in the blob.</span></span>|  
|`PageRange/@Length`|<span data-ttu-id="aa9de-175">屬性、整數</span><span class="sxs-lookup"><span data-stu-id="aa9de-175">Attribute, Integer</span></span>|<span data-ttu-id="aa9de-176">頁面範圍的長度 (以位元組為單位)。</span><span class="sxs-lookup"><span data-stu-id="aa9de-176">Length in bytes of the page range.</span></span>|  
|`PageRange/@Hash`|<span data-ttu-id="aa9de-177">屬性、字串</span><span class="sxs-lookup"><span data-stu-id="aa9de-177">Attribute, String</span></span>|<span data-ttu-id="aa9de-178">頁面範圍的 Base16 式編碼的 MD5 雜湊。</span><span class="sxs-lookup"><span data-stu-id="aa9de-178">Base16-encoded MD5 hash of the page range.</span></span>|  
|`PageRange/@Status`|<span data-ttu-id="aa9de-179">屬性、字串</span><span class="sxs-lookup"><span data-stu-id="aa9de-179">Attribute, String</span></span>|<span data-ttu-id="aa9de-180">頁面範圍處理狀態。</span><span class="sxs-lookup"><span data-stu-id="aa9de-180">Status of processing the page range.</span></span>|  
|`BlockList`|<span data-ttu-id="aa9de-181">巢狀的 XML 元素</span><span class="sxs-lookup"><span data-stu-id="aa9de-181">Nested XML element</span></span>|<span data-ttu-id="aa9de-182">代表區塊 Blob 的區塊清單。</span><span class="sxs-lookup"><span data-stu-id="aa9de-182">Represents a list of blocks for a block blob.</span></span>|  
|`Block`|<span data-ttu-id="aa9de-183">XML 元素</span><span class="sxs-lookup"><span data-stu-id="aa9de-183">XML element</span></span>|<span data-ttu-id="aa9de-184">代表區塊。</span><span class="sxs-lookup"><span data-stu-id="aa9de-184">Represents a block.</span></span>|  
|`Block/@Offset`|<span data-ttu-id="aa9de-185">屬性、整數</span><span class="sxs-lookup"><span data-stu-id="aa9de-185">Attribute, Integer</span></span>|<span data-ttu-id="aa9de-186">Blob 中的區塊起始位移。</span><span class="sxs-lookup"><span data-stu-id="aa9de-186">Starting offset of the block in the blob.</span></span>|  
|`Block/@Length`|<span data-ttu-id="aa9de-187">屬性、整數</span><span class="sxs-lookup"><span data-stu-id="aa9de-187">Attribute, Integer</span></span>|<span data-ttu-id="aa9de-188">區塊的長度 (以位元組為單位)。</span><span class="sxs-lookup"><span data-stu-id="aa9de-188">Length in bytes of the block.</span></span>|  
|`Block/@Id`|<span data-ttu-id="aa9de-189">屬性、字串</span><span class="sxs-lookup"><span data-stu-id="aa9de-189">Attribute, String</span></span>|<span data-ttu-id="aa9de-190">區塊識別碼。</span><span class="sxs-lookup"><span data-stu-id="aa9de-190">The block ID.</span></span>|  
|`Block/@Hash`|<span data-ttu-id="aa9de-191">屬性、字串</span><span class="sxs-lookup"><span data-stu-id="aa9de-191">Attribute, String</span></span>|<span data-ttu-id="aa9de-192">區塊的 Base16 式編碼的 MD5 雜湊。</span><span class="sxs-lookup"><span data-stu-id="aa9de-192">Base16-encoded MD5 hash of the block.</span></span>|  
|`Block/@Status`|<span data-ttu-id="aa9de-193">屬性、字串</span><span class="sxs-lookup"><span data-stu-id="aa9de-193">Attribute, String</span></span>|<span data-ttu-id="aa9de-194">區塊處理狀態。</span><span class="sxs-lookup"><span data-stu-id="aa9de-194">Status of processing the block.</span></span>|  
|`Metadata`|<span data-ttu-id="aa9de-195">巢狀的 XML 元素</span><span class="sxs-lookup"><span data-stu-id="aa9de-195">Nested XML element</span></span>|<span data-ttu-id="aa9de-196">代表 Blob 的中繼資料。</span><span class="sxs-lookup"><span data-stu-id="aa9de-196">Represents the blob's metadata.</span></span>|  
|`Metadata/@Status`|<span data-ttu-id="aa9de-197">屬性、字串</span><span class="sxs-lookup"><span data-stu-id="aa9de-197">Attribute, String</span></span>|<span data-ttu-id="aa9de-198">Blob 中繼資料處理狀態。</span><span class="sxs-lookup"><span data-stu-id="aa9de-198">Status of processing of the blob metadata.</span></span>|  
|`Metadata/GlobalPath`|<span data-ttu-id="aa9de-199">String</span><span class="sxs-lookup"><span data-stu-id="aa9de-199">String</span></span>|<span data-ttu-id="aa9de-200">全域中繼資料檔案的相對路徑。</span><span class="sxs-lookup"><span data-stu-id="aa9de-200">Relative path to the global metadata file.</span></span>|  
|`Metadata/GlobalPath/@Hash`|<span data-ttu-id="aa9de-201">屬性、字串</span><span class="sxs-lookup"><span data-stu-id="aa9de-201">Attribute, String</span></span>|<span data-ttu-id="aa9de-202">全域中繼資料檔案的 Base16 式編碼的 MD5 雜湊。</span><span class="sxs-lookup"><span data-stu-id="aa9de-202">Base16-encoded MD5 hash of the global metadata file.</span></span>|  
|`Metadata/Path`|<span data-ttu-id="aa9de-203">String</span><span class="sxs-lookup"><span data-stu-id="aa9de-203">String</span></span>|<span data-ttu-id="aa9de-204">中繼資料檔案的相對路徑。</span><span class="sxs-lookup"><span data-stu-id="aa9de-204">Relative path to the metadata file.</span></span>|  
|`Metadata/Path/@Hash`|<span data-ttu-id="aa9de-205">屬性、字串</span><span class="sxs-lookup"><span data-stu-id="aa9de-205">Attribute, String</span></span>|<span data-ttu-id="aa9de-206">中繼資料檔案的 Base16 式編碼的 MD5 雜湊。</span><span class="sxs-lookup"><span data-stu-id="aa9de-206">Base16-encoded MD5 hash of the metadata file.</span></span>|  
|`Properties`|<span data-ttu-id="aa9de-207">巢狀的 XML 元素</span><span class="sxs-lookup"><span data-stu-id="aa9de-207">Nested XML element</span></span>|<span data-ttu-id="aa9de-208">表示 Blob 屬性。</span><span class="sxs-lookup"><span data-stu-id="aa9de-208">Represents the blob properties.</span></span>|  
|`Properties/@Status`|<span data-ttu-id="aa9de-209">屬性、字串</span><span class="sxs-lookup"><span data-stu-id="aa9de-209">Attribute, String</span></span>|<span data-ttu-id="aa9de-210">Blob 屬性處理狀態，例如，找不到檔案、已完成。</span><span class="sxs-lookup"><span data-stu-id="aa9de-210">Status of processing the blob properties, e.g. file not found, completed.</span></span>|  
|`Properties/GlobalPath`|<span data-ttu-id="aa9de-211">String</span><span class="sxs-lookup"><span data-stu-id="aa9de-211">String</span></span>|<span data-ttu-id="aa9de-212">全域屬性檔案的相對路徑。</span><span class="sxs-lookup"><span data-stu-id="aa9de-212">Relative path to the global properties file.</span></span>|  
|`Properties/GlobalPath/@Hash`|<span data-ttu-id="aa9de-213">屬性、字串</span><span class="sxs-lookup"><span data-stu-id="aa9de-213">Attribute, String</span></span>|<span data-ttu-id="aa9de-214">全域屬性檔案的 Base16 式編碼的 MD5 雜湊。</span><span class="sxs-lookup"><span data-stu-id="aa9de-214">Base16-encoded MD5 hash of the global properties file.</span></span>|  
|`Properties/Path`|<span data-ttu-id="aa9de-215">String</span><span class="sxs-lookup"><span data-stu-id="aa9de-215">String</span></span>|<span data-ttu-id="aa9de-216">屬性檔案的相對路徑。</span><span class="sxs-lookup"><span data-stu-id="aa9de-216">Relative path to the properties file.</span></span>|  
|`Properties/Path/@Hash`|<span data-ttu-id="aa9de-217">屬性、字串</span><span class="sxs-lookup"><span data-stu-id="aa9de-217">Attribute, String</span></span>|<span data-ttu-id="aa9de-218">屬性檔案的 Base16 式編碼的 MD5 雜湊。</span><span class="sxs-lookup"><span data-stu-id="aa9de-218">Base16-encoded MD5 hash of the properties file.</span></span>|  
|`Blob/Status`|<span data-ttu-id="aa9de-219">String</span><span class="sxs-lookup"><span data-stu-id="aa9de-219">String</span></span>|<span data-ttu-id="aa9de-220">Blob 處理狀態。</span><span class="sxs-lookup"><span data-stu-id="aa9de-220">Status of processing the blob.</span></span>|  
  
# <a name="drive-status-codes"></a><span data-ttu-id="aa9de-221">磁碟機狀態碼</span><span class="sxs-lookup"><span data-stu-id="aa9de-221">Drive status codes</span></span>  
<span data-ttu-id="aa9de-222">下表列出磁碟機處理的狀態碼。</span><span class="sxs-lookup"><span data-stu-id="aa9de-222">The following table lists the status codes for processing a drive.</span></span>  
  
|<span data-ttu-id="aa9de-223">狀態碼</span><span class="sxs-lookup"><span data-stu-id="aa9de-223">Status code</span></span>|<span data-ttu-id="aa9de-224">說明</span><span class="sxs-lookup"><span data-stu-id="aa9de-224">Description</span></span>|  
|-----------------|-----------------|  
|`Completed`|<span data-ttu-id="aa9de-225">磁碟機已完成處理，沒有任何錯誤。</span><span class="sxs-lookup"><span data-stu-id="aa9de-225">The drive has finished processing without any errors.</span></span>|  
|`CompletedWithWarnings`|<span data-ttu-id="aa9de-226">磁碟機已完成處理，並根據為 Blob 指定的匯入配置在一或多個 Blob 中發出警告。</span><span class="sxs-lookup"><span data-stu-id="aa9de-226">The drive has finished processing with warnings in one or more blobs per the import dispositions specified for the blobs.</span></span>|  
|`CompletedWithErrors`|<span data-ttu-id="aa9de-227">磁碟機已完成，一或多個 Blob 或區塊中發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="aa9de-227">The drive has finished with errors in one or more blobs or chunks.</span></span>|  
|`DiskNotFound`|<span data-ttu-id="aa9de-228">在磁碟機上找不到磁碟。</span><span class="sxs-lookup"><span data-stu-id="aa9de-228">No disk is found on the drive.</span></span>|  
|`VolumeNotNtfs`|<span data-ttu-id="aa9de-229">磁碟上的第一個資料磁碟區不是 NTFS 格式。</span><span class="sxs-lookup"><span data-stu-id="aa9de-229">The first data volume on the disk is not in NTFS format.</span></span>|  
|`DiskOperationFailed`|<span data-ttu-id="aa9de-230">在磁碟機上執行作業時發生未知的失敗。</span><span class="sxs-lookup"><span data-stu-id="aa9de-230">An unknown failure occurred when performing operations on the drive.</span></span>|  
|`BitLockerVolumeNotFound`|<span data-ttu-id="aa9de-231">找不到 BitLocker 可加密磁碟區。</span><span class="sxs-lookup"><span data-stu-id="aa9de-231">No BitLocker encryptable volume is found.</span></span>|  
|`BitLockerNotActivated`|<span data-ttu-id="aa9de-232">磁碟區上未啟用 BitLocker。</span><span class="sxs-lookup"><span data-stu-id="aa9de-232">BitLocker is not enabled on the volume.</span></span>|  
|`BitLockerProtectorNotFound`|<span data-ttu-id="aa9de-233">數字密碼金鑰保護裝置不存在磁碟區上。</span><span class="sxs-lookup"><span data-stu-id="aa9de-233">The numerical password key protector does not exist on the volume.</span></span>|  
|`BitLockerKeyInvalid`|<span data-ttu-id="aa9de-234">提供的數字密碼無法解除鎖定磁碟區。</span><span class="sxs-lookup"><span data-stu-id="aa9de-234">The numerical password provided cannot unlock the volume.</span></span>|  
|`BitLockerUnlockVolumeFailed`|<span data-ttu-id="aa9de-235">嘗試解除鎖定磁碟區時發生未知的失敗。</span><span class="sxs-lookup"><span data-stu-id="aa9de-235">Unknown failure has happened when trying to unlock the volume.</span></span>|  
|`BitLockerFailed`|<span data-ttu-id="aa9de-236">執行 BitLocker 作業時發生未知的失敗。</span><span class="sxs-lookup"><span data-stu-id="aa9de-236">An unknown failure occurred while performing BitLocker operations.</span></span>|  
|`ManifestNameInvalid`|<span data-ttu-id="aa9de-237">資訊清單檔案名稱無效。</span><span class="sxs-lookup"><span data-stu-id="aa9de-237">The manifest file name is invalid.</span></span>|  
|`ManifestNameTooLong`|<span data-ttu-id="aa9de-238">資訊清單檔案名稱太長。</span><span class="sxs-lookup"><span data-stu-id="aa9de-238">The manifest file name is too long.</span></span>|  
|`ManifestNotFound`|<span data-ttu-id="aa9de-239">找不到資訊清單檔案。</span><span class="sxs-lookup"><span data-stu-id="aa9de-239">The manifest file is not found.</span></span>|  
|`ManifestAccessDenied`|<span data-ttu-id="aa9de-240">拒絕存取資訊清單檔案。</span><span class="sxs-lookup"><span data-stu-id="aa9de-240">Access to the manifest file is denied.</span></span>|  
|`ManifestCorrupted`|<span data-ttu-id="aa9de-241">資訊清單檔案已損毀 (內容不符合其雜湊)。</span><span class="sxs-lookup"><span data-stu-id="aa9de-241">The manifest file is corrupted (the content does not match its hash).</span></span>|  
|`ManifestFormatInvalid`|<span data-ttu-id="aa9de-242">資訊清單內容不符合所需格式。</span><span class="sxs-lookup"><span data-stu-id="aa9de-242">The manifest content does not conform to the required format.</span></span>|  
|`ManifestDriveIdMismatch`|<span data-ttu-id="aa9de-243">資訊清單檔案中的磁碟機識別碼與從磁碟機讀取的不符。</span><span class="sxs-lookup"><span data-stu-id="aa9de-243">The drive ID in the manifest file does not match the one read from the drive.</span></span>|  
|`ReadManifestFailed`|<span data-ttu-id="aa9de-244">讀取資訊清單時發生磁碟 I/O 失敗。</span><span class="sxs-lookup"><span data-stu-id="aa9de-244">A disk I/O failure occurred while reading from the manifest.</span></span>|  
|`BlobListFormatInvalid`|<span data-ttu-id="aa9de-245">匯出 Blob 清單 Blob 不符合所需格式。</span><span class="sxs-lookup"><span data-stu-id="aa9de-245">The export blob list blob does not conform to the required format.</span></span>|  
|`BlobRequestForbidden`|<span data-ttu-id="aa9de-246">禁止存取儲存體帳戶中的 Blob。</span><span class="sxs-lookup"><span data-stu-id="aa9de-246">Access to the blobs in the storage account is forbidden.</span></span> <span data-ttu-id="aa9de-247">這可能是因為儲存體帳戶金鑰或容器 SAS 無效。</span><span class="sxs-lookup"><span data-stu-id="aa9de-247">This might be due to invalid storage account key or container SAS.</span></span>|  
|`InternalError`|<span data-ttu-id="aa9de-248">處理磁碟機時發生內部錯誤。</span><span class="sxs-lookup"><span data-stu-id="aa9de-248">And internal error occurred while processing the drive.</span></span>|  
  
## <a name="blob-status-codes"></a><span data-ttu-id="aa9de-249">Blob 狀態碼</span><span class="sxs-lookup"><span data-stu-id="aa9de-249">Blob status codes</span></span>  
<span data-ttu-id="aa9de-250">下表列出 Blob 處理的狀態碼。</span><span class="sxs-lookup"><span data-stu-id="aa9de-250">The following table lists the status codes for processing a blob.</span></span>  
  
|<span data-ttu-id="aa9de-251">狀態碼</span><span class="sxs-lookup"><span data-stu-id="aa9de-251">Status code</span></span>|<span data-ttu-id="aa9de-252">說明</span><span class="sxs-lookup"><span data-stu-id="aa9de-252">Description</span></span>|  
|-----------------|-----------------|  
|`Completed`|<span data-ttu-id="aa9de-253">Blob 已完成處理，沒有任何錯誤。</span><span class="sxs-lookup"><span data-stu-id="aa9de-253">The blob has finished processing without errors.</span></span>|  
|`CompletedWithErrors`|<span data-ttu-id="aa9de-254">Blob 已完成處理，一或多個頁面範圍或區塊、 中繼資料或屬性中發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="aa9de-254">The blob has finished processing with errors in one or more page ranges or blocks, metadata, or properties.</span></span>|  
|`FileNameInvalid`|<span data-ttu-id="aa9de-255">檔案名稱無效。</span><span class="sxs-lookup"><span data-stu-id="aa9de-255">The file name is invalid.</span></span>|  
|`FileNameTooLong`|<span data-ttu-id="aa9de-256">檔案名稱太長。</span><span class="sxs-lookup"><span data-stu-id="aa9de-256">The file name is too long.</span></span>|  
|`FileNotFound`|<span data-ttu-id="aa9de-257">找不到檔案。</span><span class="sxs-lookup"><span data-stu-id="aa9de-257">The file is not found.</span></span>|  
|`FileAccessDenied`|<span data-ttu-id="aa9de-258">拒絕存取檔案。</span><span class="sxs-lookup"><span data-stu-id="aa9de-258">Access to the file is denied.</span></span>|  
|`BlobRequestFailed`|<span data-ttu-id="aa9de-259">存取 Blob 的 Blob 服務要求失敗。</span><span class="sxs-lookup"><span data-stu-id="aa9de-259">The Blob service request to access the blob has failed.</span></span>|  
|`BlobRequestForbidden`|<span data-ttu-id="aa9de-260">禁止存取 Blob 的 Blob 服務要求。</span><span class="sxs-lookup"><span data-stu-id="aa9de-260">The Blob service request to access the blob is forbidden.</span></span> <span data-ttu-id="aa9de-261">這可能是因為儲存體帳戶金鑰或容器 SAS 無效。</span><span class="sxs-lookup"><span data-stu-id="aa9de-261">This might be due to invalid storage account key or container SAS.</span></span>|  
|`RenameFailed`|<span data-ttu-id="aa9de-262">無法重新命名 Blob (匯入工作) 或檔案 (匯出工作)。</span><span class="sxs-lookup"><span data-stu-id="aa9de-262">Failed to rename the blob (for an import job) or the file (for an export job).</span></span>|  
|`BlobUnexpectedChange`|<span data-ttu-id="aa9de-263">Blob (匯出工作) 發生未預期的變更。</span><span class="sxs-lookup"><span data-stu-id="aa9de-263">An unexpected change has occurred with the blob (for an export job).</span></span>|  
|`LeasePresent`|<span data-ttu-id="aa9de-264">Blob 上有一個租約。</span><span class="sxs-lookup"><span data-stu-id="aa9de-264">There is a lease present on the blob.</span></span>|  
|`IOFailed`|<span data-ttu-id="aa9de-265">處理 Blob 時發生磁碟或網路 I/O 失敗。</span><span class="sxs-lookup"><span data-stu-id="aa9de-265">A disk or network I/O failure occurred while processing the blob.</span></span>|  
|`Failed`|<span data-ttu-id="aa9de-266">處理 Blob 時發生未知的失敗。</span><span class="sxs-lookup"><span data-stu-id="aa9de-266">An unknown failure occurred while processing the blob.</span></span>|  
  
## <a name="import-disposition-status-codes"></a><span data-ttu-id="aa9de-267">匯入配置狀態碼</span><span class="sxs-lookup"><span data-stu-id="aa9de-267">Import disposition status codes</span></span>  
<span data-ttu-id="aa9de-268">下表列出解決匯入配置的狀態碼。</span><span class="sxs-lookup"><span data-stu-id="aa9de-268">The following table lists the status codes for resolving an import disposition.</span></span>  
  
|<span data-ttu-id="aa9de-269">狀態碼</span><span class="sxs-lookup"><span data-stu-id="aa9de-269">Status code</span></span>|<span data-ttu-id="aa9de-270">說明</span><span class="sxs-lookup"><span data-stu-id="aa9de-270">Description</span></span>|  
|-----------------|-----------------|  
|`Created`|<span data-ttu-id="aa9de-271">Blob 已建立。</span><span class="sxs-lookup"><span data-stu-id="aa9de-271">The blob has been created.</span></span>|  
|`Renamed`|<span data-ttu-id="aa9de-272">Blob 已依照重新命名匯入配置重新命名。</span><span class="sxs-lookup"><span data-stu-id="aa9de-272">The blob has been renamed per rename import disposition.</span></span> <span data-ttu-id="aa9de-273">`Blob/BlobPath` 元素包含已重新命名的 Blob 的 URI。</span><span class="sxs-lookup"><span data-stu-id="aa9de-273">The `Blob/BlobPath` element contains the URI for the renamed blob.</span></span>|  
|`Skipped`|<span data-ttu-id="aa9de-274">已根據 `no-overwrite` 匯入配置略過 Blob。</span><span class="sxs-lookup"><span data-stu-id="aa9de-274">The blob has been skipped per `no-overwrite` import disposition.</span></span>|  
|`Overwritten`|<span data-ttu-id="aa9de-275">Blob 已根據 `overwrite` 匯入配置覆寫現有的 Blob。</span><span class="sxs-lookup"><span data-stu-id="aa9de-275">The blob has overwritten an existing blob per `overwrite` import disposition.</span></span>|  
|`Cancelled`|<span data-ttu-id="aa9de-276">先前的失敗已停止進一步處理匯入配置。</span><span class="sxs-lookup"><span data-stu-id="aa9de-276">A prior failure has stopped further processing of the import disposition.</span></span>|  
  
## <a name="page-rangeblock-status-codes"></a><span data-ttu-id="aa9de-277">頁面範圍/區塊狀態碼</span><span class="sxs-lookup"><span data-stu-id="aa9de-277">Page range/block status codes</span></span>  
<span data-ttu-id="aa9de-278">下表列出頁面範圍或區塊處理的狀態碼。</span><span class="sxs-lookup"><span data-stu-id="aa9de-278">The following table lists the status codes for processing a page range or a block.</span></span>  
  
|<span data-ttu-id="aa9de-279">狀態碼</span><span class="sxs-lookup"><span data-stu-id="aa9de-279">Status code</span></span>|<span data-ttu-id="aa9de-280">說明</span><span class="sxs-lookup"><span data-stu-id="aa9de-280">Description</span></span>|  
|-----------------|-----------------|  
|`Completed`|<span data-ttu-id="aa9de-281">頁面範圍或區塊已完成處理，沒有任何錯誤。</span><span class="sxs-lookup"><span data-stu-id="aa9de-281">The page range or block has finished processing without any errors.</span></span>|  
|`Committed`|<span data-ttu-id="aa9de-282">區塊已認可，但不在完整區塊清單中，因為其他區塊失敗，或是放置完整區塊清單本身失敗。</span><span class="sxs-lookup"><span data-stu-id="aa9de-282">The block has been committed,  but not in the full block list because other blocks have failed, or put full block list itself has failed.</span></span>|  
|`Uncommitted`|<span data-ttu-id="aa9de-283">區塊已上傳但尚未認可。</span><span class="sxs-lookup"><span data-stu-id="aa9de-283">The block is uploaded but not committed.</span></span>|  
|`Corrupted`|<span data-ttu-id="aa9de-284">頁面範圍或區塊已損毀 (內容不符合其雜湊)。</span><span class="sxs-lookup"><span data-stu-id="aa9de-284">The page range or block is corrupted (the content does not match its hash).</span></span>|  
|`FileUnexpectedEnd`|<span data-ttu-id="aa9de-285">發現非預期的檔案結尾。</span><span class="sxs-lookup"><span data-stu-id="aa9de-285">An unexpected end of file has been encountered.</span></span>|  
|`BlobUnexpectedEnd`|<span data-ttu-id="aa9de-286">發現非預期的 Blob 結尾。</span><span class="sxs-lookup"><span data-stu-id="aa9de-286">An unexpected end of blob has been encountered.</span></span>|  
|`BlobRequestFailed`|<span data-ttu-id="aa9de-287">存取頁面範圍或區塊的 Blob 服務要求失敗。</span><span class="sxs-lookup"><span data-stu-id="aa9de-287">The Blob service request to access the page range or block has failed.</span></span>|  
|`IOFailed`|<span data-ttu-id="aa9de-288">處理頁面範圍或區塊時發生磁碟或網路 I/O 失敗。</span><span class="sxs-lookup"><span data-stu-id="aa9de-288">A disk or network I/O failure occurred while processing the page range or block.</span></span>|  
|`Failed`|<span data-ttu-id="aa9de-289">處理頁面範圍或區塊時發生未知的失敗。</span><span class="sxs-lookup"><span data-stu-id="aa9de-289">An unknown failure occurred while processing the page range or block.</span></span>|  
|`Cancelled`|<span data-ttu-id="aa9de-290">先前的失敗已停止進一步處理頁面範圍或區塊。</span><span class="sxs-lookup"><span data-stu-id="aa9de-290">A prior failure has stopped further processing of the page range or block.</span></span>|  
  
## <a name="metadata-status-codes"></a><span data-ttu-id="aa9de-291">中繼資料狀態碼</span><span class="sxs-lookup"><span data-stu-id="aa9de-291">Metadata status codes</span></span>  
<span data-ttu-id="aa9de-292">下表列出 Blob 中繼資料處理的狀態碼。</span><span class="sxs-lookup"><span data-stu-id="aa9de-292">The following table lists the status codes for processing blob metadata.</span></span>  
  
|<span data-ttu-id="aa9de-293">狀態碼</span><span class="sxs-lookup"><span data-stu-id="aa9de-293">Status code</span></span>|<span data-ttu-id="aa9de-294">說明</span><span class="sxs-lookup"><span data-stu-id="aa9de-294">Description</span></span>|  
|-----------------|-----------------|  
|`Completed`|<span data-ttu-id="aa9de-295">中繼資料已完成處理，沒有任何錯誤。</span><span class="sxs-lookup"><span data-stu-id="aa9de-295">The metadata has finished processing without errors.</span></span>|  
|`FileNameInvalid`|<span data-ttu-id="aa9de-296">中繼資料檔案名稱無效。</span><span class="sxs-lookup"><span data-stu-id="aa9de-296">The metadata file name is invalid.</span></span>|  
|`FileNameTooLong`|<span data-ttu-id="aa9de-297">中繼資料檔案名稱太長。</span><span class="sxs-lookup"><span data-stu-id="aa9de-297">The metadata file name is too long.</span></span>|  
|`FileNotFound`|<span data-ttu-id="aa9de-298">找不到中繼資料檔案。</span><span class="sxs-lookup"><span data-stu-id="aa9de-298">The metadata file is not found.</span></span>|  
|`FileAccessDenied`|<span data-ttu-id="aa9de-299">拒絕存取中繼資料檔案。</span><span class="sxs-lookup"><span data-stu-id="aa9de-299">Access to the metadata file is denied.</span></span>|  
|`Corrupted`|<span data-ttu-id="aa9de-300">中繼資料檔案已損毀 (內容不符合其雜湊)。</span><span class="sxs-lookup"><span data-stu-id="aa9de-300">The metadata file is corrupted (the content does not match its hash).</span></span>|  
|`XmlReadFailed`|<span data-ttu-id="aa9de-301">中繼資料內容不符合所需格式。</span><span class="sxs-lookup"><span data-stu-id="aa9de-301">The metadata content does not conform to the required format.</span></span>|  
|`XmlWriteFailed`|<span data-ttu-id="aa9de-302">寫入中繼資料 XML 失敗。</span><span class="sxs-lookup"><span data-stu-id="aa9de-302">Writing the metadata XML has failed.</span></span>|  
|`BlobRequestFailed`|<span data-ttu-id="aa9de-303">存取中繼資料的 Blob 服務要求失敗。</span><span class="sxs-lookup"><span data-stu-id="aa9de-303">The Blob service request to access the metadata has failed.</span></span>|  
|`IOFailed`|<span data-ttu-id="aa9de-304">處理中繼資料時發生磁碟或網路 I/O 失敗。</span><span class="sxs-lookup"><span data-stu-id="aa9de-304">A disk or network I/O failure occurred while processing the metadata.</span></span>|  
|`Failed`|<span data-ttu-id="aa9de-305">處理中繼資料時發生未知的失敗。</span><span class="sxs-lookup"><span data-stu-id="aa9de-305">An unknown failure occurred while processing the metadata.</span></span>|  
|`Cancelled`|<span data-ttu-id="aa9de-306">先前的失敗已停止進一步處理中繼資料。</span><span class="sxs-lookup"><span data-stu-id="aa9de-306">A prior failure has stopped further processing of the metadata.</span></span>|  
  
## <a name="properties-status-codes"></a><span data-ttu-id="aa9de-307">屬性狀態碼</span><span class="sxs-lookup"><span data-stu-id="aa9de-307">Properties status codes</span></span>  
<span data-ttu-id="aa9de-308">下表列出 Blob 屬性處理的狀態碼。</span><span class="sxs-lookup"><span data-stu-id="aa9de-308">The following table lists the status codes for processing blob properties.</span></span>  
  
|<span data-ttu-id="aa9de-309">狀態碼</span><span class="sxs-lookup"><span data-stu-id="aa9de-309">Status code</span></span>|<span data-ttu-id="aa9de-310">說明</span><span class="sxs-lookup"><span data-stu-id="aa9de-310">Description</span></span>|  
|-----------------|-----------------|  
|`Completed`|<span data-ttu-id="aa9de-311">屬性已完成處理，沒有任何錯誤。</span><span class="sxs-lookup"><span data-stu-id="aa9de-311">The properties have finished processing without any errors.</span></span>|  
|`FileNameInvalid`|<span data-ttu-id="aa9de-312">屬性檔案名稱無效。</span><span class="sxs-lookup"><span data-stu-id="aa9de-312">The properties file name is invalid.</span></span>|  
|`FileNameTooLong`|<span data-ttu-id="aa9de-313">屬性檔案名稱太長。</span><span class="sxs-lookup"><span data-stu-id="aa9de-313">The properties file name is too long.</span></span>|  
|`FileNotFound`|<span data-ttu-id="aa9de-314">找不到屬性檔案。</span><span class="sxs-lookup"><span data-stu-id="aa9de-314">The properties file is not found.</span></span>|  
|`FileAccessDenied`|<span data-ttu-id="aa9de-315">拒絕存取屬性檔案。</span><span class="sxs-lookup"><span data-stu-id="aa9de-315">Access to the properties file is denied.</span></span>|  
|`Corrupted`|<span data-ttu-id="aa9de-316">屬性檔案已損毀 (內容不符合其雜湊)。</span><span class="sxs-lookup"><span data-stu-id="aa9de-316">The properties file is corrupted (the content does not match its hash).</span></span>|  
|`XmlReadFailed`|<span data-ttu-id="aa9de-317">屬性內容不符合所需格式。</span><span class="sxs-lookup"><span data-stu-id="aa9de-317">The properties content does not conform to the required format.</span></span>|  
|`XmlWriteFailed`|<span data-ttu-id="aa9de-318">寫入屬性 XML 失敗。</span><span class="sxs-lookup"><span data-stu-id="aa9de-318">Writing the properties XML has failed.</span></span>|  
|`BlobRequestFailed`|<span data-ttu-id="aa9de-319">存取屬性的 Blob 服務要求失敗。</span><span class="sxs-lookup"><span data-stu-id="aa9de-319">The Blob service request to access the properties has failed.</span></span>|  
|`IOFailed`|<span data-ttu-id="aa9de-320">處理屬性時發生磁碟或網路 I/O 失敗。</span><span class="sxs-lookup"><span data-stu-id="aa9de-320">A disk or network I/O failure occurred while processing the properties.</span></span>|  
|`Failed`|<span data-ttu-id="aa9de-321">處理屬性時發生未知的失敗。</span><span class="sxs-lookup"><span data-stu-id="aa9de-321">An unknown failure occurred while processing the properties.</span></span>|  
|`Cancelled`|<span data-ttu-id="aa9de-322">先前的失敗已停止進一步處理屬性。</span><span class="sxs-lookup"><span data-stu-id="aa9de-322">A prior failure has stopped further processing of the properties.</span></span>|  
  
## <a name="sample-logs"></a><span data-ttu-id="aa9de-323">範例記錄</span><span class="sxs-lookup"><span data-stu-id="aa9de-323">Sample logs</span></span>  
<span data-ttu-id="aa9de-324">以下是詳細資訊記錄檔的範例。</span><span class="sxs-lookup"><span data-stu-id="aa9de-324">The following is an example of verbose log.</span></span>  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<DriveLog Version="2014-11-01">  
    <DriveId>WD-WMATV123456</DriveId>  
    <Blob Status="Completed">  
       <BlobPath>pictures/bob/wild/desert.jpg</BlobPath>  
       <FilePath>\Users\bob\Pictures\wild\desert.jpg</FilePath>  
       <Length>98304</Length>  
       <ImportDisposition Status="Created">overwrite</ImportDisposition>  
       <BlockList>  
          <Block Offset="0" Length="65536" Id="AAAAAA==" Hash=" 9C8AE14A55241F98533C4D80D85CDC68" Status="Completed"/>  
          <Block Offset="65536" Length="32768" Id="AQAAAA==" Hash=" DF54C531C9B3CA2570FDDDB3BCD0E27D" Status="Completed"/>  
       </BlockList>  
       <Metadata Status="Completed">  
          <GlobalPath Hash=" E34F54B7086BCF4EC1601D056F4C7E37">\Users\bob\Pictures\wild\metadata.xml</GlobalPath>  
       </Metadata>  
    </Blob>  
    <Blob Status="CompletedWithErrors">  
       <BlobPath>pictures/bob/animals/koala.jpg</BlobPath>  
       <FilePath>\Users\bob\Pictures\animals\koala.jpg</FilePath>  
       <Length>163840</Length>  
       <ImportDisposition Status="Overwritten">overwrite</ImportDisposition>  
       <PageRangeList>  
          <PageRange Offset="0" Length="65536" Hash="19701B8877418393CB3CB567F53EE225" Status="Completed"/>  
          <PageRange Offset="65536" Length="65536" Hash="AA2585F6F6FD01C4AD4256E018240CD4" Status="Corrupted"/>  
          <PageRange Offset="131072" Length="4096" Hash="9BA552E1C3EEAFFC91B42B979900A996" Status="Completed"/>  
       </PageRangeList>  
       <Properties Status="Completed">  
          <Path Hash="38D7AE80653F47F63C0222FEE90EC4E7">\Users\bob\Pictures\animals\koala.jpg.properties</Path>  
       </Properties>  
    </Blob>  
    <Status>CompletedWithErrors</Status>  
</DriveLog>  
```  
  
<span data-ttu-id="aa9de-325">對應的錯誤記錄檔顯示如下：</span><span class="sxs-lookup"><span data-stu-id="aa9de-325">The corresponding error log is shown below.</span></span>  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<DriveLog Version="2014-11-01">  
    <DriveId>WD-WMATV6965824</DriveId>  
    <Blob Status="CompletedWithErrors">  
       <BlobPath>pictures/bob/animals/koala.jpg</BlobPath>  
       <FilePath>\Users\bob\Pictures\animals\koala.jpg</FilePath>  
       <Length>163840</Length>  
       <ImportDisposition Status="Overwritten">overwrite</ImportDisposition>  
       <PageRangeList>  
          <PageRange Offset="65536" Length="65536" Hash="AA2585F6F6FD01C4AD4256E018240CD4" Status="Corrupted"/>  
       </PageRangeList>  
    </Blob>  
    <Status>CompletedWithErrors</Status>  
</DriveLog>  
```

 <span data-ttu-id="aa9de-326">匯入工作的下列錯誤記錄檔包含在匯入磁碟機上找不到檔案的相關錯誤。</span><span class="sxs-lookup"><span data-stu-id="aa9de-326">The follow error log for an import job contains an error about a file not found on the import drive.</span></span> <span data-ttu-id="aa9de-327">請注意，後續元件的狀態是 `Cancelled`。</span><span class="sxs-lookup"><span data-stu-id="aa9de-327">Note that the status of subsequent components is `Cancelled`.</span></span>  
  
```xml
<?xml version="1.0" encoding="utf-8"?>  
<DriveLog Version="2014-11-01">  
  <DriveId>9WM35C2V</DriveId>  
  <Blob Status="FileNotFound">  
    <BlobPath>pictures/animals/koala.jpg</BlobPath>  
    <FilePath>\animals\koala.jpg</FilePath>  
    <Length>30310</Length>  
    <ImportDisposition Status="Cancelled">rename</ImportDisposition>  
    <BlockList>  
      <Block Offset="0" Length="6062" Id="MD5/cAzn4h7VVSWXf696qp5Uaw==" Hash="700CE7E21ED55525977FAF7AAA9E546B" Status="Cancelled" />  
      <Block Offset="6062" Length="6062" Id="MD5/PEnGwYOI8LPLNYdfKr7kAg==" Hash="3C49C6C18388F0B3CB35875F2ABEE402" Status="Cancelled" />  
      <Block Offset="12124" Length="6062" Id="MD5/FG4WxqfZKuUWZ2nGTU2qVA==" Hash="146E16C6A7D92AE5166769C64D4DAA54" Status="Cancelled" />  
      <Block Offset="18186" Length="6062" Id="MD5/ZzibNDzr3IRBQENRyegeXQ==" Hash="67389B343CEBDC8441404351C9E81E5D" Status="Cancelled" />  
      <Block Offset="24248" Length="6062" Id="MD5/ZzibNDzr3IRBQENRyegeXQ==" Hash="67389B343CEBDC8441404351C9E81E5D" Status="Cancelled" />  
    </BlockList>  
  </Blob>  
  <Status>CompletedWithErrors</Status>  
</DriveLog>  
```

<span data-ttu-id="aa9de-328">匯出工作的下列錯誤記錄檔指出 Blob 內容已順利寫入至磁碟機，但匯出 Blob 的屬性時發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="aa9de-328">The following error log for an export job indicates that the blob content has been successfully written to the drive, but that an error occurred while exporting the blob's properties.</span></span>  
  
```xml
<?xml version="1.0" encoding="utf-8"?>  
<DriveLog Version="2014-11-01">  
  <DriveId>9WM35C3U</DriveId>  
  <Blob Status="CompletedWithErrors">  
    <BlobPath>pictures/wild/canyon.jpg</BlobPath>  
    <FilePath>\pictures\wild\canyon.jpg</FilePath>  
    <LastModified>2012-09-18T23:47:08Z</LastModified>  
    <Length>163840</Length>  
    <BlockList />  
    <Properties Status="Failed" />  
  </Blob>  
  <Status>CompletedWithErrors</Status>  
</DriveLog>  
```
  
## <a name="next-steps"></a><span data-ttu-id="aa9de-329">後續步驟</span><span class="sxs-lookup"><span data-stu-id="aa9de-329">Next steps</span></span>
 
* [<span data-ttu-id="aa9de-330">儲存體匯入/匯出 REST API</span><span class="sxs-lookup"><span data-stu-id="aa9de-330">Storage Import/Export REST API</span></span>](/rest/api/storageimportexport/)
