---
title: "Azure 匯入/匯出匯出工作-v1 aaaRepairing |Microsoft 文件"
description: "了解如何匯出工作，所建立及執行使用 toorepair hello Azure 匯入/匯出服務。"
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
ms.openlocfilehash: 96c674fc7c697c37882fb2980c340303896ac6c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="repairing-an-export-job"></a><span data-ttu-id="1ffc3-103">修復匯出作業</span><span class="sxs-lookup"><span data-stu-id="1ffc3-103">Repairing an export job</span></span>
<span data-ttu-id="1ffc3-104">匯出工作完成後，您可以執行 Microsoft Azure 匯入/匯出工具提供從內部部署的 hello:</span><span class="sxs-lookup"><span data-stu-id="1ffc3-104">After an export job has completed, you can run hello Microsoft Azure Import/Export Tool on-premises to:</span></span>  
  
1.  <span data-ttu-id="1ffc3-105">下載 hello Azure 匯入/匯出服務是無法 tooexport 任何檔案。</span><span class="sxs-lookup"><span data-stu-id="1ffc3-105">Download any files that hello Azure Import/Export service was unable tooexport.</span></span>  
  
2.  <span data-ttu-id="1ffc3-106">驗證 hello 磁碟機上的 hello 檔案已正確匯出。</span><span class="sxs-lookup"><span data-stu-id="1ffc3-106">Validate that hello files on hello drive were correctly exported.</span></span>  
  
<span data-ttu-id="1ffc3-107">您必須擁有連線 tooAzure 儲存體 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="1ffc3-107">You must have connectivity tooAzure Storage toouse this functionality.</span></span>  
  
<span data-ttu-id="1ffc3-108">hello 命令來修復匯入工作是**RepairExport**。</span><span class="sxs-lookup"><span data-stu-id="1ffc3-108">hello command for repairing an import job is **RepairExport**.</span></span>

## <a name="repairexport-parameters"></a><span data-ttu-id="1ffc3-109">RepairExport 參數</span><span class="sxs-lookup"><span data-stu-id="1ffc3-109">RepairExport parameters</span></span>

<span data-ttu-id="1ffc3-110">hello 指定下列參數可以與**RepairExport**:</span><span class="sxs-lookup"><span data-stu-id="1ffc3-110">hello following parameters can be specified with **RepairExport**:</span></span>  
  
