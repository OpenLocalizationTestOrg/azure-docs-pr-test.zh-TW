---
title: "設定 Azure 匯入/匯出工具 v1 | Microsoft Docs"
description: "了解如何設定 Azure 匯入/匯出服務的磁碟機準備及修復工具。 這是指 v1 的匯入/匯出工具。"
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: c312b1ab-5b9e-4d24-becd-790a88b3ba8d
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/15/2017
ms.author: muralikk
ms.openlocfilehash: 4fb4c7e39c0385cae7c7984eb774d6a468ee18e4
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="setting-up-the-azure-importexport-tool"></a><span data-ttu-id="612f2-104">設定 Azure 匯入/匯出工具</span><span class="sxs-lookup"><span data-stu-id="612f2-104">Setting up the Azure Import/Export Tool</span></span>
<span data-ttu-id="612f2-105">Microsoft Azure 匯入/匯出工具是磁碟機準備及修復工具，可搭配 Microsoft Azure 匯入/匯出服務使用。</span><span class="sxs-lookup"><span data-stu-id="612f2-105">The Microsoft Azure Import/Export Tool is the drive preparation and repair tool that you can use with the Microsoft Azure Import/Export service.</span></span> <span data-ttu-id="612f2-106">您可以使用此工具來執行下列功能︰</span><span class="sxs-lookup"><span data-stu-id="612f2-106">You can use the tool for the following functions:</span></span>  
  
-   <span data-ttu-id="612f2-107">在建立匯入工作之前，您可以使用此工具，將資料複製到要寄送至 Windows Azure 資料中心的硬碟。</span><span class="sxs-lookup"><span data-stu-id="612f2-107">Before creating an import job, you can use this tool to copy data to the hard drives you are going to ship to a Windows Azure data center.</span></span>  
  
-   <span data-ttu-id="612f2-108">匯入工作完成後，您可以使用此工具來修復損毀、遺漏或與其他 Blob 衝突的任何 Blob。</span><span class="sxs-lookup"><span data-stu-id="612f2-108">After an import job has completed, you can use this tool to repair any blobs that were corrupted, were missing, or conflicted with other blobs.</span></span>  
  
-   <span data-ttu-id="612f2-109">當您收到已完成的匯出工作中的磁碟機後，您可以使用此工具來修復磁碟機上損毀或遺漏的任何檔案。</span><span class="sxs-lookup"><span data-stu-id="612f2-109">After you receive the drives from a completed export job, you can use this tool to repair any files that were corrupted or missing on the drives.</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="612f2-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="612f2-110">Prerequisites</span></span>  
<span data-ttu-id="612f2-111">如果您要準備匯入作業的磁碟機，您必須符合下列必要條件︰</span><span class="sxs-lookup"><span data-stu-id="612f2-111">If you are preparing drives for an import job, you will need to meet the following prerequisites:</span></span>  
  
-   <span data-ttu-id="612f2-112">您必須擁有有效的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="612f2-112">You must have an active Azure subscription.</span></span>  
  
-   <span data-ttu-id="612f2-113">您的訂用帳戶必須包含可用空間足夠儲存您要匯入之檔案的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="612f2-113">Your subscription must include a storage account with enough available space to store the files you are going to import.</span></span>  
  
-   <span data-ttu-id="612f2-114">您需要至少一個儲存體帳戶的帳戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="612f2-114">You need at least one of the account keys for the storage account.</span></span>  
  
-   <span data-ttu-id="612f2-115">您需要安裝 Windows 7、Windows Server 2008 R2 或更新版本 Windows 作業系統的電腦 (「複製電腦」)。</span><span class="sxs-lookup"><span data-stu-id="612f2-115">You need a computer (the "copy machine") with Windows 7, Windows Server 2008 R2, or a newer Windows operating system installed.</span></span>  
  
-   <span data-ttu-id="612f2-116">複製電腦上必須安裝 .NET Framework 4。</span><span class="sxs-lookup"><span data-stu-id="612f2-116">The .NET Framework 4 must be installed on the copy machine.</span></span>  
  
