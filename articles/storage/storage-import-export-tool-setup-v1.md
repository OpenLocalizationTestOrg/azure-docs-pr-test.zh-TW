---
title: "向上 hello Azure 匯入/匯出工具 v1 aaaSetting |Microsoft 文件"
description: "了解組成 hello tooset 磁碟機準備及修復工具 hello Azure 匯入/匯出服務。 這是指 toov1 的 hello 匯入/匯出工具。"
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
ms.openlocfilehash: 4a737f2d2d0b1d00057e7fed6f9cf7b58e555b23
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="setting-up-hello-azure-importexport-tool"></a><span data-ttu-id="40fc7-104">設定 hello Azure 匯入/匯出工具</span><span class="sxs-lookup"><span data-stu-id="40fc7-104">Setting up hello Azure Import/Export Tool</span></span>
<span data-ttu-id="40fc7-105">hello Microsoft Azure 匯入/匯出工具是 hello 磁碟機準備及修復工具可讓您以 hello Microsoft Azure 匯入/匯出服務。</span><span class="sxs-lookup"><span data-stu-id="40fc7-105">hello Microsoft Azure Import/Export Tool is hello drive preparation and repair tool that you can use with hello Microsoft Azure Import/Export service.</span></span> <span data-ttu-id="40fc7-106">您可以使用下列函式的 hello hello 工具：</span><span class="sxs-lookup"><span data-stu-id="40fc7-106">You can use hello tool for hello following functions:</span></span>  
  
-   <span data-ttu-id="40fc7-107">在建立匯入工作之前，您可以使用此工具 toocopy 資料 toohello 硬碟要 tooship tooa Windows Azure 資料中心。</span><span class="sxs-lookup"><span data-stu-id="40fc7-107">Before creating an import job, you can use this tool toocopy data toohello hard drives you are going tooship tooa Windows Azure data center.</span></span>  
  
-   <span data-ttu-id="40fc7-108">匯入工作完成後，您可以使用此工具 toorepair 損毀、 遺漏或衝突的任何 blob 與其他 blob。</span><span class="sxs-lookup"><span data-stu-id="40fc7-108">After an import job has completed, you can use this tool toorepair any blobs that were corrupted, were missing, or conflicted with other blobs.</span></span>  
  
-   <span data-ttu-id="40fc7-109">您已完成的匯出工作收到 hello 磁碟機之後，您可以使用此工具 toorepair 任何檔案已損毀或遺失 hello 磁碟機上。</span><span class="sxs-lookup"><span data-stu-id="40fc7-109">After you receive hello drives from a completed export job, you can use this tool toorepair any files that were corrupted or missing on hello drives.</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="40fc7-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="40fc7-110">Prerequisites</span></span>  
<span data-ttu-id="40fc7-111">如果您正在匯入工作準備磁碟機，您需要下列必要條件 toomeet hello:</span><span class="sxs-lookup"><span data-stu-id="40fc7-111">If you are preparing drives for an import job, you will need toomeet hello following prerequisites:</span></span>  
  
-   <span data-ttu-id="40fc7-112">您必須擁有有效的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="40fc7-112">You must have an active Azure subscription.</span></span>  
  
-   <span data-ttu-id="40fc7-113">您的訂閱必須包含儲存體帳戶具有足夠的可用空間 toostore hello 檔案要 tooimport。</span><span class="sxs-lookup"><span data-stu-id="40fc7-113">Your subscription must include a storage account with enough available space toostore hello files you are going tooimport.</span></span>  
  
-   <span data-ttu-id="40fc7-114">您至少需要一個 hello 帳戶金鑰的 hello 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="40fc7-114">You need at least one of hello account keys for hello storage account.</span></span>  
  
-   <span data-ttu-id="40fc7-115">您需要 Windows 7、 Windows Server 2008 R2 或更新版本安裝 Windows 作業系統的電腦 (hello 「 複製電腦 」)。</span><span class="sxs-lookup"><span data-stu-id="40fc7-115">You need a computer (hello "copy machine") with Windows 7, Windows Server 2008 R2, or a newer Windows operating system installed.</span></span>  
  
-   <span data-ttu-id="40fc7-116">hello 複製電腦上必須安裝.NET Framework 4 hello。</span><span class="sxs-lookup"><span data-stu-id="40fc7-116">hello .NET Framework 4 must be installed on hello copy machine.</span></span>  
  
