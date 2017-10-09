---
title: "向上 hello Azure 匯入/匯出工具 aaaSetting |Microsoft 文件"
description: "了解組成 hello tooset 磁碟機準備及修復工具 hello Azure 匯入/匯出服務。"
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: muralikk
ms.openlocfilehash: ee5bb99bd84ea5ee2f6b6e99c5a375b215e94ea8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="setting-up-hello-azure-importexport-tool"></a><span data-ttu-id="21c7d-103">設定 hello Azure 匯入/匯出工具</span><span class="sxs-lookup"><span data-stu-id="21c7d-103">Setting up hello Azure Import/Export Tool</span></span>

<span data-ttu-id="21c7d-104">hello Microsoft Azure 匯入/匯出工具是 hello 磁碟機準備及修復工具可讓您以 hello Microsoft Azure 匯入/匯出服務。</span><span class="sxs-lookup"><span data-stu-id="21c7d-104">hello Microsoft Azure Import/Export Tool is hello drive preparation and repair tool that you can use with hello Microsoft Azure Import/Export service.</span></span> <span data-ttu-id="21c7d-105">您可以使用下列函式的 hello hello 工具：</span><span class="sxs-lookup"><span data-stu-id="21c7d-105">You can use hello tool for hello following functions:</span></span>

* <span data-ttu-id="21c7d-106">在建立匯入工作之前，您可以使用此工具 toocopy 資料 toohello 硬碟要 tooship tooan Azure 資料中心。</span><span class="sxs-lookup"><span data-stu-id="21c7d-106">Before creating an import job, you can use this tool toocopy data toohello hard drives you are going tooship tooan Azure data center.</span></span>
* <span data-ttu-id="21c7d-107">匯入工作完成後，您可以使用此工具 toorepair 損毀、 遺漏或衝突的任何 blob 與其他 blob。</span><span class="sxs-lookup"><span data-stu-id="21c7d-107">After an import job has completed, you can use this tool toorepair any blobs that were corrupted, were missing, or conflicted with other blobs.</span></span>
* <span data-ttu-id="21c7d-108">您已完成的匯出工作收到 hello 磁碟機之後，您可以使用此工具 toorepair 任何檔案已損毀或遺失 hello 磁碟機上。</span><span class="sxs-lookup"><span data-stu-id="21c7d-108">After you receive hello drives from a completed export job, you can use this tool toorepair any files that were corrupted or missing on hello drives.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="21c7d-109">必要條件</span><span class="sxs-lookup"><span data-stu-id="21c7d-109">Prerequisites</span></span>

<span data-ttu-id="21c7d-110">如果您是**來準備磁碟機**匯入工作，必須符合下列必要條件 hello:</span><span class="sxs-lookup"><span data-stu-id="21c7d-110">If you are **preparing drives** for an import job, hello following prerequisites must be met:</span></span>

* <span data-ttu-id="21c7d-111">您必須擁有有效的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="21c7d-111">You must have an active Azure subscription.</span></span>
* <span data-ttu-id="21c7d-112">您的訂閱必須包含儲存體帳戶具有足夠的可用空間 toostore hello 檔案要 tooimport。</span><span class="sxs-lookup"><span data-stu-id="21c7d-112">Your subscription must include a storage account with enough available space toostore hello files you are going tooimport.</span></span>
* <span data-ttu-id="21c7d-113">您必須至少一個 hello 儲存體帳戶存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="21c7d-113">You need at least one of hello storage account access keys.</span></span>
* <span data-ttu-id="21c7d-114">您需要 Windows 7、 Windows Server 2008 R2 或更新版本安裝 Windows 作業系統的電腦 (hello 「 複製電腦 」)。</span><span class="sxs-lookup"><span data-stu-id="21c7d-114">You need a computer (hello "copy machine") with Windows 7, Windows Server 2008 R2, or a newer Windows operating system installed.</span></span>
* <span data-ttu-id="21c7d-115">hello 複製電腦上必須安裝.NET Framework 4 hello。</span><span class="sxs-lookup"><span data-stu-id="21c7d-115">hello .NET Framework 4 must be installed on hello copy machine.</span></span>
* <span data-ttu-id="21c7d-116">必須在 hello 複製電腦上啟用 BitLocker。</span><span class="sxs-lookup"><span data-stu-id="21c7d-116">BitLocker must be enabled on hello copy machine.</span></span>
* <span data-ttu-id="21c7d-117">您需要一個或多個空 3.5 吋 SATA 硬碟連接 toohello 複製電腦。</span><span class="sxs-lookup"><span data-stu-id="21c7d-117">You need one or more empty 3.5-inch SATA hard drives connected toohello copy machine.</span></span>
* <span data-ttu-id="21c7d-118">您計劃 tooimport hello 檔案必須能夠從 hello 複製電腦，存取，不論它們在網路共用或本機硬碟上。</span><span class="sxs-lookup"><span data-stu-id="21c7d-118">hello files you plan tooimport must be accessible from hello copy machine, whether they are on a network share or a local hard drive.</span></span>

