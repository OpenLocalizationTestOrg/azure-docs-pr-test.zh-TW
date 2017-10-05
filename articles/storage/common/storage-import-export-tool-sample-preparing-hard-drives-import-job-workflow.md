---
title: "針對 Azure 匯入/匯出匯入作業準備硬碟的範例工作流程 | Microsoft Docs"
description: "請參閱在 Azure 匯入/匯出服務中為匯入作業準備硬碟之完整程序的逐步解說。"
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
ms.date: 04/07/2017
ms.author: muralikk
ms.openlocfilehash: 83cb82b9807718e7a509312d159eb766a5da1d2c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="sample-workflow-to-prepare-hard-drives-for-an-import-job"></a><span data-ttu-id="cba23-103">針對匯入作業準備硬碟的範例工作流程</span><span class="sxs-lookup"><span data-stu-id="cba23-103">Sample workflow to prepare hard drives for an import job</span></span>

<span data-ttu-id="cba23-104">本文章會引導您完成為匯入作業準備硬碟的完整程序。</span><span class="sxs-lookup"><span data-stu-id="cba23-104">This article walks you through the complete process of preparing drives for an import job.</span></span>

## <a name="sample-data"></a><span data-ttu-id="cba23-105">範例資料</span><span class="sxs-lookup"><span data-stu-id="cba23-105">Sample data</span></span>

<span data-ttu-id="cba23-106">此範例會將下列資料匯入名為 `mystorageaccount` 的 Azure 儲存體帳戶：</span><span class="sxs-lookup"><span data-stu-id="cba23-106">This example imports the following data into an Azure storage account named `mystorageaccount`:</span></span>

|<span data-ttu-id="cba23-107">位置</span><span class="sxs-lookup"><span data-stu-id="cba23-107">Location</span></span>|<span data-ttu-id="cba23-108">說明</span><span class="sxs-lookup"><span data-stu-id="cba23-108">Description</span></span>|<span data-ttu-id="cba23-109">資料大小</span><span class="sxs-lookup"><span data-stu-id="cba23-109">Data size</span></span>|
|--------------|-----------------|-----|
|<span data-ttu-id="cba23-110">H:\Video\\</span><span class="sxs-lookup"><span data-stu-id="cba23-110">H:\Video\\</span></span> |<span data-ttu-id="cba23-111">視訊集合</span><span class="sxs-lookup"><span data-stu-id="cba23-111">A collection of videos</span></span>|<span data-ttu-id="cba23-112">12 TB</span><span class="sxs-lookup"><span data-stu-id="cba23-112">12 TB</span></span>|
|<span data-ttu-id="cba23-113">H:\Photo\\</span><span class="sxs-lookup"><span data-stu-id="cba23-113">H:\Photo\\</span></span> |<span data-ttu-id="cba23-114">相片集合</span><span class="sxs-lookup"><span data-stu-id="cba23-114">A collection of photos</span></span>|<span data-ttu-id="cba23-115">30 GB</span><span class="sxs-lookup"><span data-stu-id="cba23-115">30 GB</span></span>|
|<span data-ttu-id="cba23-116">K:\Temp\FavoriteMovie.ISO</span><span class="sxs-lookup"><span data-stu-id="cba23-116">K:\Temp\FavoriteMovie.ISO</span></span>|<span data-ttu-id="cba23-117">藍光 (Blu-Ray™) 磁碟映像</span><span class="sxs-lookup"><span data-stu-id="cba23-117">A Blu-Ray™ disk image</span></span>|<span data-ttu-id="cba23-118">25 GB</span><span class="sxs-lookup"><span data-stu-id="cba23-118">25 GB</span></span>|
|<span data-ttu-id="cba23-119">\\\bigshare\john\music\\</span><span class="sxs-lookup"><span data-stu-id="cba23-119">\\\bigshare\john\music\\</span></span>|<span data-ttu-id="cba23-120">網路共用上的音樂檔案集合</span><span class="sxs-lookup"><span data-stu-id="cba23-120">A collection of music files on a network share</span></span>|<span data-ttu-id="cba23-121">10 GB</span><span class="sxs-lookup"><span data-stu-id="cba23-121">10 GB</span></span>|

