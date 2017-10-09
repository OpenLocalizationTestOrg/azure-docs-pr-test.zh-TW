---
title: "aaaPreparing 硬碟的 Azure 匯入/匯出匯入作業 |Microsoft 文件"
description: "了解如何使用 tooprepare 硬碟 hello WAImportExport 工具 toocreate hello Azure 匯入/匯出服務的匯入工作。"
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
ms.openlocfilehash: 3f247a9efee29da2d18140353edc9dd7103a0761
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="preparing-hard-drives-for-an-import-job"></a>準備匯入工作的硬碟

hello WAImportExport 工具是 hello 磁碟機準備及修復工具可讓您以 hello [Microsoft Azure 匯入/匯出服務](storage-import-export-service.md)。 您可以使用此工具 toocopy 資料 toohello 硬碟要 tooship tooan Azure 資料中心。 匯入工作完成後，您可以使用此工具 toorepair 損毀、 遺漏或衝突的任何 blob 與其他 blob。 您已完成的匯出工作收到 hello 磁碟機之後，您可以使用此工具 toorepair 任何檔案已損毀或遺失 hello 磁碟機上。 在本文中，我們會通過 hello 使用此工具。

## <a name="prerequisites"></a>必要條件

### <a name="requirements-for-waimportexportexe"></a>WAImportExport.exe 的需求

