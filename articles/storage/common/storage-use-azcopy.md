---
title: "aaaCopy 或移動資料 tooAzure 利用 azcopy 進行 Windows 上的儲存體 |Microsoft 文件"
description: "使用 hello AzCopy 上的 Windows 公用程式 toomove 或複製資料 tooor 從 blob、 資料表和檔案內容。 複製資料 tooAzure 存放裝置從本機檔案，或複製資料內或之間的儲存體帳戶。 輕鬆地將移轉您的資料 tooAzure 儲存體。"
services: storage
documentationcenter: 
author: seguler
manager: jahogg
editor: tysonn
ms.assetid: aa155738-7c69-4a83-94f8-b97af4461274
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/14/2017
ms.author: seguler
ms.openlocfilehash: a063a0380b7b8e6b212d0cec276f7d0f421936ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="transfer-data-with-hello-azcopy-on-windows"></a>傳送資料，以在 Windows 上的 AzCopy hello
AzCopy 是設計來複製資料 tooand 從 Microsoft Azure Blob、 檔案和資料表儲存體使用簡單的命令，以獲得最佳效能的命令列公用程式。 儲存體帳戶內或之間的儲存體帳戶，您可以從一個物件 tooanother 複製資料。

有兩個 AzCopy 版本可供您下載。 AzCopy on Windows 內建有 .NET Framework，並且提供 Windows 樣式的命令列選項。 [AzCopy on Linux](storage-use-azcopy-linux.md) 內建有 .NET Core Framework，其以提供 POSIX 樣式命令列選項的 Linux 平台為目標。 本文涵蓋之內容包括 AzCopy on Windows。

