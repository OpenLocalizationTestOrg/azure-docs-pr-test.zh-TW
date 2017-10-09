---
title: "aaaSample 工作流程 tooprep 硬碟機的 Azure 匯入/匯出匯入作業-v1 |Microsoft 文件"
description: "Hello hello Azure 匯入/匯出服務中匯入工作準備磁碟機的完整程序的逐步解說，請參閱。"
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 6eb1b1b7-c69f-4365-b5ef-3cd5e05eb72a
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: eb77831a88c16c14838179a6432ddb06503067dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="sample-workflow-tooprepare-hard-drives-for-an-import-job"></a><span data-ttu-id="bc0f3-103">匯入工作的範例工作流程 tooprepare 硬碟機</span><span class="sxs-lookup"><span data-stu-id="bc0f3-103">Sample workflow tooprepare hard drives for an import job</span></span>
<span data-ttu-id="bc0f3-104">本主題會引導您完成 hello 完成程序來準備磁碟機匯入工作。</span><span class="sxs-lookup"><span data-stu-id="bc0f3-104">This topic walks you through hello complete process of preparing drives for an import job.</span></span>  
  
<span data-ttu-id="bc0f3-105">這個範例會匯入至 Window Azure 儲存體帳戶名稱為下列資料的 hello `mystorageaccount`:</span><span class="sxs-lookup"><span data-stu-id="bc0f3-105">This example imports hello following data into a Window Azure storage account named `mystorageaccount`:</span></span>  
  
|<span data-ttu-id="bc0f3-106">位置</span><span class="sxs-lookup"><span data-stu-id="bc0f3-106">Location</span></span>|<span data-ttu-id="bc0f3-107">說明</span><span class="sxs-lookup"><span data-stu-id="bc0f3-107">Description</span></span>|  
|--------------|-----------------|  
|<span data-ttu-id="bc0f3-108">H:\Video</span><span class="sxs-lookup"><span data-stu-id="bc0f3-108">H:\Video</span></span>|<span data-ttu-id="bc0f3-109">視訊集合，總共 5 TB。</span><span class="sxs-lookup"><span data-stu-id="bc0f3-109">A collection of videos, 5 TB in total.</span></span>|  
|<span data-ttu-id="bc0f3-110">H:\Photo</span><span class="sxs-lookup"><span data-stu-id="bc0f3-110">H:\Photo</span></span>|<span data-ttu-id="bc0f3-111">相片集合，總共 30 GB。</span><span class="sxs-lookup"><span data-stu-id="bc0f3-111">A collection of photos, 30 GB in total.</span></span>|  
|<span data-ttu-id="bc0f3-112">K:\Temp\FavoriteMovie.ISO</span><span class="sxs-lookup"><span data-stu-id="bc0f3-112">K:\Temp\FavoriteMovie.ISO</span></span>|<span data-ttu-id="bc0f3-113">藍光 (Blu-Ray™) 磁碟映像，25 GB。</span><span class="sxs-lookup"><span data-stu-id="bc0f3-113">A Blu-Ray™ disk image, 25 GB.</span></span>|  
|<span data-ttu-id="bc0f3-114">\\\bigshare\john\music</span><span class="sxs-lookup"><span data-stu-id="bc0f3-114">\\\bigshare\john\music</span></span>|<span data-ttu-id="bc0f3-115">網路共用上的音樂檔案集合，總共 10 GB。</span><span class="sxs-lookup"><span data-stu-id="bc0f3-115">A collection of music files on a network share, 10 GB in total.</span></span>|  
  
<span data-ttu-id="bc0f3-116">hello 匯入工作此資料匯入到下列目的地 hello 儲存體帳戶中的 hello:</span><span class="sxs-lookup"><span data-stu-id="bc0f3-116">hello import job imports this data into hello following destinations in hello storage account:</span></span>  
  
