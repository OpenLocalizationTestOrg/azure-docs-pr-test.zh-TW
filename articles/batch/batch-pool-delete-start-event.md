---
title: "aaa\"Azure Batch 集區刪除開始事件 |Microsoft 文件 」"
description: "Batch 集區刪除開始事件的參考。"
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
ms.openlocfilehash: 79bb28bffc760a49cc0a95062f5086dc96c6a795
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="pool-delete-start-event"></a>集區刪除開始事件

 集區刪除作業開始時，就會發出此事件。 由於 hello 集區刪除非同步事件，您可以預期發出一次 hello 刪除作業的集區刪除完成事件 toobe 完成。

 hello 下列範例顯示 hello 主體的集區刪除開始事件。

```
{
    "id": "myPool1"
}
```

|元素|類型|注意事項|
|-------------|----------|-----------|
|id|String|hello hello 集區識別碼。|
