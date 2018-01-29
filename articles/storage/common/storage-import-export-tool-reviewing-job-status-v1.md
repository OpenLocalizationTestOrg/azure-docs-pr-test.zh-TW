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
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/11/2017
---
# <a name="reviewing-azure-importexport-job-status-with-copy-log-files"></a>使用複製記錄檔來檢閱 Azure 匯入/匯出作業狀態
當 Microsoft Azure 匯入/匯出服務處理與匯入或匯出作業相關聯的磁碟機時，它會將複製記錄檔寫入到您匯入或匯出 blob 的儲存體帳戶。 記錄檔包含每個已匯入或匯出檔案的詳細狀態。 查詢已完成作業的狀態時會傳回每個複製記錄檔的 URL；如需詳細資訊，請參閱[取得作業](/rest/api/storageservices/Get-Job3)。  

## <a name="example-urls"></a>範例 URL

以下是包含兩個磁碟機之匯入作業的複製記錄檔的範例 URL：  
  
 `http://myaccount.blob.core.windows.net/ImportExportStatesPath/waies/myjob_9WM35C2V_20130921-034307-902_error.xml`  
  
 `http://myaccount.blob.core.windows.net/ImportExportStatesPath/waies/myjob_9WM45A6Q_20130921-042122-021_error.xml`  
  
 如需複製記錄的格式和狀態碼的完整清單，請參閱[匯入/匯出服務記錄檔格式](../storage-import-export-file-format-log.md)。  
  
## <a name="next-steps"></a>後續步驟
 
 * [設定 Azure 匯入/匯出工具](storage-import-export-tool-setup-v1.md)   
 * [針對匯入作業準備硬碟](../storage-import-export-tool-preparing-hard-drives-import-v1.md)   
 * [修復匯入作業](../storage-import-export-tool-repairing-an-import-job-v1.md)   
 * [修復匯出作業](../storage-import-export-tool-repairing-an-export-job-v1.md)   
 * [針對 Azure 匯入/匯出工具進行疑難排解](storage-import-export-tool-troubleshooting-v1.md)