|<span data-ttu-id="bc0f3-117">來源</span><span class="sxs-lookup"><span data-stu-id="bc0f3-117">Source</span></span>|<span data-ttu-id="bc0f3-118">目的地虛擬目錄或 Blob</span><span class="sxs-lookup"><span data-stu-id="bc0f3-118">Destination virtual directory or blob</span></span>|  
|------------|-------------------------------------------|  
|<span data-ttu-id="bc0f3-119">H:\Video</span><span class="sxs-lookup"><span data-stu-id="bc0f3-119">H:\Video</span></span>|<span data-ttu-id="bc0f3-120">https://mystorageaccount.blob.core.windows.net/video</span><span class="sxs-lookup"><span data-stu-id="bc0f3-120">https://mystorageaccount.blob.core.windows.net/video</span></span>|  
|<span data-ttu-id="bc0f3-121">H:\Photo</span><span class="sxs-lookup"><span data-stu-id="bc0f3-121">H:\Photo</span></span>|<span data-ttu-id="bc0f3-122">https://mystorageaccount.blob.core.windows.net/photo</span><span class="sxs-lookup"><span data-stu-id="bc0f3-122">https://mystorageaccount.blob.core.windows.net/photo</span></span>|  
|<span data-ttu-id="bc0f3-123">K:\Temp\FavoriteMovie.ISO</span><span class="sxs-lookup"><span data-stu-id="bc0f3-123">K:\Temp\FavoriteMovie.ISO</span></span>|<span data-ttu-id="bc0f3-124">https://mystorageaccount.blob.core.windows.net/favorite/FavoriteMovies.ISO</span><span class="sxs-lookup"><span data-stu-id="bc0f3-124">https://mystorageaccount.blob.core.windows.net/favorite/FavoriteMovies.ISO</span></span>|  
|<span data-ttu-id="bc0f3-125">\\\bigshare\john\music</span><span class="sxs-lookup"><span data-stu-id="bc0f3-125">\\\bigshare\john\music</span></span>|<span data-ttu-id="bc0f3-126">https://mystorageaccount.blob.core.windows.net/music</span><span class="sxs-lookup"><span data-stu-id="bc0f3-126">https://mystorageaccount.blob.core.windows.net/music</span></span>|  
  
<span data-ttu-id="bc0f3-127">透過此對應，hello 檔案`H:\Video\Drama\GreatMovie.mov`是匯入的 toohello blob `https://mystorageaccount.blob.core.windows.net/video/Drama/GreatMovie.mov`。</span><span class="sxs-lookup"><span data-stu-id="bc0f3-127">With this mapping, hello file `H:\Video\Drama\GreatMovie.mov` is imported toohello blob `https://mystorageaccount.blob.core.windows.net/video/Drama/GreatMovie.mov`.</span></span>  
  
<span data-ttu-id="bc0f3-128">下一步 toodetermine 需要多少硬碟機，則計算 hello hello 資料大小：</span><span class="sxs-lookup"><span data-stu-id="bc0f3-128">Next, toodetermine how many hard drives are needed, compute hello size of hello data:</span></span>  
  
`5TB + 30GB + 25GB + 10GB = 5TB + 65GB`  
  
<span data-ttu-id="bc0f3-129">針對此範例，兩個 3 TB 的硬碟應該就已足夠。</span><span class="sxs-lookup"><span data-stu-id="bc0f3-129">For this example, two 3-TB hard drives should be sufficient.</span></span> <span data-ttu-id="bc0f3-130">不過，由於 hello 來源目錄`H:\Video`擁有 5TB 的資料，而您單一硬碟容量只有 3TB，它是必要的 toobreak`H:\Video`分割成兩個較小的目錄：`H:\Video1`和`H:\Video2`，才能執行 hello MicrosoftAzure 匯入/匯出工具。</span><span class="sxs-lookup"><span data-stu-id="bc0f3-130">However, since hello source directory `H:\Video` has 5 TB of data and your single hard drive's capacity is only 3 TB, it's necessary toobreak `H:\Video` into two smaller directories: `H:\Video1` and `H:\Video2`, before running hello Microsoft Azure Import/Export Tool.</span></span> <span data-ttu-id="bc0f3-131">此步驟會產生下列來源目錄的 hello:</span><span class="sxs-lookup"><span data-stu-id="bc0f3-131">This step yields hello following source directories:</span></span>  
  