-   <span data-ttu-id="40fc7-117">必須在 hello 複製電腦上啟用 BitLocker。</span><span class="sxs-lookup"><span data-stu-id="40fc7-117">BitLocker must be enabled on hello copy machine.</span></span>  
  
-   <span data-ttu-id="40fc7-118">您必須包含資料 toobe 匯入的一或多個磁碟機，或空的 3.5 英寸 SATA 硬碟機連線 toohello 複製電腦。</span><span class="sxs-lookup"><span data-stu-id="40fc7-118">You will need one or more drives that contains data toobe imported or empty 3.5-inch SATA hard drives connected toohello copy machine.</span></span>  
  
-   <span data-ttu-id="40fc7-119">您計劃 tooimport hello 檔案必須能夠從 hello 複製電腦，存取，不論它們在網路共用或本機硬碟上。</span><span class="sxs-lookup"><span data-stu-id="40fc7-119">hello files you plan tooimport must be accessible from hello copy machine, whether they are on a network share or a local hard drive.</span></span> 
  
<span data-ttu-id="40fc7-120">如果您正嘗試 toorepair 匯入已有部分失敗，您需要：</span><span class="sxs-lookup"><span data-stu-id="40fc7-120">If you are attempting toorepair an import that has partially failed, you will need:</span></span>  
  
-   <span data-ttu-id="40fc7-121">hello 複製記錄檔</span><span class="sxs-lookup"><span data-stu-id="40fc7-121">hello copy log files</span></span>  
  
-   <span data-ttu-id="40fc7-122">hello 儲存體帳戶金鑰</span><span class="sxs-lookup"><span data-stu-id="40fc7-122">hello storage account key</span></span>  
  
  <span data-ttu-id="40fc7-123">如果您正嘗試 toorepair 已有部分失敗的匯出，您需要：</span><span class="sxs-lookup"><span data-stu-id="40fc7-123">If you are attempting toorepair an export that has partially failed, you will need:</span></span>  
  
-   <span data-ttu-id="40fc7-124">hello 複製記錄檔</span><span class="sxs-lookup"><span data-stu-id="40fc7-124">hello copy log files</span></span>  
  
-   <span data-ttu-id="40fc7-125">hello 資訊清單檔案 （選擇性）</span><span class="sxs-lookup"><span data-stu-id="40fc7-125">hello manifest files (optional)</span></span>  
  
-   <span data-ttu-id="40fc7-126">hello 儲存體帳戶金鑰</span><span class="sxs-lookup"><span data-stu-id="40fc7-126">hello storage account key</span></span>  
  
## <a name="installing-hello-azure-importexport-tool"></a><span data-ttu-id="40fc7-127">安裝 hello Azure 匯入/匯出工具</span><span class="sxs-lookup"><span data-stu-id="40fc7-127">Installing hello Azure Import/Export Tool</span></span>  
 <span data-ttu-id="40fc7-128">hello Azure 匯入/匯出工具包含下列檔案的 hello:</span><span class="sxs-lookup"><span data-stu-id="40fc7-128">hello Azure Import/Export Tool consists of hello following files:</span></span>  
  
-   <span data-ttu-id="40fc7-129">WAImportExport.exe</span><span class="sxs-lookup"><span data-stu-id="40fc7-129">WAImportExport.exe</span></span>  
  
-   <span data-ttu-id="40fc7-130">WAImportExport.exe.config</span><span class="sxs-lookup"><span data-stu-id="40fc7-130">WAImportExport.exe.config</span></span>  
  
-   <span data-ttu-id="40fc7-131">WAImportExportCore.dll</span><span class="sxs-lookup"><span data-stu-id="40fc7-131">WAImportExportCore.dll</span></span>  
  
-   <span data-ttu-id="40fc7-132">WAImportExportRepair.dll</span><span class="sxs-lookup"><span data-stu-id="40fc7-132">WAImportExportRepair.dll</span></span>  
  
-   <span data-ttu-id="40fc7-133">Microsoft.WindowsAzure.Storage.dll</span><span class="sxs-lookup"><span data-stu-id="40fc7-133">Microsoft.WindowsAzure.Storage.dll</span></span>  
  
