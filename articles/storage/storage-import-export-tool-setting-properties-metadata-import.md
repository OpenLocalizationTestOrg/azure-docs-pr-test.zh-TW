---
title: "aaaSetting 屬性和中繼資料，使用 Azure 匯入/匯出 |Microsoft 文件"
description: "了解如何 toospecify 屬性和中繼資料 toobe 設定 hello 目的地 blob 上執行您的磁碟機的 hello Azure 匯入/匯出工具 tooprepare 時。"
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
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: 05c2b13bead793c8ab5aac6ce25816be97fffb14
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="setting-properties-and-metadata-during-hello-import-process"></a><span data-ttu-id="fb141-103">設定屬性及 hello 期間的中繼資料匯入程序</span><span class="sxs-lookup"><span data-stu-id="fb141-103">Setting properties and metadata during hello import process</span></span>

<span data-ttu-id="fb141-104">當您執行 hello Microsoft Azure 匯入/匯出工具 tooprepare 您的磁碟機時，您可以指定屬性和中繼資料 toobe hello 目的地 blob 上設定。</span><span class="sxs-lookup"><span data-stu-id="fb141-104">When you run hello Microsoft Azure Import/Export Tool tooprepare your drives, you can specify properties and metadata toobe set on hello destination blobs.</span></span> <span data-ttu-id="fb141-105">請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="fb141-105">Follow these steps:</span></span>

1.  <span data-ttu-id="fb141-106">tooset blob 屬性，建立指定屬性名稱和值在本機電腦上的文字檔。</span><span class="sxs-lookup"><span data-stu-id="fb141-106">tooset blob properties, create a text file on your local computer that specifies property names and values.</span></span>
2.  <span data-ttu-id="fb141-107">tooset blob 中繼資料時，建立指定的中繼資料名稱和值在本機電腦上的文字檔。</span><span class="sxs-lookup"><span data-stu-id="fb141-107">tooset blob metadata, create a text file on your local computer that specifies metadata names and values.</span></span>
3.  <span data-ttu-id="fb141-108">Hello 一部分傳遞 hello 完整路徑 tooone 或多個這些檔案 toohello Azure 匯入/匯出工具`PrepImport`作業。</span><span class="sxs-lookup"><span data-stu-id="fb141-108">Pass hello full path tooone or both of these files toohello Azure Import/Export Tool as part of hello `PrepImport` operation.</span></span>

> [!NOTE]
>  <span data-ttu-id="fb141-109">當您指定屬性或中繼資料檔案做為複製工作階段的一部分時，會設定每個做為該複製工作階段一部分的 blob 之屬性或中繼資料。</span><span class="sxs-lookup"><span data-stu-id="fb141-109">When you specify a properties or metadata file as part of a copy session, those properties or metadata are set for every blob that is imported as part of that copy session.</span></span> <span data-ttu-id="fb141-110">如果您正在匯入的 hello blob 的某些想 toospecify 一組不同的屬性或中繼資料，您將需要的 toocreate 個別複製工作階段不同的屬性或中繼資料檔案。</span><span class="sxs-lookup"><span data-stu-id="fb141-110">If you want toospecify a different set of properties or metadata for some of hello blobs being imported, you'll need toocreate a separate copy session with different properties or metadata files.</span></span>

## <a name="specify-blob-properties-in-a-text-file"></a><span data-ttu-id="fb141-111">在文字檔案中指定 blob 屬性</span><span class="sxs-lookup"><span data-stu-id="fb141-111">Specify blob properties in a text file</span></span>

<span data-ttu-id="fb141-112">toospecify blob 屬性，建立本機文字檔，並包含指定屬性名稱做為元素、 屬性值做為值的 XML。</span><span class="sxs-lookup"><span data-stu-id="fb141-112">toospecify blob properties, create a local text file, and include XML that specifies property names as elements, and property values as values.</span></span> <span data-ttu-id="fb141-113">以下是指定一些屬性值的範例︰</span><span class="sxs-lookup"><span data-stu-id="fb141-113">Here's an example that specifies some property values:</span></span>

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Properties>
    <Content-Type>application/octet-stream</Content-Type>
    <Content-MD5>Q2hlY2sgSW50ZWdyaXR5IQ==</Content-MD5>
    <Cache-Control>no-cache</Cache-Control>
</Properties>
```

<span data-ttu-id="fb141-114">儲存 hello 檔案 tooa 本機位置，例如`C:\WAImportExport\ImportProperties.txt`。</span><span class="sxs-lookup"><span data-stu-id="fb141-114">Save hello file tooa local location like `C:\WAImportExport\ImportProperties.txt`.</span></span>

## <a name="specify-blob-metadata-in-a-text-file"></a><span data-ttu-id="fb141-115">指定文字檔案中的 blob 中繼資料</span><span class="sxs-lookup"><span data-stu-id="fb141-115">Specify blob metadata in a text file</span></span>

<span data-ttu-id="fb141-116">同樣地，toospecify blob 中繼資料，並建立本機文字檔，指定中繼資料名稱做為項目，並做為值的中繼資料值。</span><span class="sxs-lookup"><span data-stu-id="fb141-116">Similarly, toospecify blob metadata, create a local text file that specifies metadata names as elements, and metadata values as values.</span></span> <span data-ttu-id="fb141-117">以下是指定一些中繼資料值的範例︰</span><span class="sxs-lookup"><span data-stu-id="fb141-117">Here's an example that specifies some metadata values:</span></span>

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Metadata>
    <UploadMethod>Windows Azure Import/Export service</UploadMethod>
    <DataSetName>SampleData</DataSetName>
    <CreationDate>10/1/2013</CreationDate>
</Metadata>
```

<span data-ttu-id="fb141-118">儲存 hello 檔案 tooa 本機位置，例如`C:\WAImportExport\ImportMetadata.txt`。</span><span class="sxs-lookup"><span data-stu-id="fb141-118">Save hello file tooa local location like `C:\WAImportExport\ImportMetadata.txt`.</span></span>

## <a name="add-hello-path-tooproperties-and-metadata-files-in-datasetcsv"></a><span data-ttu-id="fb141-119">加入在 dataset.csv hello 路徑 tooproperties 和中繼資料檔案</span><span class="sxs-lookup"><span data-stu-id="fb141-119">Add hello path tooproperties and metadata files in dataset.csv</span></span>

```
BasePath,DstBlobPathOrPrefix,BlobType,Disposition,MetadataFile,PropertiesFile
H:\Video\,https://mystorageaccount.blob.core.windows.net/video/,BlockBlob,rename,None,H:\mydirectory\properties.xml
H:\Photo\,https://mystorageaccount.blob.core.windows.net/photo/,BlockBlob,rename,None,H:\mydirectory\properties.xml
K:\Temp\FavoriteVideo.ISO,https://mystorageaccount.blob.core.windows.net/favorite/FavoriteVideo.ISO,BlockBlob,rename,None,H:\mydirectory\properties.xml
\\myshare\john\music\,https://mystorageaccount.blob.core.windows.net/music/,BlockBlob,rename,None,H:\mydirectory\properties.xml
```

## <a name="next-steps"></a><span data-ttu-id="fb141-120">後續步驟</span><span class="sxs-lookup"><span data-stu-id="fb141-120">Next steps</span></span>

* [<span data-ttu-id="fb141-121">匯入/匯出服務中繼資料和屬性檔案格式</span><span class="sxs-lookup"><span data-stu-id="fb141-121">Import/Export service metadata and properties file format</span></span>](storage-import-export-file-format-metadata-and-properties.md)
