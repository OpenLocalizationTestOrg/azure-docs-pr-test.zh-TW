---
title: "aaaTroubleshooting hello Azure 匯入/匯出工具 |Microsoft 文件"
description: "了解一些 hello 常見的問題使用 hello Azure 匯入/匯出工具，以及如何 toohandle 它們。"
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: b91ca5eb-c557-460a-9afc-0590b38471f9
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/15/2017
ms.author: muralikk
ms.openlocfilehash: 254439c15797862dded5d80028b8780ad163b2b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-hello-azure-importexport-tool"></a><span data-ttu-id="f92a1-103">疑難排解 hello Azure 匯入/匯出工具</span><span class="sxs-lookup"><span data-stu-id="f92a1-103">Troubleshooting hello Azure Import/Export Tool</span></span>
<span data-ttu-id="f92a1-104">如果發生問題，hello Microsoft Azure 匯入/匯出工具會傳回錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="f92a1-104">hello Microsoft Azure Import/Export Tool returns error messages if it runs into issues.</span></span> <span data-ttu-id="f92a1-105">本主題列出使用者可能會遇到的一些常見問題。</span><span class="sxs-lookup"><span data-stu-id="f92a1-105">This topic lists some common issues that users may run into.</span></span>  
  
## <a name="a-copy-session-fails-what-i-should-do"></a><span data-ttu-id="f92a1-106">複製工作階段失敗，我該怎麼做？</span><span class="sxs-lookup"><span data-stu-id="f92a1-106">A copy session fails, what I should do?</span></span>  
 <span data-ttu-id="f92a1-107">當複製工作階段失敗時，有兩個選項︰</span><span class="sxs-lookup"><span data-stu-id="f92a1-107">When a copy session fails, there are two options:</span></span>  
  
 <span data-ttu-id="f92a1-108">如果 hello 錯誤重試的例如，如果 hello 網路共用已離線的短週期和現在已回復連線，您可以繼續 hello 複製工作階段。</span><span class="sxs-lookup"><span data-stu-id="f92a1-108">If hello error is retryable, for example if hello network share was offline for a short period and now is back online, you can resume hello copy session.</span></span> <span data-ttu-id="f92a1-109">如果是無法重試的例如，如果您指定 hello 命令列參數中的 hello 錯誤的來源檔案目錄 hello 錯誤，您會需要 tooabort hello 複製工作階段。</span><span class="sxs-lookup"><span data-stu-id="f92a1-109">If hello error is not retryable, for example if you specified hello wrong source file directory in hello command line parameters, you need tooabort hello copy session.</span></span> <span data-ttu-id="f92a1-110">如需有關繼續和中止複製工作階段的詳細資訊，請參閱[針對匯入作業準備硬碟](../storage-import-export-tool-preparing-hard-drives-import-v1.md)。</span><span class="sxs-lookup"><span data-stu-id="f92a1-110">See [Preparing Hard Drives for an Import Job](../storage-import-export-tool-preparing-hard-drives-import-v1.md) for more information about resuming and aborting copy sessions.</span></span>  
  
## <a name="i-cant-resume-or-abort-a-copy-session"></a><span data-ttu-id="f92a1-111">我無法繼續或中止複製工作階段。</span><span class="sxs-lookup"><span data-stu-id="f92a1-111">I can't resume or abort a copy session.</span></span>  
 <span data-ttu-id="f92a1-112">如果 hello 複製工作階段 hello 磁碟機中，第一個複製工作階段則應該清楚 hello 錯誤訊息: 「 hello 第一個複製工作階段無法繼續或中止。 」</span><span class="sxs-lookup"><span data-stu-id="f92a1-112">If hello copy session is hello first copy session for a drive, then hello error message should state: "hello first copy session cannot be resumed or aborted."</span></span> <span data-ttu-id="f92a1-113">在此情況下，您可以刪除 hello 舊的日誌檔，然後重新執行 hello 命令。</span><span class="sxs-lookup"><span data-stu-id="f92a1-113">In this case, you can delete hello old journal file and rerun hello command.</span></span>  
  
 <span data-ttu-id="f92a1-114">如果複製工作階段不是 hello 第一個磁碟機，它可以永遠是繼續或中止。</span><span class="sxs-lookup"><span data-stu-id="f92a1-114">If a copy session is not hello first one for a drive, it can always be resumed or aborted.</span></span>  
  
## <a name="i-lost-hello-journal-file-can-i-still-create-hello-job"></a><span data-ttu-id="f92a1-115">我遺失 hello 日誌檔，我還是可以建立 hello 作業嗎？</span><span class="sxs-lookup"><span data-stu-id="f92a1-115">I lost hello journal file, can I still create hello job?</span></span>  
 <span data-ttu-id="f92a1-116">hello 磁碟機的日誌檔內含 hello 資料 toothis 磁碟機，將複製的完整資訊，並需要的 tooadd 多個檔案 toohello 磁碟機及將會使用的 toocreate 匯入工作。</span><span class="sxs-lookup"><span data-stu-id="f92a1-116">hello journal file for a drive contains hello complete information of copying data toothis drive, and it is needed tooadd more files toohello drive and will be used toocreate an import job.</span></span> <span data-ttu-id="f92a1-117">Hello 日誌檔遺失時，您必須 tooredo hello 磁碟機的所有 hello 複製工作階段。</span><span class="sxs-lookup"><span data-stu-id="f92a1-117">If hello journal file is lost, you will have tooredo all hello copy sessions for hello drive.</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="f92a1-118">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f92a1-118">Next steps</span></span>
 
* [<span data-ttu-id="f92a1-119">設定 hello azure 匯入/匯出工具</span><span class="sxs-lookup"><span data-stu-id="f92a1-119">Setting up hello azure import/export tool</span></span>](../storage-import-export-tool-setup-v1.md)   
* [<span data-ttu-id="f92a1-120">針對匯入作業準備硬碟</span><span class="sxs-lookup"><span data-stu-id="f92a1-120">Preparing hard drives for an import job</span></span>](../storage-import-export-tool-preparing-hard-drives-import-v1.md)   
* [<span data-ttu-id="f92a1-121">利用複製記錄檔檢閱作業狀態</span><span class="sxs-lookup"><span data-stu-id="f92a1-121">Reviewing job status with copy log files</span></span>](../storage-import-export-tool-reviewing-job-status-v1.md)   
* [<span data-ttu-id="f92a1-122">修復匯入作業</span><span class="sxs-lookup"><span data-stu-id="f92a1-122">Repairing an import job</span></span>](../storage-import-export-tool-repairing-an-import-job-v1.md)   
* [<span data-ttu-id="f92a1-123">修復匯出作業</span><span class="sxs-lookup"><span data-stu-id="f92a1-123">Repairing an export job</span></span>](../storage-import-export-tool-repairing-an-export-job-v1.md)
