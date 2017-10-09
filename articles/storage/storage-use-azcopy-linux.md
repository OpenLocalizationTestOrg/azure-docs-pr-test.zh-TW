---
title: "aaaCopy 或移動資料 tooAzure 利用 azcopy 進行 Linux 上的儲存體 |Microsoft 文件"
description: "使用 hello AzCopy 上的 Linux 公用程式 toomove 或複製資料 tooor 從 blob 和檔案的內容。 複製資料 tooAzure 存放裝置從本機檔案，或複製資料內或之間的儲存體帳戶。 輕鬆地將移轉您的資料 tooAzure 儲存體。"
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
ms.date: 05/11/2017
ms.author: seguler
ms.openlocfilehash: dccb03c9e8cc3ea661494e7834f307b0e3e30cb9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="transfer-data-with-azcopy-on-linux"></a>使用 AzCopy on Linux 傳送資料
在 Linux 上的 AzCopy 是設計來複製資料 tooand 從 Microsoft Azure Blob 和檔案的儲存體使用簡單的命令，以獲得最佳效能的命令列公用程式。 儲存體帳戶內或之間的儲存體帳戶，您可以從一個物件 tooanother 複製資料。

有兩個 AzCopy 版本可供您下載。 AzCopy on Linux 內建有 .NET Core Framework，其以提供 POSIX 樣式命令列選項的 Linux 平台為目標。 [AzCopy on Windows](storage-use-azcopy.md) 內建有 .NET Framework，並且提供 Windows 樣式的命令列選項。 本文涵蓋之內容包括 AzCopy on Linux。

## <a name="download-and-install-azcopy"></a>下載並安裝 AzCopy
### <a name="installation-on-linux"></a>在 Linux 上安裝

