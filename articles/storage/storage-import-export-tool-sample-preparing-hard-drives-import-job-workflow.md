---
title: "aaaSample 工作流程 tooprep 硬碟機的 Azure 匯入/匯出匯入作業 |Microsoft 文件"
description: "Hello hello Azure 匯入/匯出服務中匯入工作準備磁碟機的完整程序的逐步解說，請參閱。"
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
ms.openlocfilehash: 560220b7dc9f87416f1fec1ff30fa5cd65812ce5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="sample-workflow-tooprepare-hard-drives-for-an-import-job"></a><span data-ttu-id="4ecb3-103">匯入工作的範例工作流程 tooprepare 硬碟機</span><span class="sxs-lookup"><span data-stu-id="4ecb3-103">Sample workflow tooprepare hard drives for an import job</span></span>

<span data-ttu-id="4ecb3-104">這篇文章會引導您完成 hello 完成程序來準備磁碟機匯入工作。</span><span class="sxs-lookup"><span data-stu-id="4ecb3-104">This article walks you through hello complete process of preparing drives for an import job.</span></span>

## <a name="sample-data"></a><span data-ttu-id="4ecb3-105">範例資料</span><span class="sxs-lookup"><span data-stu-id="4ecb3-105">Sample data</span></span>

<span data-ttu-id="4ecb3-106">這個範例會匯入追蹤資料到 Azure 儲存體帳戶名稱的 hello `mystorageaccount`:</span><span class="sxs-lookup"><span data-stu-id="4ecb3-106">This example imports hello following data into an Azure storage account named `mystorageaccount`:</span></span>

|<span data-ttu-id="4ecb3-107">位置</span><span class="sxs-lookup"><span data-stu-id="4ecb3-107">Location</span></span>|<span data-ttu-id="4ecb3-108">說明</span><span class="sxs-lookup"><span data-stu-id="4ecb3-108">Description</span></span>|<span data-ttu-id="4ecb3-109">資料大小</span><span class="sxs-lookup"><span data-stu-id="4ecb3-109">Data size</span></span>|
|--------------|-----------------|-----|
|<span data-ttu-id="4ecb3-110">H:\Video\\</span><span class="sxs-lookup"><span data-stu-id="4ecb3-110">H:\Video\\</span></span> |<span data-ttu-id="4ecb3-111">視訊集合</span><span class="sxs-lookup"><span data-stu-id="4ecb3-111">A collection of videos</span></span>|<span data-ttu-id="4ecb3-112">12 TB</span><span class="sxs-lookup"><span data-stu-id="4ecb3-112">12 TB</span></span>|
|<span data-ttu-id="4ecb3-113">H:\Photo\\</span><span class="sxs-lookup"><span data-stu-id="4ecb3-113">H:\Photo\\</span></span> |<span data-ttu-id="4ecb3-114">相片集合</span><span class="sxs-lookup"><span data-stu-id="4ecb3-114">A collection of photos</span></span>|<span data-ttu-id="4ecb3-115">30 GB</span><span class="sxs-lookup"><span data-stu-id="4ecb3-115">30 GB</span></span>|
|<span data-ttu-id="4ecb3-116">K:\Temp\FavoriteMovie.ISO</span><span class="sxs-lookup"><span data-stu-id="4ecb3-116">K:\Temp\FavoriteMovie.ISO</span></span>|<span data-ttu-id="4ecb3-117">藍光 (Blu-Ray™) 磁碟映像</span><span class="sxs-lookup"><span data-stu-id="4ecb3-117">A Blu-Ray™ disk image</span></span>|<span data-ttu-id="4ecb3-118">25 GB</span><span class="sxs-lookup"><span data-stu-id="4ecb3-118">25 GB</span></span>|
|<span data-ttu-id="4ecb3-119">\\\bigshare\john\music\\</span><span class="sxs-lookup"><span data-stu-id="4ecb3-119">\\\bigshare\john\music\\</span></span>|<span data-ttu-id="4ecb3-120">網路共用上的音樂檔案集合</span><span class="sxs-lookup"><span data-stu-id="4ecb3-120">A collection of music files on a network share</span></span>|<span data-ttu-id="4ecb3-121">10 GB</span><span class="sxs-lookup"><span data-stu-id="4ecb3-121">10 GB</span></span>|

