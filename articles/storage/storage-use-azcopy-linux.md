---
title: "使用 AzCopy on Linux 複製或移動資料到 Azure 儲存體 | Microsoft Docs"
description: "使用 AzCopy on Linux 公用程式來從 Blob 和檔案內容移動或來回複製資料。 從本機檔案複製資料到 Azure 儲存體，或在儲存體帳戶內或之間複製資料。 輕鬆地將資料移轉至 Azure 儲存體。"
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
ms.openlocfilehash: d17f63dcee590529756d48d699f78b3fb30f973c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="transfer-data-with-azcopy-on-linux"></a><span data-ttu-id="a322b-105">使用 AzCopy on Linux 傳送資料</span><span class="sxs-lookup"><span data-stu-id="a322b-105">Transfer data with AzCopy on Linux</span></span>
<span data-ttu-id="a322b-106">AzCopy on Linux 是個命令列公用程式，專為使用簡單命令高效率地將資料複製到和複製出 Microsoft Azure Blob 和檔案儲存體所設計。</span><span class="sxs-lookup"><span data-stu-id="a322b-106">AzCopy on Linux is a command-line utility designed for copying data to and from Microsoft Azure Blob and File storage using simple commands with optimal performance.</span></span> <span data-ttu-id="a322b-107">您可以從儲存體帳戶內或是在儲存體帳戶之間，從一個物件複製資料到另一個物件。</span><span class="sxs-lookup"><span data-stu-id="a322b-107">You can copy data from one object to another within your storage account, or between storage accounts.</span></span>

<span data-ttu-id="a322b-108">有兩個 AzCopy 版本可供您下載。</span><span class="sxs-lookup"><span data-stu-id="a322b-108">There are two versions of AzCopy that you can download.</span></span> <span data-ttu-id="a322b-109">AzCopy on Linux 內建有 .NET Core Framework，其以提供 POSIX 樣式命令列選項的 Linux 平台為目標。</span><span class="sxs-lookup"><span data-stu-id="a322b-109">AzCopy on Linux is built with .NET Core Framework, which targets Linux platforms offering POSIX style command-line options.</span></span> <span data-ttu-id="a322b-110">[AzCopy on Windows](storage-use-azcopy.md) 內建有 .NET Framework，並且提供 Windows 樣式的命令列選項。</span><span class="sxs-lookup"><span data-stu-id="a322b-110">[AzCopy on Windows](storage-use-azcopy.md) is built with .NET Framework, and offers Windows style command-line options.</span></span> <span data-ttu-id="a322b-111">本文涵蓋之內容包括 AzCopy on Linux。</span><span class="sxs-lookup"><span data-stu-id="a322b-111">This article covers AzCopy on Linux.</span></span>

## <a name="download-and-install-azcopy"></a><span data-ttu-id="a322b-112">下載並安裝 AzCopy</span><span class="sxs-lookup"><span data-stu-id="a322b-112">Download and install AzCopy</span></span>
### <a name="installation-on-linux"></a><span data-ttu-id="a322b-113">在 Linux 上安裝</span><span class="sxs-lookup"><span data-stu-id="a322b-113">Installation on Linux</span></span>