<span data-ttu-id="21c7d-119">若您嘗試過**修復匯入**已有部分失敗，您需要：</span><span class="sxs-lookup"><span data-stu-id="21c7d-119">If you are attempting too**repair an import** that has partially failed, you need:</span></span>

* <span data-ttu-id="21c7d-120">hello 複製記錄檔</span><span class="sxs-lookup"><span data-stu-id="21c7d-120">hello copy log files</span></span>
* <span data-ttu-id="21c7d-121">hello 儲存體帳戶金鑰</span><span class="sxs-lookup"><span data-stu-id="21c7d-121">hello storage account key</span></span>

<span data-ttu-id="21c7d-122">若您嘗試過**修復匯出**已有部分失敗，您需要：</span><span class="sxs-lookup"><span data-stu-id="21c7d-122">If you are attempting too**repair an export**  that has partially failed, you need:</span></span>

* <span data-ttu-id="21c7d-123">hello 複製記錄檔</span><span class="sxs-lookup"><span data-stu-id="21c7d-123">hello copy log files</span></span>
* <span data-ttu-id="21c7d-124">hello 資訊清單檔案 （選擇性）</span><span class="sxs-lookup"><span data-stu-id="21c7d-124">hello manifest files (optional)</span></span>
* <span data-ttu-id="21c7d-125">hello 儲存體帳戶金鑰</span><span class="sxs-lookup"><span data-stu-id="21c7d-125">hello storage account key</span></span>

## <a name="installing-hello-azure-importexport-tool"></a><span data-ttu-id="21c7d-126">安裝 hello Azure 匯入/匯出工具</span><span class="sxs-lookup"><span data-stu-id="21c7d-126">Installing hello Azure Import/Export Tool</span></span>