## <a name="storage-account-destinations"></a><span data-ttu-id="cba23-122">儲存體帳戶目的地</span><span class="sxs-lookup"><span data-stu-id="cba23-122">Storage account destinations</span></span>

<span data-ttu-id="cba23-123">匯入作業會將資料匯入儲存體帳戶中的下列目的地：</span><span class="sxs-lookup"><span data-stu-id="cba23-123">The import job will import the data into the following destinations in the storage account:</span></span>

|<span data-ttu-id="cba23-124">來源</span><span class="sxs-lookup"><span data-stu-id="cba23-124">Source</span></span>|<span data-ttu-id="cba23-125">目的地虛擬目錄或 Blob</span><span class="sxs-lookup"><span data-stu-id="cba23-125">Destination virtual directory or blob</span></span>|
|------------|-------------------------------------------|
|<span data-ttu-id="cba23-126">H:\Video\\</span><span class="sxs-lookup"><span data-stu-id="cba23-126">H:\Video\\</span></span> |<span data-ttu-id="cba23-127">video/</span><span class="sxs-lookup"><span data-stu-id="cba23-127">video/</span></span>|
|<span data-ttu-id="cba23-128">H:\Photo\\</span><span class="sxs-lookup"><span data-stu-id="cba23-128">H:\Photo\\</span></span> |<span data-ttu-id="cba23-129">photo/</span><span class="sxs-lookup"><span data-stu-id="cba23-129">photo/</span></span>|
|<span data-ttu-id="cba23-130">K:\Temp\FavoriteMovie.ISO</span><span class="sxs-lookup"><span data-stu-id="cba23-130">K:\Temp\FavoriteMovie.ISO</span></span>|<span data-ttu-id="cba23-131">favorite/FavoriteMovies.ISO</span><span class="sxs-lookup"><span data-stu-id="cba23-131">favorite/FavoriteMovies.ISO</span></span>|
|<span data-ttu-id="cba23-132">\\\bigshare\john\music\\</span><span class="sxs-lookup"><span data-stu-id="cba23-132">\\\bigshare\john\music\\</span></span> |<span data-ttu-id="cba23-133">music</span><span class="sxs-lookup"><span data-stu-id="cba23-133">music</span></span>|

<span data-ttu-id="cba23-134">透過此對應，檔案 `H:\Video\Drama\GreatMovie.mov` 將會匯入 Blob `https://mystorageaccount.blob.core.windows.net/video/Drama/GreatMovie.mov`。</span><span class="sxs-lookup"><span data-stu-id="cba23-134">With this mapping, the file `H:\Video\Drama\GreatMovie.mov` will be imported to the blob `https://mystorageaccount.blob.core.windows.net/video/Drama/GreatMovie.mov`.</span></span>

## <a name="determine-hard-drive-requirements"></a><span data-ttu-id="cba23-135">判斷硬碟需求</span><span class="sxs-lookup"><span data-stu-id="cba23-135">Determine hard drive requirements</span></span>

<span data-ttu-id="cba23-136">接下來，為了判斷需要幾個硬碟，將會計算資料大小：</span><span class="sxs-lookup"><span data-stu-id="cba23-136">Next, to determine how many hard drives are needed, compute the size of the data:</span></span>

`12TB + 30GB + 25GB + 10GB = 12TB + 65GB`

<span data-ttu-id="cba23-137">針對此範例，兩個 8TB 的硬碟應該就已足夠。</span><span class="sxs-lookup"><span data-stu-id="cba23-137">For this example, two 8TB hard drives should be sufficient.</span></span> <span data-ttu-id="cba23-138">不過，由於來源目錄 `H:\Video` 具有 12TB 的資料，而您的單一硬碟容量只有 8TB，您將可以在 **driveset.csv** 檔案中以下列方法指定這個情況：</span><span class="sxs-lookup"><span data-stu-id="cba23-138">However, since the source directory `H:\Video` has 12TB of data and your single hard drive's capacity is only 8TB, you will be able to specify this in the following way in the **driveset.csv** file:</span></span>

