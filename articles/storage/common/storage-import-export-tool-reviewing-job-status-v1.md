---
title: "檢閱 Azure 匯入/匯出作業狀態 - v1 | Microsoft Docs"
description: "了解如何使用執行匯入或匯出作業時建立的記錄檔來查看匯入/匯出作業的狀態。"
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: c69d1d69-6403-4eee-9949-0185faeecfa1
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/26/2017
ms.author: muralikk
ms.openlocfilehash: bdb30bc28c36ab9e969efc8be3b87b97e4027b39
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="reviewing-azure-importexport-job-status-with-copy-log-files"></a><span data-ttu-id="1bc62-103">使用複製記錄檔來檢閱 Azure 匯入/匯出作業狀態</span><span class="sxs-lookup"><span data-stu-id="1bc62-103">Reviewing Azure Import/Export job status with copy log files</span></span>
<span data-ttu-id="1bc62-104">當 Microsoft Azure 匯入/匯出服務處理與匯入或匯出作業相關聯的磁碟機時，它會將複製記錄檔寫入到您匯入或匯出 blob 的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="1bc62-104">When the Microsoft Azure Import/Export service processes drives associated with an import or export job, it writes copy log files to the storage account to or from which you are importing or exporting blobs.</span></span> <span data-ttu-id="1bc62-105">記錄檔包含每個已匯入或匯出檔案的詳細狀態。</span><span class="sxs-lookup"><span data-stu-id="1bc62-105">The log file contains detailed status about each file that was imported or exported.</span></span> <span data-ttu-id="1bc62-106">查詢已完成作業的狀態時會傳回每個複製記錄檔的 URL；如需詳細資訊，請參閱[取得作業](/rest/api/storageservices/Get-Job3)。</span><span class="sxs-lookup"><span data-stu-id="1bc62-106">The URL to each copy log file is returned when you query the status of a completed job; see [Get Job](/rest/api/storageservices/Get-Job3) for more information.</span></span>  

## <a name="example-urls"></a><span data-ttu-id="1bc62-107">範例 URL</span><span class="sxs-lookup"><span data-stu-id="1bc62-107">Example URLs</span></span>

<span data-ttu-id="1bc62-108">以下是包含兩個磁碟機之匯入作業的複製記錄檔的範例 URL：</span><span class="sxs-lookup"><span data-stu-id="1bc62-108">The following are example URLs for copy log files for an import job with two drives:</span></span>  
  
 `http://myaccount.blob.core.windows.net/ImportExportStatesPath/waies/myjob_9WM35C2V_20130921-034307-902_error.xml`  
  
 `http://myaccount.blob.core.windows.net/ImportExportStatesPath/waies/myjob_9WM45A6Q_20130921-042122-021_error.xml`  
  
 <span data-ttu-id="1bc62-109">如需複製記錄的格式和狀態碼的完整清單，請參閱[匯入/匯出服務記錄檔格式](../storage-import-export-file-format-log.md)。</span><span class="sxs-lookup"><span data-stu-id="1bc62-109">See [Import/Export service Log File Format](../storage-import-export-file-format-log.md) for the format of copy logs and the full list of status codes.</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="1bc62-110">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1bc62-110">Next steps</span></span>
 
 * [<span data-ttu-id="1bc62-111">設定 Azure 匯入/匯出工具</span><span class="sxs-lookup"><span data-stu-id="1bc62-111">Setting Up the Azure Import/Export Tool</span></span>](storage-import-export-tool-setup-v1.md)   
 * [<span data-ttu-id="1bc62-112">針對匯入作業準備硬碟</span><span class="sxs-lookup"><span data-stu-id="1bc62-112">Preparing hard drives for an import job</span></span>](../storage-import-export-tool-preparing-hard-drives-import-v1.md)   
 * [<span data-ttu-id="1bc62-113">修復匯入作業</span><span class="sxs-lookup"><span data-stu-id="1bc62-113">Repairing an import job</span></span>](../storage-import-export-tool-repairing-an-import-job-v1.md)   
 * [<span data-ttu-id="1bc62-114">修復匯出作業</span><span class="sxs-lookup"><span data-stu-id="1bc62-114">Repairing an export job</span></span>](../storage-import-export-tool-repairing-an-export-job-v1.md)   
 * [<span data-ttu-id="1bc62-115">針對 Azure 匯入/匯出工具進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="1bc62-115">Troubleshooting the Azure Import/Export Tool</span></span>](storage-import-export-tool-troubleshooting-v1.md)