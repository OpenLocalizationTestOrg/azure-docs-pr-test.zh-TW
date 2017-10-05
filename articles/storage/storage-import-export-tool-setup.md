---
title: "設定 Azure 匯入/匯出工具 | Microsoft Docs"
description: "了解如何設定 Azure 匯入/匯出服務的磁碟機準備及修復工具。"
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
ms.openlocfilehash: d39ec89b4877e2fca01b68b30bb287a120f2eb71
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="setting-up-the-azure-importexport-tool"></a><span data-ttu-id="64815-103">設定 Azure 匯入/匯出工具</span><span class="sxs-lookup"><span data-stu-id="64815-103">Setting up the Azure Import/Export Tool</span></span>

<span data-ttu-id="64815-104">Microsoft Azure 匯入/匯出工具是磁碟機準備及修復工具，可搭配 Microsoft Azure 匯入/匯出服務使用。</span><span class="sxs-lookup"><span data-stu-id="64815-104">The Microsoft Azure Import/Export Tool is the drive preparation and repair tool that you can use with the Microsoft Azure Import/Export service.</span></span> <span data-ttu-id="64815-105">您可以使用此工具來執行下列功能︰</span><span class="sxs-lookup"><span data-stu-id="64815-105">You can use the tool for the following functions:</span></span>

* <span data-ttu-id="64815-106">在建立匯入工作之前，您可以使用此工具，將資料複製到要寄送至 Azure 資料中心的硬碟。</span><span class="sxs-lookup"><span data-stu-id="64815-106">Before creating an import job, you can use this tool to copy data to the hard drives you are going to ship to an Azure data center.</span></span>
* <span data-ttu-id="64815-107">匯入工作完成後，您可以使用此工具來修復損毀、遺漏或與其他 Blob 衝突的任何 Blob。</span><span class="sxs-lookup"><span data-stu-id="64815-107">After an import job has completed, you can use this tool to repair any blobs that were corrupted, were missing, or conflicted with other blobs.</span></span>
* <span data-ttu-id="64815-108">當您收到已完成的匯出工作中的磁碟機後，您可以使用此工具來修復磁碟機上損毀或遺漏的任何檔案。</span><span class="sxs-lookup"><span data-stu-id="64815-108">After you receive the drives from a completed export job, you can use this tool to repair any files that were corrupted or missing on the drives.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="64815-109">必要條件</span><span class="sxs-lookup"><span data-stu-id="64815-109">Prerequisites</span></span>

<span data-ttu-id="64815-110">如果您正針對匯入作業**準備磁碟機**，就必須符合下列必要條件：</span><span class="sxs-lookup"><span data-stu-id="64815-110">If you are **preparing drives** for an import job, the following prerequisites must be met:</span></span>

* <span data-ttu-id="64815-111">您必須擁有有效的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="64815-111">You must have an active Azure subscription.</span></span>
* <span data-ttu-id="64815-112">您的訂用帳戶必須包含可用空間足夠儲存您要匯入之檔案的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="64815-112">Your subscription must include a storage account with enough available space to store the files you are going to import.</span></span>
* <span data-ttu-id="64815-113">您至少需要一個儲存體帳戶存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="64815-113">You need at least one of the storage account access keys.</span></span>
* <span data-ttu-id="64815-114">您需要安裝 Windows 7、Windows Server 2008 R2 或更新版本 Windows 作業系統的電腦 (「複製電腦」)。</span><span class="sxs-lookup"><span data-stu-id="64815-114">You need a computer (the "copy machine") with Windows 7, Windows Server 2008 R2, or a newer Windows operating system installed.</span></span>
* <span data-ttu-id="64815-115">複製電腦上必須安裝 .NET Framework 4。</span><span class="sxs-lookup"><span data-stu-id="64815-115">The .NET Framework 4 must be installed on the copy machine.</span></span>
* <span data-ttu-id="64815-116">複製電腦上必須啟用 BitLocker。</span><span class="sxs-lookup"><span data-stu-id="64815-116">BitLocker must be enabled on the copy machine.</span></span>
* <span data-ttu-id="64815-117">您需要一或多個連接至複製電腦的空白 3.5 英吋 SATA 硬碟。</span><span class="sxs-lookup"><span data-stu-id="64815-117">You need one or more empty 3.5-inch SATA hard drives connected to the copy machine.</span></span>
* <span data-ttu-id="64815-118">您想匯入的檔案必須可從複製機器上存取，無論它們是在網路共用或本機硬碟上。</span><span class="sxs-lookup"><span data-stu-id="64815-118">The files you plan to import must be accessible from the copy machine, whether they are on a network share or a local hard drive.</span></span>

