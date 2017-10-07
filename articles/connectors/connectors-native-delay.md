---
title: "邏輯應用程式中的延遲 aaaAdd |Microsoft 文件"
description: "Hello 概觀延遲和延遲的動作，直到以及如何 toouse 其與 Azure 邏輯應用程式。"
services: 
documentationcenter: 
author: jeffhollan
manager: erikre
editor: 
tags: connectors
ms.assetid: 915f48bf-3bd8-4656-be73-91a941d0afcd
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2016
ms.author: jehollan
ms.openlocfilehash: e5bc9d639adbddc01ee0f6a4c68716f586d4344a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-delay-and-delay-until-actions"></a>開始使用 hello 延遲，並且延遲-直到動作
使用 hello 延遲和 「 延遲-直到 」 動作，您可以完成的工作流程案例。

例如，您可以：

* 請等到工作日 toosend 狀態更新透過電子郵件。
* HTTP 呼叫的延遲 hello 工作流程有時間 toofinish 之前繼續並擷取 hello 結果。

請參閱 < 開始使用邏輯應用程式中的 hello 動作延遲 tooget[建立邏輯應用程式](../logic-apps/logic-apps-create-a-logic-app.md)。

## <a name="use-hello-delay-actions"></a>使用 hello 延遲的動作
動作是由定義在邏輯應用程式中的 hello 工作流程執行的作業。 [深入了解動作](connectors-overview.md)。

以下是如何 toouse 延遲步驟在邏輯應用程式中的範例順序：

1. 新增觸發程序後, 按一下**新步驟**tooadd 動作。
2. 搜尋**延遲**toobring 向上 hello 延遲的動作。 在此範例中，我們將會選取 [延遲] 。
   
    ![延遲動作](./media/connectors-native-delay/using-action-1.png)
3. 完成所有 hello 動作屬性 tooconfigure hello 延遲。
   
    ![延遲設定](./media/connectors-native-delay/using-action-2.png)
4. 按一下**儲存**toopublish 並啟用 hello 邏輯應用程式。

## <a name="action-details"></a>動作詳細資料
hello 循環觸發程序有下列屬性可設定的 hello。

### <a name="delay-action"></a>延遲動作
針對一段時間間隔執行此動作的延遲 hello。
標示 * 代表必要欄位。

| 顯示名稱 | 屬性名稱 | 說明 |
| --- | --- | --- |
| 計數 * |計數 |時間單位 toodelay 的 hello 數目 |
| 單位 * |unit |時間單位 hello: `Second`， `Minute`， `Hour`，或`Day` |

<br>

### <a name="delay-until-action"></a>延遲直到動作
這個動作會延遲到指定的日期/時間執行的 hello。
標示 * 代表必要欄位。

| 顯示名稱 | 屬性名稱 | 說明 |
| --- | --- | --- |
| 年 * |timestamp |(GMT) 直到 hello 年 toodelay |
| 月 * |timestamp |(GMT) 直到 hello 月份 toodelay |
| 日 * |timestamp |(GMT) 直到 hello 天 toodelay |

<br>

## <a name="next-steps"></a>後續步驟
現在，試用 hello 平台和[建立邏輯應用程式](../logic-apps/logic-apps-create-a-logic-app.md)。 您可以瀏覽 hello 邏輯應用程式中其他可用的連接器，藉由查看我們[Api 清單](apis-list.md)。

