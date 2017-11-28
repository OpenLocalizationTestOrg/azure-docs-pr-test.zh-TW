---
title: "針對 Azure 匯入/匯出匯入作業準備硬碟的範例工作流程 - v1 | Microsoft Docs"
description: "請參閱在 Azure 匯入/匯出服務中為匯入作業準備硬碟之完整程序的逐步解說。"
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
ms.openlocfilehash: 313f8c1f3962a943b4c98c530c324ff28aa84c10
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="sample-workflow-to-prepare-hard-drives-for-an-import-job"></a><span data-ttu-id="da491-103">針對匯入作業準備硬碟的範例工作流程</span><span class="sxs-lookup"><span data-stu-id="da491-103">Sample workflow to prepare hard drives for an import job</span></span>
<span data-ttu-id="da491-104">本主題會引導您完成為匯入作業準備硬碟的完整程序。</span><span class="sxs-lookup"><span data-stu-id="da491-104">This topic walks you through the complete process of preparing drives for an import job.</span></span>  
  
<span data-ttu-id="da491-105">此範例會將下列資料匯入名為 `mystorageaccount` 的 Windows Azure 儲存體帳戶：</span><span class="sxs-lookup"><span data-stu-id="da491-105">This example imports the following data into a Window Azure storage account named `mystorageaccount`:</span></span>  
  
|<span data-ttu-id="da491-106">位置</span><span class="sxs-lookup"><span data-stu-id="da491-106">Location</span></span>|<span data-ttu-id="da491-107">說明</span><span class="sxs-lookup"><span data-stu-id="da491-107">Description</span></span>|  
|--------------|-----------------|  
|<span data-ttu-id="da491-108">H:\Video</span><span class="sxs-lookup"><span data-stu-id="da491-108">H:\Video</span></span>|<span data-ttu-id="da491-109">視訊集合，總共 5 TB。</span><span class="sxs-lookup"><span data-stu-id="da491-109">A collection of videos, 5 TB in total.</span></span>|  
|<span data-ttu-id="da491-110">H:\Photo</span><span class="sxs-lookup"><span data-stu-id="da491-110">H:\Photo</span></span>|<span data-ttu-id="da491-111">相片集合，總共 30 GB。</span><span class="sxs-lookup"><span data-stu-id="da491-111">A collection of photos, 30 GB in total.</span></span>|  
|<span data-ttu-id="da491-112">K:\Temp\FavoriteMovie.ISO</span><span class="sxs-lookup"><span data-stu-id="da491-112">K:\Temp\FavoriteMovie.ISO</span></span>|<span data-ttu-id="da491-113">藍光 (Blu-Ray™) 磁碟映像，25 GB。</span><span class="sxs-lookup"><span data-stu-id="da491-113">A Blu-Ray™ disk image, 25 GB.</span></span>|  
|<span data-ttu-id="da491-114">\\\bigshare\john\music</span><span class="sxs-lookup"><span data-stu-id="da491-114">\\\bigshare\john\music</span></span>|<span data-ttu-id="da491-115">網路共用上的音樂檔案集合，總共 10 GB。</span><span class="sxs-lookup"><span data-stu-id="da491-115">A collection of music files on a network share, 10 GB in total.</span></span>|  
  
<span data-ttu-id="da491-116">匯入作業會將此資料匯入儲存體帳戶中的下列目的地：</span><span class="sxs-lookup"><span data-stu-id="da491-116">The import job will import this data into the following destinations in the storage account:</span></span>  
  
