---
title: "Azure 匯入/匯出匯入工作-v1 aaaRepairing |Microsoft 文件"
description: "了解如何匯入工作，所建立及執行使用 toorepair hello Azure 匯入/匯出服務。"
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 38cc16bd-ad55-4625-9a85-e1726c35fd1b
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: b1cb7d7832276a05c0912cf57505e2a5d79e7846
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="repairing-an-import-job"></a>修復匯入作業
hello Microsoft Azure 匯入/匯出服務可能會失敗 toocopy 一些檔案或檔案 toohello Windows Azure Blob 服務的部分。 部分的失敗原因包括︰  
  
-   損毀的檔案  
  
-   損壞的磁碟機  
  
-   在傳輸 hello 檔案時，變更 hello 儲存體帳戶金鑰。  
  
您可以執行 hello hello 匯入作業的複製記錄檔，和 hello 工具上傳 hello 遺失的檔案 （或檔案的部分） 的 Microsoft Azure 匯入/匯出工具 tooyour Windows Azure 儲存體帳戶 toocomplete hello 匯入工作。  
  
## <a name="repairimport-parameters"></a>RepairImport 參數

hello 指定下列參數可以與**RepairImport**: 
  
|||  
|-|-|  
|**/r:**<RepairFile\>|**必要。** 路徑 toohello 修復檔案，追蹤 hello hello 修復進度，並可讓您 tooresume 中斷的修復。 每個磁碟機需要一個修復檔案，而且只能有一個。 當您開始在給定的磁碟機的修復時，傳入 hello 路徑 tooa 修復檔案，它不存在。 tooresume 中斷的修復，您應傳入 hello 現有的修復檔名稱。 一律必須指定 hello 修復檔案對應 toohello 目標磁碟機。|  
|**/logdir:**<LogDirectory\>|**選用。** hello 記錄檔目錄。 詳細資訊的記錄檔會寫入 toothis 目錄。 如果未不指定任何記錄檔目錄，則 hello 目前目錄當做 hello 記錄目錄中。|  
|**/d:**<TargetDirectories\>|**必要。** 一或多個以分號分隔目錄，其中包含 hello 原始匯入的檔案。 hello 匯入磁碟機也可以使用，但如果原始檔的替代位置可用，就不需要。|  
|**/bk:**<BitLockerKey\>|**選用。** 如果您想 hello 工具 toounlock 有可用 hello 原始的檔案加密的磁碟機，您應該指定 hello BitLocker 金鑰。|  
|**/sn:**<StorageAccountName\>|**必要。** hello 名稱 hello hello 儲存體帳戶匯入作業。|  
|**/sk:**<StorageAccountKey\>|如果未指定 (且只有在未指定) 容器 SAS 時，才是**必要**參數。 hello hello hello 的儲存體帳戶的帳戶金鑰匯入作業。|  
|**/csas:**<ContainerSas\>|**需要**如果且只有未指定 hello 儲存體帳戶金鑰。 用於存取與 hello 匯入工作相關聯的 hello blob hello 容器 SAS。|  
|**/CopyLogFile:**<DriveCopyLogFile\>|**必要。** 路徑 toohello 磁碟機複製記錄檔 （詳細資訊記錄檔或錯誤記錄檔）。 hello 檔案 hello Windows Azure 匯入/匯出服務所產生，並可從 hello 與 hello 工作相關聯的 blob 儲存體下載。 hello 複製記錄檔包含失敗的 blob 或檔案，也就是 toobe 修復的相關資訊。|  
|**/PathMapFile:**<DrivePathMapFile\>|**選用。** 可用的路徑 tooa 文字檔案 tooresolve 語意模糊，如果您有多個檔案，以相同的名稱，您已匯入中的 hello hello 相同的作業。 hello 第一個階段 hello 工具執行時，它可以填入此檔案的所有 hello 模稜兩可的名稱。 後續的執行中的 hello 工具會使用此檔案 tooresolve hello 模稜兩可。|  
  
## <a name="using-hello-repairimport-command"></a>使用 hello RepairImport 命令  
toorepair hello 網路透過串流處理 hello 資料匯入資料，您必須指定 hello 目錄，其中包含已匯入使用 hello 原始檔案 hello`/d`參數。 您也必須指定您從儲存體帳戶下載的 hello 複製記錄檔。 一般命令列 toorepair 部分失敗之匯入工作看起來像：  
  
```  
WAImportExport.exe RepairImport /r:C:\WAImportExport\9WM35C2V.rep /d:C:\Users\bob\Pictures;X:\BobBackup\photos /sn:bobmediaaccount /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /CopyLogFile:C:\WAImportExport\9WM35C2V.log  
```  
  
