---
title: "使用 Azure 匯入/匯出來設定屬性和中繼資料 | Microsoft Docs"
description: "了解執行 Azure 匯入/匯出工具準備磁碟機時，如何指定要在目的地 blob 上設定的屬性和中繼資料。"
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
ms.openlocfilehash: bdc7a53f82d1fbbb726e2b1bd5d96678a8563566
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="setting-properties-and-metadata-during-the-import-process"></a><span data-ttu-id="12874-103">在匯入程序期間設定屬性和中繼資料</span><span class="sxs-lookup"><span data-stu-id="12874-103">Setting properties and metadata during the import process</span></span>

<span data-ttu-id="12874-104">當您執行 Microsoft Azure 匯入/匯出工具準備磁碟機時，可以指定要在目的地 blob 上設定的屬性和中繼資料。</span><span class="sxs-lookup"><span data-stu-id="12874-104">When you run the Microsoft Azure Import/Export Tool to prepare your drives, you can specify properties and metadata to be set on the destination blobs.</span></span> <span data-ttu-id="12874-105">請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="12874-105">Follow these steps:</span></span>

1.  <span data-ttu-id="12874-106">若要設定 blob 屬性，建立本機電腦上指定屬性名稱和值的文字檔案。</span><span class="sxs-lookup"><span data-stu-id="12874-106">To set blob properties, create a text file on your local computer that specifies property names and values.</span></span>
2.  <span data-ttu-id="12874-107">若要設定 blob 中繼資料，建立本機電腦上指定中繼資料名稱和值的文字檔案。</span><span class="sxs-lookup"><span data-stu-id="12874-107">To set blob metadata, create a text file on your local computer that specifies metadata names and values.</span></span>
3.  <span data-ttu-id="12874-108">將完整路徑傳遞至一或兩個 Azure 匯入/匯出工具，做為 `PrepImport` 作業的一部分。</span><span class="sxs-lookup"><span data-stu-id="12874-108">Pass the full path to one or both of these files to the Azure Import/Export Tool as part of the `PrepImport` operation.</span></span>

> [!NOTE]
>  <span data-ttu-id="12874-109">當您指定屬性或中繼資料檔案做為複製工作階段的一部分時，會設定每個做為該複製工作階段一部分的 blob 之屬性或中繼資料。</span><span class="sxs-lookup"><span data-stu-id="12874-109">When you specify a properties or metadata file as part of a copy session, those properties or metadata are set for every blob that is imported as part of that copy session.</span></span> <span data-ttu-id="12874-110">如果您想要指定要匯入之 blob 部分的一組不同的屬性或中繼資料，您必須使用不同的屬性或中繼資料檔案建立個別複製工作階段。</span><span class="sxs-lookup"><span data-stu-id="12874-110">If you want to specify a different set of properties or metadata for some of the blobs being imported, you'll need to create a separate copy session with different properties or metadata files.</span></span>

## <a name="specify-blob-properties-in-a-text-file"></a><span data-ttu-id="12874-111">在文字檔案中指定 blob 屬性</span><span class="sxs-lookup"><span data-stu-id="12874-111">Specify blob properties in a text file</span></span>

<span data-ttu-id="12874-112">若要指定 blob 屬性，建立本機文字檔，並包含指定屬性名稱做為元素的 XML 以及做為值的屬性值。</span><span class="sxs-lookup"><span data-stu-id="12874-112">To specify blob properties, create a local text file, and include XML that specifies property names as elements, and property values as values.</span></span> <span data-ttu-id="12874-113">以下是指定一些屬性值的範例︰</span><span class="sxs-lookup"><span data-stu-id="12874-113">Here's an example that specifies some property values:</span></span>

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Properties>
    <Content-Type>application/octet-stream</Content-Type>
    <Content-MD5>Q2hlY2sgSW50ZWdyaXR5IQ==</Content-MD5>
    <Cache-Control>no-cache</Cache-Control>
</Properties>
```

<span data-ttu-id="12874-114">將檔案儲存至本機位置，例如 `C:\WAImportExport\ImportProperties.txt`。</span><span class="sxs-lookup"><span data-stu-id="12874-114">Save the file to a local location like `C:\WAImportExport\ImportProperties.txt`.</span></span>

## <a name="specify-blob-metadata-in-a-text-file"></a><span data-ttu-id="12874-115">指定文字檔案中的 blob 中繼資料</span><span class="sxs-lookup"><span data-stu-id="12874-115">Specify blob metadata in a text file</span></span>

<span data-ttu-id="12874-116">同樣地，若要指定 blob 中繼資料，建立指定中繼資料名稱做為項目的本機文字檔，以及做為值的中繼資料值。</span><span class="sxs-lookup"><span data-stu-id="12874-116">Similarly, to specify blob metadata, create a local text file that specifies metadata names as elements, and metadata values as values.</span></span> <span data-ttu-id="12874-117">以下是指定一些中繼資料值的範例︰</span><span class="sxs-lookup"><span data-stu-id="12874-117">Here's an example that specifies some metadata values:</span></span>

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Metadata>
    <UploadMethod>Windows Azure Import/Export service</UploadMethod>
    <DataSetName>SampleData</DataSetName>
    <CreationDate>10/1/2013</CreationDate>
</Metadata>
```

<span data-ttu-id="12874-118">將檔案儲存至本機位置，例如 `C:\WAImportExport\ImportMetadata.txt`。</span><span class="sxs-lookup"><span data-stu-id="12874-118">Save the file to a local location like `C:\WAImportExport\ImportMetadata.txt`.</span></span>

## <a name="add-the-path-to-properties-and-metadata-files-in-datasetcsv"></a><span data-ttu-id="12874-119">在 dataset.csv 中新增屬性和中繼資料檔案的路徑</span><span class="sxs-lookup"><span data-stu-id="12874-119">Add the path to properties and metadata files in dataset.csv</span></span>

```
BasePath,DstBlobPathOrPrefix,BlobType,Disposition,MetadataFile,PropertiesFile
H:\Video\,https://mystorageaccount.blob.core.windows.net/video/,BlockBlob,rename,None,H:\mydirectory\properties.xml
H:\Photo\,https://mystorageaccount.blob.core.windows.net/photo/,BlockBlob,rename,None,H:\mydirectory\properties.xml
K:\Temp\FavoriteVideo.ISO,https://mystorageaccount.blob.core.windows.net/favorite/FavoriteVideo.ISO,BlockBlob,rename,None,H:\mydirectory\properties.xml
\\myshare\john\music\,https://mystorageaccount.blob.core.windows.net/music/,BlockBlob,rename,None,H:\mydirectory\properties.xml
```

## <a name="next-steps"></a><span data-ttu-id="12874-120">後續步驟</span><span class="sxs-lookup"><span data-stu-id="12874-120">Next steps</span></span>

* [<span data-ttu-id="12874-121">匯入/匯出服務中繼資料和屬性檔案格式</span><span class="sxs-lookup"><span data-stu-id="12874-121">Import/Export service metadata and properties file format</span></span>](storage-import-export-file-format-metadata-and-properties.md)
