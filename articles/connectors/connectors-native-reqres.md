---
title: "aaaUse 要求和回應動作 |Microsoft 文件"
description: "Hello 要求和回應觸發程序和動作中的 Azure 邏輯應用程式概觀"
services: 
documentationcenter: 
author: jeffhollan
manager: erikre
editor: 
tags: connectors
ms.assetid: 566924a4-0988-4d86-9ecd-ad22507858c0
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2016
ms.author: jehollan
ms.openlocfilehash: 24c378cc12d5f3f65116d5e59278236186a99662
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-request-and-response-components"></a>開始使用 hello 要求和回應的元件
Hello 要求和回應中元件的邏輯應用程式，您可以在即時 tooevents 回覆。

例如，您可以：

* 從內部部署的資料庫邏輯應用程式透過回應 tooan 含有資料的 HTTP 要求。
* 從外部 Webhook 事件觸發邏輯應用程式。
* 從另一個邏輯應用程式內使用要求和回應動作呼叫邏輯應用程式。

請參閱 < 開始使用邏輯應用程式中的 hello 要求和回應動作的 tooget[建立邏輯應用程式](../logic-apps/logic-apps-create-a-logic-app.md)。

## <a name="use-hello-http-request-trigger"></a>使用 hello HTTP 要求的觸發程序
觸發程序是可以使用的 toostart hello 工作流程邏輯應用程式中所定義的事件。 [深入了解觸發程序](connectors-overview.md)。

以下是如何設定 HTTP tooset 要求 hello 邏輯應用程式的設計工具中的範例順序。

1. 加入 hello 觸發程序**要求-當 HTTP 要求**邏輯應用程式中。 您可以選擇性地提供 JSON 結構描述 (使用這類工具[JSONSchema.net](http://jsonschema.net)) hello 要求主體。 這可以讓 hello HTTP 要求內容的 hello 設計工具 toogenerate 權杖。
2. 加入另一個動作，讓您可以將儲存 hello 邏輯應用程式。
3. 在儲存之後 hello 邏輯應用程式，您可以從 hello 要求卡取得 hello HTTP 要求的 URL。
4. HTTP POST (您可以使用這類工具[郵差](https://www.getpostman.com/)) toohello URL 觸發程序 hello 邏輯應用程式。

> [!NOTE]
> 如果您未定義的回應動作， `202 ACCEPTED` toohello 呼叫立即傳回回應。 您可以使用 hello 回應動作 toocustomize 回應。
> 
> 

![回應觸發程序](./media/connectors-native-reqres/using-trigger.png)

## <a name="use-hello-http-response-action"></a>使用 hello HTTP 回應動作
當您使用的 HTTP 要求所觸發工作流程中才有效 hello HTTP 回應的動作。 如果您未定義的回應動作， `202 ACCEPTED` toohello 呼叫立即傳回回應。  您可以加入回應動作的 hello 工作流程內的任何步驟。 hello 邏輯應用程式只會保留 hello 連入要求開啟之回應的一分鐘。  在一分鐘，如果沒有回應傳送 hello 工作流程 （和回應動作存在 hello 定義中） 後,`504 GATEWAY TIMEOUT`傳回 toohello 呼叫端。

以下是如何 tooadd HTTP 回應動作：

1. 選取 hello**新步驟** 按鈕。
2. 選擇 [新增動作] 。
3. 在 hello 動作搜尋方塊中，輸入**回應**toolist hello 回應動作。
   
    ![選取 hello 回應動作](./media/connectors-native-reqres/using-action-1.png)
4. 新增任何所需的 hello HTTP 回應訊息的參數。
   
    ![完整的 hello 回應動作](./media/connectors-native-reqres/using-action-2.png)
5. 按一下 hello 左上角 hello 工具列 toosave 和您邏輯應用程式會同時將儲存並發行 （啟動）。

## <a name="request-trigger"></a>要求觸發程序
以下是 hello hello 觸發程序，此連接器支援的詳細資料。 只有一個要求觸發程序。

| 觸發程序 | 說明 |
| --- | --- |
| 要求 |收到 HTTP 要求時發生 |

## <a name="response-action"></a>回應動作
以下是此連接器支援的 hello 動作的 hello 詳細資料。 只有一個回應動作，此動作只能在伴隨要求觸發程序時使用。

| 動作 | 說明 |
| --- | --- |
| Response |傳回回應 toohello 相互關聯的 HTTP 要求 |

### <a name="trigger-and-action-details"></a>觸發程序和動作詳細資料
hello 下列資料表描述 hello 輸入的欄位 hello 觸發程序和動作，並 hello 對應的輸出詳細資料。

#### <a name="request-trigger"></a>要求觸發程序
hello 以下是 hello 觸發程序，從傳入的 HTTP 要求的輸入的欄位。

| 顯示名稱 | 屬性名稱 | 說明 |
| --- | --- | --- |
| JSON 結構描述 |結構描述 |hello hello HTTP 要求主體的 JSON 結構描述 |

<br>

**輸出詳細資料**

hello 如下 hello 要求的輸出詳細資料。

| 屬性名稱 | 資料類型 | 說明 |
| --- | --- | --- |
| headers |物件 |要求標頭 |
| 內文 |物件 |要求物件 |

#### <a name="response-action"></a>回應動作
hello 如下 hello HTTP 回應動作的輸入的欄位。 標示 * 代表必要欄位。

| 顯示名稱 | 屬性名稱 | 說明 |
| --- | --- | --- |
| 狀態碼 * |StatusCode |hello HTTP 狀態碼 |
| headers |headers |JSON 物件的任何回應標頭 tooinclude |
| 內文 |body |hello 回應主體 |

## <a name="next-steps"></a>後續步驟
現在，試用 hello 平台和[建立邏輯應用程式](../logic-apps/logic-apps-create-a-logic-app.md)。 您可以瀏覽 hello 邏輯應用程式中其他可用的連接器，藉由查看我們[Api 清單](apis-list.md)。