-   <span data-ttu-id="40fc7-134">Hddid.dll</span><span class="sxs-lookup"><span data-stu-id="40fc7-134">Hddid.dll</span></span>  
  
 <span data-ttu-id="40fc7-135">複製這些檔案 tooa 工作目錄，例如`c:\WAImportExport`。</span><span class="sxs-lookup"><span data-stu-id="40fc7-135">Copy these files tooa working directory, for example, `c:\WAImportExport`.</span></span> <span data-ttu-id="40fc7-136">接下來，以系統管理員模式開啟命令列視窗中，並將 hello 上述目錄設為目前的目錄。</span><span class="sxs-lookup"><span data-stu-id="40fc7-136">Next, open a command line window in Administrator mode, and set hello above directory as current directory.</span></span>  
  
 <span data-ttu-id="40fc7-137">hello 命令，執行不含參數的 hello 工具 toooutput 說明：</span><span class="sxs-lookup"><span data-stu-id="40fc7-137">toooutput help for hello command, run hello tool without parameters:</span></span>  
  
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
        - Required. Path toohello journal file. Each drive must have one and only one  
          journal file. hello journal file corresponding toohello target drive must always  
          be specified.  
    /logdir:<LogDirectory>  
        - Optional. hello log directory. Verbose log files as well as some temporary  
          files will be written toothis directory. If not specified, current directory  
          will be used as hello log directory.  
    /id:<SessionId>  
        - Required. hello session Id is used tooidentify a copy session. It is used too 
          ensure accurate recovery of an interrupted copy session. In addition, files  
          that are copied in a copy session are stored in a directory named after hello  
          session Id on hello target drive.  
    /resumesession  
        - Optional. If hello last copy session was terminated abnormally, this parameter  
          can be specified tooresume hello session.  
    /abortsession  
        - Optional. If hello last copy session was terminated abnormally, this parameter  
          can be specified tooabort hello session.  
    /sn:<StorageAccountName>  
        - Required. Only applicable for RepairImport and RepairExport. hello name of  
          hello storage account.  
    /sk:<StorageAccountKey>  
        - Optional. hello key of hello storage account. One of /sk: and /csas: must be  
          specified.  
    /csas:<ContainerSas>  
        - Optional. A container SAS, in format of <ContainerName>?<SasString>, toobe  
          used for import hello data. One of /sk: and /csas: must be specified.  
    /t:<TargetDriveLetter>  
        - Required. Drive letter of hello target drive.  
    /r:<RepairFile>  
        - Required. Only applicable for RepairImport and RepairExport.  
          Path toohello file for tracking repair progress. Each drive must have one  
          and only one repair file.  
    /d:<TargetDirectories>  
        - Required. Only applicable for RepairImport and RepairExport.  
          For RepairImport, one or more semicolon-separated directories toorepair;  
          For RepairExport, one directory toorepair, e.g. root directory of hello drive.  
    /format  
        - Optional. If specified, hello target drive will be formatted. DO NOT specify  
          this parameter if you do not want tooformat hello drive.  
    /silentmode  
        - Optional. If not specified, hello /format parameter will require a confirmation  
          from console before hello tool formats hello drive. If this parameter is specified,  
          not confirmation will be given for formatting hello drive.  
    /encrypt  
        - Optional. If specified, hello target drive will be encrypted with BitLocker.  
          If hello drive has already been encrypted with BitLocker, do not specify this  
          parameter and instead specify hello BitLocker key using hello "/k" parameter.  
    /bk:<BitLockerKey>  
        - Optional. hello current BitLocker key if hello drive has already been encrypted  
          with BitLocker.  
    /Disposition:<Disposition>  
        - Optional. Specifies hello behavior when a blob with hello same path as hello one  
          being imported already exists. Valid values are: rename, no-overwrite and  
          overwrite (case-sensitive). If not specified, "rename" will be used as hello  
          default value.  
    /BlobType:<BlobType>  
        - Optional. hello blob type for hello imported blob(s). Valid values are BlockBlob  
          and PageBlob. If not specified, BlockBlob will be used as hello default value.  
    /PropertyFile:<PropertyFile>  
        - Optional. Path toohello property file for hello file(s) toobe imported.  
    /MetadataFile:<MetadataFile>  
        - Optional. Path toohello metadata file for hello file(s) toobe imported.  
    /CopyLogFile:<DriveCopyLogFile>  
        - Required. Only applicable for RepairImport and RepairExport. Path toohello  
          drive copy log file (verbose or error).  
    /ManifestFile:<DriveManifestFile>  
        - Required. Only applicable for RepairExport. Path toohello drive manifest file.  
    /PathMapFile:<DrivePathMapFile>  
        - Optional. Only applicable for RepairImport. Path toohello file containing  
          mappings of file paths relative toohello drive root toolocations of actual files  
          (tab-delimited). When first specified, it will be populated with file paths  
          with empty targets, which means either they are not found in TargetDirectories,  
          access denied, with invalid name, or they exist in multiple directories. hello  
          path map file can be manually edited tooinclude hello correct target paths and  
          specified again for hello tool tooresolve hello file paths correctly.  
    /ExportBlobListFile:<ExportBlobListFile>  
        - Required. Path toohello XML file containing list of blob paths or blob path  
          prefixes for hello blobs toobe exported. hello file format is hello same as hello  
          blob list blob format in hello Put Job operation of hello Import/Export service  
          REST API.  
    /DriveSize:<DriveSize>  
        - Required. Size of drives toobe used for export. For example, 500GB, 1.5TB.  
          Note: 1 GB = 1,000,000,000 bytes  
                1 TB = 1,000,000,000,000 bytes  
    /srcdir:<SourceDirectory>  
        - Required. Source directory that contains files toobe copied toohello  
          target drives.  
    /dstdir:<DestinationBlobVirtualDirectory>  
        - Required. Destination blob virtual directory toowhich hello files will  
          be imported.  
    /srcfile:<SourceFilePath>  
        - Required. Path toohello source file toobe imported.  
    /dstblob:<DestinationBlobPath>  
        - Required. Destination blob path for hello file toobe imported.  
    /skipwrite
        - Optional. tooskip write process. Used for inplace data drive preparation.
          Be sure tooreserve enough space (3 GB per 7TB) for drive manifest file!