|<span data-ttu-id="da491-117">來源</span><span class="sxs-lookup"><span data-stu-id="da491-117">Source</span></span>|<span data-ttu-id="da491-118">目的地虛擬目錄或 Blob</span><span class="sxs-lookup"><span data-stu-id="da491-118">Destination virtual directory or blob</span></span>|  
|------------|-------------------------------------------|  
|<span data-ttu-id="da491-119">H:\Video</span><span class="sxs-lookup"><span data-stu-id="da491-119">H:\Video</span></span>|<span data-ttu-id="da491-120">https://mystorageaccount.blob.core.windows.net/video</span><span class="sxs-lookup"><span data-stu-id="da491-120">https://mystorageaccount.blob.core.windows.net/video</span></span>|  
|<span data-ttu-id="da491-121">H:\Photo</span><span class="sxs-lookup"><span data-stu-id="da491-121">H:\Photo</span></span>|<span data-ttu-id="da491-122">https://mystorageaccount.blob.core.windows.net/photo</span><span class="sxs-lookup"><span data-stu-id="da491-122">https://mystorageaccount.blob.core.windows.net/photo</span></span>|  
|<span data-ttu-id="da491-123">K:\Temp\FavoriteMovie.ISO</span><span class="sxs-lookup"><span data-stu-id="da491-123">K:\Temp\FavoriteMovie.ISO</span></span>|<span data-ttu-id="da491-124">https://mystorageaccount.blob.core.windows.net/favorite/FavoriteMovies.ISO</span><span class="sxs-lookup"><span data-stu-id="da491-124">https://mystorageaccount.blob.core.windows.net/favorite/FavoriteMovies.ISO</span></span>|  
|<span data-ttu-id="da491-125">\\\bigshare\john\music</span><span class="sxs-lookup"><span data-stu-id="da491-125">\\\bigshare\john\music</span></span>|<span data-ttu-id="da491-126">https://mystorageaccount.blob.core.windows.net/music</span><span class="sxs-lookup"><span data-stu-id="da491-126">https://mystorageaccount.blob.core.windows.net/music</span></span>|  
  
<span data-ttu-id="da491-127">透過此對應，檔案 `H:\Video\Drama\GreatMovie.mov` 將會匯入 Blob `https://mystorageaccount.blob.core.windows.net/video/Drama/GreatMovie.mov`。</span><span class="sxs-lookup"><span data-stu-id="da491-127">With this mapping, the file `H:\Video\Drama\GreatMovie.mov` will be imported to the blob `https://mystorageaccount.blob.core.windows.net/video/Drama/GreatMovie.mov`.</span></span>  
  
<span data-ttu-id="da491-128">接下來，為了判斷需要幾個硬碟，將會計算資料大小：</span><span class="sxs-lookup"><span data-stu-id="da491-128">Next, to determine how many hard drives are needed, compute the size of the data:</span></span>  
  
`5TB + 30GB + 25GB + 10GB = 5TB + 65GB`  
  
<span data-ttu-id="da491-129">針對此範例，兩個 3TB 的硬碟應該就已足夠。</span><span class="sxs-lookup"><span data-stu-id="da491-129">For this example, two 3TB hard drives should be sufficient.</span></span> <span data-ttu-id="da491-130">不過，由於來源目錄 `H:\Video` 具有 5TB 的資料，而您的單一硬碟容量只有 3TB，因此必須在執行 Microsoft Azure 匯入/匯出工具之前，將 `H:\Video` 分為兩個較小的目錄：`H:\Video1` 和 `H:\Video2`。</span><span class="sxs-lookup"><span data-stu-id="da491-130">However, since the source directory `H:\Video` has 5TB of data and your single hard drive's capacity is only 3TB, it's necessary to break `H:\Video` into two smaller directories before running the Microsoft Azure Import/Export Tool: `H:\Video1` and `H:\Video2`.</span></span> <span data-ttu-id="da491-131">此步驟將會產生下列來源目錄：</span><span class="sxs-lookup"><span data-stu-id="da491-131">This step yields the following source directories:</span></span>  
  
