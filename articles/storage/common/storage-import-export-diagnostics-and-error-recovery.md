---
title: "Azure 匯入/匯出工作的 aaaDiagnostics 和錯誤復原 |Microsoft 文件"
description: "深入了解如何 tooenable 詳細資訊記錄的 Microsoft Azure 匯入/匯出服務作業。"
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 096cc795-9af6-4335-9fe8-fffa9f239a17
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: 48164279e7904c78fed802aa3cff66e589c3f12c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="diagnostics-and-error-recovery-for-azure-importexport-jobs"></a>Azure 匯入/匯出作業的診斷和錯誤復原
處理每個磁碟機，hello Azure 匯入/匯出服務會建立錯誤記錄檔相關聯的 hello 儲存體帳戶中。 您也可以設定 hello 啟用詳細資訊記錄`LogLevel`屬性太`Verbose`時呼叫 hello [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate)或[Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update)作業。

 根據預設，記錄檔寫入名為 tooa 容器`waimportexport`。 您可以指定不同的名稱設定 hello`DiagnosticsPath`屬性時呼叫 hello`Put Job`或`Update Job Properties`作業。 hello 記錄檔會儲存為區塊 blob 以 hello 遵循命名慣例： `waies/jobname_driveid_timestamp_logtype.xml`。

 您可以擷取由呼叫 hello hello hello 作業的記錄檔的 URI [Get Job](/rest/api/storageimportexport/jobs#Jobs_Get)作業。 hello 詳細資訊記錄檔的 hello URI 會傳回在 hello`VerboseLogUri`屬性每個磁碟機，而 hello 錯誤記錄檔的 hello URI 會傳回在 hello`ErrorLogUri`屬性。

您可以使用記錄資料 tooidentify hello 下列問題的 hello。

## <a name="drive-errors"></a>磁碟機錯誤

hello 下列項目分類為磁碟機錯誤：

-   資訊清單檔案的存取或讀取 hello 的錯誤

-   不正確的 BitLocker 金鑰

-   磁碟機讀取/寫入錯誤

## <a name="blob-errors"></a>Blob 錯誤

hello 下列項目分類為 blob 錯誤：

-   不正確或衝突的 blob 或名稱

-   遺失的檔案

-   找不到 Blob

-   截斷 （hello 磁碟上的 hello 檔案則小於 hello 資訊清單中指定） 的檔案

-   損毀的檔案內容 (適用於匯入工作，偵測到與 MD5 總和檢查碼不符)

-   損毀的 blob 中繼資料和屬性檔 (偵測到與 MD5 總和檢查碼不符)

-   不正確的結構描述的 hello blob 屬性及/或中繼資料檔案

可能有其中一些組件的匯入或匯出工作無法順利完成，hello 整體工作仍然完成時的情況。 在此情況下，您可以上傳或下載 hello 遺漏 hello 資料透過網路，或您可以建立新的工作 tootransfer hello 資料。 請參閱 hello [Azure 匯入/匯出工具參考](storage-import-export-tool-how-to-v1.md)toolearn toorepair hello 資料透過網路的方式。

## <a name="next-steps"></a>後續步驟

* [使用 hello 匯入/匯出服務 REST API](storage-import-export-using-the-rest-api.md)
