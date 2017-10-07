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
# <a name="troubleshooting-hello-azure-importexport-tool"></a>疑難排解 hello Azure 匯入/匯出工具
如果發生問題，hello Microsoft Azure 匯入/匯出工具會傳回錯誤訊息。 本主題列出使用者可能會遇到的一些常見問題。  
  
## <a name="a-copy-session-fails-what-i-should-do"></a>複製工作階段失敗，我該怎麼做？  
 當複製工作階段失敗時，有兩個選項︰  
  
 如果 hello 錯誤重試的例如，如果 hello 網路共用已離線的短週期和現在已回復連線，您可以繼續 hello 複製工作階段。 如果是無法重試的例如，如果您指定 hello 命令列參數中的 hello 錯誤的來源檔案目錄 hello 錯誤，您會需要 tooabort hello 複製工作階段。 如需有關繼續和中止複製工作階段的詳細資訊，請參閱[針對匯入作業準備硬碟](../storage-import-export-tool-preparing-hard-drives-import-v1.md)。  
  
## <a name="i-cant-resume-or-abort-a-copy-session"></a>我無法繼續或中止複製工作階段。  
 如果 hello 複製工作階段 hello 磁碟機中，第一個複製工作階段則應該清楚 hello 錯誤訊息: 「 hello 第一個複製工作階段無法繼續或中止。 」 在此情況下，您可以刪除 hello 舊的日誌檔，然後重新執行 hello 命令。  
  
 如果複製工作階段不是 hello 第一個磁碟機，它可以永遠是繼續或中止。  
  
## <a name="i-lost-hello-journal-file-can-i-still-create-hello-job"></a>我遺失 hello 日誌檔，我還是可以建立 hello 作業嗎？  
 hello 磁碟機的日誌檔內含 hello 資料 toothis 磁碟機，將複製的完整資訊，並需要的 tooadd 多個檔案 toohello 磁碟機及將會使用的 toocreate 匯入工作。 Hello 日誌檔遺失時，您必須 tooredo hello 磁碟機的所有 hello 複製工作階段。  
  
## <a name="next-steps"></a>後續步驟
 
* [設定 hello azure 匯入/匯出工具](../storage-import-export-tool-setup-v1.md)   
* [針對匯入作業準備硬碟](../storage-import-export-tool-preparing-hard-drives-import-v1.md)   
* [利用複製記錄檔檢閱作業狀態](../storage-import-export-tool-reviewing-job-status-v1.md)   
* [修復匯入作業](../storage-import-export-tool-repairing-an-import-job-v1.md)   
* [修復匯出作業](../storage-import-export-tool-repairing-an-export-job-v1.md)
