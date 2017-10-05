---
title: "修復 Azure 匯入/匯出匯出作業 - v1 | Microsoft Docs"
description: "了解如何修復使用 Azure 匯入/匯出服務建立和執行的匯出作業。"
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 728e2a42-04ce-4be8-9375-e9e2bc6827a5
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: 30ca0f8d06cb1927c19e66035ff485db0fc09e5a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="repairing-an-export-job"></a><span data-ttu-id="62fad-103">修復匯出作業</span><span class="sxs-lookup"><span data-stu-id="62fad-103">Repairing an export job</span></span>
<span data-ttu-id="62fad-104">完成匯出作業之後，您可以在內部部署上執行 Microsoft Azure 匯入/匯出工具，以便：</span><span class="sxs-lookup"><span data-stu-id="62fad-104">After an export job has completed, you can run the Microsoft Azure Import/Export Tool on-premises to:</span></span>  
  
1.  <span data-ttu-id="62fad-105">下載 Azure 匯入/匯出服務無法匯出的檔案。</span><span class="sxs-lookup"><span data-stu-id="62fad-105">Download any files that the Azure Import/Export service was unable to export.</span></span>  
  
2.  <span data-ttu-id="62fad-106">驗證磁碟機上已正確匯出的檔案。</span><span class="sxs-lookup"><span data-stu-id="62fad-106">Validate that the files on the drive were correctly exported.</span></span>  
  
<span data-ttu-id="62fad-107">您必須能夠連線到 Azure 儲存體，才能使用這項功能。</span><span class="sxs-lookup"><span data-stu-id="62fad-107">You must have connectivity to Azure Storage to use this functionality.</span></span>  
  
<span data-ttu-id="62fad-108">用於修復匯出作業的命令是 **RepairExport**。</span><span class="sxs-lookup"><span data-stu-id="62fad-108">The command for repairing an import job is **RepairExport**.</span></span>

## <a name="repairexport-parameters"></a><span data-ttu-id="62fad-109">RepairExport 參數</span><span class="sxs-lookup"><span data-stu-id="62fad-109">RepairExport parameters</span></span>

<span data-ttu-id="62fad-110">您可以搭配 **RepairExport** 指定下列參數：</span><span class="sxs-lookup"><span data-stu-id="62fad-110">The following parameters can be specified with **RepairExport**:</span></span>  
  
