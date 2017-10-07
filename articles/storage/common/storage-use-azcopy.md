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
# <a name="transfer-data-with-hello-azcopy-on-windows"></a><span data-ttu-id="3e136-105">傳送資料，以在 Windows 上的 AzCopy hello</span><span class="sxs-lookup"><span data-stu-id="3e136-105">Transfer data with hello AzCopy on Windows</span></span>
<span data-ttu-id="3e136-106">AzCopy 是設計來複製資料 tooand 從 Microsoft Azure Blob、 檔案和資料表儲存體使用簡單的命令，以獲得最佳效能的命令列公用程式。</span><span class="sxs-lookup"><span data-stu-id="3e136-106">AzCopy is a command-line utility designed for copying data tooand from Microsoft Azure Blob, File, and Table storage using simple commands with optimal performance.</span></span> <span data-ttu-id="3e136-107">儲存體帳戶內或之間的儲存體帳戶，您可以從一個物件 tooanother 複製資料。</span><span class="sxs-lookup"><span data-stu-id="3e136-107">You can copy data from one object tooanother within your storage account, or between storage accounts.</span></span>

<span data-ttu-id="3e136-108">有兩個 AzCopy 版本可供您下載。</span><span class="sxs-lookup"><span data-stu-id="3e136-108">There are two versions of AzCopy that you can download.</span></span> <span data-ttu-id="3e136-109">AzCopy on Windows 內建有 .NET Framework，並且提供 Windows 樣式的命令列選項。</span><span class="sxs-lookup"><span data-stu-id="3e136-109">AzCopy on Windows is built with .NET Framework, and offers Windows style command-line options.</span></span> <span data-ttu-id="3e136-110">[AzCopy on Linux](storage-use-azcopy-linux.md) 內建有 .NET Core Framework，其以提供 POSIX 樣式命令列選項的 Linux 平台為目標。</span><span class="sxs-lookup"><span data-stu-id="3e136-110">[AzCopy on Linux](storage-use-azcopy-linux.md) is built with .NET Core Framework which targets Linux platforms offering POSIX style command-line options.</span></span> <span data-ttu-id="3e136-111">本文涵蓋之內容包括 AzCopy on Windows。</span><span class="sxs-lookup"><span data-stu-id="3e136-111">This article covers AzCopy on Windows.</span></span>

