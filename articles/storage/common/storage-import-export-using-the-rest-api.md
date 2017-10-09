---
title: "aaaUsing hello Azure 匯入/匯出服務 REST API |Microsoft 文件"
description: "了解 toofind 資源使用 hello Azure 匯入/匯出服務 REST API，包括這兩種方式 tooand 參考資料的位置。"
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 233f80e9-2e7f-48e0-9639-5c7785e7d743
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/15/2017
ms.author: muralikk
ms.openlocfilehash: fc7e1007ad632cf6f771c2545644f8de43c8f181
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-azure-importexport-service-rest-api"></a>使用 hello Azure 匯入/匯出服務 REST API

hello Microsoft Azure 匯入/匯出服務會公開 REST API tooenable 以程式設計方式控制匯入/匯出工作。 您可以使用 hello REST API tooperform hello 的所有匯入/匯出作業，您可以執行以 hello [Azure 入口網站](https://portal.azure.com/)。 此外，您可以使用 hello REST API tooperform 某些精細的作業，例如查詢 hello 目前不提供 hello Azure 傳統入口網站中工作的完成百分比。

請參閱[使用 hello Microsoft Azure 匯入/匯出服務 tooTransfer 資料 tooBlob 儲存體](../storage-import-export-service.md)hello 匯入/匯出服務，並示範如何 toouse hello 傳統入口網站 toocreate 及管理匯入的教學課程的概觀和匯出工作。

## <a name="service-endpoints"></a>服務端點

hello Azure 匯入/匯出服務是 Azure 資源管理員的資源提供者，並提供一組 REST Api 在下列 HTTPS 端點，以管理匯入/匯出工作的 hello:

```
https://management.azure.com/subscriptions/<subscription-id>/resourceGroups/<resource-group>/providers/Microsoft.ImportExport/jobs/<job-name>
```

## <a name="versioning"></a>版本控制

要求 toohello 匯入/匯出服務必須指定 hello`api-version`參數並將其值設定為太`2016-11-01`。

## <a name="importexport-service-operations"></a>匯入/匯出服務作業

[建立匯入作業](../storage-import-export-creating-an-import-job.md)

[建立匯出作業](../storage-import-export-creating-an-export-job.md)

[擷取作業的狀態資訊](storage-import-export-retrieving-state-info-for-a-job.md)

[列舉作業](../storage-import-export-enumerating-jobs.md)

[取消和刪除作業](storage-import-export-cancelling-and-deleting-jobs.md)

[備份磁碟機資訊清單](../storage-import-export-backing-up-drive-manifests.md)

[匯入/匯出作業的診斷和錯誤復原](../storage-import-export-diagnostics-and-error-recovery.md)

## <a name="next-steps"></a>後續步驟

* [儲存體匯入/匯出 REST](/rest/api/storageimportexport)