|<span data-ttu-id="62fad-111">參數</span><span class="sxs-lookup"><span data-stu-id="62fad-111">Parameter</span></span>|<span data-ttu-id="62fad-112">說明</span><span class="sxs-lookup"><span data-stu-id="62fad-112">Description</span></span>|  
|---------------|-----------------|  
|<span data-ttu-id="62fad-113">**/r:<RepairFile\>**</span><span class="sxs-lookup"><span data-stu-id="62fad-113">**/r:<RepairFile\>**</span></span>|<span data-ttu-id="62fad-114">必要。</span><span class="sxs-lookup"><span data-stu-id="62fad-114">Required.</span></span> <span data-ttu-id="62fad-115">修復檔案的路徑，可追蹤修復進度，並可讓您繼續中斷的修復。</span><span class="sxs-lookup"><span data-stu-id="62fad-115">Path to the repair file, which tracks the progress of the repair, and allows you to resume an interrupted repair.</span></span> <span data-ttu-id="62fad-116">每個磁碟機必須只能有一個修復檔案。</span><span class="sxs-lookup"><span data-stu-id="62fad-116">Each drive must have one and only one repair file.</span></span> <span data-ttu-id="62fad-117">當您啟動指定磁碟機的修復時，您將會傳入尚不存在之修復檔的路徑。</span><span class="sxs-lookup"><span data-stu-id="62fad-117">When you start a repair for a given drive, you will pass in the path to a repair file which does not yet exist.</span></span> <span data-ttu-id="62fad-118">若要恢復中斷的修復，您應傳入現有修復檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="62fad-118">To resume an interrupted repair, you should pass in the name of an existing repair file.</span></span> <span data-ttu-id="62fad-119">一律必須指定對應於目標磁碟機的修復檔。</span><span class="sxs-lookup"><span data-stu-id="62fad-119">The repair file corresponding to the target drive must always be specified.</span></span>|  
|<span data-ttu-id="62fad-120">**/logdir:\><LogDirectory**</span><span class="sxs-lookup"><span data-stu-id="62fad-120">**/logdir:<LogDirectory\>**</span></span>|<span data-ttu-id="62fad-121">選用。</span><span class="sxs-lookup"><span data-stu-id="62fad-121">Optional.</span></span> <span data-ttu-id="62fad-122">記錄檔目錄。</span><span class="sxs-lookup"><span data-stu-id="62fad-122">The log directory.</span></span> <span data-ttu-id="62fad-123">詳細資訊記錄檔會寫入至這個目錄。</span><span class="sxs-lookup"><span data-stu-id="62fad-123">Verbose log files will be written to this directory.</span></span> <span data-ttu-id="62fad-124">如未指定記錄檔目錄，則會使用目前的目錄做為記錄檔目錄。</span><span class="sxs-lookup"><span data-stu-id="62fad-124">If no log directory is specified, the current directory will be used as the log directory.</span></span>|  
|<span data-ttu-id="62fad-125">**/d:<TargetDirectory\>**</span><span class="sxs-lookup"><span data-stu-id="62fad-125">**/d:<TargetDirectory\>**</span></span>|<span data-ttu-id="62fad-126">必要。</span><span class="sxs-lookup"><span data-stu-id="62fad-126">Required.</span></span> <span data-ttu-id="62fad-127">要驗證及修復的目錄。</span><span class="sxs-lookup"><span data-stu-id="62fad-127">The directory to validate and repair.</span></span> <span data-ttu-id="62fad-128">這通常是匯出磁碟機的根目錄，但也可能是含有匯出檔案複本的網路檔案共用。</span><span class="sxs-lookup"><span data-stu-id="62fad-128">This is usually the root directory of the export drive, but could also be a network file share containing a copy of the exported files.</span></span>|  
|<span data-ttu-id="62fad-129">**/bk:<BitLockerKey\>**</span><span class="sxs-lookup"><span data-stu-id="62fad-129">**/bk:<BitLockerKey\>**</span></span>|<span data-ttu-id="62fad-130">選用。</span><span class="sxs-lookup"><span data-stu-id="62fad-130">Optional.</span></span> <span data-ttu-id="62fad-131">如果您希望該工具解除鎖定存放匯出檔案的加密磁碟機，您應指定 BitLocker 金鑰。</span><span class="sxs-lookup"><span data-stu-id="62fad-131">You should specify the BitLocker key if you want the tool to unlock an encrypted where the exported files are stored.</span></span>|  
|<span data-ttu-id="62fad-132">**/sn:<StorageAccountName\>**</span><span class="sxs-lookup"><span data-stu-id="62fad-132">**/sn:<StorageAccountName\>**</span></span>|<span data-ttu-id="62fad-133">必要。</span><span class="sxs-lookup"><span data-stu-id="62fad-133">Required.</span></span> <span data-ttu-id="62fad-134">匯出作業的儲存體帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="62fad-134">The name of the storage account for the export job.</span></span>|  
|<span data-ttu-id="62fad-135">**/sk:<StorageAccountKey\>**</span><span class="sxs-lookup"><span data-stu-id="62fad-135">**/sk:<StorageAccountKey\>**</span></span>|<span data-ttu-id="62fad-136">如果未指定 (且只有在未指定) 容器 SAS 時，才是**必要**參數。</span><span class="sxs-lookup"><span data-stu-id="62fad-136">**Required** if and only if a container SAS is not specified.</span></span> <span data-ttu-id="62fad-137">匯出作業之儲存體帳戶的帳戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="62fad-137">The account key for the storage account for the export job.</span></span>|  
|<span data-ttu-id="62fad-138">**/csas:<ContainerSas\>**</span><span class="sxs-lookup"><span data-stu-id="62fad-138">**/csas:<ContainerSas\>**</span></span>|<span data-ttu-id="62fad-139">如果未指定 (且只有在未指定) 儲存體帳戶金鑰時，才是**必要**參數。</span><span class="sxs-lookup"><span data-stu-id="62fad-139">**Required** if and only if the storage account key is not specified.</span></span> <span data-ttu-id="62fad-140">存取與匯出作業相關聯的 Blob 所用的容器 SAS。</span><span class="sxs-lookup"><span data-stu-id="62fad-140">The container SAS for accessing the blobs associated with the export job.</span></span>|  
|<span data-ttu-id="62fad-141">**/CopyLogFile:<DriveCopyLogFile\>**</span><span class="sxs-lookup"><span data-stu-id="62fad-141">**/CopyLogFile:<DriveCopyLogFile\>**</span></span>|<span data-ttu-id="62fad-142">必要。</span><span class="sxs-lookup"><span data-stu-id="62fad-142">Required.</span></span> <span data-ttu-id="62fad-143">磁碟機複製記錄檔的路徑。</span><span class="sxs-lookup"><span data-stu-id="62fad-143">The path to the drive copy log file.</span></span> <span data-ttu-id="62fad-144">此檔案是由 Windows Azure 匯入/匯出服務所產生，您可以從與作業相關聯的 blob 儲存體下載。</span><span class="sxs-lookup"><span data-stu-id="62fad-144">The file is generated by the Windows Azure Import/Export service and can be downloaded from the blob storage associated with the job.</span></span> <span data-ttu-id="62fad-145">複製記錄檔包含所要修復之失敗 blob 或檔案的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="62fad-145">The copy log file contains information about failed blobs or files which are to be repaired.</span></span>|  
|<span data-ttu-id="62fad-146">**/ManifestFile:<DriveManifestFile\>**</span><span class="sxs-lookup"><span data-stu-id="62fad-146">**/ManifestFile:<DriveManifestFile\>**</span></span>|<span data-ttu-id="62fad-147">選用。</span><span class="sxs-lookup"><span data-stu-id="62fad-147">Optional.</span></span> <span data-ttu-id="62fad-148">匯出磁碟機的資訊清單檔案路徑。</span><span class="sxs-lookup"><span data-stu-id="62fad-148">The path to the export drive's manifest file.</span></span> <span data-ttu-id="62fad-149">此檔案是由 Windows Azure 匯入/匯出服務所產生並儲存在匯出磁碟機上，並選擇性地儲存在與作業相關聯之儲存體帳戶的 blob 中。</span><span class="sxs-lookup"><span data-stu-id="62fad-149">This file is generated by the Windows Azure Import/Export service and stored on the export drive, and optionally in a blob in the storage account associated with the job.</span></span><br /><br /> <span data-ttu-id="62fad-150">工具將會使用此檔案內含的 MD5 雜湊，驗證匯出磁碟機上的檔案內容。</span><span class="sxs-lookup"><span data-stu-id="62fad-150">The content of the files on the export drive will be verified with the MD5 hashes contained in this file.</span></span> <span data-ttu-id="62fad-151">任何被斷定為損毀的檔案都將會下載並重新寫入至目標目錄。</span><span class="sxs-lookup"><span data-stu-id="62fad-151">Any files that are determined to be corrupted will be downloaded and rewritten to the target directories.</span></span>|  
  