|<span data-ttu-id="1ffc3-111">參數</span><span class="sxs-lookup"><span data-stu-id="1ffc3-111">Parameter</span></span>|<span data-ttu-id="1ffc3-112">說明</span><span class="sxs-lookup"><span data-stu-id="1ffc3-112">Description</span></span>|  
|---------------|-----------------|  
|<span data-ttu-id="1ffc3-113">**/r:<RepairFile\>**</span><span class="sxs-lookup"><span data-stu-id="1ffc3-113">**/r:<RepairFile\>**</span></span>|<span data-ttu-id="1ffc3-114">必要。</span><span class="sxs-lookup"><span data-stu-id="1ffc3-114">Required.</span></span> <span data-ttu-id="1ffc3-115">路徑 toohello 修復檔案，追蹤 hello hello 修復進度，並可讓您 tooresume 中斷的修復。</span><span class="sxs-lookup"><span data-stu-id="1ffc3-115">Path toohello repair file, which tracks hello progress of hello repair, and allows you tooresume an interrupted repair.</span></span> <span data-ttu-id="1ffc3-116">每個磁碟機需要一個修復檔案，而且只能有一個。</span><span class="sxs-lookup"><span data-stu-id="1ffc3-116">Each drive must have one and only one repair file.</span></span> <span data-ttu-id="1ffc3-117">當您開始在給定的磁碟機的修復時，您將會傳入 hello 路徑 tooa 修復檔案尚不存在。</span><span class="sxs-lookup"><span data-stu-id="1ffc3-117">When you start a repair for a given drive, you will pass in hello path tooa repair file which does not yet exist.</span></span> <span data-ttu-id="1ffc3-118">tooresume 中斷的修復，您應傳入 hello 現有的修復檔名稱。</span><span class="sxs-lookup"><span data-stu-id="1ffc3-118">tooresume an interrupted repair, you should pass in hello name of an existing repair file.</span></span> <span data-ttu-id="1ffc3-119">一律必須指定 hello 修復檔案對應 toohello 目標磁碟機。</span><span class="sxs-lookup"><span data-stu-id="1ffc3-119">hello repair file corresponding toohello target drive must always be specified.</span></span>|  
|<span data-ttu-id="1ffc3-120">**/logdir:\><LogDirectory**</span><span class="sxs-lookup"><span data-stu-id="1ffc3-120">**/logdir:<LogDirectory\>**</span></span>|<span data-ttu-id="1ffc3-121">選用。</span><span class="sxs-lookup"><span data-stu-id="1ffc3-121">Optional.</span></span> <span data-ttu-id="1ffc3-122">hello 記錄檔目錄。</span><span class="sxs-lookup"><span data-stu-id="1ffc3-122">hello log directory.</span></span> <span data-ttu-id="1ffc3-123">詳細資訊記錄檔會寫入 toothis 目錄。</span><span class="sxs-lookup"><span data-stu-id="1ffc3-123">Verbose log files will be written toothis directory.</span></span> <span data-ttu-id="1ffc3-124">如果未不指定任何記錄檔目錄，則 hello 目前的目錄會用作 hello 記錄檔目錄。</span><span class="sxs-lookup"><span data-stu-id="1ffc3-124">If no log directory is specified, hello current directory will be used as hello log directory.</span></span>|  
|<span data-ttu-id="1ffc3-125">**/d:<TargetDirectory\>**</span><span class="sxs-lookup"><span data-stu-id="1ffc3-125">**/d:<TargetDirectory\>**</span></span>|<span data-ttu-id="1ffc3-126">必要。</span><span class="sxs-lookup"><span data-stu-id="1ffc3-126">Required.</span></span> <span data-ttu-id="1ffc3-127">hello 目錄 toovalidate 和修復。</span><span class="sxs-lookup"><span data-stu-id="1ffc3-127">hello directory toovalidate and repair.</span></span> <span data-ttu-id="1ffc3-128">這通常是 hello 根目錄的 hello 匯出磁碟機，但無法同時也網路檔案共用包含匯出的 hello 檔案的複本。</span><span class="sxs-lookup"><span data-stu-id="1ffc3-128">This is usually hello root directory of hello export drive, but could also be a network file share containing a copy of hello exported files.</span></span>|  
|<span data-ttu-id="1ffc3-129">**/bk:<BitLockerKey\>**</span><span class="sxs-lookup"><span data-stu-id="1ffc3-129">**/bk:<BitLockerKey\>**</span></span>|<span data-ttu-id="1ffc3-130">選用。</span><span class="sxs-lookup"><span data-stu-id="1ffc3-130">Optional.</span></span> <span data-ttu-id="1ffc3-131">如果您想 hello 工具 toounlock 儲存加密 hello 匯出的檔案，您應該指定 hello BitLocker 金鑰。</span><span class="sxs-lookup"><span data-stu-id="1ffc3-131">You should specify hello BitLocker key if you want hello tool toounlock an encrypted where hello exported files are stored.</span></span>|  
|<span data-ttu-id="1ffc3-132">**/sn:<StorageAccountName\>**</span><span class="sxs-lookup"><span data-stu-id="1ffc3-132">**/sn:<StorageAccountName\>**</span></span>|<span data-ttu-id="1ffc3-133">必要。</span><span class="sxs-lookup"><span data-stu-id="1ffc3-133">Required.</span></span> <span data-ttu-id="1ffc3-134">hello 名稱 hello hello 儲存體帳戶匯出工作。</span><span class="sxs-lookup"><span data-stu-id="1ffc3-134">hello name of hello storage account for hello export job.</span></span>|  
|<span data-ttu-id="1ffc3-135">**/sk:<StorageAccountKey\>**</span><span class="sxs-lookup"><span data-stu-id="1ffc3-135">**/sk:<StorageAccountKey\>**</span></span>|<span data-ttu-id="1ffc3-136">如果未指定 (且只有在未指定) 容器 SAS 時，才是**必要**參數。</span><span class="sxs-lookup"><span data-stu-id="1ffc3-136">**Required** if and only if a container SAS is not specified.</span></span> <span data-ttu-id="1ffc3-137">hello hello hello 的儲存體帳戶的帳戶金鑰匯出工作。</span><span class="sxs-lookup"><span data-stu-id="1ffc3-137">hello account key for hello storage account for hello export job.</span></span>|  
|<span data-ttu-id="1ffc3-138">**/csas:<ContainerSas\>**</span><span class="sxs-lookup"><span data-stu-id="1ffc3-138">**/csas:<ContainerSas\>**</span></span>|<span data-ttu-id="1ffc3-139">**需要**如果且只有未指定 hello 儲存體帳戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="1ffc3-139">**Required** if and only if hello storage account key is not specified.</span></span> <span data-ttu-id="1ffc3-140">用於存取與 hello 匯出工作相關聯的 hello blob hello 容器 SAS。</span><span class="sxs-lookup"><span data-stu-id="1ffc3-140">hello container SAS for accessing hello blobs associated with hello export job.</span></span>|  
|<span data-ttu-id="1ffc3-141">**/CopyLogFile:<DriveCopyLogFile\>**</span><span class="sxs-lookup"><span data-stu-id="1ffc3-141">**/CopyLogFile:<DriveCopyLogFile\>**</span></span>|<span data-ttu-id="1ffc3-142">必要。</span><span class="sxs-lookup"><span data-stu-id="1ffc3-142">Required.</span></span> <span data-ttu-id="1ffc3-143">hello 路徑 toohello 磁碟機複製記錄檔。</span><span class="sxs-lookup"><span data-stu-id="1ffc3-143">hello path toohello drive copy log file.</span></span> <span data-ttu-id="1ffc3-144">hello 檔案 hello Windows Azure 匯入/匯出服務所產生，並可從 hello 與 hello 工作相關聯的 blob 儲存體下載。</span><span class="sxs-lookup"><span data-stu-id="1ffc3-144">hello file is generated by hello Windows Azure Import/Export service and can be downloaded from hello blob storage associated with hello job.</span></span> <span data-ttu-id="1ffc3-145">hello 複製記錄檔包含失敗的 blob 或檔案，也就是 toobe 修復的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="1ffc3-145">hello copy log file contains information about failed blobs or files which are toobe repaired.</span></span>|  
|<span data-ttu-id="1ffc3-146">**/ManifestFile:<DriveManifestFile\>**</span><span class="sxs-lookup"><span data-stu-id="1ffc3-146">**/ManifestFile:<DriveManifestFile\>**</span></span>|<span data-ttu-id="1ffc3-147">選用。</span><span class="sxs-lookup"><span data-stu-id="1ffc3-147">Optional.</span></span> <span data-ttu-id="1ffc3-148">hello 路徑 toohello 匯出磁碟機的資訊清單檔案。</span><span class="sxs-lookup"><span data-stu-id="1ffc3-148">hello path toohello export drive's manifest file.</span></span> <span data-ttu-id="1ffc3-149">這個檔案是 hello Windows Azure 匯入/匯出服務所產生，而且儲存 hello 匯出磁碟機，並選擇性地在 hello 與 hello 工作相關聯的儲存體帳戶中的 blob。</span><span class="sxs-lookup"><span data-stu-id="1ffc3-149">This file is generated by hello Windows Azure Import/Export service and stored on hello export drive, and optionally in a blob in hello storage account associated with hello job.</span></span><br /><br /> <span data-ttu-id="1ffc3-150">hello hello hello 匯出磁碟機上的檔案的內容將會驗證與此檔案包含 hello MD5 雜湊。</span><span class="sxs-lookup"><span data-stu-id="1ffc3-150">hello content of hello files on hello export drive will be verified with hello MD5 hashes contained in this file.</span></span> <span data-ttu-id="1ffc3-151">決定的 toobe 損毀的檔案會下載並重寫 toohello 目標目錄。</span><span class="sxs-lookup"><span data-stu-id="1ffc3-151">Any files that are determined toobe corrupted will be downloaded and rewritten toohello target directories.</span></span>|  
  
