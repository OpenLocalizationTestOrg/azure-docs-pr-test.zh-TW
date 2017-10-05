---
title: "Azure 匯入/匯出工具匯入作業命令的快速參考 - v1 | Microsoft Docs"
description: "適用於常用匯入作業命令的 Azure 匯入/匯出工具命令參考。 這是指 v1 的匯入/匯出工具。"
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
ms.openlocfilehash: 47f450ee87dac3db2ccf7659928d52a6330a5697
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="quick-reference-for-frequently-used-commands-for-import-jobs"></a><span data-ttu-id="7277d-104">匯入作業的常用命令快速參考</span><span class="sxs-lookup"><span data-stu-id="7277d-104">Quick reference for frequently used commands for import jobs</span></span>
<span data-ttu-id="7277d-105">本章節提供一些常用命令的快速參考。</span><span class="sxs-lookup"><span data-stu-id="7277d-105">This section provides a quick references for some frequently used commands.</span></span> <span data-ttu-id="7277d-106">如需詳細使用方式，請參閱[針對匯入作業準備硬碟](storage-import-export-tool-preparing-hard-drives-import-v1.md)。</span><span class="sxs-lookup"><span data-stu-id="7277d-106">For detailed usage, see [Preparing Hard Drives for an Import Job](storage-import-export-tool-preparing-hard-drives-import-v1.md).</span></span>  

## <a name="prepare-the-disks-when-data-already-copied-to-the-disks"></a><span data-ttu-id="7277d-107">當資料已複製到磁碟時準備磁碟</span><span class="sxs-lookup"><span data-stu-id="7277d-107">Prepare the disks when data already copied to the disks</span></span>
 <span data-ttu-id="7277d-108">這是已將資料複製到尚未使用 BitLocker 加密的硬碟時，用來準備磁碟的範例命令︰</span><span class="sxs-lookup"><span data-stu-id="7277d-108">Here is a sample command to prepare a disks when data already copied to the hard drive that hasn't been yet been encrypted with BitLocker:</span></span>  
  
```  
  WAImportExport.exe PrepImport /j:9WM35C2V.jrn /id:session#1 /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /t:d /encrypt /srcdir:d:\movies\drama /dstdir:movies/drama/ /skipwrite
```    

## <a name="copy-a-single-directory-to-a-hard-drive"></a><span data-ttu-id="7277d-109">將單一目錄複製到硬碟機</span><span class="sxs-lookup"><span data-stu-id="7277d-109">Copy a single directory to a hard drive</span></span>  
 <span data-ttu-id="7277d-110">這是將單一來源目錄複製到尚未使用 BitLocker 加密之硬碟的範例命令︰</span><span class="sxs-lookup"><span data-stu-id="7277d-110">Here is a sample command to copy a single source directory to a hard drive that hasn't been yet been encrypted with BitLocker:</span></span>  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:movies /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:x /format /encrypt /srcdir:d:\Movies /dstdir:entertainment/movies/  
```  
  
## <a name="copy-wwo-directories-to-a-hard-drive"></a><span data-ttu-id="7277d-111">將 wwo 目錄複製到硬碟機</span><span class="sxs-lookup"><span data-stu-id="7277d-111">Copy wwo directories to a hard drive</span></span>  
 <span data-ttu-id="7277d-112">若要將兩個來源目錄複製到磁碟機，您需要兩個命令。</span><span class="sxs-lookup"><span data-stu-id="7277d-112">To copy two source directories to a drive, you will need two commands.</span></span>  
  
 <span data-ttu-id="7277d-113">第一個命令除了一般參數之外，會指定記錄檔目錄、儲存體帳戶金鑰、目標磁碟機代號和 `format/encrypt` 需求︰</span><span class="sxs-lookup"><span data-stu-id="7277d-113">The first command specifies the log directory, storage account key, target drive letter and `format/encrypt` requirements, in addition to the common parameters:</span></span>  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:movies /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:x /format /encrypt /srcdir:d:\Movies /dstdir:entertainment/movies/  
```  
  
 <span data-ttu-id="7277d-114">第二個命令會指定日誌檔案、新的工作階段識別碼，以及來源和目的地位置︰</span><span class="sxs-lookup"><span data-stu-id="7277d-114">The second command specifies the journal file, a new session ID, and the source and destination locations:</span></span>  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:music /srcdir:d:\Music /dstdir:entertainment/music/  
```  
  
## <a name="copy-a-large-file-to-a-hard-drive-in-a-second-copy-session"></a><span data-ttu-id="7277d-115">在第二個複製工作階段中，將大型檔案複製到硬碟機</span><span class="sxs-lookup"><span data-stu-id="7277d-115">Copy a large file to a hard drive in a second copy session</span></span>  
 <span data-ttu-id="7277d-116">以下是將單一大型檔案複製到已在前一個複製工作階段中備妥之磁碟機的範例命令︰</span><span class="sxs-lookup"><span data-stu-id="7277d-116">Here is a sample command that copies a single large file to a drive that has been prepared in a previous copy session:</span></span>  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:dvd /srcfile:d:\dvd\favoritemovie.vhd /dstblob:dvd/favoritemovie.vhd  
```  
  
## <a name="next-steps"></a><span data-ttu-id="7277d-117">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7277d-117">Next steps</span></span>

* [<span data-ttu-id="7277d-118">針對匯入作業準備硬碟的簡單工作流程</span><span class="sxs-lookup"><span data-stu-id="7277d-118">Sample workflow to prepare hard drives for an import job</span></span>](storage-import-export-tool-sample-preparing-hard-drives-import-job-workflow-v1.md)
