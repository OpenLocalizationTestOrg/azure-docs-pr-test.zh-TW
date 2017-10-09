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
# <a name="transfer-data-with-azcopy-on-linux"></a><span data-ttu-id="7b347-105">使用 AzCopy on Linux 傳送資料</span><span class="sxs-lookup"><span data-stu-id="7b347-105">Transfer data with AzCopy on Linux</span></span>
<span data-ttu-id="7b347-106">在 Linux 上的 AzCopy 是設計來複製資料 tooand 從 Microsoft Azure Blob 和檔案的儲存體使用簡單的命令，以獲得最佳效能的命令列公用程式。</span><span class="sxs-lookup"><span data-stu-id="7b347-106">AzCopy on Linux is a command-line utility designed for copying data tooand from Microsoft Azure Blob and File storage using simple commands with optimal performance.</span></span> <span data-ttu-id="7b347-107">儲存體帳戶內或之間的儲存體帳戶，您可以從一個物件 tooanother 複製資料。</span><span class="sxs-lookup"><span data-stu-id="7b347-107">You can copy data from one object tooanother within your storage account, or between storage accounts.</span></span>

<span data-ttu-id="7b347-108">有兩個 AzCopy 版本可供您下載。</span><span class="sxs-lookup"><span data-stu-id="7b347-108">There are two versions of AzCopy that you can download.</span></span> <span data-ttu-id="7b347-109">AzCopy on Linux 內建有 .NET Core Framework，其以提供 POSIX 樣式命令列選項的 Linux 平台為目標。</span><span class="sxs-lookup"><span data-stu-id="7b347-109">AzCopy on Linux is built with .NET Core Framework, which targets Linux platforms offering POSIX style command-line options.</span></span> <span data-ttu-id="7b347-110">[AzCopy on Windows](storage-use-azcopy.md) 內建有 .NET Framework，並且提供 Windows 樣式的命令列選項。</span><span class="sxs-lookup"><span data-stu-id="7b347-110">[AzCopy on Windows](storage-use-azcopy.md) is built with .NET Framework, and offers Windows style command-line options.</span></span> <span data-ttu-id="7b347-111">本文涵蓋之內容包括 AzCopy on Linux。</span><span class="sxs-lookup"><span data-stu-id="7b347-111">This article covers AzCopy on Linux.</span></span>

## <a name="download-and-install-azcopy"></a><span data-ttu-id="7b347-112">下載並安裝 AzCopy</span><span class="sxs-lookup"><span data-stu-id="7b347-112">Download and install AzCopy</span></span>
### <a name="installation-on-linux"></a><span data-ttu-id="7b347-113">在 Linux 上安裝</span><span class="sxs-lookup"><span data-stu-id="7b347-113">Installation on Linux</span></span>