|<span data-ttu-id="bc0f3-132">位置</span><span class="sxs-lookup"><span data-stu-id="bc0f3-132">Location</span></span>|<span data-ttu-id="bc0f3-133">大小</span><span class="sxs-lookup"><span data-stu-id="bc0f3-133">Size</span></span>|<span data-ttu-id="bc0f3-134">目的地虛擬目錄或 Blob</span><span class="sxs-lookup"><span data-stu-id="bc0f3-134">Destination virtual directory or blob</span></span>|  
|--------------|----------|-------------------------------------------|  
|<span data-ttu-id="bc0f3-135">H:\Video1</span><span class="sxs-lookup"><span data-stu-id="bc0f3-135">H:\Video1</span></span>|<span data-ttu-id="bc0f3-136">2.5 TB</span><span class="sxs-lookup"><span data-stu-id="bc0f3-136">2.5 TB</span></span>|<span data-ttu-id="bc0f3-137">https://mystorageaccount.blob.core.windows.net/video</span><span class="sxs-lookup"><span data-stu-id="bc0f3-137">https://mystorageaccount.blob.core.windows.net/video</span></span>|  
|<span data-ttu-id="bc0f3-138">H:\Video2</span><span class="sxs-lookup"><span data-stu-id="bc0f3-138">H:\Video2</span></span>|<span data-ttu-id="bc0f3-139">2.5 TB</span><span class="sxs-lookup"><span data-stu-id="bc0f3-139">2.5 TB</span></span>|<span data-ttu-id="bc0f3-140">https://mystorageaccount.blob.core.windows.net/video</span><span class="sxs-lookup"><span data-stu-id="bc0f3-140">https://mystorageaccount.blob.core.windows.net/video</span></span>|  
|<span data-ttu-id="bc0f3-141">H:\Photo</span><span class="sxs-lookup"><span data-stu-id="bc0f3-141">H:\Photo</span></span>|<span data-ttu-id="bc0f3-142">30 GB</span><span class="sxs-lookup"><span data-stu-id="bc0f3-142">30 GB</span></span>|<span data-ttu-id="bc0f3-143">https://mystorageaccount.blob.core.windows.net/photo</span><span class="sxs-lookup"><span data-stu-id="bc0f3-143">https://mystorageaccount.blob.core.windows.net/photo</span></span>|  
|<span data-ttu-id="bc0f3-144">K:\Temp\FavoriteMovies.ISO</span><span class="sxs-lookup"><span data-stu-id="bc0f3-144">K:\Temp\FavoriteMovies.ISO</span></span>|<span data-ttu-id="bc0f3-145">25 GB</span><span class="sxs-lookup"><span data-stu-id="bc0f3-145">25 GB</span></span>|<span data-ttu-id="bc0f3-146">https://mystorageaccount.blob.core.windows.net/favorite/FavoriteMovies.ISO</span><span class="sxs-lookup"><span data-stu-id="bc0f3-146">https://mystorageaccount.blob.core.windows.net/favorite/FavoriteMovies.ISO</span></span>|  
|<span data-ttu-id="bc0f3-147">\\\bigshare\john\music</span><span class="sxs-lookup"><span data-stu-id="bc0f3-147">\\\bigshare\john\music</span></span>|<span data-ttu-id="bc0f3-148">10 GB</span><span class="sxs-lookup"><span data-stu-id="bc0f3-148">10 GB</span></span>|<span data-ttu-id="bc0f3-149">https://mystorageaccount.blob.core.windows.net/music</span><span class="sxs-lookup"><span data-stu-id="bc0f3-149">https://mystorageaccount.blob.core.windows.net/music</span></span>|  
  
 <span data-ttu-id="bc0f3-150">即使 hello`H:\Video`目錄已分割 tootwo 目錄、 其點 toohello hello 儲存體帳戶中的同一個目的地虛擬目錄。</span><span class="sxs-lookup"><span data-stu-id="bc0f3-150">Even though hello `H:\Video`directory has been split tootwo directories, they point toohello same destination virtual directory in hello storage account.</span></span> <span data-ttu-id="bc0f3-151">如此一來，所有視訊檔案會維護的單一`video`hello 儲存體帳戶中的容器。</span><span class="sxs-lookup"><span data-stu-id="bc0f3-151">This way, all video files are maintained under a single `video` container in hello storage account.</span></span>  
  
 <span data-ttu-id="bc0f3-152">接下來，hello 前一個來源是目錄平均分佈的 toohello 兩個硬碟：</span><span class="sxs-lookup"><span data-stu-id="bc0f3-152">Next, hello previous source directories are evenly distributed toohello two hard drives:</span></span>  
  