## <a name="storage-account-destinations"></a><span data-ttu-id="4ecb3-122">儲存體帳戶目的地</span><span class="sxs-lookup"><span data-stu-id="4ecb3-122">Storage account destinations</span></span>

<span data-ttu-id="4ecb3-123">hello 匯入工作將 hello 將資料匯入下列目的地 hello 儲存體帳戶中的 hello:</span><span class="sxs-lookup"><span data-stu-id="4ecb3-123">hello import job will import hello data into hello following destinations in hello storage account:</span></span>

|<span data-ttu-id="4ecb3-124">來源</span><span class="sxs-lookup"><span data-stu-id="4ecb3-124">Source</span></span>|<span data-ttu-id="4ecb3-125">目的地虛擬目錄或 Blob</span><span class="sxs-lookup"><span data-stu-id="4ecb3-125">Destination virtual directory or blob</span></span>|
|------------|-------------------------------------------|
|<span data-ttu-id="4ecb3-126">H:\Video\\</span><span class="sxs-lookup"><span data-stu-id="4ecb3-126">H:\Video\\</span></span> |<span data-ttu-id="4ecb3-127">video/</span><span class="sxs-lookup"><span data-stu-id="4ecb3-127">video/</span></span>|
|<span data-ttu-id="4ecb3-128">H:\Photo\\</span><span class="sxs-lookup"><span data-stu-id="4ecb3-128">H:\Photo\\</span></span> |<span data-ttu-id="4ecb3-129">photo/</span><span class="sxs-lookup"><span data-stu-id="4ecb3-129">photo/</span></span>|
|<span data-ttu-id="4ecb3-130">K:\Temp\FavoriteMovie.ISO</span><span class="sxs-lookup"><span data-stu-id="4ecb3-130">K:\Temp\FavoriteMovie.ISO</span></span>|<span data-ttu-id="4ecb3-131">favorite/FavoriteMovies.ISO</span><span class="sxs-lookup"><span data-stu-id="4ecb3-131">favorite/FavoriteMovies.ISO</span></span>|
|<span data-ttu-id="4ecb3-132">\\\bigshare\john\music\\</span><span class="sxs-lookup"><span data-stu-id="4ecb3-132">\\\bigshare\john\music\\</span></span> |<span data-ttu-id="4ecb3-133">music</span><span class="sxs-lookup"><span data-stu-id="4ecb3-133">music</span></span>|

<span data-ttu-id="4ecb3-134">透過此對應，hello 檔案`H:\Video\Drama\GreatMovie.mov`會匯入的 toohello blob `https://mystorageaccount.blob.core.windows.net/video/Drama/GreatMovie.mov`。</span><span class="sxs-lookup"><span data-stu-id="4ecb3-134">With this mapping, hello file `H:\Video\Drama\GreatMovie.mov` will be imported toohello blob `https://mystorageaccount.blob.core.windows.net/video/Drama/GreatMovie.mov`.</span></span>

## <a name="determine-hard-drive-requirements"></a><span data-ttu-id="4ecb3-135">判斷硬碟需求</span><span class="sxs-lookup"><span data-stu-id="4ecb3-135">Determine hard drive requirements</span></span>

<span data-ttu-id="4ecb3-136">下一步 toodetermine 需要多少硬碟機，則計算 hello hello 資料大小：</span><span class="sxs-lookup"><span data-stu-id="4ecb3-136">Next, toodetermine how many hard drives are needed, compute hello size of hello data:</span></span>

`12TB + 30GB + 25GB + 10GB = 12TB + 65GB`

<span data-ttu-id="4ecb3-137">針對此範例，兩個 8TB 的硬碟應該就已足夠。</span><span class="sxs-lookup"><span data-stu-id="4ecb3-137">For this example, two 8TB hard drives should be sufficient.</span></span> <span data-ttu-id="4ecb3-138">不過，由於 hello 來源目錄`H:\Video`具有 12 TB 的資料，且您單一硬碟容量是 8 TB，您將無法 toospecify 這在下列方式 hello hello **driveset.csv**檔案：</span><span class="sxs-lookup"><span data-stu-id="4ecb3-138">However, since hello source directory `H:\Video` has 12TB of data and your single hard drive's capacity is only 8TB, you will be able toospecify this in hello following way in hello **driveset.csv** file:</span></span>