|<span data-ttu-id="da491-132">位置</span><span class="sxs-lookup"><span data-stu-id="da491-132">Location</span></span>|<span data-ttu-id="da491-133">大小</span><span class="sxs-lookup"><span data-stu-id="da491-133">Size</span></span>|<span data-ttu-id="da491-134">目的地虛擬目錄或 Blob</span><span class="sxs-lookup"><span data-stu-id="da491-134">Destination virtual directory or blob</span></span>|  
|--------------|----------|-------------------------------------------|  
|<span data-ttu-id="da491-135">H:\Video1</span><span class="sxs-lookup"><span data-stu-id="da491-135">H:\Video1</span></span>|<span data-ttu-id="da491-136">2.5TB</span><span class="sxs-lookup"><span data-stu-id="da491-136">2.5TB</span></span>|<span data-ttu-id="da491-137">https://mystorageaccount.blob.core.windows.net/video</span><span class="sxs-lookup"><span data-stu-id="da491-137">https://mystorageaccount.blob.core.windows.net/video</span></span>|  
|<span data-ttu-id="da491-138">H:\Video2</span><span class="sxs-lookup"><span data-stu-id="da491-138">H:\Video2</span></span>|<span data-ttu-id="da491-139">2.5TB</span><span class="sxs-lookup"><span data-stu-id="da491-139">2.5TB</span></span>|<span data-ttu-id="da491-140">https://mystorageaccount.blob.core.windows.net/video</span><span class="sxs-lookup"><span data-stu-id="da491-140">https://mystorageaccount.blob.core.windows.net/video</span></span>|  
|<span data-ttu-id="da491-141">H:\Photo</span><span class="sxs-lookup"><span data-stu-id="da491-141">H:\Photo</span></span>|<span data-ttu-id="da491-142">30GB</span><span class="sxs-lookup"><span data-stu-id="da491-142">30GB</span></span>|<span data-ttu-id="da491-143">https://mystorageaccount.blob.core.windows.net/photo</span><span class="sxs-lookup"><span data-stu-id="da491-143">https://mystorageaccount.blob.core.windows.net/photo</span></span>|  
|<span data-ttu-id="da491-144">K:\Temp\FavoriteMovies.ISO</span><span class="sxs-lookup"><span data-stu-id="da491-144">K:\Temp\FavoriteMovies.ISO</span></span>|<span data-ttu-id="da491-145">25GB</span><span class="sxs-lookup"><span data-stu-id="da491-145">25GB</span></span>|<span data-ttu-id="da491-146">https://mystorageaccount.blob.core.windows.net/favorite/FavoriteMovies.ISO</span><span class="sxs-lookup"><span data-stu-id="da491-146">https://mystorageaccount.blob.core.windows.net/favorite/FavoriteMovies.ISO</span></span>|  
|<span data-ttu-id="da491-147">\\\bigshare\john\music</span><span class="sxs-lookup"><span data-stu-id="da491-147">\\\bigshare\john\music</span></span>|<span data-ttu-id="da491-148">10GB</span><span class="sxs-lookup"><span data-stu-id="da491-148">10GB</span></span>|<span data-ttu-id="da491-149">https://mystorageaccount.blob.core.windows.net/music</span><span class="sxs-lookup"><span data-stu-id="da491-149">https://mystorageaccount.blob.core.windows.net/music</span></span>|  
  
 <span data-ttu-id="da491-150">請注意，雖然 `H:\Video` 目錄被分為兩個目錄，它們仍然會指向儲存體帳戶中的相同目的地虛擬目錄。</span><span class="sxs-lookup"><span data-stu-id="da491-150">Note that even though the `H:\Video`directory has been split to two directories, they point to the same destination virtual directory in the storage account.</span></span> <span data-ttu-id="da491-151">如此一來，所有視訊檔案都會維持在儲存體帳戶中的單一 `video` 容器中。</span><span class="sxs-lookup"><span data-stu-id="da491-151">This way, all video files are maintained under a single `video` container in the storage account.</span></span>  
  
 <span data-ttu-id="da491-152">接下來，上述來源目錄將會平均地分散到兩個硬碟：</span><span class="sxs-lookup"><span data-stu-id="da491-152">Next, the above source directories are evenly distributed to the two hard drives:</span></span>  
  