Examples:  
  
    Copy a source directory tooa drive:  
    WAImportExport.exe PrepImport  
        /j:9WM35C2V.jrn /id:session#1 /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GEL  
        xmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /t:x /format /encrypt /srcdir:d:\movi  
        es\drama /dstdir:movies/drama/  
  
    Copy another directory toohello same drive following hello above command:  
    WAImportExport.exe PrepImport  
        /j:9WM35C2V.jrn /id:session#2 /srcdir:d:\movies\action /dstdir:movies/action/  
  
    Copy another file toohello same drive following hello above commands:  
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
  
## <a name="next-steps"></a><span data-ttu-id="40fc7-138">後續步驟</span><span class="sxs-lookup"><span data-stu-id="40fc7-138">Next steps</span></span>

* [<span data-ttu-id="40fc7-139">針對匯入作業準備硬碟</span><span class="sxs-lookup"><span data-stu-id="40fc7-139">Preparing hard drives for an import job</span></span>](storage-import-export-tool-preparing-hard-drives-import-v1.md)   
* [<span data-ttu-id="40fc7-140">預覽匯出作業的磁碟機使用量</span><span class="sxs-lookup"><span data-stu-id="40fc7-140">Previewing Drive usage for an export job</span></span>](storage-import-export-tool-previewing-drive-usage-export-v1.md)   
* [<span data-ttu-id="40fc7-141">利用複製記錄檔檢閱作業狀態</span><span class="sxs-lookup"><span data-stu-id="40fc7-141">Reviewing job status with copy log files</span></span>](storage-import-export-tool-reviewing-job-status-v1.md)   
* [<span data-ttu-id="40fc7-142">修復匯入作業</span><span class="sxs-lookup"><span data-stu-id="40fc7-142">Repairing an import job</span></span>](storage-import-export-tool-repairing-an-import-job-v1.md)   
* [<span data-ttu-id="40fc7-143">修復匯出作業</span><span class="sxs-lookup"><span data-stu-id="40fc7-143">Repairing an export job</span></span>](storage-import-export-tool-repairing-an-export-job-v1.md)   
* [<span data-ttu-id="40fc7-144">疑難排解 hello Azure 匯入/匯出工具</span><span class="sxs-lookup"><span data-stu-id="40fc7-144">Troubleshooting hello Azure Import/Export Tool</span></span>](storage-import-export-tool-troubleshooting-v1.md)
