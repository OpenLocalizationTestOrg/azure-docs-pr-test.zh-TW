---
title: "Azure 匯入/匯出匯入工作-v1 aaaRepairing |Microsoft 文件"
description: "了解如何匯入工作，所建立及執行使用 toorepair hello Azure 匯入/匯出服務。"
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
ms.openlocfilehash: a9ed81f50cffd8ae6e0cb21b25a04815c2b51ee5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="repairing-an-import-job"></a><span data-ttu-id="b930f-103">修復匯入作業</span><span class="sxs-lookup"><span data-stu-id="b930f-103">Repairing an import job</span></span>
<span data-ttu-id="b930f-104">hello Microsoft Azure 匯入/匯出服務可能會失敗 toocopy 一些檔案或檔案 toohello Windows Azure Blob 服務的部分。</span><span class="sxs-lookup"><span data-stu-id="b930f-104">hello Microsoft Azure Import/Export service may fail toocopy some of your files or parts of a file toohello Windows Azure Blob service.</span></span> <span data-ttu-id="b930f-105">部分的失敗原因包括︰</span><span class="sxs-lookup"><span data-stu-id="b930f-105">Some reasons for failures include:</span></span>  
  
-   <span data-ttu-id="b930f-106">損毀的檔案</span><span class="sxs-lookup"><span data-stu-id="b930f-106">Corrupted files</span></span>  
  
-   <span data-ttu-id="b930f-107">損壞的磁碟機</span><span class="sxs-lookup"><span data-stu-id="b930f-107">Damaged drives</span></span>  
  
-   <span data-ttu-id="b930f-108">在傳輸 hello 檔案時，變更 hello 儲存體帳戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="b930f-108">hello storage account key changed while hello file was being transferred.</span></span>  
  
<span data-ttu-id="b930f-109">您可以執行 hello Microsoft Azure 匯入/匯出工具與 hello 匯入作業的複製記錄檔，而且 hello 工具都會將上傳 hello 遺失的檔案 （或檔案的部分） tooyour Windows Azure 儲存體帳戶 toocomplete 匯入工作。</span><span class="sxs-lookup"><span data-stu-id="b930f-109">You can run hello Microsoft Azure Import/Export Tool with hello import job's copy log files, and hello tool will upload hello missing files (or parts of a file) tooyour Windows Azure storage account toocomplete import job.</span></span>  
  
## <a name="repairimport-parameters"></a><span data-ttu-id="b930f-110">RepairImport 參數</span><span class="sxs-lookup"><span data-stu-id="b930f-110">RepairImport parameters</span></span>

<span data-ttu-id="b930f-111">hello 指定下列參數可以與**RepairImport**:</span><span class="sxs-lookup"><span data-stu-id="b930f-111">hello following parameters can be specified with **RepairImport**:</span></span> 
  
