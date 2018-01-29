---
title: "Durable Functions 概觀 - Azure (預覽)"
description: "Azure Functions 的 Durable Functions 擴充簡介。"
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
ms.openlocfilehash: f1def2a43edee58bc8b5a33880e206130a1b4687
ms.sourcegitcommit: 3f33787645e890ff3b73c4b3a28d90d5f814e46c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/03/2018
---
# <a name="durable-functions-overview-preview"></a>Durable Functions 概觀 (預覽)

*Durable Functions* 是 [Azure Functions](functions-overview.md) 和 [Azure WebJobs](../app-service/web-sites-create-web-jobs.md) 的擴充功能，可讓您在無伺服器環境中撰寫具狀態函式。 此擴充功能會為您管理狀態、設定檢查點和重新啟動。

此擴充功能可讓您以新的函式類型 (稱為「協調器函式」) 定義具狀態的工作流程。 以下是協調器函式的一些優點：

* 協調器函式會在程式碼中定義工作流程。 不需要 JSON 結構描述或設計工具。
* 協調器函式能以同步和非同步方式呼叫其他函式。 所呼叫之函式的輸出可儲存至本機變數。
* 協調器函式每次在進行等候時，都會自動設定其進度的檢查點。 如果處理序回收或 VM 重新開機，本機狀態永遠不會消失。

> [!NOTE]
> 處於預覽狀態的 Durable Functions 是 Azure Functions 的進階擴充功能，並非所有應用程式都適用。 本文其餘部分會假設您已非常熟悉無伺服器應用程式開發過程中所涉及的 [Azure Functions](functions-overview.md) 概念和挑戰。

Durable Functions 主要用來簡化無伺服器應用程式中複雜的具狀態協調問題。 下列各節會說明一些可因為 Durable Functions 而受益的典型應用程式模式。

## <a name="pattern-1-function-chaining"></a>模式 #1：函式鏈結

「函式鏈結」是指以特定順序執行一系列函式的模式。 一個函式的輸出通常必須套用到另一個函式的輸入。

![函式鏈結圖](media/durable-functions-overview/function-chaining.png)

Durable Functions 可讓您利用程式碼簡潔地實作此模式。

```cs
public static async Task<object> Run(DurableOrchestrationContext ctx)
{
    try
    {
        var x = await ctx.CallActivityAsync<object>("F1");
        var y = await ctx.CallActivityAsync<object>("F2", x);
        var z = await ctx.CallActivityAsync<object>("F3", y);
        return  await ctx.CallActivityAsync<object>("F4", z);
    }
    catch (Exception)
    {
        // error handling/compensation goes here
    }
}
```

"F1"、"F2"、"F3" 和 "F4" 是函式應用程式中其他函式的名稱。 控制流程可使用一般的命令式編碼建構來加以實作。 也就是說，程式碼會由上而下地執行，並可包含現有語言的控制流程語意，例如條件和迴圈。  錯誤處理邏輯則可包含在 try/catch/finally 區塊中。

`ctx` 參數 ([DurableOrchestrationContext](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.DurableOrchestrationContext.html)) 可提供方法來依名稱叫用其他函式、傳遞參數以及傳回函式的輸出。 每當程式碼呼叫 `await` 時，Durable Functions 架構便會對目前函式執行個體的進度「設定檢查點」。 如果處理序或 VM 在執行途中回收，函式執行個體便會從先前的 `await` 呼叫繼續執行。 之後會有更多關於此重新啟動行為的資訊。

## <a name="pattern-2-fan-outfan-in"></a>模式 #2：展開傳送/收合傳送

「展開傳送/收合傳送」是指以平行方式執行多個函式，然後等候所有函式完成的模式。  某些彙總工作通常會在函式傳回結果時執行。

![展開傳送/收合傳送圖](media/durable-functions-overview/fan-out-fan-in.png)

在標準函式中，可藉由讓函式傳送多個訊息給佇列來進行展開傳送。 不過，反過來的收合傳送則困難得多。 您必須撰寫程式碼來追蹤佇列所觸發的函式何時結束，並儲存函式的輸出。 Durable Functions 擴充功能會以較簡單的程式碼處理此模式。

