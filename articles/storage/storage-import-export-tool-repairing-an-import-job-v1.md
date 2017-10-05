---
title: "修復 Azure 匯入/匯出匯入作業 - v1 | Microsoft Docs"
description: "了解如何修復使用 Azure 匯入/匯出服務建立和執行的匯入作業。"
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
ms.openlocfilehash: b374eabcbafa6ffe64c639fb6c89be857ecfc221
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="repairing-an-import-job"></a><span data-ttu-id="544bc-103">修復匯入作業</span><span class="sxs-lookup"><span data-stu-id="544bc-103">Repairing an import job</span></span>
<span data-ttu-id="544bc-104">Microsoft Azure 匯入/匯出服務可能無法將某些檔案或某個檔案的部分複製到 Windows Azure Blob 服務。</span><span class="sxs-lookup"><span data-stu-id="544bc-104">The Microsoft Azure Import/Export service may fail to copy some of your files or parts of a file to the Windows Azure Blob service.</span></span> <span data-ttu-id="544bc-105">部分的失敗原因包括︰</span><span class="sxs-lookup"><span data-stu-id="544bc-105">Some reasons for failures include:</span></span>  
  
-   <span data-ttu-id="544bc-106">損毀的檔案</span><span class="sxs-lookup"><span data-stu-id="544bc-106">Corrupted files</span></span>  
  
-   <span data-ttu-id="544bc-107">損壞的磁碟機</span><span class="sxs-lookup"><span data-stu-id="544bc-107">Damaged drives</span></span>  
  
-   <span data-ttu-id="544bc-108">儲存體帳戶金鑰在傳輸檔案時變更。</span><span class="sxs-lookup"><span data-stu-id="544bc-108">The storage account key changed while the file was being transferred.</span></span>  
  
<span data-ttu-id="544bc-109">您可以使用匯入作業的複製記錄檔執行 Microsoft Azure 匯入/匯出工具，而此工具會將遺漏的檔案 (或檔案的部分) 上傳到您的 Windows Azure 儲存體帳戶，以完成匯入作業。</span><span class="sxs-lookup"><span data-stu-id="544bc-109">You can run the Microsoft Azure Import/Export Tool with the import job's copy log files, and the tool will upload the missing files (or parts of a file) to your Windows Azure storage account to complete import job.</span></span>  
  
## <a name="repairimport-parameters"></a><span data-ttu-id="544bc-110">RepairImport 參數</span><span class="sxs-lookup"><span data-stu-id="544bc-110">RepairImport parameters</span></span>

<span data-ttu-id="544bc-111">您可以搭配 **RepairImport** 指定下列參數：</span><span class="sxs-lookup"><span data-stu-id="544bc-111">The following parameters can be specified with **RepairImport**:</span></span> 
  
