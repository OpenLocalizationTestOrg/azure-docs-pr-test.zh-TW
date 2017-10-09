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
ms.openlocfilehash: 3d8897f2783112e07123669f1ba5b22576770e60
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="setting-up-hello-azure-importexport-tool"></a>設定 hello Azure 匯入/匯出工具

hello Microsoft Azure 匯入/匯出工具是 hello 磁碟機準備及修復工具可讓您以 hello Microsoft Azure 匯入/匯出服務。 您可以使用下列函式的 hello hello 工具：

* 在建立匯入工作之前，您可以使用此工具 toocopy 資料 toohello 硬碟要 tooship tooan Azure 資料中心。
* 匯入工作完成後，您可以使用此工具 toorepair 損毀、 遺漏或衝突的任何 blob 與其他 blob。
* 您已完成的匯出工作收到 hello 磁碟機之後，您可以使用此工具 toorepair 任何檔案已損毀或遺失 hello 磁碟機上。

## <a name="prerequisites"></a>必要條件

如果您是**來準備磁碟機**匯入工作，必須符合下列必要條件 hello:

* 您必須擁有有效的 Azure 訂用帳戶。
* 您的訂閱必須包含儲存體帳戶具有足夠的可用空間 toostore hello 檔案要 tooimport。
* 您必須至少一個 hello 儲存體帳戶存取金鑰。
* 您需要 Windows 7、 Windows Server 2008 R2 或更新版本安裝 Windows 作業系統的電腦 (hello 「 複製電腦 」)。
* hello 複製電腦上必須安裝.NET Framework 4 hello。
* 必須在 hello 複製電腦上啟用 BitLocker。
* 您需要一個或多個空 3.5 吋 SATA 硬碟連接 toohello 複製電腦。
* 您計劃 tooimport hello 檔案必須能夠從 hello 複製電腦，存取，不論它們在網路共用或本機硬碟上。

若您嘗試過**修復匯入**已有部分失敗，您需要：

* hello 複製記錄檔
* hello 儲存體帳戶金鑰

若您嘗試過**修復匯出**已有部分失敗，您需要：

* hello 複製記錄檔
* hello 資訊清單檔案 （選擇性）
* hello 儲存體帳戶金鑰

## <a name="installing-hello-azure-importexport-tool"></a>安裝 hello Azure 匯入/匯出工具

首先，[下載 hello Azure 匯入/匯出工具](https://www.microsoft.com/download/details.aspx?id=55280)並將它解壓縮 tooa 目錄，您在電腦上，例如`c:\WAImportExport`。

hello Azure 匯入/匯出工具包含下列檔案的 hello:

* dataset.csv
* driveset.csv
* hddid.dll
* Microsoft.Data.Services.Client.dll
* Microsoft.WindowsAzure.Storage.dll
* Microsoft.WindowsAzure.Storage.pdb
* Microsoft.WindowsAzure.Storage.xml
* WAImportExport.exe
* WAImportExport.exe.config
* WAImportExport.pdb
* WAImportExportCore.dll
* WAImportExportCore.pdb
* WAImportExportRepair.dll
* WAImportExportRepair.pdb

接下來，開啟 命令提示字元視窗中的**系統管理員模式**，並變更到包含 hello hello 目錄解壓縮檔案。

toooutput hello 命令，執行 hello 工具說明 (`WAImportExport.exe`) 不含參數：

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

## <a name="next-steps"></a>後續步驟

* [針對匯入作業準備硬碟](../storage-import-export-tool-preparing-hard-drives-import.md)
* [預覽匯出作業的磁碟機使用量](../storage-import-export-tool-previewing-drive-usage-export-v1.md)
* [利用複製記錄檔檢閱作業狀態](../storage-import-export-tool-reviewing-job-status-v1.md)
* [修復匯入作業](../storage-import-export-tool-repairing-an-import-job-v1.md)
* [修復匯出作業](../storage-import-export-tool-repairing-an-export-job-v1.md)
* [疑難排解 hello Azure 匯入/匯出工具](storage-import-export-tool-troubleshooting-v1.md)
