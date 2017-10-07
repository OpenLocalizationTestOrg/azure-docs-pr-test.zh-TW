---
title: "aaaCustom Azure 邏輯應用程式與 Azure 函式的程式碼 |Microsoft 文件"
description: "使用 Azure Functions 建立並執行適用於 Azure Logic Apps 的自訂程式碼"
services: logic-apps,functions
documentationcenter: .net,nodejs,java
author: jeffhollan
manager: anneta
editor: 
ms.assetid: 9fab1050-cfbc-4a8b-b1b3-5531bee92856
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.custom: H1Hack27Feb2017
ms.date: 10/18/2016
ms.author: LADocs; jehollan
ms.openlocfilehash: 18b3821ed7e434feb568b9b96e9a5a2189dba3bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="add-and-run-custom-code-for-logic-apps-through-azure-functions"></a>透過 Azure Functions 新增並執行適用於 Logic Apps 的自訂程式碼

toorun 自訂程式碼片段的 C# 或 node.js 邏輯應用程式中的，您可以建立自訂函式，透過 Azure 函式。 
[Azure Functions](../azure-functions/functions-overview.md) 提供 Microsoft Azure 中無伺服器運算的功能，並有助於執行下列工作：

* 邏輯應用程式中欄位的進階格式設定或計算
* 在工作流程中執行計算。
* 擴充功能，支援以 C# 或 node.js 的 hello 邏輯應用程式的功能

## <a name="create-custom-functions-for-your-logic-apps"></a>建立邏輯應用程式的自訂函式

我們建議您建立函式可在 hello Azure 函式的入口網站，從 hello**泛型 Webhook-節點**或**泛型 Webhook-C#**範本。 hello 結果建立自動填入內容的範本接受`application/json`從邏輯應用程式。 您從這些範本建立的函式會自動偵測，而且會在邏輯應用程式的設計工具出現在 hello **Azure 函式在我的區域。**

Hello hello 上的 Azure 入口網站中**整合**窗格為您的函式中，您的範本應該會顯示**模式**設定得**Webhook**和**Webhook 類型**設定得**泛型 JSON**。 

Webhook 函式接受要求，並將它傳遞到 hello 方法，透過`data`變數。 您可以使用點標記法，例如存取承載 hello 屬性`data.function-name`。 例如，簡單的 JavaScript 函式，將日期時間值轉換成日期字串看起來像下列範例中的 hello:

```
function start(req, res){
    var data = req.body;
    res = {
        body: data.date.ToDateString();
    }
}
```

## <a name="call-azure-functions-from-logic-apps"></a>從 Logic Apps 呼叫 Azure Functions

在您的訂用帳戶和您想 toocall，在邏輯應用程式設計師中，選取的 hello 函式的 toolist hello 容器按一下 hello**動作**功能表，然後選取從**Azure 函式在我的區域**。

您選取 hello 函式之後，您就詢問 toospecify 輸入的裝載物件。 此物件是 hello 邏輯應用程式傳送 toohello 函式，而且必須是 JSON 物件的 hello 訊息。 例如，如果您想要在 hello toopass**上次修改**日期 Salesforce 觸發程序，從 hello 函式的內容可能類似下列範例：

![上次修改日期][1]

## <a name="trigger-logic-apps-from-a-function"></a>從函數觸發 Logic Apps

您可以從函式內部觸發邏輯應用程式。 請參閱[做為可呼叫端點的邏輯應用程式](logic-apps-http-endpoint.md)。 建立了手動觸發程序邏輯應用程式，然後從您的函式內產生且您想要傳送 toohello 邏輯應用程式的 hello 承載 HTTP POST toohello 手動觸發程序 URL。

### <a name="create-a-function-from-logic-app-designer"></a>從邏輯應用程式設計工具建立函式

您也可以從 hello 設計工具建立 node.js webhook 函式。 首先，選取 [我的區域中的 Azure Functions]  ，然後選擇適用於您的函數的容器。 如果您還沒有容器，您需要從 hello 一個 toocreate [Azure 函式的入口網站](https://functions.azure.com/signin)。 然後選取 建立新的) 。  

toogenerate 想 toocompute，hello 資料為基礎的範本會指定您計劃 toopass 到函式的 hello 內容物件。 這個物件必須是 JSON 物件。 比方說，如果您從 FTP 動作傳入 hello 檔案內容，hello 內容承載看起來像本範例中：

![內容承載][2]

> [!NOTE]
> 因為此物件未轉換為字串，hello 的內容新增直接 toohello JSON 裝載。 不過，如果 hello 物件不是 JSON 權杖 （也就是字串或 JSON 物件/陣列），就會發生錯誤。 本文章中的 hello 第一個圖例中所示，toocast hello 物件做為字串，加上引號。
> 

hello 設計工具會產生您可以建立內嵌函式樣板。 變數會預先建立根據您計劃 toopass hello 函式的 hello 內容。

<!--Image references-->
[1]: ./media/logic-apps-azure-functions/callfunction.png
[2]: ./media/logic-apps-azure-functions/createfunction.png