## <a name="using-repairexport-mode-to-correct-failed-exports"></a><span data-ttu-id="62fad-152">使用 RepairExport 模式來更正失敗的匯出</span><span class="sxs-lookup"><span data-stu-id="62fad-152">Using RepairExport mode to correct failed exports</span></span>  
<span data-ttu-id="62fad-153">您可以使用 Azure 匯入/匯出工具來下載無法匯出的檔案。</span><span class="sxs-lookup"><span data-stu-id="62fad-153">You can use the Azure Import/Export Tool to download files that failed to export.</span></span> <span data-ttu-id="62fad-154">複製記錄檔會包含無法匯出的檔案清單。</span><span class="sxs-lookup"><span data-stu-id="62fad-154">The copy log file will contain a list of files that failed to export.</span></span>  
  
<span data-ttu-id="62fad-155">匯出失敗的原因包括下列可能性︰</span><span class="sxs-lookup"><span data-stu-id="62fad-155">The causes of export failures include the following possibilities:</span></span>  
  
-   <span data-ttu-id="62fad-156">損壞的磁碟機</span><span class="sxs-lookup"><span data-stu-id="62fad-156">Damaged drives</span></span>  
  
-   <span data-ttu-id="62fad-157">儲存體帳戶金鑰會在移轉過程中變更</span><span class="sxs-lookup"><span data-stu-id="62fad-157">The storage account key changed during the transfer process</span></span>  
  