<span data-ttu-id="64815-119">如果您正嘗試**修復已部分失敗的匯入**，您需要：</span><span class="sxs-lookup"><span data-stu-id="64815-119">If you are attempting to **repair an import** that has partially failed, you need:</span></span>

* <span data-ttu-id="64815-120">複製記錄檔</span><span class="sxs-lookup"><span data-stu-id="64815-120">The copy log files</span></span>
* <span data-ttu-id="64815-121">儲存體帳戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="64815-121">The storage account key</span></span>

<span data-ttu-id="64815-122">如果您正嘗試**修復已部分失敗的匯出**，您需要：</span><span class="sxs-lookup"><span data-stu-id="64815-122">If you are attempting to **repair an export**  that has partially failed, you need:</span></span>

* <span data-ttu-id="64815-123">複製記錄檔</span><span class="sxs-lookup"><span data-stu-id="64815-123">The copy log files</span></span>
* <span data-ttu-id="64815-124">資訊清單檔案 (選擇性)</span><span class="sxs-lookup"><span data-stu-id="64815-124">The manifest files (optional)</span></span>
* <span data-ttu-id="64815-125">儲存體帳戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="64815-125">The storage account key</span></span>

## <a name="installing-the-azure-importexport-tool"></a><span data-ttu-id="64815-126">安裝 Azure 匯入/匯出工具</span><span class="sxs-lookup"><span data-stu-id="64815-126">Installing the Azure Import/Export Tool</span></span>