```cs
public static async Task Run(DurableOrchestrationContext ctx)
{
    var parallelTasks = new List<Task<int>>();
 
    // get a list of N work items to process in parallel
    object[] workBatch = await ctx.CallActivityAsync<object[]>("F1");
    for (int i = 0; i < workBatch.Length; i++)
    {
        Task<int> task = ctx.CallActivityAsync<int>("F2", workBatch[i]);
        parallelTasks.Add(task);
    }
 
    await Task.WhenAll(parallelTasks);
 
    // aggregate all N outputs and send result to F3
    int sum = parallelTasks.Sum(t => t.Result);
    await ctx.CallActivityAsync("F3", sum);
}
```

展開傳送工作會分派給 `F2` 函式的多個執行個體，並使用動態工作清單來追蹤該工作。 系統會呼叫 .NET `Task.WhenAll` API 來等候所有已呼叫的函式完成。 然後，`F2` 函式的輸出會從動態工作清單彙總起來並傳遞給 `F3` 函式。

在 `Task.WhenAll` 的 `await` 呼叫發生的自動設定檢查點作業，可確保任何中途當機或重新開機不需要重新啟動任何已完成的工作。

## <a name="pattern-3-async-http-apis"></a>模式 #3：非同步的 HTTP API

第三個模式全都是關於協調外部用戶端之長時間執行作業狀態的問題。 此模式常見的實作方法是讓 HTTP 呼叫觸發長時間執行的動作，然後將用戶端重新導向至可供它們進行輪詢以在作業完成時得知消息的狀態端點。

![HTTP API 圖表](media/durable-functions-overview/async-http-api.png)

Durable Functions 會提供內建 API，以簡化您所撰寫來與長時間執行之函式執行互動的程式碼。 [範例](durable-functions-install.md)所顯示的是簡單的 REST 命令，此命令可用來啟動新的協調器函式執行個體。 一旦有執行個體啟動，擴充功能就會公開 Webhook HTTP API 來查詢協調器函式的狀態。 下列範例顯示的是 REST 命令，這些命令可用來啟動協調器，以及查詢其狀態。 為了清楚起見，此範例中省略了部分詳細資料。

```
> curl -X POST https://myfunc.azurewebsites.net/orchestrators/DoWork -H "Content-Length: 0" -i
HTTP/1.1 202 Accepted
Content-Type: application/json
Location: https://myfunc.azurewebsites.net/admin/extensions/DurableTaskExtension/b79baf67f717453ca9e86c5da21e03ec

{"id":"b79baf67f717453ca9e86c5da21e03ec", ...}

> curl https://myfunc.azurewebsites.net/admin/extensions/DurableTaskExtension/b79baf67f717453ca9e86c5da21e03ec -i
HTTP/1.1 202 Accepted
Content-Type: application/json
Location: https://myfunc.azurewebsites.net/admin/extensions/DurableTaskExtension/b79baf67f717453ca9e86c5da21e03ec

{"runtimeStatus":"Running","lastUpdatedTime":"2017-03-16T21:20:47Z", ...}

> curl https://myfunc.azurewebsites.net/admin/extensions/DurableTaskExtension/b79baf67f717453ca9e86c5da21e03ec -i
HTTP/1.1 200 OK
Content-Length: 175
Content-Type: application/json

{"runtimeStatus":"Completed","lastUpdatedTime":"2017-03-16T21:20:57Z", ...}
```

狀態是由 Durable Functions 執行階段所管理，因此您不必實作自己的狀態追蹤機制。

即使 Durable Functions 擴充功能有內建 Webhook 可管理長時間執行的協調流程，您仍可使用您自己的函式觸發程序 (例如 HTTP、佇列或事件中樞) 和 `orchestrationClient` 繫結來自行實作此模式。 例如，您可以使用佇列訊息來觸發終止。  或者，您可以使用由 Azure Active Directory 驗證原則保護的 HTTP 觸發程序，而不是使用內建的 Webhook (使用產生的金鑰進行驗證)。 