|||  
|-|-|  
|<span data-ttu-id="544bc-112">**/r:**<RepairFile\></span><span class="sxs-lookup"><span data-stu-id="544bc-112">**/r:**<RepairFile\></span></span>|<span data-ttu-id="544bc-113">**必要。**</span><span class="sxs-lookup"><span data-stu-id="544bc-113">**Required.**</span></span> <span data-ttu-id="544bc-114">修復檔案的路徑，可追蹤修復進度，並可讓您繼續中斷的修復。</span><span class="sxs-lookup"><span data-stu-id="544bc-114">Path to the repair file, which tracks the progress of the repair, and allows you to resume an interrupted repair.</span></span> <span data-ttu-id="544bc-115">每個磁碟機必須只能有一個修復檔案。</span><span class="sxs-lookup"><span data-stu-id="544bc-115">Each drive must have one and only one repair file.</span></span> <span data-ttu-id="544bc-116">當您啟動指定磁碟機的修復時，您將會傳入尚不存在之修復檔的路徑。</span><span class="sxs-lookup"><span data-stu-id="544bc-116">When you start a repair for a given drive, you will pass in the path to a repair file which does not yet exist.</span></span> <span data-ttu-id="544bc-117">若要恢復中斷的修復，您應傳入現有修復檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="544bc-117">To resume an interrupted repair, you should pass in the name of an existing repair file.</span></span> <span data-ttu-id="544bc-118">一律必須指定對應於目標磁碟機的修復檔。</span><span class="sxs-lookup"><span data-stu-id="544bc-118">The repair file corresponding to the target drive must always be specified.</span></span>|  
|<span data-ttu-id="544bc-119">**/logdir:**<LogDirectory\></span><span class="sxs-lookup"><span data-stu-id="544bc-119">**/logdir:**<LogDirectory\></span></span>|<span data-ttu-id="544bc-120">**選用。**</span><span class="sxs-lookup"><span data-stu-id="544bc-120">**Optional.**</span></span> <span data-ttu-id="544bc-121">記錄檔目錄。</span><span class="sxs-lookup"><span data-stu-id="544bc-121">The log directory.</span></span> <span data-ttu-id="544bc-122">詳細資訊記錄檔會寫入至這個目錄。</span><span class="sxs-lookup"><span data-stu-id="544bc-122">Verbose log files will be written to this directory.</span></span> <span data-ttu-id="544bc-123">如未指定記錄檔目錄，則會使用目前的目錄做為記錄檔目錄。</span><span class="sxs-lookup"><span data-stu-id="544bc-123">If no log directory is specified, the current directory will be used as the log directory.</span></span>|  
|<span data-ttu-id="544bc-124">**/d:**<TargetDirectories\></span><span class="sxs-lookup"><span data-stu-id="544bc-124">**/d:**<TargetDirectories\></span></span>|<span data-ttu-id="544bc-125">**必要。**</span><span class="sxs-lookup"><span data-stu-id="544bc-125">**Required.**</span></span> <span data-ttu-id="544bc-126">一或多個以分號分隔的目錄，其中包含所匯入的原始檔。</span><span class="sxs-lookup"><span data-stu-id="544bc-126">One or more semicolon-separated directories that contain the original files that were imported.</span></span> <span data-ttu-id="544bc-127">也可以使用匯入磁碟機，但如果有原始檔的替代位置可用，則非必要。</span><span class="sxs-lookup"><span data-stu-id="544bc-127">The import drive may also be used, but is not required if alternate locations of original files are available.</span></span>|  
|<span data-ttu-id="544bc-128">**/bk:**<BitLockerKey\></span><span class="sxs-lookup"><span data-stu-id="544bc-128">**/bk:**<BitLockerKey\></span></span>|<span data-ttu-id="544bc-129">**選用。**</span><span class="sxs-lookup"><span data-stu-id="544bc-129">**Optional.**</span></span> <span data-ttu-id="544bc-130">如果您希望該工具解除鎖定原始檔案所在的加密磁碟機，您應指定 BitLocker 金鑰。</span><span class="sxs-lookup"><span data-stu-id="544bc-130">You should specify the BitLocker key if you want the tool to unlock an encrypted drive where the original files are available.</span></span>|  
|<span data-ttu-id="544bc-131">**/sn:**<StorageAccountName\></span><span class="sxs-lookup"><span data-stu-id="544bc-131">**/sn:**<StorageAccountName\></span></span>|<span data-ttu-id="544bc-132">**必要。**</span><span class="sxs-lookup"><span data-stu-id="544bc-132">**Required.**</span></span> <span data-ttu-id="544bc-133">匯入作業的儲存體帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="544bc-133">The name of the storage account for the import job.</span></span>|  
|<span data-ttu-id="544bc-134">**/sk:**<StorageAccountKey\></span><span class="sxs-lookup"><span data-stu-id="544bc-134">**/sk:**<StorageAccountKey\></span></span>|<span data-ttu-id="544bc-135">如果未指定 (且只有在未指定) 容器 SAS 時，才是**必要**參數。</span><span class="sxs-lookup"><span data-stu-id="544bc-135">**Required** if and only if a container SAS is not specified.</span></span> <span data-ttu-id="544bc-136">匯入作業之儲存體帳戶的帳戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="544bc-136">The account key for the storage account for the import job.</span></span>|  
|<span data-ttu-id="544bc-137">**/csas:**<ContainerSas\></span><span class="sxs-lookup"><span data-stu-id="544bc-137">**/csas:**<ContainerSas\></span></span>|<span data-ttu-id="544bc-138">如果未指定 (且只有在未指定) 儲存體帳戶金鑰時，才是**必要**參數。</span><span class="sxs-lookup"><span data-stu-id="544bc-138">**Required** if and only if the storage account key is not specified.</span></span> <span data-ttu-id="544bc-139">存取與匯入作業相關聯的 Blob 所用的容器 SAS。</span><span class="sxs-lookup"><span data-stu-id="544bc-139">The container SAS for accessing the blobs associated with the import job.</span></span>|  
|<span data-ttu-id="544bc-140">**/CopyLogFile:**<DriveCopyLogFile\></span><span class="sxs-lookup"><span data-stu-id="544bc-140">**/CopyLogFile:**<DriveCopyLogFile\></span></span>|<span data-ttu-id="544bc-141">**必要。**</span><span class="sxs-lookup"><span data-stu-id="544bc-141">**Required.**</span></span> <span data-ttu-id="544bc-142">磁碟機複製記錄檔 (詳細資訊記錄檔或錯誤記錄檔) 的路徑。</span><span class="sxs-lookup"><span data-stu-id="544bc-142">Path to the drive copy log file (either verbose log or error log).</span></span> <span data-ttu-id="544bc-143">此檔案是由 Windows Azure 匯入/匯出服務所產生，您可以從與作業相關聯的 blob 儲存體下載。</span><span class="sxs-lookup"><span data-stu-id="544bc-143">The file is generated by the Windows Azure Import/Export service and can be downloaded from the blob storage associated with the job.</span></span> <span data-ttu-id="544bc-144">複製記錄檔包含所要修復之失敗 blob 或檔案的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="544bc-144">The copy log file contains information about failed blobs or files which are to be repaired.</span></span>|  
|<span data-ttu-id="544bc-145">**/PathMapFile:**<DrivePathMapFile\></span><span class="sxs-lookup"><span data-stu-id="544bc-145">**/PathMapFile:**<DrivePathMapFile\></span></span>|<span data-ttu-id="544bc-146">**選用。**</span><span class="sxs-lookup"><span data-stu-id="544bc-146">**Optional.**</span></span> <span data-ttu-id="544bc-147">如果您在相同作業中匯入多個同名的檔案，則為可用來解決模稜兩可情形之文字檔的路徑。</span><span class="sxs-lookup"><span data-stu-id="544bc-147">Path to a text file that can be used to resolve ambiguities if you have multiple files with the same name that you were importing in the same job.</span></span> <span data-ttu-id="544bc-148">第一次執行此工具時，它可以在此檔案中填入所有模稜兩可的名稱。</span><span class="sxs-lookup"><span data-stu-id="544bc-148">The first time the tool is run, it can populate this file with all of the ambiguous names.</span></span> <span data-ttu-id="544bc-149">後續執行此工具時，會使用此檔案來解決模稜兩可情形。</span><span class="sxs-lookup"><span data-stu-id="544bc-149">Subsequent runs of the tool will use this file to resolve the ambiguities.</span></span>|  
  