|||  
|-|-|  
|<span data-ttu-id="b930f-112">**/r:**<RepairFile\></span><span class="sxs-lookup"><span data-stu-id="b930f-112">**/r:**<RepairFile\></span></span>|<span data-ttu-id="b930f-113">**必要。**</span><span class="sxs-lookup"><span data-stu-id="b930f-113">**Required.**</span></span> <span data-ttu-id="b930f-114">路徑 toohello 修復檔案，追蹤 hello hello 修復進度，並可讓您 tooresume 中斷的修復。</span><span class="sxs-lookup"><span data-stu-id="b930f-114">Path toohello repair file, which tracks hello progress of hello repair, and allows you tooresume an interrupted repair.</span></span> <span data-ttu-id="b930f-115">每個磁碟機需要一個修復檔案，而且只能有一個。</span><span class="sxs-lookup"><span data-stu-id="b930f-115">Each drive must have one and only one repair file.</span></span> <span data-ttu-id="b930f-116">當您開始在給定的磁碟機的修復時，您將會傳入 hello 路徑 tooa 修復檔案尚不存在。</span><span class="sxs-lookup"><span data-stu-id="b930f-116">When you start a repair for a given drive, you will pass in hello path tooa repair file which does not yet exist.</span></span> <span data-ttu-id="b930f-117">tooresume 中斷的修復，您應傳入 hello 現有的修復檔名稱。</span><span class="sxs-lookup"><span data-stu-id="b930f-117">tooresume an interrupted repair, you should pass in hello name of an existing repair file.</span></span> <span data-ttu-id="b930f-118">一律必須指定 hello 修復檔案對應 toohello 目標磁碟機。</span><span class="sxs-lookup"><span data-stu-id="b930f-118">hello repair file corresponding toohello target drive must always be specified.</span></span>|  
|<span data-ttu-id="b930f-119">**/logdir:**<LogDirectory\></span><span class="sxs-lookup"><span data-stu-id="b930f-119">**/logdir:**<LogDirectory\></span></span>|<span data-ttu-id="b930f-120">**選用。**</span><span class="sxs-lookup"><span data-stu-id="b930f-120">**Optional.**</span></span> <span data-ttu-id="b930f-121">hello 記錄檔目錄。</span><span class="sxs-lookup"><span data-stu-id="b930f-121">hello log directory.</span></span> <span data-ttu-id="b930f-122">詳細資訊記錄檔會寫入 toothis 目錄。</span><span class="sxs-lookup"><span data-stu-id="b930f-122">Verbose log files will be written toothis directory.</span></span> <span data-ttu-id="b930f-123">如果未不指定任何記錄檔目錄，則 hello 目前的目錄會用作 hello 記錄檔目錄。</span><span class="sxs-lookup"><span data-stu-id="b930f-123">If no log directory is specified, hello current directory will be used as hello log directory.</span></span>|  
|<span data-ttu-id="b930f-124">**/d:**<TargetDirectories\></span><span class="sxs-lookup"><span data-stu-id="b930f-124">**/d:**<TargetDirectories\></span></span>|<span data-ttu-id="b930f-125">**必要。**</span><span class="sxs-lookup"><span data-stu-id="b930f-125">**Required.**</span></span> <span data-ttu-id="b930f-126">一或多個以分號分隔目錄，其中包含 hello 原始匯入的檔案。</span><span class="sxs-lookup"><span data-stu-id="b930f-126">One or more semicolon-separated directories that contain hello original files that were imported.</span></span> <span data-ttu-id="b930f-127">hello 匯入磁碟機也可以使用，但如果原始檔的替代位置可用，就不需要。</span><span class="sxs-lookup"><span data-stu-id="b930f-127">hello import drive may also be used, but is not required if alternate locations of original files are available.</span></span>|  
|<span data-ttu-id="b930f-128">**/bk:**<BitLockerKey\></span><span class="sxs-lookup"><span data-stu-id="b930f-128">**/bk:**<BitLockerKey\></span></span>|<span data-ttu-id="b930f-129">**選用。**</span><span class="sxs-lookup"><span data-stu-id="b930f-129">**Optional.**</span></span> <span data-ttu-id="b930f-130">如果您想 hello 工具 toounlock 有可用 hello 原始的檔案加密的磁碟機，您應該指定 hello BitLocker 金鑰。</span><span class="sxs-lookup"><span data-stu-id="b930f-130">You should specify hello BitLocker key if you want hello tool toounlock an encrypted drive where hello original files are available.</span></span>|  
|<span data-ttu-id="b930f-131">**/sn:**<StorageAccountName\></span><span class="sxs-lookup"><span data-stu-id="b930f-131">**/sn:**<StorageAccountName\></span></span>|<span data-ttu-id="b930f-132">**必要。**</span><span class="sxs-lookup"><span data-stu-id="b930f-132">**Required.**</span></span> <span data-ttu-id="b930f-133">hello 名稱 hello hello 儲存體帳戶匯入作業。</span><span class="sxs-lookup"><span data-stu-id="b930f-133">hello name of hello storage account for hello import job.</span></span>|  
|<span data-ttu-id="b930f-134">**/sk:**<StorageAccountKey\></span><span class="sxs-lookup"><span data-stu-id="b930f-134">**/sk:**<StorageAccountKey\></span></span>|<span data-ttu-id="b930f-135">如果未指定 (且只有在未指定) 容器 SAS 時，才是**必要**參數。</span><span class="sxs-lookup"><span data-stu-id="b930f-135">**Required** if and only if a container SAS is not specified.</span></span> <span data-ttu-id="b930f-136">hello hello hello 的儲存體帳戶的帳戶金鑰匯入作業。</span><span class="sxs-lookup"><span data-stu-id="b930f-136">hello account key for hello storage account for hello import job.</span></span>|  
|<span data-ttu-id="b930f-137">**/csas:**<ContainerSas\></span><span class="sxs-lookup"><span data-stu-id="b930f-137">**/csas:**<ContainerSas\></span></span>|<span data-ttu-id="b930f-138">**需要**如果且只有未指定 hello 儲存體帳戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="b930f-138">**Required** if and only if hello storage account key is not specified.</span></span> <span data-ttu-id="b930f-139">用於存取與 hello 匯入工作相關聯的 hello blob hello 容器 SAS。</span><span class="sxs-lookup"><span data-stu-id="b930f-139">hello container SAS for accessing hello blobs associated with hello import job.</span></span>|  
|<span data-ttu-id="b930f-140">**/CopyLogFile:**<DriveCopyLogFile\></span><span class="sxs-lookup"><span data-stu-id="b930f-140">**/CopyLogFile:**<DriveCopyLogFile\></span></span>|<span data-ttu-id="b930f-141">**必要。**</span><span class="sxs-lookup"><span data-stu-id="b930f-141">**Required.**</span></span> <span data-ttu-id="b930f-142">路徑 toohello 磁碟機複製記錄檔 （詳細資訊記錄檔或錯誤記錄檔）。</span><span class="sxs-lookup"><span data-stu-id="b930f-142">Path toohello drive copy log file (either verbose log or error log).</span></span> <span data-ttu-id="b930f-143">hello 檔案 hello Windows Azure 匯入/匯出服務所產生，並可從 hello 與 hello 工作相關聯的 blob 儲存體下載。</span><span class="sxs-lookup"><span data-stu-id="b930f-143">hello file is generated by hello Windows Azure Import/Export service and can be downloaded from hello blob storage associated with hello job.</span></span> <span data-ttu-id="b930f-144">hello 複製記錄檔包含失敗的 blob 或檔案，也就是 toobe 修復的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="b930f-144">hello copy log file contains information about failed blobs or files which are toobe repaired.</span></span>|  
|<span data-ttu-id="b930f-145">**/PathMapFile:**<DrivePathMapFile\></span><span class="sxs-lookup"><span data-stu-id="b930f-145">**/PathMapFile:**<DrivePathMapFile\></span></span>|<span data-ttu-id="b930f-146">**選用。**</span><span class="sxs-lookup"><span data-stu-id="b930f-146">**Optional.**</span></span> <span data-ttu-id="b930f-147">可用的路徑 tooa 文字檔案 tooresolve 語意模糊，如果您有多個檔案，以相同的名稱，您已匯入中的 hello hello 相同的作業。</span><span class="sxs-lookup"><span data-stu-id="b930f-147">Path tooa text file that can be used tooresolve ambiguities if you have multiple files with hello same name that you were importing in hello same job.</span></span> <span data-ttu-id="b930f-148">hello 第一個階段 hello 工具執行時，它可以填入此檔案的所有 hello 模稜兩可的名稱。</span><span class="sxs-lookup"><span data-stu-id="b930f-148">hello first time hello tool is run, it can populate this file with all of hello ambiguous names.</span></span> <span data-ttu-id="b930f-149">後續的執行中的 hello 工具將會使用此檔案 tooresolve hello 模稜兩可。</span><span class="sxs-lookup"><span data-stu-id="b930f-149">Subsequent runs of hello tool will use this file tooresolve hello ambiguities.</span></span>|  
  
