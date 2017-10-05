---
title: "使用 AzCopy on Windows 複製或移動資料到 Azure 儲存體 | Microsoft Docs"
description: "使用 AzCopy on Windows 公用程式來從 Blob、資料表和檔案內容移動或來回複製資料。 從本機檔案複製資料到 Azure 儲存體，或在儲存體帳戶內或之間複製資料。 輕鬆地將資料移轉至 Azure 儲存體。"
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
ms.openlocfilehash: 045778822022752295bb634bdf734daaf36ab938
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="transfer-data-with-the-azcopy-on-windows"></a><span data-ttu-id="e5dad-105">使用 AzCopy on Windows 傳送資料</span><span class="sxs-lookup"><span data-stu-id="e5dad-105">Transfer data with the AzCopy on Windows</span></span>
<span data-ttu-id="e5dad-106">AzCopy 是個命令列公用程式，專為使用簡單命令高效率地將資料複製到和複製出 Microsoft Azure Blob、檔案和表格儲存體所設計。</span><span class="sxs-lookup"><span data-stu-id="e5dad-106">AzCopy is a command-line utility designed for copying data to and from Microsoft Azure Blob, File, and Table storage using simple commands with optimal performance.</span></span> <span data-ttu-id="e5dad-107">您可以從儲存體帳戶內或是在儲存體帳戶之間，從一個物件複製資料到另一個物件。</span><span class="sxs-lookup"><span data-stu-id="e5dad-107">You can copy data from one object to another within your storage account, or between storage accounts.</span></span>

<span data-ttu-id="e5dad-108">有兩個 AzCopy 版本可供您下載。</span><span class="sxs-lookup"><span data-stu-id="e5dad-108">There are two versions of AzCopy that you can download.</span></span> <span data-ttu-id="e5dad-109">AzCopy on Windows 內建有 .NET Framework，並且提供 Windows 樣式的命令列選項。</span><span class="sxs-lookup"><span data-stu-id="e5dad-109">AzCopy on Windows is built with .NET Framework, and offers Windows style command-line options.</span></span> <span data-ttu-id="e5dad-110">[AzCopy on Linux](storage-use-azcopy-linux.md) 內建有 .NET Core Framework，其以提供 POSIX 樣式命令列選項的 Linux 平台為目標。</span><span class="sxs-lookup"><span data-stu-id="e5dad-110">[AzCopy on Linux](storage-use-azcopy-linux.md) is built with .NET Core Framework which targets Linux platforms offering POSIX style command-line options.</span></span> <span data-ttu-id="e5dad-111">本文涵蓋之內容包括 AzCopy on Windows。</span><span class="sxs-lookup"><span data-stu-id="e5dad-111">This article covers AzCopy on Windows.</span></span>