在 hello 已損毀 hello 的運送 hello 匯入工作的磁碟機上的下列複製記錄檔，檔案的一 64-K 段的範例。 由於這是 hello 只有失敗處，hello hello 作業中的 hello blob 的其餘部分已順利匯入。  
  
```xml
<?xml version="1.0" encoding="utf-8"?>  
<DriveLog>  
 <DriveId>9WM35C2V</DriveId>  
 <Blob Status="CompletedWithErrors">  
 <BlobPath>pictures/animals/koala.jpg</BlobPath>  
 <FilePath>\animals\koala.jpg</FilePath>  
 <Length>163840</Length>  
 <ImportDisposition Status="Overwritten">overwrite</ImportDisposition>  
 <PageRangeList>  
  <PageRange Offset="65536" Length="65536" Hash="AA2585F6F6FD01C4AD4256E018240CD4" Status="Corrupted" />  
 </PageRangeList>  
 </Blob>  
 <Status>CompletedWithErrors</Status>  
</DriveLog>  
```
  
當這個複製記錄傳遞 toohello Azure 匯入/匯出工具時，hello 工具會嘗試透過 hello 網路複製遺漏的 hello 內容 toofinish hello 匯入此檔案。 Hello 上述範例中，下列 hello 工具會尋找 hello 原始檔案`\animals\koala.jpg`hello 兩個目錄內`C:\Users\bob\Pictures`和`X:\BobBackup\photos`。 如果 hello 檔案`C:\Users\bob\Pictures\animals\koala.jpg`存在，hello Azure 匯入/匯出工具複本 hello 遺漏的範圍資料 toohello 對應的 blob `http://bobmediaaccount.blob.core.windows.net/pictures/animals/koala.jpg`。  
  
## <a name="resolving-conflicts-when-using-repairimport"></a>解決使用 RepairImport 時的衝突  
在某些情況下，hello 工具可能會無法 toofind 或開啟 hello 所需的檔案，其中一個 hello 下列原因： 找不到 hello 檔案、 hello 檔案無法存取、 hello 檔案名稱模稜兩可，或 hello hello 檔案內容已不正確。  
  
如果嘗試 toolocate hello 工具可能會發生模稜兩可的錯誤`\animals\koala.jpg`底下都同名的檔案且`C:\Users\bob\pictures`和`X:\BobBackup\photos`。 也就是說，兩者`C:\Users\bob\pictures\animals\koala.jpg`和`X:\BobBackup\photos\animals\koala.jpg`存在於 hello 匯入工作磁碟機上。  
  
hello`/PathMapFile`選項可讓您 tooresolve 這些錯誤。 您可以指定 hello hello 檔案名稱，其中包含 hello hello 工具的檔案清單無法 toocorrectly 識別。 hello 下列命令列範例會填入`9WM35C2V_pathmap.txt`:  
  
```
WAImportExport.exe RepairImport /r:C:\WAImportExport\9WM35C2V.rep /d:C:\Users\bob\Pictures;X:\BobBackup\photos /sn:bobmediaaccount /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /CopyLogFile:C:\WAImportExport\9WM35C2V.log /PathMapFile:C:\WAImportExport\9WM35C2V_pathmap.txt  
```
  
hello 工具接著將要撰寫 hello 有問題的檔案路徑太`9WM35C2V_pathmap.txt`，其中在每一行。 比方說，hello 檔案可能包含下列項目執行 hello 命令之後的 hello:  
 
```
\animals\koala.jpg  
\animals\kangaroo.jpg  
```
  
 Hello 清單中每個檔案，您應該嘗試 toolocate 並開啟 hello 檔案 tooensure 是可用 toohello 工具。 如果您想 tootell hello 工具明確其中 toofind 檔案，您可以修改 hello 路徑對應檔案，再新增 hello 路徑 tooeach 檔案上 hello 同一行，以 tab 字元分隔：  
  
```
\animals\koala.jpg           C:\Users\bob\Pictures\animals\koala.jpg  
\animals\kangaroo.jpg        X:\BobBackup\photos\animals\kangaroo.jpg  
```
  
讓 hello 必要的檔案可用 toohello 工具或更新的 hello 路徑對應檔案之後, 您可以重新執行 hello 工具 toocomplete hello 匯入程序。  
  
## <a name="next-steps"></a>後續步驟
 
* [正在設定 hello Azure 匯入/匯出工具](storage-import-export-tool-setup-v1.md)   
* [針對匯入作業準備硬碟](../storage-import-export-tool-preparing-hard-drives-import-v1.md)   
* [利用複製記錄檔檢閱作業狀態](storage-import-export-tool-reviewing-job-status-v1.md)   
* [修復匯出作業](../storage-import-export-tool-repairing-an-export-job-v1.md)   
* [疑難排解 hello Azure 匯入/匯出工具](storage-import-export-tool-troubleshooting-v1.md)
