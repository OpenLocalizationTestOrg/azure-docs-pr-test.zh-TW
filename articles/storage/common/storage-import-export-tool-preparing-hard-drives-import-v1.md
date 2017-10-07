---
title: "aaaPreparing 硬碟的 Azure 匯入/匯出匯入作業-v1 |Microsoft 文件"
description: "了解如何使用 tooprepare 硬碟 hello WAImportExport v1 工具 toocreate hello Azure 匯入/匯出服務匯入工作。"
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 3d818245-8b1b-4435-a41f-8e5ec1f194b2
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/15/2017
ms.author: muralikk
ms.openlocfilehash: 1eb0c3c51e984e2869b5268254f468d4b43e9d85
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="preparing-hard-drives-for-an-import-job"></a>針對匯入作業準備硬碟
tooprepare 其中一個或多個硬碟以取得匯入工作，請遵循下列步驟：

-   識別 hello 資料 tooimport 到 hello Blob 服務

-   識別目標虛擬目錄和 hello Blob 服務中的 blob

-   判斷需要多少個磁碟機

-   複製您的硬碟機 hello 資料 tooeach

 工作流程的範例，請參閱[硬式磁碟機匯入工作的範例工作流程 tooPrepare](storage-import-export-tool-sample-preparing-hard-drives-import-job-workflow-v1.md)。

## <a name="identify-hello-data-toobe-imported"></a>識別 hello 資料 toobe 匯入
 hello 第一個步驟 toocreating 匯入工作是 toodetermine 哪個目錄和檔案，您將要 tooimport。 可以是目錄清單、唯一檔案的清單或兩者的組合。 包含目錄時，hello 目錄及其子目錄中的所有檔案都會 hello 匯入工作的一部分。

> [!NOTE]
>  由於子目錄以遞迴方式包含包含上層目錄時，指定 hello 上層目錄。 請勿一併指定其任何子目錄。
>
>  目前，hello Microsoft Azure 匯入/匯出工具具有下列限制的 hello： 如果目錄包含超過一個硬碟可以包含的資料，然後 hello 目錄必須 toobe 分解為較小的目錄。 例如，如果目錄包含 2.5 TB 的資料和 hello 硬碟容量是 2 TB，則您 toobreak hello 2.5 TB 的目錄分割成較小的目錄。 中的 hello 工具更新版本，就會解決這項限制。

## <a name="identify-hello-destination-locations-in-hello-blob-service"></a>識別在 hello blob 服務中的 hello 目的地位置
 每個目錄或將匯入的檔案，您需要 tooidentify 目的地虛擬目錄或 hello Azure Blob 服務中的 blob。 您會在輸入 toohello Azure 匯入/匯出工具來使用這些目標。 請注意，應該以 hello 正斜線字元分隔的目錄"/"。

 hello 下表顯示一些 blob 目標的範例：

|來源檔案或目錄|目的地 Blob 或虛擬目錄|
|------------------------------|-------------------------------------------|
|H:\Video|https://mystorageaccount.blob.core.windows.net/video|
|H:\Photo|https://mystorageaccount.blob.core.windows.net/photo|
|K:\Temp\FavoriteVideo.ISO|https://mystorageaccount.blob.core.windows.net/favorite/FavoriteVideo.ISO|
|\\\myshare\john\music|https://mystorageaccount.blob.core.windows.net/music|

## <a name="determine-how-many-drives-are-needed"></a>判斷需要多少個磁碟機
 接下來，您需要 toodetermine:

-   hello 的硬碟數目需要 toostore hello 資料。

-   hello 目錄及/或獨立的檔案將會複製的 tooeach 硬碟機。

 確定您擁有 hello toostore hello 傳輸的資料所必須的硬碟數目。

## <a name="copy-data-tooyour-hard-drive"></a>複製資料 tooyour 硬碟
 本章節描述如何 toocall hello Azure 匯入/匯出工具 toocopy 資料 tooone 或多個硬碟。 每次呼叫 hello Azure 匯入/匯出工具時，您會建立新*複製工作階段*。 您建立至少一個複製工作階段的每個磁碟機 toowhich 複製資料。在某些情況下，您可能需要多個複製工作階段 toocopy 所有資料的 toosingle 磁碟機。 以下是一些您可能需要多個複製工作階段的原因︰

-   您必須為每個用於複製的磁碟機建立個別的複製工作階段。

