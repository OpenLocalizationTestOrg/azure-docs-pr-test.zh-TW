---
title: "aaaSetting 屬性和中繼資料，使用 Azure 匯入/匯出-v1 |Microsoft 文件"
description: "了解如何 toospecify 屬性和中繼資料 toobe 設定 hello 目的地 blob 上執行您的磁碟機的 hello Azure 匯入/匯出工具 tooprepare 時。 這是指 toov1 的 hello 匯入/匯出工具。"
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: e8541695-bcfb-4bf0-84d9-72c9de32a0a8
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: 66e55c2076fbcda9b78302f17b5ff2cf96bb24e7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="setting-properties-and-metadata-during-hello-import-process"></a>設定屬性及 hello 期間的中繼資料匯入程序
當您執行 hello Microsoft Azure 匯入/匯出工具 tooprepare 您的磁碟機時，您可以指定屬性和中繼資料 toobe hello 目的地 blob 上設定。 請遵循下列步驟：  
  
1.  tooset blob 屬性，建立指定屬性名稱和值在本機電腦上的文字檔。  
  
2.  tooset blob 中繼資料時，建立指定的中繼資料名稱和值在本機電腦上的文字檔。  
  
3.  Hello 一部分傳遞 hello 完整路徑 tooone 或多個這些檔案 toohello Azure 匯入/匯出工具`PrepImport`作業。  
  
> [!NOTE]
>  當您指定屬性或中繼資料檔案做為複製工作階段的一部分時，會設定每個做為該複製工作階段一部分的 blob 之屬性或中繼資料。 如果您正在匯入的 hello blob 的某些想 toospecify 一組不同的屬性或中繼資料，您將需要的 toocreate 個別複製工作階段不同的屬性或中繼資料檔案。  
  
## <a name="specify-blob-properties-in-a-text-file"></a>在文字檔案中指定 blob 屬性  
toospecify blob 屬性，建立本機文字檔，並包含指定屬性名稱做為元素、 屬性值做為值的 XML。 以下是指定一些屬性值的範例︰  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<Properties>  
    <Content-Type>application/octet-stream</Content-Type>  
    <Content-MD5>Q2hlY2sgSW50ZWdyaXR5IQ==</Content-MD5>  
    <Cache-Control>no-cache</Cache-Control>  
</Properties>  
```
  
儲存 hello 檔案 tooa 本機位置，例如`C:\WAImportExport\ImportProperties.txt`。  
  
## <a name="specify-blob-metadata-in-a-text-file"></a>在文字檔案中指定 blob 中繼資料  
同樣地，toospecify blob 中繼資料，並建立本機文字檔，指定中繼資料名稱做為項目，並做為值的中繼資料值。 以下是指定一些中繼資料值的範例︰  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<Metadata>  
    <UploadMethod>Windows Azure Import/Export service</UploadMethod>  
    <DataSetName>SampleData</DataSetName>  
    <CreationDate>10/1/2013</CreationDate>  
</Metadata>  
```
  
儲存 hello 檔案 tooa 本機位置，例如`C:\WAImportExport\ImportMetadata.txt`。  
  
## <a name="create-a-copy-session-including-hello-properties-or-metadata-files"></a>建立複製工作階段包括 hello 屬性或中繼資料檔案  
當您執行 hello Azure 匯入/匯出工具 tooprepare hello 匯入工作時，hello 屬性上指定檔案 hello 命令列使用 hello`PropertyFile`參數。 指定使用 hello hello 命令列上的 hello 中繼資料檔`/MetadataFile`參數。 以下是指定這兩種檔案的範例︰  
  
```
WAImportExport.exe PrepImport /j:SecondDrive.jrn /id:BlueRayIso /srcfile:K:\Temp\BlueRay.ISO /dstblob:favorite/BlueRay.ISO /MetadataFile:c:\WAImportExport\SampleMetadata.txt /PropertyFile:c:\WAImportExport\SampleProperties.txt  
```
  
## <a name="next-steps"></a>後續步驟

* [匯入/匯出服務中繼資料和屬性檔案格式](storage-import-export-file-format-metadata-and-properties.md)