## <a name="using-repairexport-mode-toocorrect-failed-exports"></a><span data-ttu-id="1ffc3-152">使用 RepairExport 模式 toocorrect 無法匯出</span><span class="sxs-lookup"><span data-stu-id="1ffc3-152">Using RepairExport mode toocorrect failed exports</span></span>  
<span data-ttu-id="1ffc3-153">您可以使用無法 tooexport hello Azure 匯入/匯出工具 toodownload 檔案。</span><span class="sxs-lookup"><span data-stu-id="1ffc3-153">You can use hello Azure Import/Export Tool toodownload files that failed tooexport.</span></span> <span data-ttu-id="1ffc3-154">hello 複製記錄檔會包含失敗 tooexport 的檔案清單。</span><span class="sxs-lookup"><span data-stu-id="1ffc3-154">hello copy log file will contain a list of files that failed tooexport.</span></span>  
  
<span data-ttu-id="1ffc3-155">hello 的匯出失敗的原因包括下列可能性 hello:</span><span class="sxs-lookup"><span data-stu-id="1ffc3-155">hello causes of export failures include hello following possibilities:</span></span>  
  
-   <span data-ttu-id="1ffc3-156">損壞的磁碟機</span><span class="sxs-lookup"><span data-stu-id="1ffc3-156">Damaged drives</span></span>  
  