||||  
|-|-|-|  
|<span data-ttu-id="da491-153">硬碟</span><span class="sxs-lookup"><span data-stu-id="da491-153">Hard drive</span></span>|<span data-ttu-id="da491-154">來源目錄</span><span class="sxs-lookup"><span data-stu-id="da491-154">Source directories</span></span>|<span data-ttu-id="da491-155">總大小</span><span class="sxs-lookup"><span data-stu-id="da491-155">Total size</span></span>|  
|<span data-ttu-id="da491-156">第一個硬碟</span><span class="sxs-lookup"><span data-stu-id="da491-156">First Drive</span></span>|<span data-ttu-id="da491-157">H:\Video1</span><span class="sxs-lookup"><span data-stu-id="da491-157">H:\Video1</span></span>|<span data-ttu-id="da491-158">2.5TB + 30GB</span><span class="sxs-lookup"><span data-stu-id="da491-158">2.5TB + 30GB</span></span>|  
||<span data-ttu-id="da491-159">H:\Photo</span><span class="sxs-lookup"><span data-stu-id="da491-159">H:\Photo</span></span>||  
|<span data-ttu-id="da491-160">第二個硬碟</span><span class="sxs-lookup"><span data-stu-id="da491-160">Second Drive</span></span>|<span data-ttu-id="da491-161">H:\Video2</span><span class="sxs-lookup"><span data-stu-id="da491-161">H:\Video2</span></span>|<span data-ttu-id="da491-162">2.5TB + 35GB</span><span class="sxs-lookup"><span data-stu-id="da491-162">2.5TB + 35GB</span></span>|  
||<span data-ttu-id="da491-163">K:\Temp\BlueRay.ISO</span><span class="sxs-lookup"><span data-stu-id="da491-163">K:\Temp\BlueRay.ISO</span></span>||  
||<span data-ttu-id="da491-164">\\\bigshare\john\music</span><span class="sxs-lookup"><span data-stu-id="da491-164">\\\bigshare\john\music</span></span>||  
  
<span data-ttu-id="da491-165">除此之外，您可以針對所有檔案設定下列中繼資料：</span><span class="sxs-lookup"><span data-stu-id="da491-165">In addition, you can set the following metadata for all files:</span></span>  
  
-   <span data-ttu-id="da491-166">**UploadMethod：**Windows Azure Import/Export service</span><span class="sxs-lookup"><span data-stu-id="da491-166">**UploadMethod:** Windows Azure Import/Export service</span></span>  
  
-   <span data-ttu-id="da491-167">**DataSetName:** SampleData</span><span class="sxs-lookup"><span data-stu-id="da491-167">**DataSetName:** SampleData</span></span>  
  
-   <span data-ttu-id="da491-168">**CreationDate:** 10/1/2013</span><span class="sxs-lookup"><span data-stu-id="da491-168">**CreationDate:** 10/1/2013</span></span>  
  
<span data-ttu-id="da491-169">若要針對匯入檔案設定中繼資料，請建立具有下列內容的文字檔 (`c:\WAImportExport\SampleMetadata.txt`)：</span><span class="sxs-lookup"><span data-stu-id="da491-169">To set metadata for the imported files, create a text file, `c:\WAImportExport\SampleMetadata.txt`, with the following content:</span></span>  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<Metadata>  
    <UploadMethod>Windows Azure Import/Export service</UploadMethod>  
    <DataSetName>SampleData</DataSetName>  
    <CreationDate>10/1/2013</CreationDate>  
</Metadata>  
```
  
<span data-ttu-id="da491-170">您也可以設定 `FavoriteMovie.ISO` Blob 的部分屬性：</span><span class="sxs-lookup"><span data-stu-id="da491-170">You can also set some properties for the `FavoriteMovie.ISO` blob:</span></span>  
  
-   <span data-ttu-id="da491-171">**Content-Type:** application/octet-stream</span><span class="sxs-lookup"><span data-stu-id="da491-171">**Content-Type:** application/octet-stream</span></span>  
  
-   <span data-ttu-id="da491-172">**Content-MD5:** Q2hlY2sgSW50ZWdyaXR5IQ==</span><span class="sxs-lookup"><span data-stu-id="da491-172">**Content-MD5:** Q2hlY2sgSW50ZWdyaXR5IQ==</span></span>  
  
-   <span data-ttu-id="da491-173">**Cache-Control:** no-cache</span><span class="sxs-lookup"><span data-stu-id="da491-173">**Cache-Control:** no-cache</span></span>  
  
<span data-ttu-id="da491-174">若要設定這些屬性，請建立文字檔 (`c:\WAImportExport\SampleProperties.txt`)：</span><span class="sxs-lookup"><span data-stu-id="da491-174">To set these properties, create a text file, `c:\WAImportExport\SampleProperties.txt`:</span></span>  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<Properties>  
    <Content-Type>application/octet-stream</Content-Type>  
    <Content-MD5>Q2hlY2sgSW50ZWdyaXR5IQ==</Content-MD5>  
    <Cache-Control>no-cache</Cache-Control>  
</Properties>  
```
  