## <a name="download-and-install-azcopy"></a><span data-ttu-id="e5dad-112">下載並安裝 AzCopy</span><span class="sxs-lookup"><span data-stu-id="e5dad-112">Download and install AzCopy</span></span>
### <a name="azcopy-on-windows"></a><span data-ttu-id="e5dad-113">AzCopy on Windows</span><span class="sxs-lookup"><span data-stu-id="e5dad-113">AzCopy on Windows</span></span>
<span data-ttu-id="e5dad-114">下載 [最新版本的 AzCopy on Windows](http://aka.ms/downloadazcopy)。</span><span class="sxs-lookup"><span data-stu-id="e5dad-114">Download the [latest version of AzCopy on Windows](http://aka.ms/downloadazcopy).</span></span>

#### <a name="installation-on-windows"></a><span data-ttu-id="e5dad-115">在 Windows 上安裝</span><span class="sxs-lookup"><span data-stu-id="e5dad-115">Installation on Windows</span></span>
<span data-ttu-id="e5dad-116">使用安裝程式安裝 AzCopy on Windows 之後，請開啟命令視窗並瀏覽至電腦上的 AzCopy 安裝目錄，也就是 `AzCopy.exe` 可執行檔的所在位置。</span><span class="sxs-lookup"><span data-stu-id="e5dad-116">After installing AzCopy on Windows using the installer, open a command window and navigate to the AzCopy installation directory on your computer - where the `AzCopy.exe` executable is located.</span></span> <span data-ttu-id="e5dad-117">若有需要，您可以在您的系統路徑中加入 AzCopy 安裝位置。</span><span class="sxs-lookup"><span data-stu-id="e5dad-117">If desired, you can add the AzCopy installation location to your system path.</span></span> <span data-ttu-id="e5dad-118">根據預設，AzCopy 會安裝到 `%ProgramFiles(x86)%\Microsoft SDKs\Azure\AzCopy` 或 `%ProgramFiles%\Microsoft SDKs\Azure\AzCopy`。</span><span class="sxs-lookup"><span data-stu-id="e5dad-118">By default, AzCopy is installed to `%ProgramFiles(x86)%\Microsoft SDKs\Azure\AzCopy` or `%ProgramFiles%\Microsoft SDKs\Azure\AzCopy`.</span></span>

## <a name="writing-your-first-azcopy-command"></a><span data-ttu-id="e5dad-119">撰寫第一個 AzCopy 命令</span><span class="sxs-lookup"><span data-stu-id="e5dad-119">Writing your first AzCopy command</span></span>
<span data-ttu-id="e5dad-120">AzCopy 命令的基本語法是：</span><span class="sxs-lookup"><span data-stu-id="e5dad-120">The basic syntax for AzCopy commands is:</span></span>

```azcopy
AzCopy /Source:<source> /Dest:<destination> [Options]
```

<span data-ttu-id="e5dad-121">下列範例會示範各種不同的 Microsoft Azure Blob、檔案和資料表資料複製案例。</span><span class="sxs-lookup"><span data-stu-id="e5dad-121">The following examples demonstrate a variety of scenarios for copying data to and from Microsoft Azure Blobs, Files, and Tables.</span></span> <span data-ttu-id="e5dad-122">如需每個範例中所使用參數的詳細說明，請參閱 [AzCopy 參數](#azcopy-parameters) 一節。</span><span class="sxs-lookup"><span data-stu-id="e5dad-122">Refer to the [AzCopy Parameters](#azcopy-parameters) section for a detailed explanation of the parameters used in each sample.</span></span>

## <a name="blob-download"></a><span data-ttu-id="e5dad-123">Blob：下載</span><span class="sxs-lookup"><span data-stu-id="e5dad-123">Blob: Download</span></span>
### <a name="download-single-blob"></a><span data-ttu-id="e5dad-124">下載單一 Blob</span><span class="sxs-lookup"><span data-stu-id="e5dad-124">Download single blob</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /Pattern:"abc.txt"
```

<span data-ttu-id="e5dad-125">請注意，如果資料夾 `C:\myfolder` 不存在，AzCopy 會加以建立並將 `abc.txt ` 下載到新資料夾。</span><span class="sxs-lookup"><span data-stu-id="e5dad-125">Note that if the folder `C:\myfolder` does not exist, AzCopy will create it and download `abc.txt ` into the new folder.</span></span>

### <a name="download-single-blob-from-secondary-region"></a><span data-ttu-id="e5dad-126">從次要地區下載單一 Blob</span><span class="sxs-lookup"><span data-stu-id="e5dad-126">Download single blob from secondary region</span></span>

```azcopy
AzCopy /Source:https://myaccount-secondary.blob.core.windows.net/mynewcontainer /Dest:C:\myfolder /SourceKey:key /Pattern:abc.txt
```

<span data-ttu-id="e5dad-127">請注意，您必須啟用讀取權限異地備援儲存體。</span><span class="sxs-lookup"><span data-stu-id="e5dad-127">Note that you must have read-access geo-redundant storage enabled.</span></span>

### <a name="download-all-blobs"></a><span data-ttu-id="e5dad-128">下載所有 Blob</span><span class="sxs-lookup"><span data-stu-id="e5dad-128">Download all blobs</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /S
```

<span data-ttu-id="e5dad-129">假設下列 Blob 位於指定容器中：</span><span class="sxs-lookup"><span data-stu-id="e5dad-129">Assume the following blobs reside in the specified container:</span></span>  

    abc.txt
    abc1.txt
    abc2.txt
    vd1\a.txt
    vd1\abcd.txt

<span data-ttu-id="e5dad-130">下載作業之後，目錄 `C:\myfolder` 將包含下列檔案：</span><span class="sxs-lookup"><span data-stu-id="e5dad-130">After the download operation, the directory `C:\myfolder` will include the following files:</span></span>

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt
    C:\myfolder\vd1\a.txt
    C:\myfolder\vd1\abcd.txt

<span data-ttu-id="e5dad-131">如果您未指定選項 `/S`，則不會下載任何 Blob。</span><span class="sxs-lookup"><span data-stu-id="e5dad-131">If you do not specify option `/S`, no blobs will be downloaded.</span></span>

### <a name="download-blobs-with-specified-prefix"></a><span data-ttu-id="e5dad-132">下載具有指定首碼的 Blob</span><span class="sxs-lookup"><span data-stu-id="e5dad-132">Download blobs with specified prefix</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /Pattern:a /S
```

<span data-ttu-id="e5dad-133">假設下列 Blob 位於指定容器中。</span><span class="sxs-lookup"><span data-stu-id="e5dad-133">Assume the following blobs reside in the specified container.</span></span> <span data-ttu-id="e5dad-134">將會下載所有以首碼 `a` 開頭的 Blob：</span><span class="sxs-lookup"><span data-stu-id="e5dad-134">All blobs beginning with the prefix `a` will be downloaded:</span></span>

    abc.txt
    abc1.txt
    abc2.txt
    xyz.txt
    vd1\a.txt
    vd1\abcd.txt

<span data-ttu-id="e5dad-135">下載作業之後，資料夾 `C:\myfolder` 將包含下列檔案：</span><span class="sxs-lookup"><span data-stu-id="e5dad-135">After the download operation, the folder `C:\myfolder` will include the following files:</span></span>

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt

<span data-ttu-id="e5dad-136">首碼會套用到虛擬目錄，虛擬目錄會構成第一部分的 Blob 名稱。</span><span class="sxs-lookup"><span data-stu-id="e5dad-136">The prefix applies to the virtual directory, which forms the first part of the blob name.</span></span> <span data-ttu-id="e5dad-137">在上述範例中，虛擬目錄不符合指定的首碼，所以不會被下載。</span><span class="sxs-lookup"><span data-stu-id="e5dad-137">In the example shown above, the virtual directory does not match the specified prefix, so it is not downloaded.</span></span> <span data-ttu-id="e5dad-138">此外，如果未指定選項 `\S` ，則 AzCopy 不會下載任何 Blob。</span><span class="sxs-lookup"><span data-stu-id="e5dad-138">In addition, if the option `\S` is not specified, AzCopy will not download any blobs.</span></span>

### <a name="set-the-last-modified-time-of-exported-files-to-be-same-as-the-source-blobs"></a><span data-ttu-id="e5dad-139">將匯出檔案的最後修改時間設定為與來源 Blob 相同的最後修改時間</span><span class="sxs-lookup"><span data-stu-id="e5dad-139">Set the last-modified time of exported files to be same as the source blobs</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /MT
```

<span data-ttu-id="e5dad-140">您也可以根據其最後修改時間，將 Blob 從下載作業中排除。</span><span class="sxs-lookup"><span data-stu-id="e5dad-140">You can also exclude blobs from the download operation based on their last-modified time.</span></span> <span data-ttu-id="e5dad-141">例如，如果您想要排除最後修改時間比目的地檔案還要新或相同的 Blob，請新增 `/XN` 選項：</span><span class="sxs-lookup"><span data-stu-id="e5dad-141">For example, if you want to exclude blobs whose last modified time is the same or newer than the destination file, add the `/XN` option:</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /MT /XN
```

<span data-ttu-id="e5dad-142">或者，如果您想要排除最後修改時間比目的地檔案還要舊或相同的 Blob，請新增 `/XO` 選項：</span><span class="sxs-lookup"><span data-stu-id="e5dad-142">Or if you want to exclude blobs whose last modified time is the same or older than the destination file, add the `/XO` option:</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /MT /XO
```

## <a name="blob-upload"></a><span data-ttu-id="e5dad-143">Blob：上傳</span><span class="sxs-lookup"><span data-stu-id="e5dad-143">Blob: Upload</span></span>
### <a name="upload-single-file"></a><span data-ttu-id="e5dad-144">上傳單一檔案</span><span class="sxs-lookup"><span data-stu-id="e5dad-144">Upload single file</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Pattern:"abc.txt"
```

<span data-ttu-id="e5dad-145">如果指定的目的地容器不存在，則 AzCopy 將建立此容器並將檔案上傳至該容器中。</span><span class="sxs-lookup"><span data-stu-id="e5dad-145">If the specified destination container does not exist, AzCopy will create it and upload the file into it.</span></span>

### <a name="upload-single-file-to-virtual-directory"></a><span data-ttu-id="e5dad-146">上傳單一檔案到虛擬目錄</span><span class="sxs-lookup"><span data-stu-id="e5dad-146">Upload single file to virtual directory</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer/vd /DestKey:key /Pattern:abc.txt
```

<span data-ttu-id="e5dad-147">如果指定的虛擬目錄不存在，則 AzCopy 將上傳檔案並在其名稱中加上此虛擬目錄 (例如，上述範例中的 `vd/abc.txt`)。</span><span class="sxs-lookup"><span data-stu-id="e5dad-147">If the specified virtual directory does not exist, AzCopy will upload the file to include the virtual directory in its name (*e.g.*, `vd/abc.txt` in the example above).</span></span>

### <a name="upload-all-files"></a><span data-ttu-id="e5dad-148">上傳所有檔案</span><span class="sxs-lookup"><span data-stu-id="e5dad-148">Upload all files</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /S
```

<span data-ttu-id="e5dad-149">指定 `/S` 選項以遞迴方式將指定目錄的內容上傳到 Blob 儲存體，這表示也會上傳所有的子資料夾及其檔案。</span><span class="sxs-lookup"><span data-stu-id="e5dad-149">Specifying option `/S` uploads the contents of the specified directory to Blob storage recursively, meaning that all subfolders and their files will be uploaded as well.</span></span> <span data-ttu-id="e5dad-150">例如，假設下列檔案位於 `C:\myfolder`資料夾內：</span><span class="sxs-lookup"><span data-stu-id="e5dad-150">For instance, assume the following files reside in folder `C:\myfolder`:</span></span>

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt
    C:\myfolder\subfolder\a.txt
    C:\myfolder\subfolder\abcd.txt

<span data-ttu-id="e5dad-151">上傳作業之後，容器將包含下列檔案：</span><span class="sxs-lookup"><span data-stu-id="e5dad-151">After the upload operation, the container will include the following files:</span></span>

    abc.txt
    abc1.txt
    abc2.txt
    subfolder\a.txt
    subfolder\abcd.txt

<span data-ttu-id="e5dad-152">如果您未指定選項 `/S`，AzCopy 將不會以遞迴方式上傳。</span><span class="sxs-lookup"><span data-stu-id="e5dad-152">If you do not specify option `/S`, AzCopy will not upload recursively.</span></span> <span data-ttu-id="e5dad-153">上傳作業之後，容器將包含下列檔案：</span><span class="sxs-lookup"><span data-stu-id="e5dad-153">After the upload operation, the container will include the following files:</span></span>

    abc.txt
    abc1.txt
    abc2.txt

### <a name="upload-files-matching-specified-pattern"></a><span data-ttu-id="e5dad-154">上傳符合指定模式的檔案</span><span class="sxs-lookup"><span data-stu-id="e5dad-154">Upload files matching specified pattern</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Pattern:a* /S
```

<span data-ttu-id="e5dad-155">假設下列檔案位於 `C:\myfolder`資料夾內：</span><span class="sxs-lookup"><span data-stu-id="e5dad-155">Assume the following files reside in folder `C:\myfolder`:</span></span>

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt
    C:\myfolder\xyz.txt
    C:\myfolder\subfolder\a.txt
    C:\myfolder\subfolder\abcd.txt

<span data-ttu-id="e5dad-156">上傳作業之後，容器將包含下列檔案：</span><span class="sxs-lookup"><span data-stu-id="e5dad-156">After the upload operation, the container will include the following files:</span></span>

    abc.txt
    abc1.txt
    abc2.txt
    subfolder\a.txt
    subfolder\abcd.txt

<span data-ttu-id="e5dad-157">如果您未指定選項 `/S`，AzCopy 將只會上傳沒有位於虛擬目錄的 Blob：</span><span class="sxs-lookup"><span data-stu-id="e5dad-157">If you do not specify option `/S`, AzCopy will only upload blobs that don't reside in a virtual directory:</span></span>

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt

### <a name="specify-the-mime-content-type-of-a-destination-blob"></a><span data-ttu-id="e5dad-158">指定目的地 blob 的 MIME 內容類型</span><span class="sxs-lookup"><span data-stu-id="e5dad-158">Specify the MIME content type of a destination blob</span></span>
<span data-ttu-id="e5dad-159">根據預設，AzCopy 會將目的地 blob 的內容類型設定為 `application/octet-stream`。</span><span class="sxs-lookup"><span data-stu-id="e5dad-159">By default, AzCopy sets the content type of a destination blob to `application/octet-stream`.</span></span> <span data-ttu-id="e5dad-160">從 3.1.0 版開始，您可以透過 `/SetContentType:[content-type]`選項明確指定內容類型。</span><span class="sxs-lookup"><span data-stu-id="e5dad-160">Beginning with version 3.1.0, you can explicitly specify the content type via the option `/SetContentType:[content-type]`.</span></span> <span data-ttu-id="e5dad-161">此語法會在上傳作業中設定所有 Blob 的內容類型。</span><span class="sxs-lookup"><span data-stu-id="e5dad-161">This syntax sets the content type for all blobs in an upload operation.</span></span>

```azcopy
AzCopy /Source:C:\myfolder\ /Dest:https://myaccount.blob.core.windows.net/myContainer/ /DestKey:key /Pattern:ab /SetContentType:video/mp4
```

<span data-ttu-id="e5dad-162">如果您指定 `/SetContentType` 但未指定任何值，則 AzCopy 會根據副檔名來設定每個 blob 或檔案的內容類型。</span><span class="sxs-lookup"><span data-stu-id="e5dad-162">If you specify `/SetContentType` without a value, then AzCopy will set each blob or file's content type according to its file extension.</span></span>

```azcopy
AzCopy /Source:C:\myfolder\ /Dest:https://myaccount.blob.core.windows.net/myContainer/ /DestKey:key /Pattern:ab /SetContentType
```

## <a name="blob-copy"></a><span data-ttu-id="e5dad-163">Blob：複製</span><span class="sxs-lookup"><span data-stu-id="e5dad-163">Blob: Copy</span></span>
### <a name="copy-single-blob-within-storage-account"></a><span data-ttu-id="e5dad-164">複製儲存體帳戶內的單一 Blob</span><span class="sxs-lookup"><span data-stu-id="e5dad-164">Copy single blob within Storage account</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer1 /Dest:https://myaccount.blob.core.windows.net/mycontainer2 /SourceKey:key /DestKey:key /Pattern:abc.txt
```

<span data-ttu-id="e5dad-165">當您複製儲存體帳戶內的 Blob 時，系統會執行 [伺服器端複製](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) 作業。</span><span class="sxs-lookup"><span data-stu-id="e5dad-165">When you copy a blob within a Storage account, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="copy-single-blob-across-storage-accounts"></a><span data-ttu-id="e5dad-166">跨儲存體帳戶複製單一 Blob</span><span class="sxs-lookup"><span data-stu-id="e5dad-166">Copy single blob across Storage accounts</span></span>

```azcopy
AzCopy /Source:https://sourceaccount.blob.core.windows.net/mycontainer1 /Dest:https://destaccount.blob.core.windows.net/mycontainer2 /SourceKey:key1 /DestKey:key2 /Pattern:abc.txt
```

<span data-ttu-id="e5dad-167">當您跨儲存體帳戶複製 Blob 時，系統會執行 [伺服器端複製](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) 作業。</span><span class="sxs-lookup"><span data-stu-id="e5dad-167">When you copy a blob across Storage accounts, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="copy-single-blob-from-secondary-region-to-primary-region"></a><span data-ttu-id="e5dad-168">將單一 Blob 從次要地區複製到主要區域</span><span class="sxs-lookup"><span data-stu-id="e5dad-168">Copy single blob from secondary region to primary region</span></span>

```azcopy
AzCopy /Source:https://myaccount1-secondary.blob.core.windows.net/mynewcontainer1 /Dest:https://myaccount2.blob.core.windows.net/mynewcontainer2 /SourceKey:key1 /DestKey:key2 /Pattern:abc.txt
```

<span data-ttu-id="e5dad-169">請注意，您必須啟用讀取權限異地備援儲存體。</span><span class="sxs-lookup"><span data-stu-id="e5dad-169">Note that you must have read-access geo-redundant storage enabled.</span></span>

### <a name="copy-single-blob-and-its-snapshots-across-storage-accounts"></a><span data-ttu-id="e5dad-170">跨儲存體帳戶複製單一 Blob 及其快照</span><span class="sxs-lookup"><span data-stu-id="e5dad-170">Copy single blob and its snapshots across Storage accounts</span></span>

```azcopy
    AzCopy /Source:https://sourceaccount.blob.core.windows.net/mycontainer1 /Dest:https://destaccount.blob.core.windows.net/mycontainer2 /SourceKey:key1 /DestKey:key2 /Pattern:abc.txt /Snapshot
```

<span data-ttu-id="e5dad-171">複製作業之後，目標容器將包含 Blob 及其快照。</span><span class="sxs-lookup"><span data-stu-id="e5dad-171">After the copy operation, the target container will include the blob and its snapshots.</span></span> <span data-ttu-id="e5dad-172">假設上述範例中的 Blob 有兩份快照，則容器將包含下列 Blob 及快照：</span><span class="sxs-lookup"><span data-stu-id="e5dad-172">Assuming the blob in the example above has two snapshots, the container will include the following blob and snapshots:</span></span>

    abc.txt
    abc (2013-02-25 080757).txt
    abc (2014-02-21 150331).txt

### <a name="synchronously-copy-blobs-across-storage-accounts"></a><span data-ttu-id="e5dad-173">以同步方式跨儲存體帳戶複製 Blob</span><span class="sxs-lookup"><span data-stu-id="e5dad-173">Synchronously copy blobs across Storage accounts</span></span>
<span data-ttu-id="e5dad-174">根據預設，AzCopy 會以非同步方式在兩個儲存體端點之間複製資料。</span><span class="sxs-lookup"><span data-stu-id="e5dad-174">AzCopy by default copies data between two storage endpoints asynchronously.</span></span> <span data-ttu-id="e5dad-175">因此，複製作業會在背景中執行，並使用在 blob 複製速度方面沒有 SLA 的備用頻寬容量，而 AzCopy 會定期檢查複製狀態，直到複製完成或失敗為止。</span><span class="sxs-lookup"><span data-stu-id="e5dad-175">Therefore, the copy operation will run in the background using spare bandwidth capacity that has no SLA in terms of how fast a blob will be copied, and AzCopy will periodically check the copy status until the copying is completed or failed.</span></span>

<span data-ttu-id="e5dad-176">`/SyncCopy` 選項可確保複製作業達到一致的速度。</span><span class="sxs-lookup"><span data-stu-id="e5dad-176">The `/SyncCopy` option ensures that the copy operation will get consistent speed.</span></span> <span data-ttu-id="e5dad-177">AzCopy 執行同步複製的方式是先將要複製的 blob，從指定的來源下載到本機記憶體，再上傳至 Blob 儲存體目的地。</span><span class="sxs-lookup"><span data-stu-id="e5dad-177">AzCopy performs the synchronous copy by downloading the blobs to copy from the specified source to local memory, and then uploading them to the Blob storage destination.</span></span>

```azcopy
AzCopy /Source:https://myaccount1.blob.core.windows.net/myContainer/ /Dest:https://myaccount2.blob.core.windows.net/myContainer/ /SourceKey:key1 /DestKey:key2 /Pattern:ab /SyncCopy
```

<span data-ttu-id="e5dad-178">`/SyncCopy` 可能會產生額外的輸出成本，建議的方法是在與來源儲存體帳戶位於同一區域的 Azure VM 中使用這個選項，以避免產生輸出成本。</span><span class="sxs-lookup"><span data-stu-id="e5dad-178">`/SyncCopy` might generate additional egress cost compared to asynchronous copy, the recommended approach is to use this option in an Azure VM that is in the same region as your source storage account to avoid egress cost.</span></span>

## <a name="file-download"></a><span data-ttu-id="e5dad-179">檔案：下載</span><span class="sxs-lookup"><span data-stu-id="e5dad-179">File: Download</span></span>
### <a name="download-single-file"></a><span data-ttu-id="e5dad-180">下載單一檔案</span><span class="sxs-lookup"><span data-stu-id="e5dad-180">Download single file</span></span>

```azcopy
AzCopy /Source:https://myaccount.file.core.windows.net/myfileshare/myfolder1/ /Dest:C:\myfolder /SourceKey:key /Pattern:abc.txt
```

<span data-ttu-id="e5dad-181">如果指定的來源是 Azure 檔案共用，則您必須指定確切檔案名稱 (例如，`abc.txt`) 以下載單一檔案，或指定 `/S` 選項以遞迴方式下載共用中的所有檔案。</span><span class="sxs-lookup"><span data-stu-id="e5dad-181">If the specified source is an Azure file share, then you must either specify the exact file name, (*e.g.* `abc.txt`) to download a single file, or specify option `/S` to download all files in the share recursively.</span></span> <span data-ttu-id="e5dad-182">嘗試同時指定檔案模式和 `/S` 選項將會造成錯誤。</span><span class="sxs-lookup"><span data-stu-id="e5dad-182">Attempting to specify both a file pattern and option `/S` together will result in an error.</span></span>

### <a name="download-all-files"></a><span data-ttu-id="e5dad-183">下載所有檔案</span><span class="sxs-lookup"><span data-stu-id="e5dad-183">Download all files</span></span>

```azcopy
AzCopy /Source:https://myaccount.file.core.windows.net/myfileshare/ /Dest:C:\myfolder /SourceKey:key /S
```

<span data-ttu-id="e5dad-184">請注意，將不會下載任何空白資料夾。</span><span class="sxs-lookup"><span data-stu-id="e5dad-184">Note that any empty folders will not be downloaded.</span></span>

## <a name="file-upload"></a><span data-ttu-id="e5dad-185">檔案：上傳</span><span class="sxs-lookup"><span data-stu-id="e5dad-185">File: Upload</span></span>
### <a name="upload-single-file"></a><span data-ttu-id="e5dad-186">上傳單一檔案</span><span class="sxs-lookup"><span data-stu-id="e5dad-186">Upload single file</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.file.core.windows.net/myfileshare/ /DestKey:key /Pattern:abc.txt
```

### <a name="upload-all-files"></a><span data-ttu-id="e5dad-187">上傳所有檔案</span><span class="sxs-lookup"><span data-stu-id="e5dad-187">Upload all files</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.file.core.windows.net/myfileshare/ /DestKey:key /S
```

<span data-ttu-id="e5dad-188">請注意，將不會上傳任何空白資料夾。</span><span class="sxs-lookup"><span data-stu-id="e5dad-188">Note that any empty folders will not be uploaded.</span></span>

### <a name="upload-files-matching-specified-pattern"></a><span data-ttu-id="e5dad-189">上傳符合指定模式的檔案</span><span class="sxs-lookup"><span data-stu-id="e5dad-189">Upload files matching specified pattern</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.file.core.windows.net/myfileshare/ /DestKey:key /Pattern:ab* /S
```

## <a name="file-copy"></a><span data-ttu-id="e5dad-190">檔案：複製</span><span class="sxs-lookup"><span data-stu-id="e5dad-190">File: Copy</span></span>
### <a name="copy-across-file-shares"></a><span data-ttu-id="e5dad-191">跨檔案共用複製</span><span class="sxs-lookup"><span data-stu-id="e5dad-191">Copy across file shares</span></span>

```azcopy
AzCopy /Source:https://myaccount1.file.core.windows.net/myfileshare1/ /Dest:https://myaccount2.file.core.windows.net/myfileshare2/ /SourceKey:key1 /DestKey:key2 /S
```
<span data-ttu-id="e5dad-192">當您跨檔案共用複製檔案時，系統會執行[伺服器端複製](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx)作業。</span><span class="sxs-lookup"><span data-stu-id="e5dad-192">When you copy a file across file shares, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="copy-from-file-share-to-blob"></a><span data-ttu-id="e5dad-193">從檔案共用複製到 Blob</span><span class="sxs-lookup"><span data-stu-id="e5dad-193">Copy from file share to blob</span></span>

```azcopy
AzCopy /Source:https://myaccount1.file.core.windows.net/myfileshare/ /Dest:https://myaccount2.blob.core.windows.net/mycontainer/ /SourceKey:key1 /DestKey:key2 /S
```
<span data-ttu-id="e5dad-194">當您將檔案從檔案共用複製到 Blob 時，系統會執行[伺服器端複製](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx)作業。</span><span class="sxs-lookup"><span data-stu-id="e5dad-194">When you copy a file from file share to blob, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>


### <a name="copy-from-blob-to-file-share"></a><span data-ttu-id="e5dad-195">從 Blob 複製到檔案共用</span><span class="sxs-lookup"><span data-stu-id="e5dad-195">Copy from blob to file share</span></span>

```azcopy
AzCopy /Source:https://myaccount1.blob.core.windows.net/mycontainer/ /Dest:https://myaccount2.file.core.windows.net/myfileshare/ /SourceKey:key1 /DestKey:key2 /S
```
<span data-ttu-id="e5dad-196">當您將檔案從 Blob 複製到檔案共用時，系統會執行[伺服器端複製](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx)作業。</span><span class="sxs-lookup"><span data-stu-id="e5dad-196">When you copy a file from blob to file share, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="synchronously-copy-files"></a><span data-ttu-id="e5dad-197">以同步方式複製檔案</span><span class="sxs-lookup"><span data-stu-id="e5dad-197">Synchronously copy files</span></span>
<span data-ttu-id="e5dad-198">您可以指定 `/SyncCopy` 選項，以同步方式從檔案儲存體複製資料到檔案儲存體、從檔案儲存體複製資料到 Blob 儲存體，以及從 Blob 儲存體複製資料到檔案儲存體，AzCopy 會將來源資料下載至本機記憶體，並重新上傳到目的地，來執行此項作業。</span><span class="sxs-lookup"><span data-stu-id="e5dad-198">You can specify the `/SyncCopy` option to copy data from File Storage to File Storage, from File Storage to Blob Storage and from Blob Storage to File Storage synchronously, AzCopy does this by downloading the source data to local memory and upload it again to destination.</span></span> <span data-ttu-id="e5dad-199">此作業會產生標準輸出成本。</span><span class="sxs-lookup"><span data-stu-id="e5dad-199">Standard egress cost will apply.</span></span>

```azcopy
AzCopy /Source:https://myaccount1.file.core.windows.net/myfileshare1/ /Dest:https://myaccount2.file.core.windows.net/myfileshare2/ /SourceKey:key1 /DestKey:key2 /S /SyncCopy
```

<span data-ttu-id="e5dad-200">從檔案儲存體複製到 Blob 儲存體時，預設的 Blob 類型是區塊 Blob，使用者可以指定 `/BlobType:page` 選項來變更目的地 Blob 類型。</span><span class="sxs-lookup"><span data-stu-id="e5dad-200">When copying from File Storage to Blob Storage, the default blob type is block blob, user can specify option `/BlobType:page` to change the destination blob type.</span></span>

<span data-ttu-id="e5dad-201">請注意，相較於非同步複製， `/SyncCopy` 可能會產生額外的輸出成本，建議的方法是在與來源儲存體帳戶位於同一區域的 Azure VM 中使用這個選項，以避免產生輸出成本。</span><span class="sxs-lookup"><span data-stu-id="e5dad-201">Note that `/SyncCopy` might generate additional egress cost comparing to asynchronous copy, the recommended approach is to use this option in the Azure VM which is in the same region as your source storage account to avoid egress cost.</span></span>

## <a name="table-export"></a><span data-ttu-id="e5dad-202">資料表：匯出</span><span class="sxs-lookup"><span data-stu-id="e5dad-202">Table: Export</span></span>
### <a name="export-table"></a><span data-ttu-id="e5dad-203">匯出資料表</span><span class="sxs-lookup"><span data-stu-id="e5dad-203">Export table</span></span>

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:C:\myfolder\ /SourceKey:key
```

<span data-ttu-id="e5dad-204">AzCopy 會將資訊清單檔寫入至指定的目的地資料夾。</span><span class="sxs-lookup"><span data-stu-id="e5dad-204">AzCopy writes a manifest file to the specified destination folder.</span></span> <span data-ttu-id="e5dad-205">匯入程序會使用資訊清單檔案來尋找必要的資料檔案，並執行資料驗證。</span><span class="sxs-lookup"><span data-stu-id="e5dad-205">The manifest file is used in the import process to locate the necessary data files and perform data validation.</span></span> <span data-ttu-id="e5dad-206">資訊清單檔預設會使用下列命令慣例：</span><span class="sxs-lookup"><span data-stu-id="e5dad-206">The manifest file uses the following naming convention by default:</span></span>

    <account name>_<table name>_<timestamp>.manifest

<span data-ttu-id="e5dad-207">使用者也可以指定 `/Manifest:<manifest file name>` 選項，設定資訊清單檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="e5dad-207">User can also specify the option `/Manifest:<manifest file name>` to set the manifest file name.</span></span>

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:C:\myfolder\ /SourceKey:key /Manifest:abc.manifest
```

### <a name="split-export-into-multiple-files"></a><span data-ttu-id="e5dad-208">將匯出分割成多個檔案</span><span class="sxs-lookup"><span data-stu-id="e5dad-208">Split export into multiple files</span></span>

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/mytable/ /Dest:C:\myfolder /SourceKey:key /S /SplitSize:100
```

<span data-ttu-id="e5dad-209">AzCopy 會在分割資料檔案名稱中使用 *磁碟區索引* ，以區分多個檔案。</span><span class="sxs-lookup"><span data-stu-id="e5dad-209">AzCopy uses a *volume index* in the split data file names to distinguish multiple files.</span></span> <span data-ttu-id="e5dad-210">磁碟區索引由兩部分組成：資料分割索引鍵範圍索引和分割檔案索引。</span><span class="sxs-lookup"><span data-stu-id="e5dad-210">The volume index consists of two parts, a *partition key range index* and a *split file index*.</span></span> <span data-ttu-id="e5dad-211">兩個索引皆以零為基礎。</span><span class="sxs-lookup"><span data-stu-id="e5dad-211">Both indexes are zero-based.</span></span>

<span data-ttu-id="e5dad-212">如果使用者未指定 `/PKRS`選項，資料分割索引鍵範圍索引將會是 0。</span><span class="sxs-lookup"><span data-stu-id="e5dad-212">The partition key range index will be 0 if user does not specify option `/PKRS`.</span></span>

<span data-ttu-id="e5dad-213">例如，在使用者指定 `/SplitSize`選項之後，假設 AzCopy 產生兩個資料檔。</span><span class="sxs-lookup"><span data-stu-id="e5dad-213">For instance, suppose AzCopy generates two data files after the user specifies option `/SplitSize`.</span></span> <span data-ttu-id="e5dad-214">產生的資料檔案名稱可能會是：</span><span class="sxs-lookup"><span data-stu-id="e5dad-214">The resulting data file names might be:</span></span>

    myaccount_mytable_20140903T051850.8128447Z_0_0_C3040FE8.json
    myaccount_mytable_20140903T051850.8128447Z_0_1_0AB9AC20.json

<span data-ttu-id="e5dad-215">請注意， `/SplitSize` 選項的最小可能值為 32MB。</span><span class="sxs-lookup"><span data-stu-id="e5dad-215">Note that the minimum possible value for option `/SplitSize` is 32MB.</span></span> <span data-ttu-id="e5dad-216">如果指定的目的地是 Blob 儲存體，則 AzCopy 會分割已達到 Blob 大小限制 (200GB) 的資料檔，而不論使用者是否已指定 `/SplitSize` 選項。</span><span class="sxs-lookup"><span data-stu-id="e5dad-216">If the specified destination is Blob storage, AzCopy will split the data file once its sizes reaches the blob size limitation (200GB), regardless of whether option `/SplitSize` has been specified by the user.</span></span>

### <a name="export-table-to-json-or-csv-data-file-format"></a><span data-ttu-id="e5dad-217">將資料表匯出為 JSON 或 CSV 資料檔案格式</span><span class="sxs-lookup"><span data-stu-id="e5dad-217">Export table to JSON or CSV data file format</span></span>
<span data-ttu-id="e5dad-218">AzCopy 依預設會將資料表匯出至 JSON 資料檔。</span><span class="sxs-lookup"><span data-stu-id="e5dad-218">AzCopy by default exports tables to JSON data files.</span></span> <span data-ttu-id="e5dad-219">您可以指定選項 `/PayloadFormat:JSON|CSV` 以將資料表匯出為 JSON 或 CSV。</span><span class="sxs-lookup"><span data-stu-id="e5dad-219">You can specify the option `/PayloadFormat:JSON|CSV` to export the tables as JSON or CSV.</span></span>

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:C:\myfolder\ /SourceKey:key /PayloadFormat:CSV
```

<span data-ttu-id="e5dad-220">在指定 CSV 裝載格式時，AzCopy 也會產生結構描述檔案，且每個資料檔的副檔名為 `.schema.csv` 。</span><span class="sxs-lookup"><span data-stu-id="e5dad-220">When specifying the CSV payload format, AzCopy will also generate a schema file with file extension `.schema.csv` for each data file.</span></span>

### <a name="export-table-entities-concurrently"></a><span data-ttu-id="e5dad-221">並行匯出資料表實體</span><span class="sxs-lookup"><span data-stu-id="e5dad-221">Export table entities concurrently</span></span>

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:C:\myfolder\ /SourceKey:key /PKRS:"aa#bb"
```

<span data-ttu-id="e5dad-222">當使用者指定 `/PKRS`選項時，AzCopy 將會啟動並行作業以匯出實體。</span><span class="sxs-lookup"><span data-stu-id="e5dad-222">AzCopy will start concurrent operations to export entities when the user specifies option `/PKRS`.</span></span> <span data-ttu-id="e5dad-223">每個作業分別會匯出一個資料分割索引鍵範圍。</span><span class="sxs-lookup"><span data-stu-id="e5dad-223">Each operation exports one partition key range.</span></span>

<span data-ttu-id="e5dad-224">請注意，並行作業的數目也由 `/NC`選項控制。</span><span class="sxs-lookup"><span data-stu-id="e5dad-224">Note that the number of concurrent operations is also controlled by option `/NC`.</span></span> <span data-ttu-id="e5dad-225">在複製資料表實體時，即使未指定 `/NC`，AzCopy 會以核心處理器的數目作為 `/NC` 的預設值。</span><span class="sxs-lookup"><span data-stu-id="e5dad-225">AzCopy uses the number of core processors as the default value of `/NC` when copying table entities, even if `/NC` was not specified.</span></span> <span data-ttu-id="e5dad-226">當使用者指定 `/PKRS`選項時，AzCopy 會從兩個值 (資料分割索引鍵範圍和隱含或明確指定的並行作業) 中選擇較小者來使用，以決定要啟動的並行作業數目。</span><span class="sxs-lookup"><span data-stu-id="e5dad-226">When the user specifies option `/PKRS`, AzCopy uses the smaller of the two values - partition key ranges versus implicitly or explicitly specified concurrent operations - to determine the number of concurrent operations to start.</span></span> <span data-ttu-id="e5dad-227">如需詳細資訊，請在命令列上輸入 `AzCopy /?:NC` 。</span><span class="sxs-lookup"><span data-stu-id="e5dad-227">For more details, type `AzCopy /?:NC` at the command line.</span></span>

### <a name="export-table-to-blob"></a><span data-ttu-id="e5dad-228">將資料表匯出至 Blob</span><span class="sxs-lookup"><span data-stu-id="e5dad-228">Export table to blob</span></span>

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:https://myaccount.blob.core.windows.net/mycontainer/ /SourceKey:key1 /Destkey:key2
```

<span data-ttu-id="e5dad-229">AzCopy 將會使用下列命令慣例，在 Blob 容器中產生 JSON 資料檔案：</span><span class="sxs-lookup"><span data-stu-id="e5dad-229">AzCopy will generate a JSON data file into the blob container with following naming convention:</span></span>

    <account name>_<table name>_<timestamp>_<volume index>_<CRC>.json

<span data-ttu-id="e5dad-230">產生的 JSON 資料檔案會遵循基本中繼資料的裝載格式。</span><span class="sxs-lookup"><span data-stu-id="e5dad-230">The generated JSON data file follows the payload format for minimal metadata.</span></span> <span data-ttu-id="e5dad-231">如需此裝載格式的詳細資訊，請參閱 [資料表服務作業的裝載格式](http://msdn.microsoft.com/library/azure/dn535600.aspx)。</span><span class="sxs-lookup"><span data-stu-id="e5dad-231">For details on this payload format, see [Payload Format for Table Service Operations](http://msdn.microsoft.com/library/azure/dn535600.aspx).</span></span>

<span data-ttu-id="e5dad-232">請注意，在將資料表匯出至 Blob 時，AzCopy 會先將資料表實體下載到本機暫存資料檔，再將這些實體上傳至 Blob。</span><span class="sxs-lookup"><span data-stu-id="e5dad-232">Note that when exporting tables to blobs, AzCopy will download the Table entities to local temporary data files and then upload those entities to the blob.</span></span> <span data-ttu-id="e5dad-233">這些暫存資料檔會放入日誌檔案資料夾中，預設路徑為 "<code>%LocalAppData%\Microsoft\Azure\AzCopy</code>"，您可以指定 /Z:[journal-file-folder] 選項來變更日誌檔案資料夾位置，從而變更暫存資料檔位置。</span><span class="sxs-lookup"><span data-stu-id="e5dad-233">These temporary data files are put into the journal file folder with the default path "<code>%LocalAppData%\Microsoft\Azure\AzCopy</code>", you can specify option /Z:[journal-file-folder] to change the journal file folder location and thus change the temporary data files location.</span></span> <span data-ttu-id="e5dad-234">暫存資料檔大小取決於資料表實體大小和您使用 /SplitSize 選項所指定的大小，雖然本機磁碟中的暫存資料檔在上傳至 Blob 之後就立即刪除，但請確定您有足夠的本機磁碟空間，以儲存尚未刪除的暫存資料檔。</span><span class="sxs-lookup"><span data-stu-id="e5dad-234">The temporary data files' size is decided by your table entities' size and the size you specified with the option /SplitSize, although the temporary data file in local disk will be deleted instantly once it has been uploaded to the blob, please make sure you have enough local disk space to store these temporary data files before they are deleted.</span></span>

## <a name="table-import"></a><span data-ttu-id="e5dad-235">資料表：匯入</span><span class="sxs-lookup"><span data-stu-id="e5dad-235">Table: Import</span></span>
### <a name="import-table"></a><span data-ttu-id="e5dad-236">匯入資料表</span><span class="sxs-lookup"><span data-stu-id="e5dad-236">Import table</span></span>

```azcopy
AzCopy /Source:C:\myfolder\ /Dest:https://myaccount.table.core.windows.net/mytable1/ /DestKey:key /Manifest:"myaccount_mytable_20140103T112020.manifest" /EntityOperation:InsertOrReplace
```

<span data-ttu-id="e5dad-237">選項 `/EntityOperation` 指出如何將實體插入資料表。</span><span class="sxs-lookup"><span data-stu-id="e5dad-237">The option `/EntityOperation` indicates how to insert entities into the table.</span></span> <span data-ttu-id="e5dad-238">可能的值包括：</span><span class="sxs-lookup"><span data-stu-id="e5dad-238">Possible values are:</span></span>

* <span data-ttu-id="e5dad-239">`InsertOrSkip`：略過現有實體，或插入新實體 (若不存在於資料表中)。</span><span class="sxs-lookup"><span data-stu-id="e5dad-239">`InsertOrSkip`: Skips an existing entity or inserts a new entity if it does not exist in the table.</span></span>
* <span data-ttu-id="e5dad-240">`InsertOrMerge`：合併現有實體，或插入新實體 (若不存在於資料表中)。</span><span class="sxs-lookup"><span data-stu-id="e5dad-240">`InsertOrMerge`: Merges an existing entity or inserts a new entity if it does not exist in the table.</span></span>
* <span data-ttu-id="e5dad-241">`InsertOrReplace`：取代現有實體，或插入新實體 (若不存在於資料表中)。</span><span class="sxs-lookup"><span data-stu-id="e5dad-241">`InsertOrReplace`: Replaces an existing entity or inserts a new entity if it does not exist in the table.</span></span>

<span data-ttu-id="e5dad-242">請注意，您無法在匯入案例中指定 `/PKRS` 選項。</span><span class="sxs-lookup"><span data-stu-id="e5dad-242">Note that you cannot specify option `/PKRS` in the import scenario.</span></span> <span data-ttu-id="e5dad-243">不同於必須指定 `/PKRS` 選項以啟動並行作業的匯出案例，AzCopy 依預設會在您匯入資料表時啟動並行作業。</span><span class="sxs-lookup"><span data-stu-id="e5dad-243">Unlike the export scenario, in which you must specify option `/PKRS` to start concurrent operations, AzCopy will by default start concurrent operations when you import a table.</span></span> <span data-ttu-id="e5dad-244">依預設啟動的並行作業數目等於核心處理器的數目；但您可以使用 `/NC`選項指定不同的並行數目。</span><span class="sxs-lookup"><span data-stu-id="e5dad-244">The default number of concurrent operations started is equal to the number of core processors; however, you can specify a different number of concurrent with option `/NC`.</span></span> <span data-ttu-id="e5dad-245">如需詳細資訊，請在命令列上輸入 `AzCopy /?:NC` 。</span><span class="sxs-lookup"><span data-stu-id="e5dad-245">For more details, type `AzCopy /?:NC` at the command line.</span></span>

<span data-ttu-id="e5dad-246">請注意，AzCopy 只支援匯入 JSON 而不支援匯入 CSV。</span><span class="sxs-lookup"><span data-stu-id="e5dad-246">Note that AzCopy only supports importing for JSON, not CSV.</span></span> <span data-ttu-id="e5dad-247">AzCopy 不支援從使用者建立的 JSON 和資訊清單檔案匯入資料表。</span><span class="sxs-lookup"><span data-stu-id="e5dad-247">AzCopy does not support table imports from user-created JSON and manifest files.</span></span> <span data-ttu-id="e5dad-248">這兩種檔案都必須來自 AzCopy 資料表匯出。</span><span class="sxs-lookup"><span data-stu-id="e5dad-248">Both of these files must come from an AzCopy table export.</span></span> <span data-ttu-id="e5dad-249">若要避免錯誤，請勿修改匯出的 JSON 或資訊清單檔案。</span><span class="sxs-lookup"><span data-stu-id="e5dad-249">To avoid errors, please do not modify the exported JSON or manifest file.</span></span>

### <a name="import-entities-to-table-using-blobs"></a><span data-ttu-id="e5dad-250">使用 Blob 將實體匯入至資料表</span><span class="sxs-lookup"><span data-stu-id="e5dad-250">Import entities to table using blobs</span></span>
<span data-ttu-id="e5dad-251">假設有 Blob 容器包含下列檔案：代表 Azure 資料表和其隨附資訊清單檔案的 JSON 檔案。</span><span class="sxs-lookup"><span data-stu-id="e5dad-251">Assume a Blob container contains the following: A JSON file representing an Azure Table and its accompanying manifest file.</span></span>

    myaccount_mytable_20140103T112020.manifest
    myaccount_mytable_20140103T112020_0_0_0AF395F1DC42E952.json

<span data-ttu-id="e5dad-252">您可以執行下列命令，以使用該 Blob 容器中的資訊清單檔案將實體匯入資料表中：</span><span class="sxs-lookup"><span data-stu-id="e5dad-252">You can run the following command to import entities into a table using the manifest file in that blob container:</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:https://myaccount.table.core.windows.net/mytable /SourceKey:key1 /DestKey:key2 /Manifest:"myaccount_mytable_20140103T112020.manifest" /EntityOperation:"InsertOrReplace"
```

## <a name="other-azcopy-features"></a><span data-ttu-id="e5dad-253">其他 AzCopy 功能</span><span class="sxs-lookup"><span data-stu-id="e5dad-253">Other AzCopy features</span></span>
### <a name="only-copy-data-that-doesnt-exist-in-the-destination"></a><span data-ttu-id="e5dad-254">只複製目的地中沒有的資料</span><span class="sxs-lookup"><span data-stu-id="e5dad-254">Only copy data that doesn't exist in the destination</span></span>
<span data-ttu-id="e5dad-255">`/XO` 和 `/XN` 參數分別可讓您在複製作業中排除較舊或較新的來源資源。</span><span class="sxs-lookup"><span data-stu-id="e5dad-255">The `/XO` and `/XN` parameters allow you to exclude older or newer source resources from being copied, respectively.</span></span> <span data-ttu-id="e5dad-256">如果您只想複製目的地中沒有的來源資源，則可以在 AzCopy 命令中同時指定這兩個參數：</span><span class="sxs-lookup"><span data-stu-id="e5dad-256">If you only want to copy source resources that don't exist in the destination, you can specify both parameters in the AzCopy command:</span></span>

    /Source:http://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:<sourcekey> /S /XO /XN

    /Source:C:\myfolder /Dest:http://myaccount.file.core.windows.net/myfileshare /DestKey:<destkey> /S /XO /XN

    /Source:http://myaccount.blob.core.windows.net/mycontainer /Dest:http://myaccount.blob.core.windows.net/mycontainer1 /SourceKey:<sourcekey> /DestKey:<destkey> /S /XO /XN

<span data-ttu-id="e5dad-257">注意，當來源或目的地其中之一是資料表時，不支援此做法。</span><span class="sxs-lookup"><span data-stu-id="e5dad-257">Note that this is not supported when either the source or destination is a table.</span></span>

### <a name="use-a-response-file-to-specify-command-line-parameters"></a><span data-ttu-id="e5dad-258">使用回應檔案指定命令列參數</span><span class="sxs-lookup"><span data-stu-id="e5dad-258">Use a response file to specify command-line parameters</span></span>

```azcopy
AzCopy /@:"C:\responsefiles\copyoperation.txt"
```

<span data-ttu-id="e5dad-259">您可以在回應檔案中包含任何 AzCopy 命令列參數。</span><span class="sxs-lookup"><span data-stu-id="e5dad-259">You can include any AzCopy command-line parameters in a response file.</span></span> <span data-ttu-id="e5dad-260">AzCopy 處理檔案中的參數，就好像在命令列上指定這些參數一様，執行使用檔案內容的直接取代。</span><span class="sxs-lookup"><span data-stu-id="e5dad-260">AzCopy processes the parameters in the file as if they had been specified on the command line, performing a direct substitution with the contents of the file.</span></span>

<span data-ttu-id="e5dad-261">假設名為 `copyoperation.txt`且包含下列資料行的回應檔案。</span><span class="sxs-lookup"><span data-stu-id="e5dad-261">Assume a response file named `copyoperation.txt`, that contains the following lines.</span></span> <span data-ttu-id="e5dad-262">每個 AzCopy 參數可以指定在同一行</span><span class="sxs-lookup"><span data-stu-id="e5dad-262">Each AzCopy parameter can be specified on a single line</span></span>

    /Source:http://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:<sourcekey> /S /Y

<span data-ttu-id="e5dad-263">或不同行：</span><span class="sxs-lookup"><span data-stu-id="e5dad-263">or on separate lines:</span></span>

    /Source:http://myaccount.blob.core.windows.net/mycontainer
    /Dest:C:\myfolder
    /SourceKey:<sourcekey>
    /S
    /Y

<span data-ttu-id="e5dad-264">如果您將參數分割成兩行，如以下的 `/sourcekey` 參數所示，則 AzCopy 將會失敗：</span><span class="sxs-lookup"><span data-stu-id="e5dad-264">AzCopy will fail if you split the parameter across two lines, as shown here for the `/sourcekey` parameter:</span></span>

    http://myaccount.blob.core.windows.net/mycontainer
     C:\myfolder
    /sourcekey:
    <sourcekey>
    /S
    /Y

### <a name="use-multiple-response-files-to-specify-command-line-parameters"></a><span data-ttu-id="e5dad-265">使用多個回應檔案指定命令列參數</span><span class="sxs-lookup"><span data-stu-id="e5dad-265">Use multiple response files to specify command-line parameters</span></span>
<span data-ttu-id="e5dad-266">假設名為 `source.txt` 且指定來源容器的回應檔案：</span><span class="sxs-lookup"><span data-stu-id="e5dad-266">Assume a response file named `source.txt` that specifies a source container:</span></span>

    /Source:http://myaccount.blob.core.windows.net/mycontainer

<span data-ttu-id="e5dad-267">及名為 `dest.txt` 且在檔案系統中指定目的地資料夾的回應檔案：</span><span class="sxs-lookup"><span data-stu-id="e5dad-267">And a response file named `dest.txt` that specifies a destination folder in the file system:</span></span>

    /Dest:C:\myfolder

<span data-ttu-id="e5dad-268">及名為 `options.txt` 且指定 AzCopy 選項的回應檔案：</span><span class="sxs-lookup"><span data-stu-id="e5dad-268">And a response file named `options.txt` that specifies options for AzCopy:</span></span>

    /S /Y

<span data-ttu-id="e5dad-269">若要使用這些回應檔案 (所有這些檔案皆位於 `C:\responsefiles`目錄內) 呼叫 AzCopy，請使用此命令：</span><span class="sxs-lookup"><span data-stu-id="e5dad-269">To call AzCopy with these response files, all of which reside in a directory `C:\responsefiles`, use this command:</span></span>

```azcopy
AzCopy /@:"C:\responsefiles\source.txt" /@:"C:\responsefiles\dest.txt" /SourceKey:<sourcekey> /@:"C:\responsefiles\options.txt"   
```

<span data-ttu-id="e5dad-270">AzCopy 處理此命令，就好像您在命令列上包含所有個別參數一樣：</span><span class="sxs-lookup"><span data-stu-id="e5dad-270">AzCopy processes this command just as it would if you included all of the individual parameters on the command line:</span></span>

```azcopy
AzCopy /Source:http://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:<sourcekey> /S /Y
```

### <a name="specify-a-shared-access-signature-sas"></a><span data-ttu-id="e5dad-271">指定共用存取簽章 (SAS)</span><span class="sxs-lookup"><span data-stu-id="e5dad-271">Specify a shared access signature (SAS)</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer1 /Dest:https://myaccount.blob.core.windows.net/mycontainer2 /SourceSAS:SAS1 /DestSAS:SAS2 /Pattern:abc.txt
```

<span data-ttu-id="e5dad-272">您也可以在容器 URI 上指定 SAS：</span><span class="sxs-lookup"><span data-stu-id="e5dad-272">You can also specify a SAS on the container URI:</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer1/?SourceSASToken /Dest:C:\myfolder /S
```

### <a name="journal-file-folder"></a><span data-ttu-id="e5dad-273">日誌檔案資料夾</span><span class="sxs-lookup"><span data-stu-id="e5dad-273">Journal file folder</span></span>
<span data-ttu-id="e5dad-274">每次發佈命令至 AzCopy 時，它會檢查預設資料夾或透過此選項指定的資料夾中是否有日誌檔案存在。</span><span class="sxs-lookup"><span data-stu-id="e5dad-274">Each time you issue a command to AzCopy, it checks whether a journal file exists in the default folder, or whether it exists in a folder that you specified via this option.</span></span> <span data-ttu-id="e5dad-275">如果在這兩個地方都找不到日誌檔案，AzCopy 會將此作業視為新的作業，並產生新的日誌檔案。</span><span class="sxs-lookup"><span data-stu-id="e5dad-275">If the journal file does not exist in either place, AzCopy treats the operation as new and generates a new journal file.</span></span>

<span data-ttu-id="e5dad-276">如果找到日誌檔案，則 AzCopy 將檢查所輸入的命令列是否符合日誌檔案中的命令列。</span><span class="sxs-lookup"><span data-stu-id="e5dad-276">If the journal file does exist, AzCopy will check whether the command line that you input matches the command line in the journal file.</span></span> <span data-ttu-id="e5dad-277">如果這兩個命令列相符，AzCopy 便會繼續未完成的作業。</span><span class="sxs-lookup"><span data-stu-id="e5dad-277">If the two command lines match, AzCopy resumes the incomplete operation.</span></span> <span data-ttu-id="e5dad-278">如果這兩個命令列不符，系統將提示您覆寫日誌檔案並開始新的作業，或取消目前作業。</span><span class="sxs-lookup"><span data-stu-id="e5dad-278">If they do not match, you will be prompted to either overwrite the journal file to start a new operation, or to cancel the current operation.</span></span>

<span data-ttu-id="e5dad-279">如果您想要使用預設的日誌檔案位置：</span><span class="sxs-lookup"><span data-stu-id="e5dad-279">If you want to use the default location for the journal file:</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Z
```

<span data-ttu-id="e5dad-280">如果省略 `/Z`，或指定 `/Z` 選項但沒有指定資料夾路徑 (如上所示)，則 AzCopy 會在預設位置上建立日誌檔案，預設位置是 `%SystemDrive%\Users\%username%\AppData\Local\Microsoft\Azure\AzCopy`。</span><span class="sxs-lookup"><span data-stu-id="e5dad-280">If you omit option `/Z`, or specify option `/Z` without the folder path, as shown above, AzCopy creates the journal file in the default location, which is `%SystemDrive%\Users\%username%\AppData\Local\Microsoft\Azure\AzCopy`.</span></span> <span data-ttu-id="e5dad-281">如果日誌檔案已存在，則 AzCopy 會根據此日誌檔案繼續作業。</span><span class="sxs-lookup"><span data-stu-id="e5dad-281">If the journal file already exists, then AzCopy resumes the operation based on the journal file.</span></span>

<span data-ttu-id="e5dad-282">如果您想要指定自訂的日誌檔案位置：</span><span class="sxs-lookup"><span data-stu-id="e5dad-282">If you want to specify a custom location for the journal file:</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Z:C:\journalfolder\
```

<span data-ttu-id="e5dad-283">如果日誌檔案不存在，本範例將建立日誌檔案。</span><span class="sxs-lookup"><span data-stu-id="e5dad-283">This example creates the journal file if it does not already exist.</span></span> <span data-ttu-id="e5dad-284">如果日誌檔案已存在，則 AzCopy 會根據此日誌檔案繼續作業。</span><span class="sxs-lookup"><span data-stu-id="e5dad-284">If it does exist, then AzCopy resumes the operation based on the journal file.</span></span>

<span data-ttu-id="e5dad-285">如果您想要繼續 AzCopy 作業：</span><span class="sxs-lookup"><span data-stu-id="e5dad-285">If you want to resume an AzCopy operation:</span></span>

```azcopy
AzCopy /Z:C:\journalfolder\
```

<span data-ttu-id="e5dad-286">本範例會繼續最後一個無法完成的作業。</span><span class="sxs-lookup"><span data-stu-id="e5dad-286">This example resumes the last operation, which may have failed to complete.</span></span>

### <a name="generate-a-log-file"></a><span data-ttu-id="e5dad-287">產生記錄檔</span><span class="sxs-lookup"><span data-stu-id="e5dad-287">Generate a log file</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /V
```

<span data-ttu-id="e5dad-288">如果指定 `/V` 選項，但沒有提供詳細資訊記錄的檔案路徑，則 AzCopy 會在預設位置上建立記錄檔，預設位置是 `%SystemDrive%\Users\%username%\AppData\Local\Microsoft\Azure\AzCopy`。</span><span class="sxs-lookup"><span data-stu-id="e5dad-288">If you specify option `/V` without providing a file path to the verbose log, then AzCopy creates the log file in the default location, which is `%SystemDrive%\Users\%username%\AppData\Local\Microsoft\Azure\AzCopy`.</span></span>

<span data-ttu-id="e5dad-289">否則，您可以在自訂位置建立記錄檔：</span><span class="sxs-lookup"><span data-stu-id="e5dad-289">Otherwise, you can create an log file in a custom location:</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /V:C:\myfolder\azcopy1.log
```

<span data-ttu-id="e5dad-290">請注意，如果您在 `/V` 選項後面指定相對路徑 (例如 `/V:test/azcopy1.log`)，則系統會在目前工作目錄中的一個名為 `test` 的子資料夾內建立詳細資訊記錄。</span><span class="sxs-lookup"><span data-stu-id="e5dad-290">Note that if you specify a relative path following option `/V`, such as `/V:test/azcopy1.log`, then the verbose log is created in the current working directory within a subfolder named `test`.</span></span>

### <a name="specify-the-number-of-concurrent-operations-to-start"></a><span data-ttu-id="e5dad-291">指定要啟動的並行作業數目</span><span class="sxs-lookup"><span data-stu-id="e5dad-291">Specify the number of concurrent operations to start</span></span>
<span data-ttu-id="e5dad-292">`/NC` 選項可指定並行複製作業的數目。</span><span class="sxs-lookup"><span data-stu-id="e5dad-292">Option `/NC` specifies the number of concurrent copy operations.</span></span> <span data-ttu-id="e5dad-293">根據預設，AzCopy 依預設會啟動特定數量的並行作業，以提高資料傳輸的輸送量。</span><span class="sxs-lookup"><span data-stu-id="e5dad-293">By default, AzCopy starts a certain number of concurrent operations to increase the data transfer throughput.</span></span> <span data-ttu-id="e5dad-294">若為資料表作業，並行作業數目等於您所擁有的處理器數目。</span><span class="sxs-lookup"><span data-stu-id="e5dad-294">For Table operations, the number of concurrent operations is equal to the number of processors you have.</span></span> <span data-ttu-id="e5dad-295">若為 Blob 和檔案作業，並行作業數目等於您所擁有處理器數目的 8 倍。</span><span class="sxs-lookup"><span data-stu-id="e5dad-295">For Blob and File operations, the number of concurrent operations is equal 8 times the number of processors you have.</span></span> <span data-ttu-id="e5dad-296">如果您在低頻寬的網路上執行 AzCopy，則您可以在 /NC 中指定較低的數字，以避免因為資源競爭所導致的失敗。</span><span class="sxs-lookup"><span data-stu-id="e5dad-296">If you are running AzCopy across a low-bandwidth network, you can specify a lower number for /NC to avoid failure caused by resource competition.</span></span>

### <a name="run-azcopy-against-azure-storage-emulator"></a><span data-ttu-id="e5dad-297">針對 Azure 儲存體模擬器執行 AzCopy</span><span class="sxs-lookup"><span data-stu-id="e5dad-297">Run AzCopy against Azure Storage Emulator</span></span>
<span data-ttu-id="e5dad-298">您可以針對 Blob，對 [Azure 儲存體模擬器](storage-use-emulator.md) 執行 AzCopy：</span><span class="sxs-lookup"><span data-stu-id="e5dad-298">You can run AzCopy against the [Azure Storage Emulator](storage-use-emulator.md) for Blobs:</span></span>

```azcopy
AzCopy /Source:https://127.0.0.1:10000/myaccount/mycontainer/ /Dest:C:\myfolder /SourceKey:key /SourceType:Blob /S
```

<span data-ttu-id="e5dad-299">以及針對資料表來執行：</span><span class="sxs-lookup"><span data-stu-id="e5dad-299">and Tables:</span></span>

```azcopy
AzCopy /Source:https://127.0.0.1:10002/myaccount/mytable/ /Dest:C:\myfolder /SourceKey:key /SourceType:Table
```

## <a name="azcopy-parameters"></a><span data-ttu-id="e5dad-300">AzCopy 參數</span><span class="sxs-lookup"><span data-stu-id="e5dad-300">AzCopy Parameters</span></span>
<span data-ttu-id="e5dad-301">以下內容說明 AzCopy 的參數。</span><span class="sxs-lookup"><span data-stu-id="e5dad-301">Parameters for AzCopy are described below.</span></span> <span data-ttu-id="e5dad-302">您也可以從命令列中輸入下列其中一個命令，以取得 AzCopy 的使用說明：</span><span class="sxs-lookup"><span data-stu-id="e5dad-302">You can also type one of the following commands from the command line for help in using AzCopy:</span></span>

* <span data-ttu-id="e5dad-303">如需 AzCopy 的詳細命令列說明： `AzCopy /?`</span><span class="sxs-lookup"><span data-stu-id="e5dad-303">For detailed command-line help for AzCopy: `AzCopy /?`</span></span>
* <span data-ttu-id="e5dad-304">如需任何 AzCopy 參數的詳細說明： `AzCopy /?:SourceKey`</span><span class="sxs-lookup"><span data-stu-id="e5dad-304">For detailed help with any AzCopy parameter: `AzCopy /?:SourceKey`</span></span>
* <span data-ttu-id="e5dad-305">如需命令列範例： `AzCopy /?:Samples`</span><span class="sxs-lookup"><span data-stu-id="e5dad-305">For command-line examples: `AzCopy /?:Samples`</span></span>

### <a name="sourcesource"></a><span data-ttu-id="e5dad-306">/Source:"source"</span><span class="sxs-lookup"><span data-stu-id="e5dad-306">/Source:"source"</span></span>
<span data-ttu-id="e5dad-307">指定要複製的來源資料。</span><span class="sxs-lookup"><span data-stu-id="e5dad-307">Specifies the source data from which to copy.</span></span> <span data-ttu-id="e5dad-308">來源可以是檔案系統目錄、Blob 容器、Blob 虛擬目錄、儲存體檔案共用、儲存體檔案目錄或 Azure 資料表。</span><span class="sxs-lookup"><span data-stu-id="e5dad-308">The source can be a file system directory, a blob container, a blob virtual directory, a storage file share, a storage file directory, or an Azure table.</span></span>

<span data-ttu-id="e5dad-309">**適用於：** Blob、檔案、資料表</span><span class="sxs-lookup"><span data-stu-id="e5dad-309">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="destdestination"></a><span data-ttu-id="e5dad-310">/Dest:"destination"</span><span class="sxs-lookup"><span data-stu-id="e5dad-310">/Dest:"destination"</span></span>
<span data-ttu-id="e5dad-311">指定複製的目的地。</span><span class="sxs-lookup"><span data-stu-id="e5dad-311">Specifies the destination to copy to.</span></span> <span data-ttu-id="e5dad-312">目的地可以是檔案系統目錄、Blob 容器、Blob 虛擬目錄、儲存體檔案共用、儲存體檔案目錄或 Azure 資料表。</span><span class="sxs-lookup"><span data-stu-id="e5dad-312">The destination can be a file system directory, a blob container, a blob virtual directory, a storage file share, a storage file directory, or an Azure table.</span></span>

<span data-ttu-id="e5dad-313">**適用於：** Blob、檔案、資料表</span><span class="sxs-lookup"><span data-stu-id="e5dad-313">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="patternfile-pattern"></a><span data-ttu-id="e5dad-314">/Pattern:"file-pattern"</span><span class="sxs-lookup"><span data-stu-id="e5dad-314">/Pattern:"file-pattern"</span></span>
<span data-ttu-id="e5dad-315">指定一個檔案模式以指出所要複製的檔案。</span><span class="sxs-lookup"><span data-stu-id="e5dad-315">Specifies a file pattern that indicates which files to copy.</span></span> <span data-ttu-id="e5dad-316">/Pattern 參數的行為取決於來源資料的位置以及是否有遞迴模式選項。</span><span class="sxs-lookup"><span data-stu-id="e5dad-316">The behavior of the /Pattern parameter is determined by the location of the source data, and the presence of the recursive mode option.</span></span> <span data-ttu-id="e5dad-317">遞迴模式可透過選項 /S 來指定。</span><span class="sxs-lookup"><span data-stu-id="e5dad-317">Recursive mode is specified via option /S.</span></span>

<span data-ttu-id="e5dad-318">如果指定來源是檔案系統中的目錄，則標準萬用字元便會立即生效，且所提供的檔案模式會與目錄中的檔案做比對。</span><span class="sxs-lookup"><span data-stu-id="e5dad-318">If the specified source is a directory in the file system, then standard wildcards are in effect, and the file pattern provided is matched against files within the directory.</span></span> <span data-ttu-id="e5dad-319">如果已指定選項 /S，則 AzCopy 也會將指定模式與該目錄下任何子資料夾中的所有檔案做比對。</span><span class="sxs-lookup"><span data-stu-id="e5dad-319">If option /S is specified, then AzCopy also matches the specified pattern against all files in any subfolders beneath the directory.</span></span>

<span data-ttu-id="e5dad-320">如果指定來源是 Blob 容器或虛擬目錄，則萬用字元並不適用。</span><span class="sxs-lookup"><span data-stu-id="e5dad-320">If the specified source is a blob container or virtual directory, then wildcards are not applied.</span></span> <span data-ttu-id="e5dad-321">如果已指定選項 /S，則 AzCopy 會將指定的檔案模式解譯為 Blob 首碼。</span><span class="sxs-lookup"><span data-stu-id="e5dad-321">If option /S is specified, then AzCopy interprets the specified file pattern as a blob prefix.</span></span> <span data-ttu-id="e5dad-322">如果未指定選項 /S，則 AzCopy 會將檔案模型與確切 Blob 名稱做比對。</span><span class="sxs-lookup"><span data-stu-id="e5dad-322">If option /S is not specified, then AzCopy matches the file pattern against exact blob names.</span></span>

<span data-ttu-id="e5dad-323">如果指定來源是 Azure 檔案共用，則您必須指定確切檔案名稱 (例如 abc.txt) 以複製單一檔案，或指定選項 /S 以遞迴方式複製共用中的所有檔案。</span><span class="sxs-lookup"><span data-stu-id="e5dad-323">If the specified source is an Azure file share, then you must either specify the exact file name, (e.g. abc.txt) to copy a single file, or specify option /S to copy all files in the share recursively.</span></span> <span data-ttu-id="e5dad-324">嘗試同時指定檔案模式和選項 /S，將會造成錯誤。</span><span class="sxs-lookup"><span data-stu-id="e5dad-324">Attempting to specify both a file pattern and option /S together will result in an error.</span></span>

<span data-ttu-id="e5dad-325">當 /Source 是 Blob 容器或 Blob 的虛擬目錄時，AzCopy 會使用區分大小寫比對，並在所有其他情況下使用不區分大小寫比對。</span><span class="sxs-lookup"><span data-stu-id="e5dad-325">AzCopy uses case-sensitive matching when the /Source is a blob container or blob virtual directory, and uses case-insensitive matching in all the other cases.</span></span>

<span data-ttu-id="e5dad-326">未指定檔案模式時，使用的預設檔案模式如下：針對檔案系統位置，會使用 *。*</span><span class="sxs-lookup"><span data-stu-id="e5dad-326">The default file pattern used when no file pattern is specified is *.*</span></span> <span data-ttu-id="e5dad-327">，針對「Azure 儲存體」位置，則是使用空白首碼。</span><span class="sxs-lookup"><span data-stu-id="e5dad-327">for a file system location or an empty prefix for an Azure Storage location.</span></span> <span data-ttu-id="e5dad-328">不支援指定多個檔案模式。</span><span class="sxs-lookup"><span data-stu-id="e5dad-328">Specifying multiple file patterns is not supported.</span></span>

<span data-ttu-id="e5dad-329">**適用於：** Blob、檔案</span><span class="sxs-lookup"><span data-stu-id="e5dad-329">**Applicable to:** Blobs, Files</span></span>

### <a name="destkeystorage-key"></a><span data-ttu-id="e5dad-330">/DestKey:"storage-key"</span><span class="sxs-lookup"><span data-stu-id="e5dad-330">/DestKey:"storage-key"</span></span>
<span data-ttu-id="e5dad-331">指定目的地資源的儲存體帳戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="e5dad-331">Specifies the storage account key for the destination resource.</span></span>

<span data-ttu-id="e5dad-332">**適用於：** Blob、檔案、資料表</span><span class="sxs-lookup"><span data-stu-id="e5dad-332">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="destsassas-token"></a><span data-ttu-id="e5dad-333">/DestSAS:"sas-token"</span><span class="sxs-lookup"><span data-stu-id="e5dad-333">/DestSAS:"sas-token"</span></span>
<span data-ttu-id="e5dad-334">以讀取和寫入權限指定目的地的共用存取簽章 (SAS) (如果適用的話)。</span><span class="sxs-lookup"><span data-stu-id="e5dad-334">Specifies a Shared Access Signature (SAS) with READ and WRITE permissions for the destination (if applicable).</span></span> <span data-ttu-id="e5dad-335">為 SAS 加上雙引號，因為它可能包含特殊命令列字元。</span><span class="sxs-lookup"><span data-stu-id="e5dad-335">Surround the SAS with double quotes, as it may contains special command-line characters.</span></span>

<span data-ttu-id="e5dad-336">如果目的地資源是 Blob 容器、檔案共用或資料表，您可以指定此選項後面接著 SAS 權杖，或者您可以不使用此選項，直接將 SAS 指定為目的地 Blob 容器、檔案共用或資料表 URI 的一部分。</span><span class="sxs-lookup"><span data-stu-id="e5dad-336">If the destination resource is a blob container, file share or table, you can either specify this option followed by the SAS token, or you can specify the SAS as part of the destination blob container, file share or table's URI, without this option.</span></span>

<span data-ttu-id="e5dad-337">如果來源和目的地都是 Blob，則目的地 Blob 必須與來源 Blob 位於相同的儲存體帳戶中。</span><span class="sxs-lookup"><span data-stu-id="e5dad-337">If the source and destination are both blobs, then the destination blob must reside within the same storage account as the source blob.</span></span>

<span data-ttu-id="e5dad-338">**適用於：** Blob、檔案、資料表</span><span class="sxs-lookup"><span data-stu-id="e5dad-338">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="sourcekeystorage-key"></a><span data-ttu-id="e5dad-339">/SourceKey:"storage-key"</span><span class="sxs-lookup"><span data-stu-id="e5dad-339">/SourceKey:"storage-key"</span></span>
<span data-ttu-id="e5dad-340">指定來源資源的儲存體帳戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="e5dad-340">Specifies the storage account key for the source resource.</span></span>

<span data-ttu-id="e5dad-341">**適用於：** Blob、檔案、資料表</span><span class="sxs-lookup"><span data-stu-id="e5dad-341">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="sourcesassas-token"></a><span data-ttu-id="e5dad-342">/SourceSAS:"sas-token"</span><span class="sxs-lookup"><span data-stu-id="e5dad-342">/SourceSAS:"sas-token"</span></span>
<span data-ttu-id="e5dad-343">以讀取和清單權限指定來源的共用存取簽章 (如果適用的話)。</span><span class="sxs-lookup"><span data-stu-id="e5dad-343">Specifies a Shared Access Signature with READ and LIST permissions for the source (if applicable).</span></span> <span data-ttu-id="e5dad-344">為 SAS 加上雙引號，因為它可能包含特殊命令列字元。</span><span class="sxs-lookup"><span data-stu-id="e5dad-344">Surround the SAS with double quotes, as it may contains special command-line characters.</span></span>

<span data-ttu-id="e5dad-345">如果來源資源是 Blob 容器，且未提供金鑰及 SAS，則可透過匿名存取讀取該 Blob 容器。</span><span class="sxs-lookup"><span data-stu-id="e5dad-345">If the source resource is a blob container, and neither a key nor a SAS is provided, then the blob container will be read via anonymous access.</span></span>

<span data-ttu-id="e5dad-346">如果來源是檔案共用或資料表，則必須提供金鑰或 SAS。</span><span class="sxs-lookup"><span data-stu-id="e5dad-346">If the source is a file share or table, a key or a SAS must be provided.</span></span>

<span data-ttu-id="e5dad-347">**適用於：** Blob、檔案、資料表</span><span class="sxs-lookup"><span data-stu-id="e5dad-347">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="s"></a><span data-ttu-id="e5dad-348">/S</span><span class="sxs-lookup"><span data-stu-id="e5dad-348">/S</span></span>
<span data-ttu-id="e5dad-349">指定複製作業的遞迴模式。</span><span class="sxs-lookup"><span data-stu-id="e5dad-349">Specifies recursive mode for copy operations.</span></span> <span data-ttu-id="e5dad-350">在遞迴模式中，AzCopy 將複製所有符合指定檔案模式的 Blob 或檔案，包括子資料夾中的 Blob 或檔案。</span><span class="sxs-lookup"><span data-stu-id="e5dad-350">In recursive mode, AzCopy will copy all blobs or files that match the specified file pattern, including those in subfolders.</span></span>

<span data-ttu-id="e5dad-351">**適用於：** Blob、檔案</span><span class="sxs-lookup"><span data-stu-id="e5dad-351">**Applicable to:** Blobs, Files</span></span>

### <a name="blobtypeblock--page--append"></a><span data-ttu-id="e5dad-352">/BlobType:"block" | "page" | "append"</span><span class="sxs-lookup"><span data-stu-id="e5dad-352">/BlobType:"block" | "page" | "append"</span></span>
<span data-ttu-id="e5dad-353">指定目的地 Blob 是區塊 Blob、分頁 Blob 或附加 Blob。</span><span class="sxs-lookup"><span data-stu-id="e5dad-353">Specifies whether the destination blob is a block blob, a page blob, or an append blob.</span></span> <span data-ttu-id="e5dad-354">此選項僅在上傳 Blob 時才適用。</span><span class="sxs-lookup"><span data-stu-id="e5dad-354">This option is applicable only when you are uploading a blob.</span></span> <span data-ttu-id="e5dad-355">否則會產生錯誤。</span><span class="sxs-lookup"><span data-stu-id="e5dad-355">Otherwise, an error is generated.</span></span> <span data-ttu-id="e5dad-356">如果目的地是 Blob 且未指定此選項，則 AzCopy 預設會建立區塊 Blob。</span><span class="sxs-lookup"><span data-stu-id="e5dad-356">If the destination is a blob and this option is not specified, by default, AzCopy creates a block blob.</span></span>

<span data-ttu-id="e5dad-357">**適用於：** Blob</span><span class="sxs-lookup"><span data-stu-id="e5dad-357">**Applicable to:** Blobs</span></span>

### <a name="checkmd5"></a><span data-ttu-id="e5dad-358">/CheckMD5</span><span class="sxs-lookup"><span data-stu-id="e5dad-358">/CheckMD5</span></span>
<span data-ttu-id="e5dad-359">計算下載資料的 MD5 雜湊，並驗證 MD5 雜湊是否儲存在符合計算之雜湊的 Blob 或檔案的 Content-MD5 屬性中。</span><span class="sxs-lookup"><span data-stu-id="e5dad-359">Calculates an MD5 hash for downloaded data and verifies that the MD5 hash stored in the blob or file's Content-MD5 property matches the calculated hash.</span></span> <span data-ttu-id="e5dad-360">MD5 檢查依預設為關閉，因此您必須指定此選項，才能在下載資料時執行 MD5 檢查。</span><span class="sxs-lookup"><span data-stu-id="e5dad-360">The MD5 check is turned off by default, so you must specify this option to perform the MD5 check when downloading data.</span></span>

<span data-ttu-id="e5dad-361">請注意，Azure 儲存體並不保證儲存供 Blob 或檔案使用的 MD5 雜湊是最新的版本。</span><span class="sxs-lookup"><span data-stu-id="e5dad-361">Note that Azure Storage doesn't guarantee that the MD5 hash stored for the blob or file is up-to-date.</span></span> <span data-ttu-id="e5dad-362">每次修改 Blob 或檔案時將 MD5 更新是用戶端的責任。</span><span class="sxs-lookup"><span data-stu-id="e5dad-362">It is client's responsibility to update the MD5 whenever the blob or file is modified.</span></span>

<span data-ttu-id="e5dad-363">在上傳至服務之後，AzCopy 一定會為 Azure Blob 或檔案設定 Content-MD5 屬性。</span><span class="sxs-lookup"><span data-stu-id="e5dad-363">AzCopy always sets the Content-MD5 property for an Azure blob or file after uploading it to the service.</span></span>  

<span data-ttu-id="e5dad-364">**適用於：** Blob、檔案</span><span class="sxs-lookup"><span data-stu-id="e5dad-364">**Applicable to:** Blobs, Files</span></span>

### <a name="snapshot"></a><span data-ttu-id="e5dad-365">/Snapshot</span><span class="sxs-lookup"><span data-stu-id="e5dad-365">/Snapshot</span></span>
<span data-ttu-id="e5dad-366">指出是否傳輸快照。</span><span class="sxs-lookup"><span data-stu-id="e5dad-366">Indicates whether to transfer snapshots.</span></span> <span data-ttu-id="e5dad-367">此選項僅在來源是 Blob 才有效。</span><span class="sxs-lookup"><span data-stu-id="e5dad-367">This option is only valid when the source is a blob.</span></span>

<span data-ttu-id="e5dad-368">傳輸的 Blob 快照集會以下列格式重新命名：blob-name (snapshot-time).extension</span><span class="sxs-lookup"><span data-stu-id="e5dad-368">The transferred blob snapshots are renamed in this format: blob-name (snapshot-time).extension</span></span>

<span data-ttu-id="e5dad-369">依預設，不會複製快照。</span><span class="sxs-lookup"><span data-stu-id="e5dad-369">By default, snapshots are not copied.</span></span>

<span data-ttu-id="e5dad-370">**適用於：** Blob</span><span class="sxs-lookup"><span data-stu-id="e5dad-370">**Applicable to:** Blobs</span></span>

### <a name="vverbose-log-file"></a><span data-ttu-id="e5dad-371">/V:[verbose-log-file]</span><span class="sxs-lookup"><span data-stu-id="e5dad-371">/V:[verbose-log-file]</span></span>
<span data-ttu-id="e5dad-372">將詳細資訊狀態訊息輸出至記錄檔。</span><span class="sxs-lookup"><span data-stu-id="e5dad-372">Outputs verbose status messages into a log file.</span></span>

<span data-ttu-id="e5dad-373">根據預設，在 `%LocalAppData%\Microsoft\Azure\AzCopy`中詳細資訊記錄檔會被命名為 AzCopyVerbose.log。</span><span class="sxs-lookup"><span data-stu-id="e5dad-373">By default, the verbose log file is named AzCopyVerbose.log in `%LocalAppData%\Microsoft\Azure\AzCopy`.</span></span> <span data-ttu-id="e5dad-374">如果您在此選項中指定現有檔案位置，則詳細資訊記錄將會被附加到該檔案。</span><span class="sxs-lookup"><span data-stu-id="e5dad-374">If you specify an existing file location for this option, the verbose log will be appended to that file.</span></span>  

<span data-ttu-id="e5dad-375">**適用於：** Blob、檔案、資料表</span><span class="sxs-lookup"><span data-stu-id="e5dad-375">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="zjournal-file-folder"></a><span data-ttu-id="e5dad-376">/Z:[journal-file-folder]</span><span class="sxs-lookup"><span data-stu-id="e5dad-376">/Z:[journal-file-folder]</span></span>
<span data-ttu-id="e5dad-377">指定用於繼續作業的日誌檔案資料夾。</span><span class="sxs-lookup"><span data-stu-id="e5dad-377">Specifies a journal file folder for resuming an operation.</span></span>

<span data-ttu-id="e5dad-378">如果作業遭到中斷，AzCopy 絕對支援繼續作業。</span><span class="sxs-lookup"><span data-stu-id="e5dad-378">AzCopy always supports resuming if an operation has been interrupted.</span></span>

<span data-ttu-id="e5dad-379">如果未指定此選項，或指定此選項但沒有指定資料夾路徑，則 AzCopy 將在預設位置上建立日誌檔案，預設位置是 %LocalAppData%\Microsoft\Azure\AzCopy。</span><span class="sxs-lookup"><span data-stu-id="e5dad-379">If this option is not specified, or it is specified without a folder path, then AzCopy will create the journal file in the default location, which is %LocalAppData%\Microsoft\Azure\AzCopy.</span></span>

<span data-ttu-id="e5dad-380">每次發佈命令至 AzCopy 時，它會檢查預設資料夾或透過此選項指定的資料夾中是否有日誌檔案存在。</span><span class="sxs-lookup"><span data-stu-id="e5dad-380">Each time you issue a command to AzCopy, it checks whether a journal file exists in the default folder, or whether it exists in a folder that you specified via this option.</span></span> <span data-ttu-id="e5dad-381">如果在這兩個地方都找不到日誌檔案，AzCopy 會將此作業視為新的作業，並產生新的日誌檔案。</span><span class="sxs-lookup"><span data-stu-id="e5dad-381">If the journal file does not exist in either place, AzCopy treats the operation as new and generates a new journal file.</span></span>

<span data-ttu-id="e5dad-382">如果找到日誌檔案，則 AzCopy 將檢查所輸入的命令列是否符合日誌檔案中的命令列。</span><span class="sxs-lookup"><span data-stu-id="e5dad-382">If the journal file does exist, AzCopy will check whether the command line that you input matches the command line in the journal file.</span></span> <span data-ttu-id="e5dad-383">如果這兩個命令列相符，AzCopy 便會繼續未完成的作業。</span><span class="sxs-lookup"><span data-stu-id="e5dad-383">If the two command lines match, AzCopy resumes the incomplete operation.</span></span> <span data-ttu-id="e5dad-384">如果這兩個命令列不符，系統將提示您覆寫日誌檔案並開始新的作業，或取消目前作業。</span><span class="sxs-lookup"><span data-stu-id="e5dad-384">If they do not match, you will be prompted to either overwrite the journal file to start a new operation, or to cancel the current operation.</span></span>

<span data-ttu-id="e5dad-385">成功完成作業時，系統便會將日誌檔案刪除。</span><span class="sxs-lookup"><span data-stu-id="e5dad-385">The journal file is deleted upon successful completion of the operation.</span></span>

<span data-ttu-id="e5dad-386">請注意，不支援根據舊版的 AzCopy 所建立的日誌檔案繼續作業。</span><span class="sxs-lookup"><span data-stu-id="e5dad-386">Note that resuming an operation from a journal file created by a previous version of AzCopy is not supported.</span></span>

<span data-ttu-id="e5dad-387">**適用於：** Blob、檔案、資料表</span><span class="sxs-lookup"><span data-stu-id="e5dad-387">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="parameter-file"></a><span data-ttu-id="e5dad-388">/@:"parameter-file"</span><span class="sxs-lookup"><span data-stu-id="e5dad-388">/@:"parameter-file"</span></span>
<span data-ttu-id="e5dad-389">指定包含參數的檔案。</span><span class="sxs-lookup"><span data-stu-id="e5dad-389">Specifies a file that contains parameters.</span></span> <span data-ttu-id="e5dad-390">AzCopy 處理檔案中的參數，就好像在命令列上指定這些參數一様。</span><span class="sxs-lookup"><span data-stu-id="e5dad-390">AzCopy processes the parameters in the file just as if they had been specified on the command line.</span></span>

<span data-ttu-id="e5dad-391">在回應檔案中，您可以在單行中指定多個參數，或每一行各自指定一個參數。</span><span class="sxs-lookup"><span data-stu-id="e5dad-391">In a response file, you can either specify multiple parameters on a single line, or specify each parameter on its own line.</span></span> <span data-ttu-id="e5dad-392">請注意，各個參數無法橫跨多行。</span><span class="sxs-lookup"><span data-stu-id="e5dad-392">Note that an individual parameter cannot span multiple lines.</span></span>

<span data-ttu-id="e5dad-393">回應檔案可包含開頭為 # 符號的命令列。</span><span class="sxs-lookup"><span data-stu-id="e5dad-393">Response files can include comments lines that begin with the # symbol.</span></span>

<span data-ttu-id="e5dad-394">您可以指定多個回應檔案。</span><span class="sxs-lookup"><span data-stu-id="e5dad-394">You can specify multiple response files.</span></span> <span data-ttu-id="e5dad-395">不過，請記住 AzCopy 不支援巢狀回應檔案。</span><span class="sxs-lookup"><span data-stu-id="e5dad-395">However, note that AzCopy does not support nested response files.</span></span>

<span data-ttu-id="e5dad-396">**適用於：** Blob、檔案、資料表</span><span class="sxs-lookup"><span data-stu-id="e5dad-396">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="y"></a><span data-ttu-id="e5dad-397">/Y</span><span class="sxs-lookup"><span data-stu-id="e5dad-397">/Y</span></span>
<span data-ttu-id="e5dad-398">隱藏所有 AzCopy 確認提示。</span><span class="sxs-lookup"><span data-stu-id="e5dad-398">Suppresses all AzCopy confirmation prompts.</span></span>

<span data-ttu-id="e5dad-399">**適用於：** Blob、檔案、資料表</span><span class="sxs-lookup"><span data-stu-id="e5dad-399">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="l"></a><span data-ttu-id="e5dad-400">/L</span><span class="sxs-lookup"><span data-stu-id="e5dad-400">/L</span></span>
<span data-ttu-id="e5dad-401">僅指定清單作業，不會複製資料。</span><span class="sxs-lookup"><span data-stu-id="e5dad-401">Specifies a listing operation only; no data is copied.</span></span>

<span data-ttu-id="e5dad-402">AzCopy 會解譯使用這個選項為模擬不使用 /L 選項來執行此命令列，而且會計算有多少物件會被複製，您可以同時指定 /V 選項，檢查要複製哪些物件到詳細記錄檔中。</span><span class="sxs-lookup"><span data-stu-id="e5dad-402">AzCopy will interpret the using of this option as a simulation for running the command line without this option /L and count how many objects will be copied, you can specify option /V at the same time to check which objects will be copied in the verbose log.</span></span>

<span data-ttu-id="e5dad-403">這個選項的行為還取決於來源資料的位置，以及是否有遞迴模式選項 /S 和檔案模式選項 /Pattern。</span><span class="sxs-lookup"><span data-stu-id="e5dad-403">The behavior of this option is also determined by the location of the source data and the presence of the recursive mode option /S and file pattern option /Pattern.</span></span>

<span data-ttu-id="e5dad-404">使用此選項時，AzCopy 會需要此來源位置的清單和讀取權限。</span><span class="sxs-lookup"><span data-stu-id="e5dad-404">AzCopy requires LIST and READ permission of this source location when using this option.</span></span>

<span data-ttu-id="e5dad-405">**適用於：** Blob、檔案</span><span class="sxs-lookup"><span data-stu-id="e5dad-405">**Applicable to:** Blobs, Files</span></span>

### <a name="mt"></a><span data-ttu-id="e5dad-406">/MT</span><span class="sxs-lookup"><span data-stu-id="e5dad-406">/MT</span></span>
<span data-ttu-id="e5dad-407">將下載檔案的最後修改時間設定為與來源 Blob 或檔案相同的最後修改時間。</span><span class="sxs-lookup"><span data-stu-id="e5dad-407">Sets the downloaded file's last-modified time to be the same as the source blob or file's.</span></span>

<span data-ttu-id="e5dad-408">**適用於：** Blob、檔案</span><span class="sxs-lookup"><span data-stu-id="e5dad-408">**Applicable to:** Blobs, Files</span></span>

### <a name="xn"></a><span data-ttu-id="e5dad-409">/XN</span><span class="sxs-lookup"><span data-stu-id="e5dad-409">/XN</span></span>
<span data-ttu-id="e5dad-410">排除較新的來源資源。</span><span class="sxs-lookup"><span data-stu-id="e5dad-410">Excludes a newer source resource.</span></span> <span data-ttu-id="e5dad-411">如果最後修改時間比目的地還要新或同時間，則不會複製資源。</span><span class="sxs-lookup"><span data-stu-id="e5dad-411">The resource will not be copied if the last modified time of the source is the same or newer than destination.</span></span>

<span data-ttu-id="e5dad-412">**適用於：** Blob、檔案</span><span class="sxs-lookup"><span data-stu-id="e5dad-412">**Applicable to:** Blobs, Files</span></span>

### <a name="xo"></a><span data-ttu-id="e5dad-413">/XO</span><span class="sxs-lookup"><span data-stu-id="e5dad-413">/XO</span></span>
<span data-ttu-id="e5dad-414">排除較舊的來源資源。</span><span class="sxs-lookup"><span data-stu-id="e5dad-414">Excludes an older source resource.</span></span> <span data-ttu-id="e5dad-415">如果最後修改時間比目的地還要舊或同時間，則不會複製資源。</span><span class="sxs-lookup"><span data-stu-id="e5dad-415">The resource will not be copied if the last modified time of the source is the same or older than destination.</span></span>

<span data-ttu-id="e5dad-416">**適用於：** Blob、檔案</span><span class="sxs-lookup"><span data-stu-id="e5dad-416">**Applicable to:** Blobs, Files</span></span>

### <a name="a"></a><span data-ttu-id="e5dad-417">/A</span><span class="sxs-lookup"><span data-stu-id="e5dad-417">/A</span></span>
<span data-ttu-id="e5dad-418">僅上傳已設定 [封存] 屬性的檔案。</span><span class="sxs-lookup"><span data-stu-id="e5dad-418">Uploads only files that have the Archive attribute set.</span></span>

<span data-ttu-id="e5dad-419">**適用於：** Blob、檔案</span><span class="sxs-lookup"><span data-stu-id="e5dad-419">**Applicable to:** Blobs, Files</span></span>

### <a name="iarashcnetoi"></a><span data-ttu-id="e5dad-420">/IA:[RASHCNETOI]</span><span class="sxs-lookup"><span data-stu-id="e5dad-420">/IA:[RASHCNETOI]</span></span>
<span data-ttu-id="e5dad-421">僅上傳已設定任何指定屬性的檔案。</span><span class="sxs-lookup"><span data-stu-id="e5dad-421">Uploads only files that have any of the specified attributes set.</span></span>

<span data-ttu-id="e5dad-422">可用屬性包括：</span><span class="sxs-lookup"><span data-stu-id="e5dad-422">Available attributes include:</span></span>

* <span data-ttu-id="e5dad-423">R = 唯讀檔案</span><span class="sxs-lookup"><span data-stu-id="e5dad-423">R = Read-only files</span></span>
* <span data-ttu-id="e5dad-424">A = 準備封存的檔案</span><span class="sxs-lookup"><span data-stu-id="e5dad-424">A = Files ready for archiving</span></span>
* <span data-ttu-id="e5dad-425">S = 系統檔案</span><span class="sxs-lookup"><span data-stu-id="e5dad-425">S = System files</span></span>
* <span data-ttu-id="e5dad-426">H = 隱藏檔案</span><span class="sxs-lookup"><span data-stu-id="e5dad-426">H = Hidden files</span></span>
* <span data-ttu-id="e5dad-427">C = 壓縮檔案</span><span class="sxs-lookup"><span data-stu-id="e5dad-427">C = Compressed files</span></span>
* <span data-ttu-id="e5dad-428">N = 正常檔案</span><span class="sxs-lookup"><span data-stu-id="e5dad-428">N = Normal files</span></span>
* <span data-ttu-id="e5dad-429">E = 加密檔案</span><span class="sxs-lookup"><span data-stu-id="e5dad-429">E = Encrypted files</span></span>
* <span data-ttu-id="e5dad-430">T = 暫存檔案</span><span class="sxs-lookup"><span data-stu-id="e5dad-430">T = Temporary files</span></span>
* <span data-ttu-id="e5dad-431">O = 離線檔案</span><span class="sxs-lookup"><span data-stu-id="e5dad-431">O = Offline files</span></span>
* <span data-ttu-id="e5dad-432">I = 未編製索引的檔案</span><span class="sxs-lookup"><span data-stu-id="e5dad-432">I = Non-indexed files</span></span>

<span data-ttu-id="e5dad-433">**適用於：** Blob、檔案</span><span class="sxs-lookup"><span data-stu-id="e5dad-433">**Applicable to:** Blobs, Files</span></span>

### <a name="xarashcnetoi"></a><span data-ttu-id="e5dad-434">/XA:[RASHCNETOI]</span><span class="sxs-lookup"><span data-stu-id="e5dad-434">/XA:[RASHCNETOI]</span></span>
<span data-ttu-id="e5dad-435">排除已設定任何指定屬性的檔案。</span><span class="sxs-lookup"><span data-stu-id="e5dad-435">Excludes files that have any of the specified attributes set.</span></span>

<span data-ttu-id="e5dad-436">可用屬性包括：</span><span class="sxs-lookup"><span data-stu-id="e5dad-436">Available attributes include:</span></span>

* <span data-ttu-id="e5dad-437">R = 唯讀檔案</span><span class="sxs-lookup"><span data-stu-id="e5dad-437">R = Read-only files</span></span>
* <span data-ttu-id="e5dad-438">A = 準備封存的檔案</span><span class="sxs-lookup"><span data-stu-id="e5dad-438">A = Files ready for archiving</span></span>
* <span data-ttu-id="e5dad-439">S = 系統檔案</span><span class="sxs-lookup"><span data-stu-id="e5dad-439">S = System files</span></span>
* <span data-ttu-id="e5dad-440">H = 隱藏檔案</span><span class="sxs-lookup"><span data-stu-id="e5dad-440">H = Hidden files</span></span>
* <span data-ttu-id="e5dad-441">C = 壓縮檔案</span><span class="sxs-lookup"><span data-stu-id="e5dad-441">C = Compressed files</span></span>
* <span data-ttu-id="e5dad-442">N = 正常檔案</span><span class="sxs-lookup"><span data-stu-id="e5dad-442">N = Normal files</span></span>
* <span data-ttu-id="e5dad-443">E = 加密檔案</span><span class="sxs-lookup"><span data-stu-id="e5dad-443">E = Encrypted files</span></span>
* <span data-ttu-id="e5dad-444">T = 暫存檔案</span><span class="sxs-lookup"><span data-stu-id="e5dad-444">T = Temporary files</span></span>
* <span data-ttu-id="e5dad-445">O = 離線檔案</span><span class="sxs-lookup"><span data-stu-id="e5dad-445">O = Offline files</span></span>
* <span data-ttu-id="e5dad-446">I = 未編製索引的檔案</span><span class="sxs-lookup"><span data-stu-id="e5dad-446">I = Non-indexed files</span></span>

<span data-ttu-id="e5dad-447">**適用於：** Blob、檔案</span><span class="sxs-lookup"><span data-stu-id="e5dad-447">**Applicable to:** Blobs, Files</span></span>

### <a name="delimiterdelimiter"></a><span data-ttu-id="e5dad-448">/Delimiter:"delimiter"</span><span class="sxs-lookup"><span data-stu-id="e5dad-448">/Delimiter:"delimiter"</span></span>
<span data-ttu-id="e5dad-449">指出在 Blob 名稱中，用來分隔虛擬目錄的分隔符號字元。</span><span class="sxs-lookup"><span data-stu-id="e5dad-449">Indicates the delimiter character used to delimit virtual directories in a blob name.</span></span>

<span data-ttu-id="e5dad-450">依預設，AzCopy 會使用 / 作為分隔符號字元。</span><span class="sxs-lookup"><span data-stu-id="e5dad-450">By default, AzCopy uses / as the delimiter character.</span></span> <span data-ttu-id="e5dad-451">不過，AzCopy 支援使用任何常見字元 (例如 @、# 或 %) 作為分隔符號。</span><span class="sxs-lookup"><span data-stu-id="e5dad-451">However, AzCopy supports using any common character (such as @, #, or %) as a delimiter.</span></span> <span data-ttu-id="e5dad-452">如果您必須在命令列中包含其中一個特殊字元，請為檔案名稱加上雙引號。</span><span class="sxs-lookup"><span data-stu-id="e5dad-452">If you need to include one of these special characters on the command line, enclose the file name with double quotes.</span></span>

<span data-ttu-id="e5dad-453">此選項僅適用於下載 Blob。</span><span class="sxs-lookup"><span data-stu-id="e5dad-453">This option is only applicable for downloading blobs.</span></span>

<span data-ttu-id="e5dad-454">**適用於：** Blob</span><span class="sxs-lookup"><span data-stu-id="e5dad-454">**Applicable to:** Blobs</span></span>

### <a name="ncnumber-of-concurrent-operations"></a><span data-ttu-id="e5dad-455">/NC:"number-of-concurrent-operations"</span><span class="sxs-lookup"><span data-stu-id="e5dad-455">/NC:"number-of-concurrent-operations"</span></span>
<span data-ttu-id="e5dad-456">指定並行作業的數目。</span><span class="sxs-lookup"><span data-stu-id="e5dad-456">Specifies the number of concurrent operations.</span></span>

<span data-ttu-id="e5dad-457">AzCopy 依預設會啟動特定數量的並行作業，以提高資料傳輸的輸送量。</span><span class="sxs-lookup"><span data-stu-id="e5dad-457">AzCopy by default starts a certain number of concurrent operations to increase the data transfer throughput.</span></span> <span data-ttu-id="e5dad-458">請注意，在低頻寬環境中的大量並行作業有可能會拖垮網路連線，並使作業無法完成。</span><span class="sxs-lookup"><span data-stu-id="e5dad-458">Note that large number of concurrent operations in a low-bandwidth environment may overwhelm the network connection and prevent the operations from fully completing.</span></span> <span data-ttu-id="e5dad-459">根據實際可用網路頻寬來節流處理並行作業。</span><span class="sxs-lookup"><span data-stu-id="e5dad-459">Throttle concurrent operations based on actual available network bandwidth.</span></span>

<span data-ttu-id="e5dad-460">並行作業數的上限為 512。</span><span class="sxs-lookup"><span data-stu-id="e5dad-460">The upper limit for concurrent operations is 512.</span></span>

<span data-ttu-id="e5dad-461">**適用於：** Blob、檔案、資料表</span><span class="sxs-lookup"><span data-stu-id="e5dad-461">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="sourcetypeblob--table"></a><span data-ttu-id="e5dad-462">/SourceType:"Blob" | "Table"</span><span class="sxs-lookup"><span data-stu-id="e5dad-462">/SourceType:"Blob" | "Table"</span></span>
<span data-ttu-id="e5dad-463">指定 `source` 資源是本機開發環境中可用、於儲存體模擬器中執行的 Blob。</span><span class="sxs-lookup"><span data-stu-id="e5dad-463">Specifies that the `source` resource is a blob available in the local development environment, running in the storage emulator.</span></span>

<span data-ttu-id="e5dad-464">**適用於：** Blob、資料表</span><span class="sxs-lookup"><span data-stu-id="e5dad-464">**Applicable to:** Blobs, Tables</span></span>

### <a name="desttypeblob--table"></a><span data-ttu-id="e5dad-465">/DestType:"Blob" | "Table"</span><span class="sxs-lookup"><span data-stu-id="e5dad-465">/DestType:"Blob" | "Table"</span></span>
<span data-ttu-id="e5dad-466">指定 `destination` 資源是本機開發環境中可用、於儲存體模擬器中執行的 Blob。</span><span class="sxs-lookup"><span data-stu-id="e5dad-466">Specifies that the `destination` resource is a blob available in the local development environment, running in the storage emulator.</span></span>

<span data-ttu-id="e5dad-467">**適用於：** Blob、資料表</span><span class="sxs-lookup"><span data-stu-id="e5dad-467">**Applicable to:** Blobs, Tables</span></span>

### <a name="pkrskey1key2key3"></a><span data-ttu-id="e5dad-468">/PKRS:"key1#key2#key3#..."</span><span class="sxs-lookup"><span data-stu-id="e5dad-468">/PKRS:"key1#key2#key3#..."</span></span>
<span data-ttu-id="e5dad-469">分割資料分割索引鍵範圍以支援平行匯出資料表資料的作業，這樣可以加快匯出作業的速度。</span><span class="sxs-lookup"><span data-stu-id="e5dad-469">Splits the partition key range to enable exporting table data in parallel, which increases the speed of the export operation.</span></span>

<span data-ttu-id="e5dad-470">若未指定此選項，AzCopy 會使用單一執行緒來匯出資料表實體。</span><span class="sxs-lookup"><span data-stu-id="e5dad-470">If this option is not specified, then AzCopy uses a single thread to export table entities.</span></span> <span data-ttu-id="e5dad-471">例如，如果使用者指定 /PKRS:"aa#bb"，則 AzCopy 會啟動三個並行作業。</span><span class="sxs-lookup"><span data-stu-id="e5dad-471">For example, if the user specifies /PKRS:"aa#bb", then AzCopy starts three concurrent operations.</span></span>

<span data-ttu-id="e5dad-472">每個作業分別會匯出三個資料分割索引鍵範圍的其中一個，如下所示：</span><span class="sxs-lookup"><span data-stu-id="e5dad-472">Each operation exports one of three partition key ranges, as shown below:</span></span>

  <span data-ttu-id="e5dad-473">[first-partition-key, aa)</span><span class="sxs-lookup"><span data-stu-id="e5dad-473">[first-partition-key, aa)</span></span>

  <span data-ttu-id="e5dad-474">[aa, bb)</span><span class="sxs-lookup"><span data-stu-id="e5dad-474">[aa, bb)</span></span>

  <span data-ttu-id="e5dad-475">[bb, last-partition-key]</span><span class="sxs-lookup"><span data-stu-id="e5dad-475">[bb, last-partition-key]</span></span>

<span data-ttu-id="e5dad-476">**適用於：** 資料表</span><span class="sxs-lookup"><span data-stu-id="e5dad-476">**Applicable to:** Tables</span></span>

### <a name="splitsizefile-size"></a><span data-ttu-id="e5dad-477">/SplitSize:"file-size"</span><span class="sxs-lookup"><span data-stu-id="e5dad-477">/SplitSize:"file-size"</span></span>
<span data-ttu-id="e5dad-478">指定匯出的檔案分割大小 (以 MB 為單位)，允許的最小值為 32。</span><span class="sxs-lookup"><span data-stu-id="e5dad-478">Specifies the exported file split size in MB, the minimal value allowed is 32.</span></span>

<span data-ttu-id="e5dad-479">若未指定此選項，則 AzCopy 會將資料表資料匯出至單一檔案。</span><span class="sxs-lookup"><span data-stu-id="e5dad-479">If this option is not specified, AzCopy will export table data to single file.</span></span>

<span data-ttu-id="e5dad-480">如果資料表資料匯出至 Blob，且匯出的檔案大小達到 Blob 的大小限制 200 GB，則 AzCopy 會分割匯出的檔案，即使未指定此選項亦然。</span><span class="sxs-lookup"><span data-stu-id="e5dad-480">If the table data is exported to a blob, and the exported file size reaches the 200 GB limit for blob size, then AzCopy will split the exported file, even if this option is not specified.</span></span>

<span data-ttu-id="e5dad-481">**適用於：** 資料表</span><span class="sxs-lookup"><span data-stu-id="e5dad-481">**Applicable to:** Tables</span></span>

### <a name="entityoperationinsertorskip--insertormerge--insertorreplace"></a><span data-ttu-id="e5dad-482">/EntityOperation:"InsertOrSkip" | "InsertOrMerge" | "InsertOrReplace"</span><span class="sxs-lookup"><span data-stu-id="e5dad-482">/EntityOperation:"InsertOrSkip" | "InsertOrMerge" | "InsertOrReplace"</span></span>
<span data-ttu-id="e5dad-483">指定資料表資料匯入行為。</span><span class="sxs-lookup"><span data-stu-id="e5dad-483">Specifies the table data import behavior.</span></span>

* <span data-ttu-id="e5dad-484">InsertOrSkip - 略過現有實體，或插入新實體 (若不存在於資料表中)。</span><span class="sxs-lookup"><span data-stu-id="e5dad-484">InsertOrSkip - Skips an existing entity or inserts a new entity if it does not exist in the table.</span></span>
* <span data-ttu-id="e5dad-485">InsertOrMerge - 合併現有實體，或插入新實體 (若不存在於資料表中)。</span><span class="sxs-lookup"><span data-stu-id="e5dad-485">InsertOrMerge - Merges an existing entity or inserts a new entity if it does not exist in the table.</span></span>
* <span data-ttu-id="e5dad-486">InsertOrReplace - 取代現有實體，或插入新實體 (若不存在於資料表中)。</span><span class="sxs-lookup"><span data-stu-id="e5dad-486">InsertOrReplace - Replaces an existing entity or inserts a new entity if it does not exist in the table.</span></span>

<span data-ttu-id="e5dad-487">**適用於：** 資料表</span><span class="sxs-lookup"><span data-stu-id="e5dad-487">**Applicable to:** Tables</span></span>

### <a name="manifestmanifest-file"></a><span data-ttu-id="e5dad-488">/Manifest:"manifest-file"</span><span class="sxs-lookup"><span data-stu-id="e5dad-488">/Manifest:"manifest-file"</span></span>
<span data-ttu-id="e5dad-489">指定資料表匯出和匯入作業的資訊清單檔。</span><span class="sxs-lookup"><span data-stu-id="e5dad-489">Specifies the manifest file for the table export and import operation.</span></span>

<span data-ttu-id="e5dad-490">在匯出作業期間，此選項是選擇性的，如果沒有指定這個選項，AzCopy 便會產生具有預先定義名稱的資訊清單檔案。</span><span class="sxs-lookup"><span data-stu-id="e5dad-490">This option is optional during the export operation, AzCopy will generate a manifest file with predefined name if this option is not specified.</span></span>

<span data-ttu-id="e5dad-491">在匯入作業期間，為了尋找資料檔案，這是必要選項。</span><span class="sxs-lookup"><span data-stu-id="e5dad-491">This option is required during the import operation for locating the data files.</span></span>

<span data-ttu-id="e5dad-492">**適用於：** 資料表</span><span class="sxs-lookup"><span data-stu-id="e5dad-492">**Applicable to:** Tables</span></span>

### <a name="synccopy"></a><span data-ttu-id="e5dad-493">/SyncCopy</span><span class="sxs-lookup"><span data-stu-id="e5dad-493">/SyncCopy</span></span>
<span data-ttu-id="e5dad-494">指出在兩個 Azure 儲存體端點之間是否以同步方式複製 blob 或檔案。</span><span class="sxs-lookup"><span data-stu-id="e5dad-494">Indicates whether to synchronously copy blobs or files between two Azure Storage endpoints.</span></span>

<span data-ttu-id="e5dad-495">AzCopy 依預設會使用伺服器端的非同步複本。</span><span class="sxs-lookup"><span data-stu-id="e5dad-495">AzCopy by default uses server-side asynchronous copy.</span></span> <span data-ttu-id="e5dad-496">指定此選項可執行同步複製，也就是將 blog 或檔案下載至本機記憶體，再上傳至 Azure 儲存體。</span><span class="sxs-lookup"><span data-stu-id="e5dad-496">Specify this option to perform a synchronous copy, which downloads blobs or files to local memory and then uploads them to Azure Storage.</span></span>

<span data-ttu-id="e5dad-497">當您複製檔案是在 Blob 儲存體內、在檔案儲存體內，或從 Blob 儲存體到檔案儲存體 (或反過來) 時，您可以使用此選項。</span><span class="sxs-lookup"><span data-stu-id="e5dad-497">You can use this option when copying files within Blob storage, within File storage, or from Blob storage to File storage or vice versa.</span></span>

<span data-ttu-id="e5dad-498">**適用於：** Blob、檔案</span><span class="sxs-lookup"><span data-stu-id="e5dad-498">**Applicable to:** Blobs, Files</span></span>

### <a name="setcontenttypecontent-type"></a><span data-ttu-id="e5dad-499">/SetContentType:"content-type"</span><span class="sxs-lookup"><span data-stu-id="e5dad-499">/SetContentType:"content-type"</span></span>
<span data-ttu-id="e5dad-500">指定目的地 blob 或檔案的 MIME 內容類型。</span><span class="sxs-lookup"><span data-stu-id="e5dad-500">Specifies the MIME content type for destination blobs or files.</span></span>

<span data-ttu-id="e5dad-501">AzCopy 預設會將 blob 或檔案的內容類型設定為 application/octet-stream。</span><span class="sxs-lookup"><span data-stu-id="e5dad-501">AzCopy sets the content type for a blob or file to application/octet-stream by default.</span></span> <span data-ttu-id="e5dad-502">您可以明確指定這個選項的值來設定所有 blob 或檔案的內容類型。</span><span class="sxs-lookup"><span data-stu-id="e5dad-502">You can set the content type for all blobs or files by explicitly specifying a value for this option.</span></span>

<span data-ttu-id="e5dad-503">如果您指定這個選項但未指定任何值，則 AzCopy 會根據副檔名來設定每個 blob 或檔案的內容類型。</span><span class="sxs-lookup"><span data-stu-id="e5dad-503">If you specify this option without a value, then AzCopy will set each blob or file's content type according to its file extension.</span></span>

<span data-ttu-id="e5dad-504">**適用於：** Blob、檔案</span><span class="sxs-lookup"><span data-stu-id="e5dad-504">**Applicable to:** Blobs, Files</span></span>

### <a name="payloadformatjson--csv"></a><span data-ttu-id="e5dad-505">/PayloadFormat:"JSON" | "CSV"</span><span class="sxs-lookup"><span data-stu-id="e5dad-505">/PayloadFormat:"JSON" | "CSV"</span></span>
<span data-ttu-id="e5dad-506">指定資料表匯出的資料檔格式。</span><span class="sxs-lookup"><span data-stu-id="e5dad-506">Specifies the format of the table exported data file.</span></span>

<span data-ttu-id="e5dad-507">如果未指定此選項，根據預設，AzCopy 會匯出 JSON 格式的資料表資料檔案。</span><span class="sxs-lookup"><span data-stu-id="e5dad-507">If this option is not specified, by default AzCopy exports table data file in JSON format.</span></span>

<span data-ttu-id="e5dad-508">**適用於：** 資料表</span><span class="sxs-lookup"><span data-stu-id="e5dad-508">**Applicable to:** Tables</span></span>

## <a name="known-issues-and-best-practices"></a><span data-ttu-id="e5dad-509">已知問題和最佳作法</span><span class="sxs-lookup"><span data-stu-id="e5dad-509">Known Issues and Best Practices</span></span>
### <a name="limit-concurrent-writes-while-copying-data"></a><span data-ttu-id="e5dad-510">限制複製資料時的並行寫入</span><span class="sxs-lookup"><span data-stu-id="e5dad-510">Limit concurrent writes while copying data</span></span>
<span data-ttu-id="e5dad-511">使用 AzCopy 複製 Blob 或檔案時，請留意當您在複製資料時，另一個應用程式可能正在修改該資料。</span><span class="sxs-lookup"><span data-stu-id="e5dad-511">When you copy blobs or files with AzCopy, keep in mind that another application may be modifying the data while you are copying it.</span></span> <span data-ttu-id="e5dad-512">請儘可能地確定在複製作業過程中，您正要複製的資料並不在修改中。</span><span class="sxs-lookup"><span data-stu-id="e5dad-512">If possible, ensure that the data you are copying is not being modified during the copy operation.</span></span> <span data-ttu-id="e5dad-513">例如，當複製與 Azure 虛擬機器相關聯的 VHD 時，請確定目前沒有其他應用程式正在寫入此 VHD。</span><span class="sxs-lookup"><span data-stu-id="e5dad-513">For example, when copying a VHD associated with an Azure virtual machine, make sure that no other applications are currently writing to the VHD.</span></span> <span data-ttu-id="e5dad-514">要這樣做的一個好方法是租用要複製的資源。</span><span class="sxs-lookup"><span data-stu-id="e5dad-514">A good way to do this is by leasing the resource to be copied.</span></span> <span data-ttu-id="e5dad-515">此外，您可以首先建立 VHD 的快照，然後複製此快照。</span><span class="sxs-lookup"><span data-stu-id="e5dad-515">Alternately, you can create a snapshot of the VHD first and then copy the snapshot.</span></span>

<span data-ttu-id="e5dad-516">如果您無法在複製時防止其他應用程式寫入 Blob 或檔案，請記住，工作完成時，複製的資源可能不再與來源資源完全相同。</span><span class="sxs-lookup"><span data-stu-id="e5dad-516">If you cannot prevent other applications from writing to blobs or files while they are being copied, then keep in mind that by the time the job finishes, the copied resources may no longer have full parity with the source resources.</span></span>

### <a name="run-one-azcopy-instance-on-one-machine"></a><span data-ttu-id="e5dad-517">在一部電腦上執行一個 AzCopy 執行個體。</span><span class="sxs-lookup"><span data-stu-id="e5dad-517">Run one AzCopy instance on one machine.</span></span>
<span data-ttu-id="e5dad-518">AzCopy 設計為充分利用電腦資源來加速資料傳輸，建議您在一部電腦上只執行一個 AzCopy 執行個體，如果需要更多並行作業，您可以指定 `/NC` 選項。</span><span class="sxs-lookup"><span data-stu-id="e5dad-518">AzCopy is designed to maximize the utilization of your machine resource to accelerate the data transfer, we recommend you run only one AzCopy instance on one machine, and specify the option `/NC` if you need more concurrent operations.</span></span> <span data-ttu-id="e5dad-519">如需詳細資訊，請在命令列上輸入 `AzCopy /?:NC` 。</span><span class="sxs-lookup"><span data-stu-id="e5dad-519">For more details, type `AzCopy /?:NC` at the command line.</span></span>

### <a name="enable-fips-compliant-md5-algorithms-for-azcopy-when-you-use-fips-compliant-algorithms-for-encryption-hashing-and-signing"></a><span data-ttu-id="e5dad-520">當您「使用 FIPS 相容演算法於加密、雜湊及簽章」時，請為 AzCopy 啟用 FIPS 相容的 MD5 演算法。</span><span class="sxs-lookup"><span data-stu-id="e5dad-520">Enable FIPS compliant MD5 algorithms for AzCopy when you "Use FIPS compliant algorithms for encryption, hashing and signing".</span></span>
<span data-ttu-id="e5dad-521">複製物件時，AzCopy 預設會使用 .NET MD5 實作來計算此 MD5，但仍有一些需要 AzCopy 啟用 FIPS 相容 MD5 設定的安全性需求。</span><span class="sxs-lookup"><span data-stu-id="e5dad-521">AzCopy by default uses .NET MD5 implementation to calculate the MD5 when copying objects, but there are some security requirements that need AzCopy to enable FIPS compliant MD5 setting.</span></span>

<span data-ttu-id="e5dad-522">您可以建立具有 `AzureStorageUseV1MD5` 屬性的 app.config 檔案 `AzCopy.exe.config`，並將它放在 AzCopy.exe 旁邊。</span><span class="sxs-lookup"><span data-stu-id="e5dad-522">You can create an app.config file `AzCopy.exe.config` with property `AzureStorageUseV1MD5` and put it aside with AzCopy.exe.</span></span>

    <?xml version="1.0" encoding="utf-8" ?>
    <configuration>
      <appSettings>
        <add key="AzureStorageUseV1MD5" value="false"/>
      </appSettings>
    </configuration>

<span data-ttu-id="e5dad-523">針對屬性 "AzureStorageUseV1MD5" • True - 預設值，AzCopy 將使用 .NET MD5 實作。</span><span class="sxs-lookup"><span data-stu-id="e5dad-523">For property "AzureStorageUseV1MD5" • True - The default value, AzCopy will use .NET MD5 implementation.</span></span>
<span data-ttu-id="e5dad-524">• False – AzCopy 將使用 FIPS 相容的 MD5 演算法。</span><span class="sxs-lookup"><span data-stu-id="e5dad-524">• False – AzCopy will use FIPS compliant MD5 algorithm.</span></span>

<span data-ttu-id="e5dad-525">請注意 Windows 電腦預設會停用 FIPS 相容演算法，可以在您執行的視窗中輸入 secpol.msc，並在 [安全性設定] -> [本機原則] -> [安全性選項] -> [系統密碼編譯: 使用 FIPS 相容演算法於加密、雜湊及簽章] 檢查此參數。</span><span class="sxs-lookup"><span data-stu-id="e5dad-525">Note that FIPS compliant algorithms is disabled by default on your Windows machine, you can type secpol.msc in your Run window and check this switch at Security Setting->Local Policy->Security Options->System cryptography: Use FIPS compliant algorithms for encryption, hashing and signing.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e5dad-526">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e5dad-526">Next steps</span></span>
<span data-ttu-id="e5dad-527">如需關於 Azure 儲存體和 AzCopy 的詳細資訊，請參閱下列資源。</span><span class="sxs-lookup"><span data-stu-id="e5dad-527">For more information about Azure Storage and AzCopy, refer to the following resources.</span></span>

### <a name="azure-storage-documentation"></a><span data-ttu-id="e5dad-528">Azure 儲存體文件：</span><span class="sxs-lookup"><span data-stu-id="e5dad-528">Azure Storage documentation:</span></span>
* [<span data-ttu-id="e5dad-529">Azure 儲存體簡介</span><span class="sxs-lookup"><span data-stu-id="e5dad-529">Introduction to Azure Storage</span></span>](storage-introduction.md)
* [<span data-ttu-id="e5dad-530">如何使用 .NET 的 Blob 儲存體</span><span class="sxs-lookup"><span data-stu-id="e5dad-530">How to use Blob storage from .NET</span></span>](storage-dotnet-how-to-use-blobs.md)
* [<span data-ttu-id="e5dad-531">如何使用 .NET 的檔案儲存體</span><span class="sxs-lookup"><span data-stu-id="e5dad-531">How to use File storage from .NET</span></span>](storage-dotnet-how-to-use-files.md)
* [<span data-ttu-id="e5dad-532">如何使用 .NET 的資料表儲存體</span><span class="sxs-lookup"><span data-stu-id="e5dad-532">How to use Table storage from .NET</span></span>](storage-dotnet-how-to-use-tables.md)
* [<span data-ttu-id="e5dad-533">如何建立、管理或刪除儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="e5dad-533">How to create, manage, or delete a storage account</span></span>](storage-create-storage-account.md)
* [<span data-ttu-id="e5dad-534">使用 AzCopy on Linux 傳送資料</span><span class="sxs-lookup"><span data-stu-id="e5dad-534">Transfer data with AzCopy on Linux</span></span>](storage-use-azcopy-linux.md)

### <a name="azure-storage-blog-posts"></a><span data-ttu-id="e5dad-535">Azure 儲存體部落格文章：</span><span class="sxs-lookup"><span data-stu-id="e5dad-535">Azure Storage blog posts:</span></span>
* [<span data-ttu-id="e5dad-536">Azure 儲存體資料移動文件庫預覽簡介</span><span class="sxs-lookup"><span data-stu-id="e5dad-536">Introducing Azure Storage Data Movement Library Preview</span></span>](https://azure.microsoft.com/blog/introducing-azure-storage-data-movement-library-preview-2/)
* [<span data-ttu-id="e5dad-537">AzCopy：簡介同步複製和自訂內容類型</span><span class="sxs-lookup"><span data-stu-id="e5dad-537">AzCopy: Introducing synchronous copy and customized content type</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2015/01/13/azcopy-introducing-synchronous-copy-and-customized-content-type.aspx)
* [<span data-ttu-id="e5dad-538">AzCopy: 宣布正式發行 AzCopy 3.0 和具有資料表和檔案支援的 AzCopy 4.0 預覽版本</span><span class="sxs-lookup"><span data-stu-id="e5dad-538">AzCopy: Announcing General Availability of AzCopy 3.0 plus preview release of AzCopy 4.0 with Table and File support</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/10/29/azcopy-announcing-general-availability-of-azcopy-3-0-plus-preview-release-of-azcopy-4-0-with-table-and-file-support.aspx)
* [<span data-ttu-id="e5dad-539">AzCopy: 針對大規模複製案例最佳化</span><span class="sxs-lookup"><span data-stu-id="e5dad-539">AzCopy: Optimized for Large-Scale Copy Scenarios</span></span>](http://go.microsoft.com/fwlink/?LinkId=507682)
* [<span data-ttu-id="e5dad-540">AzCopy: 支援讀取存取異地備援儲存體</span><span class="sxs-lookup"><span data-stu-id="e5dad-540">AzCopy: Support for read-access geo-redundant storage</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/04/07/azcopy-support-for-read-access-geo-redundant-account.aspx)
* [<span data-ttu-id="e5dad-541">AzCopy: 使用可重新啟動模式和 SAS 權杖傳輸資料</span><span class="sxs-lookup"><span data-stu-id="e5dad-541">AzCopy: Transfer data with re-startable mode and SAS token</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/09/07/azcopy-transfer-data-with-re-startable-mode-and-sas-token.aspx)
* [<span data-ttu-id="e5dad-542">AzCopy: 使用跨帳戶複製 Blob</span><span class="sxs-lookup"><span data-stu-id="e5dad-542">AzCopy: Using cross-account Copy Blob</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/04/01/azcopy-using-cross-account-copy-blob.aspx)
* [<span data-ttu-id="e5dad-543">AzCopy: 上傳/下載 Azure Blob 的檔案</span><span class="sxs-lookup"><span data-stu-id="e5dad-543">AzCopy: Uploading/downloading files for Azure Blobs</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/12/03/azcopy-uploading-downloading-files-for-windows-azure-blobs.aspx)

