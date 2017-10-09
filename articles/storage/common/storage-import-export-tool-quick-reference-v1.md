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
# <a name="quick-reference-for-frequently-used-commands-for-import-jobs"></a><span data-ttu-id="7a382-104">匯入作業的常用命令快速參考</span><span class="sxs-lookup"><span data-stu-id="7a382-104">Quick reference for frequently used commands for import jobs</span></span>
<span data-ttu-id="7a382-105">本章節提供一些常用命令的快速參考。</span><span class="sxs-lookup"><span data-stu-id="7a382-105">This section provides a quick reference for some frequently used commands.</span></span> <span data-ttu-id="7a382-106">如需詳細使用方式，請參閱[針對匯入作業準備硬碟](../storage-import-export-tool-preparing-hard-drives-import-v1.md)。</span><span class="sxs-lookup"><span data-stu-id="7a382-106">For detailed usage, see [Preparing Hard Drives for an Import Job](../storage-import-export-tool-preparing-hard-drives-import-v1.md).</span></span>  

## <a name="prepare-a-hard-drive-when-data-has-already-been-copied-toohello-hard-drive"></a><span data-ttu-id="7a382-107">準備硬碟時已經過資料複製 toohello 硬碟機</span><span class="sxs-lookup"><span data-stu-id="7a382-107">Prepare a hard drive when data has already been copied toohello hard drive</span></span>
 <span data-ttu-id="7a382-108">當資料已經複製的 tooit，但尚未以 BitLocker 加密，下列命令的 hello 準備硬碟機：</span><span class="sxs-lookup"><span data-stu-id="7a382-108">hello following command prepares a hard drive when data has already been copied tooit, but has not yet been encrypted with BitLocker:</span></span>  
  
```  
  WAImportExport.exe PrepImport /j:9WM35C2V.jrn /id:session#1 /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /t:d /encrypt /srcdir:d:\movies\drama /dstdir:movies/drama/ /skipwrite
```    

## <a name="copy-a-single-directory-tooa-hard-drive"></a><span data-ttu-id="7a382-109">複製單一目錄 tooa 硬碟機</span><span class="sxs-lookup"><span data-stu-id="7a382-109">Copy a single directory tooa hard drive</span></span>  
 <span data-ttu-id="7a382-110">hello，下列命令會將複製的單一來源目錄 tooa 硬式磁碟機尚未以 BitLocker 加密：</span><span class="sxs-lookup"><span data-stu-id="7a382-110">hello following command copies a single source directory tooa hard drive that has not yet been encrypted with BitLocker:</span></span>  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:movies /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:x /format /encrypt /srcdir:d:\Movies /dstdir:entertainment/movies/  
```  
  
## <a name="copy-two-directories-tooa-hard-drive"></a><span data-ttu-id="7a382-111">複製兩個目錄 tooa 硬碟機</span><span class="sxs-lookup"><span data-stu-id="7a382-111">Copy two directories tooa hard drive</span></span>  
 <span data-ttu-id="7a382-112">toocopy 兩個來源目錄 tooa 磁碟機，下列命令使用 hello:</span><span class="sxs-lookup"><span data-stu-id="7a382-112">toocopy two source directories tooa drive, use hello following commands:</span></span>  
  
 <span data-ttu-id="7a382-113">hello 第一個命令會指定 hello 記錄檔目錄、 儲存體帳戶金鑰、 目標磁碟機代號，`format/encrypt`需求，以及一般參數：</span><span class="sxs-lookup"><span data-stu-id="7a382-113">hello first command specifies hello log directory, storage account key, target drive letter, `format/encrypt` requirements, and common parameters:</span></span>  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:movies /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:x /format /encrypt /srcdir:d:\Movies /dstdir:entertainment/movies/  
```  
  
 <span data-ttu-id="7a382-114">hello 第二個命令會指定 hello 日誌檔、 新的工作階段識別碼和 hello 來源和目的地位置：</span><span class="sxs-lookup"><span data-stu-id="7a382-114">hello second command specifies hello journal file, a new session ID, and hello source and destination locations:</span></span>  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:music /srcdir:d:\Music /dstdir:entertainment/music/  
```  
  
## <a name="copy-a-large-file-tooa-hard-drive-in-a-second-copy-session"></a><span data-ttu-id="7a382-115">在第二個複製工作階段複製大型檔案 tooa 硬碟機</span><span class="sxs-lookup"><span data-stu-id="7a382-115">Copy a large file tooa hard drive in a second copy session</span></span>  
 <span data-ttu-id="7a382-116">hello，下列命令會將單一大型檔案 tooa 硬碟機的已備妥的前一個複製工作階段中︰</span><span class="sxs-lookup"><span data-stu-id="7a382-116">hello following command copies a single large file tooa hard drive that was prepared in a previous copy session:</span></span>  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:dvd /srcfile:d:\dvd\favoritemovie.vhd /dstblob:dvd/favoritemovie.vhd  
```  
  
## <a name="next-steps"></a><span data-ttu-id="7a382-117">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7a382-117">Next steps</span></span>

* [<span data-ttu-id="7a382-118">匯入工作的範例工作流程 tooprepare 硬碟機</span><span class="sxs-lookup"><span data-stu-id="7a382-118">Sample workflow tooprepare hard drives for an import job</span></span>](storage-import-export-tool-sample-preparing-hard-drives-import-job-workflow-v1.md)