<span data-ttu-id="a322b-114">AzCopy on Linux 需要在平台上有 .NET Core framework。</span><span class="sxs-lookup"><span data-stu-id="a322b-114">AzCopy on Linux requires .NET Core framework on the platform.</span></span> <span data-ttu-id="a322b-115">請參閱 [.NET Core](https://www.microsoft.com/net/core#linuxubuntu) \(英文\) 頁面上的安裝指示。</span><span class="sxs-lookup"><span data-stu-id="a322b-115">See the installation instructions on the [.NET Core](https://www.microsoft.com/net/core#linuxubuntu) page.</span></span>

<span data-ttu-id="a322b-116">例如，讓我們在 Ubuntu 16.10 上安裝 .NET Core。</span><span class="sxs-lookup"><span data-stu-id="a322b-116">As an example, let's install .NET Core on Ubuntu 16.10.</span></span> <span data-ttu-id="a322b-117">如需最新安裝指南，請造訪 [.NET Core on Linux](https://www.microsoft.com/net/core#linuxubuntu) \(英文\) 安裝頁面。</span><span class="sxs-lookup"><span data-stu-id="a322b-117">For the latest installation guide, visit [.NET Core on Linux](https://www.microsoft.com/net/core#linuxubuntu) installation page.</span></span>


```bash
sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ yakkety main" > /etc/apt/sources.list.d/dotnetdev.list' 
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893
sudo apt-get update
sudo apt-get install dotnet-dev-1.0.3
```

<span data-ttu-id="a322b-118">安裝 .NET Core 之後，下載並安裝 AzCopy。</span><span class="sxs-lookup"><span data-stu-id="a322b-118">Once you have installed .NET Core, download and install AzCopy.</span></span>

```bash
wget -O azcopy.tar.gz https://aka.ms/downloadazcopyprlinux
tar -xf azcopy.tar.gz
sudo ./install.sh
```

<span data-ttu-id="a322b-119">安裝 AzCopy on Linux 之後，您便可移除解壓縮後的檔案。</span><span class="sxs-lookup"><span data-stu-id="a322b-119">You can remove the extracted files once AzCopy on Linux is installed.</span></span> <span data-ttu-id="a322b-120">或者，如果您沒有 superuser 權限，也可以使用解壓縮資料夾中的 shell 指令碼「azcopy」執行 AzCopy。</span><span class="sxs-lookup"><span data-stu-id="a322b-120">Alternatively if you do not have superuser privileges, you can also run AzCopy using the shell script 'azcopy' in the extracted folder.</span></span> 

### <a name="alternative-installation-on-ubuntu"></a><span data-ttu-id="a322b-121">Ubuntu 上的替代安裝</span><span class="sxs-lookup"><span data-stu-id="a322b-121">Alternative Installation on Ubuntu</span></span>

<span data-ttu-id="a322b-122">**Ubuntu 14.04**</span><span class="sxs-lookup"><span data-stu-id="a322b-122">**Ubuntu 14.04**</span></span>

<span data-ttu-id="a322b-123">新增適用於 .Net Core 的 apt 來源：</span><span class="sxs-lookup"><span data-stu-id="a322b-123">Add apt source for .Net Core:</span></span>

```bash
sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ trusty main" > /etc/apt/sources.list.d/dotnetdev.list' 
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893
```

<span data-ttu-id="a322b-124">新增適用於 Microsoft Linux 產品存放庫的 apt 來源並安裝 AzCopy：</span><span class="sxs-lookup"><span data-stu-id="a322b-124">Add apt source for Microsoft Linux product repository and install AzCopy:</span></span>

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

<span data-ttu-id="a322b-125">**Ubuntu 16.04**</span><span class="sxs-lookup"><span data-stu-id="a322b-125">**Ubuntu 16.04**</span></span>

<span data-ttu-id="a322b-126">新增適用於 .Net Core 的 apt 來源：</span><span class="sxs-lookup"><span data-stu-id="a322b-126">Add apt source for .Net Core:</span></span>

```bash
sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ xenial main" > /etc/apt/sources.list.d/dotnetdev.list' 
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893
```

<span data-ttu-id="a322b-127">新增適用於 Microsoft Linux 產品存放庫的 apt 來源並安裝 AzCopy：</span><span class="sxs-lookup"><span data-stu-id="a322b-127">Add apt source for Microsoft Linux product repository and install AzCopy:</span></span>

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

<span data-ttu-id="a322b-128">**Ubuntu 16.10**</span><span class="sxs-lookup"><span data-stu-id="a322b-128">**Ubuntu 16.10**</span></span>

<span data-ttu-id="a322b-129">新增適用於 .Net Core 的 apt 來源：</span><span class="sxs-lookup"><span data-stu-id="a322b-129">Add apt source for .Net Core:</span></span>

```bash
sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ yakkety main" > /etc/apt/sources.list.d/dotnetdev.list' 
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893
```

<span data-ttu-id="a322b-130">新增適用於 Microsoft Linux 產品存放庫的 apt 來源並安裝 AzCopy：</span><span class="sxs-lookup"><span data-stu-id="a322b-130">Add apt source for Microsoft Linux product repository and install AzCopy:</span></span>

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

## <a name="writing-your-first-azcopy-command"></a><span data-ttu-id="a322b-131">撰寫第一個 AzCopy 命令</span><span class="sxs-lookup"><span data-stu-id="a322b-131">Writing your first AzCopy command</span></span>
<span data-ttu-id="a322b-132">AzCopy 命令的基本語法是：</span><span class="sxs-lookup"><span data-stu-id="a322b-132">The basic syntax for AzCopy commands is:</span></span>

```azcopy
azcopy --source <source> --destination <destination> [Options]
```

<span data-ttu-id="a322b-133">下列範例會示範各種不同的 Microsoft Azure Blob 和檔案資料複製案例。</span><span class="sxs-lookup"><span data-stu-id="a322b-133">The following examples demonstrate various scenarios for copying data to and from Microsoft Azure Blobs and Files.</span></span> <span data-ttu-id="a322b-134">如需每個範例中所使用參數的詳細說明，請參閱 `azcopy --help`功能表。</span><span class="sxs-lookup"><span data-stu-id="a322b-134">Refer to the `azcopy --help` menu for a detailed explanation of the parameters used in each sample.</span></span>

## <a name="blob-download"></a><span data-ttu-id="a322b-135">Blob：下載</span><span class="sxs-lookup"><span data-stu-id="a322b-135">Blob: Download</span></span>
### <a name="download-single-blob"></a><span data-ttu-id="a322b-136">下載單一 Blob</span><span class="sxs-lookup"><span data-stu-id="a322b-136">Download single blob</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --include "abc.txt"
```

<span data-ttu-id="a322b-137">如果資料夾 `/mnt/myfiles` 不存在，AzCopy 會加以建立並將 `abc.txt ` 下載到新資料夾。</span><span class="sxs-lookup"><span data-stu-id="a322b-137">If the folder `/mnt/myfiles` does not exist, AzCopy creates it and downloads `abc.txt ` into the new folder.</span></span>

### <a name="download-single-blob-from-secondary-region"></a><span data-ttu-id="a322b-138">從次要地區下載單一 Blob</span><span class="sxs-lookup"><span data-stu-id="a322b-138">Download single blob from secondary region</span></span>

```azcopy
azcopy \
    --source https://myaccount-secondary.blob.core.windows.net/mynewcontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --include "abc.txt"
```

<span data-ttu-id="a322b-139">請注意，您必須啟用讀取權限異地備援儲存體。</span><span class="sxs-lookup"><span data-stu-id="a322b-139">Note that you must have read-access geo-redundant storage enabled.</span></span>

### <a name="download-all-blobs"></a><span data-ttu-id="a322b-140">下載所有 Blob</span><span class="sxs-lookup"><span data-stu-id="a322b-140">Download all blobs</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --recursive
```

<span data-ttu-id="a322b-141">假設下列 Blob 位於指定容器中：</span><span class="sxs-lookup"><span data-stu-id="a322b-141">Assume the following blobs reside in the specified container:</span></span>  

```
abc.txt
abc1.txt
abc2.txt
vd1/a.txt
vd1/abcd.txt
```

<span data-ttu-id="a322b-142">下載作業之後，目錄 `/mnt/myfiles` 會包含下列檔案：</span><span class="sxs-lookup"><span data-stu-id="a322b-142">After the download operation, the directory `/mnt/myfiles` includes the following files:</span></span>

```
/mnt/myfiles/abc.txt
/mnt/myfiles/abc1.txt
/mnt/myfiles/abc2.txt
/mnt/myfiles/vd1/a.txt
/mnt/myfiles/vd1/abcd.txt
```

<span data-ttu-id="a322b-143">如果您未指定選項 `--recursive`，則不會下載任何 Blob。</span><span class="sxs-lookup"><span data-stu-id="a322b-143">If you do not specify option `--recursive`, no blob will be downloaded.</span></span>

### <a name="download-blobs-with-specified-prefix"></a><span data-ttu-id="a322b-144">下載具有指定首碼的 Blob</span><span class="sxs-lookup"><span data-stu-id="a322b-144">Download blobs with specified prefix</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --include "a" \
    --recursive
```

<span data-ttu-id="a322b-145">假設下列 Blob 位於指定容器中。</span><span class="sxs-lookup"><span data-stu-id="a322b-145">Assume the following blobs reside in the specified container.</span></span> <span data-ttu-id="a322b-146">會下載所有以首碼 `a` 開頭的 Blob。</span><span class="sxs-lookup"><span data-stu-id="a322b-146">All blobs beginning with the prefix `a` are downloaded.</span></span>

```
abc.txt
abc1.txt
abc2.txt
xyz.txt
vd1\a.txt
vd1\abcd.txt
```

<span data-ttu-id="a322b-147">下載作業之後，資料夾 `/mnt/myfiles` 會包含下列檔案：</span><span class="sxs-lookup"><span data-stu-id="a322b-147">After the download operation, the folder `/mnt/myfiles` includes the following files:</span></span>

```
/mnt/myfiles/abc.txt
/mnt/myfiles/abc1.txt
/mnt/myfiles/abc2.txt
```

<span data-ttu-id="a322b-148">首碼會套用到虛擬目錄，虛擬目錄會構成第一部分的 Blob 名稱。</span><span class="sxs-lookup"><span data-stu-id="a322b-148">The prefix applies to the virtual directory, which forms the first part of the blob name.</span></span> <span data-ttu-id="a322b-149">在上述範例中，虛擬目錄不符合指定的首碼，所以不會下載任何 Blob。</span><span class="sxs-lookup"><span data-stu-id="a322b-149">In the example shown above, the virtual directory does not match the specified prefix, so no blob is downloaded.</span></span> <span data-ttu-id="a322b-150">此外，如果未指定選項 `--recursive` ，則 AzCopy 不會下載任何 Blob。</span><span class="sxs-lookup"><span data-stu-id="a322b-150">In addition, if the option `--recursive` is not specified, AzCopy does not download any blobs.</span></span>

### <a name="set-the-last-modified-time-of-exported-files-to-be-same-as-the-source-blobs"></a><span data-ttu-id="a322b-151">將匯出檔案的最後修改時間設定為與來源 Blob 相同的最後修改時間</span><span class="sxs-lookup"><span data-stu-id="a322b-151">Set the last-modified time of exported files to be same as the source blobs</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination "/mnt/myfiles" \
    --source-key <key> \
    --preserve-last-modified-time
```

<span data-ttu-id="a322b-152">您也可以根據其最後修改時間，將 Blob 從下載作業中排除。</span><span class="sxs-lookup"><span data-stu-id="a322b-152">You can also exclude blobs from the download operation based on their last-modified time.</span></span> <span data-ttu-id="a322b-153">例如，如果您想要排除最後修改時間比目的地檔案還要新或相同的 Blob，請新增 `--exclude-newer` 選項：</span><span class="sxs-lookup"><span data-stu-id="a322b-153">For example, if you want to exclude blobs whose last modified time is the same or newer than the destination file, add the `--exclude-newer` option:</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --preserve-last-modified-time \
    --exclude-newer
```

<span data-ttu-id="a322b-154">或者，如果您想要排除最後修改時間比目的地檔案還要舊或相同的 Blob，請新增 `--exclude-older` 選項：</span><span class="sxs-lookup"><span data-stu-id="a322b-154">Or if you want to exclude blobs whose last modified time is the same or older than the destination file, add the `--exclude-older` option:</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --preserve-last-modified-time \
    --exclude-older
```

## <a name="blob-upload"></a><span data-ttu-id="a322b-155">Blob：上傳</span><span class="sxs-lookup"><span data-stu-id="a322b-155">Blob: Upload</span></span>
### <a name="upload-single-file"></a><span data-ttu-id="a322b-156">上傳單一檔案</span><span class="sxs-lookup"><span data-stu-id="a322b-156">Upload single file</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --include "abc.txt"
```

<span data-ttu-id="a322b-157">如果指定的目的地容器不存在，則 AzCopy 會建立此容器並將檔案上傳至該容器中。</span><span class="sxs-lookup"><span data-stu-id="a322b-157">If the specified destination container does not exist, AzCopy creates it and uploads the file into it.</span></span>

### <a name="upload-single-file-to-virtual-directory"></a><span data-ttu-id="a322b-158">上傳單一檔案到虛擬目錄</span><span class="sxs-lookup"><span data-stu-id="a322b-158">Upload single file to virtual directory</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --include "abc.txt"
```

<span data-ttu-id="a322b-159">如果指定的虛擬目錄不存在，則 AzCopy 會上傳檔案並在 Blob 名稱中加上此虛擬目錄 (例如，上述範例中的 `vd/abc.txt`)。</span><span class="sxs-lookup"><span data-stu-id="a322b-159">If the specified virtual directory does not exist, AzCopy uploads the file to include the virtual directory in the blob name (*e.g.*, `vd/abc.txt` in the example above).</span></span>

### <a name="upload-all-files"></a><span data-ttu-id="a322b-160">上傳所有檔案</span><span class="sxs-lookup"><span data-stu-id="a322b-160">Upload all files</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --recursive
```

<span data-ttu-id="a322b-161">指定 `--recursive` 選項以遞迴方式將指定目錄的內容上傳到 Blob 儲存體，這表示也會上傳所有的子資料夾及其檔案。</span><span class="sxs-lookup"><span data-stu-id="a322b-161">Specifying option `--recursive` uploads the contents of the specified directory to Blob storage recursively, meaning that all subfolders and their files are uploaded as well.</span></span> <span data-ttu-id="a322b-162">例如，假設下列檔案位於 `/mnt/myfiles`資料夾內：</span><span class="sxs-lookup"><span data-stu-id="a322b-162">For instance, assume the following files reside in folder `/mnt/myfiles`:</span></span>

```
/mnt/myfiles/abc.txt
/mnt/myfiles/abc1.txt
/mnt/myfiles/abc2.txt
/mnt/myfiles/subfolder/a.txt
/mnt/myfiles/subfolder/abcd.txt
```

<span data-ttu-id="a322b-163">上傳作業之後，容器會包含下列檔案：</span><span class="sxs-lookup"><span data-stu-id="a322b-163">After the upload operation, the container includes the following files:</span></span>

```
abc.txt
abc1.txt
abc2.txt
subfolder/a.txt
subfolder/abcd.txt
```

<span data-ttu-id="a322b-164">未指定選項 `--recursive` 時，只會上傳下列三個檔案：</span><span class="sxs-lookup"><span data-stu-id="a322b-164">When the option `--recursive` is not specified, only the following three files are uploaded:</span></span>

```
abc.txt
abc1.txt
abc2.txt
```

### <a name="upload-files-matching-specified-pattern"></a><span data-ttu-id="a322b-165">上傳符合指定模式的檔案</span><span class="sxs-lookup"><span data-stu-id="a322b-165">Upload files matching specified pattern</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --include "a*" \
    --recursive
```

<span data-ttu-id="a322b-166">假設下列檔案位於 `/mnt/myfiles`資料夾內：</span><span class="sxs-lookup"><span data-stu-id="a322b-166">Assume the following files reside in folder `/mnt/myfiles`:</span></span>

```
/mnt/myfiles/abc.txt
/mnt/myfiles/abc1.txt
/mnt/myfiles/abc2.txt
/mnt/myfiles/xyz.txt
/mnt/myfiles/subfolder/a.txt
/mnt/myfiles/subfolder/abcd.txt
```

<span data-ttu-id="a322b-167">上傳作業之後，容器會包含下列檔案：</span><span class="sxs-lookup"><span data-stu-id="a322b-167">After the upload operation, the container includes the following files:</span></span>

```
abc.txt
abc1.txt
abc2.txt
subfolder/a.txt
subfolder/abcd.txt
```

<span data-ttu-id="a322b-168">未指定選項 `--recursive` 時，AzCopy 會跳過子目錄中的檔案：</span><span class="sxs-lookup"><span data-stu-id="a322b-168">When the option `--recursive` is not specified, AzCopy skips files that are in sub-directories:</span></span>

```
abc.txt
abc1.txt
abc2.txt
```

### <a name="specify-the-mime-content-type-of-a-destination-blob"></a><span data-ttu-id="a322b-169">指定目的地 blob 的 MIME 內容類型</span><span class="sxs-lookup"><span data-stu-id="a322b-169">Specify the MIME content type of a destination blob</span></span>
<span data-ttu-id="a322b-170">根據預設，AzCopy 會將目的地 blob 的內容類型設定為 `application/octet-stream`。</span><span class="sxs-lookup"><span data-stu-id="a322b-170">By default, AzCopy sets the content type of a destination blob to `application/octet-stream`.</span></span> <span data-ttu-id="a322b-171">但是，您可以透過 `--set-content-type [content-type]` 選項明確指定內容類型。</span><span class="sxs-lookup"><span data-stu-id="a322b-171">However, you can explicitly specify the content type via the option `--set-content-type [content-type]`.</span></span> <span data-ttu-id="a322b-172">此語法會在上傳作業中設定所有 Blob 的內容類型。</span><span class="sxs-lookup"><span data-stu-id="a322b-172">This syntax sets the content type for all blobs in an upload operation.</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/myContainer/ \
    --dest-key <key> \
    --include "ab" \
    --set-content-type "video/mp4"
```

<span data-ttu-id="a322b-173">若已指定選項 `--set-content-type` 但未指定任何值，則 AzCopy 會根據副檔名來設定每個 blob 或檔案的內容類型。</span><span class="sxs-lookup"><span data-stu-id="a322b-173">If the option `--set-content-type` is specified without a value, then AzCopy sets each blob or file's content type according to its file extension.</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/myContainer/ \
    --dest-key <key> \
    --include "ab" \
    --set-content-type
```

## <a name="blob-copy"></a><span data-ttu-id="a322b-174">Blob：複製</span><span class="sxs-lookup"><span data-stu-id="a322b-174">Blob: Copy</span></span>
### <a name="copy-single-blob-within-storage-account"></a><span data-ttu-id="a322b-175">複製儲存體帳戶內的單一 Blob</span><span class="sxs-lookup"><span data-stu-id="a322b-175">Copy single blob within Storage account</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer1 \
    --destination https://myaccount.blob.core.windows.net/mycontainer2 \
    --source-key <key> \
    --dest-key <key> \
    --include "abc.txt"
```

<span data-ttu-id="a322b-176">當您未以 --sync-copy 選項複製 Blob 時，系統會執行[伺服器端複製](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) \(英文\) 作業。</span><span class="sxs-lookup"><span data-stu-id="a322b-176">When you copy a blob without --sync-copy option, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="copy-single-blob-across-storage-accounts"></a><span data-ttu-id="a322b-177">跨儲存體帳戶複製單一 Blob</span><span class="sxs-lookup"><span data-stu-id="a322b-177">Copy single blob across Storage accounts</span></span>

```azcopy
azcopy \
    --source https://sourceaccount.blob.core.windows.net/mycontainer1 \
    --destination https://destaccount.blob.core.windows.net/mycontainer2 \
    --source-key <key1> \
    --dest-key <key2> \
    --include "abc.txt"
```

<span data-ttu-id="a322b-178">當您未以 --sync-copy 選項複製 Blob 時，系統會執行[伺服器端複製](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) \(英文\) 作業。</span><span class="sxs-lookup"><span data-stu-id="a322b-178">When you copy a blob without --sync-copy option, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="copy-single-blob-from-secondary-region-to-primary-region"></a><span data-ttu-id="a322b-179">將單一 Blob 從次要地區複製到主要區域</span><span class="sxs-lookup"><span data-stu-id="a322b-179">Copy single blob from secondary region to primary region</span></span>

```azcopy
azcopy \
    --source https://myaccount1-secondary.blob.core.windows.net/mynewcontainer1 \
    --destination https://myaccount2.blob.core.windows.net/mynewcontainer2 \
    --source-key <key1> \
    --dest-key <key2> \
    --include "abc.txt"
```

<span data-ttu-id="a322b-180">請注意，您必須啟用讀取權限異地備援儲存體。</span><span class="sxs-lookup"><span data-stu-id="a322b-180">Note that you must have read-access geo-redundant storage enabled.</span></span>

### <a name="copy-single-blob-and-its-snapshots-across-storage-accounts"></a><span data-ttu-id="a322b-181">跨儲存體帳戶複製單一 Blob 及其快照</span><span class="sxs-lookup"><span data-stu-id="a322b-181">Copy single blob and its snapshots across Storage accounts</span></span>

```azcopy
azcopy \
    --source https://sourceaccount.blob.core.windows.net/mycontainer1 \
    --destination https://destaccount.blob.core.windows.net/mycontainer2 \
    --source-key <key1> \
    --dest-key <key2> \
    --include "abc.txt" \
    --include-snapshot
```

<span data-ttu-id="a322b-182">複製作業之後，目標容器會包含 Blob 及其快照集。</span><span class="sxs-lookup"><span data-stu-id="a322b-182">After the copy operation, the target container includes the blob and its snapshots.</span></span> <span data-ttu-id="a322b-183">容器包含下列 Blob 及其快照集：</span><span class="sxs-lookup"><span data-stu-id="a322b-183">The container includes the following blob and its snapshots:</span></span>

```
abc.txt
abc (2013-02-25 080757).txt
abc (2014-02-21 150331).txt
```

### <a name="synchronously-copy-blobs-across-storage-accounts"></a><span data-ttu-id="a322b-184">以同步方式跨儲存體帳戶複製 Blob</span><span class="sxs-lookup"><span data-stu-id="a322b-184">Synchronously copy blobs across Storage accounts</span></span>
<span data-ttu-id="a322b-185">根據預設，AzCopy 會以非同步方式在兩個儲存體端點之間複製資料。</span><span class="sxs-lookup"><span data-stu-id="a322b-185">AzCopy by default copies data between two storage endpoints asynchronously.</span></span> <span data-ttu-id="a322b-186">因此，複製作業會在背景中使用並未以 SLA 規範應以多快速度複製 Blob 的備用頻寬能力執行。</span><span class="sxs-lookup"><span data-stu-id="a322b-186">Therefore, the copy operation runs in the background using spare bandwidth capacity that has no SLA in terms of how fast a blob is copied.</span></span> 

<span data-ttu-id="a322b-187">`--sync-copy` 選項可確保複製作業達到一致的速度。</span><span class="sxs-lookup"><span data-stu-id="a322b-187">The `--sync-copy` option ensures that the copy operation gets consistent speed.</span></span> <span data-ttu-id="a322b-188">AzCopy 執行同步複製的方式是先將要複製的 blob，從指定的來源下載到本機記憶體，再上傳至 Blob 儲存體目的地。</span><span class="sxs-lookup"><span data-stu-id="a322b-188">AzCopy performs the synchronous copy by downloading the blobs to copy from the specified source to local memory, and then uploading them to the Blob storage destination.</span></span>

```azcopy
azcopy \
    --source https://myaccount1.blob.core.windows.net/myContainer/ \
    --destination https://myaccount2.blob.core.windows.net/myContainer/ \
    --source-key <key1> \
    --dest-key <key2> \
    --include "ab" \
    --sync-copy
```

<span data-ttu-id="a322b-189">相較於非同步複製，`--sync-copy` 可能會產生額外的輸出成本。</span><span class="sxs-lookup"><span data-stu-id="a322b-189">`--sync-copy` might generate additional egress cost compared to asynchronous copy.</span></span> <span data-ttu-id="a322b-190">建議的方法是在與您來源儲存體帳戶位於同一區域的 Azure VM 中使用這個選項，以避免產生輸出成本。</span><span class="sxs-lookup"><span data-stu-id="a322b-190">The recommended approach is to use this option in an Azure VM, that is in the same region as your source storage account to avoid egress cost.</span></span>

## <a name="file-download"></a><span data-ttu-id="a322b-191">檔案：下載</span><span class="sxs-lookup"><span data-stu-id="a322b-191">File: Download</span></span>
### <a name="download-single-file"></a><span data-ttu-id="a322b-192">下載單一檔案</span><span class="sxs-lookup"><span data-stu-id="a322b-192">Download single file</span></span>

```azcopy
azcopy \
    --source https://myaccount.file.core.windows.net/myfileshare/myfolder1/ \
    --destination /mnt/myfiles \
    --source-key <key> \
    --include "abc.txt"
```

<span data-ttu-id="a322b-193">如果指定的來源是 Azure 檔案共用，則您必須指定確切檔案名稱 (例如，`abc.txt`) 以下載單一檔案，或指定 `--recursive` 選項以遞迴方式下載共用中的所有檔案。</span><span class="sxs-lookup"><span data-stu-id="a322b-193">If the specified source is an Azure file share, then you must either specify the exact file name, (*e.g.* `abc.txt`) to download a single file, or specify option `--recursive` to download all files in the share recursively.</span></span> <span data-ttu-id="a322b-194">嘗試同時指定檔案模式和 `--recursive` 選項會造成錯誤。</span><span class="sxs-lookup"><span data-stu-id="a322b-194">Attempting to specify both a file pattern and option `--recursive` together results in an error.</span></span>

### <a name="download-all-files"></a><span data-ttu-id="a322b-195">下載所有檔案</span><span class="sxs-lookup"><span data-stu-id="a322b-195">Download all files</span></span>

```azcopy
azcopy \
    --source https://myaccount.file.core.windows.net/myfileshare/ \
    --destination /mnt/myfiles \
    --source-key <key> \
    --recursive
```

<span data-ttu-id="a322b-196">請注意，並不會下載任何空白資料夾。</span><span class="sxs-lookup"><span data-stu-id="a322b-196">Note that any empty folders are not downloaded.</span></span>

## <a name="file-upload"></a><span data-ttu-id="a322b-197">檔案：上傳</span><span class="sxs-lookup"><span data-stu-id="a322b-197">File: Upload</span></span>
### <a name="upload-single-file"></a><span data-ttu-id="a322b-198">上傳單一檔案</span><span class="sxs-lookup"><span data-stu-id="a322b-198">Upload single file</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.file.core.windows.net/myfileshare/ \
    --dest-key <key> \
    --include abc.txt
```

### <a name="upload-all-files"></a><span data-ttu-id="a322b-199">上傳所有檔案</span><span class="sxs-lookup"><span data-stu-id="a322b-199">Upload all files</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.file.core.windows.net/myfileshare/ \
    --dest-key <key> \
    --recursive
```

<span data-ttu-id="a322b-200">請注意，並不會上傳任何空白資料夾。</span><span class="sxs-lookup"><span data-stu-id="a322b-200">Note that any empty folders are not uploaded.</span></span>

### <a name="upload-files-matching-specified-pattern"></a><span data-ttu-id="a322b-201">上傳符合指定模式的檔案</span><span class="sxs-lookup"><span data-stu-id="a322b-201">Upload files matching specified pattern</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.file.core.windows.net/myfileshare/ \
    --dest-key <key> \
    --include "ab*" \
    --recursive
```

## <a name="file-copy"></a><span data-ttu-id="a322b-202">檔案：複製</span><span class="sxs-lookup"><span data-stu-id="a322b-202">File: Copy</span></span>
### <a name="copy-across-file-shares"></a><span data-ttu-id="a322b-203">跨檔案共用複製</span><span class="sxs-lookup"><span data-stu-id="a322b-203">Copy across file shares</span></span>

```azcopy
azcopy \
    --source https://myaccount1.file.core.windows.net/myfileshare1/ \
    --destination https://myaccount2.file.core.windows.net/myfileshare2/ \
    --source-key <key1> \
    --dest-key <key2> \
    --recursive
```
<span data-ttu-id="a322b-204">當您跨檔案共用複製檔案時，系統會執行[伺服器端複製](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx)作業。</span><span class="sxs-lookup"><span data-stu-id="a322b-204">When you copy a file across file shares, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="copy-from-file-share-to-blob"></a><span data-ttu-id="a322b-205">從檔案共用複製到 Blob</span><span class="sxs-lookup"><span data-stu-id="a322b-205">Copy from file share to blob</span></span>

```azcopy
azcopy \ 
    --source https://myaccount1.file.core.windows.net/myfileshare/ \
    --destination https://myaccount2.blob.core.windows.net/mycontainer/ \
    --source-key <key1> \
    --dest-key <key2> \
    --recursive
```
<span data-ttu-id="a322b-206">當您將檔案從檔案共用複製到 Blob 時，系統會執行[伺服器端複製](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx)作業。</span><span class="sxs-lookup"><span data-stu-id="a322b-206">When you copy a file from file share to blob, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="copy-from-blob-to-file-share"></a><span data-ttu-id="a322b-207">從 Blob 複製到檔案共用</span><span class="sxs-lookup"><span data-stu-id="a322b-207">Copy from blob to file share</span></span>

```azcopy
azcopy \
    --source https://myaccount1.blob.core.windows.net/mycontainer/ \
    --destination https://myaccount2.file.core.windows.net/myfileshare/ \
    --source-key <key1> \
    --dest-key <key2> \
    --recursive
```
<span data-ttu-id="a322b-208">當您將檔案從 Blob 複製到檔案共用時，系統會執行[伺服器端複製](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx)作業。</span><span class="sxs-lookup"><span data-stu-id="a322b-208">When you copy a file from blob to file share, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="synchronously-copy-files"></a><span data-ttu-id="a322b-209">以同步方式複製檔案</span><span class="sxs-lookup"><span data-stu-id="a322b-209">Synchronously copy files</span></span>
<span data-ttu-id="a322b-210">您可以指定 `--sync-copy` 選項，以同步方式從檔案儲存體複製資料到檔案儲存體、從檔案儲存體複製資料到 Blob 儲存體，以及從 Blob 儲存體複製資料到檔案儲存體。</span><span class="sxs-lookup"><span data-stu-id="a322b-210">You can specify the `--sync-copy` option to copy data from File Storage to File Storage, from File Storage to Blob Storage and from Blob Storage to File Storage synchronously.</span></span> <span data-ttu-id="a322b-211">AzCopy 會將來源資料下載至本機記憶體，然後上傳到目的地，來執行此項作業。</span><span class="sxs-lookup"><span data-stu-id="a322b-211">AzCopy runs this operation by downloading the source data to local memory, and then uploading it to destination.</span></span> <span data-ttu-id="a322b-212">在此情況下，會產生標準輸出成本。</span><span class="sxs-lookup"><span data-stu-id="a322b-212">In this case, standard egress cost applies.</span></span>

```azcopy
azcopy \
    --source https://myaccount1.file.core.windows.net/myfileshare1/ \
    --destination https://myaccount2.file.core.windows.net/myfileshare2/ \
    --source-key <key1> \
    --dest-key <key2> \
    --recursive \
    --sync-copy
```

<span data-ttu-id="a322b-213">從檔案儲存體複製到 Blob 儲存體時，預設的 Blob 類型是區塊 Blob，使用者可以指定 `/BlobType:page` 選項來變更目的地 Blob 類型。</span><span class="sxs-lookup"><span data-stu-id="a322b-213">When copying from File Storage to Blob Storage, the default blob type is block blob, user can specify option `/BlobType:page` to change the destination blob type.</span></span>

<span data-ttu-id="a322b-214">請注意，相較於非同步複製，`--sync-copy` 可能會產生額外的輸出成本。</span><span class="sxs-lookup"><span data-stu-id="a322b-214">Note that `--sync-copy` might generate additional egress cost comparing to asynchronous copy.</span></span> <span data-ttu-id="a322b-215">建議的方法是在與您來源儲存體帳戶位於同一區域的 Azure VM 中使用這個選項，以避免產生輸出成本。</span><span class="sxs-lookup"><span data-stu-id="a322b-215">The recommended approach is to use this option in an Azure VM, that is in the same region as your source storage account to avoid egress cost.</span></span>

## <a name="other-azcopy-features"></a><span data-ttu-id="a322b-216">其他 AzCopy 功能</span><span class="sxs-lookup"><span data-stu-id="a322b-216">Other AzCopy features</span></span>
### <a name="only-copy-data-that-doesnt-exist-in-the-destination"></a><span data-ttu-id="a322b-217">只複製目的地中沒有的資料</span><span class="sxs-lookup"><span data-stu-id="a322b-217">Only copy data that doesn't exist in the destination</span></span>
<span data-ttu-id="a322b-218">`--exclude-older` 和 `--exclude-newer` 參數分別可讓您在複製作業中排除較舊或較新的來源資源。</span><span class="sxs-lookup"><span data-stu-id="a322b-218">The `--exclude-older` and `--exclude-newer` parameters allow you to exclude older or newer source resources from being copied, respectively.</span></span> <span data-ttu-id="a322b-219">如果您只想複製目的地中沒有的來源資源，則可以在 AzCopy 命令中同時指定這兩個參數：</span><span class="sxs-lookup"><span data-stu-id="a322b-219">If you only want to copy source resources that don't exist in the destination, you can specify both parameters in the AzCopy command:</span></span>

    --source http://myaccount.blob.core.windows.net/mycontainer --destination /mnt/myfiles --source-key <sourcekey> --recursive --exclude-older --exclude-newer

    --source /mnt/myfiles --destination http://myaccount.file.core.windows.net/myfileshare --dest-key <destkey> --recursive --exclude-older --exclude-newer

    --source http://myaccount.blob.core.windows.net/mycontainer --destination http://myaccount.blob.core.windows.net/mycontainer1 --source-key <sourcekey> --dest-key <destkey> --recursive --exclude-older --exclude-newer

### <a name="use-a-configuration-file-to-specify-command-line-parameters"></a><span data-ttu-id="a322b-220">使用組態檔指定命令列參數</span><span class="sxs-lookup"><span data-stu-id="a322b-220">Use a configuration file to specify command-line parameters</span></span>

```azcopy
azcopy --config-file "azcopy-config.ini"
```

<span data-ttu-id="a322b-221">您可以在組態檔中包含任何 AzCopy 命令列參數。</span><span class="sxs-lookup"><span data-stu-id="a322b-221">You can include any AzCopy command-line parameters in a configuration file.</span></span> <span data-ttu-id="a322b-222">AzCopy 處理檔案中的參數，就好像在命令列上指定這些參數一様，執行使用檔案內容的直接取代。</span><span class="sxs-lookup"><span data-stu-id="a322b-222">AzCopy processes the parameters in the file as if they had been specified on the command line, performing a direct substitution with the contents of the file.</span></span>

<span data-ttu-id="a322b-223">假設名為 `copyoperation` 且包含下列資料行的組態檔。</span><span class="sxs-lookup"><span data-stu-id="a322b-223">Assume a configuration file named `copyoperation`, that contains the following lines.</span></span> <span data-ttu-id="a322b-224">每個 AzCopy 參數可以指定在同一行。</span><span class="sxs-lookup"><span data-stu-id="a322b-224">Each AzCopy parameter can be specified on a single line.</span></span>

    --source http://myaccount.blob.core.windows.net/mycontainer --destination /mnt/myfiles --source-key <sourcekey> --recursive --quiet

<span data-ttu-id="a322b-225">或不同行：</span><span class="sxs-lookup"><span data-stu-id="a322b-225">or on separate lines:</span></span>

    --source http://myaccount.blob.core.windows.net/mycontainer
    --destination /mnt/myfiles
    --source-key<sourcekey>
    --recursive
    --quiet

<span data-ttu-id="a322b-226">如果您將參數分割成兩行，如以下的 `--source-key` 參數所示，則 AzCopy 會失敗：</span><span class="sxs-lookup"><span data-stu-id="a322b-226">AzCopy fails if you split the parameter across two lines, as shown here for the `--source-key` parameter:</span></span>

    http://myaccount.blob.core.windows.net/mycontainer
    /mnt/myfiles
    --sourcekey
    <sourcekey>
    --recursive
    --quiet

### <a name="specify-a-shared-access-signature-sas"></a><span data-ttu-id="a322b-227">指定共用存取簽章 (SAS)</span><span class="sxs-lookup"><span data-stu-id="a322b-227">Specify a shared access signature (SAS)</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer1 \
    --destination https://myaccount.blob.core.windows.net/mycontainer2 \
    --source-sas <SAS1> \
    --dest-sas <SAS2> \
    --include abc.txt
```

<span data-ttu-id="a322b-228">您也可以在容器 URI 上指定 SAS：</span><span class="sxs-lookup"><span data-stu-id="a322b-228">You can also specify a SAS on the container URI:</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer1/?SourceSASToken \
    --destination /mnt/myfiles \
    --recursive
```

<span data-ttu-id="a322b-229">請注意，AzCopy 目前僅支援[帳戶 SAS](https://docs.microsoft.com/en-us/azure/storage/storage-dotnet-shared-access-signature-part-1) \(英文\)。</span><span class="sxs-lookup"><span data-stu-id="a322b-229">Note that AzCopy currently only supports the [Account SAS](https://docs.microsoft.com/en-us/azure/storage/storage-dotnet-shared-access-signature-part-1).</span></span>

### <a name="journal-file-folder"></a><span data-ttu-id="a322b-230">日誌檔案資料夾</span><span class="sxs-lookup"><span data-stu-id="a322b-230">Journal file folder</span></span>
<span data-ttu-id="a322b-231">每次發佈命令至 AzCopy 時，它會檢查預設資料夾或透過此選項指定的資料夾中是否有日誌檔案存在。</span><span class="sxs-lookup"><span data-stu-id="a322b-231">Each time you issue a command to AzCopy, it checks whether a journal file exists in the default folder, or whether it exists in a folder that you specified via this option.</span></span> <span data-ttu-id="a322b-232">如果在這兩個地方都找不到日誌檔案，AzCopy 會將此作業視為新的作業，並產生新的日誌檔案。</span><span class="sxs-lookup"><span data-stu-id="a322b-232">If the journal file does not exist in either place, AzCopy treats the operation as new and generates a new journal file.</span></span>

<span data-ttu-id="a322b-233">如果找到日誌檔案，則 AzCopy 會檢查所輸入的命令列是否符合日誌檔案中的命令列。</span><span class="sxs-lookup"><span data-stu-id="a322b-233">If the journal file does exist, AzCopy checks whether the command line that you input matches the command line in the journal file.</span></span> <span data-ttu-id="a322b-234">如果這兩個命令列相符，AzCopy 便會繼續未完成的作業。</span><span class="sxs-lookup"><span data-stu-id="a322b-234">If the two command lines match, AzCopy resumes the incomplete operation.</span></span> <span data-ttu-id="a322b-235">如果這兩個命令列不符，AzCopy 會提示使用者覆寫日誌檔案並開始新的作業，或取消目前作業。</span><span class="sxs-lookup"><span data-stu-id="a322b-235">If they do not match, AzCopy prompts user to either overwrite the journal file to start a new operation, or to cancel the current operation.</span></span>

<span data-ttu-id="a322b-236">如果您想要使用預設的日誌檔案位置：</span><span class="sxs-lookup"><span data-stu-id="a322b-236">If you want to use the default location for the journal file:</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --resume
```

<span data-ttu-id="a322b-237">如果省略 `--resume`，或指定 `--resume` 選項但沒有指定資料夾路徑 (如上所示)，則 AzCopy 會在預設位置上建立日誌檔案，預設位置是 `~\Microsoft\Azure\AzCopy`。</span><span class="sxs-lookup"><span data-stu-id="a322b-237">If you omit option `--resume`, or specify option `--resume` without the folder path, as shown above, AzCopy creates the journal file in the default location, which is `~\Microsoft\Azure\AzCopy`.</span></span> <span data-ttu-id="a322b-238">如果日誌檔案已存在，則 AzCopy 會根據此日誌檔案繼續作業。</span><span class="sxs-lookup"><span data-stu-id="a322b-238">If the journal file already exists, then AzCopy resumes the operation based on the journal file.</span></span>

<span data-ttu-id="a322b-239">如果您想要指定自訂的日誌檔案位置：</span><span class="sxs-lookup"><span data-stu-id="a322b-239">If you want to specify a custom location for the journal file:</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key key \
    --resume "/mnt/myjournal"
```

<span data-ttu-id="a322b-240">如果日誌檔案不存在，本範例將建立日誌檔案。</span><span class="sxs-lookup"><span data-stu-id="a322b-240">This example creates the journal file if it does not already exist.</span></span> <span data-ttu-id="a322b-241">如果日誌檔案已存在，則 AzCopy 會根據此日誌檔案繼續作業。</span><span class="sxs-lookup"><span data-stu-id="a322b-241">If it does exist, then AzCopy resumes the operation based on the journal file.</span></span>

<span data-ttu-id="a322b-242">如果您想要繼續 AzCopy 作業，請重複相同的命令。</span><span class="sxs-lookup"><span data-stu-id="a322b-242">If you want to resume an AzCopy operation, repeat the same command.</span></span> <span data-ttu-id="a322b-243">然後 AzCopy on Linux 會提示您確認：</span><span class="sxs-lookup"><span data-stu-id="a322b-243">AzCopy on Linux then will prompt for confirmation:</span></span>

```azcopy
Incomplete operation with same command line detected at the journal directory "/home/myaccount/Microsoft/Azure/AzCopy", do you want to resume the operation? Choose Yes to resume, choose No to overwrite the journal to start a new operation. (Yes/No)
```

### <a name="output-verbose-logs"></a><span data-ttu-id="a322b-244">輸出詳細資訊記錄檔</span><span class="sxs-lookup"><span data-stu-id="a322b-244">Output verbose logs</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --verbose
```

### <a name="specify-the-number-of-concurrent-operations-to-start"></a><span data-ttu-id="a322b-245">指定要啟動的並行作業數目</span><span class="sxs-lookup"><span data-stu-id="a322b-245">Specify the number of concurrent operations to start</span></span>
<span data-ttu-id="a322b-246">`--parallel-level` 選項可指定並行複製作業的數目。</span><span class="sxs-lookup"><span data-stu-id="a322b-246">Option `--parallel-level` specifies the number of concurrent copy operations.</span></span> <span data-ttu-id="a322b-247">根據預設，AzCopy 依預設會啟動特定數量的並行作業，以提高資料傳輸的輸送量。</span><span class="sxs-lookup"><span data-stu-id="a322b-247">By default, AzCopy starts a certain number of concurrent operations to increase the data transfer throughput.</span></span> <span data-ttu-id="a322b-248">並行作業數目等於您所擁有處理器數目的八倍。</span><span class="sxs-lookup"><span data-stu-id="a322b-248">The number of concurrent operations is equal eight times the number of processors you have.</span></span> <span data-ttu-id="a322b-249">如果您在低頻寬的網路上執行 AzCopy，則您可以針對平行層級指定較低的數字，以避免因為資源競爭所導致的失敗。</span><span class="sxs-lookup"><span data-stu-id="a322b-249">If you are running AzCopy across a low-bandwidth network, you can specify a lower number for --parallel-level to avoid failure caused by resource competition.</span></span>

[!TIP]
><span data-ttu-id="a322b-250">若要檢視 AzCopy 參數的完整清單，請參閱 [azcopy --說明] 功能表。</span><span class="sxs-lookup"><span data-stu-id="a322b-250">To view the complete list of AzCopy parameters, check out 'azcopy --help' menu.</span></span>

## <a name="known-issues-and-best-practices"></a><span data-ttu-id="a322b-251">已知問題和最佳作法</span><span class="sxs-lookup"><span data-stu-id="a322b-251">Known issues and best practices</span></span>
### <a name="error-net-core-is-not-found-in-the-system"></a><span data-ttu-id="a322b-252">錯誤：在系統中找不到 .NET Core。</span><span class="sxs-lookup"><span data-stu-id="a322b-252">Error: .NET Core is not found in the system.</span></span>
<span data-ttu-id="a322b-253">如果您遇到錯誤，表示系統中並未安裝 .NET Core，則可能遺失 .NET Core 二進位 `dotnet` 的 PATH。</span><span class="sxs-lookup"><span data-stu-id="a322b-253">If you encounter an error stating that .NET Core is not installed in the system, the PATH to the .NET Core binary `dotnet` may be missing.</span></span>

<span data-ttu-id="a322b-254">若要解決此問題，請在系統中尋找 .NET Core 二進位：</span><span class="sxs-lookup"><span data-stu-id="a322b-254">In order to address this issue, find the .NET Core binary in the system:</span></span>
```bash
sudo find / -name dotnet
```

<span data-ttu-id="a322b-255">這樣會傳回 dotnet 二進位的路徑。</span><span class="sxs-lookup"><span data-stu-id="a322b-255">This returns the path to the dotnet binary.</span></span> 

    /opt/rh/rh-dotnetcore11/root/usr/bin/dotnet
    /opt/rh/rh-dotnetcore11/root/usr/lib64/dotnetcore/dotnet
    /opt/rh/rh-dotnetcore11/root/usr/lib64/dotnetcore/shared/Microsoft.NETCore.App/1.1.2/dotnet

<span data-ttu-id="a322b-256">現在將此路徑新增至 PATH 變數。</span><span class="sxs-lookup"><span data-stu-id="a322b-256">Now add this path to the PATH variable.</span></span> <span data-ttu-id="a322b-257">針對 sudo，請編輯 secure_path，使其包含 dotnet 二進位的路徑：</span><span class="sxs-lookup"><span data-stu-id="a322b-257">For sudo, edit secure_path to contain the path to the dotnet binary:</span></span>
```bash 
sudo visudo
### Append the path found in the preceding example to 'secure_path' variable
```

<span data-ttu-id="a322b-258">在此範例中，secure_path 變數會顯示為：</span><span class="sxs-lookup"><span data-stu-id="a322b-258">In this example, secure_path variable reads as:</span></span>

```
secure_path = /sbin:/bin:/usr/sbin:/usr/bin:/opt/rh/rh-dotnetcore11/root/usr/bin/
```

<span data-ttu-id="a322b-259">針對目前使用者，請編輯 .bash_profile/.profile，使其在 PATH 變數中包含 dotnet 二進位的路徑</span><span class="sxs-lookup"><span data-stu-id="a322b-259">For the current user, edit .bash_profile/.profile to include the path to the dotnet binary in PATH variable</span></span> 
```bash
vi ~/.bash_profile
### Append the path found in the preceding example to 'PATH' variable
```

<span data-ttu-id="a322b-260">確認 .NET Core 現在位於 PATH 中：</span><span class="sxs-lookup"><span data-stu-id="a322b-260">Verify that .NET Core is now in PATH:</span></span>
```bash
which dotnet
sudo which dotnet
```

### <a name="error-installing-azcopy"></a><span data-ttu-id="a322b-261">安裝 AzCopy 時發生錯誤</span><span class="sxs-lookup"><span data-stu-id="a322b-261">Error Installing AzCopy</span></span>
<span data-ttu-id="a322b-262">如果您遇到 AzCopy 安裝的問題，可以嘗試使用解壓縮 `azcopy` 資料夾中的 bash 指令碼執行 AzCopy。</span><span class="sxs-lookup"><span data-stu-id="a322b-262">If you encounter issues with AzCopy installation, you may try to run AzCopy using the bash script in the extracted `azcopy` folder.</span></span>

```bash
cd azcopy
./azcopy
```

### <a name="limit-concurrent-writes-while-copying-data"></a><span data-ttu-id="a322b-263">限制複製資料時的並行寫入</span><span class="sxs-lookup"><span data-stu-id="a322b-263">Limit concurrent writes while copying data</span></span>
<span data-ttu-id="a322b-264">使用 AzCopy 複製 Blob 或檔案時，請留意當您在複製資料時，另一個應用程式可能正在修改該資料。</span><span class="sxs-lookup"><span data-stu-id="a322b-264">When you copy blobs or files with AzCopy, keep in mind that another application may be modifying the data while you are copying it.</span></span> <span data-ttu-id="a322b-265">請儘可能地確定在複製作業過程中，您正要複製的資料並不在修改中。</span><span class="sxs-lookup"><span data-stu-id="a322b-265">If possible, ensure that the data you are copying is not being modified during the copy operation.</span></span> <span data-ttu-id="a322b-266">例如，當複製與 Azure 虛擬機器相關聯的 VHD 時，請確定目前沒有其他應用程式正在寫入此 VHD。</span><span class="sxs-lookup"><span data-stu-id="a322b-266">For example, when copying a VHD associated with an Azure virtual machine, make sure that no other applications are currently writing to the VHD.</span></span> <span data-ttu-id="a322b-267">要這樣做的一個好方法是租用要複製的資源。</span><span class="sxs-lookup"><span data-stu-id="a322b-267">A good way to do this is by leasing the resource to be copied.</span></span> <span data-ttu-id="a322b-268">此外，您可以首先建立 VHD 的快照，然後複製此快照。</span><span class="sxs-lookup"><span data-stu-id="a322b-268">Alternately, you can create a snapshot of the VHD first and then copy the snapshot.</span></span>

<span data-ttu-id="a322b-269">如果您無法在複製時防止其他應用程式寫入 Blob 或檔案，請記住，工作完成時，複製的資源可能不再與來源資源完全相同。</span><span class="sxs-lookup"><span data-stu-id="a322b-269">If you cannot prevent other applications from writing to blobs or files while they are being copied, then keep in mind that by the time the job finishes, the copied resources may no longer have full parity with the source resources.</span></span>

### <a name="run-one-azcopy-instance-on-one-machine"></a><span data-ttu-id="a322b-270">在一部電腦上執行一個 AzCopy 執行個體。</span><span class="sxs-lookup"><span data-stu-id="a322b-270">Run one AzCopy instance on one machine.</span></span>
<span data-ttu-id="a322b-271">AzCopy 設計為充分利用電腦資源來加速資料傳輸，建議您在一部電腦上只執行一個 AzCopy 執行個體，如果需要更多並行作業，您可以指定 `--parallel-level` 選項。</span><span class="sxs-lookup"><span data-stu-id="a322b-271">AzCopy is designed to maximize the utilization of your machine resource to accelerate the data transfer, we recommend you run only one AzCopy instance on one machine, and specify the option `--parallel-level` if you need more concurrent operations.</span></span> <span data-ttu-id="a322b-272">如需詳細資訊，請在命令列上輸入 `AzCopy --help parallel-level` 。</span><span class="sxs-lookup"><span data-stu-id="a322b-272">For more details, type `AzCopy --help parallel-level` at the command line.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a322b-273">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a322b-273">Next steps</span></span>
<span data-ttu-id="a322b-274">如需關於 Azure 儲存體和 AzCopy 的詳細資訊，請參閱下列資源：</span><span class="sxs-lookup"><span data-stu-id="a322b-274">For more information about Azure Storage and AzCopy, see the following resources:</span></span>

### <a name="azure-storage-documentation"></a><span data-ttu-id="a322b-275">Azure 儲存體文件：</span><span class="sxs-lookup"><span data-stu-id="a322b-275">Azure Storage documentation:</span></span>
* [<span data-ttu-id="a322b-276">Azure 儲存體簡介</span><span class="sxs-lookup"><span data-stu-id="a322b-276">Introduction to Azure Storage</span></span>](storage-introduction.md)
* [<span data-ttu-id="a322b-277">建立儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="a322b-277">Create a storage account</span></span>](storage-create-storage-account.md)
* <span data-ttu-id="a322b-278">[使用儲存體總管來管理 Blob](https://docs.microsoft.com/en-us/azure/vs-azure-tools-storage-explorer-blobs) \(英文\)</span><span class="sxs-lookup"><span data-stu-id="a322b-278">[Manage blobs with Storage Explorer](https://docs.microsoft.com/en-us/azure/vs-azure-tools-storage-explorer-blobs)</span></span>
* [<span data-ttu-id="a322b-279">使用 Azure CLI 2.0 搭配 Azure 儲存體</span><span class="sxs-lookup"><span data-stu-id="a322b-279">Using the Azure CLI 2.0 with Azure Storage</span></span>](storage-azure-cli.md)
* [<span data-ttu-id="a322b-280">如何使用 C++ 的 Blob 儲存體</span><span class="sxs-lookup"><span data-stu-id="a322b-280">How to use Blob storage from C++</span></span>](storage-c-plus-plus-how-to-use-blobs.md)
* [<span data-ttu-id="a322b-281">如何使用 Java 的 Blob 儲存體</span><span class="sxs-lookup"><span data-stu-id="a322b-281">How to use Blob storage from Java</span></span>](storage-java-how-to-use-blob-storage.md)
* [<span data-ttu-id="a322b-282">如何使用 Node.js 的 Blob 儲存體</span><span class="sxs-lookup"><span data-stu-id="a322b-282">How to use Blob storage from Node.js</span></span>](storage-nodejs-how-to-use-blob-storage.md)
* [<span data-ttu-id="a322b-283">如何使用 Python 的 Blob 儲存體</span><span class="sxs-lookup"><span data-stu-id="a322b-283">How to use Blob storage from Python</span></span>](storage-python-how-to-use-blob-storage.md)

### <a name="azure-storage-blog-posts"></a><span data-ttu-id="a322b-284">Azure 儲存體部落格文章：</span><span class="sxs-lookup"><span data-stu-id="a322b-284">Azure Storage blog posts:</span></span>
* <span data-ttu-id="a322b-285">[宣告 AzCopy on Linux 預覽](https://azure.microsoft.com/en-in/blog/announcing-azcopy-on-linux-preview/) \(英文\)</span><span class="sxs-lookup"><span data-stu-id="a322b-285">[Announcing AzCopy on Linux Preview](https://azure.microsoft.com/en-in/blog/announcing-azcopy-on-linux-preview/)</span></span>
* [<span data-ttu-id="a322b-286">Azure 儲存體資料移動文件庫預覽簡介</span><span class="sxs-lookup"><span data-stu-id="a322b-286">Introducing Azure Storage Data Movement Library Preview</span></span>](https://azure.microsoft.com/blog/introducing-azure-storage-data-movement-library-preview-2/)
* [<span data-ttu-id="a322b-287">AzCopy：簡介同步複製和自訂內容類型</span><span class="sxs-lookup"><span data-stu-id="a322b-287">AzCopy: Introducing synchronous copy and customized content type</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2015/01/13/azcopy-introducing-synchronous-copy-and-customized-content-type.aspx)
* [<span data-ttu-id="a322b-288">AzCopy: 宣布正式發行 AzCopy 3.0 和具有資料表和檔案支援的 AzCopy 4.0 預覽版本</span><span class="sxs-lookup"><span data-stu-id="a322b-288">AzCopy: Announcing General Availability of AzCopy 3.0 plus preview release of AzCopy 4.0 with Table and File support</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/10/29/azcopy-announcing-general-availability-of-azcopy-3-0-plus-preview-release-of-azcopy-4-0-with-table-and-file-support.aspx)
* [<span data-ttu-id="a322b-289">AzCopy: 針對大規模複製案例最佳化</span><span class="sxs-lookup"><span data-stu-id="a322b-289">AzCopy: Optimized for Large-Scale Copy Scenarios</span></span>](http://go.microsoft.com/fwlink/?LinkId=507682)
* [<span data-ttu-id="a322b-290">AzCopy: 支援讀取存取異地備援儲存體</span><span class="sxs-lookup"><span data-stu-id="a322b-290">AzCopy: Support for read-access geo-redundant storage</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/04/07/azcopy-support-for-read-access-geo-redundant-account.aspx)
* <span data-ttu-id="a322b-291">[AzCopy：使用可重新啟動模式和 SAS 權杖傳輸資料](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/09/07/azcopy-transfer-data-with-re-startable-mode-and-sas-token.aspx) \(英文\)</span><span class="sxs-lookup"><span data-stu-id="a322b-291">[AzCopy: Transfer data with restartable mode and SAS token](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/09/07/azcopy-transfer-data-with-re-startable-mode-and-sas-token.aspx)</span></span>
* [<span data-ttu-id="a322b-292">AzCopy: 使用跨帳戶複製 Blob</span><span class="sxs-lookup"><span data-stu-id="a322b-292">AzCopy: Using cross-account Copy Blob</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/04/01/azcopy-using-cross-account-copy-blob.aspx)
* [<span data-ttu-id="a322b-293">AzCopy: 上傳/下載 Azure Blob 的檔案</span><span class="sxs-lookup"><span data-stu-id="a322b-293">AzCopy: Uploading/downloading files for Azure Blobs</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/12/03/azcopy-uploading-downloading-files-for-windows-azure-blobs.aspx)

