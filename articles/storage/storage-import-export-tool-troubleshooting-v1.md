---
title: "針對 Azure 匯入/匯出工具進行疑難排解 | Microsoft Docs"
description: "了解使用 Azure 匯入/匯出工具時見到的一些常見問題及其處理方式。"
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
ms.openlocfilehash: 43b5d5a57df6bdda57a31ff0330ec6eff7aa732c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting-the-azure-importexport-tool"></a><span data-ttu-id="21733-103">針對 Azure 匯入/匯出工具進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="21733-103">Troubleshooting the Azure Import/Export Tool</span></span>
<span data-ttu-id="21733-104">如果發生問題，Microsoft Azure 匯入/匯出工具會傳回錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="21733-104">The Microsoft Azure Import/Export Tool returns error messages if it runs into issues.</span></span> <span data-ttu-id="21733-105">本主題列出使用者可能會遇到的一些常見問題。</span><span class="sxs-lookup"><span data-stu-id="21733-105">This topic lists some common issues that users may run into.</span></span>  
  
## <a name="a-copy-session-fails-what-i-should-do"></a><span data-ttu-id="21733-106">複製工作階段失敗，我該怎麼做？</span><span class="sxs-lookup"><span data-stu-id="21733-106">A copy session fails, what I should do?</span></span>  
 <span data-ttu-id="21733-107">當複製工作階段失敗時，有兩個選項︰</span><span class="sxs-lookup"><span data-stu-id="21733-107">When a copy session fails, there are two options:</span></span>  
  
 <span data-ttu-id="21733-108">如果錯誤可以重試 (例如，網路共用曾短暫離線，而現已上線)，您可以繼續複製工作階段。</span><span class="sxs-lookup"><span data-stu-id="21733-108">If the error is retryable, for example if the network share was offline for a short period and now is back online, you can resume the copy session.</span></span> <span data-ttu-id="21733-109">如果錯誤不可重試 (例如，您在命令列參數中指定了錯誤的來源檔案目錄)，您需要中止複製工作階段。</span><span class="sxs-lookup"><span data-stu-id="21733-109">If the error is not retryable, for example if you specified the wrong source file directory in the command line parameters, you need to abort the copy session.</span></span> <span data-ttu-id="21733-110">如需有關繼續和中止複製工作階段的詳細資訊，請參閱[針對匯入作業準備硬碟](storage-import-export-tool-preparing-hard-drives-import-v1.md)。</span><span class="sxs-lookup"><span data-stu-id="21733-110">See [Preparing Hard Drives for an Import Job](storage-import-export-tool-preparing-hard-drives-import-v1.md) for more information about resuming and aborting copy sessions.</span></span>  
  
## <a name="i-cant-resume-or-abort-a-copy-session"></a><span data-ttu-id="21733-111">我無法繼續或中止複製工作階段。</span><span class="sxs-lookup"><span data-stu-id="21733-111">I can't resume or abort a copy session.</span></span>  
 <span data-ttu-id="21733-112">如果複製工作階段是磁碟機的第一個複製工作階段，則錯誤訊息應如下所示：「第一個複製工作階段無法繼續或中止。」</span><span class="sxs-lookup"><span data-stu-id="21733-112">If the copy session is the first copy session for a drive, then the error message should state: "The first copy session cannot be resumed or aborted."</span></span> <span data-ttu-id="21733-113">在此情況下，您可以刪除舊的日誌檔，然後重新執行命令。</span><span class="sxs-lookup"><span data-stu-id="21733-113">In this case, you can delete the old journal file and rerun the command.</span></span>  
  
 <span data-ttu-id="21733-114">如果複製工作階段不是磁碟機的第一個複製工作階段，則可以永遠繼續或中止。</span><span class="sxs-lookup"><span data-stu-id="21733-114">If a copy session is not the first one for a drive, it can always be resumed or aborted.</span></span>  
  
## <a name="i-lost-the-journal-file-can-i-still-create-the-job"></a><span data-ttu-id="21733-115">我遺失了日誌檔，還可以建立作業嗎？</span><span class="sxs-lookup"><span data-stu-id="21733-115">I lost the journal file, can I still create the job?</span></span>  
 <span data-ttu-id="21733-116">磁碟機的日誌檔包含將資料複製到這個磁碟機的完整資訊，而且必須將更多檔案新增到磁碟機並將用來建立匯入作業。</span><span class="sxs-lookup"><span data-stu-id="21733-116">The journal file for a drive contains the complete information of copying data to this drive, and it is needed to add more files to the drive and will be used to create an import job.</span></span> <span data-ttu-id="21733-117">如果日誌檔案遺失，您必須針對磁碟機重做所有的複製工作階段。</span><span class="sxs-lookup"><span data-stu-id="21733-117">If the journal file is lost, you will have to redo all the copy sessions for the drive.</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="21733-118">後續步驟</span><span class="sxs-lookup"><span data-stu-id="21733-118">Next steps</span></span>
 
* [<span data-ttu-id="21733-119">設定 Azure 匯入/匯出工具</span><span class="sxs-lookup"><span data-stu-id="21733-119">Setting up the azure import/export tool</span></span>](storage-import-export-tool-setup-v1.md)   
* [<span data-ttu-id="21733-120">針對匯入作業準備硬碟</span><span class="sxs-lookup"><span data-stu-id="21733-120">Preparing hard drives for an import job</span></span>](storage-import-export-tool-preparing-hard-drives-import-v1.md)   
* [<span data-ttu-id="21733-121">利用複製記錄檔檢閱作業狀態</span><span class="sxs-lookup"><span data-stu-id="21733-121">Reviewing job status with copy log files</span></span>](storage-import-export-tool-reviewing-job-status-v1.md)   
* [<span data-ttu-id="21733-122">修復匯入作業</span><span class="sxs-lookup"><span data-stu-id="21733-122">Repairing an import job</span></span>](storage-import-export-tool-repairing-an-import-job-v1.md)   
* [<span data-ttu-id="21733-123">修復匯出作業</span><span class="sxs-lookup"><span data-stu-id="21733-123">Repairing an export job</span></span>](storage-import-export-tool-repairing-an-export-job-v1.md)