<span data-ttu-id="7b347-114">在 Linux 上的 AzCopy 需要 hello 平台上的.NET Core framework。</span><span class="sxs-lookup"><span data-stu-id="7b347-114">AzCopy on Linux requires .NET Core framework on hello platform.</span></span> <span data-ttu-id="7b347-115">請參閱 hello hello 安裝指示[.NET Core](https://www.microsoft.com/net/core#linuxubuntu)頁面。</span><span class="sxs-lookup"><span data-stu-id="7b347-115">See hello installation instructions on hello [.NET Core](https://www.microsoft.com/net/core#linuxubuntu) page.</span></span>

<span data-ttu-id="7b347-116">例如，讓我們在 Ubuntu 16.10 上安裝 .NET Core。</span><span class="sxs-lookup"><span data-stu-id="7b347-116">As an example, let's install .NET Core on Ubuntu 16.10.</span></span> <span data-ttu-id="7b347-117">Hello 最新的安裝指南，請瀏覽[Linux 上的.NET Core](https://www.microsoft.com/net/core#linuxubuntu)安裝 頁面。</span><span class="sxs-lookup"><span data-stu-id="7b347-117">For hello latest installation guide, visit [.NET Core on Linux](https://www.microsoft.com/net/core#linuxubuntu) installation page.</span></span>


```bash
sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ yakkety main" > /etc/apt/sources.list.d/dotnetdev.list' 
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893
sudo apt-get update
sudo apt-get install dotnet-dev-1.0.3
```

<span data-ttu-id="7b347-118">安裝 .NET Core 之後，下載並安裝 AzCopy。</span><span class="sxs-lookup"><span data-stu-id="7b347-118">Once you have installed .NET Core, download and install AzCopy.</span></span>

```bash
wget -O azcopy.tar.gz https://aka.ms/downloadazcopyprlinux
tar -xf azcopy.tar.gz
sudo ./install.sh
```

<span data-ttu-id="7b347-119">在 Linux 上的 AzCopy 會安裝之後，您可以移除 hello 擷取檔案。</span><span class="sxs-lookup"><span data-stu-id="7b347-119">You can remove hello extracted files once AzCopy on Linux is installed.</span></span> <span data-ttu-id="7b347-120">或者如果您沒有 superuser 權限，您也可以執行使用 hello 殼層指令碼的 AzCopy 'azcopy' hello 解壓縮的資料夾中。</span><span class="sxs-lookup"><span data-stu-id="7b347-120">Alternatively if you do not have superuser privileges, you can also run AzCopy using hello shell script 'azcopy' in hello extracted folder.</span></span> 

### <a name="alternative-installation-on-ubuntu"></a><span data-ttu-id="7b347-121">Ubuntu 上的替代安裝</span><span class="sxs-lookup"><span data-stu-id="7b347-121">Alternative Installation on Ubuntu</span></span>

<span data-ttu-id="7b347-122">**Ubuntu 14.04**</span><span class="sxs-lookup"><span data-stu-id="7b347-122">**Ubuntu 14.04**</span></span>

<span data-ttu-id="7b347-123">新增適用於 .Net Core 的 apt 來源：</span><span class="sxs-lookup"><span data-stu-id="7b347-123">Add apt source for .Net Core:</span></span>

```bash
sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ trusty main" > /etc/apt/sources.list.d/dotnetdev.list' 
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893
```

<span data-ttu-id="7b347-124">新增適用於 Microsoft Linux 產品存放庫的 apt 來源並安裝 AzCopy：</span><span class="sxs-lookup"><span data-stu-id="7b347-124">Add apt source for Microsoft Linux product repository and install AzCopy:</span></span>

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

<span data-ttu-id="7b347-125">**Ubuntu 16.04**</span><span class="sxs-lookup"><span data-stu-id="7b347-125">**Ubuntu 16.04**</span></span>

<span data-ttu-id="7b347-126">新增適用於 .Net Core 的 apt 來源：</span><span class="sxs-lookup"><span data-stu-id="7b347-126">Add apt source for .Net Core:</span></span>

```bash
sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ xenial main" > /etc/apt/sources.list.d/dotnetdev.list' 
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893
```

<span data-ttu-id="7b347-127">新增適用於 Microsoft Linux 產品存放庫的 apt 來源並安裝 AzCopy：</span><span class="sxs-lookup"><span data-stu-id="7b347-127">Add apt source for Microsoft Linux product repository and install AzCopy:</span></span>

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

<span data-ttu-id="7b347-128">**Ubuntu 16.10**</span><span class="sxs-lookup"><span data-stu-id="7b347-128">**Ubuntu 16.10**</span></span>

<span data-ttu-id="7b347-129">新增適用於 .Net Core 的 apt 來源：</span><span class="sxs-lookup"><span data-stu-id="7b347-129">Add apt source for .Net Core:</span></span>

```bash
sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ yakkety main" > /etc/apt/sources.list.d/dotnetdev.list' 
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893
```

<span data-ttu-id="7b347-130">新增適用於 Microsoft Linux 產品存放庫的 apt 來源並安裝 AzCopy：</span><span class="sxs-lookup"><span data-stu-id="7b347-130">Add apt source for Microsoft Linux product repository and install AzCopy:</span></span>

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

## <a name="writing-your-first-azcopy-command"></a><span data-ttu-id="7b347-131">撰寫第一個 AzCopy 命令</span><span class="sxs-lookup"><span data-stu-id="7b347-131">Writing your first AzCopy command</span></span>
<span data-ttu-id="7b347-132">hello 的 AzCopy 命令的基本語法如下：</span><span class="sxs-lookup"><span data-stu-id="7b347-132">hello basic syntax for AzCopy commands is:</span></span>

```azcopy
azcopy --source <source> --destination <destination> [Options]
```

<span data-ttu-id="7b347-133">hello 遵循範例示範如何從 Microsoft Azure Blob 和檔案複製資料 tooand 的各種案例。</span><span class="sxs-lookup"><span data-stu-id="7b347-133">hello following examples demonstrate various scenarios for copying data tooand from Microsoft Azure Blobs and Files.</span></span> <span data-ttu-id="7b347-134">請參閱 toohello`azcopy --help`功能表 hello 參數，每個範例中所使用的詳細說明。</span><span class="sxs-lookup"><span data-stu-id="7b347-134">Refer toohello `azcopy --help` menu for a detailed explanation of hello parameters used in each sample.</span></span>

## <a name="blob-download"></a><span data-ttu-id="7b347-135">Blob：下載</span><span class="sxs-lookup"><span data-stu-id="7b347-135">Blob: Download</span></span>
### <a name="download-single-blob"></a><span data-ttu-id="7b347-136">下載單一 Blob</span><span class="sxs-lookup"><span data-stu-id="7b347-136">Download single blob</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --include "abc.txt"
```

<span data-ttu-id="7b347-137">如果 hello 資料夾`/mnt/myfiles`不存在，AzCopy 會加以建立，並下載`abc.txt `hello 新資料夾。</span><span class="sxs-lookup"><span data-stu-id="7b347-137">If hello folder `/mnt/myfiles` does not exist, AzCopy creates it and downloads `abc.txt ` into hello new folder.</span></span>

### <a name="download-single-blob-from-secondary-region"></a><span data-ttu-id="7b347-138">從次要地區下載單一 Blob</span><span class="sxs-lookup"><span data-stu-id="7b347-138">Download single blob from secondary region</span></span>

```azcopy
azcopy \
    --source https://myaccount-secondary.blob.core.windows.net/mynewcontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --include "abc.txt"
```

<span data-ttu-id="7b347-139">請注意，您必須啟用讀取權限異地備援儲存體。</span><span class="sxs-lookup"><span data-stu-id="7b347-139">Note that you must have read-access geo-redundant storage enabled.</span></span>

### <a name="download-all-blobs"></a><span data-ttu-id="7b347-140">下載所有 Blob</span><span class="sxs-lookup"><span data-stu-id="7b347-140">Download all blobs</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --recursive
```

<span data-ttu-id="7b347-141">假設下列 hello 位於 hello 指定容器的 blob:</span><span class="sxs-lookup"><span data-stu-id="7b347-141">Assume hello following blobs reside in hello specified container:</span></span>  

```
abc.txt
abc1.txt
abc2.txt
vd1/a.txt
vd1/abcd.txt
```

<span data-ttu-id="7b347-142">Hello 下載作業之後，hello 目錄`/mnt/myfiles`包含下列檔案的 hello:</span><span class="sxs-lookup"><span data-stu-id="7b347-142">After hello download operation, hello directory `/mnt/myfiles` includes hello following files:</span></span>

```
/mnt/myfiles/abc.txt
/mnt/myfiles/abc1.txt
/mnt/myfiles/abc2.txt
/mnt/myfiles/vd1/a.txt
/mnt/myfiles/vd1/abcd.txt
```

<span data-ttu-id="7b347-143">如果您未指定選項 `--recursive`，則不會下載任何 Blob。</span><span class="sxs-lookup"><span data-stu-id="7b347-143">If you do not specify option `--recursive`, no blob will be downloaded.</span></span>

### <a name="download-blobs-with-specified-prefix"></a><span data-ttu-id="7b347-144">下載具有指定首碼的 Blob</span><span class="sxs-lookup"><span data-stu-id="7b347-144">Download blobs with specified prefix</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --include "a" \
    --recursive
```

<span data-ttu-id="7b347-145">假設 hello 下列 blob 位於 hello 指定的容器。</span><span class="sxs-lookup"><span data-stu-id="7b347-145">Assume hello following blobs reside in hello specified container.</span></span> <span data-ttu-id="7b347-146">以 hello 前置詞開頭的所有 blob`a`下載。</span><span class="sxs-lookup"><span data-stu-id="7b347-146">All blobs beginning with hello prefix `a` are downloaded.</span></span>

```
abc.txt
abc1.txt
abc2.txt
xyz.txt
vd1\a.txt
vd1\abcd.txt
```

<span data-ttu-id="7b347-147">Hello 下載作業之後，hello 資料夾`/mnt/myfiles`包含下列檔案的 hello:</span><span class="sxs-lookup"><span data-stu-id="7b347-147">After hello download operation, hello folder `/mnt/myfiles` includes hello following files:</span></span>

```
/mnt/myfiles/abc.txt
/mnt/myfiles/abc1.txt
/mnt/myfiles/abc2.txt
```

<span data-ttu-id="7b347-148">hello 前置詞會套用 toohello 虛擬目錄，可形成 hello hello blob 名稱第一個部分。</span><span class="sxs-lookup"><span data-stu-id="7b347-148">hello prefix applies toohello virtual directory, which forms hello first part of hello blob name.</span></span> <span data-ttu-id="7b347-149">Hello 虛擬目錄在 hello 上述範例中，它不符合 hello 指定之前置詞，因此沒有 blob 下載。</span><span class="sxs-lookup"><span data-stu-id="7b347-149">In hello example shown above, hello virtual directory does not match hello specified prefix, so no blob is downloaded.</span></span> <span data-ttu-id="7b347-150">此外，如果 hello 選項`--recursive`未指定，AzCopy 不會下載任何 blob。</span><span class="sxs-lookup"><span data-stu-id="7b347-150">In addition, if hello option `--recursive` is not specified, AzCopy does not download any blobs.</span></span>

### <a name="set-hello-last-modified-time-of-exported-files-toobe-same-as-hello-source-blobs"></a><span data-ttu-id="7b347-151">設定 hello toobe 匯出的檔案的上次修改時間與 hello 來源 blob 相同</span><span class="sxs-lookup"><span data-stu-id="7b347-151">Set hello last-modified time of exported files toobe same as hello source blobs</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination "/mnt/myfiles" \
    --source-key <key> \
    --preserve-last-modified-time
```

<span data-ttu-id="7b347-152">您也可以從其上次修改時間為基礎的 hello 下載作業排除的 blob。</span><span class="sxs-lookup"><span data-stu-id="7b347-152">You can also exclude blobs from hello download operation based on their last-modified time.</span></span> <span data-ttu-id="7b347-153">例如，如果您想 tooexclude blob 的上次修改的時間為 hello 相同或較 hello 目的地檔案，加入 hello`--exclude-newer`選項：</span><span class="sxs-lookup"><span data-stu-id="7b347-153">For example, if you want tooexclude blobs whose last modified time is hello same or newer than hello destination file, add hello `--exclude-newer` option:</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --preserve-last-modified-time \
    --exclude-newer
```

<span data-ttu-id="7b347-154">如果您想 tooexclude blob 的上次修改的時間為 hello 相同或比 hello 目的地檔案還舊，新增 hello 或`--exclude-older`選項：</span><span class="sxs-lookup"><span data-stu-id="7b347-154">Or if you want tooexclude blobs whose last modified time is hello same or older than hello destination file, add hello `--exclude-older` option:</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --preserve-last-modified-time \
    --exclude-older
```

## <a name="blob-upload"></a><span data-ttu-id="7b347-155">Blob：上傳</span><span class="sxs-lookup"><span data-stu-id="7b347-155">Blob: Upload</span></span>
### <a name="upload-single-file"></a><span data-ttu-id="7b347-156">上傳單一檔案</span><span class="sxs-lookup"><span data-stu-id="7b347-156">Upload single file</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --include "abc.txt"
```

<span data-ttu-id="7b347-157">如果 hello 指定的目的地容器不存在，AzCopy 建立及上傳 hello 到其中的檔案。</span><span class="sxs-lookup"><span data-stu-id="7b347-157">If hello specified destination container does not exist, AzCopy creates it and uploads hello file into it.</span></span>

### <a name="upload-single-file-toovirtual-directory"></a><span data-ttu-id="7b347-158">單一檔案上傳 toovirtual 目錄</span><span class="sxs-lookup"><span data-stu-id="7b347-158">Upload single file toovirtual directory</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --include "abc.txt"
```

<span data-ttu-id="7b347-159">如果 hello 指定虛擬目錄不存在，AzCopy 上傳 hello 檔案 tooinclude hello 中的虛擬目錄 hello blob 名稱 (*例如*， `vd/abc.txt` hello 上述範例中)。</span><span class="sxs-lookup"><span data-stu-id="7b347-159">If hello specified virtual directory does not exist, AzCopy uploads hello file tooinclude hello virtual directory in hello blob name (*e.g.*, `vd/abc.txt` in hello example above).</span></span>

### <a name="upload-all-files"></a><span data-ttu-id="7b347-160">上傳所有檔案</span><span class="sxs-lookup"><span data-stu-id="7b347-160">Upload all files</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --recursive
```

<span data-ttu-id="7b347-161">指定選項`--recursive`hello 上傳 hello 內容所指定目錄 tooBlob 儲存體以遞迴方式，這表示所有子資料夾及檔案會上傳以及。</span><span class="sxs-lookup"><span data-stu-id="7b347-161">Specifying option `--recursive` uploads hello contents of hello specified directory tooBlob storage recursively, meaning that all subfolders and their files are uploaded as well.</span></span> <span data-ttu-id="7b347-162">比方說，假設 hello 下列檔案位於資料夾`/mnt/myfiles`:</span><span class="sxs-lookup"><span data-stu-id="7b347-162">For instance, assume hello following files reside in folder `/mnt/myfiles`:</span></span>

```
/mnt/myfiles/abc.txt
/mnt/myfiles/abc1.txt
/mnt/myfiles/abc2.txt
/mnt/myfiles/subfolder/a.txt
/mnt/myfiles/subfolder/abcd.txt
```

<span data-ttu-id="7b347-163">Hello 上傳作業之後，hello 容器會包含下列檔案的 hello:</span><span class="sxs-lookup"><span data-stu-id="7b347-163">After hello upload operation, hello container includes hello following files:</span></span>

```
abc.txt
abc1.txt
abc2.txt
subfolder/a.txt
subfolder/abcd.txt
```

<span data-ttu-id="7b347-164">當 hello 選項`--recursive`未指定，只有 hello 下列三個檔案上傳：</span><span class="sxs-lookup"><span data-stu-id="7b347-164">When hello option `--recursive` is not specified, only hello following three files are uploaded:</span></span>

```
abc.txt
abc1.txt
abc2.txt
```

### <a name="upload-files-matching-specified-pattern"></a><span data-ttu-id="7b347-165">上傳符合指定模式的檔案</span><span class="sxs-lookup"><span data-stu-id="7b347-165">Upload files matching specified pattern</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --include "a*" \
    --recursive
```

<span data-ttu-id="7b347-166">假設 hello 下列檔案位於資料夾`/mnt/myfiles`:</span><span class="sxs-lookup"><span data-stu-id="7b347-166">Assume hello following files reside in folder `/mnt/myfiles`:</span></span>

```
/mnt/myfiles/abc.txt
/mnt/myfiles/abc1.txt
/mnt/myfiles/abc2.txt
/mnt/myfiles/xyz.txt
/mnt/myfiles/subfolder/a.txt
/mnt/myfiles/subfolder/abcd.txt
```

<span data-ttu-id="7b347-167">Hello 上傳作業之後，hello 容器會包含下列檔案的 hello:</span><span class="sxs-lookup"><span data-stu-id="7b347-167">After hello upload operation, hello container includes hello following files:</span></span>

```
abc.txt
abc1.txt
abc2.txt
subfolder/a.txt
subfolder/abcd.txt
```

<span data-ttu-id="7b347-168">當 hello 選項`--recursive`未指定，AzCopy 會略過在子目錄中的檔案：</span><span class="sxs-lookup"><span data-stu-id="7b347-168">When hello option `--recursive` is not specified, AzCopy skips files that are in sub-directories:</span></span>

```
abc.txt
abc1.txt
abc2.txt
```

### <a name="specify-hello-mime-content-type-of-a-destination-blob"></a><span data-ttu-id="7b347-169">指定目的地 blob hello MIME 內容的類型</span><span class="sxs-lookup"><span data-stu-id="7b347-169">Specify hello MIME content type of a destination blob</span></span>
<span data-ttu-id="7b347-170">根據預設，AzCopy 設定 hello 的目的地 blob 的內容型別太`application/octet-stream`。</span><span class="sxs-lookup"><span data-stu-id="7b347-170">By default, AzCopy sets hello content type of a destination blob too`application/octet-stream`.</span></span> <span data-ttu-id="7b347-171">不過，您可以明確指定 hello 透過 hello 選項的內容類型`--set-content-type [content-type]`。</span><span class="sxs-lookup"><span data-stu-id="7b347-171">However, you can explicitly specify hello content type via hello option `--set-content-type [content-type]`.</span></span> <span data-ttu-id="7b347-172">此語法中上傳作業設定 hello 的所有 blob 的內容類型。</span><span class="sxs-lookup"><span data-stu-id="7b347-172">This syntax sets hello content type for all blobs in an upload operation.</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/myContainer/ \
    --dest-key <key> \
    --include "ab" \
    --set-content-type "video/mp4"
```

<span data-ttu-id="7b347-173">如果 hello 選項`--set-content-type`AzCopy 會將每個 blob 或檔案，但沒有值，指定的內容類型，根據 tooits 副檔名。</span><span class="sxs-lookup"><span data-stu-id="7b347-173">If hello option `--set-content-type` is specified without a value, then AzCopy sets each blob or file's content type according tooits file extension.</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/myContainer/ \
    --dest-key <key> \
    --include "ab" \
    --set-content-type
```

## <a name="blob-copy"></a><span data-ttu-id="7b347-174">Blob：複製</span><span class="sxs-lookup"><span data-stu-id="7b347-174">Blob: Copy</span></span>
### <a name="copy-single-blob-within-storage-account"></a><span data-ttu-id="7b347-175">複製儲存體帳戶內的單一 Blob</span><span class="sxs-lookup"><span data-stu-id="7b347-175">Copy single blob within Storage account</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer1 \
    --destination https://myaccount.blob.core.windows.net/mycontainer2 \
    --source-key <key> \
    --dest-key <key> \
    --include "abc.txt"
```

<span data-ttu-id="7b347-176">當您未以 --sync-copy 選項複製 Blob 時，系統會執行[伺服器端複製](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) \(英文\) 作業。</span><span class="sxs-lookup"><span data-stu-id="7b347-176">When you copy a blob without --sync-copy option, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="copy-single-blob-across-storage-accounts"></a><span data-ttu-id="7b347-177">跨儲存體帳戶複製單一 Blob</span><span class="sxs-lookup"><span data-stu-id="7b347-177">Copy single blob across Storage accounts</span></span>

```azcopy
azcopy \
    --source https://sourceaccount.blob.core.windows.net/mycontainer1 \
    --destination https://destaccount.blob.core.windows.net/mycontainer2 \
    --source-key <key1> \
    --dest-key <key2> \
    --include "abc.txt"
```

<span data-ttu-id="7b347-178">當您未以 --sync-copy 選項複製 Blob 時，系統會執行[伺服器端複製](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) \(英文\) 作業。</span><span class="sxs-lookup"><span data-stu-id="7b347-178">When you copy a blob without --sync-copy option, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="copy-single-blob-from-secondary-region-tooprimary-region"></a><span data-ttu-id="7b347-179">從次要區域 tooprimary 區域複製單一 blob</span><span class="sxs-lookup"><span data-stu-id="7b347-179">Copy single blob from secondary region tooprimary region</span></span>

```azcopy
azcopy \
    --source https://myaccount1-secondary.blob.core.windows.net/mynewcontainer1 \
    --destination https://myaccount2.blob.core.windows.net/mynewcontainer2 \
    --source-key <key1> \
    --dest-key <key2> \
    --include "abc.txt"
```

<span data-ttu-id="7b347-180">請注意，您必須啟用讀取權限異地備援儲存體。</span><span class="sxs-lookup"><span data-stu-id="7b347-180">Note that you must have read-access geo-redundant storage enabled.</span></span>

### <a name="copy-single-blob-and-its-snapshots-across-storage-accounts"></a><span data-ttu-id="7b347-181">跨儲存體帳戶複製單一 Blob 及其快照</span><span class="sxs-lookup"><span data-stu-id="7b347-181">Copy single blob and its snapshots across Storage accounts</span></span>

```azcopy
azcopy \
    --source https://sourceaccount.blob.core.windows.net/mycontainer1 \
    --destination https://destaccount.blob.core.windows.net/mycontainer2 \
    --source-key <key1> \
    --dest-key <key2> \
    --include "abc.txt" \
    --include-snapshot
```

<span data-ttu-id="7b347-182">Hello 複製作業之後，hello 目標容器包含 hello blob 和其快照集。</span><span class="sxs-lookup"><span data-stu-id="7b347-182">After hello copy operation, hello target container includes hello blob and its snapshots.</span></span> <span data-ttu-id="7b347-183">hello 容器包含 hello 下列 blob 和其快照集：</span><span class="sxs-lookup"><span data-stu-id="7b347-183">hello container includes hello following blob and its snapshots:</span></span>

```
abc.txt
abc (2013-02-25 080757).txt
abc (2014-02-21 150331).txt
```

### <a name="synchronously-copy-blobs-across-storage-accounts"></a><span data-ttu-id="7b347-184">以同步方式跨儲存體帳戶複製 Blob</span><span class="sxs-lookup"><span data-stu-id="7b347-184">Synchronously copy blobs across Storage accounts</span></span>
<span data-ttu-id="7b347-185">根據預設，AzCopy 會以非同步方式在兩個儲存體端點之間複製資料。</span><span class="sxs-lookup"><span data-stu-id="7b347-185">AzCopy by default copies data between two storage endpoints asynchronously.</span></span> <span data-ttu-id="7b347-186">因此，複製 hello 背景使用的備用頻寬容量且沒有 SLA 方面的速度有多快 blob 中的 hello 複製作業執行。</span><span class="sxs-lookup"><span data-stu-id="7b347-186">Therefore, hello copy operation runs in hello background using spare bandwidth capacity that has no SLA in terms of how fast a blob is copied.</span></span> 

<span data-ttu-id="7b347-187">hello`--sync-copy`選項可確保 hello 複製作業取得一致的速度。</span><span class="sxs-lookup"><span data-stu-id="7b347-187">hello `--sync-copy` option ensures that hello copy operation gets consistent speed.</span></span> <span data-ttu-id="7b347-188">AzCopy 下載 hello blob 執行 hello 同步複本 toocopy hello 從指定來源 toolocal 記憶體，並再將其上傳 toohello Blob 儲存體目的地。</span><span class="sxs-lookup"><span data-stu-id="7b347-188">AzCopy performs hello synchronous copy by downloading hello blobs toocopy from hello specified source toolocal memory, and then uploading them toohello Blob storage destination.</span></span>

```azcopy
azcopy \
    --source https://myaccount1.blob.core.windows.net/myContainer/ \
    --destination https://myaccount2.blob.core.windows.net/myContainer/ \
    --source-key <key1> \
    --dest-key <key2> \
    --include "ab" \
    --sync-copy
```

<span data-ttu-id="7b347-189">`--sync-copy`可能會產生額外的輸出成本比較 tooasynchronous 複製。</span><span class="sxs-lookup"><span data-stu-id="7b347-189">`--sync-copy` might generate additional egress cost compared tooasynchronous copy.</span></span> <span data-ttu-id="7b347-190">hello 建議的方法是 toouse 處於 hello Azure VM 中的這個選項與您來源儲存體帳戶 tooavoid 出口成本相同的區域。</span><span class="sxs-lookup"><span data-stu-id="7b347-190">hello recommended approach is toouse this option in an Azure VM, that is in hello same region as your source storage account tooavoid egress cost.</span></span>

## <a name="file-download"></a><span data-ttu-id="7b347-191">檔案：下載</span><span class="sxs-lookup"><span data-stu-id="7b347-191">File: Download</span></span>
### <a name="download-single-file"></a><span data-ttu-id="7b347-192">下載單一檔案</span><span class="sxs-lookup"><span data-stu-id="7b347-192">Download single file</span></span>

```azcopy
azcopy \
    --source https://myaccount.file.core.windows.net/myfileshare/myfolder1/ \
    --destination /mnt/myfiles \
    --source-key <key> \
    --include "abc.txt"
```

<span data-ttu-id="7b347-193">如果 hello 指定來源是 Azure 的檔案共用，則您必須指定 hello 確切的檔名，(*例如* `abc.txt`) toodownload 單一檔案，或指定選項`--recursive`toodownload 所有檔案在 hello 共用以遞迴方式。</span><span class="sxs-lookup"><span data-stu-id="7b347-193">If hello specified source is an Azure file share, then you must either specify hello exact file name, (*e.g.* `abc.txt`) toodownload a single file, or specify option `--recursive` toodownload all files in hello share recursively.</span></span> <span data-ttu-id="7b347-194">檔案模式和選項，嘗試 toospecify`--recursive`一起會產生錯誤。</span><span class="sxs-lookup"><span data-stu-id="7b347-194">Attempting toospecify both a file pattern and option `--recursive` together results in an error.</span></span>

### <a name="download-all-files"></a><span data-ttu-id="7b347-195">下載所有檔案</span><span class="sxs-lookup"><span data-stu-id="7b347-195">Download all files</span></span>

```azcopy
azcopy \
    --source https://myaccount.file.core.windows.net/myfileshare/ \
    --destination /mnt/myfiles \
    --source-key <key> \
    --recursive
```

<span data-ttu-id="7b347-196">請注意，並不會下載任何空白資料夾。</span><span class="sxs-lookup"><span data-stu-id="7b347-196">Note that any empty folders are not downloaded.</span></span>

## <a name="file-upload"></a><span data-ttu-id="7b347-197">檔案：上傳</span><span class="sxs-lookup"><span data-stu-id="7b347-197">File: Upload</span></span>
### <a name="upload-single-file"></a><span data-ttu-id="7b347-198">上傳單一檔案</span><span class="sxs-lookup"><span data-stu-id="7b347-198">Upload single file</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.file.core.windows.net/myfileshare/ \
    --dest-key <key> \
    --include abc.txt
```

### <a name="upload-all-files"></a><span data-ttu-id="7b347-199">上傳所有檔案</span><span class="sxs-lookup"><span data-stu-id="7b347-199">Upload all files</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.file.core.windows.net/myfileshare/ \
    --dest-key <key> \
    --recursive
```

<span data-ttu-id="7b347-200">請注意，並不會上傳任何空白資料夾。</span><span class="sxs-lookup"><span data-stu-id="7b347-200">Note that any empty folders are not uploaded.</span></span>

### <a name="upload-files-matching-specified-pattern"></a><span data-ttu-id="7b347-201">上傳符合指定模式的檔案</span><span class="sxs-lookup"><span data-stu-id="7b347-201">Upload files matching specified pattern</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.file.core.windows.net/myfileshare/ \
    --dest-key <key> \
    --include "ab*" \
    --recursive
```

## <a name="file-copy"></a><span data-ttu-id="7b347-202">檔案：複製</span><span class="sxs-lookup"><span data-stu-id="7b347-202">File: Copy</span></span>
### <a name="copy-across-file-shares"></a><span data-ttu-id="7b347-203">跨檔案共用複製</span><span class="sxs-lookup"><span data-stu-id="7b347-203">Copy across file shares</span></span>

```azcopy
azcopy \
    --source https://myaccount1.file.core.windows.net/myfileshare1/ \
    --destination https://myaccount2.file.core.windows.net/myfileshare2/ \
    --source-key <key1> \
    --dest-key <key2> \
    --recursive
```
<span data-ttu-id="7b347-204">當您跨檔案共用複製檔案時，系統會執行[伺服器端複製](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx)作業。</span><span class="sxs-lookup"><span data-stu-id="7b347-204">When you copy a file across file shares, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="copy-from-file-share-tooblob"></a><span data-ttu-id="7b347-205">從檔案共用 tooblob 複製</span><span class="sxs-lookup"><span data-stu-id="7b347-205">Copy from file share tooblob</span></span>

```azcopy
azcopy \ 
    --source https://myaccount1.file.core.windows.net/myfileshare/ \
    --destination https://myaccount2.blob.core.windows.net/mycontainer/ \
    --source-key <key1> \
    --dest-key <key2> \
    --recursive
```
<span data-ttu-id="7b347-206">當您複製檔案從檔案共用 tooblob，[伺服器端副本](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx)執行作業。</span><span class="sxs-lookup"><span data-stu-id="7b347-206">When you copy a file from file share tooblob, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="copy-from-blob-toofile-share"></a><span data-ttu-id="7b347-207">複製 blob toofile 共用</span><span class="sxs-lookup"><span data-stu-id="7b347-207">Copy from blob toofile share</span></span>

```azcopy
azcopy \
    --source https://myaccount1.blob.core.windows.net/mycontainer/ \
    --destination https://myaccount2.file.core.windows.net/myfileshare/ \
    --source-key <key1> \
    --dest-key <key2> \
    --recursive
```
<span data-ttu-id="7b347-208">當您複製檔案從 blob toofile 共用，[伺服器端副本](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx)執行作業。</span><span class="sxs-lookup"><span data-stu-id="7b347-208">When you copy a file from blob toofile share, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="synchronously-copy-files"></a><span data-ttu-id="7b347-209">以同步方式複製檔案</span><span class="sxs-lookup"><span data-stu-id="7b347-209">Synchronously copy files</span></span>
<span data-ttu-id="7b347-210">您可以指定 hello`--sync-copy`同步選項 toocopy 資料從檔案儲存體 tooFile 存放裝置、 檔案儲存體 tooBlob 儲存體和 Blob 儲存體 tooFile 儲存體。</span><span class="sxs-lookup"><span data-stu-id="7b347-210">You can specify hello `--sync-copy` option toocopy data from File Storage tooFile Storage, from File Storage tooBlob Storage and from Blob Storage tooFile Storage synchronously.</span></span> <span data-ttu-id="7b347-211">AzCopy 會藉由下載 hello 來源資料 toolocal 記憶體，然後將它上傳 toodestination 執行此作業。</span><span class="sxs-lookup"><span data-stu-id="7b347-211">AzCopy runs this operation by downloading hello source data toolocal memory, and then uploading it toodestination.</span></span> <span data-ttu-id="7b347-212">在此情況下，會產生標準輸出成本。</span><span class="sxs-lookup"><span data-stu-id="7b347-212">In this case, standard egress cost applies.</span></span>

```azcopy
azcopy \
    --source https://myaccount1.file.core.windows.net/myfileshare1/ \
    --destination https://myaccount2.file.core.windows.net/myfileshare2/ \
    --source-key <key1> \
    --dest-key <key2> \
    --recursive \
    --sync-copy
```

<span data-ttu-id="7b347-213">當複製檔案的儲存體 tooBlob 儲存體，hello 預設 blob 型別是區塊 blob，使用者可以指定選項`/BlobType:page`toochange hello 目的地 blob 類型。</span><span class="sxs-lookup"><span data-stu-id="7b347-213">When copying from File Storage tooBlob Storage, hello default blob type is block blob, user can specify option `/BlobType:page` toochange hello destination blob type.</span></span>

<span data-ttu-id="7b347-214">請注意，`--sync-copy`可能會產生額外成本比較 tooasynchronous 複製的輸出。</span><span class="sxs-lookup"><span data-stu-id="7b347-214">Note that `--sync-copy` might generate additional egress cost comparing tooasynchronous copy.</span></span> <span data-ttu-id="7b347-215">hello 建議的方法是 toouse 處於 hello Azure VM 中的這個選項與您來源儲存體帳戶 tooavoid 出口成本相同的區域。</span><span class="sxs-lookup"><span data-stu-id="7b347-215">hello recommended approach is toouse this option in an Azure VM, that is in hello same region as your source storage account tooavoid egress cost.</span></span>

## <a name="other-azcopy-features"></a><span data-ttu-id="7b347-216">其他 AzCopy 功能</span><span class="sxs-lookup"><span data-stu-id="7b347-216">Other AzCopy features</span></span>
### <a name="only-copy-data-that-doesnt-exist-in-hello-destination"></a><span data-ttu-id="7b347-217">只複製 hello 目的地中不存在的資料</span><span class="sxs-lookup"><span data-stu-id="7b347-217">Only copy data that doesn't exist in hello destination</span></span>
<span data-ttu-id="7b347-218">hello`--exclude-older`和`--exclude-newer`參數可讓您從要複製，分別 tooexclude 更舊或更新的來源資源。</span><span class="sxs-lookup"><span data-stu-id="7b347-218">hello `--exclude-older` and `--exclude-newer` parameters allow you tooexclude older or newer source resources from being copied, respectively.</span></span> <span data-ttu-id="7b347-219">如果您只想 toocopy 來源資源不存在於 hello 目的地中，您可以在 hello AzCopy 命令中指定這兩個參數：</span><span class="sxs-lookup"><span data-stu-id="7b347-219">If you only want toocopy source resources that don't exist in hello destination, you can specify both parameters in hello AzCopy command:</span></span>

    --source http://myaccount.blob.core.windows.net/mycontainer --destination /mnt/myfiles --source-key <sourcekey> --recursive --exclude-older --exclude-newer

    --source /mnt/myfiles --destination http://myaccount.file.core.windows.net/myfileshare --dest-key <destkey> --recursive --exclude-older --exclude-newer

    --source http://myaccount.blob.core.windows.net/mycontainer --destination http://myaccount.blob.core.windows.net/mycontainer1 --source-key <sourcekey> --dest-key <destkey> --recursive --exclude-older --exclude-newer

### <a name="use-a-configuration-file-toospecify-command-line-parameters"></a><span data-ttu-id="7b347-220">使用組態檔 toospecify 命令列參數</span><span class="sxs-lookup"><span data-stu-id="7b347-220">Use a configuration file toospecify command-line parameters</span></span>

```azcopy
azcopy --config-file "azcopy-config.ini"
```

<span data-ttu-id="7b347-221">您可以在組態檔中包含任何 AzCopy 命令列參數。</span><span class="sxs-lookup"><span data-stu-id="7b347-221">You can include any AzCopy command-line parameters in a configuration file.</span></span> <span data-ttu-id="7b347-222">AzCopy 處理程序 hello hello 檔案中的參數，如同它們已執行 hello 檔案直接替代與 hello 內容的 hello 命令列上指定。</span><span class="sxs-lookup"><span data-stu-id="7b347-222">AzCopy processes hello parameters in hello file as if they had been specified on hello command line, performing a direct substitution with hello contents of hello file.</span></span>

<span data-ttu-id="7b347-223">假設名為組態檔`copyoperation`，其中包含下列行 hello。</span><span class="sxs-lookup"><span data-stu-id="7b347-223">Assume a configuration file named `copyoperation`, that contains hello following lines.</span></span> <span data-ttu-id="7b347-224">每個 AzCopy 參數可以指定在同一行。</span><span class="sxs-lookup"><span data-stu-id="7b347-224">Each AzCopy parameter can be specified on a single line.</span></span>

    --source http://myaccount.blob.core.windows.net/mycontainer --destination /mnt/myfiles --source-key <sourcekey> --recursive --quiet

<span data-ttu-id="7b347-225">或不同行：</span><span class="sxs-lookup"><span data-stu-id="7b347-225">or on separate lines:</span></span>

    --source http://myaccount.blob.core.windows.net/mycontainer
    --destination /mnt/myfiles
    --source-key<sourcekey>
    --recursive
    --quiet

<span data-ttu-id="7b347-226">AzCopy 失敗如果 hello 參數分成兩行，如下所示為 hello`--source-key`參數：</span><span class="sxs-lookup"><span data-stu-id="7b347-226">AzCopy fails if you split hello parameter across two lines, as shown here for hello `--source-key` parameter:</span></span>

    http://myaccount.blob.core.windows.net/mycontainer
    /mnt/myfiles
    --sourcekey
    <sourcekey>
    --recursive
    --quiet

### <a name="specify-a-shared-access-signature-sas"></a><span data-ttu-id="7b347-227">指定共用存取簽章 (SAS)</span><span class="sxs-lookup"><span data-stu-id="7b347-227">Specify a shared access signature (SAS)</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer1 \
    --destination https://myaccount.blob.core.windows.net/mycontainer2 \
    --source-sas <SAS1> \
    --dest-sas <SAS2> \
    --include abc.txt
```

<span data-ttu-id="7b347-228">您也可以指定 SAS hello 容器 URI 上：</span><span class="sxs-lookup"><span data-stu-id="7b347-228">You can also specify a SAS on hello container URI:</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer1/?SourceSASToken \
    --destination /mnt/myfiles \
    --recursive
```

<span data-ttu-id="7b347-229">請注意，AzCopy 目前僅支援 hello[帳戶 SAS](https://docs.microsoft.com/en-us/azure/storage/storage-dotnet-shared-access-signature-part-1)。</span><span class="sxs-lookup"><span data-stu-id="7b347-229">Note that AzCopy currently only supports hello [Account SAS](https://docs.microsoft.com/en-us/azure/storage/storage-dotnet-shared-access-signature-part-1).</span></span>

### <a name="journal-file-folder"></a><span data-ttu-id="7b347-230">日誌檔案資料夾</span><span class="sxs-lookup"><span data-stu-id="7b347-230">Journal file folder</span></span>
<span data-ttu-id="7b347-231">每次您提交命令 tooAzCopy，它會檢查日誌檔是否存在於 hello 預設資料夾，或是否有您指定透過這個選項的資料夾中。</span><span class="sxs-lookup"><span data-stu-id="7b347-231">Each time you issue a command tooAzCopy, it checks whether a journal file exists in hello default folder, or whether it exists in a folder that you specified via this option.</span></span> <span data-ttu-id="7b347-232">如果在任一處，hello 日誌檔不存在，AzCopy hello 作業視為新，並產生新的日誌檔。</span><span class="sxs-lookup"><span data-stu-id="7b347-232">If hello journal file does not exist in either place, AzCopy treats hello operation as new and generates a new journal file.</span></span>

<span data-ttu-id="7b347-233">如果 hello 日誌檔案存在，AzCopy 會檢查您輸入的 hello 命令列是否符合 hello hello 筆記本檔案中的命令列。</span><span class="sxs-lookup"><span data-stu-id="7b347-233">If hello journal file does exist, AzCopy checks whether hello command line that you input matches hello command line in hello journal file.</span></span> <span data-ttu-id="7b347-234">如果兩個命令列 hello 相符，AzCopy 會繼續 hello 未完成作業。</span><span class="sxs-lookup"><span data-stu-id="7b347-234">If hello two command lines match, AzCopy resumes hello incomplete operation.</span></span> <span data-ttu-id="7b347-235">如果不相符，AzCopy 會提示使用者 tooeither 覆寫 hello 日誌檔案 toostart，新增作業或 toocancel hello 目前的作業。</span><span class="sxs-lookup"><span data-stu-id="7b347-235">If they do not match, AzCopy prompts user tooeither overwrite hello journal file toostart a new operation, or toocancel hello current operation.</span></span>

<span data-ttu-id="7b347-236">如果您想 hello 日誌檔 toouse hello 預設位置：</span><span class="sxs-lookup"><span data-stu-id="7b347-236">If you want toouse hello default location for hello journal file:</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --resume
```

<span data-ttu-id="7b347-237">如果您省略選項`--resume`，或指定選項`--resume`未 hello 資料夾路徑，如上所示，AzCopy 會建立 hello 日誌檔 hello 預設位置，也就是在`~\Microsoft\Azure\AzCopy`。</span><span class="sxs-lookup"><span data-stu-id="7b347-237">If you omit option `--resume`, or specify option `--resume` without hello folder path, as shown above, AzCopy creates hello journal file in hello default location, which is `~\Microsoft\Azure\AzCopy`.</span></span> <span data-ttu-id="7b347-238">如果 hello 日誌檔已經存在，然後 AzCopy 會繼續 hello hello 日誌檔為基礎的作業。</span><span class="sxs-lookup"><span data-stu-id="7b347-238">If hello journal file already exists, then AzCopy resumes hello operation based on hello journal file.</span></span>

<span data-ttu-id="7b347-239">如果您想 toospecify hello 日誌檔的自訂位置：</span><span class="sxs-lookup"><span data-stu-id="7b347-239">If you want toospecify a custom location for hello journal file:</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key key \
    --resume "/mnt/myjournal"
```

<span data-ttu-id="7b347-240">如果不存在，此範例會建立 hello 日誌檔。</span><span class="sxs-lookup"><span data-stu-id="7b347-240">This example creates hello journal file if it does not already exist.</span></span> <span data-ttu-id="7b347-241">如果檔案存在，然後 AzCopy 會繼續依據 hello 日誌檔的 hello 作業。</span><span class="sxs-lookup"><span data-stu-id="7b347-241">If it does exist, then AzCopy resumes hello operation based on hello journal file.</span></span>

<span data-ttu-id="7b347-242">如果您想 tooresume AzCopy 作業時，重複 hello 相同的命令。</span><span class="sxs-lookup"><span data-stu-id="7b347-242">If you want tooresume an AzCopy operation, repeat hello same command.</span></span> <span data-ttu-id="7b347-243">然後 AzCopy on Linux 會提示您確認：</span><span class="sxs-lookup"><span data-stu-id="7b347-243">AzCopy on Linux then will prompt for confirmation:</span></span>

```azcopy
Incomplete operation with same command line detected at hello journal directory "/home/myaccount/Microsoft/Azure/AzCopy", do you want tooresume hello operation? Choose Yes tooresume, choose No toooverwrite hello journal toostart a new operation. (Yes/No)
```

### <a name="output-verbose-logs"></a><span data-ttu-id="7b347-244">輸出詳細資訊記錄檔</span><span class="sxs-lookup"><span data-stu-id="7b347-244">Output verbose logs</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --verbose
```

### <a name="specify-hello-number-of-concurrent-operations-toostart"></a><span data-ttu-id="7b347-245">指定的並行作業 toostart hello</span><span class="sxs-lookup"><span data-stu-id="7b347-245">Specify hello number of concurrent operations toostart</span></span>
<span data-ttu-id="7b347-246">選項`--parallel-level`指定 hello 並行的複製作業數目。</span><span class="sxs-lookup"><span data-stu-id="7b347-246">Option `--parallel-level` specifies hello number of concurrent copy operations.</span></span> <span data-ttu-id="7b347-247">根據預設，AzCopy 會啟動特定數目的並行作業 tooincrease hello 資料傳輸輸送量。</span><span class="sxs-lookup"><span data-stu-id="7b347-247">By default, AzCopy starts a certain number of concurrent operations tooincrease hello data transfer throughput.</span></span> <span data-ttu-id="7b347-248">並行作業的 hello 數目等於八次 hello 您擁有的處理器數目。</span><span class="sxs-lookup"><span data-stu-id="7b347-248">hello number of concurrent operations is equal eight times hello number of processors you have.</span></span> <span data-ttu-id="7b347-249">如果您正在執行 AzCopy 透過低頻寬網路，您可以指定較低的數字-平行層級 tooavoid 失敗的資源競爭所造成。</span><span class="sxs-lookup"><span data-stu-id="7b347-249">If you are running AzCopy across a low-bandwidth network, you can specify a lower number for --parallel-level tooavoid failure caused by resource competition.</span></span>

[!TIP]
><span data-ttu-id="7b347-250">tooview hello 完整清單的 AzCopy 參數，請查看 'azcopy-說明' 功能表。</span><span class="sxs-lookup"><span data-stu-id="7b347-250">tooview hello complete list of AzCopy parameters, check out 'azcopy --help' menu.</span></span>

## <a name="known-issues-and-best-practices"></a><span data-ttu-id="7b347-251">已知問題和最佳作法</span><span class="sxs-lookup"><span data-stu-id="7b347-251">Known issues and best practices</span></span>
### <a name="error-net-core-is-not-found-in-hello-system"></a><span data-ttu-id="7b347-252">錯誤： Hello 系統中找不到.NET Core。</span><span class="sxs-lookup"><span data-stu-id="7b347-252">Error: .NET Core is not found in hello system.</span></span>
<span data-ttu-id="7b347-253">如果您遇到錯誤，指出 hello 系統中未安裝的.NET Core，hello 路徑 toohello.NET Core 二進位`dotnet`可能會遺失。</span><span class="sxs-lookup"><span data-stu-id="7b347-253">If you encounter an error stating that .NET Core is not installed in hello system, hello PATH toohello .NET Core binary `dotnet` may be missing.</span></span>

<span data-ttu-id="7b347-254">在順序 tooaddress 此問題，尋找 hello 系統中的 hello.NET Core 二進位檔：</span><span class="sxs-lookup"><span data-stu-id="7b347-254">In order tooaddress this issue, find hello .NET Core binary in hello system:</span></span>
```bash
sudo find / -name dotnet
```

<span data-ttu-id="7b347-255">這會傳回 hello 路徑 toohello dotnet 二進位。</span><span class="sxs-lookup"><span data-stu-id="7b347-255">This returns hello path toohello dotnet binary.</span></span> 

    /opt/rh/rh-dotnetcore11/root/usr/bin/dotnet
    /opt/rh/rh-dotnetcore11/root/usr/lib64/dotnetcore/dotnet
    /opt/rh/rh-dotnetcore11/root/usr/lib64/dotnetcore/shared/Microsoft.NETCore.App/1.1.2/dotnet

<span data-ttu-id="7b347-256">現在加入此路徑 toohello 路徑變數。</span><span class="sxs-lookup"><span data-stu-id="7b347-256">Now add this path toohello PATH variable.</span></span> <span data-ttu-id="7b347-257">Sudo，編輯 secure_path toocontain hello 路徑 toohello dotnet 二進位：</span><span class="sxs-lookup"><span data-stu-id="7b347-257">For sudo, edit secure_path toocontain hello path toohello dotnet binary:</span></span>
```bash 
sudo visudo
### Append hello path found in hello preceding example too'secure_path' variable
```

<span data-ttu-id="7b347-258">在此範例中，secure_path 變數會顯示為：</span><span class="sxs-lookup"><span data-stu-id="7b347-258">In this example, secure_path variable reads as:</span></span>

```
secure_path = /sbin:/bin:/usr/sbin:/usr/bin:/opt/rh/rh-dotnetcore11/root/usr/bin/
```

<span data-ttu-id="7b347-259">Hello 目前的使用者編輯.bash_profile/.profile tooinclude hello 路徑 toohello dotnet 二進位 PATH 變數中</span><span class="sxs-lookup"><span data-stu-id="7b347-259">For hello current user, edit .bash_profile/.profile tooinclude hello path toohello dotnet binary in PATH variable</span></span> 
```bash
vi ~/.bash_profile
### Append hello path found in hello preceding example too'PATH' variable
```

<span data-ttu-id="7b347-260">確認 .NET Core 現在位於 PATH 中：</span><span class="sxs-lookup"><span data-stu-id="7b347-260">Verify that .NET Core is now in PATH:</span></span>
```bash
which dotnet
sudo which dotnet
```

### <a name="error-installing-azcopy"></a><span data-ttu-id="7b347-261">安裝 AzCopy 時發生錯誤</span><span class="sxs-lookup"><span data-stu-id="7b347-261">Error Installing AzCopy</span></span>
<span data-ttu-id="7b347-262">如果您遇到的 AzCopy 安裝問題，您可以嘗試的 toorun AzCopy hello 中使用 hello bash 指令碼擷取`azcopy`資料夾。</span><span class="sxs-lookup"><span data-stu-id="7b347-262">If you encounter issues with AzCopy installation, you may try toorun AzCopy using hello bash script in hello extracted `azcopy` folder.</span></span>

```bash
cd azcopy
./azcopy
```

### <a name="limit-concurrent-writes-while-copying-data"></a><span data-ttu-id="7b347-263">限制複製資料時的並行寫入</span><span class="sxs-lookup"><span data-stu-id="7b347-263">Limit concurrent writes while copying data</span></span>
<span data-ttu-id="7b347-264">當您複製 blob 或利用 azcopy 進行的檔案時，請注意，另一個應用程式可能會修改 hello 資料將複製時。</span><span class="sxs-lookup"><span data-stu-id="7b347-264">When you copy blobs or files with AzCopy, keep in mind that another application may be modifying hello data while you are copying it.</span></span> <span data-ttu-id="7b347-265">可能的話，請確定不會被您要複製的 hello 資料修改 hello 複製作業期間。</span><span class="sxs-lookup"><span data-stu-id="7b347-265">If possible, ensure that hello data you are copying is not being modified during hello copy operation.</span></span> <span data-ttu-id="7b347-266">比方說，當複製與 Azure 虛擬機器相關聯的 VHD，請確定沒有其他應用程式目前正在撰寫 toohello VHD。</span><span class="sxs-lookup"><span data-stu-id="7b347-266">For example, when copying a VHD associated with an Azure virtual machine, make sure that no other applications are currently writing toohello VHD.</span></span> <span data-ttu-id="7b347-267">這是預設租用 hello 資源 toobe 複製的好方法 toodo。</span><span class="sxs-lookup"><span data-stu-id="7b347-267">A good way toodo this is by leasing hello resource toobe copied.</span></span> <span data-ttu-id="7b347-268">或者，您可以先建立 hello VHD 的快照集，然後複製 hello 快照集。</span><span class="sxs-lookup"><span data-stu-id="7b347-268">Alternately, you can create a snapshot of hello VHD first and then copy hello snapshot.</span></span>

<span data-ttu-id="7b347-269">如果您不能防止其他應用程式無法寫入 tooblobs 或檔案，它們會被複製，則請記住，hello 時間 hello 作業完成時，hello 複製的資源可能不再需要完整的同位檢查，但 hello 來源資源。</span><span class="sxs-lookup"><span data-stu-id="7b347-269">If you cannot prevent other applications from writing tooblobs or files while they are being copied, then keep in mind that by hello time hello job finishes, hello copied resources may no longer have full parity with hello source resources.</span></span>

### <a name="run-one-azcopy-instance-on-one-machine"></a><span data-ttu-id="7b347-270">在一部電腦上執行一個 AzCopy 執行個體。</span><span class="sxs-lookup"><span data-stu-id="7b347-270">Run one AzCopy instance on one machine.</span></span>
<span data-ttu-id="7b347-271">AzCopy 是設計的 toomaximize hello 善用您的電腦資源 tooaccelerate hello 資料傳輸，因此建議您只有一個 AzCopy 執行個體執行一個在電腦上，並指定 hello 選項`--parallel-level`如果您需要更多的並行作業。</span><span class="sxs-lookup"><span data-stu-id="7b347-271">AzCopy is designed toomaximize hello utilization of your machine resource tooaccelerate hello data transfer, we recommend you run only one AzCopy instance on one machine, and specify hello option `--parallel-level` if you need more concurrent operations.</span></span> <span data-ttu-id="7b347-272">如需詳細資訊，請輸入`AzCopy --help parallel-level`在 hello 命令列。</span><span class="sxs-lookup"><span data-stu-id="7b347-272">For more details, type `AzCopy --help parallel-level` at hello command line.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7b347-273">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7b347-273">Next steps</span></span>
<span data-ttu-id="7b347-274">如需 Azure 儲存體和 AzCopy 的詳細資訊，請參閱下列資源的 hello:</span><span class="sxs-lookup"><span data-stu-id="7b347-274">For more information about Azure Storage and AzCopy, see hello following resources:</span></span>

### <a name="azure-storage-documentation"></a><span data-ttu-id="7b347-275">Azure 儲存體文件：</span><span class="sxs-lookup"><span data-stu-id="7b347-275">Azure Storage documentation:</span></span>
* [<span data-ttu-id="7b347-276">簡介 tooAzure 儲存體</span><span class="sxs-lookup"><span data-stu-id="7b347-276">Introduction tooAzure Storage</span></span>](storage-introduction.md)
* [<span data-ttu-id="7b347-277">建立儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="7b347-277">Create a storage account</span></span>](storage-create-storage-account.md)
* <span data-ttu-id="7b347-278">[使用儲存體總管來管理 Blob](https://docs.microsoft.com/en-us/azure/vs-azure-tools-storage-explorer-blobs) \(英文\)</span><span class="sxs-lookup"><span data-stu-id="7b347-278">[Manage blobs with Storage Explorer](https://docs.microsoft.com/en-us/azure/vs-azure-tools-storage-explorer-blobs)</span></span>
* [<span data-ttu-id="7b347-279">使用 Azure CLI 2.0 hello 與 Azure 儲存體</span><span class="sxs-lookup"><span data-stu-id="7b347-279">Using hello Azure CLI 2.0 with Azure Storage</span></span>](storage-azure-cli.md)
* [<span data-ttu-id="7b347-280">如何 toouse 從 c + + 的 Blob 儲存體</span><span class="sxs-lookup"><span data-stu-id="7b347-280">How toouse Blob storage from C++</span></span>](storage-c-plus-plus-how-to-use-blobs.md)
* [<span data-ttu-id="7b347-281">如何從 Java 的 Blob 儲存體 toouse</span><span class="sxs-lookup"><span data-stu-id="7b347-281">How toouse Blob storage from Java</span></span>](storage-java-how-to-use-blob-storage.md)
* [<span data-ttu-id="7b347-282">如何 toouse Node.js 從 Blob 儲存體</span><span class="sxs-lookup"><span data-stu-id="7b347-282">How toouse Blob storage from Node.js</span></span>](storage-nodejs-how-to-use-blob-storage.md)
* [<span data-ttu-id="7b347-283">如何 toouse 來自 Python 的 Blob 儲存體</span><span class="sxs-lookup"><span data-stu-id="7b347-283">How toouse Blob storage from Python</span></span>](storage-python-how-to-use-blob-storage.md)

### <a name="azure-storage-blog-posts"></a><span data-ttu-id="7b347-284">Azure 儲存體部落格文章：</span><span class="sxs-lookup"><span data-stu-id="7b347-284">Azure Storage blog posts:</span></span>
* <span data-ttu-id="7b347-285">[宣告 AzCopy on Linux 預覽](https://azure.microsoft.com/en-in/blog/announcing-azcopy-on-linux-preview/) \(英文\)</span><span class="sxs-lookup"><span data-stu-id="7b347-285">[Announcing AzCopy on Linux Preview](https://azure.microsoft.com/en-in/blog/announcing-azcopy-on-linux-preview/)</span></span>
* [<span data-ttu-id="7b347-286">Azure 儲存體資料移動文件庫預覽簡介</span><span class="sxs-lookup"><span data-stu-id="7b347-286">Introducing Azure Storage Data Movement Library Preview</span></span>](https://azure.microsoft.com/blog/introducing-azure-storage-data-movement-library-preview-2/)
* [<span data-ttu-id="7b347-287">AzCopy：簡介同步複製和自訂內容類型</span><span class="sxs-lookup"><span data-stu-id="7b347-287">AzCopy: Introducing synchronous copy and customized content type</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2015/01/13/azcopy-introducing-synchronous-copy-and-customized-content-type.aspx)
* [<span data-ttu-id="7b347-288">AzCopy: 宣布正式發行 AzCopy 3.0 和具有資料表和檔案支援的 AzCopy 4.0 預覽版本</span><span class="sxs-lookup"><span data-stu-id="7b347-288">AzCopy: Announcing General Availability of AzCopy 3.0 plus preview release of AzCopy 4.0 with Table and File support</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/10/29/azcopy-announcing-general-availability-of-azcopy-3-0-plus-preview-release-of-azcopy-4-0-with-table-and-file-support.aspx)
* [<span data-ttu-id="7b347-289">AzCopy: 針對大規模複製案例最佳化</span><span class="sxs-lookup"><span data-stu-id="7b347-289">AzCopy: Optimized for Large-Scale Copy Scenarios</span></span>](http://go.microsoft.com/fwlink/?LinkId=507682)
* [<span data-ttu-id="7b347-290">AzCopy: 支援讀取存取異地備援儲存體</span><span class="sxs-lookup"><span data-stu-id="7b347-290">AzCopy: Support for read-access geo-redundant storage</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/04/07/azcopy-support-for-read-access-geo-redundant-account.aspx)
* <span data-ttu-id="7b347-291">[AzCopy：使用可重新啟動模式和 SAS 權杖傳輸資料](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/09/07/azcopy-transfer-data-with-re-startable-mode-and-sas-token.aspx) \(英文\)</span><span class="sxs-lookup"><span data-stu-id="7b347-291">[AzCopy: Transfer data with restartable mode and SAS token](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/09/07/azcopy-transfer-data-with-re-startable-mode-and-sas-token.aspx)</span></span>
* [<span data-ttu-id="7b347-292">AzCopy: 使用跨帳戶複製 Blob</span><span class="sxs-lookup"><span data-stu-id="7b347-292">AzCopy: Using cross-account Copy Blob</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/04/01/azcopy-using-cross-account-copy-blob.aspx)
* [<span data-ttu-id="7b347-293">AzCopy: 上傳/下載 Azure Blob 的檔案</span><span class="sxs-lookup"><span data-stu-id="7b347-293">AzCopy: Uploading/downloading files for Azure Blobs</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/12/03/azcopy-uploading-downloading-files-for-windows-azure-blobs.aspx)

