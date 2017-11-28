---
title: "Azure 匯入/匯出作業狀態 v1 aaaReviewing |Microsoft 文件"
description: "深入了解 toouse hello 記錄檔時，建立 hello 匯入或匯出工作的方式執行 toosee hello hello 匯入/匯出工作狀態。"
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
ms.openlocfilehash: 378bc9a7ef6bfe65209413c8c4134f313a2c0d79
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="reviewing-azure-importexport-job-status-with-copy-log-files"></a><span data-ttu-id="ad894-103">使用複製記錄檔來檢閱 Azure 匯入/匯出作業狀態</span><span class="sxs-lookup"><span data-stu-id="ad894-103">Reviewing Azure Import/Export job status with copy log files</span></span>
<span data-ttu-id="ad894-104">Hello Microsoft Azure 匯入/匯出服務處理與匯入或匯出工作相關聯的磁碟機時，它會寫入複製記錄檔 toohello 儲存體帳戶 tooor 您要從中匯入或匯出 blob。</span><span class="sxs-lookup"><span data-stu-id="ad894-104">When hello Microsoft Azure Import/Export service processes drives associated with an import or export job, it writes copy log files toohello storage account tooor from which you are importing or exporting blobs.</span></span> <span data-ttu-id="ad894-105">hello 記錄檔包含有關每個已匯入或匯出檔案的詳細的狀態。</span><span class="sxs-lookup"><span data-stu-id="ad894-105">hello log file contains detailed status about each file that was imported or exported.</span></span> <span data-ttu-id="ad894-106">當您查詢已完成的工作; hello 狀態時，會傳回 hello URL tooeach 複製記錄檔請參閱[Get Job](/rest/api/storageservices/Get-Job3)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="ad894-106">hello URL tooeach copy log file is returned when you query hello status of a completed job; see [Get Job](/rest/api/storageservices/Get-Job3) for more information.</span></span>  

## <a name="example-urls"></a><span data-ttu-id="ad894-107">範例 URL</span><span class="sxs-lookup"><span data-stu-id="ad894-107">Example URLs</span></span>

<span data-ttu-id="ad894-108">hello 下面是兩個磁碟機匯入工作複製記錄檔的範例 Url:</span><span class="sxs-lookup"><span data-stu-id="ad894-108">hello following are example URLs for copy log files for an import job with two drives:</span></span>  
  
 `http://myaccount.blob.core.windows.net/ImportExportStatesPath/waies/myjob_9WM35C2V_20130921-034307-902_error.xml`  
  
 `http://myaccount.blob.core.windows.net/ImportExportStatesPath/waies/myjob_9WM45A6Q_20130921-042122-021_error.xml`  
  
 <span data-ttu-id="ad894-109">請參閱[匯入/匯出服務記錄檔格式](storage-import-export-file-format-log.md)hello 格式的複製記錄檔和 hello 的狀態碼的完整清單。</span><span class="sxs-lookup"><span data-stu-id="ad894-109">See [Import/Export service Log File Format](storage-import-export-file-format-log.md) for hello format of copy logs and hello full list of status codes.</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="ad894-110">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ad894-110">Next steps</span></span>
 
 * [<span data-ttu-id="ad894-111">正在設定 hello Azure 匯入/匯出工具</span><span class="sxs-lookup"><span data-stu-id="ad894-111">Setting Up hello Azure Import/Export Tool</span></span>](storage-import-export-tool-setup-v1.md)   
 * [<span data-ttu-id="ad894-112">針對匯入作業準備硬碟</span><span class="sxs-lookup"><span data-stu-id="ad894-112">Preparing hard drives for an import job</span></span>](storage-import-export-tool-preparing-hard-drives-import-v1.md)   
 * [<span data-ttu-id="ad894-113">修復匯入作業</span><span class="sxs-lookup"><span data-stu-id="ad894-113">Repairing an import job</span></span>](storage-import-export-tool-repairing-an-import-job-v1.md)   
 * [<span data-ttu-id="ad894-114">修復匯出作業</span><span class="sxs-lookup"><span data-stu-id="ad894-114">Repairing an export job</span></span>](storage-import-export-tool-repairing-an-export-job-v1.md)   
 * [<span data-ttu-id="ad894-115">疑難排解 hello Azure 匯入/匯出工具</span><span class="sxs-lookup"><span data-stu-id="ad894-115">Troubleshooting hello Azure Import/Export Tool</span></span>](storage-import-export-tool-troubleshooting-v1.md)