## <a name="using-hello-repairimport-command"></a><span data-ttu-id="b930f-150">使用 hello RepairImport 命令</span><span class="sxs-lookup"><span data-stu-id="b930f-150">Using hello RepairImport command</span></span>  
<span data-ttu-id="b930f-151">toorepair hello 網路透過串流處理 hello 資料匯入資料，您必須指定 hello 目錄，其中包含已匯入使用 hello 原始檔案 hello`/d`參數。</span><span class="sxs-lookup"><span data-stu-id="b930f-151">toorepair import data by streaming hello data over hello network, you must specify hello directories that contain hello original files you were importing using hello `/d` parameter.</span></span> <span data-ttu-id="b930f-152">您也必須指定您從儲存體帳戶下載的 hello 複製記錄檔。</span><span class="sxs-lookup"><span data-stu-id="b930f-152">You must also specify hello copy log file that you downloaded from your storage account.</span></span> <span data-ttu-id="b930f-153">一般命令列 toorepair 部分失敗之匯入工作看起來像：</span><span class="sxs-lookup"><span data-stu-id="b930f-153">A typical command line toorepair an import job with partial failures looks like:</span></span>  
  
```  
WAImportExport.exe RepairImport /r:C:\WAImportExport\9WM35C2V.rep /d:C:\Users\bob\Pictures;X:\BobBackup\photos /sn:bobmediaaccount /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /CopyLogFile:C:\WAImportExport\9WM35C2V.log  
```  
  
