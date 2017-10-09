---
title: "Azure 匯入/匯出匯出工作-v1 aaaPreviewing 磁碟機使用量 |Microsoft 文件"
description: "了解如何 toopreview hello 清單的 blob 您選取用於匯出工作 hello Azure 匯入/匯出服務中。"
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 7707d744-7ec7-4de8-ac9b-93a18608dc9a
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/15/2017
ms.author: muralikk
ms.openlocfilehash: 7378c159f6d11702cda9ae7654e84d85f9b671b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="previewing-drive-usage-for-an-export-job"></a>預覽匯出作業的磁碟機使用量
建立匯出工作之前，您會需要的 toochoose blob toobe 一組匯出。 hello Microsoft Azure 匯入/匯出服務可讓您 toouse 一份 blob 路徑或 blob 前置詞 toorepresent hello blob，您已選取。  
  
接下來，您需要 toodetermine 多少磁碟機需要 toosend。 hello 匯入/匯出工具提供 hello`PreviewExport`選取命令 toopreview 磁碟機使用量。 hello blob 時，根據 hello hello 磁碟機大小要 toouse。

## <a name="command-line-parameters"></a>命令列參數

您可以使用下列參數，當使用 hello hello `PreviewExport` hello 匯入/匯出工具的命令。

|命令列參數|說明|  
|--------------------------|-----------------|  
|**/logdir:**<LogDirectory\>|選用。 hello 記錄檔目錄。 詳細資訊記錄檔會寫入 toothis 目錄。 如果未不指定任何記錄檔目錄，則 hello 目前的目錄會用作 hello 記錄檔目錄。|  
|**/sn:**<StorageAccountName\>|必要。 hello 名稱 hello hello 儲存體帳戶匯出工作。|  
|**/sk:**<StorageAccountKey\>|如果未指定 (且只有在未指定) 容器 SAS 時，才是必要參數。 hello hello hello 的儲存體帳戶的帳戶金鑰匯出工作。|  
|**/csas:**<ContainerSas\>|如果未指定 (且只有在未指定) 儲存體帳戶金鑰時，才是必要參數。 用於列出 hello blob toobe hello 容器 SAS 匯出 hello 匯出工作。|  
|**/ExportBlobListFile:**<ExportBlobListFile\>|必要。 路徑 toohello XML 檔案包含清單的 blob 路徑或 blob 路徑前置詞 hello blob toobe 匯出。 hello 檔案格式用於 hello `BlobListBlobPath` hello 中的項目[Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) hello 匯入/匯出服務 REST API 的作業。|  
|**/DriveSize:**<DriveSize\>|必要。 hello 大小為匯出工作，如磁碟機 toouse*例如*，500GB、 1.5 t B。|  

## <a name="command-line-example"></a>命令列範例

hello 下列範例會示範 hello`PreviewExport`命令：  
  
```  
WAImportExport.exe PreviewExport /sn:bobmediaaccount /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /ExportBlobListFile:C:\WAImportExport\mybloblist.xml /DriveSize:500GB    
```  
  
hello 匯出 blob 清單檔案可能包含 blob 名稱和 blob 前置詞，如下所示：  
  
```xml 
<?xml version="1.0" encoding="utf-8"?>  
<BlobList>  
<BlobPath>pictures/animals/koala.jpg</BlobPath>  
<BlobPathPrefix>/vhds/</BlobPathPrefix>  
<BlobPathPrefix>/movies/</BlobPathPrefix>  
</BlobList>  
```

hello Azure 匯入/匯出工具會列出所有匯出的 blob toobe 和計算的 toopack hello 的磁碟機到指定大小，而不顧及任何必要的額外負荷，接著評估 hello 的磁碟機數目所需 toohold hello blob 和磁碟機使用情形資訊。  
  
Hello 輸出，以省略資訊的記錄檔的範例如下：  
  
```  
Number of unique blob paths/prefixes:   3  
Number of duplicate blob paths/prefixes:        0  
Number of nonexistent blob paths/prefixes:      1  
  
Drive size:     500.00 GB  
Number of blobs that can be exported:   6  
Number of blobs that cannot be exported:        2  
Number of drives needed:        3  
        Drive #1:       blobs = 1, occupied space = 454.74 GB  
        Drive #2:       blobs = 3, occupied space = 441.37 GB  
        Drive #3:       blobs = 2, occupied space = 131.28 GB    
```  
  
## <a name="next-steps"></a>後續步驟

* [Azure 匯入/匯出工具參考](../storage-import-export-tool-how-to-v1.md)
