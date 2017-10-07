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
ms.openlocfilehash: 363731ede4751124a714b4ce96852e0b8c4dbca4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="reviewing-azure-importexport-job-status-with-copy-log-files"></a>使用複製記錄檔來檢閱 Azure 匯入/匯出作業狀態
Hello Microsoft Azure 匯入/匯出服務處理與匯入或匯出工作相關聯的磁碟機時，它會寫入複製記錄檔 toohello 儲存體帳戶 tooor 您要從中匯入或匯出 blob。 hello 記錄檔包含有關每個已匯入或匯出檔案的詳細的狀態。 當您查詢已完成的工作; hello 狀態時，會傳回 hello URL tooeach 複製記錄檔請參閱[Get Job](/rest/api/storageservices/Get-Job3)如需詳細資訊。  

## <a name="example-urls"></a>範例 URL

hello 下面是兩個磁碟機匯入工作複製記錄檔的範例 Url:  
  
 `http://myaccount.blob.core.windows.net/ImportExportStatesPath/waies/myjob_9WM35C2V_20130921-034307-902_error.xml`  
  
 `http://myaccount.blob.core.windows.net/ImportExportStatesPath/waies/myjob_9WM45A6Q_20130921-042122-021_error.xml`  
  
 請參閱[匯入/匯出服務記錄檔格式](../storage-import-export-file-format-log.md)hello 格式的複製記錄檔和 hello 的狀態碼的完整清單。  
  
## <a name="next-steps"></a>後續步驟
 
 * [正在設定 hello Azure 匯入/匯出工具](storage-import-export-tool-setup-v1.md)   
 * [針對匯入作業準備硬碟](../storage-import-export-tool-preparing-hard-drives-import-v1.md)   
 * [修復匯入作業](../storage-import-export-tool-repairing-an-import-job-v1.md)   
 * [修復匯出作業](../storage-import-export-tool-repairing-an-export-job-v1.md)   
 * [疑難排解 hello Azure 匯入/匯出工具](storage-import-export-tool-troubleshooting-v1.md)