-   <span data-ttu-id="612f2-117">複製電腦上必須啟用 BitLocker。</span><span class="sxs-lookup"><span data-stu-id="612f2-117">BitLocker must be enabled on the copy machine.</span></span>  
  
-   <span data-ttu-id="612f2-118">您將需要一個或多個包含要匯入資料的磁碟機，或連接至複製電腦的空白 3.5 吋 SATA 硬碟。</span><span class="sxs-lookup"><span data-stu-id="612f2-118">You will need one or more drives that contains data to be imported or empty 3.5-inch SATA hard drives connected to the copy machine.</span></span>  
  
-   <span data-ttu-id="612f2-119">您想匯入的檔案必須可從複製機器上存取，無論它們是在網路共用或本機硬碟上。</span><span class="sxs-lookup"><span data-stu-id="612f2-119">The files you plan to import must be accessible from the copy machine, whether they are on a network share or a local hard drive.</span></span> 
  
<span data-ttu-id="612f2-120">如果您嘗試修復已部分失敗的匯入，您將需要︰</span><span class="sxs-lookup"><span data-stu-id="612f2-120">If you are attempting to repair an import that has partially failed, you will need:</span></span>  
  
-   <span data-ttu-id="612f2-121">複製記錄檔</span><span class="sxs-lookup"><span data-stu-id="612f2-121">The copy log files</span></span>  
  
-   <span data-ttu-id="612f2-122">儲存體帳戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="612f2-122">The storage account key</span></span>  
  
  <span data-ttu-id="612f2-123">如果您嘗試修復已部分失敗的匯出，您將需要︰</span><span class="sxs-lookup"><span data-stu-id="612f2-123">If you are attempting to repair an export that has partially failed, you will need:</span></span>  
  
-   <span data-ttu-id="612f2-124">複製記錄檔</span><span class="sxs-lookup"><span data-stu-id="612f2-124">The copy log files</span></span>  
  
-   <span data-ttu-id="612f2-125">資訊清單檔案 (選擇性)</span><span class="sxs-lookup"><span data-stu-id="612f2-125">The manifest files (optional)</span></span>  
  
-   <span data-ttu-id="612f2-126">儲存體帳戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="612f2-126">The storage account key</span></span>  
  
## <a name="installing-the-azure-importexport-tool"></a><span data-ttu-id="612f2-127">安裝 Azure 匯入/匯出工具</span><span class="sxs-lookup"><span data-stu-id="612f2-127">Installing the Azure Import/Export Tool</span></span>  
 <span data-ttu-id="612f2-128">Azure 匯入/匯出工具包含下列檔案：</span><span class="sxs-lookup"><span data-stu-id="612f2-128">The Azure Import/Export Tool consists of the following files:</span></span>  
  
-   <span data-ttu-id="612f2-129">WAImportExport.exe</span><span class="sxs-lookup"><span data-stu-id="612f2-129">WAImportExport.exe</span></span>  
  
-   <span data-ttu-id="612f2-130">WAImportExport.exe.config</span><span class="sxs-lookup"><span data-stu-id="612f2-130">WAImportExport.exe.config</span></span>  
  
-   <span data-ttu-id="612f2-131">WAImportExportCore.dll</span><span class="sxs-lookup"><span data-stu-id="612f2-131">WAImportExportCore.dll</span></span>  
  
-   <span data-ttu-id="612f2-132">WAImportExportRepair.dll</span><span class="sxs-lookup"><span data-stu-id="612f2-132">WAImportExportRepair.dll</span></span>  
  
-   <span data-ttu-id="612f2-133">Microsoft.WindowsAzure.Storage.dll</span><span class="sxs-lookup"><span data-stu-id="612f2-133">Microsoft.WindowsAzure.Storage.dll</span></span>  
  
