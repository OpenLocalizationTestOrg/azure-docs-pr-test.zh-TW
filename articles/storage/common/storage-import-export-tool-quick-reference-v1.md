---
title: "Azure 匯入/匯出工具匯入作業命令 v1 aaaQuick 參考 |Microsoft 文件"
description: "適用於常用匯入作業命令的 Azure 匯入/匯出工具命令參考。 這是指 toov1 的 hello 匯入/匯出工具。"
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
ms.date: 01/15/2017
ms.author: muralikk
ms.openlocfilehash: 945eb4f9eff28c92ec963585d27cba73a7eb59bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="quick-reference-for-frequently-used-commands-for-import-jobs"></a>匯入作業的常用命令快速參考
本章節提供一些常用命令的快速參考。 如需詳細使用方式，請參閱[針對匯入作業準備硬碟](../storage-import-export-tool-preparing-hard-drives-import-v1.md)。  

## <a name="prepare-a-hard-drive-when-data-has-already-been-copied-toohello-hard-drive"></a>準備硬碟時已經過資料複製 toohello 硬碟機
 當資料已經複製的 tooit，但尚未以 BitLocker 加密，下列命令的 hello 準備硬碟機：  
  
```  
  WAImportExport.exe PrepImport /j:9WM35C2V.jrn /id:session#1 /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /t:d /encrypt /srcdir:d:\movies\drama /dstdir:movies/drama/ /skipwrite
```    

## <a name="copy-a-single-directory-tooa-hard-drive"></a>複製單一目錄 tooa 硬碟機  
 hello，下列命令會將複製的單一來源目錄 tooa 硬式磁碟機尚未以 BitLocker 加密：  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:movies /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:x /format /encrypt /srcdir:d:\Movies /dstdir:entertainment/movies/  
```  
  
## <a name="copy-two-directories-tooa-hard-drive"></a>複製兩個目錄 tooa 硬碟機  
 toocopy 兩個來源目錄 tooa 磁碟機，下列命令使用 hello:  
  
 hello 第一個命令會指定 hello 記錄檔目錄、 儲存體帳戶金鑰、 目標磁碟機代號，`format/encrypt`需求，以及一般參數：  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:movies /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:x /format /encrypt /srcdir:d:\Movies /dstdir:entertainment/movies/  
```  
  
 hello 第二個命令會指定 hello 日誌檔、 新的工作階段識別碼和 hello 來源和目的地位置：  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:music /srcdir:d:\Music /dstdir:entertainment/music/  
```  
  
## <a name="copy-a-large-file-tooa-hard-drive-in-a-second-copy-session"></a>在第二個複製工作階段複製大型檔案 tooa 硬碟機  
 hello，下列命令會將單一大型檔案 tooa 硬碟機的已備妥的前一個複製工作階段中︰  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:dvd /srcfile:d:\dvd\favoritemovie.vhd /dstblob:dvd/favoritemovie.vhd  
```  
  
## <a name="next-steps"></a>後續步驟

* [匯入工作的範例工作流程 tooprepare 硬碟機](storage-import-export-tool-sample-preparing-hard-drives-import-job-workflow-v1.md)
