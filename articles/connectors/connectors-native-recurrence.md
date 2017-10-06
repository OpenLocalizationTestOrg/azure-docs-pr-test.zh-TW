---
title: "aaaAdd hello 循環觸發程序中的 logic apps |Microsoft 文件"
description: "Hello 循環觸發程序的概觀以及如何 toouse 它與 Azure 邏輯應用程式。"
services: 
documentationcenter: 
author: jeffhollan
manager: erikre
editor: 
tags: connectors
ms.assetid: 51dd4f22-7dc5-41af-a0a9-e7148378cd50
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2016
ms.author: jehollan
ms.openlocfilehash: e7c625c382a88a1e7cdfff4ddc0caf55727232bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-recurrence-trigger"></a>開始使用 hello 循環觸發程序
藉由使用 hello 循環觸發程序，您可以建立功能強大的工作流程 hello 雲端中。

例如，您可以：

* 每日排程工作流程 toorun SQL 預存程序。
* 電子郵件傳送 hello 特定說明有關過去一週內的所有推文的摘要。

tooget 開始使用 hello 循環觸發程序，在邏輯應用程式，請參閱[建立邏輯應用程式](../logic-apps/logic-apps-create-a-logic-app.md)。

## <a name="use-a-recurrence-trigger"></a>使用循環觸發程序
觸發程序是可以使用的 toostart hello 工作流程邏輯應用程式中所定義的事件。 [深入了解觸發程序](connectors-overview.md)。

以下是 tooset 向上循環觸發程序邏輯應用程式中的範例順序：

1. 新增 hello**循環**hello 邏輯應用程式中的第一個步驟的觸發程序。
2. Hello 參數填入 hello 循環間隔。

hello 邏輯應用程式啟動的每個間隔後執行。

![HTTP 觸發程序](./media/connectors-native-recurrence/using-trigger.png)

## <a name="trigger-details"></a>觸發程序詳細資料
hello 循環觸發程序有下列屬性，您可以設定的 hello。

它會在指定的時間間隔之後引發邏輯應用程式。
標示 * 代表必要欄位。

| 顯示名稱 | 屬性名稱 | 說明 |
| --- | --- | --- |
| 頻率 * |frequency |時間單位 hello: `Second`， `Minute`， `Hour`， `Day`，或`Year`。 |
| 間隔 * |interval |hello hello 給 hello 循環頻率間隔。 |
| 時區 |timeZone |如果提供開始時間時未指定 UTC 時差，將會使用此時區。 |
| 開始時間 |startTime |hello 的開始時間[ISO 8601 格式](https://en.wikipedia.org/wiki/ISO_8601#Combined_date_and_time_representations)。 |

<br>

## <a name="next-steps"></a>後續步驟
現在，試用 hello 平台和[建立邏輯應用程式](../logic-apps/logic-apps-create-a-logic-app.md)。 您可以瀏覽 hello 邏輯應用程式中其他可用的連接器，藉由查看我們[Api 清單](apis-list.md)。