```cs
// HTTP-triggered function to start a new orchestrator function instance.
public static async Task<HttpResponseMessage> Run(
    HttpRequestMessage req,
    DurableOrchestrationClient starter,
    string functionName,
    TraceWriter log)
{
    // Function name comes from the request URL.
    // Function input comes from the request content.
    dynamic eventData = await req.Content.ReadAsAsync<object>();
    string instanceId = await starter.StartNewAsync(functionName, eventData);
    
    log.Info($"Started orchestration with ID = '{instanceId}'.");
    
    return starter.CreateCheckStatusResponse(req, instanceId);
}
```

[DurableOrchestrationClient](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.DurableOrchestrationClient.html) `starter` 參數是來自 `orchestrationClient` 輸出繫結 (此繫結是 Durable Functions 擴充功能的一部分) 的值。 它可提供方法來啟動、終止、和查詢新的或現有的協調器函式執行個體，以及對其傳送事件。 在上述範例中，HTTP 所觸發的函式會從傳入 URL 取得 `functionName` 值，並將該值傳遞到 [StartNewAsync](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.DurableOrchestrationClient.html#Microsoft_Azure_WebJobs_DurableOrchestrationClient_StartNewAsync_)。 這個繫結 API 接著會傳回回應，回應中包含了 `Location` 標頭和其他有關執行個體的資訊，以在稍後用來查詢已啟動之執行個體的狀態或將該執行個體終止。

## <a name="pattern-4-stateful-singletons"></a>模式 #4：具狀態 Singleton

大部分函式都有明確的開始和結束，而不會直接與外部事件來源互動。 不過，協調流程所支援的[具狀態 Singleton](durable-functions-singletons.md) 模式則可讓協調流程的行為類似分散式運算中的可靠[動作項目](https://en.wikipedia.org/wiki/Actor_model)。

下圖所說明的函式，會在處理從外部來源所接收的事件時，於無限迴圈中執行。

![具狀態 Singleton 圖表](media/durable-functions-overview/stateful-singleton.png)

Durable Functions 雖非動作項目模型的實作，但協調器函式的確具有許多相同的執行階段特性。 例如，它們會長時間執行 (可能永無止盡)、具狀態、可靠、具單一執行緒、位置透明，且可全域定址。 這會讓協調器函式適用於「動作項目」之類的案例。

一般函式並無狀態，因此不適合用來實作具狀態 Singleton 模式。 不過，Durable Functions 擴充功能可讓具狀態 Singleton 模式的實作變得相對簡單。 下列程式碼是簡單的協調器函式，可實作計數器。

```cs
public static async Task Run(DurableOrchestrationContext ctx)
{
    int counterState = ctx.GetInput<int>();

    string operation = await ctx.WaitForExternalEvent<string>("operation");
    if (operation == "incr")
    {
        counterState++;
    }
    else if (operation == "decr")
    {
        counterState--;
    }

    ctx.ContinueAsNew(counterState);
}
```

您可能會將此程式碼描述為「外部協調流程」&mdash;也就是說，一旦開始就永不結束。 它會執行下列步驟：

* 在 `counterState` 中輸入值來開始。
* 無限期地等候稱為 `operation` 的訊息。
* 執行某些邏輯以更新其本機狀態。
* 呼叫 `ctx.ContinueAsNew` 以自行「重新啟動」。
* 再次無限期地等候下一次作業。

## <a name="pattern-5-human-interaction"></a>模式 #5：人為互動

許多程序都會牽涉到某種類型的人為互動。 自動化程序卻需人為涉入的弔詭之處在於，人無法像雲端服務一樣隨時有空能夠回應。 自動化程序卻必須如此，其作法往往是使用逾時和補償邏輯。

核准程序便是需要人為互動的其中一個商務程序範例。 例如，超過特定金額的費用報告就可能需要管理員核准。 如果管理員未在 72 小時內核准 (可能是放假了)，系統就會啟動向上呈報程序，以尋求其他人的核准 (或許是管理員的管理員)。

![人為互動圖](media/durable-functions-overview/approval.png)

使用協調器函式即可實作此模式。 協調器會使用[長期計時器](durable-functions-timers.md)來要求核准，並在逾時後向上呈報。 它會等候[外部事件](durable-functions-external-events.md)，例如某些人為互動所產生的通知。

```cs
public static async Task Run(DurableOrchestrationContext ctx)
{
    await ctx.CallActivityAsync("RequestApproval");
    using (var timeoutCts = new CancellationTokenSource())
    {
        DateTime dueTime = ctx.CurrentUtcDateTime.AddHours(72);
        Task durableTimeout = ctx.CreateTimer(dueTime, timeoutCts.Token);

        Task<bool> approvalEvent = ctx.WaitForExternalEvent<bool>("ApprovalEvent");
        if (approvalEvent == await Task.WhenAny(approvalEvent, durableTimeout))
        {
            timeoutCts.Cancel();
            await ctx.CallActivityAsync("ProcessApproval", approvalEvent.Result);
        }
        else
        {
            await ctx.CallActivityAsync("Escalate");
        }
    }
}
```

呼叫 `ctx.CreateTimer` 即可建立長期計時器。 通知則由 `ctx.WaitForExternalEvent` 接收。 此外，還會呼叫 `Task.WhenAny` 以決定是要向上呈報 (先發生逾時) 還是處理核准 (逾時前收到核准)。

## <a name="the-technology"></a>技術

Durable Functions 擴充功能其實是以[長期工作架構](https://github.com/Azure/durabletask)為基礎所建置的，長期工作架構是 GitHub 上的開放原始碼程式庫，可用來建置長期工作協調流程。 Azure Functions 是 Azure WebJobs 的無伺服器演化，極為類似的是，Durable Functions 也是長期工作架構的無伺服器演化。 長期工作架構廣泛用於 Microsoft 內部和外部，以便自動執行任務關鍵性程序。 它天生就適合無伺服器的 Azure Functions 環境。

### <a name="event-sourcing-checkpointing-and-replay"></a>事件來源、檢查點和重新執行

協調器函式能夠使用稱為[事件來源](https://docs.microsoft.com/azure/architecture/patterns/event-sourcing)的雲端設計模式，可靠地維持其執行狀態。 長期擴充功能會使用僅限附加的存放區來記錄函式協調流程所採取的「一系列完整動作」，而不會直接儲存協調流程的「目前」狀態。 相對於「傾印」完整的執行階段狀態，這種作法有許多優點，包括提升效能、延展性及回應性。 其他優點包括為交易資料提供最終一致性，以及維持完整的稽核記錄和歷程記錄。 稽核記錄本身可啟用可靠的補償動作。

此擴充功能會透明地使用事件來源。 實際上，協調器函式中的 `await` 運算子會將協調器執行緒的控制往回產生給長期工作架構發送器。 發送器接著會將協調器函式所排程的任何新的動作 (例如，呼叫一或多個子函式或排程長期計時器) 認可至儲存體。 此透明認可動作會附加至協調流程執行個體的「執行歷程記錄」。 歷程記錄會儲存在儲存體資料表。 認可動作接著會將訊息新增至佇列以排程實際的工作。 此時，協調器函式即可從記憶體卸載。 如果您使用 Azure Functions 取用方案，則會停止其計費。  有更多工作要執行時，便會重新啟動函式，而且其狀態會重新建構。

協調流程函式在收到更多要執行的工作後 (例如，收到回應訊息或長期計時器過期)，協調器會再度甦醒，並從頭開始重新執行整個函式，以便重建本機狀態。 如果在此重新執行期間，這個程式碼嘗試呼叫函式 (或進行任何其他非同步工作)，長期工作架構便會諮詢目前協調流程的「執行歷程記錄」。 如果它發現活動函式已執行並產生某種結果，便會重新執行該函式的結果，而協調器程式碼則會繼續執行。 這種情況會繼續發生，直到函式程式碼已完成，或已排程新的非同步工作。

### <a name="orchestrator-code-constraints"></a>協調器程式碼條件約束

重新執行行為會建立可以在協調器函式撰寫之程式碼的類型條件約束。 例如，協調器程式碼必須具有確定性，因為它會重新執行多次，而且每次都必須產生相同的結果。 完整的條件約束清單可於**設定檢查點和重新啟動**一文的[協調器程式碼條件約束](durable-functions-checkpointing-and-replay.md#orchestrator-code-constraints)一節中找到。

## <a name="language-support"></a>語言支援

Durable Functions 目前僅支援 C# 語言。 這包括協調器函式和活動函式。 未來，我們會對 Azure Functions 所支援的所有語言皆新增支援。 請參閱 Azure Functions 的 [GitHub 存放庫問題清單](https://github.com/Azure/azure-functions-durable-extension/issues)，以查看其他語言支援工作的最新狀態。

## <a name="monitoring-and-diagnostics"></a>監視和診斷

持久的函式延伸模組會自動追蹤結構化的資料發出到[Application Insights](functions-monitoring.md)當函式應用程式設定為 Application Insights 檢測金鑰。 這個追蹤資料可用於監視協調流程的行為和進度。

以下是 Durable Functions 追蹤事件在使用 [Application Insights 分析](https://docs.microsoft.com/azure/application-insights/app-insights-analytics)時，於 Application Insights 入口網站中所呈現之樣貌的範例：

![App Insights 查詢結果](media/durable-functions-overview/app-insights-1.png)

有很多有用的結構化資料封裝到每個記錄項目的 `customDimensions` 欄位。 以下是某個這類項目完全展開時的範例。

![App Insights 查詢中的 customDimensions 欄位](media/durable-functions-overview/app-insights-2.png)

由於長期工作架構發送器的重新執行行為，您應該會看到重新執行的動作有重複的記錄項目。 這對於了解核心引擎的重新執行行為會有幫助。 [診斷](durable-functions-diagnostics.md)一文會說明可篩選掉重新執行記錄，以便只看到「即時」記錄的查詢範例。

## <a name="storage-and-scalability"></a>儲存體和延展性

Durable Functions 擴充功能會使用 Azure 儲存體佇列、資料表和 Blob，來保存執行歷程記錄狀態和觸發函式的執行。 您可以使用函式應用程式的預設儲存體帳戶，也可以設定不同的儲存體帳戶。 儲存體輸送量會有限制，因此您可能會想要不同的帳戶。 您所撰寫的協調器程式碼不必 (而且也不應該) 與這些儲存體帳戶中的實體互動。 這些實體會直接由長期工作架構管理，以作為實作詳細資料。

協調器函式會排程活動函式，並透過內部佇列訊息收到其回應。 當函式應用程式在 Azure Functions 取用方案中執行時，則會由 [Azure Functions 縮放控制器](functions-scale.md#how-the-consumption-plan-works)監視這些佇列，並視需要新增計算執行個體。 當相應放大為多個 VM 時，協調器函式可能會在某個 VM 上執行，其所呼叫的活動函式則在數個不同的 VM 上執行。 您可以在[效能和延展性](durable-functions-perf-and-scale.md)找到 Durable Functions 的縮放行為詳細資訊。

表格儲存體可用來儲存協調器帳戶的執行歷程記錄。 每當特定 VM 上有執行個體解除凍結時，該執行個體就會從表格儲存體擷取其執行歷程記錄，以便重建其本機狀態。 在表格儲存體中提供歷程記錄的其中一個便利之處在於，您可以使用 [Microsoft Azure 儲存體總管](https://docs.microsoft.com/azure/vs-azure-tools-storage-manage-with-storage-explorer) 之類的工具，來查看協調流程的歷程記錄。

![Azure 儲存體總管螢幕擷取畫面](media/durable-functions-overview/storage-explorer.png)

> [!WARNING]
> 雖然您可以簡單且方便地在表格儲存體中查看執行歷程記錄，但請避免對此表格建立任何相依性。 當 Durable Functions 擴充功能進化時，此相依性可能會改變。

## <a name="known-issues-and-faq"></a>已知問題和常見問題集

一般來說，[GitHub 問題](https://github.com/Azure/azure-functions-durable-extension/issues)清單中應該會追蹤所有的已知問題。 如果您遇到問題，但在 GitHub 中卻找不到此問題，請開啟新的問題，並包含問題的詳細說明。 即使您只是想要提出問題，也歡迎您開啟 GitHub 問題，並將其標記為提問。

## <a name="next-steps"></a>後續步驟

> [!div class="nextstepaction"]
> [繼續閱讀 Durable Functions 文件](durable-functions-bindings.md)

> [!div class="nextstepaction"]
> [安裝 Durable Functions 擴充功能和範例](durable-functions-install.md)

