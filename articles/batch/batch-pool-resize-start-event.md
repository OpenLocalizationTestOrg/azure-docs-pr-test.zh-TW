---
title: "aaa\"Azure Batch 集區調整大小開始事件 |Microsoft 文件 」"
description: "Batch 集區調整大小開始事件的參考。"
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
ms.openlocfilehash: 2ca2a4f1195c3f785ae5b051b63340f70eecbc22
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="pool-resize-start-event"></a>集區調整大小開始事件

 集區調整大小開始時，就會發出此事件。 由於 hello 集區調整大小是非同步的事件，您可以預期發出一次 hello 的調整大小作業的集區調整大小完成事件 toobe 完成。

 下列範例顯示 hello 0 too2 節點手動調整大小集區的集區調整大小開始事件的本文 hello 調整大小。

```
{
    "poolId": "myPool1",
    "nodeDeallocationOption": "invalid",
    "currentDedicated": 0,
    "targetDedicated": 2,
    "enableAutoScale": false,
    "isAutoPool": false
}
```

|元素|類型|注意事項|
|-------------|----------|-----------|
|poolId|String|hello hello 集區識別碼。|
|nodeDeallocationOption|String|指定當節點可能會移除從 hello 集區中，如果 hello 集區大小減少。<br /><br /> 可能的值包括：<br /><br /> **requeue** – 終止執行中工作並重新排入佇列。 hello 作業啟用時，會再次執行 hello 工作。 一旦工作終止，隨即移除節點。<br /><br /> **terminate** – 終止執行中工作。 hello 工作不會執行一次。 一旦工作終止，隨即移除節點。<br /><br /> **taskcompletion** -允許正在執行工作 toocomplete。 等待時不排程任何新的工作。 所有工作完成時，即移除節點。<br /><br /> **Retaineddata** -允許正在執行的工作 toocomplete，然後等待所有工作的資料保留週期 tooexpire。 等待時不排程任何新的工作。 當所有工作保留期到期時即移除節點。<br /><br /> hello 預設值為重新排入佇列。<br /><br /> 如果 hello 集區大小增加，則 hello 值會設定太**無效**。|
|currentDedicated|Int32|hello 的運算節點數目目前已指派 toohello 集區。|
|targetDedicated|Int32|hello hello 集區要求的運算節點數目。|
|enableAutoScale|Bool|指定是否 hello 集區大小會自動調整一段時間。|
|isAutoPool|Bool|指定是否已透過作業的 AutoPool 機制建立 hello 集區。|