<span data-ttu-id="64815-127">首先，[下載 Azure 匯入/匯出工具](https://www.microsoft.com/download/details.aspx?id=55280)並解壓縮至您電腦上的目錄，例如 `c:\WAImportExport`。</span><span class="sxs-lookup"><span data-stu-id="64815-127">First, [download the Azure Import/Export Tool](https://www.microsoft.com/download/details.aspx?id=55280) and extract it to a directory on your computer, for example `c:\WAImportExport`.</span></span>

<span data-ttu-id="64815-128">Azure 匯入/匯出工具包含下列檔案：</span><span class="sxs-lookup"><span data-stu-id="64815-128">The Azure Import/Export Tool consists of the following files:</span></span>

* <span data-ttu-id="64815-129">dataset.csv</span><span class="sxs-lookup"><span data-stu-id="64815-129">dataset.csv</span></span>
* <span data-ttu-id="64815-130">driveset.csv</span><span class="sxs-lookup"><span data-stu-id="64815-130">driveset.csv</span></span>
* <span data-ttu-id="64815-131">hddid.dll</span><span class="sxs-lookup"><span data-stu-id="64815-131">hddid.dll</span></span>
* <span data-ttu-id="64815-132">Microsoft.Data.Services.Client.dll</span><span class="sxs-lookup"><span data-stu-id="64815-132">Microsoft.Data.Services.Client.dll</span></span>
* <span data-ttu-id="64815-133">Microsoft.WindowsAzure.Storage.dll</span><span class="sxs-lookup"><span data-stu-id="64815-133">Microsoft.WindowsAzure.Storage.dll</span></span>
* <span data-ttu-id="64815-134">Microsoft.WindowsAzure.Storage.pdb</span><span class="sxs-lookup"><span data-stu-id="64815-134">Microsoft.WindowsAzure.Storage.pdb</span></span>
* <span data-ttu-id="64815-135">Microsoft.WindowsAzure.Storage.xml</span><span class="sxs-lookup"><span data-stu-id="64815-135">Microsoft.WindowsAzure.Storage.xml</span></span>
* <span data-ttu-id="64815-136">WAImportExport.exe</span><span class="sxs-lookup"><span data-stu-id="64815-136">WAImportExport.exe</span></span>
* <span data-ttu-id="64815-137">WAImportExport.exe.config</span><span class="sxs-lookup"><span data-stu-id="64815-137">WAImportExport.exe.config</span></span>
* <span data-ttu-id="64815-138">WAImportExport.pdb</span><span class="sxs-lookup"><span data-stu-id="64815-138">WAImportExport.pdb</span></span>
* <span data-ttu-id="64815-139">WAImportExportCore.dll</span><span class="sxs-lookup"><span data-stu-id="64815-139">WAImportExportCore.dll</span></span>
* <span data-ttu-id="64815-140">WAImportExportCore.pdb</span><span class="sxs-lookup"><span data-stu-id="64815-140">WAImportExportCore.pdb</span></span>
* <span data-ttu-id="64815-141">WAImportExportRepair.dll</span><span class="sxs-lookup"><span data-stu-id="64815-141">WAImportExportRepair.dll</span></span>
* <span data-ttu-id="64815-142">WAImportExportRepair.pdb</span><span class="sxs-lookup"><span data-stu-id="64815-142">WAImportExportRepair.pdb</span></span>

<span data-ttu-id="64815-143">接下來，在**系統管理員模式**中開啟 [命令提示字元] 視窗，並變更為包含解壓縮檔案的目錄。</span><span class="sxs-lookup"><span data-stu-id="64815-143">Next, open a Command Prompt window in **Administrator mode**, and change into the directory containing the extracted files.</span></span>

<span data-ttu-id="64815-144">若要輸出命令的說明，請執行此工具(`WAImportExport.exe`) 而不包含參數：</span><span class="sxs-lookup"><span data-stu-id="64815-144">To output help for the command, run the tool (`WAImportExport.exe`) without parameters:</span></span>

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
        - Required. Path to the journal file. A journal file tracks a set of drives and
          records the progress in preparing these drives. The journal file must always
          be specified.
    /logdir:<LogDirectory>
        - Optional. The log directory. Verbose log files as well as some temporary
          files will be written to this directory. If not specified, current directory
          will be used as the log directory. The log directory can be specified only
          once for the same journal file.
    /id:<SessionId>
        - Optional. The session Id is used to identify a copy session. It is used to
          ensure accurate recovery of an interrupted copy session.
    /ResumeSession
        - Optional. If the last copy session was terminated abnormally, this parameter
          can be specified to resume the session.
    /AbortSession
        - Optional. If the last copy session was terminated abnormally, this parameter
          can be specified to abort the session.
    /sn:<StorageAccountName>
        - Required. Only applicable for RepairImport and RepairExport. The name of
          the storage account.
    /sk:<StorageAccountKey>
        - Required. The key of the storage account.
    /InitialDriveSet:<driveset.csv>
        - Required. A .csv file that contains a list of drives to prepare.
    /AdditionalDriveSet:<driveset.csv>
        - Required. A .csv file that contains a list of additional drives to be added.
    /r:<RepairFile>
        - Required. Only applicable for RepairImport and RepairExport.
          Path to the file for tracking repair progress. Each drive must have one
          and only one repair file.
    /d:<TargetDirectories>
        - Required. Only applicable for RepairImport and RepairExport.
          For RepairImport, one or more semicolon-separated directories to repair;
          For RepairExport, one directory to repair, e.g. root directory of the drive.
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
          blob list blob format in the Put Job operation of the Import/Export Service
          REST API.
    /DriveSize:<DriveSize>
        - Required. Size of drives to be used for export. For example, 500GB, 1.5TB.
          Note: 1 GB = 1,000,000,000 bytes
                1 TB = 1,000,000,000,000 bytes
    /DataSet:<dataset.csv>
        - Required. A .csv file that contains a list of directories and/or a list files
          to be copied to target drives.

    /silentmode
        - Optional. If not specified, it will remind you the requirement of drives and
          need your confirmation to continue.

Examples:

    Copy a data set to a drive:
    WAImportExport.exe PrepImport
        /j:9WM35C2V.jrn /id:session#1 /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GEL
        xmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /InitialDriveSet:driveset1.csv
        /DataSet:data.csv

    Copy another dataset to the same drive following the above command:
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

## <a name="next-steps"></a><span data-ttu-id="64815-145">後續步驟</span><span class="sxs-lookup"><span data-stu-id="64815-145">Next steps</span></span>

* [<span data-ttu-id="64815-146">針對匯入作業準備硬碟</span><span class="sxs-lookup"><span data-stu-id="64815-146">Preparing hard drives for an import job</span></span>](storage-import-export-tool-preparing-hard-drives-import.md)
* [<span data-ttu-id="64815-147">預覽匯出作業的磁碟機使用量</span><span class="sxs-lookup"><span data-stu-id="64815-147">Previewing drive usage for an export job</span></span>](storage-import-export-tool-previewing-drive-usage-export-v1.md)
* [<span data-ttu-id="64815-148">利用複製記錄檔檢閱作業狀態</span><span class="sxs-lookup"><span data-stu-id="64815-148">Reviewing job status with copy log files</span></span>](storage-import-export-tool-reviewing-job-status-v1.md)
* [<span data-ttu-id="64815-149">修復匯入作業</span><span class="sxs-lookup"><span data-stu-id="64815-149">Repairing an import job</span></span>](storage-import-export-tool-repairing-an-import-job-v1.md)
* [<span data-ttu-id="64815-150">修復匯出作業</span><span class="sxs-lookup"><span data-stu-id="64815-150">Repairing an export job</span></span>](storage-import-export-tool-repairing-an-export-job-v1.md)
* [<span data-ttu-id="64815-151">針對 Azure 匯入/匯出工具進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="64815-151">Troubleshooting the Azure Import/Export Tool</span></span>](storage-import-export-tool-troubleshooting-v1.md)
