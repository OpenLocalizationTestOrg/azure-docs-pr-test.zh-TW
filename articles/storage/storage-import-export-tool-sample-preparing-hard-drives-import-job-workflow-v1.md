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
ms.openlocfilehash: f836fc6104d8b4ad5660cb110a62f61b40b0b7ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="sample-workflow-tooprepare-hard-drives-for-an-import-job"></a>匯入工作的範例工作流程 tooprepare 硬碟機
本主題會引導您完成 hello 完成程序來準備磁碟機匯入工作。  
  
這個範例會匯入至 Window Azure 儲存體帳戶名稱為下列資料的 hello `mystorageaccount`:  
  
|位置|說明|  
|--------------|-----------------|  
|H:\Video|視訊集合，總共 5 TB。|  
|H:\Photo|相片集合，總共 30 GB。|  
|K:\Temp\FavoriteMovie.ISO|藍光 (Blu-Ray™) 磁碟映像，25 GB。|  
|\\\bigshare\john\music|網路共用上的音樂檔案集合，總共 10 GB。|  
  
hello 匯入工作會將此資料匯入到下列目的地 hello 儲存體帳戶中的 hello:  
  
|來源|目的地虛擬目錄或 Blob|  
|------------|-------------------------------------------|  
|H:\Video|https://mystorageaccount.blob.core.windows.net/video|  
|H:\Photo|https://mystorageaccount.blob.core.windows.net/photo|  
|K:\Temp\FavoriteMovie.ISO|https://mystorageaccount.blob.core.windows.net/favorite/FavoriteMovies.ISO|  
|\\\bigshare\john\music|https://mystorageaccount.blob.core.windows.net/music|  
  
透過此對應，hello 檔案`H:\Video\Drama\GreatMovie.mov`會匯入的 toohello blob `https://mystorageaccount.blob.core.windows.net/video/Drama/GreatMovie.mov`。  
  
下一步 toodetermine 需要多少硬碟機，則計算 hello hello 資料大小：  
  
`5TB + 30GB + 25GB + 10GB = 5TB + 65GB`  
  
針對此範例，兩個 3TB 的硬碟應該就已足夠。 不過，由於 hello 來源目錄`H:\Video`擁有 5TB 的資料，而您單一硬碟容量只有 3TB，它是必要的 toobreak`H:\Video`分割成兩個較小的目錄，再執行 hello Microsoft Azure 匯入/匯出工具： `H:\Video1`和`H:\Video2`。 此步驟會產生下列來源目錄的 hello:  
  
|位置|大小|目的地虛擬目錄或 Blob|  
|--------------|----------|-------------------------------------------|  
|H:\Video1|2.5TB|https://mystorageaccount.blob.core.windows.net/video|  
|H:\Video2|2.5TB|https://mystorageaccount.blob.core.windows.net/video|  
|H:\Photo|30GB|https://mystorageaccount.blob.core.windows.net/photo|  
|K:\Temp\FavoriteMovies.ISO|25GB|https://mystorageaccount.blob.core.windows.net/favorite/FavoriteMovies.ISO|  
|\\\bigshare\john\music|10GB|https://mystorageaccount.blob.core.windows.net/music|  
  
 請注意，即使 hello`H:\Video`目錄已分割 tootwo 目錄、 其點 toohello hello 儲存體帳戶中的同一個目的地虛擬目錄。 如此一來，所有視訊檔案會維護的單一`video`hello 儲存體帳戶中的容器。  
  
 接下來，上述來源目錄都是平均 hello 分散式 toohello 兩個硬碟：  
  
||||  
|-|-|-|  
|硬碟|來源目錄|總大小|  
|第一個硬碟|H:\Video1|2.5TB + 30GB|  
||H:\Photo||  
|第二個硬碟|H:\Video2|2.5TB + 35GB|  
||K:\Temp\BlueRay.ISO||  
||\\\bigshare\john\music||  
  
此外，您可以設定下列中繼資料的所有檔案的 hello:  
  
-   **UploadMethod：**Windows Azure Import/Export service  
  
-   **DataSetName:** SampleData  
  
-   **CreationDate:** 10/1/2013  
  
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
  
-   **Content-Type:** application/octet-stream  
  
-   **Content-MD5:** Q2hlY2sgSW50ZWdyaXR5IQ==  
  
-   **Cache-Control:** no-cache  
  