```
DriveLetter,FormatOption,SilentOrPromptOnFormat,Encryption,ExistingBitLockerKey
X,Format,SilentMode,Encrypt,
Y,Format,SilentMode,Encrypt,
```
<span data-ttu-id="4ecb3-139">hello 工具會將資料分散在兩個硬碟以最佳化方式。</span><span class="sxs-lookup"><span data-stu-id="4ecb3-139">hello tool will distribute data across two hard drives in an optimized way.</span></span>

## <a name="attach-drives-and-configure-hello-job"></a><span data-ttu-id="4ecb3-140">附加磁碟機，以及設定 hello 工作</span><span class="sxs-lookup"><span data-stu-id="4ecb3-140">Attach drives and configure hello job</span></span>
<span data-ttu-id="4ecb3-141">您會將這兩個磁碟 toohello 機器附加並建立磁碟區。</span><span class="sxs-lookup"><span data-stu-id="4ecb3-141">You will attach both disks toohello machine and create volumes.</span></span> <span data-ttu-id="4ecb3-142">然後撰寫 **dataset.csv** 檔案：</span><span class="sxs-lookup"><span data-stu-id="4ecb3-142">Then author **dataset.csv** file:</span></span>
```
BasePath,DstBlobPathOrPrefix,BlobType,Disposition,MetadataFile,PropertiesFile
H:\Video\,video/,BlockBlob,rename,None,H:\mydirectory\properties.xml
H:\Photo\,photo/,BlockBlob,rename,None,H:\mydirectory\properties.xml
K:\Temp\FavoriteVideo.ISO,favorite/FavoriteVideo.ISO,BlockBlob,rename,None,H:\mydirectory\properties.xml
\\myshare\john\music\,music/,BlockBlob,rename,None,H:\mydirectory\properties.xml
```

<span data-ttu-id="4ecb3-143">此外，您可以設定下列中繼資料的所有檔案的 hello:</span><span class="sxs-lookup"><span data-stu-id="4ecb3-143">In addition, you can set hello following metadata for all files:</span></span>

* <span data-ttu-id="4ecb3-144">**UploadMethod：**Windows Azure Import/Export service</span><span class="sxs-lookup"><span data-stu-id="4ecb3-144">**UploadMethod:** Windows Azure Import/Export service</span></span>
* <span data-ttu-id="4ecb3-145">**DataSetName:** SampleData</span><span class="sxs-lookup"><span data-stu-id="4ecb3-145">**DataSetName:** SampleData</span></span>
* <span data-ttu-id="4ecb3-146">**CreationDate:** 10/1/2013</span><span class="sxs-lookup"><span data-stu-id="4ecb3-146">**CreationDate:** 10/1/2013</span></span>

<span data-ttu-id="4ecb3-147">tooset hello 匯入檔案的中繼資料建立文字檔， `c:\WAImportExport\SampleMetadata.txt`，以下列內容的 hello:</span><span class="sxs-lookup"><span data-stu-id="4ecb3-147">tooset metadata for hello imported files, create a text file, `c:\WAImportExport\SampleMetadata.txt`, with hello following content:</span></span>

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Metadata>
    <UploadMethod>Windows Azure Import/Export service</UploadMethod>
    <DataSetName>SampleData</DataSetName>
    <CreationDate>10/1/2013</CreationDate>