||||  
|-|-|-|  
|<span data-ttu-id="bc0f3-153">硬碟</span><span class="sxs-lookup"><span data-stu-id="bc0f3-153">Hard drive</span></span>|<span data-ttu-id="bc0f3-154">來源目錄</span><span class="sxs-lookup"><span data-stu-id="bc0f3-154">Source directories</span></span>|<span data-ttu-id="bc0f3-155">總大小</span><span class="sxs-lookup"><span data-stu-id="bc0f3-155">Total size</span></span>|  
|<span data-ttu-id="bc0f3-156">第一個硬碟</span><span class="sxs-lookup"><span data-stu-id="bc0f3-156">First Drive</span></span>|<span data-ttu-id="bc0f3-157">H:\Video1</span><span class="sxs-lookup"><span data-stu-id="bc0f3-157">H:\Video1</span></span>|<span data-ttu-id="bc0f3-158">2.5 TB + 30 GB</span><span class="sxs-lookup"><span data-stu-id="bc0f3-158">2.5 TB + 30 GB</span></span>|  
||<span data-ttu-id="bc0f3-159">H:\Photo</span><span class="sxs-lookup"><span data-stu-id="bc0f3-159">H:\Photo</span></span>||  
|<span data-ttu-id="bc0f3-160">第二個硬碟</span><span class="sxs-lookup"><span data-stu-id="bc0f3-160">Second Drive</span></span>|<span data-ttu-id="bc0f3-161">H:\Video2</span><span class="sxs-lookup"><span data-stu-id="bc0f3-161">H:\Video2</span></span>|<span data-ttu-id="bc0f3-162">2.5 TB + 35 GB</span><span class="sxs-lookup"><span data-stu-id="bc0f3-162">2.5 TB + 35 GB</span></span>|  
||<span data-ttu-id="bc0f3-163">K:\Temp\BlueRay.ISO</span><span class="sxs-lookup"><span data-stu-id="bc0f3-163">K:\Temp\BlueRay.ISO</span></span>||  
||<span data-ttu-id="bc0f3-164">\\\bigshare\john\music</span><span class="sxs-lookup"><span data-stu-id="bc0f3-164">\\\bigshare\john\music</span></span>||  
  
<span data-ttu-id="bc0f3-165">此外，您可以設定下列中繼資料的所有檔案的 hello:</span><span class="sxs-lookup"><span data-stu-id="bc0f3-165">In addition, you can set hello following metadata for all files:</span></span>  
  
-   <span data-ttu-id="bc0f3-166">**UploadMethod：**Windows Azure Import/Export service</span><span class="sxs-lookup"><span data-stu-id="bc0f3-166">**UploadMethod:** Windows Azure Import/Export service</span></span>  
  