<span data-ttu-id="21c7d-127">首先，[下載 hello Azure 匯入/匯出工具](https://www.microsoft.com/download/details.aspx?id=55280)並將它解壓縮 tooa 目錄，您在電腦上，例如`c:\WAImportExport`。</span><span class="sxs-lookup"><span data-stu-id="21c7d-127">First, [download hello Azure Import/Export Tool](https://www.microsoft.com/download/details.aspx?id=55280) and extract it tooa directory on your computer, for example `c:\WAImportExport`.</span></span>

<span data-ttu-id="21c7d-128">hello Azure 匯入/匯出工具包含下列檔案的 hello:</span><span class="sxs-lookup"><span data-stu-id="21c7d-128">hello Azure Import/Export Tool consists of hello following files:</span></span>

* <span data-ttu-id="21c7d-129">dataset.csv</span><span class="sxs-lookup"><span data-stu-id="21c7d-129">dataset.csv</span></span>
* <span data-ttu-id="21c7d-130">driveset.csv</span><span class="sxs-lookup"><span data-stu-id="21c7d-130">driveset.csv</span></span>
* <span data-ttu-id="21c7d-131">hddid.dll</span><span class="sxs-lookup"><span data-stu-id="21c7d-131">hddid.dll</span></span>
* <span data-ttu-id="21c7d-132">Microsoft.Data.Services.Client.dll</span><span class="sxs-lookup"><span data-stu-id="21c7d-132">Microsoft.Data.Services.Client.dll</span></span>
* <span data-ttu-id="21c7d-133">Microsoft.WindowsAzure.Storage.dll</span><span class="sxs-lookup"><span data-stu-id="21c7d-133">Microsoft.WindowsAzure.Storage.dll</span></span>
* <span data-ttu-id="21c7d-134">Microsoft.WindowsAzure.Storage.pdb</span><span class="sxs-lookup"><span data-stu-id="21c7d-134">Microsoft.WindowsAzure.Storage.pdb</span></span>
* <span data-ttu-id="21c7d-135">Microsoft.WindowsAzure.Storage.xml</span><span class="sxs-lookup"><span data-stu-id="21c7d-135">Microsoft.WindowsAzure.Storage.xml</span></span>
* <span data-ttu-id="21c7d-136">WAImportExport.exe</span><span class="sxs-lookup"><span data-stu-id="21c7d-136">WAImportExport.exe</span></span>
* <span data-ttu-id="21c7d-137">WAImportExport.exe.config</span><span class="sxs-lookup"><span data-stu-id="21c7d-137">WAImportExport.exe.config</span></span>
* <span data-ttu-id="21c7d-138">WAImportExport.pdb</span><span class="sxs-lookup"><span data-stu-id="21c7d-138">WAImportExport.pdb</span></span>
* <span data-ttu-id="21c7d-139">WAImportExportCore.dll</span><span class="sxs-lookup"><span data-stu-id="21c7d-139">WAImportExportCore.dll</span></span>
* <span data-ttu-id="21c7d-140">WAImportExportCore.pdb</span><span class="sxs-lookup"><span data-stu-id="21c7d-140">WAImportExportCore.pdb</span></span>
* <span data-ttu-id="21c7d-141">WAImportExportRepair.dll</span><span class="sxs-lookup"><span data-stu-id="21c7d-141">WAImportExportRepair.dll</span></span>
* <span data-ttu-id="21c7d-142">WAImportExportRepair.pdb</span><span class="sxs-lookup"><span data-stu-id="21c7d-142">WAImportExportRepair.pdb</span></span>

<span data-ttu-id="21c7d-143">接下來，開啟 命令提示字元視窗中的**系統管理員模式**，並變更到包含 hello hello 目錄解壓縮檔案。</span><span class="sxs-lookup"><span data-stu-id="21c7d-143">Next, open a Command Prompt window in **Administrator mode**, and change into hello directory containing hello extracted files.</span></span>

<span data-ttu-id="21c7d-144">toooutput hello 命令，執行 hello 工具說明 (`WAImportExport.exe`) 不含參數：</span><span class="sxs-lookup"><span data-stu-id="21c7d-144">toooutput help for hello command, run hello tool (`WAImportExport.exe`) without parameters:</span></span>

```
WAImportExport, a client tool for Windows Azure Import/Export Service. Microsoft (c) 2013


Copy directories and/or files with a new copy session:
    WAImportExport.exe PrepImport /j:<JournalFile> /id:<SessionId> [/logdir:<LogDirectory>]
        [/sk:<StorageAccountKey>] [/silentmode] [/InitialDriveSet:<driveset.csv>]
        DataSet:<dataset.csv>

Add more drives:
    WAImportExport.exe PrepImport /j:<JournalFile> /id:<SessionId> /AdditionalDriveSet:<driveset.csv>

Abort an interrupted copy session:
    WAImportExport.exe PrepImport /j:<JournalFile> /id:<SessionId> /AbortSession

Resume an interrupted copy session:
    WAImportExport.exe PrepImport /j:<JournalFile> /id:<SessionId> /ResumeSession

List drives:
    WAImportExport.exe PrepImport /j:<JournalFile> /ListDrives

List copy sessions:
    WAImportExport.exe PrepImport /j:<JournalFile> /ListCopySessions

Repair a Drive:
    WAImportExport.exe RepairImport | RepairExport
        /r:<RepairFile> [/logdir:<LogDirectory>]
        [/d:<TargetDirectories>] [/bk:<BitLockerKey>]
        /sn:<StorageAccountName> /sk:<StorageAccountKey>
        [/CopyLogFile:<DriveCopyLogFile>] [/ManifestFile:<DriveManifestFile>]
        [/PathMapFile:<DrivePathMapFile>]

Preview an Export Job:
    WAImportExport.exe PreviewExport
        [/logdir:<LogDirectory>]
        /sn:<StorageAccountName> /sk:<StorageAccountKey>
        /ExportBlobListFile:<ExportBlobListFile> /DriveSize:<DriveSize>

Parameters:

    /j:<JournalFile>
        - Required. Path toohello journal file. A journal file tracks a set of drives and
          records hello progress in preparing these drives. hello journal file must always
          be specified.
    /logdir:<LogDirectory>
        - Optional. hello log directory. Verbose log files as well as some temporary
          files will be written toothis directory. If not specified, current directory
          will be used as hello log directory. hello log directory can be specified only
          once for hello same journal file.
    /id:<SessionId>
        - Optional. hello session Id is used tooidentify a copy session. It is used to
          ensure accurate recovery of an interrupted copy session.
    /ResumeSession
        - Optional. If hello last copy session was terminated abnormally, this parameter
          can be specified tooresume hello session.
    /AbortSession
        - Optional. If hello last copy session was terminated abnormally, this parameter
          can be specified tooabort hello session.
    /sn:<StorageAccountName>
        - Required. Only applicable for RepairImport and RepairExport. hello name of
          hello storage account.
    /sk:<StorageAccountKey>
        - Required. hello key of hello storage account.
    /InitialDriveSet:<driveset.csv>
        - Required. A .csv file that contains a list of drives tooprepare.
    /AdditionalDriveSet:<driveset.csv>
        - Required. A .csv file that contains a list of additional drives toobe added.
    /r:<RepairFile>
        - Required. Only applicable for RepairImport and RepairExport.
          Path toohello file for tracking repair progress. Each drive must have one
          and only one repair file.
    /d:<TargetDirectories>
        - Required. Only applicable for RepairImport and RepairExport.
          For RepairImport, one or more semicolon-separated directories toorepair;
          For RepairExport, one directory toorepair, e.g. root directory of hello drive.
    /CopyLogFile:<DriveCopyLogFile>
        - Required. Only applicable for RepairImport and RepairExport. Path toothe
          drive copy log file (verbose or error).
    /ManifestFile:<DriveManifestFile>
        - Required. Only applicable for RepairExport. Path toohello drive manifest file.
    /PathMapFile:<DrivePathMapFile>
        - Optional. Only applicable for RepairImport. Path toohello file containing
          mappings of file paths relative toohello drive root toolocations of actual files
          (tab-delimited). When first specified, it will be populated with file paths
          with empty targets, which means either they are not found in TargetDirectories,
          access denied, with invalid name, or they exist in multiple directories. The
          path map file can be manually edited tooinclude hello correct target paths and
          specified again for hello tool tooresolve hello file paths correctly.
    /ExportBlobListFile:<ExportBlobListFile>
        - Required. Path toohello XML file containing list of blob paths or blob path
          prefixes for hello blobs toobe exported. hello file format is hello same as the
          blob list blob format in hello Put Job operation of hello Import/Export Service
          REST API.
    /DriveSize:<DriveSize>
        - Required. Size of drives toobe used for export. For example, 500GB, 1.5TB.
          Note: 1 GB = 1,000,000,000 bytes
                1 TB = 1,000,000,000,000 bytes
    /DataSet:<dataset.csv>
        - Required. A .csv file that contains a list of directories and/or a list files
          toobe copied tootarget drives.

    /silentmode
        - Optional. If not specified, it will remind you hello requirement of drives and
          need your confirmation toocontinue.

Examples:

    Copy a data set tooa drive:
    WAImportExport.exe PrepImport
        /j:9WM35C2V.jrn /id:session#1 /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GEL
        xmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /InitialDriveSet:driveset1.csv
        /DataSet:data.csv

    Copy another dataset toohello same drive following hello above command:
    WAImportExport.exe PrepImport /j:9WM35C2V.jrn /id:session#2 /DataSet:dataset2.csv

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
```

## <a name="next-steps"></a><span data-ttu-id="21c7d-145">後續步驟</span><span class="sxs-lookup"><span data-stu-id="21c7d-145">Next steps</span></span>

* [<span data-ttu-id="21c7d-146">針對匯入作業準備硬碟</span><span class="sxs-lookup"><span data-stu-id="21c7d-146">Preparing hard drives for an import job</span></span>](storage-import-export-tool-preparing-hard-drives-import.md)
* [<span data-ttu-id="21c7d-147">預覽匯出作業的磁碟機使用量</span><span class="sxs-lookup"><span data-stu-id="21c7d-147">Previewing drive usage for an export job</span></span>](storage-import-export-tool-previewing-drive-usage-export-v1.md)
* [<span data-ttu-id="21c7d-148">利用複製記錄檔檢閱作業狀態</span><span class="sxs-lookup"><span data-stu-id="21c7d-148">Reviewing job status with copy log files</span></span>](storage-import-export-tool-reviewing-job-status-v1.md)
* [<span data-ttu-id="21c7d-149">修復匯入作業</span><span class="sxs-lookup"><span data-stu-id="21c7d-149">Repairing an import job</span></span>](storage-import-export-tool-repairing-an-import-job-v1.md)
* [<span data-ttu-id="21c7d-150">修復匯出作業</span><span class="sxs-lookup"><span data-stu-id="21c7d-150">Repairing an export job</span></span>](storage-import-export-tool-repairing-an-export-job-v1.md)
* [<span data-ttu-id="21c7d-151">疑難排解 hello Azure 匯入/匯出工具</span><span class="sxs-lookup"><span data-stu-id="21c7d-151">Troubleshooting hello Azure Import/Export Tool</span></span>](storage-import-export-tool-troubleshooting-v1.md)