## <a name="using-the-repairimport-command"></a><span data-ttu-id="544bc-150">使用 RepairImport 命令</span><span class="sxs-lookup"><span data-stu-id="544bc-150">Using the RepairImport command</span></span>  
<span data-ttu-id="544bc-151">若要透過網路串流資料來修復匯入資料，您必須指定內含您使用 `/d` 參數匯入之原始檔的目錄。</span><span class="sxs-lookup"><span data-stu-id="544bc-151">To repair import data by streaming the data over the network, you must specify the directories that contain the original files you were importing using the `/d` parameter.</span></span> <span data-ttu-id="544bc-152">您也必須指定您從儲存體帳戶下載的複製記錄檔。</span><span class="sxs-lookup"><span data-stu-id="544bc-152">You must also specify the copy log file that you downloaded from your storage account.</span></span> <span data-ttu-id="544bc-153">用於修復部分失敗之匯入作業的典型命令行如下所示︰</span><span class="sxs-lookup"><span data-stu-id="544bc-153">A typical command line to repair an import job with partial failures looks like:</span></span>  
  
```  
WAImportExport.exe RepairImport /r:C:\WAImportExport\9WM35C2V.rep /d:C:\Users\bob\Pictures;X:\BobBackup\photos /sn:bobmediaaccount /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /CopyLogFile:C:\WAImportExport\9WM35C2V.log  
```  
  