-   複製工作階段可以複製單一目錄或單一 blob toohello 磁碟機。 如果您複製多個目錄、 多個 blob 或兩者的組合，您將需要 toocreate 多個複製工作階段。

-   您可以指定屬性和中繼資料將匯入做為匯入工作一部分的 hello blob 上設定。 hello 屬性或您指定的複製工作階段的中繼資料將會套用該複製工作階段所指定的 tooall blob。 如果您想要某些 blob toospecify 不同的屬性或中繼資料，您將需要的 toocreate 個別複製工作階段。 請參閱[設定屬性和中繼資料在 hello 匯入程序期間](storage-import-export-tool-setting-properties-metadata-import-v1.md)如需詳細資訊。

> [!NOTE]
>  如果您擁有 hello 需求中所述的多部電腦[設定 hello Azure 匯入/匯出工具](storage-import-export-tool-setup-v1.md)，您也可以在每部機器上執行此工具的執行個體以平行方式複製資料 toomultiple 硬碟機。

 Hello 工具會為您準備以 hello Azure 匯入/匯出工具每個硬碟，建立單一日誌檔。 您必須從所有磁碟機 toocreate hello 匯入工作 hello 日誌檔案。 如果中斷 hello 工具 hello 日誌檔也可以是使用的 tooresume 磁碟機準備。

### <a name="azure-importexport-tool-syntax-for-an-import-job"></a>適用於匯入作業的 Azure 匯入/匯出工具語法
 tooprepare 磁碟機匯入工作，呼叫以 hello hello Azure 匯入/匯出工具**PrepImport**命令。 這是 hello 第一個複製工作階段或後續複製工作階段取決於您加入的參數。

 hello 磁碟機的第一個複製工作階段需要一些額外的參數 toospecify hello 儲存體帳戶金鑰。hello 目標磁碟機代號。是否必須格式化 hello 磁碟機。hello 磁碟機是否必須加密，而且如果是這樣，hello BitLocker 金鑰。和 hello 記錄檔目錄。 以下是初始複本工作階段 toocopy hello 語法，目錄或單一檔案：

 **第一次複製工作階段 toocopy 單一目錄**

 `WAImportExport PrepImport /sk:<StorageAccountKey> /csas:<ContainerSas> /t: <TargetDriveLetter> [/format] [/silentmode] [/encrypt] [/bk:<BitLockerKey>] [/logdir:<LogDirectory>] /j:<JournalFile> /id:<SessionId> /srcdir:<SourceDirectory> /dstdir:<DestinationBlobVirtualDirectory> [/Disposition:<Disposition>] [/BlobType:<BlockBlob|PageBlob>] [/PropertyFile:<PropertyFile>] [/MetadataFile:<MetadataFile>]`

 **第一次複製工作階段 toocopy 單一檔案**

 `WAImportExport PrepImport /sk:<StorageAccountKey> /csas:<ContainerSas> /t: <TargetDriveLetter> [/format] [/silentmode] [/encrypt] [/bk:<BitLockerKey>] [/logdir:<LogDirectory>] /j:<JournalFile> /id:<SessionId> /srcfile:<SourceFile> /dstblob:<DestinationBlobPath> [/Disposition:<Disposition>] [/BlobType:<BlockBlob|PageBlob>] [/PropertyFile:<PropertyFile>] [/MetadataFile:<MetadataFile>]`

 在後續複製工作階段，您不需要 toospecify hello 初始參數。 以下是後續複製工作階段 toocopy hello 語法，目錄或單一檔案：

 **後續複製工作階段 toocopy 單一目錄**

 `WAImportExport PrepImport /j:<JournalFile> /id:<SessionId> /srcdir:<SourceDirectory> /dstdir:<DestinationBlobVirtualDirectory> [/Disposition:<Disposition>] [/BlobType:<BlockBlob|PageBlob>] [/PropertyFile:<PropertyFile>] [/MetadataFile:<MetadataFile>]`

 **後續複製工作階段 toocopy 單一檔案**

 `WAImportExport PrepImport /j:<JournalFile> /id:<SessionId> /srcfile:<SourceFile> /dstblob:<DestinationBlobPath> [/Disposition:<Disposition>] [/BlobType:<BlockBlob|PageBlob>] [/PropertyFile:<PropertyFile>] [/MetadataFile:<MetadataFile>]`