-   <span data-ttu-id="bc0f3-167">**DataSetName:** SampleData</span><span class="sxs-lookup"><span data-stu-id="bc0f3-167">**DataSetName:** SampleData</span></span>  
  
-   <span data-ttu-id="bc0f3-168">**CreationDate:** 10/1/2013</span><span class="sxs-lookup"><span data-stu-id="bc0f3-168">**CreationDate:** 10/1/2013</span></span>  
  
<span data-ttu-id="bc0f3-169">tooset hello 匯入檔案的中繼資料建立文字檔， `c:\WAImportExport\SampleMetadata.txt`，以下列內容的 hello:</span><span class="sxs-lookup"><span data-stu-id="bc0f3-169">tooset metadata for hello imported files, create a text file, `c:\WAImportExport\SampleMetadata.txt`, with hello following content:</span></span>  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<Metadata>  
    <UploadMethod>Windows Azure Import/Export service</UploadMethod>  
    <DataSetName>SampleData</DataSetName>  
    <CreationDate>10/1/2013</CreationDate>  
</Metadata>  
```
  
<span data-ttu-id="bc0f3-170">您也可以設定某些屬性 hello `FavoriteMovie.ISO` blob:</span><span class="sxs-lookup"><span data-stu-id="bc0f3-170">You can also set some properties for hello `FavoriteMovie.ISO` blob:</span></span>  
  
-   <span data-ttu-id="bc0f3-171">**Content-Type:** application/octet-stream</span><span class="sxs-lookup"><span data-stu-id="bc0f3-171">**Content-Type:** application/octet-stream</span></span>  
  
-   <span data-ttu-id="bc0f3-172">**Content-MD5:** Q2hlY2sgSW50ZWdyaXR5IQ==</span><span class="sxs-lookup"><span data-stu-id="bc0f3-172">**Content-MD5:** Q2hlY2sgSW50ZWdyaXR5IQ==</span></span>  
  
-   <span data-ttu-id="bc0f3-173">**Cache-Control:** no-cache</span><span class="sxs-lookup"><span data-stu-id="bc0f3-173">**Cache-Control:** no-cache</span></span>  
  
<span data-ttu-id="bc0f3-174">tooset 這些內容，請建立文字檔， `c:\WAImportExport\SampleProperties.txt`:</span><span class="sxs-lookup"><span data-stu-id="bc0f3-174">tooset these properties, create a text file, `c:\WAImportExport\SampleProperties.txt`:</span></span>  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<Properties>  
    <Content-Type>application/octet-stream</Content-Type>  
    <Content-MD5>Q2hlY2sgSW50ZWdyaXR5IQ==</Content-MD5>  
    <Cache-Control>no-cache</Cache-Control>  
</Properties>  
```
  
<span data-ttu-id="bc0f3-175">現在您已準備好 toorun hello Azure 匯入/匯出工具 tooprepare hello 兩個硬碟。</span><span class="sxs-lookup"><span data-stu-id="bc0f3-175">Now you are ready toorun hello Azure Import/Export Tool tooprepare hello two hard drives.</span></span> <span data-ttu-id="bc0f3-176">請注意：</span><span class="sxs-lookup"><span data-stu-id="bc0f3-176">Note that:</span></span>  
  
-   <span data-ttu-id="bc0f3-177">hello 第一個磁碟機裝載為磁碟機 X。</span><span class="sxs-lookup"><span data-stu-id="bc0f3-177">hello first drive is mounted as drive X.</span></span>  
  
-   <span data-ttu-id="bc0f3-178">hello 第二個磁碟機裝載為磁碟機 Y。</span><span class="sxs-lookup"><span data-stu-id="bc0f3-178">hello second drive is mounted as drive Y.</span></span>  
  
-   <span data-ttu-id="bc0f3-179">hello 儲存體帳戶的 hello 金鑰`mystorageaccount`是`8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg==`。</span><span class="sxs-lookup"><span data-stu-id="bc0f3-179">hello key for hello storage account `mystorageaccount` is `8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg==`.</span></span>  

