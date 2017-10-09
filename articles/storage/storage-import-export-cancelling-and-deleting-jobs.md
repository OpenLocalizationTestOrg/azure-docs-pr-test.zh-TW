---
title: "aaaCancel 和刪除 Azure 匯入/匯出作業 |Microsoft 文件"
description: "了解如何 toocancel 和 delete 作業 hello Microsoft Azure 匯入/匯出服務。"
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: fd3d66f0-1dbb-4c75-9223-307d5abaeefc
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: 5d2aba510dafd0ca9a10f5643f721e7059a6a8f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="canceling-and-deleting-azure-importexport-jobs"></a>取消及刪除 Azure 匯入/匯出作業

您可以要求在 hello 前取消工作`Packaging`呼叫 hello 狀態[Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update)作業及設定 hello`CancelRequested`項目太`true`。 將取消 hello 作業，以最佳方式為基礎。 如果磁碟機中傳送資料的 hello 程序，資料可能會繼續 toobe 轉移，即使已經要求取消之後也一樣。

 已取消的工作會移動 toohello`Completed`狀態並保留 90 天，此時便會被刪除。

 toodelete 作業呼叫 hello[刪除作業](/rest/api/storageimportexport/jobs#Jobs_Delete)作業之前已出貨 hello 作業 (*也就是*，而 hello 工作處於 hello`Creating`狀態)。 您也可以在 hello 時刪除作業`Completed`狀態。 已刪除的工作之後，其資訊和狀態便無法再存取透過 hello REST API 或 hello Azure 入口網站。

## <a name="next-steps"></a>後續步驟

* [使用 hello 匯入/匯出服務 REST API](storage-import-export-using-the-rest-api.md)
