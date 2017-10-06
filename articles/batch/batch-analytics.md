---
title: "aaaAzure 批次分析 |Microsoft 文件"
description: "Azure Batch 分析的參考。"
services: batch
author: tamram
manager: timlt
ms.assetid: 
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 04/20/2017
ms.author: tamram
ms.openlocfilehash: 462fbad1ac522b485ae18c1e8891b9d2cabd45e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="batch-analytics"></a>批次分析
在批次分析中的 hello 主題包含 hello 事件和警示適用於批次服務資源的參考資訊。

請參閱[記錄事件以便對 Batch 解決方案進行診斷評估和監視](https://azure.microsoft.com/documentation/articles/batch-diagnostics/)，以取得啟用與取用批次診斷記錄檔的詳細資訊。

## <a name="diagnostic-logs"></a>診斷記錄檔

hello Azure 批次服務會發出診斷記錄的事件遵循特定的資源，批次 hello 存留期間的 hello。

**服務記錄檔事件**
* [建立集區](batch-pool-create-event.md)
* [開始刪除集區](batch-pool-delete-start-event.md)
* [完成集區刪除](batch-pool-delete-complete-event.md)
* [開始調整集區大小](batch-pool-resize-start-event.md)
* [完成集區大小調整](batch-pool-resize-complete-event.md)
* [開始工作](batch-task-start-event.md)
* [完成工作](batch-task-complete-event.md)
* [工作失敗](batch-task-fail-event.md)