-   <span data-ttu-id="1ffc3-157">hello hello 傳輸程序期間變更的儲存體帳戶金鑰</span><span class="sxs-lookup"><span data-stu-id="1ffc3-157">hello storage account key changed during hello transfer process</span></span>  
  
<span data-ttu-id="1ffc3-158">中的 toorun hello 工具**RepairExport**模式中，您必須先包含 hello 匯出的檔案 tooyour 電腦 tooconnect hello 磁碟機。</span><span class="sxs-lookup"><span data-stu-id="1ffc3-158">toorun hello tool in **RepairExport** mode, you first need tooconnect hello drive containing hello exported files tooyour computer.</span></span> <span data-ttu-id="1ffc3-159">接下來，執行 Azure 匯入/匯出工具，以 hello 指定 hello 路徑 toothat 磁碟機 hello`/d`參數。</span><span class="sxs-lookup"><span data-stu-id="1ffc3-159">Next, run hello Azure Import/Export Tool, specifying hello path toothat drive with hello `/d` parameter.</span></span> <span data-ttu-id="1ffc3-160">您也需要您下載的 toospecify hello 路徑 toohello 磁碟機的複製記錄檔。</span><span class="sxs-lookup"><span data-stu-id="1ffc3-160">You also need toospecify hello path toohello drive's copy log file that you downloaded.</span></span> <span data-ttu-id="1ffc3-161">hello 下方的下列命令列範例會執行 hello 工具 toorepair 失敗 tooexport 任何檔案：</span><span class="sxs-lookup"><span data-stu-id="1ffc3-161">hello following command line example below runs hello tool toorepair any files that failed tooexport:</span></span>  
  
```  
WAImportExport.exe RepairExport /r:C:\WAImportExport\9WM35C3U.rep /d:G:\ /sn:bobmediaaccount /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /CopyLogFile:C:\WAImportExport\9WM35C3U.log  
```  
  
<span data-ttu-id="1ffc3-162">hello 如下顯示的一個區塊中 hello blob 失敗 tooexport 複製記錄檔的範例：</span><span class="sxs-lookup"><span data-stu-id="1ffc3-162">hello following is an example of a copy log file that shows that one block in hello blob failed tooexport:</span></span>  
  
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
  
<span data-ttu-id="1ffc3-163">hello 複製記錄檔指出 hello Windows Azure 匯入/匯出服務將其中一個下載 hello 匯出磁碟機上的 hello blob 的區塊 toohello 檔案時發生失敗。</span><span class="sxs-lookup"><span data-stu-id="1ffc3-163">hello copy log file indicates that a failure occurred while hello Windows Azure Import/Export service was downloading one of hello blob's blocks toohello file on hello export drive.</span></span> <span data-ttu-id="1ffc3-164">hello hello 檔案成功，下載的其他元件，並已正確設定 hello 檔案長度。</span><span class="sxs-lookup"><span data-stu-id="1ffc3-164">hello other components of hello file downloaded successfully, and hello file length was correctly set.</span></span> <span data-ttu-id="1ffc3-165">在此情況下，hello 工具會開啟 hello hello 磁碟機上的檔案，請下載 hello 區塊從 hello 儲存體帳戶，並將它寫 toohello 檔案範圍從長度為 65536 位移 65536 開始。</span><span class="sxs-lookup"><span data-stu-id="1ffc3-165">In this case, hello tool will open hello file on hello drive, download hello block from hello storage account, and write it toohello file range starting from offset 65536 with length 65536.</span></span>  
  
## <a name="using-repairexport-toovalidate-drive-contents"></a><span data-ttu-id="1ffc3-166">使用 RepairExport toovalidate 磁碟機內容</span><span class="sxs-lookup"><span data-stu-id="1ffc3-166">Using RepairExport toovalidate drive contents</span></span>  
<span data-ttu-id="1ffc3-167">您也可以使用 Azure 匯入/匯出以 hello **RepairExport** hello 磁碟機上的選項 toovalidate hello 內容是否正確。</span><span class="sxs-lookup"><span data-stu-id="1ffc3-167">You can also use Azure Import/Export with hello **RepairExport** option toovalidate hello contents on hello drive are correct.</span></span> <span data-ttu-id="1ffc3-168">hello 每個匯出磁碟機上的資訊清單檔包含 hello hello 磁碟機內容的 md5。</span><span class="sxs-lookup"><span data-stu-id="1ffc3-168">hello manifest file on each export drive contains MD5s for hello contents of hello drive.</span></span>  
  