</Metadata>
```

<span data-ttu-id="4ecb3-148">您也可以設定某些屬性 hello `FavoriteMovie.ISO` blob:</span><span class="sxs-lookup"><span data-stu-id="4ecb3-148">You can also set some properties for hello `FavoriteMovie.ISO` blob:</span></span>

* <span data-ttu-id="4ecb3-149">**Content-Type:** application/octet-stream</span><span class="sxs-lookup"><span data-stu-id="4ecb3-149">**Content-Type:** application/octet-stream</span></span>
* <span data-ttu-id="4ecb3-150">**Content-MD5:** Q2hlY2sgSW50ZWdyaXR5IQ==</span><span class="sxs-lookup"><span data-stu-id="4ecb3-150">**Content-MD5:** Q2hlY2sgSW50ZWdyaXR5IQ==</span></span>
* <span data-ttu-id="4ecb3-151">**Cache-Control:** no-cache</span><span class="sxs-lookup"><span data-stu-id="4ecb3-151">**Cache-Control:** no-cache</span></span>

<span data-ttu-id="4ecb3-152">tooset 這些內容，請建立文字檔， `c:\WAImportExport\SampleProperties.txt`:</span><span class="sxs-lookup"><span data-stu-id="4ecb3-152">tooset these properties, create a text file, `c:\WAImportExport\SampleProperties.txt`:</span></span>

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Properties>
    <Content-Type>application/octet-stream</Content-Type>
    <Content-MD5>Q2hlY2sgSW50ZWdyaXR5IQ==</Content-MD5>
    <Cache-Control>no-cache</Cache-Control>
</Properties>
```

## <a name="run-hello-azure-importexport-tool-waimportexportexe"></a><span data-ttu-id="4ecb3-153">執行的 hello Azure 匯入/匯出工具 (WAImportExport.exe)</span><span class="sxs-lookup"><span data-stu-id="4ecb3-153">Run hello Azure Import/Export Tool (WAImportExport.exe)</span></span>

<span data-ttu-id="4ecb3-154">現在您已準備好 toorun hello Azure 匯入/匯出工具 tooprepare hello 兩個硬碟。</span><span class="sxs-lookup"><span data-stu-id="4ecb3-154">Now you are ready toorun hello Azure Import/Export Tool tooprepare hello two hard drives.</span></span>

<span data-ttu-id="4ecb3-155">**Hello 第一個工作階段：**</span><span class="sxs-lookup"><span data-stu-id="4ecb3-155">**For hello first session:**</span></span>

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#1  /sk:************* /InitialDriveSet:driveset-1.csv /DataSet:dataset-1.csv /logdir:F:\logs
```

<span data-ttu-id="4ecb3-156">如果更多資料需要加入 toobe，建立另一個資料集檔案 （Initialdataset 與相同的格式）。</span><span class="sxs-lookup"><span data-stu-id="4ecb3-156">If any more data needs toobe added, create another dataset file (same format as Initialdataset).</span></span>

<span data-ttu-id="4ecb3-157">**Hello 第二個工作階段：**</span><span class="sxs-lookup"><span data-stu-id="4ecb3-157">**For hello second session:**</span></span>

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#2  /DataSet:dataset-2.csv
```

<span data-ttu-id="4ecb3-158">Hello 複製工作階段完成之後，您可以從 hello 複製電腦中斷連線 hello 兩部磁碟機，並將它們寄送 toohello 適當的 Azure 資料中心。</span><span class="sxs-lookup"><span data-stu-id="4ecb3-158">Once hello copy sessions have completed, you can disconnect hello two drives from hello copy computer and ship them toohello appropriate Azure data center.</span></span> <span data-ttu-id="4ecb3-159">您要上傳 hello 兩個日誌檔，`<FirstDriveSerialNumber>.xml`和`<SecondDriveSerialNumber>.xml`，當您建立 hello Azure 入口網站中的 hello 匯入工作。</span><span class="sxs-lookup"><span data-stu-id="4ecb3-159">You'll upload hello two journal files, `<FirstDriveSerialNumber>.xml` and `<SecondDriveSerialNumber>.xml`, when you create hello import job in hello Azure portal.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4ecb3-160">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4ecb3-160">Next steps</span></span>

* [<span data-ttu-id="4ecb3-161">針對匯入作業準備硬碟</span><span class="sxs-lookup"><span data-stu-id="4ecb3-161">Preparing hard drives for an import job</span></span>](storage-import-export-tool-preparing-hard-drives-import.md)
* [<span data-ttu-id="4ecb3-162">常用命令快速參考</span><span class="sxs-lookup"><span data-stu-id="4ecb3-162">Quick reference for frequently used commands</span></span>](storage-import-export-tool-quick-reference.md)