<span data-ttu-id="b930f-154">hello 下列是複製記錄檔的範例。</span><span class="sxs-lookup"><span data-stu-id="b930f-154">hello following is an example of a copy log file.</span></span> <span data-ttu-id="b930f-155">在此情況下，其中有 64k 檔案的片段損毀的運送 hello 匯入工作的 hello 磁碟機上。</span><span class="sxs-lookup"><span data-stu-id="b930f-155">In this case, one 64K piece of a file was corrupted on hello drive that was shipped for hello import job.</span></span> <span data-ttu-id="b930f-156">由於這是 hello 只有失敗處，hello hello 作業中的 hello blob 的其餘部分已順利匯入。</span><span class="sxs-lookup"><span data-stu-id="b930f-156">Since this is hello only failure indicated, hello rest of hello blobs in hello job were successfully imported.</span></span>  
  
```xml
<?xml version="1.0" encoding="utf-8"?>  
<DriveLog>  
 <DriveId>9WM35C2V</DriveId>  
 <Blob Status="CompletedWithErrors">  
 <BlobPath>pictures/animals/koala.jpg</BlobPath>  
 <FilePath>\animals\koala.jpg</FilePath>  
 <Length>163840</Length>  
 <ImportDisposition Status="Overwritten">overwrite</ImportDisposition>  
 <PageRangeList>  
  <PageRange Offset="65536" Length="65536" Hash="AA2585F6F6FD01C4AD4256E018240CD4" Status="Corrupted" />  
 </PageRangeList>  
 </Blob>  
 <Status>CompletedWithErrors</Status>  
</DriveLog>  
```
  