<span data-ttu-id="da491-175">現在您已準備好執行 Azure 匯入/匯出工具以準備兩個硬碟。</span><span class="sxs-lookup"><span data-stu-id="da491-175">Now you are ready to run the Azure Import/Export Tool to prepare the two hard drives.</span></span> <span data-ttu-id="da491-176">請注意：</span><span class="sxs-lookup"><span data-stu-id="da491-176">Note that:</span></span>  
  
-   <span data-ttu-id="da491-177">第一個硬碟會裝載為硬碟 X。</span><span class="sxs-lookup"><span data-stu-id="da491-177">The first drive is mounted as drive X.</span></span>  
  
-   <span data-ttu-id="da491-178">第二個硬碟會裝載為硬碟 Y。</span><span class="sxs-lookup"><span data-stu-id="da491-178">The second drive is mounted as drive Y.</span></span>  
  
-   <span data-ttu-id="da491-179">儲存體帳戶 `mystorageaccount` 的金鑰是 `8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg==`。</span><span class="sxs-lookup"><span data-stu-id="da491-179">The key for the storage account `mystorageaccount` is `8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg==`.</span></span>  

## <a name="preparing-disk-for-import-when-data-is-pre-loaded"></a><span data-ttu-id="da491-180">在資料已預先載入時針對匯入準備磁碟</span><span class="sxs-lookup"><span data-stu-id="da491-180">Preparing disk for import when data is pre-loaded</span></span>
 
 <span data-ttu-id="da491-181">如果要匯入的資料已經存在於磁碟上，請使用 /skipwrite 旗標。</span><span class="sxs-lookup"><span data-stu-id="da491-181">If the data to be imported is already present on the disk, use the flag /skipwrite.</span></span> <span data-ttu-id="da491-182">/t 和 /srcdir 的值都應該指向正在針對匯入進行準備的磁碟。</span><span class="sxs-lookup"><span data-stu-id="da491-182">Value of /t and /srcdir both should point to the disk being prepared for import.</span></span> <span data-ttu-id="da491-183">如果磁碟上有部分資料不需要移至相同的目的地虛擬目錄或儲存體帳戶的根，請針對每個目錄獨立執行相同的命令，使 /id 的值在每次執行時都相同。</span><span class="sxs-lookup"><span data-stu-id="da491-183">If not all the data on the disk needs to go to the same destination virtual directory or root of the storage account, run the same command for each directory separately keeping the value of /id same across all runs.</span></span>

>[!NOTE] 
><span data-ttu-id="da491-184">請不要指定 /format，因為這將會清除磁碟上所有的資料。</span><span class="sxs-lookup"><span data-stu-id="da491-184">Do not specify /format as it will wipe the data on the disk.</span></span> <span data-ttu-id="da491-185">根據磁碟是否已經加密，您可以指定 /encrypt 或 /bk。</span><span class="sxs-lookup"><span data-stu-id="da491-185">You can specify /encrypt or /bk depending on whether the disk is already encrypted or not.</span></span> 
>

```
    When data is already present on the disk for each drive run the following command.
    WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:Video1 /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:x /format /encrypt /srcdir:x:\Video1 /dstdir:video/ /MetadataFile:c:\WAImportExport\SampleMetadata.txt /skipwrite
```

## <a name="copy-sessions---first-drive"></a><span data-ttu-id="da491-186">複製工作階段 - 第一個硬碟</span><span class="sxs-lookup"><span data-stu-id="da491-186">Copy sessions - first drive</span></span>

<span data-ttu-id="da491-187">針對第一個硬碟，執行 Azure 匯入/匯出工具兩次以複製兩個來源目錄：</span><span class="sxs-lookup"><span data-stu-id="da491-187">For the first drive, run the Azure Import/Export Tool twice to copy the two source directories:</span></span>  

<span data-ttu-id="da491-188">**第一個複製工作階段**</span><span class="sxs-lookup"><span data-stu-id="da491-188">**First copy session**</span></span>
  