## <a name="download-and-install-azcopy"></a>下載並安裝 AzCopy
### <a name="azcopy-on-windows"></a>AzCopy on Windows
下載 hello[最新版本的 Windows 上的 AzCopy](http://aka.ms/downloadazcopy)。

#### <a name="installation-on-windows"></a>在 Windows 上安裝
安裝之後 AzCopy 使用 hello 安裝程式在 Windows 上，開啟命令視窗，並瀏覽在您的電腦-toohello AzCopy 安裝目錄，其中 hello`AzCopy.exe`可執行檔所在。 如有需要，您可以加入 hello AzCopy 安裝位置 tooyour 系統路徑。 根據預設，AzCopy 會太安裝`%ProgramFiles(x86)%\Microsoft SDKs\Azure\AzCopy`或`%ProgramFiles%\Microsoft SDKs\Azure\AzCopy`。

## <a name="writing-your-first-azcopy-command"></a>撰寫第一個 AzCopy 命令
hello 的 AzCopy 命令的基本語法如下：

```azcopy
AzCopy /Source:<source> /Dest:<destination> [Options]
```

hello 遵循範例示範的各種案例來複製資料 tooand 從 Microsoft Azure Blob、 檔案和資料表。 請參閱 toohello [AzCopy 參數](#azcopy-parameters)hello 參數，每個範例中所使用的詳細說明一節。

## <a name="blob-download"></a>Blob：下載
### <a name="download-single-blob"></a>下載單一 Blob

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /Pattern:"abc.txt"
```

請注意，如果 hello 資料夾`C:\myfolder`不存在，AzCopy 會建立它，並下載`abc.txt `hello 新資料夾。

### <a name="download-single-blob-from-secondary-region"></a>從次要地區下載單一 Blob

```azcopy
AzCopy /Source:https://myaccount-secondary.blob.core.windows.net/mynewcontainer /Dest:C:\myfolder /SourceKey:key /Pattern:abc.txt
```

請注意，您必須啟用讀取權限異地備援儲存體。

### <a name="download-all-blobs"></a>下載所有 Blob

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /S
```

假設下列 hello 位於 hello 指定容器的 blob:  

    abc.txt
    abc1.txt
    abc2.txt
    vd1\a.txt
    vd1\abcd.txt

Hello 下載作業之後，hello 目錄`C:\myfolder`包含下列檔案的 hello:

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt
    C:\myfolder\vd1\a.txt
    C:\myfolder\vd1\abcd.txt

如果您未指定選項 `/S`，則不會下載任何 Blob。

### <a name="download-blobs-with-specified-prefix"></a>下載具有指定首碼的 Blob

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /Pattern:a /S
```

假設 hello 下列 blob 位於 hello 指定的容器。 以 hello 前置詞開頭的所有 blob`a`下載：

    abc.txt
    abc1.txt
    abc2.txt
    xyz.txt
    vd1\a.txt
    vd1\abcd.txt

Hello 下載作業之後，hello 資料夾`C:\myfolder`包含下列檔案的 hello:

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt

hello 前置詞會套用 toohello 虛擬目錄，可形成 hello hello blob 名稱第一個部分。 Hello 虛擬目錄在 hello 上述範例中，它不符合 hello 指定之前置詞，因此它不會下載。 此外，如果 hello 選項`\S`未指定，AzCopy 不會下載任何 blob。

### <a name="set-hello-last-modified-time-of-exported-files-toobe-same-as-hello-source-blobs"></a>設定 hello toobe 匯出的檔案的上次修改時間與 hello 來源 blob 相同

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /MT
```

您也可以從其上次修改時間為基礎的 hello 下載作業排除的 blob。 例如，如果您想 tooexclude blob 的上次修改的時間為 hello 相同或較 hello 目的地檔案，加入 hello`/XN`選項：

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /MT /XN
```

如果您想 tooexclude blob 的上次修改的時間為 hello 相同或比 hello 目的地檔案還舊，新增 hello 或`/XO`選項：

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /MT /XO
```

## <a name="blob-upload"></a>Blob：上傳
### <a name="upload-single-file"></a>上傳單一檔案

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Pattern:"abc.txt"
```

如果 hello 指定的目的地容器不存在，AzCopy 建立及上傳 hello 到其中的檔案。

### <a name="upload-single-file-toovirtual-directory"></a>單一檔案上傳 toovirtual 目錄

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer/vd /DestKey:key /Pattern:abc.txt
```

如果 hello 指定虛擬目錄不存在，AzCopy 上傳 hello 檔案 tooinclude hello 虛擬目錄名稱 (*例如*， `vd/abc.txt` hello 上述範例中)。

### <a name="upload-all-files"></a>上傳所有檔案

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /S
```

指定選項`/S`hello 上傳 hello 內容所指定目錄 tooBlob 儲存體以遞迴方式，這表示所有子資料夾及檔案會上傳以及。 比方說，假設 hello 下列檔案位於資料夾`C:\myfolder`:

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt
    C:\myfolder\subfolder\a.txt
    C:\myfolder\subfolder\abcd.txt

Hello 上傳作業之後，hello 容器會包含下列檔案的 hello:

    abc.txt
    abc1.txt
    abc2.txt
    subfolder\a.txt
    subfolder\abcd.txt

如果您未指定選項 `/S`，AzCopy 不會以遞迴方式上傳。 Hello 上傳作業之後，hello 容器會包含下列檔案的 hello:

    abc.txt
    abc1.txt
    abc2.txt

### <a name="upload-files-matching-specified-pattern"></a>上傳符合指定模式的檔案

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Pattern:a* /S
```

假設 hello 下列檔案位於資料夾`C:\myfolder`:

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt
    C:\myfolder\xyz.txt
    C:\myfolder\subfolder\a.txt
    C:\myfolder\subfolder\abcd.txt

Hello 上傳作業之後，hello 容器會包含下列檔案的 hello:

    abc.txt
    abc1.txt
    abc2.txt
    subfolder\a.txt
    subfolder\abcd.txt

如果您未指定選項 `/S`，AzCopy 只會上傳沒有位於虛擬目錄的 Blob：

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt

### <a name="specify-hello-mime-content-type-of-a-destination-blob"></a>指定目的地 blob hello MIME 內容的類型
根據預設，AzCopy 設定 hello 的目的地 blob 的內容型別太`application/octet-stream`。 從 3.1.0 版開始，您可以明確指定 hello 透過 hello 選項的內容類型`/SetContentType:[content-type]`。 此語法中上傳作業設定 hello 的所有 blob 的內容類型。

```azcopy
AzCopy /Source:C:\myfolder\ /Dest:https://myaccount.blob.core.windows.net/myContainer/ /DestKey:key /Pattern:ab /SetContentType:video/mp4
```

如果您指定`/SetContentType`沒有值，AzCopy 會設定每個 blob 或根據 tooits 副檔名的檔案的內容類型。

```azcopy
AzCopy /Source:C:\myfolder\ /Dest:https://myaccount.blob.core.windows.net/myContainer/ /DestKey:key /Pattern:ab /SetContentType
```

## <a name="blob-copy"></a>Blob：複製
### <a name="copy-single-blob-within-storage-account"></a>複製儲存體帳戶內的單一 Blob

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer1 /Dest:https://myaccount.blob.core.windows.net/mycontainer2 /SourceKey:key /DestKey:key /Pattern:abc.txt
```

當您複製儲存體帳戶內的 Blob 時，系統會執行 [伺服器端複製](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) 作業。

### <a name="copy-single-blob-across-storage-accounts"></a>跨儲存體帳戶複製單一 Blob

```azcopy
AzCopy /Source:https://sourceaccount.blob.core.windows.net/mycontainer1 /Dest:https://destaccount.blob.core.windows.net/mycontainer2 /SourceKey:key1 /DestKey:key2 /Pattern:abc.txt
```

當您跨儲存體帳戶複製 Blob 時，系統會執行 [伺服器端複製](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) 作業。

### <a name="copy-single-blob-from-secondary-region-tooprimary-region"></a>從次要區域 tooprimary 區域複製單一 blob

```azcopy
AzCopy /Source:https://myaccount1-secondary.blob.core.windows.net/mynewcontainer1 /Dest:https://myaccount2.blob.core.windows.net/mynewcontainer2 /SourceKey:key1 /DestKey:key2 /Pattern:abc.txt
```

請注意，您必須啟用讀取權限異地備援儲存體。

### <a name="copy-single-blob-and-its-snapshots-across-storage-accounts"></a>跨儲存體帳戶複製單一 Blob 及其快照

```azcopy
    AzCopy /Source:https://sourceaccount.blob.core.windows.net/mycontainer1 /Dest:https://destaccount.blob.core.windows.net/mycontainer2 /SourceKey:key1 /DestKey:key2 /Pattern:abc.txt /Snapshot
```

Hello 複製作業之後，hello 目標容器包含 hello blob 和其快照集。 假設在 hello 上述範例中的 hello blob 具有兩個快照集，hello 容器包含 hello 下列 blob 和快照集：

    abc.txt
    abc (2013-02-25 080757).txt
    abc (2014-02-21 150331).txt

### <a name="synchronously-copy-blobs-across-storage-accounts"></a>以同步方式跨儲存體帳戶複製 Blob
根據預設，AzCopy 會以非同步方式在兩個儲存體端點之間複製資料。 因此，複製 hello 背景使用的備用頻寬容量且沒有 SLA 方面的速度有多快 blob 中的 hello 複製作業執行時，而且 AzCopy 定期檢查 hello 複製狀態，直到 hello 複製完成或失敗。

hello`/SyncCopy`選項可確保 hello 複製作業取得一致的速度。 AzCopy 下載 hello blob 執行 hello 同步複本 toocopy hello 從指定來源 toolocal 記憶體，並再將其上傳 toohello Blob 儲存體目的地。

```azcopy
AzCopy /Source:https://myaccount1.blob.core.windows.net/myContainer/ /Dest:https://myaccount2.blob.core.windows.net/myContainer/ /SourceKey:key1 /DestKey:key2 /Pattern:ab /SyncCopy
```

`/SyncCopy`可能會用來產生建議的方法包括的額外成本比較的 tooasynchronous 複製 hello 的輸出是 toouse 處於 hello Azure VM 中的這個選項與您來源儲存體帳戶 tooavoid 出口成本相同的區域。

## <a name="file-download"></a>檔案：下載
### <a name="download-single-file"></a>下載單一檔案

```azcopy
AzCopy /Source:https://myaccount.file.core.windows.net/myfileshare/myfolder1/ /Dest:C:\myfolder /SourceKey:key /Pattern:abc.txt
```

如果 hello 指定來源是 Azure 的檔案共用，則您必須指定 hello 確切的檔名，(*例如* `abc.txt`) toodownload 單一檔案，或指定選項`/S`toodownload 所有檔案在 hello 共用以遞迴方式。 檔案模式和選項，嘗試 toospecify`/S`一起會產生錯誤。

### <a name="download-all-files"></a>下載所有檔案

```azcopy
AzCopy /Source:https://myaccount.file.core.windows.net/myfileshare/ /Dest:C:\myfolder /SourceKey:key /S
```

請注意，並不會下載任何空白資料夾。

## <a name="file-upload"></a>檔案：上傳
### <a name="upload-single-file"></a>上傳單一檔案

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.file.core.windows.net/myfileshare/ /DestKey:key /Pattern:abc.txt
```

### <a name="upload-all-files"></a>上傳所有檔案

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.file.core.windows.net/myfileshare/ /DestKey:key /S
```

請注意，並不會上傳任何空白資料夾。

### <a name="upload-files-matching-specified-pattern"></a>上傳符合指定模式的檔案

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.file.core.windows.net/myfileshare/ /DestKey:key /Pattern:ab* /S
```

## <a name="file-copy"></a>檔案：複製
### <a name="copy-across-file-shares"></a>跨檔案共用複製

```azcopy
AzCopy /Source:https://myaccount1.file.core.windows.net/myfileshare1/ /Dest:https://myaccount2.file.core.windows.net/myfileshare2/ /SourceKey:key1 /DestKey:key2 /S
```
當您跨檔案共用複製檔案時，系統會執行[伺服器端複製](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx)作業。

### <a name="copy-from-file-share-tooblob"></a>從檔案共用 tooblob 複製

```azcopy
AzCopy /Source:https://myaccount1.file.core.windows.net/myfileshare/ /Dest:https://myaccount2.blob.core.windows.net/mycontainer/ /SourceKey:key1 /DestKey:key2 /S
```
當您複製檔案從檔案共用 tooblob，[伺服器端副本](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx)執行作業。


### <a name="copy-from-blob-toofile-share"></a>複製 blob toofile 共用

```azcopy
AzCopy /Source:https://myaccount1.blob.core.windows.net/mycontainer/ /Dest:https://myaccount2.file.core.windows.net/myfileshare/ /SourceKey:key1 /DestKey:key2 /S
```
當您複製檔案從 blob toofile 共用，[伺服器端副本](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx)執行作業。

### <a name="synchronously-copy-files"></a>以同步方式複製檔案
您可以指定 hello`/SyncCopy`選項 toocopy 資料檔案儲存體 tooFile 存放裝置，從檔案儲存體 tooBlob 存放裝置，然後從 Blob 儲存體 tooFile 存放同步執行，AzCopy 會下載 hello 來源資料 toolocal 記憶體並將它上傳再次 toodestination。 這會產生標準輸出成本。

```azcopy
AzCopy /Source:https://myaccount1.file.core.windows.net/myfileshare1/ /Dest:https://myaccount2.file.core.windows.net/myfileshare2/ /SourceKey:key1 /DestKey:key2 /S /SyncCopy
```

當複製檔案的儲存體 tooBlob 儲存體，hello 預設 blob 型別是區塊 blob，使用者可以指定選項`/BlobType:page`toochange hello 目的地 blob 類型。

請注意，`/SyncCopy`可能會產生額外成本比較 tooasynchronous 複製的輸出，hello 建議的方法是中的這個選項 hello Azure VM 中 hello toouse 來源儲存體帳戶 tooavoid 出口成本與相同的區域。

## <a name="table-export"></a>資料表：匯出
### <a name="export-table"></a>匯出資料表

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:C:\myfolder\ /SourceKey:key
```

AzCopy 寫入資訊清單檔案 toohello 指定的目的地資料夾。 hello 資訊清單檔案用於 hello 匯入程序 toolocate hello 必要的資料檔案，並執行資料驗證。 hello 資訊清單檔案會使用下列預設的命名慣例的 hello:

    <account name>_<table name>_<timestamp>.manifest

使用者也可以指定 hello 選項`/Manifest:<manifest file name>`tooset hello 資訊清單檔案名稱。

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:C:\myfolder\ /SourceKey:key /Manifest:abc.manifest
```

### <a name="split-export-into-multiple-files"></a>將匯出分割成多個檔案

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/mytable/ /Dest:C:\myfolder /SourceKey:key /S /SplitSize:100
```

使用 AzCopy*成交量*hello 資料分割中檔案名稱 toodistinguish 多個檔案。 hello 磁碟區索引由兩個部分組成，*資料分割索引鍵範圍索引*和*分割檔案索引*。 兩個索引皆以零為基礎。

hello 資料分割索引鍵範圍索引為 0，如果 hello 使用者未指定選項`/PKRS`。

例如，假設 AzCopy 會產生兩個資料檔案之後 hello 使用者指定選項, `/SplitSize`。 可能造成資料檔案名稱的 hello:

    myaccount_mytable_20140903T051850.8128447Z_0_0_C3040FE8.json
    myaccount_mytable_20140903T051850.8128447Z_0_1_0AB9AC20.json

請注意該 hello 最小可能值選項`/SplitSize`為 32 MB。 如果 hello 指定目的地 Blob 儲存體，AzCopy 分割 hello 資料檔案，一旦它的大小達到 hello blob 大小上限 (200 GB)，不論是否選項`/SplitSize`hello 使用者尚未指定。

### <a name="export-table-toojson-or-csv-data-file-format"></a>匯出資料表 tooJSON 或 CSV 資料檔格式
預設的 AzCopy 匯出資料表 tooJSON 資料檔案。 您可以指定 hello 選項`/PayloadFormat:JSON|CSV`tooexport hello 資料表做為 JSON 或 CSV。

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:C:\myfolder\ /SourceKey:key /PayloadFormat:CSV
```

指定 hello CSV 裝載格式，AzCopy 也會產生結構描述檔案具有副檔名`.schema.csv`每個資料檔。

### <a name="export-table-entities-concurrently"></a>並行匯出資料表實體

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:C:\myfolder\ /SourceKey:key /PKRS:"aa#bb"
```

AzCopy hello 使用者指定 選項時，請啟動並行作業 tooexport 實體`/PKRS`。 每個作業分別會匯出一個資料分割索引鍵範圍。

請注意 hello 並行作業的數目也由選項`/NC`。 AzCopy hello 預設值為使用核心處理器的 hello 數目`/NC`複製資料表實體時即使`/NC`未指定。 當 hello 使用者指定選項`/PKRS`，AzCopy 會使用 hello 的並行作業 toostart hello 兩個值-使用隱含或明確地指定並行作業與資料分割索引鍵範圍-toodetermine hello 數目的較小者。 如需詳細資訊，請輸入`AzCopy /?:NC`在 hello 命令列。

### <a name="export-table-tooblob"></a>匯出資料表 tooblob

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:https://myaccount.blob.core.windows.net/mycontainer/ /SourceKey:key1 /Destkey:key2
```

AzCopy 會將 JSON 資料檔產生至 hello blob 容器中具有下列命名慣例：

    <account name>_<table name>_<timestamp>_<volume index>_<CRC>.json

hello 產生 JSON 資料檔會遵循最小中繼資料的 hello 裝載格式。 如需此裝載格式的詳細資訊，請參閱 [資料表服務作業的裝載格式](http://msdn.microsoft.com/library/azure/dn535600.aspx)。

請注意，匯出資料表 tooblobs 時, AzCopy 會下載 hello 資料表實體 toolocal 暫存資料檔案，然後將這些實體 toohello blob 上傳。 這些暫存資料檔案會放入與 hello 預設路徑 hello 日誌檔案的資料夾"<code>%LocalAppData%\Microsoft\Azure\AzCopy</code>」，您可以指定選項/z: [日誌-檔案-資料夾] toochange hello 日誌檔案資料夾位置，並因此變更 hello 暫存資料檔案位置。 hello 雖然一旦它已在本機磁碟中的 hello 暫存資料檔案會立即刪除，檔案的大小由資料表實體的大小和您指定了與 hello 選項 /SplitSize，hello 大小來決定暫存資料上傳 toohello blob，請確定您有足夠的本機磁碟空間 toostore 這些暫存資料檔案之前，先刪除它們。

## <a name="table-import"></a>資料表：匯入
### <a name="import-table"></a>匯入資料表

```azcopy
AzCopy /Source:C:\myfolder\ /Dest:https://myaccount.table.core.windows.net/mytable1/ /DestKey:key /Manifest:"myaccount_mytable_20140103T112020.manifest" /EntityOperation:InsertOrReplace
```

hello 選項`/EntityOperation`表示成 tooinsert 實體 hello 資料表的方式。 可能的值包括：

* `InsertOrSkip`： 略過現有的實體，或如果不存在於 hello 資料表插入新實體。
* `InsertOrMerge`： 會合併現有的實體，或不存在於 hello 資料表插入新實體。
* `InsertOrReplace`： 取代現有的實體，或不存在於 hello 資料表插入新實體。

請注意，您不能指定選項`/PKRS`hello 匯入案例中。 不同於 hello 匯出案例中，您必須在其中指定選項`/PKRS`toostart 並行作業，AzCopy 並行作業，預設會啟動匯入資料表時。 並行作業啟動的 hello 預設數目是相等的 toohello 核心處理器數目;不過，您可以指定不同數目的並行選項`/NC`。 如需詳細資訊，請輸入`AzCopy /?:NC`在 hello 命令列。

請注意，AzCopy 只支援匯入 JSON 而不支援匯入 CSV。 AzCopy 不支援從使用者建立的 JSON 和資訊清單檔案匯入資料表。 這兩種檔案都必須來自 AzCopy 資料表匯出。 tooavoid 錯誤，請勿修改 hello 匯出 JSON 或資訊清單檔案。

### <a name="import-entities-tootable-using-blobs"></a>匯入實體 tootable 使用 blob
假設 Blob 容器包含 hello 下列： 代表 Azure 資料表和其隨附的資訊清單檔案的 JSON 檔案。

    myaccount_mytable_20140103T112020.manifest
    myaccount_mytable_20140103T112020_0_0_0AF395F1DC42E952.json

您可以執行下列命令 tooimport 實體插入資料表，使用該 blob 容器中的 hello 資訊清單檔案的 hello:

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:https://myaccount.table.core.windows.net/mytable /SourceKey:key1 /DestKey:key2 /Manifest:"myaccount_mytable_20140103T112020.manifest" /EntityOperation:"InsertOrReplace"
```

## <a name="other-azcopy-features"></a>其他 AzCopy 功能
### <a name="only-copy-data-that-doesnt-exist-in-hello-destination"></a>只複製 hello 目的地中不存在的資料
hello`/XO`和`/XN`參數可讓您從要複製，分別 tooexclude 更舊或更新的來源資源。 如果您只想 toocopy 來源資源不存在於 hello 目的地中，您可以在 hello AzCopy 命令中指定這兩個參數：

    /Source:http://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:<sourcekey> /S /XO /XN

    /Source:C:\myfolder /Dest:http://myaccount.file.core.windows.net/myfileshare /DestKey:<destkey> /S /XO /XN

    /Source:http://myaccount.blob.core.windows.net/mycontainer /Dest:http://myaccount.blob.core.windows.net/mycontainer1 /SourceKey:<sourcekey> /DestKey:<destkey> /S /XO /XN

請注意，這不支援當 hello 來源或目的地資料表。

### <a name="use-a-response-file-toospecify-command-line-parameters"></a>您可以使用回應檔案 toospecify 命令列參數

```azcopy
AzCopy /@:"C:\responsefiles\copyoperation.txt"
```

您可以在回應檔案中包含任何 AzCopy 命令列參數。 AzCopy 處理程序 hello hello 檔案中的參數，如同它們已執行 hello 檔案直接替代與 hello 內容的 hello 命令列上指定。

假設名為的回應檔案`copyoperation.txt`，其中包含下列行 hello。 每個 AzCopy 參數可以指定在同一行

    /Source:http://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:<sourcekey> /S /Y

或不同行：

    /Source:http://myaccount.blob.core.windows.net/mycontainer
    /Dest:C:\myfolder
    /SourceKey:<sourcekey>
    /S
    /Y

AzCopy 失敗如果 hello 參數分成兩行，如下所示為 hello`/sourcekey`參數：

    http://myaccount.blob.core.windows.net/mycontainer
     C:\myfolder
    /sourcekey:
    <sourcekey>
    /S
    /Y

### <a name="use-multiple-response-files-toospecify-command-line-parameters"></a>使用多個回應檔案 toospecify 命令列參數
假設名為 `source.txt` 且指定來源容器的回應檔案：

    /Source:http://myaccount.blob.core.windows.net/mycontainer

名為的回應檔案和`dest.txt`hello 檔案系統中指定的目的地資料夾：

    /Dest:C:\myfolder

及名為 `options.txt` 且指定 AzCopy 選項的回應檔案：

    /S /Y

這些回應檔案 toocall AzCopy，全部都是位於目錄`C:\responsefiles`，使用此命令：

```azcopy
AzCopy /@:"C:\responsefiles\source.txt" /@:"C:\responsefiles\dest.txt" /SourceKey:<sourcekey> /@:"C:\responsefiles\options.txt"   
```

AzCopy 會處理這個命令就如同您所包含的所有 hello hello 命令列上的個別參數都一樣：

```azcopy
AzCopy /Source:http://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:<sourcekey> /S /Y
```

### <a name="specify-a-shared-access-signature-sas"></a>指定共用存取簽章 (SAS)

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer1 /Dest:https://myaccount.blob.core.windows.net/mycontainer2 /SourceSAS:SAS1 /DestSAS:SAS2 /Pattern:abc.txt
```

您也可以指定 SAS hello 容器 URI 上：

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer1/?SourceSASToken /Dest:C:\myfolder /S
```

### <a name="journal-file-folder"></a>日誌檔案資料夾
每次您提交命令 tooAzCopy，它會檢查日誌檔是否存在於 hello 預設資料夾，或是否有您指定透過這個選項的資料夾中。 如果在任一處，hello 日誌檔不存在，AzCopy hello 作業視為新，並產生新的日誌檔。

如果 hello 日誌檔案存在，AzCopy 會檢查您輸入的 hello 命令列是否符合 hello hello 筆記本檔案中的命令列。 如果兩個命令列 hello 相符，AzCopy 會繼續 hello 未完成作業。 如果不相符，則提示的 tooeither 覆寫 hello 日誌檔案 toostart，新增作業或 toocancel hello 目前的作業。

如果您想 hello 日誌檔 toouse hello 預設位置：

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Z
```

如果您省略選項`/Z`，或指定選項`/Z`未 hello 資料夾路徑，如上所示，AzCopy 會建立 hello 日誌檔 hello 預設位置，也就是在`%SystemDrive%\Users\%username%\AppData\Local\Microsoft\Azure\AzCopy`。 如果 hello 日誌檔已經存在，然後 AzCopy 會繼續 hello hello 日誌檔為基礎的作業。

如果您想 toospecify hello 日誌檔的自訂位置：

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Z:C:\journalfolder\
```

如果不存在，此範例會建立 hello 日誌檔。 如果檔案存在，然後 AzCopy 會繼續依據 hello 日誌檔的 hello 作業。

如果您想 tooresume AzCopy 作業：

```azcopy
AzCopy /Z:C:\journalfolder\
```

此範例也會繼續 hello 最後一個作業，可能無法 toocomplete。

### <a name="generate-a-log-file"></a>產生記錄檔

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /V
```

如果您指定選項`/V`但未提供檔案路徑 toohello 詳細資訊記錄檔，再 AzCopy hello 記錄檔中建立 hello 預設位置，也就是`%SystemDrive%\Users\%username%\AppData\Local\Microsoft\Azure\AzCopy`。

否則，您可以在自訂位置建立記錄檔：

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /V:C:\myfolder\azcopy1.log
```

請注意，如果您指定下列選項的相對路徑`/V`，例如`/V:test/azcopy1.log`，則 hello 詳細資訊記錄檔會建立名為的子資料夾內 hello 目前工作目錄中`test`。

### <a name="specify-hello-number-of-concurrent-operations-toostart"></a>指定的並行作業 toostart hello
選項`/NC`指定 hello 並行的複製作業數目。 根據預設，AzCopy 會啟動特定數目的並行作業 tooincrease hello 資料傳輸輸送量。 資料表作業，hello 並行作業的數目會等於 toohello 您擁有的處理器數目。 為 Blob 和檔案作業中，並行作業的 hello 數目等於的處理器您有 8 次 hello 數目。 如果您正在執行 AzCopy 透過低頻寬網路，您可以指定較低的數字，因資源競爭 /NC tooavoid 失敗。

### <a name="run-azcopy-against-azure-storage-emulator"></a>針對 Azure 儲存體模擬器執行 AzCopy
您可以針對 hello 執行 AzCopy [Azure 儲存體模擬器](storage-use-emulator.md)的 Blob:

```azcopy
AzCopy /Source:https://127.0.0.1:10000/myaccount/mycontainer/ /Dest:C:\myfolder /SourceKey:key /SourceType:Blob /S
```

以及針對資料表來執行：

```azcopy
AzCopy /Source:https://127.0.0.1:10002/myaccount/mytable/ /Dest:C:\myfolder /SourceKey:key /SourceType:Table
```

## <a name="azcopy-parameters"></a>AzCopy 參數
以下內容說明 AzCopy 的參數。 您也可以輸入 hello 的說明使用 AzCopy hello 命令列中的下列命令：

* 如需 AzCopy 的詳細命令列說明： `AzCopy /?`
* 如需任何 AzCopy 參數的詳細說明： `AzCopy /?:SourceKey`
* 如需命令列範例： `AzCopy /?:Samples`

### <a name="sourcesource"></a>/Source:"source"
指定從哪個 toocopy hello 來源資料。 hello 來源可以是檔案系統目錄、 blob 容器、 blob 的虛擬目錄、 儲存體檔案共用、 儲存檔案目錄或 Azure 資料表。

**適用於：** Blob、檔案、資料表

### <a name="destdestination"></a>/Dest:"destination"
指定要 hello 目的地 toocopy。 hello 目的地可以是檔案系統目錄、 blob 容器、 blob 的虛擬目錄、 儲存體檔案共用、 儲存檔案目錄或 Azure 資料表。

**適用於：** Blob、檔案、資料表

### <a name="patternfile-pattern"></a>/Pattern:"file-pattern"
指定指出哪些檔案 toocopy 檔案模式。 hello /Pattern 參數 hello 行為取決於 hello 來源資料的 hello 位置和 hello 與否 hello 遞迴模式選項。 遞迴模式可透過選項 /S 來指定。

如果 hello 指定的來源是在 hello 檔案系統中，目錄，則標準萬用字元是作用中，並提供的 hello 檔案模式比對 hello 目錄內的檔案。 如果選項指定 /S，然後 AzCopy 也會比對 hello hello 目錄下的任何子資料夾中的所有檔案對指定的模式。

如果 hello 指定的來源 blob 容器或虛擬目錄，然後不會套用萬用字元。 如果選項指定 /S，然後 AzCopy 會當做 blob 前置詞解譯 hello 指定的檔案模式。 如果選項未指定 /S，然後 AzCopy 符合 hello 檔案模式比對確切 blob 名稱。

如果來源是 Azure 的檔案共用，則您必須指定 hello 確切的檔名 (例如 abc.txt)，指定 hello toocopy 單一檔案，或指定選項 /S toocopy hello 共用以遞迴方式中的所有檔案。 正在嘗試 toospecify 這兩個檔案模式和選項 /S 一起會導致錯誤。

AzCopy 會使用區分大小寫比對時 hello /Source blob 容器或 blob 的虛擬目錄，而且會使用不區分大小寫比對所有 hello 其他情況。

hello 不指定任何檔案模式時使用的預設檔案模式是*。* ，針對「Azure 儲存體」位置，則是使用空白首碼。 不支援指定多個檔案模式。

**適用於：** Blob、檔案

### <a name="destkeystorage-key"></a>/DestKey:"storage-key"
指定 hello hello 目的地資源的儲存體帳戶金鑰。

**適用於：** Blob、檔案、資料表

### <a name="destsassas-token"></a>/DestSAS:"sas-token"
指定共用存取簽章 (SAS) hello 目的讀取及寫入權限 （如果適用）。 範圍陳述式 hello SAS 雙引號括住，因為它可能包含命令列的特殊字元。

如果 hello 目的地資源是 blob 容器、 檔案共用或資料表，您可以指定這個選項後面接著 hello SAS 權杖，或您可以指定 hello SAS 為 hello 目的地 blob 容器、 檔案共用或資料表的 URI，如果沒有這個選項的一部分。

如果 hello 來源和目的地是這兩個 blob，則 hello 目的地 blob 都必須在 hello 相同 hello 來源 blob 儲存體帳戶。

**適用於：** Blob、檔案、資料表

### <a name="sourcekeystorage-key"></a>/SourceKey:"storage-key"
指定 hello hello 來源資源的儲存體帳戶金鑰。

**適用於：** Blob、檔案、資料表

### <a name="sourcesassas-token"></a>/SourceSAS:"sas-token"
指定共用存取簽章 hello 來源的讀取和清單權限 （如果適用）。 範圍陳述式 hello SAS 雙引號括住，因為它可能包含命令列的特殊字元。

如果 hello 來源資源是 blob 容器，並提供索引鍵都 SAS，透過匿名存取讀取 hello blob 容器。

如果 hello 來源為檔案共用或資料表，必須提供的索引鍵或 SAS。

**適用於：** Blob、檔案、資料表

### <a name="s"></a>/S
指定複製作業的遞迴模式。 在遞迴模式中，AzCopy 會將複製所有的 blob 或符合 hello 指定的檔案模式，包括子資料夾中的檔案。

**適用於：** Blob、檔案

### <a name="blobtypeblock--page--append"></a>/BlobType:"block" | "page" | "append"
指定 hello 目的地 blob 是區塊 blob、 分頁 blob 或附加 blob。 此選項僅在上傳 Blob 時才適用。 否則會產生錯誤。 如果 hello 目的地是 blob，且未指定此選項，根據預設，AzCopy 會建立區塊 blob。

**適用於：** Blob

### <a name="checkmd5"></a>/CheckMD5
計算下載資料的 MD5 雜湊，並確認 hello MD5 雜湊儲存在 hello blob，或檔案的內容 MD5 屬性符合 hello 計算雜湊。 hello MD5 核取是預設關閉，所以下載資料時，您必須指定這個選項 tooperform hello MD5 核取。

請注意 Azure 儲存體，並不保證該 hello hello blob 儲存的 MD5 雜湊或是最新的檔案。 每當修改 hello blob 或檔案，它就會為用戶端的責任 tooupdate hello MD5。

AzCopy 永遠設定 hello content-md5 屬性的 Azure blob 或檔案之後將它上傳 toohello 服務。  

**適用於：** Blob、檔案

### <a name="snapshot"></a>/Snapshot
指出是否 tootransfer 快照集。 Hello 來源 blob 時，此選項才有效。

hello 傳送的 blob 快照集在重新命名此格式：.extension blob 名稱 （快照集時間）

依預設，不會複製快照。

**適用於：** Blob

### <a name="vverbose-log-file"></a>/V:[verbose-log-file]
將詳細資訊狀態訊息輸出至記錄檔。

根據預設，名為 hello 詳細的記錄檔中的 AzCopyVerbose.log `%LocalAppData%\Microsoft\Azure\AzCopy`。 如果您指定這個選項是現有的檔案位置，hello 詳細資訊記錄檔會是附加的 toothat 檔案。  

**適用於：** Blob、檔案、資料表

### <a name="zjournal-file-folder"></a>/Z:[journal-file-folder]
指定用於繼續作業的日誌檔案資料夾。

如果作業遭到中斷，AzCopy 絕對支援繼續作業。

如果未指定此選項，或指定不包含資料夾路徑，AzCopy 會建立 hello 日誌檔 hello 預設位置為 %localappdata%\microsoft\azure\azcopy 中。

每次您提交命令 tooAzCopy，它會檢查日誌檔是否存在於 hello 預設資料夾，或是否有您指定透過這個選項的資料夾中。 如果在任一處，hello 日誌檔不存在，AzCopy hello 作業視為新，並產生新的日誌檔。

如果 hello 日誌檔案存在，AzCopy 會檢查您輸入的 hello 命令列是否符合 hello hello 筆記本檔案中的命令列。 如果兩個命令列 hello 相符，AzCopy 會繼續 hello 未完成作業。 如果不相符，則提示的 tooeither 覆寫 hello 日誌檔案 toostart，新增作業或 toocancel hello 目前的作業。

hello 作業順利完成時，會刪除 hello 日誌檔案。

請注意，不支援根據舊版的 AzCopy 所建立的日誌檔案繼續作業。

**適用於：** Blob、檔案、資料表

### <a name="parameter-file"></a>/@:"parameter-file"
指定包含參數的檔案。 AzCopy 處理程序 hello hello 檔案中的參數，就如同 hello 命令列上指定。

在回應檔案中，您可以在單行中指定多個參數，或每一行各自指定一個參數。 請注意，各個參數無法橫跨多行。

回應檔案可以包含註解以 hello # 符號為開頭的行。

您可以指定多個回應檔案。 不過，請記住 AzCopy 不支援巢狀回應檔案。

**適用於：** Blob、檔案、資料表

### <a name="y"></a>/Y
隱藏所有 AzCopy 確認提示。

**適用於：** Blob、檔案、資料表

### <a name="l"></a>/L
僅指定清單作業，不會複製資料。

AzCopy 會解譯 hello 使用這個選項做執行 hello 命令列未執行此動作的模擬選項 /L 和計數會複製物件數目，您可以指定在相同時間 toocheck 哪些物件會在 hello 詳細資訊記錄檔中複製的 hello 選項 /V。

此選項 hello 行為也取決於 hello hello 來源資料的位置和 hello 遞迴模式選項 /S 和檔案模式選項 /Pattern hello 存在。

使用此選項時，AzCopy 會需要此來源位置的清單和讀取權限。

**適用於：** Blob、檔案

### <a name="mt"></a>/MT
設定 toobe 相同為 hello 來源 blob 或檔案的 hello 的 hello 下載的檔案的上次修改的時間。

**適用於：** Blob、檔案

### <a name="xn"></a>/XN
排除較新的來源資源。 hello 資源不會複製如果 hello hello 來源的上次修改的時間為 hello 相同或更新版本比目的地。

**適用於：** Blob、檔案

### <a name="xo"></a>/XO
排除較舊的來源資源。 hello 資源不會複製如果 hello hello 來源的上次修改的時間為 hello 相同或早於目的地。

**適用於：** Blob、檔案

### <a name="a"></a>/A
上傳已設定的 hello 保存屬性的檔案。

**適用於：** Blob、檔案

### <a name="iarashcnetoi"></a>/IA:[RASHCNETOI]
上傳的檔案具有任何 hello 指定屬性集。

可用屬性包括：

* R = 唯讀檔案
* A = 準備封存的檔案
* S = 系統檔案
* H = 隱藏檔案
* C = 壓縮檔案
* N = 正常檔案
* E = 加密檔案
* T = 暫存檔案
* O = 離線檔案
* I = 未編製索引的檔案

**適用於：** Blob、檔案

### <a name="xarashcnetoi"></a>/XA:[RASHCNETOI]
具有任何指定的 hello 檔案中排除屬性集。

可用屬性包括：

* R = 唯讀檔案
* A = 準備封存的檔案
* S = 系統檔案
* H = 隱藏檔案
* C = 壓縮檔案
* N = 正常檔案
* E = 加密檔案
* T = 暫存檔案
* O = 離線檔案
* I = 未編製索引的檔案

**適用於：** Blob、檔案

### <a name="delimiterdelimiter"></a>/Delimiter:"delimiter"
指出 blob 名稱中使用 toodelimit 虛擬目錄的 hello 分隔符號字元。

根據預設，AzCopy 會使用 / 為 hello 分隔符號字元。 不過，AzCopy 支援使用任何常見字元 (例如 @、# 或 %) 作為分隔符號。 如果您需要 tooinclude 其中一個 hello 命令列上的特殊字元時，括住 hello 雙引號括住的檔案名稱。

此選項僅適用於下載 Blob。

**適用於：** Blob

### <a name="ncnumber-of-concurrent-operations"></a>/NC:"number-of-concurrent-operations"
指定 hello 並行作業數。

預設的 AzCopy 會啟動特定數目的並行作業 tooincrease hello 資料傳輸輸送量。 請注意，大量的並行作業，在低頻寬的環境中可能會淹沒 hello 網路連線避免 hello 作業完全完成。 根據實際可用網路頻寬來節流處理並行作業。

hello 之並行作業的時間上限為 512。

**適用於：** Blob、檔案、資料表

### <a name="sourcetypeblob--table"></a>/SourceType:"Blob" | "Table"
指定該 hello`source`資源是 blob hello 儲存體模擬器中執行的 hello 本機開發環境中可用。

**適用於：** Blob、資料表

### <a name="desttypeblob--table"></a>/DestType:"Blob" | "Table"
指定該 hello`destination`資源是 blob hello 儲存體模擬器中執行的 hello 本機開發環境中可用。

**適用於：** Blob、資料表

### <a name="pkrskey1key2key3"></a>/PKRS:"key1#key2#key3#..."
分割 hello 資料分割索引鍵範圍 tooenable 匯出資料表資料，以平行方式，會增加 hello hello 匯出作業的速度。

如果未指定此選項，AzCopy 會使用單一執行緒 tooexport 資料表實體。 例如，如果 hello 使用者指定 /PKRS:"aa #bb"，然後 AzCopy 會啟動三個並行作業。

每個作業分別會匯出三個資料分割索引鍵範圍的其中一個，如下所示：

  [first-partition-key, aa)

  [aa, bb)

  [bb, last-partition-key]

**適用於：** 資料表

### <a name="splitsizefile-size"></a>/SplitSize:"file-size"
指定 hello 匯出的檔案分割大小 （mb），hello 允許的最小值為 32。

如果未指定此選項，AzCopy 會將匯出資料表資料 tooa 單一檔案。

如果 hello 資料表資料是匯出的 tooa blob，而且 hello 匯出的檔案的大小到達的 blob 大小的 hello 200 GB 限制，然後 AzCopy 會分割 hello 匯出的檔案，即使沒有指定這個選項。

**適用於：** 資料表

### <a name="entityoperationinsertorskip--insertormerge--insertorreplace"></a>/EntityOperation:"InsertOrSkip" | "InsertOrMerge" | "InsertOrReplace"
指定 hello 資料表資料匯入行為。

* InsertOrSkip-跳過現有的實體，或如果不存在於 hello 資料表插入新實體。
* InsertOrMerge-合併現有的實體，或如果不存在於 hello 資料表插入新實體。
* InsertOrReplace-取代現有的實體，或如果不存在於 hello 資料表插入新實體。

**適用於：** 資料表

### <a name="manifestmanifest-file"></a>/Manifest:"manifest-file"
Hello 資料表匯出和匯入作業指定 hello 資訊清單檔案。

這個選項是選擇性的 hello 匯出作業期間，AzCopy 會產生資訊清單檔與預先定義的名稱，如果沒有指定這個選項。

這是必要選項，以便將 hello 資料檔案的 hello 匯入作業期間。

**適用於：** 資料表

### <a name="synccopy"></a>/SyncCopy
指出 toosynchronously 複製 blob 或兩個 Azure 儲存體端點之間的檔案。

AzCopy 依預設會使用伺服器端的非同步複本。 指定此選項 tooperform 同步複製，這會下載 blob 或檔案 toolocal 記憶體並再將它們上傳 tooAzure 儲存體。

複製 Blob 儲存體，或從 Blob 儲存體 tooFile 儲存體，反之亦然中檔案存放裝置中的檔案時，您可以使用此選項。

**適用於：** Blob、檔案

### <a name="setcontenttypecontent-type"></a>/SetContentType:"content-type"
指定目的地 blob 或檔案的 hello MIME 內容類型。

AzCopy 集 hello blob 的內容類型，或預設檔案資料流 tooapplication/八位元。 您可以藉由明確指定這個選項的值設定 hello 的所有 blob 或檔案的內容類型。

如果您指定這個選項沒有值，AzCopy 會設定每個 blob 或根據 tooits 副檔名的檔案的內容類型。

**適用於：** Blob、檔案

### <a name="payloadformatjson--csv"></a>/PayloadFormat:"JSON" | "CSV"
指定 hello hello 資料表匯出的資料檔格式。

如果未指定此選項，根據預設，AzCopy 會匯出 JSON 格式的資料表資料檔案。

**適用於：** 資料表

## <a name="known-issues-and-best-practices"></a>已知問題和最佳作法
### <a name="limit-concurrent-writes-while-copying-data"></a>限制複製資料時的並行寫入
當您複製 blob 或利用 azcopy 進行的檔案時，請注意，另一個應用程式可能會修改 hello 資料將複製時。 可能的話，請確定不會被您要複製的 hello 資料修改 hello 複製作業期間。 比方說，當複製與 Azure 虛擬機器相關聯的 VHD，請確定沒有其他應用程式目前正在撰寫 toohello VHD。 這是預設租用 hello 資源 toobe 複製的好方法 toodo。 或者，您可以先建立 hello VHD 的快照集，然後複製 hello 快照集。

如果您不能防止其他應用程式無法寫入 tooblobs 或檔案，它們會被複製，則請記住，hello 時間 hello 作業完成時，hello 複製的資源可能不再需要完整的同位檢查，但 hello 來源資源。

### <a name="run-one-azcopy-instance-on-one-machine"></a>在一部電腦上執行一個 AzCopy 執行個體。
AzCopy 是設計的 toomaximize hello 善用您的電腦資源 tooaccelerate hello 資料傳輸，因此建議您只有一個 AzCopy 執行個體執行一個在電腦上，並指定 hello 選項`/NC`如果您需要更多的並行作業。 如需詳細資訊，請輸入`AzCopy /?:NC`在 hello 命令列。

### <a name="enable-fips-compliant-md5-algorithms-for-azcopy-when-you-use-fips-compliant-algorithms-for-encryption-hashing-and-signing"></a>當您「使用 FIPS 相容演算法於加密、雜湊及簽章」時，請為 AzCopy 啟用 FIPS 相容的 MD5 演算法。
預設的 AzCopy.NET MD5 實作 toocalculate hello MD5 複製物件，但有一些需要 AzCopy tooenable FIPS 相容 MD5 設定的安全性需求。

您可以建立具有 `AzureStorageUseV1MD5` 屬性的 app.config 檔案 `AzCopy.exe.config`，並將它放在 AzCopy.exe 旁邊。

    <?xml version="1.0" encoding="utf-8" ?>
    <configuration>
      <appSettings>
        <add key="AzureStorageUseV1MD5" value="false"/>
      </appSettings>
    </configuration>

屬性"AzureStorageUseV1MD5"• True-hello 預設值，AzCopy 會使用.NET MD5 實作。
• False – AzCopy 會使用 FIPS 相容的 MD5 演算法。

請注意 Windows 電腦預設會停用 FIPS 相容演算法，可以在您執行的視窗中輸入 secpol.msc，並在 [安全性設定] -> [本機原則] -> [安全性選項] -> [系統密碼編譯: 使用 FIPS 相容演算法於加密、雜湊及簽章] 檢查此參數。

## <a name="next-steps"></a>後續步驟
如需 Azure 儲存體和 AzCopy 的詳細資訊，請參閱下列資源的 hello:

### <a name="azure-storage-documentation"></a>Azure 儲存體文件：
* [簡介 tooAzure 儲存體](../storage-introduction.md)
* [如何 toouse 與.NET 的 Blob 儲存體](../blobs/storage-dotnet-how-to-use-blobs.md)
* [如何 toouse 檔案與.NET 的儲存體](../storage-dotnet-how-to-use-files.md)
* [如何 toouse 資料表與.NET 的儲存體](../../cosmos-db/table-storage-how-to-use-dotnet.md)
* [Toocreate，如何管理或刪除儲存體帳戶](../storage-create-storage-account.md)
* [使用 AzCopy on Linux 傳送資料](storage-use-azcopy-linux.md)

### <a name="azure-storage-blog-posts"></a>Azure 儲存體部落格文章：
* [Azure 儲存體資料移動文件庫預覽簡介](https://azure.microsoft.com/blog/introducing-azure-storage-data-movement-library-preview-2/)
* [AzCopy：簡介同步複製和自訂內容類型](http://blogs.msdn.com/b/windowsazurestorage/archive/2015/01/13/azcopy-introducing-synchronous-copy-and-customized-content-type.aspx)
* [AzCopy: 宣布正式發行 AzCopy 3.0 和具有資料表和檔案支援的 AzCopy 4.0 預覽版本](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/10/29/azcopy-announcing-general-availability-of-azcopy-3-0-plus-preview-release-of-azcopy-4-0-with-table-and-file-support.aspx)
* [AzCopy: 針對大規模複製案例最佳化](http://go.microsoft.com/fwlink/?LinkId=507682)
* [AzCopy: 支援讀取存取異地備援儲存體](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/04/07/azcopy-support-for-read-access-geo-redundant-account.aspx)
* [AzCopy: 使用可重新啟動模式和 SAS 權杖傳輸資料](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/09/07/azcopy-transfer-data-with-re-startable-mode-and-sas-token.aspx)
* [AzCopy: 使用跨帳戶複製 Blob](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/04/01/azcopy-using-cross-account-copy-blob.aspx)
* [AzCopy: 上傳/下載 Azure Blob 的檔案](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/12/03/azcopy-uploading-downloading-files-for-windows-azure-blobs.aspx)

