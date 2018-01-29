---
title: "Durable Functions 中的函式鏈結 - Azure"
description: "了解如何執行 Durable Functions 範例來執行一連串的函式。"
services: functions
author: cgillum
manager: cfowler
editor: 
tags: 
keywords: 
ms.service: functions
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 09/29/2017
ms.author: azfuncdf
ms.openlocfilehash: 9ba1cdc5c72e04802d29794fa6cb40a29cc1d353
ms.sourcegitcommit: a48e503fce6d51c7915dd23b4de14a91dd0337d8
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/05/2017
---
# <a name="function-chaining-in-durable-functions---hello-sequence-sample"></a>Durable Functions 中的函式鏈結- Hello 序列範例

函式鏈結是指以特定順序執行一連串函式的模式。 通常，一個函式的輸出必須套用至另一個函式的輸入。 本文以一個範例說明如何使用 [Durable Functions](durable-functions-overview.md) 來實作函式鏈結。

## <a name="prerequisites"></a>必要條件

* 請依照[安裝 Durable Functions](durable-functions-install.md) 中的指示來設定範例。

## <a name="the-functions"></a>函式

本文說明範例應用程式中的函式如下：

* `E1_HelloSequence`：此協調器函式連續呼叫 `E1_SayHello` 多次。 它會儲存 `E1_SayHello` 呼叫的輸出，並記錄結果。
* `E1_SayHello`：此活動函式在字串前面加上 "Hello"。

下列各節說明用於 Azure 入口網站開發的設定和程式碼。 適用於 Visual Studio 開發的程式碼顯示在本文結尾。
 
## <a name="functionjson-file"></a>function.json 檔案

如果您使用 Visual Studio Code 或 Azure 入口網站進行開發，以下是適用於協調器函式的 *function.json* 檔案內容。 大部分協調器 *function.json* 檔案看起來幾乎完全像這樣。

[!code-json[Main](~/samples-durable-functions/samples/csx/E1_HelloSequence/function.json)]

重要的是 `orchestrationTrigger` 繫結類型。 所有協調器函式必須都使用此觸發程序類型。

> [!WARNING]
> 為了遵守協調器函式的「沒有 I/O」規則，當您使用 `orchestrationTrigger` 觸發程序繫結時，請勿使用任何輸入或輸出繫結。  如果需要其他輸入或輸出繫結，請改為在協調器所呼叫之 `activityTrigger` 函式的內容中使用。

## <a name="c-script-visual-studio-code-and-azure-portal-sample-code"></a>C# 指令碼 (Visual Studio Code 和 Azure 入口網站範例程式碼) 

以下是原始程式碼：

[!code-csharp[Main](~/samples-durable-functions/samples/csx/E1_HelloSequence/run.csx)]

所有 C# 協調流程函式都必須有 `DurableOrchestrationContext` 類型的參數 (在 `Microsoft.Azure.WebJobs.Extensions.DurableTask` 組件中)。 如果您使用 C# 指令碼，請利用 `#r` 標記法來參考此組件。 此內容物件可讓您使用其 [CallActivityAsync](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.DurableOrchestrationContext.html#Microsoft_Azure_WebJobs_DurableOrchestrationContext_CallActivityAsync_) 方法來呼叫其他「活動」函式並傳遞輸入參數。

程式碼中以不同的參數值連續呼叫 `E1_SayHello` 三次。 每次呼叫的傳回值會新增至函式最後傳回的 `outputs` 清單。

活動函式 `E1_SayHello` 和 `E1_HelloSequence`的 *function.json*檔案很類似，差別在於前者使用 `activityTrigger` 繫結型別，而不是 `orchestrationTrigger` 繫結型別。

[!code-json[Main](~/samples-durable-functions/samples/csx/E1_SayHello/function.json)]

> [!NOTE]
> 協調流程函式所呼叫的任何函式必須使用 `activityTrigger` 繫結。

`E1_SayHello` 的實作是相當簡單的字串格式化作業。

[!code-csharp[Main](~/samples-durable-functions/samples/csx/E1_SayHello/run.csx)]

此函式具有 [DurableActivityContext](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.DurableActivityContext.html) 類型的參數，其會使用此參數來取得協調器函式呼叫 [`CallActivityAsync<T>`](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.DurableOrchestrationContext.html#Microsoft_Azure_WebJobs_DurableOrchestrationContext_CallActivityAsync_) 時所傳回的輸入。

## <a name="run-the-sample"></a>執行範例

若要執行 `E1_HelloSequence` 協調流程，請傳送下列 HTTP POST 要求。

```
POST http://{host}/orchestrators/E1_HelloSequence
```

例如，如果您在名為 "myfunctionapp" 的函式應用程式中執行範例，請將 "{host}" 取代為 "myfunctionapp.azurewebsites.net"。

結果會是 HTTP 202 回應，就像這樣 (為了簡潔起見已修剪)：

```
HTTP/1.1 202 Accepted
Content-Length: 719
Content-Type: application/json; charset=utf-8
Location: http://{host}/admin/extensions/DurableTaskExtension/instances/96924899c16d43b08a536de376ac786b?taskHub=DurableFunctionsHub&connection=Storage&code={systemKey}

(...trimmed...)
```

現在，協調流程已排入佇列，並立即開始執行。 `Location` 標頭中的 URL 可以用來檢查執行的狀態。

```
GET http://{host}/admin/extensions/DurableTaskExtension/instances/96924899c16d43b08a536de376ac786b?taskHub=DurableFunctionsHub&connection=Storage&code={systemKey}
```

結果會是協調流程的狀態。 執行和完成都很快速，您會看到 *Completed* 狀態，而且回應看起來像這樣 (為了簡潔起見已修剪)：

```
HTTP/1.1 200 OK
Content-Length: 179
Content-Type: application/json; charset=utf-8

{"runtimeStatus":"Completed","input":null,"output":["Hello Tokyo!","Hello Seattle!","Hello London!"],"createdTime":"2017-06-29T05:24:57Z","lastUpdatedTime":"2017-06-29T05:24:59Z"}
```

如您所見，執行個體的 `runtimeStatus` 是 *Completed*，而 `output` 包含協調器函式執行的 JSON 序列化結果。

> [!NOTE]
> 在範例應用程式中，啟動協調器函式的 HTTP POST 端點是以名為 "HttpStart" 的 HTTP 觸發程序函式實作。 您可以對其他觸發程序類型實作類似的起始邏輯，例如 `queueTrigger`、`eventHubTrigger` 或 `timerTrigger`。

查看函式執行記錄。 由於[概觀](durable-functions-overview.md)中所述的重新執行行為，`E1_HelloSequence` 函式會啟動並完成多次。 相反地，`E1_SayHello` 只執行三次，因為這幾次函式執行不會再來一次。

## <a name="visual-studio-sample-code"></a>Visual Studio 範例程式碼

以下是 Visual Studio 專案中的單一 C# 檔案所示範的協調流程：

[!code-csharp[Main](~/samples-durable-functions/samples/precompiled/HelloSequence.cs)]

## <a name="next-steps"></a>後續步驟

此範例已示範簡單的函式鏈結協調流程。 下一個範例會說明如何實作展開傳送/收合傳送模式。 

> [!div class="nextstepaction"]
> [執行展開傳送/收合傳送範例](durable-functions-cloud-backup.md)