```
DriveLetter,FormatOption,SilentOrPromptOnFormat,Encryption,ExistingBitLockerKey
X,Format,SilentMode,Encrypt,
Y,Format,SilentMode,Encrypt,
```
<span data-ttu-id="cba23-139">該工具將會把資料以最佳化的方式分散到兩個硬碟。</span><span class="sxs-lookup"><span data-stu-id="cba23-139">The tool will distribute data across two hard drives in an optimized way.</span></span>

## <a name="attach-drives-and-configure-the-job"></a><span data-ttu-id="cba23-140">附加磁碟並設定作業</span><span class="sxs-lookup"><span data-stu-id="cba23-140">Attach drives and configure the job</span></span>
<span data-ttu-id="cba23-141">您將兩個磁碟連接到機器，並建立磁碟區。</span><span class="sxs-lookup"><span data-stu-id="cba23-141">You will attach both disks to the machine and create volumes.</span></span> <span data-ttu-id="cba23-142">然後撰寫 **dataset.csv** 檔案：</span><span class="sxs-lookup"><span data-stu-id="cba23-142">Then author **dataset.csv** file:</span></span>
```
BasePath,DstBlobPathOrPrefix,BlobType,Disposition,MetadataFile,PropertiesFile
H:\Video\,video/,BlockBlob,rename,None,H:\mydirectory\properties.xml
H:\Photo\,photo/,BlockBlob,rename,None,H:\mydirectory\properties.xml
K:\Temp\FavoriteVideo.ISO,favorite/FavoriteVideo.ISO,BlockBlob,rename,None,H:\mydirectory\properties.xml
\\myshare\john\music\,music/,BlockBlob,rename,None,H:\mydirectory\properties.xml
```

<span data-ttu-id="cba23-143">除此之外，您可以針對所有檔案設定下列中繼資料：</span><span class="sxs-lookup"><span data-stu-id="cba23-143">In addition, you can set the following metadata for all files:</span></span>

* <span data-ttu-id="cba23-144">**UploadMethod：**Windows Azure Import/Export service</span><span class="sxs-lookup"><span data-stu-id="cba23-144">**UploadMethod:** Windows Azure Import/Export service</span></span>
* <span data-ttu-id="cba23-145">**DataSetName:** SampleData</span><span class="sxs-lookup"><span data-stu-id="cba23-145">**DataSetName:** SampleData</span></span>
* <span data-ttu-id="cba23-146">**CreationDate:** 10/1/2013</span><span class="sxs-lookup"><span data-stu-id="cba23-146">**CreationDate:** 10/1/2013</span></span>

<span data-ttu-id="cba23-147">若要針對匯入檔案設定中繼資料，請建立具有下列內容的文字檔 (`c:\WAImportExport\SampleMetadata.txt`)：</span><span class="sxs-lookup"><span data-stu-id="cba23-147">To set metadata for the imported files, create a text file, `c:\WAImportExport\SampleMetadata.txt`, with the following content:</span></span>

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Metadata>
    <UploadMethod>Windows Azure Import/Export service</UploadMethod>
    <DataSetName>SampleData</DataSetName>
    <CreationDate>10/1/2013</CreationDate>