### <a name="parameters-for-hello-first-copy-session-for-a-hard-drive"></a>Hello 參數先複製工作階段的硬碟機
 每次執行 hello Azure 匯入/匯出工具 toocopy 檔 toohello 硬碟 hello 工具會建立複製工作階段。 每個複製工作階段複製單一目錄或單一檔案 tooa 硬碟機。 hello hello 複製工作階段狀態是寫入 toohello 日誌檔。 如果複製工作階段中斷 （例如，由於 tooa 喪失系統電源），它可以繼續執行 hello 工具一次，並指定 hello hello 命令列上的日誌檔中。

> [!WARNING]
>  如果您指定 hello **/格式化**hello 第一個複製工作階段的參數，將格式化 hello 磁碟機，並將清除 hello 磁碟機上的所有資料。 建議您僅使用空白的磁碟機進行複製工作階段。

 每個磁碟機的第一個複製工作階段用於 hello 的 hello 命令需要比 hello 命令的不同參數的後續複製工作階段。 hello 下表列出可供 hello 第一個複製工作階段的 hello 額外參數：

|命令列參數|說明|
|-----------------------------|-----------------|
|**/sk:**<StorageAccountKey\>|`Optional.`將匯入 hello hello 儲存體帳戶 toowhich hello 資料的儲存體帳戶金鑰。 您必須包含**/sk:**< StorageAccountKey\>或**/csas:**< Containersas>\> hello 命令中。|
|**/csas:**<ContainerSas\>|`Optional`。 hello 容器 SAS toouse tooimport 資料 toohello 儲存體帳戶。 您必須包含**/sk:**< StorageAccountKey\>或**/csas:**< Containersas>\> hello 命令中。<br /><br /> 這個參數的 hello 值的開頭必須 hello 容器名稱，後面加上問號 （？） 和 hello SAS 權杖。 例如：<br /><br /> `mycontainer?sv=2014-02-14&sr=c&si=abcde&sig=LiqEmV%2Fs1LF4loC%2FJs9ZM91%2FkqfqHKhnz0JM6bqIqN0%3D&se=2014-11-20T23%3A54%3A14Z&sp=rwdl`<br /><br /> hello 權限，是否 hello URL 或預存的存取原則中指定時，必須包含讀取、 寫入和刪除匯入工作，並讀取、 寫入和清單匯出工作。<br /><br /> 當指定這個參數時，匯入或匯出的所有 blob toobe 都必須 hello hello 共用的存取簽章中指定的容器內。|
|**/t:**<TargetDriveLetter\>|`Required.`hello hello 目前複製工作階段，不含尾端冒號 hello hello 目標硬碟機的磁碟機代號。|
|**/format**|`Optional.`指定此參數，當 hello 磁碟機需要 toobe 格式化;否則請省略它。 Hello 工具格式化 hello 磁碟機之前，會提示您進行確認，以從主控台。 toosuppress hello 確認，請指定 hello /silentmode 參數。|
|**/silentmode**|`Optional.`指定此參數 toosuppress hello 的確認訊息格式 hello 磁碟機。|
|**/encrypt**|`Optional.`當 hello 磁碟機未加密的 BitLocker 和需求 toobe hello 工具來加密，請指定此參數。 如果已使用 BitLocker 加密 hello 磁碟機，然後省略此參數並指定 hello`/bk`參數，以提供 hello 現有的 BitLocker 金鑰。<br /><br /> 如果您指定 hello`/format`參數，則您也必須指定 hello`/encrypt`參數。|
|**/bk:**<BitLockerKey\>|`Optional.`若指定 `/encrypt`，請省略這個參數。 如果`/encrypt`已省略，則您需要 toohave 已加密 hello 與 BitLocker 的磁碟機。 使用此參數 toospecify hello BitLocker 金鑰。 匯入工作的所有硬碟都需要 BitLocker 加密。|
|**/logdir:**<LogDirectory\>|`Optional.`hello 記錄檔目錄指定目錄 toobe 使用 toostore 詳細資訊記錄檔，以及暫存清單檔。 如果未指定，hello 目前的目錄將會用為 hello 記錄檔目錄。|

### <a name="parameters-required-for-all-copy-sessions"></a>所有複製工作階段需要的參數
 hello 日誌檔包含硬碟機的所有複製工作階段的 hello 狀態。 也包含 hello 資訊所需 toocreate hello 匯入作業。 執行 hello Azure 匯入/匯出工具，以及複製工作階段識別碼時，您一律必須指定日誌檔：