<span data-ttu-id="62fad-158">若要在 **RepairExport** 模式中執行此工具，您必須先將含有匯出檔案的磁碟機連接到您的電腦。</span><span class="sxs-lookup"><span data-stu-id="62fad-158">To run the tool in **RepairExport** mode, you first need to connect the drive containing the exported files to your computer.</span></span> <span data-ttu-id="62fad-159">接下來，執行 Azure 匯入/匯出工具，並使用 `/d` 參數指定該磁碟機的路徑。</span><span class="sxs-lookup"><span data-stu-id="62fad-159">Next, run the Azure Import/Export Tool, specifying the path to that drive with the `/d` parameter.</span></span> <span data-ttu-id="62fad-160">您也必須指定您下載之磁碟機複製記錄檔的路徑。</span><span class="sxs-lookup"><span data-stu-id="62fad-160">You also need to specify the path to the drive's copy log file that you downloaded.</span></span> <span data-ttu-id="62fad-161">下列命令行範例會執行工具，以修復任何無法匯出的檔案︰</span><span class="sxs-lookup"><span data-stu-id="62fad-161">The following command line example below runs the tool to repair any files that failed to export:</span></span>  
  
```  
WAImportExport.exe RepairExport /r:C:\WAImportExport\9WM35C3U.rep /d:G:\ /sn:bobmediaaccount /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /CopyLogFile:C:\WAImportExport\9WM35C3U.log  
```  
  
<span data-ttu-id="62fad-162">以下的複製記錄檔範例顯示 blob 中無法匯出的一個區塊︰</span><span class="sxs-lookup"><span data-stu-id="62fad-162">The following is an example of a copy log file that shows that one block in the blob failed to export:</span></span>  
  
```xml
<?xml version="1.0" encoding="utf-8"?>  
<DriveLog>  
  <DriveId>9WM35C2V</DriveId>  
  <Blob Status="CompletedWithErrors">  
    <BlobPath>pictures/wild/desert.jpg</BlobPath>  
    <FilePath>\pictures\wild\desert.jpg</FilePath>  
    <LastModified>2012-09-18T23:47:08Z</LastModified>  
    <Length>163840</Length>  
    <BlockList>  
      <Block Offset="65536" Length="65536" Id="AQAAAA==" Status="Failed" />  
    </BlockList>  
  </Blob>  
  <Status>CompletedWithErrors</Status>  
</DriveLog>  
```  
  
<span data-ttu-id="62fad-163">此複製記錄檔指出當 Windows Azure 匯入/匯出服務將其中一個 blob 區塊下載至匯出磁碟機上的檔案時所發生的錯誤。</span><span class="sxs-lookup"><span data-stu-id="62fad-163">The copy log file indicates that a failure occurred while the Windows Azure Import/Export service was downloading one of the blob's blocks to the file on the export drive.</span></span> <span data-ttu-id="62fad-164">已成功下載檔案的其他元件，並已正確設定檔案長度。</span><span class="sxs-lookup"><span data-stu-id="62fad-164">The other components of the file downloaded successfully, and the file length was correctly set.</span></span> <span data-ttu-id="62fad-165">在此情況下，工具會開啟磁碟機上的這個檔案，從儲存體帳戶下載此區塊，並將它寫入至從位移 65536 開始且長度為 65536 的檔案範圍。</span><span class="sxs-lookup"><span data-stu-id="62fad-165">In this case, the tool will open the file on the drive, download the block from the storage account, and write it to the file range starting from offset 65536 with length 65536.</span></span>  
  