-   <span data-ttu-id="612f2-134">Hddid.dll</span><span class="sxs-lookup"><span data-stu-id="612f2-134">Hddid.dll</span></span>  
  
 <span data-ttu-id="612f2-135">將這些檔案複製到工作目錄，例如，`c:\WAImportExport`。</span><span class="sxs-lookup"><span data-stu-id="612f2-135">Copy these files to a working directory, for example, `c:\WAImportExport`.</span></span> <span data-ttu-id="612f2-136">接下來，在系統管理員模式中開啟命令列視窗，並將上述目錄設為目前的目錄。</span><span class="sxs-lookup"><span data-stu-id="612f2-136">Next, open a command line window in Administrator mode, and set the above directory as current directory.</span></span>  
  
 <span data-ttu-id="612f2-137">若要輸出命令的說明，執行此工具而不包含參數︰</span><span class="sxs-lookup"><span data-stu-id="612f2-137">To output help for the command, run the tool without parameters:</span></span>  
  
```  
WAImportExport, a client tool for Microsoft Azure Import/Export service. Microsoft (c) 2013, 2014  
  
Copy a Directory:  
    WAImportExport.exe PrepImport  
        /j:<JournalFile> [/logdir:<LogDirectory>] [/id:<SessionId>] [/resumesession]  
        [/abortsession] [/sk:<StorageAccountKey>] [/csas:<ContainerSas>]  
        [/t:<TargetDriveLetter>] [/format] [/silentmode] [/encrypt]  
        [/bk:<BitLockerKey>] [/Disposition:<Disposition>] [/BlobType:<BlobType>]  
        [/PropertyFile:<PropertyFile>] [/MetadataFile:<MetadataFile>]  
        /srcdir:<SourceDirectory> /dstdir:<DestinationBlobVirtualDirectory>  
  
Copy a File:  
    WAImportExport.exe PrepImport  
        /j:<JournalFile> [/logdir:<LogDirectory>] [/id:<SessionId>] [/resumesession]  
        [/abortsession] [/sk:<StorageAccountKey>] [/csas:<ContainerSas>]  
        [/t:<TargetDriveLetter>] [/format] [/silentmode] [/encrypt]  
        [/bk:<BitLockerKey>] [/Disposition:<Disposition>] [/BlobType:<BlobType>]  
        [/PropertyFile:<PropertyFile>] [/MetadataFile:<MetadataFile>]  
        /srcfile:<SourceFilePath> /dstblob:<DestinationBlobPath>  
  
Repair a Drive:  
    WAImportExport.exe RepairImport | RepairExport  
        /r:<RepairFile> [/logdir:<LogDirectory>]  
        [/d:<TargetDirectories>] [/bk:<BitLockerKey>]  
        /sn:<StorageAccountName> [/sk:<StorageAccountKey> | /csas:<ContainerSas>]  
        [/CopyLogFile:<DriveCopyLogFile>] [/ManifestFile:<DriveManifestFile>]  
        [/PathMapFile:<DrivePathMapFile>]  
  
Preview an Export Job:  
    WAImportExport.exe PreviewExport  
        [/logdir:<LogDirectory>]  
        /sn:<StorageAccountName> [/sk:<StorageAccountKey> | /csas:<ContainerSas>]  
        /ExportBlobListFile:<ExportBlobListFile> /DriveSize:<DriveSize>  
  
Parameters:  
  
    /j:<JournalFile>  
        - Required. Path to the journal file. Each drive must have one and only one  
          journal file. The journal file corresponding to the target drive must always  
          be specified.  
    /logdir:<LogDirectory>  
        - Optional. The log directory. Verbose log files as well as some temporary  
          files will be written to this directory. If not specified, current directory  
          will be used as the log directory.  
    /id:<SessionId>  
        - Required. The session Id is used to identify a copy session. It is used to  
          ensure accurate recovery of an interrupted copy session. In addition, files  
          that are copied in a copy session are stored in a directory named after the  
          session Id on the target drive.  
    /resumesession  
        - Optional. If the last copy session was terminated abnormally, this parameter  
          can be specified to resume the session.  
    /abortsession  
        - Optional. If the last copy session was terminated abnormally, this parameter  
          can be specified to abort the session.  
    /sn:<StorageAccountName>  
        - Required. Only applicable for RepairImport and RepairExport. The name of  
          the storage account.  
    /sk:<StorageAccountKey>  
        - Optional. The key of the storage account. One of /sk: and /csas: must be  
          specified.  
    /csas:<ContainerSas>  
        - Optional. A container SAS, in format of <ContainerName>?<SasString>, to be  
          used for import the data. One of /sk: and /csas: must be specified.  
    /t:<TargetDriveLetter>  
        - Required. Drive letter of the target drive.  
    /r:<RepairFile>  
        - Required. Only applicable for RepairImport and RepairExport.  
          Path to the file for tracking repair progress. Each drive must have one  
          and only one repair file.  
    /d:<TargetDirectories>  
        - Required. Only applicable for RepairImport and RepairExport.  
          For RepairImport, one or more semicolon-separated directories to repair;  
          For RepairExport, one directory to repair, e.g. root directory of the drive.  
    /format  
        - Optional. If specified, the target drive will be formatted. DO NOT specify  
          this parameter if you do not want to format the drive.  
    /silentmode  
        - Optional. If not specified, the /format parameter will require a confirmation  
          from console before the tool formats the drive. If this parameter is specified,  
          not confirmation will be given for formatting the drive.  
    /encrypt  
        - Optional. If specified, the target drive will be encrypted with BitLocker.  
          If the drive has already been encrypted with BitLocker, do not specify this  
          parameter and instead specify the BitLocker key using the "/k" parameter.  
    /bk:<BitLockerKey>  
        - Optional. The current BitLocker key if the drive has already been encrypted  
          with BitLocker.  
    /Disposition:<Disposition>  
        - Optional. Specifies the behavior when a blob with the same path as the one  
          being imported already exists. Valid values are: rename, no-overwrite and  
          overwrite (case-sensitive). If not specified, "rename" will be used as the  
          default value.  
    /BlobType:<BlobType>  
        - Optional. The blob type for the imported blob(s). Valid values are BlockBlob  
          and PageBlob. If not specified, BlockBlob will be used as the default value.  
    /PropertyFile:<PropertyFile>  
        - Optional. Path to the property file for the file(s) to be imported.  
    /MetadataFile:<MetadataFile>  
        - Optional. Path to the metadata file for the file(s) to be imported.  
    /CopyLogFile:<DriveCopyLogFile>  
        - Required. Only applicable for RepairImport and RepairExport. Path to the  
          drive copy log file (verbose or error).  
    /ManifestFile:<DriveManifestFile>  
        - Required. Only applicable for RepairExport. Path to the drive manifest file.  
    /PathMapFile:<DrivePathMapFile>  
        - Optional. Only applicable for RepairImport. Path to the file containing  
          mappings of file paths relative to the drive root to locations of actual files  
          (tab-delimited). When first specified, it will be populated with file paths  
          with empty targets, which means either they are not found in TargetDirectories,  
          access denied, with invalid name, or they exist in multiple directories. The  
          path map file can be manually edited to include the correct target paths and  
          specified again for the tool to resolve the file paths correctly.  
    /ExportBlobListFile:<ExportBlobListFile>  
        - Required. Path to the XML file containing list of blob paths or blob path  
          prefixes for the blobs to be exported. The file format is the same as the  
          blob list blob format in the Put Job operation of the Import/Export service  
          REST API.  
    /DriveSize:<DriveSize>  
        - Required. Size of drives to be used for export. For example, 500GB, 1.5TB.  
          Note: 1 GB = 1,000,000,000 bytes  
                1 TB = 1,000,000,000,000 bytes  
    /srcdir:<SourceDirectory>  
        - Required. Source directory that contains files to be copied to the  
          target drives.  
    /dstdir:<DestinationBlobVirtualDirectory>  
        - Required. Destination blob virtual directory to which the files will  
          be imported.  
    /srcfile:<SourceFilePath>  
        - Required. Path to the source file to be imported.  
    /dstblob:<DestinationBlobPath>  
        - Required. Destination blob path for the file to be imported.  
    /skipwrite
        - Optional. To skip write process. Used for inplace data drive preparation.
          Be sure to reserve enough space (3 GB per 7TB) for drive manifest file!
Examples:  
  
    Copy a source directory to a drive:  
    WAImportExport.exe PrepImport  
        /j:9WM35C2V.jrn /id:session#1 /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GEL  
        xmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /t:x /format /encrypt /srcdir:d:\movi  
        es\drama /dstdir:movies/drama/  
  
    Copy another directory to the same drive following the above command:  
    WAImportExport.exe PrepImport  
        /j:9WM35C2V.jrn /id:session#2 /srcdir:d:\movies\action /dstdir:movies/action/  
  
    Copy another file to the same drive following the above commands:  
    WAImportExport.exe PrepImport  
        /j:9WM35C2V.jrn /id:session#3 /srcfile:d:\movies\dvd.vhd /dstblob:movies/dvd.vhd /BlobType:PageBlob  
  
    Preview how many 1.5 TB drives are needed for an export job:  
    WAImportExport.exe PreviewExport  
        /sn:mytestaccount /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7K  
        ysbbeKLDksg7VoN1W/a5UuM2zNgQ== /ExportBlobListFile:C:\temp\myexportbloblist.xml  
        /DriveSize:1.5TB  
  
    Repair an finished import job:  
    WAImportExport.exe RepairImport  
        /r:9WM35C2V.rep /d:X:\ /bk:442926-020713-108086-436744-137335-435358-242242-2795  
        98 /sn:mytestaccount /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94  
        f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /CopyLogFile:C:\temp\9WM35C2V_error.log 

    Skip write process, inplace data drive preparation:
    WAImportExport.exe PrepImport
        /j:9WM35C2V.jrn /id:session#1 /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GEL
        xmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /t:d /encrypt /srcdir:d:\movi
        es\drama /dstdir:movies/drama/ /skipwrite
```  
  
