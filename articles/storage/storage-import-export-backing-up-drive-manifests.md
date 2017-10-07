---
title: "Azure 匯入/匯出磁碟機資訊清單中向上 aaaBacking |Microsoft 文件"
description: "了解如何 toohave 您的磁碟機資訊清單 hello Microsoft Azure 匯入/匯出服務會自動備份。"
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 594abd80-b834-4077-a474-d8a0f4b7928a
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: f48b97a2cce62714aace2b30a393305202c7ecd9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="backing-up-drive-manifests-for-azure-importexport-jobs"></a>備份 Azure 匯入/匯出作業的磁碟機資訊清單

磁碟機資訊清單可以自動備份 tooblobs 所設定的 hello`BackupDriveManifest`屬性太`true`在 hello [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate)或[Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) REST API 作業。 根據預設，hello 磁碟機資訊清單不會備份。 hello 磁碟機資訊清單備份會儲存為 hello 與 hello 工作相關聯的儲存體帳戶內的容器中的區塊 blob。 根據預設，hello 容器名稱是`waimportexport`，但是您可以指定不同的名稱在 hello`DiagnosticsPath`屬性時呼叫 hello`Put Job`或`Update Job Properties`作業。 hello 備份資訊清單的 blob 命名 hello 下列格式： `waies/jobname_driveid_timestamp_manifest.xml`。

 您可以擷取由呼叫 hello URI hello 備份磁碟機資訊清單作業的 hello [Get Job](/rest/api/storageimportexport/jobs#Jobs_Get)作業。 hello blob URI 會傳回在 hello`ManifestUri`屬性每個磁碟機。

## <a name="next-steps"></a>後續步驟

* [使用 hello 匯入/匯出服務 REST API](storage-import-export-using-the-rest-api.md)