</Metadata>
```

<span data-ttu-id="cba23-148">您也可以設定 `FavoriteMovie.ISO` Blob 的部分屬性：</span><span class="sxs-lookup"><span data-stu-id="cba23-148">You can also set some properties for the `FavoriteMovie.ISO` blob:</span></span>

* <span data-ttu-id="cba23-149">**Content-Type:** application/octet-stream</span><span class="sxs-lookup"><span data-stu-id="cba23-149">**Content-Type:** application/octet-stream</span></span>
* <span data-ttu-id="cba23-150">**Content-MD5:** Q2hlY2sgSW50ZWdyaXR5IQ==</span><span class="sxs-lookup"><span data-stu-id="cba23-150">**Content-MD5:** Q2hlY2sgSW50ZWdyaXR5IQ==</span></span>
* <span data-ttu-id="cba23-151">**Cache-Control:** no-cache</span><span class="sxs-lookup"><span data-stu-id="cba23-151">**Cache-Control:** no-cache</span></span>

<span data-ttu-id="cba23-152">若要設定這些屬性，請建立文字檔 (`c:\WAImportExport\SampleProperties.txt`)：</span><span class="sxs-lookup"><span data-stu-id="cba23-152">To set these properties, create a text file, `c:\WAImportExport\SampleProperties.txt`:</span></span>

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Properties>
    <Content-Type>application/octet-stream</Content-Type>
    <Content-MD5>Q2hlY2sgSW50ZWdyaXR5IQ==</Content-MD5>
    <Cache-Control>no-cache</Cache-Control>
</Properties>
```

## <a name="run-the-azure-importexport-tool-waimportexportexe"></a><span data-ttu-id="cba23-153">執行 Azure 匯入/匯出工具 (WAImportExport.exe)</span><span class="sxs-lookup"><span data-stu-id="cba23-153">Run the Azure Import/Export Tool (WAImportExport.exe)</span></span>

<span data-ttu-id="cba23-154">現在您已準備好執行 Azure 匯入/匯出工具以準備兩個硬碟。</span><span class="sxs-lookup"><span data-stu-id="cba23-154">Now you are ready to run the Azure Import/Export Tool to prepare the two hard drives.</span></span>

<span data-ttu-id="cba23-155">**第一個工作階段︰**</span><span class="sxs-lookup"><span data-stu-id="cba23-155">**For the first session:**</span></span>

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#1  /sk:************* /InitialDriveSet:driveset-1.csv /DataSet:dataset-1.csv /logdir:F:\logs
```

<span data-ttu-id="cba23-156">如果需要新增額外的資料，請建立另一個資料集檔案 (和初始資料集相同格式)。</span><span class="sxs-lookup"><span data-stu-id="cba23-156">If any more data needs to be added, create another dataset file (same format as Initialdataset).</span></span>

<span data-ttu-id="cba23-157">**第二個工作階段︰**</span><span class="sxs-lookup"><span data-stu-id="cba23-157">**For the second session:**</span></span>

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#2  /DataSet:dataset-2.csv
```

<span data-ttu-id="cba23-158">當複製工作階段完成後，您可以將兩個磁碟和複製電腦中斷連線，並將它們寄送到適當的 Azure 資料中心。</span><span class="sxs-lookup"><span data-stu-id="cba23-158">Once the copy sessions have completed, you can disconnect the two drives from the copy computer and ship them to the appropriate Azure data center.</span></span> <span data-ttu-id="cba23-159">當您在 Azure 入口網站建立匯入作業時，您將會上傳兩個日誌檔案 (`<FirstDriveSerialNumber>.xml` 和 `<SecondDriveSerialNumber>.xml`)。</span><span class="sxs-lookup"><span data-stu-id="cba23-159">You'll upload the two journal files, `<FirstDriveSerialNumber>.xml` and `<SecondDriveSerialNumber>.xml`, when you create the import job in the Azure portal.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cba23-160">後續步驟</span><span class="sxs-lookup"><span data-stu-id="cba23-160">Next steps</span></span>

* [<span data-ttu-id="cba23-161">針對匯入作業準備硬碟</span><span class="sxs-lookup"><span data-stu-id="cba23-161">Preparing hard drives for an import job</span></span>](../storage-import-export-tool-preparing-hard-drives-import.md)
* [<span data-ttu-id="cba23-162">常用命令快速參考</span><span class="sxs-lookup"><span data-stu-id="cba23-162">Quick reference for frequently used commands</span></span>](../storage-import-export-tool-quick-reference.md)