## <a name="using-repairexport-to-validate-drive-contents"></a><span data-ttu-id="62fad-166">使用 RepairExport 驗證磁碟機內容</span><span class="sxs-lookup"><span data-stu-id="62fad-166">Using RepairExport to validate drive contents</span></span>  
<span data-ttu-id="62fad-167">您也可以使用 Azure 匯入/匯出服務搭配 **RepairExport** 選項，以驗證磁碟機上的內容是否正確。</span><span class="sxs-lookup"><span data-stu-id="62fad-167">You can also use Azure Import/Export with the **RepairExport** option to validate the contents on the drive are correct.</span></span> <span data-ttu-id="62fad-168">每個匯出磁碟機上的資訊清單檔案都包含磁碟機內容適用的 MD5。</span><span class="sxs-lookup"><span data-stu-id="62fad-168">The manifest file on each export drive contains MD5s for the contents of the drive.</span></span>  
  
<span data-ttu-id="62fad-169">Azure 匯入/匯出服務也可以在匯出期間將資訊清單檔案儲存到儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="62fad-169">The Azure Import/Export service can also save the manifest files to a storage account during the export process.</span></span> <span data-ttu-id="62fad-170">當作業完成時，可透過 [Get Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) 作業，取得資訊清單檔案的位置。</span><span class="sxs-lookup"><span data-stu-id="62fad-170">The location of the manifest files is available via the [Get Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operation when the job has completed.</span></span> <span data-ttu-id="62fad-171">如需磁碟機資訊清單檔案的格式，請參閱[匯入/匯出服務資訊清單檔案格式](storage-import-export-file-format-metadata-and-properties.md)。</span><span class="sxs-lookup"><span data-stu-id="62fad-171">See [Import/Export service Manifest File Format](storage-import-export-file-format-metadata-and-properties.md) for more information about the format of a drive manifest file.</span></span>  
  
<span data-ttu-id="62fad-172">下列範例示範如何搭配 **/ManifestFile** 和 **/CopyLogFile** 參數執行 Azure 匯入/匯出工具：</span><span class="sxs-lookup"><span data-stu-id="62fad-172">The following example shows how to run the Azure Import/Export Tool with the **/ManifestFile** and **/CopyLogFile** parameters:</span></span>  
  
```  
WAImportExport.exe RepairExport /r:C:\WAImportExport\9WM35C3U.rep /d:G:\ /sn:bobmediaaccount /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /CopyLogFile:C:\WAImportExport\9WM35C3U.log /ManifestFile:G:\9WM35C3U.manifest  
```  
  
<span data-ttu-id="62fad-173">以下是資訊清單檔案的範例：</span><span class="sxs-lookup"><span data-stu-id="62fad-173">The following is an example of a manifest file:</span></span>  
  
```xml
<?xml version="1.0" encoding="utf-8"?>  
<DriveManifest Version="2011-10-01">  
  <Drive>  
    <DriveId>9WM35C3U</DriveId>  
    <ClientCreator>Windows Azure Import/Export service</ClientCreator>  
    <BlobList>
      <Blob>  
        <BlobPath>pictures/city/redmond.jpg</BlobPath>  
        <FilePath>\pictures\city\redmond.jpg</FilePath>  
        <Length>15360</Length>  
        <PageRangeList>  
          <PageRange Offset="0" Length="3584" Hash="72FC55ED9AFDD40A0C8D5C4193208416" />  
          <PageRange Offset="3584" Length="3584" Hash="68B28A561B73D1DA769D4C24AA427DB8" />  
          <PageRange Offset="7168" Length="512" Hash="F521DF2F50C46BC5F9EA9FB787A23EED" />  
        </PageRangeList>  
        <PropertiesPath Hash="E72A22EA959566066AD89E3B49020C0A">\pictures\city\redmond.jpg.properties</PropertiesPath>  
      </Blob>  
      <Blob>  
        <BlobPath>pictures/wild/canyon.jpg</BlobPath>  
        <FilePath>\pictures\wild\canyon.jpg</FilePath>  
        <Length>10884</Length>  
        <BlockList>  
          <Block Offset="0" Length="2721" Id="AAAAAA==" Hash="263DC9C4B99C2177769C5EBE04787037" />  
          <Block Offset="2721" Length="2721" Id="AQAAAA==" Hash="0C52BAE2CC20EFEC15CC1E3045517AA6" />  
          <Block Offset="5442" Length="2721" Id="AgAAAA==" Hash="73D1CB62CB426230C34C9F57B7148F10" />  
          <Block Offset="8163" Length="2721" Id="AwAAAA==" Hash="11210E665C5F8E7E4F136D053B243E6A" />  
        </BlockList>  
        <PropertiesPath Hash="81D7F81B2C29F10D6E123D386C3A4D5A">\pictures\wild\canyon.jpg.properties</PropertiesPath>  
      </Blob> 
    </BlobList>  
 </Drive>  
</DriveManifest>  
``` 
  
<span data-ttu-id="62fad-174">完成修復程序之後，工具會讀取資訊清單檔案中參考的每個檔案，並以 MD5 雜湊驗證檔案的完整性。</span><span class="sxs-lookup"><span data-stu-id="62fad-174">After finishing the repair process, the tool will read through each file referenced in the manifest file and verify the file's integrity with the MD5 hashes.</span></span> <span data-ttu-id="62fad-175">在上述資訊清單中，將會逐步進行下列元件。</span><span class="sxs-lookup"><span data-stu-id="62fad-175">For the manifest above, it will go through the following components.</span></span>  

```  
G:\pictures\city\redmond.jpg, offset 0, length 3584  
  
G:\pictures\city\redmond.jpg, offset 3584, length 3584  
  
G:\pictures\city\redmond.jpg, offset 7168, length 3584  
  
G:\pictures\city\redmond.jpg.properties  
  
G:\pictures\wild\canyon.jpg, offset 0, length 2721  
  
G:\pictures\wild\canyon.jpg, offset 2721, length 2721  
  
G:\pictures\wild\canyon.jpg, offset 5442, length 2721  
  
G:\pictures\wild\canyon.jpg, offset 8163, length 2721  
  
G:\pictures\wild\canyon.jpg.properties  
```

<span data-ttu-id="62fad-176">工具將會下載驗證失敗的所有元件，並將它們重新寫入至磁碟機上的相同檔案。</span><span class="sxs-lookup"><span data-stu-id="62fad-176">Any component failing the verification will be downloaded by the tool and rewritten to the same file on the drive.</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="62fad-177">後續步驟</span><span class="sxs-lookup"><span data-stu-id="62fad-177">Next steps</span></span>
 
* [<span data-ttu-id="62fad-178">設定 Azure 匯入/匯出工具</span><span class="sxs-lookup"><span data-stu-id="62fad-178">Setting Up the Azure Import/Export Tool</span></span>](storage-import-export-tool-setup-v1.md)   
* [<span data-ttu-id="62fad-179">針對匯入作業準備硬碟</span><span class="sxs-lookup"><span data-stu-id="62fad-179">Preparing hard drives for an import job</span></span>](storage-import-export-tool-preparing-hard-drives-import-v1.md)   
* [<span data-ttu-id="62fad-180">利用複製記錄檔檢閱作業狀態</span><span class="sxs-lookup"><span data-stu-id="62fad-180">Reviewing job status with copy log files</span></span>](storage-import-export-tool-reviewing-job-status-v1.md)   
* [<span data-ttu-id="62fad-181">修復匯入作業</span><span class="sxs-lookup"><span data-stu-id="62fad-181">Repairing an import job</span></span>](storage-import-export-tool-repairing-an-import-job-v1.md)   
* [<span data-ttu-id="62fad-182">針對 Azure 匯入/匯出工具進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="62fad-182">Troubleshooting the Azure Import/Export Tool</span></span>](storage-import-export-tool-troubleshooting-v1.md)