<span data-ttu-id="1ffc3-169">hello Azure 匯入/匯出服務也可以儲存 hello 資訊清單檔案 tooa 儲存體帳戶期間 hello 匯出程序。</span><span class="sxs-lookup"><span data-stu-id="1ffc3-169">hello Azure Import/Export service can also save hello manifest files tooa storage account during hello export process.</span></span> <span data-ttu-id="1ffc3-170">hello hello 資訊清單檔案的位置可透過 hello [Get Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) hello 作業已完成的作業。</span><span class="sxs-lookup"><span data-stu-id="1ffc3-170">hello location of hello manifest files is available via hello [Get Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operation when hello job has completed.</span></span> <span data-ttu-id="1ffc3-171">請參閱[匯入/匯出服務資訊清單檔案格式](storage-import-export-file-format-metadata-and-properties.md)有關 hello 格式的磁碟機資訊清單檔案。</span><span class="sxs-lookup"><span data-stu-id="1ffc3-171">See [Import/Export service Manifest File Format](storage-import-export-file-format-metadata-and-properties.md) for more information about hello format of a drive manifest file.</span></span>  
  
<span data-ttu-id="1ffc3-172">hello 下列範例示範如何 toorun hello 以 hello 的 Azure 匯入/匯出工具**/ManifestFile**和**/CopyLogFile**參數：</span><span class="sxs-lookup"><span data-stu-id="1ffc3-172">hello following example shows how toorun hello Azure Import/Export Tool with hello **/ManifestFile** and **/CopyLogFile** parameters:</span></span>  
  
```  
WAImportExport.exe RepairExport /r:C:\WAImportExport\9WM35C3U.rep /d:G:\ /sn:bobmediaaccount /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /CopyLogFile:C:\WAImportExport\9WM35C3U.log /ManifestFile:G:\9WM35C3U.manifest  
```  
  
<span data-ttu-id="1ffc3-173">hello 以下是範例資訊清單檔案：</span><span class="sxs-lookup"><span data-stu-id="1ffc3-173">hello following is an example of a manifest file:</span></span>  
  
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
  
<span data-ttu-id="1ffc3-174">分頁裝訂的 hello 修復程序之後, hello 工具會透過參考 hello 資訊清單檔中每個檔案讀取，並確認 hello 檔案的完整性與 hello MD5 雜湊。</span><span class="sxs-lookup"><span data-stu-id="1ffc3-174">After finishing hello repair process, hello tool will read through each file referenced in hello manifest file and verify hello file's integrity with hello MD5 hashes.</span></span> <span data-ttu-id="1ffc3-175">對於上述的 hello 資訊清單，它將會經歷下列元件的 hello。</span><span class="sxs-lookup"><span data-stu-id="1ffc3-175">For hello manifest above, it will go through hello following components.</span></span>  

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

<span data-ttu-id="1ffc3-176">Hello 驗證失敗的任何元件會下載 hello 工具，而且重寫的 toohello 相同 hello 磁碟機的檔案。</span><span class="sxs-lookup"><span data-stu-id="1ffc3-176">Any component failing hello verification will be downloaded by hello tool and rewritten toohello same file on hello drive.</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="1ffc3-177">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1ffc3-177">Next steps</span></span>
 
* [<span data-ttu-id="1ffc3-178">正在設定 hello Azure 匯入/匯出工具</span><span class="sxs-lookup"><span data-stu-id="1ffc3-178">Setting Up hello Azure Import/Export Tool</span></span>](storage-import-export-tool-setup-v1.md)   
* [<span data-ttu-id="1ffc3-179">針對匯入作業準備硬碟</span><span class="sxs-lookup"><span data-stu-id="1ffc3-179">Preparing hard drives for an import job</span></span>](storage-import-export-tool-preparing-hard-drives-import-v1.md)   
* [<span data-ttu-id="1ffc3-180">利用複製記錄檔檢閱作業狀態</span><span class="sxs-lookup"><span data-stu-id="1ffc3-180">Reviewing job status with copy log files</span></span>](storage-import-export-tool-reviewing-job-status-v1.md)   
* [<span data-ttu-id="1ffc3-181">修復匯入作業</span><span class="sxs-lookup"><span data-stu-id="1ffc3-181">Repairing an import job</span></span>](storage-import-export-tool-repairing-an-import-job-v1.md)   
* [<span data-ttu-id="1ffc3-182">疑難排解 hello Azure 匯入/匯出工具</span><span class="sxs-lookup"><span data-stu-id="1ffc3-182">Troubleshooting hello Azure Import/Export Tool</span></span>](storage-import-export-tool-troubleshooting-v1.md)