## <a name="preparing-disk-for-import-when-data-is-pre-loaded"></a><span data-ttu-id="bc0f3-180">在資料已預先載入時針對匯入準備磁碟</span><span class="sxs-lookup"><span data-stu-id="bc0f3-180">Preparing disk for import when data is pre-loaded</span></span>
 
 <span data-ttu-id="bc0f3-181">如果 hello 資料 toobe 匯入已存在於 hello 磁碟上，使用 hello 旗標 /skipwrite。</span><span class="sxs-lookup"><span data-stu-id="bc0f3-181">If hello data toobe imported is already present on hello disk, use hello flag /skipwrite.</span></span> <span data-ttu-id="bc0f3-182">/t 和 /srcdir hello 值應該在準備用來匯入這兩個點 toohello 磁碟。</span><span class="sxs-lookup"><span data-stu-id="bc0f3-182">hello value of /t and /srcdir should both point toohello disk being prepared for import.</span></span> <span data-ttu-id="bc0f3-183">如果所有 hello 資料 toobe 匯入不會進入 toohello 相同的目的地虛擬目錄或 hello 儲存體帳戶，執行 hello 相同個別命令的每個目的地目錄的根目錄將 /id hello 值保持在 hello 跨所有執行相同。</span><span class="sxs-lookup"><span data-stu-id="bc0f3-183">If all of hello data toobe imported is not going toohello same destination virtual directory or root of hello storage account, run hello same command for each destination directory separately, keeping hello value of /id hello same across all runs.</span></span>

>[!NOTE] 
><span data-ttu-id="bc0f3-184">請勿指定 /format，因為它將會抹除 hello 資料 hello 磁碟上。</span><span class="sxs-lookup"><span data-stu-id="bc0f3-184">Do not specify /format as it will wipe hello data on hello disk.</span></span> <span data-ttu-id="bc0f3-185">您可以指定 / 加密或 /bk 根據是否 hello 磁碟已加密。</span><span class="sxs-lookup"><span data-stu-id="bc0f3-185">You can specify /encrypt or /bk depending on whether hello disk is already encrypted or not.</span></span> 
>

```
    When data is already present on hello disk for each drive run hello following command.
    WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:Video1 /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:x /format /encrypt /srcdir:x:\Video1 /dstdir:video/ /MetadataFile:c:\WAImportExport\SampleMetadata.txt /skipwrite
```

## <a name="copy-sessions---first-drive"></a><span data-ttu-id="bc0f3-186">複製工作階段 - 第一個硬碟</span><span class="sxs-lookup"><span data-stu-id="bc0f3-186">Copy sessions - first drive</span></span>

<span data-ttu-id="bc0f3-187">Hello 第一個磁碟機會執行 hello Azure 匯入/匯出工具兩次 toocopy hello 兩個來源目錄：</span><span class="sxs-lookup"><span data-stu-id="bc0f3-187">For hello first drive, run hello Azure Import/Export Tool twice toocopy hello two source directories:</span></span>  

<span data-ttu-id="bc0f3-188">**第一個複製工作階段**</span><span class="sxs-lookup"><span data-stu-id="bc0f3-188">**First copy session**</span></span>
  
```
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:Video1 /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:x /format /encrypt /srcdir:H:\Video1 /dstdir:video/ /MetadataFile:c:\WAImportExport\SampleMetadata.txt  
```

<span data-ttu-id="bc0f3-189">**第二個複製工作階段**</span><span class="sxs-lookup"><span data-stu-id="bc0f3-189">**Second copy session**</span></span>

```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:Photo /srcdir:H:\Photo /dstdir:photo/ /MetadataFile:c:\WAImportExport\SampleMetadata.txt
```