<span data-ttu-id="544bc-154">以下是複製記錄檔的範例。</span><span class="sxs-lookup"><span data-stu-id="544bc-154">The following is an example of a copy log file.</span></span> <span data-ttu-id="544bc-155">在此情況下，針對匯入作業送交的磁碟機上有一個 64K 的檔案片段已損毀。</span><span class="sxs-lookup"><span data-stu-id="544bc-155">In this case, one 64K piece of a file was corrupted on the drive that was shipped for the import job.</span></span> <span data-ttu-id="544bc-156">這是唯一的失敗處，所以已順利匯入作業中其餘的 blob。</span><span class="sxs-lookup"><span data-stu-id="544bc-156">Since this is the only failure indicated, the rest of the blobs in the job were successfully imported.</span></span>  
  
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
  
<span data-ttu-id="544bc-157">將此複製記錄檔傳遞至 Azure 匯入/匯出工具時，此工具將嘗試透過網路複製遺漏的內容來完成此檔案匯入。</span><span class="sxs-lookup"><span data-stu-id="544bc-157">When this copy log is passed to the Azure Import/Export Tool, the tool will try to finish the import for this file by copying the missing contents across the network.</span></span> <span data-ttu-id="544bc-158">在上述範例之後，此工具會在 `C:\Users\bob\Pictures` 和 `X:\BobBackup\photos` 兩個目錄中尋找原始檔案 `\animals\koala.jpg`。</span><span class="sxs-lookup"><span data-stu-id="544bc-158">Following the example above, the tool will look for the original file `\animals\koala.jpg` within the two directories `C:\Users\bob\Pictures` and `X:\BobBackup\photos`.</span></span> <span data-ttu-id="544bc-159">如果檔案 `C:\Users\bob\Pictures\animals\koala.jpg` 存在，則 Azure 匯入/匯出工具會將遺漏的資料範圍複製到對應的 blob `http://bobmediaaccount.blob.core.windows.net/pictures/animals/koala.jpg`。</span><span class="sxs-lookup"><span data-stu-id="544bc-159">If the file `C:\Users\bob\Pictures\animals\koala.jpg` exists, the Azure Import/Export Tool will copy the missing range of data to the corresponding blob `http://bobmediaaccount.blob.core.windows.net/pictures/animals/koala.jpg`.</span></span>  
  
## <a name="resolving-conflicts-when-using-repairimport"></a><span data-ttu-id="544bc-160">解決使用 RepairImport 時的衝突</span><span class="sxs-lookup"><span data-stu-id="544bc-160">Resolving conflicts when using RepairImport</span></span>  
<span data-ttu-id="544bc-161">在某些情況下，基於下列原因之一，此工具可能無法找到或開啟所需的檔案︰找不到檔案、無法存取檔案、檔案名稱模稜兩可，或檔案的內容已不正確。</span><span class="sxs-lookup"><span data-stu-id="544bc-161">In some situations, the tool may not be able to find or open the necessary file for one of the following reasons: the file could not be found, the file is not accessible, the file name is ambiguous, or the content of the file is no longer correct.</span></span>  
  
<span data-ttu-id="544bc-162">如果此工具嘗試找出 `\animals\koala.jpg`，而 `C:\Users\bob\pictures` 和 `X:\BobBackup\photos` 之下同時有該名稱的檔案，則可能會發生模稜兩可錯誤。</span><span class="sxs-lookup"><span data-stu-id="544bc-162">An ambiguous error could occur if the tool is trying to locate `\animals\koala.jpg` and there is a file with that name under both `C:\Users\bob\pictures` and `X:\BobBackup\photos`.</span></span> <span data-ttu-id="544bc-163">也就是說，`C:\Users\bob\pictures\animals\koala.jpg` 和 `X:\BobBackup\photos\animals\koala.jpg` 兩者都存在於匯入作業磁碟機上。</span><span class="sxs-lookup"><span data-stu-id="544bc-163">That is, both `C:\Users\bob\pictures\animals\koala.jpg` and `X:\BobBackup\photos\animals\koala.jpg` exist on the import job drives.</span></span>  
  