## <a name="next-steps"></a><span data-ttu-id="612f2-138">後續步驟</span><span class="sxs-lookup"><span data-stu-id="612f2-138">Next steps</span></span>

* [<span data-ttu-id="612f2-139">針對匯入作業準備硬碟</span><span class="sxs-lookup"><span data-stu-id="612f2-139">Preparing hard drives for an import job</span></span>](../storage-import-export-tool-preparing-hard-drives-import-v1.md)   
* [<span data-ttu-id="612f2-140">預覽匯出作業的磁碟機使用量</span><span class="sxs-lookup"><span data-stu-id="612f2-140">Previewing Drive usage for an export job</span></span>](../storage-import-export-tool-previewing-drive-usage-export-v1.md)   
* [<span data-ttu-id="612f2-141">利用複製記錄檔檢閱作業狀態</span><span class="sxs-lookup"><span data-stu-id="612f2-141">Reviewing job status with copy log files</span></span>](../storage-import-export-tool-reviewing-job-status-v1.md)   
* [<span data-ttu-id="612f2-142">修復匯入作業</span><span class="sxs-lookup"><span data-stu-id="612f2-142">Repairing an import job</span></span>](../storage-import-export-tool-repairing-an-import-job-v1.md)   
* [<span data-ttu-id="612f2-143">修復匯出作業</span><span class="sxs-lookup"><span data-stu-id="612f2-143">Repairing an export job</span></span>](../storage-import-export-tool-repairing-an-export-job-v1.md)   
* [<span data-ttu-id="612f2-144">針對 Azure 匯入/匯出工具進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="612f2-144">Troubleshooting the Azure Import/Export Tool</span></span>](storage-import-export-tool-troubleshooting-v1.md)
