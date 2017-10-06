---
title: "aaaAzure 匯入/匯出記錄檔檔案格式 |Microsoft 文件"
description: "深入了解 hello hello 建立之記錄檔的步驟執行匯入/匯出服務作業時的格式。"
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
ms.openlocfilehash: 15a652455aa947922af0aa39ccefe68811a3db19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-importexport-service-log-file-format"></a><span data-ttu-id="7b008-103">Azure 匯入/匯出服務記錄檔格式</span><span class="sxs-lookup"><span data-stu-id="7b008-103">Azure Import/Export service log file format</span></span>
<span data-ttu-id="7b008-104">當 hello Microsoft Azure 匯入/匯出服務磁碟機上執行的動作，匯入工作或匯出工作的一部分時，記錄檔寫入 tooblock blob hello 與該工作相關聯的儲存體帳戶中。</span><span class="sxs-lookup"><span data-stu-id="7b008-104">When hello Microsoft Azure Import/Export service performs an action on a drive as part of an import job or an export job, logs are written tooblock blobs in hello storage account associated with that job.</span></span>  
  
<span data-ttu-id="7b008-105">有兩個可能 hello 匯入/匯出服務所寫入的記錄檔：</span><span class="sxs-lookup"><span data-stu-id="7b008-105">There are two logs that may be written by hello Import/Export service:</span></span>  
  
-   <span data-ttu-id="7b008-106">hello 錯誤事件中，一定會產生 hello 錯誤記錄檔。</span><span class="sxs-lookup"><span data-stu-id="7b008-106">hello error log is always generated in hello event of an error.</span></span>  
  
-   <span data-ttu-id="7b008-107">hello 詳細資訊記錄檔未啟用依預設，但是可能加以啟用設定 hello`EnableVerboseLog`屬性[Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate)或[Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update)作業。</span><span class="sxs-lookup"><span data-stu-id="7b008-107">hello verbose log is not enabled by default, but may be enabled by setting hello `EnableVerboseLog` property on a [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) or [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) operation.</span></span>  
  
## <a name="log-file-location"></a><span data-ttu-id="7b008-108">記錄檔位置</span><span class="sxs-lookup"><span data-stu-id="7b008-108">Log file location</span></span>  
<span data-ttu-id="7b008-109">hello 記錄檔寫入 tooblock blob hello 容器或 hello 所指定的虛擬目錄中`ImportExportStatesPath`設定，您可以設定`Put Job`作業。</span><span class="sxs-lookup"><span data-stu-id="7b008-109">hello logs are written tooblock blobs in hello container or virtual directory specified by hello `ImportExportStatesPath` setting, which you can set on a `Put Job` operation.</span></span> <span data-ttu-id="7b008-110">hello 位置 toowhich hello 記錄檔寫入取決於如何指定 hello 作業，以及指定 hello 值驗證`ImportExportStatesPath`。</span><span class="sxs-lookup"><span data-stu-id="7b008-110">hello location toowhich hello logs are written depends on how authentication is specified for hello job, together with hello value specified for `ImportExportStatesPath`.</span></span> <span data-ttu-id="7b008-111">您可以透過儲存體帳戶金鑰或容器 SAS （共用的存取簽章） 指定 hello 工作的驗證。</span><span class="sxs-lookup"><span data-stu-id="7b008-111">Authentication for hello job may be specified via a storage account key, or a container SAS (shared access signature).</span></span>  
  
<span data-ttu-id="7b008-112">hello hello 容器或虛擬目錄的名稱可能是預設名稱 hello `waimportexport`，或另一個容器或您指定的虛擬目錄名稱。</span><span class="sxs-lookup"><span data-stu-id="7b008-112">hello name of hello container or virtual directory may either be hello default name of `waimportexport`, or another container or virtual directory name that you specify.</span></span>  
  
<span data-ttu-id="7b008-113">hello 下表顯示 hello 可能的選項：</span><span class="sxs-lookup"><span data-stu-id="7b008-113">hello table below shows hello possible options:</span></span>  
  
|<span data-ttu-id="7b008-114">驗證方法</span><span class="sxs-lookup"><span data-stu-id="7b008-114">Authentication Method</span></span>|<span data-ttu-id="7b008-115">`ImportExportStatesPath` 元素的值</span><span class="sxs-lookup"><span data-stu-id="7b008-115">Value of `ImportExportStatesPath`Element</span></span>|<span data-ttu-id="7b008-116">記錄檔 Blob 的位置</span><span class="sxs-lookup"><span data-stu-id="7b008-116">Location of Log Blobs</span></span>|  
|---------------------------|----------------------------------------------|---------------------------|  
|<span data-ttu-id="7b008-117">儲存體帳戶金鑰</span><span class="sxs-lookup"><span data-stu-id="7b008-117">Storage account key</span></span>|<span data-ttu-id="7b008-118">預設值</span><span class="sxs-lookup"><span data-stu-id="7b008-118">Default value</span></span>|<span data-ttu-id="7b008-119">名為的容器`waimportexport`，這是 hello 預設容器。</span><span class="sxs-lookup"><span data-stu-id="7b008-119">A container named `waimportexport`, which is hello default container.</span></span> <span data-ttu-id="7b008-120">例如：</span><span class="sxs-lookup"><span data-stu-id="7b008-120">For example:</span></span><br /><br /> `https://myaccount.blob.core.windows.net/waimportexport`|  
|<span data-ttu-id="7b008-121">儲存體帳戶金鑰</span><span class="sxs-lookup"><span data-stu-id="7b008-121">Storage account key</span></span>|<span data-ttu-id="7b008-122">使用者指定值</span><span class="sxs-lookup"><span data-stu-id="7b008-122">User-specified value</span></span>|<span data-ttu-id="7b008-123">名為 hello 使用者的容器。</span><span class="sxs-lookup"><span data-stu-id="7b008-123">A container named by hello user.</span></span> <span data-ttu-id="7b008-124">例如：</span><span class="sxs-lookup"><span data-stu-id="7b008-124">For example:</span></span><br /><br /> `https://myaccount.blob.core.windows.net/mylogcontainer`|  
|<span data-ttu-id="7b008-125">容器 SAS</span><span class="sxs-lookup"><span data-stu-id="7b008-125">Container SAS</span></span>|<span data-ttu-id="7b008-126">預設值</span><span class="sxs-lookup"><span data-stu-id="7b008-126">Default value</span></span>|<span data-ttu-id="7b008-127">命名的虛擬目錄`waimportexport`，這是 hello hello SAS 中指定的容器下方的 hello 預設名稱。</span><span class="sxs-lookup"><span data-stu-id="7b008-127">A virtual directory named `waimportexport`, which is hello default name, beneath hello container specified in hello SAS.</span></span><br /><br /> <span data-ttu-id="7b008-128">例如，如果 hello SAS 指定 hello 工作是`https://myaccount.blob.core.windows.net/mylogcontainer?sv=2012-02-12&se=2015-05-22T06%3A54%3A55Z&sr=c&sp=wl&sig=sigvalue`，則會是 hello 記錄檔位置`https://myaccount.blob.core.windows.net/mylogcontainer/waimportexport`</span><span class="sxs-lookup"><span data-stu-id="7b008-128">For example, if hello SAS specified for hello job is  `https://myaccount.blob.core.windows.net/mylogcontainer?sv=2012-02-12&se=2015-05-22T06%3A54%3A55Z&sr=c&sp=wl&sig=sigvalue`, then hello log location would be `https://myaccount.blob.core.windows.net/mylogcontainer/waimportexport`</span></span>|  
|<span data-ttu-id="7b008-129">容器 SAS</span><span class="sxs-lookup"><span data-stu-id="7b008-129">Container SAS</span></span>|<span data-ttu-id="7b008-130">使用者指定值</span><span class="sxs-lookup"><span data-stu-id="7b008-130">User-specified value</span></span>|<span data-ttu-id="7b008-131">由 hello hello SAS 中指定的容器下方的 hello 使用者命名的虛擬目錄。</span><span class="sxs-lookup"><span data-stu-id="7b008-131">A virtual directory named by hello user, beneath hello container specified in hello SAS.</span></span><br /><br /> <span data-ttu-id="7b008-132">例如，如果 hello SAS 指定 hello 工作是`https://myaccount.blob.core.windows.net/mylogcontainer?sv=2012-02-12&se=2015-05-22T06%3A54%3A55Z&sr=c&sp=wl&sig=sigvalue`，而且 hello 可讓您指定虛擬目錄叫作`mylogblobs`，hello 記錄檔位置將是`https://myaccount.blob.core.windows.net/mylogcontainer/waimportexport/mylogblobs`。</span><span class="sxs-lookup"><span data-stu-id="7b008-132">For example, if hello SAS specified for hello job is  `https://myaccount.blob.core.windows.net/mylogcontainer?sv=2012-02-12&se=2015-05-22T06%3A54%3A55Z&sr=c&sp=wl&sig=sigvalue`, and hello specified virtual directory is named `mylogblobs`, then hello log location would be `https://myaccount.blob.core.windows.net/mylogcontainer/waimportexport/mylogblobs`.</span></span>|  
  