## <a name="download-and-install-azcopy"></a><span data-ttu-id="3e136-112">下載並安裝 AzCopy</span><span class="sxs-lookup"><span data-stu-id="3e136-112">Download and install AzCopy</span></span>
### <a name="azcopy-on-windows"></a><span data-ttu-id="3e136-113">AzCopy on Windows</span><span class="sxs-lookup"><span data-stu-id="3e136-113">AzCopy on Windows</span></span>
<span data-ttu-id="3e136-114">下載 hello[最新版本的 Windows 上的 AzCopy](http://aka.ms/downloadazcopy)。</span><span class="sxs-lookup"><span data-stu-id="3e136-114">Download hello [latest version of AzCopy on Windows](http://aka.ms/downloadazcopy).</span></span>

#### <a name="installation-on-windows"></a><span data-ttu-id="3e136-115">在 Windows 上安裝</span><span class="sxs-lookup"><span data-stu-id="3e136-115">Installation on Windows</span></span>
<span data-ttu-id="3e136-116">安裝之後 AzCopy 使用 hello 安裝程式在 Windows 上，開啟命令視窗，並瀏覽在您的電腦-toohello AzCopy 安裝目錄，其中 hello`AzCopy.exe`可執行檔所在。</span><span class="sxs-lookup"><span data-stu-id="3e136-116">After installing AzCopy on Windows using hello installer, open a command window and navigate toohello AzCopy installation directory on your computer - where hello `AzCopy.exe` executable is located.</span></span> <span data-ttu-id="3e136-117">如有需要，您可以加入 hello AzCopy 安裝位置 tooyour 系統路徑。</span><span class="sxs-lookup"><span data-stu-id="3e136-117">If desired, you can add hello AzCopy installation location tooyour system path.</span></span> <span data-ttu-id="3e136-118">根據預設，AzCopy 會太安裝`%ProgramFiles(x86)%\Microsoft SDKs\Azure\AzCopy`或`%ProgramFiles%\Microsoft SDKs\Azure\AzCopy`。</span><span class="sxs-lookup"><span data-stu-id="3e136-118">By default, AzCopy is installed too`%ProgramFiles(x86)%\Microsoft SDKs\Azure\AzCopy` or `%ProgramFiles%\Microsoft SDKs\Azure\AzCopy`.</span></span>

## <a name="writing-your-first-azcopy-command"></a><span data-ttu-id="3e136-119">撰寫第一個 AzCopy 命令</span><span class="sxs-lookup"><span data-stu-id="3e136-119">Writing your first AzCopy command</span></span>
<span data-ttu-id="3e136-120">hello 的 AzCopy 命令的基本語法如下：</span><span class="sxs-lookup"><span data-stu-id="3e136-120">hello basic syntax for AzCopy commands is:</span></span>

```azcopy
AzCopy /Source:<source> /Dest:<destination> [Options]
```

<span data-ttu-id="3e136-121">hello 遵循範例示範的各種案例來複製資料 tooand 從 Microsoft Azure Blob、 檔案和資料表。</span><span class="sxs-lookup"><span data-stu-id="3e136-121">hello following examples demonstrate a variety of scenarios for copying data tooand from Microsoft Azure Blobs, Files, and Tables.</span></span> <span data-ttu-id="3e136-122">請參閱 toohello [AzCopy 參數](#azcopy-parameters)hello 參數，每個範例中所使用的詳細說明一節。</span><span class="sxs-lookup"><span data-stu-id="3e136-122">Refer toohello [AzCopy Parameters](#azcopy-parameters) section for a detailed explanation of hello parameters used in each sample.</span></span>

## <a name="blob-download"></a><span data-ttu-id="3e136-123">Blob：下載</span><span class="sxs-lookup"><span data-stu-id="3e136-123">Blob: Download</span></span>
### <a name="download-single-blob"></a><span data-ttu-id="3e136-124">下載單一 Blob</span><span class="sxs-lookup"><span data-stu-id="3e136-124">Download single blob</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /Pattern:"abc.txt"
```

<span data-ttu-id="3e136-125">請注意，如果 hello 資料夾`C:\myfolder`不存在，AzCopy 會建立它，並下載`abc.txt `hello 新資料夾。</span><span class="sxs-lookup"><span data-stu-id="3e136-125">Note that if hello folder `C:\myfolder` does not exist, AzCopy creates it and download `abc.txt ` into hello new folder.</span></span>

### <a name="download-single-blob-from-secondary-region"></a><span data-ttu-id="3e136-126">從次要地區下載單一 Blob</span><span class="sxs-lookup"><span data-stu-id="3e136-126">Download single blob from secondary region</span></span>

```azcopy
AzCopy /Source:https://myaccount-secondary.blob.core.windows.net/mynewcontainer /Dest:C:\myfolder /SourceKey:key /Pattern:abc.txt
```

<span data-ttu-id="3e136-127">請注意，您必須啟用讀取權限異地備援儲存體。</span><span class="sxs-lookup"><span data-stu-id="3e136-127">Note that you must have read-access geo-redundant storage enabled.</span></span>

### <a name="download-all-blobs"></a><span data-ttu-id="3e136-128">下載所有 Blob</span><span class="sxs-lookup"><span data-stu-id="3e136-128">Download all blobs</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /S
```

<span data-ttu-id="3e136-129">假設下列 hello 位於 hello 指定容器的 blob:</span><span class="sxs-lookup"><span data-stu-id="3e136-129">Assume hello following blobs reside in hello specified container:</span></span>  

    abc.txt
    abc1.txt
    abc2.txt
    vd1\a.txt
    vd1\abcd.txt

<span data-ttu-id="3e136-130">Hello 下載作業之後，hello 目錄`C:\myfolder`包含下列檔案的 hello:</span><span class="sxs-lookup"><span data-stu-id="3e136-130">After hello download operation, hello directory `C:\myfolder` includes hello following files:</span></span>

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt
    C:\myfolder\vd1\a.txt
    C:\myfolder\vd1\abcd.txt

<span data-ttu-id="3e136-131">如果您未指定選項 `/S`，則不會下載任何 Blob。</span><span class="sxs-lookup"><span data-stu-id="3e136-131">If you do not specify option `/S`, no blobs are downloaded.</span></span>

### <a name="download-blobs-with-specified-prefix"></a><span data-ttu-id="3e136-132">下載具有指定首碼的 Blob</span><span class="sxs-lookup"><span data-stu-id="3e136-132">Download blobs with specified prefix</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /Pattern:a /S
```

<span data-ttu-id="3e136-133">假設 hello 下列 blob 位於 hello 指定的容器。</span><span class="sxs-lookup"><span data-stu-id="3e136-133">Assume hello following blobs reside in hello specified container.</span></span> <span data-ttu-id="3e136-134">以 hello 前置詞開頭的所有 blob`a`下載：</span><span class="sxs-lookup"><span data-stu-id="3e136-134">All blobs beginning with hello prefix `a` are downloaded:</span></span>

    abc.txt
    abc1.txt
    abc2.txt
    xyz.txt
    vd1\a.txt
    vd1\abcd.txt

<span data-ttu-id="3e136-135">Hello 下載作業之後，hello 資料夾`C:\myfolder`包含下列檔案的 hello:</span><span class="sxs-lookup"><span data-stu-id="3e136-135">After hello download operation, hello folder `C:\myfolder` includes hello following files:</span></span>

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt

<span data-ttu-id="3e136-136">hello 前置詞會套用 toohello 虛擬目錄，可形成 hello hello blob 名稱第一個部分。</span><span class="sxs-lookup"><span data-stu-id="3e136-136">hello prefix applies toohello virtual directory, which forms hello first part of hello blob name.</span></span> <span data-ttu-id="3e136-137">Hello 虛擬目錄在 hello 上述範例中，它不符合 hello 指定之前置詞，因此它不會下載。</span><span class="sxs-lookup"><span data-stu-id="3e136-137">In hello example shown above, hello virtual directory does not match hello specified prefix, so it is not downloaded.</span></span> <span data-ttu-id="3e136-138">此外，如果 hello 選項`\S`未指定，AzCopy 不會下載任何 blob。</span><span class="sxs-lookup"><span data-stu-id="3e136-138">In addition, if hello option `\S` is not specified, AzCopy does not download any blobs.</span></span>

### <a name="set-hello-last-modified-time-of-exported-files-toobe-same-as-hello-source-blobs"></a><span data-ttu-id="3e136-139">設定 hello toobe 匯出的檔案的上次修改時間與 hello 來源 blob 相同</span><span class="sxs-lookup"><span data-stu-id="3e136-139">Set hello last-modified time of exported files toobe same as hello source blobs</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /MT
```

<span data-ttu-id="3e136-140">您也可以從其上次修改時間為基礎的 hello 下載作業排除的 blob。</span><span class="sxs-lookup"><span data-stu-id="3e136-140">You can also exclude blobs from hello download operation based on their last-modified time.</span></span> <span data-ttu-id="3e136-141">例如，如果您想 tooexclude blob 的上次修改的時間為 hello 相同或較 hello 目的地檔案，加入 hello`/XN`選項：</span><span class="sxs-lookup"><span data-stu-id="3e136-141">For example, if you want tooexclude blobs whose last modified time is hello same or newer than hello destination file, add hello `/XN` option:</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /MT /XN
```

<span data-ttu-id="3e136-142">如果您想 tooexclude blob 的上次修改的時間為 hello 相同或比 hello 目的地檔案還舊，新增 hello 或`/XO`選項：</span><span class="sxs-lookup"><span data-stu-id="3e136-142">Or if you want tooexclude blobs whose last modified time is hello same or older than hello destination file, add hello `/XO` option:</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /MT /XO
```

## <a name="blob-upload"></a><span data-ttu-id="3e136-143">Blob：上傳</span><span class="sxs-lookup"><span data-stu-id="3e136-143">Blob: Upload</span></span>
### <a name="upload-single-file"></a><span data-ttu-id="3e136-144">上傳單一檔案</span><span class="sxs-lookup"><span data-stu-id="3e136-144">Upload single file</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Pattern:"abc.txt"
```

<span data-ttu-id="3e136-145">如果 hello 指定的目的地容器不存在，AzCopy 建立及上傳 hello 到其中的檔案。</span><span class="sxs-lookup"><span data-stu-id="3e136-145">If hello specified destination container does not exist, AzCopy creates it and uploads hello file into it.</span></span>

### <a name="upload-single-file-toovirtual-directory"></a><span data-ttu-id="3e136-146">單一檔案上傳 toovirtual 目錄</span><span class="sxs-lookup"><span data-stu-id="3e136-146">Upload single file toovirtual directory</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer/vd /DestKey:key /Pattern:abc.txt
```

<span data-ttu-id="3e136-147">如果 hello 指定虛擬目錄不存在，AzCopy 上傳 hello 檔案 tooinclude hello 虛擬目錄名稱 (*例如*， `vd/abc.txt` hello 上述範例中)。</span><span class="sxs-lookup"><span data-stu-id="3e136-147">If hello specified virtual directory does not exist, AzCopy uploads hello file tooinclude hello virtual directory in its name (*e.g.*, `vd/abc.txt` in hello example above).</span></span>

### <a name="upload-all-files"></a><span data-ttu-id="3e136-148">上傳所有檔案</span><span class="sxs-lookup"><span data-stu-id="3e136-148">Upload all files</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /S
```

<span data-ttu-id="3e136-149">指定選項`/S`hello 上傳 hello 內容所指定目錄 tooBlob 儲存體以遞迴方式，這表示所有子資料夾及檔案會上傳以及。</span><span class="sxs-lookup"><span data-stu-id="3e136-149">Specifying option `/S` uploads hello contents of hello specified directory tooBlob storage recursively, meaning that all subfolders and their files are uploaded as well.</span></span> <span data-ttu-id="3e136-150">比方說，假設 hello 下列檔案位於資料夾`C:\myfolder`:</span><span class="sxs-lookup"><span data-stu-id="3e136-150">For instance, assume hello following files reside in folder `C:\myfolder`:</span></span>

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt
    C:\myfolder\subfolder\a.txt
    C:\myfolder\subfolder\abcd.txt

<span data-ttu-id="3e136-151">Hello 上傳作業之後，hello 容器會包含下列檔案的 hello:</span><span class="sxs-lookup"><span data-stu-id="3e136-151">After hello upload operation, hello container includes hello following files:</span></span>

    abc.txt
    abc1.txt
    abc2.txt
    subfolder\a.txt
    subfolder\abcd.txt

<span data-ttu-id="3e136-152">如果您未指定選項 `/S`，AzCopy 不會以遞迴方式上傳。</span><span class="sxs-lookup"><span data-stu-id="3e136-152">If you do not specify option `/S`, AzCopy does not upload recursively.</span></span> <span data-ttu-id="3e136-153">Hello 上傳作業之後，hello 容器會包含下列檔案的 hello:</span><span class="sxs-lookup"><span data-stu-id="3e136-153">After hello upload operation, hello container includes hello following files:</span></span>

    abc.txt
    abc1.txt
    abc2.txt

### <a name="upload-files-matching-specified-pattern"></a><span data-ttu-id="3e136-154">上傳符合指定模式的檔案</span><span class="sxs-lookup"><span data-stu-id="3e136-154">Upload files matching specified pattern</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Pattern:a* /S
```

<span data-ttu-id="3e136-155">假設 hello 下列檔案位於資料夾`C:\myfolder`:</span><span class="sxs-lookup"><span data-stu-id="3e136-155">Assume hello following files reside in folder `C:\myfolder`:</span></span>

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt
    C:\myfolder\xyz.txt
    C:\myfolder\subfolder\a.txt
    C:\myfolder\subfolder\abcd.txt

<span data-ttu-id="3e136-156">Hello 上傳作業之後，hello 容器會包含下列檔案的 hello:</span><span class="sxs-lookup"><span data-stu-id="3e136-156">After hello upload operation, hello container includes hello following files:</span></span>

    abc.txt
    abc1.txt
    abc2.txt
    subfolder\a.txt
    subfolder\abcd.txt

<span data-ttu-id="3e136-157">如果您未指定選項 `/S`，AzCopy 只會上傳沒有位於虛擬目錄的 Blob：</span><span class="sxs-lookup"><span data-stu-id="3e136-157">If you do not specify option `/S`, AzCopy only uploads blobs that don't reside in a virtual directory:</span></span>

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt

### <a name="specify-hello-mime-content-type-of-a-destination-blob"></a><span data-ttu-id="3e136-158">指定目的地 blob hello MIME 內容的類型</span><span class="sxs-lookup"><span data-stu-id="3e136-158">Specify hello MIME content type of a destination blob</span></span>
<span data-ttu-id="3e136-159">根據預設，AzCopy 設定 hello 的目的地 blob 的內容型別太`application/octet-stream`。</span><span class="sxs-lookup"><span data-stu-id="3e136-159">By default, AzCopy sets hello content type of a destination blob too`application/octet-stream`.</span></span> <span data-ttu-id="3e136-160">從 3.1.0 版開始，您可以明確指定 hello 透過 hello 選項的內容類型`/SetContentType:[content-type]`。</span><span class="sxs-lookup"><span data-stu-id="3e136-160">Beginning with version 3.1.0, you can explicitly specify hello content type via hello option `/SetContentType:[content-type]`.</span></span> <span data-ttu-id="3e136-161">此語法中上傳作業設定 hello 的所有 blob 的內容類型。</span><span class="sxs-lookup"><span data-stu-id="3e136-161">This syntax sets hello content type for all blobs in an upload operation.</span></span>

```azcopy
AzCopy /Source:C:\myfolder\ /Dest:https://myaccount.blob.core.windows.net/myContainer/ /DestKey:key /Pattern:ab /SetContentType:video/mp4
```

<span data-ttu-id="3e136-162">如果您指定`/SetContentType`沒有值，AzCopy 會設定每個 blob 或根據 tooits 副檔名的檔案的內容類型。</span><span class="sxs-lookup"><span data-stu-id="3e136-162">If you specify `/SetContentType` without a value, AzCopy sets each blob or file's content type according tooits file extension.</span></span>

```azcopy
AzCopy /Source:C:\myfolder\ /Dest:https://myaccount.blob.core.windows.net/myContainer/ /DestKey:key /Pattern:ab /SetContentType
```

## <a name="blob-copy"></a><span data-ttu-id="3e136-163">Blob：複製</span><span class="sxs-lookup"><span data-stu-id="3e136-163">Blob: Copy</span></span>
### <a name="copy-single-blob-within-storage-account"></a><span data-ttu-id="3e136-164">複製儲存體帳戶內的單一 Blob</span><span class="sxs-lookup"><span data-stu-id="3e136-164">Copy single blob within Storage account</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer1 /Dest:https://myaccount.blob.core.windows.net/mycontainer2 /SourceKey:key /DestKey:key /Pattern:abc.txt
```

<span data-ttu-id="3e136-165">當您複製儲存體帳戶內的 Blob 時，系統會執行 [伺服器端複製](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) 作業。</span><span class="sxs-lookup"><span data-stu-id="3e136-165">When you copy a blob within a Storage account, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="copy-single-blob-across-storage-accounts"></a><span data-ttu-id="3e136-166">跨儲存體帳戶複製單一 Blob</span><span class="sxs-lookup"><span data-stu-id="3e136-166">Copy single blob across Storage accounts</span></span>

```azcopy
AzCopy /Source:https://sourceaccount.blob.core.windows.net/mycontainer1 /Dest:https://destaccount.blob.core.windows.net/mycontainer2 /SourceKey:key1 /DestKey:key2 /Pattern:abc.txt
```

<span data-ttu-id="3e136-167">當您跨儲存體帳戶複製 Blob 時，系統會執行 [伺服器端複製](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) 作業。</span><span class="sxs-lookup"><span data-stu-id="3e136-167">When you copy a blob across Storage accounts, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="copy-single-blob-from-secondary-region-tooprimary-region"></a><span data-ttu-id="3e136-168">從次要區域 tooprimary 區域複製單一 blob</span><span class="sxs-lookup"><span data-stu-id="3e136-168">Copy single blob from secondary region tooprimary region</span></span>

```azcopy
AzCopy /Source:https://myaccount1-secondary.blob.core.windows.net/mynewcontainer1 /Dest:https://myaccount2.blob.core.windows.net/mynewcontainer2 /SourceKey:key1 /DestKey:key2 /Pattern:abc.txt
```

<span data-ttu-id="3e136-169">請注意，您必須啟用讀取權限異地備援儲存體。</span><span class="sxs-lookup"><span data-stu-id="3e136-169">Note that you must have read-access geo-redundant storage enabled.</span></span>

### <a name="copy-single-blob-and-its-snapshots-across-storage-accounts"></a><span data-ttu-id="3e136-170">跨儲存體帳戶複製單一 Blob 及其快照</span><span class="sxs-lookup"><span data-stu-id="3e136-170">Copy single blob and its snapshots across Storage accounts</span></span>

```azcopy
    AzCopy /Source:https://sourceaccount.blob.core.windows.net/mycontainer1 /Dest:https://destaccount.blob.core.windows.net/mycontainer2 /SourceKey:key1 /DestKey:key2 /Pattern:abc.txt /Snapshot
```

<span data-ttu-id="3e136-171">Hello 複製作業之後，hello 目標容器包含 hello blob 和其快照集。</span><span class="sxs-lookup"><span data-stu-id="3e136-171">After hello copy operation, hello target container includes hello blob and its snapshots.</span></span> <span data-ttu-id="3e136-172">假設在 hello 上述範例中的 hello blob 具有兩個快照集，hello 容器包含 hello 下列 blob 和快照集：</span><span class="sxs-lookup"><span data-stu-id="3e136-172">Assuming hello blob in hello example above has two snapshots, hello container includes hello following blob and snapshots:</span></span>

    abc.txt
    abc (2013-02-25 080757).txt
    abc (2014-02-21 150331).txt

### <a name="synchronously-copy-blobs-across-storage-accounts"></a><span data-ttu-id="3e136-173">以同步方式跨儲存體帳戶複製 Blob</span><span class="sxs-lookup"><span data-stu-id="3e136-173">Synchronously copy blobs across Storage accounts</span></span>
<span data-ttu-id="3e136-174">根據預設，AzCopy 會以非同步方式在兩個儲存體端點之間複製資料。</span><span class="sxs-lookup"><span data-stu-id="3e136-174">AzCopy by default copies data between two storage endpoints asynchronously.</span></span> <span data-ttu-id="3e136-175">因此，複製 hello 背景使用的備用頻寬容量且沒有 SLA 方面的速度有多快 blob 中的 hello 複製作業執行時，而且 AzCopy 定期檢查 hello 複製狀態，直到 hello 複製完成或失敗。</span><span class="sxs-lookup"><span data-stu-id="3e136-175">Therefore, hello copy operation runs in hello background using spare bandwidth capacity that has no SLA in terms of how fast a blob is copied, and AzCopy periodically checks hello copy status until hello copying is completed or failed.</span></span>

<span data-ttu-id="3e136-176">hello`/SyncCopy`選項可確保 hello 複製作業取得一致的速度。</span><span class="sxs-lookup"><span data-stu-id="3e136-176">hello `/SyncCopy` option ensures that hello copy operation gets consistent speed.</span></span> <span data-ttu-id="3e136-177">AzCopy 下載 hello blob 執行 hello 同步複本 toocopy hello 從指定來源 toolocal 記憶體，並再將其上傳 toohello Blob 儲存體目的地。</span><span class="sxs-lookup"><span data-stu-id="3e136-177">AzCopy performs hello synchronous copy by downloading hello blobs toocopy from hello specified source toolocal memory, and then uploading them toohello Blob storage destination.</span></span>

```azcopy
AzCopy /Source:https://myaccount1.blob.core.windows.net/myContainer/ /Dest:https://myaccount2.blob.core.windows.net/myContainer/ /SourceKey:key1 /DestKey:key2 /Pattern:ab /SyncCopy
```

<span data-ttu-id="3e136-178">`/SyncCopy`可能會用來產生建議的方法包括的額外成本比較的 tooasynchronous 複製 hello 的輸出是 toouse 處於 hello Azure VM 中的這個選項與您來源儲存體帳戶 tooavoid 出口成本相同的區域。</span><span class="sxs-lookup"><span data-stu-id="3e136-178">`/SyncCopy` might generate additional egress cost compared tooasynchronous copy, hello recommended approach is toouse this option in an Azure VM that is in hello same region as your source storage account tooavoid egress cost.</span></span>

## <a name="file-download"></a><span data-ttu-id="3e136-179">檔案：下載</span><span class="sxs-lookup"><span data-stu-id="3e136-179">File: Download</span></span>
### <a name="download-single-file"></a><span data-ttu-id="3e136-180">下載單一檔案</span><span class="sxs-lookup"><span data-stu-id="3e136-180">Download single file</span></span>

```azcopy
AzCopy /Source:https://myaccount.file.core.windows.net/myfileshare/myfolder1/ /Dest:C:\myfolder /SourceKey:key /Pattern:abc.txt
```

<span data-ttu-id="3e136-181">如果 hello 指定來源是 Azure 的檔案共用，則您必須指定 hello 確切的檔名，(*例如* `abc.txt`) toodownload 單一檔案，或指定選項`/S`toodownload 所有檔案在 hello 共用以遞迴方式。</span><span class="sxs-lookup"><span data-stu-id="3e136-181">If hello specified source is an Azure file share, then you must either specify hello exact file name, (*e.g.* `abc.txt`) toodownload a single file, or specify option `/S` toodownload all files in hello share recursively.</span></span> <span data-ttu-id="3e136-182">檔案模式和選項，嘗試 toospecify`/S`一起會產生錯誤。</span><span class="sxs-lookup"><span data-stu-id="3e136-182">Attempting toospecify both a file pattern and option `/S` together results in an error.</span></span>

### <a name="download-all-files"></a><span data-ttu-id="3e136-183">下載所有檔案</span><span class="sxs-lookup"><span data-stu-id="3e136-183">Download all files</span></span>

```azcopy
AzCopy /Source:https://myaccount.file.core.windows.net/myfileshare/ /Dest:C:\myfolder /SourceKey:key /S
```

<span data-ttu-id="3e136-184">請注意，並不會下載任何空白資料夾。</span><span class="sxs-lookup"><span data-stu-id="3e136-184">Note that any empty folders are not downloaded.</span></span>

## <a name="file-upload"></a><span data-ttu-id="3e136-185">檔案：上傳</span><span class="sxs-lookup"><span data-stu-id="3e136-185">File: Upload</span></span>
### <a name="upload-single-file"></a><span data-ttu-id="3e136-186">上傳單一檔案</span><span class="sxs-lookup"><span data-stu-id="3e136-186">Upload single file</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.file.core.windows.net/myfileshare/ /DestKey:key /Pattern:abc.txt
```

### <a name="upload-all-files"></a><span data-ttu-id="3e136-187">上傳所有檔案</span><span class="sxs-lookup"><span data-stu-id="3e136-187">Upload all files</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.file.core.windows.net/myfileshare/ /DestKey:key /S
```

<span data-ttu-id="3e136-188">請注意，並不會上傳任何空白資料夾。</span><span class="sxs-lookup"><span data-stu-id="3e136-188">Note that any empty folders are not uploaded.</span></span>

### <a name="upload-files-matching-specified-pattern"></a><span data-ttu-id="3e136-189">上傳符合指定模式的檔案</span><span class="sxs-lookup"><span data-stu-id="3e136-189">Upload files matching specified pattern</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.file.core.windows.net/myfileshare/ /DestKey:key /Pattern:ab* /S
```

## <a name="file-copy"></a><span data-ttu-id="3e136-190">檔案：複製</span><span class="sxs-lookup"><span data-stu-id="3e136-190">File: Copy</span></span>
### <a name="copy-across-file-shares"></a><span data-ttu-id="3e136-191">跨檔案共用複製</span><span class="sxs-lookup"><span data-stu-id="3e136-191">Copy across file shares</span></span>

```azcopy
AzCopy /Source:https://myaccount1.file.core.windows.net/myfileshare1/ /Dest:https://myaccount2.file.core.windows.net/myfileshare2/ /SourceKey:key1 /DestKey:key2 /S
```
<span data-ttu-id="3e136-192">當您跨檔案共用複製檔案時，系統會執行[伺服器端複製](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx)作業。</span><span class="sxs-lookup"><span data-stu-id="3e136-192">When you copy a file across file shares, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="copy-from-file-share-tooblob"></a><span data-ttu-id="3e136-193">從檔案共用 tooblob 複製</span><span class="sxs-lookup"><span data-stu-id="3e136-193">Copy from file share tooblob</span></span>

```azcopy
AzCopy /Source:https://myaccount1.file.core.windows.net/myfileshare/ /Dest:https://myaccount2.blob.core.windows.net/mycontainer/ /SourceKey:key1 /DestKey:key2 /S
```
<span data-ttu-id="3e136-194">當您複製檔案從檔案共用 tooblob，[伺服器端副本](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx)執行作業。</span><span class="sxs-lookup"><span data-stu-id="3e136-194">When you copy a file from file share tooblob, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>


### <a name="copy-from-blob-toofile-share"></a><span data-ttu-id="3e136-195">複製 blob toofile 共用</span><span class="sxs-lookup"><span data-stu-id="3e136-195">Copy from blob toofile share</span></span>

```azcopy
AzCopy /Source:https://myaccount1.blob.core.windows.net/mycontainer/ /Dest:https://myaccount2.file.core.windows.net/myfileshare/ /SourceKey:key1 /DestKey:key2 /S
```
<span data-ttu-id="3e136-196">當您複製檔案從 blob toofile 共用，[伺服器端副本](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx)執行作業。</span><span class="sxs-lookup"><span data-stu-id="3e136-196">When you copy a file from blob toofile share, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="synchronously-copy-files"></a><span data-ttu-id="3e136-197">以同步方式複製檔案</span><span class="sxs-lookup"><span data-stu-id="3e136-197">Synchronously copy files</span></span>
<span data-ttu-id="3e136-198">您可以指定 hello`/SyncCopy`選項 toocopy 資料檔案儲存體 tooFile 存放裝置，從檔案儲存體 tooBlob 存放裝置，然後從 Blob 儲存體 tooFile 存放同步執行，AzCopy 會下載 hello 來源資料 toolocal 記憶體並將它上傳再次 toodestination。</span><span class="sxs-lookup"><span data-stu-id="3e136-198">You can specify hello `/SyncCopy` option toocopy data from File Storage tooFile Storage, from File Storage tooBlob Storage and from Blob Storage tooFile Storage synchronously, AzCopy does this by downloading hello source data toolocal memory and upload it again toodestination.</span></span> <span data-ttu-id="3e136-199">這會產生標準輸出成本。</span><span class="sxs-lookup"><span data-stu-id="3e136-199">Standard egress cost applies.</span></span>

```azcopy
AzCopy /Source:https://myaccount1.file.core.windows.net/myfileshare1/ /Dest:https://myaccount2.file.core.windows.net/myfileshare2/ /SourceKey:key1 /DestKey:key2 /S /SyncCopy
```

<span data-ttu-id="3e136-200">當複製檔案的儲存體 tooBlob 儲存體，hello 預設 blob 型別是區塊 blob，使用者可以指定選項`/BlobType:page`toochange hello 目的地 blob 類型。</span><span class="sxs-lookup"><span data-stu-id="3e136-200">When copying from File Storage tooBlob Storage, hello default blob type is block blob, user can specify option `/BlobType:page` toochange hello destination blob type.</span></span>

<span data-ttu-id="3e136-201">請注意，`/SyncCopy`可能會產生額外成本比較 tooasynchronous 複製的輸出，hello 建議的方法是中的這個選項 hello Azure VM 中 hello toouse 來源儲存體帳戶 tooavoid 出口成本與相同的區域。</span><span class="sxs-lookup"><span data-stu-id="3e136-201">Note that `/SyncCopy` might generate additional egress cost comparing tooasynchronous copy, hello recommended approach is toouse this option in hello Azure VM which is in hello same region as your source storage account tooavoid egress cost.</span></span>

## <a name="table-export"></a><span data-ttu-id="3e136-202">資料表：匯出</span><span class="sxs-lookup"><span data-stu-id="3e136-202">Table: Export</span></span>
### <a name="export-table"></a><span data-ttu-id="3e136-203">匯出資料表</span><span class="sxs-lookup"><span data-stu-id="3e136-203">Export table</span></span>

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:C:\myfolder\ /SourceKey:key
```

<span data-ttu-id="3e136-204">AzCopy 寫入資訊清單檔案 toohello 指定的目的地資料夾。</span><span class="sxs-lookup"><span data-stu-id="3e136-204">AzCopy writes a manifest file toohello specified destination folder.</span></span> <span data-ttu-id="3e136-205">hello 資訊清單檔案用於 hello 匯入程序 toolocate hello 必要的資料檔案，並執行資料驗證。</span><span class="sxs-lookup"><span data-stu-id="3e136-205">hello manifest file is used in hello import process toolocate hello necessary data files and perform data validation.</span></span> <span data-ttu-id="3e136-206">hello 資訊清單檔案會使用下列預設的命名慣例的 hello:</span><span class="sxs-lookup"><span data-stu-id="3e136-206">hello manifest file uses hello following naming convention by default:</span></span>

    <account name>_<table name>_<timestamp>.manifest

<span data-ttu-id="3e136-207">使用者也可以指定 hello 選項`/Manifest:<manifest file name>`tooset hello 資訊清單檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="3e136-207">User can also specify hello option `/Manifest:<manifest file name>` tooset hello manifest file name.</span></span>

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:C:\myfolder\ /SourceKey:key /Manifest:abc.manifest
```

### <a name="split-export-into-multiple-files"></a><span data-ttu-id="3e136-208">將匯出分割成多個檔案</span><span class="sxs-lookup"><span data-stu-id="3e136-208">Split export into multiple files</span></span>

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/mytable/ /Dest:C:\myfolder /SourceKey:key /S /SplitSize:100
```

<span data-ttu-id="3e136-209">使用 AzCopy*成交量*hello 資料分割中檔案名稱 toodistinguish 多個檔案。</span><span class="sxs-lookup"><span data-stu-id="3e136-209">AzCopy uses a *volume index* in hello split data file names toodistinguish multiple files.</span></span> <span data-ttu-id="3e136-210">hello 磁碟區索引由兩個部分組成，*資料分割索引鍵範圍索引*和*分割檔案索引*。</span><span class="sxs-lookup"><span data-stu-id="3e136-210">hello volume index consists of two parts, a *partition key range index* and a *split file index*.</span></span> <span data-ttu-id="3e136-211">兩個索引皆以零為基礎。</span><span class="sxs-lookup"><span data-stu-id="3e136-211">Both indexes are zero-based.</span></span>

<span data-ttu-id="3e136-212">hello 資料分割索引鍵範圍索引為 0，如果 hello 使用者未指定選項`/PKRS`。</span><span class="sxs-lookup"><span data-stu-id="3e136-212">hello partition key range index is 0 if hello user does not specify option `/PKRS`.</span></span>

<span data-ttu-id="3e136-213">例如，假設 AzCopy 會產生兩個資料檔案之後 hello 使用者指定選項, `/SplitSize`。</span><span class="sxs-lookup"><span data-stu-id="3e136-213">For instance, suppose AzCopy generates two data files after hello user specifies option `/SplitSize`.</span></span> <span data-ttu-id="3e136-214">可能造成資料檔案名稱的 hello:</span><span class="sxs-lookup"><span data-stu-id="3e136-214">hello resulting data file names might be:</span></span>

    myaccount_mytable_20140903T051850.8128447Z_0_0_C3040FE8.json
    myaccount_mytable_20140903T051850.8128447Z_0_1_0AB9AC20.json

<span data-ttu-id="3e136-215">請注意該 hello 最小可能值選項`/SplitSize`為 32 MB。</span><span class="sxs-lookup"><span data-stu-id="3e136-215">Note that hello minimum possible value for option `/SplitSize` is 32MB.</span></span> <span data-ttu-id="3e136-216">如果 hello 指定目的地 Blob 儲存體，AzCopy 分割 hello 資料檔案，一旦它的大小達到 hello blob 大小上限 (200 GB)，不論是否選項`/SplitSize`hello 使用者尚未指定。</span><span class="sxs-lookup"><span data-stu-id="3e136-216">If hello specified destination is Blob storage, AzCopy splits hello data file once its sizes reaches hello blob size limitation (200GB), regardless of whether option `/SplitSize` has been specified by hello user.</span></span>

### <a name="export-table-toojson-or-csv-data-file-format"></a><span data-ttu-id="3e136-217">匯出資料表 tooJSON 或 CSV 資料檔格式</span><span class="sxs-lookup"><span data-stu-id="3e136-217">Export table tooJSON or CSV data file format</span></span>
<span data-ttu-id="3e136-218">預設的 AzCopy 匯出資料表 tooJSON 資料檔案。</span><span class="sxs-lookup"><span data-stu-id="3e136-218">AzCopy by default exports tables tooJSON data files.</span></span> <span data-ttu-id="3e136-219">您可以指定 hello 選項`/PayloadFormat:JSON|CSV`tooexport hello 資料表做為 JSON 或 CSV。</span><span class="sxs-lookup"><span data-stu-id="3e136-219">You can specify hello option `/PayloadFormat:JSON|CSV` tooexport hello tables as JSON or CSV.</span></span>

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:C:\myfolder\ /SourceKey:key /PayloadFormat:CSV
```

<span data-ttu-id="3e136-220">指定 hello CSV 裝載格式，AzCopy 也會產生結構描述檔案具有副檔名`.schema.csv`每個資料檔。</span><span class="sxs-lookup"><span data-stu-id="3e136-220">When specifying hello CSV payload format, AzCopy also generates a schema file with file extension `.schema.csv` for each data file.</span></span>

### <a name="export-table-entities-concurrently"></a><span data-ttu-id="3e136-221">並行匯出資料表實體</span><span class="sxs-lookup"><span data-stu-id="3e136-221">Export table entities concurrently</span></span>

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:C:\myfolder\ /SourceKey:key /PKRS:"aa#bb"
```

<span data-ttu-id="3e136-222">AzCopy hello 使用者指定 選項時，請啟動並行作業 tooexport 實體`/PKRS`。</span><span class="sxs-lookup"><span data-stu-id="3e136-222">AzCopy starts concurrent operations tooexport entities when hello user specifies option `/PKRS`.</span></span> <span data-ttu-id="3e136-223">每個作業分別會匯出一個資料分割索引鍵範圍。</span><span class="sxs-lookup"><span data-stu-id="3e136-223">Each operation exports one partition key range.</span></span>

<span data-ttu-id="3e136-224">請注意 hello 並行作業的數目也由選項`/NC`。</span><span class="sxs-lookup"><span data-stu-id="3e136-224">Note that hello number of concurrent operations is also controlled by option `/NC`.</span></span> <span data-ttu-id="3e136-225">AzCopy hello 預設值為使用核心處理器的 hello 數目`/NC`複製資料表實體時即使`/NC`未指定。</span><span class="sxs-lookup"><span data-stu-id="3e136-225">AzCopy uses hello number of core processors as hello default value of `/NC` when copying table entities, even if `/NC` was not specified.</span></span> <span data-ttu-id="3e136-226">當 hello 使用者指定選項`/PKRS`，AzCopy 會使用 hello 的並行作業 toostart hello 兩個值-使用隱含或明確地指定並行作業與資料分割索引鍵範圍-toodetermine hello 數目的較小者。</span><span class="sxs-lookup"><span data-stu-id="3e136-226">When hello user specifies option `/PKRS`, AzCopy uses hello smaller of hello two values - partition key ranges versus implicitly or explicitly specified concurrent operations - toodetermine hello number of concurrent operations toostart.</span></span> <span data-ttu-id="3e136-227">如需詳細資訊，請輸入`AzCopy /?:NC`在 hello 命令列。</span><span class="sxs-lookup"><span data-stu-id="3e136-227">For more details, type `AzCopy /?:NC` at hello command line.</span></span>

### <a name="export-table-tooblob"></a><span data-ttu-id="3e136-228">匯出資料表 tooblob</span><span class="sxs-lookup"><span data-stu-id="3e136-228">Export table tooblob</span></span>

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:https://myaccount.blob.core.windows.net/mycontainer/ /SourceKey:key1 /Destkey:key2
```

<span data-ttu-id="3e136-229">AzCopy 會將 JSON 資料檔產生至 hello blob 容器中具有下列命名慣例：</span><span class="sxs-lookup"><span data-stu-id="3e136-229">AzCopy generates a JSON data file into hello blob container with following naming convention:</span></span>

    <account name>_<table name>_<timestamp>_<volume index>_<CRC>.json

<span data-ttu-id="3e136-230">hello 產生 JSON 資料檔會遵循最小中繼資料的 hello 裝載格式。</span><span class="sxs-lookup"><span data-stu-id="3e136-230">hello generated JSON data file follows hello payload format for minimal metadata.</span></span> <span data-ttu-id="3e136-231">如需此裝載格式的詳細資訊，請參閱 [資料表服務作業的裝載格式](http://msdn.microsoft.com/library/azure/dn535600.aspx)。</span><span class="sxs-lookup"><span data-stu-id="3e136-231">For details on this payload format, see [Payload Format for Table Service Operations](http://msdn.microsoft.com/library/azure/dn535600.aspx).</span></span>

<span data-ttu-id="3e136-232">請注意，匯出資料表 tooblobs 時, AzCopy 會下載 hello 資料表實體 toolocal 暫存資料檔案，然後將這些實體 toohello blob 上傳。</span><span class="sxs-lookup"><span data-stu-id="3e136-232">Note that when exporting tables tooblobs, AzCopy downloads hello Table entities toolocal temporary data files and then uploads those entities toohello blob.</span></span> <span data-ttu-id="3e136-233">這些暫存資料檔案會放入與 hello 預設路徑 hello 日誌檔案的資料夾"<code>%LocalAppData%\Microsoft\Azure\AzCopy</code>」，您可以指定選項/z: [日誌-檔案-資料夾] toochange hello 日誌檔案資料夾位置，並因此變更 hello 暫存資料檔案位置。</span><span class="sxs-lookup"><span data-stu-id="3e136-233">These temporary data files are put into hello journal file folder with hello default path "<code>%LocalAppData%\Microsoft\Azure\AzCopy</code>", you can specify option /Z:[journal-file-folder] toochange hello journal file folder location and thus change hello temporary data files location.</span></span> <span data-ttu-id="3e136-234">hello 雖然一旦它已在本機磁碟中的 hello 暫存資料檔案會立即刪除，檔案的大小由資料表實體的大小和您指定了與 hello 選項 /SplitSize，hello 大小來決定暫存資料上傳 toohello blob，請確定您有足夠的本機磁碟空間 toostore 這些暫存資料檔案之前，先刪除它們。</span><span class="sxs-lookup"><span data-stu-id="3e136-234">hello temporary data files' size is decided by your table entities' size and hello size you specified with hello option /SplitSize, although hello temporary data file in local disk is deleted instantly once it has been uploaded toohello blob, please make sure you have enough local disk space toostore these temporary data files before they are deleted.</span></span>

## <a name="table-import"></a><span data-ttu-id="3e136-235">資料表：匯入</span><span class="sxs-lookup"><span data-stu-id="3e136-235">Table: Import</span></span>
### <a name="import-table"></a><span data-ttu-id="3e136-236">匯入資料表</span><span class="sxs-lookup"><span data-stu-id="3e136-236">Import table</span></span>

```azcopy
AzCopy /Source:C:\myfolder\ /Dest:https://myaccount.table.core.windows.net/mytable1/ /DestKey:key /Manifest:"myaccount_mytable_20140103T112020.manifest" /EntityOperation:InsertOrReplace
```

<span data-ttu-id="3e136-237">hello 選項`/EntityOperation`表示成 tooinsert 實體 hello 資料表的方式。</span><span class="sxs-lookup"><span data-stu-id="3e136-237">hello option `/EntityOperation` indicates how tooinsert entities into hello table.</span></span> <span data-ttu-id="3e136-238">可能的值包括：</span><span class="sxs-lookup"><span data-stu-id="3e136-238">Possible values are:</span></span>

* <span data-ttu-id="3e136-239">`InsertOrSkip`： 略過現有的實體，或如果不存在於 hello 資料表插入新實體。</span><span class="sxs-lookup"><span data-stu-id="3e136-239">`InsertOrSkip`: Skips an existing entity or inserts a new entity if it does not exist in hello table.</span></span>
* <span data-ttu-id="3e136-240">`InsertOrMerge`： 會合併現有的實體，或不存在於 hello 資料表插入新實體。</span><span class="sxs-lookup"><span data-stu-id="3e136-240">`InsertOrMerge`: Merges an existing entity or inserts a new entity if it does not exist in hello table.</span></span>
* <span data-ttu-id="3e136-241">`InsertOrReplace`： 取代現有的實體，或不存在於 hello 資料表插入新實體。</span><span class="sxs-lookup"><span data-stu-id="3e136-241">`InsertOrReplace`: Replaces an existing entity or inserts a new entity if it does not exist in hello table.</span></span>

<span data-ttu-id="3e136-242">請注意，您不能指定選項`/PKRS`hello 匯入案例中。</span><span class="sxs-lookup"><span data-stu-id="3e136-242">Note that you cannot specify option `/PKRS` in hello import scenario.</span></span> <span data-ttu-id="3e136-243">不同於 hello 匯出案例中，您必須在其中指定選項`/PKRS`toostart 並行作業，AzCopy 並行作業，預設會啟動匯入資料表時。</span><span class="sxs-lookup"><span data-stu-id="3e136-243">Unlike hello export scenario, in which you must specify option `/PKRS` toostart concurrent operations, AzCopy starts concurrent operations by default when you import a table.</span></span> <span data-ttu-id="3e136-244">並行作業啟動的 hello 預設數目是相等的 toohello 核心處理器數目;不過，您可以指定不同數目的並行選項`/NC`。</span><span class="sxs-lookup"><span data-stu-id="3e136-244">hello default number of concurrent operations started is equal toohello number of core processors; however, you can specify a different number of concurrent with option `/NC`.</span></span> <span data-ttu-id="3e136-245">如需詳細資訊，請輸入`AzCopy /?:NC`在 hello 命令列。</span><span class="sxs-lookup"><span data-stu-id="3e136-245">For more details, type `AzCopy /?:NC` at hello command line.</span></span>

<span data-ttu-id="3e136-246">請注意，AzCopy 只支援匯入 JSON 而不支援匯入 CSV。</span><span class="sxs-lookup"><span data-stu-id="3e136-246">Note that AzCopy only supports importing for JSON, not CSV.</span></span> <span data-ttu-id="3e136-247">AzCopy 不支援從使用者建立的 JSON 和資訊清單檔案匯入資料表。</span><span class="sxs-lookup"><span data-stu-id="3e136-247">AzCopy does not support table imports from user-created JSON and manifest files.</span></span> <span data-ttu-id="3e136-248">這兩種檔案都必須來自 AzCopy 資料表匯出。</span><span class="sxs-lookup"><span data-stu-id="3e136-248">Both of these files must come from an AzCopy table export.</span></span> <span data-ttu-id="3e136-249">tooavoid 錯誤，請勿修改 hello 匯出 JSON 或資訊清單檔案。</span><span class="sxs-lookup"><span data-stu-id="3e136-249">tooavoid errors, please do not modify hello exported JSON or manifest file.</span></span>

### <a name="import-entities-tootable-using-blobs"></a><span data-ttu-id="3e136-250">匯入實體 tootable 使用 blob</span><span class="sxs-lookup"><span data-stu-id="3e136-250">Import entities tootable using blobs</span></span>
<span data-ttu-id="3e136-251">假設 Blob 容器包含 hello 下列： 代表 Azure 資料表和其隨附的資訊清單檔案的 JSON 檔案。</span><span class="sxs-lookup"><span data-stu-id="3e136-251">Assume a Blob container contains hello following: A JSON file representing an Azure Table and its accompanying manifest file.</span></span>

    myaccount_mytable_20140103T112020.manifest
    myaccount_mytable_20140103T112020_0_0_0AF395F1DC42E952.json

<span data-ttu-id="3e136-252">您可以執行下列命令 tooimport 實體插入資料表，使用該 blob 容器中的 hello 資訊清單檔案的 hello:</span><span class="sxs-lookup"><span data-stu-id="3e136-252">You can run hello following command tooimport entities into a table using hello manifest file in that blob container:</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:https://myaccount.table.core.windows.net/mytable /SourceKey:key1 /DestKey:key2 /Manifest:"myaccount_mytable_20140103T112020.manifest" /EntityOperation:"InsertOrReplace"
```

## <a name="other-azcopy-features"></a><span data-ttu-id="3e136-253">其他 AzCopy 功能</span><span class="sxs-lookup"><span data-stu-id="3e136-253">Other AzCopy features</span></span>
### <a name="only-copy-data-that-doesnt-exist-in-hello-destination"></a><span data-ttu-id="3e136-254">只複製 hello 目的地中不存在的資料</span><span class="sxs-lookup"><span data-stu-id="3e136-254">Only copy data that doesn't exist in hello destination</span></span>
<span data-ttu-id="3e136-255">hello`/XO`和`/XN`參數可讓您從要複製，分別 tooexclude 更舊或更新的來源資源。</span><span class="sxs-lookup"><span data-stu-id="3e136-255">hello `/XO` and `/XN` parameters allow you tooexclude older or newer source resources from being copied, respectively.</span></span> <span data-ttu-id="3e136-256">如果您只想 toocopy 來源資源不存在於 hello 目的地中，您可以在 hello AzCopy 命令中指定這兩個參數：</span><span class="sxs-lookup"><span data-stu-id="3e136-256">If you only want toocopy source resources that don't exist in hello destination, you can specify both parameters in hello AzCopy command:</span></span>

    /Source:http://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:<sourcekey> /S /XO /XN

    /Source:C:\myfolder /Dest:http://myaccount.file.core.windows.net/myfileshare /DestKey:<destkey> /S /XO /XN

    /Source:http://myaccount.blob.core.windows.net/mycontainer /Dest:http://myaccount.blob.core.windows.net/mycontainer1 /SourceKey:<sourcekey> /DestKey:<destkey> /S /XO /XN

<span data-ttu-id="3e136-257">請注意，這不支援當 hello 來源或目的地資料表。</span><span class="sxs-lookup"><span data-stu-id="3e136-257">Note that this is not supported when either hello source or destination is a table.</span></span>

### <a name="use-a-response-file-toospecify-command-line-parameters"></a><span data-ttu-id="3e136-258">您可以使用回應檔案 toospecify 命令列參數</span><span class="sxs-lookup"><span data-stu-id="3e136-258">Use a response file toospecify command-line parameters</span></span>

```azcopy
AzCopy /@:"C:\responsefiles\copyoperation.txt"
```

<span data-ttu-id="3e136-259">您可以在回應檔案中包含任何 AzCopy 命令列參數。</span><span class="sxs-lookup"><span data-stu-id="3e136-259">You can include any AzCopy command-line parameters in a response file.</span></span> <span data-ttu-id="3e136-260">AzCopy 處理程序 hello hello 檔案中的參數，如同它們已執行 hello 檔案直接替代與 hello 內容的 hello 命令列上指定。</span><span class="sxs-lookup"><span data-stu-id="3e136-260">AzCopy processes hello parameters in hello file as if they had been specified on hello command line, performing a direct substitution with hello contents of hello file.</span></span>

<span data-ttu-id="3e136-261">假設名為的回應檔案`copyoperation.txt`，其中包含下列行 hello。</span><span class="sxs-lookup"><span data-stu-id="3e136-261">Assume a response file named `copyoperation.txt`, that contains hello following lines.</span></span> <span data-ttu-id="3e136-262">每個 AzCopy 參數可以指定在同一行</span><span class="sxs-lookup"><span data-stu-id="3e136-262">Each AzCopy parameter can be specified on a single line</span></span>

    /Source:http://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:<sourcekey> /S /Y

<span data-ttu-id="3e136-263">或不同行：</span><span class="sxs-lookup"><span data-stu-id="3e136-263">or on separate lines:</span></span>

    /Source:http://myaccount.blob.core.windows.net/mycontainer
    /Dest:C:\myfolder
    /SourceKey:<sourcekey>
    /S
    /Y

<span data-ttu-id="3e136-264">AzCopy 失敗如果 hello 參數分成兩行，如下所示為 hello`/sourcekey`參數：</span><span class="sxs-lookup"><span data-stu-id="3e136-264">AzCopy fails if you split hello parameter across two lines, as shown here for hello `/sourcekey` parameter:</span></span>

    http://myaccount.blob.core.windows.net/mycontainer
     C:\myfolder
    /sourcekey:
    <sourcekey>
    /S
    /Y

### <a name="use-multiple-response-files-toospecify-command-line-parameters"></a><span data-ttu-id="3e136-265">使用多個回應檔案 toospecify 命令列參數</span><span class="sxs-lookup"><span data-stu-id="3e136-265">Use multiple response files toospecify command-line parameters</span></span>
<span data-ttu-id="3e136-266">假設名為 `source.txt` 且指定來源容器的回應檔案：</span><span class="sxs-lookup"><span data-stu-id="3e136-266">Assume a response file named `source.txt` that specifies a source container:</span></span>

    /Source:http://myaccount.blob.core.windows.net/mycontainer

<span data-ttu-id="3e136-267">名為的回應檔案和`dest.txt`hello 檔案系統中指定的目的地資料夾：</span><span class="sxs-lookup"><span data-stu-id="3e136-267">And a response file named `dest.txt` that specifies a destination folder in hello file system:</span></span>

    /Dest:C:\myfolder

<span data-ttu-id="3e136-268">及名為 `options.txt` 且指定 AzCopy 選項的回應檔案：</span><span class="sxs-lookup"><span data-stu-id="3e136-268">And a response file named `options.txt` that specifies options for AzCopy:</span></span>

    /S /Y

<span data-ttu-id="3e136-269">這些回應檔案 toocall AzCopy，全部都是位於目錄`C:\responsefiles`，使用此命令：</span><span class="sxs-lookup"><span data-stu-id="3e136-269">toocall AzCopy with these response files, all of which reside in a directory `C:\responsefiles`, use this command:</span></span>

```azcopy
AzCopy /@:"C:\responsefiles\source.txt" /@:"C:\responsefiles\dest.txt" /SourceKey:<sourcekey> /@:"C:\responsefiles\options.txt"   
```

<span data-ttu-id="3e136-270">AzCopy 會處理這個命令就如同您所包含的所有 hello hello 命令列上的個別參數都一樣：</span><span class="sxs-lookup"><span data-stu-id="3e136-270">AzCopy processes this command just as it would if you included all of hello individual parameters on hello command line:</span></span>

```azcopy
AzCopy /Source:http://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:<sourcekey> /S /Y
```

### <a name="specify-a-shared-access-signature-sas"></a><span data-ttu-id="3e136-271">指定共用存取簽章 (SAS)</span><span class="sxs-lookup"><span data-stu-id="3e136-271">Specify a shared access signature (SAS)</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer1 /Dest:https://myaccount.blob.core.windows.net/mycontainer2 /SourceSAS:SAS1 /DestSAS:SAS2 /Pattern:abc.txt
```

<span data-ttu-id="3e136-272">您也可以指定 SAS hello 容器 URI 上：</span><span class="sxs-lookup"><span data-stu-id="3e136-272">You can also specify a SAS on hello container URI:</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer1/?SourceSASToken /Dest:C:\myfolder /S
```

### <a name="journal-file-folder"></a><span data-ttu-id="3e136-273">日誌檔案資料夾</span><span class="sxs-lookup"><span data-stu-id="3e136-273">Journal file folder</span></span>
<span data-ttu-id="3e136-274">每次您提交命令 tooAzCopy，它會檢查日誌檔是否存在於 hello 預設資料夾，或是否有您指定透過這個選項的資料夾中。</span><span class="sxs-lookup"><span data-stu-id="3e136-274">Each time you issue a command tooAzCopy, it checks whether a journal file exists in hello default folder, or whether it exists in a folder that you specified via this option.</span></span> <span data-ttu-id="3e136-275">如果在任一處，hello 日誌檔不存在，AzCopy hello 作業視為新，並產生新的日誌檔。</span><span class="sxs-lookup"><span data-stu-id="3e136-275">If hello journal file does not exist in either place, AzCopy treats hello operation as new and generates a new journal file.</span></span>

<span data-ttu-id="3e136-276">如果 hello 日誌檔案存在，AzCopy 會檢查您輸入的 hello 命令列是否符合 hello hello 筆記本檔案中的命令列。</span><span class="sxs-lookup"><span data-stu-id="3e136-276">If hello journal file does exist, AzCopy checks whether hello command line that you input matches hello command line in hello journal file.</span></span> <span data-ttu-id="3e136-277">如果兩個命令列 hello 相符，AzCopy 會繼續 hello 未完成作業。</span><span class="sxs-lookup"><span data-stu-id="3e136-277">If hello two command lines match, AzCopy resumes hello incomplete operation.</span></span> <span data-ttu-id="3e136-278">如果不相符，則提示的 tooeither 覆寫 hello 日誌檔案 toostart，新增作業或 toocancel hello 目前的作業。</span><span class="sxs-lookup"><span data-stu-id="3e136-278">If they do not match, you are prompted tooeither overwrite hello journal file toostart a new operation, or toocancel hello current operation.</span></span>

<span data-ttu-id="3e136-279">如果您想 hello 日誌檔 toouse hello 預設位置：</span><span class="sxs-lookup"><span data-stu-id="3e136-279">If you want toouse hello default location for hello journal file:</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Z
```

<span data-ttu-id="3e136-280">如果您省略選項`/Z`，或指定選項`/Z`未 hello 資料夾路徑，如上所示，AzCopy 會建立 hello 日誌檔 hello 預設位置，也就是在`%SystemDrive%\Users\%username%\AppData\Local\Microsoft\Azure\AzCopy`。</span><span class="sxs-lookup"><span data-stu-id="3e136-280">If you omit option `/Z`, or specify option `/Z` without hello folder path, as shown above, AzCopy creates hello journal file in hello default location, which is `%SystemDrive%\Users\%username%\AppData\Local\Microsoft\Azure\AzCopy`.</span></span> <span data-ttu-id="3e136-281">如果 hello 日誌檔已經存在，然後 AzCopy 會繼續 hello hello 日誌檔為基礎的作業。</span><span class="sxs-lookup"><span data-stu-id="3e136-281">If hello journal file already exists, then AzCopy resumes hello operation based on hello journal file.</span></span>

<span data-ttu-id="3e136-282">如果您想 toospecify hello 日誌檔的自訂位置：</span><span class="sxs-lookup"><span data-stu-id="3e136-282">If you want toospecify a custom location for hello journal file:</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Z:C:\journalfolder\
```

<span data-ttu-id="3e136-283">如果不存在，此範例會建立 hello 日誌檔。</span><span class="sxs-lookup"><span data-stu-id="3e136-283">This example creates hello journal file if it does not already exist.</span></span> <span data-ttu-id="3e136-284">如果檔案存在，然後 AzCopy 會繼續依據 hello 日誌檔的 hello 作業。</span><span class="sxs-lookup"><span data-stu-id="3e136-284">If it does exist, then AzCopy resumes hello operation based on hello journal file.</span></span>

<span data-ttu-id="3e136-285">如果您想 tooresume AzCopy 作業：</span><span class="sxs-lookup"><span data-stu-id="3e136-285">If you want tooresume an AzCopy operation:</span></span>

```azcopy
AzCopy /Z:C:\journalfolder\
```

<span data-ttu-id="3e136-286">此範例也會繼續 hello 最後一個作業，可能無法 toocomplete。</span><span class="sxs-lookup"><span data-stu-id="3e136-286">This example resumes hello last operation, which may have failed toocomplete.</span></span>

### <a name="generate-a-log-file"></a><span data-ttu-id="3e136-287">產生記錄檔</span><span class="sxs-lookup"><span data-stu-id="3e136-287">Generate a log file</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /V
```

<span data-ttu-id="3e136-288">如果您指定選項`/V`但未提供檔案路徑 toohello 詳細資訊記錄檔，再 AzCopy hello 記錄檔中建立 hello 預設位置，也就是`%SystemDrive%\Users\%username%\AppData\Local\Microsoft\Azure\AzCopy`。</span><span class="sxs-lookup"><span data-stu-id="3e136-288">If you specify option `/V` without providing a file path toohello verbose log, then AzCopy creates hello log file in hello default location, which is `%SystemDrive%\Users\%username%\AppData\Local\Microsoft\Azure\AzCopy`.</span></span>

<span data-ttu-id="3e136-289">否則，您可以在自訂位置建立記錄檔：</span><span class="sxs-lookup"><span data-stu-id="3e136-289">Otherwise, you can create an log file in a custom location:</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /V:C:\myfolder\azcopy1.log
```

<span data-ttu-id="3e136-290">請注意，如果您指定下列選項的相對路徑`/V`，例如`/V:test/azcopy1.log`，則 hello 詳細資訊記錄檔會建立名為的子資料夾內 hello 目前工作目錄中`test`。</span><span class="sxs-lookup"><span data-stu-id="3e136-290">Note that if you specify a relative path following option `/V`, such as `/V:test/azcopy1.log`, then hello verbose log is created in hello current working directory within a subfolder named `test`.</span></span>

### <a name="specify-hello-number-of-concurrent-operations-toostart"></a><span data-ttu-id="3e136-291">指定的並行作業 toostart hello</span><span class="sxs-lookup"><span data-stu-id="3e136-291">Specify hello number of concurrent operations toostart</span></span>
<span data-ttu-id="3e136-292">選項`/NC`指定 hello 並行的複製作業數目。</span><span class="sxs-lookup"><span data-stu-id="3e136-292">Option `/NC` specifies hello number of concurrent copy operations.</span></span> <span data-ttu-id="3e136-293">根據預設，AzCopy 會啟動特定數目的並行作業 tooincrease hello 資料傳輸輸送量。</span><span class="sxs-lookup"><span data-stu-id="3e136-293">By default, AzCopy starts a certain number of concurrent operations tooincrease hello data transfer throughput.</span></span> <span data-ttu-id="3e136-294">資料表作業，hello 並行作業的數目會等於 toohello 您擁有的處理器數目。</span><span class="sxs-lookup"><span data-stu-id="3e136-294">For Table operations, hello number of concurrent operations is equal toohello number of processors you have.</span></span> <span data-ttu-id="3e136-295">為 Blob 和檔案作業中，並行作業的 hello 數目等於的處理器您有 8 次 hello 數目。</span><span class="sxs-lookup"><span data-stu-id="3e136-295">For Blob and File operations, hello number of concurrent operations is equal 8 times hello number of processors you have.</span></span> <span data-ttu-id="3e136-296">如果您正在執行 AzCopy 透過低頻寬網路，您可以指定較低的數字，因資源競爭 /NC tooavoid 失敗。</span><span class="sxs-lookup"><span data-stu-id="3e136-296">If you are running AzCopy across a low-bandwidth network, you can specify a lower number for /NC tooavoid failure caused by resource competition.</span></span>

### <a name="run-azcopy-against-azure-storage-emulator"></a><span data-ttu-id="3e136-297">針對 Azure 儲存體模擬器執行 AzCopy</span><span class="sxs-lookup"><span data-stu-id="3e136-297">Run AzCopy against Azure Storage Emulator</span></span>
<span data-ttu-id="3e136-298">您可以針對 hello 執行 AzCopy [Azure 儲存體模擬器](storage-use-emulator.md)的 Blob:</span><span class="sxs-lookup"><span data-stu-id="3e136-298">You can run AzCopy against hello [Azure Storage Emulator](storage-use-emulator.md) for Blobs:</span></span>

```azcopy
AzCopy /Source:https://127.0.0.1:10000/myaccount/mycontainer/ /Dest:C:\myfolder /SourceKey:key /SourceType:Blob /S
```

<span data-ttu-id="3e136-299">以及針對資料表來執行：</span><span class="sxs-lookup"><span data-stu-id="3e136-299">and Tables:</span></span>

```azcopy
AzCopy /Source:https://127.0.0.1:10002/myaccount/mytable/ /Dest:C:\myfolder /SourceKey:key /SourceType:Table
```

## <a name="azcopy-parameters"></a><span data-ttu-id="3e136-300">AzCopy 參數</span><span class="sxs-lookup"><span data-stu-id="3e136-300">AzCopy Parameters</span></span>
<span data-ttu-id="3e136-301">以下內容說明 AzCopy 的參數。</span><span class="sxs-lookup"><span data-stu-id="3e136-301">Parameters for AzCopy are described below.</span></span> <span data-ttu-id="3e136-302">您也可以輸入 hello 的說明使用 AzCopy hello 命令列中的下列命令：</span><span class="sxs-lookup"><span data-stu-id="3e136-302">You can also type one of hello following commands from hello command line for help in using AzCopy:</span></span>

* <span data-ttu-id="3e136-303">如需 AzCopy 的詳細命令列說明： `AzCopy /?`</span><span class="sxs-lookup"><span data-stu-id="3e136-303">For detailed command-line help for AzCopy: `AzCopy /?`</span></span>
* <span data-ttu-id="3e136-304">如需任何 AzCopy 參數的詳細說明： `AzCopy /?:SourceKey`</span><span class="sxs-lookup"><span data-stu-id="3e136-304">For detailed help with any AzCopy parameter: `AzCopy /?:SourceKey`</span></span>
* <span data-ttu-id="3e136-305">如需命令列範例： `AzCopy /?:Samples`</span><span class="sxs-lookup"><span data-stu-id="3e136-305">For command-line examples: `AzCopy /?:Samples`</span></span>

### <a name="sourcesource"></a><span data-ttu-id="3e136-306">/Source:"source"</span><span class="sxs-lookup"><span data-stu-id="3e136-306">/Source:"source"</span></span>
<span data-ttu-id="3e136-307">指定從哪個 toocopy hello 來源資料。</span><span class="sxs-lookup"><span data-stu-id="3e136-307">Specifies hello source data from which toocopy.</span></span> <span data-ttu-id="3e136-308">hello 來源可以是檔案系統目錄、 blob 容器、 blob 的虛擬目錄、 儲存體檔案共用、 儲存檔案目錄或 Azure 資料表。</span><span class="sxs-lookup"><span data-stu-id="3e136-308">hello source can be a file system directory, a blob container, a blob virtual directory, a storage file share, a storage file directory, or an Azure table.</span></span>

<span data-ttu-id="3e136-309">**適用於：** Blob、檔案、資料表</span><span class="sxs-lookup"><span data-stu-id="3e136-309">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="destdestination"></a><span data-ttu-id="3e136-310">/Dest:"destination"</span><span class="sxs-lookup"><span data-stu-id="3e136-310">/Dest:"destination"</span></span>
<span data-ttu-id="3e136-311">指定要 hello 目的地 toocopy。</span><span class="sxs-lookup"><span data-stu-id="3e136-311">Specifies hello destination toocopy to.</span></span> <span data-ttu-id="3e136-312">hello 目的地可以是檔案系統目錄、 blob 容器、 blob 的虛擬目錄、 儲存體檔案共用、 儲存檔案目錄或 Azure 資料表。</span><span class="sxs-lookup"><span data-stu-id="3e136-312">hello destination can be a file system directory, a blob container, a blob virtual directory, a storage file share, a storage file directory, or an Azure table.</span></span>

<span data-ttu-id="3e136-313">**適用於：** Blob、檔案、資料表</span><span class="sxs-lookup"><span data-stu-id="3e136-313">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="patternfile-pattern"></a><span data-ttu-id="3e136-314">/Pattern:"file-pattern"</span><span class="sxs-lookup"><span data-stu-id="3e136-314">/Pattern:"file-pattern"</span></span>
<span data-ttu-id="3e136-315">指定指出哪些檔案 toocopy 檔案模式。</span><span class="sxs-lookup"><span data-stu-id="3e136-315">Specifies a file pattern that indicates which files toocopy.</span></span> <span data-ttu-id="3e136-316">hello /Pattern 參數 hello 行為取決於 hello 來源資料的 hello 位置和 hello 與否 hello 遞迴模式選項。</span><span class="sxs-lookup"><span data-stu-id="3e136-316">hello behavior of hello /Pattern parameter is determined by hello location of hello source data, and hello presence of hello recursive mode option.</span></span> <span data-ttu-id="3e136-317">遞迴模式可透過選項 /S 來指定。</span><span class="sxs-lookup"><span data-stu-id="3e136-317">Recursive mode is specified via option /S.</span></span>

<span data-ttu-id="3e136-318">如果 hello 指定的來源是在 hello 檔案系統中，目錄，則標準萬用字元是作用中，並提供的 hello 檔案模式比對 hello 目錄內的檔案。</span><span class="sxs-lookup"><span data-stu-id="3e136-318">If hello specified source is a directory in hello file system, then standard wildcards are in effect, and hello file pattern provided is matched against files within hello directory.</span></span> <span data-ttu-id="3e136-319">如果選項指定 /S，然後 AzCopy 也會比對 hello hello 目錄下的任何子資料夾中的所有檔案對指定的模式。</span><span class="sxs-lookup"><span data-stu-id="3e136-319">If option /S is specified, then AzCopy also matches hello specified pattern against all files in any subfolders beneath hello directory.</span></span>

<span data-ttu-id="3e136-320">如果 hello 指定的來源 blob 容器或虛擬目錄，然後不會套用萬用字元。</span><span class="sxs-lookup"><span data-stu-id="3e136-320">If hello specified source is a blob container or virtual directory, then wildcards are not applied.</span></span> <span data-ttu-id="3e136-321">如果選項指定 /S，然後 AzCopy 會當做 blob 前置詞解譯 hello 指定的檔案模式。</span><span class="sxs-lookup"><span data-stu-id="3e136-321">If option /S is specified, then AzCopy interprets hello specified file pattern as a blob prefix.</span></span> <span data-ttu-id="3e136-322">如果選項未指定 /S，然後 AzCopy 符合 hello 檔案模式比對確切 blob 名稱。</span><span class="sxs-lookup"><span data-stu-id="3e136-322">If option /S is not specified, then AzCopy matches hello file pattern against exact blob names.</span></span>

<span data-ttu-id="3e136-323">如果來源是 Azure 的檔案共用，則您必須指定 hello 確切的檔名 (例如 abc.txt)，指定 hello toocopy 單一檔案，或指定選項 /S toocopy hello 共用以遞迴方式中的所有檔案。</span><span class="sxs-lookup"><span data-stu-id="3e136-323">If hello specified source is an Azure file share, then you must either specify hello exact file name, (e.g. abc.txt) toocopy a single file, or specify option /S toocopy all files in hello share recursively.</span></span> <span data-ttu-id="3e136-324">正在嘗試 toospecify 這兩個檔案模式和選項 /S 一起會導致錯誤。</span><span class="sxs-lookup"><span data-stu-id="3e136-324">Attempting toospecify both a file pattern and option /S together results in an error.</span></span>

<span data-ttu-id="3e136-325">AzCopy 會使用區分大小寫比對時 hello /Source blob 容器或 blob 的虛擬目錄，而且會使用不區分大小寫比對所有 hello 其他情況。</span><span class="sxs-lookup"><span data-stu-id="3e136-325">AzCopy uses case-sensitive matching when hello /Source is a blob container or blob virtual directory, and uses case-insensitive matching in all hello other cases.</span></span>

<span data-ttu-id="3e136-326">hello 不指定任何檔案模式時使用的預設檔案模式是*。*</span><span class="sxs-lookup"><span data-stu-id="3e136-326">hello default file pattern used when no file pattern is specified is *.*</span></span> <span data-ttu-id="3e136-327">，針對「Azure 儲存體」位置，則是使用空白首碼。</span><span class="sxs-lookup"><span data-stu-id="3e136-327">for a file system location or an empty prefix for an Azure Storage location.</span></span> <span data-ttu-id="3e136-328">不支援指定多個檔案模式。</span><span class="sxs-lookup"><span data-stu-id="3e136-328">Specifying multiple file patterns is not supported.</span></span>

<span data-ttu-id="3e136-329">**適用於：** Blob、檔案</span><span class="sxs-lookup"><span data-stu-id="3e136-329">**Applicable to:** Blobs, Files</span></span>

### <a name="destkeystorage-key"></a><span data-ttu-id="3e136-330">/DestKey:"storage-key"</span><span class="sxs-lookup"><span data-stu-id="3e136-330">/DestKey:"storage-key"</span></span>
<span data-ttu-id="3e136-331">指定 hello hello 目的地資源的儲存體帳戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="3e136-331">Specifies hello storage account key for hello destination resource.</span></span>

<span data-ttu-id="3e136-332">**適用於：** Blob、檔案、資料表</span><span class="sxs-lookup"><span data-stu-id="3e136-332">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="destsassas-token"></a><span data-ttu-id="3e136-333">/DestSAS:"sas-token"</span><span class="sxs-lookup"><span data-stu-id="3e136-333">/DestSAS:"sas-token"</span></span>
<span data-ttu-id="3e136-334">指定共用存取簽章 (SAS) hello 目的讀取及寫入權限 （如果適用）。</span><span class="sxs-lookup"><span data-stu-id="3e136-334">Specifies a Shared Access Signature (SAS) with READ and WRITE permissions for hello destination (if applicable).</span></span> <span data-ttu-id="3e136-335">範圍陳述式 hello SAS 雙引號括住，因為它可能包含命令列的特殊字元。</span><span class="sxs-lookup"><span data-stu-id="3e136-335">Surround hello SAS with double quotes, as it may contains special command-line characters.</span></span>

<span data-ttu-id="3e136-336">如果 hello 目的地資源是 blob 容器、 檔案共用或資料表，您可以指定這個選項後面接著 hello SAS 權杖，或您可以指定 hello SAS 為 hello 目的地 blob 容器、 檔案共用或資料表的 URI，如果沒有這個選項的一部分。</span><span class="sxs-lookup"><span data-stu-id="3e136-336">If hello destination resource is a blob container, file share or table, you can either specify this option followed by hello SAS token, or you can specify hello SAS as part of hello destination blob container, file share or table's URI, without this option.</span></span>

<span data-ttu-id="3e136-337">如果 hello 來源和目的地是這兩個 blob，則 hello 目的地 blob 都必須在 hello 相同 hello 來源 blob 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="3e136-337">If hello source and destination are both blobs, then hello destination blob must reside within hello same storage account as hello source blob.</span></span>

<span data-ttu-id="3e136-338">**適用於：** Blob、檔案、資料表</span><span class="sxs-lookup"><span data-stu-id="3e136-338">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="sourcekeystorage-key"></a><span data-ttu-id="3e136-339">/SourceKey:"storage-key"</span><span class="sxs-lookup"><span data-stu-id="3e136-339">/SourceKey:"storage-key"</span></span>
<span data-ttu-id="3e136-340">指定 hello hello 來源資源的儲存體帳戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="3e136-340">Specifies hello storage account key for hello source resource.</span></span>

<span data-ttu-id="3e136-341">**適用於：** Blob、檔案、資料表</span><span class="sxs-lookup"><span data-stu-id="3e136-341">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="sourcesassas-token"></a><span data-ttu-id="3e136-342">/SourceSAS:"sas-token"</span><span class="sxs-lookup"><span data-stu-id="3e136-342">/SourceSAS:"sas-token"</span></span>
<span data-ttu-id="3e136-343">指定共用存取簽章 hello 來源的讀取和清單權限 （如果適用）。</span><span class="sxs-lookup"><span data-stu-id="3e136-343">Specifies a Shared Access Signature with READ and LIST permissions for hello source (if applicable).</span></span> <span data-ttu-id="3e136-344">範圍陳述式 hello SAS 雙引號括住，因為它可能包含命令列的特殊字元。</span><span class="sxs-lookup"><span data-stu-id="3e136-344">Surround hello SAS with double quotes, as it may contains special command-line characters.</span></span>

<span data-ttu-id="3e136-345">如果 hello 來源資源是 blob 容器，並提供索引鍵都 SAS，透過匿名存取讀取 hello blob 容器。</span><span class="sxs-lookup"><span data-stu-id="3e136-345">If hello source resource is a blob container, and neither a key nor a SAS is provided, then hello blob container is read via anonymous access.</span></span>

<span data-ttu-id="3e136-346">如果 hello 來源為檔案共用或資料表，必須提供的索引鍵或 SAS。</span><span class="sxs-lookup"><span data-stu-id="3e136-346">If hello source is a file share or table, a key or a SAS must be provided.</span></span>

<span data-ttu-id="3e136-347">**適用於：** Blob、檔案、資料表</span><span class="sxs-lookup"><span data-stu-id="3e136-347">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="s"></a><span data-ttu-id="3e136-348">/S</span><span class="sxs-lookup"><span data-stu-id="3e136-348">/S</span></span>
<span data-ttu-id="3e136-349">指定複製作業的遞迴模式。</span><span class="sxs-lookup"><span data-stu-id="3e136-349">Specifies recursive mode for copy operations.</span></span> <span data-ttu-id="3e136-350">在遞迴模式中，AzCopy 會將複製所有的 blob 或符合 hello 指定的檔案模式，包括子資料夾中的檔案。</span><span class="sxs-lookup"><span data-stu-id="3e136-350">In recursive mode, AzCopy copies all blobs or files that match hello specified file pattern, including those in subfolders.</span></span>

<span data-ttu-id="3e136-351">**適用於：** Blob、檔案</span><span class="sxs-lookup"><span data-stu-id="3e136-351">**Applicable to:** Blobs, Files</span></span>

### <a name="blobtypeblock--page--append"></a><span data-ttu-id="3e136-352">/BlobType:"block" | "page" | "append"</span><span class="sxs-lookup"><span data-stu-id="3e136-352">/BlobType:"block" | "page" | "append"</span></span>
<span data-ttu-id="3e136-353">指定 hello 目的地 blob 是區塊 blob、 分頁 blob 或附加 blob。</span><span class="sxs-lookup"><span data-stu-id="3e136-353">Specifies whether hello destination blob is a block blob, a page blob, or an append blob.</span></span> <span data-ttu-id="3e136-354">此選項僅在上傳 Blob 時才適用。</span><span class="sxs-lookup"><span data-stu-id="3e136-354">This option is applicable only when you are uploading a blob.</span></span> <span data-ttu-id="3e136-355">否則會產生錯誤。</span><span class="sxs-lookup"><span data-stu-id="3e136-355">Otherwise, an error is generated.</span></span> <span data-ttu-id="3e136-356">如果 hello 目的地是 blob，且未指定此選項，根據預設，AzCopy 會建立區塊 blob。</span><span class="sxs-lookup"><span data-stu-id="3e136-356">If hello destination is a blob and this option is not specified, by default, AzCopy creates a block blob.</span></span>

<span data-ttu-id="3e136-357">**適用於：** Blob</span><span class="sxs-lookup"><span data-stu-id="3e136-357">**Applicable to:** Blobs</span></span>

### <a name="checkmd5"></a><span data-ttu-id="3e136-358">/CheckMD5</span><span class="sxs-lookup"><span data-stu-id="3e136-358">/CheckMD5</span></span>
<span data-ttu-id="3e136-359">計算下載資料的 MD5 雜湊，並確認 hello MD5 雜湊儲存在 hello blob，或檔案的內容 MD5 屬性符合 hello 計算雜湊。</span><span class="sxs-lookup"><span data-stu-id="3e136-359">Calculates an MD5 hash for downloaded data and verifies that hello MD5 hash stored in hello blob or file's Content-MD5 property matches hello calculated hash.</span></span> <span data-ttu-id="3e136-360">hello MD5 核取是預設關閉，所以下載資料時，您必須指定這個選項 tooperform hello MD5 核取。</span><span class="sxs-lookup"><span data-stu-id="3e136-360">hello MD5 check is turned off by default, so you must specify this option tooperform hello MD5 check when downloading data.</span></span>

<span data-ttu-id="3e136-361">請注意 Azure 儲存體，並不保證該 hello hello blob 儲存的 MD5 雜湊或是最新的檔案。</span><span class="sxs-lookup"><span data-stu-id="3e136-361">Note that Azure Storage doesn't guarantee that hello MD5 hash stored for hello blob or file is up-to-date.</span></span> <span data-ttu-id="3e136-362">每當修改 hello blob 或檔案，它就會為用戶端的責任 tooupdate hello MD5。</span><span class="sxs-lookup"><span data-stu-id="3e136-362">It is client's responsibility tooupdate hello MD5 whenever hello blob or file is modified.</span></span>

<span data-ttu-id="3e136-363">AzCopy 永遠設定 hello content-md5 屬性的 Azure blob 或檔案之後將它上傳 toohello 服務。</span><span class="sxs-lookup"><span data-stu-id="3e136-363">AzCopy always sets hello Content-MD5 property for an Azure blob or file after uploading it toohello service.</span></span>  

<span data-ttu-id="3e136-364">**適用於：** Blob、檔案</span><span class="sxs-lookup"><span data-stu-id="3e136-364">**Applicable to:** Blobs, Files</span></span>

### <a name="snapshot"></a><span data-ttu-id="3e136-365">/Snapshot</span><span class="sxs-lookup"><span data-stu-id="3e136-365">/Snapshot</span></span>
<span data-ttu-id="3e136-366">指出是否 tootransfer 快照集。</span><span class="sxs-lookup"><span data-stu-id="3e136-366">Indicates whether tootransfer snapshots.</span></span> <span data-ttu-id="3e136-367">Hello 來源 blob 時，此選項才有效。</span><span class="sxs-lookup"><span data-stu-id="3e136-367">This option is only valid when hello source is a blob.</span></span>

<span data-ttu-id="3e136-368">hello 傳送的 blob 快照集在重新命名此格式：.extension blob 名稱 （快照集時間）</span><span class="sxs-lookup"><span data-stu-id="3e136-368">hello transferred blob snapshots are renamed in this format: blob-name (snapshot-time).extension</span></span>

<span data-ttu-id="3e136-369">依預設，不會複製快照。</span><span class="sxs-lookup"><span data-stu-id="3e136-369">By default, snapshots are not copied.</span></span>

<span data-ttu-id="3e136-370">**適用於：** Blob</span><span class="sxs-lookup"><span data-stu-id="3e136-370">**Applicable to:** Blobs</span></span>

### <a name="vverbose-log-file"></a><span data-ttu-id="3e136-371">/V:[verbose-log-file]</span><span class="sxs-lookup"><span data-stu-id="3e136-371">/V:[verbose-log-file]</span></span>
<span data-ttu-id="3e136-372">將詳細資訊狀態訊息輸出至記錄檔。</span><span class="sxs-lookup"><span data-stu-id="3e136-372">Outputs verbose status messages into a log file.</span></span>

<span data-ttu-id="3e136-373">根據預設，名為 hello 詳細的記錄檔中的 AzCopyVerbose.log `%LocalAppData%\Microsoft\Azure\AzCopy`。</span><span class="sxs-lookup"><span data-stu-id="3e136-373">By default, hello verbose log file is named AzCopyVerbose.log in `%LocalAppData%\Microsoft\Azure\AzCopy`.</span></span> <span data-ttu-id="3e136-374">如果您指定這個選項是現有的檔案位置，hello 詳細資訊記錄檔會是附加的 toothat 檔案。</span><span class="sxs-lookup"><span data-stu-id="3e136-374">If you specify an existing file location for this option, hello verbose log is appended toothat file.</span></span>  

<span data-ttu-id="3e136-375">**適用於：** Blob、檔案、資料表</span><span class="sxs-lookup"><span data-stu-id="3e136-375">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="zjournal-file-folder"></a><span data-ttu-id="3e136-376">/Z:[journal-file-folder]</span><span class="sxs-lookup"><span data-stu-id="3e136-376">/Z:[journal-file-folder]</span></span>
<span data-ttu-id="3e136-377">指定用於繼續作業的日誌檔案資料夾。</span><span class="sxs-lookup"><span data-stu-id="3e136-377">Specifies a journal file folder for resuming an operation.</span></span>

<span data-ttu-id="3e136-378">如果作業遭到中斷，AzCopy 絕對支援繼續作業。</span><span class="sxs-lookup"><span data-stu-id="3e136-378">AzCopy always supports resuming if an operation has been interrupted.</span></span>

<span data-ttu-id="3e136-379">如果未指定此選項，或指定不包含資料夾路徑，AzCopy 會建立 hello 日誌檔 hello 預設位置為 %localappdata%\microsoft\azure\azcopy 中。</span><span class="sxs-lookup"><span data-stu-id="3e136-379">If this option is not specified, or it is specified without a folder path, then AzCopy creates hello journal file in hello default location, which is %LocalAppData%\Microsoft\Azure\AzCopy.</span></span>

<span data-ttu-id="3e136-380">每次您提交命令 tooAzCopy，它會檢查日誌檔是否存在於 hello 預設資料夾，或是否有您指定透過這個選項的資料夾中。</span><span class="sxs-lookup"><span data-stu-id="3e136-380">Each time you issue a command tooAzCopy, it checks whether a journal file exists in hello default folder, or whether it exists in a folder that you specified via this option.</span></span> <span data-ttu-id="3e136-381">如果在任一處，hello 日誌檔不存在，AzCopy hello 作業視為新，並產生新的日誌檔。</span><span class="sxs-lookup"><span data-stu-id="3e136-381">If hello journal file does not exist in either place, AzCopy treats hello operation as new and generates a new journal file.</span></span>

<span data-ttu-id="3e136-382">如果 hello 日誌檔案存在，AzCopy 會檢查您輸入的 hello 命令列是否符合 hello hello 筆記本檔案中的命令列。</span><span class="sxs-lookup"><span data-stu-id="3e136-382">If hello journal file does exist, AzCopy checks whether hello command line that you input matches hello command line in hello journal file.</span></span> <span data-ttu-id="3e136-383">如果兩個命令列 hello 相符，AzCopy 會繼續 hello 未完成作業。</span><span class="sxs-lookup"><span data-stu-id="3e136-383">If hello two command lines match, AzCopy resumes hello incomplete operation.</span></span> <span data-ttu-id="3e136-384">如果不相符，則提示的 tooeither 覆寫 hello 日誌檔案 toostart，新增作業或 toocancel hello 目前的作業。</span><span class="sxs-lookup"><span data-stu-id="3e136-384">If they do not match, you are prompted tooeither overwrite hello journal file toostart a new operation, or toocancel hello current operation.</span></span>

<span data-ttu-id="3e136-385">hello 作業順利完成時，會刪除 hello 日誌檔案。</span><span class="sxs-lookup"><span data-stu-id="3e136-385">hello journal file is deleted upon successful completion of hello operation.</span></span>

<span data-ttu-id="3e136-386">請注意，不支援根據舊版的 AzCopy 所建立的日誌檔案繼續作業。</span><span class="sxs-lookup"><span data-stu-id="3e136-386">Note that resuming an operation from a journal file created by a previous version of AzCopy is not supported.</span></span>

<span data-ttu-id="3e136-387">**適用於：** Blob、檔案、資料表</span><span class="sxs-lookup"><span data-stu-id="3e136-387">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="parameter-file"></a><span data-ttu-id="3e136-388">/@:"parameter-file"</span><span class="sxs-lookup"><span data-stu-id="3e136-388">/@:"parameter-file"</span></span>
<span data-ttu-id="3e136-389">指定包含參數的檔案。</span><span class="sxs-lookup"><span data-stu-id="3e136-389">Specifies a file that contains parameters.</span></span> <span data-ttu-id="3e136-390">AzCopy 處理程序 hello hello 檔案中的參數，就如同 hello 命令列上指定。</span><span class="sxs-lookup"><span data-stu-id="3e136-390">AzCopy processes hello parameters in hello file just as if they had been specified on hello command line.</span></span>

<span data-ttu-id="3e136-391">在回應檔案中，您可以在單行中指定多個參數，或每一行各自指定一個參數。</span><span class="sxs-lookup"><span data-stu-id="3e136-391">In a response file, you can either specify multiple parameters on a single line, or specify each parameter on its own line.</span></span> <span data-ttu-id="3e136-392">請注意，各個參數無法橫跨多行。</span><span class="sxs-lookup"><span data-stu-id="3e136-392">Note that an individual parameter cannot span multiple lines.</span></span>

<span data-ttu-id="3e136-393">回應檔案可以包含註解以 hello # 符號為開頭的行。</span><span class="sxs-lookup"><span data-stu-id="3e136-393">Response files can include comments lines that begin with hello # symbol.</span></span>

<span data-ttu-id="3e136-394">您可以指定多個回應檔案。</span><span class="sxs-lookup"><span data-stu-id="3e136-394">You can specify multiple response files.</span></span> <span data-ttu-id="3e136-395">不過，請記住 AzCopy 不支援巢狀回應檔案。</span><span class="sxs-lookup"><span data-stu-id="3e136-395">However, note that AzCopy does not support nested response files.</span></span>

<span data-ttu-id="3e136-396">**適用於：** Blob、檔案、資料表</span><span class="sxs-lookup"><span data-stu-id="3e136-396">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="y"></a><span data-ttu-id="3e136-397">/Y</span><span class="sxs-lookup"><span data-stu-id="3e136-397">/Y</span></span>
<span data-ttu-id="3e136-398">隱藏所有 AzCopy 確認提示。</span><span class="sxs-lookup"><span data-stu-id="3e136-398">Suppresses all AzCopy confirmation prompts.</span></span>

<span data-ttu-id="3e136-399">**適用於：** Blob、檔案、資料表</span><span class="sxs-lookup"><span data-stu-id="3e136-399">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="l"></a><span data-ttu-id="3e136-400">/L</span><span class="sxs-lookup"><span data-stu-id="3e136-400">/L</span></span>
<span data-ttu-id="3e136-401">僅指定清單作業，不會複製資料。</span><span class="sxs-lookup"><span data-stu-id="3e136-401">Specifies a listing operation only; no data is copied.</span></span>

<span data-ttu-id="3e136-402">AzCopy 會解譯 hello 使用這個選項做執行 hello 命令列未執行此動作的模擬選項 /L 和計數會複製物件數目，您可以指定在相同時間 toocheck 哪些物件會在 hello 詳細資訊記錄檔中複製的 hello 選項 /V。</span><span class="sxs-lookup"><span data-stu-id="3e136-402">AzCopy interprets hello using of this option as a simulation for running hello command line without this option /L and counts how many objects are copied, you can specify option /V at hello same time toocheck which objects are copied in hello verbose log.</span></span>

<span data-ttu-id="3e136-403">此選項 hello 行為也取決於 hello hello 來源資料的位置和 hello 遞迴模式選項 /S 和檔案模式選項 /Pattern hello 存在。</span><span class="sxs-lookup"><span data-stu-id="3e136-403">hello behavior of this option is also determined by hello location of hello source data and hello presence of hello recursive mode option /S and file pattern option /Pattern.</span></span>

<span data-ttu-id="3e136-404">使用此選項時，AzCopy 會需要此來源位置的清單和讀取權限。</span><span class="sxs-lookup"><span data-stu-id="3e136-404">AzCopy requires LIST and READ permission of this source location when using this option.</span></span>

<span data-ttu-id="3e136-405">**適用於：** Blob、檔案</span><span class="sxs-lookup"><span data-stu-id="3e136-405">**Applicable to:** Blobs, Files</span></span>

### <a name="mt"></a><span data-ttu-id="3e136-406">/MT</span><span class="sxs-lookup"><span data-stu-id="3e136-406">/MT</span></span>
<span data-ttu-id="3e136-407">設定 toobe 相同為 hello 來源 blob 或檔案的 hello 的 hello 下載的檔案的上次修改的時間。</span><span class="sxs-lookup"><span data-stu-id="3e136-407">Sets hello downloaded file's last-modified time toobe hello same as hello source blob or file's.</span></span>

<span data-ttu-id="3e136-408">**適用於：** Blob、檔案</span><span class="sxs-lookup"><span data-stu-id="3e136-408">**Applicable to:** Blobs, Files</span></span>

### <a name="xn"></a><span data-ttu-id="3e136-409">/XN</span><span class="sxs-lookup"><span data-stu-id="3e136-409">/XN</span></span>
<span data-ttu-id="3e136-410">排除較新的來源資源。</span><span class="sxs-lookup"><span data-stu-id="3e136-410">Excludes a newer source resource.</span></span> <span data-ttu-id="3e136-411">hello 資源不會複製如果 hello hello 來源的上次修改的時間為 hello 相同或更新版本比目的地。</span><span class="sxs-lookup"><span data-stu-id="3e136-411">hello resource is not copied if hello last modified time of hello source is hello same or newer than destination.</span></span>

<span data-ttu-id="3e136-412">**適用於：** Blob、檔案</span><span class="sxs-lookup"><span data-stu-id="3e136-412">**Applicable to:** Blobs, Files</span></span>

### <a name="xo"></a><span data-ttu-id="3e136-413">/XO</span><span class="sxs-lookup"><span data-stu-id="3e136-413">/XO</span></span>
<span data-ttu-id="3e136-414">排除較舊的來源資源。</span><span class="sxs-lookup"><span data-stu-id="3e136-414">Excludes an older source resource.</span></span> <span data-ttu-id="3e136-415">hello 資源不會複製如果 hello hello 來源的上次修改的時間為 hello 相同或早於目的地。</span><span class="sxs-lookup"><span data-stu-id="3e136-415">hello resource is not copied if hello last modified time of hello source is hello same or older than destination.</span></span>

<span data-ttu-id="3e136-416">**適用於：** Blob、檔案</span><span class="sxs-lookup"><span data-stu-id="3e136-416">**Applicable to:** Blobs, Files</span></span>

### <a name="a"></a><span data-ttu-id="3e136-417">/A</span><span class="sxs-lookup"><span data-stu-id="3e136-417">/A</span></span>
<span data-ttu-id="3e136-418">上傳已設定的 hello 保存屬性的檔案。</span><span class="sxs-lookup"><span data-stu-id="3e136-418">Uploads only files that have hello Archive attribute set.</span></span>

<span data-ttu-id="3e136-419">**適用於：** Blob、檔案</span><span class="sxs-lookup"><span data-stu-id="3e136-419">**Applicable to:** Blobs, Files</span></span>

### <a name="iarashcnetoi"></a><span data-ttu-id="3e136-420">/IA:[RASHCNETOI]</span><span class="sxs-lookup"><span data-stu-id="3e136-420">/IA:[RASHCNETOI]</span></span>
<span data-ttu-id="3e136-421">上傳的檔案具有任何 hello 指定屬性集。</span><span class="sxs-lookup"><span data-stu-id="3e136-421">Uploads only files that have any of hello specified attributes set.</span></span>

<span data-ttu-id="3e136-422">可用屬性包括：</span><span class="sxs-lookup"><span data-stu-id="3e136-422">Available attributes include:</span></span>

* <span data-ttu-id="3e136-423">R = 唯讀檔案</span><span class="sxs-lookup"><span data-stu-id="3e136-423">R = Read-only files</span></span>
* <span data-ttu-id="3e136-424">A = 準備封存的檔案</span><span class="sxs-lookup"><span data-stu-id="3e136-424">A = Files ready for archiving</span></span>
* <span data-ttu-id="3e136-425">S = 系統檔案</span><span class="sxs-lookup"><span data-stu-id="3e136-425">S = System files</span></span>
* <span data-ttu-id="3e136-426">H = 隱藏檔案</span><span class="sxs-lookup"><span data-stu-id="3e136-426">H = Hidden files</span></span>
* <span data-ttu-id="3e136-427">C = 壓縮檔案</span><span class="sxs-lookup"><span data-stu-id="3e136-427">C = Compressed files</span></span>
* <span data-ttu-id="3e136-428">N = 正常檔案</span><span class="sxs-lookup"><span data-stu-id="3e136-428">N = Normal files</span></span>
* <span data-ttu-id="3e136-429">E = 加密檔案</span><span class="sxs-lookup"><span data-stu-id="3e136-429">E = Encrypted files</span></span>
* <span data-ttu-id="3e136-430">T = 暫存檔案</span><span class="sxs-lookup"><span data-stu-id="3e136-430">T = Temporary files</span></span>
* <span data-ttu-id="3e136-431">O = 離線檔案</span><span class="sxs-lookup"><span data-stu-id="3e136-431">O = Offline files</span></span>
* <span data-ttu-id="3e136-432">I = 未編製索引的檔案</span><span class="sxs-lookup"><span data-stu-id="3e136-432">I = Non-indexed files</span></span>

<span data-ttu-id="3e136-433">**適用於：** Blob、檔案</span><span class="sxs-lookup"><span data-stu-id="3e136-433">**Applicable to:** Blobs, Files</span></span>

### <a name="xarashcnetoi"></a><span data-ttu-id="3e136-434">/XA:[RASHCNETOI]</span><span class="sxs-lookup"><span data-stu-id="3e136-434">/XA:[RASHCNETOI]</span></span>
<span data-ttu-id="3e136-435">具有任何指定的 hello 檔案中排除屬性集。</span><span class="sxs-lookup"><span data-stu-id="3e136-435">Excludes files that have any of hello specified attributes set.</span></span>

<span data-ttu-id="3e136-436">可用屬性包括：</span><span class="sxs-lookup"><span data-stu-id="3e136-436">Available attributes include:</span></span>

* <span data-ttu-id="3e136-437">R = 唯讀檔案</span><span class="sxs-lookup"><span data-stu-id="3e136-437">R = Read-only files</span></span>
* <span data-ttu-id="3e136-438">A = 準備封存的檔案</span><span class="sxs-lookup"><span data-stu-id="3e136-438">A = Files ready for archiving</span></span>
* <span data-ttu-id="3e136-439">S = 系統檔案</span><span class="sxs-lookup"><span data-stu-id="3e136-439">S = System files</span></span>
* <span data-ttu-id="3e136-440">H = 隱藏檔案</span><span class="sxs-lookup"><span data-stu-id="3e136-440">H = Hidden files</span></span>
* <span data-ttu-id="3e136-441">C = 壓縮檔案</span><span class="sxs-lookup"><span data-stu-id="3e136-441">C = Compressed files</span></span>
* <span data-ttu-id="3e136-442">N = 正常檔案</span><span class="sxs-lookup"><span data-stu-id="3e136-442">N = Normal files</span></span>
* <span data-ttu-id="3e136-443">E = 加密檔案</span><span class="sxs-lookup"><span data-stu-id="3e136-443">E = Encrypted files</span></span>
* <span data-ttu-id="3e136-444">T = 暫存檔案</span><span class="sxs-lookup"><span data-stu-id="3e136-444">T = Temporary files</span></span>
* <span data-ttu-id="3e136-445">O = 離線檔案</span><span class="sxs-lookup"><span data-stu-id="3e136-445">O = Offline files</span></span>
* <span data-ttu-id="3e136-446">I = 未編製索引的檔案</span><span class="sxs-lookup"><span data-stu-id="3e136-446">I = Non-indexed files</span></span>

<span data-ttu-id="3e136-447">**適用於：** Blob、檔案</span><span class="sxs-lookup"><span data-stu-id="3e136-447">**Applicable to:** Blobs, Files</span></span>

### <a name="delimiterdelimiter"></a><span data-ttu-id="3e136-448">/Delimiter:"delimiter"</span><span class="sxs-lookup"><span data-stu-id="3e136-448">/Delimiter:"delimiter"</span></span>
<span data-ttu-id="3e136-449">指出 blob 名稱中使用 toodelimit 虛擬目錄的 hello 分隔符號字元。</span><span class="sxs-lookup"><span data-stu-id="3e136-449">Indicates hello delimiter character used toodelimit virtual directories in a blob name.</span></span>

<span data-ttu-id="3e136-450">根據預設，AzCopy 會使用 / 為 hello 分隔符號字元。</span><span class="sxs-lookup"><span data-stu-id="3e136-450">By default, AzCopy uses / as hello delimiter character.</span></span> <span data-ttu-id="3e136-451">不過，AzCopy 支援使用任何常見字元 (例如 @、# 或 %) 作為分隔符號。</span><span class="sxs-lookup"><span data-stu-id="3e136-451">However, AzCopy supports using any common character (such as @, #, or %) as a delimiter.</span></span> <span data-ttu-id="3e136-452">如果您需要 tooinclude 其中一個 hello 命令列上的特殊字元時，括住 hello 雙引號括住的檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="3e136-452">If you need tooinclude one of these special characters on hello command line, enclose hello file name with double quotes.</span></span>

<span data-ttu-id="3e136-453">此選項僅適用於下載 Blob。</span><span class="sxs-lookup"><span data-stu-id="3e136-453">This option is only applicable for downloading blobs.</span></span>

<span data-ttu-id="3e136-454">**適用於：** Blob</span><span class="sxs-lookup"><span data-stu-id="3e136-454">**Applicable to:** Blobs</span></span>

### <a name="ncnumber-of-concurrent-operations"></a><span data-ttu-id="3e136-455">/NC:"number-of-concurrent-operations"</span><span class="sxs-lookup"><span data-stu-id="3e136-455">/NC:"number-of-concurrent-operations"</span></span>
<span data-ttu-id="3e136-456">指定 hello 並行作業數。</span><span class="sxs-lookup"><span data-stu-id="3e136-456">Specifies hello number of concurrent operations.</span></span>

<span data-ttu-id="3e136-457">預設的 AzCopy 會啟動特定數目的並行作業 tooincrease hello 資料傳輸輸送量。</span><span class="sxs-lookup"><span data-stu-id="3e136-457">AzCopy by default starts a certain number of concurrent operations tooincrease hello data transfer throughput.</span></span> <span data-ttu-id="3e136-458">請注意，大量的並行作業，在低頻寬的環境中可能會淹沒 hello 網路連線避免 hello 作業完全完成。</span><span class="sxs-lookup"><span data-stu-id="3e136-458">Note that large number of concurrent operations in a low-bandwidth environment may overwhelm hello network connection and prevent hello operations from fully completing.</span></span> <span data-ttu-id="3e136-459">根據實際可用網路頻寬來節流處理並行作業。</span><span class="sxs-lookup"><span data-stu-id="3e136-459">Throttle concurrent operations based on actual available network bandwidth.</span></span>

<span data-ttu-id="3e136-460">hello 之並行作業的時間上限為 512。</span><span class="sxs-lookup"><span data-stu-id="3e136-460">hello upper limit for concurrent operations is 512.</span></span>

<span data-ttu-id="3e136-461">**適用於：** Blob、檔案、資料表</span><span class="sxs-lookup"><span data-stu-id="3e136-461">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="sourcetypeblob--table"></a><span data-ttu-id="3e136-462">/SourceType:"Blob" | "Table"</span><span class="sxs-lookup"><span data-stu-id="3e136-462">/SourceType:"Blob" | "Table"</span></span>
<span data-ttu-id="3e136-463">指定該 hello`source`資源是 blob hello 儲存體模擬器中執行的 hello 本機開發環境中可用。</span><span class="sxs-lookup"><span data-stu-id="3e136-463">Specifies that hello `source` resource is a blob available in hello local development environment, running in hello storage emulator.</span></span>

<span data-ttu-id="3e136-464">**適用於：** Blob、資料表</span><span class="sxs-lookup"><span data-stu-id="3e136-464">**Applicable to:** Blobs, Tables</span></span>

### <a name="desttypeblob--table"></a><span data-ttu-id="3e136-465">/DestType:"Blob" | "Table"</span><span class="sxs-lookup"><span data-stu-id="3e136-465">/DestType:"Blob" | "Table"</span></span>
<span data-ttu-id="3e136-466">指定該 hello`destination`資源是 blob hello 儲存體模擬器中執行的 hello 本機開發環境中可用。</span><span class="sxs-lookup"><span data-stu-id="3e136-466">Specifies that hello `destination` resource is a blob available in hello local development environment, running in hello storage emulator.</span></span>

<span data-ttu-id="3e136-467">**適用於：** Blob、資料表</span><span class="sxs-lookup"><span data-stu-id="3e136-467">**Applicable to:** Blobs, Tables</span></span>

### <a name="pkrskey1key2key3"></a><span data-ttu-id="3e136-468">/PKRS:"key1#key2#key3#..."</span><span class="sxs-lookup"><span data-stu-id="3e136-468">/PKRS:"key1#key2#key3#..."</span></span>
<span data-ttu-id="3e136-469">分割 hello 資料分割索引鍵範圍 tooenable 匯出資料表資料，以平行方式，會增加 hello hello 匯出作業的速度。</span><span class="sxs-lookup"><span data-stu-id="3e136-469">Splits hello partition key range tooenable exporting table data in parallel, which increases hello speed of hello export operation.</span></span>

<span data-ttu-id="3e136-470">如果未指定此選項，AzCopy 會使用單一執行緒 tooexport 資料表實體。</span><span class="sxs-lookup"><span data-stu-id="3e136-470">If this option is not specified, then AzCopy uses a single thread tooexport table entities.</span></span> <span data-ttu-id="3e136-471">例如，如果 hello 使用者指定 /PKRS:"aa #bb"，然後 AzCopy 會啟動三個並行作業。</span><span class="sxs-lookup"><span data-stu-id="3e136-471">For example, if hello user specifies /PKRS:"aa#bb", then AzCopy starts three concurrent operations.</span></span>

<span data-ttu-id="3e136-472">每個作業分別會匯出三個資料分割索引鍵範圍的其中一個，如下所示：</span><span class="sxs-lookup"><span data-stu-id="3e136-472">Each operation exports one of three partition key ranges, as shown below:</span></span>

  <span data-ttu-id="3e136-473">[first-partition-key, aa)</span><span class="sxs-lookup"><span data-stu-id="3e136-473">[first-partition-key, aa)</span></span>

  <span data-ttu-id="3e136-474">[aa, bb)</span><span class="sxs-lookup"><span data-stu-id="3e136-474">[aa, bb)</span></span>

  <span data-ttu-id="3e136-475">[bb, last-partition-key]</span><span class="sxs-lookup"><span data-stu-id="3e136-475">[bb, last-partition-key]</span></span>

<span data-ttu-id="3e136-476">**適用於：** 資料表</span><span class="sxs-lookup"><span data-stu-id="3e136-476">**Applicable to:** Tables</span></span>

### <a name="splitsizefile-size"></a><span data-ttu-id="3e136-477">/SplitSize:"file-size"</span><span class="sxs-lookup"><span data-stu-id="3e136-477">/SplitSize:"file-size"</span></span>
<span data-ttu-id="3e136-478">指定 hello 匯出的檔案分割大小 （mb），hello 允許的最小值為 32。</span><span class="sxs-lookup"><span data-stu-id="3e136-478">Specifies hello exported file split size in MB, hello minimal value allowed is 32.</span></span>

<span data-ttu-id="3e136-479">如果未指定此選項，AzCopy 會將匯出資料表資料 tooa 單一檔案。</span><span class="sxs-lookup"><span data-stu-id="3e136-479">If this option is not specified, AzCopy exports table data tooa single file.</span></span>

<span data-ttu-id="3e136-480">如果 hello 資料表資料是匯出的 tooa blob，而且 hello 匯出的檔案的大小到達的 blob 大小的 hello 200 GB 限制，然後 AzCopy 會分割 hello 匯出的檔案，即使沒有指定這個選項。</span><span class="sxs-lookup"><span data-stu-id="3e136-480">If hello table data is exported tooa blob, and hello exported file size reaches hello 200 GB limit for blob size, then AzCopy splits hello exported file, even if this option is not specified.</span></span>

<span data-ttu-id="3e136-481">**適用於：** 資料表</span><span class="sxs-lookup"><span data-stu-id="3e136-481">**Applicable to:** Tables</span></span>

### <a name="entityoperationinsertorskip--insertormerge--insertorreplace"></a><span data-ttu-id="3e136-482">/EntityOperation:"InsertOrSkip" | "InsertOrMerge" | "InsertOrReplace"</span><span class="sxs-lookup"><span data-stu-id="3e136-482">/EntityOperation:"InsertOrSkip" | "InsertOrMerge" | "InsertOrReplace"</span></span>
<span data-ttu-id="3e136-483">指定 hello 資料表資料匯入行為。</span><span class="sxs-lookup"><span data-stu-id="3e136-483">Specifies hello table data import behavior.</span></span>

* <span data-ttu-id="3e136-484">InsertOrSkip-跳過現有的實體，或如果不存在於 hello 資料表插入新實體。</span><span class="sxs-lookup"><span data-stu-id="3e136-484">InsertOrSkip - Skips an existing entity or inserts a new entity if it does not exist in hello table.</span></span>
* <span data-ttu-id="3e136-485">InsertOrMerge-合併現有的實體，或如果不存在於 hello 資料表插入新實體。</span><span class="sxs-lookup"><span data-stu-id="3e136-485">InsertOrMerge - Merges an existing entity or inserts a new entity if it does not exist in hello table.</span></span>
* <span data-ttu-id="3e136-486">InsertOrReplace-取代現有的實體，或如果不存在於 hello 資料表插入新實體。</span><span class="sxs-lookup"><span data-stu-id="3e136-486">InsertOrReplace - Replaces an existing entity or inserts a new entity if it does not exist in hello table.</span></span>

<span data-ttu-id="3e136-487">**適用於：** 資料表</span><span class="sxs-lookup"><span data-stu-id="3e136-487">**Applicable to:** Tables</span></span>

### <a name="manifestmanifest-file"></a><span data-ttu-id="3e136-488">/Manifest:"manifest-file"</span><span class="sxs-lookup"><span data-stu-id="3e136-488">/Manifest:"manifest-file"</span></span>
<span data-ttu-id="3e136-489">Hello 資料表匯出和匯入作業指定 hello 資訊清單檔案。</span><span class="sxs-lookup"><span data-stu-id="3e136-489">Specifies hello manifest file for hello table export and import operation.</span></span>

<span data-ttu-id="3e136-490">這個選項是選擇性的 hello 匯出作業期間，AzCopy 會產生資訊清單檔與預先定義的名稱，如果沒有指定這個選項。</span><span class="sxs-lookup"><span data-stu-id="3e136-490">This option is optional during hello export operation, AzCopy generates a manifest file with predefined name if this option is not specified.</span></span>

<span data-ttu-id="3e136-491">這是必要選項，以便將 hello 資料檔案的 hello 匯入作業期間。</span><span class="sxs-lookup"><span data-stu-id="3e136-491">This option is required during hello import operation for locating hello data files.</span></span>

<span data-ttu-id="3e136-492">**適用於：** 資料表</span><span class="sxs-lookup"><span data-stu-id="3e136-492">**Applicable to:** Tables</span></span>

### <a name="synccopy"></a><span data-ttu-id="3e136-493">/SyncCopy</span><span class="sxs-lookup"><span data-stu-id="3e136-493">/SyncCopy</span></span>
<span data-ttu-id="3e136-494">指出 toosynchronously 複製 blob 或兩個 Azure 儲存體端點之間的檔案。</span><span class="sxs-lookup"><span data-stu-id="3e136-494">Indicates whether toosynchronously copy blobs or files between two Azure Storage endpoints.</span></span>

<span data-ttu-id="3e136-495">AzCopy 依預設會使用伺服器端的非同步複本。</span><span class="sxs-lookup"><span data-stu-id="3e136-495">AzCopy by default uses server-side asynchronous copy.</span></span> <span data-ttu-id="3e136-496">指定此選項 tooperform 同步複製，這會下載 blob 或檔案 toolocal 記憶體並再將它們上傳 tooAzure 儲存體。</span><span class="sxs-lookup"><span data-stu-id="3e136-496">Specify this option tooperform a synchronous copy, which downloads blobs or files toolocal memory and then uploads them tooAzure Storage.</span></span>

<span data-ttu-id="3e136-497">複製 Blob 儲存體，或從 Blob 儲存體 tooFile 儲存體，反之亦然中檔案存放裝置中的檔案時，您可以使用此選項。</span><span class="sxs-lookup"><span data-stu-id="3e136-497">You can use this option when copying files within Blob storage, within File storage, or from Blob storage tooFile storage or vice versa.</span></span>

<span data-ttu-id="3e136-498">**適用於：** Blob、檔案</span><span class="sxs-lookup"><span data-stu-id="3e136-498">**Applicable to:** Blobs, Files</span></span>

### <a name="setcontenttypecontent-type"></a><span data-ttu-id="3e136-499">/SetContentType:"content-type"</span><span class="sxs-lookup"><span data-stu-id="3e136-499">/SetContentType:"content-type"</span></span>
<span data-ttu-id="3e136-500">指定目的地 blob 或檔案的 hello MIME 內容類型。</span><span class="sxs-lookup"><span data-stu-id="3e136-500">Specifies hello MIME content type for destination blobs or files.</span></span>

<span data-ttu-id="3e136-501">AzCopy 集 hello blob 的內容類型，或預設檔案資料流 tooapplication/八位元。</span><span class="sxs-lookup"><span data-stu-id="3e136-501">AzCopy sets hello content type for a blob or file tooapplication/octet-stream by default.</span></span> <span data-ttu-id="3e136-502">您可以藉由明確指定這個選項的值設定 hello 的所有 blob 或檔案的內容類型。</span><span class="sxs-lookup"><span data-stu-id="3e136-502">You can set hello content type for all blobs or files by explicitly specifying a value for this option.</span></span>

<span data-ttu-id="3e136-503">如果您指定這個選項沒有值，AzCopy 會設定每個 blob 或根據 tooits 副檔名的檔案的內容類型。</span><span class="sxs-lookup"><span data-stu-id="3e136-503">If you specify this option without a value, then AzCopy sets each blob or file's content type according tooits file extension.</span></span>

<span data-ttu-id="3e136-504">**適用於：** Blob、檔案</span><span class="sxs-lookup"><span data-stu-id="3e136-504">**Applicable to:** Blobs, Files</span></span>

### <a name="payloadformatjson--csv"></a><span data-ttu-id="3e136-505">/PayloadFormat:"JSON" | "CSV"</span><span class="sxs-lookup"><span data-stu-id="3e136-505">/PayloadFormat:"JSON" | "CSV"</span></span>
<span data-ttu-id="3e136-506">指定 hello hello 資料表匯出的資料檔格式。</span><span class="sxs-lookup"><span data-stu-id="3e136-506">Specifies hello format of hello table exported data file.</span></span>

<span data-ttu-id="3e136-507">如果未指定此選項，根據預設，AzCopy 會匯出 JSON 格式的資料表資料檔案。</span><span class="sxs-lookup"><span data-stu-id="3e136-507">If this option is not specified, by default AzCopy exports table data file in JSON format.</span></span>

<span data-ttu-id="3e136-508">**適用於：** 資料表</span><span class="sxs-lookup"><span data-stu-id="3e136-508">**Applicable to:** Tables</span></span>

## <a name="known-issues-and-best-practices"></a><span data-ttu-id="3e136-509">已知問題和最佳作法</span><span class="sxs-lookup"><span data-stu-id="3e136-509">Known Issues and Best Practices</span></span>
### <a name="limit-concurrent-writes-while-copying-data"></a><span data-ttu-id="3e136-510">限制複製資料時的並行寫入</span><span class="sxs-lookup"><span data-stu-id="3e136-510">Limit concurrent writes while copying data</span></span>
<span data-ttu-id="3e136-511">當您複製 blob 或利用 azcopy 進行的檔案時，請注意，另一個應用程式可能會修改 hello 資料將複製時。</span><span class="sxs-lookup"><span data-stu-id="3e136-511">When you copy blobs or files with AzCopy, keep in mind that another application may be modifying hello data while you are copying it.</span></span> <span data-ttu-id="3e136-512">可能的話，請確定不會被您要複製的 hello 資料修改 hello 複製作業期間。</span><span class="sxs-lookup"><span data-stu-id="3e136-512">If possible, ensure that hello data you are copying is not being modified during hello copy operation.</span></span> <span data-ttu-id="3e136-513">比方說，當複製與 Azure 虛擬機器相關聯的 VHD，請確定沒有其他應用程式目前正在撰寫 toohello VHD。</span><span class="sxs-lookup"><span data-stu-id="3e136-513">For example, when copying a VHD associated with an Azure virtual machine, make sure that no other applications are currently writing toohello VHD.</span></span> <span data-ttu-id="3e136-514">這是預設租用 hello 資源 toobe 複製的好方法 toodo。</span><span class="sxs-lookup"><span data-stu-id="3e136-514">A good way toodo this is by leasing hello resource toobe copied.</span></span> <span data-ttu-id="3e136-515">或者，您可以先建立 hello VHD 的快照集，然後複製 hello 快照集。</span><span class="sxs-lookup"><span data-stu-id="3e136-515">Alternately, you can create a snapshot of hello VHD first and then copy hello snapshot.</span></span>

<span data-ttu-id="3e136-516">如果您不能防止其他應用程式無法寫入 tooblobs 或檔案，它們會被複製，則請記住，hello 時間 hello 作業完成時，hello 複製的資源可能不再需要完整的同位檢查，但 hello 來源資源。</span><span class="sxs-lookup"><span data-stu-id="3e136-516">If you cannot prevent other applications from writing tooblobs or files while they are being copied, then keep in mind that by hello time hello job finishes, hello copied resources may no longer have full parity with hello source resources.</span></span>

### <a name="run-one-azcopy-instance-on-one-machine"></a><span data-ttu-id="3e136-517">在一部電腦上執行一個 AzCopy 執行個體。</span><span class="sxs-lookup"><span data-stu-id="3e136-517">Run one AzCopy instance on one machine.</span></span>
<span data-ttu-id="3e136-518">AzCopy 是設計的 toomaximize hello 善用您的電腦資源 tooaccelerate hello 資料傳輸，因此建議您只有一個 AzCopy 執行個體執行一個在電腦上，並指定 hello 選項`/NC`如果您需要更多的並行作業。</span><span class="sxs-lookup"><span data-stu-id="3e136-518">AzCopy is designed toomaximize hello utilization of your machine resource tooaccelerate hello data transfer, we recommend you run only one AzCopy instance on one machine, and specify hello option `/NC` if you need more concurrent operations.</span></span> <span data-ttu-id="3e136-519">如需詳細資訊，請輸入`AzCopy /?:NC`在 hello 命令列。</span><span class="sxs-lookup"><span data-stu-id="3e136-519">For more details, type `AzCopy /?:NC` at hello command line.</span></span>

### <a name="enable-fips-compliant-md5-algorithms-for-azcopy-when-you-use-fips-compliant-algorithms-for-encryption-hashing-and-signing"></a><span data-ttu-id="3e136-520">當您「使用 FIPS 相容演算法於加密、雜湊及簽章」時，請為 AzCopy 啟用 FIPS 相容的 MD5 演算法。</span><span class="sxs-lookup"><span data-stu-id="3e136-520">Enable FIPS compliant MD5 algorithms for AzCopy when you "Use FIPS compliant algorithms for encryption, hashing and signing".</span></span>
<span data-ttu-id="3e136-521">預設的 AzCopy.NET MD5 實作 toocalculate hello MD5 複製物件，但有一些需要 AzCopy tooenable FIPS 相容 MD5 設定的安全性需求。</span><span class="sxs-lookup"><span data-stu-id="3e136-521">AzCopy by default uses .NET MD5 implementation toocalculate hello MD5 when copying objects, but there are some security requirements that need AzCopy tooenable FIPS compliant MD5 setting.</span></span>

<span data-ttu-id="3e136-522">您可以建立具有 `AzureStorageUseV1MD5` 屬性的 app.config 檔案 `AzCopy.exe.config`，並將它放在 AzCopy.exe 旁邊。</span><span class="sxs-lookup"><span data-stu-id="3e136-522">You can create an app.config file `AzCopy.exe.config` with property `AzureStorageUseV1MD5` and put it aside with AzCopy.exe.</span></span>

    <?xml version="1.0" encoding="utf-8" ?>
    <configuration>
      <appSettings>
        <add key="AzureStorageUseV1MD5" value="false"/>
      </appSettings>
    </configuration>

<span data-ttu-id="3e136-523">屬性"AzureStorageUseV1MD5"• True-hello 預設值，AzCopy 會使用.NET MD5 實作。</span><span class="sxs-lookup"><span data-stu-id="3e136-523">For property "AzureStorageUseV1MD5" • True - hello default value, AzCopy uses .NET MD5 implementation.</span></span>
<span data-ttu-id="3e136-524">• False – AzCopy 會使用 FIPS 相容的 MD5 演算法。</span><span class="sxs-lookup"><span data-stu-id="3e136-524">• False – AzCopy uses FIPS compliant MD5 algorithm.</span></span>

<span data-ttu-id="3e136-525">請注意 Windows 電腦預設會停用 FIPS 相容演算法，可以在您執行的視窗中輸入 secpol.msc，並在 [安全性設定] -> [本機原則] -> [安全性選項] -> [系統密碼編譯: 使用 FIPS 相容演算法於加密、雜湊及簽章] 檢查此參數。</span><span class="sxs-lookup"><span data-stu-id="3e136-525">Note that FIPS compliant algorithms is disabled by default on your Windows machine, you can type secpol.msc in your Run window and check this switch at Security Setting->Local Policy->Security Options->System cryptography: Use FIPS compliant algorithms for encryption, hashing and signing.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3e136-526">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3e136-526">Next steps</span></span>
<span data-ttu-id="3e136-527">如需 Azure 儲存體和 AzCopy 的詳細資訊，請參閱下列資源的 hello:</span><span class="sxs-lookup"><span data-stu-id="3e136-527">For more information about Azure Storage and AzCopy, see hello following resources:</span></span>

### <a name="azure-storage-documentation"></a><span data-ttu-id="3e136-528">Azure 儲存體文件：</span><span class="sxs-lookup"><span data-stu-id="3e136-528">Azure Storage documentation:</span></span>
* [<span data-ttu-id="3e136-529">簡介 tooAzure 儲存體</span><span class="sxs-lookup"><span data-stu-id="3e136-529">Introduction tooAzure Storage</span></span>](../storage-introduction.md)
* [<span data-ttu-id="3e136-530">如何 toouse 與.NET 的 Blob 儲存體</span><span class="sxs-lookup"><span data-stu-id="3e136-530">How toouse Blob storage from .NET</span></span>](../blobs/storage-dotnet-how-to-use-blobs.md)
* [<span data-ttu-id="3e136-531">如何 toouse 檔案與.NET 的儲存體</span><span class="sxs-lookup"><span data-stu-id="3e136-531">How toouse File storage from .NET</span></span>](../storage-dotnet-how-to-use-files.md)
* [<span data-ttu-id="3e136-532">如何 toouse 資料表與.NET 的儲存體</span><span class="sxs-lookup"><span data-stu-id="3e136-532">How toouse Table storage from .NET</span></span>](../../cosmos-db/table-storage-how-to-use-dotnet.md)
* [<span data-ttu-id="3e136-533">Toocreate，如何管理或刪除儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="3e136-533">How toocreate, manage, or delete a storage account</span></span>](../storage-create-storage-account.md)
* [<span data-ttu-id="3e136-534">使用 AzCopy on Linux 傳送資料</span><span class="sxs-lookup"><span data-stu-id="3e136-534">Transfer data with AzCopy on Linux</span></span>](storage-use-azcopy-linux.md)

### <a name="azure-storage-blog-posts"></a><span data-ttu-id="3e136-535">Azure 儲存體部落格文章：</span><span class="sxs-lookup"><span data-stu-id="3e136-535">Azure Storage blog posts:</span></span>
* [<span data-ttu-id="3e136-536">Azure 儲存體資料移動文件庫預覽簡介</span><span class="sxs-lookup"><span data-stu-id="3e136-536">Introducing Azure Storage Data Movement Library Preview</span></span>](https://azure.microsoft.com/blog/introducing-azure-storage-data-movement-library-preview-2/)
* [<span data-ttu-id="3e136-537">AzCopy：簡介同步複製和自訂內容類型</span><span class="sxs-lookup"><span data-stu-id="3e136-537">AzCopy: Introducing synchronous copy and customized content type</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2015/01/13/azcopy-introducing-synchronous-copy-and-customized-content-type.aspx)
* [<span data-ttu-id="3e136-538">AzCopy: 宣布正式發行 AzCopy 3.0 和具有資料表和檔案支援的 AzCopy 4.0 預覽版本</span><span class="sxs-lookup"><span data-stu-id="3e136-538">AzCopy: Announcing General Availability of AzCopy 3.0 plus preview release of AzCopy 4.0 with Table and File support</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/10/29/azcopy-announcing-general-availability-of-azcopy-3-0-plus-preview-release-of-azcopy-4-0-with-table-and-file-support.aspx)
* [<span data-ttu-id="3e136-539">AzCopy: 針對大規模複製案例最佳化</span><span class="sxs-lookup"><span data-stu-id="3e136-539">AzCopy: Optimized for Large-Scale Copy Scenarios</span></span>](http://go.microsoft.com/fwlink/?LinkId=507682)
* [<span data-ttu-id="3e136-540">AzCopy: 支援讀取存取異地備援儲存體</span><span class="sxs-lookup"><span data-stu-id="3e136-540">AzCopy: Support for read-access geo-redundant storage</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/04/07/azcopy-support-for-read-access-geo-redundant-account.aspx)
* [<span data-ttu-id="3e136-541">AzCopy: 使用可重新啟動模式和 SAS 權杖傳輸資料</span><span class="sxs-lookup"><span data-stu-id="3e136-541">AzCopy: Transfer data with re-startable mode and SAS token</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/09/07/azcopy-transfer-data-with-re-startable-mode-and-sas-token.aspx)
* [<span data-ttu-id="3e136-542">AzCopy: 使用跨帳戶複製 Blob</span><span class="sxs-lookup"><span data-stu-id="3e136-542">AzCopy: Using cross-account Copy Blob</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/04/01/azcopy-using-cross-account-copy-blob.aspx)
* [<span data-ttu-id="3e136-543">AzCopy: 上傳/下載 Azure Blob 的檔案</span><span class="sxs-lookup"><span data-stu-id="3e136-543">AzCopy: Uploading/downloading files for Azure Blobs</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/12/03/azcopy-uploading-downloading-files-for-windows-azure-blobs.aspx)