|||
|-|-|
|命令列參數|說明|
|**/j:**<JournalFile\>|`Required.`hello 路徑 toohello 日誌檔。 每個磁碟機必須只有一個日誌檔案。 請注意該 hello 日誌檔不得位於 hello 目標磁碟機。 hello 日誌檔的副檔名是`.jrn`。|
|**/id:**<SessionId\>|`Required.`hello 工作階段 ID 識別一個複製工作階段。 它是使用的 tooensure 中斷的複製工作階段的精確的復原。 會在複製工作階段中複製的檔案儲存在名為 hello hello 目標磁碟機上的工作階段識別碼之後的目錄。|

### <a name="parameters-for-copying-a-single-directory"></a>用以複製單一目錄的參數
 當複製單一目錄，hello 下列必要和選擇性的參數適用於：

|命令列參數|說明|
|----------------------------|-----------------|
|**/srcdir:**<SourceDirectory\>|`Required.`包含檔案 toobe hello 來源目錄複製 toohello 目標磁碟機。 hello 目錄路徑必須是絕對路徑 （而不是相對路徑）。|
|**/dstdir:**<DestinationBlobVirtualDirectory\>|`Required.`hello 路徑 toohello 目的地虛擬目錄 Windows Azure 儲存體帳戶中。 hello 虛擬目錄可能或可能不存在。<br /><br /> 您可以指定容器或 Blob 前置詞，如 `music/70s/`。 hello 目的地目錄必須以 hello 容器名稱開頭，後面接著正斜線"/"，而且可能會選擇包含結尾的虛擬 blob 目錄"/"。<br /><br /> Hello 目的地容器為 hello 根容器時，您必須明確指定 hello 根容器，包括 hello 斜線做為`$root/`。 因為 hello 根容器下的 blob 不能包含 「 / 」 在其名稱中，hello 目的目錄為 hello 根容器時，將不會複製 hello 來源目錄中的任何子目錄。<br /><br /> 指定目的地虛擬目錄或 blob 時是確定 toouse 有效的容器名稱。 請記住容器名稱必須是小寫。 關於容器命名規則，請參閱[命名和參考容器、Blob 及中繼資料](/rest/api/storageservices/naming-and-referencing-containers--blobs--and-metadata)。|
|**/Disposition:**<rename&#124;no-overwrite&#124;overwrite>|`Optional.`Hello 的 blob 指定地址已經存在時，請指定 hello 行為。 這個參數的有效值為︰`rename`、`no-overwrite`及 `overwrite`。 請注意，這些值區分大小寫。 如果未不指定任何值，hello 預設值是`rename`。<br /><br /> hello 值指定給此參數會影響指定 hello hello 目錄中的所有 hello 檔案`/srcdir`參數。|
|**/BlobType:**<BlockBlob&#124;PageBlob>|`Optional.`指定 hello hello 目的地 blob 的 blob 類型。 有效值為：`BlockBlob`和 `PageBlob`。 請注意，這些值區分大小寫。 如果未不指定任何值，hello 預設值是`BlockBlob`。<br /><br /> 在大部分情況下，建議使用 `BlockBlob`。 如果您指定`PageBlob`，hello hello 目錄中每個檔案的長度必須是 512，針對分頁 blob 的頁面的 hello 大小的倍數。|
|**/PropertyFile:**<PropertyFile\>|`Optional.`路徑 toohello hello 目的地 blob 的內容檔案。 如需詳細資訊，請參閱[匯入/匯出服務中繼資料和屬性檔案格式](../storage-import-export-file-format-metadata-and-properties.md)。|
|**/MetadataFile:**<MetadataFile\>|`Optional.`路徑 toohello hello 目的地 blob 的中繼資料檔案。 如需詳細資訊，請參閱[匯入/匯出服務中繼資料和屬性檔案格式](../storage-import-export-file-format-metadata-and-properties.md)。|

### <a name="parameters-for-copying-a-single-file"></a>用以複製單一檔案的參數
 當複製單一檔案，hello 必要和選擇性套用下列參數：