tooset 這些內容，請建立文字檔， `c:\WAImportExport\SampleProperties.txt`:  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<Properties>  
    <Content-Type>application/octet-stream</Content-Type>  
    <Content-MD5>Q2hlY2sgSW50ZWdyaXR5IQ==</Content-MD5>  
    <Cache-Control>no-cache</Cache-Control>  
</Properties>  
```
  
現在您已準備好 toorun hello Azure 匯入/匯出工具 tooprepare hello 兩個硬碟。 請注意：  
  
-   hello 第一個磁碟機裝載為磁碟機 X。  
  
-   hello 第二個磁碟機裝載為磁碟機 Y。  
  
-   hello 儲存體帳戶的 hello 金鑰`mystorageaccount`是`8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg==`。  

## <a name="preparing-disk-for-import-when-data-is-pre-loaded"></a>在資料已預先載入時針對匯入準備磁碟
 
 如果 hello 資料 toobe 匯入已存在於 hello 磁碟上，使用 hello 旗標 /skipwrite。 /T 和 /srcdir 的值應該指向 toohello 磁碟在準備用來匯入。 如果不是所有 hello 資料上 hello 磁碟需要 toogo toohello 相同的目的地虛擬目錄或 hello 儲存體帳戶，執行 hello 相同命令分別將 /id hello 值保持在每個目錄的根目錄跨所有執行相同。

>[!NOTE] 
>請勿指定 /format，因為它將會抹除 hello 資料 hello 磁碟上。 您可以指定 / 加密或 /bk 根據是否 hello 磁碟已加密。 
>

```
    When data is already present on hello disk for each drive run hello following command.
    WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:Video1 /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:x /format /encrypt /srcdir:x:\Video1 /dstdir:video/ /MetadataFile:c:\WAImportExport\SampleMetadata.txt /skipwrite
```

## <a name="copy-sessions---first-drive"></a>複製工作階段 - 第一個硬碟

Hello 第一個磁碟機會執行 hello Azure 匯入/匯出工具兩次 toocopy hello 兩個來源目錄：  

**第一個複製工作階段**
  
```
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:Video1 /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:x /format /encrypt /srcdir:H:\Video1 /dstdir:video/ /MetadataFile:c:\WAImportExport\SampleMetadata.txt  
```

**第二個複製工作階段**

```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:Photo /srcdir:H:\Photo /dstdir:photo/ /MetadataFile:c:\WAImportExport\SampleMetadata.txt
```

## <a name="copy-sessions---second-drive"></a>複製工作階段 - 第二個硬碟
 
Hello 第二個磁碟機，執行 hello Azure 匯入/匯出工具三次之後每個 hello 來源目錄，並一次針對 hello 獨立 Blu-Ray™ 影像檔,):  
  
**第一個複製工作階段** 

```
WAImportExport.exe PrepImport /j:SecondDrive.jrn /id:Video2 /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:y /format /encrypt /srcdir:H:\Video2 /dstdir:video/ /MetadataFile:c:\WAImportExport\SampleMetadata.txt  
```
  
**第二個複製工作階段**

```
WAImportExport.exe PrepImport /j:SecondDrive.jrn /id:Music /srcdir:\\bigshare\john\music /dstdir:music/ /MetadataFile:c:\WAImportExport\SampleMetadata.txt  
```  
  
**第三個複製工作階段**  

```
WAImportExport.exe PrepImport /j:SecondDrive.jrn /id:BlueRayIso /srcfile:K:\Temp\BlueRay.ISO /dstblob:favorite/BlueRay.ISO /MetadataFile:c:\WAImportExport\SampleMetadata.txt /PropertyFile:c:\WAImportExport\SampleProperties.txt  
```

## <a name="copy-session-completion"></a>複製工作階段完成

Hello 複製工作階段完成之後，您可以從 hello 複製電腦中斷連線 hello 兩部磁碟機，並將它們寄送 toohello 適當的 Windows Azure 資料中心。 您要上傳 hello 兩個日誌檔，`FirstDrive.jrn`和`SecondDrive.jrn`，當您建立可在 hello hello 匯入作業[Windows Azure 管理入口網站](https://manage.windowsazure.com/)。  
  
## <a name="next-steps"></a>後續步驟

* [針對匯入作業準備硬碟](storage-import-export-tool-preparing-hard-drives-import-v1.md)   
* [常用命令快速參考](storage-import-export-tool-quick-reference-v1.md) 