- **電腦組態**
  - Windows 7、Windows Server 2008 R2 或更新版本的 Windows 作業系統
  - 必須安裝 .NET framework 4。 請參閱[常見問題集](#faq)如何 toocheck.Net Framework 是否安裝在 hello 電腦上。
- **儲存體帳戶金鑰**-您至少需要一個 hello 帳戶金鑰的 hello 儲存體帳戶。

### <a name="preparing-disk-for-import-job"></a>準備匯入工作的磁碟

- **BitLocker-** hello 機器執行 hello WAImportExport 工具上必須啟用 BitLocker。 請參閱 hello[常見問題集](#faq)如何 tooenable BitLocker。
- **磁碟**必須可從執行 WAImportExport 工具的電腦上存取。 如需磁碟規格的詳細資訊，請參閱[常見問題集](#faq)。
- **原始程式檔**-您計劃 tooimport hello 檔案必須能夠從 hello 複製電腦，不論它們是否在網路共用或本機硬碟上。

### <a name="repairing-a-partially-failed-import-job"></a>修復部分失敗的匯入工作

- **複製記錄檔**，是 Azure 匯入/匯出服務在儲存體帳戶和磁碟之間複製資料時產生的。 此檔案位於您的目標儲存體帳戶。

### <a name="repairing-a-partially-failed-export-job"></a>修復部分失敗的匯出工作

- **複製記錄檔**，是 Azure 匯入/匯出服務在儲存體帳戶和磁碟之間複製資料時產生的。 此檔案位於您的來源儲存體帳戶。
- **資訊清單檔案** - [選擇性] 位於 Microsoft 寄回的匯出磁碟機上。

## <a name="download-and-install-waimportexport"></a>下載和安裝 WAImportExport

下載 hello[最新版本的 WAImportExport.exe](https://www.microsoft.com/download/details.aspx?id=55280)。 擷取您電腦上的 hello 壓縮內容 tooa 目錄。

您的下一個工作是 toocreate CSV 檔案。

## <a name="prepare-hello-dataset-csv-file"></a>準備 hello 資料集中的 CSV 檔案

### <a name="what-is-dataset-csv"></a>什麼是資料集 CSV

資料集的 CSV 檔案是 hello /dataset 旗標的值是包含的目錄清單和/或一份檔案複製 toobe tootarget 磁碟機的 CSV 檔案。 hello 第一個步驟 toocreating 匯入工作是 toodetermine 哪個目錄和檔案，您將要 tooimport。 可以是目錄清單、唯一檔案的清單或兩者的組合。 包含目錄時，hello 目錄及其子目錄中的所有檔案都會 hello 匯入工作的一部分。

匯入每個目錄或檔案 toobe，您必須識別目的地虛擬目錄或 blob hello Azure Blob 服務中。 您會在輸入 toohello WAImportExport 工具來使用這些目標。 目錄應該分隔 hello 正斜線字元"/"。

hello 下表顯示一些 blob 目標的範例：

| 來源檔案或目錄 | 目的地 Blob 或虛擬目錄 |
| --- | --- |
| H:\Video | https://mystorageaccount.blob.core.windows.net/video |
| H:\Photo | https://mystorageaccount.blob.core.windows.net/photo |
| K:\Temp\FavoriteVideo.ISO | https://mystorageaccount.blob.core.windows.net/favorite/FavoriteVideo.ISO |
| \\myshare\john\music | https://mystorageaccount.blob.core.windows.net/music |

### <a name="sample-datasetcsv"></a>範例 dataset.csv

```
BasePath,DstBlobPathOrPrefix,BlobType,Disposition,MetadataFile,PropertiesFile
"F:\50M_original\100M_1.csv.txt","containername/100M_1.csv.txt",BlockBlob,rename,"None",None
"F:\50M_original\","containername/",BlockBlob,rename,"None",None
```

### <a name="dataset-csv-file-fields"></a>資料集 CSV 檔案欄位

| 欄位 | 說明 |
| --- | --- |
| 基本路徑 | **[必要]**<br/>此參數的 hello 值代表 hello hello 資料 toobe 匯入所在的來源。 hello 工具將會以遞迴方式複製位於這個路徑下的所有資料。<br><br/>**允許的值**： 這具有 toobe，本機電腦上的有效路徑或有效的共用路徑，而且必須能夠存取由 hello 使用者。 hello 目錄路徑必須是絕對路徑 （而不是相對路徑）。 如果 hello 路徑的結尾 」\\"，它代表其他目錄路徑，而不結束"\\"代表檔案。<br/>此欄位中不允許 Regex。 如果 hello 路徑包含空格，請將它放在 「 」。<br><br/>**範例**："c:\Directory\c\Directory\File.txt"<br>"\\\\FBaseFilesharePath.domain.net\sharename\directory\"  |
| DstBlobPathOrPrefix | **[必要]**<br/> hello 路徑 toohello 目的地虛擬目錄 Windows Azure 儲存體帳戶中。 hello 虛擬目錄可能或可能不存在。 如果不存在，匯入/匯出服務將會建立一個。<br/><br/>指定目的地虛擬目錄或 blob 時是確定 toouse 有效的容器名稱。 請記住容器名稱必須是小寫。 關於容器命名規則，請參閱[命名和參考容器、Blob 及中繼資料](/rest/api/storageservices/naming-and-referencing-containers--blobs--and-metadata)。 如果只指定根，hello 來源 hello 目錄結構將會複寫 hello 目的地 blob 容器中。 如果想要不同的目錄結構比 hello 在來源中，csv 檔案中對應的多個資料列的其中一個<br/><br/>您可以指定容器或 blob 首碼，如 music/70s/。 hello 目的地目錄必須以 hello 容器名稱開頭，後面接著正斜線"/"，而且可能會選擇包含結尾的虛擬 blob 目錄"/"。<br/><br/>Hello 目的地容器為 hello 根容器時，您必須明確指定 hello 根容器，包括 hello 正斜線，$root 為 /。 因為 hello 根容器下的 blob 不能包含 「 / 」 在其名稱中，hello 目的目錄為 hello 根容器時，將不會複製 hello 來源目錄中的任何子目錄。<br/><br/>**範例**<br/>如果 https://mystorageaccount.blob.core.windows.net/video hello 目的地 blob 路徑，這個欄位的 hello 值可以是視訊 /  |
| BlobType | **[選用]** block &#124; page<br/>目前匯入/匯出服務支援兩種 Blob。 分頁 blob 和區塊 Blob，所有檔案預設會匯入為區塊 Blob。 和\*.vhd 和\*頁面 BlobsThere 現狀 hello 區塊 blob 和分頁 blob 的允許大小的限制，將匯入.vhdx。 如需詳細資訊，請參閱[儲存體延展性目標](storage-scalability-targets.md#scalability-targets-for-blobs-queues-tables-and-files) (英文)。  |
| Disposition | **[選用]** rename &#124; no-overwrite &#124; overwrite <br/> 此欄位會指定在匯入也就是 hello 複製行為 當資料正在上傳 toohello 從 hello 磁碟的儲存體帳戶。 可用的選項有： 重新命名 &#124; 是否覆寫 &#124; 否-覆寫。預設值太"rename"如果指定的執行任何動作。 <br/><br/>**Rename**︰如果已經有同名的物件，則在目的地建立複本。<br/>覆寫： 覆寫 hello 檔案較新的檔案。 上次修改 wins hello 檔案。<br/>**否-覆寫**： 撰寫 hello 略過檔案已經存在。|
| MetadataFile | **[選用]** <br/>hello 值 toothis 欄位是 hello 中繼資料檔案即會提供一個 hello 需要 toopreserve hello hello 物件中繼資料，或是提供自訂中繼資料。 路徑 toohello hello 目的地 blob 的中繼資料檔案。 如需詳細資訊，請參閱[匯入/匯出服務中繼資料和屬性檔案格式](storage-import-export-file-format-metadata-and-properties.md)。 |
| PropertiesFile | **[選用]** <br/>路徑 toohello hello 目的地 blob 的內容檔案。 如需詳細資訊，請參閱[匯入/匯出服務中繼資料和屬性檔案格式](storage-import-export-file-format-metadata-and-properties.md)。 |

## <a name="prepare-initialdriveset-or-additionaldriveset-csv-file"></a>準備 InitialDriveSet 或 AdditionalDriveSet CSV 檔案

### <a name="what-is-driveset-csv"></a>什麼是磁碟機集 CSV

hello hello /InitialDriveSet 或 /AdditionalDriveSet 旗標的值是包含 hello hello 工具可以正確地挑選準備磁碟 toobe hello 清單對應 toowhich hello 磁碟機代號的磁碟清單的 CSV 檔案。 Hello 資料大小大於單一磁碟大小，如果 hello WAImportExport 工具會將 hello 資料散發在多個磁碟，以最佳化方式編列此 CSV 檔案中。

沒有可寫入磁碟 hello 資料的 hello 數目沒有限制 tooin 單一工作階段。 hello 工具將會散發資料是根據磁碟大小及資料夾的大小。 它會選取 hello 磁碟最適合 hello 物件大小。 hello 資料上傳時 toohello 儲存體帳戶將會是資料集檔案中所指定的聚合式回復 toohello 目錄結構。 在順序 toocreate driveset CSV，遵循下列的 hello 步驟。

### <a name="create-basic-volume-and-assign-drive-letter"></a>建立基本磁碟區並指派磁碟機代號

在排序 toocreate 基本磁碟區並指派磁碟機代號，請依照 「 簡單資料分割建立 」 在指定的 hello 指示[磁碟管理概觀](https://technet.microsoft.com/library/cc754936.aspx)。

### <a name="sample-initialdriveset-and-additionaldriveset-csv-file"></a>範例 InitialDriveSet 與 AdditionalDriveSet CSV 檔案

```
DriveLetter,FormatOption,SilentOrPromptOnFormat,Encryption,ExistingBitLockerKey
G,AlreadyFormatted,SilentMode,AlreadyEncrypted,060456-014509-132033-080300-252615-584177-672089-411631
H,Format,SilentMode,Encrypt,
```

### <a name="driveset-csv-file-fields"></a>磁碟機集 CSV 檔案欄位

| 欄位 | 值 |
| --- | --- |
| DriveLetter | **[必要]**<br/> 做為 hello 目的地 toohello 工具所提供之每個磁碟機必須有一個簡單的 NTFS 磁碟區和磁碟機代號指派 tooit。<br/> <br/>**範例**R 或 r |
| FormatOption | **[必要]** Format &#124; AlreadyFormatted<br/><br/> **格式**： 指定這個將會格式化 hello 磁碟上的所有 hello 資料。 <br/>**AlreadyFormatted**: hello 工具將略過格式指定此值時。 |
| SilentOrPromptOnFormat | **[必要]** SilentMode &#124; PromptOnFormat<br/><br/>**SilentMode**： 提供這個值可讓使用者 toorun hello 工具，以無訊息模式。 <br/>**PromptOnFormat**: hello 工具將會提示 hello 使用者 tooconfirm hello 動作真的要在每一種格式。<br/><br/>如果未設定，命令將會中止並顯示錯誤訊息："Incorrect value for SilentOrPromptOnFormat: none" \(SilentOrPromptOnFormat 的值不正確：無\) |
| 加密 | **[必要]** Encrypt &#124; AlreadyEncrypted<br/> hello 這個欄位的值會決定哪些磁碟 tooencrypt 和無法供所示。 <br/><br/>**加密**： 工具將會格式化 hello 磁碟機。 如果 「 FormatOption 」 欄位的值是"Format"這個值會是需要的 toobe"Encrypt"。 如果在此情況下指定 "AlreadyEncrypted"，則會造成下列錯誤：「指定 Format 時，也必須指定 Encrypt」。<br/>**AlreadyEncrypted**： 工具將會解密使用 hello BitLockerKey"ExistingBitLockerKey 」 欄位中提供的 hello 磁碟機。 如果 "FormatOption" 欄位的值是 "AlreadyFormatted"，這個值可以是 "Encrypt" 或 "AlreadyEncrypted" |
| ExistingBitLockerKey | **[必要]** 如果 "Encryption" 欄位的值是 "AlreadyEncrypted"<br/> hello 這個欄位的值為 hello 與 hello 特定磁碟相關聯的 BitLocker 金鑰。 <br/><br/>此欄位保留空白如果 hello 「 加密 」 欄位值為"Encrypt"。  如果在此情況下指定 BitLocker 金鑰，則會造成下列錯誤：「不應指定 Bitlocker 金鑰」。<br/>  **範例**：060456-014509-132033-080300-252615-584177-672089-411631|

##  <a name="preparing-disk-for-import-job"></a>準備匯入工作的磁碟

tooprepare 磁碟機匯入工作，呼叫以 hello hello WAImportExport 工具**PrepImport**命令。 這是 hello 第一個複製工作階段或後續複製工作階段取決於您加入的參數。

### <a name="first-session"></a>第一個工作階段

第一個複製工作階段 tooCopy Single/Multiple 目錄 tooa 一或多個磁碟 （取決於 CSV 檔案中所指定） WAImportExport 工具 hello PrepImport 命令先複製工作階段 toocopy 目錄及/或新的複製工作階段的檔案：

```
WAImportExport.exe PrepImport /j:<JournalFile> /id:<SessionId> [/logdir:<LogDirectory>] [/sk:<StorageAccountKey>] [/silentmode] [/InitialDriveSet:<driveset.csv>] DataSet:<dataset.csv>
```

**範例：**

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#1  /sk:\*\*\*\*\*\*\*\*\*\*\*\*\* /InitialDriveSet:driveset-1.csv /DataSet:dataset-1.csv /logdir:F:\logs
```

### <a name="add-data-in-subsequent-session"></a>在後續工作階段中加入資料

在後續複製工作階段，您不需要 toospecify hello 初始參數。 您需要 toouse hello 相同日誌檔 hello 工具 tooremember 處 hello 中前一個工作階段。 hello hello 複製工作階段狀態是寫入 toohello 日誌檔。 以下是 hello 語法的後續複製工作階段 toocopy 其他目錄，或檔案：

```
WAImportExport.exe PrepImport /j:<SameJournalFile> /id:<DifferentSessionId>  [DataSet:<differentdataset.csv>]
```

**範例：**

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#2  /DataSet:dataset-2.csv
```

### <a name="add-drives-toolatest-session"></a>新增磁碟機 toolatest 工作階段

如果指定的磁碟機中 InitialDriveset 無法符合 hello 資料，都可以使用 hello 工具 tooadd 其他磁碟機 toosame 複製工作階段。 

>[!NOTE] 
>hello 工作階段識別碼都應該符合 hello 前一個工作階段識別碼。日誌檔應符合在前一個工作階段中指定的其中一個 hello。
>
```
WAImportExport.exe PrepImport /j:<SameJournalFile> /id:<SameSessionId> /AdditionalDriveSet:<newdriveset.csv>
```

**範例：**

```
WAImportExport.exe PrepImport /j:SameJournalTest.jrn /id:session#2  /AdditionalDriveSet:driveset-2.csv
```

### <a name="abort-hello-latest-session"></a>中止 hello 最新的工作階段：

如果複製工作階段中斷，而且它不可能 tooresume （例如，如果來源目錄已證實無法存取），您就必須中止 hello 目前工作階段，以便可以復原該交易可以啟動後，新的複製工作階段：

```
WAImportExport.exe PrepImport /j:<SameJournalFile> /id:<SameSessionId> /AbortSession
```

**範例：**

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#2  /AbortSession
```

只有 hello 最後一個複製工作階段，不正常終止會中止。 請注意，您無法停止 hello 磁碟機的第一個複製工作階段。 相反地，您必須使用新的日誌檔重新 hello 複製工作階段。

### <a name="resume-a-latest-interrupted-session"></a>繼續最近中斷的工作階段

如果複製工作階段因故中斷，您可以執行 hello 工具並使用只 hello 指定日誌檔來繼續：

```
WAImportExport.exe PrepImport /j:<SameJournalFile> /id:<SameSessionId> /ResumeSession
```

**範例：**

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#2 /ResumeSession
```

> [!IMPORTANT] 
> 當您繼續複製工作階段時，請勿修改 hello 來源資料檔案和目錄加入或移除檔案。

## <a name="waimportexport-parameters"></a>WAImportExport 參數

| 參數 | 說明 |
| --- | --- |
|     /j:&lt;JournalFile&gt;  | **必要**<br/> 路徑 toohello 日誌檔。 日誌檔追蹤一組磁碟機，並記錄 hello 準備這些磁碟機的進度。 一律必須指定 hello 日誌檔。  |
|     /logdir:&lt;LogDirectory&gt;  | **選用**。 hello 記錄檔目錄。<br/> 詳細資訊記錄檔，以及某些暫存檔案會寫入 toothis 目錄。 如果未指定，目前的目錄將會使用為 hello 記錄檔目錄。 hello 記錄檔目錄可以一次針對指定 hello 相同的日誌檔。  |
|     /id:&lt;SessionId&gt;  | **必要**<br/> 識別碼是一個複製工作階段使用的 tooidentify hello 工作階段。 它是使用的 tooensure 中斷的複製工作階段的精確的復原。  |
|     /ResumeSession  | 選用。 Hello 最後一個複製工作階段已不正常終止，則這個參數可以是指定的 tooresume hello 工作階段。   |
|     /AbortSession  | 選用。 Hello 最後一個複製工作階段已不正常終止，則這個參數可以是指定的 tooabort hello 工作階段。  |
|     /sn:&lt;StorageAccountName&gt;  | **必要**<br/> 僅適用於 RepairImport 和 RepairExport。 hello hello 儲存體帳戶名稱。  |
|     /sk:&lt;StorageAccountKey&gt;  | **必要**<br/> hello hello 儲存體帳戶金鑰。 |
|     /InitialDriveSet:&lt;driveset.csv&gt;  | **需要**時執行第一個複製工作階段 hello<br/> CSV 檔案包含磁碟機 tooprepare 的清單。  |
|     /AdditionalDriveSet:&lt;driveset.csv&gt; | **必要**。 當新增磁碟機 toocurrent 複製工作階段。 <br/> CSV 檔案包含的其他磁碟機 toobe 加入清單。  |
|      /r:&lt;RepairFile&gt; | **必要** 僅適用於 RepairImport 和 RepairExport。<br/> 追蹤修復進度時的路徑 toohello 檔案。 每個磁碟機需要一個修復檔案，而且只能有一個。  |
|     /d:&lt;TargetDirectories&gt; | **必要**。 僅適用於 RepairImport 和 RepairExport。 RepairImport，針對一個或多個以分號分隔目錄 toorepair;如 RepairExport，一個目錄 toorepair 例如根 hello 磁碟機的目錄。  |
|     /CopyLogFile:&lt;DriveCopyLogFile&gt; | **必要** 僅適用於 RepairImport 和 RepairExport。 路徑 toohello 磁碟機複製記錄檔 (詳細資訊或錯誤)。  |
|     /ManifestFile:&lt;DriveManifestFile&gt; | **必要** 僅適用於 RepairExport。<br/> Toohello 磁碟機資訊清單檔案路徑。  |
|     /PathMapFile:&lt;DrivePathMapFile&gt; | **選用**。 僅適用於 RepairImport。<br/> 包含對應的檔案路徑相對 toohello 磁碟機根目錄 toolocations （tab 分隔） 的實際檔案的路徑 toohello 檔案。 第一次指定時，它會填入空白目標的檔案路徑，表示在 TargetDirectories 中找不到它們、存取被拒、具有無效名稱，或它們存在多個目錄中。 hello 路徑對應檔案可以是手動編輯的 tooinclude hello 正確的目標路徑，並再次指定 hello 工具 tooresolve hello 檔案路徑正確。  |
|     /ExportBlobListFile:&lt;ExportBlobListFile&gt; | **必要**。 僅適用於 PreviewExport。<br/> 路徑 toohello XML 檔案包含清單的 blob 路徑或 blob 路徑前置詞 hello blob toobe 匯出。 hello 檔案格式是 hello 為 hello hello 匯入/匯出服務 REST API 的 Put Job 作業在 hello blob 清單 blob 格式相同。  |
|     /DriveSize:&lt;DriveSize&gt; | **必要**。 僅適用於 PreviewExport。<br/>  磁碟機 toobe 用於匯出的大小。 例如，500 GB、1.5 TB。 注意：1 GB = 1,000,000,000 個位元組 1 TB = 1,000,000,000,000 個位元組  |
|     /DataSet:&lt;dataset.csv&gt; | **必要**<br/> CSV 檔案包含的目錄清單及/或一份檔案 toobe 複製 tootarget 磁碟機。  |
|     /silentmode  | **選用**。<br/> 如果未指定，它會提醒您 hello 的磁碟機的需求，而且需要確認 toocontinue。  |

## <a name="tool-output"></a>工具輸出

### <a name="sample-drive-manifest-file"></a>範例磁碟機資訊清單檔案

```xml
<?xml version="1.0" encoding="UTF-8"?>
<DriveManifest Version="2011-MM-DD">
   <Drive>
      <DriveId>drive-id</DriveId>
      <StorageAccountKey>storage-account-key</StorageAccountKey>
      <ClientCreator>client-creator</ClientCreator>
      <!-- First Blob List -->
      <BlobList Id="session#1-0">
         <!-- Global properties and metadata that applies tooall blobs -->
         <MetadataPath Hash="md5-hash">global-metadata-file-path</MetadataPath>
         <PropertiesPath Hash="md5-hash">global-properties-file-path</PropertiesPath>
         <!-- First Blob -->
         <Blob>
            <BlobPath>blob-path-relative-to-account</BlobPath>
            <FilePath>file-path-relative-to-transfer-disk</FilePath>
            <ClientData>client-data</ClientData>
            <Length>content-length</Length>
            <ImportDisposition>import-disposition</ImportDisposition>
            <!-- page-range-list-or-block-list -->
            <!-- page-range-list -->
            <PageRangeList>
               <PageRange Offset="1073741824" Length="512" Hash="md5-hash" />
               <PageRange Offset="1073741824" Length="512" Hash="md5-hash" />
            </PageRangeList>
            <!-- block-list -->
            <BlockList>
               <Block Offset="1073741824" Length="4194304" Id="block-id" Hash="md5-hash" />
               <Block Offset="1073741824" Length="4194304" Id="block-id" Hash="md5-hash" />
            </BlockList>
            <MetadataPath Hash="md5-hash">metadata-file-path</MetadataPath>
            <PropertiesPath Hash="md5-hash">properties-file-path</PropertiesPath>
         </Blob>
      </BlobList>
   </Drive>
</DriveManifest>
```

### <a name="sample-journal-file-xml-for-each-drive"></a>每個磁碟機的範例日誌檔案 (XML)

```xml
[BeginUpdateRecord][2016/11/01 21:22:25.379][Type:ActivityRecord]
ActivityId: DriveInfo
DriveState: [BeginValue]
<?xml version="1.0" encoding="UTF-8"?>
<Drive>
   <DriveId>drive-id</DriveId>
   <BitLockerKey>*******</BitLockerKey>
   <ManifestFile>\DriveManifest.xml</ManifestFile>
   <ManifestHash>D863FE44F861AE0DA4DCEAEEFFCCCE68</ManifestHash> </Drive>
[EndValue]
SaveCommandOutput: Completed
[EndUpdateRecord]
```

### <a name="sample-journal-file-jrn-for-session-that-records-hello-trail-of-sessions"></a>日誌檔範例 (JRN) 記錄 hello 軌跡的工作階段的工作階段

```
[BeginUpdateRecord][2016/11/02 18:24:14.735][Type:NewJournalFile]
VocabularyVersion: 2013-02-01
[EndUpdateRecord]
[BeginUpdateRecord][2016/11/02 18:24:14.749][Type:ActivityRecord]
ActivityId: PrepImportDriveCommandContext
LogDirectory: F:\logs
[EndUpdateRecord]
[BeginUpdateRecord][2016/11/02 18:24:14.754][Type:ActivityRecord]
ActivityId: PrepImportDriveCommandContext
StorageAccountKey: *******
[EndUpdateRecord]
```

## <a name="faq"></a>常見問題集

### <a name="general"></a>一般

#### <a name="what-is-waimportexport-tool"></a>什麼是 WAImportExport 工具？

hello WAImportExport 工具是 hello 磁碟機準備及修復工具可讓您以 hello Microsoft Azure 匯入/匯出服務。 您可以使用此工具 toocopy 資料 toohello 硬碟要 tooship tooan Azure 資料中心。 匯入工作完成後，您可以使用此工具 toorepair 損毀、 遺漏或衝突的任何 blob 與其他 blob。 您已完成的匯出工作收到 hello 磁碟機之後，您可以使用此工具 toorepair 任何檔案已損毀或遺失 hello 磁碟機上。

#### <a name="how-does-hello-waimportexport-tool-work-on-multiple-source-dir-and-disks"></a>沒有 hello WAImportExport 工具如何在多個來源目錄和磁碟嗎？

如果 hello 資料大小大於 hello 磁碟大小，hello WAImportExport 工具會將 hello 資料分散到 hello 磁碟以最佳化方式。 以平行方式或以循序方式可以完成 hello 資料複製 toomultiple 磁碟。 沒有可寫入磁碟 hello 資料的 hello 數目沒有限制 toosimultaneously。 hello 工具將會散發資料是根據磁碟大小及資料夾的大小。 它會選取 hello 磁碟最適合 hello 物件大小。 hello 資料上傳時 toohello 儲存體帳戶將會回交集 toohello 指定目錄結構。

#### <a name="where-can-i-find-previous-version-of-waimportexport-tool"></a>哪裡可以找到舊版的 WAImportExport 工具？

WAImportExport 工具擁有 WAImportExport V1 工具的所有功能。 WAImportExport 工具可讓使用者 toospecify，多個來源和寫入 toomultiple 磁碟機。 此外，其中一個可以輕鬆地管理多個從中 hello 資料需要 toobe 在單一 CSV 檔案中複製的來源位置。 不過，萬一您需要 SAS 支援或想 toocopy 單一來源 toosingle 磁碟，您可以 [下載 WAImportExport V1 工具] (http://go.microsoft.com/fwlink/?LinkID = 301900&amp;: //go.microsoft.com/fwlink/？ linkid = 0x409)，並參考太[WAImportExport V1 參考](storage-import-export-tool-how-to-v1.md)WAImportExport V1 使用量的相關說明。

#### <a name="what-is-a-session-id"></a>什麼是工作階段識別碼？

hello 工具預期 hello 複製工作階段 (/ 識別碼) 參數 toobe hello 相同，如果 hello 意圖 toospread hello 資料跨多個磁碟。 維護 hello 相同的 hello 複製工作階段的名稱可讓使用者 toocopy 資料從分割成一或多個目的地磁碟/目錄的一或多個來源位置。 維護相同的工作階段識別碼，可讓 hello 工具 toopick 向上 hello 複製的檔案，從它已中斷的地方 hello 最後一次。

不過，相同的複製工作階段不能使用的 tooimport 資料 toodifferent 儲存體帳戶。

當跨多個回合 hello 工具的複製工作階段名稱相同，hello 記錄檔 (/ logdir) 和儲存體帳戶金鑰 (/ sk) 是也預期的 toobe hello 相同。

工作階段識別碼可以包含字母、0~9、底線 (\_)、虛線 (-) 或井字鍵 (#)，且其長度必須是 3~30。

例如︰session-1 或 session#1 或 session\_1

#### <a name="what-is-a-journal-file"></a>什麼是日誌檔案？

每當您執行 WAImportExport 工具 toocopy 檔案 toohello 硬碟機，hello hello 工具會建立複製工作階段。 hello hello 複製工作階段狀態是寫入 toohello 日誌檔。 如果複製工作階段中斷 （例如，由於 tooa 喪失系統電源），它可以繼續執行 hello 工具一次，並指定 hello hello 命令列上的日誌檔中。

為您準備以 hello Azure 匯入/匯出工具每個硬碟，hello 工具將會建立單一日誌檔名稱"&lt;DriveID&gt;.xml"hello 工具的 toohello 磁碟機的磁碟機識別碼是相關聯的 hello 序號已讀取hello 磁碟。 您必須從所有磁碟機 toocreate hello 匯入工作 hello 日誌檔案。 如果中斷 hello 工具 hello 日誌檔也可以是使用的 tooresume 磁碟機準備。

#### <a name="what-is-a-log-directory"></a>什麼是記錄檔目錄？

hello 記錄檔目錄指定目錄 toobe 使用 toostore 詳細資訊記錄檔，以及暫存清單檔。 如果未指定，hello 目前的目錄將會用為 hello 記錄檔目錄。 hello 記錄是詳細資訊記錄。

### <a name="prerequisites"></a>必要條件

#### <a name="what-are-hello-specifications-of-my-disk"></a>我的磁碟的 hello 規格有哪些？

一個或多個空 2.5 英吋或 3.5 吋 SATAII 或 III 硬碟 SSD 磁碟機連線的 toohello 複製電腦。

#### <a name="how-can-i-enable-bitlocker-on-my-machine"></a>如何啟用我電腦上的 BitLocker？

簡單的方式 toocheck 是以滑鼠右鍵按一下系統磁碟機上。 它會顯示您選項 Bitlocker 如果 hello 功能已開啟。 如果此功能已關閉，您就不會看到它。

![檢查 BitLocker](./media/storage-import-export-tool-preparing-hard-drives-import/BitLocker.png)

以下是發行項上[如何 tooenable BitLocker](https://technet.microsoft.com/library/cc766295.aspx)

您的電腦很可能沒有 TPM 晶片。 如果您未取得使用 tpm.msc 輸出，請查看 hello 下一個常見問題集。

#### <a name="how-toodisable-trusted-platform-module-tpm-in-bitlocker"></a>如何 toodisable 中 BitLocker 的信賴平台模組 (TPM)？
> [!NOTE]
> 只有當他們的伺服器中有沒有 TPM，您會需要 toodisable TPM 原則。 如果使用者的伺服器中沒有受信任的 TPM，它是不必要 toodisable TPM。 
> 

在順序 toodisable 中 BitLocker 的 TPM，進行下列步驟的 hello:<br/>
1. 在命令提示字元中輸入 gpedit.msc 以啟動**群組原則編輯器**。 如果**群組原則編輯器**出現 toobe 無法使用，第一次啟用 BitLocker。 請參閱先前的常見問題集。
2. 開啟 [本機電腦原則] &gt;[電腦設定] &gt; [系統管理範本] &gt; [Windows 元件] &gt; [BitLocker 磁碟機加密] &gt; [作業系統磁碟機]。
3. 編輯 [啟動時需要其他驗證] 原則。
4. 設定 hello 原則太**啟用**，並確定**允許在不含相容 TPM 的 BitLocker**已核取。

####  <a name="how-toocheck-if-net-4-or-higher-version-is-installed-on-my-machine"></a>如何 toocheck 如果我的電腦已安裝.NET 4 或更高的版本嗎？

所有 Microsoft .NET Framework 版本均會安裝在下列目錄︰%windir%\Microsoft.NET\Framework\

瀏覽 toohello 提及的組件中的 hello 工具需要 toorun 目標電腦上的上方。 尋找開頭為 "v4" 的資料夾名稱。 如果此目錄不存在，表示您的電腦上並未安裝 .NET 4。 您可以使用 [Microsoft .NET Framework 4 (Web 安裝程式)](https://www.microsoft.com/download/details.aspx?id=17851) 在您的電腦上下載 .Net 4。

### <a name="limits"></a>限制

#### <a name="how-many-drives-can-i-preparesend-at-hello-same-time"></a>多少磁碟機可以我準備/傳送嗨在相同的時間？

沒有可以準備 hello hello 工具的磁碟數目沒有限制。 不過，hello 工具預期的磁碟機代號做為輸入。 這會限制 too25 磁碟同時準備。 單一工作一次最多可處理 10 個磁碟。 如果您準備 10 個以上的磁碟目標 hello 相同儲存體帳戶、 hello 磁碟可以分散安裝在多個工作。

#### <a name="can-i-target-more-than-one-storage-account"></a>可以對應一個以上的儲存體帳戶嗎？

每個工作只能提交一個儲存體帳戶，且一個儲存體帳戶只能用於單一複製工作階段。

### <a name="capabilities"></a>功能

#### <a name="does-waimportexportexe-encrypt-my-data"></a>WAImportExport.exe 是否會加密資料？

是。 此程序會啟用必須的 BitLocker 加密。

#### <a name="what-will-be-hello-hierarchy-of-my-data-when-it-appears-in-hello-storage-account"></a>所要 hello 階層的 我的資料時顯示 hello 儲存體帳戶中？

雖然資料會分散到磁碟，hello 資料上傳時將會交集 toohello 儲存體帳戶回 toohello hello 資料集中的 CSV 檔案中指定的目錄結構。

#### <a name="how-many-of-hello-input-disks-will-have-active-io-in-parallel-when-copy-is-in-progress"></a>多少個 hello 輸入磁碟將有作用中的 IO 以平行方式，正在進行複製？

hello 工具會將資料分散到 hello 輸入 hello hello 輸入檔案大小為基礎的磁碟。 話雖如此，以平行方式的作用中磁碟的 hello 數目完全 delends hello 性質 hello 輸入資料上。 取決於輸入資料集中 hello 的個別檔案的 hello 規模、 一個或多個磁碟可能會以平行方式顯示使用中的 IO。 如需詳細資料，請參閱下一個問題。

#### <a name="how-does-hello-tool-distribute-hello-files-across-hello-disks"></a>如何沒有 hello 工具將 hello 檔案分散到 hello 磁碟？

WAImportExport 工具會以批次方式讀取和寫入檔案，一個批次最多包含 100000 個檔案。 這表示最多可以平行寫入 100000 個檔案。 會寫入多個磁碟，如果這些 100000 檔案 toosimultaneously 分散式 toomulti 磁碟機。 不過是否 hello 工具 toomultiple 磁碟將同時寫入或 hello 累計 hello 批次大小取決於單一磁碟。 比方說，發生較小的檔案，如果所有 10,0000 檔案都在單一磁碟機中，可以 toofit 工具寫入 tooonly 一個磁碟 hello 處理此批次的期間。

### <a name="waimportexport-output"></a>WAImportExport 輸出

#### <a name="there-are-two-journal-files-which-one-should-i-upload-tooazure-portal"></a>有兩個日誌檔，其中應該將上傳 tooAzure 入口網站？

**.xml** -為您準備 hello WAImportExport 工具每個硬碟，hello 工具將會建立單一日誌檔名稱`<DriveID>.xml`其中 DriveID 是相關聯的 hello 序號 toohello hello 工具的磁碟機從磁碟中讀取 hello。 您必須從所有 hello Azure 入口網站中的磁碟機 toocreate hello 匯入工作的 hello 日誌檔案。 這個日誌檔也可以使用的 tooresume 磁碟機準備如果 hello 工具中斷。

**.jrn** -hello 與後置字元的日誌檔`.jrn`hello 狀態包含硬碟機的所有複製工作階段。 也包含 hello 資訊所需 toocreate hello 匯入作業。 您永遠必須指定日誌檔，當執行 hello WAImportExport 工具，以及複製工作階段識別碼。

## <a name="next-steps"></a>後續步驟

* [正在設定 hello Azure 匯入/匯出工具](storage-import-export-tool-setup.md)
* [設定屬性及 hello 期間的中繼資料匯入程序](storage-import-export-tool-setting-properties-metadata-import.md)
* [匯入工作的範例工作流程 tooprepare 硬碟機](storage-import-export-tool-sample-preparing-hard-drives-import-job-workflow.md)
* [常用命令快速參考](storage-import-export-tool-quick-reference.md) 
* [利用複製記錄檔檢閱作業狀態](storage-import-export-tool-reviewing-job-status-v1.md)
* [修復匯入作業](storage-import-export-tool-repairing-an-import-job-v1.md)
* [修復匯出作業](storage-import-export-tool-repairing-an-export-job-v1.md)
* [疑難排解 hello Azure 匯入/匯出工具](storage-import-export-tool-troubleshooting-v1.md)