在 Linux 上的 AzCopy 需要 hello 平台上的.NET Core framework。 請參閱 hello hello 安裝指示[.NET Core](https://www.microsoft.com/net/core#linuxubuntu)頁面。

例如，讓我們在 Ubuntu 16.10 上安裝 .NET Core。 Hello 最新的安裝指南，請瀏覽[Linux 上的.NET Core](https://www.microsoft.com/net/core#linuxubuntu)安裝 頁面。


```bash
sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ yakkety main" > /etc/apt/sources.list.d/dotnetdev.list' 
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893
sudo apt-get update
sudo apt-get install dotnet-dev-1.0.3
```

安裝 .NET Core 之後，下載並安裝 AzCopy。

```bash
wget -O azcopy.tar.gz https://aka.ms/downloadazcopyprlinux
tar -xf azcopy.tar.gz
sudo ./install.sh
```

在 Linux 上的 AzCopy 會安裝之後，您可以移除 hello 擷取檔案。 或者如果您沒有 superuser 權限，您也可以執行使用 hello 殼層指令碼的 AzCopy 'azcopy' hello 解壓縮的資料夾中。 

### <a name="alternative-installation-on-ubuntu"></a>Ubuntu 上的替代安裝

**Ubuntu 14.04**

新增適用於 .Net Core 的 apt 來源：

```bash
sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ trusty main" > /etc/apt/sources.list.d/dotnetdev.list' 
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893
```

新增適用於 Microsoft Linux 產品存放庫的 apt 來源並安裝 AzCopy：

```bash
curl https://packages.microsoft.com/config/ubuntu/14.04/prod.list > ./microsoft-prod.list
sudo cp ./microsoft-prod.list /etc/apt/sources.list.d/
curl https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > microsoft.gpg
sudo cp ./microsoft.gpg /etc/apt/trusted.gpg.d/
```

```bash
sudo apt-get update
sudo apt-get install azcopy
```

**Ubuntu 16.04**

新增適用於 .Net Core 的 apt 來源：

```bash
sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ xenial main" > /etc/apt/sources.list.d/dotnetdev.list' 
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893
```

新增適用於 Microsoft Linux 產品存放庫的 apt 來源並安裝 AzCopy：

```bash
curl https://packages.microsoft.com/config/ubuntu/16.04/prod.list > ./microsoft-prod.list
sudo cp ./microsoft-prod.list /etc/apt/sources.list.d/
curl https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > microsoft.gpg
sudo cp ./microsoft.gpg /etc/apt/trusted.gpg.d/
```

```bash
sudo apt-get update
sudo apt-get install azcopy
```

**Ubuntu 16.10**

新增適用於 .Net Core 的 apt 來源：

```bash
sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ yakkety main" > /etc/apt/sources.list.d/dotnetdev.list' 
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893
```

新增適用於 Microsoft Linux 產品存放庫的 apt 來源並安裝 AzCopy：

```bash
curl https://packages.microsoft.com/config/ubuntu/16.10/prod.list > ./microsoft-prod.list
sudo cp ./microsoft-prod.list /etc/apt/sources.list.d/
curl https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > microsoft.gpg
sudo cp ./microsoft.gpg /etc/apt/trusted.gpg.d/
```

```bash
sudo apt-get update
sudo apt-get install azcopy
```

## <a name="writing-your-first-azcopy-command"></a>撰寫第一個 AzCopy 命令
hello 的 AzCopy 命令的基本語法如下：

```azcopy
azcopy --source <source> --destination <destination> [Options]
```

hello 遵循範例示範如何從 Microsoft Azure Blob 和檔案複製資料 tooand 的各種案例。 請參閱 toohello`azcopy --help`功能表 hello 參數，每個範例中所使用的詳細說明。

## <a name="blob-download"></a>Blob：下載
### <a name="download-single-blob"></a>下載單一 Blob

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --include "abc.txt"
```

如果 hello 資料夾`/mnt/myfiles`不存在，AzCopy 會加以建立，並下載`abc.txt `hello 新資料夾。

### <a name="download-single-blob-from-secondary-region"></a>從次要地區下載單一 Blob

```azcopy
azcopy \
    --source https://myaccount-secondary.blob.core.windows.net/mynewcontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --include "abc.txt"
```

請注意，您必須啟用讀取權限異地備援儲存體。

### <a name="download-all-blobs"></a>下載所有 Blob

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --recursive
```

假設下列 hello 位於 hello 指定容器的 blob:  

```
abc.txt
abc1.txt
abc2.txt
vd1/a.txt
vd1/abcd.txt
```

Hello 下載作業之後，hello 目錄`/mnt/myfiles`包含下列檔案的 hello:

```
/mnt/myfiles/abc.txt
/mnt/myfiles/abc1.txt
/mnt/myfiles/abc2.txt
/mnt/myfiles/vd1/a.txt
/mnt/myfiles/vd1/abcd.txt
```

如果您未指定選項 `--recursive`，則不會下載任何 Blob。

### <a name="download-blobs-with-specified-prefix"></a>下載具有指定首碼的 Blob

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --include "a" \
    --recursive
```

假設 hello 下列 blob 位於 hello 指定的容器。 以 hello 前置詞開頭的所有 blob`a`下載。

```
abc.txt
abc1.txt
abc2.txt
xyz.txt
vd1\a.txt
vd1\abcd.txt
```

Hello 下載作業之後，hello 資料夾`/mnt/myfiles`包含下列檔案的 hello:

```
/mnt/myfiles/abc.txt
/mnt/myfiles/abc1.txt
/mnt/myfiles/abc2.txt
```

hello 前置詞會套用 toohello 虛擬目錄，可形成 hello hello blob 名稱第一個部分。 Hello 虛擬目錄在 hello 上述範例中，它不符合 hello 指定之前置詞，因此沒有 blob 下載。 此外，如果 hello 選項`--recursive`未指定，AzCopy 不會下載任何 blob。

### <a name="set-hello-last-modified-time-of-exported-files-toobe-same-as-hello-source-blobs"></a>設定 hello toobe 匯出的檔案的上次修改時間與 hello 來源 blob 相同

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination "/mnt/myfiles" \
    --source-key <key> \
    --preserve-last-modified-time
```

您也可以從其上次修改時間為基礎的 hello 下載作業排除的 blob。 例如，如果您想 tooexclude blob 的上次修改的時間為 hello 相同或較 hello 目的地檔案，加入 hello`--exclude-newer`選項：

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --preserve-last-modified-time \
    --exclude-newer
```

如果您想 tooexclude blob 的上次修改的時間為 hello 相同或比 hello 目的地檔案還舊，新增 hello 或`--exclude-older`選項：

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --preserve-last-modified-time \
    --exclude-older
```

## <a name="blob-upload"></a>Blob：上傳
### <a name="upload-single-file"></a>上傳單一檔案

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --include "abc.txt"
```

如果 hello 指定的目的地容器不存在，AzCopy 建立及上傳 hello 到其中的檔案。

### <a name="upload-single-file-toovirtual-directory"></a>單一檔案上傳 toovirtual 目錄

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --include "abc.txt"
```

如果 hello 指定虛擬目錄不存在，AzCopy 上傳 hello 檔案 tooinclude hello 中的虛擬目錄 hello blob 名稱 (*例如*， `vd/abc.txt` hello 上述範例中)。

### <a name="upload-all-files"></a>上傳所有檔案

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --recursive
```

指定選項`--recursive`hello 上傳 hello 內容所指定目錄 tooBlob 儲存體以遞迴方式，這表示所有子資料夾及檔案會上傳以及。 比方說，假設 hello 下列檔案位於資料夾`/mnt/myfiles`:

```
/mnt/myfiles/abc.txt
/mnt/myfiles/abc1.txt
/mnt/myfiles/abc2.txt
/mnt/myfiles/subfolder/a.txt
/mnt/myfiles/subfolder/abcd.txt
```

Hello 上傳作業之後，hello 容器會包含下列檔案的 hello:

```
abc.txt
abc1.txt
abc2.txt
subfolder/a.txt
subfolder/abcd.txt
```

當 hello 選項`--recursive`未指定，只有 hello 下列三個檔案上傳：

```
abc.txt
abc1.txt
abc2.txt
```

### <a name="upload-files-matching-specified-pattern"></a>上傳符合指定模式的檔案

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --include "a*" \
    --recursive
```

假設 hello 下列檔案位於資料夾`/mnt/myfiles`:

```
/mnt/myfiles/abc.txt
/mnt/myfiles/abc1.txt
/mnt/myfiles/abc2.txt
/mnt/myfiles/xyz.txt
/mnt/myfiles/subfolder/a.txt
/mnt/myfiles/subfolder/abcd.txt
```

Hello 上傳作業之後，hello 容器會包含下列檔案的 hello:

```
abc.txt
abc1.txt
abc2.txt
subfolder/a.txt
subfolder/abcd.txt
```

當 hello 選項`--recursive`未指定，AzCopy 會略過在子目錄中的檔案：

```
abc.txt
abc1.txt
abc2.txt
```

### <a name="specify-hello-mime-content-type-of-a-destination-blob"></a>指定目的地 blob hello MIME 內容的類型
根據預設，AzCopy 設定 hello 的目的地 blob 的內容型別太`application/octet-stream`。 不過，您可以明確指定 hello 透過 hello 選項的內容類型`--set-content-type [content-type]`。 此語法中上傳作業設定 hello 的所有 blob 的內容類型。

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/myContainer/ \
    --dest-key <key> \
    --include "ab" \
    --set-content-type "video/mp4"
```

如果 hello 選項`--set-content-type`AzCopy 會將每個 blob 或檔案，但沒有值，指定的內容類型，根據 tooits 副檔名。

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/myContainer/ \
    --dest-key <key> \
    --include "ab" \
    --set-content-type
```

## <a name="blob-copy"></a>Blob：複製
### <a name="copy-single-blob-within-storage-account"></a>複製儲存體帳戶內的單一 Blob

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer1 \
    --destination https://myaccount.blob.core.windows.net/mycontainer2 \
    --source-key <key> \
    --dest-key <key> \
    --include "abc.txt"
```

當您未以 --sync-copy 選項複製 Blob 時，系統會執行[伺服器端複製](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) \(英文\) 作業。

### <a name="copy-single-blob-across-storage-accounts"></a>跨儲存體帳戶複製單一 Blob

```azcopy
azcopy \
    --source https://sourceaccount.blob.core.windows.net/mycontainer1 \
    --destination https://destaccount.blob.core.windows.net/mycontainer2 \
    --source-key <key1> \
    --dest-key <key2> \
    --include "abc.txt"
```

當您未以 --sync-copy 選項複製 Blob 時，系統會執行[伺服器端複製](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) \(英文\) 作業。

### <a name="copy-single-blob-from-secondary-region-tooprimary-region"></a>從次要區域 tooprimary 區域複製單一 blob

```azcopy
azcopy \
    --source https://myaccount1-secondary.blob.core.windows.net/mynewcontainer1 \
    --destination https://myaccount2.blob.core.windows.net/mynewcontainer2 \
    --source-key <key1> \
    --dest-key <key2> \
    --include "abc.txt"
```

請注意，您必須啟用讀取權限異地備援儲存體。

### <a name="copy-single-blob-and-its-snapshots-across-storage-accounts"></a>跨儲存體帳戶複製單一 Blob 及其快照

```azcopy
azcopy \
    --source https://sourceaccount.blob.core.windows.net/mycontainer1 \
    --destination https://destaccount.blob.core.windows.net/mycontainer2 \
    --source-key <key1> \
    --dest-key <key2> \
    --include "abc.txt" \
    --include-snapshot
```

Hello 複製作業之後，hello 目標容器包含 hello blob 和其快照集。 hello 容器包含 hello 下列 blob 和其快照集：

```
abc.txt
abc (2013-02-25 080757).txt
abc (2014-02-21 150331).txt
```

### <a name="synchronously-copy-blobs-across-storage-accounts"></a>以同步方式跨儲存體帳戶複製 Blob
根據預設，AzCopy 會以非同步方式在兩個儲存體端點之間複製資料。 因此，複製 hello 背景使用的備用頻寬容量且沒有 SLA 方面的速度有多快 blob 中的 hello 複製作業執行。 

hello`--sync-copy`選項可確保 hello 複製作業取得一致的速度。 AzCopy 下載 hello blob 執行 hello 同步複本 toocopy hello 從指定來源 toolocal 記憶體，並再將其上傳 toohello Blob 儲存體目的地。

```azcopy
azcopy \
    --source https://myaccount1.blob.core.windows.net/myContainer/ \
    --destination https://myaccount2.blob.core.windows.net/myContainer/ \
    --source-key <key1> \
    --dest-key <key2> \
    --include "ab" \
    --sync-copy
```

`--sync-copy`可能會產生額外的輸出成本比較 tooasynchronous 複製。 hello 建議的方法是 toouse 處於 hello Azure VM 中的這個選項與您來源儲存體帳戶 tooavoid 出口成本相同的區域。

## <a name="file-download"></a>檔案：下載
### <a name="download-single-file"></a>下載單一檔案

```azcopy
azcopy \
    --source https://myaccount.file.core.windows.net/myfileshare/myfolder1/ \
    --destination /mnt/myfiles \
    --source-key <key> \
    --include "abc.txt"
```

如果 hello 指定來源是 Azure 的檔案共用，則您必須指定 hello 確切的檔名，(*例如* `abc.txt`) toodownload 單一檔案，或指定選項`--recursive`toodownload 所有檔案在 hello 共用以遞迴方式。 檔案模式和選項，嘗試 toospecify`--recursive`一起會產生錯誤。

### <a name="download-all-files"></a>下載所有檔案

```azcopy
azcopy \
    --source https://myaccount.file.core.windows.net/myfileshare/ \
    --destination /mnt/myfiles \
    --source-key <key> \
    --recursive
```

請注意，並不會下載任何空白資料夾。

## <a name="file-upload"></a>檔案：上傳
### <a name="upload-single-file"></a>上傳單一檔案

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.file.core.windows.net/myfileshare/ \
    --dest-key <key> \
    --include abc.txt
```

### <a name="upload-all-files"></a>上傳所有檔案

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.file.core.windows.net/myfileshare/ \
    --dest-key <key> \
    --recursive
```

請注意，並不會上傳任何空白資料夾。

### <a name="upload-files-matching-specified-pattern"></a>上傳符合指定模式的檔案

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.file.core.windows.net/myfileshare/ \
    --dest-key <key> \
    --include "ab*" \
    --recursive
```

## <a name="file-copy"></a>檔案：複製
### <a name="copy-across-file-shares"></a>跨檔案共用複製

```azcopy
azcopy \
    --source https://myaccount1.file.core.windows.net/myfileshare1/ \
    --destination https://myaccount2.file.core.windows.net/myfileshare2/ \
    --source-key <key1> \
    --dest-key <key2> \
    --recursive
```
當您跨檔案共用複製檔案時，系統會執行[伺服器端複製](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx)作業。

### <a name="copy-from-file-share-tooblob"></a>從檔案共用 tooblob 複製

```azcopy
azcopy \ 
    --source https://myaccount1.file.core.windows.net/myfileshare/ \
    --destination https://myaccount2.blob.core.windows.net/mycontainer/ \
    --source-key <key1> \
    --dest-key <key2> \
    --recursive
```
當您複製檔案從檔案共用 tooblob，[伺服器端副本](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx)執行作業。

### <a name="copy-from-blob-toofile-share"></a>複製 blob toofile 共用

```azcopy
azcopy \
    --source https://myaccount1.blob.core.windows.net/mycontainer/ \
    --destination https://myaccount2.file.core.windows.net/myfileshare/ \
    --source-key <key1> \
    --dest-key <key2> \
    --recursive
```
當您複製檔案從 blob toofile 共用，[伺服器端副本](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx)執行作業。

### <a name="synchronously-copy-files"></a>以同步方式複製檔案
您可以指定 hello`--sync-copy`同步選項 toocopy 資料從檔案儲存體 tooFile 存放裝置、 檔案儲存體 tooBlob 儲存體和 Blob 儲存體 tooFile 儲存體。 AzCopy 會藉由下載 hello 來源資料 toolocal 記憶體，然後將它上傳 toodestination 執行此作業。 在此情況下，會產生標準輸出成本。

```azcopy
azcopy \
    --source https://myaccount1.file.core.windows.net/myfileshare1/ \
    --destination https://myaccount2.file.core.windows.net/myfileshare2/ \
    --source-key <key1> \
    --dest-key <key2> \
    --recursive \
    --sync-copy
```

當複製檔案的儲存體 tooBlob 儲存體，hello 預設 blob 型別是區塊 blob，使用者可以指定選項`/BlobType:page`toochange hello 目的地 blob 類型。

請注意，`--sync-copy`可能會產生額外成本比較 tooasynchronous 複製的輸出。 hello 建議的方法是 toouse 處於 hello Azure VM 中的這個選項與您來源儲存體帳戶 tooavoid 出口成本相同的區域。

## <a name="other-azcopy-features"></a>其他 AzCopy 功能
### <a name="only-copy-data-that-doesnt-exist-in-hello-destination"></a>只複製 hello 目的地中不存在的資料
hello`--exclude-older`和`--exclude-newer`參數可讓您從要複製，分別 tooexclude 更舊或更新的來源資源。 如果您只想 toocopy 來源資源不存在於 hello 目的地中，您可以在 hello AzCopy 命令中指定這兩個參數：

    --source http://myaccount.blob.core.windows.net/mycontainer --destination /mnt/myfiles --source-key <sourcekey> --recursive --exclude-older --exclude-newer

    --source /mnt/myfiles --destination http://myaccount.file.core.windows.net/myfileshare --dest-key <destkey> --recursive --exclude-older --exclude-newer

    --source http://myaccount.blob.core.windows.net/mycontainer --destination http://myaccount.blob.core.windows.net/mycontainer1 --source-key <sourcekey> --dest-key <destkey> --recursive --exclude-older --exclude-newer

### <a name="use-a-configuration-file-toospecify-command-line-parameters"></a>使用組態檔 toospecify 命令列參數

```azcopy
azcopy --config-file "azcopy-config.ini"
```

您可以在組態檔中包含任何 AzCopy 命令列參數。 AzCopy 處理程序 hello hello 檔案中的參數，如同它們已執行 hello 檔案直接替代與 hello 內容的 hello 命令列上指定。

假設名為組態檔`copyoperation`，其中包含下列行 hello。 每個 AzCopy 參數可以指定在同一行。

    --source http://myaccount.blob.core.windows.net/mycontainer --destination /mnt/myfiles --source-key <sourcekey> --recursive --quiet

或不同行：

    --source http://myaccount.blob.core.windows.net/mycontainer
    --destination /mnt/myfiles
    --source-key<sourcekey>
    --recursive
    --quiet

AzCopy 失敗如果 hello 參數分成兩行，如下所示為 hello`--source-key`參數：

    http://myaccount.blob.core.windows.net/mycontainer
    /mnt/myfiles
    --sourcekey
    <sourcekey>
    --recursive
    --quiet

### <a name="specify-a-shared-access-signature-sas"></a>指定共用存取簽章 (SAS)

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer1 \
    --destination https://myaccount.blob.core.windows.net/mycontainer2 \
    --source-sas <SAS1> \
    --dest-sas <SAS2> \
    --include abc.txt
```

您也可以指定 SAS hello 容器 URI 上：

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer1/?SourceSASToken \
    --destination /mnt/myfiles \
    --recursive
```

請注意，AzCopy 目前僅支援 hello[帳戶 SAS](https://docs.microsoft.com/en-us/azure/storage/storage-dotnet-shared-access-signature-part-1)。

### <a name="journal-file-folder"></a>日誌檔案資料夾
每次您提交命令 tooAzCopy，它會檢查日誌檔是否存在於 hello 預設資料夾，或是否有您指定透過這個選項的資料夾中。 如果在任一處，hello 日誌檔不存在，AzCopy hello 作業視為新，並產生新的日誌檔。

如果 hello 日誌檔案存在，AzCopy 會檢查您輸入的 hello 命令列是否符合 hello hello 筆記本檔案中的命令列。 如果兩個命令列 hello 相符，AzCopy 會繼續 hello 未完成作業。 如果不相符，AzCopy 會提示使用者 tooeither 覆寫 hello 日誌檔案 toostart，新增作業或 toocancel hello 目前的作業。

如果您想 hello 日誌檔 toouse hello 預設位置：

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --resume
```

如果您省略選項`--resume`，或指定選項`--resume`未 hello 資料夾路徑，如上所示，AzCopy 會建立 hello 日誌檔 hello 預設位置，也就是在`~\Microsoft\Azure\AzCopy`。 如果 hello 日誌檔已經存在，然後 AzCopy 會繼續 hello hello 日誌檔為基礎的作業。

如果您想 toospecify hello 日誌檔的自訂位置：

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key key \
    --resume "/mnt/myjournal"
```

如果不存在，此範例會建立 hello 日誌檔。 如果檔案存在，然後 AzCopy 會繼續依據 hello 日誌檔的 hello 作業。

如果您想 tooresume AzCopy 作業時，重複 hello 相同的命令。 然後 AzCopy on Linux 會提示您確認：

```azcopy
Incomplete operation with same command line detected at hello journal directory "/home/myaccount/Microsoft/Azure/AzCopy", do you want tooresume hello operation? Choose Yes tooresume, choose No toooverwrite hello journal toostart a new operation. (Yes/No)
```

### <a name="output-verbose-logs"></a>輸出詳細資訊記錄檔

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --verbose
```

### <a name="specify-hello-number-of-concurrent-operations-toostart"></a>指定的並行作業 toostart hello
選項`--parallel-level`指定 hello 並行的複製作業數目。 根據預設，AzCopy 會啟動特定數目的並行作業 tooincrease hello 資料傳輸輸送量。 並行作業的 hello 數目等於八次 hello 您擁有的處理器數目。 如果您正在執行 AzCopy 透過低頻寬網路，您可以指定較低的數字-平行層級 tooavoid 失敗的資源競爭所造成。

[!TIP]
>tooview hello 完整清單的 AzCopy 參數，請查看 'azcopy-說明' 功能表。

## <a name="known-issues-and-best-practices"></a>已知問題和最佳作法
### <a name="error-net-core-is-not-found-in-hello-system"></a>錯誤： Hello 系統中找不到.NET Core。
如果您遇到錯誤，指出 hello 系統中未安裝的.NET Core，hello 路徑 toohello.NET Core 二進位`dotnet`可能會遺失。

在順序 tooaddress 此問題，尋找 hello 系統中的 hello.NET Core 二進位檔：
```bash
sudo find / -name dotnet
```

這會傳回 hello 路徑 toohello dotnet 二進位。 

    /opt/rh/rh-dotnetcore11/root/usr/bin/dotnet
    /opt/rh/rh-dotnetcore11/root/usr/lib64/dotnetcore/dotnet
    /opt/rh/rh-dotnetcore11/root/usr/lib64/dotnetcore/shared/Microsoft.NETCore.App/1.1.2/dotnet

現在加入此路徑 toohello 路徑變數。 Sudo，編輯 secure_path toocontain hello 路徑 toohello dotnet 二進位：
```bash 
sudo visudo
### Append hello path found in hello preceding example too'secure_path' variable
```

在此範例中，secure_path 變數會顯示為：

```
secure_path = /sbin:/bin:/usr/sbin:/usr/bin:/opt/rh/rh-dotnetcore11/root/usr/bin/
```

Hello 目前的使用者編輯.bash_profile/.profile tooinclude hello 路徑 toohello dotnet 二進位 PATH 變數中 
```bash
vi ~/.bash_profile
### Append hello path found in hello preceding example too'PATH' variable
```

確認 .NET Core 現在位於 PATH 中：
```bash
which dotnet
sudo which dotnet
```

### <a name="error-installing-azcopy"></a>安裝 AzCopy 時發生錯誤
如果您遇到的 AzCopy 安裝問題，您可以嘗試的 toorun AzCopy hello 中使用 hello bash 指令碼擷取`azcopy`資料夾。

```bash
cd azcopy
./azcopy
```

### <a name="limit-concurrent-writes-while-copying-data"></a>限制複製資料時的並行寫入
當您複製 blob 或利用 azcopy 進行的檔案時，請注意，另一個應用程式可能會修改 hello 資料將複製時。 可能的話，請確定不會被您要複製的 hello 資料修改 hello 複製作業期間。 比方說，當複製與 Azure 虛擬機器相關聯的 VHD，請確定沒有其他應用程式目前正在撰寫 toohello VHD。 這是預設租用 hello 資源 toobe 複製的好方法 toodo。 或者，您可以先建立 hello VHD 的快照集，然後複製 hello 快照集。

如果您不能防止其他應用程式無法寫入 tooblobs 或檔案，它們會被複製，則請記住，hello 時間 hello 作業完成時，hello 複製的資源可能不再需要完整的同位檢查，但 hello 來源資源。

### <a name="run-one-azcopy-instance-on-one-machine"></a>在一部電腦上執行一個 AzCopy 執行個體。
AzCopy 是設計的 toomaximize hello 善用您的電腦資源 tooaccelerate hello 資料傳輸，因此建議您只有一個 AzCopy 執行個體執行一個在電腦上，並指定 hello 選項`--parallel-level`如果您需要更多的並行作業。 如需詳細資訊，請輸入`AzCopy --help parallel-level`在 hello 命令列。

## <a name="next-steps"></a>後續步驟
如需 Azure 儲存體和 AzCopy 的詳細資訊，請參閱下列資源的 hello:

### <a name="azure-storage-documentation"></a>Azure 儲存體文件：
* [簡介 tooAzure 儲存體](storage-introduction.md)
* [建立儲存體帳戶](storage-create-storage-account.md)
* [使用儲存體總管來管理 Blob](https://docs.microsoft.com/en-us/azure/vs-azure-tools-storage-explorer-blobs) \(英文\)
* [使用 Azure CLI 2.0 hello 與 Azure 儲存體](storage-azure-cli.md)
* [如何 toouse 從 c + + 的 Blob 儲存體](storage-c-plus-plus-how-to-use-blobs.md)
* [如何從 Java 的 Blob 儲存體 toouse](storage-java-how-to-use-blob-storage.md)
* [如何 toouse Node.js 從 Blob 儲存體](storage-nodejs-how-to-use-blob-storage.md)
* [如何 toouse 來自 Python 的 Blob 儲存體](storage-python-how-to-use-blob-storage.md)

### <a name="azure-storage-blog-posts"></a>Azure 儲存體部落格文章：
* [宣告 AzCopy on Linux 預覽](https://azure.microsoft.com/en-in/blog/announcing-azcopy-on-linux-preview/) \(英文\)
* [Azure 儲存體資料移動文件庫預覽簡介](https://azure.microsoft.com/blog/introducing-azure-storage-data-movement-library-preview-2/)
* [AzCopy：簡介同步複製和自訂內容類型](http://blogs.msdn.com/b/windowsazurestorage/archive/2015/01/13/azcopy-introducing-synchronous-copy-and-customized-content-type.aspx)
* [AzCopy: 宣布正式發行 AzCopy 3.0 和具有資料表和檔案支援的 AzCopy 4.0 預覽版本](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/10/29/azcopy-announcing-general-availability-of-azcopy-3-0-plus-preview-release-of-azcopy-4-0-with-table-and-file-support.aspx)
* [AzCopy: 針對大規模複製案例最佳化](http://go.microsoft.com/fwlink/?LinkId=507682)
* [AzCopy: 支援讀取存取異地備援儲存體](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/04/07/azcopy-support-for-read-access-geo-redundant-account.aspx)
* [AzCopy：使用可重新啟動模式和 SAS 權杖傳輸資料](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/09/07/azcopy-transfer-data-with-re-startable-mode-and-sas-token.aspx) \(英文\)
* [AzCopy: 使用跨帳戶複製 Blob](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/04/01/azcopy-using-cross-account-copy-blob.aspx)
* [AzCopy: 上傳/下載 Azure Blob 的檔案](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/12/03/azcopy-uploading-downloading-files-for-windows-azure-blobs.aspx)