<span data-ttu-id="b930f-157">當這個複製記錄傳遞 toohello Azure 匯入/匯出工具時，hello 工具會嘗試 toofinish hello 此檔案匯入透過 hello 網路複製遺漏 hello 的內容。</span><span class="sxs-lookup"><span data-stu-id="b930f-157">When this copy log is passed toohello Azure Import/Export Tool, hello tool will try toofinish hello import for this file by copying hello missing contents across hello network.</span></span> <span data-ttu-id="b930f-158">Hello 上述範例中，下列 hello 工具會尋找 hello 原始檔案`\animals\koala.jpg`hello 兩個目錄內`C:\Users\bob\Pictures`和`X:\BobBackup\photos`。</span><span class="sxs-lookup"><span data-stu-id="b930f-158">Following hello example above, hello tool will look for hello original file `\animals\koala.jpg` within hello two directories `C:\Users\bob\Pictures` and `X:\BobBackup\photos`.</span></span> <span data-ttu-id="b930f-159">如果 hello 檔案`C:\Users\bob\Pictures\animals\koala.jpg`存在，hello Azure 匯入/匯出工具將會複製 hello 遺漏的資料 toohello 對應的 blob 範圍`http://bobmediaaccount.blob.core.windows.net/pictures/animals/koala.jpg`。</span><span class="sxs-lookup"><span data-stu-id="b930f-159">If hello file `C:\Users\bob\Pictures\animals\koala.jpg` exists, hello Azure Import/Export Tool will copy hello missing range of data toohello corresponding blob `http://bobmediaaccount.blob.core.windows.net/pictures/animals/koala.jpg`.</span></span>  
  
## <a name="resolving-conflicts-when-using-repairimport"></a><span data-ttu-id="b930f-160">解決使用 RepairImport 時的衝突</span><span class="sxs-lookup"><span data-stu-id="b930f-160">Resolving conflicts when using RepairImport</span></span>  
<span data-ttu-id="b930f-161">在某些情況下，hello 工具可能會無法 toofind 或開啟 hello 所需的檔案，其中一個 hello 下列原因： 找不到 hello 檔案、 hello 檔案無法存取、 hello 檔案名稱模稜兩可，或 hello hello 檔案內容已不正確。</span><span class="sxs-lookup"><span data-stu-id="b930f-161">In some situations, hello tool may not be able toofind or open hello necessary file for one of hello following reasons: hello file could not be found, hello file is not accessible, hello file name is ambiguous, or hello content of hello file is no longer correct.</span></span>  
  
<span data-ttu-id="b930f-162">如果嘗試 toolocate hello 工具可能會發生模稜兩可的錯誤`\animals\koala.jpg`底下都同名的檔案且`C:\Users\bob\pictures`和`X:\BobBackup\photos`。</span><span class="sxs-lookup"><span data-stu-id="b930f-162">An ambiguous error could occur if hello tool is trying toolocate `\animals\koala.jpg` and there is a file with that name under both `C:\Users\bob\pictures` and `X:\BobBackup\photos`.</span></span> <span data-ttu-id="b930f-163">也就是說，兩者`C:\Users\bob\pictures\animals\koala.jpg`和`X:\BobBackup\photos\animals\koala.jpg`存在於 hello 匯入工作磁碟機上。</span><span class="sxs-lookup"><span data-stu-id="b930f-163">That is, both `C:\Users\bob\pictures\animals\koala.jpg` and `X:\BobBackup\photos\animals\koala.jpg` exist on hello import job drives.</span></span>  
  
<span data-ttu-id="b930f-164">hello`/PathMapFile`選項可以讓您 tooresolve 這些錯誤。</span><span class="sxs-lookup"><span data-stu-id="b930f-164">hello `/PathMapFile` option will allow you tooresolve these errors.</span></span> <span data-ttu-id="b930f-165">您可以指定 hello hello 檔案將包含 hello 清單的 hello 工具的檔案名稱不能 toocorrectly 識別。</span><span class="sxs-lookup"><span data-stu-id="b930f-165">You can specify hello name of hello file which will contains hello list of files that hello tool was not able toocorrectly identify.</span></span> <span data-ttu-id="b930f-166">hello 下列是命令列範例填入`9WM35C2V_pathmap.txt`:</span><span class="sxs-lookup"><span data-stu-id="b930f-166">hello following is an example command line that would populate `9WM35C2V_pathmap.txt`:</span></span>  
  
