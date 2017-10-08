---
title: "中的 logic apps aaaAdd hello 查詢動作 |Microsoft 文件"
description: "Hello 查詢動作執行動作篩選條件陣列類似的概觀。"
services: 
documentationcenter: 
author: jeffhollan
manager: erikre
editor: 
tags: connectors
ms.assetid: 34e702c7-f9e5-4885-9266-fc7404adecfe
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/20/2016
ms.author: jehollan
ms.openlocfilehash: 3d4be901e7e6bf1b644057648930667ab34f2124
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-query-action"></a>開始使用 hello 查詢動作
藉由使用 hello 查詢動作，您可以使用批次和陣列 tooaccomplish 的工作流程：

* 從資料庫建立所有高優先順序記錄的工作。
* 將電子郵件的所有 PDF 附件儲存到 Azure Blob。

請參閱 < 開始使用邏輯應用程式中的 hello 查詢動作 tooget[建立邏輯應用程式](../logic-apps/logic-apps-create-a-logic-app.md)。

## <a name="use-hello-query-action"></a>使用 hello 查詢動作
動作是由定義在邏輯應用程式中的 hello 工作流程執行的作業。 [深入了解動作](connectors-overview.md)。  

目前的 hello 查詢動作都有一個稱為 hello 篩選陣列、 在 hello 設計工具中公開的作業。 這可讓您 tooquery 陣列並傳回一組的篩選結果。

以下說明如何將它新增至邏輯應用程式︰

1. 選取 hello**新步驟** 按鈕。
2. 選擇 [新增動作] 。
3. 在 hello 動作搜尋方塊中，輸入**篩選**toolist hello**篩選陣列**動作。
   
    ![選取 hello 查詢動作](./media/connectors-native-query/using-action-1.png)
4. 選取陣列 toofilter。 （hello 下列螢幕擷取畫面顯示 hello Twitter 搜尋結果陣列）。
5. 建立條件 tooevaluate 上每個項目。 （下列螢幕擷取畫面的 hello 篩選具有 100 個以上的實行項目之使用者的推文）。
   
    ![完整的 hello 查詢動作](./media/connectors-native-query/using-action-2.png)
   
    hello 動作會輸出新的陣列，其中包含符合 hello 篩選需求的結果。
6. 按一下 hello 左上角 hello 工具列 toosave 和您邏輯應用程式會同時將儲存並發行 （啟動）。

## <a name="query-action"></a>查詢動作
以下是此連接器支援的 hello 動作的 hello 詳細資料。 hello 連接器有一個可能的動作。

| 動作 | 說明 |
| --- | --- |
| 篩選陣列 |評估的條件陣列中每個項目，並傳回 hello 結果 |

## <a name="action-details"></a>動作詳細資料
hello 查詢動作隨附一個可能的動作。 hello 下列表格說明必要的 hello 與 hello 動作和 hello 對應輸出的詳細資料與使用 hello 動作相關聯的選擇性輸入的欄位。

### <a name="filter-array"></a>篩選陣列
hello 如下 hello 動作，使外送 HTTP 要求的輸入的欄位。
標示 * 代表必要欄位。

| 顯示名稱 | 屬性名稱 | 說明 |
| --- | --- | --- |
| 從* |from |hello 陣列 toofilter |
| 條件* |其中 |hello 條件 tooevaluate 每個項目 |

<br>

### <a name="output-details"></a>輸出詳細資料
hello 以下是輸出 hello HTTP 回應的詳細資料。

| 屬性名稱 | 資料類型 | 說明 |
| --- | --- | --- |
| 篩選的陣列 |array |陣列，其中包含每筆篩選結果的物件 |

## <a name="next-steps"></a>後續步驟
現在，試用 hello 平台和[建立邏輯應用程式](../logic-apps/logic-apps-create-a-logic-app.md)。 您可以瀏覽 hello 邏輯應用程式中其他可用的連接器，藉由查看我們[Api 清單](apis-list.md)。