```
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:Video1 /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:x /format /encrypt /srcdir:H:\Video1 /dstdir:video/ /MetadataFile:c:\WAImportExport\SampleMetadata.txt  
```

<span data-ttu-id="da491-189">**第二個複製工作階段**</span><span class="sxs-lookup"><span data-stu-id="da491-189">**Second copy session**</span></span>

```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:Photo /srcdir:H:\Photo /dstdir:photo/ /MetadataFile:c:\WAImportExport\SampleMetadata.txt
```

## <a name="copy-sessions---second-drive"></a><span data-ttu-id="da491-190">複製工作階段 - 第二個硬碟</span><span class="sxs-lookup"><span data-stu-id="da491-190">Copy sessions - second drive</span></span>
 
<span data-ttu-id="da491-191">針對第二個硬碟，執行 Azure 匯入/匯出工具三次 (針對兩個來源目錄各一次，針對獨立藍光 (Blu-Ray™) 映像檔一次)：</span><span class="sxs-lookup"><span data-stu-id="da491-191">For the second drive, run the Azure Import/Export Tool three times, once each for the source directories, and once for the standalone Blu-Ray™ image file):</span></span>  
  
<span data-ttu-id="da491-192">**第一個複製工作階段**</span><span class="sxs-lookup"><span data-stu-id="da491-192">**First copy session**</span></span> 

```
WAImportExport.exe PrepImport /j:SecondDrive.jrn /id:Video2 /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:y /format /encrypt /srcdir:H:\Video2 /dstdir:video/ /MetadataFile:c:\WAImportExport\SampleMetadata.txt  
```
  
<span data-ttu-id="da491-193">**第二個複製工作階段**</span><span class="sxs-lookup"><span data-stu-id="da491-193">**Second copy session**</span></span>

```
WAImportExport.exe PrepImport /j:SecondDrive.jrn /id:Music /srcdir:\\bigshare\john\music /dstdir:music/ /MetadataFile:c:\WAImportExport\SampleMetadata.txt  
```  
  
<span data-ttu-id="da491-194">**第三個複製工作階段**</span><span class="sxs-lookup"><span data-stu-id="da491-194">**Third copy session**</span></span>  

```
WAImportExport.exe PrepImport /j:SecondDrive.jrn /id:BlueRayIso /srcfile:K:\Temp\BlueRay.ISO /dstblob:favorite/BlueRay.ISO /MetadataFile:c:\WAImportExport\SampleMetadata.txt /PropertyFile:c:\WAImportExport\SampleProperties.txt  
```

## <a name="copy-session-completion"></a><span data-ttu-id="da491-195">複製工作階段完成</span><span class="sxs-lookup"><span data-stu-id="da491-195">Copy session completion</span></span>

<span data-ttu-id="da491-196">當複製工作階段完成後，您可以將兩個磁碟和複製電腦中斷連線，並將它們寄送到適當的 Microsoft Azure 資料中心。</span><span class="sxs-lookup"><span data-stu-id="da491-196">Once the copy sessions have completed, you can disconnect the two drives from the copy computer and ship them to the appropriate Windows Azure data center.</span></span> <span data-ttu-id="da491-197">當您在 [Microsoft Azure 管理入口網站](https://manage.windowsazure.com/)建立匯入作業時，您將會上傳兩個日誌檔案 (`FirstDrive.jrn` 和 `SecondDrive.jrn`)。</span><span class="sxs-lookup"><span data-stu-id="da491-197">You'll upload the two journal files, `FirstDrive.jrn` and `SecondDrive.jrn`, when you create the import job in the [Windows Azure Management Portal](https://manage.windowsazure.com/).</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="da491-198">後續步驟</span><span class="sxs-lookup"><span data-stu-id="da491-198">Next steps</span></span>

* [<span data-ttu-id="da491-199">針對匯入作業準備硬碟</span><span class="sxs-lookup"><span data-stu-id="da491-199">Preparing hard drives for an import job</span></span>](storage-import-export-tool-preparing-hard-drives-import-v1.md)   
* [<span data-ttu-id="da491-200">常用命令快速參考</span><span class="sxs-lookup"><span data-stu-id="da491-200">Quick reference for frequently used commands</span></span>](storage-import-export-tool-quick-reference-v1.md) 