<span data-ttu-id="7b008-133">您可以擷取 hello 錯誤和詳細資訊記錄檔的 hello URL 呼叫 hello [Get Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate)作業。</span><span class="sxs-lookup"><span data-stu-id="7b008-133">You can retrieve hello URL for hello error and verbose logs by calling hello [Get Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operation.</span></span> <span data-ttu-id="7b008-134">hello 磁碟機處理完成後，並提供 hello 記錄。</span><span class="sxs-lookup"><span data-stu-id="7b008-134">hello logs are available after processing of hello drive is complete.</span></span>  
  
## <a name="log-file-format"></a><span data-ttu-id="7b008-135">記錄檔格式</span><span class="sxs-lookup"><span data-stu-id="7b008-135">Log file format</span></span>  
<span data-ttu-id="7b008-136">hello 這兩個記錄的格式是 hello 相同： blob，其中包含的 hello 事件複製 hello 硬碟機和 hello 客戶帳戶之間的 blob 時所發生的 XML 描述。</span><span class="sxs-lookup"><span data-stu-id="7b008-136">hello format for both logs is hello same: a blob containing XML descriptions of hello events that occurred while copying blobs between hello hard drive and hello customer's account.</span></span>  
  
<span data-ttu-id="7b008-137">hello 詳細資訊記錄檔包含 hello 複製作業，每個 blob （用於匯入工作） 或 （適用於匯出工作），檔案的 hello 狀態的完整資訊，而 hello 錯誤記錄檔只包含 hello 資訊之 blob 或 hello 期間發生錯誤的檔案匯入或匯出工作。</span><span class="sxs-lookup"><span data-stu-id="7b008-137">hello verbose log contains complete information about hello status of hello copy operation for every blob (for an import job) or file (for an export job), whereas hello error log contains only hello information for blobs or files that encountered errors during hello import or export job.</span></span>  
  
<span data-ttu-id="7b008-138">hello 詳細資訊記錄檔格式如下所示。</span><span class="sxs-lookup"><span data-stu-id="7b008-138">hello verbose log format is shown below.</span></span> <span data-ttu-id="7b008-139">hello 錯誤記錄檔有的 hello 相同結構，但是它會篩選出成功的作業。</span><span class="sxs-lookup"><span data-stu-id="7b008-139">hello error log has hello same structure, but filters out successful operations.</span></span>  

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

<span data-ttu-id="7b008-140">hello 下表描述 hello hello 記錄檔項目。</span><span class="sxs-lookup"><span data-stu-id="7b008-140">hello following table describes hello elements of hello log file.</span></span>  
  
|<span data-ttu-id="7b008-141">XML 元素</span><span class="sxs-lookup"><span data-stu-id="7b008-141">XML Element</span></span>|<span data-ttu-id="7b008-142">類型</span><span class="sxs-lookup"><span data-stu-id="7b008-142">Type</span></span>|<span data-ttu-id="7b008-143">說明</span><span class="sxs-lookup"><span data-stu-id="7b008-143">Description</span></span>|  
|-----------------|----------|-----------------|  
|`DriveLog`|<span data-ttu-id="7b008-144">XML 元素</span><span class="sxs-lookup"><span data-stu-id="7b008-144">XML Element</span></span>|<span data-ttu-id="7b008-145">代表磁碟機記錄檔。</span><span class="sxs-lookup"><span data-stu-id="7b008-145">Represents a drive log.</span></span>|  
|`Version`|<span data-ttu-id="7b008-146">屬性、字串</span><span class="sxs-lookup"><span data-stu-id="7b008-146">Attribute, String</span></span>|<span data-ttu-id="7b008-147">hello hello 記錄格式版本。</span><span class="sxs-lookup"><span data-stu-id="7b008-147">hello version of hello log format.</span></span>|  
|`DriveId`|<span data-ttu-id="7b008-148">String</span><span class="sxs-lookup"><span data-stu-id="7b008-148">String</span></span>|<span data-ttu-id="7b008-149">hello 磁碟機的硬體序號。</span><span class="sxs-lookup"><span data-stu-id="7b008-149">hello drive's hardware serial number.</span></span>|  
|`Status`|<span data-ttu-id="7b008-150">String</span><span class="sxs-lookup"><span data-stu-id="7b008-150">String</span></span>|<span data-ttu-id="7b008-151">Hello 磁碟機處理的狀態。</span><span class="sxs-lookup"><span data-stu-id="7b008-151">Status of hello drive processing.</span></span> <span data-ttu-id="7b008-152">請參閱 hello`Drive Status Codes`表格如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="7b008-152">See hello `Drive Status Codes` table below for more information.</span></span>|  
|`Blob`|<span data-ttu-id="7b008-153">巢狀的 XML 元素</span><span class="sxs-lookup"><span data-stu-id="7b008-153">Nested XML element</span></span>|<span data-ttu-id="7b008-154">代表 Blob。</span><span class="sxs-lookup"><span data-stu-id="7b008-154">Represents a blob.</span></span>|  
|`Blob/BlobPath`|<span data-ttu-id="7b008-155">String</span><span class="sxs-lookup"><span data-stu-id="7b008-155">String</span></span>|<span data-ttu-id="7b008-156">hello hello blob 的 URI。</span><span class="sxs-lookup"><span data-stu-id="7b008-156">hello URI of hello blob.</span></span>|  
|`Blob/FilePath`|<span data-ttu-id="7b008-157">String</span><span class="sxs-lookup"><span data-stu-id="7b008-157">String</span></span>|<span data-ttu-id="7b008-158">hello 相對路徑 toohello hello 磁碟機檔案。</span><span class="sxs-lookup"><span data-stu-id="7b008-158">hello relative path toohello file on hello drive.</span></span>|  
|`Blob/Snapshot`|<span data-ttu-id="7b008-159">DateTime</span><span class="sxs-lookup"><span data-stu-id="7b008-159">DateTime</span></span>|<span data-ttu-id="7b008-160">hello hello blob，僅限於匯出工作的快照集版本。</span><span class="sxs-lookup"><span data-stu-id="7b008-160">hello snapshot version of hello blob, for an export job only.</span></span>|  
|`Blob/Length`|<span data-ttu-id="7b008-161">Integer</span><span class="sxs-lookup"><span data-stu-id="7b008-161">Integer</span></span>|<span data-ttu-id="7b008-162">hello 的 hello blob 以位元組為單位的總長度。</span><span class="sxs-lookup"><span data-stu-id="7b008-162">hello total length of hello blob in bytes.</span></span>|  
|`Blob/LastModified`|<span data-ttu-id="7b008-163">DateTime</span><span class="sxs-lookup"><span data-stu-id="7b008-163">DateTime</span></span>|<span data-ttu-id="7b008-164">hello 日期/時間 hello blob 上次修改僅限於匯出工作。</span><span class="sxs-lookup"><span data-stu-id="7b008-164">hello date/time that hello blob was last modified, for an export job only.</span></span>|  
|`Blob/ImportDisposition`|<span data-ttu-id="7b008-165">String</span><span class="sxs-lookup"><span data-stu-id="7b008-165">String</span></span>|<span data-ttu-id="7b008-166">hello 匯入的 hello blob，僅限於匯入工作的配置。</span><span class="sxs-lookup"><span data-stu-id="7b008-166">hello import disposition of hello blob, for an import job only.</span></span>|  
|`Blob/ImportDisposition/@Status`|<span data-ttu-id="7b008-167">屬性、字串</span><span class="sxs-lookup"><span data-stu-id="7b008-167">Attribute, String</span></span>|<span data-ttu-id="7b008-168">hello hello 狀態匯入配置。</span><span class="sxs-lookup"><span data-stu-id="7b008-168">hello status of hello import disposition.</span></span>|  
|`PageRangeList`|<span data-ttu-id="7b008-169">巢狀的 XML 元素</span><span class="sxs-lookup"><span data-stu-id="7b008-169">Nested XML element</span></span>|<span data-ttu-id="7b008-170">代表分頁 Blob 的頁面範圍清單。</span><span class="sxs-lookup"><span data-stu-id="7b008-170">Represents a list of page ranges for a page blob.</span></span>|  
|`PageRange`|<span data-ttu-id="7b008-171">XML 元素</span><span class="sxs-lookup"><span data-stu-id="7b008-171">XML element</span></span>|<span data-ttu-id="7b008-172">代表頁面範圍。</span><span class="sxs-lookup"><span data-stu-id="7b008-172">Represents a page range.</span></span>|  
|`PageRange/@Offset`|<span data-ttu-id="7b008-173">屬性、整數</span><span class="sxs-lookup"><span data-stu-id="7b008-173">Attribute, Integer</span></span>|<span data-ttu-id="7b008-174">Hello blob 中的起始位移 hello 頁面範圍。</span><span class="sxs-lookup"><span data-stu-id="7b008-174">Starting offset of hello page range in hello blob.</span></span>|  
|`PageRange/@Length`|<span data-ttu-id="7b008-175">屬性、整數</span><span class="sxs-lookup"><span data-stu-id="7b008-175">Attribute, Integer</span></span>|<span data-ttu-id="7b008-176">以位元組為單位的 hello 頁面範圍的長度。</span><span class="sxs-lookup"><span data-stu-id="7b008-176">Length in bytes of hello page range.</span></span>|  
|`PageRange/@Hash`|<span data-ttu-id="7b008-177">屬性、字串</span><span class="sxs-lookup"><span data-stu-id="7b008-177">Attribute, String</span></span>|<span data-ttu-id="7b008-178">Base16 編碼 MD5 雜湊的 hello 頁面範圍。</span><span class="sxs-lookup"><span data-stu-id="7b008-178">Base16-encoded MD5 hash of hello page range.</span></span>|  
|`PageRange/@Status`|<span data-ttu-id="7b008-179">屬性、字串</span><span class="sxs-lookup"><span data-stu-id="7b008-179">Attribute, String</span></span>|<span data-ttu-id="7b008-180">處理 hello 頁面範圍的狀態。</span><span class="sxs-lookup"><span data-stu-id="7b008-180">Status of processing hello page range.</span></span>|  
|`BlockList`|<span data-ttu-id="7b008-181">巢狀的 XML 元素</span><span class="sxs-lookup"><span data-stu-id="7b008-181">Nested XML element</span></span>|<span data-ttu-id="7b008-182">代表區塊 Blob 的區塊清單。</span><span class="sxs-lookup"><span data-stu-id="7b008-182">Represents a list of blocks for a block blob.</span></span>|  
|`Block`|<span data-ttu-id="7b008-183">XML 元素</span><span class="sxs-lookup"><span data-stu-id="7b008-183">XML element</span></span>|<span data-ttu-id="7b008-184">代表區塊。</span><span class="sxs-lookup"><span data-stu-id="7b008-184">Represents a block.</span></span>|  
|`Block/@Offset`|<span data-ttu-id="7b008-185">屬性、整數</span><span class="sxs-lookup"><span data-stu-id="7b008-185">Attribute, Integer</span></span>|<span data-ttu-id="7b008-186">Hello blob 中的 hello 區塊起始位移。</span><span class="sxs-lookup"><span data-stu-id="7b008-186">Starting offset of hello block in hello blob.</span></span>|  
|`Block/@Length`|<span data-ttu-id="7b008-187">屬性、整數</span><span class="sxs-lookup"><span data-stu-id="7b008-187">Attribute, Integer</span></span>|<span data-ttu-id="7b008-188">以位元組為單位的 hello 區塊的長度。</span><span class="sxs-lookup"><span data-stu-id="7b008-188">Length in bytes of hello block.</span></span>|  
|`Block/@Id`|<span data-ttu-id="7b008-189">屬性、字串</span><span class="sxs-lookup"><span data-stu-id="7b008-189">Attribute, String</span></span>|<span data-ttu-id="7b008-190">hello 區塊識別碼。</span><span class="sxs-lookup"><span data-stu-id="7b008-190">hello block ID.</span></span>|  
|`Block/@Hash`|<span data-ttu-id="7b008-191">屬性、字串</span><span class="sxs-lookup"><span data-stu-id="7b008-191">Attribute, String</span></span>|<span data-ttu-id="7b008-192">Base16 編碼 MD5 雜湊的 hello 區塊。</span><span class="sxs-lookup"><span data-stu-id="7b008-192">Base16-encoded MD5 hash of hello block.</span></span>|  
|`Block/@Status`|<span data-ttu-id="7b008-193">屬性、字串</span><span class="sxs-lookup"><span data-stu-id="7b008-193">Attribute, String</span></span>|<span data-ttu-id="7b008-194">處理 hello 區塊的狀態。</span><span class="sxs-lookup"><span data-stu-id="7b008-194">Status of processing hello block.</span></span>|  
|`Metadata`|<span data-ttu-id="7b008-195">巢狀的 XML 元素</span><span class="sxs-lookup"><span data-stu-id="7b008-195">Nested XML element</span></span>|<span data-ttu-id="7b008-196">代表 hello blob 的中繼資料。</span><span class="sxs-lookup"><span data-stu-id="7b008-196">Represents hello blob's metadata.</span></span>|  
|`Metadata/@Status`|<span data-ttu-id="7b008-197">屬性、字串</span><span class="sxs-lookup"><span data-stu-id="7b008-197">Attribute, String</span></span>|<span data-ttu-id="7b008-198">Hello blob 中繼資料的處理狀態。</span><span class="sxs-lookup"><span data-stu-id="7b008-198">Status of processing of hello blob metadata.</span></span>|  
|`Metadata/GlobalPath`|<span data-ttu-id="7b008-199">String</span><span class="sxs-lookup"><span data-stu-id="7b008-199">String</span></span>|<span data-ttu-id="7b008-200">相對路徑 toohello 全域中繼資料檔案。</span><span class="sxs-lookup"><span data-stu-id="7b008-200">Relative path toohello global metadata file.</span></span>|  
|`Metadata/GlobalPath/@Hash`|<span data-ttu-id="7b008-201">屬性、字串</span><span class="sxs-lookup"><span data-stu-id="7b008-201">Attribute, String</span></span>|<span data-ttu-id="7b008-202">Base16 編碼 MD5 雜湊的 hello 全域中繼資料檔案。</span><span class="sxs-lookup"><span data-stu-id="7b008-202">Base16-encoded MD5 hash of hello global metadata file.</span></span>|  
|`Metadata/Path`|<span data-ttu-id="7b008-203">String</span><span class="sxs-lookup"><span data-stu-id="7b008-203">String</span></span>|<span data-ttu-id="7b008-204">相對路徑 toohello 中繼資料檔案。</span><span class="sxs-lookup"><span data-stu-id="7b008-204">Relative path toohello metadata file.</span></span>|  
|`Metadata/Path/@Hash`|<span data-ttu-id="7b008-205">屬性、字串</span><span class="sxs-lookup"><span data-stu-id="7b008-205">Attribute, String</span></span>|<span data-ttu-id="7b008-206">Base16 編碼 MD5 雜湊的 hello 中繼資料檔案。</span><span class="sxs-lookup"><span data-stu-id="7b008-206">Base16-encoded MD5 hash of hello metadata file.</span></span>|  
|`Properties`|<span data-ttu-id="7b008-207">巢狀的 XML 元素</span><span class="sxs-lookup"><span data-stu-id="7b008-207">Nested XML element</span></span>|<span data-ttu-id="7b008-208">代表 hello blob 屬性。</span><span class="sxs-lookup"><span data-stu-id="7b008-208">Represents hello blob properties.</span></span>|  
|`Properties/@Status`|<span data-ttu-id="7b008-209">屬性、字串</span><span class="sxs-lookup"><span data-stu-id="7b008-209">Attribute, String</span></span>|<span data-ttu-id="7b008-210">狀態處理 hello blob 屬性，例如找不到檔案，已完成。</span><span class="sxs-lookup"><span data-stu-id="7b008-210">Status of processing hello blob properties, e.g. file not found, completed.</span></span>|  
|`Properties/GlobalPath`|<span data-ttu-id="7b008-211">String</span><span class="sxs-lookup"><span data-stu-id="7b008-211">String</span></span>|<span data-ttu-id="7b008-212">相對路徑 toohello 全域屬性檔。</span><span class="sxs-lookup"><span data-stu-id="7b008-212">Relative path toohello global properties file.</span></span>|  
|`Properties/GlobalPath/@Hash`|<span data-ttu-id="7b008-213">屬性、字串</span><span class="sxs-lookup"><span data-stu-id="7b008-213">Attribute, String</span></span>|<span data-ttu-id="7b008-214">Base16 編碼 MD5 雜湊的 hello 全域屬性檔。</span><span class="sxs-lookup"><span data-stu-id="7b008-214">Base16-encoded MD5 hash of hello global properties file.</span></span>|  
|`Properties/Path`|<span data-ttu-id="7b008-215">String</span><span class="sxs-lookup"><span data-stu-id="7b008-215">String</span></span>|<span data-ttu-id="7b008-216">相對路徑 toohello 屬性檔。</span><span class="sxs-lookup"><span data-stu-id="7b008-216">Relative path toohello properties file.</span></span>|  
|`Properties/Path/@Hash`|<span data-ttu-id="7b008-217">屬性、字串</span><span class="sxs-lookup"><span data-stu-id="7b008-217">Attribute, String</span></span>|<span data-ttu-id="7b008-218">Base16 編碼 MD5 雜湊的 hello 屬性檔。</span><span class="sxs-lookup"><span data-stu-id="7b008-218">Base16-encoded MD5 hash of hello properties file.</span></span>|  
|`Blob/Status`|<span data-ttu-id="7b008-219">String</span><span class="sxs-lookup"><span data-stu-id="7b008-219">String</span></span>|<span data-ttu-id="7b008-220">處理 hello blob 的狀態。</span><span class="sxs-lookup"><span data-stu-id="7b008-220">Status of processing hello blob.</span></span>|  
  
# <a name="drive-status-codes"></a><span data-ttu-id="7b008-221">磁碟機狀態碼</span><span class="sxs-lookup"><span data-stu-id="7b008-221">Drive status codes</span></span>  
<span data-ttu-id="7b008-222">hello 下表列出處理磁碟機的 hello 狀態碼。</span><span class="sxs-lookup"><span data-stu-id="7b008-222">hello following table lists hello status codes for processing a drive.</span></span>  
  
|<span data-ttu-id="7b008-223">狀態碼</span><span class="sxs-lookup"><span data-stu-id="7b008-223">Status code</span></span>|<span data-ttu-id="7b008-224">說明</span><span class="sxs-lookup"><span data-stu-id="7b008-224">Description</span></span>|  
|-----------------|-----------------|  
|`Completed`|<span data-ttu-id="7b008-225">hello 磁碟機已完成處理，沒有任何錯誤。</span><span class="sxs-lookup"><span data-stu-id="7b008-225">hello drive has finished processing without any errors.</span></span>|  
|`CompletedWithWarnings`|<span data-ttu-id="7b008-226">hello 磁碟機已完成處理，但每 hello hello blob 指定的匯入配置出現一個或多個 blob 中的警告。</span><span class="sxs-lookup"><span data-stu-id="7b008-226">hello drive has finished processing with warnings in one or more blobs per hello import dispositions specified for hello blobs.</span></span>|  
|`CompletedWithErrors`|<span data-ttu-id="7b008-227">hello 磁碟機已完成但一或多個 blob 或區塊發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="7b008-227">hello drive has finished with errors in one or more blobs or chunks.</span></span>|  
|`DiskNotFound`|<span data-ttu-id="7b008-228">Hello 磁碟機上找到的磁碟。</span><span class="sxs-lookup"><span data-stu-id="7b008-228">No disk is found on hello drive.</span></span>|  
|`VolumeNotNtfs`|<span data-ttu-id="7b008-229">hello 第一個資料磁碟上的磁碟區 hello 不是 NTFS 格式。</span><span class="sxs-lookup"><span data-stu-id="7b008-229">hello first data volume on hello disk is not in NTFS format.</span></span>|  
|`DiskOperationFailed`|<span data-ttu-id="7b008-230">Hello 磁碟機上執行作業時發生未知的失敗。</span><span class="sxs-lookup"><span data-stu-id="7b008-230">An unknown failure occurred when performing operations on hello drive.</span></span>|  
|`BitLockerVolumeNotFound`|<span data-ttu-id="7b008-231">找不到 BitLocker 可加密磁碟區。</span><span class="sxs-lookup"><span data-stu-id="7b008-231">No BitLocker encryptable volume is found.</span></span>|  
|`BitLockerNotActivated`|<span data-ttu-id="7b008-232">不會在 hello 磁碟區上啟用 BitLocker。</span><span class="sxs-lookup"><span data-stu-id="7b008-232">BitLocker is not enabled on hello volume.</span></span>|  
|`BitLockerProtectorNotFound`|<span data-ttu-id="7b008-233">hello 數字密碼金鑰保護裝置 hello 磁碟區上不存在。</span><span class="sxs-lookup"><span data-stu-id="7b008-233">hello numerical password key protector does not exist on hello volume.</span></span>|  
|`BitLockerKeyInvalid`|<span data-ttu-id="7b008-234">提供的 hello 數字密碼無法解除鎖定 hello 磁碟區。</span><span class="sxs-lookup"><span data-stu-id="7b008-234">hello numerical password provided cannot unlock hello volume.</span></span>|  
|`BitLockerUnlockVolumeFailed`|<span data-ttu-id="7b008-235">嘗試 toounlock hello 磁碟區時，發生未知的失敗。</span><span class="sxs-lookup"><span data-stu-id="7b008-235">Unknown failure has happened when trying toounlock hello volume.</span></span>|  
|`BitLockerFailed`|<span data-ttu-id="7b008-236">執行 BitLocker 作業時發生未知的失敗。</span><span class="sxs-lookup"><span data-stu-id="7b008-236">An unknown failure occurred while performing BitLocker operations.</span></span>|  
|`ManifestNameInvalid`|<span data-ttu-id="7b008-237">hello 資訊清單檔案名稱無效。</span><span class="sxs-lookup"><span data-stu-id="7b008-237">hello manifest file name is invalid.</span></span>|  
|`ManifestNameTooLong`|<span data-ttu-id="7b008-238">hello 資訊清單檔案名稱過長。</span><span class="sxs-lookup"><span data-stu-id="7b008-238">hello manifest file name is too long.</span></span>|  
|`ManifestNotFound`|<span data-ttu-id="7b008-239">找不到 hello 資訊清單檔案。</span><span class="sxs-lookup"><span data-stu-id="7b008-239">hello manifest file is not found.</span></span>|  
|`ManifestAccessDenied`|<span data-ttu-id="7b008-240">拒絕存取 toohello 資訊清單檔案。</span><span class="sxs-lookup"><span data-stu-id="7b008-240">Access toohello manifest file is denied.</span></span>|  
|`ManifestCorrupted`|<span data-ttu-id="7b008-241">hello 資訊清單檔案已損毀 （hello 內容不符合其雜湊）。</span><span class="sxs-lookup"><span data-stu-id="7b008-241">hello manifest file is corrupted (hello content does not match its hash).</span></span>|  
|`ManifestFormatInvalid`|<span data-ttu-id="7b008-242">hello 資訊清單內容不符合 toohello 所需的格式。</span><span class="sxs-lookup"><span data-stu-id="7b008-242">hello manifest content does not conform toohello required format.</span></span>|  
|`ManifestDriveIdMismatch`|<span data-ttu-id="7b008-243">hello hello 資訊清單檔中的識別碼不符合的 hello 一個讀取 hello 磁碟機的磁碟機。</span><span class="sxs-lookup"><span data-stu-id="7b008-243">hello drive ID in hello manifest file does not match hello one read from hello drive.</span></span>|  
|`ReadManifestFailed`|<span data-ttu-id="7b008-244">Hello 資訊清單讀取時發生磁碟 I/O 失敗。</span><span class="sxs-lookup"><span data-stu-id="7b008-244">A disk I/O failure occurred while reading from hello manifest.</span></span>|  
|`BlobListFormatInvalid`|<span data-ttu-id="7b008-245">hello 匯出 blob 清單 blob 不符合 toohello 所需的格式。</span><span class="sxs-lookup"><span data-stu-id="7b008-245">hello export blob list blob does not conform toohello required format.</span></span>|  
|`BlobRequestForbidden`|<span data-ttu-id="7b008-246">禁止存取 toohello blob hello 儲存體帳戶中。</span><span class="sxs-lookup"><span data-stu-id="7b008-246">Access toohello blobs in hello storage account is forbidden.</span></span> <span data-ttu-id="7b008-247">這可能是由於 tooinvalid 儲存體帳戶金鑰或容器 SAS。</span><span class="sxs-lookup"><span data-stu-id="7b008-247">This might be due tooinvalid storage account key or container SAS.</span></span>|  
|`InternalError`|<span data-ttu-id="7b008-248">和處理 hello 磁碟機時發生內部錯誤。</span><span class="sxs-lookup"><span data-stu-id="7b008-248">And internal error occurred while processing hello drive.</span></span>|  
  
## <a name="blob-status-codes"></a><span data-ttu-id="7b008-249">Blob 狀態碼</span><span class="sxs-lookup"><span data-stu-id="7b008-249">Blob status codes</span></span>  
<span data-ttu-id="7b008-250">hello 下表列出處理 blob hello 狀態碼。</span><span class="sxs-lookup"><span data-stu-id="7b008-250">hello following table lists hello status codes for processing a blob.</span></span>  
  
|<span data-ttu-id="7b008-251">狀態碼</span><span class="sxs-lookup"><span data-stu-id="7b008-251">Status code</span></span>|<span data-ttu-id="7b008-252">說明</span><span class="sxs-lookup"><span data-stu-id="7b008-252">Description</span></span>|  
|-----------------|-----------------|  
|`Completed`|<span data-ttu-id="7b008-253">hello blob 已完成處理，沒有錯誤。</span><span class="sxs-lookup"><span data-stu-id="7b008-253">hello blob has finished processing without errors.</span></span>|  
|`CompletedWithErrors`|<span data-ttu-id="7b008-254">hello blob 已完成處理，但其中一個或多個頁面範圍或區塊、 中繼資料或屬性中的錯誤。</span><span class="sxs-lookup"><span data-stu-id="7b008-254">hello blob has finished processing with errors in one or more page ranges or blocks, metadata, or properties.</span></span>|  
|`FileNameInvalid`|<span data-ttu-id="7b008-255">hello 檔案名稱無效。</span><span class="sxs-lookup"><span data-stu-id="7b008-255">hello file name is invalid.</span></span>|  
|`FileNameTooLong`|<span data-ttu-id="7b008-256">hello 檔案名稱過長。</span><span class="sxs-lookup"><span data-stu-id="7b008-256">hello file name is too long.</span></span>|  
|`FileNotFound`|<span data-ttu-id="7b008-257">找不到 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="7b008-257">hello file is not found.</span></span>|  
|`FileAccessDenied`|<span data-ttu-id="7b008-258">拒絕存取 toohello 檔案。</span><span class="sxs-lookup"><span data-stu-id="7b008-258">Access toohello file is denied.</span></span>|  
|`BlobRequestFailed`|<span data-ttu-id="7b008-259">hello tooaccess hello blob 的 Blob 服務要求失敗。</span><span class="sxs-lookup"><span data-stu-id="7b008-259">hello Blob service request tooaccess hello blob has failed.</span></span>|  
|`BlobRequestForbidden`|<span data-ttu-id="7b008-260">禁止 hello tooaccess hello blob 的 Blob 服務要求。</span><span class="sxs-lookup"><span data-stu-id="7b008-260">hello Blob service request tooaccess hello blob is forbidden.</span></span> <span data-ttu-id="7b008-261">這可能是由於 tooinvalid 儲存體帳戶金鑰或容器 SAS。</span><span class="sxs-lookup"><span data-stu-id="7b008-261">This might be due tooinvalid storage account key or container SAS.</span></span>|  
|`RenameFailed`|<span data-ttu-id="7b008-262">無法 toorename hello blob （用於匯入工作） 或 hello 檔案 （適用於匯出工作）。</span><span class="sxs-lookup"><span data-stu-id="7b008-262">Failed toorename hello blob (for an import job) or hello file (for an export job).</span></span>|  
|`BlobUnexpectedChange`|<span data-ttu-id="7b008-263">Hello blob （用於匯出工作） 發生未預期的變更。</span><span class="sxs-lookup"><span data-stu-id="7b008-263">An unexpected change has occurred with hello blob (for an export job).</span></span>|  
|`LeasePresent`|<span data-ttu-id="7b008-264">沒有 hello blob 上出現租用。</span><span class="sxs-lookup"><span data-stu-id="7b008-264">There is a lease present on hello blob.</span></span>|  
|`IOFailed`|<span data-ttu-id="7b008-265">處理 hello blob 時發生磁碟或網路 I/O 失敗。</span><span class="sxs-lookup"><span data-stu-id="7b008-265">A disk or network I/O failure occurred while processing hello blob.</span></span>|  
|`Failed`|<span data-ttu-id="7b008-266">處理 hello blob 時發生未知的失敗。</span><span class="sxs-lookup"><span data-stu-id="7b008-266">An unknown failure occurred while processing hello blob.</span></span>|  
  
## <a name="import-disposition-status-codes"></a><span data-ttu-id="7b008-267">匯入配置狀態碼</span><span class="sxs-lookup"><span data-stu-id="7b008-267">Import disposition status codes</span></span>  
<span data-ttu-id="7b008-268">hello 下表列出解決匯入配置 hello 狀態碼。</span><span class="sxs-lookup"><span data-stu-id="7b008-268">hello following table lists hello status codes for resolving an import disposition.</span></span>  
  
|<span data-ttu-id="7b008-269">狀態碼</span><span class="sxs-lookup"><span data-stu-id="7b008-269">Status code</span></span>|<span data-ttu-id="7b008-270">說明</span><span class="sxs-lookup"><span data-stu-id="7b008-270">Description</span></span>|  
|-----------------|-----------------|  
|`Created`|<span data-ttu-id="7b008-271">已建立 hello blob。</span><span class="sxs-lookup"><span data-stu-id="7b008-271">hello blob has been created.</span></span>|  
|`Renamed`|<span data-ttu-id="7b008-272">hello blob 已重新命名每個重新命名匯入配置。</span><span class="sxs-lookup"><span data-stu-id="7b008-272">hello blob has been renamed per rename import disposition.</span></span> <span data-ttu-id="7b008-273">hello`Blob/BlobPath`元素包含 hello URI hello 重新命名 blob。</span><span class="sxs-lookup"><span data-stu-id="7b008-273">hello `Blob/BlobPath` element contains hello URI for hello renamed blob.</span></span>|  
|`Skipped`|<span data-ttu-id="7b008-274">每個已略過 hello blob`no-overwrite`匯入配置。</span><span class="sxs-lookup"><span data-stu-id="7b008-274">hello blob has been skipped per `no-overwrite` import disposition.</span></span>|  
|`Overwritten`|<span data-ttu-id="7b008-275">hello blob 已覆寫現有的 blob，每個`overwrite`匯入配置。</span><span class="sxs-lookup"><span data-stu-id="7b008-275">hello blob has overwritten an existing blob per `overwrite` import disposition.</span></span>|  
|`Cancelled`|<span data-ttu-id="7b008-276">先前的失敗已停止進一步處理 hello 匯入配置。</span><span class="sxs-lookup"><span data-stu-id="7b008-276">A prior failure has stopped further processing of hello import disposition.</span></span>|  
  
## <a name="page-rangeblock-status-codes"></a><span data-ttu-id="7b008-277">頁面範圍/區塊狀態碼</span><span class="sxs-lookup"><span data-stu-id="7b008-277">Page range/block status codes</span></span>  
<span data-ttu-id="7b008-278">hello 下表列出處理頁面範圍或區塊 hello 狀態碼。</span><span class="sxs-lookup"><span data-stu-id="7b008-278">hello following table lists hello status codes for processing a page range or a block.</span></span>  
  
|<span data-ttu-id="7b008-279">狀態碼</span><span class="sxs-lookup"><span data-stu-id="7b008-279">Status code</span></span>|<span data-ttu-id="7b008-280">說明</span><span class="sxs-lookup"><span data-stu-id="7b008-280">Description</span></span>|  
|-----------------|-----------------|  
|`Completed`|<span data-ttu-id="7b008-281">hello 頁面範圍或區塊已完成處理，沒有任何錯誤。</span><span class="sxs-lookup"><span data-stu-id="7b008-281">hello page range or block has finished processing without any errors.</span></span>|  
|`Committed`|<span data-ttu-id="7b008-282">hello 區塊已認可，但不是在 hello 完整區塊清單，因為其他區塊失敗，或放置完整區塊清單本身失敗。</span><span class="sxs-lookup"><span data-stu-id="7b008-282">hello block has been committed,  but not in hello full block list because other blocks have failed, or put full block list itself has failed.</span></span>|  
|`Uncommitted`|<span data-ttu-id="7b008-283">hello 區塊是上傳，但尚未認可。</span><span class="sxs-lookup"><span data-stu-id="7b008-283">hello block is uploaded but not committed.</span></span>|  
|`Corrupted`|<span data-ttu-id="7b008-284">hello 頁面範圍或區塊已損毀 （hello 內容不符合其雜湊）。</span><span class="sxs-lookup"><span data-stu-id="7b008-284">hello page range or block is corrupted (hello content does not match its hash).</span></span>|  
|`FileUnexpectedEnd`|<span data-ttu-id="7b008-285">發現非預期的檔案結尾。</span><span class="sxs-lookup"><span data-stu-id="7b008-285">An unexpected end of file has been encountered.</span></span>|  
|`BlobUnexpectedEnd`|<span data-ttu-id="7b008-286">發現非預期的 Blob 結尾。</span><span class="sxs-lookup"><span data-stu-id="7b008-286">An unexpected end of blob has been encountered.</span></span>|  
|`BlobRequestFailed`|<span data-ttu-id="7b008-287">hello Blob 服務要求 tooaccess hello 頁面範圍或區塊已失敗。</span><span class="sxs-lookup"><span data-stu-id="7b008-287">hello Blob service request tooaccess hello page range or block has failed.</span></span>|  
|`IOFailed`|<span data-ttu-id="7b008-288">處理 hello 頁面範圍或區塊時發生磁碟或網路 I/O 失敗。</span><span class="sxs-lookup"><span data-stu-id="7b008-288">A disk or network I/O failure occurred while processing hello page range or block.</span></span>|  
|`Failed`|<span data-ttu-id="7b008-289">處理 hello 頁面範圍或區塊時發生未知的失敗。</span><span class="sxs-lookup"><span data-stu-id="7b008-289">An unknown failure occurred while processing hello page range or block.</span></span>|  
|`Cancelled`|<span data-ttu-id="7b008-290">先前的失敗已停止進一步處理 hello 頁面範圍或區塊。</span><span class="sxs-lookup"><span data-stu-id="7b008-290">A prior failure has stopped further processing of hello page range or block.</span></span>|  
  
## <a name="metadata-status-codes"></a><span data-ttu-id="7b008-291">中繼資料狀態碼</span><span class="sxs-lookup"><span data-stu-id="7b008-291">Metadata status codes</span></span>  
<span data-ttu-id="7b008-292">hello 下表列出處理 blob 中繼資料的 hello 狀態碼。</span><span class="sxs-lookup"><span data-stu-id="7b008-292">hello following table lists hello status codes for processing blob metadata.</span></span>  
  
|<span data-ttu-id="7b008-293">狀態碼</span><span class="sxs-lookup"><span data-stu-id="7b008-293">Status code</span></span>|<span data-ttu-id="7b008-294">說明</span><span class="sxs-lookup"><span data-stu-id="7b008-294">Description</span></span>|  
|-----------------|-----------------|  
|`Completed`|<span data-ttu-id="7b008-295">hello 中繼資料已完成處理，沒有錯誤。</span><span class="sxs-lookup"><span data-stu-id="7b008-295">hello metadata has finished processing without errors.</span></span>|  
|`FileNameInvalid`|<span data-ttu-id="7b008-296">hello 中繼資料檔案名稱無效。</span><span class="sxs-lookup"><span data-stu-id="7b008-296">hello metadata file name is invalid.</span></span>|  
|`FileNameTooLong`|<span data-ttu-id="7b008-297">hello 中繼資料檔案名稱過長。</span><span class="sxs-lookup"><span data-stu-id="7b008-297">hello metadata file name is too long.</span></span>|  
|`FileNotFound`|<span data-ttu-id="7b008-298">找不到 hello 中繼資料檔案。</span><span class="sxs-lookup"><span data-stu-id="7b008-298">hello metadata file is not found.</span></span>|  
|`FileAccessDenied`|<span data-ttu-id="7b008-299">拒絕存取 toohello 中繼資料檔案。</span><span class="sxs-lookup"><span data-stu-id="7b008-299">Access toohello metadata file is denied.</span></span>|  
|`Corrupted`|<span data-ttu-id="7b008-300">hello 中繼資料檔案已損毀 （hello 內容不符合其雜湊）。</span><span class="sxs-lookup"><span data-stu-id="7b008-300">hello metadata file is corrupted (hello content does not match its hash).</span></span>|  
|`XmlReadFailed`|<span data-ttu-id="7b008-301">hello 中繼資料內容不符合 toohello 所需的格式。</span><span class="sxs-lookup"><span data-stu-id="7b008-301">hello metadata content does not conform toohello required format.</span></span>|  
|`XmlWriteFailed`|<span data-ttu-id="7b008-302">撰寫 hello 中繼資料 XML 失敗。</span><span class="sxs-lookup"><span data-stu-id="7b008-302">Writing hello metadata XML has failed.</span></span>|  
|`BlobRequestFailed`|<span data-ttu-id="7b008-303">hello tooaccess hello 中繼資料的 Blob 服務要求失敗。</span><span class="sxs-lookup"><span data-stu-id="7b008-303">hello Blob service request tooaccess hello metadata has failed.</span></span>|  
|`IOFailed`|<span data-ttu-id="7b008-304">處理 hello 中繼資料時發生磁碟或網路 I/O 失敗。</span><span class="sxs-lookup"><span data-stu-id="7b008-304">A disk or network I/O failure occurred while processing hello metadata.</span></span>|  
|`Failed`|<span data-ttu-id="7b008-305">處理 hello 中繼資料時發生未知的失敗。</span><span class="sxs-lookup"><span data-stu-id="7b008-305">An unknown failure occurred while processing hello metadata.</span></span>|  
|`Cancelled`|<span data-ttu-id="7b008-306">先前的失敗已停止進一步處理 hello 中繼資料。</span><span class="sxs-lookup"><span data-stu-id="7b008-306">A prior failure has stopped further processing of hello metadata.</span></span>|  
  
## <a name="properties-status-codes"></a><span data-ttu-id="7b008-307">屬性狀態碼</span><span class="sxs-lookup"><span data-stu-id="7b008-307">Properties status codes</span></span>  
<span data-ttu-id="7b008-308">hello 下表列出處理 blob 屬性 hello 狀態碼。</span><span class="sxs-lookup"><span data-stu-id="7b008-308">hello following table lists hello status codes for processing blob properties.</span></span>  
  
|<span data-ttu-id="7b008-309">狀態碼</span><span class="sxs-lookup"><span data-stu-id="7b008-309">Status code</span></span>|<span data-ttu-id="7b008-310">說明</span><span class="sxs-lookup"><span data-stu-id="7b008-310">Description</span></span>|  
|-----------------|-----------------|  
|`Completed`|<span data-ttu-id="7b008-311">hello 屬性已完成處理，沒有任何錯誤。</span><span class="sxs-lookup"><span data-stu-id="7b008-311">hello properties have finished processing without any errors.</span></span>|  
|`FileNameInvalid`|<span data-ttu-id="7b008-312">hello 屬性檔名稱無效。</span><span class="sxs-lookup"><span data-stu-id="7b008-312">hello properties file name is invalid.</span></span>|  
|`FileNameTooLong`|<span data-ttu-id="7b008-313">hello 屬性檔名稱過長。</span><span class="sxs-lookup"><span data-stu-id="7b008-313">hello properties file name is too long.</span></span>|  
|`FileNotFound`|<span data-ttu-id="7b008-314">找不到 hello 屬性檔。</span><span class="sxs-lookup"><span data-stu-id="7b008-314">hello properties file is not found.</span></span>|  
|`FileAccessDenied`|<span data-ttu-id="7b008-315">拒絕存取 toohello 屬性檔。</span><span class="sxs-lookup"><span data-stu-id="7b008-315">Access toohello properties file is denied.</span></span>|  
|`Corrupted`|<span data-ttu-id="7b008-316">hello 屬性檔已損毀 （hello 內容不符合其雜湊）。</span><span class="sxs-lookup"><span data-stu-id="7b008-316">hello properties file is corrupted (hello content does not match its hash).</span></span>|  
|`XmlReadFailed`|<span data-ttu-id="7b008-317">hello 屬性內容不符合 toohello 所需的格式。</span><span class="sxs-lookup"><span data-stu-id="7b008-317">hello properties content does not conform toohello required format.</span></span>|  
|`XmlWriteFailed`|<span data-ttu-id="7b008-318">寫入 hello 屬性 XML 失敗。</span><span class="sxs-lookup"><span data-stu-id="7b008-318">Writing hello properties XML has failed.</span></span>|  
|`BlobRequestFailed`|<span data-ttu-id="7b008-319">hello tooaccess hello 屬性的 Blob 服務要求失敗。</span><span class="sxs-lookup"><span data-stu-id="7b008-319">hello Blob service request tooaccess hello properties has failed.</span></span>|  
|`IOFailed`|<span data-ttu-id="7b008-320">處理 hello 屬性時發生磁碟或網路 I/O 失敗。</span><span class="sxs-lookup"><span data-stu-id="7b008-320">A disk or network I/O failure occurred while processing hello properties.</span></span>|  
|`Failed`|<span data-ttu-id="7b008-321">處理 hello 屬性時發生未知的失敗。</span><span class="sxs-lookup"><span data-stu-id="7b008-321">An unknown failure occurred while processing hello properties.</span></span>|  
|`Cancelled`|<span data-ttu-id="7b008-322">先前的失敗已停止進一步處理 hello 屬性。</span><span class="sxs-lookup"><span data-stu-id="7b008-322">A prior failure has stopped further processing of hello properties.</span></span>|  
  
## <a name="sample-logs"></a><span data-ttu-id="7b008-323">範例記錄</span><span class="sxs-lookup"><span data-stu-id="7b008-323">Sample logs</span></span>  
<span data-ttu-id="7b008-324">hello 下列是範例的詳細資訊記錄檔。</span><span class="sxs-lookup"><span data-stu-id="7b008-324">hello following is an example of verbose log.</span></span>  
  
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
  
<span data-ttu-id="7b008-325">hello 對應錯誤記錄檔如下所示。</span><span class="sxs-lookup"><span data-stu-id="7b008-325">hello corresponding error log is shown below.</span></span>  
  
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

 <span data-ttu-id="7b008-326">匯入工作的 hello 後續錯誤記錄檔包含 hello 匯入磁碟機上找不到檔案的相關錯誤。</span><span class="sxs-lookup"><span data-stu-id="7b008-326">hello follow error log for an import job contains an error about a file not found on hello import drive.</span></span> <span data-ttu-id="7b008-327">請注意，後續元件 hello 狀態`Cancelled`。</span><span class="sxs-lookup"><span data-stu-id="7b008-327">Note that hello status of subsequent components is `Cancelled`.</span></span>  
  
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

<span data-ttu-id="7b008-328">hello 下列的錯誤記錄檔，匯出工作的表示，hello blob 內容已成功寫入 toohello 磁碟機，但匯出 hello blob 的內容時，發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="7b008-328">hello following error log for an export job indicates that hello blob content has been successfully written toohello drive, but that an error occurred while exporting hello blob's properties.</span></span>  
  
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
  
## <a name="next-steps"></a><span data-ttu-id="7b008-329">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7b008-329">Next steps</span></span>
 
* [<span data-ttu-id="7b008-330">儲存體匯入/匯出 REST API</span><span class="sxs-lookup"><span data-stu-id="7b008-330">Storage Import/Export REST API</span></span>](/rest/api/storageimportexport/)