```
WAImportExport.exe RepairImport /r:C:\WAImportExport\9WM35C2V.rep /d:C:\Users\bob\Pictures;X:\BobBackup\photos /sn:bobmediaaccount /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /CopyLogFile:C:\WAImportExport\9WM35C2V.log /PathMapFile:C:\WAImportExport\9WM35C2V_pathmap.txt  
```
  
<span data-ttu-id="b930f-167">hello 工具接著將要撰寫 hello 有問題的檔案路徑太`9WM35C2V_pathmap.txt`，其中在每一行。</span><span class="sxs-lookup"><span data-stu-id="b930f-167">hello tool will then write hello problematic file paths too`9WM35C2V_pathmap.txt`, one on each line.</span></span> <span data-ttu-id="b930f-168">比方說，hello 檔案可能包含下列項目執行 hello 命令之後的 hello:</span><span class="sxs-lookup"><span data-stu-id="b930f-168">For instance, hello file may contain hello following entries after running hello command:</span></span>  
 
```
\animals\koala.jpg  
\animals\kangaroo.jpg  
```
  
 <span data-ttu-id="b930f-169">Hello 清單中每個檔案，您應該嘗試 toolocate 並開啟 hello 檔案 tooensure 是可用 toohello 工具。</span><span class="sxs-lookup"><span data-stu-id="b930f-169">For each file in hello list, you should attempt toolocate and open hello file tooensure it is available toohello tool.</span></span> <span data-ttu-id="b930f-170">如果您想 tootell hello 工具明確其中 toofind 檔案，您可以修改 hello 路徑對應檔案，再新增 hello 路徑 tooeach 檔案上 hello 同一行，以 tab 字元分隔：</span><span class="sxs-lookup"><span data-stu-id="b930f-170">If you wish tootell hello tool explicitly where toofind a file, you can modify hello path map file and add hello path tooeach file on hello same line, separated by a tab character:</span></span>  
  
```
\animals\koala.jpg           C:\Users\bob\Pictures\animals\koala.jpg  
\animals\kangaroo.jpg        X:\BobBackup\photos\animals\kangaroo.jpg  
```
  
<span data-ttu-id="b930f-171">讓 hello 必要的檔案可用 toohello 工具或更新的 hello 路徑對應檔案之後, 您可以重新執行 hello 工具 toocomplete hello 匯入程序。</span><span class="sxs-lookup"><span data-stu-id="b930f-171">After making hello necessary files available toohello tool, or updating hello path map file, you can rerun hello tool toocomplete hello import process.</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="b930f-172">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b930f-172">Next steps</span></span>
 
* [<span data-ttu-id="b930f-173">正在設定 hello Azure 匯入/匯出工具</span><span class="sxs-lookup"><span data-stu-id="b930f-173">Setting Up hello Azure Import/Export Tool</span></span>](storage-import-export-tool-setup-v1.md)   
* [<span data-ttu-id="b930f-174">針對匯入作業準備硬碟</span><span class="sxs-lookup"><span data-stu-id="b930f-174">Preparing hard drives for an import job</span></span>](storage-import-export-tool-preparing-hard-drives-import-v1.md)   
* [<span data-ttu-id="b930f-175">利用複製記錄檔檢閱作業狀態</span><span class="sxs-lookup"><span data-stu-id="b930f-175">Reviewing job status with copy log files</span></span>](storage-import-export-tool-reviewing-job-status-v1.md)   
* [<span data-ttu-id="b930f-176">修復匯出作業</span><span class="sxs-lookup"><span data-stu-id="b930f-176">Repairing an export job</span></span>](storage-import-export-tool-repairing-an-export-job-v1.md)   
* [<span data-ttu-id="b930f-177">疑難排解 hello Azure 匯入/匯出工具</span><span class="sxs-lookup"><span data-stu-id="b930f-177">Troubleshooting hello Azure Import/Export Tool</span></span>](storage-import-export-tool-troubleshooting-v1.md)