<span data-ttu-id="544bc-164">`/PathMapFile` 選項可讓您解決這些錯誤。</span><span class="sxs-lookup"><span data-stu-id="544bc-164">The `/PathMapFile` option will allow you to resolve these errors.</span></span> <span data-ttu-id="544bc-165">您可以指定檔案名稱，其中內含工具無法正確識別的檔案清單。</span><span class="sxs-lookup"><span data-stu-id="544bc-165">You can specify the name of the file which will contains the list of files that the tool was not able to correctly identify.</span></span> <span data-ttu-id="544bc-166">以下是會填入 `9WM35C2V_pathmap.txt` 的範例命令行：</span><span class="sxs-lookup"><span data-stu-id="544bc-166">The following is an example command line that would populate `9WM35C2V_pathmap.txt`:</span></span>  
  
```
WAImportExport.exe RepairImport /r:C:\WAImportExport\9WM35C2V.rep /d:C:\Users\bob\Pictures;X:\BobBackup\photos /sn:bobmediaaccount /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /CopyLogFile:C:\WAImportExport\9WM35C2V.log /PathMapFile:C:\WAImportExport\9WM35C2V_pathmap.txt  
```
  
<span data-ttu-id="544bc-167">工具會接著將有問題的檔案路徑寫入至 `9WM35C2V_pathmap.txt`，一行一個。</span><span class="sxs-lookup"><span data-stu-id="544bc-167">The tool will then write the problematic file paths to `9WM35C2V_pathmap.txt`, one on each line.</span></span> <span data-ttu-id="544bc-168">比方說，此檔案在執行命令後可能包含下列項目︰</span><span class="sxs-lookup"><span data-stu-id="544bc-168">For instance, the file may contain the following entries after running the command:</span></span>  
 
```
\animals\koala.jpg  
\animals\kangaroo.jpg  
```
  
 <span data-ttu-id="544bc-169">對於清單中的每個檔案，您應該嘗試找出並開啟檔案，以確保其可供工具使用。</span><span class="sxs-lookup"><span data-stu-id="544bc-169">For each file in the list, you should attempt to locate and open the file to ensure it is available to the tool.</span></span> <span data-ttu-id="544bc-170">如果您想明確地告訴工具何處尋找檔案，您可以修改路徑對應檔並將路徑新增至同一行上的每個檔案 (以 Tab 字元分隔)︰</span><span class="sxs-lookup"><span data-stu-id="544bc-170">If you wish to tell the tool explicitly where to find a file, you can modify the path map file and add the path to each file on the same line, separated by a tab character:</span></span>  
  
```
\animals\koala.jpg           C:\Users\bob\Pictures\animals\koala.jpg  
\animals\kangaroo.jpg        X:\BobBackup\photos\animals\kangaroo.jpg  
```
  
<span data-ttu-id="544bc-171">讓必要檔案可供工具使用，或更新路徑對應檔之後，您可以重新執行工具，以完成匯入程序。</span><span class="sxs-lookup"><span data-stu-id="544bc-171">After making the necessary files available to the tool, or updating the path map file, you can rerun the tool to complete the import process.</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="544bc-172">後續步驟</span><span class="sxs-lookup"><span data-stu-id="544bc-172">Next steps</span></span>
 
* [<span data-ttu-id="544bc-173">設定 Azure 匯入/匯出工具</span><span class="sxs-lookup"><span data-stu-id="544bc-173">Setting Up the Azure Import/Export Tool</span></span>](storage-import-export-tool-setup-v1.md)   
* [<span data-ttu-id="544bc-174">針對匯入作業準備硬碟</span><span class="sxs-lookup"><span data-stu-id="544bc-174">Preparing hard drives for an import job</span></span>](storage-import-export-tool-preparing-hard-drives-import-v1.md)   
* [<span data-ttu-id="544bc-175">利用複製記錄檔檢閱作業狀態</span><span class="sxs-lookup"><span data-stu-id="544bc-175">Reviewing job status with copy log files</span></span>](storage-import-export-tool-reviewing-job-status-v1.md)   
* [<span data-ttu-id="544bc-176">修復匯出作業</span><span class="sxs-lookup"><span data-stu-id="544bc-176">Repairing an export job</span></span>](storage-import-export-tool-repairing-an-export-job-v1.md)   
* [<span data-ttu-id="544bc-177">針對 Azure 匯入/匯出工具進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="544bc-177">Troubleshooting the Azure Import/Export Tool</span></span>](storage-import-export-tool-troubleshooting-v1.md)
