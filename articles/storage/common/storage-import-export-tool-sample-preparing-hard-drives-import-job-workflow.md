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
ms.openlocfilehash: fa7f36300b35b81757523de4960fd583bd4bf305
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="sample-workflow-tooprepare-hard-drives-for-an-import-job"></a>匯入工作的範例工作流程 tooprepare 硬碟機

這篇文章會引導您完成 hello 完成程序來準備磁碟機匯入工作。

## <a name="sample-data"></a>範例資料

這個範例會匯入追蹤資料到 Azure 儲存體帳戶名稱的 hello `mystorageaccount`:

|位置|說明|資料大小|
|--------------|-----------------|-----|
|H:\Video\ |視訊集合|12 TB|
|H:\Photo\ |相片集合|30 GB|
|K:\Temp\FavoriteMovie.ISO|藍光 (Blu-Ray™) 磁碟映像|25 GB|
|\\\bigshare\john\music\|網路共用上的音樂檔案集合|10 GB|

## <a name="storage-account-destinations"></a>儲存體帳戶目的地

hello 匯入工作將 hello 將資料匯入下列目的地 hello 儲存體帳戶中的 hello:

|來源|目的地虛擬目錄或 Blob|
|------------|-------------------------------------------|
|H:\Video\ |video/|
|H:\Photo\ |photo/|
|K:\Temp\FavoriteMovie.ISO|favorite/FavoriteMovies.ISO|
|\\\bigshare\john\music\ |music|

透過此對應，hello 檔案`H:\Video\Drama\GreatMovie.mov`會匯入的 toohello blob `https://mystorageaccount.blob.core.windows.net/video/Drama/GreatMovie.mov`。

## <a name="determine-hard-drive-requirements"></a>判斷硬碟需求

下一步 toodetermine 需要多少硬碟機，則計算 hello hello 資料大小：

`12TB + 30GB + 25GB + 10GB = 12TB + 65GB`

針對此範例，兩個 8TB 的硬碟應該就已足夠。 不過，由於 hello 來源目錄`H:\Video`具有 12 TB 的資料，且您單一硬碟容量是 8 TB，您將無法 toospecify 這在下列方式 hello hello **driveset.csv**檔案：

```
DriveLetter,FormatOption,SilentOrPromptOnFormat,Encryption,ExistingBitLockerKey
X,Format,SilentMode,Encrypt,
Y,Format,SilentMode,Encrypt,
```
hello 工具會將資料分散在兩個硬碟以最佳化方式。

## <a name="attach-drives-and-configure-hello-job"></a>附加磁碟機，以及設定 hello 工作
您會將這兩個磁碟 toohello 機器附加並建立磁碟區。 然後撰寫 **dataset.csv** 檔案：
```
BasePath,DstBlobPathOrPrefix,BlobType,Disposition,MetadataFile,PropertiesFile
H:\Video\,video/,BlockBlob,rename,None,H:\mydirectory\properties.xml
H:\Photo\,photo/,BlockBlob,rename,None,H:\mydirectory\properties.xml
K:\Temp\FavoriteVideo.ISO,favorite/FavoriteVideo.ISO,BlockBlob,rename,None,H:\mydirectory\properties.xml
\\myshare\john\music\,music/,BlockBlob,rename,None,H:\mydirectory\properties.xml
```

此外，您可以設定下列中繼資料的所有檔案的 hello:

* **UploadMethod：**Windows Azure Import/Export service
* **DataSetName:** SampleData
* **CreationDate:** 10/1/2013

tooset hello 匯入檔案的中繼資料建立文字檔， `c:\WAImportExport\SampleMetadata.txt`，以下列內容的 hello:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Metadata>
    <UploadMethod>Windows Azure Import/Export service</UploadMethod>
    <DataSetName>SampleData</DataSetName>
    <CreationDate>10/1/2013</CreationDate>
</Metadata>
```

您也可以設定某些屬性 hello `FavoriteMovie.ISO` blob:

* **Content-Type:** application/octet-stream
* **Content-MD5:** Q2hlY2sgSW50ZWdyaXR5IQ==
* **Cache-Control:** no-cache

tooset 這些內容，請建立文字檔， `c:\WAImportExport\SampleProperties.txt`:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Properties>
    <Content-Type>application/octet-stream</Content-Type>
    <Content-MD5>Q2hlY2sgSW50ZWdyaXR5IQ==</Content-MD5>
    <Cache-Control>no-cache</Cache-Control>
</Properties>
```

## <a name="run-hello-azure-importexport-tool-waimportexportexe"></a>執行的 hello Azure 匯入/匯出工具 (WAImportExport.exe)

現在您已準備好 toorun hello Azure 匯入/匯出工具 tooprepare hello 兩個硬碟。

**Hello 第一個工作階段：**

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#1  /sk:************* /InitialDriveSet:driveset-1.csv /DataSet:dataset-1.csv /logdir:F:\logs
```

如果更多資料需要加入 toobe，建立另一個資料集檔案 （Initialdataset 與相同的格式）。

**Hello 第二個工作階段：**

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#2  /DataSet:dataset-2.csv
```

Hello 複製工作階段完成之後，您可以從 hello 複製電腦中斷連線 hello 兩部磁碟機，並將它們寄送 toohello 適當的 Azure 資料中心。 您要上傳 hello 兩個日誌檔，`<FirstDriveSerialNumber>.xml`和`<SecondDriveSerialNumber>.xml`，當您建立 hello Azure 入口網站中的 hello 匯入工作。

## <a name="next-steps"></a>後續步驟

* [針對匯入作業準備硬碟](../storage-import-export-tool-preparing-hard-drives-import.md)
* [常用命令快速參考](../storage-import-export-tool-quick-reference.md)