## <a name="copy-sessions---second-drive"></a><span data-ttu-id="bc0f3-190">複製工作階段 - 第二個硬碟</span><span class="sxs-lookup"><span data-stu-id="bc0f3-190">Copy sessions - second drive</span></span>
 
<span data-ttu-id="bc0f3-191">Hello 第二個磁碟機，執行 hello Azure 匯入/匯出工具三次之後每個 hello 來源目錄，並一次針對 hello 獨立 Blu-Ray™ 影像檔,):</span><span class="sxs-lookup"><span data-stu-id="bc0f3-191">For hello second drive, run hello Azure Import/Export Tool three times, once each for hello source directories, and once for hello standalone Blu-Ray™ image file):</span></span>  
  
<span data-ttu-id="bc0f3-192">**第一個複製工作階段**</span><span class="sxs-lookup"><span data-stu-id="bc0f3-192">**First copy session**</span></span> 

```
WAImportExport.exe PrepImport /j:SecondDrive.jrn /id:Video2 /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:y /format /encrypt /srcdir:H:\Video2 /dstdir:video/ /MetadataFile:c:\WAImportExport\SampleMetadata.txt  
```
  
<span data-ttu-id="bc0f3-193">**第二個複製工作階段**</span><span class="sxs-lookup"><span data-stu-id="bc0f3-193">**Second copy session**</span></span>

```
WAImportExport.exe PrepImport /j:SecondDrive.jrn /id:Music /srcdir:\\bigshare\john\music /dstdir:music/ /MetadataFile:c:\WAImportExport\SampleMetadata.txt  
```  
  
<span data-ttu-id="bc0f3-194">**第三個複製工作階段**</span><span class="sxs-lookup"><span data-stu-id="bc0f3-194">**Third copy session**</span></span>  

```
WAImportExport.exe PrepImport /j:SecondDrive.jrn /id:BlueRayIso /srcfile:K:\Temp\BlueRay.ISO /dstblob:favorite/BlueRay.ISO /MetadataFile:c:\WAImportExport\SampleMetadata.txt /PropertyFile:c:\WAImportExport\SampleProperties.txt  
```

## <a name="copy-session-completion"></a><span data-ttu-id="bc0f3-195">複製工作階段完成</span><span class="sxs-lookup"><span data-stu-id="bc0f3-195">Copy session completion</span></span>

<span data-ttu-id="bc0f3-196">Hello 複製工作階段完成之後，您可以從 hello 複製電腦中斷連線 hello 兩部磁碟機，並將它們寄送 toohello 適當的 Windows Azure 資料中心。</span><span class="sxs-lookup"><span data-stu-id="bc0f3-196">Once hello copy sessions have completed, you can disconnect hello two drives from hello copy computer and ship them toohello appropriate Windows Azure data center.</span></span> <span data-ttu-id="bc0f3-197">上傳 hello 兩個日誌檔，`FirstDrive.jrn`和`SecondDrive.jrn`，當您建立可在 hello hello 匯入作業[Windows Azure 入口網站](https://manage.windowsazure.com/)。</span><span class="sxs-lookup"><span data-stu-id="bc0f3-197">Upload hello two journal files, `FirstDrive.jrn` and `SecondDrive.jrn`, when you create hello import job in hello [Windows Azure portal](https://manage.windowsazure.com/).</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="bc0f3-198">後續步驟</span><span class="sxs-lookup"><span data-stu-id="bc0f3-198">Next steps</span></span>

* [<span data-ttu-id="bc0f3-199">針對匯入作業準備硬碟</span><span class="sxs-lookup"><span data-stu-id="bc0f3-199">Preparing hard drives for an import job</span></span>](../storage-import-export-tool-preparing-hard-drives-import-v1.md)   
* [<span data-ttu-id="bc0f3-200">常用命令快速參考</span><span class="sxs-lookup"><span data-stu-id="bc0f3-200">Quick reference for frequently used commands</span></span>](../storage-import-export-tool-quick-reference-v1.md) 