|命令列參數|說明|
|----------------------------|-----------------|
|**/srcfile:**<SourceFile\>|`Required.`hello 完整路徑 toohello 檔案 toobe 複製。 hello 目錄路徑必須是絕對路徑 （而不是相對路徑）。|
|**/dstblob:**<DestinationBlobPath\>|`Required.`hello 路徑 toohello 目的地 blob 在 Windows Azure 儲存體帳戶。 hello blob 可能會或可能不存在。<br /><br /> 指定 hello 容器名稱開頭 hello blob 名稱。 hello blob 名稱不得以"/"或 hello 儲存體帳戶名稱。 關於 Blob 命名規則，請參閱[命名和參考容器、Blob 及中繼資料](/rest/api/storageservices/naming-and-referencing-containers--blobs--and-metadata)。<br /><br /> Hello 目的地容器為 hello 根容器時，您必須明確指定`$root`hello 容器，例如當`$root/sample.txt`。 請注意，hello 根容器下的 blob 不能包含"/"中的名稱。|
|**/Disposition:**<rename&#124;no-overwrite&#124;overwrite>|`Optional.`Hello 的 blob 指定地址已經存在時，請指定 hello 行為。 這個參數的有效值為︰`rename`、`no-overwrite`及 `overwrite`。 請注意，這些值區分大小寫。 如果未不指定任何值，hello 預設值是`rename`。|
|**/BlobType:**<BlockBlob&#124;PageBlob>|`Optional.`指定 hello hello 目的地 blob 的 blob 類型。 有效值為：`BlockBlob`和 `PageBlob`。 請注意，這些值區分大小寫。 如果未不指定任何值，hello 預設值是`BlockBlob`。<br /><br /> 在大部分情況下，建議使用 `BlockBlob`。 如果您指定`PageBlob`，hello hello 目錄中每個檔案的長度必須是 512，針對分頁 blob 的頁面的 hello 大小的倍數。|
|**/PropertyFile:**<PropertyFile\>|`Optional.`路徑 toohello hello 目的地 blob 的內容檔案。 如需詳細資訊，請參閱[匯入/匯出服務中繼資料和屬性檔案格式](../storage-import-export-file-format-metadata-and-properties.md)。|
|**/MetadataFile:**<MetadataFile\>|`Optional.`路徑 toohello hello 目的地 blob 的中繼資料檔案。 如需詳細資訊，請參閱[匯入/匯出服務中繼資料和屬性檔案格式](../storage-import-export-file-format-metadata-and-properties.md)。|

### <a name="resuming-an-interrupted-copy-session"></a>繼續中斷的複製工作階段
 如果複製工作階段因故中斷，您可以執行 hello 工具並使用只 hello 指定日誌檔來繼續：

```
WAImportExport.exe PrepImport /j:<JournalFile> /id:<SessionId> /ResumeSession
```

 只有 hello 最近複製工作階段，不正常終止可以繼續。

> [!IMPORTANT]
>  當您繼續複製工作階段時，請勿修改 hello 來源資料檔案和目錄加入或移除檔案。

### <a name="aborting-an-interrupted-copy-session"></a>中止中斷的複製工作階段
 如果複製工作階段中斷，而且它不可能 tooresume （例如，如果來源目錄已證實無法存取），您就必須中止 hello 目前工作階段，以便可以復原該交易可以啟動後，新的複製工作階段：

```
WAImportExport.exe PrepImport /j:<JournalFile> /id:<SessionId> /AbortSession
```

 只有 hello 最後一個複製工作階段，不正常終止會中止。 請注意，您無法停止 hello 磁碟機的第一個複製工作階段。 相反地，您必須使用新的日誌檔重新 hello 複製工作階段。

## <a name="next-steps"></a>後續步驟

* [正在設定 hello Azure 匯入/匯出工具](storage-import-export-tool-setup-v1.md)
* [設定屬性及 hello 期間的中繼資料匯入程序](storage-import-export-tool-setting-properties-metadata-import-v1.md)
* [匯入工作的範例工作流程 tooprepare 硬碟機](storage-import-export-tool-sample-preparing-hard-drives-import-job-workflow-v1.md)
* [常用命令快速參考](storage-import-export-tool-quick-reference-v1.md) 
* [利用複製記錄檔檢閱作業狀態](storage-import-export-tool-reviewing-job-status-v1.md)
* [修復匯入作業](storage-import-export-tool-repairing-an-import-job-v1.md)
* [修復匯出作業](storage-import-export-tool-repairing-an-export-job-v1.md)
* [疑難排解 hello Azure 匯入/匯出工具](storage-import-export-tool-troubleshooting-v1.md)
