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
ms.openlocfilehash: 370cf6fae7ae106e8341f65086c8b8187d335746
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="quick-reference-for-frequently-used-commands-for-import-jobs"></a><span data-ttu-id="ba325-104">匯入作業的常用命令快速參考</span><span class="sxs-lookup"><span data-stu-id="ba325-104">Quick reference for frequently used commands for import jobs</span></span>
<span data-ttu-id="ba325-105">本章節提供一些常用命令的快速參考。</span><span class="sxs-lookup"><span data-stu-id="ba325-105">This section provides a quick reference for some frequently used commands.</span></span> <span data-ttu-id="ba325-106">如需詳細使用方式，請參閱[針對匯入作業準備硬碟](../storage-import-export-tool-preparing-hard-drives-import-v1.md)。</span><span class="sxs-lookup"><span data-stu-id="ba325-106">For detailed usage, see [Preparing Hard Drives for an Import Job](../storage-import-export-tool-preparing-hard-drives-import-v1.md).</span></span>  

## <a name="prepare-a-hard-drive-when-data-has-already-been-copied-to-the-hard-drive"></a><span data-ttu-id="ba325-107">當資料已複製到硬碟時，讓硬碟做好準備</span><span class="sxs-lookup"><span data-stu-id="ba325-107">Prepare a hard drive when data has already been copied to the hard drive</span></span>
 <span data-ttu-id="ba325-108">下列命令會在資料已複製到硬碟，但尚未以 BitLocker 加密時，讓硬碟做好準備：</span><span class="sxs-lookup"><span data-stu-id="ba325-108">The following command prepares a hard drive when data has already been copied to it, but has not yet been encrypted with BitLocker:</span></span>  
  
```  
  WAImportExport.exe PrepImport /j:9WM35C2V.jrn /id:session#1 /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /t:d /encrypt /srcdir:d:\movies\drama /dstdir:movies/drama/ /skipwrite
```    

## <a name="copy-a-single-directory-to-a-hard-drive"></a><span data-ttu-id="ba325-109">將單一目錄複製到硬碟機</span><span class="sxs-lookup"><span data-stu-id="ba325-109">Copy a single directory to a hard drive</span></span>  
 <span data-ttu-id="ba325-110">下列命令會將單一來源目錄複製到尚未以 BitLocker 加密的硬碟︰</span><span class="sxs-lookup"><span data-stu-id="ba325-110">The following command copies a single source directory to a hard drive that has not yet been encrypted with BitLocker:</span></span>  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:movies /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:x /format /encrypt /srcdir:d:\Movies /dstdir:entertainment/movies/  
```  
  
## <a name="copy-two-directories-to-a-hard-drive"></a><span data-ttu-id="ba325-111">將兩個目錄複製到硬碟</span><span class="sxs-lookup"><span data-stu-id="ba325-111">Copy two directories to a hard drive</span></span>  
 <span data-ttu-id="ba325-112">若要將兩個來源目錄複製到硬碟，請使用下列命令：</span><span class="sxs-lookup"><span data-stu-id="ba325-112">To copy two source directories to a drive, use the following commands:</span></span>  
  
 <span data-ttu-id="ba325-113">第一個命令會指定記錄目錄、儲存體帳戶金鑰、目標磁碟機代號和 `format/encrypt` 需求以及一般參數︰</span><span class="sxs-lookup"><span data-stu-id="ba325-113">The first command specifies the log directory, storage account key, target drive letter, `format/encrypt` requirements, and common parameters:</span></span>  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:movies /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:x /format /encrypt /srcdir:d:\Movies /dstdir:entertainment/movies/  
```  
  
 <span data-ttu-id="ba325-114">第二個命令會指定日誌檔案、新的工作階段識別碼，以及來源和目的地位置︰</span><span class="sxs-lookup"><span data-stu-id="ba325-114">The second command specifies the journal file, a new session ID, and the source and destination locations:</span></span>  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:music /srcdir:d:\Music /dstdir:entertainment/music/  
```  
  
## <a name="copy-a-large-file-to-a-hard-drive-in-a-second-copy-session"></a><span data-ttu-id="ba325-115">在第二個複製工作階段中，將大型檔案複製到硬碟機</span><span class="sxs-lookup"><span data-stu-id="ba325-115">Copy a large file to a hard drive in a second copy session</span></span>  
 <span data-ttu-id="ba325-116">下列命令會將單一大型檔案複製到已在前一個複製工作階段中備妥的硬碟︰</span><span class="sxs-lookup"><span data-stu-id="ba325-116">The following command copies a single large file to a hard drive that was prepared in a previous copy session:</span></span>  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:dvd /srcfile:d:\dvd\favoritemovie.vhd /dstblob:dvd/favoritemovie.vhd  
```  
  
## <a name="next-steps"></a><span data-ttu-id="ba325-117">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ba325-117">Next steps</span></span>

* [<span data-ttu-id="ba325-118">針對匯入作業準備硬碟的簡單工作流程</span><span class="sxs-lookup"><span data-stu-id="ba325-118">Sample workflow to prepare hard drives for an import job</span></span>](storage-import-export-tool-sample-preparing-hard-drives-import-job-workflow-v1.md)
